---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-validation-to-the-model
title: "유효성 검사 (C#) 모델에 추가 | Microsoft Docs"
author: Rick-Anderson
description: "컨트롤러 만들기"
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2011
ms.topic: article
ms.assetid: 9af927e2-1c3b-43d9-917d-1df75be3c482
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-validation-to-the-model
msc.type: authoredcontent
ms.openlocfilehash: 1e1235972d1e16153faee113af09edaa676d70d8
ms.sourcegitcommit: 016f4d58663bcd442930227022de23fb3abee0b3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/12/2018
---
<a name="adding-validation-to-the-model-c"></a><span data-ttu-id="9ff34-103">모델 (C#)에 유효성 검사 추가</span><span class="sxs-lookup"><span data-stu-id="9ff34-103">Adding Validation to the Model (C#)</span></span>
====================
<span data-ttu-id="9ff34-104">으로 [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="9ff34-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> > [!NOTE]
> > <span data-ttu-id="9ff34-105">이 자습서의 업데이트 된 버전은 사용할 수 있는 [여기](../../../getting-started/introduction/getting-started.md) ASP.NET MVC 5 및 Visual Studio 2013을 사용 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-105">An updated version of this tutorial is available [here](../../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="9ff34-106">더 안전 하 고 따라 하기 쉽고 이며 더 많은 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-106">It's more secure, much simpler to follow and demonstrates more features.</span></span>
> 
> 
> <span data-ttu-id="9ff34-107">이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 즉 Microsoft Visual Studio의 무료 버전을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 구축 하는 기초 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-107">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="9ff34-108">시작 하기 전에 아래에 나열 된 필수 구성 요소가 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-108">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="9ff34-109">다음 링크를 클릭 하 여 모두를 설치할 수 있습니다: [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-109">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="9ff34-110">또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-110">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="9ff34-111">Visual Studio Web Developer Express SP1 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="9ff34-111">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="9ff34-112">ASP.NET MVC 3 도구 업데이트</span><span class="sxs-lookup"><span data-stu-id="9ff34-112">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="9ff34-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)</span><span class="sxs-lookup"><span data-stu-id="9ff34-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="9ff34-114">Visual Studio 2010 Visual Web Developer 2010 대신를 사용 하는 경우 다음 링크를 클릭 하 여 필수 구성 요소 설치: [Visual Studio 2010 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-114">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="9ff34-115">이 항목에 수반 C# 소스 코드를 사용 하 여 Visual Web Developer 프로젝트 ´ ù.</span><span class="sxs-lookup"><span data-stu-id="9ff34-115">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="9ff34-116">[C# 버전을 다운로드](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-116">[Download the C# version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="9ff34-117">Visual Basic을 선호 하는 경우 전환의 [Visual Basic 버전](../vb/intro-to-aspnet-mvc-3.md) 이 자습서의 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-117">If you prefer Visual Basic, switch to the [Visual Basic version](../vb/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>


<span data-ttu-id="9ff34-118">이 섹션에서는 유효성 검사 논리를 추가 합니다는 `Movie` 모델과 하면 사용자가 만들거나 응용 프로그램을 사용 하 여 동영상을 편집 하는 언제 든 지 유효성 검사 규칙이 적용 되도록 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-118">In this section you'll add validation logic to the `Movie` model, and you'll ensure that the validation rules are enforced any time a user attempts to create or edit a movie using the application.</span></span>

## <a name="keeping-things-dry"></a><span data-ttu-id="9ff34-119">건조 구성을</span><span class="sxs-lookup"><span data-stu-id="9ff34-119">Keeping Things DRY</span></span>

<span data-ttu-id="9ff34-120">ASP.NET MVC의 핵심 디자인 개념 중 하나 드라이 ("하지 않는 반복 직접")입니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-120">One of the core design tenets of ASP.NET MVC is DRY ("Don't Repeat Yourself").</span></span> <span data-ttu-id="9ff34-121">ASP.NET MVC 기능 또는 동작을 한 번만 지정 한 다음 응용 프로그램에 everywhere 반영 하는 것이 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-121">ASP.NET MVC encourages you to specify functionality or behavior only once, and then have it be reflected everywhere in an application.</span></span> <span data-ttu-id="9ff34-122">이를 작성 해야 하는 코드의 양을 줄이고 유지 하기 위해 훨씬 쉽게 작성 하는 코드를 만들기.</span><span class="sxs-lookup"><span data-stu-id="9ff34-122">This reduces the amount of code you need to write and makes the code you do write much easier to maintain.</span></span>

<span data-ttu-id="9ff34-123">ASP.NET MVC 및 Entity Framework Code First 제공 하는 유효성 검사 지원은 동작의 건조 원칙의 좋은 예입니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-123">The validation support provided by ASP.NET MVC and Entity Framework Code First is a great example of the DRY principle in action.</span></span> <span data-ttu-id="9ff34-124">(모델 클래스)의 한 지점에서 유효성 검사 규칙을 선언적으로 지정할 수 있습니다 및 다음 해당 규칙이 응용 프로그램의 모든 위치에서 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-124">You can declaratively specify validation rules in one place (in the model class) and then those rules are enforced everywhere in the application.</span></span>

<span data-ttu-id="9ff34-125">있습니다 사용할 수 있는 방법을이 유효성 검사 지원의 영화 응용 프로그램에서 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-125">Let's look at how you can take advantage of this validation support in the movie application.</span></span>

## <a name="adding-validation-rules-to-the-movie-model"></a><span data-ttu-id="9ff34-126">영화 모델에 유효성 검사 규칙 추가</span><span class="sxs-lookup"><span data-stu-id="9ff34-126">Adding Validation Rules to the Movie Model</span></span>

<span data-ttu-id="9ff34-127">일부 유효성 검사 논리를 추가 하 여 먼저는 `Movie` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-127">You'll begin by adding some validation logic to the `Movie` class.</span></span>

<span data-ttu-id="9ff34-128">*Movie.cs* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-128">Open the *Movie.cs* file.</span></span> <span data-ttu-id="9ff34-129">추가 `using` 문을 참조 하는 파일 맨 위에 있는 [ `System.ComponentModel.DataAnnotations` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) 네임 스페이스:</span><span class="sxs-lookup"><span data-stu-id="9ff34-129">Add a `using` statement at the top of the file that references the [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace:</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample1.cs)]

<span data-ttu-id="9ff34-130">네임 스페이스에는.NET Framework의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-130">The namespace is part of the .NET Framework.</span></span> <span data-ttu-id="9ff34-131">모든 클래스 또는 속성에 선언적으로 적용할 수 있는 유효성 검사 특성의 기본 제공 된 집합을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-131">It provides a built-in set of validation attributes that you can apply declaratively to any class or property.</span></span>

<span data-ttu-id="9ff34-132">이제 업데이트 된 `Movie` 클래스는 기본 제공 기능을 활용 하려면 [ `Required` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx), [ `StringLength` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx), 및 [ `Range` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) 유효성 검사 특성 .</span><span class="sxs-lookup"><span data-stu-id="9ff34-132">Now update the `Movie` class to take advantage of the built-in [`Required`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx), [`StringLength`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx), and [`Range`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) validation attributes.</span></span> <span data-ttu-id="9ff34-133">특성을 적용 대상의 예를 들어 다음 코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-133">Use the following code as an example of where to apply the attributes.</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample2.cs)]

<span data-ttu-id="9ff34-134">이 유효성 검사 특성은 적용되는 모델 속성에 시행하려는 동작을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-134">The validation attributes specify behavior that you want to enforce on the model properties they are applied to.</span></span> <span data-ttu-id="9ff34-135">`Required` 특성 나타냅니다 속성 값을 가져야 합니다;이 샘플에서는 동영상은에 대 한 값은 `Title`, `ReleaseDate`, `Genre`, 및 `Price` 유효 하려면 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-135">The `Required` attribute indicates that a property must have a value; in this sample, a movie has to have values for the `Title`, `ReleaseDate`, `Genre`, and `Price` properties in order to be valid.</span></span> <span data-ttu-id="9ff34-136">`Range` 특성은 지정된 범위 내의 값을 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-136">The `Range` attribute constrains a value to within a specified range.</span></span> <span data-ttu-id="9ff34-137">`StringLength` 특성을 사용하면 문자열 속성의 최대 길이와, 필요에 따라 최소 길이를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-137">The `StringLength` attribute lets you set the maximum length of a string property, and optionally its minimum length.</span></span>

<span data-ttu-id="9ff34-138">코드는 먼저 응용 프로그램 데이터베이스에 변경 내용을 저장 하기 전에 모델 클래스에서 지정 된 유효성 검사 규칙 적용 되도록 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-138">Code First ensures that the validation rules you specify on a model class are enforced before the application saves changes in the database.</span></span> <span data-ttu-id="9ff34-139">예를 들어 아래 코드는 예외를 throw 할 때는 `SaveChanges` 메서드는, 여러 필요 하기 때문에 `Movie` 속성 값이 누락 되 고 가격 기본값은 0 (이 범위를 벗어났습니다).</span><span class="sxs-lookup"><span data-stu-id="9ff34-139">For example, the code below will throw an exception when the `SaveChanges` method is called, because several required `Movie` property values are missing and the price is zero (which is out of the valid range).</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample3.cs)]

<span data-ttu-id="9ff34-140">.NET Framework에 의해 자동으로 적용 하는 유효성 검사 규칙을 만드는 것 사용 하면 확인 응용 프로그램 보다 강력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-140">Having validation rules automatically enforced by the .NET Framework helps make your application more robust.</span></span> <span data-ttu-id="9ff34-141">또한 유효성 검사를 잊거나, 데이터베이스에 불량 데이터가 실수로 들어가지 않게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-141">It also ensures that you can't forget to validate something and inadvertently let bad data into the database.</span></span>

<span data-ttu-id="9ff34-142">다음은 업데이트 된 항목에 대 한 전체 코드 *Movie.cs* 파일:</span><span class="sxs-lookup"><span data-stu-id="9ff34-142">Here's a complete code listing for the updated *Movie.cs* file:</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample4.cs)]

## <a name="validation-error-ui-in-aspnet-mvc"></a><span data-ttu-id="9ff34-143">ASP.NET MVC에서 UI 유효성 검사 오류</span><span class="sxs-lookup"><span data-stu-id="9ff34-143">Validation Error UI in ASP.NET MVC</span></span>

<span data-ttu-id="9ff34-144">응용 프로그램을 다시 실행을 탐색 하 고 */Movies* URL입니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-144">Re-run the application and navigate to the */Movies* URL.</span></span>

<span data-ttu-id="9ff34-145">클릭는 **만들 영화** 새 동영상을 추가 하는 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-145">Click the **Create Movie** link to add a new movie.</span></span> <span data-ttu-id="9ff34-146">일부 잘못 된 값으로 양식을 작성 한 다음 클릭는 **만들기** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-146">Fill out the form with some invalid values and then click the **Create** button.</span></span>

<span data-ttu-id="9ff34-147">[![8_validationErrors](adding-validation-to-the-model/_static/image2.png)](adding-validation-to-the-model/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="9ff34-147">[![8_validationErrors](adding-validation-to-the-model/_static/image2.png)](adding-validation-to-the-model/_static/image1.png)</span></span>

<span data-ttu-id="9ff34-148">어떻게 폼이 자동으로를 사용 하는 배경색 각 옆에 있는 적절 한 유효성 검사 오류 메시지가 방사 및 잘못 된 데이터를 포함 하는 텍스트 상자에 강조 표시를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-148">Notice how the form has automatically used a background color to highlight the text boxes that contain invalid data and has emitted an appropriate validation error message next to each one.</span></span> <span data-ttu-id="9ff34-149">주석이 지정 하면 지정 된 오류 문자열은 일치 하는 오류 메시지는 `Movie` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-149">The error messages match the error strings you specified when you annotated the `Movie` class.</span></span> <span data-ttu-id="9ff34-150">오류 (경우에 사용자가 JavaScript를 사용 하지 않도록 설정) (JavaScript 사용) 하는 클라이언트 쪽 및 서버측 모두 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-150">The errors are enforced both client-side (using JavaScript) and server-side (in case a user has JavaScript disabled).</span></span>

<span data-ttu-id="9ff34-151">실제 혜택은 한 줄의 코드를 변경 해야 하지 않은 `MoviesController` 클래스 또는 *Create.cshtml* UI이 유효성이 검사를 사용 하도록 설정 하려면 보기.</span><span class="sxs-lookup"><span data-stu-id="9ff34-151">A real benefit is that you didn't need to change a single line of code in the `MoviesController` class or in the *Create.cshtml* view in order to enable this validation UI.</span></span> <span data-ttu-id="9ff34-152">컨트롤러 및 자동으로이 자습서의 앞부분에서 만든 보기에서 특성을 사용 하 여 지정 된 유효성 검사 규칙을 받아서는 `Movie` 모델 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-152">The controller and views you created earlier in this tutorial automatically picked up the validation rules that you specified using attributes on the `Movie` model class.</span></span>

## <a name="how-validation-occurs-in-the-create-view-and-create-action-method"></a><span data-ttu-id="9ff34-153">만들기 확인 하 고 작업 메서드를 작성할 유효성 검사에서 발생 하는 방법</span><span class="sxs-lookup"><span data-stu-id="9ff34-153">How Validation Occurs in the Create View and Create Action Method</span></span>

<span data-ttu-id="9ff34-154">컨트롤러나 보기에서 코드에 대한 업데이트 없이 어떻게 유효성 검사 UI가 생성되는지 궁금할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-154">You might wonder how the validation UI was generated without any updates to the code in the controller or views.</span></span> <span data-ttu-id="9ff34-155">다음 목록에서는 `Create` 의 메서드는 `MovieController` 클래스 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-155">The next listing shows what the `Create` methods in the `MovieController` class look like.</span></span> <span data-ttu-id="9ff34-156">만든 방법으로이 자습서의 앞부분에 나오는 것에서 변경 하기가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-156">They're unchanged from how you created them earlier in this tutorial.</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample5.cs)]

<span data-ttu-id="9ff34-157">첫 번째 작업 메서드 초기 만들기 폼이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-157">The first action method displays the initial Create form.</span></span> <span data-ttu-id="9ff34-158">두 번째 폼 post를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-158">The second handles the form post.</span></span> <span data-ttu-id="9ff34-159">두 번째 `Create` 메서드 호출 `ModelState.IsValid` 동영상에 모든 유효성 검사 오류가 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-159">The second `Create` method calls `ModelState.IsValid` to check whether the movie has any validation errors.</span></span> <span data-ttu-id="9ff34-160">이 메서드 호출에서는 개체에 적용된 모든 유효성 검사 특성을 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-160">Calling this method evaluates any validation attributes that have been applied to the object.</span></span> <span data-ttu-id="9ff34-161">개체 유효성 검사 오류가 있으면는 `Create` 메서드 다시 표시 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-161">If the object has validation errors, the `Create` method redisplays the form.</span></span> <span data-ttu-id="9ff34-162">오류가 없으면 메서드가 데이터베이스에 새 동영상을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-162">If there are no errors, the method saves the new movie in the database.</span></span>

<span data-ttu-id="9ff34-163">다음은 이러한는 *Create.cshtml* 자습서의 앞부분에 나오는 스 캐 폴드 된 템플릿 보기.</span><span class="sxs-lookup"><span data-stu-id="9ff34-163">Below is the *Create.cshtml* view template that you scaffolded earlier in the tutorial.</span></span> <span data-ttu-id="9ff34-164">이 항목은 위 두 작업 메서드에서 최초 양식을 표시하고 오류 시 다시 표시하기 위해 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-164">It's used by the action methods shown above both to display the initial form and to redisplay it in the event of an error.</span></span>

[!code-cshtml[Main](adding-validation-to-the-model/samples/sample6.cshtml)]

<span data-ttu-id="9ff34-165">코드 사용 하는 여는 `Html.EditorFor` 출력 하는 도우미는 `<input>` 요소 각각에 대해 `Movie` 속성.</span><span class="sxs-lookup"><span data-stu-id="9ff34-165">Notice how the code uses an `Html.EditorFor` helper to output the `<input>` element for each `Movie` property.</span></span> <span data-ttu-id="9ff34-166">이 도우미 옆에 대 한 호출 되는 `Html.ValidationMessageFor` 도우미 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-166">Next to this helper is a call to the `Html.ValidationMessageFor` helper method.</span></span> <span data-ttu-id="9ff34-167">이러한 두 개의 도우미 메서드를 보기에는 컨트롤러에 의해 전달 되는 모델 개체 사용 (이 경우는 `Movie` 개체).</span><span class="sxs-lookup"><span data-stu-id="9ff34-167">These two helper methods work with the model object that's passed by the controller to the view (in this case, a `Movie` object).</span></span> <span data-ttu-id="9ff34-168">적절 하 게 모델 및 표시 오류 메시지에 지정 된 유효성 검사 특성에 대 한 자동으로 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-168">They automatically look for validation attributes specified on the model and display error messages as appropriate.</span></span>

<span data-ttu-id="9ff34-169">이 방법에 대 한 훌륭한은 컨트롤러도 아니고 만들기 보기 템플릿이 알고 있는 아무 것도 표시 되는 특정 오류 메시지 또는 적용을 실제 유효성 검사 규칙에 대 한입니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-169">What's really nice about this approach is that neither the controller nor the Create view template knows anything about the actual validation rules being enforced or about the specific error messages displayed.</span></span> <span data-ttu-id="9ff34-170">유효성 검사 규칙 및 오류 문자열은 `Movie` 클래스에서만 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-170">The validation rules and the error strings are specified only in the `Movie` class.</span></span>

<span data-ttu-id="9ff34-171">유효성 검사 논리를 나중에 변경 하려는 경우 정확 하 게 한 곳에서 그렇게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-171">If you want to change the validation logic later, you can do so in exactly one place.</span></span> <span data-ttu-id="9ff34-172">모든 유효성 검사 논리가 한 곳에 정의되어 모든 곳에서 사용되므로 응용 프로그램의 서로 다른 부분이 규칙 적용 방법에 부합하는지 우려하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-172">You won't have to worry about different parts of the application being inconsistent with how the rules are enforced — all validation logic will be defined in one place and used everywhere.</span></span> <span data-ttu-id="9ff34-173">이렇게 하면 코드가 매우 깔끔해지고 유지 관리 및 확장이 간편합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-173">This keeps the code very clean, and makes it easy to maintain and evolve.</span></span> <span data-ttu-id="9ff34-174">또한 반복 금지 원칙에 완전히 부합하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-174">And it means that you'll be fully honoring the DRY principle.</span></span>

## <a name="adding-formatting-to-the-movie-model"></a><span data-ttu-id="9ff34-175">영화 모델에 서식 추가</span><span class="sxs-lookup"><span data-stu-id="9ff34-175">Adding Formatting to the Movie Model</span></span>

<span data-ttu-id="9ff34-176">*Movie.cs* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-176">Open the *Movie.cs* file.</span></span> <span data-ttu-id="9ff34-177">[ `System.ComponentModel.DataAnnotations` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) 네임 스페이스는 기본 제공 유효성 검사 특성 집합 외에 서식 특성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-177">The [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace provides formatting attributes in addition to the built-in set of validation attributes.</span></span> <span data-ttu-id="9ff34-178">적용 하는 [ `DisplayFormat` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) 특성 및 [ `DataType` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 출시 날짜에 시작 및 끝 price 필드 열거형 값입니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-178">You'll apply the [`DisplayFormat`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) attribute and a [`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) enumeration value to the release date and to the price fields.</span></span> <span data-ttu-id="9ff34-179">다음 코드는 `ReleaseDate` 및 `Price` 는 적절 한 속성 [ `DisplayFormat` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-179">The following code shows the `ReleaseDate` and `Price` properties with the appropriate [`DisplayFormat`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) attribute.</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample7.cs)]

<span data-ttu-id="9ff34-180">명시적으로 설정 수 또는 [ `DataFormatString` ](https://msdn.microsoft.com/library/system.string.format.aspx) 값입니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-180">Alternatively, you could explicitly set a [`DataFormatString`](https://msdn.microsoft.com/library/system.string.format.aspx) value.</span></span> <span data-ttu-id="9ff34-181">다음 코드와 날짜 형식 문자열을 사용 하 여 릴리스 날짜 속성 (즉, "d").</span><span class="sxs-lookup"><span data-stu-id="9ff34-181">The following code shows the release date property with a date format string (namely, "d").</span></span> <span data-ttu-id="9ff34-182">않으려면 시간 릴리스 날짜의 일환으로 지정 하려면이 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-182">You'd use this to specify that you don't want to time as part of the release date.</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample8.cs)]

<span data-ttu-id="9ff34-183">다음 코드 형식에서 `Price` 통화로 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-183">The following code formats the `Price` property as currency.</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample9.cs)]

<span data-ttu-id="9ff34-184">전체 `Movie` 클래스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-184">The complete `Movie` class is shown below.</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample10.cs)]

<span data-ttu-id="9ff34-185">응용 프로그램을 실행 하 고를 찾습니다는 `Movies` 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-185">Run the application and browse to the `Movies` controller.</span></span>

![8_format_SM](adding-validation-to-the-model/_static/image3.png)

<span data-ttu-id="9ff34-187">이 시리즈의 다음 부분에서는 응용 프로그램을 검토하고 자동 생성된 `Details` 및 `Delete` 메서드를 몇 가지 개선합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff34-187">In the next part of the series, we'll review the application and make some improvements to the automatically generated `Details` and `Delete` methods.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="9ff34-188">[이전](adding-a-new-field.md)
[다음](improving-the-details-and-delete-methods.md)</span><span class="sxs-lookup"><span data-stu-id="9ff34-188">[Previous](adding-a-new-field.md)
[Next](improving-the-details-and-delete-methods.md)</span></span>
