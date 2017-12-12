---
uid: mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
title: "마스터 페이지 및 부분을 사용 하 여 UI를 사용 하 여 다시 | Microsoft Docs"
author: microsoft
description: "7 단계 부분 뷰 서식 파일 및 마스터 페이지를 사용 하 여 코드 중복을 제거 하는 보기 템플릿 내에서 ' 건조 원칙 '를 적용할 수 있습니다 하는 방법을 살펴봅니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: d4243a4a-e91c-4116-9ae0-5c08e5285677
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
msc.type: authoredcontent
ms.openlocfilehash: c42cd6aca40b08a9f8461532fbfd0589901b64ad
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="re-use-ui-using-master-pages-and-partials"></a><span data-ttu-id="f9cd1-103">마스터 페이지 및 부분을 사용 하 여 UI를 다시 사용</span><span class="sxs-lookup"><span data-stu-id="f9cd1-103">Re-use UI Using Master Pages and Partials</span></span>
====================
<span data-ttu-id="f9cd1-104">여 [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="f9cd1-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="f9cd1-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="f9cd1-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="f9cd1-106">이 무료의 7 단계 ["업그레이드 되었으며 수정" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 하는 워크 쓰루는 작고 빌드만 ASP.NET MVC 1을 사용 하 여 웹 응용 프로그램을 완료 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-106">This is step 7 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="f9cd1-107">7 단계 부분 뷰 서식 파일 및 마스터 페이지를 사용 하 여 코드 중복을 제거 하는 보기 템플릿 내에서 "건조 원칙"을 적용할 수 있습니다 하는 방법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-107">Step 7 looks at ways we can apply the "DRY Principle" within our view templates to eliminate code duplication, using partial view templates and master pages.</span></span>
> 
> <span data-ttu-id="f9cd1-108">ASP.NET MVC 3을 사용 하는 경우 수행한 것이 좋습니다는 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-step-7-partials-and-master-pages"></a><span data-ttu-id="f9cd1-109">업그레이드 되었으며 수정 단계 7: 부분 및 마스터 페이지</span><span class="sxs-lookup"><span data-stu-id="f9cd1-109">NerdDinner Step 7: Partials and Master Pages</span></span>

<span data-ttu-id="f9cd1-110">ASP.NET MVC 수용 디자인 이론 중 하나 (일반적으로 "드라이" 라고 함) "수행 하지 반복 직접" 원칙입니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-110">One of the design philosophies ASP.NET MVC embraces is the "Do Not Repeat Yourself" principle (commonly referred to as "DRY").</span></span> <span data-ttu-id="f9cd1-111">건조 디자인 코드 및 빌드를 빠르고 쉽게 유지 관리 하는 응용 프로그램에 궁극적으로 낮추는 논리의 복제를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-111">A DRY design helps eliminate the duplication of code and logic, which ultimately makes applications faster to build and easier to maintain.</span></span>

<span data-ttu-id="f9cd1-112">몇 가지 업그레이드 되었으며 수정 시나리오에서 적용 건조 원칙을 이미 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-112">We've already seen the DRY principle applied in several of our NerdDinner scenarios.</span></span> <span data-ttu-id="f9cd1-113">몇 가지 예: 두 편집에서 강제 적용 하 고 컨트롤러; 시나리오를 만들 수 있도록 하는 모델 계층 내에서 유효성 검사 논리 구현 됩니다 편집, 세부 정보 및 Delete 동작 메서드를 통해 다시 사용 "NotFound" 보기 템플릿 규칙-명명 패턴 View() 도우미 메서드를 호출할 때 이름을 명시적으로 지정 하지 않아도 우리의 뷰 템플릿으로 사용 하 여 우리는 다시 사용 하 여 고 DinnerFormViewModel 클래스 모두 편집에 대 한 작업 시나리오를 만들 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-113">A few examples: our validation logic is implemented within our model layer, which enables it to be enforced across both edit and create scenarios in our controller; we are re-using the "NotFound" view template across the Edit, Details and Delete action methods; we are using a convention- naming pattern with our view templates, which eliminates the need to explicitly specify the name when we call the View() helper method; and we are re-using the DinnerFormViewModel class for both Edit and Create action scenarios.</span></span>

<span data-ttu-id="f9cd1-114">이제 방법을 살펴보겠습니다 "건조 원칙"을 적용할 수 있습니다도 없는 코드 중복을 제거 하는 보기 템플릿 내에서.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-114">Let's now look at ways we can apply the "DRY Principle" within our view templates to eliminate code duplication there as well.</span></span>

### <a name="re-visiting-our-edit-and-create-view-templates"></a><span data-ttu-id="f9cd1-115">다시 파악 하 여 편집 및 보기 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="f9cd1-115">Re-visiting our Edit and Create View Templates</span></span>

<span data-ttu-id="f9cd1-116">현재 두 개의 서로 다른 뷰 템플릿 – "Edit.aspx" 및 "Create.aspx" – Dinner 폼 UI를 표시 하려면 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-116">Currently we are using two different view templates – "Edit.aspx" and "Create.aspx" – to display our Dinner form UI.</span></span> <span data-ttu-id="f9cd1-117">그중에서 빠르게 시각적 비교는 얼마나 비슷한지 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-117">A quick visual comparison of them highlights how similar they are.</span></span> <span data-ttu-id="f9cd1-118">다음은 폼 만들기의 모양을입니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-118">Below is what the create form looks like:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image1.png)

<span data-ttu-id="f9cd1-119">및 "편집" 폼의 모양은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-119">And here is what our "Edit" form looks like:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image2.png)

<span data-ttu-id="f9cd1-120">큰 차이 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="f9cd1-120">Not much of a difference is there?</span></span> <span data-ttu-id="f9cd1-121">제목 및 머리글 텍스트 이외의 폼 레이아웃 및 입력 컨트롤은 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-121">Other than the title and header text, the form layout and input controls are identical.</span></span>

<span data-ttu-id="f9cd1-122">템플릿 보기 소요 됩니다 "Edit.aspx" 및 "Create.aspx"를 열고에서는 동일한 폼 레이아웃 및 입력 제어 코드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-122">If we open up the "Edit.aspx" and "Create.aspx" view templates we'll find that they contain identical form layout and input control code.</span></span> <span data-ttu-id="f9cd1-123">이러한 중복 두 번 소개 우리 하거나 적합 하지 않습니다 새 Dinner 속성-변경로 인해 변경 하지 정리할 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-123">This duplication means we end up having to make changes twice anytime we introduce or change a new Dinner property - which is not good.</span></span>

### <a name="using-partial-view-templates"></a><span data-ttu-id="f9cd1-124">부분 뷰 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="f9cd1-124">Using Partial View Templates</span></span>

<span data-ttu-id="f9cd1-125">ASP.NET MVC 페이지의 하위 부분 뷰 렌더링 논리를 캡슐화 하는 데 사용할 수 있는 "부분 뷰" 템플릿을 정의 하는 기능을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-125">ASP.NET MVC supports the ability to define "partial view" templates that can be used to encapsulate view rendering logic for a sub-portion of a page.</span></span> <span data-ttu-id="f9cd1-126">뷰 렌더링 논리를 한 번 정의 하는 유용한 방법을 제공 하 고 다시 사용 될 여러 위치에서 응용 프로그램 간에 하는 "부분".</span><span class="sxs-lookup"><span data-stu-id="f9cd1-126">"Partials" provide a useful way to define view rendering logic once, and then re-use it in multiple places across an application.</span></span>

<span data-ttu-id="f9cd1-127">"드라이" 우리의 Edit.aspx 및 Create.aspx 보기 템플릿 복제를 위해 폼 레이아웃 및 둘 다에 공통 되는 입력된 요소를 캡슐화 하는 "DinnerForm.ascx" 라는 부분 뷰 템플릿을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-127">To help "DRY-up" our Edit.aspx and Create.aspx view template duplication, we can create a partial view template named "DinnerForm.ascx" that encapsulates the form layout and input elements common to both.</span></span> <span data-ttu-id="f9cd1-128">우리의/뷰/Dinners 디렉터리를 마우스 오른쪽 단추로 클릭 하 고 선택 하 여 수행 됩니다는 "추가-&gt;보기" 메뉴 명령:</span><span class="sxs-lookup"><span data-stu-id="f9cd1-128">We'll do this by right-clicking on our /Views/Dinners directory and choosing the "Add-&gt;View" menu command:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image3.png)

<span data-ttu-id="f9cd1-129">이 "뷰 추가" 대화 상자를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-129">This will display the "Add View" dialog.</span></span> <span data-ttu-id="f9cd1-130">이름을 새 보기를 만드는 "DinnerForm", "부분 뷰 만들기" 대화 상자에서 확인란을 선택 하 고는 통과 됩니다 것 DinnerFormViewModel 클래스를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-130">We'll name the new view we want to create "DinnerForm", select the "Create a partial view" checkbox within the dialog, and indicate that we will pass it a DinnerFormViewModel class:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image4.png)

<span data-ttu-id="f9cd1-131">"추가" 단추를 클릭 하면 Visual Studio에서는 us에 대 한 새 "DinnerForm.ascx" 보기 템플릿을 "\Views\Dinners" 디렉터리 내에서 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-131">When we click the "Add" button, Visual Studio will create a new "DinnerForm.ascx" view template for us within the "\Views\Dinners" directory.</span></span>

<span data-ttu-id="f9cd1-132">म 수 다음 복사/붙여넣기 중복 폼 레이아웃 / 우리의 새 "DinnerForm.ascx" 부분 뷰 템플릿으로 우리의 Edit.aspx/ Create.aspx 보기 템플릿에서 제어 코드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-132">We can then copy/paste the duplicate form layout / input control code from our Edit.aspx/ Create.aspx view templates into our new "DinnerForm.ascx" partial view template:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample1.aspx)]

<span data-ttu-id="f9cd1-133">그런 다음이 편집 및 Create 템플릿 보기 DinnerForm 부분 서식 파일을 호출 하 고 중복 제거 하 여 폼을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-133">We can then update our Edit and Create view templates to call the DinnerForm partial template and eliminate the form duplication.</span></span> <span data-ttu-id="f9cd1-134">우리의 보기 템플릿 내 Html.RenderPartial("DinnerForm") 호출 하 여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-134">We can do this by calling Html.RenderPartial("DinnerForm") within our view templates:</span></span>

##### <a name="createaspx"></a><span data-ttu-id="f9cd1-135">Create.aspx</span><span class="sxs-lookup"><span data-stu-id="f9cd1-135">Create.aspx</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample2.aspx)]

##### <a name="editaspx"></a><span data-ttu-id="f9cd1-136">Edit.aspx</span><span class="sxs-lookup"><span data-stu-id="f9cd1-136">Edit.aspx</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample3.aspx)]

<span data-ttu-id="f9cd1-137">Html.RenderPartial를 호출할 때 원하는 부분 서식 파일의 경로 명시적으로 한정할 수 있습니다 (예: ~ Views/Dinners/DinnerForm.ascx ").</span><span class="sxs-lookup"><span data-stu-id="f9cd1-137">You can explicitly qualify the path of the partial template you want when calling Html.RenderPartial (for example: ~Views/Dinners/DinnerForm.ascx").</span></span> <span data-ttu-id="f9cd1-138">위의 코드에서 하지만 내 ASP.NET MVC에서 규칙 기반 명명 패턴을 활용 하기 위해 했으며 "DinnerForm" 렌더링할 부분 이름으로 지정 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-138">In our code above, though, we are taking advantage of the convention-based naming pattern within ASP.NET MVC, and just specifying "DinnerForm" as the name of the partial to render.</span></span> <span data-ttu-id="f9cd1-139">이 작업을 수행 하는 경우 ASP.NET MVC는 검색 규칙 기반 views 디렉터리의 첫 번째 (DinnersController/뷰/Dinners 것) 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-139">When we do this ASP.NET MVC will look first in the convention-based views directory (for DinnersController this would be /Views/Dinners).</span></span> <span data-ttu-id="f9cd1-140">부분 서식 파일을 찾지 못하는 경우 있습니다를 다음 찾습니다 것 /Views/Shared 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-140">If it doesn't find the partial template there it will then look for it in the /Views/Shared directory.</span></span>

<span data-ttu-id="f9cd1-141">Html.RenderPartial() 부분 뷰의 이름으로 호출 되 면 ASP.NET MVC에서 호출 뷰 템플릿이 사용 되는 동일한 모델 및 ViewData 사전 개체 부분 뷰로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-141">When Html.RenderPartial() is called with just the name of the partial view, ASP.NET MVC will pass to the partial view the same Model and ViewData dictionary objects used by the calling view template.</span></span> <span data-ttu-id="f9cd1-142">또는 대체 모델 개체 및/또는 부분 뷰를 인덱싱하지에 대 한 사전은 전달할 수 있도록 하는 오버 로드 된 버전의 Html.RenderPartial() 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-142">Alternatively, there are overloaded versions of Html.RenderPartial() that enable you to pass an alternate Model object and/or ViewData dictionary for the partial view to use.</span></span> <span data-ttu-id="f9cd1-143">만을 저장할 전체 모델/ViewModel의 하위 집합을 전달 하는 시나리오에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-143">This is useful for scenarios where you only want to pass a subset of the full Model/ViewModel.</span></span>

| <span data-ttu-id="f9cd1-144">**쪽 주제: 이유 &lt;% %&gt; 대신 &lt;% = %&gt;?**</span><span class="sxs-lookup"><span data-stu-id="f9cd1-144">**Side Topic: Why &lt;% %&gt; instead of &lt;%= %&gt;?**</span></span> |
| --- |
| <span data-ttu-id="f9cd1-145">사용 함을 위의 코드와 함께 보았을 것 미묘한 작업 중 하나는 &lt;% %&gt; 대신 차단는 &lt;% = %&gt; Html.RenderPartial()를 호출할 때 차단 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-145">One of the subtle things you might have noticed with the code above is that we are using a &lt;% %&gt; block instead of a &lt;%= %&gt; block when calling Html.RenderPartial().</span></span> <span data-ttu-id="f9cd1-146">&lt;% = %&gt; 블록 ASP.NET에서 개발자가 지정된 된 값을 렌더링 하려고 나타냅니다 (예: &lt;% = "Hello" %&gt; "Hello" 하 게 렌더링).</span><span class="sxs-lookup"><span data-stu-id="f9cd1-146">&lt;%= %&gt; blocks in ASP.NET indicate that a developer wants to render a specified value (for example: &lt;%= "Hello" %&gt; would render "Hello").</span></span> <span data-ttu-id="f9cd1-147">&lt;% %&gt; 블록 코드를 실행 하려는 개발자 및 그 안에 포함 하는 출력을 렌더링 된 어떠한 이루어져야 합니다. 명시적으로 나타냅니다 (예: &lt;% Response.Write("Hello") %&gt;합니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-147">&lt;% %&gt; blocks instead indicate that the developer wants to execute code, and that any rendered output within them must be done explicitly (for example: &lt;% Response.Write("Hello") %&gt;.</span></span> <span data-ttu-id="f9cd1-148">사용 하는 이유는 &lt;% %&gt; 위의 우리의 Html.RenderPartial 코드와 함께 블록은 Html.RenderPartial() 메서드는 문자열을 반환 하 고 대신 호출 템플릿 보기에 직접 콘텐츠를 스트림의 출력을 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-148">The reason we are using a &lt;% %&gt; block with our Html.RenderPartial code above is because the Html.RenderPartial() method doesn't return a string, and instead outputs the content directly to the calling view template's output stream.</span></span> <span data-ttu-id="f9cd1-149">성능상의 이유로 효율성 및 (잠재적으로 매우 큰) 임시 문자열 개체를 만들지 않아도 되므로 수행 하 여 이렇게 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-149">It does this for performance efficiency reasons, and by doing so it avoids the need to create a (potentially very large) temporary string object.</span></span> <span data-ttu-id="f9cd1-150">이 메모리 사용을 줄이고 전반적인 응용 프로그램 처리량을 향상 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-150">This reduces memory usage and improves overall application throughput.</span></span> <span data-ttu-id="f9cd1-151">Html.RenderPartial()을 사용 하는 내에 없을 때 호출의 끝에 세미콜론을 추가 하는 경우 한 가지 일반적인 실수는 &lt;% %&gt; 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-151">One common mistake when using Html.RenderPartial() is to forget to add a semi-colon at the end of the call when it is within a &lt;% %&gt; block.</span></span> <span data-ttu-id="f9cd1-152">예를 들어이 코드는 컴파일러 오류 하면: &lt;% Html.RenderPartial("DinnerForm") %&gt; 작성 해야 하는 대신: &lt;%Html.RenderPartial("DinnerForm"); %&gt; 때문에 이것이 &lt;% %&gt; 블록은 자체 포함 된 코드 문을 때 및 C# 코드 문은 세미콜론으로 종료 해야 할를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-152">For example, this code will cause a compiler error: &lt;% Html.RenderPartial("DinnerForm") %&gt; You instead need to write: &lt;% Html.RenderPartial("DinnerForm"); %&gt; This is because &lt;% %&gt; blocks are self-contained code statements, and when using C# code statements need to be terminated with a semi-colon.</span></span> |

### <a name="using-partial-view-templates-to-clarify-code"></a><span data-ttu-id="f9cd1-153">부분 뷰 템플릿을 사용 하 여 코드를 명확 하 게</span><span class="sxs-lookup"><span data-stu-id="f9cd1-153">Using Partial View Templates to Clarify Code</span></span>

<span data-ttu-id="f9cd1-154">여러 위치에서 뷰 렌더링 논리 중복 되지 않도록 하려면 "DinnerForm" 부분 뷰 템플릿을 만들었는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-154">We created the "DinnerForm" partial view template to avoid duplicating view rendering logic in multiple places.</span></span> <span data-ttu-id="f9cd1-155">부분 뷰 템플릿을 만들 수는 가장 일반적인 이유입니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-155">This is the most common reason to create partial view templates.</span></span>

<span data-ttu-id="f9cd1-156">경우에 따라 여전히 이렇게 하면 부분 뷰를 한 곳에만 호출 되는 경우에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-156">Sometimes it still makes sense to create partial views even when they are only being called in a single place.</span></span> <span data-ttu-id="f9cd1-157">매우 복잡 한 뷰 템플릿 종종 뷰 렌더링 논리 추출 하 고 하나에 분할 또는 부분 서식 파일을 이름이 더 잘 읽을 하기가 훨씬 커질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-157">Very complicated view templates can often become much easier to read when their view rendering logic is extracted and partitioned into one or more well named partial templates.</span></span>

<span data-ttu-id="f9cd1-158">예를 들어는 아래 코드 조각 (있음 살펴볼 것에 곧) 프로젝트에는 Site.master 파일에서입니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-158">For example, consider the below code-snippet from the Site.master file in our project (which we will be looking at shortly).</span></span> <span data-ttu-id="f9cd1-159">코드는 비교적 간단 읽을 – 로그인/로그 아웃을 표시 하는 논리를 위쪽에 링크 있기 때문에 화면 오른쪽 "LogOnUserControl" 부분 내에서 캡슐화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-159">The code is relatively straight-forward to read – partly because the logic to display a login/logout link at the top right of the screen is encapsulated within the "LogOnUserControl" partial:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample4.aspx)]

<span data-ttu-id="f9cd1-160">혼란 사용자 자신이 때마다 템플릿 보기 내에서 태그를 html/코드를 이해, 여부 추출 되 고 잘 명명 된 부분 뷰도 리팩터링 되는데이 중 일부 하면 분명히 알 수 없게 하는 것이 좋습니다. 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-160">Whenever you find yourself getting confused trying to understand the html/code markup within a view-template, consider whether it wouldn't be clearer if some of it was extracted and refactored into well-named partial views.</span></span>

### <a name="master-pages"></a><span data-ttu-id="f9cd1-161">마스터 페이지</span><span class="sxs-lookup"><span data-stu-id="f9cd1-161">Master Pages</span></span>

<span data-ttu-id="f9cd1-162">부분 뷰를 지원할 뿐 아니라 ASP.NET MVC도 일반적인 레이아웃 및 사이트의 최상위 html을 정의 하는 데 사용할 수 있는 "마스터 페이지" 템플릿을 만들 수 있는 기능을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-162">In addition to supporting partial views, ASP.NET MVC also supports the ability to create "master page" templates that can be used to define the common layout and top-level html of a site.</span></span> <span data-ttu-id="f9cd1-163">콘텐츠 자리 표시자 컨트롤 "" 의해 채워진 뷰 또는 재정의 될 수 있는 대체 가능 영역을 식별 하는 마스터 페이지에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-163">Content placeholder controls can then be added to the master page to identify replaceable regions that can be overridden or "filled in" by views.</span></span> <span data-ttu-id="f9cd1-164">이 응용 프로그램에 걸쳐 공통 레이아웃을 적용 하는 매우 효과적인 (및 건조) 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-164">This provides a very effective (and DRY) way to apply a common layout across an application.</span></span>

<span data-ttu-id="f9cd1-165">기본적으로 새 ASP.NET MVC 프로젝트에 자동으로 추가 하는 마스터 페이지 서식 파일을가지고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-165">By default, new ASP.NET MVC projects have a master page template automatically added to them.</span></span> <span data-ttu-id="f9cd1-166">이 마스터 페이지에는 "Site.master" 및 생활 \Views\Shared\ 폴더 내에서 이름이 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-166">This master page is named "Site.master" and lives within the \Views\Shared\ folder:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image5.png)

<span data-ttu-id="f9cd1-167">기본 Site.master 파일은 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-167">The default Site.master file looks like below.</span></span> <span data-ttu-id="f9cd1-168">위쪽 탐색을 위한 메뉴와 함께 사이트의 외부 html을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-168">It defines the outer html of the site, along with a menu for navigation at the top.</span></span> <span data-ttu-id="f9cd1-169">제목, 용이고 다른 페이지의 기본 콘텐츠 바꿔야에 대 한 두 개의 대체 가능 콘텐츠 자리 표시자 컨트롤-포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-169">It contains two replaceable content placeholder controls – one for the title, and the other for where the primary content of a page should be replaced:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample5.aspx)]

<span data-ttu-id="f9cd1-170">업그레이드 되었으며 수정 응용 프로그램 ("List", "Details", "편집", "만들기", "NotFound" 등)에 대 한 만들었습니다 템플릿 보기의 모든 토대로이 Site.master 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-170">All of the view templates we've created for our NerdDinner application ("List", "Details", "Edit", "Create", "NotFound", etc) have been based on this Site.master template.</span></span> <span data-ttu-id="f9cd1-171">이 기본적으로 위쪽에 추가 된 "MasterPageFile" 특성을 통해 표시 &lt;% 페이지 % @&gt; 지시문 "뷰 추가" 대화 상자를 사용 하 여이 뷰를 만들 때:</span><span class="sxs-lookup"><span data-stu-id="f9cd1-171">This is indicated via the "MasterPageFile" attribute that was added by default to the top &lt;% @ Page %&gt; directive when we created our views using the "Add View" dialog:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample6.aspx)]

<span data-ttu-id="f9cd1-172">따라서 Site.master 콘텐츠를 변경할 수 있습니다 및가 변경 내용을 자동으로 적용 하 고 사용할 म 우리의 보기 템플릿 중 하나를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-172">What this means is that we can change the Site.master content, and have the changes automatically be applied and used when we render any of our view templates.</span></span>

<span data-ttu-id="f9cd1-173">응용 프로그램의 머리글은 "내 MVC 응용 프로그램" 대신 "업그레이드 되었으며 수정" 되도록 우리의 Site.master 헤더 섹션을 업데이트 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-173">Let's update our Site.master's header section so that the header of our application is "NerdDinner" instead of "My MVC Application".</span></span> <span data-ttu-id="f9cd1-174">보겠습니다도 업데이트 우리의 탐색 메뉴 첫 번째 탭이 "찾을 정도 Dinner" (HomeController의 index () 동작 메서드에서 처리), 되 고 "호스트 정도 Dinner" (DinnersController의 create () 동작 메서드에서 처리) 이라고 하는 새 탭을 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-174">Let's also update our navigation menu so that the first tab is "Find a Dinner" (handled by the HomeController's Index() action method), and let's add a new tab called "Host a Dinner" (handled by the DinnersController's Create() action method):</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample7.aspx)]

<span data-ttu-id="f9cd1-175">Site.master 파일 및 새로 고침을 저장 하는 경우이 헤더를 보면 브라우저 표시 응용 프로그램 내에서 모든 뷰에 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-175">When we save the Site.master file and refresh our browser we'll see our header changes show up across all views within our application.</span></span> <span data-ttu-id="f9cd1-176">예:</span><span class="sxs-lookup"><span data-stu-id="f9cd1-176">For example:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image6.png)

<span data-ttu-id="f9cd1-177">와 */Dinners/편집 / [id]* URL:</span><span class="sxs-lookup"><span data-stu-id="f9cd1-177">And with the */Dinners/Edit/[id]* URL:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image7.png)

### <a name="next-step"></a><span data-ttu-id="f9cd1-178">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f9cd1-178">Next Step</span></span>

<span data-ttu-id="f9cd1-179">부분 및 마스터 페이지 보기를 완전히 구성 수 있도록 하는 매우 유연한 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-179">Partials and master pages provide very flexible options that enable you to cleanly organize views.</span></span> <span data-ttu-id="f9cd1-180">도움말 보기 중복을 피하기 위해 콘텐츠 / 코드, 고 있다고 보기 템플릿을 보다 쉽게 읽고 유지 관리할 수 있도록를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-180">You'll find that they help you avoid duplicating view content/ code, and make your view templates easier to read and maintain.</span></span>

<span data-ttu-id="f9cd1-181">보겠습니다 이제 앞에서 만든 목록 시나리오를 다시 확인 하 고 확장 가능한 페이징 지원을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9cd1-181">Let's now revisit the listing scenario we built earlier and enable scalable paging support.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="f9cd1-182">[이전](use-viewdata-and-implement-viewmodel-classes.md)
[다음](implement-efficient-data-paging.md)</span><span class="sxs-lookup"><span data-stu-id="f9cd1-182">[Previous](use-viewdata-and-implement-viewmodel-classes.md)
[Next](implement-efficient-data-paging.md)</span></span>
