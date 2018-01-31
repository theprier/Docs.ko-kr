---
uid: signalr/overview/testing-and-debugging/unit-testing-signalr-applications
title: "SignalR 응용 프로그램 유닛 테스트 | Microsoft Docs"
author: pfletcher
description: "이 문서에서는 SignalR 2.0의 단위 테스트 기능을 사용 하는 방법을 설명 합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2014
ms.topic: article
ms.assetid: d1983524-e0d5-4ee6-9d87-1f552f7cb964
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/testing-and-debugging/unit-testing-signalr-applications
msc.type: authoredcontent
ms.openlocfilehash: d767e1a9d27670387133e5a48a8f92f5bdd39d9e
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="unit-testing-signalr-applications"></a>단위 테스트 SignalR 응용 프로그램
====================
으로 [Patrick Fletcher](https://github.com/pfletcher)

> 이 문서에서는 SignalR 2의 단위 테스트 기능을 사용 하 여 설명 합니다. 
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
> ## <a name="questions-and-comments"></a>질문이 나 의견이
> 
> 이 자습서를 연결 하는 방법 및 페이지의 맨 아래에 주석에서 향상 될 수 있습니다 어떻게에 의견을 남겨 주세요. 자습서를 직접 관련 되지 않는 질문 해야 하도록를 게시할 수 있습니다는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)합니다.


<a id="unit"></a>
## <a name="unit-testing-signalr-applications"></a>SignalR 응용 프로그램 유닛 테스트

SignalR 2에서 단위 테스트를 만드는 SignalR 응용 프로그램에 대 한 단위 테스트 기능을 사용할 수 있습니다. SignalR 2에 포함 되어는 [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) 인터페이스를 테스트 하기 위한 허브 메서드를 시뮬레이션 하는 모의 개체를 만드는 데 사용할 수 있습니다.

이 섹션에서는 만든 응용 프로그램에 대 한 단위 테스트 추가 [시작 자습서](../getting-started/tutorial-getting-started-with-signalr.md) 를 사용 하 여 [XUnit.net](https://github.com/xunit/xunit) 및 [Moq](https://github.com/Moq/moq4)합니다.

XUnit.net; 테스트를 제어 하는 데 사용 됩니다. Moq 만드는 데 사용할 됩니다는 [의 모의 알림](http://en.wikipedia.org/wiki/Mock_object) 테스트에 대 한 개체입니다. 원하는; 경우 다른 모의 프레임 워크를 사용할 수 있습니다. [NSubstitute](http://nsubstitute.github.io/) 도 것이 좋습니다. 이 자습서에서는 두 가지 방법으로 모의 개체를 설정 하는 방법을 설명: 사용 하 여 먼저는 `dynamic` 개체 (.NET Framework 4에 도입 된) 및 인터페이스를 사용 하 여 두 번째입니다.

### <a name="contents"></a>목차

이 자습서는 다음 섹션이 포함 되어 있습니다.

- [동적을 사용한 단위 테스트](#dynamic)
- [단위 테스트 유형별로](#type)

<a id="dynamic"></a>
### <a name="unit-testing-with-dynamic"></a>동적을 사용한 단위 테스트

이 섹션에서 만든 응용 프로그램에 대 한 단위 테스트를 추가 합니다는 [시작 자습서](../getting-started/tutorial-getting-started-with-signalr.md) 동적 개체를 사용 하 여 합니다.

1. 설치는 [XUnit Runner 확장](https://visualstudiogallery.msdn.microsoft.com/463c5987-f82b-46c8-a97e-b1cde42b9099) Visual Studio 2013 용입니다.
2. 완료 하거나는 [시작 자습서](../getting-started/tutorial-getting-started-with-signalr.md)에서 완성 된 응용 프로그램을 다운로드 하거나 [MSDN 코드 갤러리](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)합니다.
3. 시작 응용 프로그램의 다운로드 버전이 사용 하는 경우 열 **패키지 관리자 콘솔** 클릭 **복원** SignalR 패키지 프로젝트를 추가 하려면.

    ![패키지를 복원](unit-testing-signalr-applications/_static/image1.png)
4. 단위 테스트에 대 한 솔루션에 프로젝트를 추가 합니다. 솔루션을 마우스 오른쪽 단추로 클릭 **솔루션 탐색기** 선택 **추가**, **새 프로젝트...** . 아래는 **C#** 노드를 선택는 **Windows** 노드. 선택 **클래스 라이브러리**합니다. 새 프로젝트의 이름을 **TestLibrary** 클릭 **확인**합니다.

    ![테스트 라이브러리 만들기](unit-testing-signalr-applications/_static/image2.png)
5. SignalRChat 프로젝트에 테스트 라이브러리 프로젝트에 대 한 참조를 추가 합니다. 마우스 오른쪽 단추로 클릭는 **TestLibrary** 프로젝트를 마우스 선택 **추가**, **참조 중...** . 선택 된 **프로젝트** 노드 아래의 **솔루션** 노드와 검사 **SignalRChat**합니다. **확인**을 클릭합니다.

    ![프로젝트 참조 추가](unit-testing-signalr-applications/_static/image3.png)
6. SignalR, Moq, 및 XUnit 패키지에 추가 된 **TestLibrary** 프로젝트. 에 **패키지 관리자 콘솔**설정는 **기본 프로젝트** 드롭다운을 **TestLibrary**합니다. 콘솔 창에 다음 명령을 실행 합니다.

    - `Install-Package Microsoft.AspNet.SignalR`
    - `Install-Package Moq`
    - `Install-Package XUnit`

    ![패키지 설치](unit-testing-signalr-applications/_static/image4.png)
7. 테스트 파일을 만듭니다. 마우스 오른쪽 단추로 클릭는 **TestLibrary** 프로젝트 **추가 중...** , **클래스**합니다. 클래스의 새 이름을 **Tests.cs**합니다.
8. Tests.cs의 내용을 다음 코드로 바꿉니다.

    [!code-csharp[Main](unit-testing-signalr-applications/samples/sample1.cs)]

    위의 코드에서 테스트 클라이언트 사용 하 여 만들어집니다는 `Mock` 에서 개체는 [Moq](https://github.com/Moq/moq4) 형식의 라이브러리 [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) (SignalR 2.1에서 할당 `dynamic` 유형에 대 한 매개 변수입니다.) `IHubCallerConnectionContext` 인터페이스는 클라이언트에서 메서드를 호출 하는 프록시 개체입니다. `broadcastMessage` 함수는 다음에 대해 정의 된 모의 클라이언트에서 호출할 수 있도록는 `ChatHub` 클래스입니다. 테스트 엔진에서 호출 된 `Send` 의 메서드는 `ChatHub` 호출 하는 모의 클래스 `broadcastMessage` 함수.
9. 키를 눌러 솔루션을 빌드합니다 **F6**합니다.
10. 단위 테스트를 실행합니다. Visual Studio에서 선택 **테스트**, **Windows**, **테스트 탐색기**합니다. 테스트 탐색기 창에서 마우스 오른쪽 단추로 클릭 **HubsAreMockableViaDynamic** 선택 **선택 된 테스트 실행**합니다.

    ![테스트 탐색기](unit-testing-signalr-applications/_static/image5.png)
11. 테스트 탐색기 창의 아래쪽 창 확인 하 여 테스트에 통과 했는지 확인 합니다. 창에서 테스트를 통과 했음이 표시 됩니다.

    ![테스트 통과](unit-testing-signalr-applications/_static/image6.png)

<a id="type"></a>
### <a name="unit-testing-by-type"></a>단위 테스트 유형별로

이 섹션에서 만든 응용 프로그램에 대 한 테스트를 추가 합니다는 [시작 자습서](../getting-started/tutorial-getting-started-with-signalr.md) 테스트할 메서드를 포함 하는 인터페이스를 사용 하 여 합니다.

1. 1-7 단계에서 완료 된 [동적을 사용한 단위 테스트](#dynamic) 위의 자습서입니다.
2. Tests.cs의 내용을 다음 코드로 바꿉니다.

    [!code-csharp[Main](unit-testing-signalr-applications/samples/sample2.cs)]

    위의 코드에서 인터페이스의 서명을 정의 생성 됩니다는 `broadcastMessage` 메서드 테스트 엔진에서는 모의 클라이언트를 만듭니다. 모의 클라이언트를 사용 하 여 만들고 그런 다음는 `Mock` 형식의 개체 [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) (SignalR 2.1에서 할당 `dynamic` 형식 매개 변수.) `IHubCallerConnectionContext` 인터페이스는 클라이언트에서 메서드를 호출 하는 프록시 개체입니다.

    테스트의 인스턴스를 만든 후 `ChatHub`, 다음의 모의 버전을 만듭니다는 `broadcastMessage` 메서드를 호출 하 여 호출 되는 `Send` 허브에서 메서드.
3. 키를 눌러 솔루션을 빌드합니다 **F6**합니다.
4. 단위 테스트를 실행합니다. Visual Studio에서 선택 **테스트**, **Windows**, **테스트 탐색기**합니다. 테스트 탐색기 창에서 마우스 오른쪽 단추로 클릭 **HubsAreMockableViaDynamic** 선택 **선택 된 테스트 실행**합니다.

    ![테스트 탐색기](unit-testing-signalr-applications/_static/image7.png)
5. 테스트 탐색기 창의 아래쪽 창 확인 하 여 테스트에 통과 했는지 확인 합니다. 창에서 테스트를 통과 했음이 표시 됩니다.

    ![테스트 통과](unit-testing-signalr-applications/_static/image8.png)
