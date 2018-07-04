---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
title: ASP.NET Web API 2에 대 한 보안 지침 OData | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/06/2013
ms.topic: article
ms.assetid: b91e6424-1544-4747-bd0b-d1f8418c9653
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
msc.type: authoredcontent
ms.openlocfilehash: 72aee37e715fa11ccfe5d02eef4e450dd747095a
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37378033"
---
<a name="security-guidance-for-aspnet-web-api-2-odata"></a>ASP.NET Web API 2에 대 한 보안 지침 OData
====================
[Mike Wasson](https://github.com/MikeWasson)

이 항목에서는 OData 통해 데이터 집합을 노출 하는 경우 고려해 야 하는 보안 문제 중 일부를 설명 합니다.

## <a name="edm-security"></a>EDM 보안

쿼리 의미 체계 엔터티 데이터 모델 (EDM)에서 기본 모델 형식 기반으로 합니다. EDM에서 속성을 제외할 수 있습니다 및 쿼리에 표시 되지 않습니다. 예를 들어 모델에는 급여 속성을 포함 하는 직원 형식 포함 되어 있습니다. 클라이언트에서 숨기려면 EDM에서이 속성을 제외 수 있습니다.

두 가지는 제외를 EDM 속성입니다. 설정할 수 있습니다 합니다 **[IgnoreDataMember]** 모델 클래스의 속성을 특성:

[!code-csharp[Main](odata-security-guidance/samples/sample1.cs)]

프로그래밍 방식으로 EDM에서 속성을 제거할 수도 있습니다.

[!code-csharp[Main](odata-security-guidance/samples/sample2.cs)]

## <a name="query-security"></a>쿼리 보안

악성 또는 네이티브 클라이언트를 실행 하는 매우 긴 시간이 소요 되는 쿼리를 만들 수 있습니다. 최악의 경우에서이 서비스에 대 한 액세스를 방해할 수 있습니다.

합니다 **[Queryable]** 가 구문 분석, 유효성을 검사, 쿼리를 적용 하는 작업 필터 특성입니다. 필터는 LINQ 식에 쿼리 옵션을 변환합니다. OData 컨트롤러를 반환 하는 경우는 **IQueryable** 형식에는 **IQueryable** LINQ 공급자는 LINQ 식 쿼리로 변환 합니다. 따라서 성능에 사용 되는 LINQ 공급자 및 데이터 집합 또는 데이터베이스 스키마의 특정 특성에 따라 다릅니다.

ASP.NET Web API에서 OData 쿼리 옵션을 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [OData 쿼리 옵션 지원](supporting-odata-query-options.md)합니다.

않을 (예를 들어, 엔터프라이즈 환경)에서 모든 클라이언트는 신뢰할 수 있는지 알고 있는 경우 또는 데이터 집합이 작은 경우 쿼리 성능 문제를 하지 수 있습니다. 그렇지 않은 경우 다음 권장 사항을 고려해 야 합니다.

- 다양 한 쿼리를 사용 하 여 서비스를 테스트 하 고 DB를 프로 파일링 합니다.
- 한 쿼리에서 큰 데이터 집합을 반환 하지 않으려면 서버 기반 페이징이 사용 하도록 설정 합니다. 자세한 내용은 [Server-Driven 페이징](supporting-odata-query-options.md#server-paging)합니다. 

    [!code-csharp[Main](odata-security-guidance/samples/sample3.cs)]
- $Filter 및 $orderby 필요 한가요? 일부 응용 프로그램 페이징 $top $skip을 사용 하 여, 클라이언트 허용 되었지만 다른 쿼리 옵션을 사용 하지 않도록 설정 됩니다. 

    [!code-csharp[Main](odata-security-guidance/samples/sample4.cs)]
- 클러스터형된 인덱스의 속성에 $orderby를 제한 하는 것이 좋습니다. 클러스터형된 인덱스가 없는 큰 데이터를 정렬 하는 속도가 느립니다. 

    [!code-csharp[Main](odata-security-guidance/samples/sample5.cs)]
- 최대 노드 수: 합니다 **MaxNodeCount** 속성을 **[Queryable]** $filter 구문 트리에서 허용 된 최대 노드를 설정 합니다. 기본값은 100으로 하지만 많은 수의 노드는 컴파일 느린 수 있기 때문에 더 낮은 값을 설정 하려면 가리키려는 합니다. LINQ to Objects (즉, 중간 LINQ 공급자를 사용 하지 않고 메모리에서 컬렉션에 대 한 LINQ 쿼리)를 사용 하는 경우 특히 그렇습니다. 

    [!code-csharp[Main](odata-security-guidance/samples/sample6.cs)]
- 속도가 느려질 수 있습니다 이러한 any () 및 all ()과 함수를 사용 하지 않도록 설정 살펴봅니다. 

    [!code-csharp[Main](odata-security-guidance/samples/sample7.cs)]
- 큰 문자열 및 #8212for 예제, 제품 설명 또는 블로그 항목 및 문자열 함수를 사용 하지 않도록 설정 하는 #8212consider 모든 문자열 속성에 포함 되어 있습니다. 

    [!code-csharp[Main](odata-security-guidance/samples/sample8.cs)]
- 탐색 속성에 대해 필터링을 허용 하지 않는 것이 좋습니다. 데이터베이스 스키마에 따라 저하 될 수 있는 조인에서는 탐색 속성에 대해 필터링 될 수 있습니다. 다음 코드에서는 탐색 속성에 대해 필터링을 방지 하는 쿼리 검사기를 보여 줍니다. 쿼리 유효성 검사기에 대 한 자세한 내용은 참조 하세요. [쿼리 유효성 검사](supporting-odata-query-options.md#query-validation)합니다. 

    [!code-csharp[Main](odata-security-guidance/samples/sample9.cs)]
- 데이터베이스에 대 한 사용자 지정 된 유효성 검사기를 작성 하 여 $filter 쿼리를 제한 하는 것이 좋습니다. 예를 들어,이 두 가지 쿼리를 고려 합니다. 

  - 마지막으로 이름이 'A'로 시작 하는 행위자를 사용 하 여 모든 동영상입니다.
  - 1994 년에 릴리스된 모든 동영상입니다.

    행위자가 영화는 인덱싱되지 않는 한 첫 번째 쿼리는 동영상의 전체 목록을 검색 하려면 DB 엔진이 필요할 수 있습니다. 두 번째 쿼리는 허용 될 수 있습니다, 있지만 릴리스 연도별 되었다고 가정 하 고 영화가 인덱싱됩니다.

    다음 코드에 있지만 "ReleaseYear" 및 "Title" 속성을 필터링 할 수 있습니다 하는 유효성 검사기를 보여 줍니다.

    [!code-csharp[Main](odata-security-guidance/samples/sample10.cs)]
- 일반적으로 필요한 $filter 함수를 것이 좋습니다. 클라이언트의 $filter의 전체 표현이 필요 하지 않은 경우에 허용 된 함수를 제한할 수 있습니다.
