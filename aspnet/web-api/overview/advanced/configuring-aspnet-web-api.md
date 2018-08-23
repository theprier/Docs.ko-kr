---
uid: web-api/overview/advanced/configuring-aspnet-web-api
title: ASP.NET Web API 2 구성 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 03/31/2014
ms.assetid: 9e10a700-8d91-4d2e-a31e-b8b569fe867c
msc.legacyurl: /web-api/overview/advanced/configuring-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 81119b35fb375bb2299edc4f08289a89aecfcd88
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41836720"
---
<a name="configuring-aspnet-web-api-2"></a>ASP.NET Web API 2 구성
====================
[Mike Wasson](https://github.com/MikeWasson)

이 항목에서는 ASP.NET Web API를 구성 하는 방법을 설명 합니다.

- [구성 설정](#settings)
- [Web API를 사용 하 여 ASP.NET 호스팅 구성](#webhost)
- [OWIN 자체 호스팅을 사용 하 여 Web API 구성](#selfhost)
- [글로벌 웹 API 서비스](#services)
- [-컨트롤러 구성](#percontrollerconfig)

<a id="settings"></a>
## <a name="configuration-settings"></a>구성 설정

Web API 구성 설정에 정의 된 [HttpConfiguration](https://msdn.microsoft.com/library/system.web.http.httpconfiguration.aspx) 클래스입니다.

| 멤버 | 설명 |
| --- | --- |
| **DependencyResolver** | 컨트롤러에 대 한 종속성 주입을 사용 하도록 설정 합니다. 참조 [Web API 종속성 확인자를 사용 하 여](dependency-injection.md)입니다. |
| **필터** | 작업 필터입니다. |
| **포맷터** | [미디어 유형 포맷터](../formats-and-model-binding/media-formatters.md)합니다. |
| **IncludeErrorDetailPolicy** | 서버 HTTP 응답 메시지에 예외 메시지, 스택 추적 등의 오류 정보를 포함할지 여부를 지정 합니다. 참조 [IncludeErrorDetailPolicy](https://msdn.microsoft.com/library/system.web.http.includeerrordetailpolicy(v=vs.108))합니다. |
| **Initializer** | 구성의 최종 초기화를 수행 하는 함수를 **HttpConfiguration**합니다. |
| **MessageHandlers** | [HTTP 메시지 처리기](http-message-handlers.md)합니다. |
| **ParameterBindingRules** | 컨트롤러 작업에서 매개 변수를 바인딩하는 규칙의 컬렉션입니다. |
| **속성** | 제네릭 속성 모음입니다. |
| **경로** | 경로의 컬렉션입니다. 참조 [ASP.NET Web API에서에서 라우팅](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)합니다. |
| **서비스** | 서비스의 컬렉션입니다. 참조 [Services](#services)합니다. |


## <a name="prerequisites"></a>전제 조건

[Visual Studio 2017](https://www.visualstudio.com/vs/) Community, Professional 또는 Enterprise Edition.

<a id="webhost"></a>
## <a name="configuring-web-api-with-aspnet-hosting"></a>Web API를 사용 하 여 ASP.NET 호스팅 구성

ASP.NET 응용 프로그램에서 Web API를 호출 하 여 구성 합니다 [GlobalConfiguration.Configure](https://msdn.microsoft.com/library/system.web.http.globalconfiguration.configure.aspx) 에 **응용 프로그램\_시작** 메서드. 합니다 **구성** 메서드는 형식의 단일 매개 변수를 사용 하 여 대리자 **HttpConfiguration**합니다. 모든 대리자 내에 구성 수행 합니다.

익명 대리자를 사용 하는 예제는 다음과 같습니다.

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample1.cs)]

Visual Studio 2017에서 "ASP.NET 웹 응용 프로그램" 프로젝트 템플릿을 자동으로 설정 구성 코드에 "Web API"를 선택 합니다 **새 ASP.NET 프로젝트** 대화 합니다.

[![](configuring-aspnet-web-api/_static/image2.png)](configuring-aspnet-web-api/_static/image1.png)

프로젝트 템플릿은 앱 내에서 WebApiConfig.cs 파일을 만듭니다\_시작 폴더입니다. 이 코드 파일에 Web API 구성 코드를 두어야 하는 대리자를 정의 합니다.

![](configuring-aspnet-web-api/_static/image3.png)

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample2.cs?highlight=12)]

추가 대리자를 호출 하는 코드 프로젝트 템플릿은 **응용 프로그램\_시작**합니다.

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample3.cs?highlight=5)]

<a id="selfhost"></a>
## <a name="configuring-web-api-with-owin-self-hosting"></a>OWIN 자체 호스팅을 사용 하 여 Web API 구성

OWIN을 사용 하 여 자체 호스팅 인 경우 새로 만듭니다 **HttpConfiguration** 인스턴스. 이 인스턴스에서 모든 구성을 수행 하 고 인스턴스를 전달 합니다 **Owin.UseWebApi** 확장 메서드.

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample4.cs)]

이 자습서 [여 ASP.NET Web API 2를 사용 하 여 OWIN](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md) 완료 단계를 보여 줍니다.

<a id="services"></a>
## <a name="global-web-api-services"></a>글로벌 웹 API 서비스

합니다 **HttpConfiguration.Services** 컬렉션 Web API 컨트롤러 선택 및 콘텐츠 협상 같은 다양 한 작업을 수행 하는 데 사용 하는 글로벌 서비스 집합을 포함 합니다.

> [!NOTE]
> 합니다 **Services** 컬렉션 서비스 검색 또는 종속성 주입을 위한 일반 용도의 메커니즘은 없습니다. Web API 프레임 워크에 알려지지 않은 서비스 유형 저장 하기만 합니다.


합니다 **Services** 컬렉션 서비스의 기본 집합을 사용 하 여 초기화 되 고 사용자 고유의 사용자 지정 구현을 제공할 수 있습니다. 일부 서비스 인스턴스를 하나만 가질 수 있습니다 다른 여러 인스턴스를 지원 합니다. 그러나 (컨트롤러 수준에서 서비스를 제공할 수도 있습니다; 참조 [-컨트롤러 구성](#percontrollerconfig)합니다.

단일 인스턴스 서비스


| 서비스 | 설명 |
| --- | --- |
| **IActionValueBinder** | 매개 변수에 대 한 바인딩을 가져옵니다. |
| **IApiExplorer** | 응용 프로그램에 의해 노출 된 Api의 설명을 가져옵니다. 참조 [Web API에 대 한 도움말 페이지 만들기](../getting-started-with-aspnet-web-api/creating-api-help-pages.md)합니다. |
| **IAssembliesResolver** | 응용 프로그램에 대 한 어셈블리의 목록을 가져옵니다. 참조 [라우팅 및 작업 선택](../web-api-routing-and-actions/routing-and-action-selection.md)합니다. |
| **IBodyModelValidator** | 미디어 유형 포맷터를 요청 본문에서 읽을 수 있는 모델의 유효성을 검사 합니다. |
| **IContentNegotiator** | 콘텐츠 협상을 수행 합니다. |
| **IDocumentationProvider** | Api에 대 한 설명서를 제공합니다. 기본값은 **null**합니다. 참조 [Web API에 대 한 도움말 페이지 만들기](../getting-started-with-aspnet-web-api/creating-api-help-pages.md)합니다. |
| **IHostBufferPolicySelector** | 호스트 HTTP 메시지 엔터티 본문을 버퍼링 해야 하는지 여부를 나타냅니다. |
| **IHttpActionInvoker** | 컨트롤러 작업을 호출합니다. 참조 [라우팅 및 작업 선택](../web-api-routing-and-actions/routing-and-action-selection.md)합니다. |
| **IHttpActionSelector** | 컨트롤러 작업을 선택합니다. 참조 [라우팅 및 작업 선택](../web-api-routing-and-actions/routing-and-action-selection.md)합니다. |
| **IHttpControllerActivator** | 컨트롤러를 활성화합니다. 참조 [라우팅 및 작업 선택](../web-api-routing-and-actions/routing-and-action-selection.md)합니다. |
| **IHttpControllerSelector** | 컨트롤러를 선택합니다. 참조 [라우팅 및 작업 선택](../web-api-routing-and-actions/routing-and-action-selection.md)합니다. |
| **IHttpControllerTypeResolver** | 응용 프로그램에서 Web API 컨트롤러 형식 목록을 제공합니다. 참조 [라우팅 및 작업 선택](../web-api-routing-and-actions/routing-and-action-selection.md)합니다. |
| **ITraceManager** | 추적 프레임 워크를 초기화 합니다. 참조 [ASP.NET Web API에서에서 추적](../testing-and-debugging/tracing-in-aspnet-web-api.md)합니다. |
| **ITraceWriter** | 추적 기록기를 제공합니다. 기본값은 no-op "추적 작성기입니다. 참조 [ASP.NET Web API에서에서 추적](../testing-and-debugging/tracing-in-aspnet-web-api.md)합니다. |
| **IModelValidatorCache** | 모델 유효성 검사기의 캐시를 제공합니다. |

다중 인스턴스 서비스


|                 서비스                 |                                                                                                              설명                                                                                                               |
|-----------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <strong>IFilterProvider</strong>     |                                                                                           컨트롤러 작업에 대 한 필터의 목록을 반환합니다.                                                                                           |
|  <strong>ModelBinderProvider</strong>   |                                                                                                지정된 된 형식에 대 한 모델 바인더를 반환 합니다.                                                                                                |
| <strong>ModelMetadataProvider</strong>  |                                                                                                     모델에 대 한 메타 데이터를 제공합니다.                                                                                                     |
| <strong>ModelValidatorProvider</strong> |                                                                                                   모델 유효성 검사기를 제공 합니다.                                                                                                    |
|  <strong>ValueProviderFactory</strong>  | 값 공급자를 만듭니다. 자세한 내용은 Mike Stall의 블로그 게시물을 참조 하세요. [WebAPI에서 사용자 지정 값 공급자를 만드는 방법](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx) |

사용자 지정 구현에는 다중 인스턴스 서비스를 추가 하려면 호출 **추가** 또는 **삽입** 에 **Services** 컬렉션:

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample5.cs)]

호출 하는 단일 인스턴스 서비스 사용자 지정 구현으로 바꾸려면 **바꿉니다** 에 **Services** 컬렉션:

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample6.cs)]

<a id="percontrollerconfig"></a>
## <a name="per-controller-configuration"></a>-컨트롤러 구성

-컨트롤러 별로 다음 설정을 재정의할 수 있습니다.

- 미디어 유형 포맷터
- 매개 변수 바인딩 규칙
- 서비스

이 위해 구현 하는 사용자 지정 특성을 정의 합니다 **IControllerConfiguration** 인터페이스입니다. 컨트롤러에 특성을 적용 합니다.

다음 예제에서는 기본 미디어 유형 포맷터를 사용자 지정 포맷터를 바꿉니다.

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample7.cs)]

합니다 **IControllerConfiguration.Initialize** 메서드는 두 개의 매개 변수를 사용 합니다.

- **HttpControllerSettings** 개체
- **HttpControllerDescriptor** 개체

합니다 **HttpControllerDescriptor** 확인용으로 (즉, 두 명의 컨트롤러를 구분 하기 위해) 검사할 수 있는 컨트롤러에 대 한 설명을 포함 합니다.

사용 된 **HttpControllerSettings** 컨트롤러를 구성 하는 개체입니다. 이 개체는 구성 매개 변수-컨트롤러 별로 재정의할 수 있는 하위 집합을 포함 합니다. 변경 되지 않는 설정을 기본적으로 전역 **HttpConfiguration** 개체입니다.
