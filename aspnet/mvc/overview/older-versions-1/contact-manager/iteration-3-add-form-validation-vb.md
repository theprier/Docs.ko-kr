---
uid: mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-vb
title: '반복 #3-양식 유효성 검사 추가 (VB) | Microsoft Docs'
author: microsoft
description: 세 번째 반복에서는 기본 양식 유효성 검사를 추가합니다. 사용자를 방지할 수를 필요한 형식의 필드를 완료 하지 않고 폼을 제출 합니다. 또한 emai 유효성을 검사 하는 중...
ms.author: aspnetcontent
ms.date: 02/20/2009
ms.assetid: 4805e75a-7911-46e3-b11b-229a6eed245e
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-vb
msc.type: authoredcontent
ms.openlocfilehash: a02178bfb662f180343ad32a6453b910e8e70471
ms.sourcegitcommit: a25b572eaed21791230c85416f449f66a405ec19
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2018
ms.locfileid: "39396210"
---
<a name="iteration-3--add-form-validation-vb"></a><span data-ttu-id="871ad-105">반복 #3-양식 유효성 검사 추가 (VB)</span><span class="sxs-lookup"><span data-stu-id="871ad-105">Iteration #3 – Add form validation (VB)</span></span>
====================
<span data-ttu-id="871ad-106">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="871ad-106">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="871ad-107">코드 다운로드</span><span class="sxs-lookup"><span data-stu-id="871ad-107">Download Code</span></span>](iteration-3-add-form-validation-vb/_static/contactmanager_3_vb1.zip)

> <span data-ttu-id="871ad-108">세 번째 반복에서는 기본 양식 유효성 검사를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-108">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="871ad-109">사용자를 방지할 수를 필요한 형식의 필드를 완료 하지 않고 폼을 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-109">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="871ad-110">또한 전자 메일 주소 및 전화 번호 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-110">We also validate email addresses and phone numbers.</span></span>


## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a><span data-ttu-id="871ad-111">연락처 관리 ASP.NET MVC 응용 프로그램을 작성 (VB)</span><span class="sxs-lookup"><span data-stu-id="871ad-111">Building a Contact Management ASP.NET MVC Application (VB)</span></span>
  

<span data-ttu-id="871ad-112">이 시리즈의 자습서에서 전체 연락처 관리 응용을 프로그램 시작부터 완료를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-112">In this series of tutorials, we build an entire Contact Management application from start to finish.</span></span> <span data-ttu-id="871ad-113">연락처 관리자 응용 프로그램에 사용자의 목록을 포함 된 상점 연락처 정보-이름, 전화 번호 및 전자 메일 주소-할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-113">The Contact Manager application enables you to store contact information - names, phone numbers and email addresses - for a list of people.</span></span>

<span data-ttu-id="871ad-114">여러 반복에 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-114">We build the application over multiple iterations.</span></span> <span data-ttu-id="871ad-115">각 반복에서 점진적으로 응용 프로그램을 개선 했습니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-115">With each iteration, we gradually improve the application.</span></span> <span data-ttu-id="871ad-116">이렇게 여러 반복의 목표는 각 변경의 이유를 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-116">The goal of this multiple iteration approach is to enable you to understand the reason for each change.</span></span>

- <span data-ttu-id="871ad-117">반복 #1-응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-117">Iteration #1 - Create the application.</span></span> <span data-ttu-id="871ad-118">첫 번째 반복에서 연락처 관리자에서에서 만드는 가장 간단한 방법은 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-118">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="871ad-119">기본 데이터베이스 작업에 대 한 지원 추가: 만들기, 읽기, 업데이트 및 삭제 (CRUD).</span><span class="sxs-lookup"><span data-stu-id="871ad-119">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>

- <span data-ttu-id="871ad-120">반복 #2-보기 좋게 응용 프로그램을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-120">Iteration #2 - Make the application look nice.</span></span> <span data-ttu-id="871ad-121">이 반복에서 기본 ASP.NET MVC 보기 마스터 페이지를 수정 및 스타일 시트를 연계 하 여 응용 프로그램의 모양을 개선 합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-121">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>

- <span data-ttu-id="871ad-122">반복 #3-양식 유효성 검사를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-122">Iteration #3 - Add form validation.</span></span> <span data-ttu-id="871ad-123">세 번째 반복에서는 기본 양식 유효성 검사를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-123">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="871ad-124">사용자를 방지할 수를 필요한 형식의 필드를 완료 하지 않고 폼을 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-124">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="871ad-125">또한 전자 메일 주소 및 전화 번호 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-125">We also validate email addresses and phone numbers.</span></span>

- <span data-ttu-id="871ad-126">반복 #4-느슨하게 결합 된 응용 프로그램을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-126">Iteration #4 - Make the application loosely coupled.</span></span> <span data-ttu-id="871ad-127">이 네 번째 반복에서는 활용 쉽게 유지 관리 하 고 연락처 관리자 응용 프로그램을 수정 하려면 몇 가지 소프트웨어 디자인 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-127">In this fourth iteration, we take advantage of several software design patterns to make it easier to maintain and modify the Contact Manager application.</span></span> <span data-ttu-id="871ad-128">예를 들어, 리포지토리 패턴 및 종속성 주입 패턴을 사용 하 여 응용 프로그램을 리팩터링 했습니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-128">For example, we refactor our application to use the Repository pattern and the Dependency Injection pattern.</span></span>

- <span data-ttu-id="871ad-129">반복 #5-단위 테스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-129">Iteration #5 - Create unit tests.</span></span> <span data-ttu-id="871ad-130">다섯 번째 반복에서에서는 쉽게 응용 프로그램 유지 관리 하 고 단위 테스트를 추가 하 여 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-130">In the fifth iteration, we make our application easier to maintain and modify by adding unit tests.</span></span> <span data-ttu-id="871ad-131">데이터 모델 클래스를 모의 하 고는 컨트롤러 및 유효성 검사 논리에 대 한 단위 테스트를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-131">We mock our data model classes and build unit tests for our controllers and validation logic.</span></span>

- <span data-ttu-id="871ad-132">반복 #6-테스트 중심 개발을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-132">Iteration #6 - Use test-driven development.</span></span> <span data-ttu-id="871ad-133">이 여섯 번째 반복에서는 추가 새로운 기능을 응용 프로그램 먼저 단위 테스트를 작성 하 고 단위 테스트에 대 한 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-133">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="871ad-134">이 반복에서는 메일 그룹을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-134">In this iteration, we add contact groups.</span></span>

- <span data-ttu-id="871ad-135">반복 #7 – Ajax 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-135">Iteration #7 - Add Ajax functionality.</span></span> <span data-ttu-id="871ad-136">일곱 번째 반복에서 개선할 응용 프로그램의 성능과 응답성 Ajax에 대 한 지원을 추가 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-136">In the seventh iteration, we improve the responsiveness and performance of our application by adding support for Ajax.</span></span>


## <a name="this-iteration"></a><span data-ttu-id="871ad-137">이 반복</span><span class="sxs-lookup"><span data-stu-id="871ad-137">This Iteration</span></span>

<span data-ttu-id="871ad-138">연락처 관리자 응용 프로그램의이 두 번째 반복에서는 기본 양식 유효성 검사를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-138">In this second iteration of the Contact Manager application, we add basic form validation.</span></span> <span data-ttu-id="871ad-139">사용자를 방지할 수를 필요한 형식의 필드에 대 한 값을 입력 하지 않고 연락처를 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-139">We prevent people from submitting a contact without entering values for required form fields.</span></span> <span data-ttu-id="871ad-140">또한 전화 번호 및 전자 메일 주소 (그림 1 참조) 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-140">We also validate phone numbers and email addresses (see Figure 1).</span></span>


<span data-ttu-id="871ad-141">[![새 프로젝트 대화 상자](iteration-3-add-form-validation-vb/_static/image1.jpg)](iteration-3-add-form-validation-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="871ad-141">[![The New Project dialog box](iteration-3-add-form-validation-vb/_static/image1.jpg)](iteration-3-add-form-validation-vb/_static/image1.png)</span></span>

<span data-ttu-id="871ad-142">**그림 01**: 유효성 검사를 사용 하 여 폼 ([큰 이미지를 보려면 클릭](iteration-3-add-form-validation-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="871ad-142">**Figure 01**: A form with validation ([Click to view full-size image](iteration-3-add-form-validation-vb/_static/image2.png))</span></span>


<span data-ttu-id="871ad-143">이 반복에서 컨트롤러 작업에 직접 유효성 검사 논리를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-143">In this iteration, we add the validation logic directly to the controller actions.</span></span> <span data-ttu-id="871ad-144">일반적으로 ASP.NET MVC 응용 프로그램에 유효성 검사를 추가 하려면 권장 되는 방법은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-144">In general, this is not the recommended way to add validation to an ASP.NET MVC application.</span></span> <span data-ttu-id="871ad-145">별도의 응용 프로그램 s 유효성 검사 논리를 배치 하는 것이 좋습니다 [서비스 계층](http://martinfowler.com/eaaCatalog/serviceLayer.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-145">A better approach is to place an application s validation logic in a separate [service layer](http://martinfowler.com/eaaCatalog/serviceLayer.html).</span></span> <span data-ttu-id="871ad-146">다음 반복에서 응용 프로그램을 관리할 수 있도록 연락처 관리자 응용 프로그램을 리팩터링 했습니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-146">In the next iteration, we refactor the Contact Manager application to make the application more maintainable.</span></span>

<span data-ttu-id="871ad-147">이 반복에서 간단 하 게,에서는 모든 유효성 검사 코드를 직접 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-147">In this iteration, to keep things simple, we write all of the validation code by hand.</span></span> <span data-ttu-id="871ad-148">유효성 검사 코드를 직접 작성 하는 대신 유효성 검사 프레임 워크를 활용할 수 했습니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-148">Instead of writing the validation code ourselves, we could take advantage of a validation framework.</span></span> <span data-ttu-id="871ad-149">예를 들어, ASP.NET MVC 응용 프로그램에 대 한 유효성 검사 논리를 구현 하는 Microsoft Enterprise Library 유효성 검사 응용 프로그램 블록 (VAB)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-149">For example, you can use the Microsoft Enterprise Library Validation Application Block (VAB) to implement the validation logic for your ASP.NET MVC application.</span></span> <span data-ttu-id="871ad-150">유효성 검사 응용 프로그램 블록에 대 한 자세한 내용은 다음을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="871ad-150">To learn more about the Validation Application Block, see:</span></span>

[*http://msdn.microsoft.com/library/dd203099.aspx*](https://msdn.microsoft.com/library/dd203099.aspx)

## <a name="adding-validation-to-the-create-view"></a><span data-ttu-id="871ad-151">Create View에 유효성 검사 추가</span><span class="sxs-lookup"><span data-stu-id="871ad-151">Adding Validation to the Create View</span></span>

<span data-ttu-id="871ad-152">만들기 뷰를 유효성 검사 논리를 추가 하 여 시작 s 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-152">Let s start by adding validation logic to the Create view.</span></span> <span data-ttu-id="871ad-153">다행 스럽게도 Visual Studio를 사용 하 여 만들기 뷰를 생성 하기 때문에 만들기 이미 뷰에 모든 필요한 사용자 인터페이스 논리 유효성 검사 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-153">Fortunately, because we generated the Create view with Visual Studio, the Create view already contains all of the necessary user interface logic to display validation messages.</span></span> <span data-ttu-id="871ad-154">만들기 뷰 목록 1에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-154">The Create view is contained in Listing 1.</span></span>

<span data-ttu-id="871ad-155">**목록 1-\Views\Contact\Create.aspx**</span><span class="sxs-lookup"><span data-stu-id="871ad-155">**Listing 1 - \Views\Contact\Create.aspx**</span></span>

[!code-aspx[Main](iteration-3-add-form-validation-vb/samples/sample1.aspx)]

<span data-ttu-id="871ad-156">필드 유효성 검사 오류 클래스는 Html.ValidationMessage() 도우미에 의해 렌더링 된 출력 스타일 지정에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-156">The field-validation-error class is used to style the output rendered by the Html.ValidationMessage() helper.</span></span> <span data-ttu-id="871ad-157">입력 유효성 검사 오류 클래스 스타일 Html.TextBox() 도우미에 의해 렌더링 된 텍스트 (입력)에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-157">The input-validation-error class is used to style the textbox (input) rendered by the Html.TextBox() helper.</span></span> <span data-ttu-id="871ad-158">유효성 검사-요약-오류 클래스는 렌더링 Html.ValidationSummary() 도우미에 의해 순서가 지정 되지 않은 목록 스타일에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-158">The validation-summary-errors class is used to style the unordered list rendered by the Html.ValidationSummary() helper.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="871ad-159">유효성 검사 오류 메시지의 모양을 사용자 지정 하려면이 섹션에 설명 된 스타일 시트 클래스를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-159">You can modify the style sheet classes described in this section to customize the appearance of validation error messages.</span></span>


## <a name="adding-validation-logic-to-the-create-action"></a><span data-ttu-id="871ad-160">유효성 검사 논리를 추가 된 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="871ad-160">Adding Validation Logic to the Create Action</span></span>

<span data-ttu-id="871ad-161">현재, Create view 유효성 검사 오류 메시지를 모든 메시지를 생성 하는 논리를 작성 하지 않은 것 때문에 되지 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-161">Right now, the Create view never displays validation error messages because we have not written the logic to generate any messages.</span></span> <span data-ttu-id="871ad-162">유효성 검사 오류 메시지를 표시 하려면 ModelState에 오류 메시지를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-162">In order to display validation error messages, you need to add the error messages to ModelState.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="871ad-163">UpdateModel() 메서드 오류 메시지를 추가 ModelState 자동으로 폼 필드의 값 속성에 할당 오류가 발생 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="871ad-163">The UpdateModel() method adds error messages to ModelState automatically when there is an error assigning the value of a form field to a property.</span></span> <span data-ttu-id="871ad-164">예를 들어, 날짜/시간 값을 받아들이는 BirthDate 속성에 "apple" 문자열을 할당 하려고 하면 다음 UpdateModel() 메서드는 오류를 추가 ModelState 합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-164">For example, if you attempt to assign the string "apple" to a BirthDate property that accepts DateTime values, then the UpdateModel() method adds an error to ModelState.</span></span>


<span data-ttu-id="871ad-165">목록 2에서 수정 된 create () 메서드를 데이터베이스에 새 연락처를 삽입 하기 전에 연락처 클래스의 속성의 유효성을 검사 하는 새 섹션을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-165">The modified Create() method in Listing 2 contains a new section that validates the properties of the Contact class before the new contact is inserted into the database.</span></span>

<span data-ttu-id="871ad-166">**2-Controllers\ContactController.vb (유효성 검사를 사용 하 여 만들기)를 나열합니다.**</span><span class="sxs-lookup"><span data-stu-id="871ad-166">**Listing 2 - Controllers\ContactController.vb (Create with validation)**</span></span>

[!code-vb[Main](iteration-3-add-form-validation-vb/samples/sample2.vb)]

<span data-ttu-id="871ad-167">유효성 검사 섹션은 4 개의 고유한 유효성 검사 규칙을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-167">The validate section enforces four distinct validation rules:</span></span>

- <span data-ttu-id="871ad-168">FirstName 속성에는 길이가 0 보다 크고 있어야 합니다. (및의 공백 전적으로 구성 될 수 없습니다)</span><span class="sxs-lookup"><span data-stu-id="871ad-168">The FirstName property must have a length greater than zero (and it cannot consist solely of spaces)</span></span>
- <span data-ttu-id="871ad-169">LastName 속성에는 길이가 0 보다 크고 있어야 합니다. (및의 공백 전적으로 구성 될 수 없습니다)</span><span class="sxs-lookup"><span data-stu-id="871ad-169">The LastName property must have a length greater than zero (and it cannot consist solely of spaces)</span></span>
- <span data-ttu-id="871ad-170">Phone 속성 값이 있으면 (길이가 0 보다 큰) Phone 속성에는 정규식과 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-170">If the Phone property has a value (has a length greater than 0) then the Phone property must match a regular expression.</span></span>
- <span data-ttu-id="871ad-171">전자 메일 속성 값이 있으면 (길이가 0 보다 큰) 전자 메일 속성에는 정규식과 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-171">If the Email property has a value (has a length greater than 0) then the Email property must match a regular expression.</span></span>

<span data-ttu-id="871ad-172">유효성 검사 규칙 위반의 경우 오류 메시지가 AddModelError() 메서드를 사용 하 여 ModelState에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-172">When there is a validation rule violation, an error message is added to ModelState with the help of the AddModelError() method.</span></span> <span data-ttu-id="871ad-173">ModelState에 메시지를 추가 하는 속성의 이름 및 유효성 검사 오류 메시지의 텍스트를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-173">When you add a message to ModelState, you provide the name of a property and the text of a validation error message.</span></span> <span data-ttu-id="871ad-174">이 오류 메시지는 Html.ValidationSummary() 및 Html.ValidationMessage() 도우미 메서드에서 보기에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-174">This error message is displayed in the view by the Html.ValidationSummary() and Html.ValidationMessage() helper methods.</span></span>

<span data-ttu-id="871ad-175">유효성 검사 규칙은 실행 후 ModelState의 IsValid 속성을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-175">After the validation rules are executed, the IsValid property of ModelState is checked.</span></span> <span data-ttu-id="871ad-176">ModelState에 유효성 검사 오류 메시지를 추가한 경우 IsValid 속성은 false를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-176">The IsValid property returns false when any validation error messages have been added to ModelState.</span></span> <span data-ttu-id="871ad-177">유효성 검사에 실패할 경우 오류 메시지와 함께 만들기 양식은 다시 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-177">If validation fails, the Create form is redisplayed with the error messages.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="871ad-178">정규식 리포지토리에서 전화 번호 및 전자 메일 주소 유효성을 검사 하는 것에 대 한 정규식을 받았습니다. [*http://regexlib.com*](http://regexlib.com)</span><span class="sxs-lookup"><span data-stu-id="871ad-178">I got the regular expressions for validating the phone number and email address from the regular expression repository at [*http://regexlib.com*](http://regexlib.com)</span></span>


## <a name="adding-validation-logic-to-the-edit-action"></a><span data-ttu-id="871ad-179">편집 작업으로 유효성 검사 논리를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-179">Adding Validation Logic to the Edit Action</span></span>

<span data-ttu-id="871ad-180">되 작업 연락처를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-180">The Edit() action updates a Contact.</span></span> <span data-ttu-id="871ad-181">되 작업 create () 작업으로 동일한 유효성 검사가 정확 하 게 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-181">The Edit() action needs to perform exactly the same validation as the Create() action.</span></span> <span data-ttu-id="871ad-182">동일한 유효성 검사 코드를 복제 하는 대신 동일한 유효성 검사 메서드를 호출 하는 create () 및 되 작업 있도록 연락처 컨트롤러를 리팩터링 해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-182">Instead of duplicating the same validation code, we should refactor the Contact controller so that both the Create() and Edit() actions call the same validation method.</span></span>

<span data-ttu-id="871ad-183">수정 된 연락처 컨트롤러 클래스는 목록 3에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-183">The modified Contact controller class is contained in Listing 3.</span></span> <span data-ttu-id="871ad-184">이 클래스는 create () 및 되 작업 내에서 호출 되는 새 ValidateContact() 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-184">This class has a new ValidateContact() method that is called within both the Create() and Edit() actions.</span></span>

<span data-ttu-id="871ad-185">**3-Controllers\ContactController.vb 나열**</span><span class="sxs-lookup"><span data-stu-id="871ad-185">**Listing 3 - Controllers\ContactController.vb**</span></span>

[!code-vb[Main](iteration-3-add-form-validation-vb/samples/sample3.vb)]

## <a name="summary"></a><span data-ttu-id="871ad-186">요약</span><span class="sxs-lookup"><span data-stu-id="871ad-186">Summary</span></span>

<span data-ttu-id="871ad-187">이 반복에서 연락처 관리자 응용 프로그램 기본 양식 유효성 검사를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-187">In this iteration, we added basic form validation to our Contact Manager application.</span></span> <span data-ttu-id="871ad-188">유효성 검사 논리에는 사용자가 새 연락처를 제출 하거나 FirstName 및 LastName 속성 값을 제공 하지 않고 기존 연락처를 편집 하지 못하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-188">Our validation logic prevents users from submitting a new contact or editing an existing contact without supplying values for the FirstName and LastName properties.</span></span> <span data-ttu-id="871ad-189">또한 사용자가 올바른 전화 번호 및 전자 메일 주소를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-189">Furthermore, users must supply valid phone numbers and email addresses.</span></span>

<span data-ttu-id="871ad-190">이 반복에서 추가한 유효성 검사 논리를 연락처 관리자 응용 프로그램 가능한 가장 쉬운 방법으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-190">In this iteration, we added the validation logic to our Contact Manager application in the easiest way possible.</span></span> <span data-ttu-id="871ad-191">그러나이 유효성 검사 논리는 컨트롤러 논리를 혼합 문제가 생기게 됩니다 우리 회사에 장기적으로.</span><span class="sxs-lookup"><span data-stu-id="871ad-191">However, mixing our validation logic into our controller logic will create problems for us in the long term.</span></span> <span data-ttu-id="871ad-192">응용 프로그램 유지 관리 하 고 시간이 지남에 따라 수정 하기가 더 어렵습니다 됩니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-192">Our application will be more difficult to maintain and modify over time.</span></span>

<span data-ttu-id="871ad-193">다음 반복에서에서는 리팩터링이 유효성 검사 논리 및 데이터베이스 액세스 논리는 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-193">In the next iteration, we will refactor our validation logic and database access logic out of our controllers.</span></span> <span data-ttu-id="871ad-194">이점은 더 느슨하게 결합 하 고 유지 관리, 응용 프로그램을 만들 수 있도록 몇 가지 소프트웨어 디자인 원칙을 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="871ad-194">We'll take advantage of several software design principles to enable us to create a more loosely coupled, and more maintainable, application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="871ad-195">[이전](iteration-2-make-the-application-look-nice-vb.md)
> [다음](iteration-4-make-the-application-loosely-coupled-vb.md)</span><span class="sxs-lookup"><span data-stu-id="871ad-195">[Previous](iteration-2-make-the-application-look-nice-vb.md)
[Next](iteration-4-make-the-application-loosely-coupled-vb.md)</span></span>
