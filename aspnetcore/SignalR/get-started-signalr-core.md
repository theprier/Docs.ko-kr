---
title: "SignalR에서 ASP.NET Core 시작"
author: rachelappel
description: "ASP.NET Core 용 SignalR을 사용 하 여 실시간 앱 빌드 기본 사항에 알아봅니다."
manager: wpickett
ms.author: rachelap
ms.custom: mvc
ms.date: 03/06/2018
ms.prod: aspnet-core
ms.technology: dotnet-signalr
ms.topic: tutorial
uid: signalr/get-started-signalr-core
ms.openlocfilehash: 79af59fc8c2ada71d764ada95a431e10f4f00f27
ms.sourcegitcommit: 493a215355576cfa481773365de021bcf04bb9c7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
# <a name="tutorial-get-started-with-signalr-for-aspnet-core"></a>ASP.NET Core 용 SignalR 시작 자습서:

작성자: [Rachel Appel](https://twitter.com/rachelappel)

이 자습서의 ASP.NET Core 용 SignalR을 사용 하 여 실시간 앱 빌드 기본 사항에 설명 합니다.

   ![솔루션](get-started-signalr-core/_static/signalr-get-started-finished.png)

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/get-started-signalr-core/sample/)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

이 자습서에서는 다음 SignalR 개발 작업을 보여 줍니다.

> [!div class="checklist"]
> * ASP.NET Core 웹 앱을 만듭니다.
> * 클라이언트에 콘텐츠를 푸시 하려면 SignalR 허브를 만듭니다.
> * SignalR JavaScript 라이브러리를 사용 하 여 메시지를 보내고을 허브에서 업데이트를 표시 합니다.

## <a name="prerequisites"></a>전제 조건

다음 소프트웨어를 설치 합니다.

* [.NET core 2.1.0 Preview 1 SDK](https://www.microsoft.com/net/download/dotnet-core/sdk-2.1.300-preview1) 이상 버전
* [Visual Studio 2017](https://www.visualstudio.com/downloads/) 15.6 ASP.NET 및 웹 개발 작업의 이후 버전
* [npm](https://www.npmjs.com/get-npm)

## <a name="create-an-aspnet-core-project-that-hosts-signalr-client-and-server"></a>SignalR 클라이언트와 서버를 호스팅하는 ASP.NET Core 프로젝트 만들기

1. 사용 하 여는 **파일** > **새 프로젝트** 메뉴 옵션 선택한 **ASP.NET Core 웹 응용 프로그램**합니다. 프로젝트 이름을 `SignalRChat`로 지정합니다.

  ![Visual Studio에서 새 프로젝트 대화 상자](get-started-signalr-core/_static/signalr-new-project-dialog.png)

2. 선택 **웹 응용 프로그램** Razor 페이지를 사용 하 여 프로젝트를 만듭니다. 그런 다음 선택 **확인**합니다. 수 있도록 **ASP.NET Core 2.1** SignalR 이전 버전의.NET에서 실행 하는 경우 프레임 워크 선택기에서 선택 합니다.

  ![Visual Studio에서 새 프로젝트 대화 상자](get-started-signalr-core/_static/signalr-new-project-choose-type.png)

  SignalR의 서버 쪽 코드를 호스트 하는 라이브러리 프로젝트 템플릿에 포함 됩니다. 설치와 별도로 클라이언트 쪽 JavaScript [npm](https://www.npmjs.com/)합니다.

  ```console
   npm install @aspnet/signalr
  ```

3. 복사는 *signalr.js* 에서 *node_modules\\ @aspnet\signalr\dist\browser*  에 *wwwroot\lib* 프로젝트의 폴더에에서 있습니다.

## <a name="create-the-signalr-hub"></a>SignalR 허브를 만듭니다.

허브는 클라이언트와 서버에서 다른 메서드를 호출할 수 있도록 하는 높은 수준의 파이프라인으로 사용 되는 클래스입니다.

1. 클래스를 선택 하 여 프로젝트에 추가 **파일** > **새로** > **파일** 선택 하 고 **Visual C# 클래스**합니다. 

1. 상속 `Microsoft.AspNetCore.SignalR.Hub`합니다. `Hub` 속성과 송신 및 수신 데이터 뿐 아니라 연결 그룹을 관리 하기 위한 이벤트 클래스를 포함 합니다.

1. 만들기는 `Send` 모든 연결 된 채팅 클라이언트에 메시지를 보내는 방법입니다. 반환 확인는 `Task`SignalR 비동기 이기 때문에 있습니다. 비동기 코드 확장성이 좋아집니다.

  [!code-csharp[Startup](get-started-signalr-core/sample/Hubs/ChatHub.cs?range=7-14)]

## <a name="configure-the-project-to-use-signalr"></a>SignalR을 사용 하도록 프로젝트를 구성 합니다.

SignalR 서버 signalr 요청을 전달 하려면 알 수 있도록 구성 되어야 합니다.

1. SignalR 프로젝트를 구성 하려면 수정 된 `ConfigureServices` 메서드는 응용 프로그램의 `Startup` 클래스에 대 한 호출을 삽입 하 여 `services.AddSignalR`합니다.

  `services.AddSignalR` SignalR의 일부로 추가 [ASP.NET Core 미들웨어](xref:fundamentals/middleware/index) 파이프라인.

1. 사용 하 여 허브에 대 한 라우팅을 구성 `UseSignalR`합니다.

  [!code-csharp[Startup](get-started-signalr-core/sample/Startup.cs?highlight=22,40-43)]

## <a name="create-the-signalr-client-code"></a>SignalR 클라이언트 코드 만들기

1. 에서는 교체 *Pages\Index.cshtml* 를 다음 코드로:

  [!code-cshtml[Index](get-started-signalr-core/sample/Pages/Index.cshtml)]

  위의 HTML 이름 및 메시지 필드 및 전송 단추가 표시 됩니다. 맨 아래에 스크립트 참조를 확인: SignalR에 대 한 참조 및 *chat.js*합니다.

1. 에 JavaScript 파일을 추가 *wwwroot\js* 라는 폴더 *chat.js* 다음 코드를 추가 합니다.

  [!code-javascript[Index](get-started-signalr-core/sample/wwwroot/js/chat.js)]

## <a name="run-the-app"></a>앱 실행

1. 선택 **디버그** > **디버깅 하지 않고 시작** 브라우저를 실행 하 여 로컬 웹 사이트를 로드 합니다. 주소 표시줄에서 URL을 복사 합니다.

1. 다른 브라우저 인스턴스 (모든 브라우저)를 열고 주소 표시줄에 URL을 붙여 넣습니다.

1. 브라우저 중 하나를 선택 하 고, 이름 및 메시지를 입력 한 다음 클릭는 **보낼** 단추입니다. 이름 및 메시지는 두 페이지에 즉시 표시 됩니다.

  ![솔루션](get-started-signalr-core/_static/signalr-get-started-finished.png)
