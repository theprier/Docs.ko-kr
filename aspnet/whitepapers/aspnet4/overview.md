---
uid: whitepapers/aspnet4/overview
title: ASP.NET 4 및 Visual Studio 2010 웹 개발 개요 | Microsoft Docs
author: rick-anderson
description: 이 문서는.net Framework 4 및 Visual Studio 2010에 포함 된 ASP.NET에 대 한 다양 한 새 기능에 대 한 개요를 제공 합니다.
ms.author: riande
ms.date: 02/10/2010
ms.assetid: d7729af4-1eda-4ff2-8b61-dbbe4fc11d10
msc.legacyurl: /whitepapers/aspnet4
msc.type: content
ms.openlocfilehash: 775286df610df9040cbf04125b1742b6befa055b
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41828668"
---
<a name="aspnet-4-and-visual-studio-2010-web-development-overview"></a>ASP.NET 4 및 Visual Studio 2010 웹 개발 개요
====================
> 이 문서는.net Framework 4 및 Visual Studio 2010에 포함 된 ASP.NET에 대 한 다양 한 새 기능에 대 한 개요를 제공 합니다.
> 
> [이 백서를 다운로드 합니다.](https://download.microsoft.com/download/7/1/A/71A105A9-89D6-4201-9CC5-AD6A3B7E2F22/ASP_NET_4_and_Visual_Studio_2010_Web_Development_Overview.pdf)


**목차**

**[Core Services](#0.2__Toc253429238 "_Toc253429238")**  
[Web.config 파일을 리팩터링](#0.2__Toc253429239 "_Toc253429239")  
[확장 가능한 출력 캐싱](#0.2__Toc253429240 "_Toc253429240")  
[웹 응용 프로그램을 자동으로 시작 합니다.](#0.2__Toc253429241 "_Toc253429241")  
[페이지를 영구적으로 리디렉션](#0.2__Toc253429242 "_Toc253429242")  
[세션 상태를 축소](#0.2__Toc253429243 "_Toc253429243")  
[허용 되는 Url의 범위를 확장](#0.2__Toc253429244 "_Toc253429244")  
[확장 가능한 요청 유효성 검사](#0.2__Toc253429245 "_Toc253429245")  
[개체 캐싱 및 캐싱 확장성 개체](#0.2__Toc253429246 "_Toc253429246")  
[확장 가능한 HTML, URL 및 HTTP 헤더 인코딩을](#0.2__Toc253429247 "_Toc253429247")  
[단일 작업자 프로세스에서 개별 응용 프로그램 성능 모니터링](#0.2__Toc253429248 "_Toc253429248")  
[멀티 타기 팅](#0.2__Toc253429249 "_Toc253429249")

**[Ajax](#0.2__Toc253429250 "_Toc253429250")**  
[Web Forms 및 MVC를 사용 하 여 포함 된 jQuery](#0.2__Toc253429251 "_Toc253429251")  
[콘텐츠 배달 네트워크 지원](#0.2__Toc253429252 "_Toc253429252")  
[명시적 스크립트 ScriptManager](#0.2__Toc253429253 "_Toc253429253")

**[Web Forms](#0.2__Toc253429256 "_Toc253429256")**  
[Page.MetaKeywords 및 Page.MetaDescription 속성을 사용 하 여 메타 태그를 설정](#0.2__Toc253429257 "_Toc253429257")  
[개별 컨트롤의 뷰 상태를 사용 하도록 설정](#0.2__Toc253429258 "_Toc253429258")  
[브라우저 기능 변경 내용](#0.2__Toc253429259 "_Toc253429259")  
[ASP.NET 4에서에서 라우팅](#0.2__Toc253429260 "_Toc253429260")  
[클라이언트 Id를 설정한](#0.2__Toc253429261 "_Toc253429261")  
[데이터 컨트롤에서 행 선택 보관](#0.2__Toc253429262 "_Toc253429262")  
[ASP.NET 차트 컨트롤](#0.2__Toc253429263 "_Toc253429263")  
[QueryExtender 컨트롤을 사용 하 여 데이터 필터링](#0.2__Toc253429264 "_Toc253429264")  
[Html 인코딩된 코드 식을](#0.2__Toc253429265 "_Toc253429265")  
[프로젝트 템플릿 변경](#0.2__Toc253429266 "_Toc253429266")  
[CSS 개선](#0.2__Toc253429267 "_Toc253429267")  
[Div 숨겨진 필드 주위 요소 숨기기](#0.2__Toc253429268 "_Toc253429268")  
[템플릿 기반 컨트롤에 대 한 외부 테이블을 렌더링](#0.2__Toc253429269 "_Toc253429269")  
[향상 된 ListView 컨트롤](#0.2__Toc253429270 "_Toc253429270")  
[CheckBoxList 및 RadioButtonList 컨트롤 향상](#0.2__Toc253429271 "_Toc253429271")  
[메뉴 컨트롤 개선](#0.2__Toc253429272 "_Toc253429272")  
[마법사 및 CreateUserWizard 컨트롤 56](#0.2__Toc253429273 "_Toc253429273")

**[ASP.NET MVC](#0.2__Toc253429274 "_Toc253429274")**  
[영역 지원을](#0.2__Toc253429275 "_Toc253429275")  
[데이터 주석 특성 유효성 검사 지원을](#0.2__Toc253429276 "_Toc253429276")  
[템플릿 기반 도우미](#0.2__Toc253429277 "_Toc253429277")

**[Dynamic Data](#0.2__Toc253429278 "_Toc253429278")**  
[기존 프로젝트에 대 한 동적 데이터를 사용 하도록 설정](#0.2__Toc253429279 "_Toc253429279")  
[DynamicDataManager 컨트롤 선언 구문](#0.2__Toc253429280 "_Toc253429280")  
[엔터티 템플릿이](#0.2__Toc253429281 "_Toc253429281")  
[Url 및 전자 메일 주소에 대 한 새 필드 템플릿을](#0.2__Toc253429282 "_Toc253429282")  
[DynamicHyperLink 컨트롤을 사용 하 여 링크를 만드는](#0.2__Toc253429283 "_Toc253429283")  
[데이터 모델의 상속에 대 한 지원을](#0.2__Toc253429284 "_Toc253429284")  
[다 대 다 관계 (Entity Framework에만 해당)에 대 한 지원을](#0.2__Toc253429285 "_Toc253429285")  
[컨트롤 표시 및 지원 열거형에 새 특성](#0.2__Toc253429286 "_Toc253429286")  
[필터에 대 한 지원이 향상 되었습니다](#0.2__Toc253429287 "_Toc253429287")

**[Visual Studio 2010 웹 개발 개선](#0.2__Toc253429288 "_Toc253429288")**  
[CSS 호환성 향상](#0.2__Toc253429289 "_Toc253429289")  
[HTML 및 JavaScript 조각](#0.2__Toc253429290 "_Toc253429290")  
[JavaScript IntelliSense 향상](#0.2__Toc253429291 "_Toc253429291")

**[Visual Studio 2010을 사용 하 여 응용 프로그램 배포 웹](#0.2__Toc253429292 "_Toc253429292")**  
[웹 패키징](#0.2__Toc253429293 "_Toc253429293")  
[Web.config 변환](#0.2__Toc253429294 "_Toc253429294")  
[데이터베이스 배포](#0.2__Toc253429295 "_Toc253429295")  
[웹 응용 프로그램에 대 한 One-click 게시](#0.2__Toc253429296 "_Toc253429296")  
[Resources](#0.2__Toc253429297 "_Toc253429297")

**[Disclaimer](#0.2__Toc253429298 "_Toc253429298")**

<a id="0.2__Toc224729018"></a><a id="0.2__Toc253429238"></a><a id="0.2__Toc243304612"></a>

## <a name="core-services"></a>핵심 서비스

ASP.NET 4에는 다양을 한 출력 캐싱 및 세션 상태 저장소와 같은 핵심 ASP.NET 서비스를 개선 하는 기능이 도입 되었습니다.

<a id="0.2__Toc243304613"></a><a id="0.2__Toc253429239"></a><a id="0.2__Toc224729019"></a>

### <a name="webconfig-file-refactoring"></a>리팩터링 하는 Web.config 파일

`Web.config` 웹 응용 프로그램의 규모가 상당히 지난 몇 가지 릴리스의.NET Framework를 통해 새 기능이 추가 되었습니다, Ajax와 같은 때에 대 한 구성이 포함 된 파일, 라우팅 및 IIS 7과 통합 합니다. 구성에 Visual Studio와 같은 도구 없이 새 웹 응용 프로그램을 시작 하기가 어려웠습니다에이 있습니다. 이.NET Framework 4의 주요 구성 요소를 이동 되었습니다는 `machine.config` 파일 및 응용 프로그램을 이제 이러한 설정을 상속 합니다. 따라서는 `Web.config` 비워 또는 Visual Studio에 대 한 응용 프로그램을 대상으로 하는 프레임 워크의 버전을 지정 하는 다음 줄만 포함 하도록 ASP.NET 4 응용 프로그램에서 파일:

[!code-xml[Main](overview/samples/sample1.xml)]

<a id="0.2__Toc253429240"></a><a id="0.2__Toc243304614"></a>

### <a name="extensible-output-caching"></a>확장 가능한 출력 캐싱

ASP.NET 1.0 출시 된 이후로 출력 캐싱을 개발자가 메모리에서 페이지, 컨트롤 및 HTTP 응답의 생성된 된 출력을 저장할 수 있게 되었습니다. 후속 웹 요청에 대해 ASP.NET 수 콘텐츠를 제공 보다 신속 하 게부터 출력을 다시 생성 하지 않고 메모리에서 생성된 된 출력을 검색 하 여 합니다. 그러나이 방법은 제한이-생성 되는 콘텐츠는 항상 메모리에 저장 해야 하 고 출력 캐싱을 사용 된 메모리 사용량이 발생 하는 서버에서 웹 응용 프로그램의 다른 부분에서 메모리 요구량을 사용 하 여 경쟁할 수 있습니다.

ASP.NET 4에는 하나 이상의 사용자 지정 출력 캐시 공급자를 구성할 수 있도록 출력 캐싱에 확장성 지점을 추가 합니다. 출력 캐시 공급자 모든 저장소 메커니즘을 사용 하 여 HTML 콘텐츠를 유지할 수 있습니다. 이 수 로컬 또는 원격 디스크를 포함 하는 다양 한 지 속성 메커니즘, 클라우드 저장소에 대 한 사용자 지정 출력 캐시 공급자를 만들 수 있도록 하 고 캐시 엔진을 배포 합니다.

새에서 파생 된 클래스로 사용자 지정 출력 캐시 공급자를 만들면 *System.Web.Caching.OutputCacheProvider* 형식입니다. 공급자를 구성할 수 있습니다는 `Web.config` 새을 사용 하 여 파일 *공급자* 하위 섹션은 *outputCache* 요소를 다음 예제에서와 같이:

[!code-xml[Main](overview/samples/sample2.xml)]

ASP.NET 4에서 모든 HTTP 응답에는 기본적으로 렌더링 된 페이지 및 컨트롤 앞의 예에서 같이 메모리에 출력 캐시를 사용 하 여 위치를 *defaultProvider* 특성 AspNetInternalProvider로 설정 됩니다. 다른 공급자 이름을 지정 하 여 웹 응용 프로그램에 대 한 사용 하는 기본 출력 캐시 공급자를 변경할 수 있습니다 *defaultProvider*합니다.

또한 컨트롤 및 요청에 따라 다양 한 출력 캐시 공급자를 선택할 수 있습니다. 다른 웹 사용자 컨트롤에 대 한 다양 한 출력 캐시 공급자를 선택 하는 가장 쉬운 방법은 new를 사용 하 여 선언적으로 작업을 수행 하는 것 *providerName* 제어 지시문을 다음 예제에서와 같이 특성:

[!code-aspx[Main](overview/samples/sample3.aspx)]

HTTP 요청에 대 한 다양 한 출력 캐시 공급자를 지정 하는 좀 더 많은 작업이 필요 합니다. 새 재정의 공급자를 선언적으로 지정 하는 대신 *GetOuputCacheProviderName* 에서 메서드를 `Global.asax` 파일을 프로그래밍 방식으로 특정 요청에 사용할 공급자를 지정 합니다. 다음 예제에서는 이 작업을 수행하는 방법을 보여 줍니다.

[!code-csharp[Main](overview/samples/sample4.cs)]

ASP.NET 4에 출력 캐시 공급자 확장을 추가 하 여 지금 웹 사이트에 대 한 더욱 강력 하 고 더 지능적인 출력 캐싱 전략을 추진할 수 있는 합니다. 예를 들어, 페이지를 디스크에 낮은 트래픽을 받는 캐시 하는 동안 메모리에서 사이트의 "상위 10 개의" 페이지를 캐시할 수 되었습니다. 또는 모든에서 다를 조합, 렌더링된 된 페이지에 대 한 캐시 수 있지만 메모리 사용량은 프런트 엔드 웹 서버에서 오프 로드 된 있도록 분산된 캐시를 사용 합니다.

<a id="0.2__Toc224729020"></a><a id="0.2__Toc253429241"></a><a id="0.2__Toc243304615"></a>

### <a name="auto-start-web-applications"></a>웹 응용 프로그램을 자동으로 시작 합니다.

일부 웹 응용 프로그램은 많은 양의 데이터를 로드 하거나 첫 번째 요청을 처리 하기 전에 처리 하는 비용이 많이 드는 초기화를 수행 해야 합니다. "절전" ASP.NET 응용 프로그램 및 다음 중 초기화 코드를 실행 하는 사용자 지정 방법으로 고안 했습니다 이러한 상황에 대 한 ASP.NET의 이전 버전에서의 *응용 프로그램\_부하* 의 메서드를 `Global.asax` 파일입니다.

라는 새로운 확장성 기능 *자동 시작* 직접 주소가이 시나리오는 사용 가능한 경우 ASP.NET 4에서 실행 되도록 Windows Server 2008 R2에서 IIS 7.5입니다. 자동 시작 기능에는 응용 프로그램 풀을 시작, ASP.NET 응용 프로그램을 초기화 한 다음 HTTP 요청을 받아들이기 위한 제어 되는 방법을 제공 합니다.

> [!NOTE] 
> 
> IIS 7.5 용 IIS 응용 프로그램 준비 모듈
> 
> IIS 팀 IIS 7.5 용 응용 프로그램 준비 모듈의 첫 번째 베타 테스트 버전을 출시 했습니다. 이렇게 하면 앞에서 설명한 것 보다 쉽게 응용 프로그램을 준비 합니다. 사용자 지정 코드를 작성 하는 대신 웹 응용 프로그램 네트워크의 요청을 수락 하기 전에 실행 리소스의 Url에 지정할 수 있습니다. IIS 서비스의 시작 하는 동안 발생이 준비 (IIS 응용 프로그램 풀을 구성 하는 경우 *AlwaysRunning*) 하 고 IIS 작업자 프로세스를 재활용 하는 경우. 이전 IIS 작업자 프로세스 재활용, 하는 동안 응용 프로그램 환경을 방해 하지 또는 다른 문제로 인해 unprimed 캐시를 새로 생성 된 작업자 프로세스를 완벽 하 게 준비 될 때까지 요청을 실행 계속 합니다. 이 모듈 버전 2.0부터 ASP.NET의 모든 버전을 사용 하 여 작동 하는 참고 합니다.
> 
> 자세한 내용은 [응용 프로그램 웜 업을](https://www.iis.net/extensions/applicationwarmup%20on%20the%20IIS.net) IIS.net 웹 사이트입니다. 준비 기능을 사용 하는 방법을 보여 주는 연습을 참조 하세요 [Getting Started with IIS 7.5 응용 프로그램 준비 모듈](https://www.iis.net/learn/manage) IIS.net 웹 사이트입니다.


자동 시작 기능을 사용 하려면 IIS 관리자에서 다음 구성을 사용 하 여 자동으로 시작 되도록 IIS 7.5에서 응용 프로그램 풀을 설정 합니다 `applicationHost.config` 파일:

[!code-xml[Main](overview/samples/sample5.xml)]

개별 응용 프로그램에서 다음 구성을 사용 하 여 자동으로 시작 되도록 지정 하는 단일 응용 프로그램 풀에서 여러 응용 프로그램을 포함할 수 있으므로 `applicationHost.config` 파일:

[!code-xml[Main](overview/samples/sample6.xml)]

IIS 7.5에서 정보를 사용 하는 경우 IIS 7.5 server가 콜드 시작 또는 개별 응용 프로그램 풀 재활용 될 때를 `applicationHost.config` 파일을 자동으로 시작 하는 웹 응용 프로그램 요구를 확인 합니다. IIS7.5 자동 시작 되도록 표시 된 각 응용 프로그램에 대 한 HTTP 요청 하는 동안 응용 프로그램이 일시적으로 받아들이지 않는 상태의 응용 프로그램을 시작 하려면 ASP.NET 4로 요청을 보냅니다. ASP.NET에서 정의 된 형식을 인스턴스화하이 상태의 경우 합니다 *serviceAutoStartProvider* (이전 예제에 표시) 된 특성 및 해당 공용 진입점으로 호출 합니다.

구현 하 여 필요한 진입점을 사용 하 여 관리 되는 자동으로 시작 형식을 만들 합니다 *IProcessHostPreloadClient* 다음 예제에서와 같이 인터페이스:

[!code-csharp[Main](overview/samples/sample7.cs)]

초기화 후 코드에서 실행 합니다 *미리 로드* 메서드 및 메서드는 반환 ASP.NET 응용 프로그램 요청을 처리할 준비가 되었습니다.

.5 IIS 및 ASP.NET 4 자동 시작을 추가 하 여 이제 첫 번째 HTTP 요청을 처리 하기 전에 비용이 많이 드는 응용 프로그램 초기화를 수행 하기 위한 잘 정의 된 방법입니다. 예를 들어, 응용 프로그램을 초기화 하 고 응용 프로그램 초기화 되었고 HTTP 트래픽을 허용 하도록 준비 하는 부하 분산 장치를 다음 신호를 새 자동 시작 기능을 사용할 수 있습니다.

<a id="0.2__Toc224729021"></a><a id="0.2__Toc253429242"></a><a id="0.2__Toc243304616"></a>

### <a name="permanently-redirecting-a-page"></a>페이지를 영구적으로 리디렉션

일반적으로 웹 응용 프로그램 페이지 및 관련 기타 콘텐츠 검색 엔진에서 오래 된 링크의 누적을 야기할 수 있는 시간이 지남에 따라 이동할 것입니다. ASP.NET에서 개발자가 일반적으로 요청 이전 Url 사용 하 여 처리를 사용 하 여 합니다 *Response.Redirect* 새 URL로 요청을 전달 하는 방법입니다. 그러나 합니다 *리디렉션* 메서드는 사용자가 이전 Url에 액세스 하려고 하면 왕복 추가 http 결과 HTTP 302 있음 (임시 리디렉션) 응답을 발급 합니다.

ASP.NET 4를 새로 추가 *RedirectPermanent* 문제 HTTP 301 쉽게 하는 도우미 메서드는 다음 예제와 같이 응답을 영구적으로 이동 합니다.

[!code-csharp[Main](overview/samples/sample8.cs)]

검색 엔진 및 영구 리디렉션을 인식 하는 다른 사용자 에이전트는 임시 리디렉션에 대 한 브라우저에서 불필요 한 왕복을 제거 하는 콘텐츠를 사용 하 여 연결 된 새 URL을 저장 합니다.

<a id="0.2__Toc224729022"></a><a id="0.2__Toc253429243"></a><a id="0.2__Toc243304617"></a>

### <a name="shrinking-session-state"></a>세션 상태를 축소합니다.

ASP.NET은 웹 팜에서 세션 상태를 저장 하기 위한 두 가지 기본 옵션을 제공 합니다.-out-of-process 세션 상태 서버를 사용 하는 호출 하는 세션 상태 공급자 및 Microsoft SQL Server 데이터베이스에 데이터를 저장 하는 세션 상태 공급자입니다. 두 옵션 모두 웹 응용 프로그램의 작업자 프로세스 외부 상태 정보가 저장 되므로, 세션 상태를 원격 저장소로 전송 되기 전에 직렬화 해야 합니다. 세션 상태에 저장 되는 얼 만큼의 정보에 따라 serialize 된 데이터의 크기가 상당히 커질 수 있습니다.

ASP.NET 4-out-of-process 세션 상태 공급자의 두 종류에 대 한 새 압축 옵션을 소개합니다. 경우는 *compressionEnabled* 다음 예제와 같이 하는 구성 옵션이 설정 된 *true*, ASP.NET은 압축 (및 압축 풀기).NET Framework 를사용하여serialize된세션상태 *System.IO.Compression.GZipStream* 클래스입니다.

[!code-xml[Main](overview/samples/sample9.xml)]

새 특성의 단순한 더하기를 사용 하 여는 `Web.config` 파일을 웹 서버의 예비 CPU 주기를 사용 하 여 응용 프로그램에는 serialize 된 세션 상태 데이터의 크기를 상당히 줄이는 실현할 수 있습니다.

<a id="0.2__Toc253429244"></a><a id="0.2__Toc243304618"></a>

### <a name="expanding-the-range-of-allowable-urls"></a>허용 되는 Url의 범위를 확장합니다.

ASP.NET 4 응용 프로그램 Url의 크기를 확장 하는 것에 대 한 새 옵션을 소개 합니다. 이전 버전의 ASP.NET URL 경로 길이가 260 자, NTFS 파일 경로 제한에 따라 제한 됩니다. ASP.NET 4에는 옵션이 있습니다 (늘리거나 줄이려면)이이 제한을 응용 프로그램에 대해 적절 하 게 사용 하 여 두 개의 새 *httpRuntime* 구성 특성입니다. 다음 예제에서는 이러한 새 특성을 보여 줍니다.

[!code-xml[Main](overview/samples/sample10.xml)]

더 길거나 더 짧은 경로 (프로토콜, 서버 이름 및 쿼리 문자열을 포함 하지 않는 URL의 일부)를 허용 하려면 수정 된 *[maxUrlLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxurllength.aspx)* 특성입니다. 길거나 짧은 쿼리 문자열을 허용 하려면 값을 수정 합니다 *[maxQueryStringLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxquerystringlength.aspx)* 특성입니다.

ASP.NET 4에서는 URL 문자 검사에 사용 되는 문자를 구성할 수도 있습니다. ASP.NET URL의 경로 부분에 잘못 된 문자가 찾으면 요청을 거부 하 고 HTTP 400 오류가 발생 합니다. 이전 버전의 ASP.NET에서 URL 문자 검사 고정된 된 문자 집합으로 제한 되었습니다. ASP.NET 4에서 사용 하 여 새 유효한 문자 집합이 사용자 지정할 수 있습니다 *requestPathInvalidChars* 특성을 *httpRuntime* 다음 예제에서와 같이 구성 요소:

[!code-xml[Main](overview/samples/sample11.xml)]

기본적으로 <em>requestPathInvalidChars</em> 특성은 잘못 된 것으로 8 개의 문자를 정의 합니다. (에 할당 되는 문자열에 <em>requestPathInvalidChars</em> 기본적으로<em>를</em>는 보다 작은 (&lt;), 보다 큼 (&gt;), 및 앰퍼샌드 (&amp;) 문자는 인코딩 되는 `Web.config` 파일은 XML 파일입니다.) 필요에 따라 잘못 된 문자 집합을 사용자 지정할 수 있습니다.

> [!NOTE]
> ASP.NET 4는 항상 문자 (0x00-0x1f, ASCII 범위에 포함 된 URL 경로 거부 IETF의 RFC 2396에 정의 된 대로 잘못 된 URL 문자는 참고 ([http://www.ietf.org/rfc/rfc2396.txt](http://www.ietf.org/rfc/rfc2396.txt)). IIS 6을 실행 하는 버전의 Windows Server에서 또는 이상, http.sys 프로토콜 장치 드라이버를 자동으로 거부 Url 이러한 문자를 사용 하 여 합니다.


<a id="0.2__Toc253429245"></a><a id="0.2__Toc243304619"></a>

### <a name="extensible-request-validation"></a>확장 가능한 요청 유효성 검사

ASP.NET 요청 유효성 검사는 사이트 간 스크립팅 (XSS) 공격에 자주 사용 되는 문자열에 대 한 들어오는 HTTP 요청 데이터를 검색 합니다. 잠재적인 XSS 문자열이 발견 되 면 요청 유효성 검사는 주의 대상 문자열에 플래그를 지정 하 고 오류를 반환 합니다. XSS 공격에 사용 되는 가장 일반적인 문자열을 발견 하는 경우에 기본 제공 요청 유효성 검사 오류를 반환 합니다. 너무 많은 가양성 XSS 유효성 검사를 더 적극적으로 확인 하는 이전 하려고 했습니다. 그러나 고객은 특정 페이지 또는 특정 유형의 요청에 대 한 더 공격적으로 또는 반대로 할 의도적으로 XSS를 완화 하는 요청 유효성 검사 좋습니다.

ASP.NET 4에서 요청 유효성 검사 기능 내용이 확장할 수 있는 사용자 지정 요청 유효성 검사 논리를 사용할 수 있도록 합니다. 새에서 파생 되는 클래스를 만들면 요청 유효성 검사를 확장 하려면 *System.Web.Util.RequestValidator* 유형 및 수에 응용 프로그램 구성 (에 *httpRuntime* 섹션의 `Web.config`파일) 사용자 지정 형식을 사용 합니다. 다음 예제에서는 사용자 지정 요청 유효성 검사 클래스를 구성 하는 방법을 보여 줍니다.

[!code-xml[Main](overview/samples/sample12.xml)]

새 *requestValidationType* 특성 사용자 지정 요청 유효성 검사를 제공 하는 클래스를 지정 하는 표준.NET Framework 형식 식별자 문자열이 필요 합니다. 각 요청에 대 한 ASP.NET 들어오는 HTTP 요청 데이터의 각 부분을 처리 하는 데 사용자 지정 형식을 호출 합니다. 들어오는 URL, (쿠키 및 사용자 지정 헤더), 모든 HTTP 헤더 및 엔터티 본문을 다음 예와에서 같이 사용자 지정 요청 유효성 검사 클래스에 대 한 사용 가능한 모든 같습니다.

[!code-csharp[Main](overview/samples/sample13.cs)]

여기서 하지 않으려는 경우 들어오는 HTTP 데이터를 검사 하는 경우 요청 유효성 검사 클래스 대체할 수 ASP.NET 기본 요청 유효성 검사 호출 하 여 실행할 수 있도록 *기본입니다. IsValidRequestString 합니다.*

<a id="0.2__Toc253429246"></a><a id="0.2__Toc243304620"></a>

### <a name="object-caching-and-object-caching-extensibility"></a>개체 캐싱 및 캐싱 확장성 개체

ASP.NET는 강력한 메모리 내 개체 캐시를 포함 하는 데 해당 첫 번째 릴리스 이후 (*System.Web.Caching.Cache*). 캐시 구현이 비 웹 응용 프로그램에서 사용 된는 자주 사용 되었습니다. 그러나이 작업은 까다롭습니다에 대 한 참조를 포함 하는 Windows Forms 또는 WPF 응용 프로그램에 대 한 `System.Web.dll` 를 ASP.NET 개체 캐시를 사용할 수 있습니다.

캐싱을 사용할 수 있도록 모든 응용 프로그램,.NET Framework 4에서는 새 어셈블리, 새 네임 스페이스, 몇 가지 기본 형식 및 구체적인 구현 캐싱를 소개 합니다. 새 `System.Runtime.Caching.dll` 어셈블리에는 새 캐싱 API를 포함 합니다 *System.Runtime.Caching* 네임 스페이스입니다. 클래스의 두 가지 핵심 집합을 포함 하는 네임 스페이스:

- 모든 유형의 사용자 지정 캐시 구현 작성 하기 위한 기초를 제공 하는 추상 형식입니다.
- 구체적인 메모리 내 개체 캐시 구현 (합니다 *System.Runtime.Caching.MemoryCache* 클래스).

새 *MemoryCache* ASP.NET cache 클래스와 비슷하게 모델링 됩니다 및 ASP.NET을 사용 하 여 내부 캐시 엔진 논리의 대부분을 공유 합니다. 하지만의 캐싱 Api를 공개 *System.Runtime.Caching* ASP.NET을 사용한 경우, 사용자 지정 캐시 개발을 지원 하도록 업데이트 되었습니다 *캐시* 개체의 친숙 한 개념을 찾을 수 있습니다는 새 Api입니다.

자세한 내용은 새 *MemoryCache* 클래스 및 기본 Api를 지 원하는 전체 문서를 기준으로 해야 합니다. 그러나 다음 예제에서는 사용 하면 새 캐시 API의 작동 방식을 파악 합니다. 예제에 대 한 종속성 없이 Windows Forms 응용 프로그램에 대 한 기록 된 `System.Web.dll`합니다.

[!code-csharp[Main](overview/samples/sample14.cs)]

<a id="0.2__Toc253429247"></a><a id="0.2__Toc243304621"></a>

### <a name="extensible-html-url-and-http-header-encoding"></a>확장 가능한 HTML, URL 및 HTTP 헤더 인코딩

ASP.NET 4에서는 다음 일반 텍스트 인코딩 작업에 대 한 사용자 지정 인코딩 루틴을 만들 수 있습니다.

- HTML 인코딩입니다.
- URL 인코딩입니다.
- HTML 특성 인코딩입니다.
- 아웃 바운드 HTTP 헤더를 인코딩입니다.

새에서 파생 하 여 사용자 지정 인코더를 만들 수 있습니다 *System.Web.Util.HttpEncoder* 형식 및 다음 ASP.NET 구성에서 사용자 지정 형식을 사용 하는 *httpRuntime* 섹션을 `Web.config` 파일인으로 다음 예제와 같이:

[!code-xml[Main](overview/samples/sample15.xml)]

사용자 지정 인코더를 구성한 후 ASP.NET 사용자 지정 인코딩 구현을 인코딩 방법의 공용 때마다를 자동으로 호출 합니다 *System.Web.HttpUtility* 또는 *System.Web.HttpServerUtility* 클래스 라고 합니다. 그러면 웹 개발 팀의 나머지 부분 공용 ASP.NET 인코딩 Api를 사용 하는 동안 적극적으로 문자 인코딩을 구현 하는 사용자 지정 인코더를 만드는 웹 개발 팀의 한 부분입니다. 중앙에서 사용자 지정 인코더를 구성 하 여 합니다 *httpRuntime* 요소인 보장 됩니다 인코딩 Api 공개 ASP.NET의 모든 텍스트 인코딩 호출은 사용자 지정 인코더를 통해 라우팅될 수 있도록 합니다.

<a id="0.2__Toc253429248"></a><a id="0.2__Toc243304622"></a>

### <a name="performance-monitoring-for-individual-applications-in-a-single-worker-process"></a>단일 작업자 프로세스에서 개별 응용 프로그램 성능 모니터링

단일 서버에서 호스팅될 수 있는 웹 사이트의 수를 증가 시키기 위해 여러 호스팅 서비스 공급자는 단일 작업자 프로세스에서 여러 ASP.NET 응용 프로그램을 실행 합니다. 그러나 여러 응용 프로그램에 단일 공유 작업자 프로세스를 사용 하는 경우 어렵습니다 문제가 발생 하는 개별 응용 프로그램을 식별 하는 서버 관리자에 대 한 합니다.

ASP.NET 4는 CLR에 의해 도입 된 새 리소스 모니터링 기능을 활용 합니다. 이 기능을 사용 하려면 다음 XML 구성 코드 조각을 추가할 수 있습니다는 `aspnet.config` 구성 파일입니다.

[!code-xml[Main](overview/samples/sample16.xml)]

> [!NOTE]
> 참고는 `aspnet.config` 파일은.NET Framework를 설치한 디렉터리입니다. 있지는 `Web.config` 파일입니다.


경우는 *appDomainResourceMonitoring* 기능이 설정 된, "ASP.NET 응용 프로그램" 성능 범주에서 사용할 수 있는 두 개의 새 성능 카운터: *관리 되는 프로세서 시간 백분율* 및  *관리 되는 메모리 사용*합니다. 이러한 성능 카운터 모두 예상된 CPU 시간 및 개별 ASP.NET 응용 프로그램의 관리 되는 메모리 사용률을 추적 하려면 새 CLR 응용 프로그램 도메인 리소스 관리 기능을 사용 합니다. 따라서 ASP.NET 4를 사용 하 여 관리자가 이제 단일 작업자 프로세스에서 실행 하는 개별 응용 프로그램의 리소스 소비에 더욱 세부적인 보기를 있습니다.

<a id="0.2__Toc253429249"></a><a id="0.2__Toc243304623"></a>

### <a name="multi-targeting"></a>멀티 타기팅

.NET Framework의 특정 버전을 대상으로 하는 응용 프로그램을 만들 수 있습니다. ASP.NET 4에서 새 특성에는 *컴파일* 의 요소는 `Web.config` 파일을 사용 하면.NET Framework 4 이상을 대상으로 합니다. .NET Framework 4를 명시적으로 대상 및에서 선택적 요소를 포함 하는 경우는 `Web.config` 파일에 대 한 항목 예: *system.codedom*, 이러한 요소는.NET Framework 4에 대 한 올바른 이어야 합니다. (명시적으로 대상으로 하지는.NET Framework 4를 대상 프레임 워크에 있는 항목의 부재에서 유추 됩니다는 `Web.config` 파일입니다.)

다음 예제에서는 사용을 보여 줍니다.는 *targetFramework* 특성을 *컴파일* 요소의 `Web.config` 파일입니다.

[!code-xml[Main](overview/samples/sample17.xml)]

.NET Framework의 특정 버전을 대상으로 하는 방법에 대 한 다음 note:

- .NET Framework 4 응용 프로그램 풀을 ASP.NET 빌드 시스템 가정.NET Framework 4를 대상으로 하는 경우는 `Web.config` 파일에 포함 되지 않습니다 합니다 *targetFramework* 특성 또는 경우에는 `Web.config` 파일이 없습니다. (해야.NET Framework 4 하에서 실행 되도록 응용 프로그램에 대 한 코딩 변경 합니다.)
- 포함 하는 경우를 *targetFramework* 특성인 경우에 *system.codeDom* 요소에 정의 된를 `Web.config` 파일이이 파일은.NET Framework 4에 대 한 올바른 항목을 포함 해야 합니다.
- 사용 중인 경우는 *aspnet\_컴파일러* 응용 프로그램 (예: 빌드 환경)를 미리 컴파일할 명령에 올바른 버전을 사용 해야 합니다 *aspnet\_컴파일러* 대상 프레임 워크에 대 한 명령입니다. .NET Framework 3.5 및 이전 버전에 대해 컴파일하 (%WINDIR%\Microsoft.NET\Framework\v2.0.50727)는.NET Framework 2.0을 사용 하 여 제공 되는 컴파일러를 사용 합니다. .NET Framework 4를 사용 하 여 만든 응용 프로그램 프레임 워크를 사용 하 여 또는 이상 버전을 사용 하 여 컴파일하는 데 함께 제공 되는 컴파일러를 사용 합니다.
- 런타임 시 컴파일러는 컴퓨터에 설치 된 최신 프레임 워크 어셈블리를 사용 (및 따라서 GAC에). 업데이트 하려고 하면 나중에 프레임 워크 (예를 들어 가상 버전 4.1이 설치 되어)에 프레임 워크의 최신 버전의 기능을 사용 하는 일을 할 수 있습니다는 *targetFramework* 더 낮은 버전을 대상으로 하는 특성 (4.0)로 설정과 같은 합니다. 그러나 (Visual Studio 2010 또는 사용 하는 경우 디자인 타임 합니다 *aspnet\_컴파일러* 명령, 프레임 워크의 최신 기능을 사용 하면 컴파일러 오류).

<a id="0.2__Toc224729023"></a><a id="0.2__Toc253429250"></a><a id="0.2__Toc243304624"></a>

## <a name="ajax"></a>Ajax

<a id="0.2__Toc253429251"></a><a id="0.2__Toc243304625"></a>

### <a name="jquery-included-with-web-forms-and-mvc"></a>Web Forms 및 MVC를 사용 하 여 포함 된 jQuery

Web Forms 및 MVC 용 Visual Studio 템플릿에 오픈 소스 jQuery 라이브러리를 포함합니다. 새 웹 사이트 또는 프로젝트를 만든 경우 다음 3 개의 파일이 포함 된 스크립트 폴더를 만듭니다.

- jQuery-1.4.1.js –는 사용자가 읽을 축소 되지 않은 jQuery 라이브러리의 버전입니다.
- jQuery-14.1.min.js – jQuery 라이브러리의 축소 된 버전입니다.
- jQuery-1.4.1-vsdoc.js – jQuery 라이브러리에 대 한 Intellisense 설명서 파일입니다.

응용 프로그램을 개발 하는 동안 jQuery의 축소 되지 않은 버전을 포함 합니다. 프로덕션 응용 프로그램에는 jQuery의 축소 된 버전을 포함 합니다.

예를 들어, Web Forms 페이지는 jQuery를 사용 하 여 포커스를가지고 있을 때 노란색으로 ASP.NET TextBox 컨트롤의 배경색을 변경 하는 방법을 보여 줍니다.

[!code-aspx[Main](overview/samples/sample18.aspx)]

<a id="0.2__Toc253429252"></a><a id="0.2__Toc243304626"></a>

### <a name="content-delivery-network-support"></a>Content Delivery Network 지원

Microsoft Ajax 콘텐츠 배달 네트워크 (CDN)를 사용 하면 손쉽게 웹 응용 프로그램에 ASP.NET Ajax 및 jQuery 스크립트를 추가할 수 있습니다. JQuery 라이브러리를 사용 하 여 추가 하 여 시작할 수는 예를 들어, 한 `<script>` 같이 Ajax.microsoft.com 가리키는 페이지 태그:

[!code-html[Main](overview/samples/sample19.html)]

Microsoft Ajax CDN을 활용 하 여 Ajax 응용 프로그램의 성능을 크게 개선할 수 있습니다. Microsoft Ajax CDN의 콘텐츠는 세계에 있는 서버에 캐시 됩니다. 또한 Microsoft Ajax CDN에는 브라우저 서로 다른 도메인에 있는 웹 사이트에 대 한 캐시 된 JavaScript 파일을 다시 사용할 수 있도록 설정 합니다.

Microsoft Ajax Content Delivery Network는 Secure Sockets Layer를 사용 하 여 웹 페이지를 처리 해야 하는 경우 SSL (HTTPS)을 지원 합니다.

CDN을 사용할 수 없는 경우는 대체 (fallback)를 구현 합니다. 대체를 테스트 합니다.

Microsoft Ajax CDN에 대 한 자세한 내용은 다음 웹 사이트를 방문 합니다.

[https://www.asp.net/ajaxlibrary/CDN.ashx](../../ajax/cdn/overview.md)

ASP.NET ScriptManager는 Microsoft Ajax CDN을 지원합니다. 한 가지 속성만 설정, EnableCdn 속성 하면 CDN에서 모든 ASP.NET 프레임 워크 JavaScript 파일을 검색할 수 있습니다.

[!code-aspx[Main](overview/samples/sample20.aspx)]

EnableCdn 속성 값이 true를 설정 하면 ASP.NET framework 유효성 검사 및 UpdatePanel에 사용 되는 모든 JavaScript 파일을 포함 하 여 CDN에서 모든 ASP.NET 프레임 워크 JavaScript 파일을 검색 합니다. 이 하나의 속성을 설정할 웹 응용 프로그램의 성능에 상당한 영향을 미칠 수 있습니다.

웹 리소스의 특성을 사용 하 여 고유한 JavaScript 파일에 대 한의 CDN 경로 설정할 수 있습니다. 새 CdnPath 속성 값이 true에 EnableCdn 속성을 설정할 때 사용 하는 CDN에 대 한 경로 지정 합니다.

[!code-csharp[Main](overview/samples/sample21.cs)]

<a id="0.2__Toc253429253"></a><a id="0.2__Toc243304627"></a>

### <a name="scriptmanager-explicit-scripts"></a>ScriptManager 명시적 스크립트

이전에 ASP.NET ScriptManger 사용 하는 경우 다음 해야 전체 모놀리식 ASP.NET Ajax 라이브러리를 로드 합니다. 새 ScriptManager.AjaxFrameworkMode 속성을 활용 하 여 ASP.NET Ajax 라이브러리의 구성 요소를 로드 하는 정확 하 게 제어할 수 있으며만 해야 하는 ASP.NET Ajax 라이브러리의 구성 요소를 로드할 수 있습니다.

ScriptManager.AjaxFrameworkMode 속성은 다음 값으로 설정할 수 있습니다.

- 사용 가능--지정 ScriptManager 컨트롤에 자동으로 모든 핵심 프레임 워크 스크립트 (레거시 동작)의 결합 된 스크립트 파일인 MicrosoftAjax.js 스크립트 파일을 포함 합니다.
- 사용 하지 않도록 설정-모든 Microsoft Ajax 스크립트 기능이 사용 하지 않도록 설정 됩니다 하며는 ScriptManager 컨트롤이 참조 하지 않으면 모든 스크립트가 자동으로 지정 합니다.
- 명시적-를 명시적으로 포함 페이지에서 필요로 하는 개별 프레임 워크 핵심 스크립트 파일에 대 한 스크립트 참조 및를 포함 하는 각 스크립트 파일에 필요한 종속성에 대 한 참조를 지정 합니다.

예를 들어 명시적 값으로 AjaxFrameworkMode 속성을 설정 해야 하는 특정 ASP.NET Ajax 구성 요소 스크립트 지정할 수 있습니다.

[!code-aspx[Main](overview/samples/sample22.aspx)]

<a id="0.2__The_DataView_Control"></a><a id="0.2__The_DataContext_and"></a><a id="0.2__Refactoring_the_Microsoft"></a><a id="0.2__Toc224729032"></a><a id="0.2__Toc253429256"></a><a id="0.2__Toc243304630"></a>

## <a name="web-forms"></a>Web Forms

Web Forms에 ASP.NET의 핵심 기능은 ASP.NET 1.0 릴리스 되었습니다. 다음을 포함 하 여 ASP.NET 4에 대 한이 영역의 많은 부분이 향상 되었습니다.

- 설정 하는 기능이 *meta* 태그입니다.
- 뷰 상태를 보다 자세히 제어 합니다.
- 브라우저 기능을 사용 하 여 작업을 편리 하 게 합니다.
- ASP.NET Web Forms를 사용 하 여 라우팅을 사용 하 여 지원 합니다.
- 생성 된 Id 보다 자세히 제어 합니다.
- 데이터 컨트롤에서 선택한 행을 유지할 수 있습니다.
- 렌더링 된 HTML에서 보다 자세히 제어를 *FormView* 하 고 *ListView* 컨트롤입니다.
- 데이터 소스 컨트롤에 대 한 필터링 지원 합니다.

<a id="0.2__Toc224729033"></a><a id="0.2__Toc253429257"></a><a id="0.2__Toc243304631"></a>

### <a name="setting-meta-tags-with-the-pagemetakeywords-and-pagemetadescription-properties"></a>Page.MetaKeywords 및 Page.MetaDescription 속성을 사용 하 여 메타 태그를 설정합니다.

ASP.NET 4에서는 두 개의 속성을 추가 합니다 *페이지* 클래스 *MetaKeywords* 하 고 *MetaDescription*합니다. 이러한 두 속성에 해당 나타냅니다 *meta* 다음 예제에서와 같이 페이지의 태그:

[!code-aspx[Main](overview/samples/sample23.aspx)]

이러한 두 속성 동일 하 게 작동 방식으로 페이지의 *Title* 속성입니다. 이러한 규칙을 따릅니다.

1. 없으면 없습니다 *메타* 태그를 *헤드* 속성 이름과 일치 하는 요소 (즉, 이름을 "키워드" = *Page.MetaKeywords* 이름과 = "description" 에대한 *Page.MetaDescription*, 이러한 속성을 설정 하지 않은 즉), *meta* 태그 렌더링 될 때 페이지에 추가 됩니다.
2. 이미 있는 경우 *meta* 이러한 이름의 태그를 이러한 속성 프록시로 get 및 set 메서드는 기존 태그의 내용에 대 한 합니다.

런타임에 데이터베이스 또는 다른 원본에서 콘텐츠를 가져올 수 있습니다 하 고 설명할 수 있도록 동적으로 태그를 설정할 수 있는 이러한 속성을 설정할 수 있습니다 특정 페이지입니다.

설정할 수도 있습니다는 *키워드* 및 *설명* 속성에는 *@ Page* Web Forms 페이지 태그는 다음 예제와 같이 맨 위에 있는 지시문:

[!code-aspx[Main](overview/samples/sample24.aspx)]

이렇게 무시 되는 *메타* 태그 내용을 (있는 경우) 페이지에서 이미 선언 되었습니다.

설명의 내용을 *meta* 태그는 Google의 미리 보기를 나열 하는 검색 개선에 사용 됩니다. (세부 정보를 참조 하세요 [meta 설명 변경을 사용 하 여 조각 개선](http://googlewebmastercentral.blogspot.com/2007/09/improve-snippets-with-meta-description.html) Google 웹 마스터 중앙 블로그.) Google 및 Windows Live Search를 사용 하지 키워드의 내용에 않지만 다른 검색 엔진 수 있습니다. 자세한 내용은 [Meta 키워드 조언을](http://www.searchengineguide.com/richard-ball/meta-keywords-a.php) 검색 엔진 설명서 웹 사이트입니다.

이러한 새 속성은 간단한 기능을 하지만 고유한 만드는 코드를 작성 또는 이러한 작업을 수동으로 추가 하는 요구 사항을에서 저장 하는 *meta* 태그입니다.

<a id="0.2__Toc224729034"></a><a id="0.2__Toc253429258"></a><a id="0.2__Toc243304632"></a>

### <a name="enabling-view-state-for-individual-controls"></a>개별 컨트롤의 뷰 상태를 사용 하도록 설정

기본적으로 각 컨트롤 페이지의 응용 프로그램에 대 한 필요가 없는 경우에 잠재적으로 뷰 상태를 저장 하는 결과 사용 하 여 페이지 보기 상태 사용 합니다. 뷰 상태 데이터는 페이지를 생성 한 클라이언트에 페이지를 보내고 다시 게시 하는 데 걸리는 시간의 증가 태그에 포함 됩니다. 필요한 것 보다 자세한 뷰 상태를 저장 하면 상당한 성능 저하가 발생할 수 있습니다. ASP.NET의 이전 버전에서는 개발자 페이지 크기를 줄이기 위해 개별 컨트롤의 뷰 상태를 해제할 수 있지만 개별 컨트롤에 대 한 명시적 해야 했습니다. ASP.NET 4에서 웹 서버 컨트롤에 포함 된 *ViewStateMode* 하면 기본적으로 상태 보기를 사용 하지 않도록 설정 하 고 다음 페이지에서 필요로 하는 컨트롤에 대해서만 사용 하도록 설정 하는 속성입니다.

*ViewStateMode* 속성은 세 가지 값이 포함 된 열거형: *Enabled*, *사용 안 함*, 및 *상속*합니다. *사용 하도록 설정* 로 설정 된 모든 자식 컨트롤에 대 한 상태로 해당 컨트롤의 뷰 *상속* 이거나는 아무 것도 설정 합니다. *사용 안 함* 뷰 상태를 사용 하지 않도록 설정 및 *상속* 컨트롤을 사용 하도록 지정 합니다 *ViewStateMode* 부모 컨트롤에서 설정 합니다.

다음 예제와 방법을 *ViewStateMode* 속성 작동 합니다. 태그 및 코드 페이지의 제어에 대 한 값이 포함 된 *ViewStateMode* 속성:

[!code-aspx[Main](overview/samples/sample25.aspx)]

알 수 있듯이 코드 PlaceHolder1 컨트롤의 뷰 상태를 사용 하지 않도록 설정 합니다. 이 속성 값 상속 되는 자식 label1 컨트롤 (*상속* 의 기본값은 *ViewStateMode* 컨트롤에 대 한) 따라서 뷰 상태가 저장 합니다. PlaceHolder2 컨트롤에서 *ViewStateMode* 로 설정 된 *Enabled*label2이이 속성을 상속 및 뷰 상태를 저장 합니다. 페이지가 처음 로드 되 면 합니다 *텍스트* 속성이 모두 *레이블* 컨트롤 "[DynamicValue]" 문자열로 설정 됩니다.

이러한 설정의 효과 페이지를 처음으로 로드 하는 경우 브라우저에서 다음과 같은 출력이 표시 됩니다.

사용 안 함 `: [DynamicValue]`

사용 하도록 설정 합니다.`[DynamicValue]`

다시 게시 한 후 단, 다음과 같은 출력이 표시 됩니다.

사용 안 함 `: [DeclaredValue]`

사용 하도록 설정 합니다.`[DynamicValue]`

Label1 컨트롤 (입니다 *ViewStateMode* 값으로 설정 됩니다 *비활성*) 코드에서 설정 된 값이 유지 되지에 합니다. 하지만 Label2는 제어 (입니다 *ViewStateMode* 값으로 설정 됩니다 *Enabled*) 해당 상태를 유지 했습니다.

설정할 수도 있습니다 *ViewStateMode* 에 *@ Page* 다음 예제와 같이 지시문:

[!code-aspx[Main](overview/samples/sample26.aspx)]

합니다 *페이지* 클래스는 다른 컨트롤, 페이지의 다른 모든 컨트롤에 대 한 부모 컨트롤로 작동 합니다. 기본값인 *ViewStateMode* 됩니다 *Enabled* 에 대 한 인스턴스의 *페이지*합니다. 컨트롤을 기본값으로 하기 때문에 *상속*, 컨트롤에 상속 됩니다는 *Enabled* 속성 값을 설정 하지 않으면 *ViewStateMode* 페이지나 컨트롤 수준에서.

값을 *ViewStateMode* 경우에 뷰 상태를 유지 관리 하는 경우 속성에 따라 결정를 *EnableViewState* 속성이로 설정 되어 *true*. 경우는 *EnableViewState* 속성이 *false*를 뷰 상태를 유지 하지 것입니다 경우에 *ViewStateMode* 로 설정 되어 *사용*합니다.

이 기능에 대 한 적절 하 게 사용 된 *ContentPlaceHolder* 컨트롤을 설정할 수 있는 마스터 페이지에서 *ViewStateMode* 하 *비활성화 된* 마스터에 대 한 페이지를 사용 하도록 설정한 에 대해 개별적으로 *ContentPlaceHolder* 필요한 컨트롤에 포함 된 컨트롤 상태를 확인 합니다.

<a id="0.2__Toc224729035"></a><a id="0.2__Toc253429259"></a><a id="0.2__Toc243304633"></a>

### <a name="changes-to-browser-capabilities"></a>브라우저 기능 변경

ASP.NET 사용자 라는 기능을 사용 하 여 사이트를 탐색 하는 데 사용 하는 브라우저의 기능을 결정 *브라우저 기능*합니다. 브라우저 기능으로 표시 됩니다는 *HttpBrowserCapabilities* 개체 (의해 노출 되는 *Request.Browser* 속성). 예를 들어 사용할 수 있습니다 합니다 *HttpBrowserCapabilities* 유형 및 버전 현재 브라우저의 JavaScript의 특정 버전을 지원 하는지 여부를 결정 하는 개체입니다. 또는 사용할 수는 *HttpBrowserCapabilities* 모바일 장치에서 요청이 시작 된 여부를 결정 하는 개체입니다.

합니다 *HttpBrowserCapabilities* 개체 브라우저 정의 파일 집합에 의해 결정 됩니다. 이러한 파일 특정 브라우저의 기능에 대 한 정보를 포함 합니다. ASP.NET 4에서는 이러한 브라우저 정의 파일 최근에 도입 된 브라우저 및 Google Chrome, 연구 등 동작 BlackBerry 스마트폰을 및 Apple iPhone 장치에 대 한 정보를 포함 하도록 업데이트 되었습니다.

다음은 새로운 브라우저 정의 파일을 보여 줍니다.

- *blackberry.browser*
- *chrome.browser*
- *Default.browser*
- *firefox.browser*
- *gateway.browser*
- *generic.browser*
- *ie.browser*
- *iemobile.browser*
- *iphone.browser*
- *opera.browser*
- *safari.browser*

#### <a name="using-browser-capabilities-providers"></a>브라우저 기능 공급자를 사용 하 여

Asp.net 버전 3.5 서비스 팩 1에서는 다음과 같은 방법으로 브라우저에 있는 기능을 정의할 수 있습니다.

- 컴퓨터 수준에서 만들거나 업데이트 한 `.browser` 다음 폴더에 XML 파일:

- [!code-console[Main](overview/samples/sample27.cmd)]

- 브라우저 기능을 정의한 후 브라우저 기능 어셈블리를 다시 작성 하 고 GAC에 추가 하기 위해 Visual Studio 명령 프롬프트에서 다음 명령을 실행 하면:

- [!code-console[Main](overview/samples/sample28.cmd)]

- 만든 개별 응용 프로그램을 `.browser` 응용 프로그램에서 파일 `App_Browsers` 폴더입니다.

이러한 접근 방식은 XML 파일을 변경 해야 하 고 컴퓨터 수준 변경에 대 한 다시 시작 해야 응용 프로그램 aspnet를 실행 한 후\_regbrowsers.exe 프로세스입니다.

ASP.NET 4 라고 기능이 *브라우저 기능 공급자*합니다. 이름에서 알 수 있듯이 차례로 수 있는 공급자를 구축할 수이 있습니다가 브라우저 기능을 확인 하려면 사용자 고유의 코드를 사용 합니다.

실제로 개발자가 자주 정의 하지 마십시오 사용자 지정 브라우저 기능. 브라우저 파일 업데이트 프로세스에 대 한 고 업데이트 하 여 매우 복잡 한 하기가 및에 대 한 XML 구문을 `.browser` 파일 사용 및 정의 하기가 복잡할 수 있습니다. 항목은 훨씬 더 쉽게이 프로세스는 일반적인 브라우저 정의 구문 있다면 또는 최신 브라우저 정의 또는 이러한 데이터베이스에 대 한 웹 서비스까지 포함 된 데이터베이스입니다. 새 브라우저 기능 공급자 기능을 사용 하면 이러한 시나리오가 가능 하 고 유용 타사 개발자를 위한.

두 가지 주요 새 ASP.NET 4 브라우저 기능 공급자 기능을 사용 합니다: 정의 기능을 ASP.NET 브라우저 기능을 확장 하거나 완전히 대체 합니다. 다음 섹션에서는 먼저 기능을 대체 하는 방법을 차례로 확장 하는 방법입니다.

#### <a name="replacing-the-aspnet-browser-capabilities-functionality"></a>ASP.NET 브라우저 기능 기능 대체

ASP.NET 브라우저 기능 정의 기능을 완전히 대체 하려면 다음이 단계를 수행 합니다.

1. 파생 되는 공급자 클래스를 만듭니다 *HttpCapabilitiesProvider* 를 재정의 합니다 *GetBrowserCapabilities* 다음 예제와 같이 메서드: 

    [!code-csharp[Main](overview/samples/sample29.cs)]

    이 예제의 코드를 만듭니다 *HttpBrowserCapabilities* 개체, 브라우저 및 MyCustomBrowser 기능 설정을 라는 기능에만 지정 합니다.
2. 응용 프로그램을 사용 하 여 공급자를 등록 합니다. 

    응용 프로그램에서 공급자를 사용 하려면 추가 해야 합니다 *공급자* 특성을 *browserCaps* 섹션의 `Web.config` 또는 `Machine.config` 파일. (공급자 특성을 정의할 수도 있습니다는 *위치* 특정 모바일 장치에 대 한 폴더와 같이 응용 프로그램에서 특정 디렉터리에 대 한 요소입니다.) 다음 예제에서는 설정 하는 방법을 보여 줍니다 합니다 *공급자* 구성 파일의 특성:

    [!code-xml[Main](overview/samples/sample30.xml)]

    새 브라우저 기능 정의 등록 하는 또 다른 방법은 다음 예제에서와 같이 코드를 사용 하는 것:

    [!code-csharp[Main](overview/samples/sample31.cs)]

    이 코드에서 실행 해야 합니다는 *응용 프로그램\_시작* 이벤트는 `Global.asax` 파일입니다. 변경 된 *BrowserCapabilitiesProvider* 클래스는 캐시에서 확인 된 유효한 상태의 유지 되는지 확인 하기 위해 응용 프로그램의 코드를 실행 하기 전에 있어야 합니다. *HttpCapabilitiesBase* 개체입니다.

#### <a name="caching-the-httpbrowsercapabilities-object"></a>HttpBrowserCapabilities 개체 캐싱

앞의 예제 코드를 얻기 위해 사용자 지정 공급자를 호출할 때마다 실행 하는 한 가지 문제에는 *HttpBrowserCapabilities* 개체입니다. 이 하면 각 요청 하는 동안 여러 번 발생할 수 있습니다. 예제에서는 공급자에 대 한 코드를 수행 하지 않습니다 대부분. 그러나 사용자 지정 공급자의 코드에서 중요 한 작업을 수행 하는 경우를 얻기 위해 합니다 *HttpBrowserCapabilities* 개체 성능에 영향을 줄 수 있습니다. 이 방지 하기를 캐시할 수 있습니다 합니다 *HttpBrowserCapabilities* 개체입니다. 아래 단계를 수행합니다.

1. 파생 되는 클래스를 만듭니다 *HttpCapabilitiesProvider*, 다음 예제에서와 같은: 

    [!code-csharp[Main](overview/samples/sample32.cs)]

    예제에서는 코드는 사용자 지정 BuildCacheKey 메서드를 호출 하 여 캐시 키를 생성 및 사용자 지정 GetCacheTime 메서드를 호출 하 여 캐시 기간을 가져옵니다. 코드를 다음 확인 된 추가 *HttpBrowserCapabilities* 캐시 개체입니다. 개체를 캐시에서 검색에 다시 확인 하는 후속 요청 사용자 지정 공급자를 사용 합니다.
2. 앞의 절차에 설명 된 대로 응용 프로그램을 사용 하 여 공급자를 등록 합니다.

#### <a name="extending-aspnet-browser-capabilities-functionality"></a>ASP.NET 브라우저 기능 기능 확장

이전 섹션에는 새 하는 방법을 설명 *HttpBrowserCapabilities* ASP.NET 4에는 개체입니다. 또한 ASP.NET에 포함 되어 있는 항목에 새 브라우저 기능 정의 추가 하 여 ASP.NET 브라우저 기능 기능을 확장할 수 있습니다. XML 브라우저 정의 사용 하지 않고이 수행할 수 있습니다. 다음 절차에 표시 하는 방법입니다.

1. 파생 되는 클래스를 만듭니다 *HttpCapabilitiesEvaluator* 를 재정의 합니다 *GetBrowserCapabilities* 메서드를 다음 예제에서와 같이: 

    [!code-csharp[Main](overview/samples/sample33.cs)]

    이 코드는 먼저 브라우저를 확인 하기 위해 ASP.NET 브라우저 기능 기능을 사용 합니다. 그러나 브라우저 없음이 확인 되 면 정보를 기반으로 요청에 정의 된 (즉, 합니다 *브라우저* 의 속성을 *HttpBrowserCapabilities* 개체는 문자열 "Unknown"), 호출 사용자 지정 공급자 (MyBrowserCapabilitiesEvaluator) 브라우저를 식별 합니다.
2. 이전 예제에 설명 된 대로 응용 프로그램을 사용 하 여 공급자를 등록 합니다.

#### <a name="extending-browser-capabilities-functionality-by-adding-new-capabilities-to-existing-capabilities-definitions"></a>기존 기능 정의에 새 기능을 추가 하 여 브라우저 기능 기능 확장

사용자 지정 브라우저 정의가 공급자를 만드는 것 외에도 하 고 새 브라우저 정의 동적으로 만드는 추가 기능을 사용 하 여 기존 브라우저 정의 확장할 수 있습니다. 이렇게 하면 원하는 근접 하지만 몇 가지 기능만 없는 정의 사용할 수 있습니다. 이렇게 하려면 다음 단계를 따릅니다.

1. 파생 되는 클래스를 만듭니다 *HttpCapabilitiesEvaluator* 를 재정의 합니다 *GetBrowserCapabilities* 메서드를 다음 예제에서와 같이: 

    [!code-csharp[Main](overview/samples/sample34.cs)]

    예제 코드는 기존 ASP.NET 확장 *HttpCapabilitiesEvaluator* 클래스 및 가져옵니다 합니다 *HttpBrowserCapabilities* 현재 요청 정의 다음 코드를 사용 하 여 일치 하는 개체 :

    [!code-csharp[Main](overview/samples/sample35.cs)]

    다음 코드를 추가 하거나이 브라우저에 대 한 기능을 수정할 수 있습니다. 두 가지 방법으로 새로운 브라우저 기능을 지정할 수 있습니다.

    - 에 키/값 쌍을 추가 합니다 *IDictionary* 개체에서 노출 되는 *기능* 속성의는 *HttpCapabilitiesBase* 개체. 이전 예제에서는 코드의 값을 사용 하 여 다중 터치 라는 기능을 추가 *true*합니다.
    - 기존 속성을 설정 합니다 *HttpCapabilitiesBase* 개체입니다. 이전 예제에서 코드를 설정 합니다 *프레임* 속성을 *true*합니다. 이 속성은 단순히에 대 한 접근자를 *IDictionary* 에 의해 노출 되는 개체를 *기능* 속성입니다. 

        > [!NOTE]
        > 이 모델의 모든 속성에 적용 됩니다 *HttpBrowserCapabilities*를 컨트롤 어댑터를 포함 합니다.
2. 이전 절차에서 설명 된 대로 응용 프로그램을 사용 하 여 공급자를 등록 합니다.

<a id="0.2__Toc224729036"></a><a id="0.2__Toc253429260"></a><a id="0.2__Toc243304634"></a>

### <a name="routing-in-aspnet-4"></a>ASP.NET 4에서 라우팅

ASP.NET 4 Web Forms를 사용 하 여 라우팅을 사용 하는 것에 대 한 기본 제공 지원을 추가 합니다. 적용할 응용 프로그램을 구성 하는 라우팅 하면 실제 파일에 매핑되지 않는 Url을 요청 합니다. 대신, 라우팅 Url을 사용자에 게 의미 하 고 응용 프로그램에 대 한 검색 엔진 최적화 (SEO)를 사용 하 여 도움이 되는 정의를 사용할 수는 있습니다. 예를 들어 기존 응용 프로그램의 제품 범주를 표시 하는 페이지의 URL을 다음과 같이 표시 될 수 있습니다.

[!code-console[Main](overview/samples/sample36.cmd)]

라우팅를 사용 하 여 동일한 정보를 렌더링 하는 다음 URL을 허용 하도록 응용 프로그램을 구성할 수 있습니다.

[!code-console[Main](overview/samples/sample37.cmd)]

라우팅 ASP.NET 3.5 SP1부터 제공 되었습니다. (ASP.NET 3.5 SP1의 라우팅을 사용 하는 방법의 예에 대 한 항목을 참조 하세요 [WebForms 사용 하 여 라우팅 사용 하 여](http://haacked.com/archive/2008/03/11/using-routing-with-webforms.aspx "이 항목의 제목입니다.") Phil Haack의 블로그에서.) 그러나 ASP.NET 4는 다음과 같은 쉽게 라우팅을 사용 하는 몇 가지 기능이 있습니다.

- 합니다 *PageRouteHandler* 경로 정의할 때 사용 하는 간단한 HTTP 처리기 클래스입니다. 클래스는 요청으로 라우팅되는 페이지에 데이터를 전달 합니다.
- 새 속성 *HttpRequest.RequestContext* 하 고 *Page.RouteData* (에 대 한 프록시는 합니다 *HttpRequest.RequestContext.RouteData* 개체). 이러한 속성 쉽게 경로에서 전달 되는 정보에 액세스할 수 있습니다.
- 다음 새 식 작성기에 정의 된 *System.Web.Compilation.RouteUrlExpressionBuilder* 하 고 *System.Web.Compilation.RouteValueExpressionBuilder*:
- *RouteUrl*, ASP.NET 서버 컨트롤 내에서 경로 URL에 해당 하는 URL을 만드는 간단한 방법을 제공 합니다.
- *RouteValue*에서 정보를 추출 하는 간단한 방법을 제공 합니다 *RouteContext* 개체입니다.
- 합니다 *RouteParameter* 쉽게에 포함 된 데이터를 전달 하는 클래스를 *RouteContext* 개체 데이터 소스 컨트롤에 대 한 쿼리를 (비슷합니다 [ *FormParameter* ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx)).

#### <a name="routing-for-web-forms-pages"></a>Web Forms 페이지에 대 한 라우팅

다음 예제에서는 새을 사용 하 여 Web Forms 경로 정의 하는 방법을 보여 줍니다 *MapPageRoute* 메서드는 *경로* 클래스:

[!code-csharp[Main](overview/samples/sample38.cs)]

ASP.NET 4 소개 합니다 *MapPageRoute* 메서드. 다음 예제에서는 이전 예에서 같이 SearchRoute 정의에 동일 하지만 사용 하 여 *PageRouteHandler* 클래스입니다.

[!code-csharp[Main](overview/samples/sample39.cs)]

예제에서 코드를 물리적 페이지에 경로 매핑합니다 (첫 번째 경로를 `~/search.aspx`). 첫 번째 경로 정의는 또한 searchterm 라는 매개 변수에 URL에서 추출 하는 페이지에 전달 지정 합니다.

합니다 *MapPageRoute* 메서드는 다음 메서드 오버 로드를 지원 합니다.

- *MapPageRoute (문자열 routeName, 문자열 routeUrl, 문자열 physicalFile, bool checkPhysicalUrlAccess)*
- *MapPageRoute (문자열 routeName, 문자열 routeUrl, 문자열 physicalFile, bool checkPhysicalUrlAccess, RouteValueDictionary 기본값)*
- *MapPageRoute (문자열 routeName, 문자열 routeUrl, 문자열 physicalFile, bool checkPhysicalUrlAccess, RouteValueDictionary 기본값, RouteValueDictionary 제약 조건)*

합니다 *checkPhysicalUrlAccess* 매개 변수 경로으로 라우팅되지 물리적 페이지에 대 한 보안 권한을 확인 해야 하는지 여부를 지정 합니다 (이 예제의 경우 search.aspx) 들어오는 URL에 대 한 권한과 (이 경우 검색 / {searchterm}). 경우 값 *checkPhysicalUrlAccess* 됩니다 *false*, 들어오는 URL의 사용 권한만 확인 합니다. 에 정의 된 이러한 권한을 `Web.config` 다음과 같은 설정을 사용 하는 파일:

[!code-xml[Main](overview/samples/sample40.xml)]

예제 구성에서는 액세스가 거부 되었습니다 물리적 페이지에 `search.aspx` 관리자 역할이 있는 사용자를 제외한 모든 사용자에 대 한 합니다. 경우는 *checkPhysicalUrlAccess* 매개 변수는 설정 *true* (기본값) 인 관리 사용자만 액세스할 수 있습니다 URL /search/ {searchterm} 물리적 페이지 search.aspx 이므로 해당 역할의 사용자에 게 제한 합니다. 하는 경우 *checkPhysicalUrlAccess* 로 설정 된 *false* 하 고 이전 예제와 같이 사이트를 구성 하 고 모든 인증 된 사용자 URL /search/ {searchterm}에 액세스할 수 있습니다.

#### <a name="reading-routing-information-in-a-web-forms-page"></a>Web Forms 페이지에서 라우팅 정보 읽기

Web Forms 물리적 페이지의 코드에서 URL에서 추출 된 라우팅 정보에 액세스할 수 있습니다 (또는 다른 개체를 추가 하는 기타 정보를 *RouteData* 개체) 두 개의 새로운 속성을 사용 하 여:  *HttpRequest.RequestContext* 하 고 *Page.RouteData*합니다. (*Page.RouteData* 래핑합니다 *HttpRequest.RequestContext.RouteData*.) 다음 예제에서는 사용 하는 방법을 보여 줍니다 *Page.RouteData*합니다.

[!code-csharp[Main](overview/samples/sample41.cs)]

이전 예제에서는 경로에 정의 된 대로 지정 하려면 매개 변수에 전달 된 값을 추출 합니다. 다음 요청 URL을 고려 합니다.

[!code-console[Main](overview/samples/sample42.cmd)]

경우이 요청이 "scott"에서 렌더링할 수는 단어를 `search.aspx` 페이지입니다.

#### <a name="accessing-routing-information-in-markup"></a>태그의 라우팅 정보에 액세스

이전 섹션에서 설명 하는 방법을 Web Forms 페이지의 코드에서 경로 데이터를 가져오는 방법을 보여 줍니다. 또한 태그에서 같은 정보에 액세스할 수 있는 식을 사용할 수 있습니다. 식 작성기는 선언적 코드를 사용 하는 강력 하 고 세련 된 방법입니다. (자세한 내용은 항목을 참조 하세요 [Express 직접 사용 하 여 사용자 지정 식 작성기](http://haacked.com/archive/2006/11/29/Express_Yourself_With_Custom_Expression_Builders.aspx) Phil Haack의 블로그에서.)

ASP.NET 4 Web Forms에 라우팅에 대 한 두 명의 새 식 작성기를 포함합니다. 다음 예제에서는 사용 하는 방법을 보여 줍니다.

[!code-aspx[Main](overview/samples/sample43.aspx)]

예에서는 *RouteUrl* 식은 경로 매개 변수를 기반으로 하는 URL을 정의 하는데 사용 됩니다. 이 태그에 전체 URL 하드 코딩 하지 않아도 수를 저장 하 고이 링크를 변경 하지 않고도 URL 구조를 나중에 변경할 수 있습니다.

앞에서 정의한 경로 따라이 태그는 다음 URL을 생성 합니다.

[!code-console[Main](overview/samples/sample44.cmd)]

ASP.NET 올바른 경로 자동으로 작동 (즉, 올바른 URL을 생성) 입력된 매개 변수를 기반 합니다. 또한를 사용 하 여에 대 한 경로 지정할 수 있는 식에서 경로 이름을 포함할 수 있습니다.

다음 예제에서는 사용 하는 방법을 보여 줍니다 합니다 *RouteValue* 식입니다.

[!code-aspx[Main](overview/samples/sample45.aspx)]

이 컨트롤이 포함 된 페이지를 실행 하는 경우 "scott" 값이 레이블에 표시 됩니다.

합니다 *RouteValue* 식 손쉽게 태그에서 경로 데이터를 사용 하 고 더 복잡 한 Page.RouteData["x 작업할 것을 방지 하기"] 태그의 구문입니다.

#### <a name="using-route-data-for-data-source-control-parameters"></a>경로 데이터를 사용 하 여 데이터 원본에 대 한 제어 매개 변수

합니다 *RouteParameter* 클래스를 사용 하면 데이터 소스 컨트롤에서 쿼리에 대 한 매개 변수 값으로 경로 데이터를 지정 합니다. 것 [훨씬 처럼 작동 합니다](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx) 다음 예와에서 같이 클래스:

[!code-aspx[Main](overview/samples/sample46.aspx)]

경로 매개 변수 지정 하려면 값에 사용할이 경우에 @companyname 에서 매개 변수를 <em>선택</em> 문입니다.

<a id="0.2__Toc224729037"></a><a id="0.2__Toc253429261"></a><a id="0.2__Toc243304635"></a>

### <a name="setting-client-ids"></a>클라이언트 Id를 설정합니다.

새 *ClientIDMode* ASP.NET에서 장기 문제를 해결 하는 속성 즉 만들려면 어떻게 해야 컨트롤을 *id* 렌더링 하는 요소에 대 한 특성입니다. 알면 합니다 *id* 렌더링 된 요소에 대 한 특성은 응용 프로그램에 이러한 요소를 참조 하는 클라이언트 스크립트를 포함 하는 경우에 중요 합니다.

합니다 *id* 웹 서버 컨트롤의 렌더링 된 HTML의 특성에 따라 생성 되는 *ClientID* 컨트롤의 속성입니다. ASP.NET 4에서 생성 하는 알고리즘까지 합니다 *id* 에서 특성을 *ClientID* 속성 ID를 사용 하 여 및 (반복 된 컨트롤의 경우 (해당 되는 경우)의 명명 컨테이너를 연결 했습니다 데이터 컨트롤) 접두사 및 일련 번호를 추가 합니다. 이 항상 보장 페이지에서 컨트롤의 Id는 고유 하는 동안 컨트롤 Id는 예측할 수 없습니다 및 클라이언트 스크립트에서 참조 하기 어려웠습니다 따라서 알고리즘이 했습니다.

새 *ClientIDMode* 속성을 사용 하면 클라이언트 ID가 컨트롤에 대 한 생성 하는 방법에 더 정확 하 게 지정할 수 있습니다. 설정할 수 있습니다 합니다 *ClientIDMode* 페이지에 대 한 포함 하는 모든 컨트롤에 대 한 속성입니다. 가능한 설정은 다음과 같습니다.

- *AutoID* – 생성 하는 알고리즘을 동일 *ClientID* 이전 버전의 ASP.NET에서 사용 된 속성 값입니다.
- *정적* –이 지정 된 *ClientID* 값 부모 명명 컨테이너의 Id를 연결 하지 않고 ID와 동일 하 게 됩니다. 이 웹 사용자 컨트롤에 유용할 수 있습니다. 웹 사용자 정의 컨트롤을 다른 컨테이너 컨트롤의 여러 페이지에 있는 수에 있기 때문에 어려울 수 있습니다 사용 하는 컨트롤에 대 한 클라이언트 스크립트를 작성 합니다 *AutoID* 알고리즘 ID 값을 예측할 수 없습니다. .
- *예측 가능한* –이 옵션은 주로 반복 템플릿을 사용 하는 데이터 컨트롤에서 사용 합니다. 하지만 생성 된 컨트롤의 명명 컨테이너의 ID 속성을 연결 *ClientID* 값 "ctlxxx"과 같은 문자열을 포함 하지 않습니다. 이 설정을 사용 하 여 함께 작동 하는 *ClientIDRowSuffix* 컨트롤의 속성입니다. 설정 된 *ClientIDRowSuffix* 생성 된 속성 데이터 필드의 이름 및 해당 필드의 값을 접미사로 사용 됩니다 *ClientID* 값입니다. 일반적으로 데이터 레코드의 기본 키 사용 합니다 *ClientIDRowSuffix* 값입니다.
- *상속* –이 설정은 컨트롤에 대 한 기본 동작 이므로 컨트롤의 ID를 생성이 해당 부모와 동일한 지를 지정 합니다.

설정할 수 있습니다 합니다 *ClientIDMode* 페이지 수준 속성입니다. 기본값 정의 *ClientIDMode* 현재 페이지에 있는 모든 컨트롤에 대 한 값입니다.

기본값 *ClientIDMode* 페이지 수준에서 값이 *AutoID*, 및 기본값 *ClientIDMode* 제어 수준에는 값은 *상속*. 결과적으로, 코드에서 아무 곳 이나이 속성을 설정 하지 않으면, 모든 컨트롤은 기본적으로 *AutoID* 알고리즘입니다.

페이지 수준 값을 설정 합니다 *@ Page* 지시문을 다음 예와에서 같이:

[!code-aspx[Main](overview/samples/sample47.aspx)]

설정할 수도 있습니다는 *ClientIDMode* 컴퓨터 수준 또는 응용 프로그램 수준 구성 파일의 값입니다. 기본값 정의 *ClientIDMode* 응용 프로그램의 모든 페이지에서 모든 컨트롤에 대 한 설정입니다. 기본 컴퓨터 수준에서 값을 설정 하는 경우 정의 *ClientIDMode* 해당 컴퓨터에서 모든 웹 사이트를 설정 합니다. 다음 예제와 합니다 *ClientIDMode* 구성 파일에서 설정 합니다.

[!code-xml[Main](overview/samples/sample48.xml)]

값을 앞에서 설명한 대로 합니다 *ClientID* 속성은 컨트롤의 부모에 대 한 명명 컨테이너에서 파생 됩니다. 마스터 페이지를 사용 하는 경우와 같은 일부 시나리오에서는 컨트롤 수 결국 Id를 사용 하 여 다음과 같은 HTML 렌더링:

[!code-html[Main](overview/samples/sample49.html)]

도 *입력* 태그에 표시 된 요소 (에서 *텍스트 상자* 컨트롤) 두 개의 명명 컨테이너는 페이지에서 심층 (중첩 된 *ContentPlaceholder* 컨트롤), 마스터 페이지를 처리 하는 방식으로 인해 최종 결과 다음과 같은 컨트롤 ID는:

[!code-console[Main](overview/samples/sample50.cmd)]

이 ID 페이지에서 고유성이 보장 됩니다 이지만 불필요 하 게 대부분의 시간입니다. 렌더링 된 ID의 길이를 줄이려면 ID 생성 되는 방식을 효과적으로 제어를 사용 한다고 가정해 보겠습니다. (예를 들어, 하려는 "ctlxxx" 접두사를 제거 합니다.) 설정 된 경우이 작업을 수행 하는 가장 쉬운 방법은 합니다 *ClientIDMode* 다음 예와에서 같이 속성:

[!code-aspx[Main](overview/samples/sample51.aspx)]

이 샘플에서는 합니다 *ClientIDMode* 속성이로 설정 된 *정적* 바깥쪽에 대 한 *NamingPanel* 요소와 설정 *예측 가능* 내부 *NamingControl* 요소입니다. 이러한 설정 (나머지 페이지 및 마스터 페이지는 이전 예제 에서처럼에서 동일한 것으로 간주 됩니다.) 다음 태그에서 발생 합니다.

[!code-html[Main](overview/samples/sample52.html)]

합니다 *정적* 설정은 가장 바깥쪽 안의 모든 컨트롤에 대 한 명명 계층 구조를 다시 설정의 영향을 주지 *NamingPanel* 요소 및 제거는 *ContentPlaceHolder* 하 고 *MasterPage* Id는 생성 된 id입니다. (합니다 *이름을* 렌더링 된 요소의 특성에 영향을 받지 않습니다, 정상적인 ASP.NET 기능을 보존 되는 이벤트에 대 한 상태를 확인 하 고 등.) 부작용의 명명 계층 구조를 다시 설정 하는 태그를 이동 하는 경우에 합니다 *NamingPanel* 다른 요소 *ContentPlaceholder* 컨트롤을 렌더링 된 클라이언트 Id는 동일 하 게 유지 합니다.

> [!NOTE]
> 렌더링 된 컨트롤 Id는 고유 해야 하는 것을 note 합니다. 그렇지 않은 경우 클라이언트와 같은 개별 HTML 요소에 대 한 고유 Id를 필요로 하는 모든 기능을 중단할 수 있습니다 *document.getElementById* 함수입니다.


#### <a name="creating-predictable-client-ids-in-data-bound-controls"></a>데이터 바인딩된 컨트롤에서 예측 가능한 클라이언트 Id 만들기

합니다 *ClientID* 레거시 알고리즘에서 데이터 바인딩된 목록 컨트롤의 컨트롤 수에 대해 생성 되는 값 하며를 실제로 예측할 수 없습니다. 합니다 *ClientIDMode* 기능을 통해 이러한 Id를 통해 생성 된 제어를 강화할 해야 있습니다.

다음 예제에서 태그를 *ListView* 제어 합니다.

[!code-aspx[Main](overview/samples/sample53.aspx)]

이전 예에서 합니다 *ClientIDMode* 하 고 *RowClientIDRowSuffix* 속성 태그에서 설정 됩니다. 합니다 *ClientIDRowSuffix* 속성을 데이터 바인딩된 컨트롤에만 사용할 수 있습니다 하 고 해당 동작은 사용 중인 컨트롤에 따라 다릅니다. 차이점은 다음과 같습니다.

- *GridView* 컨트롤-지정할 수 있습니다 하나 이상의 열 이름을 데이터 원본에서 런타임에 클라이언트 Id 생성에 결합 됩니다. 예를 들어, 설정 하는 경우 *RowClientIDRowSuffix* "productname, ProductId" 렌더링 된 요소는 다음과 같은 형식을 갖습니다에 대 한 Id를 제어 합니다.

- [!code-console[Main](overview/samples/sample54.cmd)]

- *ListView* 컨트롤-클라이언트 id와 같습니다. 추가 되는 데이터 원본에서 단일 열을 지정할 수 있습니다 예를 들어 설정한 *ClientIDRowSuffix* 렌더링 된 컨트롤 Id는 다음과 같은 형식을 "productname" 갖습니다.

- [!code-console[Main](overview/samples/sample55.cmd)]

- 이 경우 후행 1은 현재 데이터 항목의 제품 ID에서 파생 됩니다.

- *Repeater* 컨트롤-이 컨트롤을 지원 하지 않습니다 합니다 *ClientIDRowSuffix* 속성입니다. 에 *Repeater* 컨트롤에 현재 행의 인덱스 사용 됩니다. ClientIDMode를 사용 하는 경우 = "예측 가능"를 *Repeater* 컨트롤 형식에 있는 클라이언트 Id가 생성 됩니다.

- [!code-console[Main](overview/samples/sample56.cmd)]

- 후행 0에는 현재 행의 인덱스입니다.

합니다 *FormView* 하 고 *DetailsView* 컨트롤을 지원 하지 않는 하므로 여러 행을 표시 하지 않습니다는 *ClientIDRowSuffix* 속성입니다.

<a id="0.2__Toc224729038"></a><a id="0.2__Toc253429262"></a><a id="0.2__Toc243304636"></a>

### <a name="persisting-row-selection-in-data-controls"></a>데이터 컨트롤에서 유지 행 선택

합니다 *GridView* 하 고 *ListView* 컨트롤에는 사용자가 행을 선택할 수 있습니다. ASP.NET의 이전 버전에서는 선택을 기반으로 페이지의 행 인덱스입니다. 예를 들어 1 페이지에서 세 번째 항목을 선택 하 고 다음 2 페이지로 이동 하는 경우에 해당 페이지에서 세 번째 항목이 선택 됩니다.

보관 된 선택 된 처음에.NET Framework 3.5 SP1의 동적 데이터 프로젝트 에서만에서 지원 됩니다. 이 기능을 사용 하는 경우 현재 선택한 항목은 항목에 대 한 데이터 키를 기반으로 합니다. 이 1 페이지에서 세 번째 행을 선택 하 고 2 페이지로 이동 하는 경우 2 페이지에서 선택 된 것을 의미 합니다. 1 페이지로 다시 이동 하면 세 번째 행 선택 계속 됩니다. 보관 된 선택에 지원 됩니다는 *GridView* 및 *ListView* 사용 하 여 모든 프로젝트에서 컨트롤을 *EnablePersistedSelection* 속성에 표시 된 대로 다음 예제:

[!code-aspx[Main](overview/samples/sample57.aspx)]

<a id="0.2__Toc253429263"></a><a id="0.2__Toc243304637"></a>

### <a name="aspnet-chart-control"></a>ASP.NET 차트 컨트롤

ASP.NET *차트* 컨트롤이.NET Framework의 데이터 시각화 제품을 확장 합니다. 사용 하는 *차트* 컨트롤, ASP.NET 페이지는 복잡 한 통계 또는 재무 분석을 위해 직관적 이며 시각적으로 우수한 차트를 만들 수 있습니다. ASP.NET *차트* 컨트롤 소개 된 추가 기능으로.NET Framework 버전 3.5 SP1 릴리스 및.NET Framework 4 릴리스의 일부입니다.

컨트롤에는 다음 기능이 포함 됩니다.

- 35가지 개별 차트 종류
- 차트 영역, 제목, 범례 및 주석을의 무제한입니다.
- 다양 한 모든 차트 요소에 대 한 모양 설정 합니다.
- 대부분의 차트 종류에 대 한 3 차원 지원 합니다.
- 데이터 요소 주위에 자동으로 맞출 수 있는 스마트 데이터 레이블을 지정 합니다.
- 줄무늬 선을, 배율 구분선 및 로그 크기를 조정 합니다.
- 데이터 분석 및 변형을 위한 50개가 넘는 재무 및 통계 수식
- 단순 바인딩 및 차트 데이터의 조작 합니다.
- 날짜, 시간 및 통화와 같은 일반적인 데이터 형식 지원 합니다.
- 대화형 작업 및 클라이언트를 포함 하는 이벤트 기반 사용자 지정에 대 한 지원을 Ajax를 사용 하 여 이벤트를 클릭 합니다.
- 상태 관리
- 이진 스트리밍

다음 그림에서는 ASP.NET 차트 컨트롤에 의해 생성 되는 재무 차트의 예를 보여 줍니다.

<a id="0.2_graphic17"></a>![](overview/_static/image1.png)

그림 2: ASP.NET 차트 컨트롤 예

ASP.NET 차트 컨트롤을 사용 하는 방법의 더 많은 예제에서 샘플 코드를 다운로드 합니다 [Microsoft Chart controls 예제 환경](https://go.microsoft.com/fwlink/?LinkId=128300) MSDN 웹 사이트의 페이지입니다. 콘텐츠 커뮤니티의 많은 샘플을 찾을 수 있습니다 합니다 [차트 컨트롤 포럼](https://go.microsoft.com/fwlink/?LinkId=128713)합니다.

#### <a name="adding-the-chart-control-to-an-aspnet-page"></a>ASP.NET 페이지에 차트 컨트롤 추가

다음 예제에서는 추가 하는 방법을 보여 줍니다는 *차트* 태그를 사용 하 여 ASP.NET 페이지에는 컨트롤입니다. 예에서는 *차트* 컨트롤에 정적 데이터 요소에 대 한 세로 막대형 차트를 생성 합니다.

[!code-aspx[Main](overview/samples/sample58.aspx)]

#### <a name="using-3-d-charts"></a>3 차원 차트를 사용 하 여

*차트* 컨트롤에는 *ChartAreas* 포함할 수 있는 컬렉션 *ChartArea* 차트 영역의 특성을 정의 하는 개체. 예를 들어 3 차원 차트 영역에 대 한를 사용 하려면 사용 합니다 *있는 Area3DStyle* 다음 예제와 같이 속성:

[!code-aspx[Main](overview/samples/sample59.aspx)]

아래 그림의 4 개 시리즈를 사용 하 여 3 차원 차트의 *표시줄* 차트 종류입니다.

<a id="0.2_graphic18"></a>![](overview/_static/image2.png)

그림 3: 3 차원 가로 막대형 차트

#### <a name="using-scale-breaks-and-logarithmic-scales"></a>배율 구분선 및 로그 눈금 간격 사용

배율 구분선 눈금와 숙련도 차트에 추가할 추가 두 가지 방법입니다. 이러한 기능은 각 차트 영역 축 관련이 있습니다. 예를 들어 차트 영역의 기본 Y 축에서 이러한 기능을 사용 하려면 사용 합니다 *AxisY.IsLogarithmic* 및 *ScaleBreakStyle* 속성에는 *ChartArea* 개체. 다음 코드 조각은 기본 Y 축의 배율 구분선을 사용 하는 방법을 보여 줍니다.

[!code-aspx[Main](overview/samples/sample60.aspx)]

아래 그림에는 사용 하도록 설정 하는 배율 구분선을 사용 하 여 Y 축을 보여 줍니다.

<a id="0.2_graphic19"></a>![](overview/_static/image3.png)

그림 4: 배율 구분선

<a id="0.2__QueryExtender"></a><a id="0.2__Toc224729041"></a><a id="0.2__Toc253429264"></a><a id="0.2__Toc243304638"></a>

### <a name="filtering-data-with-the-queryextender-control"></a>QueryExtender 컨트롤을 사용 하 여 데이터를 필터링합니다.

데이터 기반 웹 페이지를 만드는 개발자를 위한 매우 일반적인 작업 데이터를 필터링 하는 것입니다. 이 일반적으로 수행 된 빌드하여 *여기서* 절에서 데이터 소스 컨트롤입니다. 이 방법은 복잡할 수 있습니다 및 일부 경우에는 *여기서* 구문 수 없다는 기본 데이터베이스의 전체 기능을 활용 합니다.

필터링을 더 쉽게 새 되도록 *QueryExtender* 컨트롤이 ASP.NET 4에 추가 되었습니다. 이 컨트롤을 추가할 수 있습니다 *EntityDataSource* 하거나 *LinqDataSource* 이러한 컨트롤에 의해 반환 되는 데이터를 필터링 하기 위해 컨트롤입니다. 때문에 합니다 *QueryExtender* LINQ에 의존 하 여, 데이터를 매우 효율적이 고 작업의 결과 페이지를에 전송 되기 전에 데이터베이스 서버에 필터가 적용 됩니다.

합니다 *QueryExtender* 컨트롤은 다양 한 필터 옵션을 지원 합니다. 다음 섹션에서는 이러한 옵션을 설명 하 고 사용 하는 방법의 예제를 제공 합니다.

#### <a name="search"></a>검색

검색 옵션에 대 한 합니다 *QueryExtender* 컨트롤 지정 된 필드에 검색을 수행 합니다. 다음 예제에서는 컨트롤 사용 TextBoxSearch 컨트롤과 내용 검색에 입력 된 텍스트를 `ProductName` 하 고 `Supplier.CompanyName` 에서 반환 되는 데이터의 열을 *LinqDataSource* 컨트롤입니다.

[!code-aspx[Main](overview/samples/sample61.aspx)]

#### <a name="range"></a>범위

범위 옵션 검색 옵션을 유사 하지만 범위를 정의 하는 값의 쌍을 지정 합니다. 다음 예에서 *QueryExtender* 검색을 제어 합니다 `UnitPrice` 에서 반환 된 데이터의 열에에서는 *LinqDataSource* 컨트롤. 범위는 페이지의 TextBoxFrom 및 TextBoxTo 컨트롤에서 읽습니다.

[!code-aspx[Main](overview/samples/sample62.aspx)]

#### <a name="propertyexpression"></a>PropertyExpression

속성 식 옵션 속성 값 비교를 정의할 수 있습니다. 식이 계산 되는 경우 *true*, 검사 되는 데이터가 반환 됩니다. 다음 예제에서는 *QueryExtender* 컨트롤의 데이터를 비교 하 여 데이터를 필터링는 `Discontinued` 페이지 CheckBoxDiscontinued 컨트롤에서 열 값을 합니다.

[!code-aspx[Main](overview/samples/sample63.aspx)]

#### <a name="customexpression"></a>CustomExpression

마지막으로 사용 하 여 사용 하 여 사용자 지정 식을 지정할 수 있습니다 합니다 *QueryExtender* 제어 합니다. 이 옵션을 통해 사용자 지정 필터 논리를 정의 하는 페이지에서 함수를 호출할 수 있습니다. 다음 예제에서는 사용자 지정 식에 선언적으로 지정 하는 방법을 보여 줍니다 합니다 *QueryExtender* 제어 합니다.

[!code-aspx[Main](overview/samples/sample64.aspx)]

다음 예제에서는 사용자 지정 함수에서 호출 하는 *QueryExtender* 제어 합니다. 포함 된 데이터베이스 쿼리를 사용 하는 대신이 경우에 *여기서* 절, 코드를 사용 하 여 LINQ 쿼리를 데이터를 필터링 합니다.

[!code-csharp[Main](overview/samples/sample65.cs)]

이러한 예제에서 사용 되는 식이 하나만 표시 합니다 *QueryExtender* 한 번에 제어 합니다. 그러나 내에서 여러 식을 포함할 수 있습니다 합니다 *QueryExtender* 제어 합니다.

<a id="0.2__Toc253429265"></a><a id="0.2__Toc243304639"></a>

### <a name="html-encoded-code-expressions"></a>Html 인코딩된 코드 식

(특히 ASP.NET MVC)와 함께 몇 가지 ASP.NET 사이트를 사용 하 여에 크게 의존 `<%` =  `expression %>` 구문 ("코드 너 깃"이 라고도 함) 응답에 일부 텍스트를 작성 합니다. 코드 식을 사용 하면 텍스트를 사용자에서 제공 되는 경우 텍스트를 입력 하 고, 해당 페이지를 열어 놓을 수는 XSS (교차 사이트 스크립팅) 공격에 HTML로 인코딩합니다 잊기 쉽습니다.

ASP.NET 4 코드 식에 대 한 새 구문을 제공합니다.

[!code-aspx[Main](overview/samples/sample66.aspx)]

이 구문은 HTML 응답을 쓸 때 기본적으로 인코딩을 사용 합니다. 이 새 식 다음에 효과적으로 변환합니다.

[!code-aspx[Main](overview/samples/sample67.aspx)]

예를 들어 &lt;%: 요청 ["/userinput&gt"] %&gt; 의 값에 HTML 인코딩을 수행 *["/userinput&gt"] 요청*합니다.

이 기능의 목적은 모든 단계에서 사용할 항목을 결정 하지 않아도 됩니다 있도록 새 구문을 사용 하 여 이전 구문의 모든 인스턴스를 대체할 수 있도록 합니다. 그러나 가지 사례가 출력 되는 텍스트를 HTML 알 수 있도록 하거나 이미 인코딩된 있는 이중 인코딩으로 경우에 발생할 수 있습니다.

이러한 경우에 대 한 ASP.NET 4 소개 새로운 인터페이스인 *IHtmlString*, 구체적인 구현과 함께 *HtmlString*합니다. 이러한 형식의 인스턴스를 사용 하는 반환 값 이미 올바르게 인코딩된 (이거나 그렇지 않으면 검사) HTML로 표시 하 고 따라서 값을 프로그램이 되지 않음을 HTML로 인코딩된 다시를 나타낼 수 있습니다. 예를 들어, 다음 안 됩니다 (아니며) HTML 인코딩해야 합니다.

[!code-aspx[Main](overview/samples/sample68.aspx)]

ASP.NET MVC 2 도우미 메서드 ASP.NET 4를 실행 하는 경우이 새 구문을 사용 하 여 사용 하지 않은 이중 인코딩 되도록 업데이트 된만 되었습니다. 이 새 구문은 ASP.NET 3.5 SP1을 사용 하 여 응용 프로그램을 실행 하는 경우 작동 하지 않습니다.

이 XSS 공격 으로부터 보호를 보장 하지는 것을 염두에 두십시오. 예를 들어 따옴표에 있지 않은 특성 값을 사용 하는 HTML 여전히 사용자 입력을 포함할 수 있습니다. Note ASP.NET 컨트롤 및 ASP.NET MVC 도우미 출력 항상 포함 특성 값 따옴표 안에 있는 것이 좋습니다.

마찬가지로,이 구문은 사용자 입력을 기반으로 하는 JavaScript 문자열을 만들 때와 같은 JavaScript 인코딩을 수행 하지 않습니다.

<a id="0.2__Toc253429266"></a><a id="0.2__Toc243304640"></a>

### <a name="project-template-changes"></a>프로젝트 템플릿 변경

ASP.NET의 이전 버전에서는 Visual Studio를 사용 하 여 새 웹 사이트 프로젝트 또는 웹 응용 프로그램 프로젝트를 만들 때 결과 프로젝트에 들어만 Default.aspx 페이지에서 기본값 `Web.config` 파일 및 `App_Data` 폴더 아래에 표시 된 것과 같이 그림:

<a id="0.2_graphic1A"></a>![](overview/_static/image4.png)

Visual Studio를 전혀 다음 그림에 나와 있는 것 처럼 파일이 없는 하는 빈 웹 사이트 프로젝트 형식을 지원 합니다.

<a id="0.2_graphic1B"></a>![](overview/_static/image5.png)

결과 있다는 점입니다 초보자를 위한에 대 한 지침이 거의 프로덕션 웹 응용 프로그램을 빌드하는 방법을 설명 합니다. 따라서 ASP.NET 4에서는 세 개의 새로운 템플릿이 고 빈 웹 응용 프로그램 프로젝트에 대 한 웹 응용 프로그램 및 웹 사이트 프로젝트에 대해 각각 1을 소개합니다.

#### <a name="empty-web-application-template"></a>빈 웹 응용 프로그램 템플릿

이름에서 알 수 있듯이 빈 웹 응용 프로그램 템플릿에 축소 된 기본 웹 응용 프로그램 프로젝트입니다. 다음 그림에 표시 된 것과 같이 Visual Studio 새 프로젝트 대화 상자에서이 프로젝트 템플릿을 선택 합니다.

[![](overview/_static/image7.png)](overview/_static/image6.png)

([클릭 하 여 큰 이미지 보기](overview/_static/image8.png))

빈 ASP.NET 웹 응용 프로그램을 만들면 Visual Studio는 다음 폴더의 레이아웃을 만듭니다.

<a id="0.2_graphic1D"></a>![](overview/_static/image9.png)

이 한 가지 예외를 사용 하 여 이전 버전의 ASP.NET 빈 웹 사이트 레이아웃 비슷합니다. Visual Studio 2010에서 빈 웹 응용 프로그램 및 빈 웹 사이트 프로젝트는 최소한 다음 포함 `Web.config` 하는 데 Visual Studio에서 프로젝트 대상으로 하는 프레임 워크를 식별 하는 정보가 포함 된 파일:

<a id="0.2_graphic1E"></a>![](overview/_static/image10.png)

이렇게 하지 않으면 *targetFramework* 속성을 열면 이전 응용 프로그램 호환성을 유지 하기 위해.NET Framework 2.0을 대상으로 하려면 Visual Studio 기본값입니다.

#### <a name="web-application-and-web-site-project-templates"></a>웹 응용 프로그램 및 웹 사이트 프로젝트 템플릿

다른 두 새 프로젝트 템플릿이 Visual Studio 2010과 함께 제공 되는 주요 변경 내용을 포함 합니다. 다음 그림 새 웹 응용 프로그램 프로젝트를 만들 때 생성 되는 프로젝트 레이아웃을 보여 줍니다. (웹 사이트 프로젝트에 대 한 레이아웃은 거의 동일 합니다.)

- <a id="0.2_graphic1F"></a>![](overview/_static/image11.png)

프로젝트는 이전 버전에서 생성 되지 않은 파일의 수를 포함 합니다. 또한 새 웹 응용 프로그램 프로젝트를 빠르게 새 응용 프로그램에 대 한 액세스를 보호 하기 시작할 수 있는 기본 멤버 자격 기능을 사용 하 여 구성 됩니다. 이 포함 되어 있어는 `Web.config` 멤버 자격, 역할 및 프로필 구성에 사용 되는 항목을 포함 하는 새 프로젝트 파일입니다. 다음 예제와 `Web.config` 새 웹 응용 프로그램 프로젝트에 대 한 파일입니다. (이 예에서 *roleManager* 을 사용할 수 없습니다.)

[![](overview/_static/image13.png)](overview/_static/image12.png)

([클릭 하 여 큰 이미지 보기](overview/_static/image14.png))

프로젝트에 두 번째도 포함 되어 있습니다 `Web.config` 파일을 `Account` 디렉터리입니다. 두 번째 구성 파일을 비-로그인 한 사용자에 대 한 ChangePassword.aspx 페이지에 대 한 액세스를 보호 하는 방법을 제공 합니다. 다음 예제에서는 두 번째 내용의 `Web.config` 파일입니다.

![](overview/_static/image15.png)

새 프로젝트 템플릿에 기본적으로 생성 하는 페이지에는 또한 이전 버전 보다 더 많은 내용을 포함 됩니다. 프로젝트 기본 마스터 페이지 및 CSS 파일을 포함 하 고 기본 페이지 (Default.aspx)는 기본적으로 마스터 페이지를 사용 하도록 구성 됩니다. 결과 웹 응용 프로그램 또는 웹 사이트를 처음 실행 하면 기본 (홈) 페이지는 이미 기능. 실제로 새 MVC 응용 프로그램을 시작할 때 표시 된 기본 페이지에 비슷합니다.

[![](overview/_static/image17.png)](overview/_static/image16.png)

([클릭 하 여 큰 이미지 보기](overview/_static/image18.png))

프로젝트 템플릿에 이러한 변경의 의도 새 웹 응용 프로그램 빌드를 시작 하는 방법에 지침을 제공 하는 것입니다. 의미적으로, 엄격한 XHTML 1.0 규격 태그를 사용 하 여 및 CSS를 사용 하 여 지정 된 레이아웃을 사용 하 여 템플릿에 페이지는 ASP.NET 4 웹 응용 프로그램을 구축 하기 위한 모범 사례를 나타냅니다. 기본 페이지를 쉽게 사용자 지정할 수 있는 2 열 레이아웃을 수도 있습니다.

예를 들어 한다고 가정해 보겠습니다 새 웹 응용 프로그램에 대 한 색 중 일부를 변경 하 여 내 ASP.NET 응용 프로그램 로고 대신 회사 로고를 삽입 합니다. 이 작업을 수행 하려면 아래 새 디렉터리를 만들어야 `Content` 로고 이미지를 저장 합니다.

<a id="0.2_graphic23"></a>![](overview/_static/image19.png)

페이지에 이미지를 추가 하려면 다음 엽니다는 `Site.Master` 파일 찾기, 여기서 내 ASP.NET 응용 프로그램 텍스트를 정의로 바꿉니다는 *이미지* 요소입니다 *src* 특성이 새 로고로 설정 된 다음 예제와 같이 이미지:

[![](overview/_static/image21.png)](overview/_static/image20.png)

([클릭 하 여 큰 이미지 보기](overview/_static/image22.png))

그런 다음 Site.css 파일로 이동 하 고 페이지의 배경색 및 헤더를 변경 하는 CSS 클래스 정의 수정할 수 있습니다.

이러한 변경의 결과 다음과 매우 간편 하 게 사용자 지정된 홈 페이지를 표시할 수 있습니다.

[![](overview/_static/image24.png)](overview/_static/image23.png)

([클릭 하 여 큰 이미지 보기](overview/_static/image25.png))

<a id="0.2__Toc253429267"></a><a id="0.2__Toc243304641"></a>

### <a name="css-improvements"></a>향상 된 CSS 기능

ASP.NET 4에는 작업의 주요 영역 중 하나는 최신 HTML 표준을 준수 하는 HTML을 렌더링 하는 데 되었습니다. ASP.NET 웹 서버 컨트롤에서 CSS 스타일을 사용 하는 방법에 대 한 변경 내용이 포함 됩니다.

#### <a name="compatibility-setting-for-rendering"></a>렌더링에 대 한 호환성 설정

기본적으로 웹 응용 프로그램 또는 웹 사이트를.NET Framework 4를 대상으로 하는 경우는 *controlRenderingCompatibilityVersion* 특성을 *페이지* 요소 "4.0"으로 설정 됩니다. 컴퓨터 수준에서이 요소가 정의 `Web.config` 파일과 기본적으로 모든 ASP.NET 4 응용 프로그램에 적용 됩니다.

[!code-xml[Main](overview/samples/sample69.xml)]

에 대 한 값 *controlRenderingCompatibility* 잠재적인 새 버전 정의 이후 릴리스에서 허용 하는 문자열입니다. 현재 릴리스에서 다음 값이이 속성에 대 한 지원 됩니다.

- "3.5". 이 설정은 레거시 렌더링 및 태그를 나타냅니다. 컨트롤에서 렌더링 되는 태그는 100% 호환 및 설정 합니다 *xhtmlConformance* 속성이 적용 됩니다.
- "4.0". 속성에이 설정을 ASP.NET 웹 서버 컨트롤은 다음을 수행 합니다.
- 합니다 *xhtmlConformance* 속성은 항상 "Strict"으로 처리 됩니다. 결과적으로, 컨트롤 XHTML 1.0 Strict 태그를 렌더링합니다.
- 잘못 된 스타일을 렌더링 비 입력 컨트롤을 더 이상 사용 하지 않도록 설정 합니다.
- *div* 숨겨진 필드 요소는 사용자가 만든 CSS 규칙을 사용 하 여 방해 하지 있도록 이제 스타일이 지정 합니다.
- 메뉴 컨트롤에는 의미 체계가 올바르고 내게 필요한 옵션 지침을 사용 하 여 호환 되는 태그를 렌더링 합니다.
- 유효성 검사 컨트롤 인라인 스타일을 렌더링 하지 않습니다.
- 이전에 테두리를 렌더링 하는 제어 = "0" (ASP.NET에서 파생 된 컨트롤 *테이블* 컨트롤과 ASP.NET *이미지* 컨트롤) 더 이상이 특성을 렌더링 합니다.

#### <a name="disabling-controls"></a>컨트롤을 사용 하지 않도록 설정

ASP.NET 3.5 SP1 및 이전 버전의 프레임 워크는 다음과 같이 렌더링 됩니다. 합니다 *사용 하지 않도록 설정* 모든 컨트롤에 대 한 HTML 태그에 특성 *Enabled* 속성이로 설정 *false*합니다. 그러나 HTML 4.01 사양에 따라 *입력* 요소에는이 특성이 있어야 합니다.

ASP.NET 4에서 설정할 수 있습니다 합니다 *controlRenderingCompatabilityVersion* "3.5" 다음 예제와 같이 속성:

[!code-xml[Main](overview/samples/sample70.xml)]

에 대 한 태그를 만들 수 있습니다는 *레이블* 컨트롤을 사용 하지 않도록 설정 하는 다음과 같은 제어 합니다.

[!code-aspx[Main](overview/samples/sample71.aspx)]

합니다 *레이블* 제어는 다음 HTML을 렌더링 합니다.

[!code-html[Main](overview/samples/sample72.html)]

ASP.NET 4에서 설정할 수 있습니다 합니다 *controlRenderingCompatabilityVersion* "4.0"입니다. 이 경우 렌더링 되는 제어 *입력* 요소가 렌더링 됩니다는 *사용 하지 않도록 설정* 때 특성 컨트롤의 *사용* 속성이 *false* . HTML 렌더링 되지 않는 컨트롤 *입력* 요소 대신 렌더링을 *클래스* 컨트롤에 대 한 비활성화 된 모양을 정의 하는 데 사용할 수 있는 CSS 클래스를 참조 하는 특성입니다. 예를 들어 합니다 *레이블* 앞의 예제에 표시 되는 컨트롤은 다음 태그를 생성 합니다.

[!code-html[Main](overview/samples/sample73.html)]

이 컨트롤에 대해 지정 하는 클래스에 대 한 기본값은 "aspNetDisabled"입니다. 그러나 정적 설정 하 여이 기본값을 변경할 수 있습니다 *DisabledCssClass* 의 정적 속성을 *WebControl* 클래스입니다. 컨트롤 개발자에 게 특정 컨트롤에 사용할 동작을 정의할 수도 있습니다를 사용 하 여 *SupportsDisabledAttribute* 속성입니다.

<a id="0.2__Toc253429268"></a><a id="0.2__Toc243304642"></a>

### <a name="hiding-div-elements-around-hidden-fields"></a>Div 숨겨진 필드 주위 요소 숨기기

ASP.NET 2.0 및 이후 버전에는 시스템 관련 숨겨진된 필드 렌더링 (같은 합니다 *숨겨진* 뷰 상태 정보를 저장 하는 데 사용 되는 요소) 내 *div* XHTML 표준을 준수 하기 위해 요소입니다. 그러나 CSS 규칙을 적용 하면 문제가 발생할 수 있습니다이 *div* 페이지의 요소입니다. 예를 들어 페이지에 표시 되는 1 픽셀 줄에서 발생할 수 있습니다 약 숨겨진 *div* 요소입니다. ASP.NET 4에서 *div* ASP.NET에서 생성 된 숨겨진된 필드를 포함 하는 요소는 다음 예제와 같이 CSS 클래스 참조를 추가 합니다.

[!code-html[Main](overview/samples/sample74.html)]

다음에 적용 되는 CSS 클래스를 정의할 수 있습니다 합니다 *숨겨진* 다음 예제와 같이 ASP.NET에서 생성 되는 요소:

[!code-css[Main](overview/samples/sample75.css)]

<a id="0.2__Toc253429269"></a><a id="0.2__Toc243304643"></a>

### <a name="rendering-an-outer-table-for-templated-controls"></a>템플릿 기반 컨트롤에 대 한 외부 테이블을 렌더링

기본적으로 템플릿을 지 원하는 다음 ASP.NET 웹 서버 컨트롤은 인라인 스타일을 적용 하는 데 사용 되는 외부 테이블에 자동으로 줄:

- *FormView*
- *로그인*
- *PasswordRecovery*
- *ChangePassword*
- *마법사*
- *CreateUserWizard*

라는 새 속성을 *RenderOuterTable* 태그에서 제거할 외부 테이블을 허용 하는 이러한 컨트롤에 추가 되었습니다. 예를 들어 다음 예제는 *FormView* 제어 합니다.

[!code-aspx[Main](overview/samples/sample76.aspx)]

이 태그에 다음 출력을 HTML 테이블을 포함 하는 페이지를 렌더링 합니다.

[!code-html[Main](overview/samples/sample77.html)]

테이블을 렌더링 되지 않도록 방지 하려면 설정할 수 있습니다 합니다 *FormView* 컨트롤의 *RenderOuterTable* 다음 예제와 같이 속성:

[!code-aspx[Main](overview/samples/sample78.aspx)]

앞의 예제 출력을 하지 않고 다음 렌더링 합니다 *테이블*를 *tr*, 및 *td* 요소:

> 콘텐츠


이 향상 된이 기능 수 쉽게 스타일 CSS 사용 하 여 컨트롤의 콘텐츠 컨트롤에 의해 예기치 않은 태그가 렌더링 되기 때문에 있습니다.

> [!NOTE]
> 이 변경 때문에 더 이상 Visual Studio 2010 디자이너에서 자동 format 함수에 대 한 지원을 사용 하지 않도록 설정 하는 참고를 *테이블* 자동 서식 옵션에 의해 생성 되는 스타일 특성을 호스트할 수 있는 요소입니다.


<a id="0.2__Toc253429270"></a><a id="0.2__Toc243304644"></a>

### <a name="listview-control-enhancements"></a>향상 된 ListView 컨트롤

합니다 *ListView* 컨트롤 내용이 ASP.NET 4에서 사용 하기 쉽습니다. 컨트롤의 이전 버전 알려진 id 서버 컨트롤을 포함 하는 레이아웃 템플릿을 지정 하는 데 필요한 다음 태그를 사용 하는 방법의 일반적인 예제는 *ListView* ASP.NET 3.5에서 컨트롤입니다.

[!code-aspx[Main](overview/samples/sample79.aspx)]

ASP.NET 4에는 *ListView* 컨트롤의 레이아웃 템플릿이 필요가 없습니다. 이전 예에서 같이 태그에 다음 태그를 사용 하 여 바꿀 수 있습니다.

[!code-aspx[Main](overview/samples/sample80.aspx)]

<a id="0.2__Toc253429271"></a><a id="0.2__Toc243304645"></a>

### <a name="checkboxlist-and-radiobuttonlist-control-enhancements"></a>CheckBoxList 및 RadioButtonList 컨트롤 향상 된 기능

ASP.NET 3.5에서에 대 한 레이아웃을 지정할 수 있습니다 합니다 *CheckBoxList* 하 고 *RadioButtonList* 다음 두 설정을 사용 하 여:

- *흐름*합니다. 컨트롤 렌더링 *걸쳐* 해당 콘텐츠를 포함 하는 요소입니다.
- *테이블*합니다. 컨트롤 렌더링을 *테이블* 해당 콘텐츠를 포함 하는 요소입니다.

다음 예제에서는 이러한 각 컨트롤에 대 한 태그를 보여 줍니다.

[!code-aspx[Main](overview/samples/sample81.aspx)]

기본적으로 컨트롤을 렌더링 HTML 다음과 비슷합니다.

[!code-html[Main](overview/samples/sample82.html)]

HTML 목록을 사용 하 여 해당 콘텐츠를 렌더링 해야 이러한 컨트롤 의미적으로 HTML을 렌더링 하기 위한 항목 목록이 포함 되어 있으므로 (*li*) 요소입니다. 이렇게 하면 보조 기술을 사용 하 여 웹 페이지를 읽고 컨트롤을 더 쉽게 CSS를 사용 하 여 스타일을 사용자에 대해 쉽게 합니다.

ASP.NET 4에는 *CheckBoxList* 및 *RadioButtonList* 컨트롤에 대 한 다음 새 값을 지원 합니다 *RepeatLayout* 속성:

- *OrderedList* –으로 콘텐츠를 렌더링할 *li* 내에서 요소를 *ol* 요소입니다.
- *UnorderedList* –으로 콘텐츠를 렌더링할 *li* 내에서 요소를 *ul* 요소입니다.

다음 예제에서는 이러한 새 값을 사용 하는 방법을 보여 줍니다.

[!code-aspx[Main](overview/samples/sample83.aspx)]

위의 태그는 다음 HTML을 생성합니다.

[!code-html[Main](overview/samples/sample84.html)]

> [!NOTE]
> 설정 하는 경우 *RepeatLayout* 하 *OrderedList* 또는 *UnorderedList*서 *RepeatDirection* 속성이 더 이상 사용할 수 있으며 됩니다 태그 또는 코드 내에서 속성을 설정한 경우 런타임 시 예외를 throw 합니다. CSS를 대신 사용 하 여 이러한 컨트롤의 시각적 레이아웃 정의 되어 있으므로 속성 값이 없는 것입니다.


<a id="0.2__Toc253429272"></a><a id="0.2__Toc243304646"></a>

### <a name="menu-control-improvements"></a>메뉴 제어 기능 향상

ASP.NET 4 이전 합니다 *메뉴* 컨트롤이 일련의 HTML 테이블을 렌더링 합니다. 이 인라인 속성을 설정 하는 외부 CSS 스타일을 적용 하는 것이 어려울 수 및 없습니다. 또한 접근성 표준을 준수 합니다.

ASP.NET 4에서 컨트롤이 이제 순서 없는 목록 및 목록 요소 구성 된 의미 체계 태그를 사용 하 여 HTML을 렌더링 합니다. 다음 예제에 대 한 ASP.NET 페이지에서 태그를 보여 줍니다.는 *메뉴* 제어 합니다.

[!code-aspx[Main](overview/samples/sample85.aspx)]

페이지가 렌더링 하는 경우 컨트롤은 다음 HTML을 생성 하는 (합니다 *onclick* 코드 명확성을 위해 생략 됨):

[!code-html[Main](overview/samples/sample86.html)]

렌더링 향상 된 메뉴의 키보드 탐색 기능이 향상 되었습니다 포커스 관리를 사용 하 여. 경우는 *메뉴* 컨트롤이 포커스를 받으면, 화살표 키를 사용 하 여 요소를 이동할 수 있습니다. *메뉴* 제어도 액세스할 수 있는 풍부한 인터넷 응용 프로그램 (ARIA) 역할을 연결 및 함 특성[wing 합니다](http://www.w3.org/TR/wai-aria-practices/#menu "메뉴 ARIA 지침")개선 내게 필요한 옵션입니다.

메뉴 컨트롤에 대 한 스타일을 스타일 블록의 맨 위에 있는 페이지 대신 렌더링 된 HTML 요소에 따라 렌더링 됩니다. 컨트롤의 스타일을 통해 완전 한 제어 하려는 경우 설정할 수 있습니다 새 *IncludeStyleBlock* 속성을 *false*, 스타일 블록을 내보내지 않는 경우. 이 속성을 사용 하는 한 가지 방법은 메뉴의 모양을 설정 하는 Visual Studio 디자이너에서 자동 서식 기능을 사용 하는 것입니다. 다음 페이지를 실행, 페이지 원본을 열고 렌더링된 스타일 블록 외부 CSS 파일에 복사 합니다. Visual Studio의 스타일 지정 및 집합 실행 취소 *IncludeStyleBlock* 하 *false*합니다. 결과 메뉴가 표시 스타일을 사용 하 여 외부 스타일 시트에 정의 됩니다.

<a id="0.2__Toc253429273"></a><a id="0.2__Toc243304647"></a>

### <a name="wizard-and-createuserwizard-controls"></a>마법사 및 CreateUserWizard 컨트롤

ASP.NET *마법사* 하 고 *CreateUserWizard* 컨트롤을 렌더링 하는 HTML을 정의할 수 있는 템플릿을 지원 합니다. (*CreateUserWizard* 에서 파생 되 *마법사*.) 다음 예제에서는 완전히 템플릿 기반 태그를 보여 줍니다 *CreateUserWizard* 제어 합니다.

[!code-aspx[Main](overview/samples/sample87.aspx)]

컨트롤 다음과 유사한 HTML을 렌더링합니다.

[!code-html[Main](overview/samples/sample88.html)]

ASP.NET 3.5 sp1의 경우 템플릿 내용을 변경할 수 있지만 여전히 제한의 출력을 제어 합니다 *마법사* 제어 합니다. ASP.NET 4에서 만들 수 있습니다를 *LayoutTemplate* 템플릿과 삽입 *자리 표시자* 방법을 지정할 수 있습니다 (예약 된 이름 사용)을 제어 합니다 *마법사 컨트롤* 렌더링 하 합니다. 다음 예제에서는이 보여 줍니다.

[!code-aspx[Main](overview/samples/sample89.aspx)]

명명 된 자리 표시자에 다음을 포함 하는 예제는 *LayoutTemplate* 요소:

- *headerPlaceholder* – 런타임 시이 바뀝니다 내용의 합니다 *머리글 템플릿의* 요소입니다.
- *sideBarPlaceholder* – 런타임 시이 바뀝니다 내용의 합니다 *SideBarTemplate* 요소입니다.
- *wizardStepPlaceHolder* – 런타임 시이 바뀝니다 내용의 합니다 *WizardStepTemplate* 요소입니다.
- *navigationPlaceholder* – 런타임 시 정의 된 모든 탐색 템플릿에서 대체 됩니다이 있습니다.

자리 표시자를 사용 하는 예제 태그 (실제로 템플릿에 정의 된 콘텐츠) 없이 다음 HTML을 렌더링 합니다.

[!code-html[Main](overview/samples/sample90.html)]

이제 정의 되지 않은 사용자-만 HTML이를 *걸쳐* 요소입니다. (릴리스에서 향후 예정 아무리 *s p a n* 요소 렌더링 되지 것입니다.) 이 구문은 이제에서 생성 되는 거의 모든 콘텐츠에 대 한 전체 권한을 제공 합니다 *마법사* 제어 합니다.

<a id="0.2_dyndata"></a><a id="0.2__Toc253429274"></a><a id="0.2__Toc243304648"></a><a id="0.2__Toc224729042"></a>

## <a name="aspnet-mvc"></a>ASP.NET MVC

ASP.NET MVC 2009 년 3 월에에서는 추가 기능 프레임 워크로 ASP.NET 3.5 SP1에 도입 되었습니다. Visual Studio 2010 새로운 특징과 기능을 포함 하는 ASP.NET MVC 2를 포함 합니다.

<a id="0.2__Toc253429275"></a>

### <a name="areas-support"></a>영역 지원

영역을 사용 하면 다른 섹션에서 상대 격리에서 많은 응용 프로그램의 섹션으로 그룹 컨트롤러 및 보기. 각 영역으로 주 응용 프로그램에서 참조 될 수 있는 별도 ASP.NET MVC 프로젝트를 구현할 수 있습니다. 이 대규모 응용 프로그램을 빌드할 때 복잡성을 관리 하는 데 도움이 됩니다 하 고 쉽게 여러 팀이 단일 응용 프로그램에서 함께 작동 합니다.

<a id="0.2__Toc253429276"></a>

### <a name="data-annotation-attribute-validation-support"></a>데이터 주석 특성의 유효성 검사 지원

*DataAnnotations* 특성 메타 데이터 특성을 사용 하 여 모델에 유효성 검사 논리를 연결할 수 있습니다. *DataAnnotations* 특성 ASP.NET Dynamic Data ASP.NET 3.5 sp1에서에서 도입 되었습니다. 이러한 특성은 기본 모델 바인더에 통합 되었습니다 및 사용자 입력의 유효성을 검사 하는 메타 데이터 기반 방법을 제공 합니다.

<a id="0.2__Toc253429277"></a>

### <a name="templated-helpers"></a>템플릿 기반 도우미

자동으로 연결 편집 수 하 고 데이터 형식을 사용 하 여 템플릿을 표시 하는 템플릿 기반 도우미입니다. 예를 들어, 날짜 선택 UI 요소에 대해 자동으로 렌더링 되는 지정 하는 템플릿 도우미를 사용할 수 있습니다는 *System.DateTime* 값입니다. ASP.NET Dynamic Data에 필드 템플릿에 것과 비슷합니다.

합니다 *Html.EditorFor* 하 고 *Html.DisplayFor* 여러 속성을 사용 하 여도 복잡 한 개체 형식 표준 데이터 렌더링에 대 한 도우미 메서드는 기본 제공 지원. 또한 렌더링을 사용자 지정 데이터 주석 특성을 적용할 수 있도록 하 여 *DisplayName* 하 고 *ScaffoldColumn* 에 *ViewModel* 개체입니다.

종종 하려는 UI 도우미 더욱에서 출력을 사용자 지정 및 완전히 제어 생성 됩니다. 합니다 *Html.EditorFor* 하 고 *Html.DisplayFor* 도우미 메서드를 지원이 재정의할 수 있는 외부 템플릿과 컨트롤 렌더링 된 출력을 정의할 수 있는 템플릿 메커니즘을 사용 하 여 합니다. 템플릿은 클래스에 대해 개별적으로 렌더링할 수 있습니다.

<a id="0.2__Toc253429278"></a><a id="0.2__Toc243304649"></a>

## <a name="dynamic-data"></a>Dynamic Data

동적 데이터 도입 2008 년 중순에.NET Framework 3.5 SP1 릴리스에서 합니다. 이 기능은 다음을 포함 하는 데이터 기반 응용 프로그램에 대 한 많은 향상 된 기능을 제공 합니다.

- 데이터 기반 웹 사이트를 신속 하 게 빌드하기 위한 RAD 환경.
- 데이터 모델에 정의 된 제약 조건을 기반으로 하는 자동 유효성 검사
- 필드에 대해 생성 되는 태그를 쉽게 변경할 수는 *GridView* 하 고 *DetailsView* 동적 데이터 프로젝트의 일부인 필드 템플릿을 사용 하 여 컨트롤입니다.

> [!NOTE]
> 자세한 내용은 참고를 참조 하십시오 합니다 [동적 데이터 설명서](https://msdn.microsoft.com/library/cc488545.aspx) MSDN 라이브러리에서.


ASP.NET 4에 대 한 동적 데이터 신속 하 게 데이터 기반 웹 사이트를 구축 하기 위한 개발자에 게 더 많은 기능을 제공 하도록 향상 되었습니다.

<a id="0.2__Toc253429279"></a><a id="0.2__Toc243304650"></a>

### <a name="enabling-dynamic-data-for-existing-projects"></a>기존 프로젝트에 대 한 동적 데이터를 사용 하도록 설정

.NET Framework 3.5 SP1에서 제공 되는 동적 데이터 기능 상태가 다음과 같은 새로운 기능:

- 필드 템플릿 – 데이터 바인딩된 컨트롤에 대 한 데이터 형식을 기반 템플릿을 제공합니다. 필드 템플릿을 템플릿 필드를 사용 하 여 각 필드에 대 한 보다 데이터 컨트롤의 모양을 사용자 지정 하는 간단한 방법을 제공 합니다.
- 유효성 검사 – 동적 데이터에서 사용할 수 있습니다 특성 데이터 클래스 필수 필드, 범위 검사, 형식 검사, 패턴 일치, 정규식을 사용 하 여 일반적인 시나리오에 대 한 유효성 검사 및 사용자 지정 유효성 검사를 지정 합니다. 유효성 검사는 데이터 컨트롤에 의해 적용 됩니다.

그러나 이러한 기능에는 다음 요구 사항이 있었습니다.

- Entity Framework 또는 LINQ to SQL 기반으로 하는 데이터 액세스 계층이 했습니다.
- 유일한 데이터 소스 컨트롤과 이러한 기능에 대해 지원 되는 *EntityDataSource* 또는 *LinqDataSource* 컨트롤입니다.
- 기능에는 기능을 지원 해야 하는 모든 파일을 위해서는 동적 데이터 또는 동적 데이터 엔터티 템플릿을 사용 하 여 만든 웹 프로젝트를 필요 합니다.

ASP.NET 4에서 동적 데이터 지원의 주요 목표는 모든 ASP.NET 응용 프로그램에 대 한 동적 데이터의 새 기능. 다음 예제에서는 기존 페이지에 Dynamic Data 기능을 사용할 수 있는 컨트롤에 대 한 태그를 보여 줍니다.

[!code-aspx[Main](overview/samples/sample91.aspx)]

페이지에 대 한 코드에서 이러한 컨트롤에 대 한 동적 데이터 지원을 사용 하도록 설정 하려면 다음 코드를 추가 합니다.

[!code-csharp[Main](overview/samples/sample92.cs)]

경우는 *GridView* 컨트롤이 편집 모드 인지, 동적 데이터를 자동으로 입력 한 데이터가 올바른 형식 인지 확인 합니다. 없는 경우 오류 메시지가 표시 됩니다.

이 기능에도 다른 이점이, 값 삽입 모드 등 기본값을 지정할 수 있습니다. 동적 데이터 없이 필드에 대해 기본값을 구현 해야 합니다 이벤트에 연결 하십시오 컨트롤을 찾습니다 (사용 하 여 *FindControl*), 해당 값을 설정 합니다. ASP.NET 4에서 합니다 *EnableDynamicData* 호출이 예와에서 같이 개체에서 모든 필드에 대 한 기본 값을 전달할 수 있도록 하는 두 번째 매개 변수를 지원 합니다.

[!code-csharp[Main](overview/samples/sample93.cs)]

<a id="0.2__Toc224729043"></a><a id="0.2__Toc253429280"></a><a id="0.2__Toc243304651"></a>

### <a name="declarative-dynamicdatamanager-control-syntax"></a>DynamicDataManager 컨트롤 선언 구문

합니다 *DynamicDataManager* 선언적으로 구성할 수 있도록 제어 기능이 향상 되었습니다 마찬가지로 코드에서 하는 대신 ASP.NET에서 대부분의 컨트롤입니다. 에 대 한 태그를 *DynamicDataManager* 컨트롤은 다음 예제와 같습니다.

[!code-aspx[Main](overview/samples/sample94.aspx)]

이 태그에서 참조 되는 GridView1 컨트롤에 대 한 동적 데이터 동작을 활성화 합니다 *다음* 부분을 *DynamicDataManager* 컨트롤.

<a id="0.2__Toc224729044"></a><a id="0.2__Toc253429281"></a><a id="0.2__Toc243304652"></a>

### <a name="entity-templates"></a>엔터티 템플릿

엔터티 템플릿을 사용자 지정 페이지 할 필요 없이 데이터의 레이아웃을 사용자 지정 하는 새로운 방법을 제공 합니다. 템플릿을 사용 하 여 페이지의 *FormView* 컨트롤 (대신 합니다 *DetailsView* 동적 데이터의 이전 버전의 페이지 템플릿에서 사용 되는 컨트롤) 및 *DynamicEntity* 엔터티 템플릿이 렌더링 될 컨트롤입니다. Dynamic Data에서 렌더링 되는 태그를 자세한 제어할 수 있습니다.

다음은 엔터티 템플릿이 포함 된 새 프로젝트 디렉터리 레이아웃을 보여 줍니다.

[!code-console[Main](overview/samples/sample95.cmd)]

`EntityTemplate` 디렉터리 데이터 모델 개체를 표시 하는 방법에 대 한 템플릿을 포함 합니다. 기본적으로 개체를 사용 하 여 렌더링 됩니다는 `Default.ascx` 에서 만든 태그 처럼 보이는 태그를 제공 하는 템플릿 합니다 *DetailsView* ASP.NET 3.5 SP1에 Dynamic Data에서 사용 되는 컨트롤입니다. 다음 예제에서는 태그를 보여 줍니다.는 `Default.ascx` 제어 합니다.

[!code-aspx[Main](overview/samples/sample96.aspx)]

전체 사이트에 대 한 디자인을 변경 하려면 기본 템플릿은 편집할 수 있습니다. 표시, 편집 및 삽입 작업에 대 한 템플릿이 있습니다. 새 템플릿은 추가할 수 있습니다 데이터 개체의 이름에 따라 한 가지 유형의 개체의 모양과 느낌을 변경 하려면. 예를 들어 다음 템플릿을 추가할 수 있습니다.

[!code-console[Main](overview/samples/sample97.cmd)]

서식 파일에 다음 태그를 포함할 수 있습니다.

[!code-aspx[Main](overview/samples/sample98.aspx)]

새 엔터티 템플릿을 새을 사용 하 여 페이지에 표시 됩니다 *DynamicEntity* 제어 합니다. 런타임 시이 컨트롤은 엔터티 템플릿의 내용으로 대체 됩니다. 에서는 다음 태그를 *FormView* 에서 제어할는 `Detail.aspx` 엔터티 템플릿을 사용 하는 페이지 템플릿. 알림 합니다 *DynamicEntity* 태그의 요소에에서 있습니다.

[!code-aspx[Main](overview/samples/sample99.aspx)]

<a id="0.2__Toc224729045"></a><a id="0.2__Toc253429282"></a><a id="0.2__Toc243304653"></a>

### <a name="new-field-templates-for-urls-and-email-addresses"></a>Url 및 전자 메일 주소에 대 한 새 필드 템플릿

ASP.NET 4에서는 두 가지 새로운 기본 제공 필드 템플릿 `EmailAddress.ascx` 고 `Url.ascx`입니다. 로 표시 된 필드에 대 한 이러한 템플릿을 사용 하 *EmailAddress* 또는 *Url* 사용 하 여 합니다 *DataType* 특성입니다. 에 대 한 *EmailAddress* 개체를 사용 하 여 만든 하이퍼링크로 필드가 표시 되는 *mailto:* 프로토콜입니다. 사용자가 링크를 클릭 하는 경우 사용자의 전자 메일 클라이언트 열리고 기본 메시지를 만듭니다. 로 형식화 된 개체가 *Url* 일반 하이퍼링크로 표시 됩니다.

다음 예에서는 필드는 표시 하는 방법을 보여 줍니다.

[!code-csharp[Main](overview/samples/sample100.cs)]

<a id="0.2__Toc224729046"></a><a id="0.2__Toc253429283"></a><a id="0.2__Toc243304654"></a>

### <a name="creating-links-with-the-dynamichyperlink-control"></a>DynamicHyperLink 컨트롤을 사용 하 여 링크 만들기

동적 데이터 웹 사이트에 액세스할 때 최종 사용자에 게 표시 되는 Url을 제어 하려면.NET Framework 3.5 SP1에 추가 된 새로운 라우팅 기능을 사용 합니다. 새 *DynamicHyperLink* 컨트롤을 사용 하면 쉽게 Dynamic Data 사이트의 페이지에 대 한 링크를 빌드할 수 있습니다. 다음 예제에서는 사용 하는 방법을 보여 줍니다 합니다 *DynamicHyperLink* 제어 합니다.

[!code-aspx[Main](overview/samples/sample101.aspx)]

이 태그에 대 한 목록 페이지를 가리키는 링크를 만듭니다는 `Products` 테이블에 정의 된 경로에 따라는 `Global.asax` 파일입니다. 컨트롤에는 자동으로 동적 데이터 페이지를 기반으로 하는 기본 테이블 이름을 사용 합니다.

<a id="0.2__Toc224729047"></a><a id="0.2__Toc253429284"></a><a id="0.2__Toc243304655"></a>

### <a name="support-for-inheritance-in-the-data-model"></a>데이터 모델의 상속에 대 한 지원

Entity Framework 및 LINQ to SQL 해당 데이터 모델에서 상속을 지원합니다. 이 예가 포함 된 데이터베이스 수는 `InsurancePolicy` 테이블입니다. 포함할 수도 있습니다 `CarPolicy` 하 고 `HousePolicy` 와 동일한 필드가 있는 테이블 `InsurancePolicy` 다음 더 많은 필드를 추가 합니다. 동적 데이터 데이터 모델에서 상속 된 개체를 이해 하 고 상속된 된 테이블에 대 한 스 캐 폴딩을 지원 하도록 수정 되었습니다.

<a id="0.2__Toc224729048"></a><a id="0.2__Toc253429285"></a><a id="0.2__Toc243304656"></a>

### <a name="support-for-many-to-many-relationships-entity-framework-only"></a>다 대 다 관계 (Entity Framework에만 해당)에 대 한 지원

Entity Framework에서 컬렉션으로 관계를 노출 하 여 구현 되는 테이블 간에 다 대 다 관계에 대 한 다양 한 지원에는 *엔터티* 개체입니다. 새 `ManyToMany.ascx` 고 `ManyToMany_Edit.ascx` 필드 템플릿을 추가한 다 대 다 관계에 관련 된 데이터 표시 및 편집에 대 한 지원을 제공 합니다.

<a id="0.2__Toc224729049"></a><a id="0.2__Toc253429286"></a><a id="0.2__Toc243304657"></a>

### <a name="new-attributes-to-control-display-and-support-enumerations"></a>컨트롤 표시 및 지원 열거형에 새 특성

합니다 *DisplayAttribute* 통해 추가 필드가 표시 되는 방식을 제어할 수에 추가 되었습니다. 합니다 *DisplayName* 특성이 이전 버전의 동적 데이터 필드에 대 한 캡션으로 사용 되는 이름을 변경할 수 있습니다. 새 *DisplayAttribute* 클래스 필드를 필터로 사용 되는 필드를 사용할지 여부 및 필드가 표시 되는 순서와 같은 표시 옵션을 추가로 지정할 수 있습니다. 제공 독립적으로 제어의 레이블 지정에 사용 되는 이름 특성을 *GridView* 컨트롤에 사용할 이름을 *DetailsView* 필드 도움말 텍스트를 제어 및 워터 마크에 사용 되는 필드 (필드는 텍스트 입력을 받아들이는) 경우입니다.

합니다 *EnumDataTypeAttribute* 열거형 필드를 매핑할 수 있도록 클래스가 추가 되었습니다. 필드에이 특성을 적용 하면 열거형 형식을 지정 합니다. 동적 데이터를 사용 하 여 새 `Enumeration.ascx` 필드 템플릿을 표시 하 고 열거형 값을 편집에 대 한 UI를 만듭니다. 템플릿을은 열거형의 이름에는 데이터베이스에서 값을 매핑합니다.

<a id="0.2__Toc224729050"></a><a id="0.2__Toc253429287"></a><a id="0.2__Toc243304658"></a>

### <a name="enhanced-support-for-filters"></a>필터에 대 한 향상 된 지원

동적 데이터 1.0 부울 열과 외래 키 열에 대 한 기본 제공 필터를 사용 하 여 제공 합니다. 필터 여부를 표시 하기 또는 표시 된 순서에서 지정을 허용 하지 않았습니다. 새 *DisplayAttribute* 특성 주소 둘 다 제공 하 여 이러한 문제의 열 필터로 표시 되는지 여부 제어 및 순서에 표시 됩니다.

추가 향상은 필터링 지원 되었는지 다시[새 쓸](#0.2__QueryExtender "_QueryExtender") Web Forms의 기능입니다. 이 필터를 사용 하 여 사용할 데이터 소스 컨트롤에 대 한 지식이 필요 없이 필터를 만들 수 있습니다. 이러한 확장과 함께 필터도이 켜진 템플릿 컨트롤에 새 템플릿을 추가할 수 있습니다. 마지막으로, 합니다 *DisplayAttribute* 앞에서 언급 한 클래스를 통해 동일한 재정의 되도록 기본 필터 방식으로 *UIHint* 를 재정의할 수 열에 대 한 기본 필드 템플릿을 허용 합니다.

<a id="0.2__Toc224729051"></a><a id="0.2__Toc253429288"></a><a id="0.2__Toc243304659"></a>

## <a name="visual-studio-2010-web-development-improvements"></a>Visual Studio 2010 웹 개발 향상

Visual Studio 2010의 웹 개발 큰 CSS 호환성을 위해 HTML 및 ASP.NET 태그 조각 및 새 동적 IntelliSense JavaScript를 통해 향상 된 생산성 향상 되었습니다.

<a id="0.2__Toc224729052"></a><a id="0.2__Toc253429289"></a><a id="0.2__Toc243304660"></a>

### <a name="improved-css-compatibility"></a>향상 된 CSS 호환성

Visual Studio 2010의 Visual Web Developer 디자이너를 사용 하는 CSS 2.1 표준 준수를 개선 하기 위해 업데이트 되었습니다. 더 잘 디자이너 HTML 소스의 무결성을 유지 하 고 이전 버전의 Visual Studio 보다 더 강력 합니다. 내부적으로 아키텍처도 향상 되었습니다 렌더링, 레이아웃 및 효율성의 이후 향상 기능을 향상 하도록 해당 됩니다.

<a id="0.2__Toc224729053"></a><a id="0.2__Toc253429290"></a><a id="0.2__Toc243304661"></a>

### <a name="html-and-javascript-snippets"></a>HTML 및 JavaScript 코드 조각

HTML 편집기에서 IntelliSense 자동 완성 태그 이름입니다. IntelliSense 코드 조각 기능을 자동으로 완성 전체 태그 등입니다. Visual Studio 2010과 함께 C# 및 Visual Basic, Visual Studio의 이전 버전에서 지원 되므로 JavaScript 용 IntelliSense 코드 조각 지원 됩니다.

Visual Studio 2010에는 자동 완성 일반적인 ASP.NET 및 HTML 태그를 필수 특성을 포함 하 여 도움이 되는 200 개 이상의 조각이 포함 되어 있습니다. (같은 runat = "server") 및 태그에 특정 공통 특성 (같은 *ID*,  *DataSourceID*하십시오 *ControlToValidate*, 및 *텍스트*).

추가 코드 조각을 다운로드 하거나 일반적인 작업에 대 한 사용자 또는 팀을 사용 하는 태그의 요소를 캡슐화 하는 사용자 고유의 코드 조각을 작성할 수 있습니다.

<a id="0.2__Toc224729054"></a><a id="0.2__Toc253429291"></a><a id="0.2__Toc243304662"></a>

### <a name="javascript-intellisense-enhancements"></a>JavaScript IntelliSense 향상 된 기능

Visual 2010에서는 JavaScript IntelliSense는 풍부한 편집 환경을 제공 하기 위해 다시 디자인 되었습니다. IntelliSense는 이제 동적으로 생성 된 메서드에서 같은 개체 인식 *registerNamespace* 및 다른 JavaScript 프레임 워크에서 사용 하는 비슷한 기술을 통해. 스크립트의 대규모 라이브러리를 분석 하 고 IntelliSense를 거의 또는 전혀 처리 지연 표시 성능이 향상 되었습니다. 거의 모든 타사 라이브러리를 지원 하 고 다양 한 코딩 스타일을 지원 하도록 호환성 크게 증가 되었습니다. 문서 주석은 입력 하 고 IntelliSense에서 즉시 활용은 이제 구문 분석 됩니다.

<a id="0.2__Toc224729055"></a><a id="0.2__Toc253429292"></a><a id="0.2__Toc243304663"></a>

## <a name="web-application-deployment-with-visual-studio-2010"></a>Visual Studio 2010을 사용한 웹 응용 프로그램 배포

ASP.NET 개발자는 웹 응용 프로그램을 배포 하는 경우 종종 어려워하는 다음과 같은 문제가 발생 하 합니다.

- 공유 호스팅 사이트 배포 속도가 느려질 수 있습니다는 FTP와 같은 기술 필요 합니다. 또한 수동으로 데이터베이스를 구성 하는 SQL 스크립트 실행과 같은 작업을 수행 해야 하 고 응용 프로그램으로 가상 디렉터리 폴더를 구성 하는 등의 IIS 설정을 변경 해야 합니다.
- 엔터프라이즈 환경에서 웹 응용 프로그램 파일을 배포 하는 것 외에도 관리자 자주 수정 해야 ASP.NET 구성 파일과 IIS 설정 합니다. 데이터베이스 관리자는 일련의 실행 중인 응용 프로그램 데이터베이스를 가져오려면 SQL 스크립트를 실행 해야 합니다. 이러한 설치는 많은 수동 작업, 완료 하는 데 시간이 걸릴 신중 하 게 문서화 해야 합니다.

Visual Studio 2010에는 이러한 문제를 해결 하 고 웹 응용 프로그램에 원활 하 게 배포할 수 있는 기술이 포함 되어 있습니다. 이러한 기술 중 하나에서 IIS 웹 배포 도구 (MsDeploy.exe)입니다.

Visual Studio 2010의 웹 배포 기능에는 다음 주요 영역이 포함 됩니다.

- 웹 패키징
- Web.config 변환
- 데이터베이스 배포
- 웹 응용 프로그램에 대 한 one-click 게시

다음 섹션에서는 이러한 기능에 대 한 세부 정보를 제공 합니다.

<a id="0.2__Toc224729056"></a><a id="0.2__Toc253429293"></a><a id="0.2__Toc243304664"></a>

### <a name="web-packaging"></a>웹 패키징

Visual Studio 2010 MSDeploy 도구를 사용 하 여 응용 프로그램 이라고 하는 압축된 (.zip) 파일을 만들 하는 *웹 패키지*합니다. 다음 콘텐츠 및 응용 프로그램에 대 한 메타 데이터를 포함 하는 패키지 파일:

- 응용 프로그램 풀 설정, 오류 페이지 설정 및 등을 포함 하는 IIS 설정입니다.
- 실제 웹 콘텐츠를 웹 페이지, 사용자 컨트롤, 정적 콘텐츠 (이미지 및 HTML 파일) 및 등을 포함 합니다.
- SQL Server 데이터베이스 스키마 및 데이터입니다.
- 보안 인증서, GAC, 레지스트리 설정에서 설치할 구성 요소입니다.

웹 패키지를 서버에 복사 하 고 IIS 관리자를 사용 하 여 수동으로 설치할 수 있습니다. 또는, 자동화 된 배포 패키지 또는 설치할 수 있습니다 명령줄 명령을 사용 하 여 배포 Api를 사용 하 여 합니다.

MSBuild 작업 및 대상 웹 패키지를 만드는 기본 제공 visual Studio 2010 제공 합니다. 자세한 내용은 [ASP.NET 웹 응용 프로그램 프로젝트 배포 개요](https://msdn.microsoft.com/library/dd394698%28VS.100%29.aspx) MSDN 웹 사이트에서 및 [웹 패키지를 만들어야 하는 10 + 20 이유](http://vishaljoshi.blogspot.com/2009/07/10-20-reasons-why-you-should-create-web.html) 인 Vishal Joshi의 블로그입니다.

<a id="0.2__Toc224729057"></a><a id="0.2__Toc253429294"></a><a id="0.2__Toc243304665"></a>

### <a name="webconfig-transformation"></a>Web.config 변환

Visual Studio 2010 웹 응용 프로그램 배포에 대 한 소개 [문서 변환 XDT (XML)](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html)을 변형할 수 있는 기능인는 `Web.config` 개발 설정에서 파일을 프로덕션 설정 합니다. 변환 설정 이라는 변환 파일에 지정 된 `web.debug.config`, `web.release.config`등입니다. (이러한 파일의 이름은 MSBuild 구성와 일치 합니다.) 변환 파일을 포함 하는 배포 해야 하는 변경 내용만 `Web.config` 파일입니다. 간단한 구문을 사용 하 여 변경 내용을 지정 합니다.

다음 예제에서는 부분을 `web.release.config` 릴리스 구성의 배포에 대 한 생성 될 수 있는 파일입니다. 예제의 대체 키워드를 배포 하는 동안 지정 합니다 *connectionString* 에서 노드를 `Web.config` 파일 예제에 나와 있는 값으로 바뀝니다.

[!code-xml[Main](overview/samples/sample102.xml)]

자세한 내용은 [웹 응용 프로그램 프로젝트 배포를 위한 Web.config 변환 구문](https://msdn.microsoft.com/library/dd465326%28VS.100%29.aspx) msdn <a id="0.2_a"> </a> 웹 사이트 및[웹 배포: Web.Config 변환](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html)인 Vishal Joshi의 블로그입니다.

<a id="0.2__Toc224729058"></a><a id="0.2__Toc253429295"></a><a id="0.2__Toc243304666"></a>

### <a name="database-deployment"></a>데이터베이스 배포

Visual Studio 2010 배포 패키지를 SQL Server 데이터베이스에 대 한 종속성을 포함할 수 있습니다. 패키지 정의의 일부로 원본 데이터베이스에 대 한 연결 문자열을 제공 합니다. 웹 패키지를 만들면 Visual Studio 2010 및 필요에 따라 데이터를 데이터베이스 스키마에 대 한 SQL 스크립트를 만들고 패키지에 추가 합니다. 또한 사용자 지정 SQL 스크립트를 제공 하 고 서버에서 실행 되도록 순서를 지정할 수 있습니다. 대상 서버에 적절 한 연결 문자열을 제공 하면 배포 시에 배포 프로세스는 다음 데이터베이스 스키마를 만들고 데이터를 추가 하는 스크립트를 실행 하려면이 연결 문자열을 사용 합니다.

또한 한 번의 클릭을 사용 하 여 게시, 배포 응용 프로그램 원격 공유 호스팅 사이트에 게시 되 면 데이터베이스를 직접 게시를 구성할 수 있습니다. 자세한 내용은 참조 하세요. [방법:는 데이터베이스 프로젝트를 통해 웹 응용 프로그램을 배포](https://msdn.microsoft.com/library/dd465343%28VS.100%29.aspx) MSDN 웹 사이트 및 [VS 2010을 사용 하 여 데이터베이스 배포](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html) 인 Vishal Joshi의 블로그입니다.

<a id="0.2__Toc224729059"></a><a id="0.2__Toc253429296"></a><a id="0.2__Toc243304667"></a>

### <a name="one-click-publish-for-web-applications"></a>웹 응용 프로그램에 대 한 One-click 게시

Visual Studio 2010에서는 IIS 원격 관리 서비스를 사용 하 여 원격 서버에 웹 응용 프로그램을 게시할 수도 있습니다. 호스팅 계정 또는 서버를 테스트 하거나 스테이징 서버에 대 한 게시 프로필을 만들 수 있습니다. 각 프로필은 적절 한 자격 증명을 안전 하 게 저장할 수 있습니다. 대상에 배포할 수 있습니다 웹 한 번의 클릭을 사용 하 여 한 번의 클릭을 사용 하 여 서버 도구 모음을 게시 합니다. Visual Studio 2010을 사용 하 여 MSBuild 명령줄을 사용 하 여 게시할 수 있습니다. 이렇게 하면 연속 통합 모델의 게시를 포함 하도록 팀 빌드 환경을 구성할 수 있습니다.

자세한 내용은 참조 하세요. [방법: 웹 응용 프로그램 프로젝트를 사용 하 여 One-click 게시 및 웹 배포 배포](https://msdn.microsoft.com/library/dd465337%28VS.100%29.aspx) MSDN 웹 사이트 및 [VS 2010을 사용 하 여 원클릭 게시 웹](http://vishaljoshi.blogspot.com/2009/05/web-1-click-publish-with-vs-2010.html) 인 Vishal Joshi의 블로그입니다. Visual Studio 2010에서 웹 응용 프로그램 배포에 대 한 비디오 프레젠테이션을 보려면을 참조 하세요 [웹 개발자 미리 보기에 대 한 VS 2010](http://vishaljoshi.blogspot.com/2008/12/vs-2010-for-web-developer-previews.html) 인 Vishal Joshi의 블로그입니다.

<a id="0.2__Toc224729060"></a><a id="0.2__Toc253429297"></a><a id="0.2__Toc243304668"></a>

### <a name="resources"></a>자료

다음 웹 사이트는 ASP.NET 4 및 Visual Studio 2010에 대 한 추가 정보를 제공 합니다.

- [ASP.NET 4](https://msdn.microsoft.com/library/ee532866%28VS.100%29.aspx) -MSDN 웹 사이트에서 ASP.NET 4에 대 한 공식 설명서.
- [https://www.asp.net/](https://www.asp.net/) -ASP.NET 팀의 웹 사이트입니다.
- [https://www.asp.net/dynamicdata/](https://msdn.microsoft.com/library/cc488545.aspx) 및 [ASP.NET 동적 데이터 콘텐츠 맵](https://msdn.microsoft.com/library/cc488545%28VS.100%29.aspx) -ASP.NET 팀 사이트에 ASP.NET Dynamic Data에 대 한 공식 설명서의 온라인 리소스입니다.
- [https://www.asp.net/ajax/](../../ajax/index.md) ASP.NET Ajax 개발을 위한-주 웹 리소스입니다.
- [https://blogs.msdn.com/webdevtools/](https://blogs.msdn.com/webdevtools/) Visual Studio 2010의 기능에 대 한 정보를 포함 하는-Visual Web Developer 팀 블로그입니다.
- [ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack) -미리 보기 버전의 ASP.NET에 대 한 기본 웹 리소스입니다.

<a id="0.2__Toc224729061"></a><a id="0.2__Toc253429298"></a><a id="0.2__Toc243304669"></a>

## <a name="disclaimer"></a>고지 사항

본 문서는 예비 문서이며, 여기에 설명한 소프트웨어의 최종 상업적 출시 전에 크게 변경될 수 있습니다.

이 문서에 포함된 정보는 게시 날짜 현재 논의된 문제에 대한 Microsoft Corporation의 당시 관점을 나타냅니다. Microsoft는 변화하는 시장 상황에 부응해야 하므로, Microsoft의 일부에 대한 책임으로 해석되어서는 안되며, 게시 날짜 이후 소개된 정보의 정확성을 Microsoft가 보증할 수 없습니다.

이 백서는 정보 제공만을 목적으로 합니다. Microsoft는 이 문서에 있는 정보에 대한 명시적 또는 묵시적, 법적인 보증을 하지 않습니다.

해당 저작권법을 준수하는 것은 사용자의 책임입니다. 저작권에서의 권리와는 별도로, 이 설명서의 어떠한 부분도 Microsoft의 명시적인 서면 승인 없이는 어떠한 형식이나 수단(전기적, 기계적, 복사기에 의한 복사, 디스크 복사 또는 다른 방법) 또는 목적으로도 복제되거나, 검색 시스템에 저장 또는 도입되거나, 전송될 수 없습니다.

Microsoft가 이 설명서 본안에 관련된 특허권, 상표권, 저작권 또는 기타 지적 재산권 등을 보유할 수도 있습니다. 서면 사용권 계약에 따라 Microsoft로부터 귀하에게 명시적으로 제공된 권리 이외에, 이 문서의 제공은 귀하에게 이러한 특허권, 상표권, 저작권, 또는 기타 지적 소유권 등에 대한 어떠한 사용권도 허여하지 않습니다.

다른 언급이 없는 경우 예제 회사, 조직, 제품, 도메인 이름, 전자 메일 주소, 로고, 사람, 장소 및 이벤트 용례은 실제 데이터가 아닙니다 및 실제 회사, 조직, 제품, 도메인 이름, 전자 메일 연관 시킬 의도가 없으며 주소, 로고, 사람, 장소 또는 이벤트는 또는 유추 하도록 지정 합니다.

© 2009 Microsoft Corporation. All rights reserved.

Microsoft 및 Windows는 미국 및/또는 기타 국가에서 Microsoft Corporation의 상표이거나 등록된 상표입니다.

여기에 언급된 실제 회사와 제품의 이름은 각각 해당 소유자의 상표일 수 있습니다.
