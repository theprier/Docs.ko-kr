---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part3
title: 뷰 추가 | Microsoft Docs
author: shanselman
description: ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 읽기 및 쓰기는 데이터베이스에서 단순 웹 응용 프로그램을 만듭니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/14/2010
ms.topic: article
ms.assetid: e8f1515c-c277-47ff-a23e-224118f13f02
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part3
msc.type: authoredcontent
ms.openlocfilehash: 978d7980274c072ed559b54ed69ab86245b6c5a7
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="adding-a-view"></a><span data-ttu-id="5c283-104">뷰 추가</span><span class="sxs-lookup"><span data-stu-id="5c283-104">Adding a View</span></span>
====================
<span data-ttu-id="5c283-105">으로 [Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="5c283-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="5c283-106">ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="5c283-107">읽기 및 쓰기는 데이터베이스에서 단순 웹 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="5c283-108">방문는 [ASP.NET MVC 학습 센터](../../../index.md) 자습서 및 예제에는 다른 ASP.NET MVC를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>


<span data-ttu-id="5c283-109">이 섹션에서는 하겠습니다 보기 템플릿 파일을 사용 하 여 클라이언트에 다시 생성 HTML 응답 캡슐화 HelloWorldController 클래스 수 있는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-109">In this section we are going to look at how we can have our HelloWorldController class use a View template file to cleanly encapsulate generating HTML responses back to a client.</span></span>

<span data-ttu-id="5c283-110">이 인덱스 메서드로 템플릿 보기를 사용 하 여 시작 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-110">Let's start by using a View template with our Index method.</span></span> <span data-ttu-id="5c283-111">이 메서드는 인덱스 및는 HelloWorldController에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-111">Our method is called Index and it's in the HelloWorldController.</span></span> <span data-ttu-id="5c283-112">현재이 index () 메서드는 컨트롤러 클래스 내에서 하드 코드 된 메시지가 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-112">Currently our Index() method returns a string with a message that is hardcoded within the Controller class.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample1.cs)]

<span data-ttu-id="5c283-113">이제 인덱스 메서드를 대신 다음과 같이 표시를 바꿔보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-113">Let's now change the Index method to instead look like this:</span></span>

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample2.cs)]

<span data-ttu-id="5c283-114">Index () 메서드에 대 한 사용할 수 있는 프로젝트에 템플릿 보기를 지금 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-114">Let's now add a View template to our project that we can use for our Index() method.</span></span> <span data-ttu-id="5c283-115">이 수행 하려면 인덱스 메서드 중간 어딘가에 마우스 오른쪽 단추로 클릭 하 고 추가 보기를 클릭...</span><span class="sxs-lookup"><span data-stu-id="5c283-115">To do this, right-click with your mouse somewhere in the middle of the Index method and click Add View...</span></span>

![이미지](getting-started-with-mvc-part3/_static/image1.png)

<span data-ttu-id="5c283-117">그러면 우리 우리의 인덱스 메서드에 의해 사용할 수 있는 보기 템플릿을 만드는 하고자 하는 방법에 대 한 몇 가지 옵션을 제공 하 여 "뷰 추가" 대화 상자를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-117">This will bring up the "Add View" dialog which provides us some options for how we want to create a view template that can be used by our Index method.</span></span> <span data-ttu-id="5c283-118">지금은 없습니다 아무것도 변경 및 추가 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-118">For now, don't change anything, and just click the Add button.</span></span>

<span data-ttu-id="5c283-119">[![뷰 추가 대화 상자](getting-started-with-mvc-part3/_static/image3.png)](getting-started-with-mvc-part3/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="5c283-119">[![Add View Dialog](getting-started-with-mvc-part3/_static/image3.png)](getting-started-with-mvc-part3/_static/image2.png)</span></span>

<span data-ttu-id="5c283-120">추가 클릭 한 후에 새 폴더 및 새 파일 나타납니다 솔루션 폴더에 다음 그림과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-120">After you click Add, a new folder and a new file will appear in the Solution Folder, as seen here.</span></span> <span data-ttu-id="5c283-121">이제 해당 폴더 내의 보기 및 Index.aspx 파일에서 HelloWorld 폴더를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-121">I now have a HelloWorld folder under Views, and an Index.aspx file inside that folder.</span></span>

<span data-ttu-id="5c283-122">[![solutionexplorerwithindex](getting-started-with-mvc-part3/_static/image5.png)](getting-started-with-mvc-part3/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="5c283-122">[![solutionexplorerwithindex](getting-started-with-mvc-part3/_static/image5.png)](getting-started-with-mvc-part3/_static/image4.png)</span></span>

<span data-ttu-id="5c283-123">새 인덱스 파일 이기도 이미 열려 있고 편집을 위해 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-123">The new Index file is also already opened and ready for editing.</span></span> <span data-ttu-id="5c283-124">첫 번째에서 일부 텍스트 추가 &lt;h2&gt;인덱스&lt;/h2&gt; "Hello World."와 같은</span><span class="sxs-lookup"><span data-stu-id="5c283-124">Add some text under the first &lt;h2&gt;Index&lt;/h2&gt; like "Hello World."</span></span>

[!code-html[Main](getting-started-with-mvc-part3/samples/sample3.html)]

<span data-ttu-id="5c283-125">ְ ְ ¿כ 방문 [ `http://localhost:xx/HelloWorld` ](http://localhostxx) 브라우저에서 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-125">Run your application and visit [`http://localhost:xx/HelloWorld`](http://localhostxx) again in your browser.</span></span> <span data-ttu-id="5c283-126">이 예에서 컨트롤러 인덱스 메서드 한 작업을 수행 하지 않은 하지만 보기 템플릿 파일을 사용 하 여 클라이언트에 다시 응답을 렌더링 하 려 표시 "반환 View()" 호출 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-126">The Index method in our controller in this example didn't do any work, but did call "return View()" which indicated that we wanted to use a view template file to render a response back to the client.</span></span> <span data-ttu-id="5c283-127">사용할 보기 템플릿 파일의 이름, 명시적으로 지정 되지 않았기 때문에 ASP.NET MVC Index.aspx 뷰 파일을 사용 하 여 \Views\HelloWorld 폴더 내에 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-127">Because we did not explicitly specify the name of the view template file to use, ASP.NET MVC defaulted to using the Index.aspx view file within the \Views\HelloWorld folder.</span></span> <span data-ttu-id="5c283-128">이제 우리 하드 코드 된 우리의 보기에서 문자열을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-128">Now we see the string we hard-coded in our View.</span></span>

<span data-ttu-id="5c283-129">[![인덱스-Windows Internet Explorer](getting-started-with-mvc-part3/_static/image7.png)](getting-started-with-mvc-part3/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="5c283-129">[![Index - Windows Internet Explorer](getting-started-with-mvc-part3/_static/image7.png)](getting-started-with-mvc-part3/_static/image6.png)</span></span>

<span data-ttu-id="5c283-130">잘 보입니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-130">Looks pretty good.</span></span> <span data-ttu-id="5c283-131">그러나 고 해당 데이터베이스는 브라우저의 제목 "Index" 라는 페이지에서 큰 제목에 "내 MVC 응용 프로그램입니다." 라고 표시</span><span class="sxs-lookup"><span data-stu-id="5c283-131">However, notice that the Browser's title says "Index" and the big title on the page says "My MVC Application."</span></span> <span data-ttu-id="5c283-132">이러한 변경 해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-132">Let's change those.</span></span>

### <a name="changing-views-and-master-pages"></a><span data-ttu-id="5c283-133">뷰 및 마스터 페이지를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-133">Changing Views and Master Pages</span></span>

<span data-ttu-id="5c283-134">첫째, 바꿔보겠습니다 텍스트 "내 MVC 응용 프로그램입니다."</span><span class="sxs-lookup"><span data-stu-id="5c283-134">First, let's change the text "My MVC Application."</span></span> <span data-ttu-id="5c283-135">해당 텍스트를 공유 하 고 모든 페이지에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-135">That text is shared and appears on every page.</span></span> <span data-ttu-id="5c283-136">실제로 나타납니다 한 위치를 코드에만 앱의 모든 페이지에는.</span><span class="sxs-lookup"><span data-stu-id="5c283-136">It actually appears in only one place in our code, even though it's on every page in our app.</span></span> <span data-ttu-id="5c283-137">솔루션 탐색기에서 /Views/Shared 폴더 이동한 Site.Master 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-137">Go to the /Views/Shared folder in the Solution Explorer and open the Site.Master file.</span></span> <span data-ttu-id="5c283-138">이 파일은 마스터 페이지 라고 하 고 공유 "셸" 우리의 다른 모든 페이지를 사용 하는 것이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-138">This file is called a Master Page and it's the shared "shell" that all our other pages use.</span></span>

<span data-ttu-id="5c283-139">이 파일의 일부 라는 텍스트를 "MainContent" ContentPlaceholder 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-139">Notice some text that says ContentPlaceholder "MainContent" in this file.</span></span>

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample4.aspx)]

<span data-ttu-id="5c283-140">자리 표시자 위치를 만들면 모든 페이지 표시 됩니다, 마스터 페이지에 "래핑되어"입니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-140">That placeholder is where all the pages you create will show up, "wrapped" in the master page.</span></span> <span data-ttu-id="5c283-141">바꾸려고 제목, 응용 프로그램을 실행 하 고 여러 페이지를 방문 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-141">Try changing the title, then run your app and visit multiple pages.</span></span> <span data-ttu-id="5c283-142">하나의 변경 내용을 여러 페이지에 표시 되는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-142">You'll notice that your one change appears on multiple pages.</span></span>

[!code-html[Main](getting-started-with-mvc-part3/samples/sample5.html)]

<span data-ttu-id="5c283-143">"내 MVC 영화 응용 프로그램입니다.."의 H1-이제 모든 페이지를 기본 제목-갖습니다입니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-143">Now every page will have the Primary Heading - that's H1 - of "My MVC Movie Application."</span></span> <span data-ttu-id="5c283-144">위쪽에 있는 모든 페이지에서 공유 되는 흰색 텍스트를 처리 하는입니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-144">That handles the white text at the top there that's shared across all the pages.</span></span>

<span data-ttu-id="5c283-145">이 변경 된 제목으로 한 번에는 Site.Master 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-145">Here is the Site.Master in its entirety with our changed title:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample6.aspx)]

<span data-ttu-id="5c283-146">이제 인덱스 페이지의 제목을 변경 해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-146">Now, let's change the title of the Index page.</span></span>

<span data-ttu-id="5c283-147">/HelloWorld/Index.aspx를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-147">Open /HelloWorld/Index.aspx.</span></span> <span data-ttu-id="5c283-148">두 곳 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-148">There's two places to change.</span></span> <span data-ttu-id="5c283-149">첫째, 제목에에서 나타나는 보조 헤더-도 h-2에는 브라우저의 제목입니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-149">First, the Title that appears in the title of the browser, then the secondary header - that's H2 - as well.</span></span> <span data-ttu-id="5c283-150">각 비트는 코드를 확인할 수 있도록 약간 다른 응용 프로그램의 어느 부분이 변경 시킬 겁니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-150">I'll make them each slightly different so you can see which bit of code changes which part of the app.</span></span>

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample7.aspx)]

<span data-ttu-id="5c283-151">응용 프로그램을 실행 하 고 /Movies를 방문 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-151">Run your app and visit /Movies.</span></span> <span data-ttu-id="5c283-152">브라우저의 제목, 기본 제목 및 작은 제목을 변경 되었습니다. 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-152">Notice that the browser title, the primary heading and the secondary headings have changed.</span></span> <span data-ttu-id="5c283-153">크게 변경 약간 변경 된 응용 프로그램에서 보기에 두는 것이 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-153">It's easy to make big changes in your app with small changes to your view.</span></span>

<span data-ttu-id="5c283-154">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part3/_static/image9.png)](getting-started-with-mvc-part3/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="5c283-154">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part3/_static/image9.png)](getting-started-with-mvc-part3/_static/image8.png)</span></span>

<span data-ttu-id="5c283-155">우리의 약간 (이 경우 "Hello World!"의 "데이터"의</span><span class="sxs-lookup"><span data-stu-id="5c283-155">Our little bit of "data" (in this case the "Hello World!"</span></span> <span data-ttu-id="5c283-156">그러나 코딩 된 메시지)는 하드입니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-156">message) was hard coded though.</span></span> <span data-ttu-id="5c283-157">V (Views) 준비 하 고 C (컨트롤러) 하지만 없는 M (모델) 아직 접수 했습니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-157">We've got V (Views) and we've got C (Controllers), but no M (Model) yet.</span></span> <span data-ttu-id="5c283-158">방법 곧 살펴봅니다 데이터베이스를 만들고 여기에서 모델 데이터를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-158">We'll shortly walk through how create a database and retrieve model data from it.</span></span>

## <a name="passing-a-viewmodel"></a><span data-ttu-id="5c283-159">ViewModel 전달</span><span class="sxs-lookup"><span data-stu-id="5c283-159">Passing a ViewModel</span></span>

<span data-ttu-id="5c283-160">데이터베이스를 이동 하 고 모델에 대해 설명 하는, 그러나 처음에 대해 살펴보기 "Viewmodel입니다."</span><span class="sxs-lookup"><span data-stu-id="5c283-160">Before we go to a database and talk about Models, though, let's first talk about "ViewModels."</span></span> <span data-ttu-id="5c283-161">이들은 HTML 응답을 클라이언트로 다시 렌더링 해야 하는 뷰 템플릿을 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-161">These are objects that represent what a View template requires to render an HTML response back to a client.</span></span> <span data-ttu-id="5c283-162">일반적으로 만들어지는 및 템플릿 보기에는 컨트롤러 클래스에 의해 전달 하며 뷰 템플릿에 필요한-데이터와 더 이상 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-162">They are typically created and passed by a Controller class to a View template, and should only contain the data that the View template requires - and no more.</span></span>

<span data-ttu-id="5c283-163">이전에 HelloWorld 샘플의 경우와 우리의 Welcome() 동작 메서드는 이름과 numTimes 매개 변수 하 고 브라우저에 출력.</span><span class="sxs-lookup"><span data-stu-id="5c283-163">Previously with our HelloWorld sample, our Welcome() action method took a name and a numTimes parameter and output it to the browser.</span></span> <span data-ttu-id="5c283-164">이 응답을 직접 렌더링 하 계속 컨트롤러를 갖는 대신 대신 만들어 보겠습니다 데이터를 저장 하 고 다시 사용 하 여 HTML 응답을 렌더링 하는 보기 템플릿을를 통해 전달 하기 위한 작은 클래스.</span><span class="sxs-lookup"><span data-stu-id="5c283-164">Rather than have the Controller continue to render this response directly,let's instead make a small class to hold that data and then pass it over to a View template to render back the HTML response using it.</span></span> <span data-ttu-id="5c283-165">컨트롤러는 한 가지 및 템플릿 보기와 관련 되어 이러한 방식으로 다른 – 정리 "문제의 분리" 응용 프로그램 내에서 유지 관리를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-165">This way the Controller is concerned with one thing and the View template another – enabling us to maintain clean "separation of concerns" within our application.</span></span>

<span data-ttu-id="5c283-166">HelloWorldController.cs 파일을 반환 하 고 새 "WelcomeViewModel" 클래스를 추가 하 고 컨트롤러 내 시작 방법을 변경.</span><span class="sxs-lookup"><span data-stu-id="5c283-166">Return to the HelloWorldController.cs file and add a new "WelcomeViewModel" class and change the Welcome method inside your controller.</span></span> <span data-ttu-id="5c283-167">다음은 동일한 파일에서 새 클래스와 함께 전체 HelloWorldController.cs입니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-167">Here is the complete HelloWorldController.cs with the new class in the same file.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample8.cs)]

<span data-ttu-id="5c283-168">여러 줄에는 것이 시작 방법은 실제로 두 개의 코드 문을 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-168">Even though it's on multiple lines, our Welcome method is really only two code statements.</span></span> <span data-ttu-id="5c283-169">ViewModel 개체 및 두 번째 단계에는 두 개의 매개 변수를 결과 개체 보기에 패키지 하는 첫 번째 문입니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-169">The first statement packages up our two parameters into a ViewModel object, and the second passes the resulting object onto the View.</span></span>

<span data-ttu-id="5c283-170">이제 시작 뷰 템플릿이 필요 합니다!</span><span class="sxs-lookup"><span data-stu-id="5c283-170">Now we need a Welcome View template!</span></span> <span data-ttu-id="5c283-171">시작 메서드에서 마우스 오른쪽 단추로 클릭 하 고 추가 보기를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-171">Right click in the Welcome method and select Add View.</span></span> <span data-ttu-id="5c283-172">이 시간 확인 "강력한 형식의 뷰 만들기" 알아보고 하겠습니다 WelcomeViewModel 클래스 드롭 다운 목록에서에서 선택.</span><span class="sxs-lookup"><span data-stu-id="5c283-172">This time, we'll check "Create a strongly-typed view" and select our WelcomeViewModel class from the drop down list.</span></span> <span data-ttu-id="5c283-173">이 새 보기 WelcomeViewModels 및 다른 형식의 개체에 대 한만 알게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-173">This new view will only know about WelcomeViewModels and no other types of objects.</span></span>

> <span data-ttu-id="5c283-174">*참고: 드롭다운 목록에에서 표시에 대 한 프로그램 WelcomeViewModel을 추가한 후 한 번 컴파일한 해야 합니다.*</span><span class="sxs-lookup"><span data-stu-id="5c283-174">*NOTE: You'll need to have compiled once after adding your WelcomeViewModel for to show up in the drop down list.*</span></span>


<span data-ttu-id="5c283-175">뷰 추가 대화 상자에는 모양은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-175">Here's what your Add View dialog should look like.</span></span> <span data-ttu-id="5c283-176">추가 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-176">Click the Add button.</span></span> ![보기 원으로 표시 추가](getting-started-with-mvc-part3/_static/image10.png)

<span data-ttu-id="5c283-178">아래이 코드를 추가 &lt;h2&gt; 프로그램 새 Welcome.aspx에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-178">Add this code under the &lt;h2&gt; in your new Welcome.aspx.</span></span> <span data-ttu-id="5c283-179">사용자가 중요 횟수 만큼 Hello 말 알아보고 루프 확인 하겠습니다!</span><span class="sxs-lookup"><span data-stu-id="5c283-179">We'll make a loop and say Hello as many times as the user says we should!</span></span>

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample9.aspx)]

<span data-ttu-id="5c283-180">또한이 뷰는 WelcomeViewModel에 대 한 말씀 때문에 입력 하는 동안 확인 (결혼 여부는, 기억?) 될 때마다를 참조 하는 모델 개체 아래 스크린샷에서 보듯이 유용한 Intellisense을 얻기:</span><span class="sxs-lookup"><span data-stu-id="5c283-180">Also, notice while you're typing that because we told this View about the WelcomeViewModel (they are married, remember?) that we get helpful Intellisense each time we reference our Model object as seen in the screenshot below:</span></span>

<span data-ttu-id="5c283-181">[![NumTime 소스 코드](getting-started-with-mvc-part3/_static/image12.png)](getting-started-with-mvc-part3/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="5c283-181">[![NumTime Source Code](getting-started-with-mvc-part3/_static/image12.png)](getting-started-with-mvc-part3/_static/image11.png)</span></span>

<span data-ttu-id="5c283-182">ְ ְ ¿כ 방문 `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4` 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-182">Run your application and visit `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4` again.</span></span> <span data-ttu-id="5c283-183">त ु म 데이터 URL에서, 이제 Controller에 자동 전달, Controller는 ViewModel으로 데이터를 패키지 하 고이 보기에 해당 개체를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-183">Now we're taking data from the URL, it's passed into our Controller automatically, our Controller packages up the data into a ViewModel and passes that object onto our View.</span></span> <span data-ttu-id="5c283-184">사용자에 게 데이터를 HTML로 표시 하는 보다 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-184">The View than displays the data as HTML to the user.</span></span>

<span data-ttu-id="5c283-185">[![Windows Internet Explorer-시작](getting-started-with-mvc-part3/_static/image14.png)](getting-started-with-mvc-part3/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="5c283-185">[![Welcome - Windows Internet Explorer](getting-started-with-mvc-part3/_static/image14.png)](getting-started-with-mvc-part3/_static/image13.png)</span></span>

<span data-ttu-id="5c283-186">이 였 종류를 모델에 대 한 "M"의 하지만 데이터베이스 종류 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-186">Well, that was a kind of an "M" for Model, but not the database kind.</span></span> <span data-ttu-id="5c283-187">지금까지 학습 및 기능 영화 데이터베이스를 만들 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5c283-187">Let's take what we've learned and create a database of Movies.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5c283-188">[이전](getting-started-with-mvc-part2.md)
> [다음](getting-started-with-mvc-part4.md)</span><span class="sxs-lookup"><span data-stu-id="5c283-188">[Previous](getting-started-with-mvc-part2.md)
[Next](getting-started-with-mvc-part4.md)</span></span>
