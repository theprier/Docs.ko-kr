---
title: "미사용 데이터 암호화 키"
author: rick-anderson
description: "이 문서에는 ASP.NET Core 데이터 보호 키 암호화의 구현 세부 사항을 설명합니다."
manager: wpickett
ms.author: riande
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/data-protection/implementation/key-encryption-at-rest
ms.openlocfilehash: c66430bfe547cf061e9e79a703ac665a968bbe0b
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="key-encryption-at-rest"></a><span data-ttu-id="4a321-103">미사용 데이터 암호화 키</span><span class="sxs-lookup"><span data-stu-id="4a321-103">Key Encryption At Rest</span></span>

<a name="data-protection-implementation-key-encryption-at-rest"></a>

<span data-ttu-id="4a321-104">기본적으로 데이터 보호 시스템 [경험적 접근을 사용](xref:security/data-protection/configuration/default-settings) 어떻게 암호화 키 자료를 확인 하려면 휴지 암호화 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a321-104">By default, the data protection system [employs a heuristic](xref:security/data-protection/configuration/default-settings) to determine how cryptographic key material should be encrypted at rest.</span></span> <span data-ttu-id="4a321-105">개발자는 추론은 무시 하 고 수동으로 키를 미사용 암호화 해야 하는 방법을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a321-105">The developer can override the heuristic and manually specify how keys should be encrypted at rest.</span></span>

> [!NOTE]
> <span data-ttu-id="4a321-106">나머지 메커니즘에는 명시적 키 암호화를 지정 하는 경우 데이터 보호 시스템의 추론은 제공 하는 기본 키 저장소 메커니즘 등록을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a321-106">If you specify an explicit key encryption at rest mechanism, the data protection system will deregister the default key storage mechanism that the heuristic provided.</span></span> <span data-ttu-id="4a321-107">수행 해야 [명시적 키 저장소 메커니즘을 지정](key-storage-providers.md#data-protection-implementation-key-storage-providers), 그렇지 않으면 데이터 보호 시스템 시작에 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a321-107">You must [specify an explicit key storage mechanism](key-storage-providers.md#data-protection-implementation-key-storage-providers), otherwise the data protection system will fail to start.</span></span>

<a name="data-protection-implementation-key-encryption-at-rest-providers"></a>

<span data-ttu-id="4a321-108">데이터 보호 시스템 세 가지 기본 키 암호화 메커니즘 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a321-108">The data protection system ships with three in-box key encryption mechanisms.</span></span>

## <a name="windows-dpapi"></a><span data-ttu-id="4a321-109">Windows DPAPI</span><span class="sxs-lookup"><span data-stu-id="4a321-109">Windows DPAPI</span></span>

<span data-ttu-id="4a321-110">*이 메커니즘은 Windows 에서만 사용할 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="4a321-110">*This mechanism is available only on Windows.*</span></span>

<span data-ttu-id="4a321-111">통해 Windows DPAPI를 사용 하면 키 자료를 암호화할 [cryptprotectdata가](https://msdn.microsoft.com/library/windows/desktop/aa380261(v=vs.85).aspx) 전에 저장소에 유지 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a321-111">When Windows DPAPI is used, key material will be encrypted via [CryptProtectData](https://msdn.microsoft.com/library/windows/desktop/aa380261(v=vs.85).aspx) before being persisted to storage.</span></span> <span data-ttu-id="4a321-112">DPAPI는 현재 시스템 외부에서 되지 읽을 수 있는 데이터에 대 한 적절 한 암호화 메커니즘 (Active Directory까지 이러한 키를 백업할 수는; 참조 하지만 [DPAPI 및 로밍 프로필](https://support.microsoft.com/kb/309408/#6)).</span><span class="sxs-lookup"><span data-stu-id="4a321-112">DPAPI is an appropriate encryption mechanism for data that will never be read outside of the current machine (though it's possible to back these keys up to Active Directory; see [DPAPI and Roaming Profiles](https://support.microsoft.com/kb/309408/#6)).</span></span> <span data-ttu-id="4a321-113">예를 DPAPI 키 휴지 암호화를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a321-113">For example to configure DPAPI key-at-rest encryption.</span></span>

```csharp
sc.AddDataProtection()
    // only the local user account can decrypt the keys
    .ProtectKeysWithDpapi();
```

<span data-ttu-id="4a321-114">경우 `ProtectKeysWithDpapi` 현재 Windows 사용자 계정이 지속형된 키 자료를 해독할 수 있습니다만 매개 변수 없이 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a321-114">If `ProtectKeysWithDpapi` is called with no parameters, only the current Windows user account can decipher the persisted key material.</span></span> <span data-ttu-id="4a321-115">컴퓨터 (뿐 아니라 현재 사용자 계정)의 모든 사용자 계정이 되도록 키 자료를 해독할 수와 같이 필요에 따라 지정할 수 있습니다는 아래 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="4a321-115">You can optionally specify that any user account on the machine (not just the current user account) should be able to decipher the key material, as shown in the below example.</span></span>

```csharp
sc.AddDataProtection()
    // all user accounts on the machine can decrypt the keys
    .ProtectKeysWithDpapi(protectToLocalMachine: true);
```

## <a name="x509-certificate"></a><span data-ttu-id="4a321-116">X.509 인증서</span><span class="sxs-lookup"><span data-stu-id="4a321-116">X.509 certificate</span></span>

<span data-ttu-id="4a321-117">*이 메커니즘에서 사용할 수 없습니다. `.NET Core 1.0` 또는 `1.1`합니다.*</span><span class="sxs-lookup"><span data-stu-id="4a321-117">*This mechanism isn't available on `.NET Core 1.0` or `1.1`.*</span></span>

<span data-ttu-id="4a321-118">여러 컴퓨터 간에 분산 되는 응용 프로그램 편리한 컴퓨터 간에 공유 하는 X.509 인증서를 배포 하 고 미사용 키의 암호화에 대 한이 인증서를 사용 하려면 응용 프로그램을 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a321-118">If your application is spread across multiple machines, it may be convenient to distribute a shared X.509 certificate across the machines and to configure applications to use this certificate for encryption of keys at rest.</span></span> <span data-ttu-id="4a321-119">예를 보려면 아래를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="4a321-119">See below for an example.</span></span>

```csharp
sc.AddDataProtection()
    // searches the cert store for the cert with this thumbprint
    .ProtectKeysWithCertificate("3BCE558E2AD3E0E34A7743EAB5AEA2A9BD2575A0");
```

<span data-ttu-id="4a321-120">.NET Framework 제한으로 인해 CAPI 개인 키가 있는 인증서만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a321-120">Due to .NET Framework limitations only certificates with CAPI private keys are supported.</span></span> <span data-ttu-id="4a321-121">참조 [인증서 기반 암호화와 Windows DPAPI-NG](#data-protection-implementation-key-encryption-at-rest-dpapi-ng) 아래 가능한 해결 방법에 이러한 제한 사항에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a321-121">See [Certificate-based encryption with Windows DPAPI-NG](#data-protection-implementation-key-encryption-at-rest-dpapi-ng) below for possible workarounds to these limitations.</span></span>

<a name="data-protection-implementation-key-encryption-at-rest-dpapi-ng"></a>

## <a name="windows-dpapi-ng"></a><span data-ttu-id="4a321-122">Windows DPAPI NG</span><span class="sxs-lookup"><span data-stu-id="4a321-122">Windows DPAPI-NG</span></span>

<span data-ttu-id="4a321-123">*이 메커니즘은 Windows 8에만 사용할 수 있는 / Windows Server 2012 이상.*</span><span class="sxs-lookup"><span data-stu-id="4a321-123">*This mechanism is available only on Windows 8 / Windows Server 2012 and later.*</span></span>

<span data-ttu-id="4a321-124">Windows 8 부터는 운영 체제 DPAPI NG (CNG DPAPI 라고도 함)를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a321-124">Beginning with Windows 8, the operating system supports DPAPI-NG (also called CNG DPAPI).</span></span> <span data-ttu-id="4a321-125">Microsoft 사용 시나리오는 다음과 같이 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="4a321-125">Microsoft lays out its usage scenario as follows.</span></span>

   <span data-ttu-id="4a321-126">그러나 클라우드 컴퓨팅 종종 해야 해당 콘텐츠를 암호화 된 컴퓨터에 다른 암호를 해독할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a321-126">Cloud computing, however, often requires that content encrypted on one computer be decrypted on another.</span></span> <span data-ttu-id="4a321-127">따라서 Windows 8 부터는 Microsoft 확장 된 클라우드 시나리오를 포함 하는 비교적 간단 하므로 API를 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4a321-127">Therefore, beginning with Windows 8, Microsoft extended the idea of using a relatively straightforward API to encompass cloud scenarios.</span></span> <span data-ttu-id="4a321-128">DPAPI-NG 라는이 새로운 API를 사용 하는 서로 다른 컴퓨터에 적절 한 인증 및 권한 부여 후 해제 하는 데 사용할 수 있는 보안 주체 집합에이 보호 하 여 비밀 (키, 암호, 키 자료) 및 메시지를 안전 하 게 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a321-128">This new API, called DPAPI-NG, enables you to securely share secrets (keys, passwords, key material) and messages by protecting them to a set of principals that can be used to unprotect them on different computers after proper authentication and authorization.</span></span>

   <span data-ttu-id="4a321-129">[CNG DPAPI에 대 한](https://msdn.microsoft.com/library/windows/desktop/hh706794(v=vs.85).aspx)</span><span class="sxs-lookup"><span data-stu-id="4a321-129">From [About CNG DPAPI](https://msdn.microsoft.com/library/windows/desktop/hh706794(v=vs.85).aspx)</span></span>

<span data-ttu-id="4a321-130">주 서버는 보호 설명자 규칙으로 인코딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a321-130">The principal is encoded as a protection descriptor rule.</span></span> <span data-ttu-id="4a321-131">고려는 아래 예제에서는 암호화 키 자료를 도메인에 가입 된 사용자만 지정 된 SID 가진 키 자료를 해독할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a321-131">Consider the below example, which encrypts key material such that only the domain-joined user with the specified SID can decrypt the key material.</span></span>

```csharp
sc.AddDataProtection()
    // uses the descriptor rule "SID=S-1-5-21-..."
    .ProtectKeysWithDpapiNG("SID=S-1-5-21-...",
    flags: DpapiNGProtectionDescriptorFlags.None);
```

<span data-ttu-id="4a321-132">매개 변수가 없는 오버 로드를 이기도 `ProtectKeysWithDpapiNG`합니다.</span><span class="sxs-lookup"><span data-stu-id="4a321-132">There's also a parameterless overload of `ProtectKeysWithDpapiNG`.</span></span> <span data-ttu-id="4a321-133">이 규칙을 지정 하기 위한 편리한 방법 "SID 마이닝 =" 여기서 내 것은 현재 Windows 사용자 계정의 SID.</span><span class="sxs-lookup"><span data-stu-id="4a321-133">This is a convenience method for specifying the rule "SID=mine", where mine is the SID of the current Windows user account.</span></span>

```csharp
sc.AddDataProtection()
    // uses the descriptor rule "SID={current account SID}"
    .ProtectKeysWithDpapiNG();
```

<span data-ttu-id="4a321-134">이 시나리오에서 AD 도메인 컨트롤러는 DPAPI NG 작업에 의해 사용 된 암호화 키를 배포 하는 일을 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a321-134">In this scenario, the AD domain controller is responsible for distributing the encryption keys used by the DPAPI-NG operations.</span></span> <span data-ttu-id="4a321-135">대상 사용자 (제공 하는 프로세스가 실행 되는 해당 id에서) 도메인에 가입 된 컴퓨터에서 암호화 된 페이로드를 해독할 수 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a321-135">The target user will be able to decipher the encrypted payload from any domain-joined machine (provided that the process is running under their identity).</span></span>

## <a name="certificate-based-encryption-with-windows-dpapi-ng"></a><span data-ttu-id="4a321-136">인증서 기반 암호화와 Windows DPAPI-NG</span><span class="sxs-lookup"><span data-stu-id="4a321-136">Certificate-based encryption with Windows DPAPI-NG</span></span>

<span data-ttu-id="4a321-137">Windows 8.1 실행 하는 경우 / Windows Server 2012 R2 이상 버전에서는 사용할 수 있습니다 Windows DPAPI NG 인증서 기반 암호화를 수행 하는 응용 프로그램에서 실행 중인 경우에 [.NET Core](https://www.microsoft.com/net/core)합니다.</span><span class="sxs-lookup"><span data-stu-id="4a321-137">If you're running on Windows 8.1 / Windows Server 2012 R2 or later, you can use Windows DPAPI-NG to perform certificate-based encryption, even if the application is running on [.NET Core](https://www.microsoft.com/net/core).</span></span> <span data-ttu-id="4a321-138">를 이용 하려면이 규칙 설명자 문자열을 사용 하 여 "인증서 HashId:thumbprint =" 지문을 사용 하는 인증서의 16 진수로 인코딩된 SHA1 지문을 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="4a321-138">To take advantage of this, use the rule descriptor string "CERTIFICATE=HashId:thumbprint", where thumbprint is the hex-encoded SHA1 thumbprint of the certificate to use.</span></span> <span data-ttu-id="4a321-139">예를 보려면 아래를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="4a321-139">See below for an example.</span></span>

```csharp
sc.AddDataProtection()
    // searches the cert store for the cert with this thumbprint
    .ProtectKeysWithDpapiNG("CERTIFICATE=HashId:3BCE558E2AD3E0E34A7743EAB5AEA2A9BD2575A0",
        flags: DpapiNGProtectionDescriptorFlags.None);
```

<span data-ttu-id="4a321-140">Windows 8.1이 리포지토리를 가리켜야 하는 응용 프로그램을 실행 해야 / Windows Server 2012 R2 또는 나중에이 키를 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a321-140">Any application which is pointed at this repository must be running on Windows 8.1 / Windows Server 2012 R2 or later to be able to decipher this key.</span></span>

## <a name="custom-key-encryption"></a><span data-ttu-id="4a321-141">사용자 지정 키 암호화</span><span class="sxs-lookup"><span data-stu-id="4a321-141">Custom key encryption</span></span>

<span data-ttu-id="4a321-142">개발자는 사용자 지정을 제공 하 여 고유 키 암호화 메커니즘을 지정할 수는 기본 메커니즘 적합 하지 않은 경우 `IXmlEncryptor`합니다.</span><span class="sxs-lookup"><span data-stu-id="4a321-142">If the in-box mechanisms are not appropriate, the developer can specify their own key encryption mechanism by providing a custom `IXmlEncryptor`.</span></span>
