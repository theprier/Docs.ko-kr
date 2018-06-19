---
uid: web-api/overview/releases/whats-new-in-aspnet-web-api-odata-53
title: ASP.NET Web API OData 5.3의에서 새로운 기능 | Microsoft Docs
author: microsoft
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/16/2014
ms.topic: article
ms.assetid: e39eaa25-83ff-41dc-869d-3818d59a88ae
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/releases/whats-new-in-aspnet-web-api-odata-53
msc.type: authoredcontent
ms.openlocfilehash: e918f86ebd813f31ad0c21566e617482fc7dd963
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
ms.locfileid: "26508112"
---
<a name="whats-new-in-aspnet-web-api-odata-53"></a>ASP.NET Web API OData 5.3의에서 새로운 기능
====================
여 [Microsoft](https://github.com/microsoft)

이 항목에서는 ASP.NET Web API OData 5.3에 대 한 새로운 기능을 설명 합니다.

- [다운로드](#download)
- [문서](#documentation)
- [OData 핵심 라이브러리](#corelib)
- [새로운 기능](#newf)
- [알려진된 문제 및 주요 변경 내용](#known-issues)
- [버그 수정](#bug-fixes)
- [ASP.NET Web API OData 5.3.1](#OD)

<a id="download"></a>
## <a name="download"></a>다운로드

런타임 기능은 NuGet 갤러리에서 NuGet 패키지로 해제 됩니다. 설치 하거나 NuGet 패키지 관리자 콘솔을 사용 하 여 출시 된 NuGet 패키지를 업데이트할 수 있습니다.

[!code-console[Main](whats-new-in-aspnet-web-api-odata-53/samples/sample1.cmd)]

<a id="documentation"></a>
## <a name="documentation"></a>설명서

자습서 및 ASP.NET Web API OData에 대 한 기타 문서를 찾을 수 있습니다는 [ASP.NET 웹 사이트](../odata-support-in-aspnet-web-api/index.md)합니다.

<a id="corelib"></a>
## <a name="odata-core-libraries"></a>OData 핵심 라이브러리

OData v 4에 대 한 Web API 이제 ODataLib 사용 하 여 6.5.0 버전

<a id="newf"></a>
## <a name="new-features-in-aspnet-web-api-odata-53"></a>새로운 기능에 ASP.NET Web API OData 5.3

### <a name="support-for-levels-in-expand"></a>$에서 $Levels에 대 한 지원 확장

$levels를 사용할 수 있습니다 쿼리 옵션 $에서 쿼리를 확장 합니다. 예:

[!code-console[Main](whats-new-in-aspnet-web-api-odata-53/samples/sample2.cmd)]

이 쿼리는 다음과 같습니다.

[!code-console[Main](whats-new-in-aspnet-web-api-odata-53/samples/sample3.cmd)]

<a id="open-entity-types"></a>
### <a name="support-for-open-entity-types"></a>열린 엔터티 형식에 대 한 지원

*형식을 열* 형식 정의에 선언 된 모든 속성과 함께 동적 속성을 포함 하는 stuctured 형식입니다. 개방형 형식이 데이터 모델에 유연성을 추가할 수 있습니다. 자세한 내용은 xxxx를 참조 하십시오.

### <a name="support-for-dynamic-collection-properties-in-open-types"></a>개방형 형식의 동적 컬렉션 속성에 대 한 지원

이전에 동적 속성 값을 단일 해야 했습니다. 5.3, 동적 속성 컬렉션 값을 가질 수 있습니다. 예를 들어 다음 JSON 페이로드가에 `Emails` 속성 동적 속성 이며 문자열 형식의 컬렉션입니다.

[!code-console[Main](whats-new-in-aspnet-web-api-odata-53/samples/sample4.cmd)]

### <a name="support-for-inheritance-for-complex-types"></a>복합 형식에 대 한 상속에 대 한 지원

이제 복합 형식은 기본 형식에서 상속할 수 있습니다. 예를 들어 OData 서비스는 다음 복합 유형을 정의할 수 있습니다.

[!code-csharp[Main](whats-new-in-aspnet-web-api-odata-53/samples/sample5.cs)]

이 예제에 대 한 EDM 다음과 같습니다.

[!code-xml[Main](whats-new-in-aspnet-web-api-odata-53/samples/sample6.xml?highlight=8,15)]

자세한 내용은 참조 [OData 복합 형식 상속 샘플](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt)합니다.

<a id="known-issues"></a>
## <a name="known-issues-and-breaking-changes"></a>알려진된 문제 및 주요 변경 내용

이 섹션에서는 알려진된 문제 및 ASP.NET Web API OData 5.3의 주요 변경 내용에 설명 합니다.

### <a name="odata-v4"></a>OData v4

#### <a name="query-options"></a>쿼리 옵션

문제: 중첩 된 $를 사용 하 여 확장 하 여 $levels 된 = 잘못 된 확장 깊이의 최대 결과입니다.

예를 들어 다음 요청을 가정합니다.

[!code-console[Main](whats-new-in-aspnet-web-api-odata-53/samples/sample7.cmd)]

경우 `MaxExpansionDepth` 가 5 이면 6 확장 깊이이 쿼리를 초래 합니다.

<a id="bug-fixes"></a>
## <a name="bug-fixes-and-minor-feature-updates"></a>버그 수정 및 사소한 기능 업데이트

이 릴리스에 여러 가지 버그 수정 및 사소한 기능에도 기능이 업데이트 합니다. 전체 목록은 여기를 찾을 수 있습니다.

- [버그 수정](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=v5.3%20Beta&assignedTo=All&component=Web%20API|Web%20API%20OData&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="OD"></a>
## <a name="aspnet-web-api-odata-531"></a>ASP.NET Web API OData 5.3.1

이 릴리스에서 변경 된 [버그 수정](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=v5.3.1%20Beta&amp;assignedTo=All&amp;component=Web%20API%20OData&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0&amp;reasonClosed=All) AllowedFunctions 열거형 중 일부에 대 한 합니다. 이 릴리스의 버그 수정 또는 새로운 기능 필요는 없습니다.
