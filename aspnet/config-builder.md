---
uid: config-builder
title: ASP.NET에 대 한 구성 작성기
author: rick-anderson
description: 외부 소스의 web.config 값 이외의 원본에서 구성 데이터를 가져오는 방법에 알아봅니다.
ms.author: riande
ms.date: 10/29/2018
ms.technology: aspnet
msc.type: content
ms.openlocfilehash: d5a3916c3df9778d14be80342bafbc3456a69a03
ms.sourcegitcommit: f2d14a7518d6ee51aca9333818ac1276e7b5ecef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50134537"
---
# <a name="configuration-builders-for-aspnet"></a>ASP.NET에 대 한 구성 작성기

하 여 [Stephen Molloy](https://github.com/StephenMolloy) 고 [Rick Anderson](https://twitter.com/RickAndMSFT)

구성 작성기 외부 원본에서 구성 값을 가져오려면 ASP.NET 앱에 대 한 현대적이 고 민첩 한 메커니즘을 제공 합니다.

구성 작성기:

* 이상 및.NET Framework 4.7.1에서에서 제공 됩니다.
* 구성 값을 읽기 위한 유연한 메커니즘을 제공 합니다.
* 컨테이너로 이동 하 고 클라우드 포커스가 있는 환경 일부 앱의 기본 요구를 해결 합니다.
* 사용할 수 있습니다 (예: Azure Key Vault 및 환경 변수) 이전에 사용할 수 없는 원본의 그리는 방식으로 구성 데이터에 대 한 보호를 개선 하기 위해.NET 구성 시스템에서.

## <a name="keyvalue-configuration-builders"></a>키/값 구성 작성기

구성 작성기에 의해 처리 될 수 있는 일반적인 시나리오는 키/값 패턴을 따르는 구성 섹션에 대 한 기본 키/값 대체 메커니즘을 제공 하는 것입니다. .NET Framework에 대 한 개념이 ConfigurationBuilders 특정 구성 섹션 또는 패턴으로 제한 됩니다. 그러나 구성 작성기에 많은 `Microsoft.Configuration.ConfigurationBuilders` ([github](https://github.com/aspnet/MicrosoftConfigurationBuilders)), [NuGet](https://www.nuget.org/packages?q=Microsoft.Configuration.ConfigurationBuilders) 키/쌍 패턴 내에서 작동 합니다.

## <a name="keyvalue-configuration-builders-settings"></a>키/값 구성 작성기 설정

다음 설정의 모든 키/값 구성 작성기를 적용할 `Microsoft.Configuration.ConfigurationBuilders`합니다.

### <a name="mode"></a>모드

키/값 정보가 외부 원본 구성 시스템의 선택 된 키/값 요소를 채우는 데 사용 하는 구성 작성기입니다. 특히 합니다 `<appSettings/>` 고 `<connectionStrings/>` 섹션 구성 작성기에서 특별 한 처리를 수신 합니다. 작성기는 세 가지 모드로 작동합니다.

* `Strict` -기본 모드입니다. 이 모드에서는 구성 작성기를 잘 알려진 키/값 중심 구성 섹션에 대해서만 작동 합니다. `Strict` 모드 섹션에서 각 키를 열거합니다. 일치 하는 키가 없으면 외부 원본:

   * 구성 작성기는 외부 원본에서 값을 사용 하 여 결과 구성 섹션에서 값을 대체합니다.
* `Greedy` -이 모드는 밀접 한 관련이 `Strict` 모드입니다. 대신 원래 구성에 이미 존재 하는 키를 제한 합니다.

  * 구성 작성기 결과 구성 섹션에는 외부 원본에서 모든 키/값 쌍을 추가 합니다.

* `Expand` -구성 섹션 개체를 구문 분석 전에 원시 XML에서 작동 합니다. 이 문자열에서 토큰의 확장으로 간주 될 수 있습니다. 패턴과 일치 하는 원시 XML 문자열의 일부가 `${token}` 토큰 확장에 대 한 후보입니다. 해당 값이 없는 외부 소스에 없으면 토큰 변경 되지 않습니다. 이 모드는 작성기에 제한 되지 않습니다.는 `<appSettings/>` 및 `<connectionStrings/>` 섹션입니다.

다음과 같은 태그가 *web.config* 사용 하도록 설정 된 [EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/) 에서 `Strict` 모드:

[!code-xml[Main](config-builder/MyConfigBuilders/WebDefault.config?name=snippet)]

다음 코드는 읽기를 `<appSettings/>` 하 고 `<connectionStrings/>` 앞의 *web.config* 파일:

[!code-csharp[Main](config-builder/MyConfigBuilders/About.aspx.cs)]

위의 코드 속성 값을 설정 하 고:

* 값을 *web.config* 키 환경 변수에 설정 되어 있지 않으면 파일입니다.
* 환경 값 경우 변수를 설정 합니다.

예를 들어 `ServiceID` 포함 됩니다.

* "ServiceID" value web.config의 경우 환경 변수 `ServiceID` 설정 되지 않았습니다.
* 값을 `ServiceID` 환경 변수인 경우 설정 합니다.

다음 이미지는 `<appSettings/>` 앞의 키/값 *web.config* 환경 편집기에서 파일 설정:

![환경 편집기](config-builder/static/env.png)

참고: 종료 하 고 환경 변수에서 변경 내용을 확인 하려면 Visual Studio를 다시 시작 해야 할 수 있습니다.

### <a name="prefix-handling"></a>접두사 처리

때문에 키 접두사 설정 키를 간소화할 수 있습니다.

* .NET Framework 구성이 복잡 하 고 중첩 되었습니다.
* 외부 키/값 소스는 일반적으로 기본 및 특성상 평면입니다. 예를 들어, 환경 변수 중첩 되지 않은 합니다.

다음 방법 중 하나를 사용 하 여 둘 다를 삽입할 `<appSettings/>` 고 `<connectionStrings/>` 환경 변수를 통해 구성에:

* 사용 하 여 합니다 `EnvironmentConfigBuilder` 기본에서 `Strict` 모드 및 구성 파일에서 적절 한 키 이름입니다. 이전 코드와 태그에서는이 접근 방식을 사용 합니다. 이렇게 할 수 있습니다 **되지** 키 모두에 동일 하 게 명명 된 `<appSettings/>` 및 `<connectionStrings/>`합니다.
* 사용 하 여 두 `EnvironmentConfigBuilder`에서 s `Greedy` 고유한 접두사를 사용 하 여 모드 및 `stripPrefix`. 이 방법을 사용 하 여 앱 읽어보세요 `<appSettings/>` 및 `<connectionStrings/>` 구성 파일을 업데이트 하지 않고도 합니다. 다음 섹션인 [stripPrefix](#stripprefix),이 작업을 수행 하는 방법을 보여 줍니다.
* 사용 하 여 두 `EnvironmentConfigBuilder`의 `Greedy` 고유한 접두사를 사용 하 여 모드입니다. 이 방법을 사용 하 여 키 이름을 접두사로 달라 야 하는 대로 중복 키 이름 수는 없습니다.  예를 들어:

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefix.config?name=snippet&highlight=11-99)]

위의 태그를 사용 하 여 동일한 기본 키/값 소스를 채우는 두 개의 서로 다른 섹션에 대 한 구성을 사용할 수 있습니다.

다음 이미지는 `<appSettings/>` 하 고 `<connectionStrings/>` 앞에서 키/값 *web.config* 환경 편집기에서 파일 설정:

![환경 편집기](config-builder/static/prefix.png)

다음 코드는 읽기를 `<appSettings/>` 하 고 `<connectionStrings/>` 앞에 포함 된 키/값 *web.config* 파일:

[!code-csharp[Main](config-builder/MyConfigBuilders/Contact.aspx.cs?name=snippet)]

위의 코드 속성 값을 설정 하 고:

* 값을 *web.config* 키 환경 변수에 설정 되어 있지 않으면 파일입니다.
* 환경 값 경우 변수를 설정 합니다.

예를 들어 이전 사용 하 여 *web.config* 파일인 이전 환경 편집기 이미지를 이전 코드를 다음 값의 키/값 설정 됩니다.

|  Key              | 값 |
| ----------------- | ------------ |
|     AppSetting_ServiceID           | 환경 변수에서 AppSetting_ServiceID|
|    AppSetting_default            | Env AppSetting_default 값 |
|       ConnStr_default         | Env에서 ConnStr_default val|

### <a name="stripprefix"></a>stripPrefix

`stripPrefix`: 부울, 기본값은 `false`합니다. 

이전 XML 태그를 사용 하는 앱 설정에서 연결 문자열을 구분 하지만에서 모든 키가 필요 합니다 *web.config* 지정된 된 접두사를 사용 하는 파일입니다. 예를 들어 접두사 `AppSetting` 에 추가 해야 합니다 `ServiceID` 키 ("AppSetting_ServiceID"). 사용 하 여 `stripPrefix`, 접두사에서 사용 되지 않습니다 합니다 *web.config* 파일입니다. 구성 작성기 소스 (예를 들어, 환경에서.)에 붙여야 합니다. 대부분의 개발자가 사용 하는 것으로 예상 `stripPrefix`합니다.

응용 프로그램은 일반적으로 접두사를 제거합니다. 다음 *web.config* 접두사를 제거 합니다.

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefixStrip.config?name=snippet&highlight=14,19)]

앞의 *web.config* 파일을 `default` 키가 둘 다에 `<appSettings/>` 및 `<connectionStrings/>`합니다.

다음 이미지는 `<appSettings/>` 하 고 `<connectionStrings/>` 앞에서 키/값 *web.config* 환경 편집기에서 파일 설정:

![환경 편집기](config-builder/static/prefix.png)

다음 코드는 읽기를 `<appSettings/>` 하 고 `<connectionStrings/>` 앞에 포함 된 키/값 *web.config* 파일:

[!code-csharp[Main](config-builder/MyConfigBuilders/About2.aspx.cs?name=snippet)]

위의 코드 속성 값을 설정 하 고:

* 값을 *web.config* 키 환경 변수에 설정 되어 있지 않으면 파일입니다.
* 환경 값 경우 변수를 설정 합니다.

예를 들어 이전 사용 하 여 *web.config* 파일인 이전 환경 편집기 이미지를 이전 코드를 다음 값의 키/값 설정 됩니다.

|  Key              | 값 |
| ----------------- | ------------ |
|     ServiceID           | 환경 변수에서 AppSetting_ServiceID|
|    default            | Env AppSetting_default 값 |
|    default         | Env에서 ConnStr_default val|

### <a name="tokenpattern"></a>tokenPattern

`tokenPattern`: String, 기본값은 `@"\$\{(\w+)\}"`

합니다 `Expand` 처럼 보이는 토큰에 대 한 원시 XML을 검색 하는 동작 작성기 중 `${token}`합니다. 기본 정규식을 사용 하 여 수행 됩니다 검색 `@"\$\{(\w+)\}"`합니다. 일치 하는 문자 집합이 `\w` XML과 많은 구성 소스 허용 보다 더 엄격 합니다. 사용 하 여 `tokenPattern` 때 보다 이상의 문자 `@"\$\{(\w+)\}"` 토큰 이름에 필요 합니다.

`tokenPattern`: 문자열:

* 개발자를 토큰 일치에 사용 되는 정규식을 변경할 수 있습니다.
* 잘 구성 된, 위험한 regex 인지 유효성을 검사 하지 이루어집니다.
* 캡처 그룹을 포함 해야 합니다. 전체 정규식에는 전체 토큰을 일치 해야 합니다. 첫 번째 캡처 구성 소스에서 찾을 토큰 이름 이어야 합니다.

## <a name="configuration-builders-in-microsoftconfigurationconfigurationbuilders"></a>구성 작성기 Microsoft.Configuration.ConfigurationBuilders에서

### <a name="environmentconfigbuilder"></a>EnvironmentConfigBuilder

```xml
<add name="Environment"
    [mode|prefix|stripPrefix|tokenPattern] 
    type="Microsoft.Configuration.ConfigurationBuilders.EnvironmentConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Environment" />
```

합니다 [EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/):

* 가장 구성 작성기의 간단 합니다.
* 환경에서 값을 읽습니다.
* 추가 구성 옵션이 없습니다.
* `name` 특성 값은 임의입니다.

**참고:** Windows 컨테이너 환경에서 런타임 시 설정 된 변수 EntryPoint 프로세스 환경에 삽입만 됩니다. 서비스로 실행 되는 앱 또는 컨테이너의 메커니즘을 통해 삽입 된이 고, 그렇지 않으면 이러한 변수를 진입점이 아닌 프로세스를 선택 하지 않습니다. 에 대 한 [IIS](https://github.com/Microsoft/iis-docker/pull/41)/[ASP.NET](https://github.com/Microsoft/aspnet-docker)-현재 버전의 컨테이너 기반 [ServiceMonitor.exe](https://github.com/Microsoft/iis-docker/pull/41) 이 처리 합니다 *DefaultAppPool* 만 합니다. 다른 Windows 기반 컨테이너 변형 진입점이 아닌 프로세스에 대 한 자신의 주입 메커니즘을 개발 해야 합니다.

### <a name="usersecretsconfigbuilder"></a>UserSecretsConfigBuilder

> [!WARNING]
> 암호 저장, 중요 한 연결 문자열 또는 기타 중요 한 데이터 소스 코드에서 하지 않습니다. 프로덕션 비밀을 사용 하지 않아야 개발 또는 테스트에 대 한 합니다.

```xml
<add name="UserSecrets"
    [mode|prefix|stripPrefix|tokenPattern]
    (userSecretsId="{secret string, typically a GUID}" | userSecretsFile="~\secrets.file")
    [optional="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.UserSecretsConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.UserSecrets" />
```

이 구성 작성기는 유사한 기능을 제공 [ASP.NET Core 암호 관리자](/aspnet/core/security/app-secrets)합니다.

합니다 [UserSecretsConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.UserSecrets/) .NET Framework 프로젝트에서 사용할 수 있지만 암호 파일을 지정 해야 합니다. 정의할 수 있습니다는 `UserSecretsId` 프로젝트의 속성이 파일을 읽기 위한 올바른 위치에 원시 비밀 파일을 만듭니다. 외부 프로젝트 종속성을 유지 하려면 비밀 파일에는 서식이 지정 된 XML입니다. XML 서식 지정는 구현 세부 정보 이며 형식 방법에 의존 해야 합니다. 공유 하는 경우는 *secrets.json* .NET Core 프로젝트를 사용 하 여 파일을 사용 하는 것이 좋습니다는 [SimpleJsonConfigBuilder](#simplejsonconfig)합니다. `SimpleJsonConfigBuilder` .NET Core도 고려해 야 변경 될 수 있습니다 구현 세부 정보에 대 한 서식을 지정 합니다.

구성에 대 한 특성 `UserSecretsConfigBuilder`:

* `userSecretsId` -이것이 XML 비밀 파일을 식별 하기 위한 기본 방법입니다. .NET Core를 사용 하 여 비슷하게 작동을 `UserSecretsId` 프로젝트 속성을이 식별자를 저장 합니다. 문자열은 고유 해야 합니다., GUID 여야 필요 하지 않습니다. 이 특성을 사용 합니다 `UserSecretsConfigBuilder` 잘 알려진 로컬 위치에서 (`%APPDATA%\Microsoft\UserSecrets\<UserSecrets Id>\secrets.xml`)이이 식별자에 속하는 비밀 파일에 대 한 합니다.
* `userSecretsFile` 암호를 포함 하는 파일 지정-선택적 특성입니다. `~` 응용 프로그램 루트를 참조 하는 시작 시 문자를 사용할 수 있습니다. 이 특성 중 하나 또는 `userSecretsId` 특성이 필요 합니다. 둘 다 지정 `userSecretsFile` 우선적으로 적용 합니다.
* `optional`: 부울 기본값 `true` -비밀 파일을 찾을 수 없는 경우 예외를 방지 합니다. 
* `name` 특성 값은 임의입니다.

비밀 파일을 다음 형식으로 되어 있습니다.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<root>
  <secrets ver="1.0">
    <secret name="secret key name" value="secret value" />
  </secrets>
</root>
```

### <a name="azurekeyvaultconfigbuilder"></a>AzureKeyVaultConfigBuilder

```xml
<add name="AzureKeyVault"
    [mode|prefix|stripPrefix|tokenPattern]
    (vaultName="MyVaultName" |
     uri="https:/MyVaultName.vault.azure.net")
    [connectionString="connection string"]
    [version="secrets version"]
    [preloadSecretNames="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.AzureKeyVaultConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Azure" />
```

합니다 [AzureKeyVaultConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Azure/) 에 저장 된 값을 읽고 합니다 [Azure Key Vault](/azure/key-vault/key-vault-whatis)합니다.

`vaultName` (자격 증명 모음의 이름) 또는 자격 증명 모음 URI 필요 합니다. 다른 특성에 연결할 자격 증명 모음에 대 한 제어를 허용 하지만 응용 프로그램을 사용 하는 환경에서 실행 하지 않는 경우에 필요는 `Microsoft.Azure.Services.AppAuthentication`합니다. Azure 서비스 인증 라이브러리가 자동으로 실행 환경에서 연결 정보를 가능 하면 선택 하는 데 사용 됩니다. 자동으로 재정의할 수 있습니다 연결 정보의 연결 문자열을 제공 하 여 선택 합니다.

* `vaultName` -필요한 경우 `uri` 에서 제공 되지 않았습니다. 키/값 쌍을 읽어 올 Azure 구독에서 자격 증명 모음의 이름을 지정 합니다.
* `connectionString` 사용할 연결 문자열- [AzureServiceTokenProvider](https://docs.microsoft.com/en-us/azure/key-vault/service-to-service-authentication#connection-string-support)
* `uri` -지정 된 다른 Key Vault 공급자에 연결 합니다. `uri` 값입니다. 지정 하지 않으면 Azure (`vaultName`) 자격 증명 모음 공급자입니다.
* `version` -Azure Key Vault 비밀에 대 한 버전 관리 기능을 제공합니다. 경우 `version` 를 지정 하면 작성기만이 버전을 일치 하는 비밀을 검색 합니다.
* `preloadSecretNames` -기본적으로이 작성기 쿼리 **모든** 초기화 될 때 키를 key vault의 이름입니다. 모든 키 값 읽기를 방지 하려면이 특성을 설정 `false`합니다. 이 값을 설정 `false` 한 번에 한 암호를 읽습니다. 한 번에 하나씩 유용할 수 있습니다 자격 증명 모음 "Get" 액세스를 허용 하지만 하지 "목록"에 액세스 하는 경우 비밀을 읽는 중입니다. **참고:** 사용 하는 경우 `Greedy` 모드 `preloadSecretNames` 있어야 `true` (기본값입니다.)

### <a name="keyperfileconfigbuilder"></a>KeyPerFileConfigBuilder

```xml
<add name="KeyPerFile"
    [mode|prefix|stripPrefix|tokenPattern]
    (directoryPath="PathToSourceDirectory")
    [ignorePrefix="ignore."]
    [keyDelimiter=":"]
    [optional="false"]
    type="Microsoft.Configuration.ConfigurationBuilders.KeyPerFileConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.KeyPerFile" />
```

[KeyPerFileConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.KeyPerFile/) 값의 원본으로 디렉터리의 파일을 사용 하는 기본 구성 작성기를 됩니다. 파일의 이름을 키가 고 내용이 값입니다. 이 구성 작성기 오케스트레이션된 컨테이너 환경에서 실행 하는 경우 유용할 수 있습니다. Docker Swarm 및 Kubernetes를 제공 하는 같은 시스템 `secrets` 해당 오케스트레이션된 windows 컨테이너로이 키 파일 방식입니다.

특성 세부 정보:

* `directoryPath` - 필수입니다. 값에 대 한 확인에 대 한 경로 지정 합니다. 암호에 저장 되는 Windows 용 docker를 *C:\ProgramData\Docker\secrets* 기본적으로 디렉터리입니다.
* `ignorePrefix` -이 접두사로 시작 하는 파일 제외 됩니다. 기본값은 "무시 합니다."입니다.
* `keyDelimiter` -기본값은 `null`합니다. 를 지정 하는 경우 구성 작성기를 트래버스 디렉터리의 여러 수준을 구분이 기호와 함께 키 이름을 작성 합니다. 이 값이 `null`, 디렉터리의 최상위 수준에서 구성 작성기를 검색 합니다.
* `optional` -기본값은 `false`합니다. 소스 디렉터리가 없는 경우 구성 작성기에서 오류가 발생 해야 하는지 여부를 지정 합니다.

### <a name="simplejsonconfigbuilder"></a>SimpleJsonConfigBuilder

> [!WARNING]
> 암호 저장, 중요 한 연결 문자열 또는 기타 중요 한 데이터 소스 코드에서 하지 않습니다. 프로덕션 비밀을 사용 하지 않아야 개발 또는 테스트에 대 한 합니다.

```xml
<add name="SimpleJson"
    [mode|prefix|stripPrefix|tokenPattern]
    jsonFile="~\config.json"
    [optional="true"]
    [jsonMode="(Flat|Sectional)"]
    type="Microsoft.Configuration.ConfigurationBuilders.SimpleJsonConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Json" />
```

.NET core 프로젝트는 자주 구성에 대 한 JSON 파일을 사용합니다. 합니다 [SimpleJsonConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Json/) .NET Framework에서 사용할.NET Core JSON 파일을 허용 하는 작성기입니다. 이 구성 작성기는.NET Framework 구성의 특정 키/값 영역에 기본 키/값 원본에서 기본 매핑을 제공 합니다. 이 구성 작성기 않습니다 **되지** 계층적 구성에 대 한 제공 합니다. JSON 지원 파일을 사전에 복잡 한 계층적 개체가 아니라는 것과 비슷합니다. 여러 수준의 계층적 파일을 사용할 수 있습니다. 이 공급자 `flatten`s 각 수준을 사용 하 여 속성 이름을 추가 하 여 깊이 `:` 를 구분 합니다.

특성 세부 정보:

* `jsonFile` - 필수입니다. JSON 파일을 읽어올 수를 지정 합니다. `~` 앱 루트를 참조 하는 시작 시 문자를 사용할 수 있습니다.
* `optional` -부울, 기본값은 `true`합니다. 방지 JSON 파일을 찾을 수 없는 경우 예외를 throw 합니다.
* `jsonMode` - `[Flat|Sectional]`. 기본값은 `Flat`입니다. 때 `jsonMode` 는 `Flat`, JSON 파일을 단일 플랫 키/값 원본입니다. 합니다 `EnvironmentConfigBuilder` 및 `AzureKeyVaultConfigBuilder` 단일 플랫 키/값 소스 이기도 합니다. 경우는 `SimpleJsonConfigBuilder` 에 구성 된 `Sectional` 모드:

  * JSON 파일을 여러 사전에 최상위 수준에 개념적으로 구분 됩니다.
  * 각 사전에 연결 된 최상위 속성 이름과 일치 하는 구성 섹션에만 적용 됩니다. 예를 들어:

```json
    {
        "appSettings" : {
            "setting1" : "value1",
            "setting2" : "value2",
            "complex" : {
                "setting1" : "complex:value1",
                "setting2" : "complex:value2",
            }
        }
    }
```

## <a name="implementing-a-custom-keyvalue-configuration-builder"></a>사용자 지정 키/값 구성 작성기 구현

구성 작성기에는 요구 사항을 충족 하지 않습니다, 경우에 사용자 지정을 작성할 수 있습니다. `KeyValueConfigBuilder` 대체 모드 및 대부분의 접두사 문제를 처리 하는 기본 클래스입니다. 구현 하는 프로젝트만 필요 합니다.

* 기본 클래스에서 상속 되며 통해 키/값 쌍의 기본 소스를 구현 합니다 `GetValue` 고 `GetAllValues`:
* 추가 된 [Microsoft.Configuration.ConfigurationBuilders.Base](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Base/) 프로젝트입니다.

[!code-csharp[Main](config-builder/MyConfigBuilders/MyCustomConfigBuilder.cs)]

`KeyValueConfigBuilder` 기본 클래스는 많이 제공 및 일관 된 동작 키/값에서 구성 작성기입니다.

## <a name="additional-resources"></a>추가 자료

* [구성 작성기 GitHub 리포지토리](https://github.com/aspnet/MicrosoftConfigurationBuilders)
* [.NET을 사용 하 여 Azure Key Vault에 서비스 간 인증](/azure/key-vault/service-to-service-authentication#connection-string-support)
