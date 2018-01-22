---
title: "ASP.NET Core 및 Mac용 Visual Studio를 사용하여 Web API 만들기"
description: "ASP.NET Core MVC 및 Mac용 Visual Studio를 사용하여 Web API 만들기"
author: rick-anderson
ms.author: riande
ms.date: 09/15/2017
ms.topic: get-started-article
ms.prod: asp.net-core
uid: tutorials/first-web-api-mac
helpviewer_heywords: ASP.NET Core, WebAPI, Web API, REST, mac, macOS, HTTP, Service, HTTP Service
ms.technology: aspnet
manager: wpickett
ms.openlocfilehash: 4f2643a91e1523008b68df670a9734e3d4dea5a8
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="create-a-web-api-with-aspnet-core-mvc-and-visual-studio-for-mac"></a><span data-ttu-id="0f4da-103">ASP.NET Core MVC 및 Mac용 Visual Studio를 사용하여 Web API 만들기</span><span class="sxs-lookup"><span data-stu-id="0f4da-103">Create a Web API with ASP.NET Core MVC and Visual Studio for Mac</span></span>

<span data-ttu-id="0f4da-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Mike Wasson](https://github.com/mikewasson)</span><span class="sxs-lookup"><span data-stu-id="0f4da-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Mike Wasson](https://github.com/mikewasson)</span></span>

<span data-ttu-id="0f4da-105">이 자습서에서는 “할 일” 항목 목록을 관리하기 위한 웹 API를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-105">In this tutorial, you’ll build a web API for managing a list of "to-do" items.</span></span> <span data-ttu-id="0f4da-106">UI는 빌드하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-106">You won’t build a UI.</span></span>

<span data-ttu-id="0f4da-107">이 자습서는 세 가지 버전이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-107">There are 3 versions of this tutorial:</span></span>

* <span data-ttu-id="0f4da-108">macOS: Mac용 Visual Studio를 사용한 Web API(이 자습서)</span><span class="sxs-lookup"><span data-stu-id="0f4da-108">macOS: Web API with Visual Studio for Mac (This tutorial)</span></span>
* <span data-ttu-id="0f4da-109">Windows: [Windows용 Visual Studio를 사용한 Web API](xref:tutorials/first-web-api)</span><span class="sxs-lookup"><span data-stu-id="0f4da-109">Windows: [Web API with Visual Studio for Windows](xref:tutorials/first-web-api)</span></span>
* <span data-ttu-id="0f4da-110">macOS, Linux, Windows: [Visual Studio Code를 사용한 Web API](xref:tutorials/web-api-vsc)</span><span class="sxs-lookup"><span data-stu-id="0f4da-110">macOS, Linux, Windows: [Web API with Visual Studio Code](xref:tutorials/web-api-vsc)</span></span>

<!-- WARNING: The code AND images in this doc are used by uid: tutorials/web-api-vsc, tutorials/first-web-api-mac and tutorials/first-web-api. If you change any code/images in this tutorial, update uid: tutorials/web-api-vsc -->

[!INCLUDE[template files](../includes/webApi/intro.md)]

* <span data-ttu-id="0f4da-111">영구 데이터베이스를 사용하는 예제를 보려면 [Mac 또는 Linux의 ASP.NET Core MVC 소개](xref:tutorials/first-mvc-app-xplat/index)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f4da-111">See [Introduction to ASP.NET Core MVC on Mac or Linux](xref:tutorials/first-mvc-app-xplat/index) for an example that uses a persistent database.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0f4da-112">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="0f4da-112">Prerequisites</span></span>

<span data-ttu-id="0f4da-113">다음을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-113">Install the following:</span></span>

- <span data-ttu-id="0f4da-114">[.NET Core 2.0.0 SDK](https://www.microsoft.com/net/core) 이상</span><span class="sxs-lookup"><span data-stu-id="0f4da-114">[.NET Core 2.0.0 SDK](https://www.microsoft.com/net/core) or later</span></span>
- [<span data-ttu-id="0f4da-115">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="0f4da-115">Visual Studio for Mac</span></span>](https://www.visualstudio.com/vs/visual-studio-mac/)

## <a name="create-the-project"></a><span data-ttu-id="0f4da-116">프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-116">Create the project</span></span>

<span data-ttu-id="0f4da-117">Visual Studio에서 **파일 > 새 솔루션**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-117">From Visual Studio, select **File > New Solution**.</span></span>

![macOS 새 솔루션](first-web-api-mac/_static/sln.png)

<span data-ttu-id="0f4da-119">**.NET Core App > ASP.NET Core Web API > 다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-119">Select **.NET Core App >  ASP.NET Core Web API > Next**.</span></span>

![macOS 새 프로젝트 대화 상자](first-web-api-mac/_static/1.png)

<span data-ttu-id="0f4da-121">**프로젝트 이름**으로 **TodoApi**를 입력하고 [만들기]를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-121">Enter **TodoApi** for the **Project Name**, and then select Create.</span></span>

![구성 대화 상자](first-web-api-mac/_static/2.png)

### <a name="launch-the-app"></a><span data-ttu-id="0f4da-123">앱 시작</span><span class="sxs-lookup"><span data-stu-id="0f4da-123">Launch the app</span></span>

<span data-ttu-id="0f4da-124">Visual Studio에서 **실행 > 디버깅 시작**을 선택하여 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-124">In Visual Studio, select **Run > Start With Debugging** to launch the app.</span></span> <span data-ttu-id="0f4da-125">Visual Studio가 브라우저를 시작하고 `http://localhost:5000`으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-125">Visual Studio launches a browser and navigates to `http://localhost:5000`.</span></span> <span data-ttu-id="0f4da-126">HTTP 404(찾을 수 없음) 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-126">You get an HTTP 404 (Not Found) error.</span></span>  <span data-ttu-id="0f4da-127">URL을 `http://localhost:port/api/values`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-127">Change the URL to `http://localhost:port/api/values`.</span></span> <span data-ttu-id="0f4da-128">`ValuesController` 데이터가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-128">The `ValuesController` data will be displayed:</span></span>

```
["value1","value2"]
```

### <a name="add-support-for-entity-framework-core"></a><span data-ttu-id="0f4da-129">Entity Framework Core에 대한 지원 추가</span><span class="sxs-lookup"><span data-stu-id="0f4da-129">Add support for Entity Framework Core</span></span>

<span data-ttu-id="0f4da-130">[Entity Framework Core InMemory](https://docs.microsoft.com/ef/core/providers/in-memory/) 데이터베이스 공급자를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-130">Install the [Entity Framework Core InMemory](https://docs.microsoft.com/ef/core/providers/in-memory/) database provider.</span></span> <span data-ttu-id="0f4da-131">이 데이터베이스 공급자를 설치하면 Entity Framework Core를 메모리 내 데이터베이스에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-131">This database provider allows Entity Framework Core to be used with an in-memory database.</span></span>

* <span data-ttu-id="0f4da-132">**프로젝트** 메뉴에서 **NuGet 패키지 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-132">From the **Project** menu, select **Add NuGet Packages**.</span></span> 

  *  <span data-ttu-id="0f4da-133">또는 **종속성**을 마우스 오른쪽 단추로 클릭하고 **패키지 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-133">Alternately, you can right-click **Dependencies**, and then select **Add Packages**.</span></span>

* <span data-ttu-id="0f4da-134">검색 상자에 `EntityFrameworkCore.InMemory`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-134">Enter `EntityFrameworkCore.InMemory` in the search box.</span></span>
* <span data-ttu-id="0f4da-135">`Microsoft.EntityFrameworkCore.InMemory`를 선택하고 **패키지 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-135">Select `Microsoft.EntityFrameworkCore.InMemory`, and then select **Add Package**.</span></span>

### <a name="add-a-model-class"></a><span data-ttu-id="0f4da-136">모델 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="0f4da-136">Add a model class</span></span>

<span data-ttu-id="0f4da-137">모델은 응용 프로그램에서 데이터를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-137">A model is an object that represents the data in your application.</span></span> <span data-ttu-id="0f4da-138">이 경우 유일한 모델은 할 일 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-138">In this case, the only model is a to-do item.</span></span>

<span data-ttu-id="0f4da-139">*Models* 폴더를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-139">Add a folder named *Models*.</span></span> <span data-ttu-id="0f4da-140">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-140">In Solution Explorer, right-click the project.</span></span> <span data-ttu-id="0f4da-141">**추가** > **새 폴더**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-141">Select **Add** > **New Folder**.</span></span> <span data-ttu-id="0f4da-142">폴더 이름을 *Models*로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-142">Name the folder *Models*.</span></span>

![새 폴더](first-web-api-mac/_static/folder.png)

<span data-ttu-id="0f4da-144">참고: 프로젝트의 아무 곳에나 모델 클래스를 넣을 수 있지만 일반적으로 *Models* 폴더를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-144">Note: You can put model classes anywhere in your project, but the *Models* folder is used by convention.</span></span>

<span data-ttu-id="0f4da-145">`TodoItem` 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-145">Add a `TodoItem` class.</span></span> <span data-ttu-id="0f4da-146">*Models* 폴더를 마우스 오른쪽 단추로 클릭하고 **추가 > 새 파일 > 일반 > 빈 클래스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-146">Right-click the *Models* folder and select **Add > New File > General > Empty Class**.</span></span> <span data-ttu-id="0f4da-147">클래스 이름을 `TodoItem`으로 지정하고 **새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-147">Name the class `TodoItem`, and then select **New**.</span></span>

<span data-ttu-id="0f4da-148">생성된 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-148">Replace the generated code with:</span></span>

[!code-csharp[Main](first-web-api/sample/TodoApi/Models/TodoItem.cs)]

<span data-ttu-id="0f4da-149">`TodoItem`이 만들어질 때 데이터베이스가 `Id`를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-149">The database generates the `Id` when a `TodoItem` is created.</span></span>

### <a name="create-the-database-context"></a><span data-ttu-id="0f4da-150">데이터베이스 컨텍스트 만들기</span><span class="sxs-lookup"><span data-stu-id="0f4da-150">Create the database context</span></span>

<span data-ttu-id="0f4da-151">*데이터베이스 컨텍스트*는 특정 데이터 모델에 맞게 Entity Framework 기능을 조정하는 주 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-151">The *database context* is the main class that coordinates Entity Framework functionality for a given data model.</span></span> <span data-ttu-id="0f4da-152">`Microsoft.EntityFrameworkCore.DbContext` 클래스에서 파생시키는 방식으로 이 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-152">You create this class by deriving from the `Microsoft.EntityFrameworkCore.DbContext` class.</span></span>

<span data-ttu-id="0f4da-153">`TodoContext` 클래스를 *Models* 폴더에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-153">Add a `TodoContext` class to the *Models* folder.</span></span>

[!code-csharp[Main](first-web-api/sample/TodoApi/Models/TodoContext.cs)]

[!INCLUDE[Register the database context](../includes/webApi/register_dbContext.md)]

## <a name="add-a-controller"></a><span data-ttu-id="0f4da-154">컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="0f4da-154">Add a controller</span></span>

<span data-ttu-id="0f4da-155">솔루션 탐색기의 *Controllers* 폴더에서 `TodoController` 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-155">In Solution Explorer, in the *Controllers* folder, add the class `TodoController`.</span></span>

<span data-ttu-id="0f4da-156">생성된 코드를 다음으로 바꾸고 닫는 중괄호를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-156">Replace the generated code with the following (and add closing braces):</span></span>

[!INCLUDE[code and get todo items](../includes/webApi/getTodoItems.md)]

### <a name="launch-the-app"></a><span data-ttu-id="0f4da-157">앱 시작</span><span class="sxs-lookup"><span data-stu-id="0f4da-157">Launch the app</span></span>

<span data-ttu-id="0f4da-158">Visual Studio에서 **실행 > 디버깅 시작**을 선택하여 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-158">In Visual Studio, select **Run > Start With Debugging** to launch the app.</span></span> <span data-ttu-id="0f4da-159">Visual Studio가 브라우저를 시작하고 `http://localhost:port`로 이동합니다. 여기서 *port*는 임의로 선택된 포트 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-159">Visual Studio launches a browser and navigates to `http://localhost:port`, where *port* is a randomly chosen port number.</span></span> <span data-ttu-id="0f4da-160">HTTP 404(찾을 수 없음) 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-160">You get an HTTP 404 (Not Found) error.</span></span>  <span data-ttu-id="0f4da-161">URL을 `http://localhost:port/api/values`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-161">Change the URL to `http://localhost:port/api/values`.</span></span> <span data-ttu-id="0f4da-162">`ValuesController` 데이터가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-162">The `ValuesController` data will be displayed:</span></span>

```
["value1","value2"]
```

<span data-ttu-id="0f4da-163">`Todo` 컨트롤러(`http://localhost:port/api/todo`)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-163">Navigate to the `Todo` controller at`http://localhost:port/api/todo`:</span></span>

```
[{"key":1,"name":"Item1","isComplete":false}]
```

## <a name="implement-the-other-crud-operations"></a><span data-ttu-id="0f4da-164">기타 CRUD 작업 구현</span><span class="sxs-lookup"><span data-stu-id="0f4da-164">Implement the other CRUD operations</span></span>

<span data-ttu-id="0f4da-165">`Create`, `Update` 및 `Delete` 메서드를 컨트롤러에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-165">We'll add `Create`, `Update`, and `Delete` methods to the controller.</span></span> <span data-ttu-id="0f4da-166">이러한 메서드는 테마에 대한 변형이므로 코드를 표시하고 주요 차이점을 강조 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-166">These are variations on a theme, so I'll just show the code and highlight the main differences.</span></span> <span data-ttu-id="0f4da-167">코드를 추가하거나 변경한 후 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-167">Build the project after adding or changing code.</span></span>

### <a name="create"></a><span data-ttu-id="0f4da-168">만들기</span><span class="sxs-lookup"><span data-stu-id="0f4da-168">Create</span></span>

[!code-csharp[Main](first-web-api/sample/TodoApi/Controllers/TodoController.cs?name=snippet_Create)]

<span data-ttu-id="0f4da-169">[`[HttpPost]`](/aspnet/core/api/microsoft.aspnetcore.mvc.httppostattribute) 특성으로 나타내는 HTTP POST 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-169">This is an HTTP POST method, indicated by the [`[HttpPost]`](/aspnet/core/api/microsoft.aspnetcore.mvc.httppostattribute) attribute.</span></span> <span data-ttu-id="0f4da-170">[`[FromBody]`](/aspnet/core/api/microsoft.aspnetcore.mvc.frombodyattribute) 특성은 HTTP 요청 본문에서 할 일 항목 값을 가져오도록 MVC에 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-170">The [`[FromBody]`](/aspnet/core/api/microsoft.aspnetcore.mvc.frombodyattribute) attribute tells MVC to get the value of the to-do item from the body of the HTTP request.</span></span>

<span data-ttu-id="0f4da-171">`CreatedAtRoute` 메서드는 서버에서 새 리소스를 만드는 HTTP POST 메서드의 표준 응답인 201 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-171">The `CreatedAtRoute` method returns a 201 response, which is the standard response for an HTTP POST method that creates a new resource on the server.</span></span> <span data-ttu-id="0f4da-172">`CreatedAtRoute`는 응답에 대한 위치 헤더도 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-172">`CreatedAtRoute` also adds a Location header to the response.</span></span> <span data-ttu-id="0f4da-173">위치 헤더는 새로 만들어진 할 일 항목의 URI를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-173">The Location header specifies the URI of the newly created to-do item.</span></span> <span data-ttu-id="0f4da-174">[10.2.2 201 Created](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)(10.2.2 201 생성됨)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f4da-174">See [10.2.2 201 Created](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html).</span></span>

### <a name="use-postman-to-send-a-create-request"></a><span data-ttu-id="0f4da-175">Postman을 사용하여 만들기 요청 보내기</span><span class="sxs-lookup"><span data-stu-id="0f4da-175">Use Postman to send a Create request</span></span>

* <span data-ttu-id="0f4da-176">앱을 시작합니다(**실행 > 디버깅 시작**).</span><span class="sxs-lookup"><span data-stu-id="0f4da-176">Start the app (**Run > Start With Debugging**).</span></span>
* <span data-ttu-id="0f4da-177">Postman을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-177">Start Postman.</span></span>

![Postman 콘솔](first-web-api/_static/pmc.png)

* <span data-ttu-id="0f4da-179">HTTP 메서드를 `POST`로 설정</span><span class="sxs-lookup"><span data-stu-id="0f4da-179">Set the HTTP method to `POST`</span></span>
* <span data-ttu-id="0f4da-180">**본문** 라디오 단추 선택</span><span class="sxs-lookup"><span data-stu-id="0f4da-180">Select the **Body** radio button</span></span>
* <span data-ttu-id="0f4da-181">**원시** 라디오 단추 선택</span><span class="sxs-lookup"><span data-stu-id="0f4da-181">Select the **raw** radio button</span></span>
* <span data-ttu-id="0f4da-182">형식을 JSON으로 설정</span><span class="sxs-lookup"><span data-stu-id="0f4da-182">Set the type to JSON</span></span>
* <span data-ttu-id="0f4da-183">키 값 편집기에서 다음과 같이 Todo 항목 입력</span><span class="sxs-lookup"><span data-stu-id="0f4da-183">In the key-value editor, enter a Todo item such as</span></span>

```json
{
    "name":"walk dog",
    "isComplete":true
}
```

* <span data-ttu-id="0f4da-184">**보내기** 선택</span><span class="sxs-lookup"><span data-stu-id="0f4da-184">Select **Send**</span></span>

* <span data-ttu-id="0f4da-185">아래쪽 창에서 [헤더] 탭을 선택하고 **위치** 헤더를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-185">Select the Headers tab in the lower pane and copy the **Location** header:</span></span>

![Postman 콘솔의 헤더 탭](first-web-api/_static/pmget.png)

<span data-ttu-id="0f4da-187">위치 헤더 URI를 사용하여 방금 만든 리소스에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-187">You can use the Location header URI to access the resource you just created.</span></span> <span data-ttu-id="0f4da-188">`GetById` 메서드에서 만들어진 `"GetTodo"` 경로를 회수합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-188">Recall the `GetById` method created the `"GetTodo"` named route:</span></span>

```csharp
[HttpGet("{id}", Name = "GetTodo")]
public IActionResult GetById(string id)
```

### <a name="update"></a><span data-ttu-id="0f4da-189">업데이트</span><span class="sxs-lookup"><span data-stu-id="0f4da-189">Update</span></span>

[!code-csharp[Main](first-web-api/sample/TodoApi/Controllers/TodoController.cs?name=snippet_Update)]

<span data-ttu-id="0f4da-190">`Update`는 `Create`와 비슷하지만 HTTP PUT을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-190">`Update` is similar to `Create`, but uses HTTP PUT.</span></span> <span data-ttu-id="0f4da-191">응답은 [204(콘텐츠 없음)](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)입니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-191">The response is [204 (No Content)](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html).</span></span> <span data-ttu-id="0f4da-192">HTTP 사양에 따라 PUT 요청의 경우 클라이언트는 델타만이 아니라 전체 업데이트된 엔터티를 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-192">According to the HTTP spec, a PUT request requires the client to send the entire updated entity, not just the deltas.</span></span> <span data-ttu-id="0f4da-193">부분 업데이트를 지원하려면 HTTP PATCH를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-193">To support partial updates, use HTTP PATCH.</span></span>

```json
{
  "key": 1,
  "name": "walk dog",
  "isComplete": true
}
```

![204(콘텐츠 없음) 응답을 보여주는 Postman 콘솔](first-web-api/_static/pmcput.png)

### <a name="delete"></a><span data-ttu-id="0f4da-195">삭제</span><span class="sxs-lookup"><span data-stu-id="0f4da-195">Delete</span></span>

[!code-csharp[Main](first-web-api/sample/TodoApi/Controllers/TodoController.cs?name=snippet_Delete)]

<span data-ttu-id="0f4da-196">응답은 [204(콘텐츠 없음)](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)입니다.</span><span class="sxs-lookup"><span data-stu-id="0f4da-196">The response is [204 (No Content)](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html).</span></span>

![204(콘텐츠 없음) 응답을 보여주는 Postman 콘솔](first-web-api/_static/pmd.png)

## <a name="next-steps"></a><span data-ttu-id="0f4da-198">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0f4da-198">Next steps</span></span>

* [<span data-ttu-id="0f4da-199">컨트롤러 작업에 라우팅</span><span class="sxs-lookup"><span data-stu-id="0f4da-199">Routing to Controller Actions</span></span>](xref:mvc/controllers/routing)
* <span data-ttu-id="0f4da-200">API 배포에 대한 자세한 내용은 [호스트 및 배포](xref:host-and-deploy/index)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f4da-200">For information about deploying your API, see [Host and deploy](xref:host-and-deploy/index).</span></span>
* <span data-ttu-id="0f4da-201">[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/first-web-api/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="0f4da-201">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/first-web-api/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>
* [<span data-ttu-id="0f4da-202">Postman</span><span class="sxs-lookup"><span data-stu-id="0f4da-202">Postman</span></span>](https://www.getpostman.com/)
* [<span data-ttu-id="0f4da-203">Fiddler</span><span class="sxs-lookup"><span data-stu-id="0f4da-203">Fiddler</span></span>](https://www.telerik.com/download/fiddler)
