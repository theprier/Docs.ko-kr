---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
title: "Entity Framework 6 Code First MVC 5를 사용 하 여 시작 | Microsoft Docs"
author: tdykstra
description: "이 자습서 시리즈의 최신 버전을 사용할 수 있는: Visual Studio 2015를 사용 하 여 Entity Framework Core 및 ASP.NET Core 시작 합니다. Contoso Universi 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/22/2015
ms.topic: article
ms.assetid: 00bc8b51-32ed-4fd3-9745-be4c2a9c1eaf
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 46f53279e2e6daa4266c06feb4ba544e14b68a03
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="getting-started-with-entity-framework-6-code-first-using-mvc-5"></a>MVC 5를 사용하여 Entity Framework 6 Code First 시작
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

[완료 된 프로젝트를 다운로드](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8) 또는 [PDF 다운로드](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20Entity%20Framework%206%20Code%20First%20using%20MVC%205.pdf)

> > [!NOTE] 
> > 
> > 이 자습서 시리즈의 최신 버전을 사용할 수 있는: [ASP.NET Core 및 Visual Studio 2015를 사용 하 여 Entity Framework Core 시작](https://docs.asp.net/en/latest/data/ef-mvc/intro.html)합니다.
> 
> 
> Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 6 및 Visual Studio 2013을 사용 하 여 ASP.NET MVC 5 응용 프로그램을 만드는 방법을 보여 줍니다. 이 자습서에서는 코드 첫 번째 워크플로 사용 합니다. Code First, Database First 및 Model First 선택 하는 방법에 대 한 정보를 참조 하십시오. [Entity Framework 개발 워크플로에](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)합니다.
> 
> 샘플 응용 프로그램은 웹 사이트 가상 Contoso 대학입니다. 학생 진입, 과정 만들기 및 강사 할당 등의 기능을 포함합니다. 이 자습서 시리즈 Contoso 대학 샘플 응용 프로그램을 작성 하는 방법에 설명 합니다. 있습니다 수 [완성 된 응용 프로그램 다운로드](https://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8)합니다.
> 
> Mike Brind에 의해 번역 Visual Basic 버전은 사용할 수 있는: [Visual Basic의 EF 6 MVC 5](http://www.mikesdotnetting.com/Article/241/MVC-5-with-EF-6-in-Visual-Basic-Creating-an-Entity-Framework-Data-Model) Mikesdotnetting 사이트에 있습니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - .NET 4.5
> - Entity Framework 6 (EntityFramework 6.1.0 NuGet 패키지)
> - [Windows Azure SDK 2.2](https://go.microsoft.com/fwlink/p/?linkid=323510) (선택 사항)
>   
> 
> 이 자습서도 호환 [Visual Studio 2013 Express for Web](https://www.microsoft.com/visualstudio/eng/2013-downloads#d-2013-express) 또는 Visual Studio 2012입니다. [VS 2012 버전의 Windows Azure SDK](https://go.microsoft.com/fwlink/p/?linkid=323511) Visual Studio 2012를 사용한 Windows Azure 배포에 필요 합니다.
> 
> 
> ## <a name="tutorial-versions"></a>자습서 버전
> 
> 이 자습서의 이전 버전에 대 한 참조 [EF 4.1 / MVC 3 전자책](https://social.technet.microsoft.com/wiki/contents/articles/11608.e-book-gallery-for-microsoft-technologies.aspx#GettingStartedwiththeEntityFramework4.1usingASP.NETMVC) 및 [MVC 4를 사용 하 여 EF 5 시작](../../older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다.
> 
> ## <a name="questions-and-comments"></a>질문이 나 의견이
> 
> 이 자습서를 연결 하는 방법 및 페이지의 맨 아래에 주석에서 향상 될 수 있습니다 어떻게에 의견을 남겨 주세요. 자습서를 직접 관련 되지 않는 질문 해야 하도록를 게시할 수 있습니다는 [ASP.NET Entity Framework 포럼](https://forums.asp.net/1227.aspx), [Entity Framework와 LINQ to Entities 포럼](https://social.msdn.microsoft.com/forums/adodotnetentityframework/threads/), 또는 [ StackOverflow.com](http://stackoverflow.com/)합니다.
> 
> 문제를 해결할 수 없는 실행 하는 경우 코드를 다운로드할 수 있는 완료 된 프로젝트를 비교 하 여 일반적으로 문제에 솔루션을 찾을 수 있습니다. 몇 가지 일반적인 오류 및 해결 하는 방법에 대 한 참조 [일반적인 오류 및 솔루션 또는 해당에 대 한 대안입니다.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)


## <a name="the-contoso-university-web-application"></a>Contoso 대학 웹 응용 프로그램

이 자습서에를 작성 하는 응용 프로그램은 간단한 대학 웹 사이트.

사용자가 볼 수 있으며 학생과에서는 강사 정보 업데이트 됩니다. 다음은 몇 화면을 만듭니다.

![Students_Index_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image1.png)

![학생 편집](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image2.png)

이 자습서는 Entity Framework를 사용 하는 방법에 주로 초점을 맞출 수 있도록이 사이트의 사용자 인터페이스 스타일은 기본 제공 템플릿에서 생성 내용을 가까운 유지 되었습니다.

## <a name="prerequisites"></a>필수 구성 요소

참조 **소프트웨어 버전** 페이지의 위쪽에 있습니다. Entity Framework 6 자습서의 일부로 EF NuGet 패키지를 설치 하기 때문에 필수 구성 요소 않습니다.

## <a name="create-an-mvc-web-application"></a>MVC 웹 응용 프로그램 만들기

Visual Studio를 열고 "ContosoUniversity" 라는 새로운 C# 웹 프로젝트를 만듭니다.

![New_project_dialog_box](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image3.png)

에 **새 ASP.NET 프로젝트** 대화 상자 선택 된 **MVC** 서식 파일입니다.

경우는 **클라우드의 호스트에에서** 확인란에는 **Microsoft Azure** 섹션을 선택 하면 확인란의 선택을 취소 합니다.

클릭 **인증 변경**합니다.

![New_project_dialog_box](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image4.png)

에 **인증 변경** 대화 상자에서 **인증 안 함**, 클릭 하 고 **확인**합니다. 이 자습서에 대 한 없습니다 수에 로그온 하려면 사용자에 게 요청 하거나 로그온 한 사용자에 따라 액세스를 제한 합니다.

![New_project_dialog_box](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image5.png)

새 ASP.NET 프로젝트 대화 상자에서 다시 클릭 **확인** 프로젝트를 만듭니다.

## <a name="set-up-the-site-style"></a>사이트 스타일 설정

몇 가지 간단한 변경 사항이 사이트 메뉴, 레이아웃 및 홈 페이지를 설정 합니다.

열기 *Views\Shared\\_Layout.cshtml*, 다음과 같이 변경 하 고 있습니다.

- "내 ASP.NET 응용 프로그램" 및 "응용 프로그램 이름"의 "Contoso 대학"으로 변경 합니다.
- 학생, 강의 교사, 및 부서를 위한 메뉴 항목을 추가 하 고 연락처 항목을 삭제 합니다.

변경 내용은 강조 표시 됩니다.

[!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample1.cshtml?highlight=6,19,24-27,38)]

*Views\Home\Index.cshtml*, 파일의 내용을이 응용 프로그램에 대 한 텍스트도 ASP.NET MVC에 대 한 텍스트를 바꾸려면 다음 코드로 바꿉니다.

[!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample2.cshtml)]

사이트를 실행 하려면 CTRL + f 5를 누릅니다. 주 메뉴와 홈 페이지가 나타납니다.

![Contoso_University_home_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image6.png)

## <a name="install-entity-framework-6"></a>Entity Framework 6을 설치 합니다.

**도구** 메뉴 클릭 **NuGet 패키지 관리자** 클릭 하 고 **패키지 관리자 콘솔**합니다.

에 **패키지 관리자 콘솔** 창에 다음 명령을 입력 합니다.

`Install-Package EntityFramework`

![EF 설치](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image7.png)

이미지를 설치 하 고 6.0.0 보여주지만 NuGet 됩니다 최신 버전 (시험판 버전은 제외), Entity Framework의 설치는 설치부터 자습서에 대 한 가장 최근의 업데이트 6.1.1.

이 단계는이 자습서에는 수동으로 작업을 수행할 수 있지만 수행 하기 위해 자동으로 ASP.NET MVC 스 캐 폴딩 기능으로 몇 가지 단계 중 하나입니다. 수행 하는 작업을 수동으로 Entity Framework를 사용 하는 데 필요한 단계를 볼 수 있도록 합니다. 나중에 사용할 스 캐 폴딩 MVC 컨트롤러와 뷰를 만듭니다. 스 캐 폴딩 자동으로 EF NuGet 패키지 설치, 데이터베이스 컨텍스트 클래스를 만들고 연결 문자열을 만들 수 있도록 것이 좋습니다. 이런 방식으로 작업을 수행할 준비가 해야 할 모든 경우에 이러한 단계를 건너뛰고 엔터티 클래스를 만든 후에 MVC 컨트롤러를 스 캐 폴드 있습니다.

## <a name="create-the-data-model"></a>데이터 모델 만들기

다음 Contoso 대학교 응용 프로그램에 대 한 엔터티 클래스 만듭니다. 다음 세 가지 엔터티부터 시작 합니다.

![Class_diagram](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image8.png)

간의 일 대 다 관계가 `Student` 및 `Enrollment` 엔터티 간의 일 대 다 관계 이며 `Course` 및 `Enrollment` 엔터티. 즉, 학생 과정을 개수에 관계 없이 등록 될 수 있습니다 및 과정에 학생에 등록 여러 개가 있을 수 있습니다.

다음 섹션에서는 각각에 대 한 이러한 엔터티의 클래스를 만듭니다.

> [!NOTE]
> 이러한 엔터티 클래스의 모든 만들기를 완료 하기 전에 프로젝트를 컴파일할 하려고 하면 컴파일러 오류가 발생 합니다.


### <a name="the-student-entity"></a>학생 엔터티

![Student_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image9.png)

에 *모델* 폴더를 라는 클래스 파일을 만들 *Student.cs* 템플릿 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample3.cs)]

`ID` 속성이이 클래스에 해당 하는 데이터베이스 테이블의 기본 키 열이 됩니다. Entity Framework를 기본적으로 명명 된 속성을 해석 `ID` 또는 *classname* `ID` 기본 키로 합니다.

`Enrollments` 속성은 한 *탐색 속성*합니다. 이 엔터티와 관련 된 다른 엔터티와 탐색 속성을 보유 합니다. 이 경우에 `Enrollments` 속성은 `Student` 의 모든 엔터티를 포함할는 `Enrollment` 엔터티는 관련 된 `Student` 엔터티. 즉, 하는 경우는 주어진 `Student` 데이터베이스의 행에는 관련 된 두 개의 `Enrollment` 행 (해당 학생의 기본 키를 포함 하는 행에서 값을 해당 `StudentID` 외래 키 열), 해당 `Student` 엔터티의 `Enrollments` 탐색 속성 이 두 들어갑니다 `Enrollment` 엔터티.

탐색 속성은 일반적으로 정의 `virtual` 특정 Entity Framework 기능을 이용와 같은 많이 있도록 *한 지연 로딩이*합니다. (한 지연 로딩이 설명 있습니다의 뒷부분에 나오는 [관련 데이터를 읽는](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) 이 시리즈의 뒷부분에 나오는 자습서입니다.)

해당 형식은 항목 추가, 삭제 및 업데이트와 같은 될 수 있는 목록 이어야 합니다는 탐색 속성 (예: 다 대 다 또는 일 대 다 관계) 여러 엔터티를 보유할 수, 하는 경우 `ICollection`합니다.

### <a name="the-enrollment-entity"></a>등록 엔터티

![Enrollment_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image10.png)

에 *모델* 폴더를 만들 *Enrollment.cs* 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample4.cs)]

`EnrollmentID` 속성은 기본 키를 됩니다;이 엔터티 사용는 *classname* `ID` 대신 패턴 `ID` 에서 본 것 처럼 자체적으로 `Student` 엔터티. 일반적으로 한 패턴을 선택 하는 데이터 모델 전체에서 사용 합니다. 여기서는 변형 패턴 중 하나를 사용할 수 있는 보여 줍니다. 자습서의 뒷부분에 표시 됩니다 방법을 사용 하 여 `ID` 없이 `classname` 데이터 모델에서 상속을 구현 하기가 쉬워집니다.

`Grade` 속성은 한 [enum](https://msdn.microsoft.com/data/hh859576.aspx)합니다. 후 물음표는 `Grade` 형식 선언을 나타냅니다는 `Grade` 속성은 [nullable](https://msdn.microsoft.com/library/2cf62fcy.aspx)합니다. Null이 등급은 0 개 등급 다릅니다-의미 하는 등급 알려진 또는 아직 할당 되지 않았습니다.

`StudentID` 속성은 외래 키 및 해당 탐색 속성은 `Student`합니다. `Enrollment` 엔터티는 하 나와 연결 `Student` 엔터티, 속성에는 단일만 포함할 수 있으므로 `Student` 엔터티 (달리는 `Student.Enrollments` 탐색 속성 했 듯이, 여러을 보유할 수 있는 `Enrollment` 엔터티)입니다.

`CourseID` 속성은 외래 키 및 해당 탐색 속성은 `Course`합니다. `Enrollment` 엔터티는 하 나와 연결 `Course` 엔터티.

Entity Framework 라고 하는 경우 외래 키 속성으로 속성을 해석  *&lt;탐색 속성 이름&gt;&lt;기본 키 속성 이름&gt;*  (예를 들어 `StudentID`에 대 한는 `Student` 이후 탐색 속성에서 `Student` 엔터티의 기본 키가 `ID`). 외래 키 속성 수 또한 같은 이름 단순히  *&lt;기본 키 속성 이름&gt;*  (예를 들어 `CourseID` 이후는 `Course` 엔터티의 기본 키가 `CourseID`).

### <a name="the-course-entity"></a>과정 엔터티

![Course_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image11.png)

에 *모델* 폴더를 만들 *Course.cs*, 템플릿 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample5.cs)]

`Enrollments` 속성은 탐색 속성입니다. A `Course` 개수에 관계 없이 관련 될 수 있는 엔터티 `Enrollment` 엔터티.

에 대 한 내용은 라고는 [DatabaseGenerated](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedattribute(v=vs.110).aspx) 이 시리즈의 자습서의 뒷부분에서 특성입니다. 기본적으로,이 특성 과정 대신 생성 하는 데이터베이스에 대 한 기본 키를 입력할 수 있습니다.

## <a name="create-the-database-context"></a>데이터베이스 컨텍스트 만들기

지정된 된 데이터 모델에 대 한 Entity Framework 기능을 조정 하는 기본 클래스는는 *데이터베이스 컨텍스트* 클래스입니다. 이 클래스에서 파생 시켜 만들는 [System.Data.Entity.DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx) 클래스입니다. 코드에서 데이터 모델에 포함 된 엔터티 지정 합니다. 특정 Entity Framework 동작을 사용자 지정할 수 있습니다. 이 프로젝트에 클래스 이름은 `SchoolContext`합니다.

프로젝트를 마우스 오른쪽 단추로 클릭 ContosoUniversity 프로젝트의 폴더를 만들려고 **솔루션 탐색기** 클릭 **추가**, 클릭 하 고 **새 폴더**합니다. 새 폴더 이름을 *DAL* (데이터 액세스 계층)에 대 한 합니다. 해당 폴더에 라는 새 클래스 파일을 만들 *SchoolContext.cs*, 템플릿 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample6.cs)]

### <a name="specifying-entity-sets"></a>지정 하 여 엔터티 집합

이 코드에서는 [DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=VS.103).aspx) 각 엔터티 집합에 대 한 속성입니다. Entity Framework 용어에서는 *엔터티 집합* 일반적으로 데이터베이스 테이블에 해당 및 *엔터티* 테이블의 행에 해당 합니다.

> [!NOTE] 
> 
> 생략 했습니다 수는 `DbSet<Enrollment>` 및 `DbSet<Course>` 문과 것은 동일 하 게 작동 합니다. Entity Framework 하기 때문에 암시적으로 해당 포함 됩니다는 `Student` 엔터티 참조는 `Enrollment` 엔터티 및 `Enrollment` 엔터티 참조는 `Course` 엔터티.


### <a name="specifying-the-connection-string"></a>연결 문자열을 지정

(나중에 추가할 web.config)이 표시 되는 연결 문자열의 이름에는 생성자에 전달 됩니다.

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample7.cs?highlight=1)]

또한 Web.config 파일에 저장 된의 이름이 아니라 연결 문자열 자체에 전달할 수 있습니다. 사용 하도록 데이터베이스를 지정 하기 위한 옵션에 대 한 자세한 내용은 참조 [Entity Framework 연결 및 모델](https://msdn.microsoft.com/data/jj592674)합니다.

연결 문자열 또는 하나의 이름을 명시적으로 지정 하지 않으면, Entity Framework 연결 문자열 이름이 클래스 이름과 이라고 가정 합니다. 이 예제의 기본 연결 문자열 이름이 됩니다. `SchoolContext`, 명시적으로 지정 하는 어떤와 동일 합니다.

### <a name="specifying-singular-table-names"></a>단일 테이블 이름 지정

`modelBuilder.Conventions.Remove` 의 문에서 [OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx) 복수화 되 고에서 테이블 이름을 수 없습니다. 이렇게 하지 않은 데이터베이스에 생성된 된 테이블 이름이 `Students`, `Courses`, 및 `Enrollments`합니다. 테이블 이름이 됩니다 대신 `Student`, `Course`, 및 `Enrollment`합니다. 개발자는 테이블 이름을 복수화할지 여부에 대해 동의하지 않습니다. 이 자습서에서는 단 수 형태를 사용 하지만 중요 한 점은 포함 하거나 코드이 줄을 생략 하 여 원하는 어떤 폼을 선택할 수 있습니다.

## <a name="set-up-ef-to-initialize-the-database-with-test-data"></a>테스트 데이터로 데이터베이스 초기화에 EF를 설정 합니다.

Entity Framework 수 자동으로 만들기 (또는 삭제 및 재생성이) 응용 프로그램을 실행 하는 시기에 대 한 데이터베이스입니다. 이렇게 해야 응용 프로그램이 실행 될 때마다 또는 모델은 기존 데이터베이스와 동기화 하는 경우에 지정할 수 있습니다. 작성할 수도 있습니다는 `Seed` 메서드 Entity Framework 자동으로 테스트 데이터로 채우기 위해 데이터베이스를 만든 후 호출 합니다.

기본 동작은 데이터베이스를 만드는 경우에 해당 하지 않는 존재 (모델 변경 되었으며이 데이터베이스가 이미 있는 경우 예외를 throw)입니다. 이 섹션에서는 데이터베이스 삭제 후 모델 변경 될 때마다 다시 생성을 지정 합니다. 데이터베이스를 삭제 하면 모든 데이터의 손실입니다. 이 일반적으로 정상 개발 하는 동안 때문에 `Seed` 메서드는 데이터베이스는 다시 생성 하 고 다시 생성 하 여 테스트 데이터를 실행 합니다. 않으려는 프로덕션 환경에서 일반적으로 데이터베이스 스키마를 변경 해야 할 때마다 모든 데이터를 보호 합니다. 나중에 모델 변경 내용을 삭제 하 고 데이터베이스를 다시 작성 하는 대신 데이터베이스 스키마를 변경 하려면 Code First 마이그레이션을 사용 하 여 처리 하는 방법을 볼 수 있습니다.

DAL 폴더에 라는 새 클래스 파일을 만들 *SchoolInitializer.cs* 누르고와 템플릿 코드는  
다음 코드를 만들 때 데이터베이스 필요 하 고 새 데이터베이스에 테스트 데이터를 로드 합니다.

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample8.cs)]

`Seed` 메서드가 데이터베이스 컨텍스트 개체를 입력된 매개 변수로 하 고 사용 하 여 메서드의 코드  
개체를 데이터베이스에 새 엔터티를 추가 합니다. 각 엔터티 형식에 대 한 코드의 컬렉션을 만들고 새로운  
 엔터티를 적절 한에 추가 `DbSet` 속성을 선택한 다음 변경 내용이 데이터베이스에 저장 합니다. 그것이 아니야  
호출할 필요는 `SaveChanges` 엔터티의:는 여기에서 하지만 이렇게 하면 도움이 되는 것 처럼 각 그룹 뒤 메서드  
코드는 데이터베이스에 쓰는 동안 예외가 발생 하는 경우에 문제의 원인을 찾습니다.

요소를 추가할 이니셜라이저 클래스를 사용 하려면 Entity Framework를 판단할 수는 `entityFramework` 응용 프로그램의 요소 *Web.config* 파일 (파일은 루트 프로젝트 폴더에), 다음 예제에서와 같이:

[!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample9.xml?highlight=2-6)]

`context type` 정규화 된 컨텍스트 클래스 이름 및에 어셈블리를 지정 및 `databaseinitializer type` 이니셜라이저 클래스 및 중인 어셈블리의 정규화 된 이름을 지정 합니다. (이니셜라이저를 사용 하는 EF를 사용 하지 않으려는 경우에 특성을 설정할 수 있습니다는 `context` 요소: `disableDatabaseInitialization="true"`.) 자세한 내용은 참조 [Entity Framework-구성 파일 설정](https://msdn.microsoft.com/data/jj556606)합니다.

에 이니셜라이저를 설정 하는 대신는 *Web.config* 파일은 추가 하 여 코드에서 수행 하는 `Database.SetInitializer` 문을 `Application_Start` 에서 메서드는 *Global.asax.cs* 파일입니다. 자세한 내용은 참조 [의 Entity Framework Code First 이해 데이터베이스 이니셜라이저](http://www.codeguru.com/csharp/article.php/c19999/Understanding-Database-Initializers-in-Entity-Framework-Code-First.htm)합니다.

응용 프로그램은 이제 설정 하는 데이터베이스의 지정 된 실행에서 처음으로 액세스할 때까지  
응용 프로그램을 Entity Framework 모델에 데이터베이스를 비교 합니다 (프로그램 `SchoolContext` 와 엔터티 클래스). 차이점이 있을 경우 응용 프로그램을 삭제 하 고 다시 데이터베이스를 만듭니다.

> [!NOTE]
> 프로덕션 웹 서버에 응용 프로그램을 배포 하는 경우 제거 하거나 삭제 되 고 데이터베이스를 다시 생성 하는 코드를 사용 하지 않도록 설정 해야 합니다. 하 한이 시리즈의 자습서의 뒷부분에서 수행 합니다.


## <a name="set-up-ef-to-use-a-sql-server-express-localdb-database"></a>EF SQL Server Express LocalDB 데이터베이스를 사용 하도록 설정

[LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx) 는 SQL Server Express 데이터베이스 엔진의 경량 버전입니다. 설치 및 구성, 요청 시 시작 되며 사용자 모드에서 실행 합니다. LocalDB 데이터베이스도 작업할 수 있도록 SQL Server Express의 특수 실행 모드에서 실행 *.mdf* 파일입니다. 에 LocalDB 데이터베이스 파일을 넣을 수 있습니다는 *앱\_데이터* 프로젝트와 데이터베이스를 복사할 수 있게 되기를 원하는 경우 웹 프로젝트의 폴더입니다. SQL Server express 사용자 인스턴스 기능 또한 작업할 수 있습니다 *.mdf* 은 사용자 인스턴스 기능은 사용 되지 않습니다; 따라서 LocalDB를 사용 하기 위한 좋습니다 *.mdf* 파일입니다. Visual Studio 2012 이상 버전에서 LocalDB는 Visual Studio를 사용 하 여 기본적으로 설치 됩니다.

일반적으로 SQL Server Express 프로덕션 웹 응용 프로그램에 대 한 사용 되지 않습니다. LocalDB 특히 권장 되지 않습니다 웹 응용 프로그램의 프로덕션 사용을 위해 하므로 IIS와 함께 작동 하도록 설계 되지 않았습니다.

이 자습서에서는 LocalDB 작업할 수 있습니다. 응용 프로그램을 열고 *Web.config* 파일을 추가 `connectionStrings` 요소 앞의 `appSettings` 요소를 다음 예제와 같이 합니다. (업데이트 해야는 *Web.config* 루트 프로젝트 폴더의 파일입니다. 또한는 *Web.config* 중인 파일의 *뷰* 업데이트할 필요가 없는 하위 폴더입니다.)

Visual Studio 2015를 사용 하는 경우에 기본 SQL Server 인스턴스 이름을 변경 하는 대로 "v11.0을" 연결 문자열에 "MSSQLLocalDB"으로 바꿉니다.

[!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample10.xml?highlight=1-3)]

사용자가 추가한 연결 문자열 지정 Entity Framework가 명명 된 LocalDB 데이터베이스를 사용 합니다 *ContosoUniversity1.mdf*합니다. (데이터베이스가 존재 하지 않으면; EF을 만듭니다.) 데이터베이스에 생성 될 경우 프로그램 *앱\_데이터* 폴더를 추가할 수 있습니다 `AttachDBFilename=|DataDirectory|\ContosoUniversity1.mdf` 연결 문자열에 있습니다. 연결 문자열에 대 한 자세한 내용은 참조 [ASP.NET 웹 응용 프로그램에 대 한 SQL Server 연결 문자열](https://msdn.microsoft.com/library/jj653752.aspx)합니다.

연결 문자열이 있이 필요가 실제로 *Web.config* 파일입니다. 연결 문자열을 지정 하지 않으면 Entity Framework는 기본 컨텍스트 클래스에 따라 하나를 사용 합니다. 자세한 내용은 참조 [Code First를 새 데이터베이스로](https://msdn.microsoft.com/data/jj193542)합니다.

## <a name="creating-a-student-controller-and-views"></a>학생 컨트롤러 및 뷰 만들기

이제 데이터를 표시 하는 웹 페이지를 만들어 봅니다 한 데이터를 요청 하는 과정은 자동으로 트리거  
데이터베이스 만들기입니다. 새 컨트롤러를 만들어 되기 시작 합니다. 하지만 그렇게 하기 전에 모델 및 컨텍스트 클래스를 MVC 컨트롤러 스 캐 폴딩을 사용할 수 있도록 프로젝트를 빌드합니다.

1. 마우스 오른쪽 단추로 클릭는 **컨트롤러** 폴더에 **솔루션 탐색기**선택, **추가**, 클릭 하 고 **스 캐 폴드 된 새 항목**합니다.
- 에 **추가 스 캐 폴드** 대화 상자에서 **Entity Framework를 사용 하 여 뷰를 포함 된 MVC 5 컨트롤러**합니다.

    ![스 캐 폴드를 추가 합니다.](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image12.png)
- 컨트롤러 추가 대화 상자에서 다음 옵션 선택 하 고 클릭 **추가**:

    - 모델 클래스: **학생 (ContosoUniversity.Models)**합니다. (드롭 다운 목록에서이 옵션을 표시 되지 않으면, 프로젝트 빌드 및 다시 시도 하십시오.)
    - 데이터 컨텍스트 클래스: **SchoolContext (ContosoUniversity.DAL)**합니다.
    - 컨트롤러 이름: **StudentController** (하지 StudentsController).
    - 다른 필드에 대 한 기본값 그대로 둡니다.

    ![Add_Controller_dialog_box_for_Student_controller](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image13.png)

    클릭할 때 **추가**는 scaffolder StudentController.cs 파일과 뷰 (.cshtml 파일)는 컨트롤러를 사용 하는 집합을 만듭니다. Entity Framework를 사용 하는 프로젝트를 만들 때에 나중에 사용자도 활용할 수는 scaffolder의 몇 가지 추가 기능: 방금 첫 번째 모델 클래스를 만들기, 연결 문자열을 만들지 않는 한 다음는 **컨트롤러추가** 상자 새 컨텍스트 클래스를 지정 합니다. scaffolder 만들어집니다 프로그램 `DbContext` 뿐만 아니라 컨트롤러 및 뷰 클래스 및 연결 문자열입니다.
- Visual Studio가 열릴는 *Controllers\StudentController.cs* 파일입니다. 클래스 변수 만들어진 데이터베이스 컨텍스트 개체를 인스턴스화하는 것이 표시 됩니다.

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

    `Index` 동작 메서드가에서 학생의 목록을 가져옵니다는 *학생* 엔터티 참조 하 여 집합에서 `Students` 데이터베이스 컨텍스트 인스턴스의 속성:

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

    *Student\Index.cshtml* 보기 테이블에이 목록에 표시 됩니다.

    [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample13.cshtml)]
- Ctrl+F5를 눌러 프로젝트를 실행합니다. ("섀도 복사본을 만들 수 없습니다" 오류가 발생할 경우 브라우저를 닫고 다시 시도 하십시오.)

    클릭는 **학생** 테스트 데이터를 탭 하는 `Seed` 삽입 메서드. 최소에 따라 브라우저 창, 학생 탭 링크 상위 주소 표시줄에 표시 또는 경우 링크를 표시 하려면 오른쪽 위 모서리를 클릭 해야 합니다.

    ![메뉴 단추](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image14.png)

    ![학생 인덱스 페이지](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image15.png)

## <a name="view-the-database"></a>데이터베이스 보기

학생 페이지를 실행 하는 경우 응용 프로그램 데이터베이스에 액세스 하려고 한 EF 준다는 사실을 알았습니다 데이터베이스가 없습니다. 발생 하 고 하나를 만들었습니다, 다음 실행 데이터와 데이터베이스를 채우는 seed 메서드.

사용할 수 있습니다 **서버 탐색기** 또는 **SQL Server 개체 탐색기** (SSOX) Visual Studio에서 데이터베이스를 볼 수 있습니다. 이 자습서에 대 한 사용 **서버 탐색기**합니다. (2013 년 보다 이전 버전 Visual Studio Express에서 **서버 탐색기** 라고 **데이터베이스 탐색기**.)

1. 브라우저를 닫습니다.
2. **서버 탐색기**, 확장 **데이터 연결**, 확장 **학교 컨텍스트 (ContosoUniversity)**, 펼친 다음 **테이블** 를 보려면 새 데이터베이스의 테이블입니다.

    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image16.png)
3. 마우스 오른쪽 단추로 클릭는 **학생** 테이블 마우스 클릭 **테이블 데이터 표시** 생성 된 열과 테이블에 삽입 된 행을 볼 수 있습니다.

    ![학생 테이블](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image17.png)
4. 닫기는 **서버 탐색기** 연결 합니다.

*ContosoUniversity1.mdf* 및 *.ldf* 데이터베이스 파일은는 `C:\Users\<yourusername>` 폴더입니다.

사용 중 이므로 `DropCreateDatabaseIfModelChanges` 이니셜라이저, 이제 해도에 대 한 변경의 `Student` 클래스 응용 프로그램을 다시 실행 하 고 데이터베이스는 자동으로 변경 내용을 맞게 다시 만들어질 수 있습니다. 예를 들어, 추가 하는 경우는 `EmailAddress` 속성을는 `Student` 클래스, 학생 페이지를 다시 실행 한 한 다음 보고 테이블 다시, 나타납니다 새 `EmailAddress` 열입니다.

## <a name="conventions"></a>규칙

사용으로 인해 전체 데이터베이스를 만들 수도 수 있게 되기를 Entity Framework에 대 한 순서 대로 작성 해야 했습니다 코드의 양을 최소화 됩니다 *규칙*, 또는 Entity Framework에서는 가정 합니다. 그 중 일부를 이미 확인 또는 대략적으로 사용자가 없이 사용 된:

- Pluralized 형태의 엔터티 클래스 이름은 테이블 이름으로 사용 됩니다.
- 엔터티 속성 이름은 열 이름에 사용 됩니다.
- 명명 된 엔터티 속성 `ID` 또는 *classname* `ID` 기본 키 속성으로 인식 됩니다.
- 라고 하는 경우 외래 키 속성으로는 속성을 해석  *&lt;탐색 속성 이름&gt;&lt;기본 키 속성 이름&gt;*  (예를 들어 `StudentID` 는 에대한`Student` 이후 탐색 속성에서 `Student` 엔터티의 기본 키가 `ID`). 외래 키 속성 수 또한 같은 이름 단순히 &lt;기본 키 속성 이름&gt; (예를 들어 `EnrollmentID` 이후는 `Enrollment` 엔터티의 기본 키가 `EnrollmentID`).

살펴본 규칙을 재정의할 수 있습니다. 예를 들어 지정한 테이블 이름을 복수화 됩니다 하지 않아야, 나중에 확인할 수 명시적으로 외래 키 속성으로 속성을 표시 하는 방법입니다. 규칙 및 재정의에 해당 하는 방법에 대해 자세히 알아봅니다는 [더 복잡 한 데이터 모델을 만드는](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md) 이 시리즈의 뒷부분에 나오는 자습서입니다. 규칙에 대 한 자세한 내용은 참조 [코드 첫 번째 규칙](https://msdn.microsoft.com/data/jj679962)합니다.

## <a name="summary"></a>요약

이제 Entity Framework 및 SQL Server Express LocalDB를 사용 하 여 저장 하 고 데이터를 표시 하는 간단한 응용 프로그램을 만들었습니다. 다음 자습서에서는 기본 CRUD 수행 하는 방법을 배우게 됩니다 (만들기, 읽기, 업데이트, 삭제) 작업입니다.

이 자습서를 연결 하는 방법 및 향상 될 수 있습니다에 의견을 남겨 주세요. 새 항목을 요청할 수도 있습니다 [Me 방법으로 코드 보기](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code)합니다.

다른 Entity Framework 리소스에 대 한 링크에서 확인할 수 있습니다 [ASP.NET 데이터 액세스-권장 리소스](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.

>[!div class="step-by-step"]
[다음](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)
