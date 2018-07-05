---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/calling-an-odata-service-from-a-net-client
title: .NET 클라이언트 (C#)에서 OData 서비스를 호출 합니다. | Microsoft Docs
author: MikeWasson
description: 이 자습서에서는 C# 클라이언트 응용 프로그램에서 OData 서비스를 호출 하는 방법을 보여 줍니다. 자습서 Visual Studio 2013 (호환 Visual S....에 사용 되는 소프트웨어 버전
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/26/2014
ms.topic: article
ms.assetid: 6f448917-ad23-4dcc-9789-897fad74051b
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/calling-an-odata-service-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: d987e7fbe737055b3e2b690ef3e8de5ca7e2b937
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37369785"
---
<a name="calling-an-odata-service-from-a-net-client-c"></a>.NET 클라이언트 (C#)에서 OData 서비스를 호출합니다.
====================
[Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트 다운로드](http://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> 이 자습서에서는 C# 클라이언트 응용 프로그램에서 OData 서비스를 호출 하는 방법을 보여 줍니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
> 
> 
> - [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads) (Visual Studio 2012를 사용 하 여 작동)
> - [WCF Data Services 클라이언트 라이브러리](https://msdn.microsoft.com/library/cc668772.aspx)
> - Web API 2입니다. (예제에서는 OData 서비스 Web API 2를 사용 하 여 빌드됩니다. 하지만 클라이언트 응용 프로그램이 웹 API에 종속 되지 않습니다.)


이 자습서에서는 OData 서비스를 호출 하는 클라이언트 응용 프로그램을 작성 하는 방법을 살펴보겠습니다. OData 서비스는 다음 엔터티를 노출합니다.

- `Product`
- `Supplier`
- `ProductRating`

![](calling-an-odata-service-from-a-net-client/_static/image1.png)

다음 문서를 웹 API에서 OData 서비스를 구현 하는 방법에 설명 합니다. (필요가 있지만이 자습서에서는 이해 하기 읽을 수 있습니다.)

- [Web API 2에서에서 OData 끝점 만들기](creating-an-odata-endpoint.md)
- [Web API 2 OData 엔터티 관계](working-with-entity-relations.md)
- [Web API 2의 OData 작업](odata-actions.md)

## <a name="generate-the-service-proxy"></a>서비스 프록시를 생성 합니다.

첫 번째 단계는 서비스 프록시를 생성 하는 것입니다. 서비스 프록시는 OData 서비스에 액세스 하기 위한 메서드를 정의 하는.NET 클래스입니다. 프록시는 HTTP 요청에 대 한 메서드 호출으로 변환합니다.

![](calling-an-odata-service-from-a-net-client/_static/image2.png)

Visual Studio에서 OData 서비스 프로젝트를 열어 시작 합니다. IIS Express에서 로컬로 서비스를 실행 하려면 CTRL + F5 키를 누릅니다. Visual Studio 할당 하는 포트 번호를 포함 하 여 로컬 주소를 note 합니다. 프록시를 만들 때이 주소가 필요 합니다.

다음으로, Visual Studio의 다른 인스턴스를 열고 콘솔 응용 프로그램 프로젝트를 만듭니다. 콘솔 응용 프로그램에는 OData 클라이언트 응용 프로그램이 됩니다. (추가할 수 있습니다도 프로젝트 서비스와 동일한 솔루션에.)

> [!NOTE]
> 나머지 단계를 콘솔 프로젝트를 참조 하세요.


솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 **참조가** 선택한 **서비스 참조 추가**합니다.

![](calling-an-odata-service-from-a-net-client/_static/image3.png)

에 **서비스 참조 추가** 대화 상자에서 OData 서비스의 주소를 입력 합니다.

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample1.cmd)]

여기서 *포트* 포트 번호입니다.

[![](calling-an-odata-service-from-a-net-client/_static/image5.png)](calling-an-odata-service-from-a-net-client/_static/image4.png)

에 대 한 **Namespace**, "ProductService"를 입력 합니다. 이 옵션은 프록시 클래스의 네임 스페이스를 정의 합니다.

**찾기**를 클릭합니다. Visual Studio에는 서비스에서 엔터티를 검색할 OData 메타 데이터 문서를 읽습니다.

[![](calling-an-odata-service-from-a-net-client/_static/image7.png)](calling-an-odata-service-from-a-net-client/_static/image6.png)

클릭 **확인** 프로젝트에 프록시 클래스를 추가 합니다.

![](calling-an-odata-service-from-a-net-client/_static/image8.png)

## <a name="create-an-instance-of-the-service-proxy-class"></a>서비스 프록시 클래스의 인스턴스를 만듭니다

내부 프로그램 `Main` 메서드를 다음과 같이 프록시 클래스의 새 인스턴스를 만듭니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample2.cs)]

를 사용 하 여 실제 포트 번호를 서비스가 실행 되는 위치입니다. 서비스를 배포 하는 경우에 라이브 서비스의 URI를 사용 합니다. 프록시를 업데이트할 필요가 없습니다.

다음 코드는 콘솔 창에는 요청 Uri를 출력 하는 이벤트 처리기를 추가 합니다. 이 단계 필요 없지만 각 쿼리에 대 한 Uri를 확인 하려면 흥미롭습니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample3.cs)]

## <a name="query-the-service"></a>서비스를 쿼리 합니다.

다음 코드는 OData 서비스에서 제품 목록을 가져옵니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample4.cs)]

HTTP 요청을 보내거나 응답을 구문 분석을 위해 어떠한 코드도 작성할 필요가 있는지 확인 합니다. 프록시 클래스는 자동으로 열거 하는 `Container.Products` 컬렉션에는 **foreach** 루프입니다.

응용 프로그램을 실행 하는 경우 출력은 다음과 같아야 합니다.

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample5.cmd)]

ID에 따라 엔터티를 가져오려면는 `where` 절.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample6.cs)]

이 항목의 나머지 부분에 대 한 전체 소개 하지 `Main` 서비스를 호출 하는 데 필요한 코드에만 작동 합니다.

## <a name="apply-query-options"></a>쿼리 옵션을 적용

OData는 정의 [쿼리 옵션](../supporting-odata-query-options.md) 필터, 정렬, 페이지 데이터 등을 사용할 수 있습니다. 서비스 프록시에 다양 한 LINQ 식을 사용 하 여 이러한 옵션을 적용할 수 있습니다.

이 섹션에서는 간단한 예를 살펴보겠습니다. 자세한 내용은 항목을 참조 하세요 [LINQ 고려 사항 (WCF Data Services)](https://msdn.microsoft.com/library/ee622463.aspx) MSDN에 있습니다.

### <a name="filtering-filter"></a>필터링 ($filter)

필터링에 사용 된 `where` 절. 제품 범주에 따라 다음 예제에서는 필터입니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample7.cs)]

이 코드는 다음 OData 쿼리에 해당합니다.

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample8.cmd)]

프록시를 변환 하는 `where` OData 절 `$filter` 식입니다.

### <a name="sorting-orderby"></a>정렬 ($orderby)

정렬에 사용 하 여는 `orderby` 절. 다음 예제에서는 가격 최상위에서 최하위 순으로 정렬합니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample9.cs)]

해당 OData 요청은 다음과 같습니다.

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample10.cmd)]

### <a name="client-side-paging-skip-and-top"></a>클라이언트 쪽 페이징 ($skip 및 $top)

큰 엔터티 집합에 대 한 클라이언트 결과의 수를 제한 해야 할 수도 있습니다. 예를 들어, 클라이언트는 한 번에 10 개 항목을 표시할 수 있습니다. 이 이라고 *클라이언트 쪽 페이징*합니다. (이기도 [서버측 페이징이](../supporting-odata-query-options.md#server-paging), 서버에서 결과의 수를 제한 하는 위치입니다.) 클라이언트 쪽 페이징을 수행 하려면 LINQ를 사용 **Skip** 하 고 **걸릴** 메서드. 다음 예제는 처음 40 결과 건너뛰고 10을 사용 합니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample11.cs)]

해당 OData 요청은 다음과 같습니다.

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample12.cmd)]

### <a name="select-select-and-expand-expand"></a>선택 ($select) 및 확장 ($expand)

관련된 엔터티를 포함 하려면 사용 된 `DataServiceQuery<t>.Expand` 메서드. 예를 들어 포함 된 `Supplier` 각각에 대해 `Product`:

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample13.cs)]

해당 OData 요청은 다음과 같습니다.

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample14.cmd)]

LINQ를 사용 하 여 응답의 형태를 변경 하려면 **선택** 절. 다음 예제에서는 다른 속성이 없는 각 제품의 이름을 가져옵니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample15.cs)]

해당 OData 요청은 다음과 같습니다.

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample16.cmd)]

Select 절 관련된 엔터티를 포함할 수 있습니다. 이 경우 호출 하지 마세요 **확장**; 프록시를 자동으로 포함 확장이 경우. 다음 예제에서는 각 제품의 공급 업체와 이름을 가져옵니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample17.cs)]

해당 OData 요청은 다음과 같습니다. 포함 하는 **$expand** 옵션입니다.

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample18.cmd)]

$Select 및 $에 대 한 자세한 정보에 대 한 확장 참조 하세요 [$expand $select 사용 및 Web API 2에서 $value](../using-select-expand-and-value.md)합니다.

## <a name="add-a-new-entity"></a>새 엔터티를 추가 합니다.

엔터티 집합에 새 엔터티를 추가할 호출 `AddToEntitySet`, 여기서 *EntitySet* 엔터티 집합의 이름입니다. 예를 들어 `AddToProducts` 새 `Product` 에 `Products` 엔터티 집합입니다. 프록시를 생성 하면 WCF Data Services를 자동으로 만듭니다 이러한 강력한 **AddTo** 메서드.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample19.cs)]

두 엔터티 간의 링크를 추가 하려면 사용 합니다 **AddLink** 하 고 **SetLink** 메서드. 다음 코드는 새 공급 업체 및 새 제품을 추가 하 고 간의 링크를 만듭니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample20.cs)]

사용 하 여 **AddLink** 경우 탐색 속성이 컬렉션입니다. 이 예제에서는 제품을 추가 하 고는 `Products` 공급자의 컬렉션입니다.

사용 하 여 **SetLink** 경우 탐색 속성은 단일 엔터티. 이 예제에서는 설정 된 것을 `Supplier` 제품에는 속성입니다.

## <a name="update--patch"></a>업데이트/패치

엔터티를 업데이트 하려면 호출을 **UpdateObject** 메서드.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample21.cs)]

호출 하는 경우 업데이트를 수행한 **SaveChanges**합니다. 기본적으로 WCF는 HTTP MERGE 요청을 보냅니다. **PatchOnUpdate** 옵션은 WCF는 HTTP PATCH를 대신 보낼에 지시 합니다.

> [!NOTE]
> 병합 및 패치는 이유? 원래 HTTP 1.1 사양 ([RCF 2616](http://tools.ietf.org/html/rfc2616)) "부분 업데이트" 의미 체계를 사용 하 여 모든 HTTP 메서드를 정의 하지 않았습니다. 부분 업데이트를 지원 하려면 OData 사양을 MERGE 메서드를 정의 합니다. 2010에서는 [RFC 5789](http://tools.ietf.org/html/rfc5789) 부분 업데이트에 대 한 PATCH 메서드를 정의 합니다. 이 기록의 일부를 읽을 수 있습니다 [블로그 게시물](https://blogs.msdn.com/b/astoriateam/archive/2008/05/20/merge-vs-replace-semantics-for-update-operations.aspx) WCF Data Services 블로그에서입니다. 현재 패치 보다 선호 됩니다 병합 합니다. Web API 스 캐 폴딩을 통해 만든 OData 컨트롤러에는 두 방법 모두 지원 합니다.


전체 엔터티 (PUT 의미 체계가 아님)를 대체 하려는 경우 지정 된 **ReplaceOnUpdate** 옵션입니다. 이렇게 하면 WCF는 HTTP PUT 요청을 보내야 합니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample22.cs)]

## <a name="delete-an-entity"></a>엔터티 삭제

엔터티를 삭제 하려면 호출 **DeleteObject**합니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample23.cs)]

## <a name="invoke-an-odata-action"></a>OData 작업을 호출 합니다.

Odata에서 [작업](odata-actions.md) 엔터티에 대 한 CRUD 작업으로 쉽게 정의 되어 있지 않은 서버 쪽 동작을 추가 하는 방법입니다.

프록시 클래스는 작업을 설명 하는 OData 메타 데이터 문서, 하지만에 강력한 형식의 메서드 만들어지지 않습니다. 제네릭 사용 하 여 OData 작업을 실행할 수 있습니다 **Execute** 메서드. 그러나 매개 변수 및 반환 값의 데이터 형식을 알 해야 합니다.

예를 들어, 합니다 `RateProduct` "등급" 형식의 명명 된 매개 변수를 사용 하는 작업 `Int32` 반환을 `double`. 다음 코드에는이 작업을 호출 하는 방법을 보여 줍니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample24.cs)]

자세한 내용은[서비스 작업 호출 및 작업](https://msdn.microsoft.com/library/hh230677.aspx)합니다.

한 가지 옵션은 확장 합니다 **컨테이너** 작업을 호출 하는 강력한 형식의 메서드를 제공 하기 위해 클래스:

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample25.cs)]
