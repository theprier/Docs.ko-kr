---
title: '자습서: ASP.NET Core에서 SignalR 시작'
author: tdykstra
description: 이 자습서에서는 ASP.NET Core용 SignalR을 사용하는 채팅 앱을 만듭니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 08/20/2018
uid: tutorials/signalr
ms.openlocfilehash: db7f31963f6a4280069f1f4f82a547e2879e64bb
ms.sourcegitcommit: d27317c16f113e7c111583042ec7e4c5a26adf6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2018
ms.locfileid: "41751696"
---
# <a name="tutorial-get-started-with-signalr-on-aspnet-core"></a>자습서: ASP.NET Core에서 SignalR 시작

이 자습서에서는 SignalR을 사용하여 실시간 앱을 빌드하는 방법에 대한 기본 사항을 설명합니다. 여기에서는 다음과 같은 작업을 수행하는 방법에 대해 배우게 됩니다.

> [!div class="checklist"]
> * ASP.NET Core에서 SignalR을 사용하는 웹앱을 만듭니다.
> * 서버에서 SignalR 허브를 만듭니다.
> * JavaScript 클라이언트에서 SignalR 허브에 연결합니다.
> * 허브를 사용하여 모든 클라이언트에서 연결된 모든 클라이언트에 메시지를 보냅니다.

작동하는 채팅 앱이 만들어집니다.

![SignalR 샘플 앱](signalr/_static/signalr-get-started-finished.png)

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/signalr/sample) ([다운로드 방법](xref:tutorials/index#how-to-download-a-sample)).

## <a name="prerequisites"></a>전제 조건

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

* [Visual Studio 2017 버전 15.7.3 이상](https://www.visualstudio.com/downloads/)(**ASP.NET 및 웹 개발** 워크로드 포함)
* [.NET Core SDK 2.1 이상](https://www.microsoft.com/net/download/all)
* [npm](https://www.npmjs.com/get-npm)(SignalR JavaScript 클라이언트 라이브러리에 사용되는 Node.js용 패키지 관리자)

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code)

* [Visual Studio Code](https://code.visualstudio.com/download)
* [.NET Core SDK 2.1 이상](https://www.microsoft.com/net/download/all)
* [Visual Studio Code용 C#](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)
* [npm](https://www.npmjs.com/get-npm)(SignalR JavaScript 클라이언트 라이브러리에 사용되는 Node.js용 패키지 관리자)

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[Visual Studio for Mac](#tab/visual-studio-mac)

* [Mac용 Visual Studio 버전 7.5.4 이상](https://www.visualstudio.com/downloads/)
* [.NET Core SDK 2.1 이상](https://www.microsoft.com/net/download/all)(Visual Studio 설치에 포함됨)
* [npm](https://www.npmjs.com/get-npm)(SignalR JavaScript 클라이언트 라이브러리에 사용되는 Node.js용 패키지 관리자)

---

## <a name="create-the-project"></a>프로젝트를 만듭니다.

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio/)

* 메뉴에서 **파일 > 새 프로젝트**를 선택합니다.

* **새 프로젝트** 대화 상자에서 **설치됨 > Visual C# > 웹 > ASP.NET Core 웹 응용 프로그램**을 선택합니다. 프로젝트의 이름을 *SignalRChat*로 지정합니다.

  ![Visual Studio의 새 프로젝트 대화 상자](signalr/_static/signalr-new-project-dialog.png)

* Razor Pages를 사용하는 프로젝트를 생성하려면 **웹 응용 프로그램**을 선택합니다.

* **.NET Core**의 대상 프레임워크를 선택하고, **ASP.NET Core 2.1**을 선택하고, **확인**을 클릭합니다.

  ![Visual Studio의 새 프로젝트 대화 상자](signalr/_static/signalr-new-project-choose-type.png)

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code/)

* 새 프로젝트에 사용할 수 있는 폴더를 엽니다.

* **통합 터미널**에서 다음 명령을 실행합니다.

   ```console
   dotnet new webapp -o SignalRChat
   ```

   [!INCLUDE[](~/includes/webapp-alias-notice.md)]

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[Visual Studio for Mac](#tab/visual-studio-mac)

* 메뉴에서 **파일 > 새 솔루션**을 선택합니다.

* **.NET Core > 앱 > ASP.NET Core 웹앱**(**ASP.NET Core 웹앱(MVC) 선택 안 함**)을 선택합니다.

* **새로 만들기**를 선택합니다.

* 프로젝트 이름을 *SignalRChat*으로 지정한 다음, **만들기**를 선택합니다.

---

## <a name="add-the-signalr-client-library"></a>SignalR 클라이언트 라이브러리 추가

SignalR 서버 라이브러리는 [Microsoft.AspNetCore.App 메타패키지](xref:fundamentals/metapackage-app)에 포함되어 있습니다. 하지만 npm, Node.js 패키지 관리자에서 JavaScript 클라이언트 라이브러리를 가져와야 합니다.

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio/)

* **패키지 관리자 콘솔**(PMC)에서 프로젝트 폴더로 변경합니다(*SignalRChat.csproj* 파일을 포함하는 폴더).

  ```console
  cd SignalRChat
  ```

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code/)

2. 새 프로젝트 폴더로 변경합니다.

  ```console
  cd SignalRChat
  ``` 

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[Visual Studio for Mac](#tab/visual-studio-mac)

* **터미널**에서 프로젝트 폴더로 이동합니다(*SignalRChat.csproj* 파일을 포함하는 폴더).

---

* npm 이니셜라이저를 실행하여 *package.json* 파일을 만듭니다.

  ```console
  npm init -y
  ```

  명령은 다음 예제와 유사한 출력을 만듭니다.

  ```console
  Wrote to C:\tmp\SignalRChat\package.json:
  {
    "name": "SignalRChat",
    "version": "1.0.0",
    "description": "",
    "main": "index.js",
    "scripts": {
      "test": "echo \"Error: no test specified\" && exit 1"
    },
    "keywords": [],
    "author": "",
    "license": "ISC"0
  }
  ```

* 클라이언트 라이브러리 패키지를 설치합니다.

  ```console
  npm install @aspnet/signalr
  ```

  명령은 다음 예제와 유사한 출력을 만듭니다.

  ```
  npm notice created a lockfile as package-lock.json. You should commit this file.
  npm WARN signalrchat@1.0.0 No description
  npm WARN signalrchat@1.0.0 No repository field.

  + @aspnet/signalr@1.0.2
  added 1 package in 0.98s
  ```

`npm install` 명령은 *node_modules* 아래의 하위 폴더에 JavaScript 클라이언트 라이브러리를 다운로드했습니다. 여기에서 채팅 앱 웹 페이지에서 참조할 수 있는 *wwwroot* 아래의 폴더에 복사합니다.

* *wwwroot/lib*에 *signalr* 폴더를 만듭니다.

* *node_modules/@aspnet/signalr/dist/browser*에서 새 *wwwroot/lib/signalr* 폴더로 *signalr.js* 파일을 복사합니다.

## <a name="create-the-signalr-hub"></a>SignalR 허브 만들기

[허브](xref:signalr/hubs)는 클라이언트-서버 통신을 처리하는 높은 수준의 파이프라인으로 제공되는 클래스입니다.

* SignalRChat 프로젝트 폴더에서 *Hubs* 폴더를 만듭니다.

* *Hubs* 폴더에 다음 코드를 사용하여 *ChatHub.cs* 파일을 만듭니다.

  [!code-csharp[Startup](signalr/sample/Hubs/ChatHub.cs)]

  `ChatHub` 클래스는 SignalR [Hub](/dotnet/api/microsoft.aspnetcore.signalr.hub) 클래스에서 상속합니다. `Hub` 클래스는 연결, 그룹 및 메시징을 관리합니다.

  연결된 모든 클라이언트에서 `SendMessage` 메서드를 호출할 수 있습니다. 모든 클라이언트에 수신된 메시지를 보냅니다. SignalR 코드는 최대 확장성을 제공하도록 비동기적입니다.

## <a name="configure-the-project-to-use-signalr"></a>SignalR을 사용하도록 프로젝트 구성

SignalR 서버는 SignalR에 SignalR 요청을 전달하도록 구성되어야 합니다.

* 다음 강조 표시된 코드를 *Startup.cs* 파일에 추가합니다.

  [!code-csharp[Startup](signalr/sample/Startup.cs?highlight=7,33,52-55)]

  이러한 변경 사항은 [종속성 주입](xref:fundamentals/dependency-injection) 시스템 및 [미들웨어](xref:fundamentals/middleware/index) 파이프라인에 SignalR을 추가합니다.

## <a name="create-the-signalr-client-code"></a>SignalR 클라이언트 코드 만들기

* *Pages\Index.cshtml*의 콘텐츠를 다음으로 바꿉니다.

  [!code-cshtml[Index](signalr/sample/Pages/Index.cshtml)]

  위의 코드:

  * 이름 및 메시지 텍스트에 대한 텍스트 상자 및 전송 단추를 만듭니다.
  * SignalR 허브에서 받은 메시지를 표시하기 위해 `id="messagesList"`를 사용하여 목록을 만듭니다.
  * SignalR에 대한 스크립트 참조 및 다음 단계에서 만드는 *chat.js* 응용 프로그램 코드를 포함합니다.

* *wwwroot/js* 폴더에서 다음 코드를 사용하여 *chat.js* 파일을 만듭니다.

  [!code-javascript[Index](signalr/sample/wwwroot/js/chat.js)]

  위의 코드:

  * 연결을 만들고 시작합니다.
  * 허브에 메시지를 전송하는 처리기를 전송 단추에 추가합니다.
  * 허브에서 메시지를 수신하고 목록에 추가하는 처리기를 연결 개체에 추가합니다.

## <a name="run-the-app"></a>앱 실행

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

* **CTRL+F5** 키를 눌러 디버깅 없이 앱을 실행합니다.

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code)

* **CTRL+F5** 키를 눌러 디버깅 없이 앱을 실행합니다.

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[Visual Studio for Mac](#tab/visual-studio-mac)

* 메뉴에서 **실행 > 디버깅하지 않고 시작**을 선택합니다.

---

* 주소 표시줄에서 URL을 복사하고, 다른 브라우저 인스턴스 또는 탭을 열고, 주소 표시줄에 URL을 붙여넣습니다.

* 브라우저 중 하나를 선택하고, 이름 및 메시지를 입력하고, **보내기** 단추를 선택합니다.

  이름과 메시지는 두 페이지 모두에 즉시 표시됩니다.

  ![SignalR 샘플 앱](signalr/_static/signalr-get-started-finished.png)

> [!TIP]
> 앱이 작동하지 않는 경우 브라우저 개발자 도구(F12)를 열고 콘솔로 이동합니다. HTML 및 JavaScript 코드와 관련된 오류를 볼 수 있습니다. 예를 들어 지정되지 않은 다른 폴더에 *signalr.js*를 넣었다고 가정합니다. 이 경우 해당 파일에 대한 참조는 작동하지 않으며 콘솔에 404 오류가 표시됩니다.
> ![signalr.js 찾을 수 없음 오류](signalr/_static/f12-console.png)

## <a name="next-steps"></a>다음 단계

클라이언트를 다른 도메인의 SignalR 앱에 연결하려는 경우 CORS(원본 간 리소스 공유)를 활성화해야 합니다. 자세한 내용은 [원본 간 리소스 공유](xref:signalr/security?view=aspnetcore-2.1#cross-origin-resource-sharing)를 참조하세요.

SignalR, 허브 및 JavaScript 클라이언트에 대해 자세히 알아보려면 다음 리소스를 참조하세요.

* [ASP.NET Core용 SignalR 소개](xref:signalr/introduction)
* [ASP.NET Core용 SignalR에서 허브 사용](xref:signalr/hubs)
* [ASP.NET Core SignalR JavaScript 클라이언트](xref:signalr/javascript-client)
