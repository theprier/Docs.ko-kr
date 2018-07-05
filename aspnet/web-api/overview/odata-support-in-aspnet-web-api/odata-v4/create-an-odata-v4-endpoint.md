---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint
title: ASP.NET Web API 2.2 사용 하 여 OData v4 엔드포인트 만들기 | Microsoft Docs
author: MikeWasson
description: Open Data Protocol (OData)는 웹에 대 한 데이터 액세스 프로토콜. OData 쿼리 및 CRUD 작업을 통해 데이터 집합을 조작할 일관 된 방식으로 제공 하는 중...
ms.author: aspnetcontent
ms.date: 06/24/2014
ms.assetid: 1e1927c0-ded1-4752-80fd-a146628d2f09
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint
msc.type: authoredcontent
ms.openlocfilehash: 04fad9b569972f11256c6b7288db34d4996ca8bf
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37804214"
---
<a name="create-an-odata-v4-endpoint-using-aspnet-web-api-22"></a>ASP.NET Web API 2.2 사용 하 여 OData v4 엔드포인트 만들기
====================
[Mike Wasson](https://github.com/MikeWasson)

> Open Data Protocol (OData)는 웹에 대 한 데이터 액세스 프로토콜. OData 쿼리 및 CRUD 작업을 통해 데이터 집합을 조작할 일관 된 방식으로 제공 (만들기, 읽기, 업데이트 및 삭제).
> 
> ASP.NET Web API v3 및 v4 프로토콜을 지원합니다. Side-by-side-를 실행 하는 v4 엔드포인트 수도 v3 엔드포인트를 사용 하 여 합니다.
> 
> 이 자습서에는 CRUD 작업을 지 원하는 OData v4 엔드포인트를 만드는 방법을 보여 줍니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
> 
> 
> - Web API 2.2
> - OData v4
> - [Visual Studio 2013 업데이트 2](https://www.visualstudio.com/downloads/download-visual-studio-vs)
> - Entity Framework 6
> - .NET 4.5
> 
> 
> ## <a name="tutorial-versions"></a>자습서 버전
> 
> OData 버전 3에 대 한 참조 [OData v3 엔드포인트 만들기](../odata-v3/creating-an-odata-endpoint.md)합니다.


## <a name="create-the-visual-studio-project"></a>Visual Studio 프로젝트 만들기

Visual Studio에서에서 합니다 **파일** 메뉴에서 **새로 만들기** &gt; **프로젝트**합니다.

확장 **설치 됨** &gt; **템플릿** &gt; **Visual C#** &gt; **웹**를 선택 합니다  **ASP.NET 웹 응용 프로그램** 템플릿. 프로젝트 이름을 &quot;ProductService&quot;합니다.

[![](create-an-odata-v4-endpoint/_static/image2.png)](create-an-odata-v4-endpoint/_static/image1.png)

에 **새 프로젝트** 대화 상자에서 선택 합니다 **빈** 템플릿. 아래 &quot;폴더를 추가 하 고 핵심 참조 하는 중... &quot;, 클릭 **Web API**합니다. **확인**을 클릭합니다.

[![](create-an-odata-v4-endpoint/_static/image4.png)](create-an-odata-v4-endpoint/_static/image3.png)

## <a name="install-the-odata-packages"></a>OData 패키지 설치

**도구** 메뉴에서 **NuGet 패키지 관리자** &gt; **패키지 관리자 콘솔**을 선택합니다. 패키지 관리자 콘솔 창에서 다음을 입력 합니다.

[!code-console[Main](create-an-odata-v4-endpoint/samples/sample1.cmd)]

이 명령은 최신 OData NuGet 패키지를 설치합니다.

## <a name="add-a-model-class"></a>모델 클래스 추가

A *모델* 는 응용 프로그램에서 데이터 엔터티를 나타내는 개체입니다.

솔루션 탐색기에서 Models 폴더를 마우스 오른쪽 단추로 클릭 합니다. 상황에 맞는 메뉴에서 선택 **추가** &gt; **클래스**합니다.

[![](create-an-odata-v4-endpoint/_static/image6.png)](create-an-odata-v4-endpoint/_static/image5.png)

> [!NOTE]
> 규칙에 따라 모델 클래스는 Models 폴더에 배치 됩니다 있지만 사용자 고유의 프로젝트에서이 규칙에 따라 필요가 없습니다.


클래스 이름을 `Product`로 지정합니다. Product.cs 파일에서 다음을 사용 하 여 상용구 코드를 바꿉니다.

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample2.cs)]

`Id` 속성이 엔터티 키입니다. 클라이언트는 키로 엔터티를 쿼리할 수 있습니다. 예를 들어, ID가 5 인 제품을 얻으려면 URI는 `/Products(5)`합니다. `Id` 속성 백 엔드 데이터베이스의 기본 키도 됩니다.

## <a name="enable-entity-framework"></a>Entity Framework를 사용 하도록 설정

이 자습서에서는 사용 하겠습니다 (EF) Entity Framework Code First 백 엔드 데이터베이스를 만듭니다.

> [!NOTE]
> Web API OData EF가 필요 하지 않습니다. 모델 데이터베이스 엔터티를 변환할 수 있는 모든 데이터 액세스 계층을 사용 합니다.


첫째, EF에 대 한 NuGet 패키지를 설치 합니다. **도구** 메뉴에서 **NuGet 패키지 관리자** &gt; **패키지 관리자 콘솔**을 선택합니다. 패키지 관리자 콘솔 창에서 다음을 입력 합니다.

[!code-console[Main](create-an-odata-v4-endpoint/samples/sample3.cmd)]

Web.config 파일을 열고 내에서 다음 섹션을 추가 합니다 **구성** 요소 후 합니다 **configSections** 요소.

[!code-xml[Main](create-an-odata-v4-endpoint/samples/sample4.xml?highlight=6)]

이 설정은 LocalDB 데이터베이스에 대 한 연결 문자열을 추가합니다. 이 데이터베이스는 앱을 로컬로 실행할 때 사용 됩니다.

다음으로, 라는 클래스를 추가 `ProductsContext` 모델 폴더:

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample5.cs)]

생성자에서 `"name=ProductsContext"` 연결 문자열의 이름을 지정 합니다.

## <a name="configure-the-odata-endpoint"></a>OData 끝점 구성

앱 파일을 열고\_Start/WebApiConfig.cs 합니다. 다음을 추가 합니다 **를 사용 하 여** 문:

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample6.cs)]

다음 코드를 추가 합니다 **등록** 메서드:

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample7.cs)]

이 코드는 두 가지를 수행합니다.

- EDM (엔터티 데이터 모델)을 만듭니다.
- 경로 추가합니다.

EDM은 데이터의 추상적 모델입니다. EDM은 서비스 메타 데이터 문서를 만드는 데 사용 됩니다. 합니다 **ODataConventionModelBuilder** 클래스 기본 명명 규칙을 사용 하 여 EDM을 만듭니다. 이 방법은 최소한의 코드에 필요합니다. EDM 통해 더 많은 제어를 원하는 경우 사용할 수 있습니다 합니다 **된 ODataModelBuilder** 속성, 키 및 탐색 속성을 명시적으로 추가 하 여 EDM을 만들려면 클래스입니다.

A *경로* Web API 끝점에 HTTP 요청을 라우팅하는 방법을 알려 줍니다. OData v4 경로 만들려면 다음을 호출 합니다 **MapODataServiceRoute** 확장 메서드.

응용 프로그램의 OData 끝점을 여러 개 있으면 각각에 대해 별도 경로 만듭니다. 고유 경로 이름 및 접두사에는 각 경로 제공 합니다.

## <a name="add-the-odata-controller"></a>OData 컨트롤러 추가

A *컨트롤러* 는 HTTP 요청을 처리 하는 클래스입니다. OData 서비스에서 설정 하는 각 엔터티에 대해 별도 컨트롤러 만들기 이 자습서에서는 만들려는 하나의 컨트롤러에 대 한는 `Product` 엔터티.

솔루션 탐색기에서 컨트롤러 폴더를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가** &gt; **클래스**합니다. 클래스 이름을 `ProductsController`로 지정합니다.

> [!NOTE]
> OData v3 사용에 대 한이 자습서의 버전을 **컨트롤러 추가** 스 캐 폴딩 합니다. 현재는 OData v4에 대 한 스 캐 폴딩 되지 않습니다.


다음 ProductsController.cs의 상용구 코드를 대체 합니다.

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample8.cs)]

컨트롤러에서 사용 하 여 `ProductsContext` EF를 사용 하 여 데이터베이스에 액세스 하는 클래스입니다. 컨트롤러를 재정의 하는 **Dispose** 삭제 하는 방법을 **ProductsContext**합니다.

컨트롤러에 대 한 시작 지점입니다. 다음으로, 모든 CRUD 작업에 대 한 메서드를 추가 하겠습니다.

## <a name="querying-the-entity-set"></a>엔터티 집합 쿼리

다음 메서드를 추가 `ProductsController`합니다.

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample9.cs)]

매개 변수가 없는 버전은 `Get` 메서드 전체 제품 컬렉션을 반환 합니다. `Get` 메서드를 *키* 매개 변수는 키로 제품 조회 (이 경우는 `Id` 속성).

합니다 **[EnableQuery]** 특성 $filter와 $sort, $page 쿼리 옵션을 사용 하 여 쿼리를 수정 하는 클라이언트를 사용 하도록 설정 합니다. 자세한 내용은 [OData 쿼리 옵션 지원](../supporting-odata-query-options.md)합니다.

## <a name="adding-an-entity-to-the-entity-set"></a>엔터티 집합에 엔터티 추가

데이터베이스에 새 제품을 추가 하려면 클라이언트를 사용 하려면 다음 메서드를 추가 `ProductsController`합니다.

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample10.cs)]

## <a name="updating-an-entity"></a>엔터티 업데이트

OData는 엔터티, PATCH 및 PUT 업데이트를 위해 두 개의 서로 다른 의미 체계를 지원 합니다.

- 패치를 부분적으로 업데이트를 수행합니다. 클라이언트를 업데이트 하는 속성만 지정 합니다.
- PUT는 전체 엔터티를 대체 합니다.

PUT의 단점은 클라이언트 변경 하지 않는 하는 값을 포함 하 여 엔터티의 모든 속성의 값을 송신 해야 함을입니다. 합니다 [OData 사양을](http://docs.oasis-open.org/odata/odata/v4.0/os/part1-protocol/odata-v4.0-os-part1-protocol.html#_Toc372793719) 패치는 기본 상태입니다.

어떤 경우 든, PATCH 및 PUT 메서드에 대 한 코드가 같습니다.

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample11.cs)]

PATCH의 경우 컨트롤러를 사용 하는 **델타&lt;T&gt;**  변경 내용을 추적 하는 형식입니다.

## <a name="deleting-an-entity"></a>엔터티 삭제

데이터베이스에서 제품을 삭제 하도록 클라이언트를 사용 하려면 다음 메서드를 추가 `ProductsController`합니다.

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample12.cs)]
