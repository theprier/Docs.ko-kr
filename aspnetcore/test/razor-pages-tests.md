---
title: ASP.NET Core에서 razor 페이지 단위 테스트
author: guardrex
description: Razor 페이지 앱에 대 한 단위 테스트를 만드는 방법에 알아봅니다.
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 11/27/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: test/razor-pages-tests
ms.openlocfilehash: df74d8e44b2dff00e76139edba47fd8a30ce33ef
ms.sourcegitcommit: 63fb07fb3f71b32daf2c9466e132f2e7cc617163
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/10/2018
ms.locfileid: "35252307"
---
# <a name="razor-pages-unit-tests-in-aspnet-core"></a>ASP.NET Core에서 razor 페이지 단위 테스트

[Luke Latham](https://github.com/guardrex)으로

ASP.NET Core Razor 페이지 응용 프로그램의 단위 테스트를 지원합니다. 테스트 데이터의 DAL (계층)에 액세스 하 고 페이지 모델 보장할 합니다.

* Razor 페이지 앱의 일부 응용 프로그램 생성 하는 동안 하나의 단위로 독립적으로 작동합니다.
* 클래스 및 메서드 책임 범위 제한 됩니다.
* 추가 설명서는 응용 프로그램 동작 방식에 있습니다.
* 자동화 된 빌드 및 배포 하는 동안 재발 코드를 업데이트 하 여에 대 한 상태가 오류가 있습니다.

이 항목에서는 Razor 페이지 앱 및 단위 테스트에 대 한 기본적인 이해 있다고 가정 합니다. Razor 페이지 응용 프로그램 또는 테스트 개념 잘 모르는 경우 다음 항목을 참조 합니다.

* [Razor 페이지 소개](xref:mvc/razor-pages/index)
* [Razor 페이지 시작](xref:tutorials/razor-pages/razor-pages-start)
* [에서 단위 테스트 C#.NET Core dotnet 테스트, xUnit를 사용 하 여](/dotnet/articles/core/testing/unit-testing-with-dotnet-test)

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/razor-pages-tests/samples)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

샘플 프로젝트에는 두 응용 프로그램이 구성 됩니다.

| 앱         | 프로젝트 폴더                        | 설명 |
| ----------- | ------------------------------------- | ----------- |
| 응용 프로그램 메시지 | *src/RazorPagesTestSample*            | 추가, 하나를 삭제 하 고, all, 삭제 하 고 메시지를 분석할 수 있습니다. |
| 응용 프로그램 테스트    | *tests/RazorPagesTestSample.Tests*    | 단위 테스트 메시지 응용 프로그램에 사용 되는: DAL (계층) 및 인덱스 페이지 모델 데이터에 액세스 합니다. |

와 같은 IDE의 기본 제공 테스트 기능을 사용 하는 테스트를 실행할 수 있습니다 [Visual Studio](https://www.visualstudio.com/vs/)합니다. 사용 하는 경우 [Visual Studio Code](https://code.visualstudio.com/) 또는 명령줄에서 명령 프롬프트에서 다음 명령을 실행 하는 *tests/RazorPagesTestSample.Tests* 폴더:

```console
dotnet test
```

## <a name="message-app-organization"></a>메시지 앱 조직

메시지 앱은 간단한 Razor 페이지 메시지 시스템에서 다음과 같은 특성:

* 응용 프로그램의 인덱스 페이지 (*Pages/Index.cshtml* 및 *Pages/Index.cshtml.cs*) UI 및 페이지를 추가, 삭제 및 메시지 (메시지 마다 평균 단어) 분석을 제어 하려면 모델 메서드 제공 .
* 메시지에서 설명 된 `Message` 클래스 (*Data/Message.cs*) 두 개의 속성이 있는: `Id` (키) 및 `Text` (메시지). `Text` 속성 인수가 필요 하 고 200 자로 제한 됩니다.
* 메시지를 사용 하 여 저장 된 [Entity Framework의 메모리 내 데이터베이스](/ef/core/providers/in-memory/)&#8224;합니다.
* 앱의 데이터베이스 컨텍스트 클래스의 데이터 액세스 계층 (DAL)에 포함 되어 `AppDbContext` (*Data/AppDbContext.cs*). DAL 메서드는 표시 `virtual`, 테스트에서 사용 하기 위해 메서드를 모의 수 있습니다.
* 데이터베이스 응용 프로그램 시작 시에 비어 있으면 메시지 저장소 세 가지 메시지와 함께 초기화 됩니다. 이러한 *메시지 시드* 테스트에도 사용 됩니다.

&#8224;EF 항목 [with InMemory 테스트](/ef/core/miscellaneous/testing/in-memory), MSTest 사용 하 여 테스트에 대 한 메모리 내 데이터베이스를 사용 하는 방법에 설명 합니다. 이 항목에서는 [xUnit](https://xunit.github.io/) 테스트 프레임 워크입니다. 다른 테스트 프레임 워크에서 테스트 구현 및 테스트 개념은 유사 하지만 동일 하지는 않습니다.

응용 프로그램을 사용 하지 않는 있지만 [리포지토리 패턴](http://martinfowler.com/eaaCatalog/repository.html) 와의 효율적인 예가 없습니다는 [작업 단위 (UoW) 패턴](https://martinfowler.com/eaaCatalog/unitOfWork.html), Razor 페이지 개발의 이러한 패턴을 지원 합니다. 자세한 내용은 참조 [인프라 지 속성 계층 디자인](/dotnet/standard/microservices-architecture/microservice-ddd-cqrs-patterns/infrastructure-persistence-layer-design), [ASP.NET MVC 응용 프로그램에서 저장소 및 작업 단위 패턴을 구현](/aspnet/mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application), 및 [테스트 컨트롤러 논리](/aspnet/core/mvc/controllers/testing) (샘플 리포지토리 패턴을 구현 하는 데 사용).

## <a name="test-app-organization"></a>조직 앱 테스트

테스트 응용 프로그램은 콘솔 앱 내에서 *tests/RazorPagesTestSample.Tests* 폴더입니다.

| 테스트 응용 프로그램 폴더 | 설명 |
| --------------- | ----------- |
| *UnitTests*     | <ul><li>*DataAccessLayerTest.cs* DAL에 대 한 단위 테스트를 포함 합니다.</li><li>*IndexPageTests.cs* 인덱스 페이지 모델에 대 한 단위 테스트를 포함 합니다.</li></ul> |
| *유틸리티*     | 포함 된 `TestingDbContextOptions` 새 데이터베이스를 만들 각 DAL 단위 테스트에 대 한 상황에 맞는 옵션 데이터베이스를 각 테스트에 대 한 초기 상태로 다시 설정 되도록 사용 하는 방법입니다. |

테스트 프레임 워크는 [xUnit](https://xunit.github.io/)합니다. 프레임 워크를 모의 개체는 [Moq](https://github.com/moq/moq4)합니다.

## <a name="unit-tests-of-the-data-access-layer-dal"></a>데이터의 단위 테스트 DAL (계층)에 액세스

메시지가 응용 프로그램에 포함 된 4 가지 방법으로는 DAL에는 `AppDbContext` 클래스 (*src/RazorPagesTestSample/Data/AppDbContext.cs*). 각 메서드에 테스트 응용 프로그램의 하나 또는 두 개의 단위 테스트에 있습니다.

| DAL 메서드               | 기능                                                                   |
| ------------------------ | -------------------------------------------------------------------------- |
| `GetMessagesAsync`       | 가져옵니다는 `List<Message>` 기준으로 정렬 하는 데이터베이스에서는 `Text` 속성입니다. |
| `AddMessageAsync`        | 추가 `Message` 데이터베이스에 있습니다.                                          |
| `DeleteAllMessagesAsync` | 모든 삭제 `Message` 데이터베이스에서 항목입니다.                           |
| `DeleteMessageAsync`     | 단일 삭제 `Message` 하 여 데이터베이스에서 `Id`합니다.                      |

DAL의 단위 테스트에 필요한 [DbContextOptions](/dotnet/api/microsoft.entityframeworkcore.dbcontextoptions) 를 새로 만들 때 `AppDbContext` 각 테스트에 대 한 합니다. 만드는 한 가지 방법은 `DbContextOptions` 각 테스트를 사용 하는 것을 [DbContextOptionsBuilder](/dotnet/api/microsoft.entityframeworkcore.dbcontextoptionsbuilder):

```csharp
var optionsBuilder = new DbContextOptionsBuilder<AppDbContext>()
    .UseInMemoryDatabase("InMemoryDb");

using (var db = new AppDbContext(optionsBuilder.Options))
{
    // Use the db here in the unit test.
}
```

이 방법을 사용이 문제는 각 테스트에서 상태로 이전 테스트 된 상태로 남아 서 데이터베이스를 받습니다. 서로 간섭 하지 않는 원자성 단위 테스트를 작성 하려고 할 때 문제가 될 수 있습니다. 강제로 `AppDbContext` 제공할 각 테스트에 대 한 새 데이터베이스 컨텍스트를 사용 하는 `DbContextOptions` 새 서비스 공급자를 기반으로 하는 인스턴스. 테스트 응용 프로그램을 사용 하는 방법을 보여 줍니다 해당 `Utilities` 클래스 메서드에 `TestingDbContextOptions` (*tests/RazorPagesTestSample.Tests/Utilities/Utilities.cs*):

[!code-csharp[](razor-pages-tests/samples/2.x/tests/RazorPagesTestSample.Tests/Utilities/Utilities.cs?name=snippet1)]

사용 하 여 `DbContextOptions` DAL 단위 테스트는 새 데이터베이스 인스턴스와 개별적으로 실행 하려면 각 테스트를 수 있습니다.:

```csharp
using (var db = new AppDbContext(Utilities.TestingDbContextOptions()))
{
    // Use the db here in the unit test.
}
```

각 테스트 메서드는 `DataAccessLayerTest` 클래스 (*UnitTests/DataAccessLayerTest.cs*) 정렬 Act Assert 비슷한 패턴을 따릅니다.

1. 정렬: 데이터베이스가 테스트에 대해 구성 된 및/또는 정의 된 예상된 결과
1. Act: 테스트 실행 됩니다.
1. Assert: 테스트 결과 성공 인지 확인 하려면 어설션은 수행 됩니다.

예를 들어는 `DeleteMessageAsync` 로 식별 되는 단일 메시지를 제거 하기 위한 메서드는 해당 `Id` (*src/RazorPagesTestSample/Data/AppDbContext.cs*):

[!code-csharp[](razor-pages-tests/samples/2.x/src/RazorPagesTestSample/Data/AppDbContext.cs?name=snippet4)]

이 메서드에 대 한 두 개의 테스트가 있습니다. 하나의 테스트 메서드는 메시지가 데이터베이스에 있는 경우 메시지를 삭제를 확인 합니다. 데이터베이스는 변경 되지 않습니다는 다른 메서드 테스트 메시지 `Id` 삭제 존재 하지 않습니다. `DeleteMessageAsync_MessageIsDeleted_WhenMessageIsFound` 메서드는 다음과 같습니다.

[!code-csharp[](razor-pages-tests/samples_snapshot/2.x/tests/RazorPagesTestSample.Tests/UnitTests/DataAccessLayerTest.cs?name=snippet1)]

먼저, 메서드는 작업 단계에 대 한 준비 일어나 정렬 단계를 수행 합니다. 시드 메시지를 얻고에 보관 `seedMessages`합니다. 시드 메시지는 데이터베이스에 저장 됩니다. 사용 하 여 메시지는 `Id` 의 `1` 삭제에 대해 설정 됩니다. 경우는 `DeleteMessageAsync` 메서드 실행 되 고, 필요한 메시지의 모든 메시지로 레코드를 제외 하 고 있어야는 `Id` 의 `1`합니다. `expectedMessages` 변수는이 예상된 결과 나타냅니다.

[!code-csharp[](razor-pages-tests/samples/2.x/tests/RazorPagesTestSample.Tests/UnitTests/DataAccessLayerTest.cs?name=snippet1)]

메서드는 역할:는 `DeleteMessageAsync` 전달 메서드가 실행 되는 `recId` 의 `1`:

[!code-csharp[](razor-pages-tests/samples/2.x/tests/RazorPagesTestSample.Tests/UnitTests/DataAccessLayerTest.cs?name=snippet2)]

마지막으로 메서드가 가져오면는 `Messages` 컨텍스트에서 비교는 `expectedMessages` 둘이 같으면 어설션하:

[!code-csharp[](razor-pages-tests/samples/2.x/tests/RazorPagesTestSample.Tests/UnitTests/DataAccessLayerTest.cs?name=snippet3)]

비교를 위해 두 `List<Message>` 동일 합니다.

* 메시지의 기준으로 정렬 된 `Id`합니다.
* 메시지 쌍에 비교 되는 `Text` 속성입니다.

비슷한 테스트 메서드, `DeleteMessageAsync_NoMessageIsDeleted_WhenMessageIsNotFound` 존재 하지 않는 메시지를 삭제 하는 결과 확인 합니다. 이 경우 데이터베이스에서 예상된 메시지 같아야 하 후 실제 메시지는 `DeleteMessageAsync` 메서드를 실행 합니다. 데이터베이스의 콘텐츠를 변경 해야 합니다.

[!code-csharp[](razor-pages-tests/samples/2.x/tests/RazorPagesTestSample.Tests/UnitTests/DataAccessLayerTest.cs?name=snippet4)]

## <a name="unit-tests-of-the-page-model-methods"></a>페이지 모델 메서드의 단위 테스트

다른 일련의 단위 테스트는 테스트 페이지 모델 메서드를 담당 합니다. 메시지 응용 프로그램에서 인덱스 페이지 모델에서 발견 되는 `IndexModel` 클래스 *src/RazorPagesTestSample/Pages/Index.cshtml.cs*합니다.

| 페이지 모델 메서드 | 기능 |
| ----------------- | -------- |
| `OnGetAsync` | 사용 하 여 UI에 대 한 DAL에서 메시지를 가져옵니다는 `GetMessagesAsync` 메서드. |
| `OnPostAddMessageAsync` | 경우는 `ModelState` 올바른지, 호출 `AddMessageAsync` 데이터베이스에 메시지를 추가 합니다. |
| `OnPostDeleteAllMessagesAsync` | 호출 `DeleteAllMessagesAsync` 모든 데이터베이스에서 메시지를 삭제 합니다. |
| `OnPostDeleteMessageAsync` | 실행 `DeleteMessageAsync` 포함 된 메시지를 삭제 하는 `Id` 지정 합니다. |
| `OnPostAnalyzeMessagesAsync` | 하나 이상의 메시지는 데이터베이스에 있으면 메시지당 단어의 평균 수를 계산 합니다. |

페이지 모델 메서드 테스트에서 7 개의 테스트를 사용 하 여 `IndexPageTests` 클래스 (*tests/RazorPagesTestSample.Tests/UnitTests/IndexPageTests.cs*). 테스트는 친숙 한 정렬 Assert Act 패턴을 사용 합니다. 이러한 테스트에 집중 합니다.

* 메서드 수행 올바른 동작을 결정 하는 경우는 `ModelState` 올바르지 않습니다.
* 올바르게 생성 방법을 확인 `IActionResult`합니다.
* 속성 값을 할당 내용이 확인 중입니다.

이 그룹의 테스트 페이지 모델 메서드가 실행 될 작업 단계에 대 한 예상 되는 데이터를 생성 하기 위해 DAL의 메서드를 종종 모의 합니다. 예를 들어는 `GetMessagesAsync` 의 메서드는 `AppDbContext` 출력을 생성 모의 합니다. 이 메서드를 실행 하는 페이지 모델 메서드를 모의 결과 반환 합니다. 데이터는 데이터베이스에서 가져와야 하지 않습니다. 이 메서드는 DAL을 사용 하 여 페이지 모델 테스트에 대 한 예측 가능 하 고 신뢰할 수 있는 테스트 조건을 만듭니다.

`OnGetAsync_PopulatesThePageModel_WithAListOfMessages` 테스트 표시 방법을 `GetMessagesAsync` 페이지 모델에 대 한 메서드는 모의:

[!code-csharp[](razor-pages-tests/samples/2.x/tests/RazorPagesTestSample.Tests/UnitTests/IndexPageTests.cs?name=snippet1&highlight=3-4)]

경우는 `OnGetAsync` 메서드는 동작 단계에서 실행 되 고, 페이지 모델 호출 `GetMessagesAsync` 메서드.

단위 테스트에 Act 단계 (*tests/RazorPagesTestSample.Tests/UnitTests/IndexPageTests.cs*):

[!code-csharp[](razor-pages-tests/samples/2.x/tests/RazorPagesTestSample.Tests/UnitTests/IndexPageTests.cs?name=snippet2)]

`IndexPage` 페이지 모델 `OnGetAsync` 메서드 (*src/RazorPagesTestSample/Pages/Index.cshtml.cs*):

[!code-csharp[](razor-pages-tests/samples/2.x/src/RazorPagesTestSample/Pages/Index.cshtml.cs?name=snippet1&highlight=3)]

`GetMessagesAsync` DAL에서 메서드는이 메서드 호출에 대 한 결과 반환 하지 않습니다. 모의 버전의 메서드는 결과 반환합니다.

에 `Assert` 단계, 실제 메시지 (`actualMessages`)에서 할당 되는 `Messages` 페이지 모델의 속성입니다. 형식 검사를 메시지에 할당 된 경우에 수행 됩니다. 예상 및 실제 메시지를 통해 비교 됩니다 자신의 `Text` 속성입니다. 테스트를 어설션하는 두 `List<Message>` 인스턴스 같은 메시지를 포함 합니다.

[!code-csharp[](razor-pages-tests/samples/2.x/tests/RazorPagesTestSample.Tests/UnitTests/IndexPageTests.cs?name=snippet3)]

이 그룹의 다른 테스트 페이지를 포함 하는 모델 개체 만들기는 `DefaultHttpContext`, `ModelStateDictionary`, `ActionContext` 설정 하는 `PageContext`, `ViewDataDictionary`, 및 `PageContext`합니다. 이들은 테스트를 수행 하는 데 유용 합니다. 예를 들어 메시지 응용 프로그램 설정는 `ModelState` 오류로 `AddModelError` 있는지 여부를 확인 하는 유효한 `PageResult` 이 반환 됩니다 `OnPostAddMessageAsync` 실행 됩니다:

[!code-csharp[](razor-pages-tests/samples/2.x/tests/RazorPagesTestSample.Tests/UnitTests/IndexPageTests.cs?name=snippet4&highlight=11,26,29,32)]

## <a name="additional-resources"></a>추가 자료

* [에서 단위 테스트 C#.NET Core dotnet 테스트, xUnit를 사용 하 여](/dotnet/articles/core/testing/unit-testing-with-dotnet-test)
* [테스트 컨트롤러](xref:mvc/controllers/testing)
* [단위 테스트 코드](/visualstudio/test/unit-test-your-code) (Visual Studio)
* [통합 테스트](xref:test/integration-tests)
* [xUnit.net](https://xunit.github.io/)
* [시작 xUnit.net (.NET Core/ASP.NET 코어)](https://xunit.github.io/docs/getting-started-dotnet-core)
* [Moq](https://github.com/moq/moq4)
* [Moq 빠른 시작](https://github.com/Moq/moq4/wiki/Quickstart)
