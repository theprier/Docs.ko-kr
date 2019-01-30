---
uid: mvc/overview/getting-started/database-first-development/customizing-a-view
title: '자습서: ASP.NET MVC 앱을 사용 하 여 EF Database First에 대 한 보기를 사용자 지정'
description: 이 자습서는 프레젠테이션을 개선할에 자동으로 생성 된 보기를 변경에 중점을 둡니다.
author: Rick-Anderson
ms.author: riande
ms.date: 01/24/2019
ms.topic: tutorial
ms.assetid: 269380ff-d7e1-4035-8ad1-fe1316a25f76
msc.legacyurl: /mvc/overview/getting-started/database-first-development/customizing-a-view
msc.type: authoredcontent
ms.openlocfilehash: 89b8a0eb84b6e287c45bc141c68a2c76e63b0e41
ms.sourcegitcommit: c47d7c131eebbcd8811e31edda210d64cf4b9d6b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2019
ms.locfileid: "55236499"
---
# <a name="tutorial-customize-view-for-ef-database-first-with-aspnet-mvc-app"></a>자습서: ASP.NET MVC 앱을 사용 하 여 EF Database First에 대 한 보기를 사용자 지정

MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여, 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다. 이 자습서 시리즈에서는 자동으로 표시, 편집, 만들기, 사용자를 사용 하는 코드를 생성 하 고 데이터베이스 테이블에 있는 데이터를 삭제 하는 방법을 보여 줍니다. 생성된 된 코드는 데이터베이스 테이블의 열에 해당합니다.

이 자습서는 프레젠테이션을 개선할에 자동으로 생성 된 보기를 변경에 중점을 둡니다.

이 자습서에서는 다음을 수행했습니다.

> [!div class="checklist"]
> * 학생 세부 정보 페이지에 강좌 추가
> * 강좌 페이지에 추가 되어 있는지 확인 합니다.

## <a name="prerequisites"></a>전제 조건

* [데이터베이스 변경](changing-the-database.md)

## <a name="add-courses-to-student-detail"></a>과정 학생 정보 추가

생성된 된 코드는 응용 프로그램에 대 한 좋은 시작점을 제공 하지만 필요 하지 않습니다 모든 응용 프로그램에 필요한 기능입니다. 응용 프로그램의 특정 요구 사항에 맞게 코드를 사용자 지정할 수 있습니다. 현재 응용 프로그램 선택한 학생에 대 한 등록된 과정을 표시 하지 않습니다. 이 섹션에서는 추가 등록된 과정을 각 학생에 대 한 합니다 **세부 정보** 학생에 대 한 보기입니다.

오픈 **뷰** > **학생** > *Details.cshtml*합니다. 마지막으로 아래 &lt;/dl&gt; 태그를 닫기 전에 &lt;/div&gt; 태그에 다음 코드를 추가 합니다.

[!code-cshtml[Main](customizing-a-view/samples/sample1.cshtml)]

이 코드에서는 선택한 학생에 대해 Enrollment 테이블의 각 레코드에 대 한 행을 표시 하는 테이블을 만듭니다. 합니다 **표시** 메서드는 expression을 나타내는 개체 (modelItem)에 대 한 HTML을 렌더링 합니다. 표시 메서드를 사용 하면 단순히 코드에서 속성 값을 포함) (대신 값의 해당 형식 및 해당 형식에 대 한 서식 파일에 따라 올바르게 서식이 지정 되는지 확인 합니다. 이 예제에서는 각 식 루프의 현재 레코드에서 단일 속성을 반환 하 고 값 형식은 기본 텍스트로 렌더링 됩니다.

## <a name="confirm-courses-are-added"></a>강좌가 추가 확인

솔루션을 실행합니다. 클릭 **학생의 목록을** 선택한 **세부 정보** 학습자 중 하나에 대 한 합니다. 보기에 포함 된 등록된 과정을 볼 수 있습니다.

![학생 등록](customizing-a-view/_static/image1.png)

## <a name="next-steps"></a>다음 단계
이 자습서에서는 다음을 수행했습니다.

> [!div class="checklist"]
> * 학생 세부 정보 페이지로 추가 과정
> * 강좌 페이지에 추가 되어 있는지 확인 합니다.

데이터 주석 유효성 검사 요구 사항을 지정 및 서식을 추가 하는 방법을 알아보려면 다음 자습서로 이동 합니다.
> [!div class="nextstepaction"]
> [데이터 유효성 검사 향상](enhancing-data-validation.md)
