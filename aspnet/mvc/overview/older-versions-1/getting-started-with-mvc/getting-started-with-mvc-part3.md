---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part3
title: 뷰 추가 | Microsoft Docs
author: shanselman
description: ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 읽기 및 쓰기 데이터베이스에서 간단한 웹 응용 프로그램을 만듭니다.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: e8f1515c-c277-47ff-a23e-224118f13f02
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part3
msc.type: authoredcontent
ms.openlocfilehash: f55e558dd056e86bdd2310894959aef02a9d8de2
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41831525"
---
<a name="adding-a-view"></a><span data-ttu-id="c52cf-104">뷰 추가</span><span class="sxs-lookup"><span data-stu-id="c52cf-104">Adding a View</span></span>
====================
<span data-ttu-id="c52cf-105">[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="c52cf-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="c52cf-106">ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="c52cf-107">읽기 및 쓰기 데이터베이스는 간단한 웹 응용 프로그램을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="c52cf-108">방문 합니다 [ASP.NET MVC 학습 센터](../../../index.md) 자습서 및 샘플 다른 ASP.NET MVC를 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>


<span data-ttu-id="c52cf-109">이 섹션에서는 하겠습니다 뷰 템플릿 파일을 완전히 다시 클라이언트에 HTML 응답을 생성을 캡슐화 하는 데 HelloWorldController 클래스를 가질 수 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-109">In this section we are going to look at how we can have our HelloWorldController class use a View template file to cleanly encapsulate generating HTML responses back to a client.</span></span>

<span data-ttu-id="c52cf-110">인덱스 메서드에 보기 템플릿을 사용 하 여 시작 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-110">Let's start by using a View template with our Index method.</span></span> <span data-ttu-id="c52cf-111">이 메서드는 인덱스 이며 HelloWorldController 합니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-111">Our method is called Index and it's in the HelloWorldController.</span></span> <span data-ttu-id="c52cf-112">현재 index () 메서드는 컨트롤러 클래스 내에서 하드 코딩 된 메시지를 사용 하 여 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-112">Currently our Index() method returns a string with a message that is hardcoded within the Controller class.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample1.cs)]

<span data-ttu-id="c52cf-113">인덱스 방법 대신 다음과 같이 이제 변경해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-113">Let's now change the Index method to instead look like this:</span></span>

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample2.cs)]

<span data-ttu-id="c52cf-114">Index () 메서드를 사용할 수 있는 프로젝트를 뷰 템플릿으로 지금 추가 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-114">Let's now add a View template to our project that we can use for our Index() method.</span></span> <span data-ttu-id="c52cf-115">이렇게 하려면 인덱스 메서드에 중간 어딘가에 마우스 오른쪽 단추로 클릭 하 고 추가 보기를 클릭 하는 중...</span><span class="sxs-lookup"><span data-stu-id="c52cf-115">To do this, right-click with your mouse somewhere in the middle of the Index method and click Add View...</span></span>

![이미지](getting-started-with-mvc-part3/_static/image1.png)

<span data-ttu-id="c52cf-117">우리는 인덱스 메서드에서 사용할 수 있는 보기 템플릿을 만들려고 하는 방법에 대 한 몇 가지 옵션을 제공 하는 "뷰 추가" 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-117">This will bring up the "Add View" dialog which provides us some options for how we want to create a view template that can be used by our Index method.</span></span> <span data-ttu-id="c52cf-118">지금은 없습니다 아무것도 변경 및 추가 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-118">For now, don't change anything, and just click the Add button.</span></span>

<span data-ttu-id="c52cf-119">[![뷰 추가 대화 상자](getting-started-with-mvc-part3/_static/image3.png)](getting-started-with-mvc-part3/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="c52cf-119">[![Add View Dialog](getting-started-with-mvc-part3/_static/image3.png)](getting-started-with-mvc-part3/_static/image2.png)</span></span>

<span data-ttu-id="c52cf-120">추가 클릭 하면 새 폴더 및 새 파일 나타납니다 솔루션 폴더에 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-120">After you click Add, a new folder and a new file will appear in the Solution Folder, as seen here.</span></span> <span data-ttu-id="c52cf-121">이제 뷰 및 Index.aspx 파일에 HelloWorld 폴더를 해당 폴더 내에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-121">I now have a HelloWorld folder under Views, and an Index.aspx file inside that folder.</span></span>

<span data-ttu-id="c52cf-122">[![solutionexplorerwithindex](getting-started-with-mvc-part3/_static/image5.png)](getting-started-with-mvc-part3/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="c52cf-122">[![solutionexplorerwithindex](getting-started-with-mvc-part3/_static/image5.png)](getting-started-with-mvc-part3/_static/image4.png)</span></span>

<span data-ttu-id="c52cf-123">새 인덱스 파일이 이미 열린 및 편집을 위해 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-123">The new Index file is also already opened and ready for editing.</span></span> <span data-ttu-id="c52cf-124">첫 번째 텍스트를 추가 &lt;h2&gt;인덱스&lt;/h2&gt; "Hello World."와 같은</span><span class="sxs-lookup"><span data-stu-id="c52cf-124">Add some text under the first &lt;h2&gt;Index&lt;/h2&gt; like "Hello World."</span></span>

[!code-html[Main](getting-started-with-mvc-part3/samples/sample3.html)]

<span data-ttu-id="c52cf-125">응용 프로그램을 실행 하 고 방문 [ `http://localhost:xx/HelloWorld` ](http://localhostxx) 브라우저에서 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-125">Run your application and visit [`http://localhost:xx/HelloWorld`](http://localhostxx) again in your browser.</span></span> <span data-ttu-id="c52cf-126">이 예제에서 컨트롤러의 인덱스 메서드에서 모든 작업을 수행 하지 않은 하지만 보기 템플릿 파일을 사용 하 여 클라이언트에 다시 응답을 렌더링 하려고 했습니다 나타내는 "반환 View()"를 호출 하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-126">The Index method in our controller in this example didn't do any work, but did call "return View()" which indicated that we wanted to use a view template file to render a response back to the client.</span></span> <span data-ttu-id="c52cf-127">에서는 않았습니다 지정 하지 않으므로 명시적으로 사용 하 여 뷰 템플릿 파일의 이름, Index.aspx 뷰 파일을 사용 하 여 \Views\HelloWorld 폴더 내에 ASP.NET MVC 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-127">Because we did not explicitly specify the name of the view template file to use, ASP.NET MVC defaulted to using the Index.aspx view file within the \Views\HelloWorld folder.</span></span> <span data-ttu-id="c52cf-128">이제에서는 하드 코드 된 뷰에 문자열이 표시 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-128">Now we see the string we hard-coded in our View.</span></span>

<span data-ttu-id="c52cf-129">[![Windows Internet Explorer 인덱스](getting-started-with-mvc-part3/_static/image7.png)](getting-started-with-mvc-part3/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="c52cf-129">[![Index - Windows Internet Explorer](getting-started-with-mvc-part3/_static/image7.png)](getting-started-with-mvc-part3/_static/image6.png)</span></span>

<span data-ttu-id="c52cf-130">잘 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-130">Looks pretty good.</span></span> <span data-ttu-id="c52cf-131">그러나 브라우저의 제목 "Index" 라는 페이지의 큰 제목에 "내 MVC 응용 프로그램입니다." 라는 것을 알합니다</span><span class="sxs-lookup"><span data-stu-id="c52cf-131">However, notice that the Browser's title says "Index" and the big title on the page says "My MVC Application."</span></span> <span data-ttu-id="c52cf-132">이러한 파일을 변경해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-132">Let's change those.</span></span>

### <a name="changing-views-and-master-pages"></a><span data-ttu-id="c52cf-133">보기 및 마스터 페이지를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-133">Changing Views and Master Pages</span></span>

<span data-ttu-id="c52cf-134">먼저 텍스트 "내 MVC 응용 프로그램입니다."을 변경해 보겠습니다</span><span class="sxs-lookup"><span data-stu-id="c52cf-134">First, let's change the text "My MVC Application."</span></span> <span data-ttu-id="c52cf-135">해당 텍스트를 공유 하 고 모든 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-135">That text is shared and appears on every page.</span></span> <span data-ttu-id="c52cf-136">실제로 나타나는 곳 에서만 코드를 앱에서 모든 페이지에도 합니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-136">It actually appears in only one place in our code, even though it's on every page in our app.</span></span> <span data-ttu-id="c52cf-137">솔루션 탐색기에서 /Views/Shared 폴더로 이동한 Site.Master 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-137">Go to the /Views/Shared folder in the Solution Explorer and open the Site.Master file.</span></span> <span data-ttu-id="c52cf-138">이 파일은 마스터 페이지 라고 하 고 공유 "셸"는 다른 모든 페이지를 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-138">This file is called a Master Page and it's the shared "shell" that all our other pages use.</span></span>

<span data-ttu-id="c52cf-139">이 파일의 ContentPlaceholder "MainContent" 라는 텍스트를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-139">Notice some text that says ContentPlaceholder "MainContent" in this file.</span></span>

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample4.aspx)]

<span data-ttu-id="c52cf-140">자리 표시자 이며 여기서 만든 모든 페이지 표시 됩니다, 마스터 페이지에 "래핑된"</span><span class="sxs-lookup"><span data-stu-id="c52cf-140">That placeholder is where all the pages you create will show up, "wrapped" in the master page.</span></span> <span data-ttu-id="c52cf-141">앱을 실행 하 고 여러 페이지를 방문 제목을 변경을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-141">Try changing the title, then run your app and visit multiple pages.</span></span> <span data-ttu-id="c52cf-142">하나의 변경 내용을 여러 페이지에 표시 되는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-142">You'll notice that your one change appears on multiple pages.</span></span>

[!code-html[Main](getting-started-with-mvc-part3/samples/sample5.html)]

<span data-ttu-id="c52cf-143">H1-"내 MVC 동영상 응용 프로그램입니다."의 모든 페이지를 기본 제목-이제는</span><span class="sxs-lookup"><span data-stu-id="c52cf-143">Now every page will have the Primary Heading - that's H1 - of "My MVC Movie Application."</span></span> <span data-ttu-id="c52cf-144">맨 위쪽에 있는 모든 페이지 간에 공유 되는 흰색 텍스트를 처리 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-144">That handles the white text at the top there that's shared across all the pages.</span></span>

<span data-ttu-id="c52cf-145">변경 된 제목이 사용 하 여 전체에서 Site.Master 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-145">Here is the Site.Master in its entirety with our changed title:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample6.aspx)]

<span data-ttu-id="c52cf-146">이제 인덱스 페이지의 제목을 변경 해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-146">Now, let's change the title of the Index page.</span></span>

<span data-ttu-id="c52cf-147">/HelloWorld/Index.aspx를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-147">Open /HelloWorld/Index.aspx.</span></span> <span data-ttu-id="c52cf-148">변경 하려면 두 위치 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-148">There's two places to change.</span></span> <span data-ttu-id="c52cf-149">첫째, 제목에에서 나타나는 보조 머리글도 H2-는 브라우저의 제목입니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-149">First, the Title that appears in the title of the browser, then the secondary header - that's H2 - as well.</span></span> <span data-ttu-id="c52cf-150">만들겠습니다 각각는 약간의 코드를 볼 수 있도록 약간 다른 앱의 어느 부분을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-150">I'll make them each slightly different so you can see which bit of code changes which part of the app.</span></span>

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample7.aspx)]

<span data-ttu-id="c52cf-151">앱을 실행 하 고 /Movies를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="c52cf-151">Run your app and visit /Movies.</span></span> <span data-ttu-id="c52cf-152">브라우저 제목, 기본 제목 및 작은 제목이 변경 되었습니다. 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-152">Notice that the browser title, the primary heading and the secondary headings have changed.</span></span> <span data-ttu-id="c52cf-153">보기에 작은 변경 내용을 사용 하 여 앱에서 큰 변화를 확인 하기 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-153">It's easy to make big changes in your app with small changes to your view.</span></span>

<span data-ttu-id="c52cf-154">[![영화 목록-Windows Internet Explorer](getting-started-with-mvc-part3/_static/image9.png)](getting-started-with-mvc-part3/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="c52cf-154">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part3/_static/image9.png)](getting-started-with-mvc-part3/_static/image8.png)</span></span>

<span data-ttu-id="c52cf-155">우리의 약간 (이 경우 "Hello World!"의 "데이터"의</span><span class="sxs-lookup"><span data-stu-id="c52cf-155">Our little bit of "data" (in this case the "Hello World!"</span></span> <span data-ttu-id="c52cf-156">메시지)는 하드 코딩 하지만입니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-156">message) was hard coded though.</span></span> <span data-ttu-id="c52cf-157">했습니다 V (뷰) 및 C (컨트롤러) 하지만 없습니다 M (모델) 아직를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-157">We've got V (Views) and we've got C (Controllers), but no M (Model) yet.</span></span> <span data-ttu-id="c52cf-158">방법을 곧 살펴보겠습니다 데이터베이스를 만들고 여기에서 모델 데이터를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-158">We'll shortly walk through how create a database and retrieve model data from it.</span></span>

## <a name="passing-a-viewmodel"></a><span data-ttu-id="c52cf-159">ViewModel을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-159">Passing a ViewModel</span></span>

<span data-ttu-id="c52cf-160">전에 데이터베이스를 이동 하 고 모델에 대 한 설명, 그러나 처음에 대해 살펴보겠습니다 "Viewmodel"로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-160">Before we go to a database and talk about Models, though, let's first talk about "ViewModels."</span></span> <span data-ttu-id="c52cf-161">이 클라이언트에 HTML 응답을 렌더링 해야 하는 뷰 템플릿을 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-161">These are objects that represent what a View template requires to render an HTML response back to a client.</span></span> <span data-ttu-id="c52cf-162">일반적으로 생성 됩니다 및 템플릿 보기, 컨트롤러 클래스에 의해 전달 하며 보기 템플릿이 필요 하며 받는 데이터 및 더 이상 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-162">They are typically created and passed by a Controller class to a View template, and should only contain the data that the View template requires - and no more.</span></span>

<span data-ttu-id="c52cf-163">이전에 HelloWorld 샘플을 사용 하 여이 Welcome() 작업 메서드 이름과 numTimes 매개 변수는 데 걸린 및 브라우저에 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-163">Previously with our HelloWorld sample, our Welcome() action method took a name and a numTimes parameter and output it to the browser.</span></span> <span data-ttu-id="c52cf-164">계속 직접이 응답을 렌더링 하는 컨트롤러에 있는 것이 아니라 대신 보겠습니다 작은 클래스를를 해당 데이터를 보유할 보기 템플릿을 사용 하 여 HTML 응답을 렌더링 하를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-164">Rather than have the Controller continue to render this response directly,let's instead make a small class to hold that data and then pass it over to a View template to render back the HTML response using it.</span></span> <span data-ttu-id="c52cf-165">컨트롤러 보기 템플릿에서 한 가지와 관련이이 이렇게 다른 – 정리 "문제의 분리" 응용 프로그램 내에서 유지 관리를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-165">This way the Controller is concerned with one thing and the View template another – enabling us to maintain clean "separation of concerns" within our application.</span></span>

<span data-ttu-id="c52cf-166">HelloWorldController.cs 파일 및 새 "WelcomeViewModel" 클래스를 추가 돌아가서 컨트롤러 내에서 시작 하는 방법을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-166">Return to the HelloWorldController.cs file and add a new "WelcomeViewModel" class and change the Welcome method inside your controller.</span></span> <span data-ttu-id="c52cf-167">동일한 파일에서 새 클래스를 사용 하 여 전체 HelloWorldController.cs 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-167">Here is the complete HelloWorldController.cs with the new class in the same file.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample8.cs)]

<span data-ttu-id="c52cf-168">여러 줄에 있는 경우에이 시작 방법은 실제로 두 개의 코드 문을입니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-168">Even though it's on multiple lines, our Welcome method is really only two code statements.</span></span> <span data-ttu-id="c52cf-169">첫 번째 문은 결과 개체 보기를 ViewModel 개체에 두 번째 패스는 두 매개 변수를 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-169">The first statement packages up our two parameters into a ViewModel object, and the second passes the resulting object onto the View.</span></span>

<span data-ttu-id="c52cf-170">이제 시작 보기 템플릿이 필요 합니다!</span><span class="sxs-lookup"><span data-stu-id="c52cf-170">Now we need a Welcome View template!</span></span> <span data-ttu-id="c52cf-171">시작 메서드를 마우스 오른쪽 단추로 클릭 하 고 뷰 추가 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-171">Right click in the Welcome method and select Add View.</span></span> <span data-ttu-id="c52cf-172">이 이번에 됩니다 "강력한 형식의 뷰 만들기"를 확인 하 고 드롭다운 목록에서에서 WelcomeViewModel 클래스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-172">This time, we'll check "Create a strongly-typed view" and select our WelcomeViewModel class from the drop down list.</span></span> <span data-ttu-id="c52cf-173">이 새 보기는 WelcomeViewModels 및 다른 종류의 개체에 대해서만 인식 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-173">This new view will only know about WelcomeViewModels and no other types of objects.</span></span>

> <span data-ttu-id="c52cf-174">*참고: 드롭다운 목록에에서 표시에 대 한 프로그램 WelcomeViewModel 추가 후 한 번 컴파일한 해야 합니다.*</span><span class="sxs-lookup"><span data-stu-id="c52cf-174">*NOTE: You'll need to have compiled once after adding your WelcomeViewModel for to show up in the drop down list.*</span></span>


<span data-ttu-id="c52cf-175">뷰 추가 대화 상자 모양을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-175">Here's what your Add View dialog should look like.</span></span> <span data-ttu-id="c52cf-176">추가 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-176">Click the Add button.</span></span> ![보기 원으로 표시 추가](getting-started-with-mvc-part3/_static/image10.png)

<span data-ttu-id="c52cf-178">아래에이 코드를 추가 합니다 &lt;h2&gt; 에 새 Welcome.aspx에서.</span><span class="sxs-lookup"><span data-stu-id="c52cf-178">Add this code under the &lt;h2&gt; in your new Welcome.aspx.</span></span> <span data-ttu-id="c52cf-179">루프를 확인 하 고 사용자가 해야 만큼 살펴보기 드리겠습니다!</span><span class="sxs-lookup"><span data-stu-id="c52cf-179">We'll make a loop and say Hello as many times as the user says we should!</span></span>

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample9.aspx)]

<span data-ttu-id="c52cf-180">또한 기억할지이 WelcomeViewModel에 대 한 보기 때문에 입력 하는 동안 확인 (결혼 여부는, 기억?)은 모델 개체 아래 스크린샷에 표시 된 참조 될 때마다 유용한 Intellisense를 시작 하기:</span><span class="sxs-lookup"><span data-stu-id="c52cf-180">Also, notice while you're typing that because we told this View about the WelcomeViewModel (they are married, remember?) that we get helpful Intellisense each time we reference our Model object as seen in the screenshot below:</span></span>

<span data-ttu-id="c52cf-181">[![NumTime 소스 코드](getting-started-with-mvc-part3/_static/image12.png)](getting-started-with-mvc-part3/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="c52cf-181">[![NumTime Source Code](getting-started-with-mvc-part3/_static/image12.png)](getting-started-with-mvc-part3/_static/image11.png)</span></span>

<span data-ttu-id="c52cf-182">응용 프로그램을 실행 하 고 방문 `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4` 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-182">Run your application and visit `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4` again.</span></span> <span data-ttu-id="c52cf-183">URL에서 데이터 취하고 이제 자동으로 컨트롤러에 전달 될, 컨트롤러 ViewModel에 대 한 데이터를 패키지 하 고 보기에 해당 개체를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-183">Now we're taking data from the URL, it's passed into our Controller automatically, our Controller packages up the data into a ViewModel and passes that object onto our View.</span></span> <span data-ttu-id="c52cf-184">사용자에 게 HTML로 데이터를 표시 하는 보다 뷰.</span><span class="sxs-lookup"><span data-stu-id="c52cf-184">The View than displays the data as HTML to the user.</span></span>

<span data-ttu-id="c52cf-185">[![시작-Windows Internet Explorer](getting-started-with-mvc-part3/_static/image14.png)](getting-started-with-mvc-part3/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="c52cf-185">[![Welcome - Windows Internet Explorer](getting-started-with-mvc-part3/_static/image14.png)](getting-started-with-mvc-part3/_static/image13.png)</span></span>

<span data-ttu-id="c52cf-186">물론 특정 유형의 모델에 대 한 "M" 이지만 데이터베이스 유형은 하지 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-186">Well, that was a kind of an "M" for Model, but not the database kind.</span></span> <span data-ttu-id="c52cf-187">새로운 지금까지 학습 한 동영상의 데이터베이스를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c52cf-187">Let's take what we've learned and create a database of Movies.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c52cf-188">[이전](getting-started-with-mvc-part2.md)
> [다음](getting-started-with-mvc-part4.md)</span><span class="sxs-lookup"><span data-stu-id="c52cf-188">[Previous](getting-started-with-mvc-part2.md)
[Next](getting-started-with-mvc-part4.md)</span></span>
