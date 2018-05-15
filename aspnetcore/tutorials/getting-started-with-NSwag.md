---
title: NSwag 및 ASP.NET Core 시작
author: zuckerthoben
description: NSwag를 사용하여 ASP.NET Core Web API 앱에 대한 설명서 및 도움말 페이지를 생성하는 방법을 배웁니다.
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 03/15/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: tutorials/get-started-with-nswag
ms.openlocfilehash: 80e6a9e1702d8f68d139d2ff9c3a01a27c40cecb
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="get-started-with-nswag-and-aspnet-core"></a><span data-ttu-id="3e357-103">NSwag 및 ASP.NET Core 시작</span><span class="sxs-lookup"><span data-stu-id="3e357-103">Get started with NSwag and ASP.NET Core</span></span>

<span data-ttu-id="3e357-104">작성자: [Christoph Nienaber](https://twitter.com/zuckerthoben) 및 [Rico Suter](https://rsuter.com)</span><span class="sxs-lookup"><span data-stu-id="3e357-104">By [Christoph Nienaber](https://twitter.com/zuckerthoben) and [Rico Suter](https://rsuter.com)</span></span>

<span data-ttu-id="3e357-105">ASP.NET Core 미들웨어에서 [NSwag](https://github.com/RSuter/NSwag)를 사용하려면 [NSwag.AspNetCore](https://www.nuget.org/packages/NSwag.AspNetCore/) NuGet 패키지가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3e357-105">Using [NSwag](https://github.com/RSuter/NSwag) with ASP.NET Core middleware requires the [NSwag.AspNetCore](https://www.nuget.org/packages/NSwag.AspNetCore/) NuGet package.</span></span> <span data-ttu-id="3e357-106">이 패키지는 Swagger 생성기, Swagger UI(v2 및 v3) 및 [ReDoc UI](https://github.com/Rebilly/ReDoc)로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e357-106">The package consists of a Swagger generator, Swagger UI (v2 and v3), and [ReDoc UI](https://github.com/Rebilly/ReDoc).</span></span>

<span data-ttu-id="3e357-107">NSwag의 코드 생성 기능을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3e357-107">It's highly recommended to make use of NSwag's code generation capabilities.</span></span> <span data-ttu-id="3e357-108">코드 생성을 위해 다음 옵션 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3e357-108">Choose one of the following options for code generation:</span></span>

* <span data-ttu-id="3e357-109">API용 C# 및 TypeScript로 클라이언트 코드를 생성하는 Windows 데스크톱 앱인 [NSwagStudio](https://github.com/NSwag/NSwag/wiki/NSwagStudio) 사용</span><span class="sxs-lookup"><span data-stu-id="3e357-109">Use [NSwagStudio](https://github.com/NSwag/NSwag/wiki/NSwagStudio), a Windows desktop app for generating client code in C# and TypeScript for your API</span></span>
* <span data-ttu-id="3e357-110">프로젝트 내에서 코드 생성을 수행하기 위해 [NSwag.CodeGeneration.CSharp](https://www.nuget.org/packages/NSwag.CodeGeneration.CSharp/) 또는 [NSwag.CodeGeneration.TypeScript](https://www.nuget.org/packages/NSwag.CodeGeneration.TypeScript/) NuGet 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="3e357-110">Use the [NSwag.CodeGeneration.CSharp](https://www.nuget.org/packages/NSwag.CodeGeneration.CSharp/) or [NSwag.CodeGeneration.TypeScript](https://www.nuget.org/packages/NSwag.CodeGeneration.TypeScript/) NuGet packages to do code generation inside your project</span></span>
* <span data-ttu-id="3e357-111">[명령줄](https://github.com/NSwag/NSwag/wiki/CommandLine)에서 NSwag 사용</span><span class="sxs-lookup"><span data-stu-id="3e357-111">Use NSwag from the [command line](https://github.com/NSwag/NSwag/wiki/CommandLine)</span></span>
* <span data-ttu-id="3e357-112">[NSwag.MSBuild](https://github.com/NSwag/NSwag/wiki/MSBuild) NuGet 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="3e357-112">Use the [NSwag.MSBuild](https://github.com/NSwag/NSwag/wiki/MSBuild) NuGet package</span></span>

## <a name="features"></a><span data-ttu-id="3e357-113">기능</span><span class="sxs-lookup"><span data-stu-id="3e357-113">Features</span></span>

<span data-ttu-id="3e357-114">NSwag를 사용하는 주요 이유는 UI Swagger 및 Swagger 생성기를 도입할 뿐만 아니라 유연한 코드 생성 기능을 사용하기 위함입니다.</span><span class="sxs-lookup"><span data-stu-id="3e357-114">The main reason to use NSwag is the ability to not only introduce the Swagger UI and Swagger generator, but to make use of the flexible code generation capabilities.</span></span> <span data-ttu-id="3e357-115">기존 API가 필요하지 않으므로 Swagger를 통합하고 NSwag가 클라이언트 구현을 생성하도록 하는 타사 API를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e357-115">You don't need an existing API&mdash;you can use third-party APIs that incorporate Swagger and let NSwag generate a client implementation.</span></span> <span data-ttu-id="3e357-116">어느 쪽이든 개발 주기가 빠르며 API 변경에 보다 쉽게 대응할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e357-116">Either way, the development cycle is expedited and you can more easily adapt to API changes.</span></span>

## <a name="package-installation"></a><span data-ttu-id="3e357-117">패키지 설치</span><span class="sxs-lookup"><span data-stu-id="3e357-117">Package installation</span></span>

<span data-ttu-id="3e357-118">다음 방법으로 NSwag NuGet 패키지를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e357-118">The NSwag NuGet package can be added with the following approaches:</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="3e357-119">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3e357-119">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="3e357-120">**패키지 관리자 콘솔** 창에서:</span><span class="sxs-lookup"><span data-stu-id="3e357-120">From the **Package Manager Console** window:</span></span>

    ```powershell
    Install-Package NSwag.AspNetCore
    ```

* <span data-ttu-id="3e357-121">**NuGet 패키지 관리** 대화 상자에서:</span><span class="sxs-lookup"><span data-stu-id="3e357-121">From the **Manage NuGet Packages** dialog:</span></span>
  * <span data-ttu-id="3e357-122">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 > **NuGet 패키지 관리** 선택</span><span class="sxs-lookup"><span data-stu-id="3e357-122">Right-click your project in **Solution Explorer** > **Manage NuGet Packages**</span></span>
  * <span data-ttu-id="3e357-123">**패키지 소스**를 “nuget.org”로 설정</span><span class="sxs-lookup"><span data-stu-id="3e357-123">Set the **Package source** to "nuget.org"</span></span>
  * <span data-ttu-id="3e357-124">검색 상자에 “NSwag.AspNetCore” 입력</span><span class="sxs-lookup"><span data-stu-id="3e357-124">Enter "NSwag.AspNetCore" in the search box</span></span>
  * <span data-ttu-id="3e357-125">**찾아보기** 탭에서 "NSwag.AspNetCore" 패키지를 선택하고 **설치** 클릭</span><span class="sxs-lookup"><span data-stu-id="3e357-125">Select the "NSwag.AspNetCore" package from the **Browse** tab and click **Install**</span></span>

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="3e357-126">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="3e357-126">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

* <span data-ttu-id="3e357-127">**Solution Pad**에서 *Packages* 폴더를 마우스 오른쪽 단추로 클릭 > **패키지 추가...** 선택</span><span class="sxs-lookup"><span data-stu-id="3e357-127">Right-click the *Packages* folder in **Solution Pad** > **Add Packages...**</span></span>
* <span data-ttu-id="3e357-128">**패키지 추가** 창의 **소스** 드롭다운을 “nuget.org”로 설정</span><span class="sxs-lookup"><span data-stu-id="3e357-128">Set the **Add Packages** window's **Source** drop-down to "nuget.org"</span></span>
* <span data-ttu-id="3e357-129">검색 상자에 NSwag.AspNetCore 입력</span><span class="sxs-lookup"><span data-stu-id="3e357-129">Enter NSwag.AspNetCore in the search box</span></span>
* <span data-ttu-id="3e357-130">결과 창에서 NSwag.AspNetCore 패키지를 선택하고 **패키지 추가** 클릭</span><span class="sxs-lookup"><span data-stu-id="3e357-130">Select the NSwag.AspNetCore package from the results pane and click **Add Package**</span></span>

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="3e357-131">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="3e357-131">Visual Studio Code</span></span>](#tab/visual-studio-code)

<span data-ttu-id="3e357-132">**통합 터미널**에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3e357-132">Run the following command from the **Integrated Terminal**:</span></span>

```console
dotnet add TodoApi.NSwag.csproj package NSwag.AspNetCore
```

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="3e357-133">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="3e357-133">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="3e357-134">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3e357-134">Run the following command:</span></span>

```console
dotnet add TodoApi.NSwag.csproj package NSwag.AspNetCore
```

---

## <a name="add-and-configure-swagger-middleware"></a><span data-ttu-id="3e357-135">Swagger 미들웨어 추가 및 구성</span><span class="sxs-lookup"><span data-stu-id="3e357-135">Add and configure Swagger middleware</span></span>

<span data-ttu-id="3e357-136">`Info` 클래스에서 다음 네임스페이스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3e357-136">Import the following namespaces in the `Info` class:</span></span>

```csharp
using NSwag.AspNetCore;
using System.Reflection;
using NJsonSchema;
```

<span data-ttu-id="3e357-137">`Startup.Configure` 메서드에서 생성된 Swagger 사양 및 Swagger UI를 지원하기 위해 미들웨어를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3e357-137">In the `Startup.Configure` method, enable the middleware for serving the generated Swagger specification and the Swagger UI:</span></span>

[!code-cs[](../tutorials/web-api-help-pages-using-swagger/samples/TodoApi.NSwag/Startup.cs?name=snippet_Configure&highlight=4,7-10)]

<span data-ttu-id="3e357-138">앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3e357-138">Launch the app.</span></span> <span data-ttu-id="3e357-139">Swagger UI를 보려면 `/swagger`로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3e357-139">Navigate to `/swagger` to view the Swagger UI.</span></span> <span data-ttu-id="3e357-140">Swagger 사양을 보려면 `/swagger/v1/swagger.json`으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3e357-140">Navigate to `/swagger/v1/swagger.json` to view the Swagger specification.</span></span>

## <a name="code-generation"></a><span data-ttu-id="3e357-141">코드 생성</span><span class="sxs-lookup"><span data-stu-id="3e357-141">Code generation</span></span>

### <a name="via-nswagstudio"></a><span data-ttu-id="3e357-142">NSwagStudio를 통해</span><span class="sxs-lookup"><span data-stu-id="3e357-142">Via NSwagStudio</span></span>

* <span data-ttu-id="3e357-143">공식 [GitHub 리포지토리](https://github.com/RSuter/NSwag/wiki/NSwagStudio)에서 `NSwagStudio`를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3e357-143">Install `NSwagStudio` from the official [GitHub repository](https://github.com/RSuter/NSwag/wiki/NSwagStudio).</span></span>

* <span data-ttu-id="3e357-144">NSwagStudio를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3e357-144">Launch NSwagStudio.</span></span> <span data-ttu-id="3e357-145">*swagger.json*의 위치를 입력하거나 직접 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3e357-145">Enter the location of your *swagger.json* or copy it directly:</span></span>

![NSwagStudio](web-api-help-pages-using-swagger/_static/NSwagStudio.png)

* <span data-ttu-id="3e357-147">원하는 클라이언트 출력 유형을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3e357-147">Indicate the desired client output type.</span></span> <span data-ttu-id="3e357-148">옵션에는 **TypeScript 클라이언트**, **CSharp 클라이언트** 또는 **CSharp Web API 컨트롤러**가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e357-148">Options include **TypeScript Client**, **CSharp Client**, or **CSharp Web API Controller**.</span></span> <span data-ttu-id="3e357-149">Web API 컨트롤러를 사용할 경우 기본적으로 역방향으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e357-149">Using a Web API Controller is basically a reverse generation.</span></span> <span data-ttu-id="3e357-150">서비스의 사양을 사용하여 서비스가 다시 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e357-150">It uses a specification of a service to rebuild the service.</span></span>

* <span data-ttu-id="3e357-151">**출력 생성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e357-151">Click **Generate Outputs**.</span></span>

* <span data-ttu-id="3e357-152">여기서 C#으로 작성된 *TodoApi.NSwag* 샘플의 완전한 클라이언트 구현을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e357-152">Here you see a complete client implementation of the *TodoApi.NSwag* sample in C#:</span></span>

![NSwagStudio-Output](web-api-help-pages-using-swagger/_static/NSwagStudio-Output.png)

* <span data-ttu-id="3e357-154">파일을 클라이언트 프로젝트(예: [Xamarin.Forms](/xamarin/xamarin-forms/) 앱)에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="3e357-154">Put the file into a client project (for example, a [Xamarin.Forms](/xamarin/xamarin-forms/) app).</span></span> <span data-ttu-id="3e357-155">API 사용 시작:</span><span class="sxs-lookup"><span data-stu-id="3e357-155">Start consuming the API:</span></span>

```csharp
var todoClient = new TodoClient();

// Gets all Todos from the Api
var allTodos = await todoClient.GetAllAsync();

// Create a new TodoItem and save it in the Api
var createdTodo = await todoClient.CreateAsync(new TodoItem);

// Get a single Todo by Id
var foundTodo = await todoClient.GetByIdAsync(1);
```

> [!NOTE]
> <span data-ttu-id="3e357-156">기본 URL 및/또는 HTTP 클라이언트를 API 클라이언트에 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e357-156">You can inject a base URL and/or a HTTP client into the API client.</span></span> <span data-ttu-id="3e357-157">가장 좋은 방법은 항상 [HttpClient를 다시 사용](https://aspnetmonsters.com/2016/08/2016-08-27-httpclientwrong/)하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3e357-157">The best practice is to always [reuse the HttpClient](https://aspnetmonsters.com/2016/08/2016-08-27-httpclientwrong/).</span></span>

<span data-ttu-id="3e357-158">이제 클라이언트 프로젝트에 API를 쉽게 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e357-158">You can now start implementing your API into client projects easily.</span></span>

### <a name="other-ways-to-generate-client-code"></a><span data-ttu-id="3e357-159">클라이언트 코드를 생성하는 다른 방법</span><span class="sxs-lookup"><span data-stu-id="3e357-159">Other ways to generate client code</span></span>

<span data-ttu-id="3e357-160">워크플로에 더 적합한 다른 방법으로 코드를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e357-160">You can generate the code in other ways, more suited to your workflow:</span></span>

* [<span data-ttu-id="3e357-161">MSBuild</span><span class="sxs-lookup"><span data-stu-id="3e357-161">MSBuild</span></span>](https://www.nuget.org/packages/NSwag.MSBuild/)

* [<span data-ttu-id="3e357-162">코드 내</span><span class="sxs-lookup"><span data-stu-id="3e357-162">In code</span></span>](https://github.com/NSwag/NSwag/wiki/SwaggerToCSharpClientGenerator)

* [<span data-ttu-id="3e357-163">T4 템플릿</span><span class="sxs-lookup"><span data-stu-id="3e357-163">T4 templates</span></span>](https://github.com/NSwag/NSwag/wiki/T4)

## <a name="customization"></a><span data-ttu-id="3e357-164">사용자 지정</span><span class="sxs-lookup"><span data-stu-id="3e357-164">Customization</span></span>

### <a name="xml-comments"></a><span data-ttu-id="3e357-165">XML 주석</span><span class="sxs-lookup"><span data-stu-id="3e357-165">XML comments</span></span>

<span data-ttu-id="3e357-166">XML 주석은 다음과 같은 방법으로 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e357-166">XML comments are enabled with the following approaches:</span></span>

#### <a name="visual-studiotabvisual-studio-xml"></a>[<span data-ttu-id="3e357-167">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3e357-167">Visual Studio</span></span>](#tab/visual-studio-xml/)
* <span data-ttu-id="3e357-168">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성** 선택</span><span class="sxs-lookup"><span data-stu-id="3e357-168">Right-click the project in **Solution Explorer** and select **Properties**</span></span>
* <span data-ttu-id="3e357-169">**빌드** 탭의 **출력** 섹션에서 **XML 문서 파일** 상자 선택:</span><span class="sxs-lookup"><span data-stu-id="3e357-169">Check the **XML documentation file** box under the **Output** section of the **Build** tab:</span></span>

![프로젝트 속성의 빌드 탭](web-api-help-pages-using-swagger/_static/swagger-xml-comments.png)

#### <a name="visual-studio-for-mactabvisual-studio-mac-xml"></a>[<span data-ttu-id="3e357-171">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="3e357-171">Visual Studio for Mac</span></span>](#tab/visual-studio-mac-xml/)
* <span data-ttu-id="3e357-172">**프로젝트 옵션** 대화 상자 열기 > **빌드** > **컴파일러** 선택</span><span class="sxs-lookup"><span data-stu-id="3e357-172">Open the **Project Options** dialog > **Build** > **Compiler**</span></span>
* <span data-ttu-id="3e357-173">**일반 옵션** 섹션에서 **XML 문서 생성** 상자 선택:</span><span class="sxs-lookup"><span data-stu-id="3e357-173">Check the **Generate xml documentation** box under the **General Options** section:</span></span>

![프로젝트 옵션의 일반 옵션 섹션](web-api-help-pages-using-swagger/_static/swagger-xml-comments-mac.png)

#### <a name="visual-studio-codetabvisual-studio-code-xml"></a>[<span data-ttu-id="3e357-175">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="3e357-175">Visual Studio Code</span></span>](#tab/visual-studio-code-xml/)
<span data-ttu-id="3e357-176">*.csproj* 파일에 다음 코드 조각을 수동으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3e357-176">Manually add the following snippet to the *.csproj* file:</span></span>

[!code-xml[](../tutorials/web-api-help-pages-using-swagger/samples/TodoApi.NSwag/TodoApiNSwag.csproj?range=7-9)]

* * *
## <a name="data-annotations"></a><span data-ttu-id="3e357-177">데이터 주석</span><span class="sxs-lookup"><span data-stu-id="3e357-177">Data annotations</span></span>

<span data-ttu-id="3e357-178">NSwag는 [리플렉션](/dotnet/csharp/programming-guide/concepts/reflection)을 사용하며, Web API 작업의 가장 좋은 방법은 [IActionResult](/dotnet/api/microsoft.aspnetcore.mvc.iactionresult)를 반환하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3e357-178">NSwag uses [Reflection](/dotnet/csharp/programming-guide/concepts/reflection), and the best practice for Web API actions is to return [IActionResult](/dotnet/api/microsoft.aspnetcore.mvc.iactionresult).</span></span> <span data-ttu-id="3e357-179">따라서 NSwag는 사용자가 무슨 작업을 수행하고 반환하는지 유추할 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3e357-179">Consequently, NSwag can't infer what your action is doing and what it returns.</span></span> <span data-ttu-id="3e357-180">다음 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e357-180">Consider the following example:</span></span>

```csharp
public IActionResult Create([FromBody] TodoItem item)
{
    if (item == null)
    {
        return BadRequest();
    }

    _context.TodoItems.Add(item);
    _context.SaveChanges();

     return CreatedAtRoute("GetTodo", new { id = item.Id }, item);
}
```

<span data-ttu-id="3e357-181">이전 작업은 `IActionResult`를 반환하지만 작업 내에서는 [CreatedAtRoute](/dotnet/api/system.web.http.apicontroller.createdatroute) 또는 [BadRequest](/dotnet/api/system.web.http.apicontroller.badrequest)를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="3e357-181">The preceding action returns `IActionResult`, but inside the action it's returning either [CreatedAtRoute](/dotnet/api/system.web.http.apicontroller.createdatroute) or [BadRequest](/dotnet/api/system.web.http.apicontroller.badrequest).</span></span> <span data-ttu-id="3e357-182">데이터 주석은 이 작업이 반환하는 HTTP 응답을 클라이언트에 알리는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e357-182">Data annotations are used to tell clients which HTTP response this action is returning.</span></span> <span data-ttu-id="3e357-183">다음 특성으로 작업을 데코레이트하세요.</span><span class="sxs-lookup"><span data-stu-id="3e357-183">Decorate the action with the following attributes:</span></span>

```csharp
[HttpPost]
[ProducesResponseType(typeof(TodoItem), 201)] // Created
[ProducesResponseType(typeof(TodoItem), 400)] // BadRequest
public IActionResult Create([FromBody] TodoItem item)
```

<span data-ttu-id="3e357-184">이제 Swagger 생성기는 이 작업을 정확하게 설명할 수 있으며, 생성된 클라이언트가 엔드포인트를 호출할 때 수신한 내용을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e357-184">The Swagger generator can now accurately describe this action, and generated clients know what they receive when calling the endpoint.</span></span> <span data-ttu-id="3e357-185">이러한 특성으로 모든 작업을 데코레이트하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3e357-185">Decorating all actions with these attributes is highly recommended.</span></span> <span data-ttu-id="3e357-186">API 작업에서 반환해야 하는 HTTP 응답에 대한 지침은 [RFC 7231 사양](https://tools.ietf.org/html/rfc7231#section-4.3)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e357-186">For guidelines on what HTTP responses your API actions should return, see the [RFC 7231 specification](https://tools.ietf.org/html/rfc7231#section-4.3).</span></span>
