---
uid: mvc/overview/getting-started/database-first-development/enhancing-data-validation
title: '자습서: ASP.NET MVC 앱을 사용 하 여 EF Database First에 대 한 데이터 유효성 검사 향상'
description: 이 자습서는 데이터 주석 유효성 검사 요구 사항을 지정 하 여 서식 지정을 표시 하는 데이터 모델에 추가 하는 방법에 중점을 둡니다.
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: 0ed5e67a-34c0-4b57-84a6-802b0fb3cd00
msc.legacyurl: /mvc/overview/getting-started/database-first-development/enhancing-data-validation
msc.type: authoredcontent
ms.openlocfilehash: 897cd7c6a40445e2a4abede50d81e101372d3233
ms.sourcegitcommit: ed76cc752966c604a795fbc56d5a71d16ded0b58
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/02/2019
ms.locfileid: "55667624"
---
# <a name="tutorial-enhance-data-validation-for-ef-database-first-with-aspnet-mvc-app"></a><span data-ttu-id="4c071-103">자습서: ASP.NET MVC 앱을 사용 하 여 EF Database First에 대 한 데이터 유효성 검사 향상</span><span class="sxs-lookup"><span data-stu-id="4c071-103">Tutorial: Enhance data validation for EF Database First with ASP.NET MVC app</span></span>

<span data-ttu-id="4c071-104">MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여, 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="4c071-105">이 자습서 시리즈에서는 자동으로 표시, 편집, 만들기, 사용자를 사용 하는 코드를 생성 하 고 데이터베이스 테이블에 있는 데이터를 삭제 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="4c071-106">생성된 된 코드는 데이터베이스 테이블의 열에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="4c071-107">이 자습서는 데이터 주석 유효성 검사 요구 사항을 지정 하 여 서식 지정을 표시 하는 데이터 모델에 추가 하는 방법에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-107">This tutorial focuses on adding data annotations to the data model to specify validation requirements and display formatting.</span></span> <span data-ttu-id="4c071-108">의견 섹션에는 사용자의 의견에로 기반 향상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-108">It was improved based on feedback from users in the comments section.</span></span>

<span data-ttu-id="4c071-109">이 자습서에서는 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-109">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4c071-110">데이터 주석 추가</span><span class="sxs-lookup"><span data-stu-id="4c071-110">Add data annotations</span></span>
> * <span data-ttu-id="4c071-111">메타 데이터 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-111">Add metadata classes</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4c071-112">전제 조건</span><span class="sxs-lookup"><span data-stu-id="4c071-112">Prerequisites</span></span>

* [<span data-ttu-id="4c071-113">보기를 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="4c071-113">Customize a view</span></span>](customizing-a-view.md)

## <a name="add-data-annotations"></a><span data-ttu-id="4c071-114">데이터 주석 추가</span><span class="sxs-lookup"><span data-stu-id="4c071-114">Add data annotations</span></span>

<span data-ttu-id="4c071-115">이전 항목에서 살펴본 것 처럼 일부 데이터 유효성 검사 규칙의 사용자 입력에 자동으로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-115">As you saw in an earlier topic, some data validation rules are automatically applied to the user input.</span></span> <span data-ttu-id="4c071-116">예를 들어, 등급 속성에 대해 번호를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-116">For example, you can only provide a number for the Grade property.</span></span> <span data-ttu-id="4c071-117">더 많은 데이터 유효성 검사 규칙을 지정 하려면 데이터 주석 모델 클래스에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-117">To specify more data validation rules, you can add data annotations to your model class.</span></span> <span data-ttu-id="4c071-118">이러한 주석은 지정된 된 속성에 대 한 웹 응용 프로그램 전체에서 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-118">These annotations are applied throughout your web application for the specified property.</span></span> <span data-ttu-id="4c071-119">속성을 표시 되는 방법을 변경 하는 서식 특성을 적용할 수도 있습니다. 와 같은 텍스트 레이블에 사용 되는 값을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-119">You can also apply formatting attributes that change how the properties are displayed; such as, changing the value used for text labels.</span></span>

<span data-ttu-id="4c071-120">이 자습서에서는 데이터 FirstName, LastName 및 MiddleName 속성에 대해 제공 된 값의 길이 제한 하는 주석을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-120">In this tutorial, you will add data annotations to restrict the length of the values provided for the FirstName, LastName, and MiddleName properties.</span></span> <span data-ttu-id="4c071-121">데이터베이스에서 이러한 값은 50 자로; 제한 그러나 웹 응용 프로그램에서 해당 문자 제한이 현재 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-121">In the database, these values are limited to 50 characters; however, in your web application that character limit is currently not enforced.</span></span> <span data-ttu-id="4c071-122">이러한 값 중 하나에 대 한 50 개 이상의 문자를 제공 하는 사용자, 페이지 값을 데이터베이스에 저장 하려고 할 때 작동이 중단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-122">If a user provides more than 50 characters for one of those values, the page will crash when attempting to save the value to the database.</span></span> <span data-ttu-id="4c071-123">또한 0에서 4 사이의 값으로 등급은 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-123">You will also restrict Grade to values between 0 and 4.</span></span>

<span data-ttu-id="4c071-124">선택 **모델** > **ContosoModel.edmx** > **ContosoModel.tt** 연 합니다 *Student.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-124">Select **Models** > **ContosoModel.edmx** > **ContosoModel.tt** and open the *Student.cs* file.</span></span> <span data-ttu-id="4c071-125">클래스에 다음 강조 표시 된 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-125">Add the following highlighted code to the class.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample1.cs?highlight=5,15,17,20)]

<span data-ttu-id="4c071-126">오픈 *Enrollment.cs* 다음 강조 표시 된 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-126">Open *Enrollment.cs* and add the following highlighted code.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample2.cs?highlight=5,10)]

<span data-ttu-id="4c071-127">솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-127">Build the solution.</span></span>

<span data-ttu-id="4c071-128">클릭 **학생의 목록을** 선택한 **편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-128">Click **List of students** and select **Edit**.</span></span> <span data-ttu-id="4c071-129">50 개 이상의 문자를 입력 하려고 하면 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-129">If you attempt to enter more than 50 characters, an error message is displayed.</span></span>

![오류 메시지를 표시 합니다.](enhancing-data-validation/_static/image1.png)

<span data-ttu-id="4c071-131">홈 페이지로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-131">Go back to the home page.</span></span> <span data-ttu-id="4c071-132">클릭 **등록 목록** 선택한 **편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-132">Click **List of enrollments** and select **Edit**.</span></span> <span data-ttu-id="4c071-133">위의 4 등급을 제공 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-133">Attempt to provide a grade above 4.</span></span> <span data-ttu-id="4c071-134">이 오류를 받게 됩니다. *필드 등급은 0에서 4 사이 여야 합니다.*</span><span class="sxs-lookup"><span data-stu-id="4c071-134">You will receive this error: *The field Grade must be between 0 and 4.*</span></span>

## <a name="add-metadata-classes"></a><span data-ttu-id="4c071-135">메타 데이터 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-135">Add metadata classes</span></span>

<span data-ttu-id="4c071-136">데이터베이스를 변경 하지 않는 경우에 작동 모델 클래스에 직접 유효성 검사 특성을 추가 합니다. 그러나 모델 클래스를 다시 생성 하 여 데이터베이스를 변경 하 고 필요한 경우 모델 클래스에 적용 한 특성을 모두 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-136">Adding the validation attributes directly to the model class works when you do not expect the database to change; however, if your database changes and you need to regenerate the model class, you will lose all of the attributes you had applied to the model class.</span></span> <span data-ttu-id="4c071-137">이 방법은 매우 비효율적이 고 중요 한 유효성 검사 규칙이 손실 발생 하기 쉬운 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-137">This approach can be very inefficient and prone to losing important validation rules.</span></span>

<span data-ttu-id="4c071-138">이 문제를 방지 하려면 특성을 포함 하는 메타 데이터 클래스를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-138">To avoid this problem, you can add a metadata class that contains the attributes.</span></span> <span data-ttu-id="4c071-139">메타 데이터 클래스 모델 클래스를 연결 하면 해당 특성은 모델에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-139">When you associate the model class to the metadata class, those attributes are applied to the model.</span></span> <span data-ttu-id="4c071-140">이 방법에서는 모델 클래스의 모든 메타 데이터 클래스에 적용 된 특성을 손실 하지 않고 다시 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-140">In this approach, the model class can be regenerated without losing all of the attributes that have been applied to the metadata class.</span></span>

<span data-ttu-id="4c071-141">에 **모델** 폴더를 라는 클래스를 추가 *Metadata.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-141">In the **Models** folder, add a class named *Metadata.cs*.</span></span>

<span data-ttu-id="4c071-142">코드를 바꿔 *Metadata.cs* 다음 코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-142">Replace the code in *Metadata.cs* with the following code.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample3.cs)]

<span data-ttu-id="4c071-143">이러한 메타 데이터 클래스에는 모든 모델 클래스를 이전에 적용 하는 유효성 검사 특성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-143">These metadata classes contain all of the validation attributes that you had previously applied to the model classes.</span></span> <span data-ttu-id="4c071-144">합니다 **표시** 특성 텍스트 레이블에 사용 되는 값을 변경 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-144">The **Display** attribute is used to change the value used for text labels.</span></span>

<span data-ttu-id="4c071-145">이제 메타 데이터 클래스를 사용 하 여 모델 클래스를 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-145">Now, you must associate the model classes with the metadata classes.</span></span>

<span data-ttu-id="4c071-146">에 **모델** 폴더를 라는 클래스를 추가 *PartialClasses.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-146">In the **Models** folder, add a class named *PartialClasses.cs*.</span></span>

<span data-ttu-id="4c071-147">파일의 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-147">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample4.cs)]

<span data-ttu-id="4c071-148">각 클래스에으로 표시 되는 `partial` 클래스 및 각 자동으로 생성 된 클래스 이름 및 네임 스페이스를 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-148">Notice that each class is marked as a `partial` class, and each matches the name and namespace as the class that is automatically generated.</span></span> <span data-ttu-id="4c071-149">Partial 클래스에는 메타 데이터 특성을 적용 하 여 데이터 유효성 검사 특성을 자동으로 생성 된 클래스에 적용할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-149">By applying the metadata attribute to the partial class, you ensure that the data validation attributes will be applied to the automatically-generated class.</span></span> <span data-ttu-id="4c071-150">이러한 특성 메타 데이터 특성을 다시 생성 되지 않습니다는 partial 클래스에서 적용 되기 때문에 모델 클래스를 다시 생성 하면 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-150">These attributes will not be lost when you regenerate the model classes because the metadata attribute is applied in partial classes that are not regenerated.</span></span>

<span data-ttu-id="4c071-151">자동으로 생성 된 클래스를 다시 생성 하려면 엽니다는 *ContosoModel.edmx* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-151">To regenerate the automatically-generated classes, open the *ContosoModel.edmx* file.</span></span> <span data-ttu-id="4c071-152">이번에 디자인 화면에서 마우스 오른쪽 단추로 클릭 **데이터베이스에서 모델 업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-152">Once again, right-click on the design surface and select **Update Model from Database**.</span></span> <span data-ttu-id="4c071-153">데이터베이스를 변경 하지 않은 경우에이 프로세스는 클래스를 다시 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-153">Even though you have not changed the database, this process will regenerate the classes.</span></span> <span data-ttu-id="4c071-154">에 **새로 고침** 탭을 선택 **테이블** 하 고 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-154">In the **Refresh** tab, select **Tables** and **Finish**.</span></span>

<span data-ttu-id="4c071-155">저장 된 *ContosoModel.edmx* 파일 변경 내용을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-155">Save the *ContosoModel.edmx* file to apply the changes.</span></span>

<span data-ttu-id="4c071-156">열기는 *Student.cs* 파일 또는 *Enrollment.cs* 파일 및 이전에 적용 된 데이터 유효성 검사 특성은 파일에 더 이상입니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-156">Open the *Student.cs* file or the *Enrollment.cs* file, and notice that the data validation attributes you applied earlier are no longer in the file.</span></span> <span data-ttu-id="4c071-157">그러나 응용 프로그램을 실행 하 고 데이터를 입력할 때 유효성 검사 규칙이 계속 적용 됩니다 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-157">However, run the application, and notice that the validation rules are still applied when you enter data.</span></span>

## <a name="conclusion"></a><span data-ttu-id="4c071-158">결론</span><span class="sxs-lookup"><span data-stu-id="4c071-158">Conclusion</span></span>

<span data-ttu-id="4c071-159">이 시리즈 사용자가 편집, 업데이트, 만들기 및 데이터를 삭제할 수 있는 기존 데이터베이스에서 코드를 생성 하는 방법의 간단한 예제를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-159">This series provided a simple example of how to generate code from an existing database that enables users to edit, update, create and delete data.</span></span> <span data-ttu-id="4c071-160">ASP.NET MVC 5, Entity Framework 및 ASP.NET 스 캐 폴딩 프로젝트를 만들려면 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-160">It used ASP.NET MVC 5, Entity Framework and ASP.NET Scaffolding to create the project.</span></span> 

<span data-ttu-id="4c071-161">Code First 개발을 소개 하는 예제를 보려면 [ASP.NET MVC 5 시작](../introduction/getting-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-161">For an introductory example of Code First development, see [Getting Started with ASP.NET MVC 5](../introduction/getting-started.md).</span></span> 

<span data-ttu-id="4c071-162">고급 예제를 보려면 [ASP.NET MVC 4 응용 프로그램에 대 한 Entity Framework 데이터 모델을 만드는](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-162">For a more advanced example, see [Creating an Entity Framework Data Model for an ASP.NET MVC 4 App](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="4c071-163">Database First에서 데이터로 작업에 사용 하는 DbContext API는 동일 Code First에서 데이터로 작업 하기 위한 사용 API로 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-163">Note that the DbContext API that you use for working with data in Database First is the same as the API you use for working with data in Code First.</span></span> <span data-ttu-id="4c071-164">Database First 사용 하려는 경우에 코드 첫 번째 자습서 등에서 동시성 충돌 처리 관련된 데이터 읽기 및 업데이트와 같은 더 복잡 한 시나리오를 처리 하는 방법을 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-164">Even if you intend to use Database First, you can learn how to handle more complex scenarios such as reading and updating related data, handling concurrency conflicts, and so forth from a Code First tutorial.</span></span> <span data-ttu-id="4c071-165">유일한 차이점은 데이터베이스, 상황에 맞는 클래스 및 엔터티 클래스를 생성 하는 방법</span><span class="sxs-lookup"><span data-stu-id="4c071-165">The only difference is in how the database, context class, and entity classes are created.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4c071-166">추가 자료</span><span class="sxs-lookup"><span data-stu-id="4c071-166">Additional resources</span></span>

<span data-ttu-id="4c071-167">속성 및 클래스에 적용할 수는 데이터 유효성 검사 주석의 전체 목록을 참조 하세요 [System.ComponentModel.DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-167">For a full list of data validation annotations you can apply to properties and classes, see [System.ComponentModel.DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c071-168">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4c071-168">Next steps</span></span>

<span data-ttu-id="4c071-169">이 자습서에서는 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="4c071-169">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4c071-170">추가 데이터 주석</span><span class="sxs-lookup"><span data-stu-id="4c071-170">Added data annotations</span></span>
> * <span data-ttu-id="4c071-171">추가 메타 데이터 클래스</span><span class="sxs-lookup"><span data-stu-id="4c071-171">Added metadata classes</span></span>

<span data-ttu-id="4c071-172">Azure App Service 웹 앱 및 SQL database를 배포 하는 방법에 알아보려면이 자습서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="4c071-172">To learn how to deploy a web app and SQL database to Azure App Service, see this tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="4c071-173">Azure App Service에.NET 앱 배포</span><span class="sxs-lookup"><span data-stu-id="4c071-173">Deploy a .NET app to Azure App Service</span></span>](/azure/app-service/app-service-web-tutorial-dotnet-sqldatabase/)
