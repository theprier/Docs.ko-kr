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
ms.openlocfilehash: 8612824cc9d4a9ace1c214411c44754350100f06
ms.sourcegitcommit: 7e87671fea9a5f36ca516616fe3b40b537f428d2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35341810"
---
# <a name="publish-an-aspnet-core-signalr-app-to-an-azure-web-app"></a><span data-ttu-id="a604a-103">ASP.NET Core 게시 된 Azure 웹 앱에 SignalR 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="a604a-103">Publish an ASP.NET Core SignalR app to an Azure Web App</span></span>

<span data-ttu-id="a604a-104">[Azure 웹 앱](/azure/app-service/app-service-web-overview) 는 [Microsoft 클라우드 컴퓨팅](https://azure.microsoft.com/) ASP.NET Core를 포함 하 여 웹 응용 프로그램을 호스팅하기 위한 플랫폼 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="a604a-104">[Azure Web App](/azure/app-service/app-service-web-overview) is a [Microsoft cloud computing](https://azure.microsoft.com/) platform service for hosting web apps, including ASP.NET Core.</span></span>

> [!NOTE]
> <span data-ttu-id="a604a-105">이 문서에서는 Visual Studio에서 ASP.NET Core SignalR 응용 프로그램을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a604a-105">This article refers to publishing an ASP.NET Core SignalR app from Visual Studio.</span></span> <span data-ttu-id="a604a-106">방문 [Azure SignalR 서비스](https://azure.microsoft.com/en-gb/services/signalr-service?) SignalR을 사용 하 여 Azure에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="a604a-106">Visit [SignalR service for Azure](https://azure.microsoft.com/en-gb/services/signalr-service?) for more information about using SignalR on Azure.</span></span>

## <a name="publish-the-app"></a><span data-ttu-id="a604a-107">앱 게시</span><span class="sxs-lookup"><span data-stu-id="a604a-107">Publish the app</span></span>

<span data-ttu-id="a604a-108">Visual Studio는 Azure 웹 앱에 게시에 대 한 기본 제공 도구를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a604a-108">Visual Studio provides built-in tools for publishing to an Azure Web App.</span></span> <span data-ttu-id="a604a-109">Visual Studio Code 사용자 צ ְ ײ [Azure CLI](/cli/azure) Azure에 앱을 게시 하기 위해 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="a604a-109">Visual Studio Code user can use [Azure CLI](/cli/azure) commands to publish apps to Azure.</span></span> <span data-ttu-id="a604a-110">이 문서에서는 Visual Studio에서 도구를 사용 하 여 게시에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a604a-110">This article covers publishing using the tools in Visual Studio.</span></span> <span data-ttu-id="a604a-111">Azure CLI를 사용 하 여 앱을 게시 하려면 참조 [명령줄 도구를 사용 하 여 Azure에 ASP.NET Core 응용 프로그램을 게시](xref:tutorials/publish-to-azure-webapp-using-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="a604a-111">To publish an app using Azure CLI, see [Publish an ASP.NET Core app to Azure with command line tools](xref:tutorials/publish-to-azure-webapp-using-cli).</span></span>

<span data-ttu-id="a604a-112">프로젝트를 마우스 오른쪽 단추로 클릭 **솔루션 탐색기** 선택 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="a604a-112">Right-click on the project in **Solution Explorer** and select **Publish**.</span></span> <span data-ttu-id="a604a-113">확인 **새로 만들기** 체크 인은 **게시 대상 선택** 대화 상자를 닫고 선택 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="a604a-113">Confirm that **Create new** is checked in the **Pick a publish target** dialog, and select **Publish**.</span></span>

![선택 대상 게시](publish-to-azure-web-app/_static/pick-publish-target-dialog.png)

<span data-ttu-id="a604a-115">다음 정보를 입력의 **응용 프로그램 서비스 만들기** 대화 상자와 선택 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="a604a-115">Enter the following information in the **Create App Service** dialog and select **Create**.</span></span>

| <span data-ttu-id="a604a-116">항목</span><span class="sxs-lookup"><span data-stu-id="a604a-116">Item</span></span> | <span data-ttu-id="a604a-117">설명</span><span class="sxs-lookup"><span data-stu-id="a604a-117">Description</span></span> |
| ---- | ----------- |
| <span data-ttu-id="a604a-118">**응용 프로그램 이름**</span><span class="sxs-lookup"><span data-stu-id="a604a-118">**App name**</span></span> | <span data-ttu-id="a604a-119">응용 프로그램의 고유 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a604a-119">A unique name of the app.</span></span> |
| <span data-ttu-id="a604a-120">**구독**</span><span class="sxs-lookup"><span data-stu-id="a604a-120">**Subscription**</span></span> | <span data-ttu-id="a604a-121">응용 프로그램을 사용 하는 Azure 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="a604a-121">The Azure subscription that the app uses.</span></span> |
| <span data-ttu-id="a604a-122">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="a604a-122">**Resource Group**</span></span> | <span data-ttu-id="a604a-123">응용 프로그램 속해 있는 관련된 리소스의 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="a604a-123">The group of related resources to which the app belongs.</span></span>  |
| <span data-ttu-id="a604a-124">**호스팅 계획**</span><span class="sxs-lookup"><span data-stu-id="a604a-124">**Hosting Plan**</span></span> | <span data-ttu-id="a604a-125">웹 앱에 대 한 가격 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="a604a-125">The pricing plan for the web app.</span></span> |

![앱 서비스 만들기](publish-to-azure-web-app/_static/create-app-service-dialog.png)

<span data-ttu-id="a604a-127">Visual Studio에서는 다음과 같은 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="a604a-127">Visual Studio completes the following tasks:</span></span>

* <span data-ttu-id="a604a-128">게시 프로필을 만듭니다 포함 된 게시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a604a-128">Creates a Publish Profile containing publish settings.</span></span>
* <span data-ttu-id="a604a-129">만들거나 기존의 사용 *Azure 웹 앱* 제공 된 세부 정보를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a604a-129">Creates or uses an existing *Azure Web App* with the provided details.</span></span>
* <span data-ttu-id="a604a-130">응용 프로그램을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="a604a-130">Publishes the app.</span></span>
* <span data-ttu-id="a604a-131">로드 된 게시 된 웹 앱과 함께 브라우저를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a604a-131">Launches a browser, with the published web app loaded.</span></span>

<span data-ttu-id="a604a-132">응용 프로그램에 대 한 URL의 형식이 확인 *{응용 프로그램 이름}.azurewebsites.net*합니다.</span><span class="sxs-lookup"><span data-stu-id="a604a-132">Notice the format of the URL for the app is *{app name}.azurewebsites.net*.</span></span> <span data-ttu-id="a604a-133">예를 들어 앱 `SignalRChattR` 에 다음과 같은 URL `https://signalrchattr.azurewebsites.net`합니다.</span><span class="sxs-lookup"><span data-stu-id="a604a-133">For example, an app named `SignalRChattR` has a URL that looks like `https://signalrchattr.azurewebsites.net`.</span></span>

<span data-ttu-id="a604a-134">HTTP 502.2 오류가 발생 하는 경우 참조 [Azure 앱 서비스에 ASP.NET Core 배포 미리 보기 릴리스의](xref:host-and-deploy/azure-apps/index) 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a604a-134">If an HTTP 502.2 error occurs, see [Deploy ASP.NET Core preview release to Azure App Service](xref:host-and-deploy/azure-apps/index) to resolve it.</span></span>

## <a name="configure-signalr-web-app"></a><span data-ttu-id="a604a-135">SignalR 웹 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="a604a-135">Configure SignalR web app</span></span>

<span data-ttu-id="a604a-136">Azure 웹 앱으로 게시 하는 ASP.NET SignalR Core 앱 [ARR 선호도](https://en.wikipedia.org/wiki/Application_Request_Routing) 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a604a-136">ASP.NET Core SignalR apps that are published as an Azure Web App must have [ARR Affinity](https://en.wikipedia.org/wiki/Application_Request_Routing) enabled.</span></span> <span data-ttu-id="a604a-137">[Websocket](xref:fundamentals/websockets) 하면 Websocket 전송에서 함수를 허용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a604a-137">[WebSockets](xref:fundamentals/websockets) should be enabled, to allow the WebSockets transport to function.</span></span>

<span data-ttu-id="a604a-138">Azure 포털에서으로 이동 **앱 설정** 웹 앱에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a604a-138">In the Azure portal, navigate to **App Settings** for your web app.</span></span> <span data-ttu-id="a604a-139">설정 **Websocket** 를 **에**, 확인 하 고 **ARR 선호도** 은 **에**합니다.</span><span class="sxs-lookup"><span data-stu-id="a604a-139">Set **WebSockets** to **On**, and verify **ARR Affinity** is **On**.</span></span>

![Azure 포털에서 azure 웹 앱 설정](publish-to-azure-web-app/_static/azure-web-app-settings.png)

 <span data-ttu-id="a604a-141">Websocket 및 다른 전송의 [앱 서비스 계획에 따라 제한 됩니다](/azure/azure-subscription-service-limits#app-service-limits)합니다.</span><span class="sxs-lookup"><span data-stu-id="a604a-141">WebSockets and other transports [are limited based on the App Service Plan](/azure/azure-subscription-service-limits#app-service-limits).</span></span>

## <a name="related-resources"></a><span data-ttu-id="a604a-142">관련 참고 자료</span><span class="sxs-lookup"><span data-stu-id="a604a-142">Related resources</span></span>

* [<span data-ttu-id="a604a-143">명령줄 도구를 사용 하 여 Azure에 ASP.NET Core 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="a604a-143">Publish an ASP.NET Core app to Azure with command line tools</span></span>](xref:tutorials/publish-to-azure-webapp-using-cli?tabs=windows)
* [<span data-ttu-id="a604a-144">Visual Studio 사용 하 여 Azure에 ASP.NET Core 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="a604a-144">Publish an ASP.NET Core app to Azure with Visual Studio</span></span>](xref:tutorials/publish-to-azure-webapp-using-vs)
* [<span data-ttu-id="a604a-145">호스트 및 Azure에서 ASP.NET Core 미리 보기 앱 배포</span><span class="sxs-lookup"><span data-stu-id="a604a-145">Host and deploy ASP.NET Core Preview apps on Azure</span></span>](xref:host-and-deploy/azure-apps/index#deploy-aspnet-core-preview-release-to-azure-app-service)
