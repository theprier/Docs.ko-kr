---
title: Blazor 시작
author: guardrex
description: 만들고 Blazor 프로젝트를 수정 하 여 Blazor를 사용 하 여 시작 하는 방법에 알아봅니다.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 02/12/2019
uid: spa/blazor/get-started
ms.openlocfilehash: 8c984bab8a13b4fc2d87fd1a7e0b285dfa25ba09
ms.sourcegitcommit: af8a6eb5375ef547a52ffae22465e265837aa82b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56159606"
---
# <a name="get-started-with-blazor"></a><span data-ttu-id="950d0-103">Blazor 시작</span><span class="sxs-lookup"><span data-stu-id="950d0-103">Get started with Blazor</span></span>

<span data-ttu-id="950d0-104">하 여 [Daniel Roth](https://github.com/danroth27) 고 [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="950d0-104">By [Daniel Roth](https://github.com/danroth27) and [Luke Latham](https://github.com/guardrex)</span></span>

[!INCLUDE[](~/includes/razor-components-preview-notice.md)]

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="950d0-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="950d0-105">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="950d0-106">필수 구성 요소:</span><span class="sxs-lookup"><span data-stu-id="950d0-106">Prerequisites:</span></span>

[!INCLUDE[](~/includes/net-core-prereqs-vs-3.0.md)]

<span data-ttu-id="950d0-107">Visual Studio에서 첫 번째 Blazor 프로젝트를 만들려면:</span><span class="sxs-lookup"><span data-stu-id="950d0-107">To create your first Blazor project in Visual Studio:</span></span>

1. <span data-ttu-id="950d0-108">최신 설치 [Blazor 언어 서비스 확장](https://go.microsoft.com/fwlink/?linkid=870389) Visual Studio Marketplace에서.</span><span class="sxs-lookup"><span data-stu-id="950d0-108">Install the latest [Blazor Language Services extension](https://go.microsoft.com/fwlink/?linkid=870389) from the Visual Studio Marketplace.</span></span> <span data-ttu-id="950d0-109">이 단계에 게 Blazor 템플릿을 사용할 수 있는 Visual Studio입니다.</span><span class="sxs-lookup"><span data-stu-id="950d0-109">This step makes Blazor templates available to Visual Studio.</span></span>
1. <span data-ttu-id="950d0-110">명령 셸에서 다음 명령을 실행 하 여.NET Core CLI와 함께 사용할 Blazor 템플릿을 확인:</span><span class="sxs-lookup"><span data-stu-id="950d0-110">Make the Blazor templates available for use with the .NET Core CLI by running the following command in a command shell:</span></span>

   ```console
   dotnet new -i Microsoft.AspNetCore.Blazor.Templates
   ```

1. <span data-ttu-id="950d0-111">선택 **파일** > **새 프로젝트** > **Web** > **ASP.NET Core 웹 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="950d0-111">Select **File** > **New Project** > **Web** > **ASP.NET Core Web Application**.</span></span>
1. <span data-ttu-id="950d0-112">했는지 **.NET Core** 하 고 **ASP.NET Core 3.0** 맨 위에 있는 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="950d0-112">Make sure **.NET Core** and **ASP.NET Core 3.0** are selected at the top.</span></span>
1. <span data-ttu-id="950d0-113">**Blazor** 템플릿을 선택하고 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="950d0-113">Choose the **Blazor** template and select **OK**.</span></span>
1. <span data-ttu-id="950d0-114">**F5** 키를 눌러 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="950d0-114">Press **F5** to run the app.</span></span>

<span data-ttu-id="950d0-115">지금까지</span><span class="sxs-lookup"><span data-stu-id="950d0-115">Congratulations!</span></span> <span data-ttu-id="950d0-116">지금까지 첫 번째 Blazor 앱을 실행 했습니다!</span><span class="sxs-lookup"><span data-stu-id="950d0-116">You just ran your first Blazor app!</span></span>

<!--

# [Visual Studio Code](#tab/visual-studio-code)

Prerequisites:

[!INCLUDE[](~/includes/net-core-prereqs-vsc-3.0.md)]

To create your first Blazor project in Visual Studio Code:

1. Execute the following command in a command shell:

   ```console
   dotnet new blazor -o WebApplication1
   ```

1. Open the *WebApplication1* folder in Visual Studio Code.

1. Visual Studio code offers to create assets to build and debug the app, which includes the *tasks.json* and *launch.json* files. Select **Yes** to add the assets.

1. Execute the app using the Visual Studio Code debugger.

1. In a browser, navigate to `https://localhost:5001`.

Congratulations! You just ran your first Blazor app!

# [Visual Studio for Mac](#tab/visual-studio-mac)

.NET Core 3.0 will be supported with Visual Studio for Mac version 8.0 or later. Visual Studio for Mac version 8.0 Preview isn't available at this time.

Use the [.NET Core CLI version of this topic](xref:razor-components/get-started?tabs=netcore-cli) on macOS.

[!INCLUDE[](~/includes/net-core-prereqs-mac-3.0.md)]

To create your first project Blazor project in Visual Studio for Mac:

1. Select **File** > **New Solution** or **New Project**.
1. In the sidebar, select **.NET Core** > **App**.
1. Select **Blazor** and select **Next**.
1. The **Target Framework** defaults to **.NET Core 3.0**. Select **Next**.
1. In the **Project Name** field, enter `WebApplication1`. Select **Create**.
1. Select **Run** > **Run Without Debugging** to run the app *without the debugger*. Running with the debugger isn't supported at this time.

Congratulations! You just ran your first Blazor app!
-->

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="950d0-117">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="950d0-117">.NET Core CLI</span></span>](#tab/netcore-cli/)

<span data-ttu-id="950d0-118">필수 구성 요소:</span><span class="sxs-lookup"><span data-stu-id="950d0-118">Prerequisites:</span></span>

* [<span data-ttu-id="950d0-119">.NET core SDK 3.0 미리 보기</span><span class="sxs-lookup"><span data-stu-id="950d0-119">.NET Core SDK 3.0 Preview</span></span>](https://dotnet.microsoft.com/download/dotnet-core/3.0)

1. <span data-ttu-id="950d0-120">명령 셸에서 다음 명령을 실행 하 여 Blazor 템플릿을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="950d0-120">Add the Blazor templates by running the following command in a command shell:</span></span>

   ```console
   dotnet new -i Microsoft.AspNetCore.Blazor.Templates
   ```

1. <span data-ttu-id="950d0-121">명령 셸에서 첫 번째 Blazor 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="950d0-121">Create your first Blazor project in a command shell:</span></span>

   ```console
   dotnet new blazor -o WebApplication1
   cd WebApplication1
   dotnet run
   ```

1. <span data-ttu-id="950d0-122">브라우저에서 `https://localhost:5001`로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="950d0-122">In a browser, navigate to `https://localhost:5001`.</span></span>

<span data-ttu-id="950d0-123">지금까지</span><span class="sxs-lookup"><span data-stu-id="950d0-123">Congratulations!</span></span> <span data-ttu-id="950d0-124">지금까지 첫 번째 Blazor 앱을 실행 했습니다!</span><span class="sxs-lookup"><span data-stu-id="950d0-124">You just ran your first Blazor app!</span></span>

---

## <a name="blazor-project"></a><span data-ttu-id="950d0-125">Blazor 프로젝트</span><span class="sxs-lookup"><span data-stu-id="950d0-125">Blazor project</span></span>

<span data-ttu-id="950d0-126">앱을 실행 하는 경우 여러 페이지 세로 막대의 탭에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="950d0-126">When the app is run, multiple pages are available from tabs in the sidebar:</span></span>

* <span data-ttu-id="950d0-127">홈</span><span class="sxs-lookup"><span data-stu-id="950d0-127">Home</span></span>
* <span data-ttu-id="950d0-128">카운터</span><span class="sxs-lookup"><span data-stu-id="950d0-128">Counter</span></span>
* <span data-ttu-id="950d0-129">데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="950d0-129">Fetch data</span></span>

<span data-ttu-id="950d0-130">카운터 페이지에서 선택 합니다 **Click me** 페이지 새로 고침 없이 카운터를 증가 하는 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="950d0-130">On the Counter page, select the **Click me** button to increment the counter without a page refresh.</span></span> <span data-ttu-id="950d0-131">일반적으로 웹 페이지에서 카운터를 증가 하려면 JavaScript를 작성 해야 하지만 Blazor 사용 하 여 더 나은 접근 방식을 제공 C#입니다.</span><span class="sxs-lookup"><span data-stu-id="950d0-131">Incrementing a counter in a webpage normally requires writing JavaScript, but Blazor provides a better approach using C#.</span></span>

<span data-ttu-id="950d0-132">*Pages/Counter.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="950d0-132">*Pages/Counter.cshtml*:</span></span>

[!code-cshtml[](get-started/samples_snapshot/3.x/Counter1.cshtml)]

<span data-ttu-id="950d0-133">에 대 한 요청 `/counter` 에 지정 된 대로 브라우저에서을 `@page` 맨 위에 있는 지시문 하면 카운터 구성 요소를 해당 콘텐츠를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="950d0-133">A request for `/counter` in the browser, as specified by the `@page` directive at the top, causes the Counter component to render its content.</span></span> <span data-ttu-id="950d0-134">구성 요소는 메모리 내 표현을 유연 하 고 효율적인 방식으로 UI를 업데이트 하는 데 사용할 수 있는 렌더링 트리를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="950d0-134">Components render into an in-memory representation of the render tree that can then be used to update the UI in a flexible and efficient way.</span></span>

<span data-ttu-id="950d0-135">각 시간 합니다 **Click me** 단추를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="950d0-135">Each time the **Click me** button is selected:</span></span>

* <span data-ttu-id="950d0-136">`onclick` 이벤트가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="950d0-136">The `onclick` event is fired.</span></span>
* <span data-ttu-id="950d0-137">`IncrementCount` 메서드가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="950d0-137">The `IncrementCount` method is called.</span></span>
* <span data-ttu-id="950d0-138">`currentCount` 증분됩니다.</span><span class="sxs-lookup"><span data-stu-id="950d0-138">The `currentCount` is incremented.</span></span>
* <span data-ttu-id="950d0-139">구성 요소를 다시 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="950d0-139">The component is rendered again.</span></span>

<span data-ttu-id="950d0-140">런타임에 이전 내용으로 새 콘텐츠를 비교 하 여 변경 된 내용이만 문서 개체 모델 (DOM)에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="950d0-140">The runtime compares the new content to the previous content and only applies the changed content to the Document Object Model (DOM).</span></span>

<span data-ttu-id="950d0-141">HTML과 유사한 구문을 사용 하는 다른 구성 요소는 구성 요소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="950d0-141">Add a component to another component using an HTML-like syntax.</span></span> <span data-ttu-id="950d0-142">구성 요소 매개 변수는 특성 또는 자식 콘텐츠를 사용 하 여 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="950d0-142">Component parameters are specified using attributes or child content.</span></span> <span data-ttu-id="950d0-143">예를 들어, 카운터 구성 요소 수에 추가할 앱의 홈 페이지를 추가 하 여를 `<Counter />` 요소 인덱스 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="950d0-143">For example, a Counter component can be added to the app's homepage by adding a `<Counter />` element to the Index component.</span></span>

<span data-ttu-id="950d0-144">*pages/Index.cshtml*, 카운터 구성 요소를 사용 하 여 설문 조사 프롬프트 구성 요소를 교체 합니다.</span><span class="sxs-lookup"><span data-stu-id="950d0-144">In *Pages/Index.cshtml*, replace the Survey Prompt component with a Counter component:</span></span>

[!code-cshtml[](get-started/samples_snapshot/3.x/Index1.cshtml?highlight=7)]

<span data-ttu-id="950d0-145">앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="950d0-145">Run the app.</span></span> <span data-ttu-id="950d0-146">홈 페이지에는 자체 카운터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="950d0-146">The homepage has its own counter.</span></span>

<span data-ttu-id="950d0-147">매개 변수를 카운터 구성 요소를 추가 하려면 구성 요소의 업데이트 `@functions` 블록:</span><span class="sxs-lookup"><span data-stu-id="950d0-147">To add a parameter to the Counter component, update the component's `@functions` block:</span></span>

* <span data-ttu-id="950d0-148">에 대 한 속성을 추가 `IncrementAmount` 데코 레이트 된 `[Parameter]` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="950d0-148">Add a property for `IncrementAmount` decorated with the `[Parameter]` attribute.</span></span>
* <span data-ttu-id="950d0-149">변경 된 `IncrementCount` 메서드를 사용 하 여 합니다 `IncrementAmount` 의 값을 증가 하는 경우 `currentCount`합니다.</span><span class="sxs-lookup"><span data-stu-id="950d0-149">Change the `IncrementCount` method to use the `IncrementAmount` when increasing the value of `currentCount`.</span></span>

<span data-ttu-id="950d0-150">*Pages/Counter.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="950d0-150">*Pages/Counter.cshtml*:</span></span>

[!code-cshtml[](get-started/samples_snapshot/3.x/Counter2.cshtml?highlight=4,8)]

<span data-ttu-id="950d0-151">지정 된 `IncrementAmount` 홈 구성 요소에서 매개 변수 `<Counter>` 특성을 사용 하 여 요소.</span><span class="sxs-lookup"><span data-stu-id="950d0-151">Specify an `IncrementAmount` parameter in the Home component's `<Counter>` element using an attribute.</span></span>

<span data-ttu-id="950d0-152">*Pages/Index.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="950d0-152">*Pages/Index.cshtml*:</span></span>

[!code-cshtml[](get-started/samples_snapshot/3.x/Index2.cshtml)]

<span data-ttu-id="950d0-153">앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="950d0-153">Run the app.</span></span> <span data-ttu-id="950d0-154">홈 페이지에는 각 시간을 10 씩 증가 하는 자체 카운터가 합니다 **Click me** 단추를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="950d0-154">The homepage has its own counter that increments by ten each time the **Click me** button is selected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="950d0-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="950d0-155">Next steps</span></span>

<xref:tutorials/first-razor-components-app>
