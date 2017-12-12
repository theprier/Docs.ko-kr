---
title: "ASP.NET Core에서 데이터 보호를 구성합니다."
author: rick-anderson
description: "ASP.NET Core에서 데이터 보호를 구성 하는 방법을 알아봅니다."
keywords: "ASP.NET Core, 데이터 보호, 구성"
ms.author: riande
manager: wpickett
ms.date: 07/17/2017
ms.topic: article
ms.assetid: 0e4881a3-a94d-4e35-9c1c-f025d65dcff0
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/data-protection/configuration/overview
ms.openlocfilehash: 4713c2bed04af784e74586daa10ec847262a1345
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
# <a name="configuring-data-protection-in-aspnet-core"></a>ASP.NET Core에서 데이터 보호를 구성합니다.

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)

데이터 보호 시스템 초기화 될 때 적용 [기본 설정](xref:security/data-protection/configuration/default-settings) 운영 환경에 따라 합니다. 이 설정은 일반적으로 단일 컴퓨터에서 실행 되는 앱에 적합 합니다. 개발자 이거나 준수 이유 여러 컴퓨터 간에 분산 되는 응용 프로그램 때문에 기본 설정을 아마도 변경 해야 할 수는 있는 경우가 많습니다. 이러한 시나리오에 대 한 데이터 보호 시스템 풍부한 구성 API를 제공합니다.

확장 메서드가 없는 [AddDataProtection](/dotnet/api/microsoft.extensions.dependencyinjection.dataprotectionservicecollectionextensions.adddataprotection) 반환 하는 [IDataProtectionBuilder](/dotnet/api/microsoft.aspnetcore.dataprotection.idataprotectionbuilder)합니다. `IDataProtectionBuilder`확장 메서드를 함께 결합할 수 데이터 보호를 구성 하려면 옵션을 표시 합니다.

## <a name="persistkeystofilesystem"></a>PersistKeysToFileSystem

키에서 대신 UNC 공유에 저장 하는 *% LOCALAPPDATA %* 기본 위치를 사용 하 여 시스템 구성 [PersistKeysToFileSystem](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystofilesystem):

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .PersistKeysToFileSystem(new DirectoryInfo(@"\\server\share\directory\"));
}
```

> [!WARNING]
> 지 속성 키 위치를 변경 하면 DPAPI는 적절 한 암호화 메커니즘 인지 알 수 없기 때문 시스템이 더 이상 자동으로 미사용 키를 암호화 합니다.

## <a name="protectkeyswith"></a>ProtectKeysWith\*

시스템을 미사용 키 중 하나를 호출 하 여 보호를 구성할 수는 [ProtectKeysWith\* ](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions) 구성 Api입니다. 아래 UNC 공유의 키를 저장 하 고 저장 된 상태의 특정 X.509 인증서와 해당 키를 암호화 하는 예를 살펴보십시오.

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .PersistKeysToFileSystem(new DirectoryInfo(@"\\server\share\directory\"))
        .ProtectKeysWithCertificate("thumbprint");
}
```

참조 [휴지 키 암호화](xref:security/data-protection/implementation/key-encryption-at-rest) 추가 예제 및 기본 제공 키 암호화 메커니즘에 대 한 토론에 대 한 합니다.

## <a name="setdefaultkeylifetime"></a>SetDefaultKeyLifetime

90 일 동안 14 일의 키 수명 기본값 대신 사용 하도록 시스템을 구성 하려면 사용 [SetDefaultKeyLifetime](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setdefaultkeylifetime):

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .SetDefaultKeyLifetime(TimeSpan.FromDays(14));
}
```

## <a name="setapplicationname"></a>SetApplicationName

기본적으로 데이터 보호 시스템 동일한 물리적 키 저장소를 공유 하는 경우에 서로에서 응용 프로그램을 격리 합니다. 이렇게 하면 앱을에서 다른 사용자의 보호 된 페이로드 이해지 않습니다. 두 앱 간에 보호 된 페이로드를 공유 하려면 사용 하 여 [SetApplicationName](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setapplicationname) 각 앱에 대 한 값:

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .SetApplicationName("shared app name");
}
```

## <a name="disableautomatickeygeneration"></a>DisableAutomaticKeyGeneration

앱이 자동으로 만료를 성능의 키 (새 키 만들기)을 롤 않도록 하려는 시나리오를 할 수 있습니다. 기본 응용 프로그램 키 관리 고려 사항에 대 한 책임이 보조 앱 하기만 키 링의 읽기 전용 보기를 주/보조 관계에서를 설정 하는 앱이 예로 들 수 있습니다. 보조 앱 키 링을 사용 하 여 시스템을 구성 하 여 읽기 전용으로 처리 하도록 구성할 수 있습니다 [DisableAutomaticKeyGeneration](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.disableautomatickeygeneration):

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .DisableAutomaticKeyGeneration();
}
```

## <a name="per-application-isolation"></a>응용 프로그램 격리

데이터 보호 시스템 ASP.NET Core 호스트에 의해 제공 되 면 문제가 응용 프로그램 같은 작업자 프로세스 계정에서 실행 되 고 동일한 마스터 키 자료를 사용 하는 경우에 서로의 앱을 자동으로 격리 합니다. 이 비슷합니다는 IsolateApps 한정자 System.Web의에서  **\<machineKey >** 요소입니다.

따라서 고유 테 넌 트로 로컬 컴퓨터에서 각 응용 프로그램을 고려 하 여 격리 메커니즘의 작동은 [IDataProtector](/dotnet/api/microsoft.aspnetcore.dataprotection.idataprotector) 판별자로 응용 프로그램 ID를 자동으로 포함 하는 지정 된 모든 앱에 대 한 루트입니다. 응용 프로그램의 고유 ID 두 위치 중 하나에서 나옵니다.

1. 응용 프로그램을 IIS에서 호스트 하는 경우 고유 식별자는 응용 프로그램의 구성 경로입니다. 응용 프로그램을 웹 팜 환경에 배포 하는 경우이 값은 웹 팜의 모든 컴퓨터에 IIS 환경 비슷하게 구성 이라고 가정할 안정적인 여야 합니다.

2. 응용 프로그램을 IIS에서 호스트 되지 않습니다. 하는 경우 고유 식별자는 앱의 실제 경로입니다.

고유 식별자 다시 설정 후에 유지 하도록 되어 &mdash; 개별 응용 프로그램 및 컴퓨터 자체입니다.

이 격리 메커니즘 앱 악성이 아닌지 가정 합니다. 악성 앱 동일한 작업자 프로세스 계정에서 실행 중인 다른 모든 앱에 항상 영향을 줄 수입니다. 응용 프로그램 상호 신뢰할 수 없는 공유 호스팅 환경에서 호스팅 공급자 간의 분리 앱의 기본 키 저장소를 포함 하 여 운영 체제 수준 격리를 보장 하는 단계를 수행 해야 합니다.

ASP.NET Core 호스트에서 데이터 보호 시스템 제공 되지 않습니다 (통해 인스턴스화하는 경우에 예를 들어는 `DataProtectionProvider` 구체적 형식)는 기본적으로 응용 프로그램 격리를 해제 합니다. 적절 한 제공으로 뒷받침 되며 동일한 키 자료는 모든 응용 프로그램 페이로드를 공유할 수 앱 격리가 비활성화 된 경우 [목적으로](xref:security/data-protection/consumer-apis/purpose-strings)합니다. 이 환경에서 응용 프로그램 격리를 제공 하려면 호출는 [SetApplicationName](#setapplicationname) 구성에 대 한 메서드 개체 및 각 응용 프로그램에 대 한 고유 이름을 제공 합니다.

## <a name="changing-algorithms-with-usecryptographicalgorithms"></a>UseCryptographicAlgorithms와 알고리즘을 변경합니다.

데이터 보호 스택의 사용 하면 새로 생성 된 키로 사용 되는 기본 알고리즘을 변경할 수 있습니다. 호출 하는 것이 작업을 수행 하는 가장 간단한 방법은 [UseCryptographicAlgorithms](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.usecryptographicalgorithms) 구성 콜백에서:

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

기본 EncryptionAlgorithm CBC AES 256-, 이며 기본 ValidationAlgorithm HMACSHA256 합니다. 기본 정책을 통해 시스템 관리자가 설정할 수 있습니다는 [시스템 수준의 정책](xref:security/data-protection/configuration/machine-wide-policy), 하지만를 명시적으로 호출 `UseCryptographicAlgorithms` 기본 정책 보다 우선 합니다.

호출 `UseCryptographicAlgorithms` 미리 정의 된 기본 제공 목록에서 원하는 알고리즘을 지정할 수 있습니다. 알고리즘의 구현에 대해 걱정할 필요가 없습니다. 위의 시나리오에서 데이터 보호 시스템에는 Windows에서 실행 되는 경우 AES의 CNG 구현을 사용 하 여 시도 합니다. 그렇지 않으면로 대체은 관리 되는 [System.Security.Cryptography.Aes](/dotnet/api/system.security.cryptography.aes) 클래스입니다.

호출을 통해 구현을 직접 지정할 수 있습니다 [UseCustomCryptographicAlgorithms](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.usecustomcryptographicalgorithms)합니다.

> [!TIP]
> 알고리즘 변경 키 링의 기존 키 영향을 주지 않습니다. 새로 생성 된 키를만 영향을 줍니다.

### <a name="specifying-custom-managed-algorithms"></a>관리 되는 사용자 지정 알고리즘을 지정

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

관리 되는 사용자 지정 알고리즘을 지정 하려면 만듭니다는 [ManagedAuthenticatedEncryptionSettings](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.managedauthenticatedencryptionsettings) 구현 형식을 가리키는 인스턴스:

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

일반적으로 \*형식 속성 콘크리트를 가리켜야 합니다. (공용 매개 변수가 없는 생성자)를 통해 인스턴스화할 수 있는 구현 [SymmetricAlgorithm](/dotnet/api/system.security.cryptography.symmetricalgorithm) 및 [KeyedHashAlgorithm](/dotnet/api/system.security.cryptography.keyedhashalgorithm)경우에 시스템 특수 한 경우와 같은 일부 값 `typeof(Aes)` 편의 위해.

> [!NOTE]
> `SymmetricAlgorithm` 의 키 길이 > = 128 비트의 블록 크기 > 64 비트 고 PKCS #7 안쪽 여백 사용 하 여 CBC 모드 암호화를 지원 해야 합니다. `KeyedHashAlgorithm` 다이제스트 크기인 있어야 합니다. > = 128 비트 키 길이 해시 알고리즘의 다이제스트 길이 지원 해야 하 고 있습니다. `KeyedHashAlgorithm` HMAC를 엄격 하 게 필요 하지 않습니다.
> ≥ 128 비트의 키 길이 및 ≥ 64 비트의 블록 크기는 SymmetricAlgorithm 있어야 하 고 PKCS #7 안쪽 여백 사용 하 여 CBC 모드 암호화를 지원 해야 합니다. KeyedHashAlgorithm 다이제스트 크기인 있어야 합니다. > = 128 비트 키 길이 해시 알고리즘의 다이제스트 길이 지원 해야 하 고 있습니다. KeyedHashAlgorithm HMAC를 엄격 하 게 필요 하지 않습니다.

### <a name="specifying-custom-windows-cng-algorithms"></a>사용자 지정 Windows CNG 알고리즘 지정

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

CBC 모드 암호화를 사용 하 여 HMAC 유효성 검사와 함께 사용자 지정 Windows CNG 알고리즘을 지정 하려면 만듭니다는 [CngCbcAuthenticatedEncryptorConfiguration](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.configurationmodel.cngcbcauthenticatedencryptorconfiguration) 알고리즘 정보를 포함 하는 인스턴스:

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

CBC 모드 암호화를 사용 하 여 HMAC 유효성 검사와 함께 사용자 지정 Windows CNG 알고리즘을 지정 하려면 만듭니다는 [CngCbcAuthenticatedEncryptionSettings](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.cngcbcauthenticatedencryptionsettings) 알고리즘 정보를 포함 하는 인스턴스:

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
> 블록 대칭 암호화 알고리즘의 키 길이 있어야 합니다. > = 128 비트의 블록 크기 > 64 비트 고 PKCS #7 안쪽 여백 사용 하 여 CBC 모드 암호화를 지원 해야 합니다. 해시 알고리즘의 다이제스트 크기 있어야 합니다. > = 128 비트 하 고는 BCRYPT 열린 지원 해야\_ALG\_처리\_HMAC\_플래그 플래그입니다. \*공급자 속성은 지정된 된 알고리즘에 대 한 기본 공급자를 사용 하려면 null로 설정할 수 있습니다. 참조는 [BCryptOpenAlgorithmProvider](https://msdn.microsoft.com/library/windows/desktop/aa375479(v=vs.85).aspx) 자세한 정보에 대 한 설명서입니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

유효성 검사와 Galois/카운터 모드 암호화를 사용 하 여 사용자 지정 Windows CNG 알고리즘을 지정 하려면 만듭니다는 [CngGcmAuthenticatedEncryptorConfiguration](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.configurationmodel.cnggcmauthenticatedencryptorconfiguration) 알고리즘 정보를 포함 하는 인스턴스:

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

유효성 검사와 Galois/카운터 모드 암호화를 사용 하 여 사용자 지정 Windows CNG 알고리즘을 지정 하려면 만듭니다는 [CngGcmAuthenticatedEncryptionSettings](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.cnggcmauthenticatedencryptionsettings) 알고리즘 정보를 포함 하는 인스턴스:

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
> 블록 대칭 암호화 알고리즘의 키 길이 있어야 합니다. > = 128 비트 정확히 128 비트의 블록 크기 및 GCM 암호화를 지원 해야 합니다. 설정할 수 있습니다는 [EncryptionAlgorithmProvider](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.configurationmodel.cngcbcauthenticatedencryptorconfiguration.encryptionalgorithmprovider) 속성을 null로 지정된 된 알고리즘에 대 한 기본 공급자를 사용 합니다. 참조는 [BCryptOpenAlgorithmProvider](https://msdn.microsoft.com/library/windows/desktop/aa375479(v=vs.85).aspx) 자세한 정보에 대 한 설명서입니다.

### <a name="specifying-other-custom-algorithms"></a>다른 사용자 지정 알고리즘을 지정

경우에 첫 번째 클래스 API로 노출 되지 데이터 보호 시스템은 거의 모든 종류의 알고리즘을 지정할 수 있을 만큼 확장 가능. 예를 들어 하드웨어 보안 모듈 (HSM) 내에 포함 된 모든 키를 유지 하 고 암호화 및 암호 해독 루틴의 핵심 사용자 지정 구현을 제공 됩니다. 참조 [IAuthenticatedEncryptor](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.iauthenticatedencryptor) 에 [암호화 확장성을 핵심](xref:security/data-protection/extensibility/core-crypto) 자세한 정보에 대 한 합니다.

## <a name="persisting-keys-when-hosting-in-a-docker-container"></a>Docker 컨테이너에서 호스팅하는 경우에 영구적 키

호스팅하는 경우는 [Docker](/dotnet/standard/microservices-architecture/container-docker-introduction/) 컨테이너에서 키를 유지 해야 합니다.

* 예: 공유 볼륨 또는 호스트 탑재 된 볼륨 컨테이너의 수명이 유지 되는 Docker 볼륨이 있는 폴더입니다.
* 외부 공급자와 같은 [Azure 키 자격 증명 모음](https://azure.microsoft.com/services/key-vault/) 또는 [Redis](https://redis.io/)합니다.

## <a name="see-also"></a>참고 항목

* [비 DI 인식 시나리오](xref:security/data-protection/configuration/non-di-scenarios)
* [컴퓨터 수준 정책](xref:security/data-protection/configuration/machine-wide-policy)
