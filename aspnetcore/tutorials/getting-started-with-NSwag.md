---
title: NSwag 및 ASP.NET Core 시작
author: zuckerthoben
description: NSwag를 사용하여 ASP.NET Core Web API의 설명서 및 도움말 페이지를 생성하는 방법을 알아봅니다.
ms.author: scaddie
ms.custom: mvc
ms.date: 12/18/2018
uid: tutorials/get-started-with-nswag
ms.openlocfilehash: 8af5bed1e042c4f6d83043b05084c51b3064a548
ms.sourcegitcommit: ea215df889e89db44037a6ac2f01baede0450da9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2018
ms.locfileid: "53595362"
---
# <a name="get-started-with-nswag-and-aspnet-core"></a><span data-ttu-id="47a7c-103">NSwag 및 ASP.NET Core 시작</span><span class="sxs-lookup"><span data-stu-id="47a7c-103">Get started with NSwag and ASP.NET Core</span></span>

<span data-ttu-id="47a7c-104">작성자: [Christoph Nienaber](https://twitter.com/zuckerthoben) 및 [Rico Suter](https://rsuter.com)</span><span class="sxs-lookup"><span data-stu-id="47a7c-104">By [Christoph Nienaber](https://twitter.com/zuckerthoben) and [Rico Suter](https://rsuter.com)</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="47a7c-105">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.NSwag) ([다운로드 방법](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="47a7c-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.NSwag) ([how to download](xref:index#how-to-download-a-sample))</span></span>

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

<span data-ttu-id="47a7c-106">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.NSwag) ([다운로드 방법](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="47a7c-106">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.NSwag) ([how to download](xref:index#how-to-download-a-sample))</span></span>

::: moniker-end

<span data-ttu-id="47a7c-107">다음 작업을 수행하려면 NSwag 미들웨어를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-107">Register the NSwag middlewares to:</span></span>

* <span data-ttu-id="47a7c-108">구현된 Web API에 대한 Swagger 사양을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-108">Generate the Swagger specification for the implemented web API.</span></span>
* <span data-ttu-id="47a7c-109">Web API를 찾아보고 테스트하는 Swagger UI를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-109">Serve the Swagger UI to browse and test the web API.</span></span>

<span data-ttu-id="47a7c-110">[NSwag](https://github.com/RSuter/NSwag) ASP.NET Core 미들웨어를 사용하려면 [NSwag.AspNetCore](https://www.nuget.org/packages/NSwag.AspNetCore/) NuGet 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-110">To use the [NSwag](https://github.com/RSuter/NSwag) ASP.NET Core middlewares, install the [NSwag.AspNetCore](https://www.nuget.org/packages/NSwag.AspNetCore/) NuGet package.</span></span> <span data-ttu-id="47a7c-111">이 패키지에는 Swagger 사양, Swagger UI(v2 및 v3) 및 [ReDoc UI](https://github.com/Rebilly/ReDoc)를 생성하고 제공하는 미들웨어가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-111">This package contains the middlewares to generate and serve the Swagger specification, Swagger UI (v2 and v3), and [ReDoc UI](https://github.com/Rebilly/ReDoc).</span></span>

<span data-ttu-id="47a7c-112">또한 NSwag의 코드 생성 기능을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-112">Additionally, it's highly recommended to make use of NSwag's code generation capabilities.</span></span> <span data-ttu-id="47a7c-113">코드 생성 기능을 사용하려면 다음 옵션 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-113">Choose one of the following options to use the code generation capabilities:</span></span>

* <span data-ttu-id="47a7c-114">API에 C# 및 TypeScript로 클라이언트 코드를 생성하는 Windows 데스크톱 앱인 [NSwagStudio](https://github.com/NSwag/NSwag/wiki/NSwagStudio)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-114">Use [NSwagStudio](https://github.com/NSwag/NSwag/wiki/NSwagStudio), a Windows desktop app for generating client code in C# and TypeScript for your API.</span></span>
* <span data-ttu-id="47a7c-115">프로젝트 내에서 코드 생성을 수행하기 위해 [NSwag.CodeGeneration.CSharp](https://www.nuget.org/packages/NSwag.CodeGeneration.CSharp/) 또는 [NSwag.CodeGeneration.TypeScript](https://www.nuget.org/packages/NSwag.CodeGeneration.TypeScript/) NuGet 패키지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-115">Use the [NSwag.CodeGeneration.CSharp](https://www.nuget.org/packages/NSwag.CodeGeneration.CSharp/) or [NSwag.CodeGeneration.TypeScript](https://www.nuget.org/packages/NSwag.CodeGeneration.TypeScript/) NuGet packages to do code generation inside your project.</span></span>
* <span data-ttu-id="47a7c-116">[명령줄](https://github.com/NSwag/NSwag/wiki/CommandLine)에서 NSwag를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-116">Use NSwag from the [command line](https://github.com/NSwag/NSwag/wiki/CommandLine).</span></span>
* <span data-ttu-id="47a7c-117">[NSwag.MSBuild](https://github.com/NSwag/NSwag/wiki/MSBuild) NuGet 패키지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-117">Use the [NSwag.MSBuild](https://github.com/NSwag/NSwag/wiki/MSBuild) NuGet package.</span></span>

## <a name="features"></a><span data-ttu-id="47a7c-118">기능</span><span class="sxs-lookup"><span data-stu-id="47a7c-118">Features</span></span>

<span data-ttu-id="47a7c-119">NSwag를 사용하는 주요 이유는 Swagger UI 및 Swagger 생성기를 도입할 뿐만 아니라 유연한 코드 생성 기능을 이용할 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-119">The main reason to use NSwag is the ability to not only introduce the Swagger UI and Swagger generator, but to also make use of the flexible code generation capabilities.</span></span> <span data-ttu-id="47a7c-120">기존 API가 필요하지 않으므로 Swagger를 통합하고 NSwag가 클라이언트 구현을 생성하도록 하는 타사 API를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-120">You don't need an existing API&mdash;you can use third-party APIs that incorporate Swagger and let NSwag generate a client implementation.</span></span> <span data-ttu-id="47a7c-121">어느 쪽이든 개발 주기가 빠르며 API 변경에 보다 쉽게 대응할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-121">Either way, the development cycle is expedited and you can more easily adapt to API changes.</span></span>

## <a name="package-installation"></a><span data-ttu-id="47a7c-122">패키지 설치</span><span class="sxs-lookup"><span data-stu-id="47a7c-122">Package installation</span></span>

<span data-ttu-id="47a7c-123">다음 방법으로 NSwag NuGet 패키지를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-123">The NSwag NuGet package can be added with the following approaches:</span></span>

### <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="47a7c-124">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="47a7c-124">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="47a7c-125">**패키지 관리자 콘솔** 창에서:</span><span class="sxs-lookup"><span data-stu-id="47a7c-125">From the **Package Manager Console** window:</span></span>
  * <span data-ttu-id="47a7c-126">**보기** > **다른 창** > **패키지 관리자 콘솔**로 이동</span><span class="sxs-lookup"><span data-stu-id="47a7c-126">Go to **View** > **Other Windows** > **Package Manager Console**</span></span>
  * <span data-ttu-id="47a7c-127">*TodoApi.csproj* 파일이 위치한 디렉터리로 이동</span><span class="sxs-lookup"><span data-stu-id="47a7c-127">Navigate to the directory in which the *TodoApi.csproj* file exists</span></span>
  * <span data-ttu-id="47a7c-128">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-128">Execute the following command:</span></span>

    ```powershell
    Install-Package NSwag.AspNetCore
    ```

* <span data-ttu-id="47a7c-129">**NuGet 패키지 관리** 대화 상자에서:</span><span class="sxs-lookup"><span data-stu-id="47a7c-129">From the **Manage NuGet Packages** dialog:</span></span>
  * <span data-ttu-id="47a7c-130">**솔루션 탐색기** > **NuGet 패키지 관리**에서 프로젝트를 마우스 오른쪽 단추로 클릭</span><span class="sxs-lookup"><span data-stu-id="47a7c-130">Right-click the project in **Solution Explorer** > **Manage NuGet Packages**</span></span>
  * <span data-ttu-id="47a7c-131">**패키지 소스**를 “nuget.org”로 설정</span><span class="sxs-lookup"><span data-stu-id="47a7c-131">Set the **Package source** to "nuget.org"</span></span>
  * <span data-ttu-id="47a7c-132">검색 상자에 “NSwag.AspNetCore” 입력</span><span class="sxs-lookup"><span data-stu-id="47a7c-132">Enter "NSwag.AspNetCore" in the search box</span></span>
  * <span data-ttu-id="47a7c-133">**찾아보기** 탭에서 "NSwag.AspNetCore" 패키지를 선택하고 **설치** 클릭</span><span class="sxs-lookup"><span data-stu-id="47a7c-133">Select the "NSwag.AspNetCore" package from the **Browse** tab and click **Install**</span></span>

### <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="47a7c-134">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="47a7c-134">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

* <span data-ttu-id="47a7c-135">**Solution Pad**에서 *Packages* 폴더를 마우스 오른쪽 단추로 클릭 > **패키지 추가...** 선택</span><span class="sxs-lookup"><span data-stu-id="47a7c-135">Right-click the *Packages* folder in **Solution Pad** > **Add Packages...**</span></span>
* <span data-ttu-id="47a7c-136">**패키지 추가** 창의 **소스** 드롭다운을 “nuget.org”로 설정</span><span class="sxs-lookup"><span data-stu-id="47a7c-136">Set the **Add Packages** window's **Source** drop-down to "nuget.org"</span></span>
* <span data-ttu-id="47a7c-137">검색 상자에 “NSwag.AspNetCore” 입력</span><span class="sxs-lookup"><span data-stu-id="47a7c-137">Enter "NSwag.AspNetCore" in the search box</span></span>
* <span data-ttu-id="47a7c-138">결과 창에서 "NSwag.AspNetCore" 패키지를 선택하고 **패키지 추가** 클릭</span><span class="sxs-lookup"><span data-stu-id="47a7c-138">Select the "NSwag.AspNetCore" package from the results pane and click **Add Package**</span></span>

### <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="47a7c-139">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="47a7c-139">Visual Studio Code</span></span>](#tab/visual-studio-code)

<span data-ttu-id="47a7c-140">**통합 터미널**에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-140">Run the following command from the **Integrated Terminal**:</span></span>

```console
dotnet add TodoApi.csproj package NSwag.AspNetCore
```

### <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="47a7c-141">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="47a7c-141">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="47a7c-142">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-142">Run the following command:</span></span>

```console
dotnet add TodoApi.csproj package NSwag.AspNetCore
```

---

## <a name="add-and-configure-swagger-middleware"></a><span data-ttu-id="47a7c-143">Swagger 미들웨어 추가 및 구성</span><span class="sxs-lookup"><span data-stu-id="47a7c-143">Add and configure Swagger middleware</span></span>

<span data-ttu-id="47a7c-144">`Startup` 클래스에서 다음 네임스페이스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-144">Import the following namespaces in the `Startup` class:</span></span>

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.NSwag/Startup.cs?name=snippet_StartupConfigureImports)]

<span data-ttu-id="47a7c-145">`Startup.ConfigureServices` 메서드에서 필수 Swagger 서비스를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-145">In the `Startup.ConfigureServices` method, register the required Swagger services:</span></span> 

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.NSwag/Startup.cs?name=snippet_ConfigureServices&highlight=8)]

<span data-ttu-id="47a7c-146">`Startup.Configure` 메서드에서 미들웨어가 생성된 Swagger 사양 및 Swagger UI v3를 제공할 수 있도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-146">In the `Startup.Configure` method, enable the middleware for serving the generated Swagger specification and the Swagger UI v3:</span></span>

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.NSwag/Startup.cs?name=snippet_Configure&highlight=6-10)]

<span data-ttu-id="47a7c-147">앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-147">Launch the app.</span></span> <span data-ttu-id="47a7c-148">Swagger UI를 보려면 `http://localhost:<port>/swagger`로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-148">Navigate to `http://localhost:<port>/swagger` to view the Swagger UI.</span></span> <span data-ttu-id="47a7c-149">Swagger 사양을 보려면 `http://localhost:<port>/swagger/v1/swagger.json`으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-149">Navigate to `http://localhost:<port>/swagger/v1/swagger.json` to view the Swagger specification.</span></span>

## <a name="code-generation"></a><span data-ttu-id="47a7c-150">코드 생성</span><span class="sxs-lookup"><span data-stu-id="47a7c-150">Code generation</span></span>

### <a name="via-nswagstudio"></a><span data-ttu-id="47a7c-151">NSwagStudio를 통해</span><span class="sxs-lookup"><span data-stu-id="47a7c-151">Via NSwagStudio</span></span>

* <span data-ttu-id="47a7c-152">공식 [GitHub 리포지토리](https://github.com/RSuter/NSwag/wiki/NSwagStudio)에서 NSwagStudio를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-152">Install NSwagStudio from the official [GitHub repository](https://github.com/RSuter/NSwag/wiki/NSwagStudio).</span></span>
* <span data-ttu-id="47a7c-153">NSwagStudio를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-153">Launch NSwagStudio.</span></span> <span data-ttu-id="47a7c-154">**Swagger 사양 URL** 텍스트 상자에서 *swagger.json* 파일 URL을 입력하고, **로컬 복사본 만들기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-154">Enter the *swagger.json* file URL in the **Swagger Specification URL** textbox, and click the **Create local Copy** button.</span></span>
* <span data-ttu-id="47a7c-155">**CSharp 클라이언트** 클라이언트 출력 형식을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-155">Select the **CSharp Client** client output type.</span></span> <span data-ttu-id="47a7c-156">다른 옵션에는 **TypeScript 클라이언트** 및 **CSharp Web API 컨트롤러**가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-156">Other options include **TypeScript Client** and **CSharp Web API Controller**.</span></span> <span data-ttu-id="47a7c-157">Web API 컨트롤러를 사용할 경우 기본적으로 역방향으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-157">Using a Web API Controller is basically a reverse generation.</span></span> <span data-ttu-id="47a7c-158">서비스의 사양을 사용하여 서비스가 다시 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-158">It uses a specification of a service to rebuild the service.</span></span>
* <span data-ttu-id="47a7c-159">**출력 생성** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-159">Click the **Generate Outputs** button.</span></span> <span data-ttu-id="47a7c-160">*TodoApi.NSwag* 프로젝트의 완전한 C# 클라이언트 구현이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-160">A complete C# client implementation of the *TodoApi.NSwag* project is produced.</span></span> <span data-ttu-id="47a7c-161">**출력** 섹션의 **CSharp 클라이언트** 탭을 클릭하여 생성된 클라이언트 코드를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-161">Click the **CSharp Client** tab of the **Outputs** section to see the generated client code:</span></span>

```csharp
//----------------------
// <auto-generated>
//     Generated using the NSwag toolchain v11.17.3.0 (NJsonSchema v9.10.46.0 (Newtonsoft.Json v9.0.0.0)) (http://NSwag.org)
// </auto-generated>
//----------------------

namespace MyNamespace
{
    #pragma warning disable // Disable all warnings

    [System.CodeDom.Compiler.GeneratedCode("NSwag",
        "11.17.3.0 (NJsonSchema v9.10.46.0 (Newtonsoft.Json v9.0.0.0))")]
    public partial class TodoClient
    {
        private string _baseUrl = "http://localhost:50499";
        private System.Lazy<Newtonsoft.Json.JsonSerializerSettings> _settings;

        public TodoClient()
        {
            _settings = new System.Lazy
                <Newtonsoft.Json.JsonSerializerSettings>(() =>
            {
                var settings = new Newtonsoft.Json.JsonSerializerSettings();
                UpdateJsonSerializerSettings(settings);
                return settings;
            });
        }

        public string BaseUrl
        {
            get { return _baseUrl; }
            set { _baseUrl = value; }
        }

        // code omitted for brevity
```

> [!TIP]
> <span data-ttu-id="47a7c-162">C# 클라이언트 코드는 **CSharp 클라이언트** 탭의 **설정** 탭에 정의된 설정에 따라 생성됩니다. 기본 네임 스페이스 이름 바꾸기 및 동기 메서드 생성 등의 작업을 수행하도록 설정을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-162">The C# client code is generated based on settings defined in the **Settings** tab of the **CSharp Client** tab. Modify the settings to perform tasks such as default namespace renaming and synchronous method generation.</span></span>

* <span data-ttu-id="47a7c-163">생성된 C# 파일을 클라이언트 프로젝트(예: [Xamarin.Forms](/xamarin/xamarin-forms/) 앱)의 파일에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-163">Copy the generated C# code into a file in a client project (for example, a [Xamarin.Forms](/xamarin/xamarin-forms/) app).</span></span>
* <span data-ttu-id="47a7c-164">Web API를 사용하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-164">Start consuming the web API:</span></span>

```csharp
var todoClient = new TodoClient();

// Gets all to-dos from the API
var allTodos = await todoClient.GetAllAsync();

// Create a new TodoItem, and save it in the API
var createdTodo = await todoClient.CreateAsync(new TodoItem());

// Get a single to-do by ID
var foundTodo = await todoClient.GetByIdAsync(1);
```

> [!NOTE]
> <span data-ttu-id="47a7c-165">기본 URL 및/또는 HTTP 클라이언트를 API 클라이언트에 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-165">You can inject a base URL and/or a HTTP client into the API client.</span></span> <span data-ttu-id="47a7c-166">가장 좋은 방법은 항상 [HttpClient를 다시 사용](https://aspnetmonsters.com/2016/08/2016-08-27-httpclientwrong/)하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-166">The best practice is to always [reuse the HttpClient](https://aspnetmonsters.com/2016/08/2016-08-27-httpclientwrong/).</span></span>

### <a name="other-ways-to-generate-client-code"></a><span data-ttu-id="47a7c-167">클라이언트 코드를 생성하는 다른 방법</span><span class="sxs-lookup"><span data-stu-id="47a7c-167">Other ways to generate client code</span></span>

<span data-ttu-id="47a7c-168">워크플로에 더 적합한 다른 방법으로 클라이언트 코드를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-168">You can generate the client code in other ways, more suited to your workflow:</span></span>

* [<span data-ttu-id="47a7c-169">MSBuild</span><span class="sxs-lookup"><span data-stu-id="47a7c-169">MSBuild</span></span>](https://www.nuget.org/packages/NSwag.MSBuild/)

* [<span data-ttu-id="47a7c-170">코드 내</span><span class="sxs-lookup"><span data-stu-id="47a7c-170">In code</span></span>](https://github.com/NSwag/NSwag/wiki/SwaggerToCSharpClientGenerator)

* [<span data-ttu-id="47a7c-171">T4 템플릿</span><span class="sxs-lookup"><span data-stu-id="47a7c-171">T4 templates</span></span>](https://github.com/NSwag/NSwag/wiki/T4)

## <a name="customize"></a><span data-ttu-id="47a7c-172">사용자 지정</span><span class="sxs-lookup"><span data-stu-id="47a7c-172">Customize</span></span>

<span data-ttu-id="47a7c-173">Swagger는 Web API를 보다 쉽게 사용하도록 개체 모델을 문서화하는 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-173">Swagger provides options for documenting the object model to ease consumption of the web API.</span></span>

### <a name="api-info-and-description"></a><span data-ttu-id="47a7c-174">API 정보 및 설명</span><span class="sxs-lookup"><span data-stu-id="47a7c-174">API info and description</span></span>

<span data-ttu-id="47a7c-175">`Startup.Configure` 메서드에서 `UseSwagger` 메서드에 전달되는 구성 작업은 작성자, 라이선스 및 설명과 같은 정보를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-175">In the `Startup.Configure` method, a configuration action passed to the `UseSwagger` method adds information such as the author, license, and description:</span></span>

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.NSwag/Startup2.cs?name=snippet_UseSwagger)]

<span data-ttu-id="47a7c-176">Swagger UI는 버전의 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-176">The Swagger UI displays the version's information:</span></span>

![버전 정보를 포함한 Swagger UI](web-api-help-pages-using-swagger/_static/custom-info-nswag.png)

### <a name="xml-comments"></a><span data-ttu-id="47a7c-178">XML 주석</span><span class="sxs-lookup"><span data-stu-id="47a7c-178">XML comments</span></span>

<span data-ttu-id="47a7c-179">XML 주석은 다음과 같은 방법으로 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-179">XML comments are enabled with the following approaches:</span></span>

# <a name="visual-studiotabvisual-studio-xml"></a>[<span data-ttu-id="47a7c-180">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="47a7c-180">Visual Studio</span></span>](#tab/visual-studio-xml/)

::: moniker range=">= aspnetcore-2.0"

* <span data-ttu-id="47a7c-181">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **<project_name>.csproj 편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-181">Right-click the project in **Solution Explorer** and select **Edit <project_name>.csproj**.</span></span>
* <span data-ttu-id="47a7c-182">강조 표시된 줄을 *.csproj* 파일에 수동으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-182">Manually add the highlighted lines to the *.csproj* file:</span></span>

[!code-xml[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.NSwag/TodoApi.csproj?name=snippet_DocumentationFileElement&highlight=1-2,4)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

* <span data-ttu-id="47a7c-183">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성** 선택</span><span class="sxs-lookup"><span data-stu-id="47a7c-183">Right-click the project in **Solution Explorer** and select **Properties**</span></span>
* <span data-ttu-id="47a7c-184">**빌드** 탭의 **출력** 섹션에서 **XML 문서 파일** 상자 선택</span><span class="sxs-lookup"><span data-stu-id="47a7c-184">Check the **XML documentation file** box under the **Output** section of the **Build** tab</span></span>

::: moniker-end

# <a name="visual-studio-for-mactabvisual-studio-mac-xml"></a>[<span data-ttu-id="47a7c-185">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="47a7c-185">Visual Studio for Mac</span></span>](#tab/visual-studio-mac-xml/)

::: moniker range=">= aspnetcore-2.0"

* <span data-ttu-id="47a7c-186">*Solution Pad*에서 **control** 키를 누르고 프로젝트 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-186">From the *Solution Pad*, press **control** and click the project name.</span></span> <span data-ttu-id="47a7c-187">**도구** > **파일 편집**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-187">Navigate to **Tools** > **Edit File**.</span></span>
* <span data-ttu-id="47a7c-188">강조 표시된 줄을 *.csproj* 파일에 수동으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-188">Manually add the highlighted lines to the *.csproj* file:</span></span>

[!code-xml[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.NSwag/TodoApi.csproj?name=snippet_DocumentationFileElement&highlight=1-2,4)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

* <span data-ttu-id="47a7c-189">**프로젝트 옵션** 대화 상자 > **빌드** > **컴파일러**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-189">Open the **Project Options** dialog > **Build** > **Compiler**</span></span>
* <span data-ttu-id="47a7c-190">**일반 옵션** 섹션에서 **XML 문서 생성** 상자 선택</span><span class="sxs-lookup"><span data-stu-id="47a7c-190">Check the **Generate xml documentation** box under the **General Options** section</span></span>

::: moniker-end

# <a name="visual-studio-codetabvisual-studio-code-xml"></a>[<span data-ttu-id="47a7c-191">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="47a7c-191">Visual Studio Code</span></span>](#tab/visual-studio-code-xml/)

<span data-ttu-id="47a7c-192">강조 표시된 줄을 *.csproj* 파일에 수동으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-192">Manually add the highlighted lines to the *.csproj* file:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-xml[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.NSwag/TodoApi.csproj?name=snippet_DocumentationFileElement&highlight=1-2,4)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

[!code-xml[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.NSwag/TodoApi.csproj?name=snippet_DocumentationFileElement&highlight=1-2,4)]

::: moniker-end

---

### <a name="data-annotations"></a><span data-ttu-id="47a7c-193">데이터 주석</span><span class="sxs-lookup"><span data-stu-id="47a7c-193">Data annotations</span></span>

::: moniker range="<= aspnetcore-2.0"

<span data-ttu-id="47a7c-194">NSwag는 [리플렉션](/dotnet/csharp/programming-guide/concepts/reflection)을 사용하며, Web API 작업의 가장 좋은 반환 형식은 [IActionResult](/dotnet/api/microsoft.aspnetcore.mvc.iactionresult)입니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-194">NSwag uses [Reflection](/dotnet/csharp/programming-guide/concepts/reflection), and the recommended return type for web API actions is [IActionResult](/dotnet/api/microsoft.aspnetcore.mvc.iactionresult).</span></span> <span data-ttu-id="47a7c-195">따라서 NSwag는 사용자가 무슨 작업을 수행하고 반환하는지 유추할 없습니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-195">Consequently, NSwag can't infer what your action is doing and what it returns.</span></span> <span data-ttu-id="47a7c-196">다음 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47a7c-196">Consider the following example:</span></span>

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.NSwag/Controllers/TodoController.cs?name=snippet_CreateAction)]

<span data-ttu-id="47a7c-197">이전 작업은 `IActionResult`를 반환하지만 작업 내에서는 [CreatedAtRoute](/dotnet/api/system.web.http.apicontroller.createdatroute) 또는 [BadRequest](/dotnet/api/system.web.http.apicontroller.badrequest)를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-197">The preceding action returns `IActionResult`, but inside the action it's returning either [CreatedAtRoute](/dotnet/api/system.web.http.apicontroller.createdatroute) or [BadRequest](/dotnet/api/system.web.http.apicontroller.badrequest).</span></span> <span data-ttu-id="47a7c-198">데이터 주석을 사용하여 이 작업이 반환하는 것으로 알려진 HTTP 상태 코드를 클라이언트에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-198">Data annotations are used to tell clients which HTTP status codes this action is known to return.</span></span> <span data-ttu-id="47a7c-199">다음 특성으로 작업을 데코레이트하세요.</span><span class="sxs-lookup"><span data-stu-id="47a7c-199">Decorate the action with the following attributes:</span></span>

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.NSwag/Controllers/TodoController.cs?name=snippet_CreateActionAttributes)]

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="47a7c-200">NSwag는 [리플렉션](/dotnet/csharp/programming-guide/concepts/reflection)을 사용하며, Web API 작업의 가장 좋은 반환 형식은 [ActionResult\<T>](/dotnet/api/microsoft.aspnetcore.mvc.actionresult-1)입니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-200">NSwag uses [Reflection](/dotnet/csharp/programming-guide/concepts/reflection), and the recommended return type for web API actions is [ActionResult\<T>](/dotnet/api/microsoft.aspnetcore.mvc.actionresult-1).</span></span> <span data-ttu-id="47a7c-201">따라서 NSwag만이 `T`에서 정의한 반환 형식을 유추할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-201">Consequently, NSwag can only infer the return type defined by `T`.</span></span> <span data-ttu-id="47a7c-202">작업에서 가능한 다른 반환 형식은 유추할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-202">Other possible return types in the action cannot be inferred.</span></span> <span data-ttu-id="47a7c-203">다음 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47a7c-203">Consider the following example:</span></span>

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.NSwag/Controllers/TodoController.cs?name=snippet_CreateAction)]

<span data-ttu-id="47a7c-204">이전 작업이 `ActionResult<T>`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-204">The preceding action returns `ActionResult<T>`.</span></span> <span data-ttu-id="47a7c-205">작업 내에서 [CreatedAtRoute](xref:System.Web.Http.ApiController.CreatedAtRoute*)를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-205">Inside the action, it's returning [CreatedAtRoute](xref:System.Web.Http.ApiController.CreatedAtRoute*).</span></span> <span data-ttu-id="47a7c-206">컨트롤러가 [[ApiController]](xref:Microsoft.AspNetCore.Mvc.ApiControllerAttribute) 특성을 사용하여 데코레이트되므로 [BadRequest](xref:System.Web.Http.ApiController.BadRequest*) 응답도 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-206">Since the controller is decorated with the [[ApiController]](xref:Microsoft.AspNetCore.Mvc.ApiControllerAttribute) attribute, a [BadRequest](xref:System.Web.Http.ApiController.BadRequest*) response is possible, too.</span></span> <span data-ttu-id="47a7c-207">자세한 정보는 [자동 HTTP 400 응답](xref:web-api/index#automatic-http-400-responses)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47a7c-207">For more information, see [Automatic HTTP 400 responses](xref:web-api/index#automatic-http-400-responses).</span></span> <span data-ttu-id="47a7c-208">데이터 주석을 사용하여 이 작업이 반환하는 것으로 알려진 HTTP 상태 코드를 클라이언트에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-208">Data annotations are used to tell clients which HTTP status codes this action is known to return.</span></span> <span data-ttu-id="47a7c-209">다음 특성으로 작업을 데코레이트하세요.</span><span class="sxs-lookup"><span data-stu-id="47a7c-209">Decorate the action with the following attributes:</span></span>

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.NSwag/Controllers/TodoController.cs?name=snippet_CreateActionAttributes)]

<span data-ttu-id="47a7c-210">ASP.NET Core 2.2 이상에서는 `[ProducesResponseType]`을 사용하여 명시적으로 개별 작업을 데코레이팅하는 대신 규칙을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-210">In ASP.NET Core 2.2 or later, conventions can be used as an alternative to explicitly decorating individual actions with `[ProducesResponseType]`.</span></span> <span data-ttu-id="47a7c-211">자세한 내용은 <xref:web-api/advanced/conventions>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47a7c-211">For more information, see <xref:web-api/advanced/conventions>.</span></span>

::: moniker-end

<span data-ttu-id="47a7c-212">이제 Swagger 생성기는 이 작업을 정확하게 설명할 수 있으며, 생성된 클라이언트가 엔드포인트를 호출할 때 수신한 내용을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-212">The Swagger generator can now accurately describe this action, and generated clients know what they receive when calling the endpoint.</span></span> <span data-ttu-id="47a7c-213">이러한 특성으로 모든 작업을 데코레이트하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="47a7c-213">Decorating all actions with these attributes is highly recommended.</span></span> <span data-ttu-id="47a7c-214">API 작업에서 반환해야 하는 HTTP 응답에 대한 지침은 [RFC 7231 사양](https://tools.ietf.org/html/rfc7231#section-4.3)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47a7c-214">For guidelines on what HTTP responses your API actions should return, see the [RFC 7231 specification](https://tools.ietf.org/html/rfc7231#section-4.3).</span></span>
