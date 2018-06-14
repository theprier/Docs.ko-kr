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
ms.openlocfilehash: cd1fa7957ca50db0de71f71234f84d3fbc631f45
ms.sourcegitcommit: 7e87671fea9a5f36ca516616fe3b40b537f428d2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35341745"
---
# <a name="razor-pages-authorization-conventions-in-aspnet-core"></a><span data-ttu-id="c9480-103">ASP.NET Core의 razor 페이지 권한 부여 규칙</span><span class="sxs-lookup"><span data-stu-id="c9480-103">Razor Pages authorization conventions in ASP.NET Core</span></span>

<span data-ttu-id="c9480-104">[Luke Latham](https://github.com/guardrex)으로</span><span class="sxs-lookup"><span data-stu-id="c9480-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="c9480-105">Razor 페이지 응용 프로그램에서 액세스를 제어 하는 한 가지 방법은 시작 시 권한 부여 규칙을 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c9480-105">One way to control access in your Razor Pages app is to use authorization conventions at startup.</span></span> <span data-ttu-id="c9480-106">이러한 규칙을 사용 하 여 사용자 권한을 부여 하 고 익명 사용자가 개별 페이지나 페이지의 하위 폴더에 액세스할 수 있도록 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9480-106">These conventions allow you to authorize users and allow anonymous users to access individual pages or folders of pages.</span></span> <span data-ttu-id="c9480-107">자동으로이 항목에서 설명 하는 규칙이 적용 [권한 부여 필터](xref:mvc/controllers/filters#authorization-filters) 액세스를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9480-107">The conventions described in this topic automatically apply [authorization filters](xref:mvc/controllers/filters#authorization-filters) to control access.</span></span>

<span data-ttu-id="c9480-108">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/razor-pages-authorization/samples)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="c9480-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/razor-pages-authorization/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="c9480-109">샘플 앱에서는 [ASP.NET Core Id 없이 쿠키 인증](xref:security/authentication/cookie)합니다.</span><span class="sxs-lookup"><span data-stu-id="c9480-109">The sample app uses [Cookie authentication without ASP.NET Core Identity](xref:security/authentication/cookie).</span></span> <span data-ttu-id="c9480-110">가상의 사용자, Maria Rodriguez에 대 한 사용자 계정에는 응용 프로그램에 하드 코드 된입니다.</span><span class="sxs-lookup"><span data-stu-id="c9480-110">The user account for the hypothetical user, Maria Rodriguez, is hardcoded into the app.</span></span> <span data-ttu-id="c9480-111">전자 메일 이름을 사용 하 여 "maria.rodriguez@contoso.com" 및 사용자를 로그인 할 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="c9480-111">Use the Email username "maria.rodriguez@contoso.com" and any password to sign in the user.</span></span> <span data-ttu-id="c9480-112">사용자가 인증 된 `AuthenticateUser` 에서 메서드는 *Pages/Account/Login.cshtml.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c9480-112">The user is authenticated in the `AuthenticateUser` method in the *Pages/Account/Login.cshtml.cs* file.</span></span> <span data-ttu-id="c9480-113">실제 예제에서 데이터베이스에 대해 사용자를 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9480-113">In a real-world example, the user would be authenticated against a database.</span></span> <span data-ttu-id="c9480-114">지침에 따라 ASP.NET Core Id를 사용 하려면는 [ASP.NET Core에 Id 소개](xref:security/authentication/identity) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="c9480-114">To use ASP.NET Core Identity, follow the guidance in the [Introduction to Identity on ASP.NET Core](xref:security/authentication/identity) topic.</span></span> <span data-ttu-id="c9480-115">개념 및이 항목에 나오는 예에서는 ASP.NET Core Id를 사용 하는 앱을 동일 하 게 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9480-115">The concepts and examples shown in this topic apply equally to apps that use ASP.NET Core Identity.</span></span>

## <a name="require-authorization-to-access-a-page"></a><span data-ttu-id="c9480-116">페이지에 액세스할 수 있는 인증 필요</span><span class="sxs-lookup"><span data-stu-id="c9480-116">Require authorization to access a page</span></span>

<span data-ttu-id="c9480-117">사용 하 여는 [AuthorizePage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizepage) 규칙을 통해 [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) 추가 하는 [AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter) 지정된 된 경로에 대 한 페이지에:</span><span class="sxs-lookup"><span data-stu-id="c9480-117">Use the [AuthorizePage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizepage) convention via [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) to add an [AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter) to the page at the specified path:</span></span>

[!code-csharp[](razor-pages-authorization/samples/2.x/AuthorizationSample/Startup.cs?name=snippet1&highlight=2,4)]

<span data-ttu-id="c9480-118">지정한 경로가 뷰 엔진 경로 슬래시를 포함 하 고 확장명 없이 Razor 페이지 루트 상대 경로 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c9480-118">The specified path is the View Engine path, which is the Razor Pages root relative path without an extension and containing only forward slashes.</span></span>

<span data-ttu-id="c9480-119">[AuthorizePage 오버 로드](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizepage#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_AuthorizePage_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_String_System_String_) 권한 부여 정책을 지정 해야 할 경우에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9480-119">An [AuthorizePage overload](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizepage#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_AuthorizePage_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_String_System_String_) is available if you need to specify an authorization policy.</span></span>

::: moniker range=">= aspnetcore-2.1"

> [!NOTE]
> <span data-ttu-id="c9480-120">`AuthorizeFilter` 사용 하는 페이지 모델 클래스에 적용할 수는 `[Authorize]` 필터 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="c9480-120">An `AuthorizeFilter` can be applied to a page model class with the `[Authorize]` filter attribute.</span></span> <span data-ttu-id="c9480-121">자세한 내용은 참조 [권한 부여 필터 특성](xref:mvc/razor-pages/filter#authorize-filter-attribute)합니다.</span><span class="sxs-lookup"><span data-stu-id="c9480-121">For more information, see [Authorize filter attribute](xref:mvc/razor-pages/filter#authorize-filter-attribute).</span></span>

::: moniker-end

## <a name="require-authorization-to-access-a-folder-of-pages"></a><span data-ttu-id="c9480-122">페이지 폴더에 액세스할 수 있는 인증 필요</span><span class="sxs-lookup"><span data-stu-id="c9480-122">Require authorization to access a folder of pages</span></span>

<span data-ttu-id="c9480-123">사용 하 여는 [AuthorizeFolder](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizefolder) 규칙을 통해 [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) 추가 하는 [AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter) 의 모든 페이지에 지정된 된 경로에 폴더:</span><span class="sxs-lookup"><span data-stu-id="c9480-123">Use the [AuthorizeFolder](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizefolder) convention via [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) to add an [AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter) to all of the pages in a folder at the specified path:</span></span>

[!code-csharp[](razor-pages-authorization/samples/2.x/AuthorizationSample/Startup.cs?name=snippet1&highlight=2,5)]

<span data-ttu-id="c9480-124">지정한 경로가 뷰 엔진 경로 Razor 페이지 루트의 상대 경로 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c9480-124">The specified path is the View Engine path, which is the Razor Pages root relative path.</span></span>

<span data-ttu-id="c9480-125">[AuthorizeFolder 오버 로드](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizefolder#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_AuthorizeFolder_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_String_System_String_) 권한 부여 정책을 지정 해야 할 경우에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9480-125">An [AuthorizeFolder overload](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizefolder#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_AuthorizeFolder_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_String_System_String_) is available if you need to specify an authorization policy.</span></span>

## <a name="allow-anonymous-access-to-a-page"></a><span data-ttu-id="c9480-126">페이지에 익명 액세스 허용</span><span class="sxs-lookup"><span data-stu-id="c9480-126">Allow anonymous access to a page</span></span>

<span data-ttu-id="c9480-127">사용 하 여는 [AllowAnonymousToPage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.allowanonymoustopage) 규칙을 통해 [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) 추가 하는 [AllowAnonymousFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.allowanonymousfilter) 지정된 된 경로에 페이지에:</span><span class="sxs-lookup"><span data-stu-id="c9480-127">Use the [AllowAnonymousToPage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.allowanonymoustopage) convention via [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) to add an [AllowAnonymousFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.allowanonymousfilter) to a page at the specified path:</span></span>

[!code-csharp[](razor-pages-authorization/samples/2.x/AuthorizationSample/Startup.cs?name=snippet1&highlight=2,6)]

<span data-ttu-id="c9480-128">지정한 경로가 뷰 엔진 경로 슬래시를 포함 하 고 확장명 없이 Razor 페이지 루트 상대 경로 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c9480-128">The specified path is the View Engine path, which is the Razor Pages root relative path without an extension and containing only forward slashes.</span></span>

## <a name="allow-anonymous-access-to-a-folder-of-pages"></a><span data-ttu-id="c9480-129">페이지의 폴더에 대 한 익명 액세스 허용</span><span class="sxs-lookup"><span data-stu-id="c9480-129">Allow anonymous access to a folder of pages</span></span>

<span data-ttu-id="c9480-130">사용 하 여는 [AllowAnonymousToFolder](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.allowanonymoustofolder) 규칙을 통해 [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) 추가 하는 [AllowAnonymousFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.allowanonymousfilter) 의 모든 페이지에 지정된 된 경로에 폴더:</span><span class="sxs-lookup"><span data-stu-id="c9480-130">Use the [AllowAnonymousToFolder](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.allowanonymoustofolder) convention via [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) to add an [AllowAnonymousFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.allowanonymousfilter) to all of the pages in a folder at the specified path:</span></span>

[!code-csharp[](razor-pages-authorization/samples/2.x/AuthorizationSample/Startup.cs?name=snippet1&highlight=2,7)]

<span data-ttu-id="c9480-131">지정한 경로가 뷰 엔진 경로 Razor 페이지 루트의 상대 경로 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c9480-131">The specified path is the View Engine path, which is the Razor Pages root relative path.</span></span>

## <a name="note-on-combining-authorized-and-anonymous-access"></a><span data-ttu-id="c9480-132">익명 액세스 및 권한이 결합에 대 한 참고</span><span class="sxs-lookup"><span data-stu-id="c9480-132">Note on combining authorized and anonymous access</span></span>

<span data-ttu-id="c9480-133">완벽 하 게 페이지 관련 폴더 권한을 부여 받아야 및 해당 폴더 내의 페이지 익명 액세스를 허용 하는지 지정 하는 것이 올바릅니다.</span><span class="sxs-lookup"><span data-stu-id="c9480-133">It's perfectly valid to specify that a folder of pages require authorization and specify that a page within that folder allows anonymous access:</span></span>

```csharp
// This works.
.AuthorizeFolder("/Private").AllowAnonymousToPage("/Private/Public")
```

<span data-ttu-id="c9480-134">그러나 그 반대의 경우은 true입니다.</span><span class="sxs-lookup"><span data-stu-id="c9480-134">The reverse, however, isn't true.</span></span> <span data-ttu-id="c9480-135">익명 액세스에 대 한 페이지의 폴더를 선언 하 고 권한 부여를 위해 내에서 페이지를 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c9480-135">You can't declare a folder of pages for anonymous access and specify a page within for authorization:</span></span>

```csharp
// This doesn't work!
.AllowAnonymousToFolder("/Public").AuthorizePage("/Public/Private") 
```

<span data-ttu-id="c9480-136">개인 페이지에 권한 부여가 필요한 수 없으므로 작동 하지 때 모두는 `AllowAnonymousFilter` 및 `AuthorizeFilter` 페이지에 필터가 적용 된는 `AllowAnonymousFilter` wins 및 액세스를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9480-136">Requiring authorization on the Private page won't work because when both the `AllowAnonymousFilter` and `AuthorizeFilter` filters are applied to the page, the `AllowAnonymousFilter` wins and controls access.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c9480-137">추가 자료</span><span class="sxs-lookup"><span data-stu-id="c9480-137">Additional resources</span></span>

* [<span data-ttu-id="c9480-138">Razor 페이지 사용자 지정 경로 및 페이지 모델 공급자</span><span class="sxs-lookup"><span data-stu-id="c9480-138">Razor Pages custom route and page model providers</span></span>](xref:mvc/razor-pages/razor-pages-conventions)
* <span data-ttu-id="c9480-139">[PageConventionCollection](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection) 클래스</span><span class="sxs-lookup"><span data-stu-id="c9480-139">[PageConventionCollection](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection) class</span></span>
