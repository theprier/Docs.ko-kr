---
title: ASP.NET Core SignalR 지원 플랫폼
author: tdykstra
description: ASP.NET Core SignalR 지원 플랫폼
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 09/26/2018
uid: signalr/supported-platforms
ms.openlocfilehash: d6d74a55d35ddb34a6f66a171bfe3f343dd61b63
ms.sourcegitcommit: 7b4e3936feacb1a8fcea7802aab3e2ea9c8af5b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48577628"
---
# <a name="aspnet-core-signalr-supported-platforms"></a>ASP.NET Core SignalR 지원 플랫폼

## <a name="server-system-requirements"></a>서버 시스템 요구 사항

ASP.NET Core SignalR은 ASP.NET Core가 지원하는 모든 서버 플랫폼을 지원합니다.

## <a name="javascript-client"></a>JavaScript 클라이언트

[JavaScript 클라이언트](https://www.npmjs.com/package/@aspnet/signalr)는 NodeJS 8 이상의 버전과 다음 브라우저에서 실행됩니다.

| 브라우저 | 버전 |
| ------- | ------- |
| Microsoft Edge | 현재 |
| Mozilla Firefox | 현재 |
| Google Chrome(Android 포함) | 현재 |
| Safari(iOS 포함) | 현재 |
| Microsoft Internet Explorer | 11 |
 
## <a name="net-client"></a>.NET 클라이언트

[.NET 클라이언트](https://www.nuget.org/packages/Microsoft.AspNetCore.SignalR/)는 ASP.NET Core가 지원하는 모든 서버 플랫폼에서 실행됩니다.

서버에서 IIS를 실행하는 경우 WebSockets 전송을 사용하려면 Windows Server 2012 이상에서 IIS 8.0 이상의 버전이 필요합니다. 다른 전송 방식들은 모든 플랫폼에서 지원됩니다.

## <a name="java-client"></a>Java 클라이언트

[Java 클라이언트](https://search.maven.org/artifact/com.microsoft.aspnet/signalr)는 Java 8 이상의 버전을 지원합니다.

## <a name="unsupported-clients"></a>지원되지 않는 클라이언트

다음 클라이언트는 사용할 수는 있지만 실험적이거나 비공식적입니다. 현재 지원되지 않으며 앞으로도 지원되지 않을 수 있습니다.

* [C++ 클라이언트](https://github.com/aspnet/SignalR/tree/master/clients/cpp)

* [Swift 클라이언트](https://github.com/moozzyk/SignalR-Client-Swift)
