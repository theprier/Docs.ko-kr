---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
title: '2 부: 데이터 액세스 계층 | Microsoft Docs'
author: JoeStagner
description: 이 자습서 시리즈 모든 Tailspin Spyworks 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 2 부에서는 데이터 액세스 계층을 추가 합니다.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 5a9d5429-d70b-411c-8474-f42cf7ef8a2b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
msc.type: authoredcontent
ms.openlocfilehash: 5b5ae08b157054bf0f3231782127ee3110f36d00
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41838214"
---
<a name="part-2-data-access-layer"></a>2 부: 데이터 액세스 계층
====================
[Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks.NET 플랫폼에 대 한 강력 하 고 확장 가능한 응용 프로그램을 생성 하는 방법을 매우 단순 하는 방법을 보여 줍니다. 해제 쇼핑, 체크 아웃 및 관리를 포함 하는 온라인 상점을 만들려고 ASP.NET 4에서 강력한 새 기능을 사용 하는 방법을 보여 줍니다.
> 
> 이 자습서 시리즈 모든 Tailspin Spyworks 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 2 부에서는 데이터 액세스 계층을 추가 합니다.


## <a id="_Toc260221668"></a>  데이터 액세스 계층 추가

전자 상거래 응용 프로그램은 두 개의 데이터베이스에 따라 달라 집니다.

고객 정보에 대 한 표준 ASP.NET 멤버 자격 데이터베이스를 사용 하겠습니다. 쇼핑 카트 및 제품 카탈로그에 대 한 SQL Express 데이터베이스를 다음과 같이 구현 됩니다 것입니다.

![](tailspin-spyworks-part-2/_static/image1.jpg)

응용 프로그램의 앱에서 (Commerce.mdf) 데이터베이스를 만들었으므로\_데이터 폴더.NET Entity Framework를 사용 하 여 데이터 액세스 계층 만들기를 진행할 수 있습니다.

라는 폴더를 만들겠습니다 "데이터\_액세스" 폴더를 마우스 오른쪽 단추로 클릭 하 고 "새 항목 추가"를 선택 합니다.

"설치 된 템플릿" 항목을 선택한 후 "ADO.NET Entity Data Model" 입력 EDM\_Commerce.edmx 이름으로 "추가" 단추를 클릭 합니다.

![](tailspin-spyworks-part-2/_static/image2.jpg)

"데이터베이스에서 생성"을 선택 합니다.

![](tailspin-spyworks-part-2/_static/image1.png)

![](tailspin-spyworks-part-2/_static/image2.png)

![](tailspin-spyworks-part-2/_static/image3.png)

![](tailspin-spyworks-part-2/_static/image3.jpg)

저장 하 고 빌드하십시오.

이제 첫 번째 – 특집 제품 범주 메뉴를 추가할 준비가 되었습니다.

> [!div class="step-by-step"]
> [이전](tailspin-spyworks-part-1.md)
> [다음](tailspin-spyworks-part-3.md)
