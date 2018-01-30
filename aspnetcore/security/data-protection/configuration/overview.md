---
title: "ASP.NET Core에서 데이터 보호를 구성합니다."
author: rick-anderson
description: "ASP.NET Core에서 데이터 보호를 구성 하는 방법을 알아봅니다."
manager: wpickett
ms.author: riande
ms.date: 07/17/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/data-protection/configuration/overview
ms.openlocfilehash: 0fe1fd7b81a0e5aa00ae14c7e6fdbd9cc88ec4fe
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="configuring-data-protection-in-aspnet-core"></a><span data-ttu-id="87216-103">ASP.NET Core에서 데이터 보호를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="87216-103">Configuring Data Protection in ASP.NET Core</span></span>

<span data-ttu-id="87216-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="87216-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="87216-105">데이터 보호 시스템 초기화 될 때 적용 [기본 설정](xref:security/data-protection/configuration/default-settings) 운영 환경에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="87216-105">When the Data Protection system is initialized, it applies [default settings](xref:security/data-protection/configuration/default-settings) based on the operational environment.</span></span> <span data-ttu-id="87216-106">이 설정은 일반적으로 단일 컴퓨터에서 실행 되는 앱에 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="87216-106">These settings are generally appropriate for apps running on a single machine.</span></span> <span data-ttu-id="87216-107">개발자 이거나 준수 이유 여러 컴퓨터 간에 분산 되는 응용 프로그램 때문에 기본 설정을 아마도 변경 해야 할 수는 있는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="87216-107">There are cases where a developer may want to change the default settings, perhaps because their app is spread across multiple machines or for compliance reasons.</span></span> <span data-ttu-id="87216-108">이러한 시나리오에 대 한 데이터 보호 시스템 풍부한 구성 API를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="87216-108">For these scenarios, the Data Protection system offers a rich configuration API.</span></span>

<span data-ttu-id="87216-109">확장 메서드가 없는 [AddDataProtection](/dotnet/api/microsoft.extensions.dependencyinjection.dataprotectionservicecollectionextensions.adddataprotection) 반환 하는 [IDataProtectionBuilder](/dotnet/api/microsoft.aspnetcore.dataprotection.idataprotectionbuilder)합니다.</span><span class="sxs-lookup"><span data-stu-id="87216-109">There's an extension method [AddDataProtection](/dotnet/api/microsoft.extensions.dependencyinjection.dataprotectionservicecollectionextensions.adddataprotection) that returns an [IDataProtectionBuilder](/dotnet/api/microsoft.aspnetcore.dataprotection.idataprotectionbuilder).</span></span> <span data-ttu-id="87216-110">`IDataProtectionBuilder`확장 메서드를 함께 결합할 수 데이터 보호를 구성 하려면 옵션을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="87216-110">`IDataProtectionBuilder` exposes extension methods that you can chain together to configure Data Protection options.</span></span>

## <a name="persistkeystofilesystem"></a><span data-ttu-id="87216-111">PersistKeysToFileSystem</span><span class="sxs-lookup"><span data-stu-id="87216-111">PersistKeysToFileSystem</span></span>

<span data-ttu-id="87216-112">키에서 대신 UNC 공유에 저장 하는 *% LOCALAPPDATA %* 기본 위치를 사용 하 여 시스템 구성 [PersistKeysToFileSystem](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystofilesystem):</span><span class="sxs-lookup"><span data-stu-id="87216-112">To store keys on a UNC share instead of at the *%LOCALAPPDATA%* default location, configure the system with [PersistKeysToFileSystem](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystofilesystem):</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .PersistKeysToFileSystem(new DirectoryInfo(@"\\server\share\directory\"));
}
```

> [!WARNING]
> <span data-ttu-id="87216-113">지 속성 키 위치를 변경 하면 DPAPI는 적절 한 암호화 메커니즘 인지 알 수 없기 때문 시스템이 더 이상 자동으로 미사용 키를 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="87216-113">If you change the key persistence location, the system no longer automatically encrypts keys at rest, since it doesn't know whether DPAPI is an appropriate encryption mechanism.</span></span>

## <a name="protectkeyswith"></a><span data-ttu-id="87216-114">ProtectKeysWith\*</span><span class="sxs-lookup"><span data-stu-id="87216-114">ProtectKeysWith\*</span></span>

<span data-ttu-id="87216-115">시스템을 미사용 키 중 하나를 호출 하 여 보호를 구성할 수는 [ProtectKeysWith\* ](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions) 구성 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="87216-115">You can configure the system to protect keys at rest by calling any of the [ProtectKeysWith\*](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions) configuration APIs.</span></span> <span data-ttu-id="87216-116">아래 UNC 공유의 키를 저장 하 고 저장 된 상태의 특정 X.509 인증서와 해당 키를 암호화 하는 예를 살펴보십시오.</span><span class="sxs-lookup"><span data-stu-id="87216-116">Consider the example below, which stores keys on a UNC share and encrypts those keys at rest with a specific X.509 certificate:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .PersistKeysToFileSystem(new DirectoryInfo(@"\\server\share\directory\"))
        .ProtectKeysWithCertificate("thumbprint");
}
```

<span data-ttu-id="87216-117">참조 [휴지 키 암호화](xref:security/data-protection/implementation/key-encryption-at-rest) 추가 예제 및 기본 제공 키 암호화 메커니즘에 대 한 토론에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="87216-117">See [Key Encryption At Rest](xref:security/data-protection/implementation/key-encryption-at-rest) for more examples and discussion on the built-in key encryption mechanisms.</span></span>

## <a name="setdefaultkeylifetime"></a><span data-ttu-id="87216-118">SetDefaultKeyLifetime</span><span class="sxs-lookup"><span data-stu-id="87216-118">SetDefaultKeyLifetime</span></span>

<span data-ttu-id="87216-119">90 일 동안 14 일의 키 수명 기본값 대신 사용 하도록 시스템을 구성 하려면 사용 [SetDefaultKeyLifetime](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setdefaultkeylifetime):</span><span class="sxs-lookup"><span data-stu-id="87216-119">To configure the system to use a key lifetime of 14 days instead of the default 90 days, use [SetDefaultKeyLifetime](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setdefaultkeylifetime):</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .SetDefaultKeyLifetime(TimeSpan.FromDays(14));
}
```

## <a name="setapplicationname"></a><span data-ttu-id="87216-120">SetApplicationName</span><span class="sxs-lookup"><span data-stu-id="87216-120">SetApplicationName</span></span>

<span data-ttu-id="87216-121">기본적으로 데이터 보호 시스템 동일한 물리적 키 저장소를 공유 하는 경우에 서로에서 응용 프로그램을 격리 합니다.</span><span class="sxs-lookup"><span data-stu-id="87216-121">By default, the Data Protection system isolates apps from one another, even if they're sharing the same physical key repository.</span></span> <span data-ttu-id="87216-122">이렇게 하면 앱을에서 다른 사용자의 보호 된 페이로드 이해지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="87216-122">This prevents the apps from understanding each other's protected payloads.</span></span> <span data-ttu-id="87216-123">두 앱 간에 보호 된 페이로드를 공유 하려면 사용 하 여 [SetApplicationName](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setapplicationname) 각 앱에 대 한 값:</span><span class="sxs-lookup"><span data-stu-id="87216-123">To share protected payloads between two apps, use [SetApplicationName](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setapplicationname) with the same value for each app:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .SetApplicationName("shared app name");
}
```

## <a name="disableautomatickeygeneration"></a><span data-ttu-id="87216-124">DisableAutomaticKeyGeneration</span><span class="sxs-lookup"><span data-stu-id="87216-124">DisableAutomaticKeyGeneration</span></span>

<span data-ttu-id="87216-125">앱이 자동으로 만료를 성능의 키 (새 키 만들기)을 롤 않도록 하려는 시나리오를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87216-125">You may have a scenario where you don't want an app to automatically roll keys (create new keys) as they approach expiration.</span></span> <span data-ttu-id="87216-126">기본 응용 프로그램 키 관리 고려 사항에 대 한 책임이 보조 앱 하기만 키 링의 읽기 전용 보기를 주/보조 관계에서를 설정 하는 앱이 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87216-126">One example of this might be apps set up in a primary/secondary relationship, where only the primary app is responsible for key management concerns and secondary apps simply have a read-only view of the key ring.</span></span> <span data-ttu-id="87216-127">보조 앱 키 링을 사용 하 여 시스템을 구성 하 여 읽기 전용으로 처리 하도록 구성할 수 있습니다 [DisableAutomaticKeyGeneration](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.disableautomatickeygeneration):</span><span class="sxs-lookup"><span data-stu-id="87216-127">The secondary apps can be configured to treat the key ring as read-only by configuring the system with [DisableAutomaticKeyGeneration](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.disableautomatickeygeneration):</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .DisableAutomaticKeyGeneration();
}
```

## <a name="per-application-isolation"></a><span data-ttu-id="87216-128">응용 프로그램 격리</span><span class="sxs-lookup"><span data-stu-id="87216-128">Per-application isolation</span></span>

<span data-ttu-id="87216-129">데이터 보호 시스템 ASP.NET Core 호스트에 의해 제공 되 면 문제가 응용 프로그램 같은 작업자 프로세스 계정에서 실행 되 고 동일한 마스터 키 자료를 사용 하는 경우에 서로의 앱을 자동으로 격리 합니다.</span><span class="sxs-lookup"><span data-stu-id="87216-129">When the Data Protection system is provided by an ASP.NET Core host, it automatically isolates apps from one another, even if those apps are running under the same worker process account and are using the same master keying material.</span></span> <span data-ttu-id="87216-130">이 비슷합니다는 IsolateApps 한정자 System.Web의에서  **\<machineKey >** 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="87216-130">This is somewhat similar to the IsolateApps modifier from System.Web's **\<machineKey>** element.</span></span>

<span data-ttu-id="87216-131">따라서 고유 테 넌 트로 로컬 컴퓨터에서 각 응용 프로그램을 고려 하 여 격리 메커니즘의 작동은 [IDataProtector](/dotnet/api/microsoft.aspnetcore.dataprotection.idataprotector) 판별자로 응용 프로그램 ID를 자동으로 포함 하는 지정 된 모든 앱에 대 한 루트입니다.</span><span class="sxs-lookup"><span data-stu-id="87216-131">The isolation mechanism works by considering each app on the local machine as a unique tenant, thus the [IDataProtector](/dotnet/api/microsoft.aspnetcore.dataprotection.idataprotector) rooted for any given app automatically includes the app ID as a discriminator.</span></span> <span data-ttu-id="87216-132">응용 프로그램의 고유 ID 두 위치 중 하나에서 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="87216-132">The app's unique ID comes from one of two places:</span></span>

1. <span data-ttu-id="87216-133">응용 프로그램을 IIS에서 호스트 하는 경우 고유 식별자는 응용 프로그램의 구성 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="87216-133">If the app is hosted in IIS, the unique identifier is the app's configuration path.</span></span> <span data-ttu-id="87216-134">응용 프로그램을 웹 팜 환경에 배포 하는 경우이 값은 웹 팜의 모든 컴퓨터에 IIS 환경 비슷하게 구성 이라고 가정할 안정적인 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87216-134">If an app is deployed in a web farm environment, this value should be stable assuming that the IIS environments are configured similarly across all machines in the web farm.</span></span>

2. <span data-ttu-id="87216-135">응용 프로그램을 IIS에서 호스트 되지 않습니다. 하는 경우 고유 식별자는 앱의 실제 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="87216-135">If the app isn't hosted in IIS, the unique identifier is the physical path of the app.</span></span>

<span data-ttu-id="87216-136">고유 식별자 다시 설정 후에 유지 하도록 되어 &mdash; 개별 응용 프로그램 및 컴퓨터 자체입니다.</span><span class="sxs-lookup"><span data-stu-id="87216-136">The unique identifier is designed to survive resets &mdash; both of the individual app and of the machine itself.</span></span>

<span data-ttu-id="87216-137">이 격리 메커니즘 앱 악성이 아닌지 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="87216-137">This isolation mechanism assumes that the apps are not malicious.</span></span> <span data-ttu-id="87216-138">악성 앱 동일한 작업자 프로세스 계정에서 실행 중인 다른 모든 앱에 항상 영향을 줄 수입니다.</span><span class="sxs-lookup"><span data-stu-id="87216-138">A malicious app can always impact any other app running under the same worker process account.</span></span> <span data-ttu-id="87216-139">응용 프로그램 상호 신뢰할 수 없는 공유 호스팅 환경에서 호스팅 공급자 간의 분리 앱의 기본 키 저장소를 포함 하 여 운영 체제 수준 격리를 보장 하는 단계를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87216-139">In a shared hosting environment where apps are mutually untrusted, the hosting provider should take steps to ensure OS-level isolation between apps, including separating the apps' underlying key repositories.</span></span>

<span data-ttu-id="87216-140">ASP.NET Core 호스트에서 데이터 보호 시스템 제공 되지 않습니다 (통해 인스턴스화하는 경우에 예를 들어는 `DataProtectionProvider` 구체적 형식)는 기본적으로 응용 프로그램 격리를 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="87216-140">If the Data Protection system isn't provided by an ASP.NET Core host (for example, if you instantiate it via the `DataProtectionProvider` concrete type) app isolation is disabled by default.</span></span> <span data-ttu-id="87216-141">적절 한 제공으로 뒷받침 되며 동일한 키 자료는 모든 응용 프로그램 페이로드를 공유할 수 앱 격리가 비활성화 된 경우 [목적으로](xref:security/data-protection/consumer-apis/purpose-strings)합니다.</span><span class="sxs-lookup"><span data-stu-id="87216-141">When app isolation is disabled, all apps backed by the same keying material can share payloads as long as they provide the appropriate [purposes](xref:security/data-protection/consumer-apis/purpose-strings).</span></span> <span data-ttu-id="87216-142">이 환경에서 응용 프로그램 격리를 제공 하려면 호출는 [SetApplicationName](#setapplicationname) 구성에 대 한 메서드 개체 및 각 응용 프로그램에 대 한 고유 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="87216-142">To provide app isolation in this environment, call the [SetApplicationName](#setapplicationname) method on the configuration object and provide a unique name for each app.</span></span>

## <a name="changing-algorithms-with-usecryptographicalgorithms"></a><span data-ttu-id="87216-143">UseCryptographicAlgorithms와 알고리즘을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="87216-143">Changing algorithms with UseCryptographicAlgorithms</span></span>

<span data-ttu-id="87216-144">데이터 보호 스택의 사용 하면 새로 생성 된 키로 사용 되는 기본 알고리즘을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87216-144">The Data Protection stack allows you to change the default algorithm used by newly-generated keys.</span></span> <span data-ttu-id="87216-145">호출 하는 것이 작업을 수행 하는 가장 간단한 방법은 [UseCryptographicAlgorithms](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.usecryptographicalgorithms) 구성 콜백에서:</span><span class="sxs-lookup"><span data-stu-id="87216-145">The simplest way to do this is to call [UseCryptographicAlgorithms](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.usecryptographicalgorithms) from the configuration callback:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="87216-146">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="87216-146">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
services.AddDataProtection()
    .UseCryptographicAlgorithms(
        new AuthenticatedEncryptorConfiguration()
    {
        EncryptionAlgorithm = EncryptionAlgorithm.AES_256_CBC,
        ValidationAlgorithm = ValidationAlgorithm.HMACSHA256
    });
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="87216-147">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="87216-147">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

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

<span data-ttu-id="87216-148">기본 EncryptionAlgorithm CBC AES 256-, 이며 기본 ValidationAlgorithm HMACSHA256 합니다.</span><span class="sxs-lookup"><span data-stu-id="87216-148">The default EncryptionAlgorithm is AES-256-CBC, and the default ValidationAlgorithm is HMACSHA256.</span></span> <span data-ttu-id="87216-149">기본 정책을 통해 시스템 관리자가 설정할 수 있습니다는 [시스템 수준의 정책](xref:security/data-protection/configuration/machine-wide-policy), 하지만를 명시적으로 호출 `UseCryptographicAlgorithms` 기본 정책 보다 우선 합니다.</span><span class="sxs-lookup"><span data-stu-id="87216-149">The default policy can be set by a system administrator via a [machine-wide policy](xref:security/data-protection/configuration/machine-wide-policy), but an explicit call to `UseCryptographicAlgorithms` overrides the default policy.</span></span>

<span data-ttu-id="87216-150">호출 `UseCryptographicAlgorithms` 미리 정의 된 기본 제공 목록에서 원하는 알고리즘을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87216-150">Calling `UseCryptographicAlgorithms` allows you to specify the desired algorithm from a predefined built-in list.</span></span> <span data-ttu-id="87216-151">알고리즘의 구현에 대해 걱정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="87216-151">You don't need to worry about the implementation of the algorithm.</span></span> <span data-ttu-id="87216-152">위의 시나리오에서 데이터 보호 시스템에는 Windows에서 실행 되는 경우 AES의 CNG 구현을 사용 하 여 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="87216-152">In the scenario above, the Data Protection system attempts to use the CNG implementation of AES if running on Windows.</span></span> <span data-ttu-id="87216-153">그렇지 않으면로 대체은 관리 되는 [System.Security.Cryptography.Aes](/dotnet/api/system.security.cryptography.aes) 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="87216-153">Otherwise, it falls back to the managed [System.Security.Cryptography.Aes](/dotnet/api/system.security.cryptography.aes) class.</span></span>

<span data-ttu-id="87216-154">호출을 통해 구현을 직접 지정할 수 있습니다 [UseCustomCryptographicAlgorithms](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.usecustomcryptographicalgorithms)합니다.</span><span class="sxs-lookup"><span data-stu-id="87216-154">You can manually specify an implementation via a call to [UseCustomCryptographicAlgorithms](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.usecustomcryptographicalgorithms).</span></span>

> [!TIP]
> <span data-ttu-id="87216-155">알고리즘 변경 키 링의 기존 키 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="87216-155">Changing algorithms doesn't affect existing keys in the key ring.</span></span> <span data-ttu-id="87216-156">새로 생성 된 키를만 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="87216-156">It only affects newly-generated keys.</span></span>

### <a name="specifying-custom-managed-algorithms"></a><span data-ttu-id="87216-157">관리 되는 사용자 지정 알고리즘을 지정</span><span class="sxs-lookup"><span data-stu-id="87216-157">Specifying custom managed algorithms</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="87216-158">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="87216-158">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="87216-159">관리 되는 사용자 지정 알고리즘을 지정 하려면 만듭니다는 [ManagedAuthenticatedEncryptorConfiguration](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.configurationmodel.managedauthenticatedencryptorconfiguration) 구현 형식을 가리키는 인스턴스:</span><span class="sxs-lookup"><span data-stu-id="87216-159">To specify custom managed algorithms, create a [ManagedAuthenticatedEncryptorConfiguration](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.configurationmodel.managedauthenticatedencryptorconfiguration) instance that points to the implementation types:</span></span>

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

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="87216-160">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="87216-160">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="87216-161">관리 되는 사용자 지정 알고리즘을 지정 하려면 만듭니다는 [ManagedAuthenticatedEncryptionSettings](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.managedauthenticatedencryptionsettings) 구현 형식을 가리키는 인스턴스:</span><span class="sxs-lookup"><span data-stu-id="87216-161">To specify custom managed algorithms, create a [ManagedAuthenticatedEncryptionSettings](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.managedauthenticatedencryptionsettings) instance that points to the implementation types:</span></span>

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

<span data-ttu-id="87216-162">일반적으로 \*형식 속성 콘크리트를 가리켜야 합니다. (공용 매개 변수가 없는 생성자)를 통해 인스턴스화할 수 있는 구현 [SymmetricAlgorithm](/dotnet/api/system.security.cryptography.symmetricalgorithm) 및 [KeyedHashAlgorithm](/dotnet/api/system.security.cryptography.keyedhashalgorithm)경우에 시스템 특수 한 경우와 같은 일부 값 `typeof(Aes)` 편의 위해.</span><span class="sxs-lookup"><span data-stu-id="87216-162">Generally the \*Type properties must point to concrete, instantiable (via a public parameterless ctor) implementations of [SymmetricAlgorithm](/dotnet/api/system.security.cryptography.symmetricalgorithm) and [KeyedHashAlgorithm](/dotnet/api/system.security.cryptography.keyedhashalgorithm), though the system special-cases some values like `typeof(Aes)` for convenience.</span></span>

> [!NOTE]
> <span data-ttu-id="87216-163">≥ 128 비트의 키 길이 및 ≥ 64 비트의 블록 크기는 SymmetricAlgorithm 있어야 하 고 PKCS #7 안쪽 여백 사용 하 여 CBC 모드 암호화를 지원 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87216-163">The SymmetricAlgorithm must have a key length of ≥ 128 bits and a block size of ≥ 64 bits, and it must support CBC-mode encryption with PKCS #7 padding.</span></span> <span data-ttu-id="87216-164">KeyedHashAlgorithm 다이제스트 크기인 있어야 합니다. > = 128 비트 키 길이 해시 알고리즘의 다이제스트 길이 지원 해야 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87216-164">The KeyedHashAlgorithm must have a digest size of >= 128 bits, and it must support keys of length equal to the hash algorithm's digest length.</span></span> <span data-ttu-id="87216-165">KeyedHashAlgorithm 엄격 하 게 HMAC 될 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="87216-165">The KeyedHashAlgorithm isn't strictly required to be HMAC.</span></span>

### <a name="specifying-custom-windows-cng-algorithms"></a><span data-ttu-id="87216-166">사용자 지정 Windows CNG 알고리즘 지정</span><span class="sxs-lookup"><span data-stu-id="87216-166">Specifying custom Windows CNG algorithms</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="87216-167">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="87216-167">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="87216-168">CBC 모드 암호화를 사용 하 여 HMAC 유효성 검사와 함께 사용자 지정 Windows CNG 알고리즘을 지정 하려면 만듭니다는 [CngCbcAuthenticatedEncryptorConfiguration](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.configurationmodel.cngcbcauthenticatedencryptorconfiguration) 알고리즘 정보를 포함 하는 인스턴스:</span><span class="sxs-lookup"><span data-stu-id="87216-168">To specify a custom Windows CNG algorithm using CBC-mode encryption with HMAC validation, create a [CngCbcAuthenticatedEncryptorConfiguration](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.configurationmodel.cngcbcauthenticatedencryptorconfiguration) instance that contains the algorithmic information:</span></span>

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

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="87216-169">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="87216-169">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="87216-170">CBC 모드 암호화를 사용 하 여 HMAC 유효성 검사와 함께 사용자 지정 Windows CNG 알고리즘을 지정 하려면 만듭니다는 [CngCbcAuthenticatedEncryptionSettings](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.cngcbcauthenticatedencryptionsettings) 알고리즘 정보를 포함 하는 인스턴스:</span><span class="sxs-lookup"><span data-stu-id="87216-170">To specify a custom Windows CNG algorithm using CBC-mode encryption with HMAC validation, create a [CngCbcAuthenticatedEncryptionSettings](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.cngcbcauthenticatedencryptionsettings) instance that contains the algorithmic information:</span></span>

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
> <span data-ttu-id="87216-171">블록 대칭 암호화 알고리즘의 키 길이 있어야 합니다. > = 128 비트의 블록 크기 > 64 비트 고 PKCS #7 안쪽 여백 사용 하 여 CBC 모드 암호화를 지원 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87216-171">The symmetric block cipher algorithm must have a key length of >= 128 bits, a block size of >= 64 bits, and it must support CBC-mode encryption with PKCS #7 padding.</span></span> <span data-ttu-id="87216-172">해시 알고리즘의 다이제스트 크기 있어야 합니다. > = 128 비트 하 고는 BCRYPT 열린 지원 해야\_ALG\_처리\_HMAC\_플래그 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="87216-172">The hash algorithm must have a digest size of >= 128 bits and must support being opened with the BCRYPT\_ALG\_HANDLE\_HMAC\_FLAG flag.</span></span> <span data-ttu-id="87216-173">\*공급자 속성은 지정된 된 알고리즘에 대 한 기본 공급자를 사용 하려면 null로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87216-173">The \*Provider properties can be set to null to use the default provider for the specified algorithm.</span></span> <span data-ttu-id="87216-174">참조는 [BCryptOpenAlgorithmProvider](https://msdn.microsoft.com/library/windows/desktop/aa375479(v=vs.85).aspx) 자세한 정보에 대 한 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="87216-174">See the [BCryptOpenAlgorithmProvider](https://msdn.microsoft.com/library/windows/desktop/aa375479(v=vs.85).aspx) documentation for more information.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="87216-175">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="87216-175">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="87216-176">유효성 검사와 Galois/카운터 모드 암호화를 사용 하 여 사용자 지정 Windows CNG 알고리즘을 지정 하려면 만듭니다는 [CngGcmAuthenticatedEncryptorConfiguration](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.configurationmodel.cnggcmauthenticatedencryptorconfiguration) 알고리즘 정보를 포함 하는 인스턴스:</span><span class="sxs-lookup"><span data-stu-id="87216-176">To specify a custom Windows CNG algorithm using Galois/Counter Mode encryption with validation, create a [CngGcmAuthenticatedEncryptorConfiguration](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.configurationmodel.cnggcmauthenticatedencryptorconfiguration) instance that contains the algorithmic information:</span></span>

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

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="87216-177">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="87216-177">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="87216-178">유효성 검사와 Galois/카운터 모드 암호화를 사용 하 여 사용자 지정 Windows CNG 알고리즘을 지정 하려면 만듭니다는 [CngGcmAuthenticatedEncryptionSettings](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.cnggcmauthenticatedencryptionsettings) 알고리즘 정보를 포함 하는 인스턴스:</span><span class="sxs-lookup"><span data-stu-id="87216-178">To specify a custom Windows CNG algorithm using Galois/Counter Mode encryption with validation, create a [CngGcmAuthenticatedEncryptionSettings](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.cnggcmauthenticatedencryptionsettings) instance that contains the algorithmic information:</span></span>

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
> <span data-ttu-id="87216-179">블록 대칭 암호화 알고리즘의 키 길이 있어야 합니다. > = 128 비트 정확히 128 비트의 블록 크기 및 GCM 암호화를 지원 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87216-179">The symmetric block cipher algorithm must have a key length of >= 128 bits, a block size of exactly 128 bits, and it must support GCM encryption.</span></span> <span data-ttu-id="87216-180">설정할 수 있습니다는 [EncryptionAlgorithmProvider](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.configurationmodel.cngcbcauthenticatedencryptorconfiguration.encryptionalgorithmprovider) 속성을 null로 지정된 된 알고리즘에 대 한 기본 공급자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="87216-180">You can set the [EncryptionAlgorithmProvider](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.configurationmodel.cngcbcauthenticatedencryptorconfiguration.encryptionalgorithmprovider) property to null to use the default provider for the specified algorithm.</span></span> <span data-ttu-id="87216-181">참조는 [BCryptOpenAlgorithmProvider](https://msdn.microsoft.com/library/windows/desktop/aa375479(v=vs.85).aspx) 자세한 정보에 대 한 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="87216-181">See the [BCryptOpenAlgorithmProvider](https://msdn.microsoft.com/library/windows/desktop/aa375479(v=vs.85).aspx) documentation for more information.</span></span>

### <a name="specifying-other-custom-algorithms"></a><span data-ttu-id="87216-182">다른 사용자 지정 알고리즘을 지정</span><span class="sxs-lookup"><span data-stu-id="87216-182">Specifying other custom algorithms</span></span>

<span data-ttu-id="87216-183">경우에 첫 번째 클래스 API로 노출 되지 데이터 보호 시스템은 거의 모든 종류의 알고리즘을 지정할 수 있을 만큼 확장 가능.</span><span class="sxs-lookup"><span data-stu-id="87216-183">Though not exposed as a first-class API, the Data Protection system is extensible enough to allow specifying almost any kind of algorithm.</span></span> <span data-ttu-id="87216-184">예를 들어 하드웨어 보안 모듈 (HSM) 내에 포함 된 모든 키를 유지 하 고 암호화 및 암호 해독 루틴의 핵심 사용자 지정 구현을 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="87216-184">For example, it's possible to keep all keys contained within a Hardware Security Module (HSM) and to provide a custom implementation of the core encryption and decryption routines.</span></span> <span data-ttu-id="87216-185">참조 [IAuthenticatedEncryptor](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.iauthenticatedencryptor) 에 [암호화 확장성을 핵심](xref:security/data-protection/extensibility/core-crypto) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="87216-185">See [IAuthenticatedEncryptor](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.iauthenticatedencryptor) in [Core cryptography extensibility](xref:security/data-protection/extensibility/core-crypto) for more information.</span></span>

## <a name="persisting-keys-when-hosting-in-a-docker-container"></a><span data-ttu-id="87216-186">Docker 컨테이너에서 호스팅하는 경우에 영구적 키</span><span class="sxs-lookup"><span data-stu-id="87216-186">Persisting keys when hosting in a Docker container</span></span>

<span data-ttu-id="87216-187">호스팅하는 경우는 [Docker](/dotnet/standard/microservices-architecture/container-docker-introduction/) 컨테이너에서 키를 유지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87216-187">When hosting in a [Docker](/dotnet/standard/microservices-architecture/container-docker-introduction/) container, keys should be maintained in either:</span></span>

* <span data-ttu-id="87216-188">예: 공유 볼륨 또는 호스트 탑재 된 볼륨 컨테이너의 수명이 유지 되는 Docker 볼륨이 있는 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="87216-188">A folder that's a Docker volume that persists beyond the container's lifetime, such as a shared volume or a host-mounted volume.</span></span>
* <span data-ttu-id="87216-189">외부 공급자와 같은 [Azure 키 자격 증명 모음](https://azure.microsoft.com/services/key-vault/) 또는 [Redis](https://redis.io/)합니다.</span><span class="sxs-lookup"><span data-stu-id="87216-189">An external provider, such as [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) or [Redis](https://redis.io/).</span></span>

## <a name="see-also"></a><span data-ttu-id="87216-190">참고 항목</span><span class="sxs-lookup"><span data-stu-id="87216-190">See also</span></span>

* [<span data-ttu-id="87216-191">비 DI 인식 시나리오</span><span class="sxs-lookup"><span data-stu-id="87216-191">Non DI Aware Scenarios</span></span>](xref:security/data-protection/configuration/non-di-scenarios)
* [<span data-ttu-id="87216-192">컴퓨터 수준 정책</span><span class="sxs-lookup"><span data-stu-id="87216-192">Machine Wide Policy</span></span>](xref:security/data-protection/configuration/machine-wide-policy)
