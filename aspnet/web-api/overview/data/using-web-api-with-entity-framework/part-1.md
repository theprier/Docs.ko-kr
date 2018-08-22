---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-1
title: Entity Framework 6 사용 하 여 Web API 2 사용 하 여 | Microsoft Docs
author: MikeWasson
description: 이 자습서는 ASP.NET Web API를 사용 하 여 웹 응용 프로그램 만들기의 기본 사항을 백 엔드 배우게를 보여 줍니다. 이 자습서에서는 데이터 레이아웃에 대 한 Entity Framework 6을 사용 하는 중...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: e879487e-dbcd-4b33-b092-d67c37ae768c
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-1
msc.type: authoredcontent
ms.openlocfilehash: 4abe0e06dfd927765efd8e566584e111cf4117d5
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41827756"
---
<a name="using-web-api-2-with-entity-framework-6"></a><span data-ttu-id="06a89-104">Entity Framework 6 사용 하 여 Web API 2 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="06a89-104">Using Web API 2 with Entity Framework 6</span></span>
====================
<span data-ttu-id="06a89-105">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="06a89-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="06a89-106">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="06a89-106">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

> <span data-ttu-id="06a89-107">이 자습서는 ASP.NET Web API를 사용 하 여 웹 응용 프로그램 만들기의 기본 사항을 백 엔드 배우게를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="06a89-107">This tutorial will teach you the basics of creating a web application with an ASP.NET Web API back end.</span></span> <span data-ttu-id="06a89-108">자습서를 사용 하면 데이터 계층 Knockout.js 위해 Entity Framework 6을 사용 하는 클라이언트 쪽 JavaScript 응용 프로그램에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="06a89-108">The tutorial uses Entity Framework 6 for the data layer, and Knockout.js for the client-side JavaScript application.</span></span> <span data-ttu-id="06a89-109">또한 자습서에는 Azure App Service Web Apps에 앱을 배포 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="06a89-109">The tutorial also shows how to deploy the app to Azure App Service Web Apps.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="06a89-110">이 자습서에 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="06a89-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="06a89-111">Web API 2.1</span><span class="sxs-lookup"><span data-stu-id="06a89-111">Web API 2.1</span></span>
> - [<span data-ttu-id="06a89-112">Visual Studio 2013 업데이트 2</span><span class="sxs-lookup"><span data-stu-id="06a89-112">Visual Studio 2013 Update 2</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs)
> - <span data-ttu-id="06a89-113">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="06a89-113">Entity Framework 6</span></span>
> - <span data-ttu-id="06a89-114">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="06a89-114">.NET 4.5</span></span>
> - <span data-ttu-id="06a89-115">[Knockout.js](http://knockoutjs.com/) 3.1</span><span class="sxs-lookup"><span data-stu-id="06a89-115">[Knockout.js](http://knockoutjs.com/) 3.1</span></span>


<span data-ttu-id="06a89-116">이 자습서에서는 백 엔드 데이터베이스를 조작 하는 웹 응용 프로그램을 만드는 Entity Framework 6을 사용 하 여 ASP.NET Web API 2를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="06a89-116">This tutorial uses ASP.NET Web API 2 with Entity Framework 6 to create a web application that manipulates a back-end database.</span></span> <span data-ttu-id="06a89-117">만들려는 응용 프로그램의 스크린샷은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="06a89-117">Here is a screen shot of the application that you will create.</span></span>

[![](part-1/_static/image2.png)](part-1/_static/image1.png)

<span data-ttu-id="06a89-118">앱에는 단일 페이지 응용 프로그램 (SPA) 디자인을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="06a89-118">The app uses a single-page application (SPA) design.</span></span> <span data-ttu-id="06a89-119">"단일 페이지 응용 프로그램"은 하나의 HTML 페이지를 로드 하 고 그런 다음 새 페이지를 로드 하는 대신 페이지를 동적으로 업데이트 하는 웹 응용 프로그램에 대 한 일반 용어입니다.</span><span class="sxs-lookup"><span data-stu-id="06a89-119">"Single-page application" is the general term for a web application that loads a single HTML page and then updates the page dynamically, instead of loading new pages.</span></span> <span data-ttu-id="06a89-120">초기 페이지 로드 후 앱은 AJAX 요청을 통해 서버를 사용 하 여 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="06a89-120">After the initial page load, the app talks with the server through AJAX requests.</span></span> <span data-ttu-id="06a89-121">AJAX 요청 앱 UI 업데이트를 사용 하 여 JSON 데이터를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="06a89-121">The AJAX requests return JSON data, which the app uses to update the UI.</span></span>

<span data-ttu-id="06a89-122">AJAX 새 없지만 오늘 가지 쉽게 구축 하 고 대형 정교한 SPA 응용 프로그램을 관리 하는 JavaScript 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="06a89-122">AJAX isn't new, but today there are JavaScript frameworks that make it easier to build and maintain a large sophisticated SPA application.</span></span> <span data-ttu-id="06a89-123">이 자습서에서는 [Knockout.js](http://knockoutjs.com/), 하지만 JavaScript 클라이언트 프레임 워크를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06a89-123">This tutorial uses [Knockout.js](http://knockoutjs.com/), but you can use any JavaScript client framework.</span></span>

<span data-ttu-id="06a89-124">이 앱에 대 한 기본 구성 요소는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="06a89-124">Here are the main building blocks for this app:</span></span>

- <span data-ttu-id="06a89-125">ASP.NET MVC는 HTML 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="06a89-125">ASP.NET MVC creates the HTML page.</span></span>
- <span data-ttu-id="06a89-126">ASP.NET Web API는 AJAX 요청을 처리 하 고 JSON 데이터를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="06a89-126">ASP.NET Web API handles the AJAX requests and returns JSON data.</span></span>
- <span data-ttu-id="06a89-127">Knockout.js 데이터 바인딩 HTML 요소를 JSON 데이터로 합니다.</span><span class="sxs-lookup"><span data-stu-id="06a89-127">Knockout.js data-binds the HTML elements to the JSON data.</span></span>
- <span data-ttu-id="06a89-128">Entity Framework는 데이터베이스에 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="06a89-128">Entity Framework talks to the database.</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="06a89-129">Azure에서 실행 되는이 앱 참조</span><span class="sxs-lookup"><span data-stu-id="06a89-129">See this App Running on Azure</span></span>

<span data-ttu-id="06a89-130">라이브 웹 앱으로 실행 하는 완성 된 사이트를 참조 하 시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="06a89-130">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="06a89-131">다음 단추를 클릭 하 여 Azure 계정에 앱의 전체 버전을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06a89-131">You can deploy a complete version of the app to your Azure account by simply clicking the following button.</span></span>

[![](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/BookService)

<span data-ttu-id="06a89-132">이 솔루션을 Azure에 배포 하려면 Azure 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="06a89-132">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="06a89-133">계정이 아직 없는 경우 다음 옵션:</span><span class="sxs-lookup"><span data-stu-id="06a89-133">If you do not already have an account, you have the following options:</span></span>

- <span data-ttu-id="06a89-134">[Azure 계정을 무료로 개설](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) -크레딧을 받게 사용 하면 유료 Azure 서비스를 사용해볼 수 있습니다 하 고 사용한 후에 계정을 유지 하면 최대 사용 하 여 무료 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="06a89-134">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="06a89-135">[MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) -MSDN 구독은 크레딧을 매달 제공 유료 Azure 서비스에 사용할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="06a89-135">[Activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="06a89-136">프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="06a89-136">Create the Project</span></span>

<span data-ttu-id="06a89-137">Visual Studio를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="06a89-137">Open Visual Studio.</span></span> <span data-ttu-id="06a89-138">**파일** 메뉴에서 **새로 만들기**을 선택한 후 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="06a89-138">From the **File** menu, select **New**, then select **Project**.</span></span> <span data-ttu-id="06a89-139">(키를 누르거나 **새 프로젝트** 시작 페이지에서.)</span><span class="sxs-lookup"><span data-stu-id="06a89-139">(Or click **New Project** on the Start page.)</span></span>

<span data-ttu-id="06a89-140">에 **새 프로젝트** 대화 상자에서 클릭 **웹** 왼쪽된 창에서와 **ASP.NET 웹 응용 프로그램** 가운데 창에서.</span><span class="sxs-lookup"><span data-stu-id="06a89-140">In the **New Project** dialog, click **Web** in the left pane and **ASP.NET Web Application** in the middle pane.</span></span> <span data-ttu-id="06a89-141">BookService 프로젝트 이름을 지정 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="06a89-141">Name the project BookService and click **OK**.</span></span>

[![](part-1/_static/image4.png)](part-1/_static/image3.png)

<span data-ttu-id="06a89-142">에 **새 ASP.NET 프로젝트** 대화 상자에서 선택 합니다 **Web API** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="06a89-142">In the **New ASP.NET Project** dialog, select the **Web API** template.</span></span>

[![](part-1/_static/image6.png)](part-1/_static/image5.png)

<span data-ttu-id="06a89-143">Azure App Service에서 프로젝트를 호스트 하려는 경우는 **클라우드에서 호스트** 확인란이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06a89-143">If you want to host the project in a Azure App Service, leave the **Host in the cloud** box checked.</span></span>

<span data-ttu-id="06a89-144">**확인**을 클릭해 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="06a89-144">Click **OK** to create the project.</span></span>

## <a name="configure-azure-settings-optional"></a><span data-ttu-id="06a89-145">(선택 사항) Azure 설정 구성</span><span class="sxs-lookup"><span data-stu-id="06a89-145">Configure Azure Settings (Optional)</span></span>

<span data-ttu-id="06a89-146">생략 하면 합니다 **클라우드에서 호스트** 옵션 선택 하면 Visual Studio를 Microsoft Azure에 로그인 하 라는 메시지가 나타납니다</span><span class="sxs-lookup"><span data-stu-id="06a89-146">If you left the **Host in Cloud** option checked, Visual Studio will prompt you to sign in to Microsoft Azure</span></span>

[![](part-1/_static/image8.png)](part-1/_static/image7.png)

<span data-ttu-id="06a89-147">Azure에 로그인 한 후 Visual Studio 웹 앱을 구성 하 라는 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="06a89-147">After you sign in to Azure, Visual Studio prompts you to configure the web app.</span></span> <span data-ttu-id="06a89-148">사이트에 대 한 이름을 입력 하 고 Azure 구독에 선택한 지리적 지역을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="06a89-148">Enter a name for the site, select your Azure subscription, and select a geographical region.</span></span> <span data-ttu-id="06a89-149">아래 **데이터베이스 서버**를 선택 **새 서버 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="06a89-149">Under **Database server**, select **Create new server**.</span></span> <span data-ttu-id="06a89-150">관리자 사용자 이름 및 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="06a89-150">Enter an administrator username and password.</span></span>

[![](part-1/_static/image10.png)](part-1/_static/image9.png)

> [!div class="step-by-step"]
> [<span data-ttu-id="06a89-151">다음</span><span class="sxs-lookup"><span data-stu-id="06a89-151">Next</span></span>](part-2.md)
