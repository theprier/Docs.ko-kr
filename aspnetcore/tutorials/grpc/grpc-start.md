---
title: '자습서: ASP.NET Core에서 gRPC 시작'
author: juntaoluo
description: 이 자습서 시리즈는 ASP.NET Core에서 gRPC 서비스를 만드는 방법을 보여 줍니다. gRPC 서비스 프로젝트를 만들고, proto 파일을 편집하고, 이중 스트리밍 호출을 추가하는 방법을 알아봅니다.
monikerRange: '>= aspnetcore-3.0'
ms.author: johluo
ms.date: 2/26/2019
uid: tutorials/grpc/grpc-start
ms.openlocfilehash: 5f7a2f6b57804b3295b23c322dcbac553b05528b
ms.sourcegitcommit: 088e6744cd67a62f214f25146313a53949b17d35
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/21/2019
ms.locfileid: "58320058"
---
# <a name="tutorial-get-started-with-grpc-service-in-aspnet-core"></a>자습서: ASP.NET Core에서 gRPC 서비스 시작

작성자: [John Luo](https://github.com/juntaoluo)

이 자습서는 ASP.NET Core에서 gRPC 서비스를 빌드하는 작업의 기본 사항을 설명합니다.

이 자습서를 마치면 인사말을 에코하는 gRPC 서비스를 빌드할 수 있습니다.

[!INCLUDE[View or download sample code](~/includes/grpc/download.md)]

이 자습서에서는 다음을 수행했습니다.

> [!div class="checklist"]
> * gRPC 서비스를 만듭니다.
> * 서비스를 실행합니다.
> * 프로젝트 파일을 검사합니다.

[!INCLUDE[](~/includes/net-core-prereqs-all-3.0.md)]

## <a name="create-a-grpc-service"></a>gRPC 서비스 만들기

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

* Visual Studio **파일** 메뉴에서 **새로 만들기** > **프로젝트**를 선택합니다.
* 새 ASP.NET Core 웹 애플리케이션을 만듭니다.
  ![새 ASP.NET Core 웹 애플리케이션](grpc-start/_static/np_3_0.1.png)
* 프로젝트 이름을 **GrpcGreeter**로 지정합니다. 코드를 복사하여 붙여넣을 때 네임스페이스가 일치하도록 프로젝트 이름을 *GrpcGreeter*로 지정해야 합니다.
  ![새 ASP.NET Core 웹 애플리케이션](grpc-start/_static/np_3_0.2.png)
* 드롭다운에서 **.NET Core** 및 **ASP.NET Core 3.0**을 선택합니다. **gRPC 서비스** 템플릿을 선택합니다.

  다음 시작 프로젝트를 만듭니다.

  ![솔루션 탐색기](grpc-start/_static/se3.0.png)

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code)

* [통합 터미널](https://code.visualstudio.com/docs/editor/integrated-terminal)을 엽니다.
* 디렉터리(`cd`)를 프로젝트를 포함하는 폴더로 변경합니다.
* 다음 명령을 실행합니다.

  ```console
  dotnet new grpc -o GrpcGreeter
  code -r GrpcGreeter
  ```

  * `dotnet new` 명령은 *GrpcGreeter* 폴더에 새 gRPC 서비스를 만듭니다.
  * `code` 명령은 Visual Studio Code의 새 인스턴스에서 *GrpcGreeter* 폴더를 엽니다.

  다음과 같은 대화 상자가 표시됩니다. **‘GrpcGreeter’에서 빌드 및 디버그에 필요한 자산이 누락되었습니다. 추가할까요?**
* **예**를 선택합니다.

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[Visual Studio for Mac](#tab/visual-studio-mac)

터미널에서 다음 명령을 실행합니다.

```console
  dotnet new grpc -o GrpcGreeter
  cd GrpcGreeter
```

이전 명령은 [.NET Core CLI](/dotnet/core/tools/dotnet)를 사용하여 gRPC 서비스를 만듭니다.

### <a name="open-the-project"></a>프로젝트 열기

Visual Studio에서 **파일 > 열기**를 선택하고 *GrpcGreeter.sln* 파일을 선택합니다.

<!-- End of VS tabs -->

---

### <a name="test-the-service"></a>서비스 테스트

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

* **GrpcGreeter.Server**가 시작 프로젝트로 설정되어 있는지 확인하고 Ctrl+F5를 눌러 디버거를 사용하지 않고 gRPC 서비스를 실행합니다.

  Visual Studio는 명령 프롬프트에서 서비스를 실행합니다. 로그에는 서비스가 `http://localhost:50051`에서 수신을 시작했다고 나옵니다.

  ![새 ASP.NET Core 웹 애플리케이션](grpc-start/_static/server_start.png)

* 서비스가 실행 중이면 **GrpcGreeter.Client**를 시작 프로젝트로 설정하고 Ctrl+F5를 눌러 디버거를 사용하지 않고 클라이언트를 실행합니다.

  클라이언트가 자신의 이름 “GreeterClient”가 포함된 메시지와 함께 인사말을 서비스에 보냅니다. 서비스가 명령 프롬프트에 표시되는 응답으로 “Hello GreeterClient” 메시지를 보냅니다.

  ![새 ASP.NET Core 웹 애플리케이션](grpc-start/_static/client.png)

  서비스가 명령 프롬프트에 기록되는 로그에 성공한 호출의 세부 정보를 기록합니다.

  ![새 ASP.NET Core 웹 애플리케이션](grpc-start/_static/server_complete.png)

# <a name="visual-studio-code--visual-studio-for-mactabvisual-studio-codevisual-studio-mac"></a>[Visual Studio Code / Visual Studio for Mac](#tab/visual-studio-code+visual-studio-mac)

* `dotnet run`을 사용하여 명령줄에서 서버 프로젝트 GrpcGreeter.Server를 실행합니다. 로그에는 서비스가 `http://localhost:50051`에서 수신을 시작했다고 나옵니다.

```console
info: Microsoft.Hosting.Lifetime[0]
      Now listening on: http://localhost:50051
info: Microsoft.Hosting.Lifetime[0]
      Application started. Press Ctrl+C to shut down.
info: Microsoft.Hosting.Lifetime[0]
      Hosting environment: Development
info: Microsoft.Hosting.Lifetime[0]
      Content root path: C:\example\GrpcGreeter\GrpcGreeter.Server
```

* `dotnet run`을 사용하여 별도의 명령줄에서 클라이언트 프로젝트 GrpcGreeter.Client를 실행합니다.

클라이언트가 자신의 이름 “GreeterClient”가 포함된 메시지와 함께 인사말을 서비스에 보냅니다. 서비스가 명령 프롬프트에 표시되는 응답으로 “Hello GreeterClient” 메시지를 보냅니다.

```console
Greeting: Hello GreeterClient
Press any key to exit...
```

서비스가 명령 프롬프트에 기록되는 로그에 성공한 호출의 세부 정보를 기록합니다.

```console
info: Microsoft.Hosting.Lifetime[0]
      Now listening on: http://localhost:50051
info: Microsoft.Hosting.Lifetime[0]
      Application started. Press Ctrl+C to shut down.
info: Microsoft.Hosting.Lifetime[0]
      Hosting environment: Development
info: Microsoft.Hosting.Lifetime[0]
      Content root path: C:\gh\tp\GrpcGreeter\GrpcGreeter.Server
info: Microsoft.AspNetCore.Hosting.Internal.GenericWebHostService[1]
      Request starting HTTP/2 POST http://localhost:50051/Greet.Greeter/SayHello application/grpc
info: Microsoft.AspNetCore.Hosting.Internal.GenericWebHostService[2]
      Request finished in 107.46730000000001ms 200 application/grpc
```

<!-- End of combined VS/Mac tabs -->

---

### <a name="examine-the-project-files-of-the-grpc-project"></a>gRPC 프로젝트의 프로젝트 파일 검토

GrpcGreeter.Server 파일:

* greet.proto: *Protos/greet.proto* 파일은 `Greeter` gRPC를 정의하고 gRPC 서버 자산을 생성하는 데 사용됩니다. 자세한 내용은 <xref:grpc/index>을 참조하세요.
* *Services* 폴더: `Greeter` 서비스의 구현을 포함합니다.
* *appSettings.json*: Kestrel에서 사용하는 프로토콜과 같은 구성 데이터를 포함합니다. 자세한 내용은 <xref:fundamentals/configuration/index>을 참조하세요.
* *Program.cs*: gRPC 서비스의 진입점을 포함합니다. 자세한 내용은 <xref:fundamentals/host/web-host>을 참조하세요.
* Startup.cs

앱 동작을 구성하는 코드를 포함합니다. 자세한 내용은 <xref:fundamentals/startup>을 참조하세요.

gRPC 클라이언트 GrpcGreeter.Client 파일:

*Program.cs*는 gRPC 클라이언트의 진입점 및 논리를 포함합니다.

이 자습서에서는 다음을 수행했습니다.

> [!div class="checklist"]
> * gRPC 서비스를 만들었습니다.
> * 서비스 및 클라이언트를 실행하여 서비스를 테스트했습니다.
> * 프로젝트 파일을 검사했습니다.
