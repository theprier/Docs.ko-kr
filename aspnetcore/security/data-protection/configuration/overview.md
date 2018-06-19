---
title: ASP.NET Core 데이터 보호를 구성 합니다.
author: rick-anderson
description: ASP.NET Core에서 데이터 보호를 구성 하는 방법을 알아봅니다.
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 07/17/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/data-protection/configuration/overview
ms.openlocfilehash: 803b81f5f69496900791ca1d1976f70f8c266f29
ms.sourcegitcommit: 466300d32f8c33e64ee1b419a2cbffe702863cdf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/27/2018
ms.locfileid: "34555419"
---
# <a name="configure-aspnet-core-data-protection"></a>ASP.NET Core 데이터 보호를 구성 합니다.

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)

데이터 보호 시스템이 초기화 될 때, 운영 환경에 따른 [기본 설정](xref:security/data-protection/configuration/default-settings) 이 적용됩니다. 대부분 이런 기본 설정은 단일 컴퓨터에서 실행되는 앱에 적합합니다. 개발자는 기본 설정을 변경 해야 할 수는 있는 경우가 있습니다.

* 여러 컴퓨터 간에 분산 되는 앱입니다.
* 준수 이유 때문입니다.

이러한 시나리오에 대 한 데이터 보호 시스템 풍부한 구성 API를 제공합니다.

> [!WARNING]
> 마찬가지로 구성 파일, 데이터 보호 키 링 보호 해야 적절 한 사용 권한을 사용 합니다. 을 미사용 키를 암호화 하도록 선택할 수 있습니다 하지만이 되지 않도록 공격자가 새 키를 만드는 합니다. 따라서 응용 프로그램의 보안이 저하 됩니다. 데이터 보호를 사용 하 여 구성 저장소 위치는 응용 프로그램 구성 파일을 보호 하는 방식과 유사 하 게 자체가으로 제한 된 액세스 권한이 있어야 합니다. 예를 들어 키 링 디스크에 저장 하려는 경우에 파일 시스템 권한을 사용 합니다. id만 보장 웹 앱에서 실행 되는 대 한 읽기, 쓰기 및 해당 디렉터리에 대 한 액세스를 만듭니다. Azure 테이블 저장소를 사용 하는 경우 웹 앱에만 읽기, 쓰기 또는 등 테이블 저장소에 새 항목을 만들 수가 있어야 합니다.
>
> 확장 메서드 [AddDataProtection](/dotnet/api/microsoft.extensions.dependencyinjection.dataprotectionservicecollectionextensions.adddataprotection) 반환는 [IDataProtectionBuilder](/dotnet/api/microsoft.aspnetcore.dataprotection.idataprotectionbuilder)합니다. `IDataProtectionBuilder` 는 함께 연이어 호출해서 데이터 보호 옵션을 구성할 수 있는 확장 메서드들을 노출합니다. 

::: moniker range=">= aspnetcore-2.1"

## <a name="protectkeyswithazurekeyvault"></a>ProtectKeysWithAzureKeyVault

키를 저장할 [Azure 키 자격 증명 모음](https://azure.microsoft.com/services/key-vault/), 시스템 구성 [ProtectKeysWithAzureKeyVault](/dotnet/api/microsoft.aspnetcore.dataprotection.azuredataprotectionbuilderextensions.protectkeyswithazurekeyvault) 에 `Startup` 클래스:

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .PersistKeysToAzureBlobStorage(new Uri("<blobUriWithSasToken>"))
        .ProtectKeysWithAzureKeyVault("<keyIdentifier>", "<clientId>", "<clientSecret>");
}
```

키 링 저장소 위치 설정 (예를 들어 [PersistKeysToAzureBlobStorage](/dotnet/api/microsoft.aspnetcore.dataprotection.azuredataprotectionbuilderextensions.persistkeystoazureblobstorage)). 호출 하기 때문에 위치를 설정 해야 `ProtectKeysWithAzureKeyVault` 구현 하는 [IXmlEncryptor](/dotnet/api/microsoft.aspnetcore.dataprotection.xmlencryption.ixmlencryptor) 키 링 저장소 위치를 포함 한 데이터 자동 보호 설정을 사용 하지 않도록 설정 하는 합니다. 앞의 예제에서는 키 링을 유지 하기 위해 Azure Blob 저장소를 사용 합니다. 자세한 내용은 참조 [키 저장소 공급자: Azure와 Redis](xref:security/data-protection/implementation/key-storage-providers#azure-and-redis)합니다. 사용 하 여 로컬로 키 링을 유지할 수 있습니다 [PersistKeysToFileSystem](xref:security/data-protection/implementation/key-storage-providers#file-system)합니다.

`keyIdentifier` 는 키 암호화에 사용 되는 주요 자격 증명 모음 키 식별자 (예를 들어 `https://contosokeyvault.vault.azure.net/keys/dataprotection/`).

`ProtectKeysWithAzureKeyVault` 오버 로드:

* [ProtectKeysWithAzureKeyVault (IDataProtectionBuilder, KeyVaultClient, String)](/dotnet/api/microsoft.aspnetcore.dataprotection.azuredataprotectionbuilderextensions.protectkeyswithazurekeyvault#Microsoft_AspNetCore_DataProtection_AzureDataProtectionBuilderExtensions_ProtectKeysWithAzureKeyVault_Microsoft_AspNetCore_DataProtection_IDataProtectionBuilder_Microsoft_Azure_KeyVault_KeyVaultClient_System_String_) 사용할 수는 [KeyVaultClient](/dotnet/api/microsoft.azure.keyvault.keyvaultclient) 주요 자격 증명 모음을 사용 하도록 데이터 보호 시스템 수 있도록 합니다.
* [(IDataProtectionBuilder, String, String, X509Certificate2) ProtectKeysWithAzureKeyVault](/dotnet/api/microsoft.aspnetcore.dataprotection.azuredataprotectionbuilderextensions.protectkeyswithazurekeyvault#Microsoft_AspNetCore_DataProtection_AzureDataProtectionBuilderExtensions_ProtectKeysWithAzureKeyVault_Microsoft_AspNetCore_DataProtection_IDataProtectionBuilder_System_String_System_String_System_Security_Cryptography_X509Certificates_X509Certificate2_) 사용할 수는 `ClientId` 및 [X509Certificate](/dotnet/api/system.security.cryptography.x509certificates.x509certificate2) 주요 자격 증명 모음을 사용 하도록 데이터 보호 시스템 수 있도록 합니다.
* [(IDataProtectionBuilder, String, String, String) ProtectKeysWithAzureKeyVault](/dotnet/api/microsoft.aspnetcore.dataprotection.azuredataprotectionbuilderextensions.protectkeyswithazurekeyvault#Microsoft_AspNetCore_DataProtection_AzureDataProtectionBuilderExtensions_ProtectKeysWithAzureKeyVault_Microsoft_AspNetCore_DataProtection_IDataProtectionBuilder_System_String_System_String_System_String_) 사용할 수는 `ClientId` 및 `ClientSecret` 주요 자격 증명 모음을 사용 하도록 데이터 보호 시스템 수 있도록 합니다.

::: moniker-end

## <a name="persistkeystofilesystem"></a>PersistKeysToFileSystem

기본 위치인 *%LOCALAPPDATA%* 대신 UNC 공유에 키를 저장하려면 [PersistKeysToFileSystem](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystofilesystem)을 이용해서 다음과 같이 시스템을 구성합니다.

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .PersistKeysToFileSystem(new DirectoryInfo(@"\\server\share\directory\"));
}
```

> [!WARNING]
> 키의 저장 위치를 변경하면 데이터 보호 시스템이 더 이상 저장된 비활성 키를 자동으로 암호화하지 않는데, 이는 DPAPI가 적절한 암호화 메커니즘인지 판단하기가 곤란하기 때문입니다.

## <a name="protectkeyswith"></a>ProtectKeysWith\*

[ProtectKeysWith\*](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions) 구성 API들 중 하나를 호출하면 시스템이 저장된 비활성 키를 보호하도록 구성할 수 있습니다. 다음 예제는 키를 UNC 공유에 저장하고 특정 X.509 인증서를 이용해서 저장된 비활성 키를 암호화합니다.

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .PersistKeysToFileSystem(new DirectoryInfo(@"\\server\share\directory\"))
        .ProtectKeysWithCertificate("thumbprint");
}
```

내장 키 암호화 메커니즘에 대한 더 많은 예제와 설명은 [비활성 키 암호화](xref:security/data-protection/implementation/key-encryption-at-rest)를 참고하시기 바랍니다.

## <a name="setdefaultkeylifetime"></a>SetDefaultKeyLifetime

키의 기본 수명인 90일 대신 14일의 키 수명을 사용하도록 시스템을 구성하려면 [SetDefaultKeyLifetime](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setdefaultkeylifetime)을 사용합니다.

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .SetDefaultKeyLifetime(TimeSpan.FromDays(14));
}
```

## <a name="setapplicationname"></a>SetApplicationName

데이터 보호 시스템은 기본적으로 앱들이 동일한 물리적 키 저장소를 공유하는 경우에도 앱들을 서로 격리합니다. 따라서 앱들은 서로 다른 앱이 보호한 페이로드를 이해할 수 없습니다. 서로 다른 두 앱 간에 보호된 페이로드를 공유하려면, 각 앱 모두에서 [SetApplicationName](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setapplicationname) 을 이용해서 동일한 앱 이름을 전달하여 시스템을 구성해야 합니다.

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .SetApplicationName("shared app name");
}
```

## <a name="disableautomatickeygeneration"></a>DisableAutomaticKeyGeneration

키 만료가 다가오더라도 앱이 자동으로 키를 롤링하지 않도록 (새로운 키를 생성하지 않도록) 구성해야 하는 시나리오도 있을 수 있습니다. 한 가지 사례는 앱들이 주/보조 관계를 갖도록 설정되어 있어서 주 앱만 키 관리 작업을 수행하고 나머지 모든 보조 앱들은 단순히 키 링의 읽기 전용 뷰만 갖고 있는 경우입니다. 그런 경우에는 [DisableAutomaticKeyGeneration](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.disableautomatickeygeneration)으로 보조 앱은 키 링을 읽기 전용으로만 처리하도록 시스템을 구성할 수 있습니다.

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .DisableAutomaticKeyGeneration();
}
```

## <a name="per-application-isolation"></a>응용 프로그램 격리

ASP.NET Core 호스트에 의해서 데이터 보호 시스템이 제공되는 경우, 여러 앱이 동일한 작업자 프로세스 계정으로 실행되고 동일한 마스터 키 관련 자료를 사용하더라도 서로 자동으로 격리됩니다 이런 특징은 System.Web의  **\<machineKey >** 요소에서 제공되는 IsolateApps 한정자의 동작과 다소 유사합니다.

이 격리 메커니즘은 로컬 컴퓨터의 각 응용 프로그램들을 고유한 테넌트로 간주하는 방식으로 동작하며, 따라서 해당하는 모든 응용 프로그램에 루트로 제공되는 [IDataProtector](/dotnet/api/microsoft.aspnetcore.dataprotection.idataprotector) 에는 자동으로 응용 프로그램 ID가 판별자로 포함됩니다. 여기에 사용되는 응용 프로그램 고유 ID는 다음 두 가지 방법 중 한 가지 방식으로 얻어집니다.

1. 응용 프로그램이 IIS에서 호스트 될 경우, 응용 프로그램의 구성 경로가 고유 식별자로 사용됩니다. 만약 응용 프로그램이 팜 환경에 배포된다면 팜에 포함된 모든 컴퓨터 간에 IIS 환경이 비슷하게 구성되었다는 전제하에 이 값이 일정해야 합니다.

2. 응용 프로그램이 IIS에서 호스트 되지 않을 경우, 응용 프로그램의 물리적 경로가 고유 식별자로 사용됩니다.

고유 식별자 다시 설정 후에 유지 하도록 되어 &mdash; 개별 응용 프로그램 및 컴퓨터 자체입니다.

이 격리 메커니즘은 응용 프로그램에 악의적인 의사가 없음을 전제로 합니다. 악의적인 응용 프로그램은 언제든지 동일한 작업자 프로세스 계정으로 동작하는 다른 모든 응용 프로그램에 영향을 미칠 수 있습니다. 응용 프로그램들 간에 서로 신뢰할 수 없는 공유 호스팅 환경에서는 호스팅 공급자가 응용 프로그램의 기본 키 저장소를 분리하는 등, OS 수준에서 응용 프로그램 간에 격리를 담보할 수 있는 조치를 취해야만 합니다. 

데이터 보호 시스템이 ASP.NET Core 호스트에 의해 제공되지 않는 경우에는 (가령, 개발자가 직접 구체적인 `DataProtectionProvider` 형식을 이용해서 인스턴스를 생성하는 등), 자동으로 응용 프로그램 격리가 비활성화되며 적절한 [용도](xref:security/data-protection/consumer-apis/purpose-strings)를 제공하기만 하면 동일한 키 관련 자료를 사용하는 모든 응용 프로그램들 간에 페이로드를 공유할 수 있습니다. 이런 환경에서 응용 프로그램 간 격리를 제공하려면 앞에서 살펴본 예제처럼 구성 개체의 [SetApplicationName](#setapplicationname) 메서드를 호출하면 됩니다.

## <a name="changing-algorithms-with-usecryptographicalgorithms"></a>UseCryptographicAlgorithms으로 알고리즘 변경하기

새로 생성된 키에 의해 사용되는 데이터 보호 스택의 기본 알고리즘을 변경할 수도 있습니다. 이 작업을 수행하는 가장 간단한 방법은 구성 콜백에서 [UseCryptographicAlgorithms](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.usecryptographicalgorithms) 을 호출하는 것입니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

```csharp
services.AddDataProtection()
    .UseCryptographicAlgorithms(
        new AuthenticatedEncryptorConfiguration()
    {
        EncryptionAlgorithm = EncryptionAlgorithm.AES_256_CBC,
        ValidationAlgorithm = ValidationAlgorithm.HMACSHA256
    });
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

```csharp
services.AddDataProtection()
    .UseCryptographicAlgorithms(
        new AuthenticatedEncryptionSettings()
    {
        EncryptionAlgorithm = EncryptionAlgorithm.AES_256_CBC,
        ValidationAlgorithm = ValidationAlgorithm.HMACSHA256
    });
```

---

EncryptionAlgorithm 및 ValidationAlgorithm의 기본값은 각각 AES-256-CBC와 HMACSHA256 입니다. 시스템 관리자가 [컴퓨터 수준 정책](xref:security/data-protection/configuration/machine-wide-policy)을 통해서 기본 정책을 설정할 수도 있지만, 명시적으로 `UseCryptographicAlgorithms`를 호출하면 기본 정책이 재정의됩니다.

`UseCryptographicAlgorithms` 을 호출하면 미리 제공되는 목록 중에서 원하는 알고리즘을 지정할 수 있습니다. 개발자는 알고리즘 구현을 걱정할 필요가 없습니다. 위의 시나리오에서 데이터 보호 시스템이 Windows에서 실행 중이라면 AES의 CNG 구현을 사용하려고 시도하고,  그렇지 않으면 관리되는 [System.Security.Cryptography.Aes](/dotnet/api/system.security.cryptography.aes) 클래스로 대체됩니다.

[UseCustomCryptographicAlgorithms](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.usecustomcryptographicalgorithms)를 호출해서 원하는 구현을 직접 지정할 수도 있습니다.

> [!TIP]
> 알고리즘을 변경하더라도 키 링에 존재하는 기존 키에는 영향을 주지 않습니다. 알고리즘 변경은 새로 생성되는 키에만 영향을 줍니다.

### <a name="specifying-custom-managed-algorithms"></a>관리되는 사용자 지정 알고리즘 지정하기

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

관리 되는 사용자 지정 알고리즘을 지정 하려면 만듭니다는 [ManagedAuthenticatedEncryptorConfiguration](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.configurationmodel.managedauthenticatedencryptorconfiguration) 구현 형식을 가리키는 인스턴스:

```csharp
serviceCollection.AddDataProtection()
    .UseCustomCryptographicAlgorithms(
        new ManagedAuthenticatedEncryptorConfiguration()
    {
        // A type that subclasses SymmetricAlgorithm
        EncryptionAlgorithmType = typeof(Aes),

        // Specified in bits
        EncryptionAlgorithmKeySize = 256,

        // A type that subclasses KeyedHashAlgorithm
        ValidationAlgorithmType = typeof(HMACSHA256)
    });
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

관리되는 사용자 지정 알고리즘을 지정하려면, 구현 형식을 가리키는 [ManagedAuthenticatedEncryptionSettings](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.managedauthenticatedencryptionsettings) 의 인스턴스를 생성합니다.

```csharp
serviceCollection.AddDataProtection()
    .UseCustomCryptographicAlgorithms(
        new ManagedAuthenticatedEncryptionSettings()
    {
        // A type that subclasses SymmetricAlgorithm
        EncryptionAlgorithmType = typeof(Aes),

        // Specified in bits
        EncryptionAlgorithmKeySize = 256,

        // A type that subclasses KeyedHashAlgorithm
        ValidationAlgorithmType = typeof(HMACSHA256)
    });
```

---

일반적으로 \*Type 속성들은 구체적이고 인스턴스를 생성할 수 있는 (매개변수가 없는 public 생성자를 통해서) [SymmetricAlgorithm](/dotnet/api/system.security.cryptography.symmetricalgorithm) 및 [KeyedHashAlgorithm](/dotnet/api/system.security.cryptography.keyedhashalgorithm)의 구현을 가리켜야 하지만, 시스템 상 특수한 경우에는 편의를 위해 `typeof(Aes)` 같은 특정 값들을 지정하기도 합니다

> [!NOTE]
> SymmetricAlgorithm 은 반드시 키 길이가 128 비트 이상이고 블럭 크키가 64 비트 이상이어야 하며, PKCS #7 패딩을 사용하는 CBC 모드 암호화를 지원해야 합니다. KeyedHashAlgorithm 은 다이제스트 크기가 128 비트 이상이어야 하고, 해시 알고리즘의 다이제스트 길이와 동일한 키 길이를 지원해야 합니다 KeyedHashAlgorithm 이 반드시 HMAC여야 할 필요는 없습니다

### <a name="specifying-custom-windows-cng-algorithms"></a>사용자 지정 Windows CNG 알고리즘 지정하기

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

CBC 모드 암호화 + HMAC 유효성 검사를 사용하는 사용자 지정 Windows CNG 알고리즘을 지정하려면, 알고리즘 정보를 담고 있는 [CngCbcAuthenticatedEncryptorConfiguration](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.configurationmodel.cngcbcauthenticatedencryptorconfiguration)의 인스턴스를 생성합니다

```csharp
services.AddDataProtection()
    .UseCustomCryptographicAlgorithms(
        new CngCbcAuthenticatedEncryptorConfiguration()
    {
        // Passed to BCryptOpenAlgorithmProvider
        EncryptionAlgorithm = "AES",
        EncryptionAlgorithmProvider = null,

        // Specified in bits
        EncryptionAlgorithmKeySize = 256,

        // Passed to BCryptOpenAlgorithmProvider
        HashAlgorithm = "SHA256",
        HashAlgorithmProvider = null
    });
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

CBC 모드 암호화 + HMAC 유효성 검사를 사용하는 사용자 지정 Windows CNG 알고리즘을 지정하려면, 알고리즘 정보를 담고 있는 [CngCbcAuthenticatedEncryptionSettings](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.cngcbcauthenticatedencryptionsettings) 의 인스턴스를 생성합니다.

```csharp
services.AddDataProtection()
    .UseCustomCryptographicAlgorithms(
        new CngCbcAuthenticatedEncryptionSettings()
    {
        // Passed to BCryptOpenAlgorithmProvider
        EncryptionAlgorithm = "AES",
        EncryptionAlgorithmProvider = null,

        // Specified in bits
        EncryptionAlgorithmKeySize = 256,

        // Passed to BCryptOpenAlgorithmProvider
        HashAlgorithm = "SHA256",
        HashAlgorithmProvider = null
    });
```

---

> [!NOTE]
> 대칭형 블럭 암호화 알고리즘(Symmetric Block Cipher Algorithm)은 반드시 키 길이가 128 비트 이상이고 블럭 크키가 64 비트 이상이어야 하며, PKCS #7 패딩을 사용하는 CBC 모드 암호화를 지원해야 합니다. 해시 알고리즘은 다이제스트 크기가 128 비트 이상이어야 하고, BCRYPT\_ALG\_HANDLE\_HMAC\_FLAG 플래그로 시작할 수 있도록 지원해야 합니다. \*Provider 속성들을 null로 설정해서 지정된 알고리즘에 대한 기본 공급자를 사용할 수 있습니다. 보다 자세한 정보는 [BCryptOpenAlgorithmProvider](https://msdn.microsoft.com/library/windows/desktop/aa375479(v=vs.85).aspx) 를 참고하시기 바랍니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

갈루아(Galois)/카운터 모드 암호화 + 유효성 검사를 사용하는 사용자 지정 Windows CNG 알고리즘을 지정하려면, 알고리즘 정보를 담고 있는 [CngGcmAuthenticatedEncryptorConfiguration](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.configurationmodel.cnggcmauthenticatedencryptorconfiguration) 의 인스턴스를 생성합니다.

```csharp
services.AddDataProtection()
    .UseCustomCryptographicAlgorithms(
        new CngGcmAuthenticatedEncryptorConfiguration()
    {
        // Passed to BCryptOpenAlgorithmProvider
        EncryptionAlgorithm = "AES",
        EncryptionAlgorithmProvider = null,

        // Specified in bits
        EncryptionAlgorithmKeySize = 256
    });
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

갈루아(Galois)/카운터 모드 암호화 + 유효성 검사를 사용하는 사용자 지정 Windows CNG 알고리즘을 지정하려면, 알고리즘 정보를 담고 있는 [CngGcmAuthenticatedEncryptionSettings](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.cnggcmauthenticatedencryptionsettings) 의 인스턴스를 생성합니다.

```csharp
services.AddDataProtection()
    .UseCustomCryptographicAlgorithms(
        new CngGcmAuthenticatedEncryptionSettings()
    {
        // Passed to BCryptOpenAlgorithmProvider
        EncryptionAlgorithm = "AES",
        EncryptionAlgorithmProvider = null,

        // Specified in bits
        EncryptionAlgorithmKeySize = 256
    });
```

---

> [!NOTE]
> 대칭형 블럭 암호화 알고리즘(Symmetric Block Cipher Algorithm)은 반드시 키 길이가 128 비트 이상이고 블럭 크키가 정확히 128 비트여야 하며, GCM 암호화를 지원해야 합니다. [EncryptionAlgorithmProvider](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.configurationmodel.cngcbcauthenticatedencryptorconfiguration.encryptionalgorithmprovider) 속성을 null로 설정해서 지정된 알고리즘에 대한 기본 공급자를 사용할 수 있습니다. 보다 자세한 정보는 [BCryptOpenAlgorithmProvider](https://msdn.microsoft.com/library/windows/desktop/aa375479(v=vs.85).aspx) 를 참고하시기 바랍니다.

### <a name="specifying-other-custom-algorithms"></a>다른 사용자 지정 알고리즘 지정하기

기본적인 API로 제공되지는 않지만 데이터 보호 시스템은 거의 모든 유형의 알고리즘을 지정할 수 있도록 충분한 확장이 가능합니다. 예를 들어서, 하드웨어 보안 모듈 (HSM) 내에 포함된 모든 키들을 유지하고, 핵심 암호화 및 복호화 루틴의 사용자 지정 구현을 제공하는 것도 가능합니다. 보다 자세한 정보는 [핵심 암호화 확장성(Core Cryptography Extensibility)](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.iauthenticatedencryptor)의 [IAuthenticatedEncryptor](xref:security/data-protection/extensibility/core-crypto) 절을 참고하시기 바랍니다.

## <a name="persisting-keys-when-hosting-in-a-docker-container"></a>Docker 컨테이너에서 호스팅할 때 키 유지하기

[Docker](/dotnet/standard/microservices-architecture/container-docker-introduction/) 컨테이너에서 호스팅할 경우, 다음 중 한 곳에 키를 저장해야 합니다.

* 공유 볼륨이나 호스트 탑재 볼륨 같이 컨테이너의 수명과 무관하게 유지되는 Docker 볼륨의 폴더
* [Azure 키 자격 증명 모음](https://azure.microsoft.com/services/key-vault/) 또는 [Redis](https://redis.io/)와 같은 외부 공급자

## <a name="see-also"></a>참고자료

* [비 DI 인식 시나리오](xref:security/data-protection/configuration/non-di-scenarios)
* [컴퓨터 수준 정책](xref:security/data-protection/configuration/machine-wide-policy)
