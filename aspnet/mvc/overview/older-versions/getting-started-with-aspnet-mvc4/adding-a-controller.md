---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-controller
title: 컨트롤러 추가 | Microsoft Docs
author: Rick-Anderson
description: 참고:이 자습서의 업데이트 된 버전은 ASP.NET MVC 5 및 Visual Studio 2013을 사용 하는 있습니다. 것이 더 안전 하 고 진행할 데모를 단순...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/28/2012
ms.topic: article
ms.assetid: 0267d31c-892f-49a1-9e7a-3ae8cc12b2ca
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: bb76c0a87d935322406b9d8e18fbdb3e41f327f5
ms.sourcegitcommit: 6784510cfb589308c3875ccb5113eb31031766b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2018
ms.locfileid: "30868869"
---
<a name="adding-a-controller"></a><span data-ttu-id="50fb9-104">컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="50fb9-104">Adding a Controller</span></span>
====================
<span data-ttu-id="50fb9-105">으로 [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="50fb9-105">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> > [!NOTE]
> > <span data-ttu-id="50fb9-106">이 자습서의 업데이트 된 버전은 사용할 수 있는 [여기](../../getting-started/introduction/getting-started.md) ASP.NET MVC 5 및 Visual Studio 2013을 사용 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="50fb9-107">더 안전 하 고 따라 하기 쉽고 이며 더 많은 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>


<span data-ttu-id="50fb9-108">MVC는 *모델-뷰-컨트롤러*합니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-108">MVC stands for *model-view-controller*.</span></span> <span data-ttu-id="50fb9-109">MVC는은 잘 설계, 테스트 및 유지 관리 하기 쉬운 응용 프로그램을 개발 하기 위한 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-109">MVC is a pattern for developing applications that are well architected, testable and easy to maintain.</span></span> <span data-ttu-id="50fb9-110">MVC 기반 응용 프로그램에는 다음이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-110">MVC-based applications contain:</span></span>

- <span data-ttu-id="50fb9-111">**M** odels: 유효성 검사 논리를 사용 하 여 해당 데이터에 대 한 비즈니스 규칙을 적용 하 고 응용 프로그램의 데이터를 나타내는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-111">**M** odels: Classes that represent the data of the application and that use validation logic to enforce business rules for that data.</span></span>
- <span data-ttu-id="50fb9-112">**V** iews: 응용 프로그램 사용 HTML 응답을 동적으로 생성 하는 템플릿 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-112">**V** iews: Template files that your application uses to dynamically generate HTML responses.</span></span>
- <span data-ttu-id="50fb9-113">**C** ontrollers: 들어오는 브라우저 요청을 처리 하는 클래스 모델 데이터를 검색 한 다음 브라우저에 대 한 응답을 반환 하는 템플릿 보기를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-113">**C** ontrollers: Classes that handle incoming browser requests, retrieve model data, and then specify view templates that return a response to the browser.</span></span>

<span data-ttu-id="50fb9-114">이 자습서 시리즈의 이러한 모든 개념을 다루는 수 알아보고 응용 프로그램을 만들고이 사용 하는 방법을 설명 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-114">We'll be covering all these concepts in this tutorial series and show you how to use them to build an application.</span></span>

<span data-ttu-id="50fb9-115">컨트롤러 클래스를 만들어 시작 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-115">Let's begin by creating a controller class.</span></span> <span data-ttu-id="50fb9-116">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 *컨트롤러* 폴더 및 다음 선택 **컨트롤러 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-116">In **Solution Explorer**, right-click the *Controllers* folder and then select **Add Controller**.</span></span>

![](adding-a-controller/_static/image1.png)

<span data-ttu-id="50fb9-117">새 컨트롤러 이름을 &quot;HelloWorldController&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-117">Name your new controller &quot;HelloWorldController&quot;.</span></span> <span data-ttu-id="50fb9-118">기본 템플릿을으로 둡니다 **빈 MVC 컨트롤러** 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-118">Leave the default template as **Empty MVC controller** and click **Add**.</span></span>

![컨트롤러 추가](adding-a-controller/_static/image2.png)

<span data-ttu-id="50fb9-120">**솔루션 탐색기** 새 파일이 만들어졌음을 명명 *HelloWorldController.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-120">Notice in **Solution Explorer** that a new file has been created named *HelloWorldController.cs*.</span></span> <span data-ttu-id="50fb9-121">IDE에서 열려 있는 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-121">The file is open in the IDE.</span></span>

![](adding-a-controller/_static/image3.png)

<span data-ttu-id="50fb9-122">파일의 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-122">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

<span data-ttu-id="50fb9-123">예를 들어 컨트롤러 메서드에 html 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-123">The controller methods will return a string of HTML as an example.</span></span> <span data-ttu-id="50fb9-124">컨트롤러 이름은 `HelloWorldController` 고 위의 첫 번째 방법은 이름이 `Index`합니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-124">The controller is named `HelloWorldController` and the first method above is named `Index`.</span></span> <span data-ttu-id="50fb9-125">브라우저에서 호출 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-125">Let's invoke it from a browser.</span></span> <span data-ttu-id="50fb9-126">(누름 F5 또는 Ctrl + F5) 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-126">Run the application (press F5 or Ctrl+F5).</span></span> <span data-ttu-id="50fb9-127">브라우저에서 추가 &quot;HelloWorld&quot; 주소 표시줄에 경로에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-127">In the browser, append &quot;HelloWorld&quot; to the path in the address bar.</span></span> <span data-ttu-id="50fb9-128">(의 아래 그림의 예를 들어 `http://localhost:1234/HelloWorld.`) 브라우저에서 페이지는 다음 스크린샷과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-128">(For example, in the illustration below, it's `http://localhost:1234/HelloWorld.`) The page in the browser will look like the following screenshot.</span></span> <span data-ttu-id="50fb9-129">위의 메서드 코드 문자열이 직접 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-129">In the method above, the code returned a string directly.</span></span> <span data-ttu-id="50fb9-130">일부 HTML 반환할을 시스템에서 설정한 다시!</span><span class="sxs-lookup"><span data-stu-id="50fb9-130">You told the system to just return some HTML, and it did!</span></span>

![](adding-a-controller/_static/image4.png)

<span data-ttu-id="50fb9-131">ASP.NET MVC 들어오는 URL에 따라 다른 컨트롤러 클래스 (및 다른 작업 메서드 내에서)를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-131">ASP.NET MVC invokes different controller classes (and different action methods within them) depending on the incoming URL.</span></span> <span data-ttu-id="50fb9-132">ASP.NET MVC에서 사용 하는 기본 URL 라우팅 논리를 호출 하는 코드를 확인 하려면 다음과 같은 형식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-132">The default URL routing logic used by ASP.NET MVC uses a format like this to determine what code to invoke:</span></span>

`/[Controller]/[ActionName]/[Parameters]`

<span data-ttu-id="50fb9-133">URL의 첫 번째 부분 컨트롤러 클래스를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-133">The first part of the URL determines the controller class to execute.</span></span> <span data-ttu-id="50fb9-134">따라서 */HelloWorld* 매핑되는 `HelloWorldController` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-134">So */HelloWorld* maps to the `HelloWorldController` class.</span></span> <span data-ttu-id="50fb9-135">URL의 두 번째 부분 클래스에 작업 메서드를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-135">The second part of the URL determines the action method on the class to execute.</span></span> <span data-ttu-id="50fb9-136">따라서 */HelloWorld/인덱스* 으 리라 예상는 `Index` 의 메서드는 `HelloWorldController` 실행 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-136">So */HelloWorld/Index* would cause the `Index` method of the `HelloWorldController` class to execute.</span></span> <span data-ttu-id="50fb9-137">로 이동 했습니다 사라졌는지 */HelloWorld* 및 `Index` 기본적으로 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-137">Notice that we only had to browse to */HelloWorld* and the `Index` method was used by default.</span></span> <span data-ttu-id="50fb9-138">라는 메서드가 때문에 이것이 `Index` 은 명시적으로 지정 되지 않은 경우 컨트롤러에서 호출 되는 기본 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-138">This is because a method named `Index` is the default method that will be called on a controller if one is not explicitly specified.</span></span>

<span data-ttu-id="50fb9-139">`http://localhost:xxxx/HelloWorld/Welcome`으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-139">Browse to `http://localhost:xxxx/HelloWorld/Welcome`.</span></span> <span data-ttu-id="50fb9-140">`Welcome` 메서드가 실행 되 고 문자열을 반환 &quot;이 시작 작업 방법... &quot;.</span><span class="sxs-lookup"><span data-stu-id="50fb9-140">The `Welcome` method runs and returns the string &quot;This is the Welcome action method...&quot;.</span></span> <span data-ttu-id="50fb9-141">기본 MVC 매핑이 `/[Controller]/[ActionName]/[Parameters]`합니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-141">The default MVC mapping is `/[Controller]/[ActionName]/[Parameters]`.</span></span> <span data-ttu-id="50fb9-142">이 URL의 경우 컨트롤러는 `HelloWorld`이고 `Welcome`은 작업 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-142">For this URL, the controller is `HelloWorld` and `Welcome` is the action method.</span></span> <span data-ttu-id="50fb9-143">아직 URL의 `[Parameters]` 부분을 사용하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-143">You haven't used the `[Parameters]` part of the URL yet.</span></span>

![](adding-a-controller/_static/image5.png)

<span data-ttu-id="50fb9-144">수정 해 보겠습니다 예제 약간를 컨트롤러에 URL에서 일부 매개 변수 정보를 전달할 수 있습니다 (예를 들어 */HelloWorld/시작? name = Scott&amp;numtimes = 4*).</span><span class="sxs-lookup"><span data-stu-id="50fb9-144">Let's modify the example slightly so that you can pass some parameter information from the URL to the controller (for example, */HelloWorld/Welcome?name=Scott&amp;numtimes=4*).</span></span> <span data-ttu-id="50fb9-145">변경 하면 `Welcome` 메서드를 다음과 같이 두 개의 매개 변수를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-145">Change your `Welcome` method to include two parameters as shown below.</span></span> <span data-ttu-id="50fb9-146">코드는 C# 기능 선택적 매개 변수를 사용 하 여 임을 나타내는 참고는 `numTimes` 경우 해당 매개 변수에 대해 값은 1의 매개 변수 기본값은입니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-146">Note that the code uses the C# optional-parameter feature to indicate that the `numTimes` parameter should default to 1 if no value is passed for that parameter.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample2.cs)]

<span data-ttu-id="50fb9-147">ְ ְ ¿כ 예제 URL로 이동 (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4)`합니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-147">Run your application and browse to the example URL (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4)`.</span></span> <span data-ttu-id="50fb9-148">에 대해 다른 값을 시도할 수 `name` 및 `numtimes` url에서입니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-148">You can try different values for `name` and `numtimes` in the URL.</span></span> <span data-ttu-id="50fb9-149">[ASP.NET MVC 모델 바인딩 시스템이](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) 메서드의 매개 변수에 주소 표시줄에는 쿼리 문자열에서 명명 된 매개 변수를 자동으로 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-149">The [ASP.NET MVC model binding system](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) automatically maps the named parameters from the query string in the address bar to parameters in your method.</span></span>

![](adding-a-controller/_static/image6.png)

<span data-ttu-id="50fb9-150">이러한 예제 모두에 컨트롤러에 작업을 하 고는 &quot;VC&quot; MVC의 부분 — 뷰와 컨트롤러 작업 즉, 합니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-150">In both these examples the controller has been doing the &quot;VC&quot; portion of MVC — that is, the view and controller work.</span></span> <span data-ttu-id="50fb9-151">컨트롤러 HTML을 직접 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-151">The controller is returning HTML directly.</span></span> <span data-ttu-id="50fb9-152">일반적으로 코드에 번거로운 되므로 HTML을 직접 반환 하는 컨트롤러 않으려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-152">Ordinarily you don't want controllers returning HTML directly, since that becomes very cumbersome to code.</span></span> <span data-ttu-id="50fb9-153">대신 일반적으로에서는 별도 뷰를 서식 파일을 HTML 응답을 생성할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-153">Instead we'll typically use a separate view template file to help generate the HTML response.</span></span> <span data-ttu-id="50fb9-154">다음 방법을 수행 수에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="50fb9-154">Let's look next at how we can do this.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="50fb9-155">[이전](intro-to-aspnet-mvc-4.md)
> [다음](adding-a-view.md)</span><span class="sxs-lookup"><span data-stu-id="50fb9-155">[Previous](intro-to-aspnet-mvc-4.md)
[Next](adding-a-view.md)</span></span>
