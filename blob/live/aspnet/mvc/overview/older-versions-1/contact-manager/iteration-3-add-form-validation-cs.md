---
uid: mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-cs
title: "반복 #3-추가 폼 유효성 검사 (C#) | Microsoft Docs"
author: microsoft
description: "세 번째 반복에서 기본적인 형태의 유효성 검사를 추가 했습니다. म 중이거나 사용자에서 필수 양식 필드를 완료 하지 않고 폼을 제출 합니다. 또한 emai을 확인 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2009
ms.topic: article
ms.assetid: 51a0d175-913b-43d8-95e3-840fb96ad1a9
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-cs
msc.type: authoredcontent
ms.openlocfilehash: 06c7fc31e138e9009640d20202e4745a61b68eeb
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="iteration-3--add-form-validation-c"></a><span data-ttu-id="8bb39-105">반복 #3-추가 폼 유효성 검사 (C#)</span><span class="sxs-lookup"><span data-stu-id="8bb39-105">Iteration #3 – Add form validation (C#)</span></span>
====================
<span data-ttu-id="8bb39-106">여 [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="8bb39-106">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="8bb39-107">코드 다운로드</span><span class="sxs-lookup"><span data-stu-id="8bb39-107">Download Code</span></span>](iteration-3-add-form-validation-cs/_static/contactmanager_3_cs1.zip)

> <span data-ttu-id="8bb39-108">세 번째 반복에서 기본적인 형태의 유효성 검사를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-108">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="8bb39-109">म 중이거나 사용자에서 필수 양식 필드를 완료 하지 않고 폼을 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-109">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="8bb39-110">또한 전자 메일 주소, 전화 번호를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-110">We also validate email addresses and phone numbers.</span></span>


## <a name="building-a-contact-management-aspnet-mvc-application-c"></a><span data-ttu-id="8bb39-111">ASP.NET MVC 연락처 관리 응용 프로그램 (C#) 빌드</span><span class="sxs-lookup"><span data-stu-id="8bb39-111">Building a Contact Management ASP.NET MVC Application (C#)</span></span>
  

<span data-ttu-id="8bb39-112">이 일련의 자습서에서는 전체 연락처 관리 응용을 프로그램의 시작 끝나기를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-112">In this series of tutorials, we build an entire Contact Management application from start to finish.</span></span> <span data-ttu-id="8bb39-113">관리자에 게 문의 응용 프로그램을 사람 목록에 대 한 사용-이름, 전화 번호 및 전자 메일 주소-연락처 정보를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-113">The Contact Manager application enables you to store contact information - names, phone numbers and email addresses - for a list of people.</span></span>

<span data-ttu-id="8bb39-114">여러 반복을 통해에 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-114">We build the application over multiple iterations.</span></span> <span data-ttu-id="8bb39-115">각 반복에서 점진적으로 응용 프로그램을 개선 했습니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-115">With each iteration, we gradually improve the application.</span></span> <span data-ttu-id="8bb39-116">이 여러 개의 반복 접근 방법의 목적은 각 변경의 이유를 이해 하는 데 사용할 수 있도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-116">The goal of this multiple iteration approach is to enable you to understand the reason for each change.</span></span>

- <span data-ttu-id="8bb39-117">반복 #1-응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-117">Iteration #1 - Create the application.</span></span> <span data-ttu-id="8bb39-118">첫 번째 반복에서는 만듭니다 연락처 관리자에는 가장 간단한 방법은 가능한.</span><span class="sxs-lookup"><span data-stu-id="8bb39-118">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="8bb39-119">기본적인 데이터베이스 작업에 대 한 지원을 추가 하 여: 만들기, 읽기, 업데이트 및 삭제 (CRUD).</span><span class="sxs-lookup"><span data-stu-id="8bb39-119">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>

- <span data-ttu-id="8bb39-120">반복 #2-모양이 아닌 응용 프로그램을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-120">Iteration #2 - Make the application look nice.</span></span> <span data-ttu-id="8bb39-121">이 반복에서 기본 ASP.NET MVC 뷰 마스터 페이지를 수정 및 스타일 시트를 연계 하 여 응용 프로그램의 모양을 개선 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-121">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>

- <span data-ttu-id="8bb39-122">반복 #3-폼 유효성 검사를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-122">Iteration #3 - Add form validation.</span></span> <span data-ttu-id="8bb39-123">세 번째 반복에서 기본적인 형태의 유효성 검사를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-123">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="8bb39-124">म 중이거나 사용자에서 필수 양식 필드를 완료 하지 않고 폼을 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-124">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="8bb39-125">또한 전자 메일 주소, 전화 번호를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-125">We also validate email addresses and phone numbers.</span></span>

- <span data-ttu-id="8bb39-126">반복 #4-느슨하게 결합 된 응용 프로그램을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-126">Iteration #4 - Make the application loosely coupled.</span></span> <span data-ttu-id="8bb39-127">이 세 번째 반복에서 우리 활용 여러 가지 소프트웨어 디자인 패턴을 쉽게 유지 관리 하 고 않아 응용 프로그램을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-127">In this third iteration, we take advantage of several software design patterns to make it easier to maintain and modify the Contact Manager application.</span></span> <span data-ttu-id="8bb39-128">예를 들어 리팩터링한 리포지토리 패턴 및 종속성 주입 패턴을 사용 하도록 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-128">For example, we refactor our application to use the Repository pattern and the Dependency Injection pattern.</span></span>

- <span data-ttu-id="8bb39-129">반복 #5-단위 테스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-129">Iteration #5 - Create unit tests.</span></span> <span data-ttu-id="8bb39-130">다섯 번째 반복에서 하도록 응용 프로그램이 쉽게 유지 관리 및 단위 테스트를 추가 하 여 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-130">In the fifth iteration, we make our application easier to maintain and modify by adding unit tests.</span></span> <span data-ttu-id="8bb39-131">데이터 모델 클래스를 모의 하 고 우리의 컨트롤러 및 유효성 검사 논리에 대 한 단위 테스트를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-131">We mock our data model classes and build unit tests for our controllers and validation logic.</span></span>

- <span data-ttu-id="8bb39-132">반복 6-테스트 기반 개발을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-132">Iteration #6 - Use test-driven development.</span></span> <span data-ttu-id="8bb39-133">이 6 번째 반복에서에서는 새 기능을 추가할 응용 프로그램 먼저 단위 테스트를 작성 하 고 단위 테스트에 대해 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-133">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="8bb39-134">이 반복 메일 그룹을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-134">In this iteration, we add contact groups.</span></span>

- <span data-ttu-id="8bb39-135">반복 #7-Ajax 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-135">Iteration #7 - Add Ajax functionality.</span></span> <span data-ttu-id="8bb39-136">일곱 번째 반복에서 개선할 응용 프로그램의 성능과 응답성 ajax 지원을 추가 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-136">In the seventh iteration, we improve the responsiveness and performance of our application by adding support for Ajax.</span></span>


## <a name="this-iteration"></a><span data-ttu-id="8bb39-137">이 반복</span><span class="sxs-lookup"><span data-stu-id="8bb39-137">This Iteration</span></span>

<span data-ttu-id="8bb39-138">않아 응용 프로그램의이 두 번째 반복에서 기본적인 형태의 유효성 검사를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-138">In this second iteration of the Contact Manager application, we add basic form validation.</span></span> <span data-ttu-id="8bb39-139">म 중이거나 사용자에서 필수 양식 필드에 값을 입력 하지 않고 연락처를 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-139">We prevent people from submitting a contact without entering values for required form fields.</span></span> <span data-ttu-id="8bb39-140">또한 전화 번호 및 전자 메일 주소 (그림 1 참조)을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-140">We also validate phone numbers and email addresses (see Figure 1).</span></span>


<span data-ttu-id="8bb39-141">[![새 프로젝트 대화 상자](iteration-3-add-form-validation-cs/_static/image1.jpg)](iteration-3-add-form-validation-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8bb39-141">[![The New Project dialog box](iteration-3-add-form-validation-cs/_static/image1.jpg)](iteration-3-add-form-validation-cs/_static/image1.png)</span></span>

<span data-ttu-id="8bb39-142">**그림 01**: 유효성 검사를 사용 하 여 폼 ([전체 크기 이미지를 보려면 클릭](iteration-3-add-form-validation-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="8bb39-142">**Figure 01**: A form with validation ([Click to view full-size image](iteration-3-add-form-validation-cs/_static/image2.png))</span></span>


<span data-ttu-id="8bb39-143">이 반복에서 컨트롤러 작업에 직접 유효성 검사 논리를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-143">In this iteration, we add the validation logic directly to the controller actions.</span></span> <span data-ttu-id="8bb39-144">일반적으로 ASP.NET MVC 응용 프로그램에 유효성 검사를 추가할 권장 방법은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-144">In general, this is not the recommended way to add validation to an ASP.NET MVC application.</span></span> <span data-ttu-id="8bb39-145">별도의 응용 프로그램 s 유효성 검사 논리를 배치 하는 것이 좋습니다 [서비스 계층](http://martinfowler.com/eaaCatalog/serviceLayer.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-145">A better approach is to place an application s validation logic in a separate [service layer](http://martinfowler.com/eaaCatalog/serviceLayer.html).</span></span> <span data-ttu-id="8bb39-146">응용 프로그램을 더 쉽게 유지 관리할 않아 응용 프로그램을 리팩터링한 다음 반복에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-146">In the next iteration, we refactor the Contact Manager application to make the application more maintainable.</span></span>

<span data-ttu-id="8bb39-147">이 반복에 간단 하 게,에서는 모든 유효성 검사 코드를 직접 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-147">In this iteration, to keep things simple, we write all of the validation code by hand.</span></span> <span data-ttu-id="8bb39-148">유효성 검사 코드를 직접 작성 하는 대신 유효성 검사 프레임 워크를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-148">Instead of writing the validation code ourselves, we could take advantage of a validation framework.</span></span> <span data-ttu-id="8bb39-149">예를 들어 ASP.NET MVC 응용 프로그램에 대 한 유효성 검사 논리를 구현 하는 Microsoft Enterprise 라이브러리 유효성 검사 응용 프로그램 블록 (VAB)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-149">For example, you can use the Microsoft Enterprise Library Validation Application Block (VAB) to implement the validation logic for your ASP.NET MVC application.</span></span> <span data-ttu-id="8bb39-150">유효성 검사 응용 프로그램 블록에 대 한 자세한 내용은 다음을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="8bb39-150">To learn more about the Validation Application Block, see:</span></span>

[<span data-ttu-id="8bb39-151">*http://msdn.microsoft.com/en-us/library/dd203099.aspx*</span><span class="sxs-lookup"><span data-stu-id="8bb39-151">*http://msdn.microsoft.com/en-us/library/dd203099.aspx*</span></span>](https://msdn.microsoft.com/en-us/library/dd203099.aspx)

## <a name="adding-validation-to-the-create-view"></a><span data-ttu-id="8bb39-152">만들기 뷰에 유효성 검사 추가</span><span class="sxs-lookup"><span data-stu-id="8bb39-152">Adding Validation to the Create View</span></span>

<span data-ttu-id="8bb39-153">만들기 뷰를 유효성 검사 논리를 추가 하 여 시작 s를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-153">Let s start by adding validation logic to the Create view.</span></span> <span data-ttu-id="8bb39-154">다행히 Visual Studio와 함께 만들기 뷰를 생성 했습니다 때문에 Create view 이미 포함 되어 모든 유효성 검사 메시지를 표시 하는 데 필요한 사용자 인터페이스 논리입니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-154">Fortunately, because we generated the Create view with Visual Studio, the Create view already contains all of the necessary user interface logic to display validation messages.</span></span> <span data-ttu-id="8bb39-155">만들기 뷰 목록 1에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-155">The Create view is contained in Listing 1.</span></span>

<span data-ttu-id="8bb39-156">**목록 1-\Views\Contact\Create.aspx**</span><span class="sxs-lookup"><span data-stu-id="8bb39-156">**Listing 1 - \Views\Contact\Create.aspx**</span></span>

[!code-aspx[Main](iteration-3-add-form-validation-cs/samples/sample1.aspx)]

<span data-ttu-id="8bb39-157">HTML 폼 바로 위에 있는 Html.ValidationSummary() 도우미 메서드에 대 한 호출을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-157">Notice the call to the Html.ValidationSummary() helper method that appears immediately above the HTML form.</span></span> <span data-ttu-id="8bb39-158">유효성 검사 오류 메시지에 있는이 메서드는 글머리 기호 목록에서 유효성 검사 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-158">If there are validation error messages, then this method displays validation messages in a bulleted list.</span></span>

<span data-ttu-id="8bb39-159">공지, 또한 각 양식 필드 옆에 나타나는 Html.ValidationMessage()에 대 한 호출입니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-159">Notice, furthermore, the calls to Html.ValidationMessage() that appear next to each form field.</span></span> <span data-ttu-id="8bb39-160">ValidationMessage() 도우미 각 유효성 검사 오류 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-160">The ValidationMessage() helper displays an individual validation error message.</span></span> <span data-ttu-id="8bb39-161">목록 1의 경우 별표 유효성 검사 오류가 있을 때 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-161">In the case of Listing 1, an asterisk is displayed when there is a validation error.</span></span>

<span data-ttu-id="8bb39-162">마지막으로, Html.TextBox() 도우미 자동으로 렌더링 연계 스타일 시트 클래스 도우미에서 표시 되는 속성와 관련 된 유효성 검사 오류가 있을 때.</span><span class="sxs-lookup"><span data-stu-id="8bb39-162">Finally, the Html.TextBox() helper automatically renders a Cascading Style Sheet class when there is a validation error associated with the property displayed by the helper.</span></span> <span data-ttu-id="8bb39-163">라는 클래스를 렌더링 하는 Html.TextBox() 도우미 **입력 유효성 검사 오류**합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-163">The Html.TextBox() helper renders a class named **input-validation-error**.</span></span>

<span data-ttu-id="8bb39-164">새 ASP.NET MVC 응용 프로그램을 만들 때 Site.css 명명 된 스타일 시트의 내용 폴더에서 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-164">When you create a new ASP.NET MVC application, a style sheet named Site.css is created in the Content folder automatically.</span></span> <span data-ttu-id="8bb39-165">이 스타일 시트는 CSS 클래스 유효성 검사 오류 메시지의 모양에 대 한 다음 정의 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-165">This style sheet contains the following definitions for CSS classes related to the appearance of validation error messages:</span></span>

[!code-css[Main](iteration-3-add-form-validation-cs/samples/sample2.css)]

<span data-ttu-id="8bb39-166">필드 유효성 검사 오류 클래스 Html.ValidationMessage() 도우미에서 렌더링 된 출력 스타일에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-166">The field-validation-error class is used to style the output rendered by the Html.ValidationMessage() helper.</span></span> <span data-ttu-id="8bb39-167">Html.TextBox() 도우미에서 렌더링 되는 텍스트 (입력) 스타일을 지정 하는 입력 유효성 검사 오류 클래스 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-167">The input-validation-error class is used to style the textbox (input) rendered by the Html.TextBox() helper.</span></span> <span data-ttu-id="8bb39-168">유효성 검사 요약-오류 클래스 스타일을 렌더링 Html.ValidationSummary() 도우미에서 순서가 지정 되지 않은 목록 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-168">The validation-summary-errors class is used to style the unordered list rendered by the Html.ValidationSummary() helper.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="8bb39-169">유효성 검사 오류 메시지의 모양을 사용자 지정 하려면이 섹션에 설명 된 스타일 시트 클래스를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-169">You can modify the style sheet classes described in this section to customize the appearance of validation error messages.</span></span>


## <a name="adding-validation-logic-to-the-create-action"></a><span data-ttu-id="8bb39-170">유효성 검사 논리를 추가 된 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="8bb39-170">Adding Validation Logic to the Create Action</span></span>

<span data-ttu-id="8bb39-171">지금 바로 사용, Create view 유효성 검사 오류 메시지를 모든 메시지를 생성 하는 논리 기록 되지 않은 것 이므로 되지 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-171">Right now, the Create view never displays validation error messages because we have not written the logic to generate any messages.</span></span> <span data-ttu-id="8bb39-172">유효성 검사 오류 메시지를 표시 하려면 ModelState에 오류 메시지를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-172">In order to display validation error messages, you need to add the error messages to ModelState.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="8bb39-173">UpdateModel() 메서드 추가 오류 메시지 ModelState 자동으로 때 속성 양식 필드의 값을 할당 하는 동안 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-173">The UpdateModel() method adds error messages to ModelState automatically when there is an error assigning the value of a form field to a property.</span></span> <span data-ttu-id="8bb39-174">예를 들어 날짜/시간 값을 받아 들이는 BirthDate 속성에 "apple" 문자열을 할당 하려고 하면 다음 UpdateModel() 메서드 오류를 추가 ModelState 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-174">For example, if you attempt to assign the string "apple" to a BirthDate property that accepts DateTime values, then the UpdateModel() method adds an error to ModelState.</span></span>


<span data-ttu-id="8bb39-175">목록 2에서 수정 된 create () 메서드는 데이터베이스에 새 연락처를 삽입 하기 전에 연락처 클래스의 속성의 유효성을 검사 하는 새 섹션을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-175">The modified Create() method in Listing 2 contains a new section that validates the properties of the Contact class before the new contact is inserted into the database.</span></span>

<span data-ttu-id="8bb39-176">**2-Controllers\ContactController.cs (유효성 검사와 함께 만들기)를 나열합니다.**</span><span class="sxs-lookup"><span data-stu-id="8bb39-176">**Listing 2 - Controllers\ContactController.cs (Create with validation)**</span></span>

[!code-csharp[Main](iteration-3-add-form-validation-cs/samples/sample3.cs)]

<span data-ttu-id="8bb39-177">유효성 검사 섹션에는 4 개의 고유한 유효성 검사 규칙이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-177">The validate section enforces four distinct validation rules:</span></span>

- <span data-ttu-id="8bb39-178">FirstName 속성의 길이 0 보다 커야 있어야 합니다. (및 공백으로 이루어질 수 없습니다 것)</span><span class="sxs-lookup"><span data-stu-id="8bb39-178">The FirstName property must have a length greater than zero (and it cannot consist solely of spaces)</span></span>
- <span data-ttu-id="8bb39-179">LastName 속성이 0 보다 큰 길이 여야 합니다. (및 공백으로 이루어질 수 없습니다 것)</span><span class="sxs-lookup"><span data-stu-id="8bb39-179">The LastName property must have a length greater than zero (and it cannot consist solely of spaces)</span></span>
- <span data-ttu-id="8bb39-180">Phone 속성 값이 있으면 (길이가 0 보다 큰) Phone 속성에 정규식과 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-180">If the Phone property has a value (has a length greater than 0) then the Phone property must match a regular expression.</span></span>
- <span data-ttu-id="8bb39-181">전자 메일 속성 값이 있으면 (길이가 0 보다 큰)의 전자 메일 속성에 정규식과 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-181">If the Email property has a value (has a length greater than 0) then the Email property must match a regular expression.</span></span>

<span data-ttu-id="8bb39-182">유효성 검사 규칙 위반 되는 경우 오류 메시지가 AddModelError() 메서드를 사용 하 여 ModelState에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-182">When there is a validation rule violation, an error message is added to ModelState with the help of the AddModelError() method.</span></span> <span data-ttu-id="8bb39-183">ModelState에 메시지를 추가 하는 경우 속성의 이름 및 유효성 검사 오류 메시지 텍스트 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-183">When you add a message to ModelState, you provide the name of a property and the text of a validation error message.</span></span> <span data-ttu-id="8bb39-184">이 오류 메시지가 Html.ValidationSummary() 및 Html.ValidationMessage() 도우미 메서드에서 보기에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-184">This error message is displayed in the view by the Html.ValidationSummary() and Html.ValidationMessage() helper methods.</span></span>

<span data-ttu-id="8bb39-185">유효성 검사 규칙을 실행 한 후의 ModelState IsValid 속성이 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-185">After the validation rules are executed, the IsValid property of ModelState is checked.</span></span> <span data-ttu-id="8bb39-186">IsValid 속성 유효성 검사 오류 메시지 ModelState에 추가 되 면 false를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-186">The IsValid property returns false when any validation error messages have been added to ModelState.</span></span> <span data-ttu-id="8bb39-187">유효성 검사에 실패할 경우 오류 메시지와 함께 폼 만들기 다시 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-187">If validation fails, the Create form is redisplayed with the error messages.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="8bb39-188">정규식 리포지토리에서 전화 번호 및 전자 메일 주소 유효성을 검사 하는 것에 대 한 정규식 수신 됨 [ *http://regexlib.com*](http://regexlib.com)</span><span class="sxs-lookup"><span data-stu-id="8bb39-188">I got the regular expressions for validating the phone number and email address from the regular expression repository at [*http://regexlib.com*](http://regexlib.com)</span></span>


## <a name="adding-validation-logic-to-the-edit-action"></a><span data-ttu-id="8bb39-189">편집 작업에 유효성 검사 논리를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-189">Adding Validation Logic to the Edit Action</span></span>

<span data-ttu-id="8bb39-190">연락처를 업데이트 하는 Edit() 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-190">The Edit() action updates a Contact.</span></span> <span data-ttu-id="8bb39-191">Edit() 동작 create () 작업으로 동일한 유효성 검사 정확 하 게 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-191">The Edit() action needs to perform exactly the same validation as the Create() action.</span></span> <span data-ttu-id="8bb39-192">동일한 유효성 검사 코드를 복제 하는 대신 동일한 유효성 검사 메서드를 호출 하는 create ()와 Edit() 동작을 연락처 컨트롤러를 리팩터링 해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-192">Instead of duplicating the same validation code, we should refactor the Contact controller so that both the Create() and Edit() actions call the same validation method.</span></span>

<span data-ttu-id="8bb39-193">수정 된 연락처 컨트롤러 클래스 보기 3에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-193">The modified Contact controller class is contained in Listing 3.</span></span> <span data-ttu-id="8bb39-194">이 클래스는 create ()와 Edit() 작업 내에서 호출 하는 새 ValidateContact() 메서드.</span><span class="sxs-lookup"><span data-stu-id="8bb39-194">This class has a new ValidateContact() method that is called within both the Create() and Edit() actions.</span></span>

<span data-ttu-id="8bb39-195">**3-Controllers\ContactController.cs 나열**</span><span class="sxs-lookup"><span data-stu-id="8bb39-195">**Listing 3 - Controllers\ContactController.cs**</span></span>

[!code-csharp[Main](iteration-3-add-form-validation-cs/samples/sample4.cs)]

## <a name="summary"></a><span data-ttu-id="8bb39-196">요약</span><span class="sxs-lookup"><span data-stu-id="8bb39-196">Summary</span></span>

<span data-ttu-id="8bb39-197">이 반복에서 기본적인 형태의 유효성 검사 않아 응용 프로그램을 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-197">In this iteration, we added basic form validation to our Contact Manager application.</span></span> <span data-ttu-id="8bb39-198">유효성 검사 논리에는 사용자가 새 연락처를 전송 하거나 FirstName 및 LastName 속성의 값을 제공 하지 않고 기존 연락처를 편집할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-198">Our validation logic prevents users from submitting a new contact or editing an existing contact without supplying values for the FirstName and LastName properties.</span></span> <span data-ttu-id="8bb39-199">또한 사용자가 올바른 전화 번호 및 전자 메일 주소를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-199">Furthermore, users must supply valid phone numbers and email addresses.</span></span>

<span data-ttu-id="8bb39-200">이 반복에는 가장 쉬운 방법은 가능한에서 않아 응용 프로그램에 유효성 검사 논리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-200">In this iteration, we added the validation logic to our Contact Manager application in the easiest way possible.</span></span> <span data-ttu-id="8bb39-201">그러나 트 컨트롤러 논리에 유효성 검사 논리를 혼합 문제가 생기게 됩니다 우리 장기적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-201">However, mixing our validation logic into our controller logic will create problems for us in the long term.</span></span> <span data-ttu-id="8bb39-202">응용 프로그램 유지 관리 하 고 시간이 지남에 따라 수정 하기가 더 어려워집니다 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-202">Our application will be more difficult to maintain and modify over time.</span></span>

<span data-ttu-id="8bb39-203">다음 반복에 됩니다 리팩터링한 우리의 유효성 검사 논리 및 데이터베이스 액세스 논리는 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-203">In the next iteration, we will refactor our validation logic and database access logic out of our controllers.</span></span> <span data-ttu-id="8bb39-204">더 유지 하 고 느슨하게 결합 된 응용 프로그램을 만들 수 있도록 몇 가지 소프트웨어 디자인 원칙을 활용을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-204">We'll take advantage of several software design principles to enable us to create a more loosely coupled, and more maintainable, application.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="8bb39-205">[이전](iteration-2-make-the-application-look-nice-cs.md)
[다음](iteration-4-make-the-application-loosely-coupled-cs.md)</span><span class="sxs-lookup"><span data-stu-id="8bb39-205">[Previous](iteration-2-make-the-application-look-nice-cs.md)
[Next](iteration-4-make-the-application-loosely-coupled-cs.md)</span></span>
