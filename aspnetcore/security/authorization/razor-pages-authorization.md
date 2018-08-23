---
title: ASP.NET Core에서 razor 페이지 권한 부여 규칙
author: guardrex
description: 사용자 권한 부여 및 익명 사용자가 페이지 또는 페이지의 폴더에 액세스 하도록 허용 하는 규칙을 사용 하 여 페이지에 대 한 액세스를 제어 하는 방법에 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 10/27/2017
uid: security/authorization/razor-pages-authorization
ms.openlocfilehash: d3ecb41765da912df68aeb829350d27e4d087e3a
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41836109"
---
# <a name="razor-pages-authorization-conventions-in-aspnet-core"></a>ASP.NET Core에서 razor 페이지 권한 부여 규칙

[Luke Latham](https://github.com/guardrex)으로

Razor 페이지 앱에 대 한 액세스를 제어 하는 한 가지 방법은 시작 시 권한 부여 규칙을 사용 하는 것입니다. 이러한 규칙을 사용 하면 사용자 권한을 부여 하 고 익명 사용자가 개별 페이지 또는 페이지의 폴더에 액세스할 수 있습니다. 자동으로이 항목에서 설명 하는 규칙이 적용 [권한 부여 필터](xref:mvc/controllers/filters#authorization-filters) 액세스 제어 합니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/razor-pages-authorization/samples)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

샘플 앱에서는 [ASP.NET Core Id 없이 쿠키 인증](xref:security/authentication/cookie)합니다. Maria Rodriguez 가상 사용자의 사용자 계정에는 앱에 대 한 하드 코딩 됩니다. 전자 메일 사용자 이름을 사용 하 여 "maria.rodriguez@contoso.com" 및 사용자를 로그인 할 암호입니다. 사용자가 인증을 `AuthenticateUser` 의 메서드를 *Pages/Account/Login.cshtml.cs* 파일입니다. 실제 예제에서는 데이터베이스에 대해 사용자를 인증 됩니다. ASP.NET Core Id를 사용 하려면의 지침에 따라 합니다 [ASP.NET core Id 소개](xref:security/authentication/identity) 항목입니다. 개념 및이 항목에 표시 하는 예제 ASP.NET Core Id를 사용 하는 앱에 동일 하 게 적용 됩니다.

## <a name="require-authorization-to-access-a-page"></a>페이지에 액세스 권한 부여 필요

사용 하 여는 [AuthorizePage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizepage) 규칙을 통해 [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) 추가 하는 [AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter) 지정된 된 경로에서 페이지:

[!code-csharp[](razor-pages-authorization/samples/2.x/AuthorizationSample/Startup.cs?name=snippet1&highlight=2,4)]

지정된 된 경로 경로인 뷰 엔진에만 슬래시를 포함 하 고 확장 없이 Razor 페이지 루트 상대 경로입니다.

[AuthorizePage 오버 로드](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizepage#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_AuthorizePage_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_String_System_String_) 권한 부여 정책을 지정 해야 하는 경우 사용할 수 있습니다.

::: moniker range=">= aspnetcore-2.1"

> [!NOTE]
> `AuthorizeFilter` 사용 하 여 페이지 모델 클래스에 적용할 수는 `[Authorize]` 필터 특성입니다. 자세한 내용은 [권한 부여 필터 특성](xref:razor-pages/filter#authorize-filter-attribute)합니다.

::: moniker-end

## <a name="require-authorization-to-access-a-folder-of-pages"></a>페이지 폴더 액세스 권한 부여 필요

사용 합니다 [AuthorizeFolder](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizefolder) 규칙을 통해 [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) 추가 하는 [AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter) 지정된 된 경로에 폴더에 있는 페이지의 모든:

[!code-csharp[](razor-pages-authorization/samples/2.x/AuthorizationSample/Startup.cs?name=snippet1&highlight=2,5)]

지정된 된 경로 경로인 뷰 엔진, Razor 페이지 루트 상대 경로입니다.

[AuthorizeFolder 오버 로드](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizefolder#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_AuthorizeFolder_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_String_System_String_) 권한 부여 정책을 지정 해야 하는 경우 사용할 수 있습니다.

::: moniker range=">= aspnetcore-2.1"

## <a name="require-authorization-to-access-an-area-page"></a>영역 페이지에 액세스할 수 있는 인증 필요

사용 하 여는 [AuthorizeAreaPage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizeareapage) 규칙을 통해 [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) 추가 하는 [AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter) 지정 된 경로의 영역 페이지:

```csharp
options.Conventions.AuthorizeAreaPage("Identity", "/Manage/Accounts");
```

페이지 이름은 지정된 된 영역에 대 한 페이지 루트 디렉터리에 상대적인 확장명 없이 파일의 경로입니다. 예를 들어 파일의 페이지 이름을 *Areas/Identity/Pages/Manage/Accounts.cshtml* 됩니다 */관리/계정*합니다.

[AuthorizeAreaPage 오버 로드](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizeareapage#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_AuthorizeAreaPage_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_String_System_String_System_String_) 권한 부여 정책을 지정 해야 하는 경우 사용할 수 있습니다.

## <a name="require-authorization-to-access-a-folder-of-areas"></a>영역의 폴더 액세스 권한 부여 필요

사용 합니다 [AuthorizeAreaFolder](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizeareafolder) 규칙을 통해 [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) 추가할를 [AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter) 모든 지정된 된 경로에 폴더에서:

```csharp
options.Conventions.AuthorizeAreaFolder("Identity", "/Manage");
```

폴더 경로가 지정된 된 영역에 대 한 페이지 루트 디렉터리에 상대적인 폴더의 경로입니다. 예를 들어, 아래에 있는 파일에 대 한 폴더 경로 *영역/Identity/페이지/관리/* 됩니다 */관리*합니다.

[AuthorizeAreaFolder 오버 로드](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizeareafolder#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_AuthorizeAreaFolder_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_String_System_String_System_String_) 권한 부여 정책을 지정 해야 하는 경우 사용할 수 있습니다.

::: moniker-end

## <a name="allow-anonymous-access-to-a-page"></a>페이지에 대 한 익명 액세스를 허용 합니다.

사용 하 여는 [AllowAnonymousToPage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.allowanonymoustopage) 규칙을 통해 [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) 추가 하는 [AllowAnonymousFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.allowanonymousfilter) 지정된 된 경로에 페이지:

[!code-csharp[](razor-pages-authorization/samples/2.x/AuthorizationSample/Startup.cs?name=snippet1&highlight=2,6)]

지정된 된 경로 경로인 뷰 엔진에만 슬래시를 포함 하 고 확장 없이 Razor 페이지 루트 상대 경로입니다.

## <a name="allow-anonymous-access-to-a-folder-of-pages"></a>페이지의 폴더에 대 한 익명 액세스를 허용 합니다.

사용 합니다 [AllowAnonymousToFolder](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.allowanonymoustofolder) 규칙을 통해 [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) 추가 하는 [AllowAnonymousFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.allowanonymousfilter) 지정된 된 경로에 폴더에 있는 페이지의 모든:

[!code-csharp[](razor-pages-authorization/samples/2.x/AuthorizationSample/Startup.cs?name=snippet1&highlight=2,7)]

지정된 된 경로 경로인 뷰 엔진, Razor 페이지 루트 상대 경로입니다.

## <a name="note-on-combining-authorized-and-anonymous-access"></a>익명 액세스 및 권한이 결합에 대 한 참고

페이지 폴더 권한 부여가 필요 하며 해당 폴더 내의 페이지 익명 액세스를 허용 하는지 지정 되도록 지정 하려면 완벽 하 게 유효 합니다.

```csharp
// This works.
.AuthorizeFolder("/Private").AllowAnonymousToPage("/Private/Public")
```

그러나 반대의 경우 true 되지 않습니다. 익명 액세스에 대 한 페이지의 폴더를 선언 하 고 권한 부여를 위해 내에서 페이지를 지정할 수 없습니다.

```csharp
// This doesn't work!
.AllowAnonymousToFolder("/Public").AuthorizePage("/Public/Private") 
```

때문에 작동 하지 않습니다 개인 페이지의 권한 부여를 요구 때 모두를 `AllowAnonymousFilter` 및 `AuthorizeFilter` 필터 페이지에 적용 됩니다는 `AllowAnonymousFilter` wins 및 액세스를 제어 합니다.

## <a name="additional-resources"></a>추가 자료

* [Razor 페이지 사용자 지정 경로 및 페이지 모델 공급자](xref:razor-pages/razor-pages-conventions)
* [PageConventionCollection](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection) 클래스
