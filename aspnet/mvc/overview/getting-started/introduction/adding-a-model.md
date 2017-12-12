---
uid: mvc/overview/getting-started/introduction/adding-a-model
title: "모델 추가 | Microsoft Docs"
author: Rick-Anderson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/28/2015
ms.topic: article
ms.assetid: 276552b5-f349-4fcf-8f40-6d042f7aa88e
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: 13aab58e86829a8d4accd1d304420dcb34ffa472
ms.sourcegitcommit: ec9371e2fbfcb8d62e7e7cae69e7752f3f205385
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/23/2017
---
<a name="adding-a-model"></a>모델 추가
====================
으로 [Rick Anderson](https://github.com/Rick-Anderson)

[!INCLUDE[Tutorial Note](sample/code-location.md)]

이 섹션에서는 데이터베이스에서 영화를 관리 하기 위한 몇 가지 클래스를 추가 합니다. 이러한 클래스 됩니다는 &quot;모델&quot; ASP.NET MVC 응용 프로그램의 일부입니다.

라고 하는.NET Framework 데이터 액세스 기술 사용의 [Entity Framework](https://docs.microsoft.com/ef/) 정의 하 고 이러한 모델 클래스를 사용 합니다. Entity Framework (EF 라고도 함)에서 지 원하는 개발 패러다임 호출 *Code First*합니다. 먼저 코드에서는 간단한 클래스를 작성 하 여 모델 개체를 만들 수 있습니다. (이러한 라 하 고 POCO 클래스에서 &quot;old CLR 개체입니다.&quot;) 다음 클래스에서는 매우 명확 하 고 신속 하 게 개발 워크플로 매핑함으로써 즉석에서 생성 된 데이터베이스를 사용할 수 있습니다. 데이터베이스를 만들려면 먼저 해야 할 경우에 EF 및 MVC 응용 프로그램 개발에 대 한 자세한 내용은이 자습서를 따를 수 있습니다. Tom Fizmakens 수행 수 있습니다 [ASP.NET 스 캐 폴딩](xref:visual-studio/overview/2013/aspnet-scaffolding-overview) 자습서 데이터베이스 첫 번째 접근 방식에 설명 합니다.

## <a name="adding-model-classes"></a>모델 클래스를 추가합니다.

**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 *모델* 폴더를 **추가**를 선택한 후 **클래스**합니다.

![](adding-a-model/_static/image1.png)

입력은 *클래스* 이름 &quot;영화&quot;합니다.

다음 5 개의 속성을 추가 `Movie` 클래스:

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

에서는 `Movie` 를 데이터베이스에서 영화를 나타내는 클래스입니다. 각 인스턴스는 `Movie` 개체는 데이터베이스 테이블과의 각 속성에 있는 행에 해당 하는 `Movie` 클래스는 테이블의 열에 매핑됩니다.

참고: System.Data.Entity, 및 관련된 클래스를 사용 하기 위해 설치 해야는 [Entity Framework NuGet 패키지](https://www.nuget.org/packages/EntityFramework/)합니다. 자세한 내용은 링크를 따라 이동 합니다.

같은 파일에 다음 추가 `MovieDBContext` 클래스:

[!code-csharp[Main](adding-a-model/samples/sample2.cs?highlight=2,15-18)]

`MovieDBContext` 클래스 인출 저장 하 고 업데이트를 처리 하는 Entity Framework 영화 데이터베이스 컨텍스트를 나타냅니다. `Movie` 클래스 인스턴스는 데이터베이스에 있습니다. `MovieDBContext` 에서 파생 되는 `DbContext` 기본 클래스는 Entity Framework에서 제공 합니다.

참조할 수 있도록 `DbContext` 및 `DbSet`, 다음 코드를 추가 해야 할 `using` 문을 파일의 맨:

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

수동으로 using를 추가 하 여 이렇게 하려면 문이 빨간색의 구불구불한 선 위로 마우스를 가져가고 수, 클릭 `Show potential fixes` 클릭`using System.Data.Entity;`

![](adding-a-model/_static/image2.png)

참고: 일부 사용 되지 않는 `using` 문이 제거 되었습니다. Visual Studio 회색으로 사용 하지 않는 종속성이 표시 됩니다. 회색 종속성 위로 이동 하 여 unnused 종속성을 제거, 클릭 수 `Show potential fixes` 클릭 **사용 하지 않는 Using 제거 합니다.**

![](adding-a-model/_static/image3.png)

마지막으로 모델 (MVC에서 M) 추가 했습니다. 다음 섹션에서 데이터베이스 연결 문자열이 작업할 수 있습니다.

>[!div class="step-by-step"]
[이전](adding-a-view.md)
[다음](creating-a-connection-string.md)
