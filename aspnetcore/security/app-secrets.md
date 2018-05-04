---
title: ASP.NET Core에서 개발의 앱 암호의 안전한 저장소
author: rick-anderson
description: 개발 중 보안 정보를 안전하게 저장하는 방법을 보여줍니다.
manager: wpickett
ms.author: riande
ms.date: 09/15/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/app-secrets
ms.openlocfilehash: 0a04f5762a35426f342b58b8b60288c66c057ae7
ms.sourcegitcommit: 5130b3034165f5cf49d829fe7475a84aa33d2693
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="safe-storage-of-app-secrets-in-development-in-aspnet-core"></a>ASP.NET Core에서 개발의 앱 암호의 안전한 저장소

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT), [김 Roth](https://github.com/danroth27), 및 [Scott Addie](https://scottaddie.com) 

이 문서에서는 개발 중 Secret Manager 도구를 이용해서 코드 외부에 보안 정보를 저장하는 방법을 보여줍니다. 무엇보다 중요한 점은 절대로 소스 코드에 암호나 기타 중요한 데이터를 저장하면 안 될 뿐만 아니라, 프로덕션 환경의 보안 정보를 개발 및 테스트 모드에서 사용해서는 안 된다는 것입니다. 대신, 이런 값들을 [구성](xref:fundamentals/configuration/index) 시스템을 이용해서 환경 변수로부터 읽거나, 또는 Secret Manager 도구를 이용해서 저장된 값으로부터 읽어올 수 있습니다. Secret Manager 도구는 민감한 보안 정보가 소스 제어에 체크인되지 않게 도와줍니다. 이 문서에서 설명하는 Secret Manager 도구를 이용해서 저장된 보안 정보는 [구성](xref:fundamentals/configuration/index) 시스템으로 읽을 수 있습니다

Secret Manager 도구는 개발 시에만 사용됩니다. Azure의 테스트 및 프로덕션 보안 데이터는 [Microsoft Azure Key Vault](https://azure.microsoft.com/services/key-vault/) 구성 공급자를 이용해서 보호할 수 있습니다. 보다 자세한 정보는 [Azure 키 자격 증명 모음 구성 공급자](xref:security/key-vault-configuration)를 참고하시기 바랍니다. 

## <a name="environment-variables"></a>환경 변수

코드나 로컬 구성 파일에 응용 프로그램의 보안 정보를 저장하지 않으려면 환경 변수에 보안 정보를 저장합니다.  `AddEnvironmentVariables` 를 호출하면 환경 변수에서 값을 읽도록 [구성](xref:fundamentals/configuration/index) 프레임워크를 설정합니다. 그런 다음, 환경 변수를 사용해서 기존에 지정된 모든 구성 소스의 구성 값을 재지정 할 수 있습니다. 

예를 들어, Visual Studio에서 개별 사용자 계정 옵션으로 새로운 ASP.NET Core 웹 응용 프로그램을 생성하면, 프로젝트의 *appsettings.json* 파일에 `DefaultConnection`이라는 키를 가진 기본 연결 문자열이 추가됩니다. 이 기본 연결 문자열은 사용자 모드에서 실행되고 암호를 요구하지 않는 LocalDB를 사용하도록 구성됩니다.  응용 프로그램을 테스트 서버나 프로덕션 서버에 배포할 때, `DefaultConnection` 키의 값을 테스트 또는 프로덕션 데이터베이스 서버의 연결 문자열이 지정된(민감한 자격 증명이 포함될 수 있는) 환경 변수 설정으로 재정의할 수 있습니다.

>[!WARNING]
> 일반적으로 환경 변수는 평문으로 저장되며 암호화되지 않습니다. 컴퓨터나 프로세스가 손상될 경우, 신뢰할 수 없는 사용자가 환경 변수에 접근할 수 있습니다. 따라서 여전히 사용자의 보안 정보 유출을 방지하기 위한 추가적인 방안이 필요할 수도 있습니다.

## <a name="secret-manager"></a>Secret Manager

Secret Manager 도구는 개발 작업에 필요한 민감한 데이터를 프로젝트의 디렉터리 구조 외부에 저장합니다. 암호 관리자 도구는 개발 하는 동안.NET Core 프로젝트에 대 한 기밀 정보를 사용할 수 있는 프로젝트 도구입니다. Secret Manager 도구를 사용하면 응용 프로그램의 보안 정보를 특정 프로젝트와 연결하고 이를 여러 프로젝트에서 공유할 수 있습니다.

>[!WARNING]
> 암호 관리자 도구 저장 된 암호를 암호화 하지 않습니다 하 고 신뢰할 수 있는 저장소로 처리 하지 않아야 합니다. 개발 용도로입니다. 키와 값은 사용자 프로필 디렉터리에 위치한 JSON 구성 파일에 저장됩니다. 

## <a name="installing-the-secret-manager-tool"></a>Secret Manager 도구 설치하기

#### <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio/)
마우스 오른쪽 버튼으로 솔루션 탐색기에서 프로젝트를 클릭한 다음, 컨텍스트 메뉴에서 **\<project_name\>.csproj 편집 (Edit \<project_name\>.csproj)** 을 선택합니다. 다음에 강조 표시된 줄을 *.csproj* 파일에 추가하고 저장하면 관련된 NuGet 패키지가 복원됩니다.

[!code-xml[](app-secrets/sample/UserSecrets/UserSecrets-before.csproj?highlight=10)]

다시 마우스 오른쪽 버튼으로 솔루션 탐색기에서 프로젝트를 클릭한 다음, 컨텍스트 메뉴에서 **사용자 암호 관리 (Manage User Secrets)** 를 선택합니다.  그러면 다음 예제에 강조 표시된 것처럼 *.csproj* 파일의 `PropertyGroup` 노드 하위에 새로운 `UserSecretsId` 노드가 추가됩니다.

[!code-xml[](app-secrets/sample/UserSecrets/UserSecrets-after.csproj?highlight=4)]

수정된 *.csproj* 파일을 저장하면 텍스트 편집기에서 `secrets.json` 파일이 열립니다. `secrets.json` 파일의 내용을 다음 코드로 대체합니다.

```json
{
    "MySecret": "ValueOfMySecret"
}
```

#### <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code/)
추가 `Microsoft.Extensions.SecretManager.Tools` 에 *.csproj* 파일을 실행 [dotnet 복원](/dotnet/core/tools/dotnet-restore)합니다. 명령줄에서 동일한 단계를 사용해서 Secret Manager 도구를 설치할 수 있습니다. 

[!code-xml[](app-secrets/sample/UserSecrets/UserSecrets-before.csproj?highlight=10)]

다음 명령을 실행해서 Secret Manager 도구를 테스트합니다.

```console
dotnet user-secrets -h
```

그러면 Secret Manager 도구의 사용법, 옵션 및 명령 도움말이 표시됩니다.

> [!NOTE]
> 이렇게 *.csproj* 파일의 `DotNetCliToolReference` 노드에 정의된 도구를 실행하려면 *.csproj* 파일과 동일한 디렉터리에 위치해 있어야 합니다. 

Secret Manager 도구는 사용자 프로필에 저장된 프로젝트별 구성 설정을 대상으로 동작합니다. 사용자 보안 정보를 사용하려면 프로젝트의 *.csproj* 파일에 `UserSecretsId` 값을 지정해야 합니다.  `UserSecretsId` 값은 선택적이긴 하지만 일반적으로 프로젝트에 고유합니다. 개발자는 대부분 `UserSecretsId` 값에 GUID를 생성해서 지정합니다. 

프로젝트의 *.csproj* 파일에 `UserSecretsId` 를 추가합니다.

[!code-xml[](app-secrets/sample/UserSecrets/UserSecrets-after.csproj?highlight=4)]

Secret Manager 도구를 사용해서 보안 정보를 설정합니다. 예를 들어 프로젝트 디렉터리의 명령 창에 다음과 같이 입력합니다.

```console
dotnet user-secrets set MySecret ValueOfMySecret
```

다른 디렉터리에서 Secret Manager 도구를 실행할 수도 있지만, `--project` 옵션을 사용해서 *.csproj* 파일의 경로를 전달해야 합니다.

```console
dotnet user-secrets set MySecret ValueOfMySecret --project c:\work\WebApp1\src\webapp1
```

Secret Manager 도구를 사용해서 응용 프로그램의 보안 정보의 목록을 나열하거나 제거하고 초기화시킬 수도 있습니다. 

* * *
## <a name="accessing-user-secrets-via-configuration"></a>구성을 통해서 사용자 보안 정보에 접근하기

구성 시스템을 통해서 Secret Manager 도구의 사용자 보안 정보에 접근할 수 있습니다. 추가 `Microsoft.Extensions.Configuration.UserSecrets` 패키지 및 실행 [dotnet 복원](/dotnet/core/tools/dotnet-restore)합니다.

그리고 `Startup`의 생성자에 사용자 보안 정보 구성 소스를 추가합니다.

[!code-csharp[](app-secrets/sample/UserSecrets/Startup.cs?highlight=16-19)]

그러면 구성 API를 통해서 사용자 보안 정보에 접근할 수 있습니다.

[!code-csharp[](app-secrets/sample/UserSecrets/Startup.cs?highlight=26-29)]

## <a name="how-the-secret-manager-tool-works"></a>Secret Manager 도구의 동작 방식

Secret Manager 도구는 값이 저장되는 위치 및 방법 같은 구현에 관한 세부적인 내용을 추상화합니다. 이런 세부적인 내용을 모르더라도 Secret Manager 도구를 사용하는 데는 아무런 지장이 없습니다.  현재 버전에서는 사용자 프로필 디렉터리의 [JSON](http://json.org/) 구성 파일에 값이 저장됩니다.

* Windows: `%APPDATA%\microsoft\UserSecrets\<userSecretsId>\secrets.json`

* Linux: `~/.microsoft/usersecrets/<userSecretsId>/secrets.json`

* macOS: `~/.microsoft/usersecrets/<userSecretsId>/secrets.json`

여기서 `userSecretsId` 의 값은 *.csproj* 파일에 지정된 값입니다. 

이러한 구현 정보 변경 될 수 있으므로 위치나 암호 관리자 도구와 함께 저장 된 데이터의 형식에 따라 달라 지 코드를 작성 하지 않아야 합니다. 예를 들어, 지금은 보안 정보가 암호화되지 *않지만* 나중에는 암호화될 수도 있습니다.

## <a name="additional-resources"></a>추가 자료

* [구성](xref:fundamentals/configuration/index)
