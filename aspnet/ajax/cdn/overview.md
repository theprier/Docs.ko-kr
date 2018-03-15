---
uid: ajax/cdn/overview
title: "Microsoft Ajax 콘텐츠 배달 네트워크 | Microsoft Docs"
author: rick-anderson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/14/2017
ms.topic: article
ms.assetid: 8935bf14-ca6d-4a4e-9dbe-b96ce74cef49
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /ajax/cdn
msc.type: content
ms.openlocfilehash: f1225f06e5218d893e3f49b2ccc67d56365b30e5
ms.sourcegitcommit: 493a215355576cfa481773365de021bcf04bb9c7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
<a name="microsoft-ajax-content-delivery-network"></a><span data-ttu-id="b3197-102">Microsoft Ajax 콘텐츠 배달 네트워크</span><span class="sxs-lookup"><span data-stu-id="b3197-102">Microsoft Ajax Content Delivery Network</span></span>
====================
<span data-ttu-id="b3197-103">참고: Microsoft Ajax CDN에 Azure CDN을 사용 하 여 보다 많은 SLA는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-103">Note: The Microsoft Ajax CDN has no SLA above and beyond using an Azure CDN.</span></span>

## <a name="table-of-contents"></a><span data-ttu-id="b3197-104">목차</span><span class="sxs-lookup"><span data-stu-id="b3197-104">Table of Contents</span></span>

<span data-ttu-id="b3197-105">**[ajax.microsoft.com ajax.aspnetcdn.com로 변경](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span><span class="sxs-lookup"><span data-stu-id="b3197-105">**[ajax.microsoft.com renamed to ajax.aspnetcdn.com](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span></span>  
<span data-ttu-id="b3197-106">**[Visual Studio .vsdoc Support](#Visual_Studio_vsdoc_Support_19)**</span><span class="sxs-lookup"><span data-stu-id="b3197-106">**[Visual Studio .vsdoc Support](#Visual_Studio_vsdoc_Support_19)**</span></span>  
<span data-ttu-id="b3197-107">**[ASP.NET Ajax CDN에서 사용 하 여](#Using_ASPNET_Ajax_from_the_CDN_20)**</span><span class="sxs-lookup"><span data-stu-id="b3197-107">**[Using ASP.NET Ajax from the CDN](#Using_ASPNET_Ajax_from_the_CDN_20)**</span></span>  
<span data-ttu-id="b3197-108">**[CDN에서 jQuery를 사용 하 여](#Using_jQuery_from_the_CDN_21)**</span><span class="sxs-lookup"><span data-stu-id="b3197-108">**[Using jQuery from the CDN](#Using_jQuery_from_the_CDN_21)**</span></span>  
<span data-ttu-id="b3197-109">**[JQuery UI에서 CDN 사용 하 여](#Using_jQuery_UI_from_the_CDN_22)**</span><span class="sxs-lookup"><span data-stu-id="b3197-109">**[Using jQuery UI from the CDN](#Using_jQuery_UI_from_the_CDN_22)**</span></span>  
<span data-ttu-id="b3197-110">**[CDN에서 제 3 자 파일](#Third-Party_Files_on_the_CDN_23)**</span><span class="sxs-lookup"><span data-stu-id="b3197-110">**[Third-Party Files on the CDN](#Third-Party_Files_on_the_CDN_23)**</span></span>  
  
 [<span data-ttu-id="b3197-111">CDN에서 jQuery 릴리스</span><span class="sxs-lookup"><span data-stu-id="b3197-111">jQuery Releases on the CDN</span></span>](#jQuery_Releases_on_the_CDN_0)  
 [<span data-ttu-id="b3197-112">CDN에서 jQuery 마이그레이션할 릴리스</span><span class="sxs-lookup"><span data-stu-id="b3197-112">jQuery Migrate Releases on the CDN</span></span>](#jQuery_Migrate_Releases_on_the_CDN_1)  
 [<span data-ttu-id="b3197-113">jQuery UI CDN에 있는 릴리스</span><span class="sxs-lookup"><span data-stu-id="b3197-113">jQuery UI Releases on the CDN</span></span>](#jQuery_UI_Releases_on_the_CDN_2)  
 [<span data-ttu-id="b3197-114">jQuery 유효성 검사는 CDN에 있는 릴리스</span><span class="sxs-lookup"><span data-stu-id="b3197-114">jQuery Validation Releases on the CDN</span></span>](#jQuery_Validation_Releases_on_the_CDN_3)  
 [<span data-ttu-id="b3197-115">jQuery Mobile CDN에 있는 릴리스</span><span class="sxs-lookup"><span data-stu-id="b3197-115">jQuery Mobile Releases on the CDN</span></span>](#jQuery_Mobile_Releases_on_the_CDN_4)  
 [<span data-ttu-id="b3197-116">jQuery CDN에서 템플릿 릴리스</span><span class="sxs-lookup"><span data-stu-id="b3197-116">jQuery Templates Releases on the CDN</span></span>](#jQuery_Templates_Releases_on_the_CDN_5)  
 [<span data-ttu-id="b3197-117">jQuery CDN에서 주기 릴리스</span><span class="sxs-lookup"><span data-stu-id="b3197-117">jQuery Cycle Releases on the CDN</span></span>](#jQuery_Cycle_Releases_on_the_CDN_6)  
 [<span data-ttu-id="b3197-118">jQuery CDN에서 DataTables 릴리스</span><span class="sxs-lookup"><span data-stu-id="b3197-118">jQuery DataTables Releases on the CDN</span></span>](#jQuery_DataTables_Releases_on_the_CDN_7)  
 [<span data-ttu-id="b3197-119">CDN에서 Modernizr 릴리스</span><span class="sxs-lookup"><span data-stu-id="b3197-119">Modernizr Releases on the CDN</span></span>](#Modernizr_Releases_on_the_CDN_8)  
 [<span data-ttu-id="b3197-120">CDN에서 JSHint 릴리스</span><span class="sxs-lookup"><span data-stu-id="b3197-120">JSHint Releases on the CDN</span></span>](#JSHint_Releases_on_the_CDN_10)  
 [<span data-ttu-id="b3197-121">CDN에서 knockout 릴리스</span><span class="sxs-lookup"><span data-stu-id="b3197-121">Knockout Releases on the CDN</span></span>](#Knockout_Releases_on_the_CDN_11)  
 [<span data-ttu-id="b3197-122">CDN에서 릴리스 전역화</span><span class="sxs-lookup"><span data-stu-id="b3197-122">Globalize Releases on the CDN</span></span>](#Globalize_Releases_on_the_CDN_12)  
 [<span data-ttu-id="b3197-123">CDN에서 릴리스 응답</span><span class="sxs-lookup"><span data-stu-id="b3197-123">Respond Releases on the CDN</span></span>](#Respond_Releases_on_the_CDN_13)  
 [<span data-ttu-id="b3197-124">CDN에서 부트스트랩 릴리스</span><span class="sxs-lookup"><span data-stu-id="b3197-124">Bootstrap Releases on the CDN</span></span>](#Bootstrap_Releases_on_the_CDN_14)  
 [<span data-ttu-id="b3197-125">CDN에서 부트스트랩 TouchCarousel 릴리스</span><span class="sxs-lookup"><span data-stu-id="b3197-125">Bootstrap TouchCarousel Releases on the CDN</span></span>](#BootstrapTouchCarousel_Releases_on_the_CDN_18)  
 [<span data-ttu-id="b3197-126">CDN에서 Hammer.js 릴리스</span><span class="sxs-lookup"><span data-stu-id="b3197-126">Hammer.js Releases on the CDN</span></span>](#Hammerjs_Releases_on_the_CDN_19)  
 [<span data-ttu-id="b3197-127">ASP.NET Web Forms 및 CDN에서 Ajax 릴리스</span><span class="sxs-lookup"><span data-stu-id="b3197-127">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>](#ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15)  
 [<span data-ttu-id="b3197-128">CDN에 ASP.NET MVC 릴리스</span><span class="sxs-lookup"><span data-stu-id="b3197-128">ASP.NET MVC Releases on the CDN</span></span>](#ASPNET_MVC_Releases_on_the_CDN_16)  
 [<span data-ttu-id="b3197-129">CDN에서 ASP.NET SignalR 해제</span><span class="sxs-lookup"><span data-stu-id="b3197-129">ASP.NET SignalR Releases on the CDN</span></span>](#ASPNET_SignalR_Releases_on_the_CDN_17)

<span data-ttu-id="b3197-130">Microsoft Ajax 콘텐츠 배달 네트워크 (CDN) jQuery와 같은 인기 있는 제 3 자 JavaScript 라이브러리를 호스팅하고 웹 응용 프로그램에를 쉽게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-130">The Microsoft Ajax Content Delivery Network (CDN) hosts popular third party JavaScript libraries such as jQuery and enables you to easily add them to your Web applications.</span></span> <span data-ttu-id="b3197-131">이 CDN에서 호스팅되는 jQuery를 사용 하 여 추가 하 여 시작할 수는 예를 들어 한 &lt;스크립트&gt; ajax.aspnetcdn.com 가리키는 페이지에는 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-131">For example, you can start using jQuery which is hosted on this CDN simply by adding a &lt;script&gt; tag to your page that points to ajax.aspnetcdn.com.</span></span>

<span data-ttu-id="b3197-132">CDN 활용 하기 위해, Ajax 응용 프로그램의 성능을 크게 향상 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-132">By taking advantage of the CDN, you can significantly improve the performance of your Ajax applications.</span></span> <span data-ttu-id="b3197-133">CDN의 콘텐츠는 세계에 있는 서버에 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-133">The contents of the CDN are cached on servers located around the world.</span></span> <span data-ttu-id="b3197-134">또한 CDN에는 브라우저 서로 다른 도메인에 있는 웹 사이트에 대 한 캐시 된 제 3 자 JavaScript 파일을 다시 사용할 수 있도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-134">In addition, the CDN enables browsers to reuse cached third party JavaScript files for web sites that are located in different domains.</span></span>

<span data-ttu-id="b3197-135">CDN은 Secure Sockets Layer를 사용 하 여 웹 페이지를 처리 해야 하는 경우 SSL (HTTPS)을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-135">The CDN supports SSL (HTTPS) in case you need to serve a web page using the Secure Sockets Layer.</span></span>

<span data-ttu-id="b3197-136">CDN 업로드 된 및 해당 라이브러리의 소유자가 사용자에 게 사용이 허가 하는 다음 제 3 자 스크립트 라이브러리를 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-136">The CDN hosts the following third party script libraries which have been uploaded, and are licensed to you, by the owners of those libraries:</span></span>

- <span data-ttu-id="b3197-137">jQuery (www.jquery.com)</span><span class="sxs-lookup"><span data-stu-id="b3197-137">jQuery (www.jquery.com)</span></span>
- <span data-ttu-id="b3197-138">jQuery UI (www.jqueryui.com)</span><span class="sxs-lookup"><span data-stu-id="b3197-138">jQuery UI (www.jqueryui.com)</span></span>
- <span data-ttu-id="b3197-139">jQuery Mobile (www.jquerymobile.com)</span><span class="sxs-lookup"><span data-stu-id="b3197-139">jQuery Mobile (www.jquerymobile.com)</span></span>
- <span data-ttu-id="b3197-140">jQuery 유효성 검사 (www.jquery.com)</span><span class="sxs-lookup"><span data-stu-id="b3197-140">jQuery Validation (www.jquery.com)</span></span>
- <span data-ttu-id="b3197-141">jQuery 주기 (www.malsup.com/jquery/cycle/)</span><span class="sxs-lookup"><span data-stu-id="b3197-141">jQuery Cycle (www.malsup.com/jquery/cycle/)</span></span>
- <span data-ttu-id="b3197-142">jQuery Datatable 드 (http://datatables.net/)</span><span class="sxs-lookup"><span data-stu-id="b3197-142">jQuery DataTables (http://datatables.net/)</span></span>

<span data-ttu-id="b3197-143">Microsoft Ajax CDN는 Microsoft에서 업로드 한 다음 라이브러리를도 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-143">The Microsoft Ajax CDN also includes the following libraries which have been uploaded by Microsoft:</span></span>

- <span data-ttu-id="b3197-144">ASP.NET Ajax</span><span class="sxs-lookup"><span data-stu-id="b3197-144">ASP.NET Ajax</span></span>
- <span data-ttu-id="b3197-145">ASP.NET MVC JavaScript 파일</span><span class="sxs-lookup"><span data-stu-id="b3197-145">ASP.NET MVC JavaScript Files</span></span>
- <span data-ttu-id="b3197-146">ASP.NET SignalR JavaScript 파일</span><span class="sxs-lookup"><span data-stu-id="b3197-146">ASP.NET SignalR JavaScript Files</span></span>

<span data-ttu-id="b3197-147">Microsoft는이 CDN에서 호스팅되는 모든 타사 라이브러리의 소유권을 주장 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-147">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="b3197-148">저작권 소유자는 라이브러리에 이러한 라이브러리를 라이선스 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-148">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="b3197-149">해당 저작권 소유자가 단독으로 다운로드 하 고 이러한 라이브러리를 사용 해야 할 수 있는 모든 권한이 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-149">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="b3197-150">이들은 Microsoft 라이브러리 Microsoft 지적 재산권 권한 라이선스 (묵시적된 특허 권한이 없음 포함) 없음이나 보증을이 CDN에서 호스트 되는 타사 라이브러리에 대 한 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-150">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<span data-ttu-id="b3197-151">JavaScript 라이브러리를 제출 하려면이 고 라이브러리에는 상위 JavaScript 라이브러리 중 하나 (에 나열 된 http://trends.builtwith.com) 또는 확장/플러그 인을 이러한 라이브러리는 (a) 인기 있는; 또는 (b) 유용한 ASP.NET에서 사용 하기 위해 다음에 게 문의 하십시오 AjaxCDNSubmission@Microsoft.com합니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-151">If you wish to submit your JavaScript library and your library is one of the top JavaScript libraries (as listed on http://trends.builtwith.com) or extensions/plugins to these libraries that are (a) popular; or (b) helpful for use on ASP.NET then please contact AjaxCDNSubmission@Microsoft.com.</span></span>

<a id="ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18"></a>

## <a name="ajaxmicrosoftcom-renamed-to-ajaxaspnetcdncom"></a><span data-ttu-id="b3197-152">ajax.microsoft.com ajax.aspnetcdn.com로 변경</span><span class="sxs-lookup"><span data-stu-id="b3197-152">ajax.microsoft.com renamed to ajax.aspnetcdn.com</span></span>

<span data-ttu-id="b3197-153">CDN은 microsoft.com 도메인 이름을 사용 하는 데 사용 하 고 aspnetcdn.com 도메인 이름을 사용 하도록 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-153">The CDN used to use the microsoft.com domain name and has been changed to use the aspnetcdn.com domain name.</span></span> <span data-ttu-id="b3197-154">각 요청과 함께 네트워크를 통해 모든 쿠키를 보내야 해당 도메인에서 했기 브라우저 microsoft.com 도메인을 참조 하기 때문에 성능을 향상 시키기 위해이 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-154">This change was made to increase performance because when a browser referenced the microsoft.com domain it would send any cookies from that domain across the wire with each request.</span></span> <span data-ttu-id="b3197-155">Microsoft.com 이외의 도메인 이름으로 바꾸어 25%로 많은 성능으로 증가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-155">By renaming to a domain name other than microsoft.com performance can be increased by as much to 25%.</span></span> <span data-ttu-id="b3197-156">참고 ajax.microsoft.com은 계속 작동 하지만 ajax.aspnetcdn.com를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-156">Note ajax.microsoft.com will continue to function but ajax.aspnetcdn.com is recommended.</span></span>

- <span data-ttu-id="b3197-157">이전 형식: http://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="b3197-157">Old Format: http://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span></span>
- <span data-ttu-id="b3197-158">새 형식: http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="b3197-158">New Format: http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span></span>

<a id="Visual_Studio_vsdoc_Support_19"></a>

## <a name="visual-studio-vsdoc-support"></a><span data-ttu-id="b3197-159">Visual Studio.vsdoc 지원</span><span class="sxs-lookup"><span data-stu-id="b3197-159">Visual Studio .vsdoc Support</span></span>

<span data-ttu-id="b3197-160">Visual Studio 2008 및 2008 s p 1이 있는지 확인 해야 할.vsdoc 파일을 제대로 사용 하려면 설치 하 고 vsdoc 파일에 대 한 핫픽스를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-160">To use the .vsdoc files properly with Visual Studio 2008 you need to make sure that you have VS 2008 SP1 installed and the hotfix for vsdoc files installed.</span></span> <span data-ttu-id="b3197-161">여기에서 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-161">You can get these from here:</span></span>

- [<span data-ttu-id="b3197-162">Visual Studio 2008 s p 1을 다운로드</span><span class="sxs-lookup"><span data-stu-id="b3197-162">Download Visual Studio 2008 SP1</span></span>](https://www.microsoft.com/downloads/en/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en "Visual Studio 2008 s p 1을 다운로드 합니다.")
- [<span data-ttu-id="b3197-163">Visual Studio 2008 s p 1에 대 한.vsdoc 핫픽스 다운로드</span><span class="sxs-lookup"><span data-stu-id="b3197-163">Download .vsdoc hotfix for Visual Studio 2008 SP1</span></span>](https://code.msdn.microsoft.com/KB958502/Release/ProjectReleases.aspx?ReleaseId=1736 "Visual Studio 2008 s p 1에 대 한.vsdoc 핫픽스 다운로드")

<span data-ttu-id="b3197-164">Visual Studio 2010 추가 패치 없이.vsdoc 파일을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-164">Visual Studio 2010 supports .vsdoc files without any additional patches.</span></span>

<a id="Using_ASPNET_Ajax_from_the_CDN_20"></a>

## <a name="using-aspnet-ajax-from-the-cdn"></a><span data-ttu-id="b3197-165">ASP.NET Ajax CDN에서 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="b3197-165">Using ASP.NET Ajax from the CDN</span></span>

<span data-ttu-id="b3197-166">ASP.NET 4를 사용 하는 경우 cdn ASP.NET framework 스크립트에 대 한 모든 요청을 리디렉션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-166">When using ASP.NET 4, you can redirect all requests for ASP.NET framework scripts to the CDN.</span></span> <span data-ttu-id="b3197-167">로컬 웹 서버 대신 CDN에서 스크립트 검색 공용 ASP.NET 웹 사이트의 성능을 상당히 개선 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-167">Retrieving scripts from the CDN instead of your local web server can substantially improve the performance of public ASP.NET websites.</span></span>

<span data-ttu-id="b3197-168">ScriptManager EnableCDN 속성을 사용 하 여 모든 요청을 리디렉션할 ASP.NET 프레임 워크 스크립트 Microsoft Ajax CDN에:</span><span class="sxs-lookup"><span data-stu-id="b3197-168">Use the ScriptManager EnableCDN property to redirect all ASP.NET framework script requests to the Microsoft Ajax CDN:</span></span>

[!code-aspx[Main](overview/samples/sample1.aspx)]

<a id="Using_jQuery_from_the_CDN_21"></a>

## <a name="using-jquery-from-the-cdn"></a><span data-ttu-id="b3197-169">CDN에서 jQuery를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="b3197-169">Using jQuery from the CDN</span></span>

<span data-ttu-id="b3197-170">페이지에는 다음 스크립트 요소를 추가 하 여 CDN에서 웹 응용 프로그램에서 호스팅되는 jQuery 스크립트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-170">You can use jQuery scripts hosted on CDN in your Web application by adding the following script element to a page:</span></span>

[!code-html[Main](overview/samples/sample2.html)]

<span data-ttu-id="b3197-171">CDN에 액세스할 수 있는 jQuery 스크립트의 축소 된 버전도 포함 됩니다는 다음 요소를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="b3197-171">The CDN also includes the minified version of the jQuery script, which you can get using the following element:</span></span>

[!code-html[Main](overview/samples/sample3.html)]

<span data-ttu-id="b3197-172">대체 인증 CDN를 사용할 수 없는 경우 자신의 웹 사이트에 로컬 경로에서 jQuery를 로드 하려면 페이지를 허용 하려면 CDN 참조 요소 바로 뒤 다음 요소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-172">To allow your page to fallback to loading jQuery from a local path on your own website if the CDN happens to be unavailable, add the following element immediately after the element referencing the CDN:</span></span>

[!code-html[Main](overview/samples/sample4.html)]

<span data-ttu-id="b3197-173">다음 샘플 페이지 CDN 버전 (로컬 복사본으로 대체) 사용 하 여 jQuery 라이브러리의를 사용 하 여는 단추를 클릭할 때 div 요소 내용을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-173">The following sample page uses the CDN version of the jQuery library (with fallback to a local copy) to display the contents of a div element when a button is clicked.</span></span>

[!code-html[Main](overview/samples/sample5.html)]

<span data-ttu-id="b3197-174">JQuery에 대 한 자세한 정보 및 방문 하 여 jQuery의 로컬 복사본을 다운로드할 수 있습니다는 [jQuery](http://jquery.com/) 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-174">You can learn more about jQuery and download a local copy of jQuery by visiting the [jQuery](http://jquery.com/) Web site.</span></span>

<a id="Using_jQuery_UI_from_the_CDN_22"></a>

## <a name="using-jquery-ui-from-the-cdn"></a><span data-ttu-id="b3197-175">JQuery UI에서 CDN 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="b3197-175">Using jQuery UI from the CDN</span></span>

<span data-ttu-id="b3197-176">또한 CDN jQuery UI 라이브러리를 호스트합니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-176">The CDN also hosts the jQuery UI library.</span></span> <span data-ttu-id="b3197-177">JQuery UI 라이브러리는 다양 한 위젯 및 ASP.NET 응용 프로그램에서 사용할 수 있는 효과 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-177">The jQuery UI library includes a rich set of widgets and effects that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="b3197-178">예를 들어 다음 페이지는 ASP.NET Web Forms 응용 프로그램의 컨텍스트에서 jQuery UI Datepicker 팝업 달력이 표시를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-178">For example, the following page illustrates how you can use the jQuery UI Datepicker in the context of an ASP.NET Web Forms application to display a pop-up calendar:</span></span>

[!code-aspx[Main](overview/samples/sample6.aspx)]

<span data-ttu-id="b3197-179">키보드를 사용 하 여 텍스트 상자에 포커스를 이동 하면 달력이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-179">When you move focus to the TextBox using your keyboard, a calendar is displayed:</span></span>

![만든 Datepicker 팝업 일정](overview/_static/image1.png)

<span data-ttu-id="b3197-181">위의 코드에서 CDN에서 3 개의 파일을 포함 해야 하는 사항을 참고 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b3197-181">Notice that you must include three files from the CDN in the code above:</span></span>

- <span data-ttu-id="b3197-182">JQuery 라이브러리 &mdash; jQuery UI 라이브러리는 jQuery 라이브러리에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-182">The jQuery library &mdash; The jQuery UI library depends on the jQuery library.</span></span> <span data-ttu-id="b3197-183">JQuery 라이브러리 jQuery UI 라이브러리를 추가 하기 전에 페이지에 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-183">You must add the jQuery library to your page before you add the jQuery UI library.</span></span>
- <span data-ttu-id="b3197-184">JQuery UI 라이브러리 &mdash; jQuery UI 라이브러리 모든 위의 페이지에 사용 된 Datepicker 위젯 같은 위젯 및 jQuery UI 효과 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-184">The jQuery UI library &mdash; The jQuery UI library contains all of the jQuery UI effects and widgets such as the Datepicker widget used in the page above.</span></span>
- <span data-ttu-id="b3197-185">JQuery UI 테마 &mdash; jQuery UI 다양 한 테마를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-185">A jQuery UI theme &mdash; The jQuery UI supports different themes.</span></span> <span data-ttu-id="b3197-186">위의 페이지 Redmond 테마 가져올 CSS 파일에 대 한 링크를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-186">The page above includes a link to a CSS file to import the Redmond theme.</span></span>

<span data-ttu-id="b3197-187">모든 표준 jQuery UI 테마는 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-187">All of the standard jQuery UI themes are hosted on the CDN.</span></span> <span data-ttu-id="b3197-188">[이 페이지를 방문](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 Microsoft Ajax CDN에서") 각 테마에 대 한 축소판 그림을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-188">[Visit this page](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 on the Microsoft Ajax CDN") to view thumbnails for each theme.</span></span>

<span data-ttu-id="b3197-189">JQuery UI 라이브러리에 대 한 자세한 내용은 방문 공식 [jQuery UI 웹 사이트](http://jQueryUI.com "jQuery UI 웹 사이트")합니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-189">To learn more about the jQuery UI library, visit the official [jQuery UI website](http://jQueryUI.com "jQuery UI website").</span></span>

<a id="Third-Party_Files_on_the_CDN_23"></a>

## <a name="third-party-files-on-the-cdn"></a><span data-ttu-id="b3197-190">CDN에서 제 3 자 파일</span><span class="sxs-lookup"><span data-stu-id="b3197-190">Third-Party Files on the CDN</span></span>

<span data-ttu-id="b3197-191">CDN은 가장 일반적인 제 3 자 JavaScript 라이브러리 중 일부를 호스팅합니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-191">The CDN hosts some of the most popular third party JavaScript libraries.</span></span> <span data-ttu-id="b3197-192">Microsoft는이 CDN에서 호스팅되는 모든 타사 라이브러리의 소유권을 주장 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-192">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="b3197-193">저작권 소유자는 라이브러리에 이러한 라이브러리를 라이선스 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-193">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="b3197-194">해당 저작권 소유자가 단독으로 다운로드 하 고 이러한 라이브러리를 사용 해야 할 수 있는 모든 권한이 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-194">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="b3197-195">이들은 Microsoft 라이브러리 Microsoft 지적 재산권 권한 라이선스 (묵시적된 특허 권한이 없음 포함) 없음이나 보증을이 CDN에서 호스트 되는 타사 라이브러리에 대 한 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-195">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<a id="jQuery_Releases_on_the_CDN_0"></a>

### <a name="jquery-releases-on-the-cdn"></a><span data-ttu-id="b3197-196">CDN에서 jQuery 릴리스</span><span class="sxs-lookup"><span data-stu-id="b3197-196">jQuery Releases on the CDN</span></span>

<span data-ttu-id="b3197-197">다음 버전의 jQuery CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-197">The following releases of jQuery are hosted on the CDN:</span></span>

#### <a name="jquery-version-331"></a><span data-ttu-id="b3197-198">3.3.1 jQuery 버전</span><span class="sxs-lookup"><span data-stu-id="b3197-198">jQuery version 3.3.1</span></span>
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.map
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.map

#### <a name="jquery-version-321"></a><span data-ttu-id="b3197-199">jQuery 버전 3.2.1</span><span class="sxs-lookup"><span data-stu-id="b3197-199">jQuery version 3.2.1</span></span>
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.map
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.map

#### <a name="jquery-version-320"></a><span data-ttu-id="b3197-200">jQuery 버전 3.2.0</span><span class="sxs-lookup"><span data-stu-id="b3197-200">jQuery version 3.2.0</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.map
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.map

#### <a name="jquery-version-311"></a><span data-ttu-id="b3197-201">3.1.1 jQuery 버전</span><span class="sxs-lookup"><span data-stu-id="b3197-201">jQuery version 3.1.1</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.map
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.map

#### <a name="jquery-version-310"></a><span data-ttu-id="b3197-202">jQuery 버전 3.1.0</span><span class="sxs-lookup"><span data-stu-id="b3197-202">jQuery version 3.1.0</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.map
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.map

#### <a name="jquery-version-300"></a><span data-ttu-id="b3197-203">jQuery 버전 3.0.0</span><span class="sxs-lookup"><span data-stu-id="b3197-203">jQuery version 3.0.0</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.map
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.map

#### <a name="jquery-version-224"></a><span data-ttu-id="b3197-204">jQuery 버전 2.2.4</span><span class="sxs-lookup"><span data-stu-id="b3197-204">jQuery version 2.2.4</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.map

#### <a name="jquery-version-223"></a><span data-ttu-id="b3197-205">jQuery 버전 2.2.3</span><span class="sxs-lookup"><span data-stu-id="b3197-205">jQuery version 2.2.3</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.map

#### <a name="jquery-version-222"></a><span data-ttu-id="b3197-206">jQuery 버전 2.2.2</span><span class="sxs-lookup"><span data-stu-id="b3197-206">jQuery version 2.2.2</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.map

#### <a name="jquery-version-221"></a><span data-ttu-id="b3197-207">jQuery 버전 2.2.1</span><span class="sxs-lookup"><span data-stu-id="b3197-207">jQuery version 2.2.1</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.map

#### <a name="jquery-version-220"></a><span data-ttu-id="b3197-208">jQuery 버전 2.2.0</span><span class="sxs-lookup"><span data-stu-id="b3197-208">jQuery version 2.2.0</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.map

#### <a name="jquery-version-214"></a><span data-ttu-id="b3197-209">jQuery 버전 2.1.4</span><span class="sxs-lookup"><span data-stu-id="b3197-209">jQuery version 2.1.4</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.map

#### <a name="jquery-version-213"></a><span data-ttu-id="b3197-210">jQuery 버전 2.1.3</span><span class="sxs-lookup"><span data-stu-id="b3197-210">jQuery version 2.1.3</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.map

#### <a name="jquery-version-212"></a><span data-ttu-id="b3197-211">jQuery 버전 2.1.2</span><span class="sxs-lookup"><span data-stu-id="b3197-211">jQuery version 2.1.2</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.min.js

#### <a name="jquery-version-211"></a><span data-ttu-id="b3197-212">jQuery 버전 2.1.1</span><span class="sxs-lookup"><span data-stu-id="b3197-212">jQuery version 2.1.1</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.map

#### <a name="jquery-version-210"></a><span data-ttu-id="b3197-213">jQuery 버전 2.1.0</span><span class="sxs-lookup"><span data-stu-id="b3197-213">jQuery version 2.1.0</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0-vsdoc.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.map

#### <a name="jquery-version-203"></a><span data-ttu-id="b3197-214">jQuery 버전 2.0.3</span><span class="sxs-lookup"><span data-stu-id="b3197-214">jQuery version 2.0.3</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3-vsdoc.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.map

#### <a name="jquery-version-202"></a><span data-ttu-id="b3197-215">jQuery 버전 2.0.2</span><span class="sxs-lookup"><span data-stu-id="b3197-215">jQuery version 2.0.2</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2-vsdoc.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.map

#### <a name="jquery-version-201"></a><span data-ttu-id="b3197-216">jQuery 버전 2.0.1</span><span class="sxs-lookup"><span data-stu-id="b3197-216">jQuery version 2.0.1</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1-vsdoc.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.map

#### <a name="jquery-version-200"></a><span data-ttu-id="b3197-217">jQuery 버전 2.0.0</span><span class="sxs-lookup"><span data-stu-id="b3197-217">jQuery version 2.0.0</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0-vsdoc.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.map

#### <a name="jquery-version-1124"></a><span data-ttu-id="b3197-218">jQuery 버전 1.12.4</span><span class="sxs-lookup"><span data-stu-id="b3197-218">jQuery version 1.12.4</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.map

#### <a name="jquery-version-1123"></a><span data-ttu-id="b3197-219">jQuery 버전 1.12.3</span><span class="sxs-lookup"><span data-stu-id="b3197-219">jQuery version 1.12.3</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.map

#### <a name="jquery-version-1122"></a><span data-ttu-id="b3197-220">jQuery 버전 1.12.2</span><span class="sxs-lookup"><span data-stu-id="b3197-220">jQuery version 1.12.2</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.map

#### <a name="jquery-version-1121"></a><span data-ttu-id="b3197-221">jQuery 버전 1.12.1</span><span class="sxs-lookup"><span data-stu-id="b3197-221">jQuery version 1.12.1</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.map

#### <a name="jquery-version-1120"></a><span data-ttu-id="b3197-222">jQuery 버전 1.12.0</span><span class="sxs-lookup"><span data-stu-id="b3197-222">jQuery version 1.12.0</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.map

#### <a name="jquery-version-1113"></a><span data-ttu-id="b3197-223">jQuery 버전 1.11.3</span><span class="sxs-lookup"><span data-stu-id="b3197-223">jQuery version 1.11.3</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.map

#### <a name="jquery-version-1112"></a><span data-ttu-id="b3197-224">jQuery 버전 1.11.2</span><span class="sxs-lookup"><span data-stu-id="b3197-224">jQuery version 1.11.2</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.map

#### <a name="jquery-version-1111"></a><span data-ttu-id="b3197-225">jQuery 버전 1.11.1</span><span class="sxs-lookup"><span data-stu-id="b3197-225">jQuery version 1.11.1</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.map

#### <a name="jquery-version-1110"></a><span data-ttu-id="b3197-226">jQuery 버전 1.11.0</span><span class="sxs-lookup"><span data-stu-id="b3197-226">jQuery version 1.11.0</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0-vsdoc.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.map

#### <a name="jquery-version-1102"></a><span data-ttu-id="b3197-227">jQuery 1.10.2 버전</span><span class="sxs-lookup"><span data-stu-id="b3197-227">jQuery version 1.10.2</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2-vsdoc.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.map

#### <a name="jquery-version-1101"></a><span data-ttu-id="b3197-228">jQuery 버전 1.10.1</span><span class="sxs-lookup"><span data-stu-id="b3197-228">jQuery version 1.10.1</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1-vsdoc.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.map

#### <a name="jquery-version-1100"></a><span data-ttu-id="b3197-229">jQuery 버전 1.10.0</span><span class="sxs-lookup"><span data-stu-id="b3197-229">jQuery version 1.10.0</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0-vsdoc.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.map

#### <a name="jquery-version-191"></a><span data-ttu-id="b3197-230">jQuery 버전 1.9.1</span><span class="sxs-lookup"><span data-stu-id="b3197-230">jQuery version 1.9.1</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1-vsdoc.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.map

#### <a name="jquery-version-190"></a><span data-ttu-id="b3197-231">1.9.0 jQuery 버전</span><span class="sxs-lookup"><span data-stu-id="b3197-231">jQuery version 1.9.0</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0-vsdoc.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.map

#### <a name="jquery-version-183"></a><span data-ttu-id="b3197-232">1.8.3 jQuery 버전</span><span class="sxs-lookup"><span data-stu-id="b3197-232">jQuery version 1.8.3</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3-vsdoc.js

#### <a name="jquery-version-182"></a><span data-ttu-id="b3197-233">1.8.2 jQuery 버전</span><span class="sxs-lookup"><span data-stu-id="b3197-233">jQuery version 1.8.2</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2-vsdoc.js

#### <a name="jquery-version-181"></a><span data-ttu-id="b3197-234">1.8.1 jQuery 버전</span><span class="sxs-lookup"><span data-stu-id="b3197-234">jQuery version 1.8.1</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1-vsdoc.js

#### <a name="jquery-version-180"></a><span data-ttu-id="b3197-235">jQuery 버전 1.8.0</span><span class="sxs-lookup"><span data-stu-id="b3197-235">jQuery version 1.8.0</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0-vsdoc.js

#### <a name="jquery-version-172"></a><span data-ttu-id="b3197-236">1.7.2 jQuery 버전</span><span class="sxs-lookup"><span data-stu-id="b3197-236">jQuery version 1.7.2</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js

#### <a name="jquery-version-171"></a><span data-ttu-id="b3197-237">jQuery 버전 1.7.1</span><span class="sxs-lookup"><span data-stu-id="b3197-237">jQuery version 1.7.1</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1-vsdoc.js

#### <a name="jquery-version-17"></a><span data-ttu-id="b3197-238">jQuery 버전 1.7</span><span class="sxs-lookup"><span data-stu-id="b3197-238">jQuery version 1.7</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7-vsdoc.js

#### <a name="jquery-version-164"></a><span data-ttu-id="b3197-239">jQuery 버전 1.6.4</span><span class="sxs-lookup"><span data-stu-id="b3197-239">jQuery version 1.6.4</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4-vsdoc.js

#### <a name="jquery-version-163"></a><span data-ttu-id="b3197-240">jQuery 버전 1.6.3</span><span class="sxs-lookup"><span data-stu-id="b3197-240">jQuery version 1.6.3</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3-vsdoc.js

#### <a name="jquery-version-162"></a><span data-ttu-id="b3197-241">jQuery 버전 1.6.2</span><span class="sxs-lookup"><span data-stu-id="b3197-241">jQuery version 1.6.2</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2-vsdoc.js

#### <a name="jquery-version-161"></a><span data-ttu-id="b3197-242">jQuery 버전 1.6.1</span><span class="sxs-lookup"><span data-stu-id="b3197-242">jQuery version 1.6.1</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1-vsdoc.js

#### <a name="jquery-version-16"></a><span data-ttu-id="b3197-243">jQuery 버전 1.6</span><span class="sxs-lookup"><span data-stu-id="b3197-243">jQuery version 1.6</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6-vsdoc.js

#### <a name="jquery-version-152"></a><span data-ttu-id="b3197-244">1.5.2 jQuery 버전</span><span class="sxs-lookup"><span data-stu-id="b3197-244">jQuery version 1.5.2</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2-vsdoc.js

#### <a name="jquery-version-151"></a><span data-ttu-id="b3197-245">1.5.1 jQuery 버전</span><span class="sxs-lookup"><span data-stu-id="b3197-245">jQuery version 1.5.1</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1-vsdoc.js

#### <a name="jquery-version-15"></a><span data-ttu-id="b3197-246">jQuery 버전 1.5</span><span class="sxs-lookup"><span data-stu-id="b3197-246">jQuery version 1.5</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5-vsdoc.js

#### <a name="jquery-version-144"></a><span data-ttu-id="b3197-247">jQuery 버전 1.4.4</span><span class="sxs-lookup"><span data-stu-id="b3197-247">jQuery version 1.4.4</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4-vsdoc.js

#### <a name="jquery-version-143"></a><span data-ttu-id="b3197-248">jQuery 버전 1.4.3</span><span class="sxs-lookup"><span data-stu-id="b3197-248">jQuery version 1.4.3</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3-vsdoc.js

#### <a name="jquery-version-142"></a><span data-ttu-id="b3197-249">1.4.2 jQuery 버전</span><span class="sxs-lookup"><span data-stu-id="b3197-249">jQuery version 1.4.2</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2-vsdoc.js

#### <a name="jquery-version-141"></a><span data-ttu-id="b3197-250">1.4.1 jQuery 버전</span><span class="sxs-lookup"><span data-stu-id="b3197-250">jQuery version 1.4.1</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1-vsdoc.js

#### <a name="jquery-version-14"></a><span data-ttu-id="b3197-251">jQuery 버전 1.4</span><span class="sxs-lookup"><span data-stu-id="b3197-251">jQuery version 1.4</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.min.js

#### <a name="jquery-version-132"></a><span data-ttu-id="b3197-252">1.3.2 jQuery 버전</span><span class="sxs-lookup"><span data-stu-id="b3197-252">jQuery version 1.3.2</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2-vsdoc.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min-vsdoc.js

<a id="jQuery_Migrate_Releases_on_the_CDN_1"></a>

### <a name="jquery-migrate-releases-on-the-cdn"></a><span data-ttu-id="b3197-253">CDN에서 jQuery 마이그레이션할 릴리스</span><span class="sxs-lookup"><span data-stu-id="b3197-253">jQuery Migrate Releases on the CDN</span></span>

<span data-ttu-id="b3197-254">다음 버전의 jQuery 마이그레이션 CDN에 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-254">The following releases of jQuery Migrate are hosted on the CDN:</span></span>

#### <a name="jquery-migrate-version-300"></a><span data-ttu-id="b3197-255">jQuery 버전 3.0.0 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="b3197-255">jQuery Migrate version 3.0.0</span></span>

- http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.js
- http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.min.js

#### <a name="jquery-migrate-version-121"></a><span data-ttu-id="b3197-256">jQuery 버전 1.2.1 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="b3197-256">jQuery Migrate version 1.2.1</span></span>

- http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.js
- http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.min.js

<span data-ttu-id="b3197-257">jQuery 버전 1.2.0 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="b3197-257">jQuery Migrate version 1.2.0</span></span>

- http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.js
- http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.min.js

#### <a name="jquery-migrate-version-111"></a><span data-ttu-id="b3197-258">jQuery 버전 1.1.1 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="b3197-258">jQuery Migrate version 1.1.1</span></span>

- http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.js
- http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.min.js

#### <a name="jquery-migrate-version-110"></a><span data-ttu-id="b3197-259">jQuery 버전 1.1.0 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="b3197-259">jQuery Migrate version 1.1.0</span></span>

- http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.js
- http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.min.js

#### <a name="jquery-migrate-version-100"></a><span data-ttu-id="b3197-260">jQuery 버전 1.0.0 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="b3197-260">jQuery Migrate version 1.0.0</span></span>

- http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.js
- http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.min.js

<a id="jQuery_UI_Releases_on_the_CDN_2"></a>

### <a name="jquery-ui-releases-on-the-cdn"></a><span data-ttu-id="b3197-261">jQuery UI CDN에 있는 릴리스</span><span class="sxs-lookup"><span data-stu-id="b3197-261">jQuery UI Releases on the CDN</span></span>

<span data-ttu-id="b3197-262">JQuery UI 라이브러리의 다음 릴리스에서이 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-262">The following releases of the jQuery UI library are hosted on this CDN.</span></span> <span data-ttu-id="b3197-263">파일의 실제 목록을 확인 하려면 각 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-263">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="b3197-264">jQuery UI 1.12.1</span><span class="sxs-lookup"><span data-stu-id="b3197-264">jQuery UI 1.12.1</span></span>](jquery-ui/cdnjqueryui1121.md "jQuery UI 1.12.1 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-265">jQuery UI 1.12.0</span><span class="sxs-lookup"><span data-stu-id="b3197-265">jQuery UI 1.12.0</span></span>](jquery-ui/cdnjqueryui1120.md "jQuery UI 1.12.0 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-266">jQuery UI 1.11.4</span><span class="sxs-lookup"><span data-stu-id="b3197-266">jQuery UI 1.11.4</span></span>](jquery-ui/cdnjqueryui1114.md "jQuery UI 1.11.4 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-267">jQuery UI 1.11.3</span><span class="sxs-lookup"><span data-stu-id="b3197-267">jQuery UI 1.11.3</span></span>](jquery-ui/cdnjqueryui1113.md "jQuery UI 1.11.3 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-268">jQuery UI 1.11.2</span><span class="sxs-lookup"><span data-stu-id="b3197-268">jQuery UI 1.11.2</span></span>](jquery-ui/cdnjqueryui1112.md "jQuery UI 1.11.2 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-269">jQuery UI 1.11.1</span><span class="sxs-lookup"><span data-stu-id="b3197-269">jQuery UI 1.11.1</span></span>](jquery-ui/cdnjqueryui1111.md "jQuery UI 1.11.1 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-270">jQuery UI 1.11.0</span><span class="sxs-lookup"><span data-stu-id="b3197-270">jQuery UI 1.11.0</span></span>](jquery-ui/cdnjqueryui1110.md "jQuery UI 1.11.0 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-271">jQuery UI 1.10.4</span><span class="sxs-lookup"><span data-stu-id="b3197-271">jQuery UI 1.10.4</span></span>](jquery-ui/cdnjqueryui1104.md "jQuery UI 1.10.4 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-272">jQuery UI 1.10.3</span><span class="sxs-lookup"><span data-stu-id="b3197-272">jQuery UI 1.10.3</span></span>](jquery-ui/cdnjqueryui1103.md "jQuery UI 1.10.3 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-273">jQuery 1.10.2 UI</span><span class="sxs-lookup"><span data-stu-id="b3197-273">jQuery UI 1.10.2</span></span>](jquery-ui/cdnjqueryui1102.md "jQuery 1.10.2 Microsoft Ajax CDN에서 UI")
- [<span data-ttu-id="b3197-274">jQuery UI 1.10.1</span><span class="sxs-lookup"><span data-stu-id="b3197-274">jQuery UI 1.10.1</span></span>](jquery-ui/cdnjqueryui1101.md "jQuery UI 1.10.1 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-275">jQuery UI 1.10.0</span><span class="sxs-lookup"><span data-stu-id="b3197-275">jQuery UI 1.10.0</span></span>](jquery-ui/cdnjqueryui1100.md "jQuery UI 1.10.0 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-276">jQuery UI 1.9.2</span><span class="sxs-lookup"><span data-stu-id="b3197-276">jQuery UI 1.9.2</span></span>](jquery-ui/cdnjqueryui192.md "jQuery UI 1.9.2 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-277">jQuery UI 1.9.1</span><span class="sxs-lookup"><span data-stu-id="b3197-277">jQuery UI 1.9.1</span></span>](jquery-ui/cdnjqueryui191.md "jQuery UI 1.9.1 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-278">jQuery UI 1.9.0</span><span class="sxs-lookup"><span data-stu-id="b3197-278">jQuery UI 1.9.0</span></span>](jquery-ui/cdnjqueryui190.md "jQuery UI 1.9.0 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-279">jQuery UI 1.8.24</span><span class="sxs-lookup"><span data-stu-id="b3197-279">jQuery UI 1.8.24</span></span>](jquery-ui/cdnjqueryui1824.md "jQuery UI 1.8.24 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-280">jQuery UI 1.8.23</span><span class="sxs-lookup"><span data-stu-id="b3197-280">jQuery UI 1.8.23</span></span>](jquery-ui/cdnjqueryui1823.md "jQuery UI 1.8.23 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-281">jQuery UI 1.8.22</span><span class="sxs-lookup"><span data-stu-id="b3197-281">jQuery UI 1.8.22</span></span>](jquery-ui/cdnjqueryui1822.md "jQuery UI 1.8.22 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-282">jQuery UI 1.8.21</span><span class="sxs-lookup"><span data-stu-id="b3197-282">jQuery UI 1.8.21</span></span>](jquery-ui/cdnjqueryui1821.md "jQuery UI 1.8.21 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-283">jQuery UI 1.8.20</span><span class="sxs-lookup"><span data-stu-id="b3197-283">jQuery UI 1.8.20</span></span>](jquery-ui/cdnjqueryui1820.md "jQuery UI 1.8.20 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-284">jQuery UI 1.8.19</span><span class="sxs-lookup"><span data-stu-id="b3197-284">jQuery UI 1.8.19</span></span>](jquery-ui/cdnjqueryui1819.md "jQuery UI 1.8.19 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-285">jQuery UI 1.8.18</span><span class="sxs-lookup"><span data-stu-id="b3197-285">jQuery UI 1.8.18</span></span>](jquery-ui/cdnjqueryui1818.md "jQuery UI 1.8.18 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-286">jQuery UI 1.8.17</span><span class="sxs-lookup"><span data-stu-id="b3197-286">jQuery UI 1.8.17</span></span>](jquery-ui/cdnjqueryui1817.md "jQuery UI 1.8.17 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-287">jQuery UI 1.8.16</span><span class="sxs-lookup"><span data-stu-id="b3197-287">jQuery UI 1.8.16</span></span>](jquery-ui/cdnjqueryui1816.md "jQuery UI 1.8.16 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-288">jQuery UI 1.8.15</span><span class="sxs-lookup"><span data-stu-id="b3197-288">jQuery UI 1.8.15</span></span>](jquery-ui/cdnjqueryui1815.md "jQuery UI 1.8.15 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-289">jQuery UI 1.8.14</span><span class="sxs-lookup"><span data-stu-id="b3197-289">jQuery UI 1.8.14</span></span>](jquery-ui/cdnjqueryui1814.md "jQuery UI 1.8.14 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-290">jQuery UI 1.8.13</span><span class="sxs-lookup"><span data-stu-id="b3197-290">jQuery UI 1.8.13</span></span>](jquery-ui/cdnjqueryui1813.md "jQuery UI 1.8.13 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-291">jQuery UI 1.8.12</span><span class="sxs-lookup"><span data-stu-id="b3197-291">jQuery UI 1.8.12</span></span>](jquery-ui/cdnjqueryui1812.md "jQuery UI 1.8.12 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-292">jQuery UI 1.8.11</span><span class="sxs-lookup"><span data-stu-id="b3197-292">jQuery UI 1.8.11</span></span>](jquery-ui/cdnjqueryui1811.md "jQuery UI 1.8.11 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-293">jQuery UI 1.8.10</span><span class="sxs-lookup"><span data-stu-id="b3197-293">jQuery UI 1.8.10</span></span>](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-294">jQuery UI 1.8.9</span><span class="sxs-lookup"><span data-stu-id="b3197-294">jQuery UI 1.8.9</span></span>](jquery-ui/cdnjqueryui189.md "jQuery UI 1.8.9 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-295">jQuery UI 1.8.8</span><span class="sxs-lookup"><span data-stu-id="b3197-295">jQuery UI 1.8.8</span></span>](jquery-ui/cdnjqueryui188.md "jQuery UI 1.8.8 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-296">jQuery UI 1.8.7</span><span class="sxs-lookup"><span data-stu-id="b3197-296">jQuery UI 1.8.7</span></span>](jquery-ui/cdnjqueryui187.md "jQuery UI 1.8.7 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-297">jQuery UI 1.8.6</span><span class="sxs-lookup"><span data-stu-id="b3197-297">jQuery UI 1.8.6</span></span>](jquery-ui/cdnjqueryui186.md "jQuery UI 1.8.6 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-298">jQuery UI 1.8.5</span><span class="sxs-lookup"><span data-stu-id="b3197-298">jQuery UI 1.8.5</span></span>](jquery-ui/cdnjqueryui185.md "jQuery UI 1.8.5")

<a id="jQuery_Validation_Releases_on_the_CDN_3"></a>

### <a name="jquery-validation-releases-on-the-cdn"></a><span data-ttu-id="b3197-299">jQuery 유효성 검사는 CDN에 있는 릴리스</span><span class="sxs-lookup"><span data-stu-id="b3197-299">jQuery Validation Releases on the CDN</span></span>

<span data-ttu-id="b3197-300">JQuery 유효성 검사 라이브러리의 다음 릴리스에서이 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-300">The following releases of the jQuery Validation library are hosted on this CDN.</span></span> <span data-ttu-id="b3197-301">파일의 실제 목록을 확인 하려면 각 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-301">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="b3197-302">jQuery 유효성 검사 1.17.0</span><span class="sxs-lookup"><span data-stu-id="b3197-302">jQuery Validate 1.17.0</span></span>](jquery-validate/cdnjqueryvalidate1170.md "jQuery 유효성 검사 1.17.0")
- [<span data-ttu-id="b3197-303">jQuery 유효성 검사 1.16.0</span><span class="sxs-lookup"><span data-stu-id="b3197-303">jQuery Validate 1.16.0</span></span>](jquery-validate/cdnjqueryvalidate1160.md "jQuery 유효성 검사 1.16.0")
- [<span data-ttu-id="b3197-304">jQuery 유효성 검사 1.15.1</span><span class="sxs-lookup"><span data-stu-id="b3197-304">jQuery Validate 1.15.1</span></span>](jquery-validate/cdnjqueryvalidate1151.md "jQuery 유효성 검사 1.15.1")
- [<span data-ttu-id="b3197-305">jQuery 유효성 검사 1.15.0</span><span class="sxs-lookup"><span data-stu-id="b3197-305">jQuery Validate 1.15.0</span></span>](jquery-validate/cdnjqueryvalidate1150.md "jQuery 유효성 검사 1.15.0")
- [<span data-ttu-id="b3197-306">jQuery 유효성 검사 1.14.0</span><span class="sxs-lookup"><span data-stu-id="b3197-306">jQuery Validate 1.14.0</span></span>](jquery-validate/cdnjqueryvalidate1140.md "jQuery 유효성 검사 1.14.0")
- [<span data-ttu-id="b3197-307">jQuery 유효성 검사 1.13.1</span><span class="sxs-lookup"><span data-stu-id="b3197-307">jQuery Validate 1.13.1</span></span>](jquery-validate/cdnjqueryvalidate1131.md "jQuery 유효성 검사 1.13.1")
- [<span data-ttu-id="b3197-308">jQuery 유효성 검사 1.13.0</span><span class="sxs-lookup"><span data-stu-id="b3197-308">jQuery Validate 1.13.0</span></span>](jquery-validate/cdnjqueryvalidate1130.md "jQuery 유효성 검사 1.13.0")
- [<span data-ttu-id="b3197-309">jQuery 유효성 검사 1.12.0</span><span class="sxs-lookup"><span data-stu-id="b3197-309">jQuery Validate 1.12.0</span></span>](jquery-validate/cdnjqueryvalidate1120.md "jQuery 유효성 검사 1.12.0")
- [<span data-ttu-id="b3197-310">jQuery 유효성 검사 1.11.1</span><span class="sxs-lookup"><span data-stu-id="b3197-310">jQuery Validate 1.11.1</span></span>](jquery-validate/cdnjqueryvalidate1111.md "jQuery 유효성 검사 1.11.1")
- [<span data-ttu-id="b3197-311">jQuery 유효성 검사 1.11.0</span><span class="sxs-lookup"><span data-stu-id="b3197-311">jQuery Validate 1.11.0</span></span>](jquery-validate/cdnjqueryvalidate111.md "jQuery 유효성 검사 1.11.0")
- [<span data-ttu-id="b3197-312">jQuery 유효성 검사 1.10.0</span><span class="sxs-lookup"><span data-stu-id="b3197-312">jQuery Validate 1.10.0</span></span>](jquery-validate/cdnjqueryvalidate110.md "jQuery 유효성 검사 1.10.0")
- [<span data-ttu-id="b3197-313">jQuery 유효성 검사 1.9</span><span class="sxs-lookup"><span data-stu-id="b3197-313">jQuery Validate 1.9</span></span>](jquery-validate/cdnjqueryvalidate19.md "jquery.validate 버전 1.9")
- [<span data-ttu-id="b3197-314">jQuery 유효성 검사 1.8.1</span><span class="sxs-lookup"><span data-stu-id="b3197-314">jQuery Validate 1.8.1</span></span>](jquery-validate/cdnjqueryvalidate181.md "1.8.1 jquery.validate 버전")
- [<span data-ttu-id="b3197-315">jQuery 유효성 검사 1.8</span><span class="sxs-lookup"><span data-stu-id="b3197-315">jQuery Validate 1.8</span></span>](jquery-validate/cdnjqueryvalidate18.md "jquery.validate 버전 1.8")
- [<span data-ttu-id="b3197-316">jQuery 유효성 검사 1.7</span><span class="sxs-lookup"><span data-stu-id="b3197-316">jQuery Validate 1.7</span></span>](jquery-validate/cdnjqueryvalidate17.md "jquery.validate 버전 1.7")
- [<span data-ttu-id="b3197-317">jQuery 유효성 검사 1.6</span><span class="sxs-lookup"><span data-stu-id="b3197-317">jQuery Validate 1.6</span></span>](jquery-validate/cdnjqueryvalidate16.md "jQuery 유효성 검사 1.6")
- [<span data-ttu-id="b3197-318">jQuery 유효성 검사 1.5.5</span><span class="sxs-lookup"><span data-stu-id="b3197-318">jQuery Validate 1.5.5</span></span>](jquery-validate/cdnjqueryvalidate155.md "jQuery 유효성 검사 1.5.5")

<a id="jQuery_Mobile_Releases_on_the_CDN_4"></a>

### <a name="jquery-mobile-releases-on-the-cdn"></a><span data-ttu-id="b3197-319">jQuery Mobile CDN에 있는 릴리스</span><span class="sxs-lookup"><span data-stu-id="b3197-319">jQuery Mobile Releases on the CDN</span></span>

<span data-ttu-id="b3197-320">JQuery 모바일 라이브러리의 다음 릴리스에서이 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-320">The following releases of the jQuery Mobile library are hosted on this CDN.</span></span> <span data-ttu-id="b3197-321">파일의 실제 목록을 확인 하려면 각 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-321">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="b3197-322">jQuery Mobile 1.4.5</span><span class="sxs-lookup"><span data-stu-id="b3197-322">jQuery Mobile 1.4.5</span></span>](jquery-mobile/cdnjquerymobile145.md "jQuery Mobile 1.4.5 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-323">jQuery Mobile 1.4.2</span><span class="sxs-lookup"><span data-stu-id="b3197-323">jQuery Mobile 1.4.2</span></span>](jquery-mobile/cdnjquerymobile142.md "jQuery Mobile 1.4.2 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-324">jQuery Mobile 1.4.1</span><span class="sxs-lookup"><span data-stu-id="b3197-324">jQuery Mobile 1.4.1</span></span>](jquery-mobile/cdnjquerymobile141.md "jQuery Mobile 1.4.1 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-325">jQuery Mobile 1.4.0</span><span class="sxs-lookup"><span data-stu-id="b3197-325">jQuery Mobile 1.4.0</span></span>](jquery-mobile/cdnjquerymobile140.md "jQuery Mobile 1.4.0 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-326">jQuery Mobile 1.3.2</span><span class="sxs-lookup"><span data-stu-id="b3197-326">jQuery Mobile 1.3.2</span></span>](jquery-mobile/cdnjquerymobile132.md "jQuery Mobile 1.3.2 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-327">jQuery Mobile 1.3.1</span><span class="sxs-lookup"><span data-stu-id="b3197-327">jQuery Mobile 1.3.1</span></span>](jquery-mobile/cdnjquerymobile131.md "jQuery Mobile 1.3.1 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-328">jQuery Mobile 1.3.0</span><span class="sxs-lookup"><span data-stu-id="b3197-328">jQuery Mobile 1.3.0</span></span>](jquery-mobile/cdnjquerymobile130.md "jQuery Mobile 1.3.0 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-329">jQuery Mobile 1.2.0</span><span class="sxs-lookup"><span data-stu-id="b3197-329">jQuery Mobile 1.2.0</span></span>](jquery-mobile/cdnjquerymobile120.md "jQuery Mobile 1.2.0 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-330">jQuery Mobile 1.1.2</span><span class="sxs-lookup"><span data-stu-id="b3197-330">jQuery Mobile 1.1.2</span></span>](jquery-mobile/cdnjquerymobile112.md "jQuery Mobile 1.1.2 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-331">jQuery Mobile 1.1.1</span><span class="sxs-lookup"><span data-stu-id="b3197-331">jQuery Mobile 1.1.1</span></span>](jquery-mobile/cdnjquerymobile111.md "jQuery Mobile 1.1.1 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-332">jQuery Mobile 1.1.0</span><span class="sxs-lookup"><span data-stu-id="b3197-332">jQuery Mobile 1.1.0</span></span>](jquery-mobile/cdnjquerymobile110.md "jQuery Mobile 1.1.0 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-333">jQuery Mobile 1.1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="b3197-333">jQuery Mobile 1.1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile110rc2.md "jQuery Mobile 1.1.0 RC2 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-334">jQuery Mobile 1.0.1</span><span class="sxs-lookup"><span data-stu-id="b3197-334">jQuery Mobile 1.0.1</span></span>](jquery-mobile/cdnjquerymobile101.md "jQuery Mobile 1.0.1 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-335">jQuery Mobile 1.0</span><span class="sxs-lookup"><span data-stu-id="b3197-335">jQuery Mobile 1.0</span></span>](jquery-mobile/cdnjquerymobile10.md "jQuery Mobile 1.0 Microsoft Ajax CDN에서")
- [<span data-ttu-id="b3197-336">jQuery Mobile 1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="b3197-336">jQuery Mobile 1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile10rc2.md "Microsoft Ajax CDN에서 jQuery Mobile 1.0 RC2")
- [<span data-ttu-id="b3197-337">jQuery Mobile 1.0 RC 1</span><span class="sxs-lookup"><span data-stu-id="b3197-337">jQuery Mobile 1.0 RC 1</span></span>](jquery-mobile/cdnjquerymobile10rc1.md "Microsoft Ajax CDN에서 jQuery Mobile 1.0 RC1")
- [<span data-ttu-id="b3197-338">jQuery Mobile 1.0 베타 3</span><span class="sxs-lookup"><span data-stu-id="b3197-338">jQuery Mobile 1.0 beta 3</span></span>](jquery-mobile/cdnjquerymobile10b3.md "Microsoft Ajax CDN에서 jQuery Mobile 1.0 베타 3")

<a id="jQuery_Templates_Releases_on_the_CDN_5"></a>

### <a name="jquery-templates-releases-on-the-cdn"></a><span data-ttu-id="b3197-339">jQuery CDN에서 템플릿 릴리스</span><span class="sxs-lookup"><span data-stu-id="b3197-339">jQuery Templates Releases on the CDN</span></span>

<span data-ttu-id="b3197-340">다음 버전의 jQuery 템플릿 플러그 인이이 CDN에서 호스트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-340">The following releases of the jQuery Templates plugin are hosted on this CDN.</span></span> <span data-ttu-id="b3197-341">파일의 실제 목록을 확인 하려면 각 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-341">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="b3197-342">jQuery 템플릿 베타 1</span><span class="sxs-lookup"><span data-stu-id="b3197-342">jQuery Templates Beta 1</span></span>](jquery-templates/cdnjquerytemplatesbeta1.md "jQuery 템플릿 베타 1")

<a id="jQuery_Cycle_Releases_on_the_CDN_6"></a>

### <a name="jquery-cycle-releases-on-the-cdn"></a><span data-ttu-id="b3197-343">jQuery CDN에서 주기 릴리스</span><span class="sxs-lookup"><span data-stu-id="b3197-343">jQuery Cycle Releases on the CDN</span></span>

<span data-ttu-id="b3197-344">다음 릴리스에 jQuery 주기 플러그 인을이 CDN에서 호스트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-344">The following releases of the jQuery Cycle plugin are hosted on this CDN.</span></span> <span data-ttu-id="b3197-345">파일의 실제 목록을 확인 하려면 각 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-345">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="b3197-346">jQuery Cycle 2.99</span><span class="sxs-lookup"><span data-stu-id="b3197-346">jQuery Cycle 2.99</span></span>](jquery-cycle/cdnjquerycycle299.md "jQuery Cycle 2.99")
- [<span data-ttu-id="b3197-347">jQuery Cycle 2.94</span><span class="sxs-lookup"><span data-stu-id="b3197-347">jQuery Cycle 2.94</span></span>](jquery-cycle/cdnjquerycycle294.md "jQuery Cycle 2.94")
- [<span data-ttu-id="b3197-348">jQuery Cycle 2.88</span><span class="sxs-lookup"><span data-stu-id="b3197-348">jQuery Cycle 2.88</span></span>](jquery-cycle/cdnjquerycycle288.md "jQuery Cycle 2.88")

<a id="jQuery_DataTables_Releases_on_the_CDN_7"></a>

### <a name="jquery-datatables-releases-on-the-cdn"></a><span data-ttu-id="b3197-349">jQuery CDN에서 DataTables 릴리스</span><span class="sxs-lookup"><span data-stu-id="b3197-349">jQuery DataTables Releases on the CDN</span></span>

<span data-ttu-id="b3197-350">다음 릴리스에 jQuery Datatable 플러그 인을이 CDN에서 호스트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-350">The following releases of the jQuery DataTables plugin are hosted on this CDN.</span></span> <span data-ttu-id="b3197-351">파일의 실제 목록을 확인 하려면 각 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-351">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="b3197-352">jQuery Datatable 1.10.5</span><span class="sxs-lookup"><span data-stu-id="b3197-352">jQuery DataTables 1.10.5</span></span>](jquery-datatables/cdnjquerydatatables105.md "jQuery Datatable 1.10.5")
- [<span data-ttu-id="b3197-353">jQuery Datatable 1.10.4</span><span class="sxs-lookup"><span data-stu-id="b3197-353">jQuery DataTables 1.10.4</span></span>](jquery-datatables/cdnjquerydatatables104.md "jQuery Datatable 1.10.4")
- [<span data-ttu-id="b3197-354">jQuery Datatable 1.9.4</span><span class="sxs-lookup"><span data-stu-id="b3197-354">jQuery DataTables 1.9.4</span></span>](jquery-datatables/cdnjquerydatatables194.md "jQuery Datatable 1.9.4")
- [<span data-ttu-id="b3197-355">jQuery Datatable 1.9.3</span><span class="sxs-lookup"><span data-stu-id="b3197-355">jQuery DataTables 1.9.3</span></span>](jquery-datatables/cdnjquerydatatables193.md "jQuery Datatable 1.9.3")
- [<span data-ttu-id="b3197-356">jQuery Datatable 1.9.2</span><span class="sxs-lookup"><span data-stu-id="b3197-356">jQuery DataTables 1.9.2</span></span>](jquery-datatables/cdnjquerydatatables192.md "jQuery Datatable 1.9.2")
- [<span data-ttu-id="b3197-357">jQuery Datatable 1.9.1</span><span class="sxs-lookup"><span data-stu-id="b3197-357">jQuery DataTables 1.9.1</span></span>](jquery-datatables/cdnjquerydatatables191.md "jQuery Datatable 1.9.1")
- [<span data-ttu-id="b3197-358">jQuery Datatable 1.9.0</span><span class="sxs-lookup"><span data-stu-id="b3197-358">jQuery DataTables 1.9.0</span></span>](jquery-datatables/cdnjquerydatatables190.md "jQuery Datatable 1.9.0")
- [<span data-ttu-id="b3197-359">jQuery Datatable 1.8.2</span><span class="sxs-lookup"><span data-stu-id="b3197-359">jQuery DataTables 1.8.2</span></span>](jquery-datatables/cdnjquerydatatables182.md "jQuery Datatable 1.8.2")

<a id="Modernizr_Releases_on_the_CDN_8"></a>

### <a name="modernizr-releases-on-the-cdn"></a><span data-ttu-id="b3197-360">CDN에서 Modernizr 릴리스</span><span class="sxs-lookup"><span data-stu-id="b3197-360">Modernizr Releases on the CDN</span></span>

<span data-ttu-id="b3197-361">다음 릴리스의 [Modernizr](http://www.modernizr.com "Modernizr") CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-361">The following releases of [Modernizr](http://www.modernizr.com "Modernizr") are hosted on the CDN:</span></span>

- http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.8.3.js
- http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.2.js
- http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.1.js
- http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.6.2.js
- http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-1.7-development-only.js
- http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.0.6-development-only.js

<a id="JSHint_Releases_on_the_CDN_10"></a>

### <a name="jshint-releases-on-the-cdn"></a><span data-ttu-id="b3197-362">CDN에서 JSHint 릴리스</span><span class="sxs-lookup"><span data-stu-id="b3197-362">JSHint Releases on the CDN</span></span>

<span data-ttu-id="b3197-363">다음 릴리스의 [JSHint](http://www.jshint.com "JSHint") CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-363">The following releases of [JSHint](http://www.jshint.com "JSHint") are hosted on the CDN:</span></span>

- http://ajax.aspnetcdn.com/ajax/jshint/r07/jshint.js

<a id="Knockout_Releases_on_the_CDN_11"></a>

### <a name="knockout-releases-on-the-cdn"></a><span data-ttu-id="b3197-364">CDN에서 knockout 릴리스</span><span class="sxs-lookup"><span data-stu-id="b3197-364">Knockout Releases on the CDN</span></span>

<span data-ttu-id="b3197-365">다음 릴리스의 [Knockout](http://www.knockoutjs.com "Knockout") CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-365">The following releases of [Knockout](http://www.knockoutjs.com "Knockout") are hosted on the CDN:</span></span>

- http://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.1.js
- http://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.1.debug.js
- http://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.0.js
- http://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.0.debug.js
- http://ajax.aspnetcdn.com/ajax/knockout/knockout-2.1.0.js
- http://ajax.aspnetcdn.com/ajax/knockout/knockout-2.1.0.debug.js
- http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.0.0.js
- http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.0.0.debug.js
- http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.1.0.js
- http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.1.0.debug.js
- http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.2.0.js
- http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.2.0.debug.js
- http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.3.0.js
- http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.3.0.debug.js
- http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.0.js
- http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.0.debug.js
- http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.1.js
- http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.1.debug.js
- http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.2.js
- http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.2.debug.js

<a id="Globalize_Releases_on_the_CDN_12"></a>

### <a name="globalize-releases-on-the-cdn"></a><span data-ttu-id="b3197-366">CDN에서 릴리스 전역화</span><span class="sxs-lookup"><span data-stu-id="b3197-366">Globalize Releases on the CDN</span></span>

<span data-ttu-id="b3197-367">다음 릴리스의 [Globalize](https://github.com/jquery/globalize "Globalize") CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-367">The following releases of [Globalize](https://github.com/jquery/globalize "Globalize") are hosted on the CDN:</span></span>

#### <a name="globalize-version-100"></a><span data-ttu-id="b3197-368">버전 1.0.0을 전역화</span><span class="sxs-lookup"><span data-stu-id="b3197-368">Globalize version 1.0.0</span></span>

- http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize.js
- http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/node-main.js
- http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/currency.js
- http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/date.js
- http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/message.js
- http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/number.js
- http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/plural.js
- http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/relative-time.js

#### <a name="globalize-version-011"></a><span data-ttu-id="b3197-369">버전 0.1.1 전역화</span><span class="sxs-lookup"><span data-stu-id="b3197-369">Globalize version 0.1.1</span></span>

- http://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.min.js
- http://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.js
- http://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.cultures.js

    - <span data-ttu-id="b3197-370">모든 문화권</span><span class="sxs-lookup"><span data-stu-id="b3197-370">all cultures</span></span>
- http://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.culture.{culture-code}.js

    - <span data-ttu-id="b3197-371">"{코드 문화권을 (를)"를 원하는 culture 코드로 바꿉니다, globalize.culture.en GB.js== Microsoft CDN에 예를 들어 파일을이 = = Microsoft에서 라이브러리가 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-371">Replace "{culture-code}" with the desired culture code, e.g. globalize.culture.en-GB.js== Microsoft Files on the CDN ==These libraries were uploaded by Microsoft.</span></span>

<a id="Respond_Releases_on_the_CDN_13"></a>

### <a name="respond-releases-on-the-cdn"></a><span data-ttu-id="b3197-372">CDN에서 릴리스 응답</span><span class="sxs-lookup"><span data-stu-id="b3197-372">Respond Releases on the CDN</span></span>

<span data-ttu-id="b3197-373">다음 릴리스의 [ https://github.com/scottjehl/Respond ] (https://github.com/scottjehl/Respond " https://github.com/scottjehl/Respond ") 응답 하는 CDN에 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-373">The following releases of [https://github.com/scottjehl/Respond](https://github.com/scottjehl/Respond "https://github.com/scottjehl/Respond") Respond are hosted on the CDN:</span></span>

#### <a name="respond-version-142"></a><span data-ttu-id="b3197-374">1.4.2 버전 응답</span><span class="sxs-lookup"><span data-stu-id="b3197-374">Respond version 1.4.2</span></span>

- http://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.js
- http://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.min.js
- http://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.js
- http://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.min.js

#### <a name="respond-version-141"></a><span data-ttu-id="b3197-375">1.4.1 버전 응답</span><span class="sxs-lookup"><span data-stu-id="b3197-375">Respond version 1.4.1</span></span>

- http://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.js
- http://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.min.js
- http://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.js
- http://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.min.js

#### <a name="respond-version-140"></a><span data-ttu-id="b3197-376">버전 1.4.0 응답</span><span class="sxs-lookup"><span data-stu-id="b3197-376">Respond version 1.4.0</span></span>

- http://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.js
- http://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.min.js
- http://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.js
- http://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.min.js

#### <a name="respond-version-130"></a><span data-ttu-id="b3197-377">버전 1.3.0 응답</span><span class="sxs-lookup"><span data-stu-id="b3197-377">Respond version 1.3.0</span></span>

- http://ajax.aspnetcdn.com/ajax/respond/1.3.0/respond.js

#### <a name="respond-version-120"></a><span data-ttu-id="b3197-378">버전 1.2.0 응답</span><span class="sxs-lookup"><span data-stu-id="b3197-378">Respond version 1.2.0</span></span>

- http://ajax.aspnetcdn.com/ajax/respond/1.2.0/respond.js

<a id="Bootstrap_Releases_on_the_CDN_14"></a>

### <a name="bootstrap-releases-on-the-cdn"></a><span data-ttu-id="b3197-379">CDN에서 부트스트랩 릴리스</span><span class="sxs-lookup"><span data-stu-id="b3197-379">Bootstrap Releases on the CDN</span></span>

<span data-ttu-id="b3197-380">다음 릴리스의 [getbootstrap.com](http://getbootstrap.com "getbootstrap.com") 부트스트랩 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-380">The following releases of [getbootstrap.com](http://getbootstrap.com "getbootstrap.com") bootstrap are hosted on the CDN:</span></span>

#### <a name="bootstrap-version-400"></a><span data-ttu-id="b3197-381">부트스트랩 버전 4.0.0</span><span class="sxs-lookup"><span data-stu-id="b3197-381">Bootstrap version 4.0.0</span></span>

- http://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.min.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/fonts/glyphicons-halflings-regular.eot
- http://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/fonts/glyphicons-halflings-regular.svg
- http://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/fonts/glyphicons-halflings-regular.ttf
- http://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/fonts/glyphicons-halflings-regular.woff
- http://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-337"></a><span data-ttu-id="b3197-382">3.3.7 부트스트랩 버전</span><span class="sxs-lookup"><span data-stu-id="b3197-382">Bootstrap version 3.3.7</span></span>

- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.min.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.eot
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.svg
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.ttf
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-336"></a><span data-ttu-id="b3197-383">부트스트랩 버전 3.3.6</span><span class="sxs-lookup"><span data-stu-id="b3197-383">Bootstrap version 3.3.6</span></span>

- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/bootstrap.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/bootstrap.min.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.eot
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.svg
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.ttf
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.woff
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-335"></a><span data-ttu-id="b3197-384">부트스트랩 버전 3.3.5</span><span class="sxs-lookup"><span data-stu-id="b3197-384">Bootstrap version 3.3.5</span></span>

- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/bootstrap.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/bootstrap.min.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.eot
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.svg
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.ttf
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.woff
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-334"></a><span data-ttu-id="b3197-385">3.3.4 부트스트랩 버전</span><span class="sxs-lookup"><span data-stu-id="b3197-385">Bootstrap version 3.3.4</span></span>

- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.min.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.eot
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.svg
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.ttf
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.woff
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-332"></a><span data-ttu-id="b3197-386">3.3.2 부트스트랩 버전</span><span class="sxs-lookup"><span data-stu-id="b3197-386">Bootstrap version 3.3.2</span></span>

- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.min.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.eot
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.svg
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.ttf
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.woff
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-331"></a><span data-ttu-id="b3197-387">3.3.1 부트스트랩 버전</span><span class="sxs-lookup"><span data-stu-id="b3197-387">Bootstrap version 3.3.1</span></span>

- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/bootstrap.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/bootstrap.min.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.eot
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.svg
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.ttf
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-330"></a><span data-ttu-id="b3197-388">부트스트랩 버전 3.3.0</span><span class="sxs-lookup"><span data-stu-id="b3197-388">Bootstrap version 3.3.0</span></span>

- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/bootstrap.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/bootstrap.min.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.eot
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.svg
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.ttf
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-320"></a><span data-ttu-id="b3197-389">부트스트랩 버전 3.2.0</span><span class="sxs-lookup"><span data-stu-id="b3197-389">Bootstrap version 3.2.0</span></span>

- http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.eot
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.svg
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.ttf
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-311"></a><span data-ttu-id="b3197-390">3.1.1 부트스트랩 버전</span><span class="sxs-lookup"><span data-stu-id="b3197-390">Bootstrap version 3.1.1</span></span>

- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/bootstrap.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/bootstrap.min.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.eot
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.svg
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.ttf
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-310"></a><span data-ttu-id="b3197-391">부트스트랩 버전 3.1.0</span><span class="sxs-lookup"><span data-stu-id="b3197-391">Bootstrap version 3.1.0</span></span>

- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/bootstrap.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/bootstrap.min.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.eot
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.svg
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.ttf
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-303"></a><span data-ttu-id="b3197-392">부트스트랩 버전 3.0.3</span><span class="sxs-lookup"><span data-stu-id="b3197-392">Bootstrap version 3.0.3</span></span>

- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/bootstrap.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/bootstrap.min.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap-theme.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap-theme.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.eot
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.svg
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.ttf
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-302"></a><span data-ttu-id="b3197-393">부트스트랩 버전 3.0.2</span><span class="sxs-lookup"><span data-stu-id="b3197-393">Bootstrap version 3.0.2</span></span>

- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/bootstrap.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/bootstrap.min.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap-theme.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap-theme.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.eot
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.svg
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.ttf
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-301"></a><span data-ttu-id="b3197-394">부트스트랩 버전 3.0.1</span><span class="sxs-lookup"><span data-stu-id="b3197-394">Bootstrap version 3.0.1</span></span>

- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/bootstrap.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/bootstrap.min.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap-theme.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap-theme.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.eot
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.svg
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.ttf
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-300"></a><span data-ttu-id="b3197-395">부트스트랩 버전 3.0.0</span><span class="sxs-lookup"><span data-stu-id="b3197-395">Bootstrap version 3.0.0</span></span>

- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/bootstrap.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/bootstrap.min.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap-theme.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap-theme.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.eot
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.svg
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.ttf
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-232"></a><span data-ttu-id="b3197-396">부트스트랩 버전 2.3.2</span><span class="sxs-lookup"><span data-stu-id="b3197-396">Bootstrap version 2.3.2</span></span>

- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.min.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings.png
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings-white.png

#### <a name="bootstrap-version-231"></a><span data-ttu-id="b3197-397">부트스트랩 버전 2.3.1</span><span class="sxs-lookup"><span data-stu-id="b3197-397">Bootstrap version 2.3.1</span></span>

- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.min.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings.png
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings-white.png

<a id="BootstrapTouchCarousel_Releases_on_the_CDN_18"></a>

### <a name="bootstrap-touchcarousel-releases-on-the-cdn"></a><span data-ttu-id="b3197-398">CDN에서 부트스트랩 TouchCarousel 릴리스</span><span class="sxs-lookup"><span data-stu-id="b3197-398">Bootstrap TouchCarousel Releases on the CDN</span></span>

<span data-ttu-id="b3197-399">다음 릴리스의 [ https://github.com/ixisio/bootstrap-touch-carousel ] (https://github.com/ixisio/bootstrap-touch-carousel " https://github.com/ixisio/bootstrap-touch-carousel ") 부트스트랩 TouchCarousel 릴리스 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-399">The following releases of [https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel") Bootstrap TouchCarousel releases are hosted on the CDN:</span></span>

#### <a name="bootstrap-touchcarousel-version-080"></a><span data-ttu-id="b3197-400">부트스트랩 TouchCarousel 버전 0.8.0</span><span class="sxs-lookup"><span data-stu-id="b3197-400">Bootstrap TouchCarousel version 0.8.0</span></span>

- http://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/css/bootstrap-touch-carousel.css
- http://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/js/bootstrap-touch-carousel.js

<a id="Hammerjs_Releases_on_the_CDN_19"></a>

### <a name="hammerjs-releases-on-the-cdn"></a><span data-ttu-id="b3197-401">CDN에서 Hammer.js 릴리스</span><span class="sxs-lookup"><span data-stu-id="b3197-401">Hammer.js Releases on the CDN</span></span>

<span data-ttu-id="b3197-402">다음 버전의 [ http://hammerjs.github.io/ ] (http://hammerjs.github.io/ " http://hammerjs.github.io/ ") Hammer.js 릴리스 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-402">The following releases of [http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/") Hammer.js releases are hosted on the CDN:</span></span>

#### <a name="hammerjs-version-204"></a><span data-ttu-id="b3197-403">2.0.4 Hammer.js 버전</span><span class="sxs-lookup"><span data-stu-id="b3197-403">Hammer.js version 2.0.4</span></span>

- http://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.js
- http://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.js
- http://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.map

<a id="ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15"></a>

### <a name="aspnet-web-forms-and-ajax-releases-on-the-cdn"></a><span data-ttu-id="b3197-404">ASP.NET Web Forms 및 CDN에서 Ajax 릴리스</span><span class="sxs-lookup"><span data-stu-id="b3197-404">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>

<span data-ttu-id="b3197-405">ASP.NET Ajax 라이브러리의 다음 릴리스에서 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-405">The following releases of the ASP.NET Ajax Library are hosted on the CDN.</span></span> <span data-ttu-id="b3197-406">파일의 실제 목록을 확인 하려면 각 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-406">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="b3197-407">ASP.NET Web Forms 및 Ajax 버전 4.5.2</span><span class="sxs-lookup"><span data-stu-id="b3197-407">ASP.NET Web Forms and Ajax version 4.5.2</span></span>](cdnajax452.md "ASP.NET Web Forms 및 Ajax 4.5.2")
- [<span data-ttu-id="b3197-408">ASP.NET Web Forms 및 Ajax 버전 4</span><span class="sxs-lookup"><span data-stu-id="b3197-408">ASP.NET Web Forms and Ajax version 4</span></span>](cdnajax4.md "ASP.NET Web Forms 및 Ajax 4")
- [<span data-ttu-id="b3197-409">ASP.NET Ajax 버전 3.5</span><span class="sxs-lookup"><span data-stu-id="b3197-409">ASP.NET Ajax version 3.5</span></span>](cdnajax35.md "ASP.NET Ajax 3.5")

<a id="ASPNET_MVC_Releases_on_the_CDN_16"></a>

### <a name="aspnet-mvc-releases-on-the-cdn"></a><span data-ttu-id="b3197-410">CDN에 ASP.NET MVC 릴리스</span><span class="sxs-lookup"><span data-stu-id="b3197-410">ASP.NET MVC Releases on the CDN</span></span>

<span data-ttu-id="b3197-411">다음 ASP.NET MVC JavaScript 파일이이 CDN에서 호스트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-411">The following ASP.NET MVC JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-mvc-523"></a><span data-ttu-id="b3197-412">ASP.NET MVC 5.2.3</span><span class="sxs-lookup"><span data-stu-id="b3197-412">ASP.NET MVC 5.2.3</span></span>

- http://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.js
- http://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-51"></a><span data-ttu-id="b3197-413">ASP.NET MVC 5.1</span><span class="sxs-lookup"><span data-stu-id="b3197-413">ASP.NET MVC 5.1</span></span>

- http://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.js
- http://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-50"></a><span data-ttu-id="b3197-414">ASP.NET MVC 5.0</span><span class="sxs-lookup"><span data-stu-id="b3197-414">ASP.NET MVC 5.0</span></span>

- http://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.js
- http://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-40"></a><span data-ttu-id="b3197-415">ASP.NET MVC 4.0</span><span class="sxs-lookup"><span data-stu-id="b3197-415">ASP.NET MVC 4.0</span></span>

- http://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.js
- http://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-30"></a><span data-ttu-id="b3197-416">ASP.NET MVC 3.0</span><span class="sxs-lookup"><span data-stu-id="b3197-416">ASP.NET MVC 3.0</span></span>

- http://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.js
- http://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.min.js
- http://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.js
- http://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.min.js
- http://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.js
- http://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-20"></a><span data-ttu-id="b3197-417">ASP.NET MVC 2.0</span><span class="sxs-lookup"><span data-stu-id="b3197-417">ASP.NET MVC 2.0</span></span>

- http://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.js
- http://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-10"></a><span data-ttu-id="b3197-418">ASP.NET MVC 1.0</span><span class="sxs-lookup"><span data-stu-id="b3197-418">ASP.NET MVC 1.0</span></span>

- http://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.js
- http://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.debug.js

<a id="ASPNET_SignalR_Releases_on_the_CDN_17"></a>

### <a name="aspnet-signalr-releases-on-the-cdn"></a><span data-ttu-id="b3197-419">CDN에서 ASP.NET SignalR 해제</span><span class="sxs-lookup"><span data-stu-id="b3197-419">ASP.NET SignalR Releases on the CDN</span></span>

<span data-ttu-id="b3197-420">다음 ASP.NET SignalR JavaScript 파일이이 CDN에서 호스트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-420">The following ASP.NET SignalR JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-signalr-222"></a><span data-ttu-id="b3197-421">ASP.NET SignalR 2.2.2</span><span class="sxs-lookup"><span data-stu-id="b3197-421">ASP.NET SignalR 2.2.2</span></span>

- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.min.js
- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.js

#### <a name="aspnet-signalr-221"></a><span data-ttu-id="b3197-422">ASP.NET SignalR 2.2.1</span><span class="sxs-lookup"><span data-stu-id="b3197-422">ASP.NET SignalR 2.2.1</span></span>

- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.min.js
- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.js

#### <a name="aspnet-signalr-220"></a><span data-ttu-id="b3197-423">ASP.NET SignalR 2.2.0</span><span class="sxs-lookup"><span data-stu-id="b3197-423">ASP.NET SignalR 2.2.0</span></span>

- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.min.js
- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.js

#### <a name="aspnet-signalr-210"></a><span data-ttu-id="b3197-424">ASP.NET SignalR 2.1.0</span><span class="sxs-lookup"><span data-stu-id="b3197-424">ASP.NET SignalR 2.1.0</span></span>

- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.min.js
- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.js

#### <a name="aspnet-signalr-203"></a><span data-ttu-id="b3197-425">ASP.NET SignalR 2.0.3</span><span class="sxs-lookup"><span data-stu-id="b3197-425">ASP.NET SignalR 2.0.3</span></span>

- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.min.js
- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.js

#### <a name="aspnet-signalr-202"></a><span data-ttu-id="b3197-426">ASP.NET SignalR 2.0.2</span><span class="sxs-lookup"><span data-stu-id="b3197-426">ASP.NET SignalR 2.0.2</span></span>

- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.min.js
- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.js

#### <a name="aspnet-signalr-201"></a><span data-ttu-id="b3197-427">ASP.NET SignalR 2.0.1</span><span class="sxs-lookup"><span data-stu-id="b3197-427">ASP.NET SignalR 2.0.1</span></span>

- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.min.js
- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.js

#### <a name="aspnet-signalr-200"></a><span data-ttu-id="b3197-428">ASP.NET SignalR 2.0.0</span><span class="sxs-lookup"><span data-stu-id="b3197-428">ASP.NET SignalR 2.0.0</span></span>

- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.min.js
- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.js

#### <a name="aspnet-signalr-113"></a><span data-ttu-id="b3197-429">ASP.NET SignalR 1.1.3</span><span class="sxs-lookup"><span data-stu-id="b3197-429">ASP.NET SignalR 1.1.3</span></span>

- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.min.js
- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.js

#### <a name="aspnet-signalr-112"></a><span data-ttu-id="b3197-430">ASP.NET SignalR 1.1.2</span><span class="sxs-lookup"><span data-stu-id="b3197-430">ASP.NET SignalR 1.1.2</span></span>

- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.min.js
- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.js

#### <a name="aspnet-signalr-111"></a><span data-ttu-id="b3197-431">ASP.NET SignalR 1.1.1</span><span class="sxs-lookup"><span data-stu-id="b3197-431">ASP.NET SignalR 1.1.1</span></span>

- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.min.js
- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.js

#### <a name="aspnet-signalr-110"></a><span data-ttu-id="b3197-432">ASP.NET SignalR 1.1.0</span><span class="sxs-lookup"><span data-stu-id="b3197-432">ASP.NET SignalR 1.1.0</span></span>

- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.min.js
- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.js

#### <a name="aspnet-signalr-101"></a><span data-ttu-id="b3197-433">ASP.NET SignalR 1.0.1</span><span class="sxs-lookup"><span data-stu-id="b3197-433">ASP.NET SignalR 1.0.1</span></span>

- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.min.js
- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.js

<span data-ttu-id="b3197-434">CDN에 대 한 사용 조건에 대 한 정보를 참조 하십시오. [Microsoft Ajax CDN 사용 약관](https://www.asp.net/terms-of-use "Microsoft Ajax CDN 사용 약관")합니다.</span><span class="sxs-lookup"><span data-stu-id="b3197-434">For information about the terms of use for the CDN, see [Microsoft Ajax CDN Terms of Use](https://www.asp.net/terms-of-use "Microsoft Ajax CDN Terms of Use").</span></span>
