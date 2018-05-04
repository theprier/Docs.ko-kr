---
title: 권한 부여에 의해 보호 되는 사용자 데이터와 ASP.NET Core 응용 프로그램 만들기
author: rick-anderson
description: 권한 부여에 의해 보호 되는 사용자 데이터와 함께 Razor 페이지 앱을 만드는 방법에 알아봅니다. HTTPS, 인증, 보안, ASP.NET Core Id를 포함합니다.
manager: wpickett
ms.author: riande
ms.date: 01/24/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: security/authorization/secure-data
ms.openlocfilehash: e42f299efcae7c6a0e3d20b157c591eed98c99d0
ms.sourcegitcommit: 5130b3034165f5cf49d829fe7475a84aa33d2693
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="create-an-aspnet-core-app-with-user-data-protected-by-authorization"></a>권한 부여에 의해 보호 되는 사용자 데이터와 ASP.NET Core 응용 프로그램 만들기

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Joe Audette](https://twitter.com/joeaudette)

이 자습서에는 권한 부여에 의해 보호 되는 사용자 데이터와 ASP.NET Core 웹 앱을 만드는 방법을 보여 줍니다. 인증 된 (등록 된) 사용자 연락처 목록을 표시를 만들었습니다. 세 가지 보안 그룹이 있습니다.

* **사용자가 등록** 수 편집/삭제 자신의 데이터 및 승인 된 모든 데이터를 볼 수 있습니다.
* **관리자** 승인 또는 연락처 데이터를 거부할 수 있습니다. 승인 된 연락처에만 사용자에 게 표시 됩니다.
* **관리자** 수 승인/거부 및 모든 데이터를 편집/삭제 합니다.

다음 이미지에서는 Rick 사용자 (`rick@example.com`)에 로그인 합니다. Rick 승인 된 연락처를 보기만 할 수 있습니다 및 **편집**/**삭제**/**새로 만들기** 그의 연락처에 대 한 링크입니다. 마지막 레코드만 Rick를 표시 하 여 만든 **편집** 및 **삭제** 링크 합니다. 다른 사용자에 게는 관리자 또는 관리자가 상태를 "승인 됨"으로 변경 될 때까지 마지막 레코드를 표시 되지 않습니다.

![이전 이미지 설명](secure-data/_static/rick.png)

다음 그림에 `manager@contoso.com` 관리자 역할에서 서명:

![이전 이미지 설명](secure-data/_static/manager1.png)

다음 이미지는 관리자의 연락처 세부 정보 보기를 보여 줍니다.

![이전 이미지 설명](secure-data/_static/manager.png)

**승인** 및 **거부** 단추가 관리자와 관리자만 표시 됩니다.

다음 그림에 `admin@contoso.com` 관리자 역할에서 서명:

![이전 이미지 설명](secure-data/_static/admin.png)

관리자는 모든 권한을 갖습니다. 그녀는 모든 연락처 읽기/편집/삭제 수 한 연락처의 상태를 변경 했습니다.

응용 프로그램에서 만들어진 [스 캐 폴딩](xref:tutorials/first-mvc-app-xplat/adding-model#scaffold-the-moviecontroller) 다음 `Contact` 모델:

[!code-csharp[](secure-data/samples/starter2/Models/Contact.cs?name=snippet1)]

이 샘플에 다음 권한 부여 처리기를 포함 되어 있습니다.

* `ContactIsOwnerAuthorizationHandler`: 사용자가 데이터를 편집할 수만 보장 합니다.
* `ContactManagerAuthorizationHandler`: 관리자가 승인 또는 거부 연락처 수 있도록 합니다.
* `ContactAdministratorsAuthorizationHandler`: 관리자가 승인 또는 연락처를 거부 하 고 연락처 편집 하거나 삭제할 수 있습니다.

## <a name="prerequisites"></a>전제 조건

이 자습서를 진행 됩니다. 에 대해 잘 알고 있어야 합니다.

* [ASP.NET Core](xref:tutorials/first-mvc-app/start-mvc)
* [인증](xref:security/authentication/index)
* [계정 확인 및 비밀번호 복구](xref:security/authentication/accconfirm)
* [권한 부여](xref:security/authorization/index)
* [Entity Framework Core](xref:data/ef-mvc/intro)

참조 [이 PDF 파일](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/asp.net_repo_pdf_1-16-18.pdf) ASP.NET Core MVC 버전에 대 한 합니다. 이 자습서의 ASP.NET Core 1.1 버전은에 [이](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data) 폴더입니다. ASP.NET Core 예제에는 1.1는 [샘플](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/final2)합니다.

## <a name="the-starter-and-completed-app"></a>시작 및 완료 된 앱

[다운로드](xref:tutorials/index#how-to-download-a-sample) 는 [완료](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/final2) 응용 프로그램입니다. [테스트](#test-the-completed-app) 해당 보안 기능에 잘 알고 있으므로 완료 된 앱입니다.

### <a name="the-starter-app"></a>시작 응용 프로그램

[다운로드](xref:tutorials/index#how-to-download-a-sample) 는 [스타터](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/starter2) 응용 프로그램입니다.

응용 프로그램 실행을 탭의 **ContactManager** 링크를 선택한 만들기, 편집 및 연락처를 삭제를 확인 합니다.

## <a name="secure-user-data"></a>사용자 데이터 보호

다음 섹션에서는 보안 사용자 데이터 응용 프로그램을 만드는 모든 주요 단계 있어야 합니다. 완료 된 프로젝트를 참조 하는 것이 유용할 수 있습니다.

### <a name="tie-the-contact-data-to-the-user"></a>사용자에 게 연락 데이터를 연결 합니다.

ASP.NET을 사용 하 여 [Identity](xref:security/authentication/identity) 가 데이터를 하지만 다른 사용자가 데이터가 아닌 사용자 ID 사용자를 편집할 수 있습니다. 추가 `OwnerID` 및 `ContactStatus` 에 `Contact` 모델:

[!code-csharp[](secure-data/samples/final2/Models/Contact.cs?name=snippet1&highlight=5-6,16-999)]

`OwnerID` 사용자의 id는 `AspNetUser` 테이블에 [Identity](xref:security/authentication/identity) 데이터베이스입니다. `Status` 필드 연락처 일반 사용자가 볼 수 있는지 여부를 결정 합니다.

새 마이그레이션 만들고 데이터베이스를 업데이트 합니다.

```console
dotnet ef migrations add userID_Status
dotnet ef database update
```

### <a name="require-https-and-authenticated-users"></a>HTTPS 및 인증 된 사용자가 필요 합니다.

추가 [IHostingEnvironment](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment) 를 `Startup`:

[!code-csharp[](secure-data/samples/final2/Startup.cs?name=snippet_env)]

에 `ConfigureServices` 의 메서드는 *Startup.cs* 파일에서 추가 된 [RequireHttpsAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requirehttpsattribute) 권한 부여 필터:

[!code-csharp[](secure-data/samples/final2/Startup.cs?name=snippet_SSL&highlight=10-999)]

Visual Studio를 사용 하는 경우에 HTTPS를 활성화 합니다.

참조를 HTTPS로 HTTP 요청을 리디렉션할 [URL 다시 쓰기 미들웨어](xref:fundamentals/url-rewriting)합니다. Visual Studio 코드를 사용 하 여 이거나 HTTPS에 대 한 테스트 인증서를 포함 되지 않은 로컬 플랫폼에 대 한 테스트:

  설정 `"LocalTest:skipSSL": true` 에 *appsettings 합니다. Developement.json* 파일입니다.

### <a name="require-authenticated-users"></a>인증 된 사용자가 필요 합니다.

사용자를 인증 하도록 요구 하는 기본 인증 정책을 설정 합니다. 인증을 통해 Razor 페이지, 컨트롤러 또는 동작 메서드 수준에서 옵트아웃을 선택할 수 있습니다는 `[AllowAnonymous]` 특성입니다. 새로 추가 된 Razor 페이지와 컨트롤러 보호 사용자를 인증 하도록 요구 하는 기본 인증 정책을 설정 합니다. 기본적으로 필요한 인증은 새로운 컨트롤러와 Razor 페이지를 포함 하도록 이용 보다 더 안전한 것은 `[Authorize]` 특성입니다. 

인증 되 면 모든 사용자의 요구 사항에서 [AuthorizeFolder](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizefolder?view=aspnetcore-2.0#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_AuthorizeFolder_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_String_System_String_) 및 [AuthorizePage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizepage?view=aspnetcore-2.0) 호출이 필요 하지 않습니다.

업데이트 `ConfigureServices` 다음과 같이 변경 된:

* 주석으로 처리 `AuthorizeFolder` 및 `AuthorizePage`합니다.
* 사용자를 인증 하도록 요구 하는 기본 인증 정책을 설정 합니다.

[!code-csharp[](secure-data/samples/final2/Startup.cs?name=snippet_defaultPolicy&highlight=23-27,31-999)]

추가 [AllowAnonymous](/dotnet/api/microsoft.aspnetcore.authorization.allowanonymousattribute) 인덱스 및 연락처 정보, 페이지 익명 사용자가 등록 하기 전에 사이트에 대 한 정보를 가져올 수 있도록 합니다. 

[!code-csharp[](secure-data/samples/final2/Pages/Index.cshtml.cs?name=snippet&highlight=2)]

추가 `[AllowAnonymous]` 에 [LoginModel 및 RegisterModel](https://github.com/aspnet/templating/issues/238)합니다.

### <a name="configure-the-test-account"></a>테스트 계정 구성

`SeedData` 클래스에는 두 개의 계정을 만듭니다: 관리자 및 관리자입니다. 사용 하 여는 [암호 관리자 도구](xref:security/app-secrets) 이러한 계정에 대 한 암호를 설정 합니다. 프로젝트 디렉터리에서 암호를 설정 (포함 된 디렉터리 *Program.cs*):

```console
dotnet user-secrets set SeedUserPW <PW>
```

업데이트 `Main` 테스트 암호를 사용 합니다.

[!code-csharp[](secure-data/samples/final2/Program.cs?name=snippet)]

### <a name="create-the-test-accounts-and-update-the-contacts"></a>테스트 계정을 만들고 연락처를 업데이트 합니다.

업데이트는 `Initialize` 에서 메서드는 `SeedData` 테스트 계정을 만들 클래스:

[!code-csharp[](secure-data/samples/final2/Data/SeedData.cs?name=snippet_Initialize)]

관리자 사용자 ID를 추가 하 고 `ContactStatus` 연락처에 있습니다. "제출 됨" 및 "Rejected" 하나의 연락처 중 하나를 확인 합니다. 사용자 ID 및 상태에 있는 모든 연락처를 추가 합니다. 하나만 표시 됩니다.

[!code-csharp[](secure-data/samples/final2/Data/SeedData.cs?name=snippet1&highlight=17,18)]

## <a name="create-owner-manager-and-administrator-authorization-handlers"></a>소유자, 관리자 및 관리자 권한 부여 처리기 만들기

만들기는 `ContactIsOwnerAuthorizationHandler` 클래스에 *권한 부여* 폴더입니다. `ContactIsOwnerAuthorizationHandler` 리소스에 대해 작동 하는 사용자 리소스를 소유 하는지 확인 합니다.

[!code-csharp[](secure-data/samples/final2/Authorization/ContactIsOwnerAuthorizationHandler.cs)]

`ContactIsOwnerAuthorizationHandler` 호출 [컨텍스트. 성공](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandlercontext.succeed#Microsoft_AspNetCore_Authorization_AuthorizationHandlerContext_Succeed_Microsoft_AspNetCore_Authorization_IAuthorizationRequirement_) 현재 인증 된 사용자가 연락처 소유자 인 경우. 권한 부여 처리기 일반적으로:

* 반환할 `context.Succeed` 에서 요구 사항이 충족 합니다.
* 반환할 `Task.CompletedTask` 요구 사항이 충족 되지 않으면 경우. `Task.CompletedTask` 모두 성공 또는 실패는&mdash;다른 권한 부여 처리기 실행할 수 있습니다.

명시적으로 실패 해야 할 경우 반환 [컨텍스트. 실패](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandlercontext.fail)합니다.

응용 프로그램 자체 데이터 연락처 소유자가 데이터를 편집/삭제/만들기를 허용합니다. `ContactIsOwnerAuthorizationHandler` 요구 사항 매개 변수에서 전달 하 고 작업을 확인 하려면 필요 하지 않습니다.

### <a name="create-a-manager-authorization-handler"></a>관리자 권한 부여 처리기 만들기

만들기는 `ContactManagerAuthorizationHandler` 클래스에 *권한 부여* 폴더입니다. `ContactManagerAuthorizationHandler` 리소스에 대해 작동 하는 사용자는 관리자를 확인 합니다. 관리자만 승인 하거나 (새롭거나 변경 된) 콘텐츠 변경 내용을 거부할 수 있습니다.

[!code-csharp[](secure-data/samples/final2/Authorization/ContactManagerAuthorizationHandler.cs)]

### <a name="create-an-administrator-authorization-handler"></a>관리자 권한 부여 처리기 만들기

만들기는 `ContactAdministratorsAuthorizationHandler` 클래스에 *권한 부여* 폴더입니다. `ContactAdministratorsAuthorizationHandler` 리소스에 대해 작동 하는 사용자가 관리자를 확인 합니다. 관리자는 모든 작업을 수행할 수 있습니다.

[!code-csharp[](secure-data/samples/final2/Authorization/ContactAdministratorsAuthorizationHandler.cs)]

## <a name="register-the-authorization-handlers"></a>인증 처리기를 등록 합니다.

Entity Framework Core를 사용 하 여 서비스를 위해 등록 되어야 [종속성 주입](xref:fundamentals/dependency-injection) 를 사용 하 여 [AddScoped](/dotnet/api/microsoft.extensions.dependencyinjection.servicecollectionserviceextensions)합니다. `ContactIsOwnerAuthorizationHandler` ASP.NET Core를 사용 하 여 [Identity](xref:security/authentication/identity), Entity Framework Core 기반입니다. 가 사용할 수 있도록 서비스 컬렉션에 처리기를 등록 된 `ContactsController` 통해 [종속성 주입](xref:fundamentals/dependency-injection)합니다. 다음 코드의 끝에 추가 `ConfigureServices`:

[!code-csharp[](secure-data/samples/final2/Startup.cs?name=ConfigureServices&highlight=41-999)]

`ContactAdministratorsAuthorizationHandler` 및 `ContactManagerAuthorizationHandler` 단일 항목으로 추가 됩니다. EF를 사용 하지 않는 하 고 필요한 모든 정보는 되므로 singleton 하기가 `Context` 의 매개 변수는 `HandleRequirementAsync` 메서드.

## <a name="support-authorization"></a>권한 부여를 지원 합니다.

이 섹션에서는 Razor 페이지를 업데이트 및 운영 요구 사항 클래스를 추가 합니다.

### <a name="review-the-contact-operations-requirements-class"></a>연락처 작업 요구 사항 클래스를 검토 합니다.

검토는 `ContactOperations` 클래스입니다. 이 클래스는 요구 사항이 포함 되어 응용 프로그램이 지 원하는:

[!code-csharp[](secure-data/samples/final2/Authorization/ContactOperations.cs)]

### <a name="create-a-base-class-for-the-razor-pages"></a>Razor 페이지에 대 한 기본 클래스를 만들으십시오

Razor 페이지에 있는 연락처에 사용 되는 서비스를 포함 하는 기본 클래스를 만듭니다. 해당 초기화 코드가 한 위치에 배치 하는 기본 클래스:

[!code-csharp[](secure-data/samples/final2/Pages/Contacts/DI_BasePageModel.cs)]

위의 코드:

* 추가 `IAuthorizationService` 서비스가 권한 부여 처리기에 액세스할 수 있습니다.
* Id를 추가 `UserManager` 서비스입니다.
* `ApplicationDbContext`를 추가합니다.

### <a name="update-the-createmodel"></a>업데이트는 CreateModel

사용 하도록 만들기 페이지 모델 생성자를 업데이트는 `DI_BasePageModel` 기본 클래스:

[!code-csharp[](secure-data/samples/final2/Pages/Contacts/Create.cshtml.cs?name=snippetCtor)]

업데이트는 `CreateModel.OnPostAsync` 메서드:

* 사용자 ID를 추가 `Contact` 모델입니다.
* 사용자에 게 연락처를 만들 수 있는 권한을 확인 하는 권한 부여 처리기를 호출 합니다.

[!code-csharp[](secure-data/samples/final2/Pages/Contacts/Create.cshtml.cs?name=snippet_Create)]

### <a name="update-the-indexmodel"></a>업데이트는 IndexModel

업데이트는 `OnGetAsync` 메서드 연락처만 승인 된 일반 사용자에 게 표시 됩니다.

[!code-csharp[](secure-data/samples/final2/Pages/Contacts/Index.cshtml.cs?name=snippet)]

### <a name="update-the-editmodel"></a>업데이트는 EditModel

연락처를 소유 하 고 확인 하기 위해 인증 처리기를 추가 합니다. 리소스 권한 부여가 유효성을 검사 하기 때문에 `[Authorize]` 특성 충분 하지 않습니다. 앱에 특성 평가 되는 경우 리소스에 액세스할 수 없는 합니다. 리소스 기반 권한 부여는 명령적 이어야 합니다. 페이지 모델에 로드 하 여 또는 자체 처리기 내에서 로드 하 여 응용 프로그램에는 리소스에 대 한 액세스 검사를 수행 해야 합니다. 리소스 키를 전달 하 여 리소스에 액세스할 자주 있습니다.

[!code-csharp[](secure-data/samples/final2/Pages/Contacts/Edit.cshtml.cs?name=snippet)]

### <a name="update-the-deletemodel"></a>업데이트는 DeleteModel

Delete 페이지 모델 사용자에 게 연락처에 delete 권한을 확인 하려면 권한 부여 처리기를 사용 하도록 업데이트 합니다.

[!code-csharp[](secure-data/samples/final2/Pages/Contacts/Delete.cshtml.cs?name=snippet)]

## <a name="inject-the-authorization-service-into-the-views"></a>인증 서비스는 뷰에 삽입

현재 UI에 표시 된 편집한 사용자가을 수정할 수 없는 데이터에 대 한 링크를 삭제 합니다. UI는 권한 부여 처리기 보기에 적용 하 여 고정 됩니다.

권한 부여 서비스를 주입는 *Views/_ViewImports.cshtml* 모든 보기에 사용할 수 있도록 파일:

[!code-cshtml[](secure-data/samples/final2/Pages/_ViewImports.cshtml?highlight=6-9)]

위의 태그 몇 개 추가 `using` 문.

업데이트는 **편집** 및 **삭제** 에서는 정적으로 연결 *Pages/Contacts/Index.cshtml* 적절 한 사용 권한 가진 사용자만 렌더링 될 있도록:

[!code-cshtml[](secure-data/samples/final2/Pages/Contacts/Index.cshtml?highlight=34-36,64-999)]

> [!WARNING]
> 데이터를 변경할 수 있는 권한이 없는 사용자 로부터 링크 숨기기 응용 프로그램 보안을 설정 하지 않습니다. 링크 숨기기 하면 유효한 링크를 표시 하 여 응용 프로그램 보다 사용자 친화적인 있습니다. 사용자가 편집을 호출 하 고 자신이 소유 하지 않는 데이터에 대 한 작업을 삭제 하도록 생성 된 Url 해킹 수 있습니다. Razor 페이지 또는 컨트롤러는 데이터 보호를 위해 액세스 검사를 적용 해야 합니다.

### <a name="update-details"></a>세부 정보 업데이트

관리자 승인 또는 연락처를 거부할 수 있도록 자세히 보기를 업데이트 합니다.

[!code-cshtml[](secure-data/samples/final2/Pages/Contacts/Details.cshtml?range=48-999)]

세부 정보 페이지 모델을 업데이트 합니다.

[!code-csharp[](secure-data/samples/final2/Pages/Contacts/Details.cshtml.cs?name=snippet)]

## <a name="test-the-completed-app"></a>완성 된 응용 프로그램 테스트

Visual Studio 코드를 사용 하 여 이거나 HTTPS에 대 한 테스트 인증서를 포함 되지 않은 로컬 플랫폼에 대 한 테스트:

* 설정 `"LocalTest:skipSSL": true` 에 *appsettings 합니다. Developement.json* HTTPS 요구 사항이 하 파일입니다. 개발 컴퓨터에만 Skip HTTPS입니다.

응용 프로그램에 연락처 하는 경우:

* 모든 레코드를 삭제는 `Contact` 테이블입니다.
* 응용 프로그램에서 데이터베이스를 시드하고 다시 시작 합니다.

연락처 검색에 대 한 사용자를 등록 합니다.

완성 된 앱을 테스트 하는 쉬운 방법은 세 가지 서로 다른 브라우저 (또는 incognito/InPrivate 버전)를 시작 하려면입니다. 하나의 브라우저에서 새 사용자를 등록 합니다 (예를 들어 `test@example.com`). 각 브라우저에 다른 사용자로 로그인 합니다. 다음 작업을 확인 합니다.

* 등록 된 사용자의 승인 된 모든 연락처 데이터를 볼 수 있습니다.
* 등록 된 사용자 수 편집/삭제 자신의 데이터입니다.
* 관리자 승인 하거나 연락 데이터를 거부할 수 있습니다. `Details` 보기 보여줍니다 **승인** 및 **거부** 단추입니다.
* 관리자 승인/거부 있으며 편집/삭제 된 데이터.

| 사용자| 옵션 |
| ------------ | ---------|
| test@example.com | 수 편집/삭제 자체 데이터 |
| manager@contoso.com | 승인/거부 및 편집/삭제를 데이터 소유할 수 있습니까 |
| admin@contoso.com | 편집/삭제 있고 모든 데이터를 승인/거부 합니다.|

관리자의 브라우저에서 연락처를 만듭니다. Delete에 대 한 URL을 복사 하 고 관리자 연락처에서 편집 합니다. 테스트 사용자는 이러한 작업을 수행할 수를 확인 하려면 테스트 사용자의 브라우저에 다음이 링크를 붙여 넣습니다.

## <a name="create-the-starter-app"></a>시작 응용 프로그램 만들기

* "ContactManager" 라는 Razor 페이지 응용 프로그램 만들기

  * 응용 프로그램을 만들 **개별 사용자 계정**합니다.
  * 네임 스페이스에는 샘플에 사용 된 네임 스페이스와 일치 하므로 "ContactManager" 이름을 지정 합니다.

  ```console
  dotnet new razor -o ContactManager -au Individual -uld
  ```

  * `-uld` SQLite는 대신 LocalDB를 지정합니다.

* 다음 추가 `Contact` 모델:

  [!code-csharp[](secure-data/samples/starter2/Models/Contact.cs?name=snippet1)]

* 스 캐 폴드 된 `Contact` 모델:

```console
dotnet aspnet-codegenerator razorpage -m Contact -udl -dc ApplicationDbContext -outDir Pages\Contacts --referenceScriptLibraries
```

* 업데이트는 **ContactManager** 고정는 *Pages/_Layout.cshtml* 파일:

```cshtml
<a asp-page="/Contacts/Index" class="navbar-brand">ContactManager</a>
```

* 초기 마이그레이션을 스 캐 폴드 하 고 데이터베이스를 업데이트 합니다.

```console
dotnet ef migrations add initial
dotnet ef database update
```

* 만들고, 편집 및 연락처를 삭제 하 여 앱을 테스트 합니다.

### <a name="seed-the-database"></a>데이터베이스 시드

추가 `SeedData` 클래스는 *데이터* 폴더입니다. 샘플을 다운로드 하는 경우 복사할 수 있습니다는 *SeedData.cs* 파일을 여 *데이터* 시작 프로젝트의 폴더입니다.

호출 `SeedData.Initialize` 에서 `Main`:

[!code-csharp[](secure-data/samples/starter2/Program.cs?name=snippet)]

응용 프로그램 데이터베이스 시드 있는지 테스트 합니다. DB 연락처의 모든 행이 있는 경우에 초기값 메서드 실행 되지 않습니다.

<a name="secure-data-add-resources-label"></a>

### <a name="additional-resources"></a>추가 자료

* [ASP.NET Core 권한 부여 랩](https://github.com/blowdart/AspNetAuthorizationWorkshop)합니다. 이 자습서에 도입 된 보안 기능에이 랩 자세히 알아봅니다.
* [ASP.NET Core에서 권한 부여: 단순, 역할, 클레임 기반 및 사용자 지정](xref:security/authorization/index)
* [사용자 지정 정책 기반 권한 부여](xref:security/authorization/policies)
