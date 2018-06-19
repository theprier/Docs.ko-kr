---
uid: mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-vb
title: IDataErrorInfo 인터페이스 (VB)으로 유효성 검사 | Microsoft Docs
author: StephenWalther
description: Stephen Walther IDataErrorInfo 인터페이스 모델 클래스에서 구현 하 여 사용자 지정 유효성 검사 오류 메시지를 표시 하는 방법을 보여 줍니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/02/2009
ms.topic: article
ms.assetid: 3a8a9d9f-82dd-4959-b7c6-960e9ce95df1
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-vb
msc.type: authoredcontent
ms.openlocfilehash: 60df0f934432484e0c97e0caef25c15605beb14f
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30870091"
---
<a name="validating-with-the-idataerrorinfo-interface-vb"></a><span data-ttu-id="7aa99-103">IDataErrorInfo 인터페이스 (VB)으로 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="7aa99-103">Validating with the IDataErrorInfo Interface (VB)</span></span>
====================
<span data-ttu-id="7aa99-104">으로 [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="7aa99-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="7aa99-105">Stephen Walther IDataErrorInfo 인터페이스 모델 클래스에서 구현 하 여 사용자 지정 유효성 검사 오류 메시지를 표시 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-105">Stephen Walther shows you how to display custom validation error messages by implementing the IDataErrorInfo interface in a model class.</span></span>


<span data-ttu-id="7aa99-106">이 자습서의 목표는 ASP.NET MVC 응용 프로그램에서 유효성 검사를 수행 하는 한 가지 방법을 설명 하는입니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-106">The goal of this tutorial is to explain one approach to performing validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="7aa99-107">다른 사용자가 필수 양식 필드에 대 한 값을 제공 하지 않는 HTML 폼을 제출 하지 못하도록 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-107">You learn how to prevent someone from submitting an HTML form without providing values for required form fields.</span></span> <span data-ttu-id="7aa99-108">이 자습서에서는 IErrorDataInfo 인터페이스를 사용 하 여 유효성 검사를 수행 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-108">In this tutorial, you learn how to perform validation by using the IErrorDataInfo interface.</span></span>

## <a name="assumptions"></a><span data-ttu-id="7aa99-109">Assumptions</span><span class="sxs-lookup"><span data-stu-id="7aa99-109">Assumptions</span></span>

<span data-ttu-id="7aa99-110">이 자습서에서는 MoviesDB 데이터베이스 및 동영상 데이터베이스 테이블 사용 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-110">In this tutorial, I'll use the MoviesDB database and the Movies database table.</span></span> <span data-ttu-id="7aa99-111">이 테이블에는 다음과 같은 열에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-111">This table has the following columns:</span></span>

<a id="0.6_table01"></a>


| <span data-ttu-id="7aa99-112">**열 이름**</span><span class="sxs-lookup"><span data-stu-id="7aa99-112">**Column Name**</span></span> | <span data-ttu-id="7aa99-113">**데이터 형식**</span><span class="sxs-lookup"><span data-stu-id="7aa99-113">**Data Type**</span></span> | <span data-ttu-id="7aa99-114">**Null 허용**</span><span class="sxs-lookup"><span data-stu-id="7aa99-114">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7aa99-115">ID</span><span class="sxs-lookup"><span data-stu-id="7aa99-115">Id</span></span> | <span data-ttu-id="7aa99-116">Int</span><span class="sxs-lookup"><span data-stu-id="7aa99-116">Int</span></span> | <span data-ttu-id="7aa99-117">False</span><span class="sxs-lookup"><span data-stu-id="7aa99-117">False</span></span> |
| <span data-ttu-id="7aa99-118">제목</span><span class="sxs-lookup"><span data-stu-id="7aa99-118">Title</span></span> | <span data-ttu-id="7aa99-119">Nvarchar(100)</span><span class="sxs-lookup"><span data-stu-id="7aa99-119">Nvarchar(100)</span></span> | <span data-ttu-id="7aa99-120">False</span><span class="sxs-lookup"><span data-stu-id="7aa99-120">False</span></span> |
| <span data-ttu-id="7aa99-121">감독</span><span class="sxs-lookup"><span data-stu-id="7aa99-121">Director</span></span> | <span data-ttu-id="7aa99-122">Nvarchar(100)</span><span class="sxs-lookup"><span data-stu-id="7aa99-122">Nvarchar(100)</span></span> | <span data-ttu-id="7aa99-123">False</span><span class="sxs-lookup"><span data-stu-id="7aa99-123">False</span></span> |
| <span data-ttu-id="7aa99-124">DateReleased</span><span class="sxs-lookup"><span data-stu-id="7aa99-124">DateReleased</span></span> | <span data-ttu-id="7aa99-125">DateTime</span><span class="sxs-lookup"><span data-stu-id="7aa99-125">DateTime</span></span> | <span data-ttu-id="7aa99-126">False</span><span class="sxs-lookup"><span data-stu-id="7aa99-126">False</span></span> |


<span data-ttu-id="7aa99-127">이 자습서에서는 Microsoft Entity Framework를 사용 합니까 내 데이터베이스 모델 클래스를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-127">In this tutorial, I use the Microsoft Entity Framework to generate my database model classes.</span></span> <span data-ttu-id="7aa99-128">Entity Framework에서 생성 되는 동영상 클래스는 그림 1에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-128">The Movie class generated by the Entity Framework is displayed in Figure 1.</span></span>


<span data-ttu-id="7aa99-129">[![영화 엔터티](validating-with-the-idataerrorinfo-interface-vb/_static/image1.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7aa99-129">[![The Movie entity](validating-with-the-idataerrorinfo-interface-vb/_static/image1.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image1.png)</span></span>

<span data-ttu-id="7aa99-130">**그림 01**: The 영화 엔터티 ([전체 크기 이미지를 보려면 클릭](validating-with-the-idataerrorinfo-interface-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="7aa99-130">**Figure 01**: The Movie entity([Click to view full-size image](validating-with-the-idataerrorinfo-interface-vb/_static/image2.png))</span></span>


> [!NOTE] 
> 
> <span data-ttu-id="7aa99-131">데이터베이스 모델 클래스를 생성 하려면 Entity Framework를 사용 하는 방법에 대 한 자세한 내용은 참조 내 자습서 Entity Framework를 사용 하 여 모델 클래스 만들기.</span><span class="sxs-lookup"><span data-stu-id="7aa99-131">To learn more about using the Entity Framework to generate your database model classes, see my tutorial entitled Creating Model Classes with the Entity Framework.</span></span>


## <a name="the-controller-class"></a><span data-ttu-id="7aa99-132">컨트롤러 클래스</span><span class="sxs-lookup"><span data-stu-id="7aa99-132">The Controller Class</span></span>

<span data-ttu-id="7aa99-133">목록 영화 Home 컨트롤러를 사용 하 여 하 고 새 동영상을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-133">We use the Home controller to list movies and create new movies.</span></span> <span data-ttu-id="7aa99-134">이 클래스에 대 한 코드 목록 1에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-134">The code for this class is contained in Listing 1.</span></span>

<span data-ttu-id="7aa99-135">**Listing 1 - Controllers\HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="7aa99-135">**Listing 1 - Controllers\HomeController.vb**</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample1.vb)]

<span data-ttu-id="7aa99-136">목록 1의 홈 컨트롤러 클래스는 두 가지 create () 동작을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-136">The Home controller class in Listing 1 contains two Create() actions.</span></span> <span data-ttu-id="7aa99-137">첫 번째 동작인 새 동영상을 만들기 위한 HTML 폼이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-137">The first action displays the HTML form for creating a new movie.</span></span> <span data-ttu-id="7aa99-138">두 번째 create () 동작 데이터베이스에 새 동영상의 실제 삽입을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-138">The second Create() action performs the actual insert of the new movie into the database.</span></span> <span data-ttu-id="7aa99-139">두 번째 create () 작업은 첫 번째 create () 작업에 의해 표시 된 폼이 서버에 전송 될 때 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-139">The second Create() action is invoked when the form displayed by the first Create() action is submitted to the server.</span></span>

<span data-ttu-id="7aa99-140">두 번째 create () 동작에 다음 코드 줄이 포함 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-140">Notice that the second Create() action contains the following lines of code:</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample2.vb)]

<span data-ttu-id="7aa99-141">IsValid 속성 유효성 검사 오류가 있을 때 false를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-141">The IsValid property returns false when there is a validation error.</span></span> <span data-ttu-id="7aa99-142">이 경우 movie를 만들기 위한 HTML 폼이 포함 된 Create view 다시 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-142">In that case, the Create view that contains the HTML form for creating a movie is redisplayed.</span></span>

## <a name="creating-a-partial-class"></a><span data-ttu-id="7aa99-143">Partial 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="7aa99-143">Creating a Partial Class</span></span>

<span data-ttu-id="7aa99-144">영화 클래스는 Entity Framework에서 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-144">The Movie class is generated by the Entity Framework.</span></span> <span data-ttu-id="7aa99-145">솔루션 탐색기 창에서 MoviesDBModel.edmx 파일을 확장 하 고 코드 편집기에서 MoviesDBModel.Designer.vb 파일을 열 경우 영화 클래스에 대 한 코드를 볼 수 있습니다 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="7aa99-145">You can see the code for the Movie class if you expand the MoviesDBModel.edmx file in the Solution Explorer window and open the MoviesDBModel.Designer.vb file in the Code Editor (see Figure 2).</span></span>


<span data-ttu-id="7aa99-146">[![영화 엔터티에 대 한 코드](validating-with-the-idataerrorinfo-interface-vb/_static/image2.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="7aa99-146">[![The code for the Movie entity](validating-with-the-idataerrorinfo-interface-vb/_static/image2.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image3.png)</span></span>

<span data-ttu-id="7aa99-147">**그림 02**: 영화 엔터티에 대 한 코드 ([전체 크기 이미지를 보려면 클릭](validating-with-the-idataerrorinfo-interface-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="7aa99-147">**Figure 02**: The code for the Movie entity([Click to view full-size image](validating-with-the-idataerrorinfo-interface-vb/_static/image4.png))</span></span>


<span data-ttu-id="7aa99-148">영화 클래스는 partial 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-148">The Movie class is a partial class.</span></span> <span data-ttu-id="7aa99-149">즉,을 영화 클래스의 기능을 확장 하는 이름이 같은 다른 partial 클래스를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-149">That means that we can add another partial class with the same name to extend the functionality of the Movie class.</span></span> <span data-ttu-id="7aa99-150">새 부분 클래스에 유효성 검사 논리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-150">We'll add our validation logic to the new partial class.</span></span>

<span data-ttu-id="7aa99-151">모델 폴더에 목록 2의 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-151">Add the class in Listing 2 to the Models folder.</span></span>

<span data-ttu-id="7aa99-152">**Listing 2 - Models\Movie.vb**</span><span class="sxs-lookup"><span data-stu-id="7aa99-152">**Listing 2 - Models\Movie.vb**</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample3.vb)]

<span data-ttu-id="7aa99-153">알림 목록 2의 클래스를 포함 하는 *부분* 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-153">Notice that the class in Listing 2 includes the *partial* modifier.</span></span> <span data-ttu-id="7aa99-154">메서드 또는 속성이이 클래스에 추가 하는 Entity Framework에서 생성 되는 동영상 클래스의 일부가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-154">Any methods or properties that you add to this class become part of the Movie class generated by the Entity Framework.</span></span>

## <a name="adding-onchanging-and-onchanged-partial-methods"></a><span data-ttu-id="7aa99-155">OnChanging 및 OnChanged 부분 메서드 추가</span><span class="sxs-lookup"><span data-stu-id="7aa99-155">Adding OnChanging and OnChanged Partial Methods</span></span>

<span data-ttu-id="7aa99-156">Entity Framework는 엔터티 클래스를 생성할 때 Entity Framework 부분 메서드는 클래스에 자동으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-156">When the Entity Framework generates an entity class, the Entity Framework adds partial methods to the class automatically.</span></span> <span data-ttu-id="7aa99-157">Entity Framework 클래스의 각 속성에 해당 하는 OnChanging 및 OnChanged 부분 메서드를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-157">The Entity Framework generates OnChanging and OnChanged partial methods that correspond to each property of the class.</span></span>

<span data-ttu-id="7aa99-158">Entity Framework 영화 클래스의 경우 다음 메서드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-158">In the case of the Movie class, the Entity Framework creates the following methods:</span></span>

- <span data-ttu-id="7aa99-159">OnIdChanging</span><span class="sxs-lookup"><span data-stu-id="7aa99-159">OnIdChanging</span></span>
- <span data-ttu-id="7aa99-160">OnIdChanged</span><span class="sxs-lookup"><span data-stu-id="7aa99-160">OnIdChanged</span></span>
- <span data-ttu-id="7aa99-161">OnTitleChanging</span><span class="sxs-lookup"><span data-stu-id="7aa99-161">OnTitleChanging</span></span>
- <span data-ttu-id="7aa99-162">OnTitleChanged</span><span class="sxs-lookup"><span data-stu-id="7aa99-162">OnTitleChanged</span></span>
- <span data-ttu-id="7aa99-163">OnDirectorChanging</span><span class="sxs-lookup"><span data-stu-id="7aa99-163">OnDirectorChanging</span></span>
- <span data-ttu-id="7aa99-164">OnDirectorChanged</span><span class="sxs-lookup"><span data-stu-id="7aa99-164">OnDirectorChanged</span></span>
- <span data-ttu-id="7aa99-165">OnDateReleasedChanging</span><span class="sxs-lookup"><span data-stu-id="7aa99-165">OnDateReleasedChanging</span></span>
- <span data-ttu-id="7aa99-166">OnDateReleasedChanged</span><span class="sxs-lookup"><span data-stu-id="7aa99-166">OnDateReleasedChanged</span></span>

<span data-ttu-id="7aa99-167">OnChanging 메서드는 해당 속성을 변경 하기 전에 오른쪽 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-167">The OnChanging method is called right before the corresponding property is changed.</span></span> <span data-ttu-id="7aa99-168">OnChanged 메서드는 속성을 변경한 후 올바른 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-168">The OnChanged method is called right after the property is changed.</span></span>

<span data-ttu-id="7aa99-169">영화 클래스에 유효성 검사 논리를 추가 하려면 이러한 부분 메서드의 이용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-169">You can take advantage of these partial methods to add validation logic to the Movie class.</span></span> <span data-ttu-id="7aa99-170">업데이트 목록 3에서 영화 클래스 제목 및 감독 속성 비어 있지 않은 값을 할당 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-170">The update Movie class in Listing 3 verifies that the Title and Director properties are assigned nonempty values.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="7aa99-171">부분 메서드는 구현에 필요 없는 클래스에 정의 된 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-171">A partial method is a method defined in a class that you are not required to implement.</span></span> <span data-ttu-id="7aa99-172">부분 메서드를 구현 하지 않는 경우 컴파일러 메서드 시그니처를 제거 하 고 없으므로 메서드에 대 한 모든 호출 되는 부분 메서드와 관련 된 런타임 비용이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-172">If you don't implement a partial method then the compiler removes the method signature and all calls to the method so there are no run-time costs associated with the partial method.</span></span> <span data-ttu-id="7aa99-173">Visual Studio 코드 편집기에서 키워드를 입력 하 여 부분 메서드를 추가할 수 있습니다 *부분* 공백 구현 하는 부분 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-173">In the Visual Studio Code Editor, you can add a partial method by typing the keyword *partial* followed by a space to view a list of partials to implement.</span></span>


<span data-ttu-id="7aa99-174">**3-Models\Movie.vb 나열**</span><span class="sxs-lookup"><span data-stu-id="7aa99-174">**Listing 3 - Models\Movie.vb**</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample4.vb)]

<span data-ttu-id="7aa99-175">예를 들어 Title 속성에 빈 문자열을 할당 하려고 하면 다음 오류 메시지가 속하는 라는 사전이 \_오류입니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-175">For example, if you attempt to assign an empty string to the Title property, then an error message is assigned to a Dictionary named \_errors.</span></span>

<span data-ttu-id="7aa99-176">이 시점에서 실제로 일어나지 Title 속성에 빈 문자열을 할당 하 고 오류가 개인에 추가 됩니다 \_오류 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-176">At this point, nothing actually happens when you assign an empty string to the Title property and an error is added to the private \_errors field.</span></span> <span data-ttu-id="7aa99-177">ASP.NET MVC 프레임 워크를 이러한 유효성 검사 오류를 노출 하려면 IDataErrorInfo 인터페이스를 구현 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-177">We need to implement the IDataErrorInfo interface to expose these validation errors to the ASP.NET MVC framework.</span></span>

## <a name="implementing-the-idataerrorinfo-interface"></a><span data-ttu-id="7aa99-178">IDataErrorInfo 인터페이스를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-178">Implementing the IDataErrorInfo Interface</span></span>

<span data-ttu-id="7aa99-179">IDataErrorInfo 인터페이스는 첫 번째 버전부터.NET framework의 일부를 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-179">The IDataErrorInfo interface has been part of the .NET framework since the first version.</span></span> <span data-ttu-id="7aa99-180">이 인터페이스는 매우 간단한 인터페이스:</span><span class="sxs-lookup"><span data-stu-id="7aa99-180">This interface is a very simple interface:</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample5.vb)]

<span data-ttu-id="7aa99-181">IDataErrorInfo 인터페이스 클래스에서 구현 하는 경우에 ASP.NET MVC 프레임 워크 클래스의 인스턴스를 만들 때이 인터페이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-181">If a class implements the IDataErrorInfo interface, the ASP.NET MVC framework will use this interface when creating an instance of the class.</span></span> <span data-ttu-id="7aa99-182">예를 들어 Home 컨트롤러 create () 작업에는 영화 클래스의 인스턴스는 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-182">For example, the Home controller Create() action accepts an instance of the Movie class:</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample6.vb)]

<span data-ttu-id="7aa99-183">ASP.NET MVC 프레임 워크는 모델 바인더 (DefaultModelBinder)를 사용 하 여 create () 작업에 전달 된 동영상의 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-183">The ASP.NET MVC framework creates the instance of the Movie passed to the Create() action by using a model binder (the DefaultModelBinder).</span></span> <span data-ttu-id="7aa99-184">모델 바인더는 영화 개체의 인스턴스를 HTML 양식 필드를 바인딩하여 영화 개체의 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-184">The model binder is responsible for creating an instance of the Movie object by binding the HTML form fields to an instance of the Movie object.</span></span>

<span data-ttu-id="7aa99-185">DefaultModelBinder 클래스 IDataErrorInfo 인터페이스를 구현 하는지 여부를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-185">The DefaultModelBinder detects whether or not a class implements the IDataErrorInfo interface.</span></span> <span data-ttu-id="7aa99-186">이 인터페이스를 구현 하는 클래스는 모델 바인더 클래스의 각 속성에 대 한 IDataErrorInfo.this 인덱서를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-186">If a class implements this interface then the model binder invokes the IDataErrorInfo.this indexer for each property of the class.</span></span> <span data-ttu-id="7aa99-187">인덱서는 오류 메시지를 반환 하는 경우 모델 바인더를 상태를 자동으로 모델링이 오류 메시지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-187">If the indexer returns an error message then the model binder adds this error message to model state automatically.</span></span>

<span data-ttu-id="7aa99-188">또한는 DefaultModelBinder IDataErrorInfo.Error 속성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-188">The DefaultModelBinder also checks the IDataErrorInfo.Error property.</span></span> <span data-ttu-id="7aa99-189">이 속성의 클래스와 연결 된 비 속성 특정 유효성 검사 오류를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-189">This property is intended to represent non-property specific validation errors associated with the class.</span></span> <span data-ttu-id="7aa99-190">예를 들어 다음 영화 클래스의 여러 속성의 값에 따라 달라 지는 유효성 검사 규칙을 적용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-190">For example, you might want to enforce a validation rule that depends on the values of multiple properties of the Movie class.</span></span> <span data-ttu-id="7aa99-191">이 경우 오류 속성에서는 유효성 검사 오류를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-191">In that case, you would return a validation error from the Error property.</span></span>

<span data-ttu-id="7aa99-192">목록 4에 업데이트 된 영화 클래스 IDataErrorInfo 인터페이스를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-192">The updated Movie class in Listing 4 implements the IDataErrorInfo interface.</span></span>

<span data-ttu-id="7aa99-193">**4-Models\Movie.vb (IDataErrorInfo 구현)를 나열 합니다.**</span><span class="sxs-lookup"><span data-stu-id="7aa99-193">**Listing 4 - Models\Movie.vb (implements IDataErrorInfo)**</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample7.vb)]

<span data-ttu-id="7aa99-194">인덱서 속성 검사 목록 4에는 \_인덱서에 오류 컬렉션을 속성 이름에 해당 하는 키를 포함 하는 경우 참조를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-194">In Listing 4, the indexer property checks the \_errors collection to see if it contains a key that corresponds to the property name passed to the indexer.</span></span> <span data-ttu-id="7aa99-195">속성에 연결 된 유효성 검사 오류가 없는 경우 빈 문자열이 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-195">If there is no validation error associated with the property then an empty string is returned.</span></span>

<span data-ttu-id="7aa99-196">수정 된 영화 클래스를 사용 하는 어떤 방식으로든에서 Home 컨트롤러를 수정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-196">You don't need to modify the Home controller in any way to use the modified Movie class.</span></span> <span data-ttu-id="7aa99-197">그림 3에 표시 되는 페이지 제목 또는 Director 양식 필드에 없는 값을 입력 하는 경우를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-197">The page displayed in Figure 3 illustrates what happens when no value is entered for the Title or Director form fields.</span></span>


<span data-ttu-id="7aa99-198">[![작업 메서드를 자동으로 만들기](validating-with-the-idataerrorinfo-interface-vb/_static/image3.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="7aa99-198">[![Creating action methods automatically](validating-with-the-idataerrorinfo-interface-vb/_static/image3.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image5.png)</span></span>

<span data-ttu-id="7aa99-199">**그림 03**: 값이 누락 된 양식을 ([전체 크기 이미지를 보려면 클릭](validating-with-the-idataerrorinfo-interface-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="7aa99-199">**Figure 03**: A form with missing values ([Click to view full-size image](validating-with-the-idataerrorinfo-interface-vb/_static/image6.png))</span></span>


<span data-ttu-id="7aa99-200">공지 DateReleased 값 자동으로 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-200">Notice that the DateReleased value is validated automatically.</span></span> <span data-ttu-id="7aa99-201">DateReleased 속성은 NULL 값을 수락 하지 않으므로 DefaultModelBinder이이 속성에 대 한 유효성 검사 오류를 자동으로 생성 값에 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="7aa99-201">Because the DateReleased property does not accept NULL values, the DefaultModelBinder generates a validation error for this property automatically when it does not have a value.</span></span> <span data-ttu-id="7aa99-202">DateReleased 속성에 대 한 오류 메시지를 수정 하려는 경우 사용자 지정 모델 바인더를 만드는 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-202">If you want to modify the error message for the DateReleased property then you need to create a custom model binder.</span></span>

## <a name="summary"></a><span data-ttu-id="7aa99-203">요약</span><span class="sxs-lookup"><span data-stu-id="7aa99-203">Summary</span></span>

<span data-ttu-id="7aa99-204">이 자습서에서는 유효성 검사 오류 메시지를 생성 하려면 IDataErrorInfo 인터페이스를 사용 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-204">In this tutorial, you learned how to use the IDataErrorInfo interface to generate validation error messages.</span></span> <span data-ttu-id="7aa99-205">먼저 Entity Framework에서 생성 되는 부분 영화 클래스의 기능을 확장 하는 부분 영화 클래스를 만들었는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-205">First, we created a partial Movie class that extends the functionality of the partial Movie class generated by the Entity Framework.</span></span> <span data-ttu-id="7aa99-206">다음으로 영화 클래스 OnTitleChanging() 및 OnDirectorChanging() 부분 메서드를 유효성 검사 논리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aa99-206">Next, we added validation logic to the Movie class OnTitleChanging() and OnDirectorChanging() partial methods.</span></span> <span data-ttu-id="7aa99-207">마지막으로, ASP.NET MVC 프레임 워크를 이러한 유효성 검사 메시지를 노출 하려면 IDataErrorInfo 인터페이스 구현.</span><span class="sxs-lookup"><span data-stu-id="7aa99-207">Finally, we implemented the IDataErrorInfo interface in order to expose these validation messages to the ASP.NET MVC framework.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7aa99-208">[이전](performing-simple-validation-vb.md)
> [다음](validating-with-a-service-layer-vb.md)</span><span class="sxs-lookup"><span data-stu-id="7aa99-208">[Previous](performing-simple-validation-vb.md)
[Next](validating-with-a-service-layer-vb.md)</span></span>
