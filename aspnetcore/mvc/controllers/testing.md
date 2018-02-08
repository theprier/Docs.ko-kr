---
title: "ASP.NET Core에서 컨트롤러 논리 테스트"
author: ardalis
description: "ASP.NET Core에서 Moq 및 xUnit로 컨트롤러 논리를 테스트하는 방법을 알아봅니다."
manager: wpickett
ms.author: riande
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: mvc/controllers/testing
ms.openlocfilehash: cabb1d2498e6c993b327c2fb9719525ec2181f9e
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="testing-controller-logic-in-aspnet-core"></a>ASP.NET Core에서 컨트롤러 논리 테스트

작성자: [Steve Smith](https://ardalis.com/)

ASP.NET MVC 앱의 컨트롤러는 크기가 작아야 하고 사용자 인터페이스 문제에 초점을 맞춰야 합니다. UI 이외의 문제를 처리하는 대형 컨트롤러는 테스트 및 유지 관리가 더 어렵습니다.

[GitHub에서 샘플 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/controllers/testing/sample)

## <a name="testing-controllers"></a>컨트롤러 테스트

컨트롤러는 모든 ASP.NET Core MVC 응용 프로그램의 핵심 요소입니다. 따라서 앱에서 의도한 대로 동작한다고 확신할 수 있어야 합니다. 자동화된 테스트를 통해 이러한 확신을 얻고 오류가 발생하기 전에 미리 검색할 수 있습니다. 컨트롤러 내에 불필요한 책임을 지우는 것을 피하고 테스트의 초점을 컨트롤러 책임으로 집중하는 것이 중요합니다.

컨트롤러 논리는 최소화되어야 하고 비즈니스 논리나 인프라 문제(예: 데이터 액세스)에 집중하면 안 됩니다. 프레임워크가 아닌 컨트롤러 논리를 테스트합니다. 유효한 입력 또는 잘못된 입력을 통해 컨트롤러의 *동작* 방식을 테스트합니다. 컨트롤러가 수행하는 비즈니스 작업의 결과를 바탕으로 컨트롤러 응답을 테스트합니다.

컨트롤러의 일반적인 책임:

* `ModelState.IsValid`를 확인합니다.
* `ModelState`가 올바르지 않으면 오류 응답을 반환합니다.
* 지속성 저장소에서 비즈니스 엔터티를 검색합니다.
* 비즈니스 엔터티에서 작업을 수행합니다.
* 보관할 비즈니스 엔터티를 저장합니다.
* 적절한 `IActionResult`를 반환합니다.

## <a name="unit-testing"></a>유닛 테스트

[단위 테스트](https://docs.microsoft.com/dotnet/articles/core/testing/unit-testing-with-dotnet-test)는 인프라 및 종속성으로부터 격리된 상태에서 앱의 일부를 테스트하는 것입니다. 컨트롤러 논리를 단위 테스트하는 경우 단일 작업의 콘텐츠만 테스트되고, 종속성 또는 프레임워크 자체의 동작은 테스트되지 않습니다. 컨트롤러 작업을 단위 테스트할 때에는 동작에만 집중해야 합니다. 컨트롤러 단위 테스트는 [필터](filters.md), [라우팅](../../fundamentals/routing.md), [모델 바인딩](../models/model-binding.md) 같은 것들이 필요 없습니다. 단위 테스트는 하나를 테스트하는 데 집중하기 때문에 일반적으로 작성 방법이 간단하고 신속하게 실행할 수 있습니다. 잘 작성된 단위 테스트 집합은 많은 오버헤드 없이 자주 실행할 수 있습니다. 그러나 단위 테스트는 구성 요소 간의 상호 작용 문제를 검색하지 않습니다. 이 문제는 [통합 테스트](xref:mvc/controllers/testing#integration-testing)의 목적입니다.

사용자 지정 필터, 경로 등을 작성할 때 단위 테스트를 수행해야 하지만, 특정 컨트롤러 작업에 대한 테스트의 일부로 수행하면 안 됩니다. 격리된 상태에서 테스트해야 합니다.

> [!TIP]
> [Visual Studio를 사용하여 단위 테스트를 만들고 실행](https://docs.microsoft.com/visualstudio/test/unit-test-your-code)

단위 테스트를 시연하려면 다음 컨트롤러를 검토합니다. 이 컨트롤러는 브레인스토밍 세션 목록을 표시하며 POST를 사용하여 새로운 브레인스토밍 세션을 만들 수 있습니다.

[!code-csharp[Main](testing/sample/TestingControllersSample/src/TestingControllersSample/Controllers/HomeController.cs?highlight=12,16,21,42,43)]

이 컨트롤러는 [명시적 종속성 원칙](http://deviq.com/explicit-dependencies-principle/)을 따르며, `IBrainstormSessionRepository` 인스턴스를 제공하는 종속성 주입을 예상합니다. 따라서 [Moq](https://www.nuget.org/packages/Moq/) 같은 모의 개체 프레임워크를 사용하여 매우 간편하게 테스트할 수 있습니다. `HTTP GET Index` 메서드는 반복 또는 분기가 없으며 한 가지 메서드만 호출합니다. 이 `Index` 메서드를 테스트하려면 리포지토리의 `List` 메서드에서 `ViewModel`를 사용하여 `ViewResult`가 반환되는지 확인해야 합니다.

[!code-csharp[Main](testing/sample/TestingControllersSample/tests/TestingControllersSample.Tests/UnitTests/HomeControllerTests.cs?highlight=17-18&range=1-33,76-95)]

위에서 나온 `HomeController` `HTTP POST Index` 메서드는 다음을 확인해야 합니다.

* `ModelState.IsValid`가 `false`이면 작업 메서드는 적절한 데이터와 함께 잘못된 요청 `ViewResult`를 반환합니다.

* `ModelState.IsValid`가 true이면 리포지토리의 `Add` 메서드가 호출되고 올바른 인수와 함께 `RedirectToActionResult`가 반환됩니다.

아래의 첫 번째 테스트처럼 `AddModelError`로 오류를 추가하여 잘못된 모델 상태를 테스트할 수 있습니다.

[!code-csharp[Main](testing/sample/TestingControllersSample/tests/TestingControllersSample.Tests/UnitTests/HomeControllerTests.cs?highlight=8,15-16,37-39&range=35-75)]

첫 번째 테스트는 `ModelState`가 잘못된 경우 `GET` 요청과 마찬가지로 동일한 `ViewResult`가 반환되는지 확인합니다. 이 테스트는 잘못된 모델을 전달하려고 시도하지 않습니다. 모델 바인딩이 실행되고 있지 않으므로([통합 테스트](xref:mvc/controllers/testing#integration-testing)에서 연습 모델 바인딩을 사용하겠지만) 어떤 방법으로도 작동하지 않습니다. 이 예에서는 모델 바인딩을 테스트하지 않습니다. 이러한 단위 테스트는 작업 메서드의 코드에서 하는 일만 테스트합니다.

두 번째 테스트는 `ModelState`가 잘못된 경우 새 `BrainstormSession`이 추가되는지(리포지토리를 통해), 메서드가 예상된 속성과 함께 `RedirectToActionResult`를 반환하는지 확인합니다. 호출되지 않은 모의 호출은 일반적으로 무시되지만, 설정 호출의 끝부분에서 `Verifiable`을 호출하면 테스트에서 확인할 수 있습니다. 이것은 `mockRepo.Verify` 호출을 통해 수행되며, 예상된 메서드가 호출되지 않으면 테스트가 실패합니다.

> [!NOTE]
> 이 샘플에 사용된 Moq 라이브러리를 사용하면 확인 가능한 또는 "엄격한" 모의 개체를 확인 불가능한 모의 개체("느슨한" 모의 개체 또는 스텁이라고도 함)와 손쉽게 혼합할 수 있습니다. [Moq를 사용하여 모의 동작 사용자 지정](https://github.com/Moq/moq4/wiki/Quickstart#customizing-mock-behavior)에 대해 자세히 알아보세요.

앱의 다른 컨트롤러는 특정 브레인스토밍 세션과 관련된 정보를 표시합니다. 잘못된 id 값을 처리하는 일부 논리를 포함합니다.

[!code-csharp[Main](./testing/sample/TestingControllersSample/src/TestingControllersSample/Controllers/SessionController.cs?highlight=19,20,21,22,25,26,27,28)]

컨트롤러 작업에는 테스트할 사례가 각 `return` 문에 하나씩, 총 세 개 있습니다.

[!code-csharp[Main](testing/sample/TestingControllersSample/tests/TestingControllersSample.Tests/UnitTests/SessionControllerTests.cs?highlight=27,28,29,46,47,64,65,66,67,68)]

앱에서는 기능을 웹 API(브레인스토밍 세션과 관련된 아이디어 목록 및 세션에 새 아이디어를 추가하기 위한 메서드)로 노출합니다.

<a name="ideas-controller"></a>

[!code-csharp[Main](testing/sample/TestingControllersSample/src/TestingControllersSample/Api/IdeasController.cs?highlight=21,22,27,30,31,32,33,34,35,36,41,42,46,52,65)]

`ForSession` 메서드는 `IdeaDTO` 형식 목록을 반환합니다. API 호출을 통해 직접 비즈니스 도메인 엔터티를 반환하지 마세요. API 호출은 API 클라이언트에서 요구하는 것보다 더 많은 데이터를 포함하고 앱의 내부 도메인 모델을 외부에 노출되는 API와 불필요하게 연결하는 경우가 자주 있기 때문입니다. 도메인 엔터티와 유선으로 반환할 형식 간의 매핑은 수동으로(여기 보이는 것처럼 LINQ `Select` 사용) 또는 [AutoMapper](https://github.com/AutoMapper/AutoMapper) 같은 라이브러리를 사용하여 수행할 수 있습니다.

`Create` 및 `ForSession` API 메서드에 대한 단위 테스트:

[!code-csharp[Main](testing/sample/TestingControllersSample/tests/TestingControllersSample.Tests/UnitTests/ApiIdeasControllerTests.cs?highlight=18,23,29,33,38-39,43,50,58-59,68-70,76-78&range=1-83,121-135)]

앞서 언급했듯이, `ModelState`가 유효하지 않을 때 메서드의 동작을 테스트하려면 테스트의 일부로 컨트롤러에 모델 오류를 추가합니다. 단위 테스트에서 모델 유효성 검사 또는 모델 바인딩을 테스트하지 말고, 특정 `ModelState` 값이 나타나면 작업 메서드의 동작만 테스트하세요.

두 번째 테스트는 null을 반환하는 리포지토리를 사용하므로 모의 리포지토리가 null을 반환하도록 구성됩니다. 테스트 데이터베이스를 만들고(메모리 내부에 또는 다른 위치에) 이 결과를 반환하는 쿼리를 작성할 필요가 없습니다. 다음과 같이 단일 명령문으로 수행할 수 있습니다.

마지막 테스트는 리포지토리의 `Update` 메서드가 호출되는지 확인합니다. 앞에서 살펴본 것처럼, `Verifiable`을 통해 모의 개체가 호출된 후 확인 가능한 메서드가 실행되었는지 확인하기 위해 모의 리포지토리의 `Verify` 메서드가 호출됩니다. `Update` 메서드가 데이터를 저장하도록 보장하는 것은 단위 테스트의 책임이 아니며, 통합 테스트로 수행할 수 있습니다.

## <a name="integration-testing"></a>통합 테스트

[통합 테스트](../../testing/integration-testing.md)는 앱 내의 개별 모듈이 함께 올바르게 작동하도록 보장하기 위해 수행됩니다. 일반적으로 단위 테스트로 테스트할 수 있는 것은 통합 테스트로도 테스트할 수 있지만, 그 반대는 아닙니다. 그러나 통합 테스트는 단위 테스트보다 훨씬 느린 경향이 있습니다. 따라서 되도록이면 단위 테스트를 사용하고, 여러 협력자가 참여하는 시나리오에는 통합 테스트를 사용하는 것이 좋습니다.

모의 개체는 여전히 유용할 수도 있지만, 통합 테스트에 사용되는 경우는 거의 없습니다. 단위 테스트에서, 모의 개체는 테스트되는 단위 외부의 협력자가 테스트 목적에 맞게 행동하려면 어떻게 해야 하는지 제어하는 효율적인 방법입니다. 통합 테스트에서, 실제 협력자는 전체 하위 시스템이 정상적으로 함께 작동하는지 확인하는 데 사용됩니다.

### <a name="application-state"></a>응용 프로그램 상태

통합 테스트를 수행할 때 중요한 고려 사항 중 하나는 앱 상태를 설정하는 방법입니다. 테스트는 서로 독립적으로 실행되어야 하므로 각 테스트에서 알려진 상태의 앱을 시작해야 합니다. 앱에서 데이터베이스를 사용하지 않거나 지속성이 없는 경우에는 이것이 문제가 되지 않을 수 있습니다. 그러나 대부분의 실제 앱은 데이터 저장소에 상태를 저장하므로 데이터 저장소를 다시 설정하지 않는 한, 한 테스트에서 수정된 내용이 다른 테스트에 영향을 줄 수 있습니다. 기본 제공 `TestServer`를 사용하면 통합 테스트 내에서 매우 간단하게 ASP.NET Core 앱을 호스트할 수 있지만, 사용할 데이터에 대한 액세스 권한을 반드시 부여하지는 않습니다. 실제 데이터베이스를 사용하는 경우 테스트에서 액세스할 수 있는 테스트 데이터베이스에 앱을 연결하고, 각 테스트가 실행되기 전에 테스트를 알려진 상태로 다시 설정하는 방법이 있습니다.

이 응용 프로그램 예제에서는 Entity Framework Core의 InMemoryDatabase 지원을 사용하기 때문에 테스트 프로젝트에서 연결할 수 없습니다. 그 대신, 저는 `Development` 환경에 있는 경우 앱이 시작될 때 호출되는 `Startup` 클래스의 `InitializeDatabase` 메서드를 노출하겠습니다. 제가 만든 통합 테스트는 환경을 `Development`로 설정하는 한 자동으로 이 이점을 누리게 됩니다. 앱이 다시 시작될 때마다 InMemoryDatabase가 다시 설정되므로 데이터베이스 재설정에 대해 걱정할 필요가 없습니다.

`Startup` 클래스:

[!code-csharp[Main](testing/sample/TestingControllersSample/src/TestingControllersSample/Startup.cs?highlight=19,20,34,35,43,52)]

아래의 통합 테스트에서 `GetTestSession` 메서드가 자주 사용되는 것을 볼 수 있습니다.

### <a name="accessing-views"></a>보기 액세스

각 통합 테스트 클래스는 ASP.NET Core 앱을 실행할 `TestServer`를 구성합니다. 기본적으로 `TestServer`는 현재 실행되고 있는 폴더에 웹앱을 호스트하는데, 이 예에서는 테스트 프로젝트 폴더입니다. 따라서 `ViewResult`를 반환하는 테스트 컨트롤러 작업을 테스트하려고 시도하면 다음과 같은 오류가 표시될 수 있습니다.

```
The view 'Index' wasn't found. The following locations were searched:
(list of locations)
```

이 문제를 해결하려면 테스트 중인 프로젝트에 대한 보기를 찾을 수 있도록 서버의 콘텐츠 루트를 구성해야 합니다. 이 작업은 아래와 같이 `TestFixture` 클래스의 `UseContentRoot`를 호출하여 수행됩니다.

[!code-csharp[Main](testing/sample/TestingControllersSample/tests/TestingControllersSample.Tests/IntegrationTests/TestFixture.cs?highlight=30,33)]

`TestFixture` 클래스는 `TestServer`를 구성 및 생성하고, `TestServer`와 통신하도록 `HttpClient`를 설정하는 역할을 합니다. 각 통합 테스트에서는 `Client` 속성을 사용하여 테스트 서버에 연결하고 요청을 만듭니다.

[!code-csharp[Main](testing/sample/TestingControllersSample/tests/TestingControllersSample.Tests/IntegrationTests/HomeControllerTests.cs?highlight=20,26,29,30,31,35,38,39,40,41,44,47,48)]

위의 첫 번째 테스트에서, `responseString`은 보기에서 렌더링된 실제 HTML을 보관하며, 이것을 검사하여 예상 결과를 포함하고 있는지 확인할 수 있습니다.

두 번째 테스트는 고유한 세션 이름으로 POST 양식을 만들어서 앱에 게시한 다음, 예상한 리디렉션이 반환되는지 확인합니다.

### <a name="api-methods"></a>API 메서드

앱에서 웹 API를 노출하는 경우 자동화된 테스트를 통해 웹 API가 예상대로 실행되는지 확인하는 것이 좋습니다. 기본 제공 `TestServer`를 사용하면 간편하게 웹 API를 테스트할 수 있습니다. API 메서드에서 모델 바인딩을 사용하는 경우 항상 `ModelState.IsValid`를 확인해야 하며, 통합 테스트를 통해 모델 유효성 검사가 제대로 작동하는지 확인할 수 있습니다.

다음 테스트 집합은 위에 보이는 [IdeasController](xref:mvc/controllers/testing#ideas-controller) 클래스의 `Create` 메서드를 대상으로 합니다.

[!code-csharp[Main](testing/sample/TestingControllersSample/tests/TestingControllersSample.Tests/IntegrationTests/ApiIdeasControllerTests.cs)]

HTML 보기를 반환하는 작업 통합 테스트와는 달리, 결과를 반환하는 웹 API 메서드는 일반적으로 위에 보이는 마지막 테스트처럼 강력한 형식의 개체로 deserialize할 수 있습니다. 이 예의 테스트는 결과를 `BrainstormSession` 인스턴스로 deserialize하고, 아이디어가 아이디어 컬렉션에 올바르게 추가되었는지 확인합니다.

이 문서의 [샘플 프로젝트](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/controllers/testing/sample)에서 더 많은 통합 테스트 예제를 찾을 수 있습니다.
