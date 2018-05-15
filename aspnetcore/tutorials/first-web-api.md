---
title: ASP.NET Core 및 Windows용 Visual Studio를 사용하여 Web API 만들기
author: rick-anderson
description: ASP.NET Core MVC 및 Windows용 Visual Studio를 사용하여 Web API 빌드
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 04/27/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: tutorials/first-web-api
ms.openlocfilehash: 962c24a7e654328df7e8893e589e45b19e87b931
ms.sourcegitcommit: 5130b3034165f5cf49d829fe7475a84aa33d2693
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="create-a-web-api-with-aspnet-core-and-visual-studio-for-windows"></a><span data-ttu-id="30d50-103">ASP.NET Core 및 Windows용 Visual Studio를 사용하여 Web API 만들기</span><span class="sxs-lookup"><span data-stu-id="30d50-103">Create a Web API with ASP.NET Core and Visual Studio for Windows</span></span>

<span data-ttu-id="30d50-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Mike Wasson](https://github.com/mikewasson)</span><span class="sxs-lookup"><span data-stu-id="30d50-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Mike Wasson](https://github.com/mikewasson)</span></span>

::: moniker range="= aspnetcore-2.1"
[!INCLUDE[](~/includes/2.1.md)]
::: moniker-end

<span data-ttu-id="30d50-106">이 자습서에서는 “할 일” 항목 목록을 관리하기 위한 웹 API를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="30d50-106">This tutorial builds a web API for managing a list of "to-do" items.</span></span> <span data-ttu-id="30d50-107">UI(사용자 인터페이스)는 만들어지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30d50-107">A user interface (UI) isn't created.</span></span>

<span data-ttu-id="30d50-108">이 자습서는 다음 세 가지 버전으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="30d50-108">There are three versions of this tutorial:</span></span>

* <span data-ttu-id="30d50-109">Windows: Windows용 Visual Studio를 사용한 Web API(이 자습서)</span><span class="sxs-lookup"><span data-stu-id="30d50-109">Windows: Web API with Visual Studio for Windows (This tutorial)</span></span>
* <span data-ttu-id="30d50-110">macOS: [Mac용 Visual Studio를 사용한 Web API](xref:tutorials/first-web-api-mac)</span><span class="sxs-lookup"><span data-stu-id="30d50-110">macOS: [Web API with Visual Studio for Mac](xref:tutorials/first-web-api-mac)</span></span>
* <span data-ttu-id="30d50-111">macOS, Linux, Windows: [Visual Studio Code를 사용한 Web API](xref:tutorials/web-api-vsc)</span><span class="sxs-lookup"><span data-stu-id="30d50-111">macOS, Linux, Windows: [Web API with Visual Studio Code](xref:tutorials/web-api-vsc)</span></span>

<!-- WARNING: The code AND images in this doc are used by uid: tutorials/web-api-vsc, tutorials/first-web-api-mac and tutorials/first-web-api. If you change any code/images in this tutorial, update uid: tutorials/web-api-vsc -->

[!INCLUDE[intro to web API](../includes/webApi/intro.md)]

## <a name="prerequisites"></a><span data-ttu-id="30d50-112">전제 조건</span><span class="sxs-lookup"><span data-stu-id="30d50-112">Prerequisites</span></span>

[!INCLUDE[](~/includes/net-core-prereqs-windows.md)]

## <a name="create-the-project"></a><span data-ttu-id="30d50-113">프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30d50-113">Create the project</span></span>

<span data-ttu-id="30d50-114">Visual Studio에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="30d50-114">Follow these steps in Visual Studio:</span></span>

* <span data-ttu-id="30d50-115">**파일** 메뉴에서 **새로 만들기** > **프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="30d50-115">From the **File** menu, select **New** > **Project**.</span></span>
* <span data-ttu-id="30d50-116">**ASP.NET Core 웹 응용 프로그램** 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="30d50-116">Select the **ASP.NET Core Web Application** template.</span></span> <span data-ttu-id="30d50-117">프로젝트 이름을 *TodoApi*로 지정하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30d50-117">Name the project *TodoApi* and click **OK**.</span></span>
* <span data-ttu-id="30d50-118">**새 ASP.NET Core 웹 응용 프로그램 - TodoApi** 대화 상자에서 ASP.NET Core 버전을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="30d50-118">In the **New ASP.NET Core Web Application - TodoApi** dialog, choose the ASP.NET Core version.</span></span> <span data-ttu-id="30d50-119">**API** 템플릿을 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30d50-119">Select the **API** template and click **OK**.</span></span> <span data-ttu-id="30d50-120">**Docker 지원 사용**을 선택하지 **마세요**.</span><span class="sxs-lookup"><span data-stu-id="30d50-120">Do **not** select **Enable Docker Support**.</span></span>

### <a name="launch-the-app"></a><span data-ttu-id="30d50-121">앱 시작</span><span class="sxs-lookup"><span data-stu-id="30d50-121">Launch the app</span></span>

<span data-ttu-id="30d50-122">Visual Studio에서 CTRL+F5를 눌러 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="30d50-122">In Visual Studio, press CTRL+F5 to launch the app.</span></span> <span data-ttu-id="30d50-123">Visual Studio가 브라우저를 시작하고 `http://localhost:<port>/api/values`로 이동합니다. 여기서 `<port>`는 임의로 선택된 포트 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="30d50-123">Visual Studio launches a browser and navigates to `http://localhost:<port>/api/values`, where `<port>` is a randomly chosen port number.</span></span> <span data-ttu-id="30d50-124">Chrome, Microsoft Edge 및 Firefox에는 다음 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="30d50-124">Chrome, Microsoft Edge, and Firefox display the following output:</span></span>

```json
["value1","value2"]
```

### <a name="add-a-model-class"></a><span data-ttu-id="30d50-125">모델 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="30d50-125">Add a model class</span></span>

<span data-ttu-id="30d50-126">모델은 앱의 데이터를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="30d50-126">A model is an object representing the data in the app.</span></span> <span data-ttu-id="30d50-127">이 경우 유일한 모델은 할 일 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="30d50-127">In this case, the only model is a to-do item.</span></span>

<span data-ttu-id="30d50-128">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30d50-128">In Solution Explorer, right-click the project.</span></span> <span data-ttu-id="30d50-129">**추가** > **새 폴더**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="30d50-129">Select **Add** > **New Folder**.</span></span> <span data-ttu-id="30d50-130">폴더 이름을 *Models*로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="30d50-130">Name the folder *Models*.</span></span>

> [!NOTE]
> <span data-ttu-id="30d50-131">모델 클래스는 프로젝트의 어디에서나 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30d50-131">The model classes can go anywhere in the project.</span></span> <span data-ttu-id="30d50-132">*Models* 폴더는 모델 클래스에 대한 규칙에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="30d50-132">The *Models* folder is used by convention for model classes.</span></span>

<span data-ttu-id="30d50-133">솔루션 탐색기에서 *Models* 폴더를 마우스 오른쪽 단추로 클릭하고 **추가** > **클래스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="30d50-133">In Solution Explorer, right-click the *Models* folder and select **Add** > **Class**.</span></span> <span data-ttu-id="30d50-134">클래스 이름을 *TodoItem*으로 지정하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30d50-134">Name the class *TodoItem* and click **Add**.</span></span>

<span data-ttu-id="30d50-135">`TodoItem` 클래스를 다음 코드로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="30d50-135">Update the `TodoItem` class with the following code:</span></span>

[!code-csharp[](first-web-api/samples/2.0/TodoApi/Models/TodoItem.cs)]

<span data-ttu-id="30d50-136">`TodoItem`이 만들어질 때 데이터베이스가 `Id`를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="30d50-136">The database generates the `Id` when a `TodoItem` is created.</span></span>

### <a name="create-the-database-context"></a><span data-ttu-id="30d50-137">데이터베이스 컨텍스트 만들기</span><span class="sxs-lookup"><span data-stu-id="30d50-137">Create the database context</span></span>

<span data-ttu-id="30d50-138">*데이터베이스 컨텍스트*는 특정 데이터 모델에 맞게 Entity Framework 기능을 조정하는 주 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="30d50-138">The *database context* is the main class that coordinates Entity Framework functionality for a given data model.</span></span> <span data-ttu-id="30d50-139">`Microsoft.EntityFrameworkCore.DbContext` 클래스에서 파생시키는 방식으로 이 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30d50-139">This class is created by deriving from the `Microsoft.EntityFrameworkCore.DbContext` class.</span></span>

<span data-ttu-id="30d50-140">솔루션 탐색기에서 *Models* 폴더를 마우스 오른쪽 단추로 클릭하고 **추가** > **클래스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="30d50-140">In Solution Explorer, right-click the *Models* folder and select **Add** > **Class**.</span></span> <span data-ttu-id="30d50-141">클래스 이름을 *TodoContext*로 지정하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30d50-141">Name the class *TodoContext* and click **Add**.</span></span>

<span data-ttu-id="30d50-142">클래스를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="30d50-142">Replace the class with the following code:</span></span>

[!code-csharp[](first-web-api/samples/2.0/TodoApi/Models/TodoContext.cs)]

[!INCLUDE [Register the database context](../includes/webApi/register_dbContext.md)]

### <a name="add-a-controller"></a><span data-ttu-id="30d50-143">컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="30d50-143">Add a controller</span></span>

<span data-ttu-id="30d50-144">솔루션 탐색기에서 *Controllers* 폴더를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30d50-144">In Solution Explorer, right-click the *Controllers* folder.</span></span> <span data-ttu-id="30d50-145">**추가** > **새 항목**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="30d50-145">Select **Add** > **New Item**.</span></span> <span data-ttu-id="30d50-146">**새 항목 추가** 대화 상자에서 **API 컨트롤러 클래스** 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="30d50-146">In the **Add New Item** dialog, select the **API Controller Class** template.</span></span> <span data-ttu-id="30d50-147">클래스 이름을 *TodoController*로 지정하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30d50-147">Name the class *TodoController*, and click **Add**.</span></span>

![검색 상자의 컨트롤러 및 Web API 컨트롤러가 선택된 새 항목 추가 대화 상자](first-web-api/_static/new_controller.png)

<span data-ttu-id="30d50-149">클래스를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="30d50-149">Replace the class with the following code:</span></span>

[!INCLUDE[code and get todo items](../includes/webApi/getTodoItems.md)]

### <a name="launch-the-app"></a><span data-ttu-id="30d50-150">앱 시작</span><span class="sxs-lookup"><span data-stu-id="30d50-150">Launch the app</span></span>

<span data-ttu-id="30d50-151">Visual Studio에서 CTRL+F5를 눌러 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="30d50-151">In Visual Studio, press CTRL+F5 to launch the app.</span></span> <span data-ttu-id="30d50-152">Visual Studio가 브라우저를 시작하고 `http://localhost:<port>/api/values`로 이동합니다. 여기서 `<port>`는 임의로 선택된 포트 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="30d50-152">Visual Studio launches a browser and navigates to `http://localhost:<port>/api/values`, where `<port>` is a randomly chosen port number.</span></span> <span data-ttu-id="30d50-153">`http://localhost:<port>/api/todo`의 `Todo` 컨트롤러로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="30d50-153">Navigate to the `Todo` controller at `http://localhost:<port>/api/todo`.</span></span>

[!INCLUDE[last part of web API](../includes/webApi/end.md)]

[!INCLUDE[jQuery](../includes/webApi/add-jquery.md)]

[!INCLUDE[next steps](../includes/webApi/next.md)]
