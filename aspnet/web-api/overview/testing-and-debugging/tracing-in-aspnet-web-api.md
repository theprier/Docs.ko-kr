---
uid: web-api/overview/testing-and-debugging/tracing-in-aspnet-web-api
title: ASP.NET Web API 2에서에서 추적 | Microsoft Docs
author: MikeWasson
description: ASP.NET Web API에서 추적을 사용 하는 방법을 보여 줍니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/25/2014
ms.topic: article
ms.assetid: 66a837e9-600b-4b72-97a9-19804231c64a
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/testing-and-debugging/tracing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: f9c33e62a1d04bc7851be13560a2bd39e997448f
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37366866"
---
<a name="tracing-in-aspnet-web-api-2"></a>ASP.NET Web API 2에서 추적
====================
[Mike Wasson](https://github.com/MikeWasson)

> 웹 기반 응용 프로그램을 디버그 하려는 경우에 좋은 집합이 추적 로그에 대 한 조치는 없습니다. 이 자습서에서는 ASP.NET Web API에서 추적을 사용 하는 방법을 보여줍니다. Web API 프레임 워크에 컨트롤러 호출 전후에 추적 하려면이 기능을 사용할 수 있습니다. 사용자 고유의 코드를 추적에 사용할 수 있습니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
> 
> 
> - [Visual Studio 2017](https://www.visualstudio.com/downloads/) (Visual Studio 2015를 사용 하 여 작동)
> - Web API 2
> - [Microsoft.AspNet.WebApi.Tracing](http://www.nuget.org/packages/Microsoft.AspNet.WebApi.Tracing)


## <a name="enable-systemdiagnostics-tracing-in-web-api"></a>Web API에서에서 추적 System.Diagnostics를 사용 하도록 설정

먼저 새 ASP.NET 웹 응용 프로그램 프로젝트를 만듭니다. Visual Studio에서에서 **파일** 메뉴에서 **새로 만들기**, 한 다음 **프로젝트**합니다. 아래 **템플릿을**를 **웹**를 선택 **ASP.NET 웹 응용 프로그램**합니다.

[![](tracing-in-aspnet-web-api/_static/image2.png)](tracing-in-aspnet-web-api/_static/image1.png)

Web API 프로젝트 템플릿을 선택 합니다.

[![](tracing-in-aspnet-web-api/_static/image4.png)](tracing-in-aspnet-web-api/_static/image3.png)

**도구** 메뉴에서 **라이브러리 패키지 관리자**, 한 다음 **패키지 관리 콘솔**.

패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

[!code-console[Main](tracing-in-aspnet-web-api/samples/sample1.cmd)]

첫 번째 명령은 최신 Web API 추적 패키지를 설치합니다. 또한 core Web API 패키지를 업데이트합니다. 두 번째 명령은 최신 버전으로 WebApi.WebHost 패키지를 업데이트합니다.

> [!NOTE]
> 사용 하 여 웹 API의 특정 버전을 대상으로 하려는 경우 추적 패키지를 설치할 때-버전 플래그입니다.


앱에서 WebApiConfig.cs 파일을 열고\_시작 폴더입니다. 다음 코드를 추가 합니다 **등록** 메서드.

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample2.cs?highlight=6)]

이 코드를 추가 합니다 [SystemDiagnosticsTraceWriter](https://msdn.microsoft.com/library/system.web.http.tracing.systemdiagnosticstracewriter.aspx) Web API 파이프라인에 클래스입니다. 합니다 **SystemDiagnosticsTraceWriter** 클래스에 대 한 추적 정보를 기록 [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace)합니다.

추적을 확인 하려면 디버거에서 응용 프로그램을 실행 합니다. 브라우저에서 이동 `/api/values`합니다.

![](tracing-in-aspnet-web-api/_static/image5.png)

Trace 문 Visual Studio의 출력 창에 기록 됩니다. (에서 합니다 **뷰** 메뉴에서 **출력**).

[![](tracing-in-aspnet-web-api/_static/image7.png)](tracing-in-aspnet-web-api/_static/image6.png)

때문에 **SystemDiagnosticsTraceWriter** 추적을 작성 **System.Diagnostics.Trace**, 추가 추적 수신기를 등록할 수 있습니다; 예를 들어 쓸 추적 로그 파일에 있습니다. 추적 기록기에 대 한 자세한 내용은 참조는 [추적 수신기](https://msdn.microsoft.com/library/4y5y10s7.aspx) MSDN 항목.

### <a name="configuring-systemdiagnosticstracewriter"></a>SystemDiagnosticsTraceWriter를 구성합니다.

다음 코드에 추적 작성기를 구성 하는 방법을 보여 줍니다.

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample3.cs)]

제어할 수 있는 두 가지 설정이 있습니다.

- IsVerbose: false 인 경우 각 추적 최소한의 정보만을 포함 합니다. True 이면 추적에는 자세한 정보가 포함 됩니다.
- MinimumLevel: 최소 추적 수준을 설정합니다. 추적 수준을 순서 대로 디버그, 정보, 경고, 오류 및 치명적 됩니다.

## <a name="adding-traces-to-your-web-api-application"></a>웹 API 응용 프로그램에 추적 추가

추적 작성기를 추가 즉시 액세스할 수 있게 하는 Web API 파이프라인을 만들어 추적 합니다. 또한 사용자 고유의 코드를 추적 하려면 추적 작성기를 사용할 수 있습니다.

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample4.cs)]

호출 추적 기록기를 가져오려면 **HttpConfiguration.Services.GetTraceWriter**합니다. 이 메서드는 컨트롤러에서를 통해 액세스할 수 합니다 **ApiController.Configuration** 속성입니다.

추적을 작성 하려면 호출할 수 있습니다 합니다 **ITraceWriter.Trace** 메서드를 직접 있지만 [ITraceWriterExtensions](https://msdn.microsoft.com/library/system.web.http.tracing.itracewriterextensions.aspx) 더 친숙 한 수 있는 몇 가지 확장 메서드를 정의 하는 클래스입니다. 예를 들어 합니다 **정보** 위에 표시 된 메서드는 추적 수준을 사용 하 여 추적을 만듭니다 **정보**합니다.

## <a name="web-api-tracing-infrastructure"></a>Web API 추적 인프라

이 섹션에서는 웹 API에 대 한 사용자 지정 추적 작성기를 작성 하는 방법을 설명 합니다.

Microsoft.AspNet.WebApi.Tracing 패키지는 Web API는 보다 일반적인 추적 인프라를 기반으로 합니다. Microsoft.AspNet.WebApi.Tracing를 사용 하는 대신도 연결 하 여 일부 다른 추적/고 라이브러리와 같은 [NLog](http://nlog-project.org/) 하거나 [log4net](http://logging.apache.org/log4net/)합니다.

추적을 수집 하려면 구현 합니다 **ITraceWriter** 인터페이스입니다. 간단한 예는 다음과 같습니다.

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample5.cs)]

합니다 **ITraceWriter.Trace** 메서드는 추적을 만듭니다. 호출자에 게 범주 및 추적 수준을 지정 합니다. 범주에는 사용자 정의 문자열일 수 있습니다. 구현의 **추적** 다음을 수행 해야 합니다.

1. 새 **TraceRecord**합니다. 표시 된 것 처럼 요청, 범주 및 추적 수준을 사용 하 여 초기화 합니다. 이러한 값은 호출자에 의해 제공 됩니다.
2. 호출 된 *traceAction* 위임 합니다. 이 대리자 내에서 호출자는 나머지를 입력 하 여 **TraceRecord**합니다.
3. 작성 된 **TraceRecord**, 원하는 모든 로깅 기술을 사용 하 여 합니다. 여기에 표시 된 예제를 단순히 호출 **System.Diagnostics.Trace**합니다.

## <a name="setting-the-trace-writer"></a>추적 기록기를 설정합니다.

추적을 사용 하려면 사용 하는 웹 API를 구성 해야 하 **ITraceWriter** 구현 합니다. 통해이 작업을 수행 합니다 **HttpConfiguration** 다음 코드 에서처럼 개체:

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample6.cs)]

하나의 추적 기록기를 활성화할 수 있습니다. 기본적으로 웹 API는 다음과 같이 설정 됩니다.는 &quot;아무&quot; 아무 작업도 수행 하지는 추적 프로그램입니다. (합니다 &quot;아무&quot; 추적 프로그램에 추적 코드는 추적 기록기가 있는지 여부를 확인 하지 않아도 되도록 존재 **null** 추적을 작성 하기 전에.)

## <a name="how-web-api-tracing-works"></a>어떻게 작동을 추적 하는 API를 웹

Web API 사용 시에 웹 API를 사용 하 여 추적을 *외관* 패턴: Web API 추적을 사용 하는 경우 추적 호출을 수행 하는 클래스를 사용 하 여 요청 파이프라인의 다양 한 부분을 래핑합니다.

예를 들어 컨트롤러를 선택할 때 파이프라인을 사용 하 여 **IHttpControllerSelector** 인터페이스입니다. pipleline 사용 하도록 설정 하는 추적 기능을 구현 하는 클래스를 삽입 **IHttpControllerSelector** 하지만 실제 구현을 통해 호출 합니다.

![Web API 추적 외관 패턴을 사용합니다.](tracing-in-aspnet-web-api/_static/image8.png)

이 디자인의 이점은 다음과 같습니다.

- 추적 기록기를 추가 하면 추적 구성 요소는 인스턴스화되지 않으며 성능 영향이 없습니다.
- 와 같은 기본 서비스를 대체 하는 경우 **IHttpControllerSelector** 고유한 사용자 지정 구현을 사용 하 여 추적에 영향을 주지 추적 래퍼 개체로 수행 되기 때문에 있습니다.

기본 대체 하 여 사용자 고유의 사용자 지정 프레임 워크를 사용 하 여 전체 Web API 추적 프레임 워크를 바꿀 수도 있습니다 **ITraceManager** 서비스:

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample7.cs)]

구현 **ITraceManager.Initialize** 추적 시스템을 초기화 합니다. 이 대체 알고 있어야 합니다 *전체* 모든 Web API로 빌드되는 추적 코드를 포함 하 여 추적 프레임 워크입니다.
