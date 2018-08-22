---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
title: Entity Framework 6 Code First MVC 5를 사용 하 여 시작 | Microsoft Docs
author: tdykstra
description: '이 자습서 시리즈의 최신 버전을 사용할 수 있습니다: ASP.NET Core 및 Visual Studio 2015를 사용 하 여 Entity Framework Core를 사용 하 여 시작 합니다. Contoso Universi...'
ms.author: riande
ms.date: 10/22/2015
ms.assetid: 00bc8b51-32ed-4fd3-9745-be4c2a9c1eaf
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 29004ec2271dbf77395f07e030533e23662b67c1
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41823859"
---
<a name="getting-started-with-entity-framework-6-code-first-using-mvc-5"></a>MVC 5를 사용하여 Entity Framework 6 Code First 시작
====================
[Tom Dykstra](https://github.com/tdykstra)

[완료 된 프로젝트를 다운로드](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8) 또는 [PDF 다운로드](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20Entity%20Framework%206%20Code%20First%20using%20MVC%205.pdf)

> > [!NOTE] 
> > 
> > 이 자습서 시리즈의 최신 버전을 사용할 수 있습니다: [ASP.NET Core 및 Visual Studio 2015를 사용 하 여 Entity Framework Core 시작](https://docs.asp.net/en/latest/data/ef-mvc/intro.html)합니다.
> 
> 
> Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 6 및 Visual Studio 2013을 사용 하 여 ASP.NET MVC 5 응용 프로그램을 만드는 방법을 보여 줍니다. 이 자습서에서는 Code First 워크플로 사용 합니다. Code First, Database First 및 Model First 중에서 선택 하는 방법에 대 한 자세한 내용은 [Entity Framework 개발 워크플로](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)합니다.
> 
> 샘플 응용 프로그램은 가상 Contoso University의 웹 사이트입니다. 학생 입학, 강좌 개설 및 강사 할당과 같은 기능이 있습니다. 이 자습서 시리즈에는 Contoso University 샘플 응용 프로그램을 빌드하는 방법을 설명 합니다. 할 수 있습니다 [완성된 된 응용 프로그램 다운로드](https://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8)합니다.
> 
> Mike Brind에서 변환 하는 Visual Basic 버전을 사용할 수: [MVC 5를 Visual Basic의 EF 6](http://www.mikesdotnetting.com/Article/241/MVC-5-with-EF-6-in-Visual-Basic-Creating-an-Entity-Framework-Data-Model) Mikesdotnetting 사이트입니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
> 
> 
> - [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - .NET 4.5
> - Entity Framework 6 (6.1.0 EntityFramework NuGet 패키지)
> - [Windows Azure SDK 2.2](https://go.microsoft.com/fwlink/p/?linkid=323510) (선택 사항)
>   
> 
> 자습서도 함께 해야 [Visual Studio 2013 Express for Web](https://www.microsoft.com/visualstudio/eng/2013-downloads#d-2013-express) 또는 Visual Studio 2012. 합니다 [VS 2012 버전의 Windows Azure SDK](https://go.microsoft.com/fwlink/p/?linkid=323511) Visual Studio 2012를 사용 하 여 Windows Azure 배포에 필요 합니다.
> 
> 
> ## <a name="tutorial-versions"></a>자습서 버전
> 
> 이 자습서의 이전 버전에 대 한 참조 [EF 4.1 / MVC 3 전자책](https://social.technet.microsoft.com/wiki/contents/articles/11608.e-book-gallery-for-microsoft-technologies.aspx#GettingStartedwiththeEntityFramework4.1usingASP.NETMVC) 하 고 [MVC 4를 사용 하 여 EF 5 시작](../../older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다.
> 
> ## <a name="questions-and-comments"></a>질문이 나 의견이 있으면
> 
> 이 자습서를 연결 하는 방법 및 새로운 개선할 수 있습니다 페이지의 맨 아래에 의견에서에 의견을 남겨 주세요. 에 자습서로 직접 관련 되지 않은 질문이 있을 수를 게시할 수 있습니다 합니다 [ASP.NET Entity Framework 포럼](https://forums.asp.net/1227.aspx)서 [Entity Framework 및 LINQ to Entities 포럼](https://social.msdn.microsoft.com/forums/adodotnetentityframework/threads/), 또는 [ StackOverflow.com](http://stackoverflow.com/)합니다.
> 
> 해결할 수 없는 문제를 실행 하는 경우 다운로드할 수 있는 완성 된 프로젝트에 코드를 비교 하 여 일반적으로 문제에 솔루션을 찾을 수 있습니다. 몇 가지 일반적인 오류 및 해결 하는 방법에 대 한 참조 [일반적인 오류 해결 방법 또는 해당 합니다.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)


## <a name="the-contoso-university-web-application"></a>Contoso University 웹 응용 프로그램

이 자습서에서 빌드하는 응용 프로그램은 간단한 대학 웹 사이트입니다.

사용자는 학생, 강좌 및 강사 정보를 보고 업데이트할 수 있습니다. 다음은 만들 몇 가지 화면입니다.

![Students_Index_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image1.png)

![학생 편집](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image2.png)

자습서가 Entity Framework를 사용하는 방법에 주로 초점을 맞출 수 있도록 이 사이트의 UI 스타일은 기본 제공 템플릿에서 생성된 내용에 가깝게 유지되었습니다.

## <a name="prerequisites"></a>전제 조건

참조 **소프트웨어 버전** 페이지의 맨 위에 있는 합니다. Entity Framework 6 아니므로 필수 구성 요소 자습서의 일부로 EF NuGet 패키지를 설치 합니다.

## <a name="create-an-mvc-web-application"></a>MVC 웹 응용 프로그램 만들기

Visual Studio를 열고 "ContosoUniversity" 라는 새 C# 웹 프로젝트를 만듭니다.

![New_project_dialog_box](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image3.png)

에 **새 ASP.NET 프로젝트** 대화 상자 선택 합니다 **MVC** 템플릿.

경우는 **클라우드에서 호스트** 확인란 합니다 **Microsoft Azure** 섹션을 선택 하면 확인란의 선택을 취소 합니다.

클릭 **인증 변경**합니다.

![New_project_dialog_box](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image4.png)

에 **인증 변경** 대화 상자에서 **인증 안 함**를 클릭 하 고 **확인**합니다. 이 자습서에 대 한 있습니다 없습니다 로그온 사용자에 게 요청 되거나 로그온 한 사용자에 따라 액세스를 제한 합니다.

![New_project_dialog_box](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image5.png)

새 ASP.NET 프로젝트 대화 상자에서 다시 **확인** 프로젝트를 만듭니다.

## <a name="set-up-the-site-style"></a>사이트 스타일 설정

몇 가지 간단한 변경 내용으로 사이트 메뉴, 레이아웃 및 홈 페이지를 설정합니다.

오픈 *Views\Shared\\_Layout.cshtml*를 다음과 같이 변경 하 고:

- "Contoso University"를 "My ASP.NET Application" 및 "Application name"로 변경 합니다.
- 학생, 강좌, 강사, 및 부서에 대 한 메뉴 항목을 추가 하 고 연락처 항목을 삭제 합니다.

변경 내용은 강조 표시되어 있습니다.

[!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample1.cshtml?highlight=6,19,24-27,38)]

*Views\Home\Index.cshtml*,이 응용 프로그램에 대 한 텍스트를 사용 하 여 ASP.NET 및 MVC에 대 한 텍스트를 바꾸려면 다음 코드로 파일의 내용을 바꿉니다.

[!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample2.cshtml)]

사이트를 실행 하려면 CTRL + F5 키를 누릅니다. 주 메뉴를 사용 하 여 홈 페이지가 표시 됩니다.

![Contoso_University_home_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image6.png)

## <a name="install-entity-framework-6"></a>Entity Framework 6를 설치 합니다.

**도구** 메뉴 **NuGet 패키지 관리자** 을 클릭 한 다음 **패키지 관리자 콘솔**합니다.

에 **패키지 관리자 콘솔** 창에 다음 명령을 입력 합니다.

`Install-Package EntityFramework`

![EF 설치](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image7.png)

이미지를 설치 하 고 6.0.0 보여주지만 NuGet은 설치 최신 (시험판 버전 제외), Entity Framework 6.1.1는 최신 자습서 업데이트를 기준으로 하는 합니다.

이 단계는이 자습서에는 수동으로 작업을 수행할 수 있지만 수행 하기 위해 자동으로 ASP.NET MVC 스 캐 폴딩 기능을 통해 몇 가지 단계 중 하나입니다. Entity Framework를 사용 하는 데 필요한 단계를 볼 수 있도록 수동으로 수행 하 고 있습니다. 스 캐 폴딩 MVC 컨트롤러 및 뷰를 만들려면 나중에 사용 합니다. 스 캐 폴딩 자동으로 EF NuGet 패키지를 설치할 데이터베이스 컨텍스트 클래스를 만들고 연결 문자열을 만들 수 있도록 것이 좋습니다. 이런 방식으로 작업을 수행 하는 준비 된 경우 수행 해야 하는 모든 경우 이러한 단계를 건너뛰고 엔터티 클래스를 만든 후에 MVC 컨트롤러를 스 캐 폴드

## <a name="create-the-data-model"></a>데이터 모델 만들기

다음으로 Contoso University 응용 프로그램에 대한 엔터티 클래스를 만듭니다. 다음 세 가지 엔터티를 사용 하 여 시작할 수 있습니다.

![Class_diagram](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image8.png)

`Student` 및 `Enrollment` 엔터티 간에 일대다 관계가 있으며 `Course` 및 `Enrollment` 엔터티 간에 일대다 관계가 있습니다. 즉, 학생은 개수에 관계 없이 강좌에 등록될 수 있으며 강좌는 등록된 학생이 여러 명일 수 있습니다.

다음 섹션에서 이러한 엔터티 각각에 대한 클래스를 만듭니다.

> [!NOTE]
> 이러한 엔터티 클래스의 모든 만들기를 완료 하기 전에 프로젝트를 컴파일할 하려고 하면 컴파일러 오류를 얻게 됩니다.


### <a name="the-student-entity"></a>학생 엔터티

![Student_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image9.png)

에 *모델* 폴더를 라는 클래스 파일을 만듭니다 *Student.cs* 템플릿 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample3.cs)]

`ID` 속성은 이 클래스에 해당하는 데이터베이스 테이블의 기본 키 열이 됩니다. 기본적으로 Entity Framework는 명명 된 속성을 해석 `ID` 나 *classname* `ID` 기본 키로 합니다.

합니다 `Enrollments` 속성을 *탐색 속성*합니다. 탐색 속성은 이 엔터티와 관련된 다른 엔터티를 포함합니다. 이 경우에 `Enrollments` 의 속성을 `Student` 엔터티 모두 보유할를 `Enrollment` 는 관련 된 엔터티 `Student` 엔터티. 즉, 경우를 지정 `Student` 데이터베이스의 행에는 관련 된 두 개의 `Enrollment` 행 (해당 학생의 기본 키를 포함 하는 행 값을 해당 `StudentID` 외래 키 열), 해당 `Student` 엔터티의 `Enrollments` 탐색 속성 이러한 두 사용 될 `Enrollment` 엔터티.

탐색 속성은 일반적으로 정의 됩니다 `virtual` 를 같은 특정 Entity Framework 기능을 취할 수 있습니다 *지연 로딩*합니다. (지연 로딩에 설명의 뒷부분에 나오는 합니다 [관련 데이터를 읽는](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) 이 시리즈의 뒷부분에 나오는 자습서입니다.)

탐색 속성이 여러 엔터티를 포함할 수 있는 경우(다대다 또는 일대다 관계로), 해당 형식은 `ICollection`와 같이 항목이 추가, 삭제 및 업데이트될 수 있는 목록이어야 합니다.

### <a name="the-enrollment-entity"></a>등록 엔터티

![Enrollment_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image10.png)

*Models* 폴더에서*Enrollment.cs*를 만들고 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample4.cs)]

`EnrollmentID` 속성을 기본 키 수,이 엔터티는 합니다 *classname* `ID` 대신 패턴 `ID` 에서 본 것 자체로 `Student` 엔터티. 일반적으로 하나의 패턴을 선택하고 이를 데이터 모델 전체에서 사용합니다. 여기에서 변형은 패턴 중 하나를 사용할 수 있음을 보여 줍니다. 자습서의 뒷부분에서 볼 수 방법을 `ID` 없이 `classname` 데이터 모델에서 상속을 구현 하기가 쉬워집니다.

합니다 `Grade` 속성은는 [enum](https://msdn.microsoft.com/data/hh859576.aspx)합니다. 후 물음표 합니다 `Grade` 형식 선언을 나타냅니다는 `Grade` 속성은 [nullable](https://msdn.microsoft.com/library/2cf62fcy.aspx)합니다. Null 인 등급은 0 등급과 다릅니다-null 성적 알려질 하거나 아직 할당 되지 않은 것을 의미 합니다.

`StudentID` 속성은 외래 키로, 해당 탐색 속성은 `Student`입니다. `Enrollment` 엔터티는 하나의 `Student` 엔터티와 연결되어 있으므로 속성은 단일 `Student` 엔터티만 포함할 수 있습니다(이전에 살펴본 여러 `Enrollment` 엔터티를 포함할 수 있는 `Student.Enrollments` 탐색 속성과 달리).

`CourseID` 속성은 외래 키로, 해당 탐색 속성은 `Course`입니다. `Enrollment` 엔터티는 하나의 `Course` 엔터티와 연결됩니다.

엔터티 프레임 워크 라고 하는 경우 외래 키 속성으로 속성을 해석 *&lt;탐색 속성 이름을&gt;&lt;기본 키 속성 이름&gt;* (예를 들어 `StudentID`에 대 한 합니다 `Student` 이후의 탐색 속성을 `Student` 엔터티의 기본 키가 `ID`). 외래 키 속성 수도 같은 이름 단순히 *&lt;기본 키 속성 이름&gt;* (예를 들어 `CourseID` 이므로 합니다 `Course` 엔터티의 기본 키가 `CourseID`).

### <a name="the-course-entity"></a>강좌 엔터티

![Course_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image11.png)

에 *모델* 폴더를 만듭니다 *Course.cs*, 템플릿 코드를 다음 코드로 바꾸어:

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample5.cs)]

`Enrollments` 속성은 탐색 속성입니다. `Course` 엔터티는 `Enrollment` 엔터티의 개수와 관련이 있을 수 있습니다.

클릭 합니다. 자세한 정보는 [DatabaseGenerated](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedattribute(v=vs.110).aspx) 이 시리즈의 자습서의 뒷부분에서 특성입니다. 기본적으로 이 특성을 통해 생성하는 데이터베이스를 갖는 대신 강좌에 대한 기본 키를 입력할 수 있습니다.

## <a name="create-the-database-context"></a>데이터베이스 컨텍스트 만들기

지정 된 데이터 모델에 대 한 Entity Framework 기능을 조정 하는 주 클래스는 합니다 *데이터베이스 컨텍스트* 클래스입니다. 이 클래스에서 파생 하 여 만든 합니다 [System.Data.Entity.DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx) 클래스입니다. 코드에서 데이터 모델에 포함되는 엔터티를 지정합니다. 특정 Entity Framework 동작을 사용자 지정할 수도 있습니다. 이 프로젝트에서 클래스 이름은 `SchoolContext`로 지정됩니다.

프로젝트를 마우스 오른쪽 단추로 클릭 ContosoUniversity 프로젝트에서 폴더를 만들려고 **솔루션 탐색기** 클릭 **추가**를 클릭 하 고 **새 폴더**합니다. 새 폴더의 이름을 *DAL* (데이터 액세스 계층)에 대 한 합니다. 해당 폴더에서 라는 새 클래스 파일을 만듭니다 *SchoolContext.cs*, 템플릿 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample6.cs)]

### <a name="specifying-entity-sets"></a>엔터티 집합 지정

이 코드에서는 한 [DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=VS.103).aspx) 각 엔터티 집합에 대 한 속성입니다. Entity Framework 용어에서는 *엔터티 집합* 일반적으로 데이터베이스 테이블에 해당와 *엔터티* 테이블의 행에 해당 합니다.

> [!NOTE] 
> 
> 생략 했습니다 수는 `DbSet<Enrollment>` 및 `DbSet<Course>` 문과 것은 동일 하 게 작동 합니다. `Student` 엔터티는 `Enrollment` 엔터티를 참조하고 `Enrollment` 엔터티는 `Course` 엔터티를 참조하기 때문에 Entity Framework는 이를 암시적으로 포함합니다.


### <a name="specifying-the-connection-string"></a>연결 문자열을 지정

(나중에 추가할 Web.config 파일에)이 표시 되는 연결 문자열의 이름은 생성자에 전달 됩니다.

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample7.cs?highlight=1)]

또한 Web.config 파일에 저장 된 이름 대신 연결 문자열 자체에 전달할 수 있습니다. 사용 하 여 데이터베이스를 지정 하기 위한 옵션에 대 한 자세한 내용은 참조 하세요. [Entity Framework-연결 모델과](https://msdn.microsoft.com/data/jj592674)합니다.

하나의 이름이 나 연결 문자열을 명시적으로 지정 하지 않으면, Entity Framework 연결 문자열 이름이 클래스 이름과 동일 이라고 가정 합니다. 이 예제에서 기본 연결 문자열 이름을 같게 됩니다. `SchoolContext`를 명시적으로 지정 하는 항목 동일 합니다.

### <a name="specifying-singular-table-names"></a>단 수 테이블 이름을 지정합니다.

합니다 `modelBuilder.Conventions.Remove` 문에서 [OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx) 메서드는 테이블 이름을 복수화 되에서 않도록 합니다. 데이터베이스에서 생성된 된 테이블 이름은이 수행 하지 않은 경우 `Students`, `Courses`, 및 `Enrollments`합니다. 테이블 이름 대신 됩니다 `Student`, `Course`, 및 `Enrollment`합니다. 개발자는 테이블 이름을 복수화할지 여부에 대해 동의하지 않습니다. 이 자습서에서는 단 수 형태를 사용 하지만 중요 한 점은 포함 하거나 코드이 줄을 생략 하 여 원하는 어떤 폼을 선택할 수 있습니다.

## <a name="set-up-ef-to-initialize-the-database-with-test-data"></a>테스트 데이터로 데이터베이스를 초기화 하려면 EF 설정

Entity Framework 수 자동으로 만듭니다 (또는 삭제 및 다시 만들기) 하는 응용 프로그램을 실행 하는 경우에 대 한 데이터베이스입니다. 이 작업은 응용 프로그램이 실행 될 때마다 또는 모델은 기존 데이터베이스와 동기화 하는 경우에 지정할 수 있습니다. 작성할 수도 있습니다는 `Seed` 메서드는 Entity Framework를 자동으로 테스트 데이터로 채우기 위해 데이터베이스를 만든 후 호출 합니다.

기본 동작은 해당 하지 않습니다 (있으며 모델 변경 되었으며이 데이터베이스가 이미 있는 경우 예외를 throw) 하는 경우에 데이터베이스를 만들 수 있습니다. 이 단원의 데이터베이스 삭제 후 모델이 변경 될 때마다 다시 생성을 지정 합니다. 데이터베이스를 삭제 하면 모든 데이터가 손실이 됩니다. 이 일반적으로 정상 개발 하는 동안 때문에 `Seed` 데이터베이스 다시 생성 되 고 다시 테스트 데이터 생성 하는 경우 메서드가 실행 됩니다. 그러나 프로덕션 환경에서 일반적으로 원하지 데이터베이스 스키마를 변경 해야 할 때마다 모든 데이터를 보호 합니다. 나중에 삭제 하 고 데이터베이스를 다시 작성 하는 대신 데이터베이스 스키마를 변경 하려면 Code First 마이그레이션을 사용 하 여 모델 변경 내용을 처리 하는 방법을 배웁니다.

DAL 폴더 라는 새 클래스 파일을 만듭니다 *SchoolInitializer.cs* 템플릿 코드를 바꾸고는  
다음 코드를 만들 때 데이터베이스 필요 하 고 새 데이터베이스에 테스트 데이터를 로드 합니다.

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample8.cs)]

`Seed` 메서드는 입력된 매개 변수로 데이터베이스 컨텍스트 개체를 사용 하 고 메서드에서 코드를 해당 개체를 사용 하 여 데이터베이스에 새 엔터티를 추가 합니다. 각 엔터티 형식에 대 한 코드는 새 엔터티 컬렉션을 만듭니다, 적절 한 추가 `DbSet` 속성 및 데이터베이스에 변경 내용 저장 합니다. 호출할 필요가 없습니다를 `SaveChanges` 엔터티의 각 그룹 뒤 메서드를으로 여기에서 수행 되지만 코드는 데이터베이스에 쓰는 동안 예외가 발생 하는 경우 문제의 소스를 찾을 수 있습니다 작업을 수행 합니다.

Entity Framework 이니셜라이저 클래스를 사용 하 게 요소를 추가 합니다 `entityFramework` 응용 프로그램에서 요소 *Web.config* 파일 (파일의 루트 프로젝트 폴더에서), 다음 예와에서 같이:

[!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample9.xml?highlight=2-6)]

합니다 `context type` 정규화 된 상황에 맞는 클래스 이름 및 어셈블리에 지정 및 `databaseinitializer type` 이니셜라이저 클래스와 있는 어셈블리의 정규화 된 이름을 지정 합니다. (이니셜라이저를 사용 하는 EF를 사용 하지 않으려는 경우에 특성을 설정할 수 있습니다 합니다 `context` 요소: `disableDatabaseInitialization="true"`.) 자세한 내용은 [Entity Framework-구성 파일 설정을](https://msdn.microsoft.com/data/jj556606)합니다.

이니셜라이저를 설정 하는 대신 합니다 *Web.config* 파일을 추가 하 여 코드에서 수행 하려면을 `Database.SetInitializer` 문을 `Application_Start` 에서 메서드를 *Global.asax.cs* 파일. 자세한 내용은 [Entity Framework Code first 데이터베이스 이니셜라이저 이해](http://www.codeguru.com/csharp/article.php/c19999/Understanding-Database-Initializers-in-Entity-Framework-Code-First.htm)합니다.

응용 프로그램은 이제 설정의 지정 된 실행에서 처음으로 데이터베이스에 액세스할 때 수 있도록 설정 합니다  
응용 프로그램에서 Entity Framework 모델 데이터베이스를 비교 합니다 (프로그램 `SchoolContext` 및 엔터티 클래스). 차이가 있으면 응용 프로그램을 삭제 하 고 다시 데이터베이스를 만듭니다.

> [!NOTE]
> 프로덕션 웹 서버에 응용 프로그램을 배포한 경우 제거 하거나 삭제 되 고 데이터베이스를 다시 생성 하는 코드를 사용 하지 않도록 설정 해야 합니다. 이 시리즈의 자습서의 뒷부분에서 할 수 있습니다.


## <a name="set-up-ef-to-use-a-sql-server-express-localdb-database"></a>EF는 SQL Server Express LocalDB 데이터베이스를 사용 하도록 설정

[LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx) SQL Server Express 데이터베이스 엔진의 경량 버전입니다. 설치 및 구성 하는 작업을 쉽게, 요청 시 시작 하며 사용자 모드에서 실행 됩니다. LocalDB 데이터베이스를 사용 하 여 작업할 수 있도록 하는 SQL Server Express의 특수 실행 모드에서 실행 *.mdf* 파일입니다. LocalDB 데이터베이스 파일에 넣을 수 있습니다 합니다 *앱\_데이터* 프로젝트를 사용 하 여 데이터베이스를 복사할 수 있게 되기를 원하는 경우 웹 프로젝트의 폴더입니다. SQL Server express 사용자 인스턴스 기능 또한 작업할 수 있습니다 *.mdf* 파일을 하지만 사용자 인스턴스 기능 사용 되지 않으면 따라서 LocalDB가 사용 하기 위한 권장 *.mdf* 파일입니다. Visual Studio 2012 및 이후 버전에서는 LocalDB Visual Studio를 사용 하 여 기본적으로 설치 됩니다.

일반적으로 SQL Server Express 프로덕션 웹 응용 프로그램에 대 한 사용 되지 않습니다. LocalDB 특히 권장 되지 않습니다 프로덕션 웹 응용 프로그램을 사용 하므로 IIS와 함께 작동 하도록 설계 되지는 않았습니다.

이 자습서에서는 LocalDB를 작업할 수 있습니다. 응용 프로그램을 엽니다 *Web.config* 파일을 추가 `connectionStrings` 요소 앞의 `appSettings` 요소를 다음 예제에서와 같이 합니다. (업데이트 해야 합니다 *Web.config* 루트 프로젝트 폴더의 파일입니다. 도 *Web.config* 파일은 합니다 *뷰* 하위 폴더를 업데이트할 필요가 없습니다.)

Visual Studio 2015를 사용 하는 경우에 기본 SQL Server 인스턴스 이름을 변경 되어 연결 문자열에 "v11.0"을 "MSSQLLocalDB"로 대체 합니다.

[!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample10.xml?highlight=1-3)]

Entity Framework는 명명 된 LocalDB 데이터베이스를 사용 하 여 추가한 다음 연결 문자열 지정 *ContosoUniversity1.mdf*합니다. (데이터베이스가 아직 존재 하지 않으면 EF에서 만듭니다.) 데이터베이스를 만들 수 하려는 경우에 *앱\_데이터* 폴더를 추가할 수 있습니다 `AttachDBFilename=|DataDirectory|\ContosoUniversity1.mdf` 연결 문자열에 있습니다. 연결 문자열에 대 한 자세한 내용은 참조 하세요. [ASP.NET 웹 응용 프로그램에 대 한 SQL Server 연결 문자열](https://msdn.microsoft.com/library/jj653752.aspx)합니다.

연결 문자열에 실제로 없는 합니다 *Web.config* 파일입니다. 연결 문자열을 지정 하지 않으면 Entity Framework는 컨텍스트 클래스에 따라 하나 기본값을 사용 합니다. 자세한 내용은 [Code First 새 데이터베이스로](https://msdn.microsoft.com/data/jj193542)합니다.

## <a name="creating-a-student-controller-and-views"></a>학생 컨트롤러 및 뷰 만들기

이제 데이터를 표시할 웹 페이지를 만듭니다 및 데이터를 요청 프로세스를 자동으로 트리거합니다.  
데이터베이스 생성 합니다. 새 컨트롤러를 만들어 시작할 수 있습니다. 하지만 그렇게 하기 전에 모델 및 상황에 맞는 클래스를 MVC 컨트롤러 스 캐 폴딩 가능 프로젝트를 빌드합니다.

1. 마우스 오른쪽 단추로 클릭 합니다 **컨트롤러** 폴더에 **솔루션 탐색기**를 선택 **추가**를 클릭 하 고 **새 스 캐 폴드 된 항목**합니다.
2. 에 **스 캐 폴드 추가** 대화 상자에서 **Entity Framework를 사용 하 여 뷰를 사용 하 여 MVC 5 컨트롤러**합니다.

     ![스 캐 폴드 추가](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image12.png)
3. 컨트롤러 추가 대화 상자에서 다음 옵션 선택 하 고 클릭 **추가**:

   - 모델 클래스: **학생 (ContosoUniversity.Models)** 합니다. (드롭다운 목록에서이 옵션을 보이지 않으면 프로젝트를 빌드 및 다시 시도 하십시오.)
   - 데이터 컨텍스트 클래스: **SchoolContext (ContosoUniversity.DAL)** 합니다.
   - 컨트롤러 이름: **StudentController** (없습니다 StudentsController).
   - 다른 필드에 대 한 기본값을 그대로 둡니다.

     ![Add_Controller_dialog_box_for_Student_controller](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image13.png)

     클릭 하면 **추가**를 scaffolder StudentController.cs 파일 및 컨트롤러를 사용 하는 뷰 (.cshtml 파일)의 집합을 만듭니다. 또한 일부 추가 기능을 스 캐 폴더의 Entity Framework를 사용 하는 프로젝트를 만들 때에 나중에 수: 방금 첫 번째 모델 클래스를 만들고, 연결 문자열을 만들지 한 다음는 **컨트롤러 추가** 상자는 새 컨텍스트 클래스를 지정 합니다. 캐 만들어집니다 프로그램 `DbContext` 뿐만 아니라 컨트롤러 및 뷰 클래스 및 연결 문자열입니다.
4. Visual Studio가 열립니다는 *Controllers\StudentController.cs* 파일입니다. 클래스 변수를 만든 데이터베이스 컨텍스트 개체를 인스턴스화하는 것이 표시 됩니다.

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

     `Index` 동작 메서드가의 학생 들의 목록을 가져옵니다 합니다 *학생* 엔터티 집합 참조 하 여는 `Students` 데이터베이스 컨텍스트 인스턴스의 속성:

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

     합니다 *Student\Index.cshtml* 보기 테이블의이 목록에 표시 됩니다.

     [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample13.cshtml)]
5. Ctrl+F5를 눌러 프로젝트를 실행합니다. ("섀도 복사본을 만들 수 없습니다" 오류가 발생할 경우 브라우저를 닫고 다시 시도 하십시오.)

     클릭 합니다 **학생** 테스트 데이터를 보려면 탭은는 `Seed` 삽입 하는 메서드. 폭에 따라 브라우저 창을 인 상위 주소 표시줄에 학생 탭 링크가 표시 또는 링크를 보기 위해 오른쪽 위 모서리를 클릭 해야 합니다.

     ![메뉴 단추](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image14.png)

     ![학생 인덱스 페이지](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image15.png)

## <a name="view-the-database"></a>데이터베이스 보기

학생 페이지를 실행 하 고 응용 프로그램 데이터베이스에 액세스 하려고 한 경우 EF는 데이터베이스가 없는 하 고 하나를 만들었습니다, 다음 실행 데이터를 사용 하 여 데이터베이스를 채우는 데 seed 메서드를 살펴보았습니다.

사용할 수 있습니다 **서버 탐색기** 하거나 **SQL Server 개체 탐색기** (SSOX) Visual Studio에서 데이터베이스를 봅니다. 이 자습서를 사용 하 여 **서버 탐색기**합니다. (버전 Visual Studio Express 2013 이전의 **서버 탐색기** 이라고 **데이터베이스 탐색기**.)

1. 브라우저를 닫습니다.
2. **서버 탐색기**, 확장 **데이터 연결**를 확장 **학교 컨텍스트 (ContosoUniversity)** 를 차례로 확장 **테이블** 보려는 새 데이터베이스의 테이블입니다.

    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image16.png)
3. 마우스 오른쪽 단추로 클릭 합니다 **학생** 테이블을 클릭 **테이블 데이터 표시** 생성 된 열 및 테이블에 삽입 된 행을 볼 수 있습니다.

    ![Student 테이블](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image17.png)
4. 닫기 합니다 **서버 탐색기** 연결 합니다.

합니다 *ContosoUniversity1.mdf* 하 고 *.ldf* 데이터베이스 파일이 있는 `C:\Users\<yourusername>` 폴더입니다.

사용 중 이므로 합니다 `DropCreateDatabaseIfModelChanges` 이니셜라이저를 만들 수 있습니다 이제 변경은 `Student` 클래스 다시 응용 프로그램을 실행 하 고 데이터베이스는 자동으로 변경 내용에 맞도록으로 다시 생성 됩니다. 예를 들어, 추가 하는 경우는 `EmailAddress` 속성을 `Student` 클래스, 학생 페이지를 다시 실행 한 다음 표에서 다시를 살펴보려면 보면 새 `EmailAddress` 열입니다.

## <a name="conventions"></a>규칙

사용 했기 때문에 전체 데이터베이스를 만들 수를 Entity Framework에서 작성 해야 했던 코드의 양을 최소화 됩니다 *규칙*, 또는 Entity Framework에서 만드는 가정 합니다. 그 중 일부 메모해 두어야 이미 또는 되 고 인식 없이 사용 되었습니다.

- 엔터티 클래스 이름의 복수화 양식은 테이블 이름으로 사용 됩니다.
- 엔터티 속성 이름은 열 이름에 사용됩니다.
- 명명 된 엔터티 속성 `ID` 나 *classname* `ID` 기본 키 속성으로 인식 됩니다.
- 라고 하는 경우 외래 키 속성으로는 속성을 해석 *&lt;탐색 속성 이름을&gt;&lt;기본 키 속성 이름&gt;* (예를 들어 `StudentID` 합니다 에대한`Student` 이후의 탐색 속성을 `Student` 엔터티의 기본 키가 `ID`). 외래 키 속성 수도 같은 이름 단순히 &lt;기본 키 속성 이름&gt; (예를 들어 `EnrollmentID` 되므로 합니다 `Enrollment` 엔터티의 기본 키가 `EnrollmentID`).

규칙을 재정의할 수 있음을 확인 했습니다. 예를 들어 지정한 테이블 이름을 복수화 하지 않아야, 나중에 볼 수 명시적으로 외래 키 속성으로 속성을 표시 하는 방법입니다. 규칙 및 재정의에 해당 하는 방법을 자세히 알아봅니다 합니다 [더 복잡 한 데이터 모델을 만드는](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md) 이 시리즈의 뒷부분에 나오는 자습서입니다. 규칙에 대 한 자세한 내용은 참조 하세요. [코드의 첫 번째 규칙](https://msdn.microsoft.com/data/jj679962)합니다.

## <a name="summary"></a>요약

이제 Entity Framework 및 SQL Server Express LocalDB를 사용 하 여 저장 하 고 데이터를 표시 하는 간단한 응용 프로그램을 만들었습니다. 다음 자습서의 기본 CRUD를 수행 하는 방법을 알아봅니다 (만들기, 읽기, 업데이트, 삭제) 작업입니다.

이 자습서를 연결 하는 방법을 개선할 수 것에 의견을 남겨 주세요. 새 항목을 요청할 수도 있습니다 [표시 코드 사용 방법 보기](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code)합니다.

다른 Entity Framework 리소스에 대 한 링크에서 찾을 수 있습니다 [ASP.NET 데이터 액세스-권장 리소스](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.

> [!div class="step-by-step"]
> [다음](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)
