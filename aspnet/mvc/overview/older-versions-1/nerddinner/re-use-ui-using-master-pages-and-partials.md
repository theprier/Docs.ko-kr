---
uid: mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
title: 마스터 페이지 및 부분을 사용 하 여 UI를 다시 사용할 | Microsoft Docs
author: microsoft
description: 7 단계 템플릿 부분 보기 및 마스터 페이지를 사용 하 여, 코드 중복을 제거 하는 보기 템플릿 내에서 ' 반복 금지 원칙의 ' 적용할 수 있습니다 하는 방법에 살펴봅니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: d4243a4a-e91c-4116-9ae0-5c08e5285677
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
msc.type: authoredcontent
ms.openlocfilehash: f96d3f3059a442f977d4422797c872b865a55695
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37391433"
---
<a name="re-use-ui-using-master-pages-and-partials"></a><span data-ttu-id="17379-103">마스터 페이지 및 부분을 사용 하 여 UI를 다시 사용</span><span class="sxs-lookup"><span data-stu-id="17379-103">Re-use UI Using Master Pages and Partials</span></span>
====================
<span data-ttu-id="17379-104">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="17379-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="17379-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="17379-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="17379-106">이 무료의 7 단계 ["NerdDinner" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 는 안내를 통한 작은 빌드 하지만 ASP.NET MVC 1을 사용 하 여 웹 응용 프로그램을 완료 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="17379-106">This is step 7 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="17379-107">7 단계 템플릿 부분 보기 및 마스터 페이지를 사용 하 여, 코드 중복을 제거 하는 보기 템플릿 내에서 "반복 금지 원칙의" 적용할 수 있습니다 하는 방법에 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="17379-107">Step 7 looks at ways we can apply the "DRY Principle" within our view templates to eliminate code duplication, using partial view templates and master pages.</span></span>
> 
> <span data-ttu-id="17379-108">ASP.NET MVC 3을 사용 하는 경우 수행 하는 것이 좋습니다 합니다 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 하거나 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="17379-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-step-7-partials-and-master-pages"></a><span data-ttu-id="17379-109">NerdDinner 단계 7: 부분 및 마스터 페이지</span><span class="sxs-lookup"><span data-stu-id="17379-109">NerdDinner Step 7: Partials and Master Pages</span></span>

<span data-ttu-id="17379-110">ASP.NET MVC는 수용 디자인 원칙 중 하나는 "수행 하지 반복 금지" 원칙 ("시험" 라고 함)입니다.</span><span class="sxs-lookup"><span data-stu-id="17379-110">One of the design philosophies ASP.NET MVC embraces is the "Do Not Repeat Yourself" principle (commonly referred to as "DRY").</span></span> <span data-ttu-id="17379-111">DRY 디자인 코드와는 궁극적으로 빌드를 빠르고 쉽게 유지 관리 하는 응용 프로그램 논리의 중복을 제거 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17379-111">A DRY design helps eliminate the duplication of code and logic, which ultimately makes applications faster to build and easier to maintain.</span></span>

<span data-ttu-id="17379-112">NerdDinner 시나리오의 몇 가지 적용 반복 금지 원칙의 이미 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="17379-112">We've already seen the DRY principle applied in several of our NerdDinner scenarios.</span></span> <span data-ttu-id="17379-113">몇 가지 예: 유효성 검사 논리는 컨트롤러;에서 시나리오를 만들고 편집에서 적용할 수 있도록 하는 모델 계층 내에서 구현 됩니다 편집, 세부 정보 및 삭제 작업 메서드를 통해 다시 사용 "NotFound" 보기 템플릿 View() 도우미 메서드를 호출할 때 이름을 명시적으로 지정 하지 않아도 되는 뷰 템플릿을 사용 하 여 규칙-명명 패턴을 사용 하는 것 및는 다시 편집에 대 한 DinnerFormViewModel 클래스를 사용 하 고 작업 시나리오를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="17379-113">A few examples: our validation logic is implemented within our model layer, which enables it to be enforced across both edit and create scenarios in our controller; we are re-using the "NotFound" view template across the Edit, Details and Delete action methods; we are using a convention- naming pattern with our view templates, which eliminates the need to explicitly specify the name when we call the View() helper method; and we are re-using the DinnerFormViewModel class for both Edit and Create action scenarios.</span></span>

<span data-ttu-id="17379-114">이제 방법을 살펴보겠습니다 "반복 금지 원칙의" 적용할 수 있습니다도 있습니다 코드 중복을 제거 하는 보기 템플릿 내에서.</span><span class="sxs-lookup"><span data-stu-id="17379-114">Let's now look at ways we can apply the "DRY Principle" within our view templates to eliminate code duplication there as well.</span></span>

### <a name="re-visiting-our-edit-and-create-view-templates"></a><span data-ttu-id="17379-115">다시 방문 하 여 편집 및 보기 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="17379-115">Re-visiting our Edit and Create View Templates</span></span>

<span data-ttu-id="17379-116">현재 Dinner 폼 UI를 표시할 두 개의 서로 다른 뷰 템플릿 – "Edit.aspx" 및 "Create.aspx" –를 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="17379-116">Currently we are using two different view templates – "Edit.aspx" and "Create.aspx" – to display our Dinner form UI.</span></span> <span data-ttu-id="17379-117">이러한 빠른 visual 비교는 얼마나 유사한 지 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="17379-117">A quick visual comparison of them highlights how similar they are.</span></span> <span data-ttu-id="17379-118">만들기 폼 모양은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="17379-118">Below is what the create form looks like:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image1.png)

<span data-ttu-id="17379-119">및 "편집" 폼 모양은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="17379-119">And here is what our "Edit" form looks like:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image2.png)

<span data-ttu-id="17379-120">큰 차이 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="17379-120">Not much of a difference is there?</span></span> <span data-ttu-id="17379-121">제목 및 헤더 텍스트 이외에 다른 폼 레이아웃 및 입력 컨트롤은 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="17379-121">Other than the title and header text, the form layout and input controls are identical.</span></span>

<span data-ttu-id="17379-122">보기 템플릿은 소요 됩니다 "Edit.aspx" 및 "Create.aspx" 열에서는 경우에 동일한 양식 레이아웃 및 입력 컨트롤 코드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="17379-122">If we open up the "Edit.aspx" and "Create.aspx" view templates we'll find that they contain identical form layout and input control code.</span></span> <span data-ttu-id="17379-123">이 중복이 소개에서는 또는 좋은 없는 새 Dinner 속성-변경 하는 때마다에 두 번 변경 생길 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="17379-123">This duplication means we end up having to make changes twice anytime we introduce or change a new Dinner property - which is not good.</span></span>

### <a name="using-partial-view-templates"></a><span data-ttu-id="17379-124">부분 뷰 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="17379-124">Using Partial View Templates</span></span>

<span data-ttu-id="17379-125">ASP.NET MVC 페이지의 하위 부분 뷰 렌더링 논리를 캡슐화 하는 "부분 보기" 템플릿을 정의 하는 기능을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="17379-125">ASP.NET MVC supports the ability to define "partial view" templates that can be used to encapsulate view rendering logic for a sub-portion of a page.</span></span> <span data-ttu-id="17379-126">"부분" 뷰 렌더링 논리를 한 번 정의 하는 유용한 방법을 제공 하 고 다시 사용 여러 위치에서 응용 프로그램 간에 합니다.</span><span class="sxs-lookup"><span data-stu-id="17379-126">"Partials" provide a useful way to define view rendering logic once, and then re-use it in multiple places across an application.</span></span>

<span data-ttu-id="17379-127">"시험" 우리의 Edit.aspx 및 Create.aspx 보기 템플릿 복제를 위해 "DinnerForm.ascx" 양식 레이아웃 및 둘 다에 공통적으로 적용 되는 입력된 요소를 캡슐화 하는 명명 된 부분 뷰 템플릿을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17379-127">To help "DRY-up" our Edit.aspx and Create.aspx view template duplication, we can create a partial view template named "DinnerForm.ascx" that encapsulates the form layout and input elements common to both.</span></span> <span data-ttu-id="17379-128">우리의/보기/Dinners 디렉터리를 마우스 오른쪽 단추로 클릭 하 고 선택 하 여이 작업을 수행 하겠습니다는 "추가-&gt;보기" 메뉴 명령:</span><span class="sxs-lookup"><span data-stu-id="17379-128">We'll do this by right-clicking on our /Views/Dinners directory and choosing the "Add-&gt;View" menu command:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image3.png)

<span data-ttu-id="17379-129">그러면 "뷰 추가" 대화 상자를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17379-129">This will display the "Add View" dialog.</span></span> <span data-ttu-id="17379-130">이름을 새 보기 "DinnerForm"를 만들고,이 대화 상자에 "부분 뷰 만들기" 확인란을 선택 하 고는 전달 되는 것을 DinnerFormViewModel 클래스를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="17379-130">We'll name the new view we want to create "DinnerForm", select the "Create a partial view" checkbox within the dialog, and indicate that we will pass it a DinnerFormViewModel class:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image4.png)

<span data-ttu-id="17379-131">"추가" 단추를 클릭 하는 경우 Visual Studio는 우리 회사에 새 "DinnerForm.ascx" 보기 템플릿을 "\Views\Dinners" 디렉터리 내에서 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="17379-131">When we click the "Add" button, Visual Studio will create a new "DinnerForm.ascx" view template for us within the "\Views\Dinners" directory.</span></span>

<span data-ttu-id="17379-132">에서는 다음 붙여 넣을 수 중복 폼 레이아웃 /에 새 "DinnerForm.ascx" 부분 보기 템플릿은 Edit.aspx/ Create.aspx 우리의 보기 템플릿에서 컨트롤 코드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="17379-132">We can then copy/paste the duplicate form layout / input control code from our Edit.aspx/ Create.aspx view templates into our new "DinnerForm.ascx" partial view template:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample1.aspx)]

<span data-ttu-id="17379-133">그런 다음 DinnerForm 부분 템플릿을 호출할 폼 중복을 제거 하는 편집 및 만들기 보기 템플릿을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17379-133">We can then update our Edit and Create view templates to call the DinnerForm partial template and eliminate the form duplication.</span></span> <span data-ttu-id="17379-134">에서는 이렇게 호출 Html.RenderPartial("DinnerForm") 우리의 보기 템플릿 내에서:</span><span class="sxs-lookup"><span data-stu-id="17379-134">We can do this by calling Html.RenderPartial("DinnerForm") within our view templates:</span></span>

##### <a name="createaspx"></a><span data-ttu-id="17379-135">Create.aspx</span><span class="sxs-lookup"><span data-stu-id="17379-135">Create.aspx</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample2.aspx)]

##### <a name="editaspx"></a><span data-ttu-id="17379-136">Edit.aspx</span><span class="sxs-lookup"><span data-stu-id="17379-136">Edit.aspx</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample3.aspx)]

<span data-ttu-id="17379-137">Html.RenderPartial를 호출 하는 경우 원하는 부분 서식 파일의 경로 명시적으로 한정할 수 있습니다 (예: ~ Views/Dinners/DinnerForm.ascx ").</span><span class="sxs-lookup"><span data-stu-id="17379-137">You can explicitly qualify the path of the partial template you want when calling Html.RenderPartial (for example: ~Views/Dinners/DinnerForm.ascx").</span></span> <span data-ttu-id="17379-138">위의 코드에서 그러나는 ASP.NET MVC에서 규칙 기반 명명 패턴을 활용 하 고 렌더링할 부분 이름으로 "DinnerForm"를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="17379-138">In our code above, though, we are taking advantage of the convention-based naming pattern within ASP.NET MVC, and just specifying "DinnerForm" as the name of the partial to render.</span></span> <span data-ttu-id="17379-139">이 작업을 수행 하는 경우 ASP.NET MVC는 찾습니다 규칙 기반 views 디렉터리의 첫 번째 (DinnersController/보기/Dinners 됩니다).</span><span class="sxs-lookup"><span data-stu-id="17379-139">When we do this ASP.NET MVC will look first in the convention-based views directory (for DinnersController this would be /Views/Dinners).</span></span> <span data-ttu-id="17379-140">부분 템플릿을 찾지 못하면 있습니다 다음 보일지에 대 한 /Views/Shared 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17379-140">If it doesn't find the partial template there it will then look for it in the /Views/Shared directory.</span></span>

<span data-ttu-id="17379-141">Html.RenderPartial() 부분 보기의 이름만 사용 하 여 호출 되 면 ASP.NET MVC 동일한 모델과 ViewData 사전을 사용 하는 개체 뷰 템플릿을 호출 하 여 부분 보기에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="17379-141">When Html.RenderPartial() is called with just the name of the partial view, ASP.NET MVC will pass to the partial view the same Model and ViewData dictionary objects used by the calling view template.</span></span> <span data-ttu-id="17379-142">또는 대체 모델 개체 및/또는 ViewData 사전을 사용 하 여 부분 뷰를 전달할 수 있도록 하는 오버 로드 된 버전의 Html.RenderPartial() 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17379-142">Alternatively, there are overloaded versions of Html.RenderPartial() that enable you to pass an alternate Model object and/or ViewData dictionary for the partial view to use.</span></span> <span data-ttu-id="17379-143">만을 저장할 전체 모델/ViewModel의 하위 집합을 전달 하는 시나리오에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="17379-143">This is useful for scenarios where you only want to pass a subset of the full Model/ViewModel.</span></span>

| <span data-ttu-id="17379-144">**쪽 항목: 왜 &lt;% %&gt; of &lt;% = %&gt;?**</span><span class="sxs-lookup"><span data-stu-id="17379-144">**Side Topic: Why &lt;% %&gt; instead of &lt;%= %&gt;?**</span></span> |
| --- |
| <span data-ttu-id="17379-145">사용 하는 미묘한 위의 코드를 사용 하 여 보았을 것 중 하나를 &lt;% %&gt; 블록 대신를 &lt;% = %&gt; Html.RenderPartial()를 호출 하는 경우 차단 합니다.</span><span class="sxs-lookup"><span data-stu-id="17379-145">One of the subtle things you might have noticed with the code above is that we are using a &lt;% %&gt; block instead of a &lt;%= %&gt; block when calling Html.RenderPartial().</span></span> <span data-ttu-id="17379-146">&lt;% = %&gt; 개발자가 지정된 된 값을 렌더링 하는 ASP.NET의 블록 나타냅니다 (예: &lt;% = "Hello" %&gt; "Hello"를 렌더링 하는).</span><span class="sxs-lookup"><span data-stu-id="17379-146">&lt;%= %&gt; blocks in ASP.NET indicate that a developer wants to render a specified value (for example: &lt;%= "Hello" %&gt; would render "Hello").</span></span> <span data-ttu-id="17379-147">&lt;% %&gt; 블록에는 대신 개발자가 코드를 실행 하려고 하 고 내에 출력을 렌더링 된 어떠한 이루어져야 합니다. 명시적으로 함을 나타냅니다 (예: &lt;Response.Write("Hello") %&gt;합니다.</span><span class="sxs-lookup"><span data-stu-id="17379-147">&lt;% %&gt; blocks instead indicate that the developer wants to execute code, and that any rendered output within them must be done explicitly (for example: &lt;% Response.Write("Hello") %&gt;.</span></span> <span data-ttu-id="17379-148">사용 하는 이유는 &lt;% %&gt; 위의 Html.RenderPartial 코드 블록은 Html.RenderPartial() 메서드는 문자열을 반환 하지 않습니다 하 고 대신 호출 템플릿 보기에 직접 콘텐츠를 스트림에 출력을 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="17379-148">The reason we are using a &lt;% %&gt; block with our Html.RenderPartial code above is because the Html.RenderPartial() method doesn't return a string, and instead outputs the content directly to the calling view template's output stream.</span></span> <span data-ttu-id="17379-149">성능상의 이유로 효율성 및 해당 하면 (잠재적으로 매우 큼) 임시 문자열 개체를 만들 필요가 없습니다. 이렇게 하 여이 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="17379-149">It does this for performance efficiency reasons, and by doing so it avoids the need to create a (potentially very large) temporary string object.</span></span> <span data-ttu-id="17379-150">메모리 사용량 줄이고 전체 응용 프로그램 처리량을 향상 합니다.</span><span class="sxs-lookup"><span data-stu-id="17379-150">This reduces memory usage and improves overall application throughput.</span></span> <span data-ttu-id="17379-151">한 가지 일반적인 실수 때 Html.RenderPartial()를 사용 하 여 내에 없을 때 호출의 끝에 세미콜론을 추가 해야 하는 &lt;% %&gt; 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="17379-151">One common mistake when using Html.RenderPartial() is to forget to add a semi-colon at the end of the call when it is within a &lt;% %&gt; block.</span></span> <span data-ttu-id="17379-152">예를 들어이 코드 하면 컴파일러 오류가 발생 합니다. &lt;Html.RenderPartial("DinnerForm") %&gt; 작성 해야 하는 대신: &lt;Html.RenderPartial("DinnerForm") %; %&gt; 때문에 이것이 &lt;% %&gt; 블록은 자체 포함 된 코드 문의 문을 세미콜론으로 종료 하는 데 필요한 C# 코드를 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="17379-152">For example, this code will cause a compiler error: &lt;% Html.RenderPartial("DinnerForm") %&gt; You instead need to write: &lt;% Html.RenderPartial("DinnerForm"); %&gt; This is because &lt;% %&gt; blocks are self-contained code statements, and when using C# code statements need to be terminated with a semi-colon.</span></span> |

### <a name="using-partial-view-templates-to-clarify-code"></a><span data-ttu-id="17379-153">부분 뷰 템플릿을 사용 하 여 코드를 명확 하 게</span><span class="sxs-lookup"><span data-stu-id="17379-153">Using Partial View Templates to Clarify Code</span></span>

<span data-ttu-id="17379-154">여러 위치에서 뷰 렌더링 논리를 복제 하지 않으려면 "DinnerForm" 부분 뷰 템플릿을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="17379-154">We created the "DinnerForm" partial view template to avoid duplicating view rendering logic in multiple places.</span></span> <span data-ttu-id="17379-155">부분 뷰 템플릿을 만드는 가장 일반적인 이유입니다.</span><span class="sxs-lookup"><span data-stu-id="17379-155">This is the most common reason to create partial view templates.</span></span>

<span data-ttu-id="17379-156">경우에 따라 여전히는 것이 좋습니다만 단일 위치에서 호출 될 경우에 부분 보기를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17379-156">Sometimes it still makes sense to create partial views even when they are only being called in a single place.</span></span> <span data-ttu-id="17379-157">매우 복잡 한 뷰 템플릿 자주 해당 뷰 렌더링 논리를 추출 및 하나로 분할 또는 템플릿의 부분을 더 잘 라는 하는 경우 읽기를 훨씬 쉽게 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17379-157">Very complicated view templates can often become much easier to read when their view rendering logic is extracted and partitioned into one or more well named partial templates.</span></span>

<span data-ttu-id="17379-158">예를 들어를 Site.master 파일 (살펴볼 것에서 곧)는 프로젝트에서 코드 조각 아래.</span><span class="sxs-lookup"><span data-stu-id="17379-158">For example, consider the below code-snippet from the Site.master file in our project (which we will be looking at shortly).</span></span> <span data-ttu-id="17379-159">코드는 비교적 간단 읽을 – 맨 위에 있는 로그인/로그 아웃을 표시 하는 논리를 연결 하기 때문에 부분적으로 화면의 오른쪽 "LogOnUserControl" 부분 내에서 캡슐화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17379-159">The code is relatively straight-forward to read – partly because the logic to display a login/logout link at the top right of the screen is encapsulated within the "LogOnUserControl" partial:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample4.aspx)]

<span data-ttu-id="17379-160">혼란 직접 찾을 때마다 템플릿 보기 내에서 html/코드 태그를 이해 하는 동안, 여부를 추출 하 고 이름을 잘 지정 부분 보기로 리팩터링 되었으면 일부 정보를 더 분명히 알 수 없습니다 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="17379-160">Whenever you find yourself getting confused trying to understand the html/code markup within a view-template, consider whether it wouldn't be clearer if some of it was extracted and refactored into well-named partial views.</span></span>

### <a name="master-pages"></a><span data-ttu-id="17379-161">마스터 페이지</span><span class="sxs-lookup"><span data-stu-id="17379-161">Master Pages</span></span>

<span data-ttu-id="17379-162">ASP.NET MVC 부분 뷰를 지원할 뿐 아니라 일반적인 레이아웃 및 최상위 html 사이트의 정의를 사용할 수 있는 "마스터 페이지" 템플릿을 만드는 기능도 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="17379-162">In addition to supporting partial views, ASP.NET MVC also supports the ability to create "master page" templates that can be used to define the common layout and top-level html of a site.</span></span> <span data-ttu-id="17379-163">콘텐츠 자리 표시자 컨트롤 재정의 하거나 "입력" 보기에서 실행할 수 있는 대체 가능 영역을 식별 하는 마스터 페이지에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17379-163">Content placeholder controls can then be added to the master page to identify replaceable regions that can be overridden or "filled in" by views.</span></span> <span data-ttu-id="17379-164">응용 프로그램 간에 일반적인 레이아웃을 적용 하는 매우 효과적인 (및 반복 금지) 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="17379-164">This provides a very effective (and DRY) way to apply a common layout across an application.</span></span>

<span data-ttu-id="17379-165">기본적으로 새 ASP.NET MVC 프로젝트에 자동으로 추가 하는 마스터 페이지 템플릿을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="17379-165">By default, new ASP.NET MVC projects have a master page template automatically added to them.</span></span> <span data-ttu-id="17379-166">이 마스터 페이지에는 "Site.master" 및 \Views\Shared\ 폴더 내에서 있는 이름이 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17379-166">This master page is named "Site.master" and lives within the \Views\Shared\ folder:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image5.png)

<span data-ttu-id="17379-167">기본 Site.master 파일을 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="17379-167">The default Site.master file looks like below.</span></span> <span data-ttu-id="17379-168">맨 위에 있는 탐색에 대 한 메뉴와 함께 사이트의 외부 html을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="17379-168">It defines the outer html of the site, along with a menu for navigation at the top.</span></span> <span data-ttu-id="17379-169">콘텐츠 자리 표시자를 대체할 수 있는 두 개의 – 제목 및 페이지의 기본 콘텐츠는 바꿔야 하는 것에 대 한 기타 하나 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="17379-169">It contains two replaceable content placeholder controls – one for the title, and the other for where the primary content of a page should be replaced:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample5.aspx)]

<span data-ttu-id="17379-170">NerdDinner 응용 프로그램 ("List", "Details", "편집", "만들기", "NotFound" 등) 용으로 만든 모든 보기 기반을 두었습니다이 Site.master 템플릿.</span><span class="sxs-lookup"><span data-stu-id="17379-170">All of the view templates we've created for our NerdDinner application ("List", "Details", "Edit", "Create", "NotFound", etc) have been based on this Site.master template.</span></span> <span data-ttu-id="17379-171">이 기본적으로 위쪽에 추가 된 "MasterPageFile" 특성을 통해 표시 됩니다 &lt;% @ 페이지 %&gt; 지시문 "뷰 추가" 대화 상자를 사용 하 여 뷰를 만들 때:</span><span class="sxs-lookup"><span data-stu-id="17379-171">This is indicated via the "MasterPageFile" attribute that was added by default to the top &lt;% @ Page %&gt; directive when we created our views using the "Add View" dialog:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample6.aspx)]

<span data-ttu-id="17379-172">즉 Site.master 콘텐츠를 변경할 수 있습니다 및가 변경 내용을 자동으로 적용 되며 우리의 보기 템플릿 중 하나를 렌더링 하는 경우에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="17379-172">What this means is that we can change the Site.master content, and have the changes automatically be applied and used when we render any of our view templates.</span></span>

<span data-ttu-id="17379-173">응용 프로그램의 헤더는 "내 MVC 응용 프로그램" 대신 "NerdDinner" 있도록 우리의 Site.master 헤더 섹션을 업데이트 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="17379-173">Let's update our Site.master's header section so that the header of our application is "NerdDinner" instead of "My MVC Application".</span></span> <span data-ttu-id="17379-174">보겠습니다도 업데이트는 탐색 메뉴 되도록 첫 번째 탭 "찾기는 저녁 식사" (HomeController의 index () 동작 메서드에서 처리), "호스트를 저녁 식사" (DinnersController의 create () 동작 메서드에서 처리 됨) 이라는 새 탭을 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="17379-174">Let's also update our navigation menu so that the first tab is "Find a Dinner" (handled by the HomeController's Index() action method), and let's add a new tab called "Host a Dinner" (handled by the DinnersController's Create() action method):</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample7.aspx)]

<span data-ttu-id="17379-175">Site.master 파일 및 새로 고침 저장이 헤더를 보면 브라우저는 표시 응용 프로그램 내에서 모든 뷰에 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="17379-175">When we save the Site.master file and refresh our browser we'll see our header changes show up across all views within our application.</span></span> <span data-ttu-id="17379-176">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="17379-176">For example:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image6.png)

<span data-ttu-id="17379-177">와 */Dinners/편집 / [id]* URL:</span><span class="sxs-lookup"><span data-stu-id="17379-177">And with the */Dinners/Edit/[id]* URL:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image7.png)

### <a name="next-step"></a><span data-ttu-id="17379-178">다음 단계</span><span class="sxs-lookup"><span data-stu-id="17379-178">Next Step</span></span>

<span data-ttu-id="17379-179">마스터 페이지 및 부분 뷰를 완전히 구성할 수 있도록 매우 유연한 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="17379-179">Partials and master pages provide very flexible options that enable you to cleanly organize views.</span></span> <span data-ttu-id="17379-180">뷰에서 중복을 방지할 수 콘텐츠 / 코드 하며 보기 템플릿을 더 쉽게 읽고 유지 관리를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17379-180">You'll find that they help you avoid duplicating view content/ code, and make your view templates easier to read and maintain.</span></span>

<span data-ttu-id="17379-181">보겠습니다 이제 앞서 작성 목록 시나리오를 다시 방문 및 확장 가능한 페이징 지원을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="17379-181">Let's now revisit the listing scenario we built earlier and enable scalable paging support.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="17379-182">[이전](use-viewdata-and-implement-viewmodel-classes.md)
> [다음](implement-efficient-data-paging.md)</span><span class="sxs-lookup"><span data-stu-id="17379-182">[Previous](use-viewdata-and-implement-viewmodel-classes.md)
[Next](implement-efficient-data-paging.md)</span></span>
