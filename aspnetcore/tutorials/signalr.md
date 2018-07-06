---
title: ASP.NET Core에서 SignalR 시작
author: rachelappel
description: 이 자습서에서는 ASP.NET Core용 SignalR을 사용하여 앱을 만듭니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: rachelap
ms.custom: mvc
ms.date: 05/22/2018
uid: tutorials/signalr
ms.openlocfilehash: ca9145d9e16c23e34bbc1d84ff01ce02709187ce
ms.sourcegitcommit: 08f1a9baa97060da5168840b332c9c0805b5f901
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37144874"
---
# <a name="get-started-with-signalr-on-aspnet-core"></a>ASP.NET Core에서 SignalR 시작

작성자: [Rachel Appel](https://twitter.com/rachelappel)

이 자습서에서는 ASP.NET Core용 SignalR을 사용하여 실시간 앱을 빌드하는 방법에 대한 기본 사항을 설명합니다.

   ![솔루션](signalr/_static/signalr-get-started-finished.png)

이 자습서에서는 다음과 같은 SignalR 개발 작업을 설명합니다.

> [!div class="checklist"]
> * ASP.NET Core 웹앱에서 SignalR을 만듭니다.
> * 클라이언트에 콘텐츠를 푸시하는 SignalR Hub를 만듭니다.
> * `Startup` 클래스를 수정하고 앱을 구성합니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/signalr/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

## <a name="prerequisites"></a>전제 조건

다음 소프트웨어를 설치합니다.

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

* [.NET Core SDK 2.1 이상](https://www.microsoft.com/net/download/all)
* [Visual Studio 2017](https://www.visualstudio.com/downloads/) 버전 15.7 이상(**ASP.NET 및 웹 개발** 워크로드 포함)
* [npm](https://www.npmjs.com/get-npm)

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code)

* [.NET Core SDK 2.1 이상](https://www.microsoft.com/net/download/all)
* [Visual Studio Code](https://code.visualstudio.com/download)
* [Visual Studio Code용 C#](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)
* [npm](https://www.npmjs.com/get-npm)

-----

## <a name="create-an-aspnet-core-project-that-hosts-signalr-client-and-server"></a>SignalR 클라이언트와 서버를 호스팅하는 ASP.NET Core 프로젝트 만들기

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio/)

1. **파일** > **새 프로젝트** 메뉴 옵션을 사용하고 **ASP.NET Core 웹 응용 프로그램**을 선택합니다. 프로젝트의 이름을 *SignalRChat*로 지정합니다.

   ![Visual Studio의 새 프로젝트 대화 상자](signalr/_static/signalr-new-project-dialog.png)

2. Razor Pages를 사용하여 프로젝트를 생성하려면 **웹 응용 프로그램**을 선택합니다. 그런 다음, **확인**을 선택합니다. SignalR이 이전 버전의 .NET에서 실행되는 경우에도 프레임워크 선택기에서 **ASP.NET Core 2.1**을 선택해야 합니다.

   ![Visual Studio의 새 프로젝트 대화 상자](signalr/_static/signalr-new-project-choose-type.png)

Visual Studio에는 **ASP.NET Core 웹 응용 프로그램** 템플릿의 일부로 서버 라이브러리가 포함된 `Microsoft.AspNetCore.SignalR` 패키지가 포함되어 있습니다. 그러나 SignalR용 JavaScript 클라이언트 라이브러리는 *npm*을 사용하여 설치해야 합니다.

3. **패키지 관리자 콘솔** 창의 프로젝트 루트에서 다음 명령을 실행합니다.

    ```console
    npm init -y
    npm install @aspnet/signalr
    ```

4. 프로젝트의 *lib* 폴더 안에 "signalr"라는 새 폴더를 만듭니다. *signalr.js* 파일을 *node_modules\\@aspnet\signalr\dist\browser*에서 이 폴더로 복사합니다.

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code/)

1. **통합 터미널**에서 다음 명령을 실행합니다.

    ```console
    dotnet new webapp -o SignalRChat
    ```

    [!INCLUDE[](~/includes/webapp-alias-notice.md)]

2. *npm*을 사용하여 JavaScript 클라이언트 라이브러리를 설치합니다.

    ```console
    npm init -y
    npm install @aspnet/signalr
    ```

3. 프로젝트의 *lib* 폴더 안에 "signalr"라는 새 폴더를 만듭니다. *signalr.js* 파일을 *node_modules\\@aspnet\signalr\dist\browser*에서 이 폴더로 복사합니다.

---

## <a name="create-the-signalr-hub"></a>SignalR Hub 만들기

허브는 클라이언트와 서버가 서로 메서드를 호출할 수 있도록 하는 높은 수준의 파이프라인 역할을 하는 클래스입니다.

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio/)

1. **파일** > **새로 만들기** > **파일**을 선택하고 **Visual C# 클래스**를 선택하여 클래스를 프로젝트에 추가합니다. `ChatHub` 클래스 및 *ChatHub.cs* 파일의 이름을 지정합니다.

2. `Microsoft.AspNetCore.SignalR.Hub`에서 상속합니다. `Hub` 클래스는 데이터 전송 및 수신뿐만 아니라, 연결 및 그룹 관리를 위한 속성 및 이벤트도 포함합니다.

3. 연결된 모든 채팅 클라이언트에 메시지를 보내는 `SendMessage` 메서드를 만듭니다. SignalR은 비동기이기 때문에 [작업](https://msdn.microsoft.com/library/system.threading.tasks.task(v=vs.110).aspx)을 반환합니다. 비동기 코드는 더 잘 확장됩니다.

   [!code-csharp[Startup](signalr/sample/Hubs/ChatHub.cs)]

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code/)

1. Visual Studio Code에서 *SignalRChat* 폴더를 엽니다.

2. 메뉴에서 **파일** > **새 파일**을 선택하여 프로젝트에 클래스를 추가합니다. `ChatHub` 클래스 및 *ChatHub.cs* 파일의 이름을 지정합니다.

3. `Microsoft.AspNetCore.SignalR.Hub`에서 상속합니다. `Hub` 클래스는 클라이언트에 대한 데이터 전송 및 수신뿐만 아니라, 연결 및 그룹 관리를 위한 속성 및 이벤트를 포함합니다.

4. 클래스에 `SendMessage` 메서드를 추가합니다. `SendMessage` 메서드는 연결된 모든 채팅 클라이언트에 메시지를 보냅니다. SignalR은 비동기이기 때문에 [작업](/dotnet/api/system.threading.tasks.task)을 반환합니다. 비동기 코드는 더 잘 확장됩니다.

   [!code-csharp[Startup](signalr/sample/Hubs/ChatHub.cs)]

-----

## <a name="configure-the-project-to-use-signalr"></a>SignalR을 사용하도록 프로젝트 구성

SignalR 서버는 SignalR에 요청을 전달할 수 있도록 구성되어야 합니다.

1. SignalR 프로젝트를 구성하려면 프로젝트의 `Startup.ConfigureServices` 메서드를 수정합니다.

   `services.AddSignalR`을 통해 [종속성 주입](xref:fundamentals/dependency-injection) 시스템에 SignalR 서비스를 사용할 수 있습니다.

1. `Configure` 메서드에서 `UseSignalR`을 사용하여 허브에 대한 경로를 구성합니다. `app.UseSignalR`은 [미들웨어](xref:fundamentals/middleware/index) 파이프라인에 SignalR을 추가합니다.

   [!code-csharp[Startup](signalr/sample/Startup.cs?highlight=37,57-60)]

## <a name="create-the-signalr-client-code"></a>SignalR 클라이언트 코드 만들기

1. *chat.js*라는 JavaScript 파일을 *wwwroot\js* 폴더에 추가합니다. 파일에 다음 코드를 추가합니다.

   [!code-javascript[Index](signalr/sample/wwwroot/js/chat.js)]

2. *Pages\Index.cshtml*의 콘텐츠를 다음 코드로 바꿉니다.

   [!code-cshtml[Index](signalr/sample/Pages/Index.cshtml)]

   앞의 HTML에는 이름과 메시지 필드 및 제출 단추가 표시됩니다. 맨 아래에 있는 스크립트 참조(SignalR 및 *chat.js*에 대한 참조)를 확인합니다.

## <a name="run-the-app"></a>앱 실행

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

1. **디버그** > **디버깅 없이 시작**을 선택하여 브라우저를 실행하고 웹 사이트를 로컬로 로드합니다. 주소 표시줄에서 URL을 복사합니다.

1. 다른 브라우저 인스턴스(모든 브라우저)를 열고 주소 표시줄에 URL을 붙여 넣습니다.

1. 브라우저 중 하나를 선택하고 이름과 메시지를 입력한 후, **보내기** 단추를 클릭합니다. 이름과 메시지는 두 페이지 모두에 즉시 표시됩니다.

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code)

1. **디버그**(F5) 키를 눌러 프로그램을 빌드하고 실행합니다. 프로그램을 실행하면 브라우저 창이 열립니다.

1. 다른 브라우저 창을 열고 웹 사이트를 로컬로 로드합니다.

1. 브라우저 중 하나를 선택하고 이름과 메시지를 입력한 후, **보내기** 단추를 클릭합니다. 이름과 메시지는 두 페이지 모두에 즉시 표시됩니다.

---

  ![솔루션](signalr/_static/signalr-get-started-finished.png)

## <a name="related-resources"></a>관련 참고 자료

[ASP.NET Core SignalR 소개](xref:signalr/introduction)
