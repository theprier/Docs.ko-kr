---
uid: web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
title: OWIN를 사용 하 여 ASP.NET Web API 2 자체 호스트할 | Microsoft Docs
author: rick-anderson
description: 이 자습서에는 OWIN 자체 호스트 하는 Web API 프레임 워크를 사용 하 여 콘솔 응용 프로그램에서 ASP.NET 웹 API를 호스트 하는 방법을 보여 줍니다. .NET (OWIN) d에 대 한 웹 인터페이스를 열기...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/09/2013
ms.topic: article
ms.assetid: a90a04ce-9d07-43ad-8250-8a92fb2bd3d5
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
msc.type: authoredcontent
ms.openlocfilehash: fda0db8155c3303907331a690af35f619b589154
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
ms.locfileid: "26506972"
---
<a name="use-owin-to-self-host-aspnet-web-api-2"></a><span data-ttu-id="68572-104">OWIN를 사용 하 여 자체 호스트 하는 ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="68572-104">Use OWIN to Self-Host ASP.NET Web API 2</span></span>
====================
<span data-ttu-id="68572-105">으로 [Kanchan Mehrotra](https://twitter.com/kanchanmeh)</span><span class="sxs-lookup"><span data-stu-id="68572-105">by [Kanchan Mehrotra](https://twitter.com/kanchanmeh)</span></span>

> <span data-ttu-id="68572-106">이 자습서에는 OWIN 자체 호스트 하는 Web API 프레임 워크를 사용 하 여 콘솔 응용 프로그램에서 ASP.NET 웹 API를 호스트 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="68572-106">This tutorial shows how to host ASP.NET Web API in a console application, using OWIN to self-host the Web API framework.</span></span>
> 
> <span data-ttu-id="68572-107">[.NET 용 웹 인터페이스를 열고](http://owin.org) (OWIN).NET 웹 서버와 웹 응용 프로그램 간의 추상화를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="68572-107">[Open Web Interface for .NET](http://owin.org) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="68572-108">OWIN은 OWIN를 자체 IIS 외부의 사용자가 소유한 프로세스에는 웹 응용 프로그램을 호스트 하기에 이상적인는 서버에서 웹 응용 프로그램을 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="68572-108">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="68572-109">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="68572-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="68572-110">[Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads) (Visual Studio 2012와도 작동)</span><span class="sxs-lookup"><span data-stu-id="68572-110">[Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads) (also works with Visual Studio 2012)</span></span>
> - <span data-ttu-id="68572-111">Web API 2</span><span class="sxs-lookup"><span data-stu-id="68572-111">Web API 2</span></span>


> [!NOTE]
> <span data-ttu-id="68572-112">이 자습서에 대 한 전체 소스 코드를 찾을 수 있습니다 [aspnet.codeplex.com](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OwinSelfhostSample/ReadMe.txt)합니다.</span><span class="sxs-lookup"><span data-stu-id="68572-112">You can find the complete source code for this tutorial at [aspnet.codeplex.com](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OwinSelfhostSample/ReadMe.txt).</span></span>


## <a name="create-a-console-application"></a><span data-ttu-id="68572-113">콘솔 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="68572-113">Create a Console Application</span></span>

<span data-ttu-id="68572-114">에 **파일** 메뉴를 클릭 **새로**, 클릭 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="68572-114">On the **File** menu, click **New**, then click **Project**.</span></span> <span data-ttu-id="68572-115">**설치 된 템플릿**, Visual C#, 클릭 **Windows** 클릭 하 고 **콘솔 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="68572-115">From **Installed Templates**, under Visual C#, click **Windows** and then click **Console Application**.</span></span> <span data-ttu-id="68572-116">"OwinSelfhostSample" 프로젝트 이름을 지정 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="68572-116">Name the project "OwinSelfhostSample" and click **OK**.</span></span>

[![](use-owin-to-self-host-web-api/_static/image2.png)](use-owin-to-self-host-web-api/_static/image1.png)

## <a name="add-the-web-api-and-owin-packages"></a><span data-ttu-id="68572-117">Web API 및 OWIN 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="68572-117">Add the Web API and OWIN Packages</span></span>

<span data-ttu-id="68572-118">**도구** 메뉴를 클릭 하 여 **라이브러리 패키지 관리자**, 클릭 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="68572-118">From the **Tools** menu, click **Library Package Manager**, then click **Package Manager Console**.</span></span> <span data-ttu-id="68572-119">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="68572-119">In the Package Manager Console window, enter the following command:</span></span>

`Install-Package Microsoft.AspNet.WebApi.OwinSelfHost`

<span data-ttu-id="68572-120">그러면 WebAPI OWIN selfhost 패키지 및 필요한 모든 OWIN 패키지가 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68572-120">This will install the WebAPI OWIN selfhost package and all the required OWIN packages.</span></span>

[![](use-owin-to-self-host-web-api/_static/image4.png)](use-owin-to-self-host-web-api/_static/image3.png)

## <a name="configure-web-api-for-self-host"></a><span data-ttu-id="68572-121">Web API에 대 한 구성 자체 호스트</span><span class="sxs-lookup"><span data-stu-id="68572-121">Configure Web API for Self-Host</span></span>

<span data-ttu-id="68572-122">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가** / **클래스** 새 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="68572-122">In Solution Explorer, right click the project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="68572-123">클래스 이름을 `Startup`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="68572-123">Name the class `Startup`.</span></span>

![](use-owin-to-self-host-web-api/_static/image5.png)

<span data-ttu-id="68572-124">다음으로이 파일에 있는 상용구 코드의 모든를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="68572-124">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample1.cs)]

## <a name="add-a-web-api-controller"></a><span data-ttu-id="68572-125">웹 API 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="68572-125">Add a Web API Controller</span></span>

<span data-ttu-id="68572-126">다음으로, 웹 API 컨트롤러 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="68572-126">Next, add a Web API controller class.</span></span> <span data-ttu-id="68572-127">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가** / **클래스** 새 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="68572-127">In Solution Explorer, right click the project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="68572-128">클래스 이름을 `ValuesController`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="68572-128">Name the class `ValuesController`.</span></span>

<span data-ttu-id="68572-129">다음으로이 파일에 있는 상용구 코드의 모든를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="68572-129">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample2.cs)]

## <a name="start-the-owin-host-and-make-a-request-using-httpclient"></a><span data-ttu-id="68572-130">OWIN 호스트를 시작 하 고 HttpClient를 사용 하 여 요청</span><span class="sxs-lookup"><span data-stu-id="68572-130">Start the OWIN Host and Make a Request Using HttpClient</span></span>

<span data-ttu-id="68572-131">다음으로 Program.cs 파일에 있는 상용구 코드의 모든를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="68572-131">Replace all of the boilerplate code in the Program.cs file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample3.cs)]

## <a name="running-the-application"></a><span data-ttu-id="68572-132">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="68572-132">Running the Application</span></span>

<span data-ttu-id="68572-133">응용 프로그램을 실행 하려면 Visual Studio에서 F5 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="68572-133">To run the application, press F5 in Visual Studio.</span></span> <span data-ttu-id="68572-134">출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="68572-134">The output should look like the following:</span></span>

[!code-console[Main](use-owin-to-self-host-web-api/samples/sample4.cmd)]

![](use-owin-to-self-host-web-api/_static/image6.png)

## <a name="additional-resources"></a><span data-ttu-id="68572-135">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="68572-135">Additional Resources</span></span>

[<span data-ttu-id="68572-136">프로젝트 Katana의 개요</span><span class="sxs-lookup"><span data-stu-id="68572-136">An Overview of Project Katana</span></span>](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)

[<span data-ttu-id="68572-137">Azure 작업자 역할에 ASP.NET Web API를 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="68572-137">Host ASP.NET Web API in an Azure Worker Role</span></span>](host-aspnet-web-api-in-an-azure-worker-role.md)
