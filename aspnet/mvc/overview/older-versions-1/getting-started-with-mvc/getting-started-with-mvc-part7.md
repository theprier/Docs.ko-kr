---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part7
title: "모델에 유효성 검사 추가 | Microsoft Docs"
author: shanselman
description: "ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 읽기 및 쓰기는 데이터베이스에서 단순 웹 응용 프로그램을 만듭니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/14/2010
ms.topic: article
ms.assetid: aa7b3e8e-e23d-49f1-b160-f99a7f2982bd
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part7
msc.type: authoredcontent
ms.openlocfilehash: 5616c3c3bc77be0a770540d04cc2ae48ba9eedff
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
<a name="adding-validation-to-the-model"></a><span data-ttu-id="c491d-104">모델에 유효성 검사 추가</span><span class="sxs-lookup"><span data-stu-id="c491d-104">Adding Validation to the Model</span></span>
====================
<span data-ttu-id="c491d-105">으로 [Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="c491d-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="c491d-106">ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="c491d-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="c491d-107">읽기 및 쓰기는 데이터베이스에서 단순 웹 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c491d-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="c491d-108">방문는 [ASP.NET MVC 학습 센터](../../../index.md) 자습서 및 예제에는 다른 ASP.NET MVC를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c491d-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>


<span data-ttu-id="c491d-109">이 섹션에서는 하겠습니다 응용 프로그램 내에서 입력된 유효성 검사를 사용 하는 데 필요한 지원을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="c491d-109">In this section we are going to implement the support necessary to enable input validation within our application.</span></span> <span data-ttu-id="c491d-110">म 합니다 확인 데이터베이스 콘텐츠 올바른지 항상 시도 하 고 잘못 된 동영상 데이터를 입력할 때 최종 사용자에 게 유용한 오류 메시지를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c491d-110">We'll ensure that our database content is always correct, and provide helpful error messages to end users when they try and enter Movie data which is not valid.</span></span> <span data-ttu-id="c491d-111">영화 클래스에 유효성 검사 논리를 약간 추가 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c491d-111">We'll begin by adding a little validation logic to the Movie class.</span></span>

<span data-ttu-id="c491d-112">모델 폴더를 마우스 오른쪽 단추로 클릭 하 고 추가 클래스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c491d-112">Right click on the Model folder and select Add Class.</span></span> <span data-ttu-id="c491d-113">영화 클래스를 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c491d-113">Name your class Movie.</span></span>

<span data-ttu-id="c491d-114">앞, 동영상 엔터티 모델에서 만든 동영상 클래스를 IDE 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c491d-114">When we created the Movie Entity Model earlier, the IDE created a Movie class.</span></span> <span data-ttu-id="c491d-115">사실, 영화 클래스의 일부는 한 파일의 다른 파트에 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c491d-115">In fact, part of the Movie class can be in one file and part in another.</span></span> <span data-ttu-id="c491d-116">이 Partial 클래스 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c491d-116">This is called a Partial Class.</span></span> <span data-ttu-id="c491d-117">다른 파일에서 영화 클래스를 확장 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c491d-117">We're going to extend the Movie class from another file.</span></span>

<span data-ttu-id="c491d-118">시스템에 유효성 검사 힌트를 제공 하는 일부 특성을 가진 "버디 클래스"를 가리키는 부분 영화 클래스를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c491d-118">We'll create a partial movie class that points to a "buddy class" with some attributes that will give validation hints to the system.</span></span> <span data-ttu-id="c491d-119">또한 책정할 특정 범위 내 되도록 요구 알아보고 제목과 가격 필수로 표시 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c491d-119">We'll mark the Title and Price as Required, and also insist that the Price be within a certain range.</span></span> <span data-ttu-id="c491d-120">모델 폴더를 마우스 오른쪽 단추로 클릭 하 고 추가 클래스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c491d-120">Right click the Models folder and select Add Class.</span></span> <span data-ttu-id="c491d-121">영화 클래스 이름을 지정 하 고 확인 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c491d-121">Name your class Movie and Click the OK button.</span></span> <span data-ttu-id="c491d-122">이 부분 영화 클래스의 모양은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c491d-122">Here's what our partial Movie class looks like.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part7/samples/sample1.cs)]

<span data-ttu-id="c491d-123">다시 응용 프로그램을 실행 하 고 가격이 100 초과 동영상을 입력 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c491d-123">Re-Run your application and try to enter a movie with a price over 100.</span></span> <span data-ttu-id="c491d-124">오류가 폼을 제출 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c491d-124">You'll get an error after you've submitted the form.</span></span> <span data-ttu-id="c491d-125">오류는 서버 쪽에서 발생 하 고는 폼이 게시 한 후 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="c491d-125">The error is caught on the server side and occurs after the Form is POSTed.</span></span> <span data-ttu-id="c491d-126">ASP.NET MVC의 기본 제공 HTML 도우미 된 오류 메시지를 표시 하 여 textbox 요소 내에서 us에 대 한 값을 유지 관리 방법을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c491d-126">Notice how ASP.NET MVC's built-in HTML helpers were smart enough to display the error message and maintain the values for us within the textbox elements:</span></span>

<span data-ttu-id="c491d-127">[![CreateMovieWithValidation](getting-started-with-mvc-part7/_static/image2.png)](getting-started-with-mvc-part7/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c491d-127">[![CreateMovieWithValidation](getting-started-with-mvc-part7/_static/image2.png)](getting-started-with-mvc-part7/_static/image1.png)</span></span>

<span data-ttu-id="c491d-128">이 방식은 효과적, 이지만 그 좋을 것을 확인할 수 사용자 클라이언트 쪽에서 즉시 전에 서버 관련 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c491d-128">This works great, but it'd be nice if we could tell the user on the client-side, immediately, before the server gets involved.</span></span>

<span data-ttu-id="c491d-129">JavaScript 일부 클라이언트 쪽 유효성 검사가 가능 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c491d-129">Let's enable some client-side validation with JavaScript.</span></span>

## <a name="adding-client-side-validation"></a><span data-ttu-id="c491d-130">클라이언트 쪽 유효성 검사 추가</span><span class="sxs-lookup"><span data-stu-id="c491d-130">Adding Client-Side Validation</span></span>

<span data-ttu-id="c491d-131">영화 클래스에는 일부 유효성 검사 특성에 이미 있으므로 방금 해야 우리의 Create.aspx 보기 서식 파일에 몇 개의 JavaScript 파일을 추가 하 고 수행 되려면 클라이언트 쪽 유효성 검사를 사용 하는 코드 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c491d-131">Since our Movie class already has some validation attributes, we'll just need to add a few JavaScript files to our Create.aspx View template and add a line of code to enable client-side validation to take place.</span></span>

<span data-ttu-id="c491d-132">내에서 VWD 우리의 동영상 보기/폴더를 이동 하 고 Create.aspx를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c491d-132">From within VWD go our Views/Movie folder and open up Create.aspx.</span></span>

<span data-ttu-id="c491d-133">솔루션 탐색기에서 스크립트 폴더를 열고 내에서 다음 세 가지 스크립트를 끌어는 &lt;h e a d&gt; 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="c491d-133">Open up the Scripts folder in the Solution Explorer and drag the following three scripts to within the &lt;head&gt; tag.</span></span>

- <span data-ttu-id="c491d-134">MicrosoftAjax.js</span><span class="sxs-lookup"><span data-stu-id="c491d-134">MicrosoftAjax.js</span></span>
- <span data-ttu-id="c491d-135">MicrosoftMvcValidation.js</span><span class="sxs-lookup"><span data-stu-id="c491d-135">MicrosoftMvcValidation.js</span></span>

<span data-ttu-id="c491d-136">원하는이 순서로 표시 되도록이 스크립트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c491d-136">You want these script files to appear in this order.</span></span>

[!code-html[Main](getting-started-with-mvc-part7/samples/sample2.html)]

<span data-ttu-id="c491d-137">또한는 Html.BeginForm 위에이 한 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c491d-137">Also, add this single line above the Html.BeginForm:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part7/samples/sample3.aspx)]

<span data-ttu-id="c491d-138">IDE 내에서 표시 된 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c491d-138">Here's the code shown within the IDE.</span></span>

<span data-ttu-id="c491d-139">[![동영상-Microsoft Visual 웹 Developer 2010 Express (10)](getting-started-with-mvc-part7/_static/image4.png)](getting-started-with-mvc-part7/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="c491d-139">[![Movies - Microsoft Visual Web Developer 2010 Express (10)](getting-started-with-mvc-part7/_static/image4.png)](getting-started-with-mvc-part7/_static/image3.png)</span></span>

<span data-ttu-id="c491d-140">응용 프로그램을 실행 하 고 /Movies/Create 다시 방문 하 고 데이터를 입력 하지 않고 만들기를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c491d-140">Run your application and visit /Movies/Create again, and click Create without entering any data.</span></span> <span data-ttu-id="c491d-141">오류 메시지가 즉시 표시 데이터 보내기 연관 플래시 페이지 없이 거슬러 올라갑니다 서버에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c491d-141">The error messages appear immediately without the page flash that we associate with sending data all the way back to the server.</span></span> <span data-ttu-id="c491d-142">이 ASP.NET MVC는 이제 한 입력 유효성 검사 둘 다에서 (JavaScript를 사용 하 여) 클라이언트 때문에 서버에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c491d-142">This is because ASP.NET MVC is now validating the input on both the client (using JavaScript) and on the server.</span></span>

<span data-ttu-id="c491d-143">[![만들기-Windows Internet Explorer](getting-started-with-mvc-part7/_static/image6.png)](getting-started-with-mvc-part7/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="c491d-143">[![Create - Windows Internet Explorer](getting-started-with-mvc-part7/_static/image6.png)](getting-started-with-mvc-part7/_static/image5.png)</span></span>

<span data-ttu-id="c491d-144">좋은 볼 됩니다!</span><span class="sxs-lookup"><span data-stu-id="c491d-144">This is looking good!</span></span> <span data-ttu-id="c491d-145">데이터베이스에 추가 열 하나를 지금 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c491d-145">Let's now add one additional column to the database.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="c491d-146">[이전](getting-started-with-mvc-part6.md)
[다음](getting-started-with-mvc-part8.md)</span><span class="sxs-lookup"><span data-stu-id="c491d-146">[Previous](getting-started-with-mvc-part6.md)
[Next](getting-started-with-mvc-part8.md)</span></span>
