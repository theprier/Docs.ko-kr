---
title: SignalR에서 ASP.NET Core 시작
author: rachelappel
description: 이 자습서에서는 ASP.NET Core 용 SignalR을 사용 하 여 응용 프로그램을 만듭니다.
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: rachelap
ms.custom: mvc
ms.date: 05/22/2018
ms.prod: aspnet-core
ms.topic: tutorial
ms.technology: aspnet
uid: signalr/get-started
ms.openlocfilehash: 880abd87805990baf8dd977c340a60582e54d2df
ms.sourcegitcommit: 43bd79667bbdc8a07bd39fb4cd6f7ad3e70212fb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34729505"
---
# <a name="get-started-with-signalr-on-aspnet-core"></a>SignalR에서 ASP.NET Core 시작

작성자: [Rachel Appel](https://twitter.com/rachelappel)

이 자습서의 ASP.NET Core 용 SignalR을 사용 하 여 실시간 앱 빌드 기본 사항에 설명 합니다.

   ![솔루션](get-started/_static/signalr-get-started-finished.png)

이 자습서에서는 다음 SignalR 개발 작업을 보여 줍니다.

> [!div class="checklist"]
> * ASP.NET Core 웹 앱에는 SignalR을 만듭니다.
> * 클라이언트에 콘텐츠를 푸시 하려면 SignalR 허브를 만듭니다.
> * 수정 된 `Startup` 클래스 및 응용 프로그램을 구성 합니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/get-started/sample/)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

# <a name="prerequisites"></a>전제 조건

다음 소프트웨어를 설치 합니다.

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

* [.NET core SDK 2.1 이상](https://www.microsoft.com/net/download/all)
* [Visual Studio 2017](https://www.visualstudio.com/downloads/) 15.7 이상 버전에서 **ASP.NET 및 웹 개발** 작업
* [npm](https://www.npmjs.com/get-npm)

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code)

* [.NET core SDK 2.1 이상](https://www.microsoft.com/net/download/all)
* [Visual Studio Code](https://code.visualstudio.com/download)
* [Visual Studio 코드에 대 한 C#](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)
* [npm](https://www.npmjs.com/get-npm)

-----

## <a name="create-an-aspnet-core-project-that-hosts-signalr-client-and-server"></a>SignalR 클라이언트와 서버를 호스팅하는 ASP.NET Core 프로젝트 만들기

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio/)

1. 사용 하 여는 **파일** > **새 프로젝트** 메뉴 옵션 선택한 **ASP.NET Core 웹 응용 프로그램**합니다. 프로젝트 이름을 *SignalRChat*합니다.

   ![Visual Studio에서 새 프로젝트 대화 상자](get-started/_static/signalr-new-project-dialog.png)

2. 선택 **웹 응용 프로그램** Razor 페이지를 사용 하 여 프로젝트를 만듭니다. 그런 다음 선택 **확인**합니다. 수 있도록 **ASP.NET Core 2.1** SignalR 이전 버전의.NET에서 실행 하는 경우 프레임 워크 선택기에서 선택 합니다.

   ![Visual Studio에서 새 프로젝트 대화 상자](get-started/_static/signalr-new-project-choose-type.png)

Visual Studio에 포함 되어는 `Microsoft.AspNetCore.SignalR` 서버 라이브러리의 일부로 포함 된 패키지의 **ASP.NET Core 웹 응용 프로그램** 템플릿. 그러나 SignalR 용 JavaScript 클라이언트 라이브러리 해야 설치를 사용 하 여 *npm*합니다.

3. 다음 명령을 실행 하는 **패키지 관리자 콘솔** 프로젝트 루트에서 창:

    ```console
    npm init -y
    npm install @aspnet/signalr
    ```     

4. 내부 "signalr" 라는 새 폴더 만들기는 *lib* 프로젝트의 폴더에에서 있습니다. 그런 다음 복사는 *signalr.js* 에서 파일을 *node_modules\\ @aspnet\signalr\dist\browser*  이 폴더에 있습니다.

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code/)

1. **통합 터미널**, 다음 명령을 실행 합니다.

    ```console
    dotnet new webapp -o SignalRChat
    ```

2. 사용 하 여 JavaScript 클라이언트 라이브러리를 설치 *npm*합니다.

    ```console
    npm init -y
    npm install @aspnet/signalr
    ```

3. 복사는 *signalr.js* 에서 파일을 *node_modules\\ @aspnet\signalr\dist\browser*  에 *lib* 프로젝트의 폴더에에서 있습니다.

-----

## <a name="create-the-signalr-hub"></a>SignalR 허브를 만듭니다.

허브는 클라이언트와 서버에서 다른 메서드를 호출할 수 있도록 하는 높은 수준의 파이프라인으로 사용 되는 클래스입니다.

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio/)

1. 클래스를 선택 하 여 프로젝트에 추가 **파일** > **새로** > **파일** 선택 하 고 **Visual C# 클래스**합니다. 파일 이름을 *ChatHub*합니다. 

2. 상속 `Microsoft.AspNetCore.SignalR.Hub`합니다. `Hub` 속성과 송신 및 수신 데이터 뿐 아니라 연결 그룹을 관리 하기 위한 이벤트 클래스를 포함 합니다.

3. 만들기는 `SendMessage` 모든 연결 된 채팅 클라이언트에 메시지를 보내는 방법입니다. 반환 확인는 [작업](https://msdn.microsoft.com/library/system.threading.tasks.task(v=vs.110).aspx)SignalR 비동기 이기 때문에 있습니다. 비동기 코드 확장성이 좋아집니다.

   [!code-csharp[Startup](get-started/sample/Hubs/ChatHub.cs)]

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code/)

1. 열기는 *SignalRChat* Visual Studio Code에서 폴더입니다.

2. 클래스를 선택 하 여 프로젝트에 추가 **파일** > **새 파일** 메뉴에서 합니다.

3. 상속 `Microsoft.AspNetCore.SignalR.Hub`합니다. `Hub` 속성 및 이벤트 데이터를 클라이언트로 보내는 소켓과 받는 뿐 아니라 연결 그룹을 관리 하기 위한 클래스를 포함 합니다.

4. 클래스에 `SendMessage` 메서드를 추가합니다. `SendMessage` 메서드는 모든 연결 된 채팅 클라이언트에 메시지를 보냅니다. 반환 확인는 [작업](/dotnet/api/system.threading.tasks.task)SignalR 비동기 이기 때문에 있습니다. 비동기 코드 확장성이 좋아집니다.

   [!code-csharp[Startup](get-started/sample/Hubs/ChatHub.cs?range=6-12)]

-----

## <a name="configure-the-project-to-use-signalr"></a>SignalR을 사용 하도록 프로젝트를 구성 합니다.

SignalR 서버 signalr 요청을 전달 하려면 알 수 있도록 구성 되어야 합니다.

1. SignalR 프로젝트를 구성 하려면 프로젝트의 수정 `Startup.ConfigureServices` 메서드.

   `services.AddSignalR` SignalR의 일부로 추가 [미들웨어](xref:fundamentals/middleware/index) 파이프라인.

2. 사용 하 여 허브에 대 한 라우팅을 구성 `UseSignalR`합니다.


   [!code-csharp[Startup](get-started/sample/Startup.cs?highlight=37,57-60)]


## <a name="create-the-signalr-client-code"></a>SignalR 클라이언트 코드 만들기

1. 에서는 교체 *Pages\Index.cshtml* 를 다음 코드로:

   [!code-cshtml[Index](get-started/sample/Pages/Index.cshtml)]

   위의 HTML 이름 및 메시지 필드 및 전송 단추가 표시 됩니다. 맨 아래에 스크립트 참조를 확인: SignalR에 대 한 참조 및 *chat.js*합니다.

2. 명명 된 JavaScript 파일을 추가 *chat.js*을 *wwwroot\js* 폴더입니다. 파일에 다음 코드를 추가합니다.

   [!code-javascript[Index](get-started/sample/wwwroot/js/chat.js)]

## <a name="run-the-app"></a>앱 실행

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

1. 선택 **디버그** > **디버깅 하지 않고 시작** 브라우저를 실행 하 여 로컬 웹 사이트를 로드 합니다. 주소 표시줄에서 URL을 복사 합니다.

1. 다른 브라우저 인스턴스 (모든 브라우저)를 열고 주소 표시줄에 URL을 붙여 넣습니다.

1. 브라우저 중 하나를 선택 하 고, 이름 및 메시지를 입력 한 다음 클릭는 **보낼** 단추입니다. 이름 및 메시지는 두 페이지에 즉시 표시 됩니다.

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code)

1. **디버그**(F5) 키를 눌러 프로그램을 빌드하고 실행합니다. 프로그램을 실행 브라우저 창을 엽니다.

1. 다른 브라우저 창을 열고에서 로컬로 웹 사이트를 로드 합니다.

1. 브라우저 중 하나를 선택 하 고, 이름 및 메시지를 입력 한 다음 클릭는 **보낼** 단추입니다. 이름 및 메시지는 두 페이지에 즉시 표시 됩니다.

---

  ![솔루션](get-started/_static/signalr-get-started-finished.png)

## <a name="related-resources"></a>관련 참고 자료

[ASP.NET Core SignalR 소개](introduction.md)
