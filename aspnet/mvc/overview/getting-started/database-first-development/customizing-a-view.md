---
uid: mvc/overview/getting-started/database-first-development/customizing-a-view
title: 'ASP.NET MVC를 사용 하 여 먼저 EF Database: 보기 사용자 지정 | Microsoft Docs'
author: tfitzmac
description: MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여, 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다. 이 자습서 seri...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/01/2014
ms.topic: article
ms.assetid: 269380ff-d7e1-4035-8ad1-fe1316a25f76
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/getting-started/database-first-development/customizing-a-view
msc.type: authoredcontent
ms.openlocfilehash: bfbcfd39dd1cf0abe89a00d2958ca010f0e5e109
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37376500"
---
<a name="ef-database-first-with-aspnet-mvc-customizing-a-view"></a>ASP.NET MVC를 사용 하 여 먼저 EF Database: 보기 사용자 지정
====================
[Tom FitzMacken](https://github.com/tfitzmac)

> MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여, 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다. 이 자습서 시리즈에서는 자동으로 표시, 편집, 만들기, 사용자를 사용 하는 코드를 생성 하 고 데이터베이스 테이블에 있는 데이터를 삭제 하는 방법을 보여 줍니다. 생성된 된 코드는 데이터베이스 테이블의 열에 해당합니다.
> 
> 시리즈의이 부분 프레젠테이션을 개선할에 자동으로 생성 된 보기를 변경에 중점을 둡니다.


## <a name="add-enrolled-courses-to-student-details"></a>등록 된 과정 학생 세부 정보 추가

생성된 된 코드는 응용 프로그램에 대 한 좋은 시작점을 제공 하지만 필요 하지 않습니다 모든 응용 프로그램에 필요한 기능입니다. 응용 프로그램의 특정 요구 사항에 맞게 코드를 사용자 지정할 수 있습니다. 현재 응용 프로그램 선택한 학생에 대 한 등록된 과정을 표시 하지 않습니다. 이 섹션에서는 추가 등록된 과정을 각 학생에 대 한 합니다 **세부 정보** 학생에 대 한 보기입니다.

열기 **Students/Details.cshtml**, 및 마지막 아래 &lt;/dl&gt; 탭, 닫히기 전까지 &lt;/div&gt; 태그에 다음 코드를 추가 합니다.

[!code-cshtml[Main](customizing-a-view/samples/sample1.cshtml)]

이 코드에서는 선택한 학생에 대해 Enrollment 테이블의 각 레코드에 대 한 행을 표시 하는 테이블을 만듭니다. 합니다 **표시** 메서드는 expression을 나타내는 개체 (modelItem)에 대 한 HTML을 렌더링 합니다. 표시 메서드를 사용 하면 단순히 코드에서 속성 값을 포함) (대신 값의 해당 형식 및 해당 형식에 대 한 서식 파일에 따라 올바르게 서식이 지정 되는지 확인 합니다. 이 예제에서는 각 식 루프의 현재 레코드에서 단일 속성을 반환 하 고 값 형식은 기본 텍스트로 렌더링 됩니다.

학생/인덱스 보기로 다시 이동 및 선택 **세부 정보** 학습자 중 하나에 대 한 합니다. 보기에 포함 된 등록된 과정을 볼 수 있습니다.

![학생 등록](customizing-a-view/_static/image1.png)

> [!div class="step-by-step"]
> [이전](changing-the-database.md)
> [다음](enhancing-data-validation.md)
