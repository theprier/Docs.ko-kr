---
uid: signalr/overview/performance/using-signalr-performance-counters-in-an-azure-web-role
title: Azure 웹 역할에서 SignalR 성능 카운터를 사용 하 여 | Microsoft Docs
author: guardrex
description: 설치 및 Azure 웹 역할에서 SignalR 성능 카운터를 사용 하는 방법입니다.
keywords: ASP.NET,signalr,performance 카운터, azure 웹 역할
ms.author: riande
ms.date: 10/03/2018
ms.assetid: 2a127d3b-21ed-4cc9-bec0-cdab4e742a25
msc.legacyurl: /signalr/overview/performance/using-signalr-performance-counters-in-an-azure-web-role
msc.type: authoredcontent
ms.openlocfilehash: bdd875201895c6eaf155b54582d0898c2570d93c
ms.sourcegitcommit: 74e3be25ea37b5fc8b4b433b0b872547b4b99186
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2018
ms.locfileid: "53287718"
---
# <a name="using-signalr-performance-counters-in-an-azure-web-role"></a><span data-ttu-id="a974a-104">Azure 웹 역할에서 SignalR 성능 카운터 사용</span><span class="sxs-lookup"><span data-stu-id="a974a-104">Using SignalR performance counters in an Azure Web Role</span></span>

<span data-ttu-id="a974a-105">[Luke Latham](https://github.com/guardrex)으로</span><span class="sxs-lookup"><span data-stu-id="a974a-105">By [Luke Latham](https://github.com/guardrex)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="a974a-106">SignalR 성능 카운터는 Azure 웹 역할에서 앱의 성능을 모니터링 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-106">SignalR performance counters are used to monitor your app's performance in an Azure Web Role.</span></span> <span data-ttu-id="a974a-107">카운터는 Microsoft Azure 진단에서 캡처됩니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-107">The counters are captured by Microsoft Azure Diagnostics.</span></span> <span data-ttu-id="a974a-108">SignalR 성능 카운터를 사용 하 여 Azure에서 설치한 *signalr.exe*, 독립 실행형 또는 온-프레미스 앱에 사용 되는 동일한 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-108">You install SignalR performance counters on Azure with *signalr.exe*, the same tool used for standalone or on-premises apps.</span></span> <span data-ttu-id="a974a-109">Azure 역할 일시적인 되므로 설치 및 시작 시 SignalR 성능 카운터를 등록 하려면 앱을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-109">Since Azure roles are transient, you configure an app to install and register SignalR performance counters upon startup.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a974a-110">전제 조건</span><span class="sxs-lookup"><span data-stu-id="a974a-110">Prerequisites</span></span>

* <span data-ttu-id="a974a-111">Visual Studio 2015 또는 [2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)</span><span class="sxs-lookup"><span data-stu-id="a974a-111">Visual Studio 2015 or [2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)</span></span>
* <span data-ttu-id="a974a-112">[Microsoft Azure SDK for Visual Studio](https://azure.microsoft.com/downloads/) **참고 합니다. SDK를 설치한 후 컴퓨터를 다시 시작 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a974a-112">[Microsoft Azure SDK for Visual Studio](https://azure.microsoft.com/downloads/) **Note: Restart your machine after installing the SDK.**</span></span>
* <span data-ttu-id="a974a-113">Microsoft Azure 구독: 무료 Azure 평가판 계정에 대 한 등록을 참조 하세요 [Azure 무료 평가판](https://azure.microsoft.com/free/)합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-113">Microsoft Azure subscription: To sign up for a free Azure trial account, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="creating-an-azure-web-role-application-that-exposes-signalr-performance-counters"></a><span data-ttu-id="a974a-114">SignalR 성능 카운터를 노출 하는 Azure 웹 역할 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="a974a-114">Creating an Azure Web Role application that exposes SignalR performance counters</span></span>

1. <span data-ttu-id="a974a-115">Visual Studio를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-115">Open Visual Studio.</span></span>

2. <span data-ttu-id="a974a-116">Visual Studio에서 **파일** > **새로 만들기** > **프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-116">In Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="a974a-117">에 **새 프로젝트** 대화 상자에서를 **Visual C#** > **클라우드** 왼쪽의 범주를 선택한는 **Azure클라우드서비스** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="a974a-117">In the **New Project** dialog box, select the **Visual C#** > **Cloud** category on the left, and then select the **Azure Cloud Service** template.</span></span> <span data-ttu-id="a974a-118">앱의 이름을 **SignalRPerfCounters** 선택한 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-118">Name the app **SignalRPerfCounters** and select **OK**.</span></span>

   ![새 클라우드 응용 프로그램](using-signalr-performance-counters-in-an-azure-web-role/_static/image1.png)

   > [!NOTE]
   > <span data-ttu-id="a974a-120">표시 되지 않는 경우는 **클라우드** 템플릿 범주 또는 **Azure 클라우드 서비스** 템플릿을 설치 해야 합니다 **Azure 개발** Visual Studio 2017에 대 한 워크 로드.</span><span class="sxs-lookup"><span data-stu-id="a974a-120">If you don't see the **Cloud** template category or the **Azure Cloud Service** template, you need to install the **Azure development** workload for Visual Studio 2017.</span></span> <span data-ttu-id="a974a-121">선택 합니다 **Visual Studio 설치 관리자 열기** 의 왼쪽 맨 아래에서 링크는 **새 프로젝트** Visual Studio 설치 관리자를 열려면 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="a974a-121">Choose the **Open Visual Studio Installer** link on the bottom-left side of the **New Project** dialog to open Visual Studio Installer.</span></span> <span data-ttu-id="a974a-122">선택 된 **Azure 개발** 워크 로드를 선택한 후 **수정** 워크 로드를 설치 하려면.</span><span class="sxs-lookup"><span data-stu-id="a974a-122">Select the **Azure development** workload, and then choose **Modify** to start installing the workload.</span></span>
   >
   > ![Visual Studio 설치 관리자의 azure 개발 워크 로드](using-signalr-performance-counters-in-an-azure-web-role/_static/azure-development-workload.png)

4. <span data-ttu-id="a974a-124">에 **새 Microsoft Azure 클라우드 서비스** 대화 상자에서 **ASP.NET 웹 역할** 선택한를 > 프로젝트에 역할을 추가 하려면 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-124">In the **New Microsoft Azure Cloud Service** dialog, select **ASP.NET Web Role** and select the > button to add the role to the project.</span></span> <span data-ttu-id="a974a-125">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-125">Select **OK**.</span></span>

   ![ASP.NET 웹 역할 추가](using-signalr-performance-counters-in-an-azure-web-role/_static/image2.png)

5. <span data-ttu-id="a974a-127">에 **새 ASP.NET 웹 응용 프로그램-WebRole1** 대화 상자에서 선택 합니다 **MVC** 템플릿을 선택한 후 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-127">In the **New ASP.NET Web Application - WebRole1** dialog, select the **MVC** template, and then select **OK**.</span></span>

   ![MVC 및 Web API를 추가 합니다.](using-signalr-performance-counters-in-an-azure-web-role/_static/image3.png)

6. <span data-ttu-id="a974a-129">**솔루션 탐색기**오픈 합니다 *diagnostics.wadcfgx* 파일 **WebRole1**합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-129">In **Solution Explorer**, open the *diagnostics.wadcfgx* file under **WebRole1**.</span></span>

   ![솔루션 탐색기 diagnostics.wadcfgx](using-signalr-performance-counters-in-an-azure-web-role/_static/image4.png)

7. <span data-ttu-id="a974a-131">다음 구성을 사용 하 여 파일의 내용을 바꾸고 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-131">Replace the contents of the file with the following configuration and save the file:</span></span>

   [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample1.xml)]

8. <span data-ttu-id="a974a-132">엽니다는 **패키지 관리자 콘솔** 에서 **도구** > **NuGet 패키지 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-132">Open the **Package Manager Console** from **Tools** > **NuGet Package Manager**.</span></span> <span data-ttu-id="a974a-133">최신 버전의 SignalR 및 SignalR 유틸리티 패키지를 설치 하려면 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-133">Enter the following commands to install the latest version of SignalR and the SignalR utilities package:</span></span>

   [!code-powershell[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample2.ps1)]

9. <span data-ttu-id="a974a-134">시작 하거나 재활용 하는 경우 역할 인스턴스로 SignalR 성능 카운터를 설치 하도록 앱을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-134">Configure the app to install the SignalR performance counters into the role instance when it starts up or recycles.</span></span> <span data-ttu-id="a974a-135">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **WebRole1** 프로젝트를 마우스 **추가** > **새 폴더**합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-135">In **Solution Explorer**, right-click on the **WebRole1** project and select **Add** > **New Folder**.</span></span> <span data-ttu-id="a974a-136">새 폴더의 이름을 *시작*합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-136">Name the new folder *Startup*.</span></span>

   ![시작 폴더를 추가 합니다.](using-signalr-performance-counters-in-an-azure-web-role/_static/image5.png)

10. <span data-ttu-id="a974a-138">복사 합니다 *signalr.exe* 파일 (사용 하 여 추가 합니다 **Microsoft.AspNet.SignalR.Utils** 패키지)에서 \<프로젝트 폴더 > / SignalRPerfCounters/packages/Microsoft.AspNet.SignalR.Utils.\< 버전 > 도구 / 합니다 *시작* 이전 단계에서 만든 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-138">Copy the *signalr.exe* file (added with the **Microsoft.AspNet.SignalR.Utils** package) from \<project folder>/SignalRPerfCounters/packages/Microsoft.AspNet.SignalR.Utils.\<version>/tools to the *Startup* folder you created in the previous step.</span></span>

11. <span data-ttu-id="a974a-139">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 *시작* 폴더를 선택 **추가** > **기존 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-139">In **Solution Explorer**, right-click the *Startup* folder and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="a974a-140">나타나는 대화 상자에서 선택 *signalr.exe* 선택한 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-140">In the dialog that appears, select *signalr.exe* and select **Add**.</span></span>

    ![Signalr.exe 프로젝트에 추가](using-signalr-performance-counters-in-an-azure-web-role/_static/image6.png)

12. <span data-ttu-id="a974a-142">마우스 오른쪽 단추로 클릭 합니다 *시작* 사용자가 만든 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-142">Right-click on the *Startup* folder you created.</span></span> <span data-ttu-id="a974a-143">**추가** > **새 항목**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-143">Select **Add** > **New Item**.</span></span> <span data-ttu-id="a974a-144">선택 합니다 **일반** 노드를 선택 **텍스트 파일**, 및 새 항목의 이름을 *SignalRPerfCounterInstall.cmd*합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-144">Select the **General** node, select **Text File**, and name the new item *SignalRPerfCounterInstall.cmd*.</span></span> <span data-ttu-id="a974a-145">이 명령 파일은 웹 역할에 SignalR 성능 카운터를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-145">This command file will install the SignalR performance counters into the web role.</span></span>

    ![SignalR 성능 카운터 설치 일괄 처리 파일 만들기](using-signalr-performance-counters-in-an-azure-web-role/_static/image7.png)

13. <span data-ttu-id="a974a-147">Visual Studio를 만들 때 합니다 *SignalRPerfCounterInstall.cmd* 파일을 자동으로 열립니다 주 창에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-147">When Visual Studio creates the *SignalRPerfCounterInstall.cmd* file, it will automatically open in the main window.</span></span> <span data-ttu-id="a974a-148">다음 스크립트를 사용 하 여 파일의 내용을 대체 하 고 저장 파일을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-148">Replace the contents of the file with the following script, then save and close the file.</span></span> <span data-ttu-id="a974a-149">이 스크립트 실행 *signalr.exe*, 역할 인스턴스에 SignalR 성능 카운터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-149">This script executes *signalr.exe*, which adds the SignalR performance counters to the role instance.</span></span>

    [!code-console[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample3.cmd)]

14. <span data-ttu-id="a974a-150">선택 된 *signalr.exe* 파일 **솔루션 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-150">Select the *signalr.exe* file in **Solution Explorer**.</span></span> <span data-ttu-id="a974a-151">파일의 **속성**설정 **출력 디렉터리로 복사** 하 **항상 복사**합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-151">In the file's **Properties**, set **Copy to Output Directory** to **Copy Always**.</span></span>

    ![항상 복사을 출력 디렉터리로 복사 설정](using-signalr-performance-counters-in-an-azure-web-role/_static/image8.png)

15. <span data-ttu-id="a974a-153">에 대 한 이전 단계를 반복 합니다 *SignalRPerfCounterInstall.cmd* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-153">Repeat the previous step for the *SignalRPerfCounterInstall.cmd* file.</span></span>


16. <span data-ttu-id="a974a-154">마우스 오른쪽 단추로 클릭 합니다 *SignalRPerfCounterInstall.cmd* 파일을 선택 **연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-154">Right-click on the *SignalRPerfCounterInstall.cmd* file and select **Open With**.</span></span> <span data-ttu-id="a974a-155">나타나는 대화 상자에서 선택 **바이너리 편집기** 선택한 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-155">In the dialog that appears, select **Binary Editor** and select **OK**.</span></span>

    ![바이너리 편집기를 사용 하 여 열기](using-signalr-performance-counters-in-an-azure-web-role/_static/image9.png)

17. <span data-ttu-id="a974a-157">바이너리 편집기에서 파일에서 모든 선행 바이트를 선택 하 고 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-157">In the binary editor, select any leading bytes in the file and delete them.</span></span> <span data-ttu-id="a974a-158">파일을 저장한 후 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-158">Save and close the file.</span></span>

    ![선행 바이트를 삭제 합니다.](using-signalr-performance-counters-in-an-azure-web-role/_static/image10.png)

18. <span data-ttu-id="a974a-160">열기 *ServiceDefinition.csdef* 를 실행 하는 시작 작업을 추가 합니다 *SignalrPerfCounterInstall.cmd* 서비스를 시작할 때 파일:</span><span class="sxs-lookup"><span data-stu-id="a974a-160">Open *ServiceDefinition.csdef* and add a startup task that executes the *SignalrPerfCounterInstall.cmd* file when the service starts up:</span></span>

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample4.xml?highlight=4-7)]

19. <span data-ttu-id="a974a-161">열기 `Views/Shared/_Layout.cshtml` jQuery 번들 스크립트 파일의 끝에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-161">Open `Views/Shared/_Layout.cshtml` and remove the jQuery bundle script from the end of the file.</span></span>

    [!code-cshtml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample5.cshtml)]

20. <span data-ttu-id="a974a-162">계속 해 서 호출 하는 JavaScript 클라이언트를 추가 합니다 `increment` 서버의 메서드.</span><span class="sxs-lookup"><span data-stu-id="a974a-162">Add a JavaScript client that continuously calls the `increment` method on the server.</span></span> <span data-ttu-id="a974a-163">열기 `Views/Home/Index.cshtml` 그 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-163">Open `Views/Home/Index.cshtml` and replace the contents with the following code:</span></span>

    [!code-cshtml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample6.cshtml)]

21. <span data-ttu-id="a974a-164">새 폴더를 만듭니다는 **WebRole1** 라는 프로젝트가 *Hubs*합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-164">Create a new folder in the **WebRole1** project named *Hubs*.</span></span> <span data-ttu-id="a974a-165">마우스 오른쪽 단추로 클릭 합니다 *Hubs* 폴더에서 **솔루션 탐색기** 선택한 **추가** > **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-165">Right-click the *Hubs* folder in **Solution Explorer** and select **Add** > **New Item**.</span></span> <span data-ttu-id="a974a-166">에 **새 항목 추가** 대화 상자를 선택 합니다 **웹** > **SignalR** 범주를 선택한 후는 **SignalR 허브 클래스 (v2)** 항목 템플릿.</span><span class="sxs-lookup"><span data-stu-id="a974a-166">In the **Add New Item** dialog box, select the **Web** > **SignalR** category, and then select the **SignalR Hub Class (v2)** item template.</span></span> <span data-ttu-id="a974a-167">새 허브의 이름을 *MyHub.cs* 선택한 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-167">Name the new hub *MyHub.cs* and select **Add**.</span></span>

    ![새 항목 추가 대화 상자에서 허브 폴더로 SignalR 허브 클래스 추가](using-signalr-performance-counters-in-an-azure-web-role/_static/image13.png)

22. <span data-ttu-id="a974a-169">*MyHub.cs* 주 창에 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-169">*MyHub.cs* will automatically open in the main window.</span></span> <span data-ttu-id="a974a-170">콘텐츠를 다음 코드로 바꿉니다 하 고 저장 파일을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-170">Replace the contents with the following code, then save and close the file:</span></span>

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample7.cs)]

23. <span data-ttu-id="a974a-171">*[Crank.exe](signalr-connection-density-testing-with-crank.md)*  SignalR 코드 베이스를 사용 하 여 제공 하는 도구를 테스트 하는 연결 밀도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-171">*[Crank.exe](signalr-connection-density-testing-with-crank.md)* is a connection density testing tool provided with the SignalR codebase.</span></span> <span data-ttu-id="a974a-172">크랭크를 영구 연결을 요구 하므로를 추가 하면 사용할 사이트를 테스트할 때.</span><span class="sxs-lookup"><span data-stu-id="a974a-172">Since Crank requires a persistent connection, you add one to your site for use when testing.</span></span> <span data-ttu-id="a974a-173">새 폴더를 추가 합니다 **WebRole1** 라는 프로젝트 *PersistentConnections*합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-173">Add a new folder to the **WebRole1** project called *PersistentConnections*.</span></span> <span data-ttu-id="a974a-174">이 폴더를 마우스 오른쪽 단추로 누르고 **추가** > **클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-174">Right-click this folder and select **Add** > **Class**.</span></span> <span data-ttu-id="a974a-175">새 클래스 파일의 이름을 *MyPersistentConnections.cs* 선택한 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-175">Name the new class file *MyPersistentConnections.cs* and select **Add**.</span></span>

24. <span data-ttu-id="a974a-176">Visual Studio에서 열립니다는 *MyPersistentConnections.cs* 주 창에는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-176">Visual Studio will open the *MyPersistentConnections.cs* file in the main window.</span></span> <span data-ttu-id="a974a-177">콘텐츠를 다음 코드로 바꿉니다 하 고 저장 파일을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-177">Replace the contents with the following code, then save and close the file:</span></span>

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample8.cs)]

25. <span data-ttu-id="a974a-178">사용 하는 `Startup` OWIN 시작 되 면 클래스, SignalR 개체를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-178">Using the `Startup` class, the SignalR objects start when OWIN starts up.</span></span> <span data-ttu-id="a974a-179">열기 또는 만들기 *Startup.cs* 그 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-179">Open or create *Startup.cs* and replace the contents with the following code:</span></span>

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample9.cs)]

    <span data-ttu-id="a974a-180">위의 코드는 `OwinStartup` 특성이이 OWIN 시작이 클래스를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-180">In the code above, the `OwinStartup` attribute marks this class to start OWIN.</span></span> <span data-ttu-id="a974a-181">`Configuration` 메서드 SignalR을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-181">The `Configuration` method starts SignalR.</span></span>

26. <span data-ttu-id="a974a-182">키를 눌러 Microsoft Azure 에뮬레이터에서 응용 프로그램을 테스트 **F5**합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-182">Test your application in the Microsoft Azure Emulator by pressing **F5**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a974a-183">발생 하는 경우는 **FileLoadException** 언제 **MapSignalR**에 바인딩 리디렉션을 변경 *web.config* 다음과:</span><span class="sxs-lookup"><span data-stu-id="a974a-183">If you encounter a **FileLoadException** at **MapSignalR**, change the binding redirects in *web.config* to the following:</span></span>

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample12.xml?highlight=3,7)]

27. <span data-ttu-id="a974a-184">1 분 정도 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-184">Wait about one minute.</span></span> <span data-ttu-id="a974a-185">Visual Studio에서 클라우드 탐색기 도구 창을 엽니다 (**뷰** > **클라우드 탐색기**) 경로 확장 하 고 `(Local)/Storage Accounts/(Development)/Tables`입니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-185">Open the Cloud Explorer tool window in Visual Studio (**View** > **Cloud Explorer**) and expand the path `(Local)/Storage Accounts/(Development)/Tables`.</span></span> <span data-ttu-id="a974a-186">두 번 클릭 **WADPerformanceCountersTable**합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-186">Double-click **WADPerformanceCountersTable**.</span></span> <span data-ttu-id="a974a-187">테이블 데이터의 SignalR 카운터에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-187">You should see SignalR counters in the table data.</span></span> <span data-ttu-id="a974a-188">테이블 표시 되지 않으면, Azure Storage 자격 증명을 다시 입력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-188">If you don't see the table, you may need to re-enter your Azure Storage credentials.</span></span> <span data-ttu-id="a974a-189">선택 해야 할 수도 있습니다는 **새로 고침** 의 표를 참조 하는 단추 **클라우드 탐색기** 선택 또는 합니다 **새로 고침** 테이블 데이터를 보려면 테이블 열기 창에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-189">You may need to select the **Refresh** button to see the table in **Cloud Explorer** or select the **Refresh** button in the open table window to see data in the table.</span></span>

    ![Visual Studio 클라우드 탐색기에서 WAD 성능 카운터 테이블 선택](using-signalr-performance-counters-in-an-azure-web-role/_static/image11.png)

    ![WAD 성능 카운터 테이블에서 수집 된 카운터를 표시 합니다.](using-signalr-performance-counters-in-an-azure-web-role/_static/image12.png)

28. <span data-ttu-id="a974a-192">클라우드에서 응용 프로그램을 테스트 하려면 업데이트를 **ServiceConfiguration.Cloud.cscfg** 파일을 `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` 유효한 Azure 저장소 계정 연결 문자열을 합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-192">To test your application in the cloud, update the **ServiceConfiguration.Cloud.cscfg** file and set the `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` to a valid Azure Storage account connection string.</span></span>

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample10.xml)]

29. <span data-ttu-id="a974a-193">Azure 구독에 응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-193">Deploy the application to your Azure subscription.</span></span> <span data-ttu-id="a974a-194">Azure에 응용 프로그램을 배포 하는 방법에 대 한 내용은 참조 하세요 [클라우드 서비스 만들기 및 배포 하는 방법을](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-194">For details on how to deploy an application to Azure, see [How to Create and Deploy a Cloud Service](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).</span></span>

30. <span data-ttu-id="a974a-195">몇 분 동안 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-195">Wait a few minutes.</span></span> <span data-ttu-id="a974a-196">**클라우드 탐색기**, 위에서 구성한 저장소 계정 키를 찾아 찾을 `WADPerformanceCountersTable` 에 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-196">In **Cloud Explorer**, locate the storage account you configured above and find the `WADPerformanceCountersTable` table in it.</span></span> <span data-ttu-id="a974a-197">테이블 데이터의 SignalR 카운터에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-197">You should see SignalR counters in the table data.</span></span> <span data-ttu-id="a974a-198">테이블 표시 되지 않으면, Azure Storage 자격 증명을 다시 입력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-198">If you don't see the table, you may need to re-enter your Azure Storage credentials.</span></span> <span data-ttu-id="a974a-199">선택 해야 할 수도 있습니다는 **새로 고침** 의 표를 참조 하는 단추 **클라우드 탐색기** 선택 또는 합니다 **새로 고침** 테이블 데이터를 보려면 테이블 열기 창에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-199">You may need to select the **Refresh** button to see the table in **Cloud Explorer** or select the **Refresh** button in the open table window to see data in the table.</span></span>

<span data-ttu-id="a974a-200">특히 감사 드립니다 [Martin Richard](https://social.msdn.microsoft.com/profile/Martin+Richard) 이 자습서에 사용 되는 원래 콘텐츠에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a974a-200">Special thanks to [Martin Richard](https://social.msdn.microsoft.com/profile/Martin+Richard) for the original content used in this tutorial.</span></span>
