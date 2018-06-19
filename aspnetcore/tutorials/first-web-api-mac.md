---
title: ASP.NET Core 및 Mac용 Visual Studio를 사용하여 Web API 만들기
author: rick-anderson
description: ASP.NET Core MVC 및 Mac용 Visual Studio를 사용하여 Web API 만들기
helpviewer_heywords: ASP.NET Core, WebAPI, Web API, REST, mac, macOS, HTTP, Service, HTTP Service
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 05/08/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: tutorials/first-web-api-mac
ms.openlocfilehash: 699fbbf54abf1dc5c4156c559761110cdb375558
ms.sourcegitcommit: c867d7427bd4a88a78b2322e156367733b532730
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2018
ms.locfileid: "33923206"
---
# <a name="create-a-web-api-with-aspnet-core-and-visual-studio-for-mac"></a><span data-ttu-id="95791-103">ASP.NET Core 및 Mac용 Visual Studio를 사용하여 Web API 만들기</span><span class="sxs-lookup"><span data-stu-id="95791-103">Create a Web API with ASP.NET Core and Visual Studio for Mac</span></span>

<span data-ttu-id="95791-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Mike Wasson](https://github.com/mikewasson)</span><span class="sxs-lookup"><span data-stu-id="95791-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Mike Wasson](https://github.com/mikewasson)</span></span>

<span data-ttu-id="95791-105">이 자습서에서는 “할 일” 항목 목록을 관리하기 위한 웹 API를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-105">In this tutorial, build a web API for managing a list of "to-do" items.</span></span> <span data-ttu-id="95791-106">UI는 생성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="95791-106">The UI isn't constructed.</span></span>

<span data-ttu-id="95791-107">이 자습서는 다음 세 가지 버전으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="95791-107">There are three versions of this tutorial:</span></span>

* <span data-ttu-id="95791-108">macOS: Mac용 Visual Studio를 사용한 Web API(이 자습서)</span><span class="sxs-lookup"><span data-stu-id="95791-108">macOS: Web API with Visual Studio for Mac (This tutorial)</span></span>
* <span data-ttu-id="95791-109">Windows: [Windows용 Visual Studio를 사용한 Web API](xref:tutorials/first-web-api)</span><span class="sxs-lookup"><span data-stu-id="95791-109">Windows: [Web API with Visual Studio for Windows](xref:tutorials/first-web-api)</span></span>
* <span data-ttu-id="95791-110">macOS, Linux, Windows: [Visual Studio Code를 사용한 Web API](xref:tutorials/web-api-vsc)</span><span class="sxs-lookup"><span data-stu-id="95791-110">macOS, Linux, Windows: [Web API with Visual Studio Code](xref:tutorials/web-api-vsc)</span></span>

<!-- WARNING: The code AND images in this doc are used by uid: tutorials/web-api-vsc, tutorials/first-web-api-mac and tutorials/first-web-api. If you change any code/images in this tutorial, update uid: tutorials/web-api-vsc -->

[!INCLUDE[template files](../includes/webApi/intro.md)]

<span data-ttu-id="95791-111">영구 데이터베이스를 사용하는 예제를 보려면 [macOS 또는 Linux의 ASP.NET Core MVC 소개](xref:tutorials/first-mvc-app-xplat/index)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95791-111">See [Introduction to ASP.NET Core MVC on macOS or Linux](xref:tutorials/first-mvc-app-xplat/index) for an example that uses a persistent database.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95791-112">전제 조건</span><span class="sxs-lookup"><span data-stu-id="95791-112">Prerequisites</span></span>

[!INCLUDE[](~/includes/net-core-prereqs-macos.md)]

## <a name="create-the-project"></a><span data-ttu-id="95791-113">프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="95791-113">Create the project</span></span>

<span data-ttu-id="95791-114">Visual Studio에서 **파일** > **새 솔루션**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-114">From Visual Studio, select **File** > **New Solution**.</span></span>

![macOS 새 솔루션](first-web-api-mac/_static/sln.png)

<span data-ttu-id="95791-116">**.NET Core App** > **ASP.NET Core Web API** > **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-116">Select **.NET Core App** > **ASP.NET Core Web API** > **Next**.</span></span>

![macOS 새 프로젝트 대화 상자](first-web-api-mac/_static/1.png)

<span data-ttu-id="95791-118">**프로젝트 이름**으로 *TodoApi*를 입력한 다음, **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-118">Enter *TodoApi* for the **Project Name**, and then click **Create**.</span></span>

![구성 대화 상자](first-web-api-mac/_static/2.png)

### <a name="launch-the-app"></a><span data-ttu-id="95791-120">앱 시작</span><span class="sxs-lookup"><span data-stu-id="95791-120">Launch the app</span></span>

<span data-ttu-id="95791-121">Visual Studio에서 **실행** > **디버깅 시작**을 선택하여 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-121">In Visual Studio, select **Run** > **Start With Debugging** to launch the app.</span></span> <span data-ttu-id="95791-122">Visual Studio가 브라우저를 시작하고 `http://localhost:5000`으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-122">Visual Studio launches a browser and navigates to `http://localhost:5000`.</span></span> <span data-ttu-id="95791-123">HTTP 404(찾을 수 없음) 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="95791-123">You get an HTTP 404 (Not Found) error.</span></span> <span data-ttu-id="95791-124">URL을 `http://localhost:<port>/api/values`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-124">Change the URL to `http://localhost:<port>/api/values`.</span></span> <span data-ttu-id="95791-125">`ValuesController` 데이터가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="95791-125">The `ValuesController` data is displayed:</span></span>

```json
["value1","value2"]
```

### <a name="add-support-for-entity-framework-core"></a><span data-ttu-id="95791-126">Entity Framework Core에 대한 지원 추가</span><span class="sxs-lookup"><span data-stu-id="95791-126">Add support for Entity Framework Core</span></span>

<span data-ttu-id="95791-127">[Entity Framework Core InMemory](/ef/core/providers/in-memory/) 데이터베이스 공급자를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-127">Install the [Entity Framework Core InMemory](/ef/core/providers/in-memory/) database provider.</span></span> <span data-ttu-id="95791-128">이 데이터베이스 공급자를 설치하면 Entity Framework Core를 메모리 내 데이터베이스에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95791-128">This database provider allows Entity Framework Core to be used with an in-memory database.</span></span>

* <span data-ttu-id="95791-129">**프로젝트** 메뉴에서 **NuGet 패키지 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-129">From the **Project** menu, select **Add NuGet Packages**.</span></span>

  * <span data-ttu-id="95791-130">또는 **종속성**을 마우스 오른쪽 단추로 클릭한 다음, **패키지 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-130">Alternatively, you can right-click **Dependencies**, and then select **Add Packages**.</span></span>

* <span data-ttu-id="95791-131">검색 상자에 `EntityFrameworkCore.InMemory`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-131">Enter `EntityFrameworkCore.InMemory` in the search box.</span></span>
* <span data-ttu-id="95791-132">`Microsoft.EntityFrameworkCore.InMemory`를 선택하고 **패키지 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-132">Select `Microsoft.EntityFrameworkCore.InMemory`, and then select **Add Package**.</span></span>

### <a name="add-a-model-class"></a><span data-ttu-id="95791-133">모델 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="95791-133">Add a model class</span></span>

<span data-ttu-id="95791-134">모델은 앱에서 데이터를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="95791-134">A model is an object representing the data in your app.</span></span> <span data-ttu-id="95791-135">이 경우 유일한 모델은 할 일 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="95791-135">In this case, the only model is a to-do item.</span></span>

<span data-ttu-id="95791-136">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-136">In Solution Explorer, right-click the project.</span></span> <span data-ttu-id="95791-137">**추가** > **새 폴더**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-137">Select **Add** > **New Folder**.</span></span> <span data-ttu-id="95791-138">폴더 이름을 *Models*로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-138">Name the folder *Models*.</span></span>

![새 폴더](first-web-api-mac/_static/folder.png)

> [!NOTE]
> <span data-ttu-id="95791-140">프로젝트의 아무 곳에나 모델 클래스를 넣을 수 있지만 일반적으로 *Models* 폴더를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-140">You can put model classes anywhere in your project, but the *Models* folder is used by convention.</span></span>

<span data-ttu-id="95791-141">*모델* 폴더를 마우스 오른쪽 단추로 클릭하고 **추가** > **새 파일** > **일반** > **빈 클래스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-141">Right-click the *Models* folder, and select **Add** > **New File** > **General** > **Empty Class**.</span></span> <span data-ttu-id="95791-142">클래스 이름을 *TodoItem*으로 지정한 다음, **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-142">Name the class *TodoItem*, and then click **New**.</span></span>

<span data-ttu-id="95791-143">생성된 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="95791-143">Replace the generated code with:</span></span>

[!code-csharp[](first-web-api/samples/2.0/TodoApi/Models/TodoItem.cs)]

<span data-ttu-id="95791-144">`TodoItem`이 만들어질 때 데이터베이스가 `Id`를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-144">The database generates the `Id` when a `TodoItem` is created.</span></span>

### <a name="create-the-database-context"></a><span data-ttu-id="95791-145">데이터베이스 컨텍스트 만들기</span><span class="sxs-lookup"><span data-stu-id="95791-145">Create the database context</span></span>

<span data-ttu-id="95791-146">*데이터베이스 컨텍스트*는 특정 데이터 모델에 맞게 Entity Framework 기능을 조정하는 주 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="95791-146">The *database context* is the main class that coordinates Entity Framework functionality for a given data model.</span></span> <span data-ttu-id="95791-147">`Microsoft.EntityFrameworkCore.DbContext` 클래스에서 파생시키는 방식으로 이 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="95791-147">You create this class by deriving from the `Microsoft.EntityFrameworkCore.DbContext` class.</span></span>

<span data-ttu-id="95791-148">`TodoContext` 클래스를 *Models* 폴더에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-148">Add a `TodoContext` class to the *Models* folder.</span></span>

[!code-csharp[](first-web-api/samples/2.0/TodoApi/Models/TodoContext.cs)]

[!INCLUDE[Register the database context](../includes/webApi/register_dbContext.md)]

## <a name="add-a-controller"></a><span data-ttu-id="95791-149">컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="95791-149">Add a controller</span></span>

<span data-ttu-id="95791-150">솔루션 탐색기의 *Controllers* 폴더에서 `TodoController` 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-150">In Solution Explorer, in the *Controllers* folder, add the class `TodoController`.</span></span>

<span data-ttu-id="95791-151">생성된 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="95791-151">Replace the generated code with the following:</span></span>

[!INCLUDE[code and get todo items](../includes/webApi/getTodoItems.md)]

### <a name="launch-the-app"></a><span data-ttu-id="95791-152">앱 시작</span><span class="sxs-lookup"><span data-stu-id="95791-152">Launch the app</span></span>

<span data-ttu-id="95791-153">Visual Studio에서 **실행** > **디버깅 시작**을 선택하여 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-153">In Visual Studio, select **Run** > **Start With Debugging** to launch the app.</span></span> <span data-ttu-id="95791-154">Visual Studio가 브라우저를 시작하고 `http://localhost:<port>`로 이동합니다. 여기서 `<port>`는 임의로 선택된 포트 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="95791-154">Visual Studio launches a browser and navigates to `http://localhost:<port>`, where `<port>` is a randomly chosen port number.</span></span> <span data-ttu-id="95791-155">HTTP 404(찾을 수 없음) 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="95791-155">You get an HTTP 404 (Not Found) error.</span></span> <span data-ttu-id="95791-156">URL을 `http://localhost:<port>/api/values`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-156">Change the URL to `http://localhost:<port>/api/values`.</span></span> <span data-ttu-id="95791-157">`ValuesController` 데이터가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="95791-157">The `ValuesController` data is displayed:</span></span>

```json
["value1","value2"]
```

<span data-ttu-id="95791-158">`http://localhost:<port>/api/todo`의 `Todo` 컨트롤러로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-158">Navigate to the `Todo` controller at `http://localhost:<port>/api/todo`.</span></span> <span data-ttu-id="95791-159">다음 JSON이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="95791-159">The following JSON is returned:</span></span>

```json
[{"key":1,"name":"Item1","isComplete":false}]
```

## <a name="implement-the-other-crud-operations"></a><span data-ttu-id="95791-160">기타 CRUD 작업 구현</span><span class="sxs-lookup"><span data-stu-id="95791-160">Implement the other CRUD operations</span></span>

<span data-ttu-id="95791-161">`Create`, `Update` 및 `Delete` 메서드를 컨트롤러에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-161">We'll add `Create`, `Update`, and `Delete` methods to the controller.</span></span> <span data-ttu-id="95791-162">이러한 메서드는 테마에 대한 변형이므로 코드를 표시하고 주요 차이점을 강조 표시하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="95791-162">These methods are variations on a theme, so I'll just show the code and highlight the main differences.</span></span> <span data-ttu-id="95791-163">코드를 추가하거나 변경한 후 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-163">Build the project after adding or changing code.</span></span>

### <a name="create"></a><span data-ttu-id="95791-164">만들기</span><span class="sxs-lookup"><span data-stu-id="95791-164">Create</span></span>

::: moniker range="<= aspnetcore-2.0"
<span data-ttu-id="95791-165">[!code-csharp[](first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_Create)]</span><span class="sxs-lookup"><span data-stu-id="95791-165">[!code-csharp[](first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_Create)]</span></span>

<span data-ttu-id="95791-166">이전 메서드는 [[HttpPost]](/dotnet/api/microsoft.aspnetcore.mvc.httppostattribute) 특성으로 표시되는 HTTP POST에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-166">The preceding method responds to an HTTP POST, as indicated by the [[HttpPost]](/dotnet/api/microsoft.aspnetcore.mvc.httppostattribute) attribute.</span></span> <span data-ttu-id="95791-167">[[FromBody]](/dotnet/api/microsoft.aspnetcore.mvc.frombodyattribute) 특성은 HTTP 요청 본문에서 할 일 항목 값을 가져오도록 MVC에 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-167">The [[FromBody]](/dotnet/api/microsoft.aspnetcore.mvc.frombodyattribute) attribute tells MVC to get the value of the to-do item from the body of the HTTP request.</span></span>
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
<span data-ttu-id="95791-168">[!code-csharp[](first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=snippet_Create)]</span><span class="sxs-lookup"><span data-stu-id="95791-168">[!code-csharp[](first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=snippet_Create)]</span></span>

<span data-ttu-id="95791-169">이전 메서드는 [[HttpPost]](/dotnet/api/microsoft.aspnetcore.mvc.httppostattribute) 특성으로 표시되는 HTTP POST에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-169">The preceding method responds to an HTTP POST, as indicated by the [[HttpPost]](/dotnet/api/microsoft.aspnetcore.mvc.httppostattribute) attribute.</span></span> <span data-ttu-id="95791-170">MVC는 HTTP 요청 본문에서 할 일 항목 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="95791-170">MVC gets the value of the to-do item from the body of the HTTP request.</span></span>
::: moniker-end

<span data-ttu-id="95791-171">`CreatedAtRoute` 메서드는 201 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-171">The `CreatedAtRoute` method returns a 201 response.</span></span> <span data-ttu-id="95791-172">이는 서버에서 새 리소스를 만드는 HTTP POST 메서드의 표준 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="95791-172">It's the standard response for an HTTP POST method that creates a new resource on the server.</span></span> <span data-ttu-id="95791-173">`CreatedAtRoute`는 응답에 대한 위치 헤더도 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-173">`CreatedAtRoute` also adds a Location header to the response.</span></span> <span data-ttu-id="95791-174">위치 헤더는 새로 만들어진 할 일 항목의 URI를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-174">The Location header specifies the URI of the newly created to-do item.</span></span> <span data-ttu-id="95791-175">[10.2.2 201 Created](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)(10.2.2 201 생성됨)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95791-175">See [10.2.2 201 Created](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html).</span></span>

### <a name="use-postman-to-send-a-create-request"></a><span data-ttu-id="95791-176">Postman을 사용하여 만들기 요청 보내기</span><span class="sxs-lookup"><span data-stu-id="95791-176">Use Postman to send a Create request</span></span>

* <span data-ttu-id="95791-177">앱을 시작합니다(**실행** > **디버깅 시작**).</span><span class="sxs-lookup"><span data-stu-id="95791-177">Start the app (**Run** > **Start With Debugging**).</span></span>
* <span data-ttu-id="95791-178">Postman을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="95791-178">Open Postman.</span></span>

![Postman 콘솔](first-web-api/_static/pmc.png)

* <span data-ttu-id="95791-180">localhost URL에서 포트 번호를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-180">Update the port number in the localhost URL.</span></span>
* <span data-ttu-id="95791-181">HTTP 메서드를 *POST*로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-181">Set the HTTP method to *POST*.</span></span>
* <span data-ttu-id="95791-182">**본문** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-182">Click the **Body** tab.</span></span>
* <span data-ttu-id="95791-183">**원시** 라디오 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-183">Select the **raw** radio button.</span></span>
* <span data-ttu-id="95791-184">유형을 *JSON(application/json)* 으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-184">Set the type to *JSON (application/json)*.</span></span>
* <span data-ttu-id="95791-185">다음 JSON과 같은 할 일 항목을 사용하여 요청 본문을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-185">Enter a request body with a to-do item resembling the following JSON:</span></span>

```json
{
  "name":"walk dog",
  "isComplete":true
}
```

* <span data-ttu-id="95791-186">**보내기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-186">Click the **Send** button.</span></span>

::: moniker range=">= aspnetcore-2.1"
> [!TIP]
> <span data-ttu-id="95791-187">**보내기**를 클릭한 후 응답이 표시되지 않는 경우 **SSL 인증 유효성 검사** 옵션을 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="95791-187">If no response displays after clicking **Send**, disable the **SSL certification verification** option.</span></span> <span data-ttu-id="95791-188">이 옵션은 **파일** > **설정** 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95791-188">This is found under **File** > **Settings**.</span></span> <span data-ttu-id="95791-189">설정을 사용하지 못하게 한 후 **보내기** 단추를 다시 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-189">Click the **Send** button again after disabling the setting.</span></span>
::: moniker-end

<span data-ttu-id="95791-190">**응답** 창에서 **헤더** 탭을 클릭하고 **위치** 헤더 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-190">Click the **Headers** tab in the **Response** pane and copy the **Location** header value:</span></span>

![Postman 콘솔의 헤더 탭](first-web-api/_static/pmc2.png)

<span data-ttu-id="95791-192">위치 헤더 URI를 사용하여 만든 리소스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95791-192">You can use the Location header URI to access the resource you created.</span></span> <span data-ttu-id="95791-193">`Create` 메서드는 [CreatedAtRoute](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.createdatroute#Microsoft_AspNetCore_Mvc_ControllerBase_CreatedAtRoute_System_String_System_Object_System_Object_)를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-193">The `Create` method returns [CreatedAtRoute](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.createdatroute#Microsoft_AspNetCore_Mvc_ControllerBase_CreatedAtRoute_System_String_System_Object_System_Object_).</span></span> <span data-ttu-id="95791-194">`CreatedAtRoute`에 전달된 첫 번째 매개 변수는 URL을 생성하는 데 사용할 이름이 지정된 경로를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="95791-194">The first parameter passed to `CreatedAtRoute` represents the named route to use for generating the URL.</span></span> <span data-ttu-id="95791-195">`GetById` 메서드가 `"GetTodo"`로 명명된 경로를 만들었다는 사실을 기억하세요.</span><span class="sxs-lookup"><span data-stu-id="95791-195">Recall that the `GetById` method created the `"GetTodo"` named route:</span></span>

```csharp
[HttpGet("{id}", Name = "GetTodo")]
```

### <a name="update"></a><span data-ttu-id="95791-196">업데이트</span><span class="sxs-lookup"><span data-stu-id="95791-196">Update</span></span>

::: moniker range="<= aspnetcore-2.0"
<span data-ttu-id="95791-197">[!code-csharp[](first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_Update)]</span><span class="sxs-lookup"><span data-stu-id="95791-197">[!code-csharp[](first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_Update)]</span></span>
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
<span data-ttu-id="95791-198">[!code-csharp[](first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=snippet_Update)]</span><span class="sxs-lookup"><span data-stu-id="95791-198">[!code-csharp[](first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=snippet_Update)]</span></span>
::: moniker-end

<span data-ttu-id="95791-199">`Update`는 `Create`와 비슷하지만 HTTP PUT을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-199">`Update` is similar to `Create`, but uses HTTP PUT.</span></span> <span data-ttu-id="95791-200">응답은 [204(콘텐츠 없음)](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)입니다.</span><span class="sxs-lookup"><span data-stu-id="95791-200">The response is [204 (No Content)](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html).</span></span> <span data-ttu-id="95791-201">HTTP 사양에 따라 PUT 요청의 경우 클라이언트는 델타만이 아니라 전체 업데이트된 엔터티를 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-201">According to the HTTP spec, a PUT request requires the client to send the entire updated entity, not just the deltas.</span></span> <span data-ttu-id="95791-202">부분 업데이트를 지원하려면 HTTP PATCH를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="95791-202">To support partial updates, use HTTP PATCH.</span></span>

```json
{
  "key": 1,
  "name": "walk dog",
  "isComplete": true
}
```

![204(콘텐츠 없음) 응답을 보여주는 Postman 콘솔](first-web-api/_static/pmcput.png)

### <a name="delete"></a><span data-ttu-id="95791-204">삭제</span><span class="sxs-lookup"><span data-stu-id="95791-204">Delete</span></span>

[!code-csharp[](first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_Delete)]

<span data-ttu-id="95791-205">응답은 [204(콘텐츠 없음)](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)입니다.</span><span class="sxs-lookup"><span data-stu-id="95791-205">The response is [204 (No Content)](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html).</span></span>

![204(콘텐츠 없음) 응답을 보여주는 Postman 콘솔](first-web-api/_static/pmd.png)

[!INCLUDE[jQuery](../includes/webApi/add-jquery.md)]

[!INCLUDE[next steps](../includes/webApi/next.md)]
