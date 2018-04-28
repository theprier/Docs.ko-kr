---
title: ASP.NET Core 게시 SignalR 앱을 Azure 웹 앱에
author: rachelappel
description: ASP.NET Core 게시 SignalR 앱을 Azure 웹 앱에
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: rachelap
ms.custom: mvc
ms.date: 04/20/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: signalr/publish-to-azure-web-app
ms.openlocfilehash: fd7d38ad47d9004db2ae7b5858dc22609943f601
ms.sourcegitcommit: 2ab550f8c46e1a8a5d45e58be44d151c676af256
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2018
---
# <a name="publish-an-aspnet-core-signalr-app-to-an-azure-web-app"></a><span data-ttu-id="ed3b1-103">ASP.NET Core 게시 된 Azure 웹 앱에 SignalR 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="ed3b1-103">Publish an ASP.NET Core SignalR app to an Azure Web App</span></span>

<span data-ttu-id="ed3b1-104">[Azure 웹 앱](/azure/app-service/app-service-web-overview) 는 [Microsoft 클라우드 컴퓨팅](https://azure.microsoft.com/) ASP.NET Core를 포함 하 여 웹 응용 프로그램을 호스팅하기 위한 플랫폼 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="ed3b1-104">[Azure Web App](/azure/app-service/app-service-web-overview) is a [Microsoft cloud computing](https://azure.microsoft.com/) platform service for hosting web apps, including ASP.NET Core.</span></span>

## <a name="publish-the-app"></a><span data-ttu-id="ed3b1-105">앱 게시</span><span class="sxs-lookup"><span data-stu-id="ed3b1-105">Publish the app</span></span>

<span data-ttu-id="ed3b1-106">Visual Studio는 Azure 웹 앱에 게시에 대 한 기본 제공 도구를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3b1-106">Visual Studio provides built-in tools for publishing to an Azure Web App.</span></span> <span data-ttu-id="ed3b1-107">Visual Studio Code 사용자 צ ְ ײ [Azure CLI](/cli/azure) Azure에 앱을 게시 하기 위해 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="ed3b1-107">Visual Studio Code user can use [Azure CLI](/cli/azure) commands to publish apps to Azure.</span></span> <span data-ttu-id="ed3b1-108">이 문서에서는 Visual Studio에서 도구를 사용 하 여 게시에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3b1-108">This article covers publishing using the tools in Visual Studio.</span></span> <span data-ttu-id="ed3b1-109">Azure CLI를 사용 하 여 앱을 게시 하려면 참조 [명령줄 도구를 사용 하 여 Azure에 ASP.NET Core 응용 프로그램을 게시](xref:tutorials/publish-to-azure-webapp-using-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3b1-109">To publish an app using Azure CLI, see [Publish an ASP.NET Core app to Azure with command line tools](xref:tutorials/publish-to-azure-webapp-using-cli).</span></span>

<span data-ttu-id="ed3b1-110">프로젝트를 마우스 오른쪽 단추로 클릭 **솔루션 탐색기** 선택 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3b1-110">Right-click on the project in **Solution Explorer** and select **Publish**.</span></span> <span data-ttu-id="ed3b1-111">확인 **새로 만들기** 체크 인은 **게시 대상 선택** 대화 상자를 닫고 선택 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3b1-111">Confirm that **Create new** is checked in the **Pick a publish target** dialog, and select **Publish**.</span></span>

![선택 대상 게시](publish-to-azure-web-app/_static/pick-publish-target-dialog.png)

<span data-ttu-id="ed3b1-113">다음 정보를 입력의 **응용 프로그램 서비스 만들기** 대화 상자와 선택 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3b1-113">Enter the following information in the **Create App Service** dialog and select **Create**.</span></span>

| <span data-ttu-id="ed3b1-114">항목</span><span class="sxs-lookup"><span data-stu-id="ed3b1-114">Item</span></span> | <span data-ttu-id="ed3b1-115">설명</span><span class="sxs-lookup"><span data-stu-id="ed3b1-115">Description</span></span> |
| ---- | ----------- |
| <span data-ttu-id="ed3b1-116">**응용 프로그램 이름**</span><span class="sxs-lookup"><span data-stu-id="ed3b1-116">**App name**</span></span> | <span data-ttu-id="ed3b1-117">응용 프로그램의 고유 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ed3b1-117">A unique name of the app.</span></span> |
| <span data-ttu-id="ed3b1-118">**구독**</span><span class="sxs-lookup"><span data-stu-id="ed3b1-118">**Subscription**</span></span> | <span data-ttu-id="ed3b1-119">응용 프로그램을 사용 하는 Azure 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="ed3b1-119">The Azure subscription that the app uses.</span></span> |
| <span data-ttu-id="ed3b1-120">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="ed3b1-120">**Resource Group**</span></span> | <span data-ttu-id="ed3b1-121">응용 프로그램 속해 있는 관련된 리소스의 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="ed3b1-121">The group of related resources to which the app belongs.</span></span>  |
| <span data-ttu-id="ed3b1-122">**호스팅 계획**</span><span class="sxs-lookup"><span data-stu-id="ed3b1-122">**Hosting Plan**</span></span> | <span data-ttu-id="ed3b1-123">웹 앱에 대 한 가격 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3b1-123">The pricing plan for the web app.</span></span> |

![앱 서비스 만들기](publish-to-azure-web-app/_static/create-app-service-dialog.png)

<span data-ttu-id="ed3b1-125">Visual Studio에서는 다음과 같은 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3b1-125">Visual Studio completes the following tasks:</span></span>

* <span data-ttu-id="ed3b1-126">게시 프로필을 만듭니다 포함 된 게시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3b1-126">Creates a Publish Profile containing publish settings.</span></span>
* <span data-ttu-id="ed3b1-127">만들거나 기존의 사용 *Azure 웹 앱* 제공 된 세부 정보를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3b1-127">Creates or uses an existing *Azure Web App* with the provided details.</span></span>
* <span data-ttu-id="ed3b1-128">응용 프로그램을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3b1-128">Publishes the app.</span></span>
* <span data-ttu-id="ed3b1-129">로드 된 게시 된 웹 앱과 함께 브라우저를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3b1-129">Launches a browser, with the published web app loaded.</span></span>

<span data-ttu-id="ed3b1-130">응용 프로그램에 대 한 URL의 형식이 확인 *{응용 프로그램 이름}.azurewebsites.net*합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3b1-130">Notice the format of the URL for the app is *{app name}.azurewebsites.net*.</span></span> <span data-ttu-id="ed3b1-131">예를 들어 앱 `SignalRChattR` 에 다음과 같은 URL `https://signalrchattr.azurewebsites.net`합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3b1-131">For example, an app named `SignalRChattR` has a URL that looks like `https://signalrchattr.azurewebsites.net`.</span></span>

<span data-ttu-id="ed3b1-132">HTTP 502.2 오류가 발생 하는 경우 참조 [Azure 앱 서비스에 ASP.NET Core 배포 미리 보기 릴리스의](xref:host-and-deploy/azure-apps/index) 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3b1-132">If an HTTP 502.2 error occurs, see [Deploy ASP.NET Core preview release to Azure App Service](xref:host-and-deploy/azure-apps/index) to resolve it.</span></span>

## <a name="configure-signalr-web-app"></a><span data-ttu-id="ed3b1-133">SignalR 웹 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="ed3b1-133">Configure SignalR web app</span></span>

<span data-ttu-id="ed3b1-134">Azure 웹 앱으로 게시 하는 ASP.NET SignalR Core 앱 [ARR 선호도](https://en.wikipedia.org/wiki/Application_Request_Routing) 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3b1-134">ASP.NET Core SignalR apps that are published as an Azure Web App must have [ARR Affinity](https://en.wikipedia.org/wiki/Application_Request_Routing) enabled.</span></span> <span data-ttu-id="ed3b1-135">[Websocket](xref:fundamentals/websockets) 하면 Websocket 전송에서 함수를 허용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3b1-135">[WebSockets](xref:fundamentals/websockets) should be enabled, to allow the WebSockets transport to function.</span></span>

<span data-ttu-id="ed3b1-136">Azure 포털에서으로 이동 **앱 설정** 웹 앱에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3b1-136">In the Azure portal, navigate to **App Settings** for your web app.</span></span> <span data-ttu-id="ed3b1-137">설정 **Websocket** 를 **에**, 확인 하 고 **ARR 선호도** 은 **에**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3b1-137">Set **WebSockets** to **On**, and verify **ARR Affinity** is **On**.</span></span>

![Azure 포털에서 azure 웹 앱 설정](publish-to-azure-web-app/_static/azure-web-app-settings.png)

 <span data-ttu-id="ed3b1-139">Websocket 및 다른 전송의 [앱 서비스 계획에 따라 제한 됩니다](/azure/azure-subscription-service-limits#app-service-limits)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3b1-139">WebSockets and other transports [are limited based on the App Service Plan](/azure/azure-subscription-service-limits#app-service-limits).</span></span>

## <a name="related-resources"></a><span data-ttu-id="ed3b1-140">관련 참고 자료</span><span class="sxs-lookup"><span data-stu-id="ed3b1-140">Related resources</span></span>

* [<span data-ttu-id="ed3b1-141">명령줄 도구를 사용 하 여 Azure에 ASP.NET Core 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="ed3b1-141">Publish an ASP.NET Core app to Azure with command line tools</span></span>](xref:tutorials/publish-to-azure-webapp-using-cli?tabs=windows)
* [<span data-ttu-id="ed3b1-142">Visual Studio 사용 하 여 Azure에 ASP.NET Core 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="ed3b1-142">Publish an ASP.NET Core app to Azure with Visual Studio</span></span>](xref:tutorials/publish-to-azure-webapp-using-vs)
* [<span data-ttu-id="ed3b1-143">호스트 및 Azure에서 ASP.NET Core 미리 보기 앱 배포</span><span class="sxs-lookup"><span data-stu-id="ed3b1-143">Host and deploy ASP.NET Core Preview apps on Azure</span></span>](xref:host-and-deploy/azure-apps/index#deploy-aspnet-core-preview-release-to-azure-app-service)
