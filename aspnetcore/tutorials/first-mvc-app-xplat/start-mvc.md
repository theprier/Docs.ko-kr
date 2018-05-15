---
title: macOS, Linux 또는 Windows의 ASP.NET Core MVC 소개
author: rick-anderson
description: macOS, Linux 또는 Windows에서 ASP.NET Core MVC 및 Visual Studio Code를 시작하는 방법 알아보기
manager: wpickett
ms.author: riande
ms.date: 07/07/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: tutorials/first-mvc-app-xplat/start-mvc
ms.openlocfilehash: 50fbd54c6b0cc1146271afda7e45a0dab590dd7d
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="introduction-to-aspnet-core-mvc-on-macos-linux-or-windows"></a><span data-ttu-id="3ccb4-103">macOS, Linux 또는 Windows의 ASP.NET Core MVC 소개</span><span class="sxs-lookup"><span data-stu-id="3ccb4-103">Introduction to ASP.NET Core MVC on macOS, Linux, or Windows</span></span>

<span data-ttu-id="3ccb4-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="3ccb4-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="3ccb4-105">이 자습서에서는 [Visual Studio Code](https://code.visualstudio.com)(VS Code)를 사용하여 ASP.NET Core MVC 웹앱을 빌드하는 기본 사항에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-105">This tutorial will teach you the basics of building an ASP.NET Core MVC web app using [Visual Studio Code](https://code.visualstudio.com) (VS Code).</span></span> <span data-ttu-id="3ccb4-106">이 자습서에서는 VS 코드를 잘 알고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-106">The tutorial assumes familarity with VS Code.</span></span> <span data-ttu-id="3ccb4-107">자세한 내용은 [VS 코드 시작](https://code.visualstudio.com/docs) 및 [Visual Studio Code 도움말](#visual-studio-code-help)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-107">See [Getting started with VS Code](https://code.visualstudio.com/docs) and [Visual Studio Code help](#visual-studio-code-help) for more information.</span></span> 

[!INCLUDE [consider RP](../../includes/razor.md)]

<span data-ttu-id="3ccb4-108">이 자습서는 세 가지 버전이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-108">There are 3 versions of this tutorial:</span></span>

* <span data-ttu-id="3ccb4-109">macOS: [Mac용 Visual Studio를 사용하여 ASP.NET Core MVC 앱 만들기](xref:tutorials/first-mvc-app-mac/start-mvc)</span><span class="sxs-lookup"><span data-stu-id="3ccb4-109">macOS: [Create an ASP.NET Core MVC app with Visual Studio for Mac](xref:tutorials/first-mvc-app-mac/start-mvc)</span></span>
* <span data-ttu-id="3ccb4-110">Windows: [Visual Studio를 사용하여 ASP.NET Core MVC 앱 만들기](xref:tutorials/first-mvc-app/start-mvc)</span><span class="sxs-lookup"><span data-stu-id="3ccb4-110">Windows: [Create an ASP.NET Core MVC app with Visual Studio](xref:tutorials/first-mvc-app/start-mvc)</span></span>
* <span data-ttu-id="3ccb4-111">macOS, Linux 및 Windows: [Visual Studio Code를 사용하여 ASP.NET Core MVC 앱 만들기](xref:tutorials/first-mvc-app-xplat/start-mvc)</span><span class="sxs-lookup"><span data-stu-id="3ccb4-111">macOS, Linux, and Windows: [Create an ASP.NET Core MVC app with Visual Studio Code](xref:tutorials/first-mvc-app-xplat/start-mvc)</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3ccb4-112">전제 조건</span><span class="sxs-lookup"><span data-stu-id="3ccb4-112">Prerequisites</span></span>

[!INCLUDE [](~/includes/net-core-prereqs-vscode.md)]

## <a name="create-a-web-app-with-dotnet"></a><span data-ttu-id="3ccb4-113">Dotnet와 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="3ccb4-113">Create a web app with dotnet</span></span>

<span data-ttu-id="3ccb4-114">터미널에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-114">From a terminal, run the following commands:</span></span>

```console
mkdir MvcMovie
cd MvcMovie
dotnet new mvc
```

<span data-ttu-id="3ccb4-115">VS Code(Visual Studio Code)에서 *MvcMovie* 폴더를 열고 *Startup.cs* 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-115">Open the *MvcMovie* folder in Visual Studio Code (VS Code) and select the *Startup.cs* file.</span></span>

- <span data-ttu-id="3ccb4-116">다음 **경고** 메시지에 대해 **예**를 선택합니다. “빌드 및 디버그에 필요한 자산이 'MvcMovie'에서 누락되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-116">Select **Yes** to the **Warn** message "Required assets to build and debug are missing from 'MvcMovie'.</span></span> <span data-ttu-id="3ccb4-117">추가할까요?”</span><span class="sxs-lookup"><span data-stu-id="3ccb4-117">Add them?"</span></span>
- <span data-ttu-id="3ccb4-118">다음 **정보** 메시지에 대해 **복원**을 선택합니다. “확인되지 않은 종속성이 있습니다.”</span><span class="sxs-lookup"><span data-stu-id="3ccb4-118">Select **Restore** to the **Info** message "There are unresolved dependencies".</span></span>

![VS Code, 경고: 빌드 및 디버그에 필요한 자산이 'MvcMovie'에서 누락되었습니다. ](../web-api-vsc/_static/vsc_restore.png)

<span data-ttu-id="3ccb4-122">**디버그**(F5) 키를 눌러 프로그램을 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-122">Press **Debug** (F5) to build and run the program.</span></span>

![앱 실행](../first-mvc-app/start-mvc/_static/1.png)

<span data-ttu-id="3ccb4-124">VS Code가 [Kestrel](xref:fundamentals/servers/kestrel) 웹 서버를 시작하고 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-124">VS Code starts the [Kestrel](xref:fundamentals/servers/kestrel) web server and runs your app.</span></span> <span data-ttu-id="3ccb4-125">주소 표시줄에 `localhost:5000`이 표시되고 `example.com` 등은 표시되지 않음을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-125">Notice that the address bar shows `localhost:5000` and not something like `example.com`.</span></span> <span data-ttu-id="3ccb4-126">그 이유는 `localhost`가 로컬 컴퓨터의 표준 이름이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-126">That's because `localhost` is the standard hostname for your local computer.</span></span>

<span data-ttu-id="3ccb4-127">기본 템플릿은 작동하는 **홈, 정보** 및 **연락처** 링크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-127">The default template gives you working **Home, About** and **Contact** links.</span></span> <span data-ttu-id="3ccb4-128">위의 브라우저 이미지에는 이러한 링크가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-128">The browser image above doesn't show these links.</span></span> <span data-ttu-id="3ccb4-129">브라우저 크기에 따라 탐색 아이콘을 클릭하여 링크를 표시해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-129">Depending on the size of your browser, you might need to click the navigation icon to show them.</span></span>

![오른쪽 위의 탐색 아이콘](../first-mvc-app/start-mvc/_static/2.png)

<span data-ttu-id="3ccb4-131">이 자습서의 다음 부분에서는 MVC에 대해 알아보고 일부 코드 작성을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3ccb4-131">In the next part of this tutorial, we'll learn about MVC and start writing some code.</span></span>

## <a name="visual-studio-code-help"></a><span data-ttu-id="3ccb4-132">Visual Studio Code 도움말</span><span class="sxs-lookup"><span data-stu-id="3ccb4-132">Visual Studio Code help</span></span>

- [<span data-ttu-id="3ccb4-133">시작</span><span class="sxs-lookup"><span data-stu-id="3ccb4-133">Getting started</span></span>](https://code.visualstudio.com/docs)
- [<span data-ttu-id="3ccb4-134">디버깅</span><span class="sxs-lookup"><span data-stu-id="3ccb4-134">Debugging</span></span>](https://code.visualstudio.com/docs/editor/debugging)
- [<span data-ttu-id="3ccb4-135">통합 터미널</span><span class="sxs-lookup"><span data-stu-id="3ccb4-135">Integrated terminal</span></span>](https://code.visualstudio.com/docs/editor/integrated-terminal)
- [<span data-ttu-id="3ccb4-136">바로 가기 키</span><span class="sxs-lookup"><span data-stu-id="3ccb4-136">Keyboard shortcuts</span></span>](https://code.visualstudio.com/docs/getstarted/keybindings#_keyboard-shortcuts-reference)

  - [<span data-ttu-id="3ccb4-137">macOS 바로 가기 키</span><span class="sxs-lookup"><span data-stu-id="3ccb4-137">macOS keyboard shortcuts</span></span>](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-macos.pdf)
  - [<span data-ttu-id="3ccb4-138">Linux 바로 가기 키</span><span class="sxs-lookup"><span data-stu-id="3ccb4-138">Linux keyboard shortcuts</span></span>](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-linux.pdf)
  - [<span data-ttu-id="3ccb4-139">Windows 바로 가기 키</span><span class="sxs-lookup"><span data-stu-id="3ccb4-139">Windows keyboard shortcuts</span></span>](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-windows.pdf)

> [!div class="step-by-step"]
> [<span data-ttu-id="3ccb4-140">다음 - 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="3ccb4-140">Next - Add a controller</span></span>](adding-controller.md)
