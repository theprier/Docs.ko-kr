---
title: ASP.NET Core 및 Visual Studio를 사용하여 Web API 만들기
author: rick-anderson
description: Windows에서 ASP.NET Core MVC 및 Visual Studio를 사용하여 Web API 빌드
ms.author: riande
ms.custom: mvc
ms.date: 05/17/2018
uid: tutorials/first-web-api
ms.openlocfilehash: eb23d5376742e04712f714263815582fddc5d18e
ms.sourcegitcommit: e9b99854b0a8021dafabee0db5e1338067f250a9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52450699"
---
# <a name="create-a-web-api-with-aspnet-core-and-visual-studio"></a><span data-ttu-id="eb4f5-103">ASP.NET Core 및 Visual Studio를 사용하여 Web API 만들기</span><span class="sxs-lookup"><span data-stu-id="eb4f5-103">Create a Web API with ASP.NET Core and Visual Studio</span></span>

<span data-ttu-id="eb4f5-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Mike Wasson](https://github.com/mikewasson)</span><span class="sxs-lookup"><span data-stu-id="eb4f5-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Mike Wasson](https://github.com/mikewasson)</span></span>

<span data-ttu-id="eb4f5-105">이 자습서에서는 “할 일” 항목 목록을 관리하기 위한 웹 API를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="eb4f5-105">This tutorial builds a web API for managing a list of "to-do" items.</span></span> <span data-ttu-id="eb4f5-106">UI(사용자 인터페이스)는 만들어지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eb4f5-106">A user interface (UI) isn't created.</span></span>

<span data-ttu-id="eb4f5-107">이 자습서는 다음 세 가지 버전으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb4f5-107">There are three versions of this tutorial:</span></span>

* <span data-ttu-id="eb4f5-108">Windows: Windows에서 Visual Studio를 사용한 Web API(이 자습서, [비디오 버전](https://www.youtube.com/watch?v=TTkhEyGBfAk) 참조)</span><span class="sxs-lookup"><span data-stu-id="eb4f5-108">Windows: Web API with Visual Studio on Windows (This tutorial, see the [video version](https://www.youtube.com/watch?v=TTkhEyGBfAk))</span></span>
* <span data-ttu-id="eb4f5-109">macOS: [Mac용 Visual Studio를 사용한 Web API](xref:tutorials/first-web-api-mac)</span><span class="sxs-lookup"><span data-stu-id="eb4f5-109">macOS: [Web API with Visual Studio for Mac](xref:tutorials/first-web-api-mac)</span></span>
* <span data-ttu-id="eb4f5-110">macOS, Linux, Windows: [Visual Studio Code를 사용한 Web API](xref:tutorials/web-api-vsc)</span><span class="sxs-lookup"><span data-stu-id="eb4f5-110">macOS, Linux, Windows: [Web API with Visual Studio Code](xref:tutorials/web-api-vsc)</span></span>

<!-- WARNING: The code AND images in this doc are used by uid: tutorials/web-api-vsc, tutorials/first-web-api-mac and tutorials/first-web-api. If you change any code/images in this tutorial, update uid: tutorials/web-api-vsc -->

> [!NOTE]
> <span data-ttu-id="eb4f5-111">ASP.NET Core 목차에 대해 제안된 새 구조의 유용성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="eb4f5-111">We’re testing the usability of a proposed new structure for the ASP.NET Core table of contents.</span></span>  <span data-ttu-id="eb4f5-112">몇 분 동안 현재 또는 제안된 목차에서 다른 7개의 항목을 찾는 연습을 수행하는 경우 [여기를 클릭하여 연구에 참여하세요](https://dpk4xbh5.optimalworkshop.com/treejack/rps16hd5).</span><span class="sxs-lookup"><span data-stu-id="eb4f5-112">If you have a few minutes to try an exercise of finding 7 different topics in the current or proposed table of contents, please [click here to participate in the study](https://dpk4xbh5.optimalworkshop.com/treejack/rps16hd5).</span></span>

[!INCLUDE[intro to web API](../includes/webApi/intro.md)]

## <a name="prerequisites"></a><span data-ttu-id="eb4f5-113">전제 조건</span><span class="sxs-lookup"><span data-stu-id="eb4f5-113">Prerequisites</span></span>

[!INCLUDE[](~/includes/net-core-prereqs-windows.md)]

## <a name="create-the-project"></a><span data-ttu-id="eb4f5-114">프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eb4f5-114">Create the project</span></span>

<span data-ttu-id="eb4f5-115">Visual Studio에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="eb4f5-115">Follow these steps in Visual Studio:</span></span>

* <span data-ttu-id="eb4f5-116">**파일** 메뉴에서 **새로 만들기** > **프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eb4f5-116">From the **File** menu, select **New** > **Project**.</span></span>
* <span data-ttu-id="eb4f5-117">**ASP.NET Core 웹 응용 프로그램** 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eb4f5-117">Select the **ASP.NET Core Web Application** template.</span></span> <span data-ttu-id="eb4f5-118">프로젝트 이름을 *TodoApi*로 지정하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eb4f5-118">Name the project *TodoApi* and click **OK**.</span></span>
* <span data-ttu-id="eb4f5-119">**새 ASP.NET Core 웹 응용 프로그램 - TodoApi** 대화 상자에서 ASP.NET Core 버전을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eb4f5-119">In the **New ASP.NET Core Web Application - TodoApi** dialog, choose the ASP.NET Core version.</span></span> <span data-ttu-id="eb4f5-120">**API** 템플릿을 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eb4f5-120">Select the **API** template and click **OK**.</span></span> <span data-ttu-id="eb4f5-121">**Docker 지원 사용**을 선택하지 **마세요**.</span><span class="sxs-lookup"><span data-stu-id="eb4f5-121">Do **not** select **Enable Docker Support**.</span></span>

### <a name="launch-the-app"></a><span data-ttu-id="eb4f5-122">앱 시작</span><span class="sxs-lookup"><span data-stu-id="eb4f5-122">Launch the app</span></span>

<span data-ttu-id="eb4f5-123">Visual Studio에서 CTRL+F5를 눌러 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="eb4f5-123">In Visual Studio, press CTRL+F5 to launch the app.</span></span> <span data-ttu-id="eb4f5-124">Visual Studio가 브라우저를 시작하고 `http://localhost:<port>/api/values`로 이동합니다. 여기서 `<port>`는 임의로 선택된 포트 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="eb4f5-124">Visual Studio launches a browser and navigates to `http://localhost:<port>/api/values`, where `<port>` is a randomly chosen port number.</span></span> <span data-ttu-id="eb4f5-125">Chrome, Microsoft Edge 및 Firefox에는 다음 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb4f5-125">Chrome, Microsoft Edge, and Firefox display the following output:</span></span>

```json
["value1","value2"]
```

<span data-ttu-id="eb4f5-126">Internet Explorer를 사용 중인 경우 *values.json* 파일을 저장하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb4f5-126">If using Internet Explorer, you'll be prompted to save a *values.json* file.</span></span>

### <a name="add-a-model-class"></a><span data-ttu-id="eb4f5-127">모델 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="eb4f5-127">Add a model class</span></span>

<span data-ttu-id="eb4f5-128">모델은 앱의 데이터를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="eb4f5-128">A model is an object representing the data in the app.</span></span> <span data-ttu-id="eb4f5-129">이 경우 유일한 모델은 할 일 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="eb4f5-129">In this case, the only model is a to-do item.</span></span>

<span data-ttu-id="eb4f5-130">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eb4f5-130">In Solution Explorer, right-click the project.</span></span> <span data-ttu-id="eb4f5-131">**추가** > **새 폴더**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eb4f5-131">Select **Add** > **New Folder**.</span></span> <span data-ttu-id="eb4f5-132">폴더 이름을 *Models*로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="eb4f5-132">Name the folder *Models*.</span></span>

> [!NOTE]
> <span data-ttu-id="eb4f5-133">모델 클래스는 프로젝트의 어디에서나 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb4f5-133">The model classes can go anywhere in the project.</span></span> <span data-ttu-id="eb4f5-134">*Models* 폴더는 모델 클래스에 대한 규칙에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb4f5-134">The *Models* folder is used by convention for model classes.</span></span>

<span data-ttu-id="eb4f5-135">솔루션 탐색기에서 *Models* 폴더를 마우스 오른쪽 단추로 클릭하고 **추가** > **클래스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eb4f5-135">In Solution Explorer, right-click the *Models* folder and select **Add** > **Class**.</span></span> <span data-ttu-id="eb4f5-136">클래스 이름을 *TodoItem*으로 지정하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eb4f5-136">Name the class *TodoItem* and click **Add**.</span></span>

<span data-ttu-id="eb4f5-137">`TodoItem` 클래스를 다음 코드로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="eb4f5-137">Update the `TodoItem` class with the following code:</span></span>

[!code-csharp[](first-web-api/samples/2.0/TodoApi/Models/TodoItem.cs)]

<span data-ttu-id="eb4f5-138">`TodoItem`이 만들어질 때 데이터베이스가 `Id`를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="eb4f5-138">The database generates the `Id` when a `TodoItem` is created.</span></span>

### <a name="create-the-database-context"></a><span data-ttu-id="eb4f5-139">데이터베이스 컨텍스트 만들기</span><span class="sxs-lookup"><span data-stu-id="eb4f5-139">Create the database context</span></span>

<span data-ttu-id="eb4f5-140">*데이터베이스 컨텍스트*는 특정 데이터 모델에 맞게 Entity Framework 기능을 조정하는 주 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="eb4f5-140">The *database context* is the main class that coordinates Entity Framework functionality for a given data model.</span></span> <span data-ttu-id="eb4f5-141">`Microsoft.EntityFrameworkCore.DbContext` 클래스에서 파생시키는 방식으로 이 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eb4f5-141">This class is created by deriving from the `Microsoft.EntityFrameworkCore.DbContext` class.</span></span>

<span data-ttu-id="eb4f5-142">솔루션 탐색기에서 *Models* 폴더를 마우스 오른쪽 단추로 클릭하고 **추가** > **클래스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eb4f5-142">In Solution Explorer, right-click the *Models* folder and select **Add** > **Class**.</span></span> <span data-ttu-id="eb4f5-143">클래스 이름을 *TodoContext*로 지정하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eb4f5-143">Name the class *TodoContext* and click **Add**.</span></span>

<span data-ttu-id="eb4f5-144">클래스를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="eb4f5-144">Replace the class with the following code:</span></span>

[!code-csharp[](first-web-api/samples/2.0/TodoApi/Models/TodoContext.cs)]

[!INCLUDE[Register the database context](../includes/webApi/register_dbContext.md)]

### <a name="add-a-controller"></a><span data-ttu-id="eb4f5-145">컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="eb4f5-145">Add a controller</span></span>

<span data-ttu-id="eb4f5-146">솔루션 탐색기에서 *Controllers* 폴더를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eb4f5-146">In Solution Explorer, right-click the *Controllers* folder.</span></span> <span data-ttu-id="eb4f5-147">**추가** > **새 항목**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eb4f5-147">Select **Add** > **New Item**.</span></span> <span data-ttu-id="eb4f5-148">**새 항목 추가** 대화 상자에서 **API 컨트롤러 클래스** 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eb4f5-148">In the **Add New Item** dialog, select the **API Controller Class** template.</span></span> <span data-ttu-id="eb4f5-149">클래스 이름을 *TodoController*로 지정하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eb4f5-149">Name the class *TodoController*, and click **Add**.</span></span>

![검색 상자의 컨트롤러 및 Web API 컨트롤러가 선택된 새 항목 추가 대화 상자](first-web-api/_static/new_controller.png)

<span data-ttu-id="eb4f5-151">클래스를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="eb4f5-151">Replace the class with the following code:</span></span>

[!INCLUDE[code and get todo items](../includes/webApi/getTodoItems.md)]

### <a name="launch-the-app"></a><span data-ttu-id="eb4f5-152">앱 시작</span><span class="sxs-lookup"><span data-stu-id="eb4f5-152">Launch the app</span></span>

<span data-ttu-id="eb4f5-153">Visual Studio에서 CTRL+F5를 눌러 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="eb4f5-153">In Visual Studio, press CTRL+F5 to launch the app.</span></span> <span data-ttu-id="eb4f5-154">Visual Studio가 브라우저를 시작하고 `http://localhost:<port>/api/values`로 이동합니다. 여기서 `<port>`는 임의로 선택된 포트 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="eb4f5-154">Visual Studio launches a browser and navigates to `http://localhost:<port>/api/values`, where `<port>` is a randomly chosen port number.</span></span> <span data-ttu-id="eb4f5-155">`http://localhost:<port>/api/todo`의 `Todo` 컨트롤러로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="eb4f5-155">Navigate to the `Todo` controller at `http://localhost:<port>/api/todo`.</span></span>

[!INCLUDE[last part of web API](../includes/webApi/end.md)]

[!INCLUDE[jQuery](../includes/webApi/add-jquery.md)]

[!INCLUDE[next steps](../includes/webApi/next.md)]
