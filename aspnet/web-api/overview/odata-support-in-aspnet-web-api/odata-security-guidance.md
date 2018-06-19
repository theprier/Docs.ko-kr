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
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
msc.type: authoredcontent
ms.openlocfilehash: 41b05f2a2f8247853d8358e6cc1246c8b438a6db
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30868710"
---
<a name="security-guidance-for-aspnet-web-api-2-odata"></a>ASP.NET Web API 2에 대 한 보안 지침 OData
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

이 항목에는 OData 통해 데이터 집합을 노출 하는 경우를 고려해 야 할 보안 문제 중 일부를 설명 합니다.

## <a name="edm-security"></a>EDM 보안

쿼리 의미 체계 엔터티 데이터 모델 (EDM) 기본 모델 유형 기반으로 합니다. EDM에서 속성을 제외할 수 있습니다 및 쿼리에 표시 되지 않습니다. 예를 들어 모델에는 급여 속성을 포함 하는 직원 형식 포함 되어 있다고 가정 합니다. 클라이언트에서 숨길 EDM에서이 속성을 제외 수 있습니다.

EDM에서 속성은 제외 하는 두 가지입니다. 설정할 수 있습니다는 **[IgnoreDataMember]** 모델 클래스의 속성을 특성:

[!code-csharp[Main](odata-security-guidance/samples/sample1.cs)]

프로그래밍 방식으로 EDM에서 속성을 제거할 수도 있습니다.

[!code-csharp[Main](odata-security-guidance/samples/sample2.cs)]

## <a name="query-security"></a>쿼리 보안

악의적 이거나 naïve 클라이언트를 실행 하는 데 시간이 오래 걸리는 쿼리를 생성할 수 있습니다. 최악의 경우에서이 서비스에 대 한 액세스 중단 될 수 있습니다.

**[Queryable]** 특성은 구문 분석 하 고 유효성을 검사, 쿼리를 적용 하는 작업 필터입니다. 필터 쿼리 옵션 LINQ 식으로 변환 합니다. OData 컨트롤러 반환 하는 경우는 **IQueryable** 종류는 **IQueryable** LINQ 공급자는 쿼리에 LINQ 식을 변환 합니다. 따라서 성능에 사용 되는 LINQ 공급자 뿐만 아니라 데이터 집합 또는 데이터베이스 스키마의 특정 특성에 따라 다릅니다.

ASP.NET Web API에서 OData 쿼리 옵션을 사용 하는 방법에 대 한 자세한 내용은 참조 [OData 쿼리 옵션을 지 원하는](supporting-odata-query-options.md)합니다.

모든 클라이언트 (예를 들어, 엔터프라이즈 환경)에서 신뢰할 수 있는지 알고 있거나 데이터 집합이 작으면 쿼리 성능이 문제가 아닐 수 있습니다. 그렇지 않은 경우 다음 권장 사항을 고려해 야 합니다.

- DB 프로 파일링 및 다양 한 쿼리를 사용 하 여 서비스를 테스트 합니다.
- 큰 데이터 집합을 한 쿼리에서 반환 되지 않도록 하려면 서버 기반 페이징 사용 하도록 설정 합니다. 자세한 내용은 참조 [Server-Driven 페이징](supporting-odata-query-options.md#server-paging)합니다. 

    [!code-csharp[Main](odata-security-guidance/samples/sample3.cs)]
- $Filter 및 $orderby 필요 한가요? 일부 응용 프로그램 클라이언트 페이징 $top $skip을 사용 하 여, 허용 수도 있지만 다른 쿼리 옵션을 사용 하지 않도록 설정 됩니다. 

    [!code-csharp[Main](odata-security-guidance/samples/sample4.cs)]
- 클러스터형된 인덱스의 속성에 대 한 $orderby를 제한 하는 것이 좋습니다. 클러스터형된 인덱스가 없는 큰 데이터를 정렬 하는 속도가 느립니다. 

    [!code-csharp[Main](odata-security-guidance/samples/sample5.cs)]
- 최대 노드 수:는 **maxnodecount에** 속성 **[Queryable]** $filter 구문 트리에 허용 되는 최대 숫자 노드를 설정 합니다. 기본값은 100, 하지만 많은 수의 노드가 컴파일 속도가 느려질 수 있으므로 더 낮은 값을 설정 하려면 좋습니다. LINQ to Objects (즉, 중간 LINQ 공급자를 사용 하지 않고 메모리에서 컬렉션에 대 한 LINQ 쿼리)를 사용 하는 경우 특히 그렇습니다. 

    [!code-csharp[Main](odata-security-guidance/samples/sample6.cs)]
- 느려질 수 있습니다는 any () 및 all() 함수를 사용 하지 않도록 설정 보십시오. 

    [!code-csharp[Main](odata-security-guidance/samples/sample7.cs)]
- 모든 문자열 속성에는 큰 문자열 & #8212for 예제, 제품 설명 또는 블로그 항목 & #8212consider 문자열 함수를 사용 하지 않도록 설정 포함 되어 있습니다. 

    [!code-csharp[Main](odata-security-guidance/samples/sample8.cs)]
- 탐색 속성으로 필터링을 허용 하는 것이 좋습니다. 탐색 속성에 대해 필터링 데이터베이스 스키마에 따라 속도가 느려질 수 있습니다 하는 조인을 발생할 수 있습니다. 다음 코드에서는 탐색 속성으로 필터링 하지 못하도록 하는 쿼리 검사기를 보여 줍니다. 쿼리 유효성 검사기에 대 한 자세한 내용은 참조 [쿼리 유효성 검사](supporting-odata-query-options.md#query-validation)합니다. 

    [!code-csharp[Main](odata-security-guidance/samples/sample9.cs)]
- 데이터베이스에 대 한 사용자 지정 된 유효성 검사기를 작성 하 여 $filter 쿼리를 제한 하는 것이 좋습니다. 예를 들어,이 두 쿼리를 것이 좋습니다. 

  - 'A'로 시작 하는 행위자와 모든 동영상 합니다.
  - 모든 동영상 1994에 배포 합니다.

    동영상은 행위자로 인덱싱하지 않을 경우 첫 번째 쿼리에서 동영상의 전체 목록을 검색 하려면 DB 엔진이 필요할 수 있습니다. 두 번째 쿼리에서 사용할 수도 있지만 되었다고 가정 하면 영화 릴리스 연도별 인덱싱됩니다.

    다음 코드에서는 "ReleaseYear" 및 "Title" 속성 하지만 다른 속성이 없는 필터링 하는 유효성 검사기를 보여 줍니다.

    [!code-csharp[Main](odata-security-guidance/samples/sample10.cs)]
- 일반적으로 원하는 $filter 함수를 것이 좋습니다. 클라이언트의 $filter의 전체 표현성 필요 하지 않은 경우에 허용 된 함수를 제한할 수 있습니다.
