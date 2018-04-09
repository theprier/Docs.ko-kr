---
uid: ajax/cdn/overview
title: Microsoft Ajax 콘텐츠 배달 네트워크 | Microsoft Docs
author: rick-anderson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/14/2017
ms.topic: article
ms.assetid: 8935bf14-ca6d-4a4e-9dbe-b96ce74cef49
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /ajax/cdn
msc.type: content
ms.openlocfilehash: bc5f40746ad6b1ed8a74bcb75def9ff8f08fb789
ms.sourcegitcommit: 7d02ca5f5ddc2ca3eb0258fdd6996fbf538c129a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/03/2018
---
<a name="microsoft-ajax-content-delivery-network"></a><span data-ttu-id="0ae52-102">Microsoft Ajax 콘텐츠 배달 네트워크</span><span class="sxs-lookup"><span data-stu-id="0ae52-102">Microsoft Ajax Content Delivery Network</span></span>
====================
> [!WARNING]
> <span data-ttu-id="0ae52-103">프로덕션 응용 프로그램 CDN 자산에 하드 종속성을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-103">Production applications should not take a hard dependency on CDN assets.</span></span> <span data-ttu-id="0ae52-104">응용 프로그램 참조 CDN 자산에 대 한 테스트 및 CDN을 사용할 수 없는 경우 대체 (fallback)는 자산을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-104">Applications should test for the CDN asset referenced, and use a fallback asset when the CDN is not available.</span></span> 
>
> <span data-ttu-id="0ae52-105">Microsoft Ajax CDN에 Azure CDN을 사용 하 여 보다 많은 SLA는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-105">The Microsoft Ajax CDN has no SLA above and beyond using an Azure CDN.</span></span>
>
> <span data-ttu-id="0ae52-106">사용 하 여 [이 GitHub 문제](https://github.com/aspnet/Docs/issues/5832) 에 Microsoft Ajax CDN 문제를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-106">Use [this GitHub issue](https://github.com/aspnet/Docs/issues/5832) to report problems with the Microsoft Ajax CDN.</span></span>

## <a name="table-of-contents"></a><span data-ttu-id="0ae52-107">목차</span><span class="sxs-lookup"><span data-stu-id="0ae52-107">Table of Contents</span></span>

<span data-ttu-id="0ae52-108">**[ajax.microsoft.com ajax.aspnetcdn.com로 변경](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span><span class="sxs-lookup"><span data-stu-id="0ae52-108">**[ajax.microsoft.com renamed to ajax.aspnetcdn.com](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span></span>  
<span data-ttu-id="0ae52-109">**[Visual Studio .vsdoc Support](#Visual_Studio_vsdoc_Support_19)**</span><span class="sxs-lookup"><span data-stu-id="0ae52-109">**[Visual Studio .vsdoc Support](#Visual_Studio_vsdoc_Support_19)**</span></span>  
<span data-ttu-id="0ae52-110">**[ASP.NET Ajax CDN에서 사용 하 여](#Using_ASPNET_Ajax_from_the_CDN_20)**</span><span class="sxs-lookup"><span data-stu-id="0ae52-110">**[Using ASP.NET Ajax from the CDN](#Using_ASPNET_Ajax_from_the_CDN_20)**</span></span>  
<span data-ttu-id="0ae52-111">**[CDN에서 jQuery를 사용 하 여](#Using_jQuery_from_the_CDN_21)**</span><span class="sxs-lookup"><span data-stu-id="0ae52-111">**[Using jQuery from the CDN](#Using_jQuery_from_the_CDN_21)**</span></span>  
<span data-ttu-id="0ae52-112">**[JQuery UI에서 CDN 사용 하 여](#Using_jQuery_UI_from_the_CDN_22)**</span><span class="sxs-lookup"><span data-stu-id="0ae52-112">**[Using jQuery UI from the CDN](#Using_jQuery_UI_from_the_CDN_22)**</span></span>  
<span data-ttu-id="0ae52-113">**[CDN에서 제 3 자 파일](#Third-Party_Files_on_the_CDN_23)**</span><span class="sxs-lookup"><span data-stu-id="0ae52-113">**[Third-Party Files on the CDN](#Third-Party_Files_on_the_CDN_23)**</span></span>  
  
 [<span data-ttu-id="0ae52-114">CDN에서 jQuery 릴리스</span><span class="sxs-lookup"><span data-stu-id="0ae52-114">jQuery Releases on the CDN</span></span>](#jQuery_Releases_on_the_CDN_0)  
 [<span data-ttu-id="0ae52-115">CDN에서 jQuery 마이그레이션할 릴리스</span><span class="sxs-lookup"><span data-stu-id="0ae52-115">jQuery Migrate Releases on the CDN</span></span>](#jQuery_Migrate_Releases_on_the_CDN_1)  
 [<span data-ttu-id="0ae52-116">jQuery UI CDN에 있는 릴리스</span><span class="sxs-lookup"><span data-stu-id="0ae52-116">jQuery UI Releases on the CDN</span></span>](#jQuery_UI_Releases_on_the_CDN_2)  
 [<span data-ttu-id="0ae52-117">jQuery 유효성 검사는 CDN에 있는 릴리스</span><span class="sxs-lookup"><span data-stu-id="0ae52-117">jQuery Validation Releases on the CDN</span></span>](#jQuery_Validation_Releases_on_the_CDN_3)  
 [<span data-ttu-id="0ae52-118">jQuery Mobile CDN에 있는 릴리스</span><span class="sxs-lookup"><span data-stu-id="0ae52-118">jQuery Mobile Releases on the CDN</span></span>](#jQuery_Mobile_Releases_on_the_CDN_4)  
 [<span data-ttu-id="0ae52-119">jQuery CDN에서 템플릿 릴리스</span><span class="sxs-lookup"><span data-stu-id="0ae52-119">jQuery Templates Releases on the CDN</span></span>](#jQuery_Templates_Releases_on_the_CDN_5)  
 [<span data-ttu-id="0ae52-120">jQuery CDN에서 주기 릴리스</span><span class="sxs-lookup"><span data-stu-id="0ae52-120">jQuery Cycle Releases on the CDN</span></span>](#jQuery_Cycle_Releases_on_the_CDN_6)  
 [<span data-ttu-id="0ae52-121">jQuery CDN에서 DataTables 릴리스</span><span class="sxs-lookup"><span data-stu-id="0ae52-121">jQuery DataTables Releases on the CDN</span></span>](#jQuery_DataTables_Releases_on_the_CDN_7)  
 [<span data-ttu-id="0ae52-122">CDN에서 Modernizr 릴리스</span><span class="sxs-lookup"><span data-stu-id="0ae52-122">Modernizr Releases on the CDN</span></span>](#Modernizr_Releases_on_the_CDN_8)  
 [<span data-ttu-id="0ae52-123">CDN에서 JSHint 릴리스</span><span class="sxs-lookup"><span data-stu-id="0ae52-123">JSHint Releases on the CDN</span></span>](#JSHint_Releases_on_the_CDN_10)  
 [<span data-ttu-id="0ae52-124">CDN에서 knockout 릴리스</span><span class="sxs-lookup"><span data-stu-id="0ae52-124">Knockout Releases on the CDN</span></span>](#Knockout_Releases_on_the_CDN_11)  
 [<span data-ttu-id="0ae52-125">CDN에서 릴리스 전역화</span><span class="sxs-lookup"><span data-stu-id="0ae52-125">Globalize Releases on the CDN</span></span>](#Globalize_Releases_on_the_CDN_12)  
 [<span data-ttu-id="0ae52-126">CDN에서 릴리스 응답</span><span class="sxs-lookup"><span data-stu-id="0ae52-126">Respond Releases on the CDN</span></span>](#Respond_Releases_on_the_CDN_13)  
 [<span data-ttu-id="0ae52-127">CDN에서 부트스트랩 릴리스</span><span class="sxs-lookup"><span data-stu-id="0ae52-127">Bootstrap Releases on the CDN</span></span>](#Bootstrap_Releases_on_the_CDN_14)  
 [<span data-ttu-id="0ae52-128">CDN에서 부트스트랩 TouchCarousel 릴리스</span><span class="sxs-lookup"><span data-stu-id="0ae52-128">Bootstrap TouchCarousel Releases on the CDN</span></span>](#BootstrapTouchCarousel_Releases_on_the_CDN_18)  
 [<span data-ttu-id="0ae52-129">CDN에서 Hammer.js 릴리스</span><span class="sxs-lookup"><span data-stu-id="0ae52-129">Hammer.js Releases on the CDN</span></span>](#Hammerjs_Releases_on_the_CDN_19)  
 [<span data-ttu-id="0ae52-130">ASP.NET Web Forms 및 CDN에서 Ajax 릴리스</span><span class="sxs-lookup"><span data-stu-id="0ae52-130">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>](#ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15)  
 [<span data-ttu-id="0ae52-131">CDN에 ASP.NET MVC 릴리스</span><span class="sxs-lookup"><span data-stu-id="0ae52-131">ASP.NET MVC Releases on the CDN</span></span>](#ASPNET_MVC_Releases_on_the_CDN_16)  
 [<span data-ttu-id="0ae52-132">CDN에서 ASP.NET SignalR 해제</span><span class="sxs-lookup"><span data-stu-id="0ae52-132">ASP.NET SignalR Releases on the CDN</span></span>](#ASPNET_SignalR_Releases_on_the_CDN_17)

<span data-ttu-id="0ae52-133">Microsoft Ajax 콘텐츠 배달 네트워크 (CDN) jQuery와 같은 인기 있는 제 3 자 JavaScript 라이브러리를 호스팅하고 웹 응용 프로그램에를 쉽게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-133">The Microsoft Ajax Content Delivery Network (CDN) hosts popular third party JavaScript libraries such as jQuery and enables you to easily add them to your Web applications.</span></span> <span data-ttu-id="0ae52-134">이 CDN에서 호스팅되는 jQuery를 사용 하 여 추가 하 여 시작할 수는 예를 들어 한 &lt;스크립트&gt; ajax.aspnetcdn.com 가리키는 페이지에는 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-134">For example, you can start using jQuery which is hosted on this CDN simply by adding a &lt;script&gt; tag to your page that points to ajax.aspnetcdn.com.</span></span>

<span data-ttu-id="0ae52-135">CDN 활용 하기 위해, Ajax 응용 프로그램의 성능을 크게 향상 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-135">By taking advantage of the CDN, you can significantly improve the performance of your Ajax applications.</span></span> <span data-ttu-id="0ae52-136">CDN의 콘텐츠는 세계에 있는 서버에 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-136">The contents of the CDN are cached on servers located around the world.</span></span> <span data-ttu-id="0ae52-137">또한 CDN에는 브라우저 서로 다른 도메인에 있는 웹 사이트에 대 한 캐시 된 제 3 자 JavaScript 파일을 다시 사용할 수 있도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-137">In addition, the CDN enables browsers to reuse cached third party JavaScript files for web sites that are located in different domains.</span></span>

<span data-ttu-id="0ae52-138">CDN은 Secure Sockets Layer를 사용 하 여 웹 페이지를 처리 해야 하는 경우 SSL (HTTPS)을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-138">The CDN supports SSL (HTTPS) in case you need to serve a web page using the Secure Sockets Layer.</span></span>

<span data-ttu-id="0ae52-139">CDN 업로드 된 및 해당 라이브러리의 소유자가 사용자에 게 사용이 허가 하는 다음 제 3 자 스크립트 라이브러리를 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-139">The CDN hosts the following third party script libraries which have been uploaded, and are licensed to you, by the owners of those libraries:</span></span>

- <span data-ttu-id="0ae52-140">jQuery (www.jquery.com)</span><span class="sxs-lookup"><span data-stu-id="0ae52-140">jQuery (www.jquery.com)</span></span>
- <span data-ttu-id="0ae52-141">jQuery UI (www.jqueryui.com)</span><span class="sxs-lookup"><span data-stu-id="0ae52-141">jQuery UI (www.jqueryui.com)</span></span>
- <span data-ttu-id="0ae52-142">jQuery Mobile (www.jquerymobile.com)</span><span class="sxs-lookup"><span data-stu-id="0ae52-142">jQuery Mobile (www.jquerymobile.com)</span></span>
- <span data-ttu-id="0ae52-143">jQuery 유효성 검사 (www.jquery.com)</span><span class="sxs-lookup"><span data-stu-id="0ae52-143">jQuery Validation (www.jquery.com)</span></span>
- <span data-ttu-id="0ae52-144">jQuery 주기 (www.malsup.com/jquery/cycle/)</span><span class="sxs-lookup"><span data-stu-id="0ae52-144">jQuery Cycle (www.malsup.com/jquery/cycle/)</span></span>
- <span data-ttu-id="0ae52-145">jQuery Datatable 드 (http://datatables.net/)</span><span class="sxs-lookup"><span data-stu-id="0ae52-145">jQuery DataTables (http://datatables.net/)</span></span>

<span data-ttu-id="0ae52-146">Microsoft Ajax CDN는 Microsoft에서 업로드 한 다음 라이브러리를도 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-146">The Microsoft Ajax CDN also includes the following libraries which have been uploaded by Microsoft:</span></span>

- <span data-ttu-id="0ae52-147">ASP.NET Ajax</span><span class="sxs-lookup"><span data-stu-id="0ae52-147">ASP.NET Ajax</span></span>
- <span data-ttu-id="0ae52-148">ASP.NET MVC JavaScript 파일</span><span class="sxs-lookup"><span data-stu-id="0ae52-148">ASP.NET MVC JavaScript Files</span></span>
- <span data-ttu-id="0ae52-149">ASP.NET SignalR JavaScript 파일</span><span class="sxs-lookup"><span data-stu-id="0ae52-149">ASP.NET SignalR JavaScript Files</span></span>

<span data-ttu-id="0ae52-150">Microsoft는이 CDN에서 호스팅되는 모든 타사 라이브러리의 소유권을 주장 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-150">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="0ae52-151">저작권 소유자는 라이브러리에 이러한 라이브러리를 라이선스 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-151">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="0ae52-152">해당 저작권 소유자가 단독으로 다운로드 하 고 이러한 라이브러리를 사용 해야 할 수 있는 모든 권한이 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-152">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="0ae52-153">이들은 Microsoft 라이브러리 Microsoft 지적 재산권 권한 라이선스 (묵시적된 특허 권한이 없음 포함) 없음이나 보증을이 CDN에서 호스트 되는 타사 라이브러리에 대 한 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-153">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<span data-ttu-id="0ae52-154">JavaScript 라이브러리를 제출 하려면이 고 라이브러리에는 상위 JavaScript 라이브러리 중 하나 (에 나열 된 http://trends.builtwith.com) 또는 확장/플러그 인을 이러한 라이브러리는 (a) 인기 있는; 또는 (b) 유용한 ASP.NET에서 사용 하기 위해 다음에 게 문의 하십시오 AjaxCDNSubmission@Microsoft.com합니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-154">If you wish to submit your JavaScript library and your library is one of the top JavaScript libraries (as listed on http://trends.builtwith.com) or extensions/plugins to these libraries that are (a) popular; or (b) helpful for use on ASP.NET then please contact AjaxCDNSubmission@Microsoft.com.</span></span>

<a id="ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18"></a>

## <a name="ajaxmicrosoftcom-renamed-to-ajaxaspnetcdncom"></a><span data-ttu-id="0ae52-155">ajax.microsoft.com ajax.aspnetcdn.com로 변경</span><span class="sxs-lookup"><span data-stu-id="0ae52-155">ajax.microsoft.com renamed to ajax.aspnetcdn.com</span></span>

<span data-ttu-id="0ae52-156">CDN은 microsoft.com 도메인 이름을 사용 하는 데 사용 하 고 aspnetcdn.com 도메인 이름을 사용 하도록 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-156">The CDN used to use the microsoft.com domain name and has been changed to use the aspnetcdn.com domain name.</span></span> <span data-ttu-id="0ae52-157">각 요청과 함께 네트워크를 통해 모든 쿠키를 보내야 해당 도메인에서 했기 브라우저 microsoft.com 도메인을 참조 하기 때문에 성능을 향상 시키기 위해이 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-157">This change was made to increase performance because when a browser referenced the microsoft.com domain it would send any cookies from that domain across the wire with each request.</span></span> <span data-ttu-id="0ae52-158">Microsoft.com 이외의 도메인 이름으로 바꾸어 25%로 많은 성능으로 증가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-158">By renaming to a domain name other than microsoft.com performance can be increased by as much to 25%.</span></span> <span data-ttu-id="0ae52-159">참고 ajax.microsoft.com은 계속 작동 하지만 ajax.aspnetcdn.com를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-159">Note ajax.microsoft.com will continue to function but ajax.aspnetcdn.com is recommended.</span></span>

- <span data-ttu-id="0ae52-160">이전 형식: https://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="0ae52-160">Old Format: https://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span></span>
- <span data-ttu-id="0ae52-161">새 형식: https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="0ae52-161">New Format: https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span></span>

<a id="Visual_Studio_vsdoc_Support_19"></a>

## <a name="visual-studio-vsdoc-support"></a><span data-ttu-id="0ae52-162">Visual Studio.vsdoc 지원</span><span class="sxs-lookup"><span data-stu-id="0ae52-162">Visual Studio .vsdoc Support</span></span>

<span data-ttu-id="0ae52-163">Visual Studio 2008 및 2008 s p 1이 있는지 확인 해야 할.vsdoc 파일을 제대로 사용 하려면 설치 하 고 vsdoc 파일에 대 한 핫픽스를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-163">To use the .vsdoc files properly with Visual Studio 2008 you need to make sure that you have VS 2008 SP1 installed and the hotfix for vsdoc files installed.</span></span> <span data-ttu-id="0ae52-164">여기에서 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-164">You can get these from here:</span></span>

- [<span data-ttu-id="0ae52-165">Visual Studio 2008 s p 1을 다운로드</span><span class="sxs-lookup"><span data-stu-id="0ae52-165">Download Visual Studio 2008 SP1</span></span>](https://www.microsoft.com/downloads/en/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en "Visual Studio 2008 s p 1을 다운로드 합니다.")
- [<span data-ttu-id="0ae52-166">Visual Studio 2008 s p 1에 대 한.vsdoc 핫픽스 다운로드</span><span class="sxs-lookup"><span data-stu-id="0ae52-166">Download .vsdoc hotfix for Visual Studio 2008 SP1</span></span>](https://code.msdn.microsoft.com/KB958502/Release/ProjectReleases.aspx?ReleaseId=1736 "Visual Studio 2008 s p 1에 대 한.vsdoc 핫픽스 다운로드")

<span data-ttu-id="0ae52-167">Visual Studio 2010 추가 패치 없이.vsdoc 파일을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-167">Visual Studio 2010 supports .vsdoc files without any additional patches.</span></span>

<a id="Using_ASPNET_Ajax_from_the_CDN_20"></a>

## <a name="using-aspnet-ajax-from-the-cdn"></a><span data-ttu-id="0ae52-168">ASP.NET Ajax CDN에서 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="0ae52-168">Using ASP.NET Ajax from the CDN</span></span>

<span data-ttu-id="0ae52-169">ASP.NET 4를 사용 하는 경우 cdn ASP.NET framework 스크립트에 대 한 모든 요청을 리디렉션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-169">When using ASP.NET 4, you can redirect all requests for ASP.NET framework scripts to the CDN.</span></span> <span data-ttu-id="0ae52-170">로컬 웹 서버 대신 CDN에서 스크립트 검색 공용 ASP.NET 웹 사이트의 성능을 상당히 개선 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-170">Retrieving scripts from the CDN instead of your local web server can substantially improve the performance of public ASP.NET websites.</span></span>

<span data-ttu-id="0ae52-171">ScriptManager EnableCDN 속성을 사용 하 여 모든 요청을 리디렉션할 ASP.NET 프레임 워크 스크립트 Microsoft Ajax CDN에:</span><span class="sxs-lookup"><span data-stu-id="0ae52-171">Use the ScriptManager EnableCDN property to redirect all ASP.NET framework script requests to the Microsoft Ajax CDN:</span></span>

[!code-aspx[Main](overview/samples/sample1.aspx)]

<a id="Using_jQuery_from_the_CDN_21"></a>

## <a name="using-jquery-from-the-cdn"></a><span data-ttu-id="0ae52-172">CDN에서 jQuery를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="0ae52-172">Using jQuery from the CDN</span></span>

<span data-ttu-id="0ae52-173">페이지에는 다음 스크립트 요소를 추가 하 여 CDN에서 웹 응용 프로그램에서 호스팅되는 jQuery 스크립트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-173">You can use jQuery scripts hosted on CDN in your Web application by adding the following script element to a page:</span></span>

[!code-html[Main](overview/samples/sample2.html)]

<span data-ttu-id="0ae52-174">CDN에 액세스할 수 있는 jQuery 스크립트의 축소 된 버전도 포함 됩니다는 다음 요소를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="0ae52-174">The CDN also includes the minified version of the jQuery script, which you can get using the following element:</span></span>

[!code-html[Main](overview/samples/sample3.html)]

<span data-ttu-id="0ae52-175">대체 인증 CDN를 사용할 수 없는 경우 자신의 웹 사이트에 로컬 경로에서 jQuery를 로드 하려면 페이지를 허용 하려면 CDN 참조 요소 바로 뒤 다음 요소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-175">To allow your page to fallback to loading jQuery from a local path on your own website if the CDN happens to be unavailable, add the following element immediately after the element referencing the CDN:</span></span>

[!code-html[Main](overview/samples/sample4.html)]

<span data-ttu-id="0ae52-176">다음 샘플 페이지 CDN 버전 (로컬 복사본으로 대체) 사용 하 여 jQuery 라이브러리의를 사용 하 여는 단추를 클릭할 때 div 요소 내용을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-176">The following sample page uses the CDN version of the jQuery library (with fallback to a local copy) to display the contents of a div element when a button is clicked.</span></span>

[!code-html[Main](overview/samples/sample5.html)]

<span data-ttu-id="0ae52-177">JQuery에 대 한 자세한 정보 및 방문 하 여 jQuery의 로컬 복사본을 다운로드할 수 있습니다는 [jQuery](http://jquery.com/) 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-177">You can learn more about jQuery and download a local copy of jQuery by visiting the [jQuery](http://jquery.com/) Web site.</span></span>

<a id="Using_jQuery_UI_from_the_CDN_22"></a>

## <a name="using-jquery-ui-from-the-cdn"></a><span data-ttu-id="0ae52-178">JQuery UI에서 CDN 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="0ae52-178">Using jQuery UI from the CDN</span></span>

<span data-ttu-id="0ae52-179">또한 CDN jQuery UI 라이브러리를 호스트합니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-179">The CDN also hosts the jQuery UI library.</span></span> <span data-ttu-id="0ae52-180">JQuery UI 라이브러리는 다양 한 위젯 및 ASP.NET 응용 프로그램에서 사용할 수 있는 효과 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-180">The jQuery UI library includes a rich set of widgets and effects that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="0ae52-181">예를 들어 다음 페이지는 ASP.NET Web Forms 응용 프로그램의 컨텍스트에서 jQuery UI Datepicker 팝업 달력이 표시를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-181">For example, the following page illustrates how you can use the jQuery UI Datepicker in the context of an ASP.NET Web Forms application to display a pop-up calendar:</span></span>

[!code-aspx[Main](overview/samples/sample6.aspx)]

<span data-ttu-id="0ae52-182">키보드를 사용 하 여 텍스트 상자에 포커스를 이동 하면 달력이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-182">When you move focus to the TextBox using your keyboard, a calendar is displayed:</span></span>

![만든 Datepicker 팝업 일정](overview/_static/image1.png)

<span data-ttu-id="0ae52-184">위의 코드에서 CDN에서 3 개의 파일을 포함 해야 하는 사항을 참고 하십시오.</span><span class="sxs-lookup"><span data-stu-id="0ae52-184">Notice that you must include three files from the CDN in the code above:</span></span>

- <span data-ttu-id="0ae52-185">JQuery 라이브러리 &mdash; jQuery UI 라이브러리는 jQuery 라이브러리에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-185">The jQuery library &mdash; The jQuery UI library depends on the jQuery library.</span></span> <span data-ttu-id="0ae52-186">JQuery 라이브러리 jQuery UI 라이브러리를 추가 하기 전에 페이지에 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-186">You must add the jQuery library to your page before you add the jQuery UI library.</span></span>
- <span data-ttu-id="0ae52-187">JQuery UI 라이브러리 &mdash; jQuery UI 라이브러리 모든 위의 페이지에 사용 된 Datepicker 위젯 같은 위젯 및 jQuery UI 효과 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-187">The jQuery UI library &mdash; The jQuery UI library contains all of the jQuery UI effects and widgets such as the Datepicker widget used in the page above.</span></span>
- <span data-ttu-id="0ae52-188">JQuery UI 테마 &mdash; jQuery UI 다양 한 테마를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-188">A jQuery UI theme &mdash; The jQuery UI supports different themes.</span></span> <span data-ttu-id="0ae52-189">위의 페이지 Redmond 테마 가져올 CSS 파일에 대 한 링크를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-189">The page above includes a link to a CSS file to import the Redmond theme.</span></span>

<span data-ttu-id="0ae52-190">모든 표준 jQuery UI 테마는 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-190">All of the standard jQuery UI themes are hosted on the CDN.</span></span> <span data-ttu-id="0ae52-191">[이 페이지를 방문](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 Microsoft Ajax CDN에서") 각 테마에 대 한 축소판 그림을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-191">[Visit this page](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 on the Microsoft Ajax CDN") to view thumbnails for each theme.</span></span>

<span data-ttu-id="0ae52-192">JQuery UI 라이브러리에 대 한 자세한 내용은 방문 공식 [jQuery UI 웹 사이트](http://jQueryUI.com "jQuery UI 웹 사이트")합니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-192">To learn more about the jQuery UI library, visit the official [jQuery UI website](http://jQueryUI.com "jQuery UI website").</span></span>

<a id="Third-Party_Files_on_the_CDN_23"></a>

## <a name="third-party-files-on-the-cdn"></a><span data-ttu-id="0ae52-193">CDN에서 제 3 자 파일</span><span class="sxs-lookup"><span data-stu-id="0ae52-193">Third-Party Files on the CDN</span></span>

<span data-ttu-id="0ae52-194">CDN은 가장 일반적인 제 3 자 JavaScript 라이브러리 중 일부를 호스팅합니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-194">The CDN hosts some of the most popular third party JavaScript libraries.</span></span> <span data-ttu-id="0ae52-195">Microsoft는이 CDN에서 호스팅되는 모든 타사 라이브러리의 소유권을 주장 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-195">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="0ae52-196">저작권 소유자는 라이브러리에 이러한 라이브러리를 라이선스 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-196">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="0ae52-197">해당 저작권 소유자가 단독으로 다운로드 하 고 이러한 라이브러리를 사용 해야 할 수 있는 모든 권한이 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-197">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="0ae52-198">이들은 Microsoft 라이브러리 Microsoft 지적 재산권 권한 라이선스 (묵시적된 특허 권한이 없음 포함) 없음이나 보증을이 CDN에서 호스트 되는 타사 라이브러리에 대 한 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-198">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<a id="jQuery_Releases_on_the_CDN_0"></a>

### <a name="jquery-releases-on-the-cdn"></a><span data-ttu-id="0ae52-199">CDN에서 jQuery 릴리스</span><span class="sxs-lookup"><span data-stu-id="0ae52-199">jQuery Releases on the CDN</span></span>

<span data-ttu-id="0ae52-200">다음 버전의 jQuery CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-200">The following releases of jQuery are hosted on the CDN:</span></span>

#### <a name="jquery-version-331"></a><span data-ttu-id="0ae52-201">3.3.1 jQuery 버전</span><span class="sxs-lookup"><span data-stu-id="0ae52-201">jQuery version 3.3.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.map

#### <a name="jquery-version-321"></a><span data-ttu-id="0ae52-202">jQuery 버전 3.2.1</span><span class="sxs-lookup"><span data-stu-id="0ae52-202">jQuery version 3.2.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.map

#### <a name="jquery-version-320"></a><span data-ttu-id="0ae52-203">jQuery 버전 3.2.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-203">jQuery version 3.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.map

#### <a name="jquery-version-311"></a><span data-ttu-id="0ae52-204">3.1.1 jQuery 버전</span><span class="sxs-lookup"><span data-stu-id="0ae52-204">jQuery version 3.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.map

#### <a name="jquery-version-310"></a><span data-ttu-id="0ae52-205">jQuery 버전 3.1.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-205">jQuery version 3.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.map

#### <a name="jquery-version-300"></a><span data-ttu-id="0ae52-206">jQuery 버전 3.0.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-206">jQuery version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.map

#### <a name="jquery-version-224"></a><span data-ttu-id="0ae52-207">jQuery 버전 2.2.4</span><span class="sxs-lookup"><span data-stu-id="0ae52-207">jQuery version 2.2.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.map

#### <a name="jquery-version-223"></a><span data-ttu-id="0ae52-208">jQuery 버전 2.2.3</span><span class="sxs-lookup"><span data-stu-id="0ae52-208">jQuery version 2.2.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.map

#### <a name="jquery-version-222"></a><span data-ttu-id="0ae52-209">jQuery 버전 2.2.2</span><span class="sxs-lookup"><span data-stu-id="0ae52-209">jQuery version 2.2.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.map

#### <a name="jquery-version-221"></a><span data-ttu-id="0ae52-210">jQuery 버전 2.2.1</span><span class="sxs-lookup"><span data-stu-id="0ae52-210">jQuery version 2.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.map

#### <a name="jquery-version-220"></a><span data-ttu-id="0ae52-211">jQuery 버전 2.2.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-211">jQuery version 2.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.map

#### <a name="jquery-version-214"></a><span data-ttu-id="0ae52-212">jQuery 버전 2.1.4</span><span class="sxs-lookup"><span data-stu-id="0ae52-212">jQuery version 2.1.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.map

#### <a name="jquery-version-213"></a><span data-ttu-id="0ae52-213">jQuery 버전 2.1.3</span><span class="sxs-lookup"><span data-stu-id="0ae52-213">jQuery version 2.1.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.map

#### <a name="jquery-version-212"></a><span data-ttu-id="0ae52-214">jQuery 버전 2.1.2</span><span class="sxs-lookup"><span data-stu-id="0ae52-214">jQuery version 2.1.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.min.js

#### <a name="jquery-version-211"></a><span data-ttu-id="0ae52-215">jQuery 버전 2.1.1</span><span class="sxs-lookup"><span data-stu-id="0ae52-215">jQuery version 2.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.map

#### <a name="jquery-version-210"></a><span data-ttu-id="0ae52-216">jQuery 버전 2.1.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-216">jQuery version 2.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.map

#### <a name="jquery-version-203"></a><span data-ttu-id="0ae52-217">jQuery 버전 2.0.3</span><span class="sxs-lookup"><span data-stu-id="0ae52-217">jQuery version 2.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.map

#### <a name="jquery-version-202"></a><span data-ttu-id="0ae52-218">jQuery 버전 2.0.2</span><span class="sxs-lookup"><span data-stu-id="0ae52-218">jQuery version 2.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.map

#### <a name="jquery-version-201"></a><span data-ttu-id="0ae52-219">jQuery 버전 2.0.1</span><span class="sxs-lookup"><span data-stu-id="0ae52-219">jQuery version 2.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.map

#### <a name="jquery-version-200"></a><span data-ttu-id="0ae52-220">jQuery 버전 2.0.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-220">jQuery version 2.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.map

#### <a name="jquery-version-1124"></a><span data-ttu-id="0ae52-221">jQuery 버전 1.12.4</span><span class="sxs-lookup"><span data-stu-id="0ae52-221">jQuery version 1.12.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.map

#### <a name="jquery-version-1123"></a><span data-ttu-id="0ae52-222">jQuery 버전 1.12.3</span><span class="sxs-lookup"><span data-stu-id="0ae52-222">jQuery version 1.12.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.map

#### <a name="jquery-version-1122"></a><span data-ttu-id="0ae52-223">jQuery 버전 1.12.2</span><span class="sxs-lookup"><span data-stu-id="0ae52-223">jQuery version 1.12.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.map

#### <a name="jquery-version-1121"></a><span data-ttu-id="0ae52-224">jQuery 버전 1.12.1</span><span class="sxs-lookup"><span data-stu-id="0ae52-224">jQuery version 1.12.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.map

#### <a name="jquery-version-1120"></a><span data-ttu-id="0ae52-225">jQuery 버전 1.12.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-225">jQuery version 1.12.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.map

#### <a name="jquery-version-1113"></a><span data-ttu-id="0ae52-226">jQuery 버전 1.11.3</span><span class="sxs-lookup"><span data-stu-id="0ae52-226">jQuery version 1.11.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.map

#### <a name="jquery-version-1112"></a><span data-ttu-id="0ae52-227">jQuery 버전 1.11.2</span><span class="sxs-lookup"><span data-stu-id="0ae52-227">jQuery version 1.11.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.map

#### <a name="jquery-version-1111"></a><span data-ttu-id="0ae52-228">jQuery 버전 1.11.1</span><span class="sxs-lookup"><span data-stu-id="0ae52-228">jQuery version 1.11.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.map

#### <a name="jquery-version-1110"></a><span data-ttu-id="0ae52-229">jQuery 버전 1.11.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-229">jQuery version 1.11.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.map

#### <a name="jquery-version-1102"></a><span data-ttu-id="0ae52-230">jQuery 1.10.2 버전</span><span class="sxs-lookup"><span data-stu-id="0ae52-230">jQuery version 1.10.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.map

#### <a name="jquery-version-1101"></a><span data-ttu-id="0ae52-231">jQuery 버전 1.10.1</span><span class="sxs-lookup"><span data-stu-id="0ae52-231">jQuery version 1.10.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.map

#### <a name="jquery-version-1100"></a><span data-ttu-id="0ae52-232">jQuery 버전 1.10.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-232">jQuery version 1.10.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.map

#### <a name="jquery-version-191"></a><span data-ttu-id="0ae52-233">jQuery 버전 1.9.1</span><span class="sxs-lookup"><span data-stu-id="0ae52-233">jQuery version 1.9.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.map

#### <a name="jquery-version-190"></a><span data-ttu-id="0ae52-234">1.9.0 jQuery 버전</span><span class="sxs-lookup"><span data-stu-id="0ae52-234">jQuery version 1.9.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.map

#### <a name="jquery-version-183"></a><span data-ttu-id="0ae52-235">1.8.3 jQuery 버전</span><span class="sxs-lookup"><span data-stu-id="0ae52-235">jQuery version 1.8.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3-vsdoc.js

#### <a name="jquery-version-182"></a><span data-ttu-id="0ae52-236">1.8.2 jQuery 버전</span><span class="sxs-lookup"><span data-stu-id="0ae52-236">jQuery version 1.8.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2-vsdoc.js

#### <a name="jquery-version-181"></a><span data-ttu-id="0ae52-237">1.8.1 jQuery 버전</span><span class="sxs-lookup"><span data-stu-id="0ae52-237">jQuery version 1.8.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1-vsdoc.js

#### <a name="jquery-version-180"></a><span data-ttu-id="0ae52-238">jQuery 버전 1.8.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-238">jQuery version 1.8.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0-vsdoc.js

#### <a name="jquery-version-172"></a><span data-ttu-id="0ae52-239">1.7.2 jQuery 버전</span><span class="sxs-lookup"><span data-stu-id="0ae52-239">jQuery version 1.7.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js

#### <a name="jquery-version-171"></a><span data-ttu-id="0ae52-240">jQuery 버전 1.7.1</span><span class="sxs-lookup"><span data-stu-id="0ae52-240">jQuery version 1.7.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1-vsdoc.js

#### <a name="jquery-version-17"></a><span data-ttu-id="0ae52-241">jQuery 버전 1.7</span><span class="sxs-lookup"><span data-stu-id="0ae52-241">jQuery version 1.7</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7-vsdoc.js

#### <a name="jquery-version-164"></a><span data-ttu-id="0ae52-242">jQuery 버전 1.6.4</span><span class="sxs-lookup"><span data-stu-id="0ae52-242">jQuery version 1.6.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4-vsdoc.js

#### <a name="jquery-version-163"></a><span data-ttu-id="0ae52-243">jQuery 버전 1.6.3</span><span class="sxs-lookup"><span data-stu-id="0ae52-243">jQuery version 1.6.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3-vsdoc.js

#### <a name="jquery-version-162"></a><span data-ttu-id="0ae52-244">jQuery 버전 1.6.2</span><span class="sxs-lookup"><span data-stu-id="0ae52-244">jQuery version 1.6.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2-vsdoc.js

#### <a name="jquery-version-161"></a><span data-ttu-id="0ae52-245">jQuery 버전 1.6.1</span><span class="sxs-lookup"><span data-stu-id="0ae52-245">jQuery version 1.6.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1-vsdoc.js

#### <a name="jquery-version-16"></a><span data-ttu-id="0ae52-246">jQuery 버전 1.6</span><span class="sxs-lookup"><span data-stu-id="0ae52-246">jQuery version 1.6</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6-vsdoc.js

#### <a name="jquery-version-152"></a><span data-ttu-id="0ae52-247">1.5.2 jQuery 버전</span><span class="sxs-lookup"><span data-stu-id="0ae52-247">jQuery version 1.5.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2-vsdoc.js

#### <a name="jquery-version-151"></a><span data-ttu-id="0ae52-248">1.5.1 jQuery 버전</span><span class="sxs-lookup"><span data-stu-id="0ae52-248">jQuery version 1.5.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1-vsdoc.js

#### <a name="jquery-version-15"></a><span data-ttu-id="0ae52-249">jQuery 버전 1.5</span><span class="sxs-lookup"><span data-stu-id="0ae52-249">jQuery version 1.5</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5-vsdoc.js

#### <a name="jquery-version-144"></a><span data-ttu-id="0ae52-250">jQuery 버전 1.4.4</span><span class="sxs-lookup"><span data-stu-id="0ae52-250">jQuery version 1.4.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4-vsdoc.js

#### <a name="jquery-version-143"></a><span data-ttu-id="0ae52-251">jQuery 버전 1.4.3</span><span class="sxs-lookup"><span data-stu-id="0ae52-251">jQuery version 1.4.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3-vsdoc.js

#### <a name="jquery-version-142"></a><span data-ttu-id="0ae52-252">1.4.2 jQuery 버전</span><span class="sxs-lookup"><span data-stu-id="0ae52-252">jQuery version 1.4.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2-vsdoc.js

#### <a name="jquery-version-141"></a><span data-ttu-id="0ae52-253">1.4.1 jQuery 버전</span><span class="sxs-lookup"><span data-stu-id="0ae52-253">jQuery version 1.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1-vsdoc.js

#### <a name="jquery-version-14"></a><span data-ttu-id="0ae52-254">jQuery 버전 1.4</span><span class="sxs-lookup"><span data-stu-id="0ae52-254">jQuery version 1.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.min.js

#### <a name="jquery-version-132"></a><span data-ttu-id="0ae52-255">1.3.2 jQuery 버전</span><span class="sxs-lookup"><span data-stu-id="0ae52-255">jQuery version 1.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min-vsdoc.js

<a id="jQuery_Migrate_Releases_on_the_CDN_1"></a>

### <a name="jquery-migrate-releases-on-the-cdn"></a><span data-ttu-id="0ae52-256">CDN에서 jQuery 마이그레이션할 릴리스</span><span class="sxs-lookup"><span data-stu-id="0ae52-256">jQuery Migrate Releases on the CDN</span></span>

<span data-ttu-id="0ae52-257">다음 버전의 jQuery 마이그레이션 CDN에 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-257">The following releases of jQuery Migrate are hosted on the CDN:</span></span>

#### <a name="jquery-migrate-version-300"></a><span data-ttu-id="0ae52-258">jQuery 버전 3.0.0 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="0ae52-258">jQuery Migrate version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.min.js

#### <a name="jquery-migrate-version-121"></a><span data-ttu-id="0ae52-259">jQuery 버전 1.2.1 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="0ae52-259">jQuery Migrate version 1.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.min.js

<span data-ttu-id="0ae52-260">jQuery 버전 1.2.0 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="0ae52-260">jQuery Migrate version 1.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.min.js

#### <a name="jquery-migrate-version-111"></a><span data-ttu-id="0ae52-261">jQuery 버전 1.1.1 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="0ae52-261">jQuery Migrate version 1.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.min.js

#### <a name="jquery-migrate-version-110"></a><span data-ttu-id="0ae52-262">jQuery 버전 1.1.0 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="0ae52-262">jQuery Migrate version 1.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.min.js

#### <a name="jquery-migrate-version-100"></a><span data-ttu-id="0ae52-263">jQuery 버전 1.0.0 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="0ae52-263">jQuery Migrate version 1.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.min.js

<a id="jQuery_UI_Releases_on_the_CDN_2"></a>

### <a name="jquery-ui-releases-on-the-cdn"></a><span data-ttu-id="0ae52-264">jQuery UI CDN에 있는 릴리스</span><span class="sxs-lookup"><span data-stu-id="0ae52-264">jQuery UI Releases on the CDN</span></span>

<span data-ttu-id="0ae52-265">JQuery UI 라이브러리의 다음 릴리스에서이 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-265">The following releases of the jQuery UI library are hosted on this CDN.</span></span> <span data-ttu-id="0ae52-266">파일의 실제 목록을 확인 하려면 각 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-266">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="0ae52-267">jQuery UI 1.12.1</span><span class="sxs-lookup"><span data-stu-id="0ae52-267">jQuery UI 1.12.1</span></span>](jquery-ui/cdnjqueryui1121.md "jQuery UI 1.12.1 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-268">jQuery UI 1.12.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-268">jQuery UI 1.12.0</span></span>](jquery-ui/cdnjqueryui1120.md "jQuery UI 1.12.0 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-269">jQuery UI 1.11.4</span><span class="sxs-lookup"><span data-stu-id="0ae52-269">jQuery UI 1.11.4</span></span>](jquery-ui/cdnjqueryui1114.md "jQuery UI 1.11.4 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-270">jQuery UI 1.11.3</span><span class="sxs-lookup"><span data-stu-id="0ae52-270">jQuery UI 1.11.3</span></span>](jquery-ui/cdnjqueryui1113.md "jQuery UI 1.11.3 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-271">jQuery UI 1.11.2</span><span class="sxs-lookup"><span data-stu-id="0ae52-271">jQuery UI 1.11.2</span></span>](jquery-ui/cdnjqueryui1112.md "jQuery UI 1.11.2 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-272">jQuery UI 1.11.1</span><span class="sxs-lookup"><span data-stu-id="0ae52-272">jQuery UI 1.11.1</span></span>](jquery-ui/cdnjqueryui1111.md "jQuery UI 1.11.1 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-273">jQuery UI 1.11.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-273">jQuery UI 1.11.0</span></span>](jquery-ui/cdnjqueryui1110.md "jQuery UI 1.11.0 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-274">jQuery UI 1.10.4</span><span class="sxs-lookup"><span data-stu-id="0ae52-274">jQuery UI 1.10.4</span></span>](jquery-ui/cdnjqueryui1104.md "jQuery UI 1.10.4 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-275">jQuery UI 1.10.3</span><span class="sxs-lookup"><span data-stu-id="0ae52-275">jQuery UI 1.10.3</span></span>](jquery-ui/cdnjqueryui1103.md "jQuery UI 1.10.3 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-276">jQuery 1.10.2 UI</span><span class="sxs-lookup"><span data-stu-id="0ae52-276">jQuery UI 1.10.2</span></span>](jquery-ui/cdnjqueryui1102.md "jQuery 1.10.2 Microsoft Ajax CDN에서 UI")
- [<span data-ttu-id="0ae52-277">jQuery UI 1.10.1</span><span class="sxs-lookup"><span data-stu-id="0ae52-277">jQuery UI 1.10.1</span></span>](jquery-ui/cdnjqueryui1101.md "jQuery UI 1.10.1 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-278">jQuery UI 1.10.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-278">jQuery UI 1.10.0</span></span>](jquery-ui/cdnjqueryui1100.md "jQuery UI 1.10.0 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-279">jQuery UI 1.9.2</span><span class="sxs-lookup"><span data-stu-id="0ae52-279">jQuery UI 1.9.2</span></span>](jquery-ui/cdnjqueryui192.md "jQuery UI 1.9.2 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-280">jQuery UI 1.9.1</span><span class="sxs-lookup"><span data-stu-id="0ae52-280">jQuery UI 1.9.1</span></span>](jquery-ui/cdnjqueryui191.md "jQuery UI 1.9.1 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-281">jQuery UI 1.9.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-281">jQuery UI 1.9.0</span></span>](jquery-ui/cdnjqueryui190.md "jQuery UI 1.9.0 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-282">jQuery UI 1.8.24</span><span class="sxs-lookup"><span data-stu-id="0ae52-282">jQuery UI 1.8.24</span></span>](jquery-ui/cdnjqueryui1824.md "jQuery UI 1.8.24 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-283">jQuery UI 1.8.23</span><span class="sxs-lookup"><span data-stu-id="0ae52-283">jQuery UI 1.8.23</span></span>](jquery-ui/cdnjqueryui1823.md "jQuery UI 1.8.23 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-284">jQuery UI 1.8.22</span><span class="sxs-lookup"><span data-stu-id="0ae52-284">jQuery UI 1.8.22</span></span>](jquery-ui/cdnjqueryui1822.md "jQuery UI 1.8.22 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-285">jQuery UI 1.8.21</span><span class="sxs-lookup"><span data-stu-id="0ae52-285">jQuery UI 1.8.21</span></span>](jquery-ui/cdnjqueryui1821.md "jQuery UI 1.8.21 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-286">jQuery UI 1.8.20</span><span class="sxs-lookup"><span data-stu-id="0ae52-286">jQuery UI 1.8.20</span></span>](jquery-ui/cdnjqueryui1820.md "jQuery UI 1.8.20 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-287">jQuery UI 1.8.19</span><span class="sxs-lookup"><span data-stu-id="0ae52-287">jQuery UI 1.8.19</span></span>](jquery-ui/cdnjqueryui1819.md "jQuery UI 1.8.19 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-288">jQuery UI 1.8.18</span><span class="sxs-lookup"><span data-stu-id="0ae52-288">jQuery UI 1.8.18</span></span>](jquery-ui/cdnjqueryui1818.md "jQuery UI 1.8.18 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-289">jQuery UI 1.8.17</span><span class="sxs-lookup"><span data-stu-id="0ae52-289">jQuery UI 1.8.17</span></span>](jquery-ui/cdnjqueryui1817.md "jQuery UI 1.8.17 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-290">jQuery UI 1.8.16</span><span class="sxs-lookup"><span data-stu-id="0ae52-290">jQuery UI 1.8.16</span></span>](jquery-ui/cdnjqueryui1816.md "jQuery UI 1.8.16 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-291">jQuery UI 1.8.15</span><span class="sxs-lookup"><span data-stu-id="0ae52-291">jQuery UI 1.8.15</span></span>](jquery-ui/cdnjqueryui1815.md "jQuery UI 1.8.15 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-292">jQuery UI 1.8.14</span><span class="sxs-lookup"><span data-stu-id="0ae52-292">jQuery UI 1.8.14</span></span>](jquery-ui/cdnjqueryui1814.md "jQuery UI 1.8.14 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-293">jQuery UI 1.8.13</span><span class="sxs-lookup"><span data-stu-id="0ae52-293">jQuery UI 1.8.13</span></span>](jquery-ui/cdnjqueryui1813.md "jQuery UI 1.8.13 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-294">jQuery UI 1.8.12</span><span class="sxs-lookup"><span data-stu-id="0ae52-294">jQuery UI 1.8.12</span></span>](jquery-ui/cdnjqueryui1812.md "jQuery UI 1.8.12 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-295">jQuery UI 1.8.11</span><span class="sxs-lookup"><span data-stu-id="0ae52-295">jQuery UI 1.8.11</span></span>](jquery-ui/cdnjqueryui1811.md "jQuery UI 1.8.11 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-296">jQuery UI 1.8.10</span><span class="sxs-lookup"><span data-stu-id="0ae52-296">jQuery UI 1.8.10</span></span>](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-297">jQuery UI 1.8.9</span><span class="sxs-lookup"><span data-stu-id="0ae52-297">jQuery UI 1.8.9</span></span>](jquery-ui/cdnjqueryui189.md "jQuery UI 1.8.9 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-298">jQuery UI 1.8.8</span><span class="sxs-lookup"><span data-stu-id="0ae52-298">jQuery UI 1.8.8</span></span>](jquery-ui/cdnjqueryui188.md "jQuery UI 1.8.8 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-299">jQuery UI 1.8.7</span><span class="sxs-lookup"><span data-stu-id="0ae52-299">jQuery UI 1.8.7</span></span>](jquery-ui/cdnjqueryui187.md "jQuery UI 1.8.7 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-300">jQuery UI 1.8.6</span><span class="sxs-lookup"><span data-stu-id="0ae52-300">jQuery UI 1.8.6</span></span>](jquery-ui/cdnjqueryui186.md "jQuery UI 1.8.6 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-301">jQuery UI 1.8.5</span><span class="sxs-lookup"><span data-stu-id="0ae52-301">jQuery UI 1.8.5</span></span>](jquery-ui/cdnjqueryui185.md "jQuery UI 1.8.5")

<a id="jQuery_Validation_Releases_on_the_CDN_3"></a>

### <a name="jquery-validation-releases-on-the-cdn"></a><span data-ttu-id="0ae52-302">jQuery 유효성 검사는 CDN에 있는 릴리스</span><span class="sxs-lookup"><span data-stu-id="0ae52-302">jQuery Validation Releases on the CDN</span></span>

<span data-ttu-id="0ae52-303">JQuery 유효성 검사 라이브러리의 다음 릴리스에서이 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-303">The following releases of the jQuery Validation library are hosted on this CDN.</span></span> <span data-ttu-id="0ae52-304">파일의 실제 목록을 확인 하려면 각 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-304">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="0ae52-305">jQuery 유효성 검사 1.17.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-305">jQuery Validate 1.17.0</span></span>](jquery-validate/cdnjqueryvalidate1170.md "jQuery 유효성 검사 1.17.0")
- [<span data-ttu-id="0ae52-306">jQuery 유효성 검사 1.16.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-306">jQuery Validate 1.16.0</span></span>](jquery-validate/cdnjqueryvalidate1160.md "jQuery 유효성 검사 1.16.0")
- [<span data-ttu-id="0ae52-307">jQuery 유효성 검사 1.15.1</span><span class="sxs-lookup"><span data-stu-id="0ae52-307">jQuery Validate 1.15.1</span></span>](jquery-validate/cdnjqueryvalidate1151.md "jQuery 유효성 검사 1.15.1")
- [<span data-ttu-id="0ae52-308">jQuery 유효성 검사 1.15.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-308">jQuery Validate 1.15.0</span></span>](jquery-validate/cdnjqueryvalidate1150.md "jQuery 유효성 검사 1.15.0")
- [<span data-ttu-id="0ae52-309">jQuery 유효성 검사 1.14.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-309">jQuery Validate 1.14.0</span></span>](jquery-validate/cdnjqueryvalidate1140.md "jQuery 유효성 검사 1.14.0")
- [<span data-ttu-id="0ae52-310">jQuery 유효성 검사 1.13.1</span><span class="sxs-lookup"><span data-stu-id="0ae52-310">jQuery Validate 1.13.1</span></span>](jquery-validate/cdnjqueryvalidate1131.md "jQuery 유효성 검사 1.13.1")
- [<span data-ttu-id="0ae52-311">jQuery 유효성 검사 1.13.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-311">jQuery Validate 1.13.0</span></span>](jquery-validate/cdnjqueryvalidate1130.md "jQuery 유효성 검사 1.13.0")
- [<span data-ttu-id="0ae52-312">jQuery 유효성 검사 1.12.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-312">jQuery Validate 1.12.0</span></span>](jquery-validate/cdnjqueryvalidate1120.md "jQuery 유효성 검사 1.12.0")
- [<span data-ttu-id="0ae52-313">jQuery 유효성 검사 1.11.1</span><span class="sxs-lookup"><span data-stu-id="0ae52-313">jQuery Validate 1.11.1</span></span>](jquery-validate/cdnjqueryvalidate1111.md "jQuery 유효성 검사 1.11.1")
- [<span data-ttu-id="0ae52-314">jQuery 유효성 검사 1.11.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-314">jQuery Validate 1.11.0</span></span>](jquery-validate/cdnjqueryvalidate111.md "jQuery 유효성 검사 1.11.0")
- [<span data-ttu-id="0ae52-315">jQuery 유효성 검사 1.10.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-315">jQuery Validate 1.10.0</span></span>](jquery-validate/cdnjqueryvalidate110.md "jQuery 유효성 검사 1.10.0")
- [<span data-ttu-id="0ae52-316">jQuery 유효성 검사 1.9</span><span class="sxs-lookup"><span data-stu-id="0ae52-316">jQuery Validate 1.9</span></span>](jquery-validate/cdnjqueryvalidate19.md "jquery.validate 버전 1.9")
- [<span data-ttu-id="0ae52-317">jQuery 유효성 검사 1.8.1</span><span class="sxs-lookup"><span data-stu-id="0ae52-317">jQuery Validate 1.8.1</span></span>](jquery-validate/cdnjqueryvalidate181.md "1.8.1 jquery.validate 버전")
- [<span data-ttu-id="0ae52-318">jQuery 유효성 검사 1.8</span><span class="sxs-lookup"><span data-stu-id="0ae52-318">jQuery Validate 1.8</span></span>](jquery-validate/cdnjqueryvalidate18.md "jquery.validate 버전 1.8")
- [<span data-ttu-id="0ae52-319">jQuery 유효성 검사 1.7</span><span class="sxs-lookup"><span data-stu-id="0ae52-319">jQuery Validate 1.7</span></span>](jquery-validate/cdnjqueryvalidate17.md "jquery.validate 버전 1.7")
- [<span data-ttu-id="0ae52-320">jQuery 유효성 검사 1.6</span><span class="sxs-lookup"><span data-stu-id="0ae52-320">jQuery Validate 1.6</span></span>](jquery-validate/cdnjqueryvalidate16.md "jQuery 유효성 검사 1.6")
- [<span data-ttu-id="0ae52-321">jQuery 유효성 검사 1.5.5</span><span class="sxs-lookup"><span data-stu-id="0ae52-321">jQuery Validate 1.5.5</span></span>](jquery-validate/cdnjqueryvalidate155.md "jQuery 유효성 검사 1.5.5")

<a id="jQuery_Mobile_Releases_on_the_CDN_4"></a>

### <a name="jquery-mobile-releases-on-the-cdn"></a><span data-ttu-id="0ae52-322">jQuery Mobile CDN에 있는 릴리스</span><span class="sxs-lookup"><span data-stu-id="0ae52-322">jQuery Mobile Releases on the CDN</span></span>

<span data-ttu-id="0ae52-323">JQuery 모바일 라이브러리의 다음 릴리스에서이 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-323">The following releases of the jQuery Mobile library are hosted on this CDN.</span></span> <span data-ttu-id="0ae52-324">파일의 실제 목록을 확인 하려면 각 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-324">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="0ae52-325">jQuery Mobile 1.4.5</span><span class="sxs-lookup"><span data-stu-id="0ae52-325">jQuery Mobile 1.4.5</span></span>](jquery-mobile/cdnjquerymobile145.md "jQuery Mobile 1.4.5 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-326">jQuery Mobile 1.4.2</span><span class="sxs-lookup"><span data-stu-id="0ae52-326">jQuery Mobile 1.4.2</span></span>](jquery-mobile/cdnjquerymobile142.md "jQuery Mobile 1.4.2 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-327">jQuery Mobile 1.4.1</span><span class="sxs-lookup"><span data-stu-id="0ae52-327">jQuery Mobile 1.4.1</span></span>](jquery-mobile/cdnjquerymobile141.md "jQuery Mobile 1.4.1 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-328">jQuery Mobile 1.4.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-328">jQuery Mobile 1.4.0</span></span>](jquery-mobile/cdnjquerymobile140.md "jQuery Mobile 1.4.0 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-329">jQuery Mobile 1.3.2</span><span class="sxs-lookup"><span data-stu-id="0ae52-329">jQuery Mobile 1.3.2</span></span>](jquery-mobile/cdnjquerymobile132.md "jQuery Mobile 1.3.2 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-330">jQuery Mobile 1.3.1</span><span class="sxs-lookup"><span data-stu-id="0ae52-330">jQuery Mobile 1.3.1</span></span>](jquery-mobile/cdnjquerymobile131.md "jQuery Mobile 1.3.1 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-331">jQuery Mobile 1.3.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-331">jQuery Mobile 1.3.0</span></span>](jquery-mobile/cdnjquerymobile130.md "jQuery Mobile 1.3.0 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-332">jQuery Mobile 1.2.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-332">jQuery Mobile 1.2.0</span></span>](jquery-mobile/cdnjquerymobile120.md "jQuery Mobile 1.2.0 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-333">jQuery Mobile 1.1.2</span><span class="sxs-lookup"><span data-stu-id="0ae52-333">jQuery Mobile 1.1.2</span></span>](jquery-mobile/cdnjquerymobile112.md "jQuery Mobile 1.1.2 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-334">jQuery Mobile 1.1.1</span><span class="sxs-lookup"><span data-stu-id="0ae52-334">jQuery Mobile 1.1.1</span></span>](jquery-mobile/cdnjquerymobile111.md "jQuery Mobile 1.1.1 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-335">jQuery Mobile 1.1.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-335">jQuery Mobile 1.1.0</span></span>](jquery-mobile/cdnjquerymobile110.md "jQuery Mobile 1.1.0 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-336">jQuery Mobile 1.1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="0ae52-336">jQuery Mobile 1.1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile110rc2.md "jQuery Mobile 1.1.0 RC2 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-337">jQuery Mobile 1.0.1</span><span class="sxs-lookup"><span data-stu-id="0ae52-337">jQuery Mobile 1.0.1</span></span>](jquery-mobile/cdnjquerymobile101.md "jQuery Mobile 1.0.1 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-338">jQuery Mobile 1.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-338">jQuery Mobile 1.0</span></span>](jquery-mobile/cdnjquerymobile10.md "jQuery Mobile 1.0 Microsoft Ajax CDN에서")
- [<span data-ttu-id="0ae52-339">jQuery Mobile 1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="0ae52-339">jQuery Mobile 1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile10rc2.md "Microsoft Ajax CDN에서 jQuery Mobile 1.0 RC2")
- [<span data-ttu-id="0ae52-340">jQuery Mobile 1.0 RC 1</span><span class="sxs-lookup"><span data-stu-id="0ae52-340">jQuery Mobile 1.0 RC 1</span></span>](jquery-mobile/cdnjquerymobile10rc1.md "Microsoft Ajax CDN에서 jQuery Mobile 1.0 RC1")
- [<span data-ttu-id="0ae52-341">jQuery Mobile 1.0 베타 3</span><span class="sxs-lookup"><span data-stu-id="0ae52-341">jQuery Mobile 1.0 beta 3</span></span>](jquery-mobile/cdnjquerymobile10b3.md "Microsoft Ajax CDN에서 jQuery Mobile 1.0 베타 3")

<a id="jQuery_Templates_Releases_on_the_CDN_5"></a>

### <a name="jquery-templates-releases-on-the-cdn"></a><span data-ttu-id="0ae52-342">jQuery CDN에서 템플릿 릴리스</span><span class="sxs-lookup"><span data-stu-id="0ae52-342">jQuery Templates Releases on the CDN</span></span>

<span data-ttu-id="0ae52-343">다음 버전의 jQuery 템플릿 플러그 인이이 CDN에서 호스트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-343">The following releases of the jQuery Templates plugin are hosted on this CDN.</span></span> <span data-ttu-id="0ae52-344">파일의 실제 목록을 확인 하려면 각 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-344">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="0ae52-345">jQuery 템플릿 베타 1</span><span class="sxs-lookup"><span data-stu-id="0ae52-345">jQuery Templates Beta 1</span></span>](jquery-templates/cdnjquerytemplatesbeta1.md "jQuery 템플릿 베타 1")

<a id="jQuery_Cycle_Releases_on_the_CDN_6"></a>

### <a name="jquery-cycle-releases-on-the-cdn"></a><span data-ttu-id="0ae52-346">jQuery CDN에서 주기 릴리스</span><span class="sxs-lookup"><span data-stu-id="0ae52-346">jQuery Cycle Releases on the CDN</span></span>

<span data-ttu-id="0ae52-347">다음 릴리스에 jQuery 주기 플러그 인을이 CDN에서 호스트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-347">The following releases of the jQuery Cycle plugin are hosted on this CDN.</span></span> <span data-ttu-id="0ae52-348">파일의 실제 목록을 확인 하려면 각 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-348">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="0ae52-349">jQuery Cycle 2.99</span><span class="sxs-lookup"><span data-stu-id="0ae52-349">jQuery Cycle 2.99</span></span>](jquery-cycle/cdnjquerycycle299.md "jQuery Cycle 2.99")
- [<span data-ttu-id="0ae52-350">jQuery Cycle 2.94</span><span class="sxs-lookup"><span data-stu-id="0ae52-350">jQuery Cycle 2.94</span></span>](jquery-cycle/cdnjquerycycle294.md "jQuery Cycle 2.94")
- [<span data-ttu-id="0ae52-351">jQuery Cycle 2.88</span><span class="sxs-lookup"><span data-stu-id="0ae52-351">jQuery Cycle 2.88</span></span>](jquery-cycle/cdnjquerycycle288.md "jQuery Cycle 2.88")

<a id="jQuery_DataTables_Releases_on_the_CDN_7"></a>

### <a name="jquery-datatables-releases-on-the-cdn"></a><span data-ttu-id="0ae52-352">jQuery CDN에서 DataTables 릴리스</span><span class="sxs-lookup"><span data-stu-id="0ae52-352">jQuery DataTables Releases on the CDN</span></span>

<span data-ttu-id="0ae52-353">다음 릴리스에 jQuery Datatable 플러그 인을이 CDN에서 호스트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-353">The following releases of the jQuery DataTables plugin are hosted on this CDN.</span></span> <span data-ttu-id="0ae52-354">파일의 실제 목록을 확인 하려면 각 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-354">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="0ae52-355">jQuery Datatable 1.10.5</span><span class="sxs-lookup"><span data-stu-id="0ae52-355">jQuery DataTables 1.10.5</span></span>](jquery-datatables/cdnjquerydatatables105.md "jQuery Datatable 1.10.5")
- [<span data-ttu-id="0ae52-356">jQuery Datatable 1.10.4</span><span class="sxs-lookup"><span data-stu-id="0ae52-356">jQuery DataTables 1.10.4</span></span>](jquery-datatables/cdnjquerydatatables104.md "jQuery Datatable 1.10.4")
- [<span data-ttu-id="0ae52-357">jQuery Datatable 1.9.4</span><span class="sxs-lookup"><span data-stu-id="0ae52-357">jQuery DataTables 1.9.4</span></span>](jquery-datatables/cdnjquerydatatables194.md "jQuery Datatable 1.9.4")
- [<span data-ttu-id="0ae52-358">jQuery Datatable 1.9.3</span><span class="sxs-lookup"><span data-stu-id="0ae52-358">jQuery DataTables 1.9.3</span></span>](jquery-datatables/cdnjquerydatatables193.md "jQuery Datatable 1.9.3")
- [<span data-ttu-id="0ae52-359">jQuery Datatable 1.9.2</span><span class="sxs-lookup"><span data-stu-id="0ae52-359">jQuery DataTables 1.9.2</span></span>](jquery-datatables/cdnjquerydatatables192.md "jQuery Datatable 1.9.2")
- [<span data-ttu-id="0ae52-360">jQuery Datatable 1.9.1</span><span class="sxs-lookup"><span data-stu-id="0ae52-360">jQuery DataTables 1.9.1</span></span>](jquery-datatables/cdnjquerydatatables191.md "jQuery Datatable 1.9.1")
- [<span data-ttu-id="0ae52-361">jQuery Datatable 1.9.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-361">jQuery DataTables 1.9.0</span></span>](jquery-datatables/cdnjquerydatatables190.md "jQuery Datatable 1.9.0")
- [<span data-ttu-id="0ae52-362">jQuery Datatable 1.8.2</span><span class="sxs-lookup"><span data-stu-id="0ae52-362">jQuery DataTables 1.8.2</span></span>](jquery-datatables/cdnjquerydatatables182.md "jQuery Datatable 1.8.2")

<a id="Modernizr_Releases_on_the_CDN_8"></a>

### <a name="modernizr-releases-on-the-cdn"></a><span data-ttu-id="0ae52-363">CDN에서 Modernizr 릴리스</span><span class="sxs-lookup"><span data-stu-id="0ae52-363">Modernizr Releases on the CDN</span></span>

<span data-ttu-id="0ae52-364">다음 릴리스의 [Modernizr](http://www.modernizr.com "Modernizr") CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-364">The following releases of [Modernizr](http://www.modernizr.com "Modernizr") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.8.3.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.1.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.6.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-1.7-development-only.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.0.6-development-only.js

<a id="JSHint_Releases_on_the_CDN_10"></a>

### <a name="jshint-releases-on-the-cdn"></a><span data-ttu-id="0ae52-365">CDN에서 JSHint 릴리스</span><span class="sxs-lookup"><span data-stu-id="0ae52-365">JSHint Releases on the CDN</span></span>

<span data-ttu-id="0ae52-366">다음 릴리스의 [JSHint](http://www.jshint.com "JSHint") CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-366">The following releases of [JSHint](http://www.jshint.com "JSHint") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/jshint/r07/jshint.js

<a id="Knockout_Releases_on_the_CDN_11"></a>

### <a name="knockout-releases-on-the-cdn"></a><span data-ttu-id="0ae52-367">CDN에서 knockout 릴리스</span><span class="sxs-lookup"><span data-stu-id="0ae52-367">Knockout Releases on the CDN</span></span>

<span data-ttu-id="0ae52-368">다음 릴리스의 [Knockout](http://www.knockoutjs.com "Knockout") CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-368">The following releases of [Knockout](http://www.knockoutjs.com "Knockout") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.1.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.1.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.1.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.1.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.0.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.1.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.1.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.2.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.2.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.3.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.3.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.1.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.1.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.2.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.2.debug.js

<a id="Globalize_Releases_on_the_CDN_12"></a>

### <a name="globalize-releases-on-the-cdn"></a><span data-ttu-id="0ae52-369">CDN에서 릴리스 전역화</span><span class="sxs-lookup"><span data-stu-id="0ae52-369">Globalize Releases on the CDN</span></span>

<span data-ttu-id="0ae52-370">다음 릴리스의 [Globalize](https://github.com/jquery/globalize "Globalize") CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-370">The following releases of [Globalize](https://github.com/jquery/globalize "Globalize") are hosted on the CDN:</span></span>

#### <a name="globalize-version-100"></a><span data-ttu-id="0ae52-371">버전 1.0.0을 전역화</span><span class="sxs-lookup"><span data-stu-id="0ae52-371">Globalize version 1.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/node-main.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/currency.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/date.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/message.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/number.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/plural.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/relative-time.js

#### <a name="globalize-version-011"></a><span data-ttu-id="0ae52-372">버전 0.1.1 전역화</span><span class="sxs-lookup"><span data-stu-id="0ae52-372">Globalize version 0.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.min.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.cultures.js

    - <span data-ttu-id="0ae52-373">모든 문화권</span><span class="sxs-lookup"><span data-stu-id="0ae52-373">all cultures</span></span>
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.culture.{culture-code}.js

    - <span data-ttu-id="0ae52-374">"{코드 문화권을 (를)"를 원하는 culture 코드로 바꿉니다, globalize.culture.en GB.js== Microsoft CDN에 예를 들어 파일을이 = = Microsoft에서 라이브러리가 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-374">Replace "{culture-code}" with the desired culture code, e.g. globalize.culture.en-GB.js== Microsoft Files on the CDN ==These libraries were uploaded by Microsoft.</span></span>

<a id="Respond_Releases_on_the_CDN_13"></a>

### <a name="respond-releases-on-the-cdn"></a><span data-ttu-id="0ae52-375">CDN에서 릴리스 응답</span><span class="sxs-lookup"><span data-stu-id="0ae52-375">Respond Releases on the CDN</span></span>

<span data-ttu-id="0ae52-376">다음 릴리스의 [ https://github.com/scottjehl/Respond ] (https://github.com/scottjehl/Respond " https://github.com/scottjehl/Respond ") 응답 하는 CDN에 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-376">The following releases of [https://github.com/scottjehl/Respond](https://github.com/scottjehl/Respond "https://github.com/scottjehl/Respond") Respond are hosted on the CDN:</span></span>

#### <a name="respond-version-142"></a><span data-ttu-id="0ae52-377">1.4.2 버전 응답</span><span class="sxs-lookup"><span data-stu-id="0ae52-377">Respond version 1.4.2</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.min.js

#### <a name="respond-version-141"></a><span data-ttu-id="0ae52-378">1.4.1 버전 응답</span><span class="sxs-lookup"><span data-stu-id="0ae52-378">Respond version 1.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.min.js

#### <a name="respond-version-140"></a><span data-ttu-id="0ae52-379">버전 1.4.0 응답</span><span class="sxs-lookup"><span data-stu-id="0ae52-379">Respond version 1.4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.min.js

#### <a name="respond-version-130"></a><span data-ttu-id="0ae52-380">버전 1.3.0 응답</span><span class="sxs-lookup"><span data-stu-id="0ae52-380">Respond version 1.3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.3.0/respond.js

#### <a name="respond-version-120"></a><span data-ttu-id="0ae52-381">버전 1.2.0 응답</span><span class="sxs-lookup"><span data-stu-id="0ae52-381">Respond version 1.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.2.0/respond.js

<a id="Bootstrap_Releases_on_the_CDN_14"></a>

### <a name="bootstrap-releases-on-the-cdn"></a><span data-ttu-id="0ae52-382">CDN에서 부트스트랩 릴리스</span><span class="sxs-lookup"><span data-stu-id="0ae52-382">Bootstrap Releases on the CDN</span></span>

<span data-ttu-id="0ae52-383">다음 릴리스의 [getbootstrap.com](http://getbootstrap.com "getbootstrap.com") 부트스트랩 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-383">The following releases of [getbootstrap.com](http://getbootstrap.com "getbootstrap.com") bootstrap are hosted on the CDN:</span></span>

#### <a name="bootstrap-version-400"></a><span data-ttu-id="0ae52-384">부트스트랩 버전 4.0.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-384">Bootstrap version 4.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-337"></a><span data-ttu-id="0ae52-385">3.3.7 부트스트랩 버전</span><span class="sxs-lookup"><span data-stu-id="0ae52-385">Bootstrap version 3.3.7</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-336"></a><span data-ttu-id="0ae52-386">부트스트랩 버전 3.3.6</span><span class="sxs-lookup"><span data-stu-id="0ae52-386">Bootstrap version 3.3.6</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-335"></a><span data-ttu-id="0ae52-387">부트스트랩 버전 3.3.5</span><span class="sxs-lookup"><span data-stu-id="0ae52-387">Bootstrap version 3.3.5</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-334"></a><span data-ttu-id="0ae52-388">3.3.4 부트스트랩 버전</span><span class="sxs-lookup"><span data-stu-id="0ae52-388">Bootstrap version 3.3.4</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-332"></a><span data-ttu-id="0ae52-389">3.3.2 부트스트랩 버전</span><span class="sxs-lookup"><span data-stu-id="0ae52-389">Bootstrap version 3.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-331"></a><span data-ttu-id="0ae52-390">3.3.1 부트스트랩 버전</span><span class="sxs-lookup"><span data-stu-id="0ae52-390">Bootstrap version 3.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-330"></a><span data-ttu-id="0ae52-391">부트스트랩 버전 3.3.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-391">Bootstrap version 3.3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-320"></a><span data-ttu-id="0ae52-392">부트스트랩 버전 3.2.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-392">Bootstrap version 3.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-311"></a><span data-ttu-id="0ae52-393">3.1.1 부트스트랩 버전</span><span class="sxs-lookup"><span data-stu-id="0ae52-393">Bootstrap version 3.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-310"></a><span data-ttu-id="0ae52-394">부트스트랩 버전 3.1.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-394">Bootstrap version 3.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-303"></a><span data-ttu-id="0ae52-395">부트스트랩 버전 3.0.3</span><span class="sxs-lookup"><span data-stu-id="0ae52-395">Bootstrap version 3.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-302"></a><span data-ttu-id="0ae52-396">부트스트랩 버전 3.0.2</span><span class="sxs-lookup"><span data-stu-id="0ae52-396">Bootstrap version 3.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-301"></a><span data-ttu-id="0ae52-397">부트스트랩 버전 3.0.1</span><span class="sxs-lookup"><span data-stu-id="0ae52-397">Bootstrap version 3.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-300"></a><span data-ttu-id="0ae52-398">부트스트랩 버전 3.0.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-398">Bootstrap version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-232"></a><span data-ttu-id="0ae52-399">부트스트랩 버전 2.3.2</span><span class="sxs-lookup"><span data-stu-id="0ae52-399">Bootstrap version 2.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings-white.png

#### <a name="bootstrap-version-231"></a><span data-ttu-id="0ae52-400">부트스트랩 버전 2.3.1</span><span class="sxs-lookup"><span data-stu-id="0ae52-400">Bootstrap version 2.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings-white.png

<a id="BootstrapTouchCarousel_Releases_on_the_CDN_18"></a>

### <a name="bootstrap-touchcarousel-releases-on-the-cdn"></a><span data-ttu-id="0ae52-401">CDN에서 부트스트랩 TouchCarousel 릴리스</span><span class="sxs-lookup"><span data-stu-id="0ae52-401">Bootstrap TouchCarousel Releases on the CDN</span></span>

<span data-ttu-id="0ae52-402">다음 릴리스의 [ https://github.com/ixisio/bootstrap-touch-carousel ] (https://github.com/ixisio/bootstrap-touch-carousel " https://github.com/ixisio/bootstrap-touch-carousel ") 부트스트랩 TouchCarousel 릴리스 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-402">The following releases of [https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel") Bootstrap TouchCarousel releases are hosted on the CDN:</span></span>

#### <a name="bootstrap-touchcarousel-version-080"></a><span data-ttu-id="0ae52-403">부트스트랩 TouchCarousel 버전 0.8.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-403">Bootstrap TouchCarousel version 0.8.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/css/bootstrap-touch-carousel.css
- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/js/bootstrap-touch-carousel.js

<a id="Hammerjs_Releases_on_the_CDN_19"></a>

### <a name="hammerjs-releases-on-the-cdn"></a><span data-ttu-id="0ae52-404">CDN에서 Hammer.js 릴리스</span><span class="sxs-lookup"><span data-stu-id="0ae52-404">Hammer.js Releases on the CDN</span></span>

<span data-ttu-id="0ae52-405">다음 버전의 [ http://hammerjs.github.io/ ] (http://hammerjs.github.io/ " http://hammerjs.github.io/ ") Hammer.js 릴리스 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-405">The following releases of [http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/") Hammer.js releases are hosted on the CDN:</span></span>

#### <a name="hammerjs-version-204"></a><span data-ttu-id="0ae52-406">2.0.4 Hammer.js 버전</span><span class="sxs-lookup"><span data-stu-id="0ae52-406">Hammer.js version 2.0.4</span></span>

- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.map

<a id="ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15"></a>

### <a name="aspnet-web-forms-and-ajax-releases-on-the-cdn"></a><span data-ttu-id="0ae52-407">ASP.NET Web Forms 및 CDN에서 Ajax 릴리스</span><span class="sxs-lookup"><span data-stu-id="0ae52-407">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>

<span data-ttu-id="0ae52-408">ASP.NET Ajax 라이브러리의 다음 릴리스에서 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-408">The following releases of the ASP.NET Ajax Library are hosted on the CDN.</span></span> <span data-ttu-id="0ae52-409">파일의 실제 목록을 확인 하려면 각 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-409">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="0ae52-410">ASP.NET Web Forms 및 Ajax 버전 4.5.2</span><span class="sxs-lookup"><span data-stu-id="0ae52-410">ASP.NET Web Forms and Ajax version 4.5.2</span></span>](cdnajax452.md "ASP.NET Web Forms 및 Ajax 4.5.2")
- [<span data-ttu-id="0ae52-411">ASP.NET Web Forms 및 Ajax 버전 4</span><span class="sxs-lookup"><span data-stu-id="0ae52-411">ASP.NET Web Forms and Ajax version 4</span></span>](cdnajax4.md "ASP.NET Web Forms 및 Ajax 4")
- [<span data-ttu-id="0ae52-412">ASP.NET Ajax 버전 3.5</span><span class="sxs-lookup"><span data-stu-id="0ae52-412">ASP.NET Ajax version 3.5</span></span>](cdnajax35.md "ASP.NET Ajax 3.5")

<a id="ASPNET_MVC_Releases_on_the_CDN_16"></a>

### <a name="aspnet-mvc-releases-on-the-cdn"></a><span data-ttu-id="0ae52-413">CDN에 ASP.NET MVC 릴리스</span><span class="sxs-lookup"><span data-stu-id="0ae52-413">ASP.NET MVC Releases on the CDN</span></span>

<span data-ttu-id="0ae52-414">다음 ASP.NET MVC JavaScript 파일이이 CDN에서 호스트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-414">The following ASP.NET MVC JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-mvc-523"></a><span data-ttu-id="0ae52-415">ASP.NET MVC 5.2.3</span><span class="sxs-lookup"><span data-stu-id="0ae52-415">ASP.NET MVC 5.2.3</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-51"></a><span data-ttu-id="0ae52-416">ASP.NET MVC 5.1</span><span class="sxs-lookup"><span data-stu-id="0ae52-416">ASP.NET MVC 5.1</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-50"></a><span data-ttu-id="0ae52-417">ASP.NET MVC 5.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-417">ASP.NET MVC 5.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-40"></a><span data-ttu-id="0ae52-418">ASP.NET MVC 4.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-418">ASP.NET MVC 4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-30"></a><span data-ttu-id="0ae52-419">ASP.NET MVC 3.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-419">ASP.NET MVC 3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.min.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.min.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-20"></a><span data-ttu-id="0ae52-420">ASP.NET MVC 2.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-420">ASP.NET MVC 2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-10"></a><span data-ttu-id="0ae52-421">ASP.NET MVC 1.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-421">ASP.NET MVC 1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.debug.js

<a id="ASPNET_SignalR_Releases_on_the_CDN_17"></a>

### <a name="aspnet-signalr-releases-on-the-cdn"></a><span data-ttu-id="0ae52-422">CDN에서 ASP.NET SignalR 해제</span><span class="sxs-lookup"><span data-stu-id="0ae52-422">ASP.NET SignalR Releases on the CDN</span></span>

<span data-ttu-id="0ae52-423">다음 ASP.NET SignalR JavaScript 파일이이 CDN에서 호스트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-423">The following ASP.NET SignalR JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-signalr-222"></a><span data-ttu-id="0ae52-424">ASP.NET SignalR 2.2.2</span><span class="sxs-lookup"><span data-stu-id="0ae52-424">ASP.NET SignalR 2.2.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.js

#### <a name="aspnet-signalr-221"></a><span data-ttu-id="0ae52-425">ASP.NET SignalR 2.2.1</span><span class="sxs-lookup"><span data-stu-id="0ae52-425">ASP.NET SignalR 2.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.js

#### <a name="aspnet-signalr-220"></a><span data-ttu-id="0ae52-426">ASP.NET SignalR 2.2.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-426">ASP.NET SignalR 2.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.js

#### <a name="aspnet-signalr-210"></a><span data-ttu-id="0ae52-427">ASP.NET SignalR 2.1.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-427">ASP.NET SignalR 2.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.js

#### <a name="aspnet-signalr-203"></a><span data-ttu-id="0ae52-428">ASP.NET SignalR 2.0.3</span><span class="sxs-lookup"><span data-stu-id="0ae52-428">ASP.NET SignalR 2.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.js

#### <a name="aspnet-signalr-202"></a><span data-ttu-id="0ae52-429">ASP.NET SignalR 2.0.2</span><span class="sxs-lookup"><span data-stu-id="0ae52-429">ASP.NET SignalR 2.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.js

#### <a name="aspnet-signalr-201"></a><span data-ttu-id="0ae52-430">ASP.NET SignalR 2.0.1</span><span class="sxs-lookup"><span data-stu-id="0ae52-430">ASP.NET SignalR 2.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.js

#### <a name="aspnet-signalr-200"></a><span data-ttu-id="0ae52-431">ASP.NET SignalR 2.0.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-431">ASP.NET SignalR 2.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.js

#### <a name="aspnet-signalr-113"></a><span data-ttu-id="0ae52-432">ASP.NET SignalR 1.1.3</span><span class="sxs-lookup"><span data-stu-id="0ae52-432">ASP.NET SignalR 1.1.3</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.js

#### <a name="aspnet-signalr-112"></a><span data-ttu-id="0ae52-433">ASP.NET SignalR 1.1.2</span><span class="sxs-lookup"><span data-stu-id="0ae52-433">ASP.NET SignalR 1.1.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.js

#### <a name="aspnet-signalr-111"></a><span data-ttu-id="0ae52-434">ASP.NET SignalR 1.1.1</span><span class="sxs-lookup"><span data-stu-id="0ae52-434">ASP.NET SignalR 1.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.js

#### <a name="aspnet-signalr-110"></a><span data-ttu-id="0ae52-435">ASP.NET SignalR 1.1.0</span><span class="sxs-lookup"><span data-stu-id="0ae52-435">ASP.NET SignalR 1.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.js

#### <a name="aspnet-signalr-101"></a><span data-ttu-id="0ae52-436">ASP.NET SignalR 1.0.1</span><span class="sxs-lookup"><span data-stu-id="0ae52-436">ASP.NET SignalR 1.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.js

<span data-ttu-id="0ae52-437">CDN에 대 한 사용 조건에 대 한 정보를 참조 하십시오. [Microsoft Ajax CDN 사용 약관](https://www.asp.net/terms-of-use "Microsoft Ajax CDN 사용 약관")합니다.</span><span class="sxs-lookup"><span data-stu-id="0ae52-437">For information about the terms of use for the CDN, see [Microsoft Ajax CDN Terms of Use](https://www.asp.net/terms-of-use "Microsoft Ajax CDN Terms of Use").</span></span>
