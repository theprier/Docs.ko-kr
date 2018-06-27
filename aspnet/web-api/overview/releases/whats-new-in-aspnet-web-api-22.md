---
uid: web-api/overview/releases/whats-new-in-aspnet-web-api-22
title: ASP.NET Web API 2.2의에서 새로운 기능 | Microsoft Docs
author: microsoft
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/25/2014
ms.topic: article
ms.assetid: 99c59ae4-167e-4f66-a6cd-d3f1098c4e4a
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/releases/whats-new-in-aspnet-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: 89b065fccd0e4864f4a24c37b4caa29a1e127840
ms.sourcegitcommit: 356c8d394aaf384c834e9c90cabab43bfe36e063
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2018
ms.locfileid: "36961301"
---
<a name="whats-new-in-aspnet-web-api-22"></a>ASP.NET Web API 2.2의에서 새로운 기능
====================
여 [Microsoft](https://github.com/microsoft)

이 항목에서는 ASP.NET 웹 API 2.2에 대 한 새로운 기능을 설명 합니다.

- [다운로드](#download)
- [문서](#documentation)
- [ASP.NET Web API 2.2의에서 새로운 기능](#newf)

    - [OData v4](#OData)
    - [라우팅 향상 된 기능 특성](#ARI)
    - [Windows Phone 8.1에 대 한 웹 API 클라이언트 지원](#phone)
- [알려진된 문제 및 주요 변경 내용](#known-issues)
- [버그 수정](#bug-fixes)
- [Microsoft.AspNet.OData 5.2.1](#odata521)
- [5.2.2 Microsoft.AspNet.WebAPI](#522RC)
- [5.2.3 Microsoft.AspNet.WebAPI 베타](#523)

<a id="download"></a>
## <a name="download"></a>다운로드

런타임 기능은 NuGet 갤러리에서 NuGet 패키지로 해제 됩니다. 모든 런타임 패키지에 따라는 [의미 체계 버전 관리](http://semver.org/) 사양입니다. 최신 ASP.NET 웹 API 2.2 패키지에는 다음 버전: "5.2.0"입니다. 설치 또는 업데이트를 통해 이러한 패키지 [NuGet](http://www.nuget.org/packages/Microsoft.AspNet.WebApi/)합니다. 릴리스에 NuGet에 해당 지역화 된 패키지도 포함 됩니다.

설치 하거나 NuGet 패키지 관리자 콘솔을 사용 하 여 출시 된 NuGet 패키지를 업데이트할 수 있습니다.

[!code-console[Main](whats-new-in-aspnet-web-api-22/samples/sample1.cmd)]

<a id="documentation"></a>
## <a name="documentation"></a>설명서

ASP.NET 웹 사이트에서 사용할 수 있는 자습서 및 ASP.NET 웹 API 2.2에 대 한 기타 정보 ([https://www.asp.net/web-api](../../index.md)).

<a id="newf"></a>
## <a name="new-features-in-aspnet-web-api-22"></a>ASP.NET Web API 2.2의에서 새로운 기능

<a id="OData"></a>
### <a name="odata-v4"></a>OData v4

이 릴리스에서 OData v4 프로토콜에 대 한 지원을 추가합니다. 자세한 내용은 참조는 [Web API OData v4 설명서입니다.](../odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint.md)

다음은 몇 가지 주요 기능 및 OData v 4에 대 한 변경입니다.

- [OData 모델의 별칭 속성에 대 한 지원](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataModelAliasingSample/)
- [ComplexTypeAttribute, AssociationAttribute, TimesTampAttribute 및 ConcurrencyCheckAttribute ODataConventionModelBuilder에에 대 한 지원](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataEtagSample/)
- [작업에 대 한 친숙 한 Title을 제공 하는 기능을 제공 합니다.](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataActionsSample/)
- ODL UriParser와 통합
- 에 대 한 지원 [enum](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataEnumTypeSample/ODataEnumTypeSample/), [제약](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataContainmentSample/) 및 [singleton](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataSingletonSample/)
- 기본 형식에 캐스팅 지원
- [OData 함수 지원 추가](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataFunctionSample/)
- [함수 호출에 대 한 매개 변수 별칭을 지원 합니다.](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataFunctionSample/)
- [모델에 카멜 케이스 명명 규칙을 지원 합니다.](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataCamelCaseSample/)
- 캐스팅할 $filter에에 대 한 지원
- 개방형 복합 형식에 대 한 지원
- 제거 EntitySetController 및 AsyncEntitySetController
- [변경 된 $link $ref](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataServiceSample/)
- [특성 라우팅 지원 추가](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataAttributeRoutingSample/)
- 6.4.0 OData 핵심 라이브러리를 사용 하 여

<a id="ARI"></a>
### <a name="attribute-routing-improvements"></a>라우팅 향상 된 기능 특성

특성 라우팅을 이제 호출 IDirectRouteProvider 특성 경로 검색 하 고 구성 하는 방식을 완전히 제어할 수 있는 확장성 지점을 제공 합니다. IDirectRouteProvider는 이러한 작업에 대 한 어떤 라우팅 구성이 가능 정확 하 게 지정 하려면 연결 된 경로 정보 함께 컨트롤러 및 작업의 목록을 제공 하는 일을 담당 합니다. IDirectRouteProvider 구현은 MapAttributes/MapHttpAttributeRoutes를 호출할 때 지정할 수 있습니다.

IDirectRouteProvider 사용자 지정의 기본 구현에서는 DefaultDirectRouteProvider를 확장 하 여 가장 쉬운 수 있습니다. 이 클래스는 특성 검색 경로 항목을 만들고 경로 접두사와 영역 접두사를 검색 하기 위한 논리를 변경 하는 별도 재정의 가능한 가상 메서드를 제공 합니다.

다음은이 새로운 확장 지점으로 수행할 수는 몇 가지 예제입니다.

1. 경로 특성 상속을 지원 합니다.

    예제:

    Like "/ 10/api/값" 요청은 "성공: 10"을 성공적으로 여기 반환

    [!code-csharp[Main](whats-new-in-aspnet-web-api-22/samples/sample2.cs)]
2. 원하는 몇 가지 규칙에 따라 특성 경로 대 한 기본 경로 이름을 제공 합니다. 기본적으로 특성 라우팅을 특성 경로 대 한 이름을 만들 자동으로 하지 않습니다.
3. 경로 테이블에 결국 전에 하나의 중앙 위치에 경로 템플릿을 특성 경로 수정 합니다.

<a id="phone"></a>
### <a name="web-api-client-support-for-windows-phone-81"></a>Windows Phone 8.1에 대 한 웹 API 클라이언트 지원

이제 Windows Phone 8.1을 대상으로 할 때 또는 웹 API 클라이언트 논리를 구현 하는 웹 API 클라이언트 NuGet 패키지를 사용할 수 있습니다는 유니버설 앱 내에서.

<a id="known-issues"></a>
## <a name="known-issues-and-breaking-changes"></a>알려진된 문제 및 주요 변경 내용

이 섹션에서는 알려진된 문제 및 ASP.NET 웹 API 2.2의 주요 변경 내용에 설명 합니다.

### <a name="odata-v4"></a>OData v4

#### <a name="model-builder"></a>모델 작성기

문제: 오버 로드 된 함수의 표시 되지 않았습니다 FunctionImport로

있는 경우 오버 로드 된 함수 2 고 FunctionImport System.InvalidOperationException ~/GetAllConventionCustomers(CustomerName={customerName}) 결과 요청 하는 다음 아래와 같이 수도 있습니다.

[!code-xml[Main](whats-new-in-aspnet-web-api-22/samples/sample3.xml)]

해결 방법:이 문제에 대 한 해결 FunctionImports로 모두 함수 오버 로드를 추가 하는 것입니다.

#### <a name="odata-routing"></a>OData 라우팅

URL을 포함 하는 문자열 리터럴을 슬래시 (%2F) 인코딩되고 backslash(%5C) OData 리소스 경로에 사용 될 때 404 오류를 발생 합니다.

예를 들어 함수의 매개 변수 또는 엔터티 집합의 키 값으로 OData 리소스 경로에 문자열 리터럴은 사용할 수 수 있습니다.

/Employees/Total.GetCount(Name='Name%2F')

/Employees('Name%5C')

서비스는 호스트는 이스케이프 해제 이러한 요청을 수신 하는 것에 웹 API 런타임에 전달 하기 전에 시퀀스 이스케이프 합니다. 이 다음과 같은 공격 으로부터 보호합니다.  
  
`http://www.contoso.com/..%2F..%2F/Windows/System32/cmd.exe?/c+dir+c:`

그러면 Web API OData 스택이 404 (찾을 수 없음) 오류를 반환 합니다. 이 오류를 방지 하려면 클라이언트에는 슬래시 (%252F)에 대 한 이중 이스케이프 시퀀스와 백슬래시 (%255 C)를 사용 해야 합니다. /Employees 같은 쿼리 문자열에 대 한이 문제가 발생 하지? $filter Name eq '이름 %2F' =

**언 이스케이프 된 슬래시 ('/')에 유의 하 고 백슬래시 (")는 OData 리소스 경로 문자열 리터럴에 사용할 수 없습니다. 슬래시 경로 구분 기호에만 표시 되어야 백슬래시 OData 리소스 경로에 전혀 표시 되지 않으며 (모두는 OData 쿼리 문자열의 특정 부분에서 사용할 수 있습니다.)**

해결 방법: DefaultODataPathHandler 실제로 구문 분석 하기 전에 슬래시 및 문자열 리터럴에 백슬래시를 이스케이프 하의 Parse 메서드를 재정의할 수 있습니다. 이 접근 방법의 예제를 찾을 수 있습니다.

### <a name="odata-v3"></a>OData v 3

#### <a name="queryable"></a>[쿼리 가능]

[Queryable] 특성을 사용 하는 사용 되지 않습니다. 새 OData v3 응용 프로그램 사용 해야 **System.Web.Http.OData.EnableQueryAttribute**합니다.

**ODataHttpConfigurationExtensions.EnableQuerySupport** 확장 메서드는 이제 추가 **EnableQueryAttribute** 를 전역 필터 컬렉션입니다. 모든 컨트롤러에 포함 하는 경우는 **[Queryable]** 특성, 호출 `config.EnableQuerySupport()` 하면는 **[Queryable]** 실패 하는 특성

이 문제를 해결 하는 권장된 방법의 모든 인스턴스는 **QueryableAttribute** 와 **System.Web.Http.OData.EnableQueryAttribute**합니다.

다른 해결 Web API 구성에서 다음 코드를 사용 하는 것입니다.

[!code-csharp[Main](whats-new-in-aspnet-web-api-22/samples/sample4.cs)]

### <a name="attribute-routing"></a>특성 라우팅

문제: FromUri 특성으로 데코레이팅되 어는 복합 형식의 모델 바인딩 다르게 동작 특성 라우팅을 사용 하는 경우.

다음 링크 문제를 추적 하 고도 문제를 해결 하는 방법에 대 한 세부 정보를 포함 합니다.  
[http://aspnetwebstack.codeplex.com/workitem/1944](http://aspnetwebstack.codeplex.com/workitem/1944)

문제: 스 캐 폴딩 MVC/웹 API 5.2.0 사용 하 여 프로젝트에 패키지 결과 5.1.2에서 프로젝트에 이미 존재 하지 않는 것에 대 한 패키지

ASP.NET MVC 5.2에 대 한 NuGet 패키지를 업데이트 해도 ASP.NET 스 캐 폴딩 같은 Visual Studio 도구 또는 ASP.NET 웹 응용 프로그램 프로젝트 템플릿을 업데이트 되지 않습니다. 이전 버전의 ASP.NET 런타임 패키지 (예:: Update 2에서 5.1.2) 사용합니다. 결과적으로, ASP.NET 스 캐 폴딩은 이미 프로젝트에서 사용할 수 없는 경우에 필요한 패키지의 이전 버전 (예:: Update 2에서 5.1.2)으로 설치 됩니다. 그러나 Visual Studio 2013 RTM 또는 업데이트 1에서 ASP.NET 스 캐 폴딩을 프로젝트에서 최신 패키지를 덮어쓰지 않습니다. ASP.NET 웹 API 2.2 또는 ASP.NET MVC 5.2로 프로젝트의 패키지를 업데이트 한 후에 스 캐 폴딩을 사용 하는 경우에 버전의 웹 API 및 ASP.NET MVC 일치 하는지 확인 합니다.

<a id="bug-fixes"></a>
## <a name="bug-fixes-and-minor-feature-updates"></a>버그 수정 및 사소한 기능 업데이트

이 릴리스에 여러 가지 버그 수정 및 사소한 기능에도 기능이 업데이트 합니다. 전체 목록은 여기를 찾을 수 있습니다.

- [5.2 패키지](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=v5.2%20RC|v5.2%20RTM&assignedTo=All&component=Web%20API|Web%20API%20OData&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="odata521"></a>
## <a name="microsoftaspnetodata-521"></a>Microsoft.AspNet.OData 5.2.1

Microsoft.AspNet.OData 5.2.1 패키지 없는 버그 수정 하지만 NuGet 종속성 업데이트를 포함합니다. 이 업데이트를 더 이상 엄격한 종속성에 Microsoft.OData.Core 6.4.0, 있지만 하나 6.4.0 사이의 7.0.0까지 차단 버전으로 업그레이드할 수 없습니다.

<a id="522RC"></a>
## <a name="microsoftaspnetwebapi-522"></a>5.2.2 Microsoft.AspNet.WebAPI

이 릴리스에서 종속성에 대 한 변경 기능이 되었습니다 `Json.Net 6.0.4`합니다. 이 버전의 새로운 기능에 대 한 자세한 내용은 `Json.NET`, 참조 [Json.NET 6.0 릴리스 4-JSON 병합 종속성 주입](http://james.newtonking.com/archive/2014/08/04/json-net-6-0-release-4-json-merge-dependency-injection)합니다. 이 릴리스에서 웹 API의 새로운 기능 또는 버그 수정 되어 있지 않습니다. 이후에이 새 버전의 웹 API에 따라 달라 지도록 소유 म 다른 모든 종속 패키지를 업데이트 합니다.

<a id="523"></a>
## <a name="microsoftaspnetwebapi-523-beta"></a>5.2.3 Microsoft.AspNet.WebAPI 베타

릴리스에 대 한 읽을 수 [여기](https://blogs.msdn.com/b/webdev/archive/2014/12/17/asp-net-mvc-5-2-3-web-pages-5-2-3-and-web-api-5-2-3-beta-releases.aspx)합니다. 이 릴리스에 버그 수정만 포함 됩니다. 사용할 수 있습니다 [이 쿼리](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=Closed&amp;type=All&amp;priority=All&amp;release=v5.2.3%20Beta&amp;assignedTo=All&amp;component=Web%20API&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0&amp;reasonClosed=Fixed) 이 릴리스에서 수정 된 문제 목록을 볼 수 있습니다.
