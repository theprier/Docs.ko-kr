---
uid: mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-cs
title: 데이터 뷰 마스터 페이지 (C#)를 전달 | Microsoft Docs
author: microsoft
description: 이 자습서의 목표 뷰 마스터 페이지에는 컨트롤러에서 데이터를 전달 하는 방법을 설명 하는 것입니다. 살펴볼 데이터 보기 m에 전달 하기 위한 두 가지 전략 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/16/2008
ms.topic: article
ms.assetid: 5fee879b-8bde-42a9-a434-60ba6b1cf747
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: bfb58cbe0c415c092f3a41e518281a7461d2803c
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="passing-data-to-view-master-pages-c"></a><span data-ttu-id="1dab2-104">데이터 뷰 마스터 페이지 (C#)를 전달</span><span class="sxs-lookup"><span data-stu-id="1dab2-104">Passing Data to View Master Pages (C#)</span></span>
====================
<span data-ttu-id="1dab2-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="1dab2-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="1dab2-106">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="1dab2-106">Download PDF</span></span>](http://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_13_CS.pdf)

> <span data-ttu-id="1dab2-107">이 자습서의 목표 뷰 마스터 페이지에는 컨트롤러에서 데이터를 전달 하는 방법을 설명 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-107">The goal of this tutorial is to explain how you can pass data from a controller to a view master page.</span></span> <span data-ttu-id="1dab2-108">데이터 뷰 마스터 페이지를 전달 하는 두 가지 전략이 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-108">We examine two strategies for passing data to a view master page.</span></span> <span data-ttu-id="1dab2-109">첫째, 유지 관리 하기 어려운 응용 프로그램에서 발생 하는 손쉬운 솔루션을 논의 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-109">First, we discuss an easy solution that results in an application that is difficult to maintain.</span></span> <span data-ttu-id="1dab2-110">다음으로, 보다 나은 솔루션을 필요한 약간 더 많은 초기 작업이 훨씬 더 쉽게 유지 관리할 응용 프로그램에서 결과 제외한 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-110">Next, we examine a much better solution that requires a little more initial work but results in a much more maintainable application.</span></span>


## <a name="passing-data-to-view-master-pages"></a><span data-ttu-id="1dab2-111">마스터 페이지 보기에 대 한 데이터 전달</span><span class="sxs-lookup"><span data-stu-id="1dab2-111">Passing Data to View Master Pages</span></span>

<span data-ttu-id="1dab2-112">이 자습서의 목표 뷰 마스터 페이지에는 컨트롤러에서 데이터를 전달 하는 방법을 설명 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-112">The goal of this tutorial is to explain how you can pass data from a controller to a view master page.</span></span> <span data-ttu-id="1dab2-113">데이터 뷰 마스터 페이지를 전달 하는 두 가지 전략이 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-113">We examine two strategies for passing data to a view master page.</span></span> <span data-ttu-id="1dab2-114">첫째, 유지 관리 하기 어려운 응용 프로그램에서 발생 하는 손쉬운 솔루션을 논의 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-114">First, we discuss an easy solution that results in an application that is difficult to maintain.</span></span> <span data-ttu-id="1dab2-115">다음으로, 보다 나은 솔루션을 필요한 약간 더 많은 초기 작업이 훨씬 더 쉽게 유지 관리할 응용 프로그램에서 결과 제외한 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-115">Next, we examine a much better solution that requires a little more initial work but results in a much more maintainable application.</span></span>

### <a name="the-problem"></a><span data-ttu-id="1dab2-116">문제</span><span class="sxs-lookup"><span data-stu-id="1dab2-116">The Problem</span></span>

<span data-ttu-id="1dab2-117">영화 데이터베이스 응용 프로그램을 작성 하는 한 응용 프로그램에서 모든 페이지에 동영상 범주 목록을 표시 하려면 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="1dab2-117">Imagine that you are building a movie database application and you want to display the list of movie categories on every page in your application (see Figure 1).</span></span> <span data-ttu-id="1dab2-118">또한 영화 범주 목록 데이터베이스 테이블에 저장 되도록 가정해 보세요.</span><span class="sxs-lookup"><span data-stu-id="1dab2-118">Imagine, furthermore, that the list of movie categories is stored in a database table.</span></span> <span data-ttu-id="1dab2-119">이 경우 하기가 데이터베이스에서 사용 하 고 범주를 검색 하 고 뷰 마스터 페이지 내에서 영화 범주 목록이 렌더링할 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-119">In that case, it would make sense to retrieve the categories from the database and render the list of movie categories within a view master page.</span></span>


<span data-ttu-id="1dab2-120">[![영화 범주 뷰 마스터 페이지에 표시](passing-data-to-view-master-pages-cs/_static/image2.png)](passing-data-to-view-master-pages-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="1dab2-120">[![Displaying movie categories in a view master page](passing-data-to-view-master-pages-cs/_static/image2.png)](passing-data-to-view-master-pages-cs/_static/image1.png)</span></span>

<span data-ttu-id="1dab2-121">**그림 01**: 영화 범주 뷰 마스터 페이지에 표시 ([전체 크기 이미지를 보려면 클릭](passing-data-to-view-master-pages-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="1dab2-121">**Figure 01**: Displaying movie categories in a view master page ([Click to view full-size image](passing-data-to-view-master-pages-cs/_static/image3.png))</span></span>


<span data-ttu-id="1dab2-122">이 문제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-122">Here's the problem.</span></span> <span data-ttu-id="1dab2-123">마스터 페이지에 동영상 범주 목록이 검색 방법을</span><span class="sxs-lookup"><span data-stu-id="1dab2-123">How do you retrieve the list of movie categories in the master page?</span></span> <span data-ttu-id="1dab2-124">마스터 페이지에서 모델 클래스의 메서드를 직접 호출 하기 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-124">It is tempting to call methods of your model classes in the master page directly.</span></span> <span data-ttu-id="1dab2-125">즉, 마스터 페이지에서 데이터베이스 오른쪽에서 데이터를 검색 하기 위한 코드를 포함 하는 캐시는 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-125">In other words, it is tempting to include the code for retrieving the data from the database right in your master page.</span></span> <span data-ttu-id="1dab2-126">그러나 데이터베이스에 액세스 하기 위해 MVC 컨트롤러 무시 MVC 응용 프로그램 빌드 과정의 주요 이점 중 하나는 문제의 정리 분리를 위반 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-126">However, bypassing your MVC controllers to access the database would violate the clean separation of concerns that is one of the primary benefits of building an MVC application.</span></span>

<span data-ttu-id="1dab2-127">MVC 응용 프로그램에서 MVC 컨트롤러에서 처리를 사용해 MVC 뷰 및 MVC 모델 간의 모든 상호 작용을 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-127">In an MVC application, you want all interaction between your MVC views and your MVC model to be handled by your MVC controllers.</span></span> <span data-ttu-id="1dab2-128">이 문제의 분리 보다 유지 관리할 수, 적응력이 고 테스트 가능 응용 프로그램에서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-128">This separation of concerns results in a more maintainable, adaptable, and testable application.</span></span>

<span data-ttu-id="1dab2-129">MVC 응용 프로그램에서 컨트롤러 작업에 의해 뷰 마스터 페이지를 포함 하 고 여 보기에 전달 되는 모든 데이터 보기에 전달 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-129">In an MVC application, all data passed to a view – including a view master page – should be passed to a view by a controller action.</span></span> <span data-ttu-id="1dab2-130">또한 데이터 뷰 데이터를 활용 하 여 전달 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-130">Furthermore, the data should be passed by taking advantage of view data.</span></span> <span data-ttu-id="1dab2-131">이 자습서의 나머지 부분에서 뷰 마스터 페이지를 뷰 데이터를 전달 하는 두 가지 방법을 검토 하려면.</span><span class="sxs-lookup"><span data-stu-id="1dab2-131">In the remainder of this tutorial, I examine two methods of passing view data to a view master page.</span></span>

### <a name="the-simple-solution"></a><span data-ttu-id="1dab2-132">간단한 솔루션</span><span class="sxs-lookup"><span data-stu-id="1dab2-132">The Simple Solution</span></span>

<span data-ttu-id="1dab2-133">뷰 마스터 페이지에는 컨트롤러에서 뷰 데이터를 전달 하는 가장 간단한 솔루션으로 시작 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-133">Let's start with the simplest solution to passing view data from a controller to a view master page.</span></span> <span data-ttu-id="1dab2-134">간단한 솔루션은 각 컨트롤러 작업에서 마스터 페이지에 대 한 뷰 데이터를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-134">The simplest solution is to pass the view data for the master page in each and every controller action.</span></span>

<span data-ttu-id="1dab2-135">목록 1의 컨트롤러를 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-135">Consider the controller in Listing 1.</span></span> <span data-ttu-id="1dab2-136">라는 두 가지 동작을 노출 `Index()` 및 `Details()`합니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-136">It exposes two actions named `Index()` and `Details()`.</span></span> <span data-ttu-id="1dab2-137">`Index()` 작업 메서드가 영화 데이터베이스 테이블의 모든 동영상을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-137">The `Index()` action method returns every movie in the Movies database table.</span></span> <span data-ttu-id="1dab2-138">`Details()` 작업 메서드가 특정 영화 범주에 있는 모든 동영상을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-138">The `Details()` action method returns every movie in a particular movie category.</span></span>

<span data-ttu-id="1dab2-139">**1 – 나열 `Controllers\HomeController.cs`**</span><span class="sxs-lookup"><span data-stu-id="1dab2-139">**Listing 1 – `Controllers\HomeController.cs`**</span></span>

[!code-csharp[Main](passing-data-to-view-master-pages-cs/samples/sample1.cs)]

<span data-ttu-id="1dab2-140">index ()와 Details() 작업 모두에 데이터를 보려면 두 항목을 추가 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-140">Notice that both the Index() and the Details() actions add two items to view data.</span></span> <span data-ttu-id="1dab2-141">두 키를 추가 하는 index () 동작: 범주 및 동영상 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-141">The Index() action adds two keys: categories and movies.</span></span> <span data-ttu-id="1dab2-142">범주 키 보기 마스터 페이지에서 표시 영화 범주의 목록을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-142">The categories key represents the list of movie categories displayed by the view master page.</span></span> <span data-ttu-id="1dab2-143">영화 키 인덱스 뷰 페이지에서 표시 하는 동영상 목록을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-143">The movies key represents the list of movies displayed by the Index view page.</span></span>

<span data-ttu-id="1dab2-144">또한 Details() 작업 범주 및 동영상 라는 두 개의 키를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-144">The Details() action also adds two keys named categories and movies.</span></span> <span data-ttu-id="1dab2-145">범주 키에는 다시 한 번 영화 범주 보기 마스터 페이지에서 표시 된 목록을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-145">The categories key, once again, represents the list of movie categories displayed by the view master page.</span></span> <span data-ttu-id="1dab2-146">영화 키 세부 정보 보기 페이지에서 표시를 특정 범주에는 동영상 목록을 나타냅니다 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="1dab2-146">The movies key represents the list of movies in a particular category displayed by the Details view page (see Figure 2).</span></span>


<span data-ttu-id="1dab2-147">[![세부 정보 보기](passing-data-to-view-master-pages-cs/_static/image5.png)](passing-data-to-view-master-pages-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="1dab2-147">[![The Details view](passing-data-to-view-master-pages-cs/_static/image5.png)](passing-data-to-view-master-pages-cs/_static/image4.png)</span></span>

<span data-ttu-id="1dab2-148">**그림 02**: 세부 정보 보기 ([전체 크기 이미지를 보려면 클릭](passing-data-to-view-master-pages-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="1dab2-148">**Figure 02**: The Details view ([Click to view full-size image](passing-data-to-view-master-pages-cs/_static/image6.png))</span></span>


<span data-ttu-id="1dab2-149">인덱스 뷰 목록 2에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-149">The Index view is contained in Listing 2.</span></span> <span data-ttu-id="1dab2-150">단순히 데이터 보기에서에서 영화 항목으로 표시 하는 동영상 목록을 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-150">It simply iterates through the list of movies represented by the movies item in view data.</span></span>

<span data-ttu-id="1dab2-151">**2 – 나열 `Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="1dab2-151">**Listing 2 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](passing-data-to-view-master-pages-cs/samples/sample2.aspx)]

<span data-ttu-id="1dab2-152">마스터 페이지 보기는 보기 3에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-152">The view master page is contained in Listing 3.</span></span> <span data-ttu-id="1dab2-153">마스터 페이지 보기 반복 하 고 모든 데이터 보기에서에서 범주 항목이 나타내는 영화 범주를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-153">The view master page iterates and renders all of the movie categories represented by the categories item from view data.</span></span>

<span data-ttu-id="1dab2-154">**3 – 나열 `Views\Shared\Site.master`**</span><span class="sxs-lookup"><span data-stu-id="1dab2-154">**Listing 3 – `Views\Shared\Site.master`**</span></span>

[!code-aspx[Main](passing-data-to-view-master-pages-cs/samples/sample3.aspx)]

<span data-ttu-id="1dab2-155">모든 데이터 보기와 보기의 마스터 페이지에 데이터 보기를 통해 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-155">All data is passed to the view and the view master page through view data.</span></span> <span data-ttu-id="1dab2-156">마스터 페이지에 데이터를 전달 하는 올바른 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-156">That is the correct way to pass data to the master page.</span></span>

<span data-ttu-id="1dab2-157">따라서이 솔루션과 이유가 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="1dab2-157">So, what's wrong with this solution?</span></span> <span data-ttu-id="1dab2-158">문제는이 솔루션 (하지 반복 직접) 드라이 원칙을 위반 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-158">The problem is that this solution violates the DRY (Don't Repeat Yourself) principle.</span></span> <span data-ttu-id="1dab2-159">각 컨트롤러 작업 동일한 데이터를 보려면 영화 범주 목록에 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-159">Each and every controller action must add the very same list of movie categories to view data.</span></span> <span data-ttu-id="1dab2-160">중복 되는 코드를 응용 프로그램에 두면 응용 프로그램 유지 관리 하 고 적용, 수정 하기가 훨씬 더 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-160">Having duplicate code in your application makes your application much more difficult to maintain, adapt, and modify.</span></span>

### <a name="the-good-solution"></a><span data-ttu-id="1dab2-161">적합 한 솔루션</span><span class="sxs-lookup"><span data-stu-id="1dab2-161">The Good Solution</span></span>

<span data-ttu-id="1dab2-162">이 섹션에서는 뷰 마스터 페이지에는 컨트롤러 작업에서 데이터를 전달 하는 대체를 하 고, 더 나은 솔루션을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-162">In this section, we examine an alternative, and better, solution to passing data from a controller action to a view master page.</span></span> <span data-ttu-id="1dab2-163">각 컨트롤러 작업에서 마스터 페이지에 대 한 동영상 범주를 추가 하는 대신 추가 영화 범주 뷰 데이터를 한 번만 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-163">Instead of adding the movie categories for the master page in each and every controller action, we add the movie categories to the view data only once.</span></span> <span data-ttu-id="1dab2-164">데이터 뷰 마스터 페이지에서 사용 하는 모든 보기 응용 프로그램 컨트롤러에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-164">All view data used by the view master page is added in an Application controller.</span></span>

<span data-ttu-id="1dab2-165">ApplicationController 클래스 목록 4에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-165">The ApplicationController class is contained in Listing 4.</span></span>

<span data-ttu-id="1dab2-166">**4 – 나열 `Controllers\ApplicationController.cs`**</span><span class="sxs-lookup"><span data-stu-id="1dab2-166">**Listing 4 – `Controllers\ApplicationController.cs`**</span></span>

[!code-csharp[Main](passing-data-to-view-master-pages-cs/samples/sample4.cs)]

<span data-ttu-id="1dab2-167">다음 세 가지 목록 4에 응용 프로그램 컨트롤러에 대 한 확인할 수 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-167">There are three things that you should notice about the Application controller in Listing 4.</span></span> <span data-ttu-id="1dab2-168">클래스의 기본 System.Web.Mvc.Controller 클래스에서 상속 되는 첫 번째, 알림 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-168">First, notice that the class inherits from the base System.Web.Mvc.Controller class.</span></span> <span data-ttu-id="1dab2-169">응용 프로그램 컨트롤러는 컨트롤러 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-169">The Application controller is a controller class.</span></span>

<span data-ttu-id="1dab2-170">둘째, 응용 프로그램 컨트롤러 클래스는 추상 클래스를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-170">Second, notice that the Application controller class is an abstract class.</span></span> <span data-ttu-id="1dab2-171">추상 클래스는 구체적 클래스에 의해 구현 되어야 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-171">An abstract class is a class that must be implemented by a concrete class.</span></span> <span data-ttu-id="1dab2-172">응용 프로그램 컨트롤러 클래스는 추상 클래스를 때문에는 클래스에 직접 정의 하는 메서드를 호출할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-172">Because the Application controller is an abstract class, you cannot not invoke any methods defined in the class directly.</span></span> <span data-ttu-id="1dab2-173">응용 프로그램 클래스를 직접 호출 하려고 하면 다음 메시지가 표시 됩니다는 리소스를 찾을 수 없는 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-173">If you attempt to invoke the Application class directly then you'll get a Resource Cannot Be Found error message.</span></span>

<span data-ttu-id="1dab2-174">셋째, 데이터를 보려면 영화 범주 목록에 추가 하는 생성자는 응용 프로그램 컨트롤러에 포함 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-174">Third, notice that the Application controller contains a constructor that adds the list of movie categories to view data.</span></span> <span data-ttu-id="1dab2-175">응용 프로그램 컨트롤러에서 상속 되는 모든 컨트롤러 클래스는 자동으로 응용 프로그램 컨트롤러의 생성자를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-175">Every controller class that inherits from the Application controller calls the Application controller's constructor automatically.</span></span> <span data-ttu-id="1dab2-176">응용 프로그램 컨트롤러에서 상속 되는 모든 컨트롤러에서 모든 작업을 호출할 때마다 영화 범주 뷰 데이터에 자동으로 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-176">Whenever you call any action on any controller that inherits from the Application controller, the movie categories is included in the view data automatically.</span></span>

<span data-ttu-id="1dab2-177">영화 컨트롤러 목록 5에는 응용 프로그램 컨트롤러에서 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-177">The Movies controller in Listing 5 inherits from the Application controller.</span></span>

<span data-ttu-id="1dab2-178">**5-나열 `Controllers\MoviesController.cs`**</span><span class="sxs-lookup"><span data-stu-id="1dab2-178">**Listing 5 – `Controllers\MoviesController.cs`**</span></span>

[!code-csharp[Main](passing-data-to-view-master-pages-cs/samples/sample5.cs)]

<span data-ttu-id="1dab2-179">라는 두 개의 작업 메서드를 노출 하는 이전 섹션에서 설명한 Home 컨트롤러와 마찬가지로 영화 컨트롤러 `Index()` 및 `Details()`합니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-179">The Movies controller, just like the Home controller discussed in the previous section, exposes two action methods named `Index()` and `Details()`.</span></span> <span data-ttu-id="1dab2-180">공지 보기 마스터 페이지에서 표시 하는 영화 범주 목록에는 없는 추가 중 하나에서 데이터를 볼는 `Index()` 또는 `Details()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="1dab2-180">Notice that the list of movie categories displayed by the view master page is not added to view data in either the `Index()` or `Details()` method.</span></span> <span data-ttu-id="1dab2-181">영화 컨트롤러 응용 프로그램 컨트롤러에서 상속 하기 때문에 동영상 범주 목록 데이터를 자동으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-181">Because the Movies controller inherits from the Application controller, the list of movie categories is added to view data automatically.</span></span>

<span data-ttu-id="1dab2-182">공지 보기 마스터 페이지에 대 한 뷰 데이터를 추가 하도록이 솔루션 (하지 반복 직접) 드라이 원칙을 위반 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-182">Notice that this solution to adding view data for a view master page does not violate the DRY (Don't Repeat Yourself) principle.</span></span> <span data-ttu-id="1dab2-183">하나의 위치에 포함 된 데이터를 보려면 영화 범주 목록에 추가 하기 위한 코드: 응용 프로그램 컨트롤러에 대 한 생성자입니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-183">The code for adding the list of movie categories to view data is contained in only one location: the constructor for the Application controller.</span></span>

### <a name="summary"></a><span data-ttu-id="1dab2-184">요약</span><span class="sxs-lookup"><span data-stu-id="1dab2-184">Summary</span></span>

<span data-ttu-id="1dab2-185">이 자습서에서는 뷰 마스터 페이지에는 컨트롤러에서 뷰 데이터를 전달 하는 두 가지 방법에 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-185">In this tutorial, we discussed two approaches to passing view data from a controller to a view master page.</span></span> <span data-ttu-id="1dab2-186">첫째, 접근 방식을 어려워질 수 있지만 간단한을 검사 했습니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-186">First, we examined a simple, but difficult to maintain approach.</span></span> <span data-ttu-id="1dab2-187">첫 번째 섹션에서는 응용 프로그램에서 각 모든 컨트롤러 동작의 뷰 마스터 페이지에 대 한 데이터 보기를 추가할 수는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-187">In the first section, we discussed how you can add view data for a view master page in each every controller action in your application.</span></span> <span data-ttu-id="1dab2-188">이 잘못 된 접근 방식 (하지 반복 직접) 드라이 원칙을 위반 하기 때문에 결론을 내렸습니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-188">We concluded that this was a bad approach because it violates the DRY (Don't Repeat Yourself) principle.</span></span>

<span data-ttu-id="1dab2-189">다음으로 데이터를 보려면 보기 마스터 페이지에서 필요한 데이터를 추가 하는 데 훨씬 더 좋은 전략을 검사 했습니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-189">Next, we examined a much better strategy for adding data required by a view master page to view data.</span></span> <span data-ttu-id="1dab2-190">각 컨트롤러 작업에서 데이터 보기를 추가 하는 대신 응용 프로그램 컨트롤러 내에서 한 번만 뷰 데이터를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-190">Instead of adding the view data in each and every controller action, we added the view data only once within an Application controller.</span></span> <span data-ttu-id="1dab2-191">이런 방식으로 ASP.NET MVC 응용 프로그램의 뷰 마스터 페이지에 데이터를 전달 하는 경우 코드 중복을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dab2-191">That way, you can avoid duplicate code when passing data to a view master page in an ASP.NET MVC application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1dab2-192">[이전](creating-page-layouts-with-view-master-pages-cs.md)
> [다음](asp-net-mvc-views-overview-vb.md)</span><span class="sxs-lookup"><span data-stu-id="1dab2-192">[Previous](creating-page-layouts-with-view-master-pages-cs.md)
[Next](asp-net-mvc-views-overview-vb.md)</span></span>
