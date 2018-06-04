---
uid: mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4
title: ASP.NET MVC 4의에서 비동기 메서드를 사용 하 여 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서는 무료 했습니다 웹용 Visual Studio Express 2012를 사용 하 여 비동기 ASP.NET MVC 웹 응용 프로그램을 구축 하는 기초 알려 드리겠습니다 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/06/2012
ms.topic: article
ms.assetid: a56572ba-81c3-47af-826d-941e9c4775ec
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 5b3b9b82fa64155c1dfd2a49649def10d7dae87e
ms.sourcegitcommit: 43bd79667bbdc8a07bd39fb4cd6f7ad3e70212fb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34729183"
---
<a name="using-asynchronous-methods-in-aspnet-mvc-4"></a>ASP.NET MVC 4에서 비동기 메서드 사용
====================
으로 [Rick Anderson](https://github.com/Rick-Anderson)

> 이 자습서는 사용 하 여 비동기 ASP.NET MVC 웹 응용 프로그램을 구축 하는 기초 업무량이 [Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/11), Microsoft Visual Studio의 무료 버전입니다. 사용할 수도 있습니다 [Visual Studio 2012](https://www.microsoft.com/visualstudio/11)합니다.
> 
> 전체 샘플은 github에서이 자습서에 제공 된  [https://github.com/RickAndMSFT/Async-ASP.NET/](https://github.com/RickAndMSFT/Async-ASP.NET/)


ASP.NET MVC 4 [컨트롤러](https://msdn.microsoft.com/library/system.web.mvc.controller(VS.108).aspx) 조합에서 클래스 [.NET 4.5](https://msdn.microsoft.com/library/w0x726c2(VS.110).aspx) 형식의 개체를 반환 하는 비동기 작업 메서드를 작성할 수 있게 [작업&lt;ActionResult&gt; ](https://msdn.microsoft.com/library/dd321424(VS.110).aspx). .NET Framework 4 라고 하는 비동기 프로그래밍 개념을 도입는 [작업](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) ASP.NET MVC 4를 지원 하 고 [작업](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)합니다. 작업으로 표시 됩니다는 **작업** 유형과 관련 된 형식을 [System.Threading.Tasks](https://msdn.microsoft.com/library/system.threading.tasks.aspx) 네임 스페이스입니다. 이 비동기 지원을 사용을 기반으로 하는.NET Framework 4.5는 [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) 및 [비동기](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) 작업할 수 있게 하는 키워드 [작업](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) 이전 보다 훨씬 덜 복잡 한 개체 비동기 접근 방식입니다. [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) 키워드 구문의 줄임 표기를 나타내는 코드를 코드의 다른 부분에서 비동기적으로 대기 해야 하는 합니다. [비동기](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) 키워드 작업 기반 비동기 메서드로 메서드를 표시 하는 데 사용할 수 있는 힌트를 나타냅니다. 조합의 **await**, **비동기**, 및 **작업** 개체를 사용 하면 훨씬 쉽게.NET 4.5에서 비동기 코드를 작성할 수 있습니다. 비동기 메서드에 대해 새로운 모델 라고는 *작업 기반 비동기 패턴* (**탭**). 이 자습서에서는 사용 하 여 비동기 프로그래밍을 잘 알고 있다고 가정 [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) 및 [비동기](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) 키워드 및 [작업](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) 네임 스페이스입니다.

사용 하 여 자세한 내용은 [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) 및 [비동기](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) 키워드 및 [작업](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) 네임 스페이스에 다음을 참조 합니다.

- [백서: 비동기.NET에](https://go.microsoft.com/fwlink/?LinkId=204844)
- [Async/Await FAQ](https://blogs.msdn.com/b/pfxteam/archive/2012/04/12/10293335.aspx)
- [Visual Studio 비동기 프로그래밍](https://msdn.microsoft.com/vstudio/gg316360)

## <a id="HowRequestsProcessedByTP"></a>  스레드 풀에서 요청을 처리 하는 방법

웹 서버에서.NET Framework에는 ASP.NET 요청을 처리 하는 데 사용 되는 스레드 풀을 유지 관리 합니다. 요청이 도착 하면 해당 요청을 처리 하는 풀의 스레드가 디스패치 됩니다. 요청이 동기적으로 처리 하는 경우 요청을 처리 하는 스레드 이며 사용 중인 요청 하는 동안 처리 되는 동안 스레드 다른 요청을 처리할 수 없습니다.   
  
이 아닐 수 있습니다는 문제가 있으므로 스레드 풀은 사용 중인 많은 스레드를 수용할 수 만들 수 있습니다. 하지만 스레드 풀의 스레드 수가 제한 됩니다 (기본.NET 4.5에 대 한 최대값은 5000). 큰 응용 프로그램 동시성이 높은 된 장기 실행 요청에서는 사용 가능한 모든 스레드가 사용 중인 수도 있습니다. 이 조건은 스레드 부족 문제 라고 합니다. 이 조건에 도달 하면 웹 서버 요청을 대기 합니다. 요청 큐가 꽉 차면 웹 서버는 HTTP 503 상태 (서버 사용량이 많음)을 사용 하 여 요청을 거부 합니다. CLR 스레드 풀에 새 스레드 삽입에 제한이 있습니다. 동시성 돌발적 이면 (즉, 웹 사이트 갑자기 얻을 수 많은 수의 요청) 및 모든 사용 가능한 요청 스레드가 사용 중이거나 백 엔드 호출이 높은 대기 시간으로, 제한 된 스레드 삽입 속도 매우 불완전 하 게 응답 하는 응용 프로그램을 만들 수 있습니다. 또한 각 새 스레드는 스레드 풀에 추가 오버 헤드 (예: 스택 메모리 1MB)에 있습니다. 여기서 스레드 풀에 도달한.NET 4.5 기본값 5의 최대 대기 시간이 긴 서비스를 호출 하는 동기 메서드를 사용 하는 웹 응용 프로그램 000 스레드를 사용할 5GB 정도 수는 응용 프로그램 보다 더 많은 메모리를 사용 하 여 요청 서비스 동일 비동기 메서드와 50 개의 스레드입니다. 비동기 작업을 수행할 때 항상 사용할 스레드입니다. 예를 들어 비동기 웹 서비스 요청을 수행 하면 ASP.NET를 사용 하지 않는 사이의 모든 스레드는 **비동기** 메서드 호출 및 **await**합니다. 대기 시간이 긴 요청을 스레드 풀을 사용 하 여 큰 메모리 사용 공간 및 서버 하드웨어의 사용률 저하가 발생할 수 있습니다.

## <a name="processing-asynchronous-requests"></a>비동기 요청 처리

많은 수의 시작 시 동시 요청을 보거나 돌발적 부하가 (여기서 동시성이 갑자기 증가)는 웹 응용 프로그램에서 이러한 웹 서비스 호출을 비동기 만드는 응용 프로그램의 응답성을 늘어납니다. 비동기 요청 동기 요청으로 처리 하는 동일한 기간을 사용 합니다. 예를 들어 웹 서비스는 호출을 수행 하는 경우에 2 초를 완료 하려면 요청에서 수행 하는 2 초 동기적 또는 비동기적으로 수행 하는 것이 있는지 여부 필요 합니다. 그러나 비동기 호출 스레드가 첫 번째 요청을 완료를 기다리는 동안 다른 요청에 응답 하지 않도록 차단 되지 않습니다. 따라서 비동기 요청 장기 실행 작업을 호출 하는 많은 동시 요청이 없는 경우 요청 큐 및 스레드 풀 커지지를 않도록 합니다.

## <a id="ChoosingSyncVasync"></a>  동기 또는 비동기 작업 메서드를 선택합니다.

이 섹션에는 동기 또는 비동기 작업 메서드를 사용 하는 경우에 대 한 지침이 나와 있습니다. 이러한 내용은 지침일 뿐입니다. 비동기 메서드가 성능에 도움이 될 수 있는지 여부를 결정을 개별적으로 각 응용 프로그램을 검사 합니다.

일반적으로 다음 조건에 대 한 동기 메서드를 사용 합니다.

- 작업에는 단순 하거나 단기 실행 합니다.
- 단순성이 효율성 보다 더 중요 합니다.
- 작업은 광범위 한 디스크 또는 네트워크 오버 헤드를 포함 하는 작업 아닌 주로 CPU 작업입니다. 비동기 작업 메서드를 사용 하 여 CPU 바인딩 작업에서 이점은 없고 및 오버 헤드만 증가 합니다.

  일반적으로 다음 조건에 대 한 비동기 메서드를 사용 합니다.

- 비동기 메서드를 통해 사용할 수 있는 서비스를 호출 하 고.NET 4.5 이상을 사용 하는 합니다.
- 작업에는 네트워크 또는 I/o-바인딩된 CPU 바인딩된 대신 합니다.
- 병렬 처리는 코드의 단순성 보다 더 중요 합니다.
- 사용자가 장기 실행 요청은 취소할 수 있는 메커니즘을 제공 하려고 합니다.
- 때 스레드 전환의 이점은 컨텍스트 전환 비용을 보다 큽니다. 일반적으로 지정 해야 메서드에 비동기 동기 메서드로 ASP.NET 요청 스레드의 아무 작업도 수행 하는 동안 대기 하는 경우. 호출을 비동기 실행 하 여 ASP.NET 요청 스레드의 되지 동안에 웹 서비스 요청을 완료를 기다리는 동안 작업이 없습니다.
- 테스트 차단 사이트 성능에 병목 현상이 되 게와 IIS가 차단 되는 이러한 호출에 대 한 비동기 메서드를 사용 하 여 더 많은 요청을 처리할 수 있음을 보여 줍니다.

  다운로드 가능한 샘플에는 비동기 작업 메서드를 효율적으로 사용 하는 방법을 보여 줍니다. 제공 된 샘플은.NET 4.5를 사용 하 여 ASP.NET MVC 4의 비동기 프로그래밍의 간단한 데모를 제공 하도록 설계 되었습니다. 이 샘플은 ASP.NET MVC에서 비동기 프로그래밍에 대 한 참조 아키텍처 없습니다. 샘플 프로그램 호출 [ASP.NET Web API](../../../web-api/index.md) 메서드를 호출 하는 [Task.Delay](https://msdn.microsoft.com/library/hh139096(VS.110).aspx) 장기 실행 웹 서비스 호출을 시뮬레이션할 수 있습니다. 대부분의 프로덕션 응용 프로그램에는 비동기 작업 메서드 사용으로 뚜렷한 이점을 표시 되지 않습니다.   
  
응용 프로그램은 거의 모든 작업 메서드에 비동기적 필요 합니다. 대개 몇 가지 동기 작업 메서드를 비동기 메서드로 변환 필요한 작업량는 것이 효율성 증대를 제공 합니다.

## <a id="SampleApp"></a>  샘플 응용 프로그램

샘플 응용 프로그램을 다운로드할 수 있습니다 [ https://github.com/RickAndMSFT/Async-ASP.NET/ ](https://github.com/RickAndMSFT/Async-ASP.NET) 에 [GitHub](https://github.com/) 사이트입니다. 저장소는 다음의 세 프로젝트로 구성 됩니다.

- *Mvc4Async*:이 자습서에 사용 되는 코드를 포함 하는 ASP.NET MVC 4 프로젝트. Web API 호출에서 **WebAPIpgw** 서비스입니다.
- *WebAPIpgw*: 구현 하는 ASP.NET MVC 4 Web API 프로젝트는 `Products, Gizmos and Widgets` 컨트롤러입니다. 에 대 한 데이터를 제공는 *WebAppAsync* 프로젝트 및 *Mvc4Async* 프로젝트.
- *WebAppAsync*: ASP.NET Web Forms 프로젝트를 다른 자습서에 사용 합니다.

## <a id="GizmosSynch"></a>  Gizmos 동기 작업 메서드

 다음 코드는 `Gizmos` gizmos의 목록을 표시 하는 데 사용 되는 동기 작업 메서드. (이 문서에 대 한 한 gizmo 가상의 기계적 장치입니다.) 

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample1.cs)]

다음 코드는 `GetGizmos` gizmo 서비스의 메서드.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample2.cs)]

`GizmoService GetGizmos` 메서드 gizmos 데이터의 목록을 반환 하는 ASP.NET Web API HTTP 서비스에는 URI를 전달 합니다. *WebAPIpgw* 프로젝트에 웹 API의 구현이 포함 되어 `gizmos, widget` 및 `product` 컨트롤러입니다.  
다음 이미지는 샘플 프로젝트에서 gizmos 뷰를 보여 줍니다.

![Gizmos](using-asynchronous-methods-in-aspnet-mvc-4/_static/image1.png)

## <a id="CreatingAsynchGizmos"></a>  비동기 Gizmos 작업 메서드 만들기

샘플에서는 새 [비동기](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) 및 [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) 키워드 (.NET 4.5 및 Visual Studio 2012에서 사용 가능) 하는 복잡 한 변환에 필요한 유지 관리 하는 일을 담당 하 고 컴파일러 비동기 프로그래밍 합니다. 컴파일러를 사용 하면 코드는 C#의 동기 제어 흐름을 생성 하는 사용 하 여 작성 하 고 컴파일러에 스레드를 차단 되지 않도록 하기 위해 콜백을 사용 하는 데 필요한 변환을 자동으로 적용 됩니다.

다음 코드는 `Gizmos` 동기 메서드 및 `GizmosAsync` 비동기 메서드. 브라우저가 지 원하는 경우는 [HTML 5 `<mark>` 요소](http://www.w3.org/wiki/HTML/Elements/mark)의 변경 내용을 표시 `GizmosAsync` 의 노란색 강조 표시 합니다.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample3.cs)]

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample4.cs?highlight=1,3,5)]

 다음과 같은 변경을 허용 하도록 적용 된는 `GizmosAsync` 비동기적 이어야 합니다.

- 메서드가로 표시 되는 [비동기](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) 본문의 부분에 대 한 콜백을 생성 하 고 자동으로 만들 수는 컴파일러가 키워드는 `Task<ActionResult>` 반환 되는 합니다.
- &quot;비동기&quot; 메서드 이름에 추가 되었습니다. "Async"를 추가 합니다.은 필요 하지 않지만 비동기 메서드를 작성할 때 규칙이 적용 됩니다.
- 반환 형식이에서 변경 된 `ActionResult` 를 `Task<ActionResult>`합니다. 반환 형식을 `Task<ActionResult>` 진행 중인 작업을 나타내며 비동기 작업이 완료 될 때까지 대기 하는 핸들 사용 하 여 메서드의 호출자를 제공 합니다. 이 경우 호출자는 웹 서비스. `Task<ActionResult>` 나타냅니다 진행 중인 작업의 결과 함께 `ActionResult.`
- [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) 키워드 웹 서비스 호출에 적용 되었습니다.
- 비동기 웹 서비스 API를 호출 했습니다 (`GetGizmosAsync`).

내부에 `GetGizmosAsync` 메서드는 다른 비동기 메서드 본문 `GetGizmosAsync` 호출 됩니다. `GetGizmosAsync` 즉시 반환는 `Task<List<Gizmo>>` 하는 데이터를 사용할 수 있는 경우을 결국 완료 됩니다. 코드 작업을 기다립니다 gizmo 데이터 구성할 때까지 다른 작업을 수행 하지 않으려면 때문에 (사용 하는 **await** 키워드)입니다. 사용할 수는 **await** 주석으로 추가 된 경우에 키워드는 **비동기** 키워드입니다.

**await** 키워드는 작업이 완료 될 때까지 스레드를 차단 하지 않습니다. 태스크에 대 한 콜백 메서드의 나머지 부분을 서명 하 고 즉시 반환 합니다. 대기 중인된 작업을 완료 하면 해당 콜백을 호출 되며 따라서 중단 메서드 오른쪽의 실행을 다시 시작 합니다. 사용 하 여 대 한 자세한 내용은 [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) 및 [비동기](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) 키워드 및 [작업](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) 네임 스페이스 참조는 [비동기 참조](https://docs.microsoft.com/dotnet/csharp/language-reference/keywords/async)합니다.

다음 코드는 `GetGizmos` 및 `GetGizmosAsync` 메서드.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample5.cs)]

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample6.cs?highlight=1,4-8)]

 비동기 변경이 하려고 하는 것과 유사한는 **GizmosAsync** 위에 있습니다. 

- 메서드 시그니처를 주석 처리는 [비동기](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) 키워드, 반환 형식으로 변경 되었습니다 `Task<List<Gizmo>>`, 및 *비동기* 메서드 이름에 추가 되었습니다.
- 비동기 [HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(VS.110).aspx) 클래스 대신 사용 되는 [WebClient](https://msdn.microsoft.com/library/system.net.webclient.aspx) 클래스입니다.
- [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) 에 적용 된 키워드는 [HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(VS.110).aspx) 비동기 메서드.

다음 그림에서는 비동기 gizmo 보기를 보여 줍니다.

![async](using-asynchronous-methods-in-aspnet-mvc-4/_static/image2.png)

브라우저 표현의 gizmos 데이터는 동기 호출으로 생성 된 뷰에 동일 합니다. 유일한 차이점은 비동기 버전 로드가 뛰어날 수 있습니다.

## <a id="Parallel"></a>  동시에 여러 작업을 수행합니다.

비동기 작업 메서드는 동작 여러 개의 독립적인 작업을 수행 해야 하는 경우 동기 메서드를 통해 중요 한 장점을 갖습니다. 제공 된 샘플 동기 메서드로 `PWG`(에 대 한 제품, Widget 및 Gizmos) 제품, widget 및 gizmos 목록을 가져오려면 세 가지 웹 서비스 호출의 결과 표시 합니다. [ASP.NET Web API](../../../web-api/index.md) 이러한 제공 하는 프로젝트 서비스 사용 하 여 [Task.Delay](https://msdn.microsoft.com/library/hh139096(VS.110).aspx) 시 지연 또는 느린 네트워크를 시뮬레이션 하기 위해 호출 합니다. 지연 비동기 500 밀리초로 설정 되 면 `PWGasync` 메서드는 동기 동안 완료를 약간 넘는 500 밀리초 `PWG` 버전 1, 500 밀리초 보다 우선 합니다. 동기 `PWG` 메서드는 다음 코드에 표시 됩니다.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample7.cs)]

비동기 `PWGasync` 메서드는 다음 코드에 표시 됩니다.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample8.cs?highlight=1,3,12)]

반환 된 보기를 표시 하는 다음 이미지는 **PWGasync** 메서드.

![pwgAsync](using-asynchronous-methods-in-aspnet-mvc-4/_static/image3.png)

## <a id="CancelToken"></a>  취소 토큰을 사용 하 여

반환 하는 비동기 작업 메서드에 `Task<ActionResult>`가지도록 되는 취소할 수 있는는 [CancellationToken](https://msdn.microsoft.com/library/system.threading.cancellationtoken(VS.110).aspx) 하나와 함께 제공 되는 경우 매개 변수는 [AsyncTimeout](https://msdn.microsoft.com/library/system.web.mvc.asynctimeoutattribute(VS.108).aspx) 특성입니다. 다음 코드는 `GizmosCancelAsync` 150 밀리초의 시간 제한 사용 하 여 메서드.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample9.cs?highlight=1-3,5,10)]

다음 코드에서는 사용 GetGizmosAsync 오버 로드는 [CancellationToken](https://msdn.microsoft.com/library/system.threading.cancellationtoken(VS.110).aspx) 매개 변수입니다.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample10.cs)]

제공 된 샘플 응용 프로그램에서 선택 하 고 *취소 토큰 데모* 호출 링크는 `GizmosCancelAsync` 메서드 비동기 호출의 취소를 보여 줍니다.

## <a id="ServerConfig"></a>  높은 동시성/높은 대기 시간이 웹 서비스 호출에 대 한 서버 구성

비동기 웹 응용 프로그램의 이점을 실현 하려면 기본 서버 구성을 일부 변경 해야 할 수 있습니다. 스트레스 테스트 비동기 웹 응용 프로그램을 구성할 때 염두 다음에 유의 합니다.

- Windows 7, Windows Vista 및 모든 Windows 클라이언트 운영 체제 최대 10 개의 동시 요청 했습니다. Windows Server 운영 체제를 과부하 상태에서 비동기 메서드의 이점을 활용 해야 합니다.
- 관리자 권한 명령 프롬프트에서 IIS를.NET 4.5를 등록 합니다.  
  %windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet\_regiis -i  
  참조 [ASP.NET IIS 등록 도구 (Aspnet\_regiis.exe)](https://msdn.microsoft.com/library/k6h9cz8h.aspx)
- 늘려야 할 수는 [HTTP.sys](https://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture) 1000에서 5000 기본값에서 큐 제한 합니다. 표시 될 수 설정이 너무 낮으면 [HTTP.sys](https://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture) HTTP 503 상태와 함께 요청을 거부 합니다. 변경 하려면 HTTP.sys 큐 제한:

    - IIS 관리자를 열고 응용 프로그램 풀 창으로 이동 합니다.
    - 대상 응용 프로그램 풀을 마우스 오른쪽 단추로 클릭 하 고 선택 **고급 설정**합니다.  
        ![advanced](using-asynchronous-methods-in-aspnet-mvc-4/_static/image4.png)
    - 에 **고급 설정** 대화 상자에서 변경 *Queue Length* 5000 1000에서입니다.  
        ![큐 길이](using-asynchronous-methods-in-aspnet-mvc-4/_static/image5.png)  
  
  Note 위의 이미지는 응용 프로그램 풀에서.NET 4.5를 사용 하는 경우에.NET framework v 4.0으로 나열 됩니다. 이 처럼 시간의 불일치가이 확인을 이해 하려면 다음을 참조 합니다.

    - [.NET 4.0으로 현재 위치 업그레이드 하는.NET 버전 관리 및 멀티 타기 팅-.NET 4.5](http://www.hanselman.com/blog/NETVersioningAndMultiTargetingNET45IsAnInplaceUpgradeToNET40.aspx)
    - [IIS 응용 프로그램 또는 AppPool 2.0 보다는 ASP.NET 3.5를 사용 하도록 설정 하는 방법](http://www.hanselman.com/blog/HowToSetAnIISApplicationOrAppPoolToUseASPNET35RatherThan20.aspx)
    - [.NET Framework 버전 및 종속성](https://msdn.microsoft.com/library/bb822049(VS.110).aspx)
- 응용 프로그램에서 웹 서비스를 이용 또는 HTTP를 통해는 백엔드와 통신 하는 System.NET 증가 시켜야 하는 경우는 [connectionManagement/maxconnection](https://msdn.microsoft.com/library/fb6y0fyc(VS.110).aspx) 요소입니다. ASP.NET 응용 프로그램에 대 한이 12 배 Cpu 수를 자동 구성 기능에 의해 제한 됩니다. 즉, 쿼드 프로세서에은 수는 최대 12 \* 4 = 48 IP 끝점에 대 한 동시 연결 합니다. 이에 연결 되기 때문에 [autoConfig](https://msdn.microsoft.com/library/7w2sway1(VS.110).aspx), 증가 하는 가장 쉬운 방법은 `maxconnection` ASP.NET 응용 프로그램으로 설정 하는 [System.Net.ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit(VS.110).aspx) 에 프로그래밍 방식으로 `Application_Start` 에서 메서드는 *global.asax* 파일입니다. 예제 다운로드 샘플을 참조 하십시오.
- .NET 4.5, 5000 기본값인 [MaxConcurrentRequestsPerCPU](https://blogs.msdn.com/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx) 이 괜찮아 야 합니다.
