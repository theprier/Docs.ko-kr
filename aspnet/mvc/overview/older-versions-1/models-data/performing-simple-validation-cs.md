---
uid: mvc/overview/older-versions-1/models-data/performing-simple-validation-cs
title: 간단한 유효성 검사 (C#)를 수행 합니다. | Microsoft Docs
author: StephenWalther
description: ASP.NET MVC 응용 프로그램에서 유효성 검사를 수행 하는 방법에 알아봅니다. 이 자습서에서는 Stephen Walther 소개 모델 상태 및 유효성 검사 HTML 도우미 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/02/2009
ms.topic: article
ms.assetid: 21383c9d-6aea-4bad-a99b-b5f2c9d6503f
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/models-data/performing-simple-validation-cs
msc.type: authoredcontent
ms.openlocfilehash: 7fc1dcc6935841382215f67a519cd241ac68931a
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="performing-simple-validation-c"></a><span data-ttu-id="45568-104">간단한 유효성 검사 (C#)를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="45568-104">Performing Simple Validation (C#)</span></span>
====================
<span data-ttu-id="45568-105">으로 [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="45568-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="45568-106">ASP.NET MVC 응용 프로그램에서 유효성 검사를 수행 하는 방법에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="45568-106">Learn how to perform validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="45568-107">이 자습서에서는 Stephen Walther 모델 상태 수 및 HTML 유효성 검사 도우미를 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="45568-107">In this tutorial, Stephen Walther introduces you to model state and the validation HTML helpers.</span></span>


<span data-ttu-id="45568-108">이 자습서의 목표는 ASP.NET MVC 응용 프로그램 내에서 유효성 검사를 수행 하는 방법에 대해 설명 하는입니다.</span><span class="sxs-lookup"><span data-stu-id="45568-108">The goal of this tutorial is to explain how you can perform validation within an ASP.NET MVC application.</span></span> <span data-ttu-id="45568-109">예를 들어 필수 필드에 대 한 값을 포함 하지 않는 폼이 전송에서 다른 사용자를 방지 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="45568-109">For example, you learn how to prevent someone from submitting a form that does not contain a value for a required field.</span></span> <span data-ttu-id="45568-110">모델 상태 및 유효성 검사 HTML 도우미를 사용 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="45568-110">You learn how to use model state and the validation HTML helpers.</span></span>

## <a name="understanding-model-state"></a><span data-ttu-id="45568-111">모델 상태 이해</span><span class="sxs-lookup"><span data-stu-id="45568-111">Understanding Model State</span></span>

<span data-ttu-id="45568-112">유효성 검사 오류를 나타내기 위해 모델 상태-또는-모델 상태 사전에서 보다 정확 하 게 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="45568-112">You use model state - or more accurately, the model state dictionary - to represent validation errors.</span></span> <span data-ttu-id="45568-113">예를 들어 create () 동작 목록 1의 데이터베이스에 제품 클래스를 추가 하기 전에 제품 클래스의 속성을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="45568-113">For example, the Create() action in Listing 1 validates the properties of a Product class before adding the Product class to a database.</span></span>


<span data-ttu-id="45568-114">필자가 하지 추천 컨트롤러에 데이터베이스 또는 유효성 검사 논리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="45568-114">I'm not recommending that you add your validation or database logic to a controller.</span></span> <span data-ttu-id="45568-115">컨트롤러 응용 프로그램 흐름 제어와 관련 된 논리만 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45568-115">A controller should contain only logic related to application flow control.</span></span> <span data-ttu-id="45568-116">바로 가기를 간단 하 게 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="45568-116">We are taking a shortcut to keep things simple.</span></span>


<span data-ttu-id="45568-117">**1-Controllers\ProductController.cs 나열**</span><span class="sxs-lookup"><span data-stu-id="45568-117">**Listing 1 - Controllers\ProductController.cs**</span></span>

[!code-csharp[Main](performing-simple-validation-cs/samples/sample1.cs)]

<span data-ttu-id="45568-118">목록 1의 제품 클래스의 이름, 설명 및 UnitsInStock 속성 유효성이 검사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45568-118">In Listing 1, the Name, Description, and UnitsInStock properties of the Product class are validated.</span></span> <span data-ttu-id="45568-119">이러한 속성 중 하나라도 실패 한 유효성 검사 테스트 오류가 (컨트롤러 클래스의 ModelState 속성에 의해 표현 됨) 모델 상태 사전에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45568-119">If any of these properties fail a validation test then an error is added to the model state dictionary (represented by the ModelState property of the Controller class).</span></span>

<span data-ttu-id="45568-120">모델 상태에서 오류가 경우 ModelState.IsValid 속성이 false 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="45568-120">If there are any errors in model state then the ModelState.IsValid property returns false.</span></span> <span data-ttu-id="45568-121">이 경우 새 제품을 만들기 위한 HTML 폼 다시 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45568-121">In that case, the HTML form for creating a new product is redisplayed.</span></span> <span data-ttu-id="45568-122">그렇지 않으면 유효성 검사 오류가 있을 경우 새 제품 데이터베이스에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45568-122">Otherwise, if there are no validation errors, the new Product is added to the database.</span></span>

## <a name="using-the-validation-helpers"></a><span data-ttu-id="45568-123">유효성 검사 도우미를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="45568-123">Using the Validation Helpers</span></span>

<span data-ttu-id="45568-124">ASP.NET MVC 프레임 워크에는 두 명의 유효성 검사 도우미가 포함 되어: Html.ValidationMessage() 도우미와 Html.ValidationSummary() 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="45568-124">The ASP.NET MVC framework includes two validation helpers: the Html.ValidationMessage() helper and the Html.ValidationSummary() helper.</span></span> <span data-ttu-id="45568-125">보기에서 이러한 두 도우미 클래스를 사용 하 여 유효성 검사 오류 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="45568-125">You use these two helpers in a view to display validation error messages.</span></span>

<span data-ttu-id="45568-126">Html.ValidationMessage() 및 Html.ValidationSummary() 도우미 ASP.NET MVC 스 캐 폴딩 하 여 자동으로 생성 되는 뷰 만들기 및 편집에에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45568-126">The Html.ValidationMessage() and Html.ValidationSummary() helpers are used in the Create and Edit views that are generated automatically by the ASP.NET MVC scaffolding.</span></span> <span data-ttu-id="45568-127">만들기 뷰를 생성 하려면 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="45568-127">Follow these steps to generate the Create view:</span></span>

1. <span data-ttu-id="45568-128">제품 컨트롤러에서 create () 작업을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **뷰 추가** (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="45568-128">Right-click the Create() action in the Product controller and select the menu option **Add View** (see Figure 1).</span></span>
2. <span data-ttu-id="45568-129">에 **뷰 추가** 대화 상자에서 확인란 확인 **강력한 형식의 뷰 만들기** (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="45568-129">In the **Add View** dialog, check the checkbox labeled **Create a strongly-typed view** (see Figure 2).</span></span>
3. <span data-ttu-id="45568-130">**데이터 클래스 보기** 드롭다운 목록에서 Product 클래스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="45568-130">From the **View data class** dropdown list, select the Product class.</span></span>
4. <span data-ttu-id="45568-131">**콘텐츠를 볼** 드롭다운 목록에서 만들기를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="45568-131">From the **View content** dropdown list, select Create.</span></span>
5. <span data-ttu-id="45568-132">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="45568-132">Click the **Add** button.</span></span>


<span data-ttu-id="45568-133">뷰를 추가 하기 전에 응용 프로그램을 작성 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="45568-133">Make sure that you build your application before adding a view.</span></span> <span data-ttu-id="45568-134">클래스의 목록에 나타나지 않습니다는 그렇지 않은 경우는 **데이터 클래스 보기** 드롭다운 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="45568-134">Otherwise, the list of classes won't appear in the **View data class** dropdown list.</span></span>


<span data-ttu-id="45568-135">[![새 프로젝트 대화 상자](performing-simple-validation-cs/_static/image1.jpg)](performing-simple-validation-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="45568-135">[![The New Project dialog box](performing-simple-validation-cs/_static/image1.jpg)](performing-simple-validation-cs/_static/image1.png)</span></span>

<span data-ttu-id="45568-136">**그림 01**: 뷰 추가 ([전체 크기 이미지를 보려면 클릭](performing-simple-validation-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="45568-136">**Figure 01**: Adding a view([Click to view full-size image](performing-simple-validation-cs/_static/image2.png))</span></span>


<span data-ttu-id="45568-137">[![새 프로젝트 대화 상자](performing-simple-validation-cs/_static/image2.jpg)](performing-simple-validation-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="45568-137">[![The New Project dialog box](performing-simple-validation-cs/_static/image2.jpg)](performing-simple-validation-cs/_static/image3.png)</span></span>

<span data-ttu-id="45568-138">**그림 02**: 강력한 형식의 뷰 만들기 ([전체 크기 이미지를 보려면 클릭](performing-simple-validation-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="45568-138">**Figure 02**: Creating a strongly-typed view ([Click to view full-size image](performing-simple-validation-cs/_static/image4.png))</span></span>


<span data-ttu-id="45568-139">다음이 단계를 완료 한 후에 목록 2의 만들기 뷰를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="45568-139">After you complete these steps, you get the Create view in Listing 2.</span></span>

<span data-ttu-id="45568-140">**Listing 2 - Views\Product\Create.aspx**</span><span class="sxs-lookup"><span data-stu-id="45568-140">**Listing 2 - Views\Product\Create.aspx**</span></span>

[!code-aspx[Main](performing-simple-validation-cs/samples/sample2.aspx)]

<span data-ttu-id="45568-141">목록 2 Html.ValidationSummary() 도우미 HTML 폼 위에 바로 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45568-141">In Listing 2, the Html.ValidationSummary() helper is called immediately above the HTML form.</span></span> <span data-ttu-id="45568-142">이 도우미는 유효성 검사 오류 메시지 목록을 표시 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45568-142">This helper is used to display a list of validation error messages.</span></span> <span data-ttu-id="45568-143">Html.ValidationSummary() 도우미 글머리 기호 목록에서 오류를 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="45568-143">The Html.ValidationSummary() helper renders the errors in a bulleted list.</span></span>

<span data-ttu-id="45568-144">각 HTML 폼 필드 옆에 있는 Html.ValidationMessage() 도우미 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="45568-144">The Html.ValidationMessage() helper is called next to each of the HTML form fields.</span></span> <span data-ttu-id="45568-145">이 도우미는 양식 필드 오른쪽에 오류 메시지를 표시 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45568-145">This helper is used to display an error message right next to a form field.</span></span> <span data-ttu-id="45568-146">목록 2의 경우는 오류가 있을 때 Html.ValidationMessage() 도우미는 별표를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="45568-146">In the case of Listing 2, the Html.ValidationMessage() helper displays an asterisk when there is an error.</span></span>

<span data-ttu-id="45568-147">그림 3에 있는 페이지는 누락 된 필드와 잘못 된 값이 폼이 전송 될 때 유효성 검사 도우미에서 렌더링 오류 메시지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="45568-147">The page in Figure 3 illustrates the error messages rendered by the validation helpers when the form is submitted with missing fields and invalid values.</span></span>


<span data-ttu-id="45568-148">[![새 프로젝트 대화 상자](performing-simple-validation-cs/_static/image3.jpg)](performing-simple-validation-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="45568-148">[![The New Project dialog box](performing-simple-validation-cs/_static/image3.jpg)](performing-simple-validation-cs/_static/image5.png)</span></span>

<span data-ttu-id="45568-149">**그림 03**: 제출 된 문제는 Create view ([전체 크기 이미지를 보려면 클릭](performing-simple-validation-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="45568-149">**Figure 03**: The Create view submitted with problems ([Click to view full-size image](performing-simple-validation-cs/_static/image6.png))</span></span>


<span data-ttu-id="45568-150">HTML의 모양을 필드는 유효성 검사 오류가 있을 때에 수정 됩니다 입력 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="45568-150">Notice that the appearance of the HTML input fields are also modified when there is a validation error.</span></span> <span data-ttu-id="45568-151">Html.TextBox() 도우미 렌더링 되는 *클래스 "입력 유효성 검사 오류" =* 특성 유효성 검사 오류가 있을 때 속성에 연결 된 Html.TextBox() 도우미에서 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="45568-151">The Html.TextBox() helper renders a *class="input-validation-error"* attribute when there is a validation error associated with the property rendered by the Html.TextBox() helper.</span></span>

<span data-ttu-id="45568-152">다음 세 가지가 연계 스타일 시트의 유효성 검사 오류 표시 모양을 제어 하는 데 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="45568-152">There are three cascading style sheet classes used to control the appearance of validation errors:</span></span>

- <span data-ttu-id="45568-153">입력-유효성 검사 오류-에 적용 된 &lt;입력&gt; Html.TextBox() 도우미에서 렌더링 되는 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="45568-153">input-validation-error - Applied to the &lt;input&gt; tag rendered by Html.TextBox() helper.</span></span>
- <span data-ttu-id="45568-154">에 적용 된 필드-유효성 검사 오류-는 &lt;걸쳐&gt; Html.ValidationMessage() 도우미에서 렌더링 되는 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="45568-154">field-validation-error - Applied to the &lt;span&gt; tag rendered by the Html.ValidationMessage() helper.</span></span>
- <span data-ttu-id="45568-155">유효성 검사-요약 오류-적용할는 &lt;ul&gt; Html.ValidationSumamry() 도우미에서 렌더링 되는 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="45568-155">validation-summary-errors - Applied to the &lt;ul&gt; tag rendered by the Html.ValidationSumamry() helper.</span></span>

<span data-ttu-id="45568-156">이러한 연계 스타일 시트 클래스를 수정 하 고 따라서 콘텐츠 폴더에 있는 Site.css 파일을 수정 하 여 유효성 검사 오류의 모양을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45568-156">You can modify these cascading style sheet classes, and therefore modify the appearance of the validation errors, by modifying the Site.css file located in the Content folder.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="45568-157">HtmlHelper 클래스 CSS 관련 유효성 검사의 이름 검색에 대 한 읽기 전용 정적 속성에 포함 되어 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="45568-157">The HtmlHelper class includes read-only static properties for retrieving the names of the validation related CSS classes.</span></span> <span data-ttu-id="45568-158">이러한 정적 속성에는 ValidationInputCssClassName, ValidationFieldCssClassName, 및 ValidationSummaryCssClassName 이름이 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45568-158">These static properties are named ValidationInputCssClassName, ValidationFieldCssClassName, and ValidationSummaryCssClassName.</span></span>


## <a name="prebinding-validation-and-postbinding-validation"></a><span data-ttu-id="45568-159">유효성 검사 및 Postbinding prebinding</span><span class="sxs-lookup"><span data-stu-id="45568-159">Prebinding Validation and Postbinding Validation</span></span>

<span data-ttu-id="45568-160">제품을 만들기 위한 HTML 폼을 제출 하는 경우 price 필드 및 UnitsInStock 필드에 대 한 값에 대 한 잘못 된 값을 입력 하면 그림 4에 표시 되는 유효성 검사 메시지를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45568-160">If you submit the HTML form for creating a Product, and you enter an invalid value for the price field and no value for the UnitsInStock field, then you'll get the validation messages displayed in Figure 4.</span></span> <span data-ttu-id="45568-161">이러한 유효성 검사 오류 메시지에서 제공 않은 위치</span><span class="sxs-lookup"><span data-stu-id="45568-161">Where do these validation error messages come from?</span></span>


<span data-ttu-id="45568-162">[![새 프로젝트 대화 상자](performing-simple-validation-cs/_static/image4.jpg)](performing-simple-validation-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="45568-162">[![The New Project dialog box](performing-simple-validation-cs/_static/image4.jpg)](performing-simple-validation-cs/_static/image7.png)</span></span>

<span data-ttu-id="45568-163">**그림 04**: Prebinding 유효성 검사 오류 ([전체 크기 이미지를 보려면 클릭](performing-simple-validation-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="45568-163">**Figure 04**: Prebinding Validation Errors([Click to view full-size image](performing-simple-validation-cs/_static/image8.png))</span></span>


<span data-ttu-id="45568-164">실제로 두 가지 유형의 HTML 양식 필드는 클래스에 바인딩되고 양식 필드는 클래스에 바인딩된 후에 생성 된 전에 생성 된 유효성 검사 오류 메시지-있습니다.</span><span class="sxs-lookup"><span data-stu-id="45568-164">There are actually two types of validation error messages - those generated before the HTML form fields are bound to a class and those generated after the form fields are bound to the class.</span></span> <span data-ttu-id="45568-165">즉,는 prebinding 유효성 검사 오류 및 유효성 검사 오류 postbinding 합니다.</span><span class="sxs-lookup"><span data-stu-id="45568-165">In other words, there are prebinding validation errors and postbinding validation errors.</span></span>

<span data-ttu-id="45568-166">목록 1의 제품 컨트롤러에 의해 노출 되는 create () 동작 제품 클래스의 인스턴스를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="45568-166">The Create() action exposed by the Product controller in Listing 1 accepts an instance of the Product class.</span></span> <span data-ttu-id="45568-167">Create 메서드 시그니처는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="45568-167">The signature of the Create method looks like this:</span></span>

[!code-csharp[Main](performing-simple-validation-cs/samples/sample3.cs)]

<span data-ttu-id="45568-168">모델 바인더를 호출 하는 방식으로 폼 만들기에서에서 HTML 폼 필드의 값 productToCreate 클래스에 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="45568-168">The values of the HTML form fields from the Create form are bound to the productToCreate class by something called a model binder.</span></span> <span data-ttu-id="45568-169">기본 모델 바인더 오류 메시지가 모델 상태를 자동으로 때 추가 된 양식 필드 형식 속성에 바인딩할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="45568-169">The default model binder adds an error message to model state automatically when it cannot bind a form field to a form property.</span></span>

<span data-ttu-id="45568-170">기본 모델 바인더에서는 문자열 "apple"를 제품 클래스의 가격 속성에 바인딩할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="45568-170">The default model binder cannot bind the string "apple" to the Price property of the Product class.</span></span> <span data-ttu-id="45568-171">10 진수 속성에 문자열을 할당할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="45568-171">You can't assign a string to a decimal property.</span></span> <span data-ttu-id="45568-172">따라서, 모델 바인더 모델 상태에 오류를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="45568-172">Therefore, the model binder adds an error to model state.</span></span>

<span data-ttu-id="45568-173">또한 기본 모델 바인더 null을 허용 하지 않는 속성에 null 값을 할당할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="45568-173">The default model binder also cannot assign a null value to a property that does not accept nulls.</span></span> <span data-ttu-id="45568-174">특히, 모델 바인더 UnitsInStock 속성에 null 값을 할당할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="45568-174">In particular, the model binder cannot assign a null value to the UnitsInStock property.</span></span> <span data-ttu-id="45568-175">다시 한 번, 모델 바인더를 포기 하 고 모델 상태 오류 메시지가 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45568-175">Once again, the model binder gives up and adds an error message to model state.</span></span>

<span data-ttu-id="45568-176">Prebinding 오류 메시지를 이러한 모양을 사용자 지정 하려는 경우 이러한 메시지에 대 한 리소스 문자열을 만들 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45568-176">If you want to customize the appearance of these prebinding error messages then you need to create resource strings for these messages.</span></span>

## <a name="summary"></a><span data-ttu-id="45568-177">요약</span><span class="sxs-lookup"><span data-stu-id="45568-177">Summary</span></span>

<span data-ttu-id="45568-178">이 자습서의 목표는 ASP.NET MVC 프레임 워크에서 유효성 검사의 기본 메커니즘에 설명 하는 것 이었습니다.</span><span class="sxs-lookup"><span data-stu-id="45568-178">The goal of this tutorial was to describe the basic mechanics of validation in the ASP.NET MVC framework.</span></span> <span data-ttu-id="45568-179">모델 상태 및 유효성 검사 HTML 도우미를 사용 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="45568-179">You learned how to use model state and the validation HTML helpers.</span></span> <span data-ttu-id="45568-180">유효성 검사 postbinding prebinding 간 구분을 논의 합니다.</span><span class="sxs-lookup"><span data-stu-id="45568-180">We also discussed the distinction between prebinding and postbinding validation.</span></span> <span data-ttu-id="45568-181">다른 자습서에 모델 클래스를 컨트롤러에 유효성 검사 코드를 이동 하기 위한 다양 한 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="45568-181">In other tutorials, we'll discuss various strategies for moving your validation code out of your controllers and into your model classes.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="45568-182">[이전](displaying-a-table-of-database-data-cs.md)
> [다음](validating-with-the-idataerrorinfo-interface-cs.md)</span><span class="sxs-lookup"><span data-stu-id="45568-182">[Previous](displaying-a-table-of-database-data-cs.md)
[Next](validating-with-the-idataerrorinfo-interface-cs.md)</span></span>
