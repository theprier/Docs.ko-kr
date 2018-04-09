---
uid: mvc/overview/getting-started/database-first-development/enhancing-data-validation
title: 'ASP.NET MVC를 사용 하 여 먼저 EF 데이터베이스: 데이터 유효성 검사 향상 | Microsoft Docs'
author: tfitzmac
description: MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다. 이 자습서 seri 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/29/2014
ms.topic: article
ms.assetid: 0ed5e67a-34c0-4b57-84a6-802b0fb3cd00
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/database-first-development/enhancing-data-validation
msc.type: authoredcontent
ms.openlocfilehash: 8ea2e94db7956b76c5ccf0a139ac024e38910b49
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="ef-database-first-with-aspnet-mvc-enhancing-data-validation"></a><span data-ttu-id="3c0a1-104">ASP.NET MVC를 사용 하 여 먼저 EF 데이터베이스: 데이터 유효성 검사 향상</span><span class="sxs-lookup"><span data-stu-id="3c0a1-104">EF Database First with ASP.NET MVC: Enhancing Data Validation</span></span>
====================
<span data-ttu-id="3c0a1-105">으로 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="3c0a1-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="3c0a1-106">MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-106">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="3c0a1-107">이 자습서 시리즈 자동으로 표시, 편집를 만들 수 있도록 하는 코드를 생성 하 고 데이터베이스 테이블에 있는 데이터를 삭제 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-107">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="3c0a1-108">생성 된 코드는 데이터베이스 테이블의 열에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-108">The generated code corresponds to the columns in the database table.</span></span>
> 
> <span data-ttu-id="3c0a1-109">이 부분에서는 계열의 데이터 주석 유효성 검사 요구 사항을 지정 하 고 서식을 표시 하려면 데이터 모델에 추가 하는 방법에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-109">This part of the series focuses on adding data annotations to the data model to specify validation requirements and display formatting.</span></span> <span data-ttu-id="3c0a1-110">설명 섹션에는 사용자의 의견에로 기반 향상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-110">It was improved based on feedback from users in the comments section.</span></span>


## <a name="add-data-annotations"></a><span data-ttu-id="3c0a1-111">데이터 주석 추가</span><span class="sxs-lookup"><span data-stu-id="3c0a1-111">Add data annotations</span></span>

<span data-ttu-id="3c0a1-112">이전 항목에서 볼 수 있듯이 일부 데이터 유효성 검사 규칙 사용자 입력에 자동으로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-112">As you saw in an earlier topic, some data validation rules are automatically applied to the user input.</span></span> <span data-ttu-id="3c0a1-113">예를 들어 등급 속성에 대 한 번호를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-113">For example, you can only provide a number for the Grade property.</span></span> <span data-ttu-id="3c0a1-114">더 많은 데이터 유효성 검사 규칙을 지정 하려면 데이터 주석 모델 클래스를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-114">To specify more data validation rules, you can add data annotations to your model class.</span></span> <span data-ttu-id="3c0a1-115">이러한 주석은 지정된 된 속성에 대 한 웹 응용 프로그램 전체에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-115">These annotations are applied throughout your web application for the specified property.</span></span> <span data-ttu-id="3c0a1-116">속성이 표시 되는 방식을 변경 하는 서식 특성을 적용할 수 있습니다. 와 같은 텍스트 레이블에 사용 되는 값을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-116">You can also apply formatting attributes that change how the properties are displayed; such as, changing the value used for text labels.</span></span>

<span data-ttu-id="3c0a1-117">이 자습서에서는 데이터 FirstName, LastName 및 MiddleName 속성에 대해 제공 된 값의 길이 제한 하는 주석을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-117">In this tutorial, you will add data annotations to restrict the length of the values provided for the FirstName, LastName, and MiddleName properties.</span></span> <span data-ttu-id="3c0a1-118">데이터베이스에서 이러한 값은; 50 자로 제한 그러나 웹 응용 프로그램에서 해당 문자 제한 현재 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-118">In the database, these values are limited to 50 characters; however, in your web application that character limit is currently not enforced.</span></span> <span data-ttu-id="3c0a1-119">이러한 값 중 하나에 대 한 50 개 이상의 문자를 제공 하는 사용자, 페이지를 데이터베이스에 값을 저장 하는 동안 작동이 중단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-119">If a user provides more than 50 characters for one of those values, the page will crash when attempting to save the value to the database.</span></span> <span data-ttu-id="3c0a1-120">또한 0에서 4 사이의 값으로 등급을 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-120">You will also restrict Grade to values between 0 and 4.</span></span>

<span data-ttu-id="3c0a1-121">열기는 **Student.cs** 파일에 **모델** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-121">Open the **Student.cs** file in the **Models** folder.</span></span> <span data-ttu-id="3c0a1-122">클래스에 다음 강조 표시 된 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-122">Add the following highlighted code to the class.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample1.cs?highlight=5,15,17,20)]

<span data-ttu-id="3c0a1-123">Enrollment.cs, 다음 강조 표시 된 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-123">In Enrollment.cs, add the following highlighted code.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample2.cs?highlight=5,10)]

<span data-ttu-id="3c0a1-124">솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-124">Build the solution.</span></span>

<span data-ttu-id="3c0a1-125">편집 하거나 만들 학생에 대 한 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-125">Browse to a page for editing or creating a student.</span></span> <span data-ttu-id="3c0a1-126">50 개 이상의 문자를 입력 하려고 하면 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-126">If you attempt to enter more than 50 characters, an error message is displayed.</span></span>

![오류 메시지를 표시 합니다.](enhancing-data-validation/_static/image1.png)

<span data-ttu-id="3c0a1-128">등록을 편집 하기 위해 페이지를 찾아 4 위에 등급을 제공 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-128">Browse to the page for editing enrollments, and attempt to provide a grade above 4.</span></span>

![등급 범위 오류](enhancing-data-validation/_static/image2.png)

<span data-ttu-id="3c0a1-130">속성 및 클래스를 적용할 수 있는 데이터 유효성 검사 주석 목록은 전체 참조 [System.ComponentModel.DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-130">For a full list of data validation annotations you can apply to properties and classes, see [System.ComponentModel.DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx).</span></span>

## <a name="add-metadata-classes"></a><span data-ttu-id="3c0a1-131">메타 데이터 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-131">Add metadata classes</span></span>

<span data-ttu-id="3c0a1-132">변경할; 데이터베이스를 하지 않을 경우에 작동 모델 클래스에 직접 유효성 검사 특성을 추가 그러나 데이터베이스 변경 하 고 모델 클래스를 생성 해야 할 모델 클래스에 적용 한 특성을 모두 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-132">Adding the validation attributes directly to the model class works when you do not expect the database to change; however, if your database changes and you need to regenerate the model class, you will lose all of the attributes you had applied to the model class.</span></span> <span data-ttu-id="3c0a1-133">이 방법은 매우 비효율적인 하 고 중요 한 유효성 검사 규칙이 손실 되는 경향이 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-133">This approach can be very inefficient and prone to losing important validation rules.</span></span>

<span data-ttu-id="3c0a1-134">이 문제를 방지 하려면 특성을 포함 하는 메타 데이터 클래스를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-134">To avoid this problem, you can add a metadata class that contains the attributes.</span></span> <span data-ttu-id="3c0a1-135">메타 데이터 클래스에 모델 클래스를 연결 하면 해당 특성은 모델에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-135">When you associate the model class to the metadata class, those attributes are applied to the model.</span></span> <span data-ttu-id="3c0a1-136">이 방법에서 모델 클래스의 모든 메타 데이터 클래스에 적용 된 특성을 손실 하지 않고 다시 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-136">In this approach, the model class can be regenerated without losing all of the attributes that have been applied to the metadata class.</span></span>

<span data-ttu-id="3c0a1-137">에 **모델** 폴더 라는 클래스를 추가 **Metadata.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-137">In the **Models** folder, add a class named **Metadata.cs**.</span></span>

![메타 데이터 클래스를 추가 합니다.](enhancing-data-validation/_static/image3.png)

<span data-ttu-id="3c0a1-139">Metadata.cs의 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-139">Replace the code in Metadata.cs with the following code.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample3.cs)]

<span data-ttu-id="3c0a1-140">이러한 메타 데이터 클래스에는 이전에 모델 클래스에 적용 하는 유효성 검사 특성의 모두 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-140">These metadata classes contain all of the validation attributes that you had previously applied to the model classes.</span></span> <span data-ttu-id="3c0a1-141">**디스플레이** 특성 텍스트 레이블에 사용 되는 값을 변경 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-141">The **Display** attribute is used to change the value used for text labels.</span></span>

<span data-ttu-id="3c0a1-142">이제 모델 클래스 메타 데이터 클래스와 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-142">Now, you must associate the model classes with the metadata classes.</span></span>

<span data-ttu-id="3c0a1-143">에 **모델** 폴더 라는 클래스를 추가 **PartialClasses.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-143">In the **Models** folder, add a class named **PartialClasses.cs**.</span></span>

<span data-ttu-id="3c0a1-144">파일의 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-144">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample4.cs)]

<span data-ttu-id="3c0a1-145">각 클래스로 표시 된 통지는 `partial` 클래스 및 각 일치로 자동으로 생성 된 클래스 이름 및 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-145">Notice that each class is marked as a `partial` class, and each matches the name and namespace as the class that is automatically generated.</span></span> <span data-ttu-id="3c0a1-146">메타 데이터 특성을 partial 클래스를 적용 하 여 데이터 유효성 검사 특성을 자동으로 생성 된 클래스에 적용 됩니다 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-146">By applying the metadata attribute to the partial class, you ensure that the data validation attributes will be applied to the automatically-generated class.</span></span> <span data-ttu-id="3c0a1-147">이러한 특성의 메타 데이터 특성이 다시 생성 되지 않습니다 partial 클래스에 적용 되기 때문에 모델 클래스를 다시 생성 하면 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-147">These attributes will not be lost when you regenerate the model classes because the metadata attribute is applied in partial classes that are not regenerated.</span></span>

<span data-ttu-id="3c0a1-148">자동으로 생성 된 클래스를 다시 생성 하려면 ContosoModel.edmx 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-148">To regenerate the automatically-generated classes, open the ContosoModel.edmx file.</span></span> <span data-ttu-id="3c0a1-149">다시 한 번 단추로 클릭 하 고 디자인 화면 및 선택 **데이터베이스에서 모델 업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-149">Once again, right-click on the design surface and select **Update Model from Database**.</span></span> <span data-ttu-id="3c0a1-150">데이터베이스를 변경 하지 않은 경우에이 프로세스는 클래스 다시 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-150">Even though you have not changed the database, this process will regenerate the classes.</span></span> <span data-ttu-id="3c0a1-151">에 **새로 고침** 탭에서 **테이블** 및 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-151">In the **Refresh** tab, select **Tables** and **Finish**.</span></span>

![테이블을 새로 고치려면](enhancing-data-validation/_static/image4.png)

<span data-ttu-id="3c0a1-153">변경 내용을 적용할 ContosoModel.edmx 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-153">Save the ContosoModel.edmx file to apply the changes.</span></span>

<span data-ttu-id="3c0a1-154">Student.cs 파일이 나 Enrollment.cs 파일을 열고 더 이상 이전에 적용 된 데이터 유효성 검사 특성 파일의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-154">Open the Student.cs file or the Enrollment.cs file, and notice that the data validation attributes you applied earlier are no longer in the file.</span></span> <span data-ttu-id="3c0a1-155">그러나 응용 프로그램을 실행 하 고 데이터를 입력할 때 유효성 검사 규칙 여전히 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c0a1-155">However, run the application, and notice that the validation rules are still applied when you enter data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3c0a1-156">[이전](customizing-a-view.md)
> [다음](publish-to-azure.md)</span><span class="sxs-lookup"><span data-stu-id="3c0a1-156">[Previous](customizing-a-view.md)
[Next](publish-to-azure.md)</span></span>
