---
uid: web-api/overview/advanced/configuring-aspnet-web-api
title: ASP.NET Web API 2 구성 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/31/2014
ms.topic: article
ms.assetid: 9e10a700-8d91-4d2e-a31e-b8b569fe867c
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/advanced/configuring-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: de2396710fb9434c84bf14a2faa37b98154f34d8
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30874982"
---
<a name="configuring-aspnet-web-api-2"></a>ASP.NET Web API 2 구성합니다.
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

이 항목에서는 ASP.NET Web API를 구성 하는 방법에 설명 합니다.

- [구성 설정](#settings)
- [ASP.NET 호스팅와 Web API 구성](#webhost)
- [Web API OWIN 자체 호스팅을 사용 구성](#selfhost)
- [전역 웹 API 서비스](#services)
- [-컨트롤러 구성](#percontrollerconfig)

<a id="settings"></a>
## <a name="configuration-settings"></a>구성 설정

구성 설정은 웹 API에 정의 된는 [HttpConfiguration](https://msdn.microsoft.com/library/system.web.http.httpconfiguration.aspx) 클래스입니다.

| 멤버 | 설명 |
| --- | --- |
| **DependencyResolver** | 컨트롤러에 대 한 종속성 주입을 사용 하도록 설정 합니다. 참조 [Web API 종속성 확인자를 사용 하 여](dependency-injection.md)합니다. |
| **필터** | 작업 필터입니다. |
| **포맷터** | [미디어 유형 포맷터](../formats-and-model-binding/media-formatters.md)합니다. |
| **IncludeErrorDetailPolicy** | 서버 HTTP 응답 메시지에 예외 메시지, 스택 추적 등의 오류 정보를 포함할지 여부를 지정 합니다. 참조 [IncludeErrorDetailPolicy](https://msdn.microsoft.com/library/system.web.http.includeerrordetailpolicy(v=vs.108))합니다. |
| **Initializer** | 최종 초기화를 수행 하는 함수는 **HttpConfiguration**합니다. |
| **MessageHandlers** | [HTTP 메시지 처리기](http-message-handlers.md)합니다. |
| **ParameterBindingRules** | 바인딩 매개 변수에서 컨트롤러 작업에 대 한 규칙의 컬렉션입니다. |
| **속성** | 일반 속성 모음입니다. |
| **경로** | 경로의 컬렉션입니다. 참조 [ASP.NET Web API의에서 라우팅](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)합니다. |
| **서비스** | 서비스의 컬렉션입니다. 참조 [서비스](#services)합니다. |


## <a name="prerequisites"></a>전제 조건

[Visual Studio 2017](https://www.visualstudio.com/vs/) Community, Professional 또는 Enterprise Edition.

<a id="webhost"></a>
## <a name="configuring-web-api-with-aspnet-hosting"></a>ASP.NET 호스팅와 Web API 구성

ASP.NET 응용 프로그램에서 Web API를 호출 하 여 구성 [GlobalConfiguration.Configure](https://msdn.microsoft.com/library/system.web.http.globalconfiguration.configure.aspx) 에 **응용 프로그램\_시작** 메서드. **구성** 형식의 단일 매개 변수를 사용 하 여 대리자 메서드를 사용 하며 **HttpConfiguration**합니다. 대리자 내 구성 프로그램을 모두 수행 합니다.

익명 대리자를 사용 하는 예제는 다음과 같습니다.

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample1.cs)]

Visual Studio 2017 년에서 "ASP.NET 웹 응용 프로그램" 프로젝트 템플릿을 자동으로 설정 구성 코드에서 "웹 API"를 선택 하는 경우는 **새 ASP.NET 프로젝트** 대화 상자.

[![](configuring-aspnet-web-api/_static/image2.png)](configuring-aspnet-web-api/_static/image1.png)

프로젝트 템플릿은 응용 프로그램 안에 WebApiConfig.cs 라는 파일을 만듭니다\_시작 폴더입니다. 이 코드 파일 Web API 구성 코드를 입력 해야 하는 대리자를 정의 합니다.

![](configuring-aspnet-web-api/_static/image3.png)

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample2.cs?highlight=12)]

프로젝트 템플릿에 또한에서 대리자를 호출 하는 코드 추가 **응용 프로그램\_시작**합니다.

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample3.cs?highlight=5)]

<a id="selfhost"></a>
## <a name="configuring-web-api-with-owin-self-hosting"></a>Web API OWIN 자체 호스팅을 사용 구성

경우 OWIN과 자체 호스트를 만들 새 **HttpConfiguration** 인스턴스. 이 인스턴스에서 구성을 수행 하 고 그런 다음 인스턴스를는 **Owin.UseWebApi** 확장 메서드.

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample4.cs)]

자습서 [Self-Host ASP.NET Web API 2를 사용 하 여 OWIN](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md) 전체 단계를 보여 줍니다.

<a id="services"></a>
## <a name="global-web-api-services"></a>전역 웹 API 서비스

**HttpConfiguration.Services** 컬렉션 Web API 컨트롤러 선택 및 콘텐츠 협상 등의 다양 한 작업을 수행 하기 위해 사용 하는 글로벌 서비스의 집합을 포함 합니다.

> [!NOTE]
> **서비스** 컬렉션 서비스 검색 또는 종속성 주입을 위한 일반 용도의 메커니즘은 없습니다. Web API 프레임 워크에 알려진 서비스 종류를 저장 하기만 합니다.


**서비스** 컬렉션 서비스의 기본 집합으로 초기화 되 고 사용자 고유의 사용자 지정 구현을 제공할 수 있습니다. 인스턴스가 하나만 있을 수 있지만 다른 일부 서비스에서 여러 인스턴스를 지원 합니다. 그러나 (컨트롤러 수준에서 서비스를 제공할 수도 있습니다; 참조 [-컨트롤러 구성](#percontrollerconfig)합니다.

단일 인스턴스 서비스


| 서비스 | 설명 |
| --- | --- |
| **IActionValueBinder** | 매개 변수 바인딩을 가져옵니다. |
| **IApiExplorer** | 응용 프로그램에 의해 노출 된 Api의 설명을 가져옵니다. 참조 [웹 API에 대 한 도움말 페이지를 만드는](../getting-started-with-aspnet-web-api/creating-api-help-pages.md)합니다. |
| **IAssembliesResolver** | 응용 프로그램에 대 한 어셈블리의 목록을 가져옵니다. 참조 [라우팅 및 작업 선택](../web-api-routing-and-actions/routing-and-action-selection.md)합니다. |
| **IBodyModelValidator** | 미디어 유형 포맷터는 요청 본문에서 읽을 수 있는 모델의 유효성을 검사 합니다. |
| **IContentNegotiator** | 콘텐츠 협상을 수행 합니다. |
| **IDocumentationProvider** | Api에 대 한 설명서를 제공합니다. 기본값은 **null**합니다. 참조 [웹 API에 대 한 도움말 페이지를 만드는](../getting-started-with-aspnet-web-api/creating-api-help-pages.md)합니다. |
| **IHostBufferPolicySelector** | 호스트 HTTP 메시지의 엔터티 본문을 버퍼링 해야 하는지 여부를 나타냅니다. |
| **IHttpActionInvoker** | 컨트롤러 동작을 호출합니다. 참조 [라우팅 및 작업 선택](../web-api-routing-and-actions/routing-and-action-selection.md)합니다. |
| **IHttpActionSelector** | 컨트롤러 동작을 선택 합니다. 참조 [라우팅 및 작업 선택](../web-api-routing-and-actions/routing-and-action-selection.md)합니다. |
| **IHttpControllerActivator** | 컨트롤러를 활성화합니다. 참조 [라우팅 및 작업 선택](../web-api-routing-and-actions/routing-and-action-selection.md)합니다. |
| **IHttpControllerSelector** | 컨트롤러를 선택합니다. 참조 [라우팅 및 작업 선택](../web-api-routing-and-actions/routing-and-action-selection.md)합니다. |
| **IHttpControllerTypeResolver** | 응용 프로그램에서 Web API 컨트롤러 형식의 목록을 제공합니다. 참조 [라우팅 및 작업 선택](../web-api-routing-and-actions/routing-and-action-selection.md)합니다. |
| **ITraceManager** | 추적 프레임 워크를 초기화합니다. 참조 [ASP.NET Web API의에서 추적](../testing-and-debugging/tracing-in-aspnet-web-api.md)합니다. |
| **ITraceWriter** | 추적 기록기를 제공합니다. 기본값은 "아무" 추적 기록기입니다. 참조 [ASP.NET Web API의에서 추적](../testing-and-debugging/tracing-in-aspnet-web-api.md)합니다. |
| **IModelValidatorCache** | 모델 유효성 검사기의 캐시를 제공합니다. |

다중 인스턴스 서비스


|                 서비스                 |                                                                                                              설명                                                                                                               |
|-----------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <strong>IFilterProvider</strong>     |                                                                                           컨트롤러 작업에 대 한 필터의 목록을 반환합니다.                                                                                           |
|  <strong>ModelBinderProvider</strong>   |                                                                                                지정된 된 형식에 대 한 모델 바인더를 반환합니다.                                                                                                |
| <strong>ModelMetadataProvider</strong>  |                                                                                                     모델에 대 한 메타 데이터를 제공합니다.                                                                                                     |
| <strong>ModelValidatorProvider</strong> |                                                                                                   모델 유효성 검사기를 제공 합니다.                                                                                                    |
|  <strong>ValueProviderFactory</strong>  | 값 공급자를 만듭니다. 자세한 내용은 Mike Stall 블로그 게시물을 참조 하십시오. [WebAPI에 사용자 지정 값 공급자를 만드는 방법](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx) |

여러 인스턴스 서비스에 사용자 지정 구현을 추가 하려면 **추가** 또는 **삽입** 에 **서비스** 컬렉션:

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample5.cs)]

단일 인스턴스 서비스 사용자 지정 구현으로 교체 하려면 호출 **대체** 에 **서비스** 컬렉션:

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample6.cs)]

<a id="percontrollerconfig"></a>
## <a name="per-controller-configuration"></a>-컨트롤러 구성

-컨트롤러 별로 다음 설정을 재정의할 수 있습니다.

- 미디어 유형 포맷터
- 매개 변수 바인딩 규칙
- 서비스

이렇게 하려면 사용자 지정 특성을 구현 하는 정의 **IControllerConfiguration** 인터페이스입니다. 컨트롤러에 특성을 적용 합니다.

다음 예제에서는 사용자 지정 포맷터와 기본 미디어 유형 포맷터를 대체합니다.

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample7.cs)]

**IControllerConfiguration.Initialize** 메서드는 두 개의 매개 변수를 사용 합니다.

- **HttpControllerSettings** 개체
- **HttpControllerDescriptor** 개체

**HttpControllerDescriptor** 정보 제공 목적으로 (예를 들어 두 명의 컨트롤러를 구분 하기 위해)를 검사할 수 있습니다는 컨트롤러에 대 한 설명을 포함 합니다.

사용 하 여 **HttpControllerSettings** 컨트롤러를 구성 하는 개체입니다. 이 개체의 구성 매개 변수-컨트롤러 별로 재정의할 수 있는 하위 집합을 포함 합니다. 모든 설정을 변경 하지 않으면 기본적으로 전역 **HttpConfiguration** 개체입니다.
