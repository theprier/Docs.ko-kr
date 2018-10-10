---
uid: mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2
title: 웹 API 프로젝트를 ASP.NET MVC 5 및 Web API 2 및 ASP.NET MVC 4를 업그레이드 하는 방법 | Microsoft Docs
author: Rick-Anderson
description: ASP.NET MVC 5 및 Web API 2 호스트 특성 라우팅, 인증 필터 및 등을 포함 하 여 새 기능을 제공 합니다.
ms.author: riande
ms.date: 10/17/2013
ms.assetid: db0d02d9-58e8-4a0b-8d7d-b8df8ea97b88
msc.legacyurl: /mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: 2566e201e44ccd9642abda7c7996056c73178fd6
ms.sourcegitcommit: a4dcca4f1cb81227c5ed3c92dc0e28be6e99447b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2018
ms.locfileid: "48912854"
---
<a name="how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2"></a><span data-ttu-id="1c807-103">ASP.NET MVC 5 및 Web API 2에는 ASP.NET MVC 4 및 Web API 프로젝트를 업그레이드 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1c807-103">How to Upgrade an ASP.NET MVC 4 and Web API Project to ASP.NET MVC 5 and Web API 2</span></span>
====================
<span data-ttu-id="1c807-104">[Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="1c807-104">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

> <span data-ttu-id="1c807-105">ASP.NET MVC 5 및 Web API 2 호스트 특성 라우팅, 인증 필터 및 등을 포함 하 여 새 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-105">ASP.NET MVC 5 and Web API 2 bring a host of new features, including attribute routing, authentication filters, and much more.</span></span> <span data-ttu-id="1c807-106">참조 [ https://www.asp.net/vnext ](https://www.asp.net/core) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-106">See [https://www.asp.net/vnext](https://www.asp.net/core) for more details.</span></span>
> 
> <span data-ttu-id="1c807-107">이 연습에서는 최신 버전으로 응용 프로그램을 업그레이드 하는 데 필요한 단계를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-107">This walkthrough will guide you with the steps required to upgrade your application to the latest version.</span></span>  
> 
> > [!NOTE]
> > <span data-ttu-id="1c807-108">참조 하세요 [ASP.NET 및 Web Tools for Visual Studio 2013 릴리스 정보](../../../visual-studio/overview/2013/release-notes.md) 주요 MVC 4 및 Web API에서 다음 버전의 변경 내용에 대 한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-108">Please see [ASP.NET and Web Tools for Visual Studio 2013 Release Notes](../../../visual-studio/overview/2013/release-notes.md) for information on breaking changes from MVC 4 and Web API to the next version.</span></span>
> 
>   
> 
> <span data-ttu-id="1c807-109">이 문서는 Youngjune 홍콩 및 Rick Anderson으로 작성 되었습니다 ( [ @RickAndMSFT ](https://twitter.com/#!/RickAndMSFT) )</span><span class="sxs-lookup"><span data-stu-id="1c807-109">This article was written by Youngjune Hong and Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) )</span></span>


## <a name="upgrade-steps"></a><span data-ttu-id="1c807-110">업그레이드 단계</span><span class="sxs-lookup"><span data-stu-id="1c807-110">Upgrade Steps</span></span>

1. <span data-ttu-id="1c807-111">프로젝트를 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-111">Backup your project.</span></span> <span data-ttu-id="1c807-112">이 연습에서는 프로젝트 파일, 패키지 구성 및 web.config 파일에 변경 가능 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-112">This walkthrough will require you to make changes to your project file, package configuration, and web.config files.</span></span>
2. <span data-ttu-id="1c807-113">Global.asax의 Web API에서 Web API 2로 업그레이드를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-113">For upgrading from Web API to Web API 2, in global.asax, change:</span></span>

    [!code-csharp[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample1.cs)]

   <span data-ttu-id="1c807-114">다음으로 변경:</span><span class="sxs-lookup"><span data-stu-id="1c807-114">to</span></span>

    [!code-csharp[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample2.cs)]
3. <span data-ttu-id="1c807-115">프로젝트를 사용 하는 모든 패키지 MVC 5 및 Web API 2와 호환 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-115">Make sure all the packages that your projects use are compatible with MVC 5 and Web API 2.</span></span> <span data-ttu-id="1c807-116">다음 테이블에서는 MVC 4 및 Web API를 변경 해야 하는 보다 패키지와 관련 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-116">The following table shows the MVC 4 and Web API related packages than need to be changed.</span></span> <span data-ttu-id="1c807-117">아래에 나열 된 패키지 중 하나에 종속 된 패키지에 있는 MVC 5 및 Web API 2와 호환 되는 최신 버전을 가져오는 게시자에 게 문의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="1c807-117">If you have a package that is dependent on one of the packages listed below, please contact the publishers to get the newer versions that are compatible with MVC 5 and Web API 2.</span></span> <span data-ttu-id="1c807-118">해당 패키지에 대 한 소스 코드가 있는 MVC 5 및 Web API 2의 새로운 어셈블리와 함께 다시 컴파일합니다 해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-118">If you have the source code for those packages, you should recompile them with the new assemblies of MVC 5 and Web API 2.</span></span>   

    | <span data-ttu-id="1c807-119">**패키지 Id**</span><span class="sxs-lookup"><span data-stu-id="1c807-119">**Package Id**</span></span> | <span data-ttu-id="1c807-120">**이전 버전**</span><span class="sxs-lookup"><span data-stu-id="1c807-120">**Old version**</span></span> | <span data-ttu-id="1c807-121">**새 버전**</span><span class="sxs-lookup"><span data-stu-id="1c807-121">**New version**</span></span> |
    | --- | --- | --- |
    | <span data-ttu-id="1c807-122">Microsoft.AspNet.Razor</span><span class="sxs-lookup"><span data-stu-id="1c807-122">Microsoft.AspNet.Razor</span></span> | <span data-ttu-id="1c807-123">2.0.x.x</span><span class="sxs-lookup"><span data-stu-id="1c807-123">2.0.x.x</span></span> | <span data-ttu-id="1c807-124">3.0.0</span><span class="sxs-lookup"><span data-stu-id="1c807-124">3.0.0</span></span> |
    | <span data-ttu-id="1c807-125">Microsoft.AspNet.WebPages</span><span class="sxs-lookup"><span data-stu-id="1c807-125">Microsoft.AspNet.WebPages</span></span> | <span data-ttu-id="1c807-126">2.0.x.x</span><span class="sxs-lookup"><span data-stu-id="1c807-126">2.0.x.x</span></span> | <span data-ttu-id="1c807-127">3.0.0</span><span class="sxs-lookup"><span data-stu-id="1c807-127">3.0.0</span></span> |
    | <span data-ttu-id="1c807-128">Microsoft.AspNet.WebPages.WebData</span><span class="sxs-lookup"><span data-stu-id="1c807-128">Microsoft.AspNet.WebPages.WebData</span></span> | <span data-ttu-id="1c807-129">2.0.x.x</span><span class="sxs-lookup"><span data-stu-id="1c807-129">2.0.x.x</span></span> | <span data-ttu-id="1c807-130">3.0.0</span><span class="sxs-lookup"><span data-stu-id="1c807-130">3.0.0</span></span> |
    | <span data-ttu-id="1c807-131">Microsoft.AspNet.WebPages.OAuth</span><span class="sxs-lookup"><span data-stu-id="1c807-131">Microsoft.AspNet.WebPages.OAuth</span></span> | <span data-ttu-id="1c807-132">2.0.x.x</span><span class="sxs-lookup"><span data-stu-id="1c807-132">2.0.x.x</span></span> | <span data-ttu-id="1c807-133">3.0.0</span><span class="sxs-lookup"><span data-stu-id="1c807-133">3.0.0</span></span> |
    | <span data-ttu-id="1c807-134">Microsoft.AspNet.Mvc</span><span class="sxs-lookup"><span data-stu-id="1c807-134">Microsoft.AspNet.Mvc</span></span> | <span data-ttu-id="1c807-135">4.0.x.x</span><span class="sxs-lookup"><span data-stu-id="1c807-135">4.0.x.x</span></span> | <span data-ttu-id="1c807-136">5.0.0</span><span class="sxs-lookup"><span data-stu-id="1c807-136">5.0.0</span></span> |
    | <span data-ttu-id="1c807-137">Microsoft.AspNet.Mvc.Facebook</span><span class="sxs-lookup"><span data-stu-id="1c807-137">Microsoft.AspNet.Mvc.Facebook</span></span> | <span data-ttu-id="1c807-138">4.0.x.x</span><span class="sxs-lookup"><span data-stu-id="1c807-138">4.0.x.x</span></span> | <span data-ttu-id="1c807-139">5.0.0</span><span class="sxs-lookup"><span data-stu-id="1c807-139">5.0.0</span></span> |
    | <span data-ttu-id="1c807-140">Microsoft.AspNet.WebApi.Core</span><span class="sxs-lookup"><span data-stu-id="1c807-140">Microsoft.AspNet.WebApi.Core</span></span> | <span data-ttu-id="1c807-141">4.0.x.x</span><span class="sxs-lookup"><span data-stu-id="1c807-141">4.0.x.x</span></span> | <span data-ttu-id="1c807-142">5.0.0</span><span class="sxs-lookup"><span data-stu-id="1c807-142">5.0.0</span></span> |
    | <span data-ttu-id="1c807-143">Microsoft.AspNet.WebApi.SelfHost</span><span class="sxs-lookup"><span data-stu-id="1c807-143">Microsoft.AspNet.WebApi.SelfHost</span></span> | <span data-ttu-id="1c807-144">4.0.x.x</span><span class="sxs-lookup"><span data-stu-id="1c807-144">4.0.x.x</span></span> | <span data-ttu-id="1c807-145">5.0.0</span><span class="sxs-lookup"><span data-stu-id="1c807-145">5.0.0</span></span> |
    | <span data-ttu-id="1c807-146">Microsoft.AspNet.WebApi.Client</span><span class="sxs-lookup"><span data-stu-id="1c807-146">Microsoft.AspNet.WebApi.Client</span></span> | <span data-ttu-id="1c807-147">4.0.x.x</span><span class="sxs-lookup"><span data-stu-id="1c807-147">4.0.x.x</span></span> | <span data-ttu-id="1c807-148">5.0.0</span><span class="sxs-lookup"><span data-stu-id="1c807-148">5.0.0</span></span> |
    | <span data-ttu-id="1c807-149">Microsoft.AspNet.WebApi.OData</span><span class="sxs-lookup"><span data-stu-id="1c807-149">Microsoft.AspNet.WebApi.OData</span></span> | <span data-ttu-id="1c807-150">4.0.x.x</span><span class="sxs-lookup"><span data-stu-id="1c807-150">4.0.x.x</span></span> | <span data-ttu-id="1c807-151">5.0.0</span><span class="sxs-lookup"><span data-stu-id="1c807-151">5.0.0</span></span> |
    | <span data-ttu-id="1c807-152">Microsoft.AspNet.WebApi</span><span class="sxs-lookup"><span data-stu-id="1c807-152">Microsoft.AspNet.WebApi</span></span> | <span data-ttu-id="1c807-153">4.0.x.x</span><span class="sxs-lookup"><span data-stu-id="1c807-153">4.0.x.x</span></span> | <span data-ttu-id="1c807-154">5.0.0</span><span class="sxs-lookup"><span data-stu-id="1c807-154">5.0.0</span></span> |
    | <span data-ttu-id="1c807-155">Microsoft.AspNet.WebApi.WebHost</span><span class="sxs-lookup"><span data-stu-id="1c807-155">Microsoft.AspNet.WebApi.WebHost</span></span> | <span data-ttu-id="1c807-156">4.0.x.x</span><span class="sxs-lookup"><span data-stu-id="1c807-156">4.0.x.x</span></span> | <span data-ttu-id="1c807-157">5.0.0</span><span class="sxs-lookup"><span data-stu-id="1c807-157">5.0.0</span></span> |
    | <span data-ttu-id="1c807-158">Microsoft.AspNet.WebApi.Tracing</span><span class="sxs-lookup"><span data-stu-id="1c807-158">Microsoft.AspNet.WebApi.Tracing</span></span> | <span data-ttu-id="1c807-159">4.0.x.x</span><span class="sxs-lookup"><span data-stu-id="1c807-159">4.0.x.x</span></span> | <span data-ttu-id="1c807-160">5.0.0</span><span class="sxs-lookup"><span data-stu-id="1c807-160">5.0.0</span></span> |
    | <span data-ttu-id="1c807-161">Microsoft.AspNet.WebApi.HelpPage</span><span class="sxs-lookup"><span data-stu-id="1c807-161">Microsoft.AspNet.WebApi.HelpPage</span></span> | <span data-ttu-id="1c807-162">4.0.x.x</span><span class="sxs-lookup"><span data-stu-id="1c807-162">4.0.x.x</span></span> | <span data-ttu-id="1c807-163">5.0.0</span><span class="sxs-lookup"><span data-stu-id="1c807-163">5.0.0</span></span> |
    | <span data-ttu-id="1c807-164">Microsoft.net.http</span><span class="sxs-lookup"><span data-stu-id="1c807-164">Microsoft.Net.Http</span></span> | <span data-ttu-id="1c807-165">2.0.x.</span><span class="sxs-lookup"><span data-stu-id="1c807-165">2.0.x.</span></span> | <span data-ttu-id="1c807-166">2.2.x.</span><span class="sxs-lookup"><span data-stu-id="1c807-166">2.2.x.</span></span> |
    | <span data-ttu-id="1c807-167">Microsoft.Data.OData</span><span class="sxs-lookup"><span data-stu-id="1c807-167">Microsoft.Data.OData</span></span> | <span data-ttu-id="1c807-168">5.2.x</span><span class="sxs-lookup"><span data-stu-id="1c807-168">5.2.x</span></span> | <span data-ttu-id="1c807-169">5.6.x</span><span class="sxs-lookup"><span data-stu-id="1c807-169">5.6.x</span></span> |
    | <span data-ttu-id="1c807-170">System.Spatial</span><span class="sxs-lookup"><span data-stu-id="1c807-170">System.Spatial</span></span> | <span data-ttu-id="1c807-171">5.2.x</span><span class="sxs-lookup"><span data-stu-id="1c807-171">5.2.x</span></span> | <span data-ttu-id="1c807-172">5.6.x</span><span class="sxs-lookup"><span data-stu-id="1c807-172">5.6.x</span></span> |
    | <span data-ttu-id="1c807-173">Microsoft.Data.Edm</span><span class="sxs-lookup"><span data-stu-id="1c807-173">Microsoft.Data.Edm</span></span> | <span data-ttu-id="1c807-174">5.2.x</span><span class="sxs-lookup"><span data-stu-id="1c807-174">5.2.x</span></span> | <span data-ttu-id="1c807-175">5.6.x</span><span class="sxs-lookup"><span data-stu-id="1c807-175">5.6.x</span></span> |
    | <span data-ttu-id="1c807-176">Microsoft.AspNet.Mvc.FixedDisplayModes</span><span class="sxs-lookup"><span data-stu-id="1c807-176">Microsoft.AspNet.Mvc.FixedDisplayModes</span></span> | <span data-ttu-id="1c807-177">< 된 >< / 된 ></span><span class="sxs-lookup"><span data-stu-id="1c807-177"><o:p> </o:p></span></span> | <span data-ttu-id="1c807-178">제거됨</span><span class="sxs-lookup"><span data-stu-id="1c807-178">Removed</span></span> |
    | <span data-ttu-id="1c807-179">Microsoft.AspNet.WebPages.Administration</span><span class="sxs-lookup"><span data-stu-id="1c807-179">Microsoft.AspNet.WebPages.Administration</span></span> | <span data-ttu-id="1c807-180">< 된 >< / 된 ></span><span class="sxs-lookup"><span data-stu-id="1c807-180"><o:p> </o:p></span></span> | <span data-ttu-id="1c807-181">제거됨</span><span class="sxs-lookup"><span data-stu-id="1c807-181">Removed</span></span> |
    | <span data-ttu-id="1c807-182">Microsoft-Web-Helpers</span><span class="sxs-lookup"><span data-stu-id="1c807-182">Microsoft-Web-Helpers</span></span> | <span data-ttu-id="1c807-183">< 된 >< / 된 ></span><span class="sxs-lookup"><span data-stu-id="1c807-183"><o:p> </o:p></span></span> | <span data-ttu-id="1c807-184">Microsoft.AspNet.WebHelpers</span><span class="sxs-lookup"><span data-stu-id="1c807-184">Microsoft.AspNet.WebHelpers</span></span> |

    > [!NOTE]
    > <span data-ttu-id="1c807-185">Microsoft-웹-도우미 Microsoft.AspNet.WebHelpers 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-185">Microsoft-Web-Helpers has been replaced with Microsoft.AspNet.WebHelpers.</span></span> <span data-ttu-id="1c807-186">이전 패키지를 먼저 제거 하 고 최신 패키지를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-186">You should remove the old package first, and then install the newer package.</span></span>   
    >   
    > <span data-ttu-id="1c807-187">주요 ASP.NET 패키지 간에 교차 버전 모드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-187">There is no cross version compatibility among major ASP.NET packages.</span></span> <span data-ttu-id="1c807-188">예를 들어 MVC 5와 호환 되만 3 Razor, Razor 2 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-188">For example, MVC 5 is compatible with only Razor 3, and not Razor 2.</span></span>
4. <span data-ttu-id="1c807-189">Visual Studio에서 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-189">Open your project in Visual Studio.</span></span>
5. <span data-ttu-id="1c807-190">설치 된 다음 ASP.NET NuGet 패키지를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-190">Remove any of the following ASP.NET NuGet packages that are installed.</span></span> <span data-ttu-id="1c807-191">(PMC (패키지 관리자 콘솔)를 사용 하 여 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-191">You will remove these using the Package Manager Console (PMC).</span></span> <span data-ttu-id="1c807-192">PMC를 열려면 선택 합니다 **도구** 메뉴를 선택 합니다 **NuGet 패키지 관리자** 선택한 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-192">To open the PMC, select the **Tools** menu and then select **NuGet Package Manager,** then select **Package Manager Console**.</span></span> <span data-ttu-id="1c807-193">프로젝트가이 모두를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-193">Your project might not include all of these.</span></span>

    1. `Microsoft.AspNet.WebPages.Administration`  
   <span data-ttu-id="1c807-194">이 패키지는 MVC 3에서 MVC 4로 업그레이드 하는 경우에 일반적으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-194">This package is typically added when upgrading from MVC 3 to MVC 4.</span></span> <span data-ttu-id="1c807-195">를 제거 하려면 PMC에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-195">To remove it, run the following command in the PMC:</span></span>  
        `Uninstall-Package -Id Microsoft.AspNet.WebPages.Administration`
    2. `Microsoft-Web-Helpers`   
   <span data-ttu-id="1c807-196">으로이 패키지의 브랜드가 `Microsoft.AspNet.WebHelpers`합니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-196">This package has been rebranded as `Microsoft.AspNet.WebHelpers`.</span></span> <span data-ttu-id="1c807-197">를 제거 하려면 PMC에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-197">To remove it, run the following command in the PMC:</span></span>  
        `Uninstall-Package -Id Microsoft-Web-Helpers`
    3. `Microsoft.AspNet.Mvc.FixedDisplayMode`  
   <span data-ttu-id="1c807-198">이 패키지는 MVC 5에서 해결 되었으며 MVC 4의 버그 해결을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-198">This package contains a work around for a bug in MVC 4 that has been fixed in MVC 5.</span></span> <span data-ttu-id="1c807-199">를 제거 하려면 PMC에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-199">To remove it, run the following command in the PMC:</span></span>  
        `Uninstall-Package -Id Microsoft.AspNet.Mvc.FixedDisplayModes`
6. <span data-ttu-id="1c807-200">PMC를 사용 하 여 모든 ASP.NET NuGet 패키지를 업그레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-200">Upgrade all the ASP.NET NuGet packages using the PMC.</span></span> <span data-ttu-id="1c807-201">PMC에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-201">In the PMC, run the following command:</span></span>  
    `Update-Package`  
   <span data-ttu-id="1c807-202">`Update-Package` 명령을 매개 변수는 모든 패키지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-202">The `Update-Package` command without any parameters will update every package.</span></span> <span data-ttu-id="1c807-203">ID 인수를 사용 하 여 패키지를 개별적으로 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-203">You can update packages individually by using the ID argument.</span></span> <span data-ttu-id="1c807-204">업데이트 명령에 대 한 자세한 내용은 실행 `get-help update-package` 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-204">For more information about the update command, run     `get-help update-package` .</span></span>

## <a name="update-the-application-webconfig-file"></a><span data-ttu-id="1c807-205">응용 프로그램을 업데이트 *web.config* 파일</span><span class="sxs-lookup"><span data-stu-id="1c807-205">Update the Application *web.config* File</span></span>

<span data-ttu-id="1c807-206">앱에서 이러한 변경을 수행 해야 *web.config* 파일을 하지는 *web.config* 파일을 *뷰* 폴더.</span><span class="sxs-lookup"><span data-stu-id="1c807-206">Be sure to make these changes in the app *web.config* file, not the *web.config* file in the *Views* folder.</span></span>

<span data-ttu-id="1c807-207">찾을 `<runtime>/<assemblyBinding>` 섹션을 다음과 같이 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-207">Locate the `<runtime>/<assemblyBinding>` section, and make the following changes:</span></span>

1. <span data-ttu-id="1c807-208">이름 특성이 "System.Web.Mvc" 요소를 "5.0.0.0"를 "4.0.0.0"에서 버전 번호를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-208">In the elements with the name attribute "System.Web.Mvc", change the version number from "4.0.0.0" to "5.0.0.0".</span></span> <span data-ttu-id="1c807-209">(해당 요소에서 두 가지 변경 합니다.)</span><span class="sxs-lookup"><span data-stu-id="1c807-209">(Two changes in that element.)</span></span>
2. <span data-ttu-id="1c807-210">요소의 name 특성을 사용 하 여 &quot;System.Web.Helpers "하 고 &quot;System.Web.WebPages&quot; "3.0.0.0 "를"2.0.0.0"에서 버전 번호를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-210">In elements with the name attribute &quot;System.Web.Helpers" and &quot;System.Web.WebPages&quot; change the version number from "2.0.0.0" to "3.0.0.0".</span></span> <span data-ttu-id="1c807-211">4 개의 변경 내용 발생의 각 요소에 두.</span><span class="sxs-lookup"><span data-stu-id="1c807-211">Four changes will occur, two in each of the elements.</span></span>

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample3.xml?highlight=6,10,14)]
3. <span data-ttu-id="1c807-212">찾을 `<appSettings>` 섹션 하 고 아래와 같이 3.0.0.0 2.0.0.0.0에서 webpages:version 업데이트:</span><span class="sxs-lookup"><span data-stu-id="1c807-212">Locate the `<appSettings>` section and update the webpages:version from 2.0.0.0.0 to 3.0.0.0 as shown below:</span></span>

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample4.xml?highlight=2)]
4. <span data-ttu-id="1c807-213">전체 이외의 모든 신뢰 수준을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-213">Remove any trust levels other than Full.</span></span> <span data-ttu-id="1c807-214">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="1c807-214">For example:</span></span>

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample5.xml?highlight=2)]

## <a name="update-the-webconfig-files-under-the-views-folder"></a><span data-ttu-id="1c807-215">업데이트를 *web.config* Views 폴더 아래에 있는 파일</span><span class="sxs-lookup"><span data-stu-id="1c807-215">Update the *web.config* files under the Views folder</span></span>

<span data-ttu-id="1c807-216">응용 프로그램 영역을 사용 하는 경우에 각 업데이트 해야 수도 *web.config* 파일을 *뷰* 각 Area 폴더의 하위 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-216">If your application is using areas, you will also need to update each *web.config* file in the *Views* sub-folder of each Area folder.</span></span>

1. <span data-ttu-id="1c807-217">버전 "5.0.0.0" 버전 "4.0.0.0"에서 "System.Web.Mvc"를 포함 하는 모든 요소를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-217">Update all elements that contain "System.Web.Mvc" from version "4.0.0.0" to version "5.0.0.0".</span></span>  

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample6.xml?highlight=2)]

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample7.xml?highlight=4-6,8)]
2. <span data-ttu-id="1c807-218">버전 "3.0.0.0" 버전 "2.0.0.0"에서 "system.web.webpages.razor"를 포함을 포함 하는 모든 요소를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-218">Update all elements that contain "System.Web.WebPages.Razor" from version "2.0.0.0" to version"3.0.0.0".</span></span> <span data-ttu-id="1c807-219">이 섹션에서는 "System.Web.WebPages"를 포함 하는 경우 업데이트 버전 "3.0.0.0" 버전 "2.0.0.0"에서 이러한 요소</span><span class="sxs-lookup"><span data-stu-id="1c807-219">If this section contains "System.Web.WebPages", update those elements from version "2.0.0.0" to version"3.0.0.0"</span></span>  

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample8.xml?highlight=3-5)]
3. <span data-ttu-id="1c807-220">제거한 경우 합니다 `Microsoft-Web-Helpers` 이전 단계에서 NuGet 패키지 설치 `Microsoft.AspNet.WebHelpers` PMC에서 다음 명령을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="1c807-220">If you removed the `Microsoft-Web-Helpers` NuGet package in a previous step, install `Microsoft.AspNet.WebHelpers` with the following command in the PMC:</span></span>  
    `Install-Package -Id Microsoft.AspNet.WebHelpers`
4. <span data-ttu-id="1c807-221">앱에서 사용 하는 경우는 [User.IsInRole()](https://msdn.microsoft.com/en-us/library/system.web.security.roleprincipal.isinrole(v=vs.110).aspx) 메서드를 다음을 추가 합니다 *Web.config* 파일.</span><span class="sxs-lookup"><span data-stu-id="1c807-221">If your app uses the [User.IsInRole()](https://msdn.microsoft.com/en-us/library/system.web.security.roleprincipal.isinrole(v=vs.110).aspx) method, add the following to the *Web.config* file.</span></span>

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample9.xml)]

## <a name="final-steps"></a><span data-ttu-id="1c807-222">최종 단계</span><span class="sxs-lookup"><span data-stu-id="1c807-222">Final Steps</span></span>

<span data-ttu-id="1c807-223">빌드 및 응용 프로그램을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-223">Build and test the application.</span></span>

<span data-ttu-id="1c807-224">프로젝트 파일에서 MVC 4 프로젝트 형식 GUID를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-224">Remove the MVC 4 project type GUID from the project files.</span></span>

1. <span data-ttu-id="1c807-225">솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 선택한 **프로젝트 언로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-225">In Solution Explorer, right-click the project name and then select **Unload Project**.</span></span>
2. <span data-ttu-id="1c807-226">프로젝트를 마우스 오른쪽 단추로 클릭 하 고 편집 ProjectName.csproj를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-226">Right-click the project and select Edit ProjectName.csproj.</span></span>
3. <span data-ttu-id="1c807-227">찾을 합니다 `ProjectTypeGuids` 요소를 선택한 다음 제거 MVC 4 프로젝트 GUID `{E3E379DF-F4C6-4180-9B81-6769533ABE47}`합니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-227">Locate the `ProjectTypeGuids` element and then remove the MVC 4 project GUID, `{E3E379DF-F4C6-4180-9B81-6769533ABE47}`.</span></span>
4. <span data-ttu-id="1c807-228">저장 하 고 열려 있는 프로젝트 파일을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-228">Save and close the open project file.</span></span>
5. <span data-ttu-id="1c807-229">프로젝트를 마우스 오른쪽 단추로 누르고 **프로젝트 다시 로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="1c807-229">Right-click the project and select **Reload Project**.</span></span>
