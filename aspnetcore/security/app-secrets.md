---
title: ASP.NET Core에서 개발의 앱 암호의 안전한 저장소
author: rick-anderson
description: 저장 하 고 ASP.NET Core 응용 프로그램을 개발 하는 동안 앱 암호로 중요 한 정보를 검색 하는 방법을 알아봅니다.
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 05/23/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/app-secrets
ms.openlocfilehash: ece2bf541df2b4acac60a88767cc57ede473bd49
ms.sourcegitcommit: 1b94305cc79843e2b0866dae811dab61c21980ad
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2018
---
# <a name="safe-storage-of-app-secrets-in-development-in-aspnet-core"></a>ASP.NET Core에서 개발의 앱 암호의 안전한 저장소

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT), [김 Roth](https://github.com/danroth27), 및 [Scott Addie](https://github.com/scottaddie)

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/app-secrets/samples)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

이 문서에 저장 하 고 ASP.NET Core 응용 프로그램을 개발 하는 동안 중요 한 데이터를 검색 하는 기술을 설명 합니다. 소스 코드에서 암호 또는 기타 중요 한 데이터를 저장 해서는 안 하 고 개발에서 생산 암호를 사용 하거나 모드를 테스트 하지 않아야 합니다. 저장 하 고 Azure 테스트 및 프로덕션 비밀 정보를 보호할 수는 [Azure 키 자격 증명 모음 구성 공급자](xref:security/key-vault-configuration)합니다.

## <a name="environment-variables"></a>환경 변수

응용 프로그램 보안 코드 또는 로컬 구성 파일의 저장소를 방지 하기 위해 환경 변수를 사용 합니다. 환경 변수는 모든 이전에 지정 된 구성 소스에 대 한 구성 값을 재정의 합니다.

::: moniker range="<= aspnetcore-1.1"
호출 하 여 환경 변수 값을 읽는 구성 [AddEnvironmentVariables](/dotnet/api/microsoft.extensions.configuration.environmentvariablesextensions.addenvironmentvariables) 에 `Startup` 생성자:

[!code-csharp[](app-secrets/samples/1.x/UserSecrets/Startup.cs?name=snippet_StartupConstructor&highlight=10)]
::: moniker-end

ASP.NET Core 웹 응용 프로그램 고려 **개별 사용자 계정** 보안을 사용 합니다. 프로젝트의 기본 데이터베이스 연결 문자열을 포함 되어 *appsettings.json* 키와 파일 `DefaultConnection`합니다. 기본 연결 문자열은 localdb 사용자 모드에서 실행 되 고 암호가 필요 하지 않습니다. 응용 프로그램 배포 시는 `DefaultConnection` 환경 변수 값과 키 값을 재정의할 수 있습니다. 환경 변수는 중요 한 자격 증명으로 완전 한 연결 문자열을 저장할 수 있습니다.

> [!WARNING]
> 환경 변수는 일반적으로 암호화 되지 않은 일반 텍스트에 저장 됩니다. 컴퓨터 또는 프로세스가 손상 되 면 환경 변수는 신뢰할 수 없는 당사자가 액세스할 수 있습니다. 사용자의 비밀으로 공개 되지 않도록 추가 조치가 필요할 수 있습니다.

## <a name="secret-manager"></a>Secret Manager

암호 관리자 도구는 ASP.NET Core 프로젝트를 개발 하는 동안 중요 한 데이터를 저장합니다. 이 컨텍스트에서 중요 한 데이터 조각이 응용 프로그램 암호입니다. 앱 암호는 프로젝트 트리에서 별도 위치에 저장 됩니다. 앱 암호는 특정 프로젝트와 관련 된 또는 여러 프로젝트 간에 공유 됩니다. 앱 암호는 소스 제어에 체크 인 되지 않습니다.

> [!WARNING]
> 암호 관리자 도구 저장 된 암호를 암호화 하지 않습니다 하 고 신뢰할 수 있는 저장소로 처리 하지 않아야 합니다. 개발 용도로입니다. 키와 값은 사용자 프로필 디렉터리에 위치한 JSON 구성 파일에 저장됩니다. 

## <a name="how-the-secret-manager-tool-works"></a>Secret Manager 도구의 동작 방식

Secret Manager 도구는 값이 저장되는 위치 및 방법 같은 구현에 관한 세부적인 내용을 추상화합니다. 이런 세부적인 내용을 모르더라도 Secret Manager 도구를 사용하는 데는 아무런 지장이 없습니다.  값은 로컬 컴퓨터에서 시스템으로 보호 된 사용자 프로필 폴더에는 JSON 구성 파일에 저장 됩니다.

# <a name="windowstabwindows"></a>[Windows](#tab/windows)

파일 시스템 경로:

`%APPDATA%\Microsoft\UserSecrets\<user_secrets_id>\secrets.json`

# <a name="macostabmacos"></a>[macOS](#tab/macos)

파일 시스템 경로:

`~/.microsoft/usersecrets/<user_secrets_id>/secrets.json`

# <a name="linuxtablinux"></a>[Linux](#tab/linux)

파일 시스템 경로:

`~/.microsoft/usersecrets/<user_secrets_id>/secrets.json`

---

앞의 파일 경로, 대체 `<user_secrets_id>` 와 `UserSecretsId` 에 지정 된 값의 *.csproj* 파일입니다.

위치 또는 보안 관리자 도구와 함께 저장 되는 데이터의 형식에 의존 하는 코드를 작성 하지 마십시오. 이러한 구현 정보를 변경할 수 있습니다. 예를 들어 비밀 값 암호화 되지 않습니다 되지만 나중에 있습니다.

::: moniker range="<= aspnetcore-2.0"
## <a name="install-the-secret-manager-tool"></a>암호 관리자 도구를 설치 합니다.

암호 관리자 도구는.NET Core SDK 2.1.300부터.NET Core CLI 함께 제공 됩니다. 2.1.300 이전 버전을.NET Core SDK, 도구를 설치 해야만 됩니다.

> [!TIP]
> 실행 `dotnet --version` 명령 셸을 설치 된.NET Core SDK 버전 번호를 확인 합니다.

사용 중인.NET Core SDK 도구를 포함 하는 경우 경고가 표시 됩니다.

```console
The tool 'Microsoft.Extensions.SecretManager.Tools' is now included in the .NET Core SDK. Information on resolving this warning is available at (https://aka.ms/dotnetclitools-in-box).
```

설치는 [Microsoft.Extensions.SecretManager.Tools](https://www.nuget.org/packages/Microsoft.Extensions.SecretManager.Tools/) ASP.NET Core 프로젝트에 NuGet 패키지 합니다. 예를 들어:

[!code-xml[](app-secrets/samples/1.x/UserSecrets/UserSecrets.csproj?name=snippet_CsprojFile&highlight=13-14)]

도구 설치를 확인 하는 명령 셸에서 다음 명령을 실행 합니다.

```console
dotnet user-secrets -h
```

암호 관리자 도구 사용법 예제, 옵션 및 명령 도움말을 표시합니다.

```console
Usage: dotnet user-secrets [options] [command]

Options:
  -?|-h|--help                        Show help information
  --version                           Show version information
  -v|--verbose                        Show verbose output
  -p|--project <PROJECT>              Path to project. Defaults to searching the current directory.
  -c|--configuration <CONFIGURATION>  The project configuration to use. Defaults to 'Debug'.
  --id                                The user secret ID to use.

Commands:
  clear   Deletes all the application secrets
  list    Lists all the application secrets
  remove  Removes the specified user secret
  set     Sets the user secret to the specified value

Use "dotnet user-secrets [command] --help" for more information about a command.
```

> [!NOTE]
> 와 같은 디렉터리에 있어야는 *.csproj* 파일에 정의 된 도구를 실행 하는 *.csproj* 파일의 `DotNetCliToolReference` 요소입니다.
::: moniker-end

## <a name="set-a-secret"></a>암호를 설정 합니다.

암호 관리자 도구는 사용자 프로필에 저장 된 프로젝트 관련 구성 설정에서 작동 합니다. 사용자 암호를 사용 하려면 정의 `UserSecretsId` 요소 내에서 한 `PropertyGroup` 의 *.csproj* 파일입니다. 값 `UserSecretsId` 은 선택적 요소 이지만 프로젝트에 고유 합니다. 개발자는 대부분 `UserSecretsId` 값에 GUID를 생성해서 지정합니다. 

::: moniker range="<= aspnetcore-1.1"
[!code-xml[](app-secrets/samples/1.x/UserSecrets/UserSecrets.csproj?name=snippet_PropertyGroup&highlight=3)]
::: moniker-end
::: moniker range=">= aspnetcore-2.0"
[!code-xml[](app-secrets/samples/2.x/UserSecrets/UserSecrets.csproj?name=snippet_PropertyGroup&highlight=3)]
::: moniker-end

> [!TIP]
> Visual Studio에서 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **관리 사용자의 비밀** 상황에 맞는 메뉴입니다. 이 제스처 추가 `UserSecretsId` 에 GUID로 채워진 요소는 *.csproj* 파일입니다. Visual Studio가 열릴는 *secrets.json* 파일 텍스트 편집기에서. 내용을 대체 *secrets.json* 저장할 키-값 쌍을 포함 합니다. 예를 들면 [!INCLUDE[secrets.json file](~/includes/app-secrets/secrets-json-file.md)] 같은 형식입니다.

키와 해당 값으로 구성 된 앱 암호를 정의 합니다. 암호는 해당 프로젝트와 관련 `UserSecretsId` 값입니다. 예를 들어 있는 디렉터리에서 다음 명령을 실행는 *.csproj* 파일이 있습니다.

```console
dotnet user-secrets set "Movies:ServiceApiKey" "12345"
```

앞의 예제에서 콜론 나타냅니다 `Movies` 은 개체 리터럴을 `ServiceApiKey` 속성입니다.

암호 관리자 도구는 너무 다른 디렉터리에서 사용할 수 있습니다. 사용 하 여는 `--project` 옵션을 파일 시스템 경로 제공 하는 *.csproj* 파일이 있습니다. 예를 들어:

```console
dotnet user-secrets set "Movies:ServiceApiKey" "12345" --project "C:\apps\WebApp1\src\WebApp1"
```

## <a name="set-multiple-secrets"></a>여러 암호를 설정 합니다.

JSON에 파이프 하 여 보안의 일괄 처리를 설정할 수 있습니다는 `set` 명령입니다. 다음 예제에서는 *input.json* 파일의 내용으로 파이프 되는 `set` 명령입니다.

# <a name="windowstabwindows"></a>[Windows](#tab/windows)

명령 셸을 열고 다음 명령을 실행 합니다.

  ```console
  type .\input.json | dotnet user-secrets set
  ```

# <a name="macostabmacos"></a>[macOS](#tab/macos)

명령 셸을 열고 다음 명령을 실행 합니다.

  ```console
  cat ./input.json | dotnet user-secrets set
  ```

# <a name="linuxtablinux"></a>[Linux](#tab/linux)

명령 셸을 열고 다음 명령을 실행 합니다.

  ```console
  cat ./input.json | dotnet user-secrets set
  ```

---

## <a name="access-a-secret"></a>암호에 액세스

::: moniker range="<= aspnetcore-1.1"
[ASP.NET Core 구성 API](xref:fundamentals/configuration/index) 보안 관리자 암호에 대 한 액세스를 제공 합니다. 설치는 [Microsoft.Extensions.Configuration.UserSecrets](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.UserSecrets) NuGet 패키지 합니다.

사용자 암호 구성 소스를 호출 하 여 추가 [AddUserSecrets](/dotnet/api/microsoft.extensions.configuration.usersecretsconfigurationextensions.addusersecrets) 에 `Startup` 생성자:

[!code-csharp[](app-secrets/samples/1.x/UserSecrets/Startup.cs?name=snippet_StartupConstructor&highlight=5-8)]
::: moniker-end
::: moniker range=">= aspnetcore-2.0"
[ASP.NET Core 구성 API](xref:fundamentals/configuration/index) 보안 관리자 암호에 대 한 액세스를 제공 합니다. 프로젝트가.NET Framework를 대상으로 하는 경우 설치는 [Microsoft.Extensions.Configuration.UserSecrets](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.UserSecrets) NuGet 패키지 합니다.

ASP.NET Core 2.0 이상에서는 사용자 보안 구성 소스 자동으로 추가 됩니다 개발 모드에서 프로젝트를 호출할 때 [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) 미리 구성 된 기본값을 사용 하 여 호스트의 새 인스턴스를 초기화 합니다. `CreateDefaultBuilder` 호출 [AddUserSecrets](/dotnet/api/microsoft.extensions.configuration.usersecretsconfigurationextensions.addusersecrets) 때는 [EnvironmentName](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.environmentname) 은 [개발](/dotnet/api/microsoft.aspnetcore.hosting.environmentname.development):

[!code-csharp[](app-secrets/samples/2.x/UserSecrets/Program.cs?name=snippet_CreateWebHostBuilder&highlight=2)]

때 `CreateDefaultBuilder` 없는 사용자 암호 구성 소스를 호출 하 여 추가 호스트 생성 하는 동안 호출 [AddUserSecrets](/dotnet/api/microsoft.extensions.configuration.usersecretsconfigurationextensions.addusersecrets) 에 `Startup` 생성자:

[!code-csharp[](app-secrets/samples/1.x/UserSecrets/Startup.cs?name=snippet_StartupConstructor&highlight=5-8)]
::: moniker-end

사용자 암호를 통해 검색할 수 있습니다는 `Configuration` API:

::: moniker range="<= aspnetcore-1.1"
[!code-csharp[](app-secrets/samples/1.x/UserSecrets/Startup.cs?name=snippet_StartupClass&highlight=23)]
::: moniker-end
::: moniker range=">= aspnetcore-2.0"
[!code-csharp[](app-secrets/samples/2.x/UserSecrets/Startup.cs?name=snippet_StartupClass&highlight=14)]
::: moniker-end

## <a name="string-replacement-with-secrets"></a>암호와 문자열 대체

일반 텍스트에 암호를 저장 하는 것은 위험 합니다. 데이터베이스 연결 문자열에 저장 하는 예를 들어 *appsettings.json* 지정된 된 사용자에 대 한 암호를 포함 될 수 있습니다.

[!code-json[](app-secrets/samples/2.x/UserSecrets/appsettings-unsecure.json?highlight=3)]

암호로 암호를 저장 하는 보다 안전한 방법이입니다. 예를 들어:

```console
dotnet user-secrets set "DbPassword" "pass123"
```

암호를 대체할 *appsettings.json* 을 자리 표시자입니다. 다음 예에서 `{0}` 폼에 자리 표시자로 사용 되는 [복합 형식 문자열](/dotnet/standard/base-types/composite-formatting#composite-format-string)합니다.

[!code-json[](app-secrets/samples/2.x/UserSecrets/appsettings.json?highlight=3)]

연결 문자열을 완료 하려면 자리 표시자에 암호의 값을 삽입할 수 있습니다.

::: moniker range="<= aspnetcore-1.1"
[!code-csharp[](app-secrets/samples/1.x/UserSecrets/Startup2.cs?name=snippet_StartupClass&highlight=23-25)]
::: moniker-end
::: moniker range=">= aspnetcore-2.0"
[!code-csharp[](app-secrets/samples/2.x/UserSecrets/Startup2.cs?name=snippet_StartupClass&highlight=14-16)]
::: moniker-end

## <a name="list-the-secrets"></a>암호 나열

[!INCLUDE[secrets.json file](~/includes/app-secrets/secrets-json-file-and-text.md)]

디렉터리에서 다음 명령을 실행는 *.csproj* 파일이 있습니다.

```console
dotnet user-secrets list
```

다음과 같은 출력이 표시 됩니다.

```console
Movies:ServiceApiKey = 12345
Movies:ConnectionString = Server=(localdb)\mssqllocaldb;Database=Movie-1;Trusted_Connection=True;MultipleActiveResultSets=true
```

키 이름에 콜론 앞의 예제에서 내에서 개체 계층 구조를 나타냅니다 *secrets.json*합니다.

## <a name="remove-a-single-secret"></a>단일 암호를 제거 합니다.

[!INCLUDE[secrets.json file](~/includes/app-secrets/secrets-json-file-and-text.md)]

디렉터리에서 다음 명령을 실행는 *.csproj* 파일이 있습니다.

```console
dotnet user-secrets remove "Movies:ConnectionString"
```

응용 프로그램의 *secrets.json* 와 연결 된 키-값 쌍을 제거 하려면 파일을 수정한는 `MoviesConnectionString` 키:

```json
{
  "Movies": {
    "ServiceApiKey": "12345"
  }
}
```

실행 `dotnet user-secrets list` 다음 메시지가 표시 됩니다.

```console
Movies:ServiceApiKey = 12345
```

## <a name="remove-all-secrets"></a>모든 암호를 제거 합니다.

[!INCLUDE[secrets.json file](~/includes/app-secrets/secrets-json-file-and-text.md)]

디렉터리에서 다음 명령을 실행는 *.csproj* 파일이 있습니다.

```console
dotnet user-secrets clear
```

삭제 된 응용 프로그램에 대 한 모든 사용자 암호는 *secrets.json* 파일:

```json
{}
```

실행 `dotnet user-secrets list` 다음 메시지가 표시 됩니다.

```console
No secrets configured for this application.
```

## <a name="additional-resources"></a>추가 자료

* <xref:fundamentals/configuration/index>
* <xref:security/key-vault-configuration>
