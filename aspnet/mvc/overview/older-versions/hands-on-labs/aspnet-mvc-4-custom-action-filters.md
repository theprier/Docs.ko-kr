---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters
title: ASP.NET MVC 4 사용자 지정 작업 필터 | Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 이전 또는 작업 메서드가 호출 된 후 필터링 논리를 실행 하기 위한 작업 필터를 제공 합니다. 작업 필터는 사용자 지정 특성 tha 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: 969ab824-1b98-4552-81fe-b60ef5fc6887
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters
msc.type: authoredcontent
ms.openlocfilehash: 8b135b23aea64b0c7c7d4368eef9ee80914159e4
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="aspnet-mvc-4-custom-action-filters"></a><span data-ttu-id="4ee70-104">ASP.NET MVC 4 사용자 지정 작업 필터</span><span class="sxs-lookup"><span data-stu-id="4ee70-104">ASP.NET MVC 4 Custom Action Filters</span></span>

<span data-ttu-id="4ee70-105">으로 [웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="4ee70-105">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="4ee70-106">웹 캠프 학습 키트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="4ee70-107">ASP.NET MVC 이전 또는 작업 메서드가 호출 된 후 필터링 논리를 실행 하기 위한 작업 필터를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-107">ASP.NET MVC provides Action Filters for executing filtering logic either before or after an action method is called.</span></span> <span data-ttu-id="4ee70-108">작업 필터는 이전 및 이후 작업의 동작을 추가할 컨트롤러의 작업 메서드에 선언적 수단을 제공 하는 사용자 지정 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-108">Action Filters are custom attributes that provide declarative means to add pre-action and post-action behavior to the controller's action methods.</span></span>

<span data-ttu-id="4ee70-109">이 실습 랩에서 MvcMusicStore 컨트롤러의 요청을 catch 하 고 데이터베이스 테이블에는 사이트의 활동을 기록 하는 솔루션에 사용자 지정 작업 필터 특성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-109">In this Hands-on Lab you will create a custom action filter attribute into MvcMusicStore solution to catch controller's requests and log the activity of a site into a database table.</span></span> <span data-ttu-id="4ee70-110">모든 컨트롤러 또는 동작에 삽입 하 여 로깅 필터를 추가할 수 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-110">You will be able to add your logging filter by injection to any controller or action.</span></span> <span data-ttu-id="4ee70-111">마지막으로 방문자의 목록을 보여 주는 로그 보기를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-111">Finally, you will see the log view that shows the list of visitors.</span></span>

<span data-ttu-id="4ee70-112">이 실습 랩 대 한 기본 지식이 있다고 가정 하 고 **ASP.NET MVC**합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-112">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC**.</span></span> <span data-ttu-id="4ee70-113">사용 하지 않은 경우 **ASP.NET MVC** 를 권장 앞, **ASP.NET MVC 4 기초** 실습 랩입니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-113">If you have not used **ASP.NET MVC** before, we recommend you to go over **ASP.NET MVC 4 Fundamentals** Hands-on Lab.</span></span>

> [!NOTE]
> <span data-ttu-id="4ee70-114">모든 샘플 코드와 코드 조각을 웹 캠프 교육 키트에서 사용할 수에 포함 된 [Microsoft-웹/WebCampTrainingKit 릴리스](https://aka.ms/webcamps-training-kit)합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-114">All sample code and snippets are included in the Web Camps Training Kit, available from at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="4ee70-115">이 랩에 특정 프로젝트에서 사용할 수는 [ASP.NET MVC 4 사용자 지정 작업 필터](https://github.com/Microsoft-Web/HOL-MVC4CustomActionFilters)합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-115">The project specific to this lab is available at [ASP.NET MVC 4 Custom Action Filters](https://github.com/Microsoft-Web/HOL-MVC4CustomActionFilters).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="4ee70-116">목표</span><span class="sxs-lookup"><span data-stu-id="4ee70-116">Objectives</span></span>

<span data-ttu-id="4ee70-117">이 실습 랩에서 배우게 됩니다 하는 방법:</span><span class="sxs-lookup"><span data-stu-id="4ee70-117">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="4ee70-118">필터링 기능을 확장 하는 사용자 지정 작업 필터 특성 만들기</span><span class="sxs-lookup"><span data-stu-id="4ee70-118">Create a custom action filter attribute to extend filtering capabilities</span></span>
- <span data-ttu-id="4ee70-119">특정 수준으로 삽입 하 여 사용자 지정 필터 특성을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-119">Apply a custom filter attribute by injection to a specific level</span></span>
- <span data-ttu-id="4ee70-120">사용자 지정 작업 필터를 전역으로 등록</span><span class="sxs-lookup"><span data-stu-id="4ee70-120">Register a custom action filters globally</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="4ee70-121">전제 조건</span><span class="sxs-lookup"><span data-stu-id="4ee70-121">Prerequisites</span></span>

<span data-ttu-id="4ee70-122">이 랩을 완료 하려면 다음 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-122">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="4ee70-123">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) 하거나 그 보다 뛰어난 (읽기 [부록 A](#AppendixA) 설치 하는 방법에 대 한 지침은).</span><span class="sxs-lookup"><span data-stu-id="4ee70-123">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="4ee70-124">설정</span><span class="sxs-lookup"><span data-stu-id="4ee70-124">Setup</span></span>

<span data-ttu-id="4ee70-125">**설치 하는 코드 조각**</span><span class="sxs-lookup"><span data-stu-id="4ee70-125">**Installing Code Snippets**</span></span>

<span data-ttu-id="4ee70-126">편의 위해는이 랩에 따라 관리 코드의 대부분 Visual Studio 코드 조각 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-126">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="4ee70-127">실행 코드 조각을 설치 하려면 **.\Source\Setup\CodeSnippets.vsi** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-127">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="4ee70-128">이 문서에서 부록을 참조할 수 사용 하는 방법에 알아봅니다 사용 하 고 Visual Studio 코드 조각에 익숙한 경우 &quot; [부록 c:를 사용 하 여 코드 조각을](#AppendixC)&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-128">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix C: Using Code Snippets](#AppendixC)&quot;.</span></span>

* * *

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="4ee70-129">연습</span><span class="sxs-lookup"><span data-stu-id="4ee70-129">Exercises</span></span>

<span data-ttu-id="4ee70-130">이 실습 랩에서 다음 연습으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-130">This Hands-On Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="4ee70-131">연습 1: 로깅 작업</span><span class="sxs-lookup"><span data-stu-id="4ee70-131">Exercise 1: Logging actions</span></span>](#Exercise1)
2. [<span data-ttu-id="4ee70-132">연습 2: 여러 작업 필터 관리</span><span class="sxs-lookup"><span data-stu-id="4ee70-132">Exercise 2: Managing Multiple Action Filters</span></span>](#Exercise2)

<span data-ttu-id="4ee70-133">예상 소요 시간: **30 분**합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-133">Estimated time to complete this lab: **30 minutes**.</span></span>

> [!NOTE]
> <span data-ttu-id="4ee70-134">각 연습 동반 되는 **끝** 연습을 완료 한 후 가져와야 생성 되는 솔루션에 포함 된 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-134">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="4ee70-135">연습을 통해 작업 하는 추가 도움이 필요한 경우이 솔루션 가이드로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-135">You can use this solution as a guide if you need additional help working through the exercises.</span></span>


<a id="Exercise1"></a>

<a id="Exercise_1_Logging_Actions"></a>
### <a name="exercise-1-logging-actions"></a><span data-ttu-id="4ee70-136">연습 1: 로깅 작업</span><span class="sxs-lookup"><span data-stu-id="4ee70-136">Exercise 1: Logging Actions</span></span>

<span data-ttu-id="4ee70-137">이 연습에서는 ASP.NET MVC 4 필터 공급자를 사용 하 여 사용자 지정 작업 로그 필터를 만드는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-137">In this exercise, you will learn how to create a custom action log filter by using ASP.NET MVC 4 Filter Providers.</span></span> <span data-ttu-id="4ee70-138">포함 하기 위해 선택한 컨트롤러의 모든 활동을 기록 하며 됩니다 MusicStore 사이트로 로깅 필터를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-138">For that purpose you will apply a logging filter to the MusicStore site that will record all the activities in the selected controllers.</span></span>

<span data-ttu-id="4ee70-139">필터를 확장 하면 **ActionFilterAttributeClass** 재정의 **OnActionExecuting** 메서드에서를 각 요청을 catch 한 다음 로깅 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-139">The filter will extend **ActionFilterAttributeClass** and override **OnActionExecuting** method to catch each request and then perform the logging actions.</span></span> <span data-ttu-id="4ee70-140">HTTP 요청에 대 한 컨텍스트 정보를 실행 하는 메서드, 결과 및 매개 변수에서 제공 합니다 ASP.NET MVC **ActionExecutingContext** 클래스 **합니다.**</span><span class="sxs-lookup"><span data-stu-id="4ee70-140">The context information about HTTP requests, executing methods, results and parameters will be provided by ASP.NET MVC **ActionExecutingContext** class **.**</span></span>

> [!NOTE]
> <span data-ttu-id="4ee70-141">ASP.NET MVC 4에는 기본 필터 공급자는 사용자 지정 필터를 만들지 않고 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-141">ASP.NET MVC 4 also has default filters providers you can use without creating a custom filter.</span></span> <span data-ttu-id="4ee70-142">ASP.NET MVC 4에서는 다음 유형의 필터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-142">ASP.NET MVC 4 provides the following types of filters:</span></span>
> 
> - <span data-ttu-id="4ee70-143">**권한 부여** 필터링, 같은 인증을 수행 또는 요청의 속성을 확인 하는 동작 메서드를 실행 하는 여부에 대 한 보안 결정 수 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-143">**Authorization** filter, which makes security decisions about whether to execute an action method, such as performing authentication or validating properties of the request.</span></span>
> - <span data-ttu-id="4ee70-144">**동작** 작업 메서드 실행 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-144">**Action** filter, which wraps the action method execution.</span></span> <span data-ttu-id="4ee70-145">이 필터는 동작 메서드에 추가 데이터를 제공, 반환 값 검사 또는 작업 메서드 실행을 취소 하는 등의 추가 프로세스를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-145">This filter can perform additional processing, such as providing extra data to the action method, inspecting the return value, or canceling execution of the action method</span></span>
> - <span data-ttu-id="4ee70-146">**결과** ActionResult 개체 실행의 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-146">**Result** filter, which wraps execution of the ActionResult object.</span></span> <span data-ttu-id="4ee70-147">이 필터는 결과 HTTP 응답을 수정 하는 등의 추가 처리를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-147">This filter can perform additional processing of the result, such as modifying the HTTP response.</span></span>
> - <span data-ttu-id="4ee70-148">**예외** 권한 부여 필터와 시작점과 결과의 실행 동작 메서드에서 어딘가에 발생 하는 처리 되지 않은 예외 경우에 실행 하는 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-148">**Exception** filter, which executes if there is an unhandled exception thrown somewhere in action method, starting with the authorization filters and ending with the execution of the result.</span></span> <span data-ttu-id="4ee70-149">로깅 또는 오류 페이지 표시 등의 작업에 대 한 예외 필터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-149">Exception filters can be used for tasks such as logging or displaying an error page.</span></span>
> 
> <span data-ttu-id="4ee70-150">필터 공급자에 대 한 자세한 내용은 MSDN 링크를 방문 하십시오. ([https://msdn.microsoft.com/library/dd410209.aspx](https://msdn.microsoft.com/library/dd410209.aspx)).</span><span class="sxs-lookup"><span data-stu-id="4ee70-150">For more information about Filters Providers please visit this MSDN link: ([https://msdn.microsoft.com/library/dd410209.aspx](https://msdn.microsoft.com/library/dd410209.aspx)) .</span></span>


<a id="AboutLoggingFeature"></a>

<a id="About_MVC_Music_Store_Application_logging_feature"></a>
#### <a name="about-mvc-music-store-application-logging-feature"></a><span data-ttu-id="4ee70-151">MVC 음악 스토어 응용 프로그램 로깅 기능에 대 한</span><span class="sxs-lookup"><span data-stu-id="4ee70-151">About MVC Music Store Application logging feature</span></span>

<span data-ttu-id="4ee70-152">이 Music Store 솔루션은 사이트 로깅에 대 한 새 데이터 모델 테이블 **ActionLog**, 다음 필드: 요청, 작업 호출, 클라이언트 IP 및 타임 스탬프를 수신 하는 컨트롤러의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-152">This Music Store solution has a new data model table for site logging, **ActionLog**, with the following fields: Name of the controller that received a request, Called action, Client IP and Time stamp.</span></span>

<span data-ttu-id="4ee70-153">![데이터 모델입니다. ActionLog 테이블입니다. ] (aspnet-mvc-4-custom-action-filters/_static/image1.png "데이터 모델입니다. ActionLog 테이블입니다.")</span><span class="sxs-lookup"><span data-stu-id="4ee70-153">![Data model. ActionLog table.](aspnet-mvc-4-custom-action-filters/_static/image1.png "Data model. ActionLog table.")</span></span>

<span data-ttu-id="4ee70-154">*데이터 모델-ActionLog 테이블*</span><span class="sxs-lookup"><span data-stu-id="4ee70-154">*Data model - ActionLog table*</span></span>

<span data-ttu-id="4ee70-155">솔루션에서 찾을 수 있는 작업 로그에 대 한 ASP.NET MVC 뷰를 제공 **MvcMusicStores/뷰/ActionLog**:</span><span class="sxs-lookup"><span data-stu-id="4ee70-155">The solution provides an ASP.NET MVC View for the Action log that can be found at **MvcMusicStores/Views/ActionLog**:</span></span>

<span data-ttu-id="4ee70-156">![작업 로그 보기](aspnet-mvc-4-custom-action-filters/_static/image2.png "작업 로그 보기")</span><span class="sxs-lookup"><span data-stu-id="4ee70-156">![Action Log view](aspnet-mvc-4-custom-action-filters/_static/image2.png "Action Log view")</span></span>

<span data-ttu-id="4ee70-157">*작업 로그 보기*</span><span class="sxs-lookup"><span data-stu-id="4ee70-157">*Action Log view*</span></span>

<span data-ttu-id="4ee70-158">이 구조를 제공 하는 모든 작업 컨트롤러의 요청을 중단 하 고 사용자 지정 필터링을 사용 하 여 로깅을 수행에 집중 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-158">With this given structure, all the work will be focused on interrupting controller's request and performing the logging by using custom filtering.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_a_Custom_Filter_to_Catch_a_Controllers_Request"></a>
#### <a name="task-1---creating-a-custom-filter-to-catch-a-controllers-request"></a><span data-ttu-id="4ee70-159">작업 1-컨트롤러의 요청을 Catch 하는 사용자 지정 필터 만들기</span><span class="sxs-lookup"><span data-stu-id="4ee70-159">Task 1 - Creating a Custom Filter to Catch a Controller's Request</span></span>

<span data-ttu-id="4ee70-160">이 작업의 로깅 논리를 포함 하는 사용자 지정 필터 특성 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-160">In this task you will create a custom filter attribute class that will contain the logging logic.</span></span> <span data-ttu-id="4ee70-161">ASP.NET MVC를 확장 하면 해당 용도로 **ActionFilterAttribute** 클래스 및 인터페이스 구현 **IActionFilter**합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-161">For that purpose you will extend ASP.NET MVC **ActionFilterAttribute** Class and implement the interface **IActionFilter**.</span></span>

> [!NOTE]
> <span data-ttu-id="4ee70-162">**ActionFilterAttribute** 는 모든 특성 필터에 대 한 기본 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-162">The **ActionFilterAttribute** is the base class for all the attribute filters.</span></span> <span data-ttu-id="4ee70-163">컨트롤러 동작 실행 전과 후에 특정 논리를 실행 하기 위해 다음 메서드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-163">It provides the following methods to execute a specific logic after and before controller action's execution:</span></span>
> 
> - <span data-ttu-id="4ee70-164">**OnActionExecuting**(ActionExecutingContext filterContext): 작업 바로 전에 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-164">**OnActionExecuting**(ActionExecutingContext filterContext): Just before the action method is called.</span></span>
> - <span data-ttu-id="4ee70-165">**OnActionExecuted**(ActionExecutedContext filterContext): 작업 메서드를 호출한 후 및 결과 보기 렌더링) (이전 실행 되기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-165">**OnActionExecuted**(ActionExecutedContext filterContext): After the action method is called and before the result is executed (before view render).</span></span>
> - <span data-ttu-id="4ee70-166">**OnResultExecuting**(ResultExecutingContext filterContext): (이전 뷰 렌더링) 결과 실행 하기 전에 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-166">**OnResultExecuting**(ResultExecutingContext filterContext): Just before the result is executed (before view render).</span></span>
> - <span data-ttu-id="4ee70-167">**OnResultExecuted**(ResultExecutedContext filterContext): (뷰를 렌더링할) 후 결과 실행 한 후입니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-167">**OnResultExecuted**(ResultExecutedContext filterContext): After the result is executed (after the view is rendered).</span></span>
> 
> <span data-ttu-id="4ee70-168">다음이 방법 중 하나 파생된 클래스에 재정의 함으로써 필터링 코드를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-168">By overriding any of these methods into a derived class, you can execute your own filtering code.</span></span>


1. <span data-ttu-id="4ee70-169">열기는 **시작** 솔루션에 있는 **\Source\Ex01-LoggingActions\Begin** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-169">Open the **Begin** solution located at **\Source\Ex01-LoggingActions\Begin** folder.</span></span>

   1. <span data-ttu-id="4ee70-170">계속 하기 전에 몇 가지 누락 된 NuGet 패키지를 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-170">You will need to download some missing NuGet packages before you continue.</span></span> <span data-ttu-id="4ee70-171">이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-171">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="4ee70-172">에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="4ee70-172">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="4ee70-173">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-173">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="4ee70-174">NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-174">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="4ee70-175">NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-175">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="4ee70-176">이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-176">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
      > 
      > <span data-ttu-id="4ee70-177">자세한 내용은이 문서를 참조 하십시오.: [ http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages ](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-177">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="4ee70-178">에 새 C# 클래스를 추가 **필터** 폴더 이름을 지정 *CustomActionFilter.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-178">Add a new C# class into the **Filters** folder and name it *CustomActionFilter.cs*.</span></span> <span data-ttu-id="4ee70-179">이 폴더는 모든 사용자 지정 필터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-179">This folder will store all the custom filters.</span></span>
3. <span data-ttu-id="4ee70-180">열기 **CustomActionFilter.cs** 에 대 한 참조를 추가 하 고 **System.Web.Mvc** 및 **MvcMusicStore.Models** 네임 스페이스:</span><span class="sxs-lookup"><span data-stu-id="4ee70-180">Open **CustomActionFilter.cs** and add a reference to **System.Web.Mvc** and **MvcMusicStore.Models** namespaces:</span></span>

    <span data-ttu-id="4ee70-181">(코드 조각- *ASP.NET MVC 4 사용자 지정 작업 필터-e x 1 CustomActionFilterNamespaces*)</span><span class="sxs-lookup"><span data-stu-id="4ee70-181">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex1-CustomActionFilterNamespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample1.cs)]
4. <span data-ttu-id="4ee70-182">상속 된 **CustomActionFilter** 에서 클래스 **ActionFilterAttribute** 다음 **CustomActionFilter** 클래스 구현 **IActionFilter** 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-182">Inherit the **CustomActionFilter** class from **ActionFilterAttribute** and then make **CustomActionFilter** class implement **IActionFilter** interface.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample2.cs)]
5. <span data-ttu-id="4ee70-183">확인 **CustomActionFilter** 클래스 메서드를 재정의 **OnActionExecuting** 고 필터의 실행을 기록 하는 데 필요한 논리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-183">Make **CustomActionFilter** class override the method **OnActionExecuting** and add the necessary logic to log the filter's execution.</span></span> <span data-ttu-id="4ee70-184">이 위해 내에서 강조 표시 된 다음 코드를 추가 **CustomActionFilter** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-184">To do this, add the following highlighted code within **CustomActionFilter** class.</span></span>

    <span data-ttu-id="4ee70-185">(코드 조각- *ASP.NET MVC 4 사용자 지정 작업 필터-e x 1 LoggingActions*)</span><span class="sxs-lookup"><span data-stu-id="4ee70-185">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex1-LoggingActions*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample3.cs#Highlight)]

    > [!NOTE]
    > <span data-ttu-id="4ee70-186">**OnActionExecuting** 메서드를 사용 하 여 **Entity Framework** 새 ActionLog 레지스터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-186">**OnActionExecuting** method is using **Entity Framework** to add a new ActionLog register.</span></span> <span data-ttu-id="4ee70-187">작성 하는 컨텍스트 정보로 새 엔터티 인스턴스에 **filterContext**합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-187">It creates and fills a new entity instance with the context information from **filterContext**.</span></span>
    > 
    > <span data-ttu-id="4ee70-188">에 대 한 자세한 내용은 **ControllerContext** 에 클래스 [msdn](https://msdn.microsoft.com/library/system.web.mvc.controllercontext.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-188">You can read more about **ControllerContext** class at [msdn](https://msdn.microsoft.com/library/system.web.mvc.controllercontext.aspx).</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Injecting_a_Code_Interceptor_into_the_Store_Controller_Class"></a>
#### <a name="task-2---injecting-a-code-interceptor-into-the-store-controller-class"></a><span data-ttu-id="4ee70-189">작업 2-저장소 컨트롤러 클래스에 코드 인터셉터 삽입</span><span class="sxs-lookup"><span data-stu-id="4ee70-189">Task 2 - Injecting a Code Interceptor into the Store Controller Class</span></span>

<span data-ttu-id="4ee70-190">이 작업에서 모든 컨트롤러 클래스 및 로그온할지 컨트롤러 작업에 삽입 하 여 사용자 지정 필터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-190">In this task you will add the custom filter by injecting it to all controller classes and controller actions that will be logged.</span></span> <span data-ttu-id="4ee70-191">이 연습에서는 저장소 컨트롤러 클래스는 로그를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-191">For the purpose of this exercise, the Store Controller class will have a log.</span></span>

<span data-ttu-id="4ee70-192">메서드가 **OnActionExecuting** 에서 **ActionLogFilterAttribute** 삽입 된 요소를 호출할 때 사용자 지정 필터를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-192">The method **OnActionExecuting** from **ActionLogFilterAttribute** custom filter runs when an injected element is called.</span></span>

<span data-ttu-id="4ee70-193">특정 컨트롤러 메서드를 가로채도 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-193">It is also possible to intercept a specific controller method.</span></span>

1. <span data-ttu-id="4ee70-194">열기는 **StoreController** 에서 **MvcMusicStore\Controllers** 에 대 한 참조를 추가 하 고는 **필터** 네임 스페이스:</span><span class="sxs-lookup"><span data-stu-id="4ee70-194">Open the **StoreController** at **MvcMusicStore\Controllers** and add a reference to the **Filters** namespace:</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample4.cs)]
2. <span data-ttu-id="4ee70-195">사용자 지정 필터를 주입 **CustomActionFilter** 에 **StoreController** 클래스를 추가 하 여 **[CustomActionFilter]** 특성 클래스 선언 앞입니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-195">Inject the custom filter **CustomActionFilter** into **StoreController** class by adding **[CustomActionFilter]** attribute before the class declaration.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample5.cs)]

   > [!NOTE]
   > <span data-ttu-id="4ee70-196">필터는 컨트롤러 클래스에 주입 된, 모든 작업은 삽입도 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-196">When a filter is injected into a controller class, all its actions are also injected.</span></span> <span data-ttu-id="4ee70-197">삽입 해야 일련의 동작에 대해서만 필터를 적용 하려는 경우 **[CustomActionFilter]** 중 각각에:</span><span class="sxs-lookup"><span data-stu-id="4ee70-197">If you would like to apply the filter only for a set of actions, you would have to inject **[CustomActionFilter]** to each one of them:</span></span>
   > 
   > [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample6.cs)]

<a id="Ex1Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="4ee70-198">작업 3-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="4ee70-198">Task 3 - Running the Application</span></span>

<span data-ttu-id="4ee70-199">이 태스크에서는 로깅 필터 작동 하는지 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-199">In this task, you will test that the logging filter is working.</span></span> <span data-ttu-id="4ee70-200">응용 프로그램 시작 되며,에서 스토어를 방문 하 고 기록 된 활동을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-200">You will start the application and visit the store, and then you will check logged activities.</span></span>

1. <span data-ttu-id="4ee70-201">**F5** 키를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-201">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="4ee70-202">찾아 **/ActionLog** 로그 보기 초기 상태를 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-202">Browse to **/ActionLog** to see log view initial state:</span></span>

    <span data-ttu-id="4ee70-203">![로그 페이지 작업 이전 상태 추적기](aspnet-mvc-4-custom-action-filters/_static/image3.png "로그 페이지 작업 전에 추적 장치 상태")</span><span class="sxs-lookup"><span data-stu-id="4ee70-203">![Log tracker status before page activity](aspnet-mvc-4-custom-action-filters/_static/image3.png "Log tracker status before page activity")</span></span>

    <span data-ttu-id="4ee70-204">*페이지 작업 이전 로그 추적 장치 상태*</span><span class="sxs-lookup"><span data-stu-id="4ee70-204">*Log tracker status before page activity*</span></span>

   > [!NOTE]
   > <span data-ttu-id="4ee70-205">기본적으로 한 항목의 메뉴에 대 한 기존 장르를 검색할 때 생성 되는 항상 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-205">By default, it will always show one item that is generated when retrieving the existing genres for the menu.</span></span>
   > 
   > <span data-ttu-id="4ee70-206">단순성을 위해를 정리 하 우리는 **ActionLog** 는 각 특정 작업의 확인의 로그 데이터만 표시 하도록 응용 프로그램이 실행 될 때마다 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-206">For simplicity purposes we're cleaning up the **ActionLog** table each time the application runs so it will only show the logs of each particular task's verification.</span></span>
   > 
   > <span data-ttu-id="4ee70-207">파일에서 다음 코드를 제거 해야 할 수는 **세션\_시작** 메서드 (에 **Global.asax** 클래스), 저장소 내에서 실행 되는 모든 작업에 대 한 기록 로그를 저장 하려면 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-207">You might need to remove the following code from the **Session\_Start** method (in the **Global.asax** class), in order to save an historical log for all the actions executed within the Store Controller.</span></span>
   > 
   > [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample7.cs)]
3. <span data-ttu-id="4ee70-208">중 하나를 클릭는 **장르** 메뉴에서 사용할 수 있는 앨범 화, 일부 작업을 수행 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-208">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
4. <span data-ttu-id="4ee70-209">찾아 **/ActionLog** 로그 빈 키를 눌러가 고 **F5** 페이지를 새로 고칠 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-209">Browse to **/ActionLog** and if the log is empty press **F5** to refresh the page.</span></span> <span data-ttu-id="4ee70-210">프로그램 환자가 내 원 추적 된 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-210">Check that your visits were tracked:</span></span>

    <span data-ttu-id="4ee70-211">![기록 된 동작을 사용 하 여 작업 로그](aspnet-mvc-4-custom-action-filters/_static/image4.png "기록 된 동작을 사용 하 여 작업 로그")</span><span class="sxs-lookup"><span data-stu-id="4ee70-211">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image4.png "Action log with activity logged")</span></span>

    <span data-ttu-id="4ee70-212">*기록 된 동작을 사용 하 여 작업 로그*</span><span class="sxs-lookup"><span data-stu-id="4ee70-212">*Action log with activity logged*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Managing_Multiple_Action_Filters"></a>
### <a name="exercise-2-managing-multiple-action-filters"></a><span data-ttu-id="4ee70-213">연습 2: 여러 작업 필터 관리</span><span class="sxs-lookup"><span data-stu-id="4ee70-213">Exercise 2: Managing Multiple Action Filters</span></span>

<span data-ttu-id="4ee70-214">이 연습에서는 StoreController 클래스에 두 번째 사용자 지정 작업 필터를 추가 하 고 두 필터가 모두 실행할 수 있는 특정 순서를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-214">In this exercise you will add a second Custom Action Filter to the StoreController class and define the specific order in which both filters will be executed.</span></span> <span data-ttu-id="4ee70-215">그런 다음 필터를 전역으로 등록 하는 코드를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-215">Then you will update the code to register the filter Globally.</span></span>

<span data-ttu-id="4ee70-216">필터의 실행 순서를 정의할 때 고려해 야 할 다른 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-216">There are different options to take into account when defining the Filters' execution order.</span></span> <span data-ttu-id="4ee70-217">예를 들어 Order 속성 및 필터 범위:</span><span class="sxs-lookup"><span data-stu-id="4ee70-217">For example, the Order property and the Filters' scope:</span></span>

<span data-ttu-id="4ee70-218">정의할 수는 **범위** 각 필터에 대 한 예를 들어 수 범위 내에서 실행 하는 모든 작업 필터는 **컨트롤러 범위**, 및에서 실행 되도록 모든 권한 부여 필터 **전역 범위** .</span><span class="sxs-lookup"><span data-stu-id="4ee70-218">You can define a **Scope** for each of the Filters, for example, you could scope all the Action Filters to run within the **Controller Scope**, and all Authorization Filters to run in **Global scope**.</span></span> <span data-ttu-id="4ee70-219">범위에 정의 된 실행 순서는 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-219">The scopes have a defined execution order.</span></span>

<span data-ttu-id="4ee70-220">또한 각 작업 필터는 필터의 범위에서 실행 순서를 결정 하는 데 사용 되는 순서 속성을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-220">Additionally, each action filter has an Order property which is used to determine the execution order in the scope of the filter.</span></span>

<span data-ttu-id="4ee70-221">사용자 지정 작업 필터 실행 순서에 대 한 자세한 내용은이 MSDN 문서를 참조 하십시오. ([https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx](https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx)).</span><span class="sxs-lookup"><span data-stu-id="4ee70-221">For more information about Custom Action Filters execution order, please visit this MSDN article: ([https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx](https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx)).</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_Creating_a_new_Custom_Action_Filter"></a>
#### <a name="task-1-creating-a-new-custom-action-filter"></a><span data-ttu-id="4ee70-222">태스크 1: 새 사용자 지정 작업 필터 만들기</span><span class="sxs-lookup"><span data-stu-id="4ee70-222">Task 1: Creating a new Custom Action Filter</span></span>

<span data-ttu-id="4ee70-223">이 태스크에서는 만들어집니다 StoreController 클래스에 삽입할 새 사용자 지정 작업 필터는 필터의 실행 순서를 관리 하는 방법에 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-223">In this task, you will create a new Custom Action Filter to inject into the StoreController class, learning how to manage the execution order of the filters.</span></span>

1. <span data-ttu-id="4ee70-224">열기는 **시작** 솔루션에 있는 **\Source\Ex02-ManagingMultipleActionFilters\Begin** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-224">Open the **Begin** solution located at **\Source\Ex02-ManagingMultipleActionFilters\Begin** folder.</span></span> <span data-ttu-id="4ee70-225">그렇지 않은 경우 계속 사용할 수도 있습니다는 **끝** 솔루션, 이전 연습을 완료 하 여 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-225">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

    1. <span data-ttu-id="4ee70-226">제공 된 연 경우 **시작** 를 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 솔루션을 계속 하려면.</span><span class="sxs-lookup"><span data-stu-id="4ee70-226">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="4ee70-227">이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-227">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="4ee70-228">에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="4ee70-228">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
    3. <span data-ttu-id="4ee70-229">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-229">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

        > [!NOTE]
        > <span data-ttu-id="4ee70-230">NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-230">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="4ee70-231">NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-231">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="4ee70-232">이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-232">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
        > 
        > <span data-ttu-id="4ee70-233">자세한 내용은이 문서를 참조 하십시오.: [ http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages ](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-233">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="4ee70-234">에 새 C# 클래스를 추가 **필터** 폴더 이름을 지정 *MyNewCustomActionFilter.cs*</span><span class="sxs-lookup"><span data-stu-id="4ee70-234">Add a new C# class into the **Filters** folder and name it *MyNewCustomActionFilter.cs*</span></span>
3. <span data-ttu-id="4ee70-235">열기 **MyNewCustomActionFilter.cs** 에 대 한 참조를 추가 하 고 **System.Web.Mvc** 및 **MvcMusicStore.Models** 네임 스페이스:</span><span class="sxs-lookup"><span data-stu-id="4ee70-235">Open **MyNewCustomActionFilter.cs** and add a reference to **System.Web.Mvc** and the **MvcMusicStore.Models** namespace:</span></span>

    <span data-ttu-id="4ee70-236">(코드 조각- *ASP.NET MVC 4 사용자 지정 작업 필터-e x 2 MyNewCustomActionFilterNamespaces*)</span><span class="sxs-lookup"><span data-stu-id="4ee70-236">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex2-MyNewCustomActionFilterNamespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample8.cs)]
4. <span data-ttu-id="4ee70-237">기본 클래스 선언을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-237">Replace the default class declaration with the following code.</span></span>

    <span data-ttu-id="4ee70-238">(코드 조각- *ASP.NET MVC 4 사용자 지정 작업 필터-e x 2 MyNewCustomActionFilterClass*)</span><span class="sxs-lookup"><span data-stu-id="4ee70-238">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex2-MyNewCustomActionFilterClass*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample9.cs)]

    > [!NOTE]
    > <span data-ttu-id="4ee70-239">이 사용자 지정 작업 필터는 이전 연습에서 만든 것 보다 거의 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-239">This Custom Action Filter is almost the same than the one you created in the previous exercise.</span></span> <span data-ttu-id="4ee70-240">주요 차이점은 있다는 *&quot;기록 하 여&quot;* wich 필터를 식별 하는이 새 클래스의이 이름으로 업데이트 하는 특성의 로그를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-240">The main difference is that it has the *&quot;Logged By&quot;* attribute updated with this new class' name to identify wich filter registered the log.</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_Injecting_a_new_Code_Interceptor_into_the_StoreController_Class"></a>
#### <a name="task-2-injecting-a-new-code-interceptor-into-the-storecontroller-class"></a><span data-ttu-id="4ee70-241">작업 2: StoreController 클래스에 새 코드 인터셉터 삽입</span><span class="sxs-lookup"><span data-stu-id="4ee70-241">Task 2: Injecting a new Code Interceptor into the StoreController Class</span></span>

<span data-ttu-id="4ee70-242">이 태스크에서는 StoreController 클래스에 새 사용자 지정 필터를를 추가 하 고 확인 방법을 두 필터는 함께 작동 하도록 솔루션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-242">In this task, you will add a new custom filter into the StoreController Class and run the solution to verify how both filters work together.</span></span>

1. <span data-ttu-id="4ee70-243">열기는 **StoreController** 클래스에 있는 **MvcMusicStore\Controllers** 새 사용자 지정 필터를 삽입 하 고 **MyNewCustomActionFilter** 에  **StoreController** 와 같은 클래스는 다음 코드에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-243">Open the **StoreController** class located at **MvcMusicStore\Controllers** and inject the new custom filter **MyNewCustomActionFilter** into **StoreController** class like is shown in the following code.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample10.cs)]
2. <span data-ttu-id="4ee70-244">이제 이러한 두 사용자 지정 작업 필터 어떻게 표시 되는지 확인 하려면 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-244">Now, run the application in order to see how these two Custom Action Filters work.</span></span> <span data-ttu-id="4ee70-245">이 작업을 수행 하려면 키를 누릅니다 **F5** 응용 프로그램이 시작 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-245">To do this, press **F5** and wait until the application starts.</span></span>
3. <span data-ttu-id="4ee70-246">찾아 **/ActionLog** 로그 보기 초기 상태를 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-246">Browse to **/ActionLog** to see log view initial state.</span></span>

    <span data-ttu-id="4ee70-247">![로그 페이지 작업 이전 상태 추적기](aspnet-mvc-4-custom-action-filters/_static/image5.png "로그 페이지 작업 전에 추적 장치 상태")</span><span class="sxs-lookup"><span data-stu-id="4ee70-247">![Log tracker status before page activity](aspnet-mvc-4-custom-action-filters/_static/image5.png "Log tracker status before page activity")</span></span>

    <span data-ttu-id="4ee70-248">*페이지 작업 이전 로그 추적 장치 상태*</span><span class="sxs-lookup"><span data-stu-id="4ee70-248">*Log tracker status before page activity*</span></span>
4. <span data-ttu-id="4ee70-249">중 하나를 클릭는 **장르** 메뉴에서 사용할 수 있는 앨범 화, 일부 작업을 수행 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-249">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
5. <span data-ttu-id="4ee70-250">이 시간; 있는지 여부를 확인합니다 따라 방문 두 번 추적 된:에서 추가 사용자 지정 작업 필터의 각 면의 **StorageController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-250">Check that this time; your visits were tracked twice: once for each of the Custom Action Filters you added in the **StorageController** class.</span></span>

    <span data-ttu-id="4ee70-251">![기록 된 동작을 사용 하 여 작업 로그](aspnet-mvc-4-custom-action-filters/_static/image6.png "기록 된 동작을 사용 하 여 작업 로그")</span><span class="sxs-lookup"><span data-stu-id="4ee70-251">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image6.png "Action log with activity logged")</span></span>

    <span data-ttu-id="4ee70-252">*기록 된 동작을 사용 하 여 작업 로그*</span><span class="sxs-lookup"><span data-stu-id="4ee70-252">*Action log with activity logged*</span></span>
6. <span data-ttu-id="4ee70-253">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-253">Close the browser.</span></span>

<a id="Ex2Task3"></a>

<a id="Task_3_Managing_Filter_Ordering"></a>
#### <a name="task-3-managing-filter-ordering"></a><span data-ttu-id="4ee70-254">작업 3: 필터 순서 관리</span><span class="sxs-lookup"><span data-stu-id="4ee70-254">Task 3: Managing Filter Ordering</span></span>

<span data-ttu-id="4ee70-255">이 작업 순서 속성을 사용 하 여 필터 실행 순서를 관리 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-255">In this task, you will learn how to manage the filters' execution order by using the Order propery.</span></span>

1. <span data-ttu-id="4ee70-256">열기는 **StoreController** 클래스에 있는 **MvcMusicStore\Controllers** 지정는 **순서** 속성 필터 둘 모두에 같은 아래에 표시 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-256">Open the **StoreController** class located at **MvcMusicStore\Controllers** and specify the **Order** property in both filters like shown below.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample11.cs)]
2. <span data-ttu-id="4ee70-257">이제, 해당 순서 속성의 값에 따라 필터는 실행 하는 방법을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-257">Now, verify how the filters are executed depending on its Order property's value.</span></span> <span data-ttu-id="4ee70-258">필터에서 가장 작은 값으로 볼 수 있습니다 (**CustomActionFilter**)이 실행 되는 첫 번째 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-258">You will find that the filter with the smallest Order value (**CustomActionFilter**) is the first one that is executed.</span></span> <span data-ttu-id="4ee70-259">키를 눌러 **F5** 응용 프로그램이 시작 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-259">Press **F5** and wait until the application starts.</span></span>
3. <span data-ttu-id="4ee70-260">찾아 **/ActionLog** 로그 보기 초기 상태를 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-260">Browse to **/ActionLog** to see log view initial state.</span></span>

    <span data-ttu-id="4ee70-261">![로그 페이지 작업 이전 상태 추적기](aspnet-mvc-4-custom-action-filters/_static/image7.png "로그 페이지 작업 전에 추적 장치 상태")</span><span class="sxs-lookup"><span data-stu-id="4ee70-261">![Log tracker status before page activity](aspnet-mvc-4-custom-action-filters/_static/image7.png "Log tracker status before page activity")</span></span>

    <span data-ttu-id="4ee70-262">*페이지 작업 이전 로그 추적 장치 상태*</span><span class="sxs-lookup"><span data-stu-id="4ee70-262">*Log tracker status before page activity*</span></span>
4. <span data-ttu-id="4ee70-263">중 하나를 클릭는 **장르** 메뉴에서 사용할 수 있는 앨범 화, 일부 작업을 수행 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-263">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
5. <span data-ttu-id="4ee70-264">필터의 순서 값에 따라 정렬 하는이 이번에 따라 방문 추적 된 확인: **CustomActionFilter** 로그의 첫 번째입니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-264">Check that this time, your visits were tracked ordered by the filters' Order value: **CustomActionFilter** logs' first.</span></span>

    <span data-ttu-id="4ee70-265">![기록 된 동작을 사용 하 여 작업 로그](aspnet-mvc-4-custom-action-filters/_static/image8.png "기록 된 동작을 사용 하 여 작업 로그")</span><span class="sxs-lookup"><span data-stu-id="4ee70-265">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image8.png "Action log with activity logged")</span></span>

    <span data-ttu-id="4ee70-266">*기록 된 동작을 사용 하 여 작업 로그*</span><span class="sxs-lookup"><span data-stu-id="4ee70-266">*Action log with activity logged*</span></span>
6. <span data-ttu-id="4ee70-267">이제 필터의 순서 값을 업데이트 한 로깅 순서 어떻게 변경 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-267">Now, you will update the Filters' order value and verify how the logging order changes.</span></span> <span data-ttu-id="4ee70-268">에 **StoreController** 클래스 아래에 표시 된 순서 값이 필터를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-268">In the **StoreController** class, update the Filters' Order value like shown below.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample12.cs)]
7. <span data-ttu-id="4ee70-269">키를 눌러 응용 프로그램을 다시 실행 **F5**합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-269">Run the application again by pressing **F5**.</span></span>
8. <span data-ttu-id="4ee70-270">중 하나를 클릭는 **장르** 메뉴에서 사용할 수 있는 앨범 화, 일부 작업을 수행 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-270">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
9. <span data-ttu-id="4ee70-271">이 이번에는 로그를 만들었음을 확인 **MyNewCustomActionFilter** 필터가 가장 먼저 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-271">Check that this time, the logs created by **MyNewCustomActionFilter** filter appears first.</span></span>

    <span data-ttu-id="4ee70-272">![기록 된 동작을 사용 하 여 작업 로그](aspnet-mvc-4-custom-action-filters/_static/image9.png "기록 된 동작을 사용 하 여 작업 로그")</span><span class="sxs-lookup"><span data-stu-id="4ee70-272">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image9.png "Action log with activity logged")</span></span>

    <span data-ttu-id="4ee70-273">*기록 된 동작을 사용 하 여 작업 로그*</span><span class="sxs-lookup"><span data-stu-id="4ee70-273">*Action log with activity logged*</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_Registering_Filters_Globally"></a>
#### <a name="task-4-registering-filters-globally"></a><span data-ttu-id="4ee70-274">작업 4: 전역 필터 등록</span><span class="sxs-lookup"><span data-stu-id="4ee70-274">Task 4: Registering Filters Globally</span></span>

<span data-ttu-id="4ee70-275">이 태스크에서는 새 필터를 등록 하려면 솔루션을 업데이트 합니다 (**MyNewCustomActionFilter**)를 글로벌 필터로 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-275">In this task, you will update the solution to register the new filter (**MyNewCustomActionFilter**) as a global filter.</span></span> <span data-ttu-id="4ee70-276">이 작업을 수행 하 여 이전 태스크에서와 같이 StoreController 것 뿐만 아니라 응용 프로그램에 모든 작업 perfomed로 실행 될 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-276">By doing this, it will be triggered by all the actions perfomed in the application and not only in the StoreController ones as in the previous task.</span></span>

1. <span data-ttu-id="4ee70-277">**StoreController** 클래스, 제거 **[MyNewCustomActionFilter]** 특성 및 순서 속성에서 **[CustomActionFilter]**합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-277">In **StoreController** class, remove **[MyNewCustomActionFilter]** attribute and the order property from **[CustomActionFilter]**.</span></span> <span data-ttu-id="4ee70-278">다음과 같은 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-278">It should look like the following:</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample13.cs)]
2. <span data-ttu-id="4ee70-279">열기 **Global.asax** 파일를 찾습니다는 **응용 프로그램\_시작** 메서드.</span><span class="sxs-lookup"><span data-stu-id="4ee70-279">Open **Global.asax** file and locate the **Application\_Start** method.</span></span> <span data-ttu-id="4ee70-280">표시 될 때마다 응용 프로그램 시작 됨이 호출 하 여 전역 필터 등록 **RegisterGlobalFilters** 메서드 내에서 **FilterConfig** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-280">Notice that each time the application starts it is registering the global filters by calling **RegisterGlobalFilters** method within **FilterConfig** class.</span></span>

    <span data-ttu-id="4ee70-281">![전역 필터 Global.asax에 등록](aspnet-mvc-4-custom-action-filters/_static/image10.png "전역 필터 Global.asax에 등록 하는 중")</span><span class="sxs-lookup"><span data-stu-id="4ee70-281">![Registering Global Filters in Global.asax](aspnet-mvc-4-custom-action-filters/_static/image10.png "Registering Global Filters in Global.asax")</span></span>

    <span data-ttu-id="4ee70-282">*전역 필터 Global.asax에 등록 하는 중*</span><span class="sxs-lookup"><span data-stu-id="4ee70-282">*Registering Global Filters in Global.asax*</span></span>
3. <span data-ttu-id="4ee70-283">열기 **FilterConfig.cs** 내에 파일이 **앱\_시작** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-283">Open **FilterConfig.cs** file within **App\_Start** folder.</span></span>
4. <span data-ttu-id="4ee70-284">System.Web.Mvc;를 사용 하 여에 대 한 참조를 추가 합니다. MvcMusicStore.Filters;를 사용 하 여 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-284">Add a reference to using System.Web.Mvc; using MvcMusicStore.Filters; namespace.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample14.cs)]
5. <span data-ttu-id="4ee70-285">업데이트 **RegisterGlobalFilters** 메서드를 사용자 지정 필터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-285">Update **RegisterGlobalFilters** method adding your custom filter.</span></span> <span data-ttu-id="4ee70-286">이 작업을 수행 하려면 강조 표시 된 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-286">To do this, add the highlighted code:</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample15.cs)]
6. <span data-ttu-id="4ee70-287">키를 눌러 응용 프로그램을 실행 **F5**합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-287">Run the application by pressing **F5**.</span></span>
7. <span data-ttu-id="4ee70-288">중 하나를 클릭는 **장르** 메뉴에서 사용할 수 있는 앨범 화, 일부 작업을 수행 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-288">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
8. <span data-ttu-id="4ee70-289">이제 검사 **[MyNewCustomActionFilter]** 너무 HomeController 및 ActionLogController에 주입 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-289">Check that now **[MyNewCustomActionFilter]** is being injected in HomeController and ActionLogController too.</span></span>

    <span data-ttu-id="4ee70-290">![기록 된 동작을 사용 하 여 작업 로그](aspnet-mvc-4-custom-action-filters/_static/image11.png "기록 된 동작을 사용 하 여 작업 로그")</span><span class="sxs-lookup"><span data-stu-id="4ee70-290">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image11.png "Action log with activity logged")</span></span>

    <span data-ttu-id="4ee70-291">*전역 작업 로그를 사용 하 여 작업 로그*</span><span class="sxs-lookup"><span data-stu-id="4ee70-291">*Action log with global activity logged*</span></span>

> [!NOTE]
> <span data-ttu-id="4ee70-292">다음 Windows Azure 웹 사이트에이 응용 프로그램을 배포할 수는 또한 [부록 b: 게시 웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램](#AppendixB)합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-292">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>


* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="4ee70-293">요약</span><span class="sxs-lookup"><span data-stu-id="4ee70-293">Summary</span></span>

<span data-ttu-id="4ee70-294">이 실습 랩을 완료 하 여 사용자 지정 작업을 실행 하는 작업 필터를 확장 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-294">By completing this Hands-On Lab you have learned how to extend an action filter to execute custom actions.</span></span> <span data-ttu-id="4ee70-295">또한 페이지 컨트롤러에 필터를 주입 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-295">You have also learned how to inject any filter to your page controllers.</span></span> <span data-ttu-id="4ee70-296">다음과 같은 개념 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-296">The following concepts were used:</span></span>

- <span data-ttu-id="4ee70-297">ASP.NET MVC ActionFilterAttribute 클래스를 사용자 지정 작업 필터를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="4ee70-297">How to create Custom Action filters with the ASP.NET MVC ActionFilterAttribute class</span></span>
- <span data-ttu-id="4ee70-298">ASP.NET MVC 컨트롤러에 필터를 삽입 하는 방법</span><span class="sxs-lookup"><span data-stu-id="4ee70-298">How to inject filters into ASP.NET MVC controllers</span></span>
- <span data-ttu-id="4ee70-299">필터 순서 속성을 사용 하 여 순서를 관리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="4ee70-299">How to manage filter ordering using the Order property</span></span>
- <span data-ttu-id="4ee70-300">필터를 전역으로 등록 하는 방법</span><span class="sxs-lookup"><span data-stu-id="4ee70-300">How to register filters globally</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="4ee70-301">부록 a: 설치 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="4ee70-301">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="4ee70-302">설치할 수 있습니다 **Microsoft Visual Studio Express 2012 for Web** 또는 다른 &quot;Express&quot; 버전을 사용 하 여 **[Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="4ee70-302">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="4ee70-303">다음 지침을 설치 하는 데 필요한 단계를 안내 하 *Visual studio Express 2012 for Web* 를 사용 하 여 *Microsoft 웹 플랫폼 설치 관리자*합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-303">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="4ee70-304">로 이동 [ [ https://go.microsoft.com/? linkid = 9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-304">Go to [[https://go.microsoft.com/? linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="4ee70-305">또는 이미 설치 된 웹 플랫폼 설치 관리자를 열 수 있습니다 및 제품에 대 한 검색 &quot; <em>Visual Studio Express 2012 for Web Windows Azure SDK와</em>&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-305">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="4ee70-306">클릭 **지금 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-306">Click on **Install Now**.</span></span> <span data-ttu-id="4ee70-307">없는 경우 **웹 플랫폼 설치 관리자** 를 다운로드 하 여 앱을 먼저 설치 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-307">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="4ee70-308">한 번 **웹 플랫폼 설치 관리자** 열려 클릭 **설치** 는 설치 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-308">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="4ee70-309">![Visual Studio Express 설치](aspnet-mvc-4-custom-action-filters/_static/image12.png "Visual Studio Express 설치")</span><span class="sxs-lookup"><span data-stu-id="4ee70-309">![Install Visual Studio Express](aspnet-mvc-4-custom-action-filters/_static/image12.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="4ee70-310">*Visual Studio Express 설치*</span><span class="sxs-lookup"><span data-stu-id="4ee70-310">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="4ee70-311">모든 제품의 라이선스 및 용어를 읽고 클릭 **동의** 를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-311">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![사용 조건 동의](aspnet-mvc-4-custom-action-filters/_static/image13.png)

    <span data-ttu-id="4ee70-313">*사용 조건 동의*</span><span class="sxs-lookup"><span data-stu-id="4ee70-313">*Accepting the license terms*</span></span>
5. <span data-ttu-id="4ee70-314">다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-314">Wait until the downloading and installation process completes.</span></span>

    ![설치 진행률](aspnet-mvc-4-custom-action-filters/_static/image14.png)

    <span data-ttu-id="4ee70-316">*설치 진행률*</span><span class="sxs-lookup"><span data-stu-id="4ee70-316">*Installation progress*</span></span>
6. <span data-ttu-id="4ee70-317">설치가 완료 되 면 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-317">When the installation completes, click **Finish**.</span></span>

    ![설치 완료](aspnet-mvc-4-custom-action-filters/_static/image15.png)

    <span data-ttu-id="4ee70-319">*설치 완료*</span><span class="sxs-lookup"><span data-stu-id="4ee70-319">*Installation completed*</span></span>
7. <span data-ttu-id="4ee70-320">클릭 **종료** 를 웹 플랫폼 설치 관리자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-320">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="4ee70-321">Visual Studio Express for Web을 열려면로 이동는 **시작** 화면를 쓰기 시작할 &quot; **VS Express**&quot;, 클릭는 **VS Express for Web** 바둑판식 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-321">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![웹 타일에 대 한 VS Express](aspnet-mvc-4-custom-action-filters/_static/image16.png)

    <span data-ttu-id="4ee70-323">*웹 타일에 대 한 VS Express*</span><span class="sxs-lookup"><span data-stu-id="4ee70-323">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="4ee70-324">부록 b: 웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="4ee70-324">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="4ee70-325">이 부록에서는 Windows Azure 관리 포털에서 새 웹 사이트를 만들고 Windows Azure에서 제공 하는 웹 배포 게시 기능을 활용 하기 위해 랩에서 수행 하 여 가져온 응용 프로그램을 게시 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-325">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="4ee70-326">작업 1-Windows에서 새 웹 사이트를 만드는 Azure 포털</span><span class="sxs-lookup"><span data-stu-id="4ee70-326">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="4ee70-327">이동 하 여 [Windows Azure 관리 포털](https://manage.windowsazure.com/) 구독에 연결 된 Microsoft 자격 증명을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-327">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4ee70-328">Windows Azure를 무료로 10 개 ASP.NET 웹 사이트를 호스트 하 고 트래픽이 증가 됨을 확장 한 다음 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-328">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="4ee70-329">등록할 수 [여기](http://aka.ms/aspnet-hol-azure)합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-329">You can sign up [here](http://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="4ee70-330">![Windows Azure 포털에 로그온](aspnet-mvc-4-custom-action-filters/_static/image17.png "Windows Azure 포털에 로그인")</span><span class="sxs-lookup"><span data-stu-id="4ee70-330">![Log on to Windows Azure portal](aspnet-mvc-4-custom-action-filters/_static/image17.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="4ee70-331">*Windows Azure 관리 포털에 로그온*</span><span class="sxs-lookup"><span data-stu-id="4ee70-331">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="4ee70-332">클릭 **새로** 명령 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-332">Click **New** on the command bar.</span></span>

    <span data-ttu-id="4ee70-333">![새 웹 사이트를 만드는](aspnet-mvc-4-custom-action-filters/_static/image18.png "새 웹 사이트 만들기")</span><span class="sxs-lookup"><span data-stu-id="4ee70-333">![Creating a new Web Site](aspnet-mvc-4-custom-action-filters/_static/image18.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="4ee70-334">*새 웹 사이트 만들기*</span><span class="sxs-lookup"><span data-stu-id="4ee70-334">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="4ee70-335">클릭 **계산** | **웹 사이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-335">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="4ee70-336">그런 다음 선택 **빠른 생성** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-336">Then select **Quick Create** option.</span></span> <span data-ttu-id="4ee70-337">새 웹 사이트에 대 한 사용 가능한 URL을 입력 하 고 클릭 **웹 사이트 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-337">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4ee70-338">Windows Azure 웹 사이트는 호스트를 제어 하 고 관리할 수 있는 클라우드에서 실행 되는 웹 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-338">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="4ee70-339">빨리 만들기 옵션을 사용 하면 완성 된 웹 응용 프로그램을 Windows Azure 웹 사이트에서 포털 외부에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-339">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="4ee70-340">데이터베이스를 설정 하기 위한 단계는 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-340">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="4ee70-341">![빠른 생성을 사용 하 여 새 웹 사이트를 만드는](aspnet-mvc-4-custom-action-filters/_static/image19.png "빠른 생성을 사용 하 여 새 웹 사이트 만들기")</span><span class="sxs-lookup"><span data-stu-id="4ee70-341">![Creating a new Web Site using Quick Create](aspnet-mvc-4-custom-action-filters/_static/image19.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="4ee70-342">*빠른 생성을 사용 하 여 새 웹 사이트 만들기*</span><span class="sxs-lookup"><span data-stu-id="4ee70-342">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="4ee70-343">새 될 때까지 기다렸다가 **웹 사이트** 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-343">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="4ee70-344">웹 사이트가 만들어지면 아래 링크를 클릭 하 고 **URL** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-344">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="4ee70-345">새 웹 사이트가 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-345">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="4ee70-346">![새 웹 사이트를 찾아](aspnet-mvc-4-custom-action-filters/_static/image20.png "새 웹 사이트를 검색 합니다.")</span><span class="sxs-lookup"><span data-stu-id="4ee70-346">![Browsing to the new web site](aspnet-mvc-4-custom-action-filters/_static/image20.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="4ee70-347">*새 웹 사이트를 검색합니다.*</span><span class="sxs-lookup"><span data-stu-id="4ee70-347">*Browsing to the new web site*</span></span>

    <span data-ttu-id="4ee70-348">![실행 중인 웹 사이트](aspnet-mvc-4-custom-action-filters/_static/image21.png "실행 중인 웹 사이트")</span><span class="sxs-lookup"><span data-stu-id="4ee70-348">![Web site running](aspnet-mvc-4-custom-action-filters/_static/image21.png "Web site running")</span></span>

    <span data-ttu-id="4ee70-349">*실행 중인 웹 사이트*</span><span class="sxs-lookup"><span data-stu-id="4ee70-349">*Web site running*</span></span>
6. <span data-ttu-id="4ee70-350">포털로 돌아가서 아래에서 웹 사이트의 이름을 클릭는 **이름** 관리 페이지를 표시 하는 열입니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-350">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="4ee70-351">![웹 사이트 관리 페이지 열기](aspnet-mvc-4-custom-action-filters/_static/image22.png "웹 사이트 관리 페이지 열기")</span><span class="sxs-lookup"><span data-stu-id="4ee70-351">![Opening the web site management pages](aspnet-mvc-4-custom-action-filters/_static/image22.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="4ee70-352">*웹 사이트 관리 페이지 열기*</span><span class="sxs-lookup"><span data-stu-id="4ee70-352">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="4ee70-353">에 **대시보드** 페이지의 **눈에 보는** 섹션에서 클릭는 **게시 프로필 다운로드** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-353">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4ee70-354">*게시 프로필* 각각의 활성화 된 게시 방법에 대 한 Windows Azure 웹 사이트에 웹 응용 프로그램을 게시 하는 데 필요한 정보가 모두 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-354">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="4ee70-355">게시 프로필에는 Url, 사용자 자격 증명 및 연결 하 고 각 게시 메서드를 사용할 수 있는 끝점에 대해 인증 하는 데 필요한 데이터베이스 문자열이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-355">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="4ee70-356">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** 및 **Microsoft Visual Studio 2012** 읽는 지원 하기 위해 게시 프로필에 대 한 이러한 프로그램의 구성을 자동화 Windows Azure 웹 사이트에 웹 응용 프로그램을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-356">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="4ee70-357">![게시 프로필 다운로드 웹 사이트](aspnet-mvc-4-custom-action-filters/_static/image23.png "게시 프로필 다운로드 웹 사이트")</span><span class="sxs-lookup"><span data-stu-id="4ee70-357">![Downloading the web site publish profile](aspnet-mvc-4-custom-action-filters/_static/image23.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="4ee70-358">*게시 프로필 다운로드 웹 사이트*</span><span class="sxs-lookup"><span data-stu-id="4ee70-358">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="4ee70-359">알려진된 위치에 게시 프로필 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-359">Download the publish profile file to a known location.</span></span> <span data-ttu-id="4ee70-360">더 이상이 연습에서는 Visual Studio에서 웹 응용 프로그램 Windows Azure 웹 사이트를 게시 하려면이 파일을 사용 하는 방법을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-360">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="4ee70-361">![게시 프로필 파일을 저장](aspnet-mvc-4-custom-action-filters/_static/image24.png "게시 프로필 저장")</span><span class="sxs-lookup"><span data-stu-id="4ee70-361">![Saving the publish profile file](aspnet-mvc-4-custom-action-filters/_static/image24.png "Saving the publish profile")</span></span>

    <span data-ttu-id="4ee70-362">*게시 프로필 파일을 저장합니다.*</span><span class="sxs-lookup"><span data-stu-id="4ee70-362">*Saving the publish profile file*</span></span>

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="4ee70-363">작업 2-데이터베이스 서버 구성</span><span class="sxs-lookup"><span data-stu-id="4ee70-363">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="4ee70-364">응용 프로그램에서 SQL Server를 활용 하는 경우 데이터베이스를 SQL 데이터베이스 서버 만들기 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-364">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="4ee70-365">SQL Server를 사용 하지 않는 간단한 응용 프로그램을 배포 하려는 경우이 태스크를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-365">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="4ee70-366">응용 프로그램 데이터베이스를 저장 하기 위해 SQL 데이터베이스 서버를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-366">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="4ee70-367">Windows Azure 관리 포털에서 구독의 SQL 데이터베이스 서버를 볼 수 있습니다 **Sql 데이터베이스** | **서버** | **서버 대시보드**합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-367">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="4ee70-368">만든 서버 없는 경우 수행 하 여 만들 수 있습니다는 **추가** 명령 모음에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-368">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="4ee70-369">기록해는 **서버 이름 및 URL, 관리자 로그인 이름 및 암호**, 다음 작업에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-369">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="4ee70-370">만들지 마십시오 데이터베이스 아직 대로 이후 단계에서 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-370">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="4ee70-371">![SQL 데이터베이스 서버 대시보드](aspnet-mvc-4-custom-action-filters/_static/image25.png "SQL 데이터베이스 서버 대시보드")</span><span class="sxs-lookup"><span data-stu-id="4ee70-371">![SQL Database Server Dashboard](aspnet-mvc-4-custom-action-filters/_static/image25.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="4ee70-372">*SQL 데이터베이스 서버 대시보드*</span><span class="sxs-lookup"><span data-stu-id="4ee70-372">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="4ee70-373">다음 태스크에서는 서버 목록에 사용자의 로컬 IP 주소를 포함 해야 이러한 이유로 Visual Studio에서 데이터베이스 연결을 테스트 **허용 IP 주소**합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-373">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="4ee70-374">작업을 수행 하려면 **구성**에서 IP 주소를 선택 **현재 클라이언트 IP 주소** 에 붙여넣습니다는 **시작 IP 주소** 및 **끝IP주소** 클릭 하 고 텍스트 상자는 ![add-client-ip-address-ok-button](aspnet-mvc-4-custom-action-filters/_static/image26.png) 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-374">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](aspnet-mvc-4-custom-action-filters/_static/image26.png) button.</span></span>

    ![클라이언트 IP 주소를 추가합니다.](aspnet-mvc-4-custom-action-filters/_static/image27.png)

    <span data-ttu-id="4ee70-376">*클라이언트 IP 주소를 추가합니다.*</span><span class="sxs-lookup"><span data-stu-id="4ee70-376">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="4ee70-377">한 번는 **클라이언트 IP 주소** 허용된 된 IP 주소에 추가 됩니다 목록에서 클릭 **저장** 하 여 변경 사항을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-377">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![변경 확인](aspnet-mvc-4-custom-action-filters/_static/image28.png)

    <span data-ttu-id="4ee70-379">*변경 확인*</span><span class="sxs-lookup"><span data-stu-id="4ee70-379">*Confirm Changes*</span></span>

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="4ee70-380">작업 3-웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="4ee70-380">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="4ee70-381">ASP.NET MVC 4 솔루션으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-381">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="4ee70-382">에 **솔루션 탐색기**웹 사이트 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-382">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="4ee70-383">![응용 프로그램을 게시](aspnet-mvc-4-custom-action-filters/_static/image29.png "응용 프로그램을 게시")</span><span class="sxs-lookup"><span data-stu-id="4ee70-383">![Publishing the Application](aspnet-mvc-4-custom-action-filters/_static/image29.png "Publishing the Application")</span></span>

    <span data-ttu-id="4ee70-384">*웹 사이트를 게시*</span><span class="sxs-lookup"><span data-stu-id="4ee70-384">*Publishing the web site*</span></span>
2. <span data-ttu-id="4ee70-385">첫 번째 작업에서 저장 한 게시 프로필을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-385">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="4ee70-386">![게시 프로필 가져오기](aspnet-mvc-4-custom-action-filters/_static/image30.png "게시 프로필 가져오기")</span><span class="sxs-lookup"><span data-stu-id="4ee70-386">![Importing the publish profile](aspnet-mvc-4-custom-action-filters/_static/image30.png "Importing the publish profile")</span></span>

    <span data-ttu-id="4ee70-387">*게시 프로필 가져오기*</span><span class="sxs-lookup"><span data-stu-id="4ee70-387">*Importing publish profile*</span></span>
3. <span data-ttu-id="4ee70-388">클릭 **연결 확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-388">Click **Validate Connection**.</span></span> <span data-ttu-id="4ee70-389">유효성 검사가 완료 되 면 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-389">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4ee70-390">연결 유효성 검사 단추 옆에 표시 녹색 확인 표시가 표시 되 면 유효성 검사가 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-390">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="4ee70-391">![연결 유효성 검사](aspnet-mvc-4-custom-action-filters/_static/image31.png "연결 유효성 검사")</span><span class="sxs-lookup"><span data-stu-id="4ee70-391">![Validating connection](aspnet-mvc-4-custom-action-filters/_static/image31.png "Validating connection")</span></span>

    <span data-ttu-id="4ee70-392">*연결 유효성 검사*</span><span class="sxs-lookup"><span data-stu-id="4ee70-392">*Validating connection*</span></span>
4. <span data-ttu-id="4ee70-393">에 **설정** 페이지의 **데이터베이스** 섹션에서 데이터베이스 연결의 텍스트 상자 옆의 단추 클릭 (즉, **DefaultConnection**).</span><span class="sxs-lookup"><span data-stu-id="4ee70-393">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="4ee70-394">![웹 배포 구성](aspnet-mvc-4-custom-action-filters/_static/image32.png "웹 배포 구성")</span><span class="sxs-lookup"><span data-stu-id="4ee70-394">![Web deploy configuration](aspnet-mvc-4-custom-action-filters/_static/image32.png "Web deploy configuration")</span></span>

    <span data-ttu-id="4ee70-395">*웹 배포 구성*</span><span class="sxs-lookup"><span data-stu-id="4ee70-395">*Web deploy configuration*</span></span>
5. <span data-ttu-id="4ee70-396">다음과 같이 데이터베이스 연결을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-396">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="4ee70-397">에 **서버 이름** SQL 데이터베이스 서버 URL 사용 하 여 입력 된 *tcp:* 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-397">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="4ee70-398">**사용자 이름** 서버 관리자 로그인 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-398">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="4ee70-399">**암호** 서버 관리자 로그인 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-399">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="4ee70-400">새 데이터베이스 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-400">Type a new database name.</span></span>

     <span data-ttu-id="4ee70-401">![대상 연결 문자열 구성](aspnet-mvc-4-custom-action-filters/_static/image33.png "대상 연결 문자열 구성")</span><span class="sxs-lookup"><span data-stu-id="4ee70-401">![Configuring destination connection string](aspnet-mvc-4-custom-action-filters/_static/image33.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="4ee70-402">*대상 연결 문자열 구성*</span><span class="sxs-lookup"><span data-stu-id="4ee70-402">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="4ee70-403">그런 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-403">Then click **OK**.</span></span> <span data-ttu-id="4ee70-404">데이터베이스를 만들려는 대화 상자가 나타나면 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-404">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="4ee70-405">![데이터베이스를 만드는](aspnet-mvc-4-custom-action-filters/_static/image34.png "데이터베이스 문자열 만들기")</span><span class="sxs-lookup"><span data-stu-id="4ee70-405">![Creating the database](aspnet-mvc-4-custom-action-filters/_static/image34.png "Creating the database string")</span></span>

    <span data-ttu-id="4ee70-406">*데이터베이스를 만드는 중*</span><span class="sxs-lookup"><span data-stu-id="4ee70-406">*Creating the database*</span></span>
7. <span data-ttu-id="4ee70-407">Windows azure에서 SQL 데이터베이스에 연결 하기 위해 사용할 연결 문자열은 기본 연결 텍스트 상자 내에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-407">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="4ee70-408">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-408">Then click **Next**.</span></span>

    <span data-ttu-id="4ee70-409">![SQL 데이터베이스를 가리키는 연결 문자열](aspnet-mvc-4-custom-action-filters/_static/image35.png "SQL 데이터베이스를 가리키는 연결 문자열")</span><span class="sxs-lookup"><span data-stu-id="4ee70-409">![Connection string pointing to SQL Database](aspnet-mvc-4-custom-action-filters/_static/image35.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="4ee70-410">*SQL 데이터베이스를 가리키는 연결 문자열*</span><span class="sxs-lookup"><span data-stu-id="4ee70-410">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="4ee70-411">에 **미리 보기** 페이지 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-411">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="4ee70-412">![웹 응용 프로그램을 게시](aspnet-mvc-4-custom-action-filters/_static/image36.png "웹 응용 프로그램 게시")</span><span class="sxs-lookup"><span data-stu-id="4ee70-412">![Publishing the web application](aspnet-mvc-4-custom-action-filters/_static/image36.png "Publishing the web application")</span></span>

    <span data-ttu-id="4ee70-413">*웹 응용 프로그램 게시*</span><span class="sxs-lookup"><span data-stu-id="4ee70-413">*Publishing the web application*</span></span>
9. <span data-ttu-id="4ee70-414">게시 프로세스가 완료 되 면 게시 된 웹 사이트 기본 브라우저가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-414">Once the publishing process finishes, your default browser will open the published web site.</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a><span data-ttu-id="4ee70-415">부록 c: 코드 조각을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="4ee70-415">Appendix C: Using Code Snippets</span></span>

<span data-ttu-id="4ee70-416">코드 조각 바로 쉽게 얻습니다 필요한 코드를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-416">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="4ee70-417">랩 문서는 알려 정확 하 게 사용 가능 시기, 다음 그림에 나와 있는 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-417">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="4ee70-418">![Visual Studio 코드 조각을 프로젝트에 코드 삽입을 사용 하 여](aspnet-mvc-4-custom-action-filters/_static/image37.png "Visual Studio를 사용 하 여 코드 조각을 프로젝트에 코드를 삽입 하려면")</span><span class="sxs-lookup"><span data-stu-id="4ee70-418">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-custom-action-filters/_static/image37.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="4ee70-419">*Visual Studio 코드 조각을 프로젝트에 코드 삽입을 사용 하 여*</span><span class="sxs-lookup"><span data-stu-id="4ee70-419">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="4ee70-420">***키보드 (C#만)를 사용 하 여 코드 조각을 추가 하려면***</span><span class="sxs-lookup"><span data-stu-id="4ee70-420">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="4ee70-421">코드를 삽입 하려는 위치에 커서를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-421">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="4ee70-422">공백 또는 하이픈만) (없이 코드 조각 이름을 입력 하기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-422">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="4ee70-423">IntelliSense 표시 조각 이름과 일치 하는 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-423">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="4ee70-424">올바른 코드 조각 선택 (또는 전체 코드 조각이 이름이 선택 될 때까지 입력 유지).</span><span class="sxs-lookup"><span data-stu-id="4ee70-424">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="4ee70-425">커서 위치에 코드 조각을 삽입 하려면 두 번 탭 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-425">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="4ee70-426">![코드 조각 이름을 입력 하기 시작](aspnet-mvc-4-custom-action-filters/_static/image38.png "조각 이름을 입력 하기 시작")</span><span class="sxs-lookup"><span data-stu-id="4ee70-426">![Start typing the snippet name](aspnet-mvc-4-custom-action-filters/_static/image38.png "Start typing the snippet name")</span></span>

<span data-ttu-id="4ee70-427">*코드 조각 이름을 입력 하기 시작*</span><span class="sxs-lookup"><span data-stu-id="4ee70-427">*Start typing the snippet name*</span></span>

<span data-ttu-id="4ee70-428">![Tab 키를 눌러 강조 표시 된 코드 조각 선택](aspnet-mvc-4-custom-action-filters/_static/image39.png "Tab 키를 눌러 강조 표시 된 코드 조각 선택")</span><span class="sxs-lookup"><span data-stu-id="4ee70-428">![Press Tab to select the highlighted snippet](aspnet-mvc-4-custom-action-filters/_static/image39.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="4ee70-429">*Tab 키를 눌러 강조 표시 된 코드 조각 선택*</span><span class="sxs-lookup"><span data-stu-id="4ee70-429">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="4ee70-430">![확장 하 고 Tab 키를 눌러 다시 코드 조각](aspnet-mvc-4-custom-action-filters/_static/image40.png "확장 하 고 Tab 키를 눌러 다시 코드 조각")</span><span class="sxs-lookup"><span data-stu-id="4ee70-430">![Press Tab again and the snippet will expand](aspnet-mvc-4-custom-action-filters/_static/image40.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="4ee70-431">*확장 하 고 Tab 키를 눌러 다시 코드 조각*</span><span class="sxs-lookup"><span data-stu-id="4ee70-431">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="4ee70-432">***마우스 (C#, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가 하려면*** 1입니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-432">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="4ee70-433">코드 조각을 삽입 하려면 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-433">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="4ee70-434">선택 **조각 삽입** 이어서 **내 코드 조각**합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-434">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="4ee70-435">클릭 하 여 목록에서 관련 조각을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ee70-435">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="4ee70-436">![코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추로 클릭](aspnet-mvc-4-custom-action-filters/_static/image41.png "코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추 클릭")</span><span class="sxs-lookup"><span data-stu-id="4ee70-436">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-custom-action-filters/_static/image41.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="4ee70-437">*코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추로 클릭*</span><span class="sxs-lookup"><span data-stu-id="4ee70-437">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="4ee70-438">![클릭 하 여 목록에서 관련 조각을 선택](aspnet-mvc-4-custom-action-filters/_static/image42.png "클릭 하 여 목록에서 관련 조각을 선택")</span><span class="sxs-lookup"><span data-stu-id="4ee70-438">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-custom-action-filters/_static/image42.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="4ee70-439">*클릭 하 여 목록에서 관련 조각을 선택합니다*</span><span class="sxs-lookup"><span data-stu-id="4ee70-439">*Pick the relevant snippet from the list, by clicking on it*</span></span>
