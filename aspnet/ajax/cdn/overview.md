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
<a name="microsoft-ajax-content-delivery-network"></a>Microsoft Ajax 콘텐츠 배달 네트워크
====================
참고: Microsoft Ajax CDN에 Azure CDN을 사용 하 여 보다 많은 SLA는 없습니다.

## <a name="table-of-contents"></a>목차

**[ajax.microsoft.com ajax.aspnetcdn.com로 변경](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**  
**[Visual Studio .vsdoc Support](#Visual_Studio_vsdoc_Support_19)**  
**[ASP.NET Ajax CDN에서 사용 하 여](#Using_ASPNET_Ajax_from_the_CDN_20)**  
**[CDN에서 jQuery를 사용 하 여](#Using_jQuery_from_the_CDN_21)**  
**[JQuery UI에서 CDN 사용 하 여](#Using_jQuery_UI_from_the_CDN_22)**  
**[CDN에서 제 3 자 파일](#Third-Party_Files_on_the_CDN_23)**  
  
 [CDN에서 jQuery 릴리스](#jQuery_Releases_on_the_CDN_0)  
 [CDN에서 jQuery 마이그레이션할 릴리스](#jQuery_Migrate_Releases_on_the_CDN_1)  
 [jQuery UI CDN에 있는 릴리스](#jQuery_UI_Releases_on_the_CDN_2)  
 [jQuery 유효성 검사는 CDN에 있는 릴리스](#jQuery_Validation_Releases_on_the_CDN_3)  
 [jQuery Mobile CDN에 있는 릴리스](#jQuery_Mobile_Releases_on_the_CDN_4)  
 [jQuery CDN에서 템플릿 릴리스](#jQuery_Templates_Releases_on_the_CDN_5)  
 [jQuery CDN에서 주기 릴리스](#jQuery_Cycle_Releases_on_the_CDN_6)  
 [jQuery CDN에서 DataTables 릴리스](#jQuery_DataTables_Releases_on_the_CDN_7)  
 [CDN에서 Modernizr 릴리스](#Modernizr_Releases_on_the_CDN_8)  
 [CDN에서 JSHint 릴리스](#JSHint_Releases_on_the_CDN_10)  
 [CDN에서 knockout 릴리스](#Knockout_Releases_on_the_CDN_11)  
 [CDN에서 릴리스 전역화](#Globalize_Releases_on_the_CDN_12)  
 [CDN에서 릴리스 응답](#Respond_Releases_on_the_CDN_13)  
 [CDN에서 부트스트랩 릴리스](#Bootstrap_Releases_on_the_CDN_14)  
 [CDN에서 부트스트랩 TouchCarousel 릴리스](#BootstrapTouchCarousel_Releases_on_the_CDN_18)  
 [CDN에서 Hammer.js 릴리스](#Hammerjs_Releases_on_the_CDN_19)  
 [ASP.NET Web Forms 및 CDN에서 Ajax 릴리스](#ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15)  
 [CDN에 ASP.NET MVC 릴리스](#ASPNET_MVC_Releases_on_the_CDN_16)  
 [CDN에서 ASP.NET SignalR 해제](#ASPNET_SignalR_Releases_on_the_CDN_17)

Microsoft Ajax 콘텐츠 배달 네트워크 (CDN) jQuery와 같은 인기 있는 제 3 자 JavaScript 라이브러리를 호스팅하고 웹 응용 프로그램에를 쉽게 추가할 수 있습니다. 이 CDN에서 호스팅되는 jQuery를 사용 하 여 추가 하 여 시작할 수는 예를 들어 한 &lt;스크립트&gt; ajax.aspnetcdn.com 가리키는 페이지에는 태그입니다.

CDN 활용 하기 위해, Ajax 응용 프로그램의 성능을 크게 향상 시킬 수 있습니다. CDN의 콘텐츠는 세계에 있는 서버에 캐시 됩니다. 또한 CDN에는 브라우저 서로 다른 도메인에 있는 웹 사이트에 대 한 캐시 된 제 3 자 JavaScript 파일을 다시 사용할 수 있도록 설정 합니다.

CDN은 Secure Sockets Layer를 사용 하 여 웹 페이지를 처리 해야 하는 경우 SSL (HTTPS)을 지원 합니다.

CDN 업로드 된 및 해당 라이브러리의 소유자가 사용자에 게 사용이 허가 하는 다음 제 3 자 스크립트 라이브러리를 호스트 합니다.

- jQuery (www.jquery.com)
- jQuery UI (www.jqueryui.com)
- jQuery Mobile (www.jquerymobile.com)
- jQuery 유효성 검사 (www.jquery.com)
- jQuery 주기 (www.malsup.com/jquery/cycle/)
- jQuery Datatable 드 (http://datatables.net/)

Microsoft Ajax CDN는 Microsoft에서 업로드 한 다음 라이브러리를도 포함 되어 있습니다.

- ASP.NET Ajax
- ASP.NET MVC JavaScript 파일
- ASP.NET SignalR JavaScript 파일

Microsoft는이 CDN에서 호스팅되는 모든 타사 라이브러리의 소유권을 주장 하지 않습니다. 저작권 소유자는 라이브러리에 이러한 라이브러리를 라이선스 됩니다. 해당 저작권 소유자가 단독으로 다운로드 하 고 이러한 라이브러리를 사용 해야 할 수 있는 모든 권한이 부여 됩니다. 이들은 Microsoft 라이브러리 Microsoft 지적 재산권 권한 라이선스 (묵시적된 특허 권한이 없음 포함) 없음이나 보증을이 CDN에서 호스트 되는 타사 라이브러리에 대 한 제공 합니다.

JavaScript 라이브러리를 제출 하려면이 고 라이브러리에는 상위 JavaScript 라이브러리 중 하나 (에 나열 된 http://trends.builtwith.com) 또는 확장/플러그 인을 이러한 라이브러리는 (a) 인기 있는; 또는 (b) 유용한 ASP.NET에서 사용 하기 위해 다음에 게 문의 하십시오 AjaxCDNSubmission@Microsoft.com합니다.

<a id="ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18"></a>

## <a name="ajaxmicrosoftcom-renamed-to-ajaxaspnetcdncom"></a>ajax.microsoft.com ajax.aspnetcdn.com로 변경

CDN은 microsoft.com 도메인 이름을 사용 하는 데 사용 하 고 aspnetcdn.com 도메인 이름을 사용 하도록 변경 되었습니다. 각 요청과 함께 네트워크를 통해 모든 쿠키를 보내야 해당 도메인에서 했기 브라우저 microsoft.com 도메인을 참조 하기 때문에 성능을 향상 시키기 위해이 변경 되었습니다. Microsoft.com 이외의 도메인 이름으로 바꾸어 25%로 많은 성능으로 증가할 수 있습니다. 참고 ajax.microsoft.com은 계속 작동 하지만 ajax.aspnetcdn.com를 사용 하는 것이 좋습니다.

- 이전 형식: http://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js
- 새 형식: http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js

<a id="Visual_Studio_vsdoc_Support_19"></a>

## <a name="visual-studio-vsdoc-support"></a>Visual Studio.vsdoc 지원

Visual Studio 2008 및 2008 s p 1이 있는지 확인 해야 할.vsdoc 파일을 제대로 사용 하려면 설치 하 고 vsdoc 파일에 대 한 핫픽스를 설치 합니다. 여기에서 얻을 수 있습니다.

- [Visual Studio 2008 s p 1을 다운로드](https://www.microsoft.com/downloads/en/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en "Visual Studio 2008 s p 1을 다운로드 합니다.")
- [Visual Studio 2008 s p 1에 대 한.vsdoc 핫픽스 다운로드](https://code.msdn.microsoft.com/KB958502/Release/ProjectReleases.aspx?ReleaseId=1736 "Visual Studio 2008 s p 1에 대 한.vsdoc 핫픽스 다운로드")

Visual Studio 2010 추가 패치 없이.vsdoc 파일을 지원합니다.

<a id="Using_ASPNET_Ajax_from_the_CDN_20"></a>

## <a name="using-aspnet-ajax-from-the-cdn"></a>ASP.NET Ajax CDN에서 사용 하 여

ASP.NET 4를 사용 하는 경우 cdn ASP.NET framework 스크립트에 대 한 모든 요청을 리디렉션할 수 있습니다. 로컬 웹 서버 대신 CDN에서 스크립트 검색 공용 ASP.NET 웹 사이트의 성능을 상당히 개선 될 수 있습니다.

ScriptManager EnableCDN 속성을 사용 하 여 모든 요청을 리디렉션할 ASP.NET 프레임 워크 스크립트 Microsoft Ajax CDN에:

[!code-aspx[Main](overview/samples/sample1.aspx)]

<a id="Using_jQuery_from_the_CDN_21"></a>

## <a name="using-jquery-from-the-cdn"></a>CDN에서 jQuery를 사용 하 여

페이지에는 다음 스크립트 요소를 추가 하 여 CDN에서 웹 응용 프로그램에서 호스팅되는 jQuery 스크립트를 사용할 수 있습니다.

[!code-html[Main](overview/samples/sample2.html)]

CDN에 액세스할 수 있는 jQuery 스크립트의 축소 된 버전도 포함 됩니다는 다음 요소를 사용 하 여:

[!code-html[Main](overview/samples/sample3.html)]

대체 인증 CDN를 사용할 수 없는 경우 자신의 웹 사이트에 로컬 경로에서 jQuery를 로드 하려면 페이지를 허용 하려면 CDN 참조 요소 바로 뒤 다음 요소를 추가 합니다.

[!code-html[Main](overview/samples/sample4.html)]

다음 샘플 페이지 CDN 버전 (로컬 복사본으로 대체) 사용 하 여 jQuery 라이브러리의를 사용 하 여는 단추를 클릭할 때 div 요소 내용을 표시 합니다.

[!code-html[Main](overview/samples/sample5.html)]

JQuery에 대 한 자세한 정보 및 방문 하 여 jQuery의 로컬 복사본을 다운로드할 수 있습니다는 [jQuery](http://jquery.com/) 웹 사이트입니다.

<a id="Using_jQuery_UI_from_the_CDN_22"></a>

## <a name="using-jquery-ui-from-the-cdn"></a>JQuery UI에서 CDN 사용 하 여

또한 CDN jQuery UI 라이브러리를 호스트합니다. JQuery UI 라이브러리는 다양 한 위젯 및 ASP.NET 응용 프로그램에서 사용할 수 있는 효과 포함 합니다. 예를 들어 다음 페이지는 ASP.NET Web Forms 응용 프로그램의 컨텍스트에서 jQuery UI Datepicker 팝업 달력이 표시를 사용 하는 방법을 보여 줍니다.

[!code-aspx[Main](overview/samples/sample6.aspx)]

키보드를 사용 하 여 텍스트 상자에 포커스를 이동 하면 달력이 표시 됩니다.

![만든 Datepicker 팝업 일정](overview/_static/image1.png)

위의 코드에서 CDN에서 3 개의 파일을 포함 해야 하는 사항을 참고 하십시오.

- JQuery 라이브러리 &mdash; jQuery UI 라이브러리는 jQuery 라이브러리에 따라 달라 집니다. JQuery 라이브러리 jQuery UI 라이브러리를 추가 하기 전에 페이지에 추가 해야 합니다.
- JQuery UI 라이브러리 &mdash; jQuery UI 라이브러리 모든 위의 페이지에 사용 된 Datepicker 위젯 같은 위젯 및 jQuery UI 효과 포함 합니다.
- JQuery UI 테마 &mdash; jQuery UI 다양 한 테마를 지원 합니다. 위의 페이지 Redmond 테마 가져올 CSS 파일에 대 한 링크를 포함 합니다.

모든 표준 jQuery UI 테마는 CDN에서 호스팅됩니다. [이 페이지를 방문](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 Microsoft Ajax CDN에서") 각 테마에 대 한 축소판 그림을 볼 수 있습니다.

JQuery UI 라이브러리에 대 한 자세한 내용은 방문 공식 [jQuery UI 웹 사이트](http://jQueryUI.com "jQuery UI 웹 사이트")합니다.

<a id="Third-Party_Files_on_the_CDN_23"></a>

## <a name="third-party-files-on-the-cdn"></a>CDN에서 제 3 자 파일

CDN은 가장 일반적인 제 3 자 JavaScript 라이브러리 중 일부를 호스팅합니다. Microsoft는이 CDN에서 호스팅되는 모든 타사 라이브러리의 소유권을 주장 하지 않습니다. 저작권 소유자는 라이브러리에 이러한 라이브러리를 라이선스 됩니다. 해당 저작권 소유자가 단독으로 다운로드 하 고 이러한 라이브러리를 사용 해야 할 수 있는 모든 권한이 부여 됩니다. 이들은 Microsoft 라이브러리 Microsoft 지적 재산권 권한 라이선스 (묵시적된 특허 권한이 없음 포함) 없음이나 보증을이 CDN에서 호스트 되는 타사 라이브러리에 대 한 제공 합니다.

<a id="jQuery_Releases_on_the_CDN_0"></a>

### <a name="jquery-releases-on-the-cdn"></a>CDN에서 jQuery 릴리스

다음 버전의 jQuery CDN에서 호스팅됩니다.

#### <a name="jquery-version-331"></a>3.3.1 jQuery 버전
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.map
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.map

#### <a name="jquery-version-321"></a>jQuery 버전 3.2.1
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.map
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.map

#### <a name="jquery-version-320"></a>jQuery 버전 3.2.0

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.map
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.map

#### <a name="jquery-version-311"></a>3.1.1 jQuery 버전

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.map
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.map

#### <a name="jquery-version-310"></a>jQuery 버전 3.1.0

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.map
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.map

#### <a name="jquery-version-300"></a>jQuery 버전 3.0.0

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.map
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.map

#### <a name="jquery-version-224"></a>jQuery 버전 2.2.4

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.map

#### <a name="jquery-version-223"></a>jQuery 버전 2.2.3

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.map

#### <a name="jquery-version-222"></a>jQuery 버전 2.2.2

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.map

#### <a name="jquery-version-221"></a>jQuery 버전 2.2.1

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.map

#### <a name="jquery-version-220"></a>jQuery 버전 2.2.0

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.map

#### <a name="jquery-version-214"></a>jQuery 버전 2.1.4

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.map

#### <a name="jquery-version-213"></a>jQuery 버전 2.1.3

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.map

#### <a name="jquery-version-212"></a>jQuery 버전 2.1.2

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.min.js

#### <a name="jquery-version-211"></a>jQuery 버전 2.1.1

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.map

#### <a name="jquery-version-210"></a>jQuery 버전 2.1.0

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0-vsdoc.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.map

#### <a name="jquery-version-203"></a>jQuery 버전 2.0.3

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3-vsdoc.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.map

#### <a name="jquery-version-202"></a>jQuery 버전 2.0.2

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2-vsdoc.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.map

#### <a name="jquery-version-201"></a>jQuery 버전 2.0.1

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1-vsdoc.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.map

#### <a name="jquery-version-200"></a>jQuery 버전 2.0.0

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0-vsdoc.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.map

#### <a name="jquery-version-1124"></a>jQuery 버전 1.12.4

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.map

#### <a name="jquery-version-1123"></a>jQuery 버전 1.12.3

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.map

#### <a name="jquery-version-1122"></a>jQuery 버전 1.12.2

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.map

#### <a name="jquery-version-1121"></a>jQuery 버전 1.12.1

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.map

#### <a name="jquery-version-1120"></a>jQuery 버전 1.12.0

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.map

#### <a name="jquery-version-1113"></a>jQuery 버전 1.11.3

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.map

#### <a name="jquery-version-1112"></a>jQuery 버전 1.11.2

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.map

#### <a name="jquery-version-1111"></a>jQuery 버전 1.11.1

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.map

#### <a name="jquery-version-1110"></a>jQuery 버전 1.11.0

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0-vsdoc.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.map

#### <a name="jquery-version-1102"></a>jQuery 1.10.2 버전

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2-vsdoc.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.map

#### <a name="jquery-version-1101"></a>jQuery 버전 1.10.1

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1-vsdoc.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.map

#### <a name="jquery-version-1100"></a>jQuery 버전 1.10.0

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0-vsdoc.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.map

#### <a name="jquery-version-191"></a>jQuery 버전 1.9.1

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1-vsdoc.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.map

#### <a name="jquery-version-190"></a>1.9.0 jQuery 버전

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0-vsdoc.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.map

#### <a name="jquery-version-183"></a>1.8.3 jQuery 버전

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3-vsdoc.js

#### <a name="jquery-version-182"></a>1.8.2 jQuery 버전

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2-vsdoc.js

#### <a name="jquery-version-181"></a>1.8.1 jQuery 버전

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1-vsdoc.js

#### <a name="jquery-version-180"></a>jQuery 버전 1.8.0

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0-vsdoc.js

#### <a name="jquery-version-172"></a>1.7.2 jQuery 버전

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js

#### <a name="jquery-version-171"></a>jQuery 버전 1.7.1

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1-vsdoc.js

#### <a name="jquery-version-17"></a>jQuery 버전 1.7

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7-vsdoc.js

#### <a name="jquery-version-164"></a>jQuery 버전 1.6.4

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4-vsdoc.js

#### <a name="jquery-version-163"></a>jQuery 버전 1.6.3

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3-vsdoc.js

#### <a name="jquery-version-162"></a>jQuery 버전 1.6.2

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2-vsdoc.js

#### <a name="jquery-version-161"></a>jQuery 버전 1.6.1

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1-vsdoc.js

#### <a name="jquery-version-16"></a>jQuery 버전 1.6

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6-vsdoc.js

#### <a name="jquery-version-152"></a>1.5.2 jQuery 버전

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2-vsdoc.js

#### <a name="jquery-version-151"></a>1.5.1 jQuery 버전

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1-vsdoc.js

#### <a name="jquery-version-15"></a>jQuery 버전 1.5

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5-vsdoc.js

#### <a name="jquery-version-144"></a>jQuery 버전 1.4.4

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4-vsdoc.js

#### <a name="jquery-version-143"></a>jQuery 버전 1.4.3

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3-vsdoc.js

#### <a name="jquery-version-142"></a>1.4.2 jQuery 버전

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2-vsdoc.js

#### <a name="jquery-version-141"></a>1.4.1 jQuery 버전

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1-vsdoc.js

#### <a name="jquery-version-14"></a>jQuery 버전 1.4

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.min.js

#### <a name="jquery-version-132"></a>1.3.2 jQuery 버전

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2-vsdoc.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min-vsdoc.js

<a id="jQuery_Migrate_Releases_on_the_CDN_1"></a>

### <a name="jquery-migrate-releases-on-the-cdn"></a>CDN에서 jQuery 마이그레이션할 릴리스

다음 버전의 jQuery 마이그레이션 CDN에 호스팅됩니다.

#### <a name="jquery-migrate-version-300"></a>jQuery 버전 3.0.0 마이그레이션

- http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.js
- http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.min.js

#### <a name="jquery-migrate-version-121"></a>jQuery 버전 1.2.1 마이그레이션

- http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.js
- http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.min.js

jQuery 버전 1.2.0 마이그레이션

- http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.js
- http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.min.js

#### <a name="jquery-migrate-version-111"></a>jQuery 버전 1.1.1 마이그레이션

- http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.js
- http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.min.js

#### <a name="jquery-migrate-version-110"></a>jQuery 버전 1.1.0 마이그레이션

- http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.js
- http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.min.js

#### <a name="jquery-migrate-version-100"></a>jQuery 버전 1.0.0 마이그레이션

- http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.js
- http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.min.js

<a id="jQuery_UI_Releases_on_the_CDN_2"></a>

### <a name="jquery-ui-releases-on-the-cdn"></a>jQuery UI CDN에 있는 릴리스

JQuery UI 라이브러리의 다음 릴리스에서이 CDN에서 호스팅됩니다. 파일의 실제 목록을 확인 하려면 각 링크를 클릭 합니다.

- [jQuery UI 1.12.1](jquery-ui/cdnjqueryui1121.md "jQuery UI 1.12.1 Microsoft Ajax CDN에서")
- [jQuery UI 1.12.0](jquery-ui/cdnjqueryui1120.md "jQuery UI 1.12.0 Microsoft Ajax CDN에서")
- [jQuery UI 1.11.4](jquery-ui/cdnjqueryui1114.md "jQuery UI 1.11.4 Microsoft Ajax CDN에서")
- [jQuery UI 1.11.3](jquery-ui/cdnjqueryui1113.md "jQuery UI 1.11.3 Microsoft Ajax CDN에서")
- [jQuery UI 1.11.2](jquery-ui/cdnjqueryui1112.md "jQuery UI 1.11.2 Microsoft Ajax CDN에서")
- [jQuery UI 1.11.1](jquery-ui/cdnjqueryui1111.md "jQuery UI 1.11.1 Microsoft Ajax CDN에서")
- [jQuery UI 1.11.0](jquery-ui/cdnjqueryui1110.md "jQuery UI 1.11.0 Microsoft Ajax CDN에서")
- [jQuery UI 1.10.4](jquery-ui/cdnjqueryui1104.md "jQuery UI 1.10.4 Microsoft Ajax CDN에서")
- [jQuery UI 1.10.3](jquery-ui/cdnjqueryui1103.md "jQuery UI 1.10.3 Microsoft Ajax CDN에서")
- [jQuery 1.10.2 UI](jquery-ui/cdnjqueryui1102.md "jQuery 1.10.2 Microsoft Ajax CDN에서 UI")
- [jQuery UI 1.10.1](jquery-ui/cdnjqueryui1101.md "jQuery UI 1.10.1 Microsoft Ajax CDN에서")
- [jQuery UI 1.10.0](jquery-ui/cdnjqueryui1100.md "jQuery UI 1.10.0 Microsoft Ajax CDN에서")
- [jQuery UI 1.9.2](jquery-ui/cdnjqueryui192.md "jQuery UI 1.9.2 Microsoft Ajax CDN에서")
- [jQuery UI 1.9.1](jquery-ui/cdnjqueryui191.md "jQuery UI 1.9.1 Microsoft Ajax CDN에서")
- [jQuery UI 1.9.0](jquery-ui/cdnjqueryui190.md "jQuery UI 1.9.0 Microsoft Ajax CDN에서")
- [jQuery UI 1.8.24](jquery-ui/cdnjqueryui1824.md "jQuery UI 1.8.24 Microsoft Ajax CDN에서")
- [jQuery UI 1.8.23](jquery-ui/cdnjqueryui1823.md "jQuery UI 1.8.23 Microsoft Ajax CDN에서")
- [jQuery UI 1.8.22](jquery-ui/cdnjqueryui1822.md "jQuery UI 1.8.22 Microsoft Ajax CDN에서")
- [jQuery UI 1.8.21](jquery-ui/cdnjqueryui1821.md "jQuery UI 1.8.21 Microsoft Ajax CDN에서")
- [jQuery UI 1.8.20](jquery-ui/cdnjqueryui1820.md "jQuery UI 1.8.20 Microsoft Ajax CDN에서")
- [jQuery UI 1.8.19](jquery-ui/cdnjqueryui1819.md "jQuery UI 1.8.19 Microsoft Ajax CDN에서")
- [jQuery UI 1.8.18](jquery-ui/cdnjqueryui1818.md "jQuery UI 1.8.18 Microsoft Ajax CDN에서")
- [jQuery UI 1.8.17](jquery-ui/cdnjqueryui1817.md "jQuery UI 1.8.17 Microsoft Ajax CDN에서")
- [jQuery UI 1.8.16](jquery-ui/cdnjqueryui1816.md "jQuery UI 1.8.16 Microsoft Ajax CDN에서")
- [jQuery UI 1.8.15](jquery-ui/cdnjqueryui1815.md "jQuery UI 1.8.15 Microsoft Ajax CDN에서")
- [jQuery UI 1.8.14](jquery-ui/cdnjqueryui1814.md "jQuery UI 1.8.14 Microsoft Ajax CDN에서")
- [jQuery UI 1.8.13](jquery-ui/cdnjqueryui1813.md "jQuery UI 1.8.13 Microsoft Ajax CDN에서")
- [jQuery UI 1.8.12](jquery-ui/cdnjqueryui1812.md "jQuery UI 1.8.12 Microsoft Ajax CDN에서")
- [jQuery UI 1.8.11](jquery-ui/cdnjqueryui1811.md "jQuery UI 1.8.11 Microsoft Ajax CDN에서")
- [jQuery UI 1.8.10](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 Microsoft Ajax CDN에서")
- [jQuery UI 1.8.9](jquery-ui/cdnjqueryui189.md "jQuery UI 1.8.9 Microsoft Ajax CDN에서")
- [jQuery UI 1.8.8](jquery-ui/cdnjqueryui188.md "jQuery UI 1.8.8 Microsoft Ajax CDN에서")
- [jQuery UI 1.8.7](jquery-ui/cdnjqueryui187.md "jQuery UI 1.8.7 Microsoft Ajax CDN에서")
- [jQuery UI 1.8.6](jquery-ui/cdnjqueryui186.md "jQuery UI 1.8.6 Microsoft Ajax CDN에서")
- [jQuery UI 1.8.5](jquery-ui/cdnjqueryui185.md "jQuery UI 1.8.5")

<a id="jQuery_Validation_Releases_on_the_CDN_3"></a>

### <a name="jquery-validation-releases-on-the-cdn"></a>jQuery 유효성 검사는 CDN에 있는 릴리스

JQuery 유효성 검사 라이브러리의 다음 릴리스에서이 CDN에서 호스팅됩니다. 파일의 실제 목록을 확인 하려면 각 링크를 클릭 합니다.

- [jQuery 유효성 검사 1.17.0](jquery-validate/cdnjqueryvalidate1170.md "jQuery 유효성 검사 1.17.0")
- [jQuery 유효성 검사 1.16.0](jquery-validate/cdnjqueryvalidate1160.md "jQuery 유효성 검사 1.16.0")
- [jQuery 유효성 검사 1.15.1](jquery-validate/cdnjqueryvalidate1151.md "jQuery 유효성 검사 1.15.1")
- [jQuery 유효성 검사 1.15.0](jquery-validate/cdnjqueryvalidate1150.md "jQuery 유효성 검사 1.15.0")
- [jQuery 유효성 검사 1.14.0](jquery-validate/cdnjqueryvalidate1140.md "jQuery 유효성 검사 1.14.0")
- [jQuery 유효성 검사 1.13.1](jquery-validate/cdnjqueryvalidate1131.md "jQuery 유효성 검사 1.13.1")
- [jQuery 유효성 검사 1.13.0](jquery-validate/cdnjqueryvalidate1130.md "jQuery 유효성 검사 1.13.0")
- [jQuery 유효성 검사 1.12.0](jquery-validate/cdnjqueryvalidate1120.md "jQuery 유효성 검사 1.12.0")
- [jQuery 유효성 검사 1.11.1](jquery-validate/cdnjqueryvalidate1111.md "jQuery 유효성 검사 1.11.1")
- [jQuery 유효성 검사 1.11.0](jquery-validate/cdnjqueryvalidate111.md "jQuery 유효성 검사 1.11.0")
- [jQuery 유효성 검사 1.10.0](jquery-validate/cdnjqueryvalidate110.md "jQuery 유효성 검사 1.10.0")
- [jQuery 유효성 검사 1.9](jquery-validate/cdnjqueryvalidate19.md "jquery.validate 버전 1.9")
- [jQuery 유효성 검사 1.8.1](jquery-validate/cdnjqueryvalidate181.md "1.8.1 jquery.validate 버전")
- [jQuery 유효성 검사 1.8](jquery-validate/cdnjqueryvalidate18.md "jquery.validate 버전 1.8")
- [jQuery 유효성 검사 1.7](jquery-validate/cdnjqueryvalidate17.md "jquery.validate 버전 1.7")
- [jQuery 유효성 검사 1.6](jquery-validate/cdnjqueryvalidate16.md "jQuery 유효성 검사 1.6")
- [jQuery 유효성 검사 1.5.5](jquery-validate/cdnjqueryvalidate155.md "jQuery 유효성 검사 1.5.5")

<a id="jQuery_Mobile_Releases_on_the_CDN_4"></a>

### <a name="jquery-mobile-releases-on-the-cdn"></a>jQuery Mobile CDN에 있는 릴리스

JQuery 모바일 라이브러리의 다음 릴리스에서이 CDN에서 호스팅됩니다. 파일의 실제 목록을 확인 하려면 각 링크를 클릭 합니다.

- [jQuery Mobile 1.4.5](jquery-mobile/cdnjquerymobile145.md "jQuery Mobile 1.4.5 Microsoft Ajax CDN에서")
- [jQuery Mobile 1.4.2](jquery-mobile/cdnjquerymobile142.md "jQuery Mobile 1.4.2 Microsoft Ajax CDN에서")
- [jQuery Mobile 1.4.1](jquery-mobile/cdnjquerymobile141.md "jQuery Mobile 1.4.1 Microsoft Ajax CDN에서")
- [jQuery Mobile 1.4.0](jquery-mobile/cdnjquerymobile140.md "jQuery Mobile 1.4.0 Microsoft Ajax CDN에서")
- [jQuery Mobile 1.3.2](jquery-mobile/cdnjquerymobile132.md "jQuery Mobile 1.3.2 Microsoft Ajax CDN에서")
- [jQuery Mobile 1.3.1](jquery-mobile/cdnjquerymobile131.md "jQuery Mobile 1.3.1 Microsoft Ajax CDN에서")
- [jQuery Mobile 1.3.0](jquery-mobile/cdnjquerymobile130.md "jQuery Mobile 1.3.0 Microsoft Ajax CDN에서")
- [jQuery Mobile 1.2.0](jquery-mobile/cdnjquerymobile120.md "jQuery Mobile 1.2.0 Microsoft Ajax CDN에서")
- [jQuery Mobile 1.1.2](jquery-mobile/cdnjquerymobile112.md "jQuery Mobile 1.1.2 Microsoft Ajax CDN에서")
- [jQuery Mobile 1.1.1](jquery-mobile/cdnjquerymobile111.md "jQuery Mobile 1.1.1 Microsoft Ajax CDN에서")
- [jQuery Mobile 1.1.0](jquery-mobile/cdnjquerymobile110.md "jQuery Mobile 1.1.0 Microsoft Ajax CDN에서")
- [jQuery Mobile 1.1.0 RC 2](jquery-mobile/cdnjquerymobile110rc2.md "jQuery Mobile 1.1.0 RC2 Microsoft Ajax CDN에서")
- [jQuery Mobile 1.0.1](jquery-mobile/cdnjquerymobile101.md "jQuery Mobile 1.0.1 Microsoft Ajax CDN에서")
- [jQuery Mobile 1.0](jquery-mobile/cdnjquerymobile10.md "jQuery Mobile 1.0 Microsoft Ajax CDN에서")
- [jQuery Mobile 1.0 RC 2](jquery-mobile/cdnjquerymobile10rc2.md "Microsoft Ajax CDN에서 jQuery Mobile 1.0 RC2")
- [jQuery Mobile 1.0 RC 1](jquery-mobile/cdnjquerymobile10rc1.md "Microsoft Ajax CDN에서 jQuery Mobile 1.0 RC1")
- [jQuery Mobile 1.0 베타 3](jquery-mobile/cdnjquerymobile10b3.md "Microsoft Ajax CDN에서 jQuery Mobile 1.0 베타 3")

<a id="jQuery_Templates_Releases_on_the_CDN_5"></a>

### <a name="jquery-templates-releases-on-the-cdn"></a>jQuery CDN에서 템플릿 릴리스

다음 버전의 jQuery 템플릿 플러그 인이이 CDN에서 호스트 됩니다. 파일의 실제 목록을 확인 하려면 각 링크를 클릭 합니다.

- [jQuery 템플릿 베타 1](jquery-templates/cdnjquerytemplatesbeta1.md "jQuery 템플릿 베타 1")

<a id="jQuery_Cycle_Releases_on_the_CDN_6"></a>

### <a name="jquery-cycle-releases-on-the-cdn"></a>jQuery CDN에서 주기 릴리스

다음 릴리스에 jQuery 주기 플러그 인을이 CDN에서 호스트 됩니다. 파일의 실제 목록을 확인 하려면 각 링크를 클릭 합니다.

- [jQuery Cycle 2.99](jquery-cycle/cdnjquerycycle299.md "jQuery Cycle 2.99")
- [jQuery Cycle 2.94](jquery-cycle/cdnjquerycycle294.md "jQuery Cycle 2.94")
- [jQuery Cycle 2.88](jquery-cycle/cdnjquerycycle288.md "jQuery Cycle 2.88")

<a id="jQuery_DataTables_Releases_on_the_CDN_7"></a>

### <a name="jquery-datatables-releases-on-the-cdn"></a>jQuery CDN에서 DataTables 릴리스

다음 릴리스에 jQuery Datatable 플러그 인을이 CDN에서 호스트 됩니다. 파일의 실제 목록을 확인 하려면 각 링크를 클릭 합니다.

- [jQuery Datatable 1.10.5](jquery-datatables/cdnjquerydatatables105.md "jQuery Datatable 1.10.5")
- [jQuery Datatable 1.10.4](jquery-datatables/cdnjquerydatatables104.md "jQuery Datatable 1.10.4")
- [jQuery Datatable 1.9.4](jquery-datatables/cdnjquerydatatables194.md "jQuery Datatable 1.9.4")
- [jQuery Datatable 1.9.3](jquery-datatables/cdnjquerydatatables193.md "jQuery Datatable 1.9.3")
- [jQuery Datatable 1.9.2](jquery-datatables/cdnjquerydatatables192.md "jQuery Datatable 1.9.2")
- [jQuery Datatable 1.9.1](jquery-datatables/cdnjquerydatatables191.md "jQuery Datatable 1.9.1")
- [jQuery Datatable 1.9.0](jquery-datatables/cdnjquerydatatables190.md "jQuery Datatable 1.9.0")
- [jQuery Datatable 1.8.2](jquery-datatables/cdnjquerydatatables182.md "jQuery Datatable 1.8.2")

<a id="Modernizr_Releases_on_the_CDN_8"></a>

### <a name="modernizr-releases-on-the-cdn"></a>CDN에서 Modernizr 릴리스

다음 릴리스의 [Modernizr](http://www.modernizr.com "Modernizr") CDN에서 호스팅됩니다.

- http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.8.3.js
- http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.2.js
- http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.1.js
- http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.6.2.js
- http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-1.7-development-only.js
- http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.0.6-development-only.js

<a id="JSHint_Releases_on_the_CDN_10"></a>

### <a name="jshint-releases-on-the-cdn"></a>CDN에서 JSHint 릴리스

다음 릴리스의 [JSHint](http://www.jshint.com "JSHint") CDN에서 호스팅됩니다.

- http://ajax.aspnetcdn.com/ajax/jshint/r07/jshint.js

<a id="Knockout_Releases_on_the_CDN_11"></a>

### <a name="knockout-releases-on-the-cdn"></a>CDN에서 knockout 릴리스

다음 릴리스의 [Knockout](http://www.knockoutjs.com "Knockout") CDN에서 호스팅됩니다.

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

### <a name="globalize-releases-on-the-cdn"></a>CDN에서 릴리스 전역화

다음 릴리스의 [Globalize](https://github.com/jquery/globalize "Globalize") CDN에서 호스팅됩니다.

#### <a name="globalize-version-100"></a>버전 1.0.0을 전역화

- http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize.js
- http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/node-main.js
- http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/currency.js
- http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/date.js
- http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/message.js
- http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/number.js
- http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/plural.js
- http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/relative-time.js

#### <a name="globalize-version-011"></a>버전 0.1.1 전역화

- http://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.min.js
- http://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.js
- http://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.cultures.js

    - 모든 문화권
- http://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.culture.{culture-code}.js

    - "{코드 문화권을 (를)"를 원하는 culture 코드로 바꿉니다, globalize.culture.en GB.js== Microsoft CDN에 예를 들어 파일을이 = = Microsoft에서 라이브러리가 업로드 합니다.

<a id="Respond_Releases_on_the_CDN_13"></a>

### <a name="respond-releases-on-the-cdn"></a>CDN에서 릴리스 응답

다음 릴리스의 [ https://github.com/scottjehl/Respond ] (https://github.com/scottjehl/Respond " https://github.com/scottjehl/Respond ") 응답 하는 CDN에 호스팅됩니다.

#### <a name="respond-version-142"></a>1.4.2 버전 응답

- http://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.js
- http://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.min.js
- http://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.js
- http://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.min.js

#### <a name="respond-version-141"></a>1.4.1 버전 응답

- http://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.js
- http://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.min.js
- http://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.js
- http://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.min.js

#### <a name="respond-version-140"></a>버전 1.4.0 응답

- http://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.js
- http://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.min.js
- http://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.js
- http://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.min.js

#### <a name="respond-version-130"></a>버전 1.3.0 응답

- http://ajax.aspnetcdn.com/ajax/respond/1.3.0/respond.js

#### <a name="respond-version-120"></a>버전 1.2.0 응답

- http://ajax.aspnetcdn.com/ajax/respond/1.2.0/respond.js

<a id="Bootstrap_Releases_on_the_CDN_14"></a>

### <a name="bootstrap-releases-on-the-cdn"></a>CDN에서 부트스트랩 릴리스

다음 릴리스의 [getbootstrap.com](http://getbootstrap.com "getbootstrap.com") 부트스트랩 CDN에서 호스팅됩니다.

#### <a name="bootstrap-version-400"></a>부트스트랩 버전 4.0.0

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

#### <a name="bootstrap-version-337"></a>3.3.7 부트스트랩 버전

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

#### <a name="bootstrap-version-336"></a>부트스트랩 버전 3.3.6

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

#### <a name="bootstrap-version-335"></a>부트스트랩 버전 3.3.5

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

#### <a name="bootstrap-version-334"></a>3.3.4 부트스트랩 버전

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

#### <a name="bootstrap-version-332"></a>3.3.2 부트스트랩 버전

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

#### <a name="bootstrap-version-331"></a>3.3.1 부트스트랩 버전

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

#### <a name="bootstrap-version-330"></a>부트스트랩 버전 3.3.0

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

#### <a name="bootstrap-version-320"></a>부트스트랩 버전 3.2.0

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

#### <a name="bootstrap-version-311"></a>3.1.1 부트스트랩 버전

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

#### <a name="bootstrap-version-310"></a>부트스트랩 버전 3.1.0

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

#### <a name="bootstrap-version-303"></a>부트스트랩 버전 3.0.3

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

#### <a name="bootstrap-version-302"></a>부트스트랩 버전 3.0.2

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

#### <a name="bootstrap-version-301"></a>부트스트랩 버전 3.0.1

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

#### <a name="bootstrap-version-300"></a>부트스트랩 버전 3.0.0

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

#### <a name="bootstrap-version-232"></a>부트스트랩 버전 2.3.2

- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.min.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings.png
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings-white.png

#### <a name="bootstrap-version-231"></a>부트스트랩 버전 2.3.1

- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.min.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings.png
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings-white.png

<a id="BootstrapTouchCarousel_Releases_on_the_CDN_18"></a>

### <a name="bootstrap-touchcarousel-releases-on-the-cdn"></a>CDN에서 부트스트랩 TouchCarousel 릴리스

다음 릴리스의 [ https://github.com/ixisio/bootstrap-touch-carousel ] (https://github.com/ixisio/bootstrap-touch-carousel " https://github.com/ixisio/bootstrap-touch-carousel ") 부트스트랩 TouchCarousel 릴리스 CDN에서 호스팅됩니다.

#### <a name="bootstrap-touchcarousel-version-080"></a>부트스트랩 TouchCarousel 버전 0.8.0

- http://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/css/bootstrap-touch-carousel.css
- http://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/js/bootstrap-touch-carousel.js

<a id="Hammerjs_Releases_on_the_CDN_19"></a>

### <a name="hammerjs-releases-on-the-cdn"></a>CDN에서 Hammer.js 릴리스

다음 버전의 [ http://hammerjs.github.io/ ] (http://hammerjs.github.io/ " http://hammerjs.github.io/ ") Hammer.js 릴리스 CDN에서 호스팅됩니다.

#### <a name="hammerjs-version-204"></a>2.0.4 Hammer.js 버전

- http://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.js
- http://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.js
- http://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.map

<a id="ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15"></a>

### <a name="aspnet-web-forms-and-ajax-releases-on-the-cdn"></a>ASP.NET Web Forms 및 CDN에서 Ajax 릴리스

ASP.NET Ajax 라이브러리의 다음 릴리스에서 CDN에서 호스팅됩니다. 파일의 실제 목록을 확인 하려면 각 링크를 클릭 합니다.

- [ASP.NET Web Forms 및 Ajax 버전 4.5.2](cdnajax452.md "ASP.NET Web Forms 및 Ajax 4.5.2")
- [ASP.NET Web Forms 및 Ajax 버전 4](cdnajax4.md "ASP.NET Web Forms 및 Ajax 4")
- [ASP.NET Ajax 버전 3.5](cdnajax35.md "ASP.NET Ajax 3.5")

<a id="ASPNET_MVC_Releases_on_the_CDN_16"></a>

### <a name="aspnet-mvc-releases-on-the-cdn"></a>CDN에 ASP.NET MVC 릴리스

다음 ASP.NET MVC JavaScript 파일이이 CDN에서 호스트 됩니다.

#### <a name="aspnet-mvc-523"></a>ASP.NET MVC 5.2.3

- http://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.js
- http://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-51"></a>ASP.NET MVC 5.1

- http://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.js
- http://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-50"></a>ASP.NET MVC 5.0

- http://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.js
- http://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-40"></a>ASP.NET MVC 4.0

- http://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.js
- http://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-30"></a>ASP.NET MVC 3.0

- http://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.js
- http://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.min.js
- http://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.js
- http://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.min.js
- http://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.js
- http://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-20"></a>ASP.NET MVC 2.0

- http://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.js
- http://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-10"></a>ASP.NET MVC 1.0

- http://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.js
- http://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.debug.js

<a id="ASPNET_SignalR_Releases_on_the_CDN_17"></a>

### <a name="aspnet-signalr-releases-on-the-cdn"></a>CDN에서 ASP.NET SignalR 해제

다음 ASP.NET SignalR JavaScript 파일이이 CDN에서 호스트 됩니다.

#### <a name="aspnet-signalr-222"></a>ASP.NET SignalR 2.2.2

- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.min.js
- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.js

#### <a name="aspnet-signalr-221"></a>ASP.NET SignalR 2.2.1

- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.min.js
- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.js

#### <a name="aspnet-signalr-220"></a>ASP.NET SignalR 2.2.0

- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.min.js
- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.js

#### <a name="aspnet-signalr-210"></a>ASP.NET SignalR 2.1.0

- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.min.js
- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.js

#### <a name="aspnet-signalr-203"></a>ASP.NET SignalR 2.0.3

- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.min.js
- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.js

#### <a name="aspnet-signalr-202"></a>ASP.NET SignalR 2.0.2

- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.min.js
- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.js

#### <a name="aspnet-signalr-201"></a>ASP.NET SignalR 2.0.1

- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.min.js
- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.js

#### <a name="aspnet-signalr-200"></a>ASP.NET SignalR 2.0.0

- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.min.js
- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.js

#### <a name="aspnet-signalr-113"></a>ASP.NET SignalR 1.1.3

- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.min.js
- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.js

#### <a name="aspnet-signalr-112"></a>ASP.NET SignalR 1.1.2

- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.min.js
- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.js

#### <a name="aspnet-signalr-111"></a>ASP.NET SignalR 1.1.1

- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.min.js
- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.js

#### <a name="aspnet-signalr-110"></a>ASP.NET SignalR 1.1.0

- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.min.js
- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.js

#### <a name="aspnet-signalr-101"></a>ASP.NET SignalR 1.0.1

- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.min.js
- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.js

CDN에 대 한 사용 조건에 대 한 정보를 참조 하십시오. [Microsoft Ajax CDN 사용 약관](https://www.asp.net/terms-of-use "Microsoft Ajax CDN 사용 약관")합니다.
