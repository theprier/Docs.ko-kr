---
title: ASP.NET Core 프로젝트에 스 캐 폴드 Id
author: rick-anderson
description: Identity ASP.NET Core 프로젝트에 스 캐 폴딩 하는 방법에 알아봅니다.
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.date: 5/16/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/authentication/scaffold-identity
ms.openlocfilehash: 7527d3c075fd845ac804d4cfd56469a0679ed7e8
ms.sourcegitcommit: a66f38071e13685bbe59d48d22aa141ac702b432
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/17/2018
---
# <a name="scaffold-identity-in-aspnet-core-projects"></a><span data-ttu-id="b317d-103">ASP.NET Core 프로젝트에 스 캐 폴드 Id</span><span class="sxs-lookup"><span data-stu-id="b317d-103">Scaffold Identity in ASP.NET Core projects</span></span>

<span data-ttu-id="b317d-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="b317d-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="b317d-105">ASP.NET Core 2.1 이상 제공 [ASP.NET Core Id](xref:security/authentication/identity) 로 [Razor 클래스 라이브러리](xref:mvc/razor-pages/ui-class)합니다.</span><span class="sxs-lookup"><span data-stu-id="b317d-105">ASP.NET Core 2.1 and later provides [ASP.NET Core Identity](xref:security/authentication/identity) as a [Razor Class Library](xref:mvc/razor-pages/ui-class).</span></span> <span data-ttu-id="b317d-106">Id가 포함 하는 응용 프로그램에 선택적으로 Identity Razor 클래스 라이브러리 (RCL)에 포함 된 소스 코드를 추가 하려면 scaffolder를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b317d-106">Applications that include Identity can apply the scaffolder to selectively add the source code contained in the Identity Razor Class Library (RCL).</span></span> <span data-ttu-id="b317d-107">코드를 수정 하 고 동작을 변경할 수 있도록 소스 코드를 생성 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b317d-107">You might want to generate source code so you can modify the code and change the behavior.</span></span> <span data-ttu-id="b317d-108">예를 들어 scaffolder 등록에 사용 하 여 코드를 생성 하도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b317d-108">For example, you could instruct the scaffolder to generate the code used in registration.</span></span> <span data-ttu-id="b317d-109">생성 된 코드 Identity RCL에서 동일한 코드 보다 우선합니다.</span><span class="sxs-lookup"><span data-stu-id="b317d-109">Generated code takes precedence over the same code in the Identity RCL.</span></span>

<span data-ttu-id="b317d-110">응용 프로그램을 **하지** 포함 인증 RCL Identity 패키지를 추가 하려면 scaffolder 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b317d-110">Applications that do **not** include authentication can apply the scaffolder to add the RCL Identity package.</span></span> <span data-ttu-id="b317d-111">선택 하는 옵션이 Identity 코드를 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b317d-111">You have the option of selecting Identity code to be generated.</span></span>

<span data-ttu-id="b317d-112">scaffolder 대부분의 필요한 코드를 생성 하지만 프로세스를 완료 하려면 프로젝트를 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b317d-112">Although the scaffolder generates most of the necessary code, you'll have to update your project to complete the process.</span></span> <span data-ttu-id="b317d-113">이 문서는 Identity 스 캐 폴딩 업데이트를 완료 하는 데 필요한 단계에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b317d-113">This document explains the steps needed to complete an Identity scaffolding update.</span></span>

<span data-ttu-id="b317d-114">Identity scaffolder 실행 되는 *ScaffoldingReadme.txt* 파일은 프로젝트 디렉터리에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b317d-114">When the Identity scaffolder is run, a *ScaffoldingReadme.txt* file is created in the project directory.</span></span> <span data-ttu-id="b317d-115">*ScaffoldingReadme.txt* 파일 Identity 스 캐 폴딩 업데이트를 완료 하는 데 필요한에 대 한 일반 지침을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b317d-115">The *ScaffoldingReadme.txt* file contains general instructions on what's need to complete the Identity scaffolding update.</span></span> <span data-ttu-id="b317d-116">이 문서에는 읽기 보다 자세한 설명은 *ScaffoldingReadme.txt* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b317d-116">This document contains more complete instructions than the read the *ScaffoldingReadme.txt* file.</span></span>

<span data-ttu-id="b317d-117">파일 차이 보여 주는 변경 취소를 사용 하면 소스 제어 시스템을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b317d-117">We recommend using a source control system that shows file differences and allows you to back out of changes.</span></span> <span data-ttu-id="b317d-118">Identity scaffolder 실행 한 후 변경 내용을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="b317d-118">Inspect the changes after running the Identity scaffolder.</span></span>

## <a name="scaffold-identity-into-an-empty-project"></a><span data-ttu-id="b317d-119">빈 프로젝트에 스 캐 폴드 identity</span><span class="sxs-lookup"><span data-stu-id="b317d-119">Scaffold identity into an empty project</span></span>

[!INCLUDE[](~/includes/scaffold-identity/id-scaffold-dlg.md)]

<span data-ttu-id="b317d-120">강조 표시 된 다음 호출을 추가 `Startup` 클래스:</span><span class="sxs-lookup"><span data-stu-id="b317d-120">Add the following highlighted calls to the `Startup` class:</span></span>

[!code-csharp[Main](scaffold-identity/sample/StartupEmpty.cs?name=snippet1&highlight=5,20-23)]

[!INCLUDE[](~/includes/scaffold-identity/hsts.md)]

[!INCLUDE[](~/includes/scaffold-identity/migrations.md)]

## <a name="scaffold-identity-into-a-razor-project-without-existing-authorization"></a><span data-ttu-id="b317d-121">기존 인증 없이 Razor 프로젝트에 스 캐 폴드 identity</span><span class="sxs-lookup"><span data-stu-id="b317d-121">Scaffold identity into a Razor project without existing authorization</span></span>

<!--
set projNam=RPnoAuth
set projType=razor
set version=2.1.0-rc1-final

dotnet new %projType% -o %projNam%
cd %projNam%
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design -v %version%
dotnet restore
dotnet aspnet-codegenerator identity --useDefaultUI
dotnet ef migrations add CreateIdentitySchema
dotnet ef database update
-->

[!INCLUDE[](~/includes/scaffold-identity/id-scaffold-dlg.md)]

<span data-ttu-id="b317d-122">id가 구성 *Areas/Identity/IdentityHostingStartup.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="b317d-122">Identity is configured in *Areas/Identity/IdentityHostingStartup.cs*.</span></span> <span data-ttu-id="b317d-123">자세한 내용은 참조 [IHostingStartup](xref:fundamentals/configuration/platform-specific-configuration)합니다.</span><span class="sxs-lookup"><span data-stu-id="b317d-123">for more information, see [IHostingStartup](xref:fundamentals/configuration/platform-specific-configuration).</span></span>

[!INCLUDE[](~/includes/scaffold-identity/migrations.md)]

<span data-ttu-id="b317d-124">에 `Configure` 의 메서드는 `Startup` 클래스, 호출 [UseAuthentication](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_AuthAppBuilderExtensions_UseAuthentication_Microsoft_AspNetCore_Builder_IApplicationBuilder_) 후 `UseStaticFiles`:</span><span class="sxs-lookup"><span data-stu-id="b317d-124">In the `Configure` method of the `Startup` class, call [UseAuthentication](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_AuthAppBuilderExtensions_UseAuthentication_Microsoft_AspNetCore_Builder_IApplicationBuilder_) after `UseStaticFiles`:</span></span>

[!code-csharp[Main](scaffold-identity/sample/StartupRPnoAuth.cs?name=snippet1&highlight=29)]

[!INCLUDE[](~/includes/scaffold-identity/hsts.md)]

### <a name="layout-changes"></a><span data-ttu-id="b317d-125">레이아웃 변경</span><span class="sxs-lookup"><span data-stu-id="b317d-125">Layout changes</span></span>

<span data-ttu-id="b317d-126">선택 사항: 부분 로그인을 추가 (`_LoginPartial`) 레이아웃 파일에:</span><span class="sxs-lookup"><span data-stu-id="b317d-126">Optional: Add the login partial (`_LoginPartial`) to the layout file:</span></span>

[!code-html[Main](scaffold-identity/sample/_Layout.cshtml?highlight=37)]

## <a name="scaffold-identity-into-a-razor-project-with-individual-authorization"></a><span data-ttu-id="b317d-127">개별 권한 부여를 사용 하 여 Razor 프로젝트에 스 캐 폴드 identity</span><span class="sxs-lookup"><span data-stu-id="b317d-127">Scaffold identity into a Razor project with individual authorization</span></span>

<!--
dotnet new razor -au Individual -o RPauth
cd RPauth
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design -v "2.1.0-rc1-final"
dotnet restore
dotnet aspnet-codegenerator identity -dc RPauth.Data.ApplicationDbContext --files Account.Register
-->

[!INCLUDE[](~/includes/scaffold-identity/id-scaffold-dlg-auth.md)]
<span data-ttu-id="b317d-128">일부 Id 옵션에 구성 된 *Areas/Identity/IdentityHostingStartup.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="b317d-128">Some Identity options are configured in *Areas/Identity/IdentityHostingStartup.cs*.</span></span> <span data-ttu-id="b317d-129">자세한 내용은 참조 [IHostingStartup](xref:fundamentals/configuration/platform-specific-configuration)합니다.</span><span class="sxs-lookup"><span data-stu-id="b317d-129">For more information, see [IHostingStartup](xref:fundamentals/configuration/platform-specific-configuration).</span></span>

## <a name="scaffold-identity-into-an-mvc-project-without-existing-authorization"></a><span data-ttu-id="b317d-130">기존 인증 없이 MVC 프로젝트에 스 캐 폴드 identity</span><span class="sxs-lookup"><span data-stu-id="b317d-130">Scaffold identity into an MVC project without existing authorization</span></span>

<!--
set projNam=MvcNoAuth
set projType=mvc
set version=2.1.0-rc1-final

dotnet new %projType% -o %projNam%
cd %projNam%
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design -v %version%
dotnet restore
dotnet aspnet-codegenerator identity --useDefaultUI
dotnet ef migrations add CreateIdentitySchema
dotnet ef database update
-->

[!INCLUDE[](~/includes/scaffold-identity/id-scaffold-dlg.md)]

<span data-ttu-id="b317d-131">선택 사항: 부분 로그인을 추가 (`_LoginPartial`)에 *Views/Shared/_Layout.cshtml* 파일:</span><span class="sxs-lookup"><span data-stu-id="b317d-131">Optional: Add the login partial (`_LoginPartial`) to the *Views/Shared/_Layout.cshtml* file:</span></span>

[!code-html[Main](scaffold-identity/sample/_LayoutMvc.cshtml?highlight=37)]

* <span data-ttu-id="b317d-132">이동 된 *Pages/Shared/_LoginPartial.cshtml* 파일을 *Views/Shared/_LoginPartial.cshtml*</span><span class="sxs-lookup"><span data-stu-id="b317d-132">Move the *Pages/Shared/_LoginPartial.cshtml* file to *Views/Shared/_LoginPartial.cshtml*</span></span>

<span data-ttu-id="b317d-133">id가 구성 *Areas/Identity/IdentityHostingStartup.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="b317d-133">Identity is configured in *Areas/Identity/IdentityHostingStartup.cs*.</span></span> <span data-ttu-id="b317d-134">자세한 내용은 IHostingStartup를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b317d-134">For more information, see IHostingStartup.</span></span>

[!INCLUDE[](~/includes/scaffold-identity/migrations.md)]

<span data-ttu-id="b317d-135">호출 [UseAuthentication](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_AuthAppBuilderExtensions_UseAuthentication_Microsoft_AspNetCore_Builder_IApplicationBuilder_) 후 `UseStaticFiles`:</span><span class="sxs-lookup"><span data-stu-id="b317d-135">Call [UseAuthentication](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_AuthAppBuilderExtensions_UseAuthentication_Microsoft_AspNetCore_Builder_IApplicationBuilder_) after `UseStaticFiles`:</span></span>

[!code-csharp[Main](scaffold-identity/sample/StartupMvcNoAuth.cs?name=snippet1&highlight=23)]

[!INCLUDE[](~/includes/scaffold-identity/hsts.md)]

## <a name="scaffold-identity-into-an-mvc-project-with-individual-authorization"></a><span data-ttu-id="b317d-136">개별 권한 부여를 사용 하는 MVC 프로젝트에 스 캐 폴드 identity</span><span class="sxs-lookup"><span data-stu-id="b317d-136">Scaffold identity into an MVC project with individual authorization</span></span>

<!--
dotnet new mvc -au Individual -o MvcAuth
cd MvcAuth
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design -v "2.1.0-rc1-final"
dotnet restore
dotnet aspnet-codegenerator identity -dc MvcAuth.Data.ApplicationDbContext --files Account.Register
-->

[!INCLUDE[](~/includes/scaffold-identity/id-scaffold-dlg-auth.md)]

<span data-ttu-id="b317d-137">삭제 된 *페이지/공유* 폴더와 해당 폴더의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b317d-137">Delete the *Pages/Shared* folder and the files in that folder.</span></span>
