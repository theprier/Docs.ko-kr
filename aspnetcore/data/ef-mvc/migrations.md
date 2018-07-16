---
title: ASP.NET Core MVC 및 EF Core - 마이그레이션 - 4/10
author: rick-anderson
description: 이 자습서에서는 ASP.NET Core MVC 응용 프로그램에서 데이터 모델 변경 관리를 위해 EF Core 마이그레이션 기능을 사용하는 것을 시작합니다.
ms.author: tdykstra
ms.date: 03/15/2018
uid: data/ef-mvc/migrations
ms.openlocfilehash: f710b33ac1a6017b0e3d7e8c3e528675a41424bb
ms.sourcegitcommit: b8a2f14bf8dd346d7592977642b610bbcb0b0757
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38194172"
---
# <a name="aspnet-core-mvc-with-ef-core---migrations---4-of-10"></a>ASP.NET Core MVC 및 EF Core - 마이그레이션 - 4/10

[!INCLUDE [RP better than MVC](~/includes/RP-EF/rp-over-mvc-21.md)]

::: moniker range="= aspnetcore-2.0"

작성자: [Tom Dykstra](https://github.com/tdykstra) 및 [Rick Anderson](https://twitter.com/RickAndMSFT)

Contoso University 웹 응용 프로그램 예제는 Entity Framework Core 및 Visual Studio를 사용하여 ASP.NET Core MVC 웹 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대한 정보는 [시리즈의 첫 번째 자습서](intro.md)를 참조하세요.

이 자습서에서는 데이터 모델 변경을 관리하기 위해 EF Core 마이그레이션 기능을 사용하기 시작합니다. 이후의 자습서에서는 데이터 모델을 변경하면서 더 많은 마이그레이션을 추가하게 됩니다.

## <a name="introduction-to-migrations"></a>마이그레이션 소개

새 응용 프로그램을 개발하는 경우 데이터 모델은 자주 변경되며 모델이 변경될 때마다 데이터베이스와 동기화를 가져옵니다. 데이터베이스가 존재하지 않는 경우 Entity Framework를 구성하여 만들면서 이러한 자습서를 시작하였습니다. 그런 다음, 엔터티 클래스를 추가, 제거 또는 변경하거나 DbContext 클래스를 변경하면서 데이터 모델을 변경할 때마다 데이터베이스를 삭제할 수 있습니다. 또한 EF는 모델에 일치하는 새로운 항목을 만들고 테스트 데이터로 시드합니다.

데이터베이스를 데이터 모델과 동기화된 상태로 유지하는 이 메서드는 응용 프로그램을 프로덕션 환경에 배포할 때까지 잘 작동합니다. 응용 프로그램이 프로덕션 환경에서 실행 중인 경우, 일반적으로 새 열을 추가하는 것처럼 사용자가 변경할 때마다 유지하려는 데이터 및 손실하지 않으려는 데이터를 저장합니다. EF Core 마이그레이션 기능은 EF가 새 데이터베이스를 만드는 대신 데이터베이스 스키마를 업데이트하도록 설정하여 이 문제를 해결합니다.

## <a name="entity-framework-core-nuget-packages-for-migrations"></a>마이그레이션을 위한 Entity Framework Core NuGet 패키지

마이그레이션을 수행하기 위해 **PMC(패키지 관리자 콘솔)** 또는 CLI(명령줄 인터페이스)를 사용할 수 있습니다.  이러한 자습서에는 CLI 명령을 사용하는 방법을 보여 줍니다. PMC에 대한 정보는 [이 자습서의 마지막](#pmc)에 나와 있습니다.

CLI(명령줄 인터페이스)용 EF 도구는 [Microsoft.EntityFrameworkCore.Tools.DotNet](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools.DotNet)에서 제공됩니다. 이 패키지를 설치하려면 표시된 것처럼 *.csproj* 파일의 `DotNetCliToolReference` 컬렉션에 패키지를 추가합니다. **참고:** *.csproj* 파일을 편집하여 이 패키지를 설치해야 합니다. `install-package` 명령이나 패키지 관리자 GUI를 사용할 수 없습니다. **솔루션 탐색기**에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭하고 **ContosoUniversity.csproj 편집**을 선택하여 *.csproj* 파일을 편집합니다.

[!code-xml[](intro/samples/cu/ContosoUniversity.csproj?range=12-15&highlight=2)]
  
(이 예제의 버전 번호는 이 자습서가 작성된 당시의 버전 번호입니다.)

## <a name="change-the-connection-string"></a>연결 문자열 변경

*appsettings.json* 파일에서 연결 문자열에 있는 데이터베이스의 이름을 ContosoUniversity2 또는 사용 중인 컴퓨터에서 사용한 적 없는 다른 이름으로 변경합니다.

[!code-json[](intro/samples/cu/appsettings2.json?range=1-4)]

이러한 변경은 첫 번째 마이그레이션이 새 데이터베이스를 만드는 프로젝트를 설정합니다. 이는 마이그레이션을 시작하는 데 필수는 아니지만 나중에 이에 대한 이점을 확인할 수 있습니다.

> [!NOTE]
> 데이터베이스 이름을 변경하는 대신, 데이터베이스를 삭제할 수 있습니다. **SSOX(SQL Server 개체 탐색기)** 또는 `database drop` CLI 명령을 사용합니다.
> ```console
> dotnet ef database drop
> ```
> 다음 섹션에서는 CLI 명령을 실행하는 방법을 설명합니다.

## <a name="create-an-initial-migration"></a>초기 마이그레이션 만들기

변경 내용을 저장하고 프로젝트를 빌드합니다. 그런 다음, 명령 창을 열고 프로젝트 폴더로 이동합니다. 작업을 수행하는 빠른 방법은 다음과 같습니다.

* **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 바로 가기 메뉴에서 **파일 탐색기에서 열기**를 선택합니다.

  ![파일 탐색기에서 열기 메뉴 항목](migrations/_static/open-in-file-explorer.png)

* 주소 표시줄에 “cmd”를 입력하고 Enter 키를 누릅니다.

  ![열기 명령 창](migrations/_static/open-command-window.png)

명령 창에서 다음 명령을 입력합니다.

```console
dotnet ef migrations add InitialCreate
```

명령 창에 다음과 같은 출력이 표시됩니다.

```console
info: Microsoft.AspNetCore.DataProtection.KeyManagement.XmlKeyManager[0]
      User profile is available. Using 'C:\Users\username\AppData\Local\ASP.NET\DataProtection-Keys' as key repository and Windows DPAPI to encrypt keys at rest.
info: Microsoft.EntityFrameworkCore.Infrastructure[100403]
      Entity Framework Core 2.0.0-rtm-26452 initialized 'SchoolContext' using provider 'Microsoft.EntityFrameworkCore.SqlServer' with options: None
Done. To undo this action, use 'ef migrations remove'
```

> [!NOTE]
> *No executable found matching command "dotnet-ef"(명령 “dotnet-ef”에 일치하는 실행 파일을 찾을 수 없음)* 오류 메시지가 표시되면 [이 블로그 게시물](http://thedatafarm.com/data-access/no-executable-found-matching-command-dotnet-ef/)을 참조하여 문제 해결에 도움을 받으세요.

“*cannot access the file ... ContosoUniversity.dll because it is being used by another process.*(다른 프로세스에서 사용 중이므로 ContosoUniversity.dll 파일에 액세스할 수 없음.)” 오류 메시지가 표시되면 Windows 시스템 트레이에서 IIS Express 아이콘을 찾아 마우스 오른쪽 단추로 클릭한 다음, **ContosoUniversity > 사이트 중단**을 클릭합니다.

## <a name="examine-the-up-and-down-methods"></a>Up 및 Down 메서드 검사

`migrations add` 명령을 실행하면 EF는 데이터베이스를 처음부터 만드는 코드를 생성했습니다. 이 코드는 *\<timestamp>_InitialCreate.cs*라는 파일의 *Migrations* 폴더에 있습니다. 다음 예제와 같이 `InitialCreate` 클래스의 `Up` 메서드는 데이터 모델 엔터티 집합에 해당하는 데이터베이스 테이블을 만들고 `Down` 메서드는 이를 삭제합니다.

[!code-csharp[](intro/samples/cu/Migrations/20170215220724_InitialCreate.cs?range=92-118)]

마이그레이션에서는 마이그레이션을 위한 데이터 모델 변경을 구현하기 위해 `Up` 메서드를 호출합니다. 업데이트를 롤백하는 명령을 입력하면 마이그레이션에서 `Down` 메서드를 호출합니다.

이 코드는 `migrations add InitialCreate` 명령을 입력했을 때 만들어진 초기 마이그레이션을 위한 것입니다. 파일 이름에는 마이그레이션 이름 매개 변수(이 예제에서 “InitialCreate”)가 사용되며 사용자가 원하는 이름일 수 있습니다. 마이그레이션에서 수행 중인 작업을 요약한 단어 또는 구를 선택하는 것이 가장 좋습니다. 예를 들어 이후 마이그레이션의 이름을 “AddDepartmentTable”로 지정할 수도 있습니다.

데이터베이스가 이미 존재할 때 초기 마이그레이션을 만든 경우 데이터베이스 만들기 코드가 생성되지만 데이터베이스는 이미 데이터 모델과 일치하기 때문에 실행할 필요는 없습니다. 데이터베이스가 아직 없는 다른 환경에 앱을 배포하는 경우 이 코드를 실행하여 데이터베이스를 만들기 때문에 먼저 테스트하는 것이 좋습니다. 바로 이것이 앞서 연결 문자열의 데이터베이스 이름을 변경한 이유입니다. 따라서 해당 마이그레이션은 처음부터 새로운 데이터베이스를 만들 수 있습니다.

## <a name="the-data-model-snapshot"></a>데이터 모델 스냅숏

마이그레이션은 현재 데이터베이스 스키마의 *스냅숏*을 *Migrations/SchoolContextModelSnapshot.cs*에 만듭니다. 마이그레이션을 추가하면 EF가 데이터 모델을 스냅숏 파일과 비교하여 변경 내용을 확인합니다.

마이그레이션을 삭제할 때는 [dotnet ef migrations remove](https://docs.microsoft.com/ef/core/miscellaneous/cli/dotnet#dotnet-ef-migrations-remove) 명령을 사용합니다. `dotnet ef migrations remove`는 마이그레이션을 삭제하고 스냅숏이 올바르게 다시 설정되도록 합니다.

스냅숏 파일을 사용하는 방법에 대한 자세한 내용은 [팀 환경의 EF Core 마이그레이션](/ef/core/managing-schemas/migrations/teams)을 참조하세요.

## <a name="apply-the-migration-to-the-database"></a>새 마이그레이션을 데이터베이스에 적용

명령 창에서 다음 명령을 입력하여 데이터베이스 및 테이블을 만듭니다.

```console
dotnet ef database update
```

명령의 출력은 데이터베이스를 설정하는 SQL 명령에 대한 로그가 표시되는 것 외에 `migrations add` 명령과 유사합니다. 대부분의 로그는 다음 예제 출력에서 생략됩니다. 로그 메시지의 세부 수준을 줄이는 것을 선호하는 경우 *appsettings.Development.json* 파일에서 로그 수준을 변경할 수 있습니다. 자세한 내용은 [로깅 소개](xref:fundamentals/logging/index)를 참조하세요.

```text
info: Microsoft.AspNetCore.DataProtection.KeyManagement.XmlKeyManager[0]
      User profile is available. Using 'C:\Users\username\AppData\Local\ASP.NET\DataProtection-Keys' as key repository and Windows DPAPI to encrypt keys at rest.
info: Microsoft.EntityFrameworkCore.Infrastructure[100403]
      Entity Framework Core 2.0.0-rtm-26452 initialized 'SchoolContext' using provider 'Microsoft.EntityFrameworkCore.SqlServer' with options: None
info: Microsoft.EntityFrameworkCore.Database.Command[200101]
      Executed DbCommand (467ms) [Parameters=[], CommandType='Text', CommandTimeout='60']
      CREATE DATABASE [ContosoUniversity2];
info: Microsoft.EntityFrameworkCore.Database.Command[200101]
      Executed DbCommand (20ms) [Parameters=[], CommandType='Text', CommandTimeout='30']
      CREATE TABLE [__EFMigrationsHistory] (
          [MigrationId] nvarchar(150) NOT NULL,
          [ProductVersion] nvarchar(32) NOT NULL,
          CONSTRAINT [PK___EFMigrationsHistory] PRIMARY KEY ([MigrationId])
      );

<logs omitted for brevity>

info: Microsoft.EntityFrameworkCore.Database.Command[200101]
      Executed DbCommand (3ms) [Parameters=[], CommandType='Text', CommandTimeout='30']
      INSERT INTO [__EFMigrationsHistory] ([MigrationId], [ProductVersion])
      VALUES (N'20170816151242_InitialCreate', N'2.0.0-rtm-26452');
Done.
```

**SQL Server 개체 탐색기**를 사용하여 첫 번째 자습서에서와 같이 데이터베이스를 검사합니다.  데이터베이스에 어떤 마이그레이션이 적용되는지를 추적하는 __EFMigrationsHistory 테이블이 추가된 것을 확인할 수 있습니다. 해당 테이블의 데이터를 보면 첫 번째 마이그레이션에 대해 한 행이 표시됩니다. (앞의 CLI 출력 예제의 마지막 로그는 이 행을 만드는 INSERT 문을 보여 줍니다.)

응용 프로그램을 실행하여 모든 항목이 여전히 이전과 동일하게 작동하는지 확인합니다.

![학생 인덱스 페이지](migrations/_static/students-index.png)

<a id="pmc"></a>
## <a name="command-line-interface-cli-vs-package-manager-console-pmc"></a>CLI(명령줄 인터페이스) 대 PMC(패키지 관리자 콘솔)

마이그레이션 관리를 위한 EF 도구는 Visual Studio **PMC(패키지 관리자 콘솔)** 에서 PowerShell cmdlet 또는 .NET Core CLI 명령에서 사용할 수 있습니다. 이 자습서에는 CLI를 사용하는 방법이 나와 있지만 원하는 경우에 PMC를 사용할 수 있습니다.

PMC 명령을 위한 EF 명령은 [Microsoft.EntityFrameworkCore.Tools](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools) 패키지에 있습니다. 이 패키지는 이미 [Microsoft.AspNetCore.All](xref:fundamentals/metapackage) 메타패키지에 포함되어 있으므로 설치할 필요가 없습니다.

**중요:** *.csproj* 파일을 편집하여 CLI에 대해 설치한 것과는 다른 패키지입니다. 끝이 `Tools.DotNet`으로 끝나는 CLI 패키지 이름과 달리 이름이 `Tools`로 끝납니다.

CLI 명령에 대한 자세한 내용은 [.NET Core CLI](https://docs.microsoft.com/ef/core/miscellaneous/cli/dotnet)를 참조하세요.

PMC 명령에 대한 자세한 내용은 [패키지 관리자 콘솔(Visual Studio)](https://docs.microsoft.com/ef/core/miscellaneous/cli/powershell)을 참조하세요.

## <a name="summary"></a>요약

이 자습서에서는 첫 번째 마이그레이션을 만들고 적용하는 방법을 살펴보았습니다. 다음 자습서에서는 데이터 모델을 확장하여 더 많은 고급 항목을 살펴봅니다. 방식에 따라 추가 마이그레이션을 만들고 적용하게 됩니다.
::: moniker-end

> [!div class="step-by-step"]
> [이전](sort-filter-page.md)
> [다음](complex-data-model.md)
