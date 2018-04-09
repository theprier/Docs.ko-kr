---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-controller
title: (VB) 컨트롤러 추가 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 즉를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 구축 하는 기초 설명...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2011
ms.topic: article
ms.assetid: 741259e1-54ac-4f71-b4e8-2bd5560bb950
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 9a433083c31c7929f7599e52800c887f301d7727
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="adding-a-controller-vb"></a><span data-ttu-id="8d939-103">(VB) 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="8d939-103">Adding a Controller (VB)</span></span>
====================
<span data-ttu-id="8d939-104">으로 [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="8d939-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="8d939-105">이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 즉 Microsoft Visual Studio의 무료 버전을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 구축 하는 기초 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-105">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="8d939-106">시작 하기 전에 아래에 나열 된 필수 구성 요소가 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-106">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="8d939-107">다음 링크를 클릭 하 여 모두를 설치할 수 있습니다: [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)합니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-107">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="8d939-108">또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-108">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="8d939-109">Visual Studio Web Developer Express SP1 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="8d939-109">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="8d939-110">ASP.NET MVC 3 도구 업데이트</span><span class="sxs-lookup"><span data-stu-id="8d939-110">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="8d939-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)</span><span class="sxs-lookup"><span data-stu-id="8d939-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="8d939-112">Visual Studio 2010 Visual Web Developer 2010 대신를 사용 하는 경우 다음 링크를 클릭 하 여 필수 구성 요소 설치: [Visual Studio 2010 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)합니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-112">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="8d939-113">이 항목에 수반 VB.NET 소스 코드를 사용 하 여 Visual Web Developer 프로젝트 ´ ù.</span><span class="sxs-lookup"><span data-stu-id="8d939-113">A Visual Web Developer project with VB.NET source code is available to accompany this topic.</span></span> <span data-ttu-id="8d939-114">[VB.NET 버전을 다운로드](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)합니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-114">[Download the VB.NET version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="8d939-115">원하는 경우 C#으로 전환 된 [C# 버전](../cs/adding-a-controller.md) 이 자습서의 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-115">If you prefer C#, switch to the [C# version](../cs/adding-a-controller.md) of this tutorial.</span></span>


<span data-ttu-id="8d939-116">MVC는 *모델-뷰-컨트롤러*합니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-116">MVC stands for *model-view-controller*.</span></span> <span data-ttu-id="8d939-117">MVC는 각 부분에 별도 책임 되도록 응용 프로그램을 개발 하기 위한 패턴:</span><span class="sxs-lookup"><span data-stu-id="8d939-117">MVC is a pattern for developing applications such that each part has a separate responsibility:</span></span>

- <span data-ttu-id="8d939-118">모델: 응용 프로그램에 대 한 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-118">Model: The data for your application.</span></span>
- <span data-ttu-id="8d939-119">보기: HTML 응답을 동적으로 생성 하 여 응용 프로그램에서 사용할 템플릿 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-119">Views: The template files your application will use to dynamically generate HTML responses.</span></span>
- <span data-ttu-id="8d939-120">컨트롤러의 경우: 응용 프로그램에서 들어오는 URL 요청을 처리 하는 클래스 모델 데이터를 검색 하 고 클라이언트에 대 한 응답을 렌더링 하는 템플릿 보기를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-120">Controllers: Classes that handle incoming URL requests to the application, retrieve model data, and then specify view templates that render a response to the client.</span></span>

<span data-ttu-id="8d939-121">이 자습서에서는 이러한 모든 개념을 다루는 수 알아보고 응용 프로그램을 만들고이 사용 하는 방법을 설명 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-121">We'll be covering all these concepts in this tutorial and show you how to use them to build an application.</span></span>

<span data-ttu-id="8d939-122">마우스 오른쪽 단추로 클릭 하 여 새 컨트롤러를 만들기는 *컨트롤러* 폴더에 **솔루션 탐색기** 다음를 선택 하 고 **컨트롤러 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-122">Create a new controller by right-clicking the *Controllers* folder in **Solution Explorer** and then selecting **Add Controller**.</span></span>

<span data-ttu-id="8d939-123">[![AddController](adding-a-controller/_static/image2.png "AddController")](adding-a-controller/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8d939-123">[![AddController](adding-a-controller/_static/image2.png "AddController")](adding-a-controller/_static/image1.png)</span></span>

<span data-ttu-id="8d939-124">새 컨트롤러 이름을 &quot;HelloWorldController&quot; 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-124">Name your new controller &quot;HelloWorldController&quot; and click **Add**.</span></span>

<span data-ttu-id="8d939-125">[![2AddEmptyController](adding-a-controller/_static/image4.png "2AddEmptyController")](adding-a-controller/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="8d939-125">[![2AddEmptyController](adding-a-controller/_static/image4.png "2AddEmptyController")](adding-a-controller/_static/image3.png)</span></span>

<span data-ttu-id="8d939-126">**솔루션 탐색기** 오른쪽의 명명 된 사용자에 대 한 새 파일이 만들어졌음을 *HelloWorldController.cs* 및 파일이 IDE에서 열려 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-126">Notice in **Solution Explorer** on the right that a new file has been created for you named *HelloWorldController.cs* and that the file is open in the IDE.</span></span>

<span data-ttu-id="8d939-127">새로운 내부 `public class HelloWorldController` 블록을 다음 코드 처럼 보이는 두 개의 새 메서드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-127">Inside the new `public class HelloWorldController` block, create two new methods that look like the following code.</span></span> <span data-ttu-id="8d939-128">예를 들어 컨트롤러에서 직접 html 문자열로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-128">We'll return a string of HTML directly from the controller as an example.</span></span>

[!code-vb[Main](adding-a-controller/samples/sample1.vb)]

<span data-ttu-id="8d939-129">컨트롤러 이름은 `HelloWorldController` 새로운 메서드가 즉 `Index`합니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-129">Your controller is named `HelloWorldController` and your new method is named `Index`.</span></span> <span data-ttu-id="8d939-130">(누름 F5 또는 Ctrl + F5) 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-130">Run the application (press F5 or Ctrl+F5).</span></span> <span data-ttu-id="8d939-131">브라우저 시작 된 후 추가 &quot;HelloWorld&quot; 주소 표시줄에 경로에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-131">Once your browser has started up, append &quot;HelloWorld&quot; to the path in the address bar.</span></span> <span data-ttu-id="8d939-132">(내 컴퓨터에 있기 `http://localhost:43246/HelloWorld`) 브라우저 아래 스크린샷과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-132">(On my computer, it's `http://localhost:43246/HelloWorld`) Your browser will look like the screenshot below.</span></span> <span data-ttu-id="8d939-133">위의 메서드 코드 문자열이 직접 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-133">In the method above, the code returned a string directly.</span></span> <span data-ttu-id="8d939-134">시스템에 반환할 일부 HTML를 말 하 고에서 수행한!</span><span class="sxs-lookup"><span data-stu-id="8d939-134">We told the system to just return some HTML, and it did!</span></span>

![](adding-a-controller/_static/image5.png)

<span data-ttu-id="8d939-135">ASP.NET MVC 들어오는 URL에 따라 다른 컨트롤러 클래스 (및 다른 작업 메서드 내에서)를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-135">ASP.NET MVC invokes different controller classes (and different action methods within them) depending on the incoming URL.</span></span> <span data-ttu-id="8d939-136">ASP.NET MVC에서 사용 하는 기본 매핑 논리 다음과 같은 형식을 사용 하 여 제어 어떤 코드가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-136">The default mapping logic used by ASP.NET MVC uses a format like this to control what code is invoked:</span></span>

`/[Controller]/[ActionName]/[Parameters]`

<span data-ttu-id="8d939-137">URL의 첫 번째 부분 컨트롤러 클래스를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-137">The first part of the URL determines the controller class to execute.</span></span> <span data-ttu-id="8d939-138">따라서 */HelloWorld* 매핑되는 `HelloWorldController` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-138">So */HelloWorld* maps to the `HelloWorldController` class.</span></span> <span data-ttu-id="8d939-139">URL의 두 번째 부분 클래스에 작업 메서드를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-139">The second part of the URL determines the action method on the class to execute.</span></span> <span data-ttu-id="8d939-140">따라서 */HelloWorld/인덱스* 으 리라 예상는 `Index` 의 메서드는 `HelloWorldController` 실행 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-140">So */HelloWorld/Index* would cause the `Index` method of the `HelloWorldController` class to execute.</span></span> <span data-ttu-id="8d939-141">방문 했습니다 사라졌는지 */HelloWorld* 위에 및 `Index` 기본적으로 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-141">Notice that we only had to visit */HelloWorld* above and the `Index` method was used by default.</span></span> <span data-ttu-id="8d939-142">라는 메서드가 때문에 이것이 `Index` 은 명시적으로 지정 되지 않은 경우 컨트롤러에서 호출 되는 기본 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-142">This is because a method named `Index` is the default method that will be called on a controller if one is not explicitly specified.</span></span>

<span data-ttu-id="8d939-143">`http://localhost:xxxx/HelloWorld/Welcome`으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-143">Browse to `http://localhost:xxxx/HelloWorld/Welcome`.</span></span> <span data-ttu-id="8d939-144">`Welcome` 메서드가 실행 되 고 문자열을 반환 &quot;이 시작 작업 방법... &quot;.</span><span class="sxs-lookup"><span data-stu-id="8d939-144">The `Welcome` method runs and returns the string &quot;This is the Welcome action method...&quot;.</span></span> <span data-ttu-id="8d939-145">기본 MVC 매핑이 `/[Controller]/[ActionName]/[Parameters]`합니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-145">The default MVC mapping is `/[Controller]/[ActionName]/[Parameters]`.</span></span> <span data-ttu-id="8d939-146">이 URL에 대 한 컨트롤러는 `HelloWorld` 및 `Welcome` 는 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-146">For this URL, the controller is `HelloWorld` and `Welcome` is the method.</span></span> <span data-ttu-id="8d939-147">사용 하지 않은 `[Parameters]` 아직 URL의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-147">We haven't used the `[Parameters]` part of the URL yet.</span></span>

![](adding-a-controller/_static/image6.png)

<span data-ttu-id="8d939-148">수정 해 보겠습니다 예제에서는 약간의 일부 매개 변수 정보 URL에서 컨트롤러에 전달할 수 있도록 (예를 들어 */HelloWorld/시작? name = Scott&amp;numtimes = 4*).</span><span class="sxs-lookup"><span data-stu-id="8d939-148">Let's modify the example slightly so that we can pass some parameter information in from the URL to the controller (for example, */HelloWorld/Welcome?name=Scott&amp;numtimes=4*).</span></span> <span data-ttu-id="8d939-149">변경 하면 `Welcome` 메서드를 다음과 같이 두 개의 매개 변수를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-149">Change your `Welcome` method to include two parameters as shown below.</span></span> <span data-ttu-id="8d939-150">임을 나타내는 VB 선택적 매개 변수 기능을 사용 했습니다 있는지 참고는 `numTimes` 경우 해당 매개 변수에 대해 값은 1의 매개 변수 기본값은입니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-150">Note that we've used the VB optional parameter feature to indicate that the `numTimes` parameter should default to 1 if no value is passed for that parameter.</span></span>

[!code-vb[Main](adding-a-controller/samples/sample2.vb)]

<span data-ttu-id="8d939-151">ְ ְ ¿כ를 찾아 `http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4` **합니다.**</span><span class="sxs-lookup"><span data-stu-id="8d939-151">Run your application and browse to `http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4`**.**</span></span> <span data-ttu-id="8d939-152">에 대해 다른 값을 연습할 수 `name` 및 `numtimes`합니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-152">You can try different values for `name` and `numtimes`.</span></span> <span data-ttu-id="8d939-153">시스템은 메서드의 매개 변수를 쿼리 문자열의 주소 표시줄에서 명명 된 매개 변수를 자동으로 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-153">The system automatically maps the named parameters from your query string in the address bar to parameters in your method.</span></span>

![](adding-a-controller/_static/image7.png)

<span data-ttu-id="8d939-154">이러한 예제 모두에 컨트롤러에 작업을 하 고 MVC의 VC 부분 — 뷰와 컨트롤러 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-154">In both these examples the controller has been doing the VC portion of MVC — that is the view and controller work.</span></span> <span data-ttu-id="8d939-155">컨트롤러 HTML을 직접 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-155">The controller is returning HTML directly.</span></span> <span data-ttu-id="8d939-156">일반적으로 코드에 번거로운 되므로 HTML을 직접 반환 하는 컨트롤러 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-156">Ordinarily we don't want controllers returning HTML directly, since that becomes very cumbersome to code.</span></span> <span data-ttu-id="8d939-157">대신 일반적으로에서는 별도 뷰를 서식 파일을 HTML 응답을 생성할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-157">Instead we'll typically use a separate view template file to help generate the HTML response.</span></span> <span data-ttu-id="8d939-158">어떻게 이렇게 하려면 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8d939-158">Let's look at how we can do this.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8d939-159">[이전](intro-to-aspnet-mvc-3.md)
> [다음](adding-a-view.md)</span><span class="sxs-lookup"><span data-stu-id="8d939-159">[Previous](intro-to-aspnet-mvc-3.md)
[Next](adding-a-view.md)</span></span>
