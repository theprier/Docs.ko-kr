---
title: ASP.NET Core SignalR의 지원 되는 플랫폼
author: tdykstra
description: ASP.NET Core SignalR에 대 한 지원 되는 플랫폼
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
# <a name="aspnet-core-signalr-supported-platforms"></a>ASP.NET Core SignalR의 지원 되는 플랫폼

## <a name="server-system-requirements"></a>서버 시스템 요구 사항

ASP.NET core SignalR은 ASP.NET Core에서 지 원하는 모든 서버 플랫폼을 지원 합니다.

## <a name="javascript-client"></a>JavaScript 클라이언트

합니다 [JavaScript 클라이언트](https://www.npmjs.com/package/@aspnet/signalr) NodeJS 8 및 이후 버전 및 다음 브라우저에서 실행 됩니다.

| 브라우저 | 버전 |
| ------- | ------- |
| Microsoft Edge | 현재 |
| Mozilla Firefox | 현재 |
| Google Chrome; Android를 포함합니다. | 현재 |
| Safari; iOS를 포함합니다. | 현재 |
| Microsoft Internet Explorer | 11 |
 
## <a name="net-client"></a>.NET 클라이언트

합니다 [.NET 클라이언트](https://www.nuget.org/packages/Microsoft.AspNetCore.SignalR/) ASP.NET Core에서 지 원하는 서버 플랫폼에서 실행 됩니다.

서버에서 IIS를 실행 하는 경우 Websocket 전송이 이상 Windows Server 2012에서 IIS 8.0 이상이 필요 합니다. 다른 전송 모든 플랫폼에서 지원 됩니다.

## <a name="java-client"></a>Java 클라이언트

합니다 [Java 클라이언트](https://search.maven.org/artifact/com.microsoft.aspnet/signalr) Java 8 및 이후 버전을 지원 합니다.

## <a name="unsupported-clients"></a>지원 되지 않는 클라이언트

다음 클라이언트는 사용할 수 있지만 실험적 또는 비공식 됩니다. 이제 지원 되지 않으며 적이 지원 되지 않습니다.

* [C + + 클라이언트](https://github.com/aspnet/SignalR/tree/master/clients/cpp)

* [Swift 클라이언트](https://github.com/moozzyk/SignalR-Client-Swift)
