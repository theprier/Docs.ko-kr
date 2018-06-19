---
uid: mvc/overview/getting-started/database-first-development/generating-views
title: 'ASP.NET MVC를 사용 하 여 먼저 EF 데이터베이스: 뷰를 생성 | Microsoft Docs'
author: tfitzmac
description: MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다. 이 자습서 seri 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/29/2014
ms.topic: article
ms.assetid: 669367cf-8e30-4eb6-821d-10a7d9bb906c
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/database-first-development/generating-views
msc.type: authoredcontent
ms.openlocfilehash: b60e89a187a879255eb051dc87241714cef6fa63
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30879753"
---
<a name="ef-database-first-with-aspnet-mvc-generating-views"></a>ASP.NET MVC를 사용 하 여 먼저 EF 데이터베이스: 뷰 생성
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

> MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다. 이 자습서 시리즈 자동으로 표시, 편집를 만들 수 있도록 하는 코드를 생성 하 고 데이터베이스 테이블에 있는 데이터를 삭제 하는 방법을 보여 줍니다. 생성 된 코드는 데이터베이스 테이블의 열에 해당합니다.
> 
> 시리즈의이 부분 컨트롤러와 뷰를 생성 하려면 ASP.NET 스 캐 폴딩을 사용에 중점을 둡니다.


## <a name="add-scaffold"></a>스 캐 폴드를 추가 합니다.

모델 클래스에 대 한 표준 데이터 작업을 제공 하는 코드를 생성할 준비가 되었습니다. 스 캐 폴드 항목을 추가 하 여 코드를 추가 합니다. 여러 가지 옵션이 있습니다 스 캐 폴드를 추가할 수 있습니다; 형식에 대 한 이 자습서에서는 이전 섹션에서 만든 학생과 등록 모델에 해당 하는 뷰와 컨트롤러는 스 캐 폴드 포함 됩니다.

프로젝트에서 일관성을 유지 하려면 기존에 새로운 컨트롤러를 추가 합니다 **컨트롤러** 폴더입니다. 마우스 오른쪽 단추로 클릭는 **컨트롤러** 폴더를 찾아 선택 **추가** – **스 캐 폴드 된 새 항목**합니다.

![스 캐 폴드를 추가 합니다.](generating-views/_static/image1.png)

선택 된 **Entity Framework를 사용 하 여 뷰를 포함 된 MVC 5 컨트롤러** 옵션입니다. 이 옵션은 컨트롤러와 뷰 업데이트, 삭제, 만들고 표시 하기 위한 데이터 모델에 생성 됩니다.

![mvc 컨트롤러 추가](generating-views/_static/image2.png)

선택 **학생** 선택한 모델 클래스에 대 한는 **ContosoUniversityEntities** 컨텍스트 클래스에 대 한 합니다. 컨트롤러 이름으로 유지 **StudentsController**,

![컨트롤러를 지정 합니다.](generating-views/_static/image3.png)

**추가**를 클릭합니다.

이전 섹션에서 프로젝트를 빌드하지 않은 오류가 발생 하는 경우 수 있습니다. 이 경우 프로젝트를 빌드하지 시도 하 고 다시 스 캐 폴드 된 항목을 추가 합니다.

코드 생성 프로세스가 완료 되 면 프로젝트에서 새로운 컨트롤러와 뷰를 표시 됩니다.

![보기 표시](generating-views/_static/image4.png)

동일한 단계를 다시 수행 하지만 등록 클래스에 대 한 스 캐 폴드를 추가 합니다. 완료 되 면 나면는 **EnrollmentsController.cs** 파일과 하위 폴더 **뷰** 라는 **등록** 된 만들기, 삭제, 세부 정보, 편집 및 인덱스 레이아웃.

![보기 표시](generating-views/_static/image5.png)

## <a name="add-links-to-new-views"></a>새 보기에 링크 추가

새 보기를 탐색할 수에 대 한 쉽게 학생 및 등록을 위한 인덱스 뷰를 몇 가지 하이퍼링크를 추가할 수 있습니다. 파일을 엽니다 **Views/Home/Index.cshtml**,이 사이트에 대 한 홈 페이지입니다. jumbotron 아래에 다음 코드를 추가 합니다.

[!code-cshtml[Main](generating-views/samples/sample1.cshtml)]

ActionLink 메서드 첫 번째 매개 변수는 링크에 표시할 텍스트입니다. 두 번째 매개 변수는 작업 및 세 번째 매개 변수는 컨트롤러의 이름입니다. 예를 들어 첫 번째 링크 StudentsController 있는 인덱스 작업을 가리킵니다. 실제 하이퍼링크는 다음이 값 중에서 구성 됩니다. 첫 번째 링크 궁극적으로 이동 하는 **Index.cshtml** 내에 파일이 **뷰/학생** 폴더입니다.

## <a name="display-student-views"></a>학생 보기 표시

프로젝트에 올바르게 추가 코드를 학습자의 목록을 표시 및 사용자가 편집 만들거나 데이터베이스에서 학생 레코드를 삭제할 수 있도록 확인 합니다.

마우스 오른쪽 단추로 클릭는 **Views/Home/Index.cshtml** 파일을 찾아 선택 **브라우저에서 보기**합니다. 이 페이지에서는 학생 목록에 대 한 링크를 클릭 합니다.

![](generating-views/_static/image6.png)

이 페이지에서이 데이터를 수정 하는 학생 및 링크 목록을 확인 합니다.

![학생 목록](generating-views/_static/image7.png)

클릭는 **새로 만들기** 에 연결 하 고 새 학생에 대 한 일부 값을 제공 합니다.

![새 학생 만들기](generating-views/_static/image8.png)

클릭 **만들기**, 및 새 학생 목록에 추가 됩니다.

![새 학생을 사용 하 여 목록](generating-views/_static/image9.png)

선택 된 **편집** 링크를 선택한 학생에 대 한 값 중 일부를 변경 합니다.

![학생 편집](generating-views/_static/image10.png)

클릭 **저장**, 학생 레코드가 변경 되었는지 확인 합니다.

마지막으로, 선택는 **삭제** 에 연결 하 고 확인을 클릭 하 여 레코드를 삭제 하는 **삭제** 단추입니다.

![학생을 삭제 합니다.](generating-views/_static/image11.png)

모든 코드를 작성 하지 않고도 학생 테이블의 데이터에 대 한 일반적인 작업을 수행 하는 뷰를 추가 했습니다.

필드에 대 한 텍스트 레이블을 데이터베이스 속성에 따라은 단어로 (같은 **LastName**) 되지 않습니다는 웹 페이지에 표시 하려는 합니다. 예를 들어 레이블이 되도록 할 수도 있습니다 **성**합니다. 이 자습서의 뒷부분에 나오는이 디스플레이 문제를 해결 합니다.

## <a name="display-enrollment-views"></a>등록 보기 표시

데이터베이스에 학생과 등록 테이블 Course 및 등록 테이블 간의 일 대 다 관계 사이 일 대 다 관계에 포함 됩니다. 등록에 대 한 보기 이러한 관계를 올바르게 처리합니다. 사이트 및 선택에 대 한 홈 페이지로 이동 하는 **등록 목록이** 링크 차례로 **새로 만들기** 링크 합니다. 새 등록 레코드를 만들기 위한 폼에 표시 합니다. 특히, 관련된 테이블의 값으로 채워진 두 드롭 다운 목록 폼에 포함 되어 있는지 확인 합니다.

![등록 만들기](generating-views/_static/image12.png)

또한 필드의 데이터 형식에 제공된 된 값의 유효성 검사는 따라 적용 자동으로 됩니다. 등급 호환 되지 않는 값을 제공 하려고 하면 오류 메시지가 보고서가 표시 되도록 숫자를 필요 합니다.

![유효성 검사 메시지](generating-views/_static/image13.png)

데이터베이스의 데이터로 작업 하는 사용자가 자동으로 생성 된 뷰를 사용 하면 있는지 확인 합니다. 이 시리즈의 다음 자습서에서는 데이터베이스를 업데이트 하 고 웹 응용 프로그램에서 해당 변경 됩니다.

> [!div class="step-by-step"]
> [이전](creating-the-web-application.md)
> [다음](changing-the-database.md)
