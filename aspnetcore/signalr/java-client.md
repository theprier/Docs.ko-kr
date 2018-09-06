---
title: ASP.NET Core SignalR Java 클라이언트
author: mikaelm12
description: ASP.NET Core SignalR Java 클라이언트를 사용 하는 방법에 알아봅니다.
monikerRange: '>= aspnetcore-2.2'
ms.author: mimengis
ms.custom: mvc
ms.date: 09/06/2018
uid: signalr/java-client
ms.openlocfilehash: f110f5391ac34f5cb4a72f64c16d86c8a37369a2
ms.sourcegitcommit: 4cd8dce371d63a66d780e4af1baab2bcf9d61b24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43995421"
---
# <a name="aspnet-core-signalr-java-client"></a>ASP.NET Core SignalR Java 클라이언트

[Mikael Mengistu](https://twitter.com/MikaelM_12)

Java 클라이언트 Android 앱을 포함 하 여 Java 코드에서 ASP.NET Core SignalR 서버에 연결할 수 있습니다. 같은 합니다 [JavaScript 클라이언트](xref:signalr/javascript-client) 하며 [.NET 클라이언트](xref:signalr/dotnet-client), Java 클라이언트를 사용 하면 실시간으로 허브에 메시지를 보내고 받을 수 있습니다. Java 클라이언트는 ASP.NET Core 2.2에서 사용할 수 있는 이상.

이 문서에에서 나와 있는 샘플 Java 콘솔 앱 SignalR Java 클라이언트를 사용 합니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/java-client/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

## <a name="install-the-signalr-java-client-package"></a>SignalR Java 클라이언트 패키지를 설치 합니다.

합니다 *signalr 0.1.0-preview1 35029* JAR 파일에는 클라이언트가 SignalR 허브에 연결할 수 있습니다. 최신 JAR 파일 버전 번호를 찾으려면 다음을 참조 합니다 [Maven 검색 결과](https://search.maven.org/search?q=g:com.microsoft.aspnet%20AND%20a:signalr&core=gav)합니다.

Gradle을 사용 하는 경우에 다음 줄을 추가 합니다 `dependencies` 의 섹션에 *build.gradle* 파일:

```gradle
implementation 'com.microsoft.aspnet:signalr:0.1.0-preview1-35029'
```

Maven을 사용 하 여 내에 다음 줄을 추가 합니다 `<dependencies>` 의 요소에 *pom.xml* 파일:

[!code-xml[pom.xml dependency element](java-client/sample/pom.xml?name=snippet_dependencyElement)]

## <a name="connect-to-a-hub"></a>허브에 연결

설정 하는 `HubConnection`, `HubConnectionBuilder` 사용 해야 합니다. 허브 URL 및 로그 수준에 대 한 연결을 구축 하는 동안 구성할 수 있습니다. 중 하나를 호출 하 여 필요한 모든 옵션을 구성 합니다 `HubConnectionBuilder` 하기 전에 메서드 `build`합니다. 사용 하 여 연결을 시작할 `start`합니다.

[!code-java[Build hub connection](java-client/sample/src/main/java/Chat.java?range=17-20)]

## <a name="call-hub-methods-from-client"></a>클라이언트에서 허브 메서드를 호출 합니다.

에 대 한 호출 `send` 허브 메서드를 호출 합니다. 허브 메서드 이름 및 허브 메서드를 정의 하는 모든 인수를 전달 `send`합니다.

[!code-java[send method](java-client/sample/src/main/java/Chat.java?range=31)]

## <a name="call-client-methods-from-hub"></a>허브에서 클라이언트 메서드를 호출

사용 하 여 `hubConnection.on` 허브를 호출할 수 있는 클라이언트에서 메서드를 정의 합니다. 빌드 후 있지만 연결을 시작 하기 전에 메서드를 정의 합니다.

[!code-java[Define client methods](java-client/sample/src/main/java/Chat.java?range=22-24)]

## <a name="known-limitations"></a>알려진 제한 사항

이 Java 클라이언트의 초기 미리 보기 릴리스입니다. 아직 지원 되지 않는 많은 기능이 있습니다. 향후 릴리스에 대 한 다음 간격에 작업 중인:

* 기본 형식만 매개 변수로 사용할 수 및 반환 형식입니다.
* Api는 동기입니다.
* 이 이번에는 "송신" 호출 유형만 지원 됩니다. "호출" 및 반환 값의 스트리밍 지원 되지 않습니다.
* 클라이언트에서 현재 지원 하지 않습니다 합니다 [Azure SignalR Service](/azure/azure-signalr/)합니다.
* JSON 프로토콜에만 지원 됩니다.
* Websocket 전송만 지원 됩니다.

## <a name="additional-resources"></a>추가 자료

* <xref:signalr/hubs>
* <xref:signalr/javascript-client>
* <xref:signalr/publish-to-azure-web-app>
