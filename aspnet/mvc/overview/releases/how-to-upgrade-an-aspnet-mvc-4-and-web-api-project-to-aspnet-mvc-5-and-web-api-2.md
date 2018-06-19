---
uid: mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2
title: 웹 API 프로젝트를 ASP.NET MVC 5 및 Web API 2 및 ASP.NET MVC 4를 업그레이드 하는 방법 | Microsoft Docs
author: Rick-Anderson
description: ASP.NET MVC 5 및 Web API 2의 새로운 기능을 특성이 라우팅, 인증 필터 및 등을 포함 하 여 호스트를 가져옵니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/17/2013
ms.topic: article
ms.assetid: db0d02d9-58e8-4a0b-8d7d-b8df8ea97b88
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: f61502933a5ba92896ee97cef9cff915fe23831d
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30874732"
---
<a name="how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2"></a><span data-ttu-id="afd44-103">ASP.NET MVC 5 및 Web API 2에는 ASP.NET MVC 4 및 Web API 프로젝트를 업그레이드 하는 방법</span><span class="sxs-lookup"><span data-stu-id="afd44-103">How to Upgrade an ASP.NET MVC 4 and Web API Project to ASP.NET MVC 5 and Web API 2</span></span>
====================
<span data-ttu-id="afd44-104">으로 [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="afd44-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="afd44-105">ASP.NET MVC 5 및 Web API 2의 새로운 기능을 특성이 라우팅, 인증 필터 및 등을 포함 하 여 호스트를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-105">ASP.NET MVC 5 and Web API 2 bring a host of new features, including attribute routing, authentication filters, and much more.</span></span> <span data-ttu-id="afd44-106">참조 [ https://www.asp.net/vnext ](https://www.asp.net/core) 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-106">See [https://www.asp.net/vnext](https://www.asp.net/core) for more details.</span></span>
> 
> <span data-ttu-id="afd44-107">이 연습에서는 응용 프로그램에서 최신 버전을 업그레이드 하는 데 필요한 단계를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-107">This walkthrough will guide you with the steps required to upgrade your application to the latest version.</span></span>  
> 
> > [!NOTE]
> > <span data-ttu-id="afd44-108">참조 하십시오 [ASP.NET 및 Web Tools for Visual Studio 2013 릴리스 정보](../../../visual-studio/overview/2013/release-notes.md) 주요 다음 버전으로 MVC 4 및 Web API에서 변경 내용에 대 한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-108">Please see [ASP.NET and Web Tools for Visual Studio 2013 Release Notes](../../../visual-studio/overview/2013/release-notes.md) for information on breaking changes from MVC 4 and Web API to the next version.</span></span>
> 
>   
> 
> <span data-ttu-id="afd44-109">이 문서 Youngjune 홍콩 및 Rick Anderson 썼습니다 ( [ @RickAndMSFT ](https://twitter.com/#!/RickAndMSFT) )</span><span class="sxs-lookup"><span data-stu-id="afd44-109">This article was written by Youngjune Hong and Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) )</span></span>


## <a name="upgrade-steps"></a><span data-ttu-id="afd44-110">업그레이드 단계</span><span class="sxs-lookup"><span data-stu-id="afd44-110">Upgrade Steps</span></span>

1. <span data-ttu-id="afd44-111">프로젝트를 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-111">Backup your project.</span></span> <span data-ttu-id="afd44-112">이 연습에서는 프로젝트 파일, 패키지 구성 및 web.config 파일에 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-112">This walkthrough will require you to make changes to your project file, package configuration, and web.config files.</span></span>
2. <span data-ttu-id="afd44-113">Global.asax의 웹 API에서 Web API 2로 업그레이드 하는 것에 대 한 변경:</span><span class="sxs-lookup"><span data-stu-id="afd44-113">For upgrading from Web API to Web API 2, in global.asax, change:</span></span>

    [!code-csharp[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample1.cs)]

   <span data-ttu-id="afd44-114">다음으로 변경:</span><span class="sxs-lookup"><span data-stu-id="afd44-114">to</span></span>

    [!code-csharp[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample2.cs)]
3. <span data-ttu-id="afd44-115">프로젝트를 사용 하는 모든 패키지 MVC 5 및 Web API 2와 호환 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-115">Make sure all the packages that your projects use are compatible with MVC 5 and Web API 2.</span></span> <span data-ttu-id="afd44-116">다음 표에서 MVC 4 및 Web API 관련 변경 해야 할 보다 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-116">The following table shows the MVC 4 and Web API related packages than need to be changed.</span></span> <span data-ttu-id="afd44-117">아래에 나열 된 패키지 중 하나에 종속 되어 있는 패키지를 사용 하는 경우 MVC 5와 Web API 2와 호환 되는 최신 버전을 가져올 게시자에 게 문의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="afd44-117">If you have a package that is dependent on one of the packages listed below, please contact the publishers to get the newer versions that are compatible with MVC 5 and Web API 2.</span></span> <span data-ttu-id="afd44-118">이러한 패키지에 대 한 소스 코드를 있는 MVC 5와 Web API 2의 새로운 어셈블리와 함께 다시 컴파일합니다 해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-118">If you have the source code for those packages, you should recompile them with the new assemblies of MVC 5 and Web API 2.</span></span>   

    | <span data-ttu-id="afd44-119">**패키지 Id**</span><span class="sxs-lookup"><span data-stu-id="afd44-119">**Package Id**</span></span> | <span data-ttu-id="afd44-120">**이전 버전**</span><span class="sxs-lookup"><span data-stu-id="afd44-120">**Old version**</span></span> | <span data-ttu-id="afd44-121">**새 버전**</span><span class="sxs-lookup"><span data-stu-id="afd44-121">**New version**</span></span> |
    | --- | --- | --- |
    | <span data-ttu-id="afd44-122">Microsoft.AspNet.Razor</span><span class="sxs-lookup"><span data-stu-id="afd44-122">Microsoft.AspNet.Razor</span></span> | <span data-ttu-id="afd44-123">2.0.x.x</span><span class="sxs-lookup"><span data-stu-id="afd44-123">2.0.x.x</span></span> | <span data-ttu-id="afd44-124">3.0.0</span><span class="sxs-lookup"><span data-stu-id="afd44-124">3.0.0</span></span> |
    | <span data-ttu-id="afd44-125">Microsoft.AspNet.WebPages</span><span class="sxs-lookup"><span data-stu-id="afd44-125">Microsoft.AspNet.WebPages</span></span> | <span data-ttu-id="afd44-126">2.0.x.x</span><span class="sxs-lookup"><span data-stu-id="afd44-126">2.0.x.x</span></span> | <span data-ttu-id="afd44-127">3.0.0</span><span class="sxs-lookup"><span data-stu-id="afd44-127">3.0.0</span></span> |
    | <span data-ttu-id="afd44-128">Microsoft.AspNet.WebPages.WebData</span><span class="sxs-lookup"><span data-stu-id="afd44-128">Microsoft.AspNet.WebPages.WebData</span></span> | <span data-ttu-id="afd44-129">2.0.x.x</span><span class="sxs-lookup"><span data-stu-id="afd44-129">2.0.x.x</span></span> | <span data-ttu-id="afd44-130">3.0.0</span><span class="sxs-lookup"><span data-stu-id="afd44-130">3.0.0</span></span> |
    | <span data-ttu-id="afd44-131">Microsoft.AspNet.WebPages.OAuth</span><span class="sxs-lookup"><span data-stu-id="afd44-131">Microsoft.AspNet.WebPages.OAuth</span></span> | <span data-ttu-id="afd44-132">2.0.x.x</span><span class="sxs-lookup"><span data-stu-id="afd44-132">2.0.x.x</span></span> | <span data-ttu-id="afd44-133">3.0.0</span><span class="sxs-lookup"><span data-stu-id="afd44-133">3.0.0</span></span> |
    | <span data-ttu-id="afd44-134">Microsoft.AspNet.Mvc</span><span class="sxs-lookup"><span data-stu-id="afd44-134">Microsoft.AspNet.Mvc</span></span> | <span data-ttu-id="afd44-135">4.0.x.x</span><span class="sxs-lookup"><span data-stu-id="afd44-135">4.0.x.x</span></span> | <span data-ttu-id="afd44-136">5.0.0</span><span class="sxs-lookup"><span data-stu-id="afd44-136">5.0.0</span></span> |
    | <span data-ttu-id="afd44-137">Microsoft.AspNet.Mvc.Facebook</span><span class="sxs-lookup"><span data-stu-id="afd44-137">Microsoft.AspNet.Mvc.Facebook</span></span> | <span data-ttu-id="afd44-138">4.0.x.x</span><span class="sxs-lookup"><span data-stu-id="afd44-138">4.0.x.x</span></span> | <span data-ttu-id="afd44-139">5.0.0</span><span class="sxs-lookup"><span data-stu-id="afd44-139">5.0.0</span></span> |
    | <span data-ttu-id="afd44-140">Microsoft.AspNet.WebApi.Core</span><span class="sxs-lookup"><span data-stu-id="afd44-140">Microsoft.AspNet.WebApi.Core</span></span> | <span data-ttu-id="afd44-141">4.0.x.x</span><span class="sxs-lookup"><span data-stu-id="afd44-141">4.0.x.x</span></span> | <span data-ttu-id="afd44-142">5.0.0</span><span class="sxs-lookup"><span data-stu-id="afd44-142">5.0.0</span></span> |
    | <span data-ttu-id="afd44-143">Microsoft.AspNet.WebApi.SelfHost</span><span class="sxs-lookup"><span data-stu-id="afd44-143">Microsoft.AspNet.WebApi.SelfHost</span></span> | <span data-ttu-id="afd44-144">4.0.x.x</span><span class="sxs-lookup"><span data-stu-id="afd44-144">4.0.x.x</span></span> | <span data-ttu-id="afd44-145">5.0.0</span><span class="sxs-lookup"><span data-stu-id="afd44-145">5.0.0</span></span> |
    | <span data-ttu-id="afd44-146">Microsoft.AspNet.WebApi.Client</span><span class="sxs-lookup"><span data-stu-id="afd44-146">Microsoft.AspNet.WebApi.Client</span></span> | <span data-ttu-id="afd44-147">4.0.x.x</span><span class="sxs-lookup"><span data-stu-id="afd44-147">4.0.x.x</span></span> | <span data-ttu-id="afd44-148">5.0.0</span><span class="sxs-lookup"><span data-stu-id="afd44-148">5.0.0</span></span> |
    | <span data-ttu-id="afd44-149">Microsoft.AspNet.WebApi.OData</span><span class="sxs-lookup"><span data-stu-id="afd44-149">Microsoft.AspNet.WebApi.OData</span></span> | <span data-ttu-id="afd44-150">4.0.x.x</span><span class="sxs-lookup"><span data-stu-id="afd44-150">4.0.x.x</span></span> | <span data-ttu-id="afd44-151">5.0.0</span><span class="sxs-lookup"><span data-stu-id="afd44-151">5.0.0</span></span> |
    | <span data-ttu-id="afd44-152">Microsoft.AspNet.WebApi</span><span class="sxs-lookup"><span data-stu-id="afd44-152">Microsoft.AspNet.WebApi</span></span> | <span data-ttu-id="afd44-153">4.0.x.x</span><span class="sxs-lookup"><span data-stu-id="afd44-153">4.0.x.x</span></span> | <span data-ttu-id="afd44-154">5.0.0</span><span class="sxs-lookup"><span data-stu-id="afd44-154">5.0.0</span></span> |
    | <span data-ttu-id="afd44-155">Microsoft.AspNet.WebApi.WebHost</span><span class="sxs-lookup"><span data-stu-id="afd44-155">Microsoft.AspNet.WebApi.WebHost</span></span> | <span data-ttu-id="afd44-156">4.0.x.x</span><span class="sxs-lookup"><span data-stu-id="afd44-156">4.0.x.x</span></span> | <span data-ttu-id="afd44-157">5.0.0</span><span class="sxs-lookup"><span data-stu-id="afd44-157">5.0.0</span></span> |
    | <span data-ttu-id="afd44-158">Microsoft.AspNet.WebApi.Tracing</span><span class="sxs-lookup"><span data-stu-id="afd44-158">Microsoft.AspNet.WebApi.Tracing</span></span> | <span data-ttu-id="afd44-159">4.0.x.x</span><span class="sxs-lookup"><span data-stu-id="afd44-159">4.0.x.x</span></span> | <span data-ttu-id="afd44-160">5.0.0</span><span class="sxs-lookup"><span data-stu-id="afd44-160">5.0.0</span></span> |
    | <span data-ttu-id="afd44-161">Microsoft.AspNet.WebApi.HelpPage</span><span class="sxs-lookup"><span data-stu-id="afd44-161">Microsoft.AspNet.WebApi.HelpPage</span></span> | <span data-ttu-id="afd44-162">4.0.x.x</span><span class="sxs-lookup"><span data-stu-id="afd44-162">4.0.x.x</span></span> | <span data-ttu-id="afd44-163">5.0.0</span><span class="sxs-lookup"><span data-stu-id="afd44-163">5.0.0</span></span> |
    | <span data-ttu-id="afd44-164">Microsoft.net.http</span><span class="sxs-lookup"><span data-stu-id="afd44-164">Microsoft.Net.Http</span></span> | <span data-ttu-id="afd44-165">2.0.x.</span><span class="sxs-lookup"><span data-stu-id="afd44-165">2.0.x.</span></span> | <span data-ttu-id="afd44-166">2.2.x.</span><span class="sxs-lookup"><span data-stu-id="afd44-166">2.2.x.</span></span> |
    | <span data-ttu-id="afd44-167">Microsoft.Data.OData</span><span class="sxs-lookup"><span data-stu-id="afd44-167">Microsoft.Data.OData</span></span> | <span data-ttu-id="afd44-168">5.2.x</span><span class="sxs-lookup"><span data-stu-id="afd44-168">5.2.x</span></span> | <span data-ttu-id="afd44-169">5.6.x</span><span class="sxs-lookup"><span data-stu-id="afd44-169">5.6.x</span></span> |
    | <span data-ttu-id="afd44-170">System.Spatial</span><span class="sxs-lookup"><span data-stu-id="afd44-170">System.Spatial</span></span> | <span data-ttu-id="afd44-171">5.2.x</span><span class="sxs-lookup"><span data-stu-id="afd44-171">5.2.x</span></span> | <span data-ttu-id="afd44-172">5.6.x</span><span class="sxs-lookup"><span data-stu-id="afd44-172">5.6.x</span></span> |
    | <span data-ttu-id="afd44-173">Microsoft.Data.Edm</span><span class="sxs-lookup"><span data-stu-id="afd44-173">Microsoft.Data.Edm</span></span> | <span data-ttu-id="afd44-174">5.2.x</span><span class="sxs-lookup"><span data-stu-id="afd44-174">5.2.x</span></span> | <span data-ttu-id="afd44-175">5.6.x</span><span class="sxs-lookup"><span data-stu-id="afd44-175">5.6.x</span></span> |
    | <span data-ttu-id="afd44-176">Microsoft.AspNet.Mvc.FixedDisplayModes</span><span class="sxs-lookup"><span data-stu-id="afd44-176">Microsoft.AspNet.Mvc.FixedDisplayModes</span></span> | <span data-ttu-id="afd44-177"><o:p> </o:p></span><span class="sxs-lookup"><span data-stu-id="afd44-177"><o:p> </o:p></span></span> | <span data-ttu-id="afd44-178">제거됨</span><span class="sxs-lookup"><span data-stu-id="afd44-178">Removed</span></span> |
    | <span data-ttu-id="afd44-179">Microsoft.AspNet.WebPages.Administration</span><span class="sxs-lookup"><span data-stu-id="afd44-179">Microsoft.AspNet.WebPages.Administration</span></span> | <span data-ttu-id="afd44-180"><o:p> </o:p></span><span class="sxs-lookup"><span data-stu-id="afd44-180"><o:p> </o:p></span></span> | <span data-ttu-id="afd44-181">제거됨</span><span class="sxs-lookup"><span data-stu-id="afd44-181">Removed</span></span> |
    | <span data-ttu-id="afd44-182">Microsoft-Web-Helpers</span><span class="sxs-lookup"><span data-stu-id="afd44-182">Microsoft-Web-Helpers</span></span> | <span data-ttu-id="afd44-183"><o:p> </o:p></span><span class="sxs-lookup"><span data-stu-id="afd44-183"><o:p> </o:p></span></span> | <span data-ttu-id="afd44-184">Microsoft.AspNet.WebHelpers</span><span class="sxs-lookup"><span data-stu-id="afd44-184">Microsoft.AspNet.WebHelpers</span></span> |

    > [!NOTE]
    > <span data-ttu-id="afd44-185">Microsoft 웹-도우미 Microsoft.AspNet.WebHelpers로 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-185">Microsoft-Web-Helpers has been replaced with Microsoft.AspNet.WebHelpers.</span></span> <span data-ttu-id="afd44-186">먼저, 이전 패키지를 제거 하 여 다음 최신 패키지를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-186">You should remove the old package first, and then install the newer package.</span></span>   
    >   
    > <span data-ttu-id="afd44-187">ASP.NET의 주요 패키지 간에 교차 버전 호환성이 되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-187">There is no cross version compatibility among major ASP.NET packages.</span></span> <span data-ttu-id="afd44-188">예를 들어 MVC 5는 Razor 3 및 Razor 2 하지 호환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-188">For example, MVC 5 is compatible with only Razor 3, and not Razor 2.</span></span>
4. <span data-ttu-id="afd44-189">Visual Studio 2013에서 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-189">Open your project in Visual Studio 2013.</span></span>
5. <span data-ttu-id="afd44-190">설치 된 다음 ASP.NET NuGet 패키지를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-190">Remove any of the following ASP.NET NuGet packages that are installed.</span></span> <span data-ttu-id="afd44-191">패키지 관리자 콘솔 (PMC)를 사용 하 여이 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-191">You will remove these using the Package Manager Console (PMC).</span></span> <span data-ttu-id="afd44-192">PMC를 열려면 선택 된 **도구** 메뉴를 선택 합니다 **라이브러리 패키지 관리자** 다음 선택 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-192">To open the PMC, select the **Tools** menu and then select **Library Package Manager,** then select **Package Manager Console**.</span></span> <span data-ttu-id="afd44-193">프로젝트가이 모두 포함 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-193">Your project might not include all of these.</span></span>

    1. `Microsoft.AspNet.WebPages.Administration`  
   <span data-ttu-id="afd44-194">이 패키지는 MVC 3에서 MVC 4로 업그레이드 하는 경우에 일반적으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-194">This package is typically added when upgrading from MVC 3 to MVC 4.</span></span> <span data-ttu-id="afd44-195">를 제거 하려면의 PMC에서 다음 명령을 실행:</span><span class="sxs-lookup"><span data-stu-id="afd44-195">To remove it, run the following command in the PMC:</span></span>  
        `Uninstall-Package -Id Microsoft.AspNet.WebPages.Administration`
    2. `Microsoft-Web-Helpers`   
   <span data-ttu-id="afd44-196">이 패키지의으로 브랜드가 `Microsoft.AspNet.WebHelpers`합니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-196">This package has been rebranded as `Microsoft.AspNet.WebHelpers`.</span></span> <span data-ttu-id="afd44-197">를 제거 하려면의 PMC에서 다음 명령을 실행:</span><span class="sxs-lookup"><span data-stu-id="afd44-197">To remove it, run the following command in the PMC:</span></span>  
        `Uninstall-Package -Id Microsoft-Web-Helpers`
    3. `Microsoft.AspNet.Mvc.FixedDisplayMode`  
   <span data-ttu-id="afd44-198">이 패키지의 MVC 4 MVC 5에서 수정 된 버그에 대 한 해결을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-198">This package contains a work around for a bug in MVC 4 that has been fixed in MVC 5.</span></span> <span data-ttu-id="afd44-199">를 제거 하려면의 PMC에서 다음 명령을 실행:</span><span class="sxs-lookup"><span data-stu-id="afd44-199">To remove it, run the following command in the PMC:</span></span>  
        `Uninstall-Package -Id Microsoft.AspNet.Mvc.FixedDisplayModes`
6. <span data-ttu-id="afd44-200">PMC를 사용 하 여 모든 ASP.NET NuGet 패키지를 업그레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-200">Upgrade all the ASP.NET NuGet packages using the PMC.</span></span> <span data-ttu-id="afd44-201">PMC에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-201">In the PMC, run the following command:</span></span>  
    `Update-Package`  
   <span data-ttu-id="afd44-202">`Update-Package` 명령 없이 매개 변수는 모든 패키지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-202">The `Update-Package` command without any parameters will update every package.</span></span> <span data-ttu-id="afd44-203">패키지 ID 인수를 사용 하 여 개별적으로 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-203">You can update packages individually by using the ID argument.</span></span> <span data-ttu-id="afd44-204">업데이트 명령에 대 한 자세한 내용은 실행 `get-help update-package` 합니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-204">For more information about the update command, run     `get-help update-package` .</span></span>

## <a name="update-the-application-webconfig-file"></a><span data-ttu-id="afd44-205">응용 프로그램을 업데이트 *web.config* 파일</span><span class="sxs-lookup"><span data-stu-id="afd44-205">Update the Application *web.config* File</span></span>

<span data-ttu-id="afd44-206">응용 프로그램에서 이러한 변경을 수행 해야 *web.config* 파일 없습니다는 *web.config* 파일에 *뷰* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-206">Be sure to make these changes in the app *web.config* file, not the *web.config* file in the *Views* folder.</span></span>

<span data-ttu-id="afd44-207">찾은 `<runtime>/<assemblyBinding>` 섹션 및 다음과 같이 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-207">Locate the `<runtime>/<assemblyBinding>` section, and make the following changes:</span></span>

1. <span data-ttu-id="afd44-208">이름 특성이 "System.Web.Mvc" 요소에서 "5.0.0.0"를 "4.0.0.0"에서 버전 번호를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-208">In the elements with the name attribute "System.Web.Mvc", change the version number from "4.0.0.0" to "5.0.0.0".</span></span> <span data-ttu-id="afd44-209">(해당 요소에서 두 변경 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="afd44-209">(Two changes in that element.)</span></span>
2. <span data-ttu-id="afd44-210">Name 특성을 사용 하 여 요소에서 &quot;System.Web.Helpers "및 &quot;System.Web.WebPages&quot; "3.0.0.0 "를"2.0.0.0"에서 버전 번호를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-210">In elements with the name attribute &quot;System.Web.Helpers" and &quot;System.Web.WebPages&quot; change the version number from "2.0.0.0" to "3.0.0.0".</span></span> <span data-ttu-id="afd44-211">4 개의 변경 내용은 적용 되며의 각 요소에 두 대.</span><span class="sxs-lookup"><span data-stu-id="afd44-211">Four changes will occur, two in each of the elements.</span></span>

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample3.xml?highlight=6,10,14)]
3. <span data-ttu-id="afd44-212">찾은 `<appSettings>` 섹션 및 다음과 같이 3.0.0.0에 대 한 2.0.0.0.0 webpages:version 업데이트:</span><span class="sxs-lookup"><span data-stu-id="afd44-212">Locate the `<appSettings>` section and update the webpages:version from 2.0.0.0.0 to 3.0.0.0 as shown below:</span></span>

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample4.xml?highlight=2)]
4. <span data-ttu-id="afd44-213">전체 이외의 모든 신뢰 수준을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-213">Remove any trust levels other than Full.</span></span> <span data-ttu-id="afd44-214">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="afd44-214">For example:</span></span>

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample5.xml?highlight=2)]

## <a name="update-the-webconfig-files-under-the-views-folder"></a><span data-ttu-id="afd44-215">업데이트는 *web.config* Views 폴더 아래에 있는 파일</span><span class="sxs-lookup"><span data-stu-id="afd44-215">Update the *web.config* files under the Views folder</span></span>

<span data-ttu-id="afd44-216">응용 프로그램 영역을 사용 하는 경우 각 업데이트 해야 합니다 *web.config* 파일에 *뷰* 각 영역 폴더의 하위 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-216">If your application is using areas, you will also need to update each *web.config* file in the *Views* sub-folder of each Area folder.</span></span>

1. <span data-ttu-id="afd44-217">버전 "5.0.0.0" 버전 "4.0.0.0"에서 "System.Web.Mvc"를 포함 하는 모든 요소를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-217">Update all elements that contain "System.Web.Mvc" from version "4.0.0.0" to version "5.0.0.0".</span></span>  

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample6.xml?highlight=2)]

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample7.xml?highlight=4-6,8)]
2. <span data-ttu-id="afd44-218">버전 "3.0.0.0" 버전 "2.0.0.0"에서 "system.web.webpages.razor"를 포함을 포함 하는 모든 요소를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-218">Update all elements that contain "System.Web.WebPages.Razor" from version "2.0.0.0" to version"3.0.0.0".</span></span> <span data-ttu-id="afd44-219">이 섹션에 "System.Web.WebPages"이 있으면 해당 요소에서 버전 "2.0.0.0" 버전 "3.0.0.0"를 업데이트</span><span class="sxs-lookup"><span data-stu-id="afd44-219">If this section contains "System.Web.WebPages", update those elements from version "2.0.0.0" to version"3.0.0.0"</span></span>  

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample8.xml?highlight=3-5)]
3. <span data-ttu-id="afd44-220">제거한 경우는 `Microsoft-Web-Helpers` 이전 단계에서 NuGet 패키지 설치 `Microsoft.AspNet.WebHelpers` 의 PMC에서 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-220">If you removed the `Microsoft-Web-Helpers` NuGet package in a previous step, install `Microsoft.AspNet.WebHelpers` with the following command in the PMC:</span></span>  
    `Install-Package -Id Microsoft.AspNet.WebHelpers`
4. <span data-ttu-id="afd44-221">앱에서 사용 하는 경우는 [User.IsInRole()](https://msdn.microsoft.com/en-us/library/system.web.security.roleprincipal.isinrole(v=vs.110).aspx) 메서드를 추가 하려면 다음을는 *Web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-221">If your app uses the [User.IsInRole()](https://msdn.microsoft.com/en-us/library/system.web.security.roleprincipal.isinrole(v=vs.110).aspx) method, add the following to the *Web.config* file.</span></span>

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample9.xml)]

## <a name="final-steps"></a><span data-ttu-id="afd44-222">마지막 단계는</span><span class="sxs-lookup"><span data-stu-id="afd44-222">Final Steps</span></span>

<span data-ttu-id="afd44-223">빌드하고 응용 프로그램을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-223">Build and test the application.</span></span>

<span data-ttu-id="afd44-224">프로젝트 파일에서 MVC 4 프로젝트 형식 GUID를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-224">Remove the MVC 4 project type GUID from the project files.</span></span>

1. <span data-ttu-id="afd44-225">솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 한 다음 선택 **프로젝트 언로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-225">In Solution Explorer, right-click the project name and then select **Unload Project**.</span></span>
2. <span data-ttu-id="afd44-226">프로젝트를 마우스 오른쪽 단추로 클릭 하 고 편집 ProjectName.csproj를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-226">Right-click the project and select Edit ProjectName.csproj.</span></span>
3. <span data-ttu-id="afd44-227">찾을 `ProjectTypeGuids` 요소를 선택한 다음 제거 MVC 4 프로젝트 GUID, `{E3E379DF-F4C6-4180-9B81-6769533ABE47}`합니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-227">Locate the `ProjectTypeGuids` element and then remove the MVC 4 project GUID, `{E3E379DF-F4C6-4180-9B81-6769533ABE47}`.</span></span>
4. <span data-ttu-id="afd44-228">저장 하 고 현재 열려 있는 프로젝트 파일을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-228">Save and close the open project file.</span></span>
5. <span data-ttu-id="afd44-229">프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **프로젝트 다시 로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="afd44-229">Right-click the project and select **Reload Project**.</span></span>
