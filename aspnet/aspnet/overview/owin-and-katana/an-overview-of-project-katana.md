---
uid: aspnet/overview/owin-and-katana/an-overview-of-project-katana
title: 프로젝트 Katana 개요 | Microsoft Docs
author: howarddierking
description: ASP.NET 프레임 워크는 10 년 넘게 오랫동안 및 수많은 웹 사이트 및 서비스의 개발 플랫폼이 사용 하도록 설정 합니다. 웹 응용 프로그램으로 하는 중...
ms.author: aspnetcontent
ms.date: 08/30/2013
ms.assetid: 0ee21741-c1bf-4025-a9b0-24580cae24bc
msc.legacyurl: /aspnet/overview/owin-and-katana/an-overview-of-project-katana
msc.type: authoredcontent
ms.openlocfilehash: a4c7d6cb5dc40ad68280a87acd89f60106a260a8
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37803096"
---
<a name="an-overview-of-project-katana"></a>프로젝트 Katana 개요
====================
[Howard Dierking](https://github.com/howarddierking)

> ASP.NET 프레임 워크는 10 년 넘게 오랫동안 및 수많은 웹 사이트 및 서비스의 개발 플랫폼이 사용 하도록 설정 합니다. 웹 응용 프로그램 개발 전략 진화 하는 대로 프레임 워크를 ASP.NET MVC 및 ASP.NET Web API와 같은 기술 사용 하 여 단계에서 진화 할 수 되었습니다. 클라우드 컴퓨팅의 세계로 다음 진화 단계를 사용 하는 웹 응용 프로그램 개발을 하는 대로 프로젝트 [Katana](https://channel9.msdn.com/Shows/Web+Camps+TV/The-Katana-Project-OWIN-for-ASPNET) ASP.NET 응용 프로그램을 유연 하 고 이식 가능 하며 사용할 수 있도록 구성 요소의 기본 집합을 제공 합니다. 경량 – 더 나은 성능을 제공 하 고 프로젝트, 다른 말로 [Katana](https://channel9.msdn.com/Shows/Web+Camps+TV/The-Katana-Project-OWIN-for-ASPNET) 클라우드 ASP.NET 응용 프로그램을 최적화 합니다.


## <a name="why-katana--why-now"></a>왜 Katana – 이제 이유?

 개발자 프레임 워크 또는 최종 사용자가 제품을 논의 하는 하나는 여부에 관계 없이, 것을 만들기 위한 기본 동기를 이해 해야 제품 – 및에 포함 제품에 대해 생성 된 사용자를 파악 합니다. ASP.NET 염두에서에 두 고객을 사용 하 여 원래 만들어졌습니다.   
  
**고객의 첫 번째 그룹에는 기존 ASP 개발자 들은 했습니다.** 동시에 ASP interweaving 태그 및 서버 쪽 스크립트에서 동적, 데이터 기반 웹 사이트 및 응용 프로그램을 만들기 위한 기본 기술 중 하나 였습니다. ASP 런타임 캐시, 등 추가에 대 한 액세스는 이러한 세션 및 응용 프로그램 상태 관리 서비스 제공 및 기본 HTTP 프로토콜 및 웹 서버 핵심 측면을 추상화 하는 개체의 집합을 사용 하 여 서버 쪽 스크립트를 제공 합니다. 강력, 클래식 ASP 응용 프로그램의 크기와 복잡성 증가할 때 관리 하는 문제를 되었습니다. 이 구조 스크립팅 중복 되는 코드와 태그의 인터리빙에서 발생 하는 코드를 사용 하 여 결합 된 환경에서 찾을 수 없어서 대부분 이었습니다. 해당 과제 중 일부를 해결 하는 동안 기본 ASP의 장점을 활용을 위해 ASP.NET 활용도 서버 쪽 프로그래밍 모델을 유지 하면서.NET Framework의 개체 지향 언어에서 제공 하는 코드 조직 에 클래식 ASP 개발자 토대로 했습니다.

**ASP.NET에 대 한 대상 고객의 두 번째 그룹에는 Windows 비즈니스 응용 프로그램 개발자가 되었습니다.** HTML 태그 및 자세한 HTML 태그를 생성 하는 코드를 작성 하는 데 익숙한 인 클래식 ASP 개발자에 달리 (예: 앞 VB6 개발자) WinForms 개발자 캔버스 및 다양 한 사용자를 포함 하는 디자인 타임 환경에 익숙한 것 인터페이스를 제어 합니다. 첫 번째 버전의 ASP.NET – 라고도 "Web Forms" 제공 된 사용자 인터페이스 구성 요소에 대 한 서버 쪽 이벤트 모델 및 인프라 기능 (예: ViewState) 집합이 함께 비슷한 디자인 타임 환경을 완전무결 한 개발자 환경을 만들려면 클라이언트와 서버 쪽 프로그래밍 합니다. Web Forms에서 WinForms 개발자에 게 친숙 한 상태 저장 이벤트 모델을 웹의 상태 비저장 특성을 효과적으로 hid 합니다.

### <a name="challenges-raised-by-the-historical-model"></a>기록 모델에서 발생 한 문제

**결과 완성도 높은, 풍부한 기능의 런타임 및 개발자 프로그래밍 모델을 했습니다.** 그러나 풍부한 기능을 강화 된 몇 가지 주목할 만한 문제를 제공 합니다. 먼저는 프레임 워크가 **모놀리식**를 논리적으로 서로 다른 단위의 동일한 System.Web.dll 어셈블리 (예를 들어, Web forms 프레임 워크를 사용 하 여 HTTP 핵심 개체)에 밀접 하 게 결합 되는 기능을 사용 하 여 합니다. ASP.NET 있음을 의미 하는 큰.NET Framework의 일부로 포함 된 둘째,는 **릴리스 간의 시간은 년 순서입니다.** 이 인해 모든 변경 내용을 빠르게 발전 하는 웹 개발에서 발생 하는 ASP.NET 어렵습니다. 특정 웹 호스팅 옵션에는 몇 가지 방법으로 자체 System.Web.dll를 결합 하는 마지막으로: 인터넷 정보 서비스 (IIS).

### <a name="evolutionary-steps-aspnet-mvc-and-aspnet-web-api"></a>진화 단계: ASP.NET MVC 및 ASP.NET Web API

및 웹 개발에서 발생 한 변경 많은! 많은 프레임 워크를 사용 하지 않고 구성 요소를 강조 하는 일련의 작은 웹 응용 프로그램을 개발한 되 고 점점 더 합니다. 적이 더 빠른 속도로 증가 하 고 있는 출시 빈도 뿐만 아니라 구성 요소 수 있었습니다. 웹과 속도 유지 프레임 워크를 작고 분리 된 더 크고 더 풍부한 기능의 대신 따라서 가져올 필요는 명백 합니다 **ASP.NET 팀의 제품군으로 ASP.NET을 사용 하도록 설정 하려면 몇 가지 진화 단계를 진행 합니다. 단일 프레임 워크 보다는 플러그형 웹 구성**합니다.

초기 변경이 Rails에 Ruby와 같은 웹 개발 프레임 워크 덕분 잘 알려진 모델-뷰-컨트롤러 (MVC) 디자인 패턴의 널리 사용 되 고 증가 했습니다. 이 스타일의 웹 응용 프로그램 빌드 개발자를 지정한 ASP.NET에 대 한 초기 selling 지점 중 하나는 태그 및 비즈니스 논리 분리를 보존 하면서 자신의 응용 프로그램의 태그를 통해 제어 합니다. 이 스타일의 웹 응용 프로그램 개발에 대 한 요청을 충족 하기 위해 Microsoft는 자체 위치로 기회 하 여 미래를 위한 더 나은 **대역 외에서 ASP.NET MVC 개발** (및.NET Framework의 제외). ASP.NET MVC는 독립적인 다운로드로 출시 되었습니다. 이 기능을 통해 엔지니어링 팀에 가능 했던 것 보다 훨씬 더 자주 업데이트를 제공 하는 유연성입니다.

웹 응용 프로그램 개발의 다른 변화 된 통신 하는 클라이언트 쪽 스크립트에서 생성 된 페이지의 동적 섹션을 사용 하 여 정적 초기 태그를 동적으로 서버에서 생성 된 웹 페이지에서 shift **백 엔드 Web Api를 사용 하 여을 통해 AJAX 요청**합니다. 이 아키텍처 shift ASP.NET Web API 프레임 워크를 개발 및 웹 Api의 날 려 보내는 하는 데 도움이 되었습니다. ASP.NET MVC의 경우와 같이 ASP.NET Web API의 릴리스는 ASP.NET 모듈식 프레임 워크로 더 발전 하는 또 다른 기회를 제공 합니다. 엔지니어링 팀 기회를 활용 하 고 **System.Web.dll 있는 core 프레임 워크 형식 중 하나에 종속성이 없는 이었습니다 되도록 ASP.NET Web API를 작성**. 이 두 가지를 사용 하도록 설정: 하는 것 먼저 ASP.NET Web API를 완전히 독립적인 방식으로 개선할 수 (및 NuGet을 통해 배달 되기 때문에 신속 하 게 반복을 계속 될 수 있습니다). 둘째, System.Web.dll 하는 외부 종속성 및 IIS에 종속성이 없는 따라서 있었습니다, ASP.NET Web API (예를 들어는 콘솔 응용 프로그램, Windows 서비스 등)는 사용자 지정 호스트에서 실행 하는 기능 포함

### <a name="the-future-a-nimble-framework"></a>미래: 민첩 프레임 워크

다른 프레임 워크 구성 요소를 분리 하 고 다음 NuGet에서 해제 하 여 프레임 워크 수 이제 **요금과 보다 신속 하 게 반복**합니다. 성능과 유연성 Web API의 자체 호스팅 기능을 입증 하려고 했던 개발자에 게 그다지 또한을 **소규모의 간단한 호스트** 해당 서비스에 대 한 합니다. 그다지 매력적으로 증명, 실제로 다른 프레임 워크는이 기능에도 또 다른 목표 및 각 프레임 워크 자체 기본 주소에서 자체 호스트 프로세스에서 실행 및 관리 하는 데 필요한 (시작, 중지 등)에 새로운 과제를 표시이 독립적으로 유지 합니다. 최신 웹 응용 프로그램에는 일반적으로 정적 파일 처리, 동적 페이지를 생성, Web API 및 보다 최근에 실시간으로 시간/푸시 알림을 지원합니다. 이러한 서비스의 각 실행 있고 독립적으로 관리할 필요 없었던 현실적인 합니다.

개발자는 다양 한 다른 구성 요소 및 프레임 워크에서에서 응용 프로그램을 작성 및 지 원하는 호스트에 해당 응용 프로그램을 실행 하는 단일 호스팅 추상화를가 필요 했습니다.

## <a name="the-open-web-interface-for-net-owin"></a>Open Web Interface for.NET (OWIN)

 얻을 수 있는 장점을에서 영감을 받았습니다 [랙](http://rack.github.io/) Ruby 커뮤니티의.NET 커뮤니티의 몇몇 구성원이 웹 서버와 프레임 워크 구성 요소 간의 추상화를 만듭니다. OWIN 추상화에 대 한 두 가지 디자인 목표 간단한 되었는지 및 다른 프레임 워크 형식에 가능한 한 최소한의 종속성 걸린다는 것 이었습니다. 이러한 두 가지 목표 수 있도록 합니다.

- 새 구성 요소를 보다 쉽게 개발 및 사용 될 수 없습니다.
- 응용 프로그램 호스트와 잠재적으로 전체 플랫폼/운영 체제 간에 더 쉽게 이식할 수 없습니다.

결과 추상화 두 가지 핵심 요소로 구성 됩니다. 첫 번째는 환경 사전을 합니다. 이 데이터 구조는 모든 HTTP 요청 및 응답 뿐만 아니라 해당 하는 서버 상태를 처리 하는 데 필요한 상태를 저장 하는 일을 담당 합니다. 환경 사전은 다음과 같이 정의 됩니다.

[!code-console[Main](an-overview-of-project-katana/samples/sample1.cmd)]

OWIN 호환 웹 서버를 본문 스트림 및 HTTP 요청 및 응답 헤더 컬렉션 같은 데이터를 사용 하 여 환경 사전을 채우는 담당 합니다. 응용 프로그램 또는 프레임 워크 구성 요소 채우기 또는 추가 값을 사용 하 여 사전 업데이트 및 응답 본문 스트림에 쓸를 해야 됩니다.

환경 사전에 대 한 유형을 지정 하는 것 외에도 OWIN 사양 core 사전 키 값 쌍의 목록을 정의 합니다. 예를 들어, 다음 표에서 HTTP 요청에 필요한 사전 키를 보여 줍니다.

| 키 이름 | 값 설명 |
| --- | --- |
| `"owin.RequestBody"` | 요청 본문에 있는 경우는 Stream입니다. 요청 본문이 있으면 Stream.Null 자리 표시자로 사용할 수 있습니다. 참조 [요청 본문](http://owin.org/html/owin.html#34-request-body-100-continue-and-completed-semantics)합니다. |
| `"owin.RequestHeaders"` | `IDictionary<string, string[]>` 요청 헤더입니다. 참조 [헤더](http://owin.org/html/owin.html#3-3-headers)합니다. |
| `"owin.RequestMethod"` | A `string` 요청의 HTTP 요청 메서드를 포함 (예를 들어 `"GET"`, `"POST"`). |
| `"owin.RequestPath"` | `string` 요청 경로 포함 합니다. 응용 프로그램 대리자;의 "루트"에 상대적인 경로 여야 합니다. 참조 [경로](http://owin.org/html/owin.html#5-3-paths)합니다. |
| `"owin.RequestPathBase"` | A `string` 참조 응용 프로그램 대리자;의 "루트"에 해당 하는 요청 경로의 일부를 포함 하 [경로](http://owin.org/html/owin.html#5-3-paths)합니다. |
| `"owin.RequestProtocol"` | A `string` 프로토콜 이름 및 버전 (예: `"HTTP/1.0"` 또는 `"HTTP/1.1"`). |
| `"owin.RequestQueryString"` | `string` 앞에 오는 하지 않고 HTTP 요청 URI 쿼리 문자열 구성 요소가 포함 된 "?" (예를 들어 `"foo=bar&baz=quux"`). 값은 빈 문자열일 수 있습니다. |
| `"owin.RequestScheme"` | `string` 요청에 사용 된 URI 구성표를 포함 (예를 들어 `"http"`를 `"https"`); 참조 [URI 체계](http://owin.org/html/owin.html#5-1-uri-scheme)합니다. |

OWIN의 두 번째 핵심 요소는 응용 프로그램 대리자입니다. OWIN 응용 프로그램의 모든 구성 요소 간의 기본 인터페이스로 사용 되는 함수 시그니처입니다. 응용 프로그램 대리자에 대 한 정의 다음과 같습니다.

`Func<IDictionary<string, object>, Task>;`

다음 응용 프로그램 대리자는 함수 환경 사전을 입력으로 허용 하 고는 작업을 반환 하는 여기서 Func 대리자 형식의 구현 하기만 하면 됩니다. 이 디자인은 개발자를 위한 여러 가지를 의미 합니다.

- OWIN 구성 요소를 작성 하는 데 필요한 유형 종속성의 매우 작은 여러 가지가 있습니다. 이 개발자에 게 OWIN의 접근성을 향상 되었습니다.
- 비동기 디자인 하 여 컴퓨팅 리소스에 더 많은 I/O 집약적인 작업에 특히 처리를 사용 하 여 효율적으로 추상화를 수 있습니다.
- 응용 프로그램 대리자 실행의 원자 단위 이며 OWIN 구성 요소를 쉽게 연결할 수 있으므로 환경 사전에 대리자에 매개 변수로 작업 하기 때문에 복잡 한 HTTP 처리 파이프라인을 만들어야 합니다.

OWIN은 사양 구현 측면에서 볼 때 ([http://owin.org/html/owin.html](http://owin.org/html/owin.html)). 목표 다음 웹 프레임 워크를 하지만 웹 프레임 워크 및 웹 서버 상호 작용 하는 방법에 대 한 사양 대신 해서는 안 됩니다.

조사 했습니다 하는 경우 [OWIN](http://owin.org/) 또는 [Katana](https://github.com/aspnet/AspNetKatana/wiki), 또한 했을 수는 [Owin NuGet 패키지](http://nuget.org/packages/Owin) 및 Owin.dll 합니다. 이 라이브러리는 단일 인터페이스를 포함 [IAppBuilder](https://github.com/owin/owin/blob/master/src/Owin/IAppBuilder.cs)를 공식화 하 고 시작 시퀀스에 설명 된 체계화 [섹션 4](http://owin.org/html/owin.html#4-application-startup) OWIN 사양입니다. OWIN 서버를 구축 하기 위해 필요는 없지만 합니다 [IAppBuilder](https://github.com/owin/owin/blob/master/src/Owin/IAppBuilder.cs) 인터페이스는 구체적 참조 지점으로 제공 하며 Katana 프로젝트 구성 요소에서 사용 됩니다.

## <a name="project-katana"></a>프로젝트 Katana

반면 모두를 [OWIN](http://owin.org/html/owin.html) 사양 및 *Owin.dll* 소유 하는 커뮤니티 및 오픈 소스 작업을 실행 하는 커뮤니티를 [Katana](https://github.com/aspnet/AspNetKatana/wiki) 프로젝트에 OWIN의 집합을 나타내는 여전히 오픈 소스, 하는 동안 빌드하고 Microsoft에서 출시 되는 구성 요소입니다. 이러한 구성 요소 호스트 및 서버와 같은 인프라 구성 요소 뿐만 아니라 인증 구성 요소 및 프레임 워크에 대 한 바인딩을 같은 기능적 구성 요소 포함 등 [SignalR](../../../signalr/index.md) 고 [ASP.NET 웹 API](../../../web-api/overview/getting-started-with-aspnet-web-api/index.md)합니다. 프로젝트에 다음과 같은 세 가지 상위 수준의 목표: 

- **이식 가능한** – 구성 요소를 쉽게 대체할 새 구성 요소에 대 한 사용 가능 해지면 수 있어야 합니다. 이 모든 유형의 서버 및 호스트 하기 위해 프레임 워크에서 구성 요소를 포함합니다. 이 목표의 Microsoft 프레임 워크가 타사 서버와 호스트에서 실행할 수 있지만 타사 프레임 워크 Microsoft 서버에는 실행 원활 하 게 수입니다.
- **모듈식/유연한**– 기본적으로 켜져 있는 기능이 포함 되어 있는 많은 프레임 워크와는 달리 작고 집중 된 구성 요소를 결정 하는 데 응용 프로그램 개발자에 게 컨트롤을 통해 제공 Katana 프로젝트 구성 요소 이어야 합니다 응용 프로그램에서 사용 합니다.
- **경량/성능/확장성** – 프레임 워크의 기존 개념을 작은 집합으로 분할 하 여 구성 요소는 명시적으로 추가 응용 프로그램 개발자가 더 적은 계산 결과 Katana 응용 프로그램을 사용할 수 있음 집중 리소스 및 결과적으로, 다른 유형의 서버 및 프레임 워크를 사용 하 여 보다 더 많은 부하를 처리 합니다. 응용 프로그램의 요구 사항을 기본 인프라에서 더 많은 기능을 요청 하는 대로 OWIN 파이프라인에 추가할 수는 있지만 응용 프로그램 개발자는 명시적 의사 결정 합니다. 또한 하위 수준 구성 요소 대체는 사용 가능 해지면 새로운 고성능 서버 원활 하 게 도입할 수 있습니다 이러한 응용 프로그램을 중단 하지 않고 OWIN 응용 프로그램의 성능을 개선 하기 위해 의미 합니다.

## <a name="getting-started-with-katana-components"></a>Katana 구성 요소를 사용 하 여 시작

처음으로 도입의 측면 중 하나는 [Node.js](http://nodejs.org/) 즉시 사람들의 관심을 그린는 프레임 워크가 있는 작성 및 웹 서버를 실행할 수 있습니다 하나는 단순성입니다. Katana 목표 light의 포함 된 경우 [Node.js](http://nodejs.org/), Katana 다양 한 장점을 제공 하는 한다는 것으로 요약할 수 있습니다 하나 [Node.js](http://nodejs.org/) (및 그와 같은 프레임 워크) 버릴 수 개발자 시작 하지 않고 모든 ASP.NET 웹 응용 프로그램을 개발 하는 방법에 대 한 알고 있습니다. 참이 문에 대 한 Katana 프로젝트 시작 동일 하 게 간단해 야 기본적에서 [Node.js](http://nodejs.org/)합니다.

## <a name="creating-hello-world"></a>"Hello World!" 만들기

JavaScript 및.NET 개발 간의 주요 차이점 중 하나 (유무) 컴파일러의 경우 따라서 간단한 Katana 서버에 대 한 시작 지점에는 Visual Studio 프로젝트입니다. 그러나 프로젝트 형식의 가장 최소를 사용 하 여 시작할 수 있습니다: 빈 ASP.NET 웹 응용 프로그램입니다.

[![](an-overview-of-project-katana/_static/image1.png)](http://nuget.org/packages/Microsoft.Owin.Host.SystemWeb)

다음으로 설치 합니다 [Microsoft.Owin.Host.SystemWeb](http://nuget.org/packages/Microsoft.Owin.Host.SystemWeb) 프로젝트에 NuGet 패키지. 이 패키지는 ASP.NET 요청 파이프라인에서 실행 되는 OWIN 서버를 제공 합니다. 찾을 수 있습니다 합니다 [NuGet 갤러리](http://nuget.org/packages/Microsoft.Owin.Host.SystemWeb) Visual Studio 패키지 관리자 대화 상자 또는 패키지 관리자 콘솔을 사용 하 여 다음 명령을 사용 하 여 설치할 수 있습니다.

[!code-console[Main](an-overview-of-project-katana/samples/sample2.cmd)]

설치는 `Microsoft.Owin.Host.SystemWeb` 패키지 종속성으로 몇 가지 추가 패키지를 설치 합니다. 해당 종속성 중 하나는 `Microsoft.Owin`, 몇 가지 도우미 형식 및 OWIN 응용 프로그램을 개발 하기 위한 메서드를 제공 하는 라이브러리입니다. "Hello world" 서버를 신속 하 게 쓸 이러한 형식을 사용할 수 있습니다.

[!code-csharp[Main](an-overview-of-project-katana/samples/sample3.cs)]

Visual Studio를 사용 하 여이 간단한 웹 서버를 실행할 수 있습니다 **F5** 명령 및 디버깅에 대 한 전체 지원을 포함 합니다.

## <a name="switching-hosts"></a>호스트를 전환합니다.

기본적으로 이전 "hello world" 예제는 IIS의 컨텍스트에서 System.Web를 사용 하는 ASP.NET 요청 파이프라인에서 실행 됩니다. 이 수 자체로 엄청난 하므로 값을 추가 유연성 및 관리 기능을 사용 하 여 OWIN 파이프라인을 작성 하 고 IIS의 전체 완성도 활용할 수 있도록 합니다. 그러나 여기서 IIS에서 제공 되는 혜택은 필요 하지 않습니다 하 고 더 작은가 벼 워 졌습니다 호스트에 대 한 요구는 경우가 있을 수 있습니다. 필요한 것, 그런 다음 IIS 및 System.Web와 같이 외부에서 간단한 웹 서버를 실행 하 시겠습니까?

이식성 목표를 설명 하기 위해 명령줄 호스트 웹 서버 호스트에서 이동 하려면 프로젝트의 출력 폴더에 새 서버와 호스트 종속성을 추가 하기만 하면 및 다음 호스트를 시작 합니다. 이 예제에서는 웹 서버 라는 Katana 호스트에서 호스트할 `OwinHost.exe` Katana HttpListener 기반 서버를 사용 합니다. 마찬가지로 다른 Katana 구성 요소로, 이러한 획득 다음 명령을 사용 하 여 NuGet에서:

[!code-console[Main](an-overview-of-project-katana/samples/sample4.cmd)]

명령줄에서 수 후 프로젝트 루트 폴더로 이동 하 고 실행 하는 `OwinHost.exe` (함께 설치 된 각 NuGet 패키지의 tools 폴더에서). 기본적으로 `OwinHost.exe` HttpListener 기반 서버에 대 한 확인 하도록 구성 된 이므로 추가 구성이 필요 하지 않습니다. 웹 브라우저에서 탐색 `http://localhost:5000/` 콘솔을 통해 이제 실행 중인 응용 프로그램을 보여 줍니다.

![](an-overview-of-project-katana/_static/image2.png)

## <a name="katana-architecture"></a>Katana 아키텍처

 Katana 구성 요소 아키텍처 아래와 같이 4 개의 논리적 계층으로 응용 프로그램을 나누는: *호스트, 서버, 미들웨어* 하 고 *응용 프로그램*합니다. 구성 요소 아키텍처는 이러한 계층의 구현을 쉽게 대체할 수, 대부분의 경우 응용 프로그램의 다시 컴파일하지 않고도 하는 방식으로 구분 됩니다.   

![](an-overview-of-project-katana/_static/image3.png)

## <a name="host"></a>호스트

 호스트는 담당 합니다.

- 기본 프로세스를 관리 합니다.
- 서버를 선택 하 고는 요청을 통해 OWIN 파이프라인을 생성 하는 워크플로 오케스트레이션 처리 됩니다.

  현재는 Katana 기반 응용 프로그램에 대 한 3 주 호스팅 옵션이 있습니다.  
  
**Iis/ASP.NET**: 표준 HttpModule 및 HttpHandler 형식을 사용 하 여, OWIN 파이프라인 실행할 수 있습니다 IIS에서 ASP.NET 요청 흐름의 일환으로 합니다. ASP.NET 호스팅 지원 웹 응용 프로그램 프로젝트로 Microsoft.AspNet.Host.SystemWeb NuGet 패키지를 설치 하 여 활성화 됩니다. 또한 IIS 호스트와 서버 역할을 하므로 OWIN 서버/호스트 구분은 부모의 SystemWeb 호스트를 사용 하는 경우 개발자 수 없습니다. 대체 서버 구현을 대체 하므로이 NuGet 패키지에 있습니다.  
  
**사용자 지정 호스트**: The Katana 구성 요소 제품군 있게 개발자가 자신의 사용자 지정 프로세스에서 호스트 응용 프로그램에는 콘솔 응용 프로그램, Windows 서비스 등 무엇 인지에 있습니다. 이 기능은 Web API에서 제공 되는 기능은 자체 호스트 하는 것과 유사 합니다. 다음 예제에서는 웹 API 코드의 사용자 지정 호스트를 보여 줍니다.  

[!code-csharp[Main](an-overview-of-project-katana/samples/sample5.cs)]

Katana 응용 프로그램을 위한 자체 호스트 설정이 비슷합니다.

[!code-csharp[Main](an-overview-of-project-katana/samples/sample6.cs)]

Web API 및 Katana self-host 예제 간의 주요 차이점 중 하나는 Web API 구성 코드 Katana self-host 예제에서 누락 된 경우 Katana는 이식성 및 작성을 사용 하도록 설정 하기 위해 요청 처리 파이프라인을 구성 하는 코드에서 서버를 시작 하는 코드를 구분 합니다. 그런 다음 웹 API를 구성 하는 코드는 또한 WebApplication.Start에서 형식 매개 변수로 지정 된 시작 클래스에 포함 됩니다.

[!code-csharp[Main](an-overview-of-project-katana/samples/sample7.cs)]

Startup 클래스는 문서의 뒷부분에서 자세히 설명 합니다. 그러나 코드는 ASP.NET Web API를 자체 호스팅하는 응용 프로그램에서 사용 하 여 현재 코드를 자체 호스트 프로세스 것과 상당히 비슷한 Katana를 시작 해야 합니다.

**OwinHost.exe**: Katana 웹 응용 프로그램을 실행 하는 사용자 지정 프로세스를 작성 하려고 하는 일부를 하는 동안 여러 하려는 서버를 시작 하 고 응용 프로그램을 실행할 수 있는 미리 빌드된 실행 파일을 시작 합니다. Katana 구성 요소 suite는이 시나리오에서는 다음을 포함 합니다. `OwinHost.exe`합니다. 프로젝트의 루트 디렉터리 내에서 실행 하는 경우이 실행 파일 (HttpListener 서버 기본적으로 사용) 하는 서버 시작 되며를 찾아 사용자의 startup 클래스를 실행 하려면 규칙을 사용 됩니다. 보다 세분화 된 컨트롤에 대 한 실행 파일 추가 명령줄 매개 변수 개수를 제공합니다.

![](an-overview-of-project-katana/_static/image4.png)

## <a name="server"></a>서버

 호스트는 시작 하 고 있는 응용 프로그램이 실행 되는 프로세스를 서버의 책임을 유지 관리 하는 일을 담당 하는 동안 네트워크 소켓을 열고, 요청에 대 한 수신 파이프라인의 OWIN 구성 요소를 통해 보낼 지정 (때 사용자가 이미 나타나는데,이 파이프라인은 응용 프로그램 개발자의 Startup 클래스에 지정 된) 현재 Katana 프로젝트에 두 가지 서버 구현을 포함 합니다. 

- **Microsoft.Owin.Host.SystemWeb**: 앞서 언급 했 듯이, ASP.NET 파이프라인을 사용 하 여 함께에서 IIS 호스트와 서버 역할도 합니다. 따라서이 호스팅 옵션을 선택 하는 경우 IIS 프로세스 활성화 같은 호스트 수준 문제를 관리 및 HTTP 요청을 수신 합니다. ASP.NET 웹 응용 프로그램에 대 한 다음 보냅니다 요청은 ASP.NET 파이프라인에. Katana SystemWeb 호스트는 HTTP 파이프라인을 통과 하며 사용자가 지정한 OWIN 파이프라인을 통해 보낼 요청을 가로채 ASP.NET HttpModule 및 HttpHandler를 등록 합니다.
- **Microsoft.Owin.Host.HttpListener**: 해당 이름으로이 Katana 서버 클래스 사용 하 여.NET Framework의 HttpListener 소켓을 열고 개발자가 지정한 OWIN 파이프라인으로 요청을 보냅니다. 이 옵션은 현재 Katana 자체 호스팅하는 API와 OwinHost.exe에 대 한 기본 서버 선택 합니다.

## <a name="middlewareframework"></a>미들웨어/프레임 워크

 이전에 설명한 것 처럼 서버가 클라이언트에서 요청을 수락 하는 경우 담당 OWIN 구성 요소 개발자의 시작 코드에서 지정 하는 파이프라인을 통해 전달 합니다. 이러한 파이프라인 구성 요소를 사용 하 여 미들웨어 라고 합니다.  
 기본적인 수준에서 OWIN 미들웨어 구성 요소는 간단히 호출할 수 있도록 OWIN 응용 프로그램 대리자를 구현 하 해야 합니다.

[!code-console[Main](an-overview-of-project-katana/samples/sample8.cmd)]

그러나 미들웨어 구성 요소 조합 고 개발을 간소화 하기 위해 Katana는 적은 수의 규칙 및 도우미 형식 미들웨어 구성 요소에 대 한 지원 합니다. 이러한 가장 일반적입니다는 `OwinMiddleware` 클래스입니다. 이 클래스를 사용 하 여 빌드된 사용자 지정 미들웨어 구성 요소는 다음과 비슷하게 표시 됩니다. 

[!code-csharp[Main](an-overview-of-project-katana/samples/sample9.cs)]

 이 클래스에서 파생 됩니다 `OwinMiddleware`, 해당 인수 중 하나로 파이프라인의 다음 미들웨어의 인스턴스를 받고 그런 다음 기본 생성자에 전달 하는 생성자를 구현 합니다. 또한 미들웨어를 구성 하는 데 사용 되는 추가 인수는 다음 미들웨어 매개 변수 뒤 생성자 매개 변수로 선언 됩니다.   
  
런타임 시 미들웨어가 실행 되는 재정의 통해 `Invoke` 메서드. 이 메서드는 형식의 단일 인수 `OwinContext`합니다. 이 컨텍스트 개체에서 제공 되는 `Microsoft.Owin` NuGet 패키지는 앞에서 설명한 하 고 몇 가지 추가 도우미 형식과 함께 요청, 응답 및 환경 사전에 대 한 강력한 형식의 액세스를 제공 합니다.   
  
미들웨어 클래스 쉽게 추가할 수를 OWIN 파이프라인에 응용 프로그램 시작 코드를 다음과 같이 합니다.   

[!code-csharp[Main](an-overview-of-project-katana/samples/sample10.cs)]

미들웨어 구성 요소에서 간단한에 이르기까지 Katana 인프라 OWIN 미들웨어 구성 요소를 파이프라인을 간단히 구축 및 구성 요소는 단순히 파이프라인에 참여 하도록 응용 프로그램 대리자를 지원 해야 하기 때문에 ASP.NET Web API와 같은 전체 프레임 워크에로 거 나 [SignalR](../../../signalr/index.md)합니다. 예를 들어, 이전 OWIN 파이프라인에 ASP.NET Web API를 추가할 필요 다음 시작 코드를 추가 합니다.

[!code-csharp[Main](an-overview-of-project-katana/samples/sample11.cs)]

Katana 인프라 구성 방법 IAppBuilder 개체에 추가 된 순서에 따라 미들웨어 구성 요소는 파이프라인을 작성 합니다. 그런 다음 예에서 LoggerMiddleware 이러한 요청은 궁극적으로 처리 하는 방법에 관계 없이 파이프라인을 통해 이동 하는 모든 요청을 처리할 수 있습니다. 이 미들웨어 구성 요소 (예: 인증 구성 요소) 여러 구성 요소 및 프레임 워크 (예: ASP.NET Web API, SignalR 및 정적 파일 서버)를 포함 하는 파이프라인에 대 한 요청을 처리할 수 있는 강력한 시나리오를 사용 하도록 설정 합니다.
 
## <a name="applications"></a>응용 프로그램

이전 예제에서 볼 수 있듯이, OWIN 및 Katana 프로젝트 없습니다 생각해 야 응용 프로그램 프로그래밍 모델 및 프레임 워크 서버 및 호스팅 인프라에서 분리 하는 추상화 대신 새 응용 프로그램 프로그래밍 모델을 아니라 합니다. 예를 들어, Web API 응용 프로그램을 빌드할 때 개발자 프레임 워크 Katana 프로젝트에서 구성 요소를 사용 하 여 OWIN 파이프라인의 응용 프로그램을 실행 하는 여부에 관계 없이 ASP.NET Web API 프레임 워크를 사용 하 여 계속 합니다. OWIN 관련 코드 응용 프로그램 개발자에 게 표시 될 위치 한곳 개발자 OWIN 파이프라인을 작성 하는 여기서 응용 프로그램 시작 코드에 게 됩니다. 시작 코드에서 개발자는 일련의 들어오는 요청을 처리 하는 각 미들웨어 구성 요소에 대 한 일반적으로 UseXx 문 등록 됩니다. 이 환경은 현재 System.Web 전 세계에서 HTTP 모듈을 등록 하는 것과 같은 효과 갖습니다. 일반적으로 더 큰 프레임 워크와 같은 미들웨어 ASP.NET Web API 또는 [SignalR](../../../signalr/index.md) 파이프라인의 끝에 등록 됩니다. 모든 프레임 워크 및 파이프라인의 뒷부분에서 등록 된 구성 요소에 대 한 요청 처리 됩니다 있도록 캐싱 또는 인증에 대 한 것과 같은 교차 미들웨어 구성 요소는 일반적으로 파이프라인의 시작 부분 쪽으로 등록 됩니다. 이 분리 미들웨어 구성 요소 및 기본 인프라 구성 요소에서 서로 다른 구성 요소를 전체 시스템이 안정적으로 유지 하면서 다양 한 속도에서 진화를 수 있습니다.

## <a name="components--nuget-packages"></a>구성 요소-NuGet 패키지

Katana 프로젝트 구성 요소는 많은 현재 라이브러리 및 프레임 워크와 마찬가지로 NuGet 패키지 집합으로 전달 됩니다. 이후 버전 2.0에 대 한 Katana 패키지 종속성 그래프의 형식은 다음과 같습니다. (더 크게 보려면 이미지 클릭).

[![](an-overview-of-project-katana/_static/image6.png)](an-overview-of-project-katana/_static/image5.png)

Katana 프로젝트에서 거의 모든 패키지에 따라 달라 집니다, 직접 또는 간접적으로 Owin 패키지 있습니다. 이 섹션 4 OWIN 사양에 설명 된 응용 프로그램 시작 시퀀스의 구체적인 구현을 제공 하는 IAppBuilder 인터페이스를 포함 하는 패키지는 아마 기억하실 것입니다. 또한 많은 패키지에 따라 달라 집니다 Microsoft.Owin HTTP 요청 및 응답 작업에 대 한 도우미 형식 집합을 제공 합니다. 패키지의 나머지 부분에서는 호스팅 인프라 패키지 (서버 또는 호스트) 또는 미들웨어로 분류할 수 있습니다. 패키지 및 종속성 Katana 프로젝트 외부에 주황색으로 표시 됩니다.

Katana 2.0에 대 한 호스팅 인프라의 SystemWeb 및 HttpListener 기반 서버, OwinHost.exe를 사용 하 여 OWIN 응용 프로그램을 실행 하기 위한 OwinHost 패키지 및 OWIN 응용 프로그램에서 자체 호스팅 Microsoft.Owin.Hosting 패키지 모두를 포함 한 사용자 지정 호스트 (예: 콘솔 응용 프로그램, Windows 서비스 등)

Katana 2.0 미들웨어 구성 요소는 주로 다른 인증 수단을 제공 합니다. 시작 및 오류 페이지에 대 한 지원을 사용 하도록 설정 하는 하나의 추가 미들웨어 구성 요소 진단을 위해 제공 됩니다. OWIN 호스팅 사실상 추상화로 증가 함에 따라, Microsoft 및 타사에서 개발한 것 모두 미들웨어 구성 요소 에코 시스템도 수에서 증가 합니다.

## <a name="conclusion"></a>결론

 해당부터 Katana 프로젝트의 목표를 만들고 있으므로 개발자가 또 웹 프레임 워크에 알아보려면 강제 적용 되지 않았습니다. 대신, 목표.NET 웹 응용 프로그램 개발자가 가능 했습니다 이전 보다 더 많은 선택 옵션이 제공 하는 추상화를 만들려고 했습니다. 논리적 계층을 일반적인 웹 응용 프로그램 스택의 대체할 수 있는 구성 요소 집합으로 나누면 Katana 프로젝트에서 이러한 구성 요소에 적합 한 모든 속도 향상 시킬 스택 전체에서 구성 요소를 수 있습니다. 간단한 OWIN 추상화 모든 구성 요소를 빌드하여 Katana은 프레임 워크 및 응용 프로그램을 기반으로 구축 된 다양 한 서로 다른 서버와 호스트 간에 이식 가능 합니다. 스택의 컨트롤에서 개발자를 넣어 Katana 개발자 경량 하는 방법에 대 한 궁극적인 선택할 수 있도록 보장 하는 방법 기능을 갖춘 자신의 웹 스택 이어야 합니다.  
  

## <a name="for-more-information-about-katana"></a>Katana에 대 한 자세한 내용은

- GitHub에서 Katana 프로젝트: [ https://github.com/aspnet/AspNetKatana/ ](https://github.com/aspnet/AspNetKatana/)합니다.
- 비디오: [Katana 프로젝트-ASP.NET 용 OWIN](https://channel9.msdn.com/Shows/Web+Camps+TV/The-Katana-Project-OWIN-for-ASPNET), Howard Dierking 여 합니다.

## <a name="acknowledgements"></a>감사의 글

- [Rick Anderson](https://blogs.msdn.com/b/rickandy/): (twitter [ @RickAndMSFT ](http://twitter.com/RickAndMSFT) ) Rick은 프로그래밍 수석 테크니컬 Microsoft Azure 및 MVC에 집중 합니다.
- [Scott Hanselman](http://www.hanselman.com/blog/): (twitter [ @shanselman ](https://twitter.com/shanselman) )
- [Jon Galloway](https://weblogs.asp.net/jgalloway/default.aspx): (twitter [ @jongalloway ](https://twitter.com/jongalloway) )
