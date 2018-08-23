---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
title: (1 / 10) ASP.NET MVC 응용 프로그램에 대 한 Entity Framework 데이터 모델 만들기 | Microsoft Docs
author: tdykstra
description: 이 자습서 시리즈의 최신 버전이 Visual Studio 2013, Entity Framework 6 및 MVC 5에 대 한 사용 가능 합니다. Contoso University 샘플 웹 응용 프로그램 de...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 4ba029b6-ee7c-4e45-a0e7-b703c37e5d9a
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 037f67d679762a037eaef9f0a4060156b94d97b1
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41829193"
---
<a name="creating-an-entity-framework-data-model-for-an-aspnet-mvc-application-1-of-10"></a>(1 / 10) ASP.NET MVC 응용 프로그램에 대 한 Entity Framework 데이터 모델 만들기
====================
[Tom Dykstra](https://github.com/tdykstra)

[완료 된 프로젝트 다운로드](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> > [!NOTE] 
> > 
> > A [이 자습서 시리즈의 최신 버전](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) Visual Studio 2013, Entity Framework 6 및 MVC 5를 사용할 수 있습니다.
> 
> 
> Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 5 및 Visual Studio 2012를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다. 샘플 응용 프로그램은 가상 Contoso University의 웹 사이트입니다. 학생 입학, 강좌 개설 및 강사 할당과 같은 기능이 있습니다. 이 자습서 시리즈에는 Contoso University 샘플 응용 프로그램을 빌드하는 방법을 설명 합니다. 할 수 있습니다 [완성된 된 응용 프로그램 다운로드](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)합니다.
> 
> ## <a name="code-first"></a>Code First
> 
> 세 가지 방법으로 Entity Framework에서 데이터로 작업할 수 있습니다: *Database First*를 *Model First*, 및 *Code First*합니다. Code First에 대 한이 자습서가입니다. 시나리오에 가장 적합 한 선택 하는 방법은 이러한 워크플로 및 지침 간의 차이점에 대 한 정보를 참조 하세요 [Entity Framework 개발 워크플로](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)합니다.
> 
> ## <a name="mvc"></a>MVC
> 
> 샘플 응용 프로그램에 빌드되어 [ASP.NET MVC](../../../index.md)합니다. ASP.NET Web Forms 모델을 사용 하려는 경우 참조를 [모델 바인딩 및 Web Forms](../../../../web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data.md) 자습서 시리즈와 [ASP.NET 데이터 액세스 콘텐츠 맵](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.
> 
> ## <a name="software-versions"></a>소프트웨어 버전
> 
> | **자습서에 표시** | **역시** |
> | --- | --- |
> | Windows 8 | Windows 7 |
> | Visual Studio 2012 | Visual Studio 2012 Express for Web입니다. VS 2012 또는 VS 2012 Express for Web 아직 없는 경우 자동으로 Windows Azure SDK에서 설치 됩니다. Visual Studio 2013에는 작동 하지만 자습서를 사용 하 여 테스트 되지 않았습니다 하 고 일부 메뉴 선택 및 대화 상자는 다릅니다. 합니다 [VS 2013 버전의 Windows Azure SDK](https://go.microsoft.com/fwlink/p/?linkid=323510) Windows Azure 배포에 필요 합니다. |
> | .NET 4.5 | 표시 된 기능의 대부분.NET 4에서 작동 하지만 일부 없습니다. 예를 들어, EF에서 열거형 지원.NET 4.5를 필요로 합니다. |
> | Entity Framework 5 |  |
> | [Windows Azure SDK 2.1](https://go.microsoft.com/fwlink/p/?linkid=323511) | Windows Azure 배포 단계를 건너뛰면 SDK가 필요 하지 않습니다. SDK의 새 버전이 출시 되는 경우 링크는 최신 버전을 설치 합니다. 이 경우 일부 지침은 새 UI 및 기능에 맞게 해야 합니다. |
> 
> ## <a name="questions"></a>질문
> 
> 에 자습서로 직접 관련 되지 않은 질문이 있을 수를 게시할 수 있습니다 합니다 [ASP.NET Entity Framework 포럼](https://forums.asp.net/1227.aspx)서 [Entity Framework 및 LINQ to Entities 포럼](https://social.msdn.microsoft.com/forums/adodotnetentityframework/threads/), 또는 [ StackOverflow.com](http://stackoverflow.com/)합니다.
> 
> ## <a name="acknowledgments"></a>감사의 글
> 
> 에 대 한 시리즈의 마지막 자습서를 참조 하세요 [승인 및 VB에 대 한 메모](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#acknowledgments)합니다.
> 
> ## <a name="original-version-of-the-tutorial"></a>자습서의 원래 버전
> 
> 자습서의 원래 버전이 제공 되는 [EF 4.1 / MVC 3 전자책](https://social.technet.microsoft.com/wiki/contents/articles/11608.e-book-gallery-for-microsoft-technologies.aspx#GettingStartedwiththeEntityFramework4.1usingASP.NETMVC)합니다.


## <a name="the-contoso-university-web-application"></a>Contoso University 웹 응용 프로그램

이 자습서에서 빌드하는 응용 프로그램은 간단한 대학 웹 사이트입니다.

사용자는 학생, 강좌 및 강사 정보를 보고 업데이트할 수 있습니다. 다음은 만들 몇 가지 화면입니다.

![Students_Index_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image1.png)

![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image2.png)

자습서가 Entity Framework를 사용하는 방법에 주로 초점을 맞출 수 있도록 이 사이트의 UI 스타일은 기본 제공 템플릿에서 생성된 내용에 가깝게 유지되었습니다.

## <a name="prerequisites"></a>전제 조건

지침 및이 자습서의 스크린샷에서 사용 한다고 가정 [Visual Studio 2012](https://www.microsoft.com/visualstudio/eng/downloads) 하거나 [Visual Studio 2012 Express for Web](https://go.microsoft.com/fwlink/?LinkID=275131)최신 업데이트 및 7 월을 기준으로 설치 하는.NET 용 Azure SDK를 사용 하 여 2013입니다. 다음 링크를 사용 하 여이 가져올 수 있습니다.

[Azure SDK for.NET (Visual Studio 2012)](https://go.microsoft.com/fwlink/?LinkId=254364)

Visual Studio가 설치 되어 있다면 위의 링크는 누락 된 구성 요소를 설치 합니다. Visual Studio가 없는 경우 링크는 Visual Studio 2012 Express for Web 설치 됩니다. Visual Studio 2013을 사용할 수 있지만 일부 필요한 절차와 화면 다릅니다.

## <a name="create-an-mvc-web-application"></a>MVC 웹 응용 프로그램 만들기

Visual Studio를 열고 새 C# 프로젝트 만들기 "ContosoUniversity"를 사용 하 여 명명 된 **ASP.NET MVC 4 웹 응용 프로그램** 템플릿. 대상으로 하는지 확인 **.NET Framework 4.5** (사용할 [ `enum` 속성](https://msdn.microsoft.com/data/hh859576.aspx),.NET 4.5를 필요로 하는).

![New_project_dialog_box](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image3.png)

에 **새 ASP.NET MVC 4 프로젝트** 대화 상자 선택 합니다 **인터넷 응용 프로그램** 템플릿.

유지를 **Razor** 두고 보기 엔진을 선택 합니다 **단위 테스트 프로젝트 만들기** 확인란의 선택을 취소 합니다.

**확인**을 클릭합니다.

![Project_template_options](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image4.png)

## <a name="set-up-the-site-style"></a>사이트 스타일 설정

몇 가지 간단한 변경 내용으로 사이트 메뉴, 레이아웃 및 홈 페이지를 설정합니다.

오픈 *Views\Shared\\_Layout.cshtml*, 파일의 내용을 다음 코드로 바꿉니다. 변경 내용은 강조 표시되어 있습니다.

[!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample1.cshtml?highlight=5,15,25-28,43)]

이 코드로 다음이 변경됩니다.

- "Contoso University"를 사용 하 여 "My ASP.NET MVC 응용 프로그램" 및 "사용자 로고는 여기"의 템플릿 인스턴스를 대체 합니다.
- 이 자습서의 뒷부분에서 사용할 몇 가지 작업 링크를 추가 합니다.

*Views\Home\Index.cshtml*, ASP.NET 및 MVC에 대 한 템플릿 단락을 제거 하려면 다음 코드를 사용 하 여 파일의 내용을 바꿉니다.

[!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample2.cshtml)]

*controllers\ homecontroller.cs*에 대 한 값을 변경 `ViewBag.Message` 에 `Index` 다음 예와에서 같이 "welcome Contoso University!", 작업 메서드:

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample3.cs?highlight=3)]

사이트를 실행 하려면 CTRL + F5 키를 누릅니다. 주 메뉴를 사용 하 여 홈 페이지가 표시 됩니다.

![Contoso_University_home_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image5.png)

## <a name="create-the-data-model"></a>데이터 모델 만들기

다음으로 Contoso University 응용 프로그램에 대한 엔터티 클래스를 만듭니다. 다음 세 가지 엔터티를 사용 하 여 시작할 수 있습니다.

![Class_diagram](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image6.png)

`Student` 및 `Enrollment` 엔터티 간에 일대다 관계가 있으며 `Course` 및 `Enrollment` 엔터티 간에 일대다 관계가 있습니다. 즉, 학생은 개수에 관계 없이 강좌에 등록될 수 있으며 강좌는 등록된 학생이 여러 명일 수 있습니다.

다음 섹션에서 이러한 엔터티 각각에 대한 클래스를 만듭니다.

> [!NOTE]
> 이러한 엔터티 클래스의 모든 만들기를 완료 하기 전에 프로젝트를 컴파일할 하려고 하면 컴파일러 오류를 얻게 됩니다.


### <a name="the-student-entity"></a>학생 엔터티

![Student_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image7.png)

에 *모델* 폴더를 만들기 *Student.cs* 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample4.cs)]

`StudentID` 속성은 이 클래스에 해당하는 데이터베이스 테이블의 기본 키 열이 됩니다. 기본적으로 Entity Framework는 명명 된 속성을 해석 `ID` 나 *classname* `ID` 기본 키로 합니다.

합니다 `Enrollments` 속성을 *탐색 속성*합니다. 탐색 속성은 이 엔터티와 관련된 다른 엔터티를 포함합니다. 이 경우에 `Enrollments` 의 속성을 `Student` 엔터티 모두 보유할를 `Enrollment` 는 관련 된 엔터티 `Student` 엔터티. 즉, 경우를 지정 `Student` 데이터베이스의 행에는 관련 된 두 개의 `Enrollment` 행 (해당 학생의 기본 키를 포함 하는 행 값을 해당 `StudentID` 외래 키 열), 해당 `Student` 엔터티의 `Enrollments` 탐색 속성 이러한 두 사용 될 `Enrollment` 엔터티.

탐색 속성은 일반적으로 정의 됩니다 `virtual` 를 같은 특정 Entity Framework 기능을 취할 수 있습니다 *지연 로딩*합니다. (지연 로딩에 설명의 뒷부분에 나오는 합니다 [관련 데이터를 읽는](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) 이 시리즈의 뒷부분에 나오는 자습서입니다.

탐색 속성이 여러 엔터티를 포함할 수 있는 경우(다대다 또는 일대다 관계로), 해당 형식은 `ICollection`와 같이 항목이 추가, 삭제 및 업데이트될 수 있는 목록이어야 합니다.

### <a name="the-enrollment-entity"></a>등록 엔터티

![Enrollment_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image8.png)

*Models* 폴더에서*Enrollment.cs*를 만들고 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample5.cs)]

등급 속성은는 [enum](https://msdn.microsoft.com/data/hh859576.aspx)합니다. 후 물음표 합니다 `Grade` 형식 선언을 나타냅니다는 `Grade` 속성은 [nullable](https://msdn.microsoft.com/library/2cf62fcy.aspx)합니다. Null 인 등급은 0 등급과 다릅니다-null 성적 알려질 하거나 아직 할당 되지 않은 것을 의미 합니다.

`StudentID` 속성은 외래 키로, 해당 탐색 속성은 `Student`입니다. `Enrollment` 엔터티는 하나의 `Student` 엔터티와 연결되어 있으므로 속성은 단일 `Student` 엔터티만 포함할 수 있습니다(이전에 살펴본 여러 `Enrollment` 엔터티를 포함할 수 있는 `Student.Enrollments` 탐색 속성과 달리).

`CourseID` 속성은 외래 키로, 해당 탐색 속성은 `Course`입니다. `Enrollment` 엔터티는 하나의 `Course` 엔터티와 연결됩니다.

### <a name="the-course-entity"></a>강좌 엔터티

![Course_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image9.png)

에 *모델* 폴더를 만듭니다 *Course.cs*, 기존 코드를 다음 코드로 바꾸어:

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample6.cs)]

`Enrollments` 속성은 탐색 속성입니다. `Course` 엔터티는 `Enrollment` 엔터티의 개수와 관련이 있을 수 있습니다.

클릭 합니다. 자세한 정보는 [[DatabaseGenerated](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedattribute(v=vs.110).aspx)([databasegeneratedoption입니다](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedoption(v=vs.95).aspx)합니다. 다음 자습서에서 특성 없음)]입니다. 기본적으로 이 특성을 통해 생성하는 데이터베이스를 갖는 대신 강좌에 대한 기본 키를 입력할 수 있습니다.

## <a name="create-the-database-context"></a>데이터베이스 컨텍스트 만들기

지정 된 데이터 모델에 대 한 Entity Framework 기능을 조정 하는 주 클래스는 합니다 *데이터베이스 컨텍스트* 클래스입니다. 이 클래스에서 파생 하 여 만든 합니다 [System.Data.Entity.DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx) 클래스입니다. 코드에서 데이터 모델에 포함되는 엔터티를 지정합니다. 특정 Entity Framework 동작을 사용자 지정할 수도 있습니다. 이 프로젝트에서 클래스 이름은 `SchoolContext`로 지정됩니다.

라는 폴더를 만듭니다 *DAL* (데이터 액세스 계층)에 대 한 합니다. 해당 폴더에서 라는 새 클래스 파일을 만듭니다 *SchoolContext.cs*, 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample7.cs)]

이 코드에서는 한 [DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=VS.103).aspx) 각 엔터티 집합에 대 한 속성입니다. Entity Framework 용어에서는 *엔터티 집합* 일반적으로 데이터베이스 테이블에 해당와 *엔터티* 테이블의 행에 해당 합니다.

합니다 `modelBuilder.Conventions.Remove` 문에서 [OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx) 메서드는 테이블 이름을 복수화 되에서 않도록 합니다. 생성된 된 테이블 이름은이 수행 하지 않은 경우 `Students`하십시오 `Courses`, 및 `Enrollments`합니다. 테이블 이름 대신 됩니다 `Student`, `Course`, 및 `Enrollment`합니다. 개발자는 테이블 이름을 복수화할지 여부에 대해 동의하지 않습니다. 이 자습서에서는 단 수 형태를 사용 하지만 중요 한 점은 포함 하거나 코드이 줄을 생략 하 여 원하는 어떤 폼을 선택할 수 있습니다.

## <a name="sql-server-express-localdb"></a>SQL Server Express LocalDB

[LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx) 는 SQL Server Express 데이터베이스 엔진의 요청 시 시작 하 고 사용자 모드에서 실행 되는 경량 버전입니다. LocalDB 데이터베이스를 사용 하 여 작업할 수 있도록 하는 SQL Server Express의 특수 실행 모드에서 실행 *.mdf* 파일입니다. 일반적으로, LocalDB 데이터베이스 파일에 보관 되는 *앱\_데이터* 웹 프로젝트의 폴더입니다. SQL Server express 사용자 인스턴스 기능 또한 작업할 수 있습니다 *.mdf* 파일을 하지만 사용자 인스턴스 기능 사용 되지 않으면 따라서 LocalDB가 사용 하기 위한 권장 *.mdf* 파일입니다.

일반적으로 SQL Server Express 프로덕션 웹 응용 프로그램에 대 한 사용 되지 않습니다. LocalDB 특히 권장 되지 않습니다 프로덕션 웹 응용 프로그램을 사용 하므로 IIS와 함께 작동 하도록 설계 되지는 않았습니다.

Visual Studio 2012 및 이후 버전에서는 LocalDB Visual Studio를 사용 하 여 기본적으로 설치 됩니다. Visual Studio 2010 및 이전 버전의 Visual Studio를 사용 하 여 기본적으로 설치 됩니다 (LocalDB) 없이 SQL Server Express Visual Studio 2010을 사용 하는 경우 수동으로 설치 해야 합니다.

이 자습서에서는 사용 하 여 작업할 LocalDB 데이터베이스에 저장할 수 있도록 합니다 *앱\_데이터* 폴더를 *.mdf* 파일입니다. 루트를 엽니다 *Web.config* 파일을 새 연결 문자열을 추가 합니다 `connectionStrings` 다음 예제에서와 같이 컬렉션입니다. (업데이트 해야 합니다 *Web.config* 루트 프로젝트 폴더의 파일입니다. 도 *Web.config* 파일은 합니다 *뷰* 하위 폴더를 업데이트할 필요가 없습니다.)

[!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample8.xml)]

기본적으로 Entity Framework를 찾고 이름이 연결 문자열을 `DbContext` 클래스 (`SchoolContext` 이 프로젝트에 대 한). 추가한 다음 연결 문자열을 명명 된 LocalDB 데이터베이스를 지정 합니다. *ContosoUniversity.mdf* 에 *앱\_데이터* 폴더입니다. 자세한 내용은 [ASP.NET 웹 응용 프로그램에 대 한 SQL Server 연결 문자열](https://msdn.microsoft.com/library/jj653752.aspx)합니다.

실제로 연결 문자열을 지정할 필요가 없습니다. 연결 문자열을 지정 하지 않으면, Entity Framework는 클러스터를 만들; 그러나 데이터베이스에 없을 수도 합니다 *앱\_데이터* 앱의 폴더입니다. 데이터베이스를 만들 위치에 대 한 내용은 참조 하세요 [Code First 새 데이터베이스로](https://msdn.microsoft.com/data/jj193542)합니다.

합니다 `connectionStrings` 컬렉션 라는 연결 문자열은 `DefaultConnection` 멤버 자격 데이터베이스에 사용 됩니다. 멤버 자격 데이터베이스가이 자습서에서 사용 되지 않습니다. 두 연결 문자열의 유일한 차이점에 데이터베이스 이름이 며 이름 특성 값입니다.

## <a name="set-up-and-execute-a-code-first-migration"></a>설정 하 고 Code First 마이그레이션 실행

를 처음 시작 하면 응용 프로그램을 개발할 때 데이터 모델 변경 자주 그리고 될 때마다 모델 변경 내용을 가져와서 데이터베이스와 동기화 합니다. Entity Framework를 자동으로 삭제 하 고 데이터 모델을 변경할 때마다 데이터베이스를 다시 만들지를 구성할 수 있습니다. 테스트 데이터를 쉽게 다시 만들 하지만 일반적으로 데이터베이스를 삭제 하지 않고 데이터베이스 스키마를 업데이트 하려면 프로덕션에 배포한 후에 개발 초기에 문제가 되지 않습니다. 삭제 하 고 다시 작성 하지 않고 데이터베이스를 업데이트 하려면 Code First 마이그레이션 기능 사용 하도록 설정 합니다. 새 프로젝트의 개발 주기의 초기 단계에서 사용 하려는 [DropCreateDatabaseIfModelChanges](https://msdn.microsoft.com/library/gg679604(v=vs.103).aspx) 모델 변경 될 때마다 삭제, 다시 만들고 다시 데이터베이스를 시드할 하 합니다. 응용 프로그램을 배포할 준비가 얻게 하나, 마이그레이션 방법 변환할 수 있습니다. 이 자습서에 대 한 마이그레이션만 사용할 수 있습니다. 자세한 내용은 [Code First 마이그레이션을](https://msdn.microsoft.com/data/jj591621) 하 고 [마이그레이션을 스크린 캐스트 시리즈가](https://blogs.msdn.com/b/adonet/archive/2014/03/12/migrations-screencast-series.aspx)합니다.

### <a name="enable-code-first-migrations"></a>Code First 마이그레이션 사용

1. **도구** 메뉴에서 클릭 **라이브러리 패키지 관리자** 차례로 **패키지 관리자 콘솔**합니다.

    ![Selecting_Package_Manager_Console](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image10.png)
2. 에 `PM>` 프롬프트에 다음 명령을 입력 합니다.

    [!code-powershell[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample9.ps1)]

    ![마이그레이션을 사용 하도록 설정 명령](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image11.png)

    이 명령은 만듭니다는 *마이그레이션을* ContosoUniversity 프로젝트에서 폴더는 폴더에 저장을 *Configuration.cs* 파일을 편집 하 여 마이그레이션을 구성할 수 있습니다.

    ![마이그레이션 폴더](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image12.png)

    합니다 `Configuration` 클래스에 포함 되어는 `Seed` 데이터베이스를 만들 때와 데이터 모델 변경 후 업데이트 될 때마다 호출 되는 메서드입니다.

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample10.cs)]

    이 목적은 `Seed` 메서드는 Code First으로 작성 하거나 업데이트 한 후 데이터베이스에 테스트 데이터를 삽입할 수 있도록 합니다.

### <a name="set-up-the-seed-method"></a>Seed 메서드 설정

합니다 [시드](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) 메서드는 Code First 마이그레이션을 데이터베이스를 만들 때 및 최신 마이그레이션을 위해 데이터베이스를 업데이트할 때마다 실행 됩니다. 시드 메서드가의 목적은 응용 프로그램 하기 전에 테이블에 데이터를 삽입할 수 있도록 처음으로 데이터베이스에 액세스 합니다.

Code First의 이전 버전에서 마이그레이션이 릴리스되기 전에 것이 일반적 이었습니다 `Seed` 개발 하는 동안 모델 바뀔 때마다 데이터베이스 완전히 삭제 하 고 처음부터 다시 만들 수 있었기 때문에 테스트 데이터를 삽입 하는 방법입니다. Code First 마이그레이션, 데이터베이스 변경 후 데이터는 유지 하는 테스트의 테스트 데이터를 포함 하므로 합니다 [시드](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) 일반적으로 메서드는 필요 없습니다. 사실, 원하지는 `Seed` 사용할 마이그레이션 데이터베이스를 프로덕션에 배포 하려면 때문에 경우에 테스트 데이터를 삽입 하는 방법의 `Seed` 메서드는 프로덕션 환경에서 실행 됩니다. 원하는 경우에 `Seed` 프로덕션 환경에서 삽입 하려는 데이터에만 데이터베이스에 삽입 하는 방법입니다. 예를 들어 데이터베이스의 실제 부서 이름을 포함 하려면이 좋습니다는 `Department` 응용 프로그램이 프로덕션 환경에서 사용 가능 해지면 테이블입니다.

이 자습서에서는 사용할 마이그레이션 배포용 하지만 `Seed` 메서드는 테스트 데이터 삽입 그래도 쉽게 응용 프로그램 기능을 많은 양의 데이터를 수동으로 삽입 하지 않고도 작동 하는 방식을 확인 합니다.

1. 내용을 대체 합니다 *Configuration.cs* 가 새 데이터베이스에 테스트 데이터를 로드 하는 다음 코드를 사용 하 여 파일입니다. 

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

    합니다 [시드](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) 메서드는 입력된 매개 변수로 데이터베이스 컨텍스트 개체를 사용 하 고 메서드에서 코드를 해당 개체를 사용 하 여 데이터베이스에 새 엔터티를 추가 합니다. 각 엔터티 형식에 대 한 코드를 새 엔터티 컬렉션을 만듭니다, 적절 한 추가한 [DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx) 속성 및 데이터베이스에 변경 내용 저장 합니다. 호출할 필요는 없습니다 합니다 [SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx) 엔터티의 각 그룹 뒤 메서드를으로 여기에서 수행 되지만 코드는 데이터베이스에 쓰는 동안 예외가 발생 하는 경우 문제의 소스를 찾을 수 있습니다 작업을 수행 합니다.

    일부 데이터를 삽입 하는 문을 사용 합니다 [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) "upsert" 작업을 수행 하는 방법입니다. 때문에 `Seed` 모든 마이그레이션을 사용 하 여 메서드 실행, 이기 때문에 추가 하려는 행 이미 있는 데이터베이스를 만드는 첫 번째 마이그레이션 후에 데이터를 삽입할 수 없습니다. "Upsert" 작업 하지만 이미 존재 하는 행을 삽입 하려고 할 경우는 오류를 방지할 수 ***재정의*** 응용 프로그램을 테스트 하는 동안 만들어졌을 수 있는 데이터를 변경 합니다. 일부 테이블의 테스트 데이터를 사용 하 여 하지 않으려는 경우이 위해서는: 경우에 따라 테스트 하는 동안 데이터를 변경한 경우 원하는 데이터베이스 업데이트 후 유지 하려면 변경 내용을 합니다. 조건부 삽입 작업을 수행 하려는 경우: 존재 하지 않는 경우에 행을 삽입 합니다. Seed 메서드는 두 가지 방법을 모두 사용합니다.

    첫 번째 매개 변수가 전달 되는 [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) 메서드는 행이 이미 존재 하는지 확인 하는 데 속성을 지정 합니다. 테스트 학생 데이터를 제공 하는 대 한는 `LastName` 목록의 마지막 이름이 있으므로이 목적을 위해 속성을 사용 수 있습니다.

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

    이 코드는 마지막 이름이 고유한 지를 가정 합니다. 중복 된 성 가진 학생을 수동으로 추가 하는 경우 마이그레이션을 수행한 다음에 다음 예외를 얻게 됩니다.

    시퀀스에 요소가 둘 이상

    에 대 한 자세한 내용은 합니다 `AddOrUpdate` 메서드를 참조 하세요 [EF 4.3 AddOrUpdate 메서드를 사용 하 여 주의](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/) Julie Lerman의 블로그입니다.

    추가 하는 코드 `Enrollment` 엔터티를 사용 하지는 `AddOrUpdate` 메서드. 확인 하는 경우 엔터티의 이미 있으며 존재 하지 않는 경우 엔터티를 삽입 합니다. 이 이렇게 변경 하면는 등록 등급 마이그레이션을 실행 하는 경우 유지 됩니다. 코드의 각 멤버를 반복 합니다 `Enrollment` [목록](https://msdn.microsoft.com/library/6sh2ey19.aspx) 등록 데이터베이스에 없는 경우에 등록 데이터베이스에 추가 합니다. 처음으로 데이터베이스를 업데이트할 데이터베이스 비게 됩니다 되므로 각 등록 추가 됩니다.

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample13.cs)]

    디버깅 하는 방법에 대 한 자세한 합니다 `Seed` 메서드와 "Alexander Carson" 라는 두 명의 학생이 같은 중복 데이터를 처리 하는 방법을 참조 하세요 [시드 및 디버깅 EF (Entity Framework) Db](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) Rick Anderson의 블로그에서입니다.
2. 프로젝트를 빌드합니다.

### <a name="create-and-execute-the-first-migration"></a>만들고 첫 번째 마이그레이션 실행

1. 패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다. 

    [!code-powershell[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample14.ps1)]

    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image13.png)

    `add-migration` 명령은 마이그레이션 폴더에 추가 된 *[날짜 스탬프]\_InitialCreate.cs* 데이터베이스를 만드는 코드가 포함 된 파일입니다. 첫 번째 매개 변수 (`InitialCreate)` 파일에 사용 되는 단어 또는 구를 요약 마이그레이션에서 수행 되는 일반적으로 선택;에 이름을 지정 하 고 원하는 수. 예를 들어 이후 마이그레이션의 이름을 수 있습니다 &quot;AddDepartmentTable&quot;합니다.

    ![초기 마이그레이션 사용 하 여 마이그레이션 폴더](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image14.png)

    `Up` 메서드를 `InitialCreate` 클래스에는 데이터 모델 엔터티 집합에 해당 하는 데이터베이스 테이블을 만듭니다 및 `Down` 메서드를 삭제 합니다. 마이그레이션에서는 마이그레이션을 위한 데이터 모델 변경을 구현하기 위해 `Up` 메서드를 호출합니다. 업데이트를 롤백하는 명령을 입력하면 마이그레이션에서 `Down` 메서드를 호출합니다. 다음 코드의 내용을 보여 줍니다는 `InitialCreate` 파일:

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample15.cs)]

    합니다 `update-database` 명령이 실행 되는 `Up` 데이터베이스를 만들고 해당 메서드를 실행 합니다 `Seed` 데이터베이스를 채우는 방법입니다.

이제 SQL Server 데이터베이스를 데이터 모델에 대해 만들었습니다. 데이터베이스의 이름은 *ContosoUniversity*, 및 *.mdf* 파일은 프로젝트의 *앱\_데이터* 폴더에 지정 된 것 이기 때문에 연결 문자열입니다.

사용할 수 있습니다 **서버 탐색기** 하거나 **SQL Server 개체 탐색기** (SSOX) Visual Studio에서 데이터베이스를 봅니다. 이 자습서를 사용 하 여 **서버 탐색기**합니다. Visual Studio Express 2012 for Web **서버 탐색기** 이라고 **데이터베이스 탐색기**합니다.

1. **뷰** 메뉴에서 클릭 **서버 탐색기**합니다.
2. 클릭 합니다 **연결 추가** 아이콘입니다.

    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image15.png)
3. 사용 하 여 메시지가 표시 되는 경우는 **데이터 소스 선택** 대화 상자에서 클릭 **Microsoft SQL Server**를 클릭 하 고 **계속**합니다.  
  
    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image16.png)
4. 에 **연결 추가** 대화 상자에 입력 합니다 **(localdb) \v11.0** 에 대 한 합니다 **서버 이름**합니다. 아래 **데이터베이스 이름 선택 또는 입력**, 선택 **ContosoUniversity 합니다.**  
  
    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image17.png)
5. **확인**을 클릭합니다.
6. 확장 **SchoolContext** 펼친 다음 **테이블**합니다.  
  
    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image18.png)
7. 마우스 오른쪽 단추로 클릭 합니다 **학생** 테이블을 클릭 **테이블 데이터 표시** 생성 된 열 및 테이블에 삽입 된 행을 볼 수 있습니다.

    ![Student 테이블](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image19.png)

## <a name="creating-a-student-controller-and-views"></a>학생 컨트롤러 및 뷰 만들기

다음 단계는 이러한 테이블 중 하나를 사용 하 여 사용할 수 있는 응용 프로그램에서 ASP.NET MVC 컨트롤러 및 뷰를 만드는 것입니다.

1. 만들려면를 `Student` 컨트롤러를 마우스 오른쪽 단추로 클릭 합니다 **컨트롤러** 폴더에 **솔루션 탐색기**을 선택 **추가**를 클릭 하 고 **컨트롤러** . 에 **컨트롤러 추가** 대화 상자에서 다음을 선택 하 고 클릭 **추가**: 

   - 컨트롤러 이름: **StudentController**합니다.
   - 템플릿: **읽기/쓰기 동작 및 Entity Framework를 사용 하 여 뷰를 사용 하 여 MVC 컨트롤러**합니다.
   - 모델 클래스: **학생 (ContosoUniversity.Models)** 합니다. (드롭다운 목록에서이 옵션을 보이지 않으면 프로젝트를 빌드 및 다시 시도 하십시오.)
   - 데이터 컨텍스트 클래스: **SchoolContext (ContosoUniversity.Models)** 합니다.
   - 보기: **Razor (CSHTML)** 합니다. (기본값입니다.)

     ![Add_Controller_dialog_box_for_Student_controller](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image20.png)
2. Visual Studio가 열립니다는 *Controllers\StudentController.cs* 파일입니다. 클래스 변수를 만든 데이터베이스 컨텍스트 개체를 인스턴스화하는 것이 표시 됩니다.

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample16.cs)]

     `Index` 동작 메서드가의 학생 들의 목록을 가져옵니다 합니다 *학생* 엔터티 집합 참조 하 여는 `Students` 데이터베이스 컨텍스트 인스턴스의 속성:

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample17.cs)]

     합니다 *Student\Index.cshtml* 보기 테이블의이 목록에 표시 됩니다.

     [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample18.cshtml)]
3. Ctrl+F5를 눌러 프로젝트를 실행합니다.

     클릭 합니다 **학생** 테스트 데이터를 보려면 탭은는 `Seed` 삽입 하는 메서드.

     ![학생 인덱스 페이지](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image21.png)

## <a name="conventions"></a>규칙

사용 했기 때문에 전체 데이터베이스를 만들 수를 Entity Framework에서 작성 해야 했던 코드의 양을 최소화 됩니다 *규칙*, 또는 Entity Framework에서 만드는 가정 합니다. 일부는 이미 설명 되어 있습니다.

- 엔터티 클래스 이름의 복수화 양식은 테이블 이름으로 사용 됩니다.
- 엔터티 속성 이름은 열 이름에 사용됩니다.
- 명명 된 엔터티 속성 `ID` 나 *classname* `ID` 기본 키 속성으로 인식 됩니다.

지금까지 살펴본 규칙을 재정의할 수 있습니다 (예를 들어 지정한 테이블 이름을 복수화 않아야는) 및 규칙과 재정의 하는 방법을 자세히 알아봅니다 합니다 [더 복잡 한 데이터 모델을 만드는](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md) 자습서 이 시리즈의 뒷부분에 나오는. 자세한 내용은 [코드의 첫 번째 규칙](https://msdn.microsoft.com/data/jj679962)합니다.

## <a name="summary"></a>요약

이제 Entity Framework 및 SQL Server Express를 사용 하 여 저장 하 고 데이터를 표시 하는 간단한 응용 프로그램을 만들었습니다. 다음 자습서의 기본 CRUD를 수행 하는 방법을 알아봅니다 (만들기, 읽기, 업데이트, 삭제) 작업입니다. 이 페이지의 맨 아래에 의견을 남길 수 있습니다. 알려주세요 자습서의이 부분을 연결 하는 방법 및 어떻게 개선 수 없습니다.

다른 Entity Framework 리소스에 대 한 링크에서 찾을 수 있습니다 합니다 [ASP.NET 데이터 액세스 콘텐츠 맵](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.

> [!div class="step-by-step"]
> [다음](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)
