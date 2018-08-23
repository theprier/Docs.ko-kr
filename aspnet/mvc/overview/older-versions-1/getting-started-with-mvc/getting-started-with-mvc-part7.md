---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part7
title: 모델에 유효성 검사 추가 | Microsoft Docs
author: shanselman
description: ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 읽기 및 쓰기 데이터베이스에서 간단한 웹 응용 프로그램을 만듭니다.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: aa7b3e8e-e23d-49f1-b160-f99a7f2982bd
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part7
msc.type: authoredcontent
ms.openlocfilehash: 4c7867587ba0610f0f1c23d9a0b9fbdc4040de7c
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41829789"
---
<a name="adding-validation-to-the-model"></a><span data-ttu-id="69c14-104">모델에 유효성 검사 추가</span><span class="sxs-lookup"><span data-stu-id="69c14-104">Adding Validation to the Model</span></span>
====================
<span data-ttu-id="69c14-105">[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="69c14-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="69c14-106">ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="69c14-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="69c14-107">읽기 및 쓰기 데이터베이스는 간단한 웹 응용 프로그램을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c14-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="69c14-108">방문 합니다 [ASP.NET MVC 학습 센터](../../../index.md) 자습서 및 샘플 다른 ASP.NET MVC를 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c14-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>


<span data-ttu-id="69c14-109">이 섹션의 응용 프로그램 내에서 입력된 유효성 검사를 사용 하도록 설정 하는 데 필요한 지원을 구현 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c14-109">In this section we are going to implement the support necessary to enable input validation within our application.</span></span> <span data-ttu-id="69c14-110">협력 수는 데이터베이스 콘텐츠 항상 정확 하 고 시도 하 고 잘못 된 영화 데이터를 입력할 때 최종 사용자에 게 유용한 오류 메시지를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c14-110">We'll ensure that our database content is always correct, and provide helpful error messages to end users when they try and enter Movie data which is not valid.</span></span> <span data-ttu-id="69c14-111">영화 클래스에 약간의 유효성 검사 논리를 추가 하 여 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c14-111">We'll begin by adding a little validation logic to the Movie class.</span></span>

<span data-ttu-id="69c14-112">모델 폴더를 마우스 오른쪽 단추로 클릭 하 고 추가 클래스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c14-112">Right click on the Model folder and select Add Class.</span></span> <span data-ttu-id="69c14-113">영화 클래스를 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c14-113">Name your class Movie.</span></span>

<span data-ttu-id="69c14-114">영화 엔터티 모델을 앞서 만든 경우 IDE는 영화 클래스를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="69c14-114">When we created the Movie Entity Model earlier, the IDE created a Movie class.</span></span> <span data-ttu-id="69c14-115">사실 영화 클래스의 일부는 하나의 파일의 다른 부분에 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c14-115">In fact, part of the Movie class can be in one file and part in another.</span></span> <span data-ttu-id="69c14-116">이 Partial 클래스 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c14-116">This is called a Partial Class.</span></span> <span data-ttu-id="69c14-117">다른 파일에서 영화 클래스를 확장 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="69c14-117">We're going to extend the Movie class from another file.</span></span>

<span data-ttu-id="69c14-118">만들어 부분 영화 클래스를 가리키는 "버디 클래스" 시스템 유효성 검사 힌트를 제공 하는 일부 특성을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c14-118">We'll create a partial movie class that points to a "buddy class" with some attributes that will give validation hints to the system.</span></span> <span data-ttu-id="69c14-119">제목 및 필수로 가격을 표시 하 고 특정 범위 내에 가격 되도록를 허용할지도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c14-119">We'll mark the Title and Price as Required, and also insist that the Price be within a certain range.</span></span> <span data-ttu-id="69c14-120">Models 폴더를 마우스 오른쪽 단추로 클릭 하 고 추가 클래스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c14-120">Right click the Models folder and select Add Class.</span></span> <span data-ttu-id="69c14-121">영화 클래스 이름과 확인 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c14-121">Name your class Movie and Click the OK button.</span></span> <span data-ttu-id="69c14-122">이 부분 영화 클래스의 모양은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="69c14-122">Here's what our partial Movie class looks like.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part7/samples/sample1.cs)]

<span data-ttu-id="69c14-123">응용 프로그램을 다시 실행 하 고 100 초과 하 여 가격을 사용 하 여 영화를 입력 해 보세요.</span><span class="sxs-lookup"><span data-stu-id="69c14-123">Re-Run your application and try to enter a movie with a price over 100.</span></span> <span data-ttu-id="69c14-124">폼을 제출 하 고 나면 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c14-124">You'll get an error after you've submitted the form.</span></span> <span data-ttu-id="69c14-125">오류는 서버 쪽에서 포착 되 및에 폼이 게시 한 후에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c14-125">The error is caught on the server side and occurs after the Form is POSTed.</span></span> <span data-ttu-id="69c14-126">ASP.NET MVC의 기본 제공 HTML 도우미 된 오류 메시지를 표시 하 고 텍스트 상자 요소 내에 값을 유지 하는 방법을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c14-126">Notice how ASP.NET MVC's built-in HTML helpers were smart enough to display the error message and maintain the values for us within the textbox elements:</span></span>

<span data-ttu-id="69c14-127">[![CreateMovieWithValidation](getting-started-with-mvc-part7/_static/image2.png)](getting-started-with-mvc-part7/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="69c14-127">[![CreateMovieWithValidation](getting-started-with-mvc-part7/_static/image2.png)](getting-started-with-mvc-part7/_static/image1.png)</span></span>

<span data-ttu-id="69c14-128">이 작동 하지만 좋을 수 알려줍니다 사용자 클라이언트 쪽에서 즉시 전에 서버 관련 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c14-128">This works great, but it'd be nice if we could tell the user on the client-side, immediately, before the server gets involved.</span></span>

<span data-ttu-id="69c14-129">JavaScript 사용 하 여 일부 클라이언트 쪽 유효성 검사를 사용 하도록 설정 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="69c14-129">Let's enable some client-side validation with JavaScript.</span></span>

## <a name="adding-client-side-validation"></a><span data-ttu-id="69c14-130">클라이언트 쪽 유효성 검사 추가</span><span class="sxs-lookup"><span data-stu-id="69c14-130">Adding Client-Side Validation</span></span>

<span data-ttu-id="69c14-131">영화 클래스에는 이미 일부 유효성 검사 특성에, 하므로 방금 해야 Create.aspx 보기 템플릿은에 몇 가지 JavaScript 파일을 추가 하 고 수행 하는 클라이언트 쪽 유효성 검사를 사용 하도록 설정 하려면 코드 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c14-131">Since our Movie class already has some validation attributes, we'll just need to add a few JavaScript files to our Create.aspx View template and add a line of code to enable client-side validation to take place.</span></span>

<span data-ttu-id="69c14-132">내에서 VWD 우리의 보기/영화 폴더를 이동 하 고 Create.aspx를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="69c14-132">From within VWD go our Views/Movie folder and open up Create.aspx.</span></span>

<span data-ttu-id="69c14-133">솔루션 탐색기의 스크립트 폴더를 열고 내에서 다음 세 가지 스크립트를 끌어 합니다 &lt;head&gt; 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="69c14-133">Open up the Scripts folder in the Solution Explorer and drag the following three scripts to within the &lt;head&gt; tag.</span></span>

- <span data-ttu-id="69c14-134">MicrosoftAjax.js</span><span class="sxs-lookup"><span data-stu-id="69c14-134">MicrosoftAjax.js</span></span>
- <span data-ttu-id="69c14-135">MicrosoftMvcValidation.js</span><span class="sxs-lookup"><span data-stu-id="69c14-135">MicrosoftMvcValidation.js</span></span>

<span data-ttu-id="69c14-136">이 스크립트 파일이 순서로 표시 되도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c14-136">You want these script files to appear in this order.</span></span>

[!code-html[Main](getting-started-with-mvc-part7/samples/sample2.html)]

<span data-ttu-id="69c14-137">또한는 Html.BeginForm 위에이 한 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c14-137">Also, add this single line above the Html.BeginForm:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part7/samples/sample3.aspx)]

<span data-ttu-id="69c14-138">IDE 내에서 표시 된 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="69c14-138">Here's the code shown within the IDE.</span></span>

<span data-ttu-id="69c14-139">[![동영상-Microsoft Visual Web Developer 2010 Express (10)](getting-started-with-mvc-part7/_static/image4.png)](getting-started-with-mvc-part7/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="69c14-139">[![Movies - Microsoft Visual Web Developer 2010 Express (10)](getting-started-with-mvc-part7/_static/image4.png)](getting-started-with-mvc-part7/_static/image3.png)</span></span>

<span data-ttu-id="69c14-140">응용 프로그램을 실행 하 고 /Movies/Create를 다시 방문 하 고 모든 데이터를 입력 하지 않고 만들기를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c14-140">Run your application and visit /Movies/Create again, and click Create without entering any data.</span></span> <span data-ttu-id="69c14-141">오류 메시지를 즉시 표시 데이터를 보내는 연관 플래시 페이지 없이 거슬러 올라갑니다 서버.</span><span class="sxs-lookup"><span data-stu-id="69c14-141">The error messages appear immediately without the page flash that we associate with sending data all the way back to the server.</span></span> <span data-ttu-id="69c14-142">이 ASP.NET MVC는 이제 유효성 검사 모두에 있는 입력 (JavaScript를 사용 하 여) 때문에 서버에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c14-142">This is because ASP.NET MVC is now validating the input on both the client (using JavaScript) and on the server.</span></span>

<span data-ttu-id="69c14-143">[![만들기-Windows Internet Explorer](getting-started-with-mvc-part7/_static/image6.png)](getting-started-with-mvc-part7/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="69c14-143">[![Create - Windows Internet Explorer](getting-started-with-mvc-part7/_static/image6.png)](getting-started-with-mvc-part7/_static/image5.png)</span></span>

<span data-ttu-id="69c14-144">올바른 상태입니다!</span><span class="sxs-lookup"><span data-stu-id="69c14-144">This is looking good!</span></span> <span data-ttu-id="69c14-145">데이터베이스에 추가 열이 하나를 지금 추가 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="69c14-145">Let's now add one additional column to the database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="69c14-146">[이전](getting-started-with-mvc-part6.md)
> [다음](getting-started-with-mvc-part8.md)</span><span class="sxs-lookup"><span data-stu-id="69c14-146">[Previous](getting-started-with-mvc-part6.md)
[Next](getting-started-with-mvc-part8.md)</span></span>
