---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
title: Entity Framework 6 Code First MVC 5를 사용 하 여 시작 | Microsoft Docs
author: tdykstra
ms.author: riande
ms.date: 12/04/2018
ms.assetid: 00bc8b51-32ed-4fd3-9745-be4c2a9c1eaf
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: c7ab9458f83e05af84f72d9a2519a8c1c39b84b5
ms.sourcegitcommit: 9bb58d7c8dad4bbd03419bcc183d027667fefa20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/04/2018
ms.locfileid: "52861435"
---
# <a name="get-started-with-entity-framework-6-code-first-using-mvc-5"></a>Entity Framework 6 Code First MVC 5를 사용 하 여 시작

[Tom Dykstra](https://github.com/tdykstra)

[완료 된 프로젝트 다운로드](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8)

> [!NOTE]
> 새 개발을 위한 것이 좋습니다 [ASP.NET Core Razor 페이지](/aspnet/core/razor-pages) ASP.NET MVC 컨트롤러 및 뷰를 통해. 이 이와 유사한 자습서 시리즈는 Razor 페이지에 사용할 수는 [Razor 페이지 자습서](/aspnet/core/tutorials/razor-pages/razor-pages-start):
>
> * 자습서 내용을 좀 더 쉽게 진행할 수 있습니다.
> * 더 많은 EF Core 모범 사례를 제공합니다.
> * 더 효율적인 쿼리를 사용합니다.
> * 최신 API가 탑재되어 최신 상태입니다.
> * 더 많은 기능을 다룹니다.
> * 새 응용 프로그램 개발을 위해 선호되는 방법입니다.

> 이 문서에는 Entity Framework 6 및 Visual Studio를 사용 하 여 ASP.NET MVC 5 응용 프로그램을 만드는 방법을 보여 줍니다. 이 자습서에서는 Code First 워크플로 사용 합니다. Code First, Database First 및 Model First 중에서 선택 하는 방법에 대 한 자세한 내용은 [모델을 만드는](/ef/ef6/modeling/)합니다.
>
> 샘플 응용 프로그램은 가상 Contoso University 라는 university에 대 한 웹 사이트입니다. 학생 입학, 강좌 개설 및 강사 할당과 같은 기능이 있습니다. 이 자습서 시리즈에는 Contoso University 샘플 응용 프로그램을 빌드하는 방법을 설명 합니다. 할 수 있습니다 [완성된 된 응용 프로그램 다운로드](https://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8)합니다.
>
> Mike Brind에서 변환 하는 Visual Basic 버전을 사용할 수: [MVC 5를 Visual Basic의 EF 6](http://www.mikesdotnetting.com/Article/241/MVC-5-with-EF-6-in-Visual-Basic-Creating-an-Entity-Framework-Data-Model) Mikesdotnetting 사이트입니다.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - [Entity Framework 6](https://www.nuget.org/packages/EntityFramework)
> - [Windows Azure SDK 2.2](https://go.microsoft.com/fwlink/p/?linkid=323510) (선택 사항)
>
> ## <a name="tutorial-versions"></a>자습서 버전
>
> 이 자습서의 이전 버전에 대 한 참조 [EF 4.1 / MVC 3 전자책](https://social.technet.microsoft.com/wiki/contents/articles/11608.e-book-gallery-for-microsoft-technologies.aspx#GettingStartedwiththeEntityFramework4.1usingASP.NETMVC) 하 고 [MVC 4를 사용 하 여 EF 5 시작](../../older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다.
>
> ## <a name="questions-and-comments"></a>질문이 나 의견이 있으면
>
> 이 자습서와 연결 하는 방법에 의견을 남겨 주세요 페이지의 맨 아래에서 주석을 사용 하 여 개선할 수 있습니다. 에 자습서로 직접 관련 되지 않은 질문이 있을 경우 게시할 수 하는 [ASP.NET Entity Framework 포럼](https://forums.asp.net/1227.aspx) 또는 [StackOverflow.com](http://stackoverflow.com/)합니다.
>
> 해결할 수 없는 문제를 실행 하는 경우 다운로드할 수 있는 완성 된 프로젝트에 코드를 비교 하 여 일반적으로 문제에 솔루션을 찾을 수 있습니다. 몇 가지 일반적인 오류 및 해결 방법을 참조 하세요 [일반적인 오류 해결 방법 또는](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)합니다.

## <a name="the-contoso-university-web-app"></a>Contoso University 웹앱

이 자습서에서 빌드할 응용 프로그램은 간단한 대학 웹 사이트입니다. 사용자는 학생, 강좌 및 강사 정보를 보고 업데이트할 수 있습니다. 만든 화면 중 몇 가지는 다음과 같습니다.

![Students_Index_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image1.png)

![학생 편집](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image2.png)

자습서 Entity Framework를 사용 하는 방법에 주로 초점을 맞출 수 있도록 웹 사이트의 사용자 인터페이스 않습니다 변경할 수 많은 정보를 새로운 기본 제공 템플릿에서 생성 됩니다.

## <a name="prerequisites"></a>전제 조건

참조 **소프트웨어 버전** 페이지의 맨 위에 있는 합니다. Entity Framework 6 아니므로 필수 구성 요소 자습서의 일부로 EF NuGet 패키지를 설치 합니다.

## <a name="create-an-mvc-web-app"></a>MVC 웹 앱 만들기

1. Visual Studio를 열고 새 만들기 C# 웹 프로젝트를 **ASP.NET 웹 응용 프로그램 (.NET Framework)** 템플릿. "ContosoUniversity" 프로젝트를 이름을 지정 합니다.

   ![Visual Studio에서 새 프로젝트 대화 상자](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/new-project-dialog.png)

2. 새 ASP.NET 프로젝트 대화 상자에서 선택 합니다 **MVC** 템플릿.

   ![Visual Studio에서 새 웹 앱 대화 상자](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/new-web-app-dialog.png)

3. 하는 경우 **인증** 로 설정 되어 있지 **인증 안 함**를 클릭 하 여 변경할 **인증 변경**합니다.

   에 **인증 변경** 대화 상자에서 **인증 안 함**를 선택한 후 **확인**합니다. 이 자습서에서는 웹 앱에 로그인 할 필요가 없으며 누가 로그인에 따라 액세스 제한.

   ![Visual Studio에서 인증 대화 상자 변경](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/change-authentication.png)

4. 새 ASP.NET 프로젝트 대화 상자에서 다시 **확인** 프로젝트를 만듭니다.

## <a name="set-up-the-site-style"></a>사이트 스타일 설정

몇 가지 간단한 변경 내용으로 사이트 메뉴, 레이아웃 및 홈 페이지를 설정합니다.

1. 오픈 *Views\Shared\\_Layout.cshtml*를 다음과 같이 변경 하 고:

   - "Contoso University"를 "My ASP.NET Application" 및 "Application name"로 변경 합니다.
   - 학생, 강좌, 강사, 및 부서에 대 한 메뉴 항목을 추가 하 고 연락처 항목을 삭제 합니다.

   다음 코드 조각에서 변경 내용은 강조 표시 됩니다.

   [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample1.cshtml?highlight=6,19,24-27,38)]

2. *Views\Home\Index.cshtml*,이 응용 프로그램에 대 한 텍스트를 사용 하 여 ASP.NET 및 MVC에 대 한 텍스트를 바꾸려면 다음 코드로 파일의 내용을 바꿉니다.

   [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample2.cshtml)]

3. 키를 눌러 **Ctrl**+**F5** 웹 사이트를 실행 합니다. 주 메뉴를 사용 하 여 홈 페이지가 표시 됩니다.

   ![Contoso University 홈페이지](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image6.png)

## <a name="install-entity-framework-6"></a>Entity Framework 6를 설치 합니다.

1. **도구** 메뉴 선택 **NuGet 패키지 관리자**를 선택한 후 **패키지 관리자 콘솔**합니다.

2. 에 **패키지 관리자 콘솔** 창에서 다음 명령을 입력 합니다.

   ```text
   Install-Package EntityFramework
   ```

   ![EF 설치](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image7.png)

   이미지 설치 되 고 6.0.0 보여주지만 NuGet 설치할지 최신 버전 (시험판 버전 제외), Entity Framework의 최신 자습서 업데이트를 기준으로 6.2.0입니다.

이 단계를 수행 하기 위해 자동으로 ASP.NET MVC 스 캐 폴딩 기능별 있지만이 자습서에는 수동으로 작업을 수행할 수 있는 몇 가지 단계 중 하나입니다. EF (Entity Framework)를 사용 하는 데 필요한 단계를 볼 수 있도록 수동으로 수행 하 고 있습니다. 스 캐 폴딩 MVC 컨트롤러 및 뷰를 만들려면 나중에 사용 합니다. 스 캐 폴딩 자동으로 EF NuGet 패키지를 설치할 데이터베이스 컨텍스트 클래스를 만들고 연결 문자열을 만들 수 있도록 것이 좋습니다. 이런 방식으로 작업을 수행 하는 준비 된 경우 수행 해야 하는 모든 경우 이러한 단계를 건너뛰고 엔터티 클래스를 만든 후에 MVC 컨트롤러를 스 캐 폴드

## <a name="create-the-data-model"></a>데이터 모델 만들기

다음으로 Contoso University 응용 프로그램에 대한 엔터티 클래스를 만듭니다. 다음 세 가지 엔터티를 사용 하 여 시작할 수 있습니다.

![Class_diagram](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image8.png)

`Student` 및 `Enrollment` 엔터티 간에 일대다 관계가 있으며 `Course` 및 `Enrollment` 엔터티 간에 일대다 관계가 있습니다. 즉, 학생은 개수에 관계 없이 강좌에 등록될 수 있으며 강좌는 등록된 학생이 여러 명일 수 있습니다.

다음 섹션에서는 이러한 엔터티 각각에 대 한 클래스를 만들어야 합니다.

> [!NOTE]
> 이러한 엔터티 클래스의 모든 만들기를 완료 하기 전에 프로젝트를 컴파일할 하려고 하면 컴파일러 오류를 얻게 됩니다.

### <a name="the-student-entity"></a>학생 엔터티

![Student_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image9.png)

- 에 *모델* 폴더를 라는 클래스 파일을 만듭니다 *Student.cs* 폴더를 마우스 오른쪽 단추로 클릭 하 여 **솔루션 탐색기** 선택 하 고 **추가**  >  **클래스**합니다. 템플릿 코드를 다음 코드로 바꿉니다.

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample3.cs)]

`ID` 속성은 이 클래스에 해당하는 데이터베이스 테이블의 기본 키 열이 됩니다. 기본적으로 Entity Framework는 명명 된 속성을 해석 `ID` 나 *classname* `ID` 기본 키로 합니다.

`Enrollments` 속성은 *탐색 속성*입니다. 탐색 속성은 이 엔터티와 관련된 다른 엔터티를 포함합니다. 이 경우에 `Enrollments` 의 속성을 `Student` 엔터티 모두 보유할를 `Enrollment` 는 관련 된 엔터티 `Student` 엔터티. 즉, 경우를 지정 `Student` 데이터베이스의 행에는 관련 된 두 개의 `Enrollment` 행 (해당 학생의 기본 키를 포함 하는 행 값을 해당 `StudentID` 외래 키 열), 해당 `Student` 엔터티의 `Enrollments` 탐색 속성 이러한 두 사용 될 `Enrollment` 엔터티.

탐색 속성은 일반적으로 정의 됩니다 `virtual` 를 같은 특정 Entity Framework 기능을 취할 수 있습니다 *지연 로딩*합니다. (지연 로딩에 설명의 뒷부분에 나오는 합니다 [관련 데이터를 읽는](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) 이 시리즈의 뒷부분에 나오는 자습서입니다.)

탐색 속성이 여러 엔터티를 포함할 수 있는 경우(다대다 또는 일대다 관계로), 해당 형식은 `ICollection`와 같이 항목이 추가, 삭제 및 업데이트될 수 있는 목록이어야 합니다.

### <a name="the-enrollment-entity"></a>등록 엔터티

![Enrollment_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image10.png)

- *Models* 폴더에서*Enrollment.cs*를 만들고 기존 코드를 다음 코드로 바꿉니다.

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample4.cs)]

`EnrollmentID` 속성을 기본 키 수,이 엔터티는 합니다 *classname* `ID` 대신 패턴 `ID` 에서 본 것 자체로 `Student` 엔터티. 일반적으로 하나의 패턴을 선택하고 이를 데이터 모델 전체에서 사용합니다. 여기에서 변형은 패턴 중 하나를 사용할 수 있음을 보여 줍니다. 자습서의 뒷부분에서 볼 수 방법을 `ID` 없이 `classname` 데이터 모델에서 상속을 구현 하기가 쉬워집니다.

합니다 `Grade` 속성은는 [enum](/ef/ef6/modeling/code-first/data-types/enums)합니다. 후 물음표 합니다 `Grade` 형식 선언을 나타냅니다는 `Grade` 속성은 [nullable](/dotnet/csharp/programming-guide/nullable-types/using-nullable-types)합니다. Null 인 등급은 0 등급과 다릅니다-null 성적 알려질 하거나 아직 할당 되지 않은 것을 의미 합니다.

`StudentID` 속성은 외래 키로, 해당 탐색 속성은 `Student`입니다. `Enrollment` 엔터티는 하나의 `Student` 엔터티와 연결되어 있으므로 속성은 단일 `Student` 엔터티만 포함할 수 있습니다(이전에 살펴본 여러 `Enrollment` 엔터티를 포함할 수 있는 `Student.Enrollments` 탐색 속성과 달리).

`CourseID` 속성은 외래 키로, 해당 탐색 속성은 `Course`입니다. `Enrollment` 엔터티는 하나의 `Course` 엔터티와 연결됩니다.

엔터티 프레임 워크 라고 하는 경우 외래 키 속성으로 속성을 해석 *&lt;탐색 속성 이름을&gt;&lt;기본 키 속성 이름&gt;* (예를 들어 `StudentID`에 대 한 합니다 `Student` 이후의 탐색 속성을 `Student` 엔터티의 기본 키가 `ID`). 외래 키 속성 수도 같은 이름 단순히 *&lt;기본 키 속성 이름&gt;* (예를 들어 `CourseID` 이므로 합니다 `Course` 엔터티의 기본 키가 `CourseID`).

### <a name="the-course-entity"></a>강좌 엔터티

![Course_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image11.png)

- 에 *모델* 폴더를 만듭니다 *Course.cs*, 템플릿 코드를 다음 코드로 바꾸어:

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample5.cs)]

`Enrollments` 속성은 탐색 속성입니다. `Course` 엔터티는 `Enrollment` 엔터티의 개수와 관련이 있을 수 있습니다.

클릭 합니다. 자세한 정보는 <xref:System.ComponentModel.DataAnnotations.Schema.DatabaseGeneratedAttribute> 이 시리즈의 자습서의 뒷부분에서 특성입니다. 기본적으로 이 특성을 통해 생성하는 데이터베이스를 갖는 대신 강좌에 대한 기본 키를 입력할 수 있습니다.

## <a name="create-the-database-context"></a>데이터베이스 컨텍스트 만들기

지정 된 데이터 모델에 대 한 Entity Framework 기능을 조정 하는 주 클래스는 합니다 *데이터베이스 컨텍스트* 클래스입니다. 이 클래스에서 파생 하 여 만든 합니다 [System.Data.Entity.DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.113).aspx) 클래스입니다. 코드는 엔터티 데이터 모델에 포함 된 지정 합니다. 특정 Entity Framework 동작을 사용자 지정할 수도 있습니다. 이 프로젝트에서 클래스 이름은 `SchoolContext`로 지정됩니다.

- 프로젝트를 마우스 오른쪽 단추로 클릭 ContosoUniversity 프로젝트에서 폴더를 만들려고 **솔루션 탐색기** 클릭 **추가**를 클릭 하 고 **새 폴더**합니다. 새 폴더의 이름을 *DAL* (데이터 액세스 계층)에 대 한 합니다. 해당 폴더에서 이라는 새 클래스 파일을 만듭니다 *SchoolContext.cs*, 템플릿 코드를 다음 코드로 바꿉니다.

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample6.cs)]

### <a name="specify-entity-sets"></a>엔터티 집합을 지정 합니다.

이 코드에서는 한 [DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.113).aspx) 각 엔터티 집합에 대 한 속성입니다. Entity Framework 용어에서는 *엔터티 집합* 일반적으로 데이터베이스 테이블에 해당와 *엔터티* 테이블의 행에 해당 합니다.

> [!NOTE]
>
> 생략할 수 있습니다 합니다 `DbSet<Enrollment>` 및 `DbSet<Course>` 문과 것은 동일 하 게 작동 합니다. Entity Framework는를 암시적으로 포함 하기 때문에 `Student` 엔터티 참조를 `Enrollment` 엔터티 및 `Enrollment` 엔터티 참조는 `Course` 엔터티.

### <a name="specify-the-connection-string"></a>연결 문자열 지정

(나중에 추가할 Web.config 파일에)이 표시 되는 연결 문자열의 이름은 생성자에 전달 됩니다.

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample7.cs?highlight=1)]

또한 Web.config 파일에 저장 된 이름 대신 연결 문자열 자체에 전달할 수 있습니다. 사용 하 여 데이터베이스를 지정 하기 위한 옵션에 대 한 자세한 내용은 참조 하세요. [연결 문자열 및 모델](/ef/ef6/fundamentals/configuring/connection-strings)합니다.

하나의 이름이 나 연결 문자열을 명시적으로 지정 하지 않으면, Entity Framework 연결 문자열 이름이 클래스 이름과 동일 이라고 가정 합니다. 이 예제에서 기본 연결 문자열 이름을 같게 됩니다. `SchoolContext`를 명시적으로 지정 하는 항목 동일 합니다.

### <a name="specify-singular-table-names"></a>단 수 테이블 이름을 지정 합니다.

합니다 `modelBuilder.Conventions.Remove` 문에서 [OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx) 메서드는 테이블 이름을 복수화 되에서 않도록 합니다. 데이터베이스에서 생성된 된 테이블 이름은이 수행 하지 않은 경우 `Students`, `Courses`, 및 `Enrollments`합니다. 테이블 이름 대신 됩니다 `Student`, `Course`, 및 `Enrollment`합니다. 개발자는 테이블 이름을 복수화할지 여부에 대해 동의하지 않습니다. 이 자습서에서는 단 수 형태를 사용 하지만 중요 한 점은 포함 하거나 코드이 줄을 생략 하 여 원하는 어떤 폼을 선택할 수 있습니다.

## <a name="set-up-ef-to-initialize-the-database-with-test-data"></a>테스트 데이터로 데이터베이스를 초기화 하려면 EF 설정

Entity Framework 수 자동으로 만듭니다 (또는 삭제 및 다시 만들기) 하는 응용 프로그램을 실행 하는 경우에 대 한 데이터베이스입니다. 이 작업은 응용 프로그램이 실행 될 때마다 또는 모델은 기존 데이터베이스와 동기화 하는 경우에 지정할 수 있습니다. 작성할 수도 있습니다는 `Seed` 메서드는 Entity Framework 테스트 데이터로 채우기 위해 데이터베이스를 만든 후 자동으로 호출 합니다.

기본 동작은 해당 하지 않습니다 (있으며 모델 변경 되었으며이 데이터베이스가 이미 있는 경우 예외를 throw) 하는 경우에 데이터베이스를 만들 수 있습니다. 이 섹션에서는 데이터베이스 삭제 후 모델이 변경 될 때마다 다시 생성을 지정 합니다. 데이터베이스를 삭제 하면 모든 데이터가 손실이 됩니다. 이 일반적으로 이제 개발 하는 동안 때문에 `Seed` 데이터베이스 다시 생성 되 고 다시 테스트 데이터 생성 하는 경우 메서드가 실행 됩니다. 그러나 프로덕션 환경에서 일반적으로 원하지 데이터베이스 스키마를 변경 해야 할 때마다 모든 데이터를 보호 합니다. 나중에 삭제 하 고 데이터베이스를 다시 작성 하는 대신 데이터베이스 스키마를 변경 하려면 Code First 마이그레이션을 사용 하 여 모델 변경 내용을 처리 하는 방법을 배웁니다.

1. DAL 폴더 라는 새 클래스 파일을 만듭니다 *SchoolInitializer.cs* 템플릿 코드는 필요할 때 데이터베이스를 다음 코드로 바꿉니다 하 고 로드를 새 데이터베이스로 데이터를 테스트 합니다.

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample8.cs)]

   `Seed` 메서드는 입력된 매개 변수로 데이터베이스 컨텍스트 개체를 사용 하 고 메서드에서 코드를 해당 개체를 사용 하 여 데이터베이스에 새 엔터티를 추가 합니다. 각 엔터티 형식에 대 한 코드는 새 엔터티 컬렉션을 만듭니다, 적절 한 추가 `DbSet` 속성 및 데이터베이스에 변경 내용 저장 합니다. 호출할 필요가 없습니다를 `SaveChanges` 엔터티의 각 그룹 뒤 메서드를으로 여기에서 수행 되지만 코드는 데이터베이스에 쓰는 동안 예외가 발생 하는 경우 문제의 소스를 찾을 수 있습니다 작업을 수행 합니다.

2. Entity Framework 이니셜라이저 클래스를 사용 하 게 요소를 추가 합니다 `entityFramework` 응용 프로그램에서 요소 *Web.config* 파일 (파일의 루트 프로젝트 폴더에서), 다음 예와에서 같이:

   [!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample9.xml?highlight=2-6)]

   합니다 `context type` 정규화 된 상황에 맞는 클래스 이름 및 어셈블리에 지정 및 `databaseinitializer type` 이니셜라이저 클래스와 있는 어셈블리의 정규화 된 이름을 지정 합니다. (이니셜라이저를 사용 하는 EF를 사용 하지 않으려는 경우에 특성을 설정할 수 있습니다 합니다 `context` 요소: `disableDatabaseInitialization="true"`.) 자세한 내용은 [구성 파일 설정](/ef/ef6/fundamentals/configuring/config-file)합니다.

   이니셜라이저를 설정 하는 대신 합니다 *Web.config* 파일을 추가 하 여 코드에서 수행 하려면을 `Database.SetInitializer` 문을 `Application_Start` 에서 메서드를 *Global.asax.cs* 파일. 자세한 내용은 [Entity Framework Code first 데이터베이스 이니셜라이저 이해](http://www.codeguru.com/csharp/article.php/c19999/Understanding-Database-Initializers-in-Entity-Framework-Code-First.htm)합니다.

응용 프로그램은 이제 설정 하 여 응용 프로그램의 지정 된 실행에서 처음으로 데이터베이스에 액세스 하는 경우 Entity Framework 모델 데이터베이스를 비교 (프로그램 `SchoolContext` 및 엔터티 클래스). 차이가 있으면 응용 프로그램을 삭제 하 고 다시 데이터베이스를 만듭니다.

> [!NOTE]
> 프로덕션 웹 서버에 응용 프로그램을 배포한 경우 제거 하거나 삭제 되 고 데이터베이스를 다시 생성 하는 코드를 사용 하지 않도록 설정 해야 합니다. 이 시리즈의 자습서의 뒷부분에서 할 수 있습니다.

## <a name="set-up-ef-to-use-a-sql-server-express-localdb-database"></a>EF는 SQL Server Express LocalDB 데이터베이스를 사용 하도록 설정

[LocalDB](/sql/database-engine/configure-windows/sql-server-2016-express-localdb?view=sql-server-2017) SQL Server Express 데이터베이스 엔진의 경량 버전입니다. 설치 및 구성 하는 작업을 쉽게, 요청 시 시작 하며 사용자 모드에서 실행 됩니다. LocalDB 데이터베이스를 사용 하 여 작업할 수 있도록 하는 SQL Server Express의 특수 실행 모드에서 실행 *.mdf* 파일입니다. LocalDB 데이터베이스 파일에 넣을 수 있습니다 합니다 *앱\_데이터* 프로젝트를 사용 하 여 데이터베이스를 복사할 수 있게 되기를 원하는 경우 웹 프로젝트의 폴더입니다. SQL Server express 사용자 인스턴스 기능 또한 작업할 수 있습니다 *.mdf* 파일을 하지만 사용자 인스턴스 기능 사용 되지 않으면 따라서 LocalDB가 사용 하기 위한 권장 *.mdf* 파일입니다. LocalDB는 Visual Studio를 사용 하 여 기본적으로 설치 됩니다.

일반적으로 SQL Server Express 프로덕션 웹 응용 프로그램에 대 한 사용 되지 않습니다. LocalDB 특히 권장 되지 않습니다 웹 응용 프로그램의 프로덕션 사용에 대 한 iis 기능이 없는 때문에.

- 이 자습서에서는 LocalDB를 작업할 수 있습니다. 응용 프로그램을 엽니다 *Web.config* 파일을 추가 `connectionStrings` 요소 앞의 `appSettings` 요소를 다음 예제에서와 같이 합니다. (업데이트 해야 합니다 *Web.config* 루트 프로젝트 폴더의 파일입니다. 도 *Web.config* 파일을 *뷰* 하위 폴더를 업데이트할 필요가 없습니다.)

   [!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample10.xml?highlight=1-3)]

Entity Framework는 명명 된 LocalDB 데이터베이스를 사용 하 여 추가한 다음 연결 문자열 지정 *ContosoUniversity1.mdf*합니다. (데이터베이스가 아직 존재 하지 않지만 EF에서 만듭니다.) 데이터베이스를 만들려는 경우에 *앱\_데이터* 폴더를 추가할 수 있습니다 `AttachDBFilename=|DataDirectory|\ContosoUniversity1.mdf` 연결 문자열입니다. 연결 문자열에 대 한 자세한 내용은 참조 하세요. [ASP.NET 웹 응용 프로그램에 대 한 SQL Server 연결 문자열](/previous-versions/aspnet/jj653752(v=vs.110))합니다.

연결 문자열을 실제로 필요 하지는 *Web.config* 파일입니다. 연결 문자열을 지정 하지 않으면, Entity Framework 컨텍스트 클래스를 기반으로 기본 연결 문자열을 사용 합니다. 자세한 내용은 [Code First 새 데이터베이스로](/ef/ef6/modeling/code-first/workflows/new-database)합니다.

## <a name="create-a-student-controller-and-views"></a>학생 컨트롤러 및 뷰 만들기

이제 데이터를 표시할 웹 페이지를 만들어야 합니다. 데이터를 자동으로 요청 프로세스를 데이터베이스의 생성을 트리거합니다. 새 컨트롤러를 만들어 시작할 수 있습니다. 하지만 그렇게 하기 전에 모델 및 상황에 맞는 클래스를 MVC 컨트롤러 스 캐 폴딩 가능 프로젝트를 빌드합니다.

1. 마우스 오른쪽 단추로 클릭 합니다 **컨트롤러** 폴더에 **솔루션 탐색기**를 선택 **추가**를 클릭 하 고 **새 스 캐 폴드 된 항목**합니다.
2. 에 **스 캐 폴드 추가** 대화 상자에서 **Entity Framework를 사용 하 여 뷰를 사용 하 여 MVC 5 컨트롤러**를 선택한 후 **추가**합니다.

     ![Visual Studio에서 스 캐 폴드 대화 상자 추가](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/add-scaffold.png)

3. 에 **컨트롤러 추가** 대화 상자에서 다음 옵션을 선택 하 고 선택한 **추가**:

   - 모델 클래스: **학생 (ContosoUniversity.Models)** 합니다. (드롭다운 목록에서이 옵션을 보이지 않으면 프로젝트를 빌드 및 다시 시도 하십시오.)
   - 데이터 컨텍스트 클래스: **SchoolContext (ContosoUniversity.DAL)** 합니다.
   - 컨트롤러 이름: **StudentController** (없습니다 StudentsController).
   - 다른 필드에 대 한 기본값을 그대로 둡니다.

     ![컨트롤러 추가 대화 상자에서 Visual Studio](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/add-controller.png)

     클릭 하면 **추가**를 스 캐 폴더를 만듭니다를 *StudentController.cs* 파일과 뷰 집합 (*.cshtml* 파일) 컨트롤러와 작동 하는 합니다. 나중에 Entity Framework를 사용 하는 프로젝트를 만든 경우 있습니다도 활용을 스 캐 폴더의 몇 가지 추가 기능: 첫 번째 모델 클래스를 만들고, 연결 문자열을 만들지 한 다음는 **컨트롤러 추가** 상자 지정 **새 데이터 컨텍스트에** 선택 하 여 합니다 **+** 옆 **데이터 컨텍스트 클래스**합니다. 캐 만들어집니다 프로그램 `DbContext` 뿐만 아니라 컨트롤러 및 뷰 클래스 및 연결 문자열입니다.
4. Visual Studio가 열립니다는 *Controllers\StudentController.cs* 파일입니다. 클래스 변수를 이미 만들었다고 데이터베이스 컨텍스트 개체를 인스턴스화하는 것이 표시 됩니다.

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

     `Index` 동작 메서드가의 학생 들의 목록을 가져옵니다 합니다 *학생* 엔터티 집합 참조 하 여는 `Students` 데이터베이스 컨텍스트 인스턴스의 속성:

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

     합니다 *Student\Index.cshtml* 보기 테이블의이 목록에 표시 됩니다.

     [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample13.cshtml)]
5. 키를 눌러 **Ctrl**+**F5** 프로젝트를 실행 합니다. ("섀도 복사본을 만들 수 없습니다" 오류가 발생할 경우 브라우저를 닫고 다시 시도 하십시오.)

     클릭 합니다 **학생** 테스트 데이터를 보려면 탭은는 `Seed` 삽입 하는 메서드. 폭에 따라 브라우저 창을 인 상위 주소 표시줄에 학생 탭 링크가 표시 또는 링크를 보기 위해 오른쪽 위 모서리를 클릭 해야 합니다.

     ![메뉴 단추](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image14.png)

     ![학생 인덱스 페이지](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image15.png)

## <a name="view-the-database"></a>데이터베이스 뷰

학생 페이지를 실행 하 고 응용 프로그램 데이터베이스에 액세스 하려고 한 경우 EF 데이터베이스가 없는 한 만들지를 검색 합니다. EF는 다음 데이터를 사용 하 여 데이터베이스를 채우는 데 시드 메서드를 실행 합니다.

사용할 수 있습니다 **서버 탐색기** 하거나 **SQL Server 개체 탐색기** (SSOX) Visual Studio에서 데이터베이스를 봅니다. 이 자습서에서는 사용할지 **서버 탐색기**합니다.

1. 브라우저를 닫습니다.
2. **서버 탐색기**를 확장 하 고 **데이터 연결** (먼저 새로 고침 단추를 선택 해야 할 수 있습니다), 확장 **학교 컨텍스트 (ContosoUniversity)** 를 펼친 다음  **테이블** 에 새 데이터베이스의 테이블을 확인 합니다.

    ![서버 탐색기에서 데이터베이스 테이블](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image16.png)

3. 마우스 오른쪽 단추로 클릭 합니다 **학생** 테이블을 클릭 **테이블 데이터 표시** 생성 된 열 및 테이블에 삽입 된 행을 볼 수 있습니다.

    ![Student 테이블](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/table-data.png)
4. 닫기 합니다 **서버 탐색기** 연결 합니다.

*ContosoUniversity1.mdf* 하 고 *.ldf* 데이터베이스 파일에는 *% USERPROFILE %* 폴더.

사용 중 이므로 합니다 `DropCreateDatabaseIfModelChanges` 이니셜라이저를 만들 수 있습니다 이제 변경은 `Student` 클래스 다시 응용 프로그램을 실행 하 고 데이터베이스는 자동으로 변경 내용에 맞도록으로 다시 생성 됩니다. 예를 들어, 추가 하는 경우는 `EmailAddress` 속성을 `Student` 클래스, 학생 페이지를 다시 실행 한 다음 표에서 다시를 살펴보려면 보면 새 `EmailAddress` 열입니다.

## <a name="conventions"></a>규칙

전체 데이터베이스를 만들 수를 Entity Framework에서 작성 해야 했던 코드의 양을 때문에 최소화 됩니다 *규칙*, 또는 Entity Framework에서 만드는 가정 합니다. 그 중 일부 메모해 두어야 이미 또는 되 고 인식 없이 사용 되었습니다.

- 엔터티 클래스 이름의 복수화 양식은 테이블 이름으로 사용 됩니다.
- 엔터티 속성 이름은 열 이름에 사용됩니다.
- 명명 된 엔터티 속성 `ID` 나 *classname* `ID` 기본 키 속성으로 인식 됩니다.
- 라고 하는 경우 외래 키 속성으로는 속성을 해석 *&lt;탐색 속성 이름을&gt;&lt;기본 키 속성 이름&gt;* (예를 들어 `StudentID` 합니다 에대한`Student` 이후의 탐색 속성을 `Student` 엔터티의 기본 키가 `ID`). 외래 키 속성 수도 같은 이름 단순히 &lt;기본 키 속성 이름&gt; (예를 들어 `EnrollmentID` 되므로 합니다 `Enrollment` 엔터티의 기본 키가 `EnrollmentID`).

규칙을 재정의할 수 있음을 확인 했습니다. 예를 들어 지정한 테이블 이름을 복수화 하지 않아야, 나중에 볼 수 명시적으로 외래 키 속성으로 속성을 표시 하는 방법입니다. 규칙 및 재정의에 해당 하는 방법을 자세히 알아봅니다 합니다 [더 복잡 한 데이터 모델을 만드는](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md) 이 시리즈의 뒷부분에 나오는 자습서입니다. 규칙에 대 한 자세한 내용은 참조 하세요. [코드의 첫 번째 규칙](/ef/ef6/modeling/code-first/conventions/built-in)합니다.

## <a name="summary"></a>요약

Entity Framework 및 SQL Server Express LocalDB를 사용 하 여 저장 하 고 데이터를 표시 하는 간단한 응용 프로그램을 만들었습니다. 다음에서 기본 수행 하는 방법을 알아봅니다 자습서 만들기, 읽기, 업데이트 및 삭제 (CRUD) 작업 합니다.

이 자습서를 연결 하는 방법을 개선할 수 것에 의견을 남겨 주세요.

다른 Entity Framework 리소스에 대 한 링크에서 찾을 수 있습니다 [ASP.NET 데이터 액세스-권장 리소스](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.

> [!div class="step-by-step"]
> [다음](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)
