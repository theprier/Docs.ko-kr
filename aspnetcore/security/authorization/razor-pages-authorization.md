---
title: ASP.NET Core에서 razor 페이지 권한 부여 규칙
author: guardrex
description: 사용자 권한 부여 및 익명 사용자가 페이지 또는 페이지의 폴더에 액세스 하도록 허용 하는 규칙을 사용 하 여 페이지에 대 한 액세스를 제어 하는 방법에 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 10/27/2017
uid: security/authorization/razor-pages-authorization
ms.openlocfilehash: 675dc8aa4bf00bb21981cc892a09a4acd0d53c15
ms.sourcegitcommit: 375e9a67f5e1f7b0faaa056b4b46294cc70f55b7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50207266"
---
# <a name="razor-pages-authorization-conventions-in-aspnet-core"></a><span data-ttu-id="d226a-103">ASP.NET Core에서 razor 페이지 권한 부여 규칙</span><span class="sxs-lookup"><span data-stu-id="d226a-103">Razor Pages authorization conventions in ASP.NET Core</span></span>

<span data-ttu-id="d226a-104">[Luke Latham](https://github.com/guardrex)으로</span><span class="sxs-lookup"><span data-stu-id="d226a-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="d226a-105">Razor 페이지 앱에 대 한 액세스를 제어 하는 한 가지 방법은 시작 시 권한 부여 규칙을 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d226a-105">One way to control access in your Razor Pages app is to use authorization conventions at startup.</span></span> <span data-ttu-id="d226a-106">이러한 규칙을 사용 하면 사용자 권한을 부여 하 고 익명 사용자가 개별 페이지 또는 페이지의 폴더에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d226a-106">These conventions allow you to authorize users and allow anonymous users to access individual pages or folders of pages.</span></span> <span data-ttu-id="d226a-107">자동으로이 항목에서 설명 하는 규칙이 적용 [권한 부여 필터](xref:mvc/controllers/filters#authorization-filters) 액세스 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="d226a-107">The conventions described in this topic automatically apply [authorization filters](xref:mvc/controllers/filters#authorization-filters) to control access.</span></span>

<span data-ttu-id="d226a-108">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/razor-pages-authorization/samples) ([다운로드 방법](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="d226a-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/razor-pages-authorization/samples) ([how to download](xref:index#how-to-download-a-sample))</span></span>

<span data-ttu-id="d226a-109">샘플 앱에서는 [ASP.NET Core Id 없이 쿠키 인증](xref:security/authentication/cookie)합니다.</span><span class="sxs-lookup"><span data-stu-id="d226a-109">The sample app uses [Cookie authentication without ASP.NET Core Identity](xref:security/authentication/cookie).</span></span> <span data-ttu-id="d226a-110">Maria Rodriguez 가상 사용자의 사용자 계정에는 앱에 대 한 하드 코딩 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d226a-110">The user account for the hypothetical user, Maria Rodriguez, is hardcoded into the app.</span></span> <span data-ttu-id="d226a-111">전자 메일 사용자 이름을 사용 하 여 "maria.rodriguez@contoso.com" 및 사용자를 로그인 할 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="d226a-111">Use the Email username "maria.rodriguez@contoso.com" and any password to sign in the user.</span></span> <span data-ttu-id="d226a-112">사용자가 인증을 `AuthenticateUser` 의 메서드를 *Pages/Account/Login.cshtml.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d226a-112">The user is authenticated in the `AuthenticateUser` method in the *Pages/Account/Login.cshtml.cs* file.</span></span> <span data-ttu-id="d226a-113">실제 예제에서는 데이터베이스에 대해 사용자를 인증 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d226a-113">In a real-world example, the user would be authenticated against a database.</span></span> <span data-ttu-id="d226a-114">ASP.NET Core Id를 사용 하려면의 지침에 따라 합니다 [ASP.NET core Id 소개](xref:security/authentication/identity) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="d226a-114">To use ASP.NET Core Identity, follow the guidance in the [Introduction to Identity on ASP.NET Core](xref:security/authentication/identity) topic.</span></span> <span data-ttu-id="d226a-115">개념 및이 항목에 표시 하는 예제 ASP.NET Core Id를 사용 하는 앱에 동일 하 게 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d226a-115">The concepts and examples shown in this topic apply equally to apps that use ASP.NET Core Identity.</span></span>

## <a name="require-authorization-to-access-a-page"></a><span data-ttu-id="d226a-116">페이지에 액세스 권한 부여 필요</span><span class="sxs-lookup"><span data-stu-id="d226a-116">Require authorization to access a page</span></span>

<span data-ttu-id="d226a-117">사용 하 여는 [AuthorizePage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizepage) 규칙을 통해 [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) 추가 하는 [AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter) 지정된 된 경로에서 페이지:</span><span class="sxs-lookup"><span data-stu-id="d226a-117">Use the [AuthorizePage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizepage) convention via [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) to add an [AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter) to the page at the specified path:</span></span>

[!code-csharp[](razor-pages-authorization/samples/2.x/AuthorizationSample/Startup.cs?name=snippet1&highlight=2,4)]

<span data-ttu-id="d226a-118">지정된 된 경로 경로인 뷰 엔진에만 슬래시를 포함 하 고 확장 없이 Razor 페이지 루트 상대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="d226a-118">The specified path is the View Engine path, which is the Razor Pages root relative path without an extension and containing only forward slashes.</span></span>

<span data-ttu-id="d226a-119">[AuthorizePage 오버 로드](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizepage#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_AuthorizePage_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_String_System_String_) 권한 부여 정책을 지정 해야 하는 경우 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d226a-119">An [AuthorizePage overload](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizepage#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_AuthorizePage_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_String_System_String_) is available if you need to specify an authorization policy.</span></span>

::: moniker range=">= aspnetcore-2.1"

> [!NOTE]
> <span data-ttu-id="d226a-120">`AuthorizeFilter` 사용 하 여 페이지 모델 클래스에 적용할 수는 `[Authorize]` 필터 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="d226a-120">An `AuthorizeFilter` can be applied to a page model class with the `[Authorize]` filter attribute.</span></span> <span data-ttu-id="d226a-121">자세한 내용은 [권한 부여 필터 특성](xref:razor-pages/filter#authorize-filter-attribute)합니다.</span><span class="sxs-lookup"><span data-stu-id="d226a-121">For more information, see [Authorize filter attribute](xref:razor-pages/filter#authorize-filter-attribute).</span></span>

::: moniker-end

## <a name="require-authorization-to-access-a-folder-of-pages"></a><span data-ttu-id="d226a-122">페이지 폴더 액세스 권한 부여 필요</span><span class="sxs-lookup"><span data-stu-id="d226a-122">Require authorization to access a folder of pages</span></span>

<span data-ttu-id="d226a-123">사용 합니다 [AuthorizeFolder](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizefolder) 규칙을 통해 [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) 추가 하는 [AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter) 지정된 된 경로에 폴더에 있는 페이지의 모든:</span><span class="sxs-lookup"><span data-stu-id="d226a-123">Use the [AuthorizeFolder](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizefolder) convention via [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) to add an [AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter) to all of the pages in a folder at the specified path:</span></span>

[!code-csharp[](razor-pages-authorization/samples/2.x/AuthorizationSample/Startup.cs?name=snippet1&highlight=2,5)]

<span data-ttu-id="d226a-124">지정된 된 경로 경로인 뷰 엔진, Razor 페이지 루트 상대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="d226a-124">The specified path is the View Engine path, which is the Razor Pages root relative path.</span></span>

<span data-ttu-id="d226a-125">[AuthorizeFolder 오버 로드](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizefolder#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_AuthorizeFolder_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_String_System_String_) 권한 부여 정책을 지정 해야 하는 경우 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d226a-125">An [AuthorizeFolder overload](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizefolder#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_AuthorizeFolder_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_String_System_String_) is available if you need to specify an authorization policy.</span></span>

::: moniker range=">= aspnetcore-2.1"

## <a name="require-authorization-to-access-an-area-page"></a><span data-ttu-id="d226a-126">영역 페이지에 액세스할 수 있는 인증 필요</span><span class="sxs-lookup"><span data-stu-id="d226a-126">Require authorization to access an area page</span></span>

<span data-ttu-id="d226a-127">사용 하 여는 [AuthorizeAreaPage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizeareapage) 규칙을 통해 [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) 추가 하는 [AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter) 지정 된 경로의 영역 페이지:</span><span class="sxs-lookup"><span data-stu-id="d226a-127">Use the [AuthorizeAreaPage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizeareapage) convention via [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) to add an [AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter) to the area page at the specified path:</span></span>

```csharp
options.Conventions.AuthorizeAreaPage("Identity", "/Manage/Accounts");
```

<span data-ttu-id="d226a-128">페이지 이름은 지정된 된 영역에 대 한 페이지 루트 디렉터리에 상대적인 확장명 없이 파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="d226a-128">The page name is the path of the file without an extension relative to the pages root directory for the specified area.</span></span> <span data-ttu-id="d226a-129">예를 들어 파일의 페이지 이름을 *Areas/Identity/Pages/Manage/Accounts.cshtml* 됩니다 */관리/계정*합니다.</span><span class="sxs-lookup"><span data-stu-id="d226a-129">For example, the page name for the file *Areas/Identity/Pages/Manage/Accounts.cshtml* is */Manage/Accounts*.</span></span>

<span data-ttu-id="d226a-130">[AuthorizeAreaPage 오버 로드](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizeareapage#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_AuthorizeAreaPage_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_String_System_String_System_String_) 권한 부여 정책을 지정 해야 하는 경우 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d226a-130">An [AuthorizeAreaPage overload](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizeareapage#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_AuthorizeAreaPage_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_String_System_String_System_String_) is available if you need to specify an authorization policy.</span></span>

## <a name="require-authorization-to-access-a-folder-of-areas"></a><span data-ttu-id="d226a-131">영역의 폴더 액세스 권한 부여 필요</span><span class="sxs-lookup"><span data-stu-id="d226a-131">Require authorization to access a folder of areas</span></span>

<span data-ttu-id="d226a-132">사용 합니다 [AuthorizeAreaFolder](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizeareafolder) 규칙을 통해 [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) 추가할를 [AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter) 모든 지정된 된 경로에 폴더에서:</span><span class="sxs-lookup"><span data-stu-id="d226a-132">Use the [AuthorizeAreaFolder](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizeareafolder) convention via [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) to add an [AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter) to all of the areas in a folder at the specified path:</span></span>

```csharp
options.Conventions.AuthorizeAreaFolder("Identity", "/Manage");
```

<span data-ttu-id="d226a-133">폴더 경로가 지정된 된 영역에 대 한 페이지 루트 디렉터리에 상대적인 폴더의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="d226a-133">The folder path is the path of the folder relative to the pages root directory for the specified area.</span></span> <span data-ttu-id="d226a-134">예를 들어, 아래에 있는 파일에 대 한 폴더 경로 *영역/Identity/페이지/관리/* 됩니다 */관리*합니다.</span><span class="sxs-lookup"><span data-stu-id="d226a-134">For example, the folder path for the files under *Areas/Identity/Pages/Manage/* is */Manage*.</span></span>

<span data-ttu-id="d226a-135">[AuthorizeAreaFolder 오버 로드](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizeareafolder#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_AuthorizeAreaFolder_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_String_System_String_System_String_) 권한 부여 정책을 지정 해야 하는 경우 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d226a-135">An [AuthorizeAreaFolder overload](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizeareafolder#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_AuthorizeAreaFolder_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_String_System_String_System_String_) is available if you need to specify an authorization policy.</span></span>

::: moniker-end

## <a name="allow-anonymous-access-to-a-page"></a><span data-ttu-id="d226a-136">페이지에 대 한 익명 액세스를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d226a-136">Allow anonymous access to a page</span></span>

<span data-ttu-id="d226a-137">사용 하 여는 [AllowAnonymousToPage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.allowanonymoustopage) 규칙을 통해 [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) 추가 하는 [AllowAnonymousFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.allowanonymousfilter) 지정된 된 경로에 페이지:</span><span class="sxs-lookup"><span data-stu-id="d226a-137">Use the [AllowAnonymousToPage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.allowanonymoustopage) convention via [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) to add an [AllowAnonymousFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.allowanonymousfilter) to a page at the specified path:</span></span>

[!code-csharp[](razor-pages-authorization/samples/2.x/AuthorizationSample/Startup.cs?name=snippet1&highlight=2,6)]

<span data-ttu-id="d226a-138">지정된 된 경로 경로인 뷰 엔진에만 슬래시를 포함 하 고 확장 없이 Razor 페이지 루트 상대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="d226a-138">The specified path is the View Engine path, which is the Razor Pages root relative path without an extension and containing only forward slashes.</span></span>

## <a name="allow-anonymous-access-to-a-folder-of-pages"></a><span data-ttu-id="d226a-139">페이지의 폴더에 대 한 익명 액세스를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d226a-139">Allow anonymous access to a folder of pages</span></span>

<span data-ttu-id="d226a-140">사용 합니다 [AllowAnonymousToFolder](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.allowanonymoustofolder) 규칙을 통해 [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) 추가 하는 [AllowAnonymousFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.allowanonymousfilter) 지정된 된 경로에 폴더에 있는 페이지의 모든:</span><span class="sxs-lookup"><span data-stu-id="d226a-140">Use the [AllowAnonymousToFolder](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.allowanonymoustofolder) convention via [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) to add an [AllowAnonymousFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.allowanonymousfilter) to all of the pages in a folder at the specified path:</span></span>

[!code-csharp[](razor-pages-authorization/samples/2.x/AuthorizationSample/Startup.cs?name=snippet1&highlight=2,7)]

<span data-ttu-id="d226a-141">지정된 된 경로 경로인 뷰 엔진, Razor 페이지 루트 상대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="d226a-141">The specified path is the View Engine path, which is the Razor Pages root relative path.</span></span>

## <a name="note-on-combining-authorized-and-anonymous-access"></a><span data-ttu-id="d226a-142">익명 액세스 및 권한이 결합에 대 한 참고</span><span class="sxs-lookup"><span data-stu-id="d226a-142">Note on combining authorized and anonymous access</span></span>

<span data-ttu-id="d226a-143">페이지 폴더 권한 부여가 필요 하며 해당 폴더 내의 페이지 익명 액세스를 허용 하는지 지정 되도록 지정 하려면 완벽 하 게 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="d226a-143">It's perfectly valid to specify that a folder of pages require authorization and specify that a page within that folder allows anonymous access:</span></span>

```csharp
// This works.
.AuthorizeFolder("/Private").AllowAnonymousToPage("/Private/Public")
```

<span data-ttu-id="d226a-144">그러나 반대의 경우 true 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d226a-144">The reverse, however, isn't true.</span></span> <span data-ttu-id="d226a-145">익명 액세스에 대 한 페이지의 폴더를 선언 하 고 권한 부여를 위해 내에서 페이지를 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d226a-145">You can't declare a folder of pages for anonymous access and specify a page within for authorization:</span></span>

```csharp
// This doesn't work!
.AllowAnonymousToFolder("/Public").AuthorizePage("/Public/Private") 
```

<span data-ttu-id="d226a-146">때문에 작동 하지 않습니다 개인 페이지의 권한 부여를 요구 때 모두를 `AllowAnonymousFilter` 및 `AuthorizeFilter` 필터 페이지에 적용 됩니다는 `AllowAnonymousFilter` wins 및 액세스를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="d226a-146">Requiring authorization on the Private page won't work because when both the `AllowAnonymousFilter` and `AuthorizeFilter` filters are applied to the page, the `AllowAnonymousFilter` wins and controls access.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d226a-147">추가 자료</span><span class="sxs-lookup"><span data-stu-id="d226a-147">Additional resources</span></span>

* [<span data-ttu-id="d226a-148">Razor 페이지 사용자 지정 경로 및 페이지 모델 공급자</span><span class="sxs-lookup"><span data-stu-id="d226a-148">Razor Pages custom route and page model providers</span></span>](xref:razor-pages/razor-pages-conventions)
* <span data-ttu-id="d226a-149">[PageConventionCollection](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection) 클래스</span><span class="sxs-lookup"><span data-stu-id="d226a-149">[PageConventionCollection](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection) class</span></span>
