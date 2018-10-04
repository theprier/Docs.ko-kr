---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-controller
title: 컨트롤러 추가 | Microsoft Docs
author: Rick-Anderson
description: '참고: 업데이트 된이이 자습서는 ASP.NET MVC 5 및 Visual Studio 2013을 사용 하는 있습니다. 것이 더 안전 하 고 더 간단 하 게 따르고 데모 중...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 0267d31c-892f-49a1-9e7a-3ae8cc12b2ca
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 6cc64cd9ed7a8a4cf053a63d22214bf31a80147b
ms.sourcegitcommit: 7b4e3936feacb1a8fcea7802aab3e2ea9c8af5b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48576232"
---
<a name="adding-a-controller"></a><span data-ttu-id="de2ec-104">컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="de2ec-104">Adding a Controller</span></span>
====================
<span data-ttu-id="de2ec-105">[Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="de2ec-105">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

> > [!NOTE]
> > <span data-ttu-id="de2ec-106">이 자습서는 업데이트 된 버전을 사용할 수 [여기](../../getting-started/introduction/getting-started.md) 는 ASP.NET MVC 5 및 Visual Studio 2013을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="de2ec-107">보다 안전 하 고 더 간단 하 게 수행 되며 더 많은 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>


<span data-ttu-id="de2ec-108">MVC는 의미 *모델-뷰-컨트롤러*합니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-108">MVC stands for *model-view-controller*.</span></span> <span data-ttu-id="de2ec-109">MVC는 응용 프로그램을 설계, 테스트 및 유지 관리 하기 쉬운 개발을 위한 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-109">MVC is a pattern for developing applications that are well architected, testable and easy to maintain.</span></span> <span data-ttu-id="de2ec-110">MVC 기반 응용 프로그램에는 다음이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-110">MVC-based applications contain:</span></span>

- <span data-ttu-id="de2ec-111">**M** odels: 유효성 검사 논리를 사용 하 여 해당 데이터에 대 한 비즈니스 규칙을 적용 하는 응용 프로그램의 데이터를 나타내는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-111">**M** odels: Classes that represent the data of the application and that use validation logic to enforce business rules for that data.</span></span>
- <span data-ttu-id="de2ec-112">**V** iews: 응용 프로그램 HTML 응답을 동적으로 생성 하는 데 사용 하는 템플릿 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-112">**V** iews: Template files that your application uses to dynamically generate HTML responses.</span></span>
- <span data-ttu-id="de2ec-113">**C** ontrollers: 들어오는 브라우저 요청을 처리 하는 클래스는 모델 데이터를 검색 하 고 브라우저에 대 한 응답을 반환 하는 템플릿 보기를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-113">**C** ontrollers: Classes that handle incoming browser requests, retrieve model data, and then specify view templates that return a response to the browser.</span></span>

<span data-ttu-id="de2ec-114">이 자습서 시리즈에서는 이러한 모든 개념을 다루는 수 하 고 응용 프로그램을 만들고 사용 하는 방법을 보여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-114">We'll be covering all these concepts in this tutorial series and show you how to use them to build an application.</span></span>

<span data-ttu-id="de2ec-115">컨트롤러 클래스를 만들어 시작 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-115">Let's begin by creating a controller class.</span></span> <span data-ttu-id="de2ec-116">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 *컨트롤러* 폴더를 선택 하 고 **컨트롤러 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-116">In **Solution Explorer**, right-click the *Controllers* folder and then select **Add Controller**.</span></span>

![](adding-a-controller/_static/image1.png)

<span data-ttu-id="de2ec-117">새 컨트롤러의 이름을 &quot;HelloWorldController&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-117">Name your new controller &quot;HelloWorldController&quot;.</span></span> <span data-ttu-id="de2ec-118">으로 기본 템플릿을 둡니다 **빈 MVC 컨트롤러** 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-118">Leave the default template as **Empty MVC controller** and click **Add**.</span></span>

![컨트롤러 추가](adding-a-controller/_static/image2.png)

<span data-ttu-id="de2ec-120">확인할 수 있습니다 **솔루션 탐색기** 새 파일을 이미 만들었다고 명명 *HelloWorldController.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-120">Notice in **Solution Explorer** that a new file has been created named *HelloWorldController.cs*.</span></span> <span data-ttu-id="de2ec-121">파일은 IDE에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-121">The file is open in the IDE.</span></span>

![](adding-a-controller/_static/image3.png)

<span data-ttu-id="de2ec-122">파일의 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-122">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

<span data-ttu-id="de2ec-123">컨트롤러 메서드는 예를 들어 html 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-123">The controller methods will return a string of HTML as an example.</span></span> <span data-ttu-id="de2ec-124">컨트롤러 이름은 `HelloWorldController` 위의 첫 번째 메서드는 이름이 `Index`합니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-124">The controller is named `HelloWorldController` and the first method above is named `Index`.</span></span> <span data-ttu-id="de2ec-125">브라우저에서 호출 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-125">Let's invoke it from a browser.</span></span> <span data-ttu-id="de2ec-126">(F5 또는 ctrl+f5를 누릅니다) 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-126">Run the application (press F5 or Ctrl+F5).</span></span> <span data-ttu-id="de2ec-127">브라우저에서 추가 &quot;HelloWorld&quot; 주소 표시줄의 경로에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-127">In the browser, append &quot;HelloWorld&quot; to the path in the address bar.</span></span> <span data-ttu-id="de2ec-128">(그림의 아래에서 예를 들어 `http://localhost:1234/HelloWorld.`) 페이지를 브라우저에서 다음 스크린샷과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-128">(For example, in the illustration below, it's `http://localhost:1234/HelloWorld.`) The page in the browser will look like the following screenshot.</span></span> <span data-ttu-id="de2ec-129">위의 메서드에 코드를 직접 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-129">In the method above, the code returned a string directly.</span></span> <span data-ttu-id="de2ec-130">일부 HTML을 반환 하도록 시스템을 지시 및 못해서!</span><span class="sxs-lookup"><span data-stu-id="de2ec-130">You told the system to just return some HTML, and it did!</span></span>

![](adding-a-controller/_static/image4.png)

<span data-ttu-id="de2ec-131">ASP.NET MVC는 들어오는 URL에 따라 다른 컨트롤러 클래스 (및 그 안에 다양 한 작업 메서드)를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-131">ASP.NET MVC invokes different controller classes (and different action methods within them) depending on the incoming URL.</span></span> <span data-ttu-id="de2ec-132">ASP.NET MVC에서 사용 되는 기본 URL 라우팅 논리를 호출 하는 코드를 확인 하려면 다음과 같은 형식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-132">The default URL routing logic used by ASP.NET MVC uses a format like this to determine what code to invoke:</span></span>

`/[Controller]/[ActionName]/[Parameters]`

<span data-ttu-id="de2ec-133">URL의 첫 번째 부분 실행할 컨트롤러 클래스를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-133">The first part of the URL determines the controller class to execute.</span></span> <span data-ttu-id="de2ec-134">따라서 */HelloWorld* 매핑되는 `HelloWorldController` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-134">So */HelloWorld* maps to the `HelloWorldController` class.</span></span> <span data-ttu-id="de2ec-135">URL의 두 번째 부분 클래스에 대 한 작업 메서드를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-135">The second part of the URL determines the action method on the class to execute.</span></span> <span data-ttu-id="de2ec-136">따라서 */HelloWorld/인덱스* 로 인해를 `Index` 메서드의 `HelloWorldController` 실행 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-136">So */HelloWorld/Index* would cause the `Index` method of the `HelloWorldController` class to execute.</span></span> <span data-ttu-id="de2ec-137">이동할 있었습니다 되었다는 */HelloWorld* 및 `Index` 메서드는 기본적으로 사용 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-137">Notice that we only had to browse to */HelloWorld* and the `Index` method was used by default.</span></span> <span data-ttu-id="de2ec-138">라는 메서드가 때문에 이것이 `Index` 명시적으로 지정 하지 않으면 컨트롤러에서 호출 되는 기본 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-138">This is because a method named `Index` is the default method that will be called on a controller if one is not explicitly specified.</span></span>

<span data-ttu-id="de2ec-139">`http://localhost:xxxx/HelloWorld/Welcome`으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-139">Browse to `http://localhost:xxxx/HelloWorld/Welcome`.</span></span> <span data-ttu-id="de2ec-140">합니다 `Welcome` 실행 하 고 문자열을 반환 &quot;이 시작 작업 메서드입니다... &quot;.</span><span class="sxs-lookup"><span data-stu-id="de2ec-140">The `Welcome` method runs and returns the string &quot;This is the Welcome action method...&quot;.</span></span> <span data-ttu-id="de2ec-141">기본 MVC 매핑이 `/[Controller]/[ActionName]/[Parameters]`합니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-141">The default MVC mapping is `/[Controller]/[ActionName]/[Parameters]`.</span></span> <span data-ttu-id="de2ec-142">이 URL의 경우 컨트롤러는 `HelloWorld`이고 `Welcome`은 작업 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-142">For this URL, the controller is `HelloWorld` and `Welcome` is the action method.</span></span> <span data-ttu-id="de2ec-143">아직 URL의 `[Parameters]` 부분을 사용하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-143">You haven't used the `[Parameters]` part of the URL yet.</span></span>

![](adding-a-controller/_static/image5.png)

<span data-ttu-id="de2ec-144">일부 매개 변수 정보를 URL에서 컨트롤러를 전달할 수 있도록 약간에서 예제를 보겠습니다 수정 (예를 들어 */HelloWorld/시작? name = Scott&amp;numtimes = 4*).</span><span class="sxs-lookup"><span data-stu-id="de2ec-144">Let's modify the example slightly so that you can pass some parameter information from the URL to the controller (for example, */HelloWorld/Welcome?name=Scott&amp;numtimes=4*).</span></span> <span data-ttu-id="de2ec-145">변경에 `Welcome` 아래와 같이 두 개의 매개 변수를 포함 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-145">Change your `Welcome` method to include two parameters as shown below.</span></span> <span data-ttu-id="de2ec-146">코드를 나타내는 C# 선택적 매개 변수 기능을 사용 하는 참고를 `numTimes` 매개 변수는 기본적으로 1 값이 없는 매개 변수에 대해 전달 되 면 합니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-146">Note that the code uses the C# optional-parameter feature to indicate that the `numTimes` parameter should default to 1 if no value is passed for that parameter.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample2.cs)]

<span data-ttu-id="de2ec-147">응용 프로그램을 실행 하 고 예제 URL로 이동 (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4)`합니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-147">Run your application and browse to the example URL (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4)`.</span></span> <span data-ttu-id="de2ec-148">다른 값을 사용할 수 있습니다 `name` 고 `numtimes` url에서입니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-148">You can try different values for `name` and `numtimes` in the URL.</span></span> <span data-ttu-id="de2ec-149">합니다 [ASP.NET MVC 모델 바인딩 시스템](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) 메서드에서 매개 변수로 주소 표시줄에는 쿼리 문자열에서 명명 된 매개 변수를 자동으로 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-149">The [ASP.NET MVC model binding system](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) automatically maps the named parameters from the query string in the address bar to parameters in your method.</span></span>

![](adding-a-controller/_static/image6.png)

<span data-ttu-id="de2ec-150">이러한 두 예제에서 컨트롤러 작업을 수행 합니다 &quot;VC&quot; MVC 부분-즉, 뷰 및 컨트롤러 작업.</span><span class="sxs-lookup"><span data-stu-id="de2ec-150">In both these examples the controller has been doing the &quot;VC&quot; portion of MVC — that is, the view and controller work.</span></span> <span data-ttu-id="de2ec-151">컨트롤러 HTML을 직접 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-151">The controller is returning HTML directly.</span></span> <span data-ttu-id="de2ec-152">일반적으로 컨트롤러 코드 번거로운 복잡해 지므로 HTML을 직접 반환 하지 않으려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-152">Ordinarily you don't want controllers returning HTML directly, since that becomes very cumbersome to code.</span></span> <span data-ttu-id="de2ec-153">대신 일반적으로 별도 뷰 템플릿 파일을 HTML 응답을 생성 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-153">Instead we'll typically use a separate view template file to help generate the HTML response.</span></span> <span data-ttu-id="de2ec-154">어떻게이 위해서는 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="de2ec-154">Let's look next at how we can do this.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="de2ec-155">[이전](intro-to-aspnet-mvc-4.md)
> [다음](adding-a-view.md)</span><span class="sxs-lookup"><span data-stu-id="de2ec-155">[Previous](intro-to-aspnet-mvc-4.md)
[Next](adding-a-view.md)</span></span>
