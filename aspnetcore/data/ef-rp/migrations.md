---
title: "EF Core를 사용한 Razor 페이지 - 마이그레이션 - 4/8"
author: rick-anderson
description: "이 자습서에서는 ASP.NET Core MVC 앱에서 데이터 모델 변경 관리를 위해 EF Core 마이그레이션 기능을 사용하는 것을 시작합니다."
manager: wpickett
ms.author: riande
ms.date: 10/15/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: data/ef-rp/migrations
ms.openlocfilehash: e89d95702cb94556bc6e5dc73253c51acaa11578
ms.sourcegitcommit: 18d1dc86770f2e272d93c7e1cddfc095c5995d9e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2018
---
# <a name="migrations---ef-core-with-razor-pages-tutorial-4-of-8"></a>마이그레이션 - Razor 페이지를 사용한 EF Core 자습서(4/8)

작성자: [Tom Dykstra](https://github.com/tdykstra), [Jon P Smith](https://twitter.com/thereformedprog) 및 [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE[about the series](../../includes/RP-EF/intro.md)]

이 자습서에서는 데이터 모델 변경 관리를 위한 EF Core 마이그레이션 기능이 사용됩니다.

해결할 수 없는 문제가 발생한 경우 [이 단계에 완성된 앱](
https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part4-migrations)을 다운로드합니다.

새 앱이 개발되면 데이터 모델이 자주 변경됩니다. 모델이 변경될 때마다 모델이 데이터베이스와 동기화 해제됩니다. 이 자습서는 존재하지 않는 경우 데이터베이스를 만들도록 Entity Framework를 구성하여 시작되었습니다. 데이터 모델이 변경될 때마다 다음이 수행됩니다.

* DB가 삭제됩니다.
* EF는 모델과 일치하는 새 항목을 만듭니다.
* 앱은 테스트 데이터로 DB를 시드합니다.

DB를 데이터 모델과 동기화된 상태로 유지하는 이 접근 방식은 앱을 프로덕션 환경에 배포할 때까지 잘 작동합니다. 앱이 프로덕션 환경에서 실행 중인 경우 일반적으로 유지 관리해야 하는 데이터를 저장합니다. 앱은 변경(예: 새 열 추가)될 때마다 테스트 DB로 시작될 수 없습니다. EF Core 마이그레이션 기능은 EF Core에서 새 DB를 만드는 대신 DB 스키마를 업데이트하도록 하여 이 문제를 해결합니다.

데이터 모델이 변경될 때 DB를 삭제하고 다시 작성하는 대신 마이그레이션은 스키마를 업데이트하고 기존 데이터를 유지합니다.

## <a name="entity-framework-core-nuget-packages-for-migrations"></a>마이그레이션을 위한 Entity Framework Core NuGet 패키지

마이그레이션 작업을 위해 **PMC(패키지 관리자 콘솔)** 또는 CLI(명령줄 인터페이스)를 사용합니다. 이 자습서에는 CLI 명령을 사용하는 방법을 보여 줍니다. PMC에 대한 정보는 [이 자습서의 끝](#pmc)에 있습니다.

CLI(명령줄 인터페이스)용 EF Core 도구는 [Microsoft.EntityFrameworkCore.Tools.DotNet](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools.DotNet)에서 제공됩니다. 이 패키지를 설치하려면 표시된 것처럼 *.csproj* 파일의 `DotNetCliToolReference` 컬렉션에 패키지를 추가합니다. **참고:** *.csproj* 파일을 편집하여 이 패키지를 설치해야 합니다. 이 패키지를 설치하는 데 `install-package` 명령이나 패키지 관리자 GUI를 사용할 수 없습니다. **솔루션 탐색기**에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭하고 **ContosoUniversity.csproj 편집**을 선택하여 *.csproj* 파일을 편집합니다.

다음 표시는 EF Core CLI 도구가 강조 표시된 업데이트된 *.csproj* 파일을 보여 줍니다.

[!code-xml[](intro/samples/cu/ContosoUniversity.csproj?highlight=12)]
  
이전 예제의 버전 번호는 이 자습서가 작성된 당시의 버전 번호입니다. 다른 패키지에 있는 EF Core CLI 도구에 대해 동일한 버전을 사용합니다.

## <a name="change-the-connection-string"></a>연결 문자열 변경

*appsettings.json* 파일에서 연결 문자열의 DB 이름을 ContosoUniversity2로 변경합니다.

[!code-json[Main](intro/samples/cu/appsettings2.json?range=1-4)]

연결 문자열에서 DB 이름을 변경하면 첫 번째 마이그레이션으로 인해 새 DB가 만들어집니다. 이름이 존재하지 않으므로 새 DB가 만들어집니다. 마이그레이션을 시작하기 위해 연결 문자열을 변경하지 않아도 됩니다.

DB 이름을 변경하는 다른 방법은 DB를 삭제하는 것입니다. **SSOX(SQL Server 개체 탐색기)** 또는 `database drop` CLI 명령을 사용합니다.

 ```console
 dotnet ef database drop
 ```

다음 섹션에는 CLI 명령을 실행하는 방법을 설명합니다.

## <a name="create-an-initial-migration"></a>초기 마이그레이션 만들기

프로젝트를 빌드합니다.

명령 창을 열고 프로젝트 폴더로 이동합니다. 프로젝트 폴더에는 *Startup.cs* 파일이 포함되어 있습니다.

명령 창에서 다음을 입력합니다.

```console
dotnet ef migrations add InitialCreate
```

명령 창에는 다음과 유사한 정보가 표시됩니다.

```console
info: Microsoft.AspNetCore.DataProtection.KeyManagement.XmlKeyManager[0]
      User profile is available. Using 'C:\Users\username\AppData\Local\ASP.NET\DataProtection-Keys' as key repository and Windows DPAPI to encrypt keys at rest.
info: Microsoft.EntityFrameworkCore.Infrastructure[100403]
      Entity Framework Core 2.0.0-rtm-26452 initialized 'SchoolContext' using provider 'Microsoft.EntityFrameworkCore.SqlServer' with options: None
Done. To undo this action, use 'ef migrations remove'
```

"*ContosoUniversity.dll 파일은 다른 프로세스에서 사용하고 있으므로 액세스할 수 없습니다.*"라는 메시지가 표시되고 마이그레이션에 실패하는 경우:

* IIS Express를 중지합니다.

   * Visual Studio를 종료하고 다시 시작하거나
   * Windows 시스템 트레이에서 IIS Express 아이콘을 찾습니다.
   * IIS Express 아이콘을 마우스 오른쪽 단추로 클릭한 후 **ContosoUniversity > 사이트 중지**를 클릭합니다.

오류 메시지 "빌드하지 못했습니다."가 표시되는 경우 명령을 다시 실행합니다. 이 오류가 발생할 경우 이 자습서의 맨 아래에 메모를 남깁니다.

### <a name="examine-the-up-and-down-methods"></a>Up 및 Down 메서드 검사

EF Core 명령 `migrations add`로 DB를 생성하는 코드를 생성했습니다. 이 마이그레이션 코드는 *마이그레이션\<timestamp>_InitialCreate.cs* 파일에 있습니다. `InitialCreate` 클래스dml `Up` 메서드는 데이터 모델 엔터티 집합에 해당하는 DB 테이블을 만듭니다. `Down` 메서드는 다음 예제처럼 테이블을 삭제합니다.

[!code-csharp[Main](intro/samples/cu/Migrations/20171026010210_InitialCreate.cs?range=8-24,77-)]

마이그레이션에서는 마이그레이션을 위한 데이터 모델 변경을 구현하기 위해 `Up` 메서드를 호출합니다. 업데이트를 롤백하는 명령을 입력하면 마이그레이션에서 `Down` 메서드를 호출합니다.

위의 코드는 초기 마이그레이션에 대한 코드입니다. 이 코드는 `migrations add InitialCreate` 명령을 실행할 때 만들어집니다. 파일 이름에는 마이그레이션 이름 매개 변수(이 예제에서 "InitialCreate")가 사용됩니다. 마이그레이션 이름은 임의의 유효한 파일 이름이 될 수 있습니다. 마이그레이션에서 수행 중인 작업을 요약한 단어 또는 구를 선택하는 것이 가장 좋습니다. 예를 들어 부서 테이블을 추가한 마이그레이션은 "AddDepartmentTable"이라고 할 수 있습니다.

초기 마이그레이션이 만들어지고 DB가 종료되는 경우:

* DB 만들기 코드가 생성됩니다.
* DB는 데이터 모델과 이미 일치하므로 DB 만들기 코드를 실행할 필요가 없습니다. DB 만들기 코드가 실행되면 DB가 데이터 모델과 이미 일치하므로 변경하지 않습니다.

앱이 새 환경에 배포되면 DB 만들기 코드를 실행하여 DB를 만들어야 합니다.

이전에는 DB에 새 이름을 사용하도록 연결 문자열을 변경했습니다. 지정된 DB가 존재하지 않으므로 마이그레이션에서 DB를 만듭니다.

### <a name="examine-the-data-model-snapshot"></a>데이터 모델 스냅숏 검사

마이그레이션에서는 현재 DB 스키마의 *스냅숏*을 *Migrations/SchoolContextModelSnapshot.cs*에 만듭니다.

[!code-csharp[Main](intro/samples/cu/Migrations/SchoolContextModelSnapshot1.cs?name=snippet_Truncate)]

현재 DB 스키마가 쿄드에 표시되므로 EF Core는 마이그레이션을 만들기 위해 DB와 상호 작용할 필요가 없습니다. 마이그레이션을 추가하면 EF Core가 데이터 모델과 스냅숏 파일을 비교하여 변경 내용을 확인합니다. DB를 업데이트해야 하는 경우에만 EF Core가 DB와 상호 작용합니다.

스냅숏 파일은 스냅숏이 생성된 마이그레이션과 함께 동기화되어야 합니다. *\<timestamp>_\<migrationname>.cs*라는 파일을 삭제하여 마이그레이션을 제거할 수 없습니다. 해당 파일을 삭제하면 나머지 마이그레이션이 DB 스냅숏 파일과 동기화가 해제됩니다. 추가된 마지막 마이그레이션을 삭제하려면 [dotnet ef migrations remove](https://docs.microsoft.com/ef/core/miscellaneous/cli/dotnet#dotnet-ef-migrations-remove) 명령을 사용합니다.

## <a name="remove-ensurecreated"></a>EnsureCreated 제거

초기 개발에는 `EnsureCreated` 명령이 사용되었습니다. 이 자습서에서는 마이그레이션이 사용됩니다. `EnsureCreated`에는 다음과 같은 제한 사항이 적용됩니다.

* 마이그레이션을 무시하고 DB 및 스키마를 만듭니다.
* 마이그레이션 테이블을 만들지 않습니다.
* 마이그레이션에 사용할 수 *없습니다*.
* DB를 삭제하고 자주 다시 생성하는 테스트 또는 신속한 프로토타입 만들기를 위해 설계되었습니다.

`DbInitializer`에서 다음 줄을 제거합니다.

```csharp
context.Database.EnsureCreated();
```

## <a name="apply-the-migration-to-the-db-in-development"></a>개발 중인 DB에 마이그레이션 적용

명령 창에서 다음을 입력하고 DB 및 테이블을 만듭니다.

```console
dotnet ef database update
```

참고: `update` 명령에서 "빌드하지 못했습니다."를 반환하는 경우:

* 명령을 다시 실행합니다.
* 다시 실패하는 경우 Visual Studio를 종료한 후 `update` 명령을 실행합니다.
* 페이지의 맨 아래에 메시지를 남깁니다.

명령의 출력은는 `migrations add` 명령 출력과 유사합니다. 이전 명령에서 DB를 설정하는 SQL 명령에 대한 로그가 표시됩니다. 대부분의 로그는 다음 예제 출력에서 생략됩니다.

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

로그 메시지의 세부 수준을 줄이기 위해 *appsettings 합니다. Development.json* 파일에서 로그 수준을 변경할 수 있습니다. 자세한 내용은 [로깅 소개](xref:fundamentals/logging/index)를 참조하세요.

**SQL Server 개체 탐색기**를 사용하여 DB를 검사합니다. `__EFMigrationsHistory` 테이블이 추가된 것을 볼 수 있습니다. `__EFMigrationsHistory` 테이블은 DB에 적용된 마이그레이션을 추적합니다. `__EFMigrationsHistory` 테이블의 데이터를 보면 첫 번째 마이그레이션에 대해 한 행이 표시됩니다. 앞의 CLI 출력 예제의 마지막 로그는 이 행을 만드는 INSERT 문을 보여 줍니다.

앱을 실행하고 모든 항목이 작동하는지 확인합니다.

## <a name="appling-migrations-in-production"></a>프로덕션 환경에서 마이그레이션 적용

프로덕션 앱은 응용 프로그램 시작 시 [Database.Migrate](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.relationaldatabasefacadeextensions.migrate?view=efcore-2.0#Microsoft_EntityFrameworkCore_RelationalDatabaseFacadeExtensions_Migrate_Microsoft_EntityFrameworkCore_Infrastructure_DatabaseFacade_)를 호출하지 **않는 것이** 좋습니다. 서버 팜의 앱에서 `Migrate`를 호출하면 안됩니다. 예를 들어, 앱이 스케일 아웃으로 클라우드에 배포된 경우(앱의 여러 인스턴스가 실행 중임)

데이터베이스 마이그레이션은 배포의 일부로 제어된 방식으로 수행되어야 합니다. 프로덕션 데이터베이스 마이그레이션 방법은 다음과 같습니다.

* 마이그레이션을 사용하여 SQL 스크립트를 작성하고 배포 시 SQL 스크립트 사용
* 제어된 환경에서 `dotnet ef database update` 실행

EF Core는 `__MigrationsHistory` 테이블을 사용하여 마이그레이션을 실행해야 하는지 확인합니다. DB가 최신 상태이면 마이그레이션이 실행되지 않습니다.

<a id="pmc"></a>
## <a name="command-line-interface-cli-vs-package-manager-console-pmc"></a>CLI(명령줄 인터페이스) 및 PMC(패키지 관리자 콘솔)

마이그레이션 관리를 위한 EF Core 도구는 다음에서 제공됩니다.

* .NET Core CLI 명령
* Visual Studio **PMC(패키지 관리자 콘솔)** 창에서 PowerShell cmdlet

이 자습서에서는 CLI를 사용하는 방법을 보여 주며 일부 개발자는 PMC 사용을 선호합니다.

PMC용 EF Core 명령은 [Microsoft.EntityFrameworkCore.Tools](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools) 패키지에 있습니다. 이 패키지는 [Microsoft.AspNetCore.All](xref:fundamentals/metapackage) 메타패키지에 포함되므로 설치할 필요가 없습니다.

**중요:** *.csproj* 파일을 편집하여 CLI에 대해 설치한 것과 다른 패키지입니다. 끝이 `Tools.DotNet`으로 끝나는 CLI 패키지 이름과 달리 이름이 `Tools`로 끝납니다.

CLI 명령에 대한 자세한 내용은 [.NET Core CLI](https://docs.microsoft.com/ef/core/miscellaneous/cli/dotnet)를 참조하세요.

PMC 명령에 대한 자세한 내용은 [패키지 관리자 콘솔(Visual Studio)](https://docs.microsoft.com/ef/core/miscellaneous/cli/powershell)을 참조하세요.

## <a name="troubleshooting"></a>문제 해결

[이 단계에 대해 완성된 앱](
https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part4-migrations)을 다운로드합니다.

앱에서는 다음과 같은 예외가 생성됩니다.

```text
`SqlException: Cannot open database "ContosoUniversity" requested by the login.
The login failed.
Login failed for user 'user name'.
```

해결 방법: `dotnet ef database update`를 실행합니다.

`update` 명령에서 "빌드하지 못했습니다."를 반환하는 경우:

* 명령을 다시 실행합니다.
* 페이지의 맨 아래에 메시지를 남깁니다.

>[!div class="step-by-step"]
[이전](xref:data/ef-rp/sort-filter-page)
[다음](xref:data/ef-rp/complex-data-model)
