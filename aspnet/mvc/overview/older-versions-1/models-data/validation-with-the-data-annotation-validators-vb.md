---
uid: mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
title: 데이터 주석 유효성 검사기 (VB)와 유효성 검사 | Microsoft Docs
author: microsoft
description: ASP.NET MVC 응용 프로그램 내에서 유효성 검사를 수행 하려면 데이터 주석 모델 바인더 활용 합니다. 다양 한 유형의 유효성 검사기를 사용 하는 방법 알아보기...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/29/2009
ms.topic: article
ms.assetid: 0d23ff2b-f2ec-434a-be3b-1180beeccba3
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
msc.type: authoredcontent
ms.openlocfilehash: d1987182a44a0ad3f91f455342dc934d1dd50267
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30870169"
---
<a name="validation-with-the-data-annotation-validators-vb"></a><span data-ttu-id="a82f2-104">데이터 주석 유효성 검사기 (VB)와 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="a82f2-104">Validation with the Data Annotation Validators (VB)</span></span>
====================
<span data-ttu-id="a82f2-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="a82f2-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="a82f2-106">ASP.NET MVC 응용 프로그램 내에서 유효성 검사를 수행 하려면 데이터 주석 모델 바인더 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-106">Take advantage of the Data Annotation Model Binder to perform validation within an ASP.NET MVC application.</span></span> <span data-ttu-id="a82f2-107">다양 한 유형의 유효성 검사기 특성을 사용 하 고 Microsoft Entity Framework에서 사용 하는 방법에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-107">Learn how to use the different types of validator attributes and work with them in the Microsoft Entity Framework.</span></span>


<span data-ttu-id="a82f2-108">이 자습서에서는 ASP.NET MVC 응용 프로그램에서 유효성 검사를 수행 하려면 데이터 주석 유효성 검사기를 사용 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-108">In this tutorial, you learn how to use the Data Annotation validators to perform validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="a82f2-109">데이터 주석 유효성 검사기를 사용은 필수와 같은 하나 이상의 특성 – 또는 StringLength 특성을 추가 하면 – 클래스 속성에 유효성 검사를 수행할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-109">The advantage of using the Data Annotation validators is that they enable you to perform validation simply by adding one or more attributes – such as the Required or StringLength attribute – to a class property.</span></span>

<span data-ttu-id="a82f2-110">데이터 주석 유효성 검사기를 사용 하려면 먼저 데이터 주석 모델 바인더를 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-110">Before you can use the Data Annotation validators, you must download the Data Annotations Model Binder.</span></span> <span data-ttu-id="a82f2-111">클릭 하 여 데이터 주석 모델 바인더 예제는 CodePlex 웹 사이트에서 다운로드할 수 있습니다 [여기](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471)합니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-111">You can download the Data Annotations Model Binder Sample from the CodePlex website by clicking [here](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471).</span></span>


<span data-ttu-id="a82f2-112">데이터 주석 모델 바인더에서 공식 Microsoft ASP.NET MVC 프레임 워크 부분이 아닌지 이해 하는 것이 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-112">It is important to understand that the Data Annotations Model Binder is not an official part of the Microsoft ASP.NET MVC framework.</span></span> <span data-ttu-id="a82f2-113">데이터 주석 모델 바인더는 Microsoft ASP.NET MVC 팀에 의해 생성 되었지만, 공식 제품 기술 지원 데이터 주석 모델 바인더에 대 한 설명 및이 자습서에 사용 된 Microsoft 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-113">Although the Data Annotations Model Binder was created by the Microsoft ASP.NET MVC team, Microsoft does not offer official product support for the Data Annotations Model Binder described and used in this tutorial.</span></span>


## <a name="using-the-data-annotation-model-binder"></a><span data-ttu-id="a82f2-114">데이터 주석 모델 바인더를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="a82f2-114">Using the Data Annotation Model Binder</span></span>

<span data-ttu-id="a82f2-115">데이터 주석 모델 바인더에서 ASP.NET MVC 응용 프로그램을 사용 하려면 먼저 Microsoft.Web.Mvc.DataAnnotations.dll 어셈블리와 System.ComponentModel.DataAnnotations.dll 어셈블리에 대 한 참조를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-115">In order to use the Data Annotations Model Binder in an ASP.NET MVC application, you first need to add a reference to the Microsoft.Web.Mvc.DataAnnotations.dll assembly and the System.ComponentModel.DataAnnotations.dll assembly.</span></span> <span data-ttu-id="a82f2-116">메뉴 옵션을 선택 **프로젝트, 참조 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-116">Select the menu option **Project, Add Reference**.</span></span> <span data-ttu-id="a82f2-117">그런 다음 클릭는 **찾아보기** 탭를 다운로드 (하 여 압축을 푼) 데이터 주석 모델 바인더 샘플 위치로 이동 (참조 **그림 1**).</span><span class="sxs-lookup"><span data-stu-id="a82f2-117">Next click the **Browse** tab and browse to the location where you downloaded (and unzipped) the Data Annotations Model Binder sample (see **Figure 1**).</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image2.png)](validation-with-the-data-annotation-validators-vb/_static/image1.png)

<span data-ttu-id="a82f2-118">**그림 1**: 데이터 주석 모델 바인더에 대 한 참조를 추가 ([전체 크기 이미지를 보려면 클릭](validation-with-the-data-annotation-validators-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="a82f2-118">**Figure 1**: Adding a reference to the Data Annotations Model Binder ([Click to view full-size image](validation-with-the-data-annotation-validators-vb/_static/image3.png))</span></span>

<span data-ttu-id="a82f2-119">Microsoft.Web.Mvc.DataAnnotations.dll 어셈블리와 System.ComponentModel.DataAnnotations.dll 어셈블리를 선택 하 고 클릭는 **확인** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-119">Select both the Microsoft.Web.Mvc.DataAnnotations.dll assembly and the System.ComponentModel.DataAnnotations.dll assembly and click the **OK** button.</span></span>


<span data-ttu-id="a82f2-120">데이터 주석 모델 바인더 사용 하 여.NET Framework 서비스 팩 1에 포함 된 System.ComponentModel.DataAnnotations.dll 어셈블리를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-120">You cannot use the System.ComponentModel.DataAnnotations.dll assembly included with .NET Framework Service Pack 1 with the Data Annotations Model Binder.</span></span> <span data-ttu-id="a82f2-121">데이터 주석 모델 바인더 샘플 다운로드에 포함 된 System.ComponentModel.DataAnnotations.dll 어셈블리의 버전을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-121">You must use the version of the System.ComponentModel.DataAnnotations.dll assembly included with the Data Annotations Model Binder Sample download.</span></span>


<span data-ttu-id="a82f2-122">마지막으로, DataAnnotations 모델 바인더를 Global.asax 파일에 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-122">Finally, you need to register the DataAnnotations Model Binder in the Global.asax file.</span></span> <span data-ttu-id="a82f2-123">응용 프로그램에 다음 코드 줄을 추가\_start () 이벤트 처리기를 응용 프로그램\_start () 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-123">Add the following line of code to the Application\_Start() event handler so that the Application\_Start() method looks like this:</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample1.vb)]

<span data-ttu-id="a82f2-124">이 줄의 코드 전체 ASP.NET MVC 응용 프로그램에 대 한 기본 모델 바인더는 DataAnnotationsModelBinder 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-124">This line of code registers the DataAnnotationsModelBinder as the default model binder for the entire ASP.NET MVC application.</span></span>

## <a name="using-the-data-annotation-validator-attributes"></a><span data-ttu-id="a82f2-125">데이터 주석 유효성 검사기 특성을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="a82f2-125">Using the Data Annotation Validator Attributes</span></span>

<span data-ttu-id="a82f2-126">데이터 주석 모델 바인더를 사용 하면 유효성 검사기 특성을 사용 하면 유효성 검사를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-126">When you use the Data Annotations Model Binder, you use validator attributes to perform validation.</span></span> <span data-ttu-id="a82f2-127">System.ComponentModel.DataAnnotations 네임 스페이스에는 다음과 같은 유효성 검사기 특성이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-127">The System.ComponentModel.DataAnnotations namespace includes the following validator attributes:</span></span>

- <span data-ttu-id="a82f2-128">범위는-지정된 된 범위의 값 사이 해당 속성의 값이 있는지 여부를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-128">Range – Enables you to validate whether the value of a property falls between a specified range of values.</span></span>
- <span data-ttu-id="a82f2-129">ReqularExpression-를 사용 하면 속성의 값이 지정 된 정규식 패턴과 일치 하는지 여부를 검증 합니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-129">ReqularExpression – Enables you to validate whether the value of a property matches a specified regular expression pattern.</span></span>
- <span data-ttu-id="a82f2-130">필요한 – 필요에 따라 속성을 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-130">Required – Enables you to mark a property as required.</span></span>
- <span data-ttu-id="a82f2-131">StringLength-를 사용 하는 문자열 속성에 대 한 최대 길이 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-131">StringLength – Enables you to specify a maximum length for a string property.</span></span>
- <span data-ttu-id="a82f2-132">유효성 검사-모든 유효성 검사기 특성에 대 한 기본 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-132">Validation – The base class for all validator attributes.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="a82f2-133">표준 유효성 검사기의 유효성 검사 요구 사항 충족 되지 않은 경우 그런 다음 항상 해야 새 유효성 검사기 특성의 기본 유효성 검사 특성에서 상속 하 여 사용자 지정 유효성 검사기 특성을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-133">If your validation needs are not satisfied by any of the standard validators then you always have the option of creating a custom validator attribute by inheriting a new validator attribute from the base Validation attribute.</span></span>


<span data-ttu-id="a82f2-134">Product 클래스에 **목록 1** 이러한 유효성 검사기 특성을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-134">The Product class in **Listing 1** illustrates how to use these validator attributes.</span></span> <span data-ttu-id="a82f2-135">이름, 설명 및 UnitPrice 속성 표시 해야 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="a82f2-135">The Name, Description, and UnitPrice properties are marked as required.</span></span> <span data-ttu-id="a82f2-136">Name 속성은 10 자 미만의 문자열 길이가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-136">The Name property must have a string length that is less than 10 characters.</span></span> <span data-ttu-id="a82f2-137">마지막으로, UnitPrice 속성 통화 금액을 나타내는 정규식 패턴을 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-137">Finally, the UnitPrice property must match a regular expression pattern that represents a currency amount.</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample2.vb)]

<span data-ttu-id="a82f2-138">**Listing 1**: Models\Product.vb</span><span class="sxs-lookup"><span data-stu-id="a82f2-138">**Listing 1**: Models\Product.vb</span></span>

<span data-ttu-id="a82f2-139">Product 클래스에는 하나의 추가 특성을 사용 하는 방법을 보여 줍니다: / / DisplayName 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-139">The Product class illustrates how to use one additional attribute: the DisplayName attribute.</span></span> <span data-ttu-id="a82f2-140">/ / DisplayName 특성을 사용 하면 오류 메시지가 표시 되는 속성 때 속성의 이름을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-140">The DisplayName attribute enables you to modify the name of the property when the property is displayed in an error message.</span></span> <span data-ttu-id="a82f2-141">"UnitPrice 필드는 필수" 오류 메시지를 표시 하는 대신 오류 메시지 "Price 필드는 필수" 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-141">Instead of displaying the error message "The UnitPrice field is required" you can display the error message "The Price field is required".</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="a82f2-142">완전히 유효성 검사기에서 표시 되는 오류 메시지 사용자 지정 하려는 경우 다음과 같이 유효성 검사기의 ErrorMessage 속성에 사용자 지정 오류 메시지를 할당할 수 있습니다. `<Required(ErrorMessage:="This field needs a value!")>`</span><span class="sxs-lookup"><span data-stu-id="a82f2-142">If you want to completely customize the error message displayed by a validator then you can assign a custom error message to the validator's ErrorMessage property like this: `<Required(ErrorMessage:="This field needs a value!")>`</span></span>


<span data-ttu-id="a82f2-143">Product 클래스에 사용할 수 있습니다 **목록 1** 에서 create () 컨트롤러 작업으로 **목록 2**합니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-143">You can use the Product class in **Listing 1** with the Create() controller action in **Listing 2**.</span></span> <span data-ttu-id="a82f2-144">모델 상태 오류를 포함 하는 경우이 컨트롤러 작업 만들기 뷰를 다시 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-144">This controller action redisplays the Create view when model state contains any errors.</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample3.vb)]

<span data-ttu-id="a82f2-145">**Listing 2**: Controllers\ProductController.vb</span><span class="sxs-lookup"><span data-stu-id="a82f2-145">**Listing 2**: Controllers\ProductController.vb</span></span>

<span data-ttu-id="a82f2-146">마지막으로,에서 보기를 만들 수 있습니다 **목록 3** create () 작업을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 하 여 **뷰 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-146">Finally, you can create the view in **Listing 3** by right-clicking the Create() action and selecting the menu option **Add View**.</span></span> <span data-ttu-id="a82f2-147">모델 클래스로 제품 클래스와 함께 강력한 형식의 뷰를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-147">Create a strongly-typed view with the Product class as the model class.</span></span> <span data-ttu-id="a82f2-148">선택 **만들기** 보기 콘텐츠 드롭다운 목록에서 (참조 **그림 2**).</span><span class="sxs-lookup"><span data-stu-id="a82f2-148">Select **Create** from the view content dropdown list (see **Figure 2**).</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image5.png)](validation-with-the-data-annotation-validators-vb/_static/image4.png)

<span data-ttu-id="a82f2-149">**그림 2**: 만들기 뷰 추가</span><span class="sxs-lookup"><span data-stu-id="a82f2-149">**Figure 2**: Adding the Create View</span></span>

[!code-aspx[Main](validation-with-the-data-annotation-validators-vb/samples/sample4.aspx)]

<span data-ttu-id="a82f2-150">**Listing 3**: Views\Product\Create.aspx</span><span class="sxs-lookup"><span data-stu-id="a82f2-150">**Listing 3**: Views\Product\Create.aspx</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="a82f2-151">에 의해 생성 된 양식 만들기에서에서 Id 필드를 제거는 **뷰 추가** 메뉴 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-151">Remove the Id field from the Create form generated by the **Add View** menu option.</span></span> <span data-ttu-id="a82f2-152">Id 열에 해당 하는 Id 필드를 때문에 사용자가을이 필드에 대 한 값을 입력 하지 않으려면입니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-152">Because the Id field corresponds to an Identity column, you don't want to allow users to enter a value for this field.</span></span>


<span data-ttu-id="a82f2-153">제품을 만들기 위한 양식을 전송 하면 필수 필드에 대 한 값을 입력 하지 않으면 경우 유효성 검사 오류 메시지를 **그림 3** 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-153">If you submit the form for creating a Product and you do not enter values for the required fields, then the validation error messages in **Figure 3** are displayed.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image7.png)](validation-with-the-data-annotation-validators-vb/_static/image6.png)

<span data-ttu-id="a82f2-154">**그림 3**: 누락 된 필수 필드</span><span class="sxs-lookup"><span data-stu-id="a82f2-154">**Figure 3**: Missing required fields</span></span>

<span data-ttu-id="a82f2-155">잘못 된 통화 금액을 다음 오류 메시지를 입력 하면 **그림 4** 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-155">If you enter an invalid currency amount, then the error message in **Figure 4** is displayed.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image9.png)](validation-with-the-data-annotation-validators-vb/_static/image8.png)

<span data-ttu-id="a82f2-156">**그림 4**: 잘못 된 통화 금액</span><span class="sxs-lookup"><span data-stu-id="a82f2-156">**Figure 4**: Invalid currency amount</span></span>

## <a name="using-data-annotation-validators-with-the-entity-framework"></a><span data-ttu-id="a82f2-157">데이터 주석 유효성 검사기를 사용 하 여 Entity Framework와 함께</span><span class="sxs-lookup"><span data-stu-id="a82f2-157">Using Data Annotation Validators with the Entity Framework</span></span>

<span data-ttu-id="a82f2-158">Microsoft Entity Framework를 사용 하는 데이터 모델 클래스를 생성 하는 경우 클래스에 직접 유효성 검사기 특성 적용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-158">If you are using the Microsoft Entity Framework to generate your data model classes then you cannot apply the validator attributes directly to your classes.</span></span> <span data-ttu-id="a82f2-159">Entity Framework Designer에서는 모델 클래스를 생성 하기 때문에 모델 클래스를 적용 한 변경 내용 다음에 디자이너에서 변경 하기를 덮어쓰게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-159">Because the Entity Framework Designer generates the model classes, any changes you make to the model classes will be overwritten the next time you make any changes in the Designer.</span></span>

<span data-ttu-id="a82f2-160">Entity Framework에서 생성 된 클래스와 유효성 검사기를 사용 하려면 메타 데이터 클래스를 만들 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-160">If you want to use the validators with the classes generated by the Entity Framework then you need to create meta data classes.</span></span> <span data-ttu-id="a82f2-161">유효성 검사기 실제 클래스를 적용 하는 대신 메타 데이터 클래스에 유효성 검사기를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-161">You apply the validators to the meta data class instead of applying the validators to the actual class.</span></span>

<span data-ttu-id="a82f2-162">예를 들어, Entity Framework를 사용 하 여 영화 클래스를 만든 가정해 보겠습니다 (참조 **그림 5**).</span><span class="sxs-lookup"><span data-stu-id="a82f2-162">For example, imagine that you have created a Movie class using the Entity Framework (see **Figure 5**).</span></span> <span data-ttu-id="a82f2-163">또한 영화 제목 및 감독 속성이 필수 속성을 확인 하려면 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-163">Imagine, furthermore, that you want to make the Movie Title and Director properties required properties.</span></span> <span data-ttu-id="a82f2-164">이 경우 partial 클래스와의 메타 데이터 클래스를 만들 수 있습니다 **목록 4**합니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-164">In that case, you can create the partial class and meta data class in **Listing 4**.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image11.png)](validation-with-the-data-annotation-validators-vb/_static/image10.png)

<span data-ttu-id="a82f2-165">**그림 5**: Entity Framework에서 생성 된 영화 클래스</span><span class="sxs-lookup"><span data-stu-id="a82f2-165">**Figure 5**: Movie class generated by Entity Framework</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample5.vb)]

<span data-ttu-id="a82f2-166">**Listing 4**: Models\Movie.vb</span><span class="sxs-lookup"><span data-stu-id="a82f2-166">**Listing 4**: Models\Movie.vb</span></span>

<span data-ttu-id="a82f2-167">에 있는 파일 **목록 4** 동영상, 동영상 메타 데이터 라는 두 개의 클래스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-167">The file in **Listing 4** contains two classes named Movie and MovieMetaData.</span></span> <span data-ttu-id="a82f2-168">영화 클래스는 partial 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-168">The Movie class is a partial class.</span></span> <span data-ttu-id="a82f2-169">DataModel.Designer.vb 파일에 포함 된 Entity Framework에서 생성 되는 partial 클래스에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-169">It corresponds to the partial class generated by the Entity Framework that is contained in the DataModel.Designer.vb file.</span></span>

<span data-ttu-id="a82f2-170">현재.NET framework 부분 속성을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-170">Currently, the .NET framework does not support partial properties.</span></span> <span data-ttu-id="a82f2-171">따라서 유효성 검사기 특성에 있는 파일에 정의 된 동영상 클래스의 속성에 유효성 검사기 특성을 적용 하 여 DataModel.Designer.vb 파일에 정의 된 동영상 클래스의 속성에 적용 하려면 방법이 있으면 **목록 4**.</span><span class="sxs-lookup"><span data-stu-id="a82f2-171">Therefore, there is no way to apply the validator attributes to the properties of the Movie class defined in the DataModel.Designer.vb file by applying the validator attributes to the properties of the Movie class defined in the file in **Listing 4**.</span></span>

<span data-ttu-id="a82f2-172">영화 partial 클래스 동영상 메타 데이터 클래스를 가리키는 MetadataType 특성으로 데코레이팅되 어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-172">Notice that the Movie partial class is decorated with a MetadataType attribute that points at the MovieMetaData class.</span></span> <span data-ttu-id="a82f2-173">동영상 메타 데이터 클래스는 영화 클래스의 속성에 대 한 프록시 속성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-173">The MovieMetaData class contains proxy properties for the properties of the Movie class.</span></span>

<span data-ttu-id="a82f2-174">유효성 검사기 특성 동영상 메타 데이터 클래스의 속성에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-174">The validator attributes are applied to the properties of the MovieMetaData class.</span></span> <span data-ttu-id="a82f2-175">제목, 감독 및 DateReleased 속성 모두 필수 속성으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-175">The Title, Director, and DateReleased properties are all marked as required properties.</span></span> <span data-ttu-id="a82f2-176">감독 속성 5 대 미만의 문자가 포함 된 문자열을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-176">The Director property must be assigned a string that contains less than 5 characters.</span></span> <span data-ttu-id="a82f2-177">/ / DisplayName 특성 "Date 정식 필드는 필수입니다."와 같은 오류 메시지를 표시 하려면 DateReleased 속성에 적용 되는 마지막으로,</span><span class="sxs-lookup"><span data-stu-id="a82f2-177">Finally, the DisplayName attribute is applied to the DateReleased property to display an error message like "The Date Released field is required."</span></span> <span data-ttu-id="a82f2-178">오류 대신 "DateReleased 필수 필드가입니다."</span><span class="sxs-lookup"><span data-stu-id="a82f2-178">instead of the error "The DateReleased field is required."</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="a82f2-179">공지 동영상 메타 데이터 클래스의 프록시 속성은 영화 클래스의 해당 속성을 동일한 형식을 나타낼 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-179">Notice that the proxy properties in the MovieMetaData class do not need to represent the same types as the corresponding properties in the Movie class.</span></span> <span data-ttu-id="a82f2-180">예를 들어 Director 속성이 영화 클래스에는 문자열 속성 및 동영상 메타 데이터 클래스의 개체 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-180">For example, the Director property is a string property in the Movie class and an object property in the MovieMetaData class.</span></span>


<span data-ttu-id="a82f2-181">에 있는 페이지 **그림 6** 동영상 속성에 대 한 잘못 된 값을 입력 하는 경우 반환 된 오류 메시지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-181">The page in **Figure 6** illustrates the error messages returned when you enter invalid values for the Movie properties.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image13.png)](validation-with-the-data-annotation-validators-vb/_static/image12.png)

<span data-ttu-id="a82f2-182">**그림 6**: Entity Framework와 유효성 검사기를 사용 하 여 ([전체 크기 이미지를 보려면 클릭](validation-with-the-data-annotation-validators-vb/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="a82f2-182">**Figure 6**: Using validators with the Entity Framework ([Click to view full-size image](validation-with-the-data-annotation-validators-vb/_static/image14.png))</span></span>

## <a name="summary"></a><span data-ttu-id="a82f2-183">요약</span><span class="sxs-lookup"><span data-stu-id="a82f2-183">Summary</span></span>

<span data-ttu-id="a82f2-184">이 자습서에서는 ASP.NET MVC 응용 프로그램 내에서 유효성 검사를 수행 하려면 데이터 주석 모델 바인더를 활용 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-184">In this tutorial, you learned how to take advantage of the Data Annotation Model Binder to perform validation within an ASP.NET MVC application.</span></span> <span data-ttu-id="a82f2-185">다양 한 유형의 필수 등의 유효성 검사기 특성 및 StringLength 특성을 사용 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-185">You learned how to use the different types of validator attributes such as the Required and StringLength attributes.</span></span> <span data-ttu-id="a82f2-186">또한 Microsoft Entity Framework와 함께 작업 하는 경우 이러한 특성을 사용 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="a82f2-186">You also learned how to use these attributes when working with the Microsoft Entity Framework.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="a82f2-187">이전</span><span class="sxs-lookup"><span data-stu-id="a82f2-187">Previous</span></span>](validating-with-a-service-layer-vb.md)
