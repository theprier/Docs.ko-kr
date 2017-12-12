---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/calling-an-odata-service-from-a-net-client
title: ".NET 클라이언트 (C#)에서 OData 서비스를 호출할 | Microsoft Docs"
author: MikeWasson
description: "이 자습서에서는 C# 클라이언트 응용 프로그램에서 OData 서비스를 호출 하는 방법을 보여 줍니다. (Visual S 인 works.. 자습서 Visual Studio 2013에서 사용 되는 소프트웨어 버전"
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/26/2014
ms.topic: article
ms.assetid: 6f448917-ad23-4dcc-9789-897fad74051b
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/calling-an-odata-service-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: f6266045ebf55fb7ae691bfb55e9c90cd4edcc96
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="calling-an-odata-service-from-a-net-client-c"></a>.NET 클라이언트 (C#)에서 OData 서비스를 호출합니다.
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트를 다운로드 합니다.](http://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> 이 자습서에서는 C# 클라이언트 응용 프로그램에서 OData 서비스를 호출 하는 방법을 보여 줍니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads) (Visual Studio 2012를 사용한 작동)
> - [WCF Data Services 클라이언트 라이브러리](https://msdn.microsoft.com/en-us/library/cc668772.aspx)
> - Web API 2입니다. (Web API 2를 사용 하 여 OData 서비스 예제 빌드될 있지만 클라이언트 응용 프로그램 웹 API에 의존 하지 않습니다.)


이 자습서에서는 OData 서비스를 호출 하는 클라이언트 응용 프로그램을 만드는 설명 합니다. OData 서비스는 다음과 같은 엔터티를 노출합니다.

- `Product`
- `Supplier`
- `ProductRating`

![](calling-an-odata-service-from-a-net-client/_static/image1.png)

다음 문서에는 Web API에서 OData 서비스를 구현 하는 방법을 설명 합니다. 하지만 (않아도이 자습서에서는 이해를 읽을 수 있습니다.)

- [Web API 2 OData 끝점 만들기](creating-an-odata-endpoint.md)
- [Web API 2 OData 엔터티 관계](working-with-entity-relations.md)
- [Web API 2 OData 작업](odata-actions.md)

## <a name="generate-the-service-proxy"></a>서비스 프록시를 생성 합니다.

서비스 프록시를 생성 하는 첫 번째 단계가입니다. 서비스 프록시는 OData 서비스에 액세스 하기 위한 메서드를 정의 하는.NET 클래스입니다. 프록시는 HTTP 요청에 대 한 메서드 호출으로 변환합니다.

![](calling-an-odata-service-from-a-net-client/_static/image2.png)

Visual Studio에서 OData 서비스 프로젝트를 열어 시작 합니다. IIS Express에서 로컬로 서비스를 실행 하려면 CTRL + f 5를 누릅니다. Visual Studio 할당 하는 포트 번호를 포함 하 여 로컬 주소를 note 합니다. 프록시를 만들 때이 주소가 필요 합니다.

다음으로 Visual Studio의 다른 인스턴스를 열고 콘솔 응용 프로그램 프로젝트를 만듭니다. 콘솔 응용 프로그램에는 OData 클라이언트 응용 프로그램이 됩니다. (또한 추가할 수 프로젝트는 서비스와 동일한 솔루션.)

> [!NOTE]
> 나머지 단계 콘솔 프로젝트를 참조 하십시오.


솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 **참조** 선택 **서비스 참조 추가**합니다.

![](calling-an-odata-service-from-a-net-client/_static/image3.png)

에 **서비스 참조 추가** 대화 상자에서 OData 서비스의 주소를 입력 합니다.

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample1.cmd)]

여기서 *포트* 포트 번호입니다.

[![](calling-an-odata-service-from-a-net-client/_static/image5.png)](calling-an-odata-service-from-a-net-client/_static/image4.png)

에 대 한 **Namespace**, "ProductService"를 입력 합니다. 이 옵션 프록시 클래스의 네임 스페이스를 정의합니다.

**찾기**를 클릭합니다. Visual Studio를 서비스에서 엔터티를 검색 하는 OData 메타 데이터 문서를 읽습니다.

[![](calling-an-odata-service-from-a-net-client/_static/image7.png)](calling-an-odata-service-from-a-net-client/_static/image6.png)

클릭 **확인** 프로젝트에 프록시 클래스를 추가 합니다.

![](calling-an-odata-service-from-a-net-client/_static/image8.png)

## <a name="create-an-instance-of-the-service-proxy-class"></a>서비스 프록시 클래스의 인스턴스를 만들으십시오

내부 프로그램 `Main` 메서드를 다음과 같이 프록시 클래스의 새 인스턴스를 만듭니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample2.cs)]

를 사용 하 여 실제 포트 번호 프로그램 서비스가 실행 되 고 있습니다. 서비스를 배포 하면 라이브 서비스의 URI를 사용 합니다. 프록시를 업데이트할 필요가 없습니다.

다음 코드는 요청 Uri를 콘솔 창에 출력 하는 이벤트 처리기를 추가 합니다. 이 단계 필요, 아니지만 각 쿼리에 대 한 Uri 참조를 보면 흥미롭습니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample3.cs)]

## <a name="query-the-service"></a>쿼리 서비스

다음 코드는 OData 서비스에서 제품의 목록을 가져옵니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample4.cs)]

확인할 HTTP 요청을 보내거나 응답을 구문 분석을 위해 코드를 작성할 필요가 없습니다. 프록시 클래스는 자동으로 열거 하는 `Container.Products` 컬렉션에는 **foreach** 루프입니다.

응용 프로그램을 실행 하면 다음과 같은 출력이 표시 됩니다.

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample5.cmd)]

ID에 따라 엔터티를 가져오려면는 `where` 절.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample6.cs)]

이 항목의 나머지 부분에 대 한 전체 소개 하지 `Main` 서비스를 호출 하는 데 필요한 코드만 작동 합니다.

## <a name="apply-query-options"></a>쿼리 옵션을 적용

OData 정의 [쿼리 옵션](../supporting-odata-query-options.md) 필터, 정렬, 페이지 데이터 등을 사용할 수 있는 합니다. 서비스 프록시를 다양 한 LINQ 식을 사용 하 여 이러한 옵션을 적용할 수 있습니다.

이 섹션에서는 간단한 예를 살펴보겠습니다. 자세한 내용은 항목을 참조 하십시오. [LINQ 고려 사항 (WCF Data Services)](https://msdn.microsoft.com/en-us/library/ee622463.aspx) msdn 합니다.

### <a name="filtering-filter"></a>필터링 ($filter)

필터링 하려면 사용을 `where` 절. 다음 예제 필터 제품 범주별으로 보여 줍니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample7.cs)]

이 코드는 다음 OData 쿼리에 해당합니다.

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample8.cmd)]

프록시 변환에 `where` OData 절 `$filter` 식입니다.

### <a name="sorting-orderby"></a>정렬 ($orderby)

를 정렬 하려면 사용 하 여 프로그램 `orderby` 절. 다음 예제에서는 가격별 내림차순으로 정렬합니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample9.cs)]

다음은 해당 OData 요청입니다.

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample10.cmd)]

### <a name="client-side-paging-skip-and-top"></a>클라이언트 쪽 페이징 ($skip 및 $top)

큰 엔터티 집합에 대 한 클라이언트는 결과의 수를 제한 해야 할 수도 있습니다. 예를 들어 클라이언트는 한 번에 10 개의 항목을 표시할 수 있습니다. 이 라고 *클라이언트 쪽 페이징*합니다. (또한 [서버 쪽 페이징](../supporting-odata-query-options.md#server-paging), 서버에서 결과의 수를 제한 하는 위치입니다.) LINQ를 사용 하 여 클라이언트 쪽 페이징을 수행 하려면 **Skip** 및 **걸릴** 메서드. 다음 예제에서는 처음 40 결과 건너뛰고 10을 사용 합니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample11.cs)]

다음은 해당 OData 요청이입니다.

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample12.cmd)]

### <a name="select-select-and-expand-expand"></a>Select ($select) 및 확장 ($expand)

사용 하 여 관련된 엔터티를 포함 하려면는 `DataServiceQuery<t>.Expand` 메서드. 예를 들어, 포함 하는 `Supplier` 각 `Product`:

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample13.cs)]

다음은 해당 OData 요청이입니다.

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample14.cmd)]

LINQ를 사용 하 여 응답의 셰이프를 변경 하려면 **선택** 절. 다음 예제에서는 다른 속성이 없는 각 제품의 이름만을 가져옵니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample15.cs)]

다음은 해당 OData 요청이입니다.

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample16.cmd)]

Select 절 관련된 엔터티를 포함할 수 있습니다. 이 경우 호출 하지 않으면 **확장**; 프록시를 자동으로 포함 확장이 경우. 다음 예제에서는 이름 및 각 제품의 공급 업체를 가져옵니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample17.cs)]

다음은 해당 OData 요청입니다. 여기에 포함 됩니다는 **$expand** 옵션입니다.

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample18.cmd)]

$Select 및 $에 대 한 자세한 내용은 확장 하 고, 참조 [$select을 사용 하 여 $expand, 및 Web API 2에 $value](../using-select-expand-and-value.md)합니다.

## <a name="add-a-new-entity"></a>새 엔터티 추가

엔터티 집합에 새 엔터티를 추가 하려면 `AddToEntitySet`여기서 *EntitySet* 엔터티 집합의 이름입니다. 예를 들어 `AddToProducts` 를 새로 추가 `Product` 에 `Products` 엔터티 집합입니다. 프록시를 생성 하면 WCF 데이터 서비스를 자동으로 만듭니다 이러한 강력한 형식의 **AddTo** 메서드.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample19.cs)]

두 엔터티 간의 링크를 추가 하려면 사용 된 **AddLink** 및 **SetLink** 메서드. 다음 코드 새 공급 업체를 추가 하는 새 제품을 한 다음 간의 링크를 만듭니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample20.cs)]

사용 하 여 **AddLink** 때 탐색 속성은 컬렉션입니다. 이 예제에서는 제품을 추가 하 고는 `Products` 는 공급 업체에 대 한 컬렉션입니다.

사용 하 여 **SetLink** 때 탐색 속성은 단일 엔터티입니다. 이 예제에서는 설정는 `Supplier` 제품에는 속성입니다.

## <a name="update--patch"></a>업데이트/패치

엔터티를 업데이트 하려면 호출는 **UpdateObject** 메서드.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample21.cs)]

호출 하면 업데이트가 수행 되 **SaveChanges**합니다. 기본적으로 WCF HTTP MERGE 요청을 보냅니다. **PatchOnUpdate** 옵션 대신 HTTP PATCH 보낼 WCF에 알립니다.

> [!NOTE]
> 병합 및 패치 이유? 원래 HTTP 1.1 사양 ([RCF 2616](http://tools.ietf.org/html/rfc2616)) "부분 업데이트" 의미 체계를 사용 하 여 HTTP 메서드를 정의 하지 않았습니다. 부분 업데이트를 지원 하기는 OData 사양 MERGE 메서드를 정의 합니다. 2010에서 [RFC 5789](http://tools.ietf.org/html/rfc5789) 부분 업데이트에 대 한 패치 메서드를 정의 합니다. 이 기록의 일부를 읽을 수 [블로그 게시물](https://blogs.msdn.com/b/astoriateam/archive/2008/05/20/merge-vs-replace-semantics-for-update-operations.aspx) WCF Data Services 블로그에서에 있습니다. 오늘날 패치 보다 선호 됩니다 병합 합니다. Web API 스 캐 폴딩으로 만들어진 OData 컨트롤러 두 방법 모두를 지원 합니다.


전체 엔터티 (PUT 의미 체계가 아님)를 대체 하려면 지정 된 **ReplaceOnUpdate** 옵션입니다. 이렇게 하면 WCF HTTP PUT 요청을 보냅니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample22.cs)]

## <a name="delete-an-entity"></a>엔터티 삭제

엔터티를 삭제 하려면 호출 **DeleteObject**합니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample23.cs)]

## <a name="invoke-an-odata-action"></a>OData 작업을 호출

Odata에서 [동작](odata-actions.md) 엔터티에 대 한 CRUD 작업으로 쉽게 정의 되어 있지 않은 서버 쪽 동작을 추가 하는 방법입니다.

프록시 클래스는 OData 메타 데이터 문서 작업을 설명 하지만 하는 강력한 형식의 메서드 만들어지지 않습니다. 제네릭을 사용 하 여 OData 작업을 실행할 수 있습니다 **Execute** 메서드. 그러나 매개 변수 및 반환 값의 데이터 형식을 알고 해야 합니다.

예를 들어는 `RateProduct` "등급" 형식의 명명 된 매개 변수를 사용 하는 작업 `Int32` 반환는 `double`합니다. 다음 코드에는이 작업을 호출 하는 방법을 보여 줍니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample24.cs)]

자세한 내용은 참조[서비스 작업 호출 및 작업](https://msdn.microsoft.com/en-us/library/hh230677.aspx)합니다.

확장 하는 한 가지 방법은 **컨테이너** 작업을 호출 하는 강력한 형식의 메서드를 제공 하기 위해 클래스:

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample25.cs)]
