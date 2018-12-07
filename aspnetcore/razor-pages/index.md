---
title: ASP.NET Core의 Razor 페이지 소개
author: Rick-Anderson
description: 페이지 코딩 중심의 시나리오에서 ASP.NET Core의 Razor 페이지를 사용하면 MVC를 사용할 때보다 어떻게 더 쉽고 생산적인지 알아봅니다.
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.date: 05/12/2018
uid: razor-pages/index
ms.openlocfilehash: cc881ff42d57ab1654f492a70006a995939e4844
ms.sourcegitcommit: 8a65f6c2cbe290fb2418eed58f60fb74c95392c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52892122"
---
# <a name="introduction-to-razor-pages-in-aspnet-core"></a><span data-ttu-id="0ea7c-103">ASP.NET Core의 Razor 페이지 소개</span><span class="sxs-lookup"><span data-stu-id="0ea7c-103">Introduction to Razor Pages in ASP.NET Core</span></span>

<span data-ttu-id="0ea7c-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Ryan Nowak](https://github.com/rynowak)</span><span class="sxs-lookup"><span data-stu-id="0ea7c-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Ryan Nowak](https://github.com/rynowak)</span></span>

<span data-ttu-id="0ea7c-105">Razor 페이지는 페이지 코딩 중심의 시나리오를 보다 쉽고 생산적으로 만들어주는 ASP.NET Core MVC의 새로운 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-105">Razor Pages is a new aspect of ASP.NET Core MVC that makes coding page-focused scenarios easier and more productive.</span></span>

<span data-ttu-id="0ea7c-106">모델-뷰-컨트롤러 방식을 사용하는 자습서를 찾고 있다면 [ASP.NET Core MVC 시작하기](xref:tutorials/first-mvc-app/start-mvc)를 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-106">If you're looking for a tutorial that uses the Model-View-Controller approach, see [Get started with ASP.NET Core MVC](xref:tutorials/first-mvc-app/start-mvc).</span></span>

<span data-ttu-id="0ea7c-107">이 문서에서는 Razor 페이지에 대한 소개를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-107">This document provides an introduction to Razor Pages.</span></span> <span data-ttu-id="0ea7c-108">단계별 자습서가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-108">It's not a step by step tutorial.</span></span> <span data-ttu-id="0ea7c-109">일부 섹션이 너무 어렵다고 느껴진다면 [Razor 페이지 시작하기](xref:tutorials/razor-pages/razor-pages-start)를 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-109">If you find some of the sections too advanced, see [Get started with Razor Pages](xref:tutorials/razor-pages/razor-pages-start).</span></span> <span data-ttu-id="0ea7c-110">ASP.NET Core에 대한 개요는 [ASP.NET Core 소개](xref:index)를 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-110">For an overview of ASP.NET Core, see the [Introduction to ASP.NET Core](xref:index).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ea7c-111">전제 조건</span><span class="sxs-lookup"><span data-stu-id="0ea7c-111">Prerequisites</span></span>

[!INCLUDE[](~/includes/net-core-prereqs-all-2.2.md)]

<a name="rpvs17"></a>

## <a name="create-a-razor-pages-project"></a><span data-ttu-id="0ea7c-112">Razor Pages 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="0ea7c-112">Create a Razor Pages project</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="0ea7c-113">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0ea7c-113">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="0ea7c-114">Razor Pages 프로젝트를 만드는 방법에 대한 자세한 내용은 [Razor Pages 시작](xref:tutorials/razor-pages/razor-pages-start)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-114">See [Get started with Razor Pages](xref:tutorials/razor-pages/razor-pages-start) for detailed instructions on how to create a Razor Pages project.</span></span>

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="0ea7c-115">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="0ea7c-115">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="0ea7c-116">명령줄에서 `dotnet new webapp`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-116">Run `dotnet new webapp` from the command line.</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="0ea7c-117">명령줄에서 `dotnet new razor`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-117">Run `dotnet new razor` from the command line.</span></span>

::: moniker-end

<span data-ttu-id="0ea7c-118">Mac용 Visual Studio에서 생성된 *.csproj* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-118">Open the generated *.csproj* file from Visual Studio for Mac.</span></span>

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="0ea7c-119">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="0ea7c-119">Visual Studio Code</span></span>](#tab/visual-studio-code)

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="0ea7c-120">명령줄에서 `dotnet new webapp`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-120">Run `dotnet new webapp` from the command line.</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="0ea7c-121">명령줄에서 `dotnet new razor`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-121">Run `dotnet new razor` from the command line.</span></span>

::: moniker-end

---

## <a name="razor-pages"></a><span data-ttu-id="0ea7c-122">Razor 페이지</span><span class="sxs-lookup"><span data-stu-id="0ea7c-122">Razor Pages</span></span>

<span data-ttu-id="0ea7c-123">Razor 페이지는 *Startup.cs*에서 사용할 수 있게 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-123">Razor Pages is enabled in *Startup.cs*:</span></span>

[!code-cs[](index/sample/RazorPagesIntro/Startup.cs?name=snippet_Startup)]

<span data-ttu-id="0ea7c-124">기본 페이지를 고려해 봅니다. <a name="OnGet"></a></span><span class="sxs-lookup"><span data-stu-id="0ea7c-124">Consider a basic page: <a name="OnGet"></a></span></span>

[!code-cshtml[](index/sample/RazorPagesIntro/Pages/Index.cshtml)]

<span data-ttu-id="0ea7c-125">이전 코드는 Razor 뷰 파일과 매우 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-125">The preceding code looks a lot like a Razor view file.</span></span> <span data-ttu-id="0ea7c-126">차이점은 `@page` 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-126">What makes it different is the `@page` directive.</span></span> <span data-ttu-id="0ea7c-127">`@page`는 파일을 MVC 작업으로 만듭니다. 즉, 컨트롤러를 거치지 않고 요청을 직접 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-127">`@page` makes the file into an MVC action - which means that it handles requests directly, without going through a controller.</span></span> <span data-ttu-id="0ea7c-128">`@page`는 페이지의 첫 번째 Razor 지시문이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-128">`@page` must be the first Razor directive on a page.</span></span> <span data-ttu-id="0ea7c-129">`@page`는 다른 Razor 생성자의 동작에 영향을 미칩니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-129">`@page` affects the behavior of other Razor constructs.</span></span>

<span data-ttu-id="0ea7c-130">다음 두 파일은 `PageModel` 클래스를 사용하는 비슷한 페이지를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-130">A similar page, using a `PageModel` class, is shown in the following two files.</span></span> <span data-ttu-id="0ea7c-131">*Pages/Index2.cshtml* 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-131">The *Pages/Index2.cshtml* file:</span></span>

[!code-cshtml[](index/sample/RazorPagesIntro/Pages/Index2.cshtml)]

<span data-ttu-id="0ea7c-132">*Pages/Index2.cshtml.cs* 페이지 모델은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-132">The *Pages/Index2.cshtml.cs* page model:</span></span>

[!code-cs[](index/sample/RazorPagesIntro/Pages/Index2.cshtml.cs)]

<span data-ttu-id="0ea7c-133">규약에 따라 `PageModel` 클래스 파일의 이름은 *.cs*가 추가된 Razor 페이지 파일의 이름과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-133">By convention, the `PageModel` class file has the same name as the Razor Page file with *.cs* appended.</span></span> <span data-ttu-id="0ea7c-134">예를 들어 위의 Razor 페이지는 *Pages/Index2.cshtml*입니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-134">For example, the previous Razor Page is *Pages/Index2.cshtml*.</span></span> <span data-ttu-id="0ea7c-135">그리고 `PageModel` 클래스가 포함된 파일의 이름은 *Pages/Index2.cshtml.cs*입니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-135">The file containing the `PageModel` class is named *Pages/Index2.cshtml.cs*.</span></span>

<span data-ttu-id="0ea7c-136">페이지에 대한 URL 경로 연결은 파일 시스템 상의 페이지 위치에 따라 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-136">The associations of URL paths to pages are determined by the page's location in the file system.</span></span> <span data-ttu-id="0ea7c-137">다음 표는 Razor 페이지 경로 및 그와 일치하는 URL을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-137">The following table shows a Razor Page path and the matching URL:</span></span>

| <span data-ttu-id="0ea7c-138">파일 이름 및 경로</span><span class="sxs-lookup"><span data-stu-id="0ea7c-138">File name and path</span></span>               | <span data-ttu-id="0ea7c-139">일치하는 URL</span><span class="sxs-lookup"><span data-stu-id="0ea7c-139">matching URL</span></span> |
| ----------------- | ------------ |
| <span data-ttu-id="0ea7c-140">*/Pages/Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="0ea7c-140">*/Pages/Index.cshtml*</span></span> | <span data-ttu-id="0ea7c-141">`/` 또는 `/Index`</span><span class="sxs-lookup"><span data-stu-id="0ea7c-141">`/` or `/Index`</span></span> |
| <span data-ttu-id="0ea7c-142">*/Pages/Contact.cshtml*</span><span class="sxs-lookup"><span data-stu-id="0ea7c-142">*/Pages/Contact.cshtml*</span></span> | `/Contact` |
| <span data-ttu-id="0ea7c-143">*/Pages/Store/Contact.cshtml*</span><span class="sxs-lookup"><span data-stu-id="0ea7c-143">*/Pages/Store/Contact.cshtml*</span></span> | `/Store/Contact` |
| <span data-ttu-id="0ea7c-144">*/Pages/Store/Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="0ea7c-144">*/Pages/Store/Index.cshtml*</span></span> | <span data-ttu-id="0ea7c-145">`/Store` 또는 `/Store/Index`</span><span class="sxs-lookup"><span data-stu-id="0ea7c-145">`/Store` or `/Store/Index`</span></span> |

<span data-ttu-id="0ea7c-146">메모:</span><span class="sxs-lookup"><span data-stu-id="0ea7c-146">Notes:</span></span>

* <span data-ttu-id="0ea7c-147">런타임은 기본적으로 *Pages* 폴더에서 Razor 페이지 파일을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-147">The runtime looks for Razor Pages files in the *Pages* folder by default.</span></span>
* <span data-ttu-id="0ea7c-148">URL에 페이지가 지정되어 있지 않을 경우 `Index`가 기본 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-148">`Index` is the default page when a URL doesn't include a page.</span></span>

## <a name="write-a-basic-form"></a><span data-ttu-id="0ea7c-149">기본 양식 작성</span><span class="sxs-lookup"><span data-stu-id="0ea7c-149">Write a basic form</span></span>

<span data-ttu-id="0ea7c-150">Razor 페이지는 앱을 만들때 웹 브라우저에서 사용되는 일반적인 패턴을 손쉽게 구현할 수 있도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-150">Razor Pages is designed to make common patterns used with web browsers easy to implement when building an app.</span></span> <span data-ttu-id="0ea7c-151">[모델 바인딩](xref:mvc/models/model-binding), [태그 도우미](xref:mvc/views/tag-helpers/intro) 및 HTML 도우미는 모두 Razor 페이지 클래스에 정의된 속성을 통해서 *정확하게 동작*합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-151">[Model binding](xref:mvc/models/model-binding), [Tag Helpers](xref:mvc/views/tag-helpers/intro), and HTML helpers all *just work* with the properties defined in a Razor Page class.</span></span> <span data-ttu-id="0ea7c-152">`Contact` 모델에 대한 기본적인 "연락처" 양식을 구현하는 페이지를 생각해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-152">Consider a page that implements a basic "contact us" form for the `Contact` model:</span></span>

<span data-ttu-id="0ea7c-153">이 문서의 예제에서 `DbContext`는 [Startup.cs](https://github.com/aspnet/Docs/blob/master/aspnetcore/razor-pages/index/sample/RazorPagesContacts/Startup.cs#L15-L16) 파일에서 초기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-153">For the samples in this document, the `DbContext` is initialized in the [Startup.cs](https://github.com/aspnet/Docs/blob/master/aspnetcore/razor-pages/index/sample/RazorPagesContacts/Startup.cs#L15-L16) file.</span></span>

[!code-cs[](index/sample/RazorPagesContacts/Startup.cs?highlight=15-16)]

<span data-ttu-id="0ea7c-154">데이터 모델은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-154">The data model:</span></span>

[!code-cs[](index/sample/RazorPagesContacts/Data/Customer.cs)]

<span data-ttu-id="0ea7c-155">db 컨텍스트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-155">The db context:</span></span>

[!code-cs[](index/sample/RazorPagesContacts/Data/AppDbContext.cs)]

<span data-ttu-id="0ea7c-156">*Pages/Create.cshtml* 뷰 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-156">The *Pages/Create.cshtml* view file:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts/Pages/Create.cshtml)]

<span data-ttu-id="0ea7c-157">*Pages/Create.cshtml.cs* 페이지 모델은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-157">The *Pages/Create.cshtml.cs* page model:</span></span>

[!code-cs[](index/sample/RazorPagesContacts/Pages/Create.cshtml.cs?name=snippet_ALL)]

<span data-ttu-id="0ea7c-158">규약에 따라 `PageModel` 클래스의 이름은 `<PageName>Model`로 지정하며 페이지와 동일한 네임스페이스에 위치합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-158">By convention, the `PageModel` class is called `<PageName>Model` and is in the same namespace as the page.</span></span>

<span data-ttu-id="0ea7c-159">`PageModel` 클래스를 사용하면 페이지의 논리를 페이지의 표현으로부터 분리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-159">The `PageModel` class allows separation of the logic of a page from its presentation.</span></span> <span data-ttu-id="0ea7c-160">이 클래스는 페이지로 전송된 요청에 대한 페이지 처리기와 페이지를 렌더링하기 위해 사용되는 데이터를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-160">It defines page handlers for requests sent to the page and the data used to render the page.</span></span> <span data-ttu-id="0ea7c-161">이렇게 분리함으로써 [종속성 주입](xref:fundamentals/dependency-injection)을 통해서 페이지의 종속성을 관리할 수 있고 페이지를 [단위 테스트](xref:test/razor-pages-tests) 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-161">This separation allows you to manage page dependencies through [dependency injection](xref:fundamentals/dependency-injection) and to [unit test](xref:test/razor-pages-tests) the pages.</span></span>

<span data-ttu-id="0ea7c-162">페이지에는 `POST` 요청에서 실행되는 `OnPostAsync` *처리기 메서드*가 있습니다(사용자가 폼을 게시할 때).</span><span class="sxs-lookup"><span data-stu-id="0ea7c-162">The page has an `OnPostAsync` *handler method*, which runs on `POST` requests (when a user posts the form).</span></span> <span data-ttu-id="0ea7c-163">HTTP 동사에 대한 처리기 메서드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-163">You can add handler methods for any HTTP verb.</span></span> <span data-ttu-id="0ea7c-164">가장 일반적인 처리기는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-164">The most common handlers are:</span></span>

* <span data-ttu-id="0ea7c-165">`OnGet` - 페이지에 필요한 상태를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-165">`OnGet` to initialize state needed for the page.</span></span> <span data-ttu-id="0ea7c-166">[OnGet](#OnGet) 샘플.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-166">[OnGet](#OnGet) sample.</span></span>
* <span data-ttu-id="0ea7c-167">`OnPost` - 제출에서 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-167">`OnPost` to handle form submissions.</span></span>

<span data-ttu-id="0ea7c-168">`Async` 명명 접미사는 선택 사항이지만 비동기 함수에 대한 규칙에서 종종 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-168">The `Async` naming suffix is optional but is often used by convention for asynchronous functions.</span></span> <span data-ttu-id="0ea7c-169">이전 예제의 `OnPostAsync` 코드는 일반적으로 컨트롤러에서 작성되는 것과 비슷해 보입니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-169">The `OnPostAsync` code in the preceding example looks similar to what you would normally write in a controller.</span></span> <span data-ttu-id="0ea7c-170">이전 코드는 Razor 페이지에 일반적인 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-170">The preceding code is typical for Razor Pages.</span></span> <span data-ttu-id="0ea7c-171">[모델 바인딩](xref:mvc/models/model-binding), [유효성 검사](xref:mvc/models/validation) 및 작업 결과 같은 대부분의 MVC 기본 형식이 공유됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-171">Most of the MVC primitives like [model binding](xref:mvc/models/model-binding), [validation](xref:mvc/models/validation), and action results are shared.</span></span>  <!-- Review: Ryan, can we get a list of what is shared and what isn't? -->

<span data-ttu-id="0ea7c-172">이전 `OnPostAsync` 메서드:</span><span class="sxs-lookup"><span data-stu-id="0ea7c-172">The previous `OnPostAsync` method:</span></span>

[!code-cs[](index/sample/RazorPagesContacts/Pages/Create.cshtml.cs?name=snippet_OnPostAsync)]

<span data-ttu-id="0ea7c-173">`OnPostAsync`의 기본 흐름:</span><span class="sxs-lookup"><span data-stu-id="0ea7c-173">The basic flow of `OnPostAsync`:</span></span>

<span data-ttu-id="0ea7c-174">유효성 검사 오류를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-174">Check for validation errors.</span></span>

*  <span data-ttu-id="0ea7c-175">오류가 없는 경우 데이터를 저장하고 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-175">If there are no errors, save the data and redirect.</span></span>
*  <span data-ttu-id="0ea7c-176">오류가 있는 경우 유효성 검사 메시지가 포함된 페이지를 다시 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-176">If there are errors, show the page again with validation messages.</span></span> <span data-ttu-id="0ea7c-177">클라이언트 쪽 유효성 검사는 기존 ASP.NET Core MVC 응용 프로그램과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-177">Client-side validation is identical to traditional ASP.NET Core MVC applications.</span></span> <span data-ttu-id="0ea7c-178">대부분의 경우 유효성 검사 오류는 클라이언트에서 검색되고 서버에는 제출되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-178">In many cases, validation errors would be detected on the client, and never submitted to the server.</span></span>

<span data-ttu-id="0ea7c-179">데이터를 성공적으로 입력하면 `OnPostAsync` 처리기 메서드는 `RedirectToPage` 도우미 메서드를 호출하여 `RedirectToPageResult` 인스턴스를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-179">When the data is entered successfully, the `OnPostAsync` handler method calls the `RedirectToPage` helper method to return an instance of `RedirectToPageResult`.</span></span> <span data-ttu-id="0ea7c-180">`RedirectToPage`는 `RedirectToAction` 또는 `RedirectToRoute`와 비슷하지만 페이지에 대해 사용자 지정된 새 작업 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-180">`RedirectToPage` is a new action result, similar to `RedirectToAction` or `RedirectToRoute`, but customized for pages.</span></span> <span data-ttu-id="0ea7c-181">이전 샘플에서 이 메서드는 루트 인덱스 페이지(`/Index`)로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-181">In the preceding sample, it redirects to the root Index page (`/Index`).</span></span> <span data-ttu-id="0ea7c-182">`RedirectToPage`는 [페이지에 대한 URL 생성](#url_gen) 섹션에서 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-182">`RedirectToPage` is detailed in the [URL generation for Pages](#url_gen) section.</span></span>

<span data-ttu-id="0ea7c-183">서버에 전달되는 유효성 오류가 제출된 폼에 있는 경우 `OnPostAsync` 처리기 메서드는 `Page` 도우미 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-183">When the submitted form has validation errors (that are passed to the server), the`OnPostAsync` handler method calls the `Page` helper method.</span></span> <span data-ttu-id="0ea7c-184">`Page`는 `PageResult` 인스턴스를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-184">`Page` returns an instance of `PageResult`.</span></span> <span data-ttu-id="0ea7c-185">`Page` 반환은 컨트롤의 작업이 `View`를 반환하는 방식과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-185">Returning `Page` is similar to how actions in controllers return `View`.</span></span> <span data-ttu-id="0ea7c-186">`PageResult`는 처리기 메서드의 기본 <!-- Review  --> 반환 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-186">`PageResult` is the default <!-- Review  --> return type for a handler method.</span></span> <span data-ttu-id="0ea7c-187">`void`를 반환하는 처리기 메서드는 페이지를 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-187">A handler method that returns `void` renders the page.</span></span>

<span data-ttu-id="0ea7c-188">`Customer` 속성은 `[BindProperty]` 특성을 사용하여 모델 바인딩으로 옵트인(opt in)합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-188">The `Customer` property uses `[BindProperty]` attribute to opt in to model binding.</span></span>

[!code-cs[](index/sample/RazorPagesContacts/Pages/Create.cshtml.cs?name=snippet_PageModel&highlight=10-11)]

<span data-ttu-id="0ea7c-189">Razor 페이지는 기본적으로 GET이 아닌 동사에만 속성을 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-189">Razor Pages, by default, bind properties only with non-GET verbs.</span></span> <span data-ttu-id="0ea7c-190">속성에 바인딩하면 작성해야 하는 코드 양이 감소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-190">Binding to properties can reduce the amount of code you have to write.</span></span> <span data-ttu-id="0ea7c-191">바인딩은 동일한 속성을 사용하여 폼 필드(`<input asp-for="Customer.Name" />`)를 렌더링하고 입력을 허용하는 방식으로 코드를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-191">Binding reduces code by using the same property to render form fields (`<input asp-for="Customer.Name" />`) and accept the input.</span></span>

[!INCLUDE[](~/includes/bind-get.md)]

<span data-ttu-id="0ea7c-192">홈페이지(*Index.cshtml*):</span><span class="sxs-lookup"><span data-stu-id="0ea7c-192">The home page (*Index.cshtml*):</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts/Pages/Index.cshtml)]

<span data-ttu-id="0ea7c-193">연결된 `PageModel` 클래스(*Index.cshtml.cs*):</span><span class="sxs-lookup"><span data-stu-id="0ea7c-193">The associated `PageModel` class (*Index.cshtml.cs*):</span></span>

[!code-cs[](index/sample/RazorPagesContacts/Pages/Index.cshtml.cs)]

<span data-ttu-id="0ea7c-194">*Index.cshtml* 파일에는 각 연락처의 편집 링크를 만들기 위해 다음 태그가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-194">The *Index.cshtml* file contains the following markup to create an edit link for each contact:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts/Pages/Index.cshtml?range=21)]

<span data-ttu-id="0ea7c-195">[앵커 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper)는 `asp-route-{value}` 특성을 사용하여 편집 페이지 링크를 생성했습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-195">The [Anchor Tag Helper](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper) used the `asp-route-{value}` attribute to generate a link to the Edit page.</span></span> <span data-ttu-id="0ea7c-196">링크에는 연락처 ID와 함께 경로 데이터가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-196">The link contains route data with the contact ID.</span></span> <span data-ttu-id="0ea7c-197">예를 들어, `http://localhost:5000/Edit/1`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-197">For example, `http://localhost:5000/Edit/1`.</span></span>

<span data-ttu-id="0ea7c-198">*Pages/Edit.cshtml* 파일:</span><span class="sxs-lookup"><span data-stu-id="0ea7c-198">The *Pages/Edit.cshtml* file:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts/Pages/Edit.cshtml?highlight=1)]

<span data-ttu-id="0ea7c-199">첫 번째 줄에는 `@page "{id:int}"` 지시문이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-199">The first line contains the `@page "{id:int}"` directive.</span></span> <span data-ttu-id="0ea7c-200">라우팅 제약 조건 `"{id:int}"`는 `int` 경로 데이터가 포함된 페이지에 대한 요청을 허용하도록 페이지에 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-200">The routing constraint`"{id:int}"` tells the page to accept requests to the page that contain `int` route data.</span></span> <span data-ttu-id="0ea7c-201">페이지에 대한 요청에 `int`로 변환될 수 있는 경로 데이터가 없으면 런타임은 HTTP 404(찾을 수 없음) 오류를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-201">If a request to the page doesn't contain route data that can be converted to an `int`, the runtime returns an HTTP 404 (not found) error.</span></span> <span data-ttu-id="0ea7c-202">ID를 옵션으로 설정하려면 경로 제약 조건에 `?`를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-202">To make the ID optional, append `?` to the route constraint:</span></span>

 ```cshtml
@page "{id:int?}"
```

<span data-ttu-id="0ea7c-203">*Pages/Edit.cshtml.cs* 파일:</span><span class="sxs-lookup"><span data-stu-id="0ea7c-203">The *Pages/Edit.cshtml.cs* file:</span></span>

[!code-cs[](index/sample/RazorPagesContacts/Pages/Edit.cshtml.cs)]

<span data-ttu-id="0ea7c-204">또한 *Index.cshtml* 파일에는 각 고객 연락처의 삭제 단추를 만드는 표시가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-204">The *Index.cshtml* file also contains markup to create a delete button for each customer contact:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts/Pages/Index.cshtml?range=22-23)]

<span data-ttu-id="0ea7c-205">삭제 단추가 HTML로 렌더링되는 경우 해당 `formaction`에는 다음을 위한 매개 변수가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-205">When the delete button is rendered in HTML, its `formaction` includes parameters for:</span></span>

* <span data-ttu-id="0ea7c-206">`asp-route-id` 특성에서 지정된 고객 연락처 ID</span><span class="sxs-lookup"><span data-stu-id="0ea7c-206">The customer contact ID specified by the `asp-route-id` attribute.</span></span>
* <span data-ttu-id="0ea7c-207">`asp-page-handler` 특성에서 지정된 `handler`</span><span class="sxs-lookup"><span data-stu-id="0ea7c-207">The `handler` specified by the `asp-page-handler` attribute.</span></span>

<span data-ttu-id="0ea7c-208">`1`이라는 고객 연락처 ID를 포함한 렌더링된 삭제 단추의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-208">Here is an example of a rendered delete button with a customer contact ID of `1`:</span></span>

```html
<button type="submit" formaction="/?id=1&amp;handler=delete">delete</button>
```

<span data-ttu-id="0ea7c-209">단추를 선택하면 양식 `POST` 요청이 서버에 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-209">When the button is selected, a form `POST` request is sent to the server.</span></span> <span data-ttu-id="0ea7c-210">규칙에 따라 `OnPost[handler]Async` 구성표에 해당하는 `handler` 매개 변수 값을 기반으로 처리기 메서드의 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-210">By convention, the name of the handler method is selected based on the value of the `handler` parameter according to the scheme `OnPost[handler]Async`.</span></span>

<span data-ttu-id="0ea7c-211">`handler`가 이 예제에서 `delete`이기 때문에 `OnPostDeleteAsync` 처리기 메서드는 `POST` 요청을 처리하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-211">Because the `handler` is `delete` in this example, the `OnPostDeleteAsync` handler method is used to process the `POST` request.</span></span> <span data-ttu-id="0ea7c-212">`asp-page-handler`가 `remove`와 같은 다른 값으로 설정되면 `OnPostRemoveAsync`라는 이름의 페이지 처리기 메서드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-212">If the `asp-page-handler` is set to a different value, such as `remove`, a page handler method with the name `OnPostRemoveAsync` is selected.</span></span>

[!code-cs[](index/sample/RazorPagesContacts/Pages/Index.cshtml.cs?range=26-37)]

<span data-ttu-id="0ea7c-213">`OnPostDeleteAsync` 메서드는 다음과 같은 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-213">The `OnPostDeleteAsync` method:</span></span>

* <span data-ttu-id="0ea7c-214">쿼리 문자열에서 `id`를 수용합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-214">Accepts the `id` from the query string.</span></span>
* <span data-ttu-id="0ea7c-215">`FindAsync`를 사용하여 고객 연락처의 데이터베이스를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-215">Queries the database for the customer contact with `FindAsync`.</span></span>
* <span data-ttu-id="0ea7c-216">고객 연락처를 찾으면 고객 연락처의 목록에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-216">If the customer contact is found, they're removed from the list of customer contacts.</span></span> <span data-ttu-id="0ea7c-217">데이터베이스가 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-217">The database is updated.</span></span>
* <span data-ttu-id="0ea7c-218">`RedirectToPage`를 호출하여 루트 인덱스 페이지(`/Index`)를 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-218">Calls `RedirectToPage` to redirect to the root Index page (`/Index`).</span></span>

::: moniker range=">= aspnetcore-2.1"

## <a name="mark-page-properties-as-required"></a><span data-ttu-id="0ea7c-219">페이지 속성을 필수로 표시</span><span class="sxs-lookup"><span data-stu-id="0ea7c-219">Mark page properties as required</span></span>

<span data-ttu-id="0ea7c-220">`PageModel`의 속성은 [필수](/dotnet/api/system.componentmodel.dataannotations.requiredattribute) 특성으로 데코레이팅될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-220">Properties on a `PageModel` can be decorated with the [Required](/dotnet/api/system.componentmodel.dataannotations.requiredattribute) attribute:</span></span>

[!code-cs[](index/sample/Create.cshtml.cs?highlight=3,15-16)]

<span data-ttu-id="0ea7c-221">자세한 내용은 [모델 유효성 검사](xref:mvc/models/validation)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-221">For more information, see [Model validation](xref:mvc/models/validation).</span></span>

## <a name="manage-head-requests-with-the-onget-handler"></a><span data-ttu-id="0ea7c-222">OnGet 처리기를 사용하여 HEAD 요청 관리</span><span class="sxs-lookup"><span data-stu-id="0ea7c-222">Manage HEAD requests with the OnGet handler</span></span>

<span data-ttu-id="0ea7c-223">HEAD 요청을 사용하면 특정 리소스의 헤더를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-223">HEAD requests allow you to retrieve the headers for a specific resource.</span></span> <span data-ttu-id="0ea7c-224">GET 요청과 달리 HEAD 요청은 응답 본문을 반환하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-224">Unlike GET requests, HEAD requests don't return a response body.</span></span>

<span data-ttu-id="0ea7c-225">일반적으로 HEAD 처리기는 HEAD 요청에 대해 생성 및 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-225">Ordinarily, a HEAD handler is created and called for HEAD requests:</span></span> 

```csharp
public void OnHead()
{
    HttpContext.Response.Headers.Add("HandledBy", "Handled by OnHead!");
}
```

<span data-ttu-id="0ea7c-226">HEAD 처리기(`OnHead`)가 정의되지 않으면 Razor 페이지는 ASP.NET Core 2.1 이상에서 GET 페이지 처리기(`OnGet`) 호출로 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-226">If no HEAD handler (`OnHead`) is defined, Razor Pages falls back to calling the GET page handler (`OnGet`) in ASP.NET Core 2.1 or later.</span></span> <span data-ttu-id="0ea7c-227">ASP.NET Core 2.1 및 2.2에서 이 동작은 `Startup.Configure`의 [SetCompatibilityVersion](xref:mvc/compatibility-version)에서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-227">In ASP.NET Core 2.1 and 2.2, this behavior occurs with the [SetCompatibilityVersion](xref:mvc/compatibility-version) in `Startup.Configure`:</span></span>

```csharp
services.AddMvc()
    .SetCompatibilityVersion(Microsoft.AspNetCore.Mvc.CompatibilityVersion.Version_2_1);
```

<span data-ttu-id="0ea7c-228">기본 템플릿은 ASP.NET Core 2.1 및 2.2에서 `SetCompatibilityVersion` 호출을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-228">The default templates generate the `SetCompatibilityVersion` call in ASP.NET Core 2.1 and 2.2.</span></span>

<span data-ttu-id="0ea7c-229">`SetCompatibilityVersion`은 효과적으로 Razor 페이지 옵션 `AllowMappingHeadRequestsToGetHandler`를 `true`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-229">`SetCompatibilityVersion` effectively sets the Razor Pages option `AllowMappingHeadRequestsToGetHandler` to `true`.</span></span>

<span data-ttu-id="0ea7c-230">`SetCompatibilityVersion`을 사용하여 모든 2.1 동작을 옵트인하는 대신 특정 동작을 명시적으로 옵트인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-230">Rather than opting into all 2.1 behaviors with `SetCompatibilityVersion`, you can explicitly opt-in to specific behaviors.</span></span> <span data-ttu-id="0ea7c-231">다음 코드는 HEAD 요청을 GET 처리기에 매핑을 옵트인합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-231">The following code opts into the mapping HEAD requests to the GET handler.</span></span>

```csharp
services.AddMvc()
    .AddRazorPagesOptions(options =>
    {
        options.AllowMappingHeadRequestsToGetHandler = true;
    });
```

::: moniker-end

<a name="xsrf"></a>

## <a name="xsrfcsrf-and-razor-pages"></a><span data-ttu-id="0ea7c-232">XSRF/CSRF 및 Razor 페이지</span><span class="sxs-lookup"><span data-stu-id="0ea7c-232">XSRF/CSRF and Razor Pages</span></span>

<span data-ttu-id="0ea7c-233">[위조 방지 유효성 검사](xref:security/anti-request-forgery)에 대한 코드를 작성할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-233">You don't have to write any code for [antiforgery validation](xref:security/anti-request-forgery).</span></span> <span data-ttu-id="0ea7c-234">위조 방지 토큰 생성 및 유효성 검사는 Razor 페이지에 자동으로 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-234">Antiforgery token generation and validation are automatically included in Razor Pages.</span></span>

<a name="layout"></a>
## <a name="using-layouts-partials-templates-and-tag-helpers-with-razor-pages"></a><span data-ttu-id="0ea7c-235">Razor 페이지와 함께 레이아웃, 부분, 템플릿 및 태그 도우미 사용</span><span class="sxs-lookup"><span data-stu-id="0ea7c-235">Using Layouts, partials, templates, and Tag Helpers with Razor Pages</span></span>

<span data-ttu-id="0ea7c-236">페이지는 Razor 보기 엔진의 모든 기능과 함께 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-236">Pages work with all the capabilities of the Razor view engine.</span></span> <span data-ttu-id="0ea7c-237">레이아웃, 부분, 템플릿, 태그 도우미, *_ViewStart.cshtml*, *_ViewImports.cshtml*은 기존 Razor 뷰와 동일한 방식으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-237">Layouts, partials, templates, Tag Helpers, *_ViewStart.cshtml*, *_ViewImports.cshtml* work in the same way they do for conventional Razor views.</span></span>

<span data-ttu-id="0ea7c-238">이러한 기능 중 일부를 활용하여 이 페이지의 문제를 해결해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-238">Let's declutter this page by taking advantage of some of those capabilities.</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="0ea7c-239">[레이아웃 페이지](xref:mvc/views/layout)를 *Pages/Shared/_Layout.cshtml*에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-239">Add a [layout page](xref:mvc/views/layout) to *Pages/Shared/_Layout.cshtml*:</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="0ea7c-240">[레이아웃 페이지](xref:mvc/views/layout)를 *Pages/_Layout.cshtml*에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-240">Add a [layout page](xref:mvc/views/layout) to *Pages/_Layout.cshtml*:</span></span>

::: moniker-end

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/_LayoutSimple.cshtml)]

<span data-ttu-id="0ea7c-241">[레이아웃](xref:mvc/views/layout):</span><span class="sxs-lookup"><span data-stu-id="0ea7c-241">The [Layout](xref:mvc/views/layout):</span></span>

* <span data-ttu-id="0ea7c-242">각 페이지의 레이아웃을 제어합니다(페이지가 레이아웃에서 옵트아웃(opt out)되지 않는 경우).</span><span class="sxs-lookup"><span data-stu-id="0ea7c-242">Controls the layout of each page (unless the page opts out of layout).</span></span>
* <span data-ttu-id="0ea7c-243">JavaScript 및 스타일시트 같은 HTML 구조를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-243">Imports HTML structures such as JavaScript and stylesheets.</span></span>

<span data-ttu-id="0ea7c-244">자세한 내용은 [레이아웃 페이지](xref:mvc/views/layout)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-244">See [layout page](xref:mvc/views/layout) for more information.</span></span>

<span data-ttu-id="0ea7c-245">[Layout](xref:mvc/views/layout#specifying-a-layout) 속성은 *Pages/_ViewStart.cshtml*에서 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-245">The [Layout](xref:mvc/views/layout#specifying-a-layout) property is set in *Pages/_ViewStart.cshtml*:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/_ViewStart.cshtml)]

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="0ea7c-246">레이아웃은 *Pages/Shared* 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-246">The layout is in the *Pages/Shared* folder.</span></span> <span data-ttu-id="0ea7c-247">페이지는 현재 페이지와 동일한 폴더에서 시작하여 다른 뷰(레이아웃, 템플릿, 부분)를 계층 구조로 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-247">Pages look for other views (layouts, templates, partials) hierarchically, starting in the same folder as the current page.</span></span> <span data-ttu-id="0ea7c-248">*Pages/Shared* 폴더의 레이아웃은 *Pages* 폴더 아래의 Razor 페이지에서 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-248">A layout in the *Pages/Shared* folder can be used from any Razor page under the *Pages* folder.</span></span>

<span data-ttu-id="0ea7c-249">레이아웃 파일은 *Pages/Shared* 폴더로 이동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-249">The layout file should go in the *Pages/Shared* folder.</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="0ea7c-250">레이아웃은 *Pages* 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-250">The layout is in the *Pages* folder.</span></span> <span data-ttu-id="0ea7c-251">페이지는 현재 페이지와 동일한 폴더에서 시작하여 다른 뷰(레이아웃, 템플릿, 부분)를 계층 구조로 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-251">Pages look for other views (layouts, templates, partials) hierarchically, starting in the same folder as the current page.</span></span> <span data-ttu-id="0ea7c-252">*Pages* 폴더의 레이아웃은 *Pages* 폴더 아래의 Razor 페이지에서 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-252">A layout in the *Pages* folder can be used from any Razor page under the *Pages* folder.</span></span>

::: moniker-end

<span data-ttu-id="0ea7c-253">레이아웃 파일은 *Views/Shared* 폴더에 두지 **않는** 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-253">We recommend you **not** put the layout file in the *Views/Shared* folder.</span></span> <span data-ttu-id="0ea7c-254">*Views/Shared*는 MVC 뷰 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-254">*Views/Shared* is an MVC views pattern.</span></span> <span data-ttu-id="0ea7c-255">Razor 페이지는 경로 규칙이 아니라 폴더 계층 구조를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-255">Razor Pages are meant to rely on folder hierarchy, not path conventions.</span></span>

<span data-ttu-id="0ea7c-256">Razor 페이지의 뷰 검색에는 *Pages* 폴더가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-256">View search from a Razor Page includes the *Pages* folder.</span></span> <span data-ttu-id="0ea7c-257">MVC 컨트롤러 및 기존 Razor 뷰에서 사용 중인 레이아웃, 템플릿 및 부분이 *제대로 작동*합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-257">The layouts, templates, and partials you're using with MVC controllers and conventional Razor views *just work*.</span></span>

<span data-ttu-id="0ea7c-258">*Pages/_ViewImports.cshtml* 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-258">Add a *Pages/_ViewImports.cshtml* file:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/_ViewImports.cshtml)]

<span data-ttu-id="0ea7c-259">`@namespace`는 자습서의 뒷부분에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-259">`@namespace` is explained later in the tutorial.</span></span> <span data-ttu-id="0ea7c-260">`@addTagHelper` 지시문은 [기본 제공 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/Index)를 *Pages* 폴더의 모든 페이지에 도입합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-260">The `@addTagHelper` directive brings in the [built-in Tag Helpers](xref:mvc/views/tag-helpers/builtin-th/Index) to all the pages in the *Pages* folder.</span></span>

<a name="namespace"></a>

<span data-ttu-id="0ea7c-261">`@namespace` 지시문은 페이지에서 명시적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-261">When the `@namespace` directive is used explicitly on a page:</span></span>

[!code-cshtml[](index/sample/RazorPagesIntro/Pages/Customers/Namespace2.cshtml?highlight=2)]

<span data-ttu-id="0ea7c-262">이 지시문은 페이지에 대한 네임스페이스를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-262">The directive sets the namespace for the page.</span></span> <span data-ttu-id="0ea7c-263">`@model` 지시문에는 네임스페이스가 포함될 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-263">The `@model` directive doesn't need to include the namespace.</span></span>

<span data-ttu-id="0ea7c-264">`@namespace` 지시문이 *_ViewImports.cshtml*에 포함되면 지정된 네임스페이스는 `@namespace` 지시문을 가져오는 페이지의 생성된 네임스페이스에 대한 접두사를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-264">When the `@namespace` directive is contained in *_ViewImports.cshtml*, the specified namespace supplies the prefix for the generated namespace in the Page that imports the `@namespace` directive.</span></span> <span data-ttu-id="0ea7c-265">생성된 네임스페이스의 나머지 부분(접미사 부분)은 *_ViewImports.cshtml*이 포함된 폴더와 페이지가 포함된 폴더 사이의 점으로 구분된 상대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-265">The rest of the generated namespace (the suffix portion) is the dot-separated relative path between the folder containing *_ViewImports.cshtml* and the folder containing the page.</span></span>

<span data-ttu-id="0ea7c-266">예를 들어 `PageModel` 클래스 *Pages/Customers/Edit.cshtml.cs*는 네임스페이스를 명시적으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-266">For example, the `PageModel` class *Pages/Customers/Edit.cshtml.cs* explicitly sets the namespace:</span></span>

[!code-cs[](index/sample/RazorPagesContacts2/Pages/Customers/Edit.cshtml.cs?name=snippet_namespace)]

<span data-ttu-id="0ea7c-267">*Pages/_ViewImports.cshtml* 파일은 다음 네임스페이스를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-267">The *Pages/_ViewImports.cshtml* file sets the following namespace:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/_ViewImports.cshtml?highlight=1)]

<span data-ttu-id="0ea7c-268">*Pages/Customers/Edit.cshtml* Razor 페이지에 대한 생성된 네임스페이스는 `PageModel` 클래스와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-268">The generated namespace for the *Pages/Customers/Edit.cshtml* Razor Page is the same as the `PageModel` class.</span></span>

<span data-ttu-id="0ea7c-269">`@namespace` *는 기존 Razor 뷰에서도 작동합니다.*</span><span class="sxs-lookup"><span data-stu-id="0ea7c-269">`@namespace` *also works with conventional Razor views.*</span></span>

<span data-ttu-id="0ea7c-270">원래 *Pages/Create.cshtml* 뷰 파일:</span><span class="sxs-lookup"><span data-stu-id="0ea7c-270">The original *Pages/Create.cshtml* view file:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts/Pages/Create.cshtml?highlight=2)]

<span data-ttu-id="0ea7c-271">업데이트된 *Pages/Create.cshtml* 뷰 파일:</span><span class="sxs-lookup"><span data-stu-id="0ea7c-271">The updated *Pages/Create.cshtml* view file:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/Customers/Create.cshtml?highlight=2)]

<span data-ttu-id="0ea7c-272">[Razor 페이지 시작 프로젝트](#rpvs17)에는 클라이언트 쪽 유효성 검사를 연결하는 *Pages/_ValidationScriptsPartial.cshtml*이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-272">The [Razor Pages starter project](#rpvs17) contains the *Pages/_ValidationScriptsPartial.cshtml*, which hooks up client-side validation.</span></span>

<span data-ttu-id="0ea7c-273">부분 뷰에 대한 자세한 내용은 <xref:mvc/views/partial>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-273">For more information on partial views, see <xref:mvc/views/partial>.</span></span>

<a name="url_gen"></a>

## <a name="url-generation-for-pages"></a><span data-ttu-id="0ea7c-274">페이지에 대한 URL 생성</span><span class="sxs-lookup"><span data-stu-id="0ea7c-274">URL generation for Pages</span></span>

<span data-ttu-id="0ea7c-275">이전에 표시된 `Create` 페이지에서는 `RedirectToPage`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-275">The `Create` page, shown previously, uses `RedirectToPage`:</span></span>

[!code-cs[](index/sample/RazorPagesContacts/Pages/Create.cshtml.cs?name=snippet_OnPostAsync&highlight=10)]

<span data-ttu-id="0ea7c-276">앱에는 다음 파일/폴더 구조가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-276">The app has the following file/folder structure:</span></span>

* <span data-ttu-id="0ea7c-277">*/Pages*</span><span class="sxs-lookup"><span data-stu-id="0ea7c-277">*/Pages*</span></span>

  * <span data-ttu-id="0ea7c-278">*Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="0ea7c-278">*Index.cshtml*</span></span>
  * <span data-ttu-id="0ea7c-279">*/Customers*</span><span class="sxs-lookup"><span data-stu-id="0ea7c-279">*/Customers*</span></span>

    * <span data-ttu-id="0ea7c-280">*Create.cshtml*</span><span class="sxs-lookup"><span data-stu-id="0ea7c-280">*Create.cshtml*</span></span>
    * <span data-ttu-id="0ea7c-281">*Edit.cshtml*</span><span class="sxs-lookup"><span data-stu-id="0ea7c-281">*Edit.cshtml*</span></span>
    * <span data-ttu-id="0ea7c-282">*Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="0ea7c-282">*Index.cshtml*</span></span>

<span data-ttu-id="0ea7c-283">*Pages/Customers/Create.cshtml* 및 *Pages/Customers/Edit.cshtml* 페이지는 성공 후에 *Pages/Index.cshtml*로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-283">The *Pages/Customers/Create.cshtml* and *Pages/Customers/Edit.cshtml* pages redirect to *Pages/Index.cshtml* after success.</span></span> <span data-ttu-id="0ea7c-284">문자열 `/Index`는 이전 페이지에 액세스하기 위한 URI 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-284">The string `/Index` is part of the URI to access the preceding page.</span></span> <span data-ttu-id="0ea7c-285">문자열 `/Index`는 *Pages/Index.cshtml* 페이지의 URI를 생성하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-285">The string `/Index` can be used to generate URIs to the *Pages/Index.cshtml* page.</span></span> <span data-ttu-id="0ea7c-286">예:</span><span class="sxs-lookup"><span data-stu-id="0ea7c-286">For example:</span></span>

* `Url.Page("/Index", ...)`
* `<a asp-page="/Index">My Index Page</a>`
* `RedirectToPage("/Index")`

<span data-ttu-id="0ea7c-287">페이지 이름은 루트 */Pages* 폴더에서 선행 `/`를 포함한 페이지 경로입니다(예: `/Index`).</span><span class="sxs-lookup"><span data-stu-id="0ea7c-287">The page name is the path to the page from the root */Pages* folder including a leading `/` (for example, `/Index`).</span></span> <span data-ttu-id="0ea7c-288">이전 URL 생성 샘플은 URL 하드 코딩보다 향상된 옵션과 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-288">The preceding URL generation samples offer enhanced options and functional capabilities over hardcoding a URL.</span></span> <span data-ttu-id="0ea7c-289">URL 생성은 [라우팅](xref:mvc/controllers/routing)을 사용하며 경로가 대상 경로에서 정의되는 방식에 따라 매개 변수를 생성하고 인코딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-289">URL generation uses [routing](xref:mvc/controllers/routing) and can generate and encode parameters according to how the route is defined in the destination path.</span></span>

<span data-ttu-id="0ea7c-290">페이지에 대한 URL 생성은 상대적 이름을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-290">URL generation for pages supports relative names.</span></span> <span data-ttu-id="0ea7c-291">다음 표에서는 *Pages/Customers/Create.cshtml*에서 다른 `RedirectToPage` 매개 변수를 통해 선택되는 인덱스 페이지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-291">The following table shows which Index page is selected with different `RedirectToPage` parameters from *Pages/Customers/Create.cshtml*:</span></span>

| <span data-ttu-id="0ea7c-292">RedirectToPage(x)</span><span class="sxs-lookup"><span data-stu-id="0ea7c-292">RedirectToPage(x)</span></span>| <span data-ttu-id="0ea7c-293">페이지</span><span class="sxs-lookup"><span data-stu-id="0ea7c-293">Page</span></span> |
| ----------------- | ------------ |
| <span data-ttu-id="0ea7c-294">RedirectToPage("/Index")</span><span class="sxs-lookup"><span data-stu-id="0ea7c-294">RedirectToPage("/Index")</span></span> | <span data-ttu-id="0ea7c-295">*Pages/Index*</span><span class="sxs-lookup"><span data-stu-id="0ea7c-295">*Pages/Index*</span></span> |
| <span data-ttu-id="0ea7c-296">RedirectToPage("./Index")</span><span class="sxs-lookup"><span data-stu-id="0ea7c-296">RedirectToPage("./Index");</span></span> | <span data-ttu-id="0ea7c-297">*Pages/Customers/Index*</span><span class="sxs-lookup"><span data-stu-id="0ea7c-297">*Pages/Customers/Index*</span></span> |
| <span data-ttu-id="0ea7c-298">RedirectToPage("../Index")</span><span class="sxs-lookup"><span data-stu-id="0ea7c-298">RedirectToPage("../Index")</span></span> | <span data-ttu-id="0ea7c-299">*Pages/Index*</span><span class="sxs-lookup"><span data-stu-id="0ea7c-299">*Pages/Index*</span></span> |
| <span data-ttu-id="0ea7c-300">RedirectToPage("Index")</span><span class="sxs-lookup"><span data-stu-id="0ea7c-300">RedirectToPage("Index")</span></span>  | <span data-ttu-id="0ea7c-301">*Pages/Customers/Index*</span><span class="sxs-lookup"><span data-stu-id="0ea7c-301">*Pages/Customers/Index*</span></span> |

<span data-ttu-id="0ea7c-302">`RedirectToPage("Index")`, `RedirectToPage("./Index")` 및 `RedirectToPage("../Index")`는 <em>상대적 이름</em>입니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-302">`RedirectToPage("Index")`, `RedirectToPage("./Index")`, and `RedirectToPage("../Index")`  are <em>relative names</em>.</span></span> <span data-ttu-id="0ea7c-303">`RedirectToPage` 매개 변수는 현재 페이지의 경로와 <em>결합</em>되어 대상 페이지의 이름을 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-303">The `RedirectToPage` parameter is <em>combined</em> with the path of the current page to compute the name of the destination page.</span></span>  <!-- Review: Original had The provided string is combined with the page name of the current page to compute the name of the destination page.  page name, not page path -->

<span data-ttu-id="0ea7c-304">상대적 이름 연결은 구조가 복잡한 사이트를 빌드할 때 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-304">Relative name linking is useful when building sites with a complex structure.</span></span> <span data-ttu-id="0ea7c-305">상대적 이름을 사용하여 한 폴더의 여러 페이지 간을 연결하는 경우 해당 폴더의 이름을 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-305">If you use relative names to link between pages in a folder, you can rename that folder.</span></span> <span data-ttu-id="0ea7c-306">그래도 모든 링크가 작동합니다(폴더 이름을 포함하지 않기 때문).</span><span class="sxs-lookup"><span data-stu-id="0ea7c-306">All the links still work (because they didn't include the folder name).</span></span>

::: moniker range=">= aspnetcore-2.1"

## <a name="viewdata-attribute"></a><span data-ttu-id="0ea7c-307">ViewData 특성</span><span class="sxs-lookup"><span data-stu-id="0ea7c-307">ViewData attribute</span></span>

<span data-ttu-id="0ea7c-308">[ViewDataAttribute](/dotnet/api/microsoft.aspnetcore.mvc.viewdataattribute)를 사용하여 데이터를 페이지에 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-308">Data can be passed to a page with [ViewDataAttribute](/dotnet/api/microsoft.aspnetcore.mvc.viewdataattribute).</span></span> <span data-ttu-id="0ea7c-309">`[ViewData]`로 데코레이팅된 컨트롤러 또는 Razor 페이지 모델의 속성은 값을 [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary)에 저장하고 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-309">Properties on controllers or Razor Page models decorated with `[ViewData]` have their values stored and loaded from the [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary).</span></span>

<span data-ttu-id="0ea7c-310">다음 예제에서 `AboutModel`에는 `[ViewData]`으로 데코레이팅된 `Title` 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-310">In the following example, the `AboutModel` contains a `Title` property decorated with `[ViewData]`.</span></span> <span data-ttu-id="0ea7c-311">`Title` 속성은 정보 페이지의 제목에 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-311">The `Title` property is set to the title of the About page:</span></span>

```csharp
public class AboutModel : PageModel
{
    [ViewData]
    public string Title { get; } = "About";

    public void OnGet()
    {
    }
}
```

<span data-ttu-id="0ea7c-312">정보 페이지에서 `Title` 속성을 모델 속성으로 액세스하세요.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-312">In the About page, access the `Title` property as a model property:</span></span>

```cshtml
<h1>@Model.Title</h1>
```

<span data-ttu-id="0ea7c-313">레이아웃에서 제목은 ViewData 사전에서 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-313">In the layout, the title is read from the ViewData dictionary:</span></span>

```cshtml
<!DOCTYPE html>
<html lang="en">
<head>
    <title>@ViewData["Title"] - WebApplication</title>
    ...
```

::: moniker-end

## <a name="tempdata"></a><span data-ttu-id="0ea7c-314">TempData</span><span class="sxs-lookup"><span data-stu-id="0ea7c-314">TempData</span></span>

<span data-ttu-id="0ea7c-315">ASP.NET Core는 [TempData](/dotnet/api/microsoft.aspnetcore.mvc.controller.tempdata?view=aspnetcore-2.0#Microsoft_AspNetCore_Mvc_Controller_TempData) 속성을 [컨트롤러](/dotnet/api/microsoft.aspnetcore.mvc.controller)에서 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-315">ASP.NET Core exposes the [TempData](/dotnet/api/microsoft.aspnetcore.mvc.controller.tempdata?view=aspnetcore-2.0#Microsoft_AspNetCore_Mvc_Controller_TempData) property on a [controller](/dotnet/api/microsoft.aspnetcore.mvc.controller).</span></span> <span data-ttu-id="0ea7c-316">이 속성은 판독될 때까지 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-316">This property stores data until it's read.</span></span> <span data-ttu-id="0ea7c-317">`Keep` 및 `Peek` 메서드를 사용하여 삭제 없이 데이터를 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-317">The `Keep` and `Peek` methods can be used to examine the data without deletion.</span></span> <span data-ttu-id="0ea7c-318">`TempData`는 두 개 이상의 요청에 대한 데이터가 필요할 경우 리디렉션에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-318">`TempData` is  useful for redirection, when data is needed for more than a single request.</span></span>

<span data-ttu-id="0ea7c-319">`[TempData]` 특성은 ASP.NET Core 2.0의 새로운 기능이고 컨트롤러 및 페이지에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-319">The `[TempData]` attribute is new in ASP.NET Core 2.0 and is supported on controllers and pages.</span></span>

<span data-ttu-id="0ea7c-320">다음 코드는 `TempData`를 사용하여 `Message` 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-320">The following code sets the value of `Message` using `TempData`:</span></span>

[!code-cs[](index/sample/RazorPagesContacts2/Pages/Customers/CreateDot.cshtml.cs?highlight=10-11,25&name=snippet_Temp)]

<span data-ttu-id="0ea7c-321">*Pages/Customers/Index.cshtml* 파일의 다음 태그는 `TempData`를 사용하여 `Message` 값을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-321">The following markup in the *Pages/Customers/Index.cshtml* file displays the value of `Message` using `TempData`.</span></span>

```cshtml
<h3>Msg: @Model.Message</h3>
```

<span data-ttu-id="0ea7c-322">*Pages/Customers/Index.cshtml.cs* 페이지 모델은 `[TempData]` 특성을 `Message` 속성에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-322">The *Pages/Customers/Index.cshtml.cs* page model applies the `[TempData]` attribute to the `Message` property.</span></span>

```cs
[TempData]
public string Message { get; set; }
```

<span data-ttu-id="0ea7c-323">자세한 내용은 [TempData](xref:fundamentals/app-state#tempdata)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-323">For more information, see [TempData](xref:fundamentals/app-state#tempdata) .</span></span>

<a name="mhpp"></a>
## <a name="multiple-handlers-per-page"></a><span data-ttu-id="0ea7c-324">페이지당 여러 처리기</span><span class="sxs-lookup"><span data-stu-id="0ea7c-324">Multiple handlers per page</span></span>

<span data-ttu-id="0ea7c-325">다음 페이지는 `asp-page-handler` 태그 도우미를 사용하여 두 개의 페이지 처리기에 대한 태그를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-325">The following page generates markup for two page handlers using the `asp-page-handler` Tag Helper:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/Customers/CreateFATH.cshtml?highlight=12-13)]

<!-- Review: the FormActionTagHelper applies to all <form /> elements on a Razor page, even when there's no `asp-` attribute   -->

<span data-ttu-id="0ea7c-326">이전 예제의 폼에는 두 개의 제출 단추가 있고, 각 단추는 `FormActionTagHelper`를 사용하여 다른 URL에 제출됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-326">The form in the preceding example has two submit buttons, each using the `FormActionTagHelper` to submit to a different URL.</span></span> <span data-ttu-id="0ea7c-327">`asp-page-handler` 특성은 `asp-page`와 함께 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-327">The `asp-page-handler` attribute is a companion to `asp-page`.</span></span> <span data-ttu-id="0ea7c-328">`asp-page-handler`는 페이지에서 정의된 각 처리기 메서드에 제출되는 URL을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-328">`asp-page-handler` generates URLs that submit to each of the handler methods defined by a page.</span></span> <span data-ttu-id="0ea7c-329">샘플이 현재 페이지에 연결되어 있으므로 `asp-page`가 지정되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-329">`asp-page` isn't specified because the sample is linking to the current page.</span></span>

<span data-ttu-id="0ea7c-330">페이지 모델:</span><span class="sxs-lookup"><span data-stu-id="0ea7c-330">The page model:</span></span>

[!code-cs[](index/sample/RazorPagesContacts2/Pages/Customers/CreateFATH.cshtml.cs?highlight=20,32)]

<span data-ttu-id="0ea7c-331">이전 코드는 *명명된 처리기 메서드*를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-331">The preceding code uses *named handler methods*.</span></span> <span data-ttu-id="0ea7c-332">명명된 처리기 메서드를 만들려면 `On<HTTP Verb>` 뒤와 `Async`(있는 경우) 앞에 이름의 텍스트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-332">Named handler methods are created by taking the text in the name after `On<HTTP Verb>` and before `Async` (if present).</span></span> <span data-ttu-id="0ea7c-333">이전 예제에서 페이지 메서드는 OnPost**JoinList**Async 및 OnPost**JoinListUC**Async입니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-333">In the preceding example, the page methods are OnPost**JoinList**Async and OnPost**JoinListUC**Async.</span></span> <span data-ttu-id="0ea7c-334">*OnPost* 및 *Async*가 제거된 처리기 이름은 `JoinList` 및 `JoinListUC`입니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-334">With *OnPost* and *Async* removed, the handler names are `JoinList` and `JoinListUC`.</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/Customers/CreateFATH.cshtml?range=12-13)]

<span data-ttu-id="0ea7c-335">이전 코드를 사용할 경우 `OnPostJoinListAsync`에 제출되는 URL 경로는 `http://localhost:5000/Customers/CreateFATH?handler=JoinList`입니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-335">Using the preceding code, the URL path that submits to `OnPostJoinListAsync` is `http://localhost:5000/Customers/CreateFATH?handler=JoinList`.</span></span> <span data-ttu-id="0ea7c-336">`OnPostJoinListUCAsync`에 제출되는 URL 경로는 `http://localhost:5000/Customers/CreateFATH?handler=JoinListUC`입니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-336">The URL path that submits to `OnPostJoinListUCAsync` is `http://localhost:5000/Customers/CreateFATH?handler=JoinListUC`.</span></span>

## <a name="custom-routes"></a><span data-ttu-id="0ea7c-337">사용자 지정 경로</span><span class="sxs-lookup"><span data-stu-id="0ea7c-337">Custom routes</span></span>

<span data-ttu-id="0ea7c-338">`@page` 지시문을 사용하여 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-338">Use the `@page` directive to:</span></span>

* <span data-ttu-id="0ea7c-339">페이지에 대한 사용자 지정 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-339">Specify a custom route to a page.</span></span> <span data-ttu-id="0ea7c-340">예를 들어 `@page "/Some/Other/Path"`를 사용하여 About 페이지에 대한 경로를 `/Some/Other/Path`로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-340">For example, the route to the About page can be set to `/Some/Other/Path` with `@page "/Some/Other/Path"`.</span></span>
* <span data-ttu-id="0ea7c-341">세그먼트를 페이지의 기본 경로에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-341">Append segments to a page's default route.</span></span> <span data-ttu-id="0ea7c-342">예를 들어 "항목" 세그먼트는 `@page "item"`을 사용하여 페이지의 기본 경로에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-342">For example, an "item" segment can be added to a page's default route with `@page "item"`.</span></span>
* <span data-ttu-id="0ea7c-343">매개 변수를 페이지의 기본 경로에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-343">Append parameters to a page's default route.</span></span> <span data-ttu-id="0ea7c-344">예를 들어 ID 매개 변수 `id`는 `@page "{id}"`가 있는 페이지에 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-344">For example, an ID parameter, `id`, can be required for a page with `@page "{id}"`.</span></span>

<span data-ttu-id="0ea7c-345">경로의 시작 부분에 물결표(`~`)로 지정된 루트 상대 경로가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-345">A root-relative path designated by a tilde (`~`) at the beginning of the path is supported.</span></span> <span data-ttu-id="0ea7c-346">예를 들어 `@page "~/Some/Other/Path"`은 `@page "/Some/Other/Path"`과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-346">For example, `@page "~/Some/Other/Path"` is the same as `@page "/Some/Other/Path"`.</span></span>

<span data-ttu-id="0ea7c-347">경로 템플릿 `@page "{handler?}"`를 지정하여 URL의 쿼리 문자열 `?handler=JoinList`를 경로 세그먼트 `/JoinList`로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-347">You can change the query string `?handler=JoinList` in the URL to a route segment `/JoinList` by specifying the route template `@page "{handler?}"`.</span></span>

<span data-ttu-id="0ea7c-348">URL에서 쿼리 문자열 `?handler=JoinList`를 사용하지 않으려면 경로를 변경하여 처리기 이름을 URL의 경로 부분에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-348">If you don't like the query string `?handler=JoinList` in the URL, you can change the route to put the handler name in the path portion of the URL.</span></span> <span data-ttu-id="0ea7c-349">`@page` 지시문 뒤에 큰따옴표로 묶은 경로 템플릿을 추가하여 경로를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-349">You can customize the route by adding a route template enclosed in double quotes after the `@page` directive.</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/Customers/CreateRoute.cshtml?highlight=1)]

<span data-ttu-id="0ea7c-350">이전 코드를 사용할 경우 `OnPostJoinListAsync`에 제출되는 URL 경로는 `http://localhost:5000/Customers/CreateFATH/JoinList`입니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-350">Using the preceding code, the URL path that submits to `OnPostJoinListAsync` is `http://localhost:5000/Customers/CreateFATH/JoinList`.</span></span> <span data-ttu-id="0ea7c-351">`OnPostJoinListUCAsync`에 제출되는 URL 경로는 `http://localhost:5000/Customers/CreateFATH/JoinListUC`입니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-351">The URL path that submits to `OnPostJoinListUCAsync` is `http://localhost:5000/Customers/CreateFATH/JoinListUC`.</span></span>

<span data-ttu-id="0ea7c-352">`handler` 뒤의 `?`는 경로 매개 변수가 선택 사항임을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-352">The `?` following `handler` means the route parameter is optional.</span></span>

## <a name="configuration-and-settings"></a><span data-ttu-id="0ea7c-353">구성 및 설정</span><span class="sxs-lookup"><span data-stu-id="0ea7c-353">Configuration and settings</span></span>

<span data-ttu-id="0ea7c-354">고급 옵션을 구성하려면 MVC 빌더에서 확장 메서드 `AddRazorPagesOptions`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-354">To configure advanced options, use the extension method `AddRazorPagesOptions` on the MVC builder:</span></span>

[!code-cs[](index/sample/RazorPagesContacts/StartupAdvanced.cs?name=snippet_1)]

<span data-ttu-id="0ea7c-355">현재 `RazorPagesOptions`를 사용하여 페이지의 루트 디렉터리를 설정하거나 페이지에 대한 응용 프로그램 모델 규칙을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-355">Currently you can use the `RazorPagesOptions` to set the root directory for pages, or add application model conventions for pages.</span></span> <span data-ttu-id="0ea7c-356">나중에 이 방법으로 더 큰 확장성을 지원할 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-356">We'll enable more extensibility this way in the future.</span></span>

<span data-ttu-id="0ea7c-357">뷰를 미리 컴파일하려면 [Razor 뷰 컴파일](xref:mvc/views/view-compilation)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-357">To precompile views, see [Razor view compilation](xref:mvc/views/view-compilation) .</span></span>

<span data-ttu-id="0ea7c-358">[샘플 코드를 다운로드하거나 봅니다](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-pages/index/sample).</span><span class="sxs-lookup"><span data-stu-id="0ea7c-358">[Download or view sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-pages/index/sample).</span></span>

<span data-ttu-id="0ea7c-359">이 소개에 따라 빌드되는 [Razor 페이지 시작](xref:tutorials/razor-pages/razor-pages-start)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-359">See [Get started with Razor Pages](xref:tutorials/razor-pages/razor-pages-start), which builds on this introduction.</span></span>

### <a name="specify-that-razor-pages-are-at-the-content-root"></a><span data-ttu-id="0ea7c-360">Razor 페이지를 콘텐츠 루트로 지정</span><span class="sxs-lookup"><span data-stu-id="0ea7c-360">Specify that Razor Pages are at the content root</span></span>

<span data-ttu-id="0ea7c-361">기본적으로 Razor 페이지의 루트 경로는 */Pages* 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-361">By default, Razor Pages are rooted in the */Pages* directory.</span></span> <span data-ttu-id="0ea7c-362">[AddMvc](/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addmvc#Microsoft_Extensions_DependencyInjection_MvcServiceCollectionExtensions_AddMvc_Microsoft_Extensions_DependencyInjection_IServiceCollection_)에 [WithRazorPagesAtContentRoot](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.withrazorpagesatcontentroot)를 추가하여 Razor 페이지를 앱의 콘텐츠 루트([ContentRootPath](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.contentrootpath))로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0ea7c-362">Add [WithRazorPagesAtContentRoot](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.withrazorpagesatcontentroot) to [AddMvc](/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addmvc#Microsoft_Extensions_DependencyInjection_MvcServiceCollectionExtensions_AddMvc_Microsoft_Extensions_DependencyInjection_IServiceCollection_) to specify that your Razor Pages are at the content root ([ContentRootPath](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.contentrootpath)) of the app:</span></span>

```csharp
services.AddMvc()
    .AddRazorPagesOptions(options =>
    {
        ...
    })
    .WithRazorPagesAtContentRoot();
```

### <a name="specify-that-razor-pages-are-at-a-custom-root-directory"></a><span data-ttu-id="0ea7c-363">Razor 페이지가 사용자 지정 루트 디렉터리에 있도록 지정</span><span class="sxs-lookup"><span data-stu-id="0ea7c-363">Specify that Razor Pages are at a custom root directory</span></span>

<span data-ttu-id="0ea7c-364">[AddMvc](/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addmvc#Microsoft_Extensions_DependencyInjection_MvcServiceCollectionExtensions_AddMvc_Microsoft_Extensions_DependencyInjection_IServiceCollection_)에 [WithRazorPagesRoot](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvccorebuilderextensions.withrazorpagesroot)를 추가하여 Razor 페이지가 앱의 사용자 지정 루트 디렉터리에 있도록 지정합니다(상대 경로 제공).</span><span class="sxs-lookup"><span data-stu-id="0ea7c-364">Add [WithRazorPagesRoot](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvccorebuilderextensions.withrazorpagesroot) to [AddMvc](/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addmvc#Microsoft_Extensions_DependencyInjection_MvcServiceCollectionExtensions_AddMvc_Microsoft_Extensions_DependencyInjection_IServiceCollection_) to specify that your Razor Pages are at a custom root directory in the app (provide a relative path):</span></span>

```csharp
services.AddMvc()
    .AddRazorPagesOptions(options =>
    {
        ...
    })
    .WithRazorPagesRoot("/path/to/razor/pages");
```

## <a name="additional-resources"></a><span data-ttu-id="0ea7c-365">추가 자료</span><span class="sxs-lookup"><span data-stu-id="0ea7c-365">Additional resources</span></span>

* <xref:index>
* <xref:mvc/views/razor>
* <xref:tutorials/razor-pages/razor-pages-start>
* <xref:security/authorization/razor-pages-authorization>
* <xref:razor-pages/razor-pages-conventions>
* <xref:test/razor-pages-tests>
* <xref:mvc/views/partial>
