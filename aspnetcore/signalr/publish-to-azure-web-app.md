---
title: 게시는 ASP.NET Core SignalR 앱을 Azure 웹 앱
author: tdykstra
description: 게시는 ASP.NET Core SignalR 앱을 Azure 웹 앱
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 04/20/2018
uid: signalr/publish-to-azure-web-app
ms.openlocfilehash: a6a0e44f5c67fefdac6bd26b3772c23e75f8bfc1
ms.sourcegitcommit: 32f5ee0690604d451f61e9a5c28881c9fcf85738
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/29/2018
ms.locfileid: "47454728"
---
# <a name="publish-an-aspnet-core-signalr-app-to-an-azure-web-app"></a><span data-ttu-id="b1dbb-103">게시는 ASP.NET Core SignalR 앱을 Azure 웹 앱</span><span class="sxs-lookup"><span data-stu-id="b1dbb-103">Publish an ASP.NET Core SignalR app to an Azure Web App</span></span>

<span data-ttu-id="b1dbb-104">[Azure Web App](/azure/app-service/app-service-web-overview) 되는 [Microsoft 클라우드 컴퓨팅](https://azure.microsoft.com/) ASP.NET Core를 포함 하 여 웹 앱을 호스트 하기 위한 플랫폼 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="b1dbb-104">[Azure Web App](/azure/app-service/app-service-web-overview) is a [Microsoft cloud computing](https://azure.microsoft.com/) platform service for hosting web apps, including ASP.NET Core.</span></span>

> [!NOTE]
> <span data-ttu-id="b1dbb-105">이 문서에서는 Visual Studio에서 ASP.NET Core SignalR 앱을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1dbb-105">This article refers to publishing an ASP.NET Core SignalR app from Visual Studio.</span></span> <span data-ttu-id="b1dbb-106">방문 [azure SignalR service](https://azure.microsoft.com/en-gb/services/signalr-service?) SignalR을 사용 하 여 Azure에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1dbb-106">Visit [SignalR service for Azure](https://azure.microsoft.com/en-gb/services/signalr-service?) for more information about using SignalR on Azure.</span></span>

## <a name="publish-the-app"></a><span data-ttu-id="b1dbb-107">앱 게시</span><span class="sxs-lookup"><span data-stu-id="b1dbb-107">Publish the app</span></span>

<span data-ttu-id="b1dbb-108">Visual Studio를 Azure 웹 앱 게시에 대 한 기본 제공 도구를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b1dbb-108">Visual Studio provides built-in tools for publishing to an Azure Web App.</span></span> <span data-ttu-id="b1dbb-109">Visual Studio Code 사용자 사용할 수 있습니다 [Azure CLI](/cli/azure) Azure에 앱을 게시 하는 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b1dbb-109">Visual Studio Code user can use [Azure CLI](/cli/azure) commands to publish apps to Azure.</span></span> <span data-ttu-id="b1dbb-110">이 문서에서는 Visual Studio에서 도구를 사용 하 여 게시에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1dbb-110">This article covers publishing using the tools in Visual Studio.</span></span> <span data-ttu-id="b1dbb-111">Azure CLI를 사용 하 여 앱을 게시 하려면 참조 [명령줄 도구를 사용 하 여 Azure에 ASP.NET Core 앱을 게시](/azure/app-service/app-service-web-get-started-dotnet)합니다.</span><span class="sxs-lookup"><span data-stu-id="b1dbb-111">To publish an app using Azure CLI, see [Publish an ASP.NET Core app to Azure with command line tools](/azure/app-service/app-service-web-get-started-dotnet).</span></span>

<span data-ttu-id="b1dbb-112">프로젝트를 마우스 오른쪽 단추로 클릭 **솔루션 탐색기** 선택한 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1dbb-112">Right-click on the project in **Solution Explorer** and select **Publish**.</span></span> <span data-ttu-id="b1dbb-113">확인 **새로 만들기** 체크 인 합니다 **게시 대상 선택** 대화 상자에서 선택한 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1dbb-113">Confirm that **Create new** is checked in the **Pick a publish target** dialog, and select **Publish**.</span></span>

![게시 대상 선택](publish-to-azure-web-app/_static/pick-publish-target-dialog.png)

<span data-ttu-id="b1dbb-115">다음 정보를 입력 합니다 **App Service 만들기** 대화 상자와 선택 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1dbb-115">Enter the following information in the **Create App Service** dialog and select **Create**.</span></span>

| <span data-ttu-id="b1dbb-116">항목</span><span class="sxs-lookup"><span data-stu-id="b1dbb-116">Item</span></span> | <span data-ttu-id="b1dbb-117">설명</span><span class="sxs-lookup"><span data-stu-id="b1dbb-117">Description</span></span> |
| ---- | ----------- |
| <span data-ttu-id="b1dbb-118">**앱 이름**</span><span class="sxs-lookup"><span data-stu-id="b1dbb-118">**App name**</span></span> | <span data-ttu-id="b1dbb-119">앱의 고유 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b1dbb-119">A unique name of the app.</span></span> |
| <span data-ttu-id="b1dbb-120">**구독**</span><span class="sxs-lookup"><span data-stu-id="b1dbb-120">**Subscription**</span></span> | <span data-ttu-id="b1dbb-121">앱을 사용 하는 Azure 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="b1dbb-121">The Azure subscription that the app uses.</span></span> |
| <span data-ttu-id="b1dbb-122">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="b1dbb-122">**Resource Group**</span></span> | <span data-ttu-id="b1dbb-123">앱이 속해 있는 관련된 리소스의 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="b1dbb-123">The group of related resources to which the app belongs.</span></span>  |
| <span data-ttu-id="b1dbb-124">**호스팅 계획**</span><span class="sxs-lookup"><span data-stu-id="b1dbb-124">**Hosting Plan**</span></span> | <span data-ttu-id="b1dbb-125">웹 앱에 대 한 가격 책정 계획입니다.</span><span class="sxs-lookup"><span data-stu-id="b1dbb-125">The pricing plan for the web app.</span></span> |

![App service 만들기](publish-to-azure-web-app/_static/create-app-service-dialog.png)

<span data-ttu-id="b1dbb-127">Visual Studio에는 다음 작업을 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1dbb-127">Visual Studio completes the following tasks:</span></span>

* <span data-ttu-id="b1dbb-128">게시 프로필을 만들고 게시 설정을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1dbb-128">Creates a Publish Profile containing publish settings.</span></span>
* <span data-ttu-id="b1dbb-129">만들거나 기존 사용 *Azure Web App* 제공된 된 정보를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1dbb-129">Creates or uses an existing *Azure Web App* with the provided details.</span></span>
* <span data-ttu-id="b1dbb-130">앱을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="b1dbb-130">Publishes the app.</span></span>
* <span data-ttu-id="b1dbb-131">게시 된 웹 앱 로드를 사용 하 여 브라우저를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1dbb-131">Launches a browser, with the published web app loaded.</span></span>

<span data-ttu-id="b1dbb-132">앱에 대 한 URL의 형식을 확인할 수 있습니다 *{앱 이름}.azurewebsites.net*합니다.</span><span class="sxs-lookup"><span data-stu-id="b1dbb-132">Notice the format of the URL for the app is *{app name}.azurewebsites.net*.</span></span> <span data-ttu-id="b1dbb-133">예를 들어, 명명 된 앱 `SignalRChattR` 같은 URL이 `https://signalrchattr.azurewebsites.net`합니다.</span><span class="sxs-lookup"><span data-stu-id="b1dbb-133">For example, an app named `SignalRChattR` has a URL that looks like `https://signalrchattr.azurewebsites.net`.</span></span>

<span data-ttu-id="b1dbb-134">HTTP 502.2 오류가 발생 하는 경우 참조 [Azure App Service에 ASP.NET Core 배포 미리 보기 릴리스](xref:host-and-deploy/azure-apps/index) 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1dbb-134">If an HTTP 502.2 error occurs, see [Deploy ASP.NET Core preview release to Azure App Service](xref:host-and-deploy/azure-apps/index) to resolve it.</span></span>

## <a name="configure-signalr-web-app"></a><span data-ttu-id="b1dbb-135">SignalR 웹 앱 구성</span><span class="sxs-lookup"><span data-stu-id="b1dbb-135">Configure SignalR web app</span></span>

<span data-ttu-id="b1dbb-136">Azure 웹 앱을가지고 있어야 게시 된 ASP.NET Core SignalR 앱 [ARR 선호도](https://en.wikipedia.org/wiki/Application_Request_Routing) 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1dbb-136">ASP.NET Core SignalR apps that are published as an Azure Web App must have [ARR Affinity](https://en.wikipedia.org/wiki/Application_Request_Routing) enabled.</span></span> <span data-ttu-id="b1dbb-137">[Websocket](xref:fundamentals/websockets) 하면 Websocket 전송에서 함수를 허용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1dbb-137">[WebSockets](xref:fundamentals/websockets) should be enabled, to allow the WebSockets transport to function.</span></span>

<span data-ttu-id="b1dbb-138">Azure portal로 이동 **앱 설정** 웹 앱에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1dbb-138">In the Azure portal, navigate to **App Settings** for your web app.</span></span> <span data-ttu-id="b1dbb-139">설정 **Websocket** 를 **에**를 확인 하 고 **ARR 선호도** 는 **에서**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1dbb-139">Set **WebSockets** to **On**, and verify **ARR Affinity** is **On**.</span></span>

![Azure portal에서 azure 웹 앱 설정](publish-to-azure-web-app/_static/azure-web-app-settings.png)

 <span data-ttu-id="b1dbb-141">Websocket 및 다른 전송 [App Service 계획에 따라 제한 됩니다](/azure/azure-subscription-service-limits#app-service-limits)합니다.</span><span class="sxs-lookup"><span data-stu-id="b1dbb-141">WebSockets and other transports [are limited based on the App Service Plan](/azure/azure-subscription-service-limits#app-service-limits).</span></span>

## <a name="related-resources"></a><span data-ttu-id="b1dbb-142">관련 참고 자료</span><span class="sxs-lookup"><span data-stu-id="b1dbb-142">Related resources</span></span>

* [<span data-ttu-id="b1dbb-143">명령줄 도구를 사용 하 여 Azure에 ASP.NET Core 앱 게시</span><span class="sxs-lookup"><span data-stu-id="b1dbb-143">Publish an ASP.NET Core app to Azure with command line tools</span></span>](/azure/app-service/app-service-web-get-started-dotnet)
* [<span data-ttu-id="b1dbb-144">Visual Studio 사용 하 여 Azure에 ASP.NET Core 앱 게시</span><span class="sxs-lookup"><span data-stu-id="b1dbb-144">Publish an ASP.NET Core app to Azure with Visual Studio</span></span>](xref:tutorials/publish-to-azure-webapp-using-vs)
* [<span data-ttu-id="b1dbb-145">호스트 및 Azure에서 ASP.NET Core 미리 보기 앱 배포</span><span class="sxs-lookup"><span data-stu-id="b1dbb-145">Host and deploy ASP.NET Core Preview apps on Azure</span></span>](xref:host-and-deploy/azure-apps/index#deploy-aspnet-core-preview-release-to-azure-app-service)
