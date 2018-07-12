---
uid: ajax/cdn/overview
title: Microsoft Ajax 콘텐츠 배달 네트워크 | Microsoft Docs
author: rick-anderson
description: ''
ms.author: aspnetcontent
ms.date: 10/14/2017
ms.assetid: 8935bf14-ca6d-4a4e-9dbe-b96ce74cef49
msc.legacyurl: /ajax/cdn
msc.type: content
ms.openlocfilehash: 3ec70bb0746d18e453b6e5728b6ba90b2a3e87f3
ms.sourcegitcommit: 19cbda409bdbbe42553dc385ea72d2a8e246509c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38992937"
---
<a name="microsoft-ajax-content-delivery-network"></a>Microsoft Ajax Content Delivery Network
====================
> [!WARNING]
> 프로덕션 응용 프로그램 CDN 자산 한 강한 종속성을 사용 하지 않아야 합니다. 응용 프로그램 참조 CDN 자산에 대 한 테스트 하 고 CDN을 사용할 수 없는 경우 대체 (fallback) 자산을 사용 해야 합니다. 
>
> Microsoft Ajax CDN에는 Azure CDN을 사용 하 여 이상의 SLA가 없습니다.
>
> 사용 하 여 [이 GitHub 문제](https://github.com/aspnet/Docs/issues/5832) 에 Microsoft Ajax CDN을 사용 하 여 문제를 보고 합니다.

## <a name="table-of-contents"></a>목차

**[ajax.microsoft.com ajax.aspnetcdn.com로 변경](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**  
**[Visual Studio.vsdoc 지원](#Visual_Studio_vsdoc_Support_19)**  
**[CDN에서 ASP.NET Ajax를 사용 하 여](#Using_ASPNET_Ajax_from_the_CDN_20)**  
**[CDN에서 jQuery를 사용 하 여](#Using_jQuery_from_the_CDN_21)**  
**[CDN에서 jQuery를 사용 하 여](#Using_jQuery_UI_from_the_CDN_22)**  
**[CDN의 제 3 자 파일](#Third-Party_Files_on_the_CDN_23)**  
  
 [CDN에서 jQuery 릴리스](#jQuery_Releases_on_the_CDN_0)  
 [CDN에서 jQuery 마이그레이션 릴리스](#jQuery_Migrate_Releases_on_the_CDN_1)  
 [jQuery UI 릴리스 cdn](#jQuery_UI_Releases_on_the_CDN_2)  
 [jQuery 유효성 검사 릴리스 cdn](#jQuery_Validation_Releases_on_the_CDN_3)  
 [jQuery Mobile 릴리스 cdn](#jQuery_Mobile_Releases_on_the_CDN_4)  
 [jQuery CDN에서 템플릿 릴리스](#jQuery_Templates_Releases_on_the_CDN_5)  
 [jQuery CDN에서 주기 릴리스](#jQuery_Cycle_Releases_on_the_CDN_6)  
 [jQuery DataTables 릴리스 cdn](#jQuery_DataTables_Releases_on_the_CDN_7)  
 [CDN에서 Modernizr 릴리스](#Modernizr_Releases_on_the_CDN_8)  
 [CDN에서 JSHint 릴리스](#JSHint_Releases_on_the_CDN_10)  
 [CDN에서 knockout 릴리스](#Knockout_Releases_on_the_CDN_11)  
 [CDN에서 릴리스 세계화](#Globalize_Releases_on_the_CDN_12)  
 [CDN에서 릴리스 응답](#Respond_Releases_on_the_CDN_13)  
 [CDN에서 부트스트랩 릴리스](#Bootstrap_Releases_on_the_CDN_14)  
 [CDN에서 부트스트랩 TouchCarousel 릴리스](#BootstrapTouchCarousel_Releases_on_the_CDN_18)  
 [CDN에서 Hammer.js 릴리스](#Hammerjs_Releases_on_the_CDN_19)  
 [ASP.NET Web Forms 및 CDN에서 Ajax 릴리스](#ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15)  
 [ASP.NET MVC cdn 해제](#ASPNET_MVC_Releases_on_the_CDN_16)  
 [ASP.NET SignalR cdn 해제](#ASPNET_SignalR_Releases_on_the_CDN_17)

Microsoft Ajax 콘텐츠 배달 네트워크 (CDN) jQuery 같은 인기 있는 타사 JavaScript 라이브러리를 호스팅하고 웹 응용 프로그램에 쉽게 추가할 수 있습니다. 이 CDN에 호스트 되는 jQuery를 사용 하 여 추가 하 여 시작할 수는 예를 들어, 한 &lt;스크립트&gt; ajax.aspnetcdn.com 가리키는 페이지 태그입니다.

CDN을 활용 하 여 Ajax 응용 프로그램의 성능을 크게 개선할 수 있습니다. CDN의 콘텐츠는 세계에 있는 서버에 캐시 됩니다. 또한 CDN에는 브라우저 서로 다른 도메인에 있는 웹 사이트에 대 한 캐시 된 타사 JavaScript 파일을 다시 사용할 수 있도록 설정 합니다.

CDN Secure Sockets Layer를 사용 하 여 웹 페이지를 처리 해야 하는 경우 SSL (HTTPS)을 지원 합니다.

CDN은 업로드 된 있으며, 이러한 라이브러리의 소유자가 사용이 허가 되는 다음과 같은 타사 스크립트 라이브러리를 호스트 합니다.

- jQuery (www.jquery.com)
- jQuery UI (www.jqueryui.com)
- jQuery Mobile (www.jquerymobile.com)
- jQuery 유효성 검사 (www.jquery.com)
- jQuery 주기 (www.malsup.com/jquery/cycle/)
- jQuery DataTables (http://datatables.net/)

Microsoft Ajax CDN에는 Microsoft에서 업로드 된 다음 라이브러리를 포함 합니다.

- ASP.NET Ajax
- ASP.NET MVC JavaScript 파일
- ASP.NET SignalR JavaScript 파일

Microsoft는이 CDN에 호스트 된 모든 타사 라이브러리의 소유권을 주장 하지 않습니다. 라이브러리의 저작권 소유자는 이러한 라이브러리를 라이선스 다운로드 하 고 이러한 라이브러리를 사용할 수 있는 권리는 해당 하는 저작권 소유자가 단독으로 부여 됩니다. 이들은 Microsoft 라이브러리, Microsoft 없습니다 보증 또는 지적 재산 권한 라이선스가 없는 묵시적인된 특허 권한 등이 CDN에 호스트 된 타사 라이브러리에 대 한 제공 합니다.

JavaScript 라이브러리를 제출 하려는 경우 라이브러리를 사용 하면 상위 JavaScript 라이브러리 중 하나인 (에 나열 http://trends.builtwith.com) (a) 인기 있는; 또는 (b) 하는 데 도움이 ASP.NET에서 사용 된 후에 문의 하세요 이러한 라이브러리를 확장/플러그 인 또는 AjaxCDNSubmission@Microsoft.com합니다.

<a id="ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18"></a>

## <a name="ajaxmicrosoftcom-renamed-to-ajaxaspnetcdncom"></a>ajax.microsoft.com ajax.aspnetcdn.com로 변경

CDN은 microsoft.com 도메인 이름을 사용 하는 데 사용 하 고 aspnetcdn.com 도메인 이름을 사용 하도록 변경 되었습니다. 보내기 때문에 브라우저는 microsoft.com 도메인을 참조 하는 경우이 모든 쿠키 도메인에서 각 요청을 사용 하 여 네트워크를 통해 성능 향상을 위해이 변경 되었습니다. Microsoft.com 이외의 도메인 이름으로 바꾸어 25%로 만큼 성능으로 늘릴 수 있습니다. 참고 ajax.microsoft.com 계속 작동 하지만 ajax.aspnetcdn.com를 사용 하는 것이 좋습니다.

- 이전 형식: https://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js
- 새 형식: https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js

<a id="Visual_Studio_vsdoc_Support_19"></a>

## <a name="visual-studio-vsdoc-support"></a>Visual Studio.vsdoc 지원

VS 2008 sp1이 설치 되어 있는지 확인 해야 하는 Visual Studio 2008을 사용 하 여.vsdoc 파일을 제대로 사용 하려면 설치 하 고 vsdoc 파일에 대 한 핫픽스를 설치 합니다. 여기에서 가져올 수 있습니다.

- [Visual Studio 2008 SP1을 다운로드](https://www.microsoft.com/downloads/en/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en "Visual Studio 2008 SP1 다운로드")
- [Visual Studio 2008 SP1 용.vsdoc 핫픽스를 다운로드](https://code.msdn.microsoft.com/KB958502/Release/ProjectReleases.aspx?ReleaseId=1736 ".vsdoc 핫픽스 Visual Studio 2008 sp1 다운로드")

Visual Studio 2010 추가 패치 없이.vsdoc 파일을 지원합니다.

<a id="Using_ASPNET_Ajax_from_the_CDN_20"></a>

## <a name="using-aspnet-ajax-from-the-cdn"></a>CDN에서 ASP.NET Ajax를 사용 하 여

ASP.NET 4를 사용 하는 경우에 CDN에 ASP.NET 프레임 워크 스크립트에 대 한 모든 요청을 리디렉션할 수 있습니다. 로컬 웹 서버 대신 CDN에서 스크립트 검색 공용 ASP.NET 웹 사이트의 성능을 크게 향상 시킬 수 있습니다.

Microsoft Ajax CDN에 모든 ASP.NET 프레임 워크 스크립트 요청을 리디렉션할 ScriptManager EnableCDN 속성을 사용 합니다.

[!code-aspx[Main](overview/samples/sample1.aspx)]

<a id="Using_jQuery_from_the_CDN_21"></a>

## <a name="using-jquery-from-the-cdn"></a>CDN에서 jQuery를 사용 하 여

페이지에 다음 스크립트 요소를 추가 하 여 CDN에서 웹 응용 프로그램에서 호스팅되는 jQuery 스크립트를 사용할 수 있습니다.

[!code-html[Main](overview/samples/sample2.html)]

CDN의 jQuery 스크립트를 가져올 수 있는 축소 된 버전도 포함 되어 있습니다 다음 요소를 사용 하 여:

[!code-html[Main](overview/samples/sample3.html)]

CDN을 사용할 수 없는 경우 고유한 웹 사이트의 로컬 경로에서 jQuery 로드로 대체 하기 위해 페이지를 허용 하려면 CDN 참조 요소 바로 뒤 다음 요소를 추가 합니다.

[!code-html[Main](overview/samples/sample4.html)]

다음 샘플 페이지 단추를 클릭할 때 div 요소의 내용을 표시 하려면 CDN에서 jQuery 라이브러리 (로컬 복사본으로 대체)를 버전을 사용 합니다.

[!code-html[Main](overview/samples/sample5.html)]

JQuery에 대 한 자세한 정보를 방문 하 여 jQuery의 로컬 복사본을 다운로드 합니다 [jQuery](http://jquery.com/) 웹 사이트입니다.

<a id="Using_jQuery_UI_from_the_CDN_22"></a>

## <a name="using-jquery-ui-from-the-cdn"></a>CDN에서 jQuery를 사용 하 여

또한 CDN의 jQuery UI 라이브러리를 호스트합니다. JQuery UI 라이브러리는 다양 한 위젯 및 ASP.NET 응용 프로그램에서 사용할 수 있는 효과 포함 합니다. 예를 들어, 다음 페이지는 ASP.NET Web Forms 응용 프로그램의 컨텍스트에서 jQuery UI Datepicker 팝업 달력이 표시를 사용 하는 방법을 보여 줍니다.

[!code-aspx[Main](overview/samples/sample6.aspx)]

키보드를 사용 하 여 텍스트 상자에 포커스를 이동 하면 달력이 표시 됩니다.

![Datepicker를 사용 하 여 만든 팝업 일정](overview/_static/image1.png)

위의 코드에서 CDN에서 세 개의 파일을 포함 해야 합니다는 알 수 있습니다.

- JQuery 라이브러리 &mdash; jQuery UI 라이브러리는 jQuery 라이브러리에 의존 합니다. JQuery UI 라이브러리를 추가 하기 전에 페이지에 jQuery 라이브러리를 추가 해야 합니다.
- JQuery UI 라이브러리 &mdash; jQuery UI 효과 및 위젯 Datepicker 위젯 위의 페이지에 사용 되는 등의 모든 jQuery UI 라이브러리를 포함 합니다.
- JQuery UI 테마 &mdash; jQuery UI는 다양 한 테마를 지원 합니다. 위 페이지 Redmond 테마 가져올 CSS 파일에 대 한 링크를 포함 합니다.

모든 표준 jQuery UI 테마는 CDN에서 호스팅됩니다. [이 페이지를 방문](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 Microsoft Ajax CDN") 각 테마에 대 한 미리 보기를 볼 수 있습니다.

JQuery UI 라이브러리에 대 한 자세한 내용은 공식을 방문 [jQuery UI 웹 사이트](http://jQueryUI.com "jQuery UI 웹 사이트")합니다.

<a id="Third-Party_Files_on_the_CDN_23"></a>

## <a name="third-party-files-on-the-cdn"></a>CDN의 제 3 자 파일

CDN 호스트 가장 인기 있는 타사 JavaScript 라이브러리의 일부입니다. Microsoft는이 CDN에 호스트 된 모든 타사 라이브러리의 소유권을 주장 하지 않습니다. 라이브러리의 저작권 소유자는 이러한 라이브러리를 라이선스 다운로드 하 고 이러한 라이브러리를 사용할 수 있는 권리는 해당 하는 저작권 소유자가 단독으로 부여 됩니다. 이들은 Microsoft 라이브러리, Microsoft 없습니다 보증 또는 지적 재산 권한 라이선스가 없는 묵시적인된 특허 권한 등이 CDN에 호스트 된 타사 라이브러리에 대 한 제공 합니다.

<a id="jQuery_Releases_on_the_CDN_0"></a>

### <a name="jquery-releases-on-the-cdn"></a>CDN에서 jQuery 릴리스

CDN에서 jQuery의 다음 릴리스가 호스팅됩니다.

#### <a name="jquery-version-331"></a>jQuery 버전 3.3.1
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.map

#### <a name="jquery-version-321"></a>jQuery 버전 3.2.1
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.map

#### <a name="jquery-version-320"></a>jQuery 버전 3.2.0

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.map

#### <a name="jquery-version-311"></a>3.1.1 jQuery 버전

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.map

#### <a name="jquery-version-310"></a>jQuery 버전 3.1.0

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.map

#### <a name="jquery-version-300"></a>jQuery 버전 3.0.0

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.map

#### <a name="jquery-version-224"></a>jQuery 버전 2.2.4

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.map

#### <a name="jquery-version-223"></a>jQuery 버전 2.2.3

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.map

#### <a name="jquery-version-222"></a>jQuery 버전 2.2.2

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.map

#### <a name="jquery-version-221"></a>jQuery 버전 2.2.1

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.map

#### <a name="jquery-version-220"></a>jQuery 버전 2.2.0

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.map

#### <a name="jquery-version-214"></a>jQuery 버전 2.1.4

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.map

#### <a name="jquery-version-213"></a>jQuery 버전 2.1.3

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.map

#### <a name="jquery-version-212"></a>jQuery 버전 2.1.2

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.min.js

#### <a name="jquery-version-211"></a>jQuery 버전 2.1.1

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.map

#### <a name="jquery-version-210"></a>jQuery 버전 2.1.0

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.map

#### <a name="jquery-version-203"></a>jQuery 버전 2.0.3

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.map

#### <a name="jquery-version-202"></a>jQuery 버전 2.0.2

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.map

#### <a name="jquery-version-201"></a>jQuery 버전 2.0.1

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.map

#### <a name="jquery-version-200"></a>jQuery 버전 2.0.0

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.map

#### <a name="jquery-version-1124"></a>jQuery 버전 1.12.4

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.map

#### <a name="jquery-version-1123"></a>jQuery 버전 1.12.3

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.map

#### <a name="jquery-version-1122"></a>jQuery 버전 1.12.2

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.map

#### <a name="jquery-version-1121"></a>jQuery 버전 1.12.1

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.map

#### <a name="jquery-version-1120"></a>jQuery 버전 1.12.0

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.map

#### <a name="jquery-version-1113"></a>jQuery 버전 1.11.3

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.map

#### <a name="jquery-version-1112"></a>jQuery 버전 1.11.2

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.map

#### <a name="jquery-version-1111"></a>jQuery 버전 1.11.1

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.map

#### <a name="jquery-version-1110"></a>jQuery 버전 1.11.0

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.map

#### <a name="jquery-version-1102"></a>jQuery 버전 1.10.2

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.map

#### <a name="jquery-version-1101"></a>jQuery 버전 1.10.1

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.map

#### <a name="jquery-version-1100"></a>jQuery 버전 1.10.0

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.map

#### <a name="jquery-version-191"></a>jQuery 버전 1.9.1

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.map

#### <a name="jquery-version-190"></a>jQuery 버전 1.9.0

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.map

#### <a name="jquery-version-183"></a>jQuery 버전 1.8.3

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3-vsdoc.js

#### <a name="jquery-version-182"></a>jQuery 버전 1.8.2

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2-vsdoc.js

#### <a name="jquery-version-181"></a>jQuery 버전 1.8.1

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1-vsdoc.js

#### <a name="jquery-version-180"></a>jQuery 버전 1.8.0

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0-vsdoc.js

#### <a name="jquery-version-172"></a>jQuery 버전 1.7.2

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js

#### <a name="jquery-version-171"></a>jQuery 버전 1.7.1

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1-vsdoc.js

#### <a name="jquery-version-17"></a>jQuery 버전 1.7

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7-vsdoc.js

#### <a name="jquery-version-164"></a>jQuery 버전 1.6.4

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4-vsdoc.js

#### <a name="jquery-version-163"></a>jQuery 버전 1.6.3

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3-vsdoc.js

#### <a name="jquery-version-162"></a>jQuery 버전 1.6.2

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2-vsdoc.js

#### <a name="jquery-version-161"></a>jQuery 버전 1.6.1

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1-vsdoc.js

#### <a name="jquery-version-16"></a>jQuery 버전 1.6

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6-vsdoc.js

#### <a name="jquery-version-152"></a>jQuery 1.5.2 버전

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2-vsdoc.js

#### <a name="jquery-version-151"></a>jQuery 1.5.1

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1-vsdoc.js

#### <a name="jquery-version-15"></a>jQuery 버전 1.5

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5-vsdoc.js

#### <a name="jquery-version-144"></a>jQuery 버전 1.4.4

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4-vsdoc.js

#### <a name="jquery-version-143"></a>jQuery 버전 1.4.3

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3-vsdoc.js

#### <a name="jquery-version-142"></a>jQuery 버전 1.4.2

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2-vsdoc.js

#### <a name="jquery-version-141"></a>jQuery 버전 1.4.1

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1-vsdoc.js

#### <a name="jquery-version-14"></a>jQuery 버전 1.4

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.min.js

#### <a name="jquery-version-132"></a>jQuery 버전 1.3.2

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min-vsdoc.js

<a id="jQuery_Migrate_Releases_on_the_CDN_1"></a>

### <a name="jquery-migrate-releases-on-the-cdn"></a>CDN에서 jQuery 마이그레이션 릴리스

마이그레이션 jQuery의 다음 릴리스 CDN에서 호스팅됩니다.

#### <a name="jquery-migrate-version-300"></a>jQuery 버전 3.0.0 마이그레이션

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.min.js

#### <a name="jquery-migrate-version-121"></a>jQuery 버전 1.2.1 마이그레이션

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.min.js

jQuery 버전 1.2.0 마이그레이션

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.min.js

#### <a name="jquery-migrate-version-111"></a>jQuery 버전 1.1.1 마이그레이션

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.min.js

#### <a name="jquery-migrate-version-110"></a>jQuery 버전 1.1.0 마이그레이션

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.min.js

#### <a name="jquery-migrate-version-100"></a>jQuery 버전 1.0.0 마이그레이션

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.min.js

<a id="jQuery_UI_Releases_on_the_CDN_2"></a>

### <a name="jquery-ui-releases-on-the-cdn"></a>jQuery UI 릴리스 cdn

이 CDN의 jQuery UI 라이브러리의 다음 릴리스가 호스팅됩니다. 파일의 실제 목록을 보려면 각 링크를 클릭 합니다.

- [jQuery UI 1.12.1](jquery-ui/cdnjqueryui1121.md "jQuery UI 1.12.1 Microsoft Ajax CDN")
- [jQuery UI 1.12.0](jquery-ui/cdnjqueryui1120.md "Microsoft Ajax CDN의 jQuery UI 1.12.0")
- [jQuery UI 1.11.4](jquery-ui/cdnjqueryui1114.md "Microsoft Ajax CDN의 jQuery UI 1.11.4")
- [jQuery UI 1.11.3](jquery-ui/cdnjqueryui1113.md "jQuery UI 1.11.3 Microsoft Ajax CDN")
- [jQuery UI 1.11.2](jquery-ui/cdnjqueryui1112.md "jQuery UI 1.11.2 Microsoft Ajax CDN")
- [jQuery UI 1.11.1](jquery-ui/cdnjqueryui1111.md "jQuery UI 1.11.1 Microsoft Ajax CDN")
- [jQuery UI 1.11.0](jquery-ui/cdnjqueryui1110.md "Microsoft Ajax CDN의 jQuery UI 1.11.0")
- [jQuery UI 1.10.4](jquery-ui/cdnjqueryui1104.md "jQuery UI 1.10.4 Microsoft Ajax CDN")
- [jQuery UI 1.10.3](jquery-ui/cdnjqueryui1103.md "jQuery UI 1.10.3 Microsoft Ajax CDN")
- [jQuery UI 1.10.2](jquery-ui/cdnjqueryui1102.md "jQuery UI 1.10.2 Microsoft Ajax CDN")
- [jQuery UI 1.10.1](jquery-ui/cdnjqueryui1101.md "jQuery UI 1.10.1 Microsoft Ajax CDN")
- [jQuery UI 1.10.0](jquery-ui/cdnjqueryui1100.md "jQuery UI 1.10.0 Microsoft Ajax CDN")
- [jQuery UI 1.9.2](jquery-ui/cdnjqueryui192.md "Microsoft Ajax CDN의 jQuery UI 1.9.2")
- [jQuery UI 1.9.1](jquery-ui/cdnjqueryui191.md "Microsoft Ajax CDN의 jQuery UI 1.9.1")
- [jQuery UI 1.9.0](jquery-ui/cdnjqueryui190.md "Microsoft Ajax CDN의 jQuery UI 1.9.0")
- [jQuery UI 1.8.24](jquery-ui/cdnjqueryui1824.md "jQuery UI 1.8.24 Microsoft Ajax CDN")
- [jQuery UI 1.8.23](jquery-ui/cdnjqueryui1823.md "jQuery UI 1.8.23 Microsoft Ajax CDN")
- [jQuery UI 1.8.22](jquery-ui/cdnjqueryui1822.md "jQuery UI 1.8.22 Microsoft Ajax CDN")
- [jQuery UI 1.8.21](jquery-ui/cdnjqueryui1821.md "jQuery UI 1.8.21 Microsoft Ajax CDN")
- [jQuery UI 1.8.20](jquery-ui/cdnjqueryui1820.md "jQuery UI 1.8.20 Microsoft Ajax CDN")
- [jQuery UI 1.8.19](jquery-ui/cdnjqueryui1819.md "jQuery UI 1.8.19 Microsoft Ajax CDN")
- [jQuery UI 1.8.18](jquery-ui/cdnjqueryui1818.md "jQuery UI 1.8.18 Microsoft Ajax CDN")
- [jQuery UI 1.8.17](jquery-ui/cdnjqueryui1817.md "jQuery UI 1.8.17 Microsoft Ajax CDN")
- [jQuery UI 1.8.16](jquery-ui/cdnjqueryui1816.md "jQuery UI 1.8.16 Microsoft Ajax CDN")
- [jQuery UI 1.8.15](jquery-ui/cdnjqueryui1815.md "jQuery UI 1.8.15 Microsoft Ajax CDN")
- [jQuery UI 1.8.14](jquery-ui/cdnjqueryui1814.md "jQuery UI 1.8.14 Microsoft Ajax CDN")
- [jQuery UI 1.8.13](jquery-ui/cdnjqueryui1813.md "jQuery UI 1.8.13 Microsoft Ajax CDN")
- [jQuery UI 1.8.12](jquery-ui/cdnjqueryui1812.md "jQuery UI 1.8.12 Microsoft Ajax CDN")
- [jQuery UI 1.8.11](jquery-ui/cdnjqueryui1811.md "jQuery UI 1.8.11 Microsoft Ajax CDN")
- [jQuery UI 1.8.10](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 Microsoft Ajax CDN")
- [jQuery UI 1.8.9](jquery-ui/cdnjqueryui189.md "jQuery UI 1.8.9 Microsoft Ajax CDN")
- [jQuery UI 1.8.8](jquery-ui/cdnjqueryui188.md "Microsoft Ajax CDN의 jQuery UI 1.8.8")
- [jQuery UI 1.8.7](jquery-ui/cdnjqueryui187.md "jQuery UI 1.8.7 Microsoft Ajax CDN")
- [jQuery UI 1.8.6](jquery-ui/cdnjqueryui186.md "jQuery UI 1.8.6 Microsoft Ajax CDN")
- [jQuery UI 1.8.5](jquery-ui/cdnjqueryui185.md "의 jQuery UI 1.8.5")

<a id="jQuery_Validation_Releases_on_the_CDN_3"></a>

### <a name="jquery-validation-releases-on-the-cdn"></a>jQuery 유효성 검사 릴리스 cdn

이 CDN의 jQuery 유효성 검사 라이브러리의 다음 릴리스가 호스팅됩니다. 파일의 실제 목록을 보려면 각 링크를 클릭 합니다.

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
- [jQuery 유효성 검사 1.8.1](jquery-validate/cdnjqueryvalidate181.md "jquery.validate 버전 1.8.1")
- [jQuery 유효성 검사 1.8](jquery-validate/cdnjqueryvalidate18.md "jquery.validate 버전 1.8")
- [jQuery 유효성 검사 1.7](jquery-validate/cdnjqueryvalidate17.md "jquery.validate 버전 1.7")
- [jQuery 유효성 검사 1.6](jquery-validate/cdnjqueryvalidate16.md "jQuery 1.6 유효성 검사")
- [jQuery 유효성 검사 1.5.5](jquery-validate/cdnjqueryvalidate155.md "jQuery 유효성 검사 1.5.5")

<a id="jQuery_Mobile_Releases_on_the_CDN_4"></a>

### <a name="jquery-mobile-releases-on-the-cdn"></a>jQuery Mobile 릴리스 cdn

이 CDN의 jQuery Mobile 라이브러리의 다음 릴리스가 호스팅됩니다. 파일의 실제 목록을 보려면 각 링크를 클릭 합니다.

- [jQuery Mobile 1.4.5](jquery-mobile/cdnjquerymobile145.md "Microsoft Ajax CDN의 jQuery Mobile 1.4.5")
- [jQuery Mobile 1.4.2](jquery-mobile/cdnjquerymobile142.md "Microsoft Ajax CDN의 jQuery Mobile 1.4.2")
- [jQuery Mobile 1.4.1](jquery-mobile/cdnjquerymobile141.md "Microsoft Ajax CDN의 jQuery Mobile 1.4.1")
- [jQuery Mobile 1.4.0](jquery-mobile/cdnjquerymobile140.md "Microsoft Ajax CDN의 jQuery Mobile 1.4.0")
- [jQuery Mobile 1.3.2](jquery-mobile/cdnjquerymobile132.md "Microsoft Ajax CDN의 jQuery Mobile 1.3.2")
- [jQuery Mobile 1.3.1](jquery-mobile/cdnjquerymobile131.md "Microsoft Ajax CDN의 jQuery Mobile 1.3.1")
- [jQuery Mobile 1.3.0](jquery-mobile/cdnjquerymobile130.md "Microsoft Ajax CDN의 jQuery Mobile 1.3.0")
- [jQuery Mobile 1.2.0](jquery-mobile/cdnjquerymobile120.md "Microsoft Ajax CDN의 jQuery Mobile 1.2.0")
- [jQuery Mobile 1.1.2](jquery-mobile/cdnjquerymobile112.md "Microsoft Ajax CDN의 jQuery Mobile 1.1.2")
- [jQuery Mobile 1.1.1](jquery-mobile/cdnjquerymobile111.md "Microsoft Ajax CDN의 jQuery Mobile 1.1.1")
- [jQuery Mobile 1.1.0](jquery-mobile/cdnjquerymobile110.md "Microsoft Ajax CDN의 jQuery Mobile 1.1.0")
- [jQuery Mobile 1.1.0 RC 2](jquery-mobile/cdnjquerymobile110rc2.md "Microsoft Ajax CDN의 jQuery Mobile 1.1.0 RC2")
- [jQuery Mobile 1.0.1](jquery-mobile/cdnjquerymobile101.md "Microsoft Ajax CDN의 jQuery Mobile 1.0.1")
- [jQuery Mobile 1.0](jquery-mobile/cdnjquerymobile10.md "Microsoft Ajax CDN의 jQuery Mobile 1.0")
- [jQuery Mobile 1.0 RC 2](jquery-mobile/cdnjquerymobile10rc2.md "Microsoft Ajax CDN의 jQuery Mobile 1.0 RC2")
- [jQuery Mobile 1.0 RC 1](jquery-mobile/cdnjquerymobile10rc1.md "Microsoft Ajax CDN의 jQuery Mobile 1.0 RC1")
- [jQuery Mobile 1.0 beta 3](jquery-mobile/cdnjquerymobile10b3.md "Microsoft Ajax CDN의 jQuery Mobile 1.0 Beta 3")

<a id="jQuery_Templates_Releases_on_the_CDN_5"></a>

### <a name="jquery-templates-releases-on-the-cdn"></a>jQuery CDN에서 템플릿 릴리스

다음 릴리스의 jQuery 템플릿 플러그 인이이 CDN에서 호스트 됩니다. 파일의 실제 목록을 보려면 각 링크를 클릭 합니다.

- [jQuery 템플릿 베타 1](jquery-templates/cdnjquerytemplatesbeta1.md "jQuery 템플릿 베타 1")

<a id="jQuery_Cycle_Releases_on_the_CDN_6"></a>

### <a name="jquery-cycle-releases-on-the-cdn"></a>jQuery CDN에서 주기 릴리스

다음 릴리스의 jQuery 주기 플러그 인이이 CDN에서 호스트 됩니다. 파일의 실제 목록을 보려면 각 링크를 클릭 합니다.

- [jQuery 주기 2.99](jquery-cycle/cdnjquerycycle299.md "jQuery 주기 2.99")
- [jQuery 주기 2.94](jquery-cycle/cdnjquerycycle294.md "jQuery 주기 2.94")
- [jQuery 주기 2.88](jquery-cycle/cdnjquerycycle288.md "jQuery 주기 2.88")

<a id="jQuery_DataTables_Releases_on_the_CDN_7"></a>

### <a name="jquery-datatables-releases-on-the-cdn"></a>jQuery DataTables 릴리스 cdn

JQuery DataTables 플러그인의 다음 릴리스에서이 CDN에서 호스트 됩니다. 파일의 실제 목록을 보려면 각 링크를 클릭 합니다.

- [jQuery DataTables 1.10.5](jquery-datatables/cdnjquerydatatables105.md "jQuery DataTables 1.10.5")
- [jQuery DataTables 1.10.4](jquery-datatables/cdnjquerydatatables104.md "jQuery DataTables 1.10.4")
- [jQuery DataTables 1.9.4](jquery-datatables/cdnjquerydatatables194.md "jQuery DataTables 1.9.4")
- [jQuery DataTables 1.9.3](jquery-datatables/cdnjquerydatatables193.md "jQuery DataTables 1.9.3")
- [jQuery DataTables 1.9.2](jquery-datatables/cdnjquerydatatables192.md "jQuery DataTables 1.9.2")
- [jQuery DataTables 1.9.1](jquery-datatables/cdnjquerydatatables191.md "jQuery DataTables 1.9.1")
- [jQuery DataTables 1.9.0](jquery-datatables/cdnjquerydatatables190.md "jQuery DataTables 1.9.0")
- [jQuery DataTables 1.8.2](jquery-datatables/cdnjquerydatatables182.md "jQuery DataTables 1.8.2")

<a id="Modernizr_Releases_on_the_CDN_8"></a>

### <a name="modernizr-releases-on-the-cdn"></a>CDN에서 Modernizr 릴리스

다음 릴리스에서 [Modernizr](http://www.modernizr.com "Modernizr") CDN에서 호스팅됩니다.

- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.8.3.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.1.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.6.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-1.7-development-only.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.0.6-development-only.js

<a id="JSHint_Releases_on_the_CDN_10"></a>

### <a name="jshint-releases-on-the-cdn"></a>CDN에서 JSHint 릴리스

다음 릴리스에서 [JSHint](http://www.jshint.com "JSHint") CDN에서 호스팅됩니다.

- https://ajax.aspnetcdn.com/ajax/jshint/r07/jshint.js

<a id="Knockout_Releases_on_the_CDN_11"></a>

### <a name="knockout-releases-on-the-cdn"></a>CDN에서 knockout 릴리스

다음 릴리스에서 [Knockout](http://www.knockoutjs.com "Knockout") CDN에서 호스팅됩니다.

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

### <a name="globalize-releases-on-the-cdn"></a>CDN에서 릴리스 세계화

다음 릴리스에서 [Globalize](https://github.com/jquery/globalize "Globalize") CDN에서 호스팅됩니다.

#### <a name="globalize-version-100"></a>버전 1.0.0 세계화

- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/node-main.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/currency.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/date.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/message.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/number.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/plural.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/relative-time.js

#### <a name="globalize-version-011"></a>버전 0.1.1 세계화

- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.min.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.cultures.js

    - 모든 문화권
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.culture.{culture-code}.js

    - "{Code 문화권}" 원하는 문화권 코드를 사용 하 여 대체, globalize.culture.en GB.js== Microsoft CDN에서 파일 하는 예를 들어 이러한 = = 라이브러리는 Microsoft에서 업로드 한 합니다.

<a id="Respond_Releases_on_the_CDN_13"></a>

### <a name="respond-releases-on-the-cdn"></a>CDN에서 릴리스 응답

다음 릴리스에서 [ https://github.com/scottjehl/Respond ] (https://github.com/scottjehl/Respond " https://github.com/scottjehl/Respond ") 응답 CDN에서 호스팅됩니다.

#### <a name="respond-version-142"></a>응답 버전 1.4.2

- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.min.js

#### <a name="respond-version-141"></a>응답 버전 1.4.1

- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.min.js

#### <a name="respond-version-140"></a>응답 버전 1.4.0

- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.min.js

#### <a name="respond-version-130"></a>버전 1.3.0 응답

- https://ajax.aspnetcdn.com/ajax/respond/1.3.0/respond.js

#### <a name="respond-version-120"></a>응답 버전 1.2.0

- https://ajax.aspnetcdn.com/ajax/respond/1.2.0/respond.js

<a id="Bootstrap_Releases_on_the_CDN_14"></a>

### <a name="bootstrap-releases-on-the-cdn"></a>CDN에서 부트스트랩 릴리스

다음 릴리스에서 [getbootstrap.com](http://getbootstrap.com "getbootstrap.com") 부트스트랩 CDN에서 호스팅됩니다.

#### <a name="bootstrap-version-411"></a>부트스트랩 버전 4.1.1

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-400"></a>부트스트랩 버전 4.0.0

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-337"></a>부트스트랩 버전 3.3.7

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

#### <a name="bootstrap-version-336"></a>부트스트랩 버전 3.3.6

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

#### <a name="bootstrap-version-335"></a>부트스트랩 버전 3.3.5

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

#### <a name="bootstrap-version-334"></a>3.3.4 부트스트랩 버전

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

#### <a name="bootstrap-version-332"></a>3.3.2 버전을 부트스트랩

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

#### <a name="bootstrap-version-331"></a>부트스트랩 버전 3.3.1

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

#### <a name="bootstrap-version-330"></a>부트스트랩 버전 3.3.0

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

#### <a name="bootstrap-version-320"></a>부트스트랩 버전 3.2.0

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

#### <a name="bootstrap-version-311"></a>3.1.1 부트스트랩 버전

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

#### <a name="bootstrap-version-310"></a>버전 3.1.0 부트스트랩

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

#### <a name="bootstrap-version-303"></a>부트스트랩 버전 3.0.3

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

#### <a name="bootstrap-version-302"></a>부트스트랩 버전 3.0.2

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

#### <a name="bootstrap-version-301"></a>부트스트랩 버전 3.0.1

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

#### <a name="bootstrap-version-300"></a>부트스트랩 버전 3.0.0

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

#### <a name="bootstrap-version-232"></a>버전 2.3.2를 부트스트랩 합니다.

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings-white.png

#### <a name="bootstrap-version-231"></a>부트스트랩 버전 2.3.1

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings-white.png

<a id="BootstrapTouchCarousel_Releases_on_the_CDN_18"></a>

### <a name="bootstrap-touchcarousel-releases-on-the-cdn"></a>CDN에서 부트스트랩 TouchCarousel 릴리스

다음 릴리스에서 [ https://github.com/ixisio/bootstrap-touch-carousel ] (https://github.com/ixisio/bootstrap-touch-carousel " https://github.com/ixisio/bootstrap-touch-carousel ") 부트스트랩 TouchCarousel 릴리스 CDN에서 호스팅됩니다.

#### <a name="bootstrap-touchcarousel-version-080"></a>부트스트랩 TouchCarousel 버전 0.8.0

- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/css/bootstrap-touch-carousel.css
- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/js/bootstrap-touch-carousel.js

<a id="Hammerjs_Releases_on_the_CDN_19"></a>

### <a name="hammerjs-releases-on-the-cdn"></a>CDN에서 Hammer.js 릴리스

다음 릴리스에서 [ http://hammerjs.github.io/ ] (http://hammerjs.github.io/ " http://hammerjs.github.io/ ") Hammer.js 릴리스 CDN에서 호스팅됩니다.

#### <a name="hammerjs-version-204"></a>Hammer.js 버전 2.0.4

- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.map

<a id="ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15"></a>

### <a name="aspnet-web-forms-and-ajax-releases-on-the-cdn"></a>ASP.NET Web Forms 및 CDN에서 Ajax 릴리스

ASP.NET Ajax 라이브러리의 다음 릴리스에서 CDN에 호스트 됩니다. 파일의 실제 목록을 보려면 각 링크를 클릭 합니다.

- [ASP.NET Web Forms 및 Ajax 버전 4.5.2](cdnajax452.md "ASP.NET Web Forms 및 Ajax 4.5.2")
- [ASP.NET Web Forms 및 Ajax 버전 4](cdnajax4.md "ASP.NET Web Forms 및 Ajax 4")
- [ASP.NET Ajax 버전 3.5](cdnajax35.md "ASP.NET Ajax 3.5")

<a id="ASPNET_MVC_Releases_on_the_CDN_16"></a>

### <a name="aspnet-mvc-releases-on-the-cdn"></a>ASP.NET MVC cdn 해제

다음 ASP.NET MVC JavaScript 파일이이 CDN에서 호스팅됩니다.

#### <a name="aspnet-mvc-523"></a>ASP.NET MVC 5.2.3

- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-51"></a>ASP.NET MVC 5.1

- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-50"></a>ASP.NET MVC 5.0

- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-40"></a>ASP.NET MVC 4.0

- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-30"></a>ASP.NET MVC 3.0

- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.min.js
- https://ajax.aspnetcdn.com/ajax/jquery.unobtrusive-ajax/3.2.5/jquery.unobtrusive-ajax.js
- https://ajax.aspnetcdn.com/ajax/jquery.unobtrusive-ajax/3.2.5/jquery.unobtrusive-ajax.min.js 
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.min.js
- https://ajax.aspnetcdn.com/ajax/jquery.validation.unobtrusive/3.2.10/jquery.validate.unobtrusive.js 
- https://ajax.aspnetcdn.com/ajax/jquery.validation.unobtrusive/3.2.10/jquery.validate.unobtrusive.min.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-20"></a>ASP.NET MVC 2.0

- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-10"></a>ASP.NET MVC 1.0

- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.debug.js

<a id="ASPNET_SignalR_Releases_on_the_CDN_17"></a>

### <a name="aspnet-signalr-releases-on-the-cdn"></a>ASP.NET SignalR cdn 해제

다음 ASP.NET SignalR JavaScript 파일이이 CDN에서 호스팅됩니다.

#### <a name="aspnet-signalr-222"></a>ASP.NET SignalR 2.2.2

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.js

#### <a name="aspnet-signalr-221"></a>ASP.NET SignalR 2.2.1

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.js

#### <a name="aspnet-signalr-220"></a>ASP.NET SignalR 2.2.0

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.js

#### <a name="aspnet-signalr-210"></a>ASP.NET SignalR 2.1.0

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.js

#### <a name="aspnet-signalr-203"></a>ASP.NET SignalR 2.0.3

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.js

#### <a name="aspnet-signalr-202"></a>ASP.NET SignalR 2.0.2

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.js

#### <a name="aspnet-signalr-201"></a>ASP.NET SignalR 2.0.1

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.js

#### <a name="aspnet-signalr-200"></a>ASP.NET SignalR 2.0.0

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.js

#### <a name="aspnet-signalr-113"></a>ASP.NET SignalR 1.1.3

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.js

#### <a name="aspnet-signalr-112"></a>ASP.NET SignalR 1.1.2

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.js

#### <a name="aspnet-signalr-111"></a>ASP.NET SignalR 1.1.1

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.js

#### <a name="aspnet-signalr-110"></a>ASP.NET SignalR 1.1.0

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.js

#### <a name="aspnet-signalr-101"></a>ASP.NET SignalR 1.0.1

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.js

CDN 사용 약관에 대 한 정보를 참조 하세요 [Microsoft Ajax CDN 사용 약관](https://www.asp.net/terms-of-use "Microsoft Ajax CDN 사용 약관")합니다.
