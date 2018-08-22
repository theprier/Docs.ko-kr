---
uid: signalr/overview/testing-and-debugging/unit-testing-signalr-applications
title: SignalR 응용 프로그램 유닛 테스트 | Microsoft Docs
author: pfletcher
description: 이 문서에는 SignalR 2.0의 단위 테스트 기능을 사용 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 06/10/2014
ms.assetid: d1983524-e0d5-4ee6-9d87-1f552f7cb964
msc.legacyurl: /signalr/overview/testing-and-debugging/unit-testing-signalr-applications
msc.type: authoredcontent
ms.openlocfilehash: c6c57026a54775857921075b176e893b5449d4a5
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41832289"
---
<a name="unit-testing-signalr-applications"></a>SignalR Applications 단위 테스트
====================
[Patrick Fletcher](https://github.com/pfletcher)

> 이 문서에서는 SignalR 2의 단위 테스트 기능을 사용 하 여 설명 합니다. 
> 
> ## <a name="software-versions-used-in-this-topic"></a>이 항목에서 사용 하는 소프트웨어 버전
> 
> 
> - [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - .NET 4.5
> - SignalR 버전 2
>   
> 
> 
> ## <a name="questions-and-comments"></a>질문이 나 의견이 있으면
> 
> 이 자습서를 연결 하는 방법 및 새로운 개선할 수 있습니다 페이지의 맨 아래에 의견에서에 의견을 남겨 주세요. 에 자습서로 직접 관련 되지 않은 질문이 있을 경우 게시할 수 하는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)합니다.


<a id="unit"></a>
## <a name="unit-testing-signalr-applications"></a>SignalR 응용 프로그램 유닛 테스트

SignalR 응용 프로그램에 대 한 단위 테스트를 만들려면 SignalR 2에서 단위 테스트 기능을 사용할 수 있습니다. SignalR 2를 포함 합니다 [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) 인터페이스 테스트를 위한 허브 메서드를 시뮬레이션 하기 위해 모의 개체를 만드는 데 사용할 수 있습니다.

이 섹션에서는에서 만든 응용 프로그램에 대 한 단위 테스트 추가 합니다 [시작 자습서](../getting-started/tutorial-getting-started-with-signalr.md) 를 사용 하 여 [XUnit.net](https://github.com/xunit/xunit) 하 고 [Moq](https://github.com/Moq/moq4)합니다.

XUnit.net는 테스트를 제어 하는 Moq를 만들 수는 [모의](http://en.wikipedia.org/wiki/Mock_object) 테스트에 대 한 개체입니다. 필요한 경우 다른 모의 프레임 워크를 사용할 수 있습니다. [NSubstitute](http://nsubstitute.github.io/) 적합 한 선택 이기도 합니다. 이 자습서에서는 두 가지 방법으로 모의 개체를 설정 하는 방법을 보여 줍니다: 첫 번째를 사용 하는 `dynamic` (.NET Framework 4에 도입 된), 개체 및 인터페이스를 사용 하 여 두 번째입니다.

### <a name="contents"></a>목차

이 자습서는 다음 섹션이 포함 되어 있습니다.

- [동적을 사용한 단위 테스트](#dynamic)
- [단위 형식으로 테스트](#type)

<a id="dynamic"></a>
### <a name="unit-testing-with-dynamic"></a>동적을 사용한 단위 테스트

이 섹션에서는에서 만든 응용 프로그램에 대 한 단위 테스트를 추가 합니다 [시작 자습서](../getting-started/tutorial-getting-started-with-signalr.md) 동적 개체를 사용 하 여 합니다.

1. 설치 합니다 [XUnit Runner 확장](https://visualstudiogallery.msdn.microsoft.com/463c5987-f82b-46c8-a97e-b1cde42b9099) Visual Studio 2013 용입니다.
2. 완료 하거나 합니다 [시작 자습서](../getting-started/tutorial-getting-started-with-signalr.md)에서 완성된 된 응용 프로그램을 다운로드 하거나 [MSDN 코드 갤러리](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)합니다.
3. 시작 응용 프로그램의 버전 다운로드를 사용 하는 경우 열 **패키지 관리자 콘솔** 클릭 **복원** SignalR 패키지를 프로젝트에 추가 합니다.

    ![패키지 복원](unit-testing-signalr-applications/_static/image1.png)
4. 솔루션에 단위 테스트 프로젝트를 추가 합니다. 솔루션을 마우스 오른쪽 단추로 클릭 **솔루션 탐색기** 선택한 **추가**, **새 프로젝트...** . 아래는 **C#** 노드를 선택 합니다 **Windows** 노드. 선택 **클래스 라이브러리**합니다. 새 프로젝트의 이름을 **TestLibrary** 누릅니다 **확인**합니다.

    ![테스트 라이브러리 만들기](unit-testing-signalr-applications/_static/image2.png)
5. SignalRChat 프로젝트에 테스트 라이브러리 프로젝트에 대 한 참조를 추가 합니다. 마우스 오른쪽 단추로 클릭 합니다 **TestLibrary** 프로젝트를 마우스 **추가**, **참조 하는 중...** . 선택 된 **프로젝트** 노드에서 **솔루션** 노드와 확인 **SignalRChat**합니다. **확인**을 클릭합니다.

    ![프로젝트 참조 추가](unit-testing-signalr-applications/_static/image3.png)
6. SignalR, Moq 및 XUnit 패키지를 추가 합니다 **TestLibrary** 프로젝트입니다. 에 **패키지 관리자 콘솔**설정 합니다 **기본 프로젝트** 드롭다운을 **TestLibrary**. 콘솔 창에서 다음 명령을 실행 합니다.

   - `Install-Package Microsoft.AspNet.SignalR`
   - `Install-Package Moq`
   - `Install-Package XUnit`

     ![패키지 설치](unit-testing-signalr-applications/_static/image4.png)
7. 테스트 파일을 만듭니다. 마우스 오른쪽 단추로 클릭 합니다 **TestLibrary** 프로젝트 및 클릭 **추가...** 하십시오 **클래스**합니다. 새 클래스 이름을 **Tests.cs**합니다.
8. Tests.cs의 내용을 다음 코드로 바꿉니다.

    [!code-csharp[Main](unit-testing-signalr-applications/samples/sample1.cs)]

    위의 코드에서 테스트 클라이언트를 사용 하 여 만들어집니다 합니다 `Mock` 에서 개체를 [Moq](https://github.com/Moq/moq4) 형식의 라이브러리 [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) (SignalR 2.1 할당 `dynamic` 유형에 대 한 매개 변수입니다.) `IHubCallerConnectionContext` 인터페이스는 프록시 개체는 클라이언트에서 메서드를 호출 합니다. 합니다 `broadcastMessage` 함수는 다음에 대해 정의 된 모의 클라이언트에서 호출할 수 있도록 합니다 `ChatHub` 클래스입니다. 테스트 엔진에서 호출 합니다 `Send` 메서드를 `ChatHub` 클래스를 호출 하는 모의 `broadcastMessage` 함수.
9. 키를 눌러 솔루션을 빌드합니다 **F6**합니다.
10. 단위 테스트를 실행합니다. Visual Studio에서 선택 **테스트**, **Windows**하십시오 **테스트 탐색기**합니다. 테스트 탐색기 창에서 마우스 오른쪽 단추로 클릭 **HubsAreMockableViaDynamic** 선택한 **선택한 테스트 실행**합니다.

    ![테스트 탐색기](unit-testing-signalr-applications/_static/image5.png)
11. 테스트 탐색기 창의 아래쪽 창에 확인 하 여 테스트를 통과 했음을 확인 합니다. 창의는 테스트를 통과 했음을 표시 됩니다.

    ![테스트 통과](unit-testing-signalr-applications/_static/image6.png)

<a id="type"></a>
### <a name="unit-testing-by-type"></a>단위 형식으로 테스트

이 섹션에서는에서 만든 응용 프로그램에 대 한 테스트를 추가 합니다 [시작 자습서](../getting-started/tutorial-getting-started-with-signalr.md) 테스트할 메서드가 포함 된 인터페이스를 사용 하 여 합니다.

1. 에 1 ~ 7 단계를 완료 합니다 [동적을 사용한 단위 테스트](#dynamic) 위의 자습서입니다.
2. Tests.cs의 내용을 다음 코드로 바꿉니다.

    [!code-csharp[Main](unit-testing-signalr-applications/samples/sample2.cs)]

    위의 코드에서 인터페이스 만들어집니다 서명의 정의 `broadcastMessage` 메서드 테스트 엔진에서는 모의 클라이언트를 만듭니다. 모의 클라이언트를 사용 하 여 만든은 `Mock` 형식의 개체 [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) (SignalR 2.1 할당 `dynamic` 형식 매개 변수.) `IHubCallerConnectionContext` 인터페이스는 프록시 개체는 클라이언트에서 메서드를 호출 합니다.

    테스트의 인스턴스를 만든 후 `ChatHub`을 모의 버전의 다음 만들고는 `broadcastMessage` 메서드를 호출 하 여 호출 되는 `Send` 허브 메서드.
3. 키를 눌러 솔루션을 빌드합니다 **F6**합니다.
4. 단위 테스트를 실행합니다. Visual Studio에서 선택 **테스트**, **Windows**하십시오 **테스트 탐색기**합니다. 테스트 탐색기 창에서 마우스 오른쪽 단추로 클릭 **HubsAreMockableViaDynamic** 선택한 **선택한 테스트 실행**합니다.

    ![테스트 탐색기](unit-testing-signalr-applications/_static/image7.png)
5. 테스트 탐색기 창의 아래쪽 창에 확인 하 여 테스트를 통과 했음을 확인 합니다. 창의는 테스트를 통과 했음을 표시 됩니다.

    ![테스트 통과](unit-testing-signalr-applications/_static/image8.png)
