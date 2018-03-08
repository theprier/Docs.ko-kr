---
title: "ASP.NET Core 개발 중 앱의 보안 정보를 안전하게 저장하기"
author: rick-anderson
description: "개발 중 보안 정보를 안전하게 저장하는 방법을 보여줍니다."
manager: wpickett
ms.author: riande
ms.date: 09/15/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/app-secrets
ms.openlocfilehash: 489c53c066af87e02e43ab0b42b0712d80d5ee5a
ms.sourcegitcommit: 7ac15eaae20b6d70e65f3650af050a7880115cbf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2018
---
# <a name="safe-storage-of-app-secrets-during-development-in-aspnet-core"></a>ASP.NET Core 개발 중 앱의 보안 정보를 안전하게 저장하기

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT), [김 Roth](https://github.com/danroth27), 및 [Scott Addie](https://scottaddie.com) 

이 문서에서는 개발 중 Secret Manager 도구를 이용해서 코드 외부에 보안 정보를 저장하는 방법을 보여줍니다. 무엇보다 중요한 점은 절대로 소스 코드에 암호나 기타 중요한 데이터를 저장하면 안 될 뿐만 아니라, 프로덕션 환경의 보안 정보를 개발 및 테스트 모드에서 사용해서는 안 된다는 것입니다 대신, 이런 값들을 [구성](xref:fundamentals/configuration/index) 시스템을 이용해서 환경 변수로부터 읽거나, 또는 Secret Manager 도구를 이용해서 저장된 값으로부터 읽어올 수 있습니다. 암호 관리자 도구에서 소스 제어에 체크 인 되 고 중요 한 데이터를 방지할 수 있습니다. 이 문서에서 설명하는 Secret Manager 도구를 이용해서 저장된 보안 정보는 [구성](xref:fundamentals/configuration/index) 시스템으로 읽을 수 있습니다

Secret Manager 도구는 개발 시에만 사용됩니다. Azure의 테스트 및 프로덕션 보안 데이터는 [Microsoft Azure Key Vault](https://azure.microsoft.com/services/key-vault/) 구성 공급자를 이용해서 보호할 수 있습니다. 보다 자세한 정보는 [Azure 키 자격 증명 모음 구성 공급자](https://docs.microsoft.com/aspnet/core/security/key-vault-configuration)를 참고하시기 바랍니다. 

## <a name="environment-variables"></a>환경 변수

코드나 로컬 구성 파일에 응용 프로그램의 보안 정보를 저장하지 않으려면 환경 변수에 보안 정보를 저장합니다.  `AddEnvironmentVariables` 를 호출하면 환경 변수에서 값을 읽도록 [구성](xref:fundamentals/configuration/index) 프레임워크를 설정합니다. 그런 다음, 환경 변수를 사용해서 기존에 지정된 모든 구성 소스의 구성 값을 재지정 할 수 있습니다. 

예를 들어, Visual Studio에서 개별 사용자 계정 옵션으로 새로운 ASP.NET Core 웹 응용 프로그램을 생성하면, 프로젝트의 *appsettings.json* 파일에 `DefaultConnection`이라는 키를 가진 기본 연결 문자열이 추가됩니다. 이 기본 연결 문자열은 사용자 모드에서 실행되고 암호를 요구하지 않는 LocalDB를 사용하도록 구성됩니다.  응용 프로그램을 테스트 서버나 프로덕션 서버에 배포할 때, `DefaultConnection` 키의 값을 테스트 또는 프로덕션 데이터베이스 서버의 연결 문자열이 지정된(민감한 자격 증명이 포함될 수 있는) 환경 변수 설정으로 재정의할 수 있습니다.

>[!WARNING]
> 환경 변수는 일반적으로 일반 텍스트로 저장 되며 암호화 되지 않습니다. 컴퓨터 또는 프로세스가 손상 된 환경 변수 신뢰할 수 없는 당사자가 액세스할 수 있습니다. 여전히 사용자 비밀 정보를 공개 하지 않도록 추가 조치가 필요할 수 있습니다.

## <a name="secret-manager"></a>암호 관리자

암호 관리자 도구는 프로젝트 트리 외부의 개발 작업에 대 한 중요 한 데이터를 저장합니다. 암호 관리자 도구는에 대 한 기밀 정보를 사용할 수 있는 프로젝트 도구는 [.NET Core](https://www.microsoft.com/net/core) 개발 중 프로젝트. 암호 관리자 도구를 사용 특정 프로젝트와 앱 암호를 연결 하 고 여러 프로젝트 간에 공유할 수 있습니다.

>[!WARNING]
> 암호 관리자 도구 저장 된 암호를 암호화 하지 않습니다 하 고 신뢰할 수 있는 저장소로 처리 하지 않아야 합니다. 개발 용도로입니다. 키와 값은 사용자 프로필 디렉터리에는 JSON 구성 파일에 저장 됩니다.

## <a name="installing-the-secret-manager-tool"></a>암호 관리자 도구를 설치합니다.

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **편집 \<project_name\>.csproj** 상황에 맞는 메뉴입니다. 강조 표시 된 줄을 추가 *.csproj* 파일과 연결 된 NuGet 패키지를 복원 하려면 저장:

[!code-xml[](app-secrets/sample/UserSecrets/UserSecrets-before.csproj?highlight=10)]

솔루션 탐색기에서 프로젝트를 다시 마우스 오른쪽 단추로 클릭 하 고 선택 **관리 사용자의 비밀** 상황에 맞는 메뉴입니다. 이 제스처를 새로 추가 `UserSecretsId` 내에서 노드는 `PropertyGroup` 의 *.csproj* 다음 샘플에 강조 표시 된 대로 파일:

[!code-xml[](app-secrets/sample/UserSecrets/UserSecrets-after.csproj?highlight=4)]

수정 된 저장 *.csproj* 파일도 열립니다는 `secrets.json` 파일 텍스트 편집기에서. 내용을 대체는 `secrets.json` 를 다음 코드로 파일:

```json
{
    "MySecret": "ValueOfMySecret"
}
```

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code)

추가 `Microsoft.Extensions.SecretManager.Tools` 에 *.csproj* 파일을 실행 [dotnet 복원](/dotnet/core/tools/dotnet-restore)합니다. 명령줄을 사용 하 여 암호 관리자 도구를 설치 하려면 동일한 단계를 사용할 수 있습니다.

[!code-xml[](app-secrets/sample/UserSecrets/UserSecrets-before.csproj?highlight=10)]

다음 명령을 실행 하 여 암호 관리자 도구를 테스트 합니다.

```console
dotnet user-secrets -h
```

암호 관리자 도구는 사용, 옵션 및 명령 도움말 표시 됩니다.

> [!NOTE]
> 와 같은 디렉터리에 있어야는 *.csproj* 파일에 정의 된 도구를 실행 하는 *.csproj* 파일의 `DotNetCliToolReference` 노드.

암호 관리자 도구는 사용자 프로필에 저장 되어 있는 프로젝트 관련 구성 설정에서 작동 합니다. 사용자 암호를 사용 하려면 프로젝트 지정 해야 합니다는 `UserSecretsId` 에서 값을 해당 *.csproj* 파일입니다. 값 `UserSecretsId` 은 선택적 요소 이지만 프로젝트에 일반적으로 고유 합니다. 에 대 한 GUID를 일반적으로 생성 하는 개발자는 `UserSecretsId`합니다.

추가 `UserSecretsId` 에서 프로젝트에 대 한는 *.csproj* 파일:

[!code-xml[](app-secrets/sample/UserSecrets/UserSecrets-after.csproj?highlight=4)]

암호 관리자 도구를 사용 하 여 암호를 설정할 수 있습니다. 예를 들어 프로젝트 디렉터리에서 명령 창에서 다음을 입력 합니다.

```console
dotnet user-secrets set MySecret ValueOfMySecret
```

다른 디렉터리에서 암호 관리자 도구를 실행할 수 있지만 사용 해야 합니다는 `--project` 옵션에 대 한 경로 전달 하는 *.csproj* 파일:
 
```console
dotnet user-secrets set MySecret ValueOfMySecret --project c:\work\WebApp1\src\webapp1
```

또한 나열, 제거 및 앱 암호를 지울 수는 암호 관리자 도구를 사용할 수 있습니다.

-----

## <a name="accessing-user-secrets-via-configuration"></a>구성을 통해 사용자의 비밀 정보에 액세스

구성 시스템을 통해 보안 관리자 암호에 액세스 합니다. 추가 `Microsoft.Extensions.Configuration.UserSecrets` 패키지 및 실행 [dotnet 복원](/dotnet/core/tools/dotnet-restore)합니다.

사용자 암호 구성 소스를 추가 `Startup` 메서드:

[!code-csharp[](app-secrets/sample/UserSecrets/Startup.cs?highlight=16-19)]

구성 API 통해 사용자의 비밀을 액세스할 수 있습니다.

[!code-csharp[](app-secrets/sample/UserSecrets/Startup.cs?highlight=26-29)]

## <a name="how-the-secret-manager-tool-works"></a>암호 관리자 도구 작동 방식

암호 관리자 도구 값을 저장 하는 위치와 방법을 같은 구현 세부 정보를 추상화 합니다. 이러한 구현 정보를 알 필요 없이 도구를 사용할 수 있습니다. 현재 버전의 값에 저장 됩니다는 [JSON](http://json.org/) 사용자 프로필 디렉터리에 구성 파일:

* Windows: `%APPDATA%\microsoft\UserSecrets\<userSecretsId>\secrets.json`

* Linux: `~/.microsoft/usersecrets/<userSecretsId>/secrets.json`

* Mac: `~/.microsoft/usersecrets/<userSecretsId>/secrets.json`

값 `userSecretsId` 에 지정 된 값에서 가져온 *.csproj* 파일입니다.

이러한 구현 정보 변경 될 수 있으므로 위치나 암호 관리자 도구와 함께 저장 된 데이터의 형식에 따라 달라 지 코드를 작성 하지 않아야 합니다. 예를 들어 비밀 값은 현재 *하지* 오늘 암호화 되지만 언젠가 수 있습니다.

## <a name="additional-resources"></a>추가 리소스

* [구성](xref:fundamentals/configuration/index)
