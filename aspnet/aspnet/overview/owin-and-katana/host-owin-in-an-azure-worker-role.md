---
uid: aspnet/overview/owin-and-katana/host-owin-in-an-azure-worker-role
title: Azure 작업자 역할에 OWIN 호스트 | Microsoft Docs
author: MikeWasson
description: 이 자습서에는 Microsoft Azure 작업자 역할에 OWIN 자체 호스트 하는 방법을 보여 줍니다. Open Web Interface.NET (OWIN)에 대 한.NET 웹 서버 간의 추상화를 정의 하는 중...
ms.author: riande
ms.date: 04/11/2014
ms.assetid: 07aa855a-92ee-4d43-ba66-5bfd7de20ee6
msc.legacyurl: /aspnet/overview/owin-and-katana/host-owin-in-an-azure-worker-role
msc.type: authoredcontent
ms.openlocfilehash: 6bead915491c62de809b8625d8071a63c70a6ef5
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41837935"
---
<a name="host-owin-in-an-azure-worker-role"></a><span data-ttu-id="c9ed6-104">Azure 작업자 역할에 OWIN 호스트</span><span class="sxs-lookup"><span data-stu-id="c9ed6-104">Host OWIN in an Azure Worker Role</span></span>
====================
<span data-ttu-id="c9ed6-105">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="c9ed6-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="c9ed6-106">이 자습서에는 Microsoft Azure 작업자 역할에 OWIN 자체 호스트 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-106">This tutorial shows how to self-host OWIN in a Microsoft Azure worker role.</span></span>
> 
> <span data-ttu-id="c9ed6-107">[Open Web Interface for.NET](http://owin.org/) (OWIN).NET 웹 서버 및 웹 응용 프로그램 간의 추상화를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-107">[Open Web Interface for .NET](http://owin.org/) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="c9ed6-108">이상적인 OWIN 자체 IIS 외부에서 사용자 고유의 프로세스에서 웹 응용 프로그램을 호스팅하는 서버에서 웹 응용 프로그램을 분리 하는 OWIN – Azure 작업자 역할 내에서 예를 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-108">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS–for example, inside an Azure worker role.</span></span>
> 
> <span data-ttu-id="c9ed6-109">이 자습서에서는 Microsoft Azure 작업자 역할 내에서 OWIN 응용 프로그램을 자체 호스트 하는 방법에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-109">In this tutorial, you'll learn how to self-host an OWIN applications inside a Microsoft Azure worker role.</span></span> <span data-ttu-id="c9ed6-110">작업자 역할에 대 한 자세한 내용은 참조 하세요 [Azure 실행 모델](https://azure.microsoft.com/documentation/articles/fundamentals-application-models/#CloudServices)합니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-110">To learn more about worker roles, see [Azure Execution Models](https://azure.microsoft.com/documentation/articles/fundamentals-application-models/#CloudServices).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="c9ed6-111">이 자습서에 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="c9ed6-111">Software versions used in the tutorial</span></span>
> 
> 
> - [<span data-ttu-id="c9ed6-112">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="c9ed6-112">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - [<span data-ttu-id="c9ed6-113">Azure SDK for.NET 2.3</span><span class="sxs-lookup"><span data-stu-id="c9ed6-113">Azure SDK for .NET 2.3</span></span>](https://azure.microsoft.com/downloads/)
> - [<span data-ttu-id="c9ed6-114">Microsoft.Owin.Selfhost 2.1.0</span><span class="sxs-lookup"><span data-stu-id="c9ed6-114">Microsoft.Owin.Selfhost 2.1.0</span></span>](http://www.nuget.org/packages/Microsoft.Owin.SelfHost/2.1.0)


## <a name="create-a-microsoft-azure-project"></a><span data-ttu-id="c9ed6-115">Microsoft Azure 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="c9ed6-115">Create a Microsoft Azure Project</span></span>

<span data-ttu-id="c9ed6-116">관리자 권한으로 Visual Studio를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-116">Start Visual Studio with administrator privileges.</span></span> <span data-ttu-id="c9ed6-117">Azure 계산 에뮬레이터를 사용 하 여 응용 프로그램을 로컬로 디버깅 하려면 관리자 권한이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-117">Administrator privileges are needed to debug the application locally, using the Azure compute emulator.</span></span>

<span data-ttu-id="c9ed6-118">에 **파일** 메뉴에서 클릭 **새로 만들기**, 클릭 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-118">On the **File** menu, click **New**, then click **Project**.</span></span> <span data-ttu-id="c9ed6-119">**설치 된 템플릿**, Visual C#에서 클릭 **클라우드** 을 클릭 한 다음 **Windows Azure 클라우드 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-119">From **Installed Templates**, under Visual C#, click **Cloud** and then click **Windows Azure Cloud Service**.</span></span> <span data-ttu-id="c9ed6-120">"AzureApp" 프로젝트 이름을 지정 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-120">Name the project "AzureApp" and click **OK**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image2.png)](host-owin-in-an-azure-worker-role/_static/image1.png)

<span data-ttu-id="c9ed6-121">에 **새 Windows Azure 클라우드 서비스** 대화 상자에서 두 번 클릭 **작업자 역할**입니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-121">In the **New Windows Azure Cloud Service** dialog, double-click **Worker Role**.</span></span> <span data-ttu-id="c9ed6-122">기본 이름 ("WorkerRole1")을 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-122">Leave the default name ("WorkerRole1").</span></span> <span data-ttu-id="c9ed6-123">이 단계에서는 솔루션에 작업자 역할을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-123">This step adds a worker role to the solution.</span></span> <span data-ttu-id="c9ed6-124">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-124">Click **OK**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image4.png)](host-owin-in-an-azure-worker-role/_static/image3.png)

<span data-ttu-id="c9ed6-125">만든 Visual Studio 솔루션에는 두 개의 프로젝트가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-125">The Visual Studio solution that is created contains two projects:</span></span>

- <span data-ttu-id="c9ed6-126">&quot;AzureApp&quot; 역할 및 Azure 응용 프로그램에 대 한 구성을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-126">&quot;AzureApp&quot; defines the roles and configuration for the Azure application.</span></span>
- <span data-ttu-id="c9ed6-127">&quot;WorkerRole1&quot; 작업자 역할에 대 한 코드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-127">&quot;WorkerRole1&quot; contains the code for the worker role.</span></span>

<span data-ttu-id="c9ed6-128">일반적으로 Azure 응용 프로그램을이 자습서에서는 단일 역할을 사용 하 여 여러 역할을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-128">In general, an Azure application can contain multiple roles, although this tutorial uses a single role.</span></span>

![](host-owin-in-an-azure-worker-role/_static/image5.png)

## <a name="add-the-owin-self-host-packages"></a><span data-ttu-id="c9ed6-129">OWIN 자체 호스트 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="c9ed6-129">Add the OWIN Self-Host Packages</span></span>

<span data-ttu-id="c9ed6-130">**도구** 메뉴에서 클릭 **라이브러리 패키지 관리자**, 클릭 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-130">From the **Tools** menu, click **Library Package Manager**, then click **Package Manager Console**.</span></span>

<span data-ttu-id="c9ed6-131">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-131">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](host-owin-in-an-azure-worker-role/samples/sample1.cmd)]

## <a name="add-an-http-endpoint"></a><span data-ttu-id="c9ed6-132">HTTP 끝점 추가</span><span class="sxs-lookup"><span data-stu-id="c9ed6-132">Add an HTTP Endpoint</span></span>

<span data-ttu-id="c9ed6-133">솔루션 탐색기에서 AzureApp 프로젝트를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-133">In Solution Explorer, expand the AzureApp project.</span></span> <span data-ttu-id="c9ed6-134">역할 노드를 확장, WorkerRole1를 마우스 오른쪽 단추로 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-134">Expand the Roles node, right-click WorkerRole1, and select **Properties**.</span></span>

![](host-owin-in-an-azure-worker-role/_static/image6.png)

<span data-ttu-id="c9ed6-135">클릭 **끝점**를 클릭 하 고 **끝점 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-135">Click **Endpoints**, and then click **Add Endpoint**.</span></span>

<span data-ttu-id="c9ed6-136">에 **프로토콜** 드롭다운 목록에서 "http"를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-136">In the **Protocol** dropdown list, select "http".</span></span> <span data-ttu-id="c9ed6-137">**공용 포트** 하 고 **개인 포트**, 80을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-137">In **Public Port** and **Private Port**, type 80.</span></span> <span data-ttu-id="c9ed6-138">이러한 포트 번호는 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-138">These port numbers can be different.</span></span> <span data-ttu-id="c9ed6-139">공용 포트는 클라이언트 역할에 요청을 보낼 때 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-139">The public port is what clients use when they send a request to the role.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image8.png)](host-owin-in-an-azure-worker-role/_static/image7.png)

## <a name="create-the-owin-startup-class"></a><span data-ttu-id="c9ed6-140">OWIN 시작 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="c9ed6-140">Create the OWIN Startup Class</span></span>

<span data-ttu-id="c9ed6-141">솔루션 탐색기에서 WorkerRole1 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가** / **클래스** 새 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-141">In Solution Explorer, right click the WorkerRole1 project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="c9ed6-142">클래스 이름을 `Startup`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-142">Name the class `Startup`.</span></span>

<span data-ttu-id="c9ed6-143">모든 상용구 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-143">Replace all of the boilerplate code with the following:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample2.cs)]

<span data-ttu-id="c9ed6-144">`UseWelcomePage` 확장 메서드는 사이트가 작동을 확인 하려면 응용 프로그램에 간단한 HTML 페이지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-144">The `UseWelcomePage` extension method adds a simple HTML page to your application, to verify the site is working.</span></span>

## <a name="start-the-owin-host"></a><span data-ttu-id="c9ed6-145">OWIN 호스트를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-145">Start the OWIN Host</span></span>

<span data-ttu-id="c9ed6-146">WorkerRole.cs 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-146">Open the WorkerRole.cs file.</span></span> <span data-ttu-id="c9ed6-147">이 클래스는 작업자 역할은 시작 및 중지 될 때 실행 되는 코드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-147">This class defines the code that runs when the worker role is started and stopped.</span></span>

<span data-ttu-id="c9ed6-148">다음 추가 문을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="c9ed6-148">Add the following using statement:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample3.cs)]

<span data-ttu-id="c9ed6-149">추가 된 **IDisposable** 멤버는 `WorkerRole` 클래스:</span><span class="sxs-lookup"><span data-stu-id="c9ed6-149">Add an **IDisposable** member to the `WorkerRole` class:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample4.cs)]

<span data-ttu-id="c9ed6-150">에 `OnStart` 메서드를 호스트 하려면 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-150">In the `OnStart` method, add the following code to start the host:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample5.cs?highlight=5)]

<span data-ttu-id="c9ed6-151">합니다 **WebApp.Start** 메서드 OWIN 호스트를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-151">The **WebApp.Start** method starts the OWIN host.</span></span> <span data-ttu-id="c9ed6-152">이름을 합니다 `Startup` 클래스는 메서드 형식 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-152">The name of the `Startup` class is a type parameter to the method.</span></span> <span data-ttu-id="c9ed6-153">호스트는 호출 규칙에 따라는 `Configure` 이 클래스의 메서드.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-153">By convention, the host will call the `Configure` method of this class.</span></span>

<span data-ttu-id="c9ed6-154">재정의 된 `OnStop` 삭제 하는  *\_앱* 인스턴스:</span><span class="sxs-lookup"><span data-stu-id="c9ed6-154">Override the `OnStop` to dispose of the *\_app* instance:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample6.cs)]

<span data-ttu-id="c9ed6-155">WorkerRole.cs의 전체 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-155">Here is the complete code for WorkerRole.cs:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample7.cs)]

<span data-ttu-id="c9ed6-156">솔루션을 빌드하고 f5 키를 눌러 Azure Compute 에뮬레이터에서 응용 프로그램을 로컬로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-156">Build the solution, and press F5 to run the application locally in the Azure Compute Emulator.</span></span> <span data-ttu-id="c9ed6-157">방화벽 설정에 따라 방화벽을 통해 에뮬레이터를 허용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-157">Depending on your firewall settings, you might need to allow the emulator through your firewall.</span></span>

<span data-ttu-id="c9ed6-158">계산 에뮬레이터는 로컬 IP 주소를 끝점에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-158">The compute emulator assigns a local IP address to the endpoint.</span></span> <span data-ttu-id="c9ed6-159">Compute 에뮬레이터 UI를 확인 하 여 IP 주소를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-159">You can find the IP address by viewing the Compute Emulator UI.</span></span> <span data-ttu-id="c9ed6-160">작업 표시줄 알림 영역에서에서 에뮬레이터 아이콘을 마우스 오른쪽 단추로 누르고 **Compute 에뮬레이터 UI 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-160">Right-click the emulator icon in the task bar notification area, and select **Show Compute Emulator UI**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image10.png)](host-owin-in-an-azure-worker-role/_static/image9.png)

<span data-ttu-id="c9ed6-161">배포 서비스 배포 [id], 서비스 세부 정보 아래에서 IP 주소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-161">Find the IP address under Service Deployments, deployment [id], Service Details.</span></span> <span data-ttu-id="c9ed6-162">웹 브라우저를 열고 http:// 이동할<em>주소</em>, 여기서 <em>주소</em> 계산 에뮬레이터에서 할당 한 IP 주소는 예를 들어 `http://127.0.0.1:80`합니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-162">Open a web browser and navigate to http://<em>address</em>, where <em>address</em> is the IP address assigned by the compute emulator; for example, `http://127.0.0.1:80`.</span></span> <span data-ttu-id="c9ed6-163">OWIN 시작 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-163">You should see the OWIN welcome page:</span></span>

![](host-owin-in-an-azure-worker-role/_static/image11.png)

## <a name="deploy-to-azure"></a><span data-ttu-id="c9ed6-164">Azure에 배포</span><span class="sxs-lookup"><span data-stu-id="c9ed6-164">Deploy to Azure</span></span>

<span data-ttu-id="c9ed6-165">이 단계에서는 Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-165">For this step, you must have an Azure account.</span></span> <span data-ttu-id="c9ed6-166">아직 없다면, 몇 분만에 무료 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-166">If you don't already have one, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="c9ed6-167">자세한 내용은 참조 하세요 [Microsoft Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)합니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-167">For details, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>

<span data-ttu-id="c9ed6-168">솔루션 탐색기에서 AzureApp 프로젝트를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-168">In Solution Explorer, right-click the AzureApp project.</span></span> <span data-ttu-id="c9ed6-169">**게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-169">Select **Publish**.</span></span>

![](host-owin-in-an-azure-worker-role/_static/image12.png)

<span data-ttu-id="c9ed6-170">Azure 계정에 로그인 하지 않은 경우 클릭 **로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-170">If you are not signed in to your Azure account, click **Sign In**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image14.png)](host-owin-in-an-azure-worker-role/_static/image13.png)

<span data-ttu-id="c9ed6-171">에 로그인 한 후 구독을 선택 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-171">After you are signed in, choose a subscription and click **Next**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image16.png)](host-owin-in-an-azure-worker-role/_static/image15.png)

<span data-ttu-id="c9ed6-172">클라우드 서비스에 대 한 이름을 입력 하 고 지역을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-172">Enter a name for the cloud service and choose a region.</span></span> <span data-ttu-id="c9ed6-173">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-173">Click **Create**.</span></span>

![](host-owin-in-an-azure-worker-role/_static/image17.png)

<span data-ttu-id="c9ed6-174">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-174">Click **Publish**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image19.png)](host-owin-in-an-azure-worker-role/_static/image18.png)

<span data-ttu-id="c9ed6-175">Azure 활동 로그 창에 배포 진행률이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-175">The Azure Activity Log window shows the progress of the deployment.</span></span> <span data-ttu-id="c9ed6-176">앱을 배포할 때 이동할 `http://appname.cloudapp.net/`, 여기서 *appname* 클라우드 서비스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c9ed6-176">When the app is deployed, browse to `http://appname.cloudapp.net/`, where *appname* is the name of your cloud service.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c9ed6-177">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="c9ed6-177">Additional Resources</span></span>

- [<span data-ttu-id="c9ed6-178">프로젝트 Katana 개요</span><span class="sxs-lookup"><span data-stu-id="c9ed6-178">An Overview of Project Katana</span></span>](an-overview-of-project-katana.md)
- [<span data-ttu-id="c9ed6-179">GitHub에서 Katana 프로젝트</span><span class="sxs-lookup"><span data-stu-id="c9ed6-179">Katana Project on GitHub</span></span>](https://github.com/aspnet/AspNetKatana/)
