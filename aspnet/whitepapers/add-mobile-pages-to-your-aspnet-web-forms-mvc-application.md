---
uid: whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application
title: "방법: ASP.NET Web Forms에 모바일 페이지를 추가 / MVC 응용 프로그램 | Microsoft Docs"
author: rick-anderson
description: "How To를 ASP.NET Web Forms에서 모바일 장치에 대 한 액세스에 최적화 된 페이지를 처리 하는 다양 한 방법을 설명 / MVC 응용 프로그램 아키텍처를 제안 하 고 및..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/20/2011
ms.topic: article
ms.assetid: 3124f28e-cc32-418a-afe3-519fa56f4c36
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application
msc.type: content
ms.openlocfilehash: aac359b26c508784793a67260dc2e65c30db687a
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="how-to-add-mobile-pages-to-your-aspnet-web-forms--mvc-application"></a>방법: ASP.NET Web Forms에 모바일 페이지를 추가 / MVC 응용 프로그램
====================
> **적용 대상**
> 
> - ASP.NET Web Forms 버전 4.0
> - ASP.NET MVC 버전 3.0
> 
> **요약**
> 
> How To를 ASP.NET Web Forms에서 모바일 장치에 대 한 액세스에 최적화 된 페이지를 처리 하는 다양 한 방법을 설명 / MVC 응용 프로그램 및 아키텍처를 소개 하 고 다양 한 범위의 장치를 대상으로 할 때 고려해 야 할 문제를 디자인 합니다. 이 문서는 또한 3.5에 ASP.NET 2.0에서 ASP.NET 모바일 컨트롤은 이제 사용 되지 하 고에서는 몇 가지 최신 대안을 설명 하는 이유를 설명 합니다.


## <a name="contents"></a>목차

- 개요
- 아키텍처 옵션
- 브라우저 및 장치 검색
- ASP.NET Web Forms 응용 프로그램 관련 모바일 페이지를 나타낼 수 있는 방법
- ASP.NET MVC 응용 프로그램 관련 모바일 페이지를 나타낼 수 있는 방법
- 추가 리소스

ASP.NET Web Forms 및 MVC 모두에 대해이 백서 기법을 보여 주는 다운로드 가능한 코드 샘플 [모바일 앱 및 asp.net 사이트](https://docs.microsoft.com/aspnet/mobile/overview)합니다.

## <a name="overview"></a>개요

휴대폰 – 스마트폰, 기능 전화 및 태블릿 – 웹에 액세스 하는 방법으로 최근의 추세는 계속 합니다. 많은 웹 개발자 및 비즈니스 웹 스타일에 대 한 점점 더 중요 해 해당 장치를 사용 하 여 방문자에 대 한 훌륭한 검색 환경을 제공 하는이 의미 합니다.

### <a name="how-earlier-versions-of-aspnet-supported-mobile-browsers"></a>어떻게 이전 버전의 ASP.NET 지 원하는 모바일 브라우저

ASP.NET 버전 2.0에 3.5 포함 *ASP.NET 모바일 컨트롤*:에서 모바일 장치에 대 한 서버 컨트롤의 집합은 *System.Web.Mobile.dll* 어셈블리 및  *System.Web.UI.MobileControls* 네임 스페이스입니다. 어셈블리는 ASP.NET 4에 여전히 포함 되어 있지만 사용 되지 않습니다. 이 문서에서 설명한 것과 같은 최신 인증 방법으로 마이그레이션할 개발자는 것이 좋습니다.

ASP.NET 모바일 컨트롤 않음으로 표시 된 이유 이유 디자인 2005 및 이전 버전 주위 달리 휴대폰 주위 지향은입니다. 컨트롤은 주로 해당 연대의 WAP 브라우저에 대 한 일반 HTML) (대신 WML 또는 cHTML 태그를 렌더링 하 설계 됩니다. 하지만 WAP, WML, 및 cHTML 더 이상 관련이 대부분의 프로젝트에 대 한 HTML 이제 모바일 및 데스크톱 브라우저의 경우 모두에 게 어디에서 나 태그 언어 바뀌었기 때문에 없습니다.

### <a name="the-challenges-of-supporting-mobile-devices-today"></a>모바일 장치를 오늘 지원 문제

모바일 브라우저 지금은 일반적으로 HTML를 지원 하는 경우에 훌륭한 모바일 검색 경험을 제공 하는 경우 많은 문제 여전히 발생할 것:

- ***화면 크기*** -형태로 크게 다를 모바일 장치 및 화면은 종종 많은 데스크톱 모니터 보다 작습니다. 따라서 완전히 다른 페이지 레이아웃을 디자인 해야 합니다.
- ***메서드 입력*** – 키패드 일부 장치에는, 일부는 styluses, 터치 사용 합니다. 여러 탐색 메커니즘 및 데이터 입력된 방법을 고려해 야 할 수 있습니다.
- ***표준 준수*** – 많은 모바일 브라우저 최신 HTML, CSS 또는 JavaScript 표준을 지원 하지 않습니다.
- ***대역폭*** – 셀룰러 데이터 네트워크 성능을 크게, 다르며는 메가바이트 따라 요금을 청구 관세에 몇 가지 최종 사용자가 있습니다.

만능 방법이 없는; 응용 프로그램 디자인과 액세스 하는 장치에 따라 다르게 작동 해야 합니다. 원하는 모바일 지원 수준에 따라이 "브라우저 전쟁" 바탕 화면을 이전 보다 더 큰 챌린지 웹 개발자를 위한 수 있습니다.

처음에 대 한 모바일 브라우저 지원에 처음 종종 근접 하 고 개발자가 개발자가 개인적으로 종종 등 소유할 아마도 최신 및 정교한 스마트폰 (예: Windows Phone 7, iPhone 또는 Android)을 지원 하기 위해 중요 한만 하다 고 생각 장치입니다. 그러나 저렴 전화는 매우 인기 있는 여전히 하 고 소유자의 휴대폰 광대역 연결 보다 더 쉽게 가져올 수 있는 국가에서 특히 – 웹 사이트를 탐색 하 사용지 않습니다. 비즈니스는 가능성이 높은 고객을 고려 하 여 지 원하는 장치의 범위를 결정 해야 합니다. 아마도 방문객 덜 강력한 기능을 고려해 야는 영화에 대 한 티켓 예약 시스템을 만드는 경우 반면 고급 스마트폰 대상에 비즈니스 결정을 내릴 수 luxury 상태 spa에 대 한 온라인 브로슈어 프로그램을 작성 하는 경우 전화 합니다.

## <a name="architectural-options"></a>아키텍처 옵션

MVC 또는 ASP.NET Web Forms의 특정 기술 세부 정보에 들어가기 전에 웹 개발자에 게 일반적 한지 모바일 브라우저를 지원 하기 위한 세 가지 가능한 옵션 note:

1. ***아무것도 수행 하지 않는*** 표준 데스크톱 중심 웹 응용 프로그램을 만들고을 만족 스럽게 렌더링 하는 모바일 브라우저를 사용 하기만 하면 됩니다. 

    - **장점은**: 것이 가장 저렴 한 옵션을 구현 및 유지 관리 –를 사용한 더 추가 작업
    - **단점은**: 최악의 최종 사용자 환경을 제공 합니다. 

        - 최신 스마트폰 HTML을 데스크톱 브라우저 같이 해석할 수 있습니다 하지만 사용자가 확대/축소 및 스크롤 가로 및 세로로 작은 화면에서 프로그램 콘텐츠를 사용할가 여전히 적용 됩니다. 이 최적의 크게 못 미치는 것입니다.
        - 오래 된 장치 및 기능 휴대폰 만족 스러운 방법으로 태그를 렌더링 되지 않을 수 있습니다.
        - (해당 화면 크기가 랩톱 화면 수 있음) 최신 태블릿 장치에도 다른 상호 작용 규칙이 적용 됩니다. 터치 기반 입력 단추 크기를 확대 가장 적합 확산 더 이상 떨어져 링크 및 플라이 아웃 메뉴 위에 마우스 커서를 놓고 방식은 없습니다.
2. ***클라이언트에서 문제가 해결* –** CSS 신중 하 게 사용 하 여 및 [점진적인 기능 향상](http://en.wikipedia.org/wiki/Progressive_enhancement) 태그, 스타일 및 어떤 브라우저에서 실행 중인에 맞춰 조정 되는 스크립트를 만들 수 있습니다. 예를 들어, [CSS 3 미디어 쿼리](http://www.w3.org/TR/2010/CR-css3-mediaqueries-20100727/)를 가진 스크린은 선택한 임계값 보다 적은 장치에서 단일 열 레이아웃으로 설정 하는 다중 열 레이아웃을 만들 수 있습니다. 

    - **장점은**: 있는 모든 화면 및 입력된 특성에 따라 알 수 없는 이후 장치에 대해서도 사용 중인 특정 장치에 대 한 렌더링을 최적화 합니다.
    - **장점은**:를 사용 하면 모든 장치 유형에 – 코드 또는 작업의 최소 중복을 사용 하 여 서버 쪽 논리가 공유할
    - **단점은**: 모바일 장치는 데스크톱 장치를 실제로 취소할 수 있음을 사용자 데스크톱 페이지에서 완전히 일치 하지 않아도 모바일 페이지 다른 정보를 보여 주는 하므로 다릅니다. 이러한 변형이 비효율적일 수 있습니다 또는 강력 하 게 수행할 수 없는 CSS만을 통해 특히 일관성 없이 방법을 고려 오래 된 장치 해석 CSS 규칙입니다. CSS 3 특성의 경우 특히 그렇습니다.
    - **단점은**: 다양 한 서버 쪽 논리 및 다양 한 장치에 대 한 워크플로 지원 하지 않습니다. 예를 들어 단독 CSS를 사용 하 여 모바일 사용자에 대 한 간단한 쇼핑 카트 체크 아웃 워크플로 구현할 수 없습니다, 있습니다.
    - **단점은**: 비효율적인 대역폭 사용 합니다. 서버 대상 장치는만 해당 정보의 하위 집합을 사용 하는 경우에 태그 및 모든 가능한 장치에 적용 되는 스타일을 전송 해야 할 수 있습니다.
3. ***서버에서 문제를 해결* –** 서버에 어떤 장치에 액세스 하는 것을 알고 있는 경우 또는 화면 크기 및 입력된 방법 같은 해당 장치의 최소 특성 있으며 다른 논리를 실행할 수 있는 모바일 장치-인지 하 고 HTML 태그를 다른 출력입니다. 

    - **장점:** 최대 유연성입니다. 모바일용 서버 쪽 논리를 변경 하거나 원하는, 장치별 레이아웃에 대 한 태그를 최적화 수는 얼마나 제한은 없습니다.
    - **장점:** 효율적으로 대역폭 사용 합니다. 태그 및 대상 장치를 사용 하려고 합니다. 스타일 지정 정보를 전송 하기만 하면 됩니다.
    - **단점:** 경우가 강제로 활동 또는 코드의 반복 (예: 있게 되므로 Web Forms 페이지 또는 MVC 뷰 비슷하지만 약간 다른 복사본을 만들). 여기서 일반적인 논리 기본 계층 또는 서비스 지만 아직도 UI 코드 또는 태그의 일부분으로 팩터링 합니다 가능한 복제 하 고 동시에 관리 해야 할 수 있습니다.
    - **단점:** 장치 감지 간단 하지 않습니다. 목록이 나 알려진된 장치 유형 및 특징 (하지 않을 수 있는 항상 완벽 하 게 최신) 데이터베이스를 필요로 하며 들어오는 모든 요청을 정확 하 게 맞도록 보장 되지 않습니다. 이 문서에서는 몇 가지 옵션 및 해당 문제 해결을 나중에 설명 합니다.

최상의 결과 얻으려면 대부분의 개발자는 옵션 (2) 및 (3)을 결합 하는 데 필요한 사용 합니다. 데이터, 워크플로, 또는 태그의 주요 차이점은 가장 효과적으로 서버 쪽 코드에 구현 하는 반면에 가장 잘 스타일 약간의 차이가 CSS 또는 짝수 JavaScript를 사용 하 여 클라이언트에서 지원 됩니다.

### <a name="this-paper-focuses-on-server-side-techniques"></a>이 백서에서는 서버 쪽 기술

ASP.NET Web Forms 및 MVC 주로 한 서버 쪽 기술에서 모두 이므로이 백서는 다른 태그 및 모바일 브라우저에 대 한 논리를 생성할 수 있는 서버 쪽 기술에 중심 됩니다. 물론, (예: CSS 3 미디어 쿼리를 점진적 향상 JavaScript), 모든 클라이언트 쪽 기술을 사용 하 여 이름을 결합할 수도 있습니다 하지만 ASP.NET 개발 보다 웹 디자인 함의 더입니다.

## <a name="browser-and-device-detection"></a>브라우저 및 장치 검색

모바일 장치를 지원 하기 위한 서버 쪽 기술 모두에 대 한 주요 필수 구성 요소 방문자를 사용 하 여 어떤 장치를 알고 있는 것입니다. 사실, 해당 장치의 제조업체 및 모델 번호 아는 것을 아는 것 보다 더 나은 *특성* 장치입니다. 특성을 포함할 수 있습니다.

- 모바일 장치 입니까?
- 입력된 방법 (예: 마우스/키보드, 터치, 키패드, 조이스틱,...)
- 화면 크기 (물리적으로 및 픽셀 단위)
- 지원 되는 미디어 및 데이터 형식
- 등입니다.

때문에 모델 번호 보다 특징에 기초 하 여 결정을 확인 하는 것이 다음 이후 장치를 처리 하는 데 참조할 수 수 있습니다.

### <a name="using-aspnets-built-in-browser-detection-support"></a>ASP를 사용 합니다. NET의 기본 제공 브라우저 검색 지원

ASP.NET Web Forms 및 MVC 개발자의 속성을 검사 하 여 방문 브라우저의 중요 한 특징을 즉시 검색할 수는 *Request.Browser* 개체입니다. 예를 들어 참조

- Request.Browser.IsMobileDevice
- Request.Browser.MobileDeviceManufacturer, Request.Browser.MobileDeviceModel
- Request.Browser.ScreenPixelsWidth
- Request.Browser.SupportsXmlHttp
- ... 및 다른 많은

내부적으로 ASP.NET 플랫폼 일치 들어오는 *사용자 에이전트* (UA) HTTP 헤더의 브라우저 정의 XML 파일 집합에 정규식에 대 한 합니다. 기본적으로는 플랫폼 많은 일반적인 모바일 장치에 대 한 정의 포함 하 고 인식 하려면 다른 사용자에 대 한 사용자 지정 브라우저 정의 파일을 추가할 수 있습니다. 자세한 내용은 MSDN 페이지를 참조 하십시오. [ASP.NET 웹 서버 컨트롤 및 브라우저 기능](https://msdn.microsoft.com/library/x3k2ssx2.aspx)합니다.

### <a name="using-the-wurfl-device-database-via-51degreesmobi-foundation"></a>51Degrees.mobi Foundation 통해 WURFL 장치 데이터베이스를 사용 하 여

ASP while입니다. NET의 기본 제공 브라우저 검색 지원이 많은 응용 프로그램에 대 한 충분 한 될 다음과 같은 경우 두 개의 주 않을 충분 하지 수 있습니다.

- ***최신 장치 인식 하려는***(해지지 않도록 수동으로 브라우저 정의 파일에). Note.NET 4의 브라우저 정의 파일은 최신 Windows Phone 7, Android 휴대폰, Opera Mobile 브라우저 또는 Apple Ipad를 인식 하지 않습니다.
- ***장치 기능에 대 한 보다 자세한 정보가 필요한***합니다. 장치의 입력된 방법 (예: 터치 vs 키패드)에 대해 알아야 할 수 있습니다 또는 어떤 오디오 형식 브라우저를 지원 합니다. 이 정보는 표준 브라우저 정의 파일에서 사용할 수 없습니다.

[ *무선 유니버설 리소스 파일* (WURFL) 프로젝트](http://wurfl.sourceforge.net/) 훨씬 더 최신 상태 및 세부 정보에서 사용 하 여 모바일 장치에 대 한 현재 유지 관리 합니다.

.NET 개발자를 위한 좋은 소식 해당 ASP입니다. NET의 브라우저 검색 기능을 확장할 수 이므로 이러한 문제를 해결 하기 위해이 함수는 것과 같습니다. 예를 들어 오픈 소스를 추가할 수 있습니다 [ *51Degrees.mobi Foundation* ](https://github.com/51Degrees/dotNET-Device-Detection) 프로젝트에 라이브러리입니다. ASP.NET IHttpModule 또는 브라우저 기능 공급자 (Web Forms 및 MVC 응용 프로그램 모두에 사용할 수 있는)를 직접 WURFL 데이터를 읽고 ASP에 후크하고입니다. NET의 기본 제공 브라우저 검색 메커니즘입니다. 모듈을 설치 했으면 *Request.Browser* 훨씬 더 정확 하 고 자세한 정보가 포함 갑자기 됩니다: 올바르게 여러 앞에서 언급 한 장치를 인식 하 고 해당 기능 (포함 목록 같은 추가 기능 입력된 방법). 자세한 내용은 프로젝트의 설명서를 참조 하십시오.

## <a name="how-web-forms-applications-can-present-mobile-specific-pages"></a>Web Forms 응용 프로그램 관련 모바일 페이지를 나타낼 수 있는 방법

기본적으로 다음과 같습니다 일반적인 모바일 장치에 새 Web Forms 응용 프로그램을 표시 하는 방법.

![](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/_static/image1.png)

명확 하 게 모두 레이아웃은 매우 모바일에서 잘 작동-세로 방향의 작은 화면에 대해 대규모의 가로 방향 모니터에 대 한이 페이지를 디자인 합니다. 따라서 수행할 수 있는 항목에 대 한?

이 백서의 앞에서 설명 했 듯이 여러 가지 방법으로 모바일 장치에 대 한 페이지를 조정할 수 있습니다. 몇 가지 기법에는 서버 기반, 다른 클라이언트에서 실행 합니다.

### <a name="creating-a-mobile-specific-master-page"></a>모바일 별 마스터 페이지 만들기

요구 사항에 따라 있습니다 수 모든 방문자에 대해 동일한 Web Forms를 사용 하지만 개별 마스터 페이지 2: 데스크톱 방문자에 대해 하나, 또 하나는 모바일 방문자에 대 한 합니다. 이 CSS 스타일 시트 또는 최상위 HTML 태그는 페이지 논리를 복제 하는 사용자를 강요 하지 않고도 모바일 장치에 맞게 변경의 유연성을 제공 합니다.

작업을 수행 하는 것과 쉽습니다. 예를 들어 Web Form에 다음과 같은 PreInit 처리기를 추가할 수 있습니다.

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample1.cs)]

이제 응용 프로그램의 최상위 폴더에 Mobile.Master 이라는 마스터 페이지를 만들고 모바일 장치를 검색할 때 사용 됩니다. 모바일 마스터 페이지에는 필요에 따라 모바일 전용 CSS 스타일 시트를 참조할 수 있습니다. 데스크톱 방문자는 기본 마스터 페이지, 모바일 슬라이드가 아니라 여전히 나타납니다.

### <a name="creating-independent-mobile-specific-web-forms"></a>독립 모바일 전용 웹 양식 만들기

유연성을 극대화 이동할 수 있습니다 다른 장치 유형에 대 한 별도 마스터 페이지 보다 훨씬 더 합니다. 두 개를 구현할 수 있습니다 *Web Forms 페이지의 집합을 완전히 분리* – 하나의 데스크톱 브라우저에 대 한 설정, 다른 모바일용 설정 합니다. 이것은 가장 모바일 방문자에 게 매우 다른 정보 또는 워크플로 표시 하려는 경우. 이 섹션의 나머지 부분에서는이 방법을 자세히 설명합니다.

계속 하려면는 가장 쉬운 방법은 모바일 페이지에 프로젝트 내에서 "모바일" 이라는 하위 폴더를 작성 하는 데스크톱 브라우저 하기 위한 Web Forms 응용 프로그램에 이미 있는 경우. 모두 동일한 Web Forms 응용 프로그램에 대해 사용할 수 있는 기술을 사용 하 여 마스터 페이지, 스타일 시트 및 페이지, 전체 하위 사이트를 구성할 수 있습니다. 에 대 한 모바일 동작을 생성 하기 위해 반드시 않아도 *모든* 데스크톱 사이트의 페이지,의 기능 하위 집합 모바일 방문자에 대 한 합리적 선택할 수 있습니다.

모바일 페이지 공용 정적 리소스를 공유할 수 있습니다 (이미지, JavaScript, CSS 등 파일) 하려는 경우 일반 페이지입니다. "모바일" 폴더는 이후 *하지* 표시를 별도 응용 프로그램으로 (이 Web Forms 페이지의 단순 하위 방금) IIS에서 호스팅되는 경우 것도 공유 모두 같은 구성, 세션 데이터 및 기타 인프라와 사용자 데스크톱 페이지입니다.

> [!NOTE]
> 이 일반적으로 방법은 아니지만 일부 코드의 중복 이후 (모바일 페이지는 약간의 유사성이 데스크톱 페이지와 공유할 수)으로 공용 비즈니스 논리 또는 데이터 액세스 코드는 공유 기본 계층 또는 서비스에 분류 해야 합니다. 그렇지 않으면을 만들고 응용 프로그램 유지 관리 하는 작업량 두 번 수행 합니다.


#### <a name="redirecting-mobile-visitors-to-your-mobile-pages"></a>모바일 페이지에 대 한 모바일 방문자 리디렉션

이에 대해서만 모바일 페이지에 모바일 방문자를 리디렉션하려면 편리한 경우가 많습니다는 *첫 번째* 있기 때문에 해당 검색 세션 (및 해당 세션의 모든 요청에 없는), 요청:

- 그런 다음 방금 "데스크톱 버전"로 이동 하는 마스터 페이지에 대 한 링크를 추가-만들려는 경우 데스크톱 프로그램 페이지에 액세스 하려면 모바일 방문자 쉽게 할 수 있습니다. 방문자에에서 있기 때문에 더 이상 첫 번째 요청 세션 모바일 페이지에 다시 리디렉션할 수 없습니다.
- 동적 리소스 (예: 있는 경우 사이트의 데스크톱 및 모바일 부분 IFRAME, 또는 특정 Ajax 처리기에 표시 되는 일반적인 웹 폼) 사이트의 데스크톱 및 모바일 부분 사이 공유에 대 한 요청에 방해가의 위험을 방지 하기

이 위해 리디렉션 논리에 배치할 수 있습니다는 **세션\_시작** 메서드. 예를 들어 Global.asax.cs 파일에 다음 메서드를 추가 합니다.

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample2.cs)]

#### <a name="configuring-forms-authentication-to-respect-your-mobile-pages"></a>모바일 페이지를 준수 하도록 폼 인증 구성

폼 인증에서는 특정 가정을 동안과 그 인증 프로세스 후 방문자 리디렉션할 수 있습니다 위치 하는 방법에 대 한는 note:

- 사용자를 인증 해야 하는 경우 폼 인증 리디렉션됩니다에 데스크톱 또는 모바일 사용자 있는지 여부에 관계 없이 데스크톱 로그인 페이지에 (의 개념을만 있기 때문에 *하나의* 로그인 URL). 모바일 사용자에 게 모바일 별도 로그인 페이지를 리디렉션합니다. 데스크톱 로그인 페이지를 개선 해야 모바일 로그인 페이지를 다르게 스타일을 가정 합니다. 예를 들어 다음 코드를 추가 하면 **데스크톱** 로그인 페이지 코드 숨김: 

    [!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample3.cs)]
- 사용자가 성공적으로 로그인 한 후 폼 인증은 기본적으로 리디렉션됩니다를 데스크톱 홈 페이지 (의 개념을만 있기 때문에 *하나의* 기본 페이지). 성공적으로 로그인 한 후 모바일 홈 페이지로 리디렉션합니다 모바일 로그인 페이지를 개선 해야 합니다. 예를 들어 다음 코드를 추가 하면 **모바일** 로그인 페이지 코드 숨김: 

    [!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample4.cs)]
  
 이 코드 페이지에 기본 프로젝트 템플릿을 같이 LoginUser를를 호출 하는 로그인 서버 컨트롤을 가정 합니다.

### <a name="working-with-output-caching"></a>출력 캐싱을 사용합니다.

출력 캐싱을 사용 하는 경우에 모바일 사용자가 다음 캐시 된 데스크톱 출력을 받는 데스크톱 사용자 (해당 출력을 캐시 하도록 생김) 특정 URL을 방문 하는 기본적으로 다음 있는지 주의 하세요. 이 경고는 방금 장치 유형별로 마스터 페이지에 다양 한 하거나 장치 유형 마다 별도 완전히 Web Forms를 구현 하 고 있는지 여부를 적용 합니다.

이 문제를 방지 하려면 방문자 모바일 장치를 사용 하는지 여부에 따라 캐시 항목을 변경 하는 ASP.NET을 지시할 수 있습니다. 페이지의 OutputCache 선언에 다음과 같이 VaryByCustom 매개 변수를 추가 합니다.

[!code-aspx[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample5.aspx)]

다음으로 정의 *isMobileDevice* Global.asax.cs 파일에 다음 메서드를 추가 하 여 매개 변수 재정의 하는 사용자 지정 캐시:

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample6.cs)]

이렇게 하면 모바일 페이지 방문자가 이전에 데스크톱 방문자가 캐시에 추가한 출력을 수신 하지 않습니다.

### <a name="a-working-example"></a>작업 예제

작업에 이러한 기술의 보려면 다운로드 [이 백서 코드 샘플](https://docs.microsoft.com/aspnet/mobile/overview)합니다. 자동으로 Web Forms 샘플 응용 프로그램 집합 Mobile 이라는 하위 폴더에 있는 모바일 전용 페이지에 모바일 사용자를 리디렉션합니다. 태그와 해당 페이지의 스타일은 다음 스크린샷에서에서 볼 수 있듯이 모바일 브라우저에 대 한 보다 최적화:

![](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/_static/image2.png)

모바일 브라우저에 대 한 태그와 CSS를 최적화 하는 방법에 대 한 자세한 설명에 대 한 "이 문서의 뒷부분에 나오는" 모바일 브라우저에 대 한 모바일 페이지 스타일 지정 섹션을 참조 합니다.

## <a name="how-aspnet-mvc-applications-can-present-mobile-specific-pages"></a>ASP.NET MVC 응용 프로그램 관련 모바일 페이지를 나타낼 수 있는 방법

모델-뷰-컨트롤러 패턴에서는 프레젠테이션 논리 보기의에서 (컨트롤러)에서 응용 프로그램 논리를 분리 하므로 모바일 지원 서버 쪽 코드에서 처리 하는 다음 방법 중 하나에서 선택할 수 있습니다.

1. ***데스크톱 및 모바일 브라우저에 대 한 동일한 컨트롤러와 뷰를 사용 하 하지만 다른 Razor 레이아웃에 따라 장치 유형 *를 사용 하 여 뷰를 렌더링 합니다.** 이 옵션 모든 장치에서 동일한 데이터를 표시 하는 하지만 서로 다른 CSS 스타일 시트를 제공 하거나 모바일용 최상위 HTML 요소를 몇 가지를 변경 하려는 경우에 가장 적합 합니다.
2. ***데스크톱 및 모바일 브라우저에 대해 같은 컨트롤러를 사용 하지만 장치 유형에 따라 서로 다른 뷰를 렌더링***합니다. 표시와 거의 동일한 데이터와 최종 사용자에 대 한 동일한 워크플로 제공 하는 경우이 옵션은 가장 잘 작동 하지만 사용 중인 장치에 맞게 매우 다른 HTML 태그를 렌더링 합니다.
3. ***각각에 대 한 독립적인 컨트롤러와 뷰 구현 데스크톱 및 모바일 브라우저에 대 한 별도 영역을 만들어 * 합니다.** 이 옵션 매우 다른 화면을 표시, 다른 정보가 포함 된와 앞에 자신의 장치 유형에 대 한 액세스에 최적화 된 다양 한 워크플로 통해 사용자는 경우에 가장 적합 합니다. 일부 반복 되는 코드의 의미 하지만 일반적인 논리를 기본 계층 또는 서비스 하 여를 최소화할 수 있습니다.

수행 하려는 경우는 **첫 번째** 옵션 및 Razor 레이아웃만 달라 장치 유형 마다 매우 쉽습니다. 수정 프로그램 \_ViewStart.cshtml 다음과 같이 파일:

[!code-cshtml[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample7.cshtml)]

라는 모바일 전용 레이아웃을 만들 수 이제 \_페이지 구조와 LayoutMobile.cshtml 및 CSS 규칙 모바일 장치에 대해 최적화 합니다.

수행 하려는 경우는 **두 번째** 방문자의 장치 종류에 따라 전혀 다른 뷰를 렌더링 옵션 [Scott Hanselman의 블로그 게시물](http://www.hanselman.com/blog/ABetterASPNETMVCMobileDeviceCapabilitiesViewEngine.aspx)합니다.

이 문서의 나머지 부분에 중점을 두고는 **세 번째** 별도 컨트롤러를 만드는 옵션 – *및* 기능의 하위 집합 모바일 방문자에 대해 제공 되는 정확 하 게 제어할 수 있도록 모바일 장치에 대 한 보기입니다.

### <a name="setting-up-a-mobile-area-within-your-aspnet-mvc-application"></a>ASP.NET MVC 응용 프로그램 내에서 모바일 영역 설정

기존 ASP.NET MVC 응용 프로그램 "모바일" 일반적인 방법으로 불리는 영역을 추가할 수 있습니다: 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 한 다음 추가 à 영역을 선택 합니다. 컨트롤러와 뷰 ASP.NET MVC 응용 프로그램 내의 다른 영역에 대해서와 마찬가지로 추가할 수 있습니다. 예를 들어 모바일 사용자의 지역에 새 컨트롤러를 추가 HomeController 모바일 방문자의 역할 홈 페이지를 호출 합니다.

### <a name="ensuring-the-url-mobile-reaches-the-mobile-homepage"></a>모바일 홈 페이지에 도달 하면 URL /Mobile 보장

모바일 사용자의 지역 내에 HomeController 인덱스 동작을 연결할 URL /Mobile 하려는 경우에 라우팅 구성에 두 개의 약간 변경 해야 합니다. 첫째, MobileAreaRegistration 클래스 있도록 업데이트 HomeController 모바일 해당 지역에서 기본 컨트롤러는 다음 코드에 나와 있는 것 처럼 합니다.

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample8.cs)]

즉 모바일 홈 페이지를 이제 배치할/모바일/홈, 보다는 /Mobile, 이므로 "홈" 이제는 모바일 페이지에 대 한 암시적으로 기본 컨트롤러 이름입니다.

다음으로 두 번째 HomeController에 응용 프로그램 (예: 모바일 하나, 기존 데스크톱 하나 뿐 아니라)를 추가 하면 됩니다을 위반한 것 일반 데스크톱 홈 페이지 note 합니다. 오류가 발생 하 여 실패 합니다 "*여러 형식이 일치 하는 '홈' 라는 컨트롤러*"입니다. 이 해결 하려면 모호 하는 경우 데스크톱 프로그램 HomeController가 우선 순위를 수행 해야 지정 하려면 최상위 라우팅 구성 (Global.asax.cs)에 업데이트 합니다.

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample9.cs)]

오류는 먼, 및 URL http:// 되돌려집니다 이제*yoursite*데스크톱 홈 페이지 및 http://에 도달 하면 /*yoursite*/mobile/ 모바일 홈 페이지에 도달 합니다.

### <a name="redirecting-mobile-visitors-to-your-mobile-area"></a>모바일 방문자 모바일 영역으로 리디렉션

있으므로 리디렉션 논리를 삽입할 수 있는 방법이 다양 하다는 ASP.NET MVC에 여러 다른 확장성 지점의는 있습니다. 특성을 만들려면 필터, [RedirectMobileDevicesToMobileArea] 다음 조건이 충족 될 경우 리디렉션을 수행 하는 한 가지 깔끔한 옵션은:

1. 첫 번째 요청은 사용자의 세션에서 (예: Session.IsNewSession가 true 인)
2. 모바일 브라우저에서 요청 하는 (즉, Request.Browser.IsMobileDevice가 true 인)
3. 사용자가 이미 모바일 영역에 리소스를 요청 하지 않습니다 (즉,는 *경로* URL의 일부 /Mobile로 시작 하지 않으므로)

이 문서에 포함 된 다운로드 가능한 샘플이이 논리의 구현이 포함 되어 있습니다. 권한 부여 필터를 사용 하는 출력 캐싱을 (그렇지 않으면 경우 데스크톱 방문자 첫 번째 액세스 특정 URL 데스크톱 출력 수 캐시 하 고 다음에 제공 하는 경우에 올바르게 처리할 수 있는 AuthorizeAttribute에서 파생 된 함수로 구현 후속 모바일 방문자)입니다.

필터를 그대로 선택할 수 있습니다 특정 컨트롤러 및 작업에 적용 하도록 예:

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample10.cs)]

… MVC 3으로 모든 컨트롤러 및 작업에 적용할 수 있습니다 또는 *전역 필터* Global.asax.cs 파일에:

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample11.cs)]

다운로드 가능한 샘플에는 사용자의 모바일 지역 내에서 특정 위치로 리디렉션하는이 특성의 하위 클래스를 만드는 방법을 보여 줍니다. 즉, 예를 들어 할 수 있습니다.

- 필터를 글로벌 필터로 표시 된 것 처럼 위의 모바일 모바일 홈 페이지 방문자 기본적으로 전송 하는 등록 합니다.
- 요청에 있던 모든 제품 페이지의 모바일 버전에 대 한 모바일 방문자를 사용 하는 "제품" 액션에 특수 [RedirectMobileDevicesToMobileProductPage] 필터도 적용 됩니다.
- 필터의 다른 특별 한 하위 클래스 특정 작업을 해당 하는 모바일 페이지 방문자 모바일 리디렉션에 적용

### <a name="configuring-forms-authentication-to-respect-your-mobile-pages"></a>모바일 페이지를 준수 하도록 폼 인증 구성

폼 인증을 사용 하는 경우 점에 유의 해야 하는 사용자가 로그인 해야 하는 경우 자동으로 사용자 리디렉션합니다. 단일 특정 "로그온" url, 기본적으로 **/계정/로그온**합니다. 즉, 데스크톱 로그온"액션에 모바일 사용자를 리디렉션할 수 수 있습니다.

이 문제를 방지 모바일 "로그온" 작업을를 모바일 사용자에 게 다시 리디렉션합니다 있도록 바탕 화면 "로그온" 액션에 논리를 추가 합니다. ASP.NET MVC 응용 프로그램 템플릿에서 기본값을 사용 하는 경우 다음과 같이 AccountController의 로그온 작업 업데이트.

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample12.cs)]

… 및 다음 AccountController 모바일 사용자의 지역에서 호출 하는 컨트롤러에 적합 한 모바일 전용 "로그온" 동작을 구현 합니다.

### <a name="working-with-output-caching"></a>출력 캐싱을 사용합니다.

[OutputCache] 필터를 사용 하는 경우 장치 종류에 따라 다른 캐시 엔트리의 강제 해야 합니다. 예를 들어 쓰기:

[!code-javascript[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample13.js)]

Global.asax.cs 파일에 다음 메서드를 추가 합니다.

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample14.cs)]

이렇게 하면 모바일 페이지 방문자가 이전에 데스크톱 방문자가 캐시에 추가한 출력을 수신 하지 않습니다.

### <a name="a-working-example"></a>작업 예제

작업에 이러한 기술의 보려면 다운로드 [이 백서 코드 관련 샘플](https://docs.microsoft.com/aspnet/mobile/overview)합니다. 샘플 위에 설명 된 메서드를 사용 하 여 모바일 장치를 지원 하도록 향상 되었습니다 (릴리스 후보) ASP.NET MVC 3 응용 프로그램에 포함 되어 있습니다.

## <a name="further-guidance-and-suggestions"></a>추가 설명서 및 제안

다음 논의는 Web Forms 및 MVC 개발자에 게이 문서에서 설명 하는 기술을 사용 하는에 모두 적용 됩니다.

### <a name="enhancing-your-redirection-logic-using-51degreesmobi-foundation"></a>51Degrees.mobi Foundation을 사용 하 여 리디렉션 논리 강화

이 문서에 설명 된 리디렉션 논리 완벽 하 게 응용 프로그램에 대 한 충분 한 수 있지만 지정된 된 요청 하는지 여부를 알 수 없고 하기 때문에 (세션 이러한 가질 수 없습니다) 쿠키를 거부 하는 모바일 브라우저는 또는 세션을 사용 하지 않도록 설정 하는 경우 작동 하지 않습니다. 해당 방문자에서 첫 번째입니다.

이미 오픈 소스 51Degrees.mobi Foundation ASP의 정확도 개선할 수 있는 방법을 배웠습니다. NET의 브라우저 검색 합니다. 또한 기본 제공 모바일 방문자가 Web.config에 구성 된 특정 위치로 리디렉션할 수가 있습니다. ASP.NET 세션에 따라 없이 작업 수 (및이 따른 쿠키)의 방문자의 HTTP 헤더 및 IP 주소 해시 임시 로그를 저장 하 여이 알 수 있도록 각 요청에 지정 된 vistor에서 첫 번째 인지 여부입니다.

Web.config 파일의 fiftyOne 섹션에 추가 된 다음 요소는 페이지에 검색 된 모바일 장치에서 첫 번째 요청을 리디렉션합니다 ~ / Mobile/Default.aspx 합니다. 모바일 폴더 아래에 있는 페이지에 있는 모든 요청은 *하지* 장치 종류에 관계 없이 리디렉션할 수 있습니다. 모바일 장치가 비활성 상태인 동안 20 분 또는 장치를 더을 잊지 않고 및 후속 요청 리디렉션을 위해 새로으로 처리 됩니다.

[!code-xml[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample15.xml)]

자세한 내용은 참조 하십시오. [51degrees.mobi Foundation 설명서](https://github.com/51Degrees/dotNET-Device-Detection)합니다.

> [!NOTE]
> 하면 *수* ASP.NET MVC 응용 프로그램 에서만 사용 하 여 51Degrees.mobi Foundation 리디렉션 기능 하지 라우팅 매개 변수를 기준으로 하거나 MVC 필터를 배치 하 여 일반 Url 기준으로 리디렉션 구성에 정의 해야 합니다 작업 합니다. ¿¡´ (작성 당시의) 필터 또는 라우팅 51Degrees.mobi Foundation 인식 하지 못합니다.


### <a name="disabling-transcoders-and-proxy-servers"></a>트랜스코더 및 프록시 서버를 사용 하지 않도록 설정

모바일 네트워크 운영자의 진행 방식 모바일 인터넷에서에서 광범위 한 두 가지 목표를가지고 있습니다.

1. 가능한 훨씬 관련 콘텐츠 제공
2. 제한 된 무선 네트워크 대역폭을 공유할 수 있는 고객의 수를 최대화 합니다.

많은 연산자를 사용 하는 대부분의 웹 페이지 큰 데스크톱의 화면 및 고정 줄 빠른 광대역 연결을 위한 디자인에 있으므로 *트랜스코더* 또는 *프록시 서버* 웹 콘텐츠를 동적으로 변경 합니다. HTML 태그나 CSS (특히 휴대폰용"기능" 복잡 한 레이아웃을 처리 하는 처리 기능이 없는), 보다 작은 화면에 맞게 수정할 수 있습니다 및 페이지 배달 속도 개선 하기 위해 (의 품질을 저하 크게) 이미지 다시 압축할 수 있습니다.

하지만 모바일 액세스에 최적화 된 버전의 사이트를 생성 하기 위해 노력을 얻 었을 하는 경우 원하지 않을 것 방해가 모든 추가 네트워크 운영자입니다. 페이지에 다음 줄을 추가할 수 있습니다\_모든 ASP.NET Web Form의 로드 이벤트:

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample16.cs)]

또는 ASP.NET MVC 컨트롤러의 경우 추가할 수 해당 컨트롤러에서 모든 작업에 적용 되도록 다음 메서드 재정의:

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample17.cs)]

결과 HTTP 메시지 W3C 호환 트랜스코더 한 내용을 변경 하지는 프록시에 알립니다. 물론, 보장이 없습니다 모바일 네트워크 운영자가이 메시지를 적용 합니다.

### <a name="styling-mobile-pages-for-mobile-browsers"></a>모바일 브라우저에 대 한 모바일 페이지 스타일 지정

이 문서에 상세하게에서 설명의 범위를 벗어나지만 어떤 종류의 HTML 태그 작업 올바르게 나 특정 장치에 대 한 유용성을 최대화 하는 어떤 웹 디자인 기술이 있습니다. 충분히 단순 레이아웃을 찾을 수를 최적화 모바일 크기의 화면에 대 한 신뢰할 수 없는 사용 하지 않고 HTML 또는 CSS 요령 위치 합니다. 그러나는 주의 해야 하 고, 중요 한 기술이 고 *뷰포트 메타 태그*합니다.

"뷰포트"이 라고도 하는 가상 캔버스에서 페이지를 렌더링 하는 데스크톱 모니터에 대 한 의미는 노력 디스플레이 웹 페이지에서 특정 최신 모바일 브라우저 (예: 가상 뷰포트는 iphone, 너비가 980 픽셀이 고 850 픽셀이 고 Opera Mobile에 기본적으로) 한 다음 화면의 실제 픽셀에 맞게 결과 축소 합니다. 사용자 다음 확대 하 여 해당 뷰포트 주변 합니다. 이 이점이 브라우저의 의도 된 레이아웃에 페이지를 표시할 수 있습니다 하지만 또한 한다는 단점이 확대/축소 및 이동 강제로 사용자에 대 한 편리한 않은 합니다. 모바일 앱을 위해 디자인할 경우 것이 좋습니다 디자인 좁은 화면에 대 한 확대/축소 없음이나 가로 스크롤 필요 않도록 합니다.

뷰포트 너비 여야 합니다 모바일 브라우저에 지시 하는 방법은 비표준 통해는 *뷰포트* 메타 태그입니다. 예를 들어, 다음 페이지의 H e a d 섹션을 추가 하는 경우

[!code-html[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample18.html)]

… 그런 다음 스마트폰 브라우저를 지 원하는 480 픽셀 넓은 가상 캔버스에서 페이지 레이아웃 됩니다. 즉, HTML 요소 너비가 (%)을 정의 하는 경우 백분율이 기본 뷰포트 너비가 480 픽셀 너비를 기준으로 해석 됩니다. 결과적으로, 사용자가 확대/축소 및 가로로 – 상당히 향상 모바일 탐색 환경 이동 해야 할 가능성이 더 낮아집니다.

뷰포트 너비 장치의 물리적 픽셀 일치 하도록 하려는 경우 다음을 지정할 수 있습니다.

[!code-html[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample19.html)]

이 제대로 수행 되지 명시적으로 강제 해야 해당 너비를 초과 하는 요소 (예:를 사용 하 여는 *너비* 특성 또는 CSS 속성), 브라우저에 관계 없이 더 큰 뷰포트를 사용 하 고, 그렇지 정해 집니다. 참고 항목: [비표준 뷰포트 태그에 대 한 자세한 내용은](https://developer.apple.com/library/safari/#documentation/AppleApplications/Reference/SafariHTMLRef/Articles/MetaTags.html)합니다.

대부분의 요즘 스마트폰 지원 *이중 방향*: 세로 또는 가로 모드에서 보유할 수 있습니다. 따라서는 픽셀 단위로 화면 너비에 대 한 가정을 하지 해야 합니다. 페이지에는 사용자가 장치 안내 다시 수 때문에 화면 너비 고정 되도록 가정도 하지 마십시오.

콘텐츠 라고 알려 페이지 헤더에는 다음 메타 태그 모바일 앱을 위해 최적화 된와 따라서 변환 되지 않아야에 이전 Windows Mobile 및 Blackberry 장치 허용할 수 있습니다.

[!code-html[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample20.html)]

## <a name="additional-resources"></a>추가 리소스

모바일 장치 에뮬레이터 및 시뮬레이터 모바일 ASP.NET 웹 응용 프로그램을 테스트 하는 데 사용할 수는 목록에 대 한 페이지 참조 [시뮬레이션 테스트를 위한 인기 있는 모바일 장치](../mobile/device-simulators.md)합니다.

## <a name="credits"></a>크레딧

- 기본 작성자: 서 Sanderson
- 검토자 추가 / 콘텐츠 작성자: James Rosewell, Mikael Söderström, Scott Hanselman, Scott 헌터
