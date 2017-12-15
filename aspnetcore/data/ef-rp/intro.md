---
title: "Entity Framework Core-8 자습서 1 사용 하 여 razor 페이지"
author: rick-anderson
description: "Entity Framework Core를 사용 하 여 Razor 페이지 앱을 만드는 방법을 보여 줍니다."
keywords: "ASP.NET Core, Entity Framework Core 자습서"
ms.author: riande
manager: wpickett
ms.date: 11/15/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: data/ef-rp/intro
ms.openlocfilehash: 571d683636244565b184cfec49061ec656377f11
ms.sourcegitcommit: 198fb0488e961048bfa376cf58cb853ef1d1cb91
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="getting-started-with-razor-pages-and-entity-framework-core-using-visual-studio-1-of-8"></a>Razor 페이지 및 Visual Studio (1 / 8)를 사용 하 여 Entity Framework Core 시작

여 [Tom Dykstra](https://github.com/tdykstra) 및 [Rick Anderson](https://twitter.com/RickAndMSFT)

Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework (EF) 코어 2.0 및 Visual Studio 2017을 사용 하 여 ASP.NET 코어 2.0 MVC 웹 응용 프로그램을 만드는 방법을 보여 줍니다.

샘플 응용 프로그램은 웹 사이트 가상 Contoso 대학입니다. 학생 진입, 과정 만들기 및 강사 할당 등의 기능을 포함합니다. 이 페이지는 일련의 Contoso 대학 샘플 응용 프로그램을 빌드하는 방법을 설명 하는 자습서의 첫 번째 작업이 있습니다.

[완성 된 앱을 보거나 다운로드.](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples) [다운로드 지침](xref:tutorials/index#how-to-download-a-sample)합니다.

## <a name="prerequisites"></a>필수 구성 요소

[!INCLUDE[install 2.0](../../includes/install2.0.md)]

## <a name="troubleshooting"></a>문제 해결

솔루션에 코드를 비교 하 여 일반적으로 찾을 수 문제를 해결할 수 없는 실행 하는 경우는 [단계 완료](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots) 또는 [완료 된 프로젝트](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/cu-final)합니다. 일반적인 오류 및 해결 방법을 목록은 참조 하십시오. [계열의 마지막 자습서의 문제 해결 섹션](xref:data/ef-mvc/advanced#common-errors)합니다. 에 대 한 StackOverflow.com에 질문을 게시할 수 필요한 있습니다을 찾지 못한 경우 [ASP.NET Core](https://stackoverflow.com/questions/tagged/asp.net-core) 또는 [EF 코어](https://stackoverflow.com/questions/tagged/entity-framework-core)합니다.

> [!TIP]
> 이 일련의 자습서 이전 자습서에서 수행 되는 동작과 기반으로 합니다. 각 자습서 완료 후 프로젝트의 복사본을 저장 하는 것이 좋습니다. 문제를 실행 하는 경우 시작 부분으로 다시 이동 하지 않고도 이전 자습서에서를 통해 시작할 수 있습니다. 다운로드할 수 있습니다는 [단계 완료](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots) 고 완료 된 단계를 사용 하 여 다시 시작 합니다.

## <a name="the-contoso-university-web-app"></a>Contoso 대학 웹 응용 프로그램

이 자습서에 빌드한 앱에는 기본 대학 웹 사이트입니다.

사용자가 볼 수 있으며 학생과에서는 강사 정보 업데이트 됩니다. 자습서에서 만든 화면 중 몇 가지 예입니다.

![학생 인덱스 페이지](intro/_static/students-index.png)

![학생 편집 페이지](intro/_static/student-edit.png)

이 사이트의 사용자 인터페이스 스타일에는 기본 제공 템플릿에서 생성 내용을 가깝습니다. Razor 페이지 되지 않는 UI EF 코어 자습서 위주로 설명 됩니다.

## <a name="create-a-razor-pages-web-app"></a>Razor 페이지 웹 앱 만들기

* Visual Studio **파일** 메뉴에서 **새로 만들기** > **프로젝트**를 선택합니다.
* 새 ASP.NET Core 웹 응용 프로그램을 만듭니다. 프로젝트 이름을 **ContosoUniversity**합니다. 프로젝트 이름을 해야 *ContosoUniversity* 되므로 코드를 복사/붙여 넣을 때 네임 스페이스와 일치 합니다.
 ![새 ASP.NET Core 웹 응용 프로그램](intro/_static/np.png)
* 드롭다운에서 **ASP.NET Core 2.0**을 선택하고 **웹 응용 프로그램**을 선택합니다.
 ![웹 응용 프로그램(Razor 페이지)](../../mvc/razor-pages/index/_static/np2.png)

**F5** 키를 눌러 디버그 모드에서 앱을 실행하거나 **Ctrl-F5**를 눌러 디버거를 연결하지 않고 실행합니다.

## <a name="set-up-the-site-style"></a>사이트 스타일 설정

몇 가지 변경을 사이트 메뉴, 레이아웃 및 홈 페이지를 설정합니다.

열기 *Pages/_Layout.cshtml* 다음과 같이 변경 하 고 있습니다.

* "ContosoUniversity"의 "Contoso 대학."으로 변경 다음과 같은 세 가지 항목이 없습니다.

* 메뉴 항목에 대 한 추가 **학생**, **Courses**, **강사**, 및 **부서**, 및 삭제는 **연락처** 메뉴 항목입니다.

변경 내용은 강조 표시 됩니다.

[!code-html[](intro/samples/cu/Pages/_Layout.cshtml?highlight=6,29,35-38,47&range=1-50)]

*Pages/Index.cshtml*, 파일의 내용을 텍스트를 바꿀 ASP.NET MVC에 대 한이 앱에 대 한 텍스트를 다음 코드로 바꿉니다.

[!code-html[](intro/samples/cu/Pages/Index.cshtml)]

Ctrl+F5를 눌러 프로젝트를 실행합니다. 홈 페이지는 다음 자습서에서 만든 탭으로 표시 됩니다.

![Contoso 대학 홈 페이지](intro/_static/home-page.png)

## <a name="create-the-data-model"></a>데이터 모델 만들기

Contoso 대학 앱에 대 한 엔터티 클래스를 만듭니다. 다음 세 가지 엔터티로 시작 합니다.

![학생-등록 과정-데이터 모델 다이어그램](intro/_static/data-model-diagram.png)

간의 일 대 다 관계가 `Student` 및 `Enrollment` 엔터티. 간의 일 대 다 관계가 `Course` 및 `Enrollment` 엔터티. 학생 원하는 수의 과목에 등록할 수 있습니다. 과정을 학생에 등록 된 개수에 관계 없이 있을 수 있습니다.

다음 섹션에서 각각에 대 한 이러한 엔터티는 클래스를 만듭니다.

### <a name="the-student-entity"></a>학생 엔터티

![학생 엔터티 다이어그램](intro/_static/student-entity.png)

만들기는 *모델* 폴더입니다. 에 *모델* 폴더 라는 클래스 파일을 만들어 *Student.cs* 를 다음 코드로:

[!code-csharp[Main](intro/samples/cu/Models/Student.cs?name=snippet_Intro)]

`ID` 속성은이 클래스에 해당 하는 데이터베이스 (DB) 테이블의 기본 키 열입니다. EF 코어를 기본적으로 명명 된 속성을 해석 `ID` 또는 `classnameID` 기본 키로 합니다.

`Enrollments` 속성은 탐색 속성입니다. 이 엔터티와 관련 된 다른 엔터티에 대 한 탐색 속성 링크입니다. 이 경우에 `Enrollments` 속성은 `Student entity` 모두 보유는 `Enrollment` 엔터티는 관련 된 `Student`합니다. 예를 들어 경우 DB에 학생 행에 두 개의 관련 등록 행의 `Enrollments` 탐색 속성 포함 그 두 `Enrollment` 엔터티. 관련 `Enrollment` 행은 행의 해당 학생의 기본 키 값을 포함 하는 `StudentID` 열입니다. 예를 들어 ID와 학생 = 1 두 개의 행에는 `Enrollment` 테이블입니다. `Enrollment` 테이블에 두 개의 행이 `StudentID` = 1입니다. `StudentID`외래 키에 `Enrollment` 테이블에서 학생을 지정 하는 `Student` 테이블입니다.

탐색 속성 같은 목록 유형 이어야 합니다는 탐색 속성에는 여러 엔터티 보유할 수, 하는 경우 `ICollection<T>`합니다. `ICollection<T>`지정할 수 있습니다 또는 형식으로 `List<T>` 또는 `HashSet<T>`합니다. 때 `ICollection<T>` 는 사용 하는 EF 코어 만듭니다는 `HashSet<T>` 기본적으로 컬렉션입니다. 여러 엔터티를 포함 하는 탐색 속성은 다 대 다 및 1 대 다 관계에서 제공 됩니다.

### <a name="the-enrollment-entity"></a>등록 엔터티

![등록 엔터티 다이어그램](intro/_static/enrollment-entity.png)

에 *모델* 폴더를 만들 *Enrollment.cs* 를 다음 코드로:

[!code-csharp[Main](intro/samples/cu/Models/Enrollment.cs?name=snippet_Intro)]

`EnrollmentID` 속성은 기본 키입니다. 사용 하 여이 엔터티는 `classnameID` 대신 패턴 `ID` 같은 `Student` 엔터티. 일반적으로 개발자는 패턴 중 하나를 선택 하 고 데이터 모델 전체에서 사용 합니다. 자습서의 뒷부분에서 ID를 사용 하 여 응용 프로그램 이름 없이 데이터 모델에서 상속을 구현 하는 쉽게 수행할 수 있도록 표시 됩니다.

`Grade` 속성은 한 `enum`합니다. 다음 매개 변수는 `Grade` 형식 선언을 나타냅니다는 `Grade` 속성은 null을 허용 합니다. Null이 등급은 0 개 등급 다릅니다-null 의미는 등급 알려진 또는 아직 할당 되지 않았습니다.

`StudentID` 속성은 외래 키 및 해당 탐색 속성은 `Student`합니다. `Enrollment` 엔터티는 하 나와 연결 `Student` 속성 하나를 포함 하므로 엔터티 `Student` 엔터티. `Student` 에서 다른 엔터티는 `Student.Enrollments` 여러 포함 된 탐색 속성을 `Enrollment` 엔터티.

`CourseID` 속성은 외래 키 및 해당 탐색 속성은 `Course`합니다. `Enrollment` 엔터티는 하 나와 연결 `Course` 엔터티.

EF 코어 라고 하는 경우 외래 키로 속성을 해석 `<navigation property name><primary key property name>`합니다. 예를 들어`StudentID` 에 대 한는 `Student` 탐색 속성이 있으므로 `Student` 엔터티의 기본 키가 `ID`합니다. 외래 키 속성 이름을 지정할 수 `<primary key property name>`합니다. 예를 들어 `CourseID` 이후는 `Course` 엔터티의 기본 키가 `CourseID`합니다.

### <a name="the-course-entity"></a>과정 엔터티

![과정 엔터티 다이어그램](intro/_static/course-entity.png)

에 *모델* 폴더를 만들 *Course.cs* 를 다음 코드로:

[!code-csharp[Main](intro/samples/cu/Models/Course.cs?name=snippet_Intro)]

`Enrollments` 속성은 탐색 속성입니다. A `Course` 개수에 관계 없이 관련 될 수 있는 엔터티 `Enrollment` 엔터티.

`DatabaseGenerated` 생성 DB 필요 하지 않고 특성을 사용 하면 응용 프로그램에서 기본 키를 지정 합니다.

## <a name="create-the-schoolcontext-db-context"></a>SchoolContext DB 컨텍스트 만들기

지정된 된 데이터 모델에 대 한 EF 핵심 기능을 조정 하는 주 클래스는 DB 컨텍스트 클래스입니다. 파생 되는 데이터 컨텍스트 `Microsoft.EntityFrameworkCore.DbContext`합니다. 엔터티 데이터 모델에 포함 된 데이터 컨텍스트를 지정 합니다. 이 프로젝트에 클래스 이름은 `SchoolContext`합니다.

프로젝트 폴더에 라는 폴더를 만듭니다 *데이터*합니다.

에 *데이터* 폴더 만들기 *SchoolContext.cs* 를 다음 코드로:

[!code-csharp[Main](intro/samples/cu/Data/SchoolContext.cs?name=snippet_Intro)]

이 코드에서는 `DbSet` 각 엔터티 집합에 대 한 속성입니다. EF 핵심 용어:

* 엔터티 집합을 일반적으로 DB 테이블에 해당 합니다.
* 엔터티는 테이블의 행에 해당합니다.

`DbSet<Enrollment>`및 `DbSet<Course>` 생략할 수 있습니다. EF 코어 포함 암시적으로 하기 때문에 `Student` 엔터티 참조는 `Enrollment` 엔터티 및 `Enrollment` 엔터티 참조는 `Course` 엔터티. 이 자습서에는 유지 `DbSet<Enrollment>` 및 `DbSet<Course>` 에 `SchoolContext`합니다.

DB 만들어지면 EF 코어와 동일한 이름을 갖는 테이블을 만듭니다는 `DbSet` 속성 이름입니다. 컬렉션에 대 한 속성 이름에는 일반적으로 복수 (학생 아님 학생). 개발자가 테이블 이름이 복수형 여야 하는지 여부에 대 한 동의. 이 자습서에 대 한 DbContext 단 수 테이블 이름을 지정 하 여 기본 동작 재정의 됩니다. 를 단일 테이블 이름을 지정 하려면 다음 강조 표시 된 코드를 추가 합니다.

[!code-csharp[Main](intro/samples/cu/Data/SchoolContext.cs?name=snippet_TableNames&highlight=16-21)]

## <a name="register-the-context-with-dependency-injection"></a>종속성 주입 컨텍스트 등록

ASP.NET Core 포함 [종속성 주입](xref:fundamentals/dependency-injection)합니다. 서비스 (예: EF 코어 DB 컨텍스트) 종속성 주입 응용 프로그램 시작 중에 등록 됩니다. 이러한 서비스 (예: Razor 페이지)에 필요한 구성 요소를 생성자 매개 변수를 통해 이러한 서비스 제공 됩니다. Db 컨텍스트 인스턴스를 가져오는 생성자 코드는이 자습서의 뒷부분에 나오는 표시 됩니다.

등록 하려면 `SchoolContext` 서비스를 열고 *Startup.cs*, 강조 표시 된 줄을 추가 하 고는 `ConfigureServices` 메서드.

[!code-csharp[Main](intro/samples/cu/Startup.cs?name=snippet_SchoolContext&highlight=3-4)]

연결 문자열의 이름에는 메서드를 호출 하 여 컨텍스트에 전달 됩니다는 `DbContextOptionsBuilder` 개체입니다. 로컬 개발에 대 한는 [ASP.NET Core 구성 시스템](xref:fundamentals/configuration/index) 는 연결 문자열에서 *appsettings.json* 파일입니다.

추가 `using` 에 대 한 문을 `ContosoUniversity.Data` 및 `Microsoft.EntityFrameworkCore` 네임 스페이스입니다. 프로젝트를 빌드합니다.

[!code-csharp[Main](intro/samples/cu/Startup.cs?name=snippet_Usings)]

열기는 *appsettings.json* 파일을 다음 코드에 표시 된 대로 연결 문자열을 추가 합니다.

[!code-json[](./intro/samples/cu/appsettings1.json?highlight=2-4)]

위의 연결 문자열에 사용 하 여 `ConnectRetryCount=0` 방지 하기 위해 [SQLClient](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/sqlclient-for-the-entity-framework) 내어쓰기에서 합니다.

### <a name="sql-server-express-localdb"></a>SQL Server Express LocalDB

연결 문자열에는 SQL Server LocalDB DB 지정합니다. LocalDB는 SQL Server Express 데이터베이스 엔진의 경량 버전 하며 응용 프로그램 개발의 경우 프로덕션 환경에서 사용 되지 않습니다. LocalDB는 요청 시 시작하고 사용자 모드에서 실행되므로 복잡한 구성이 없습니다. 기본적으로 LocalDB 만듭니다 *.mdf* DB 파일에 `C:/Users/<user>` 디렉터리입니다.

## <a name="add-code-to-initialize-the-db-with-test-data"></a>테스트 데이터로 DB 초기화 코드를 추가

EF 코어 빈 DB를 만듭니다. 이 섹션에서는 *시드* 테스트 데이터로 채울 메서드가 작성 됩니다.

에 *데이터* 폴더 라는 새 클래스 파일을 만들 *DbInitializer.cs* 다음 코드를 추가 하 고:

[!code-csharp[Main](intro/samples/cu/Data/DbInitializer.cs?name=snippet_Intro)]

DB에 어떤 학생 되어 있는지 확인 하는 코드입니다. DB에 없는 학생 인 DB 테스트 데이터로 마련 됩니다. 배열에 테스트 데이터를 로드 하지 않고 `List<T>` 성능을 최적화 하는 컬렉션입니다.

`EnsureCreated` 메서드는 자동으로 DB DB 컨텍스트를 만듭니다. DB 있으면 `EnsureCreated` DB 수정 하지 않고 반환 합니다.

*Program.cs*, 수정 된 `Main` 다음을 수행 하는 메서드:

* 종속성 주입 컨테이너에서 DB 컨텍스트 인스턴스를 가져옵니다.
* 컨텍스트를 전달 하는 초기값 메서드를 호출 합니다.
* 시드 메서드가 완료 되는 컨텍스트를 삭제 합니다.

다음 코드에서는 업데이트 된 *Program.cs* 파일입니다.

[!code-csharp[Main](intro/samples/cu/ProgramOriginal.cs?name=snippet)]

처음으로 앱이 실행 되는 DB 작성 되 고 시드 테스트 데이터를 사용 합니다. 데이터 모델 업데이트 될 때를 나타냅니다.
* DB를 삭제 합니다.
* Seed 메서드를 업데이트 합니다.
* 응용 프로그램을 실행 하 고 새 시드 DB 만들어집니다. 

이후의 자습서에서는 데이터 모델이 변경, 삭제 및 DB를 다시 작성 하지 않고 DB 업데이트 됩니다.

<a name="pmc"></a>
## <a name="add-scaffold-tooling"></a>스 캐 폴드 도구 추가

이 섹션에서는 패키지 관리자 콘솔 (PMC)는 Visual Studio 웹 코드 생성 패키지를 추가 하는 데 사용 됩니다. 스캐폴딩 엔진을 실행하려면 이 패키지가 필요합니다.

**도구** 메뉴에서 **NuGet 패키지 관리자** > **패키지 관리자 콘솔**을 선택합니다.

패키지 관리자 콘솔 (PMC)에서 다음 명령을 입력 합니다.

```powershell
Install-Package Microsoft.VisualStudio.Web.CodeGeneration.Design
Install-Package Microsoft.VisualStudio.Web.CodeGeneration.Utils
```

위 명령은 *.csproj 파일을 NuGet 패키지를 추가합니다.

[!code-csharp[Main](intro/samples/cu/ContosoUniversity1_csproj.txt?highlight=7-8)]

<a name="scaffold"></a>
## <a name="scaffold-the-model"></a>스 캐 폴드 모델

* 프로젝트 디렉터리(*Program.cs*, *Startup.cs* 및 *.csproj* 파일이 포함된 디렉터리)에서 명령 창을 엽니다.
* 다음 명령을 실행 합니다.


 ```console
dotnet restore
dotnet aspnet-codegenerator razorpage -m Student -dc SchoolContext -udl -outDir Pages\Students --referenceScriptLibraries
 ```
 
경우 다음과 같은 오류가 생성 됩니다.

```text
Unhandled Exception: System.IO.FileNotFoundException: 
Could not load file or assembly 
'Microsoft.VisualStudio.Web.CodeGeneration.Utils, 
Version=2.0.0.0, Culture=neutral, PublicKeyToken=adb9793829ddae60'.
The system cannot find the file specified.
```

명령을 다시 실행 하 고 페이지 아래쪽에 의견을 남겨 합니다.

오류가 표시될 경우:
  ```
No executable found matching command "dotnet-aspnet-codegenerator"
  ```

프로젝트 디렉터리(*Program.cs*, *Startup.cs* 및 *.csproj* 파일이 포함된 디렉터리)에서 명령 창을 엽니다.


프로젝트를 빌드합니다. 빌드에서는 다음과 같은 오류를 생성합니다.

 `1>Pages\Students\Index.cshtml.cs(26,38,26,45): error CS1061: 'SchoolContext' does not contain a definition for 'Student'`

 전역으로 변경 `_context.Student` 를 `_context.Students` (즉, "s"에 추가 `Student`). 7 번 발견 되 고 업데이트 됩니다. 수정 하기 위해 노력 [이 버그](https://github.com/aspnet/Scaffolding/issues/633) 다음 릴리스에서 합니다.

[!INCLUDE[model4tbl](../../includes/RP/model4tbl.md)]

 <a name="test"></a>
### <a name="test-the-app"></a>앱 테스트

응용 프로그램을 실행 하 고 선택 된 **학생** 링크 합니다. 브라우저 너비에 따라는 **학생** 링크 페이지의 맨 위에 나타납니다. 경우는 **학생** 링크가 표시 되지 않는, 오른쪽 위 모서리에서 탐색 아이콘을 클릭 합니다.

![좁은 Contoso 대학 홈 페이지](intro/_static/home-page-narrow.png)

테스트는 **만들기**, **편집**, 및 **세부 정보** 링크 합니다.

## <a name="view-the-db"></a>DB 보기

앱이 시작 되 면 `DbInitializer.Initialize` 호출 `EnsureCreated`합니다. `EnsureCreated`감지 하 여 DB 존재 하 고, 필요한 경우 하나 만듭니다. 에 있는 경우 없습니다 학생 DB는 `Initialize` 메서드 학생을 추가 합니다.

열기 **SQL Server 개체 탐색기** (SSOX)에서 고 **보기** Visual Studio에서 메뉴.
SSOX, 클릭 **(localdb) \MSSQLLocalDB > 데이터베이스 > ContosoUniversity1**합니다.

확장 된 **테이블** 노드.

마우스 오른쪽 단추로 클릭는 **학생** 테이블 마우스 클릭 **데이터 보기** 만든 열 및 테이블에 삽입 된 행을 볼 수 있습니다.

*.mdf* 및 *.ldf* DB 파일에 있는 *C:\Users\\ <yourusername>*  폴더입니다.

`EnsureCreated`다음 작업 흐름을 허용 하는 응용 프로그램 시작에서 호출 됩니다.

* DB를 삭제 합니다.
* DB 스키마를 변경 (예: 추가 `EmailAddress` 필드).
* 앱을 실행합니다.

`EnsureCreated`DB가 만듭니다는`EmailAddress` 열입니다.

## <a name="conventions"></a>규칙

규칙 또는 EF 코어에 수행 하는 가정을 사용 되기 때문에 전체 DB를 만들려면 EF 코어를 위해 작성 된 코드의 양을 최소화 됩니다.

* 이름을 `DbSet` 속성 테이블 이름으로 사용 됩니다. 엔터티에 의해 참조 되지 않는 한 `DbSet` 속성, 엔터티 클래스 이름이 테이블 이름으로 사용 됩니다.

* 엔터티 속성 이름은 열 이름에 사용 됩니다.

* ID 또는 classnameID 명명 된 엔터티 속성은 기본 키 속성으로 인식 됩니다.

* 라고 하는 경우 외래 키 속성으로는 속성을 해석  *<navigation property name> <primary key property name>*  (예를 들어 `StudentID` 에 대 한는 `Student` 이후 탐색 속성은 `Student` 엔터티의 기본 키가 `ID`). 외래 키 속성 이름을 지정할 수  *<primary key property name>*  (예를 들어 `EnrollmentID` 이후는 `Enrollment` 엔터티의 기본 키가 `EnrollmentID`).

기본 동작을 재정의할 수 있습니다. 예를 들어 테이블 이름은 지정할 수 있습니다 명시적으로,이 자습서의 앞부분에 나와 있는 것 처럼 합니다. 열 이름은 명시적으로 설정할 수 있습니다. 기본 키와 외래 키 명시적으로 설정할 수 있습니다.

## <a name="asynchronous-code"></a>비동기 코드

비동기 프로그래밍은 ASP.NET 코어 및 EF 코어에 대 한 기본 모드입니다.

웹 서버를 사용할 수 있는 스레드 수가 제한에 및 로드 양이 많으면 상황에서 모든 사용 가능한 스레드 수 사용. 이 경우 서버를 스레드가 해제 될 때까지 새 요청을 처리할 수 없습니다. I/O가 완료를 대기 하 고 있으므로 작업을 실제로 수행 되지 않습니다은 동안 많은 스레드가 동기 코드와 함께 하느라 정체 될 수 있습니다. 비동기 코드로 i/o가 완료를 대기 하는 프로세스 스레드에서 다른 요청을 처리에 사용할 서버에 대해 해제 됩니다. 따라서 비동기 코드 서버 리소스를 보다 효율적으로 사용할 수 있으며 특정가 지연 없이 더 많은 트래픽을 처리 하도록 서버를 설정 합니다.

비동기 코드는 런타임 시 약간의 오버 헤드를 소개 합니다. 트래픽이 적은 경우에 대 한 성능 저하가 트래픽이 많은 상황에 대 한 동안 무시할를 잠재적 성능 향상 됩니다.

다음 코드에서는 `async` 키워드를 `Task<T>` 값을 반환 `await` 키워드 및 `ToListAsync` 메서드를 비동기적으로 실행 하는 코드를 확인 합니다.

[!code-csharp[Main](intro/samples/cu/Pages/Students/Index.cshtml.cs?name=snippet_ScaffoldedIndex)]

* `async` 키워드는 컴파일러에 지시 합니다.

  * 메서드 본문의 부분에 대 한 콜백을 생성 합니다.
  * 자동으로 만듭니다는 [작업](https://docs.microsoft.com/dotnet/api/system.threading.tasks.task?view=netframework-4.7) 반환 되는 개체입니다. 자세한 내용은 참조 [작업 반환 형식](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/async/async-return-types#BKMK_TaskReturnType)합니다.

* 암시적 반환 형식 `Task` 은 진행 중인 작업을 나타냅니다.

* `await` 키워드는 컴파일러에 메서드가 두 부분으로 분할 합니다. 첫 번째 부분은 비동기적으로 시작 된 작업을 종료 합니다. 두 번째 부분은 작업이 완료 될 때 호출 되는 콜백 메서드에 배치 됩니다.

* `ToListAsync`비동기 버전의 `ToList` 확장 메서드.

EF 코어를 사용 하는 비동기 코드를 작성 하는 경우 고려해 야 할 몇 가지 사항은 다음과 같습니다.

* 쿼리 또는 여 DB에 보내야 하는 명령을 발생 하는 명령문만 비동기적으로 실행 됩니다. 포함 된 `ToListAsync`, `SingleOrDefaultAsync`, `FirstOrDefaultAsync`, 및 `SaveChangesAsync`합니다. 방금 변경 하는 문을 포함 하지 않습니다는 `IQueryable`와 같은 `var students = context.Students.Where(s => s.LastName == "Davolio")`합니다.

* EF 코어 컨텍스트는 스레드 안전 하지 않습니다: 동시에 여러 작업을 수행 하지 마세요. 

* 비동기 코드의 성능 이점을 활용 하려면 있는지 라이브러리 패키지 (예: 페이징) 비동기 메서드를 사용 DB에 쿼리를 전송 하는 EF 코어 메서드를 호출 하는 경우를 확인 합니다.

.NET의 비동기 프로그래밍에 대 한 자세한 내용은 참조 [비동기 개요](https://docs.microsoft.com/dotnet/articles/standard/async)합니다.

다음 자습서에서는 기본 CRUD (만들기, 읽기, 업데이트, 삭제) 작업을 검사 합니다.

>[!div class="step-by-step"]
[다음](xref:data/ef-rp/crud)
