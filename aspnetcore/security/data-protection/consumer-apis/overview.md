---
title: "소비자 Api 개요"
author: rick-anderson
description: "이 문서는 다양 한 소비자 ASP.NET Core data protection 라이브러리 내에서 사용할 수 있는 Api의 간략 한 개요를 제공합니다."
keywords: "ASP.NET Core, 데이터 보호 Api 소비자"
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.assetid: f69beb9d-a519-43a8-857c-f6b01886a903
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/data-protection/consumer-apis/overview
ms.openlocfilehash: c80ed22776b0dbbaccb686f8c2ea534e6f5d9a74
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
# <a name="consumer-apis-overview"></a>소비자 Api 개요

`IDataProtectionProvider` 및 `IDataProtector` 인터페이스는 기본 인터페이스를 소비자는 데이터 보호 시스템을 사용 합니다. 에 살고 있는 [Microsoft.AspNetCore.DataProtection.Abstractions](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.Abstractions/) 패키지 합니다.

## <a name="idataprotectionprovider"></a>IDataProtectionProvider

공급자 인터페이스는 데이터 보호 시스템의 루트를 나타냅니다. 해당 파일을 보호 하거나 데이터를 보호 해제를 직접 사용할 수 없습니다. 대신 소비자에 대 한 참조를 가져와야는 `IDataProtector` 호출 하 여 `IDataProtectionProvider.CreateProtector(purpose)`여기서 용도 대상된 소비자 사용 사례를 설명 하는 문자열입니다. 참조 [목적 문자열](purpose-strings.md) 이 매개 변수 및 적절 한 값을 선택 하는 방법의 의도에 훨씬 더 많은 정보에 대 한 합니다.

## <a name="idataprotector"></a>IDataProtector

보호기 인터페이스에 대 한 호출에서 반환 `CreateProtector`, 소비자가 수행 하는 데 사용할 수 있는이 인터페이스를 보호 하 고 작업을 보호 해제 하 고 있습니다.

일부 데이터를 보호 하려면 데이터를 전달할는 `Protect` 메서드. 기본 인터페이스는 변환 byte byte-> 메서드를 정의 하지만 또한 오버 로드 (확장 메서드로 제공) 문자열을 변환 하는 문자열->. 두 가지 방법으로 제공 되는 보안은 동일 합니다. 개발자는 어떤 오버 로드는 해당 사용 사례에 대 한 가장 편리 하 게 선택 해야 합니다. 오버 로드를 선택한 보호에서 반환 된 값에 관계 없이 메서드는 이제 보호 (서 암호화 및 조작에도 성능이 보장) 및 응용 프로그램이 신뢰할 수 없는 클라이언트에 보낼 수 있습니다.

이전에 보호 된 일부 데이터 보호를 해제 하려면 보호 된 데이터에 전달 된 `Unprotect` 메서드. (Byte-개발자 편의 위해 기반 및 문자열 기반 오버 로드 합니다.) 보호 된 페이로드 한 이전 호출에 의해 생성 된 경우 `Protect` 이 동일한 `IDataProtector`, `Unprotect` 메서드는 원래 보호 되지 않는 페이로드를 반환 합니다. 또는 보호 된 페이로드 변조 되었거나 다른를 통해 만들어진 경우 `IDataProtector`, `Unprotect` 메서드 CryptographicException를 throw 합니다.

다른와 동일한 개념 `IDataProtector` 동률 목적의 개념을 백업 합니다. 두 개 `IDataProtector` 인스턴스 동일한 루트에서 시작 된 `IDataProtectionProvider` 하지만 다른 용도로 문자열에 대 한 호출을 통해 `IDataProtectionProvider.CreateProtector`, 것으로 간주 됩니다 [다른 보호기](purpose-strings.md), 하나는 보호를 해제할 수 없습니다 다른에서 생성 된 페이로드입니다.

## <a name="consuming-these-interfaces"></a>이러한 인터페이스를 사용합니다.

DI 인식 구성 요소에 대해 원하는 사용 되는 구성 요소 걸릴는 `IDataProtectionProvider` DI 시스템 구성 요소를 인스턴스화할 때 자동으로이 서비스를 제공 하 고 생성자의 매개 변수입니다.

> [!NOTE]
> 일부 응용 프로그램 (예: 콘솔 응용 프로그램 또는 ASP.NET 4.x 응용 프로그램) DI 인식 하므로 여기서 설명 하는 메커니즘을 사용할 수 없습니다 아닐 수 있습니다. 이러한 시나리오를 참조에 대 한는 [비 DI 인식 시나리오](../configuration/non-di-scenarios.md) 의 인스턴스를 가져오는 방법에 대 한 자세한 내용은 문서는 `IDataProtection` DI를 통하지 않고는 공급자입니다.

다음 샘플에서는 세 가지 개념을 보여 줍니다.

1. [추가 데이터 보호 시스템](../configuration/overview.md) 서비스 컨테이너를

2. DI를 사용 하 여 인스턴스의 받기는 `IDataProtectionProvider`, 및

3. 만들기는 `IDataProtector` 에서 `IDataProtectionProvider` 보호 및 데이터를 보호 해제 하는 데 사용 하 합니다.

[!code-csharp[Main](../using-data-protection/samples/protectunprotect.cs?highlight=26,34,35,36,37,38,39,40)]

확장 메서드를 포함 하는 패키지 Microsoft.AspNetCore.DataProtection.Abstractions `IServiceProvider.GetDataProtector` 개발자 편의 위해. 모두 검색 하는 하나의 작업으로 캡슐화는 `IDataProtectionProvider` 서비스 공급자 및 호출 `IDataProtectionProvider.CreateProtector`합니다. 다음 샘플의 사용법을 보여 줍니다.

[!code-csharp[Main](./overview/samples/getdataprotector.cs?highlight=15)]

>[!TIP]
> 인스턴스 `IDataProtectionProvider` 및 `IDataProtector` 여러 호출자에 대 한 스레드로부터 안전 합니다. 구성 요소에 대 한 참조를 가져온 후 사용 하는 `IDataProtector` 호출을 통해 `CreateProtector`, 해당 참조를 여러 번 호출에 사용할 `Protect` 및 `Unprotect`합니다. 에 대 한 호출 `Unprotect` CryptographicException 보호 된 페이로드를 확인 하거나 해독할 수 없는 경우이 throw 합니다. 일부 구성 요소 오류를 무시 하려는 경우가 있을 수 하는 동안 작업을 보호 해제 인증 쿠키를 읽는 구성 요소 수 있습니다이 오류를 처리 하 고 전혀 쿠키가 없는 이전의 요청 처럼 처리할 대신 완전 한 요청에 실패 합니다. 구체적으로이 동작을 방지 하는 구성 요소는 모든 예외를 받아들이지 않고 CryptographicException을 catch 해야 합니다.
