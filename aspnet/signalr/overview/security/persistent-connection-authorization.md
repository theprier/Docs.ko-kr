---
uid: signalr/overview/security/persistent-connection-authorization
title: 인증 및 권한 부여 SignalR 영구 연결에 대 한 | Microsoft Docs
author: pfletcher
description: 이 항목에는 영구 연결에서 권한 부여를 적용 하는 방법을 설명 합니다. SignalR 응용 프로그램에 보안을 통합 하는 방법에 대 한 일반적인 내용은...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2014
ms.topic: article
ms.assetid: e264677b-9c01-47ec-94f9-3cd8f08f94af
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/security/persistent-connection-authorization
msc.type: authoredcontent
ms.openlocfilehash: d559cfa21f6444b2361fd003b9ce3d2c9c6c57a4
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
ms.locfileid: "28042201"
---
<a name="authentication-and-authorization-for-signalr-persistent-connections"></a>인증 및 권한 부여 SignalR 영구 연결에 대 한
====================
여 [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)

> 이 항목에는 영구 연결에서 권한 부여를 적용 하는 방법을 설명 합니다. SignalR 응용 프로그램에 보안을 통합 하는 방법에 대 한 일반 정보를 참조 하십시오. [보안 소개](introduction-to-security.md)합니다. 
> 
> ## <a name="software-versions-used-in-this-topic"></a>이 항목에서 사용 되는 소프트웨어 버전
> 
> 
> - [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - .NET 4.5
> - SignalR 버전 2
>   
> 
> 
> ## <a name="previous-versions-of-this-topic"></a>이 항목의 이전 버전
> 
> 이전 버전의 SignalR에 대 한 정보를 참조 하십시오. [SignalR 이전 버전](../older-versions/index.md)합니다.
> 
> ## <a name="questions-and-comments"></a>질문이 나 의견이
> 
> 이 자습서를 연결 하는 방법 및 페이지의 맨 아래에 주석에서 향상 될 수 있습니다 어떻게에 의견을 남겨 주세요. 자습서를 직접 관련 되지 않는 질문 해야 하도록를 게시할 수 있습니다는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)합니다.


## <a name="enforce-authorization"></a>권한 부여를 적용 합니다.

사용 하는 경우 권한 부여 규칙을 적용 하는 [PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) 재정의 해야 합니다는 `AuthorizeRequest` 메서드. 사용할 수 없습니다는 `Authorize` 영구 연결을 사용 하 여 특성입니다. `AuthorizeRequest` 메서드는 사용자가 요청한 작업을 수행할 권한이 있는지 확인 하는 모든 요청 전에 SignalR 프레임 워크에서 호출 됩니다. `AuthorizeRequest` 응용 프로그램의 표준 인증 메커니즘을 통해 사용자를 인증 대신; 클라이언트에서 메서드가 호출 되지 않습니다.

다음 예제에서는 인증 된 사용자에 대 한 요청을 제한 하는 방법을 보여 줍니다.

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

AuthorizeRequest 메서드;에 사용자 지정된 권한 부여 논리를 추가할 수 있습니다. 와 같은 사용자 특정 역할에 속하는지 여부를 확인 중입니다.
