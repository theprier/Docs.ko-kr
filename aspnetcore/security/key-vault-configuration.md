---
title: ASP.NET Core에서 azure Key Vault 구성 공급자
author: guardrex
description: Azure 키 자격 증명 모음 구성 공급자를 사용 하 여 런타임에 로드 하는 이름-값 쌍을 사용 하 여 앱을 구성 하는 방법을 알아봅니다.
ms.author: riande
ms.date: 08/01/2018
uid: security/key-vault-configuration
ms.openlocfilehash: 829c6c7e2750879b51bf3ce8225c6e472900f2ad
ms.sourcegitcommit: d53e0cc71542b92de867bcce51575b054886f529
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41828878"
---
# <a name="azure-key-vault-configuration-provider-in-aspnet-core"></a>ASP.NET Core에서 azure Key Vault 구성 공급자

하 여 [Luke Latham](https://github.com/guardrex) 고 [Andrew Stanton-nurse](https://github.com/anurse)

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

보기 또는 2.x 용 샘플 코드를 다운로드 합니다.

* [기본 샘플](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/key-vault-configuration/samples/basic-sample/2.x) ([다운로드 하는 방법을](xref:tutorials/index#how-to-download-a-sample))-앱에 비밀 값을 읽습니다.
* [키 이름 접두사 샘플](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/key-vault-configuration/samples/key-name-prefix-sample/2.x) ([다운로드 하는 방법을](xref:tutorials/index#how-to-download-a-sample))-다양 한 각 앱 버전에 대 한 비밀 값을 로드할 수 있는 앱의 버전을 나타내는 키 이름 접두사를 사용 하 여 읽기 비밀 값입니다.

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

보기 또는 1.x 용 샘플 코드를 다운로드 합니다.

* [기본 샘플](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/key-vault-configuration/samples/basic-sample/1.x) ([다운로드 하는 방법을](xref:tutorials/index#how-to-download-a-sample))-앱에 비밀 값을 읽습니다.
* [키 이름 접두사 샘플](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/key-vault-configuration/samples/key-name-prefix-sample/1.x) ([다운로드 하는 방법을](xref:tutorials/index#how-to-download-a-sample))-다양 한 각 앱 버전에 대 한 비밀 값을 로드할 수 있는 앱의 버전을 나타내는 키 이름 접두사를 사용 하 여 읽기 비밀 값입니다.

---

이 문서를 사용 하는 방법에 설명 합니다 [Microsoft Azure Key Vault](https://azure.microsoft.com/services/key-vault/) 구성 공급자를 Azure Key Vault 암호에서 앱 구성 값을 로드 합니다. Azure Key Vault는 암호화 키 및 앱 및 서비스에서 사용 하는 비밀을 보호 하는데 도움이 되는 클라우드 기반 서비스입니다. FIPS 140-2의 요구 사항을 충족 Level 2 유효성 검사가 하드웨어 보안 모듈 (HSM의) 구성 데이터를 저장 하는 경우 및 일반적인 시나리오에 중요 한 구성 데이터에 대 한 액세스 제어 포함 됩니다. 이 기능은 ASP.NET Core 1.1을 대상으로 하는 앱에 대해 사용할 수 있습니다.

## <a name="package"></a>패키지

공급자를 사용 하려면에 대 한 참조를 추가 합니다 [Microsoft.Extensions.Configuration.AzureKeyVault](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.AzureKeyVault/) 패키지 있습니다.

## <a name="app-configuration"></a>앱 구성

공급자를 탐색할 수 있습니다 합니다 [샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/key-vault-configuration/samples)합니다. Key vault를 설정 하 고 자격 증명 모음에서 비밀을 만드는 샘플 앱 안전 하 게 비밀 값을 해당 구성을 로드 후 웹 페이지에 표시 합니다.

공급자가 사용 하 여 앱의 구성에 추가 된 `AddAzureKeyVault` 확장 합니다. 샘플 앱에서 확장 프로그램에서 로드 된 세 가지 구성 값을 사용 합니다 *appsettings.json* 파일입니다.

| 앱 설정    | 설명                    | 예                                      |
| -------------- | ------------------------------ | -------------------------------------------- |
| `Vault`        | Azure Key Vault 이름           | contosovault                                 |
| `ClientId`     | Azure Active Directory 앱 Id  | 627e911e-43cc-61d4-992e-12db9c81b413         |
| `ClientSecret` | Azure Active Directory 앱 키 | g58K3dtg59o1Pa+e59v2Tx829w6VxTB2yv9sv/101di= |

[!code-csharp[Program](key-vault-configuration/samples/basic-sample/2.x/Program.cs?name=snippet1)]

## <a name="creating-key-vault-secrets-and-loading-configuration-values-basic-sample"></a>Key vault 비밀 만들기 및 구성 값 (basic-샘플)를 로드 합니다.

1. Key vault 만들기 및 Azure Active Directory (Azure AD)의 지침에 따라 앱에 대 한 설정 [Azure Key Vault를 사용 하 여 시작](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)합니다.
   * 사용 하 여 키 자격 증명 모음에 비밀을 추가 합니다 [AzureRM Key Vault PowerShell 모듈](/powershell/module/azurerm.keyvault) 에서 사용할 수 있습니다는 [PowerShell 갤러리](https://www.powershellgallery.com/packages/AzureRM.KeyVault)의 [Azure Key Vault REST API](/rest/api/keyvault/), 또는 합니다 [Azure Portal](https://portal.azure.com/)합니다. 암호 중 하나로 만들어집니다 *수동* 하거나 *인증서* 비밀입니다. *인증서* 비밀 앱 및 서비스 사용에 대 한 인증서가 있지만 구성 공급자에서 지원 되지 않습니다. 사용 해야 합니다 *수동* 구성 공급자를 사용 하 여 사용 하 여 비밀 이름-값 쌍을 만드는 옵션입니다.
     * 단순 암호는 이름-값 쌍으로 생성 됩니다. Azure Key Vault 비밀 이름은 영숫자와 대시만 제한 됩니다.
     * 계층 값 (구성 섹션) 사용 하 여 `--` (두 개의 대시) 샘플에서 구분 기호로 합니다. 일반적으로 하위 키에의 한 부분을 구분 하는 데 사용 되는 콜론 [ASP.NET Core 구성](xref:fundamentals/configuration/index), 비밀 이름에 허용 되지 않습니다. 따라서 두 개의 대시 사용 되며 암호를 앱의 구성에 로드 될 때 콜론으로 교체 됩니다.
     * 2 개를 만든 *수동* 다음 이름-값 쌍을 포함 하는 암호입니다. 첫 번째 암호 단순 이름 및 값 이며 두 번째 암호 섹션 및 비밀 이름에 하위 키를 사용 하 여 비밀 값을 만듭니다.
       * `SecretName`: `secret_value_1`
       * `Section--SecretName`: `secret_value_2`
   * Azure Active Directory를 사용 하 여 샘플 앱을 등록 합니다.
   * Key vault에 액세스 하려면 앱에 권한을 부여 합니다. 사용 하는 경우는 `Set-AzureRmKeyVaultAccessPolicy` key vault에 액세스 하려면 앱에 권한을 부여 하려면 PowerShell cmdlet을 제공 `List` 하 고 `Get` 사용 하 여 비밀에 액세스할 `-PermissionsToSecrets list,get`합니다.

2. 앱의 업데이트 *appsettings.json* 의 값을 사용 하 여 파일 `Vault`합니다 `ClientId`, 및 `ClientSecret`합니다.
3. 해당 구성 값을 가져오는 샘플 앱을 실행 `IConfigurationRoot` 비밀 이름으로 동일한 이름을 가진 합니다.
   * 비 계층 값: 값 `SecretName` 사용 하 여 가져오는 `config["SecretName"]`합니다.
   * 계층 값 (섹션): 사용 하 여 `:` (콜론) 표기법 또는 `GetSection` 확장 메서드. 이러한 방법 중 하나를 사용 하 여 구성 값을 가져옵니다.
     * `config["Section:SecretName"]`
     * `config.GetSection("Section")["SecretName"]`

앱을 실행 하는 경우 웹 페이지 로드 비밀 값을 보여줍니다.

![Azure 키 자격 증명 모음 구성 공급자를 통해 로드 하는 비밀 값을 표시 하는 브라우저 창](key-vault-configuration/_static/sample1.png)

## <a name="creating-prefixed-key-vault-secrets-and-loading-configuration-values-key-name-prefix-sample"></a>접두사가 지정 된 key vault 비밀 만들기 및 구성 값 (키-이름-접두사-샘플)를 로드 합니다.

`AddAzureKeyVault` 구현의 받아들이는 오버 로드가 제공 `IKeyVaultSecretManager`, 구성 키에 변환 된 키 자격 증명 모음 비밀을 제어할 수 있습니다. 예를 들어, 앱 시작 시 제공한 접두사 값을 기반으로 하는 비밀 값을 로드 하는 인터페이스를 구현할 수 있습니다. 이렇게 하면 앱의 버전을 기반으로 하는 비밀 정보를 로드 하려면 예를 들어 있습니다.

> [!WARNING]
> 동일한 키 자격 증명 모음에 여러 앱에 대 한 암호를 배치 하려면 또는 환경 비밀을 key vault 비밀의 접두사를 사용 하지 마세요 (예를 들어 *개발* 비교 *프로덕션* 비밀)를 동일한 자격 증명 모음입니다. 다른 앱 및 개발/프로덕션 환경 앱 환경을 가장 높은 수준의 보안 격리를 별도 키 자격 증명 모음 사용 하는 것이 좋습니다.

두 번째 샘플 응용 프로그램을 사용 하 여, 만든 비밀에 대 한 key vault에 `5000-AppSecret` (마침표는 키 자격 증명 모음 비밀 이름에 허용 되지 않음) 앱의 5.0.0.0 버전용 앱 암호를 나타내는입니다. 에 대 한 암호를 만들면 다른 버전의 경우 5.1.0.0, `5100-AppSecret`합니다. 각 앱 버전으로 해당 구성을 로드 자체 비밀 값 `AppSecret`, 비밀 로드 된 버전 해제 제거 합니다. 아래 샘플의 구현이 나와 있습니다.

[!code-csharp[Configuration builder](key-vault-configuration/samples/key-name-prefix-sample/2.x/Program.cs?name=snippet1&highlight=18)]

[!code-csharp[PrefixKeyVaultSecretManager](key-vault-configuration/samples/key-name-prefix-sample/2.x/Startup.cs?name=snippet1)]

`Load` 을 찾거나 버전 접두사를 가진 자격 증명 모음 비밀을 통해 반복 하는 알고리즘 공급자에서 호출 됩니다. 버전 접두사를 사용 하 여 검색 되 면 `Load`, 알고리즘을 사용 하는 `GetKey` 비밀 이름의 구성 이름을 반환 하는 방법입니다. 암호의 이름에서 버전 접두사를 제거 하 고 이름-값 쌍에 앱의 구성을 로드에 대 한 비밀 이름의 나머지를 반환 합니다.

이 방법은 구현 하는 경우:

1. Key vault 비밀 로드 됩니다.
2. 에 대 한 문자열 암호 `5000-AppSecret` 일치 합니다.
3. 버전 `5000` (대시로)는 하이픈이 제거 되어 종료 키 이름으로 `AppSecret` 비밀 값을 사용 하 여 앱의 구성을 로드 합니다.

> [!NOTE]
> 제공할 수도 있습니다 고유한 `KeyVaultClient` 구현을 `AddAzureKeyVault`합니다. 사용자 지정 클라이언트를 제공 합니다. 구성 공급자 및 앱의 다른 부분 간에 클라이언트의 단일 인스턴스를 공유할 수 있습니다.

1. Key vault 만들기 및 Azure Active Directory (Azure AD)의 지침에 따라 앱에 대 한 설정 [Azure Key Vault를 사용 하 여 시작](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)합니다.
   * 사용 하 여 키 자격 증명 모음에 비밀을 추가 합니다 [AzureRM Key Vault PowerShell 모듈](/powershell/module/azurerm.keyvault) 에서 사용할 수 있습니다는 [PowerShell 갤러리](https://www.powershellgallery.com/packages/AzureRM.KeyVault)의 [Azure Key Vault REST API](/rest/api/keyvault/), 또는 합니다 [Azure Portal](https://portal.azure.com/)합니다. 암호 중 하나로 만들어집니다 *수동* 하거나 *인증서* 비밀입니다. *인증서* 비밀 앱 및 서비스 사용에 대 한 인증서가 있지만 구성 공급자에서 지원 되지 않습니다. 사용 해야 합니다 *수동* 구성 공급자를 사용 하 여 사용 하 여 비밀 이름-값 쌍을 만드는 옵션입니다.
     * 계층 값 (구성 섹션) 사용 하 여 `--` (두 개의 대시) 구분 기호로 합니다.
     * 2 개를 만든 *수동* 다음 이름-값 쌍을 사용 하 여 비밀:
       * `5000-AppSecret`: `5.0.0.0_secret_value`
       * `5100-AppSecret`: `5.1.0.0_secret_value`
   * Azure Active Directory를 사용 하 여 샘플 앱을 등록 합니다.
   * Key vault에 액세스 하려면 앱에 권한을 부여 합니다. 사용 하는 경우는 `Set-AzureRmKeyVaultAccessPolicy` key vault에 액세스 하려면 앱에 권한을 부여 하려면 PowerShell cmdlet을 제공 `List` 하 고 `Get` 사용 하 여 비밀에 액세스할 `-PermissionsToSecrets list,get`합니다.

2. 앱의 업데이트 *appsettings.json* 의 값을 사용 하 여 파일 `Vault`합니다 `ClientId`, 및 `ClientSecret`합니다.
3. 해당 구성 값을 가져오는 샘플 앱을 실행 `IConfigurationRoot` 접두사가 비밀 이름으로 동일한 이름을 가진 합니다. 이 샘플에서는 접두사는 제공 된 앱의 버전을 `PrefixKeyVaultSecretManager` Azure Key Vault 구성 공급자를 추가 하는 경우. 에 대 한 값 `AppSecret` 사용 하 여 가져오는 `config["AppSecret"]`합니다. 앱에서 생성 된 웹 페이지 로드 된 값을 보여 줍니다.

   ![브라우저 창에 앱의 버전 5.0.0.0 완료 되 면 Azure 키 자격 증명 모음 구성 공급자를 통해 로드 된 비밀 값 표시](key-vault-configuration/_static/sample2-1.png)

4. 프로젝트 파일에서 해당 앱 어셈블리의 버전을 변경 `5.0.0.0` 에 `5.1.0.0` 앱을 다시 실행 합니다. 이 경우 반환 되는 비밀 값은 `5.1.0.0_secret_value`합니다. 앱에서 생성 된 웹 페이지 로드 된 값을 보여 줍니다.

   ![브라우저 창에 앱의 버전 5.1.0.0 완료 되 면 Azure 키 자격 증명 모음 구성 공급자를 통해 로드 된 비밀 값 표시](key-vault-configuration/_static/sample2-2.png)

## <a name="controlling-access-to-the-clientsecret"></a>ClientSecret에 대 한 액세스를 제어합니다.

사용 합니다 [암호 관리자 도구](xref:security/app-secrets) 유지 하기 위해는 `ClientSecret` 프로젝트 트리 외부에 원본입니다. 암호 관리자 사용 하 여 특정 프로젝트를 사용 하 여 앱 암호를 연결을 여러 프로젝트 간에 공유 합니다.

인증서를 지 원하는 환경에서.NET Framework 앱을 개발 하는 경우 X.509 인증서를 사용 하 여 Azure Key Vault에 인증할 수 있습니다. X.509 인증서의 개인 키 OS에 의해 관리 됩니다. 자세한 내용은 [클라이언트 암호 대신 인증서를 사용 하 여 인증](https://docs.microsoft.com/azure/key-vault/key-vault-use-from-web-application#authenticate-with-a-certificate-instead-of-a-client-secret)합니다. 사용 된 `AddAzureKeyVault` 받아들이는 오버 로드는 `X509Certificate2` (`_env` 다음 예제에서:

```csharp
var builtConfig = config.Build();

var store = new X509Store(StoreLocation.CurrentUser);
store.Open(OpenFlags.ReadOnly);
var cert = store.Certificates
    .Find(X509FindType.FindByThumbprint, 
        config["CertificateThumbprint"], false);

config.AddAzureKeyVault(
    builtConfig["Vault"],
    builtConfig["ClientId"],
    cert.OfType<X509Certificate2>().Single(),
    new EnvironmentSecretManager(context.HostingEnvironment.ApplicationName));

store.Close();
```

## <a name="reloading-secrets"></a>암호를 다시 로드

될 때까지 캐시 된 비밀 `IConfigurationRoot.Reload()` 라고 합니다. 만료를 비활성화 하 고 key vault에 암호를 업데이트 될 때까지 앱에서 준수 하지 않을 `Reload` 실행 됩니다.

```csharp
Configuration.Reload();
```

## <a name="disabled-and-expired-secrets"></a>사용 안 함 및 만료 된 암호

사용 안 함 및 만료 된 암호를 throw 한 `KeyVaultClientException`합니다. 앱에서 throw를 방지 하려면 앱 바꾸거나 사용 안 함/만료 된 암호를 업데이트 합니다.

## <a name="troubleshooting"></a>문제 해결

오류 메시지에 기록 됩니다 앱 공급자를 사용 하 여 구성을 로드 하지 못하면 합니다 [ASP.NET Core 로깅 인프라](xref:fundamentals/logging/index)합니다. 다음 조건 하면 구성을 로드에서 하지 것입니다.

* 앱은 Azure Active Directory에 올바르게 구성 되지 않았습니다.
* Key vault는 Azure Key Vault에 존재 하지 않습니다.
* 앱은 key vault 액세스 권한이 없는 합니다.
* 액세스 정책에 포함 되지 않습니다 `Get` 고 `List` 권한.
* 키 자격 증명 모음에 구성 데이터 (이름-값 쌍)가 이름이, 누락, 비활성화 되었거나 만료 되었습니다.
* 앱에 잘못 된 키 자격 증명 모음 이름 (`Vault`)를 Azure AD 앱 Id (`ClientId`), 또는 Azure AD 키 (`ClientSecret`).
* Azure AD Key (`ClientSecret`) 만료 되었습니다.
* 구성 키 (이름)를 로드 하려고 하는 값에 대 한 앱에서 올바르지 않습니다.

## <a name="additional-resources"></a>추가 자료

* <xref:fundamentals/configuration/index>
* [Microsoft Azure: 키 자격 증명 모음](https://azure.microsoft.com/services/key-vault/)
* [Microsoft Azure: Key Vault 설명서](/azure/key-vault/)
* [Azure Key Vault에 대 한 키 생성 및 HSM 보호 된 전송 하는 방법](/azure/key-vault/key-vault-hsm-protected-keys)
* [KeyVaultClient 클래스](/dotnet/api/microsoft.azure.keyvault.keyvaultclient)
