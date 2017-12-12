---
uid: whitepapers/aspnet4/overview
title: "ASP.NET 4 및 Visual Studio 2010 웹 개발 개요 | Microsoft Docs"
author: rick-anderson
description: "이 문서에서는.net Framework 4 및 Visual Studio 2010에 포함 된 ASP.NET에 대 한 다양 한 새로운 기능에 대 한 개요를 제공 합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/10/2010
ms.topic: article
ms.assetid: d7729af4-1eda-4ff2-8b61-dbbe4fc11d10
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /whitepapers/aspnet4
msc.type: content
ms.openlocfilehash: 226ef83f289b8fbe9a68f0d0741c7eca0d96ba94
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="aspnet-4-and-visual-studio-2010-web-development-overview"></a>ASP.NET 4 및 Visual Studio 2010 웹 개발 개요
====================
> 이 문서에서는.net Framework 4 및 Visual Studio 2010에 포함 된 ASP.NET에 대 한 다양 한 새로운 기능에 대 한 개요를 제공 합니다.
> 
> [이 백서를 다운로드 합니다.](https://download.microsoft.com/download/7/1/A/71A105A9-89D6-4201-9CC5-AD6A3B7E2F22/ASP_NET_4_and_Visual_Studio_2010_Web_Development_Overview.pdf)


**목차**

**[핵심 서비스](#0.2__Toc253429238 "_Toc253429238")**  
[Web.config 파일 리팩터링](#0.2__Toc253429239 "_Toc253429239")  
[확장 가능한 출력 캐싱](#0.2__Toc253429240 "_Toc253429240")  
[웹 응용 프로그램 자동 시작](#0.2__Toc253429241 "_Toc253429241")  
[페이지를 영구적으로 리디렉션](#0.2__Toc253429242 "_Toc253429242")  
[세션 상태 축소](#0.2__Toc253429243 "_Toc253429243")  
[허용 가능한 Url의 범위](#0.2__Toc253429244 "_Toc253429244")  
[확장 가능한 요청 유효성 검사](#0.2__Toc253429245 "_Toc253429245")  
[개체 캐싱 및 캐싱 확장성 개체](#0.2__Toc253429246 "_Toc253429246")  
[확장 가능한 HTML, URL 및 HTTP 헤더 인코딩을](#0.2__Toc253429247 "_Toc253429247")  
[단일 작업자 프로세스에서 개별 응용 프로그램에 대 한 성능 모니터링](#0.2__Toc253429248 "_Toc253429248")  
[멀티 타기 팅](#0.2__Toc253429249 "_Toc253429249")

**[Ajax](#0.2__Toc253429250 "_Toc253429250")**  
[Web Forms 및 MVC에 포함 된 jQuery](#0.2__Toc253429251 "_Toc253429251")  
[콘텐츠 배달 네트워크 지원](#0.2__Toc253429252 "_Toc253429252")  
[ScriptManager 명시적 스크립트](#0.2__Toc253429253 "_Toc253429253")

**[Web Forms](#0.2__Toc253429256 "_Toc253429256")**  
[설정 된 Page.MetaKeywords 및 Page.MetaDescription 속성 메타 태그](#0.2__Toc253429257 "_Toc253429257")  
[개별 컨트롤의 뷰 상태 사용](#0.2__Toc253429258 "_Toc253429258")  
[브라우저 기능으로 변경](#0.2__Toc253429259 "_Toc253429259")  
[ASP.NET 4에서에서의 라우팅](#0.2__Toc253429260 "_Toc253429260")  
[클라이언트 Id 설정](#0.2__Toc253429261 "_Toc253429261")  
[데이터 컨트롤에서 행 선택 보관](#0.2__Toc253429262 "_Toc253429262")  
[ASP.NET의 차트 컨트롤](#0.2__Toc253429263 "_Toc253429263")  
[QueryExtender 제어를 사용 하 여 데이터를 필터링](#0.2__Toc253429264 "_Toc253429264")  
[Html 인코딩된 코드 식을](#0.2__Toc253429265 "_Toc253429265")  
[프로젝트 템플릿 변경](#0.2__Toc253429266 "_Toc253429266")  
[CSS 개선](#0.2__Toc253429267 "_Toc253429267")  
[Div 숨겨진 필드 주위 요소 숨기기](#0.2__Toc253429268 "_Toc253429268")  
[템플릿 기반 컨트롤에 대 한 외부 테이블을 렌더링](#0.2__Toc253429269 "_Toc253429269")  
[ListView 컨트롤의 향상 된 기능](#0.2__Toc253429270 "_Toc253429270")  
[CheckBoxList 및 RadioButtonList 컨트롤 향상](#0.2__Toc253429271 "_Toc253429271")  
[메뉴 컨트롤 개선](#0.2__Toc253429272 "_Toc253429272")  
[마법사 및 CreateUserWizard 컨트롤 56](#0.2__Toc253429273 "_Toc253429273")

**[ASP.NET MVC](#0.2__Toc253429274 "_Toc253429274")**  
[영역 지원](#0.2__Toc253429275 "_Toc253429275")  
[데이터 주석을 특성 유효성 검사 지원을](#0.2__Toc253429276 "_Toc253429276")  
[템플릿 기반 도우미](#0.2__Toc253429277 "_Toc253429277")

**[동적 데이터](#0.2__Toc253429278 "_Toc253429278")**  
[기존 프로젝트에 대 한 동적 데이터 사용](#0.2__Toc253429279 "_Toc253429279")  
[DynamicDataManager 컨트롤 선언적 구문](#0.2__Toc253429280 "_Toc253429280")  
[엔터티 템플릿에](#0.2__Toc253429281 "_Toc253429281")  
[Url 및 전자 메일 주소에 대 한 새 필드 템플릿을](#0.2__Toc253429282 "_Toc253429282")  
[DynamicHyperLink 컨트롤을 사용 하 여 링크 만들기](#0.2__Toc253429283 "_Toc253429283")  
[데이터 모델의 상속에 대 한 지원](#0.2__Toc253429284 "_Toc253429284")  
[다 대 다 관계 (Entity Framework에만 해당)에 대 한 지원](#0.2__Toc253429285 "_Toc253429285")  
[새 특성을 제어 표시 및 지원 열거형](#0.2__Toc253429286 "_Toc253429286")  
[필터에 대 한 지원 강화](#0.2__Toc253429287 "_Toc253429287")

**[Visual Studio 2010 웹 개발 기능 향상](#0.2__Toc253429288 "_Toc253429288")**  
[CSS 호환성 향상](#0.2__Toc253429289 "_Toc253429289")  
[HTML 및 JavaScript 코드 조각을](#0.2__Toc253429290 "_Toc253429290")  
[JavaScript IntelliSense의 향상 된 기능](#0.2__Toc253429291 "_Toc253429291")

**[웹 응용 프로그램 배포를 Visual Studio 2010](#0.2__Toc253429292 "_Toc253429292")**  
[패키징 웹](#0.2__Toc253429293 "_Toc253429293")  
[Web.config 변환](#0.2__Toc253429294 "_Toc253429294")  
[데이터베이스 배포](#0.2__Toc253429295 "_Toc253429295")  
[웹 응용 프로그램에 대 한 One-click 게시](#0.2__Toc253429296 "_Toc253429296")  
[리소스](#0.2__Toc253429297 "_Toc253429297")

**[고 지 사항](#0.2__Toc253429298 "_Toc253429298")**

<a id="0.2__Toc224729018"></a><a id="0.2__Toc253429238"></a><a id="0.2__Toc243304612"></a>

## <a name="core-services"></a>핵심 서비스

ASP.NET 4에는 다양을 한 출력 캐싱 및 세션 상태 저장소와 같은 핵심 ASP.NET 서비스를 개선 하는 기능이 도입 되었습니다.

<a id="0.2__Toc243304613"></a><a id="0.2__Toc253429239"></a><a id="0.2__Toc224729019"></a>

### <a name="webconfig-file-refactoring"></a>리팩터링 Web.config 파일

`Web.config` 웹 응용 프로그램의 규모가 상당히 지난 몇 차례의.NET Framework를 통해 새로운 기능이 추가 되었습니다, Ajax 등으로 대 한 구성이 포함 된 파일, 라우팅 및 IIS 7와 통합 합니다. 이로 인해 구성 하거나 Visual Studio와 같은 도구 없이 새 웹 응용 프로그램을 시작 하기 어렵습니다. 이.NET Framework 4의 주요 구성 요소 이동 된는 `machine.config` 파일 및 응용 프로그램을 지금 이러한 설정을 상속 합니다. 이 통해는 `Web.config` 비어 있는 것으로 또는 Visual Studio에 대 한 응용 프로그램의 대상 프레임 워크의 버전을 지정 하는 다음 행만 포함 하는 ASP.NET 4 응용 프로그램에서 파일:

[!code-xml[Main](overview/samples/sample1.xml)]

<a id="0.2__Toc253429240"></a><a id="0.2__Toc243304614"></a>

### <a name="extensible-output-caching"></a>확장 가능한 출력 캐싱

ASP.NET 1.0 출시 된 이후에 출력 캐싱을 메모리의 페이지, 컨트롤 및 HTTP 응답의 생성된 된 출력을 저장할 수 있게 되었습니다. 후속 웹 요청에 ASP.NET 수 콘텐츠를 서비스 보다 신속 하 게 출력 처음부터 다시 생성 하는 대신 메모리에서 생성 된 출력을 검색 하 여 합니다. 그러나이 방법에는 제한 사항-생성 된 콘텐츠 항상 메모리에 저장할 수 있으며 웹 응용 프로그램의 다른 부분에서 메모리 요구가 원인와 경쟁 수 출력 캐싱을 사용 되는 메모리 사용량이 발생 하는 서버에 있습니다.

ASP.NET 4에는 하나 이상의 사용자 지정 출력 캐시 공급자를 구성할 수 있도록 출력 캐싱에 확장성 지점을 추가 합니다. 출력 캐시 공급자 HTML 콘텐츠를 유지 하는 저장소 메커니즘을 사용할 수 있습니다. 이 클라우드 저장소에 로컬 또는 원격 디스크를 포함할 수 있는 다양 한 유지 메커니즘에 대 한 사용자 지정 출력 캐시 공급자를 만들 수 있으며 분산 캐시 엔진이 있습니다.

새에서 파생 되는 클래스로 사용자 지정 출력 캐시 공급자를 만든 *System.Web.Caching.OutputCacheProvider* 유형입니다. 공급자를 구성할 수 있습니다는 `Web.config` new를 사용 하 여 파일 *공급자* 하위 섹션에서 *outputCache* 요소를 다음 예제와 같이:

[!code-xml[Main](overview/samples/sample2.xml)]

ASP.NET 4에서는 모든 HTTP 응답에에서는 기본적으로 렌더링 된 페이지 및 컨트롤 앞의 예에서 같이 메모리에 출력 캐시를 사용 하 여 여기서는 *defaultProvider* 특성은 AspNetInternalProvider로 설정 합니다. 에 대 한 다른 공급자 이름을 지정 하 여 웹 응용 프로그램에 대해 사용 되는 기본 출력 캐시 공급자를 변경할 수 있습니다 *defaultProvider*합니다.

또한 각 컨트롤에 대해 요청에 따라 되는 서로 다른 출력 캐시 공급자를 선택할 수 있습니다. New를 사용 하 여 선언적으로 작업을 수행 하는 웹 사용자 컨트롤에 대 한 다른 출력 캐시 공급자를 선택 하는 가장 쉬운 방법은 *providerName* 다음 예제와 같이 control 지시문에 특성:

[!code-aspx[Main](overview/samples/sample3.aspx)]

HTTP 요청에 대 한 다른 출력 캐시 공급자를 지정 하는 약간 더 많은 작업이 필요 합니다. 새 재정의 공급자를 선언적으로 지정 하지 않고 *GetOuputCacheProviderName* 에서 메서드는 `Global.asax` 파일을 프로그래밍 방식으로 특정 요청에 사용할 공급자를 지정 합니다. 다음 예제에서는 이 작업을 수행하는 방법을 보여 줍니다.

[!code-csharp[Main](overview/samples/sample4.cs)]

출력 캐시 공급자 확장 ASP.NET 4에 추가 하 여 웹 사이트에 대 한 더욱 강력 하 고 보다 자동화 출력 캐싱 전략을 이제 해결할 수 있습니다. 예를 들어, 페이지를 디스크에 더 낮은 트래픽을 캐시 하는 동안 메모리에 사이트의 "상위 10 개의" 페이지를 캐시할 수는 이제 있습니다. 또는 모든 다양 조합 렌더링된 된 페이지에 대 한 캐시 수 있지만 프런트 엔드 웹 서버에서 메모리 소비는 오프 로드 하도록 분산된 캐시를 사용 합니다.

<a id="0.2__Toc224729020"></a><a id="0.2__Toc253429241"></a><a id="0.2__Toc243304615"></a>

### <a name="auto-start-web-applications"></a>웹 응용 프로그램을 자동으로 시작 합니다.

일부 웹 응용 프로그램이 많은 양의 데이터를 로드 하거나 첫 번째 요청을 처리 하기 전에 처리 비용의 초기화를 수행 해야 합니다. "해제" ASP.NET 응용 프로그램을 다음 중 초기화 코드를 실행 하는 사용자 지정 방식 고안 해야 했습니다 이러한 상황에 대 한 이전 버전의 ASP.NET에는 *응용 프로그램\_부하* 에서 메서드는 `Global.asax` 파일입니다.

라는 새로운 확장성 기능 *자동 시작* 직접 주소가이 시나리오는 사용 가능한 경우 ASP.NET 4에서 실행 되도록 Windows Server 2008 r 2에서 IIS 7.5입니다. 자동 시작 기능에는 응용 프로그램 풀을 시작, ASP.NET 응용 프로그램을 초기화 한 다음 HTTP 요청을 받아들이기 위한 제어 방법을 제공 합니다.

> [!NOTE] 
> 
> IIS 7.5 용 IIS 응용 프로그램 준비 모듈
> 
> IIS 팀 IIS 7.5 용 응용 프로그램 준비 모듈의 첫 번째 베타 테스트 버전을 출시 했습니다. 이렇게 하면 앞에서 설명한 것 보다 더 쉽게 응용 프로그램을 준비 하는 중입니다. 사용자 지정 코드를 작성 하는 대신 웹 응용 프로그램에 네트워크의 요청을 수락 하기 전에 실행 하는 Url 리소스를 지정 합니다. 이 준비는 IIS 서비스의 시작 중에 발생 (으로 IIS 응용 프로그램 풀을 구성한 경우 *AlwaysRunning*) 및 IIS 작업자 프로세스가 재생 되는 경우. 재활용을 하는 동안 이전 IIS 작업자 프로세스가 요청 때까지 계속 실행 새로 만든된 작업자 프로세스는 완전히 준비를 방해 하지 또는 다른 문제로 인해 unprimed 캐시 응용 프로그램에서 발생할 수 있도록 합니다. 이 모듈의 버전 2.0 부터는 ASP.NET 모든 버전을 사용 하는 참고 합니다.
> 
> 자세한 내용은 참조 [응용 프로그램 웜 업을](https://www.iis.net/extensions/applicationwarmup%20on%20the%20IIS.net) IIS.net 웹 사이트에 있습니다. 준비 기능을 사용 하는 방법을 보여 주는 연습을 참조 하십시오. [IIS 7.5 응용 프로그램 준비 모듈 시작](https://www.iis.net/learn/manage) IIS.net 웹 사이트에 있습니다.


자동 시작 기능을 사용 하려면 IIS 관리자에서 다음 구성을 사용 하 여 자동으로 시작 되도록 IIS 7.5에서 응용 프로그램 풀을 설정의 `applicationHost.config` 파일:

[!code-xml[Main](overview/samples/sample5.xml)]

개별 응용 프로그램에 다음 구성을 사용 하 여 자동으로 시작 되도록 지정 하는 단일 응용 프로그램 풀에서 여러 응용 프로그램을 포함할 수 있으므로 `applicationHost.config` 파일:

[!code-xml[Main](overview/samples/sample6.xml)]

IIS 7.5의 정보를 사용 하 여 IIS 7.5 서버는 콜드 시작 또는 개별 응용 프로그램 풀이 재생 되는 `applicationHost.config` 파일을 자동으로 시작 되도록 어떤 웹 응용 프로그램 요구를 확인 합니다. Iis 7.5 자동 시작에 대 한 표시 된 각 응용 프로그램에 대 한 HTTP 요청 상태는 응용 프로그램이 일시적으로 허용 하지 않습니다 응용 프로그램을 시작 하려면 ASP.NET 4로 요청을 보냅니다. ASP.NET에 정의 된 형식을 인스턴스화하이 상태에 있을 때에 *serviceAutoStartProvider* 특성 (같이 이전 예에서) 및 해당 공용 진입점으로 호출 합니다.

구현 하 여 필요한 진입점과 관리 되는 자동 시작 종류를 만들는 *(는) IProcessHostPreloadClient* 다음 예제와 같이 인터페이스:

[!code-csharp[Main](overview/samples/sample7.cs)]

프로그램 초기화 된 후 코드에서 실행의 *미리 로드* 메서드 및 메서드는 반환, ASP.NET 응용 프로그램 요청을 처리할 준비가 되었습니다.

이제 자동 시작.5 IIS와 ASP.NET 4를 추가 하 여는 잘 정의 된 방식을 첫 번째 HTTP 요청을 처리 하기 전에 비용이 많이 드는 응용 프로그램 초기화를 수행 하기 위한 만들어졌습니다. 예를 들어 응용 프로그램 초기화는 응용 프로그램이 초기화 되었고 HTTP 트래픽을 허용 하도록 준비 하는 부하 분산 장치를 다음 신호를 보내는 데 새 자동 시작 기능을 사용할 수 있습니다.

<a id="0.2__Toc224729021"></a><a id="0.2__Toc253429242"></a><a id="0.2__Toc243304616"></a>

### <a name="permanently-redirecting-a-page"></a>페이지를 영구적으로 리디렉션

검색 엔진에서 유효 하지 않은 링크의 누적 될 수 있는 시간에 따라 페이지 및 콘텐츠에 주위를 이동할 수는 웹 응용 프로그램에서 일반적인이 좋습니다. Asp.net에서 개발자가 일반적으로 요청 이전 Url 사용 하 여 처리를 사용 하 여는 *Response.Redirect* 메서드를 새 URL로 요청을 전달 합니다. 그러나는 *리디렉션* 메서드 추가 http 왕복 이전 Url에 액세스 하려고 할 때 발생 하는 HTTP 302 찾을 (임시 리디렉션) 응답을 발급 합니다.

ASP.NET 4를 새로 추가 *RedirectPermanent* HTTP 301 문제를 쉽게 도우미 메서드 다음 예제와 같이 응답을 영구적으로 이동 합니다.

[!code-csharp[Main](overview/samples/sample8.cs)]

검색 엔진 및 영구 리디렉션을 인식 하는 다른 사용자 에이전트는 임시 리디렉션을 위해 브라우저에서 불필요 한 왕복을 제거 하는 콘텐츠의와 연결 된 새 URL을 저장 합니다.

<a id="0.2__Toc224729022"></a><a id="0.2__Toc253429243"></a><a id="0.2__Toc243304617"></a>

### <a name="shrinking-session-state"></a>세션 상태를 축소합니다.

ASP.NET 웹 팜 전체에서 세션 상태를 저장 하기 위한 두 가지 기본 옵션을 제공:-out-of-process 세션 상태 서버를 사용 하는 호출 하는 세션 상태 공급자 및 Microsoft SQL Server 데이터베이스에 데이터를 저장 하는 세션 상태 공급자입니다. 두 옵션 모두 웹 응용 프로그램의 작업자 프로세스 외부 상태 정보를 저장 되므로, 원격 저장소로 전송 하기 전에 serialize 할 세션 상태에 있습니다. 세션 상태에 저장 되는 정보의 양을에 따라 serialize 된 데이터의 크기가 상당히 커질 수 있습니다.

ASP.NET 4에서는 두 종류의-out-of-process 세션 상태 공급자에 대 한 새 압축 옵션을 소개합니다. 경우는 *compressionEnabled* 다음 예제에 표시 된 구성 옵션 설정 되어 *true*, ASP.NET은 압축 (및 압축 풀기) .NETFramework를사용하여serialize된세션상태 *System.IO.Compression.GZipStream* 클래스입니다.

[!code-xml[Main](overview/samples/sample9.xml)]

간단한 새 특성을 추가 하 여는 `Web.config` 파일, 응용 프로그램을 웹 서버에 배포할 예비 CPU 주기 serialize 세션 상태 데이터의 크기에 상당한 절감을 실현할 수 있습니다.

<a id="0.2__Toc253429244"></a><a id="0.2__Toc243304618"></a>

### <a name="expanding-the-range-of-allowable-urls"></a>허용 가능한 Url 범위를 확장합니다.

ASP.NET 4 응용 프로그램 Url의 크기를 확장 하는 것에 대 한 새 옵션을 소개 합니다. 이전 버전의 ASP.NET URL 경로 길이가 260 자, NTFS 파일 경로 제한에 따라 제약을 받습니다. ASP.NET 4에는 옵션이 있습니다 (늘리거나) 응용 프로그램에 따라이 한도 사용 하 여 두 개의 새 *httpRuntime* 구성 특성입니다. 다음 예제에서는 이러한 새 특성을 보여 줍니다.

[!code-xml[Main](overview/samples/sample10.xml)]

더 길거나 더 짧은 경로 (프로토콜, 서버 이름 및 쿼리 문자열을 포함 하지 않는 URL의 일부)를 허용 하려면 수정 된  *[maxUrlLength](https://msdn.microsoft.com/en-us/library/system.web.configuration.httpruntimesection.maxurllength.aspx)*  특성입니다. 길거나 짧은 쿼리 문자열을 허용 하려면 값을 수정 된  *[maxQueryStringLength](https://msdn.microsoft.com/en-us/library/system.web.configuration.httpruntimesection.maxquerystringlength.aspx)*  특성입니다.

ASP.NET 4를 사용 하면 URL 문자 검사에서 사용 되는 문자를 구성할 수 있습니다. ASP.NET URL의 경로 부분에서 잘못 된 문자를 찾습니다, 요청을 거부 하 고 HTTP 400 오류를 발생 시킵니다. ASP.NET의 이전 버전에서는 URL 문자 검사 된 고정된 문자 집합으로 제한 합니다. ASP.NET 4에서 new를 사용 하는 유효한 문자 집합이 사용자 지정할 수 *requestPathInvalidChars* 특성에는 *httpRuntime* 다음 예제와 같이 구성 요소:

[!code-xml[Main](overview/samples/sample11.xml)]

기본적으로는 *requestPathInvalidChars* 특성은 8 자 잘못 된 것으로 정의 합니다. (에 할당 된 문자열에 *requestPathInvalidChars* 기본적으로*,*는 보다 작은 (&lt;), 보다 큼 (&gt;), 및 앰퍼샌드 (&amp;) 문자는 때문에 인코딩된는 `Web.config` 파일은 XML 파일입니다.) 필요에 따라 잘못 된 문자 집합을 사용자 지정할 수 있습니다.

> [!NOTE]
> 참고의 IETF RFC 2396에 정의 된 대로 잘못 된 URL 문자는 항상 0x00-0x1f, ASCII 범위에 문자를 포함 하는 URL 경로 거부 ASP.NET 4 ([http://www.ietf.org/rfc/rfc2396.txt](http://www.ietf.org/rfc/rfc2396.txt)). IIS 6을 실행 하는 버전의 Windows Server에서 또는 이상 http.sys 프로토콜 장치 드라이버 자동으로 거부 Url이 문자로 합니다.


<a id="0.2__Toc253429245"></a><a id="0.2__Toc243304619"></a>

### <a name="extensible-request-validation"></a>확장 가능한 요청 유효성 검사

ASP.NET 요청 유효성 검사는 사이트 간 스크립팅 (XSS) 공격에 자주 사용 되는 문자열에 대 한 들어오는 HTTP 요청 데이터를 검색 합니다. 잠재적인 XSS 문자열이 발견 되 면 요청 유효성 검사는 주의 대상 문자열에 플래그를 지정 하 고 오류를 반환 합니다. XSS 공격에 사용 되는 가장 일반적인 문자열을 찾은 경우에 기본 제공 요청 유효성 검사 오류를 반환 합니다. 너무 많은 긍정 XSS 유효성 검사를 보다 적극적으로 확인을 이전의 시도가 발생 했습니다. 하지만 고객 특정 페이지 또는 특정 유형의 요청에 대 한 보다 적극적으로 또는 반대로 할 수 의도적으로 XSS을 완화 하는 요청 유효성 검사를 할 수 있습니다.

ASP.NET 4에서 요청 유효성 검사 기능 이루어졌을 확장 가능한 사용자 지정 요청 유효성 검사 논리를 사용할 수 있도록 합니다. 요청 유효성 검사를 확장 하려면 새에서 파생 되는 클래스를 만듭니다 *System.Web.Util.RequestValidator* 유형인, 응용 프로그램을 구성 합니다. (에 *httpRuntime* 는 의섹션`Web.config`파일)를 사용자 지정 형식을 사용 합니다. 다음 예제에서는 사용자 지정 요청 유효성 검사 클래스를 구성 하는 방법을 보여 줍니다.

[!code-xml[Main](overview/samples/sample12.xml)]

새 *requestValidationType* 특성에 사용자 지정 요청 유효성 검사를 제공 하는 클래스를 지정 하는 표준.NET Framework 형식 식별자 문자열이 필요 합니다. 각 요청에 대 한 ASP.NET 각 들어오는 HTTP 요청 데이터를 처리 하려면 사용자 지정 형식을 호출 합니다. 들어오는 URL, (쿠키 및 사용자 지정 헤더), 모든 HTTP 헤더 및 엔터티 본문은 다음 예제에 표시 된 같은 사용자 지정 요청 유효성 검사 클래스에 대 한 모든 사용 가능한:

[!code-csharp[Main](overview/samples/sample13.cs)]

여기서 하지 않으려는 경우 들어오는 HTTP 데이터를 검사 하는 경우 요청 유효성 검사 클래스 대체할 수 있습니다 ASP.NET 기본 요청 유효성 검사를 단순히 호출 하 여 실행할 수 있도록 *기본 합니다. IsValidRequestString 합니다.*

<a id="0.2__Toc253429246"></a><a id="0.2__Toc243304620"></a>

### <a name="object-caching-and-object-caching-extensibility"></a>개체 캐싱 및 캐싱 확장성 개체

ASP.NET가 강력한 메모리 내 개체 캐시의 첫 번째 릴리스 이후 포함 (*System.Web.Caching.Cache*). 캐시를 구현 하는 비 웹 응용 프로그램에서 사용 된는 자주 사용 되었습니다. 그러나 것이에 대 한 참조를 포함 하는 Windows Forms 또는 WPF 응용 프로그램에 대 한 잘못 된 구문이 `System.Web.dll` 를 대비해 ASP.NET 개체 캐시를 사용할 수 있습니다.

캐시를 사용 하려면 모든 응용 프로그램에 대 한.NET Framework 4에는 새 어셈블리, 새 네임 스페이스, 일부 기본 형식 및 구체적인 구현을 캐싱 도입 되었습니다. 새 `System.Runtime.Caching.dll` 에 새로운 캐싱 API를 포함 하는 어셈블리는 *System.Runtime.Caching* 네임 스페이스입니다. 네임 스페이스는 두 가지 핵심 클래스 집합이 포함 되어 있습니다.

- 모든 유형의 사용자 지정 캐시 구현 작성 하기 위한 기초를 제공 하는 추상 형식입니다.
- 구체적인 메모리에 개체 캐시 구현 (의 *System.Runtime.Caching.MemoryCache* 클래스).

새 *MemoryCache* 클래스는 ASP.NET 캐시와 비슷하게 모델링 및 내부 캐시 엔진 논리의 대부분 ASP.NET와 공유 합니다. 하지만의 공용 캐싱 Api *System.Runtime.Caching* ASP.NET을 사용한 경우 개발 된 사용자 지정의 캐시를 지원 하도록 업데이트 되었습니다 *캐시* 개체에 익숙한 개념을 찾을 수 있습니다는 새 Api입니다.

자세한 내용은 새 *MemoryCache* 클래스 및 기본 Api를 지 원하는 전체 문서를 기준으로 해야 합니다. 그러나 다음 예제에서는 제공 새 캐시 API의 작동 방식을 이해 합니다. 이 예제에서는 모든 종속성 없이 Windows Forms 응용 프로그램에 대 한 작성 되었습니다 `System.Web.dll`합니다.

[!code-csharp[Main](overview/samples/sample14.cs)]

<a id="0.2__Toc253429247"></a><a id="0.2__Toc243304621"></a>

### <a name="extensible-html-url-and-http-header-encoding"></a>확장 가능한 HTML, URL 및 HTTP 헤더 인코딩

ASP.NET 4에서 다음과 같은 일반적인 텍스트 인코딩 작업에 대 한 사용자 지정 인코딩 루틴을 만들 수 있습니다.

- HTML 인코딩입니다.
- URL 인코딩은 합니다.
- HTML 특성 인코딩입니다.
- 아웃 바운드 HTTP 헤더를 인코딩입니다.

새에서 파생 하 여 사용자 지정 인코더를 만들 수 있습니다 *System.Web.Util.HttpEncoder* 유형 및 다음 ASP.NET을 구성에서 사용자 지정 형식을 사용 하는 *httpRuntime* 의 섹션은 `Web.config` 파일을로 다음 예제에 나와 있습니다.

[!code-xml[Main](overview/samples/sample15.xml)]

ASP.NET 사용자 지정 인코딩 구현을 인코딩 방법의 공용 때마다 자동으로 호출 사용자 지정 인코더를 구성한 후의 *System.Web.HttpUtility* 또는 *System.Web.HttpServerUtility* 클래스 라고 합니다. 한 부분을 웹 개발 팀의 웹 개발 팀의 나머지 부분에서 계속 공용 ASP.NET 인코딩 Api를 사용 하는 동안 적극적인 문자 인코딩을 구현 하는 사용자 지정 인코더를 만들 수 있습니다. 사용자 지정 인코더를 중앙에서 구성 하 여는 *httpRuntime* 요소를 공용 ASP.NET 인코딩 Api의 모든 텍스트 인코딩 호출은 사용자 지정 인코더를 통해 라우팅될 수 있도록을 정렬 되어 있습니다.

<a id="0.2__Toc253429248"></a><a id="0.2__Toc243304622"></a>

### <a name="performance-monitoring-for-individual-applications-in-a-single-worker-process"></a>단일 작업자 프로세스에서 개별 응용 프로그램에 대 한 성능 모니터링

단일 서버에서 호스팅할 수 있는 웹 사이트 수를 늘리기 위해 많은 호스팅 서비스 공급자의 단일 작업자 프로세스가 여러 ASP.NET 응용 프로그램을 실행 합니다. 그러나 여러 응용 프로그램에 단일 공유 작업자 프로세스를 사용 하는 경우 어렵습니다 문제가 발생 하는 개별 응용 프로그램을 식별 하는 서버 관리자에 대 한 합니다.

ASP.NET 4 CLR에 의해 도입 된 새 리소스 모니터링 기능을 활용 합니다. 이 기능을 활성화 하려면 다음 XML 구성 코드 조각에 추가할 수 있습니다는 `aspnet.config` 구성 파일입니다.

[!code-xml[Main](overview/samples/sample16.xml)]

> [!NOTE]
> 참고는 `aspnet.config` 파일이.NET Framework를 설치한 디렉터리에 있습니다. 없으면는 `Web.config` 파일입니다.


경우는 *appDomainResourceMonitoring* 기능은, 두 개의 새로운 성능 카운터 "ASP.NET 응용 프로그램" 성능 범주에서 사용할 수 있는: *관리 되는 프로세서 시간 백분율* 및  *관리 되는 사용 되는 메모리*합니다. 이러한 성능 카운터의 모두 예상된 CPU 시간 및 개별 ASP.NET 응용 프로그램의 관리 되는 메모리 사용률을 추적 하는 새로운 CLR 응용 프로그램 도메인 리소스 관리 기능을 사용 합니다. 결과적으로, ASP.NET 4 관리자 생깁니다 단일 작업자 프로세스에서 실행 되는 개별 응용 프로그램의 리소스 소비량에 대 한 보다 세부적인 뷰.

<a id="0.2__Toc253429249"></a><a id="0.2__Toc243304623"></a>

### <a name="multi-targeting"></a>멀티 타기팅

특정 버전의.NET Framework를 대상으로 하는 응용 프로그램을 만들 수 있습니다. ASP.NET 4에서 새 특성에는 *컴파일* 의 요소는 `Web.config` 파일을 사용 하면.NET Framework 4 이상을 대상으로 합니다. .NET Framework 4를 명시적으로 대상 및에서 선택적 요소를 포함 하는 경우는 `Web.config` 파일에 대 한 항목 예: *system.codedom*, 이러한 요소는.NET Framework 4에 대 한 정확 해야 합니다. (.NET Framework 4를 명시적으로 대상 하지 않으면 대상 프레임 워크에 있는 항목의 부족에서 유추 됩니다는 `Web.config` 파일입니다.)

다음 예제에서는 사용을 보여 줍니다.는 *targetFramework* 특성에 *컴파일* 의 요소는 `Web.config` 파일입니다.

[!code-xml[Main](overview/samples/sample17.xml)]

특정 버전의.NET Framework를 대상으로 지정 하는 방법에 대 한 다음 note:

- .NET Framework 4 응용 프로그램 풀에서 ASP.NET 빌드 시스템 가정은.NET Framework 4를 대상으로 하는 경우는 `Web.config` 파일에 포함 되지 않습니다는 *targetFramework* 특성 또는 경우에는 `Web.config` 파일이 없습니다. (.NET Framework 4에서 실행 되도록 응용 프로그램을 코딩 변경 해야 할 수도 있습니다.)
- 포함 하는 경우는 *targetFramework* 특성, 경우에 *system.codeDom* 요소에 정의 된는 `Web.config` 파일을이 파일은.NET Framework 4에 대 한 올바른 항목을 포함 해야 합니다.
- 사용 하는 경우는 *aspnet\_컴파일러* 응용 프로그램 (예: 빌드 환경)를 미리 컴파일하 명령에서 올바른 버전의를 사용 해야 합니다는 *aspnet\_컴파일러* 대상 프레임 워크에 대 한 명령입니다. .NET Framework 3.5 및 이전 버전에 대 한 컴파일하는 데는.NET Framework 2.0 (%WINDIR%\Microsoft.NET\Framework\v2.0.50727)와 함께 제공 되는 컴파일러를 사용 합니다. .NET Framework 4와 함께 제공 되는 컴파일러를 사용 하 여 만든 응용 프로그램 프레임 워크를 사용 하 여 또는 이후 버전을 사용 하 여 컴파일하는 데 합니다.
- 런타임 시 컴파일러는 컴퓨터에 설치 된 최신 프레임 워크 어셈블리 사용 (일부 이므로 GAC에). Framework에 대 한 업데이트를 나중에 수행 하는 경우 (예를 들어 가상의 버전 4.1이 설치 되어), 경우에 프레임 워크의 최신 버전의 기능을 사용할 수는 *targetFramework* 더 낮은 버전을 대상 특성 (4.0과 같은). 그러나 (디자인 타임에 Visual Studio 2010 또는 사용 하는 경우에 *aspnet\_컴파일러* 명령, 프레임 워크의 최신 기능을 사용 하면 컴파일러 오류).

<a id="0.2__Toc224729023"></a><a id="0.2__Toc253429250"></a><a id="0.2__Toc243304624"></a>

## <a name="ajax"></a>Ajax

<a id="0.2__Toc253429251"></a><a id="0.2__Toc243304625"></a>

### <a name="jquery-included-with-web-forms-and-mvc"></a>jQuery Web Forms 및 MVC와 함께 제공 됨

Web Forms 및 MVC 모두에 대 한 Visual Studio 템플릿 jQuery 오픈 소스 라이브러리를 포함 합니다. 새 웹 사이트 또는 프로젝트를 만들 때 다음과 같은 3 파일이 포함 된 스크립트 폴더를 만듭니다.

- jQuery-1.4.1.js –는 사람이 읽을 수, 축소 되지 않은 버전의 jQuery 라이브러리입니다.
- jQuery 14.1.min.js-축소 된 버전의 jQuery 라이브러리입니다.
- jQuery-1.4.1-vsdoc.js – jQuery 라이브러리에 대 한 Intellisense 설명서 파일입니다.

응용 프로그램을 개발 하는 동안 축소 되지 않은 버전의 jQuery 포함 합니다. 축소 된 버전의 jQuery 프로덕션 응용 프로그램에 대 한 포함 합니다.

예를 들어 다음 Web Forms 페이지 jQuery를 사용 하 여 포커스를가지고 있을 때 노란색 ASP.NET TextBox 컨트롤의 배경색을 변경 하는 방법을 보여 줍니다.

[!code-aspx[Main](overview/samples/sample18.aspx)]

<a id="0.2__Toc253429252"></a><a id="0.2__Toc243304626"></a>

### <a name="content-delivery-network-support"></a>콘텐츠 배달 네트워크 지원

Microsoft Ajax CDN 콘텐츠 배달 네트워크 ()를 사용 하 여 웹 응용 프로그램을 ASP.NET Ajax 및 jQuery 스크립트를 쉽게 추가할 수 있습니다. JQuery 라이브러리를 사용 하 여 추가 하 여 시작할 수는 예를 들어 한 `<script>` 태그를 다음과 같이 Ajax.microsoft.com 가리키는 페이지:

[!code-html[Main](overview/samples/sample19.html)]

Microsoft Ajax CDN을 활용 하기 위해, Ajax 응용 프로그램의 성능을 크게 향상 시킬 수 있습니다. Microsoft Ajax CDN의 콘텐츠는 세계에 있는 서버에 캐시 됩니다. 또한 Microsoft Ajax CDN에는 브라우저 서로 다른 도메인에 있는 웹 사이트에 대 한 캐시 된 JavaScript 파일을 다시 사용할 수 있도록 설정 합니다.

Microsoft Ajax 콘텐츠 배달 네트워크 Secure Sockets Layer를 사용 하 여 웹 페이지를 처리 해야 하는 경우 SSL (HTTPS)을 지원 합니다.

Microsoft Ajax CDN에 대 한 자세한 내용은 다음 웹 사이트를 방문 합니다.

[https://www.asp.net/ajaxlibrary/CDN.ashx](../../ajax/cdn/overview.md)

ASP.NET ScriptManager Microsoft Ajax CDN을 지원합니다. EnableCdn 속성 설정 하나의 속성에 따라 단순히 CDN에서 모든 ASP.NET 프레임 워크 JavaScript 파일을 검색할 수 있습니다.

[!code-aspx[Main](overview/samples/sample20.aspx)]

True 값으로는 EnableCdn 속성을 설정한 후 ASP.NET 프레임 워크는 유효성 검사 및 UpdatePanel에 사용 되는 모든 JavaScript 파일을 포함 하 여 CDN에서 모든 ASP.NET 프레임 워크 JavaScript 파일을 검색 합니다. 이 하나의 속성을 설정 웹 응용 프로그램의 성능에 큰 영향을 미칠 수 있습니다.

웹 리소스의 특성을 사용 하 여 사용자 고유의 JavaScript 파일에 대 한의 CDN 경로 설정할 수 있습니다. 새 CdnPath 속성 값이 true로는 EnableCdn 속성을 설정 하는 경우 사용 되는 CDN에 대 한 경로 지정 합니다.

[!code-csharp[Main](overview/samples/sample21.cs)]

<a id="0.2__Toc253429253"></a><a id="0.2__Toc243304627"></a>

### <a name="scriptmanager-explicit-scripts"></a>ScriptManager 명시적 스크립트

이전에 ASP.NET ScriptManger 사용 하는 경우 다음 해야 했습니다 전체 모놀리식 ASP.NET Ajax 라이브러리를 로드 합니다. 새 ScriptManager.AjaxFrameworkMode 속성을 이용 ASP.NET Ajax 라이브러리의 구성 요소를 로드 하는 정확 하 게 제어 하 고만 해야 하는 ASP.NET Ajax 라이브러리의 구성 요소를 로드할 수 있습니다.

ScriptManager.AjaxFrameworkMode 속성은 다음 값으로 설정할 수 있습니다.

- 사용 가능--ScriptManager 컨트롤에 자동으로 모든 핵심 프레임 워크 스크립트 (레거시 동작)의 조합 된 스크립트 파일의 MicrosoftAjax.js 스크립트 파일을 포함 하는 작업을 지정 합니다.
- 사용 하지 않도록 설정-모든 Microsoft Ajax 스크립트 기능이 해제 되 고 있는지 ScriptManager 컨트롤을 참조 하지 않는 모든 스크립트를 자동으로 지정 합니다.
- 명시적-스크립트 참조 페이지에서 필요로 하는 개별 프레임 워크 코어 스크립트 파일에 있는 명시적으로 포함 되도록 하 고 각 스크립트 파일에 필요한 종속성에 대 한 참조를 포함 합니다를 지정 합니다.

예를 들어 AjaxFrameworkMode 속성 명시적 값을 설정 하는 경우 필요한 특정 ASP.NET Ajax 구성 요소 스크립트 지정할 수 있습니다.

[!code-aspx[Main](overview/samples/sample22.aspx)]

<a id="0.2__The_DataView_Control"></a><a id="0.2__The_DataContext_and"></a><a id="0.2__Refactoring_the_Microsoft"></a><a id="0.2__Toc224729032"></a><a id="0.2__Toc253429256"></a><a id="0.2__Toc243304630"></a>

## <a name="web-forms"></a>Web Forms

Web Forms ASP.NET 1.0의 릴리스 이후 ASP.NET의 핵심 기능은 되었습니다. 다음을 포함 하는 ASP.NET 4에 대 한이 영역에서 많은 부분이 향상 되었습니다.

- 설정 하는 기능 *메타* 태그입니다.
- 더 자세히 제어할 뷰 상태입니다.
- 브라우저 기능에 맞게 편리 하 게 합니다.
- ASP.NET Web forms 라우팅을 사용할 수 있도록 지원 합니다.
- 생성 된 Id를 보다 자세히 제어 합니다.
- 데이터 컨트롤에서 선택 된 행을 유지 하는 기능.
- 렌더링 된 HTML에 보다 자세히 제어는 *FormView* 및 *ListView* 컨트롤입니다.
- 데이터 소스 제어에 대 한 지원을 필터링 합니다.

<a id="0.2__Toc224729033"></a><a id="0.2__Toc253429257"></a><a id="0.2__Toc243304631"></a>

### <a name="setting-meta-tags-with-the-pagemetakeywords-and-pagemetadescription-properties"></a>Page.MetaDescription 속성과 Page.MetaKeywords 함께 메타 태그를 설정합니다.

두 개의 속성을 추가 하는 ASP.NET 4는 *페이지* 클래스 *MetaKeywords* 및 *MetaDescription*합니다. 이러한 두 속성에 해당 나타냅니다 *메타* 다음 예제에 표시 된 대로 페이지의 태그:

[!code-aspx[Main](overview/samples/sample23.aspx)]

이러한 두 속성은 동일 하 게 작동 방식으로 페이지의 *제목* 속성이 없습니다. 이러한 규칙을 따릅니다.

1. 없는 경우 없는 *메타* 태그는 *h e a d* 속성 이름과 일치 하는 요소 (즉, 이름을 "키워드" = *Page.MetaKeywords* 및 이름 = "description" 에대한 *Page.MetaDescription*, 이러한 속성을 설정 하지 않은 의미), *메타* 태그 렌더링 된 페이지에 추가 됩니다.
2. 이미 있을 경우 *메타* 이러한 이름으로 태그를 이러한 속성 역할을 get 및 set 메서드는 기존 태그의 내용에 대 한 합니다.

런타임 시 데이터베이스 또는 다른 원본에서 콘텐츠를 가져올 수 있습니다 및 대상을 설명 하는 동적으로 태그를 설정할 수 있는 이러한 속성을 설정할 수에 대 한 특정 페이지가 됩니다.

설정할 수도 있습니다는 *키워드* 및 *설명* 속성에는 *@ Page* Web Forms 페이지 태그는 다음 예제 에서처럼의 예외:

[!code-aspx[Main](overview/samples/sample24.aspx)]

이렇게 하면 무시 됩니다는 *메타* 태그 내용을 (있는 경우)의 페이지에 이미 선언 되었습니다.

설명의 내용을 *메타* 태그는 Google의 미리 보기를 나열 하는 검색 개선에 사용 됩니다. (세부 정보를 참조 하십시오. [메타 설명 변경 된 조각 개선](http://googlewebmastercentral.blogspot.com/2007/09/improve-snippets-with-meta-description.html) Google 웹 마스터 중앙 블로그.) Google 및 Windows Live Search 사용 하지 않고 키워드의 내용을, 이외에 그 다른 검색 엔진 수 있습니다. 자세한 내용은 참조 [메타 키워드 조언을](http://www.searchengineguide.com/richard-ball/meta-keywords-a.php) 검색 엔진 설명서 웹 사이트에 있습니다.

이러한 새 속성은 간단한 기능 하지만를 만드는 코드는 직접 작성 또는에서 이러한 작업을 수동으로 추가할 필요 절약 됩니다는 *메타* 태그입니다.

<a id="0.2__Toc224729034"></a><a id="0.2__Toc253429258"></a><a id="0.2__Toc243304632"></a>

### <a name="enabling-view-state-for-individual-controls"></a>개별 컨트롤의 뷰 상태 사용

기본적으로 뷰 상태 페이지에 있는 각 컨트롤 응용 프로그램에 대 한 필요 하지 않은 경우에 잠재적으로 뷰 상태를 저장 하는 결과와 페이지에 대 한 사용 됩니다. 뷰 상태 데이터는 페이지를 생성 하 고 페이지를 클라이언트로 전송할 다시 게시 하는 데 걸리는 시간에는 늘어나지만 태그에 포함 됩니다. 필요한 것 보다 자세한 뷰 상태가 저장 심각한 성능 저하를 발생할 수 있습니다. ASP.NET의 이전 버전에서 개발자는 페이지 크기를 줄이기 위해 개별 컨트롤에 대 한 뷰 상태를 해제할 수 있습니다 하지만 개별 컨트롤에 대 한 명시적 수행 해야 합니다. 웹 서버 컨트롤에는 ASP.NET 4에서는 *ViewStateMode* 기본적으로 상태 보기를 사용 하지 않도록 설정 하 고 다음 페이지에서 필요한 컨트롤을에 사용할 수 있는 속성입니다.

*ViewStateMode* 속성은 세 가지 값을 포함 하는 열거형을 사용: *Enabled*, *비활성화*, 및 *상속*합니다. *활성화* 해당 컨트롤에 대 한 설정 된 모든 자식 컨트롤에 대 한 상태 뷰 *상속* 이거나는 아무 것도 설정 합니다. *사용 안 함* 뷰 상태를 사용할 수 없습니다 및 *상속* 컨트롤을 사용 하도록 지정 된 *ViewStateMode* 부모 컨트롤에서 설정 합니다.

다음 예제와 방법을 *ViewStateMode* 속성의 작동 합니다. 한 값을 포함 하는 태그와 다음 페이지에 있는 컨트롤에 대 한 코드는 *ViewStateMode* 속성:

[!code-aspx[Main](overview/samples/sample25.aspx)]

볼 수 있듯이 코드 PlaceHolder1 컨트롤 뷰 상태를 해제 합니다. 이 속성 값이 상속 되는 자식 label1 컨트롤 (*상속* 에 대 한 기본값은 *ViewStateMode* 컨트롤에 대 한) 하 고 따라서 뷰 상태가 저장 합니다. PlaceHolder2 컨트롤에서 *ViewStateMode* 로 설정 되어 *사용*이므로 label2이이 속성을 상속 하 고 뷰 상태를 저장 합니다. 페이지가 처음으로 로드 하는 경우는 *텍스트* 모두의 속성이 *레이블* 컨트롤 문자열 "[DynamicValue]"로 설정 됩니다.

이러한 설정의 효과 페이지를 처음으로 로드 하는 경우 브라우저에 다음 출력이 표시 됩니다.

사용 안 함`: [DynamicValue]`

사용 가능:`[DynamicValue]`

하지만 포스트백 후 다음과 같은 출력이 표시 됩니다.

사용 안 함`: [DeclaredValue]`

사용 가능:`[DynamicValue]`

Label1 컨트롤 (해당 *ViewStateMode* 값으로 설정 되어 *비활성화 된*)에서 코드 설정 된 값은 유지 되지가 합니다. 그러나는 label2 제어할 (해당 *ViewStateMode* 값으로 설정 됩니다 *Enabled*)의 상태를 유지 했습니다.

설정할 수도 있습니다 *ViewStateMode* 에 *@ Page* 다음 예제와 같이 지시문:

[!code-aspx[Main](overview/samples/sample26.aspx)]

*페이지* 클래스는 다른 컨트롤, 역할 페이지에 있는 모든 컨트롤에 대 한 부모 컨트롤을 합니다. 기본값 *ViewStateMode* 은 *Enabled* 에 대 한 인스턴스의 *페이지*합니다. 컨트롤의 기본 설정 되므로 *상속*, 컨트롤에 상속 됩니다는 *Enabled* 속성 값을 설정 하지 않으면 *ViewStateMode* 페이지 또는 제어 수준입니다.

값은 *ViewStateMode* 속성 결정 경우에 뷰 상태를 유지 관리 하는 경우는 *EnableViewState* 속성이로 설정 되어 *true*합니다. 경우는 *EnableViewState* 속성이 *false*, 뷰 상태를 유지 하지 것입니다 경우에 *ViewStateMode* 로 설정 된 *Enabled*합니다.

이 기능에 대 한 적절 하 게 사용 된 *ContentPlaceHolder* 을 설정할 수 있는 마스터 페이지에서 컨트롤 *ViewStateMode* 를 *비활성화* 마스터에 대 한 페이지 하 고 다음 사용 하도록 설정 에 대해 개별적으로 *ContentPlaceHolder* 차례로 필요로 하는 컨트롤을 포함 하는 컨트롤 상태를 확인 합니다.

<a id="0.2__Toc224729035"></a><a id="0.2__Toc253429259"></a><a id="0.2__Toc243304633"></a>

### <a name="changes-to-browser-capabilities"></a>브라우저 기능에 대 한 변경

사용자는 이라는 기능을 사용 하 여 사이트를 탐색 하는 데 사용 하는 브라우저의 기능을 결정 하는 ASP.NET *브라우저 기능*합니다. 브라우저 기능으로 표시 됩니다는 *HttpBrowserCapabilities* 개체 (에 의해 노출 된 *Request.Browser* 속성). 예를 들어, 사용할 수는 *HttpBrowserCapabilities* 개체 유형 및 버전 현재 브라우저의 특정 버전의 JavaScript 지원 하는지 확인 합니다. 또는 사용할 수는 *HttpBrowserCapabilities* 해당 요청이 모바일 장치에서 시작 하는지 여부를 결정 하는 개체입니다.

*HttpBrowserCapabilities* 브라우저 정의 파일 집합에 의해 개체 이루어집니다. 이러한 파일의 특정 브라우저 기능에 대 한 정보를 포함 합니다. ASP.NET 4에서 최근에 도입 된 브라우저 및 Google Chrome, 리서치 등 동작 BlackBerry 스마트폰 및 Apple iPhone에서 장치에 대 한 정보를 포함 하도록 이러한 브라우저 정의 파일 업데이트 되었습니다.

다음 목록에는 새 브라우저 정의 파일을 보여 줍니다.

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

Asp.net 버전 3.5 서비스 팩 1에서는 다음과 같은 방법으로 브라우저에 기능을 정의할 수 있습니다.

- 컴퓨터 수준에서 만들거나 업데이트 한 `.browser` 다음 폴더에 XML 파일:

- [!code-console[Main](overview/samples/sample27.cmd)]

- 브라우저 기능을 정의한 후 브라우저 기능 어셈블리를 다시 작성 하 고 GAC에 추가 하기 위해 Visual Studio 명령 프롬프트에서 다음 명령을 실행 하면:

- [!code-console[Main](overview/samples/sample28.cmd)]

- 만드는 각 응용 프로그램에 대 한 한 `.browser` 응용 프로그램의 파일 `App_Browsers` 폴더입니다.

이러한 접근 방식은 요구 XML 파일을 변경 하 고 컴퓨터 수준 변경에 대 한 다시 시작 해야 응용 프로그램 aspnet를 실행 한 후\_regbrowsers.exe 프로세스입니다.

ASP.NET 4 라고도 하는 기능에 포함 되어 *브라우저 기능 공급자*합니다. 이름에서 알 수 있듯이 차례로 수 있는 공급자를 작성할 수이 있습니다 브라우저 기능을 확인 하려면 사용자 고유의 코드를 사용 합니다.

실제로, 개발자가 자주 정의 하지 않습니다 사용자 지정 브라우저 기능. 브라우저 파일은 프로세스를 업데이트, 업데이트 하는 매우 복잡 한 하드과 XML 구문을 `.browser` 파일을 사용 및 정의 복잡할 수 있습니다. 훨씬 쉽게이 수행할 수 있도록는 어떤 일반적인 브라우저 정의 구문 있는 경우 또는 최신 브라우저 정의 또는 이러한 데이터베이스에 대 한 웹 서비스도 포함 된 데이터베이스입니다. 새 브라우저 기능 공급자 기능을 사용 하면 이러한 시나리오가 가능 하 고 유용 타사 개발자를 위한 합니다.

두 가지 주요 새로운 ASP.NET 4 브라우저 기능 공급자 기능을 사용 하기 위한: ASP.NET 브라우저 기능 정의 기능을 확장 하거나 완전히 대체 합니다. 다음 섹션에서는 기능을 대체 하는 방법을 차례로 확장 하는 방법을 먼저 설명 합니다.

#### <a name="replacing-the-aspnet-browser-capabilities-functionality"></a>ASP.NET 브라우저 기능 기능 대체

ASP.NET 브라우저 기능 정의 기능을 완전히 대체 하려면 다음이 단계를 따르십시오.

1. 파생 되는 공급자 클래스를 만듭니다 *HttpCapabilitiesProvider* 를 재정의 *GetBrowserCapabilities* 다음 예제와 같이 메서드: 

    [!code-csharp[Main](overview/samples/sample29.cs)]

    이 예제의 코드에서는 새 *HttpBrowserCapabilities* 개체만 명명 된 브라우저 및 MyCustomBrowser에 해당 기능을 설정 하는 기능을 지정 합니다.
2. 응용 프로그램에서 공급자를 등록 합니다. 

    응용 프로그램으로 공급자를 사용 하려면 추가 해야 합니다는 *공급자* 특성을 *browserCaps* 섹션은 `Web.config` 또는 `Machine.config` 파일입니다. (공급자 특성을 정의할 수 있습니다는 *위치* 특정 모바일 장치에 대 한 폴더와 같이 응용 프로그램에서 특정 디렉터리에 대 한 요소입니다.) 설정 하는 방법을 보여 주는 다음 예제는 *공급자* 구성 파일의 특성:

    [!code-xml[Main](overview/samples/sample30.xml)]

    다음 예제에 표시 된 것과 같이 코드를 사용 하 여 새 브라우저 기능 정의 등록 하는 다른 방법은입니다.

    [!code-csharp[Main](overview/samples/sample31.cs)]

    이 코드 실행 해야 합니다는 *응용 프로그램\_시작* 의 이벤트는 `Global.asax` 파일입니다. 변경 된 *BrowserCapabilitiesProvider* 클래스는 캐시는 적용 된에 대 한 유효한 상태 유지 하는지 확인 하기 위해 응용 프로그램의 모든 코드를 실행 하기 전에 발생 해야 *HttpCapabilitiesBase* 개체입니다.

#### <a name="caching-the-httpbrowsercapabilities-object"></a>HttpBrowserCapabilities 개체 캐싱

앞의 예제 코드는 얻기 위해 사용자 지정 공급자를 호출할 때마다 실행 하는 한 가지 문제에는 *HttpBrowserCapabilities* 개체입니다. 각 요청 하는 동안 여러 번 발생할 수 있습니다. 예제에서는 공급자에 대 한 코드는 하지 효과가 그다지 합니다. 그러나 사용자 지정 공급자의 코드에서 많은 작업을 수행 하는 경우를 얻기 위해는 *HttpBrowserCapabilities* 개체 성능에 영향을 줄 수 있습니다. 이 방지 하기를 캐시할 수 있습니다는 *HttpBrowserCapabilities* 개체입니다. 아래 단계를 수행합니다.

1. 파생 되는 클래스를 만듭니다 *HttpCapabilitiesProvider*, 다음 예제에서와 같은: 

    [!code-csharp[Main](overview/samples/sample32.cs)]

    예제에서는 코드는 사용자 지정 BuildCacheKey 메서드를 호출 하 여 캐시 키를 생성 하 고 사용자 지정 GetCacheTime 메서드를 호출 하 여 캐시에 있는 시간의 길이 가져옵니다. 그런 다음 추가 코드는 적용 된 *HttpBrowserCapabilities* 개체를 캐시 합니다. 개체를 캐시에서 검색 및에서 다시 사용할 수 있도록 후속 요청은 사용자 지정 공급자의 사용 합니다.
2. 앞의 절차에 설명 된 대로 응용 프로그램과 함께 공급자를 등록 합니다.

#### <a name="extending-aspnet-browser-capabilities-functionality"></a>ASP.NET 브라우저 기능 기능 확장

이전 섹션에 새 하는 방법을 설명 *HttpBrowserCapabilities* ASP.NET 4에는 개체입니다. 또한 ASP.NET에 이미 있는 새 브라우저 기능 정의 추가 하 여 ASP.NET 브라우저 기능 기능을 확장할 수 있습니다. XML 브라우저 정의 사용 하지 않고이 수행할 수 있습니다. 다음 절차에 표시 된 방법입니다.

1. 파생 되는 클래스를 만듭니다 *HttpCapabilitiesEvaluator* 를 재정의 *GetBrowserCapabilities* 메서드를 다음 예제와 같이: 

    [!code-csharp[Main](overview/samples/sample33.cs)]

    이 코드는 먼저 브라우저를 식별 하려면 ASP.NET 브라우저 기능 기능을 사용 합니다. 그러나 브라우저가 없으므로 식별 되는 경우에 따라 요청에 정의 되어 있는 정보 (즉는 *브라우저* 속성은 *HttpBrowserCapabilities* 개체는 "알 수 없음" 문자열), 코드 호출 사용자 지정 공급자 (MyBrowserCapabilitiesEvaluator) 브라우저를 식별할 수 있습니다.
2. 앞의 예제에 설명 된 대로 응용 프로그램과 함께 공급자를 등록 합니다.

#### <a name="extending-browser-capabilities-functionality-by-adding-new-capabilities-to-existing-capabilities-definitions"></a>기존 기능 정의에 새로운 기능을 추가 하 여 브라우저 기능 기능 확장

사용자 지정 브라우저 정의 공급자를 만들 뿐만 아니라 및 새 브라우저 정의 동적으로 만드는 추가 기능을 가진 기존 브라우저 정의 확장할 수 있습니다. 이 대상에 근접 하는 있지만 몇 가지 기능만 없는 하는 정의 사용할 수 있습니다. 이렇게 하려면 다음 단계를 따릅니다.

1. 파생 되는 클래스를 만듭니다 *HttpCapabilitiesEvaluator* 를 재정의 *GetBrowserCapabilities* 메서드를 다음 예제와 같이: 

    [!code-csharp[Main](overview/samples/sample34.cs)]

    예제 코드를 확장 하는 기존 ASP.NET *HttpCapabilitiesEvaluator* 클래스 및 가져옵니다는 *HttpBrowserCapabilities* 다음 코드를 사용 하 여 현재 요청 정의 일치 하는 개체 :

    [!code-csharp[Main](overview/samples/sample35.cs)]

    다음 코드는 추가 하거나이 브라우저에 대 한 기능을 수정할 수 있습니다. 새 브라우저 기능을 지정 하는 방법은 두 가지가 있습니다.

    - 에 키/값 쌍을 추가 *IDictionary* 의해 노출 되는 개체는 *기능* 의 속성은 *HttpCapabilitiesBase* 개체입니다. 코드는 이전 예에서 다중 터치의 값이 지정 하는 기능을 추가 *true*합니다.
    - 기존 속성을 설정는 *HttpCapabilitiesBase* 개체입니다. 이전 예제에서 코드에서는 설정 된 *프레임* 속성을 *true*합니다. 이 속성은 대 한 접근자는 *IDictionary* 의해 노출 되는 개체는 *기능* 속성입니다. 

        > [!NOTE]
        > 이 모델의 모든 속성에 적용 됩니다. *HttpBrowserCapabilities*, 컨트롤 어댑터를 포함 합니다.
2. 이전 절차에서 설명한 대로 응용 프로그램과 함께 공급자를 등록 합니다.

<a id="0.2__Toc224729036"></a><a id="0.2__Toc253429260"></a><a id="0.2__Toc243304634"></a>

### <a name="routing-in-aspnet-4"></a>ASP.NET 4에서에서의 라우팅

ASP.NET 4 Web forms 라우팅을 사용 하 여에 대 한 기본 제공 지원을 추가 합니다. 라우팅에서는 허용 하도록 응용 프로그램을 구성할 수 요청 Url에서 물리적 파일에 매핑되지 않습니다. 대신, 라우팅 Url을 사용자에 게 의미 이며 응용 프로그램에 대 한 검색 엔진 최적화 (SEO) 도움이 될 수 있는 정의를 사용할 수는 있습니다. 예를 들어 다음 예제에서는 같은 기존 응용 프로그램에 제품 범주를 표시 하는 페이지에 대 한 URL 형식입니다.

[!code-console[Main](overview/samples/sample36.cmd)]

라우팅를 사용 하 여 동일한 정보를 렌더링할 URL을 허용 하도록 응용 프로그램을 구성할 수 있습니다.

[!code-console[Main](overview/samples/sample37.cmd)]

라우팅 ASP.NET 3.5 s p 1부터 제공 되었습니다. (ASP.NET 3.5 s p 1의 라우팅을 사용 하는 방법의 예를 들어 항목을 참조 하십시오. [WebForms와 라우팅를 사용 하 여](http://haacked.com/archive/2008/03/11/using-routing-with-webforms.aspx "이 항목의 제목입니다.") Phil Haack의 블로그에서.) 그러나 ASP.NET 4는 다음과 같은 기능 라우팅에 사용 하기 쉽도록을 포함:

- *PageRouteHandler* 클래스 경로 정의할 때 사용 하는 간단한 HTTP 처리기입니다. 클래스에 라우팅 된다고 요청 하는 페이지에 데이터를 전달 합니다.
- 새 속성 *HttpRequest.RequestContext* 및 *Page.RouteData* (변수인에 대 한 프록시는 *HttpRequest.RequestContext.RouteData* 개체). 이러한 속성 쉽게 경로에서 전달 되는 정보에 액세스할 수 있습니다.
- 다음과 같은 새 식 작성기에에 정의 된 *System.Web.Compilation.RouteUrlExpressionBuilder* 및 *System.Web.Compilation.RouteValueExpressionBuilder*:
- *RouteUrl*, ASP.NET 서버 컨트롤 내에서 경로 URL에 해당 하는 URL을 만드는 간단한 방법을 제공 합니다.
- *RouteValue*에서 정보를 추출 하는 간단한 방법을 제공 하는 *RouteContext* 개체입니다.
- *RouteParameter* 쉽게에 포함 된 데이터를 전달 하는 클래스는 *RouteContext* 개체 데이터 소스 제어에 대 한 쿼리를 (비슷합니다 [ *FormParameter* ](https://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.formparameter.aspx)).

#### <a name="routing-for-web-forms-pages"></a>Web Forms 페이지에 대 한 라우팅

다음 예제에서는 new를 사용 하 여 Web Forms 경로 정의 하는 방법을 보여 줍니다. *MapPageRoute* 의 메서드는 *경로* 클래스:

[!code-csharp[Main](overview/samples/sample38.cs)]

ASP.NET 4에 도입 된 *MapPageRoute* 메서드. 다음 예제에서는 이전 예에서 같이 SearchRoute 정의에 해당 하지만 사용 하 여는 *PageRouteHandler* 클래스입니다.

[!code-csharp[Main](overview/samples/sample39.cs)]

예제에서 코드에서는 물리적 페이지에 경로 매핑합니다 (첫 번째 경로에서 `~/search.aspx`). 첫 번째 경로 정의는 또한 매개 변수에 지정 하려면 URL에서 추출 하는 페이지에 전달 하 지정 합니다.

*MapPageRoute* 메서드는 다음 메서드 오버 로드를 지원 합니다.

- *MapPageRoute (문자열 routeName, 문자열 routeUrl, physicalFile string, bool checkPhysicalUrlAccess)*
- *MapPageRoute (문자열 routeName, 문자열 routeUrl, physicalFile string, bool checkPhysicalUrlAccess, RouteValueDictionary 기본값)*
- *MapPageRoute (문자열 routeName, 문자열 routeUrl, 문자열 physicalFile, bool checkPhysicalUrlAccess, RouteValueDictionary 기본값, RouteValueDictionary 제약 조건)*

*checkPhysicalUrlAccess* 매개 변수를 경로 라우팅이 물리적 페이지에 대 한 보안 권한을 확인 해야 하는지 여부를 지정 (이 경우 search.aspx)와 받는 URL에 대 한 권한을 (이 경우 검색 / {지정 하려면}). 하는 경우의 값 *checkPhysicalUrlAccess* 은 *false*, 받는 URL의 사용 권한만 확인 합니다. 이러한 사용 권한은에 정의 된는 `Web.config` 에서는 다음과 같은 설정을 사용 하 여 파일:

[!code-xml[Main](overview/samples/sample40.xml)]

물리적 페이지에 액세스가 거부 되 구성 예에서는 `search.aspx` 관리자 역할에 있는 것을 제외한 모든 사용자에 대 한 합니다. 경우는 *checkPhysicalUrlAccess* 로 설정 된 *true* (기본값) 인 관리자가 사용자만 액세스할 수 있습니다 {지정 하려면} URL /search/ 물리적 페이지 search.aspx 이므로 해당 역할의 사용자가 제한 합니다. 경우 *checkPhysicalUrlAccess* 로 설정 된 *false* 앞의 예제와 같이 사이트를 구성 하 고, 모든 인증 된 사용자가 URL /search/ {지정 하려면} 액세스할 수 있습니다.

#### <a name="reading-routing-information-in-a-web-forms-page"></a>Web Forms 페이지에서 라우팅 정보 읽기

Web Forms 물리적 페이지의 코드에서는 URL 라우팅을 추출에 정보에 액세스할 수 있습니다 (또는 다른 개체를 추가 하는 기타 정보는 *RouteData* 개체) 두 가지 새 속성을 사용 하 여:  *HttpRequest.RequestContext* 및 *Page.RouteData*합니다. (*Page.RouteData* 래핑합니다 *HttpRequest.RequestContext.RouteData*.) 다음 예제에서는 사용 하는 방법을 보여 줍니다. *Page.RouteData*합니다.

[!code-csharp[Main](overview/samples/sample41.cs)]

이전 예제에서는 경로에 정의 된 대로 지정 하려면 매개 변수에 대해 전달 된 값을 추출 합니다. 다음 요청 URL을 고려 합니다.

[!code-console[Main](overview/samples/sample42.cmd)]

때이 요청이 "scott" 있기에서 렌더링 단어는 `search.aspx` 페이지.

#### <a name="accessing-routing-information-in-markup"></a>태그의 라우팅 정보에 액세스

이전 섹션에서 설명 하는 방법을 Web Forms 페이지의 코드에서 경로 데이터를 가져오는 방법을 보여 줍니다. 또한 태그에서 같은 정보에 액세스 권한을 제공 하는 식을 사용할 수 있습니다. 식 작성기는 선언적 코드를 사용 하는 강력 하 고 세련 된 방법입니다. (자세한 내용은 항목을 참조 하십시오. [Express 직접와 사용자 지정 식 작성기](http://haacked.com/archive/2006/11/29/Express_Yourself_With_Custom_Expression_Builders.aspx) Phil Haack의 블로그에서.)

ASP.NET 4 Web Forms 라우팅에 대 한 두 명의 새 식 작성기 포함 되어 있습니다. 다음 예제에서는 사용 하는 방법을 보여 줍니다.

[!code-aspx[Main](overview/samples/sample43.aspx)]

예제에서는 *RouteUrl* 식은 경로 매개 변수를 기반으로 하는 URL을 정의 하는데 사용 됩니다. 이 태그에 전체 URL 하드 코딩 하지 않아도 절감 하 고이 링크의 모든 변경 내용이 필요 없이 나중에 URL의 구조를 변경할 수 있습니다.

이 태그 앞에서 정의한 경로에 따라, 다음 URL을 생성 합니다.

[!code-console[Main](overview/samples/sample44.cmd)]

ASP.NET이 자동으로 올바른 경로 작동 (즉, 올바른 URL 생성) 입력된 매개 변수를 기반 합니다. 사용에 대 한 경로 지정할 수 있도록 하는 식에서 경로 이름을 포함할 수도 있습니다.

사용 하는 방법을 보여 주는 다음 예제는 *RouteValue* 식입니다.

[!code-aspx[Main](overview/samples/sample45.aspx)]

이 컨트롤을 포함 하는 페이지를 실행 하는 경우 값 "scott" 레이블에 표시 됩니다.

*RouteValue* 식을 사용 하면 쉽게 태그에서 경로 데이터를 사용할 수 있으며 더 복잡 한 Page.RouteData["x을 고치지 사용 되지 않습니다"] 태그에는 구문입니다.

#### <a name="using-route-data-for-data-source-control-parameters"></a>데이터 소스 제어 매개 변수에 대 한 경로 데이터를 사용 하 여

*RouteParameter* 클래스를 사용 하면 데이터 소스 제어에서 쿼리에 대 한 매개 변수 값으로 경로 데이터를 지정할 수 있습니다. 그 [작동과 거의 동일한는](https://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.formparameter.aspx) 다음 예제와 같이 클래스:

[!code-aspx[Main](overview/samples/sample46.aspx)]

경로 매개 변수 지정 하려면 값에 사용할 경우에 @companyname 에서 매개 변수는 *선택* 문.

<a id="0.2__Toc224729037"></a><a id="0.2__Toc253429261"></a><a id="0.2__Toc243304635"></a>

### <a name="setting-client-ids"></a>클라이언트 Id 설정

새 *ClientIDMode* asp.net에서 오래 된 문제를 해결 하는 속성 즉 만들려면 어떻게 해야 컨트롤은 *id* 렌더링 하는 요소에 대 한 특성입니다. 알고 있으면는 *id* 렌더링 된 요소에 대 한 특성은 응용 프로그램이 이러한 요소를 참조 하는 클라이언트 스크립트를 포함 하는 경우에 중요 합니다.

*id* 웹 서버 컨트롤에 대 한 렌더링 된 html에서 특성에 따라 생성 되는 *ClientID* 컨트롤의 속성입니다. ASP.NET 4를 생성 하기 위한 알고리즘까지는 *id* 에서 특성의 *ClientID* 속성 ID로, 및 (에서 같이 반복 된 컨트롤의 경우 (있는 경우)의 명명 컨테이너를 연결 하는 것 이었습니다 데이터 컨트롤)는 접두사와 일련 번호를 추가 하려면. 이 페이지에 컨트롤의 Id는 고유 보장 항상, 동안 알고리즘은 예측 가능 값과 클라이언트 스크립트에서 참조 하기 어려웠습니다 따라서 되는 컨트롤 Id로 인해 되었습니다.

새 *ClientIDMode* 속성을 사용 하면 클라이언트 ID 컨트롤에 대해 생성 되는 방식을 보다 정확 하 게 지정할 수 있습니다. 설정할 수 있습니다는 *ClientIDMode* 속성 페이지에 대 한 포함 하는 모든 컨트롤에 대 한 합니다. 가능한 설정은 다음과 같습니다.

- *AutoID* – 생성 하기 위한 알고리즘을 동일 *ClientID* 이전 버전의 ASP.NET에서 사용 된 속성 값입니다.
- *정적* –이 지정 하는 *ClientID* 값 부모 명명 컨테이너의 Id를 연결 하지 않고 ID와 동일 하 게 됩니다. 이 웹 사용자 컨트롤에 유용할 수 있습니다. 웹 사용자 정의 컨트롤 일 수 있으므로 서로 다른 페이지와 다른 컨테이너 컨트롤에서 사용 하는 컨트롤에 대 한 클라이언트 스크립트를 작성 하기 어려울 수 있습니다는 *AutoID* 알고리즘 됩니다 ID 값을 예측할 수 없으므로 .
- *예측 가능한* –이 옵션은 반복 템플릿을 사용 하는 데이터 컨트롤에서 사용 하기 위해 주로 합니다. 하지만 생성 된 컨트롤의 명명 컨테이너의 ID 속성을 연결 *ClientID* 값 "ctlxxx"과 같은 문자열에 포함 되지 않습니다. 이 설정은와 함께 작동 하는 *ClientIDRowSuffix* 컨트롤의 속성입니다. 설정한는 *ClientIDRowSuffix* 생성 된 항목에 대 한 속성 데이터 필드의 이름 및 해당 필드의 값을 접미사로 사용할 *ClientID* 값입니다. 로 데이터 레코드의 기본 키를 사용는 일반적으로 *ClientIDRowSuffix* 값입니다.
- *상속* –이 설정은 컨트롤에 대 한 기본 동작으로, 컨트롤의 ID 생성 부모와 동일한 지 지정 합니다.

설정할 수 있습니다는 *ClientIDMode* 페이지 수준에서 속성입니다. 기본값을 정의 합니다. *ClientIDMode* 현재 페이지의 모든 컨트롤에 대 한 값입니다.

기본 *ClientIDMode* 페이지 수준에서 값은 *AutoID*, 및 기본 *ClientIDMode* 제어 수준 값은 *상속*. 결과적으로, 코드에서 아무 곳 이나이 속성을 설정 하지 않으면, 모든 컨트롤이 기본적으로 *AutoID* 알고리즘입니다.

페이지 수준 값을 설정할는 *@ Page* 지시문, 다음 예제와 같이:

[!code-aspx[Main](overview/samples/sample47.aspx)]

설정할 수도 있습니다는 *ClientIDMode* 컴퓨터 (컴퓨터) 수준에서 또는 응용 프로그램 수준에서 구성 파일의 값입니다. 기본값을 정의 합니다. *ClientIDMode* 응용 프로그램의 모든 페이지의 모든 컨트롤에 대 한 설정입니다. 기본 컴퓨터 수준에서 값을 설정 하면 정의 *ClientIDMode* 해당 컴퓨터에서 모든 웹 사이트를 설정 합니다. 다음 예제와 *ClientIDMode* 구성 파일에서 설정 합니다.

[!code-xml[Main](overview/samples/sample48.xml)]

값의 앞에서 설명한 것 처럼는 *ClientID* 컨트롤의 부모에 대 한 속성의 명명 컨테이너에서 파생 됩니다. 마스터 페이지를 사용 하는 경우와 같은 일부 시나리오에서는 컨트롤은 결국 Id를 가진 다음에서 같이 렌더링 된 HTML:

[!code-html[Main](overview/samples/sample49.html)]

경우에는 *입력* 태그에 표시 된 요소 (에서 *TextBox* 컨트롤) 두 개의 명명 컨테이너는 페이지에서 (중첩 된 *ContentPlaceholder* 컨트롤), 마스터 페이지를 처리 하는 방식으로 인해 최종 결과 다음과 같은 컨트롤 ID는:

[!code-console[Main](overview/samples/sample50.cmd)]

이 ID는 페이지에서 고유 하 게 보장 하지만 대부분의 용도 대해 불필요 하 게 됩니다. 렌더링 된 ID의 길이를 줄이려면 및 ID 생성 되는 방식을 보다 자세하게 제어를 사용 한다고 가정해 보세요. (예를 들어 하려는 "ctlxxx" 접두사를 제거 합니다.) 설정 하 여이 작업을 수행할 수는 가장 쉬운 방법은는 *ClientIDMode* 다음 예제와 같이 속성:

[!code-aspx[Main](overview/samples/sample51.aspx)]

이 샘플에는 *ClientIDMode* 속성이 *정적* 가장 바깥쪽에 대 한 *NamingPanel* 요소 및로 설정 *예측 가능* 내부에 대 한 *NamingControl* 요소입니다. 이러한 설정은 다음 태그 (이전 예제에서와 동일 하 게 페이지와 마스터 페이지의 나머지 부분 가정)에서 발생 합니다.

[!code-html[Main](overview/samples/sample52.html)]

*정적* 설정이 가장 바깥쪽 안의 모든 컨트롤에 대 한 명명 계층 구조를 다시 설정할 때의 효과 갖고 *NamingPanel* 요소를 제거 하 고는 *ContentPlaceHolder* 및 *MasterPage* Id에서 생성 된 id입니다. (의 *이름* 렌더링 된 요소의 특성은 영향을 이벤트에 대 한 일반 ASP.NET 기능 유지 하도록 뷰 상태를 하 고, 합니다.) 에 대 한 태그를 이동 하는 경우에 있는 명명 계층 구조를 다시 설정할 때의 부작용은는 *NamingPanel* 요소를 사용 하 여 다른 *ContentPlaceholder* 컨트롤을 렌더링 된 클라이언트 Id는 동일 하 게 유지 합니다.

> [!NOTE]
> Note 렌더링 된 컨트롤 Id 고유한 지 확인 하기 위해 사용자가 결정 합니다. 그러지 않은 경우 클라이언트와 같은 개별 HTML 요소에 대 한 고유 Id를 필요로 하는 모든 기능을 중단할 수 있습니다 *document.getElementById* 함수입니다.


#### <a name="creating-predictable-client-ids-in-data-bound-controls"></a>데이터 바인딩된 컨트롤에서 예측 가능한 클라이언트 Id 만들기

*ClientID* 수 레거시 알고리즘에서 데이터 바인딩된 목록 컨트롤에서 컨트롤에 대해 생성 된 값을 하며는 실제로 예측할 수 없습니다. *ClientIDMode* 있으세요 어떻게 이러한 Id를 통해 생성 된 제어 기능 유지할 수 있습니다.

다음 예제에서 태그를 포함 한 *ListView* 제어:

[!code-aspx[Main](overview/samples/sample53.aspx)]

이전 예에서 *ClientIDMode* 및 *RowClientIDRowSuffix* 속성 태그에서 설정 됩니다. *ClientIDRowSuffix* 속성 데이터 바인딩된 컨트롤에만 사용할 수 있으며 해당 동작은 사용 하는 컨트롤에 따라 달라 집니다. 차이점은 다음과 같습니다.

- *GridView* 컨트롤-지정할 수 있습니다 하나 이상의 열 이름을 데이터 원본에서 런타임에 클라이언트 Id 생성에 결합 됩니다. 예를 들어, 설정한 경우 *RowClientIDRowSuffix* "ProductName, ProductId"를 컨트롤에 대 한 렌더링 된 요소는 다음과 같은 형식 Id:

- [!code-console[Main](overview/samples/sample54.cmd)]

- *ListView* 컨트롤-클라이언트 id와 같습니다. 추가 되는 데이터 원본에서 단일 열을 지정할 수 있습니다 예를 들어, 설정한 경우 *ClientIDRowSuffix* "ProductName" 렌더링 된 컨트롤 Id는 다음과 같은 형식이 됩니다.

- [!code-console[Main](overview/samples/sample55.cmd)]

- 이 경우 후행 1은 현재 데이터 항목의 제품 ID에서 파생 됩니다.

- *반복기* 컨트롤-이 컨트롤을 지원 하지 않습니다는 *ClientIDRowSuffix* 속성입니다. 에 *반복기* 제어, 현재 행의 인덱스를 사용 합니다. ClientIDMode를 사용 하는 경우 "예측 가능" =는 *반복기* 를 다음과 같은 형식의 Id가 생성 하는 클라이언트를 제어 합니다.

- [!code-console[Main](overview/samples/sample56.cmd)]

- 후행 0에는 현재 행의 인덱스입니다.

*FormView* 및 *DetailsView* 컨트롤 지원 하지 않는 여러 행을 표시 하지 않습니다는 *ClientIDRowSuffix* 속성입니다.

<a id="0.2__Toc224729038"></a><a id="0.2__Toc253429262"></a><a id="0.2__Toc243304636"></a>

### <a name="persisting-row-selection-in-data-controls"></a>데이터 컨트롤에서 행 선택 보관

*GridView* 및 *ListView* 컨트롤에는 사용자가 행을 선택 하도록 할 수 있습니다. 이전 버전의 ASP.NET에서는 선택 페이지에서 행 인덱스에 따라 되었습니다. 예를 들어 1 페이지에서 세 번째 항목을 선택 하 고 다음 2 페이지로 이동 하는 경우에 해당 페이지에서 세 번째 항목이 선택 됩니다.

처음 지속형된 선택 된.NET Framework 3.5 s p 1에서 동적 데이터 프로젝트에만 지원 됩니다. 이 기능을 사용 하는 경우 현재 선택한 항목은 항목에 대 한 데이터 키를 기반으로 합니다. 즉, 1 페이지에서 세 번째 행을 선택 하 고 2 페이지로 이동 하는 경우는 선택한 항목이 없음을 2 페이지. 1 페이지로 다시 이동 하면 세 번째 행이 여전히 선택 합니다. 보관 된 선택에 지원 됩니다는 *GridView* 및 *ListView* 를 사용 하 여 모든 프로젝트에서 컨트롤의 *EnablePersistedSelection* 속성에 표시 된 대로 다음 예제:

[!code-aspx[Main](overview/samples/sample57.aspx)]

<a id="0.2__Toc253429263"></a><a id="0.2__Toc243304637"></a>

### <a name="aspnet-chart-control"></a>ASP.NET의 차트 컨트롤

ASP.NET *차트* 컨트롤은.NET Framework의 데이터 시각화 기능 확장 됩니다. 사용 하는 *차트* 컨트롤, ASP.NET 페이지에 복잡 한 통계 또는 재무 분석을 위해 직관적 이며 시각적으로 우수한 차트는 만들 수 있습니다. ASP.NET *차트* 제어.NET Framework 버전 3.5 SP1 릴리스를 추가 기능으로 도입 되었으며.NET Framework 4 버전의 일부입니다.

컨트롤에는 다음과 같은 기능이 포함 됩니다.

- 35가지 개별 차트 종류
- 차트 영역, 제목, 범례 및 주석을의 무제한입니다.
- 다양 한 모든 차트 요소에 대 한 모양 설정 합니다.
- 대부분의 차트 종류에 대 한 3 차원 지원 합니다.
- 데이터 요소 주위에 자동으로 맞출 수 있는 스마트 데이터 레이블을 지정 합니다.
- 줄무늬 선을, 배율 구분선 및 로그 크기를 조정 합니다.
- 데이터 분석 및 변형을 위한 50개가 넘는 재무 및 통계 수식
- 단순 바인딩 및 차트 데이터의 조작입니다.
- 에 날짜, 시간 및 통화와 같은 일반적인 데이터 형식 지원 합니다.
- 대화형 작업 및 클라이언트를 포함 하는 이벤트 기반 사용자 지정에 대 한 지원 Ajax를 사용 하 여 이벤트를 클릭 합니다.
- 상태 관리
- 이진 스트리밍

다음 그림에서는 ASP.NET의 차트 컨트롤에 의해 생성 되는 재무 차트의 예를 보여 줍니다.

<a id="0.2_graphic17"></a>![](overview/_static/image1.png)

그림 2: ASP.NET 차트 컨트롤 예

샘플 코드를 다운로드 하는 추가 예제는 ASP.NET의 차트 컨트롤을 사용 하는 방법에 대 한는 [Microsoft 차트 컨트롤에 대 한 예제 환경](https://go.microsoft.com/fwlink/?LinkId=128300) MSDN 웹 사이트의 페이지입니다. 콘텐츠 커뮤니티의 더 많은 샘플을 확인할 수 있습니다는 [차트 컨트롤 포럼](https://go.microsoft.com/fwlink/?LinkId=128713)합니다.

#### <a name="adding-the-chart-control-to-an-aspnet-page"></a>ASP.NET 페이지에 차트 컨트롤 추가

추가 하는 방법을 보여 주는 다음 예제는 *차트* 태그를 사용 하 여 ASP.NET 페이지를 제어 합니다. 예제에서는 *차트* 정적 데이터 요소에 대 한 세로 막대형 차트 컨트롤을 생성 합니다.

[!code-aspx[Main](overview/samples/sample58.aspx)]

#### <a name="using-3-d-charts"></a>3 차원 차트를 사용 하 여

*차트* 컨트롤에 포함 되어는 *ChartAreas* 컬렉션을 포함할 수 있는 *ChartArea* 특징 차트의 차트 영역을 정의 하는 개체입니다. 예를 들어 3 차원 차트 영역에 대 한를 사용 하려면 사용 하 여 *Area3DStyle* 다음 예제와 같이 속성:

[!code-aspx[Main](overview/samples/sample59.aspx)]

아래 그림 4 개의 일련의 3 차원 차트는 *모음* 차트 종류입니다.

<a id="0.2_graphic18"></a>![](overview/_static/image2.png)

그림 3: 3 차원 가로 막대형 차트

#### <a name="using-scale-breaks-and-logarithmic-scales"></a>배율 구분선 및 로그 눈금 간격 사용

배율 구분선 및 로그 눈금 간격은 두 가지 추가 숙련도 차트를 추가 하 고 있습니다. 이러한 기능은 특정 차트 영역에 있는 각 축에 있습니다. 예를 들어 차트 영역의 기본 Y 축에 이러한 기능을 사용 하려면 사용 된 *AxisY.IsLogarithmic* 및 *ScaleBreakStyle* 속성에는 *ChartArea* 개체입니다. 다음 코드 조각은 기본 Y 축에 배율 구분선을 사용 하는 방법을 보여 줍니다.

[!code-aspx[Main](overview/samples/sample60.aspx)]

아래 그림에는 사용 하도록 설정 하는 배율 구분선이 있는 Y 축을 보여 줍니다.

<a id="0.2_graphic19"></a>![](overview/_static/image3.png)

그림 4: 배율 구분선

<a id="0.2__QueryExtender"></a><a id="0.2__Toc224729041"></a><a id="0.2__Toc253429264"></a><a id="0.2__Toc243304638"></a>

### <a name="filtering-data-with-the-queryextender-control"></a>QueryExtender 컨트롤을 사용 하 여 데이터를 필터링합니다.

데이터 기반 웹 페이지를 만드는 개발자를 위해는 가장 일반적인 작업 데이터를 필터링 하는 것입니다. 이 일반적으로 수행 된 만들어서 *여기서* 절을 데이터 소스 컨트롤입니다. 이 방법은 복잡할 수 및 일부 경우에는 *여기서* 구문 사용 하는 기본 데이터베이스의 모든 기능을 활용 합니다.

필터링을 더 쉽게 새 있도록 *QueryExtender* 컨트롤이 ASP.NET 4에 추가 되었습니다. 이 컨트롤에 추가할 수 있습니다 *EntityDataSource* 또는 *LinqDataSource* 컨트롤 이러한 컨트롤에 의해 반환 되는 데이터를 필터링 합니다. 때문에 *QueryExtender* LINQ에 의존 하 여, 매우 효율적이 고 작업으로 인해 페이지와 데이터를 보내기 전에 데이터베이스 서버에 필터가 적용 됩니다.

*QueryExtender* 컨트롤에서는 다양 한 필터 옵션을 지원 합니다. 다음 섹션에서는 이러한 옵션에 설명 하 고 사용 하는 방법의 예를 제공 합니다.

#### <a name="search"></a>검색

검색 옵션에 대 한는 *QueryExtender* 컨트롤 지정 된 필드에서 검색을 수행 합니다. 다음 예제에서는 컨트롤 사용 하 여 TextBoxSearch 제어 및 검색에 내용 입력 한 텍스트는 `ProductName` 및 `Supplier.CompanyName` 에서 반환 되는 데이터의에서 열에는 *LinqDataSource* 컨트롤입니다.

[!code-aspx[Main](overview/samples/sample61.aspx)]

#### <a name="range"></a>범위

범위 옵션 검색 옵션과 유사 하지만 범위를 정의 하는 값의 쌍을 지정 합니다. 다음 예제에서는 *QueryExtender* 검색 제어는 `UnitPrice` 에서 반환 된 데이터의 열에에서는 *LinqDataSource* 제어 합니다. 범위는 페이지 TextBoxFrom 및 TextBoxTo 컨트롤에서 읽습니다.

[!code-aspx[Main](overview/samples/sample62.aspx)]

#### <a name="propertyexpression"></a>PropertyExpression

속성 식 옵션 속성 값 비교를 정의할 수 있습니다. 식이 계산 되는 경우 *true*, 검사 되 고 데이터가 반환 됩니다. 다음 예제에서는 *QueryExtender* 컨트롤의 데이터를 비교 하 여 데이터를 필터링는 `Discontinued` 페이지 CheckBoxDiscontinued 컨트롤에서 열 값을 합니다.

[!code-aspx[Main](overview/samples/sample63.aspx)]

#### <a name="customexpression"></a>CustomExpression

마지막으로을 사용 하면 사용자 지정 식을 지정할 수 있습니다는 *QueryExtender* 제어 합니다. 이 옵션에는 사용자 지정 필터 논리를 정의 하는 페이지에는 함수를 호출할 수 있습니다. 다음 예제에서는 사용자 지정 식에 선언적으로 지정 하는 *QueryExtender* 제어 합니다.

[!code-aspx[Main](overview/samples/sample64.aspx)]

다음 예제에서는 사용자 지정 함수에서 호출 하는 *QueryExtender* 제어 합니다. 포함 하는 데이터베이스 쿼리를 사용 하는 대신이 경우에 *여기서* 절, 코드를 사용 하 여 LINQ 쿼리에 데이터를 필터링 합니다.

[!code-csharp[Main](overview/samples/sample65.cs)]

이러한 예와 하나의 식에 사용 되는 *QueryExtender* 한 번에 제어 합니다. 그러나 안에 여러 개의 식을 포함할 수 있습니다는 *QueryExtender* 제어 합니다.

<a id="0.2__Toc253429265"></a><a id="0.2__Toc243304639"></a>

### <a name="html-encoded-code-expressions"></a>Html 인코딩된 코드 식

일부 ASP.NET 사이트 (특히 ASP.NET MVC)와 함께 사용 하 여에 크게 의존 `<%` =  `expression %>` 구문 ("코드 너"이 라고도 함)를 응답에 일부 텍스트를 쓸 수 있습니다. 코드 식을 사용 하면 HTML 인코딩할 텍스트 사용자에서 제공 하는 경우 텍스트를 입력 하는 경우이 페이지를 열어 놓을 수 XSS (교차 사이트 스크립팅) 공격에 잊기 쉽습니다.

ASP.NET 4 아래 코드 식에 대 한 다음 새 구문을 제공합니다.

[!code-aspx[Main](overview/samples/sample66.aspx)]

이 구문은 응답에 쓸 때 기본적으로 HTML 인코딩을 사용 합니다. 이 새 식 다음에 효과적으로 변환.

[!code-aspx[Main](overview/samples/sample67.aspx)]

예를 들어 &lt;%: ["UserInput"] 요청 %&gt; 의 값에 HTML 인코딩을 수행 *["UserInput"] 요청*합니다.

이 기능의 목표를 사용할 모든 단계에서 결정 하는로 강제 되지 않습니다 새 구문을 사용 하 여 이전 구문의 모든 인스턴스를 바꾸려면 수 있게 하는 것입니다. 그러나 경우가 있습니다 출력 하 고 있는 텍스트 HTML 알 수 있도록 또는 이미 인코딩된 이중 인코딩으로 경우 발생할 수 있습니다.

이러한 경우에 대 한 ASP.NET 4에서는 새로운 인터페이스 *IHtmlString*, 구체적 구현 함께 *HtmlString*합니다. 이러한 형식의 인스턴스를 사용 하는 반환 값은 이미 올바르게 인코딩되지 (또는 검사 하 고, 그렇지)를 HTML로 표시 하며 따라서 값 해야 하지 HTML로 인코딩된 다시 지정할 수 있습니다. 예를 들어 다음 수 없습니다 (아니며) 인코딩된 HTML:

[!code-aspx[Main](overview/samples/sample68.aspx)]

ASP.NET MVC 2 도우미 메서드가 ASP.NET 4를 실행 하는 경우에이 새 구문을 함께 사용 없는 이중 인코딩된, 되도록 업데이트 되었습니다. ASP.NET 3.5 s p 1을 사용 하 여 응용 프로그램을 실행 하는 경우에이 새로운 구문의 작동 하지 않습니다.

XSS 공격 으로부터 보호 보장 하지 않습니다이 염두에서에 둬야 합니다. 예를 들어 따옴표에 없는 특성 값을 사용 하는 HTML 여전히 취약 않은 사용자 입력을 포함할 수 있습니다. Note는 ASP.NET 컨트롤 및 ASP.NET MVC 도우미의 출력 항상가 포함 됩니다 특성 값 따옴표에서 방법이 권장된 합니다.

마찬가지로,이 구문을 사용자 입력을 기반으로 하는 JavaScript 문자열을 만들 때와 같은 JavaScript 인코딩을 수행 하지 않습니다.

<a id="0.2__Toc253429266"></a><a id="0.2__Toc243304640"></a>

### <a name="project-template-changes"></a>프로젝트 템플릿 변경 사항

이전 버전의 ASP.NET에서는 Visual Studio를 사용 하 여 새 웹 사이트 프로젝트 또는 웹 응용 프로그램 프로젝트를 만들 때 결과 프로젝트가 포함 되어는 Default.aspx 페이지만 기본 `Web.config` 파일 및 `App_Data` 폴더 아래에 나와 있는 것 처럼 그림:

<a id="0.2_graphic1A"></a>![](overview/_static/image4.png)

Visual Studio는 전혀, 다음 그림에 나와 있는 것 처럼 없는 파일을 포함 하는 빈 웹 사이트 프로젝트 형식을 지원 합니다.

<a id="0.2_graphic1B"></a>![](overview/_static/image5.png)

결과 초보자를 위한에 대 한 지침이 거의에 있는지 프로덕션 웹 응용 프로그램을 작성 하는 방법. 따라서 ASP.NET 4에는 세 개의 새로운 템플릿이, 빈 웹 응용 프로그램 프로젝트 및 각 웹 응용 프로그램 및 웹 사이트 프로젝트에 대 한 소개합니다.

#### <a name="empty-web-application-template"></a>빈 웹 응용 프로그램 템플릿

이름에서 알 수 있듯이 빈 웹 응용 프로그램 템플릿은 축소 웹 응용 프로그램 프로젝트입니다. 다음 그림에 나와 있는 것 처럼 Visual Studio 새 프로젝트 대화 상자에서이 프로젝트 템플릿을 선택 합니다.

[![](overview/_static/image7.png)](overview/_static/image6.png)

([전체 크기 이미지를 보려면 클릭](overview/_static/image8.png))

빈 ASP.NET 웹 응용 프로그램을 만들 때 Visual Studio는 다음 폴더의 레이아웃을 만듭니다.

<a id="0.2_graphic1D"></a>![](overview/_static/image9.png)

이 한 가지 예외로 이전 버전의 ASP.NET 빈 웹 사이트 레이아웃 비슷합니다. 빈 웹 응용 프로그램 및 빈 웹 사이트 프로젝트를 Visual Studio 2010에서 최소한의 다음을 포함 `Web.config` 는 프로젝트의 대상 프레임 워크를 식별 하려면 Visual Studio에서 사용 하는 정보가 포함 된 파일:

<a id="0.2_graphic1E"></a>![](overview/_static/image10.png)

이렇게 하지 않으면 *targetFramework* 속성, 이전 응용 프로그램을 열 때 호환성을 유지 하기 위해.NET Framework 2.0을 대상으로 Visual Studio 기본값입니다.

#### <a name="web-application-and-web-site-project-templates"></a>웹 응용 프로그램 및 웹 사이트 프로젝트 템플릿

다른 두 개의 새 프로젝트 템플릿이 Visual Studio 2010과 함께 제공 되는 주요 변경을 포함 합니다. 다음 그림은 새 웹 응용 프로그램 프로젝트를 만들 때 만들어지는 프로젝트 레이아웃 합니다. (웹 사이트 프로젝트에 대 한 레이아웃은 거의 동일 합니다.)

- <a id="0.2_graphic1F"></a>![](overview/_static/image11.png)

프로젝트에 이전 버전에서 생성 되지 않은 파일의 수를 포함 합니다. 또한 새 웹 응용 프로그램 프로젝트 신속 하 게 새 응용 프로그램에 대 한 액세스를 보호 하기 시작 하면 기본 회원 기능을 통해 구성 됩니다. 이 포함 되어 있어는 `Web.config` 멤버 자격, 역할 및 프로필을 구성 하는 데 사용 되는 항목을 포함 하는 새 프로젝트에 대 한 파일입니다. 다음 예제와 `Web.config` 새 웹 응용 프로그램 프로젝트에 대 한 파일입니다. (이 경우 *roleManager* 을 사용할 수 없습니다.)

[![](overview/_static/image13.png)](overview/_static/image12.png)

([전체 크기 이미지를 보려면 클릭](overview/_static/image14.png))

두 번째 프로젝트에도 포함 되어 `Web.config` 파일에 `Account` 디렉터리입니다. 두 번째 구성 파일 로그 되지 않은 사용자에서에 대 한 ChangePassword.aspx 페이지에 대 한 액세스를 보호 하는 방법을 제공 합니다. 다음 예제에서는 두 번째의 내용을 `Web.config` 파일입니다.

![](overview/_static/image15.png)

새 프로젝트 템플릿이 기본적으로 생성 페이지도 이전 버전에서 보다 더 많은 콘텐츠를 포함 합니다. 기본 마스터 페이지 및 CSS 파일을 포함 하는 프로젝트 및 기본 페이지 (Default.aspx)는 기본적으로 마스터 페이지를 사용 하도록 구성 됩니다. 결과 처음에 대 한 웹 응용 프로그램 또는 웹 사이트를 실행할 때 기본 (홈) 페이지를 이미 기능. 사실, 표시, 새 MVC 응용 프로그램을 시작 하면 기본 페이지로 비슷합니다.

[![](overview/_static/image17.png)](overview/_static/image16.png)

([전체 크기 이미지를 보려면 클릭](overview/_static/image18.png))

프로젝트 템플릿에 대 한 이러한 변경의 의도 새 웹 응용 프로그램 작성을 시작 하는 방법에 지침을 제공 합니다. 엄격한 XHTML 1.0 호환 의미적 태그와 함께 및 CSS를 사용 하 여 지정 된 레이아웃 페이지 서식 파일에 ASP.NET 4 웹 응용 프로그램을 구축 하기 위한 모범 사례를 나타냅니다. 기본 페이지는 쉽게 사용자 지정할 수 있는 2 열 레이아웃을 갖게 됩니다.

예를 들어 새 웹 응용 프로그램에 대 한 고 가정 하는 색 중 일부를 변경 하 고 내 ASP.NET 응용 프로그램 로고가 대신 회사 로고를 삽입 합니다. 아래에 새 디렉터리를 만들면이 위해 `Content` 로고 이미지를 저장할 수 있습니다.

<a id="0.2_graphic23"></a>![](overview/_static/image19.png)

페이지에 이미지를 추가 하려면 다음 엽니다는 `Site.Master` 파일, 내 ASP.NET 응용 프로그램 텍스트 정의 된 위치와 사용 하 여 대체 위치 찾기는 *이미지* 요소 인 *src* 특성은 새 로고로 설정 다음 예제와 같이 이미지:

[![](overview/_static/image21.png)](overview/_static/image20.png)

([전체 크기 이미지를 보려면 클릭](overview/_static/image22.png))

그런 다음 Site.css 파일로 이동 하 고 페이지의 배경색 및 헤더를 변경 하는 CSS 클래스 정의 수정할 수 있습니다.

이러한 변경의 결과 매우 적은 노력으로 사용자 지정된 홈 페이지를 표시할 수 있습니다.

[![](overview/_static/image24.png)](overview/_static/image23.png)

([전체 크기 이미지를 보려면 클릭](overview/_static/image25.png))

<a id="0.2__Toc253429267"></a><a id="0.2__Toc243304641"></a>

### <a name="css-improvements"></a>CSS 개선 사항

최신 HTML 표준을 준수 하는 HTML을 렌더링 하는 데 도움이 되었습니다 ASP.NET 4에는 작업의 주요 영역 중 하나입니다. ASP.NET 웹 서버 컨트롤에서 CSS 스타일을 사용 하는 방법에 대 한 변경 내용이 포함 됩니다.

#### <a name="compatibility-setting-for-rendering"></a>렌더링에 대 한 호환성 설정

웹 응용 프로그램 또는 웹 사이트는.NET Framework 4를 대상으로 하는 경우 기본적으로는 *controlRenderingCompatibilityVersion* 특성에는 *페이지* "4.0"로 설정 된 합니다. 이 요소는 컴퓨터 수준에 정의 된 `Web.config` 파일을 기본적으로 모든 ASP.NET 4 응용 프로그램에 적용 됩니다.

[!code-xml[Main](overview/samples/sample69.xml)]

에 대 한 값 *controlRenderingCompatibility* 는 새 버전의 잠재적인 정의 이후 릴리스에서 수 있는 문자열입니다. 현재 릴리스에서 다음 값이이 속성에 대해 지원 됩니다.

- "3.5". 이 설정은 레거시 렌더링 및 태그를 나타냅니다. 컨트롤에서 렌더링 되는 태그는 100% 호환 및 설정의는 *xhtmlConformance* 속성은 적용 됩니다.
- "4.0". 속성에 있는 경우이 설정은, ASP.NET 웹 서버 컨트롤은 다음을 수행 합니다.
- *xhtmlConformance* 속성은 항상 "Strict"으로 처리 됩니다. 결과적으로, 컨트롤 XHTML 1.0 Strict 태그를 렌더링합니다.
- 잘못 된 스타일을 렌더링 비 입력 컨트롤을 더 이상 사용 하지 않도록 설정 합니다.
- *div* 숨겨진된 필드 주위 요소는 사용자가 만든 CSS 규칙을 방해 하지 않도록 이제 스타일이 지정 합니다.
- 메뉴 컨트롤에 의미가 올바르고 내게 필요한 옵션 지침과 호환 되는 태그를 렌더링 합니다.
- 유효성 검사 컨트롤에는 인라인 스타일 렌더링 되지 않습니다.
- 이전에 테두리를 렌더링 하는 제어 = "0" (ASP.NET에서 파생 된 컨트롤 *테이블* 컨트롤과 ASP.NET *이미지* 컨트롤) 더 이상이 특성을 렌더링 합니다.

#### <a name="disabling-controls"></a>컨트롤을 사용 하지 않도록 설정

ASP.NET 3.5 SP1 및 이전 버전의 프레임 워크 렌더링는 *비활성화* 모든 컨트롤에 대 한 HTML 태그에서 특성 *Enabled* 속성이로 설정 *false*합니다. 그러나 HTML 4.01 사양에 따라 *입력* 요소는이 특성이 있어야 합니다.

ASP.NET 4에서 설정할 수 있습니다는 *controlRenderingCompatabilityVersion* "3.5" 다음 예제와 같이 속성:

[!code-xml[Main](overview/samples/sample70.xml)]

에 대 한 태그를 만들 수 있습니다는 *레이블* 컨트롤을 해제 하는 다음과 같은 제어:

[!code-aspx[Main](overview/samples/sample71.aspx)]

*레이블* 컨트롤 다음 HTML을 렌더링 합니다.

[!code-html[Main](overview/samples/sample72.html)]

ASP.NET 4에서 설정할 수 있습니다는 *controlRenderingCompatabilityVersion* 을 "4.0"입니다. 이 경우에 렌더링 되는 컨트롤 해당 *입력* 요소가 렌더링 됩니다는 *비활성화* 특성 컨트롤의 *Enabled* 속성이로 설정 되어 *false* . HTML 렌더링 되지 않는 컨트롤 *입력* 요소 대신 렌더링 한 *클래스* 컨트롤에 대 한 비활성화 된 모양을 정의 하는 데 사용할 수 있는 CSS 클래스를 참조 하는 특성입니다. 예를 들어는 *레이블* 컨트롤 앞의 예에 표시 된 다음 태그를 생성 합니다.

[!code-html[Main](overview/samples/sample73.html)]

이 컨트롤에 대해 지정 하는 클래스에 대 한 기본값은 "aspnetdisabled 로" 합니다. 그러나 정적 설정 하 여이 기본값을 변경할 수 있습니다 *DisabledCssClass* 의 정적 속성은 *WebControl* 클래스입니다. 컨트롤 개발자가 사용할 특정 컨트롤에 대 한 동작을 정의할 수도 있습니다를 사용 하 여 *SupportsDisabledAttribute* 속성입니다.

<a id="0.2__Toc253429268"></a><a id="0.2__Toc243304642"></a>

### <a name="hiding-div-elements-around-hidden-fields"></a>Div 숨겨진 필드 주위 요소 숨기기

ASP.NET 2.0 및 이후 버전에는 시스템 관련 숨겨진된 필드 렌더링 (같은 *숨겨진* 뷰 상태 정보를 저장 하는 데 사용 되는 요소) 내 *div* XHTML 표준을 준수 하기 위해 요소입니다. 그러나 CSS 규칙에 영향을 주는 문제가 발생할 수이 *div* 페이지의 요소입니다. 예를 들어 1 픽셀 선이 페이지에 표시 될 수 있습니다 약 숨겨진 *div* 요소입니다. ASP.NET 4에서 *div* ASP.NET에서 생성 된 숨겨진된 필드를 포함 하는 요소는 다음 예제와 같이 CSS 클래스 참조를 추가 합니다.

[!code-html[Main](overview/samples/sample74.html)]

다음에 적용 되는 CSS 클래스를 정의할 수 있습니다는 *숨겨진* 다음 예제와 같이 ASP.NET에서 생성 된 요소:

[!code-css[Main](overview/samples/sample75.css)]

<a id="0.2__Toc253429269"></a><a id="0.2__Toc243304643"></a>

### <a name="rendering-an-outer-table-for-templated-controls"></a>템플릿 기반 컨트롤에 대 한 외부 테이블을 렌더링

기본적으로 템플릿을 지 원하는 다음 ASP.NET 웹 서버 컨트롤은 인라인 스타일을 적용 하는 데 사용 되는 외부 테이블에 자동으로 줄:

- *FormView*
- *로그인*
- *PasswordRecovery*
- *암호 변경*
- *마법사*
- *CreateUserWizard*

라는 새 속성이 *RenderOuterTable* 외부 테이블에서 태그를 제거할 수 있도록 이러한 컨트롤에 추가 되었습니다. 예를 들어 다음의 예제는 *FormView* 제어:

[!code-aspx[Main](overview/samples/sample76.aspx)]

이 태그는 HTML 테이블을 포함 하는 페이지에는 다음과 같은 출력을 렌더링 합니다.

[!code-html[Main](overview/samples/sample77.html)]

테이블을 렌더링 되지 않도록 방지 하려면 설정할 수 있습니다는 *FormView* 컨트롤의 *RenderOuterTable* 다음 예제와 같이 속성:

[!code-aspx[Main](overview/samples/sample78.aspx)]

앞의 예제는 다음과 같은 출력 없이 렌더링 된 *테이블*, *tr*, 및 *td* 요소:

> 콘텐츠


이 향상 된이 기능 쉽게 만들 수 css 컨트롤의 콘텐츠 스타일을 컨트롤에 의해 태그가 없습니다. 예기치 않은 렌더링 되기 때문에 있습니다.

> [!NOTE]
> 이 변경은 더 이상 없기 때문에 Visual Studio 2010 디자이너에서 자동 format 함수에 대 한 지원을 사용 하지 않도록 설정 하는 참고는 *테이블* 자동 서식 옵션에 의해 생성 되는 스타일 특성을 호스팅할 수 있는 요소입니다.


<a id="0.2__Toc253429270"></a><a id="0.2__Toc243304644"></a>

### <a name="listview-control-enhancements"></a>ListView 컨트롤의 향상 된 기능

*ListView* 컨트롤이 쉽게 ASP.NET 4에 사용할 수 있게 되었습니다. 컨트롤의 이전 버전 알려진 id 서버 컨트롤이 포함 된 레이아웃 템플릿을 지정 하는 데 필요한 다음 태그를 사용 하는 방법의 일반적인 예를 보여 줍니다.는 *ListView* ASP.NET 3.5에서 제어 합니다.

[!code-aspx[Main](overview/samples/sample79.aspx)]

ASP.NET 4에서는 *ListView* 컨트롤 레이아웃 템플릿에 필요 하지 않습니다. 앞의 예제에 나와 있는 태그를 다음 태그로 바꿀 수 있습니다.

[!code-aspx[Main](overview/samples/sample80.aspx)]

<a id="0.2__Toc253429271"></a><a id="0.2__Toc243304645"></a>

### <a name="checkboxlist-and-radiobuttonlist-control-enhancements"></a>CheckBoxList 및 RadioButtonList 컨트롤 향상 된 기능

ASP.NET 3.5에서에 대 한 레이아웃을 지정할 수 있습니다는 *CheckBoxList* 및 *RadioButtonList* 다음 두 가지 설정을 사용 하 여:

- *흐름*합니다. 컨트롤 렌더링 *걸쳐* 요소를 사용 하는 콘텐츠를 포함 합니다.
- *테이블*합니다. 컨트롤 렌더링을 *테이블* 해당 콘텐츠를 포함 하는 요소입니다.

다음 예제에서는 이러한 각 컨트롤에 대 한 태그를 보여 줍니다.

[!code-aspx[Main](overview/samples/sample81.aspx)]

기본적으로 컨트롤을 렌더링 HTML 다음과 비슷합니다.

[!code-html[Main](overview/samples/sample82.html)]

HTML 목록을 사용 하 여 해당 콘텐츠를 렌더링 해야 이러한 컨트롤 의미적으로 HTML을 렌더링할 항목의 목록이 포함 되어 있으므로 (*li*) 요소입니다. 이렇게 하면 보조 기술을 사용 하 여 웹 페이지를 읽고 컨트롤을 더 쉽게 스타일 CSS를 사용할 수 있는 사용자에 대 한 쉽게 합니다.

ASP.NET 4에서는 *CheckBoxList* 및 *RadioButtonList* 컨트롤 지원에 대 한 다음 새 값은 *RepeatLayout* 속성:

- *OrderedList* –으로 콘텐츠는 *li* 내에서 요소는 *ol* 요소입니다.
- *UnorderedList* –으로 콘텐츠는 *li* 내에서 요소는 *ul* 요소입니다.

다음 예제에서는 이러한 새 값을 사용 하는 방법을 보여 줍니다.

[!code-aspx[Main](overview/samples/sample83.aspx)]

위의 태그에서는 다음 HTML을 생성합니다.

[!code-html[Main](overview/samples/sample84.html)]

> [!NOTE]
> 설정할 경우 *RepeatLayout* 를 *OrderedList* 또는 *UnorderedList*, *RepeatDirection* 속성이 더 이상 사용할 수 있으며 됩니다 태그 또는 코드 내에서 속성이 설정 된 경우 런타임 시 예외를 throw 합니다. 이러한 컨트롤의 시각적 레이아웃은 CSS를 대신 사용 하 여 정의 되었기 때문에 속성 값이 없는 것입니다.


<a id="0.2__Toc253429272"></a><a id="0.2__Toc243304646"></a>

### <a name="menu-control-improvements"></a>메뉴 컨트롤 향상 기능

ASP.NET 4 하기 전에 *메뉴* 컨트롤이 일련의 HTML 테이블을 렌더링 합니다. 이 인라인 속성을 설정 하는 외부 CSS 스타일을 적용 하려면 어려웠습니다 있고 없기도 내게 필요한 옵션 표준 규격인 펌웨어.

컨트롤은 ASP.NET 4에서 이제 목록 요소 및 순서가 지정 되지 않은 목록으로 구성 된 의미 체계 태그를 사용 하 여 HTML을 렌더링 합니다. 다음 예제에 대 한 ASP.NET 페이지의 태그를 보여 줍니다.는 *메뉴* 제어 합니다.

[!code-aspx[Main](overview/samples/sample85.aspx)]

컨트롤 다음 HTML 페이지가 렌더링 되 면 생성 (의 *onclick* 명확성에 대 한 코드는 생략):

[!code-html[Main](overview/samples/sample86.html)]

렌더링 개선 사항 외에도 키보드 탐색 메뉴의 늘었습니다 포커스 관리를 사용 하 여. 경우는 *메뉴* 컨트롤에 포커스를 받을 경우 요소를 이동 하려면 화살표 키를 사용할 수 있습니다. *메뉴* 컨트롤 이제 액세스할 수 있는 리치 인터넷 응용 프로그램 (ARIA) 역할을 연결 및 특성을 앞[측 벽의](http://www.w3.org/TR/wai-aria-practices/#menu "메뉴 ARIA 지침")를 개선 하기 위해 액세스 가능성입니다.

메뉴 컨트롤에 스타일을 스타일 블록에서 맨 위쪽에 렌더링 된 HTML 요소와 같은 줄이 아닌는 페이지의 렌더링 됩니다. 컨트롤에 대 한 스타일 지정을 통해 완전히 제어 하려는 경우 새 설정할 수 *IncludeStyleBlock* 속성을 *false*, 스타일 블록 내보내지 않는 경우. 이 속성을 사용 하는 한 가지 방법은 메뉴의 모양을 설정 하는 Visual Studio 디자이너에서 자동 서식 기능을 사용 하는 것입니다. 페이지를 실행 하 고 페이지 소스를 열어 다음 외부 CSS 파일에 렌더링 된 스타일 블록을 복사 후 합니다. Visual Studio에서 실행 취소 스타일 지정 및 집합 *IncludeStyleBlock* 를 *false*합니다. 결과 메뉴가 표시 되도록 외부 스타일 시트에 스타일을 사용 하 여 정의 됩니다.

<a id="0.2__Toc253429273"></a><a id="0.2__Toc243304647"></a>

### <a name="wizard-and-createuserwizard-controls"></a>마법사 및 CreateUserWizard 컨트롤

ASP.NET *마법사* 및 *CreateUserWizard* 컨트롤 렌더링 하는 HTML을 정의할 수 있는 서식 파일을 지원 합니다. (*CreateUserWizard* 에서 파생 *마법사*.) 다음 예제에서는 완벽 하 게 템플릿 기반에 대 한 태그 *CreateUserWizard* 제어:

[!code-aspx[Main](overview/samples/sample87.aspx)]

컨트롤 다음과 유사한 HTML을 렌더링합니다.

[!code-html[Main](overview/samples/sample88.html)]

ASP.NET 3.5 s p 1에서 템플릿 내용을 변경할 수 있지만 여전히 제한의 출력에 대 한 제어는 *마법사* 제어 합니다. ASP.NET 4에서 만들 수 있습니다는 *LayoutTemplate* 템플릿과 삽입 *자리 표시자* 방법을 지정할 수 있습니다 (예약 된 이름 사용)을 제어는 *Wizard 컨트롤* 렌더링 합니다. 다음 예제에서는이 보여 줍니다.

[!code-aspx[Main](overview/samples/sample89.aspx)]

이 예제에서는 명명 된 자리 표시자에는 다음이 포함 된 *LayoutTemplate* 요소:

- *headerPlaceholder* – 실행 시의 내용으로 대체 됩니다이 *HeaderTemplate* 요소입니다.
- *sideBarPlaceholder* – 실행 시의 내용으로 대체 됩니다이 *SideBarTemplate* 요소입니다.
- *wizardStepPlaceHolder* – 실행 시의 내용으로 대체 됩니다이 *WizardStepTemplate* 요소입니다.
- *navigationPlaceholder* – 런타임 시 사용자가 정의한 모든 탐색 템플릿에 의해 대체 됩니다이 있습니다.

자리 표시자를 사용 하는 예에서는 태그 (실제로 템플릿에 정의 된 콘텐츠) 없이 다음 HTML을 렌더링 합니다.

[!code-html[Main](overview/samples/sample90.html)]

이제 사용자 정의 문자열이 아닌지만 HTML이는 *걸쳐* 요소입니다. (예상는 이후 릴리스에서도 *걸쳐* 요소 렌더링 되지 것입니다.) 이 구문은 이제에서 생성 되는 거의 모든 콘텐츠에 대 한 모든 권한을 제공는 *마법사* 제어 합니다.

<a id="0.2_dyndata"></a><a id="0.2__Toc253429274"></a><a id="0.2__Toc243304648"></a><a id="0.2__Toc224729042"></a>

## <a name="aspnet-mvc"></a>ASP.NET MVC

ASP.NET MVC 2009 년 3 월에에서 추가 기능 프레임 워크로 ASP.NET 3.5 s p 1에 도입 되었습니다. Visual Studio 2010 새로운 특징과 기능을 포함 하는 ASP.NET MVC 2를 포함 합니다.

<a id="0.2__Toc253429275"></a>

### <a name="areas-support"></a>영역 지원

영역을 사용 하면 다른 섹션에서 상대 격리 상태에서 대형 응용 프로그램의 섹션으로 그룹 컨트롤러와 뷰 있습니다. 각 영역으로 주 응용 프로그램에서 참조 될 수 있는 별도 ASP.NET MVC 프로젝트를 구현할 수 있습니다. 대형 응용 프로그램을 빌드할 때 복잡해 지지 않도록 관리 고 여러 팀의 단일 응용 프로그램에서 함께 작동을 보다 쉽게 있습니다.

<a id="0.2__Toc253429276"></a>

### <a name="data-annotation-attribute-validation-support"></a>데이터 주석을 특성 유효성 검사 지원

*DataAnnotations* 특성을 사용 하는 메타 데이터 특성을 사용 하 여 유효성 검사 논리 모델에 연결할 수 있습니다. *DataAnnotations* 특성 ASP.NET Dynamic Data ASP.NET 3.5 s p 1에서에서 도입 되었습니다. 이러한 특성 기본 모델 바인더에 통합 되 고 사용자 입력의 유효성을 검사 하는 메타 데이터 기반 방법을 제공 합니다.

<a id="0.2__Toc253429277"></a>

### <a name="templated-helpers"></a>템플릿 기반 도우미

템플릿 기반 도우미 사용 하 여 자동으로 연결 편집 및 데이터 유형과 서식 파일을 표시 합니다. 예를 들어 날짜 선택 UI 요소에 대 한 자동으로 렌더링 됨을 지정 하는 템플릿 도우미를 사용할 수 있습니다는 *System.DateTime* 값입니다. ASP.NET Dynamic Data에 필드 템플릿에 것과 비슷합니다.

*Html.EditorFor* 및 *Html.DisplayFor* 여러 속성을 가진도 같이 복잡 한 개체 형식 표준 데이터 렌더링에 대 한 도우미 메서드는 기본 제공 지원 합니다. 또한 렌더링을 사용자 지정와 같은 데이터 주석을 특성을 적용할 수 있도록 하 여 *DisplayName* 및 *ScaffoldColumn* 에 *ViewModel* 개체입니다.

종종 하려는 UI 도우미를 더욱 해소에서 출력을 사용자 지정 생성 내용을 완전히 제어 합니다. *Html.EditorFor* 및 *Html.DisplayFor* 도우미 메서드를 지원이 재정의할 수 있는 외부 서식 파일 및 렌더링 된 출력 제어를 정의할 수 있는 템플릿 메커니즘을 사용 합니다. 클래스에 대 한 서식 파일을 개별적으로 렌더링할 수 있습니다.

<a id="0.2__Toc253429278"></a><a id="0.2__Toc243304649"></a>

## <a name="dynamic-data"></a>Dynamic Data

동적 데이터 도입 된 중순 2008의.NET Framework 3.5 SP1 릴리스에서 합니다. 이 기능은 다음을 포함 하는 데이터 기반 응용 프로그램을 만들기 위한 많은 향상 된 기능을 제공 합니다.

- 데이터 기반 웹 사이트를 신속 하 게 빌드하기 위한 RAD 경험 합니다.
- 데이터 모델에 정의 된 제약 조건에 따라 자동 유효성 검사 합니다.
- 필드에 대해 생성 되는 태그를 쉽게 변경할 수는 *GridView* 및 *DetailsView* 동적 데이터 프로젝트의 일부인 필드 템플릿을 사용 하 여 제어 합니다.

> [!NOTE]
> 자세한 내용은 참고를 참조 하십시오는 [동적 데이터 설명서](https://msdn.microsoft.com/en-us/library/cc488545.aspx) MSDN 라이브러리에서.


ASP.NET 4에 대 한 동적 데이터 신속 하 게 데이터 기반 웹 사이트를 구축 하기 위한 개발자에 게 더 많은 전원을 제공 하도록 향상 되었습니다.

<a id="0.2__Toc253429279"></a><a id="0.2__Toc243304650"></a>

### <a name="enabling-dynamic-data-for-existing-projects"></a>기존 프로젝트에 대 한 동적 데이터 사용

.NET Framework 3.5 s p 1에서 제공 되는 동적 데이터 기능 다음과 같은 새로운 기능으로 전환 합니다.

- 필드 템플릿 – 데이터 바인딩된 컨트롤에 대 한 데이터 형식을 기반으로 템플릿을 제공합니다. 필드 템플릿은 템플릿 필드를 사용 하 여 각 필드에 대 한 보다 데이터 컨트롤의 모양을 사용자 지정 하는 보다 간단한 방법을 제공 합니다.
- 유효성 검사-동적 데이터 사용 하면 특성 데이터 클래스에 필수 필드, 범위 검사, 형식 검사, 패턴 정규식을 사용 하 여 일치와 같은 일반적인 시나리오에 대 한 유효성 검사 및 사용자 지정 유효성 검사를 지정 하려면. 유효성 검사는 데이터 컨트롤에 의해 적용 됩니다.

그러나 이러한 기능에는 다음 요구 사항이 있었습니다.

- 데이터 액세스 계층 Entity Framework 또는 LINQ to SQL 기반으로 해야 했습니다.
- 유일한 데이터 원본 이러한 기능에 대해 지원 되는 컨트롤의 *EntityDataSource* 또는 *LinqDataSource* 컨트롤입니다.
- 기능으로 만들어진 동적 데이터 또는 동적 데이터 엔터티 서식 파일을 사용 하 여 기능을 지원 해야 하는 모든 파일을 가지려면 웹 프로젝트를 필요 합니다.

ASP.NET 4에서 동적 데이터 지원의 주요 목표는 모든 ASP.NET 응용 프로그램에 대 한 동적 데이터의 새 기능을 사용 하도록 합니다. 다음 예제에서는 기존 페이지의 동적 데이터 기능을 사용할 수 있는 컨트롤에 대 한 태그를 보여 줍니다.

[!code-aspx[Main](overview/samples/sample91.aspx)]

페이지에 대 한 코드를에서 이러한 컨트롤에 대 한 동적 데이터 지원 사용 하기 위해 다음 코드를 추가 해야 합니다.

[!code-csharp[Main](overview/samples/sample92.cs)]

경우는 *GridView* 컨트롤 편집 모드에 있으면 동적 데이터를 자동으로 입력 한 데이터가 올바른 형식 인지 확인 합니다. 그렇지 않은 경우 오류 메시지가 표시 됩니다.

삽입 모드를 값에 대 한 기본값을 지정할 수 있는 등,이 기능은 또한의 기타 유용한 기능을 제공 합니다. 동적 데이터 없이 필드에 대 한 기본값을 구현 하 있습니다 해야 이벤트에, 연결 컨트롤 찾기 (사용 하 여 *FindControl*), 값을 설정 합니다. ASP.NET 4에서는 *EnableDynamicData* 호출이이 예제에 나와 있는 것 처럼 개체에서 모든 필드에 대 한 기본 값을 전달할 수 있도록 하는 두 번째 매개 변수를 지원 합니다.

[!code-csharp[Main](overview/samples/sample93.cs)]

<a id="0.2__Toc224729043"></a><a id="0.2__Toc253429280"></a><a id="0.2__Toc243304651"></a>

### <a name="declarative-dynamicdatamanager-control-syntax"></a>DynamicDataManager 컨트롤 선언적 구문

*DynamicDataManager* 선언적으로 구성할 수 있도록 개선 되었습니다 컨트롤 코드 에서만 대신 asp.net에서 대부분의 컨트롤와 마찬가지로 합니다. 에 대 한 태그는 *DynamicDataManager* 제어는 다음 예제와 같습니다.

[!code-aspx[Main](overview/samples/sample94.aspx)]

참조 되는 GridView1 컨트롤에 대 한 동적 데이터 동작을 사용 하는이 태그는 *DataControls* 의 섹션에서 *DynamicDataManager* 제어 합니다.

<a id="0.2__Toc224729044"></a><a id="0.2__Toc253429281"></a><a id="0.2__Toc243304652"></a>

### <a name="entity-templates"></a>엔터티 서식 파일

엔터티 서식 파일을 사용자 지정 페이지를 만들 필요 없이 데이터의 레이아웃을 사용자 지정 하는 새로운 방법을 제공 합니다. 템플릿을 사용 하 여 페이지는 *FormView* 컨트롤 (대신는 *DetailsView* 동적 데이터의 이전 버전의 페이지 서식 파일에서 사용 되는 제어) 및 *DynamicEntity* 엔터티 서식 파일을 렌더링 하는 컨트롤입니다. 동적 데이터를 통해 렌더링 되는 태그를 더 제어할 수 있습니다.

다음 목록에는 엔터티 템플릿에 포함 된 새 프로젝트 디렉터리 레이아웃을 보여 줍니다.

[!code-console[Main](overview/samples/sample95.cmd)]

`EntityTemplate` 디렉터리 데이터 모델 개체를 표시 하는 방법에 대 한 템플릿을 포함 합니다. 기본적으로 개체를 사용 하 여 렌더링는 `Default.ascx` 가 만든 피드백과 같은 태그를 제공 하는 서식 파일은 *DetailsView* ASP.NET 3.5 s p 1에 동적 데이터를 사용 하는 컨트롤입니다. 다음 예제에 대 한 태그는 `Default.ascx` 제어:

[!code-aspx[Main](overview/samples/sample96.aspx)]

전체 사이트에 대 한 디자인을 변경 하려면 기본 템플릿은 편집할 수 있습니다. 표시, 편집 및 삽입 작업에 대 한 템플릿이 있습니다. 새 템플릿은 추가할 수 있습니다는 데이터 개체의 이름에 따라 한 가지 유형의 개체의 모양과 느낌을 변경 하려면. 예를 들어 다음 템플릿을 추가할 수 있습니다.

[!code-console[Main](overview/samples/sample97.cmd)]

서식 파일에 다음 태그를 포함할 수 있습니다.

[!code-aspx[Main](overview/samples/sample98.aspx)]

새 엔터티 템플릿에 새를 사용 하 여 한 페이지에 표시 됩니다 *DynamicEntity* 제어 합니다. 런타임 시이 컨트롤은 엔터티 서식 파일의 내용으로 대체 됩니다. 에서는 다음 태그는 *FormView* 컨트롤에 `Detail.aspx` 엔터티 서식 파일을 사용 하는 페이지 서식 파일입니다. 공지는 *DynamicEntity* 태그 요소에에서 있습니다.

[!code-aspx[Main](overview/samples/sample99.aspx)]

<a id="0.2__Toc224729045"></a><a id="0.2__Toc253429282"></a><a id="0.2__Toc243304653"></a>

### <a name="new-field-templates-for-urls-and-e-mail-addresses"></a>Url 및 전자 메일 주소에 대 한 새 필드 템플릿

ASP.NET 4에서는 두 개의 새로운 기본 제공 필드 템플릿을 `EmailAddress.ascx` 및 `Url.ascx`합니다. 이러한 템플릿은으로 표시 된 필드에 사용 됩니다 *EmailAddress* 또는 *Url* 와 *DataType* 특성입니다. 에 대 한 *EmailAddress* 개체를 사용 하 여 만든 하이퍼링크로 필드가 표시 됩니다는 *mailto:* 프로토콜입니다. 사용자가 링크를 클릭 하면 사용자의 전자 메일 클라이언트 열리고 기본 메시지가 만들어집니다. 로 형식화 된 개체가 *Url* 일반 하이퍼링크로 표시 됩니다.

다음 예제에서는 필드가 표시 되는 방법을 보여 줍니다.

[!code-csharp[Main](overview/samples/sample100.cs)]

<a id="0.2__Toc224729046"></a><a id="0.2__Toc253429283"></a><a id="0.2__Toc243304654"></a>

### <a name="creating-links-with-the-dynamichyperlink-control"></a>DynamicHyperLink 컨트롤을 사용 하 여 링크 만들기

Dynamic Data 웹 사이트에 액세스할 때 최종 사용자에 게 표시 하는 Url을 제어 하려면.NET Framework 3.5 SP1에서 추가 된 새 라우팅 기능을 사용 합니다. 새 *DynamicHyperLink* 컨트롤을 사용 하면 손쉽게 데이터 동적 사이트의 페이지에 대 한 링크를 만들 수 있습니다. 사용 하는 방법을 보여 주는 다음 예제는 *DynamicHyperLink* 제어:

[!code-aspx[Main](overview/samples/sample101.aspx)]

이 태그에 대 한 목록 페이지를 가리키는 링크를 만듭니다.는 `Products` 테이블에 정의 된 경로에 따라는 `Global.asax` 파일입니다. 컨트롤에는 자동으로 동적 데이터 페이지를 기반으로 하는 기본 테이블 이름을 사용 합니다.

<a id="0.2__Toc224729047"></a><a id="0.2__Toc253429284"></a><a id="0.2__Toc243304655"></a>

### <a name="support-for-inheritance-in-the-data-model"></a>데이터 모델의 상속에 대 한 지원

Entity Framework와 LINQ to SQL 해당 데이터 모델에서 상속을 지원합니다. 이러한 예에 있는 데이터베이스 수 있습니다는 `InsurancePolicy` 테이블입니다. 들어 있을 수도 있습니다 `CarPolicy` 및 `HousePolicy` 동일한 필드를이 있는 테이블 `InsurancePolicy` 다음 더 많은 필드를 추가 합니다. 동적 데이터 데이터 모델에서 상속 된 개체를 이해 하 고 상속된 된 테이블에 대 한 스 캐 폴딩을 지원 하도록 수정 되었습니다.

<a id="0.2__Toc224729048"></a><a id="0.2__Toc253429285"></a><a id="0.2__Toc243304656"></a>

### <a name="support-for-many-to-many-relationships-entity-framework-only"></a>다 대 다 관계 (Entity Framework에만 해당)에 대 한 지원

Entity Framework에서 컬렉션으로 관계를 노출 하 여 구현 하는 테이블 간에 다 대 다 관계에 대 한 다양 한 지원에는 *엔터티* 개체입니다. 새 `ManyToMany.ascx` 및 `ManyToMany_Edit.ascx` 지원을 제공 하기 위해 다 대 다 관계에 관련 데이터 표시 및 편집에 대 한 필드 템플릿이 추가 되었습니다.

<a id="0.2__Toc224729049"></a><a id="0.2__Toc253429286"></a><a id="0.2__Toc243304657"></a>

### <a name="new-attributes-to-control-display-and-support-enumerations"></a>새 특성을 제어 표시 및 지원 열거형

*DisplayAttribute* 하 게 추가 필드가 표시 되는 방식을 제어에 추가 되었습니다. *DisplayName* 특성 이전 버전의 동적 데이터 필드에 대 한 캡션으로 사용 되는 이름을 변경 하는 데 사용할 수 있습니다. 새 *DisplayAttribute* 클래스 필드를 필터로 사용 되는지 여부 및 필드가 표시 되는 순서와 같은 필드를 표시 하기 위한 옵션을 추가로 지정할 수 있습니다. 특성의 레이블에 사용 되는 이름의 독립적으로 제어할 제공는 *GridView* 제어에 사용 된은 *DetailsView* 는 필드에 대 한 도움말 텍스트를 제어 하 고에 사용 되는 워터 마크는 필드 (텍스트 입력 필드에서 허용) 하는 경우입니다.

*EnumDataTypeAttribute* 클래스 필드 열거형에 매핑할 수 있도록에 추가 되었습니다. 필드에이 특성을 적용 하는 경우 열거형 형식을 지정 합니다. 동적 데이터를 사용 하 여 새 `Enumeration.ascx` 필드 템플릿을 표시 하 고 열거형 값을 편집에 대 한 UI를 만듭니다. 서식 파일 열거형의 이름으로 데이터베이스에서 값을 매핑합니다.

<a id="0.2__Toc224729050"></a><a id="0.2__Toc253429287"></a><a id="0.2__Toc243304658"></a>

### <a name="enhanced-support-for-filters"></a>필터에 대 한 향상 된 지원

동적 데이터 1.0 부울 열과 외래 키 열에 대 한 기본 제공 필터와 함께 제공 합니다. 필터가 있는지 여부를 표시 하기 또는 표시 된 순서에서를 지정할 수 없습니다. 새 *DisplayAttribute* 특성 모두의 주소 제공 하 여 이러한 문제를 필터로 열 표시 되는지 여부를 통해 제어 하 고 순서에 표시 됩니다.

향상 된 추가 기능 지원 필터링 되었는지 다시은[새을 사용 하도록 작성](#0.2__QueryExtender "_QueryExtender") Web Forms의 기능입니다. 이 필터는 함께 사용 될 데이터 소스 컨트롤의 한 지식 없이 필터를 만들 수 있습니다. 이러한 확장과 함께 필터 변환 되었으므로 템플릿 컨트롤로 새로 추가할 수 있습니다. 마지막으로 *DisplayAttribute* 앞에서 언급 한 클래스를 통해 동일한에서 재정의 되도록 기본 필터 방식으로 *UIHint* 를 재정의할 수 열에 대 한 기본 필드 템플릿이 있습니다.

<a id="0.2__Toc224729051"></a><a id="0.2__Toc253429288"></a><a id="0.2__Toc243304659"></a>

## <a name="visual-studio-2010-web-development-improvements"></a>Visual Studio 2010 웹 개발 기능 향상

Visual Studio 2010에서 웹 개발 CSS 호환성, HTML 및 ASP.NET 마크업 코드 조각 및 새 동적 IntelliSense JavaScript를 통해 생산성 향상 되었습니다.

<a id="0.2__Toc224729052"></a><a id="0.2__Toc253429289"></a><a id="0.2__Toc243304660"></a>

### <a name="improved-css-compatibility"></a>향상 된 CSS 호환성

Visual Studio 2010의 Visual Web Developer 디자이너 CSS 2.1 표준 준수를 개선 하기 위해 업데이트 되었습니다. 더 잘 디자이너의 HTML 소스의 무결성을 유지 하 고 이전 버전의 Visual Studio 보다 더 강력 합니다. 내부적으로 아키텍처도 향상 되었습니다 렌더링, 레이아웃 및 서비스 효율성의 이후 향상 된 가능 하도록 해당 됩니다.

<a id="0.2__Toc224729053"></a><a id="0.2__Toc253429290"></a><a id="0.2__Toc243304661"></a>

### <a name="html-and-javascript-snippets"></a>HTML 및 JavaScript 코드 조각

HTML 편집기에서 IntelliSense 자동 완성 태그 이름입니다. IntelliSense 코드 조각 기능 자동 완성 전체 태그 등입니다. Visual Studio 2010의 IntelliSense 코드 조각 javascript, C# 및 Visual Basic의 경우 이전 버전의 Visual Studio에서 지원 되므로 함께 사용할 수 있습니다.

Visual Studio 2010 자동 완성 일반적인 ASP.NET 및 HTML 태그를 필수 특성을 포함 하는 데 도움이 되는 200 개가 넘는 코드 조각을 포함 (같은 runat = "server") 및 특정 태그에 공통 특성 (같은 *ID*,  *DataSourceID*, *ControlToValidate*, 및 *텍스트*).

코드 조각 추가, 다운로드 하거나 일반적인 작업에 대 한 사용자 또는 팀에서 사용 하는 태그의 블록을 캡슐화 하는 사용자 고유의 조각을 작성할 수 있습니다.

<a id="0.2__Toc224729054"></a><a id="0.2__Toc253429291"></a><a id="0.2__Toc243304662"></a>

### <a name="javascript-intellisense-enhancements"></a>JavaScript IntelliSense의 향상 된 기능

Visual 2010에서는 JavaScript IntelliSense도 다양 한 편집 환경을 제공할 수 있도록 다시 디자인 되었습니다. IntelliSense에서 동적으로 생성 된 메서드를 통해와 같은 개체를 이제 인식 *registerNamespace* 유사한 방법을 다른 JavaScript 프레임 워크에서 사용 하 여 합니다. 대용량 스크립트 라이브러리를 분석 하 고 IntelliSense를 거의 또는 전혀 처리 지연 표시 성능이 향상 되었습니다. 거의 모든 타사 라이브러리를 지원 하 고 다양 한 코딩 스타일을 지원 하도록 호환성 크게 증가 되었습니다. 문서 주석은 입력 하 고 즉시 IntelliSense에서 활용 됩니다 이제 구문 분석 됩니다.

<a id="0.2__Toc224729055"></a><a id="0.2__Toc253429292"></a><a id="0.2__Toc243304663"></a>

## <a name="web-application-deployment-with-visual-studio-2010"></a>Visual Studio 2010 웹 응용 프로그램 배포

ASP.NET 개발자는 웹 응용 프로그램을 배포 하는 경우 종종을 찾게 나올 하면 다음과 같은 문제:

- 공유 호스팅 사이트에 배포 하려면 느릴 수 있는 FTP 등의 기술 합니다. 또한 데이터베이스를 구성 하는 SQL 스크립트를 실행 하는 등 작업을 수동으로 수행 해야 하 고 응용 프로그램으로 가상 디렉터리 폴더를 구성 하는 등의 IIS 설정을 변경 해야 합니다.
- 웹 응용 프로그램 파일을 배포 하는 것 외에도, 엔터프라이즈 환경에서 관리자가 자주 해야 ASP.NET 구성 파일 및 IIS 설정을 수정 합니다. 데이터베이스 관리자는 일련의 실행 중인 응용 프로그램 데이터베이스를 가져올 SQL 스크립트를 실행 해야 합니다. 이러한 설치는 많은 수동 작업, 종종를 완료 하는 데 시간이 걸릴 신중 하 게 문서화 해야 합니다.

Visual Studio 2010에는 이러한 문제를 해결 하 고 웹 응용 프로그램을 원활 하 게 배포할 수 있는 기술이 포함 되어 있습니다. 이러한 기술 중 하나는 IIS 웹 배포 도구 (MsDeploy.exe)입니다.

Visual Studio 2010의 웹 배포 기능에는 다음과 같은 주요 영역이 포함:

- 웹 패키징
- Web.config 변환
- 데이터베이스 배포
- 웹 응용 프로그램에 대 한 one-click 게시

다음 섹션에서는 이러한 기능에 대 한 세부 정보를 제공 합니다.

<a id="0.2__Toc224729056"></a><a id="0.2__Toc253429293"></a><a id="0.2__Toc243304664"></a>

### <a name="web-packaging"></a>웹 패키징

Visual Studio 2010가 MSDeploy 도구를 사용 하 여 응용 프로그램으로 참조 되는 압축된 (.zip) 파일을 만듭니다는 *웹 패키지*합니다. 다음 콘텐츠 및 응용 프로그램에 대 한 메타 데이터를 포함 하는 패키지 파일:

- 응용 프로그램 풀 설정, 오류 페이지 설정 및에 포함 된 IIS 설정입니다.
- 실제 웹 콘텐츠: 웹 페이지, 사용자 정의 컨트롤, 정적 콘텐츠 (이미지 및 HTML 파일) 및 등을 포함 합니다.
- SQL Server 데이터베이스 스키마 및 데이터입니다.
- 보안 인증서, GAC, 레지스트리 설정, 및 등에서 설치할 구성 요소입니다.

웹 패키지 모든 서버에 복사 하 고 IIS 관리자를 사용 하 여 수동으로 설치 될 수 있습니다. 또는 자동화 된 배포 명령줄 명령을 사용 하 여 또는 배포 Api를 사용 하 여 패키지 설치할 수 있습니다.

Visual Studio 2010 기본 제공 웹 패키지를 만들 대상 및 MSBuild 작업을 제공 합니다. 자세한 내용은 참조 [ASP.NET 웹 응용 프로그램 프로젝트 배포 개요](https://msdn.microsoft.com/en-us/library/dd394698%28VS.100%29.aspx) MSDN 웹 사이트 및 [웹 패키지를 만들어야 하면 10 + 20 이유](http://vishaljoshi.blogspot.com/2009/07/10-20-reasons-why-you-should-create-web.html) Vishal Joshi 블로그.

<a id="0.2__Toc224729057"></a><a id="0.2__Toc253429294"></a><a id="0.2__Toc243304665"></a>

### <a name="webconfig-transformation"></a>Web.config 변환

Visual Studio 2010 웹 응용 프로그램 배포에 대 한 소개 [XML 문서 변환 (XDT)](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html), 변형할 수 있는 한 기능인는 `Web.config` 개발 설정에서 파일을 프로덕션 설정 합니다. 변환 설정은 명명 된 변환 파일에 지정 되어 `web.debug.config`, `web.release.config`등입니다. (이러한 파일의 이름은 MSBuild 구성과 일치 합니다.) 변환 파일 포함 하는 배포 된을 해야 하는 변경 내용을 `Web.config` 파일입니다. 간단한 구문을 사용 하 여 변경 내용을 지정 합니다.

다음 예제에서는의 일부는 `web.release.config` 릴리스 구성의 배포에 대 한 파일 생성 될 수 있습니다. 대체 키워드 예에서 배포 하는 동안 지정는 *connectionString* 의 노드는 `Web.config` 파일 예제에 나와 있는 값으로 대체 됩니다.

[!code-xml[Main](overview/samples/sample102.xml)]

자세한 내용은 참조 [웹 응용 프로그램 프로젝트 배포에 대 한 Web.config 변환 구문은](https://msdn.microsoft.com/en-us/library/dd465326%28VS.100%29.aspx) msdn <a id="0.2_a"> </a> 웹 사이트 및[웹 배포: Web.Config 변환](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html)Vishal Joshi 블로그.

<a id="0.2__Toc224729058"></a><a id="0.2__Toc253429295"></a><a id="0.2__Toc243304666"></a>

### <a name="database-deployment"></a>데이터베이스 배포

Visual Studio 2010 배포 패키지를 SQL Server 데이터베이스에 대 한 종속성을 포함할 수 있습니다. 패키지 정의의 일부로 원본 데이터베이스에 대 한 연결 문자열을 제공합니다. 웹 패키지를 만들 때 Visual Studio 2010와 필요에 따라 데이터를 데이터베이스 스키마에 대 한 SQL 스크립트 생성 및 패키지에 추가 합니다. 사용자 지정 SQL 스크립트를 제공 하 고 서버에서 실행 해야 하는 순서를 지정할 수도 있습니다. 대상 서버에 대 한 적절 한 연결 문자열로 제공 하는 배포 시 배포 프로세스는 다음이 연결 문자열 사용 하 여 데이터베이스 스키마를 만들고 데이터를 추가 하는 스크립트를 실행 합니다.

또한 한 번의 클릭을 사용 하 여 게시, 배포 응용 프로그램 원격 공유 호스팅 사이트에 게시 되 면 데이터베이스를 직접 게시할 수를 구성할 수 있습니다. 자세한 내용은 참조 [하는 방법: 한 데이터베이스와 웹 응용 프로그램 프로젝트를 배포](https://msdn.microsoft.com/en-us/library/dd465343%28VS.100%29.aspx) MSDN 웹 사이트에서 및 [VS 2010에 데이터베이스 배포](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html) Vishal Joshi 블로그.

<a id="0.2__Toc224729059"></a><a id="0.2__Toc253429296"></a><a id="0.2__Toc243304667"></a>

### <a name="one-click-publish-for-web-applications"></a>웹 응용 프로그램에 대 한 One-click 게시

Visual Studio 2010에서는 IIS 원격 관리 서비스를 사용 하 여 원격 서버에 웹 응용 프로그램을 게시할 수도 있습니다. 또는 테스트 서버 / 스테이징 서버 호스팅 계정에 대 한 게시 프로필을 만들 수 있습니다. 각 프로필은 적절 한 자격 증명을 안전 하 게 저장할 수 있습니다. 다음에 대상 중 하나에 배포할 수 웹 한 번의 클릭을 사용 하 여 한 번의 클릭 서버 도구 모음을 게시 합니다. Visual Studio 2010과 함께 MSBuild 명령줄을 사용 하 여 게시할 수 있습니다. 이렇게 하면 연속 통합 모델에 게시를 포함 하도록 팀 빌드 환경을 구성할 수 있습니다.

자세한 내용은 참조 [하는 방법: 웹 응용 프로그램 프로젝트를 사용 하 여 한 번의 클릭 게시 및 웹 배포 배포](https://msdn.microsoft.com/en-us/library/dd465337%28VS.100%29.aspx) MSDN 웹 사이트 및 [VS 2010 원클릭 게시 웹](http://vishaljoshi.blogspot.com/2009/05/web-1-click-publish-with-vs-2010.html) Vishal Joshi 블로그. Visual Studio 2010에서 웹 응용 프로그램 배포에 대 한 비디오 프레젠테이션을 보려면 참조 [VS 2010 웹 개발자 미리 보기에 대 한](http://vishaljoshi.blogspot.com/2008/12/vs-2010-for-web-developer-previews.html) Vishal Joshi 블로그.

<a id="0.2__Toc224729060"></a><a id="0.2__Toc253429297"></a><a id="0.2__Toc243304668"></a>

### <a name="resources"></a>리소스

다음 웹 사이트는 ASP.NET 4 및 Visual Studio 2010에 대 한 추가 정보를 제공 합니다.

- [ASP.NET 4](https://msdn.microsoft.com/en-us/library/ee532866%28VS.100%29.aspx) -MSDN 웹 사이트에서 ASP.NET 4에 대 한 공식 설명서입니다.
- [https://www.asp.net/](https://www.asp.net/) -ASP.NET 팀의 웹 사이트입니다.
- [https://www.asp.net/dynamicdata/](https://msdn.microsoft.com/en-us/library/cc488545.aspx) 및 [ASP.NET 동적 데이터 콘텐츠 맵](https://msdn.microsoft.com/en-us/library/cc488545%28VS.100%29.aspx) -ASP.NET 팀 사이트 및 ASP.NET Dynamic Data에 대 한 공식 설명서의 온라인 리소스.
- [https://www.asp.net/ajax/](../../ajax/index.md) -ASP.NET Ajax 개발에 대 한 기본 웹 리소스입니다.
- [https://blogs.msdn.com/webdevtools/](https://blogs.msdn.com/webdevtools/) -Visual Studio 2010의 기능에 대 한 정보를 포함 하는 경우 Visual Web Developer 팀 블로그.
- [ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack) -ASP.NET의 미리 보기 릴리스에 대 한 기본 웹 리소스입니다.

<a id="0.2__Toc224729061"></a><a id="0.2__Toc253429298"></a><a id="0.2__Toc243304669"></a>

## <a name="disclaimer"></a>고지 사항

본 문서는 예비 문서이며, 여기에 설명한 소프트웨어의 최종 상업적 출시 전에 크게 변경될 수 있습니다.

이 문서에 포함된 정보는 게시 날짜 현재 논의된 문제에 대한 Microsoft Corporation의 당시 관점을 나타냅니다. Microsoft는 변화하는 시장 상황에 부응해야 하므로, Microsoft의 일부에 대한 책임으로 해석되어서는 안되며, 게시 날짜 이후 소개된 정보의 정확성을 Microsoft가 보증할 수 없습니다.

이 백서는 정보 제공만을 목적으로 합니다. Microsoft는 이 문서에 있는 정보에 대한 명시적 또는 묵시적, 법적인 보증을 하지 않습니다.

해당 저작권법을 준수하는 것은 사용자의 책임입니다. 저작권에서의 권리와는 별도로, 이 설명서의 어떠한 부분도 Microsoft의 명시적인 서면 승인 없이는 어떠한 형식이나 수단(전기적, 기계적, 복사기에 의한 복사, 디스크 복사 또는 다른 방법) 또는 목적으로도 복제되거나, 검색 시스템에 저장 또는 도입되거나, 전송될 수 없습니다.

Microsoft가 이 설명서 본안에 관련된 특허권, 상표권, 저작권 또는 기타 지적 재산권 등을 보유할 수도 있습니다. 서면 사용권 계약에 따라 Microsoft로부터 귀하에게 명시적으로 제공된 권리 이외에, 이 문서의 제공은 귀하에게 이러한 특허권, 상표권, 저작권, 또는 기타 지적 소유권 등에 대한 어떠한 사용권도 허여하지 않습니다.

다른 설명이 없는 한, 용례에 사용된 회사, 기관, 제품, 도메인 이름, 전자 메일 주소, 로고, 사람, 장소 및 이벤트 등은 실제 데이터가 아닙니다. 어떠한 실제 회사, 기관, 제품, 도메인 이름, 전자 메일 주소, 로고, 사람, 장소 또는 이벤트와도 연관시킬 의도가 없으며 그렇게 유추해서도 안 됩니다.

© 2009 Microsoft Corporation입니다. All rights reserved.

Microsoft 및 Windows는 미국 및/또는 기타 국가에서 Microsoft Corporation의 상표이거나 등록된 상표입니다.

여기에 언급된 실제 회사와 제품의 이름은 각각 해당 소유자의 상표일 수 있습니다.
