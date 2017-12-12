---
title: "키 관리 확장성"
author: rick-anderson
description: "이 문서에서는 ASP.NET Core 데이터 보호 키 관리 확장성에 설명 합니다."
keywords: "ASP.NET Core, 데이터 보호, 키 관리"
ms.author: riande
manager: wpickett
ms.date: 11/22/2017
ms.topic: article
ms.assetid: 3606b251-8324-4485-8d52-582a2cd5cffb
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/data-protection/extensibility/key-management
ms.openlocfilehash: 0702e13163c0208e9d2863e711b02ffb257f6260
ms.sourcegitcommit: e641c5794525f983485621860926d8ab4e7360c8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/23/2017
---
# <a name="key-management-extensibility"></a><span data-ttu-id="9e835-104">키 관리 확장성</span><span class="sxs-lookup"><span data-stu-id="9e835-104">Key management extensibility</span></span>

<a name="data-protection-extensibility-key-management"></a>

>[!TIP]
> <span data-ttu-id="9e835-105">읽기는 [키 관리](../implementation/key-management.md#data-protection-implementation-key-management) 이러한 Api는 기본적인 개념 중 일부에 대해 설명 하는 대로이 섹션을 읽기 전에 섹션.</span><span class="sxs-lookup"><span data-stu-id="9e835-105">Read the [key management](../implementation/key-management.md#data-protection-implementation-key-management) section before reading this section, as it explains some of the fundamental concepts behind these APIs.</span></span>

>[!WARNING]
> <span data-ttu-id="9e835-106">다음 인터페이스 중 하나를 구현 하는 형식은 스레드로부터 안전 해야 합니다. 여러 호출자에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-106">Types that implement any of the following interfaces should be thread-safe for multiple callers.</span></span>

## <a name="key"></a><span data-ttu-id="9e835-107">Key</span><span class="sxs-lookup"><span data-stu-id="9e835-107">Key</span></span>

<span data-ttu-id="9e835-108">`IKey` 인터페이스 암호화 시스템에 있는 키의 기본 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-108">The `IKey` interface is the basic representation of a key in cryptosystem.</span></span> <span data-ttu-id="9e835-109">용어 키의 "암호화 키 자료" 리터럴 관점에 없는 추상적인 의미에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-109">The term key is used here in the abstract sense, not in the literal sense of "cryptographic key material".</span></span> <span data-ttu-id="9e835-110">키에 다음 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-110">A key has the following properties:</span></span>

* <span data-ttu-id="9e835-111">활성화, 생성 및 만료 날짜</span><span class="sxs-lookup"><span data-stu-id="9e835-111">Activation, creation, and expiration dates</span></span>

* <span data-ttu-id="9e835-112">해지 상태</span><span class="sxs-lookup"><span data-stu-id="9e835-112">Revocation status</span></span>

* <span data-ttu-id="9e835-113">키 식별자 (GUID)</span><span class="sxs-lookup"><span data-stu-id="9e835-113">Key identifier (a GUID)</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="9e835-114">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="9e835-114">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="9e835-115">또한 `IKey` 노출 한 `CreateEncryptor` 만드는 데 사용할 수 있는 메서드는 [IAuthenticatedEncryptor](core-crypto.md#data-protection-extensibility-core-crypto-iauthenticatedencryptor) 인스턴스가이 키에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-115">Additionally, `IKey` exposes a `CreateEncryptor` method which can be used to create an [IAuthenticatedEncryptor](core-crypto.md#data-protection-extensibility-core-crypto-iauthenticatedencryptor) instance tied to this key.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="9e835-116">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="9e835-116">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="9e835-117">또한 `IKey` 노출 한 `CreateEncryptorInstance` 만드는 데 사용할 수 있는 메서드는 [IAuthenticatedEncryptor](core-crypto.md#data-protection-extensibility-core-crypto-iauthenticatedencryptor) 인스턴스가이 키에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-117">Additionally, `IKey` exposes a `CreateEncryptorInstance` method which can be used to create an [IAuthenticatedEncryptor](core-crypto.md#data-protection-extensibility-core-crypto-iauthenticatedencryptor) instance tied to this key.</span></span>

---

> [!NOTE]
> <span data-ttu-id="9e835-118">API에서 원시 암호화 자료를 검색할 수는 없습니다는 `IKey` 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="9e835-118">There is no API to retrieve the raw cryptographic material from an `IKey` instance.</span></span>

## <a name="ikeymanager"></a><span data-ttu-id="9e835-119">IKeyManager</span><span class="sxs-lookup"><span data-stu-id="9e835-119">IKeyManager</span></span>

<span data-ttu-id="9e835-120">`IKeyManager` 인터페이스 일반 키 저장소, 검색 및 조작 하는 일을 담당 하는 개체를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-120">The `IKeyManager` interface represents an object responsible for general key storage, retrieval, and manipulation.</span></span> <span data-ttu-id="9e835-121">세 가지 상위 수준 작업을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-121">It exposes three high-level operations:</span></span>

* <span data-ttu-id="9e835-122">새 키를 만들고 저장소를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-122">Create a new key and persist it to storage.</span></span>

* <span data-ttu-id="9e835-123">저장소에서 모든 키를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-123">Get all keys from storage.</span></span>

* <span data-ttu-id="9e835-124">하나 이상의 키를 해지 하 고 저장소는 해지 정보를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-124">Revoke one or more keys and persist the revocation information to storage.</span></span>

>[!WARNING]
> <span data-ttu-id="9e835-125">작성 한 `IKeyManager` 는 고급 작업이 며 대부분의 개발자는 시도 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-125">Writing an `IKeyManager` is a very advanced task, and the majority of developers should not attempt it.</span></span> <span data-ttu-id="9e835-126">대신 대부분의 개발자가 제공 하는 기능 사용 해야는 [XmlKeyManager](xref:security/data-protection/extensibility/key-management#data-protection-extensibility-key-management-xmlkeymanager) 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-126">Instead, most developers should take advantage of the facilities offered by the [XmlKeyManager](xref:security/data-protection/extensibility/key-management#data-protection-extensibility-key-management-xmlkeymanager) class.</span></span>

<a name="data-protection-extensibility-key-management-xmlkeymanager"></a>

## <a name="xmlkeymanager"></a><span data-ttu-id="9e835-127">XmlKeyManager</span><span class="sxs-lookup"><span data-stu-id="9e835-127">XmlKeyManager</span></span>

<span data-ttu-id="9e835-128">`XmlKeyManager` 형식은의 기본 구체적인 구현 `IKeyManager`합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-128">The `XmlKeyManager` type is the in-box concrete implementation of `IKeyManager`.</span></span> <span data-ttu-id="9e835-129">키 위탁 및 대기 키의 암호화를 포함 하 여 몇 가지 유용한 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-129">It provides several useful facilities, including key escrow and encryption of keys at rest.</span></span> <span data-ttu-id="9e835-130">이 시스템에 있는 키 XML 요소로 표시 됩니다 (특히 [XElement](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/xelement-class-overview)).</span><span class="sxs-lookup"><span data-stu-id="9e835-130">Keys in this system are represented as XML elements (specifically, [XElement](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/xelement-class-overview)).</span></span>

<span data-ttu-id="9e835-131">`XmlKeyManager`해당 작업을 수행 하는 과정에서 다른 여러 가지 구성 요소에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-131">`XmlKeyManager` depends on several other components in the course of fulfilling its tasks:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="9e835-132">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="9e835-132">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

* <span data-ttu-id="9e835-133">`AlgorithmConfiguration`를 새 키로 사용 되는 알고리즘 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-133">`AlgorithmConfiguration`, which dictates the algorithms used by new keys.</span></span>

* <span data-ttu-id="9e835-134">`IXmlRepository`키 저장소에 유지 되는 위치를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-134">`IXmlRepository`, which controls where keys are persisted in storage.</span></span>

* <span data-ttu-id="9e835-135">`IXmlEncryptor`[옵션]을 허용 하는 저장 된 상태의 키를 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-135">`IXmlEncryptor` [optional], which allows encrypting keys at rest.</span></span>

* <span data-ttu-id="9e835-136">`IKeyEscrowSink`[선택 사항] 키 에스크로 서비스를 제공 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-136">`IKeyEscrowSink` [optional], which provides key escrow services.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="9e835-137">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="9e835-137">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

* <span data-ttu-id="9e835-138">`IXmlRepository`키 저장소에 유지 되는 위치를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-138">`IXmlRepository`, which controls where keys are persisted in storage.</span></span>

* <span data-ttu-id="9e835-139">`IXmlEncryptor`[옵션]을 허용 하는 저장 된 상태의 키를 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-139">`IXmlEncryptor` [optional], which allows encrypting keys at rest.</span></span>

* <span data-ttu-id="9e835-140">`IKeyEscrowSink`[선택 사항] 키 에스크로 서비스를 제공 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-140">`IKeyEscrowSink` [optional], which provides key escrow services.</span></span>

---

<span data-ttu-id="9e835-141">다음은 이러한 구성 요소 내에서 함께 연결 된 방식을 나타내는 개략적인 다이어그램 `XmlKeyManager`합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-141">Below are high-level diagrams which indicate how these components are wired together within `XmlKeyManager`.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="9e835-142">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="9e835-142">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

   ![키 만들기](key-management/_static/keycreation2.png)

   <span data-ttu-id="9e835-144">*키 생성 / CreateNewKey*</span><span class="sxs-lookup"><span data-stu-id="9e835-144">*Key Creation / CreateNewKey*</span></span>

<span data-ttu-id="9e835-145">구현에서 `CreateNewKey`, `AlgorithmConfiguration` 구성 요소는 고유한 만드는 데 사용 되 `IAuthenticatedEncryptorDescriptor`는 다음 XML로 serialize 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-145">In the implementation of `CreateNewKey`, the `AlgorithmConfiguration` component is used to create a unique `IAuthenticatedEncryptorDescriptor`, which is then serialized as XML.</span></span> <span data-ttu-id="9e835-146">키 에스크로 싱크가 있는 경우 원시 (암호화 되지 않은) XML 장기 저장에 대 한 싱크에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-146">If a key escrow sink is present, the raw (unencrypted) XML is provided to the sink for long-term storage.</span></span> <span data-ttu-id="9e835-147">그런 다음 암호화 되지 않은 XML를 실행 되는 `IXmlEncryptor` (필요한 경우)를 암호화 된 XML 문서를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-147">The unencrypted XML is then run through an `IXmlEncryptor` (if required) to generate the encrypted XML document.</span></span> <span data-ttu-id="9e835-148">이 암호화 된 문서를 통해 장기 저장소에 유지 되는 `IXmlRepository`합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-148">This encrypted document is persisted to long-term storage via the `IXmlRepository`.</span></span> <span data-ttu-id="9e835-149">(없는 경우 `IXmlEncryptor` 가 구성, 암호화 되지 않은 문서에서 유지 되는 `IXmlRepository`.)</span><span class="sxs-lookup"><span data-stu-id="9e835-149">(If no `IXmlEncryptor` is configured, the unencrypted document is persisted in the `IXmlRepository`.)</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="9e835-150">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="9e835-150">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

   ![키 만들기](key-management/_static/keycreation1.png)

   <span data-ttu-id="9e835-152">*키 생성 / CreateNewKey*</span><span class="sxs-lookup"><span data-stu-id="9e835-152">*Key Creation / CreateNewKey*</span></span>

<span data-ttu-id="9e835-153">구현에서 `CreateNewKey`, `IAuthenticatedEncryptorConfiguration` 구성 요소는 고유한 만드는 데 사용 되 `IAuthenticatedEncryptorDescriptor`는 다음 XML로 serialize 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-153">In the implementation of `CreateNewKey`, the `IAuthenticatedEncryptorConfiguration` component is used to create a unique `IAuthenticatedEncryptorDescriptor`, which is then serialized as XML.</span></span> <span data-ttu-id="9e835-154">키 에스크로 싱크가 있는 경우 원시 (암호화 되지 않은) XML 장기 저장에 대 한 싱크에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-154">If a key escrow sink is present, the raw (unencrypted) XML is provided to the sink for long-term storage.</span></span> <span data-ttu-id="9e835-155">그런 다음 암호화 되지 않은 XML를 실행 되는 `IXmlEncryptor` (필요한 경우)를 암호화 된 XML 문서를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-155">The unencrypted XML is then run through an `IXmlEncryptor` (if required) to generate the encrypted XML document.</span></span> <span data-ttu-id="9e835-156">이 암호화 된 문서를 통해 장기 저장소에 유지 되는 `IXmlRepository`합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-156">This encrypted document is persisted to long-term storage via the `IXmlRepository`.</span></span> <span data-ttu-id="9e835-157">(없는 경우 `IXmlEncryptor` 가 구성, 암호화 되지 않은 문서에서 유지 되는 `IXmlRepository`.)</span><span class="sxs-lookup"><span data-stu-id="9e835-157">(If no `IXmlEncryptor` is configured, the unencrypted document is persisted in the `IXmlRepository`.)</span></span>

---

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="9e835-158">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="9e835-158">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

   ![키 검색](key-management/_static/keyretrieval2.png)
   
# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="9e835-160">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="9e835-160">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

   ![키 검색](key-management/_static/keyretrieval1.png)

---

   <span data-ttu-id="9e835-162">*검색 키 / GetAllKeys*</span><span class="sxs-lookup"><span data-stu-id="9e835-162">*Key Retrieval / GetAllKeys*</span></span>

<span data-ttu-id="9e835-163">구현에서 `GetAllKeys`, XML 문서 나타내는 키 및 해지 내부에서 읽을 수 있으며 `IXmlRepository`합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-163">In the implementation of `GetAllKeys`, the XML documents representing keys and revocations are read from the underlying `IXmlRepository`.</span></span> <span data-ttu-id="9e835-164">이러한 문서를 암호화 하는 경우 시스템은 자동으로 암호 해독할 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-164">If these documents are encrypted, the system will automatically decrypt them.</span></span> <span data-ttu-id="9e835-165">`XmlKeyManager`적절 한 만듭니다 `IAuthenticatedEncryptorDescriptorDeserializer` 로 문서를 역직렬화 할 인스턴스를 다시 `IAuthenticatedEncryptorDescriptor` 개별에 래핑됩니다.이 다음에 인스턴스가 `IKey` 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="9e835-165">`XmlKeyManager` creates the appropriate `IAuthenticatedEncryptorDescriptorDeserializer` instances to deserialize the documents back into `IAuthenticatedEncryptorDescriptor` instances, which are then wrapped in individual `IKey` instances.</span></span> <span data-ttu-id="9e835-166">이 컬렉션의 `IKey` 인스턴스 호출자에 게 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-166">This collection of `IKey` instances is returned to the caller.</span></span>

<span data-ttu-id="9e835-167">특정 XML 요소에 대 한 자세한 정보를 찾을 수는 [키 저장소 형식 문서](../implementation/key-storage-format.md#data-protection-implementation-key-storage-format)합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-167">Further information on the particular XML elements can be found in the [key storage format document](../implementation/key-storage-format.md#data-protection-implementation-key-storage-format).</span></span>

## <a name="ixmlrepository"></a><span data-ttu-id="9e835-168">IXmlRepository</span><span class="sxs-lookup"><span data-stu-id="9e835-168">IXmlRepository</span></span>

<span data-ttu-id="9e835-169">`IXmlRepository` 인터페이스는 XML을 유지 하 고 백업 저장소에서 XML을 검색할 수 있는 형식을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-169">The `IXmlRepository` interface represents a type that can persist XML to and retrieve XML from a backing store.</span></span> <span data-ttu-id="9e835-170">두 개의 Api를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-170">It exposes two APIs:</span></span>

* <span data-ttu-id="9e835-171">GetAllElements(): IReadOnlyCollection<XElement></span><span class="sxs-lookup"><span data-stu-id="9e835-171">GetAllElements() : IReadOnlyCollection<XElement></span></span>

* <span data-ttu-id="9e835-172">StoreElement (XElement 요소, 문자열 friendlyName)</span><span class="sxs-lookup"><span data-stu-id="9e835-172">StoreElement(XElement element, string friendlyName)</span></span>

<span data-ttu-id="9e835-173">구현 `IXmlRepository` 을 통해 전달 되는 XML 구문 분석 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-173">Implementations of `IXmlRepository` don't need to parse the XML passing through them.</span></span> <span data-ttu-id="9e835-174">불투명으로 XML 문서 처리를 생성 하 고 문서를 구문 분석 하는 방법에 대 한 걱정 더 높은 계층을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-174">They should treat the XML documents as opaque and let higher layers worry about generating and parsing the documents.</span></span>

<span data-ttu-id="9e835-175">형식은 두 가지가 기본 제공 구체적 구현 하는 `IXmlRepository`: `FileSystemXmlRepository` 및 `RegistryXmlRepository`합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-175">There are two built-in concrete types which implement `IXmlRepository`: `FileSystemXmlRepository` and `RegistryXmlRepository`.</span></span> <span data-ttu-id="9e835-176">참조는 [키 저장소 공급자 문서](../implementation/key-storage-providers.md#data-protection-implementation-key-storage-providers) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-176">See the [key storage providers document](../implementation/key-storage-providers.md#data-protection-implementation-key-storage-providers) for more information.</span></span> <span data-ttu-id="9e835-177">사용자 지정 등록 `IXmlRepository` 는 적절 한 방법으로 예: 다른 지원 저장소를 사용 하도록 Azure Blob 저장소는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-177">Registering a custom `IXmlRepository` would be the appropriate manner to use a different backing store, e.g., Azure Blob Storage.</span></span>

<span data-ttu-id="9e835-178">기본 저장소 전체 응용 프로그램을 변경 하려면 사용자 지정 등록 `IXmlRepository` 인스턴스:</span><span class="sxs-lookup"><span data-stu-id="9e835-178">To change the default repository application-wide, register a custom `IXmlRepository` instance:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="9e835-179">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="9e835-179">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

   ```csharp
   services.Configure<KeyManagementOptions>(options => options.XmlRepository = new MyCustomXmlRepository());
   ```
   
# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="9e835-180">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="9e835-180">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

   ```csharp
   services.AddSingleton<IXmlRepository>(new MyCustomXmlRepository());
   ```

---

<a name="data-protection-extensibility-key-management-ixmlencryptor"></a>

## <a name="ixmlencryptor"></a><span data-ttu-id="9e835-181">IXmlEncryptor</span><span class="sxs-lookup"><span data-stu-id="9e835-181">IXmlEncryptor</span></span>

<span data-ttu-id="9e835-182">`IXmlEncryptor` 인터페이스는 일반 텍스트 XML 요소를 암호화할 수 있는 형식을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-182">The `IXmlEncryptor` interface represents a type that can encrypt a plaintext XML element.</span></span> <span data-ttu-id="9e835-183">단일 API를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-183">It exposes a single API:</span></span>

* <span data-ttu-id="9e835-184">(XElement plaintextElement) 암호화: EncryptedXmlInfo</span><span class="sxs-lookup"><span data-stu-id="9e835-184">Encrypt(XElement plaintextElement) : EncryptedXmlInfo</span></span>

<span data-ttu-id="9e835-185">serialize 된 경우 `IAuthenticatedEncryptorDescriptor` 다음 "암호화 필요"로 표시 하는 요소가 포함 된 `XmlKeyManager` 이러한 요소를 통해 구성 된 실행 됩니다 `IXmlEncryptor`의 `Encrypt` 가 유지할 서 암호화 요소 메서드를 보다는 일반 텍스트 요소를는 `IXmlRepository`합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-185">If a serialized `IAuthenticatedEncryptorDescriptor` contains any elements marked as "requires encryption", then `XmlKeyManager` will run those elements through the configured `IXmlEncryptor`'s `Encrypt` method, and it will persist the enciphered element rather than the plaintext element to the `IXmlRepository`.</span></span> <span data-ttu-id="9e835-186">출력은 `Encrypt` 방법은 `EncryptedXmlInfo` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-186">The output of the `Encrypt` method is an `EncryptedXmlInfo` object.</span></span> <span data-ttu-id="9e835-187">이 개체는 모두 결과 서 암호화를 포함 하는 래퍼 `XElement` 및 나타내는 유형에 `IXmlDecryptor` 해당 요소를 해독을 사용할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-187">This object is a wrapper which contains both the resultant enciphered `XElement` and the Type which represents an `IXmlDecryptor` which can be used to decipher the corresponding element.</span></span>

<span data-ttu-id="9e835-188">네 가지 기본 제공 구체적인 유형 구현 하는 `IXmlEncryptor`:</span><span class="sxs-lookup"><span data-stu-id="9e835-188">There are four built-in concrete types which implement `IXmlEncryptor`:</span></span>
* `CertificateXmlEncryptor`
* `DpapiNGXmlEncryptor`
* `DpapiXmlEncryptor`
* `NullXmlEncryptor`

<span data-ttu-id="9e835-189">참조는 [rest 문서에서 키 암호화](../implementation/key-encryption-at-rest.md#data-protection-implementation-key-encryption-at-rest) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-189">See the [key encryption at rest document](../implementation/key-encryption-at-rest.md#data-protection-implementation-key-encryption-at-rest) for more information.</span></span>

<span data-ttu-id="9e835-190">전체 응용 프로그램의 기본 휴지 키 암호화 메커니즘을 변경 하려면 사용자 지정 등록 `IXmlEncryptor` 인스턴스:</span><span class="sxs-lookup"><span data-stu-id="9e835-190">To change the default key-encryption-at-rest mechanism application-wide, register a custom `IXmlEncryptor` instance:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="9e835-191">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="9e835-191">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

   ```csharp
   services.Configure<KeyManagementOptions>(options => options.XmlEncryptor = new MyCustomXmlEncryptor());
   ```
   
# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="9e835-192">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="9e835-192">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

   ```csharp
   services.AddSingleton<IXmlEncryptor>(new MyCustomXmlEncryptor());
   ```

---

## <a name="ixmldecryptor"></a><span data-ttu-id="9e835-193">IXmlDecryptor</span><span class="sxs-lookup"><span data-stu-id="9e835-193">IXmlDecryptor</span></span>

<span data-ttu-id="9e835-194">`IXmlDecryptor` 인터페이스 해독 하는 방법을 알고 있는 형식을 나타냅니다는 `XElement` 하가 서 암호화를 통해는 `IXmlEncryptor`합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-194">The `IXmlDecryptor` interface represents a type that knows how to decrypt an `XElement` that was enciphered via an `IXmlEncryptor`.</span></span> <span data-ttu-id="9e835-195">단일 API를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-195">It exposes a single API:</span></span>

* <span data-ttu-id="9e835-196">(XElement encryptedElement) 암호 해독: XElement</span><span class="sxs-lookup"><span data-stu-id="9e835-196">Decrypt(XElement encryptedElement) : XElement</span></span>

<span data-ttu-id="9e835-197">`Decrypt` 취소할 때 수행한 암호화 `IXmlEncryptor.Encrypt`합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-197">The `Decrypt` method undoes the encryption performed by `IXmlEncryptor.Encrypt`.</span></span> <span data-ttu-id="9e835-198">일반적으로 각 비추상 `IXmlEncryptor` 구현에는 해당 콘크리트 갖습니다 `IXmlDecryptor` 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-198">Generally, each concrete `IXmlEncryptor` implementation will have a corresponding concrete `IXmlDecryptor` implementation.</span></span>

<span data-ttu-id="9e835-199">어떤 구현 형식은 `IXmlDecryptor` 두 public 생성자 중 하나 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-199">Types which implement `IXmlDecryptor` should have one of the following two public constructors:</span></span>

* <span data-ttu-id="9e835-200">.ctor(IServiceProvider)</span><span class="sxs-lookup"><span data-stu-id="9e835-200">.ctor(IServiceProvider)</span></span>
* <span data-ttu-id="9e835-201">.ctor()</span><span class="sxs-lookup"><span data-stu-id="9e835-201">.ctor()</span></span>

> [!NOTE]
> <span data-ttu-id="9e835-202">`IServiceProvider` 에 전달 된 생성자는 null 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-202">The `IServiceProvider` passed to the constructor may be null.</span></span>

## <a name="ikeyescrowsink"></a><span data-ttu-id="9e835-203">IKeyEscrowSink</span><span class="sxs-lookup"><span data-stu-id="9e835-203">IKeyEscrowSink</span></span>

<span data-ttu-id="9e835-204">`IKeyEscrowSink` 인터페이스 에스크로 중요 한 정보를 수행할 수 있는 형식을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-204">The `IKeyEscrowSink` interface represents a type that can perform escrow of sensitive information.</span></span> <span data-ttu-id="9e835-205">Serialize 된 설명자 (예: 암호화 자료)가 중요 한 정보가 포함 될 수 있습니다 및 도입이 이것이 회수는 [IXmlEncryptor](xref:security/data-protection/extensibility/key-management#data-protection-extensibility-key-management-ixmlencryptor) 처음에 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-205">Recall that serialized descriptors might contain sensitive information (such as cryptographic material), and this is what led to the introduction of the [IXmlEncryptor](xref:security/data-protection/extensibility/key-management#data-protection-extensibility-key-management-ixmlencryptor) type in the first place.</span></span> <span data-ttu-id="9e835-206">그러나 실수로 인해가 오류가 발생할 및 키 링 삭제할 수 있습니다 또는 손상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-206">However, accidents happen, and key rings can be deleted or become corrupted.</span></span>

<span data-ttu-id="9e835-207">에스크로 인터페이스에 구성 된 모든에서 변환 되기 전에 원시 serialize 된 XML에 대 한 액세스를 허용 하는 응급 이스케이프 해치 제공 [IXmlEncryptor](xref:security/data-protection/extensibility/key-management#data-protection-extensibility-key-management-ixmlencryptor)합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-207">The escrow interface provides an emergency escape hatch, allowing access to the raw serialized XML before it is transformed by any configured [IXmlEncryptor](xref:security/data-protection/extensibility/key-management#data-protection-extensibility-key-management-ixmlencryptor).</span></span> <span data-ttu-id="9e835-208">인터페이스는 단일 API를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-208">The interface exposes a single API:</span></span>

* <span data-ttu-id="9e835-209">저장소 (Guid keyId, XElement 요소)</span><span class="sxs-lookup"><span data-stu-id="9e835-209">Store(Guid keyId, XElement element)</span></span>

<span data-ttu-id="9e835-210">이 `IKeyEscrowSink` 안전한 비즈니스 정책을 사용 하 여 일관 된 방식으로 제공 된 요소를 처리 하는 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-210">It is up to the `IKeyEscrowSink` implementation to handle the provided element in a secure manner consistent with business policy.</span></span> <span data-ttu-id="9e835-211">여기서 인증서의 개인 키가 에스크로 되었습니다; 알려진된 회사 X.509 인증서를 사용 하 여 XML 요소를 암호화 하려면 에스크로 싱크에 대 한 한 가지 구현 될 수 있습니다. `CertificateXmlEncryptor` 형식이 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-211">One possible implementation could be for the escrow sink to encrypt the XML element using a known corporate X.509 certificate where the certificate's private key has been escrowed; the `CertificateXmlEncryptor` type can assist with this.</span></span> <span data-ttu-id="9e835-212">`IKeyEscrowSink` 구현에 제공된 된 요소를 적절 하 게 유지 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-212">The `IKeyEscrowSink` implementation is also responsible for persisting the provided element appropriately.</span></span>

<span data-ttu-id="9e835-213">기본적으로 에스크로 메커니즘이 없으므로 활성화, 서버 관리자 수 있지만 [전체적으로이 옵션을 구성](xref:security/data-protection/configuration/machine-wide-policy)합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-213">By default no escrow mechanism is enabled, though server administrators can [configure this globally](xref:security/data-protection/configuration/machine-wide-policy).</span></span> <span data-ttu-id="9e835-214">도 구성할 수 있습니다 프로그래밍 방식으로 통해는 `IDataProtectionBuilder.AddKeyEscrowSink` 아래 예제와 같이 메서드.</span><span class="sxs-lookup"><span data-stu-id="9e835-214">It can also be configured programmatically via the `IDataProtectionBuilder.AddKeyEscrowSink` method as shown in the sample below.</span></span> <span data-ttu-id="9e835-215">`AddKeyEscrowSink` 메서드 오버 로드 미러는 `IServiceCollection.AddSingleton` 및 `IServiceCollection.AddInstance` 오버 로드로 `IKeyEscrowSink` 인스턴스는 단일 항목으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-215">The `AddKeyEscrowSink` method overloads mirror the `IServiceCollection.AddSingleton` and `IServiceCollection.AddInstance` overloads, as `IKeyEscrowSink` instances are intended to be singletons.</span></span> <span data-ttu-id="9e835-216">여러 개인 경우 `IKeyEscrowSink` 인스턴스를 등록, 여러 메커니즘을 동시에 키를 위탁 수 있으므로 각 키 생성 시 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-216">If multiple `IKeyEscrowSink` instances are registered, each one will be called during key generation, so keys can be escrowed to multiple mechanisms simultaneously.</span></span>

<span data-ttu-id="9e835-217">API의 자료를 읽을 수는 없습니다는 `IKeyEscrowSink` 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="9e835-217">There is no API to read material from an `IKeyEscrowSink` instance.</span></span> <span data-ttu-id="9e835-218">이 에스크로 메커니즘의 디자인 이론 일치: 키 자료를 신뢰할 수 있는 기관에 액세스할 수 있도록 하기 위한 것이 하며 응용 프로그램은 자체 아니므로 신뢰할 수 있는 기관, 자체 escrowed 자료에 대 한 액세스가 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-218">This is consistent with the design theory of the escrow mechanism: it's intended to make the key material accessible to a trusted authority, and since the application is itself not a trusted authority, it shouldn't have access to its own escrowed material.</span></span>

<span data-ttu-id="9e835-219">다음 샘플 코드에서는 작성 및 등록 한 `IKeyEscrowSink` "CONTOSODomain Admins"의 구성원만 복구할 수는 키는 위탁 되는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-219">The following sample code demonstrates creating and registering an `IKeyEscrowSink` where keys are escrowed such that only members of "CONTOSODomain Admins" can recover them.</span></span>

> [!NOTE]
> <span data-ttu-id="9e835-220">이 샘플을 실행 하려면 여야 도메인에 가입 된 Windows 8에서 Windows Server 2012 컴퓨터와 도메인 컨트롤러에는 Windows Server 2012 이상 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e835-220">To run this sample, you must be on a domain-joined Windows 8 / Windows Server 2012 machine, and the domain controller must be Windows Server 2012 or later.</span></span>

[!code-csharp[Main](key-management/samples/key-management-extensibility.cs)]
