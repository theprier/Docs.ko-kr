---
title: Visual Studio Code에서 ASP.NET Core Razor 페이지 시작
author: rick-anderson
description: Visual Studio Code를 사용하여 ASP.NET Core Razor 페이지 웹앱을 빌드하는 방법에 대한 기본 사항을 배웁니다.
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.date: 08/27/2017
uid: tutorials/razor-pages-vsc/razor-pages-start
ms.openlocfilehash: b7f6ca377a892fce912dc0ee9d4b7378f40fbf24
ms.sourcegitcommit: c12ebdab65853f27fbb418204646baf6ce69515e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/21/2018
ms.locfileid: "46522929"
---
# <a name="get-started-with-aspnet-core-razor-pages-in-visual-studio-code"></a><span data-ttu-id="db4f9-103">Visual Studio Code에서 ASP.NET Core Razor 페이지 시작</span><span class="sxs-lookup"><span data-stu-id="db4f9-103">Get started with ASP.NET Core Razor Pages in Visual Studio Code</span></span>

<span data-ttu-id="db4f9-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="db4f9-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="db4f9-105">이 자습서에서는 ASP.NET Core Razor 페이지 웹앱을 빌드하는 작업의 기본 사항을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="db4f9-105">This tutorial teaches the basics of building an ASP.NET Core Razor Pages web app.</span></span> <span data-ttu-id="db4f9-106">이 자습서를 시작하기 전에 [Razor 페이지 소개](xref:razor-pages/index)를 완료하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="db4f9-106">We recommend you complete [Introduction to Razor Pages](xref:razor-pages/index) before starting this tutorial.</span></span> <span data-ttu-id="db4f9-107">Razor 페이지는 ASP.NET Core에서 웹 응용 프로그램 UI를 빌드하는 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="db4f9-107">Razor Pages is the recommended way to build UI for web applications in ASP.NET Core.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="db4f9-108">전제 조건</span><span class="sxs-lookup"><span data-stu-id="db4f9-108">Prerequisites</span></span>

[!INCLUDE [](~/includes/net-core-prereqs-vscode.md)]

## <a name="create-a-razor-web-app"></a><span data-ttu-id="db4f9-109">Razor 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="db4f9-109">Create a Razor web app</span></span>

<span data-ttu-id="db4f9-110">터미널에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="db4f9-110">From a terminal, run the following commands:</span></span>

::: moniker range=">= aspnetcore-2.1"

```console
dotnet new webapp -o RazorPagesMovie
cd RazorPagesMovie
dotnet run
```

::: moniker-end

::: moniker range="= aspnetcore-2.0"

```console
dotnet new razor -o RazorPagesMovie
cd RazorPagesMovie
dotnet run
```

::: moniker-end

<span data-ttu-id="db4f9-111">이전 명령은 [.NET Core CLI](https://docs.microsoft.com/dotnet/core/tools/dotnet)를 사용하여 Razor 페이지 프로젝트를 만들고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="db4f9-111">The preceding commands use the [.NET Core CLI](https://docs.microsoft.com/dotnet/core/tools/dotnet) to create and run a Razor Pages project.</span></span> <span data-ttu-id="db4f9-112">브라우저를 열고 http://localhost:5000으로 이동하여 응용 프로그램을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="db4f9-112">Open a browser to http://localhost:5000 to view the application.</span></span>

![홈 또는 인덱스 페이지](../razor-pages/razor-pages-start/_static/home.png)

[!INCLUDE [razor-pages-start](../../includes/RP/razor-pages-start.md)]

## <a name="open-the-project"></a><span data-ttu-id="db4f9-114">프로젝트 열기</span><span class="sxs-lookup"><span data-stu-id="db4f9-114">Open the project</span></span>

<span data-ttu-id="db4f9-115">Ctrl+C를 눌러 응용 프로그램을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="db4f9-115">Press Ctrl+C to shut down the application.</span></span>

<span data-ttu-id="db4f9-116">VS Code(Visual Studio Code)에서 **파일 > 폴더 열기**를 선택하고 *RazorPagesMovie* 폴더를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db4f9-116">From Visual Studio Code (VS Code), select **File > Open Folder**, and then select the *RazorPagesMovie* folder.</span></span>

- <span data-ttu-id="db4f9-117">다음 **경고** 메시지에 대해 **예**를 선택합니다. “빌드 및 디버그에 필요한 자산이 ‘RazorPagesMovie’에서 누락되었습니다.</span><span class="sxs-lookup"><span data-stu-id="db4f9-117">Select **Yes** to the **Warn** message "Required assets to build and debug are missing from 'RazorPagesMovie'.</span></span> <span data-ttu-id="db4f9-118">추가할까요?”</span><span class="sxs-lookup"><span data-stu-id="db4f9-118">Add them?"</span></span>
- <span data-ttu-id="db4f9-119">다음 **정보** 메시지에 대해 **복원**을 선택합니다. “확인되지 않은 종속성이 있습니다.”</span><span class="sxs-lookup"><span data-stu-id="db4f9-119">Select **Restore** to the **Info** message "There are unresolved dependencies".</span></span>

### <a name="launch-the-app"></a><span data-ttu-id="db4f9-120">앱 시작</span><span class="sxs-lookup"><span data-stu-id="db4f9-120">Launch the app</span></span>

<span data-ttu-id="db4f9-121">Ctrl+F5를 눌러 디버깅 없이 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="db4f9-121">Press Ctrl+F5 to start the app without debugging.</span></span> <span data-ttu-id="db4f9-122">또는 **디버그** 메뉴에서 **디버깅하지 않고 시작**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db4f9-122">Alternatively, from the **Debug** menu, select **Start Without Debugging**.</span></span>

<span data-ttu-id="db4f9-123">다음 자습서에서는 프로젝트에 모델을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="db4f9-123">In the next tutorial, we add a model to the project.</span></span> 

> [!div class="step-by-step"]
> [<span data-ttu-id="db4f9-124">다음: 모델 추가</span><span class="sxs-lookup"><span data-stu-id="db4f9-124">Next: Adding a model</span></span>](xref:tutorials/razor-pages-vsc/model)  
