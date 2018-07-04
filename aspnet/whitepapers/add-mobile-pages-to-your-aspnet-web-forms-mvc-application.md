---
uid: whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application
title: '방법: ASP.NET Web forms에 모바일 페이지 추가 / MVC 응용 프로그램 | Microsoft Docs'
author: rick-anderson
description: 이 방법에 ASP.NET Web Forms에서 모바일 장치에 대 한 액세스에 최적화 된 페이지를 제공 하는 다양 한 방법에 설명 / MVC 응용 프로그램 아키텍처를 제안 하 고...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/20/2011
ms.topic: article
ms.assetid: 3124f28e-cc32-418a-afe3-519fa56f4c36
ms.technology: ''
msc.legacyurl: /whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application
msc.type: content
ms.openlocfilehash: 075329087cb5e07d85bba0c546538e7cc55ac463
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37366759"
---
<a name="how-to-add-mobile-pages-to-your-aspnet-web-forms--mvc-application"></a>방법: ASP.NET Web forms에 모바일 페이지 추가 / MVC 응용 프로그램
====================
> **적용 대상**
> 
> - ASP.NET Web Forms 버전 4.0
> - ASP.NET MVC 버전 3.0
> 
> **요약**
> 
> 이 방법에 ASP.NET Web Forms에서 모바일 장치에 대 한 액세스에 최적화 된 페이지를 제공 하는 다양 한 방법에 설명 / MVC 응용 프로그램 아키텍처를 제안 하 고 광범위 한 장치를 대상으로 할 때 고려해 야 할 문제를 디자인 합니다. 이 문서는 또한 3.5 ASP.NET 2.0에서 ASP.NET 모바일 컨트롤은 사용 되지 않는 이제 이유와 일부 최신 대안을 설명 설명 합니다.


## <a name="contents"></a>목차

- 개요
- 아키텍처 옵션
- 브라우저 및 장치 검색
- ASP.NET Web Forms 응용 프로그램에서 모바일 전용 페이지를 제공할 수는 어떻게
- ASP.NET MVC 응용 프로그램에서 모바일 전용 페이지를 제공할 수는 방법
- 추가 자료

ASP.NET Web Forms 및 MVC에 대 한이 백서에서는이 기법을 보여 주는 다운로드 가능한 코드 샘플을 보려면 [Mobile Apps 및 ASP.NET 사용 하 여 사이트](https://docs.microsoft.com/aspnet/mobile/overview)합니다.

## <a name="overview"></a>개요

휴대폰 – 스마트폰, 기능 스마트폰 및 태블릿은 – 계속 웹에 액세스 하는 수단으로 널리 사용 되 고 증가 합니다. 많은 웹 개발자 및 웹 지향 기업에서 해당 장치를 사용 하 여 방문자에 대 한 뛰어난 검색 환경을 제공 하려면 점점 더 중요 한 것을 의미 합니다.

### <a name="how-earlier-versions-of-aspnet-supported-mobile-browsers"></a>어떻게 이전 버전의 지원 되는 ASP.NET 모바일 브라우저

ASP.NET 버전 2.0에 3.5 포함 *ASP.NET 모바일 컨트롤*: 모바일 장치에 대 한 서버 컨트롤의 집합을 *System.Web.Mobile.dll* 어셈블리 및  *System.Web.UI.MobileControls* 네임 스페이스입니다. 어셈블리는 ASP.NET 4에 여전히 포함 되어 있지만 사용 되지 않습니다. 개발자는이 문서에 설명 된 것과 같은 최신 방법 마이그레이션할 것이 좋습니다.

ASP.NET 모바일 컨트롤 사용 되지 않음으로 표시 된 이유는 이유는 해당 디자인은 2005 및 이전 버전 관련 일반적 사용 되 던 휴대폰 지향는입니다. 컨트롤은 주로 해당 연대의 WAP 브라우저에 대 한 일반 HTML) (대신 cHTML 또는 WML 태그를 렌더링 하도록 설계 됩니다. 하지만 WAP, WML 및 cHTML와 관련 없는 대부분의 프로젝트에 대 한 HTML에서 모두 모바일 및 데스크톱 브라우저의 유비쿼터스 태그 언어 이제 바뀌었기 때문에 없습니다.

### <a name="the-challenges-of-supporting-mobile-devices-today"></a>지금 모바일 장치 지원 문제

모바일 브라우저 이제 거의 보편적으로 HTML을 지원 하는 경우에 여전히 많은 문제 때 발생할 모바일 훌륭한 검색 환경을 만들을 찾아내기 위한:

- ***화면 크기*** -모바일 장치 형태로 매우 다양 하 고 해당 화면 경우가 대부분 데스크톱 모니터 보다 작습니다. 따라서에 완전히 다른 페이지 레이아웃을 디자인 해야 합니다.
- ***메서드 입력*** – 일부 장치 키패드, 일부 styluses로 있는 다른 사용자가 터치를 사용 합니다. 여러 탐색 메커니즘 및 데이터 입력된 메서드를 고려를 해야 합니다.
- ***표준 준수*** – 다양 한 모바일 브라우저에 HTML, CSS 또는 JavaScript 최신 표준을 지원 하지 않습니다.
- ***대역폭*** – 셀룰러 데이터 네트워크 성능을 상당히, 다르며 관세는 메가바이트도 요금을 청구 하는 몇 가지 최종 사용자가 있습니다.

모든 상황에 맞는 솔루션이 없습니다. 응용 프로그램을 찾아서 액세스 하는 장치에 따라 다르게 작동 해야 합니다. 원하는 모바일 지원 수준에 따라 보다 "브라우저 전쟁" 데스크톱 어느 웹 개발자를 위한 더 큰 문제 수 있습니다.

처음에 대 한 모바일 브라우저 지원 종종 처음 접하는 개발자 등는 개발자가 종종 개인적으로 소유 하기 때문에 (예: Windows Phone 7, iPhone 또는 Android), 최신 및 가장 정교한 스마트폰 등 지원만 반드시 생각 장치입니다. 그러나 저렴 한 휴대폰 여전히 매우 인기 있는 되며 소유자의 수행 하는 데 사용할 웹을에서 탐색 합니다 – 특히 휴대폰 광대역 연결 보다 더 쉽게 가져올 수 있는 국가. 비즈니스는 다양 한 가능성이 높은 고객을 고려 하 여 지 원하는 장치를 결정 해야 합니다. 아마도 덜 강력한 기능을 사용 하 여 방문자 고려해 야는 영화에 대 한 티켓 예약 시스템을 만들 경우 반면 고급 smartphone을 대상에 비즈니스 결정을 내릴 수 luxury 상태 spa에 대 한 온라인 브로슈어 프로그램을 빌드하는 경우 휴대폰입니다.

## <a name="architectural-options"></a>아키텍처 옵션

ASP.NET Web Forms 또는 MVC의 특정 기술 세부 정보를 시작 하기 전에 웹 개발자에 게 일반적 있는 모바일 브라우저 지원에 대 한 세 가지 가능한 옵션 note:

1. ***작업 안 함 –*** 단순히 표준 데스크톱 지향 웹 응용 프로그램을 만들고 하 만족 스럽게 렌더링 하는 모바일 브라우저를 사용 합니다. 

    - **장점은**: 것이 가장 저렴 한 옵션을 구현 및 유지 관리 – 더 추가 작업
    - **단점은**: 최악의 최종 사용자 환경을 제공 합니다. 

        - 최신 스마트폰 데스크톱 브라우저와 같이 HTML을 렌더링할 수 있지만 가로로 스크롤하여 확대/축소를 세로로 작은 화면에서 콘텐츠를 사용 하려면 사용자는 강제로 계속 합니다. 이 최적의 멀리입니다.
        - 이전 장치와 휴대폰 중 에서도 만족 스러운 방식으로 태그를 렌더링 하 실패할 수 있습니다.
        - (해당 화면 랩톱 화면 같은 대규모 일 수 있음) 최신 태블릿 장치에도 다양 한 상호 작용 규칙이 적용 됩니다. 터치 기반 입력 큰 단추를 사용 하 여 가장 잘 작동 spread 더 떨어져 있으므로, 링크 및 플라이 아웃 메뉴를 마우스 커서로 가리킨 방법이 있습니다.
2. ***클라이언트에서 문제를 해결할* –** CSS 신중 하 게 사용 하 여 및 [점진적인 기능 향상](http://en.wikipedia.org/wiki/Progressive_enhancement) 태그, 스타일 및 원하는 브라우저를 실행 하 고 조정 하는 스크립트를 만들 수 있습니다. 예를 들어 [CSS 3 미디어 쿼리](http://www.w3.org/TR/2010/CR-css3-mediaqueries-20100727/), 해당 화면 선택한 임계값 보다 좁아집니다. 장치에서 단일 열 레이아웃으로 전환 하는 여러 열 레이아웃을 만들 수 있습니다. 

    - **장점은**:가 원하는 화면 및 입력된 특성에 따라 향후 장치의 알 수 없는 경우에 사용 중인 특정 장치에 대 한 렌더링 최적화
    - **장점은**: 쉽게 코드 또는 작업의 최소 중복 – 모든 장치 유형에 서 서버 쪽 논리를 공유할 수 있습니다
    - **단점은**: 모바일 장치는 다른 데스크톱 장치 수 원하는 데스크톱 페이지와 완전히 다르게 모바일 페이지에 다양 한 정보를 표시 합니다. 이러한 변형 비효율적일 수 있습니다 또는 안정적으로 달성 하기 위해 불가능 한 단독으로 CSS를 통한 특히 일관 되지 않게 하는 방법을 고려 이전 장치 해석 CSS 규칙입니다. CSS 3 특성의 경우 특히 그렇습니다.
    - **단점은**: 다양 한 서버측 논리 및 다른 장치에 대 한 워크플로 지원 하지 않습니다. 예를 들어 CSS만을 사용 하 여 모바일 사용자에 대 한 간단한 쇼핑 카트 체크 아웃 워크플로 구현할 수 없습니다, 있습니다.
    - **단점은**: 비효율적인 대역폭 사용 합니다. 서버는 대상 장치는만 해당 정보의 하위 집합을 사용 하는 경우에 태그 및 모든 가능한 장치에 적용 되는 스타일을 전송 해야 할 수 있습니다.
3. ***서버에서 문제를 해결할* –** 서버 장치에 액세스 하는 – 알고 있는 경우 또는 화면 크기와 입력된 방법, 예: 장치의 최소 특성 다른 논리를 실행할 수 있는 모바일 장치 – 인지 여부 및 HTML 태그를 다른 출력입니다. 

    - **장점:** 최대 유연성. 모바일에 대 한 서버 쪽 논리를 다 최적화 하려는 경우에 장치 특정 레이아웃에 대 한 태그 수는 얼마나에 제한은 없습니다.
    - **장점:** 효율적인 대역폭 사용 합니다. 태그 및 대상 장치를 사용할 것 스타일 정보를 전송 해야 합니다.
    - **단점:** 반복 활동의 코드를 강제로 경우가 있습니다 (예: 만들기 Web Forms 페이지의 MVC 보기와 유사 하지만 약간 다른 복사본을 만들 수)입니다. 여기서는 기본 계층 또는 서비스 되지만 여전히 UI 코드 또는 태그의 일부 일반적인 논리 팩터링는 가능한 중복 되어 병렬로 다음 유지 관리 해야 합니다.
    - **단점:** 장치 검색은 결코 간단치있지 않습니다. 목록 또는 알려진된 장치 유형 및 해당 특성 (하지 않을 수 있는 항상 완벽 하 게 최신)의 데이터베이스를 필요로 하며 들어오는 모든 요청을 정확 하 게 일치 하도록 보장할 수 없습니다. 이 문서 뒷부분 몇 가지 옵션 및 해당 문제에 설명합니다.

최상의 결과 얻으려면 대부분의 개발자 옵션 (2) 및 (3)를 결합 해야 찾습니다. 약간의 차이가 있기는 스타일 데이터, 워크플로 또는 태그의 주요 차이점은 서버 쪽 코드로 가장 효과적으로 구현 하는 반면에 가장 CSS 또는 심지어 JavaScript를 사용 하는 클라이언트에 적용 됩니다.

### <a name="this-paper-focuses-on-server-side-techniques"></a>이 백서에서는 서버 쪽 기술

ASP.NET Web Forms 및 MVC에 모두 기본적으로 서버 쪽 기술 되므로이 백서에서는 다른 태그 및 모바일 브라우저에 대 한 논리를 생성할 수 있는 서버 쪽 기술을 중점적 합니다. 물론 모든 클라이언트 쪽 기술 (예를 들어, CSS 3 미디어 쿼리를 점진적으로 개선 JavaScript)를 사용 하 여이 결합할 수 있지만 ASP.NET 개발 보다 웹 디자인 몇 개입니다.

## <a name="browser-and-device-detection"></a>브라우저 및 장치 검색

모바일 장치를 지원 하기 위해 모든 서버 쪽 기술에 대 한 키 필수 구성 요소는 방문자를 사용 하 여 장치를 알아야 합니다. 사실, 해당 장치의 제조업체 및 모델 번호를 알고를 아는 것 보다 더 나은 합니다 *특징* 장치. 특성이 포함 될 수 있습니다.

- 모바일 장치 입니까?
- 입력된 메서드 (마우스/키보드, 터치, 키패드, 조이스틱,...)
- 화면 크기 (실제로 및 픽셀)
- 지원 되는 미디어 및 데이터 형식
- 등

때문에 모델 번호 특성을 기반으로 결정을 확인 하는 것이 좋습니다 다음 이후 장치를 처리 하는 데 참조할 수 수 있습니다.

### <a name="using-aspnets-built-in-browser-detection-support"></a>ASP를 사용합니다. NET의 기본 제공 브라우저 검색 지원

ASP.NET Web Forms 및 MVC 개발자의 속성을 검사 하 여 방문 브라우저의 중요 한 특징을 즉시 검색할 수는 *Request.Browser* 개체입니다. 예를 들어, 참조

- Request.Browser.IsMobileDevice
- Request.Browser.MobileDeviceManufacturer, Request.Browser.MobileDeviceModel
- Request.Browser.ScreenPixelsWidth
- Request.Browser.SupportsXmlHttp
- ... 및 기타

내부적으로 ASP.NET 플랫폼 일치 들어오는 *User-agent* 브라우저 정의 XML 파일 집합의 정규식에 대해 (UA) HTTP 헤더입니다. 기본적으로 플랫폼 많은 일반적인 모바일 장치에 대 한 정의 포함 하 고 인식 하려면 다른 사용자에 대 한 사용자 지정 브라우저 정의 파일을 추가할 수 있습니다. 자세한 내용은 MSDN 페이지를 참조 하세요 [ASP.NET 웹 서버 컨트롤 및 브라우저 기능](https://msdn.microsoft.com/library/x3k2ssx2.aspx)합니다.

### <a name="using-the-wurfl-device-database-via-51degreesmobi-foundation"></a>51Degrees.mobi Foundation 통해 장치가 WURFL 데이터베이스를 사용 하 여

ASP while입니다. NET의 기본 제공 브라우저 검색 지원 대부분의 응용 프로그램에 적합 하도록 두 가지 주요 사례가 하는 충분 하지 않을 경우:

- ***최신 장치를 인식 하려면***(하지 않고 해당 브라우저 정의 파일을 수동으로 만드는). .NET 4의 브라우저 정의 파일은 Windows Phone 7, Android 휴대폰, Opera Mobile 브라우저 또는 Apple Ipad를 인식할 수 있는 최신 하지 note 합니다.
- ***장치 기능에 대 한 자세한 정보가 필요한***합니다. 장치의 입력된 방법 (예: 터치 vs 키패드)를 파악 해야 하거나 어떤 오디오 형식 브라우저를 지원 합니다. 이 정보는 표준 브라우저 정의 파일에서 사용할 수 없습니다.

합니다 [ *무선 범용 리소스 파일* (WURFL) 프로젝트](http://wurfl.sourceforge.net/) 훨씬 더 많은 최신 및 세부 정보에서 사용 하 여 모바일 장치에 대 한 현재 유지 관리 합니다.

.NET 개발자를 위한 좋은 소식은 해당 ASP 합니다. 이러한 문제를 해결 하 고 향상 시킬 수 이므로 NET의 브라우저 검색 기능을 사용 하는 것이 확장 가능 합니다. 예를 들어, 오픈 소스를 추가할 수 있습니다 [ *51Degrees.mobi Foundation* ](https://github.com/51Degrees/dotNET-Device-Detection) 라이브러리 프로젝트. ASP.NET IHttpModule 또는 브라우저 기능 공급자 (Web Forms 및 MVC 응용 프로그램에서 사용할 수)를 직접 WURFL 데이터를 읽고 ASP에 연결 하는 것입니다. NET의 기본 제공 브라우저 감지 메커니즘입니다. 모듈을 설치 했으면 *Request.Browser* 훨씬 더 정확 하 고 자세한 정보가 포함 갑자기 됩니다: 올바르게 여러 앞에서 언급 한 장치를 인식 하 고 해당 기능 (포함 목록 추가 기능 입력된 메서드 등). 자세한 내용은 프로젝트의 설명서를 참조 하세요.

## <a name="how-web-forms-applications-can-present-mobile-specific-pages"></a>Web Forms 응용 프로그램에서 모바일 전용 페이지를 제공할 수는 어떻게

기본적으로 다음과 같습니다. 일반적인 모바일 장치에서 새로운 Web Forms 응용 프로그램을 표시 하는 방법

![](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/_static/image1.png)

물론 모두 레이아웃은 매우 모바일에서 잘 작동 하는 "을 찾습니다. –이 페이지는 작은 세로 방향의 화면 대 한 대규모의 가로 방향 모니터에 대 한 설계 되었습니다. 따라서 수행할 수 있는 것?

이 문서 앞부분에서 설명 했 듯이 모바일 장치에 대 한 페이지에 맞게 여러 가지가 있습니다. 몇 가지 기법에는 서버 기반, 다른 클라이언트에서 실행 합니다.

### <a name="creating-a-mobile-specific-master-page"></a>모바일 별 마스터 페이지 만들기

요구 사항에 따라 수 있습니다 모든 방문자에 대 한 동일한 Web Forms를 사용 하지만 마스터 페이지를 별도 두 가지: 데스크톱 방문자에 대 한 하나이 고, 다른 모바일 방문자입니다. 이 CSS 스타일 시트 또는 모든 페이지 논리를 복제 하지 않고도 모바일 장치에 맞게 최상위 HTML 태그를 변경 하는 유연성을 제공 합니다.

작업을 수행 하는 것과 쉽습니다. 예를 들어, Web Form에 다음과 같이 PreInit 처리기를 추가할 수 있습니다.

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample1.cs)]

이제 응용 프로그램의 최상위 폴더에 Mobile.Master 라는 마스터 페이지를 만들고 모바일 장치를 검색할 때 사용 됩니다. 모바일 마스터 페이지에는 필요한 경우 모바일 전용 CSS 스타일 시트를 참조할 수 있습니다. 데스크톱 방문자는 모바일 한 없습니다 기본 마스터 페이지를 계속 나타납니다.

### <a name="creating-independent-mobile-specific-web-forms"></a>독립 모바일 전용 웹 양식 만들기

최대 유연성을 진행할 수 있습니다 훨씬 장치 유형 마다 별도 마스터 페이지를 방금 것입니다. 두 개를 구현할 수 있습니다 *Web Forms 페이지를 완전히 분리* 하나 – 모바일용 다른 설정에 대해 데스크톱 브라우저 설정 합니다. 이 가장 좋습니다 모바일 방문자에 게 매우 다른 정보 또는 워크플로 제공 하려는 경우. 이 단원의 나머지 부분에서는이 방법을 자세히 설명합니다.

계속 하는 가장 쉬운 방법은 프로젝트 내에서 "Mobile" 라는 하위 폴더를 만들고 모바일 페이지에 구축 하는 데스크톱 브라우저를 위한 Web Forms 응용 프로그램을를 이미가지고 있다고 가정 합니다. 동일한 Web Forms 응용 프로그램에 대해 사용할 수 있는 기술을 사용 하 여 자체 마스터 페이지, 스타일 시트 및 페이지를 사용 하 여 전체 하위 사이트를 구성할 수 있습니다. 에 대 한 모바일과 같은 기능을 생성할 필요가 없습니다 *마다* 데스크톱 사이트에서 페이지; 모바일 방문자에 게 적절 한 기능의 하위 집합을 선택할 수 있습니다.

모바일 페이지에서 공용 정적 리소스를 공유할 수 있습니다 (예: 이미지, JavaScript 또는 CSS 파일) 하려는 경우 일반 페이지를 사용 하 여 합니다. "Mobile" 폴더는 이후 *되지* 표시할 별도 응용 프로그램으로 (Web Forms 페이지의 간단한 하위 방금는) IIS에서 호스팅되는 경우이 공유할 수도 모두 동일한 구성, 세션 데이터 및 기타 인프라와 사용자 데스크톱 페이지입니다.

> [!NOTE]
> 이 방법은 일반적으로 코드의 일부 중복을 포함 하므로 (모바일 페이지 가능성이 데스크톱 페이지를 사용 하 여 일부 유사성을 공유), 모든 일반적인 비즈니스 논리 또는 데이터 액세스 코드 공유 기본 계층 또는 서비스에 대 한 비율을 고려해 야 합니다. 그렇지 않으면 double 만들고 응용 프로그램 유지 관리 작업 표시 됩니다.


#### <a name="redirecting-mobile-visitors-to-your-mobile-pages"></a>모바일 페이지에 리디렉션 모바일 방문자

에 대해서만 모바일 방문자 모바일 페이지로 리디렉션합니다 하면 편리한 경우가 합니다 *첫 번째* 하므로 해당 브라우저 세션 (및 해당 세션에서 모든 요청에 없는)에서 요청:

- 그런 다음 자신이 – 방금 "데스크톱 버전"으로 이동 하는 마스터 페이지에 대 한 링크를 추가 하는 경우 데스크톱 프로그램 페이지에 액세스 하려면 모바일 방문자를 쉽게 할 수 있습니다. 방문자 이기 때문에 더 이상 첫 번째 요청은 해당 세션에서 모바일 페이지에 다시 리디렉션할 수 없습니다.
- (예를 들어 있는 경우 데스크톱 및 모바일 사이트 부분을 IFRAME에 특정 Ajax 처리기를 표시 하는 일반적인 Web Form) 사이트의 데스크톱 및 모바일 구성 요소 간에 공유 되는 모든 동적 리소스에 대 한 요청을 방해 위험을 방지 하기

이렇게 하려면에서 리디렉션 논리를 배치할 수 있습니다는 **세션\_시작** 메서드. 예를 들어 Global.asax.cs 파일에 다음 메서드를 추가 합니다.

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample2.cs)]

#### <a name="configuring-forms-authentication-to-respect-your-mobile-pages"></a>모바일 페이지를 준수 하도록 폼 인증 구성

폼 인증 하는 동안 및 인증 프로세스 후 방문자 리디렉션할 수 있습니다 위치에 대 한 특정 가정을 note:

- 사용자를 인증 해야 하는 경우 폼 인증 리디렉션됩니다 해당 데스크톱 또는 모바일 사용자 있는지 여부에 관계 없이 데스크톱 로그인 페이지에 (개념이 있어 *하나의* 로그인 URL). 다르게 모바일 로그인 페이지의 스타일을 지정 하 려 한다고 가정 하므로, 모바일 사용자에 게 모바일 별도 로그인 페이지로 리디렉션합니다 데스크톱 로그인 페이지를 개선 해야 합니다. 예를 들어, 다음 코드를 추가 하면 **데스크톱** 로그인 페이지 코드 숨김: 

    [!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample3.cs)]
- 사용자가 성공적으로 로그인 한 후 폼 인증은 기본적으로 리디렉션할 데스크톱 홈 페이지 (개념이 있어 *하나의* 기본 페이지). 성공적인 로그인 후 mobile 홈 페이지로 리디렉션합니다 모바일 로그인 페이지를 개선 해야 합니다. 예를 들어, 다음 코드를 추가 하면 **모바일** 로그인 페이지 코드 숨김: 

    [!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample4.cs)]
  
  이 코드 페이지에 기본 프로젝트 템플릿에서 같이 LoginUser, 이라는 로그인 서버 컨트롤을 가정 합니다.

### <a name="working-with-output-caching"></a>출력 캐싱을 사용합니다.

출력 캐시를 사용 하는 경우에 다음 캐시 된 데스크톱 출력을 수신 하는 모바일 사용자가 데스크톱 사용자 (해당 출력을 캐시할 생김) 특정 URL을 방문 하는 것이 불가능 기본적으로 준수 되 주의 하십시오. 이 경고 든 방금 장치 유형별로 마스터 페이지에 다양 한 장치 유형 마다 별도 완전히 Web Forms 구현에 적용 합니다.

문제를 방지 하려면 방문자 모바일 장치를 사용 하는지 여부에 따라 캐시 엔트리를 변경 하는 ASP.NET을 지시할 수 있습니다. 다음과 같이 페이지에 OutputCache 선언으로 VaryByCustom 매개 변수를 추가 합니다.

[!code-aspx[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample5.aspx)]

다음으로 정의 *isMobileDevice* 사용자 지정 캐시로 Global.asax.cs 파일에 다음 메서드를 추가 하 여 매개 변수 재정의:

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample6.cs)]

이렇게 하면 페이지로 모바일 방문자가 이전에 데스크톱 방문자에서 캐시를 넣을 출력을 수신 하지 않습니다.

### <a name="a-working-example"></a>작업 예제

이러한 기술이 작동을 확인 하려면 다운로드 [이 백서에서는 코드 샘플](https://docs.microsoft.com/aspnet/mobile/overview)합니다. Web Forms 샘플 응용 프로그램 Mobile 이라는 하위 폴더에 모바일 전용 페이지 집합에 모바일 사용자를 자동으로 리디렉션합니다. 태그와 해당 페이지의 스타일은 다음 스크린샷에서 알 수 있듯이 모바일 브라우저에 더 잘 최적화:

![](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/_static/image2.png)

모바일 브라우저에 대 한 사용자 태그와 CSS를 최적화 하는 방법에 대 한 더 많은 팁이이 문서의 뒷부분에 "모바일 브라우저에 대 한 모바일 페이지 스타일 지정" 섹션을 참조 하세요.

## <a name="how-aspnet-mvc-applications-can-present-mobile-specific-pages"></a>ASP.NET MVC 응용 프로그램에서 모바일 전용 페이지를 제공할 수는 방법

응용 프로그램 논리 (컨트롤러) 보기의 프레젠테이션 논리에서 분리 하는 모델-뷰-컨트롤러 패턴, 이후 모바일 지원 서버 쪽 코드에서 처리 하는 다음 방법 중 하나에서 선택할 수 있습니다.

1. ***데스크톱 및 모바일 브라우저에 대 한 동일한 컨트롤러 및 뷰를 사용 하 하지만 장치 형식 *에 따라 다른 Razor 레이아웃을 사용 하 여 뷰를 렌더링 합니다.** 이 그러면 모든 장치에서 동일한 데이터를 표시 하는 다양 한 CSS 스타일 시트를 제공 하거나 모바일에 대 한 몇 가지 최상위 HTML 요소를 변경 하려는 경우에 가장 적합 합니다.
2. ***데스크톱 및 모바일 브라우저에 대 한 동일한 컨트롤러를 사용 하지만 장치 유형에 따라 다른 뷰를 렌더링할***합니다. 거의 동일한 데이터를 표시 하 고 최종 사용자에 대해 동일한 워크플로 제공 하는 경우이 옵션은 가장 잘 작동 하지만 사용 중인 장치에 맞게 매우 다른 HTML 태그를 렌더링 합니다.
3. ***데스크톱 및 모바일 브라우저의 경우 각각에 대 한 독립적인 컨트롤러와 뷰를 구현 하는 별도 영역 만들기 * 합니다.** 이 옵션 하 매우 다른 화면을 표시, 다양 한 정보를 포함 하 고 각자의 장치 유형에 대 한 액세스에 최적화 된 다양 한 워크플로 통해 사용자를 선행 하는 경우에 가장 적합 합니다. 코드의 몇 가지 반복을 의미할 수 있지만 기본 계층 또는 서비스에 일반적인 논리를 제외 하 여 하를 최소화할 수 있습니다.

수행 하려는 경우는 **첫 번째** 옵션 및 Razor 레이아웃만 다를 장치 유형 마다 매우 쉽습니다. 수정 프로그램 \_ViewStart.cshtml 다음과 같이 파일:

[!code-cshtml[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample7.cshtml)]

이제 라는 모바일 전용 레이아웃을 만들 수 있습니다 \_CSS 및 LayoutMobile.cshtml 페이지 구조를 사용 하 여 모바일 장치에 대 한 액세스에 최적화 된 규칙입니다.

수행 하려는 경우는 **두 번째** 방문자의 장치 유형에 따라 완전히 다른 뷰를 렌더링 옵션을 참조 하십시오 [Scott Hanselman의 블로그 게시물](http://www.hanselman.com/blog/ABetterASPNETMVCMobileDeviceCapabilitiesViewEngine.aspx)합니다.

이 문서의 나머지 부분에 중점을 두고 합니다 **세 번째** 옵션-별도 컨트롤러를 만들기 *및* 모바일 방문자에 대 한 기능의 하위 집합으로 제공 됩니다 정확 하 게 제어할 수 있도록 모바일 장치에 대 한 보기입니다.

### <a name="setting-up-a-mobile-area-within-your-aspnet-mvc-application"></a>ASP.NET MVC 응용 프로그램 내에서 모바일 영역 설정

일반적인 방법으로 기존 ASP.NET MVC 응용 프로그램에 사용 되는 "Mobile" 불리는 영역을 추가할 수 있습니다: 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 한 다음 추가 회사 영역을 선택 합니다. 컨트롤러와 뷰 ASP.NET MVC 응용 프로그램 내의 다른 영역에 대 한 방법으로 추가할 수 있습니다. 예를 들어, 영역을 추가 하면 모바일를 모바일 방문자에 대 한 홈페이지가 프록시로 HomeController 라는 새 컨트롤러를.

### <a name="ensuring-the-url-mobile-reaches-the-mobile-homepage"></a>모바일 홈 페이지에 도달 하면 URL /Mobile 보장

HomeController 모바일 지역 내에서 인덱스 작업에 연결할 URL /Mobile 원한다 면 라우팅 구성에 두 약간 변경 해야 합니다. 먼저 업데이트 MobileAreaRegistration 클래스 HomeController 모바일 지역의 기본 컨트롤러 되도록 다음 코드 에서처럼:

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample8.cs)]

즉, 모바일 홈페이지 이제 배치 될/Mobile/Home, 보다는 /Mobile, 이므로 "홈" 이제는 모바일 페이지에 대 한 암시적으로 기본 컨트롤러 이름입니다.

다음으로 두 번째 HomeController에 응용 프로그램 (즉, 모바일 하나, 기존 데스크톱 것 외에도)를 추가 하면 됩니다 해제 일반 데스크톱 홈페이지 note 합니다. 오류와 함께 실패 "*'홈' 라는 컨트롤러와 일치 하는 여러 유형을 찾았습니다*"입니다. 이 해결 하려면 최상위 라우팅 구성 (Global.asax.cs)에 모호성이 경우 데스크톱 프로그램 HomeController가 우선 순위를 수행 해야 되도록 업데이트:

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample9.cs)]

오류는 먼, 및 URL http:// 되돌려집니다 이제<em>yoursite</em>데스크톱 홈 페이지 및 http://<em>yoursite</em>/mobile/ 에 도달 하면 모바일 홈 페이지에 도달 합니다.

### <a name="redirecting-mobile-visitors-to-your-mobile-area"></a>모바일 방문자를 모바일 리디렉션

여러 다양 한 확장성 지점을의 경우 ASP.NET MVC 되므로 리디렉션 논리를 삽입 하는 여러 가지 방법 특성을 만들려면 필터를 [RedirectMobileDevicesToMobileArea] 다음 조건이 충족 될 경우 리디렉션을 수행 하는 하나의 간단한 옵션은:

1. 첫 번째 요청은 사용자의 세션에서 (즉, Session.IsNewSession true 임)
2. 모바일 브라우저에서 요청 하는 (즉, Request.Browser.IsMobileDevice true 임)
3. 사용자는 이미 모바일 영역에 리소스를 요청 하지 (즉, 합니다 *경로* URL의 일부 /Mobile 시작 되지 않는)

이 백서에서는 포함 된 다운로드 가능한 샘플에는이 논리의 구현을 포함 합니다. 권한 부여 필터를 사용 하는 출력 캐싱 (그렇지 않으면 경우 데스크톱 방문자 첫 번째 액세스 특정 URL 데스크톱 출력 수 캐시 하 고 다음에 제공 하는 경우에 올바르게 작동할 수 있는 AuthorizeAttribute에서 파생으로 구현 후속 모바일 방문자)입니다.

필터를 그대로 선택할 수 있습니다 특정 컨트롤러 및 작업에 적용할 예

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample10.cs)]

… MVC 3으로 모든 컨트롤러 및 작업에 적용할 수 있습니다 또는 *전역 필터* Global.asax.cs 파일에서:

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample11.cs)]

다운로드 가능한 샘플에는 모바일 분야 내에서 특정 위치로 리디렉션하는이 특성의 서브 클래스를 만드는 방법을 보여 줍니다. 즉, 예를 들어, 할 수 있습니다.

- 전역 필터를 표시 된 것 처럼 위의 기본적으로 모바일 홈페이지 모바일 방문자를 전송 하는 등록 합니다.
- 모바일 방문자가 요청 했습니다. 이러한 모든 제품 페이지의 모바일 버전을 사용 하는 "제품 보기" 작업에 특수 [RedirectMobileDevicesToMobileProductPage] 필터를 적용할 수도 있습니다.
- 모바일 방문자 해당 모바일 페이지로 리디렉션 특정 작업에 적용할 필터의 다른 특별 한 서브 클래스

### <a name="configuring-forms-authentication-to-respect-your-mobile-pages"></a>모바일 페이지를 준수 하도록 폼 인증 구성

폼 인증을 사용 하는 경우는 사용자를 로그인 해야 하는 경우 자동으로 리디렉션됩니다 사용자 단일 특정 "로그온" URL을 기본적으로 기록해 두어야 **/계정/로그온**합니다. 즉, 모바일 사용자에 게 데스크톱 로그온"작업 리디렉션될 수 있습니다.

이 문제를 방지 하려면 모바일 "로그온" 작업으로 모바일 사용자에 게 다시 리디렉션합니다 있도록 논리 데스크톱 "로그온" 작업을 추가 합니다. 기본 ASP.NET MVC 응용 프로그램 템플릿을 사용 하는 경우 아래와 같이 AccountController의 로그온 작업 업데이트:

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample12.cs)]

… 및 다음 해당 모바일 지역의 AccountController 라는 컨트롤러에서 적절 한 모바일 전용 "로그온" 작업을 구현 합니다.

### <a name="working-with-output-caching"></a>출력 캐싱을 사용합니다.

[OutputCache] 필터를 사용 하는 경우에 장치 유형별로 캐시 엔트리의 강제 적용 해야 합니다. 예를 들어 쓰기:

[!code-javascript[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample13.js)]

Global.asax.cs 파일에 다음 메서드를 추가 하십시오.

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample14.cs)]

이렇게 하면 페이지로 모바일 방문자가 이전에 데스크톱 방문자에서 캐시를 넣을 출력을 수신 하지 않습니다.

### <a name="a-working-example"></a>작업 예제

이러한 기술이 작동을 확인 하려면 다운로드 [이 백서에서는이 코드 샘플 연결](https://docs.microsoft.com/aspnet/mobile/overview)합니다. 샘플은 ASP.NET MVC 3 (릴리스 후보) 응용 프로그램 위에 설명 된 메서드를 사용 하 여 모바일 장치를 지원 하도록 향상을 포함 합니다.

## <a name="further-guidance-and-suggestions"></a>추가 지침과 제안

다음 논의 Web Forms 및이 문서에 설명 된 기술을 사용 하는 MVC 개발자 모두에 적용 됩니다.

### <a name="enhancing-your-redirection-logic-using-51degreesmobi-foundation"></a>51Degrees.mobi Foundation를 사용 하 여 리디렉션 논리 향상

이 문서에 표시 된 리디렉션 논리는 완벽 하 게 응용 프로그램에 대 한 충분 한 수 있지만 세션을 사용 하지 않도록 설정 하는 경우 작동 하지 않습니다 또는 지정된 된 요청 여부를 인식 하지 못합니다 (이러한 세션 수 없습니다) 쿠키를 거부할 모바일 브라우저는 해당 방문자의 첫 번째입니다.

이미 오픈 소스 51Degrees.mobi Foundation ASP의 정확도 개선 하는 방법을 배웠습니다. NET의 브라우저 탐지 합니다. 또한 기본 제공 모바일 방문자 Web.config에 구성 된 특정 위치로 리디렉션할 수가 있습니다. ASP.NET 세션에 따라 않고 작업할 수 있습니다 (및 따라서 쿠키) 방문자의 HTTP 헤더 및 IP 주소 해시 임시 로그에 저장 하면이 알 수 있도록 각 요청에 지정 된 vistor에서 첫 번째 인지 여부입니다.

Web.config 파일의 fiftyOne 섹션에 추가 된 다음 요소를 페이지에 검색 된 모바일 장치에서 첫 번째 요청을 리디렉션할 ~ / Mobile/Default.aspx 합니다. 모바일 폴더 아래에 있는 페이지에 모든 요청이 *되지* 장치 종류에 관계 없이 리디렉션됩니다. 모바일 장치가 비활성 상태인 동안 20 분 또는 장치를 더 무시 됩니다 하 고 후속 요청이 의도치 않은 리디렉션의 새로 목적으로 처리 됩니다.

[!code-xml[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample15.xml)]

자세한 내용은 참조 하세요. [51degrees.mobi Foundation 설명서](https://github.com/51Degrees/dotNET-Device-Detection)합니다.

> [!NOTE]
> 있습니다 *수* 수 있지만 ASP.NET MVC 응용 프로그램에서 사용 하 여 51Degrees.mobi Foundation의 리디렉션 기능 라우팅 매개 변수가 아니라 또는 MVC 필터를 배치 하 여 일반 Url 기준으로 리디렉션 구성을 정의 해야 합니다. 동작 합니다. 왜냐하면 (작성 당시) 필터 또는 라우팅 51Degrees.mobi Foundation 인식 하지 못합니다.


### <a name="disabling-transcoders-and-proxy-servers"></a>트랜스코더 및 프록시 서버를 사용 하지 않도록 설정

모바일 네트워크 운영자 두 가지 목표를 광범위 한 모바일 인터넷 접근 방식이 있습니다.

1. 최대한 훨씬 관련 콘텐츠로 제공
2. 네트워크 대역폭을 제한 라디오를 공유할 수 있는 고객의 수를 최대화 합니다.

많은 연산자를 사용 하는 대형 데스크톱의 화면 및 고정 줄 빠른 광대역 연결에 대 한 대부분의 웹 페이지 디자인에 있으므로 *트랜스코더* 하거나 *프록시 서버* 웹 콘텐츠를 동적으로 변경 하는 합니다. 에 HTML 태그 또는 CSS (특히 휴대폰용"기능" 복잡 한 레이아웃을 처리 하는 처리 기능이 없는), 보다 작은 화면에 맞게 수정 될 수 있습니다 하 고 (품질을 크게 덜어) 이미지를 다시 압축 옵션 페이지 배달 속도 향상 시킬 수 있습니다.

하지만 모바일에 최적화 된 버전의 사이트 생성에 대 한 노력을 수행한 경우 원하지 않을 수 있습니다 네트워크 운영자 방해가 모든 추가 합니다. 페이지에 다음 줄을 추가할 수 있습니다\_모든 ASP.NET Web Form의 Load 이벤트:

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample16.cs)]

또는 ASP.NET MVC 컨트롤러에 대 한 추가 수 해당 컨트롤러에 대 한 모든 작업에 적용 되도록 다음 메서드 재정의:

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample17.cs)]

결과 HTTP 메시지에 W3C 호환 트랜스코더 알리고 프록시 내용을 변경 하지 않습니다. 물론 모바일 네트워크 운영자는이 메시지는 유지 하지 않을 수도가 있습니다.

### <a name="styling-mobile-pages-for-mobile-browsers"></a>모바일 브라우저에 대 한 모바일 페이지 스타일 지정

상세하게 설명 하려면이 문서의 범위를 벗어납니다 어떤 종류의 HTML 태그 작업 올바르게 또는 어떤 웹 디자인 기술을 특정 장치의 유용성 최대화 합니다. 충분히 단순형 레이아웃을 찾을 수 최적화 mobile 크기의 화면에 대 한 신뢰할 수 없는 사용 하지 않고 HTML 또는 CSS 트릭 위치 합니다. 알아낸, 중요 한 한 가지 방법은 것 인데, 합니다 *뷰포트 meta 태그*합니다.

특정 모바일 브라우저, 데스크톱 모니터에 대 한 의미는 노력 표시 웹 페이지의 렌더링 "뷰포트" 라고도 가상 캔버스를 페이지 (예를 들어 가상 뷰포트는 iPhone에서 980 픽셀 및 850 픽셀 Opera Mobile에서 기본적으로) 한 다음 화면의 실제 픽셀에 맞게 결과 축소 합니다. 사용자 확대/축소 하는 뷰포트 주변 여 합니다. 이 경우이 의도 한 해당 레이아웃에서 페이지를 표시 하는 브라우저를 통해 하는데 이기도 하는 사용자에 대 한 편리한 되지 않는 확대/축소 및 이동 한다는 단점이 있습니다. 모바일을 위해 디자인할 경우 것이 좋습니다 디자인 좁은 화면에 대 한 확대/축소 없거나 가로 스크롤이 필요 않도록 합니다.

뷰포트 너비 수 해야 모바일 브라우저에 지시 하는 방법은 비표준를 통해 것 *뷰포트* 메타 태그입니다. 예를 들어, 다음 페이지의 HEAD 섹션에 추가 하는 경우

[!code-html[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample18.html)]

… 다음 smartphone 브라우저를 지 원하는 480 픽셀 전체 가상 캔버스에서 페이지 배치 됩니다. 즉, HTML 요소를 백분율 용어로 너비가 정의 하는 경우 백분율 기본 뷰포트 너비가 480 픽셀 너비를 기준으로 해석 됩니다. 결과적으로, 사용자가 확대/축소 및 가로 – 상당히 개선의 모바일 탐색 환경으로 이동 해야 할 가능성이 적습니다.

장치의 물리적 픽셀에 맞게 뷰포트 너비를 하려는 경우 다음을 지정할 수 있습니다.

[!code-html[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample19.html)]

제대로 작동 하려면이 위해 하지 명시적으로 강제로 해야 너비를 초과 하는 요소 (예를 사용 하 여를 *너비* 특성 또는 CSS 속성)에 관계 없이 더 큰 뷰포트를 사용 하는 브라우저는 강제로 고, 그렇지 합니다. 참고: [비표준 뷰포트 태그에 대 한 자세한 내용은](https://developer.apple.com/library/safari/#documentation/AppleApplications/Reference/SafariHTMLRef/Articles/MetaTags.html)합니다.

최신 스마트폰 지원 *이중 방향*: 세로 또는 가로 모드에서 보관할 수 있습니다. 따라서 것 픽셀에서 화면 너비에 대 한 가정을 하지 않아야 합니다. 사용자 수 방향을 다시 지정 하는 장치 페이지에는 때문에 화면 너비를 고정 된 가정도 하지 마십시오.

Content 알리고 페이지 헤더에 다음 메타 태그 모바일에 최적화 된 및 따라서 변환 되지 않아야에 이전 Windows Mobile 및 Blackberry 장치 허용할 수 있습니다.

[!code-html[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample20.html)]

## <a name="additional-resources"></a>추가 리소스

모바일 장치 에뮬레이터 및 시뮬레이터 모바일 ASP.NET 웹 응용 프로그램을 테스트 하 여 목록, 페이지를 참조 [테스트를 위한 인기 있는 모바일 장치를 시뮬레이션](../mobile/device-simulators.md)합니다.

## <a name="credits"></a>크레딧

- 기본 작성자: Steven Sanderson
- 검토자 추가 / 콘텐츠 작성자: James Rosewell, Mikael Söderström, Scott hanselman이 Scott Hunter
