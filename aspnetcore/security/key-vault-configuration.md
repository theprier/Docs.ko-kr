---
title: ASP.NET Core에서 azure Key Vault 구성 공급자
author: guardrex
description: Azure 키 자격 증명 모음 구성 공급자를 사용 하 여 런타임에 로드 하는 이름-값 쌍을 사용 하 여 앱을 구성 하는 방법을 알아봅니다.
monikerRange: '>= aspnetcore-1.1'
ms.author: riande
ms.custom: mvc
ms.date: 10/24/2018
uid: security/key-vault-configuration
ms.openlocfilehash: c6dc8b9c462841351b3ada72deeae727da356a6c
ms.sourcegitcommit: 375e9a67f5e1f7b0faaa056b4b46294cc70f55b7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50207890"
---
# <a name="azure-key-vault-configuration-provider-in-aspnet-core"></a><span data-ttu-id="cb625-103">ASP.NET Core에서 azure Key Vault 구성 공급자</span><span class="sxs-lookup"><span data-stu-id="cb625-103">Azure Key Vault configuration provider in ASP.NET Core</span></span>

<span data-ttu-id="cb625-104">하 여 [Luke Latham](https://github.com/guardrex) 고 [Andrew Stanton-nurse](https://github.com/anurse)</span><span class="sxs-lookup"><span data-stu-id="cb625-104">By [Luke Latham](https://github.com/guardrex) and [Andrew Stanton-Nurse](https://github.com/anurse)</span></span>

<span data-ttu-id="cb625-105">이 문서를 사용 하는 방법에 설명 합니다 [Microsoft Azure Key Vault](https://azure.microsoft.com/services/key-vault/) 구성 공급자를 Azure Key Vault 암호에서 앱 구성 값을 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-105">This document explains how to use the [Microsoft Azure Key Vault](https://azure.microsoft.com/services/key-vault/) configuration provider to load app configuration values from Azure Key Vault secrets.</span></span> <span data-ttu-id="cb625-106">Azure Key Vault는 암호화 키 및 앱 및 서비스에서 사용 하는 비밀을 보호 하는데 도움이 되는 클라우드 기반 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-106">Azure Key Vault is a cloud-based service that helps you safeguard cryptographic keys and secrets used by apps and services.</span></span> <span data-ttu-id="cb625-107">FIPS 140-2의 요구 사항을 충족 Level 2 유효성 검사가 하드웨어 보안 모듈 (HSM의) 구성 데이터를 저장 하는 경우 및 일반적인 시나리오에 중요 한 구성 데이터에 대 한 액세스 제어 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-107">Common scenarios include controlling access to sensitive configuration data and meeting the requirement for FIPS 140-2 Level 2 validated Hardware Security Modules (HSM's) when storing configuration data.</span></span> <span data-ttu-id="cb625-108">이 기능은 ASP.NET Core 1.1을 대상으로 하는 앱에 대해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-108">This feature is available for apps that target ASP.NET Core 1.1 or higher.</span></span>

<span data-ttu-id="cb625-109">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/key-vault-configuration/samples) ([다운로드 방법](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="cb625-109">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/key-vault-configuration/samples) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="package"></a><span data-ttu-id="cb625-110">패키지</span><span class="sxs-lookup"><span data-stu-id="cb625-110">Package</span></span>

<span data-ttu-id="cb625-111">공급자를 사용 하려면에 대 한 참조를 추가 합니다 [Microsoft.Extensions.Configuration.AzureKeyVault](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.AzureKeyVault/) 패키지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-111">To use the provider, add a reference to the [Microsoft.Extensions.Configuration.AzureKeyVault](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.AzureKeyVault/) package.</span></span>

## <a name="app-configuration"></a><span data-ttu-id="cb625-112">앱 구성</span><span class="sxs-lookup"><span data-stu-id="cb625-112">App configuration</span></span>

<span data-ttu-id="cb625-113">공급자를 탐색할 수 있습니다 합니다 [샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/key-vault-configuration/samples)합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-113">You can explore the provider with the [sample apps](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/key-vault-configuration/samples).</span></span> <span data-ttu-id="cb625-114">Key vault를 설정 하 고 자격 증명 모음에서 비밀을 만드는 샘플 앱 안전 하 게 비밀 값을 해당 구성을 로드 후 웹 페이지에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-114">Once you establish a key vault and create secrets in the vault, the sample apps securely load the secret values into their configurations and display them in webpages.</span></span>

<span data-ttu-id="cb625-115">공급자가 사용 하 여 앱의 구성에 추가 된 `AddAzureKeyVault` 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-115">The provider is added to the app's configuration with the `AddAzureKeyVault` extension.</span></span> <span data-ttu-id="cb625-116">샘플 앱에서 확장 프로그램에서 로드 된 세 가지 구성 값을 사용 합니다 *appsettings.json* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-116">In the sample apps, the extension uses three configuration values loaded from the *appsettings.json* file.</span></span>

| <span data-ttu-id="cb625-117">앱 설정</span><span class="sxs-lookup"><span data-stu-id="cb625-117">App Setting</span></span>    | <span data-ttu-id="cb625-118">설명</span><span class="sxs-lookup"><span data-stu-id="cb625-118">Description</span></span>                    | <span data-ttu-id="cb625-119">예제</span><span class="sxs-lookup"><span data-stu-id="cb625-119">Example</span></span>                                      |
| -------------- | ------------------------------ | -------------------------------------------- |
| `Vault`        | <span data-ttu-id="cb625-120">Azure Key Vault 이름</span><span class="sxs-lookup"><span data-stu-id="cb625-120">Azure Key Vault name</span></span>           | <span data-ttu-id="cb625-121">contosovault</span><span class="sxs-lookup"><span data-stu-id="cb625-121">contosovault</span></span>                                 |
| `ClientId`     | <span data-ttu-id="cb625-122">Azure Active Directory 앱 Id</span><span class="sxs-lookup"><span data-stu-id="cb625-122">Azure Active Directory App Id</span></span>  | <span data-ttu-id="cb625-123">627e911e-43cc-61d4-992e-12db9c81b413</span><span class="sxs-lookup"><span data-stu-id="cb625-123">627e911e-43cc-61d4-992e-12db9c81b413</span></span>         |
| `ClientSecret` | <span data-ttu-id="cb625-124">Azure Active Directory 앱 키</span><span class="sxs-lookup"><span data-stu-id="cb625-124">Azure Active Directory App Key</span></span> | <span data-ttu-id="cb625-125">g58K3dtg59o1Pa+e59v2Tx829w6VxTB2yv9sv/101di=</span><span class="sxs-lookup"><span data-stu-id="cb625-125">g58K3dtg59o1Pa+e59v2Tx829w6VxTB2yv9sv/101di=</span></span> |

[!code-csharp[Program](key-vault-configuration/samples/basic-sample/2.x/Program.cs?name=snippet1)]

## <a name="create-key-vault-secrets-and-load-configuration-values-basic-sample"></a><span data-ttu-id="cb625-126">Key vault 비밀 만들기 및 구성 값 (basic-샘플)를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-126">Create key vault secrets and load configuration values (basic-sample)</span></span>

1. <span data-ttu-id="cb625-127">Key vault 만들기 및 Azure Active Directory (Azure AD)의 지침에 따라 앱에 대 한 설정 [Azure Key Vault를 사용 하 여 시작](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-127">Create a key vault and set up Azure Active Directory (Azure AD) for the app following the guidance in [Get started with Azure Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-get-started/).</span></span>
   * <span data-ttu-id="cb625-128">사용 하 여 키 자격 증명 모음에 비밀을 추가 합니다 [AzureRM Key Vault PowerShell 모듈](/powershell/module/azurerm.keyvault) 에서 사용할 수 있습니다는 [PowerShell 갤러리](https://www.powershellgallery.com/packages/AzureRM.KeyVault)의 [Azure Key Vault REST API](/rest/api/keyvault/), 또는 합니다 [Azure Portal](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-128">Add secrets to the key vault using the [AzureRM Key Vault PowerShell Module](/powershell/module/azurerm.keyvault) available from the [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureRM.KeyVault), the [Azure Key Vault REST API](/rest/api/keyvault/), or the [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="cb625-129">암호 중 하나로 만들어집니다 *수동* 하거나 *인증서* 비밀입니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-129">Secrets are created as either *Manual* or *Certificate* secrets.</span></span> <span data-ttu-id="cb625-130">*인증서* 비밀 앱 및 서비스 사용에 대 한 인증서가 있지만 구성 공급자에서 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-130">*Certificate* secrets are certificates for use by apps and services but are not supported by the configuration provider.</span></span> <span data-ttu-id="cb625-131">사용 해야 합니다 *수동* 구성 공급자를 사용 하 여 사용 하 여 비밀 이름-값 쌍을 만드는 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-131">You should use the *Manual* option to create name-value pair secrets for use with the configuration provider.</span></span>
     * <span data-ttu-id="cb625-132">단순 암호는 이름-값 쌍으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-132">Simple secrets are created as name-value pairs.</span></span> <span data-ttu-id="cb625-133">Azure Key Vault 비밀 이름은 영숫자와 대시만 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-133">Azure Key Vault secret names are limited to alphanumeric characters and dashes.</span></span>
     * <span data-ttu-id="cb625-134">계층 값 (구성 섹션) 사용 하 여 `--` (두 개의 대시) 샘플에서 구분 기호로 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-134">Hierarchical values (configuration sections) use `--` (two dashes) as a separator in the sample.</span></span> <span data-ttu-id="cb625-135">일반적으로 하위 키에의 한 부분을 구분 하는 데 사용 되는 콜론 [ASP.NET Core 구성](xref:fundamentals/configuration/index), 비밀 이름에 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-135">Colons, which are normally used to delimit a section from a subkey in [ASP.NET Core configuration](xref:fundamentals/configuration/index), aren't allowed in secret names.</span></span> <span data-ttu-id="cb625-136">따라서 두 개의 대시 사용 되며 암호를 앱의 구성에 로드 될 때 콜론으로 교체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-136">Therefore, two dashes are used and swapped for a colon when the secrets are loaded into the app's configuration.</span></span>
     * <span data-ttu-id="cb625-137">2 개를 만든 *수동* 다음 이름-값 쌍을 포함 하는 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-137">Create two *Manual* secrets with the following name-value pairs.</span></span> <span data-ttu-id="cb625-138">첫 번째 암호 단순 이름 및 값 이며 두 번째 암호 섹션 및 비밀 이름에 하위 키를 사용 하 여 비밀 값을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-138">The first secret is a simple name and value, and the second secret creates a secret value with a section and subkey in the secret name:</span></span>
       * <span data-ttu-id="cb625-139">`SecretName`: `secret_value_1`</span><span class="sxs-lookup"><span data-stu-id="cb625-139">`SecretName`: `secret_value_1`</span></span>
       * <span data-ttu-id="cb625-140">`Section--SecretName`: `secret_value_2`</span><span class="sxs-lookup"><span data-stu-id="cb625-140">`Section--SecretName`: `secret_value_2`</span></span>
   * <span data-ttu-id="cb625-141">Azure Active Directory를 사용 하 여 샘플 앱을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-141">Register the sample app with Azure Active Directory.</span></span>
   * <span data-ttu-id="cb625-142">Key vault에 액세스 하려면 앱에 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-142">Authorize the app to access the key vault.</span></span> <span data-ttu-id="cb625-143">사용 하는 경우는 `Set-AzureRmKeyVaultAccessPolicy` key vault에 액세스 하려면 앱에 권한을 부여 하려면 PowerShell cmdlet을 제공 `List` 하 고 `Get` 사용 하 여 비밀에 액세스할 `-PermissionsToSecrets list,get`합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-143">When you use the `Set-AzureRmKeyVaultAccessPolicy` PowerShell cmdlet to authorize the app to access the key vault, provide `List` and `Get` access to secrets with `-PermissionsToSecrets list,get`.</span></span>

2. <span data-ttu-id="cb625-144">앱의 업데이트 *appsettings.json* 의 값을 사용 하 여 파일 `Vault`합니다 `ClientId`, 및 `ClientSecret`합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-144">Update the app's *appsettings.json* file with the values of `Vault`, `ClientId`, and `ClientSecret`.</span></span>
3. <span data-ttu-id="cb625-145">해당 구성 값을 가져오는 샘플 앱을 실행 `IConfigurationRoot` 비밀 이름으로 동일한 이름을 가진 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-145">Run the sample app, which obtains its configuration values from `IConfigurationRoot` with the same name as the secret name.</span></span>
   * <span data-ttu-id="cb625-146">비 계층 값: 값 `SecretName` 사용 하 여 가져오는 `config["SecretName"]`합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-146">Non-hierarchical values: The value for `SecretName` is obtained with `config["SecretName"]`.</span></span>
   * <span data-ttu-id="cb625-147">계층 값 (섹션): 사용 하 여 `:` (콜론) 표기법 또는 `GetSection` 확장 메서드.</span><span class="sxs-lookup"><span data-stu-id="cb625-147">Hierarchical values (sections): Use `:` (colon) notation or the `GetSection` extension method.</span></span> <span data-ttu-id="cb625-148">이러한 방법 중 하나를 사용 하 여 구성 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-148">Use either of these approaches to obtain the configuration value:</span></span>
     * `config["Section:SecretName"]`
     * `config.GetSection("Section")["SecretName"]`

<span data-ttu-id="cb625-149">앱을 실행 하는 경우 웹 페이지 로드 비밀 값을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-149">When you run the app, a webpage shows the loaded secret values:</span></span>

![Azure 키 자격 증명 모음 구성 공급자를 통해 로드 하는 비밀 값을 표시 하는 브라우저 창](key-vault-configuration/_static/sample1.png)

## <a name="bind-an-array-to-a-class"></a><span data-ttu-id="cb625-151">클래스에 배열 바인딩</span><span class="sxs-lookup"><span data-stu-id="cb625-151">Bind an array to a class</span></span>

<span data-ttu-id="cb625-152">공급자는 POCO 배열에 대 한 바인딩에 배열로 구성 값을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-152">The provider is capable of reading configuration values into an array for binding to a POCO array.</span></span>

<span data-ttu-id="cb625-153">콜론을 포함 하는 키를 허용 하는 구성 소스에서 읽을 때 (`:`) 구분 기호, 숫자 키 세그먼트 배열을 구성 하는 키를 구분 하기 위해 사용 됩니다 (`:0:`, `:1:`,...</span><span class="sxs-lookup"><span data-stu-id="cb625-153">When reading from a configuration source that allows keys to contain colon (`:`) separators, a numeric key segment is used to distinguish the keys that make up an array (`:0:`, `:1:`, …</span></span> <span data-ttu-id="cb625-154">`:{n}:`).</span><span class="sxs-lookup"><span data-stu-id="cb625-154">`:{n}:`).</span></span> <span data-ttu-id="cb625-155">자세한 내용은 [구성: 클래스에 배열을 바인딩할](xref:fundamentals/configuration/index#bind-an-array-to-a-class)합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-155">For more information, see [Configuration: Bind an array to a class](xref:fundamentals/configuration/index#bind-an-array-to-a-class).</span></span>

<span data-ttu-id="cb625-156">Azure Key Vault 키를 구분 기호로 콜론을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-156">Azure Key Vault keys can't use a colon as a separator.</span></span> <span data-ttu-id="cb625-157">이 항목에서 설명한 접근 방식을 사용 하 여 이중 대시 (`--`) 계층 값 (섹션)에 대 한 구분 기호로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-157">The approach described in this topic uses double dashes (`--`) as a separator for hierarchical values (sections).</span></span> <span data-ttu-id="cb625-158">배열 키는 이중 대시 및 숫자 키 세그먼트를 사용 하 여 Azure Key Vault에 저장 됩니다 (`--0--`, `--1--`,...</span><span class="sxs-lookup"><span data-stu-id="cb625-158">Array keys are stored in Azure Key Vault with double dashes and numeric key segments (`--0--`, `--1--`, …</span></span> <span data-ttu-id="cb625-159">`--{n}--`).</span><span class="sxs-lookup"><span data-stu-id="cb625-159">`--{n}--`).</span></span>

<span data-ttu-id="cb625-160">다음 검사 [Serilog](https://serilog.net/) 로깅 공급자 구성이 JSON 파일에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-160">Examine the following [Serilog](https://serilog.net/) logging provider configuration provided by a JSON file.</span></span> <span data-ttu-id="cb625-161">두 개체에 정의 된 리터럴을 가지는 `WriteTo` 두 Serilog를 반영 하는 배열 *싱크*, 로깅 출력의 대상을 설명 하는:</span><span class="sxs-lookup"><span data-stu-id="cb625-161">There are two object literals defined in the `WriteTo` array that reflect two Serilog *sinks*, which describe destinations for logging output:</span></span>

```json
"Serilog": {
  "WriteTo": [
    {
      "Name": "AzureTableStorage",
      "Args": {
        "storageTableName": "logs",
        "connectionString": "DefaultEnd...ountKey=Eby8...GMGw=="
      }
    },
    {
      "Name": "AzureDocumentDB",
      "Args": {
        "endpointUrl": "https://contoso.documents.azure.com:443",
        "authorizationKey": "Eby8...GMGw=="
      }
    }
  ]
}
```

<span data-ttu-id="cb625-162">이전 JSON 파일에 표시 된 구성은 이중 대시를 사용 하 여 Azure Key Vault에 저장 됩니다 (`--`) 표기법 및 숫자 세그먼트:</span><span class="sxs-lookup"><span data-stu-id="cb625-162">The configuration shown in the preceding JSON file is stored in Azure Key Vault using double dash (`--`) notation and numeric segments:</span></span>

| <span data-ttu-id="cb625-163">Key</span><span class="sxs-lookup"><span data-stu-id="cb625-163">Key</span></span> | <span data-ttu-id="cb625-164">값</span><span class="sxs-lookup"><span data-stu-id="cb625-164">Value</span></span> |
| --- | ----- |
| `Serilog--WriteTo--0--Name` | `AzureTableStorage` |
| `Serilog--WriteTo--0--Args--storageTableName` | `logs` |
| `Serilog--WriteTo--0--Args--connectionString` | `DefaultEnd...ountKey=Eby8...GMGw==` |
| `Serilog--WriteTo--1--Name` | `AzureDocumentDB` |
| `Serilog--WriteTo--1--Args--endpointUrl` | `https://contoso.documents.azure.com:443` |
| `Serilog--WriteTo--1--Args--authorizationKey` | `Eby8...GMGw==` |

## <a name="create-prefixed-key-vault-secrets-and-load-configuration-values-key-name-prefix-sample"></a><span data-ttu-id="cb625-165">접두사가 지정 된 key vault 비밀 만들기 및 구성 값 (키-이름-접두사-샘플)를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-165">Create prefixed key vault secrets and load configuration values (key-name-prefix-sample)</span></span>

<span data-ttu-id="cb625-166">`AddAzureKeyVault` 구현의 받아들이는 오버 로드가 제공 `IKeyVaultSecretManager`, 구성 키에 변환 된 키 자격 증명 모음 비밀을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-166">`AddAzureKeyVault` also provides an overload that accepts an implementation of `IKeyVaultSecretManager`, which allows you to control how key vault secrets are converted into configuration keys.</span></span> <span data-ttu-id="cb625-167">예를 들어, 앱 시작 시 제공한 접두사 값을 기반으로 하는 비밀 값을 로드 하는 인터페이스를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-167">For example, you can implement the interface to load secret values based on a prefix value you provide at app startup.</span></span> <span data-ttu-id="cb625-168">이렇게 하면 앱의 버전을 기반으로 하는 비밀 정보를 로드 하려면 예를 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-168">This allows you, for example, to load secrets based on the version of the app.</span></span>

> [!WARNING]
> <span data-ttu-id="cb625-169">동일한 키 자격 증명 모음에 여러 앱에 대 한 암호를 배치 하려면 또는 환경 비밀을 key vault 비밀의 접두사를 사용 하지 마세요 (예를 들어 *개발* 비교 *프로덕션* 비밀)를 동일한 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-169">Don't use prefixes on key vault secrets to place secrets for multiple apps into the same key vault or to place environmental secrets (for example, *development* versus *production* secrets) into the same vault.</span></span> <span data-ttu-id="cb625-170">다른 앱 및 개발/프로덕션 환경 앱 환경을 가장 높은 수준의 보안 격리를 별도 키 자격 증명 모음 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-170">We recommend that different apps and development/production environments use separate key vaults to isolate app environments for the highest level of security.</span></span>

<span data-ttu-id="cb625-171">두 번째 샘플 응용 프로그램을 사용 하 여, 만든 비밀에 대 한 key vault에 `5000-AppSecret` (마침표는 키 자격 증명 모음 비밀 이름에 허용 되지 않음) 앱의 5.0.0.0 버전용 앱 암호를 나타내는입니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-171">Using the second sample app, you create a secret in the key vault for `5000-AppSecret` (periods aren't allowed in key vault secret names) representing an app secret for version 5.0.0.0 of your app.</span></span> <span data-ttu-id="cb625-172">에 대 한 암호를 만들면 다른 버전의 경우 5.1.0.0, `5100-AppSecret`합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-172">For another version, 5.1.0.0, you create a secret for `5100-AppSecret`.</span></span> <span data-ttu-id="cb625-173">각 앱 버전으로 해당 구성을 로드 자체 비밀 값 `AppSecret`, 비밀 로드 된 버전 해제 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-173">Each app version loads its own secret value into its configuration as `AppSecret`, stripping off the version as it loads the secret.</span></span> <span data-ttu-id="cb625-174">아래 샘플의 구현이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-174">The sample's implementation is shown below:</span></span>

[!code-csharp[Configuration builder](key-vault-configuration/samples/key-name-prefix-sample/2.x/Program.cs?name=snippet1&highlight=18)]

[!code-csharp[PrefixKeyVaultSecretManager](key-vault-configuration/samples/key-name-prefix-sample/2.x/Startup.cs?name=snippet1)]

<span data-ttu-id="cb625-175">`Load` 을 찾거나 버전 접두사를 가진 자격 증명 모음 비밀을 통해 반복 하는 알고리즘 공급자에서 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-175">The `Load` method is called by a provider algorithm that iterates through the vault secrets to find the ones that have the version prefix.</span></span> <span data-ttu-id="cb625-176">버전 접두사를 사용 하 여 검색 되 면 `Load`, 알고리즘을 사용 하는 `GetKey` 비밀 이름의 구성 이름을 반환 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-176">When a version prefix is found with `Load`, the algorithm uses the `GetKey` method to return the configuration name of the secret name.</span></span> <span data-ttu-id="cb625-177">암호의 이름에서 버전 접두사를 제거 하 고 이름-값 쌍에 앱의 구성을 로드에 대 한 비밀 이름의 나머지를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-177">It strips off the version prefix from the secret's name and returns the rest of the secret name for loading into the app's configuration name-value pairs.</span></span>

<span data-ttu-id="cb625-178">이 방법은 구현 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="cb625-178">When you implement this approach:</span></span>

1. <span data-ttu-id="cb625-179">Key vault 비밀 로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-179">The key vault secrets are loaded.</span></span>
2. <span data-ttu-id="cb625-180">에 대 한 문자열 암호 `5000-AppSecret` 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-180">The string secret for `5000-AppSecret` is matched.</span></span>
3. <span data-ttu-id="cb625-181">버전 `5000` (대시로)는 하이픈이 제거 되어 종료 키 이름으로 `AppSecret` 비밀 값을 사용 하 여 앱의 구성을 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-181">The version, `5000` (with the dash), is stripped off of the key name leaving `AppSecret` to load with the secret value into the app's configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="cb625-182">제공할 수도 있습니다 고유한 `KeyVaultClient` 구현을 `AddAzureKeyVault`합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-182">You can also provide your own `KeyVaultClient` implementation to `AddAzureKeyVault`.</span></span> <span data-ttu-id="cb625-183">사용자 지정 클라이언트를 제공 합니다. 구성 공급자 및 앱의 다른 부분 간에 클라이언트의 단일 인스턴스를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-183">Supplying a custom client allows you to share a single instance of the client between the configuration provider and other parts of your app.</span></span>

1. <span data-ttu-id="cb625-184">Key vault 만들기 및 Azure Active Directory (Azure AD)의 지침에 따라 앱에 대 한 설정 [Azure Key Vault를 사용 하 여 시작](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-184">Create a key vault and set up Azure Active Directory (Azure AD) for the app following the guidance in [Get started with Azure Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-get-started/).</span></span>
   * <span data-ttu-id="cb625-185">사용 하 여 키 자격 증명 모음에 비밀을 추가 합니다 [AzureRM Key Vault PowerShell 모듈](/powershell/module/azurerm.keyvault) 에서 사용할 수 있습니다는 [PowerShell 갤러리](https://www.powershellgallery.com/packages/AzureRM.KeyVault)의 [Azure Key Vault REST API](/rest/api/keyvault/), 또는 합니다 [Azure Portal](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-185">Add secrets to the key vault using the [AzureRM Key Vault PowerShell Module](/powershell/module/azurerm.keyvault) available from the [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureRM.KeyVault), the [Azure Key Vault REST API](/rest/api/keyvault/), or the [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="cb625-186">암호 중 하나로 만들어집니다 *수동* 하거나 *인증서* 비밀입니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-186">Secrets are created as either *Manual* or *Certificate* secrets.</span></span> <span data-ttu-id="cb625-187">*인증서* 비밀 앱 및 서비스 사용에 대 한 인증서가 있지만 구성 공급자에서 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-187">*Certificate* secrets are certificates for use by apps and services but are not supported by the configuration provider.</span></span> <span data-ttu-id="cb625-188">사용 해야 합니다 *수동* 구성 공급자를 사용 하 여 사용 하 여 비밀 이름-값 쌍을 만드는 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-188">You should use the *Manual* option to create name-value pair secrets for use with the configuration provider.</span></span>
     * <span data-ttu-id="cb625-189">계층 값 (구성 섹션) 사용 하 여 `--` (두 개의 대시) 구분 기호로 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-189">Hierarchical values (configuration sections) use `--` (two dashes) as a separator.</span></span>
     * <span data-ttu-id="cb625-190">2 개를 만든 *수동* 다음 이름-값 쌍을 사용 하 여 비밀:</span><span class="sxs-lookup"><span data-stu-id="cb625-190">Create two *Manual* secrets with the following name-value pairs:</span></span>
       * <span data-ttu-id="cb625-191">`5000-AppSecret`: `5.0.0.0_secret_value`</span><span class="sxs-lookup"><span data-stu-id="cb625-191">`5000-AppSecret`: `5.0.0.0_secret_value`</span></span>
       * <span data-ttu-id="cb625-192">`5100-AppSecret`: `5.1.0.0_secret_value`</span><span class="sxs-lookup"><span data-stu-id="cb625-192">`5100-AppSecret`: `5.1.0.0_secret_value`</span></span>
   * <span data-ttu-id="cb625-193">Azure Active Directory를 사용 하 여 샘플 앱을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-193">Register the sample app with Azure Active Directory.</span></span>
   * <span data-ttu-id="cb625-194">Key vault에 액세스 하려면 앱에 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-194">Authorize the app to access the key vault.</span></span> <span data-ttu-id="cb625-195">사용 하는 경우는 `Set-AzureRmKeyVaultAccessPolicy` key vault에 액세스 하려면 앱에 권한을 부여 하려면 PowerShell cmdlet을 제공 `List` 하 고 `Get` 사용 하 여 비밀에 액세스할 `-PermissionsToSecrets list,get`합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-195">When you use the `Set-AzureRmKeyVaultAccessPolicy` PowerShell cmdlet to authorize the app to access the key vault, provide `List` and `Get` access to secrets with `-PermissionsToSecrets list,get`.</span></span>

2. <span data-ttu-id="cb625-196">앱의 업데이트 *appsettings.json* 의 값을 사용 하 여 파일 `Vault`합니다 `ClientId`, 및 `ClientSecret`합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-196">Update the app's *appsettings.json* file with the values of `Vault`, `ClientId`, and `ClientSecret`.</span></span>
3. <span data-ttu-id="cb625-197">해당 구성 값을 가져오는 샘플 앱을 실행 `IConfigurationRoot` 접두사가 비밀 이름으로 동일한 이름을 가진 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-197">Run the sample app, which obtains its configuration values from `IConfigurationRoot` with the same name as the prefixed secret name.</span></span> <span data-ttu-id="cb625-198">이 샘플에서는 접두사는 제공 된 앱의 버전을 `PrefixKeyVaultSecretManager` Azure Key Vault 구성 공급자를 추가 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="cb625-198">In this sample, the prefix is the app's version, which you provided to the `PrefixKeyVaultSecretManager` when you added the Azure Key Vault configuration provider.</span></span> <span data-ttu-id="cb625-199">에 대 한 값 `AppSecret` 사용 하 여 가져오는 `config["AppSecret"]`합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-199">The value for `AppSecret` is obtained with `config["AppSecret"]`.</span></span> <span data-ttu-id="cb625-200">앱에서 생성 된 웹 페이지 로드 된 값을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-200">The webpage generated by the app shows the loaded value:</span></span>

   ![브라우저 창에 앱의 버전 5.0.0.0 완료 되 면 Azure 키 자격 증명 모음 구성 공급자를 통해 로드 된 비밀 값 표시](key-vault-configuration/_static/sample2-1.png)

4. <span data-ttu-id="cb625-202">프로젝트 파일에서 해당 앱 어셈블리의 버전을 변경 `5.0.0.0` 에 `5.1.0.0` 앱을 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-202">Change the version of the app assembly in the project file from `5.0.0.0` to `5.1.0.0` and run the app again.</span></span> <span data-ttu-id="cb625-203">이 경우 반환 되는 비밀 값은 `5.1.0.0_secret_value`합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-203">This time, the secret value returned is `5.1.0.0_secret_value`.</span></span> <span data-ttu-id="cb625-204">앱에서 생성 된 웹 페이지 로드 된 값을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-204">The webpage generated by the app shows the loaded value:</span></span>

   ![브라우저 창에 앱의 버전 5.1.0.0 완료 되 면 Azure 키 자격 증명 모음 구성 공급자를 통해 로드 된 비밀 값 표시](key-vault-configuration/_static/sample2-2.png)

## <a name="control-access-to-the-clientsecret"></a><span data-ttu-id="cb625-206">ClientSecret에 대 한 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="cb625-206">Control access to the ClientSecret</span></span>

<span data-ttu-id="cb625-207">사용 합니다 [암호 관리자 도구](xref:security/app-secrets) 유지 하기 위해는 `ClientSecret` 프로젝트 트리 외부에 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-207">Use the [Secret Manager tool](xref:security/app-secrets) to maintain the `ClientSecret` outside of your project source tree.</span></span> <span data-ttu-id="cb625-208">암호 관리자 사용 하 여 특정 프로젝트를 사용 하 여 앱 암호를 연결을 여러 프로젝트 간에 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-208">With Secret Manager, you associate app secrets with a specific project and share them across multiple projects.</span></span>

<span data-ttu-id="cb625-209">인증서를 지 원하는 환경에서.NET Framework 앱을 개발 하는 경우 X.509 인증서를 사용 하 여 Azure Key Vault에 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-209">When developing a .NET Framework app in an environment that supports certificates, you can authenticate to Azure Key Vault with an X.509 certificate.</span></span> <span data-ttu-id="cb625-210">X.509 인증서의 개인 키 OS에 의해 관리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-210">The X.509 certificate's private key is managed by the OS.</span></span> <span data-ttu-id="cb625-211">자세한 내용은 [클라이언트 암호 대신 인증서를 사용 하 여 인증](/azure/key-vault/key-vault-use-from-web-application#authenticate-with-a-certificate-instead-of-a-client-secret)합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-211">For more information, see [Authenticate with a Certificate instead of a Client Secret](/azure/key-vault/key-vault-use-from-web-application#authenticate-with-a-certificate-instead-of-a-client-secret).</span></span> <span data-ttu-id="cb625-212">사용 된 `AddAzureKeyVault` 받아들이는 오버 로드는 `X509Certificate2` (`_env` 다음 예제에서:</span><span class="sxs-lookup"><span data-stu-id="cb625-212">Use the `AddAzureKeyVault` overload that accepts an `X509Certificate2` (`_env` in the following example :</span></span>

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

## <a name="reload-secrets"></a><span data-ttu-id="cb625-213">암호를 다시 로드</span><span class="sxs-lookup"><span data-stu-id="cb625-213">Reload secrets</span></span>

<span data-ttu-id="cb625-214">될 때까지 캐시 된 비밀 `IConfigurationRoot.Reload()` 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-214">Secrets are cached until `IConfigurationRoot.Reload()` is called.</span></span> <span data-ttu-id="cb625-215">만료를 비활성화 하 고 key vault에 암호를 업데이트 될 때까지 앱에서 준수 하지 않을 `Reload` 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-215">Expired, disabled, and updated secrets in the key vault are not respected by the app until `Reload` is executed.</span></span>

```csharp
Configuration.Reload();
```

## <a name="disabled-and-expired-secrets"></a><span data-ttu-id="cb625-216">사용 안 함 및 만료 된 암호</span><span class="sxs-lookup"><span data-stu-id="cb625-216">Disabled and expired secrets</span></span>

<span data-ttu-id="cb625-217">사용 안 함 및 만료 된 암호를 throw 한 `KeyVaultClientException`합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-217">Disabled and expired secrets throw a `KeyVaultClientException`.</span></span> <span data-ttu-id="cb625-218">앱에서 throw를 방지 하려면 앱 바꾸거나 사용 안 함/만료 된 암호를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-218">To prevent your app from throwing, replace your app or update the disabled/expired secret.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="cb625-219">문제 해결</span><span class="sxs-lookup"><span data-stu-id="cb625-219">Troubleshoot</span></span>

<span data-ttu-id="cb625-220">오류 메시지에 기록 됩니다 앱 공급자를 사용 하 여 구성을 로드 하지 못하면 합니다 [ASP.NET Core 로깅 인프라](xref:fundamentals/logging/index)합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-220">When the app fails to load configuration using the provider, an error message is written to the [ASP.NET Core Logging infrastructure](xref:fundamentals/logging/index).</span></span> <span data-ttu-id="cb625-221">다음 조건 하면 구성을 로드에서 하지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-221">The following conditions will prevent configuration from loading:</span></span>

* <span data-ttu-id="cb625-222">앱은 Azure Active Directory에 올바르게 구성 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-222">The app isn't configured correctly in Azure Active Directory.</span></span>
* <span data-ttu-id="cb625-223">Key vault는 Azure Key Vault에 존재 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-223">The key vault doesn't exist in Azure Key Vault.</span></span>
* <span data-ttu-id="cb625-224">앱은 key vault 액세스 권한이 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-224">The app isn't authorized to access the key vault.</span></span>
* <span data-ttu-id="cb625-225">액세스 정책에 포함 되지 않습니다 `Get` 고 `List` 권한.</span><span class="sxs-lookup"><span data-stu-id="cb625-225">The access policy doesn't include `Get` and `List` permissions.</span></span>
* <span data-ttu-id="cb625-226">키 자격 증명 모음에 구성 데이터 (이름-값 쌍)가 이름이, 누락, 비활성화 되었거나 만료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-226">In the key vault, the configuration data (name-value pair) is incorrectly named, missing, disabled, or expired.</span></span>
* <span data-ttu-id="cb625-227">앱에 잘못 된 키 자격 증명 모음 이름 (`Vault`)를 Azure AD 앱 Id (`ClientId`), 또는 Azure AD 키 (`ClientSecret`).</span><span class="sxs-lookup"><span data-stu-id="cb625-227">The app has the wrong key vault name (`Vault`), Azure AD App Id (`ClientId`), or Azure AD Key (`ClientSecret`).</span></span>
* <span data-ttu-id="cb625-228">Azure AD Key (`ClientSecret`) 만료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-228">The Azure AD Key (`ClientSecret`) is expired.</span></span>
* <span data-ttu-id="cb625-229">구성 키 (이름)를 로드 하려고 하는 값에 대 한 앱에서 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cb625-229">The configuration key (name) is incorrect in the app for the value you're trying to load.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cb625-230">추가 자료</span><span class="sxs-lookup"><span data-stu-id="cb625-230">Additional resources</span></span>

* <xref:fundamentals/configuration/index>
* [<span data-ttu-id="cb625-231">Microsoft Azure: 키 자격 증명 모음</span><span class="sxs-lookup"><span data-stu-id="cb625-231">Microsoft Azure: Key Vault</span></span>](https://azure.microsoft.com/services/key-vault/)
* [<span data-ttu-id="cb625-232">Microsoft Azure: Key Vault 설명서</span><span class="sxs-lookup"><span data-stu-id="cb625-232">Microsoft Azure: Key Vault Documentation</span></span>](/azure/key-vault/)
* [<span data-ttu-id="cb625-233">Azure Key Vault에 대 한 키 생성 및 HSM 보호 된 전송 하는 방법</span><span class="sxs-lookup"><span data-stu-id="cb625-233">How to generate and transfer HSM-protected keys for Azure Key Vault</span></span>](/azure/key-vault/key-vault-hsm-protected-keys)
* [<span data-ttu-id="cb625-234">KeyVaultClient 클래스</span><span class="sxs-lookup"><span data-stu-id="cb625-234">KeyVaultClient Class</span></span>](/dotnet/api/microsoft.azure.keyvault.keyvaultclient)
