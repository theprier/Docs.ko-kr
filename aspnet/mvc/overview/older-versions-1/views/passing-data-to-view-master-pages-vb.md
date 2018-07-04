---
uid: mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-vb
title: 보기 마스터 페이지 (VB)에 데이터 전달 | Microsoft Docs
author: microsoft
description: 이 자습서의 목표는 보기 마스터 페이지에는 컨트롤러에서 데이터를 전달 하는 방법을 설명 합니다. 살펴봅니다 m 보기로 데이터를 전달 하기 위한 두 가지 전략을 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/16/2008
ms.topic: article
ms.assetid: 37a1ebae-8773-408f-8645-d21da7ff9ae1
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: e70f15d98101336dbef31b4f9d8b958632e46c01
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37388521"
---
<a name="passing-data-to-view-master-pages-vb"></a><span data-ttu-id="bf9d7-104">보기 마스터 페이지 (VB)에 데이터 전달</span><span class="sxs-lookup"><span data-stu-id="bf9d7-104">Passing Data to View Master Pages (VB)</span></span>
====================
<span data-ttu-id="bf9d7-105">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="bf9d7-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="bf9d7-106">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="bf9d7-106">Download PDF</span></span>](http://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_13_VB.pdf)

> <span data-ttu-id="bf9d7-107">이 자습서의 목표는 보기 마스터 페이지에는 컨트롤러에서 데이터를 전달 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-107">The goal of this tutorial is to explain how you can pass data from a controller to a view master page.</span></span> <span data-ttu-id="bf9d7-108">보기 마스터 페이지에 데이터를 전달 하기 위한 두 가지 전략을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-108">We examine two strategies for passing data to a view master page.</span></span> <span data-ttu-id="bf9d7-109">첫째, 응용 프로그램 유지 관리 하기 어려울 정도로 초래 하는 쉬운 솔루션을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-109">First, we discuss an easy solution that results in an application that is difficult to maintain.</span></span> <span data-ttu-id="bf9d7-110">다음으로 필요한 약간 더 많은 초기 작업 하지만 훨씬 더 관리 하기 쉬운 응용 프로그램에서 결과 보다 나은 솔루션을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-110">Next, we examine a much better solution that requires a little more initial work but results in a much more maintainable application.</span></span>


## <a name="passing-data-to-view-master-pages"></a><span data-ttu-id="bf9d7-111">보기 마스터 페이지에 데이터 전달</span><span class="sxs-lookup"><span data-stu-id="bf9d7-111">Passing Data to View Master Pages</span></span>

<span data-ttu-id="bf9d7-112">이 자습서의 목표는 보기 마스터 페이지에는 컨트롤러에서 데이터를 전달 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-112">The goal of this tutorial is to explain how you can pass data from a controller to a view master page.</span></span> <span data-ttu-id="bf9d7-113">보기 마스터 페이지에 데이터를 전달 하기 위한 두 가지 전략을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-113">We examine two strategies for passing data to a view master page.</span></span> <span data-ttu-id="bf9d7-114">첫째, 응용 프로그램 유지 관리 하기 어려울 정도로 초래 하는 쉬운 솔루션을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-114">First, we discuss an easy solution that results in an application that is difficult to maintain.</span></span> <span data-ttu-id="bf9d7-115">다음으로 필요한 약간 더 많은 초기 작업 하지만 훨씬 더 관리 하기 쉬운 응용 프로그램에서 결과 보다 나은 솔루션을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-115">Next, we examine a much better solution that requires a little more initial work but results in a much more maintainable application.</span></span>

### <a name="the-problem"></a><span data-ttu-id="bf9d7-116">문제</span><span class="sxs-lookup"><span data-stu-id="bf9d7-116">The Problem</span></span>

<span data-ttu-id="bf9d7-117">영화 데이터베이스 응용 프로그램을 빌드하는 하 고 영화 범주 목록 응용 프로그램에서 모든 페이지에 표시 하려는 imagine (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="bf9d7-117">Imagine that you are building a movie database application and you want to display the list of movie categories on every page in your application (see Figure 1).</span></span> <span data-ttu-id="bf9d7-118">또한 영화 범주 목록 데이터베이스 테이블에 저장 되도록 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-118">Imagine, furthermore, that the list of movie categories is stored in a database table.</span></span> <span data-ttu-id="bf9d7-119">이 경우 데이터베이스에서 범주를 검색 및 보기 마스터 페이지 내에 영화 범주 목록을 렌더링 하는 것이 없게 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-119">In that case, it would make sense to retrieve the categories from the database and render the list of movie categories within a view master page.</span></span>


<span data-ttu-id="bf9d7-120">[![보기 마스터 페이지에 동영상 범주 표시](passing-data-to-view-master-pages-vb/_static/image2.png)](passing-data-to-view-master-pages-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="bf9d7-120">[![Displaying movie categories in a view master page](passing-data-to-view-master-pages-vb/_static/image2.png)](passing-data-to-view-master-pages-vb/_static/image1.png)</span></span>

<span data-ttu-id="bf9d7-121">**그림 01**: 영화 범주 보기 마스터 페이지에 표시 ([큰 이미지를 보려면 클릭](passing-data-to-view-master-pages-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="bf9d7-121">**Figure 01**: Displaying movie categories in a view master page ([Click to view full-size image](passing-data-to-view-master-pages-vb/_static/image3.png))</span></span>


<span data-ttu-id="bf9d7-122">문제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-122">Here's the problem.</span></span> <span data-ttu-id="bf9d7-123">마스터 페이지에 동영상 범주 목록이 검색 하려면?</span><span class="sxs-lookup"><span data-stu-id="bf9d7-123">How do you retrieve the list of movie categories in the master page?</span></span> <span data-ttu-id="bf9d7-124">마스터 페이지에서 모델 클래스의 메서드를 직접 호출 하기 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-124">It is tempting to call methods of your model classes in the master page directly.</span></span> <span data-ttu-id="bf9d7-125">즉, 마스터 페이지에서 데이터베이스 오른쪽에서 데이터를 검색 하기 위한 코드를 포함 하 고 싶을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-125">In other words, it is tempting to include the code for retrieving the data from the database right in your master page.</span></span> <span data-ttu-id="bf9d7-126">그러나 데이터베이스에 액세스 하기 위해 MVC 컨트롤러 무시을 위반 하는 MVC 응용 프로그램을 구축 하는 주요 이점 중 하나는 중요 한 부분의 분리 정리 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-126">However, bypassing your MVC controllers to access the database would violate the clean separation of concerns that is one of the primary benefits of building an MVC application.</span></span>

<span data-ttu-id="bf9d7-127">MVC 응용 프로그램에서는 MVC 뷰와 MVC 모델 MVC 컨트롤러에서 처리할 간의 모든 상호 작용을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-127">In an MVC application, you want all interaction between your MVC views and your MVC model to be handled by your MVC controllers.</span></span> <span data-ttu-id="bf9d7-128">이 중요 한 부분의이 분리 더 유지 하 고, 적응력이 테스트 가능 응용 프로그램에서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-128">This separation of concerns results in a more maintainable, adaptable, and testable application.</span></span>

<span data-ttu-id="bf9d7-129">MVC 응용 프로그램의 컨트롤러 작업에 의해 – 보기 마스터 페이지를 포함 하 여 – 보기로 전달 된 모든 데이터 보기에 전달 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-129">In an MVC application, all data passed to a view – including a view master page – should be passed to a view by a controller action.</span></span> <span data-ttu-id="bf9d7-130">또한 데이터 뷰 데이터를 활용 하 여 전달 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-130">Furthermore, the data should be passed by taking advantage of view data.</span></span> <span data-ttu-id="bf9d7-131">이 자습서의 나머지 부분에서는 보기 마스터 페이지 뷰 데이터를 전달 하는 두 가지 방법을 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-131">In the remainder of this tutorial, I examine two methods of passing view data to a view master page.</span></span>

### <a name="the-simple-solution"></a><span data-ttu-id="bf9d7-132">간단한 솔루션</span><span class="sxs-lookup"><span data-stu-id="bf9d7-132">The Simple Solution</span></span>

<span data-ttu-id="bf9d7-133">보기 마스터 페이지에는 컨트롤러에서 뷰 데이터를 전달 하는 가장 간단한 솔루션을 사용 하 여 시작 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-133">Let's start with the simplest solution to passing view data from a controller to a view master page.</span></span> <span data-ttu-id="bf9d7-134">가장 간단한 방법은 각 컨트롤러 작업에서 마스터 페이지에 대 한 뷰 데이터를 전달 하 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-134">The simplest solution is to pass the view data for the master page in each and every controller action.</span></span>

<span data-ttu-id="bf9d7-135">목록 1에서 컨트롤러를 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-135">Consider the controller in Listing 1.</span></span> <span data-ttu-id="bf9d7-136">라는 두 가지 작업이 노출 `Index()` 고 `Details()`입니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-136">It exposes two actions named `Index()` and `Details()`.</span></span> <span data-ttu-id="bf9d7-137">`Index()` 작업 메서드가 영화 데이터베이스 테이블에 있는 모든 영화를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-137">The `Index()` action method returns every movie in the Movies database table.</span></span> <span data-ttu-id="bf9d7-138">`Details()` 작업 메서드가 특정 영화 범주의 모든 영화를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-138">The `Details()` action method returns every movie in a particular movie category.</span></span>

<span data-ttu-id="bf9d7-139">**목록 1 – `Controllers\HomeController.vb`**</span><span class="sxs-lookup"><span data-stu-id="bf9d7-139">**Listing 1 – `Controllers\HomeController.vb`**</span></span>

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample1.vb)]

<span data-ttu-id="bf9d7-140">모두를 `Index()` 하며 `Details()` 작업 데이터를 보려면 두 항목을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-140">Notice that both the `Index()` and the `Details()` actions add two items to view data.</span></span> <span data-ttu-id="bf9d7-141">`Index()` 두 키를 추가 하는 작업: 범주 및 동영상입니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-141">The `Index()` action adds two keys: categories and movies.</span></span> <span data-ttu-id="bf9d7-142">범주 키 보기 마스터 페이지에서 표시 하는 영화 범주 목록을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-142">The categories key represents the list of movie categories displayed by the view master page.</span></span> <span data-ttu-id="bf9d7-143">영화 키 인덱스 뷰 페이지에서 표시 하는 영화 목록을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-143">The movies key represents the list of movies displayed by the Index view page.</span></span>

<span data-ttu-id="bf9d7-144">`Details()` 작업 범주 및 영화 라는 두 개의 키 추가.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-144">The `Details()` action also adds two keys named categories and movies.</span></span> <span data-ttu-id="bf9d7-145">범주 키를 다시 한 번 보기 마스터 페이지에서 표시 하는 영화 범주 목록을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-145">The categories key, once again, represents the list of movie categories displayed by the view master page.</span></span> <span data-ttu-id="bf9d7-146">영화 키 세부 정보 보기 페이지에서 표시 하는 특정 범주에는 영화 목록을 나타냅니다 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="bf9d7-146">The movies key represents the list of movies in a particular category displayed by the Details view page (see Figure 2).</span></span>


<span data-ttu-id="bf9d7-147">[![세부 정보 보기](passing-data-to-view-master-pages-vb/_static/image5.png)](passing-data-to-view-master-pages-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="bf9d7-147">[![The Details view](passing-data-to-view-master-pages-vb/_static/image5.png)](passing-data-to-view-master-pages-vb/_static/image4.png)</span></span>

<span data-ttu-id="bf9d7-148">**그림 02**: 세부 정보 보기 ([큰 이미지를 보려면 클릭](passing-data-to-view-master-pages-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="bf9d7-148">**Figure 02**: The Details view ([Click to view full-size image](passing-data-to-view-master-pages-vb/_static/image6.png))</span></span>


<span data-ttu-id="bf9d7-149">인덱스 보기 목록 2에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-149">The Index view is contained in Listing 2.</span></span> <span data-ttu-id="bf9d7-150">단순히 데이터 보기의에서 영화 항목으로 표시 하는 영화 목록을 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-150">It simply iterates through the list of movies represented by the movies item in view data.</span></span>

<span data-ttu-id="bf9d7-151">**2 – 나열 `Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="bf9d7-151">**Listing 2 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](passing-data-to-view-master-pages-vb/samples/sample2.aspx)]

<span data-ttu-id="bf9d7-152">보기 마스터 페이지는 목록 3에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-152">The view master page is contained in Listing 3.</span></span> <span data-ttu-id="bf9d7-153">보기 마스터 페이지를 반복 하 고 모든 데이터 보기에서에서 범주 항목이 나타내는 영화 범주를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-153">The view master page iterates and renders all of the movie categories represented by the categories item from view data.</span></span>

<span data-ttu-id="bf9d7-154">**3 – 나열 `Views\Shared\Site.master`**</span><span class="sxs-lookup"><span data-stu-id="bf9d7-154">**Listing 3 – `Views\Shared\Site.master`**</span></span>

[!code-aspx[Main](passing-data-to-view-master-pages-vb/samples/sample3.aspx)]

<span data-ttu-id="bf9d7-155">모든 데이터 뷰 데이터 보기와 보기 마스터 페이지에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-155">All data is passed to the view and the view master page through view data.</span></span> <span data-ttu-id="bf9d7-156">마스터 페이지에 데이터를 전달 하는 올바른 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-156">That is the correct way to pass data to the master page.</span></span>

<span data-ttu-id="bf9d7-157">따라서이 솔루션을 사용 하 여 무엇이 있습니까?</span><span class="sxs-lookup"><span data-stu-id="bf9d7-157">So, what's wrong with this solution?</span></span> <span data-ttu-id="bf9d7-158">이 솔루션 (없습니다 반복 직접) DRY 원칙을 위반 하는 것이 문제가입니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-158">The problem is that this solution violates the DRY (Don't Repeat Yourself) principle.</span></span> <span data-ttu-id="bf9d7-159">각 컨트롤러 작업에는 동일한 데이터를 보려면 동영상 범주 목록을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-159">Each and every controller action must add the very same list of movie categories to view data.</span></span> <span data-ttu-id="bf9d7-160">응용 프로그램에 중복 코드를 포함 하면 응용 프로그램 유지 관리, 적응 및 수정 하기가 훨씬 어려워집니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-160">Having duplicate code in your application makes your application much more difficult to maintain, adapt, and modify.</span></span>

### <a name="the-good-solution"></a><span data-ttu-id="bf9d7-161">적합 한 솔루션</span><span class="sxs-lookup"><span data-stu-id="bf9d7-161">The Good Solution</span></span>

<span data-ttu-id="bf9d7-162">이 섹션에서는 보기 마스터 페이지에는 컨트롤러 작업에서 데이터를 전달 하려면 대체 하 고, 더 나은 솔루션을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-162">In this section, we examine an alternative, and better, solution to passing data from a controller action to a view master page.</span></span> <span data-ttu-id="bf9d7-163">각 컨트롤러 작업에서 마스터 페이지에 대 한 동영상 범주를 추가 하는 대신 추가 동영상 범주는 뷰 데이터에 한 번만 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-163">Instead of adding the movie categories for the master page in each and every controller action, we add the movie categories to the view data only once.</span></span> <span data-ttu-id="bf9d7-164">보기 마스터 페이지에 의해 사용 되는 모든 보기 데이터는 응용 프로그램 컨트롤러에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-164">All view data used by the view master page is added in an Application controller.</span></span>

<span data-ttu-id="bf9d7-165">ApplicationController 클래스 4에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-165">The ApplicationController class is contained in Listing 4.</span></span>

<span data-ttu-id="bf9d7-166">ApplicationController 클래스 4에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-166">The ApplicationController class is contained in Listing 4.</span></span>

<span data-ttu-id="bf9d7-167">**4-목록 `Controllers\ApplicationController.vb`**</span><span class="sxs-lookup"><span data-stu-id="bf9d7-167">**Listing 4 – `Controllers\ApplicationController.vb`**</span></span>

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample4.vb)]

<span data-ttu-id="bf9d7-168">목록 4에서 응용 프로그램 컨트롤러에 대 한 유의 해야 하는 방법은 세 가지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-168">There are three things that you should notice about the Application controller in Listing 4.</span></span> <span data-ttu-id="bf9d7-169">먼저 기본 System.Web.Mvc.Controller 클래스에서 클래스를 상속 함을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-169">First, notice that the class inherits from the base System.Web.Mvc.Controller class.</span></span> <span data-ttu-id="bf9d7-170">응용 프로그램 컨트롤러는 컨트롤러 클래스.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-170">The Application controller is a controller class.</span></span>

<span data-ttu-id="bf9d7-171">둘째, 응용 프로그램 컨트롤러 클래스 MustInherit 클래스는 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-171">Second, notice that the Application controller class is a MustInherit class.</span></span> <span data-ttu-id="bf9d7-172">MustInherit 클래스는 구체적인 클래스에서 구현 해야 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-172">An MustInherit class is a class that must be implemented by a concrete class.</span></span> <span data-ttu-id="bf9d7-173">응용 프로그램 컨트롤러는 MustInherit 클래스 이기 때문에는 클래스에 직접 정의 된 메서드를 호출할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-173">Because the Application controller is an MustInherit class, you cannot not invoke any methods defined in the class directly.</span></span> <span data-ttu-id="bf9d7-174">응용 프로그램 클래스를 직접 호출 하려고 하면 다음 하면 오류 메시지가 표시 됩니다는 리소스를 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-174">If you attempt to invoke the Application class directly then you'll get a Resource Cannot Be Found error message.</span></span>

<span data-ttu-id="bf9d7-175">셋째, 응용 프로그램 컨트롤러에 데이터를 보려면 동영상 범주 목록에 추가 하는 생성자를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-175">Third, notice that the Application controller contains a constructor that adds the list of movie categories to view data.</span></span> <span data-ttu-id="bf9d7-176">응용 프로그램 컨트롤러에서 상속 되는 모든 컨트롤러 클래스는 자동으로 응용 프로그램 컨트롤러의 생성자를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-176">Every controller class that inherits from the Application controller calls the Application controller's constructor automatically.</span></span> <span data-ttu-id="bf9d7-177">응용 프로그램 컨트롤러에서 상속 되는 모든 컨트롤러에서 모든 작업을 호출할 때마다 영화 범주 뷰 데이터에 자동으로 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-177">Whenever you call any action on any controller that inherits from the Application controller, the movie categories is included in the view data automatically.</span></span>

<span data-ttu-id="bf9d7-178">영화 컨트롤러 목록 5에서 응용 프로그램 컨트롤러에서 상속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-178">The Movies controller in Listing 5 inherits from the Application controller.</span></span>

<span data-ttu-id="bf9d7-179">**5-목록 `Controllers\MoviesController.vb`**</span><span class="sxs-lookup"><span data-stu-id="bf9d7-179">**Listing 5 – `Controllers\MoviesController.vb`**</span></span>

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample5.vb)]

<span data-ttu-id="bf9d7-180">영화 컨트롤러를 이전 섹션에서 설명한 Home 컨트롤러와 마찬가지로 라는 두 개의 작업 메서드를 노출 `Index()` 고 `Details()`입니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-180">The Movies controller, just like the Home controller discussed in the previous section, exposes two action methods named `Index()` and `Details()`.</span></span> <span data-ttu-id="bf9d7-181">보기 마스터 페이지에서 표시 하는 영화 범주 목록이 아닌 알림이 하나에서 데이터를 추가 합니다 `Index()` 또는 `Details()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-181">Notice that the list of movie categories displayed by the view master page is not added to view data in either the `Index()` or `Details()` method.</span></span> <span data-ttu-id="bf9d7-182">영화 컨트롤러를 응용 프로그램 컨트롤러에서 상속 하기 때문에 자동으로 데이터를 보려면 동영상 범주 목록이 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-182">Because the Movies controller inherits from the Application controller, the list of movie categories is added to view data automatically.</span></span>

<span data-ttu-id="bf9d7-183">보기 마스터 페이지에 대 한 뷰 데이터를 추가 하려면이 솔루션 (없습니다 반복 직접) DRY 원칙을 위반 하지 않도록 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-183">Notice that this solution to adding view data for a view master page does not violate the DRY (Don't Repeat Yourself) principle.</span></span> <span data-ttu-id="bf9d7-184">하나의 위치에 포함 된 데이터를 보려면 동영상 범주 목록에 추가 하는 것에 대 한 코드: 응용 프로그램 컨트롤러에 대 한 생성자입니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-184">The code for adding the list of movie categories to view data is contained in only one location: the constructor for the Application controller.</span></span>

### <a name="summary"></a><span data-ttu-id="bf9d7-185">요약</span><span class="sxs-lookup"><span data-stu-id="bf9d7-185">Summary</span></span>

<span data-ttu-id="bf9d7-186">이 자습서에서는 보기 마스터 페이지를 컨트롤러에서 뷰 데이터를 전달 하는 두 가지 방법에 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-186">In this tutorial, we discussed two approaches to passing view data from a controller to a view master page.</span></span> <span data-ttu-id="bf9d7-187">첫째, 접근 방식을 유지 관리 하기가 있지만 단순 하 고 검사 했습니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-187">First, we examined a simple, but difficult to maintain approach.</span></span> <span data-ttu-id="bf9d7-188">첫 번째 섹션에서는 응용 프로그램에서 각 모든 컨트롤러 작업에서 보기 마스터 페이지에 대 한 뷰 데이터를 추가 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-188">In the first section, we discussed how you can add view data for a view master page in each every controller action in your application.</span></span> <span data-ttu-id="bf9d7-189">우리는 이것이 잘못 된 방법은 (없습니다 반복 직접) DRY 원칙을 위반 하기 때문에 결론을 내렸습니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-189">We concluded that this was a bad approach because it violates the DRY (Don't Repeat Yourself) principle.</span></span>

<span data-ttu-id="bf9d7-190">다음으로 데이터를 보려면 보기 마스터 페이지에 필요한 데이터를 추가 하는 것에 대 한 훨씬 더 나은 전략을 검사 했습니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-190">Next, we examined a much better strategy for adding data required by a view master page to view data.</span></span> <span data-ttu-id="bf9d7-191">각 컨트롤러 작업에서 데이터 보기를 추가 하는 대신 응용 프로그램 제어기 내에서 한 번만 뷰 데이터를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-191">Instead of adding the view data in each and every controller action, we added the view data only once within an Application controller.</span></span> <span data-ttu-id="bf9d7-192">이런 방식으로 ASP.NET MVC 응용 프로그램에서 보기 마스터 페이지에 데이터를 전달 하는 경우 코드 중복을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf9d7-192">That way, you can avoid duplicate code when passing data to a view master page in an ASP.NET MVC application.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="bf9d7-193">이전</span><span class="sxs-lookup"><span data-stu-id="bf9d7-193">Previous</span></span>](creating-page-layouts-with-view-master-pages-vb.md)
