---
title: ASP.NET Core의 통합 테스트
author: guardrex
description: 통합 테스트를 사용하여 앱의 구성 요소가 데이터베이스, 파일 시스템 및 네트워크를 비롯한 인프라 수준에서 제대로 작동하는지 확인하는 방법을 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 05/30/2018
uid: test/integration-tests
ms.openlocfilehash: 1895b06f1af9a9eb66c14aa5c7834497fc95d583
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36277698"
---
# <a name="integration-tests-in-aspnet-core"></a>ASP.NET Core의 통합 테스트

여 [Luke Latham](https://github.com/guardrex) 및 [Steve Smith](https://ardalis.com/)

통합 테스트는 응용 프로그램의 구성 요소는 데이터베이스, 파일 시스템 및 네트워크 같은 응용 프로그램의 지원 인프라를 포함 하는 수준에서 제대로 작동 하는지 확인 합니다. ASP.NET Core 단위 테스트 프레임 워크를 사용 하 여 테스트 웹 호스트와 메모리에 테스트 서버와 통합 테스트를 지원 합니다.

이 항목에서는 단위 테스트에 대 한 기본적인 이해를 가정합니다. 테스트 개념에 익숙하지 않은 경우 참조는 [.NET Core 및.NET 표준 단위 테스트](/dotnet/core/testing/) 항목 및 연결 된 내용입니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

샘플 응용 프로그램은 Razor 페이지 앱 및 Razor 페이지의 한 기본적인 지식이 있다고 가정 합니다. Razor 페이지 사용에 익숙하지 않은 경우 다음 항목을 참조 합니다.

* [Razor 페이지 소개](xref:razor-pages/index)
* [Razor 페이지 시작](xref:tutorials/razor-pages/razor-pages-start)
* [Razor 페이지 단위 테스트](xref:test/razor-pages-tests)

## <a name="introduction-to-integration-tests"></a>통합 테스트 소개

보다 광범위 한 수준에는 응용 프로그램의 구성 요소를 평가 하는 통합 테스트 [단위 테스트](/dotnet/core/testing/)합니다. 단위 테스트 격리 된 소프트웨어 구성 요소를 개별 클래스 메서드를 테스트 하는 데 사용 됩니다. 통합 테스트 둘 이상의 응용 프로그램 구성 요소 전체 요청을 처리 하는 데 필요한 모든 구성 요소를 포함 하 여 예상된 결과 생성 하기 위해 함께 작동 하는지 확인 합니다.

이러한 범위가 넓은 테스트 응용 프로그램의 인프라 및 종종 다음과 같은 구성 요소를 포함 하는 전체 프레임 워크를 테스트 하는 데 사용 됩니다.

* 데이터베이스
* 파일 시스템
* 네트워크 장치
* 요청-응답 파이프라인

단위 테스트 라고 위조 사용 하 여 구성 요소 *fakes* 또는 *개체의 모의 알림*, 인프라 구성 요소 대신 합니다.

단위 테스트와 달리 통합 테스트:

* 프로덕션 환경에서 앱을 사용 하는 실제 구성 요소를 사용 합니다.
* 더 많은 코드 및 데이터 처리가 필요 합니다.
* 실행 하는 데 오래 걸립니다.

따라서 가장 중요 한 인프라 시나리오에 대 한 통합 테스트의 사용을 제한 합니다. 통합 테스트 또는 단위 테스트를 사용 하는 동작을 테스트할 수 있습니다, 단위 테스트를 선택 합니다.

> [!TIP]
> 데이터 및 파일 액세스와 데이터베이스 및 파일 시스템의 모든 가능한 순열에 대 한 통합 테스트를 작성 하지 마십시오. 응용 프로그램에서 관계 없이 데이터베이스 및 파일 시스템, 일련의 읽기, 쓰기, 업데이트 및 삭제 통합 테스트는 일반적으로 적절 하 게 테스트 데이터베이스 수 및 파일 시스템 구성 요소와 상호 작용 합니다. 이러한 구성 요소와 상호 작용 하는 메서드 논리의 일상적인 테스트에 사용 하 여 단위 테스트 합니다. 단위 테스트에서 인프라 사용 fakes/mocks 더 빠른 테스트 실행의 결과입니다.

> [!NOTE]
> 테스트 된 프로젝트의 통합 테스트 토론에 자주 라고는 *테스트 대상 시스템*, 또는 줄여서 "SUT"입니다.

## <a name="aspnet-core-integration-tests"></a>ASP.NET Core 통합 테스트

ASP.NET Core의 통합 테스트 요구 사항:

* 테스트 프로젝트를 포함 하 고 테스트를 실행 하는 데 사용 됩니다. 테스트 프로젝트에 라는 테스트 거친된 ASP.NET Core 프로젝트에 대 한 참조는 *테스트 대상 시스템* (SUT). _"SUT"는이 항목 전체에서 테스트 된 응용 프로그램을 참조 하는 데 사용 됩니다._
* 테스트 프로젝트는 SUT에 대 한 테스트 웹 호스트를 만들고 요청 및 응답의 SUT 처리 하기 위해 테스트 서버 클라이언트를 사용 합니다.
* Test runner는 테스트 결과 테스트와 보고서를 실행 하는 데 사용 됩니다.

통합 테스트는 일반적인 포함 하는 이벤트의 순서에 따라 *정렬*, *Act*, 및 *Assert* 테스트 단계:

1. SUT의 웹 호스트가 구성 되어 있습니다.
1. 응용 프로그램에 요청을 제출 하는 테스트 서버 클라이언트가 만들어집니다.
1. *정렬* 테스트 단계가 실행 되는: 응용 프로그램 테스트는 요청을 준비 합니다.
1. *Act* 테스트 단계가 실행 되는: 클라이언트 요청을 제출 하 고 응답을 받습니다.
1. *Assert* 테스트 단계가 실행 되는:는 *실제* 응답으로 유효성을 검사 한 *전달* 또는 *실패* 기반는 *필요 합니다.*  응답 합니다.
1. 프로세스에는 모든 테스트가 실행 될 때까지 계속 됩니다.
1. 테스트 결과 보고 됩니다.

일반적으로 테스트에 대 한 응용 프로그램의 일반 웹 호스트를 실행 하는 보다 테스트 웹 호스트와 다르게 구성 됩니다. 예를 들어, 다른 데이터베이스 또는 다른 응용 프로그램 설정은 테스트에 사용할 수 있습니다.

메모리 내 테스트 서버와 테스트 웹 호스트 등의 인프라 구성 요소 ([TestServer](/dotnet/api/microsoft.aspnetcore.testhost.testserver)), 제공 하거나 고객이 직접 관리는 [Microsoft.AspNetCore.Mvc.Testing](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Testing) 패키지 합니다. 이 패키지의 사용은 테스트 만들기 및 실행을 간소화합니다.

`Microsoft.AspNetCore.Mvc.Testing` 패키지는 다음과 같은 작업을 처리 합니다.

* 종속성 파일 복사 (*\*.deps*)에서 테스트 프로젝트에 SUT *bin* 폴더입니다.
* 페이지/뷰 및 정적 파일을 찾을 수 있도록 테스트를 실행 하면 콘텐츠 루트 SUT의 프로젝트 루트에 설정 합니다.
* 제공 된 [WebApplicationFactory](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1) 와 SUT 부트스트래핑 간소화 하는 클래스 `TestServer`합니다.

[단위 테스트](/dotnet/articles/core/testing/unit-testing-with-dotnet-test) 설명서에는 테스트 프로젝트 및 테스트 러너, 테스트 및 방법에 대 한 권장 사항 이름 테스트를 실행 하 고 클래스를 테스트 하는 방법에 자세한 내용은 함께 설정 하는 방법에 설명 합니다.

> [!NOTE]
> 응용 프로그램에 대 한 테스트 프로젝트를 만들 때 단위 테스트 통합 테스트에서 다른 프로젝트로 분리 합니다. 이렇게 하면 단위 테스트에 포함 된 테스트 구성 요소 인프라 되지 못하도록 막아야 해당 됩니다. 단위 테스트와 통합 테스트를 분리 수도 있습니다. 실행 되는 일련의 테스트를 통해 제어 합니다.

Razor 페이지 응용 프로그램의 테스트에 대 한 구성 및 MVC 응용 프로그램 간에 차이점이 거의 있습니다. 유일한 차이점은 테스트의 이름을 지정 하는 방법입니다. Razor 페이지 응용 프로그램에서 페이지 끝점에 대 한 테스트는 일반적으로 이름을 페이지 모델 클래스 (예를 들어 `IndexPageTests` 인덱스 페이지에 대 한 통합 구성 요소를 테스트 하려면). MVC 응용 프로그램의 테스트는 일반적으로 컨트롤러 클래스 별로 구성 및 테스트 컨트롤러의 이름을 딴 (예를 들어 `HomeControllerTests` Home 컨트롤러에 대 한 통합 구성 요소를 테스트 하려면).

## <a name="test-app-prerequisites"></a>테스트 응용 프로그램 필수 구성 요소

테스트 프로젝트 수행 해야합니다.

* 에 대 한 참조를 패키지 [Microsoft.AspNetCore.App](https://www.nuget.org/packages/Microsoft.AspNetCore.App/)합니다.
* 프로젝트 파일에서 웹 SDK를 사용 하 여 (`<Project Sdk="Microsoft.NET.Sdk.Web">`).

이러한 prerequesities를 볼 수는 [샘플 응용 프로그램](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples/)합니다. 검사는 *tests/RazorPagesProject.Tests/RazorPagesProject.Tests.csproj* 파일입니다.

## <a name="basic-tests-with-the-default-webapplicationfactory"></a>WebApplicationFactory 기본값을 사용 하 여 기본 테스트

[WebApplicationFactory&lt;TEntryPoint&gt; ](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1) 만드는 데 사용 되는 [TestServer](/dotnet/api/microsoft.aspnetcore.testhost.testserver) 통합 테스트에 대 한 합니다. `TEntryPoint` SUT의 진입점 클래스는 일반적으로 `Startup` 클래스입니다.

테스트 클래스 구현은 *클래스 설비* 인터페이스 (`IClassFixture`) 테스트가 포함 되어 클래스를 표시 하는 클래스에서 테스트 간에 공유 개체 인스턴스를 제공 합니다.

### <a name="basic-test-of-app-endpoints"></a>앱 끝점의 기본 테스트

다음 테스트 클래스, `BasicTests`를 사용 하 여는 `WebApplicationFactory` 는 SUT 부트스트랩을 제공 하는 [HttpClient](/dotnet/api/system.net.http.httpclient) 를 테스트 메서드에 `Get_EndpointsReturnSuccessAndCorrectContentType`합니다. 메서드 응답 상태 코드는 성공적으로 확인 (상태 코드 200 299 사이의) 및 `Content-Type` 헤더는 `text/html; charset=utf-8` 여러 응용 프로그램 페이지에 대 한 합니다.

[CreateClient](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.createclient) 의 인스턴스를 만들고 `HttpClient` 하는 자동으로 리디렉션을 따르며 쿠키를 처리 합니다.

[!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/tests/RazorPagesProject.Tests/IntegrationTests/BasicTests.cs?name=snippet1)]

### <a name="test-a-secure-endpoint"></a>보안 끝점 테스트

다른 테스트에는 `BasicTests` 클래스 보안 끝점 인증 되지 않은 사용자 응용 프로그램의 로그인 페이지로 리디렉션합니다 있는지 검사 합니다.

SUT에 `/SecurePage` 사용 하 여 페이지는 [AuthorizePage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizepage) 적용할 규칙은 [AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter) 페이지에 있습니다. 자세한 내용은 참조 [Razor 페이지 권한 부여 규칙](xref:security/authorization/razor-pages-authorization#require-authorization-to-access-a-page)합니다.

[!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/src/RazorPagesProject/Startup.cs?name=snippet1)]

에 `Get_SecurePageRequiresAnAuthenticatedUser` 를 테스트 한 [WebApplicationFactoryClientOptions](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions) 설정 하 여 리디렉션을 허용 하지 않도록 설정 되어 [AllowAutoRedirect](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions.allowautoredirect) 를 `false`:

[!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/tests/RazorPagesProject.Tests/IntegrationTests/BasicTests.cs?name=snippet2)]

에 따라 리디렉션 클라이언트를 허용 하지 않습니다, 다음 검사를 수행할 수 수 있습니다.

* SUT에서 반환 된 상태 코드를 체크 인할 수 있습니다에 대해 예상 된 [HttpStatusCode.Redirect](/dotnet/api/system.net.httpstatuscode) 결과 만드는 것이 로그인 페이지에 대 한 리디렉션 후 최종 상태 코드가 아닌 [HttpStatusCode.OK](/dotnet/api/system.net.httpstatuscode).
* `Location` 응답 헤더에 헤더 값으로 시작 되는지 확인 하기 위해 검사는 `http://localhost/Identity/Account/Login`, 하지 최종 로그인 페이지 응답, 여기서는 `Location` 헤더 있을 수 없습니다.

대 한 자세한 내용은 `WebApplicationFactoryClientOptions`, 참조는 [클라이언트 옵션](#client-options) 섹션.

## <a name="customize-webapplicationfactory"></a>WebApplicationFactory 사용자 지정

상속 하 여 웹 호스트 구성을 테스트 클래스와 독립적으로 만들 수 있습니다 `WebApplicationFactory` 하나 이상의 사용자 지정 팩터리를 만들려면:

1. 상속 `WebApplicationFactory` 재정의 [ConfigureWebHost](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.configurewebhost)합니다. [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder) 사용 하 여 서비스 컬렉션의 구성을 허용 [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.istartup.configureservices):

   [!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/tests/RazorPagesProject.Tests/CustomWebApplicationFactory.cs?name=snippet1)]

   데이터베이스에서 시드는 [샘플 응용 프로그램](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples) 에 의해 수행 됩니다는 `InitializeDbForTests` 메서드. 메서드는에 설명 되어는 [통합 테스트 샘플: 테스트 앱 조직을](#test-app-organization) 섹션.

2. 사용자 지정을 사용 하 여 `CustomWebApplicationFactory` 테스트 클래스에 있습니다. 공장을 사용 하 여 다음 예제는 `IndexPageTests` 클래스:

   [!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/tests/RazorPagesProject.Tests/IntegrationTests/IndexPageTests.cs?name=snippet1)]

   샘플 응용 프로그램의 클라이언트 수 없도록 구성 되어는 `HttpClient` 에서 다음 리디렉션합니다. 에 설명 된 대로 [보안 끝점 테스트](#test-a-secure-endpoint) 섹션, 이렇게 하면 테스트를 응용 프로그램의 첫 번째 응답의 결과 확인 합니다. 첫 번째 응답은 대부분 사용 하 여 이러한 테스트의 리디렉션은 `Location` 헤더입니다.

3. 일반적인 테스트를 사용 하 여는 `HttpClient` 및 요청 및 응답을 처리 하는 도우미 메서드.

   [!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/tests/RazorPagesProject.Tests/IntegrationTests/IndexPageTests.cs?name=snippet2)]

SUT POST 요청을 자동으로 응용 프로그램의 실행은 antiforgery 검사가 충족 해야 합니다 [데이터 보호 antiforgery 시스템](xref:security/data-protection/introduction)합니다. 테스트의 POST 요청을 정렬 하기 위해 응용 프로그램 테스트 해야 합니다.

1. 페이지에 대 한 요청을 확인 합니다.
1. Antiforgery 쿠키 및 요청 유효성 검사 응답에서 토큰을 구문 분석 합니다.
1. 원위치에서 antiforgery 쿠키 및 요청 유효성 검사 포함 된 POST 요청 토큰을 확인 합니다.

`SendAsync` 도우미 확장 메서드 (*Helpers/HttpClientExtensions.cs*) 및 `GetDocumentAsync` 도우미 메서드 (*Helpers/HtmlHelpers.cs*)에 [샘플앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples/) 사용는 [AngleSharp](https://anglesharp.github.io/) 파서 확인 작업을 처리 antiforgery 다음 방법을 사용 하 여:

* `GetDocumentAsync` &ndash; 수신 된 [HttpResponseMessage](/dotnet/api/system.net.http.httpresponsemessage) 반환는 `IHtmlDocument`합니다. `GetDocumentAsync` 준비 하는 팩터리를 사용 하 여 한 *가상 응답* 원본을 `HttpResponseMessage`합니다. 자세한 내용은 참조는 [AngleSharp 설명서](https://github.com/AngleSharp/AngleSharp#documentation)합니다.
* `SendAsync` 에 대 한 확장 메서드는 `HttpClient` 작성는 [HttpRequestMessage](/dotnet/api/system.net.http.httprequestmessage) 호출 [SendAsync(HttpRequestMessage)](/dotnet/api/system.net.http.httpclient.sendasync#System_Net_Http_HttpClient_SendAsync_System_Net_Http_HttpRequestMessage_) 는 SUT에 요청을 제출 합니다. 에 대 한 오버 로드 `SendAsync` HTML 양식을 수락 (`IHtmlFormElement`) 및 다음:
  - 폼의 단추를 제출 (`IHtmlElement`)
  - 폼 값 컬렉션 (`IEnumerable<KeyValuePair<string, string>>`)
  - 전송 단추 (`IHtmlElement`) 및 값을 양식 (`IEnumerable<KeyValuePair<string, string>>`)

> [!NOTE]
> [AngleSharp](https://anglesharp.github.io/) 제 3 자가 구문 분석 하는이 항목과 샘플 응용 프로그램의 설명을 위해 사용 되는 라이브러리입니다. AngleSharp는 ASP.NET Core 응용 프로그램의 통합 테스트에 필요한 또는 지원 되지 않습니다. 다른 파서를 사용할 수와 같은 [Html 민첩성 팩 (HAP)](http://html-agility-pack.net/)합니다. 다른 방법은 antiforgery 시스템의 요청 확인 토큰 및 antiforgery 쿠키를 직접 처리 하는 코드를 작성 하는 것입니다.

## <a name="customize-the-client-with-withwebhostbuilder"></a>WithWebHostBuilder 사용 하 여 클라이언트를 사용자 지정

추가 구성은 테스트 메서드 내에서 필요한 경우 [WithWebHostBuilder](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.withwebhostbuilder) 새 `WebApplicationFactory` 와 [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder) 한층 더 구성에 의해 사용자 지정 합니다.

`Post_DeleteMessageHandler_ReturnsRedirectToRoot` 테스트의 메서드는 [샘플 응용 프로그램](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples) 의 사용법을 보여줍니다 `WithWebHostBuilder`합니다. 이 테스트는 SUT에서 폼 제출의 트리거하여 데이터베이스에서 레코드 삭제를 수행 합니다.

다른 테스트 하기 때문에 `IndexPageTests` 모든 데이터베이스의 레코드를 삭제 하기 전에 실행 될 수 있습니다 하는 작업을 수행 하는 클래스는 `Post_DeleteMessageHandler_ReturnsRedirectToRoot` 메서드를 데이터베이스에서 삭제할 SUT에 대 한 레코드가 있는지 확인 하려면이 테스트 메서드 마련 됩니다. 선택 하 고 `deleteBtn1` 의 단추는 `messages` 는 SUT 요청에는 SUT에서 폼을 시뮬레이션:

[!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/tests/RazorPagesProject.Tests/IntegrationTests/IndexPageTests.cs?name=snippet3)]

## <a name="client-options"></a>클라이언트 옵션

다음 표에서 기본 [WebApplicationFactoryClientOptions](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions) 만들 때 사용할 수 있는 `HttpClient` 인스턴스.

| 옵션 | 설명 | 기본 |
| ------ | ----------- | ------- |
| [AllowAutoRedirect](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions.allowautoredirect) | 가져오거나 여부 `HttpClient` 인스턴스는 자동으로 리디렉션 응답을 따릅니다. | `true` |
| [BaseAddress](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions.baseaddress) | 기본 주소를 가져오거나 설정 합니다. `HttpClient` 인스턴스. | `http://localhost` |
| [HandleCookies](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions.handlecookies) | 가져오거나 여부 `HttpClient` 인스턴스 쿠키를 처리 해야 합니다. | `true` |
| [MaxAutomaticRedirections](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions.maxautomaticredirections) | 최대 리디렉션 응답 수를 가져오거나 `HttpClient` 인스턴스 따라야 합니다. | 7 |

만들기는 `WebApplicationFactoryClientOptions` 클래스에 전달 하 고는 [CreateClient](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.createclient) 메서드 (값 코드 예제에 표시 된 기본값):

```csharp
// Default client option values are shown
var clientOptions = new WebApplicationFactoryClientOptions();
clientOptions.AllowAutoRedirect = true;
clientOptions.BaseAddress = new Uri("http://localhost");
clientOptions.HandleCookies = true;
clientOptions.MaxAutomaticRedirections = 7;

_client = _factory.CreateClient(clientOptions);
```

## <a name="how-the-test-infrastructure-infers-the-app-content-root-path"></a>테스트 인프라 앱 콘텐츠 루트 경로 유추 하는 방법

`WebApplicationFactory` 검색 하 여 응용 프로그램 콘텐츠 루트 경로 유추 하는 생성자는 [WebApplicationFactoryContentRootAttribute](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactorycontentrootattribute) 같은 키가 있는 통합 테스트를 포함 하는 어셈블리에는 `TEntryPoint` 어셈블리`System.Reflection.Assembly.FullName`. 올바른 키를 사용 하 여 특성을 찾을 수 없으면 경우 `WebApplicationFactory` 솔루션 파일을 검색 하도록 대체 (*\*.sln*) 추가 `TEntryPoint` 솔루션 디렉터리에 어셈블리 이름입니다. 뷰 및 콘텐츠 파일을 검색 하는 응용 프로그램 루트 디렉터리 (콘텐츠 루트 경로) 사용 됩니다.

대부분의 경우에서 없습니다 응용 프로그램 콘텐츠 루트를 명시적으로 설정 하는 데 필요한 대로 검색 논리는 일반적으로 런타임 시 올바른 콘텐츠 루트를 찾습니다. 콘텐츠 루트를 찾을 수 없으면 없는 특수 한 경우에는 기본 제공 검색 알고리즘을 명시적으로 또는 사용자 지정 논리를 사용 하 여 루트를 지정할 수 있습니다 콘텐츠 응용 프로그램을 사용 하 여 합니다. 사용자 인터페이스에서 응용 프로그램 콘텐츠 루트를 설정 하려면 호출는 `UseSolutionRelativeContentRoot` 에서 확장 메서드는 [Microsoft.AspNetCore.TestHost](https://www.nuget.org/packages/Microsoft.AspNetCore.TestHost) 패키지 합니다. 솔루션의 상대 경로 파일 이름이 나 glob 패턴 옵션 솔루션 제공 (기본값 = `*.sln`).

호출 된 [UseSolutionRelativeContentRoot](/dotnet/api/microsoft.aspnetcore.testhost.webhostbuilderextensions.usesolutionrelativecontentroot) 확장 메서드를 사용 하 여 *하나의* 다음 방법 중:

* 테스트 클래스를 구성할 때 `WebApplicationFactory`, 제공 된 사용자 지정 구성에서 [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder):

   ```csharp
   public IndexPageTests(
       WebApplicationFactory<RazorPagesProject.Startup> factory)
   {
       var _factory = factory.WithWebHostBuilder(builder =>
       {
           builder.UseSolutionRelativeContentRoot("<SOLUTION-RELATIVE-PATH>");

           ...
       });
   }
   ```

* 사용자 지정 테스트 클래스를 구성할 때 `WebApplicationFactory`에서 상속 `WebApplicationFactory` 재정의 [ConfigureWebHost](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.configurewebhost):

   ```csharp
   public class CustomWebApplicationFactory<TStartup>
       : WebApplicationFactory<RazorPagesProject.Startup>
   {
       protected override void ConfigureWebHost(IWebHostBuilder builder)
       {
           builder.ConfigureServices(services =>
           {
               builder.UseSolutionRelativeContentRoot("<SOLUTION-RELATIVE-PATH>");

               ...
           });
       }
   }
   ```

## <a name="disable-shadow-copying"></a>섀도 복사를 사용 하지 않도록 설정

섀도 복사 하면 출력 폴더와 다른 폴더에서 실행할 테스트 합니다. 제대로 작동 하려면 테스트에 대해 섀도 복사를 비활성화 해야 합니다. [샘플 응용 프로그램](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples) xUnit를 사용 하 고 포함 하 여 xUnit의 섀도 복사가 해제는 *xunit.runner.json* 올바른 구성 설정으로는 파일입니다. 자세한 내용은 참조 [json xUnit.net 구성](https://xunit.github.io/docs/configuring-with-json.html)합니다.

추가 *xunit.runner.json* 다음 내용 사용 하 여 테스트 프로젝트의 루트에 파일:

```json
{
  "shadowCopy": false
}
```

## <a name="integration-tests-sample"></a>통합 테스트 샘플

[샘플 응용 프로그램](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples) 두 응용 프로그램으로 구성 됩니다.

| 앱 | 프로젝트 폴더 | 설명 |
| --- | -------------- | ----------- |
| 메시지가 응용 프로그램 (SUT) | *src/RazorPagesProject* | 추가, 하나를 삭제 하 고, all, 삭제 하 고 메시지를 분석할 수 있습니다. |
| 응용 프로그램 테스트 | *tests/RazorPagesProject.Tests* | 통합 테스트는 SUT 하는 데 사용 합니다. |

와 같은 IDE의 기본 제공 테스트 기능을 사용 하는 테스트를 실행할 수 있습니다 [Visual Studio](https://www.visualstudio.com/vs/)합니다. 사용 하는 경우 [Visual Studio Code](https://code.visualstudio.com/) 또는 명령줄에서 명령 프롬프트에서 다음 명령을 실행 하는 *tests/RazorPagesProject.Tests* 폴더:

```console
dotnet test
```

### <a name="message-app-sut-organization"></a>메시지가 응용 프로그램 (SUT) 조직

SUT은 Razor 페이지 메시지 시스템에서 다음과 같은 특성입니다.

* 응용 프로그램의 인덱스 페이지 (*Pages/Index.cshtml* 및 *Pages/Index.cshtml.cs*) UI 및 페이지를 추가, 삭제 및 메시지 (메시지 마다 평균 단어) 분석을 제어 하려면 모델 메서드 제공 .
* 메시지에서 설명 된 `Message` 클래스 (*Data/Message.cs*) 두 개의 속성이 있는: `Id` (키) 및 `Text` (메시지). `Text` 속성 인수가 필요 하 고 200 자로 제한 됩니다.
* 메시지를 사용 하 여 저장 된 [Entity Framework의 메모리 내 데이터베이스](/ef/core/providers/in-memory/)&#8224;합니다.
* 앱의 데이터베이스 컨텍스트 클래스의 데이터 액세스 계층 (DAL)에 포함 되어 `AppDbContext` (*Data/AppDbContext.cs*).
* 데이터베이스 응용 프로그램 시작 시에 비어 있으면 메시지 저장소 세 가지 메시지와 함께 초기화 됩니다.
* 응용 프로그램에 포함 되어는 `/SecurePage` 인증 된 사용자만 액세스할 수 있는 합니다.

&#8224;EF 항목 [with InMemory 테스트](/ef/core/miscellaneous/testing/in-memory), MSTest 사용 하 여 테스트에 대 한 메모리 내 데이터베이스를 사용 하는 방법에 설명 합니다. 이 항목에서는 [xUnit](https://xunit.github.io/) 테스트 프레임 워크입니다. 다른 테스트 프레임 워크에서 테스트 구현 및 테스트 개념은 유사 하지만 동일 하지는 않습니다.

응용 프로그램을 사용 하지 않는 있지만 [리포지토리 패턴](http://martinfowler.com/eaaCatalog/repository.html) 와의 효율적인 예가 없습니다는 [작업 단위 (UoW) 패턴](https://martinfowler.com/eaaCatalog/unitOfWork.html), Razor 페이지 개발의 이러한 패턴을 지원 합니다. 자세한 내용은 참조 [인프라 지 속성 계층 디자인](/dotnet/standard/microservices-architecture/microservice-ddd-cqrs-patterns/infrastructure-persistence-layer-design), [ASP.NET MVC 응용 프로그램에서 저장소 및 작업 단위 패턴을 구현](/aspnet/mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application), 및 [테스트 컨트롤러 논리](/aspnet/core/mvc/controllers/testing) (샘플 리포지토리 패턴을 구현 하는 데 사용).

### <a name="test-app-organization"></a>조직 앱 테스트

테스트 응용 프로그램은 콘솔 앱 내에서 *tests/RazorPagesProject.Tests* 폴더입니다.

| 테스트 응용 프로그램 폴더 | 설명 |
| --------------- | ----------- |
| *BasicTests* | *BasicTests.cs* 라우팅, 인증 되지 않은 사용자가 보안 페이지를 액세스 및 GitHub 사용자 프로필 및 프로필의 사용자 로그인 확인을 위한 테스트 메서드가 포함 되어 있습니다. |
| *IntegrationTests* | *IndexPageTests.cs* 포함 사용자 지정을 사용 하 여 인덱스 페이지에 대 한 통합 테스트 `WebApplicationFactory` 클래스입니다. |
| *도우미/유틸리티* | <ul><li>*Utilities.cs* 포함 된 `InitializeDbForTests` 메서드를 테스트 데이터로 데이터베이스를 시드하는 데 사용 합니다.</li><li>*HtmlHelpers.cs* 는 AngleSharp 반환 하는 방법을 제공 `IHtmlDocument` 에서 테스트 메서드를 사용 합니다.</li><li>*HttpClientExtensions.cs* 에 대 한 오버 로드를 제공 `SendAsync` 는 SUT에 요청을 제출 합니다.</li></ul> |

테스트 프레임 워크는 [xUnit](https://xunit.github.io/)합니다. 통합 테스트를 사용 하 여 수행 되는 [Microsoft.AspNetCore.TestHost](/dotnet/api/microsoft.aspnetcore.testhost), 포함 하는 [TestServer](/dotnet/api/microsoft.aspnetcore.testhost.testserver)합니다. 때문에 [Microsoft.AspNetCore.Mvc.Testing](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Testing) 패키지를 사용 하 여 테스트 호스트와 테스트 서버를 구성 하는 `TestHost` 및 `TestServer` 패키지 테스트 응용 프로그램의 프로젝트 파일에서 직접 패키지 참조 필요 없는 또는 테스트 응용 프로그램의 개발자 구성입니다.

**테스트를 위해 데이터베이스 시드**

통합 테스트에서 테스트 실행 하기 전에 데이터베이스의 작은 데이터 집합을 일반적으로 필요합니다. 예를 들어 delete 데이터베이스 삭제 요청이 성공 하려면에 대 한 레코드가 하나 이상 있어야 하므로 데이터베이스 레코드 삭제에 대 한 호출을 테스트 합니다.

샘플 응용 프로그램에서 세 개의 메시지가 포함 된 데이터베이스를 시드합니다 *Utilities.cs* 테스트를 실행할 때 사용할 수 있습니다.

[!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/tests/RazorPagesProject.Tests/Helpers/Utilities.cs?name=snippet1)]

## <a name="additional-resources"></a>추가 자료

* [단위 테스트](/dotnet/articles/core/testing/unit-testing-with-dotnet-test)
* [Razor 페이지 단위 테스트](xref:test/razor-pages-tests)
* [미들웨어](xref:fundamentals/middleware/index)
* [테스트 컨트롤러](xref:mvc/controllers/testing)
