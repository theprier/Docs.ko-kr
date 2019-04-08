---
title: Blazor 시작
author: guardrex
description: 만들고 Blazor 프로젝트를 수정 하 여 Blazor를 사용 하 여 시작 하는 방법에 알아봅니다.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 04/07/2019
uid: spa/blazor/get-started
ms.openlocfilehash: b3928c2812be6f34cdf2f17295a1251106f651e5
ms.sourcegitcommit: 6bde1fdf686326c080a7518a6725e56e56d8886e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2019
ms.locfileid: "59068237"
---
# <a name="get-started-with-blazor"></a><span data-ttu-id="049c4-103">Blazor 시작</span><span class="sxs-lookup"><span data-stu-id="049c4-103">Get started with Blazor</span></span>

<span data-ttu-id="049c4-104">작성자: [Daniel Roth](https://github.com/danroth27) 및 [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="049c4-104">By [Daniel Roth](https://github.com/danroth27) and [Luke Latham](https://github.com/guardrex)</span></span>

[!INCLUDE[](~/includes/razor-components-preview-notice.md)]

# [<a name="visual-studio"></a><span data-ttu-id="049c4-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="049c4-105">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="049c4-106">필수 구성 요소:</span><span class="sxs-lookup"><span data-stu-id="049c4-106">Prerequisites:</span></span>

[!INCLUDE[](~/includes/net-core-prereqs-vs-3.0.md)]

<span data-ttu-id="049c4-107">Visual Studio에서 첫 번째 Blazor 프로젝트를 만들려면:</span><span class="sxs-lookup"><span data-stu-id="049c4-107">To create your first Blazor project in Visual Studio:</span></span>

1. <span data-ttu-id="049c4-108">최신 설치 [.NET Core 3.0 미리 보기 SDK](https://dotnet.microsoft.com/download/dotnet-core/3.0) 릴리스 합니다.</span><span class="sxs-lookup"><span data-stu-id="049c4-108">Install the latest [.NET Core 3.0 Preview SDK](https://dotnet.microsoft.com/download/dotnet-core/3.0) release.</span></span>
1. <span data-ttu-id="049c4-109">미리 보기 Sdk를 사용 하도록 Visual Studio를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="049c4-109">Enable Visual Studio to use preview SDKs:</span></span>
   1. <span data-ttu-id="049c4-110">오픈 **도구가** > **옵션** 메뉴 모음에서.</span><span class="sxs-lookup"><span data-stu-id="049c4-110">Open **Tools** > **Options** in the menu bar.</span></span>
   1. <span data-ttu-id="049c4-111">엽니다는 **프로젝트 및 솔루션** 노드.</span><span class="sxs-lookup"><span data-stu-id="049c4-111">Open the **Projects and Solutions** node.</span></span> <span data-ttu-id="049c4-112">엽니다는 **.NET Core** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="049c4-112">Open the **.NET Core** tab.</span></span>
   1. <span data-ttu-id="049c4-113">확인란 **.NET Core SDK의 미리 보기를 사용 하 여**입니다.</span><span class="sxs-lookup"><span data-stu-id="049c4-113">Check the box for **Use previews of the .NET Core SDK**.</span></span> <span data-ttu-id="049c4-114">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="049c4-114">Select **OK**.</span></span>
1. <span data-ttu-id="049c4-115">최신 설치 [Blazor 확장](https://go.microsoft.com/fwlink/?linkid=870389) Visual Studio Marketplace에서.</span><span class="sxs-lookup"><span data-stu-id="049c4-115">Install the latest [Blazor extension](https://go.microsoft.com/fwlink/?linkid=870389) from the Visual Studio Marketplace.</span></span> <span data-ttu-id="049c4-116">이 단계에 게 Blazor 템플릿을 사용할 수 있는 Visual Studio입니다.</span><span class="sxs-lookup"><span data-stu-id="049c4-116">This step makes Blazor templates available to Visual Studio.</span></span>
1. <span data-ttu-id="049c4-117">명령 셸에서 다음 명령을 실행 하 여.NET Core CLI와 함께 사용할 Blazor 템플릿을 확인:</span><span class="sxs-lookup"><span data-stu-id="049c4-117">Make the Blazor templates available for use with the .NET Core CLI by running the following command in a command shell:</span></span>

   ```console
   dotnet new -i Microsoft.AspNetCore.Blazor.Templates::0.9.0-preview3-19154-02
   ```
1. <span data-ttu-id="049c4-118">새 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="049c4-118">Create a new project.</span></span>
1. <span data-ttu-id="049c4-119">**새 ASP.NET Core 웹 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="049c4-119">Select **ASP.NET Core Web Application**.</span></span> <span data-ttu-id="049c4-120">**새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="049c4-120">Select **Next**.</span></span>
1. <span data-ttu-id="049c4-121">에 이름을 제공 합니다 **프로젝트 이름** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="049c4-121">Provide a name in the **Project name** field.</span></span> <span data-ttu-id="049c4-122">확인 합니다 **위치** 항목이 올바른 또는 프로젝트의 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="049c4-122">Confirm the **Location** entry is correct or provide a location for the project.</span></span> <span data-ttu-id="049c4-123">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="049c4-123">Select **Create**.</span></span>
1. <span data-ttu-id="049c4-124">했는지 **.NET Core** 하 고 **ASP.NET Core 3.0** 맨 위에 있는 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="049c4-124">Make sure **.NET Core** and **ASP.NET Core 3.0** are selected at the top.</span></span>
1. <span data-ttu-id="049c4-125">선택 된 **Blazor** 템플릿과 선택 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="049c4-125">Select the **Blazor** template and select **Create**.</span></span>
1. <span data-ttu-id="049c4-126">**F5** 키를 눌러 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="049c4-126">Press **F5** to run the app.</span></span>

<span data-ttu-id="049c4-127">지금까지</span><span class="sxs-lookup"><span data-stu-id="049c4-127">Congratulations!</span></span> <span data-ttu-id="049c4-128">지금까지 첫 번째 Blazor 앱을 실행 했습니다!</span><span class="sxs-lookup"><span data-stu-id="049c4-128">You just ran your first Blazor app!</span></span>

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

# [<a name="net-core-cli"></a><span data-ttu-id="049c4-129">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="049c4-129">.NET Core CLI</span></span>](#tab/netcore-cli/)

<span data-ttu-id="049c4-130">필수 구성 요소:</span><span class="sxs-lookup"><span data-stu-id="049c4-130">Prerequisites:</span></span>

* [<span data-ttu-id="049c4-131">.NET core SDK 3.0 미리 보기</span><span class="sxs-lookup"><span data-stu-id="049c4-131">.NET Core SDK 3.0 Preview</span></span>](https://dotnet.microsoft.com/download/dotnet-core/3.0)

1. <span data-ttu-id="049c4-132">명령 셸에서 다음 명령을 실행 하 여 Blazor 템플릿을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="049c4-132">Add the Blazor templates by running the following command in a command shell:</span></span>

   ```console
   dotnet new -i Microsoft.AspNetCore.Blazor.Templates::0.9.0-preview3-19154-02
   ```

1. <span data-ttu-id="049c4-133">명령 셸에서 첫 번째 Blazor 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="049c4-133">Create your first Blazor project in a command shell:</span></span>

   ```console
   dotnet new blazor -o WebApplication1
   cd WebApplication1
   dotnet run
   ```

1. <span data-ttu-id="049c4-134">브라우저에서 `https://localhost:5001`로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="049c4-134">In a browser, navigate to `https://localhost:5001`.</span></span>

<span data-ttu-id="049c4-135">지금까지</span><span class="sxs-lookup"><span data-stu-id="049c4-135">Congratulations!</span></span> <span data-ttu-id="049c4-136">지금까지 첫 번째 Blazor 앱을 실행 했습니다!</span><span class="sxs-lookup"><span data-stu-id="049c4-136">You just ran your first Blazor app!</span></span>

---

## <a name="blazor-project"></a><span data-ttu-id="049c4-137">Blazor 프로젝트</span><span class="sxs-lookup"><span data-stu-id="049c4-137">Blazor project</span></span>

<span data-ttu-id="049c4-138">앱을 실행 하는 경우 여러 페이지 세로 막대의 탭에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="049c4-138">When the app is run, multiple pages are available from tabs in the sidebar:</span></span>

* <span data-ttu-id="049c4-139">홈</span><span class="sxs-lookup"><span data-stu-id="049c4-139">Home</span></span>
* <span data-ttu-id="049c4-140">카운터</span><span class="sxs-lookup"><span data-stu-id="049c4-140">Counter</span></span>
* <span data-ttu-id="049c4-141">데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="049c4-141">Fetch data</span></span>

<span data-ttu-id="049c4-142">카운터 페이지에서 **Click me** 단추를 선택하여 페이지 새로 고침 없이 카운터를 증분합니다.</span><span class="sxs-lookup"><span data-stu-id="049c4-142">On the Counter page, select the **Click me** button to increment the counter without a page refresh.</span></span> <span data-ttu-id="049c4-143">일반적으로 웹 페이지에서 카운터를 증가 하려면 JavaScript를 작성 해야 하지만 Blazor 사용 하 여 더 나은 접근 방식을 제공 C#입니다.</span><span class="sxs-lookup"><span data-stu-id="049c4-143">Incrementing a counter in a webpage normally requires writing JavaScript, but Blazor provides a better approach using C#.</span></span>

<span data-ttu-id="049c4-144">*Pages/Counter.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="049c4-144">*Pages/Counter.cshtml*:</span></span>

[!code-cshtml[](get-started/samples_snapshot/3.x/Counter1.cshtml)]

<span data-ttu-id="049c4-145">에 대 한 요청 `/counter` 에 지정 된 대로 브라우저에서을 `@page` 맨 위에 있는 지시문 하면 카운터 구성 요소를 해당 콘텐츠를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="049c4-145">A request for `/counter` in the browser, as specified by the `@page` directive at the top, causes the Counter component to render its content.</span></span> <span data-ttu-id="049c4-146">구성 요소는 메모리 내 표현을 유연 하 고 효율적인 방식으로 UI를 업데이트 하는 데 사용할 수 있는 렌더링 트리를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="049c4-146">Components render into an in-memory representation of the render tree that can then be used to update the UI in a flexible and efficient way.</span></span>

<span data-ttu-id="049c4-147">각 시간 합니다 **Click me** 단추를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="049c4-147">Each time the **Click me** button is selected:</span></span>

* <span data-ttu-id="049c4-148">`onclick` 이벤트가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="049c4-148">The `onclick` event is fired.</span></span>
* <span data-ttu-id="049c4-149">`IncrementCount` 메서드가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="049c4-149">The `IncrementCount` method is called.</span></span>
* <span data-ttu-id="049c4-150">`currentCount` 증분됩니다.</span><span class="sxs-lookup"><span data-stu-id="049c4-150">The `currentCount` is incremented.</span></span>
* <span data-ttu-id="049c4-151">구성 요소를 다시 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="049c4-151">The component is rendered again.</span></span>

<span data-ttu-id="049c4-152">런타임에 이전 내용으로 새 콘텐츠를 비교 하 여 변경 된 내용이만 문서 개체 모델 (DOM)에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="049c4-152">The runtime compares the new content to the previous content and only applies the changed content to the Document Object Model (DOM).</span></span>

<span data-ttu-id="049c4-153">HTML과 유사한 구문을 사용 하는 다른 구성 요소는 구성 요소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="049c4-153">Add a component to another component using an HTML-like syntax.</span></span> <span data-ttu-id="049c4-154">구성 요소 매개 변수는 특성 또는 자식 콘텐츠를 사용 하 여 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="049c4-154">Component parameters are specified using attributes or child content.</span></span> <span data-ttu-id="049c4-155">예를 들어, 카운터 구성 요소 수에 추가할 앱의 홈 페이지를 추가 하 여를 `<Counter />` 요소 인덱스 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="049c4-155">For example, a Counter component can be added to the app's homepage by adding a `<Counter />` element to the Index component.</span></span>

<span data-ttu-id="049c4-156">*pages/Index.cshtml*, 카운터 구성 요소를 사용 하 여 설문 조사 프롬프트 구성 요소를 교체 합니다.</span><span class="sxs-lookup"><span data-stu-id="049c4-156">In *Pages/Index.cshtml*, replace the Survey Prompt component with a Counter component:</span></span>

[!code-cshtml[](get-started/samples_snapshot/3.x/Index1.cshtml?highlight=7)]

<span data-ttu-id="049c4-157">앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="049c4-157">Run the app.</span></span> <span data-ttu-id="049c4-158">홈 페이지에는 자체 카운터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="049c4-158">The homepage has its own counter.</span></span>

<span data-ttu-id="049c4-159">매개 변수를 카운터 구성 요소를 추가 하려면 구성 요소의 업데이트 `@functions` 블록:</span><span class="sxs-lookup"><span data-stu-id="049c4-159">To add a parameter to the Counter component, update the component's `@functions` block:</span></span>

* <span data-ttu-id="049c4-160">에 대 한 속성을 추가 `IncrementAmount` 데코 레이트 된 `[Parameter]` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="049c4-160">Add a property for `IncrementAmount` decorated with the `[Parameter]` attribute.</span></span>
* <span data-ttu-id="049c4-161">`currentCount` 값을 늘릴 때 `IncrementAmount`를 사용하도록 `IncrementCount` 메서드를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="049c4-161">Change the `IncrementCount` method to use the `IncrementAmount` when increasing the value of `currentCount`.</span></span>

<span data-ttu-id="049c4-162">*Pages/Counter.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="049c4-162">*Pages/Counter.cshtml*:</span></span>

[!code-cshtml[](get-started/samples_snapshot/3.x/Counter2.cshtml?highlight=4,8)]

<span data-ttu-id="049c4-163">특성을 사용하여 Home 구성 요소의 `<Counter>` 요소에 `IncrementAmount` 매개 변수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="049c4-163">Specify an `IncrementAmount` parameter in the Home component's `<Counter>` element using an attribute.</span></span>

<span data-ttu-id="049c4-164">*Pages/Index.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="049c4-164">*Pages/Index.cshtml*:</span></span>

[!code-cshtml[](get-started/samples_snapshot/3.x/Index2.cshtml)]

<span data-ttu-id="049c4-165">앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="049c4-165">Run the app.</span></span> <span data-ttu-id="049c4-166">홈 페이지에는 각 시간을 10 씩 증가 하는 자체 카운터가 합니다 **Click me** 단추를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="049c4-166">The homepage has its own counter that increments by ten each time the **Click me** button is selected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="049c4-167">다음 단계</span><span class="sxs-lookup"><span data-stu-id="049c4-167">Next steps</span></span>

<xref:tutorials/first-razor-components-app>
