---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part2
title: 컨트롤러 추가 | Microsoft Docs
author: shanselman
description: 이 자습서는 여기 Visual Studio 2013을 사용 하 여 사용할 경우 업데이트 된 버전입니다. 새 자습서 t를 통해 많은 향상 된 기능을 제공 하는 ASP.NET MVC 5를 사용 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/14/2010
ms.topic: article
ms.assetid: ff03dcc0-da97-458d-838f-0823e7482642
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part2
msc.type: authoredcontent
ms.openlocfilehash: f20889cf1c1cd9a2a69f0008d879b518c38334d6
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37395671"
---
<a name="adding-a-controller"></a><span data-ttu-id="447f4-104">컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="447f4-104">Adding a Controller</span></span>
====================
<span data-ttu-id="447f4-105">[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="447f4-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> > [!NOTE]
> > <span data-ttu-id="447f4-106">이 자습서는 사용할 수 있는 경우 업데이트 된 버전 [같습니다](../../getting-started/introduction/getting-started.md) 사용 하 여 [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)합니다.</span><span class="sxs-lookup"><span data-stu-id="447f4-106">An updated version if this tutorial is available [here](../../getting-started/introduction/getting-started.md) using [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads).</span></span> <span data-ttu-id="447f4-107">새 자습서에는이 자습서를 통해 많은 향상 된 기능을 제공 하는 ASP.NET MVC 5를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="447f4-107">The new tutorial uses ASP.NET MVC 5, which provides many improvements over this tutorial.</span></span>
> 
> 
> <span data-ttu-id="447f4-108">ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="447f4-108">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="447f4-109">읽기 및 쓰기 데이터베이스는 간단한 웹 응용 프로그램을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="447f4-109">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="447f4-110">방문 합니다 [ASP.NET MVC 학습 센터](../../../index.md) 자습서 및 샘플 다른 ASP.NET MVC를 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="447f4-110">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>


<span data-ttu-id="447f4-111">MVC는 모델, 뷰, 컨트롤러를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="447f4-111">MVC stands for Model, View, Controller.</span></span> <span data-ttu-id="447f4-112">MVC에는 각 파트에는 서로 다른 책임을 응용 프로그램을 개발 하기 위한 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="447f4-112">MVC is a pattern for developing applications such that each part has a responsibility that is different from another.</span></span>

- <span data-ttu-id="447f4-113">데이터 응용 프로그램의 모델:</span><span class="sxs-lookup"><span data-stu-id="447f4-113">Model: The data of your application</span></span>
- <span data-ttu-id="447f4-114">보기: 동적으로 HTML 응답을 생성 하려면 응용 프로그램에서 사용할 템플릿 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="447f4-114">Views: The template files your application will use to dynamically generate HTML responses.</span></span>
- <span data-ttu-id="447f4-115">컨트롤러: 응용 프로그램에 들어오는 URL 요청을 처리 하는 클래스 모델 데이터를 검색 하 고 클라이언트에 다시 응답을 렌더링 하는 뷰 템플릿을 지정합니다</span><span class="sxs-lookup"><span data-stu-id="447f4-115">Controllers: Classes that handle incoming URL requests to the application, retrieve model data, and then specify view templates that render a response back to the client</span></span>

<span data-ttu-id="447f4-116">이 자습서에서 이러한 모든 개념을 다루는 수 하 고 응용 프로그램을 만들고 사용 하는 방법을 보여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="447f4-116">We'll be covering all these concepts in this tutorial and show you how to use them to build an application.</span></span>

<span data-ttu-id="447f4-117">솔루션 탐색기에서에서 컨트롤러 폴더를 마우스 오른쪽 단추로 클릭 하 고 컨트롤러 추가 선택 하 여 새 컨트롤러를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="447f4-117">Let's create a new controller by right-clicking the controllers folder in the solution Explorer and selecting Add Controller.</span></span>

<span data-ttu-id="447f4-118">[![AddControllerRightClick](getting-started-with-mvc-part2/_static/image2.png)](getting-started-with-mvc-part2/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="447f4-118">[![AddControllerRightClick](getting-started-with-mvc-part2/_static/image2.png)](getting-started-with-mvc-part2/_static/image1.png)</span></span>

<span data-ttu-id="447f4-119">새 컨트롤러 "HelloWorldController" 이름과 추가 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="447f4-119">Name your new controller "HelloWorldController" and click Add.</span></span>

<span data-ttu-id="447f4-120">[![컨트롤러 추가 대화 상자](getting-started-with-mvc-part2/_static/image4.png)](getting-started-with-mvc-part2/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="447f4-120">[![Add Controller Dialog](getting-started-with-mvc-part2/_static/image4.png)](getting-started-with-mvc-part2/_static/image3.png)</span></span>

<span data-ttu-id="447f4-121">HelloWorldController.cs 호출에 대해 만든 새 파일 및 해당 파일에 현재 열려 있는 오른쪽의 솔루션 탐색기에서 표시 합니다 **IDE**합니다.</span><span class="sxs-lookup"><span data-stu-id="447f4-121">Notice in the Solution Explorer on the right that a new file has been created for you called HelloWorldController.cs and that file is now opened in the **IDE**.</span></span>

<span data-ttu-id="447f4-122">[![HelloWorldControllerCode](getting-started-with-mvc-part2/_static/image6.png)](getting-started-with-mvc-part2/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="447f4-122">[![HelloWorldControllerCode](getting-started-with-mvc-part2/_static/image6.png)](getting-started-with-mvc-part2/_static/image5.png)</span></span>

<span data-ttu-id="447f4-123">다음과 같은 새 공용 클래스 HelloWorldController 내에서 두 개의 새 메서드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="447f4-123">Create two new methods that look like this inside of your new public class HelloWorldController.</span></span> <span data-ttu-id="447f4-124">예를 들어 컨트롤러에서 직접 html 문자열로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="447f4-124">We'll return a string of HTML directly from our controller as an example.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part2/samples/sample1.cs)]

<span data-ttu-id="447f4-125">컨트롤러 HelloWorldController 이름이 고 새로운 메서드가 인덱스 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="447f4-125">Your Controller is named HelloWorldController and your new Method is called Index.</span></span> <span data-ttu-id="447f4-126">응용 프로그램을 다시 실행 전과 마찬가지로 (재생 단추를 클릭 하거나 f5 키를 눌러이 작업을 수행).</span><span class="sxs-lookup"><span data-stu-id="447f4-126">Run your application again, just as before (click the play button or press F5 to do this).</span></span> <span data-ttu-id="447f4-127">브라우저에 시작 되 면 주소 표시줄에서 경로 변경 `http://localhost:xx/HelloWorld` 여기서 xx는 무엇이 든 번호 컴퓨터 구성 했습니다.</span><span class="sxs-lookup"><span data-stu-id="447f4-127">Once your browser has started up, change the path in the address bar to `http://localhost:xx/HelloWorld` where xx is whatever number your computer has chosen.</span></span> <span data-ttu-id="447f4-128">이제 브라우저 아래 스크린샷 처럼 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="447f4-128">Now your browser should look like the screenshot below.</span></span> <span data-ttu-id="447f4-129">위의 메서드를 반환 했습니다 "콘텐츠입니다." 라는 메서드로 전달 된 문자열</span><span class="sxs-lookup"><span data-stu-id="447f4-129">In our method above we returned a string passed into a method called "Content."</span></span> <span data-ttu-id="447f4-130">기억할지 시스템 일부 HTML을 반환 하 고 못해서!</span><span class="sxs-lookup"><span data-stu-id="447f4-130">We told the system just returns some HTML, and it did!</span></span>

<span data-ttu-id="447f4-131">ASP.NET MVC는 들어오는 URL에 따라 다른 컨트롤러 클래스 (및 그 안에 다양 한 작업 메서드)를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="447f4-131">ASP.NET MVC invokes different Controller classes (and different Action methods within them) depending on the incoming URL.</span></span> <span data-ttu-id="447f4-132">ASP.NET MVC에서 사용 되는 매핑 논리 다음과 같은 형식을 사용 하 여 코드 실행 제어.</span><span class="sxs-lookup"><span data-stu-id="447f4-132">The default mapping logic used by ASP.NET MVC uses a format like this to control what code is run:</span></span>

<span data-ttu-id="447f4-133">/[Controller]/[ActionName]/[Parameters]</span><span class="sxs-lookup"><span data-stu-id="447f4-133">/[Controller]/[ActionName]/[Parameters]</span></span>

<span data-ttu-id="447f4-134">URL의 첫 번째 부분 실행할 컨트롤러 클래스를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="447f4-134">The first part of the URL determines the Controller class to execute.</span></span> <span data-ttu-id="447f4-135">따라서 /HelloWorld HelloWorldController 클래스에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="447f4-135">So /HelloWorld maps to the HelloWorldController class.</span></span> <span data-ttu-id="447f4-136">URL의 두 번째 부분 클래스에 대 한 작업 메서드를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="447f4-136">The second part of the URL determines the Action method on the class to execute.</span></span> <span data-ttu-id="447f4-137">/HelloWorld/Index 없었다는 실행 HelloWorldcontroller 클래스의 index () 메서드.</span><span class="sxs-lookup"><span data-stu-id="447f4-137">So /HelloWorld/Index would cause the Index() method of the HelloWorldcontroller class to execute.</span></span> <span data-ttu-id="447f4-138">만 위의 /HelloWorld 및 인덱스 암시 된 메서드를 방문 해야 함을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="447f4-138">Notice that we only had to visit /HelloWorld above and the method Index was implied.</span></span> <span data-ttu-id="447f4-139">이 "Index" 라는 메서드를 명시적으로 지정 하지 않으면 컨트롤러에서 호출 되는 기본 방법 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="447f4-139">This is because a method named "Index" is the default method that will be called on a controller if one is not explicitly specified.</span></span>

<span data-ttu-id="447f4-140">[![내 기본 작업](getting-started-with-mvc-part2/_static/image8.png)](getting-started-with-mvc-part2/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="447f4-140">[![This is my default action](getting-started-with-mvc-part2/_static/image8.png)](getting-started-with-mvc-part2/_static/image7.png)</span></span>

<span data-ttu-id="447f4-141">이제 방문해 보도록 `http://localhost:xx/HelloWorld/Welcome.` 이제 시작 메서드는 실행 하 고 해당 HTML 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="447f4-141">Now, let's visit `http://localhost:xx/HelloWorld/Welcome.` Now our Welcome Method has executed and returned its HTML string.</span></span>

<span data-ttu-id="447f4-142">마찬가지로 / [Controller] / [ActionName] / [매개 변수] 컨트롤러 HelloWorld 이며 시작 메서드에 경우에 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="447f4-142">Again, /[Controller]/[ActionName]/[Parameters] so Controller is HelloWorld and Welcome is the Method in this case.</span></span> <span data-ttu-id="447f4-143">매개 변수를 아직 완료 하지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="447f4-143">We haven't done Parameters yet.</span></span>

<span data-ttu-id="447f4-144">[![이 시작 작업 방법](getting-started-with-mvc-part2/_static/image10.png)](getting-started-with-mvc-part2/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="447f4-144">[![This is the Welcome action method](getting-started-with-mvc-part2/_static/image10.png)](getting-started-with-mvc-part2/_static/image9.png)</span></span>

<span data-ttu-id="447f4-145">수정 해 보겠습니다 샘플 약간의 일부 정보를 URL에서 다음과 같은 예를 들어 컨트롤러에에 전달할 수 있도록: / HelloWorld/시작? name = Scott&amp;numtimes = 4.</span><span class="sxs-lookup"><span data-stu-id="447f4-145">Let's modify our sample slightly so that we can pass some information in from the URL to our controller, for example like this: /HelloWorld/Welcome?name=Scott&amp;numtimes=4.</span></span> <span data-ttu-id="447f4-146">두 매개 변수 및 아래와 같은 업데이트를 포함 하도록 시작 방법을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="447f4-146">Change your Welcome method to include two parameters and update it like below.</span></span> <span data-ttu-id="447f4-147">매개 변수 numTimes의 기본값은 1에서 전달 하지 않으면 나타내려면 C# 선택적 매개 변수 기능을 사용 했습니다에서는 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="447f4-147">Note that we've used the C# optional parameter feature to indicate that the parameter numTimes should default to 1 if it's not passed in.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part2/samples/sample2.cs)]

<span data-ttu-id="447f4-148">응용 프로그램을 실행 하 고 방문 `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4` 원하는 이름과 numtimes의 값을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="447f4-148">Run your application and visit `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4` changing the value of name and numtimes as you like.</span></span> <span data-ttu-id="447f4-149">시스템에는 메서드의 매개 변수를 쿼리 문자열의 주소 표시줄에서 명명 된 매개 변수를 자동으로 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="447f4-149">The system automatically mapped the named parameters from your query string in the address bar to parameters in your method.</span></span>

<span data-ttu-id="447f4-150">이러한 두 예제에서 컨트롤러 모든 작업을 수행 되었으며에 HTML을 직접 반환 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="447f4-150">In both these examples the controller has been doing all the work, and has been returning HTML directly.</span></span> <span data-ttu-id="447f4-151">일반적으로 컨트롤러를 원하지는 종료 코드를 매우 불편 하므로 직접 HTML을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="447f4-151">Ordinarily we don't want our Controllers returning HTML directly - since that ends up being very cumbersome to code.</span></span> <span data-ttu-id="447f4-152">대신 일반적으로 별도 뷰 템플릿 파일을 HTML 응답을 생성 하는 데 사용 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="447f4-152">Instead we'll typically use a separate View template file to help generate the HTML response.</span></span> <span data-ttu-id="447f4-153">어떻게이 위해서는 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="447f4-153">Let's look at how we can do this.</span></span> <span data-ttu-id="447f4-154">브라우저를 닫고 IDE에 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="447f4-154">Close your browser and return to the IDE.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="447f4-155">[이전](getting-started-with-mvc-part1.md)
> [다음](getting-started-with-mvc-part3.md)</span><span class="sxs-lookup"><span data-stu-id="447f4-155">[Previous](getting-started-with-mvc-part1.md)
[Next](getting-started-with-mvc-part3.md)</span></span>
