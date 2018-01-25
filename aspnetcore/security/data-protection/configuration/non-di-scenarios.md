---
title: "ASP.NET Core 데이터 보호에 대한 비-DI 인식 시나리오"
author: rick-anderson
description: "종속성 주입으로 제공되는 서비스를 사용할 수 없거나 사용하지 않는 데이터 보호 시나리오를 지원하는 방법에 대해 알아봅니다."
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
# <a name="non-di-aware-scenarios-for-data-protection-in-aspnet-core"></a>ASP.NET Core 데이터 보호에 대한 비-DI 인식 시나리오

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)

일반적으로 ASP.NET Core 데이터 보호 시스템은 [서비스 컨테이너에 추가되고](xref:security/data-protection/consumer-apis/overview), 종속 구성 요소에서 종속성 주입(DI)을 통해서 사용됩니다. 그러나 경우에 따라서는 이런 구성이 불가능한 경우도 있으며, 그 대표적인 사례가 기존 응용 프로그램에 데이터 보호 시스템을 추가하는 경우입니다.

이런 시나리오를 지원하기 위해서, [Microsoft.AspNetCore.DataProtection.Extensions](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.Extensions/) 패키지는 DI에 의존하지 않고도 데이터 보호를 사용할 수 있는 간단한 방법을 제공해주는 [DataProtectionProvider](/dotnet/api/Microsoft.AspNetCore.DataProtection.DataProtectionProvider) 구체 형식을 제공합니다. `DataProtectionProvider` 형식은 [IDataProtectionProvider](/dotnet/api/microsoft.aspnetcore.dataprotection.idataprotectionprovider)를 구현합니다. `DataProtectionProvider`를 생성하기 위해서는, 다음 예제 코드에서 볼 수 있는 것처럼 해당 공급자의 암호화 키가 저장될 위치를 가리키는 [DirectoryInfo](/dotnet/api/system.io.directoryinfo)의 인스턴스를 전달하면 됩니다:

[!code-none[Main](non-di-scenarios/_static/nodisample1.cs)]

기본적으로 `DataProtectionProvider` 구체 형식은 원시 키 관련 자료를 파일 시스템에 저장하기 전에 암호화하지 않습니다. 이는 개발자가 네트워크 공유를 지정하는 등의 경우를 지원하기 위한 것으로, 그런 경우에는 데이터 보호 시스템이 저장된 비활성 키에 대한 적절한 암호화 메커니즘을 자동으로 추론할 수 없습니다.

또한, 기본적으로 `DataProtectionProvider` 구체 형식은 [응용 프로그램을 격리](xref:security/data-protection/configuration/overview#per-application-isolation)하지 않습니다. 동일한 키 디렉터리를 가리키는 모든 응용 프로그램들은 [용도 매개 변수](xref:security/data-protection/consumer-apis/purpose-strings)가 일치하기만 하면 페이로드를 공유할 수 있습니다.

[DataProtectionProvider](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionprovider)의 생성자에는 데이터 보호 시스템의 동작을 제어할 때 사용되는 선택적 구성 콜백을 전달할 수 있습니다. 다음 예제는 명시적으로 [SetApplicationName](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setapplicationname) 메서드를 호출해서 격리 기능을 활성화시킵니다. 그리고 자동으로 Windows DPAPI를 이용해서 저장되는 키를 암호화하도록 시스템을 구성하는 방법도 보여줍니다. 만약 디렉터리가 UNC 공유를 가리키고 있다면, 관련된 모든 머신에 공유 인증서를 배포한 다음, [ProtectKeysWithCertificate](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.protectkeyswithcertificate)를 호출해서 시스템이 대신 인증서 기반 암호화를 사용하도록 구성할 수도 있습니다.

[!code-none[Main](non-di-scenarios/_static/nodisample2.cs)]

> [!TIP]
> `DataProtectionProvider` 구체 형식의 인스턴스를 생성하는 것은 비용이 많이 드는 작업입니다. 만약, 응용 프로그램이 이 형식의 인스턴스를 여러 개 관리하지만 모든 인스턴스가 동일한 키 저장소 디렉터리를 가리킨다면 응용 프로그램의 성능이 저하될 수 있습니다. `DataProtectionProvider` 형식을 사용할 때 권장되는 방식은 응용 프로그램 개발자가 이 형식의 인스턴스를 한 번만 생성한 다음, 해당 단일 참조를 가능한 여러 번 재사용하는 것입니다. `DataProtectionProvider` 형식 및 이 형식으로부터 생성된 모든 [IDataProtector](/dotnet/api/microsoft.aspnetcore.dataprotection.idataprotector)의 인스턴스는 다중 호출자에 대해 스레드로부터 안전(Thread-Safe)합니다.
