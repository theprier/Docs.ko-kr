---
title: 첫 번째 Blazor 앱 빌드
author: guardrex
description: Blazor 앱을 단계별로 빌드하고 Razor 구성 요소 프레임워크의 기본 기능을 빠르게 알아봅니다.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 01/29/2019
uid: tutorials/first-blazor-app
ms.openlocfilehash: 99396e200eb121524abccc20a7d461062c94ecc7
ms.sourcegitcommit: ed76cc752966c604a795fbc56d5a71d16ded0b58
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/02/2019
ms.locfileid: "55668031"
---
# <a name="build-your-first-blazor-app"></a><span data-ttu-id="d56b6-103">첫 번째 Blazor 앱 빌드</span><span class="sxs-lookup"><span data-stu-id="d56b6-103">Build your first Blazor app</span></span>

[!INCLUDE[](~/includes/razor-components-preview-notice.md)]

<span data-ttu-id="d56b6-104">이 자습서에서는 Blazor 앱을 단계별로 빌드하고 Razor 구성 요소 프레임워크의 기본 기능을 빠르게 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-104">In this tutorial, you build a Blazor app step-by-step and quickly learn the basic features of the Razor Components framework.</span></span>

<span data-ttu-id="d56b6-105">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/build-your-first-blazor-app/samples/) ([다운로드 방법](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="d56b6-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/build-your-first-blazor-app/samples/) ([how to download](xref:index#how-to-download-a-sample)).</span></span> <span data-ttu-id="d56b6-106">필수 구성 요소는 [시작](xref:razor-components/get-started) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d56b6-106">See the [Get started](xref:razor-components/get-started) topic for prerequisites.</span></span>

<span data-ttu-id="d56b6-107">Visual Studio에서 프로젝트를 만들려면:</span><span class="sxs-lookup"><span data-stu-id="d56b6-107">To create the project in Visual Studio:</span></span>

1. <span data-ttu-id="d56b6-108">**파일** > **새로 만들기** > **프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-108">Select **File** > **New** > **Project**.</span></span> <span data-ttu-id="d56b6-109">**웹** > **ASP.NET Core 웹 애플리케이션**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-109">Select **Web** > **ASP.NET Core Web Application**.</span></span> <span data-ttu-id="d56b6-110">**Name** 필드에 프로젝트 이름을 "BlazorApp1"로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-110">Name the project "BlazorApp1" in the **Name** field.</span></span> <span data-ttu-id="d56b6-111">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-111">Select **OK**.</span></span>

    ![새 ASP.NET Core 프로젝트](build-your-first-blazor-app/_static/new-aspnet-core-project.png)

1. <span data-ttu-id="d56b6-113">**새 ASP.NET Core 웹 애플리케이션** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-113">The **New ASP.NET Core Web Application** dialog appears.</span></span> <span data-ttu-id="d56b6-114">맨 위에 있는 **.NET Core**가 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-114">Make sure **.NET Core** is selected at the top.</span></span> <span data-ttu-id="d56b6-115">**ASP.NET Core 2.1**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-115">Select **ASP.NET Core 2.1**.</span></span> <span data-ttu-id="d56b6-116">**Blazor** 템플릿을 선택하고 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-116">Choose the **Blazor** template and select **OK**.</span></span>

    ![새 Blazor 앱 대화 상자](build-your-first-blazor-app/_static/new-blazor-app-dialog.png)

1. <span data-ttu-id="d56b6-118">프로젝트가 생성되면 **Ctrl-F5**를 눌러 *디버거 없이* 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-118">Once the project is created, press **Ctrl-F5** to run the app *without the debugger*.</span></span> <span data-ttu-id="d56b6-119">디버거로 실행(**F5**)하는 것은 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-119">Running with the debugger (**F5**) isn't supported at this time.</span></span>

> [!NOTE]
> <span data-ttu-id="d56b6-120">Visual Studio를 사용하지 않는 경우 Windows, macOS 또는 Linux의 명령 프롬프트에서 Blazor 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-120">If not using Visual Studio, create the Blazor app at a command prompt on Windows, macOS, or Linux:</span></span>
>
> ```console
> dotnet new --install "Microsoft.AspNetCore.Blazor.Templates"
> dotnet new blazor -o BlazorApp1
> cd BlazorApp1
> dotnet run
> ```
>
> <span data-ttu-id="d56b6-121">`dotnet run`이 실행된 후 콘솔 창 출력에 제공된 localhost 주소 및 포트를 사용하여 앱으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-121">Navigate to the app using the localhost address and port provided in the console window output after `dotnet run` is executed.</span></span> <span data-ttu-id="d56b6-122">콘솔 창에 **Ctrl-C**를 사용하여 앱을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-122">Use **Ctrl-C** in the console window to shutdown the app.</span></span>

<span data-ttu-id="d56b6-123">Blazor 앱은 브라우저에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-123">The Blazor app runs in the browser:</span></span>

![Blazor 앱 홈페이지](https://user-images.githubusercontent.com/1874516/39509497-5515c3ea-4d9b-11e8-887f-019ea4fdb3ee.png)

## <a name="build-components"></a><span data-ttu-id="d56b6-125">구성 요소 빌드</span><span class="sxs-lookup"><span data-stu-id="d56b6-125">Build components</span></span>

1. <span data-ttu-id="d56b6-126">각 앱의 세 페이지로 이동합니다. 홈, 카운터 및 Fetch 데이터.</span><span class="sxs-lookup"><span data-stu-id="d56b6-126">Browse to each of the app's three pages: Home, Counter, and Fetch data.</span></span>

    <span data-ttu-id="d56b6-127">이러한 세 페이지는 *페이지* 폴더에 있는 세 개의 Razor 파일로 구현됩니다. *Index.cshtml*, *Counter.cshtml* 및 *FetchData.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="d56b6-127">These three pages are implemented by the three Razor files in the *Pages* folder: *Index.cshtml*, *Counter.cshtml*, and *FetchData.cshtml*.</span></span> <span data-ttu-id="d56b6-128">이러한 파일은 각각 브라우저에서 클라이언 쪽을 컴파일하고 실행하는 구성 요소를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-128">Each of these files implements a component that's compiled and executed client-side in the browser.</span></span>

1. <span data-ttu-id="d56b6-129">카운터 페이지에서 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-129">Select the button on the Counter page.</span></span>

    ![Blazor 앱 홈페이지](https://user-images.githubusercontent.com/1874516/39509525-6e367c66-4d9b-11e8-9978-e52a9750c34b.png)

    <span data-ttu-id="d56b6-131">단추를 선택할 때마다 페이지 새로 고침 없이 카운터가 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-131">Each time the button is selected, the counter is incremented without a page refresh.</span></span> <span data-ttu-id="d56b6-132">일반적으로 이러한 종류의 클라이언트 쪽 동작은 JavaScript에서 처리됩니다. 하지만 여기서는 C# 및 .NET의 `Counter` 구성 요소로 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-132">Normally, this kind of client-side behavior is handled in JavaScript; but here, it's implemented in C# and .NET by the `Counter` component.</span></span>

1. <span data-ttu-id="d56b6-133">*Counter.cshtml* 파일에서 `Counter` 구성 요소의 구현을 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="d56b6-133">Take a look at the implementation of the `Counter` component in the *Counter.cshtml* file:</span></span>

    ```cshtml
    @page "/counter"

    <h1>Counter</h1>

    <p>Current count: @currentCount</p>

    <button class="btn btn-primary" onclick="@IncrementCount">Click me</button>

    @functions {
        int currentCount = 0;

        void IncrementCount()
        {
            currentCount++;
        }
    }
    ```

    <span data-ttu-id="d56b6-134">`Counter` 구성 요소의 UI는 일반 HTML을 사용하여 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-134">The UI for the `Counter` component is defined using normal HTML.</span></span> <span data-ttu-id="d56b6-135">동적 렌더링 논리(예: 루프, 조건, 식)는 [Razor](https://docs.microsoft.com/aspnet/core/mvc/views/razor)라는 포함된 C# 구문을 사용하여 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-135">Dynamic rendering logic (for example, loops, conditionals, expressions) is added using an embedded C# syntax called [Razor](https://docs.microsoft.com/aspnet/core/mvc/views/razor).</span></span> <span data-ttu-id="d56b6-136">HTML 태그 및 C# 렌더링 논리는 빌드 시 구성 요소 클래스로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-136">The HTML markup and C# rendering logic are converted into a component class at build time.</span></span> <span data-ttu-id="d56b6-137">생성된 .NET 클래스의 이름은 파일 이름과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-137">The name of the generated .NET class matches the name of the file.</span></span>

    <span data-ttu-id="d56b6-138">구성 요소 클래스의 멤버는 `@functions` 블록에 정의되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-138">Members of the component class are defined in a `@functions` block.</span></span> <span data-ttu-id="d56b6-139">`@functions` 블록에서 구성 요소 상태(속성, 필드) 및 메서드는 이벤트 처리 또는 기타 구성 요소를 정의하기 위해 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-139">In the `@functions` block, component state (properties, fields) and methods can be specified for event handling or for defining other component logic.</span></span> <span data-ttu-id="d56b6-140">그런 다음, 이러한 멤버를 구성 요소의 렌더링 논리의 일부 및 이벤트 처리에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-140">These members can then be used as part of the component's rendering logic and for handling events.</span></span>

    <span data-ttu-id="d56b6-141">단추를 선택하면 `Counter` 구성 요소의 등록된 `onclick` 처리기가 호출(`IncrementCount` 메서드)되고 `Counter` 구성 요소가 해당 렌더링 트리를 다시 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-141">When the button is selected, the `Counter` component's registered `onclick` handler is called (the `IncrementCount` method) and the `Counter` component regenerates its render tree.</span></span> <span data-ttu-id="d56b6-142">Blazor는 새로운 렌더링 트리를 이전 렌터링 트리와 비교하여 수정 사항을 브라우저 DOM(문서 개체 모델)에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-142">Blazor compares the new render tree against the previous one and applies any modifications to the browser Document Object Model (DOM).</span></span> <span data-ttu-id="d56b6-143">표시된 개수가 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-143">The displayed count is updated.</span></span>

1. <span data-ttu-id="d56b6-144">`Counter` 구성 요소의 태그를 업데이트하여 최상위 헤더를 더 *흥미롭게* 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-144">Update the markup for the `Counter` component to make the top-level header more *exciting*.</span></span>

    ```cshtml
    @page "/counter"
    <h1><em>Counter!!</em></h1>
    ```

1. <span data-ttu-id="d56b6-145">또한 `Counter` 구성 요소의 C# 논리를 수정하여 카운트를 하나 대신 둘씩 증가하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-145">Also modify the C# logic of the `Counter` component to make the count increment by two instead of one.</span></span>

    ```cshtml
    @functions {
        int currentCount = 0;

        void IncrementCount()
        {
            currentCount += 2;
        }
    }
    ```

1. <span data-ttu-id="d56b6-146">변경 내용을 보려면 브라우저에서 카운터 페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-146">Refresh the counter page in the browser to see the changes.</span></span>

    ![흥미로운 카운터](https://user-images.githubusercontent.com/1874516/39509668-e8949a92-4d9b-11e8-91e9-b6a494695d92.png)

## <a name="use-components"></a><span data-ttu-id="d56b6-148">구성 요소 사용</span><span class="sxs-lookup"><span data-stu-id="d56b6-148">Use components</span></span>

<span data-ttu-id="d56b6-149">구성 요소를 정의한 후에는 구성 요소를 다른 구성 요소로 구현하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-149">After a component is defined, the component can be used to implement other components.</span></span> <span data-ttu-id="d56b6-150">구성 요소 사용을 위한 태그는 태그 이름이 구성 요소 유형인 HTML 태그처럼 보입니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-150">The markup for using a component looks like an HTML tag where the name of the tag is the component type.</span></span>

1. <span data-ttu-id="d56b6-151">앱의 홈페이지(*Index.cshtml*)에 `Counter` 구성 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-151">Add a `Counter` component to the Home page of the app (*Index.cshtml*).</span></span>

    ```cshtml
    @page "/"

    <h1>Hello, world!</h1>

    Welcome to your new app.

    <SurveyPrompt Title="How is Blazor working for you?" />

    <Counter />
    ```

1. <span data-ttu-id="d56b6-152">브라우저에서 홈페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-152">Refresh the home page in the browser.</span></span> <span data-ttu-id="d56b6-153">홈페이지에서 `Counter` 구성 요소의 개별 인스턴스를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-153">Note the separate instance of the `Counter` component on the Home page.</span></span>

    ![카운터가 있는 Blazor 홈페이지](https://user-images.githubusercontent.com/1874516/39509718-224483f6-4d9c-11e8-9030-b4c7228d669d.png)

## <a name="component-parameters"></a><span data-ttu-id="d56b6-155">구성 요소 매개 변수</span><span class="sxs-lookup"><span data-stu-id="d56b6-155">Component parameters</span></span>

<span data-ttu-id="d56b6-156">구성 요소에는 `[Parameter]`로 데코레이팅된 구성 요소 클래스의 전송 속성을 사용하여 정의된 매개 변수가 있을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-156">Components can also have parameters, which are defined using private properties on the component class decorated with `[Parameter]`.</span></span> <span data-ttu-id="d56b6-157">특성을 사용하여 태그에서 구성 요소의 인수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-157">Use attributes to specify arguments for a component in markup.</span></span> 

1. <span data-ttu-id="d56b6-158">`Counter` 구성 요소를 업데이트하여 기본값이 1인 `IncrementAmount` 매개 변수를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-158">Update the `Counter` component to have an `IncrementAmount` parameter that defaults to 1.</span></span>

    ```cshtml
    @functions {
        int currentCount = 0;

        [Parameter]
        private int IncrementAmount { get; set; } = 1;

        void IncrementCount()
        {
            currentCount += IncrementAmount;
        }
    }
    ```

    > [!NOTE]
    > <span data-ttu-id="d56b6-159">Visual Studio에서 `para` 조각을 사용하여 구성 요소 매개 변수를 빠르게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-159">From Visual Studio, you can quickly add a component parameter by using the `para` snippet.</span></span> <span data-ttu-id="d56b6-160">`para`를 입력한 다음, `Tab` 키를 두 번 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-160">Type `para` and then press the `Tab` key twice.</span></span>

1. <span data-ttu-id="d56b6-161">홈페이지(*Index.cshtml*)에서 `IncrementCount`에 대한 구성 요소 속성 이름과 일치하는 특성을 설정하여 `Counter`의 증분량을 10으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-161">On the Home page (*Index.cshtml*), change the increment amount for the `Counter` to 10 by setting an attribute that matches the name of the component's property for `IncrementCount`.</span></span>

    ```cshtml
    <Counter IncrementAmount="10" />
    ```

1. <span data-ttu-id="d56b6-162">페이지를 다시 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-162">Reload the page.</span></span>

    <span data-ttu-id="d56b6-163">홈 페이지의 카운터는 이제 10씩 증가하지만 카운터 페이지의 카운터는 여전히 1씩 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-163">The counter on the Home page now increments by 10, while the counter on the Counter page still increments by 1.</span></span>

    ![Blazor 개수 10](https://user-images.githubusercontent.com/1874516/39509798-618f0720-4d9c-11e8-9125-3d4c634dff46.png)

## <a name="route-to-components"></a><span data-ttu-id="d56b6-165">구성 요소 경로</span><span class="sxs-lookup"><span data-stu-id="d56b6-165">Route to components</span></span>

<span data-ttu-id="d56b6-166">*Counter.cshtml* 파일 맨 위에 있는 `@page` 지시문은 이 구성 요소가 요청을 라우팅할 수 있는 페이지임을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-166">The `@page` directive at the top of the *Counter.cshtml* file specifies that this component is a page to which requests can be routed.</span></span> <span data-ttu-id="d56b6-167">특히 `Counter` 구성 요소는 `/Counter`에 전송된 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-167">Specifically, the `Counter` component handles requests sent to `/Counter`.</span></span> <span data-ttu-id="d56b6-168">`@page` 지시문이 없으면 구성 요소는 라우트된 요청을 처리하지 않지만 구성 요소는 다른 구성 요소에서 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-168">Without the `@page` directive, the component wouldn't handle routed requests, but the component could still be used by other components.</span></span>

## <a name="dependency-injection"></a><span data-ttu-id="d56b6-169">종속성 주입</span><span class="sxs-lookup"><span data-stu-id="d56b6-169">Dependency injection</span></span>

<span data-ttu-id="d56b6-170">앱의 서비스 공급자에 등록된 서비스는 [DI(종속성 주입)](https://docs.microsoft.com/aspnet/core/fundamentals/dependency-injection)를 통해 구성 요소에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-170">Services registered with the app's service provider are available to components via [dependency injection (DI)](https://docs.microsoft.com/aspnet/core/fundamentals/dependency-injection).</span></span> <span data-ttu-id="d56b6-171">`@inject` 지시문을 사용하여 구성 요소에 서비스를 주입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-171">Services can be injected into a component using the `@inject` directive.</span></span>

<span data-ttu-id="d56b6-172">*FetchData.cshtml*에서 `FetchData` 구성 요소의 구현을 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="d56b6-172">Take a look at the implementation of the `FetchData` component in *FetchData.cshtml*.</span></span> <span data-ttu-id="d56b6-173">`@inject` 지시문은 [HttpClient](https://docs.microsoft.com/dotnet/api/system.net.http.httpclient) 인스턴스를 구성 요소에 주입하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-173">The `@inject` directive is used to inject an [HttpClient](https://docs.microsoft.com/dotnet/api/system.net.http.httpclient) instance into the component.</span></span>

```cshtml
@page "/fetchdata"
@inject HttpClient Http
```

<span data-ttu-id="d56b6-174">`FetchData` 구성 요소는 주입된 `HttpClient`를 사용하여 구성 요소가 초기화될 때 서버에서 JSON 데이터를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-174">The `FetchData` component uses the injected `HttpClient` to retrieve JSON data from the server when the component is initialized.</span></span> <span data-ttu-id="d56b6-175">커버 아래에 Blazor 런타임에서 제공하는 `HttpClient`는 JavaScript interop을 사용하여 기본 브라우저의 Fetch API를 호출하여 요청을 보내기 위해 구현됩니다(C#에서 모든 JavaScript 라이브러리 또는 브라우저 API를 호출할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="d56b6-175">Under the covers, the `HttpClient` provided by the Blazor runtime is implemented using JavaScript interop to call the underlying browser's Fetch API to send the request (from C#, it's possible to call any JavaScript library or browser API).</span></span> <span data-ttu-id="d56b6-176">검색된 데이터는 `WeatherForecast` 개체의 배열로 `forecasts` C# 변수에 deserialize됩니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-176">The retrieved data is deserialized into the `forecasts` C# variable as an array of `WeatherForecast` objects.</span></span>

```cshtml
@functions {
    WeatherForecast[] forecasts;

    protected override async Task OnInitAsync()
    {
        forecasts = await Http.GetJsonAsync<WeatherForecast[]>("/sample-data/weather.json");
    }

    class WeatherForecast
    {
        public DateTime Date { get; set; }
        public int TemperatureC { get; set; }
        public int TemperatureF { get; set; }
        public string Summary { get; set; }
    }
}
```

<span data-ttu-id="d56b6-177">`@foreach` 루프는 각 예측 인스턴스를 날씨 테이블의 행으로 렌더링하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-177">A `@foreach` loop is used to render each forecast instance as a row in the weather table.</span></span>

```cshtml
<table class="table">
    <thead>
        <tr>
            <th>Date</th>
            <th>Temp. (C)</th>
            <th>Temp. (F)</th>
            <th>Summary</th>
        </tr>
    </thead>
    <tbody>
        @foreach (var forecast in forecasts)
        {
            <tr>
                <td>@forecast.Date.ToShortDateString()</td>
                <td>@forecast.TemperatureC</td>
                <td>@forecast.TemperatureF</td>
                <td>@forecast.Summary</td>
            </tr>
        }
    </tbody>
</table>
```

## <a name="build-a-todo-list"></a><span data-ttu-id="d56b6-178">할 일 목록 빌드</span><span class="sxs-lookup"><span data-stu-id="d56b6-178">Build a todo list</span></span>

<span data-ttu-id="d56b6-179">간단한 할 일 목록을 구현하는 앱에 새 페이지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-179">Add a new page to the app that implements a simple todo list.</span></span>

1. <span data-ttu-id="d56b6-180">빈 텍스트 파일을 *Todo.cshtml*라는 *페이지* 폴더에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-180">Add an empty text file to the *Pages* folder named *Todo.cshtml*.</span></span>

1. <span data-ttu-id="d56b6-181">페이지의 초기 태그를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-181">Provide the initial markup for the page.</span></span>

    ```cshtml
    @page "/todo"

    <h1>Todo</h1>
    ```

1. <span data-ttu-id="d56b6-182">*Shared/NavMenu.cshtml*을 업데이트하여 Todo 페이지를 탐색 모음에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-182">Add the Todo page to the navigation bar by updating *Shared/NavMenu.cshtml*.</span></span> <span data-ttu-id="d56b6-183">기존 목록 항목 아래에 다음 목록 항목 태그를 추가하여 Todo 페이지에 대한 `NavLink`를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-183">Add a `NavLink` for the Todo page by adding the following list item markup below the existing list items.</span></span>

    ```cshtml
    <li class="nav-item px-3">
        <NavLink class="nav-link" href="todo">
            <span class="oi oi-list-rich" aria-hidden="true"></span> Todo
        </NavLink>
    </li>
    ```

1. <span data-ttu-id="d56b6-184">브라우저에서 앱을 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-184">Refresh the app in the browser.</span></span> <span data-ttu-id="d56b6-185">새 Todo 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d56b6-185">See the new Todo page.</span></span>

    ![Blazor todo 시작](https://user-images.githubusercontent.com/1874516/39509907-bb27e77a-4d9c-11e8-91e7-ea1e7c01729e.png)

1. <span data-ttu-id="d56b6-187">프로젝트 루트에 *TodoItem.cs* 파일을 추가하여 할 일 항목을 나타내는 클래스를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-187">Add a *TodoItem.cs* file to the root of the project to hold a class to represent the todo items.</span></span>

1. <span data-ttu-id="d56b6-188">`TodoItem` 클래스에 대해 다음 C# 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-188">Use the following C# code for the `TodoItem` class.</span></span>

    ```csharp
    public class TodoItem
    {
        public string Title { get; set; }
        public bool IsDone { get; set; }
    }
    ```

1. <span data-ttu-id="d56b6-189">*Todo.cshtml*의 `Todo` 구성 요소로 돌아가 `@functions` 블록에서 할 일 필드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-189">Go back to the `Todo` component in *Todo.cshtml* and add a field for the todos in a `@functions` block.</span></span> <span data-ttu-id="d56b6-190">`Todo` 구성 요소는 이 필드를 사용하여 할 일 목록의 상태를 유지 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-190">The `Todo` component uses this field to maintain the state of the todo list.</span></span>

    ```cshtml
    @functions {
        IList<TodoItem> todos = new List<TodoItem>();
    }
    ```

1. <span data-ttu-id="d56b6-191">순서가 지정되지 않은 목록 태그 및 `foreach` 루프를 추가하여 각 할 일 항목을 목록 항목으로 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-191">Add unordered list markup and a `foreach` loop to render each todo item as a list item.</span></span>

    ```cshtml
    @page "/todo"

    <h1>Todo</h1>

    <ul>
        @foreach (var todo in todos)
        {
            <li>@todo.Title</li>
        }
    </ul>
    ```

1. <span data-ttu-id="d56b6-192">할 일을 목록에 추가하려면 앱에 UI 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-192">The app requires UI elements for adding todos to the list.</span></span> <span data-ttu-id="d56b6-193">텍스트 입력과 목록 아래에 단추를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-193">Add a text input and a button below the list.</span></span>

    ```cshtml
    @page "/todo"

    <h1>Todo</h1>

    <ul>
        @foreach (var todo in todos)
        {
            <li>@todo.Title</li>
        }
    </ul>

    <input placeholder="Something todo" />
    <button>Add todo</button>

    @functions {
        IList<TodoItem> todos = new List<TodoItem>();
    }
    ```

1. <span data-ttu-id="d56b6-194">브라우저를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-194">Refresh the browser.</span></span>

    ![할 일 단추 추가](https://user-images.githubusercontent.com/1874516/39512402-bc88ab46-4da5-11e8-9e3f-87b875b56383.png)

    <span data-ttu-id="d56b6-196">단추에 이벤트 처리기가 연결되어 있지 않으므로 **할 일 추가** 단추를 선택하면 아무 것도 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-196">Nothing happens when the **Add todo** button is selected because no event handler is wired up to the button.</span></span>

1. <span data-ttu-id="d56b6-197">`AddTodo` 메서드를 `Todo` 구성 요소에 추가하고 `onclick` 특성을 사용하여 단추 클릭에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-197">Add an `AddTodo` method to the `Todo` component and register it for button clicks using the `onclick` attribute.</span></span>

    ```cshtml
    <input placeholder="Something todo" />
    <button onclick="@AddTodo">Add todo</button>

    @functions {
        IList<TodoItem> todos = new List<TodoItem>();

        void AddTodo()
        {
            // Todo: Add the todo
        }
    }
    ```

    <span data-ttu-id="d56b6-198">단추를 선택할 때마다 `AddTodo` C# 메서드가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-198">The `AddTodo` C# method is called every time the button is selected.</span></span>

1. <span data-ttu-id="d56b6-199">새 할 일 항목의 제목을 가져오려면 `newTodo` 문자열 필드를 추가하고 `bind` 특성을 사용하여 텍스트 입력 값에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-199">To get the title of the new todo item, add a `newTodo` string field and bind it to the value of the text input using the `bind` attribute.</span></span>

    ```csharp
    IList<TodoItem> todos = new List<TodoItem>();
    string newTodo;
    ```

    ```cshtml
    <input placeholder="Something todo" bind="@newTodo" />
    ```

1. <span data-ttu-id="d56b6-200">`AddTodo` 메서드를 업데이트하여 지정된 제목이 있는 `TodoItem`을 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-200">Update the `AddTodo` method to add the `TodoItem` with the specified title to the list.</span></span> <span data-ttu-id="d56b6-201">`newTodo`를 빈 문자열로 설정하여 텍스트 입력 값을 지우는 것을 잊지 마세요.</span><span class="sxs-lookup"><span data-stu-id="d56b6-201">Don't forget to clear the value of the text input by setting `newTodo` to an empty string.</span></span>

    ```cshtml
    @page "/todo"

    <h1>Todo</h1>

    <ul>
        @foreach (var todo in todos)
        {
            <li>@todo.Title</li>
        }
    </ul>

    <input placeholder="Something todo" bind="@newTodo" />
    <button onclick="@AddTodo">Add todo</button>

    @functions {
        IList<TodoItem> todos = new List<TodoItem>();
        string newTodo;

        void AddTodo()
        {
            if (!string.IsNullOrWhiteSpace(newTodo))
            {
                todos.Add(new TodoItem { Title = newTodo });
                newTodo = string.Empty;
            }
        }
    }
    ```

1. <span data-ttu-id="d56b6-202">브라우저를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-202">Refresh the browser.</span></span> <span data-ttu-id="d56b6-203">할 일 목록에 일부 할 일 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-203">Add some todos to the todo list.</span></span>

    ![할 일 추가](https://user-images.githubusercontent.com/1874516/39512531-2d2ff62e-4da6-11e8-8b83-291b0efc821b.png)

1. <span data-ttu-id="d56b6-205">마지막으로, 확인란이 없는 할 일 목록이란?</span><span class="sxs-lookup"><span data-stu-id="d56b6-205">Lastly, what's a todo list without check boxes?</span></span> <span data-ttu-id="d56b6-206">각 할 일 항목의 제목 텍스트도 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-206">The title text for each todo item can be made editable as well.</span></span> <span data-ttu-id="d56b6-207">각 할 일 항목에 대한 확인란 입력과 텍스트 입력을 추가하고 해당 값을 각각 `Title` 및 `IsDone` 속성에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-207">Add a check box input and text input for each todo item and bind their values to the `Title` and `IsDone` properties, respectively.</span></span>

    ```cshtml
    <ul>
        @foreach (var todo in todos)
        {
            <li>
                <input type="checkbox" bind="@todo.IsDone" />
                <input bind="@todo.Title" />
            </li>
        }
    </ul>
    ```

1. <span data-ttu-id="d56b6-208">이러한 값이 바인딩되었는지 확인하려면 `h1` 헤더를 업데이트하여 아직 완료되지 않은 할 일 항목 수(`IsDone`이 `false`임)의 개수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-208">To verify that these values are bound, update the `h1` header to show a count of the number of todo items that are not yet done (`IsDone` is `false`).</span></span>

    ```cshtml
    <h1>Todo (@todos.Count(todo => !todo.IsDone))</h1>
    ```

1. <span data-ttu-id="d56b6-209">완료된 `Todo` 구성 요소는 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-209">The completed `Todo` component should look like this:</span></span>

    ```cshtml
    @page "/todo"

    <h1>Todo (@todos.Count(todo => !todo.IsDone))</h1>

    <ul>
        @foreach (var todo in todos)
        {
            <li>
                <input type="checkbox" bind="@todo.IsDone" />
                <input bind="@todo.Title" />
            </li>
        }
    </ul>

    <input placeholder="Something todo" bind="@newTodo" />
    <button onclick="@AddTodo">Add todo</button>

    @functions {
        IList<TodoItem> todos = new List<TodoItem>();
        string newTodo;

        void AddTodo()
        {
            if (!string.IsNullOrWhiteSpace(newTodo))
            {
                todos.Add(new TodoItem { Title = newTodo });
                newTodo = string.Empty;
            }
        }
    }
    ```

<span data-ttu-id="d56b6-210">브라우저에서 앱을 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-210">Refresh the app in the browser.</span></span> <span data-ttu-id="d56b6-211">일부 할 일 항목을 추가해 보세요.</span><span class="sxs-lookup"><span data-stu-id="d56b6-211">Try adding some todo items.</span></span>

![완료된 Blazor 할 일 목록](https://user-images.githubusercontent.com/1874516/39512621-83406508-4da6-11e8-8244-5bae2ac6b22d.png)

## <a name="publish-and-deploy"></a><span data-ttu-id="d56b6-213">게시 및 배포</span><span class="sxs-lookup"><span data-stu-id="d56b6-213">Publish and deploy</span></span>

<span data-ttu-id="d56b6-214">Visual Studio를 사용하는 경우 다음 단계를 수행하여 Todo Blazor 앱을 Azure에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-214">When using Visual Studio, perform the following steps to publish the Todo Blazor app to Azure:</span></span>

1. <span data-ttu-id="d56b6-215">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-215">Right-click on the project in **Solution Explorer** and select **Publish**.</span></span>

1. <span data-ttu-id="d56b6-216">**게시 대상 선택** 대화 상자에서 **App Service** 및 **새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-216">In the **Pick a publish target** dialog, select **App Service** and **Create New**.</span></span> <span data-ttu-id="d56b6-217">**게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-217">Select **Publish**.</span></span>

    ![게시 대상 선택](build-your-first-blazor-app/_static/blazor-publish-pick-target.png)

1. <span data-ttu-id="d56b6-219">**App Service 만들기** 대화 상자에서 앱 이름을 선택하고 구독, 리소스 그룹 및 호스팅 계획을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-219">In the **Create App Service** dialog, choose a name for the app and select the subscription, resource group, and hosting plan.</span></span> <span data-ttu-id="d56b6-220">**만들기**를 선택하여 앱 서비스를 만들고 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-220">Select **Create** to create the app service and publish the app.</span></span>

    ![앱 서비스 만들기](build-your-first-blazor-app/_static/blazor-publish-create-appservice2.png)

<span data-ttu-id="d56b6-222">앱이 배포될 때까지 약 1분 정도 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-222">Wait a minute or so for the app to be deployed.</span></span>

<span data-ttu-id="d56b6-223">이제 Azure에서 앱을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-223">The app should now be running in Azure.</span></span> <span data-ttu-id="d56b6-224">첫 번째 Blazor 앱을 빌드하려면 할 일 항목을 *완료*로 표시하세요.</span><span class="sxs-lookup"><span data-stu-id="d56b6-224">Mark the todo item to build your first Blazor app as *done*.</span></span> <span data-ttu-id="d56b6-225">잘하셨습니다!</span><span class="sxs-lookup"><span data-stu-id="d56b6-225">Nice job!</span></span>

![Azure의 Blazor](https://user-images.githubusercontent.com/1874516/39512621-83406508-4da6-11e8-8244-5bae2ac6b22d.png)

> [!NOTE]
> <span data-ttu-id="d56b6-227">Visual Studio를 사용하지 않는 경우 Windows, macOS 또는 Linux의 명령 프롬프트에서 Blazor 앱을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-227">If not using Visual Studio, publish the Blazor app at a command prompt on Windows, macOS, or Linux:</span></span>
>
> ```console
> dotnet publish -c Release
> ```
>
> <span data-ttu-id="d56b6-228">배포는 */bin/Release/\<target-framework>/publish* 폴더에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-228">The deployment is created in the */bin/Release/\<target-framework>/publish* folder.</span></span> <span data-ttu-id="d56b6-229">*publish* 폴더의 콘텐츠를 서버 또는 호스팅 서비스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d56b6-229">Move the contents of the *publish* folder to the server or hosting service.</span></span>
>
> <span data-ttu-id="d56b6-230">자세한 내용은 [호스트 및 배포](xref:host-and-deploy/razor-components/index#publish-the-app) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d56b6-230">For more information, see the [Host and deploy](xref:host-and-deploy/razor-components/index#publish-the-app) topic.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d56b6-231">추가 자료</span><span class="sxs-lookup"><span data-stu-id="d56b6-231">Additional resources</span></span>

<span data-ttu-id="d56b6-232">더 관련된 Blazor 샘플 앱을 보려면 GitHub의 [Flight Finder 샘플](https://github.com/aspnet/samples/tree/master/samples/aspnetcore/blazor)을 체그 아웃하세요.</span><span class="sxs-lookup"><span data-stu-id="d56b6-232">For a more involved Blazor sample app, check out the [Flight Finder sample](https://github.com/aspnet/samples/tree/master/samples/aspnetcore/blazor) on GitHub.</span></span>

![Blazor Flight Finder](https://msdnshared.blob.core.windows.net/media/2018/03/blazor-flight-finder.png)
