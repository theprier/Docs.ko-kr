---
title: ASP.NET Core에서 Razor 페이지 앱에 모델 추가
author: rick-anderson
description: Entity Framework Core(EF Core)를 사용하여 데이터베이스에서 영화를 관리하기 위한 클래스를 추가하는 방법을 알아봅니다.
ms.author: riande
ms.date: 05/30/2018
uid: tutorials/razor-pages/model
ms.openlocfilehash: ed8faf8b3049adc7bcc7953d63ad805b0a836bd9
ms.sourcegitcommit: 356c8d394aaf384c834e9c90cabab43bfe36e063
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2018
ms.locfileid: "36961177"
---
# <a name="add-a-model-to-a-razor-pages-app-in-aspnet-core"></a>ASP.NET Core에서 Razor 페이지 앱에 모델 추가

::: moniker range=">= aspnetcore-2.1"

[!INCLUDE [model1](~/includes/RP/model1.md)]

## <a name="add-a-data-model"></a>데이터 모델 추가

솔루션 탐색기에서 **RazorPagesMovie** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** > **새 폴더**를 선택합니다. 폴더 이름을 *Models*로 지정합니다.

*Models* 폴더를 마우스 오른쪽 단추로 클릭합니다. **추가** > **클래스**를 선택합니다. 클래스 이름을 **Movie**로 지정하고 다음 속성을 추가합니다.

`Movie` 클래스의 콘텐츠를 다음 코드로 바꿉니다.

[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie21/Models/Movie1.cs?name=snippet)]

## <a name="scaffold-the-movie-model"></a>동영상 모델 스캐폴드

이 섹션에서는 동영상 모델을 스캐폴 합니다. 즉, 스캐폴드 도구는 동영상 모델에서 CRUD(만들기, 읽기, 업데이트 및 삭제) 작업을 위한 페이지를 생성합니다.

*Pages/Movies* 폴더를 만듭니다.

* **솔루션 탐색기**에서 *Pages* 폴더 > **추가** > **새 폴더**를 마우스 오른쪽 단추로 클릭합니다.
* 폴더 이름을 *Movies*로 지정합니다.

**솔루션 탐색기**에서 *Pages/Movies* 폴더 > **추가** > **새 스캐폴드된 항목**을 마우스 오른쪽 단추로 클릭합니다.

![이전 지침의 이미지입니다.](model/_static/sca.png)

**스캐폴드 추가** 대화 상자에서 **Entity Framework(CRUD)를 사용한 Razor Pages** > **추가**를 선택합니다.

![이전 지침의 이미지입니다.](model/_static/add_scaffold.png)

**Entity Framework(CRUD)를 사용하여 Razor Pages 추가** 대화 상자를 완료합니다.

* **모델 클래스** 드롭다운에서 **동영상(RazorPagesMovie.Models)** 을 선택합니다.
* **데이터 컨텍스트 클래스** 행에서 **+** 기호를 선택하고 생성된 이름인 **RazorPagesMovie.Models.RazorPagesMovieContext**를 수용합니다.
* **데이터 컨텍스트 클래스** 드롭다운에서 **RazorPagesMovie.Models.RazorPagesMovieContext**를 선택합니다.
* **추가**를 선택합니다.

![이전 지침의 이미지입니다.](model/_static/arp.png)

스캐폴드 프로세스는 다음 파일을 생성하고 변경했습니다.

### <a name="files-created"></a>생성된 파일

* *Pages/Movies* 만들기, 삭제, 세부 정보, 편집, 인덱스입니다. 이러한 페이지는 다음 자습서에서 자세히 설명합니다.
* *Data/RazorPagesMovieContext.cs*

### <a name="files-updates"></a>파일 업데이트

* *Startup.cs*: 이 파일의 변경 내용은 다음 섹션에서 자세히 설명합니다.
* *appsettings.json*: 로컬 데이터베이스에 연결하는 데 사용된 연결 문자열이 추가됩니다.

## <a name="examine-the-context-registered-with-dependency-injection"></a>종속성 주입을 사용하여 등록된 컨텍스트 검사

ASP.NET Core는 [종속성 주입](xref:fundamentals/dependency-injection)을 사용하여 빌드됩니다. 서비스(예: EF Core DB 컨텍스트)는 응용 프로그램 시작 중에 종속성 주입에 등록됩니다. 이러한 서비스(예: Razor 페이지)가 필요한 구성 요소에는 생성자 매개 변수를 통해 이러한 서비스가 제공됩니다. DB 컨텍스트 인스턴스를 가져오는 생성자 코드는 자습서 뒷부분에 나옵니다.

스캐폴딩 도구는 자동으로 DB 컨텍스트를 생성하고 종속성 주입 컨테이너에 등록했습니다.

`Startup.ConfigureServices` 메서드를 검사합니다. 강조 표시된 줄은 스캐폴더에서 추가되었습니다.

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie21/Startup.cs?name=snippet_ConfigureServices&highlight=12-13)]

특정 데이터 모델에 맞게 EF Core 기능을 조정하는 주 클래스는 DB 컨텍스트 클래스입니다. 데이터 컨텍스트는 [Microsoft.EntityFrameworkCore.DbContext](/dotnet/api/microsoft.entityframeworkcore.dbcontext)에서 파생됩니다. 데이터 컨텍스트는 데이터 모델에 포함되는 엔터티를 지정합니다. 이 프로젝트에서 클래스 이름은 `RazorPagesMovieContext`로 지정됩니다.

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie21/Data/RazorPagesMovieContext.cs)]

이전 코드에서는 엔터티 집합에 대해 [DbSet\<Movie>](/dotnet/api/microsoft.entityframeworkcore.dbset-1) 속성을 만듭니다. Entity Framework 용어에서 엔터티 집합은 일반적으로 데이터베이스 테이블에 해당합니다. 엔터티는 테이블의 행에 해당합니다.

[DbContextOptions](/dotnet/api/microsoft.entityframeworkcore.dbcontextoptions) 개체에서 메서드를 호출하여 연결 문자열의 이름을 컨텍스트에 전달합니다. 로컬 개발의 경우 [ASP.NET Core 구성 시스템](xref:fundamentals/configuration/index)은 *appsettings.json* 파일에서 연결 문자열을 읽습니다.

<a name="pmc"></a>
## <a name="perform-initial-migration"></a>초기 마이그레이션 수행

이 섹션에서는 PMC(패키지 관리자 콘솔)를 사용하여 다음을 수행합니다.

* 초기 마이그레이션을 추가합니다.
* 초기 마이그레이션을 사용하여 데이터베이스를 업데이트합니다.

**도구** 메뉴에서 **NuGet 패키지 관리자** > **패키지 관리자 콘솔**을 선택합니다.

  ![PMC 메뉴](../first-mvc-app/adding-model/_static/pmc.png)

PMC에서 다음 명령을 입력합니다.

```PMC
Add-Migration Initial
Update-Database
```

또는 다음 .NET Core CLI 명령을 사용할 수 있습니다.

```console
dotnet ef migrations add Initial
dotnet ef database update
```

다음과 같은 경고 메시지를 무시합니다. 해당 문제를 다음 자습서에서 해결합니다.

`Microsoft.EntityFrameworkCore.Model.Validation[30000]`

      *No type was specified for the decimal column 'Price' on entity type 'Movie'. This will cause values to be silently truncated if they do not fit in the default precision and scale. Explicitly specify the SQL server column type that can accommodate all the values using 'ForHasColumnType()'.*

`Add-Migration` 명령은 초기 데이터베이스 스키마를 만드는 코드를 생성합니다. 스키마는 `RazorPagesMovieContext`에 지정된 모델을 기반으로 합니다(*Data/RazorPagesMovieContext.cs* 파일). `Initial` 인수는 마이그레이션 이름을 지정하는 데 사용됩니다. 모든 이름을 사용할 수 있지만 일반적으로 마이그레이션을 설명하는 이름을 선택합니다. 자세한 내용은 [마이그레이션 소개](xref:data/ef-mvc/migrations#introduction-to-migrations)를 참조하세요.

`Update-Database` 명령은 데이터베이스를 만드는 *Migrations/{time-stamp}_InitialCreate.cs* 파일에서 `Up` 메서드를 실행합니다.

오류가 표시될 경우:

SqlException: 로그인에서 요청한 "RazorPagesMovieContext-GUID" 데이터베이스를 열 수 없습니다. 로그인에 실패했습니다.
'User-name' 사용자에 대한 로그인에 실패했습니다.

[마이그레이션 단계](#pmc)를 누락했습니다.
::: moniker-end

::: moniker range="= aspnetcore-2.0"

[!INCLUDE [model1](~/includes/RP/model1.md)]

## <a name="add-a-data-model"></a>데이터 모델 추가

솔루션 탐색기에서 **RazorPagesMovie** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** > **새 폴더**를 선택합니다. 폴더 이름을 *Models*로 지정합니다.

*Models* 폴더를 마우스 오른쪽 단추로 클릭합니다. **추가** > **클래스**를 선택합니다. 클래스 이름을 **Movie**로 지정하고 다음 속성을 추가합니다.

[!INCLUDE [model 2](~/includes/RP/model2.md)]

<a name="cs"></a>
### <a name="add-a-database-connection-string"></a>데이터베이스 연결 문자열 추가

*appsettings.json* 파일에 연결 문자열을 추가합니다.

[!code-json[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/appsettings.json?highlight=8-10)]

<a name="reg"></a>
###  <a name="register-the-database-context"></a>데이터베이스 컨텍스트 등록

[스타트업 클래스(*Startup.cs*)의 ConfigureServices 메서드](xref:fundamentals/startup#the-startup-class)에서 [종속성 주입](xref:fundamentals/dependency-injection) 컨테이너에 데이터베이스 컨텍스트를 등록합니다.

[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Startup.cs?name=snippet_ConfigureServices&highlight=3-5,7-9)]

프로젝트를 빌드하여 오류가 없는지 확인합니다.

<a name="pmc"></a>
## <a name="add-scaffold-tooling-and-perform-initial-migration"></a>스캐폴드 도구 추가 및 초기 마이그레이션 수행

이 섹션에서는 PMC(패키지 관리자 콘솔)를 사용하여 다음을 수행합니다.

* Visual Studio 웹 코드 생성 패키지를 추가합니다. 스캐폴딩 엔진을 실행하려면 이 패키지가 필요합니다.
* 초기 마이그레이션을 추가합니다.
* 초기 마이그레이션을 사용하여 데이터베이스를 업데이트합니다.

**도구** 메뉴에서 **NuGet 패키지 관리자** > **패키지 관리자 콘솔**을 선택합니다.

  ![PMC 메뉴](../first-mvc-app/adding-model/_static/pmc.png)

PMC에서 다음 명령을 입력합니다.

```powershell
Install-Package Microsoft.VisualStudio.Web.CodeGeneration.Design -Version 2.0.3
Add-Migration Initial
Update-Database
```

또는 다음 .NET Core CLI 명령을 사용할 수 있습니다.

```console
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet ef migrations add Initial
dotnet ef database update
```

다음과 같은 메시지를 무시합니다.

    `Microsoft.EntityFrameworkCore.Model.Validation[30000]`

      *No type was specified for the decimal column 'Price' on entity type 'Movie'. This will cause values to be silently truncated if they do not fit in the default precision and scale. Explicitly specify the SQL server column type that can accommodate all the values using 'ForHasColumnType()'*

다음 자습서에서 해당 문제를 해결합니다.

`Install-Package` 명령은 스캐폴딩 엔진을 실행하는 데 필요한 도구를 설치합니다.

`Add-Migration` 명령은 초기 데이터베이스 스키마를 만드는 코드를 생성합니다. 스키마는 `DbContext`에 지정된 모델을 기반으로 합니다(*Models/MovieContext.cs* 파일에서). `Initial` 인수는 마이그레이션 이름을 지정하는 데 사용됩니다. 모든 이름을 사용할 수 있지만 일반적으로 마이그레이션을 설명하는 이름을 선택합니다. 자세한 내용은 [마이그레이션 소개](xref:data/ef-mvc/migrations#introduction-to-migrations)를 참조하세요.

`Update-Database` 명령은 데이터베이스를 만드는 *Migrations/{time-stamp}_InitialCreate.cs* 파일에서 `Up` 메서드를 실행합니다.

[!INCLUDE [model 4windows](~/includes/RP/model4Win.md)]

[!INCLUDE [model 4](~/includes/RP/model4tbl.md)]

::: moniker-end

<a name="test"></a>

### <a name="test-the-app"></a>앱 테스트

* 앱을 실행하고 브라우저에서 `/Movies`를 URL에 추가합니다(`http://localhost:port/movies`).
* **만들기** 링크를 테스트합니다.

  ![페이지 만들기](../../tutorials/razor-pages/model/_static/conan.png)

<a name="scaffold"></a>

* **편집**, **세부 정보** 및 **삭제** 링크를 테스트합니다.

SQL 예외가 발생하는 경우 마이그레이션을 실행했는지와 데이터베이스를 업데이트했는지 확인하세요.

다음 자습서에서는 스캐폴딩을 통해 만들어진 파일을 설명합니다.

> [!div class="step-by-step"]
> [이전: 시작](xref:tutorials/razor-pages/razor-pages-start)
> [다음: 스캐폴드된 Razor 페이지](xref:tutorials/razor-pages/page)
