---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
title: ASP.NET Web API 사용 하 여 OData v4의 복합 형식 상속은 | Microsoft Docs
author: microsoft
description: OData v4 사양에 따라 복합 형식은 다른 복합 형식에서 상속할 수 있습니다. (복합 형식은 키가 없는 구조적된 형식을.) Web API는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/16/2014
ms.topic: article
ms.assetid: a00d3600-9c2a-41bc-9460-06cc527904e2
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 84a887b445959c4aa6d1ee372f067f93cd725d77
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37372059"
---
<a name="complex-type-inheritance-in-odata-v4-with-aspnet-web-api"></a>ASP.NET Web API 사용 하 여 OData v4의 복합 형식 상속
====================
[Microsoft](https://github.com/microsoft)

> OData v4에 따라 [사양](http://www.odata.org/documentation/odata-version-4-0/), 복합 형식은 다른 복합 형식에서 상속할 수 있습니다. (A *복잡 한* 형식은 키가 없는 구조적된 형식입니다.) Web API OData 5.3 복합 형식 상속은 지원합니다.
> 
> 이 항목에서는 복잡 한 상속 형식을 사용 하 여 엔터티 데이터 모델 (EDM)를 빌드하는 방법을 보여 줍니다. 전체 소스 코드를 보려면 [OData 복합 형식 상속 샘플](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt)합니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
> 
> 
> - Web API OData 5.3
> - OData v4


## <a name="model-hierarchy"></a>모델 계층 구조

복합 형식 상속은 보여 주기 위해 다음 클래스 계층 구조를 사용 하겠습니다.

![](complex-type-inheritance-in-odata-v4/_static/image1.png)

`Shape` 추상 복합 형식이입니다. `Rectangle`를 `Triangle`, 및 `Circle` 에서 파생 된 복합 형식 `Shape`, 및 `RoundRectangle` 에서 파생 `Rectangle`합니다. `Window` 엔터티 형식 및 포함 된 `Shape` 인스턴스.

이러한 형식을 정의 하는 CLR 클래스는 다음과 같습니다.

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample1.cs)]

## <a name="build-the-edm-model"></a>EDM 모델 빌드

EDM을 만들려면 사용할 수 있습니다 **ODataConventionModelBuilder**, CLR 형식에서 상속 관계를 유추 하 합니다.

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample2.cs)]

빌드할 수도 있습니다 EDM 명시적으로 사용 하 여 **된 ODataModelBuilder**합니다. 더 많은 코드를 걸리지만 EDM 통해 더 많은 제어를 제공 합니다.

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample3.cs)]

이러한 두 예제에서는 동일한 EDM 스키마를 만듭니다.

## <a name="metadata-document"></a>메타 데이터 문서

복합 형식 상속을 보여 주는 OData 메타 데이터 문서는 다음과 같습니다.

[!code-xml[Main](complex-type-inheritance-in-odata-v4/samples/sample4.xml?highlight=13,17,25,30)]

메타 데이터 문서에서 볼 수 있습니다.

- `Shape` 복합 형식이 추상 인지 합니다.
- 합니다 `Rectangle`, `Triangle`, 및 `Circle` 복합 형식의 기본 형식이 `Shape`합니다.
- 합니다 `RoundRectangle` 형식은 기본 형식 `Rectangle`합니다.

## <a name="casting-complex-types"></a>복합 형식 캐스팅

복합 형식에서 캐스팅 이제 지원 됩니다. 예를 들어 다음 쿼리 캐스트를 `Shape` 에 `Rectangle`합니다.

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample5.cmd)]

응답 페이로드는 다음과 같습니다.

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample6.cmd)]
