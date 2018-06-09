---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint
title: ASP.NET Web API 2.2 사용 하 여 OData v4 끝점을 만듭니다 | Microsoft Docs
author: MikeWasson
description: 개방형 데이터 프로토콜 (OData)는 웹에 대 한 데이터 액세스 프로토콜입니다. OData는 일관 된 방식으로 쿼리 및 조작 CRUD 작업을 통해 데이터 집합을 제공...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/24/2014
ms.topic: article
ms.assetid: 1e1927c0-ded1-4752-80fd-a146628d2f09
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint
msc.type: authoredcontent
ms.openlocfilehash: a3f94818f9674b0e1e9a45b2a6cc9455edc79726
ms.sourcegitcommit: 6784510cfb589308c3875ccb5113eb31031766b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2018
ms.locfileid: "26508052"
---
<a name="create-an-odata-v4-endpoint-using-aspnet-web-api-22"></a>ASP.NET Web API 2.2 사용 하 여 OData v4 끝점 만들기
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

> 개방형 데이터 프로토콜 (OData)는 웹에 대 한 데이터 액세스 프로토콜입니다. OData는 쿼리하고 CRUD 작업을 통해 데이터 집합을 조작 하는 일관 된 방식으로 제공 (만들기, 읽기, 업데이트 및 삭제) 합니다.
> 
> ASP.NET Web API v3 및 v4 프로토콜을 모두 지원합니다. 나란히 실행 하는 v4 끝점 될 수도 있습니다 v3 끝점을 사용 합니다.
> 
> 이 자습서에는 CRUD 작업을 지 원하는 OData v4 끝점을 만드는 방법을 보여 줍니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
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
> OData 버전 3에 대 한 참조 [OData v3 끝점을 만드는](../odata-v3/creating-an-odata-endpoint.md)합니다.


## <a name="create-the-visual-studio-project"></a>Visual Studio 프로젝트 만들기

Visual Studio에서에서 **파일** 메뉴 선택 **새로** &gt; **프로젝트**합니다.

확장 **설치 됨** &gt; **템플릿** &gt; **Visual C#** &gt; **웹**는 선택 **ASP.NET 웹 응용 프로그램** 템플릿. 프로젝트 이름을 &quot;ProductService&quot;합니다.

[![](create-an-odata-v4-endpoint/_static/image2.png)](create-an-odata-v4-endpoint/_static/image1.png)

에 **새 프로젝트** 대화 상자에서는 **빈** 서식 파일입니다. &quot;폴더 추가 및 핵심 참조 중... &quot;, 클릭 **웹 API**합니다. **확인**을 클릭합니다.

[![](create-an-odata-v4-endpoint/_static/image4.png)](create-an-odata-v4-endpoint/_static/image3.png)

## <a name="install-the-odata-packages"></a>OData 패키지 설치

**도구** 메뉴 선택 **NuGet 패키지 관리자** &gt; **패키지 관리자 콘솔**합니다. 패키지 관리자 콘솔 창에서 다음을 입력 합니다.

[!code-console[Main](create-an-odata-v4-endpoint/samples/sample1.cmd)]

이 명령은 최신 OData NuGet 패키지를 설치합니다.

## <a name="add-a-model-class"></a>모델 클래스를 추가 합니다.

A *모델* 는 응용 프로그램에서 데이터 엔터티를 나타내는 개체입니다.

솔루션 탐색기에서 모델 폴더를 마우스 오른쪽 단추로 클릭 합니다. 상황에 맞는 메뉴에서 선택 **추가** &gt; **클래스**합니다.

[![](create-an-odata-v4-endpoint/_static/image6.png)](create-an-odata-v4-endpoint/_static/image5.png)

> [!NOTE]
> 규칙에 따라 모델 폴더에 모델 클래스를 포함 하지만 실제 프로젝트에서이 규칙을 따르는 필요가 없습니다.


클래스 이름을 `Product`로 지정합니다. Product.cs 파일에서 코드를 다음으로 바꿉니다.

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample2.cs)]

`Id` 속성은 엔터티 키입니다. 클라이언트는 키로 엔터티를 쿼리할 수 있습니다. 예를 들어 ID 5 인 제품을 가져오려면 URI는 `/Products(5)`합니다. `Id` 속성 백 엔드 데이터베이스의 기본 키 됩니다.

## <a name="enable-entity-framework"></a>Entity Framework를 사용 하도록 설정

이 자습서에서는 Entity Framework (EF) Code First 백 엔드 데이터베이스를 만들려고 합니다.

> [!NOTE]
> Web API OData EF가 필요 하지 않습니다. 데이터베이스 엔터티 모델로 변환할 수 있는 모든 데이터 액세스 계층을 사용 합니다.


먼저, EF에 대 한 NuGet 패키지를 설치 합니다. **도구** 메뉴 선택 **NuGet 패키지 관리자** &gt; **패키지 관리자 콘솔**합니다. 패키지 관리자 콘솔 창에서 다음을 입력 합니다.

[!code-console[Main](create-an-odata-v4-endpoint/samples/sample3.cmd)]

내부 다음 섹션을 추가 하 고 Web.config 파일을 열고는 **구성** 요소 이후에 **configSections** 요소입니다.

[!code-xml[Main](create-an-odata-v4-endpoint/samples/sample4.xml?highlight=6)]

이 설정은 LocalDB 데이터베이스에 대 한 연결 문자열을 추가합니다. 이 데이터베이스는 응용 프로그램을 로컬로 실행할 때 사용 됩니다.

다음으로 라는 클래스를 추가 `ProductsContext` 모델 폴더에 있습니다.

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample5.cs)]

생성자에서 `"name=ProductsContext"` 연결 문자열의 이름을 지정 합니다.

## <a name="configure-the-odata-endpoint"></a>OData 끝점을 구성 합니다.

응용 프로그램 파일을 열고\_Start/WebApiConfig.cs 합니다. 다음 추가 **를 사용 하 여** 문:

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample6.cs)]

다음 코드를 다음 추가 **등록** 메서드:

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample7.cs)]

이 코드는 두 가지 작업을 수행합니다.

- 엔터티 데이터 모델 (EDM)를 만듭니다.
- 경로 추가 합니다.

EDM은 데이터의 추상 모델입니다. EDM은 서비스 메타 데이터 문서를 만드는 데 사용 됩니다. **ODataConventionModelBuilder** 클래스는 EDM 기본 명명 규칙을 사용 하 여 만듭니다. 이 방법을 사용 하려면 최소 코드가 필요 합니다. EDM 통해 더 많은 제어를 원하는 경우 사용할 수 있습니다는 **된** EDM 속성, 키 및 탐색 속성을 명시적으로 추가 하 여 만들 클래스입니다.

A *경로* Web API 끝점에 HTTP 요청을 라우팅하는 방법을 알려 줍니다. OData v4 경로 만들려면 호출는 **MapODataServiceRoute** 확장 메서드.

응용 프로그램에 여러 OData 끝점 각각에 대해 별도 경로 만듭니다. 에 고유 경로 이름 및 접두사 각 경로 지정 합니다.

## <a name="add-the-odata-controller"></a>OData 컨트롤러 추가

A *컨트롤러* 는 HTTP 요청을 처리 하는 클래스입니다. OData 서비스에서 설정 하는 각 엔터티에 대 한 별도 컨트롤러 만들기 이 자습서에서는 만듭니다 컨트롤러 하나에 대 한는 `Product` 엔터티.

솔루션 탐색기에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가** &gt; **클래스**합니다. 클래스 이름을 `ProductsController`로 지정합니다.

> [!NOTE]
> OData v3 사용에 대 한이 자습서의 버전은 **컨트롤러 추가** 스 캐 폴딩 합니다. 현재로 서는 OData v 4에 대 한 스 캐 폴딩이 없습니다.


ProductsController.cs에 상용구 코드를 다음으로 바꿉니다.

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample8.cs)]

컨트롤러 사용 하 여는 `ProductsContext` EF를 사용 하 여 데이터베이스에 액세스 하는 클래스입니다. 컨트롤러를 재정의 하는 통지는 **Dispose** 메서드를 삭제 하는 **ProductsContext**합니다.

컨트롤러에 대 한 시작 지점입니다. 다음으로, 모든 CRUD 작업에 대 한 메서드를 추가 합니다.

## <a name="querying-the-entity-set"></a>엔터티 집합 쿼리

다음 메서드를 추가 `ProductsController`합니다.

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample9.cs)]

매개 변수가 없는 버전의는 `Get` 메서드 전체 제품 컬렉션을 반환 합니다. `Get` 메서드는 *키* 매개 변수가 해당 키에 따라 제품을 찾습니다 (이 경우는 `Id` 속성).

**[EnableQuery]** 특성을 사용 하면 클라이언트가 $filter, $sort, 및 $page 등의 쿼리 옵션을 사용 하 여 쿼리를 수정할 수 있습니다. 자세한 내용은 참조 [OData 쿼리 옵션을 지 원하는](../supporting-odata-query-options.md)합니다.

## <a name="adding-an-entity-to-the-entity-set"></a>엔터티 집합에 엔터티 추가

데이터베이스에 새 제품을 추가 하는 클라이언트를 사용 하려면 다음 메서드를 추가 `ProductsController`합니다.

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample10.cs)]

## <a name="updating-an-entity"></a>엔터티 업데이트

OData는 엔터티, PATCH 및 PUT를 업데이트 하기 위한 두 개의 서로 다른 의미 체계를 지원 합니다.

- 패치 부분 업데이트를 수행합니다. 클라이언트에만 업데이트할 속성을 지정 합니다.
- PUT 전체 엔터티를 바꿉니다.

PUT의 단점은 클라이언트를 변경 하지 않는 값을 포함 하는 엔터티의 모든 속성에 대 한 값을 전송 해야 합니다. [OData 사양을](http://docs.oasis-open.org/odata/odata/v4.0/os/part1-protocol/odata-v4.0-os-part1-protocol.html#_Toc372793719) 패치 기본 설정 되어 있습니다.

어떤 경우 든, 다음은 PATCH 및 PUT 모두 메서드에 대 한 코드가입니다.

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample11.cs)]

컨트롤러 사용 PATCH의 경우는 **델타&lt;T&gt;**  변경 내용을 추적 하는 형식입니다.

## <a name="deleting-an-entity"></a>엔터티 삭제

데이터베이스에서 제품을 삭제 하는 클라이언트를 사용 하려면 다음 메서드를 추가 `ProductsController`합니다.

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample12.cs)]
