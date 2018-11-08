---
title: ASP.NET Core SignalR 시작하기
author: tdykstra
description: 이 자습서에서는 ASP.NET Core SignalR을 사용하는 채팅 앱을 만듭니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 08/31/2018
uid: tutorials/signalr
ms.openlocfilehash: fcfe2fa6cc88b9eee1389e171fa5eb7711b4f14f
ms.sourcegitcommit: fc2486ddbeb15ab4969168d99b3fe0fbe91e8661
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/01/2018
ms.locfileid: "50758130"
---
# <a name="tutorial-get-started-with-aspnet-core-signalr"></a>자습서: ASP.NET Core SignalR 시작하기

본 자습서에서는 SignalR을 이용해서 실시간 앱을 구현하기 위한 기본 사항을 알려줍니다. 다음과 같은 작업을 수행하는 방법을 살펴봅니다.

> [!div class="checklist"]
> * 웹 프로젝트를 만듭니다.
> * SignalR 클라이언트 라이브러리를 추가합니다.
> * SignalR 허브를 만듭니다.
> * SignalR을 사용하도록 프로젝트를 구성합니다.
> * 모든 클라이언트에서 연결된 모든 클라이언트로 메시지를 전송하는 코드를 추가합니다.

이 모든 과정을 마치고 나면 동작하는 채팅 앱을 만들게 됩니다.

![SignalR 예제 앱](signalr/_static/signalr-get-started-finished.png)

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/signalr/sample) ([다운로드 방법](xref:index#how-to-download-a-sample))

## <a name="prerequisites"></a>전제 조건

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

* [Visual Studio 2017 버전 15.8 이상](https://www.visualstudio.com/downloads/) (**ASP.NET 및 웹 개발** 워크로드 필요)
* [.NET Core SDK 2.1 이상](https://www.microsoft.com/net/download/all)

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code)

* [Visual Studio Code](https://code.visualstudio.com/download)
* [.NET Core SDK 2.1 이상](https://www.microsoft.com/net/download/all)
* [C# for Visual Studio Code 확장](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[Visual Studio for Mac](#tab/visual-studio-mac)

* [Mac용 Visual Studio 버전 7.5.4 이상](https://www.visualstudio.com/downloads/)
* [.NET Core SDK 2.1 이상](https://www.microsoft.com/net/download/all) (Visual Studio 설치에 포함됨)

---

## <a name="create-a-web-project"></a>웹 프로젝트 만들기

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio/)

* 메뉴에서 **파일 > 새로 만들기 > 프로젝트**를 선택합니다.

* **새 프로젝트** 대화 상자에서 **설치됨 > Visual C# > 웹 > ASP.NET Core 웹 응용 프로그램**을 선택합니다. 프로젝트의 이름을 *SignalRChat*으로 지정합니다.

  ![Visual Studio의 새 프로젝트 대화 상자](signalr/_static/signalr-new-project-dialog.png)

* **웹 응용 프로그램**을 선택하여 Razor Pages를 사용하는 프로젝트를 생성합니다.

* 대상 프레임워크로 **.NET Core**를 선택하고, **ASP.NET Core 2.1**을 선택한 다음, **확인**을 클릭합니다.

  ![Visual Studio의 새 프로젝트 대화 상자](signalr/_static/signalr-new-project-choose-type.png)

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code/)

* 새 프로젝트에 사용할 수 있는 폴더를 엽니다.

* [통합 터미널](https://code.visualstudio.com/docs/editor/integrated-terminal)에서 다음 명령을 실행합니다.

   ```console
   dotnet new webapp -o SignalRChat
   ```

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[Visual Studio for Mac](#tab/visual-studio-mac)

* 메뉴에서 **파일 > 새 솔루션**을 선택합니다.

* **.NET Core > 앱 > ASP.NET Core 웹앱**을 선택합니다. (**ASP.NET Core 웹앱(MVC)**를 선택하지 마십시요.)

* **새로 만들기**를 선택합니다.

* 프로젝트의 이름을 *SignalRChat*으로 지정한 다음, **만들기**를 선택합니다.

---

## <a name="add-the-signalr-client-library"></a>SignalR 클라이언트 라이브러리 추가하기

SignalR 서버 라이브러리는 `Microsoft.AspNetCore.App` 메타패키지에 포함되어 있습니다. JavaScript 클라이언트 라이브러리는 프로젝트에 자동으로 포함되지 않습니다. 본 자습서에서는 라이브러리 관리자(LibMan)를 사용하여 *unpkg*에서 클라이언트 라이브러리를 가져옵니다. unpkg는 Node.js의 패키지 관리자인 npm에서 찾은 모든 내용을 전달할 수 있는 콘텐츠 배달 네트워크(CDN, Content Delivery Network)입니다.

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio/)

* **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 버튼으로 클릭하고 **추가** > **클라이언트 라이브러리 추가**를 선택합니다.

* **클라이언트 쪽 라이브러리 추가** 대화 상자에서 **공급자**로 **unpkg**를 선택합니다. 

* **라이브러리**에 `@aspnet/signalr@1`을 입력하고 미리 보기가 아닌 최신 버전을 선택합니다.

  ![클라이언트 쪽 라이브러리 추가 대화 상자 - 라이브러리 선택](signalr/_static/libman1.png)

* **특정 파일 선택**을 선택하고 *dist/browser* 폴더를 확장한 다음 *signalr.js* 및 *signalr.min.js*를 선택합니다.

* **대상 위치**를 *wwwroot/lib/signalr/*로 설정하고 **설치**를 선택합니다.

  ![클라이언트 쪽 라이브러리 추가 대화 상자 - 파일 및 대상 선택](signalr/_static/libman2.png)

  그러면 LibMan이 *wwwroot/lib/signalr* 폴더를 생성한 다음 여기에 선택한 파일을 복사합니다.

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code/)

* **통합 터미널**에서 다음 명령을 실행하여 LibMan을 설치합니다.

  ```console
  dotnet tool install -g Microsoft.Web.LibraryManager.Cli
  ```

* 프로젝트 폴더로 이동합니다(*SignalRChat.csproj* 파일을 포함하고 있는 폴더).

* 다음 명령을 실행하여 LibMan을 이용해서 SignalR 클라이언트 라이브러리를 가져옵니다. 출력이 표시되기 전에 잠시 기다려야 할 수도 있습니다.

  ```console
  libman install @aspnet/signalr -p unpkg -d wwwroot/lib/signalr --files dist/browser/signalr.js --files dist/browser/signalr.min.js
  ```

  이 명령의 매개 변수는 다음 옵션을 지정합니다.
  * unpkg 공급자를 사용합니다.
  * 파일을 *wwwroot/lib/signalr* 대상 위치로 복사합니다.
  * 지정된 파일만 복사합니다.

  출력 결과는 다음 예와 같습니다.

  ```console
  wwwroot/lib/signalr/dist/browser/signalr.js written to disk
  wwwroot/lib/signalr/dist/browser/signalr.min.js written to disk
  Installed library "@aspnet/signalr@1.0.3" to "wwwroot/lib/signalr"
  ```

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[Visual Studio for Mac](#tab/visual-studio-mac)

* **터미널**에서 다음 명령을 실행하여 LibMan을 설치합니다.

  ```console
  dotnet tool install -g Microsoft.Web.LibraryManager.Cli
  ```

* 프로젝트 폴더로 이동합니다(*SignalRChat.csproj* 파일을 포함하고 있는 폴더).

* 다음 명령을 실행하여 LibMan을 이용해서 SignalR 클라이언트 라이브러리를 가져옵니다.

  ```console
  libman install @aspnet/signalr -p unpkg -d wwwroot/lib/signalr --files dist/browser/signalr.js --files dist/browser/signalr.min.js
  ```

  이 명령의 매개 변수는 다음 옵션을 지정합니다.
  * unpkg 공급자를 사용합니다.
  * 파일을 *wwwroot/lib/signalr* 대상 위치로 복사합니다.
  * 지정된 파일만 복사합니다.

  출력 결과는 다음 예와 같습니다.

  ```console
  wwwroot/lib/signalr/dist/browser/signalr.js written to disk
  wwwroot/lib/signalr/dist/browser/signalr.min.js written to disk
  Installed library "@aspnet/signalr@1.0.3" to "wwwroot/lib/signalr"
  ```

---

## <a name="create-a-signalr-hub"></a>SignalR 허브 만들기

*허브*는 클라이언트-서버 통신을 처리하는 높은 수준의 파이프라인 역할을 하는 클래스입니다.

* SignalRChat 프로젝트 폴더에 *Hubs* 폴더를 만듭니다.

* *Hubs* 폴더에 다음 코드를 작성한 *ChatHub.cs* 파일을 만듭니다.

  [!code-csharp[Startup](signalr/sample/Hubs/ChatHub.cs)]

  `ChatHub` 클래스는 SignalR `Hub` 클래스를 상속받습니다. 이 `Hub` 클래스가 연결, 그룹 및 메시징을 관리합니다.

  연결된 모든 클라이언트에서 `SendMessage` 메서드를 호출할 수 있습니다. 이 메서드는 수신된 메시지를 모든 클라이언트에 전송합니다. SignalR 코드는 최대한의 확장성을 제공할 수 있도록 비동기적입니다.

## <a name="configure-signalr"></a>SignalR 구성하기

SignalR 서버는 SignalR에 SignalR 요청을 전달하도록 구성되어야 합니다.

* 다음에 강조 표시된 코드를 *Startup.cs* 파일에 추가합니다.

  [!code-csharp[Startup](signalr/sample/Startup.cs?highlight=7,33,52-55)]

  이 변경 사항들은 ASP.NET Core 종속성 주입 시스템 및 미들웨어 파이프라인에 SignalR을 추가합니다.

## <a name="add-signalr-client-code"></a>SignalR 클라이언트 코드 추가하기

* *Pages\Index.cshtml*의 내용을 다음 코드로 대체합니다.

  [!code-cshtml[Index](signalr/sample/Pages/Index.cshtml)]

  이 코드는:

  * 이름 및 메시지 텍스트를 위한 텍스트 상자 및 전송 단추를 만듭니다.
  * SignalR 허브로부터 수신된 메시지를 출력하기 위한 `id="messagesList"`가 지정된 목록을 만듭니다.
  * SignalR 및 다음 단계에서 작성하게 될 *chat.js* 응용 프로그램 코드에 대한 스크립트 참조를 포함합니다.

* 다음 코드를 사용하여 *wwwroot/js* 폴더에 *chat.js* 파일을 만듭니다.

  [!code-javascript[Index](signalr/sample/wwwroot/js/chat.js)]

  이 코드는:

  * 연결을 생성하고 시작합니다.
  * 전송 버튼에 허브에 메시지를 전송하는 처리기를 추가합니다.
  * 연결 개체에 허브로부터 메시지를 수신하고 이를 목록에 추가하는 처리기를 추가합니다.

## <a name="run-the-app"></a>앱 실행하기

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

* **CTRL+F5** 키를 눌러서 디버깅 없이 앱을 실행합니다.

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code)

* **CTRL+F5** 키를 눌러서 디버깅 없이 앱을 실행합니다.

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[Visual Studio for Mac](#tab/visual-studio-mac)

* 메뉴에서 **실행 > 디버깅하지 않고 시작**을 선택합니다.

---

* 주소 표시줄에서 URL을 복사해서, 다른 브라우저의 인스턴스 또는 탭을 열고, 주소 표시줄에 URL을 붙여넣습니다.

* 브라우저 중 하나를 선택해서 이름과 메시지를 입력하고, **Send Message** 버튼을 누릅니다.

  그 즉시 이름과 메시지가 두 페이지 모두에 출력됩니다.

  ![SignalR 샘플 앱](signalr/_static/signalr-get-started-finished.png)

> [!TIP]
> 앱이 동작하지 않을 경우 브라우저 개발자 도구(F12)를 열고 콘솔로 이동합니다. 아마도 HTML 및 JavaScript 코드와 관련된 오류를 볼 수 있을 것입니다. 예를 들어 지시한 것과 다른 폴더에 *signalr.js*를 넣었다고 가정해보겠습니다. 이 경우 해당 파일에 대한 참조는 작동하지 않으며 콘솔에 404 오류가 표시될 것입니다.
> ![signalr.js 찾을 수 없음 오류](signalr/_static/f12-console.png)

## <a name="next-steps"></a>다음 단계

본 자습서에서는 다음 작업에 관한 방법을 학습했습니다.

> [!div class="checklist"]
> * 웹 앱 프로젝트를 만듭니다.
> * SignalR 클라이언트 라이브러리를 추가합니다.
> * SignalR 허브를 만듭니다.
> * SignalR을 사용하도록 프로젝트를 구성합니다.
> * 허브를 이용하여 모든 클라이언트에서 연결된 모든 클라이언트로 메시지를 전송하는 코드를 추가합니다.

SignalR에 대한 더 자세한 내용은 다음을 참고하시기 바랍니다.

> [!div class="nextstepaction"]
> [ASP.NET Core SignalR 소개](xref:signalr/introduction)
