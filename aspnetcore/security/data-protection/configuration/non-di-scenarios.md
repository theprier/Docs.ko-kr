---
title: "비 DI 인식 시나리오 ASP.NET Core 데이터 보호"
author: rick-anderson
description: "데이터 보호 시나리오를 처리할 수 없거나 종속성 주입 제공 하는 서비스를 사용 하지 않을 지 원하는 방법에 알아봅니다."
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/data-protection/configuration/non-di-scenarios
ms.openlocfilehash: 1c84cfcf44086359a7d6900ca52781dc6f3b1b10
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="non-di-aware-scenarios-for-data-protection-in-aspnet-core"></a>비 DI 인식 시나리오 ASP.NET Core 데이터 보호

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)

ASP.NET Core 데이터 보호 시스템은 일반적으로 [서비스 컨테이너에 추가 된](xref:security/data-protection/consumer-apis/overview) 와 종속성 주입 DI ()를 통해 종속 구성 요소에서 사용 합니다. 그러나 불가능 또는 원하는 수 없는이 없는 경우도 있습니다. 특히 기존 앱에 시스템을 가져오는 경우.

이러한 시나리오를 지원 하도록는 [Microsoft.AspNetCore.DataProtection.Extensions](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.Extensions/) 패키지는 구체적인 형식이 제공 [DataProtectionProvider](/dotnet/api/Microsoft.AspNetCore.DataProtection.DataProtectionProvider), 데이터 보호를 사용 하는 간단한 방법을 제공 DI에 의존 하지 않고 합니다. `DataProtectionProvider` 구현 입력 [IDataProtectionProvider](/dotnet/api/microsoft.aspnetcore.dataprotection.idataprotectionprovider)합니다. 생성 `DataProtectionProvider` 하기만 제공 하는 [DirectoryInfo](/dotnet/api/system.io.directoryinfo) 다음 코드 예제와 같이 공급자의 암호화 키 저장 될 위치를 나타냅니다.

[!code-none[Main](non-di-scenarios/_static/nodisample1.cs)]

기본적으로는 `DataProtectionProvider` 구체적인 형식 원시 키 자료를 암호화 하지 않습니다 전에 파일 시스템에 유지 합니다. 이 시나리오를 네트워크 공유 및 데이터 보호 시스템 개발자 포인트 추론할 수 없습니다. 자동으로 적절 한 휴지 키 암호화 메커니즘을 지 원하는입니다.

또한는 `DataProtectionProvider` 구체적인 형식 하지 않는 [앱을 격리](xref:security/data-protection/configuration/overview#per-application-isolation) 기본적으로 합니다. 동일한 키 디렉터리를 사용 하 여 모든 응용 프로그램 페이로드는 공유할 수 자신의 [매개 변수 용도 위해](xref:security/data-protection/consumer-apis/purpose-strings) 일치 합니다.

[DataProtectionProvider](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionprovider) 생성자가 시스템의 동작을 조정 하는 데 사용할 수 있는 선택적 구성 콜백 허용 합니다. 다음 예제를 명시적으로 호출 된 복원 격리를 보여 줍니다. [SetApplicationName](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setapplicationname)합니다. 이 샘플에는 자동으로 보관 되는 Windows DPAPI를 사용 하 여 키를 암호화 하는 시스템 구성 보여 줍니다. 관련 된 모든 컴퓨터에 공유 인증서를 배포 하 고 시스템을 호출 하 여 인증서 기반 암호화를 사용 하도록 구성 하는 디렉터리는 UNC 공유를 가리키는 경우 지정할 수 있습니다 [ProtectKeysWithCertificate](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.protectkeyswithcertificate)합니다.

[!code-none[Main](non-di-scenarios/_static/nodisample2.cs)]

> [!TIP]
> 인스턴스는 `DataProtectionProvider` 구체적인 형식은 만드는 비용이 많이 듭니다. 앱이 유형의 여러 인스턴스를 유지 관리를 사용 하 든 모두 동일한 키 저장소 디렉터리 응용 프로그램 성능이 저하 될 수 있습니다. 사용 하는 경우는 `DataProtectionProvider` 이 유형은 한 번 만들고는 가능한 한 다시 사용할 권장 형식입니다. `DataProtectionProvider` 유형 및 모든 [IDataProtector](/dotnet/api/microsoft.aspnetcore.dataprotection.idataprotector) 에서 생성 된 인스턴스는 스레드로부터 안전 여러 호출자에 대 한 합니다.
