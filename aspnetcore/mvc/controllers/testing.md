---
title: ASP.NET Core에서 컨트롤러 논리 테스트
author: ardalis
description: ASP.NET Core에서 Moq 및 xUnit로 컨트롤러 논리를 테스트하는 방법을 알아봅니다.
ms.author: riande
ms.date: 10/14/2016
uid: mvc/controllers/testing
ms.openlocfilehash: d0b2a25d00187c088671be147844aa892f824c6e
ms.sourcegitcommit: 64c2ca86fff445944b155635918126165ee0f8aa
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2018
ms.locfileid: "41751535"
---
# <a name="test-controller-logic-in-aspnet-core"></a>ASP.NET Core에서 컨트롤러 논리 테스트

작성자: [Steve Smith](https://ardalis.com/)

컨트롤러는 모든 ASP.NET Core MVC 응용 프로그램의 핵심 요소입니다. 따라서 앱에서 의도한 대로 동작한다고 확신할 수 있어야 합니다. 자동화된 테스트를 통해 이러한 확신을 얻고 오류가 발생하기 전에 미리 검색할 수 있습니다. 컨트롤러 내에 불필요한 책임을 지우는 것을 피하고 테스트의 초점을 컨트롤러 책임으로 집중하는 것이 중요합니다.

컨트롤러 논리는 최소화되어야 하고 비즈니스 논리나 인프라 문제(예: 데이터 액세스)에 집중하면 안 됩니다. 프레임워크가 아닌 컨트롤러 논리를 테스트합니다. 유효한 입력 또는 잘못된 입력을 통해 컨트롤러의 *동작* 방식을 테스트합니다. 컨트롤러가 수행하는 비즈니스 작업의 결과를 바탕으로 컨트롤러 응답을 테스트합니다.

컨트롤러의 일반적인 책임:

* `ModelState.IsValid`를 확인합니다.
* `ModelState`가 올바르지 않으면 오류 응답을 반환합니다.
* 지속성 저장소에서 비즈니스 엔터티를 검색합니다.
* 비즈니스 엔터티에서 작업을 수행합니다.
* 보관할 비즈니스 엔터티를 저장합니다.
* 적절한 `IActionResult`를 반환합니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/controllers/testing/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

## <a name="unit-tests-of-controller-logic"></a>컨트롤러 논리의 단위 테스트

[단위 테스트](/dotnet/articles/core/testing/unit-testing-with-dotnet-test)는 인프라 및 종속성으로부터 격리된 상태에서 앱의 일부를 테스트하는 것입니다. 컨트롤러 논리를 단위 테스트하는 경우 단일 작업의 콘텐츠만 테스트되고, 종속성 또는 프레임워크 자체의 동작은 테스트되지 않습니다. 컨트롤러 작업을 단위 테스트할 때에는 동작에만 집중해야 합니다. 컨트롤러 단위 테스트는 [필터](xref:mvc/controllers/filters), [라우팅](xref:fundamentals/routing), [모델 바인딩](xref:mvc/models/model-binding) 같은 것들이 필요 없습니다. 단위 테스트는 하나를 테스트하는 데 집중하기 때문에 일반적으로 작성 방법이 간단하고 신속하게 실행할 수 있습니다. 잘 작성된 단위 테스트 집합은 많은 오버헤드 없이 자주 실행할 수 있습니다. 그러나 단위 테스트는 구성 요소 간의 상호 작용 문제를 검색하지 않습니다. 이 문제는 [통합 테스트](xref:test/integration-tests)의 목적입니다.

사용자 지정 필터 및 경로를 작성할 때 특정 컨트롤러 작업에 대한 테스트의 일부가 아닌 별도로 단위 테스트를 수행해야 합니다.

> [!TIP]
> [Visual Studio를 사용하여 단위 테스트를 만들고 실행](/visualstudio/test/unit-test-your-code)

단위 테스트를 시연하려면 다음 컨트롤러를 검토합니다. 이 컨트롤러는 브레인스토밍 세션 목록을 표시하며 POST를 사용하여 새로운 브레인스토밍 세션을 만들 수 있습니다.

[!code-csharp[](testing/sample/TestingControllersSample/src/TestingControllersSample/Controllers/HomeController.cs?highlight=12,16,21,42,43)]

이 컨트롤러는 [명시적 종속성 원칙](http://deviq.com/explicit-dependencies-principle/)을 따르며, `IBrainstormSessionRepository` 인스턴스를 제공하는 종속성 주입을 예상합니다. 따라서 [Moq](https://www.nuget.org/packages/Moq/) 같은 모의 개체 프레임워크를 사용하여 매우 간편하게 테스트할 수 있습니다. `HTTP GET Index` 메서드는 반복 또는 분기가 없으며 한 가지 메서드만 호출합니다. 이 `Index` 메서드를 테스트하려면 리포지토리의 `List` 메서드에서 `ViewModel`를 사용하여 `ViewResult`가 반환되는지 확인해야 합니다.

[!code-csharp[](testing/sample/TestingControllersSample/tests/TestingControllersSample.Tests/UnitTests/HomeControllerTests.cs?highlight=17-18&range=1-33,76-95)]

위에서 나온 `HomeController` `HTTP POST Index` 메서드는 다음을 확인해야 합니다.

* `ModelState.IsValid`가 `false`이면 작업 메서드는 적절한 데이터와 함께 잘못된 요청 `ViewResult`를 반환합니다.

* `ModelState.IsValid`가 true이면 리포지토리의 `Add` 메서드가 호출되고 올바른 인수와 함께 `RedirectToActionResult`가 반환됩니다.

아래의 첫 번째 테스트처럼 `AddModelError`로 오류를 추가하여 잘못된 모델 상태를 테스트할 수 있습니다.

[!code-csharp[](testing/sample/TestingControllersSample/tests/TestingControllersSample.Tests/UnitTests/HomeControllerTests.cs?highlight=8,15-16,37-39&range=35-75)]

첫 번째 테스트는 `ModelState`가 잘못된 경우 `GET` 요청과 마찬가지로 동일한 `ViewResult`가 반환되는지 확인합니다. 이 테스트는 잘못된 모델을 전달하려고 시도하지 않습니다. 모델 바인딩이 실행되고 있지 않으므로([통합 테스트](xref:test/integration-tests)에서 연습 모델 바인딩을 사용하겠지만) 어떤 방법으로도 작동하지 않습니다. 이 예에서는 모델 바인딩을 테스트하지 않습니다. 이러한 단위 테스트는 작업 메서드의 코드에서 하는 일만 테스트합니다.

두 번째 테스트는 `ModelState`가 잘못된 경우 새 `BrainstormSession`이 추가되는지(리포지토리를 통해), 메서드가 예상된 속성과 함께 `RedirectToActionResult`를 반환하는지 확인합니다. 호출되지 않은 모의 호출은 일반적으로 무시되지만, 설정 호출의 끝부분에서 `Verifiable`을 호출하면 테스트에서 확인할 수 있습니다. 이것은 `mockRepo.Verify` 호출을 통해 수행되며, 예상된 메서드가 호출되지 않으면 테스트가 실패합니다.

> [!NOTE]
> 이 샘플에 사용된 Moq 라이브러리를 사용하면 확인 가능한 또는 "엄격한" 모의 개체를 확인 불가능한 모의 개체("느슨한" 모의 개체 또는 스텁이라고도 함)와 손쉽게 혼합할 수 있습니다. [Moq를 사용하여 모의 동작 사용자 지정](https://github.com/Moq/moq4/wiki/Quickstart#customizing-mock-behavior)에 대해 자세히 알아보세요.

앱의 다른 컨트롤러는 특정 브레인스토밍 세션과 관련된 정보를 표시합니다. 잘못된 id 값을 처리하는 일부 논리를 포함합니다.

[!code-csharp[](testing/sample/TestingControllersSample/src/TestingControllersSample/Controllers/SessionController.cs?highlight=19,20,21,22,25,26,27,28)]

컨트롤러 작업에는 테스트할 사례가 각 `return` 문에 하나씩, 총 세 개 있습니다.

[!code-csharp[](testing/sample/TestingControllersSample/tests/TestingControllersSample.Tests/UnitTests/SessionControllerTests.cs?highlight=27,28,29,46,47,64,65,66,67,68)]

앱에서는 기능을 웹 API(브레인스토밍 세션과 관련된 아이디어 목록 및 세션에 새 아이디어를 추가하기 위한 메서드)로 노출합니다.

[!code-csharp[](testing/sample/TestingControllersSample/src/TestingControllersSample/Api/IdeasController.cs?highlight=21,22,27,30,31,32,33,34,35,36,41,42,46,52,65)]

`ForSession` 메서드는 `IdeaDTO` 형식 목록을 반환합니다. API 호출을 통해 직접 비즈니스 도메인 엔터티를 반환하지 마세요. API 호출은 API 클라이언트에서 요구하는 것보다 더 많은 데이터를 포함하고 앱의 내부 도메인 모델을 외부에 노출되는 API와 불필요하게 연결하는 경우가 자주 있기 때문입니다. 도메인 엔터티와 유선으로 반환할 형식 간의 매핑은 수동으로(여기 보이는 것처럼 LINQ `Select` 사용) 또는 [AutoMapper](https://github.com/AutoMapper/AutoMapper) 같은 라이브러리를 사용하여 수행할 수 있습니다.

`Create` 및 `ForSession` API 메서드에 대한 단위 테스트:

[!code-csharp[](testing/sample/TestingControllersSample/tests/TestingControllersSample.Tests/UnitTests/ApiIdeasControllerTests.cs?highlight=18,23,29,33,38-39,43,50,58-59,68-70,76-78&range=1-83,121-135)]

앞서 언급했듯이, `ModelState`가 유효하지 않을 때 메서드의 동작을 테스트하려면 테스트의 일부로 컨트롤러에 모델 오류를 추가합니다. 단위 테스트에서 모델 유효성 검사 또는 모델 바인딩을 테스트하지 말고, 특정 `ModelState` 값이 나타나면 작업 메서드의 동작만 테스트하세요.

두 번째 테스트는 null을 반환하는 리포지토리를 사용하므로 모의 리포지토리가 null을 반환하도록 구성됩니다. 테스트 데이터베이스를 만들고(메모리 내부에 또는 다른 위치에) 이 결과를 반환하는 쿼리를 작성할 필요가 없습니다. 다음과 같이 단일 명령문으로 수행할 수 있습니다.

마지막 테스트는 리포지토리의 `Update` 메서드가 호출되는지 확인합니다. 앞에서 살펴본 것처럼, `Verifiable`을 통해 모의 개체가 호출된 후 확인 가능한 메서드가 실행되었는지 확인하기 위해 모의 리포지토리의 `Verify` 메서드가 호출됩니다. `Update` 메서드가 데이터를 저장하도록 보장하는 것은 단위 테스트의 책임이 아니며, 통합 테스트로 수행할 수 있습니다.

## <a name="additional-resources"></a>추가 자료

* <xref:test/integration-tests>
