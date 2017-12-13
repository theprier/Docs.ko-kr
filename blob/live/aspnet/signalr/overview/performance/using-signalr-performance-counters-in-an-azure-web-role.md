---
uid: signalr/overview/performance/using-signalr-performance-counters-in-an-azure-web-role
title: "SignalR 성능 카운터를 사용 하 여 Azure 웹 역할에서 | Microsoft Docs"
author: guardrex
description: "설치 하 고 Azure 웹 역할에서 SignalR 성능 카운터를 사용 하는 방법."
keywords: "ASP.NET,signalr,performance 카운터, azure 웹 역할"
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/11/2017
ms.topic: article
ms.assetid: 2a127d3b-21ed-4cc9-bec0-cdab4e742a25
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/performance/using-signalr-performance-counters-in-an-azure-web-role
msc.type: authoredcontent
ms.openlocfilehash: 0d2717eb318d282e21e9aa8622a205f556e3a4ee
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
# <a name="using-signalr-performance-counters-in-an-azure-web-role"></a><span data-ttu-id="eefb6-104">SignalR 성능 카운터를 사용 하 여 Azure 웹 역할에서</span><span class="sxs-lookup"><span data-stu-id="eefb6-104">Using SignalR performance counters in an Azure Web Role</span></span>

<span data-ttu-id="eefb6-105">[Luke Latham](https://github.com/guardrex)으로</span><span class="sxs-lookup"><span data-stu-id="eefb6-105">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="eefb6-106">SignalR 성능 카운터는 Azure 웹 역할에서 응용 프로그램의 성능을 모니터링 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-106">SignalR performance counters are used to monitor your app's performance in an Azure Web Role.</span></span> <span data-ttu-id="eefb6-107">카운터는 Microsoft Azure 진단에서 캡처됩니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-107">The counters are captured by Microsoft Azure Diagnostics.</span></span> <span data-ttu-id="eefb6-108">SignalR 성능 카운터와 Azure에서 설치한 *signalr.exe*, 독립 실행형 또는 온-프레미스 응용 프로그램에 사용 되는 동일한 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-108">You install SignalR performance counters on Azure with *signalr.exe*, the same tool used for standalone or on-premises apps.</span></span> <span data-ttu-id="eefb6-109">Azure 역할은 일시적인, 앱 설치 및 시작할 때 SignalR 성능 카운터를 등록을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-109">Since Azure roles are transient, you configure an app to install and register SignalR performance counters upon startup.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eefb6-110">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="eefb6-110">Prerequisites</span></span>

* [<span data-ttu-id="eefb6-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="eefb6-111">Visual Studio 2015</span></span>](https://www.visualstudio.com/vs/visual-studio-express/)
* <span data-ttu-id="eefb6-112">[Visual Studio 2015 (VS2015) 용 Microsoft Azure SDK](https://azure.microsoft.com/downloads/) **참고: SDK를 설치한 후 컴퓨터를 다시 시작 합니다.**</span><span class="sxs-lookup"><span data-stu-id="eefb6-112">[Microsoft Azure SDK for Visual Studio 2015 (VS2015)](https://azure.microsoft.com/downloads/) **Note: Restart your machine after installing the SDK.**</span></span>
* <span data-ttu-id="eefb6-113">Microsoft Azure 구독: Azure 무료 평가판 계정에 등록 하려면 참조 [Azure 무료 평가판](https://azure.microsoft.com/free/)합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-113">Microsoft Azure subscription: To sign up for a free Azure trial account, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="creating-an-azure-web-role-application-that-exposes-signalr-performance-counters"></a><span data-ttu-id="eefb6-114">SignalR 성능 카운터를 노출 하는 Azure 웹 역할 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="eefb6-114">Creating an Azure Web Role application that exposes SignalR performance counters</span></span>

1. <span data-ttu-id="eefb6-115">Visual Studio 2015를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-115">Open Visual Studio 2015.</span></span>

2. <span data-ttu-id="eefb6-116">Visual Studio 2015에서 선택 **파일 &gt; 새로 &gt; 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-116">In Visual Studio 2015, select **File &gt; New &gt; Project**.</span></span>

3. <span data-ttu-id="eefb6-117">에 **템플릿** 의 창은 **새 프로젝트** 창의 **Visual C#** 노드를 선택는 **클라우드** 노드를 선택은 **Azure 클라우드 서비스** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="eefb6-117">In the **Templates** pane of the **New Project** window under the **Visual C#** node, select the **Cloud** node and select the **Azure Cloud Service** template.</span></span> <span data-ttu-id="eefb6-118">앱 이름 지정 **SignalRPerfCounters** 선택 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-118">Name the app **SignalRPerfCounters** and select **OK**.</span></span>

   ![새 클라우드 응용 프로그램](using-signalr-performance-counters-in-an-azure-web-role/_static/image1.png)
    
4. <span data-ttu-id="eefb6-120">에 **새 Microsoft Azure 클라우드 서비스** 대화 상자에서 **ASP.NET 웹 역할** 선택 하 고는  **&gt;**  단추를 역할 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-120">In the **New Microsoft Azure Cloud Service** dialog, select **ASP.NET Web Role** and select the **&gt;** button to add the role to the project.</span></span> <span data-ttu-id="eefb6-121">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-121">Select **OK**.</span></span>

   ![ASP.NET 웹 역할 추가](using-signalr-performance-counters-in-an-azure-web-role/_static/image2.png)
    
5. <span data-ttu-id="eefb6-123">에 **새 ASP.NET 웹 응용 프로그램-WebRole1** 대화 상자에서는 **MVC** 템플릿을 선택한 다음 선택 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-123">In the **New ASP.NET Web Application - WebRole1** dialog, select the **MVC** template, and then select **OK**.</span></span>

   ![MVC 및 Web API 추가](using-signalr-performance-counters-in-an-azure-web-role/_static/image3.png)
    
6. <span data-ttu-id="eefb6-125">**솔루션 탐색기**열고는 *diagnostics.wadcfgx* 아래 파일 **WebRole1**합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-125">In **Solution Explorer**, open the *diagnostics.wadcfgx* file under **WebRole1**.</span></span>

   ![솔루션 탐색기 diagnostics.wadcfgx](using-signalr-performance-counters-in-an-azure-web-role/_static/image4.png)
    
7. <span data-ttu-id="eefb6-127">다음 구성 파일의 내용을 바꿉니다 하 고 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-127">Replace the contents of the file with the following configuration and save the file:</span></span>

   [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample1.xml)]
    
8. <span data-ttu-id="eefb6-128">열기는 **패키지 관리자 콘솔** 에서 **도구 &gt; NuGet 패키지 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-128">Open the **Package Manager Console** from **Tools &gt; NuGet Package Manager**.</span></span> <span data-ttu-id="eefb6-129">SignalR 및 SignalR 유틸리티 패키지의 최신 버전을 설치 하려면 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-129">Enter the following commands to install the latest version of SignalR and the SignalR utilities package:</span></span>

   [!code-powershell[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample2.ps1)]
    
9. <span data-ttu-id="eefb6-130">시작 하거나 재활용 하는 경우 역할 인스턴스로 SignalR 성능 카운터를 설치 하려면 응용 프로그램을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-130">Configure the app to install the SignalR performance counters into the role instance when it starts up or recycles.</span></span> <span data-ttu-id="eefb6-131">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 **WebRole1** 프로젝트를 마우스 선택 **추가 &gt; 새 폴더**합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-131">In **Solution Explorer**, right-click on the **WebRole1** project and select **Add &gt; New Folder**.</span></span> <span data-ttu-id="eefb6-132">새 폴더 이름을 *시작*합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-132">Name the new folder *Startup*.</span></span>

   ![시작 폴더를 추가 합니다.](using-signalr-performance-counters-in-an-azure-web-role/_static/image5.png)
    
10. <span data-ttu-id="eefb6-134">복사는 *signalr.exe* 파일 (사용 하 여 추가 된 **Microsoft.AspNet.SignalR.Utils** 패키지)에서  **&lt;프로젝트 폴더&gt;\SignalRPerfCounters\packages\ Microsoft.AspNet.SignalR.Utils 합니다. &lt;버전&gt;\tools** 에 *시작* 이전 단계에서 만든 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-134">Copy the *signalr.exe* file (added with the **Microsoft.AspNet.SignalR.Utils** package) from **&lt;project folder&gt;\SignalRPerfCounters\packages\Microsoft.AspNet.SignalR.Utils.&lt;version&gt;\tools** to the *Startup* folder you created in the previous step.</span></span>

11. <span data-ttu-id="eefb6-135">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 *시작* 폴더와 선택 **추가 &gt; 기존 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-135">In **Solution Explorer**, right-click the *Startup* folder and select **Add &gt; Existing Item**.</span></span> <span data-ttu-id="eefb6-136">나타나는 대화 상자에서 선택 *signalr.exe* 선택 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-136">In the dialog that appears, select *signalr.exe* and select **Add**.</span></span>

    ![Signalr.exe 프로젝트에 추가](using-signalr-performance-counters-in-an-azure-web-role/_static/image6.png)
    
12. <span data-ttu-id="eefb6-138">마우스 오른쪽 단추로 클릭는 *시작* 사용자가 만든 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-138">Right-click on the *Startup* folder you created.</span></span> <span data-ttu-id="eefb6-139">선택 **추가 &gt; 새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-139">Select **Add &gt; New Item**.</span></span> <span data-ttu-id="eefb6-140">선택 된 **일반** 노드를 선택 **텍스트 파일**, 새 항목 이름을 *SignalRPerfCounterInstall.cmd*합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-140">Select the **General** node, select **Text File**, and name the new item *SignalRPerfCounterInstall.cmd*.</span></span> <span data-ttu-id="eefb6-141">이 명령 파일은 웹 역할로 SignalR 성능 카운터를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-141">This command file will install the SignalR performance counters into the web role.</span></span>

    ![SignalR 성능 카운터 설치 배치 파일 만들기](using-signalr-performance-counters-in-an-azure-web-role/_static/image7.png)
     
13. <span data-ttu-id="eefb6-143">Visual Studio를 만들 때의 *SignalRPerfCounterInstall.cmd* 파일을 자동으로 열립니다 주 창에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-143">When Visual Studio creates the *SignalRPerfCounterInstall.cmd* file, it will automatically open in the main window.</span></span> <span data-ttu-id="eefb6-144">다음 스크립트는 파일의 내용을 대체 한 다음 저장 하 고 파일을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-144">Replace the contents of the file with the following script, then save and close the file.</span></span> <span data-ttu-id="eefb6-145">이 스크립트 실행 *signalr.exe*, 역할 인스턴스 SignalR 성능 카운터에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-145">This script executes *signalr.exe*, which adds the SignalR performance counters to the role instance.</span></span>

    [!code-console[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample3.cmd)]
    
14. <span data-ttu-id="eefb6-146">선택 된 *signalr.exe* 파일 **솔루션 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-146">Select the *signalr.exe* file in **Solution Explorer**.</span></span> <span data-ttu-id="eefb6-147">파일의 **속성**설정, **출력 디렉터리로 복사** 를 **항상 복사**합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-147">In the file's **Properties**, set **Copy to Output Directory** to **Copy Always**.</span></span>

    ![항상 복사를 출력 디렉터리로 복사 설정](using-signalr-performance-counters-in-an-azure-web-role/_static/image8.png)
    
15. <span data-ttu-id="eefb6-149">에 대해 이전 단계를 반복 하는 *SignalRPerfCounterInstall.cmd* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-149">Repeat the previous step for the *SignalRPerfCounterInstall.cmd* file.</span></span>

    
16. <span data-ttu-id="eefb6-150">마우스 오른쪽 단추로 클릭는 *SignalRPerfCounterInstall.cmd* 파일을 선택 **프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-150">Right-click on the *SignalRPerfCounterInstall.cmd* file and select **Open With**.</span></span> <span data-ttu-id="eefb6-151">나타나는 대화 상자에서 선택 **바이너리 편집기** 선택 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-151">In the dialog that appears, select **Binary Editor** and select **OK**.</span></span>

    ![바이너리 편집기를 사용 하 여 열기](using-signalr-performance-counters-in-an-azure-web-role/_static/image9.png)
    
17. <span data-ttu-id="eefb6-153">바이너리 편집기에서 파일에 모든 선행 바이트를 선택 하 고 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-153">In the binary editor, select any leading bytes in the file and delete them.</span></span> <span data-ttu-id="eefb6-154">파일을 저장한 후 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-154">Save and close the file.</span></span>

    ![선행 바이트를 삭제 합니다.](using-signalr-performance-counters-in-an-azure-web-role/_static/image10.png)
    
18. <span data-ttu-id="eefb6-156">열기 *ServiceDefinition.csdef* 실행 되는 시작 작업을 추가 하 고는 *SignalrPerfCounterInstall.cmd* 서비스가 시작할 때 파일:</span><span class="sxs-lookup"><span data-stu-id="eefb6-156">Open *ServiceDefinition.csdef* and add a startup task that executes the *SignalrPerfCounterInstall.cmd* file when the service starts up:</span></span>

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample4.xml?highlight=4-7)]
    
19. <span data-ttu-id="eefb6-157">열기 `Views/Shared/_Layout.cshtml` jQuery 번들 스크립트 파일의 끝에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-157">Open `Views/Shared/_Layout.cshtml` and remove the jQuery bundle script from the end of the file.</span></span>

    [!code-cshtml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample5.cshtml)]
    
20. <span data-ttu-id="eefb6-158">추가 지속적으로 호출 하는 JavaScript 클라이언트는 `increment` 서버에서 메서드.</span><span class="sxs-lookup"><span data-stu-id="eefb6-158">Add a JavaScript client that continuously calls the `increment` method on the server.</span></span> <span data-ttu-id="eefb6-159">열기 `Views/Home/Index.cshtml` 하 고 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-159">Open `Views/Home/Index.cshtml` and replace the contents with the following code:</span></span>

    [!code-cshtml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample6.cshtml)]
    
21. <span data-ttu-id="eefb6-160">새 폴더 만들기는 **WebRole1** 라는 프로젝트 *허브*합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-160">Create a new folder in the **WebRole1** project named *Hubs*.</span></span> <span data-ttu-id="eefb6-161">마우스 오른쪽 단추로 클릭는 *허브* 폴더에 **솔루션 탐색기**선택, **웹 &gt; SignalR**를 선택 하 고 **SignalR 허브 클래스 (v2)**.</span><span class="sxs-lookup"><span data-stu-id="eefb6-161">Right-click the *Hubs* folder in **Solution Explorer**, select **Web &gt; SignalR**, and select **SignalR Hub Class (v2)**.</span></span> <span data-ttu-id="eefb6-162">새 허브 이름을 *MyHub.cs* 선택 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-162">Name the new hub *MyHub.cs* and select **Add**.</span></span>

    ![새 항목 추가 대화 상자에서 허브 폴더에 추가 하는 SignalR 허브 클래스](using-signalr-performance-counters-in-an-azure-web-role/_static/image13.png)

22. <span data-ttu-id="eefb6-164">*MyHub.cs* 주 창에 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-164">*MyHub.cs* will automatically open in the main window.</span></span> <span data-ttu-id="eefb6-165">내용을 다음 코드로 바꿉니다 다음 저장 하 고 파일을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-165">Replace the contents with the following code, then save and close the file:</span></span>

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample7.cs)]
    
23. <span data-ttu-id="eefb6-166">*[Crank.exe](signalr-connection-density-testing-with-crank.md)*  SignalR 코드 베이스와 함께 제공 되는 도구 테스트 연결 밀도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-166">*[Crank.exe](signalr-connection-density-testing-with-crank.md)* is a connection density testing tool provided with the SignalR codebase.</span></span> <span data-ttu-id="eefb6-167">크랭크 영구 연결을 요구 하므로 추가할 있습니다 사용할 사이트를 테스트할 때.</span><span class="sxs-lookup"><span data-stu-id="eefb6-167">Since Crank requires a persistent connection, you add one to your site for use when testing.</span></span> <span data-ttu-id="eefb6-168">새 폴더를 추가할는 **WebRole1** 라는 프로젝트 *PersistentConnections*합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-168">Add a new folder to the **WebRole1** project called *PersistentConnections*.</span></span> <span data-ttu-id="eefb6-169">이 폴더를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가 &gt; 클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-169">Right-click this folder and select **Add &gt; Class**.</span></span> <span data-ttu-id="eefb6-170">새 클래스 파일의 이름을 *MyPersistentConnections.cs* 선택 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-170">Name the new class file *MyPersistentConnections.cs* and select **Add**.</span></span>

24. <span data-ttu-id="eefb6-171">Visual Studio 열립니다는 *MyPersistentConnections.cs* 주 창에는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-171">Visual Studio will open the *MyPersistentConnections.cs* file in the main window.</span></span> <span data-ttu-id="eefb6-172">내용을 다음 코드로 바꿉니다 다음 저장 하 고 파일을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-172">Replace the contents with the following code, then save and close the file:</span></span>

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample8.cs)]
    
25. <span data-ttu-id="eefb6-173">사용 하는 `Startup` OWIN 시작 될 때 클래스 SignalR 개체를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-173">Using the `Startup` class, the SignalR objects start when OWIN starts up.</span></span> <span data-ttu-id="eefb6-174">열기 또는 만들기 *Startup.cs* 하 고 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-174">Open or create *Startup.cs* and replace the contents with the following code:</span></span>

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample9.cs)]
    
    <span data-ttu-id="eefb6-175">위의 코드에는 `OwinStartup` 특성 OWIN 시작 하려면이 클래스를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-175">In the code above, the `OwinStartup` attribute marks this class to start OWIN.</span></span> <span data-ttu-id="eefb6-176">`Configuration` 메서드 SignalR을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-176">The `Configuration` method starts SignalR.</span></span>
    
26. <span data-ttu-id="eefb6-177">Microsoft Azure 에뮬레이터에서 키를 눌러 응용 프로그램을 테스트 **F5**합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-177">Test your application in the Microsoft Azure Emulator by pressing **F5**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="eefb6-178">발생 하는 경우는 **FileLoadException** 에서 **MapSignalR**에 바인딩 리디렉션을 변경 *web.config* 다음과:</span><span class="sxs-lookup"><span data-stu-id="eefb6-178">If you encounter a **FileLoadException** at **MapSignalR**, change the binding redirects in *web.config* to the following:</span></span>

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample12.xml?highlight=3,7)]
    
27. <span data-ttu-id="eefb6-179">1 분 정도 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-179">Wait about one minute.</span></span> <span data-ttu-id="eefb6-180">Visual Studio에서 클라우드 탐색기 도구 창을 엽니다 (**보기 &gt; 클라우드 탐색기**) 경로 확장 하 고 `(Local)\Storage Accounts\(Development)\Tables`합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-180">Open the Cloud Explorer tool window in Visual Studio (**View &gt; Cloud Explorer**) and expand the path `(Local)\Storage Accounts\(Development)\Tables`.</span></span> <span data-ttu-id="eefb6-181">두 번 클릭 **WADPerformanceCountersTable**합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-181">Double-click **WADPerformanceCountersTable**.</span></span> <span data-ttu-id="eefb6-182">테이블 데이터의 SignalR 카운터에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-182">You should see SignalR counters in the table data.</span></span> <span data-ttu-id="eefb6-183">테이블 보이지 않으면 Azure 저장소 자격 증명을 입력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-183">If you don't see the table, you may need to re-enter your Azure Storage credentials.</span></span> <span data-ttu-id="eefb6-184">선택 해야는 **새로 고침** 표를 참조 하는 단추 **클라우드 탐색기** 선택 또는 **새로 고침** 테이블 열기 창의 테이블에 데이터를 보려면 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-184">You may need to select the **Refresh** button to see the table in **Cloud Explorer** or select the **Refresh** button in the open table window to see data in the table.</span></span>

    ![Visual Studio 클라우드 탐색기에서 WAD 성능 카운터 테이블을 선택 하면](using-signalr-performance-counters-in-an-azure-web-role/_static/image11.png)

    ![WAD 성능 카운터 테이블에서 수집 된 카운터를 표시 합니다.](using-signalr-performance-counters-in-an-azure-web-role/_static/image12.png)
    
28. <span data-ttu-id="eefb6-187">클라우드에서 응용 프로그램을 테스트 하려면 업데이트는 **ServiceConfiguration.Cloud.cscfg** 파일 및 설정는 `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` 에 유효한 Azure 저장소 계정 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-187">To test your application in the cloud, update the **ServiceConfiguration.Cloud.cscfg** file and set the `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` to a valid Azure Storage account connection string.</span></span>

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample10.xml)]

29. <span data-ttu-id="eefb6-188">Azure 구독에 응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-188">Deploy the application to your Azure subscription.</span></span> <span data-ttu-id="eefb6-189">Azure에 응용 프로그램을 배포 하는 방법에 대 한 세부 정보를 참조 하십시오. [만들어 클라우드 서비스를 배포 하는 방법을](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-189">For details on how to deploy an application to Azure, see [How to Create and Deploy a Cloud Service](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).</span></span>

30. <span data-ttu-id="eefb6-190">몇 분 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-190">Wait a few minutes.</span></span> <span data-ttu-id="eefb6-191">**클라우드 탐색기**, 위에 구성 된 저장소 계정 키를 찾아서 찾을 `WADPerformanceCountersTable` 테이블에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-191">In **Cloud Explorer**, locate the storage account you configured above and find the `WADPerformanceCountersTable` table in it.</span></span> <span data-ttu-id="eefb6-192">테이블 데이터의 SignalR 카운터에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-192">You should see SignalR counters in the table data.</span></span> <span data-ttu-id="eefb6-193">테이블 보이지 않으면 Azure 저장소 자격 증명을 입력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-193">If you don't see the table, you may need to re-enter your Azure Storage credentials.</span></span> <span data-ttu-id="eefb6-194">선택 해야는 **새로 고침** 표를 참조 하는 단추 **클라우드 탐색기** 선택 또는 **새로 고침** 테이블 열기 창의 테이블에 데이터를 보려면 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-194">You may need to select the **Refresh** button to see the table in **Cloud Explorer** or select the **Refresh** button in the open table window to see data in the table.</span></span>

<span data-ttu-id="eefb6-195">특히 감사 드립니다 [Martin Richard](https://social.msdn.microsoft.com/profile/Martin+Richard) 이 자습서에 사용 된 원래 콘텐츠에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="eefb6-195">Special thanks to [Martin Richard](https://social.msdn.microsoft.com/profile/Martin+Richard) for the original content used in this tutorial.</span></span>
