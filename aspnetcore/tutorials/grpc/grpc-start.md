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
# <a name="tutorial-get-started-with-grpc-service-in-aspnet-core"></a><span data-ttu-id="ba1ae-104">자습서: ASP.NET Core에서 gRPC 서비스 시작</span><span class="sxs-lookup"><span data-stu-id="ba1ae-104">Tutorial: Get started with gRPC service in ASP.NET Core</span></span>

<span data-ttu-id="ba1ae-105">작성자: [John Luo](https://github.com/juntaoluo)</span><span class="sxs-lookup"><span data-stu-id="ba1ae-105">By [John Luo](https://github.com/juntaoluo)</span></span>

<span data-ttu-id="ba1ae-106">이 자습서는 ASP.NET Core에서 gRPC 서비스를 빌드하는 작업의 기본 사항을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-106">This tutorial teaches the basics of building a gRPC service on ASP.NET Core.</span></span>

<span data-ttu-id="ba1ae-107">이 자습서를 마치면 인사말을 에코하는 gRPC 서비스를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-107">At the end, you'll have a gRPC service that echoes greetings.</span></span>

[!INCLUDE[View or download sample code](~/includes/grpc/download.md)]

<span data-ttu-id="ba1ae-108">이 자습서에서는 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ba1ae-109">gRPC 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-109">Create a gRPC service.</span></span>
> * <span data-ttu-id="ba1ae-110">서비스를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-110">Run the service.</span></span>
> * <span data-ttu-id="ba1ae-111">프로젝트 파일을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-111">Examine the project files.</span></span>

[!INCLUDE[](~/includes/net-core-prereqs-all-3.0.md)]

## <a name="create-a-grpc-service"></a><span data-ttu-id="ba1ae-112">gRPC 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="ba1ae-112">Create a gRPC service</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="ba1ae-113">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ba1ae-113">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="ba1ae-114">Visual Studio **파일** 메뉴에서 **새로 만들기** > **프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-114">From the Visual Studio **File** menu, select **New** > **Project**.</span></span>
* <span data-ttu-id="ba1ae-115">새 ASP.NET Core 웹 애플리케이션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-115">Create a new ASP.NET Core Web Application.</span></span>
  <span data-ttu-id="ba1ae-116">![새 ASP.NET Core 웹 애플리케이션](grpc-start/_static/np_3_0.1.png)</span><span class="sxs-lookup"><span data-stu-id="ba1ae-116">![new ASP.NET Core Web Application](grpc-start/_static/np_3_0.1.png)</span></span>
* <span data-ttu-id="ba1ae-117">프로젝트 이름을 **GrpcGreeter**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-117">Name the project **GrpcGreeter**.</span></span> <span data-ttu-id="ba1ae-118">코드를 복사하여 붙여넣을 때 네임스페이스가 일치하도록 프로젝트 이름을 *GrpcGreeter*로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-118">It's important to name the project *GrpcGreeter* so the namespaces will match when you copy and paste code.</span></span>
  <span data-ttu-id="ba1ae-119">![새 ASP.NET Core 웹 애플리케이션](grpc-start/_static/np_3_0.2.png)</span><span class="sxs-lookup"><span data-stu-id="ba1ae-119">![new ASP.NET Core Web Application](grpc-start/_static/np_3_0.2.png)</span></span>
* <span data-ttu-id="ba1ae-120">드롭다운에서 **.NET Core** 및 **ASP.NET Core 3.0**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-120">Select **.NET Core** and **ASP.NET Core 3.0** in the dropdown.</span></span> <span data-ttu-id="ba1ae-121">**gRPC 서비스** 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-121">Choose the **gRPC Service** template.</span></span>

  <span data-ttu-id="ba1ae-122">다음 시작 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-122">The following starter project is created:</span></span>

  ![솔루션 탐색기](grpc-start/_static/se3.0.png)

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="ba1ae-124">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="ba1ae-124">Visual Studio Code</span></span>](#tab/visual-studio-code)

* <span data-ttu-id="ba1ae-125">[통합 터미널](https://code.visualstudio.com/docs/editor/integrated-terminal)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-125">Open the [integrated terminal](https://code.visualstudio.com/docs/editor/integrated-terminal).</span></span>
* <span data-ttu-id="ba1ae-126">디렉터리(`cd`)를 프로젝트를 포함하는 폴더로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-126">Change directories (`cd`) to a folder which will contain the project.</span></span>
* <span data-ttu-id="ba1ae-127">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-127">Run the following commands:</span></span>

  ```console
  dotnet new grpc -o GrpcGreeter
  code -r GrpcGreeter
  ```

  * <span data-ttu-id="ba1ae-128">`dotnet new` 명령은 *GrpcGreeter* 폴더에 새 gRPC 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-128">The `dotnet new` command creates a new gRPC service in the *GrpcGreeter* folder.</span></span>
  * <span data-ttu-id="ba1ae-129">`code` 명령은 Visual Studio Code의 새 인스턴스에서 *GrpcGreeter* 폴더를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-129">The `code` command opens the *GrpcGreeter* folder in a new instance of Visual Studio Code.</span></span>

  <span data-ttu-id="ba1ae-130">다음과 같은 대화 상자가 표시됩니다. **‘GrpcGreeter’에서 빌드 및 디버그에 필요한 자산이 누락되었습니다. 추가할까요?**</span><span class="sxs-lookup"><span data-stu-id="ba1ae-130">A dialog box appears with **Required assets to build and debug are missing from 'GrpcGreeter'. Add them?**</span></span>
* <span data-ttu-id="ba1ae-131">**예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-131">Select **Yes**</span></span>

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="ba1ae-132">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="ba1ae-132">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

<span data-ttu-id="ba1ae-133">터미널에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-133">From a terminal, run the following commands:</span></span>

```console
  dotnet new grpc -o GrpcGreeter
  cd GrpcGreeter
```

<span data-ttu-id="ba1ae-134">이전 명령은 [.NET Core CLI](/dotnet/core/tools/dotnet)를 사용하여 gRPC 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-134">The preceding commands use the [.NET Core CLI](/dotnet/core/tools/dotnet) to create a gRPC service.</span></span>

### <a name="open-the-project"></a><span data-ttu-id="ba1ae-135">프로젝트 열기</span><span class="sxs-lookup"><span data-stu-id="ba1ae-135">Open the project</span></span>

<span data-ttu-id="ba1ae-136">Visual Studio에서 **파일 > 열기**를 선택하고 *GrpcGreeter.sln* 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-136">From Visual Studio, select **File > Open**, and then select the *GrpcGreeter.sln* file.</span></span>

<!-- End of VS tabs -->

---

### <a name="test-the-service"></a><span data-ttu-id="ba1ae-137">서비스 테스트</span><span class="sxs-lookup"><span data-stu-id="ba1ae-137">Test the service</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="ba1ae-138">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ba1ae-138">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="ba1ae-139">**GrpcGreeter.Server**가 시작 프로젝트로 설정되어 있는지 확인하고 Ctrl+F5를 눌러 디버거를 사용하지 않고 gRPC 서비스를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-139">Ensure the **GrpcGreeter.Server** is set as the Startup Project and press Ctrl+F5 to run the gRPC service without the debugger.</span></span>

  <span data-ttu-id="ba1ae-140">Visual Studio는 명령 프롬프트에서 서비스를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-140">Visual Studio runs the service in a command prompt.</span></span> <span data-ttu-id="ba1ae-141">로그에는 서비스가 `http://localhost:50051`에서 수신을 시작했다고 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-141">The logs show that the service started listening on `http://localhost:50051`.</span></span>

  ![새 ASP.NET Core 웹 애플리케이션](grpc-start/_static/server_start.png)

* <span data-ttu-id="ba1ae-143">서비스가 실행 중이면 **GrpcGreeter.Client**를 시작 프로젝트로 설정하고 Ctrl+F5를 눌러 디버거를 사용하지 않고 클라이언트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-143">Once the service is running, set the **GrpcGreeter.Client** is set as the Startup Project and press Ctrl+F5 to run the client without the debugger.</span></span>

  <span data-ttu-id="ba1ae-144">클라이언트가 자신의 이름 “GreeterClient”가 포함된 메시지와 함께 인사말을 서비스에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-144">The client sends a greeting to the service with a message containing its name "GreeterClient".</span></span> <span data-ttu-id="ba1ae-145">서비스가 명령 프롬프트에 표시되는 응답으로 “Hello GreeterClient” 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-145">The service will send a message "Hello GreeterClient" as a response that is displayed in the command prompt.</span></span>

  ![새 ASP.NET Core 웹 애플리케이션](grpc-start/_static/client.png)

  <span data-ttu-id="ba1ae-147">서비스가 명령 프롬프트에 기록되는 로그에 성공한 호출의 세부 정보를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-147">The service records the details of the successful call in the logs written to the command prompt.</span></span>

  ![새 ASP.NET Core 웹 애플리케이션](grpc-start/_static/server_complete.png)

# <a name="visual-studio-code--visual-studio-for-mactabvisual-studio-codevisual-studio-mac"></a>[<span data-ttu-id="ba1ae-149">Visual Studio Code / Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="ba1ae-149">Visual Studio Code / Visual Studio for Mac</span></span>](#tab/visual-studio-code+visual-studio-mac)

* <span data-ttu-id="ba1ae-150">`dotnet run`을 사용하여 명령줄에서 서버 프로젝트 GrpcGreeter.Server를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-150">Run the Server project GrpcGreeter.Server from the command line using `dotnet run`.</span></span> <span data-ttu-id="ba1ae-151">로그에는 서비스가 `http://localhost:50051`에서 수신을 시작했다고 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-151">The logs show that the service started listening on `http://localhost:50051`.</span></span>

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

* <span data-ttu-id="ba1ae-152">`dotnet run`을 사용하여 별도의 명령줄에서 클라이언트 프로젝트 GrpcGreeter.Client를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-152">Run the Client project GrpcGreeter.Client from the separate command line using `dotnet run`.</span></span>

<span data-ttu-id="ba1ae-153">클라이언트가 자신의 이름 “GreeterClient”가 포함된 메시지와 함께 인사말을 서비스에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-153">The client sends a greeting to the service with a message containing its name "GreeterClient".</span></span> <span data-ttu-id="ba1ae-154">서비스가 명령 프롬프트에 표시되는 응답으로 “Hello GreeterClient” 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-154">The service will send a message "Hello GreeterClient" as a response that is displayed in the command prompt.</span></span>

```console
Greeting: Hello GreeterClient
Press any key to exit...
```

<span data-ttu-id="ba1ae-155">서비스가 명령 프롬프트에 기록되는 로그에 성공한 호출의 세부 정보를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-155">The service records the details of the successful call in the logs written to the command prompt.</span></span>

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

### <a name="examine-the-project-files-of-the-grpc-project"></a><span data-ttu-id="ba1ae-156">gRPC 프로젝트의 프로젝트 파일 검토</span><span class="sxs-lookup"><span data-stu-id="ba1ae-156">Examine the project files of the gRPC project</span></span>

<span data-ttu-id="ba1ae-157">GrpcGreeter.Server 파일:</span><span class="sxs-lookup"><span data-stu-id="ba1ae-157">GrpcGreeter.Server files:</span></span>

* <span data-ttu-id="ba1ae-158">greet.proto: *Protos/greet.proto* 파일은 `Greeter` gRPC를 정의하고 gRPC 서버 자산을 생성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-158">greet.proto: The *Protos/greet.proto* file defines the `Greeter` gRPC and is used to generate the gRPC server assets.</span></span> <span data-ttu-id="ba1ae-159">자세한 내용은 <xref:grpc/index>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-159">For more information, see <xref:grpc/index>.</span></span>
* <span data-ttu-id="ba1ae-160">*Services* 폴더: `Greeter` 서비스의 구현을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-160">*Services* folder: Contains the implementation of the `Greeter` service.</span></span>
* <span data-ttu-id="ba1ae-161">*appSettings.json*: Kestrel에서 사용하는 프로토콜과 같은 구성 데이터를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-161">*appSettings.json*:Contains configuration data, such as protocol used by Kestrel.</span></span> <span data-ttu-id="ba1ae-162">자세한 내용은 <xref:fundamentals/configuration/index>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-162">For more information, see <xref:fundamentals/configuration/index>.</span></span>
* <span data-ttu-id="ba1ae-163">*Program.cs*: gRPC 서비스의 진입점을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-163">*Program.cs*: Contains the entry point for the gRPC service.</span></span> <span data-ttu-id="ba1ae-164">자세한 내용은 <xref:fundamentals/host/web-host>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-164">For more information, see <xref:fundamentals/host/web-host>.</span></span>
* <span data-ttu-id="ba1ae-165">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="ba1ae-165">Startup.cs</span></span>

<span data-ttu-id="ba1ae-166">앱 동작을 구성하는 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-166">Contains code that configures app behavior.</span></span> <span data-ttu-id="ba1ae-167">자세한 내용은 <xref:fundamentals/startup>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-167">For more information, see <xref:fundamentals/startup>.</span></span>

<span data-ttu-id="ba1ae-168">gRPC 클라이언트 GrpcGreeter.Client 파일:</span><span class="sxs-lookup"><span data-stu-id="ba1ae-168">gRPC client GrpcGreeter.Client file:</span></span>

<span data-ttu-id="ba1ae-169">*Program.cs*는 gRPC 클라이언트의 진입점 및 논리를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-169">*Program.cs* contains the entry point and logic for the gRPC client.</span></span>

<span data-ttu-id="ba1ae-170">이 자습서에서는 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-170">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ba1ae-171">gRPC 서비스를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-171">Created a gRPC service.</span></span>
> * <span data-ttu-id="ba1ae-172">서비스 및 클라이언트를 실행하여 서비스를 테스트했습니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-172">Ran the service and a client to test the service.</span></span>
> * <span data-ttu-id="ba1ae-173">프로젝트 파일을 검사했습니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ae-173">Examined the project files.</span></span>
