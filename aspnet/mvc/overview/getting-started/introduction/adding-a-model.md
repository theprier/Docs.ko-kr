---
uid: mvc/overview/getting-started/introduction/adding-a-model
title: 모델 추가 | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/28/2015
ms.topic: article
ms.assetid: 276552b5-f349-4fcf-8f40-6d042f7aa88e
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: 98b6693b07e4da318a649494649d9da83fe8a7d3
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37365138"
---
<a name="adding-a-model"></a>모델 추가
====================
[Rick Anderson](https://github.com/Rick-Anderson)

[!INCLUDE [Tutorial Note](sample/code-location.md)]

이 섹션에서는 데이터베이스에서 동영상을 관리 하기 위한 일부 클래스를 추가 합니다. 이러한 클래스는 &quot;모델&quot; ASP.NET MVC 앱의 일부입니다.

라고 하는.NET Framework 데이터 액세스 기술 사용 합니다 [Entity Framework](https://docs.microsoft.com/ef/) 를 정의한 다음 이러한 모델 클래스를 사용 합니다. 라고 하는 개발 패러다임을 Entity Framework (EF 라고도 함) 지원 *Code First*합니다. 먼저 코드를 사용 하면 간단한 클래스를 작성 하 여 모델 개체를 만들 수 있습니다. (이러한 이라고 POCO 클래스에서 &quot;plain old CLR object.&quot;) 그런 다음이 매우 명확 하 고 신속한 개발 워크플로 통해 클래스를에서 즉석에서 생성 된 데이터베이스를 사용할 수 있습니다. 먼저 데이터베이스를 만드는 데 필요한 인 경우에 EF 및 MVC 앱 개발에 대해 자세히 알아보려면이 자습서를 따라 계속 합니다. Tom Fizmakens 수행 수 있습니다 [ASP.NET 스 캐 폴딩](xref:visual-studio/overview/2013/aspnet-scaffolding-overview) 첫 번째 방법은 데이터베이스를 다루는 자습서입니다.

## <a name="adding-model-classes"></a>모델 클래스 추가

**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 *모델* 폴더를 선택 **추가**를 선택한 후 **클래스**합니다.

![](adding-a-model/_static/image1.png)

입력 된 *클래스* 이름 &quot;영화&quot;합니다.

다음 5 개의 속성을 추가 합니다 `Movie` 클래스:

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

사용 된 `Movie` 데이터베이스에서 동영상을 나타내는 클래스입니다. 각 인스턴스는 `Movie` 개체의 각 속성과 데이터베이스 테이블 내의 행에 해당 합니다 `Movie` 클래스는 테이블의 열에 매핑됩니다.

참고: System.Data.Entity, 및 관련된 클래스를 사용 하기 위해 설치 해야 합니다 [Entity Framework NuGet 패키지](https://www.nuget.org/packages/EntityFramework/)합니다. 추가 지침에 대 한 링크를 따릅니다.

동일한 파일에 다음 추가 `MovieDBContext` 클래스:

[!code-csharp[Main](adding-a-model/samples/sample2.cs?highlight=2,15-18)]

`MovieDBContext` 페치, 저장 및 업데이트를 처리 하는 Entity Framework 영화 데이터베이스 컨텍스트 클래스를 나타냅니다 `Movie` 클래스 인스턴스의 데이터베이스에 있습니다. 합니다 `MovieDBContext` 에서 파생 되는 `DbContext` 기본 Entity Framework에서 제공 하는 클래스입니다.

참조할 수 있도록 `DbContext` 하 고 `DbSet`, 다음을 추가 해야 `using` 파일의 맨 위에 있는 문을:

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

사용 하 여 수동으로 추가 하 여 이렇게 문 또는 있습니다 수 빨간색의 구불구불한 선을 마우스로 클릭 `Show potential fixes` 클릭 `using System.Data.Entity;`

![](adding-a-model/_static/image2.png)

참고: 여러 사용 되지 않는 `using` 문이 제거 되었습니다. Visual Studio는 사용 되지 않는 종속성 회색으로 표시 됩니다. 회색 종속성 마우스로 사용 되지 않는 종속성을 제거를 클릭 합니다 `Show potential fixes` 를 클릭 하 고 **사용 하지 않는 Using 제거 합니다.**

![](adding-a-model/_static/image3.png)

마지막으로 모델 (MVC에서 M)을 추가 했습니다. 다음 섹션에서 데이터베이스 연결 문자열을 작업할 수 있습니다.

> [!div class="step-by-step"]
> [이전](adding-a-view.md)
> [다음](creating-a-connection-string.md)
