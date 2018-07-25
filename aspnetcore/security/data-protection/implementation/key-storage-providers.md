---
title: ASP.NET Core에서 키 저장소 공급자
author: rick-anderson
description: ASP.NET Core 및 키 저장소 위치를 구성 하는 방법에 대 한 키 저장소 공급자에 알아봅니다.
ms.author: riande
ms.date: 07/16/2018
uid: security/data-protection/implementation/key-storage-providers
ms.openlocfilehash: 74d62e88b40cfcefb81d699a5aba2665c56ac51a
ms.sourcegitcommit: 8f8924ce4eb9effeaf489f177fb01b66867da16f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2018
ms.locfileid: "39219266"
---
# <a name="key-storage-providers-in-aspnet-core"></a><span data-ttu-id="2eeee-103">ASP.NET Core에서 키 저장소 공급자</span><span class="sxs-lookup"><span data-stu-id="2eeee-103">Key storage providers in ASP.NET Core</span></span>

<span data-ttu-id="2eeee-104">데이터 보호 시스템 [기본적으로 검색 메커니즘을 사용 하 여](xref:security/data-protection/configuration/default-settings) 에 암호화 키를 유지할지를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2eeee-104">The data protection system [employs a discovery mechanism by default](xref:security/data-protection/configuration/default-settings) to determine where cryptographic keys should be persisted.</span></span> <span data-ttu-id="2eeee-105">개발자는 기본 검색 메커니즘을 무시 하 고 수동으로 위치를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2eeee-105">The developer can override the default discovery mechanism and manually specify the location.</span></span>

> [!WARNING]
> <span data-ttu-id="2eeee-106">명시적 키 지 속성 위치를 지정 하는 경우 데이터 보호 시스템 키는 더 이상 휴지 상태로 암호화 되므로 rest 메커니즘을 기본 키 암호화를 등록 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="2eeee-106">If you specify an explicit key persistence location, the data protection system deregisters the default key encryption at rest mechanism, so keys are no longer encrypted at rest.</span></span> <span data-ttu-id="2eeee-107">하는 것이 좋습니다 있습니다 또한 [명시적 키 암호화 메커니즘을 지정](xref:security/data-protection/implementation/key-encryption-at-rest) 프로덕션 배포에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2eeee-107">It's recommended that you additionally [specify an explicit key encryption mechanism](xref:security/data-protection/implementation/key-encryption-at-rest) for production deployments.</span></span>

## <a name="file-system"></a><span data-ttu-id="2eeee-108">파일 시스템</span><span class="sxs-lookup"><span data-stu-id="2eeee-108">File system</span></span>

<span data-ttu-id="2eeee-109">파일 시스템 기반 키 저장소를 구성 하려면 다음을 호출 합니다 [PersistKeysToFileSystem](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystofilesystem) 아래와 같이 구성 루틴입니다.</span><span class="sxs-lookup"><span data-stu-id="2eeee-109">To configure a file system-based key repository, call the [PersistKeysToFileSystem](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystofilesystem) configuration routine as shown below.</span></span> <span data-ttu-id="2eeee-110">제공 된 [DirectoryInfo](/dotnet/api/system.io.directoryinfo) 키를 저장할 저장소를 가리키는:</span><span class="sxs-lookup"><span data-stu-id="2eeee-110">Provide a [DirectoryInfo](/dotnet/api/system.io.directoryinfo) pointing to the repository where keys should be stored:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .PersistKeysToFileSystem(new DirectoryInfo(@"c:\temp-keys\"));
}
```

<span data-ttu-id="2eeee-111">`DirectoryInfo` 로컬 컴퓨터의 디렉터리를 가리킬 수 있습니다 또는 네트워크 공유에 폴더를 가리킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2eeee-111">The `DirectoryInfo` can point to a directory on the local machine, or it can point to a folder on a network share.</span></span> <span data-ttu-id="2eeee-112">로컬 컴퓨터의 디렉터리를 가리키는 경우 (및 로컬 컴퓨터의 앱만이 리포지토리를 사용 하 여 액세스 해야 하는 시나리오는) 사용 하는 것이 좋습니다 [Windows DPAPI](xref:security/data-protection/implementation/key-encryption-at-rest) 미사용 키 암호화 (on Windows).</span><span class="sxs-lookup"><span data-stu-id="2eeee-112">If pointing to a directory on the local machine (and the scenario is that only apps on the local machine require access to use this repository), consider using [Windows DPAPI](xref:security/data-protection/implementation/key-encryption-at-rest) (on Windows) to encrypt the keys at rest.</span></span> <span data-ttu-id="2eeee-113">그렇지 않은 경우 사용 하는 것이 좋습니다는 [X.509 인증서](xref:security/data-protection/implementation/key-encryption-at-rest) 미사용 키를 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="2eeee-113">Otherwise, consider using an [X.509 certificate](xref:security/data-protection/implementation/key-encryption-at-rest) to encrypt keys at rest.</span></span>

## <a name="azure-and-redis"></a><span data-ttu-id="2eeee-114">Azure 및 Redis</span><span class="sxs-lookup"><span data-stu-id="2eeee-114">Azure and Redis</span></span>

<span data-ttu-id="2eeee-115">합니다 [Microsoft.AspNetCore.DataProtection.AzureStorage](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.AzureStorage/) 하 고 [Microsoft.AspNetCore.DataProtection.Redis](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.Redis/) 패키지를 사용 하면 Azure Storage 또는 Redis cache에서 데이터 보호 키를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2eeee-115">The [Microsoft.AspNetCore.DataProtection.AzureStorage](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.AzureStorage/) and [Microsoft.AspNetCore.DataProtection.Redis](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.Redis/) packages allow storing data protection keys in Azure Storage or a Redis cache.</span></span> <span data-ttu-id="2eeee-116">웹 앱의 여러 인스턴스 키를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2eeee-116">Keys can be shared across several instances of a web app.</span></span> <span data-ttu-id="2eeee-117">앱에는 여러 서버에서 인증 쿠키 또는 CSRF 보호 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2eeee-117">Apps can share authentication cookies or CSRF protection across multiple servers.</span></span> <span data-ttu-id="2eeee-118">Azure Blob 저장소 공급자를 구성 하려면 중 하나를 호출 합니다 [PersistKeysToAzureBlobStorage](/dotnet/api/microsoft.aspnetcore.dataprotection.azuredataprotectionbuilderextensions.persistkeystoazureblobstorage) 오버 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="2eeee-118">To configure the Azure Blob Storage provider, call one of the [PersistKeysToAzureBlobStorage](/dotnet/api/microsoft.aspnetcore.dataprotection.azuredataprotectionbuilderextensions.persistkeystoazureblobstorage) overloads:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .PersistKeysToAzureBlobStorage(new Uri("<blob URI including SAS token>"));
}
```

<span data-ttu-id="2eeee-119">Redis를 구성 하려면 중 하나를 호출 합니다 [PersistKeysToRedis](/dotnet/api/microsoft.aspnetcore.dataprotection.redisdataprotectionbuilderextensions.persistkeystoredis) 오버 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="2eeee-119">To configure on Redis, call one of the [PersistKeysToRedis](/dotnet/api/microsoft.aspnetcore.dataprotection.redisdataprotectionbuilderextensions.persistkeystoredis) overloads:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    var redis = ConnectionMultiplexer.Connect("<URI>");
    services.AddDataProtection()
        .PersistKeysToRedis(redis, "DataProtection-Keys");
}
```

<span data-ttu-id="2eeee-120">자세한 내용은 다음 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2eeee-120">For more information, see the following topics:</span></span>

* [<span data-ttu-id="2eeee-121">StackExchange.Redis ConnectionMultiplexer</span><span class="sxs-lookup"><span data-stu-id="2eeee-121">StackExchange.Redis ConnectionMultiplexer</span></span>](https://github.com/StackExchange/StackExchange.Redis/blob/master/docs/Basics.md)
* [<span data-ttu-id="2eeee-122">Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="2eeee-122">Azure Redis Cache</span></span>](/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache#connect-to-the-cache)
* [<span data-ttu-id="2eeee-123">aspnet/DataProtection 샘플</span><span class="sxs-lookup"><span data-stu-id="2eeee-123">aspnet/DataProtection samples</span></span>](https://github.com/aspnet/DataProtection/samples)

## <a name="registry"></a><span data-ttu-id="2eeee-124">레지스트리</span><span class="sxs-lookup"><span data-stu-id="2eeee-124">Registry</span></span>

<span data-ttu-id="2eeee-125">**Windows 배포에만 적용 됩니다.**</span><span class="sxs-lookup"><span data-stu-id="2eeee-125">**Only applies to Windows deployments.**</span></span>

<span data-ttu-id="2eeee-126">경우에 따라 앱 파일 시스템에 쓰기 액세스 하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2eeee-126">Sometimes the app might not have write access to the file system.</span></span> <span data-ttu-id="2eeee-127">가상 서비스 계정으로 앱 실행 되 고 있는 경우를 고려해 보십시오 (같은 *w3wp.exe*의 앱 풀 id)입니다.</span><span class="sxs-lookup"><span data-stu-id="2eeee-127">Consider a scenario where an app is running as a virtual service account (such as *w3wp.exe*'s app pool identity).</span></span> <span data-ttu-id="2eeee-128">이러한 경우 관리자 서비스 계정 id에서 액세스할 수 있는 레지스트리 키를 프로 비전 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2eeee-128">In these cases, the administrator can provision a registry key that's accessible by the service account identity.</span></span> <span data-ttu-id="2eeee-129">호출 된 [PersistKeysToRegistry](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystoregistry) 아래와 같이 확장 메서드.</span><span class="sxs-lookup"><span data-stu-id="2eeee-129">Call the [PersistKeysToRegistry](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystoregistry) extension method as shown below.</span></span> <span data-ttu-id="2eeee-130">제공 된 [RegistryKey](/dotnet/api/microsoft.aspnetcore.dataprotection.repositories.registryxmlrepository.registrykey) 암호화 키를 저장할 위치를 가리키는:</span><span class="sxs-lookup"><span data-stu-id="2eeee-130">Provide a [RegistryKey](/dotnet/api/microsoft.aspnetcore.dataprotection.repositories.registryxmlrepository.registrykey) pointing to the location where cryptographic keys should be stored:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .PersistKeysToRegistry(Registry.CurrentUser.OpenSubKey(@"SOFTWARE\Sample\keys"));
}
```

> [!IMPORTANT]
> <span data-ttu-id="2eeee-131">사용 하는 것이 좋습니다 [Windows DPAPI](xref:security/data-protection/implementation/key-encryption-at-rest) 미사용 키를 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="2eeee-131">We recommend using [Windows DPAPI](xref:security/data-protection/implementation/key-encryption-at-rest) to encrypt the keys at rest.</span></span>

## <a name="custom-key-repository"></a><span data-ttu-id="2eeee-132">사용자 지정 키 저장소</span><span class="sxs-lookup"><span data-stu-id="2eeee-132">Custom key repository</span></span>

<span data-ttu-id="2eeee-133">개발자가 사용자 지정을 제공 하 여 고유한 키 지 속성 메커니즘을 지정할 수 있습니다 기본 메커니즘은 적절 한가 없는 경우 [IXmlRepository](/dotnet/api/microsoft.aspnetcore.dataprotection.repositories.ixmlrepository)합니다.</span><span class="sxs-lookup"><span data-stu-id="2eeee-133">If the in-box mechanisms aren't appropriate, the developer can specify their own key persistence mechanism by providing a custom [IXmlRepository](/dotnet/api/microsoft.aspnetcore.dataprotection.repositories.ixmlrepository).</span></span>
