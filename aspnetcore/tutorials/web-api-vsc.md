---
title: "ASP.NET Core 및 VS Code를 사용하여 Web API 만들기"
author: rick-anderson
description: "ASP.NET Core MVC 및 Visual Studio Code를 사용하여 macOS, Linux 또는 Windows에서 웹 API 빌드"
manager: wpickett
ms.author: riande
ms.date: 09/22/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: tutorials/web-api-vsc
ms.openlocfilehash: 44566c4014400aa2ca3d512eeaa226637b5f0b97
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="create-a-web-api-with-aspnet-core-mvc-and-visual-studio-code-on-linux-macos-and-windows"></a><span data-ttu-id="5c2f0-103">Linux, macOS 및 Windows에서 ASP.NET Core MVC 및 Visual Studio Code를 사용하여 Web API 만들기</span><span class="sxs-lookup"><span data-stu-id="5c2f0-103">Create a Web API with ASP.NET Core MVC and Visual Studio Code on Linux, macOS, and Windows</span></span>

<span data-ttu-id="5c2f0-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Mike Wasson](https://github.com/mikewasson)</span><span class="sxs-lookup"><span data-stu-id="5c2f0-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Mike Wasson](https://github.com/mikewasson)</span></span>

<span data-ttu-id="5c2f0-105">이 자습서에서는 “할 일” 항목 목록을 관리하기 위한 웹 API를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="5c2f0-105">In this tutorial, build a web API for managing a list of "to-do" items.</span></span> <span data-ttu-id="5c2f0-106">UI는 생성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5c2f0-106">A UI isn't constructed.</span></span>

<span data-ttu-id="5c2f0-107">이 자습서는 세 가지 버전이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c2f0-107">There are 3 versions of this tutorial:</span></span>

* <span data-ttu-id="5c2f0-108">macOS, Linux, Windows: Visual Studio Code를 사용한 Web API(이 자습서)</span><span class="sxs-lookup"><span data-stu-id="5c2f0-108">macOS, Linux, Windows: Web API with Visual Studio Code (This tutorial)</span></span>
* <span data-ttu-id="5c2f0-109">macOS: [Mac용 Visual Studio를 사용한 Web API](xref:tutorials/first-web-api-mac)</span><span class="sxs-lookup"><span data-stu-id="5c2f0-109">macOS: [Web API with Visual Studio for Mac](xref:tutorials/first-web-api-mac)</span></span>
* <span data-ttu-id="5c2f0-110">Windows: [Windows용 Visual Studio를 사용한 Web API](xref:tutorials/first-web-api)</span><span class="sxs-lookup"><span data-stu-id="5c2f0-110">Windows: [Web API with Visual Studio for Windows](xref:tutorials/first-web-api)</span></span>

<!-- WARNING: The code AND images in this doc are used by uid: tutorials/web-api-vsc, tutorials/first-web-api-mac and tutorials/first-web-api. If you change any code/images in this tutorial, update uid: tutorials/web-api-vsc -->

[!INCLUDE[template files](../includes/webApi/intro.md)]

## <a name="set-up-your-development-environment"></a><span data-ttu-id="5c2f0-111">개발 환경 설정</span><span class="sxs-lookup"><span data-stu-id="5c2f0-111">Set up your development environment</span></span>

<span data-ttu-id="5c2f0-112">다운로드 및 설치:</span><span class="sxs-lookup"><span data-stu-id="5c2f0-112">Download and install:</span></span>
- <span data-ttu-id="5c2f0-113">[.NET Core 2.0.0 SDK](https://www.microsoft.com/net/core) 이상.</span><span class="sxs-lookup"><span data-stu-id="5c2f0-113">[.NET Core 2.0.0 SDK](https://www.microsoft.com/net/core) or later.</span></span>
- [<span data-ttu-id="5c2f0-114">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="5c2f0-114">Visual Studio Code</span></span>](https://code.visualstudio.com)
- <span data-ttu-id="5c2f0-115">Visual Studio Code [C# 확장](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)</span><span class="sxs-lookup"><span data-stu-id="5c2f0-115">Visual Studio Code [C# extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)</span></span>

## <a name="create-the-project"></a><span data-ttu-id="5c2f0-116">프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5c2f0-116">Create the project</span></span>

<span data-ttu-id="5c2f0-117">콘솔에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5c2f0-117">From a console, run the following commands:</span></span>

```console
mkdir TodoApi
cd TodoApi
dotnet new webapi
```

<span data-ttu-id="5c2f0-118">VS Code(Visual Studio Code)에서 *TodoApi* 폴더를 열고 *Startup.cs* 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5c2f0-118">Open the *TodoApi* folder in Visual Studio Code (VS Code) and select the *Startup.cs* file.</span></span>

- <span data-ttu-id="5c2f0-119">다음 **경고** 메시지에 대해 **예**를 선택합니다. “빌드 및 디버그에 필요한 자산이 ‘TodoApi’에서 누락되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5c2f0-119">Select **Yes** to the **Warn** message "Required assets to build and debug are missing from 'TodoApi'.</span></span> <span data-ttu-id="5c2f0-120">추가할까요?”</span><span class="sxs-lookup"><span data-stu-id="5c2f0-120">Add them?"</span></span>
- <span data-ttu-id="5c2f0-121">다음 **정보** 메시지에 대해 **복원**을 선택합니다. “확인되지 않은 종속성이 있습니다.”</span><span class="sxs-lookup"><span data-stu-id="5c2f0-121">Select **Restore** to the **Info** message "There are unresolved dependencies".</span></span>

<!-- uid: tutorials/first-mvc-app-xplat/start-mvc uses the pic below. If you change it, make sure it's consistent -->

![빌드 및 디버그에 필요한 자산이 ‘TodoApi’에서 누락되었습니다. 경고가 있는 VS Code](web-api-vsc/_static/vsc_restore.png)

<span data-ttu-id="5c2f0-125">**디버그**(F5) 키를 눌러 프로그램을 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5c2f0-125">Press **Debug** (F5) to build and run the program.</span></span> <span data-ttu-id="5c2f0-126">브라우저에서 http://localhost:5000/api/값으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5c2f0-126">In a browser navigate to http://localhost:5000/api/values .</span></span> <span data-ttu-id="5c2f0-127">다음이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c2f0-127">The following is displayed:</span></span>

`["value1","value2"]`

<span data-ttu-id="5c2f0-128">VS Code 사용에 대한 팁은 [Visual Studio Code 도움말](#visual-studio-code-help)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5c2f0-128">See [Visual Studio Code help](#visual-studio-code-help) for tips on using VS Code.</span></span>

## <a name="add-support-for-entity-framework-core"></a><span data-ttu-id="5c2f0-129">Entity Framework Core에 대한 지원 추가</span><span class="sxs-lookup"><span data-stu-id="5c2f0-129">Add support for Entity Framework Core</span></span>

<span data-ttu-id="5c2f0-130">.NET Core 2.0에서 새 프로젝트를 만들면 *TodoApi.csproj* 파일에 'Microsoft.AspNetCore.All' 공급자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5c2f0-130">Creating a new project in .NET Core 2.0 adds the 'Microsoft.AspNetCore.All' provider in the *TodoApi.csproj* file.</span></span> <span data-ttu-id="5c2f0-131">[Entity Framework Core InMemory](https://docs.microsoft.com/ef/core/providers/in-memory/) 데이터베이스 공급자를 별도로 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5c2f0-131">There's no need to install the [Entity Framework Core InMemory](https://docs.microsoft.com/ef/core/providers/in-memory/) database provider separately.</span></span> <span data-ttu-id="5c2f0-132">이 데이터베이스 공급자를 설치하면 Entity Framework Core를 메모리 내 데이터베이스에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c2f0-132">This database provider allows Entity Framework Core to be used with an in-memory database.</span></span>

[!code-xml[Main](web-api-vsc/sample/TodoApi/TodoApi.csproj?highlight=12)]

## <a name="add-a-model-class"></a><span data-ttu-id="5c2f0-133">모델 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="5c2f0-133">Add a model class</span></span>

<span data-ttu-id="5c2f0-134">모델은 응용 프로그램에서 데이터를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="5c2f0-134">A model is an object that represents the data in your application.</span></span> <span data-ttu-id="5c2f0-135">이 경우 유일한 모델은 할 일 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="5c2f0-135">In this case, the only model is a to-do item.</span></span>

<span data-ttu-id="5c2f0-136">*Models* 폴더를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5c2f0-136">Add a folder named *Models*.</span></span> <span data-ttu-id="5c2f0-137">프로젝트의 아무 곳에나 모델 클래스를 넣을 수 있지만 일반적으로 *Models* 폴더를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5c2f0-137">You can put model classes anywhere in your project, but the *Models* folder is used by convention.</span></span>

<span data-ttu-id="5c2f0-138">`TodoItem` 클래스를 다음 코드로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5c2f0-138">Add a `TodoItem` class with the following code:</span></span>

[!code-csharp[Main](first-web-api/sample/TodoApi/Models/TodoItem.cs)]

<span data-ttu-id="5c2f0-139">`TodoItem`이 만들어질 때 데이터베이스가 `Id`를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="5c2f0-139">The database generates the `Id` when a `TodoItem` is created.</span></span>

## <a name="create-the-database-context"></a><span data-ttu-id="5c2f0-140">데이터베이스 컨텍스트 만들기</span><span class="sxs-lookup"><span data-stu-id="5c2f0-140">Create the database context</span></span>

<span data-ttu-id="5c2f0-141">*데이터베이스 컨텍스트*는 특정 데이터 모델에 맞게 Entity Framework 기능을 조정하는 주 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="5c2f0-141">The *database context* is the main class that coordinates Entity Framework functionality for a given data model.</span></span> <span data-ttu-id="5c2f0-142">`Microsoft.EntityFrameworkCore.DbContext` 클래스에서 파생시키는 방식으로 이 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5c2f0-142">You create this class by deriving from the `Microsoft.EntityFrameworkCore.DbContext` class.</span></span>

<span data-ttu-id="5c2f0-143">*Models* 폴더에 `TodoContext` 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5c2f0-143">Add a `TodoContext` class in the *Models* folder:</span></span>

[!code-csharp[Main](first-web-api/sample/TodoApi/Models/TodoContext.cs)]

[!INCLUDE[Register the database context](../includes/webApi/register_dbContext.md)]

## <a name="add-a-controller"></a><span data-ttu-id="5c2f0-144">컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="5c2f0-144">Add a controller</span></span>

<span data-ttu-id="5c2f0-145">*Controllers* 폴더에 `TodoController`라는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5c2f0-145">In the *Controllers* folder, create a class named `TodoController`.</span></span> <span data-ttu-id="5c2f0-146">다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5c2f0-146">Add the following code:</span></span>

[!INCLUDE[code and get todo items](../includes/webApi/getTodoItems.md)]

### <a name="launch-the-app"></a><span data-ttu-id="5c2f0-147">앱 시작</span><span class="sxs-lookup"><span data-stu-id="5c2f0-147">Launch the app</span></span>

<span data-ttu-id="5c2f0-148">VS Code에서 F5 키를 눌러 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5c2f0-148">In VS Code, press F5 to launch the app.</span></span> <span data-ttu-id="5c2f0-149">http://localhost:5000/api/할 일로 이동합니다(방금 만든 `Todo` 컨트롤러).</span><span class="sxs-lookup"><span data-stu-id="5c2f0-149">Navigate to  http://localhost:5000/api/todo   (The `Todo` controller we just created).</span></span>

[!INCLUDE[last part of web API](../includes/webApi/end.md)]

## <a name="visual-studio-code-help"></a><span data-ttu-id="5c2f0-150">Visual Studio Code 도움말</span><span class="sxs-lookup"><span data-stu-id="5c2f0-150">Visual Studio Code help</span></span>

- [<span data-ttu-id="5c2f0-151">시작</span><span class="sxs-lookup"><span data-stu-id="5c2f0-151">Getting started</span></span>](https://code.visualstudio.com/docs)
- [<span data-ttu-id="5c2f0-152">디버깅</span><span class="sxs-lookup"><span data-stu-id="5c2f0-152">Debugging</span></span>](https://code.visualstudio.com/docs/editor/debugging)
- [<span data-ttu-id="5c2f0-153">통합 터미널</span><span class="sxs-lookup"><span data-stu-id="5c2f0-153">Integrated terminal</span></span>](https://code.visualstudio.com/docs/editor/integrated-terminal)
- [<span data-ttu-id="5c2f0-154">바로 가기 키</span><span class="sxs-lookup"><span data-stu-id="5c2f0-154">Keyboard shortcuts</span></span>](https://code.visualstudio.com/docs/getstarted/keybindings#_keyboard-shortcuts-reference)

  - [<span data-ttu-id="5c2f0-155">Mac 바로 가기 키</span><span class="sxs-lookup"><span data-stu-id="5c2f0-155">Mac keyboard shortcuts</span></span>](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-macos.pdf)
  - [<span data-ttu-id="5c2f0-156">Linux 바로 가기 키</span><span class="sxs-lookup"><span data-stu-id="5c2f0-156">Linux keyboard shortcuts</span></span>](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-linux.pdf)
  - [<span data-ttu-id="5c2f0-157">Windows 바로 가기 키</span><span class="sxs-lookup"><span data-stu-id="5c2f0-157">Windows keyboard shortcuts</span></span>](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-windows.pdf)

[!INCLUDE[next steps](../includes/webApi/next.md)]


