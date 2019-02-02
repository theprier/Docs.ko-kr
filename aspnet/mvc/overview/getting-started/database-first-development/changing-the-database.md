---
uid: mvc/overview/getting-started/database-first-development/changing-the-database
title: '자습서: ASP.NET MVC 앱을 사용 하 여 EF Database First에 대 한 데이터베이스 변경'
description: 이 자습서는 데이터베이스 구조를 업데이트 하 고 웹 응용 프로그램 전체에서 해당 변경 내용을 전파에 중점을 둡니다.
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: cfd5c083-a319-482e-8f25-5b38caa93954
msc.legacyurl: /mvc/overview/getting-started/database-first-development/changing-the-database
msc.type: authoredcontent
ms.openlocfilehash: 52cad1120908cf0d4f85770f8e2690f9415c5f56
ms.sourcegitcommit: ed76cc752966c604a795fbc56d5a71d16ded0b58
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/02/2019
ms.locfileid: "55667637"
---
# <a name="tutorial-change-the-database-for-ef-database-first-with-aspnet-mvc-app"></a>자습서: ASP.NET MVC 앱을 사용 하 여 EF Database First에 대 한 데이터베이스 변경

MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여, 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다. 이 자습서 시리즈에서는 자동으로 표시, 편집, 만들기, 사용자를 사용 하는 코드를 생성 하 고 데이터베이스 테이블에 있는 데이터를 삭제 하는 방법을 보여 줍니다. 생성된 된 코드는 데이터베이스 테이블의 열에 해당합니다.

이 자습서는 데이터베이스 구조를 업데이트 하 고 웹 응용 프로그램 전체에서 해당 변경 내용을 전파에 중점을 둡니다.

이 자습서에서는 다음을 수행했습니다.

> [!div class="checklist"]
> * 열 추가
> * 보기에 속성 추가

## <a name="prerequisites"></a>전제 조건

* [뷰 생성](generating-views.md)

## <a name="add-a-column"></a>열 추가

데이터베이스에서 테이블의 구조를 업데이트 하는 경우 변경 내용을 데이터 모델, 뷰 및 컨트롤러에 전파 되는 확인 해야 합니다.

이 자습서에서는 학생의 중간 이름은 기록할 학생 테이블에 새 열을 추가 합니다. 이 열을 추가 하려면 데이터베이스 프로젝트를 열고 Student.sql 파일을 엽니다. 디자이너 또는 T-SQL 코드를 통해 라는 열을 추가 **MiddleName** 는 nvarchar (50)을 NULL 값을 허용 합니다.

데이터베이스 프로젝트 (또는 f5 키)를 시작 하 여 로컬 데이터베이스에이 변경 내용을 배포 합니다. 새 필드를 테이블에 추가 됩니다. SQL Server 개체 탐색기에 표시 되지 않으면 창의 새로 고침 단추를 클릭 합니다.

![새 열을 표시](changing-the-database/_static/image2.png)

데이터베이스 테이블에 새 열이 있지만 데이터 모델 클래스에 현재 존재 하지 않습니다. 새 열을 포함 하도록 모델을 업데이트 해야 합니다. 에 **모델** 폴더를 열고 합니다 **ContosoModel.edmx** 모델 다이어그램을 표시 하는 파일입니다. 학생 모델 MiddleName 속성이 없는지 확인 합니다. 디자인 화면에서 아무 곳 이나 마우스 오른쪽 단추로 클릭 하 고 선택 **데이터베이스에서 모델 업데이트**합니다.

업데이트 마법사에서 선택 합니다 **새로 고침** 탭을 선택한 다음 **테이블** > **dbo** > **학생**합니다. **마침**을 클릭합니다.

데이터베이스 다이어그램에 새 업데이트 프로세스가 완료 되 면 **MiddleName** 속성입니다. 저장 된 **ContosoModel.edmx** 파일입니다. 새 속성에 전파에 대 한이 파일을 저장 해야 합니다 **Student.cs** 클래스입니다. 이제 데이터베이스 및 모델을 업데이트 했습니다.

솔루션을 빌드합니다.

## <a name="add-the-property-to-the-views"></a>보기에 속성 추가

그러나 뷰 여전히 없는 새 속성입니다. 뷰를 업데이트 하려면 두 가지 옵션이 있습니다-Student 클래스에 대 한 스 캐 폴딩 다시 한 번 추가 하 여 뷰를 다시 생성 하거나 수 또는 기존 보기에 새 속성을 수동으로 추가할 수 있습니다. 이 자습서에서는 스 캐 폴딩을 추가 다시 하지 사용자 지정된 내용을 자동으로 생성 된 보기에 변경한 때문입니다. 뷰를 변경 하 고 해당 변경 내용을 손실 하지 않으려는 경우 속성을 수동으로 추가 하는 것이 좋습니다.

뷰는 다시 생성, 삭제 합니다 **학생** 아래에 폴더 **뷰**, 및 삭제를 **StudentsController**. 마우스 오른쪽 단추로 클릭 합니다 **컨트롤러** 폴더에 대 한 스 캐 폴딩을 추가 및 합니다 **학생** 모델입니다. 마찬가지로 컨트롤러 이름을 **StudentsController**합니다. **추가**를 선택합니다.

솔루션을 다시 빌드하십시오. 이제는 뷰 MiddleName 속성을 포함합니다.

![중간 이름 표시](changing-the-database/_static/image5.png)

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음을 수행했습니다.

> [!div class="checklist"]
> * 열 추가
> * 보기에 속성 추가

학생 레코드에 대 한 세부 정보를 표시 하는 것에 대 한 보기를 사용자 지정 하는 방법을 알아보려면 다음 자습서로 이동 합니다.
> [!div class="nextstepaction"]
> [보기를 사용자 지정](customizing-a-view.md)