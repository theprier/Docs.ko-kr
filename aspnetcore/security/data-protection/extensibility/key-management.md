---
title: ASP.NET Core에서 키 관리 확장성
author: rick-anderson
description: ASP.NET Core 데이터 보호 키 관리 확장성에 알아봅니다.
manager: wpickett
ms.author: riande
ms.date: 11/22/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/data-protection/extensibility/key-management
ms.openlocfilehash: e3042b371cf7be8fa0218c1906042d2810b180e3
ms.sourcegitcommit: 48beecfe749ddac52bc79aa3eb246a2dcdaa1862
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
ms.locfileid: "30074166"
---
# <a name="key-management-extensibility-in-aspnet-core"></a>ASP.NET Core에서 키 관리 확장성

<a name="data-protection-extensibility-key-management"></a>

>[!TIP]
> 읽기는 [키 관리](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management) 이러한 Api는 기본적인 개념 중 일부에 대해 설명 하는 대로이 섹션을 읽기 전에 섹션.

>[!WARNING]
> 다음 인터페이스 중 하나를 구현 하는 형식은 스레드로부터 안전 해야 합니다. 여러 호출자에 대 한 합니다.

## <a name="key"></a>Key

`IKey` 인터페이스 암호화 시스템에 있는 키의 기본 표현입니다. 용어 키의 "암호화 키 자료" 리터럴 관점에 없는 추상적인 의미에서 사용 됩니다. 키에 다음 속성이 있습니다.

* 활성화, 생성 및 만료 날짜

* 해지 상태

* 키 식별자 (GUID)

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

또한 `IKey` 노출 한 `CreateEncryptor` 만드는 데 사용할 수 있는 메서드는 [IAuthenticatedEncryptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptor) 인스턴스가이 키에 연결 합니다.

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

또한 `IKey` 노출 한 `CreateEncryptorInstance` 만드는 데 사용할 수 있는 메서드는 [IAuthenticatedEncryptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptor) 인스턴스가이 키에 연결 합니다.

---

> [!NOTE]
> API에서 원시 암호화 자료를 검색할 수는 없습니다는 `IKey` 인스턴스.

## <a name="ikeymanager"></a>IKeyManager

`IKeyManager` 인터페이스 일반 키 저장소, 검색 및 조작 하는 일을 담당 하는 개체를 나타냅니다. 세 가지 상위 수준 작업을 노출 합니다.

* 새 키를 만들고 저장소를 유지 합니다.

* 저장소에서 모든 키를 가져옵니다.

* 하나 이상의 키를 해지 하 고 저장소는 해지 정보를 저장 합니다.

>[!WARNING]
> 작성 한 `IKeyManager` 는 고급 작업이 며 대부분의 개발자가 려 서는 안 됩니다. 대신 대부분의 개발자가 제공 하는 기능 사용 해야는 [XmlKeyManager](xref:security/data-protection/extensibility/key-management#data-protection-extensibility-key-management-xmlkeymanager) 클래스입니다.

<a name="data-protection-extensibility-key-management-xmlkeymanager"></a>

## <a name="xmlkeymanager"></a>XmlKeyManager

`XmlKeyManager` 형식은의 기본 구체적인 구현 `IKeyManager`합니다. 키 위탁 및 대기 키의 암호화를 포함 하 여 몇 가지 유용한 기능을 제공 합니다. 이 시스템에 있는 키 XML 요소로 표시 됩니다 (특히 [XElement](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/xelement-class-overview)).

`XmlKeyManager` 해당 작업을 수행 하는 과정에서 다른 여러 가지 구성 요소에 따라 달라 집니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

* `AlgorithmConfiguration`를 새 키로 사용 되는 알고리즘 지정 합니다.

* `IXmlRepository`키 저장소에 유지 되는 위치를 제어 합니다.

* `IXmlEncryptor` [옵션]을 허용 하는 저장 된 상태의 키를 암호화 합니다.

* `IKeyEscrowSink` [선택 사항] 키 에스크로 서비스를 제공 하는 합니다.

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

* `IXmlRepository`키 저장소에 유지 되는 위치를 제어 합니다.

* `IXmlEncryptor` [옵션]을 허용 하는 저장 된 상태의 키를 암호화 합니다.

* `IKeyEscrowSink` [선택 사항] 키 에스크로 서비스를 제공 하는 합니다.

---

다음은 이러한 구성 요소 내에서 함께 연결 된 방식을 나타내는 개략적인 다이어그램 `XmlKeyManager`합니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

   ![키 만들기](key-management/_static/keycreation2.png)

   *키 생성 / CreateNewKey*

구현에서 `CreateNewKey`, `AlgorithmConfiguration` 구성 요소는 고유한 만드는 데 사용 되 `IAuthenticatedEncryptorDescriptor`는 다음 XML로 serialize 됩니다. 키 에스크로 싱크가 있는 경우 원시 (암호화 되지 않은) XML 장기 저장에 대 한 싱크에 제공 됩니다. 그런 다음 암호화 되지 않은 XML를 실행 되는 `IXmlEncryptor` (필요한 경우)를 암호화 된 XML 문서를 생성 합니다. 이 암호화 된 문서를 통해 장기 저장소에 유지 되는 `IXmlRepository`합니다. (없는 경우 `IXmlEncryptor` 가 구성, 암호화 되지 않은 문서에서 유지 되는 `IXmlRepository`.)

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

   ![키 만들기](key-management/_static/keycreation1.png)

   *키 생성 / CreateNewKey*

구현에서 `CreateNewKey`, `IAuthenticatedEncryptorConfiguration` 구성 요소는 고유한 만드는 데 사용 되 `IAuthenticatedEncryptorDescriptor`는 다음 XML로 serialize 됩니다. 키 에스크로 싱크가 있는 경우 원시 (암호화 되지 않은) XML 장기 저장에 대 한 싱크에 제공 됩니다. 그런 다음 암호화 되지 않은 XML를 실행 되는 `IXmlEncryptor` (필요한 경우)를 암호화 된 XML 문서를 생성 합니다. 이 암호화 된 문서를 통해 장기 저장소에 유지 되는 `IXmlRepository`합니다. (없는 경우 `IXmlEncryptor` 가 구성, 암호화 되지 않은 문서에서 유지 되는 `IXmlRepository`.)

---

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

   ![키 검색](key-management/_static/keyretrieval2.png)
   
# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

   ![키 검색](key-management/_static/keyretrieval1.png)

---

   *검색 키 / GetAllKeys*

구현에서 `GetAllKeys`, XML 문서 나타내는 키 및 해지 내부에서 읽을 수 있으며 `IXmlRepository`합니다. 이러한 문서를 암호화 하는 경우 시스템은 자동으로 암호 해독할 합니다. `XmlKeyManager` 적절 한 만듭니다 `IAuthenticatedEncryptorDescriptorDeserializer` 로 문서를 역직렬화 할 인스턴스를 다시 `IAuthenticatedEncryptorDescriptor` 개별에 래핑됩니다.이 다음에 인스턴스가 `IKey` 인스턴스. 이 컬렉션의 `IKey` 인스턴스 호출자에 게 반환 됩니다.

특정 XML 요소에 대 한 자세한 정보를 찾을 수는 [키 저장소 형식 문서](xref:security/data-protection/implementation/key-storage-format#data-protection-implementation-key-storage-format)합니다.

## <a name="ixmlrepository"></a>IXmlRepository

`IXmlRepository` 인터페이스는 XML을 유지 하 고 백업 저장소에서 XML을 검색할 수 있는 형식을 나타냅니다. 두 개의 Api를 노출합니다.

* GetAllElements() : IReadOnlyCollection<XElement>

* StoreElement (XElement 요소, 문자열 friendlyName)

구현 `IXmlRepository` 을 통해 전달 되는 XML 구문 분석 필요 하지 않습니다. 불투명으로 XML 문서 처리를 생성 하 고 문서를 구문 분석 하는 방법에 대 한 걱정 더 높은 계층을 사용 합니다.

형식은 두 가지가 기본 제공 구체적 구현 하는 `IXmlRepository`: `FileSystemXmlRepository` 및 `RegistryXmlRepository`합니다. 참조는 [키 저장소 공급자 문서](xref:security/data-protection/implementation/key-storage-providers#data-protection-implementation-key-storage-providers) 자세한 정보에 대 한 합니다. 사용자 지정 등록 `IXmlRepository` 는 적절 한 방법으로 예: 다른 지원 저장소를 사용 하도록 Azure Blob 저장소는 것입니다.

기본 저장소 전체 응용 프로그램을 변경 하려면 사용자 지정 등록 `IXmlRepository` 인스턴스:

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

   ```csharp
   services.Configure<KeyManagementOptions>(options => options.XmlRepository = new MyCustomXmlRepository());
   ```
   
# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

   ```csharp
   services.AddSingleton<IXmlRepository>(new MyCustomXmlRepository());
   ```

---

<a name="data-protection-extensibility-key-management-ixmlencryptor"></a>

## <a name="ixmlencryptor"></a>IXmlEncryptor

`IXmlEncryptor` 인터페이스는 일반 텍스트 XML 요소를 암호화할 수 있는 형식을 나타냅니다. 단일 API를 노출합니다.

* (XElement plaintextElement) 암호화: EncryptedXmlInfo

serialize 된 경우 `IAuthenticatedEncryptorDescriptor` 다음 "암호화 필요"로 표시 하는 요소가 포함 된 `XmlKeyManager` 이러한 요소를 통해 구성 된 실행 됩니다 `IXmlEncryptor`의 `Encrypt` 가 유지할 서 암호화 요소 메서드를 보다는 일반 텍스트 요소를는 `IXmlRepository`합니다. 출력은 `Encrypt` 방법은 `EncryptedXmlInfo` 개체입니다. 이 개체는 모두 결과 서 암호화를 포함 하는 래퍼 `XElement` 및 나타내는 유형에 `IXmlDecryptor` 해당 요소를 해독을 사용할 수 있는 합니다.

네 가지 기본 제공 구체적인 유형 구현 하는 `IXmlEncryptor`:
* `CertificateXmlEncryptor`
* `DpapiNGXmlEncryptor`
* `DpapiXmlEncryptor`
* `NullXmlEncryptor`

참조는 [rest 문서에서 키 암호화](xref:security/data-protection/implementation/key-encryption-at-rest#data-protection-implementation-key-encryption-at-rest) 자세한 정보에 대 한 합니다.

전체 응용 프로그램의 기본 휴지 키 암호화 메커니즘을 변경 하려면 사용자 지정 등록 `IXmlEncryptor` 인스턴스:

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

   ```csharp
   services.Configure<KeyManagementOptions>(options => options.XmlEncryptor = new MyCustomXmlEncryptor());
   ```
   
# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

   ```csharp
   services.AddSingleton<IXmlEncryptor>(new MyCustomXmlEncryptor());
   ```

---

## <a name="ixmldecryptor"></a>IXmlDecryptor

`IXmlDecryptor` 인터페이스 해독 하는 방법을 알고 있는 형식을 나타냅니다는 `XElement` 하가 서 암호화를 통해는 `IXmlEncryptor`합니다. 단일 API를 노출합니다.

* (XElement encryptedElement) 암호 해독: XElement

`Decrypt` 취소할 때 수행한 암호화 `IXmlEncryptor.Encrypt`합니다. 일반적으로 각 비추상 `IXmlEncryptor` 구현에는 해당 콘크리트 갖습니다 `IXmlDecryptor` 구현 합니다.

어떤 구현 형식은 `IXmlDecryptor` 두 public 생성자 중 하나 여야 합니다.

* .ctor(IServiceProvider)
* .ctor()

> [!NOTE]
> `IServiceProvider` 에 전달 된 생성자는 null 일 수 있습니다.

## <a name="ikeyescrowsink"></a>IKeyEscrowSink

`IKeyEscrowSink` 인터페이스 에스크로 중요 한 정보를 수행할 수 있는 형식을 나타냅니다. Serialize 된 설명자 (예: 암호화 자료)가 중요 한 정보가 포함 될 수 있습니다 및 도입이 이것이 회수는 [IXmlEncryptor](xref:security/data-protection/extensibility/key-management#data-protection-extensibility-key-management-ixmlencryptor) 처음에 입력 합니다. 그러나 실수로 인해가 오류가 발생할 및 키 링 삭제할 수 있습니다 또는 손상 되었습니다.

에스크로 인터페이스에 구성 된 모든에서 변환 되기 전에 원시 serialize 된 XML에 대 한 액세스를 허용 하는 응급 이스케이프 해치 제공 [IXmlEncryptor](xref:security/data-protection/extensibility/key-management#data-protection-extensibility-key-management-ixmlencryptor)합니다. 인터페이스는 단일 API를 노출합니다.

* 저장소 (Guid keyId, XElement 요소)

이 `IKeyEscrowSink` 안전한 비즈니스 정책을 사용 하 여 일관 된 방식으로 제공 된 요소를 처리 하는 구현 합니다. 여기서 인증서의 개인 키가 에스크로 되었습니다; 알려진된 회사 X.509 인증서를 사용 하 여 XML 요소를 암호화 하려면 에스크로 싱크에 대 한 한 가지 구현 될 수 있습니다. `CertificateXmlEncryptor` 형식이 도움이 될 수 있습니다. `IKeyEscrowSink` 구현에 제공된 된 요소를 적절 하 게 유지 이기도 합니다.

기본적으로 에스크로 메커니즘이 없으므로 활성화, 서버 관리자 수 있지만 [전체적으로이 옵션을 구성](xref:security/data-protection/configuration/machine-wide-policy)합니다. 도 구성할 수 있습니다 프로그래밍 방식으로 통해는 `IDataProtectionBuilder.AddKeyEscrowSink` 아래 예제와 같이 메서드. `AddKeyEscrowSink` 메서드 오버 로드 미러는 `IServiceCollection.AddSingleton` 및 `IServiceCollection.AddInstance` 오버 로드로 `IKeyEscrowSink` 인스턴스는 단일 항목으로 사용 합니다. 여러 개인 경우 `IKeyEscrowSink` 인스턴스를 등록, 여러 메커니즘을 동시에 키를 위탁 수 있으므로 각 키 생성 시 호출 됩니다.

API의 자료를 읽을 수는 없습니다는 `IKeyEscrowSink` 인스턴스. 이 에스크로 메커니즘의 디자인 이론 일치: 키 자료를 신뢰할 수 있는 기관에 액세스할 수 있도록 하기 위한 것이 하며 응용 프로그램은 자체 아니므로 신뢰할 수 있는 기관, 자체 escrowed 자료에 대 한 액세스가 하지 않아야 합니다.

다음 샘플 코드에서는 작성 및 등록 한 `IKeyEscrowSink` "CONTOSODomain Admins"의 구성원만 복구할 수는 키는 위탁 되는 위치입니다.

> [!NOTE]
> 이 샘플을 실행 하려면 여야 도메인에 가입 된 Windows 8에서 Windows Server 2012 컴퓨터와 도메인 컨트롤러에는 Windows Server 2012 이상 이어야 합니다.

[!code-csharp[](key-management/samples/key-management-extensibility.cs)]
