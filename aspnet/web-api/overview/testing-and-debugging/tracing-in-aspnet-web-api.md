---
uid: web-api/overview/testing-and-debugging/tracing-in-aspnet-web-api
title: "ASP.NET Web API 2의에서 추적 | Microsoft Docs"
author: MikeWasson
description: "ASP.NET Web API에서 추적을 설정 하는 방법을 보여 줍니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/25/2014
ms.topic: article
ms.assetid: 66a837e9-600b-4b72-97a9-19804231c64a
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/testing-and-debugging/tracing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 7392ae5d9bc4c3aab45a9373099a0ee18e873a4f
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="tracing-in-aspnet-web-api-2"></a>ASP.NET Web API 2의 추적
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

> 웹 기반 응용 프로그램을 디버깅 하려고 시도할 때 좋은 집합 추적 로그에 대 한 조치에는 없습니다. 이 자습서에는 ASP.NET Web API에서 추적을 설정 하는 방법을 보여 줍니다. Web API 프레임 워크 수행 하는 작업 전후의 컨트롤러를 호출 하기 전에 추적 하려면이 기능을 사용할 수 있습니다. 사용자 고유의 코드를 추적에 사용할 수 있습니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - [Visual Studio 2017](https://www.visualstudio.com/downloads/) (Visual Studio 2015와 함께 작동)
> - Web API 2
> - [Microsoft.AspNet.WebApi.Tracing](http://www.nuget.org/packages/Microsoft.AspNet.WebApi.Tracing)


## <a name="enable-systemdiagnostics-tracing-in-web-api"></a>System.Diagnostics Web API에서에서 추적을 사용 하도록 설정

첫째, 새 ASP.NET 웹 응용 프로그램 프로젝트를 만들겠습니다. Visual Studio에서에서 **파일** 메뉴 선택 **새로**, 다음 **프로젝트**합니다. 아래 **템플릿**, **웹**선택, **ASP.NET 웹 응용 프로그램**합니다.

[![](tracing-in-aspnet-web-api/_static/image2.png)](tracing-in-aspnet-web-api/_static/image1.png)

웹 API 프로젝트 템플릿을 선택 합니다.

[![](tracing-in-aspnet-web-api/_static/image4.png)](tracing-in-aspnet-web-api/_static/image3.png)

**도구** 메뉴 선택 **라이브러리 패키지 관리자**, 다음 **패키지 관리 콘솔**합니다.

패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

[!code-console[Main](tracing-in-aspnet-web-api/samples/sample1.cmd)]

첫 번째 명령은 최신 웹 API 추적 패키지를 설치합니다. 또한 핵심 웹 API 패키지를 업데이트합니다. 두 번째 명령은 WebApi.WebHost 패키지를 최신 버전으로 업데이트합니다.

> [!NOTE]
> 사용 하 여 Web API의 특정 버전을 대상으로 하려는 경우 추적 패키지를 설치할 때-버전 플래그입니다.


응용 프로그램에서 WebApiConfig.cs 파일을 열고\_시작 폴더입니다. 다음 코드를 추가 하는 **등록** 메서드.

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample2.cs?highlight=6)]

이 코드는 추가 [SystemDiagnosticsTraceWriter](https://msdn.microsoft.com/library/system.web.http.tracing.systemdiagnosticstracewriter.aspx) Web API 파이프라인에는 클래스입니다. **SystemDiagnosticsTraceWriter** 클래스에 추적 정보를 기록 [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace)합니다.

추적을 보려면 디버거에서 응용 프로그램을 실행 합니다. 브라우저에서로 이동 `/api/values`합니다.

![](tracing-in-aspnet-web-api/_static/image5.png)

Trace 문은 Visual Studio의 출력 창에 기록 됩니다. (에서 **보기** 메뉴 선택 **출력**).

[![](tracing-in-aspnet-web-api/_static/image7.png)](tracing-in-aspnet-web-api/_static/image6.png)

때문에 **SystemDiagnosticsTraceWriter** 에 추적 정보를 기록 **System.Diagnostics.Trace**, 추가 추적 수신기를 등록할 수 있습니다; 예를 들어 쓸 추적 로그 파일에 있습니다. 추적 기록기에 대 한 자세한 내용은 참조는 [추적 수신기](https://msdn.microsoft.com/library/4y5y10s7.aspx) MSDN 항목.

### <a name="configuring-systemdiagnosticstracewriter"></a>SystemDiagnosticsTraceWriter를 구성합니다.

다음 코드에 추적 작성기를 구성 하는 방법을 보여 줍니다.

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample3.cs)]

제어할 수 있는 두 가지 설정이 있습니다.

- IsVerbose: false 인 경우, 각 추적 최소한의 정보만을 포함 합니다. True 이면 추적 추가 정보를 포함 합니다.
- MinimumLevel: 최소 추적 수준을 설정합니다. 추적 수준을 순서, 디버그, 정보, 경고, 오류 및 치명적 됩니다.

## <a name="adding-traces-to-your-web-api-application"></a>Web API 응용 프로그램에 추적 추가

추가 추적 작성기에 액세스할 수 즉시 Web API 파이프라인 하 여 만든 추적 합니다. 또한 사용자 고유의 코드를 추적 하려면 추적 기록기를 사용할 수 있습니다.

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample4.cs)]

추적 기록기를 얻기 위해 호출 **HttpConfiguration.Services.GetTraceWriter**합니다. 이 메서드는 컨트롤러에서를 통해 액세스할 수는 **ApiController.Configuration** 속성입니다.

추적을 작성 하기 위해 호출할 수 있습니다는 **ITraceWriter.Trace** 메서드를 직접 되지만 [ITraceWriterExtensions](https://msdn.microsoft.com/library/system.web.http.tracing.itracewriterextensions.aspx) 클래스 더 친숙 한 있는 몇 가지 확장 메서드를 정의 합니다. 예를 들어는 **정보** 메서드 위에 표시 된 추적 수준으로 추적을 만들 **정보**합니다.

## <a name="web-api-tracing-infrastructure"></a>Web API 추적 인프라

이 섹션에서는 웹 API에 대 한 사용자 지정 추적 기록기를 작성 하는 방법을 설명 합니다.

Microsoft.AspNet.WebApi.Tracing 패키지는 Web API에서 보다 일반적인 추적 인프라를 기반으로 빌드됩니다. Microsoft.AspNet.WebApi.Tracing를 사용 하지 않고 또한 연결 하 여 일부 다른 추적/로깅을 해제 라이브러리와 같은 [NLog](http://nlog-project.org/) 또는 [log4net](http://logging.apache.org/log4net/)합니다.

추적을 수집 하려면 구현 된 **ITraceWriter** 인터페이스입니다. 간단한 예는 다음과 같습니다.

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample5.cs)]

**ITraceWriter.Trace** 메서드 추적을 만듭니다. 호출자에는 범주와 추적 수준을 지정합니다. 범주에는 모든 사용자 정의 문자열일 수 있습니다. 구현 **추적** 에서 다음을 수행 해야 합니다.

1. 새 **TraceRecord**합니다. 표시 된 것 처럼 요청, 범주 및 추적 수준으로 초기화 합니다. 이러한 값은 호출자에 의해 제공 됩니다.
2. 호출 된 *traceAction* 위임 합니다. 이 대리자 내 호출자의 나머지를 작성 하는 **TraceRecord**합니다.
3. 쓰기는 **TraceRecord**, 사람에 해당 하는 로깅 기법을 사용 하 여 합니다. 이 예제를 단순히 호출 **System.Diagnostics.Trace**합니다.

## <a name="setting-the-trace-writer"></a>추적 기록기를 설정합니다.

추적을 사용 하려면 웹 API를 사용 하도록 구성 해야 프로그램 **ITraceWriter** 구현 합니다. 통해이 작업은 **HttpConfiguration** 다음 코드와 같이 개체:

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample6.cs)]

하나의 추적 기록기를 활성화할 수 있습니다. 기본적으로 웹 API 설정는 &quot;아무&quot; 는 아무 작업도 수행 하는 추적 프로그램입니다. (의 &quot;아무&quot; 추적 프로그램 존재 추적 코드에서 추적 작성기 인지 확인 하지 않도록 **null** 추적을 작성 하기 전에.)

## <a name="how-web-api-tracing-works"></a>API 추적 작동 방법 웹

웹 API 사용에 웹 API를 사용 하 여 추적 한 *외관* 패턴: Web API 추적을 사용 하는 경우 추적 호출을 수행 하는 클래스와 함께 요청 파이프라인의 다양 한 부분을 래핑합니다.

예를 들어 컨트롤러를 선택 하면 파이프라인 사용 하 여는 **IHttpControllerSelector** 인터페이스입니다. 사용 하도록 설정 하는 추적을 구현 하는 클래스는 pipleline 삽입 **IHttpControllerSelector** 하지만 실제 구현에 통해 호출 합니다.

![Web API 추적 외관 패턴을 사용 합니다.](tracing-in-aspnet-web-api/_static/image8.png)

이 디자인의 이점은 다음과 같습니다.

- 추적 기록기를 추가 하지 않으면 추적 구성 요소는 인스턴스화되지 않으며 성능 영향을 주지 않습니다.
- 와 같은 기본 서비스를 대체 하는 경우 **IHttpControllerSelector** 사용자 사용자 지정 구현으로 추적에 영향을 주지 추적 래퍼 개체에 의해 수행 되기 때문에 있습니다.

기본 대체 하 여 사용자 고유의 사용자 지정 framework를 사용 하는 전체 웹 API 추적 프레임 워크를 바꿀 수도 있습니다 **ITraceManager** 서비스:

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample7.cs)]

구현 **ITraceManager.Initialize** 추적 시스템을 초기화할 수 있습니다. 이 대체 유의 *전체* 추적 프레임 워크, 웹 API에 포함 된 추적 코드를 모두 포함 합니다.
