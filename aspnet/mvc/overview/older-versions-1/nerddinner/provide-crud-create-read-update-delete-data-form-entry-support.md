---
uid: mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
title: 제공 CRUD (만들기, 읽기, 업데이트, 삭제) 데이터 양식 항목 지원 | Microsoft Docs
author: microsoft
description: 5 단계 편집, 만들기 및도 함께 Dinners 삭제에 대 한 지원 사용 하 여 추가로 DinnersController 클래스를 사용 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: bbb976e5-6150-4283-a374-c22fbafe29f5
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
msc.type: authoredcontent
ms.openlocfilehash: 45d74249a34fc7e37e9776a398615d2f613a7582
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41828377"
---
<a name="provide-crud-create-read-update-delete-data-form-entry-support"></a><span data-ttu-id="e4f11-103">제공 CRUD (만들기, 읽기, 업데이트, 삭제) 데이터 양식 항목 지원</span><span class="sxs-lookup"><span data-stu-id="e4f11-103">Provide CRUD (Create, Read, Update, Delete) Data Form Entry Support</span></span>
====================
<span data-ttu-id="e4f11-104">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="e4f11-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="e4f11-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="e4f11-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="e4f11-106">이 무료의 5 단계 ["NerdDinner" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 는 안내를 통한 작은 빌드 하지만 ASP.NET MVC 1을 사용 하 여 웹 응용 프로그램을 완료 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-106">This is step 5 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="e4f11-107">5 단계 편집, 만들기 및도 함께 Dinners 삭제에 대 한 지원 사용 하 여 추가로 DinnersController 클래스를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-107">Step 5 shows how to take our DinnersController class further by enable support for editing, creating and deleting Dinners with it as well.</span></span>
> 
> <span data-ttu-id="e4f11-108">ASP.NET MVC 3을 사용 하는 경우 수행 하는 것이 좋습니다 합니다 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 하거나 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-step-5-create-update-delete-form-scenarios"></a><span data-ttu-id="e4f11-109">NerdDinner 5 단계: 만들기, 업데이트, 양식 시나리오를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-109">NerdDinner Step 5: Create, Update, Delete Form Scenarios</span></span>

<span data-ttu-id="e4f11-110">컨트롤러 및 보기를 도입 하 고 사용 하 여 사이트에서 Dinners에 대 한 목록/세부 정보 환경을 구현 하는 방법을 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-110">We've introduced controllers and views, and covered how to use them to implement a listing/details experience for Dinners on site.</span></span> <span data-ttu-id="e4f11-111">다음 단계는 DinnersController 클래스를 좀 더 수행 하 고 편집, 만들기 및도 함께 Dinners 삭제에 대 한 지원을 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-111">Our next step will be to take our DinnersController class further and enable support for editing, creating and deleting Dinners with it as well.</span></span>

### <a name="urls-handled-by-dinnerscontroller"></a><span data-ttu-id="e4f11-112">DinnersController에서 처리 하는 Url</span><span class="sxs-lookup"><span data-stu-id="e4f11-112">URLs handled by DinnersController</span></span>

<span data-ttu-id="e4f11-113">두 Url에 대 한 지원을 구현 하는 DinnersController에 작업 메서드 이전에 추가한: */Dinners* 하 고 */Dinners 세부 정보 / [id]* 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-113">We previously added action methods to DinnersController that implemented support for two URLs: */Dinners* and */Dinners/Details/[id]*.</span></span>

| <span data-ttu-id="e4f11-114">**URL**</span><span class="sxs-lookup"><span data-stu-id="e4f11-114">**URL**</span></span> | <span data-ttu-id="e4f11-115">**동사**</span><span class="sxs-lookup"><span data-stu-id="e4f11-115">**VERB**</span></span> | <span data-ttu-id="e4f11-116">**용도**</span><span class="sxs-lookup"><span data-stu-id="e4f11-116">**Purpose**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e4f11-117">*/Dinners/*</span><span class="sxs-lookup"><span data-stu-id="e4f11-117">*/Dinners/*</span></span> | <span data-ttu-id="e4f11-118">가져오기</span><span class="sxs-lookup"><span data-stu-id="e4f11-118">GET</span></span> | <span data-ttu-id="e4f11-119">예정 된 dinners는 HTML 목록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-119">Display an HTML list of upcoming dinners.</span></span> |
| <span data-ttu-id="e4f11-120">*/Dinners/Details/[id]*</span><span class="sxs-lookup"><span data-stu-id="e4f11-120">*/Dinners/Details/[id]*</span></span> | <span data-ttu-id="e4f11-121">가져오기</span><span class="sxs-lookup"><span data-stu-id="e4f11-121">GET</span></span> | <span data-ttu-id="e4f11-122">특정 저녁에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-122">Display details about a specific dinner.</span></span> |

<span data-ttu-id="e4f11-123">이제 세 가지 추가 Url을 구현 하는 작업 메서드를 추가 합니다. <em>/Dinners/편집 / [id], Dinners/만들기,</em>하 고<em>/Dinners/삭제 / [id]</em>합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-123">We will now add action methods to implement three additional URLs: <em>/Dinners/Edit/[id], /Dinners/Create,</em>and<em>/Dinners/Delete/[id]</em>.</span></span> <span data-ttu-id="e4f11-124">이러한 Url 편집 기존 Dinners 새 Dinners 만들고 Dinners 삭제에 대 한 지원을 사용 하도록 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-124">These URLs will enable support for editing existing Dinners, creating new Dinners, and deleting Dinners.</span></span>

<span data-ttu-id="e4f11-125">이러한 새 Url 사용 하 여 HTTP GET 및 HTTP POST 동사 상호 작용 지원할 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-125">We will support both HTTP GET and HTTP POST verb interactions with these new URLs.</span></span> <span data-ttu-id="e4f11-126">다음이 Url에 HTTP GET 요청 데이터 (폼 데이터로 Dinner "편집"의 경우, "만들기"의 경우 빈 폼 및 삭제 확인 화면이 "삭제"의 경우)의 초기 HTML 보기를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-126">HTTP GET requests to these URLs will display the initial HTML view of the data (a form populated with the Dinner data in the case of "edit", a blank form in the case of "create", and a delete confirmation screen in the case of "delete").</span></span> <span data-ttu-id="e4f11-127">다음이 Url에 HTTP POST 요청 우리의 DinnerRepository (그리고 데이터베이스에는 여기에서) Dinner 데이터를 저장/업데이트/삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-127">HTTP POST requests to these URLs will save/update/delete the Dinner data in our DinnerRepository (and from there to the database).</span></span>

| <span data-ttu-id="e4f11-128">**URL**</span><span class="sxs-lookup"><span data-stu-id="e4f11-128">**URL**</span></span> | <span data-ttu-id="e4f11-129">**동사**</span><span class="sxs-lookup"><span data-stu-id="e4f11-129">**VERB**</span></span> | <span data-ttu-id="e4f11-130">**용도**</span><span class="sxs-lookup"><span data-stu-id="e4f11-130">**Purpose**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e4f11-131">*/Dinners/Edit/[id]*</span><span class="sxs-lookup"><span data-stu-id="e4f11-131">*/Dinners/Edit/[id]*</span></span> | <span data-ttu-id="e4f11-132">가져오기</span><span class="sxs-lookup"><span data-stu-id="e4f11-132">GET</span></span> | <span data-ttu-id="e4f11-133">저녁 식사 데이터로 채워진 편집 가능한 HTML 폼을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-133">Display an editable HTML form populated with Dinner data.</span></span> |
| <span data-ttu-id="e4f11-134">올리기</span><span class="sxs-lookup"><span data-stu-id="e4f11-134">POST</span></span> | <span data-ttu-id="e4f11-135">데이터베이스에 특정 저녁 폼 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-135">Save the form changes for a particular Dinner to the database.</span></span> |
| <span data-ttu-id="e4f11-136">*/Dinners/Create*</span><span class="sxs-lookup"><span data-stu-id="e4f11-136">*/Dinners/Create*</span></span> | <span data-ttu-id="e4f11-137">가져오기</span><span class="sxs-lookup"><span data-stu-id="e4f11-137">GET</span></span> | <span data-ttu-id="e4f11-138">사용자가 새 Dinners 정의할 수 있는 빈 HTML 폼을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-138">Display an empty HTML form that allows users to define new Dinners.</span></span> |
| <span data-ttu-id="e4f11-139">올리기</span><span class="sxs-lookup"><span data-stu-id="e4f11-139">POST</span></span> | <span data-ttu-id="e4f11-140">새 Dinner 만들고 데이터베이스에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-140">Create a new Dinner and save it in the database.</span></span> |
| <span data-ttu-id="e4f11-141">*/Dinners/Delete/[id]*</span><span class="sxs-lookup"><span data-stu-id="e4f11-141">*/Dinners/Delete/[id]*</span></span> | <span data-ttu-id="e4f11-142">가져오기</span><span class="sxs-lookup"><span data-stu-id="e4f11-142">GET</span></span> | <span data-ttu-id="e4f11-143">삭제 확인 화면을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-143">Display delete confirmation screen.</span></span> |
| <span data-ttu-id="e4f11-144">올리기</span><span class="sxs-lookup"><span data-stu-id="e4f11-144">POST</span></span> | <span data-ttu-id="e4f11-145">데이터베이스에서 지정한 저녁 식사를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-145">Deletes the specified dinner from the database.</span></span> |

### <a name="edit-support"></a><span data-ttu-id="e4f11-146">편집 지원</span><span class="sxs-lookup"><span data-stu-id="e4f11-146">Edit Support</span></span>

<span data-ttu-id="e4f11-147">"편집" 시나리오를 구현 하 여 시작 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-147">Let's begin by implementing the "edit" scenario.</span></span>

#### <a name="the-http-get-edit-action-method"></a><span data-ttu-id="e4f11-148">HTTP GET 편집 작업 메서드</span><span class="sxs-lookup"><span data-stu-id="e4f11-148">The HTTP-GET Edit Action Method</span></span>

<span data-ttu-id="e4f11-149">편집 작업 메서드는 HTTP "GET" 동작을 구현 하 여 시작 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-149">We'll start by implementing the HTTP "GET" behavior of our edit action method.</span></span> <span data-ttu-id="e4f11-150">이 메서드에서 될 때 호출 된 */Dinners/편집 / [id]* URL이 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-150">This method will be invoked when the */Dinners/Edit/[id]* URL is requested.</span></span> <span data-ttu-id="e4f11-151">구현은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-151">Our implementation will look like:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample1.cs)]

<span data-ttu-id="e4f11-152">위의 코드는 Dinner 개체를 검색 하는 DinnerRepository를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-152">The code above uses the DinnerRepository to retrieve a Dinner object.</span></span> <span data-ttu-id="e4f11-153">그런 다음 Dinner 개체를 사용 하 여 보기 템플릿을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-153">It then renders a View template using the Dinner object.</span></span> <span data-ttu-id="e4f11-154">서식 파일 이름을 명시적으로 전달 하지 않았으므로 합니다 *View()* 도우미 메서드를 보기 템플릿은 해결 하려면 규칙 기반 기본 경로 사용 하면 해당: /Views/Dinners/Edit.aspx 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-154">Because we haven't explicitly passed a template name to the *View()* helper method, it will use the convention based default path to resolve the view template: /Views/Dinners/Edit.aspx.</span></span>

<span data-ttu-id="e4f11-155">이 보기 템플릿은 이제 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-155">Let's now create this view template.</span></span> <span data-ttu-id="e4f11-156">편집 메서드 내에서 마우스 오른쪽 단추로 클릭 하 고 "추가 보기" 상황에 맞는 메뉴 명령을 선택 하 여이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-156">We will do this by right-clicking within the Edit method and selecting the "Add View" context menu command:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image1.png)

<span data-ttu-id="e4f11-157">"뷰 추가" 대화 상자 내에서 해당 모델로 보기 템플릿은를 Dinner 개체를 전달 하는 것 및 자동-스 캐 폴드를 "편집" 템플릿을 선택 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-157">Within the "Add View" dialog we'll indicate that we are passing a Dinner object to our view template as its model, and choose to auto-scaffold an "Edit" template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image2.png)

<span data-ttu-id="e4f11-158">"추가" 단추를 클릭 하는 경우 Visual Studio는 "\Views\Dinners" 디렉터리 내에서 새 "Edit.aspx" 보기 템플릿 파일을를에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-158">When we click the "Add" button, Visual Studio will add a new "Edit.aspx" view template file for us within the "\Views\Dinners" directory.</span></span> <span data-ttu-id="e4f11-159">또한 코드-편집기 내 – 초기 "편집" 스 캐 폴드 구현 같은 아래 채워진 새 "Edit.aspx" 보기 템플릿을 열립니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-159">It will also open up the new "Edit.aspx" view template within the code-editor – populated with an initial "Edit" scaffold implementation like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image3.png)

<span data-ttu-id="e4f11-160">기본 "편집" 스 캐 폴드 생성에 대 한 몇 가지 변경 하 고 (제거 하는 몇 가지 속성을 노출 하지 않으려는 것) 아래 콘텐츠 보기 템플릿 편집 업데이트 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-160">Let's make a few changes to the default "edit" scaffold generated, and update the edit view template to have the content below (which removes a few of the properties we don't want to expose):</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample2.aspx)]

<span data-ttu-id="e4f11-161">응용 프로그램 및 요청을 실행할 때 합니다 *"/ 1/편집/Dinners"* URL 페이지를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-161">When we run the application and request the *"/Dinners/Edit/1"* URL we will see the following page:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image4.png)

<span data-ttu-id="e4f11-162">보기에서 생성 된 HTML 태그를 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-162">The HTML markup generated by our view looks like below.</span></span> <span data-ttu-id="e4f11-163">표준 HTML –를 &lt;폼&gt; HTTP POST를 수행 하는 요소는 */Dinners/Edit/1* URL 때 "저장" &lt;입력 형식 = "제출" /&gt; 단추를 누르면.</span><span class="sxs-lookup"><span data-stu-id="e4f11-163">It is standard HTML – with a &lt;form&gt; element that performs an HTTP POST to the */Dinners/Edit/1* URL when the "Save" &lt;input type="submit"/&gt; button is pushed.</span></span> <span data-ttu-id="e4f11-164">HTML &lt;입력 형식 = "text" /&gt; 요소는 편집 가능한 각 속성에 대 한 출력 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-164">A HTML &lt;input type="text"/&gt; element has been output for each editable property:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image5.png)

#### <a name="htmlbeginform-and-htmltextbox-html-helper-methods"></a><span data-ttu-id="e4f11-165">Html.BeginForm() 및 Html.TextBox() Html 도우미 메서드</span><span class="sxs-lookup"><span data-stu-id="e4f11-165">Html.BeginForm() and Html.TextBox() Html Helper Methods</span></span>

<span data-ttu-id="e4f11-166">"Edit.aspx" 보기 템플릿은 몇 가지 "Html 도우미" 메서드를 사용 하는: Html.ValidationSummary(), Html.BeginForm(), Html.TextBox(), 및 Html.ValidationMessage() 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-166">Our "Edit.aspx" view template is using several "Html Helper" methods: Html.ValidationSummary(), Html.BeginForm(), Html.TextBox(), and Html.ValidationMessage().</span></span> <span data-ttu-id="e4f11-167">미국에 대 한 HTML 태그를 생성 하는 것 외에도 이러한 도우미 메서드는 기본 제공 오류 처리 및 유효성 검사를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-167">In addition to generating HTML markup for us, these helper methods provide built-in error handling and validation support.</span></span>

##### <a name="htmlbeginform-helper-method"></a><span data-ttu-id="e4f11-168">Html.BeginForm() 도우미 메서드</span><span class="sxs-lookup"><span data-stu-id="e4f11-168">Html.BeginForm() helper method</span></span>

<span data-ttu-id="e4f11-169">Html.BeginForm() 도우미 메서드는 HTML 출력 &lt;폼&gt; 는 태그 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-169">The Html.BeginForm() helper method is what output the HTML &lt;form&gt; element in our markup.</span></span> <span data-ttu-id="e4f11-170">Edit.aspx 보기 템플릿은에 적용 중인 C# "using" 문을이 메서드를 사용 하는 경우 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-170">In our Edit.aspx view template you'll notice that we are applying a C# "using" statement when using this method.</span></span> <span data-ttu-id="e4f11-171">중괄호의 시작을 나타냅니다 합니다 &lt;폼&gt; 콘텐츠 및 닫는 중괄호는 끝을 나타내는 새로운 합니다 &lt;/f&gt; 요소:</span><span class="sxs-lookup"><span data-stu-id="e4f11-171">The open curly brace indicates the beginning of the &lt;form&gt; content, and the closing curly brace is what indicates the end of the &lt;/form&gt; element:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample3.cs)]

<span data-ttu-id="e4f11-172">또는 "using" 문을 있다면 다음과 같은 시나리오에 부자연 스러운 접근는 Html.BeginForm() 및 Html.EndForm() 조합 (동일한 작업을 수행)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-172">Alternatively, if you find the "using" statement approach unnatural for a scenario like this, you can use a Html.BeginForm() and Html.EndForm() combination (which does the same thing):</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample4.aspx)]

<span data-ttu-id="e4f11-173">매개 변수 없이 Html.BeginForm()를 호출 하면 현재 요청의 URL에 HTTP POST를 수행 하는 폼 요소를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-173">Calling Html.BeginForm() without any parameters will cause it to output a form element that does an HTTP-POST to the current request's URL.</span></span> <span data-ttu-id="e4f11-174">편집 보기 생성 이유 즉를 *&lt;양식 동작 = "/ Dinners/편집/1" 메서드 "post" =&gt;* 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-174">That is why our Edit view generates a *&lt;form action="/Dinners/Edit/1" method="post"&gt;* element.</span></span> <span data-ttu-id="e4f11-175">수 또는 전달 했으므로 명시적 매개 변수가 Html.BeginForm()를 다른 URL에 게시 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="e4f11-175">We could have alternatively passed explicit parameters to Html.BeginForm() if we wanted to post to a different URL.</span></span>

##### <a name="htmltextbox-helper-method"></a><span data-ttu-id="e4f11-176">Html.TextBox() 도우미 메서드</span><span class="sxs-lookup"><span data-stu-id="e4f11-176">Html.TextBox() helper method</span></span>

<span data-ttu-id="e4f11-177">Edit.aspx 뷰에 Html.TextBox() 도우미 메서드를 사용 하 여 출력 &lt;type = "text" /&gt; 요소:</span><span class="sxs-lookup"><span data-stu-id="e4f11-177">Our Edit.aspx view uses the Html.TextBox() helper method to output &lt;input type="text"/&gt; elements:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample5.aspx)]

<span data-ttu-id="e4f11-178">위의 Html.TextBox() 메서드의 i d/이름 특성을 지정 하는 데 사용 되는 단일 매개-변수를 &lt;입력 형식 = "text" /&gt; 에서 텍스트 상자 값을 채우려고 모델 속성 뿐만 아니라 출력 요소.</span><span class="sxs-lookup"><span data-stu-id="e4f11-178">The Html.TextBox() method above takes a single parameter – which is being used to specify both the id/name attributes of the &lt;input type="text"/&gt; element to output, as well as the model property to populate the textbox value from.</span></span> <span data-ttu-id="e4f11-179">예를 들어 Dinner 개체 편집 보기에 전달 했습니다 ".NET 미래", "Title" 속성 값 있어 없으므로 Html.TextBox("Title") 메서드 호출 출력: *&lt;입력된 id = "Title" name = "Title" type = "text" value = ".NET 미래" /&gt;*.</span><span class="sxs-lookup"><span data-stu-id="e4f11-179">For example, the Dinner object we passed to the Edit view had a "Title" property value of ".NET Futures", and so our Html.TextBox("Title") method call output: *&lt;input id="Title" name="Title" type="text" value=".NET Futures" /&gt;*.</span></span>

<span data-ttu-id="e4f11-180">또는 요소의 id/이름을 지정 하 고 두 번째 매개 변수로 사용할 값에 명시적으로 전달 하려면 첫 번째 Html.TextBox() 매개 변수를 사용할 수 것:</span><span class="sxs-lookup"><span data-stu-id="e4f11-180">Alternatively, we can use the first Html.TextBox() parameter to specify the id/name of the element, and then explicitly pass in the value to use as a second parameter:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample6.aspx)]

<span data-ttu-id="e4f11-181">종종 출력 되는 값에 사용자 지정 형식 지정을 수행 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-181">Often we'll want to perform custom formatting on the value that is output.</span></span> <span data-ttu-id="e4f11-182">.NET에 기본 제공 string.format () 정적 메서드가 이러한 시나리오에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-182">The String.Format() static method built-into .NET is useful for these scenarios.</span></span> <span data-ttu-id="e4f11-183">Edit.aspx 보기 템플릿은 형식을 지정 하 여이 EventDate 값 (날짜/시간 형식입니다.) 시간을 초를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-183">Our Edit.aspx view template is using this to format the EventDate value (which is of type DateTime) so that it doesn't show seconds for the time:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample7.aspx)]

<span data-ttu-id="e4f11-184">필요에 따라 Html.TextBox()는 세 번째 매개 변수 추가 HTML 특성을 출력에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-184">A third parameter to Html.TextBox() can optionally be used to output additional HTML attributes.</span></span> <span data-ttu-id="e4f11-185">아래 코드 조각에는 추가 크기를 렌더링 하는 방법을 보여 줍니다. "30" 특성과 class = = "mycssclass" 특성에는 &lt;type = "text" /&gt; 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-185">The code-snippet below demonstrates how to render an additional size="30" attribute and a class="mycssclass" attribute on the &lt;input type="text"/&gt; element.</span></span> <span data-ttu-id="e4f11-186">확인 하는 방법을 사용 하 여 클래스 특성의 이름을 이스케이프 된 것을 "@" character because "클래스"는 C#에서 예약 된 키워드:</span><span class="sxs-lookup"><span data-stu-id="e4f11-186">Note how we are escaping the name of the class attribute using a "@" character because "class" is a reserved keyword in C#:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample8.aspx)]

#### <a name="implementing-the-http-post-edit-action-method"></a><span data-ttu-id="e4f11-187">HTTP POST 편집 작업 메서드를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-187">Implementing the HTTP-POST Edit Action Method</span></span>

<span data-ttu-id="e4f11-188">이제 구현 하는 편집 작업 메서드를 HTTP GET 버전이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-188">We now have the HTTP-GET version of our Edit action method implemented.</span></span> <span data-ttu-id="e4f11-189">사용자가 요청 하는 경우는 */Dinners/Edit/1* 다음과 같은 HTML 페이지를 받은 URL:</span><span class="sxs-lookup"><span data-stu-id="e4f11-189">When a user requests the */Dinners/Edit/1* URL they receive an HTML page like the following:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image6.png)

<span data-ttu-id="e4f11-190">"저장" 단추를 누르면 폼 post를 실행 하는 */Dinners/Edit/1* URL을 HTML 제출 &lt;입력&gt; HTTP POST 동사를 사용 하 여 값을 형성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-190">Pressing the "Save" button causes a form post to the */Dinners/Edit/1* URL, and submits the HTML &lt;input&gt; form values using the HTTP POST verb.</span></span> <span data-ttu-id="e4f11-191">이제는 편집 작업 메서드의 – Dinner 저장를 처리 하는 HTTP POST 동작을 구현 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-191">Let's now implement the HTTP POST behavior of our edit action method – which will handle saving the Dinner.</span></span>

<span data-ttu-id="e4f11-192">HTTP POST 시나리오 처리 여부를 나타내는 "AcceptVerbs" 특성에는 우리의 DinnersController 오버 로드 "편집" 작업 메서드도 추가 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-192">We'll begin by adding an overloaded "Edit" action method to our DinnersController that has an "AcceptVerbs" attribute on it that indicates it handles HTTP POST scenarios:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample9.cs)]

<span data-ttu-id="e4f11-193">오버 로드 된 작업 메서드에 [AcceptVerbs] 특성이 적용 되 면 ASP.NET MVC는 자동으로 들어오는 HTTP 동사에 따라 적절 한 동작 메서드에 디스패치 요청을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-193">When the [AcceptVerbs] attribute is applied to overloaded action methods, ASP.NET MVC automatically handles dispatching requests to the appropriate action method depending on the incoming HTTP verb.</span></span> <span data-ttu-id="e4f11-194">HTTP POST 요청을 <em>/Dinners/편집 / [id]</em> Url에 다른 모든 HTTP 동사 요청 하는 동안 위의 편집 메서드를 이동 <em>/Dinners/편집 / [id]</em>Url 될 첫 번째 편집 메서드에 구현 했습니다 (않았습니다 있음 없습니다 [AcceptVerbs] 특성).</span><span class="sxs-lookup"><span data-stu-id="e4f11-194">HTTP POST requests to <em>/Dinners/Edit/[id]</em> URLs will go to the above Edit method, while all other HTTP verb requests to <em>/Dinners/Edit/[id]</em>URLs will go to the first Edit method we implemented (which did not have an [AcceptVerbs] attribute).</span></span>

| <span data-ttu-id="e4f11-195">**HTTP 동사를 통해 쪽 항목: 이유 구분?**</span><span class="sxs-lookup"><span data-stu-id="e4f11-195">**Side Topic: Why differentiate via HTTP verbs?**</span></span> |
| --- |
| <span data-ttu-id="e4f11-196">궁금할 – 단일 URL을 사용 하 고 HTTP 동사를 통해 해당 동작을 구분 했습니다 이유는 무엇 인가요?</span><span class="sxs-lookup"><span data-stu-id="e4f11-196">You might ask – why are we using a single URL and differentiating its behavior via the HTTP verb?</span></span> <span data-ttu-id="e4f11-197">편집 변경 내용 저장 및 로드를 처리 하는 두 개의 별도 Url을 방금 하면 안 되나요?</span><span class="sxs-lookup"><span data-stu-id="e4f11-197">Why not just have two separate URLs to handle loading and saving edit changes?</span></span> <span data-ttu-id="e4f11-198">예를 들어: /Dinners/편집 / [id] 초기 폼과 /Dinners/저장 / [id] 저장 하는 폼 게시를 처리 하도록 표시할?</span><span class="sxs-lookup"><span data-stu-id="e4f11-198">For example: /Dinners/Edit/[id] to display the initial form and /Dinners/Save/[id] to handle the form post to save it?</span></span> <span data-ttu-id="e4f11-199">두 개의 별도 Url 게시를 사용 하 여 단점은 경우 여기서 /Dinners/Save/2를 게시 하 고 HTML 폼 입력된 오류로 인해 다시 표시 해야 합니다 (이후에 브라우저의 주소 표시줄에 Dinners/저장/2 URL을 보유 하는 최종 사용자가 종료 됩니다. URL 형식에 게시).</span><span class="sxs-lookup"><span data-stu-id="e4f11-199">The downside with publishing two separate URLs is that in cases where we post to /Dinners/Save/2, and then need to redisplay the HTML form because of an input error, the end-user will end up having the /Dinners/Save/2 URL in their browser's address bar (since that was the URL the form posted to).</span></span> <span data-ttu-id="e4f11-200">최종 사용자가 해당 브라우저 즐겨찾기 목록에이 redisplayed 페이지 책갈피를 설정 하거나 URL 복사/붙여 넣습니다. 및 친구에 게 하는 경우 (해당 URL 게시 값에 따라 다름) 때문에 나중에 작동 하지 않는 URL을 저장 결국 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-200">If the end-user bookmarks this redisplayed page to their browser favorites list, or copy/pastes the URL and emails it to a friend, they will end up saving a URL that won't work in the future (since that URL depends on post values).</span></span> <span data-ttu-id="e4f11-201">단일 URL을 노출 하 여 (같은: 최종 사용자가 편집 페이지를 책갈피 및/또는 다른 사용자에 게 URL을 보냅니다 괜찮습니다 /Dinners/Edit/[id]) 및 HTTP 동사에서의 처리를 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-201">By exposing a single URL (like: /Dinners/Edit/[id]) and differentiating the processing of it by HTTP verb, it is safe for end-users to bookmark the edit page and/or send the URL to others.</span></span> |

#### <a name="retrieving-form-post-values"></a><span data-ttu-id="e4f11-202">폼 게시 값 검색</span><span class="sxs-lookup"><span data-stu-id="e4f11-202">Retrieving Form Post Values</span></span>

<span data-ttu-id="e4f11-203">다양 한 폼 매개 변수는 HTTP POST "편집" 메서드 내에서 게시 방법 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-203">There are a variety of ways we can access posted form parameters within our HTTP POST "Edit" method.</span></span> <span data-ttu-id="e4f11-204">한 가지 간단한 방법은 방금 폼 컬렉션에 액세스 하 여 게시 된 값을 직접 검색할 컨트롤러 기본 클래스에서 요청 속성을 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-204">One simple approach is to just use the Request property on the Controller base class to access the form collection and retrieve the posted values directly:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample10.cs)]

<span data-ttu-id="e4f11-205">위의 방법은 다소 복잡 하지만 오류 처리 논리를 추가 하는 면에 특히 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-205">The above approach is a little verbose, though, especially once we add error handling logic.</span></span>

<span data-ttu-id="e4f11-206">이 시나리오는 기본 제공을 활용 하는 방식이 더 효과적 *UpdateModel()* 컨트롤러 기본 클래스에서 도우미 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-206">A better approach for this scenario is to leverage the built-in *UpdateModel()* helper method on the Controller base class.</span></span> <span data-ttu-id="e4f11-207">들어오는 폼 매개 변수를 사용 하 여 전달 하는 개체의 속성 업데이트를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-207">It supports updating the properties of an object we pass it using the incoming form parameters.</span></span> <span data-ttu-id="e4f11-208">리플렉션을 사용 하 여 개체의 속성 이름을 확인 하 고 자동으로 변환 하 고에 클라이언트에서 제출한 입력된 값에 따라 값을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-208">It uses reflection to determine the property names on the object, and then automatically converts and assigns values to them based on the input values submitted by the client.</span></span>

<span data-ttu-id="e4f11-209">이 코드를 사용 하 여 HTTP POST 편집 작업을 간소화 하기 위해 UpdateModel() 메서드를 사용 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-209">We could use the UpdateModel() method to simplify our HTTP-POST Edit Action using this code:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample11.cs)]

<span data-ttu-id="e4f11-210">이제 방문할 수는 */Dinners/Edit/1* URL 및 우리의 Dinner의 제목 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-210">We can now visit the */Dinners/Edit/1* URL, and change the title of our Dinner:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image7.png)

<span data-ttu-id="e4f11-211">"저장" 단추를 클릭 하면 폼이 편집 작업을 수행 하겠습니다 및 업데이트 된 값이 데이터베이스에 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-211">When we click the "Save" button, we'll perform a form post to our Edit action, and the updated values will be persisted in the database.</span></span> <span data-ttu-id="e4f11-212">에서는 다음 리디렉션됩니다 정보 URL (새로 저장된 된 값이 표시 됩니다)는 저녁에:</span><span class="sxs-lookup"><span data-stu-id="e4f11-212">We will then be redirected to the Details URL for the Dinner (which will display the newly saved values):</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image8.png)

#### <a name="handling-edit-errors"></a><span data-ttu-id="e4f11-213">편집 오류 처리</span><span class="sxs-lookup"><span data-stu-id="e4f11-213">Handling Edit Errors</span></span>

<span data-ttu-id="e4f11-214">경우는 제외 –는 현재 HTTP POST 구현 작업이 제대로 수행 오류가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-214">Our current HTTP-POST implementation works fine – except when there are errors.</span></span>

<span data-ttu-id="e4f11-215">사용자 양식 편집 실수를 하면 폼은 해결 하도록 안내 하는 오류 정보 메시지와 함께 다시 표시 되도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-215">When a user makes a mistake editing a form, we need to make sure that the form is redisplayed with an informative error message that guides them to fix it.</span></span> <span data-ttu-id="e4f11-216">최종 사용자가 잘못 된 입력을 게시 하는 위치 하는 경우가 포함 됩니다 (예: 잘못 된 형식의 날짜 문자열로) 처럼 입력된 형식이 유효 인 사례와 이지만 비즈니스 규칙 위반을 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-216">This includes cases where an end-user posts incorrect input (for example: a malformed date string), as well as cases where the input format is valid but there is a business rule violation.</span></span> <span data-ttu-id="e4f11-217">오류가 발생 한 경우 양식에 사용자가 해당 변경 내용이 수동으로 충전 필요가 있도록 원래 입력 한 입력된 데이터를 유지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-217">When errors occur the form should preserve the input data the user originally entered so that they don't have to refill their changes manually.</span></span> <span data-ttu-id="e4f11-218">이 프로세스는 폼이 성공적으로 완료 될 때까지 필요한 횟수 만큼 반복 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-218">This process should repeat as many times as necessary until the form successfully completes.</span></span>

<span data-ttu-id="e4f11-219">ASP.NET MVC 오류 처리 및 양식 다시 쉽게 하는 몇 가지 유용한 기본 제공 기능이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-219">ASP.NET MVC includes some nice built-in features that make error handling and form redisplay easy.</span></span> <span data-ttu-id="e4f11-220">작업에서 이러한 기능을 보겠습니다 보려는 편집 작업 메서드를 다음 코드로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-220">To see these features in action let's update our Edit action method with the following code:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample12.cs)]

<span data-ttu-id="e4f11-221">위의 코드는 작업 주변 try/catch 오류 처리 블록에 배치 된 것을 제외 하 고 이전 구현-와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-221">The above code is similar to our previous implementation – except that we are now wrapping a try/catch error handling block around our work.</span></span> <span data-ttu-id="e4f11-222">예외가 발생 한 경우 UpdateModel()를 호출 하는 경우 또는 시도 하 고 (저장 하려고 Dinner 개체 모델 내에서 규칙 위반으로 인해 올바르지 않으면 예외가 발생 합니다)는 DinnerRepository를 저장 하는 경우이 catch 오류 처리 블록이 됩니다. 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-222">If an exception occurs either when calling UpdateModel(), or when we try and save the DinnerRepository (which will raise an exception if the Dinner object we are trying to save is invalid because of a rule violation within our model), our catch error handling block will execute.</span></span> <span data-ttu-id="e4f11-223">그 Dinner 개체에 있는 모든 규칙 위반을 반복 하 고 (곧 설명 하겠습니다)는 ModelState 개체에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-223">Within it we loop over any rule violations that exist in the Dinner object and add them to a ModelState object (which we'll discuss shortly).</span></span> <span data-ttu-id="e4f11-224">에서는 다음 뷰가 다시 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-224">We then redisplay the view.</span></span>

<span data-ttu-id="e4f11-225">이 확인 하려면 응용 프로그램을 다시 실행 해 보겠습니다 작업 저녁을 편집한 빈 제목을, "BOGUS"의 EventDate 있고 미국 국가 값을 사용 하 여 영국 전화 번호를 사용 하도록 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-225">To see this working let's re-run the application, edit a Dinner, and change it to have an empty Title, an EventDate of "BOGUS", and use a UK phone number with a country value of USA.</span></span> <span data-ttu-id="e4f11-226">"저장" 단추를 누르면에서는 HTTP POST 편집 메서드를 사용 하 여 하지 못하게 됩니다 (오류가 있기 때문에)를 저녁 식사를 저장 하 고 양식을 다시 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-226">When we press the "Save" button our HTTP POST Edit method will not be able to save the Dinner (because there are errors) and will redisplay the form:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image9.png)

<span data-ttu-id="e4f11-227">응용 프로그램에는 훌륭한 오류 환경이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-227">Our application has a decent error experience.</span></span> <span data-ttu-id="e4f11-228">잘못 된 입력이 포함 된 텍스트 요소는 빨간색으로 강조 표시 하 고 유효성 검사 오류 메시지에 대 한 최종 사용자에 게 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-228">The text elements with the invalid input are highlighted in red, and validation error messages are displayed to the end user about them.</span></span> <span data-ttu-id="e4f11-229">도 폼은 충전 아무 것도 하지 않아도 되도록 사용자가 입력 한 원래 – 입력된 데이터를 유지 해야.</span><span class="sxs-lookup"><span data-stu-id="e4f11-229">The form is also preserving the input data the user originally entered – so that they don't have to refill anything.</span></span>

<span data-ttu-id="e4f11-230">방법 인지 궁금할이 발생 했습니까?</span><span class="sxs-lookup"><span data-stu-id="e4f11-230">How, you might ask, did this occur?</span></span> <span data-ttu-id="e4f11-231">어떻게 않았습니다 EventDate, 제목과 ContactPhone 텍스트 상자 자체를 빨간색으로 강조 표시 하 고 원래 입력 한 사용자 값을 출력 하도록 알고?</span><span class="sxs-lookup"><span data-stu-id="e4f11-231">How did the Title, EventDate, and ContactPhone textboxes highlight themselves in red and know to output the originally entered user values?</span></span> <span data-ttu-id="e4f11-232">및 어떻게 않았습니다 오류 메시지 표시 맨 위에 있는 목록에서?</span><span class="sxs-lookup"><span data-stu-id="e4f11-232">And how did error messages get displayed in the list at the top?</span></span> <span data-ttu-id="e4f11-233">좋은 소식은 마법의이 발생 하지 않은-대신가 쉽게 입력된 유효성 검사 및 오류 처리 시나리오는 기본 제공 ASP.NET MVC 기능 중 일부를 사용 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-233">The good news is that this didn't occur by magic - rather it was because we used some of the built-in ASP.NET MVC features that make input validation and error handling scenarios easy.</span></span>

#### <a name="understanding-modelstate-and-the-validation-html-helper-methods"></a><span data-ttu-id="e4f11-234">ModelState 이해 및 유효성 검사 HTML 도우미 메서드</span><span class="sxs-lookup"><span data-stu-id="e4f11-234">Understanding ModelState and the Validation HTML Helper Methods</span></span>

<span data-ttu-id="e4f11-235">컨트롤러 클래스에는 오류를 보기에 전달 되는 모델 개체를 사용 하 여 없음을 표시 하는 방법을 제공 하는 "ModelState" 속성 컬렉션을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-235">Controller classes have a "ModelState" property collection which provides a way to indicate that errors exist with a model object being passed to a View.</span></span> <span data-ttu-id="e4f11-236">ModelState 컬렉션 내에서 오류 항목 문제를 사용 하 여 모델 속성의 이름을 식별 (예를 들어: "Title", "EventDate" 또는 "ContactPhone")를 지정 친숙 한 오류 메시지를 허용 하 고 (예: "Title이 필요 합니다").</span><span class="sxs-lookup"><span data-stu-id="e4f11-236">Error entries within the ModelState collection identify the name of the model property with the issue (for example: "Title", "EventDate", or "ContactPhone"), and allow a human-friendly error message to be specified (for example: "Title is required").</span></span>

<span data-ttu-id="e4f11-237">합니다 *UpdateModel()* 모델 개체에서 속성에 양식 값을 할당 하는 동안 오류가 발생할 경우 도우미 메서드 ModelState 컬렉션을 자동으로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-237">The *UpdateModel()* helper method automatically populates the ModelState collection when it encounters errors while trying to assign form values to properties on the model object.</span></span> <span data-ttu-id="e4f11-238">예를 들어 EventDate 속성은 Dinner 개체의 날짜/시간 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-238">For example, our Dinner object's EventDate property is of type DateTime.</span></span> <span data-ttu-id="e4f11-239">UpdateModel() 메서드 위의 시나리오에서 "BOGUS" 문자열 값을 할당할 수 없을 때 해당 속성을 사용 하 여 할당 오류를 나타내는 ModelState 컬렉션에 항목이 발생 UpdateModel() 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-239">When the UpdateModel() method was unable to assign the string value "BOGUS" to it in the scenario above, the UpdateModel() method added an entry to the ModelState collection indicating an assignment error had occurred with that property.</span></span>

<span data-ttu-id="e4f11-240">개발자는 "catch" 오류 처리 블록에서 현재 규칙 위반을 기준으로 항목을 사용 하 여 ModelState 컬렉션 채워지는 내에서 아래 수행 하는 것 처럼 ModelState 컬렉션에 오류 항목을 명시적으로 추가 하는 코드를 작성할 수도 합니다 저녁 식사 개체:</span><span class="sxs-lookup"><span data-stu-id="e4f11-240">Developers can also write code to explicitly add error entries into the ModelState collection like we are doing below within our "catch" error handling block, which is populating the ModelState collection with entries based on the active Rule Violations in the Dinner object:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample13.cs)]

#### <a name="html-helper-integration-with-modelstate"></a><span data-ttu-id="e4f11-241">ModelState와 html 도우미 통합</span><span class="sxs-lookup"><span data-stu-id="e4f11-241">Html Helper Integration with ModelState</span></span>

<span data-ttu-id="e4f11-242">HTML 도우미 메서드-Html.TextBox()-같은 출력을 렌더링할 때 ModelState 컬렉션을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-242">HTML helper methods - like Html.TextBox() - check the ModelState collection when rendering output.</span></span> <span data-ttu-id="e4f11-243">항목에 대 한 오류가 있는 경우 사용자가 입력 한 값과 CSS 오류 클래스를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-243">If an error for the item exists, they render the user-entered value and a CSS error class.</span></span>

<span data-ttu-id="e4f11-244">예를 들어, "편집" 보기에서는 사용 Html.TextBox() 도우미 메서드는 EventDate은 Dinner 개체의 렌더링:</span><span class="sxs-lookup"><span data-stu-id="e4f11-244">For example, in our "Edit" view we are using the Html.TextBox() helper method to render the EventDate of our Dinner object:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample14.aspx)]

<span data-ttu-id="e4f11-245">오류 시나리오에서 뷰를 렌더링 되 면 Html.TextBox() 메서드 ModelState 컬렉션은 Dinner 개체의 "EventDate" 속성과 관련 된 오류가 발생 한 경우 참조를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-245">When the view was rendered in the error scenario, the Html.TextBox() method checked the ModelState collection to see if there were any errors associated with the "EventDate" property of our Dinner object.</span></span> <span data-ttu-id="e4f11-246">오류가 발생 하는 것이 판단 하는 경우 값으로 제출 된 사용자 입력 ("BOGUS")를 렌더링 하 고 css 오류 클래스를 추가 합니다 &lt;입력 형식 = "textbox" /&gt; 태그 생성:</span><span class="sxs-lookup"><span data-stu-id="e4f11-246">When it determined that there was an error it rendered the submitted user input ("BOGUS") as the value, and added a css error class to the &lt;input type="textbox"/&gt; markup it generated:</span></span>

[!code-html[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample15.html)]

<span data-ttu-id="e4f11-247">하지만 원하는 검색할 css 오류 클래스의 모양을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-247">You can customize the appearance of the css error class to look however you want.</span></span> <span data-ttu-id="e4f11-248">– "입력-유효성 검사 오류" – 기본 CSS 오류 클래스에 정의 되어는 *\content\site.css* 아래와 같은 스타일 시트와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-248">The default CSS error class – "input-validation-error" – is defined in the *\content\site.css* stylesheet and looks like below:</span></span>

[!code-css[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample16.css)]

<span data-ttu-id="e4f11-249">이 CSS 규칙은 아래와 같은 강조 표시 하는 잘못 된 입력된 요소를 일으킨 원인을:</span><span class="sxs-lookup"><span data-stu-id="e4f11-249">This CSS rule is what caused our invalid input elements to be highlighted like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image10.png)

##### <a name="htmlvalidationmessage-helper-method"></a><span data-ttu-id="e4f11-250">Html.ValidationMessage() 도우미 메서드</span><span class="sxs-lookup"><span data-stu-id="e4f11-250">Html.ValidationMessage() Helper Method</span></span>

<span data-ttu-id="e4f11-251">특정 모델 속성과 관련 된 오류 메시지가 출력 ModelState Html.ValidationMessage() 도우미 메서드를 사용할 수 있습니다.:</span><span class="sxs-lookup"><span data-stu-id="e4f11-251">The Html.ValidationMessage() helper method can be used to output the ModelState error message associated with a particular model property:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample17.aspx)]

<span data-ttu-id="e4f11-252">위의 코드 출력:  *&lt;p a n class = "필드 유효성 검사 오류"&gt; 'BOGUS' 값이 올바르지 않습니다&lt;s&gt;*</span><span class="sxs-lookup"><span data-stu-id="e4f11-252">The above code outputs: *&lt;span class="field-validation-error"&gt; The value ‘BOGUS' is invalid&lt;/span&gt;*</span></span>

<span data-ttu-id="e4f11-253">Html.ValidationMessage() 도우미 메서드는 또한 개발자가 표시 되는 오류 텍스트 메시지를 재정의할 수 있도록 하는 두 번째 매개 변수를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-253">The Html.ValidationMessage() helper method also supports a second parameter that allows developers to override the error text message that is displayed:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample18.aspx)]

<span data-ttu-id="e4f11-254">위의 코드 출력:  <em>&lt;p a n class = "필드 유효성 검사 오류"&gt;\*&lt;s&gt;</em>기본 오류 텍스트에 대 한 오류가 있으면 대신 합니다 EventDate 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-254">The above code outputs: <em>&lt;span class="field-validation-error"&gt;\*&lt;/span&gt;</em>instead of the default error text when an error is present for the EventDate property.</span></span>

##### <a name="htmlvalidationsummary-helper-method"></a><span data-ttu-id="e4f11-255">Html.ValidationSummary() 도우미 메서드</span><span class="sxs-lookup"><span data-stu-id="e4f11-255">Html.ValidationSummary() Helper Method</span></span>

<span data-ttu-id="e4f11-256">와 함께 요약 오류 메시지를 렌더링할 Html.ValidationSummary() 도우미 메서드를 사용할 수는 &lt;ul&gt;&lt;li /&gt;&lt;/u l&gt; 목록을 모두 자세한 오류 메시지는 ModelState 컬렉션:</span><span class="sxs-lookup"><span data-stu-id="e4f11-256">The Html.ValidationSummary() helper method can be used to render a summary error message, accompanied by a &lt;ul&gt;&lt;li/&gt;&lt;/ul&gt; list of all detailed error messages in the ModelState collection:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image11.png)

<span data-ttu-id="e4f11-257">Html.ValidationSummary() 도우미 메서드를 사용 하는 자세한 오류 목록 위에 표시할 요약 오류 메시지를 정의 하는 선택적 문자열 매개-변수:</span><span class="sxs-lookup"><span data-stu-id="e4f11-257">The Html.ValidationSummary() helper method takes an optional string parameter – which defines a summary error message to display above the list of detailed errors:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample19.aspx)]

<span data-ttu-id="e4f11-258">필요에 따라 오류 목록 모양을 재정의 하려면 CSS를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-258">You can optionally use CSS to override what the error list looks like.</span></span>

#### <a name="using-a-addruleviolations-helper-method"></a><span data-ttu-id="e4f11-259">AddRuleViolations 도우미 메서드를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="e4f11-259">Using a AddRuleViolations Helper Method</span></span>

<span data-ttu-id="e4f11-260">해당 catch 블록 내에서 foreach 문을 Dinner 개체의 규칙 위반을 반복 하 여 컨트롤러의 ModelState 컬렉션에 추가 하는 데 사용 하는 초기 HTTP POST 편집 구현:</span><span class="sxs-lookup"><span data-stu-id="e4f11-260">Our initial HTTP-POST Edit implementation used a foreach statement within its catch block to loop over the Dinner object's Rule Violations and add them to the controller's ModelState collection:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample20.cs)]

<span data-ttu-id="e4f11-261">에서는이 코드는 "ControllerHelpers"를 추가 하 여 거의 깔끔하고 NerdDinner 프로젝트에 클래스 및 도우미 메서드는 ASP.NET MVC ModelStateDictionary 클래스를 추가 하는 그 안에 "AddRuleViolations" 확장 메서드를 구현 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-261">We can make this code a little cleaner by adding a "ControllerHelpers" class to the NerdDinner project, and implement an "AddRuleViolations" extension method within it that adds a helper method to the ASP.NET MVC ModelStateDictionary class.</span></span> <span data-ttu-id="e4f11-262">이 확장 메서드 ModelStateDictionary RuleViolation 오류 목록을 채우는 데 필요한 논리를 캡슐화 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-262">This extension method can encapsulate the logic necessary to populate the ModelStateDictionary with a list of RuleViolation errors:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample21.cs)]

<span data-ttu-id="e4f11-263">그런 다음이 확장 메서드는 Dinner 규칙 위반을 사용 하 여 ModelState 컬렉션을 채우는 데 사용 하는 HTTP POST 편집 작업 메서드를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-263">We can then update our HTTP-POST Edit action method to use this extension method to populate the ModelState collection with our Dinner Rule Violations.</span></span>

#### <a name="complete-edit-action-method-implementations"></a><span data-ttu-id="e4f11-264">편집 작업 메서드 구현은 완료</span><span class="sxs-lookup"><span data-stu-id="e4f11-264">Complete Edit Action Method Implementations</span></span>

<span data-ttu-id="e4f11-265">아래 코드의 모든 편집 시나리오에 필요한 컨트롤러 논리를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-265">The code below implements all of the controller logic necessary for our Edit scenario:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample22.cs)]

<span data-ttu-id="e4f11-266">편집 구현에 대 한 가지 좋은 점은 컨트롤러 클래스도 아니고 보기 템플릿은 Dinner 모델에 의해 적용 되는 비즈니스 규칙 또는 특정 유효성 검사에 대 한 모든 것을 알아야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-266">The nice thing about our Edit implementation is that neither our Controller class nor our View template has to know anything about the specific validation or business rules being enforced by our Dinner model.</span></span> <span data-ttu-id="e4f11-267">모델에 추가 규칙 나중에 추가할 수 있습니다 하 고 컨트롤러 또는 보기에서 순서 대로 지원 하기 위해 코드 변경할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-267">We can add additional rules to our model in the future and do not have to make any code changes to our controller or view in order for them to be supported.</span></span> <span data-ttu-id="e4f11-268">이 응용 프로그램의 요구 사항을 나중에 최소를 사용 하 여 코드 변경 내용 쉽게 발전 하는 유연 하 게 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-268">This provides us with the flexibility to easily evolve our application requirements in the future with a minimum of code changes.</span></span>

### <a name="create-support"></a><span data-ttu-id="e4f11-269">만들기 지원</span><span class="sxs-lookup"><span data-stu-id="e4f11-269">Create Support</span></span>

<span data-ttu-id="e4f11-270">구현 DinnersController 클래스의 "편집" 동작을 마쳤습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-270">We've finished implementing the "Edit" behavior of our DinnersController class.</span></span> <span data-ttu-id="e4f11-271">보겠습니다 이제 이동할에 – 사용자가 새 Dinners에 추가할 수 있도록 해 주는 "만들기" 지원을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-271">Let's now move on to implement the "Create" support on it – which will enable users to add new Dinners.</span></span>

#### <a name="the-http-get-create-action-method"></a><span data-ttu-id="e4f11-272">HTTP GET 작업 메서드 만들기</span><span class="sxs-lookup"><span data-stu-id="e4f11-272">The HTTP-GET Create Action Method</span></span>

<span data-ttu-id="e4f11-273">HTTP "GET" 동작을 구현 하 여 먼저는 작업 메서드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-273">We'll begin by implementing the HTTP "GET" behavior of our create action method.</span></span> <span data-ttu-id="e4f11-274">사용자가 방문 하면이 메서드가 호출 됩니다 합니다 *Dinners/만들기* URL입니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-274">This method will be called when someone visits the */Dinners/Create* URL.</span></span> <span data-ttu-id="e4f11-275">구현은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-275">Our implementation looks like:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample23.cs)]

<span data-ttu-id="e4f11-276">위의 코드 새 Dinner 개체를 만들고 해당 EventDate 속성을 나중에 1 주일 수를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-276">The code above creates a new Dinner object, and assigns its EventDate property to be one week in the future.</span></span> <span data-ttu-id="e4f11-277">그런 다음 새 Dinner 개체를 기반으로 하는 뷰를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-277">It then renders a View that is based on the new Dinner object.</span></span> <span data-ttu-id="e4f11-278">이름을 명시적으로 전달 하지 않았으므로 합니다 *View()* 도우미 메서드를 보기 템플릿은 해결 하려면 규칙 기반 기본 경로 사용 하면 해당: /Views/Dinners/Create.aspx 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-278">Because we haven't explicitly passed a name to the *View()* helper method, it will use the convention based default path to resolve the view template: /Views/Dinners/Create.aspx.</span></span>

<span data-ttu-id="e4f11-279">이 보기 템플릿은 이제 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-279">Let's now create this view template.</span></span> <span data-ttu-id="e4f11-280">만들기 작업 메서드 내에서 마우스 오른쪽 단추로 클릭 하 고 "추가 보기" 상황에 맞는 메뉴 명령을 선택 하 여이 작업을 수행 수입니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-280">We can do this by right-clicking within the Create action method and selecting the "Add View" context menu command.</span></span> <span data-ttu-id="e4f11-281">"뷰 추가" 대화 상자 내에서 보기 템플릿에 Dinner 개체를 전달 하는 것 및 자동-스 캐 폴드를 "만들기" 템플릿을 선택 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-281">Within the "Add View" dialog we'll indicate that we are passing a Dinner object to the view template, and choose to auto-scaffold a "Create" template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image12.png)

<span data-ttu-id="e4f11-282">"추가" 단추를 클릭 하는 경우 Visual Studio 새 스 캐 폴드 기반 "Create.aspx" 보기 "\Views\Dinners" 디렉터리에 저장 되며 IDE 내에서 열어 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-282">When we click the "Add" button, Visual Studio will save a new scaffold-based "Create.aspx" view to the "\Views\Dinners" directory, and open it up within the IDE:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image13.png)

<span data-ttu-id="e4f11-283">보겠습니다 우리에 게 있어 기본 "만들기" 스 캐 폴드 파일 생성 된 몇 가지 변경 하 고 다음과 같이 표시를 수정:</span><span class="sxs-lookup"><span data-stu-id="e4f11-283">Let's make a few changes to the default "create" scaffold file that was generated for us, and modify it up to look like below:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample24.aspx)]

<span data-ttu-id="e4f11-284">이제을 실행할 때이 응용 프로그램 및 액세스 하 고는 *"/ Dinners/만들기"* 만들기 작업 구현에서 아래와 같은 UI 렌더링 됩니다 브라우저 내에서 URL:</span><span class="sxs-lookup"><span data-stu-id="e4f11-284">And now when we run our application and access the *"/Dinners/Create"* URL within the browser it will render UI like below from our Create action implementation:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image14.png)

#### <a name="implementing-the-http-post-create-action-method"></a><span data-ttu-id="e4f11-285">동작 메서드를 만드는 HTTP POST를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-285">Implementing the HTTP-POST Create Action Method</span></span>

<span data-ttu-id="e4f11-286">HTTP GET 메서드 버전을이 만들기 작업 구현 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-286">We have the HTTP-GET version of our Create action method implemented.</span></span> <span data-ttu-id="e4f11-287">폼 post를 실행 하 고 "저장" 단추를 클릭할 때 수행 합니다 *Dinners/만들기* URL HTML 제출 &lt;입력&gt; HTTP POST 동사를 사용 하 여 값을 형성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-287">When a user clicks the "Save" button it performs a form post to the */Dinners/Create* URL, and submits the HTML &lt;input&gt; form values using the HTTP POST verb.</span></span>

<span data-ttu-id="e4f11-288">HTTP POST 동작을 이제 구현 해 보겠습니다 우리의 작업 메서드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-288">Let's now implement the HTTP POST behavior of our create action method.</span></span> <span data-ttu-id="e4f11-289">HTTP POST 시나리오 처리 여부를 나타내는 "AcceptVerbs" 특성에는 우리의 DinnersController 오버 로드 "만들기" 작업 메서드도 추가 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-289">We'll begin by adding an overloaded "Create" action method to our DinnersController that has an "AcceptVerbs" attribute on it that indicates it handles HTTP POST scenarios:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample25.cs)]

<span data-ttu-id="e4f11-290">다양 한 방법으로 게시 된 폼 매개 변수는 HTTP POST를 사용 하도록 설정 "만들기" 메서드 내에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-290">There are a variety of ways we can access the posted form parameters within our HTTP-POST enabled "Create" method.</span></span>

<span data-ttu-id="e4f11-291">한 가지 방법은 새 Dinner 개체를 만들고 사용 하 여 하는 *UpdateModel()* 도우미 메서드 (예: 수행한 편집 작업을 사용 하 여) 게시 된 양식 값으로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-291">One approach is to create a new Dinner object and then use the *UpdateModel()* helper method (like we did with the Edit action) to populate it with the posted form values.</span></span> <span data-ttu-id="e4f11-292">우리의 DinnerRepository를 추가 하 고 데이터베이스에 유지 다음 아래 코드를 사용 하 여 새로 만든된 저녁을 표시 하는 세부 정보 작업에 사용자를 리디렉션한 다음 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-292">We can then add it to our DinnerRepository, persist it to the database, and redirect the user to our Details action to show the newly created Dinner using the code below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample26.cs)]

<span data-ttu-id="e4f11-293">또는 메서드 매개 변수로 Dinner 개체를 사용 하는 create () 동작 메서드에 있는 접근 방식을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-293">Alternatively, we can use an approach where we have our Create() action method take a Dinner object as a method parameter.</span></span> <span data-ttu-id="e4f11-294">ASP.NET MVC는 다음 자동으로 한 새 Dinner 개체를 인스턴스화, 양식 입력을 사용 하 여 해당 속성 채우고 우리의 작업 메서드에 전달:</span><span class="sxs-lookup"><span data-stu-id="e4f11-294">ASP.NET MVC will then automatically instantiate a new Dinner object for us, populate its properties using the form inputs, and pass it to our action method:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample27.cs)]

<span data-ttu-id="e4f11-295">위의 작업 메서드는 Dinner 개체에 성공적으로 채워졌는지 폼 게시 값을 사용 하 여 ModelState.IsValid 속성을 확인 하 여 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-295">Our action method above verifies that the Dinner object has been successfully populated with the form post values by checking the ModelState.IsValid property.</span></span> <span data-ttu-id="e4f11-296">없으면 false 변환 문제 입력이 반환 됩니다 (예: EventDate 속성에 대 한 "BOGUS" 문자열), 문제가 있는 경우이 동작 메서드에 다시 표시 되 고 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-296">This will return false if there are input conversion issues (for example: a string of "BOGUS" for the EventDate property), and if there are any issues our action method redisplays the form.</span></span>

<span data-ttu-id="e4f11-297">입력된 값이 유효 하면 동작 메서드를 추가 하 고 새 저녁 식사를 DinnerRepository 저장을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-297">If the input values are valid, then the action method attempts to add and save the new Dinner to the DinnerRepository.</span></span> <span data-ttu-id="e4f11-298">Try/catch 블록 내에서이 작업을 래핑하고 다시 표시 되는 경우 (유발 하는 예외를 발생 시키려면 dinnerRepository.Save() 메서드)는 비즈니스 규칙 위반 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-298">It wraps this work within a try/catch block and redisplays the form if there are any business rule violations (which would cause the dinnerRepository.Save() method to raise an exception).</span></span>

<span data-ttu-id="e4f11-299">이 오류 처리 동작의 동작을 확인 하려면 요청 수를 *Dinners/만들기* URL 및 새 저녁에 대 한 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-299">To see this error handling behavior in action, we can request the */Dinners/Create* URL and fill out details about a new Dinner.</span></span> <span data-ttu-id="e4f11-300">잘못 된 입력 또는 값에는 아래와 같은 강조 표시 하는 오류와 함께 다시 표시 하려면 폼 만들기 하면 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-300">Incorrect input or values will cause the create form to be redisplayed with the errors highlighted like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image15.png)

<span data-ttu-id="e4f11-301">만들기 폼 정확히 동일한 유효성 검사 및 비즈니스 규칙을 편집 양식에 인식 하는 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-301">Notice how our Create form is honoring the exact same validation and business rules as our Edit form.</span></span> <span data-ttu-id="e4f11-302">이 유효성 검사 및 비즈니스 모델에 정의 된 규칙과 UI 또는 응용 프로그램의 컨트롤러 내에서 포함 되지 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-302">This is because our validation and business rules were defined in the model, and were not embedded within the UI or controller of the application.</span></span> <span data-ttu-id="e4f11-303">즉, 있습니다 나중에 변경/발전시키는 유효성 검사 또는 비즈니스 규칙에서 단일 배치 하 고 응용 프로그램 전체에서 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-303">This means we can later change/evolve our validation or business rules in a single place and have them apply throughout our application.</span></span> <span data-ttu-id="e4f11-304">우리는 필요가 없습니다 내에서 모든 코드는 편집 변경 또는 새 규칙이 나 기존 수정 사항이 자동으로 적용 하도록 동작 메서드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-304">We will not have to change any code within either our Edit or Create action methods to automatically honor any new rules or modifications to existing ones.</span></span>

<span data-ttu-id="e4f11-305">입력된 값을 수정 하 고 "저장" 단추를 클릭 합니다 DinnerRepository에는 추가 성공 하 고 데이터베이스에 추가할 새 Dinner 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-305">When we fix the input values and click the "Save" button again, our addition to the DinnerRepository will succeed, and a new Dinner will be added to the database.</span></span> <span data-ttu-id="e4f11-306">에서는 다음 리디렉션됩니다 합니다 */Dinners 세부 정보 / [id]* URL – 새로 만든된 저녁에 대 한 정보를 사용 하 여 우리가 표시 하는 위치:</span><span class="sxs-lookup"><span data-stu-id="e4f11-306">We will then be redirected to the */Dinners/Details/[id]* URL – where we will be presented with details about the newly created Dinner:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image16.png)

### <a name="delete-support"></a><span data-ttu-id="e4f11-307">Delete 지원</span><span class="sxs-lookup"><span data-stu-id="e4f11-307">Delete Support</span></span>

<span data-ttu-id="e4f11-308">우리의 DinnersController에 "삭제" 지원을 지금 추가 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-308">Let's now add "Delete" support to our DinnersController.</span></span>

#### <a name="the-http-get-delete-action-method"></a><span data-ttu-id="e4f11-309">HTTP GET Delete 동작 메서드</span><span class="sxs-lookup"><span data-stu-id="e4f11-309">The HTTP-GET Delete Action Method</span></span>

<span data-ttu-id="e4f11-310">Delete 동작 메서드는 HTTP GET 동작을 구현 하 여 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-310">We'll begin by implementing the HTTP GET behavior of our delete action method.</span></span> <span data-ttu-id="e4f11-311">사용자가 방문 하면이 메서드가 호출 됩니다 합니다 */Dinners/삭제 / [id]* URL입니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-311">This method will get called when someone visits the */Dinners/Delete/[id]* URL.</span></span> <span data-ttu-id="e4f11-312">다음은 구현이입니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-312">Below is the implementation:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample28.cs)]

<span data-ttu-id="e4f11-313">작업 메서드는 삭제할 저녁 식사를 검색 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-313">The action method attempts to retrieve the Dinner to be deleted.</span></span> <span data-ttu-id="e4f11-314">Dinner 있는 렌더링 하는 경우 뷰 개체를 기준으로 Dinner 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-314">If the Dinner exists it renders a View based on the Dinner object.</span></span> <span data-ttu-id="e4f11-315">개체 (없거나 이미 삭제 된) 해당 하는 경우 "NotFound"를 렌더링 하는 뷰를 반환 우리의 "Details" 동작 메서드에 대 한 이전에 만든 서식 파일을 보려면.</span><span class="sxs-lookup"><span data-stu-id="e4f11-315">If the object doesn't exist (or has already been deleted) it returns a View that renders the "NotFound" view template we created earlier for our "Details" action method.</span></span>

<span data-ttu-id="e4f11-316">Delete 동작 메서드 내에서 마우스 오른쪽 단추로 클릭 하 고 "추가 보기" 상황에 맞는 메뉴 명령을 선택 하 여 "삭제" 보기 템플릿을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-316">We can create the "Delete" view template by right-clicking within the Delete action method and selecting the "Add View" context menu command.</span></span> <span data-ttu-id="e4f11-317">"뷰 추가" 대화 상자 내 보기 템플릿은 해당 모델로 Dinner 개체를 전달 하는 것 및 빈 템플릿을 만들려는 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-317">Within the "Add View" dialog we'll indicate that we are passing a Dinner object to our view template as its model, and choose to create an empty template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image17.png)

<span data-ttu-id="e4f11-318">"추가" 단추를 클릭 하는 경우 Visual Studio는이 "\Views\Dinners" 디렉터리 내에서 새 "Delete.aspx" 보기 템플릿 파일을를에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-318">When we click the "Add" button, Visual Studio will add a new "Delete.aspx" view template file for us within our "\Views\Dinners" directory.</span></span> <span data-ttu-id="e4f11-319">일부 HTML 및 코드 삭제 확인 화면이 구현 하려면 템플릿에 추가 아래와 같은:</span><span class="sxs-lookup"><span data-stu-id="e4f11-319">We'll add some HTML and code to the template to implement a delete confirmation screen like below:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample29.aspx)]

<span data-ttu-id="e4f11-320">위의 코드는 삭제할 Dinner 및 출력의 제목을 표시를 &lt;폼&gt; 최종 사용자가 그 안에 "삭제" 단추를 클릭 하면 /Dinners/삭제 / [id] URL에 POST를 수행 하는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-320">The code above displays the title of the Dinner to be deleted, and outputs a &lt;form&gt; element that does a POST to the /Dinners/Delete/[id] URL if the end-user clicks the "Delete" button within it.</span></span>

<span data-ttu-id="e4f11-321">액세스 회원과 응용 프로그램을 실행할 때 합니다 *"/ Dinners/삭제 / [id]"* 유효한 저녁에 대 한 URL 개체 아래와 같은 UI 렌더링:</span><span class="sxs-lookup"><span data-stu-id="e4f11-321">When we run our application and access the *"/Dinners/Delete/[id]"* URL for a valid Dinner object it renders UI like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image18.png)

| <span data-ttu-id="e4f11-322">**쪽 항목: 우리가 왜 게시물?**</span><span class="sxs-lookup"><span data-stu-id="e4f11-322">**Side Topic: Why are we doing a POST?**</span></span> |
| --- |
| <span data-ttu-id="e4f11-323">궁금할 – 이유는 무엇 일까요의 노력을 통해는 &lt;폼&gt; 우리의 삭제 확인 화면 내에서?</span><span class="sxs-lookup"><span data-stu-id="e4f11-323">You might ask – why did we go through the effort of creating a &lt;form&gt; within our Delete confirmation screen?</span></span> <span data-ttu-id="e4f11-324">실제 삭제 작업을 수행 하는 동작 메서드에 연결 표준 하이퍼링크를 방금 사용 하지 않는 이유는?</span><span class="sxs-lookup"><span data-stu-id="e4f11-324">Why not just use a standard hyperlink to link to an action method that does the actual delete operation?</span></span> <span data-ttu-id="e4f11-325">이유는 웹 크롤러에 대비 하 고 검색 엔진 Url을 검색 하 고 링크를 따릅니까 때 삭제할 데이터를 실수로 인해 주의 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-325">The reason is because we want to be careful to guard against web-crawlers and search engines discovering our URLs and inadvertently causing data to be deleted when they follow the links.</span></span> <span data-ttu-id="e4f11-326">HTTP GET 기반 Url 액세스/탐색 하기 위해 "안전한" 것으로 간주 됩니다 및 HTTP-POST 작업을 수행 하지 할 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-326">HTTP-GET based URLs are considered "safe" for them to access/crawl, and they are supposed to not follow HTTP-POST ones.</span></span> <span data-ttu-id="e4f11-327">항상 안전 하지 않은 배치 또는 HTTP POST 요청 뒤 데이터 수정 작업 해야 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-327">A good rule is to make sure you always put destructive or data modifying operations behind HTTP-POST requests.</span></span> |

#### <a name="implementing-the-http-post-delete-action-method"></a><span data-ttu-id="e4f11-328">HTTP POST Delete 동작 메서드를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-328">Implementing the HTTP-POST Delete Action Method</span></span>

<span data-ttu-id="e4f11-329">이제 삭제 확인 화면이 표시 하는 구현 하는 Delete 동작 메서드의 GET HTTP 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-329">We now have the HTTP-GET version of our Delete action method implemented which displays a delete confirmation screen.</span></span> <span data-ttu-id="e4f11-330">최종 사용자가 "삭제" 단추를 클릭 하면 폼 post를 수행 합니다 */Dinners Dinner / [id]* URL입니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-330">When an end user clicks the "Delete" button it will perform a form post to the */Dinners/Dinner/[id]* URL.</span></span>

<span data-ttu-id="e4f11-331">아래 코드를 사용 하 여 삭제 작업 메서드의 HTTP "POST" 동작을 이제 구현 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-331">Let's now implement the HTTP "POST" behavior of the delete action method using the code below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample30.cs)]

<span data-ttu-id="e4f11-332">Delete 동작 메서드는 HTTP POST 버전이 삭제 하려면 dinner 개체를 검색 하려고 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-332">The HTTP-POST version of our Delete action method attempts to retrieve the dinner object to delete.</span></span> <span data-ttu-id="e4f11-333">(이미 삭제 된) 때문이 찾을 수 없는 경우 "NotFound" 템플릿은 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-333">If it can't find it (because it has already been deleted) it renders our "NotFound" template.</span></span> <span data-ttu-id="e4f11-334">Dinner를 찾으면는 DinnerRepository에서 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-334">If it finds the Dinner, it deletes it from the DinnerRepository.</span></span> <span data-ttu-id="e4f11-335">"삭제" 템플릿을 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-335">It then renders a "Deleted" template.</span></span>

<span data-ttu-id="e4f11-336">"삭제" 템플릿을 구현 하에서는 작업 메서드에서 마우스 오른쪽 단추로 클릭 하 고 "추가 보기" 상황에 맞는 메뉴를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-336">To implement the "Deleted" template we'll right-click in the action method and choose the "Add View" context menu.</span></span> <span data-ttu-id="e4f11-337">"삭제" 보기 이름을 하 고 빈 템플릿을 수 (및 강력한 형식의 모델 개체를 사용 하지) 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-337">We'll name our view "Deleted" and have it be an empty template (and not take a strongly-typed model object).</span></span> <span data-ttu-id="e4f11-338">일부 HTML 콘텐츠를 추가 하겠습니다 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-338">We'll then add some HTML content to it:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample31.aspx)]

<span data-ttu-id="e4f11-339">이제을 실행할 때이 응용 프로그램 및 액세스 하 고는 *"/ Dinners/삭제 / [id]"* 우리의 저녁 렌더링할 개체 삭제 확인 하는 유효한 저녁 URL 아래와 같은 화면:</span><span class="sxs-lookup"><span data-stu-id="e4f11-339">And now when we run our application and access the *"/Dinners/Delete/[id]"* URL for a valid Dinner object it will render our Dinner delete confirmation screen like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image19.png)

<span data-ttu-id="e4f11-340">"삭제" 단추를 클릭 하는 경우에 HTTP POST를 수행 합니다 */Dinners/삭제 / [id]* Dinner에서는 데이터베이스에서 삭제 하 고 "삭제" 보기 템플릿은 표시 URL:</span><span class="sxs-lookup"><span data-stu-id="e4f11-340">When we click the "Delete" button it will perform an HTTP-POST to the */Dinners/Delete/[id]* URL, which will delete the Dinner from our database, and display our "Deleted" view template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image20.png)

### <a name="model-binding-security"></a><span data-ttu-id="e4f11-341">모델 바인딩 보안</span><span class="sxs-lookup"><span data-stu-id="e4f11-341">Model Binding Security</span></span>

<span data-ttu-id="e4f11-342">ASP.NET MVC의 기본 모델 바인딩 기능을 사용 하는 두 가지에 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-342">We've discussed two different ways to use the built-in model-binding features of ASP.NET MVC.</span></span> <span data-ttu-id="e4f11-343">먼저 UpdateModel() 메서드를 사용 하 여 기존 모델 개체에 속성을 업데이트 하 고 사용 하 여 두 번째 모델 개체의 동작 메서드 매개 변수로 전달 하는 것에 대 한 ASP.NET MVC의 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-343">The first using the UpdateModel() method to update properties on an existing model object, and the second using ASP.NET MVC's support for passing model objects in as action method parameters.</span></span> <span data-ttu-id="e4f11-344">이러한 기술은 모두 매우 강력 하 고 매우 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-344">Both of these techniques are very powerful and extremely useful.</span></span>

<span data-ttu-id="e4f11-345">이 power 하면 책임입니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-345">This power also brings with it responsibility.</span></span> <span data-ttu-id="e4f11-346">것은 항상 보안에 대 한 편집 광 사용자 입력을 수락 하는 경우에 마찬가지 양식 입력 개체에 바인딩할 때 하며</span><span class="sxs-lookup"><span data-stu-id="e4f11-346">It is important to always be paranoid about security when accepting any user input, and this is also true when binding objects to form input.</span></span> <span data-ttu-id="e4f11-347">에 주의 해야 항상 HTML 인코딩 HTML 및 JavaScript 주입 공격을 방지 하 고 SQL 주입 공격에 주의 해야 사용자가 입력 한 값 (참고:이 응용 프로그램을 자동으로이 방지 하기 위해 매개 변수를 인코딩하는 방법에 대 한 LINQ to SQL 사용 공격 형식)입니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-347">You should be careful to always HTML encode any user-entered values to avoid HTML and JavaScript injection attacks, and be careful of SQL injection attacks (note: we are using LINQ to SQL for our application, which automatically encodes parameters to prevent these types of attacks).</span></span> <span data-ttu-id="e4f11-348">되지 단독으로 클라이언트 쪽 유효성 검사에 의존 하 고 항상 해커 위조 값을 보내려는 시도 방지 하기 위해 서버 쪽 유효성 검사를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-348">You should never rely on client-side validation alone, and always employ server-side validation to guard against hackers attempting to send you bogus values.</span></span>

<span data-ttu-id="e4f11-349">ASP.NET MVC의 바인딩 기능을 사용 하는 경우에 대해 생각해 야 되도록 한 추가 보안 항목에 바인딩하는 개체의 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-349">One additional security item to make sure you think about when using the binding features of ASP.NET MVC is the scope of the objects you are binding.</span></span> <span data-ttu-id="e4f11-350">특히 허용 바인딩될 실제로 업데이트할 최종 사용자가 업데이트할 수 있는 해야 하는 속성만 허용 되는지 확인 하는 속성의 보안 의미를 파악 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-350">Specifically, you want to make sure you understand the security implications of the properties you are allowing to be bound, and make sure you only allow those properties that really should be updatable by an end-user to be updated.</span></span>

<span data-ttu-id="e4f11-351">기본적으로 UpdateModel() 메서드는 들어오는 형식 매개 변수 값과 일치 하는 모델 개체에서 모든 속성을 업데이트 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-351">By default, the UpdateModel() method will attempt to update all properties on the model object that match incoming form parameter values.</span></span> <span data-ttu-id="e4f11-352">마찬가지로, 기본적으로도 작업 메서드 매개 변수로 전달 된 개체 형식 매개 변수를 통해 설정 하는 해당 속성을 모두 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-352">Likewise, objects passed as action method parameters also by default can have all of their properties set via form parameters.</span></span>

#### <a name="locking-down-binding-on-a-per-usage-basis"></a><span data-ttu-id="e4f11-353">사용 당 기준 바인딩 잠금</span><span class="sxs-lookup"><span data-stu-id="e4f11-353">Locking down binding on a per-usage basis</span></span>

<span data-ttu-id="e4f11-354">제공 하는 명시적 "include 목록" 업데이트할 수 있는 속성의 바인딩 정책 사용 당 단위로 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-354">You can lock down the binding policy on a per-usage basis by providing an explicit "include list" of properties that can be updated.</span></span> <span data-ttu-id="e4f11-355">이 아래와 같은 UpdateModel() 메서드에 추가 하는 문자열 배열 매개 변수에 전달 하 여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-355">This can be done by passing an extra string array parameter to the UpdateModel() method like below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample32.cs)]

<span data-ttu-id="e4f11-356">또한 작업 메서드 매개 변수로 전달 된 개체는 "include 목록"의 속성을 아래와 같은 지정을 사용할 수 있도록 [바인딩] 특성을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-356">Objects passed as action method parameters also support a [Bind] attribute that enables an "include list" of allowed properties to be specified like below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample33.cs)]

#### <a name="locking-down-binding-on-a-type-basis"></a><span data-ttu-id="e4f11-357">바인딩 형식으로 잠그지</span><span class="sxs-lookup"><span data-stu-id="e4f11-357">Locking down binding on a type basis</span></span>

<span data-ttu-id="e4f11-358">형식당 하나의 단위로 바인딩 규칙을 제한할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-358">You can also lock down the binding rules on a per-type basis.</span></span> <span data-ttu-id="e4f11-359">따라서 모든 컨트롤러 및 작업 메서드 (UpdateModel와 작업 메서드 매개 변수 시나리오 포함)는 모든 시나리오에 적용할 수 있도록 및 바인딩 규칙을 한 번만 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-359">This allows you to specify the binding rules once, and then have them apply in all scenarios (including both UpdateModel and action method parameter scenarios) across all controllers and action methods.</span></span>

<span data-ttu-id="e4f11-360">형식으로 [바인딩] 특성을 추가 하거나 (형식이 없고 시나리오에 유용) 응용 프로그램의 Global.asax 파일 내에서 등록 하 여 형식당 하나의 바인딩 규칙을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-360">You can customize the per-type binding rules by adding a [Bind] attribute onto a type, or by registering it within the Global.asax file of the application (useful for scenarios where you don't own the type).</span></span> <span data-ttu-id="e4f11-361">바인딩 특성의 포함을 사용할 수 있습니다. 제외 되는 속성을 제어 하는 속성은 특정 클래스 또는 인터페이스에 대 한 바인딩 가능한 하며</span><span class="sxs-lookup"><span data-stu-id="e4f11-361">You can then use the Bind attribute's Include and Exclude properties to control which properties are bindable for the particular class or interface.</span></span>

<span data-ttu-id="e4f11-362">NerdDinner 응용 프로그램에서는 Dinner 클래스에 대 한이 기술을 사용 하 고 다음 바인딩 가능한 속성의 목록을 제한 하 고 [바인딩] 특성을 추가할 것:</span><span class="sxs-lookup"><span data-stu-id="e4f11-362">We'll use this technique for the Dinner class in our NerdDinner application, and add a [Bind] attribute to it that restricts the list of bindable properties to the following:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample34.cs)]

<span data-ttu-id="e4f11-363">바인딩을 통해 조작할 않으십니까 컬렉션을 허용 하지 않는 것을 확인 하거나 바인딩을 통해 설정할 DinnerID 또는 HostedBy 속성을 허용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-363">Notice we are not allowing the RSVPs collection to be manipulated via binding, nor are we allowing the DinnerID or HostedBy properties to be set via binding.</span></span> <span data-ttu-id="e4f11-364">보안상의 이유로에서는에서는 대신만 조작 작업 메서드 내에서 명시적 코드를 사용 하 여 이러한 특정 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-364">For security reasons we'll instead only manipulate these particular properties using explicit code within our action methods.</span></span>

### <a name="crud-wrap-up"></a><span data-ttu-id="e4f11-365">CRUD 요약</span><span class="sxs-lookup"><span data-stu-id="e4f11-365">CRUD Wrap-Up</span></span>

<span data-ttu-id="e4f11-366">ASP.NET MVC에는 다양 한 시나리오를 게시 하는 폼 구현에 도움이 되는 기본 제공 기능이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-366">ASP.NET MVC includes a number of built-in features that help with implementing form posting scenarios.</span></span> <span data-ttu-id="e4f11-367">우리의 DinnerRepository 위에 CRUD UI를 지원 하려면 다양 한 이러한 기능을 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-367">We used a variety of these features to provide CRUD UI support on top of our DinnerRepository.</span></span>

<span data-ttu-id="e4f11-368">응용 프로그램을 구현 하는 모델 중심 접근 방법을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-368">We are using a model-focused approach to implement our application.</span></span> <span data-ttu-id="e4f11-369">즉, 모든 유효성 검사 및 비즈니스 규칙 논리는 컨트롤러 또는 뷰를 그리고 우리의 모델 계층 – 내에서 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-369">This means that all our validation and business rule logic is defined within our model layer – and not within our controllers or views.</span></span> <span data-ttu-id="e4f11-370">컨트롤러 클래스도 아니고 우리의 보기 템플릿은 Dinner 모델 클래스에 의해 적용 되는 특정 비즈니스 규칙에 대해 알 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-370">Neither our Controller class nor our View templates know anything about the specific business rules being enforced by our Dinner model class.</span></span>

<span data-ttu-id="e4f11-371">응용 프로그램 아키텍처를 정리 유지 되 고 쉽게 테스트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-371">This will keep our application architecture clean and make it easier to test.</span></span> <span data-ttu-id="e4f11-372">이 모델 계층에 비즈니스 규칙을 추가로 나중에 추가할 수 있습니다 및 *코드를 변경 하지 않아도* 컨트롤러 또는 보기에서 해당 순서 대로 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-372">We can add additional business rules to our model layer in the future and *not have to make any code changes* to our Controller or View in order for them to be supported.</span></span> <span data-ttu-id="e4f11-373">상당한 발전 하 고 나중에 응용 프로그램을 변경 하는 민첩성을 제공 하는 것이입니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-373">This is going to provide us with a great deal of agility to evolve and change our application in the future.</span></span>

<span data-ttu-id="e4f11-374">우리의 DinnersController 이제 Dinner 목록/세부 정보를 사용 하도록 설정 뿐만 아니라 만들기, 편집 및 삭제 지원입니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-374">Our DinnersController now enables Dinner listings/details, as well as create, edit and delete support.</span></span> <span data-ttu-id="e4f11-375">아래 클래스에 대 한 전체 코드를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-375">The complete code for the class can be found below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample35.cs)]

### <a name="next-step"></a><span data-ttu-id="e4f11-376">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e4f11-376">Next Step</span></span>

<span data-ttu-id="e4f11-377">이제 DinnersController 클래스 내에서 구현 하는 기본 CRUD (만들기, 읽기, 업데이트 및 삭제) 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-377">We now have basic CRUD (Create, Read, Update and Delete) support implement within our DinnersController class.</span></span>

<span data-ttu-id="e4f11-378">이제 살펴보겠습니다 사용 하 여 ViewData 및 ViewModel 클래스는 폼에 풍부한 UI를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4f11-378">Let's now look at how we can use ViewData and ViewModel classes to enable even richer UI on our forms.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e4f11-379">[이전](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
> [다음](use-viewdata-and-implement-viewmodel-classes.md)</span><span class="sxs-lookup"><span data-stu-id="e4f11-379">[Previous](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
[Next](use-viewdata-and-implement-viewmodel-classes.md)</span></span>
