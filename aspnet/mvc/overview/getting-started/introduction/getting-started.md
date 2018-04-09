---
uid: mvc/overview/getting-started/introduction/getting-started
title: ASP.NET MVC 5 시작 | Microsoft Docs
author: Rick-Anderson
description: 참고:이 자습서의 업데이트 된 버전은 Visual Studio 2015를 사용 하 여 사용할 수입니다. 새 자습서에서는 ASP.NET Core MVC 6 많은 improvem 제공 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/28/2015
ms.topic: article
ms.assetid: f3d8adbe-55e7-4fd4-84a8-7155bc45c676
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/introduction/getting-started
msc.type: authoredcontent
ms.openlocfilehash: 0f1fd2026691d3bc0e81b20a9731879d7a6041bb
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="getting-started-with-aspnet-mvc-5"></a><span data-ttu-id="76944-104">ASP.NET MVC 5 시작</span><span class="sxs-lookup"><span data-stu-id="76944-104">Getting Started with ASP.NET MVC 5</span></span>
====================
<span data-ttu-id="76944-105">으로 [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="76944-105">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

[!INCLUDE [consider RP](../../../../includes/razor.md)]

 <span data-ttu-id="76944-106">이 자습서는 ASP.NET MVC 5 웹 응용 프로그램 사용 하 여 프로그램을 구축 하는 기초 업무량이 [Visual Studio 2017](https://www.visualstudio.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="76944-106">This tutorial will teach you the basics of building an ASP.NET MVC 5 web app using [Visual Studio 2017](https://www.visualstudio.com/).</span></span> <span data-ttu-id="76944-107">자습서에 대 한 최종 소스에 있는 [GitHub](https://github.com/aspnet/Docs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie/MvcMovie)</span><span class="sxs-lookup"><span data-stu-id="76944-107">Final Source for tutorial located on [GitHub](https://github.com/aspnet/Docs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie/MvcMovie)</span></span>


 <span data-ttu-id="76944-108">이 자습서에 의해 작성 되었으므로 [Scott Guthrie](https://weblogs.asp.net/scottgu/) (twitter[ @scottgu ](https://twitter.com/scottgu) ), [Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [ @shanselman ](https://twitter.com/shanselman) ) 및 [Rick Anderson](https://twitter.com/RickAndMSFT) ( [ @RickAndMSFT ](https://twitter.com/#!/RickAndMSFT) )</span><span class="sxs-lookup"><span data-stu-id="76944-108">This tutorial was written by [Scott Guthrie](https://weblogs.asp.net/scottgu/) (twitter[@scottgu](https://twitter.com/scottgu) ), [Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [@shanselman](https://twitter.com/shanselman) ), and [Rick Anderson](https://twitter.com/RickAndMSFT) ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) )</span></span>

 <span data-ttu-id="76944-109">이 응용 프로그램을 Azure에 배포 하려면 Azure 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="76944-109">You need an Azure account to deploy this app to Azure:</span></span>

 - <span data-ttu-id="76944-110">있습니다 수 [무료로 Azure 계정을 개설](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) -크레딧을 얻게 유료 Azure 서비스를 실행 해 사용할 수 있으며, 사용 후에 최대 계정 등에 사용 가능한 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="76944-110">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
 - <span data-ttu-id="76944-111">있습니다 수 [MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) -Your MSDN을 구독 하면 크레딧 매달 유료 Azure 서비스에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76944-111">You can [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>


## <a name="getting-started"></a><span data-ttu-id="76944-112">시작</span><span class="sxs-lookup"><span data-stu-id="76944-112">Getting Started</span></span>

<span data-ttu-id="76944-113">설치 하 고 실행 하 여 시작 [Visual Studio 2017](https://www.visualstudio.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="76944-113">Start by installing and running [Visual Studio 2017](https://www.visualstudio.com/).</span></span>

<span data-ttu-id="76944-114">Visual Studio IDE, 또는 통합된 개발 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="76944-114">Visual Studio is an IDE, or integrated development environment.</span></span> <span data-ttu-id="76944-115">Microsoft Word를 사용 하 여 문서를 작성 하는 것 처럼 응용 프로그램을 만드는 있는 IDE를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="76944-115">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="76944-116">Visual Studio에는 사용할 수 있는 다양 한 옵션을 보여 주는 아래 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="76944-116">In Visual Studio there's a list along the bottom showing various options available to you.</span></span> <span data-ttu-id="76944-117">IDE에서 작업을 수행 하는 다른 방법은 제공 하는 메뉴가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76944-117">There's also a menu that provides another way to perform tasks in the IDE.</span></span> <span data-ttu-id="76944-118">(선택 하는 대신 예를 들어 **새 프로젝트** 에서 **시작** 페이지 메뉴를 사용 하 고 선택할 수 **파일** &gt; **새프로젝트**.)</span><span class="sxs-lookup"><span data-stu-id="76944-118">(For example, instead of selecting **New Project** from the **Start** page, you can use the menu and select **File** &gt; **New Project**.)</span></span>


![](getting-started/_static/image1.png)  


## <a name="creating-your-first-application"></a><span data-ttu-id="76944-119">응용 프로그램 처음 만들기</span><span class="sxs-lookup"><span data-stu-id="76944-119">Creating Your First Application</span></span>

<span data-ttu-id="76944-120">클릭 **새 프로젝트**을 다음 선택 Visual C#의 왼쪽에서 다음 **웹** 선택한 후 **ASP.NET 웹 응용 프로그램 (.NET Framework)**합니다.</span><span class="sxs-lookup"><span data-stu-id="76944-120">Click **New Project**, then select Visual C# on the left, then **Web** and then select **ASP.NET Web Application (.NET Framework)**.</span></span> <span data-ttu-id="76944-121">"MvcMovie" 프로젝트 이름을 지정 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="76944-121">Name your project "MvcMovie" and then click **OK**.</span></span>

![](getting-started/_static/image2.png)

<span data-ttu-id="76944-122">에 **새 ASP.NET 프로젝트** 대화 상자에서 클릭 **MVC** 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="76944-122">In the **New ASP.NET Project** dialog, click **MVC** and then click **OK**.</span></span>

![](getting-started/_static/image3.png)

<span data-ttu-id="76944-123">Visual Studio 방금 만든 ASP.NET MVC 프로젝트에 대 한 기본 서식 파일을 사용 해야 하므로 응용 프로그램 현재 아무것도 수행 하지 않고!</span><span class="sxs-lookup"><span data-stu-id="76944-123">Visual Studio used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="76944-124">간단한 "Hello World!"입니다.</span><span class="sxs-lookup"><span data-stu-id="76944-124">This is a simple "Hello World!"</span></span> <span data-ttu-id="76944-125">프로젝트의 응용 프로그램을 시작 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="76944-125">project, and it's a good place to start your application.</span></span>

![](getting-started/_static/image4.png)

<span data-ttu-id="76944-126">디버깅을 시작 하려면 f5 키를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="76944-126">Click F5 to start debugging.</span></span> <span data-ttu-id="76944-127">F 5를 눌러 Visual Studio를 시작 하면 [IIS Express](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview) 웹 앱을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="76944-127">F5 causes Visual Studio to start [IIS Express](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview) and run your web app.</span></span> <span data-ttu-id="76944-128">그런 다음 visual Studio는 브라우저를 시작 하 고 응용 프로그램의 홈 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="76944-128">Visual Studio then launches a browser and opens the application's home page.</span></span> <span data-ttu-id="76944-129">브라우저의 주소 표시줄을 `localhost:port#` 와 하지 것 같은 `example.com`합니다.</span><span class="sxs-lookup"><span data-stu-id="76944-129">Notice that the address bar of the browser says `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="76944-130">때문 `localhost` 항상 방금 빌드한 응용 프로그램을 실행 중인이 예제의 자신의 로컬 컴퓨터를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="76944-130">That's because `localhost` always points to your own local computer, which in this case is running the application you just built.</span></span> <span data-ttu-id="76944-131">Visual Studio 웹 프로젝트를 실행 하면 임의의 포트는 웹 서버에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76944-131">When Visual Studio runs a web project, a random port is used for the web server.</span></span> <span data-ttu-id="76944-132">아래 이미지에 포트 번호가 1234입니다.</span><span class="sxs-lookup"><span data-stu-id="76944-132">In the image below, the port number is 1234.</span></span> <span data-ttu-id="76944-133">응용 프로그램을 실행 하는 경우에 다른 포트 번호를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76944-133">When you run the application, you'll see a different port number.</span></span>

![](getting-started/_static/image5.png)

<span data-ttu-id="76944-134">즉시이 기본 템플릿을 사용 하면 집, 연락처 및 정보 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="76944-134">Right out of the box this default template gives you Home, Contact and About pages.</span></span> <span data-ttu-id="76944-135">위의 그림은 표시 되지 않습니다는 **홈**, **에 대 한** 및 **연락처** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="76944-135">The image above doesn't show the **Home**, **About** and **Contact** links.</span></span> <span data-ttu-id="76944-136">브라우저 창의 크기에 따라 이러한 링크를 보려면 탐색 아이콘을 클릭 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76944-136">Depending on the size of your browser window, you might need to click the navigation icon to see these links.</span></span>

![](getting-started/_static/image6.png)  

<span data-ttu-id="76944-137">또한 응용 프로그램에서는 등록 및 로그인를 합니다.</span><span class="sxs-lookup"><span data-stu-id="76944-137">The application also provides support to register and log in.</span></span> <span data-ttu-id="76944-138">이 응용 프로그램 작동 방식을 변경 하 고 ASP.NET MVC에 대해 약간 자세한 하는 다음 단계가입니다.</span><span class="sxs-lookup"><span data-stu-id="76944-138">The next step is to change how this application works and learn a little bit about ASP.NET MVC.</span></span> <span data-ttu-id="76944-139">ASP.NET MVC 응용 프로그램을 닫고 일부 코드를 변경 해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="76944-139">Close the ASP.NET MVC application and let's change some code.</span></span>

<span data-ttu-id="76944-140">목록이 현재 자습서에 대 한 참조 [권장 하는 문서 MVC](../mvc-learning-sequence.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="76944-140">For a list of current tutorials, see [MVC recommended articles](../mvc-learning-sequence.md).</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="76944-141">Azure에서 실행 되는이 응용 프로그램 참조</span><span class="sxs-lookup"><span data-stu-id="76944-141">See this App Running on Azure</span></span>

<span data-ttu-id="76944-142">실시간 웹 앱으로 실행 하는 완료 된 사이트를 참조 하 시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="76944-142">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="76944-143">다음 단추 클릭 하 여 Azure 계정에 완전 한 버전의 앱을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76944-143">You can deploy a complete version of the app to your Azure account by simply clicking the following button.</span></span>

[![](https://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?repository=https://github.com/aspnet/Docs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie&amp;WT.mc_id=deploy_azure_aspnet)

<span data-ttu-id="76944-144">Azure에이 솔루션을 배포 하려면 Azure 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="76944-144">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="76944-145">계정이 아직 없는 경우 다음 옵션:</span><span class="sxs-lookup"><span data-stu-id="76944-145">If you do not already have an account, you have the following options:</span></span>

- <span data-ttu-id="76944-146">[무료 Azure 계정을 개설](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) -크레딧을 얻게 유료 Azure 서비스를 실행 해 사용할 수 있으며, 사용 후에 최대 계정 등에 사용 가능한 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="76944-146">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="76944-147">[MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) -Your MSDN을 구독 하면 크레딧 매달 유료 Azure 서비스에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76944-147">[Activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="76944-148">다음</span><span class="sxs-lookup"><span data-stu-id="76944-148">Next</span></span>](adding-a-controller.md)
