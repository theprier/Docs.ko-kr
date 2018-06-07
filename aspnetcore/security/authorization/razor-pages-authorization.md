---
title: ASP.NET Core의 razor 페이지 권한 부여 규칙
author: guardrex
description: 사용자가 권한을 부여 하 고 익명 사용자가 페이지나 페이지의 하위 폴더에 액세스할 수 있도록 하는 규칙을 사용 하 여 페이지에 대 한 액세스를 제어 하는 방법에 알아봅니다.
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 10/27/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/authorization/razor-pages-authorization
ms.openlocfilehash: 35a21156c001d8703e09e604129c4c2c500fe25f
ms.sourcegitcommit: 726ffab258070b4fe6cf950bf030ce10c0c07bb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34734655"
---
# <a name="razor-pages-authorization-conventions-in-aspnet-core"></a>ASP.NET Core의 razor 페이지 권한 부여 규칙

[Luke Latham](https://github.com/guardrex)으로

Razor 페이지 응용 프로그램에서 액세스를 제어 하는 한 가지 방법은 시작 시 권한 부여 규칙을 사용 하는 것입니다. 이러한 규칙을 사용 하 여 사용자 권한을 부여 하 고 익명 사용자가 개별 페이지나 페이지의 하위 폴더에 액세스할 수 있도록 수 있습니다. 자동으로이 항목에서 설명 하는 규칙이 적용 [권한 부여 필터](xref:mvc/controllers/filters#authorization-filters) 액세스를 제어할 수 있습니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/razor-pages-authorization/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

샘플 앱에서는 [ASP.NET Core Id 없이 쿠키 인증](xref:security/authentication/cookie)합니다. 가상의 사용자, Maria Rodriguez에 대 한 사용자 계정에는 응용 프로그램에 하드 코드 된입니다. 전자 메일 이름을 사용 하 여 "maria.rodriguez@contoso.com" 및 사용자를 로그인 할 암호입니다. 사용자가 인증 된 `AuthenticateUser` 에서 메서드는 *Pages/Account/Login.cshtml.cs* 파일입니다. 실제 예제에서 데이터베이스에 대해 사용자를 인증 합니다. 지침에 따라 ASP.NET Core Id를 사용 하려면는 [ASP.NET Core에 Id 소개](xref:security/authentication/identity) 항목입니다. 개념 및이 항목에 나오는 예에서는 ASP.NET Core Id를 사용 하는 앱을 동일 하 게 적용 됩니다.

## <a name="require-authorization-to-access-a-page"></a>페이지에 액세스할 수 있는 인증 필요

사용 하 여는 [AuthorizePage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizepage) 규칙을 통해 [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) 추가 하는 [AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter) 지정된 된 경로에 대 한 페이지에:

[!code-csharp[](razor-pages-authorization/samples/2.x/AuthorizationSample/Startup.cs?name=snippet1&highlight=2,4)]

지정한 경로가 뷰 엔진 경로 슬래시를 포함 하 고 확장명 없이 Razor 페이지 루트 상대 경로 보여 줍니다.

[AuthorizePage 오버 로드](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizepage#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_AuthorizePage_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_String_System_String_) 권한 부여 정책을 지정 해야 할 경우에 사용할 수 있습니다.

::: moniker range=">= aspnetcore-2.1"

> [!NOTE]
> `AuthorizeFilter` 사용 하는 페이지 모델 클래스에 적용할 수는 `[Authorize]` 필터 특성입니다. 자세한 내용은 참조 [권한 부여 필터 특성](xref:mvc/razor-pages/filter#authorize-filter-attribute)합니다.

::: moniker-end

## <a name="require-authorization-to-access-a-folder-of-pages"></a>페이지 폴더에 액세스할 수 있는 인증 필요

사용 하 여는 [AuthorizeFolder](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizefolder) 규칙을 통해 [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) 추가 하는 [AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter) 의 모든 페이지에 지정된 된 경로에 폴더:

[!code-csharp[](razor-pages-authorization/samples/2.x/AuthorizationSample/Startup.cs?name=snippet1&highlight=2,5)]

지정한 경로가 뷰 엔진 경로 Razor 페이지 루트의 상대 경로 보여 줍니다.

[AuthorizeFolder 오버 로드](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizefolder#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_AuthorizeFolder_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_String_System_String_) 권한 부여 정책을 지정 해야 할 경우에 사용할 수 있습니다.

## <a name="allow-anonymous-access-to-a-page"></a>페이지에 익명 액세스 허용

사용 하 여는 [AllowAnonymousToPage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.allowanonymoustopage) 규칙을 통해 [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) 추가 하는 [AllowAnonymousFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.allowanonymousfilter) 지정된 된 경로에 페이지에:

[!code-csharp[](razor-pages-authorization/samples/2.x/AuthorizationSample/Startup.cs?name=snippet1&highlight=2,6)]

지정한 경로가 뷰 엔진 경로 슬래시를 포함 하 고 확장명 없이 Razor 페이지 루트 상대 경로 보여 줍니다.

## <a name="allow-anonymous-access-to-a-folder-of-pages"></a>페이지의 폴더에 대 한 익명 액세스 허용

사용 하 여는 [AllowAnonymousToFolder](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.allowanonymoustofolder) 규칙을 통해 [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) 추가 하는 [AllowAnonymousFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.allowanonymousfilter) 의 모든 페이지에 지정된 된 경로에 폴더:

[!code-csharp[](razor-pages-authorization/samples/2.x/AuthorizationSample/Startup.cs?name=snippet1&highlight=2,7)]

지정한 경로가 뷰 엔진 경로 Razor 페이지 루트의 상대 경로 보여 줍니다.

## <a name="note-on-combining-authorized-and-anonymous-access"></a>익명 액세스 및 권한이 결합에 대 한 참고

완벽 하 게 페이지 관련 폴더 권한을 부여 받아야 및 해당 폴더 내의 페이지 익명 액세스를 허용 하는지 지정 하는 것이 올바릅니다.

```csharp
// This works.
.AuthorizeFolder("/Private").AllowAnonymousToPage("/Private/Public")
```

그러나 그 반대의 경우은 true입니다. 익명 액세스에 대 한 페이지의 폴더를 선언 하 고 권한 부여를 위해 내에서 페이지를 지정할 수 없습니다.

```csharp
// This doesn't work!
.AllowAnonymousToFolder("/Public").AuthorizePage("/Public/Private") 
```

개인 페이지에 권한 부여가 필요한 수 없으므로 작동 하지 때 모두는 `AllowAnonymousFilter` 및 `AuthorizeFilter` 페이지에 필터가 적용 된는 `AllowAnonymousFilter` wins 및 액세스를 제어 합니다.

## <a name="additional-resources"></a>추가 자료

* [Razor 페이지 사용자 지정 경로 및 페이지 모델 공급자](xref:mvc/razor-pages/razor-pages-conventions)
* [PageConventionCollection](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection) 클래스
