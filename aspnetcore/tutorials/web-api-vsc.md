---
title: ASP.NET Core 및 Visual Studio Code를 사용하여 Web API 만들기
author: rick-anderson
description: ASP.NET Core MVC 및 Visual Studio Code를 사용하여 macOS, Linux 또는 Windows에서 웹 API 빌드
ms.author: riande
ms.custom: mvc
ms.date: 07/30/2018
uid: tutorials/web-api-vsc
ms.openlocfilehash: 740110908358a382f20bc1e54e98056296278acf
ms.sourcegitcommit: 4d74644f11e0dac52b4510048490ae731c691496
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50089666"
---
# <a name="create-a-web-api-with-aspnet-core-and-visual-studio-code"></a><span data-ttu-id="29e5d-103">ASP.NET Core 및 Visual Studio Code를 사용하여 Web API 만들기</span><span class="sxs-lookup"><span data-stu-id="29e5d-103">Create a Web API with ASP.NET Core and Visual Studio Code</span></span>

<span data-ttu-id="29e5d-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Mike Wasson](https://github.com/mikewasson)</span><span class="sxs-lookup"><span data-stu-id="29e5d-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Mike Wasson](https://github.com/mikewasson)</span></span>

<span data-ttu-id="29e5d-105">이 자습서에서는 “할 일” 항목 목록을 관리하기 위한 웹 API를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="29e5d-105">In this tutorial, build a web API for managing a list of "to-do" items.</span></span> <span data-ttu-id="29e5d-106">UI는 생성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="29e5d-106">A UI isn't constructed.</span></span>

<span data-ttu-id="29e5d-107">이 자습서는 다음 세 가지 버전으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="29e5d-107">There are three versions of this tutorial:</span></span>

* <span data-ttu-id="29e5d-108">macOS, Linux, Windows: Visual Studio Code를 사용한 Web API(이 자습서)</span><span class="sxs-lookup"><span data-stu-id="29e5d-108">macOS, Linux, Windows: Web API with Visual Studio Code (This tutorial)</span></span>
* <span data-ttu-id="29e5d-109">macOS: [Mac용 Visual Studio를 사용한 Web API](xref:tutorials/first-web-api-mac)</span><span class="sxs-lookup"><span data-stu-id="29e5d-109">macOS: [Web API with Visual Studio for Mac](xref:tutorials/first-web-api-mac)</span></span>
* <span data-ttu-id="29e5d-110">Windows: [Windows용 Visual Studio를 사용한 Web API](xref:tutorials/first-web-api)</span><span class="sxs-lookup"><span data-stu-id="29e5d-110">Windows: [Web API with Visual Studio for Windows](xref:tutorials/first-web-api)</span></span>

<!-- WARNING: The code AND images in this doc are used by uid: tutorials/web-api-vsc, tutorials/first-web-api-mac and tutorials/first-web-api. If you change any code/images in this tutorial, update uid: tutorials/web-api-vsc -->

[!INCLUDE[template files](../includes/webApi/intro.md)]

## <a name="prerequisites"></a><span data-ttu-id="29e5d-111">전제 조건</span><span class="sxs-lookup"><span data-stu-id="29e5d-111">Prerequisites</span></span>

[!INCLUDE[prerequisites](~/includes/net-core-prereqs-vscode.md)]

<span data-ttu-id="29e5d-112">VS Code 사용에 대한 팁은 [Visual Studio Code 도움말](#visual-studio-code-help)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="29e5d-112">See [Visual Studio Code help](#visual-studio-code-help) for tips on using VS Code.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="29e5d-113">프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="29e5d-113">Create the project</span></span>

<span data-ttu-id="29e5d-114">콘솔에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="29e5d-114">From a console, run the following commands:</span></span>

```console
dotnet new webapi -o TodoApi
code TodoApi
```

<span data-ttu-id="29e5d-115">*TodoApi* 폴더가 VS Code(Visual Studio Code)에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="29e5d-115">The *TodoApi* folder opens in Visual Studio Code (VS Code).</span></span> <span data-ttu-id="29e5d-116">*Startup.cs* 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="29e5d-116">Select the *Startup.cs* file.</span></span>

* <span data-ttu-id="29e5d-117">다음 **경고** 메시지에 대해 **예**를 선택합니다. “빌드 및 디버그에 필요한 자산이 ‘TodoApi’에서 누락되었습니다.</span><span class="sxs-lookup"><span data-stu-id="29e5d-117">Select **Yes** to the **Warn** message "Required assets to build and debug are missing from 'TodoApi'.</span></span> <span data-ttu-id="29e5d-118">추가할까요?”</span><span class="sxs-lookup"><span data-stu-id="29e5d-118">Add them?"</span></span>
* <span data-ttu-id="29e5d-119">다음 **정보** 메시지에 대해 **복원**을 선택합니다. “확인되지 않은 종속성이 있습니다.”</span><span class="sxs-lookup"><span data-stu-id="29e5d-119">Select **Restore** to the **Info** message "There are unresolved dependencies".</span></span>

<!-- uid: tutorials/first-mvc-app-xplat/start-mvc uses the pic below. If you change it, make sure it's consistent -->

![빌드 및 디버그에 필요한 자산이 ‘TodoApi’에서 누락되었습니다. 경고가 있는 VS Code](web-api-vsc/_static/vsc_restore.png)

<span data-ttu-id="29e5d-123">**디버그**(F5) 키를 눌러 프로그램을 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="29e5d-123">Press **Debug** (F5) to build and run the program.</span></span> <span data-ttu-id="29e5d-124">브라우저에서 http://localhost:5000/api/values로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="29e5d-124">In a browser, navigate to http://localhost:5000/api/values.</span></span> <span data-ttu-id="29e5d-125">다음 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="29e5d-125">The following output is displayed:</span></span>

```json
["value1","value2"]
```



## <a name="add-support-for-entity-framework-core"></a><span data-ttu-id="29e5d-126">Entity Framework Core에 대한 지원 추가</span><span class="sxs-lookup"><span data-stu-id="29e5d-126">Add support for Entity Framework Core</span></span>

:::moniker range=">= aspnetcore-2.1"

<span data-ttu-id="29e5d-127">ASP.NET Core 2.1 이상에서 새 프로젝트를 만들면 [Microsoft.AspNetCore.App 메타패키지](xref:fundamentals/metapackage-app)가 프로젝트 파일에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="29e5d-127">Creating a new project in ASP.NET Core 2.1 or later adds the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) to the project file:</span></span>

[!code-xml[](first-web-api/samples/2.1/TodoApi/TodoApi.csproj?name=snippet_Metapackage&highlight=2)]

:::moniker-end

:::moniker range="<= aspnetcore-2.0"

<span data-ttu-id="29e5d-128">ASP.NET Core 2.0에서 새 프로젝트를 만들면 [Microsoft.AspNetCore.All 메타패키지](xref:fundamentals/metapackage)가 프로젝트 파일에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="29e5d-128">Creating a new project in ASP.NET Core 2.0 adds the [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage) to the project file:</span></span>

[!code-xml[](first-web-api/samples/2.0/TodoApi/TodoApi.csproj?name=snippet_Metapackage&highlight=2)]

:::moniker-end

<span data-ttu-id="29e5d-129">[Entity Framework Core InMemory](/ef/core/providers/in-memory/) 데이터베이스 공급자를 별도로 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="29e5d-129">There's no need to install the [Entity Framework Core InMemory](/ef/core/providers/in-memory/) database provider separately.</span></span> <span data-ttu-id="29e5d-130">이 데이터베이스 공급자를 설치하면 Entity Framework Core를 메모리 내 데이터베이스에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29e5d-130">This database provider allows Entity Framework Core to be used with an in-memory database.</span></span>

## <a name="add-a-model-class"></a><span data-ttu-id="29e5d-131">모델 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="29e5d-131">Add a model class</span></span>

<span data-ttu-id="29e5d-132">모델은 앱에서 데이터를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="29e5d-132">A model is an object representing the data in your app.</span></span> <span data-ttu-id="29e5d-133">이 경우 유일한 모델은 할 일 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="29e5d-133">In this case, the only model is a to-do item.</span></span>

<span data-ttu-id="29e5d-134">*Models* 폴더를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="29e5d-134">Add a folder named *Models*.</span></span> <span data-ttu-id="29e5d-135">프로젝트의 아무 곳에나 모델 클래스를 넣을 수 있지만 일반적으로 *Models* 폴더를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="29e5d-135">You can put model classes anywhere in your project, but the *Models* folder is used by convention.</span></span>

<span data-ttu-id="29e5d-136">`TodoItem` 클래스를 다음 코드로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="29e5d-136">Add a `TodoItem` class with the following code:</span></span>

[!code-csharp[](first-web-api/samples/2.0/TodoApi/Models/TodoItem.cs)]

<span data-ttu-id="29e5d-137">`TodoItem`이 만들어질 때 데이터베이스가 `Id`를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="29e5d-137">The database generates the `Id` when a `TodoItem` is created.</span></span>

## <a name="create-the-database-context"></a><span data-ttu-id="29e5d-138">데이터베이스 컨텍스트 만들기</span><span class="sxs-lookup"><span data-stu-id="29e5d-138">Create the database context</span></span>

<span data-ttu-id="29e5d-139">*데이터베이스 컨텍스트*는 특정 데이터 모델에 맞게 Entity Framework 기능을 조정하는 주 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="29e5d-139">The *database context* is the main class that coordinates Entity Framework functionality for a given data model.</span></span> <span data-ttu-id="29e5d-140">`Microsoft.EntityFrameworkCore.DbContext` 클래스에서 파생시키는 방식으로 이 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="29e5d-140">You create this class by deriving from the `Microsoft.EntityFrameworkCore.DbContext` class.</span></span>

<span data-ttu-id="29e5d-141">*Models* 폴더에 `TodoContext` 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="29e5d-141">Add a `TodoContext` class in the *Models* folder:</span></span>

[!code-csharp[](first-web-api/samples/2.0/TodoApi/Models/TodoContext.cs)]

[!INCLUDE[Register the database context](../includes/webApi/register_dbContext.md)]

## <a name="add-a-controller"></a><span data-ttu-id="29e5d-142">컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="29e5d-142">Add a controller</span></span>

<span data-ttu-id="29e5d-143">*Controllers* 폴더에 `TodoController`라는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="29e5d-143">In the *Controllers* folder, create a class named `TodoController`.</span></span> <span data-ttu-id="29e5d-144">다음 코드로 콘텐츠를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="29e5d-144">Replace its contents with the following code:</span></span>

[!INCLUDE[code and get todo items](../includes/webApi/getTodoItems.md)]

### <a name="launch-the-app"></a><span data-ttu-id="29e5d-145">앱 시작</span><span class="sxs-lookup"><span data-stu-id="29e5d-145">Launch the app</span></span>

<span data-ttu-id="29e5d-146">VS Code에서 F5 키를 눌러 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="29e5d-146">In VS Code, press F5 to launch the app.</span></span> <span data-ttu-id="29e5d-147">http://localhost:5000/api/todo(만든 `Todo` 컨트롤러)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="29e5d-147">Navigate to http://localhost:5000/api/todo (the `Todo` controller we created).</span></span>

[!INCLUDE[jQuery](../includes/webApi/add-jquery.md)]

[!INCLUDE[last part of web API](../includes/webApi/end.md)]

## <a name="visual-studio-code-help"></a><span data-ttu-id="29e5d-148">Visual Studio Code 도움말</span><span class="sxs-lookup"><span data-stu-id="29e5d-148">Visual Studio Code help</span></span>

* [<span data-ttu-id="29e5d-149">시작</span><span class="sxs-lookup"><span data-stu-id="29e5d-149">Getting started</span></span>](https://code.visualstudio.com/docs)
* [<span data-ttu-id="29e5d-150">디버깅</span><span class="sxs-lookup"><span data-stu-id="29e5d-150">Debugging</span></span>](https://code.visualstudio.com/docs/editor/debugging)
* [<span data-ttu-id="29e5d-151">통합 터미널</span><span class="sxs-lookup"><span data-stu-id="29e5d-151">Integrated terminal</span></span>](https://code.visualstudio.com/docs/editor/integrated-terminal)
* [<span data-ttu-id="29e5d-152">바로 가기 키</span><span class="sxs-lookup"><span data-stu-id="29e5d-152">Keyboard shortcuts</span></span>](https://code.visualstudio.com/docs/getstarted/keybindings#_keyboard-shortcuts-reference)

  * [<span data-ttu-id="29e5d-153">macOS 바로 가기 키</span><span class="sxs-lookup"><span data-stu-id="29e5d-153">macOS keyboard shortcuts</span></span>](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-macos.pdf)
  * [<span data-ttu-id="29e5d-154">Linux 바로 가기 키</span><span class="sxs-lookup"><span data-stu-id="29e5d-154">Linux keyboard shortcuts</span></span>](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-linux.pdf)
  * [<span data-ttu-id="29e5d-155">Windows 바로 가기 키</span><span class="sxs-lookup"><span data-stu-id="29e5d-155">Windows keyboard shortcuts</span></span>](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-windows.pdf)

[!INCLUDE[next steps](../includes/webApi/next.md)]
