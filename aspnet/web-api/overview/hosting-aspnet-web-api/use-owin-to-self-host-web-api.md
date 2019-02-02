---
uid: web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
title: OWIN 자체 호스트 하는 ASP.NET Web API 사용 | Microsoft Docs
author: rick-anderson
description: 이 자습서에는 OWIN 자체 호스트 하는 Web API 프레임 워크를 사용 하 여 콘솔 응용 프로그램에서 ASP.NET Web API를 호스트 하는 방법을 보여 줍니다. Open Web Interface for.NET (OWIN) d...
ms.author: riande
ms.date: 07/09/2013
ms.assetid: a90a04ce-9d07-43ad-8250-8a92fb2bd3d5
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
msc.type: authoredcontent
ms.openlocfilehash: 59ce24aa47ca590fbe9b617dbbe8bc6b3711849e
ms.sourcegitcommit: ed76cc752966c604a795fbc56d5a71d16ded0b58
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/02/2019
ms.locfileid: "55667390"
---
<a name="use-owin-to-self-host-aspnet-web-api"></a><span data-ttu-id="92034-104">OWIN을 사용 하 여 자체 호스트 하는 ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="92034-104">Use OWIN to Self-Host ASP.NET Web API</span></span> 
====================

> <span data-ttu-id="92034-105">이 자습서에는 OWIN 자체 호스트 하는 Web API 프레임 워크를 사용 하 여 콘솔 응용 프로그램에서 ASP.NET Web API를 호스트 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="92034-105">This tutorial shows how to host ASP.NET Web API in a console application, using OWIN to self-host the Web API framework.</span></span>
>
> <span data-ttu-id="92034-106">[Open Web Interface for.NET](http://owin.org) (OWIN).NET 웹 서버 및 웹 응용 프로그램 간의 추상화를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="92034-106">[Open Web Interface for .NET](http://owin.org) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="92034-107">OWIN 이상적인 OWIN 자체 IIS 외부에서 사용자 고유의 프로세스에서 웹 응용 프로그램을 호스팅하는 서버에서 웹 응용 프로그램을 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="92034-107">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="92034-108">이 자습서에 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="92034-108">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="92034-109">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="92034-109">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/) 
> - <span data-ttu-id="92034-110">웹 API 5.2.7</span><span class="sxs-lookup"><span data-stu-id="92034-110">Web API 5.2.7</span></span>


> [!NOTE]
> <span data-ttu-id="92034-111">이 자습서에 대 한 전체 소스 코드를 찾을 수 있습니다 [aspnet.codeplex.com](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OwinSelfhostSample/ReadMe.txt)합니다.</span><span class="sxs-lookup"><span data-stu-id="92034-111">You can find the complete source code for this tutorial at [aspnet.codeplex.com](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OwinSelfhostSample/ReadMe.txt).</span></span>


## <a name="create-a-console-application"></a><span data-ttu-id="92034-112">콘솔 애플리케이션 만들기</span><span class="sxs-lookup"><span data-stu-id="92034-112">Create a console application</span></span>

<span data-ttu-id="92034-113">에 **파일** 메뉴에서 **새로 만들기**을 선택한 후 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="92034-113">On the **File** menu,  **New**, then select **Project**.</span></span> <span data-ttu-id="92034-114">**설치 됨**아래에 있는 **Visual C#** 선택 **Windows Desktop** 선택한 후 **콘솔 앱 (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="92034-114">From **Installed**, under **Visual C#**, select **Windows Desktop** and then select **Console App (.Net Framework)**.</span></span> <span data-ttu-id="92034-115">"OwinSelfhostSample" 프로젝트 이름을 선택한 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="92034-115">Name the project "OwinSelfhostSample" and select **OK**.</span></span>

[![](use-owin-to-self-host-web-api/_static/image7.png)](use-owin-to-self-host-web-api/_static/image7.png)

## <a name="add-the-web-api-and-owin-packages"></a><span data-ttu-id="92034-116">Web API 및 OWIN 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="92034-116">Add the Web API and OWIN packages</span></span>

<span data-ttu-id="92034-117">**도구** 메뉴에서 **NuGet 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="92034-117">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="92034-118">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="92034-118">In the Package Manager Console window, enter the following command:</span></span>

`Install-Package Microsoft.AspNet.WebApi.OwinSelfHost`

<span data-ttu-id="92034-119">이 WebAPI OWIN selfhost 패키지 및 모든 필수 OWIN 패키지가 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92034-119">This will install the WebAPI OWIN selfhost package and all the required OWIN packages.</span></span>

[![](use-owin-to-self-host-web-api/_static/image4.png)](use-owin-to-self-host-web-api/_static/image3.png)

## <a name="configure-web-api-for-self-host"></a><span data-ttu-id="92034-120">Web API를 구성에 대 한 자체 호스트</span><span class="sxs-lookup"><span data-stu-id="92034-120">Configure Web API for self-host</span></span>

<span data-ttu-id="92034-121">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가** / **클래스** 새 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="92034-121">In Solution Explorer, right-click the project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="92034-122">클래스 이름을 `Startup`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="92034-122">Name the class `Startup`.</span></span>

![](use-owin-to-self-host-web-api/_static/image5.png)

<span data-ttu-id="92034-123">모두이 파일의 상용구 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="92034-123">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample1.cs)]

## <a name="add-a-web-api-controller"></a><span data-ttu-id="92034-124">Web API 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="92034-124">Add a Web API controller</span></span>

<span data-ttu-id="92034-125">다음으로, Web API 컨트롤러 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="92034-125">Next, add a Web API controller class.</span></span> <span data-ttu-id="92034-126">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가** / **클래스** 새 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="92034-126">In Solution Explorer, right-click the project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="92034-127">클래스 이름을 `ValuesController`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="92034-127">Name the class `ValuesController`.</span></span>

<span data-ttu-id="92034-128">모두이 파일의 상용구 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="92034-128">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample2.cs)]

## <a name="start-the-owin-host-and-make-a-request-with-httpclient"></a><span data-ttu-id="92034-129">OWIN 호스트를 시작 하 고 HttpClient 사용 하 여 요청을 만듭니다</span><span class="sxs-lookup"><span data-stu-id="92034-129">Start the OWIN Host and make a request with HttpClient</span></span>

<span data-ttu-id="92034-130">다음을 사용 하 여 모든 Program.cs 파일의 상용구 코드를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="92034-130">Replace all of the boilerplate code in the Program.cs file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample3.cs)]

## <a name="run-the-application"></a><span data-ttu-id="92034-131">애플리케이션 실행</span><span class="sxs-lookup"><span data-stu-id="92034-131">Run the application</span></span>

<span data-ttu-id="92034-132">Visual Studio에서 F5 키를 눌러 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="92034-132">To run the application, press F5 in Visual Studio.</span></span> <span data-ttu-id="92034-133">출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="92034-133">The output should look like the following:</span></span>

[!code-console[Main](use-owin-to-self-host-web-api/samples/sample4.cmd)]

![](use-owin-to-self-host-web-api/_static/image6.png)

## <a name="additional-resources"></a><span data-ttu-id="92034-134">추가 자료</span><span class="sxs-lookup"><span data-stu-id="92034-134">Additional resources</span></span>

[<span data-ttu-id="92034-135">프로젝트 Katana 개요</span><span class="sxs-lookup"><span data-stu-id="92034-135">An Overview of Project Katana</span></span>](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)

[<span data-ttu-id="92034-136">Azure 작업자 역할에서 ASP.NET Web API 호스팅</span><span class="sxs-lookup"><span data-stu-id="92034-136">Host ASP.NET Web API in an Azure Worker Role</span></span>](host-aspnet-web-api-in-an-azure-worker-role.md)
