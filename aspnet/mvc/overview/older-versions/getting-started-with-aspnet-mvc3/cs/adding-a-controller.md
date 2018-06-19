---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-controller
title: 컨트롤러 (C#) 추가 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 어떤 i를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 구축 하는 기초 설명...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2011
ms.topic: article
ms.assetid: 0b8c56b5-fdf3-42dd-a866-98fbe0ab78a0
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 963d3bbbadf408d7045c50bfd693069e4097d45d
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30868297"
---
<a name="adding-a-controller-c"></a><span data-ttu-id="843ac-103">컨트롤러 (C#)에 추가</span><span class="sxs-lookup"><span data-stu-id="843ac-103">Adding a Controller (C#)</span></span>
====================
<span data-ttu-id="843ac-104">으로 [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="843ac-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> > [!NOTE]
> > <span data-ttu-id="843ac-105">이 자습서의 업데이트 된 버전은 사용할 수 있는 [여기](../../../getting-started/introduction/getting-started.md) ASP.NET MVC 5 및 Visual Studio 2013을 사용 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-105">An updated version of this tutorial is available [here](../../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="843ac-106">더 안전 하 고 따라 하기 쉽고 이며 더 많은 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-106">It's more secure, much simpler to follow and demonstrates more features.</span></span>
> 
> 
> <span data-ttu-id="843ac-107">이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 즉 Microsoft Visual Studio의 무료 버전을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 구축 하는 기초 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-107">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="843ac-108">시작 하기 전에 아래에 나열 된 필수 구성 요소가 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-108">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="843ac-109">다음 링크를 클릭 하 여 모두를 설치할 수 있습니다: [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)합니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-109">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="843ac-110">또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-110">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="843ac-111">Visual Studio Web Developer Express SP1 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="843ac-111">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="843ac-112">ASP.NET MVC 3 도구 업데이트</span><span class="sxs-lookup"><span data-stu-id="843ac-112">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="843ac-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)</span><span class="sxs-lookup"><span data-stu-id="843ac-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="843ac-114">Visual Studio 2010 Visual Web Developer 2010 대신를 사용 하는 경우 다음 링크를 클릭 하 여 필수 구성 요소 설치: [Visual Studio 2010 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)합니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-114">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="843ac-115">이 항목에 수반 C# 소스 코드를 사용 하 여 Visual Web Developer 프로젝트 ´ ù.</span><span class="sxs-lookup"><span data-stu-id="843ac-115">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="843ac-116">[C# 버전을 다운로드](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)합니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-116">[Download the C# version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="843ac-117">Visual Basic을 선호 하는 경우 전환의 [Visual Basic 버전](../vb/intro-to-aspnet-mvc-3.md) 이 자습서의 합니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-117">If you prefer Visual Basic, switch to the [Visual Basic version](../vb/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>


<span data-ttu-id="843ac-118">MVC는 *모델-뷰-컨트롤러*합니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-118">MVC stands for *model-view-controller*.</span></span> <span data-ttu-id="843ac-119">MVC는 잘 설계 하 고 유지 관리 하기 쉬운 되는 응용 프로그램을 개발 하기 위한 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-119">MVC is a pattern for developing applications that are well architected and easy to maintain.</span></span> <span data-ttu-id="843ac-120">MVC 기반 응용 프로그램에는 다음이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-120">MVC-based applications contain:</span></span>

- <span data-ttu-id="843ac-121">컨트롤러의 경우: 응용 프로그램에서 들어오는 요청을 처리 하는 클래스 모델 데이터를 검색 하 고 클라이언트에 대 한 응답을 반환 하는 템플릿 보기를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-121">Controllers: Classes that handle incoming requests to the application, retrieve model data, and then specify view templates that return a response to the client.</span></span>
- <span data-ttu-id="843ac-122">모델: 유효성 검사 논리를 사용 하 여 해당 데이터에 대 한 비즈니스 규칙을 적용 하 고 응용 프로그램의 데이터를 나타내는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-122">Models: Classes that represent the data of the application and that use validation logic to enforce business rules for that data.</span></span>
- <span data-ttu-id="843ac-123">응용 프로그램 HTML 응답을 동적으로 생성을 사용 하 여 보기: 템플릿 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-123">Views: Template files that your application uses to dynamically generate HTML responses.</span></span>

<span data-ttu-id="843ac-124">이 자습서 시리즈의 이러한 모든 개념을 다루는 수 알아보고 응용 프로그램을 만들고이 사용 하는 방법을 설명 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-124">We'll be covering all these concepts in this tutorial series and show you how to use them to build an application.</span></span>

<span data-ttu-id="843ac-125">컨트롤러 클래스를 만들어 시작 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-125">Let's begin by creating a controller class.</span></span> <span data-ttu-id="843ac-126">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 *컨트롤러* 폴더 및 다음 선택 **컨트롤러 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-126">In **Solution Explorer**, right-click the *Controllers* folder and then select **Add Controller**.</span></span>

[![](adding-a-controller/_static/image2.png)](adding-a-controller/_static/image1.png)

<span data-ttu-id="843ac-127">새 컨트롤러 "HelloWorldController" 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-127">Name your new controller "HelloWorldController".</span></span> <span data-ttu-id="843ac-128">기본 템플릿을으로 둡니다 **빈 컨트롤러** 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-128">Leave the default template as **Empty controller** and click **Add**.</span></span>

<span data-ttu-id="843ac-129">[![AddHelloWorldController](adding-a-controller/_static/image4.png)](adding-a-controller/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="843ac-129">[![AddHelloWorldController](adding-a-controller/_static/image4.png)](adding-a-controller/_static/image3.png)</span></span>

<span data-ttu-id="843ac-130">**솔루션 탐색기** 새 파일이 만들어졌음을 명명 *HelloWorldController.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-130">Notice in **Solution Explorer** that a new file has been created named *HelloWorldController.cs*.</span></span> <span data-ttu-id="843ac-131">IDE에서 열려 있는 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-131">The file is open in the IDE.</span></span>

![](adding-a-controller/_static/image5.png)

<span data-ttu-id="843ac-132">내에서 `public class HelloWorldController` 블록을 다음 코드 처럼 보이는 두 메서드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-132">Inside the `public class HelloWorldController` block, create two methods that look like the following code.</span></span> <span data-ttu-id="843ac-133">예를 들어 컨트롤러 html 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-133">The controller will return a string of HTML as an example.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

<span data-ttu-id="843ac-134">컨트롤러 이름은 `HelloWorldController` 고 위의 첫 번째 방법은 이름이 `Index`합니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-134">Your controller is named `HelloWorldController` and the first method above is named `Index`.</span></span> <span data-ttu-id="843ac-135">브라우저에서 호출 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-135">Let's invoke it from a browser.</span></span> <span data-ttu-id="843ac-136">(누름 F5 또는 Ctrl + F5) 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-136">Run the application (press F5 or Ctrl+F5).</span></span> <span data-ttu-id="843ac-137">브라우저에서 주소 표시줄에 경로에 "HelloWorld"를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-137">In the browser, append "HelloWorld" to the path in the address bar.</span></span> <span data-ttu-id="843ac-138">(의 아래 그림의 예를 들어 `http://localhost:43246/HelloWorld.`) 브라우저에서 페이지는 다음 스크린샷과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-138">(For example, in the illustration below, it's `http://localhost:43246/HelloWorld.`) The page in the browser will look like the following screenshot.</span></span> <span data-ttu-id="843ac-139">위의 메서드 코드 문자열이 직접 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-139">In the method above, the code returned a string directly.</span></span> <span data-ttu-id="843ac-140">일부 HTML 반환할을 시스템에서 설정한 다시!</span><span class="sxs-lookup"><span data-stu-id="843ac-140">You told the system to just return some HTML, and it did!</span></span>

![](adding-a-controller/_static/image6.png)

<span data-ttu-id="843ac-141">ASP.NET MVC 들어오는 URL에 따라 다른 컨트롤러 클래스 (및 다른 작업 메서드 내에서)를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-141">ASP.NET MVC invokes different controller classes (and different action methods within them) depending on the incoming URL.</span></span> <span data-ttu-id="843ac-142">호출 하는 코드를 확인 하려면 다음과 같은 형식을 사용 하는 ASP.NET MVC에서 사용 하는 기본 매핑 논리:</span><span class="sxs-lookup"><span data-stu-id="843ac-142">The default mapping logic used by ASP.NET MVC uses a format like this to determine what code to invoke:</span></span>

`/[Controller]/[ActionName]/[Parameters]`

<span data-ttu-id="843ac-143">URL의 첫 번째 부분 컨트롤러 클래스를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-143">The first part of the URL determines the controller class to execute.</span></span> <span data-ttu-id="843ac-144">따라서 */HelloWorld* 매핑되는 `HelloWorldController` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-144">So */HelloWorld* maps to the `HelloWorldController` class.</span></span> <span data-ttu-id="843ac-145">URL의 두 번째 부분 클래스에 작업 메서드를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-145">The second part of the URL determines the action method on the class to execute.</span></span> <span data-ttu-id="843ac-146">따라서 */HelloWorld/인덱스* 으 리라 예상는 `Index` 의 메서드는 `HelloWorldController` 실행 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-146">So */HelloWorld/Index* would cause the `Index` method of the `HelloWorldController` class to execute.</span></span> <span data-ttu-id="843ac-147">로 이동 했습니다 사라졌는지 */HelloWorld* 및 `Index` 기본적으로 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-147">Notice that we only had to browse to */HelloWorld* and the `Index` method was used by default.</span></span> <span data-ttu-id="843ac-148">라는 메서드가 때문에 이것이 `Index` 은 명시적으로 지정 되지 않은 경우 컨트롤러에서 호출 되는 기본 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-148">This is because a method named `Index` is the default method that will be called on a controller if one is not explicitly specified.</span></span>

<span data-ttu-id="843ac-149">`http://localhost:xxxx/HelloWorld/Welcome`으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-149">Browse to `http://localhost:xxxx/HelloWorld/Welcome`.</span></span> <span data-ttu-id="843ac-150">`Welcome` 메서드는 "시작 작업 메서드입니다..."라는 문자열을 실행하고 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-150">The `Welcome` method runs and returns the string "This is the Welcome action method...".</span></span> <span data-ttu-id="843ac-151">기본 MVC 매핑이 `/[Controller]/[ActionName]/[Parameters]`합니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-151">The default MVC mapping is `/[Controller]/[ActionName]/[Parameters]`.</span></span> <span data-ttu-id="843ac-152">이 URL의 경우 컨트롤러는 `HelloWorld`이고 `Welcome`은 작업 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-152">For this URL, the controller is `HelloWorld` and `Welcome` is the action method.</span></span> <span data-ttu-id="843ac-153">아직 URL의 `[Parameters]` 부분을 사용하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-153">You haven't used the `[Parameters]` part of the URL yet.</span></span>

![](adding-a-controller/_static/image7.png)

<span data-ttu-id="843ac-154">수정 해 보겠습니다 예제 약간를 컨트롤러에 URL에서 일부 매개 변수 정보를 전달할 수 있습니다 (예를 들어 */HelloWorld/시작? name = Scott&amp;numtimes = 4*).</span><span class="sxs-lookup"><span data-stu-id="843ac-154">Let's modify the example slightly so that you can pass some parameter information from the URL to the controller (for example, */HelloWorld/Welcome?name=Scott&amp;numtimes=4*).</span></span> <span data-ttu-id="843ac-155">변경 하면 `Welcome` 메서드를 다음과 같이 두 개의 매개 변수를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-155">Change your `Welcome` method to include two parameters as shown below.</span></span> <span data-ttu-id="843ac-156">코드는 C# 기능 선택적 매개 변수를 사용 하 여 임을 나타내는 참고는 `numTimes` 경우 해당 매개 변수에 대해 값은 1의 매개 변수 기본값은입니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-156">Note that the code uses the C# optional-parameter feature to indicate that the `numTimes` parameter should default to 1 if no value is passed for that parameter.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample2.cs)]

<span data-ttu-id="843ac-157">ְ ְ ¿כ 예제 URL로 이동 (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4)`합니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-157">Run your application and browse to the example URL (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4)`.</span></span> <span data-ttu-id="843ac-158">에 대해 다른 값을 시도할 수 `name` 및 `numtimes` url에서입니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-158">You can try different values for `name` and `numtimes` in the URL.</span></span> <span data-ttu-id="843ac-159">시스템은 메서드의 매개 변수에 주소 표시줄에는 쿼리 문자열에서 명명 된 매개 변수를 자동으로 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-159">The system automatically maps the named parameters from the query string in the address bar to parameters in your method.</span></span>

![](adding-a-controller/_static/image8.png)

<span data-ttu-id="843ac-160">두이 예제에서 컨트롤러는 작업을 하 고 "VC" 부분의 MVC-즉, 뷰 및 컨트롤러 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-160">In both these examples the controller has been doing the "VC" portion of MVC — that is, the view and controller work.</span></span> <span data-ttu-id="843ac-161">컨트롤러 HTML을 직접 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-161">The controller is returning HTML directly.</span></span> <span data-ttu-id="843ac-162">일반적으로 코드에 번거로운 되므로 HTML을 직접 반환 하는 컨트롤러 않으려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-162">Ordinarily you don't want controllers returning HTML directly, since that becomes very cumbersome to code.</span></span> <span data-ttu-id="843ac-163">대신 일반적으로에서는 별도 뷰를 서식 파일을 HTML 응답을 생성할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-163">Instead we'll typically use a separate view template file to help generate the HTML response.</span></span> <span data-ttu-id="843ac-164">다음 방법을 수행 수에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="843ac-164">Let's look next at how we can do this.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="843ac-165">[이전](intro-to-aspnet-mvc-3.md)
> [다음](adding-a-view.md)</span><span class="sxs-lookup"><span data-stu-id="843ac-165">[Previous](intro-to-aspnet-mvc-3.md)
[Next](adding-a-view.md)</span></span>
