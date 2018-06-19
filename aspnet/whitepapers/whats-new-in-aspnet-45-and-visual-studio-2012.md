---
uid: whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
title: ASP.NET 4.5 및 Visual Studio 2012의 새로운 기능 | Microsoft Docs
author: rick-anderson
description: 이 문서에서는 새로운 기능 및 ASP.NET 4.5에서 도입 된 향상 된 기능을 설명 합니다. 웹 개발을 위해 수행 하는 향상 된 기능에 대해서도 설명...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/29/2012
ms.topic: article
ms.assetid: ba1fabb4-31a3-4ebf-8327-41a6bbba6eaf
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
msc.type: content
ms.openlocfilehash: 16a2fa4b1b6617430703853543cbf29e18ba1103
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
ms.locfileid: "28886444"
---
<a name="whats-new-in-aspnet-45-and-visual-studio-2012"></a>ASP.NET 4.5 및 Visual Studio 2012의 새로운 기능
====================
> 이 문서에서는 새로운 기능 및 ASP.NET 4.5에서 도입 된 향상 된 기능을 설명 합니다. 또한 Visual Studio 2012에서 웹 개발에 대해 수행 되는 향상 된 기능을 설명 합니다. 이 문서를 2012 년 2 월 29 일에 원래 게시 됩니다.


- [ASP.NET Core 런타임 및 프레임 워크](#_Toc318097372)

    - [비동기적으로 읽고 쓰는 HTTP 요청 및 응답](#_Toc318097373)
    - [HttpRequest 처리의 향상 된 기능](#_Toc318097374)
    - [응답을 비동기적으로 플러시](#_Toc318097375)
    - [에 대 한 지원 *await* 및 *작업*-기반 비동기 모듈과 처리기](#_Toc318097376)
    - [비동기 HTTP 모듈](#_Toc318097377)
    - [비동기 HTTP 처리기](#_Toc318097378)
    - [새 ASP.NET 요청 유효성 검사 기능](#_Toc318097379)
    - [("지연") 요청 유효성 검사를 지연합니다.](#_Toc318097380)
    - [유효성이 검사 되지 않은 요청에 대 한 지원](#_Toc318097381)
    - [AntiXSS 라이브러리](#_Toc318097382)
    - [Websocket 프로토콜에 대 한 지원](#_Toc318097383)
    - [묶음 및 축소](#_Toc318097384)
    - [웹 호스팅에 대 한 성능 향상](#_Toc_perf)

        - [핵심 성능 요소](#_Toc_perf_1)
        - [새로운 성능 기능에 대 한 요구 사항](#_Toc_perf_2)
        - [일반적인 어셈블리 공유](#_Toc_perf_3)
        - [빠른 시작에 대 한 멀티 코어 JIT 컴파일을 사용 하 여](#_Toc_perf_4)
        - [가비지 수집을 최적화 하기 위해 메모리를 튜닝 합니다.](#_Toc_perf_5)
        - [웹 응용 프로그램 프리페치](#_Toc_perf_6)
- [ASP.NET Web Forms](#_Toc318097385)

    - [강력한 형식의 데이터 컨트롤](#_Toc318097386)
    - [모델 바인딩](#_Toc318097387)

        - [데이터 선택](#_Toc318097388)
        - [값 공급자](#_Toc318097389)
        - [컨트롤의 값으로 필터링](#_Toc318097390)
    - [HTML로 인코딩된 데이터 바인딩 식](#_Toc318097391)
    - [비 가시적인 유효성 검사](#_Toc318097392)
    - [HTML5 업데이트](#_Toc318097393)
- [ASP.NET MVC 4](#_Toc318097394)
- [ASP.NET 웹 페이지 2](#_Toc318097395)
- [Visual Studio 2012 릴리스 후보](#_Toc318097396)

    - [Visual Studio 2010 및 Visual Studio 2012 릴리스 후보 (프로젝트 호환성) 간 공유 되는 프로젝트](#project-compatibility)
    - [ASP.NET 4.5 웹 사이트 템플릿의 구성 변경 내용](#Configuration_Changes_In_ASPNET45_Website_Templates)
    - [ASP.NET 라우팅에 대 한 IIS 7에서에서 기본적으로 지원](#Native_Support_In_IIS7_For_ASPNET_Routine)
    - [HTML 편집기](#_Toc318097397)

        - [스마트 작업](#_Toc318097398)
        - [WAI ARIA 지원](#_Toc318097399)
        - [새 HTML5 조각](#_Toc318097400)
        - [사용자 정의 컨트롤로 추출](#_Toc318097401)
        - [특성에 중요 코드에 대 한 IntelliSense](#_Toc318097402)
        - [태그를 일치 하는 여는 태그 또는 닫는 태그의 이름을 바꾸면의 자동 이름 바꾸기](#_Toc318097403)
        - [이벤트 처리기 생성](#_Toc318097404)
        - [스마트 들여쓰기](#_Toc318097405)
        - [문 완성 자동 감소](#_Toc318097406)
    - [JavaScript 편집기](#_Toc318097407)

        - [코드 개요](#_Toc318097408)
        - [중괄호 일치](#_Toc318097409)
        - [정의로 이동](#_Toc318097410)
        - [ECMAScript5 지원](#_Toc318097411)
        - [DOM IntelliSense](#_Toc318097412)
        - [VSDOC 서명이 오버 로드](#_Toc318097413)
        - [암시적 참조](#_Toc318097414)
    - [CSS 편집기](#_Toc318097415)

        - [문 완성 자동 감소](#_Toc318097416)
        - [계층적 들여쓰기입니다.](#_Toc318097417)
        - [CSS 해킹 지원](#_Toc318097418)
        - [공급 업체 특정 스키마 (-moz-,-webkit)](#_Toc318097419)
        - [주석 및 주석 처리를 제거 지원](#_Toc318097420)
        - [색 선택](#_Toc318097421)
        - [조각](#_Toc318097422)
        - [사용자 지정 영역](#_Toc318097423)
    - [페이지 검사기](#_Toc318097424)
    - [Publishing](#_Toc318097425)

        - [게시 프로필](#_Toc318097426)
        - [ASP.NET 미리 컴파일 및 병합](#_Toc318097427)
- [IIS Express](#_Toc318097428)
- [Disclaimer](#_Toc318097429)

<a id="_Toc318097372"></a>
## <a name="aspnet-core-runtime-and-framework"></a>ASP.NET Core 런타임 및 프레임 워크

<a id="_Toc318097373"></a>
### <a name="asynchronously-reading-and-writing-http-requests-and-responses"></a>비동기적으로 읽고 쓰는 HTTP 요청 및 응답

ASP.NET 4로 사용 하 여 스트림의 HTTP 요청 엔터티를 읽을 수 있는 기능이 도입 된 *HttpRequest.GetBufferlessInputStream* 메서드. 이 메서드는 요청 엔터티에 대 한 스트리밍 액세스를 제공 합니다. 그러나이 동기적으로 실행에서 스레드를 요청 기간에 대 한 연결입니다.

ASP.NET 4.5는 HTTP 요청 엔터티를 비동기적으로 스트림을 읽을 수 있으며 비동기적으로 플러시할 수를 지원 합니다. ASP.NET 4.5 더블 버퍼 컨트롤러.aspx 페이지 처리기 및 ASP.NET MVC와 같은 다운스트림 HTTP 처리기와 쉽게 통합을 제공 하는 HTTP 요청 엔터티 수를 제공 합니다.

<a id="_Toc318097374"></a>
#### <a name="improvements-to-httprequest-handling"></a>HttpRequest 처리의 향상 된 기능

ASP.NET 4.5에 의해 반환 되는 스트림 참조 *HttpRequest.GetBufferlessInputStream* 동기 및 비동기 읽기 메서드를 지원 합니다. *스트림* 에서 반환 된 개체 *GetBufferlessInputStream* 이제 BeginRead와 EndRead 메서드를 구현 합니다. 비동기 *스트림* 메서드를 통해 ASP.NET 읽기는 비동기 루프의 각 반복 사이 현재 스레드를 해제 하는 동안 청크를 요청 엔터티를 비동기적으로 읽을 수 있습니다.

ASP.NET 4.5에 버퍼링 된 방식으로 요청 엔터티를 읽기 위한 도우미 메서드 추가: *HttpRequest.GetBufferedInputStream*합니다. 이 새 오버 로드와 비슷하게 작동 *GetBufferlessInputStream*, 동기 및 비동기 읽기를 지원 합니다. 그러나, 읽으면서, *GetBufferedInputStream* 도 다운스트림 모듈과 처리기 요청 엔터티가 액세스할 여전히 수 있도록 엔터티 바이트 ASP.NET 내부 버퍼를 복사 합니다. 예를 들어 일부 업스트림 파이프라인의 코드를 이미 읽은 사용 하 여 요청 엔터티 *GetBufferedInputStream*를 계속 사용할 수 있습니다 *HttpRequest.Form* 또는 *HttpRequest.Files*. 이렇게 하면 (예: 데이터베이스에 큰 파일 업로드를 스트리밍), 요청에서 비동기 처리를 수행 하지만 여전히 실행된.aspx 페이지 및 ASP.NET MVC controllers 나중에.

<a id="_Toc318097375"></a>
#### <a name="asynchronously-flushing-a-response"></a>응답을 비동기적으로 플러시

HTTP 클라이언트에 대 한 응답을 보내는 클라이언트 멀리 떨어져 또는 낮은 대역폭 연결의 경우 시간이 오래 걸릴 수 있습니다. 일반적으로 ASP.NET 응용 프로그램에 의해 만들어지면 응답 바이트를 버퍼링 합니다. ASP.NET 요청 처리의 거의 마지막 계산 된 버퍼를 단일 전송 작업을 수행합니다.

주기적으로 호출 해야 버퍼링 된 응답 (예: 큰 파일을 클라이언트로 스트리밍) 크면 *HttpResponse.Flush* 클라이언트에 버퍼링 된 출력을 보내기 위해 메모리 사용을 제어 합니다. 그러나 때문에 *플러시* 반복적으로 호출 하는 동기 호출 *플러시* 여전히 실행 시간이 긴 요청 중에 스레드를 소비 합니다.

ASP.NET 4.5를 사용 하 여 비동기적으로 플러시합니다 수행에 대 한 지원을 추가 *BeginFlush* 및 *EndFlush* 의 메서드는 *HttpResponse* 클래스입니다. 이러한 메서드를 사용 하 여 비동기 모듈 및 증분 방식으로 데이터를 보내는 클라이언트에 운영 체제 스레드에 연결 하지 않고도 비동기 처리기를 만들 수 있습니다. 사이 *BeginFlush* 및 *EndFlush* 호출, ASP.NET 현재 스레드를 해제 합니다. 이 장기 실행 HTTP 다운로드를 지원 하기 위해 필요한 활성 스레드의 총 수를 크게 저하 됩니다.

<a id="_Toc318097376"></a>
### <a name="support-for-await-and-task---based-asynchronous-modules-and-handlers"></a>에 대 한 지원 *await* 및 *작업* -기반 비동기 모듈과 처리기

.NET Framework 4 라고 하는 비동기 프로그래밍 개념을 도입는 *작업*합니다. 작업으로 표시 됩니다는 *작업* 유형과 관련 된 형식을 *System.Threading.Tasks* 네임 스페이스입니다. .NET Framework 4.5 작업할 수 있게 컴파일러 기능이 향상 된이 빌드 *작업* 개체 단순 합니다. .NET Framework 4.5에서 컴파일러는 두 개의 새로운 키워드를 지원: *await* 및 *비동기*합니다. *await* 키워드 구문의 줄임 표기를 나타내는 코드를 코드의 다른 부분에서 비동기적으로 대기 해야 하는 합니다. *비동기* 키워드 작업 기반 비동기 메서드로 메서드를 표시 하는 데 사용할 수 있는 힌트를 나타냅니다.

조합의 *await*, *비동기*, 및 *작업* 개체를 사용 하면 훨씬 쉽게.NET 4.5에서 비동기 코드를 작성할 수 있습니다. ASP.NET 4.5 비동기 HTTP 모듈 및 향상 된 새 컴파일러를 사용 하 여 비동기 HTTP 처리기를 작성할 수 있는 새 Api와 이러한 단순화를 지원 합니다.

<a id="_Toc318097377"></a>
#### <a name="asynchronous-http-modules"></a>비동기 HTTP 모듈

반환 하는 메서드 내에서 비동기 작업을 수행 하려는 경우는 *작업* 개체입니다. 다음 코드 예제에서는 Microsoft 홈 페이지를 다운로드 하려면 비동기 호출을 실행 하는 비동기 메서드를 정의 합니다. 사용은 *비동기* 메서드 서명에 있는 키워드 및 *await* 에 대 한 호출 *DownloadStringTaskAsync*합니다.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample1.cs)]

작성 해야 할 그-.NET Framework를 완료 하려면 다운로드를 기다리는 수 있을 뿐만 아니라 다운로드가 완료 된 후 호출 스택을 자동으로 복원 하는 동안 호출 스택 해제를 자동으로 처리 됩니다.

이제이 비동기 메서드를 사용 하 여 비동기 ASP.NET HTTP 모듈에서 가정 합니다. ASP.NET 4.5에는 도우미 메서드가 포함 되어 (*EventHandlerTaskAsyncHelper*) 및 새로운 대리자 형식 (*TaskEventHandler*)와 이전 작업 기반 비동기 메서드를 통합 하는 데 사용할 수 있는 비동기 프로그래밍 모델을 ASP.NET HTTP 파이프라인에 의해 노출 합니다. 이 예에서는 어떻게:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample2.cs)]

<a id="_Toc318097378"></a>
#### <a name="asynchronous-http-handlers"></a>비동기 HTTP 처리기

ASP.NET에서 비동기 처리기를 작성 하는 일반적인 방법을 구현 하는 것은 *IHttpAsyncHandler* 인터페이스입니다. ASP.NET 4.5 소개는 *HttpTaskAsyncHandler* 비동기 기본 형식에서 파생 될 수 있는 더욱 쉽게 비동기 처리기를 작성할 수 있게 해줍니다.

*HttpTaskAsyncHandler* 형식이 추상 이며 재정의 해야는 *ProcessRequestAsync* 메서드. 내부적으로 ASP.NET을 맡고 반환 서명 통합 (한 *작업* 개체)의 *ProcessRequestAsync* ASP.NET 파이프라인에서 사용 하는 오래 된 비동기 프로그래밍 모델을 사용 합니다.

다음 예제에서는 사용 하는 방법을 보여 줍니다. *작업* 및 *await* 의 비동기 HTTP 처리기 구현의 일부로:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample3.cs)]

<a id="_Toc318097379"></a>
### <a name="new-aspnet-request-validation-features"></a>새 ASP.NET 요청 유효성 검사 기능

기본적으로 ASP.NET 요청 유효성 검사를 수행-태그 또는 필드, 머리글, 쿠키 및 등의 스크립트에 대 한 요청을 검사 합니다. 검색 된 ASP.NET 예외를 throw 합니다. 이 잠재적인 교차 사이트 스크립팅 공격을 막는 최전방의 첫 번째 줄으로 사용 됩니다.

ASP.NET 4.5를 사용 하면 쉽게 선택적으로 유효성이 검사 되지 않은 요청 데이터를 읽을 수 있습니다. ASP.NET 4.5에는 또한 외부 라이브러리 였던 하는 인기 있는 AntiXSS 라이브러리를 통합 합니다.

개발자가 응용 프로그램에 대 한 요청 유효성 검사를 선택적으로 해제 하는 기능에 대 한 질문과 대답가입니다. 예를 들어 포럼 소프트웨어 응용 프로그램을 사용 하는 경우 사용자가 다른 모든 요청 유효성 검사는 하는지 여부를 확인 하지만 HTML 형식의 포럼 게시물 및 의견을 제출 하도록 허용 하는 것이 좋습니다.

ASP.NET 4.5 쉽게 유효성이 검사 되지 않은 입력을 선택 하 여 작업할 수 있도록 하는 두 가지 기능을 소개: ("지연") 요청 유효성 검사 및 유효성이 검사 되지 않은 요청 데이터에 대 한 액세스를 지연 합니다.

<a id="_Toc318097380"></a>
#### <a name="deferred-lazy-request-validation"></a>("지연") 요청 유효성 검사를 지연합니다.

ASP.NET 4.5에서 기본적으로 모든 요청 데이터를 요청 유효성 검사가 적용 합니다. 그러나 응용 프로그램 요청 데이터를 실제로 액세스 될 때까지 요청 유효성 검사를 연기을 구성할 수 있습니다. (이 라고도 지연 요청 유효성 검사를 특정 데이터 시나리오에 대 한 지연 로딩이 등의 용어를 기반으로 합니다.) 지연 된 유효성 검사를 설정 하 여 Web.config 파일에서 사용 하는 응용 프로그램을 구성할 수 있습니다는 *requestValidationMode* 특성에서 4.5로는 *httpRUntime* 다음 예제와 같이 요소:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample4.xml)]

요청 유효성 검사 모드 4.5로 설정 되 면 요청 유효성 검사는 특정 요청 값에 대해서만 하 고 코드 해당 값에 액세스 하는 경우에 발생 합니다. 예를 들어, 코드 Request.Form["forum의 값을 설정 하는 경우\_게시"], 폼 컬렉션의 해당 요소에 대 한 요청 유효성 검사를 호출 합니다. 다른 요소는 *양식* 컬렉션에 유효성을 검사 합니다. 이전 버전의 ASP.NET에서는 요청 유효성 검사 컬렉션에 있는 모든 요소를 액세스 하는 경우에 전체 요청 컬렉션에 대 한 트리거 되었습니다. 새 동작을 통해 다른 응용 프로그램 구성 요소를 다른 부분에 대해 요청 유효성 검사를 트리거하지 않고 요청 데이터의 다양 한 요소를 살펴보는 쉽게 있습니다.

<a id="_Toc318097381"></a>
#### <a name="support-for-unvalidated-requests"></a>유효성이 검사 되지 않은 요청에 대 한 지원

지연 된 요청 유효성 검사만 선택적으로 요청 유효성 검사를 생략의 문제를 해결 하지 않습니다. Request.Form["forum에 대 한 호출\_게시"] 트리거 해당 특정 요청 값에 대 한 유효성 검사를 요청 합니다. 그러나 다음 해당 필드에 태그를 허용 하려고 하기 때문에 유효성 검사를 트리거하지 않고이 필드에 액세스 하는 것이 좋습니다.

이 허용 하려면 ASP.NET 4.5 이제 요청 데이터에 대 한 유효성이 검사 되지 않은 액세스를 지원 합니다. ASP.NET 4.5 포함 새 *Unvalidated* 컬렉션 속성에는 *HttpRequest* 클래스입니다. 이 컬렉션의 모든 요청 데이터의 공통 값에 대 한 액세스를 같은 제공 *양식*, *QueryString*, *쿠키*, 및 *Url*합니다.

포럼 예제를 사용 하 여 유효성이 검사 되지 않은 요청 데이터를 읽을 수를 먼저 구성 해야 새 요청 유효성 검사 모드를 사용 하도록 응용 프로그램:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample5.xml)]

그런 다음 사용할 수는 *HttpRequest.Unvalidated* 유효성이 검사 되지 않은 폼 값을 읽을 속성:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample6.cs)]


> [!WARNING]
> 보안- *주의 하 여 유효성이 검사 되지 않은 요청 데이터를 사용 하 여!* ASP.NET 4.5 유효성이 검사 되지 않은 요청 속성과 쉽게 매우 구체적인 유효성이 검사 되지 않은 요청 데이터에 액세스할 수 있도록 컬렉션에 추가 합니다. 그러나 여전히 사용자 지정 유효성 검사에서는 원시 요청 데이터를 사용자에 게 위험한 텍스트 렌더링 되지 않습니다에서 수행 해야 합니다.


<a id="_Toc318097382"></a>
### <a name="antixss-library"></a>AntiXSS 라이브러리

Microsoft AntiXSS 라이브러리의 인기도 인해 이제 ASP.NET 4.5 버전 4.0 해당 라이브러리에서 core 인코딩 루틴에 통합 되어 있습니다.

인코딩 루틴에서 구현 되는 *AntiXssEncoder* 새 형식 *System.Web.Security.AntiXss* 네임 스페이스입니다. 사용할 수는 *AntiXssEncoder* 형식에서 구현 되는 인코딩 정적 메서드 중 하나를 호출 하 여 직접 유형입니다. 그러나 새 앤티 XSS 루틴을 사용 하기 위한 가장 쉬운 방법을 사용 하도록 ASP.NET 응용 프로그램을 구성 하는 것은 *AntiXssEncoder* 기본적으로 클래스입니다. 이 위해 Web.config 파일에 다음 특성을 추가 합니다.

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample7.xml)]

때는 *encoderType* 특성은 사용 하도록 설정 되는 *AntiXssEncoder* 유형, 모든 출력을 새 인코딩 루틴을 사용 하 여 ASP.NET에서 자동으로 인코딩.

다음은 외부 AntiXSS 라이브러리 부분에 ASP.NET 4.5에 통합 되었습니다.

- *HtmlEncode*, *HtmlFormUrlEncode*, 및 *HtmlAttributeEncode*
- *XmlAttributeEncode* 및 *XmlEncode*
- *UrlEncode* 및 *UrlPathEncode* (새로 만들기)
- *CssEncode*

<a id="_Toc318097383"></a>
### <a name="support-for-websockets-protocol"></a>Websocket 프로토콜에 대 한 지원

Websocket 프로토콜은 HTTP를 통해 클라이언트와 서버 간의 안전 하 고 실시간 양방향 통신을 설정 하는 방법을 정의 하는 표준 기반 네트워크 프로토콜입니다. Microsoft는 IETF와 W3C 표준 기관 프로토콜을 정의할 수 있도록와 협력 합니다. Websocket 프로토콜은 클라이언트와 모바일 운영 체제 모두에서 Websocket 프로토콜을 지 원하는 많은 리소스를 투자 하는 Microsoft와 모든 클라이언트 (뿐 아니라 브라우저)에서 지원 됩니다.

Websocket 프로토콜을 사용 하면 훨씬 쉽게는 클라이언트와 서버 간에 실행 시간이 긴 데이터 전송을 만들 수 있습니다. 예를 들어, 채팅 응용 프로그램을 작성 되므로 훨씬 더 쉽게 클라이언트와 서버 간의 true 실행 시간이 긴 연결을 설정할 수 있습니다. 정기 폴링을 또는 HTTP 긴 폴링 소켓의 동작을 시뮬레이션할과 같은 대안을 필요가 없습니다.

ASP.NET 4.5 및 IIS 8 사용 등이 부분적으로 Websocket 지원, ASP.NET 개발자가 비동기적으로 읽고 문자열 및 이진 데이터를 모두 Websocket 개체에 쓰기 위한 관리 되는 Api를 사용 하도록 합니다. ASP.NET 4.5는 새 *System.Web.WebSockets* Websocket 프로토콜을 사용 하기 위한 형식이 포함 된 네임 스페이스입니다.

DOM을 만들어 Websocket 연결을 설정 하는 브라우저 클라이언트가 *WebSocket* 다음 예제와 같이 ASP.NET 응용 프로그램에서 URL을 가리키는 개체입니다.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample8.cs)]

모든 종류의 모듈 또는 처리기를 사용 하 여 ASP.NET에서 Websocket 끝점을 만들 수 있습니다. 앞의 예에서.ashx 파일 처리기를 만들 수는 신속 하 게 되므로.ashx 파일 사용 되었습니다.

Websocket 프로토콜에 따라 ASP.NET 응용 프로그램을 요청 해야으로 업그레이드할 수 HTTP GET 요청 으로부터 Websocket 요청을 지정 하 여 클라이언트의 Websocket 요청을 허용 합니다. 예를 들면 다음과 같습니다.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample9.cs)]

*AcceptWebSocketRequest* ASP.NET 현재 HTTP 요청을 해제 하 고 다음 제어 하는 함수 대리자를 전달 하기 때문에 메서드는 함수 대리자를 허용 합니다. 개념적으로이 방법은 사용 하는 방법에 비슷한 *System.Threading.Thread*, 여기서는 백그라운드에서 수행 되는 작업이 스레드 시작 대리자를 정의 합니다.

ASP.NET 및 클라이언트 Websocket 핸드셰이크 성공적으로 완료, 사용자 대리자를 호출 하는 ASP.NET 및 Websocket 응용 프로그램 실행을 시작 합니다. 다음 코드 예제에서는 기본 Websocket 지원에는 ASP.NET에서 사용 하는 간단한 에코 응용을 보여 줍니다.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample10.cs)]

지원에 대 한.NET 4.5에는 *await* 키워드 및 작업 기반 비동기 작업은 적합 한 Websocket 응용 프로그램을 작성 합니다. 코드 예제에서는 ASP.NET 내부 Websocket 요청을 완전히 비동기적으로 실행 되는지 보여 줍니다. 응용 프로그램을 호출 하 여 클라이언트에서 전송 될 메시지를 비동기적으로 기다립니다. *소켓을 기다립니다. ReceiveAsync*합니다. 호출 하 여 클라이언트를 비동기 메시지를 보낼 수는 마찬가지로, *소켓을 기다립니다. SendAsync*합니다.

브라우저에서 응용 프로그램을 통해 Websocket 메시지를 받는 *onmessage* 함수입니다. 호출 브라우저에서 메시지를 보내려고는 *보낼* 의 메서드는 *WebSocket* 이 예제에 나와 있는 것 처럼 DOM 유형:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample11.cs)]

나중에이 추상 자리를 비울 하위 수준 코딩 즉 중 일부에 필요한이 기능을이 릴리스 WebSockets에 대 한 응용 프로그램에 대 한 업데이트 출시 했습니다.

<a id="_Toc318097384"></a>
### <a name="bundling-and-minification"></a>묶음 및 축소

번들로 단일 파일 처럼 처리 될 수 있는 번들에서 개별 JavaScript 및 CSS 파일 결합할 수 있습니다. 축소 공백 및 필요 하지 않은 다른 문자를 제거 하 여 JavaScript 및 CSS 파일을 압축 합니다. 이러한 기능은 웹 페이지, Web Forms 및 ASP.NET MVC와 작동 합니다.

번들 번들 클래스 또는 해당 자식 클래스, ScriptBundle 및 StyleBundle 중 하나를 사용 하 여 생성 됩니다. 번들의 인스턴스를 구성 했으면 번들 전역 BundleCollection 인스턴스를 추가 하기만 하면에 들어오는 요청에 사용할이 활성화 됩니다. 기본 서식 파일에 번들 구성은 BundleConfig 파일에서 수행 됩니다. 이 기본 구성의 모든 핵심 스크립트 및 템플릿을 사용 하는 css 파일에 대 한 번들을 만듭니다.

번들은 몇 가지 가능한 도우미 메서드 중 하나를 사용 하 여 뷰 내에서 참조 됩니다. 디버그와 릴리스 모드에서에서 번들에 대 한 다른 태그 렌더링을 지원 하기 위해 ScriptBundle 및 StyleBundle 클래스에는 도우미 메서드를 렌더링 합니다. 디버그 모드일 때는 렌더링에서 번들의 각 리소스에 대 한 태그를 생성 합니다. 릴리스 모드에서 렌더링 전체 번들에 대 한 단일 태그 요소를 생성 합니다. 설정/해제 디버그 및 릴리스 간의 모드 아래와 같이 web.config에서 컴파일 요소의 디버그 특성을 수정 하 여 구현 수 있습니다.

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample12.xml)]

또한 활성화 또는 비활성화 최적화 BundleTable.EnableOptimizations 속성을 통해 직접 설정할 수 있습니다.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample13.cs)]

파일을 번들로 제공 되는 경우 먼저 알파벳 순서로 (에 표시 되는 방식을 **솔루션 탐색기**). 다음 구성 된 라이브러리를 알 수 있도록 하 고 해당 사용자 지정 확장 프로그램 (예: jQuery, MooTools, Dojo) 가장 먼저 로드 합니다. 예를 들어 위와 같이 Scripts 폴더의 번들에 대 한 최종 순서가 됩니다.

1. jquery-1.6.2.js
2. jquery-ui.js
3. jquery.tools.js
4. a.js

CSS 파일도 사전순으로 정렬 되며 다음 reset.css 및 normalize.css 다른 파일 앞에 야 있도록 다시 구성 됩니다. 위에 표시 된 Styles 폴더의 번들의 최종 정렬이이 설정 됩니다.

1. reset.css
2. content.css
3. forms.css
4. globals.css
5. menu.css
6. styles.css

<a id="_Toc_perf"></a>
### <a name="performance-improvements-for-web-hosting"></a>웹 호스팅에 대 한 성능 향상

.NET Framework 4.5 및 Windows 8 웹 서버 워크 로드에 대 한 상당한 성능 향상을 달성 하는 데 도움이 되는 기능을 소개 합니다. 여기에 감소 (최대 35%) 모두 시작 시간 및 웹 호스팅 ASP.NET을 사용 하는 사이트의 메모리 공간입니다.

<a id="_Toc_perf_1"></a>
#### <a name="key-performance-factors"></a>핵심 성능 요소

이상적으로 모든 웹 사이트는 활성화 해야 합니다. 않았으며 다음 요청에 대 한 빠른 응답을 메모리에 때마다 제공 합니다. 사이트 응답성에 영향을 줄 수 있는 요인은 다음과 같습니다.

- 사이트에서 응용 프로그램 풀을 재활용 후에 다시 시작 소요 되는 시간입니다. 메모리에 더 이상 사이트 어셈블리 때 사이트에 대 한 웹 서버 프로세스를 시작 하는 데 걸리는 시간입니다. (플랫폼 어셈블리 되므로 메모리에 여전히 다른 사이트에서 사용 하는입니다.) 이 경우 "콜드 사이트, 웜 프레임 워크 시작" 라고 또는 방금 "콜드 사이트를 시작 합니다."
- 메모리의 양을 사이트를 차지합니다. 이 용어는 "사이트 간 메모리 소비" 또는 "작업 집합을 해제 합니다."

새 성능 향상을 이끌어 두이 요소가 모두에 집중합니다.

<a id="_Toc_perf_2"></a>
#### <a name="requirements-for-new-performance-features"></a>새로운 성능 기능에 대 한 요구 사항

새로운 기능에 대 한 요구 사항은 이러한 범주로 구분할 수 있습니다.

- .NET Framework 4에서 실행 되는 개선 되었습니다.
- .NET Framework 4.5를 필요 하지만 모든 버전의 Windows에서 실행할 수 있는 향상 된 기능입니다.
- Windows 8에서 실행 되는.NET Framework 4.5에만 사용할 수 있는 향상 된 기능입니다.

성능 향상 사용 하도록 설정할 수 있는의 각 수준에 따라 카운터가 증가 합니다.

개선 된.NET Framework 4.5 기능에도 다른 시나리오에 적용 되는 광범위 한 성능 기능을 사용 합니다.

<a id="_Toc_perf_3"></a>
#### <a name="sharing-common-assemblies"></a>일반적인 어셈블리 공유

**요구 사항**:.NET Framework 4 및 Visual Studio 11 개발자 미리 보기 SDK

서버에서 다른 사이트는 종종 동일한 도우미 어셈블리 (예: 시작 키트 또는 샘플 응용 프로그램에서 어셈블리)를 사용합니다. 각 사이트의 Bin 디렉터리에서 이러한 어셈블리의 자체 복사본을 있습니다. 어셈블리에 대 한 개체 코드는 동일 하지만 각 어셈블리는 콜드 사이트 시작 하는 동안 개별적으로 읽을 수 있도록 물리적으로 별도 어셈블리를 하 고 메모리에 개별적으로 유지 합니다.

새로운 인턴 지정 기능 이러한 비효율성을 해결 하 고 모두 RAM 요구 사항 및 부하를 줄일 수 시간입니다. 인터닝 수 있습니다 Windows 파일 시스템에 각 어셈블리의 단일 복사본을 유지 하 고 단일 복사본에 대 한 기호화 된 링크와 사이트 Bin 폴더에 개별 어셈블리가 교체 됩니다. 개별 사이트에서 서로 다른 버전의 어셈블리를 필요로 한다면 기호화 된 링크는은 어셈블리의 새 버전으로 대체 되 고 해당 사이트에만 영향을 받습니다.

Aspnet 이라는 새 장치가 필요한 기호화 된 링크를 사용 하 여 어셈블리를 공유\_intern.exe 만들고 인턴 지정된 어셈블리가의 저장소를 관리할 수 있습니다. Visual Studio 11 개발자 미리 보기 SDK의 일부분으로 제공 됩니다. 그러나 (만.NET Framework 4 설치 된 최신 기능을 설치한 것으로 가정 된 시스템에서 작동 합니다 [업데이트](https://support.microsoft.com/kb/2468871).)

Aspnet 모든 적격 어셈블리 인턴 되었습니다 하기 실행\_intern.exe 주기적으로 (예: 예약된 된 태스크로 일주일에 한 번). 일반적인 용도 다음과 같습니다.

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample14.cmd)]

모든 옵션을 보려면 하려면 인수 없이 도구를 실행 합니다.

<a id="_Toc_perf_4"></a>
#### <a name="using-multi-core-jit-compilation-for-faster-startup"></a>빠른 시작에 대 한 멀티 코어 JIT 컴파일을 사용 하 여

**요구 사항**:.NET Framework 4.5

콜드 사이트 시작을 위한 어셈블리 필요가 디스크에서 읽은 뿐만 아니라 JIT 컴파일된 사이트 이어야 합니다. 복잡 한 사이트가 지연을 추가할 수 있습니다. .NET Framework 4.5의 새로운 범용 기술으로 사용할 수 있는 프로세서 코어 JIT 컴파일 분배 하 여 이러한 지연을 줄입니다. 만큼이 작업을 수행 하 고 최대한 일찍 도중 수집 된 정보를 사용 하 여 이전 시작 사이트의. 이 기능에 의해 구현 된 [System.Runtime.ProfileOptimization.StartProfile](https://msdn.microsoft.com/library/system.runtime.profileoptimization.startprofile(VS.110).aspx) 메서드.

JIT 컴파일 여러 코어를 사용 하 여 되므로이 기능을 활용 하기 위해 아무 작업도 수행 하지 않고도 asp.net에서는 기본적으로 사용 됩니다. 이 기능을 사용 하지 않도록 설정 하려면 Web.config 파일에서 다음 설정을 확인 합니다.

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample15.xml)]

<a id="_Toc_perf_5"></a>
#### <a name="tuning-garbage-collection-to-optimize-for-memory"></a>가비지 수집을 최적화 하기 위해 메모리를 튜닝 합니다.

**요구 사항**:.NET Framework 4.5

사이트를 실행 하 고, 가비지 수집기 (GC) 힙에서 사용 하는 메모리 소비에 중요 한 요소가 수 있습니다. 모든 가비지 수집기와 같은.NET Framework GC CPU 시간 (빈도 significance는 컬렉션의) 및 메모리 사용 (새, 확보, 또는 자유 수 없는 개체에 사용 되는 추가 공간이) 간 균형을 만듭니다. 이전 릴리스에 대 한 적절 한 균형을 달성 하기 위해 GC를 구성 하는 방법에 지침 제공 된 (예를 들어 참조 [ASP.NET 2.0/3.5 공유 호스팅 구성](https://www.iis.net/learn/web-hosting/web-server-for-shared-hosting/aspnet-20-35-shared-hosting-configuration)).

.NET Framework 4.5 작업 정의 된 구성 설정은 여러 독립 실행형 설정 대신 사용할 수 없으면 수 있게 해 주는 모든에서는 이전에 권장 되는 GC 설정으로 새 튜닝의 각 사이트에 대 한 추가 성능을 제공 하는 작업 집합입니다.

튜닝 GC 메모리를 사용 하려면 다음 설정을 Windows\Microsoft.NET\Framework\v4.0.30319\aspnet.config 파일에 추가 합니다.

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample16.xml)]

(변경 내용에 대 한 이전 지침 aspnet.config 알고 인 경우이 설정은 이전 설정을 대체 참고-예를 들어 gcServer, gcConcurrent 등을 설정 하지 않아도 됩니다. 않아도 이전 설정을 제거 합니다.)

<a id="_Toc_perf_6"></a>
#### <a name="prefetching-for-web-applications"></a>웹 응용 프로그램 프리페치

**요구 사항**: Windows 8에서 실행 되는.NET Framework 4.5

Windows가 기술을 통해을 포함 하는 데 몇 번의 릴리스에서 대 한는 [prefetcher](http://en.wikipedia.org/wiki/Prefetcher) 하는 응용 프로그램 시작의 디스크 읽기 비용을 줄입니다. 콜드 시작 클라이언트 응용 프로그램에 주로 문제가 이기 때문에이 기술은 하지 하는 서버에 필요한 구성 요소만 포함 하는 Windows Server에 포함 되었습니다. 프리페치는 최신 버전의 Windows Server에서 개별 웹 사이트의 시작을 최적화할 수 있다는 것에 출시 되었습니다.

Windows Server는 prefetcher 기본적으로 사용 하지 않습니다. 을 사용 하려면 구성 고밀도 웹 호스팅을 위한 prefetcher 명령줄에서 명령 집합을 실행 합니다.

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample17.cmd)]

그런 다음는 prefetcher ASP.NET 응용 프로그램을 통합 하려면 다음 Web.config 파일에 추가:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample18.xml)]

<a id="_Toc318097385"></a>
## <a name="aspnet-web-forms"></a>ASP.NET Web Forms

<a id="_Toc318097386"></a>
### <a name="strongly-typed-data-controls"></a>강력한 형식의 데이터 컨트롤

ASP.NET 4.5 Web Forms 데이터로 작업 하기 위한 몇 가지 향상 된 기능을 포함 합니다. 첫 번째 개선은 강력한 형식의 데이터를 제어 합니다. 이전 버전의 ASP.NET Web Forms 컨트롤에 표시할 있습니다 사용 하 여 데이터 바인딩된 값 *Eval* 및 데이터 바인딩 식:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample19.aspx)]

양방향 데이터 바인딩을 사용 하 여 있습니다 *바인딩할*:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample20.aspx)]

런타임 시 이러한 호출은 리플렉션을 사용 하 여 지정된 된 멤버의 값을 읽고 태그에 결과 표시 합니다. 이 접근 방식을 쉽게 임의의 unshaped 데이터에 대 한 데이터 바인딩이 있습니다.

그러나 다음과 같은 데이터 바인딩 식 멤버 이름, (예: 정의로 이동), 탐색 또는 컴파일 타임 이러한 이름에 대 한 검사에 대 한 IntelliSense와 같은 기능을 지원 하지 않습니다.

이 문제를 해결 하기 위해 ASP.NET 4.5 컨트롤에 바인딩되는 데이터의 데이터 형식을 선언 하는 기능을 추가 합니다. 이렇게 하면 새를 사용 하 여 *ItemType* 속성입니다. 데이터 바인딩 식의 범위에 두 개의 새 형식화 된 변수는 사용할 수 있는이 속성을 설정 하는 경우: *항목* 및 *BindItem*합니다. 변수는 강력한 형식 때문에 Visual Studio 개발 환경의 모든 혜택을 얻을 합니다.


사용 하 여 양방향 데이터 바인딩 식에 대 한는 *BindItem* 변수:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample21.aspx)]


데이터 바인딩을 지 원하는 대부분 ASP.NET Web Forms 프레임 워크 컨트롤을 지원 하도록 업데이트 되었습니다는 *ItemType* 속성입니다.

<a id="_Toc318097387"></a>
### <a name="model-binding"></a>모델 바인딩

모델 바인딩 코드 중심의 데이터 액세스를 사용 하려면 ASP.NET Web Forms 컨트롤의 데이터 바인딩을 확장 합니다. 개념을 통합 하는 *ObjectDataSource* 컨트롤 및 ASP.NET mvc에서 모델 바인딩의 합니다.

<a id="_Toc318097388"></a>
#### <a name="selecting-data"></a>데이터 선택

컨트롤의 데이터를 선택 하려면 모델 바인딩을 사용 하도록 데이터 제어를 구성 하려면 설정 *SelectMethod* 속성 페이지의 코드에 있는 메서드의 이름입니다. 데이터 컨트롤 페이지 수명 주기의 적절 한 시간에 메서드를 호출 하 고 자동으로 반환된 된 데이터를 바인딩합니다. 명시적으로 호출할 필요가 없습니다는 *DataBind* 메서드.

다음 예제에서는 *GridView* 제어 라는 메서드를 사용 하도록 구성 된 *GetCategories*:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample22.aspx)]

만들는 *GetCategories* 페이지의 코드에서 메서드. 단순한 select 작업에 대 한 메서드 매개 변수 없이 필요 하 고 반환 해야는 *IEnumerable* 또는 *IQueryable* 개체입니다. 하는 경우 새 *ItemType* 속성이 설정 되어 (있도록 하는 강력한 데이터 바인딩 식을 형식에 설명 된 대로 [데이터 컨트롤 강력한 형식의](#_Toc318097386) 이전 버전), 이러한 인터페이스의 제네릭 버전 반환 되어야- *IEnumerable&lt;T&gt;*  또는 *IQueryable&lt;T&gt;* 와 *T* 매개 변수 형식과 일치 하는 *ItemType* 속성 (예를 들어 *IQueryable&lt;범주&gt;*).

다음 예제에 대 한 코드는 *GetCategories* 메서드. 이 예제에서는 Northwind 샘플 데이터베이스에서 Entity Framework Code First 모델을 사용 합니다. 코드에서는 쿼리를 통해 범주별 관련된 제품의 세부 정보를 반환 하는지 확인는 *Include* 메서드. (이렇게 하면는 *TemplateField* 태그 요소에에서 필요 없이 각 범주에서 제품의 수를 표시 한 [n + 1 선택](http://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem).)

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample23.cs)]

페이지 실행 하는 경우, *GridView* 컨트롤을 호출은 *GetCategories* 메서드 자동으로 구성 된 필드를 사용 하 여 반환 된 데이터를 렌더링 합니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.png)

Select 메서드 반환 하기 때문에 *IQueryable* 개체는 *GridView* 컨트롤 실행 되기 전에 쿼리를 추가로 조작할 수 있습니다. 예를 들어는 *GridView* 컨트롤 정렬 및 반환 된 페이징에 대 한 쿼리 식을 추가할 수 있습니다 *IQueryable* 실행 하기 전에 개체를 해당 작업은 내부에서 수행 LINQ 공급자입니다. 이 경우 Entity Framework를 사용 하는 데이터베이스에 해당 작업이 수행 됩니다 확인 됩니다.

다음 예제와 *GridView* 컨트롤 정렬 및 페이징을 사용 하도록 수정 합니다.

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample24.aspx)]

이제 페이지를 실행할 때 컨트롤 데이터의 현재 페이지에만 표시 되 고 선택한 열에 의해 정렬 된 있는지 확인 수 있습니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.png)

반환 된 데이터를 필터링 하려면 매개 변수를 select 메서드에 추가 해야 합니다. 이러한 매개 변수를 실행 하는 모델 바인딩에서 채워지며 쿼리 데이터를 반환 하기 전에 변경에 사용할 수 있습니다.

예를 들어 쿼리 문자열에 키워드를 입력 하 여 사용자가 제품 필터를 사용 한다고 가정 합니다. 메서드 매개 변수를 추가 하 고 매개 변수 값을 사용 하도록 코드를 업데이트할 수 있습니다.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample25.cs)]

이 코드를 포함 한 *여기서* 식에 값이 제공 하는 경우 *키워드* 쿼리 결과 반환 합니다.

<a id="_Toc318097389"></a>
#### <a name="value-providers"></a>값 공급자

앞의 예제에서 위치에 대 한 특정 없습니다에 대 한 값은 *키워드* 매개 변수에서 생성 되었습니다. 이 정보를 나타내려면 매개 변수 특성을 사용할 수 있습니다. 이 예에서는 사용할 수 있습니다는 *QueryStringAttribute* 에 있는 클래스는 *System.Web.ModelBinding* 네임 스페이스:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample26.cs)]

이렇게 하면 모델을 쿼리 문자열에서 값을 연결할 하려고을 바인딩하는 *키워드* 실행 시 매개 변수입니다. (여기 형식 변환을 수행 하지만 경우 하지 않습니다.) 값을 제공할 수 없습니다 형식이 nullable이 아닌 경우 예외가 throw 됩니다.

이러한 방법에 대 한 값의 소스는 값 공급자 라고 하 고를 사용 하는 값 공급자를 나타내는 매개 변수 특성 값 공급자 특성으로 간주 됩니다. Web Forms에는 Web Forms 응용 프로그램의 쿼리 문자열, 쿠키, 폼 값, 컨트롤, 상태 보기, 세션 상태 프로필 속성 등의 모든 사용자 입력의 일반적인 원본에 대 한 값 공급자 및 해당 포함 됩니다. 사용자 지정 값 공급자를 작성할 수 있습니다.

기본적으로 매개 변수 이름 값 공급자 컬렉션에 값을 찾을 키로 사용 됩니다. 예제에서는 코드 키워드를 명명 된 쿼리 문자열 값에 대 한 표시 됩니다 (예를 들어 ~ / default.aspx?keyword=chef). 매개 변수 특성에 대 한 인수로 전달 하 여 사용자 지정 키를 지정할 수 있습니다. 예를 들어 q 명명 된 쿼리 문자열 변수의 값을 사용 하려면이 수행할 수 있습니다.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample27.cs)]

이러한 방법은 페이지의 코드에 사용자가 쿼리 문자열을 사용 하는 키워드를 전달 하 여 결과 필터링 수 있습니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.png)

직접 코드를 작성 하려면 해야 하는 많은 작업을 수행 하는 모델 바인딩: 값을 읽기, null 값을 확인 하는, 적절 한 형식으로 변환 하는 동안은 변환이 성공 했는지 여부를 확인 및의 값을 사용 하 여 마지막으로 쿼리입니다. 훨씬 더 적을 코드와 응용 프로그램 전체에서 기능을 다시 사용할 수 있는 결과 바인딩을 모델링 합니다.

<a id="_Toc318097390"></a>
#### <a name="filtering-by-values-from-a-control"></a>컨트롤의 값으로 필터링

드롭다운 목록에서 필터 값을 선택할 수 있도록 예제 확장 하려면 한다고 가정 합니다. 다음 드롭 다운 목록 태그를 추가 하 고 해당 데이터를 사용 하 여 다른 메서드를 가져오기 위해 구성 된 *SelectMethod* 속성:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample28.aspx)]

일반적으로 추가할 수도 있습니다는 *emptydatatemplate이* 요소를는 *GridView* 컨트롤에서는 일치 하는 제품이 발견 되 면 메시지를 표시 되도록 합니다.

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample29.aspx)]

페이지 코드에서 새 선택 드롭다운 목록에 대 한 메서드를 추가 합니다.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample30.cs)]

마지막으로 업데이트는 *GetProducts* 드롭 다운 목록에서 선택된 된 범주 ID가 포함 된 새 매개 변수를 사용 하는 방법 선택:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample31.cs)]

이제 페이지를 실행 하는 경우 사용자가 드롭다운 목록에서 범주를 선택할 수 및 *GridView* 컨트롤은 필터링 된 데이터를 표시 하도록 자동으로 다시 바인딩. 모델 바인딩 선택 방법에 대 한 매개 변수 값을 추적 하 고 모든 매개 변수 값을 다시 게시 한 후 변경 되었는지 여부를 검색 하기 때문에 이것이 가능 합니다. 이 경우 모델 바인딩 관련된 된 데이터 컨트롤에 데이터를 다시 바인딩할 되도록 합니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.png)

<a id="_Toc318097391"></a>
### <a name="html-encoded-data-binding-expressions"></a>HTML로 인코딩된 데이터 바인딩 식

있습니다 수 이제 HTML 인코딩할 데이터 바인딩 식의 결과입니다. 콜론 (:)의 끝에 추가 &lt;데이터 바인딩 식을 표시 하는 % # 접두사:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample32.aspx)]

<a id="_Toc318097392"></a>
### <a name="unobtrusive-validation"></a>비 가시적인 유효성 검사

이제 클라이언트 쪽 유효성 검사 논리에 대 한 비 가시적인 JavaScript를 사용 하도록 기본 제공 유효성 검사 컨트롤을 구성할 수 있습니다. 이 크게 JavaScript 페이지 태그에 인라인으로 렌더링할지 줄일 수 및 전체 페이지 크기를 줄입니다. 비간섭 JavaScript 유효성 검사 컨트롤에 대 한 이러한 방법 중 하나로 구성할 수 있습니다.

- 다음 설정을 추가 하 여 전역적으로  *&lt;appSettings&gt;*  Web.config 파일의 요소: 

    [!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample33.xml)]
- 정적 설정 하 여 전역적으로 *System.Web.UI.ValidationSettings.UnobtrusiveValidationMode* 속성을 *UnobtrusiveValidationMode.WebForms* (일반적으로 *응용 프로그램 \_시작* Global.asax 파일에는 메서드).
- 새 설정 하 여 페이지에 대해 개별적으로 *UnobtrusiveValidationMode* 의 속성은 *페이지* 클래스를 *UnobtrusiveValidationMode.WebForms*합니다.

<a id="_Toc318097393"></a>
### <a name="html5-updates"></a>HTML5 업데이트

몇 가지 향상 된 기능에 적용 된 Web Forms 서버 컨트롤 HTML5의 새로운 기능을 활용 하려면:

- *TextMode* 의 속성은 *TextBox* 제어와 같은 새로운 HTML5 입력된 형식을 지원 하도록 업데이트 되었습니다 *전자 메일*, *datetime*, 및 에 있습니다.
- *파일 업로드* 지원이 HTML5 기능을 지 원하는 브라우저에서 여러 파일 업로드를 제어 합니다.
- 유효성 검사기는 이제 지원의 유효성을 검사할 HTML5 입력된 요소를 제어합니다.
- 이제 URL을 나타내는 특성이 있는 새 HTML5 요소 지원 runat = "server"입니다. 결과적으로, 사용할 수 있습니다 ASP.NET 규칙 URL 경로에 ~를 나타내는 응용 프로그램 루트 연산자 (예를 들어 &lt;비디오 runat = "server" src="~/myVideo.wmv" /&gt;).
- *UpdatePanel* 컨트롤 게시 HTML5 입력된 필드를 지원 하도록 수정 되었습니다.

<a id="_Toc318097394"></a>
## <a name="aspnet-mvc-4"></a>ASP.NET MVC 4

ASP.NET MVC 4 베타는 이제 Visual Studio 11 베타에 포함 되어 있습니다. ASP.NET MVC는 매우 테스트 가능 하 고 유지 관리 가능한 웹 응용 프로그램 모델-뷰-컨트롤러 (MVC) 패턴을 활용 하 여 개발 합니다. ASP.NET MVC 4 쉽게 모바일 웹 응용 프로그램을 개발 하 고 모든 장치에 연결할 수 있는 HTTP 서비스를 작성 하는 데 도움이 되는 ASP.NET Web API를 포함 합니다. 자세한 내용은 참조는 [ASP.NET MVC 4 릴리스 정보](mvc4-release-notes.md)합니다.

<a id="_Toc318097395"></a>
## <a name="aspnet-web-pages-2"></a>ASP.NET 웹 페이지 2

새로운 기능은 다음과 같습니다.

- 새로운 또는 업데이트 된 사이트 서식 파일입니다.
- 서버 쪽 및 클라이언트 쪽 유효성 검사를 사용 하 여 추가 된 *유효성 검사* 도우미입니다.
- 자산 관리자를 사용 하 여 스크립트를 등록 하는 기능.
- Facebook 및 OAuth 및 OpenID를 사용 하 여 다른 사이트에서의 로그인을 사용 하도록 설정 합니다.
- 사용 하 여 추가 매핑됩니다는 *매핑합니다* 도우미입니다.
- 웹 페이지 응용 프로그램에서-병렬 실행 중입니다.
- 모바일 장치에 대 한 페이지를 렌더링 합니다.

이러한 기능 및 전체 페이지 코드 예제에 대 한 자세한 내용은 참조 [웹 페이지 2 베타의 The Top 기능](https://go.microsoft.com/fwlink/?LinkID=227824)합니다.

<a id="_Toc318097396"></a>
## <a name="visual-web-developer-11-beta"></a>Visual Web Developer 11 베타

이 섹션에서는 Visual Web Developer 11 베타 및 Visual Studio 2012 릴리스 후보에서 웹 개발에 대 한 향상 된 기능에 대 한 정보를 제공 합니다.

<a id="project-compatibility"></a>
### <a name="project-sharing-between-visual-studio-2010-and-visual-studio-2012-release-candidate-project-compatibility"></a>Visual Studio 2010 및 Visual Studio 2012 릴리스 후보 (프로젝트 호환성) 간 공유 되는 프로젝트

Visual Studio 2012 릴리스 후보 될 때까지 새 버전의 Visual Studio에서 기존 프로젝트를 열기 변환 마법사를 실행 합니다. 솔루션 및 프로젝트의 콘텐츠 (자산)를 업그레이드 하는 이전 버전과 호환 되지 않은 새로운 형식에 강제로 됩니다. 따라서 변환 후 있습니다 열 수 없습니다 프로젝트는 이전 버전의 Visual Studio에서.

많은 고객 되었다는 적합 한 접근 방식의 없음을 합니다. Visual Studio 11 베타에서 이제 Visual Studio 2010 s p 1을 사용 하 여 솔루션 및 프로젝트를 공유를 지원 합니다. 이 Visual Studio 2012 릴리스 후보에서 2010 프로젝트를 열면은 여전히 Visual Studio 2010 s p 1에서 프로젝트를 열 수를 의미 합니다.

> [!NOTE]
> 몇 가지 형식의 프로젝트는 Visual Studio 2010 SP1 및 Visual Studio 2012 릴리스 후보 간에 공유할 수 없습니다. 여기 일부 (예: ASP.NET MVC 2 프로젝트) 이전 프로젝트 또는 프로젝트 (예: 설치 프로젝트의 경우) 특수 목적을 위해 포함 됩니다.

Visual Studio 11 베타에서 처음으로 Visual Studio 2010 SP1 웹 프로젝트를 열 때 다음과 같은 속성이 프로젝트 파일에 추가 됩니다.

- FileUpgradeFlags
- UpgradeBackupLocation
- OldToolsVersion
- VisualStudioVersion
- VSToolsPath

FileUpgradeFlags, UpgradeBackupLocation, 및 OldToolsVersion 프로젝트 파일 업그레이드 프로세스에서 사용 됩니다. Visual Studio 2010에서 프로젝트 작업에 영향을 주지 갖습니다.

VisualStudioVersion에 현재 프로젝트에 대 한 Visual Studio의 버전을 나타내는 MSBuild 4.5에서 사용 하는 새 속성입니다. MSBuild 4.0 (Visual Studio 2010 s p 1을 사용 하는 MSBuild의 버전)이이 속성에 존재 하지 않은 때문에 삽입 합니다. 기본값은 프로젝트 파일에 있습니다.

VSToolsPath 속성 MSBuildExtensionsPath32 설정에 의해 표시 된 경로에서 가져올 올바른.targets 파일 확인에 사용 됩니다.

Import 요소와 관련 된 몇 가지 변경 사항이 있습니다. 이러한 변경이 Visual Studio의 두 버전 간의 호환성을 지원 하기 위해 필요 합니다.

> [!NOTE]
> 프로젝트는 두 개의 서로 다른 컴퓨터에 Visual Studio 2010 SP1 및 Visual Studio 11 베타 간에 공유 되 고 하 고 프로젝트에 응용 프로그램에서 로컬 데이터베이스를 포함 하는 경우\_데이터 폴더를 확인 해야 데이터베이스에 사용 되는 SQL Server 버전이 두 컴퓨터에 설치 합니다.

<a id="Configuration_Changes_In_ASPNET45_Website_Templates"></a>
### <a name="configuration-changes-in-aspnet-45-website-templates"></a>ASP.NET 4.5 웹 사이트 템플릿의 구성 변경 내용

다음과 같이 변경 기본값에 적용 된 *Web.config* Visual Studio 2012 릴리스 후보에서 웹 사이트 템플릿을 사용 하 여 만든 사이트에 대 한 파일:

- 에 `<httpRuntime>` 요소는 `encoderType` 특성은 이제 ASP.NET에 추가 된 AntiXSS 형식을 사용 하도록 기본값으로 설정 됩니다. 자세한 내용은 참조 [AntiXSS 라이브러리](#_Toc318097382)합니다.
- 또한는 `<httpRuntime>` 요소는 `requestValidationMode` 특성을 "4.5"로 설정 합니다. 즉, 기본적으로 지연된 ("지연") 유효성 검사를 사용 하도록 요청 유효성 검사 구성 됩니다. 자세한 내용은 참조 [새로운 ASP.NET 요청 유효성 검사 기능](#_Toc318097379)합니다.
- `<modules>` 의 요소는 `<system.webServer>` 섹션에 포함 되어 있지 않습니다는 `runAllManagedModulesForAllRequests` 특성입니다. (기본값은 false입니다.) 즉, s p 1로 업데이트 되지 않은 IIS 7의 버전을 사용 하는 경우 새 사이트에서의 라우팅 문제를 할 수 있습니다. 자세한 내용은 참조 [ASP.NET 라우팅에 대 한 IIS 7에서 기본적으로 지원](#Native_Support_In_IIS7_For_ASPNET_Routine)합니다.

이러한 변경 내용은 기존 응용 프로그램 영향을 주지 않습니다. 그러나 기존 웹 사이트 및 새 템플릿을 사용 하 여 ASP.NET 4.5에 대해 만드는 새 웹 사이트 간 동작의 차이 나타낼 수 있습니다.

<a id="Native_Support_In_IIS7_For_ASPNET_Routine"></a>
### <a name="native-support-in-iis-7-for-aspnet-routing"></a>ASP.NET 라우팅에 대 한 IIS 7에서에서 기본적으로 지원

이것은 ASP.NET에 대 한 변경 이므로 아니며 SP1 업데이트 적용에 있던 IIS 7의 버전을 작업 하는 경우 영향을 주는 새 웹 사이트 프로젝트에 대 한 템플릿 변경 합니다.

Asp.net에서는 다음 구성 설정의 라우팅을 지원 하기 위해 응용 프로그램에 추가할 수 있습니다.

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample34.xml?highlight=3)]

때 **runAllManagedModulesForAllRequests** true, 같은 URL은 `http://mysite/myapp/home` 있다 하더라도 ASP.NET에서로 이동 없습니다 *.aspx*, *.mvc*, 또는 유사한 확장에는 URL입니다.

IIS 7에 수행한 업데이트는 **runAllManagedModulesForAllRequests** 불필요 한 설정 및 ASP.NET 라우팅은 고유 하 게 지원 합니다. (업데이트에 대 한 내용은 Microsoft 지원 문서를 참조 하십시오. [업데이트가 사용 하도록 설정 된 Url의 요청을 처리 하는 IIS 7.0 또는 IIS 7.5 처리기 특정 마침표로 끝나지 않는 제공 되 고](https://support.microsoft.com/kb/980368).)

웹 사이트는 IIS 7에서 실행 되 고 설정 해야 할 경우 IIS가 업데이트 된 하지 **runAllManagedModulesForAllRequests** true로 합니다. 사실, true로 설정 좋지 않습니다, 불필요 한 처리 오버 헤드가 요청에 추가 하기 때문에. 이 설정은 true를 포함 하 여 요청을 모두 *.htm*, *.jpg*, 다른 정적 파일에도 ASP.NET 요청 파이프라인을 통해 이동 합니다.

Visual Studio 2012 RC에 제공 되는 템플릿을 사용 하 여 새 ASP.NET 4.5 웹 사이트를 만들 경우 웹 사이트에 대 한 구성을 포함 되지 않습니다는 **runAllManagedModulesForAllRequests** 설정 합니다. 즉, 기본적으로 설정이 임을 false.

실행 하면 웹 사이트에서 Windows 7 s p 1을 설치 하지 않고, IIS 7 필요한 업데이트를 포함 되지 않습니다. 결과적으로 라우팅이 작동 하지 않습니다 및 오류가 표시 됩니다. 문제가 있습니다. 여기서 라우팅이 작동 하지 않습니다, 다음 중 하나를 수행할 수 있습니다.

- Windows 7 s p 1에서는 IIS 7에 업데이트를 추가 하는 업데이트 합니다.
- 앞에 나열 된 Microsoft 지원 문서에서 설명 하는 업데이트를 설치 합니다.
- 설정 **runAllManagedModulesForAllRequests** 해당 웹 사이트의 Web.config 파일에서 true로 합니다. 요청에 약간의 오버 헤드를 추가 합니다이 note 합니다.

<a id="_Toc318097397"></a>
### <a name="html-editor"></a>HTML 편집기

<a id="_Toc318097398"></a>
#### <a name="smart-tasks"></a>스마트 작업

디자인 뷰에서 종종에 서버 컨트롤의 복잡 한 속성 대화 상자와 마법사 쉽게 설정할 수 있도록 연결 합니다. 예를 들어 데이터 소스를 추가 하려면 특별 한 대화 상자를 사용할 수는 *반복기* 제어 하거나 열을 추가 하는 *GridView* 제어 합니다.

그러나이 유형의 복잡 한 속성에 대 한 UI 도움말 소스 뷰에서 제공 되지 않았습니다. 따라서 Visual Studio 11에서는 소스 뷰에 대 한 스마트 작업을 소개 합니다. 스마트 작업은 C# 및 Visual Basic 편집기에서 일반적으로 사용 되는 기능에 대 한 바로 가기 키를 컨텍스트 인식 됩니다.

ASP.NET Web Forms 컨트롤에 대 한 스마트 작업이 전자 메일 서버 태그에 작은 문자 모양 요소 안에 삽입 지점이 있을 경우:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.png)

스마트 작업 문자 모양을 클릭 하거나 CTRL + 때 확장 됩니다. (점), 코드 편집기에서와 마찬가지로 합니다. 디자인 뷰의 스마트 작업과 유사 하 게 되는 바로 가기를 표시 합니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image7.png)

예를 들어 위의 그림에서 스마트 작업 GridView 작업 옵션을 보여 줍니다. 열 편집을 선택 하는 경우 다음과 같은 대화 상자가 표시 됩니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image8.png)

대화 상자 집합의 동일한 속성을 채우는 디자인 보기에서 설정할 수 있습니다. 확인을 클릭 하면 컨트롤에 대 한 태그 새 설정으로 업데이트 됩니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image9.png)

<a id="_Toc318097399"></a>
#### <a name="wai-aria-support"></a>WAI ARIA 지원

액세스할 수 있는 웹 사이트 작성 점점 더 중요 해지고 있습니다. [WAI ARIA 내게 필요한 옵션 표준](http://www.w3.org/WAI/intro/aria) 개발자 해야 액세스할 수 있는 웹 사이트를 작성 하는 방법을 정의 합니다. 이제이 표준 Visual Studio에서 완전히 지원 됩니다.

예를 들어는 *역할* 특성에는 이제 전체 IntelliSense에:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image10.png)

WAI ARIA 표준 접두사로 사용 하는 특성은 또한 제공 *aria-* HTML5 문서 의미 체계를 추가할 수 있는 합니다. Visual Studio에 이러한 항목을 완전히 지원 *aria-* 특성:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image11.png) ![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image12.png)

<a id="_Toc318097400"></a>
#### <a name="new-html5-snippets"></a>새 HTML5 조각

자주 사용 되는 HTML5 태그를 작성을 쉽고 빠르게을 하려면 Visual Studio에 조각의 있습니다. 예는 비디오 조각을.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image13.png)

코드 조각으로 호출 하려면 tab 키를 누른 채 IntelliSense에서 요소를 선택 하는 경우에 두 번:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image14.png)

사용자 지정할 수 있는 코드 조각을 생성 됩니다.

<a id="_Toc318097401"></a>
#### <a name="extract-to-user-control"></a>사용자 정의 컨트롤로 추출

큰 웹 페이지에서 개별 조각을 사용자 정의 컨트롤로 이동 하는 것이 좋습니다 수 있습니다. 이러한 형태의 리팩터링 페이지의 가독성을 높일 수 있습니다 및 페이지 구조를 단순화할 수 있습니다.

간단 하 게 하려면이 소스 뷰에서 Web Forms 페이지를 편집할 때 있습니다 수 이제 페이지에 텍스트를 선택, 마우스 오른쪽 단추로 클릭 한 다음 사용자 정의 컨트롤로 추출.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.jpg)

<a id="_Toc318097402"></a>
#### <a name="intellisense-for-code-nuggets-in-attributes"></a>특성에 중요 코드에 대 한 IntelliSense

Visual Studio는 항상 모든 페이지 또는 제어에 서버 쪽 코드 조각에 대 한 IntelliSense를 제공 합니다. 이제 Visual Studio에서 HTML 특성에도 코드 조각에 대 한 IntelliSense를 포함 합니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image15.png)

이렇게 하면 데이터 바인딩 식을 만드는 쉽게:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image16.png)

<a id="_Toc318097403"></a>
#### <a name="automatic-renaming-of-matching-tag-when-you-rename-an-opening-or-closing-tag"></a>태그를 일치 하는 여는 태그 또는 닫는 태그의 이름을 바꾸면의 자동 이름 바꾸기

HTML 요소의 이름을 바꾸는 경우 (변경 하는 예를 들어는 *div* 되도록 태그는 *헤더* 태그), 해당를 열거나 닫는 태그를 실시간으로 변경 합니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image17.png)

이 잘못 변경 하거나 닫는 태그를 변경 하 시겠습니까 오류를 방지할 수 있습니다.

<a id="_Toc318097404"></a>
#### <a name="event-handler-generation"></a>이벤트 처리기 생성

이제 visual Studio 이벤트 처리기를 작성 하 고 수동으로 바인딩할 수 있도록 소스 뷰에서 기능이 포함 됩니다. 소스 뷰에서 이벤트 이름을 편집 하는 경우 IntelliSense 표시 &lt;새 이벤트 만들&gt;, 올바른 서명이 있는 이벤트 처리기에서에서 만들 페이지의 코드를:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.jpg)

기본적으로 이벤트 처리기의 이벤트 처리 메서드 이름에 대 한 컨트롤의 ID를 사용 합니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.jpg)

결과 이벤트 처리기는이 예제의 C#에서 다음과 같이 표시 됩니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image18.png)

<a id="_Toc318097405"></a>
#### <a name="smart-indent"></a>스마트 들여쓰기

빈 HTML 요소 내부에 있는 동안 Enter 키를 누를 때 편집기 적절 한 위치에 삽입 포인터를 됩니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image19.png)

Enter 키를 눌러이 위치에 닫는 태그가 아래로 이동이 고 여는 태그와 일치 하도록 들여씁니다. 삽입 지점이 들여쓰기 됩니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image20.png)

<a id="_Toc318097406"></a>
#### <a name="auto-reduce-statement-completion"></a>문 완성 자동 감소

Visual Studio 지금 필터만 관련 옵션 표시 되도록 입력 내용에 따라 IntelliSense 목록:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image21.png)

IntelliSense 필터 또한 IntelliSense 목록에는 개별 단어의 제목 대/소문자에 기반 합니다. 예를 들어 "dl"를 입력 하면 dl 및 asp DataList 모두 표시 됩니다.:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image22.png)

이 기능을 사용 하면 더 빠르게 알려진된 요소에 대 한 문 완성을 얻으려고 합니다.

<a id="_Toc318097407"></a>
### <a name="javascript-editor"></a>JavaScript 편집기

Visual Studio 2012 릴리스 후보의 JavaScript 편집기는 완전히 새로운 기능이 며 Visual Studio에서 JavaScript를 사용 하는 환경을 크게 높여 줍니다.

<a id="_Toc318097408"></a>
#### <a name="code-outlining"></a>코드 개요

이제 개요 영역 현재 포커스와 관련이 없는 일부 파일을 축소할 수 있도록 하는 모든 함수에 대해 자동으로 생성 됩니다.

<a id="_Toc318097409"></a>
#### <a name="brace-matching"></a>중괄호 일치

중괄호와 닫는 중괄호에 삽입 포인터를 놓으면 나와 일치 하는 편집기에서 강조 표시 합니다.

<a id="_Toc318097410"></a>
#### <a name="go-to-definition"></a>정의로 이동

로 이동 명령 정의 사용 하면 함수 또는 변수에 대 한 소스로 이동할 수 있습니다.

<a id="_Toc318097411"></a>
#### <a name="ecmascript5-support"></a>ECMAScript5 지원

편집기 ECMAScript5, JavaScript 언어에 설명 하는 표준의 최신 버전의에서 새로운 구문 및 Api를 지원 합니다.

<a id="_Toc318097412"></a>
#### <a name="dom-intellisense"></a>DOM IntelliSense

DOM Api에 대 한 IntelliSense 기능이 개선 되어 비롯 한 많은 새 HTML5 Api를 지 원하는 *querySelector*, DOM 저장, 교차 문서 메시징 및 *캔버스*합니다. 이제 DOM IntelliSense는 네이티브 형식 라이브러리 정의 아니라 단일 단순한 JavaScript 파일에 의해 결정 됩니다. 따라서 쉽게 확장 하거나 바꿀 수 있습니다.

<a id="_Toc318097413"></a>
#### <a name="vsdoc-signature-overloads"></a>VSDOC 서명이 오버 로드

자세한 IntelliSense 설명이 이제 선언할 수 JavaScript 함수의 별도 오버 로드에 대 한 새 사용 하 여  *&lt;서명&gt;*  요소를이 예제에 나와 있는 것 처럼:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample35.cs)]

<a id="_Toc318097414"></a>
#### <a name="implicit-references"></a>암시적 참조

이제 암시적으로 포함 될 파일의 목록에 지정 된 JavaScript 파일 또는 블록 참조 수 있음을 의미가 해당 내용에 대 한 IntelliSense를 얻을 수 중앙 목록에 JavaScript 파일을 추가할 수 있습니다. 예를 들어, jQuery 파일의 파일을 중앙 목록에 추가할 수 있습니다 및 얻게 됩니다 IntelliSense jQuery 함수에 대 한 파일의 모든 JavaScript 블록에서 명시적으로 참조 한 여부 (/ / /를 사용 하 여 &lt;참조 /&gt;) 여부.

<a id="_Toc318097415"></a>
### <a name="css-editor"></a>CSS 편집기

<a id="_Toc318097416"></a>
#### <a name="auto-reduce-statement-completion"></a>문 완성 자동 감소

CSS 속성을 기반으로 하는 CSS 지금 필터 및 선택한 스키마에서 지 원하는 값에 대 한 IntelliSense 목록입니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image23.png)

IntelliSense는 또한 제목 사례 검색을 지원합니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image24.png)

<a id="_Toc318097417"></a>
#### <a name="hierarchical-indentation"></a>계층적 들여쓰기

CSS 편집기를 사용 하 여 들여쓰기 계층적 규칙을 표시 한 연계 규칙은 논리적으로 구성 하는 방식을 간략하게 살펴보겠습니다. 다음 예제에서는 #list 선택 기가 목록의 연계 자식 이며 따라서 들여쓰기 됩니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image25.png)

다음 예제에서는 보다 복잡 한 상속을 보여 줍니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image26.png)

규칙의 들여쓰기는 해당 부모 규칙에 의해 결정 됩니다. 계층적 들여쓰기는 기본적으로 사용 하도록 설정 하지만 (도구, 메뉴 모음에서 옵션) 옵션 대화 상자를 해제할 수 있습니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image27.png)

<a id="_Toc318097418"></a>
#### <a name="css-hacks-support"></a>CSS 해킹 지원

수백 대의 실제 CSS 파일 분석 CSS 핵 (hack)은 매우 일반적인 및 가장 널리 사용 되는 것과 Visual Studio에서 지원 되는 이제 보여 줍니다. 이 지원에는 IntelliSense 및 유효성 검사 핫스폿에 포함 됩니다 (\*) 및 밑줄 (\_) 속성 핵 (hack):

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image28.png)

일반적인 선택기 해킹 적용 될 때에 계층적 들여쓰기 유지 되도록도 지원 됩니다. Internet Explorer 7을 대상으로 사용 되는 일반적인 선택기 해킹 된 선택기 앞에 추가 하는 것  *\*: 첫 번째 자식 + html*합니다. 해당 규칙을 사용 하 여 계층적 들여쓰기를 유지 됩니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image29.png)

<a id="_Toc318097419"></a>
#### <a name="vendor-specific-schemas--moz---webkit"></a>공급 업체 특정 스키마 (-moz--webkit)

CSS3 서로 다른 시간에 다른 브라우저에서 구현 된 많은 속성을 소개 합니다. 이 이전에 공급 업체 특정 구문을 사용 하 여 개발자가 특정 브라우저에 대 한 코드를을 강제 합니다. 이러한 브라우저와 관련 속성은 이제 IntelliSense에 포함 됩니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image30.png)

<a id="_Toc318097420"></a>
#### <a name="commenting-and-uncommenting-support"></a>주석 및 주석 처리를 제거 지원

이제 주석 처리 하 고 (Ctrl + K, 메모로 C 및 Ctrl + K, 주석 처리를 제거 하 여) 코드 편집기에서 사용 하는 동일한 바로 가기 키를 사용 하 여 CSS 규칙을 주석 처리 제거 수입니다.

<a id="_Toc318097421"></a>
#### <a name="color-picker"></a>색 선택

이전 버전의 Visual Studio에서는 IntelliSense 색상 관련 특성에 대 한 명명 된 색 값의 드롭다운 목록으로 이루어져 있습니다. 해당 목록에 모든 기능을 갖춘 색 선택 하 여 대체 되었습니다.

색 값을 입력 하면 색 선택 자동으로 표시 되 고 뒤에 기본 색 색상표에 따라 이전에 사용한 색 목록이 표시 됩니다. 마우스나 키보드를 사용 하 여 색을 선택할 수 있습니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image31.png)

목록 전체 색상 선택기 구조로 확장할 수 있습니다. 고 선택기 불투명도 슬라이더를 움직이면 RGBA를 색을 자동으로 변환 하 여 알파 채널을 제어할 수 있습니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image32.png)

<a id="_Toc318097422"></a>
#### <a name="snippets"></a>코드 조각

CSS 편집기에서 코드 조각을 더 쉽고 빠르게 교차 브라우저 스타일을 만들 수 있도록 합니다. 이제 브라우저별 설정 해야 하는 많은 CSS3 속성 조각으로 롤백 되었습니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image33.png)

CSS 조각에서 기호를 입력 하 여 (예: CSS3 미디어 쿼리) 고급 시나리오를 지원 합니다 (@), IntelliSense 목록 표시 합니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image34.png)

선택 하는 경우 @media 값 및 Tab 키를 눌러, CSS 편집기에 다음 코드 조각 삽입:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.jpg)

코드 조각에서와 마찬가지로 사용자 고유의 CSS 조각을 만들 수 있습니다.

<a id="_Toc318097423"></a>
#### <a name="custom-regions"></a>사용자 지정 영역

이미에서 사용할 수 있는 코드 편집기에서 코드 영역을 명명 된 CSS 편집을 위해 사용할 수 있습니다. 이렇게 하면 관련된 스타일 블록을 쉽게 그룹화 수 있습니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image35.png)

영역이 축소 된 영역의 이름을 표시 합니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image36.png)

<a id="_Toc318097424"></a>
### <a name="page-inspector"></a>페이지 검사기

페이지 검사기는 Visual Studio IDE에서 웹 페이지 (HTML, Web Forms, ASP.NET MVC 또는 웹 페이지)를 렌더링 하 고 소스 코드와 출력 결과 살펴볼 수 있습니다 하는 도구입니다. 페이지 검사기는 ASP.NET 페이지에 대 한 서버 쪽 코드는 브라우저에 렌더링 하는 HTML 태그에서 발생을 결정할 수 있습니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image37.png)

페이지 검사기에 대 한 자세한 내용은 다음 자습서를 참조 하십시오.

- 페이지 검사기를 사용 하 여 [ASP.NET MVC](../mvc/overview/views/using-page-inspector-in-aspnet-mvc.md)
- 페이지 검사기를 사용 하 여 [ASP.NET Web Forms](../web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project.md)

<a id="_Toc318097425"></a>
### <a name="publishing"></a>게시

<a id="_Toc318097426"></a>
#### <a name="publish-profiles"></a>게시 프로필

Visual Studio 2010에서 웹 응용 프로그램 프로젝트에 대 한 정보를 게시 하는 버전 제어에 저장 되지 않습니다 되며 다른 사용자와 공유 하는 데 설계 되지 않았습니다. Visual Studio 2012 릴리스 후보에서 게시 프로필의 형식이 변경 되었습니다. 팀 아티팩트를 향상 되었습니다 및 MSBuild에 따라 빌드에서 활용 하 여 이제 쉽습니다. 빌드 구성 정보는 게시 대화 상자에서 되므로 게시 하기 전에 빌드 구성을 쉽게 전환할 수 있습니다.

게시 프로필 PublishProfiles 폴더에 저장 됩니다. 폴더의 위치에 따라 달라 집니다 사용 중인 프로그래밍 언어에:

- C#: Properties\PublishProfiles
- Visual Basic: My Project\PublishProfiles

각 프로필은 MSBuild 파일. 게시 중 프로젝트의 MSBuild 파일에이 파일을 가져옵니다. Visual Studio 2010에서 게시 또는 패키지 프로세스에 변경 하려는 경우 해야 라는 파일에 사용자 지정 배치 **ProjectName**. wpp.targets 합니다. 이것은 현재 지원 하지만 자체 게시 프로필에 이제 사용자 지정 항목을 넣을 수 있습니다. 이런 방식으로 해당 프로필에 대 한 사용자 지정이 사용 됩니다.

이제 활용 하 여 MSBuild에서 프로필을 게시할 수도 할 수 있습니다. 이렇게 하려면 프로젝트를 빌드할 때 다음 명령을 사용 합니다.

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample36.cmd)]

Project.csproj 값은 프로젝트의 경로 이며 ProfileName 게시 프로필의 이름입니다. 에 대 한 프로필 이름을 전달 하는 대신에 또는 *PublishProfile* 속성에 전달할 수 있습니다 전체 경로에 게시 프로필.

<a id="_Toc318097427"></a>
#### <a name="aspnet-precompilation-and-merge"></a>ASP.NET 미리 컴파일 및 병합

웹 응용 프로그램 프로젝트에 대 한 Visual Studio 2012 릴리스 후보 사이트의 콘텐츠를 게시 하는 경우 또는 패키지 프로젝트를 병합 하 고 미리 컴파일할 수 있는 웹 패키지 및 게시 속성 페이지에 대 한 옵션을 추가 합니다. 이러한 옵션을 보려면 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 속성을 선택한 다음 패키지/게시 웹 속성 페이지를 선택 합니다. 다음 그림은 Precompile 옵션을 게시 하기 전에이 응용 프로그램을 보여 줍니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.jpg)

이 옵션을 선택 하면 Visual Studio 미리를 게시할 때마다 응용 프로그램 또는 웹 응용 프로그램 패키지를 컴파일합니다. 사이트 미리 컴파일된 또는 어셈블리를 병합 하는 방법을 제어 하려면 이러한 옵션을 구성 하려면 고급 단추를 클릭 합니다.

<a id="_Toc318097428"></a>
### <a name="iis-express"></a>IIS Express

Visual Studio에서 테스트 웹 프로젝트에 대 한 기본 웹 서버 IIS Express 되었습니다. Visual Studio 개발 서버를 개발 하는 동안 로컬 웹 서버에 대 한 옵션 하지만 IIS Express는 이제 권장 되는 서버. IIS Express에서 Visual Studio 11 베타 사용 경험을 사용 하 여 Visual Studio 2010 s p 1에서과 매우 비슷합니다.

<a id="_Toc318097429"></a>
## <a name="disclaimer"></a>고지 사항

본 문서는 예비 문서이며, 여기에 설명한 소프트웨어의 최종 상업적 출시 전에 크게 변경될 수 있습니다.

이 문서에 포함된 정보는 게시 날짜 현재 논의된 문제에 대한 Microsoft Corporation의 당시 관점을 나타냅니다. Microsoft는 변화하는 시장 상황에 부응해야 하므로, Microsoft의 일부에 대한 책임으로 해석되어서는 안되며, 게시 날짜 이후 소개된 정보의 정확성을 Microsoft가 보증할 수 없습니다.

이 백서는 정보 제공만을 목적으로 합니다. Microsoft는 이 문서에 있는 정보에 대한 명시적 또는 묵시적, 법적인 보증을 하지 않습니다.

해당 저작권법을 준수하는 것은 사용자의 책임입니다. 저작권에서의 권리와는 별도로, 이 설명서의 어떠한 부분도 Microsoft의 명시적인 서면 승인 없이는 어떠한 형식이나 수단(전기적, 기계적, 복사기에 의한 복사, 디스크 복사 또는 다른 방법) 또는 목적으로도 복제되거나, 검색 시스템에 저장 또는 도입되거나, 전송될 수 없습니다.

Microsoft가 이 설명서 본안에 관련된 특허권, 상표권, 저작권 또는 기타 지적 재산권 등을 보유할 수도 있습니다. 서면 사용권 계약에 따라 Microsoft로부터 귀하에게 명시적으로 제공된 권리 이외에, 이 문서의 제공은 귀하에게 이러한 특허권, 상표권, 저작권, 또는 기타 지적 소유권 등에 대한 어떠한 사용권도 허여하지 않습니다.

다른 설명이 없는 한 예제 회사, 조직, 제품, 도메인 이름, 전자 메일 주소, 로고, 사람, 장소 및 이벤트 용례은 실제 데이터가 아닙니다과 연결 된 실제 회사, 조직, 제품, 도메인 이름, 전자 메일 주소, 로고, 사람, 장소 또는 이벤트 해서도 그렇게 유추 해서도 안 됩니다.

© 2012 Microsoft Corporation. All rights reserved.

Microsoft 및 Windows는 미국 및/또는 기타 국가에서 Microsoft Corporation의 상표이거나 등록된 상표입니다.

여기에 언급된 실제 회사와 제품의 이름은 각각 해당 소유자의 상표일 수 있습니다.
