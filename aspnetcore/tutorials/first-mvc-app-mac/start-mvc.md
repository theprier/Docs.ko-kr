---
title: ASP.NET Core MVC 및 Mac용 Visual Studio 시작
author: rick-anderson
description: ASP.NET Core MVC 및 Visual Studio 시작 방법 배우기
manager: wpickett
ms.author: riande
ms.date: 8/23/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: tutorials/first-mvc-app-mac/start-mvc
ms.openlocfilehash: ffa620f07251c52c785672d8fbeefacac31ed4c1
ms.sourcegitcommit: 24c32648ab0c6f0be15333d7c23c1bf680858c43
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/21/2018
ms.locfileid: "30896642"
---
# <a name="get-started-with-aspnet-core-mvc-and-visual-studio-for-mac"></a><span data-ttu-id="9bd6f-103">ASP.NET Core MVC 및 Mac용 Visual Studio 시작</span><span class="sxs-lookup"><span data-stu-id="9bd6f-103">Get started with ASP.NET Core MVC and Visual Studio for Mac</span></span>

<span data-ttu-id="9bd6f-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="9bd6f-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="9bd6f-105">이 자습서에서는 [Mac용 Visual Studio](https://www.visualstudio.com/vs/visual-studio-mac/)를 사용하여 ASP.NET Core MVC 웹앱을 빌드하는 기본 사항에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9bd6f-105">This tutorial teaches you the basics of building an ASP.NET Core MVC web app using [Visual Studio for Mac](https://www.visualstudio.com/vs/visual-studio-mac/).</span></span> 

[!INCLUDE [consider RP](../../includes/razor.md)]

<span data-ttu-id="9bd6f-106">이 자습서는 세 가지 버전이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9bd6f-106">There are 3 versions of this tutorial:</span></span>

* <span data-ttu-id="9bd6f-107">macOS: [Mac용 Visual Studio을 사용하여 ASP.NET Core MVC 앱 빌드](xref:tutorials/first-mvc-app-mac/start-mvc)</span><span class="sxs-lookup"><span data-stu-id="9bd6f-107">macOS: [Build an ASP.NET Core MVC app with Visual Studio for Mac](xref:tutorials/first-mvc-app-mac/start-mvc)</span></span>
* <span data-ttu-id="9bd6f-108">Windows: [Visual Studio를 사용하여 ASP.NET Core MVC 앱 빌드](xref:tutorials/first-mvc-app/start-mvc)</span><span class="sxs-lookup"><span data-stu-id="9bd6f-108">Windows: [Build an ASP.NET Core MVC app with Visual Studio](xref:tutorials/first-mvc-app/start-mvc)</span></span>
* <span data-ttu-id="9bd6f-109">Linux, macOS 및 Windows: [Visual Studio Code를 사용하여 ASP.NET Core MVC 앱 빌드](xref:tutorials/first-mvc-app-xplat/start-mvc)</span><span class="sxs-lookup"><span data-stu-id="9bd6f-109">Linux, macOS, and Windows: [Build an ASP.NET Core MVC app with Visual Studio Code](xref:tutorials/first-mvc-app-xplat/start-mvc)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9bd6f-110">전제 조건</span><span class="sxs-lookup"><span data-stu-id="9bd6f-110">Prerequisites</span></span>

[!INCLUDE [](~/includes/net-core-prereqs-macos.md)]

## <a name="create-a-web-app"></a><span data-ttu-id="9bd6f-111">웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="9bd6f-111">Create a web app</span></span>

<span data-ttu-id="9bd6f-112">Visual Studio에서 **파일 > 새 솔루션**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9bd6f-112">From Visual Studio, select **File > New Solution**.</span></span>

![macOS 새 솔루션](../first-web-api-mac/_static/sln.png)

<span data-ttu-id="9bd6f-114">**.NET Core App > ASP.NET Core > 웹앱 > 다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9bd6f-114">Select **.NET Core App >  ASP.NET Core > Web App > Next**.</span></span>

![macOS 새 프로젝트 대화 상자](start-mvc/1.png)

<span data-ttu-id="9bd6f-116">프로젝트 이름을 **MvcMovie**로 지정하고 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9bd6f-116">Name the project **MvcMovie**, and then select **Create**.</span></span>

![macOS 새 프로젝트 대화 상자](start-mvc/2.png)

### <a name="launch-the-app"></a><span data-ttu-id="9bd6f-118">앱 시작</span><span class="sxs-lookup"><span data-stu-id="9bd6f-118">Launch the app</span></span>

<span data-ttu-id="9bd6f-119">Visual Studio에서 **실행 > 디버깅하지 않고 시작**을 선택하여 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9bd6f-119">In Visual Studio, select **Run > Start Without Debugging** to launch the app.</span></span> <span data-ttu-id="9bd6f-120">Visual Studio가 [Kestrel](xref:fundamentals/servers/index#kestrel)을 시작하고 브라우저를 실행하며 `http://localhost:port`로 이동합니다. 여기서 *port*는 임의로 선택된 포트 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="9bd6f-120">Visual Studio starts [Kestrel](xref:fundamentals/servers/index#kestrel), launches a browser, and navigates to `http://localhost:port`, where *port* is a randomly chosen port number.</span></span>

![새 프로젝트가 있는 브라우저](start-mvc/b1.png)

* <span data-ttu-id="9bd6f-122">주소 표시줄에 `localhost:port#`이 표시되고 `example.com` 등은 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9bd6f-122">The address bar shows `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="9bd6f-123">그 이유는 `localhost`가 로컬 컴퓨터의 표준 이름이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="9bd6f-123">That's because `localhost` is the standard hostname for your local computer.</span></span> <span data-ttu-id="9bd6f-124">Visual Studio에서 웹 프로젝트를 만들 경우 웹 서버에는 임의 포트가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9bd6f-124">When Visual Studio creates a web project, a random port is used for the web server.</span></span> <span data-ttu-id="9bd6f-125">앱을 실행할 경우 다른 포트 번호가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9bd6f-125">When you run the app, you'll see a different port number.</span></span>
* <span data-ttu-id="9bd6f-126">**실행** 메뉴 항목에서 앱을 디버그 또는 디버그 이외 모드로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9bd6f-126">You can launch the app in debug or non-debug mode from the **Run** menu.</span></span>

<span data-ttu-id="9bd6f-127">기본 템플릿은 **홈, 정보** 및 **연락처** 링크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9bd6f-127">The default template gives you **Home, About** and **Contact** links.</span></span> <span data-ttu-id="9bd6f-128">위의 브라우저 이미지에는 이러한 링크가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9bd6f-128">The browser image above doesn't show these links.</span></span> <span data-ttu-id="9bd6f-129">브라우저 크기에 따라 탐색 아이콘을 클릭하여 링크를 표시해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9bd6f-129">Depending on the size of your browser, you might need to click the navigation icon to show them.</span></span>

![새 프로젝트가 있는 브라우저](start-mvc/b2.png)

<span data-ttu-id="9bd6f-131">이 자습서의 다음 부분에서는 MVC에 대해 알아보고 일부 코드 작성을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9bd6f-131">In the next part of this tutorial, you learn about MVC and start writing some code.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="9bd6f-132">다음</span><span class="sxs-lookup"><span data-stu-id="9bd6f-132">Next</span></span>](adding-controller.md)  
