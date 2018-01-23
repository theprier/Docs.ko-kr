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
ms.openlocfilehash: f69f707ba64d13fc372b7bc44718c9dcf8cec6e2
ms.sourcegitcommit: 3f491f887074310fc0f145cd01a670aa63b969e3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/22/2018
---
<a name="microsoft-ajax-content-delivery-network"></a><span data-ttu-id="d7064-102">Microsoft Ajax 콘텐츠 배달 네트워크</span><span class="sxs-lookup"><span data-stu-id="d7064-102">Microsoft Ajax Content Delivery Network</span></span>
====================
<span data-ttu-id="d7064-103">참고: Microsoft Ajax CDN에 Azure CDN을 사용 하 여 보다 많은 SLA는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-103">Note: The Microsoft Ajax CDN has no SLA above and beyond using an Azure CDN.</span></span>

## <a name="table-of-contents"></a><span data-ttu-id="d7064-104">목차</span><span class="sxs-lookup"><span data-stu-id="d7064-104">Table of Contents</span></span>

<span data-ttu-id="d7064-105">**[ajax.microsoft.com ajax.aspnetcdn.com로 변경](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span><span class="sxs-lookup"><span data-stu-id="d7064-105">**[ajax.microsoft.com renamed to ajax.aspnetcdn.com](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span></span>  
<span data-ttu-id="d7064-106">**[Visual Studio.vsdoc 지원](#Visual_Studio_vsdoc_Support_19)**</span><span class="sxs-lookup"><span data-stu-id="d7064-106">**[Visual Studio .vsdoc Support](#Visual_Studio_vsdoc_Support_19)**</span></span>  
<span data-ttu-id="d7064-107">**[ASP.NET Ajax CDN에서 사용 하 여](#Using_ASPNET_Ajax_from_the_CDN_20)**</span><span class="sxs-lookup"><span data-stu-id="d7064-107">**[Using ASP.NET Ajax from the CDN](#Using_ASPNET_Ajax_from_the_CDN_20)**</span></span>  
<span data-ttu-id="d7064-108">**[CDN에서 jQuery를 사용 하 여](#Using_jQuery_from_the_CDN_21)**</span><span class="sxs-lookup"><span data-stu-id="d7064-108">**[Using jQuery from the CDN](#Using_jQuery_from_the_CDN_21)**</span></span>  
<span data-ttu-id="d7064-109">**[JQuery UI에서 CDN 사용 하 여](#Using_jQuery_UI_from_the_CDN_22)**</span><span class="sxs-lookup"><span data-stu-id="d7064-109">**[Using jQuery UI from the CDN](#Using_jQuery_UI_from_the_CDN_22)**</span></span>  
<span data-ttu-id="d7064-110">**[CDN에서 제 3 자 파일](#Third-Party_Files_on_the_CDN_23)**</span><span class="sxs-lookup"><span data-stu-id="d7064-110">**[Third-Party Files on the CDN](#Third-Party_Files_on_the_CDN_23)**</span></span>  
  
 [<span data-ttu-id="d7064-111">CDN에서 jQuery 릴리스</span><span class="sxs-lookup"><span data-stu-id="d7064-111">jQuery Releases on the CDN</span></span>](#jQuery_Releases_on_the_CDN_0)  
 [<span data-ttu-id="d7064-112">CDN에서 jQuery 마이그레이션할 릴리스</span><span class="sxs-lookup"><span data-stu-id="d7064-112">jQuery Migrate Releases on the CDN</span></span>](#jQuery_Migrate_Releases_on_the_CDN_1)  
 [<span data-ttu-id="d7064-113">jQuery UI CDN에 있는 릴리스</span><span class="sxs-lookup"><span data-stu-id="d7064-113">jQuery UI Releases on the CDN</span></span>](#jQuery_UI_Releases_on_the_CDN_2)  
 [<span data-ttu-id="d7064-114">jQuery 유효성 검사는 CDN에 있는 릴리스</span><span class="sxs-lookup"><span data-stu-id="d7064-114">jQuery Validation Releases on the CDN</span></span>](#jQuery_Validation_Releases_on_the_CDN_3)  
 [<span data-ttu-id="d7064-115">jQuery Mobile CDN에 있는 릴리스</span><span class="sxs-lookup"><span data-stu-id="d7064-115">jQuery Mobile Releases on the CDN</span></span>](#jQuery_Mobile_Releases_on_the_CDN_4)  
 [<span data-ttu-id="d7064-116">jQuery CDN에서 템플릿 릴리스</span><span class="sxs-lookup"><span data-stu-id="d7064-116">jQuery Templates Releases on the CDN</span></span>](#jQuery_Templates_Releases_on_the_CDN_5)  
 [<span data-ttu-id="d7064-117">jQuery CDN에서 주기 릴리스</span><span class="sxs-lookup"><span data-stu-id="d7064-117">jQuery Cycle Releases on the CDN</span></span>](#jQuery_Cycle_Releases_on_the_CDN_6)  
 [<span data-ttu-id="d7064-118">jQuery CDN에서 DataTables 릴리스</span><span class="sxs-lookup"><span data-stu-id="d7064-118">jQuery DataTables Releases on the CDN</span></span>](#jQuery_DataTables_Releases_on_the_CDN_7)  
 [<span data-ttu-id="d7064-119">CDN에서 Modernizr 릴리스</span><span class="sxs-lookup"><span data-stu-id="d7064-119">Modernizr Releases on the CDN</span></span>](#Modernizr_Releases_on_the_CDN_8)  
 [<span data-ttu-id="d7064-120">CDN에서 JSHint 릴리스</span><span class="sxs-lookup"><span data-stu-id="d7064-120">JSHint Releases on the CDN</span></span>](#JSHint_Releases_on_the_CDN_10)  
 [<span data-ttu-id="d7064-121">CDN에서 knockout 릴리스</span><span class="sxs-lookup"><span data-stu-id="d7064-121">Knockout Releases on the CDN</span></span>](#Knockout_Releases_on_the_CDN_11)  
 [<span data-ttu-id="d7064-122">CDN에서 릴리스 전역화</span><span class="sxs-lookup"><span data-stu-id="d7064-122">Globalize Releases on the CDN</span></span>](#Globalize_Releases_on_the_CDN_12)  
 [<span data-ttu-id="d7064-123">CDN에서 릴리스 응답</span><span class="sxs-lookup"><span data-stu-id="d7064-123">Respond Releases on the CDN</span></span>](#Respond_Releases_on_the_CDN_13)  
 [<span data-ttu-id="d7064-124">CDN에서 부트스트랩 릴리스</span><span class="sxs-lookup"><span data-stu-id="d7064-124">Bootstrap Releases on the CDN</span></span>](#Bootstrap_Releases_on_the_CDN_14)  
 [<span data-ttu-id="d7064-125">CDN에서 부트스트랩 TouchCarousel 릴리스</span><span class="sxs-lookup"><span data-stu-id="d7064-125">Bootstrap TouchCarousel Releases on the CDN</span></span>](#BootstrapTouchCarousel_Releases_on_the_CDN_18)  
 [<span data-ttu-id="d7064-126">CDN에서 Hammer.js 릴리스</span><span class="sxs-lookup"><span data-stu-id="d7064-126">Hammer.js Releases on the CDN</span></span>](#Hammerjs_Releases_on_the_CDN_19)  
 [<span data-ttu-id="d7064-127">ASP.NET Web Forms 및 CDN에서 Ajax 릴리스</span><span class="sxs-lookup"><span data-stu-id="d7064-127">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>](#ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15)  
 [<span data-ttu-id="d7064-128">CDN에 ASP.NET MVC 릴리스</span><span class="sxs-lookup"><span data-stu-id="d7064-128">ASP.NET MVC Releases on the CDN</span></span>](#ASPNET_MVC_Releases_on_the_CDN_16)  
 [<span data-ttu-id="d7064-129">CDN에서 ASP.NET SignalR 해제</span><span class="sxs-lookup"><span data-stu-id="d7064-129">ASP.NET SignalR Releases on the CDN</span></span>](#ASPNET_SignalR_Releases_on_the_CDN_17)

<span data-ttu-id="d7064-130">Microsoft Ajax 콘텐츠 배달 네트워크 (CDN) jQuery와 같은 인기 있는 제 3 자 JavaScript 라이브러리를 호스팅하고 웹 응용 프로그램에를 쉽게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-130">The Microsoft Ajax Content Delivery Network (CDN) hosts popular third party JavaScript libraries such as jQuery and enables you to easily add them to your Web applications.</span></span> <span data-ttu-id="d7064-131">이 CDN에서 호스팅되는 jQuery를 사용 하 여 추가 하 여 시작할 수는 예를 들어 한 &lt;스크립트&gt; ajax.aspnetcdn.com 가리키는 페이지에는 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-131">For example, you can start using jQuery which is hosted on this CDN simply by adding a &lt;script&gt; tag to your page that points to ajax.aspnetcdn.com.</span></span>

<span data-ttu-id="d7064-132">CDN 활용 하기 위해, Ajax 응용 프로그램의 성능을 크게 향상 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-132">By taking advantage of the CDN, you can significantly improve the performance of your Ajax applications.</span></span> <span data-ttu-id="d7064-133">CDN의 콘텐츠는 세계에 있는 서버에 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-133">The contents of the CDN are cached on servers located around the world.</span></span> <span data-ttu-id="d7064-134">또한 CDN에는 브라우저 서로 다른 도메인에 있는 웹 사이트에 대 한 캐시 된 제 3 자 JavaScript 파일을 다시 사용할 수 있도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-134">In addition, the CDN enables browsers to reuse cached third party JavaScript files for web sites that are located in different domains.</span></span>

<span data-ttu-id="d7064-135">CDN은 Secure Sockets Layer를 사용 하 여 웹 페이지를 처리 해야 하는 경우 SSL (HTTPS)을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-135">The CDN supports SSL (HTTPS) in case you need to serve a web page using the Secure Sockets Layer.</span></span>

<span data-ttu-id="d7064-136">CDN 업로드 된 및 해당 라이브러리의 소유자가 사용자에 게 사용이 허가 하는 다음 제 3 자 스크립트 라이브러리를 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-136">The CDN hosts the following third party script libraries which have been uploaded, and are licensed to you, by the owners of those libraries:</span></span>

- <span data-ttu-id="d7064-137">jQuery (www.jquery.com)</span><span class="sxs-lookup"><span data-stu-id="d7064-137">jQuery (www.jquery.com)</span></span>
- <span data-ttu-id="d7064-138">jQuery UI (www.jqueryui.com)</span><span class="sxs-lookup"><span data-stu-id="d7064-138">jQuery UI (www.jqueryui.com)</span></span>
- <span data-ttu-id="d7064-139">jQuery Mobile (www.jquerymobile.com)</span><span class="sxs-lookup"><span data-stu-id="d7064-139">jQuery Mobile (www.jquerymobile.com)</span></span>
- <span data-ttu-id="d7064-140">jQuery 유효성 검사 (www.jquery.com)</span><span class="sxs-lookup"><span data-stu-id="d7064-140">jQuery Validation (www.jquery.com)</span></span>
- <span data-ttu-id="d7064-141">jQuery 주기 (www.malsup.com/jquery/cycle/)</span><span class="sxs-lookup"><span data-stu-id="d7064-141">jQuery Cycle (www.malsup.com/jquery/cycle/)</span></span>
- <span data-ttu-id="d7064-142">jQuery Datatable (http://datatables.net/)</span><span class="sxs-lookup"><span data-stu-id="d7064-142">jQuery DataTables (http://datatables.net/)</span></span>

<span data-ttu-id="d7064-143">Microsoft Ajax CDN는 Microsoft에서 업로드 한 다음 라이브러리를도 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-143">The Microsoft Ajax CDN also includes the following libraries which have been uploaded by Microsoft:</span></span>

- <span data-ttu-id="d7064-144">ASP.NET Ajax</span><span class="sxs-lookup"><span data-stu-id="d7064-144">ASP.NET Ajax</span></span>
- <span data-ttu-id="d7064-145">ASP.NET MVC JavaScript 파일</span><span class="sxs-lookup"><span data-stu-id="d7064-145">ASP.NET MVC JavaScript Files</span></span>
- <span data-ttu-id="d7064-146">ASP.NET SignalR JavaScript 파일</span><span class="sxs-lookup"><span data-stu-id="d7064-146">ASP.NET SignalR JavaScript Files</span></span>

<span data-ttu-id="d7064-147">Microsoft는이 CDN에서 호스팅되는 모든 타사 라이브러리의 소유권을 주장 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-147">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="d7064-148">저작권 소유자는 라이브러리에 이러한 라이브러리를 라이선스 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-148">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="d7064-149">해당 저작권 소유자가 단독으로 다운로드 하 고 이러한 라이브러리를 사용 해야 할 수 있는 모든 권한이 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-149">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="d7064-150">이들은 Microsoft 라이브러리 Microsoft 지적 재산권 권한 라이선스 (묵시적된 특허 권한이 없음 포함) 없음이나 보증을이 CDN에서 호스트 되는 타사 라이브러리에 대 한 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-150">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<span data-ttu-id="d7064-151">JavaScript 라이브러리를 제출 하려면 고 라이브러리에는 위쪽 (http://trends.builtwith.com에 나열) 하는 대로 JavaScript 라이브러리 또는 확장/플러그 인은 이들 라이브러리 중 하나 (a) 인기 있는; 또는 (b)에 대 한 유용한 ASP.NET에서 사용 하 여 다음 문의 AjaxCDNSubmission@Microsoft.com합니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-151">If you wish to submit your JavaScript library and your library is one of the top JavaScript libraries (as listed on http://trends.builtwith.com) or extensions/plugins to these libraries that are (a) popular; or (b) helpful for use on ASP.NET then please contact AjaxCDNSubmission@Microsoft.com.</span></span>

<a id="ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18"></a>

## <a name="ajaxmicrosoftcom-renamed-to-ajaxaspnetcdncom"></a><span data-ttu-id="d7064-152">ajax.microsoft.com ajax.aspnetcdn.com로 변경</span><span class="sxs-lookup"><span data-stu-id="d7064-152">ajax.microsoft.com renamed to ajax.aspnetcdn.com</span></span>

<span data-ttu-id="d7064-153">CDN은 microsoft.com 도메인 이름을 사용 하는 데 사용 하 고 aspnetcdn.com 도메인 이름을 사용 하도록 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-153">The CDN used to use the microsoft.com domain name and has been changed to use the aspnetcdn.com domain name.</span></span> <span data-ttu-id="d7064-154">각 요청과 함께 네트워크를 통해 모든 쿠키를 보내야 해당 도메인에서 했기 브라우저 microsoft.com 도메인을 참조 하기 때문에 성능을 향상 시키기 위해이 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-154">This change was made to increase performance because when a browser referenced the microsoft.com domain it would send any cookies from that domain across the wire with each request.</span></span> <span data-ttu-id="d7064-155">Microsoft.com 이외의 도메인 이름으로 바꾸어 25%로 많은 성능으로 증가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-155">By renaming to a domain name other than microsoft.com performance can be increased by as much to 25%.</span></span> <span data-ttu-id="d7064-156">참고 ajax.microsoft.com은 계속 작동 하지만 ajax.aspnetcdn.com를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-156">Note ajax.microsoft.com will continue to function but ajax.aspnetcdn.com is recommended.</span></span>

- <span data-ttu-id="d7064-157">이전 형식: http://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="d7064-157">Old Format: http://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span></span>
- <span data-ttu-id="d7064-158">새 형식: http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="d7064-158">New Format: http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span></span>

<a id="Visual_Studio_vsdoc_Support_19"></a>

## <a name="visual-studio-vsdoc-support"></a><span data-ttu-id="d7064-159">Visual Studio.vsdoc 지원</span><span class="sxs-lookup"><span data-stu-id="d7064-159">Visual Studio .vsdoc Support</span></span>

<span data-ttu-id="d7064-160">Visual Studio 2008 및 2008 s p 1이 있는지 확인 해야 할.vsdoc 파일을 제대로 사용 하려면 설치 하 고 vsdoc 파일에 대 한 핫픽스를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-160">To use the .vsdoc files properly with Visual Studio 2008 you need to make sure that you have VS 2008 SP1 installed and the hotfix for vsdoc files installed.</span></span> <span data-ttu-id="d7064-161">여기에서 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-161">You can get these from here:</span></span>

- [<span data-ttu-id="d7064-162">Visual Studio 2008 s p 1을 다운로드</span><span class="sxs-lookup"><span data-stu-id="d7064-162">Download Visual Studio 2008 SP1</span></span>](https://www.microsoft.com/downloads/en/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en "Visual Studio 2008 s p 1을 다운로드 합니다.")
- [<span data-ttu-id="d7064-163">Visual Studio 2008 s p 1에 대 한.vsdoc 핫픽스 다운로드</span><span class="sxs-lookup"><span data-stu-id="d7064-163">Download .vsdoc hotfix for Visual Studio 2008 SP1</span></span>](https://code.msdn.microsoft.com/KB958502/Release/ProjectReleases.aspx?ReleaseId=1736 "Visual Studio 2008 s p 1에 대 한.vsdoc 핫픽스 다운로드")

<span data-ttu-id="d7064-164">Visual Studio 2010 추가 패치 없이.vsdoc 파일을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-164">Visual Studio 2010 supports .vsdoc files without any additional patches.</span></span>

<a id="Using_ASPNET_Ajax_from_the_CDN_20"></a>

## <a name="using-aspnet-ajax-from-the-cdn"></a><span data-ttu-id="d7064-165">ASP.NET Ajax CDN에서 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="d7064-165">Using ASP.NET Ajax from the CDN</span></span>

<span data-ttu-id="d7064-166">ASP.NET 4를 사용 하는 경우 cdn ASP.NET framework 스크립트에 대 한 모든 요청을 리디렉션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-166">When using ASP.NET 4, you can redirect all requests for ASP.NET framework scripts to the CDN.</span></span> <span data-ttu-id="d7064-167">로컬 웹 서버 대신 CDN에서 스크립트 검색 공용 ASP.NET 웹 사이트의 성능을 상당히 개선 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-167">Retrieving scripts from the CDN instead of your local web server can substantially improve the performance of public ASP.NET websites.</span></span>

<span data-ttu-id="d7064-168">ScriptManager EnableCDN 속성을 사용 하 여 모든 요청을 리디렉션할 ASP.NET 프레임 워크 스크립트 Microsoft Ajax CDN에:</span><span class="sxs-lookup"><span data-stu-id="d7064-168">Use the ScriptManager EnableCDN property to redirect all ASP.NET framework script requests to the Microsoft Ajax CDN:</span></span>

[!code-aspx[Main](overview/samples/sample1.aspx)]

<a id="Using_jQuery_from_the_CDN_21"></a>

## <a name="using-jquery-from-the-cdn"></a><span data-ttu-id="d7064-169">CDN에서 jQuery를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="d7064-169">Using jQuery from the CDN</span></span>

<span data-ttu-id="d7064-170">페이지에는 다음 스크립트 요소를 추가 하 여 CDN에서 웹 응용 프로그램에서 호스팅되는 jQuery 스크립트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-170">You can use jQuery scripts hosted on CDN in your Web application by adding the following script element to a page:</span></span>

[!code-html[Main](overview/samples/sample2.html)]

<span data-ttu-id="d7064-171">CDN에 액세스할 수 있는 jQuery 스크립트의 축소 된 버전도 포함 됩니다는 다음 요소를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="d7064-171">The CDN also includes the minified version of the jQuery script, which you can get using the following element:</span></span>

[!code-html[Main](overview/samples/sample3.html)]

<span data-ttu-id="d7064-172">대체 인증 CDN를 사용할 수 없는 경우 자신의 웹 사이트에 로컬 경로에서 jQuery를 로드 하려면 페이지를 허용 하려면 CDN 참조 요소 바로 뒤 다음 요소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-172">To allow your page to fallback to loading jQuery from a local path on your own website if the CDN happens to be unavailable, add the following element immediately after the element referencing the CDN:</span></span>

[!code-html[Main](overview/samples/sample4.html)]

<span data-ttu-id="d7064-173">다음 샘플 페이지 CDN 버전 (로컬 복사본으로 대체) 사용 하 여 jQuery 라이브러리의를 사용 하 여는 단추를 클릭할 때 div 요소 내용을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-173">The following sample page uses the CDN version of the jQuery library (with fallback to a local copy) to display the contents of a div element when a button is clicked.</span></span>

[!code-html[Main](overview/samples/sample5.html)]

<span data-ttu-id="d7064-174">JQuery에 대 한 자세한 정보 및 방문 하 여 jQuery의 로컬 복사본을 다운로드할 수 있습니다는 [jQuery](http://jquery.com/) 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-174">You can learn more about jQuery and download a local copy of jQuery by visiting the [jQuery](http://jquery.com/) Web site.</span></span>

<a id="Using_jQuery_UI_from_the_CDN_22"></a>

## <a name="using-jquery-ui-from-the-cdn"></a><span data-ttu-id="d7064-175">JQuery UI에서 CDN 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="d7064-175">Using jQuery UI from the CDN</span></span>

<span data-ttu-id="d7064-176">또한 CDN jQuery UI 라이브러리를 호스트합니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-176">The CDN also hosts the jQuery UI library.</span></span> <span data-ttu-id="d7064-177">JQuery UI 라이브러리는 다양 한 위젯 및 ASP.NET 응용 프로그램에서 사용할 수 있는 효과 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-177">The jQuery UI library includes a rich set of widgets and effects that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="d7064-178">예를 들어 다음 페이지는 ASP.NET Web Forms 응용 프로그램의 컨텍스트에서 jQuery UI Datepicker 팝업 달력이 표시를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-178">For example, the following page illustrates how you can use the jQuery UI Datepicker in the context of an ASP.NET Web Forms application to display a pop-up calendar:</span></span>

[!code-aspx[Main](overview/samples/sample6.aspx)]

<span data-ttu-id="d7064-179">키보드를 사용 하 여 텍스트 상자에 포커스를 이동 하면 달력이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-179">When you move focus to the TextBox using your keyboard, a calendar is displayed:</span></span>

![만든 Datepicker 팝업 일정](overview/_static/image1.png)

<span data-ttu-id="d7064-181">위의 코드에서 CDN에서 3 개의 파일을 포함 해야 하는 사항을 참고 하십시오.</span><span class="sxs-lookup"><span data-stu-id="d7064-181">Notice that you must include three files from the CDN in the code above:</span></span>

- <span data-ttu-id="d7064-182">JQuery 라이브러리 &mdash; jQuery UI 라이브러리는 jQuery 라이브러리에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-182">The jQuery library &mdash; The jQuery UI library depends on the jQuery library.</span></span> <span data-ttu-id="d7064-183">JQuery 라이브러리 jQuery UI 라이브러리를 추가 하기 전에 페이지에 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-183">You must add the jQuery library to your page before you add the jQuery UI library.</span></span>
- <span data-ttu-id="d7064-184">JQuery UI 라이브러리 &mdash; jQuery UI 라이브러리 모든 위의 페이지에 사용 된 Datepicker 위젯 같은 위젯 및 jQuery UI 효과 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-184">The jQuery UI library &mdash; The jQuery UI library contains all of the jQuery UI effects and widgets such as the Datepicker widget used in the page above.</span></span>
- <span data-ttu-id="d7064-185">JQuery UI 테마 &mdash; jQuery UI 다양 한 테마를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-185">A jQuery UI theme &mdash; The jQuery UI supports different themes.</span></span> <span data-ttu-id="d7064-186">위의 페이지 Redmond 테마 가져올 CSS 파일에 대 한 링크를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-186">The page above includes a link to a CSS file to import the Redmond theme.</span></span>

<span data-ttu-id="d7064-187">모든 표준 jQuery UI 테마는 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-187">All of the standard jQuery UI themes are hosted on the CDN.</span></span> <span data-ttu-id="d7064-188">[이 페이지를 방문](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 Microsoft Ajax CDN에서") 각 테마에 대 한 축소판 그림을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-188">[Visit this page](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 on the Microsoft Ajax CDN") to view thumbnails for each theme.</span></span>

<span data-ttu-id="d7064-189">JQuery UI 라이브러리에 대 한 자세한 내용은 방문 공식 [jQuery UI 웹 사이트](http://jQueryUI.com "jQuery UI 웹 사이트")합니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-189">To learn more about the jQuery UI library, visit the official [jQuery UI website](http://jQueryUI.com "jQuery UI website").</span></span>

<a id="Third-Party_Files_on_the_CDN_23"></a>

## <a name="third-party-files-on-the-cdn"></a><span data-ttu-id="d7064-190">CDN에서 제 3 자 파일</span><span class="sxs-lookup"><span data-stu-id="d7064-190">Third-Party Files on the CDN</span></span>

<span data-ttu-id="d7064-191">CDN은 가장 일반적인 제 3 자 JavaScript 라이브러리 중 일부를 호스팅합니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-191">The CDN hosts some of the most popular third party JavaScript libraries.</span></span> <span data-ttu-id="d7064-192">Microsoft는이 CDN에서 호스팅되는 모든 타사 라이브러리의 소유권을 주장 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-192">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="d7064-193">저작권 소유자는 라이브러리에 이러한 라이브러리를 라이선스 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-193">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="d7064-194">해당 저작권 소유자가 단독으로 다운로드 하 고 이러한 라이브러리를 사용 해야 할 수 있는 모든 권한이 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-194">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="d7064-195">이들은 Microsoft 라이브러리 Microsoft 지적 재산권 권한 라이선스 (묵시적된 특허 권한이 없음 포함) 없음이나 보증을이 CDN에서 호스트 되는 타사 라이브러리에 대 한 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-195">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<a id="jQuery_Releases_on_the_CDN_0"></a>

### <a name="jquery-releases-on-the-cdn"></a><span data-ttu-id="d7064-196">CDN에서 jQuery 릴리스</span><span class="sxs-lookup"><span data-stu-id="d7064-196">jQuery Releases on the CDN</span></span>

<span data-ttu-id="d7064-197">다음 버전의 jQuery CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-197">The following releases of jQuery are hosted on the CDN:</span></span>

#### <a name="jquery-version-331"></a><span data-ttu-id="d7064-198">3.3.1 jQuery 버전</span><span class="sxs-lookup"><span data-stu-id="d7064-198">jQuery version 3.3.1</span></span>
- <span data-ttu-id="d7064-199">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.js</span><span class="sxs-lookup"><span data-stu-id="d7064-199">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.js</span></span>
- <span data-ttu-id="d7064-200">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-200">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.js</span></span>
- <span data-ttu-id="d7064-201">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.map</span><span class="sxs-lookup"><span data-stu-id="d7064-201">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.map</span></span>
- <span data-ttu-id="d7064-202">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.js</span><span class="sxs-lookup"><span data-stu-id="d7064-202">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.js</span></span>
- <span data-ttu-id="d7064-203">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-203">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.js</span></span>
- <span data-ttu-id="d7064-204">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.map</span><span class="sxs-lookup"><span data-stu-id="d7064-204">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.map</span></span>

#### <a name="jquery-version-321"></a><span data-ttu-id="d7064-205">jQuery 버전 3.2.1</span><span class="sxs-lookup"><span data-stu-id="d7064-205">jQuery version 3.2.1</span></span>
- <span data-ttu-id="d7064-206">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.js</span><span class="sxs-lookup"><span data-stu-id="d7064-206">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.js</span></span>
- <span data-ttu-id="d7064-207">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-207">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.js</span></span>
- <span data-ttu-id="d7064-208">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.map</span><span class="sxs-lookup"><span data-stu-id="d7064-208">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.map</span></span>
- <span data-ttu-id="d7064-209">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.js</span><span class="sxs-lookup"><span data-stu-id="d7064-209">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.js</span></span>
- <span data-ttu-id="d7064-210">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-210">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.js</span></span>
- <span data-ttu-id="d7064-211">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.map</span><span class="sxs-lookup"><span data-stu-id="d7064-211">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.map</span></span>

#### <a name="jquery-version-320"></a><span data-ttu-id="d7064-212">jQuery 버전 3.2.0</span><span class="sxs-lookup"><span data-stu-id="d7064-212">jQuery version 3.2.0</span></span>

- <span data-ttu-id="d7064-213">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.js</span><span class="sxs-lookup"><span data-stu-id="d7064-213">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.js</span></span>
- <span data-ttu-id="d7064-214">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-214">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.js</span></span>
- <span data-ttu-id="d7064-215">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.map</span><span class="sxs-lookup"><span data-stu-id="d7064-215">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.map</span></span>
- <span data-ttu-id="d7064-216">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.js</span><span class="sxs-lookup"><span data-stu-id="d7064-216">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.js</span></span>
- <span data-ttu-id="d7064-217">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-217">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.js</span></span>
- <span data-ttu-id="d7064-218">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.map</span><span class="sxs-lookup"><span data-stu-id="d7064-218">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.map</span></span>

#### <a name="jquery-version-311"></a><span data-ttu-id="d7064-219">3.1.1 jQuery 버전</span><span class="sxs-lookup"><span data-stu-id="d7064-219">jQuery version 3.1.1</span></span>

- <span data-ttu-id="d7064-220">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.js</span><span class="sxs-lookup"><span data-stu-id="d7064-220">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.js</span></span>
- <span data-ttu-id="d7064-221">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-221">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.js</span></span>
- <span data-ttu-id="d7064-222">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.map</span><span class="sxs-lookup"><span data-stu-id="d7064-222">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.map</span></span>
- <span data-ttu-id="d7064-223">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.js</span><span class="sxs-lookup"><span data-stu-id="d7064-223">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.js</span></span>
- <span data-ttu-id="d7064-224">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-224">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.js</span></span>
- <span data-ttu-id="d7064-225">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.map</span><span class="sxs-lookup"><span data-stu-id="d7064-225">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.map</span></span>

#### <a name="jquery-version-310"></a><span data-ttu-id="d7064-226">jQuery 버전 3.1.0</span><span class="sxs-lookup"><span data-stu-id="d7064-226">jQuery version 3.1.0</span></span>

- <span data-ttu-id="d7064-227">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.js</span><span class="sxs-lookup"><span data-stu-id="d7064-227">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.js</span></span>
- <span data-ttu-id="d7064-228">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-228">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.js</span></span>
- <span data-ttu-id="d7064-229">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.map</span><span class="sxs-lookup"><span data-stu-id="d7064-229">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.map</span></span>
- <span data-ttu-id="d7064-230">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.js</span><span class="sxs-lookup"><span data-stu-id="d7064-230">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.js</span></span>
- <span data-ttu-id="d7064-231">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-231">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.js</span></span>
- <span data-ttu-id="d7064-232">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.map</span><span class="sxs-lookup"><span data-stu-id="d7064-232">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.map</span></span>

#### <a name="jquery-version-300"></a><span data-ttu-id="d7064-233">jQuery 버전 3.0.0</span><span class="sxs-lookup"><span data-stu-id="d7064-233">jQuery version 3.0.0</span></span>

- <span data-ttu-id="d7064-234">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.js</span><span class="sxs-lookup"><span data-stu-id="d7064-234">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.js</span></span>
- <span data-ttu-id="d7064-235">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-235">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.js</span></span>
- <span data-ttu-id="d7064-236">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.map</span><span class="sxs-lookup"><span data-stu-id="d7064-236">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.map</span></span>
- <span data-ttu-id="d7064-237">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.js</span><span class="sxs-lookup"><span data-stu-id="d7064-237">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.js</span></span>
- <span data-ttu-id="d7064-238">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-238">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.js</span></span>
- <span data-ttu-id="d7064-239">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.map</span><span class="sxs-lookup"><span data-stu-id="d7064-239">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.map</span></span>

#### <a name="jquery-version-224"></a><span data-ttu-id="d7064-240">jQuery 버전 2.2.4</span><span class="sxs-lookup"><span data-stu-id="d7064-240">jQuery version 2.2.4</span></span>

- <span data-ttu-id="d7064-241">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.js</span><span class="sxs-lookup"><span data-stu-id="d7064-241">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.js</span></span>
- <span data-ttu-id="d7064-242">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-242">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.js</span></span>
- <span data-ttu-id="d7064-243">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.map</span><span class="sxs-lookup"><span data-stu-id="d7064-243">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.map</span></span>

#### <a name="jquery-version-223"></a><span data-ttu-id="d7064-244">jQuery 버전 2.2.3</span><span class="sxs-lookup"><span data-stu-id="d7064-244">jQuery version 2.2.3</span></span>

- <span data-ttu-id="d7064-245">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.js</span><span class="sxs-lookup"><span data-stu-id="d7064-245">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.js</span></span>
- <span data-ttu-id="d7064-246">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-246">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.js</span></span>
- <span data-ttu-id="d7064-247">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.map</span><span class="sxs-lookup"><span data-stu-id="d7064-247">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.map</span></span>

#### <a name="jquery-version-222"></a><span data-ttu-id="d7064-248">jQuery 버전 2.2.2</span><span class="sxs-lookup"><span data-stu-id="d7064-248">jQuery version 2.2.2</span></span>

- <span data-ttu-id="d7064-249">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.js</span><span class="sxs-lookup"><span data-stu-id="d7064-249">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.js</span></span>
- <span data-ttu-id="d7064-250">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-250">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.js</span></span>
- <span data-ttu-id="d7064-251">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.map</span><span class="sxs-lookup"><span data-stu-id="d7064-251">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.map</span></span>

#### <a name="jquery-version-221"></a><span data-ttu-id="d7064-252">jQuery 버전 2.2.1</span><span class="sxs-lookup"><span data-stu-id="d7064-252">jQuery version 2.2.1</span></span>

- <span data-ttu-id="d7064-253">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.js</span><span class="sxs-lookup"><span data-stu-id="d7064-253">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.js</span></span>
- <span data-ttu-id="d7064-254">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-254">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.js</span></span>
- <span data-ttu-id="d7064-255">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.map</span><span class="sxs-lookup"><span data-stu-id="d7064-255">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.map</span></span>

#### <a name="jquery-version-220"></a><span data-ttu-id="d7064-256">jQuery 버전 2.2.0</span><span class="sxs-lookup"><span data-stu-id="d7064-256">jQuery version 2.2.0</span></span>

- <span data-ttu-id="d7064-257">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.js</span><span class="sxs-lookup"><span data-stu-id="d7064-257">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.js</span></span>
- <span data-ttu-id="d7064-258">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-258">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.js</span></span>
- <span data-ttu-id="d7064-259">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.map</span><span class="sxs-lookup"><span data-stu-id="d7064-259">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.map</span></span>

#### <a name="jquery-version-214"></a><span data-ttu-id="d7064-260">jQuery 버전 2.1.4</span><span class="sxs-lookup"><span data-stu-id="d7064-260">jQuery version 2.1.4</span></span>

- <span data-ttu-id="d7064-261">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.js</span><span class="sxs-lookup"><span data-stu-id="d7064-261">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.js</span></span>
- <span data-ttu-id="d7064-262">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-262">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.js</span></span>
- <span data-ttu-id="d7064-263">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.map</span><span class="sxs-lookup"><span data-stu-id="d7064-263">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.map</span></span>

#### <a name="jquery-version-213"></a><span data-ttu-id="d7064-264">jQuery 버전 2.1.3</span><span class="sxs-lookup"><span data-stu-id="d7064-264">jQuery version 2.1.3</span></span>

- <span data-ttu-id="d7064-265">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.js</span><span class="sxs-lookup"><span data-stu-id="d7064-265">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.js</span></span>
- <span data-ttu-id="d7064-266">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-266">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.js</span></span>
- <span data-ttu-id="d7064-267">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.map</span><span class="sxs-lookup"><span data-stu-id="d7064-267">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.map</span></span>

#### <a name="jquery-version-212"></a><span data-ttu-id="d7064-268">jQuery 버전 2.1.2</span><span class="sxs-lookup"><span data-stu-id="d7064-268">jQuery version 2.1.2</span></span>

- <span data-ttu-id="d7064-269">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.js</span><span class="sxs-lookup"><span data-stu-id="d7064-269">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.js</span></span>
- <span data-ttu-id="d7064-270">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-270">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.min.js</span></span>

#### <a name="jquery-version-211"></a><span data-ttu-id="d7064-271">jQuery 버전 2.1.1</span><span class="sxs-lookup"><span data-stu-id="d7064-271">jQuery version 2.1.1</span></span>

- <span data-ttu-id="d7064-272">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.js</span><span class="sxs-lookup"><span data-stu-id="d7064-272">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.js</span></span>
- <span data-ttu-id="d7064-273">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-273">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js</span></span>
- <span data-ttu-id="d7064-274">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.map</span><span class="sxs-lookup"><span data-stu-id="d7064-274">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.map</span></span>

#### <a name="jquery-version-210"></a><span data-ttu-id="d7064-275">jQuery 버전 2.1.0</span><span class="sxs-lookup"><span data-stu-id="d7064-275">jQuery version 2.1.0</span></span>

- <span data-ttu-id="d7064-276">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.js</span><span class="sxs-lookup"><span data-stu-id="d7064-276">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.js</span></span>
- <span data-ttu-id="d7064-277">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-277">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.js</span></span>
- <span data-ttu-id="d7064-278">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="d7064-278">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0-vsdoc.js</span></span>
- <span data-ttu-id="d7064-279">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.map</span><span class="sxs-lookup"><span data-stu-id="d7064-279">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.map</span></span>

#### <a name="jquery-version-203"></a><span data-ttu-id="d7064-280">jQuery 버전 2.0.3</span><span class="sxs-lookup"><span data-stu-id="d7064-280">jQuery version 2.0.3</span></span>

- <span data-ttu-id="d7064-281">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.js</span><span class="sxs-lookup"><span data-stu-id="d7064-281">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.js</span></span>
- <span data-ttu-id="d7064-282">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-282">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.js</span></span>
- <span data-ttu-id="d7064-283">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="d7064-283">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3-vsdoc.js</span></span>
- <span data-ttu-id="d7064-284">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.map</span><span class="sxs-lookup"><span data-stu-id="d7064-284">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.map</span></span>

#### <a name="jquery-version-202"></a><span data-ttu-id="d7064-285">jQuery 버전 2.0.2</span><span class="sxs-lookup"><span data-stu-id="d7064-285">jQuery version 2.0.2</span></span>

- <span data-ttu-id="d7064-286">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.js</span><span class="sxs-lookup"><span data-stu-id="d7064-286">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.js</span></span>
- <span data-ttu-id="d7064-287">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-287">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.js</span></span>
- <span data-ttu-id="d7064-288">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="d7064-288">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2-vsdoc.js</span></span>
- <span data-ttu-id="d7064-289">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.map</span><span class="sxs-lookup"><span data-stu-id="d7064-289">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.map</span></span>

#### <a name="jquery-version-201"></a><span data-ttu-id="d7064-290">jQuery 버전 2.0.1</span><span class="sxs-lookup"><span data-stu-id="d7064-290">jQuery version 2.0.1</span></span>

- <span data-ttu-id="d7064-291">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.js</span><span class="sxs-lookup"><span data-stu-id="d7064-291">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.js</span></span>
- <span data-ttu-id="d7064-292">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-292">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.js</span></span>
- <span data-ttu-id="d7064-293">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="d7064-293">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1-vsdoc.js</span></span>
- <span data-ttu-id="d7064-294">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.map</span><span class="sxs-lookup"><span data-stu-id="d7064-294">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.map</span></span>

#### <a name="jquery-version-200"></a><span data-ttu-id="d7064-295">jQuery 버전 2.0.0</span><span class="sxs-lookup"><span data-stu-id="d7064-295">jQuery version 2.0.0</span></span>

- <span data-ttu-id="d7064-296">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.js</span><span class="sxs-lookup"><span data-stu-id="d7064-296">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.js</span></span>
- <span data-ttu-id="d7064-297">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-297">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.js</span></span>
- <span data-ttu-id="d7064-298">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="d7064-298">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0-vsdoc.js</span></span>
- <span data-ttu-id="d7064-299">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.map</span><span class="sxs-lookup"><span data-stu-id="d7064-299">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.map</span></span>

#### <a name="jquery-version-1124"></a><span data-ttu-id="d7064-300">jQuery 버전 1.12.4</span><span class="sxs-lookup"><span data-stu-id="d7064-300">jQuery version 1.12.4</span></span>

- <span data-ttu-id="d7064-301">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.js</span><span class="sxs-lookup"><span data-stu-id="d7064-301">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.js</span></span>
- <span data-ttu-id="d7064-302">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-302">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.js</span></span>
- <span data-ttu-id="d7064-303">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.map</span><span class="sxs-lookup"><span data-stu-id="d7064-303">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.map</span></span>

#### <a name="jquery-version-1123"></a><span data-ttu-id="d7064-304">jQuery 버전 1.12.3</span><span class="sxs-lookup"><span data-stu-id="d7064-304">jQuery version 1.12.3</span></span>

- <span data-ttu-id="d7064-305">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.js</span><span class="sxs-lookup"><span data-stu-id="d7064-305">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.js</span></span>
- <span data-ttu-id="d7064-306">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-306">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.js</span></span>
- <span data-ttu-id="d7064-307">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.map</span><span class="sxs-lookup"><span data-stu-id="d7064-307">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.map</span></span>

#### <a name="jquery-version-1122"></a><span data-ttu-id="d7064-308">jQuery 버전 1.12.2</span><span class="sxs-lookup"><span data-stu-id="d7064-308">jQuery version 1.12.2</span></span>

- <span data-ttu-id="d7064-309">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.js</span><span class="sxs-lookup"><span data-stu-id="d7064-309">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.js</span></span>
- <span data-ttu-id="d7064-310">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-310">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.js</span></span>
- <span data-ttu-id="d7064-311">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.map</span><span class="sxs-lookup"><span data-stu-id="d7064-311">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.map</span></span>

#### <a name="jquery-version-1121"></a><span data-ttu-id="d7064-312">jQuery 버전 1.12.1</span><span class="sxs-lookup"><span data-stu-id="d7064-312">jQuery version 1.12.1</span></span>

- <span data-ttu-id="d7064-313">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.js</span><span class="sxs-lookup"><span data-stu-id="d7064-313">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.js</span></span>
- <span data-ttu-id="d7064-314">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-314">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.js</span></span>
- <span data-ttu-id="d7064-315">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.map</span><span class="sxs-lookup"><span data-stu-id="d7064-315">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.map</span></span>

#### <a name="jquery-version-1120"></a><span data-ttu-id="d7064-316">jQuery 버전 1.12.0</span><span class="sxs-lookup"><span data-stu-id="d7064-316">jQuery version 1.12.0</span></span>

- <span data-ttu-id="d7064-317">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.js</span><span class="sxs-lookup"><span data-stu-id="d7064-317">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.js</span></span>
- <span data-ttu-id="d7064-318">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-318">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.js</span></span>
- <span data-ttu-id="d7064-319">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.map</span><span class="sxs-lookup"><span data-stu-id="d7064-319">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.map</span></span>

#### <a name="jquery-version-1113"></a><span data-ttu-id="d7064-320">jQuery 버전 1.11.3</span><span class="sxs-lookup"><span data-stu-id="d7064-320">jQuery version 1.11.3</span></span>

- <span data-ttu-id="d7064-321">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.js</span><span class="sxs-lookup"><span data-stu-id="d7064-321">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.js</span></span>
- <span data-ttu-id="d7064-322">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-322">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.js</span></span>
- <span data-ttu-id="d7064-323">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.map</span><span class="sxs-lookup"><span data-stu-id="d7064-323">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.map</span></span>

#### <a name="jquery-version-1112"></a><span data-ttu-id="d7064-324">jQuery 버전 1.11.2</span><span class="sxs-lookup"><span data-stu-id="d7064-324">jQuery version 1.11.2</span></span>

- <span data-ttu-id="d7064-325">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.js</span><span class="sxs-lookup"><span data-stu-id="d7064-325">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.js</span></span>
- <span data-ttu-id="d7064-326">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-326">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js</span></span>
- <span data-ttu-id="d7064-327">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.map</span><span class="sxs-lookup"><span data-stu-id="d7064-327">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.map</span></span>

#### <a name="jquery-version-1111"></a><span data-ttu-id="d7064-328">jQuery 버전 1.11.1</span><span class="sxs-lookup"><span data-stu-id="d7064-328">jQuery version 1.11.1</span></span>

- <span data-ttu-id="d7064-329">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.js</span><span class="sxs-lookup"><span data-stu-id="d7064-329">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.js</span></span>
- <span data-ttu-id="d7064-330">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-330">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.js</span></span>
- <span data-ttu-id="d7064-331">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.map</span><span class="sxs-lookup"><span data-stu-id="d7064-331">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.map</span></span>

#### <a name="jquery-version-1110"></a><span data-ttu-id="d7064-332">jQuery 버전 1.11.0</span><span class="sxs-lookup"><span data-stu-id="d7064-332">jQuery version 1.11.0</span></span>

- <span data-ttu-id="d7064-333">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.js</span><span class="sxs-lookup"><span data-stu-id="d7064-333">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.js</span></span>
- <span data-ttu-id="d7064-334">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-334">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.js</span></span>
- <span data-ttu-id="d7064-335">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="d7064-335">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0-vsdoc.js</span></span>
- <span data-ttu-id="d7064-336">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.map</span><span class="sxs-lookup"><span data-stu-id="d7064-336">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.map</span></span>

#### <a name="jquery-version-1102"></a><span data-ttu-id="d7064-337">jQuery 1.10.2 버전</span><span class="sxs-lookup"><span data-stu-id="d7064-337">jQuery version 1.10.2</span></span>

- <span data-ttu-id="d7064-338">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.js</span><span class="sxs-lookup"><span data-stu-id="d7064-338">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.js</span></span>
- <span data-ttu-id="d7064-339">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-339">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.js</span></span>
- <span data-ttu-id="d7064-340">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="d7064-340">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2-vsdoc.js</span></span>
- <span data-ttu-id="d7064-341">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.map</span><span class="sxs-lookup"><span data-stu-id="d7064-341">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.map</span></span>

#### <a name="jquery-version-1101"></a><span data-ttu-id="d7064-342">jQuery 버전 1.10.1</span><span class="sxs-lookup"><span data-stu-id="d7064-342">jQuery version 1.10.1</span></span>

- <span data-ttu-id="d7064-343">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.js</span><span class="sxs-lookup"><span data-stu-id="d7064-343">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.js</span></span>
- <span data-ttu-id="d7064-344">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-344">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.js</span></span>
- <span data-ttu-id="d7064-345">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="d7064-345">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1-vsdoc.js</span></span>
- <span data-ttu-id="d7064-346">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.map</span><span class="sxs-lookup"><span data-stu-id="d7064-346">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.map</span></span>

#### <a name="jquery-version-1100"></a><span data-ttu-id="d7064-347">jQuery 버전 1.10.0</span><span class="sxs-lookup"><span data-stu-id="d7064-347">jQuery version 1.10.0</span></span>

- <span data-ttu-id="d7064-348">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.js</span><span class="sxs-lookup"><span data-stu-id="d7064-348">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.js</span></span>
- <span data-ttu-id="d7064-349">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-349">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.js</span></span>
- <span data-ttu-id="d7064-350">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="d7064-350">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0-vsdoc.js</span></span>
- <span data-ttu-id="d7064-351">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.map</span><span class="sxs-lookup"><span data-stu-id="d7064-351">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.map</span></span>

#### <a name="jquery-version-191"></a><span data-ttu-id="d7064-352">jQuery 버전 1.9.1</span><span class="sxs-lookup"><span data-stu-id="d7064-352">jQuery version 1.9.1</span></span>

- <span data-ttu-id="d7064-353">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.js</span><span class="sxs-lookup"><span data-stu-id="d7064-353">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.js</span></span>
- <span data-ttu-id="d7064-354">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-354">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.js</span></span>
- <span data-ttu-id="d7064-355">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="d7064-355">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1-vsdoc.js</span></span>
- <span data-ttu-id="d7064-356">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.map</span><span class="sxs-lookup"><span data-stu-id="d7064-356">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.map</span></span>

#### <a name="jquery-version-190"></a><span data-ttu-id="d7064-357">1.9.0 jQuery 버전</span><span class="sxs-lookup"><span data-stu-id="d7064-357">jQuery version 1.9.0</span></span>

- <span data-ttu-id="d7064-358">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.js</span><span class="sxs-lookup"><span data-stu-id="d7064-358">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.js</span></span>
- <span data-ttu-id="d7064-359">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-359">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.js</span></span>
- <span data-ttu-id="d7064-360">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="d7064-360">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0-vsdoc.js</span></span>
- <span data-ttu-id="d7064-361">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.map</span><span class="sxs-lookup"><span data-stu-id="d7064-361">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.map</span></span>

#### <a name="jquery-version-183"></a><span data-ttu-id="d7064-362">1.8.3 jQuery 버전</span><span class="sxs-lookup"><span data-stu-id="d7064-362">jQuery version 1.8.3</span></span>

- <span data-ttu-id="d7064-363">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.js</span><span class="sxs-lookup"><span data-stu-id="d7064-363">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.js</span></span>
- <span data-ttu-id="d7064-364">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-364">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.min.js</span></span>
- <span data-ttu-id="d7064-365">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="d7064-365">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3-vsdoc.js</span></span>

#### <a name="jquery-version-182"></a><span data-ttu-id="d7064-366">1.8.2 jQuery 버전</span><span class="sxs-lookup"><span data-stu-id="d7064-366">jQuery version 1.8.2</span></span>

- <span data-ttu-id="d7064-367">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.js</span><span class="sxs-lookup"><span data-stu-id="d7064-367">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.js</span></span>
- <span data-ttu-id="d7064-368">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-368">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.min.js</span></span>
- <span data-ttu-id="d7064-369">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="d7064-369">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2-vsdoc.js</span></span>

#### <a name="jquery-version-181"></a><span data-ttu-id="d7064-370">1.8.1 jQuery 버전</span><span class="sxs-lookup"><span data-stu-id="d7064-370">jQuery version 1.8.1</span></span>

- <span data-ttu-id="d7064-371">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.js</span><span class="sxs-lookup"><span data-stu-id="d7064-371">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.js</span></span>
- <span data-ttu-id="d7064-372">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-372">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.min.js</span></span>
- <span data-ttu-id="d7064-373">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="d7064-373">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1-vsdoc.js</span></span>

#### <a name="jquery-version-180"></a><span data-ttu-id="d7064-374">jQuery 버전 1.8.0</span><span class="sxs-lookup"><span data-stu-id="d7064-374">jQuery version 1.8.0</span></span>

- <span data-ttu-id="d7064-375">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="d7064-375">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span></span>
- <span data-ttu-id="d7064-376">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-376">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.min.js</span></span>
- <span data-ttu-id="d7064-377">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="d7064-377">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0-vsdoc.js</span></span>

#### <a name="jquery-version-172"></a><span data-ttu-id="d7064-378">1.7.2 jQuery 버전</span><span class="sxs-lookup"><span data-stu-id="d7064-378">jQuery version 1.7.2</span></span>

- <span data-ttu-id="d7064-379">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.js</span><span class="sxs-lookup"><span data-stu-id="d7064-379">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.js</span></span>
- <span data-ttu-id="d7064-380">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-380">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js</span></span>

#### <a name="jquery-version-171"></a><span data-ttu-id="d7064-381">jQuery 버전 1.7.1</span><span class="sxs-lookup"><span data-stu-id="d7064-381">jQuery version 1.7.1</span></span>

- <span data-ttu-id="d7064-382">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.js</span><span class="sxs-lookup"><span data-stu-id="d7064-382">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.js</span></span>
- <span data-ttu-id="d7064-383">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-383">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.min.js</span></span>
- <span data-ttu-id="d7064-384">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="d7064-384">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1-vsdoc.js</span></span>

#### <a name="jquery-version-17"></a><span data-ttu-id="d7064-385">jQuery 버전 1.7</span><span class="sxs-lookup"><span data-stu-id="d7064-385">jQuery version 1.7</span></span>

- <span data-ttu-id="d7064-386">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.js</span><span class="sxs-lookup"><span data-stu-id="d7064-386">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.js</span></span>
- <span data-ttu-id="d7064-387">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-387">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.min.js</span></span>
- <span data-ttu-id="d7064-388">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="d7064-388">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7-vsdoc.js</span></span>

#### <a name="jquery-version-164"></a><span data-ttu-id="d7064-389">jQuery 버전 1.6.4</span><span class="sxs-lookup"><span data-stu-id="d7064-389">jQuery version 1.6.4</span></span>

- <span data-ttu-id="d7064-390">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.js</span><span class="sxs-lookup"><span data-stu-id="d7064-390">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.js</span></span>
- <span data-ttu-id="d7064-391">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-391">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.min.js</span></span>
- <span data-ttu-id="d7064-392">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="d7064-392">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4-vsdoc.js</span></span>

#### <a name="jquery-version-163"></a><span data-ttu-id="d7064-393">jQuery 버전 1.6.3</span><span class="sxs-lookup"><span data-stu-id="d7064-393">jQuery version 1.6.3</span></span>

- <span data-ttu-id="d7064-394">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.js</span><span class="sxs-lookup"><span data-stu-id="d7064-394">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.js</span></span>
- <span data-ttu-id="d7064-395">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-395">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.min.js</span></span>
- <span data-ttu-id="d7064-396">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="d7064-396">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3-vsdoc.js</span></span>

#### <a name="jquery-version-162"></a><span data-ttu-id="d7064-397">jQuery 버전 1.6.2</span><span class="sxs-lookup"><span data-stu-id="d7064-397">jQuery version 1.6.2</span></span>

- <span data-ttu-id="d7064-398">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.js</span><span class="sxs-lookup"><span data-stu-id="d7064-398">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.js</span></span>
- <span data-ttu-id="d7064-399">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-399">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.min.js</span></span>
- <span data-ttu-id="d7064-400">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="d7064-400">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2-vsdoc.js</span></span>

#### <a name="jquery-version-161"></a><span data-ttu-id="d7064-401">jQuery 버전 1.6.1</span><span class="sxs-lookup"><span data-stu-id="d7064-401">jQuery version 1.6.1</span></span>

- <span data-ttu-id="d7064-402">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.js</span><span class="sxs-lookup"><span data-stu-id="d7064-402">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.js</span></span>
- <span data-ttu-id="d7064-403">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-403">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.min.js</span></span>
- <span data-ttu-id="d7064-404">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="d7064-404">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1-vsdoc.js</span></span>

#### <a name="jquery-version-16"></a><span data-ttu-id="d7064-405">jQuery 버전 1.6</span><span class="sxs-lookup"><span data-stu-id="d7064-405">jQuery version 1.6</span></span>

- <span data-ttu-id="d7064-406">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.js</span><span class="sxs-lookup"><span data-stu-id="d7064-406">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.js</span></span>
- <span data-ttu-id="d7064-407">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-407">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.min.js</span></span>
- <span data-ttu-id="d7064-408">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="d7064-408">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6-vsdoc.js</span></span>

#### <a name="jquery-version-152"></a><span data-ttu-id="d7064-409">1.5.2 jQuery 버전</span><span class="sxs-lookup"><span data-stu-id="d7064-409">jQuery version 1.5.2</span></span>

- <span data-ttu-id="d7064-410">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.js</span><span class="sxs-lookup"><span data-stu-id="d7064-410">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.js</span></span>
- <span data-ttu-id="d7064-411">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-411">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.min.js</span></span>
- <span data-ttu-id="d7064-412">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="d7064-412">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2-vsdoc.js</span></span>

#### <a name="jquery-version-151"></a><span data-ttu-id="d7064-413">1.5.1 jQuery 버전</span><span class="sxs-lookup"><span data-stu-id="d7064-413">jQuery version 1.5.1</span></span>

- <span data-ttu-id="d7064-414">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.js</span><span class="sxs-lookup"><span data-stu-id="d7064-414">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.js</span></span>
- <span data-ttu-id="d7064-415">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-415">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.min.js</span></span>
- <span data-ttu-id="d7064-416">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="d7064-416">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1-vsdoc.js</span></span>

#### <a name="jquery-version-15"></a><span data-ttu-id="d7064-417">jQuery 버전 1.5</span><span class="sxs-lookup"><span data-stu-id="d7064-417">jQuery version 1.5</span></span>

- <span data-ttu-id="d7064-418">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.js</span><span class="sxs-lookup"><span data-stu-id="d7064-418">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.js</span></span>
- <span data-ttu-id="d7064-419">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-419">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.min.js</span></span>
- <span data-ttu-id="d7064-420">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="d7064-420">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5-vsdoc.js</span></span>

#### <a name="jquery-version-144"></a><span data-ttu-id="d7064-421">jQuery 버전 1.4.4</span><span class="sxs-lookup"><span data-stu-id="d7064-421">jQuery version 1.4.4</span></span>

- <span data-ttu-id="d7064-422">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.js</span><span class="sxs-lookup"><span data-stu-id="d7064-422">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.js</span></span>
- <span data-ttu-id="d7064-423">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-423">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.min.js</span></span>
- <span data-ttu-id="d7064-424">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="d7064-424">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4-vsdoc.js</span></span>

#### <a name="jquery-version-143"></a><span data-ttu-id="d7064-425">jQuery 버전 1.4.3</span><span class="sxs-lookup"><span data-stu-id="d7064-425">jQuery version 1.4.3</span></span>

- <span data-ttu-id="d7064-426">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.js</span><span class="sxs-lookup"><span data-stu-id="d7064-426">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.js</span></span>
- <span data-ttu-id="d7064-427">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-427">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.min.js</span></span>
- <span data-ttu-id="d7064-428">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="d7064-428">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3-vsdoc.js</span></span>

#### <a name="jquery-version-142"></a><span data-ttu-id="d7064-429">1.4.2 jQuery 버전</span><span class="sxs-lookup"><span data-stu-id="d7064-429">jQuery version 1.4.2</span></span>

- <span data-ttu-id="d7064-430">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.js</span><span class="sxs-lookup"><span data-stu-id="d7064-430">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.js</span></span>
- <span data-ttu-id="d7064-431">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-431">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.min.js</span></span>
- <span data-ttu-id="d7064-432">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="d7064-432">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2-vsdoc.js</span></span>

#### <a name="jquery-version-141"></a><span data-ttu-id="d7064-433">1.4.1 jQuery 버전</span><span class="sxs-lookup"><span data-stu-id="d7064-433">jQuery version 1.4.1</span></span>

- <span data-ttu-id="d7064-434">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.js</span><span class="sxs-lookup"><span data-stu-id="d7064-434">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.js</span></span>
- <span data-ttu-id="d7064-435">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-435">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.min.js</span></span>
- <span data-ttu-id="d7064-436">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="d7064-436">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1-vsdoc.js</span></span>

#### <a name="jquery-version-14"></a><span data-ttu-id="d7064-437">jQuery 버전 1.4</span><span class="sxs-lookup"><span data-stu-id="d7064-437">jQuery version 1.4</span></span>

- <span data-ttu-id="d7064-438">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.js</span><span class="sxs-lookup"><span data-stu-id="d7064-438">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.js</span></span>
- <span data-ttu-id="d7064-439">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-439">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.min.js</span></span>

#### <a name="jquery-version-132"></a><span data-ttu-id="d7064-440">1.3.2 jQuery 버전</span><span class="sxs-lookup"><span data-stu-id="d7064-440">jQuery version 1.3.2</span></span>

- <span data-ttu-id="d7064-441">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.js</span><span class="sxs-lookup"><span data-stu-id="d7064-441">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.js</span></span>
- <span data-ttu-id="d7064-442">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-442">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min.js</span></span>
- <span data-ttu-id="d7064-443">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="d7064-443">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2-vsdoc.js</span></span>
- <span data-ttu-id="d7064-444">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="d7064-444">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min-vsdoc.js</span></span>

<a id="jQuery_Migrate_Releases_on_the_CDN_1"></a>

### <a name="jquery-migrate-releases-on-the-cdn"></a><span data-ttu-id="d7064-445">CDN에서 jQuery 마이그레이션할 릴리스</span><span class="sxs-lookup"><span data-stu-id="d7064-445">jQuery Migrate Releases on the CDN</span></span>

<span data-ttu-id="d7064-446">다음 버전의 jQuery 마이그레이션 CDN에 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-446">The following releases of jQuery Migrate are hosted on the CDN:</span></span>

#### <a name="jquery-migrate-version-300"></a><span data-ttu-id="d7064-447">jQuery 버전 3.0.0 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="d7064-447">jQuery Migrate version 3.0.0</span></span>

- <span data-ttu-id="d7064-448">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.js</span><span class="sxs-lookup"><span data-stu-id="d7064-448">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.js</span></span>
- <span data-ttu-id="d7064-449">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-449">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.min.js</span></span>

#### <a name="jquery-migrate-version-121"></a><span data-ttu-id="d7064-450">jQuery 버전 1.2.1 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="d7064-450">jQuery Migrate version 1.2.1</span></span>

- <span data-ttu-id="d7064-451">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.js</span><span class="sxs-lookup"><span data-stu-id="d7064-451">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.js</span></span>
- <span data-ttu-id="d7064-452">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-452">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.min.js</span></span>

<span data-ttu-id="d7064-453">jQuery 버전 1.2.0 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="d7064-453">jQuery Migrate version 1.2.0</span></span>

- <span data-ttu-id="d7064-454">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.js</span><span class="sxs-lookup"><span data-stu-id="d7064-454">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.js</span></span>
- <span data-ttu-id="d7064-455">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-455">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.min.js</span></span>

#### <a name="jquery-migrate-version-111"></a><span data-ttu-id="d7064-456">jQuery 버전 1.1.1 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="d7064-456">jQuery Migrate version 1.1.1</span></span>

- <span data-ttu-id="d7064-457">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.js</span><span class="sxs-lookup"><span data-stu-id="d7064-457">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.js</span></span>
- <span data-ttu-id="d7064-458">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-458">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.min.js</span></span>

#### <a name="jquery-migrate-version-110"></a><span data-ttu-id="d7064-459">jQuery 버전 1.1.0 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="d7064-459">jQuery Migrate version 1.1.0</span></span>

- <span data-ttu-id="d7064-460">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.js</span><span class="sxs-lookup"><span data-stu-id="d7064-460">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.js</span></span>
- <span data-ttu-id="d7064-461">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-461">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.min.js</span></span>

#### <a name="jquery-migrate-version-100"></a><span data-ttu-id="d7064-462">jQuery 버전 1.0.0 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="d7064-462">jQuery Migrate version 1.0.0</span></span>

- <span data-ttu-id="d7064-463">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.js</span><span class="sxs-lookup"><span data-stu-id="d7064-463">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.js</span></span>
- <span data-ttu-id="d7064-464">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-464">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.min.js</span></span>

<a id="jQuery_UI_Releases_on_the_CDN_2"></a>

### <a name="jquery-ui-releases-on-the-cdn"></a><span data-ttu-id="d7064-465">jQuery UI CDN에 있는 릴리스</span><span class="sxs-lookup"><span data-stu-id="d7064-465">jQuery UI Releases on the CDN</span></span>

<span data-ttu-id="d7064-466">JQuery UI 라이브러리의 다음 릴리스에서이 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-466">The following releases of the jQuery UI library are hosted on this CDN.</span></span> <span data-ttu-id="d7064-467">파일의 실제 목록을 확인 하려면 각 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-467">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="d7064-468">jQuery UI 1.12.1</span><span class="sxs-lookup"><span data-stu-id="d7064-468">jQuery UI 1.12.1</span></span>](jquery-ui/cdnjqueryui1121.md "jQuery UI 1.12.1 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-469">jQuery UI 1.12.0</span><span class="sxs-lookup"><span data-stu-id="d7064-469">jQuery UI 1.12.0</span></span>](jquery-ui/cdnjqueryui1120.md "jQuery UI 1.12.0 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-470">jQuery UI 1.11.4</span><span class="sxs-lookup"><span data-stu-id="d7064-470">jQuery UI 1.11.4</span></span>](jquery-ui/cdnjqueryui1114.md "jQuery UI 1.11.4 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-471">jQuery UI 1.11.3</span><span class="sxs-lookup"><span data-stu-id="d7064-471">jQuery UI 1.11.3</span></span>](jquery-ui/cdnjqueryui1113.md "jQuery UI 1.11.3 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-472">jQuery UI 1.11.2</span><span class="sxs-lookup"><span data-stu-id="d7064-472">jQuery UI 1.11.2</span></span>](jquery-ui/cdnjqueryui1112.md "jQuery UI 1.11.2 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-473">jQuery UI 1.11.1</span><span class="sxs-lookup"><span data-stu-id="d7064-473">jQuery UI 1.11.1</span></span>](jquery-ui/cdnjqueryui1111.md "jQuery UI 1.11.1 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-474">jQuery UI 1.11.0</span><span class="sxs-lookup"><span data-stu-id="d7064-474">jQuery UI 1.11.0</span></span>](jquery-ui/cdnjqueryui1110.md "jQuery UI 1.11.0 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-475">jQuery UI 1.10.4</span><span class="sxs-lookup"><span data-stu-id="d7064-475">jQuery UI 1.10.4</span></span>](jquery-ui/cdnjqueryui1104.md "jQuery UI 1.10.4 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-476">jQuery UI 1.10.3</span><span class="sxs-lookup"><span data-stu-id="d7064-476">jQuery UI 1.10.3</span></span>](jquery-ui/cdnjqueryui1103.md "jQuery UI 1.10.3 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-477">jQuery 1.10.2 UI</span><span class="sxs-lookup"><span data-stu-id="d7064-477">jQuery UI 1.10.2</span></span>](jquery-ui/cdnjqueryui1102.md "jQuery 1.10.2 Microsoft Ajax CDN에서 UI")
- [<span data-ttu-id="d7064-478">jQuery UI 1.10.1</span><span class="sxs-lookup"><span data-stu-id="d7064-478">jQuery UI 1.10.1</span></span>](jquery-ui/cdnjqueryui1101.md "jQuery UI 1.10.1 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-479">jQuery UI 1.10.0</span><span class="sxs-lookup"><span data-stu-id="d7064-479">jQuery UI 1.10.0</span></span>](jquery-ui/cdnjqueryui1100.md "jQuery UI 1.10.0 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-480">jQuery UI 1.9.2</span><span class="sxs-lookup"><span data-stu-id="d7064-480">jQuery UI 1.9.2</span></span>](jquery-ui/cdnjqueryui192.md "jQuery UI 1.9.2 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-481">jQuery UI 1.9.1</span><span class="sxs-lookup"><span data-stu-id="d7064-481">jQuery UI 1.9.1</span></span>](jquery-ui/cdnjqueryui191.md "jQuery UI 1.9.1 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-482">jQuery UI 1.9.0</span><span class="sxs-lookup"><span data-stu-id="d7064-482">jQuery UI 1.9.0</span></span>](jquery-ui/cdnjqueryui190.md "jQuery UI 1.9.0 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-483">jQuery UI 1.8.24</span><span class="sxs-lookup"><span data-stu-id="d7064-483">jQuery UI 1.8.24</span></span>](jquery-ui/cdnjqueryui1824.md "jQuery UI 1.8.24 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-484">jQuery UI 1.8.23</span><span class="sxs-lookup"><span data-stu-id="d7064-484">jQuery UI 1.8.23</span></span>](jquery-ui/cdnjqueryui1823.md "jQuery UI 1.8.23 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-485">jQuery UI 1.8.22</span><span class="sxs-lookup"><span data-stu-id="d7064-485">jQuery UI 1.8.22</span></span>](jquery-ui/cdnjqueryui1822.md "jQuery UI 1.8.22 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-486">jQuery UI 1.8.21</span><span class="sxs-lookup"><span data-stu-id="d7064-486">jQuery UI 1.8.21</span></span>](jquery-ui/cdnjqueryui1821.md "jQuery UI 1.8.21 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-487">jQuery UI 1.8.20</span><span class="sxs-lookup"><span data-stu-id="d7064-487">jQuery UI 1.8.20</span></span>](jquery-ui/cdnjqueryui1820.md "jQuery UI 1.8.20 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-488">jQuery UI 1.8.19</span><span class="sxs-lookup"><span data-stu-id="d7064-488">jQuery UI 1.8.19</span></span>](jquery-ui/cdnjqueryui1819.md "jQuery UI 1.8.19 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-489">jQuery UI 1.8.18</span><span class="sxs-lookup"><span data-stu-id="d7064-489">jQuery UI 1.8.18</span></span>](jquery-ui/cdnjqueryui1818.md "jQuery UI 1.8.18 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-490">jQuery UI 1.8.17</span><span class="sxs-lookup"><span data-stu-id="d7064-490">jQuery UI 1.8.17</span></span>](jquery-ui/cdnjqueryui1817.md "jQuery UI 1.8.17 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-491">jQuery UI 1.8.16</span><span class="sxs-lookup"><span data-stu-id="d7064-491">jQuery UI 1.8.16</span></span>](jquery-ui/cdnjqueryui1816.md "jQuery UI 1.8.16 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-492">jQuery UI 1.8.15</span><span class="sxs-lookup"><span data-stu-id="d7064-492">jQuery UI 1.8.15</span></span>](jquery-ui/cdnjqueryui1815.md "jQuery UI 1.8.15 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-493">jQuery UI 1.8.14</span><span class="sxs-lookup"><span data-stu-id="d7064-493">jQuery UI 1.8.14</span></span>](jquery-ui/cdnjqueryui1814.md "jQuery UI 1.8.14 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-494">jQuery UI 1.8.13</span><span class="sxs-lookup"><span data-stu-id="d7064-494">jQuery UI 1.8.13</span></span>](jquery-ui/cdnjqueryui1813.md "jQuery UI 1.8.13 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-495">jQuery UI 1.8.12</span><span class="sxs-lookup"><span data-stu-id="d7064-495">jQuery UI 1.8.12</span></span>](jquery-ui/cdnjqueryui1812.md "jQuery UI 1.8.12 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-496">jQuery UI 1.8.11</span><span class="sxs-lookup"><span data-stu-id="d7064-496">jQuery UI 1.8.11</span></span>](jquery-ui/cdnjqueryui1811.md "jQuery UI 1.8.11 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-497">jQuery UI 1.8.10</span><span class="sxs-lookup"><span data-stu-id="d7064-497">jQuery UI 1.8.10</span></span>](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-498">jQuery UI 1.8.9</span><span class="sxs-lookup"><span data-stu-id="d7064-498">jQuery UI 1.8.9</span></span>](jquery-ui/cdnjqueryui189.md "jQuery UI 1.8.9 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-499">jQuery UI 1.8.8</span><span class="sxs-lookup"><span data-stu-id="d7064-499">jQuery UI 1.8.8</span></span>](jquery-ui/cdnjqueryui188.md "jQuery UI 1.8.8 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-500">jQuery UI 1.8.7</span><span class="sxs-lookup"><span data-stu-id="d7064-500">jQuery UI 1.8.7</span></span>](jquery-ui/cdnjqueryui187.md "jQuery UI 1.8.7 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-501">jQuery UI 1.8.6</span><span class="sxs-lookup"><span data-stu-id="d7064-501">jQuery UI 1.8.6</span></span>](jquery-ui/cdnjqueryui186.md "jQuery UI 1.8.6 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-502">jQuery UI 1.8.5</span><span class="sxs-lookup"><span data-stu-id="d7064-502">jQuery UI 1.8.5</span></span>](jquery-ui/cdnjqueryui185.md "jQuery UI 1.8.5")

<a id="jQuery_Validation_Releases_on_the_CDN_3"></a>

### <a name="jquery-validation-releases-on-the-cdn"></a><span data-ttu-id="d7064-503">jQuery 유효성 검사는 CDN에 있는 릴리스</span><span class="sxs-lookup"><span data-stu-id="d7064-503">jQuery Validation Releases on the CDN</span></span>

<span data-ttu-id="d7064-504">JQuery 유효성 검사 라이브러리의 다음 릴리스에서이 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-504">The following releases of the jQuery Validation library are hosted on this CDN.</span></span> <span data-ttu-id="d7064-505">파일의 실제 목록을 확인 하려면 각 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-505">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="d7064-506">jQuery 유효성 검사 1.17.0</span><span class="sxs-lookup"><span data-stu-id="d7064-506">jQuery Validate 1.17.0</span></span>](jquery-validate/cdnjqueryvalidate1170.md "jQuery 유효성 검사 1.17.0")
- [<span data-ttu-id="d7064-507">jQuery 유효성 검사 1.16.0</span><span class="sxs-lookup"><span data-stu-id="d7064-507">jQuery Validate 1.16.0</span></span>](jquery-validate/cdnjqueryvalidate1160.md "jQuery 유효성 검사 1.16.0")
- [<span data-ttu-id="d7064-508">jQuery 유효성 검사 1.15.1</span><span class="sxs-lookup"><span data-stu-id="d7064-508">jQuery Validate 1.15.1</span></span>](jquery-validate/cdnjqueryvalidate1151.md "jQuery 유효성 검사 1.15.1")
- [<span data-ttu-id="d7064-509">jQuery 유효성 검사 1.15.0</span><span class="sxs-lookup"><span data-stu-id="d7064-509">jQuery Validate 1.15.0</span></span>](jquery-validate/cdnjqueryvalidate1150.md "jQuery 유효성 검사 1.15.0")
- [<span data-ttu-id="d7064-510">jQuery 유효성 검사 1.14.0</span><span class="sxs-lookup"><span data-stu-id="d7064-510">jQuery Validate 1.14.0</span></span>](jquery-validate/cdnjqueryvalidate1140.md "jQuery 유효성 검사 1.14.0")
- [<span data-ttu-id="d7064-511">jQuery 유효성 검사 1.13.1</span><span class="sxs-lookup"><span data-stu-id="d7064-511">jQuery Validate 1.13.1</span></span>](jquery-validate/cdnjqueryvalidate1131.md "jQuery 유효성 검사 1.13.1")
- [<span data-ttu-id="d7064-512">jQuery 유효성 검사 1.13.0</span><span class="sxs-lookup"><span data-stu-id="d7064-512">jQuery Validate 1.13.0</span></span>](jquery-validate/cdnjqueryvalidate1130.md "jQuery 유효성 검사 1.13.0")
- [<span data-ttu-id="d7064-513">jQuery 유효성 검사 1.12.0</span><span class="sxs-lookup"><span data-stu-id="d7064-513">jQuery Validate 1.12.0</span></span>](jquery-validate/cdnjqueryvalidate1120.md "jQuery 유효성 검사 1.12.0")
- [<span data-ttu-id="d7064-514">jQuery 유효성 검사 1.11.1</span><span class="sxs-lookup"><span data-stu-id="d7064-514">jQuery Validate 1.11.1</span></span>](jquery-validate/cdnjqueryvalidate1111.md "jQuery 유효성 검사 1.11.1")
- [<span data-ttu-id="d7064-515">jQuery 유효성 검사 1.11.0</span><span class="sxs-lookup"><span data-stu-id="d7064-515">jQuery Validate 1.11.0</span></span>](jquery-validate/cdnjqueryvalidate111.md "jQuery 유효성 검사 1.11.0")
- [<span data-ttu-id="d7064-516">jQuery 유효성 검사 1.10.0</span><span class="sxs-lookup"><span data-stu-id="d7064-516">jQuery Validate 1.10.0</span></span>](jquery-validate/cdnjqueryvalidate110.md "jQuery 유효성 검사 1.10.0")
- [<span data-ttu-id="d7064-517">jQuery 유효성 검사 1.9</span><span class="sxs-lookup"><span data-stu-id="d7064-517">jQuery Validate 1.9</span></span>](jquery-validate/cdnjqueryvalidate19.md "jquery.validate 버전 1.9")
- [<span data-ttu-id="d7064-518">jQuery 유효성 검사 1.8.1</span><span class="sxs-lookup"><span data-stu-id="d7064-518">jQuery Validate 1.8.1</span></span>](jquery-validate/cdnjqueryvalidate181.md "1.8.1 jquery.validate 버전")
- [<span data-ttu-id="d7064-519">jQuery 유효성 검사 1.8</span><span class="sxs-lookup"><span data-stu-id="d7064-519">jQuery Validate 1.8</span></span>](jquery-validate/cdnjqueryvalidate18.md "jquery.validate 버전 1.8")
- [<span data-ttu-id="d7064-520">jQuery 유효성 검사 1.7</span><span class="sxs-lookup"><span data-stu-id="d7064-520">jQuery Validate 1.7</span></span>](jquery-validate/cdnjqueryvalidate17.md "jquery.validate 버전 1.7")
- [<span data-ttu-id="d7064-521">jQuery 유효성 검사 1.6</span><span class="sxs-lookup"><span data-stu-id="d7064-521">jQuery Validate 1.6</span></span>](jquery-validate/cdnjqueryvalidate16.md "jQuery 유효성 검사 1.6")
- [<span data-ttu-id="d7064-522">jQuery 유효성 검사 1.5.5</span><span class="sxs-lookup"><span data-stu-id="d7064-522">jQuery Validate 1.5.5</span></span>](jquery-validate/cdnjqueryvalidate155.md "jQuery 유효성 검사 1.5.5")

<a id="jQuery_Mobile_Releases_on_the_CDN_4"></a>

### <a name="jquery-mobile-releases-on-the-cdn"></a><span data-ttu-id="d7064-523">jQuery Mobile CDN에 있는 릴리스</span><span class="sxs-lookup"><span data-stu-id="d7064-523">jQuery Mobile Releases on the CDN</span></span>

<span data-ttu-id="d7064-524">JQuery 모바일 라이브러리의 다음 릴리스에서이 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-524">The following releases of the jQuery Mobile library are hosted on this CDN.</span></span> <span data-ttu-id="d7064-525">파일의 실제 목록을 확인 하려면 각 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-525">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="d7064-526">jQuery Mobile 1.4.5</span><span class="sxs-lookup"><span data-stu-id="d7064-526">jQuery Mobile 1.4.5</span></span>](jquery-mobile/cdnjquerymobile145.md "jQuery Mobile 1.4.5 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-527">jQuery Mobile 1.4.2</span><span class="sxs-lookup"><span data-stu-id="d7064-527">jQuery Mobile 1.4.2</span></span>](jquery-mobile/cdnjquerymobile142.md "jQuery Mobile 1.4.2 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-528">jQuery Mobile 1.4.1</span><span class="sxs-lookup"><span data-stu-id="d7064-528">jQuery Mobile 1.4.1</span></span>](jquery-mobile/cdnjquerymobile141.md "jQuery Mobile 1.4.1 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-529">jQuery Mobile 1.4.0</span><span class="sxs-lookup"><span data-stu-id="d7064-529">jQuery Mobile 1.4.0</span></span>](jquery-mobile/cdnjquerymobile140.md "jQuery Mobile 1.4.0 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-530">jQuery Mobile 1.3.2</span><span class="sxs-lookup"><span data-stu-id="d7064-530">jQuery Mobile 1.3.2</span></span>](jquery-mobile/cdnjquerymobile132.md "jQuery Mobile 1.3.2 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-531">jQuery Mobile 1.3.1</span><span class="sxs-lookup"><span data-stu-id="d7064-531">jQuery Mobile 1.3.1</span></span>](jquery-mobile/cdnjquerymobile131.md "jQuery Mobile 1.3.1 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-532">jQuery Mobile 1.3.0</span><span class="sxs-lookup"><span data-stu-id="d7064-532">jQuery Mobile 1.3.0</span></span>](jquery-mobile/cdnjquerymobile130.md "jQuery Mobile 1.3.0 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-533">jQuery Mobile 1.2.0</span><span class="sxs-lookup"><span data-stu-id="d7064-533">jQuery Mobile 1.2.0</span></span>](jquery-mobile/cdnjquerymobile120.md "jQuery Mobile 1.2.0 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-534">jQuery Mobile 1.1.2</span><span class="sxs-lookup"><span data-stu-id="d7064-534">jQuery Mobile 1.1.2</span></span>](jquery-mobile/cdnjquerymobile112.md "jQuery Mobile 1.1.2 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-535">jQuery Mobile 1.1.1</span><span class="sxs-lookup"><span data-stu-id="d7064-535">jQuery Mobile 1.1.1</span></span>](jquery-mobile/cdnjquerymobile111.md "jQuery Mobile 1.1.1 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-536">jQuery Mobile 1.1.0</span><span class="sxs-lookup"><span data-stu-id="d7064-536">jQuery Mobile 1.1.0</span></span>](jquery-mobile/cdnjquerymobile110.md "jQuery Mobile 1.1.0 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-537">jQuery Mobile 1.1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="d7064-537">jQuery Mobile 1.1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile110rc2.md "jQuery Mobile 1.1.0 RC2 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-538">jQuery Mobile 1.0.1</span><span class="sxs-lookup"><span data-stu-id="d7064-538">jQuery Mobile 1.0.1</span></span>](jquery-mobile/cdnjquerymobile101.md "jQuery Mobile 1.0.1 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-539">jQuery Mobile 1.0</span><span class="sxs-lookup"><span data-stu-id="d7064-539">jQuery Mobile 1.0</span></span>](jquery-mobile/cdnjquerymobile10.md "jQuery Mobile 1.0 Microsoft Ajax CDN에서")
- [<span data-ttu-id="d7064-540">jQuery Mobile 1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="d7064-540">jQuery Mobile 1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile10rc2.md "Microsoft Ajax CDN에서 jQuery Mobile 1.0 RC2")
- [<span data-ttu-id="d7064-541">jQuery Mobile 1.0 RC 1</span><span class="sxs-lookup"><span data-stu-id="d7064-541">jQuery Mobile 1.0 RC 1</span></span>](jquery-mobile/cdnjquerymobile10rc1.md "Microsoft Ajax CDN에서 jQuery Mobile 1.0 RC1")
- [<span data-ttu-id="d7064-542">jQuery Mobile 1.0 베타 3</span><span class="sxs-lookup"><span data-stu-id="d7064-542">jQuery Mobile 1.0 beta 3</span></span>](jquery-mobile/cdnjquerymobile10b3.md "Microsoft Ajax CDN에서 jQuery Mobile 1.0 베타 3")

<a id="jQuery_Templates_Releases_on_the_CDN_5"></a>

### <a name="jquery-templates-releases-on-the-cdn"></a><span data-ttu-id="d7064-543">jQuery CDN에서 템플릿 릴리스</span><span class="sxs-lookup"><span data-stu-id="d7064-543">jQuery Templates Releases on the CDN</span></span>

<span data-ttu-id="d7064-544">다음 버전의 jQuery 템플릿 플러그 인이이 CDN에서 호스트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-544">The following releases of the jQuery Templates plugin are hosted on this CDN.</span></span> <span data-ttu-id="d7064-545">파일의 실제 목록을 확인 하려면 각 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-545">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="d7064-546">jQuery 템플릿 베타 1</span><span class="sxs-lookup"><span data-stu-id="d7064-546">jQuery Templates Beta 1</span></span>](jquery-templates/cdnjquerytemplatesbeta1.md "jQuery 템플릿 베타 1")

<a id="jQuery_Cycle_Releases_on_the_CDN_6"></a>

### <a name="jquery-cycle-releases-on-the-cdn"></a><span data-ttu-id="d7064-547">jQuery CDN에서 주기 릴리스</span><span class="sxs-lookup"><span data-stu-id="d7064-547">jQuery Cycle Releases on the CDN</span></span>

<span data-ttu-id="d7064-548">다음 릴리스에 jQuery 주기 플러그 인을이 CDN에서 호스트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-548">The following releases of the jQuery Cycle plugin are hosted on this CDN.</span></span> <span data-ttu-id="d7064-549">파일의 실제 목록을 확인 하려면 각 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-549">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="d7064-550">jQuery 주기 2.99</span><span class="sxs-lookup"><span data-stu-id="d7064-550">jQuery Cycle 2.99</span></span>](jquery-cycle/cdnjquerycycle299.md "jQuery 주기 2.99")
- [<span data-ttu-id="d7064-551">jQuery 주기 2.94</span><span class="sxs-lookup"><span data-stu-id="d7064-551">jQuery Cycle 2.94</span></span>](jquery-cycle/cdnjquerycycle294.md "jQuery 주기 2.94")
- [<span data-ttu-id="d7064-552">jQuery 주기 2.88</span><span class="sxs-lookup"><span data-stu-id="d7064-552">jQuery Cycle 2.88</span></span>](jquery-cycle/cdnjquerycycle288.md "jQuery 주기 2.88")

<a id="jQuery_DataTables_Releases_on_the_CDN_7"></a>

### <a name="jquery-datatables-releases-on-the-cdn"></a><span data-ttu-id="d7064-553">jQuery CDN에서 DataTables 릴리스</span><span class="sxs-lookup"><span data-stu-id="d7064-553">jQuery DataTables Releases on the CDN</span></span>

<span data-ttu-id="d7064-554">다음 릴리스에 jQuery Datatable 플러그 인을이 CDN에서 호스트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-554">The following releases of the jQuery DataTables plugin are hosted on this CDN.</span></span> <span data-ttu-id="d7064-555">파일의 실제 목록을 확인 하려면 각 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-555">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="d7064-556">jQuery Datatable 1.10.5</span><span class="sxs-lookup"><span data-stu-id="d7064-556">jQuery DataTables 1.10.5</span></span>](jquery-datatables/cdnjquerydatatables105.md "jQuery Datatable 1.10.5")
- [<span data-ttu-id="d7064-557">jQuery Datatable 1.10.4</span><span class="sxs-lookup"><span data-stu-id="d7064-557">jQuery DataTables 1.10.4</span></span>](jquery-datatables/cdnjquerydatatables104.md "jQuery Datatable 1.10.4")
- [<span data-ttu-id="d7064-558">jQuery Datatable 1.9.4</span><span class="sxs-lookup"><span data-stu-id="d7064-558">jQuery DataTables 1.9.4</span></span>](jquery-datatables/cdnjquerydatatables194.md "jQuery Datatable 1.9.4")
- [<span data-ttu-id="d7064-559">jQuery Datatable 1.9.3</span><span class="sxs-lookup"><span data-stu-id="d7064-559">jQuery DataTables 1.9.3</span></span>](jquery-datatables/cdnjquerydatatables193.md "jQuery Datatable 1.9.3")
- [<span data-ttu-id="d7064-560">jQuery Datatable 1.9.2</span><span class="sxs-lookup"><span data-stu-id="d7064-560">jQuery DataTables 1.9.2</span></span>](jquery-datatables/cdnjquerydatatables192.md "jQuery Datatable 1.9.2")
- [<span data-ttu-id="d7064-561">jQuery Datatable 1.9.1</span><span class="sxs-lookup"><span data-stu-id="d7064-561">jQuery DataTables 1.9.1</span></span>](jquery-datatables/cdnjquerydatatables191.md "jQuery Datatable 1.9.1")
- [<span data-ttu-id="d7064-562">jQuery Datatable 1.9.0</span><span class="sxs-lookup"><span data-stu-id="d7064-562">jQuery DataTables 1.9.0</span></span>](jquery-datatables/cdnjquerydatatables190.md "jQuery Datatable 1.9.0")
- [<span data-ttu-id="d7064-563">jQuery Datatable 1.8.2</span><span class="sxs-lookup"><span data-stu-id="d7064-563">jQuery DataTables 1.8.2</span></span>](jquery-datatables/cdnjquerydatatables182.md "jQuery Datatable 1.8.2")

<a id="Modernizr_Releases_on_the_CDN_8"></a>

### <a name="modernizr-releases-on-the-cdn"></a><span data-ttu-id="d7064-564">CDN에서 Modernizr 릴리스</span><span class="sxs-lookup"><span data-stu-id="d7064-564">Modernizr Releases on the CDN</span></span>

<span data-ttu-id="d7064-565">다음 릴리스의 [Modernizr](http://www.modernizr.com "Modernizr") CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-565">The following releases of [Modernizr](http://www.modernizr.com "Modernizr") are hosted on the CDN:</span></span>

- <span data-ttu-id="d7064-566">http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.8.3.js</span><span class="sxs-lookup"><span data-stu-id="d7064-566">http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.8.3.js</span></span>
- <span data-ttu-id="d7064-567">http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.2.js</span><span class="sxs-lookup"><span data-stu-id="d7064-567">http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.2.js</span></span>
- <span data-ttu-id="d7064-568">http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.1.js</span><span class="sxs-lookup"><span data-stu-id="d7064-568">http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.1.js</span></span>
- <span data-ttu-id="d7064-569">http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.6.2.js</span><span class="sxs-lookup"><span data-stu-id="d7064-569">http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.6.2.js</span></span>
- <span data-ttu-id="d7064-570">http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-1.7-development-only.js</span><span class="sxs-lookup"><span data-stu-id="d7064-570">http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-1.7-development-only.js</span></span>
- <span data-ttu-id="d7064-571">http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.0.6-development-only.js</span><span class="sxs-lookup"><span data-stu-id="d7064-571">http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.0.6-development-only.js</span></span>

<a id="JSHint_Releases_on_the_CDN_10"></a>

### <a name="jshint-releases-on-the-cdn"></a><span data-ttu-id="d7064-572">CDN에서 JSHint 릴리스</span><span class="sxs-lookup"><span data-stu-id="d7064-572">JSHint Releases on the CDN</span></span>

<span data-ttu-id="d7064-573">다음 릴리스의 [JSHint](http://www.jshint.com "JSHint") CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-573">The following releases of [JSHint](http://www.jshint.com "JSHint") are hosted on the CDN:</span></span>

- <span data-ttu-id="d7064-574">http://ajax.aspnetcdn.com/ajax/jshint/r07/jshint.js</span><span class="sxs-lookup"><span data-stu-id="d7064-574">http://ajax.aspnetcdn.com/ajax/jshint/r07/jshint.js</span></span>

<a id="Knockout_Releases_on_the_CDN_11"></a>

### <a name="knockout-releases-on-the-cdn"></a><span data-ttu-id="d7064-575">CDN에서 knockout 릴리스</span><span class="sxs-lookup"><span data-stu-id="d7064-575">Knockout Releases on the CDN</span></span>

<span data-ttu-id="d7064-576">다음 릴리스의 [Knockout](http://www.knockoutjs.com "Knockout") CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-576">The following releases of [Knockout](http://www.knockoutjs.com "Knockout") are hosted on the CDN:</span></span>

- <span data-ttu-id="d7064-577">http://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.1.js</span><span class="sxs-lookup"><span data-stu-id="d7064-577">http://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.1.js</span></span>
- <span data-ttu-id="d7064-578">http://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.1.debug.js</span><span class="sxs-lookup"><span data-stu-id="d7064-578">http://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.1.debug.js</span></span>
- <span data-ttu-id="d7064-579">http://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.0.js</span><span class="sxs-lookup"><span data-stu-id="d7064-579">http://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.0.js</span></span>
- <span data-ttu-id="d7064-580">http://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.0.debug.js</span><span class="sxs-lookup"><span data-stu-id="d7064-580">http://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.0.debug.js</span></span>
- <span data-ttu-id="d7064-581">http://ajax.aspnetcdn.com/ajax/knockout/knockout-2.1.0.js</span><span class="sxs-lookup"><span data-stu-id="d7064-581">http://ajax.aspnetcdn.com/ajax/knockout/knockout-2.1.0.js</span></span>
- <span data-ttu-id="d7064-582">http://ajax.aspnetcdn.com/ajax/knockout/knockout-2.1.0.debug.js</span><span class="sxs-lookup"><span data-stu-id="d7064-582">http://ajax.aspnetcdn.com/ajax/knockout/knockout-2.1.0.debug.js</span></span>
- <span data-ttu-id="d7064-583">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.0.0.js</span><span class="sxs-lookup"><span data-stu-id="d7064-583">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.0.0.js</span></span>
- <span data-ttu-id="d7064-584">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.0.0.debug.js</span><span class="sxs-lookup"><span data-stu-id="d7064-584">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.0.0.debug.js</span></span>
- <span data-ttu-id="d7064-585">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.1.0.js</span><span class="sxs-lookup"><span data-stu-id="d7064-585">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.1.0.js</span></span>
- <span data-ttu-id="d7064-586">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.1.0.debug.js</span><span class="sxs-lookup"><span data-stu-id="d7064-586">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.1.0.debug.js</span></span>
- <span data-ttu-id="d7064-587">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.2.0.js</span><span class="sxs-lookup"><span data-stu-id="d7064-587">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.2.0.js</span></span>
- <span data-ttu-id="d7064-588">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.2.0.debug.js</span><span class="sxs-lookup"><span data-stu-id="d7064-588">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.2.0.debug.js</span></span>
- <span data-ttu-id="d7064-589">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.3.0.js</span><span class="sxs-lookup"><span data-stu-id="d7064-589">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.3.0.js</span></span>
- <span data-ttu-id="d7064-590">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.3.0.debug.js</span><span class="sxs-lookup"><span data-stu-id="d7064-590">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.3.0.debug.js</span></span>
- <span data-ttu-id="d7064-591">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.0.js</span><span class="sxs-lookup"><span data-stu-id="d7064-591">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.0.js</span></span>
- <span data-ttu-id="d7064-592">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.0.debug.js</span><span class="sxs-lookup"><span data-stu-id="d7064-592">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.0.debug.js</span></span>
- <span data-ttu-id="d7064-593">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.1.js</span><span class="sxs-lookup"><span data-stu-id="d7064-593">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.1.js</span></span>
- <span data-ttu-id="d7064-594">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.1.debug.js</span><span class="sxs-lookup"><span data-stu-id="d7064-594">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.1.debug.js</span></span>
- <span data-ttu-id="d7064-595">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.2.js</span><span class="sxs-lookup"><span data-stu-id="d7064-595">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.2.js</span></span>
- <span data-ttu-id="d7064-596">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.2.debug.js</span><span class="sxs-lookup"><span data-stu-id="d7064-596">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.2.debug.js</span></span>

<a id="Globalize_Releases_on_the_CDN_12"></a>

### <a name="globalize-releases-on-the-cdn"></a><span data-ttu-id="d7064-597">CDN에서 릴리스 전역화</span><span class="sxs-lookup"><span data-stu-id="d7064-597">Globalize Releases on the CDN</span></span>

<span data-ttu-id="d7064-598">다음 릴리스의 [Globalize](https://github.com/jquery/globalize "Globalize") CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-598">The following releases of [Globalize](https://github.com/jquery/globalize "Globalize") are hosted on the CDN:</span></span>

#### <a name="globalize-version-100"></a><span data-ttu-id="d7064-599">버전 1.0.0을 전역화</span><span class="sxs-lookup"><span data-stu-id="d7064-599">Globalize version 1.0.0</span></span>

- <span data-ttu-id="d7064-600">http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize.js</span><span class="sxs-lookup"><span data-stu-id="d7064-600">http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize.js</span></span>
- <span data-ttu-id="d7064-601">http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/node-main.js</span><span class="sxs-lookup"><span data-stu-id="d7064-601">http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/node-main.js</span></span>
- <span data-ttu-id="d7064-602">http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/currency.js</span><span class="sxs-lookup"><span data-stu-id="d7064-602">http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/currency.js</span></span>
- <span data-ttu-id="d7064-603">http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/date.js</span><span class="sxs-lookup"><span data-stu-id="d7064-603">http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/date.js</span></span>
- <span data-ttu-id="d7064-604">http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/message.js</span><span class="sxs-lookup"><span data-stu-id="d7064-604">http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/message.js</span></span>
- <span data-ttu-id="d7064-605">http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/number.js</span><span class="sxs-lookup"><span data-stu-id="d7064-605">http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/number.js</span></span>
- <span data-ttu-id="d7064-606">http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/plural.js</span><span class="sxs-lookup"><span data-stu-id="d7064-606">http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/plural.js</span></span>
- <span data-ttu-id="d7064-607">http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/relative-time.js</span><span class="sxs-lookup"><span data-stu-id="d7064-607">http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/relative-time.js</span></span>

#### <a name="globalize-version-011"></a><span data-ttu-id="d7064-608">버전 0.1.1 전역화</span><span class="sxs-lookup"><span data-stu-id="d7064-608">Globalize version 0.1.1</span></span>

- <span data-ttu-id="d7064-609">http://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-609">http://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.min.js</span></span>
- <span data-ttu-id="d7064-610">http://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.js</span><span class="sxs-lookup"><span data-stu-id="d7064-610">http://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.js</span></span>
- <span data-ttu-id="d7064-611">http://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.cultures.js</span><span class="sxs-lookup"><span data-stu-id="d7064-611">http://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.cultures.js</span></span>

    - <span data-ttu-id="d7064-612">모든 문화권</span><span class="sxs-lookup"><span data-stu-id="d7064-612">all cultures</span></span>
- <span data-ttu-id="d7064-613">http://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.culture 합니다. {문화권 코드}.js</span><span class="sxs-lookup"><span data-stu-id="d7064-613">http://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.culture.{culture-code}.js</span></span>

    - <span data-ttu-id="d7064-614">"{코드 문화권을 (를)"를 원하는 culture 코드로 바꿉니다, globalize.culture.en GB.js== Microsoft CDN에 예를 들어 파일을이 = = Microsoft에서 라이브러리가 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-614">Replace "{culture-code}" with the desired culture code, e.g. globalize.culture.en-GB.js== Microsoft Files on the CDN ==These libraries were uploaded by Microsoft.</span></span>

<a id="Respond_Releases_on_the_CDN_13"></a>

### <a name="respond-releases-on-the-cdn"></a><span data-ttu-id="d7064-615">CDN에서 릴리스 응답</span><span class="sxs-lookup"><span data-stu-id="d7064-615">Respond Releases on the CDN</span></span>

<span data-ttu-id="d7064-616">다음 릴리스의 [https://github.com/scottjehl/Respond](https://github.com/scottjehl/Respond "https://github.com/scottjehl/Respond") 응답 하는 CDN에 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-616">The following releases of [https://github.com/scottjehl/Respond](https://github.com/scottjehl/Respond "https://github.com/scottjehl/Respond") Respond are hosted on the CDN:</span></span>

#### <a name="respond-version-142"></a><span data-ttu-id="d7064-617">1.4.2 버전 응답</span><span class="sxs-lookup"><span data-stu-id="d7064-617">Respond version 1.4.2</span></span>

- <span data-ttu-id="d7064-618">http://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.js</span><span class="sxs-lookup"><span data-stu-id="d7064-618">http://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.js</span></span>
- <span data-ttu-id="d7064-619">http://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-619">http://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.min.js</span></span>
- <span data-ttu-id="d7064-620">http://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.js</span><span class="sxs-lookup"><span data-stu-id="d7064-620">http://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.js</span></span>
- <span data-ttu-id="d7064-621">http://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-621">http://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.min.js</span></span>

#### <a name="respond-version-141"></a><span data-ttu-id="d7064-622">1.4.1 버전 응답</span><span class="sxs-lookup"><span data-stu-id="d7064-622">Respond version 1.4.1</span></span>

- <span data-ttu-id="d7064-623">http://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.js</span><span class="sxs-lookup"><span data-stu-id="d7064-623">http://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.js</span></span>
- <span data-ttu-id="d7064-624">http://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-624">http://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.min.js</span></span>
- <span data-ttu-id="d7064-625">http://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.js</span><span class="sxs-lookup"><span data-stu-id="d7064-625">http://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.js</span></span>
- <span data-ttu-id="d7064-626">http://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-626">http://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.min.js</span></span>

#### <a name="respond-version-140"></a><span data-ttu-id="d7064-627">버전 1.4.0 응답</span><span class="sxs-lookup"><span data-stu-id="d7064-627">Respond version 1.4.0</span></span>

- <span data-ttu-id="d7064-628">http://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.js</span><span class="sxs-lookup"><span data-stu-id="d7064-628">http://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.js</span></span>
- <span data-ttu-id="d7064-629">http://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-629">http://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.min.js</span></span>
- <span data-ttu-id="d7064-630">http://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.js</span><span class="sxs-lookup"><span data-stu-id="d7064-630">http://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.js</span></span>
- <span data-ttu-id="d7064-631">http://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-631">http://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.min.js</span></span>

#### <a name="respond-version-130"></a><span data-ttu-id="d7064-632">버전 1.3.0 응답</span><span class="sxs-lookup"><span data-stu-id="d7064-632">Respond version 1.3.0</span></span>

- <span data-ttu-id="d7064-633">http://ajax.aspnetcdn.com/ajax/respond/1.3.0/respond.js</span><span class="sxs-lookup"><span data-stu-id="d7064-633">http://ajax.aspnetcdn.com/ajax/respond/1.3.0/respond.js</span></span>

#### <a name="respond-version-120"></a><span data-ttu-id="d7064-634">버전 1.2.0 응답</span><span class="sxs-lookup"><span data-stu-id="d7064-634">Respond version 1.2.0</span></span>

- <span data-ttu-id="d7064-635">http://ajax.aspnetcdn.com/ajax/respond/1.2.0/respond.js</span><span class="sxs-lookup"><span data-stu-id="d7064-635">http://ajax.aspnetcdn.com/ajax/respond/1.2.0/respond.js</span></span>

<a id="Bootstrap_Releases_on_the_CDN_14"></a>

### <a name="bootstrap-releases-on-the-cdn"></a><span data-ttu-id="d7064-636">CDN에서 부트스트랩 릴리스</span><span class="sxs-lookup"><span data-stu-id="d7064-636">Bootstrap Releases on the CDN</span></span>

<span data-ttu-id="d7064-637">다음 릴리스의 [getbootstrap.com](http://getbootstrap.com "getbootstrap.com") 부트스트랩 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-637">The following releases of [getbootstrap.com](http://getbootstrap.com "getbootstrap.com") bootstrap are hosted on the CDN:</span></span>

#### <a name="bootstrap-version-337"></a><span data-ttu-id="d7064-638">3.3.7 부트스트랩 버전</span><span class="sxs-lookup"><span data-stu-id="d7064-638">Bootstrap version 3.3.7</span></span>

- <span data-ttu-id="d7064-639">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="d7064-639">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.js</span></span>
- <span data-ttu-id="d7064-640">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-640">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.min.js</span></span>
- <span data-ttu-id="d7064-641">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.css</span><span class="sxs-lookup"><span data-stu-id="d7064-641">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.css</span></span>
- <span data-ttu-id="d7064-642">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.css.map</span><span class="sxs-lookup"><span data-stu-id="d7064-642">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.css.map</span></span>
- <span data-ttu-id="d7064-643">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.min.css</span><span class="sxs-lookup"><span data-stu-id="d7064-643">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.min.css</span></span>
- <span data-ttu-id="d7064-644">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.css</span><span class="sxs-lookup"><span data-stu-id="d7064-644">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.css</span></span>
- <span data-ttu-id="d7064-645">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.css.map</span><span class="sxs-lookup"><span data-stu-id="d7064-645">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.css.map</span></span>
- <span data-ttu-id="d7064-646">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.min.css</span><span class="sxs-lookup"><span data-stu-id="d7064-646">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.min.css</span></span>
- <span data-ttu-id="d7064-647">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.eot</span><span class="sxs-lookup"><span data-stu-id="d7064-647">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.eot</span></span>
- <span data-ttu-id="d7064-648">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.svg</span><span class="sxs-lookup"><span data-stu-id="d7064-648">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.svg</span></span>
- <span data-ttu-id="d7064-649">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.ttf</span><span class="sxs-lookup"><span data-stu-id="d7064-649">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.ttf</span></span>
- <span data-ttu-id="d7064-650">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff</span><span class="sxs-lookup"><span data-stu-id="d7064-650">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff</span></span>
- <span data-ttu-id="d7064-651">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff2</span><span class="sxs-lookup"><span data-stu-id="d7064-651">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff2</span></span>

#### <a name="bootstrap-version-336"></a><span data-ttu-id="d7064-652">부트스트랩 버전 3.3.6</span><span class="sxs-lookup"><span data-stu-id="d7064-652">Bootstrap version 3.3.6</span></span>

- <span data-ttu-id="d7064-653">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="d7064-653">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/bootstrap.js</span></span>
- <span data-ttu-id="d7064-654">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/bootstrap.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-654">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/bootstrap.min.js</span></span>
- <span data-ttu-id="d7064-655">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.css</span><span class="sxs-lookup"><span data-stu-id="d7064-655">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.css</span></span>
- <span data-ttu-id="d7064-656">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.css.map</span><span class="sxs-lookup"><span data-stu-id="d7064-656">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.css.map</span></span>
- <span data-ttu-id="d7064-657">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.min.css</span><span class="sxs-lookup"><span data-stu-id="d7064-657">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.min.css</span></span>
- <span data-ttu-id="d7064-658">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.css</span><span class="sxs-lookup"><span data-stu-id="d7064-658">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.css</span></span>
- <span data-ttu-id="d7064-659">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.css.map</span><span class="sxs-lookup"><span data-stu-id="d7064-659">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.css.map</span></span>
- <span data-ttu-id="d7064-660">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.min.css</span><span class="sxs-lookup"><span data-stu-id="d7064-660">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.min.css</span></span>
- <span data-ttu-id="d7064-661">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.eot</span><span class="sxs-lookup"><span data-stu-id="d7064-661">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.eot</span></span>
- <span data-ttu-id="d7064-662">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.svg</span><span class="sxs-lookup"><span data-stu-id="d7064-662">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.svg</span></span>
- <span data-ttu-id="d7064-663">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.ttf</span><span class="sxs-lookup"><span data-stu-id="d7064-663">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.ttf</span></span>
- <span data-ttu-id="d7064-664">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.woff</span><span class="sxs-lookup"><span data-stu-id="d7064-664">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.woff</span></span>
- <span data-ttu-id="d7064-665">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.woff2</span><span class="sxs-lookup"><span data-stu-id="d7064-665">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.woff2</span></span>

#### <a name="bootstrap-version-335"></a><span data-ttu-id="d7064-666">부트스트랩 버전 3.3.5</span><span class="sxs-lookup"><span data-stu-id="d7064-666">Bootstrap version 3.3.5</span></span>

- <span data-ttu-id="d7064-667">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="d7064-667">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/bootstrap.js</span></span>
- <span data-ttu-id="d7064-668">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/bootstrap.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-668">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/bootstrap.min.js</span></span>
- <span data-ttu-id="d7064-669">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.css</span><span class="sxs-lookup"><span data-stu-id="d7064-669">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.css</span></span>
- <span data-ttu-id="d7064-670">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.css.map</span><span class="sxs-lookup"><span data-stu-id="d7064-670">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.css.map</span></span>
- <span data-ttu-id="d7064-671">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.min.css</span><span class="sxs-lookup"><span data-stu-id="d7064-671">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.min.css</span></span>
- <span data-ttu-id="d7064-672">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.css</span><span class="sxs-lookup"><span data-stu-id="d7064-672">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.css</span></span>
- <span data-ttu-id="d7064-673">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.css.map</span><span class="sxs-lookup"><span data-stu-id="d7064-673">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.css.map</span></span>
- <span data-ttu-id="d7064-674">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.min.css</span><span class="sxs-lookup"><span data-stu-id="d7064-674">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.min.css</span></span>
- <span data-ttu-id="d7064-675">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.eot</span><span class="sxs-lookup"><span data-stu-id="d7064-675">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.eot</span></span>
- <span data-ttu-id="d7064-676">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.svg</span><span class="sxs-lookup"><span data-stu-id="d7064-676">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.svg</span></span>
- <span data-ttu-id="d7064-677">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.ttf</span><span class="sxs-lookup"><span data-stu-id="d7064-677">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.ttf</span></span>
- <span data-ttu-id="d7064-678">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.woff</span><span class="sxs-lookup"><span data-stu-id="d7064-678">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.woff</span></span>
- <span data-ttu-id="d7064-679">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.woff2</span><span class="sxs-lookup"><span data-stu-id="d7064-679">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.woff2</span></span>

#### <a name="bootstrap-version-334"></a><span data-ttu-id="d7064-680">3.3.4 부트스트랩 버전</span><span class="sxs-lookup"><span data-stu-id="d7064-680">Bootstrap version 3.3.4</span></span>

- <span data-ttu-id="d7064-681">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="d7064-681">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.js</span></span>
- <span data-ttu-id="d7064-682">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-682">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.min.js</span></span>
- <span data-ttu-id="d7064-683">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.css</span><span class="sxs-lookup"><span data-stu-id="d7064-683">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.css</span></span>
- <span data-ttu-id="d7064-684">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.css.map</span><span class="sxs-lookup"><span data-stu-id="d7064-684">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.css.map</span></span>
- <span data-ttu-id="d7064-685">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.min.css</span><span class="sxs-lookup"><span data-stu-id="d7064-685">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.min.css</span></span>
- <span data-ttu-id="d7064-686">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.css</span><span class="sxs-lookup"><span data-stu-id="d7064-686">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.css</span></span>
- <span data-ttu-id="d7064-687">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.css.map</span><span class="sxs-lookup"><span data-stu-id="d7064-687">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.css.map</span></span>
- <span data-ttu-id="d7064-688">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.min.css</span><span class="sxs-lookup"><span data-stu-id="d7064-688">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.min.css</span></span>
- <span data-ttu-id="d7064-689">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.eot</span><span class="sxs-lookup"><span data-stu-id="d7064-689">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.eot</span></span>
- <span data-ttu-id="d7064-690">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.svg</span><span class="sxs-lookup"><span data-stu-id="d7064-690">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.svg</span></span>
- <span data-ttu-id="d7064-691">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.ttf</span><span class="sxs-lookup"><span data-stu-id="d7064-691">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.ttf</span></span>
- <span data-ttu-id="d7064-692">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.woff</span><span class="sxs-lookup"><span data-stu-id="d7064-692">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.woff</span></span>
- <span data-ttu-id="d7064-693">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.woff2</span><span class="sxs-lookup"><span data-stu-id="d7064-693">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.woff2</span></span>

#### <a name="bootstrap-version-332"></a><span data-ttu-id="d7064-694">3.3.2 부트스트랩 버전</span><span class="sxs-lookup"><span data-stu-id="d7064-694">Bootstrap version 3.3.2</span></span>

- <span data-ttu-id="d7064-695">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="d7064-695">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.js</span></span>
- <span data-ttu-id="d7064-696">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-696">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.min.js</span></span>
- <span data-ttu-id="d7064-697">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.css</span><span class="sxs-lookup"><span data-stu-id="d7064-697">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.css</span></span>
- <span data-ttu-id="d7064-698">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.css.map</span><span class="sxs-lookup"><span data-stu-id="d7064-698">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.css.map</span></span>
- <span data-ttu-id="d7064-699">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.min.css</span><span class="sxs-lookup"><span data-stu-id="d7064-699">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.min.css</span></span>
- <span data-ttu-id="d7064-700">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.css</span><span class="sxs-lookup"><span data-stu-id="d7064-700">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.css</span></span>
- <span data-ttu-id="d7064-701">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.css.map</span><span class="sxs-lookup"><span data-stu-id="d7064-701">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.css.map</span></span>
- <span data-ttu-id="d7064-702">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.min.css</span><span class="sxs-lookup"><span data-stu-id="d7064-702">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.min.css</span></span>
- <span data-ttu-id="d7064-703">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.eot</span><span class="sxs-lookup"><span data-stu-id="d7064-703">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.eot</span></span>
- <span data-ttu-id="d7064-704">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.svg</span><span class="sxs-lookup"><span data-stu-id="d7064-704">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.svg</span></span>
- <span data-ttu-id="d7064-705">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.ttf</span><span class="sxs-lookup"><span data-stu-id="d7064-705">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.ttf</span></span>
- <span data-ttu-id="d7064-706">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.woff</span><span class="sxs-lookup"><span data-stu-id="d7064-706">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.woff</span></span>
- <span data-ttu-id="d7064-707">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.woff2</span><span class="sxs-lookup"><span data-stu-id="d7064-707">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.woff2</span></span>

#### <a name="bootstrap-version-331"></a><span data-ttu-id="d7064-708">3.3.1 부트스트랩 버전</span><span class="sxs-lookup"><span data-stu-id="d7064-708">Bootstrap version 3.3.1</span></span>

- <span data-ttu-id="d7064-709">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="d7064-709">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/bootstrap.js</span></span>
- <span data-ttu-id="d7064-710">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/bootstrap.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-710">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/bootstrap.min.js</span></span>
- <span data-ttu-id="d7064-711">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.css</span><span class="sxs-lookup"><span data-stu-id="d7064-711">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.css</span></span>
- <span data-ttu-id="d7064-712">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.css.map</span><span class="sxs-lookup"><span data-stu-id="d7064-712">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.css.map</span></span>
- <span data-ttu-id="d7064-713">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.min.css</span><span class="sxs-lookup"><span data-stu-id="d7064-713">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.min.css</span></span>
- <span data-ttu-id="d7064-714">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.css</span><span class="sxs-lookup"><span data-stu-id="d7064-714">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.css</span></span>
- <span data-ttu-id="d7064-715">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.css.map</span><span class="sxs-lookup"><span data-stu-id="d7064-715">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.css.map</span></span>
- <span data-ttu-id="d7064-716">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.min.css</span><span class="sxs-lookup"><span data-stu-id="d7064-716">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.min.css</span></span>
- <span data-ttu-id="d7064-717">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.eot</span><span class="sxs-lookup"><span data-stu-id="d7064-717">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.eot</span></span>
- <span data-ttu-id="d7064-718">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.svg</span><span class="sxs-lookup"><span data-stu-id="d7064-718">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.svg</span></span>
- <span data-ttu-id="d7064-719">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.ttf</span><span class="sxs-lookup"><span data-stu-id="d7064-719">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.ttf</span></span>
- <span data-ttu-id="d7064-720">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.woff</span><span class="sxs-lookup"><span data-stu-id="d7064-720">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.woff</span></span>

#### <a name="bootstrap-version-330"></a><span data-ttu-id="d7064-721">부트스트랩 버전 3.3.0</span><span class="sxs-lookup"><span data-stu-id="d7064-721">Bootstrap version 3.3.0</span></span>

- <span data-ttu-id="d7064-722">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="d7064-722">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/bootstrap.js</span></span>
- <span data-ttu-id="d7064-723">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/bootstrap.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-723">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/bootstrap.min.js</span></span>
- <span data-ttu-id="d7064-724">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.css</span><span class="sxs-lookup"><span data-stu-id="d7064-724">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.css</span></span>
- <span data-ttu-id="d7064-725">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.css.map</span><span class="sxs-lookup"><span data-stu-id="d7064-725">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.css.map</span></span>
- <span data-ttu-id="d7064-726">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.min.css</span><span class="sxs-lookup"><span data-stu-id="d7064-726">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.min.css</span></span>
- <span data-ttu-id="d7064-727">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.css</span><span class="sxs-lookup"><span data-stu-id="d7064-727">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.css</span></span>
- <span data-ttu-id="d7064-728">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.css.map</span><span class="sxs-lookup"><span data-stu-id="d7064-728">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.css.map</span></span>
- <span data-ttu-id="d7064-729">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.min.css</span><span class="sxs-lookup"><span data-stu-id="d7064-729">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.min.css</span></span>
- <span data-ttu-id="d7064-730">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.eot</span><span class="sxs-lookup"><span data-stu-id="d7064-730">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.eot</span></span>
- <span data-ttu-id="d7064-731">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.svg</span><span class="sxs-lookup"><span data-stu-id="d7064-731">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.svg</span></span>
- <span data-ttu-id="d7064-732">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.ttf</span><span class="sxs-lookup"><span data-stu-id="d7064-732">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.ttf</span></span>
- <span data-ttu-id="d7064-733">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.woff</span><span class="sxs-lookup"><span data-stu-id="d7064-733">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.woff</span></span>

#### <a name="bootstrap-version-320"></a><span data-ttu-id="d7064-734">부트스트랩 버전 3.2.0</span><span class="sxs-lookup"><span data-stu-id="d7064-734">Bootstrap version 3.2.0</span></span>

- <span data-ttu-id="d7064-735">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="d7064-735">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.js</span></span>
- <span data-ttu-id="d7064-736">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-736">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js</span></span>
- <span data-ttu-id="d7064-737">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.css</span><span class="sxs-lookup"><span data-stu-id="d7064-737">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.css</span></span>
- <span data-ttu-id="d7064-738">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.css.map</span><span class="sxs-lookup"><span data-stu-id="d7064-738">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.css.map</span></span>
- <span data-ttu-id="d7064-739">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css</span><span class="sxs-lookup"><span data-stu-id="d7064-739">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css</span></span>
- <span data-ttu-id="d7064-740">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.css</span><span class="sxs-lookup"><span data-stu-id="d7064-740">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.css</span></span>
- <span data-ttu-id="d7064-741">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.css.map</span><span class="sxs-lookup"><span data-stu-id="d7064-741">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.css.map</span></span>
- <span data-ttu-id="d7064-742">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.min.css</span><span class="sxs-lookup"><span data-stu-id="d7064-742">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.min.css</span></span>
- <span data-ttu-id="d7064-743">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.eot</span><span class="sxs-lookup"><span data-stu-id="d7064-743">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.eot</span></span>
- <span data-ttu-id="d7064-744">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.svg</span><span class="sxs-lookup"><span data-stu-id="d7064-744">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.svg</span></span>
- <span data-ttu-id="d7064-745">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.ttf</span><span class="sxs-lookup"><span data-stu-id="d7064-745">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.ttf</span></span>
- <span data-ttu-id="d7064-746">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.woff</span><span class="sxs-lookup"><span data-stu-id="d7064-746">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.woff</span></span>

#### <a name="bootstrap-version-311"></a><span data-ttu-id="d7064-747">3.1.1 부트스트랩 버전</span><span class="sxs-lookup"><span data-stu-id="d7064-747">Bootstrap version 3.1.1</span></span>

- <span data-ttu-id="d7064-748">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="d7064-748">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/bootstrap.js</span></span>
- <span data-ttu-id="d7064-749">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/bootstrap.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-749">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/bootstrap.min.js</span></span>
- <span data-ttu-id="d7064-750">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.css</span><span class="sxs-lookup"><span data-stu-id="d7064-750">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.css</span></span>
- <span data-ttu-id="d7064-751">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.css.map</span><span class="sxs-lookup"><span data-stu-id="d7064-751">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.css.map</span></span>
- <span data-ttu-id="d7064-752">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.min.css</span><span class="sxs-lookup"><span data-stu-id="d7064-752">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.min.css</span></span>
- <span data-ttu-id="d7064-753">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.css</span><span class="sxs-lookup"><span data-stu-id="d7064-753">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.css</span></span>
- <span data-ttu-id="d7064-754">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.css.map</span><span class="sxs-lookup"><span data-stu-id="d7064-754">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.css.map</span></span>
- <span data-ttu-id="d7064-755">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.min.css</span><span class="sxs-lookup"><span data-stu-id="d7064-755">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.min.css</span></span>
- <span data-ttu-id="d7064-756">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.eot</span><span class="sxs-lookup"><span data-stu-id="d7064-756">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.eot</span></span>
- <span data-ttu-id="d7064-757">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.svg</span><span class="sxs-lookup"><span data-stu-id="d7064-757">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.svg</span></span>
- <span data-ttu-id="d7064-758">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.ttf</span><span class="sxs-lookup"><span data-stu-id="d7064-758">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.ttf</span></span>
- <span data-ttu-id="d7064-759">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.woff</span><span class="sxs-lookup"><span data-stu-id="d7064-759">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.woff</span></span>

#### <a name="bootstrap-version-310"></a><span data-ttu-id="d7064-760">부트스트랩 버전 3.1.0</span><span class="sxs-lookup"><span data-stu-id="d7064-760">Bootstrap version 3.1.0</span></span>

- <span data-ttu-id="d7064-761">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="d7064-761">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/bootstrap.js</span></span>
- <span data-ttu-id="d7064-762">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/bootstrap.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-762">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/bootstrap.min.js</span></span>
- <span data-ttu-id="d7064-763">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.css</span><span class="sxs-lookup"><span data-stu-id="d7064-763">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.css</span></span>
- <span data-ttu-id="d7064-764">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.css.map</span><span class="sxs-lookup"><span data-stu-id="d7064-764">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.css.map</span></span>
- <span data-ttu-id="d7064-765">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.min.css</span><span class="sxs-lookup"><span data-stu-id="d7064-765">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.min.css</span></span>
- <span data-ttu-id="d7064-766">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.css</span><span class="sxs-lookup"><span data-stu-id="d7064-766">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.css</span></span>
- <span data-ttu-id="d7064-767">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.css.map</span><span class="sxs-lookup"><span data-stu-id="d7064-767">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.css.map</span></span>
- <span data-ttu-id="d7064-768">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.min.css</span><span class="sxs-lookup"><span data-stu-id="d7064-768">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.min.css</span></span>
- <span data-ttu-id="d7064-769">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.eot</span><span class="sxs-lookup"><span data-stu-id="d7064-769">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.eot</span></span>
- <span data-ttu-id="d7064-770">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.svg</span><span class="sxs-lookup"><span data-stu-id="d7064-770">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.svg</span></span>
- <span data-ttu-id="d7064-771">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.ttf</span><span class="sxs-lookup"><span data-stu-id="d7064-771">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.ttf</span></span>
- <span data-ttu-id="d7064-772">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.woff</span><span class="sxs-lookup"><span data-stu-id="d7064-772">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.woff</span></span>

#### <a name="bootstrap-version-303"></a><span data-ttu-id="d7064-773">부트스트랩 버전 3.0.3</span><span class="sxs-lookup"><span data-stu-id="d7064-773">Bootstrap version 3.0.3</span></span>

- <span data-ttu-id="d7064-774">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="d7064-774">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/bootstrap.js</span></span>
- <span data-ttu-id="d7064-775">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/bootstrap.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-775">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/bootstrap.min.js</span></span>
- <span data-ttu-id="d7064-776">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap.css</span><span class="sxs-lookup"><span data-stu-id="d7064-776">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap.css</span></span>
- <span data-ttu-id="d7064-777">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap.min.css</span><span class="sxs-lookup"><span data-stu-id="d7064-777">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap.min.css</span></span>
- <span data-ttu-id="d7064-778">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap-theme.css</span><span class="sxs-lookup"><span data-stu-id="d7064-778">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap-theme.css</span></span>
- <span data-ttu-id="d7064-779">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap-theme.min.css</span><span class="sxs-lookup"><span data-stu-id="d7064-779">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap-theme.min.css</span></span>
- <span data-ttu-id="d7064-780">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.eot</span><span class="sxs-lookup"><span data-stu-id="d7064-780">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.eot</span></span>
- <span data-ttu-id="d7064-781">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.svg</span><span class="sxs-lookup"><span data-stu-id="d7064-781">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.svg</span></span>
- <span data-ttu-id="d7064-782">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.ttf</span><span class="sxs-lookup"><span data-stu-id="d7064-782">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.ttf</span></span>
- <span data-ttu-id="d7064-783">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.woff</span><span class="sxs-lookup"><span data-stu-id="d7064-783">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.woff</span></span>

#### <a name="bootstrap-version-302"></a><span data-ttu-id="d7064-784">부트스트랩 버전 3.0.2</span><span class="sxs-lookup"><span data-stu-id="d7064-784">Bootstrap version 3.0.2</span></span>

- <span data-ttu-id="d7064-785">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="d7064-785">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/bootstrap.js</span></span>
- <span data-ttu-id="d7064-786">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/bootstrap.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-786">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/bootstrap.min.js</span></span>
- <span data-ttu-id="d7064-787">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap.css</span><span class="sxs-lookup"><span data-stu-id="d7064-787">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap.css</span></span>
- <span data-ttu-id="d7064-788">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap.min.css</span><span class="sxs-lookup"><span data-stu-id="d7064-788">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap.min.css</span></span>
- <span data-ttu-id="d7064-789">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap-theme.css</span><span class="sxs-lookup"><span data-stu-id="d7064-789">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap-theme.css</span></span>
- <span data-ttu-id="d7064-790">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap-theme.min.css</span><span class="sxs-lookup"><span data-stu-id="d7064-790">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap-theme.min.css</span></span>
- <span data-ttu-id="d7064-791">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.eot</span><span class="sxs-lookup"><span data-stu-id="d7064-791">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.eot</span></span>
- <span data-ttu-id="d7064-792">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.svg</span><span class="sxs-lookup"><span data-stu-id="d7064-792">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.svg</span></span>
- <span data-ttu-id="d7064-793">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.ttf</span><span class="sxs-lookup"><span data-stu-id="d7064-793">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.ttf</span></span>
- <span data-ttu-id="d7064-794">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.woff</span><span class="sxs-lookup"><span data-stu-id="d7064-794">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.woff</span></span>

#### <a name="bootstrap-version-301"></a><span data-ttu-id="d7064-795">부트스트랩 버전 3.0.1</span><span class="sxs-lookup"><span data-stu-id="d7064-795">Bootstrap version 3.0.1</span></span>

- <span data-ttu-id="d7064-796">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="d7064-796">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/bootstrap.js</span></span>
- <span data-ttu-id="d7064-797">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/bootstrap.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-797">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/bootstrap.min.js</span></span>
- <span data-ttu-id="d7064-798">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap.css</span><span class="sxs-lookup"><span data-stu-id="d7064-798">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap.css</span></span>
- <span data-ttu-id="d7064-799">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap.min.css</span><span class="sxs-lookup"><span data-stu-id="d7064-799">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap.min.css</span></span>
- <span data-ttu-id="d7064-800">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap-theme.css</span><span class="sxs-lookup"><span data-stu-id="d7064-800">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap-theme.css</span></span>
- <span data-ttu-id="d7064-801">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap-theme.min.css</span><span class="sxs-lookup"><span data-stu-id="d7064-801">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap-theme.min.css</span></span>
- <span data-ttu-id="d7064-802">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.eot</span><span class="sxs-lookup"><span data-stu-id="d7064-802">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.eot</span></span>
- <span data-ttu-id="d7064-803">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.svg</span><span class="sxs-lookup"><span data-stu-id="d7064-803">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.svg</span></span>
- <span data-ttu-id="d7064-804">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.ttf</span><span class="sxs-lookup"><span data-stu-id="d7064-804">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.ttf</span></span>
- <span data-ttu-id="d7064-805">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.woff</span><span class="sxs-lookup"><span data-stu-id="d7064-805">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.woff</span></span>

#### <a name="bootstrap-version-300"></a><span data-ttu-id="d7064-806">부트스트랩 버전 3.0.0</span><span class="sxs-lookup"><span data-stu-id="d7064-806">Bootstrap version 3.0.0</span></span>

- <span data-ttu-id="d7064-807">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="d7064-807">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/bootstrap.js</span></span>
- <span data-ttu-id="d7064-808">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/bootstrap.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-808">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/bootstrap.min.js</span></span>
- <span data-ttu-id="d7064-809">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap.css</span><span class="sxs-lookup"><span data-stu-id="d7064-809">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap.css</span></span>
- <span data-ttu-id="d7064-810">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap.min.css</span><span class="sxs-lookup"><span data-stu-id="d7064-810">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap.min.css</span></span>
- <span data-ttu-id="d7064-811">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap-theme.css</span><span class="sxs-lookup"><span data-stu-id="d7064-811">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap-theme.css</span></span>
- <span data-ttu-id="d7064-812">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap-theme.min.css</span><span class="sxs-lookup"><span data-stu-id="d7064-812">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap-theme.min.css</span></span>
- <span data-ttu-id="d7064-813">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.eot</span><span class="sxs-lookup"><span data-stu-id="d7064-813">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.eot</span></span>
- <span data-ttu-id="d7064-814">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.svg</span><span class="sxs-lookup"><span data-stu-id="d7064-814">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.svg</span></span>
- <span data-ttu-id="d7064-815">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.ttf</span><span class="sxs-lookup"><span data-stu-id="d7064-815">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.ttf</span></span>
- <span data-ttu-id="d7064-816">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.woff</span><span class="sxs-lookup"><span data-stu-id="d7064-816">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.woff</span></span>

#### <a name="bootstrap-version-232"></a><span data-ttu-id="d7064-817">부트스트랩 버전 2.3.2</span><span class="sxs-lookup"><span data-stu-id="d7064-817">Bootstrap version 2.3.2</span></span>

- <span data-ttu-id="d7064-818">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="d7064-818">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.js</span></span>
- <span data-ttu-id="d7064-819">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-819">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.min.js</span></span>
- <span data-ttu-id="d7064-820">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.css</span><span class="sxs-lookup"><span data-stu-id="d7064-820">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.css</span></span>
- <span data-ttu-id="d7064-821">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.min.css</span><span class="sxs-lookup"><span data-stu-id="d7064-821">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.min.css</span></span>
- <span data-ttu-id="d7064-822">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.css</span><span class="sxs-lookup"><span data-stu-id="d7064-822">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.css</span></span>
- <span data-ttu-id="d7064-823">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.min.css</span><span class="sxs-lookup"><span data-stu-id="d7064-823">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.min.css</span></span>
- <span data-ttu-id="d7064-824">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings.png</span><span class="sxs-lookup"><span data-stu-id="d7064-824">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings.png</span></span>
- <span data-ttu-id="d7064-825">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings-white.png</span><span class="sxs-lookup"><span data-stu-id="d7064-825">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings-white.png</span></span>

#### <a name="bootstrap-version-231"></a><span data-ttu-id="d7064-826">부트스트랩 버전 2.3.1</span><span class="sxs-lookup"><span data-stu-id="d7064-826">Bootstrap version 2.3.1</span></span>

- <span data-ttu-id="d7064-827">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="d7064-827">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.js</span></span>
- <span data-ttu-id="d7064-828">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-828">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.min.js</span></span>
- <span data-ttu-id="d7064-829">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.css</span><span class="sxs-lookup"><span data-stu-id="d7064-829">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.css</span></span>
- <span data-ttu-id="d7064-830">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.min.css</span><span class="sxs-lookup"><span data-stu-id="d7064-830">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.min.css</span></span>
- <span data-ttu-id="d7064-831">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.css</span><span class="sxs-lookup"><span data-stu-id="d7064-831">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.css</span></span>
- <span data-ttu-id="d7064-832">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.min.css</span><span class="sxs-lookup"><span data-stu-id="d7064-832">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.min.css</span></span>
- <span data-ttu-id="d7064-833">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings.png</span><span class="sxs-lookup"><span data-stu-id="d7064-833">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings.png</span></span>
- <span data-ttu-id="d7064-834">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings-white.png</span><span class="sxs-lookup"><span data-stu-id="d7064-834">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings-white.png</span></span>

<a id="BootstrapTouchCarousel_Releases_on_the_CDN_18"></a>

### <a name="bootstrap-touchcarousel-releases-on-the-cdn"></a><span data-ttu-id="d7064-835">CDN에서 부트스트랩 TouchCarousel 릴리스</span><span class="sxs-lookup"><span data-stu-id="d7064-835">Bootstrap TouchCarousel Releases on the CDN</span></span>

<span data-ttu-id="d7064-836">다음 릴리스의 [https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel") 부트스트랩 TouchCarousel 릴리스 CDN에서 호스팅됩니다. :</span><span class="sxs-lookup"><span data-stu-id="d7064-836">The following releases of [https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel") Bootstrap TouchCarousel releases are hosted on the CDN:</span></span>

#### <a name="bootstrap-touchcarousel-version-080"></a><span data-ttu-id="d7064-837">부트스트랩 TouchCarousel 버전 0.8.0</span><span class="sxs-lookup"><span data-stu-id="d7064-837">Bootstrap TouchCarousel version 0.8.0</span></span>

- <span data-ttu-id="d7064-838">http://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/css/bootstrap-touch-carousel.css</span><span class="sxs-lookup"><span data-stu-id="d7064-838">http://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/css/bootstrap-touch-carousel.css</span></span>
- <span data-ttu-id="d7064-839">http://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/js/bootstrap-touch-carousel.js</span><span class="sxs-lookup"><span data-stu-id="d7064-839">http://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/js/bootstrap-touch-carousel.js</span></span>

<a id="Hammerjs_Releases_on_the_CDN_19"></a>

### <a name="hammerjs-releases-on-the-cdn"></a><span data-ttu-id="d7064-840">CDN에서 Hammer.js 릴리스</span><span class="sxs-lookup"><span data-stu-id="d7064-840">Hammer.js Releases on the CDN</span></span>

<span data-ttu-id="d7064-841">다음 버전의 [http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/") Hammer.js 릴리스 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-841">The following releases of [http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/") Hammer.js releases are hosted on the CDN:</span></span>

#### <a name="hammerjs-version-204"></a><span data-ttu-id="d7064-842">2.0.4 Hammer.js 버전</span><span class="sxs-lookup"><span data-stu-id="d7064-842">Hammer.js version 2.0.4</span></span>

- <span data-ttu-id="d7064-843">http://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.js</span><span class="sxs-lookup"><span data-stu-id="d7064-843">http://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.js</span></span>
- <span data-ttu-id="d7064-844">http://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-844">http://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.js</span></span>
- <span data-ttu-id="d7064-845">http://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.map</span><span class="sxs-lookup"><span data-stu-id="d7064-845">http://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.map</span></span>

<a id="ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15"></a>

### <a name="aspnet-web-forms-and-ajax-releases-on-the-cdn"></a><span data-ttu-id="d7064-846">ASP.NET Web Forms 및 CDN에서 Ajax 릴리스</span><span class="sxs-lookup"><span data-stu-id="d7064-846">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>

<span data-ttu-id="d7064-847">ASP.NET Ajax 라이브러리의 다음 릴리스에서 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-847">The following releases of the ASP.NET Ajax Library are hosted on the CDN.</span></span> <span data-ttu-id="d7064-848">파일의 실제 목록을 확인 하려면 각 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-848">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="d7064-849">ASP.NET Web Forms 및 Ajax 버전 4.5.2</span><span class="sxs-lookup"><span data-stu-id="d7064-849">ASP.NET Web Forms and Ajax version 4.5.2</span></span>](cdnajax452.md "ASP.NET Web Forms 및 Ajax 4.5.2")
- [<span data-ttu-id="d7064-850">ASP.NET Web Forms 및 Ajax 버전 4</span><span class="sxs-lookup"><span data-stu-id="d7064-850">ASP.NET Web Forms and Ajax version 4</span></span>](cdnajax4.md "ASP.NET Web Forms 및 Ajax 4")
- [<span data-ttu-id="d7064-851">ASP.NET Ajax 버전 3.5</span><span class="sxs-lookup"><span data-stu-id="d7064-851">ASP.NET Ajax version 3.5</span></span>](cdnajax35.md "ASP.NET Ajax 3.5")

<a id="ASPNET_MVC_Releases_on_the_CDN_16"></a>

### <a name="aspnet-mvc-releases-on-the-cdn"></a><span data-ttu-id="d7064-852">CDN에 ASP.NET MVC 릴리스</span><span class="sxs-lookup"><span data-stu-id="d7064-852">ASP.NET MVC Releases on the CDN</span></span>

<span data-ttu-id="d7064-853">다음 ASP.NET MVC JavaScript 파일이이 CDN에서 호스트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-853">The following ASP.NET MVC JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-mvc-523"></a><span data-ttu-id="d7064-854">ASP.NET MVC 5.2.3</span><span class="sxs-lookup"><span data-stu-id="d7064-854">ASP.NET MVC 5.2.3</span></span>

- <span data-ttu-id="d7064-855">http://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.js</span><span class="sxs-lookup"><span data-stu-id="d7064-855">http://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.js</span></span>
- <span data-ttu-id="d7064-856">http://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-856">http://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.min.js</span></span>

#### <a name="aspnet-mvc-51"></a><span data-ttu-id="d7064-857">ASP.NET MVC 5.1</span><span class="sxs-lookup"><span data-stu-id="d7064-857">ASP.NET MVC 5.1</span></span>

- <span data-ttu-id="d7064-858">http://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.js</span><span class="sxs-lookup"><span data-stu-id="d7064-858">http://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.js</span></span>
- <span data-ttu-id="d7064-859">http://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-859">http://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.min.js</span></span>

#### <a name="aspnet-mvc-50"></a><span data-ttu-id="d7064-860">ASP.NET MVC 5.0</span><span class="sxs-lookup"><span data-stu-id="d7064-860">ASP.NET MVC 5.0</span></span>

- <span data-ttu-id="d7064-861">http://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.js</span><span class="sxs-lookup"><span data-stu-id="d7064-861">http://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.js</span></span>
- <span data-ttu-id="d7064-862">http://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-862">http://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.min.js</span></span>

#### <a name="aspnet-mvc-40"></a><span data-ttu-id="d7064-863">ASP.NET MVC 4.0</span><span class="sxs-lookup"><span data-stu-id="d7064-863">ASP.NET MVC 4.0</span></span>

- <span data-ttu-id="d7064-864">http://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.js</span><span class="sxs-lookup"><span data-stu-id="d7064-864">http://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.js</span></span>
- <span data-ttu-id="d7064-865">http://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-865">http://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.min.js</span></span>

#### <a name="aspnet-mvc-30"></a><span data-ttu-id="d7064-866">ASP.NET MVC 3.0</span><span class="sxs-lookup"><span data-stu-id="d7064-866">ASP.NET MVC 3.0</span></span>

- <span data-ttu-id="d7064-867">http://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.js</span><span class="sxs-lookup"><span data-stu-id="d7064-867">http://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.js</span></span>
- <span data-ttu-id="d7064-868">http://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-868">http://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.min.js</span></span>
- <span data-ttu-id="d7064-869">http://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.js</span><span class="sxs-lookup"><span data-stu-id="d7064-869">http://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.js</span></span>
- <span data-ttu-id="d7064-870">http://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-870">http://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.min.js</span></span>
- <span data-ttu-id="d7064-871">http://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.js</span><span class="sxs-lookup"><span data-stu-id="d7064-871">http://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.js</span></span>
- <span data-ttu-id="d7064-872">http://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.debug.js</span><span class="sxs-lookup"><span data-stu-id="d7064-872">http://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.debug.js</span></span>

#### <a name="aspnet-mvc-20"></a><span data-ttu-id="d7064-873">ASP.NET MVC 2.0</span><span class="sxs-lookup"><span data-stu-id="d7064-873">ASP.NET MVC 2.0</span></span>

- <span data-ttu-id="d7064-874">http://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.js</span><span class="sxs-lookup"><span data-stu-id="d7064-874">http://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.js</span></span>
- <span data-ttu-id="d7064-875">http://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.debug.js</span><span class="sxs-lookup"><span data-stu-id="d7064-875">http://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.debug.js</span></span>

#### <a name="aspnet-mvc-10"></a><span data-ttu-id="d7064-876">ASP.NET MVC 1.0</span><span class="sxs-lookup"><span data-stu-id="d7064-876">ASP.NET MVC 1.0</span></span>

- <span data-ttu-id="d7064-877">http://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.js</span><span class="sxs-lookup"><span data-stu-id="d7064-877">http://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.js</span></span>
- <span data-ttu-id="d7064-878">http://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.debug.js</span><span class="sxs-lookup"><span data-stu-id="d7064-878">http://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.debug.js</span></span>

<a id="ASPNET_SignalR_Releases_on_the_CDN_17"></a>

### <a name="aspnet-signalr-releases-on-the-cdn"></a><span data-ttu-id="d7064-879">CDN에서 ASP.NET SignalR 해제</span><span class="sxs-lookup"><span data-stu-id="d7064-879">ASP.NET SignalR Releases on the CDN</span></span>

<span data-ttu-id="d7064-880">다음 ASP.NET SignalR JavaScript 파일이이 CDN에서 호스트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-880">The following ASP.NET SignalR JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-signalr-222"></a><span data-ttu-id="d7064-881">ASP.NET SignalR 2.2.2</span><span class="sxs-lookup"><span data-stu-id="d7064-881">ASP.NET SignalR 2.2.2</span></span>

- <span data-ttu-id="d7064-882">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-882">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.min.js</span></span>
- <span data-ttu-id="d7064-883">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.js</span><span class="sxs-lookup"><span data-stu-id="d7064-883">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.js</span></span>

#### <a name="aspnet-signalr-221"></a><span data-ttu-id="d7064-884">ASP.NET SignalR 2.2.1</span><span class="sxs-lookup"><span data-stu-id="d7064-884">ASP.NET SignalR 2.2.1</span></span>

- <span data-ttu-id="d7064-885">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-885">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.min.js</span></span>
- <span data-ttu-id="d7064-886">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.js</span><span class="sxs-lookup"><span data-stu-id="d7064-886">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.js</span></span>

#### <a name="aspnet-signalr-220"></a><span data-ttu-id="d7064-887">ASP.NET SignalR 2.2.0</span><span class="sxs-lookup"><span data-stu-id="d7064-887">ASP.NET SignalR 2.2.0</span></span>

- <span data-ttu-id="d7064-888">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-888">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.min.js</span></span>
- <span data-ttu-id="d7064-889">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.js</span><span class="sxs-lookup"><span data-stu-id="d7064-889">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.js</span></span>

#### <a name="aspnet-signalr-210"></a><span data-ttu-id="d7064-890">ASP.NET SignalR 2.1.0</span><span class="sxs-lookup"><span data-stu-id="d7064-890">ASP.NET SignalR 2.1.0</span></span>

- <span data-ttu-id="d7064-891">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-891">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.min.js</span></span>
- <span data-ttu-id="d7064-892">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.js</span><span class="sxs-lookup"><span data-stu-id="d7064-892">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.js</span></span>

#### <a name="aspnet-signalr-203"></a><span data-ttu-id="d7064-893">ASP.NET SignalR 2.0.3</span><span class="sxs-lookup"><span data-stu-id="d7064-893">ASP.NET SignalR 2.0.3</span></span>

- <span data-ttu-id="d7064-894">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-894">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.min.js</span></span>
- <span data-ttu-id="d7064-895">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.js</span><span class="sxs-lookup"><span data-stu-id="d7064-895">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.js</span></span>

#### <a name="aspnet-signalr-202"></a><span data-ttu-id="d7064-896">ASP.NET SignalR 2.0.2</span><span class="sxs-lookup"><span data-stu-id="d7064-896">ASP.NET SignalR 2.0.2</span></span>

- <span data-ttu-id="d7064-897">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-897">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.min.js</span></span>
- <span data-ttu-id="d7064-898">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.js</span><span class="sxs-lookup"><span data-stu-id="d7064-898">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.js</span></span>

#### <a name="aspnet-signalr-201"></a><span data-ttu-id="d7064-899">ASP.NET SignalR 2.0.1</span><span class="sxs-lookup"><span data-stu-id="d7064-899">ASP.NET SignalR 2.0.1</span></span>

- <span data-ttu-id="d7064-900">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-900">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.min.js</span></span>
- <span data-ttu-id="d7064-901">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.js</span><span class="sxs-lookup"><span data-stu-id="d7064-901">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.js</span></span>

#### <a name="aspnet-signalr-200"></a><span data-ttu-id="d7064-902">ASP.NET SignalR 2.0.0</span><span class="sxs-lookup"><span data-stu-id="d7064-902">ASP.NET SignalR 2.0.0</span></span>

- <span data-ttu-id="d7064-903">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-903">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.min.js</span></span>
- <span data-ttu-id="d7064-904">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.js</span><span class="sxs-lookup"><span data-stu-id="d7064-904">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.js</span></span>

#### <a name="aspnet-signalr-113"></a><span data-ttu-id="d7064-905">ASP.NET SignalR 1.1.3</span><span class="sxs-lookup"><span data-stu-id="d7064-905">ASP.NET SignalR 1.1.3</span></span>

- <span data-ttu-id="d7064-906">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-906">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.min.js</span></span>
- <span data-ttu-id="d7064-907">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.js</span><span class="sxs-lookup"><span data-stu-id="d7064-907">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.js</span></span>

#### <a name="aspnet-signalr-112"></a><span data-ttu-id="d7064-908">ASP.NET SignalR 1.1.2</span><span class="sxs-lookup"><span data-stu-id="d7064-908">ASP.NET SignalR 1.1.2</span></span>

- <span data-ttu-id="d7064-909">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-909">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.min.js</span></span>
- <span data-ttu-id="d7064-910">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.js</span><span class="sxs-lookup"><span data-stu-id="d7064-910">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.js</span></span>

#### <a name="aspnet-signalr-111"></a><span data-ttu-id="d7064-911">ASP.NET SignalR 1.1.1</span><span class="sxs-lookup"><span data-stu-id="d7064-911">ASP.NET SignalR 1.1.1</span></span>

- <span data-ttu-id="d7064-912">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-912">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.min.js</span></span>
- <span data-ttu-id="d7064-913">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.js</span><span class="sxs-lookup"><span data-stu-id="d7064-913">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.js</span></span>

#### <a name="aspnet-signalr-110"></a><span data-ttu-id="d7064-914">ASP.NET SignalR 1.1.0</span><span class="sxs-lookup"><span data-stu-id="d7064-914">ASP.NET SignalR 1.1.0</span></span>

- <span data-ttu-id="d7064-915">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-915">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.min.js</span></span>
- <span data-ttu-id="d7064-916">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.js</span><span class="sxs-lookup"><span data-stu-id="d7064-916">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.js</span></span>

#### <a name="aspnet-signalr-101"></a><span data-ttu-id="d7064-917">ASP.NET SignalR 1.0.1</span><span class="sxs-lookup"><span data-stu-id="d7064-917">ASP.NET SignalR 1.0.1</span></span>

- <span data-ttu-id="d7064-918">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.min.js</span><span class="sxs-lookup"><span data-stu-id="d7064-918">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.min.js</span></span>
- <span data-ttu-id="d7064-919">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.js</span><span class="sxs-lookup"><span data-stu-id="d7064-919">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.js</span></span>

<span data-ttu-id="d7064-920">CDN에 대 한 사용 조건에 대 한 정보를 참조 하십시오. [Microsoft Ajax CDN 사용 약관](https://www.asp.net/terms-of-use "Microsoft Ajax CDN 사용 약관")합니다.</span><span class="sxs-lookup"><span data-stu-id="d7064-920">For information about the terms of use for the CDN, see [Microsoft Ajax CDN Terms of Use](https://www.asp.net/terms-of-use "Microsoft Ajax CDN Terms of Use").</span></span>
