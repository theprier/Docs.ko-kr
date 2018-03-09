---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
title: "ASP.NET MVC 응용 프로그램 (1 / 10)에 대 한 Entity Framework 데이터 모델 만들기 | Microsoft Docs"
author: tdykstra
description: "이 자습서 시리즈의 최신 버전은 Visual Studio 2013, Entity Framework 6 및 MVC 5에 사용할 수 있습니다. Contoso 대학 샘플 웹 응용 프로그램 de 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/30/2013
ms.topic: article
ms.assetid: 4ba029b6-ee7c-4e45-a0e7-b703c37e5d9a
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 8c9971ccc70cb4b966abb64086b1b5420fc6c72a
ms.sourcegitcommit: 53ee14b9c8200f44705d8997c3619fa874192d45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2018
---
<a name="creating-an-entity-framework-data-model-for-an-aspnet-mvc-application-1-of-10"></a>ASP.NET MVC 응용 프로그램 (1 / 10)에 대 한 Entity Framework 데이터 모델 만들기
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

[완료 된 프로젝트를 다운로드 합니다.](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> > [!NOTE] 
> > 
> > A [이 자습서 시리즈의 최신 버전](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) Visual Studio 2013, Entity Framework 6 MVC 5 숫자에 사용할 수 있습니다.
> 
> 
> Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 5 및 Visual Studio 2012를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다. 샘플 응용 프로그램은 가상 Contoso University의 웹 사이트입니다. 학생 입학, 강좌 개설 및 강사 할당과 같은 기능이 있습니다. 이 자습서 시리즈 Contoso 대학 샘플 응용 프로그램을 작성 하는 방법에 설명 합니다. 있습니다 수 [완성 된 응용 프로그램 다운로드](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)합니다.
> 
> ## <a name="code-first"></a>Code First
> 
> 세 가지 방법으로 데이터 Entity Framework에서 사용할 수 있습니다: *Database First*, *Model First*, 및 *Code First*합니다. 첫 번째 코드에 대 한이 자습서가입니다. 이러한 워크플로 지침 간의 차이점에 대 한 사용자 시나리오에 가장 적합 한 선택 하는 방법에 정보를 참조 하십시오. [Entity Framework 개발 워크플로에](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)합니다.
> 
> ## <a name="mvc"></a>MVC
> 
> 샘플 응용 프로그램 기반 [ASP.NET MVC](../../../index.md)합니다. ASP.NET Web Forms 모델을 사용 하려는 경우 참조는 [모델 바인딩 및 Web Forms](../../../../web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data.md) 자습서 시리즈 및 [ASP.NET 데이터 액세스 콘텐츠 맵](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.
> 
> ## <a name="software-versions"></a>소프트웨어 버전
> 
> | **이 자습서에 표시** | **또한에 사용할 수** |
> | --- | --- |
> | Windows 8 | Windows 7 |
> | Visual Studio 2012 | Visual Studio 2012 Express for Web입니다. VS 2012 또는 VS 2012 Express for Web 아직 없는 경우 자동으로 Windows Azure SDK를 통해 설치 됩니다. Visual Studio 2013에는 작동 하지만,이 자습서를 거치지 않았으며 되며 일부 선택한 메뉴 및 대화 상자 서로 다릅니다. [VS 2013 버전의 Windows Azure SDK](https://go.microsoft.com/fwlink/p/?linkid=323510) Windows Azure 배포에 필요 합니다. |
> | .NET 4.5 | 표시 된 기능의 대부분.NET 4에서 작동 하지만 일부 되지 않습니다. 예를 들어, EF에서 enum 지원.NET 4.5를 필요합니다. |
> | Entity Framework 5 |  |
> | [Windows Azure SDK 2.1](https://go.microsoft.com/fwlink/p/?linkid=323511) | Windows Azure 배포 단계를 건너뛰면 SDK 필요는 없습니다. 새 버전의 SDK가 출시 되 면 링크에서 최신 버전을 설치 합니다. 이 경우 새 UI 및 기능에는 명령의 일부를 조정 해야 합니다. |
> 
> ## <a name="questions"></a>질문
> 
> 자습서를 직접 관련 되지 않는 질문 해야 하도록를 게시할 수 있습니다는 [ASP.NET Entity Framework 포럼](https://forums.asp.net/1227.aspx), [Entity Framework와 LINQ to Entities 포럼](https://social.msdn.microsoft.com/forums/adodotnetentityframework/threads/), 또는 [ StackOverflow.com](http://stackoverflow.com/)합니다.
> 
> ## <a name="acknowledgments"></a>감사의 글
> 
> 참조에 대 한 일련의 마지막 자습서 [승인 및 VB에 대 한 메모](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#acknowledgments)합니다.
> 
> ## <a name="original-version-of-the-tutorial"></a>자습서의 원래 버전
> 
> 자습서의 원래 버전은 제공 된 [EF 4.1 / MVC 3 전자책](https://social.technet.microsoft.com/wiki/contents/articles/11608.e-book-gallery-for-microsoft-technologies.aspx#GettingStartedwiththeEntityFramework4.1usingASP.NETMVC)합니다.


## <a name="the-contoso-university-web-application"></a>Contoso 대학 웹 응용 프로그램

이 자습서에서 빌드하는 응용 프로그램은 간단한 대학 웹 사이트입니다.

사용자는 학생, 강좌 및 강사 정보를 보고 업데이트할 수 있습니다. 다음은 만들 몇 가지 화면입니다.

![Students_Index_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image1.png)

![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image2.png)

자습서가 Entity Framework를 사용하는 방법에 주로 초점을 맞출 수 있도록 이 사이트의 UI 스타일은 기본 제공 템플릿에서 생성된 내용에 가깝게 유지되었습니다.

## <a name="prerequisites"></a>전제 조건

사용 하는 경우 directions와이 자습서의 스크린 샷을 가정 [Visual Studio 2012](https://www.microsoft.com/visualstudio/eng/downloads) 또는 [Visual Studio 2012 Express for Web](https://go.microsoft.com/fwlink/?LinkID=275131), 최신 업데이트 및 Azure SDK for.NET 7 월을 기준으로 설치 2013입니다. 다음 링크를 통해이 모든를 얻을 수 있습니다.

[Azure SDK for.NET (Visual Studio 2012)](https://go.microsoft.com/fwlink/?LinkId=254364)

Visual Studio가 설치 되어 있는 경우 위의 링크 모든 누락 된 구성 요소가 설치 됩니다. Visual Studio가 없는 경우 링크 Visual Studio 2012 Express for Web을 설치 합니다. Visual Studio 2013을 사용할 수 있지만 필요한 절차와 화면 중 일부 달라 집니다.

## <a name="create-an-mvc-web-application"></a>MVC 웹 응용 프로그램 만들기

Visual Studio를 열고 새 C# 프로젝트 만들기 "ContosoUniversity"를 사용 하 여 명명 된 **ASP.NET MVC 4 웹 응용 프로그램** 서식 파일입니다. 대상 확인 **.NET Framework 4.5** (사용 하 게 [ `enum` 속성](https://msdn.microsoft.com/data/hh859576.aspx),.NET 4.5를 필요로 하).

![New_project_dialog_box](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image3.png)

에 **새 ASP.NET MVC 4 프로젝트** 대화 상자 선택은 **인터넷 응용 프로그램** 서식 파일입니다.

둡니다는 **Razor** 보기 엔진을 선택 하 고 유지는 **단위 테스트 프로젝트 만들기** 확인란의 선택을 취소 합니다.

**확인**을 클릭합니다.

![Project_template_options](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image4.png)

## <a name="set-up-the-site-style"></a>사이트 스타일 설정

몇 가지 간단한 변경 내용으로 사이트 메뉴, 레이아웃 및 홈 페이지를 설정합니다.

열기 *Views\Shared\\_Layout.cshtml*, 파일의 내용을 다음 코드로 바꿉니다. 변경 내용은 강조 표시되어 있습니다.

[!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample1.cshtml?highlight=5,15,25-28,43)]

이 코드로 다음이 변경됩니다.

- "Contoso 대학"으로 "내 ASP.NET MVC 응용 프로그램" 및 "사용자 로고는 여기"의 템플릿 인스턴스를 바꿉니다.
- 이 자습서의 뒷부분에 나오는 사용할 수는 몇 가지 작업 링크를 추가 합니다.

*Views\Home\Index.cshtml*, ASP.NET 및 MVC에 대 한 템플릿 단락을 제거 하려면 다음 코드는 파일의 내용을 바꿉니다.

[!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample2.cshtml)]

*Controllers\HomeController.cs*에 대 한 값을 변경 `ViewBag.Message` 에 `Index` "시작 Contoso 대학!"에서 다음 예제에서와 같이 동작 메서드의:

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample3.cs?highlight=3)]

사이트를 실행 하려면 CTRL + f 5를 누릅니다. 주 메뉴와 홈 페이지가 나타납니다.

![Contoso_University_home_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image5.png)

## <a name="create-the-data-model"></a>데이터 모델 만들기

다음으로 Contoso University 응용 프로그램에 대한 엔터티 클래스를 만듭니다. 다음 세 가지 엔터티부터 시작 합니다.

![Class_diagram](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image6.png)

`Student` 및 `Enrollment` 엔터티 간에 일대다 관계가 있으며 `Course` 및 `Enrollment` 엔터티 간에 일대다 관계가 있습니다. 즉, 학생은 개수에 관계 없이 강좌에 등록될 수 있으며 강좌는 등록된 학생이 여러 명일 수 있습니다.

다음 섹션에서 이러한 엔터티 각각에 대한 클래스를 만듭니다.

> [!NOTE]
> 이러한 엔터티 클래스의 모든 만들기를 완료 하기 전에 프로젝트를 컴파일할 하려고 하면 컴파일러 오류가 발생 합니다.


### <a name="the-student-entity"></a>학생 엔터티

![Student_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image7.png)

에 *모델* 폴더를 만들 *Student.cs* 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample4.cs)]

`StudentID` 속성은 이 클래스에 해당하는 데이터베이스 테이블의 기본 키 열이 됩니다. Entity Framework를 기본적으로 명명 된 속성을 해석 `ID` 또는 *classname* `ID` 기본 키로 합니다.

`Enrollments` 속성은 한 *탐색 속성*합니다. 탐색 속성은 이 엔터티와 관련된 다른 엔터티를 포함합니다. 이 경우에 `Enrollments` 속성은 `Student` 의 모든 엔터티를 포함할는 `Enrollment` 엔터티는 관련 된 `Student` 엔터티. 즉, 하는 경우는 주어진 `Student` 데이터베이스의 행에는 관련 된 두 개의 `Enrollment` 행 (해당 학생의 기본 키를 포함 하는 행에서 값을 해당 `StudentID` 외래 키 열), 해당 `Student` 엔터티의 `Enrollments` 탐색 속성 이 두 들어갑니다 `Enrollment` 엔터티.

탐색 속성은 일반적으로 정의 `virtual` 특정 Entity Framework 기능을 이용와 같은 많이 있도록 *한 지연 로딩이*합니다. (한 지연 로딩이 설명 되어 있습니다의 뒷부분에 나오는 [관련 데이터를 읽는](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) 이 시리즈의 뒷부분에 나오는 자습서입니다.

탐색 속성이 여러 엔터티를 포함할 수 있는 경우(다대다 또는 일대다 관계로), 해당 형식은 `ICollection`와 같이 항목이 추가, 삭제 및 업데이트될 수 있는 목록이어야 합니다.

### <a name="the-enrollment-entity"></a>등록 엔터티

![Enrollment_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image8.png)

*Models* 폴더에서*Enrollment.cs*를 만들고 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample5.cs)]

등급 속성은 한 [enum](https://msdn.microsoft.com/data/hh859576.aspx)합니다. 후 물음표는 `Grade` 형식 선언을 나타냅니다는 `Grade` 속성은 [nullable](https://msdn.microsoft.com/library/2cf62fcy.aspx)합니다. Null이 등급은 0 개 등급 다릅니다-의미 하는 등급 알려진 또는 아직 할당 되지 않았습니다.

`StudentID` 속성은 외래 키로, 해당 탐색 속성은 `Student`입니다. `Enrollment` 엔터티는 하나의 `Student` 엔터티와 연결되어 있으므로 속성은 단일 `Student` 엔터티만 포함할 수 있습니다(이전에 살펴본 여러 `Enrollment` 엔터티를 포함할 수 있는 `Student.Enrollments` 탐색 속성과 달리).

`CourseID` 속성은 외래 키로, 해당 탐색 속성은 `Course`입니다. `Enrollment` 엔터티는 하나의 `Course` 엔터티와 연결됩니다.

### <a name="the-course-entity"></a>과정 엔터티

![Course_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image9.png)

에 *모델* 폴더를 만들 *Course.cs*, 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample6.cs)]

`Enrollments` 속성은 탐색 속성입니다. `Course` 엔터티는 `Enrollment` 엔터티의 개수와 관련이 있을 수 있습니다.

에 대 한 내용은 라고는 [[DatabaseGenerated](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedattribute(v=vs.110).aspx)([databasegeneratedoption입니다](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedoption(v=vs.95).aspx)합니다. 다음 자습서의 특성 없음)]입니다. 기본적으로 이 특성을 통해 생성하는 데이터베이스를 갖는 대신 강좌에 대한 기본 키를 입력할 수 있습니다.

## <a name="create-the-database-context"></a>데이터베이스 컨텍스트 만들기

지정된 된 데이터 모델에 대 한 Entity Framework 기능을 조정 하는 기본 클래스는는 *데이터베이스 컨텍스트* 클래스입니다. 이 클래스에서 파생 시켜 만들는 [System.Data.Entity.DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx) 클래스입니다. 코드에서 데이터 모델에 포함되는 엔터티를 지정합니다. 특정 Entity Framework 동작을 사용자 지정할 수도 있습니다. 이 프로젝트에서 클래스 이름은 `SchoolContext`로 지정됩니다.

라는 폴더를 만듭니다 *DAL* (데이터 액세스 계층)에 대 한 합니다. 해당 폴더에 라는 새 클래스 파일을 만들 *SchoolContext.cs*, 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample7.cs)]

이 코드에서는 [DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=VS.103).aspx) 각 엔터티 집합에 대 한 속성입니다. Entity Framework 용어에서는 *엔터티 집합* 일반적으로 데이터베이스 테이블에 해당 및 *엔터티* 테이블의 행에 해당 합니다.

`modelBuilder.Conventions.Remove` 의 문에서 [OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx) 복수화 되 고에서 테이블 이름을 수 없습니다. 이렇게 하지 않은 생성된 된 테이블 이름이 `Students`, `Courses`, 및 `Enrollments`합니다. 테이블 이름이 됩니다 대신 `Student`, `Course`, 및 `Enrollment`합니다. 개발자는 테이블 이름을 복수화할지 여부에 대해 동의하지 않습니다. 이 자습서에서는 단 수 형태를 사용 하지만 중요 한 점은 포함 하거나 코드이 줄을 생략 하 여 원하는 어떤 폼을 선택할 수 있습니다.

## <a name="sql-server-express-localdb"></a>SQL Server Express LocalDB

[LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx) 는 SQL Server Express 데이터베이스 엔진의 요청에 따라 시작 하 고 사용자 모드에서 실행 하는 경량 버전입니다. LocalDB 데이터베이스도 작업할 수 있도록 SQL Server Express의 특수 실행 모드에서 실행 *.mdf* 파일입니다. LocalDB 데이터베이스 파일에 보관 되는 일반적으로 *앱\_데이터* 웹 프로젝트의 폴더입니다. SQL Server express 사용자 인스턴스 기능 또한 작업할 수 있습니다 *.mdf* 은 사용자 인스턴스 기능은 사용 되지 않습니다; 따라서 LocalDB를 사용 하기 위한 좋습니다 *.mdf* 파일입니다.

일반적으로 SQL Server Express 프로덕션 웹 응용 프로그램에 대 한 사용 되지 않습니다. LocalDB 특히 권장 되지 않습니다 웹 응용 프로그램의 프로덕션 사용을 위해 하므로 IIS와 함께 작동 하도록 설계 되지 않았습니다.

Visual Studio 2012 이상 버전에서 LocalDB는 Visual Studio를 사용 하 여 기본적으로 설치 됩니다. Visual Studio 2010 및 이전 버전 Visual Studio;와 함께 기본적으로 설치 됩니다 (LocalDB) 없이 SQL Server Express Visual Studio 2010을 사용 하는 경우 수동으로 설치 해야 합니다.

이 자습서에서는 다루게 LocalDB 데이터베이스에 저장할 수 있도록는 *앱\_데이터* 폴더는 *.mdf* 파일입니다. 루트를 열고 *Web.config* 파일을 추가 하 여 새 연결 문자열은 `connectionStrings` 컬렉션, 다음 예제와 같이 합니다. (업데이트 해야는 *Web.config* 루트 프로젝트 폴더의 파일입니다. 또한는 *Web.config* 중인 파일의 *뷰* 업데이트할 필요가 없는 하위 폴더입니다.)

[!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample8.xml)]

기본적으로 이름이 연결 문자열에 대 한 Entity Framework 찾습니다는 `DbContext` 클래스 (`SchoolContext` 이 프로젝트에 대 한). 명명 된 LocalDB 데이터베이스를 지정 하는 사용자가 추가한 연결 문자열 *ContosoUniversity.mdf* 에 *앱\_데이터* 폴더입니다. 자세한 내용은 참조 [ASP.NET 웹 응용 프로그램에 대 한 SQL Server 연결 문자열](https://msdn.microsoft.com/library/jj653752.aspx)합니다.

실제로 연결 문자열을 지정할 필요가 없습니다. 연결 문자열을 지정 하지 않으면 Entity Framework에서 만듭니다. 그러나 데이터베이스에 없을 수도 *앱\_데이터* 응용 프로그램의 폴더입니다. 데이터베이스를 만들 위치에 대 한 정보를 참조 하십시오. [Code First를 새 데이터베이스로](https://msdn.microsoft.com/data/jj193542)합니다.

`connectionStrings` 컬렉션 이라는 연결 문자열에 `DefaultConnection` 멤버 자격 데이터베이스에 사용 됩니다. 이 자습서에서는 멤버 자격 데이터베이스를 사용 되지 않습니다. 유일한 차이점은 두 개의 연결 문자열에는 데이터베이스 이름 및 name 특성 값입니다.

## <a name="set-up-and-execute-a-code-first-migration"></a>설정 하 고 실행 코드의 첫 번째 마이그레이션

를 처음 시작 하면 응용 프로그램을 개발 하는 경우 데이터 모델 변경 내용을 자주 고 될 때마다 모델 변경 내용을 가져오는 데이터베이스와 동기화 합니다. 자동으로 삭제 하 고 데이터 모델을 변경할 때마다 데이터베이스를 다시 만드는 Entity Framework를 구성할 수 있습니다. 테스트 데이터를 쉽게 다시 만들 수 있지만 일반적으로 데이터베이스를 삭제 하지 않고 데이터베이스 스키마를 업데이트 하려면 프로덕션 환경에 배포한 후에 개발 초기에 문제가 되지 않습니다. 마이그레이션 기능 코드 첫 번째 데이터베이스를 삭제 하 고 다시 만들기를 업데이트할 수 있습니다. 새 프로젝트의 개발 주기의 초기 단계에서 사용 하려는 [DropCreateDatabaseIfModelChanges](https://msdn.microsoft.com/library/gg679604(v=vs.103).aspx) 모델 변경 될 때마다을 삭제, 다시 만들고 데이터베이스를 다시 시드해야 합니다. 응용 프로그램을 배포할 준비가 발생 하나 마이그레이션 접근 방식으로 변환할 수 있습니다. 이 자습서에 대 한 마이그레이션만 사용 합니다. 자세한 내용은 참조 [Code First 마이그레이션을](https://msdn.microsoft.com/data/jj591621) 및 [마이그레이션 동영상 가이드 시리즈](https://blogs.msdn.com/b/adonet/archive/2014/03/12/migrations-screencast-series.aspx)합니다.

### <a name="enable-code-first-migrations"></a>Code First 마이그레이션을 사용 하도록 설정

1. **도구** 메뉴를 클릭 하 여 **라이브러리 패키지 관리자** 차례로 **패키지 관리자 콘솔**합니다.

    ![Selecting_Package_Manager_Console](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image10.png)
2. 에 `PM>` 프롬프트에 다음 명령을 입력 합니다.

    [!code-powershell[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample9.ps1)]

    ![enable-migrations 명령](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image11.png)

    이 명령은 만듭니다는 *마이그레이션* 해당 폴더에 배치 하며 ContosoUniversity 프로젝트 폴더는 *Configuration.cs* 마이그레이션을 구성 하는 편집할 수 있는 파일입니다.

    ![Migrations 폴더](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image12.png)

    `Configuration` 클래스를 포함 한 `Seed` 메서드는 데이터베이스를 만들 때 데이터 모델 변경 후 업데이트 될 때마다 호출 하 합니다.

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample10.cs)]

    이렇게 함으로써 `Seed` 메서드는 Code First으로 작성 하거나 업데이트 한 후 데이터베이스에 테스트 데이터를 삽입할 수 있습니다.

### <a name="set-up-the-seed-method"></a>Seed 메서드 설정

[시드](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) Code First 마이그레이션을 데이터베이스를 만들 때 및 최신 마이그레이션을 위해 데이터베이스를 업데이트 될 때마다 메서드를 실행 합니다. Seed 메서드의 목적은 응용 프로그램 하기 전에 테이블에 데이터를 삽입할 수 있도록 처음으로 데이터베이스에 액세스 합니다.

첫 번째 코드의 이전 버전에서 마이그레이션 전에 이었습니다 `Seed` 개발 하는 동안 모델 바뀔 때마다 데이터베이스에서 발생 완전히 삭제 하 고 처음부터 다시 생성 하기 때문에 테스트 데이터를 삽입 하는 메서드. Code First 마이그레이션을, 데이터베이스 변경 된 후 데이터는 유지 하는 테스트의 테스트 데이터를 포함 하므로 [시드](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) 일반적으로 메서드는 필요 없습니다. 않도록 실제로 `Seed` 합니다 사용할 경우 마이그레이션에 데이터베이스를 프로덕션에 배포 하기 때문에 테스트 데이터를 삽입 하는 메서드는 `Seed` 메서드가 프로덕션 환경에서 실행 됩니다. 원하는 경우에 `Seed` 메서드를 프로덕션 환경에 삽입할 데이터만 데이터베이스에 삽입 합니다. 데이터베이스의 실제 부서 이름을 포함 하도록 할 수는 예를 들어는 `Department` 응용 프로그램이 프로덕션 환경에서 사용할 수 있을 때 테이블입니다.

이 자습서를 사용 하기 마이그레이션 배포에 대 한 하지만 `Seed` 메서드는 테스트 데이터 삽입 그래도 보다 쉽게 응용 프로그램 기능을 수동으로 많은 데이터를 삽입 하지 않고도 어떻게 작동 하는지 확인할 수 있도록 합니다.

1. 내용을 대체는 *Configuration.cs* 가 새 데이터베이스에 테스트 데이터를 로드 하는 다음 코드로 파일입니다. 

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

    [시드](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) 메서드가 데이터베이스 컨텍스트 개체를 입력된 매개 변수로 하 고는 메서드의 코드에서에서 해당 개체를 사용 하 여 데이터베이스에 새 엔터티를 추가 합니다. 각 엔터티 형식에 대 한 새 엔터티 컬렉션을 만듭니다을 코드에 적절 한 추가 [DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx) 속성을 선택한 다음 변경 내용이 데이터베이스에 저장 합니다. 호출할 필요가 없습니다는 [SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx) 엔터티의 각 그룹 뒤 메서드, 여기서 단원의 하지만 코드는 데이터베이스에 쓰는 동안 예외가 발생 하면 문제의 원인의 찾을 수 있습니다 작업을 수행 합니다.

    사용 하 여 일부 데이터를 삽입 하는 문에 [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) 메서드는 "upsert" 작업을 수행 하도록 합니다. 때문에 `Seed` 모든 마이그레이션을 사용 하 여 메서드 실행, 때문에 추가 하려고 하는 행 이미 있는 데이터베이스를 만드는 첫 번째 마이그레이션 후에 데이터를 삽입할 수 없습니다. "Upsert" 작업이 있지만 이미 존재 하는 행을 삽입 하려고 할 경우 수행 하는 오류를 방지할 수 ***재정의*** 응용 프로그램을 테스트 하는 동안 실행 한 데이터 변경 사항이 있습니다. 테스트 테이블의에서 데이터 일부 원하지 않을 수 있습니다이 위해서는: 경우에 따라 테스트 하는 동안 데이터를 변경 하면 원하는 변경 내용을 데이터베이스 업데이트 후 하 게 유지 합니다. 조건부 삽입 작업을 수행 하려는 경우: 존재 하지 않는 경우에 행을 삽입 합니다. Seed 메서드는 두 가지 방법을 모두 사용합니다.

    에 전달 된 첫 번째 매개 변수는 [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) 메서드 행 이미 존재 하는지 확인 하는 데 속성을 지정 합니다. 테스트 학생 데이터를 제공 하는 대 한는 `LastName` 속성 목록에 각 성이 고유 이므로이 용도로 사용할 수 수 있습니다.

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

    이 코드는 마지막 이름이 고유한 지 가정 합니다. 중복 되는 마지막 이름이 인 학생을 수동으로 추가 하는 경우 마이그레이션을 수행 하는 다음에 다음과 같은 예외를 얻을 수 있습니다.

    시퀀스에 요소가 둘 이상

    에 대 한 자세한 내용은 `AddOrUpdate` 메서드를 참조 [EF 4.3 AddOrUpdate 메서드로 주의](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/) Julie Lerman 블로그.

    추가 하는 코드 `Enrollment` 엔터티를 사용 하지 않는 `AddOrUpdate` 메서드. 확인 하는 경우 엔터티 이미 있으며 존재 하지 않는 경우 엔터티를 삽입 합니다. 이 방법은 마이그레이션을 실행 하는 경우 등록 등급에 수행한 변경 내용을 유지 됩니다. 코드의 각 멤버를 반복는 `Enrollment` [목록](https://msdn.microsoft.com/library/6sh2ey19.aspx) 등록 데이터베이스에 없는 경우에 등록 데이터베이스에 추가 합니다. 데이터베이스를 업데이트 하는 처음으로 데이터베이스가 비어 있게 됩니다, 되므로 각 등록 추가 됩니다.

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample13.cs)]

    디버깅 하는 방법에 대 한 내용은 `Seed` 메서드와 "Alexander Carson" 라는 두 명의 학생이 같은 중복 데이터를 처리 하는 방법을 참조 [Seeding 및 디버깅 Entity Framework (EF)](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) Rick Anderson의 블로그에서 합니다.
2. 프로젝트를 빌드합니다.

### <a name="create-and-execute-the-first-migration"></a>만들기 및 실행 첫 번째 마이그레이션

1. 패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다. 

    [!code-powershell[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample14.ps1)]

    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image13.png)

    `add-migration` 명령은 Migrations 폴더에 추가 *[날짜 스탬프]\_InitialCreate.cs* 데이터베이스를 만드는 코드가 포함 된 파일입니다. 첫 번째 매개 변수 (`InitialCreate)` 파일에 사용 되는 단어 또는 구를 마이그레이션에서 수행 되는 것을 요약 하는 일반적으로 선택;에 이름을 지정 하 고 원하는 작업이 무엇이 든 될 수 있습니다. 나중에 마이그레이션할 이름을 지정할 수 있습니다는 예를 들어 &quot;AddDepartmentTable&quot;합니다.

    ![초기 마이그레이션 사용 하 여 migrations 폴더](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image14.png)

    `Up` 의 메서드는 `InitialCreate` 클래스는 데이터 모델 엔터티 집합에 해당 하는 데이터베이스 테이블을 만듭니다 및 `Down` 메서드 삭제 합니다. 마이그레이션에서는 마이그레이션을 위한 데이터 모델 변경을 구현하기 위해 `Up` 메서드를 호출합니다. 업데이트를 롤백하는 명령을 입력하면 마이그레이션에서 `Down` 메서드를 호출합니다. 다음 코드의 내용을 보여 줍니다.는 `InitialCreate` 파일:

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample15.cs)]

    `update-database` 명령이 실행 되는 `Up` 데이터베이스를 만들고 해당 메서드를 실행 된 `Seed` 데이터베이스를 채우는 메서드.

데이터 모델에 대 한 SQL Server 데이터베이스를 지금 생성 되었습니다. 데이터베이스 이름은 *ContosoUniversity*, 및 *.mdf* 를 프로젝트의 파일은 *앱\_데이터* 폴더에 지정 된 것 이기 때문에 프로그램 연결 문자열입니다.

사용할 수 있습니다 **서버 탐색기** 또는 **SQL Server 개체 탐색기** (SSOX) Visual Studio에서 데이터베이스를 볼 수 있습니다. 이 자습서에 대 한 사용 **서버 탐색기**합니다. Visual Studio Express 2012 for Web에서 **서버 탐색기** 라고 **데이터베이스 탐색기**합니다.

1. **보기** 메뉴를 클릭 하 여 **서버 탐색기**합니다.
2. 클릭는 **연결 추가** 아이콘입니다.

    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image15.png)
3. 표시 되 면 하는 경우는 **데이터 소스 선택** 대화 상자에서 클릭 **Microsoft SQL Server**, 클릭 하 고 **계속**합니다.  
  
    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image16.png)
4. 에 **연결 추가** 대화 상자에 입력 **(localdb) \v11.0** 에 대 한는 **서버 이름**합니다. 아래 **데이터베이스 이름 선택 또는 입력**선택, **ContosoUniversity 합니다.**  
  
    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image17.png)
5. **확인**을 클릭합니다.
6. 확장 **SchoolContext** 펼친 다음 **테이블**합니다.  
  
    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image18.png)
7. 마우스 오른쪽 단추로 클릭는 **학생** 테이블 마우스 클릭 **테이블 데이터 표시** 생성 된 열과 테이블에 삽입 된 행을 볼 수 있습니다.

    ![학생 테이블](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image19.png)

## <a name="creating-a-student-controller-and-views"></a>학생 컨트롤러 및 뷰 만들기

다음 단계에서는 이러한 테이블 중 하나에 사용할 수 있는 응용 프로그램에서 ASP.NET MVC 컨트롤러 및 뷰를 만드는 것입니다.

1. 만들려는 `Student` 컨트롤러를 마우스 오른쪽 단추로 클릭는 **컨트롤러** 폴더에 **솔루션 탐색기**선택, **추가**, 클릭 하 고 **컨트롤러** . 에 **컨트롤러 추가** 대화 상자, 다음을 선택 하 고 클릭 **추가**: 

    - 컨트롤러 이름: **StudentController**합니다.
    - 서식 파일: **읽기/쓰기 동작 및 뷰가, Entity Framework를 사용 하 여 포함 된 MVC 컨트롤러**합니다.
    - 모델 클래스: **학생 (ContosoUniversity.Models)**합니다. (드롭 다운 목록에서이 옵션을 표시 되지 않으면, 프로젝트 빌드 및 다시 시도 하십시오.)
    - 데이터 컨텍스트 클래스: **SchoolContext (ContosoUniversity.Models)**합니다.
    - 보기: **Razor (CSHTML)**합니다. (기본값입니다.)

    ![Add_Controller_dialog_box_for_Student_controller](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image20.png)
- Visual Studio가 열릴는 *Controllers\StudentController.cs* 파일입니다. 클래스 변수 만들어진 데이터베이스 컨텍스트 개체를 인스턴스화하는 것이 표시 됩니다.

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample16.cs)]

    `Index` 동작 메서드가에서 학생의 목록을 가져옵니다는 *학생* 엔터티 참조 하 여 집합에서 `Students` 데이터베이스 컨텍스트 인스턴스의 속성:

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample17.cs)]

    *Student\Index.cshtml* 보기 테이블에이 목록에 표시 됩니다.

    [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample18.cshtml)]
- Ctrl+F5를 눌러 프로젝트를 실행합니다.

    클릭는 **학생** 테스트 데이터를 탭 하는 `Seed` 삽입 메서드.

    ![학생 인덱스 페이지](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image21.png)

## <a name="conventions"></a>규칙

사용으로 인해 전체 데이터베이스를 만들 수도 수 있게 되기를 Entity Framework에 대 한 순서 대로 작성 해야 했습니다 코드의 양을 최소화 됩니다 *규칙*, 또는 Entity Framework에서는 가정 합니다. 그 중 일부를 이미 설명 되어 있습니다.

- Pluralized 형태의 엔터티 클래스 이름은 테이블 이름으로 사용 됩니다.
- 엔터티 속성 이름은 열 이름에 사용됩니다.
- 명명 된 엔터티 속성 `ID` 또는 *classname* `ID` 기본 키 속성으로 인식 됩니다.

지금까지 살펴본 규칙을 재정의할 수 있습니다 (예를 들어 사용자가 지정한 테이블 이름을 복수화 수 해서는 안) 있으며 규칙 및 재정의에 해당 하는 방법에 대해 자세히 배울 수 있습니다는 [더 복잡 한 데이터 모델을 만드는](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md) 자습서 나중에 있습니다. 자세한 내용은 참조 [코드 첫 번째 규칙](https://msdn.microsoft.com/data/jj679962)합니다.

## <a name="summary"></a>요약

이제 Entity Framework 및 SQL Server Express를 사용 하 여 저장 하 고 데이터를 표시 하는 간단한 응용 프로그램을 만들었습니다. 다음 자습서에서는 기본 CRUD 수행 하는 방법을 배우게 됩니다 (만들기, 읽기, 업데이트, 삭제) 작업입니다. 이 페이지의 맨 아래에 피드백을 둘 수 있습니다. 알려 주시면이 자습서의이 부분 빴 어떻게 그리고 것 개선할 수 방법입니다.

다른 Entity Framework 리소스에 대 한 링크에서 확인할 수 있습니다는 [ASP.NET 데이터 액세스 콘텐츠 맵](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.

>[!div class="step-by-step"]
[다음](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)
