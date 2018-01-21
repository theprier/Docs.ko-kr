---
title: "EF 코어 8-마이그레이션-4 사용 하 여 razor 페이지"
author: rick-anderson
description: "이 자습서에서는 ASP.NET Core MVC 응용 프로그램에서 데이터 모델 변경 내용을 관리 하기 위한 EF 코어 마이그레이션 기능을 사용 하 여 시작 합니다."
ms.author: riande
manager: wpickett
ms.date: 10/15/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: data/ef-rp/migrations
ms.openlocfilehash: 26fbda99b0c1dfa2d09cf387e43f3123c58215f8
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="migrations---ef-core-with-razor-pages-tutorial-4-of-8"></a>마이그레이션-EF 코어 Razor 페이지 자습서 (8 4)

여 [Tom Dykstra](https://github.com/tdykstra), [Jon P Smith](https://twitter.com/thereformedprog), 및 [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE[about the series](../../includes/RP-EF/intro.md)]

이 자습서에서는 데이터 모델 변경 내용을 관리 하기 위한 EF 핵심 마이그레이션 기능이 사용 됩니다.

문제를 해결할 수 없는를 실행 하는 경우 다운로드는 [이 단계에 대 한 완성 된 앱](
https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part4-migrations)합니다.

새 응용 프로그램 개발 된 데이터 변경 내용을 자주 모델링 합니다. 될 때마다 모델 변경 내용을 모델이 가져옵니다 데이터베이스와 동기화 합니다. 이 자습서를 존재 하지 않는 경우 데이터베이스를 만들려면 Entity Framework를 구성 하 여 시작 합니다. 데이터 모델이 변경 될 때마다:

* DB 삭제 됩니다.
* EF는 모델과 일치 하는 새 브러시를 만듭니다.
* 응용 프로그램 테스트 데이터로 DB을 시드합니다.

DB 데이터 모델을 통해 동기화를 유지 하려면이 방법을 프로덕션에 앱을 배포할 때까지 잘 작동 합니다. 앱이 프로덕션 환경에서 실행 중인 경우 유지 관리 하는 데이터를 저장 일반적으로 합니다. 응용 프로그램 (예: 새 열 추가) 변경 될 때마다 DB 테스트를 시작할 수 없습니다. EF 코어 마이그레이션 기능 EF 새 DB 만드는 대신 DB 스키마를 업데이트 하는 코어를 사용 하 여이 문제를 해결 합니다.

삭제 하 고는 데이터 모델이 변경 하는 경우에 DB를 다시 만들어, 대신 마이그레이션 스키마를 업데이트 한 기존 데이터를 유지 합니다.

## <a name="entity-framework-core-nuget-packages-for-migrations"></a>마이그레이션을 위한 Entity Framework Core NuGet 패키지

마이그레이션 작업을 하려면 사용 된 **패키지 관리자 콘솔** (PMC) 또는 명령줄 인터페이스 (CLI). 이 자습서에는 CLI 명령을 사용 하는 방법을 보여 줍니다. PMC에 대 한 정보는 [이 자습서의 최종](#pmc)합니다.

제공 되는 CLI (명령줄 인터페이스)에 대 한 EF 핵심 도구 [Microsoft.EntityFrameworkCore.Tools.DotNet](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools.DotNet)합니다. 이 패키지를 설치 하려면 추가 하는 `DotNetCliToolReference` 컬렉션에는 *.csproj* 표시 된 것 처럼 파일입니다. **참고:** 이 패키지를 편집 하 여 설치 해야는 *.csproj* 파일입니다. `install-package` 이 패키지를 설치 명령이 나 패키지 관리자 GUI 사용할 수 없습니다. 편집 된 *.csproj* 파일에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 여 **솔루션 탐색기** 선택 하 고 **ContosoUniversity.csproj 편집**합니다.

업데이트 된 다음 태그를 보여 줍니다 *.csproj* 강조 표시 EF 코어 CLI 도구 파일:

[!code-xml[](intro/samples/cu/ContosoUniversity.csproj?highlight=12)]
  
버전 번호를 앞의 예제 자습서 기록 될 때 최신 버전 이었습니다. 다른 패키지에는 EF 코어 CLI 도구에 대 한 동일한 버전을 사용 합니다.

## <a name="change-the-connection-string"></a>연결 문자열 변경

에 *appsettings.json* 파일, DB 연결 문자열의 이름을 ContosoUniversity2로 변경 합니다.

[!code-json[Main](intro/samples/cu/appsettings2.json?range=1-4)]

연결 문자열에 DB 이름을 변경 하면 새 DB를 만들려면 첫 번째 마이그레이션이 합니다. 해당 이름으로 존재 하지 않기 때문에 새 DB 만들어집니다. 연결 문자열을 변경 마이그레이션을 시작 하기 위한 필요 하지 않습니다.

DB 이름 변경 하는 대신 DB을 삭제 하는 중입니다. 사용 하 여 **SQL Server 개체 탐색기** (SSOX) 또는 `database drop` CLI 명령을:

 ```console
 dotnet ef database drop
 ```

다음 섹션에는 CLI 명령을 실행 하는 방법을 설명 합니다.

## <a name="create-an-initial-migration"></a>초기 마이그레이션 만들기

프로젝트를 빌드합니다.

명령 창을 열고 프로젝트 폴더로 이동 합니다. 프로젝트 폴더에 포함 된 *Startup.cs* 파일입니다.

명령 창에서 다음을 입력 합니다.

```console
dotnet ef migrations add InitialCreate
```

명령 창에는 다음과 유사한 정보가 표시 됩니다.

```console
info: Microsoft.AspNetCore.DataProtection.KeyManagement.XmlKeyManager[0]
      User profile is available. Using 'C:\Users\username\AppData\Local\ASP.NET\DataProtection-Keys' as key repository and Windows DPAPI to encrypt keys at rest.
info: Microsoft.EntityFrameworkCore.Infrastructure[100403]
      Entity Framework Core 2.0.0-rtm-26452 initialized 'SchoolContext' using provider 'Microsoft.EntityFrameworkCore.SqlServer' with options: None
Done. To undo this action, use 'ef migrations remove'
```

메시지와 함께 마이그레이션이 실패할 경우 "*... 파일에 액세스할 수 없습니다 ContosoUniversity.dll 다른 프로세스에서 사용 되 고 있으므로 합니다.* " 표시 됩니다.

* IIS Express를 중지 합니다.

   * 종료 하 고 Visual Studio를 다시 시작 또는
   * Windows 시스템 트레이에서 아이콘을 IIS Express를 찾습니다.
   * IIS Express 아이콘을 마우스 오른쪽 단추로 누른 **ContosoUniversity > 사이트 중지**합니다.

오류 메시지 "빌드 실패 했습니다." 하는 경우 가 표시 된 명령을 다시 실행 합니다. 이 오류가 발생할 경우이 자습서의 맨 아래에 메모를 둡니다.

### <a name="examine-the-up-and-down-methods"></a>위쪽을 검토 하 고 아래쪽 메서드

EF 코어 명령 `migrations add` DB에서 만드는 코드를 생성 합니다. 이 마이그레이션 코드에는 *마이그레이션\<타임 스탬프 > _InitialCreate.cs* 파일입니다. `Up` 의 메서드는 `InitialCreate` 클래스는 데이터 모델 엔터티 집합에 해당 하는 DB 테이블을 만듭니다. `Down` 다음 예제와 같이, 메서드 삭제:

[!code-csharp[Main](intro/samples/cu/Migrations/20171026010210_InitialCreate.cs?range=8-24,77-)]

마이그레이션 호출은 `Up` 마이그레이션에 대 한 데이터 모델 변경 내용을 구현 하려면 메서드. Update, 마이그레이션 호출을 롤백해야 하는 명령을 입력할 때는 `Down` 메서드.

위의 코드는 초기 마이그레이션에 대 한 합니다. 해당 코드를 만든 경우의 `migrations add InitialCreate` 명령이 실행 된 합니다. 마이그레이션 name 매개 변수 (이 예제에서 "InitialCreate")는 파일 이름에 사용 됩니다. 유효한 파일 이름을 마이그레이션 이름일 수 있습니다. 단어 또는 구를 마이그레이션에서 수행 되는 것을 요약 하는 선택 하는 것이 좋습니다. 예를 들어 department 테이블을 추가 하는 마이그레이션 파일명 "AddDepartmentTable."

초기 마이그레이션 만들어지고 DB 종료 될 경우:

* DB 만들기 코드가 생성 됩니다.
* DB 만들기 코드 DB에 이미 데이터 모델 일치 하기 때문에 실행할 필요가 없습니다. DB 만들기 코드를 실행 하는 경우에 DB에 이미 데이터 모델 일치 하기 때문에 변경 내용을 확인 하지 않습니다.

응용 프로그램을 새 환경에 배포 될 때 DB 만들려고 DB 생성 코드를 실행 해야 합니다.

이전에 DB에 대 한 새 이름을 사용 하도록 연결 문자열이 변경 되었습니다. 지정 된 DB 존재 하지 않습니다 마이그레이션 DB를 만듭니다.

### <a name="examine-the-data-model-snapshot"></a>데이터 모델 스냅숏을 검사합니다

마이그레이션 만듭니다는 *스냅숏* 에 현재 DB 스키마의 *Migrations/SchoolContextModelSnapshot.cs*:

[!code-csharp[Main](intro/samples/cu/Migrations/SchoolContextModelSnapshot1.cs?name=snippet_Truncate)]

현재 DB 스키마 코드에 표시 되므로, EF 코어 마이그레이션 만들려는 DB 상호 작용할 필요가 없습니다. 마이그레이션에 추가 하면 EF 코어 스냅숏 파일에 데이터 모델을 비교 하 여 변경 내용을 결정 합니다. DB 업데이트 해야 하는 경우에 EF 코어 DB 상호 작용 합니다.

스냅숏 파일을 만든 마이그레이션과 함께 동기화 되어야 합니다. 마이그레이션 라는 파일을 삭제 하 여 제거할 수 없습니다  *\<타임 스탬프 > _\<migrationname >.cs*합니다. 해당 파일을 삭제 하는 경우 나머지 마이그레이션은 DB 스냅숏 파일과 함께 동기화 되지 않았습니다. 사용 하 여 추가 하는 마지막 마이그레이션을 삭제 하려면는 [dotnet ef 마이그레이션 제거](https://docs.microsoft.com/ef/core/miscellaneous/cli/dotnet#dotnet-ef-migrations-remove) 명령입니다.

## <a name="remove-ensurecreated"></a>EnsureCreated 제거

초기 개발 작업에 `EnsureCreated` 명령이 사용 되었습니다. 이 자습서에서는 마이그레이션은 사용 됩니다. `EnsureCreated`다음 limatitions에 있습니다.

* 마이그레이션을 무시 하 고 DB 및 스키마를 만듭니다.
* 마이그레이션 테이블을 만들지 않습니다.
* 수 *하지* 마이그레이션과 함께 사용할 수 있습니다.
* 위한 테스트, 신속한 프로토타입 DB을 삭제 하 고 다시 자주를 생성 합니다.

다음 줄을 제거 `DbInitializer`:

```csharp
context.Database.EnsureCreated();
```

## <a name="apply-the-migration-to-the-db-in-development"></a>마이그레이션 개발에서 DB에 적용

명령 창에서 DB 및 테이블을 만들려면 다음을 입력 합니다.

```console
dotnet ef database update
```

참고: 경우는 `update` 명령은 "실패 한 빌드 합니다." 오류 반환:

* 명령을 다시 실행 합니다.
* 다시 실패 하는 경우 Visual Studio를 종료 한 후 실행 된 `update` 명령입니다.
* 페이지의 맨 아래에 메시지를 유지 합니다.

명령의 출력은는 `migrations add` 출력 명령입니다. 이전 명령에서 DB를 설정 하는 SQL 명령에 대 한 로그 표시 됩니다. 대부분의 로그는 다음 예제 출력에서 생략 됩니다.

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

로그 메시지의 세부 수준을 줄이려면에서 로그 수준을 변경할 수는 *appsettings 합니다. Development.json* 파일입니다. 자세한 내용은 참조 [로깅 소개](xref:fundamentals/logging/index)합니다.

사용 하 여 **SQL Server 개체 탐색기** DB를 검사 합니다. 추가 확인 프로그램 `__EFMigrationsHistory` 테이블입니다. `__EFMigrationsHistory` DB에 적용 된 마이그레이션이 테이블의 추적 합니다. 데이터를 볼는 `__EFMigrationsHistory` 테이블을 첫 번째 마이그레이션에 한 행씩 보여 줍니다. 마지막 로그 CLI 출력 앞의 예제에서이 행을 만들고 INSERT 문을 보여 줍니다.

응용 프로그램을 실행 하 고 작동 하는 것을 확인 합니다.

## <a name="appling-migrations-in-production"></a>프로덕션 환경에서 적용 마이그레이션

프로덕션 응용 프로그램 해야 하는 것이 좋습니다 **하지** 호출 [Database.Migrate](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.relationaldatabasefacadeextensions.migrate?view=efcore-2.0#Microsoft_EntityFrameworkCore_RelationalDatabaseFacadeExtensions_Migrate_Microsoft_EntityFrameworkCore_Infrastructure_DatabaseFacade_) 응용 프로그램 시작 시. `Migrate`서버 팜의 응용 프로그램에서 호출할 수 없습니다. 예를 들어, 응용 프로그램 (앱의 여러 인스턴스가 실행 중인) 확장을 사용 하 여 배포 하는 클라우드 되었습니다.

데이터베이스 마이그레이션 제어 되는 방식에서 및 배포의 일부로 수행 되어야 합니다. 프로덕션 데이터베이스 마이그레이션 방법 다음과 같습니다.

* 마이그레이션을 사용 하 여 SQL 스크립트를 작성 및 배포에서 SQL 스크립트를 사용 하 여 합니다.
* 실행 `dotnet ef database update` 제어 된 환경에서 합니다.

사용 하 여 EF 코어는 `__MigrationsHistory` 테이블을 참조 하는 마이그레이션을 실행 해야 합니다. DB 최신 상태 이면 마이그레이션 없음 실행 됩니다.

<a id="pmc"></a>
## <a name="command-line-interface-cli-vs-package-manager-console-pmc"></a>CLI (명령줄 인터페이스) vs입니다. 패키지 관리자 콘솔 (PMC)

EF 코어 마이그레이션 관리 하기 위한 도구에서 제공 됩니다.

* .NET core CLI 명령입니다.
* Visual Studio에서 PowerShell cmdlet **패키지 관리자 콘솔** (PMC) 창.

PMC를 사용 하 여 선호 하는 개발자도,이 자습서에는 CLI를 사용 하는 방법을 보여 줍니다.

PMC EF 코어 주석은에 [Microsoft.EntityFrameworkCore.Tools](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools) 패키지 합니다. 이 패키지에 포함 되어는 [Microsoft.AspNetCore.All](xref:fundamentals/metapackage) metapackage, 하므로 설치할 필요가 없습니다.

**중요:** 이 동일한 패키지를 편집 하 여 CLI를 설치 하는 것과는 *.csproj* 파일입니다. 이 개체의 이름이 끝나는 `Tools`, CLI 패키지 이름에는 달리 `Tools.DotNet`합니다.

CLI 명령에 대 한 자세한 내용은 참조 [.NET Core CLI](https://docs.microsoft.com/ef/core/miscellaneous/cli/dotnet)합니다.

PMC 명령에 대 한 자세한 내용은 참조 [패키지 관리자 콘솔 (Visual Studio)](https://docs.microsoft.com/ef/core/miscellaneous/cli/powershell)합니다.

## <a name="troubleshooting"></a>문제 해결

다운로드는 [이 단계에 대 한 완성 된 앱](
https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part4-migrations)합니다.

응용 프로그램에서는 다음과 같은 예외가 생성 됩니다.

```text
`SqlException: Cannot open database "ContosoUniversity" requested by the login.
The login failed.
Login failed for user 'user name'.
```

솔루션: 실행`dotnet ef database update`

경우는 `update` 명령은 "실패 한 빌드 합니다." 오류 반환:

* 명령을 다시 실행 합니다.
* 페이지의 맨 아래에 메시지를 유지 합니다.

>[!div class="step-by-step"]
[이전](xref:data/ef-rp/sort-filter-page)
[다음](xref:data/ef-rp/complex-data-model)
