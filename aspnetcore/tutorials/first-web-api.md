---
title: "ASP.NET Core 및 Windows용 Visual Studio를 사용하여 Web API 만들기"
author: rick-anderson
description: "ASP.NET Core MVC 및 Windows용 Visual Studio를 사용하여 Web API 빌드"
manager: wpickett
ms.author: riande
ms.date: 08/15/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: tutorials/first-web-api
ms.openlocfilehash: 1146132693681eca8f92beb00ebabd7296534688
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
#<a name="create-a-web-api-with-aspnet-core-and-visual-studio-for-windows"></a><span data-ttu-id="61ca3-103">ASP.NET Core 및 Windows용 Visual Studio를 사용하여 Web API 만들기</span><span class="sxs-lookup"><span data-stu-id="61ca3-103">Create a web API with ASP.NET Core and Visual Studio for Windows</span></span>

<span data-ttu-id="61ca3-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Mike Wasson](https://github.com/mikewasson)</span><span class="sxs-lookup"><span data-stu-id="61ca3-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Mike Wasson](https://github.com/mikewasson)</span></span>

<span data-ttu-id="61ca3-105">이 자습서에서는 “할 일” 항목 목록을 관리하기 위한 웹 API를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="61ca3-105">This tutorial builds a web API for managing a list of "to-do" items.</span></span> <span data-ttu-id="61ca3-106">UI(사용자 인터페이스)는 만들어지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="61ca3-106">A user interface (UI) isn't created.</span></span>

<span data-ttu-id="61ca3-107">이 자습서는 세 가지 버전이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61ca3-107">There are 3 versions of this tutorial:</span></span>

* <span data-ttu-id="61ca3-108">Windows: Windows용 Visual Studio를 사용한 Web API(이 자습서)</span><span class="sxs-lookup"><span data-stu-id="61ca3-108">Windows: Web API with Visual Studio for Windows (This tutorial)</span></span>
* <span data-ttu-id="61ca3-109">macOS: [Mac용 Visual Studio를 사용한 Web API](xref:tutorials/first-web-api-mac)</span><span class="sxs-lookup"><span data-stu-id="61ca3-109">macOS: [Web API with Visual Studio for Mac](xref:tutorials/first-web-api-mac)</span></span>
* <span data-ttu-id="61ca3-110">macOS, Linux, Windows: [Visual Studio Code를 사용한 Web API](xref:tutorials/web-api-vsc)</span><span class="sxs-lookup"><span data-stu-id="61ca3-110">macOS, Linux, Windows: [Web API with Visual Studio Code](xref:tutorials/web-api-vsc)</span></span>

<!-- WARNING: The code AND images in this doc are used by uid: tutorials/web-api-vsc, tutorials/first-web-api-mac and tutorials/first-web-api. If you change any code/images in this tutorial, update uid: tutorials/web-api-vsc -->

[!INCLUDE[intro to web API](../includes/webApi/intro.md)]

## <a name="prerequisites"></a><span data-ttu-id="61ca3-111">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="61ca3-111">Prerequisites</span></span>

[!INCLUDE[install 2.0](../includes/install2.0.md)]

<span data-ttu-id="61ca3-112">ASP.NET Core 1.1 버전에 대해서는 [이 PDF](https://github.com/aspnet/Docs/blob/master/aspnetcore/tutorials/first-web-api/_static/_webAPI.pdf)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="61ca3-112">See [this PDF](https://github.com/aspnet/Docs/blob/master/aspnetcore/tutorials/first-web-api/_static/_webAPI.pdf) for the ASP.NET Core 1.1 version.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="61ca3-113">프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="61ca3-113">Create the project</span></span>

<span data-ttu-id="61ca3-114">Visual Studio에서 **파일** 메뉴 > **새로 만들기** > **프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="61ca3-114">From Visual Studio, select **File** menu, > **New** > **Project**.</span></span>

<span data-ttu-id="61ca3-115">**ASP.NET Core 웹 응용 프로그램(.NET Core)** 프로젝트 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="61ca3-115">Select the **ASP.NET Core Web Application (.NET Core)** project template.</span></span> <span data-ttu-id="61ca3-116">프로젝트 이름을 `TodoApi`로 지정하고 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="61ca3-116">Name the project `TodoApi` and select **OK**.</span></span>

![새 프로젝트 대화 상자](first-web-api/_static/new-project.png)

<span data-ttu-id="61ca3-118">**새 ASP.NET Core 웹 응용 프로그램 - TodoApi** 대화 상자에서 **Web API** 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="61ca3-118">In the **New ASP.NET Core Web Application - TodoApi** dialog, select the **Web API** template.</span></span> <span data-ttu-id="61ca3-119">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="61ca3-119">Select **OK**.</span></span> <span data-ttu-id="61ca3-120">**Docker 지원 사용**을 선택하지 **마세요**.</span><span class="sxs-lookup"><span data-stu-id="61ca3-120">Do **not** select **Enable Docker Support**.</span></span>

![ASP.NET Core 템플릿에서 Web API 프로젝트 템플릿이 선택된 새 ASP.NET 웹 응용 프로그램 대화 상자](first-web-api/_static/web-api-project.png)

### <a name="launch-the-app"></a><span data-ttu-id="61ca3-122">앱 시작</span><span class="sxs-lookup"><span data-stu-id="61ca3-122">Launch the app</span></span>

<span data-ttu-id="61ca3-123">Visual Studio에서 CTRL+F5를 눌러 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="61ca3-123">In Visual Studio, press CTRL+F5 to launch the app.</span></span> <span data-ttu-id="61ca3-124">Visual Studio가 브라우저를 시작하고 `http://localhost:port/api/values`로 이동합니다. 여기서 *port*는 임의로 선택된 포트 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="61ca3-124">Visual Studio launches a browser and navigates to `http://localhost:port/api/values`, where *port* is a randomly chosen port number.</span></span> <span data-ttu-id="61ca3-125">Chrome, Microsoft Edge 및 Firefox에는 다음 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="61ca3-125">Chrome, Microsoft Edge, and Firefox display the following output:</span></span>

```
["value1","value2"]
```

### <a name="add-a-model-class"></a><span data-ttu-id="61ca3-126">모델 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="61ca3-126">Add a model class</span></span>

<span data-ttu-id="61ca3-127">모델은 앱에서 데이터를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="61ca3-127">A model is an object that represents the data in the app.</span></span> <span data-ttu-id="61ca3-128">이 경우 유일한 모델은 할 일 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="61ca3-128">In this case, the only model is a to-do item.</span></span>

<span data-ttu-id="61ca3-129">“Models” 폴더를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="61ca3-129">Add a folder named "Models".</span></span> <span data-ttu-id="61ca3-130">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="61ca3-130">In Solution Explorer, right-click the project.</span></span> <span data-ttu-id="61ca3-131">**추가** > **새 폴더**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="61ca3-131">Select **Add** > **New Folder**.</span></span> <span data-ttu-id="61ca3-132">폴더 이름을 *Models*로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="61ca3-132">Name the folder *Models*.</span></span>

<span data-ttu-id="61ca3-133">참고: 모델 클래스는 프로젝트의 어디에서나 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61ca3-133">Note: The model classes go anywhere in the project.</span></span> <span data-ttu-id="61ca3-134">*Models* 폴더는 모델 클래스에 대한 규칙에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="61ca3-134">The *Models* folder is used by convention for model classes.</span></span>

<span data-ttu-id="61ca3-135">`TodoItem` 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="61ca3-135">Add a `TodoItem` class.</span></span> <span data-ttu-id="61ca3-136">*Models* 폴더를 마우스 오른쪽 단추로 클릭하고 **추가** > **클래스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="61ca3-136">Right-click the *Models* folder and select **Add** > **Class**.</span></span> <span data-ttu-id="61ca3-137">클래스 이름을 `TodoItem`로 지정하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="61ca3-137">Name the class `TodoItem` and select **Add**.</span></span>

<span data-ttu-id="61ca3-138">`TodoItem` 클래스를 다음 코드로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="61ca3-138">Update the `TodoItem` class with the following code:</span></span>

[!code-csharp[Main](first-web-api/sample/TodoApi/Models/TodoItem.cs)]

<span data-ttu-id="61ca3-139">`TodoItem`이 만들어질 때 데이터베이스가 `Id`를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="61ca3-139">The database generates the `Id` when a `TodoItem` is created.</span></span>

### <a name="create-the-database-context"></a><span data-ttu-id="61ca3-140">데이터베이스 컨텍스트 만들기</span><span class="sxs-lookup"><span data-stu-id="61ca3-140">Create the database context</span></span>

<span data-ttu-id="61ca3-141">*데이터베이스 컨텍스트*는 특정 데이터 모델에 맞게 Entity Framework 기능을 조정하는 주 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="61ca3-141">The *database context* is the main class that coordinates Entity Framework functionality for a given data model.</span></span> <span data-ttu-id="61ca3-142">`Microsoft.EntityFrameworkCore.DbContext` 클래스에서 파생시키는 방식으로 이 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="61ca3-142">This class is created by deriving from the `Microsoft.EntityFrameworkCore.DbContext` class.</span></span>

<span data-ttu-id="61ca3-143">`TodoContext` 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="61ca3-143">Add a `TodoContext` class.</span></span> <span data-ttu-id="61ca3-144">*Models* 폴더를 마우스 오른쪽 단추로 클릭하고 **추가** > **클래스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="61ca3-144">Right-click the *Models* folder and select **Add** > **Class**.</span></span> <span data-ttu-id="61ca3-145">클래스 이름을 `TodoContext`로 지정하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="61ca3-145">Name the class `TodoContext` and select **Add**.</span></span>

<span data-ttu-id="61ca3-146">클래스를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="61ca3-146">Replace the class with the following code:</span></span>

[!code-csharp[Main](first-web-api/sample/TodoApi/Models/TodoContext.cs)]

[!INCLUDE[Register the database context](../includes/webApi/register_dbContext.md)]

### <a name="add-a-controller"></a><span data-ttu-id="61ca3-147">컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="61ca3-147">Add a controller</span></span>

<span data-ttu-id="61ca3-148">솔루션 탐색기에서 *Controllers* 폴더를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="61ca3-148">In Solution Explorer, right-click the *Controllers* folder.</span></span> <span data-ttu-id="61ca3-149">**추가** > **새 항목**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="61ca3-149">Select **Add** > **New Item**.</span></span> <span data-ttu-id="61ca3-150">**새 항목 추가** 대화 상자에서 **Web API 컨트롤러 클래스** 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="61ca3-150">In the **Add New Item** dialog, select the **Web API Controller Class** template.</span></span> <span data-ttu-id="61ca3-151">클래스 이름을 `TodoController`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="61ca3-151">Name the class `TodoController`.</span></span>

![검색 상자의 컨트롤러 및 Web API 컨트롤러가 선택된 새 항목 추가 대화 상자](first-web-api/_static/new_controller.png)

<span data-ttu-id="61ca3-153">클래스를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="61ca3-153">Replace the class with the following code:</span></span>

[!INCLUDE[code and get todo items](../includes/webApi/getTodoItems.md)]

### <a name="launch-the-app"></a><span data-ttu-id="61ca3-154">앱 시작</span><span class="sxs-lookup"><span data-stu-id="61ca3-154">Launch the app</span></span>

<span data-ttu-id="61ca3-155">Visual Studio에서 CTRL+F5를 눌러 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="61ca3-155">In Visual Studio, press CTRL+F5 to launch the app.</span></span> <span data-ttu-id="61ca3-156">Visual Studio가 브라우저를 시작하고 `http://localhost:port/api/values`로 이동합니다. 여기서 *port*는 임의로 선택된 포트 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="61ca3-156">Visual Studio launches a browser and navigates to `http://localhost:port/api/values`, where *port* is a randomly chosen port number.</span></span> <span data-ttu-id="61ca3-157">`http://localhost:port/api/todo`의 `Todo` 컨트롤러로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="61ca3-157">Navigate to the `Todo` controller at `http://localhost:port/api/todo`.</span></span>

[!INCLUDE[last part of web API](../includes/webApi/end.md)]

[!INCLUDE[next steps](../includes/webApi/next.md)]

