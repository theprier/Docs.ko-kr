---
uid: mvc/overview/getting-started/introduction/getting-started
title: ASP.NET MVC 5 시작 | Microsoft Docs
author: Rick-Anderson
description: 참고:이 자습서의 업데이트 된 버전 여기 Visual Studio 2015를 통해 제공 됩니다. 새 자습서에서는 많은 improvem를 제공 하는 ASP.NET Core MVC 6을 사용 하는 중...
ms.author: aspnetcontent
ms.date: 05/28/2015
ms.assetid: f3d8adbe-55e7-4fd4-84a8-7155bc45c676
msc.legacyurl: /mvc/overview/getting-started/introduction/getting-started
msc.type: authoredcontent
ms.openlocfilehash: 85d5d3292ff99ade6995c710e2728c41255def4c
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37823218"
---
<a name="getting-started-with-aspnet-mvc-5"></a><span data-ttu-id="a5a4f-104">ASP.NET MVC 5 시작</span><span class="sxs-lookup"><span data-stu-id="a5a4f-104">Getting Started with ASP.NET MVC 5</span></span>
====================
<span data-ttu-id="a5a4f-105">[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="a5a4f-105">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

[!INCLUDE [consider RP](../../../../includes/razor.md)]

 <span data-ttu-id="a5a4f-106">이 자습서는 ASP.NET MVC 5 웹 앱 사용 하 여 프로그램을 빌드하는 기본 사항 설명 [Visual Studio 2017](https://www.visualstudio.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a4f-106">This tutorial will teach you the basics of building an ASP.NET MVC 5 web app using [Visual Studio 2017](https://www.visualstudio.com/).</span></span> <span data-ttu-id="a5a4f-107">자습서 마지막 소스에 있는 [GitHub](https://github.com/aspnet/Docs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie/MvcMovie)</span><span class="sxs-lookup"><span data-stu-id="a5a4f-107">Final Source for tutorial located on [GitHub](https://github.com/aspnet/Docs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie/MvcMovie)</span></span>


 <span data-ttu-id="a5a4f-108">이 자습서를 통해 작성 했습니다 [Scott Guthrie](https://weblogs.asp.net/scottgu/) (twitter[ @scottgu ](https://twitter.com/scottgu) ), [Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [ @shanselman ](https://twitter.com/shanselman) ) 및 [Rick Anderson](https://twitter.com/RickAndMSFT) ( [ @RickAndMSFT ](https://twitter.com/#!/RickAndMSFT) )</span><span class="sxs-lookup"><span data-stu-id="a5a4f-108">This tutorial was written by [Scott Guthrie](https://weblogs.asp.net/scottgu/) (twitter[@scottgu](https://twitter.com/scottgu) ), [Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [@shanselman](https://twitter.com/shanselman) ), and [Rick Anderson](https://twitter.com/RickAndMSFT) ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) )</span></span>

 <span data-ttu-id="a5a4f-109">이 앱을 Azure에 배포 하려면 Azure 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a4f-109">You need an Azure account to deploy this app to Azure:</span></span>

 - <span data-ttu-id="a5a4f-110">할 수 있습니다 [Azure 계정을 무료로 개설](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) -크레딧을 받게 사용 하면 유료 Azure 서비스를 사용해볼 수 있습니다 하 고 사용한 후에 계정을 유지 하면 최대 사용 하 여 무료 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="a5a4f-110">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
 - <span data-ttu-id="a5a4f-111">할 수 있습니다 [MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) -MSDN 구독은 크레딧을 매달 제공 유료 Azure 서비스에 사용할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a4f-111">You can [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>


## <a name="getting-started"></a><span data-ttu-id="a5a4f-112">시작</span><span class="sxs-lookup"><span data-stu-id="a5a4f-112">Getting Started</span></span>

<span data-ttu-id="a5a4f-113">설치 및 실행 하 여 시작 [Visual Studio 2017](https://www.visualstudio.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a4f-113">Start by installing and running [Visual Studio 2017](https://www.visualstudio.com/).</span></span>

<span data-ttu-id="a5a4f-114">Visual Studio IDE 또는 통합된 개발 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="a5a4f-114">Visual Studio is an IDE, or integrated development environment.</span></span> <span data-ttu-id="a5a4f-115">Microsoft Word를 사용 하 여 문서를 작성 하는 것 처럼 응용 프로그램을 만드는 IDE를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a4f-115">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="a5a4f-116">Visual Studio에서 사용할 수 있는 다양 한 옵션을 보여 주는 아래쪽 목록이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5a4f-116">In Visual Studio there's a list along the bottom showing various options available to you.</span></span> <span data-ttu-id="a5a4f-117">IDE에서 작업을 수행 하는 또 다른 방법은 제공 하는 메뉴가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5a4f-117">There's also a menu that provides another way to perform tasks in the IDE.</span></span> <span data-ttu-id="a5a4f-118">(예를 들어, 선택 하는 대신 **새 프로젝트** 에서 합니다 **시작** 페이지에서 메뉴를 사용 하 고 선택할 수 **파일** &gt; **새프로젝트**.)</span><span class="sxs-lookup"><span data-stu-id="a5a4f-118">(For example, instead of selecting **New Project** from the **Start** page, you can use the menu and select **File** &gt; **New Project**.)</span></span>


![](getting-started/_static/image1.png)  


## <a name="creating-your-first-application"></a><span data-ttu-id="a5a4f-119">응용 프로그램 처음 만들기</span><span class="sxs-lookup"><span data-stu-id="a5a4f-119">Creating Your First Application</span></span>

<span data-ttu-id="a5a4f-120">클릭 **새 프로젝트**, 선택한 Visual C# 왼쪽에서 다음 **Web** 선택한 후 **ASP.NET 웹 응용 프로그램 (.NET Framework)** 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a4f-120">Click **New Project**, then select Visual C# on the left, then **Web** and then select **ASP.NET Web Application (.NET Framework)**.</span></span> <span data-ttu-id="a5a4f-121">"MvcMovie" 프로젝트 이름을 지정 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a4f-121">Name your project "MvcMovie" and then click **OK**.</span></span>

![](getting-started/_static/image2.png)

<span data-ttu-id="a5a4f-122">에 **새 ASP.NET 프로젝트** 대화 상자에서 클릭 **MVC** 을 클릭 한 다음 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a4f-122">In the **New ASP.NET Project** dialog, click **MVC** and then click **OK**.</span></span>

![](getting-started/_static/image3.png)

<span data-ttu-id="a5a4f-123">있다면 응용 프로그램을 사용 지금은 아무 작업도 수행 하지 않고 방금 만든 ASP.NET MVC 프로젝트에 대 한 기본 템플릿을 사용 하는 visual Studio!</span><span class="sxs-lookup"><span data-stu-id="a5a4f-123">Visual Studio used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="a5a4f-124">이는 간단한 "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="a5a4f-124">This is a simple "Hello World!"</span></span> <span data-ttu-id="a5a4f-125">프로젝트의 응용 프로그램을 시작 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a5a4f-125">project, and it's a good place to start your application.</span></span>

![](getting-started/_static/image4.png)

<span data-ttu-id="a5a4f-126">디버깅을 시작 하려면 f5 키를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a4f-126">Click F5 to start debugging.</span></span> <span data-ttu-id="a5a4f-127">F5 경우 시작 하려면 Visual Studio [IIS Express](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview) 및 웹 앱을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a4f-127">F5 causes Visual Studio to start [IIS Express](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview) and run your web app.</span></span> <span data-ttu-id="a5a4f-128">그런 다음 visual Studio가 브라우저를 시작 하 고 응용 프로그램의 홈 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a5a4f-128">Visual Studio then launches a browser and opens the application's home page.</span></span> <span data-ttu-id="a5a4f-129">브라우저의 주소 표시줄에 다음과 같은 알림이 `localhost:port#` 등은 표시 되지 않습니다 및 `example.com`합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a4f-129">Notice that the address bar of the browser says `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="a5a4f-130">있기 때문입니다 `localhost` 는 방금 빌드한 응용 프로그램을 실행 하는 경우에 자신의 로컬 컴퓨터는 항상 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="a5a4f-130">That's because `localhost` always points to your own local computer, which in this case is running the application you just built.</span></span> <span data-ttu-id="a5a4f-131">Visual Studio 웹 프로젝트를 실행할 때 임의 포트를 웹 서버에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5a4f-131">When Visual Studio runs a web project, a random port is used for the web server.</span></span> <span data-ttu-id="a5a4f-132">아래 이미지에서 포트 번호가 1234입니다.</span><span class="sxs-lookup"><span data-stu-id="a5a4f-132">In the image below, the port number is 1234.</span></span> <span data-ttu-id="a5a4f-133">응용 프로그램을 실행 하는 경우 다른 포트 번호를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5a4f-133">When you run the application, you'll see a different port number.</span></span>

![](getting-started/_static/image5.png)

<span data-ttu-id="a5a4f-134">즉시이 기본 템플릿을 사용 하면 집, 연락처 및에 대 한 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="a5a4f-134">Right out of the box this default template gives you Home, Contact and About pages.</span></span> <span data-ttu-id="a5a4f-135">위의 이미지에 표시 되지 않습니다 합니다 **홈**, **에 대 한** 하 고 **연락처** 링크.</span><span class="sxs-lookup"><span data-stu-id="a5a4f-135">The image above doesn't show the **Home**, **About** and **Contact** links.</span></span> <span data-ttu-id="a5a4f-136">브라우저 창의 크기에 따라 다음이 링크를 보려면 탐색 아이콘을 클릭 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a4f-136">Depending on the size of your browser window, you might need to click the navigation icon to see these links.</span></span>

![](getting-started/_static/image6.png)  

<span data-ttu-id="a5a4f-137">응용 프로그램 등록 및 로그인 하는 지원도 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a4f-137">The application also provides support to register and log in.</span></span> <span data-ttu-id="a5a4f-138">다음 단계는이 응용 프로그램의 작동 방식을 변경할 좀 더 자세히 알아보고 ASP.NET MVC 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a5a4f-138">The next step is to change how this application works and learn a little bit about ASP.NET MVC.</span></span> <span data-ttu-id="a5a4f-139">ASP.NET MVC 응용 프로그램을 닫고 일부 코드를 변경해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a5a4f-139">Close the ASP.NET MVC application and let's change some code.</span></span>

<span data-ttu-id="a5a4f-140">현재 자습서 목록은 참조 하세요 [문서를 권장 하는 MVC](../mvc-learning-sequence.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a4f-140">For a list of current tutorials, see [MVC recommended articles](../mvc-learning-sequence.md).</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="a5a4f-141">Azure에서 실행 되는이 앱 참조</span><span class="sxs-lookup"><span data-stu-id="a5a4f-141">See this App Running on Azure</span></span>

<span data-ttu-id="a5a4f-142">라이브 웹 앱으로 실행 하는 완성 된 사이트를 참조 하 시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="a5a4f-142">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="a5a4f-143">다음 단추를 클릭 하 여 Azure 계정에 앱의 전체 버전을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5a4f-143">You can deploy a complete version of the app to your Azure account by simply clicking the following button.</span></span>

[![](https://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?repository=https://github.com/aspnet/Docs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie&amp;WT.mc_id=deploy_azure_aspnet)

<span data-ttu-id="a5a4f-144">이 솔루션을 Azure에 배포 하려면 Azure 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a4f-144">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="a5a4f-145">계정이 아직 없는 경우 다음 옵션:</span><span class="sxs-lookup"><span data-stu-id="a5a4f-145">If you do not already have an account, you have the following options:</span></span>

- <span data-ttu-id="a5a4f-146">[Azure 계정을 무료로 개설](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) -크레딧을 받게 사용 하면 유료 Azure 서비스를 사용해볼 수 있습니다 하 고 사용한 후에 계정을 유지 하면 최대 사용 하 여 무료 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="a5a4f-146">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="a5a4f-147">[MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) -MSDN 구독은 크레딧을 매달 제공 유료 Azure 서비스에 사용할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a4f-147">[Activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="a5a4f-148">다음</span><span class="sxs-lookup"><span data-stu-id="a5a4f-148">Next</span></span>](adding-a-controller.md)
