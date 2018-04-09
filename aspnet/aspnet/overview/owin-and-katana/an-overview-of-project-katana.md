---
uid: aspnet/overview/owin-and-katana/an-overview-of-project-katana
title: 프로젝트 Katana의 개요 | Microsoft Docs
author: howarddierking
description: ASP.NET 프레임 워크 주위에 지난 10 년 동안 있었고 플랫폼이 많은 웹 사이트 및 서비스의 개발을 설정 합니다. 웹 응용 프로그램으로...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/30/2013
ms.topic: article
ms.assetid: 0ee21741-c1bf-4025-a9b0-24580cae24bc
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/owin-and-katana/an-overview-of-project-katana
msc.type: authoredcontent
ms.openlocfilehash: 3c2bcbbc6e506af759f6d77af17d015278cc0bdf
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="an-overview-of-project-katana"></a>프로젝트 Katana의 개요
====================
으로 [Howard Dierking](https://github.com/howarddierking)

> ASP.NET 프레임 워크 주위에 지난 10 년 동안 있었고 플랫폼이 많은 웹 사이트 및 서비스의 개발을 설정 합니다. 웹 응용 프로그램 개발 전략 진화 하는 대로 프레임 워크를 ASP.NET MVC와 ASP.NET Web API와 같은 기술 사용 하는 단계에서 발전 있었습니다. 웹 응용 프로그램 개발이 다음 발전적인 단계로 클라우드 컴퓨팅의 전 세계를 사용 하는 대로 프로젝트 [Katana](https://channel9.msdn.com/Shows/Web+Camps+TV/The-Katana-Project-OWIN-for-ASPNET) 구성 요소를 유연 하 고, 휴대용 될 수 있도록 ASP.NET 응용 프로그램의 기본 집합을 제공 경량 – 더 나은 성능을 제공 하 고 프로젝트, 즉 [Katana](https://channel9.msdn.com/Shows/Web+Camps+TV/The-Katana-Project-OWIN-for-ASPNET) 클라우드 ASP.NET 응용 프로그램을 최적화 합니다.


## <a name="why-katana--why-now"></a>이유 Katana – 이제 이유?

 개발자 프레임 워크 또는 최종 사용자 제품을 논의 하는 하나 여부에 관계 없이, 것이 중요을 만들기 위한 기본 동기를 이해 하려면 제품 –와 그 과정에는 제품에 대해 만들어진 누구 인지 알고 있습니다. ASP.NET 염두에서 두 고객으로 원래 만들어졌습니다.   
  
**고객의 첫 번째 그룹 클래식 ASP 개발자 했습니다.** 당시에 ASP 태그 및 서버 쪽 스크립트 interweaving 하 여 동적, 데이터 기반 웹 사이트 및 응용 프로그램을 만들기 위한 기본 기술 중 하나 였습니다. ASP 런타임 기본 HTTP 프로토콜 및 웹 서버의 핵심 측면 추상화 되 고 캐시, 등 추가에 대 한 액세스 같은 세션 및 응용 프로그램 상태 관리 서비스 제공 하는 개체의 집합을 포함 하는 서버 쪽 스크립트를 제공 합니다. 강력 하는 동안 클래식 ASP 응용 프로그램의 크기와 복잡성 천으로 관리 하는 챌린지 업체가 되었습니다. 이 주로 스크립팅 환경에서 코드 및 태그의 인터리빙으로 인해 발생 하는 코드의 중복와 결합 되어 있는 구조가 없기 때문입니다. 과제 중 일부를 해결 하는 동안 기본 ASP의 장점을 이용 하기 위해 ASP.NET의 순서로 서버 쪽 프로그래밍 모델을 유지 하는 동안.NET Framework의 개체 지향 언어에서 제공 하는 코드 조직 어떤 기본 ASP를 개발자가 익숙한 발전 했습니다.

**ASP.NET에 대 한 대상 고객의 두 번째 그룹에서 Windows 비즈니스 응용 프로그램 개발자.** HTML 태그 및 더 많은 HTML 태그를 생성 하는 코드를 작성 하는 익숙한 이었던, 클래식 ASP 개발자와 달리 (예: 앞 VB6 개발자) WinForms 개발자가 익숙한 캔버스 및 다양 한 사용자를 포함 하는 디자인 타임 환경 인터페이스를 제어 합니다. 첫 번째 버전의 ASP.NET – 라고도 "Web Forms" 사용자 인터페이스 구성 요소에 대 한 서버 쪽 이벤트 모델 및 인프라 기능 (예: ViewState) 집합이 함께 비슷한 디자인 타임 환경을 만들 수 있도록 제공 원활한 개발자 환경 클라이언트와 서버 쪽 프로그래밍 합니다. Web Forms WinForms 개발자에 게 친숙 하는 상태 저장 이벤트 모델에서 웹의 상태 비저장 특성을 효과적으로 숨긴 합니다.

### <a name="challenges-raised-by-the-historical-model"></a>기록 모델에 의해 발생 하는 문제

**그 결과 성숙한, 기능을 갖춘 런타임 및 개발자의 프로그래밍 모델을 했습니다.** 그러나와 기능이 풍부 가져온 주목할 만한 몇 가지 과제입니다. 첫째, 프레임 워크를 **모놀리식**의 기능 (예를 들어 Web forms framework와 함께 HTTP 핵심 개체)의 동일한 System.Web.dll 어셈블리에 강력 하 게 결합 되 고 논리적으로 서로 다른 단위입니다. ASP.NET을 더 큰.NET Framework의 일부로 포함 된 둘째,는 **릴리스 사이 시간 년 단위인 것입니다.** 이 때문에 맞춰 모든 웹 개발을 신속 하 게 진화에서 발생 하는 변경에는 ASP.NET 용 어려운입니다. 특정 웹 호스팅 옵션에는 몇 가지 방법에서 자체 System.Web.dll 결합 된가 마지막으로,: 인터넷 정보 서비스 (IIS).

### <a name="evolutionary-steps-aspnet-mvc-and-aspnet-web-api"></a>발전적인 단계: ASP.NET MVC와 ASP.NET Web API

및 변경의 많은 웹 개발에서 발생 했습니다! 웹 응용 프로그램은 일련의 작은 큰 프레임 워크를 사용 하지 않고 구성 요소를 중심으로 점점 더 개발 되 고 합니다. 현재까지 빠른 속도로 증가 하 고 있는 출시 빈도 뿐만 아니라 구성 요소 수 있었습니다. 프레임 워크를 가져오고 작은, 분리 된 더욱 중점을 둔 크고 더 구성 요소와 대신 따라서 웹과 속도 유지할 필요는 명백는 **ASP.NET 팀의 제품군으로 ASP.NET을 사용 하도록 설정 하려면 몇 가지 혁신적인 단계를 진행 합니다. 단일 프레임 워크 보다는 플러그형 Web components**합니다.

초기 변경 사항 중 하나 레일에 인기도 Ruby 같은 웹 개발 프레임 워크 덕분에 잘 알려진 모델-뷰-컨트롤러 (MVC) 디자인 패턴의 증가 했습니다. 개발자를 지정 하는이 스타일 웹 응용 프로그램의 ASP.NET에 대 한 초기 판매 전략이 중 하나인 태그 및 비즈니스 논리의 분리를 보존 하면서 자신의 응용 프로그램의 태그에 대 한 제어 강화 합니다. 이 스타일의 웹 응용 프로그램 개발에 대 한 요구를 충족 하기 위해 Microsoft는 데 걸린 배치 하 여 미래를 위한 더 나은 **대역 외에서 ASP.NET MVC 개발** (및.NET Framework에서 제외). ASP.NET MVC는 독립적인 다운로드로 출시 되었습니다. 이 표기법을 사용 하는 엔지니어링 팀 되 던 것 보다 훨씬 더 자주 업데이트를 제공 하도록 합니다.

웹 응용 프로그램 개발에 또 다른 큰 변화를 동적 통신 하는 클라이언트 쪽 스크립트에서 생성 된 페이지 섹션을 사용 하 여 정적 초기 태그를 동적 서버에서 생성 된 웹 페이지에서 shift **웹 Api 백 엔드를 통해 AJAX 요청**합니다. 이 아키텍처 전환을 작업의 웹 Api 및 ASP.NET Web API 프레임 워크의 개발 날 려 보내는 수 있습니다. ASP.NET Web API의 릴리스는 ASP.NET MVC의 경우 ASP.NET 모듈식 프레임 워크로 추가로 개발할 수 있는 기회를 제공 합니다. 팀은 엔지니어링 팀 기회의 활용 및 **System.Web.dll에 있는 핵심 프레임 워크 형식 중 하나에 종속성이 없는 이전의 되도록 ASP.NET Web API 작성**합니다. 이 두 가지 작업을 사용할 수: 하는 것 먼저 완전히 독립 된 방법으로 ASP.NET Web API 수 발전 (및 NuGet을 통해 전달 되기 때문에 신속 하 게 반복을 계속할 수 없습니다). 둘째, System.Web.dll 하는 외부 종속성 및 IIS에 종속성이 없는 따라서 없었기 때문에 ASP.NET Web API 포함 (예를 들어는 콘솔 응용 프로그램, Windows 서비스 등)는 사용자 지정 호스트에서 실행 하는 기능

### <a name="the-future-a-nimble-framework"></a>미래: 민첩 프레임 워크

다른 프레임 워크 구성 요소를 분리 하 고 NuGet에 해제를 프레임 워크 수 이제 **독립적으로 더 및 보다 신속 하 게 반복**합니다. 또한 작업 효율성과 웹 API의 자체 호스팅 기능의 유연성 증대를 입증 원하는 개발자에 게 매우 매력적인는 **작은 사용할 수 있는 경량 호스트** 들이 서비스에 대 한 합니다. 더욱 매력적인 입증, 사실, 다른 프레임 워크에도이 기능을 원하는 있으며 각 프레임 워크 자체 기본 주소에서 자체 호스트 프로세스에서 실행 되 고 (시작, 중지 됨, 등) 관리 하는 데 필요한 새 챌린지를 표시이 독립적으로 합니다. 최신 웹 응용 프로그램에는 일반적으로 정적 파일 서비스, 동적 페이지를 생성, 웹 API 및 보다 최근에 실시간-일회용/푸시 알림을 지원합니다. 이러한 각 서비스를 실행 하 고 해야 독립적으로 관리할 필요 없습니다 단순히 현실적인.

사용 하는 다양 한 여러 구성 요소 및 프레임 워크의 응용 프로그램을 작성 하는 개발자 및 다음 지 원하는 호스트에서 해당 응용 프로그램을 실행 하는 단일 호스팅 추상화가 필요 했습니다.

## <a name="the-open-web-interface-for-net-owin"></a>For.NET (OWIN) 열린 웹 인터페이스

 얻을 수 있는 장점을에서 영감을 얻은 [랙](http://rack.github.io/) Ruby 커뮤니티.NET 커뮤니티의 여러 멤버 세우고 웹 서버와 프레임 워크 구성 요소 간의 추상화를 만들려고 합니다. OWIN 추상화에 대 한 두 가지 디자인 목표에는 이것은 단순 및 다른 프레임 워크 형식에 가능한 가장 적은 종속성 걸린다는 했습니다. 이 두 가지 목표 수 있도록 합니다.

- 새 구성 요소 보다 쉽게 개발 하 고 사용 될 수 있습니다.
- 응용 프로그램 호스트와 잠재적으로 전체 플랫폼/운영 체제 간에 더 쉽게 이식할 수 없습니다.

결과 추상화 두 가지 핵심 요소로 구성 됩니다. 첫 번째는 환경 사전입니다. 이 데이터 구조는의 모든 관련 서버 상태 뿐만 아니라 HTTP 요청 및 응답을 처리 하는 데 필요한 상태를 저장 해야 합니다. 환경 사전은 다음과 같이 정의 됩니다.

[!code-console[Main](an-overview-of-project-katana/samples/sample1.cmd)]

OWIN 호환 웹 서버는 본문 스트림과 HTTP 요청 및 응답에 대 한 헤더 컬렉션 등의 데이터를 사용 하 여 환경 사전 채우는 데 사용 합니다. 응용 프로그램이 나 프레임 워크 구성 요소를 채울 또는 추가 값이 포함 된 사전 업데이트 및 응답 본문 스트림에 쓰기 작업은 다음 합니다.

환경 사전에 대 한 형식 지정, 외에도 OWIN 사양 코어 사전 키/값 쌍의 목록을 정의 합니다. 예를 들어 다음 표에서 HTTP 요청에 필요한 사전 키를 보여 줍니다.

| 키 이름 | 값 설명 |
| --- | --- |
| `"owin.RequestBody"` | 있는 경우 요청 본문 스트림. 요청 본문이 없습니다 경우 Stream.Null 자리 표시자로 사용할 수 있습니다. 참조 [요청 본문](http://owin.org/html/owin.html#34-request-body-100-continue-and-completed-semantics)합니다. |
| `"owin.RequestHeaders"` | `IDictionary<string, string[]>` 요청 헤더의 합니다. 참조 [헤더](http://owin.org/html/owin.html#3-3-headers)합니다. |
| `"owin.RequestMethod"` | A `string` 요청의 HTTP 요청 메서드를 포함 (예: `"GET"`, `"POST"`). |
| `"owin.RequestPath"` | A `string` 요청 경로 포함 합니다. 경로 "root" 응용 프로그램 대리자;의 기준으로 해야 합니다. 참조 [경로](http://owin.org/html/owin.html#5-3-paths)합니다. |
| `"owin.RequestPathBase"` | A `string` 참조에 해당 하는 응용 프로그램 대리자;의 "root" 요청 경로 부분을 포함 하 [경로](http://owin.org/html/owin.html#5-3-paths)합니다. |
| `"owin.RequestProtocol"` | A `string` 프로토콜 이름 및 버전 (예: `"HTTP/1.0"` 또는 `"HTTP/1.1"`). |
| `"owin.RequestQueryString"` | A `string` 선행 공백 없이 HTTP 요청 URI의 쿼리 문자열 구성 요소가 포함 된 "?" (예: `"foo=bar&baz=quux"`). 값은 빈 문자열일 수 있습니다. |
| `"owin.RequestScheme"` | A `string` 요청에 사용 되는 URI 체계를 포함 (예: `"http"`, `"https"`); 참조 [URI 체계](http://owin.org/html/owin.html#5-1-uri-scheme)합니다. |

OWIN의 두 번째 주요 요소에는 응용 프로그램 대리자입니다. OWIN 응용 프로그램의 모든 구성 요소 사이의 기본 인터페이스로 사용 되는 함수 시그니처입니다. 응용 프로그램 대리자에 대 한 정의 다음과 같습니다.

`Func<IDictionary<string, object>, Task>;`

다음 응용 프로그램 대리자는 함수 환경 사전을 입력으로 수락 하 고 작업을 반환 하는 여기서 Func 대리자 형식의 구현 하기만 하면 됩니다. 이 설계는 개발자를 위한 다음을 의미 합니다.

- OWIN 구성 요소를 작성 하는 데 필요한 유형 종속성의 매우 작은 여러 가지가 있습니다. 이 개발자에 게 OWIN의 액세스 가능성을 크게 증가합니다.
- 비동기 디자인을 컴퓨팅 리소스에 더 많은 I/O 집약적인 작업에서 특히의 처리 능력으로 효율적으로 추상화 수 있습니다.
- 응용 프로그램 대리자 실행의 원자 단위 이며 OWIN 구성 요소를 쉽게 연결할 수 있으므로 대리자에 매개 변수로 환경 사전을 수행 하는 때문에 파이프라인을 처리 하는 복잡 한 HTTP를 만들어야 합니다.

구현 측면에서 볼 때 OWIN는 사양 ([http://owin.org/html/owin.html](http://owin.org/html/owin.html)). 목표 다음 웹 프레임 워크 하지만 웹 프레임 워크 및 웹 서버 상호 작용 방식에 대 한 사양 아니라 해서는 안 됩니다.

조사 한 경우 [OWIN](http://owin.org/) 또는 [Katana](https://github.com/aspnet/AspNetKatana/wiki), 또한 단어로 [Owin NuGet 패키지](http://nuget.org/packages/Owin) 및 Owin.dll 합니다. 이 라이브러리에 단일 인터페이스 [IAppBuilder](https://github.com/owin/owin/blob/master/src/Owin/IAppBuilder.cs)를 공식화 하 고 시작 시퀀스에 설명 된 것 [섹션 4](http://owin.org/html/owin.html#4-application-startup) OWIN 사양의 합니다. OWIN 서버를 구축 하기 위해 필요는 없지만 [IAppBuilder](https://github.com/owin/owin/blob/master/src/Owin/IAppBuilder.cs) 인터페이스는 구체적 참조점을 제공 하 고 Katana 프로젝트 구성 요소에서 사용 됩니다.

## <a name="project-katana"></a>프로젝트 Katana

반면 모두는 [OWIN](http://owin.org/html/owin.html) 사양 및 *Owin.dll* 소유 하는 커뮤니티 및 오픈 소스 활동을 실행 하는 커뮤니티는 [Katana](https://github.com/aspnet/AspNetKatana/wiki) 프로젝트 OWIN의 집합을 나타냅니다 여전히 오픈 소스 하는 동안 빌드 및 Microsoft에서 릴리스한 구성 요소입니다. 이러한 구성 요소 호스트와 서버 등의 인프라 구성 요소 뿐만 아니라 프레임 워크에 대 한 바인딩을 인증 구성 요소 등의 기능 구성 요소 포함와 같은 [SignalR](../../../signalr/index.md) 및 [ASP.NET 웹 API](../../../web-api/overview/getting-started-with-aspnet-web-api/index.md)합니다. 프로젝트에는 다음 세 가지 높은 수준의 목표에 있습니다. 

- **휴대용** – 구성 요소를 제공 하는 새 구성 요소에 대 한 쉽게 대체할 수 있어야 합니다. 이 모든 유형의 서버 및 호스트 하기 위해 프레임 워크에서 구성 요소를 포함합니다. 이 목표 방식은 Microsoft 프레임 워크 제 3 자 서버와 호스트에서 실행 될 수 있습니다 하는 동안 타사 프레임 워크 Microsoft 서버에서 실행할 원활 하 게 수 있습니다.
- **모듈식/유연한**–는 수많은 기본적으로 켜져 있는 기능을 포함 하는 여러 프레임 워크와 달리 작고 집중 된 구성 요소를 결정 하는 데 응용 프로그램 개발자에 게를 통해 제어할 Katana 프로젝트 구성 요소 여야 합니다 그녀의 응용 프로그램에서 사용 합니다.
- **Lightweight/성능/확장성** – 작은 집합으로 프레임 워크의 일반적인 개념을 분리 하 여 구성 요소에 의해 추가 된 명시적으로 응용 프로그램 개발자 결과 Katana 응용 프로그램은 더 적은 컴퓨팅 소비할 수 있는 포커스 있음 리소스, 결과적으로, 다른 유형의 서버 및 프레임 워크 보다 더 많은 부하를 처리 합니다. 기본 인프라에서 더 많은 기능을 요구 하는 응용 프로그램의 요구 사항, OWIN 파이프라인에 추가할 수 있는 하지만 응용 프로그램 개발자 안되며 명시적 결정 하는 수 있을 것입니다. 또한 하위 수준의 구성 요소 대체를 사용 가능 해지면 새 고성능 서버 원활 하 게 적용 될 수 있습니다 이러한 응용 프로그램을 중단 하지 않고 OWIN 응용 프로그램의 성능을 개선 하기 위해 의미 합니다.

## <a name="getting-started-with-katana-components"></a>Katana 구성 요소 시작

처음으로 도입의 한 가지 측면에서 [Node.js](http://nodejs.org/) 즉시 사람의 주의 그린 프레임 워크 단순성 하나 수를 작성 하 고 있는 웹 서버를 실행 했습니다. Katana 목표 light의 구성 된 경우 [Node.js](http://nodejs.org/), Katana 많은의 혜택을 제공 한다는 것으로 요약할 수 하나 [Node.js](http://nodejs.org/) (및 그와 같은 프레임 워크) 개발자 던져을 시작 하지 않고 모든 ASP.NET 웹 응용 프로그램을 개발 하는 방법에 대 한 알고 있습니다. 이 문을 true 유지 Katana 프로젝트 시작 동일 하 게 간단해 야 기본적에서 [Node.js](http://nodejs.org/)합니다.

## <a name="creating-hello-world"></a>"Hello World!" 만들기

중요 한 차이점 JavaScript 및.NET 개발은 컴파일러의 현재 상태 (또는 부재). 따라서 간단한 Katana 서버에 대 한 시작 지점을 Visual Studio 프로젝트입니다. 그러나 프로젝트 형식의 가장 최소 시작할 수 있습니다: 빈 ASP.NET 웹 응용 프로그램입니다.

[![](an-overview-of-project-katana/_static/image1.png)](http://nuget.org/packages/Microsoft.Owin.Host.SystemWeb)

다음으로, 설치 하겠습니다는 [Microsoft.Owin.Host.SystemWeb](http://nuget.org/packages/Microsoft.Owin.Host.SystemWeb) NuGet 패키지를 프로젝트에 있습니다. 이 패키지는 ASP.NET 요청 파이프라인에서 실행 되는 OWIN 서버를 제공 합니다. 찾을 수 있습니다는 [NuGet 갤러리](http://nuget.org/packages/Microsoft.Owin.Host.SystemWeb) 이며 Visual Studio 패키지 관리자 대화 상자 또는 패키지 관리자 콘솔을 사용 하 여 다음 명령을 사용 하 여 설치할 수 있습니다.

[!code-console[Main](an-overview-of-project-katana/samples/sample2.cmd)]

설치는 `Microsoft.Owin.Host.SystemWeb` 패키지에서는 종속성으로 몇 가지 추가 패키지를 설치 합니다. 이러한 종속성 중 하나는 `Microsoft.Owin`, 라이브러리를 여러 도우미 형식 및 OWIN 응용 프로그램을 개발 하기 위한 메서드를 제공 합니다. "Hello world" 서버를 신속 하 게 쓰려고 이러한 형식을 사용할 수 있습니다.

[!code-csharp[Main](an-overview-of-project-katana/samples/sample3.cs)]

Visual Studio를 사용 하 여이 매우 간단한 웹 서버를 실행할 수 있습니다 **F5** 명령 작성과 디버깅에 대 한 완벽 하 게 지원 합니다.

## <a name="switching-hosts"></a>호스트를 전환합니다.

기본적으로 앞의 "hello world" 예제 System.Web를 사용 하 여 IIS의 컨텍스트에서 ASP.NET 요청 파이프라인에서 실행 됩니다. 이 단독으로 추가할 수 값 엄청난 유연성과 관리 기능을 가진 OWIN 파이프라인의 작성 및 전반적인 maturity IIS의 이점을 활용할 수 있도록 합니다. 그러나 IIS에서 제공 하는 장점을 필요 하지 않습니다. 함을 소규모의 용량이 호스트 하는 경우가 있을 수 있습니다. 기능, 그런 다음 실행 하는 데는 간단한 웹 서버 IIS 및 System.Web 외부?

다음 호스트를 시작 하 고 프로젝트의 출력 폴더에 새 서버와 호스트 종속성을 추가 하기만 하면 이식성 목표를 설명 하기 위해 필요 명령줄 호스트에는 웹 서버 호스트에서 이동 합니다. 이 예제에서는 이라는 Katana 호스트의 웹 서버를 호스팅할에서는 `OwinHost.exe` Katana HttpListener 기반 서버를 사용 합니다. 마찬가지로 다른 Katana 구성 요소로, 여기에 확보 됩니다 다음 명령을 사용 하 여 NuGet에서:

[!code-console[Main](an-overview-of-project-katana/samples/sample4.cmd)]

명령줄에서 프로젝트 루트 폴더를 찾습니다 및를 실행 하면 수 우리는 `OwinHost.exe` (함께 설치 된 각 NuGet 패키지의 tools 폴더에서). 기본적으로 `OwinHost.exe` HttpListener 기반 서버에 대 한 확인 하도록 구성 되어 있으므로 추가 구성은 필요 하지 않습니다. 웹 브라우저에서 탐색 `http://localhost:5000/` 콘솔을 통해 실행 중인 응용 프로그램을 보여 줍니다.

![](an-overview-of-project-katana/_static/image2.png)

## <a name="katana-architecture"></a>Katana 아키텍처

 Katana 구성 요소 아키텍처 아래와 같이 4 개의 논리적 계층으로 응용 프로그램을 나누는: *호스트, 서버, 미들웨어* 및 *응용 프로그램*합니다. 구성 요소 아키텍처 있는지 이러한 계층의 구현 쉽게 대체할 수, 대부분의 경우에서 응용 프로그램을 컴파일하지 않고 하는 방식으로 구분 됩니다.   

![](an-overview-of-project-katana/_static/image3.png)

## <a name="host"></a>호스트

 호스트는에 대 한 합니다.

- 기본 프로세스를 관리 합니다.
- 서버를 선택 하 고 있는 요청을 통해 OWIN 파이프라인을 생성 하는 워크플로 오케스트레이션으로 처리 됩니다.

  현재,는 Katana 기반 응용 프로그램에 대 한 3 주 호스팅 옵션이 있습니다.  
  
**Iis/ASP.NET**: 표준 HttpModule 및 HttpHandler 종류를 사용 하 여 OWIN 파이프라인 실행할 수 IIS에서 ASP.NET 요청 흐름의 일환으로 합니다. 호스팅 지원 되는 ASP.NET 웹 응용 프로그램 프로젝트에 Microsoft.AspNet.Host.SystemWeb NuGet 패키지를 설치 하 여 활성화 됩니다. 또한 IIS 및 역할을 호스트 하는 서버, 때문에 OWIN 서버/호스트 구분은 혼합 SystemWeb 호스트를 사용 하는 경우 개발자 없습니다 대체 서버 구현을 대체 의미이 NuGet 패키지에 있습니다.  
  
**사용자 지정 호스트**: The Katana 구성 요소 도구 모음 기능을 제공 개발자는 자신의 사용자 지정 프로세스에서 호스트 응용 프로그램에 콘솔 응용 프로그램, Windows 서비스 등 제공할지 여부입니다. 이 기능 자체 호스트 기능은 웹 API에서 제공 하는 것과 유사 합니다. 다음 예제에서는 사용자 지정 호스트의 웹 API 코드를 보여 줍니다.  

[!code-csharp[Main](an-overview-of-project-katana/samples/sample5.cs)]

Katana 응용 프로그램에 대 한 자체 호스트 설치 프로그램은 유사 합니다.

[!code-csharp[Main](an-overview-of-project-katana/samples/sample6.cs)]

중요 한 차이점 웹 API 및 Katana 자체 호스트 예제 Web API 구성 코드 Katana 자체 호스트 예제에 나오지 된다는 점입니다. Katana 성과 작성 가능성을 사용 하려면 서버 요청 처리 파이프라인을 구성 하는 코드에서 시작 하는 코드를 구분 합니다. 다음 웹 API를 구성 하는 코드는 또한 WebApplication.Start에서 형식 매개 변수로 지정 된 시작 클래스에 포함 됩니다.

[!code-csharp[Main](an-overview-of-project-katana/samples/sample7.cs)]

시작 클래스 문서의 뒷부분에 자세히 설명 합니다. 그러나 코드는 ASP.NET Web API 자체 호스팅 응용 프로그램에서 사용 하 여 오늘 하는 코드를 자체 호스팅하는 프로세스 상당히 유사 Katana 시작 해야 합니다.

**OwinHost.exe**: Katana 웹 응용 프로그램을 실행 하는 사용자 지정 프로세스를 작성 하려고는 일부, 하지만 많은 방법을 간단히 서버를 시작 하 고 해당 응용 프로그램을 실행할 수 있는 미리 빌드된 실행 파일을 시작 합니다. Katana 구성 요소 suite에 포함 된이 시나리오에서는 `OwinHost.exe`합니다. 프로젝트의 루트 디렉터리 내에서 실행 하는 경우이 실행 파일 (사용 하 여 HttpListener 서버 기본적으로) 서버 시작 되며을 찾고 실행할 사용자의 시작 클래스입니다. 규칙을 사용 됩니다. 실행 파일 보다 세부적인 제어에는 여러 추가 명령줄 매개 변수를 제공합니다.

![](an-overview-of-project-katana/_static/image4.png)

## <a name="server"></a>서버

 호스트를 시작 하 고 있는 응용 프로그램 실행 프로세스 서버의 책임을 유지 관리 하는 동안를 네트워크 소켓을 열고 요청을 수신 대기, OWIN 구성 요소는 파이프라인을 통해 보낼 지정 (때 사용자가 이미 단어로, 응용 프로그램 개발자 시작 클래스에이 파이프라인 지정). 현재 Katana 프로젝트에는 두 서버 구현이 포함 되어 있습니다. 

- **Microsoft.Owin.Host.SystemWeb**: 듯이 ASP.NET 파이프라인와 함께에서 IIS 및 역할을 호스트 하는 서버입니다. 따라서이 호스팅 옵션을 선택할 때 IIS 프로세스 활성화와 같은 호스트 수준 문제를 관리 및 모두 HTTP 요청을 수신 합니다. ASP.NET 웹 응용 프로그램에 대 한 그 다음의 요청으로 전송 ASP.NET 파이프라인 됩니다. Katana SystemWeb 호스트는 ASP.NET HttpModule 및 HttpHandler HTTP 파이프라인을 통해 이동 하 고 사용자가 지정한 OWIN 파이프라인을 통해 보낼 요청을 가로채 등록 합니다.
- **Microsoft.Owin.Host.HttpListener**: 이름을 나타냅니다이 Katana 서버를 사용 하 여.NET Framework의 HttpListener 클래스 소켓 열 및 개발자가 지정한 OWIN 파이프라인에 요청을 보냅니다. 이 옵션은 현재 OwinHost.exe와 Katana 자체 호스팅 API에 대 한 기본 서버 선택 합니다.

## <a name="middlewareframework"></a>미들웨어/프레임 워크

 위에서 언급 한 대로 서버가 클라이언트에서 요청을 수락 하는 경우 담당 OWIN 구성 요소 개발자의 시작 코드에 의해 지정 되는 파이프라인을 통해 전달 합니다. 이러한 파이프라인 구성 요소를 사용 하 여 미들웨어도 알려져 있습니다.  
 매우 기본적인 수준에서는 OWIN 미들웨어 구성 요소 단순히를 호출할 수 있도록 OWIN 응용 프로그램 대리자를 구현 해야 합니다.

[!code-console[Main](an-overview-of-project-katana/samples/sample8.cmd)]

그러나, 개발 및 컴퍼지션 미들웨어 구성 요소를 간단 하 게 하기 위해 Katana 지원 규칙 및 도우미 형식에는 소수의 미들웨어 구성 요소에 대 한 합니다. 이 중 가장 일반적인은는 `OwinMiddleware` 클래스입니다. 이 클래스를 사용 하 여 빌드된 사용자 지정 미들웨어 구성 요소는 다음과 같습니다. 

[!code-csharp[Main](an-overview-of-project-katana/samples/sample9.cs)]

 이 클래스에서 파생 `OwinMiddleware`를 구현 하는 생성자의 인수 중 하나로 파이프라인의 다음 미들웨어의 인스턴스를 허용 하 고 기본 생성자에 전달 합니다. 미들웨어를 구성 하는 데 사용 되는 추가 인수는 다음 미들웨어 매개 변수 뒤에 생성자 매개 변수도도 선언 됩니다.   
  
런타임 시 미들웨어가 실행 되는 재정의 통해 `Invoke` 메서드. 이 메서드는 형식의 단일 인수를 사용 `OwinContext`합니다. 이 컨텍스트 개체에서 제공 되는 `Microsoft.Owin` NuGet 패키지는 앞에서 설명한 하 고 몇 가지 추가 도우미 형식과 함께 요청, 응답 및 환경 사전에 대 한 강력한 형식의 액세스를 제공 합니다.   
  
미들웨어 클래스 쉽게 추가할 수는 응용 프로그램 시작 코드 OWIN 파이프라인에 다음과 같습니다.   

[!code-csharp[Main](an-overview-of-project-katana/samples/sample10.cs)]

Katana 인프라는 단순히 OWIN 미들웨어 구성 요소는 파이프라인을 빌드 및 구성 요소는 단순히 파이프라인에 참여 하도록 응용 프로그램 대리자를 지 원하는 데 필요 하기 때문에 미들웨어 구성 요소에에서 이르기까지 다양 simple에서 ASP.NET, 웹 API와 같은 전체 프레임 워크로 거 또는 [SignalR](../../../signalr/index.md)합니다. 예를 들어, ASP.NET Web API 이전 OWIN 파이프라인에 추가 다음 시작 코드를 추가 하려면:

[!code-csharp[Main](an-overview-of-project-katana/samples/sample11.cs)]

Katana 인프라 미들웨어 구성 요소 구성 방법의 IAppBuilder 개체에 추가 된 순서에 따라 파이프라인을 작성 합니다. 다음 예제에서는 LoggerMiddleware 최종적으로 이러한 요청 처리 방법에 관계 없이 파이프라인을 통해 이동 하는 모든 요청 처리할 수 있습니다. 이렇게 하면 미들웨어 구성 요소 (예: 인증 구성 요소) 여러 구성 요소 및 프레임 워크 (예: ASP.NET Web API, SignalR에 및 정적 파일 서버)를 포함 하는 파이프라인에 대 한 요청을 처리할 수 있는 강력한 시나리오.
 
## <a name="applications"></a>응용 프로그램

이전 예제에서 볼 수 있듯이, OWIN 및 Katana 프로젝트 하지 생각해 야 새로운 응용 프로그램 프로그래밍 모델 않고 응용 프로그램 프로그래밍 모델 및 프레임 워크 서버와 호스팅 인프라에서 분리 하는 추상화로 대신 합니다. 예를 들어 Web API 응용 프로그램을 빌드하는 경우 개발자 프레임 워크 Katana 프로젝트에서 구성 요소를 사용 하 여 OWIN 파이프라인에는 응용 프로그램이 실행 되는 여부에 관계 없이 ASP.NET Web API 프레임 워크를 사용 하려면 계속 됩니다. OWIN 관련 코드 응용 프로그램 개발자에 게 표시 될 위치 한곳 개발자 OWIN 파이프라인을 구성 응용 프로그램 시작 코드에 게 됩니다. 개발자는 시작 코드에 일련의 UseXx 문에서 들어오는 요청을 처리 하는 각 미들웨어 구성 요소에 대 한 일반적으로 등록 됩니다. 이 환경은 현재 System.Web 세계에서 HTTP 모듈을 등록 하는 것과 같습니다를 갖습니다. 일반적으로 더 큰 프레임 워크와 같은 미들웨어 ASP.NET 웹 API 또는 [SignalR](../../../signalr/index.md) 파이프라인 끝에 등록 됩니다. 인증 하거나 캐싱 등 교차 편집 미들웨어 구성 요소, 일반적으로 파이프라인의 시작 부분 쪽으로 등록 되 고 모든 프레임 워크 및 파이프라인에 나중에 등록 하는 구성 요소에 대 한 요청을 처리 합니다. 이러한 분리 미들웨어 구성 요소 및 기본 인프라 구성 요소에서 서로 다른 속도에서 전체 시스템 변하지 않고 남아 있는지 확인 한 후 진화 하는 구성 요소를 수 있습니다.

## <a name="components--nuget-packages"></a>구성 요소-NuGet 패키지

많은 현재 라이브러리 및 프레임 워크와 마찬가지로 Katana 프로젝트 구성 요소는 NuGet 패키지의 집합으로 배달 됩니다. 이후 버전 2.0에 대 한 Katana 패키지 종속성 그래프의 모양은 다음과 같습니다. (에 이미지를 더 크게 보려면 클릭).

[![](an-overview-of-project-katana/_static/image6.png)](an-overview-of-project-katana/_static/image5.png)

Katana 프로젝트의 거의 모든 패키지에 따라 달라 집니다, 직접 또는 간접적으로 Owin 패키지 합니다. OWIN 사양의 섹션 4에에서 설명 된 응용 프로그램 시작 시퀀스의 구체적인 구현을 제공 하는 IAppBuilder 인터페이스를 포함 하는 패키지 임을 기억 될 수 있습니다. 또한 대부분의 패키지에 따라 다릅니다 Microsoft.Owin HTTP 요청 및 응답 작업을 위한 도우미 형식 집합을 제공 하는 합니다. 패키지의 나머지 부분에서는 호스팅 인프라 패키지 (서버 또는 호스트) 또는 미들웨어로 분류할 수 있습니다. 패키지 및 종속성 Katana 프로젝트 외부에 주황색으로 표시 됩니다.

Katana 2.0에 대 한 호스팅 인프라는 SystemWeb 및 HttpListener 기반 서버, OwinHost.exe를 사용 하 여 OWIN 응용 프로그램을 실행 하기 위한 OwinHost 패키지와 OWIN 응용 프로그램에서 자체 호스팅 Microsoft.Owin.Hosting 패키지용 모두 포함 한 사용자 지정 호스트 (예: 콘솔 응용 프로그램, Windows 서비스 등)

Katana 2.0에 대 한 미들웨어 구성 요소는에 중점을 두고 다른 인증 방법을 제공 합니다. 하나 이상의 추가 미들웨어 구성 요소 진단 시작 및 오류 페이지에 대 한 지원을 통해 제공 됩니다. OWIN를 사실상 호스팅 추상적인 개념으로 커지면 Microsoft 및 타사에서 개발 된 두 미들웨어 구성 요소의 에코 시스템 수에도 증가 합니다.

## <a name="conclusion"></a>결론

 시작에서 Katana 프로젝트 목표를 만들고 함으로써 또 다른 웹 프레임 워크에 알아보려면 개발자가 강제 적용 되지 않았습니다. 대신, 목표 가능 했던 것 보다 더 많은 선택 옵션이.NET 웹 응용 프로그램 개발자에 게 추상화를 만들려고 했습니다. 대체 가능 구성 요소 집합으로 일반적인 웹 응용 프로그램 스택의 논리적 계층을 끊음 으로써 Katana 프로젝트 전체에서 해당 구성 요소에 적합 한 모든 속도 개선 하기 위해 스택에서 구성 요소를 수 있습니다. 간단한 OWIN 추상화 주위의 모든 구성 요소를 작성 하 여 Katana 프레임 워크 및 다양 한 서로 다른 서버와 호스트 간에 이식 가능 하도록 위쪽에 작성 된 응용 프로그램을 사용 합니다. 개발자는 스택의 컨트롤에 넣어 Katana 사용 하면 개발자가 간단한 방법에 대 한 궁극적인 선택 한다고 또는 기능이 풍부한 그녀의 웹 스택 이어야 합니다.  
  

## <a name="for-more-information-about-katana"></a>Katana에 대 한 자세한 내용은

- GitHub의 Katana 프로젝트: [ https://github.com/aspnet/AspNetKatana/ ](https://github.com/aspnet/AspNetKatana/)합니다.
- 비디오: [Katana 프로젝트-ASP.NET에 대 한 OWIN](https://channel9.msdn.com/Shows/Web+Camps+TV/The-Katana-Project-OWIN-for-ASPNET), Howard Dierking 여 합니다.

## <a name="acknowledgements"></a>감사의 글

- [Rick Anderson](https://blogs.msdn.com/b/rickandy/): (twitter [ @RickAndMSFT ](http://twitter.com/RickAndMSFT) ) Rick은 microsoft Azure 및 MVC에 중점을 두기 수석 프로그래밍 기록기입니다.
- [Scott Hanselman](http://www.hanselman.com/blog/): (twitter [ @shanselman ](https://twitter.com/shanselman) )
- [Jon Galloway](https://weblogs.asp.net/jgalloway/default.aspx): (twitter [ @jongalloway ](https://twitter.com/jongalloway) )
