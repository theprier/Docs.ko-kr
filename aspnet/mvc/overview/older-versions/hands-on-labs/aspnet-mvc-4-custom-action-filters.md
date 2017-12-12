---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters
title: "ASP.NET MVC 4 사용자 지정 작업 필터 | Microsoft Docs"
author: rick-anderson
description: "ASP.NET MVC 이전 또는 작업 메서드가 호출 된 후 필터링 논리를 실행 하기 위한 작업 필터를 제공 합니다. 작업 필터는 사용자 지정 특성 tha 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: 969ab824-1b98-4552-81fe-b60ef5fc6887
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters
msc.type: authoredcontent
ms.openlocfilehash: 6362f0506934ca3b3cc86e1a927af75e7bc4e1d3
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="aspnet-mvc-4-custom-action-filters"></a><span data-ttu-id="5cbb6-104">ASP.NET MVC 4 사용자 지정 작업 필터</span><span class="sxs-lookup"><span data-stu-id="5cbb6-104">ASP.NET MVC 4 Custom Action Filters</span></span>
====================
<span data-ttu-id="5cbb6-105">으로 [웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="5cbb6-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> <span data-ttu-id="5cbb6-106">ASP.NET MVC 이전 또는 작업 메서드가 호출 된 후 필터링 논리를 실행 하기 위한 작업 필터를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-106">ASP.NET MVC provides Action Filters for executing filtering logic either before or after an action method is called.</span></span> <span data-ttu-id="5cbb6-107">작업 필터는 이전 및 이후 작업의 동작을 추가할 컨트롤러의 작업 메서드에 선언적 수단을 제공 하는 사용자 지정 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-107">Action Filters are custom attributes that provide declarative means to add pre-action and post-action behavior to the controller's action methods.</span></span>
> 
> <span data-ttu-id="5cbb6-108">이 실습 랩에서 MvcMusicStore 컨트롤러의 요청을 catch 하 고 데이터베이스 테이블에는 사이트의 활동을 기록 하는 솔루션에 사용자 지정 작업 필터 특성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-108">In this Hands-on Lab you will create a custom action filter attribute into MvcMusicStore solution to catch controller's requests and log the activity of a site into a database table.</span></span> <span data-ttu-id="5cbb6-109">모든 컨트롤러 또는 동작에 삽입 하 여 로깅 필터를 추가할 수 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-109">You will be able to add your logging filter by injection to any controller or action.</span></span> <span data-ttu-id="5cbb6-110">마지막으로 방문자의 목록을 보여 주는 로그 보기를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-110">Finally, you will see the log view that shows the list of visitors.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="5cbb6-111">이 실습 랩 대 한 기본 지식이 있다고 가정 하 고 **ASP.NET MVC**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-111">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC**.</span></span> <span data-ttu-id="5cbb6-112">사용 하지 않은 경우 **ASP.NET MVC** 를 권장 앞, **ASP.NET MVC 4 기초** 실습 랩입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-112">If you have not used **ASP.NET MVC** before, we recommend you to go over **ASP.NET MVC 4 Fundamentals** Hands-on Lab.</span></span>


<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="5cbb6-113">목표</span><span class="sxs-lookup"><span data-stu-id="5cbb6-113">Objectives</span></span>

<span data-ttu-id="5cbb6-114">이 실습 랩에서 배우게 됩니다 하는 방법:</span><span class="sxs-lookup"><span data-stu-id="5cbb6-114">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="5cbb6-115">필터링 기능을 확장 하는 사용자 지정 작업 필터 특성 만들기</span><span class="sxs-lookup"><span data-stu-id="5cbb6-115">Create a custom action filter attribute to extend filtering capabilities</span></span>
- <span data-ttu-id="5cbb6-116">특정 수준으로 삽입 하 여 사용자 지정 필터 특성을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-116">Apply a custom filter attribute by injection to a specific level</span></span>
- <span data-ttu-id="5cbb6-117">사용자 지정 작업 필터를 전역으로 등록</span><span class="sxs-lookup"><span data-stu-id="5cbb6-117">Register a custom action filters globally</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="5cbb6-118">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="5cbb6-118">Prerequisites</span></span>

<span data-ttu-id="5cbb6-119">이 랩을 완료 하려면 다음 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-119">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="5cbb6-120">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) 하거나 그 보다 뛰어난 (읽기 [부록 A](#AppendixA) 설치 하는 방법에 대 한 지침은).</span><span class="sxs-lookup"><span data-stu-id="5cbb6-120">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="5cbb6-121">설정</span><span class="sxs-lookup"><span data-stu-id="5cbb6-121">Setup</span></span>

<span data-ttu-id="5cbb6-122">**설치 하는 코드 조각**</span><span class="sxs-lookup"><span data-stu-id="5cbb6-122">**Installing Code Snippets**</span></span>

<span data-ttu-id="5cbb6-123">편의 위해는이 랩에 따라 관리 코드의 대부분 Visual Studio 코드 조각 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-123">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="5cbb6-124">실행 코드 조각을 설치 하려면 **.\Source\Setup\CodeSnippets.vsi** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-124">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="5cbb6-125">이 문서에서 부록을 참조할 수 사용 하는 방법에 알아봅니다 사용 하 고 Visual Studio 코드 조각에 익숙한 경우 &quot; [부록 c:를 사용 하 여 코드 조각을](#AppendixC)&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-125">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix C: Using Code Snippets](#AppendixC)&quot;.</span></span>

* * *

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="5cbb6-126">연습</span><span class="sxs-lookup"><span data-stu-id="5cbb6-126">Exercises</span></span>

<span data-ttu-id="5cbb6-127">이 실습 랩에서 다음 연습으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-127">This Hands-On Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="5cbb6-128">연습 1: 로깅 작업</span><span class="sxs-lookup"><span data-stu-id="5cbb6-128">Exercise 1: Logging actions</span></span>](#Exercise1)
2. [<span data-ttu-id="5cbb6-129">연습 2: 여러 작업 필터 관리</span><span class="sxs-lookup"><span data-stu-id="5cbb6-129">Exercise 2: Managing Multiple Action Filters</span></span>](#Exercise2)

<span data-ttu-id="5cbb6-130">예상 소요 시간: **30 분**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-130">Estimated time to complete this lab: **30 minutes**.</span></span>

> [!NOTE]
> <span data-ttu-id="5cbb6-131">각 연습 동반 되는 **끝** 연습을 완료 한 후 가져와야 생성 되는 솔루션에 포함 된 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-131">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="5cbb6-132">연습을 통해 작업 하는 추가 도움이 필요한 경우이 솔루션 가이드로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-132">You can use this solution as a guide if you need additional help working through the exercises.</span></span>


<a id="Exercise1"></a>

<a id="Exercise_1_Logging_Actions"></a>
### <a name="exercise-1-logging-actions"></a><span data-ttu-id="5cbb6-133">연습 1: 로깅 작업</span><span class="sxs-lookup"><span data-stu-id="5cbb6-133">Exercise 1: Logging Actions</span></span>

<span data-ttu-id="5cbb6-134">이 연습에서는 ASP.NET MVC 4 필터 공급자를 사용 하 여 사용자 지정 작업 로그 필터를 만드는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-134">In this exercise, you will learn how to create a custom action log filter by using ASP.NET MVC 4 Filter Providers.</span></span> <span data-ttu-id="5cbb6-135">포함 하기 위해 선택한 컨트롤러의 모든 활동을 기록 하며 됩니다 MusicStore 사이트로 로깅 필터를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-135">For that purpose you will apply a logging filter to the MusicStore site that will record all the activities in the selected controllers.</span></span>

<span data-ttu-id="5cbb6-136">필터를 확장 하면 **ActionFilterAttributeClass** 재정의 **OnActionExecuting** 메서드에서를 각 요청을 catch 한 다음 로깅 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-136">The filter will extend **ActionFilterAttributeClass** and override **OnActionExecuting** method to catch each request and then perform the logging actions.</span></span> <span data-ttu-id="5cbb6-137">HTTP 요청에 대 한 컨텍스트 정보를 실행 하는 메서드, 결과 및 매개 변수에서 제공 합니다 ASP.NET MVC **ActionExecutingContext** 클래스 **합니다.**</span><span class="sxs-lookup"><span data-stu-id="5cbb6-137">The context information about HTTP requests, executing methods, results and parameters will be provided by ASP.NET MVC **ActionExecutingContext** class **.**</span></span>

> [!NOTE]
> <span data-ttu-id="5cbb6-138">ASP.NET MVC 4에는 기본 필터 공급자는 사용자 지정 필터를 만들지 않고 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-138">ASP.NET MVC 4 also has default filters providers you can use without creating a custom filter.</span></span> <span data-ttu-id="5cbb6-139">ASP.NET MVC 4에서는 다음 유형의 필터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-139">ASP.NET MVC 4 provides the following types of filters:</span></span>
> 
> - <span data-ttu-id="5cbb6-140">**권한 부여** 필터링, 같은 인증을 수행 또는 요청의 속성을 확인 하는 동작 메서드를 실행 하는 여부에 대 한 보안 결정 수 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-140">**Authorization** filter, which makes security decisions about whether to execute an action method, such as performing authentication or validating properties of the request.</span></span>
> - <span data-ttu-id="5cbb6-141">**동작** 작업 메서드 실행 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-141">**Action** filter, which wraps the action method execution.</span></span> <span data-ttu-id="5cbb6-142">이 필터는 동작 메서드에 추가 데이터를 제공, 반환 값 검사 또는 작업 메서드 실행을 취소 하는 등의 추가 프로세스를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-142">This filter can perform additional processing, such as providing extra data to the action method, inspecting the return value, or canceling execution of the action method</span></span>
> - <span data-ttu-id="5cbb6-143">**결과** ActionResult 개체 실행의 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-143">**Result** filter, which wraps execution of the ActionResult object.</span></span> <span data-ttu-id="5cbb6-144">이 필터는 결과 HTTP 응답을 수정 하는 등의 추가 처리를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-144">This filter can perform additional processing of the result, such as modifying the HTTP response.</span></span>
> - <span data-ttu-id="5cbb6-145">**예외** 권한 부여 필터와 시작점과 결과의 실행 동작 메서드에서 어딘가에 발생 하는 처리 되지 않은 예외 경우에 실행 하는 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-145">**Exception** filter, which executes if there is an unhandled exception thrown somewhere in action method, starting with the authorization filters and ending with the execution of the result.</span></span> <span data-ttu-id="5cbb6-146">로깅 또는 오류 페이지 표시 등의 작업에 대 한 예외 필터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-146">Exception filters can be used for tasks such as logging or displaying an error page.</span></span>
> 
> <span data-ttu-id="5cbb6-147">필터 공급자에 대 한 자세한 내용은 MSDN 링크를 방문 하십시오. ([https://msdn.microsoft.com/en-us/library/dd410209.aspx](https://msdn.microsoft.com/en-us/library/dd410209.aspx)).</span><span class="sxs-lookup"><span data-stu-id="5cbb6-147">For more information about Filters Providers please visit this MSDN link: ([https://msdn.microsoft.com/en-us/library/dd410209.aspx](https://msdn.microsoft.com/en-us/library/dd410209.aspx)) .</span></span>


<a id="AboutLoggingFeature"></a>

<a id="About_MVC_Music_Store_Application_logging_feature"></a>
#### <a name="about-mvc-music-store-application-logging-feature"></a><span data-ttu-id="5cbb6-148">MVC 음악 스토어 응용 프로그램 로깅 기능에 대 한</span><span class="sxs-lookup"><span data-stu-id="5cbb6-148">About MVC Music Store Application logging feature</span></span>

<span data-ttu-id="5cbb6-149">이 Music Store 솔루션은 사이트 로깅에 대 한 새 데이터 모델 테이블 **ActionLog**, 다음 필드: 요청, 작업 호출, 클라이언트 IP 및 타임 스탬프를 수신 하는 컨트롤러의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-149">This Music Store solution has a new data model table for site logging, **ActionLog**, with the following fields: Name of the controller that received a request, Called action, Client IP and Time stamp.</span></span>

<span data-ttu-id="5cbb6-150">![데이터 모델입니다. ActionLog 테이블입니다. ] (aspnet-mvc-4-custom-action-filters/_static/image1.png "데이터 모델입니다. ActionLog 테이블입니다.")</span><span class="sxs-lookup"><span data-stu-id="5cbb6-150">![Data model. ActionLog table.](aspnet-mvc-4-custom-action-filters/_static/image1.png "Data model. ActionLog table.")</span></span>

<span data-ttu-id="5cbb6-151">*데이터 모델-ActionLog 테이블*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-151">*Data model - ActionLog table*</span></span>

<span data-ttu-id="5cbb6-152">솔루션에서 찾을 수 있는 작업 로그에 대 한 ASP.NET MVC 뷰를 제공 **MvcMusicStores/뷰/ActionLog**:</span><span class="sxs-lookup"><span data-stu-id="5cbb6-152">The solution provides an ASP.NET MVC View for the Action log that can be found at **MvcMusicStores/Views/ActionLog**:</span></span>

<span data-ttu-id="5cbb6-153">![작업 로그 보기](aspnet-mvc-4-custom-action-filters/_static/image2.png "작업 로그 보기")</span><span class="sxs-lookup"><span data-stu-id="5cbb6-153">![Action Log view](aspnet-mvc-4-custom-action-filters/_static/image2.png "Action Log view")</span></span>

<span data-ttu-id="5cbb6-154">*작업 로그 보기*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-154">*Action Log view*</span></span>

<span data-ttu-id="5cbb6-155">이 구조를 제공 하는 모든 작업 컨트롤러의 요청을 중단 하 고 사용자 지정 필터링을 사용 하 여 로깅을 수행에 집중 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-155">With this given structure, all the work will be focused on interrupting controller's request and performing the logging by using custom filtering.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_a_Custom_Filter_to_Catch_a_Controllers_Request"></a>
#### <a name="task-1---creating-a-custom-filter-to-catch-a-controllers-request"></a><span data-ttu-id="5cbb6-156">작업 1-컨트롤러의 요청을 Catch 하는 사용자 지정 필터 만들기</span><span class="sxs-lookup"><span data-stu-id="5cbb6-156">Task 1 - Creating a Custom Filter to Catch a Controller's Request</span></span>

<span data-ttu-id="5cbb6-157">이 작업의 로깅 논리를 포함 하는 사용자 지정 필터 특성 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-157">In this task you will create a custom filter attribute class that will contain the logging logic.</span></span> <span data-ttu-id="5cbb6-158">ASP.NET MVC를 확장 하면 해당 용도로 **ActionFilterAttribute** 클래스 및 인터페이스 구현 **IActionFilter**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-158">For that purpose you will extend ASP.NET MVC **ActionFilterAttribute** Class and implement the interface **IActionFilter**.</span></span>

> [!NOTE]
> <span data-ttu-id="5cbb6-159">**ActionFilterAttribute** 는 모든 특성 필터에 대 한 기본 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-159">The **ActionFilterAttribute** is the base class for all the attribute filters.</span></span> <span data-ttu-id="5cbb6-160">컨트롤러 동작 실행 전과 후에 특정 논리를 실행 하기 위해 다음 메서드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-160">It provides the following methods to execute a specific logic after and before controller action's execution:</span></span>
> 
> - <span data-ttu-id="5cbb6-161">**OnActionExecuting**(ActionExecutingContext filterContext): 작업 바로 전에 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-161">**OnActionExecuting**(ActionExecutingContext filterContext): Just before the action method is called.</span></span>
> - <span data-ttu-id="5cbb6-162">**OnActionExecuted**(ActionExecutedContext filterContext): 작업 메서드를 호출한 후 및 결과 보기 렌더링) (이전 실행 되기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-162">**OnActionExecuted**(ActionExecutedContext filterContext): After the action method is called and before the result is executed (before view render).</span></span>
> - <span data-ttu-id="5cbb6-163">**OnResultExecuting**(ResultExecutingContext filterContext): (이전 뷰 렌더링) 결과 실행 하기 전에 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-163">**OnResultExecuting**(ResultExecutingContext filterContext): Just before the result is executed (before view render).</span></span>
> - <span data-ttu-id="5cbb6-164">**OnResultExecuted**(ResultExecutedContext filterContext): (뷰를 렌더링할) 후 결과 실행 한 후입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-164">**OnResultExecuted**(ResultExecutedContext filterContext): After the result is executed (after the view is rendered).</span></span>
> 
> <span data-ttu-id="5cbb6-165">다음이 방법 중 하나 파생된 클래스에 재정의 함으로써 필터링 코드를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-165">By overriding any of these methods into a derived class, you can execute your own filtering code.</span></span>


1. <span data-ttu-id="5cbb6-166">열기는 **시작** 솔루션에 있는 **\Source\Ex01-LoggingActions\Begin** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-166">Open the **Begin** solution located at **\Source\Ex01-LoggingActions\Begin** folder.</span></span>

    1. <span data-ttu-id="5cbb6-167">계속 하기 전에 몇 가지 누락 된 NuGet 패키지를 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-167">You will need to download some missing NuGet packages before you continue.</span></span> <span data-ttu-id="5cbb6-168">이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-168">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="5cbb6-169">에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-169">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
    3. <span data-ttu-id="5cbb6-170">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-170">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5cbb6-171">NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-171">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="5cbb6-172">NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-172">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="5cbb6-173">이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-173">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
    > 
    > <span data-ttu-id="5cbb6-174">자세한 내용은이 문서를 참조 하십시오.: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-174">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="5cbb6-175">에 새 C# 클래스를 추가 **필터** 폴더 이름을 지정 *CustomActionFilter.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-175">Add a new C# class into the **Filters** folder and name it *CustomActionFilter.cs*.</span></span> <span data-ttu-id="5cbb6-176">이 폴더는 모든 사용자 지정 필터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-176">This folder will store all the custom filters.</span></span>
3. <span data-ttu-id="5cbb6-177">열기 **CustomActionFilter.cs** 에 대 한 참조를 추가 하 고 **System.Web.Mvc** 및 **MvcMusicStore.Models** 네임 스페이스:</span><span class="sxs-lookup"><span data-stu-id="5cbb6-177">Open **CustomActionFilter.cs** and add a reference to **System.Web.Mvc** and **MvcMusicStore.Models** namespaces:</span></span>

    <span data-ttu-id="5cbb6-178">(코드 조각- *ASP.NET MVC 4 사용자 지정 작업 필터-e x 1 CustomActionFilterNamespaces*)</span><span class="sxs-lookup"><span data-stu-id="5cbb6-178">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex1-CustomActionFilterNamespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample1.cs)]
4. <span data-ttu-id="5cbb6-179">상속 된 **CustomActionFilter** 에서 클래스 **ActionFilterAttribute** 다음 **CustomActionFilter** 클래스 구현 **IActionFilter** 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-179">Inherit the **CustomActionFilter** class from **ActionFilterAttribute** and then make **CustomActionFilter** class implement **IActionFilter** interface.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample2.cs)]
5. <span data-ttu-id="5cbb6-180">확인 **CustomActionFilter** 클래스 메서드를 재정의 **OnActionExecuting** 고 필터의 실행을 기록 하는 데 필요한 논리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-180">Make **CustomActionFilter** class override the method **OnActionExecuting** and add the necessary logic to log the filter's execution.</span></span> <span data-ttu-id="5cbb6-181">이 위해 내에서 강조 표시 된 다음 코드를 추가 **CustomActionFilter** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-181">To do this, add the following highlighted code within **CustomActionFilter** class.</span></span>

    <span data-ttu-id="5cbb6-182">(코드 조각- *ASP.NET MVC 4 사용자 지정 작업 필터-e x 1 LoggingActions*)</span><span class="sxs-lookup"><span data-stu-id="5cbb6-182">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex1-LoggingActions*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample3.cs#Highlight)]

    > [!NOTE]
    > <span data-ttu-id="5cbb6-183">**OnActionExecuting** 메서드를 사용 하 여 **Entity Framework** 새 ActionLog 레지스터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-183">**OnActionExecuting** method is using **Entity Framework** to add a new ActionLog register.</span></span> <span data-ttu-id="5cbb6-184">작성 하는 컨텍스트 정보로 새 엔터티 인스턴스에 **filterContext**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-184">It creates and fills a new entity instance with the context information from **filterContext**.</span></span>
    > 
    > <span data-ttu-id="5cbb6-185">에 대 한 자세한 내용은 **ControllerContext** 에 클래스 [msdn](https://msdn.microsoft.com/en-us/library/system.web.mvc.controllercontext.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-185">You can read more about **ControllerContext** class at [msdn](https://msdn.microsoft.com/en-us/library/system.web.mvc.controllercontext.aspx).</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Injecting_a_Code_Interceptor_into_the_Store_Controller_Class"></a>
#### <a name="task-2---injecting-a-code-interceptor-into-the-store-controller-class"></a><span data-ttu-id="5cbb6-186">작업 2-저장소 컨트롤러 클래스에 코드 인터셉터 삽입</span><span class="sxs-lookup"><span data-stu-id="5cbb6-186">Task 2 - Injecting a Code Interceptor into the Store Controller Class</span></span>

<span data-ttu-id="5cbb6-187">이 작업에서 모든 컨트롤러 클래스 및 로그온할지 컨트롤러 작업에 삽입 하 여 사용자 지정 필터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-187">In this task you will add the custom filter by injecting it to all controller classes and controller actions that will be logged.</span></span> <span data-ttu-id="5cbb6-188">이 연습에서는 저장소 컨트롤러 클래스는 로그를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-188">For the purpose of this exercise, the Store Controller class will have a log.</span></span>

<span data-ttu-id="5cbb6-189">메서드가 **OnActionExecuting** 에서 **ActionLogFilterAttribute** 삽입 된 요소를 호출할 때 사용자 지정 필터를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-189">The method **OnActionExecuting** from **ActionLogFilterAttribute** custom filter runs when an injected element is called.</span></span>

<span data-ttu-id="5cbb6-190">특정 컨트롤러 메서드를 가로채도 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-190">It is also possible to intercept a specific controller method.</span></span>

1. <span data-ttu-id="5cbb6-191">열기는 **StoreController** 에서 **MvcMusicStore\Controllers** 에 대 한 참조를 추가 하 고는 **필터** 네임 스페이스:</span><span class="sxs-lookup"><span data-stu-id="5cbb6-191">Open the **StoreController** at **MvcMusicStore\Controllers** and add a reference to the **Filters** namespace:</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample4.cs)]
2. <span data-ttu-id="5cbb6-192">사용자 지정 필터를 주입 **CustomActionFilter** 에 **StoreController** 클래스를 추가 하 여 **[CustomActionFilter]** 특성 클래스 선언 앞입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-192">Inject the custom filter **CustomActionFilter** into **StoreController** class by adding **[CustomActionFilter]** attribute before the class declaration.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample5.cs)]

    > [!NOTE]
    > <span data-ttu-id="5cbb6-193">필터는 컨트롤러 클래스에 주입 된, 모든 작업은 삽입도 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-193">When a filter is injected into a controller class, all its actions are also injected.</span></span> <span data-ttu-id="5cbb6-194">삽입 해야 일련의 동작에 대해서만 필터를 적용 하려는 경우 **[CustomActionFilter]** 중 각각에:</span><span class="sxs-lookup"><span data-stu-id="5cbb6-194">If you would like to apply the filter only for a set of actions, you would have to inject **[CustomActionFilter]** to each one of them:</span></span>
    > 
    > [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample6.cs)]

<a id="Ex1Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="5cbb6-195">작업 3-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="5cbb6-195">Task 3 - Running the Application</span></span>

<span data-ttu-id="5cbb6-196">이 태스크에서는 로깅 필터 작동 하는지 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-196">In this task, you will test that the logging filter is working.</span></span> <span data-ttu-id="5cbb6-197">응용 프로그램 시작 되며,에서 스토어를 방문 하 고 기록 된 활동을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-197">You will start the application and visit the store, and then you will check logged activities.</span></span>

1. <span data-ttu-id="5cbb6-198">**F5** 키를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-198">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="5cbb6-199">찾아 **/ActionLog** 로그 보기 초기 상태를 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-199">Browse to **/ActionLog** to see log view initial state:</span></span>

    <span data-ttu-id="5cbb6-200">![로그 페이지 작업 이전 상태 추적기](aspnet-mvc-4-custom-action-filters/_static/image3.png "로그 페이지 작업 전에 추적 장치 상태")</span><span class="sxs-lookup"><span data-stu-id="5cbb6-200">![Log tracker status before page activity](aspnet-mvc-4-custom-action-filters/_static/image3.png "Log tracker status before page activity")</span></span>

    <span data-ttu-id="5cbb6-201">*페이지 작업 이전 로그 추적 장치 상태*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-201">*Log tracker status before page activity*</span></span>

    > [!NOTE]
    > <span data-ttu-id="5cbb6-202">기본적으로 한 항목의 메뉴에 대 한 기존 장르를 검색할 때 생성 되는 항상 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-202">By default, it will always show one item that is generated when retrieving the existing genres for the menu.</span></span>
    > 
    > <span data-ttu-id="5cbb6-203">단순성을 위해를 정리 하 우리는 **ActionLog** 는 각 특정 작업의 확인의 로그 데이터만 표시 하도록 응용 프로그램이 실행 될 때마다 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-203">For simplicity purposes we're cleaning up the **ActionLog** table each time the application runs so it will only show the logs of each particular task's verification.</span></span>
    > 
    > <span data-ttu-id="5cbb6-204">파일에서 다음 코드를 제거 해야 할 수는 **세션\_시작** 메서드 (에 **Global.asax** 클래스), 저장소 내에서 실행 되는 모든 작업에 대 한 기록 로그를 저장 하려면 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-204">You might need to remove the following code from the **Session\_Start** method (in the **Global.asax** class), in order to save an historical log for all the actions executed within the Store Controller.</span></span>
    > 
    > [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample7.cs)]
3. <span data-ttu-id="5cbb6-205">중 하나를 클릭는 **장르** 메뉴에서 사용할 수 있는 앨범 화, 일부 작업을 수행 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-205">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
4. <span data-ttu-id="5cbb6-206">찾아 **/ActionLog** 로그 빈 키를 눌러가 고 **F5** 페이지를 새로 고칠 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-206">Browse to **/ActionLog** and if the log is empty press **F5** to refresh the page.</span></span> <span data-ttu-id="5cbb6-207">프로그램 환자가 내 원 추적 된 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-207">Check that your visits were tracked:</span></span>

    <span data-ttu-id="5cbb6-208">![기록 된 동작을 사용 하 여 작업 로그](aspnet-mvc-4-custom-action-filters/_static/image4.png "기록 된 동작을 사용 하 여 작업 로그")</span><span class="sxs-lookup"><span data-stu-id="5cbb6-208">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image4.png "Action log with activity logged")</span></span>

    <span data-ttu-id="5cbb6-209">*기록 된 동작을 사용 하 여 작업 로그*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-209">*Action log with activity logged*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Managing_Multiple_Action_Filters"></a>
### <a name="exercise-2-managing-multiple-action-filters"></a><span data-ttu-id="5cbb6-210">연습 2: 여러 작업 필터 관리</span><span class="sxs-lookup"><span data-stu-id="5cbb6-210">Exercise 2: Managing Multiple Action Filters</span></span>

<span data-ttu-id="5cbb6-211">이 연습에서는 StoreController 클래스에 두 번째 사용자 지정 작업 필터를 추가 하 고 두 필터가 모두 실행할 수 있는 특정 순서를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-211">In this exercise you will add a second Custom Action Filter to the StoreController class and define the specific order in which both filters will be executed.</span></span> <span data-ttu-id="5cbb6-212">그런 다음 필터를 전역으로 등록 하는 코드를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-212">Then you will update the code to register the filter Globally.</span></span>

<span data-ttu-id="5cbb6-213">필터의 실행 순서를 정의할 때 고려해 야 할 다른 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-213">There are different options to take into account when defining the Filters' execution order.</span></span> <span data-ttu-id="5cbb6-214">예를 들어 Order 속성 및 필터 범위:</span><span class="sxs-lookup"><span data-stu-id="5cbb6-214">For example, the Order property and the Filters' scope:</span></span>

<span data-ttu-id="5cbb6-215">정의할 수는 **범위** 각 필터에 대 한 예를 들어 수 범위 내에서 실행 하는 모든 작업 필터는 **컨트롤러 범위**, 및에서 실행 되도록 모든 권한 부여 필터 **전역 범위** .</span><span class="sxs-lookup"><span data-stu-id="5cbb6-215">You can define a **Scope** for each of the Filters, for example, you could scope all the Action Filters to run within the **Controller Scope**, and all Authorization Filters to run in **Global scope**.</span></span> <span data-ttu-id="5cbb6-216">범위에 정의 된 실행 순서는 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-216">The scopes have a defined execution order.</span></span>

<span data-ttu-id="5cbb6-217">또한 각 작업 필터는 필터의 범위에서 실행 순서를 결정 하는 데 사용 되는 순서 속성을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-217">Additionally, each action filter has an Order property which is used to determine the execution order in the scope of the filter.</span></span>

<span data-ttu-id="5cbb6-218">사용자 지정 작업 필터 실행 순서에 대 한 자세한 내용은이 MSDN 문서를 참조 하십시오. ([https://msdn.microsoft.com/en-us/library/dd381609(v=vs.98).aspx](https://msdn.microsoft.com/en-us/library/dd381609(v=vs.98).aspx)) 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-218">For more information about Custom Action Filters execution order, please visit this MSDN article: ([https://msdn.microsoft.com/en-us/library/dd381609(v=vs.98).aspx](https://msdn.microsoft.com/en-us/library/dd381609(v=vs.98).aspx)).</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_Creating_a_new_Custom_Action_Filter"></a>
#### <a name="task-1-creating-a-new-custom-action-filter"></a><span data-ttu-id="5cbb6-219">태스크 1: 새 사용자 지정 작업 필터 만들기</span><span class="sxs-lookup"><span data-stu-id="5cbb6-219">Task 1: Creating a new Custom Action Filter</span></span>

<span data-ttu-id="5cbb6-220">이 태스크에서는 만들어집니다 StoreController 클래스에 삽입할 새 사용자 지정 작업 필터는 필터의 실행 순서를 관리 하는 방법에 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-220">In this task, you will create a new Custom Action Filter to inject into the StoreController class, learning how to manage the execution order of the filters.</span></span>

1. <span data-ttu-id="5cbb6-221">열기는 **시작** 솔루션에 있는 **\Source\Ex02-ManagingMultipleActionFilters\Begin** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-221">Open the **Begin** solution located at **\Source\Ex02-ManagingMultipleActionFilters\Begin** folder.</span></span> <span data-ttu-id="5cbb6-222">그렇지 않은 경우 계속 사용할 수도 있습니다는 **끝** 솔루션, 이전 연습을 완료 하 여 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-222">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

    1. <span data-ttu-id="5cbb6-223">제공 된 연 경우 **시작** 를 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 솔루션을 계속 하려면.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-223">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="5cbb6-224">이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-224">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="5cbb6-225">에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-225">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
    3. <span data-ttu-id="5cbb6-226">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-226">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

        > [!NOTE]
        > <span data-ttu-id="5cbb6-227">NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-227">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="5cbb6-228">NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-228">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="5cbb6-229">이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-229">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
        > 
        > <span data-ttu-id="5cbb6-230">자세한 내용은이 문서를 참조 하십시오.: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-230">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="5cbb6-231">에 새 C# 클래스를 추가 **필터** 폴더 이름을 지정 *MyNewCustomActionFilter.cs*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-231">Add a new C# class into the **Filters** folder and name it *MyNewCustomActionFilter.cs*</span></span>
3. <span data-ttu-id="5cbb6-232">열기 **MyNewCustomActionFilter.cs** 에 대 한 참조를 추가 하 고 **System.Web.Mvc** 및 **MvcMusicStore.Models** 네임 스페이스:</span><span class="sxs-lookup"><span data-stu-id="5cbb6-232">Open **MyNewCustomActionFilter.cs** and add a reference to **System.Web.Mvc** and the **MvcMusicStore.Models** namespace:</span></span>

    <span data-ttu-id="5cbb6-233">(코드 조각- *ASP.NET MVC 4 사용자 지정 작업 필터-e x 2 MyNewCustomActionFilterNamespaces*)</span><span class="sxs-lookup"><span data-stu-id="5cbb6-233">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex2-MyNewCustomActionFilterNamespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample8.cs)]
4. <span data-ttu-id="5cbb6-234">기본 클래스 선언을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-234">Replace the default class declaration with the following code.</span></span>

    <span data-ttu-id="5cbb6-235">(코드 조각- *ASP.NET MVC 4 사용자 지정 작업 필터-e x 2 MyNewCustomActionFilterClass*)</span><span class="sxs-lookup"><span data-stu-id="5cbb6-235">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex2-MyNewCustomActionFilterClass*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample9.cs)]

    > [!NOTE]
    > <span data-ttu-id="5cbb6-236">이 사용자 지정 작업 필터는 이전 연습에서 만든 것 보다 거의 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-236">This Custom Action Filter is almost the same than the one you created in the previous exercise.</span></span> <span data-ttu-id="5cbb6-237">주요 차이점은 있다는  *&quot;기록 하 여&quot;*  wich 필터를 식별 하는이 새 클래스의이 이름으로 업데이트 하는 특성의 로그를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-237">The main difference is that it has the *&quot;Logged By&quot;* attribute updated with this new class' name to identify wich filter registered the log.</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_Injecting_a_new_Code_Interceptor_into_the_StoreController_Class"></a>
#### <a name="task-2-injecting-a-new-code-interceptor-into-the-storecontroller-class"></a><span data-ttu-id="5cbb6-238">작업 2: StoreController 클래스에 새 코드 인터셉터 삽입</span><span class="sxs-lookup"><span data-stu-id="5cbb6-238">Task 2: Injecting a new Code Interceptor into the StoreController Class</span></span>

<span data-ttu-id="5cbb6-239">이 태스크에서는 StoreController 클래스에 새 사용자 지정 필터를를 추가 하 고 확인 방법을 두 필터는 함께 작동 하도록 솔루션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-239">In this task, you will add a new custom filter into the StoreController Class and run the solution to verify how both filters work together.</span></span>

1. <span data-ttu-id="5cbb6-240">열기는 **StoreController** 클래스에 있는 **MvcMusicStore\Controllers** 새 사용자 지정 필터를 삽입 하 고 **MyNewCustomActionFilter** 에  **StoreController** 와 같은 클래스는 다음 코드에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-240">Open the **StoreController** class located at **MvcMusicStore\Controllers** and inject the new custom filter **MyNewCustomActionFilter** into **StoreController** class like is shown in the following code.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample10.cs)]
2. <span data-ttu-id="5cbb6-241">이제 이러한 두 사용자 지정 작업 필터 어떻게 표시 되는지 확인 하려면 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-241">Now, run the application in order to see how these two Custom Action Filters work.</span></span> <span data-ttu-id="5cbb6-242">이 작업을 수행 하려면 키를 누릅니다 **F5** 응용 프로그램이 시작 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-242">To do this, press **F5** and wait until the application starts.</span></span>
3. <span data-ttu-id="5cbb6-243">찾아 **/ActionLog** 로그 보기 초기 상태를 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-243">Browse to **/ActionLog** to see log view initial state.</span></span>

    <span data-ttu-id="5cbb6-244">![로그 페이지 작업 이전 상태 추적기](aspnet-mvc-4-custom-action-filters/_static/image5.png "로그 페이지 작업 전에 추적 장치 상태")</span><span class="sxs-lookup"><span data-stu-id="5cbb6-244">![Log tracker status before page activity](aspnet-mvc-4-custom-action-filters/_static/image5.png "Log tracker status before page activity")</span></span>

    <span data-ttu-id="5cbb6-245">*페이지 작업 이전 로그 추적 장치 상태*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-245">*Log tracker status before page activity*</span></span>
4. <span data-ttu-id="5cbb6-246">중 하나를 클릭는 **장르** 메뉴에서 사용할 수 있는 앨범 화, 일부 작업을 수행 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-246">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
5. <span data-ttu-id="5cbb6-247">이 시간; 있는지 여부를 확인합니다 따라 방문 두 번 추적 된:에서 추가 사용자 지정 작업 필터의 각 면의 **StorageController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-247">Check that this time; your visits were tracked twice: once for each of the Custom Action Filters you added in the **StorageController** class.</span></span>

    <span data-ttu-id="5cbb6-248">![기록 된 동작을 사용 하 여 작업 로그](aspnet-mvc-4-custom-action-filters/_static/image6.png "기록 된 동작을 사용 하 여 작업 로그")</span><span class="sxs-lookup"><span data-stu-id="5cbb6-248">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image6.png "Action log with activity logged")</span></span>

    <span data-ttu-id="5cbb6-249">*기록 된 동작을 사용 하 여 작업 로그*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-249">*Action log with activity logged*</span></span>
6. <span data-ttu-id="5cbb6-250">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-250">Close the browser.</span></span>

<a id="Ex2Task3"></a>

<a id="Task_3_Managing_Filter_Ordering"></a>
#### <a name="task-3-managing-filter-ordering"></a><span data-ttu-id="5cbb6-251">작업 3: 필터 순서 관리</span><span class="sxs-lookup"><span data-stu-id="5cbb6-251">Task 3: Managing Filter Ordering</span></span>

<span data-ttu-id="5cbb6-252">이 작업 순서 속성을 사용 하 여 필터 실행 순서를 관리 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-252">In this task, you will learn how to manage the filters' execution order by using the Order propery.</span></span>

1. <span data-ttu-id="5cbb6-253">열기는 **StoreController** 클래스에 있는 **MvcMusicStore\Controllers** 지정는 **순서** 속성 필터 둘 모두에 같은 아래에 표시 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-253">Open the **StoreController** class located at **MvcMusicStore\Controllers** and specify the **Order** property in both filters like shown below.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample11.cs)]
2. <span data-ttu-id="5cbb6-254">이제, 해당 순서 속성의 값에 따라 필터는 실행 하는 방법을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-254">Now, verify how the filters are executed depending on its Order property's value.</span></span> <span data-ttu-id="5cbb6-255">필터에서 가장 작은 값으로 볼 수 있습니다 (**CustomActionFilter**)이 실행 되는 첫 번째 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-255">You will find that the filter with the smallest Order value (**CustomActionFilter**) is the first one that is executed.</span></span> <span data-ttu-id="5cbb6-256">키를 눌러 **F5** 응용 프로그램이 시작 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-256">Press **F5** and wait until the application starts.</span></span>
3. <span data-ttu-id="5cbb6-257">찾아 **/ActionLog** 로그 보기 초기 상태를 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-257">Browse to **/ActionLog** to see log view initial state.</span></span>

    <span data-ttu-id="5cbb6-258">![로그 페이지 작업 이전 상태 추적기](aspnet-mvc-4-custom-action-filters/_static/image7.png "로그 페이지 작업 전에 추적 장치 상태")</span><span class="sxs-lookup"><span data-stu-id="5cbb6-258">![Log tracker status before page activity](aspnet-mvc-4-custom-action-filters/_static/image7.png "Log tracker status before page activity")</span></span>

    <span data-ttu-id="5cbb6-259">*페이지 작업 이전 로그 추적 장치 상태*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-259">*Log tracker status before page activity*</span></span>
4. <span data-ttu-id="5cbb6-260">중 하나를 클릭는 **장르** 메뉴에서 사용할 수 있는 앨범 화, 일부 작업을 수행 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-260">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
5. <span data-ttu-id="5cbb6-261">필터의 순서 값에 따라 정렬 하는이 이번에 따라 방문 추적 된 확인: **CustomActionFilter** 로그의 첫 번째입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-261">Check that this time, your visits were tracked ordered by the filters' Order value: **CustomActionFilter** logs' first.</span></span>

    <span data-ttu-id="5cbb6-262">![기록 된 동작을 사용 하 여 작업 로그](aspnet-mvc-4-custom-action-filters/_static/image8.png "기록 된 동작을 사용 하 여 작업 로그")</span><span class="sxs-lookup"><span data-stu-id="5cbb6-262">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image8.png "Action log with activity logged")</span></span>

    <span data-ttu-id="5cbb6-263">*기록 된 동작을 사용 하 여 작업 로그*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-263">*Action log with activity logged*</span></span>
6. <span data-ttu-id="5cbb6-264">이제 필터의 순서 값을 업데이트 한 로깅 순서 어떻게 변경 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-264">Now, you will update the Filters' order value and verify how the logging order changes.</span></span> <span data-ttu-id="5cbb6-265">에 **StoreController** 클래스 아래에 표시 된 순서 값이 필터를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-265">In the **StoreController** class, update the Filters' Order value like shown below.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample12.cs)]
7. <span data-ttu-id="5cbb6-266">키를 눌러 응용 프로그램을 다시 실행 **F5**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-266">Run the application again by pressing **F5**.</span></span>
8. <span data-ttu-id="5cbb6-267">중 하나를 클릭는 **장르** 메뉴에서 사용할 수 있는 앨범 화, 일부 작업을 수행 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-267">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
9. <span data-ttu-id="5cbb6-268">이 이번에는 로그를 만들었음을 확인 **MyNewCustomActionFilter** 필터가 가장 먼저 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-268">Check that this time, the logs created by **MyNewCustomActionFilter** filter appears first.</span></span>

    <span data-ttu-id="5cbb6-269">![기록 된 동작을 사용 하 여 작업 로그](aspnet-mvc-4-custom-action-filters/_static/image9.png "기록 된 동작을 사용 하 여 작업 로그")</span><span class="sxs-lookup"><span data-stu-id="5cbb6-269">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image9.png "Action log with activity logged")</span></span>

    <span data-ttu-id="5cbb6-270">*기록 된 동작을 사용 하 여 작업 로그*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-270">*Action log with activity logged*</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_Registering_Filters_Globally"></a>
#### <a name="task-4-registering-filters-globally"></a><span data-ttu-id="5cbb6-271">작업 4: 전역 필터 등록</span><span class="sxs-lookup"><span data-stu-id="5cbb6-271">Task 4: Registering Filters Globally</span></span>

<span data-ttu-id="5cbb6-272">이 태스크에서는 새 필터를 등록 하려면 솔루션을 업데이트 합니다 (**MyNewCustomActionFilter**)를 글로벌 필터로 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-272">In this task, you will update the solution to register the new filter (**MyNewCustomActionFilter**) as a global filter.</span></span> <span data-ttu-id="5cbb6-273">이 작업을 수행 하 여 이전 태스크에서와 같이 StoreController 것 뿐만 아니라 응용 프로그램에 모든 작업 perfomed로 실행 될 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-273">By doing this, it will be triggered by all the actions perfomed in the application and not only in the StoreController ones as in the previous task.</span></span>

1. <span data-ttu-id="5cbb6-274">**StoreController** 클래스, 제거 **[MyNewCustomActionFilter]** 특성 및 순서 속성에서 **[CustomActionFilter]**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-274">In **StoreController** class, remove **[MyNewCustomActionFilter]** attribute and the order property from **[CustomActionFilter]**.</span></span> <span data-ttu-id="5cbb6-275">다음과 같은 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-275">It should look like the following:</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample13.cs)]
2. <span data-ttu-id="5cbb6-276">열기 **Global.asax** 파일를 찾습니다는 **응용 프로그램\_시작** 메서드.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-276">Open **Global.asax** file and locate the **Application\_Start** method.</span></span> <span data-ttu-id="5cbb6-277">공지는 각 thime 응용 프로그램을 시작 하기를 호출 하 여 전역 필터 등록 **RegisterGlobalFilters** 메서드 내에서 **FilterConfig** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-277">Notice that each thime the application starts it is registering the global filters by calling **RegisterGlobalFilters** method within **FilterConfig** class.</span></span>

    <span data-ttu-id="5cbb6-278">![전역 필터 Global.asax에 등록](aspnet-mvc-4-custom-action-filters/_static/image10.png "전역 필터 Global.asax에 등록 하는 중")</span><span class="sxs-lookup"><span data-stu-id="5cbb6-278">![Registering Global Filters in Global.asax](aspnet-mvc-4-custom-action-filters/_static/image10.png "Registering Global Filters in Global.asax")</span></span>

    <span data-ttu-id="5cbb6-279">*전역 필터 Global.asax에 등록 하는 중*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-279">*Registering Global Filters in Global.asax*</span></span>
3. <span data-ttu-id="5cbb6-280">열기 **FilterConfig.cs** 내에 파일이 **앱\_시작** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-280">Open **FilterConfig.cs** file within **App\_Start** folder.</span></span>
4. <span data-ttu-id="5cbb6-281">System.Web.Mvc;를 사용 하 여에 대 한 참조를 추가 합니다. MvcMusicStore.Filters;를 사용 하 여 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-281">Add a reference to using System.Web.Mvc; using MvcMusicStore.Filters; namespace.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample14.cs)]
5. <span data-ttu-id="5cbb6-282">업데이트 **RegisterGlobalFilters** 메서드를 사용자 지정 필터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-282">Update **RegisterGlobalFilters** method adding your custom filter.</span></span> <span data-ttu-id="5cbb6-283">이 작업을 수행 하려면 강조 표시 된 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-283">To do this, add the highlighted code:</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample15.cs)]
6. <span data-ttu-id="5cbb6-284">키를 눌러 응용 프로그램을 실행 **F5**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-284">Run the application by pressing **F5**.</span></span>
7. <span data-ttu-id="5cbb6-285">중 하나를 클릭는 **장르** 메뉴에서 사용할 수 있는 앨범 화, 일부 작업을 수행 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-285">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
8. <span data-ttu-id="5cbb6-286">이제 검사 **[MyNewCustomActionFilter]** 너무 HomeController 및 ActionLogController에 주입 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-286">Check that now **[MyNewCustomActionFilter]** is being injected in HomeController and ActionLogController too.</span></span>

    <span data-ttu-id="5cbb6-287">![기록 된 동작을 사용 하 여 작업 로그](aspnet-mvc-4-custom-action-filters/_static/image11.png "기록 된 동작을 사용 하 여 작업 로그")</span><span class="sxs-lookup"><span data-stu-id="5cbb6-287">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image11.png "Action log with activity logged")</span></span>

    <span data-ttu-id="5cbb6-288">*전역 작업 로그를 사용 하 여 작업 로그*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-288">*Action log with global activity logged*</span></span>

> [!NOTE]
> <span data-ttu-id="5cbb6-289">다음 Windows Azure 웹 사이트에이 응용 프로그램을 배포할 수는 또한 [부록 b: 게시 웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램](#AppendixB)합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-289">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>


* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="5cbb6-290">요약</span><span class="sxs-lookup"><span data-stu-id="5cbb6-290">Summary</span></span>

<span data-ttu-id="5cbb6-291">이 실습 랩을 완료 하 여 사용자 지정 작업을 실행 하는 작업 필터를 확장 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-291">By completing this Hands-On Lab you have learned how to extend an action filter to execute custom actions.</span></span> <span data-ttu-id="5cbb6-292">또한 페이지 컨트롤러에 필터를 주입 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-292">You have also learned how to inject any filter to your page controllers.</span></span> <span data-ttu-id="5cbb6-293">다음과 같은 개념 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-293">The following concepts were used:</span></span>

- <span data-ttu-id="5cbb6-294">ASP.NET MVC ActionFilterAttribute 클래스를 사용자 지정 작업 필터를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="5cbb6-294">How to create Custom Action filters with the ASP.NET MVC ActionFilterAttribute class</span></span>
- <span data-ttu-id="5cbb6-295">ASP.NET MVC 컨트롤러에 필터를 삽입 하는 방법</span><span class="sxs-lookup"><span data-stu-id="5cbb6-295">How to inject filters into ASP.NET MVC controllers</span></span>
- <span data-ttu-id="5cbb6-296">필터 순서 속성을 사용 하 여 순서를 관리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="5cbb6-296">How to manage filter ordering using the Order property</span></span>
- <span data-ttu-id="5cbb6-297">필터를 전역으로 등록 하는 방법</span><span class="sxs-lookup"><span data-stu-id="5cbb6-297">How to register filters globally</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="5cbb6-298">부록 a: 설치 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="5cbb6-298">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="5cbb6-299">설치할 수 있습니다 **Microsoft Visual Studio Express 2012 for Web** 또는 다른 &quot;Express&quot; 버전을 사용 하 여  **[Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)** .</span><span class="sxs-lookup"><span data-stu-id="5cbb6-299">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="5cbb6-300">다음 지침을 설치 하는 데 필요한 단계를 안내 하 *Visual studio Express 2012 for Web* 를 사용 하 여 *Microsoft 웹 플랫폼 설치 관리자*합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-300">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="5cbb6-301">로 이동 [ [https://go.microsoft.com/? linkid = 9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-301">Go to [[https://go.microsoft.com/? linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="5cbb6-302">또는 이미 설치 된 웹 플랫폼 설치 관리자를 열 수 있습니다 및 제품에 대 한 검색 &quot; *Visual Studio Express 2012 for Web Windows Azure SDK와*&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-302">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;*Visual Studio Express 2012 for Web with Windows Azure SDK*&quot;.</span></span>
2. <span data-ttu-id="5cbb6-303">클릭 **지금 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-303">Click on **Install Now**.</span></span> <span data-ttu-id="5cbb6-304">없는 경우 **웹 플랫폼 설치 관리자** 를 다운로드 하 여 앱을 먼저 설치 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-304">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="5cbb6-305">한 번 **웹 플랫폼 설치 관리자** 열려 클릭 **설치** 는 설치 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-305">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="5cbb6-306">![Visual Studio Express 설치](aspnet-mvc-4-custom-action-filters/_static/image12.png "Visual Studio Express 설치")</span><span class="sxs-lookup"><span data-stu-id="5cbb6-306">![Install Visual Studio Express](aspnet-mvc-4-custom-action-filters/_static/image12.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="5cbb6-307">*Visual Studio Express 설치*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-307">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="5cbb6-308">모든 제품의 라이선스 및 용어를 읽고 클릭 **동의** 를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-308">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![사용 조건 동의](aspnet-mvc-4-custom-action-filters/_static/image13.png)

    <span data-ttu-id="5cbb6-310">*사용 조건 동의*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-310">*Accepting the license terms*</span></span>
5. <span data-ttu-id="5cbb6-311">다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-311">Wait until the downloading and installation process completes.</span></span>

    ![설치 진행률](aspnet-mvc-4-custom-action-filters/_static/image14.png)

    <span data-ttu-id="5cbb6-313">*설치 진행률*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-313">*Installation progress*</span></span>
6. <span data-ttu-id="5cbb6-314">설치가 완료 되 면 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-314">When the installation completes, click **Finish**.</span></span>

    ![설치 완료](aspnet-mvc-4-custom-action-filters/_static/image15.png)

    <span data-ttu-id="5cbb6-316">*설치 완료*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-316">*Installation completed*</span></span>
7. <span data-ttu-id="5cbb6-317">클릭 **종료** 를 웹 플랫폼 설치 관리자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-317">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="5cbb6-318">Visual Studio Express for Web을 열려면로 이동는 **시작** 화면를 쓰기 시작할 &quot; **VS Express**&quot;, 클릭는 **VS Express for Web** 바둑판식 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-318">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![웹 타일에 대 한 VS Express](aspnet-mvc-4-custom-action-filters/_static/image16.png)

    <span data-ttu-id="5cbb6-320">*웹 타일에 대 한 VS Express*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-320">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="5cbb6-321">부록 b: 웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="5cbb6-321">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="5cbb6-322">이 부록에서는 Windows Azure 관리 포털에서 새 웹 사이트를 만들고 Windows Azure에서 제공 하는 웹 배포 게시 기능을 활용 하기 위해 랩에서 수행 하 여 가져온 응용 프로그램을 게시 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-322">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="5cbb6-323">작업 1-Windows에서 새 웹 사이트를 만드는 Azure 포털</span><span class="sxs-lookup"><span data-stu-id="5cbb6-323">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="5cbb6-324">이동 하 여 [Windows Azure 관리 포털](https://manage.windowsazure.com/) 구독에 연결 된 Microsoft 자격 증명을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-324">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5cbb6-325">Windows Azure를 무료로 10 개 ASP.NET 웹 사이트를 호스트 하 고 트래픽이 증가 됨을 확장 한 다음 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-325">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="5cbb6-326">등록할 수 [여기](http://aka.ms/aspnet-hol-azure)합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-326">You can sign up [here](http://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="5cbb6-327">![Windows Azure 포털에 로그온](aspnet-mvc-4-custom-action-filters/_static/image17.png "Windows Azure 포털에 로그인")</span><span class="sxs-lookup"><span data-stu-id="5cbb6-327">![Log on to Windows Azure portal](aspnet-mvc-4-custom-action-filters/_static/image17.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="5cbb6-328">*Windows Azure 관리 포털에 로그온*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-328">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="5cbb6-329">클릭 **새로** 명령 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-329">Click **New** on the command bar.</span></span>

    <span data-ttu-id="5cbb6-330">![새 웹 사이트를 만드는](aspnet-mvc-4-custom-action-filters/_static/image18.png "새 웹 사이트 만들기")</span><span class="sxs-lookup"><span data-stu-id="5cbb6-330">![Creating a new Web Site](aspnet-mvc-4-custom-action-filters/_static/image18.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="5cbb6-331">*새 웹 사이트 만들기*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-331">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="5cbb6-332">클릭 **계산** | **웹 사이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-332">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="5cbb6-333">그런 다음 선택 **빠른 생성** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-333">Then select **Quick Create** option.</span></span> <span data-ttu-id="5cbb6-334">새 웹 사이트에 대 한 사용 가능한 URL을 입력 하 고 클릭 **웹 사이트 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-334">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5cbb6-335">Windows Azure 웹 사이트는 호스트를 제어 하 고 관리할 수 있는 클라우드에서 실행 되는 웹 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-335">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="5cbb6-336">빨리 만들기 옵션을 사용 하면 완성 된 웹 응용 프로그램을 Windows Azure 웹 사이트에서 포털 외부에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-336">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="5cbb6-337">데이터베이스를 설정 하기 위한 단계는 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-337">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="5cbb6-338">![빠른 생성을 사용 하 여 새 웹 사이트를 만드는](aspnet-mvc-4-custom-action-filters/_static/image19.png "빠른 생성을 사용 하 여 새 웹 사이트 만들기")</span><span class="sxs-lookup"><span data-stu-id="5cbb6-338">![Creating a new Web Site using Quick Create](aspnet-mvc-4-custom-action-filters/_static/image19.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="5cbb6-339">*빠른 생성을 사용 하 여 새 웹 사이트 만들기*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-339">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="5cbb6-340">새 될 때까지 기다렸다가 **웹 사이트** 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-340">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="5cbb6-341">웹 사이트가 만들어지면 아래 링크를 클릭 하 고 **URL** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-341">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="5cbb6-342">새 웹 사이트가 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-342">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="5cbb6-343">![새 웹 사이트를 찾아](aspnet-mvc-4-custom-action-filters/_static/image20.png "새 웹 사이트를 검색 합니다.")</span><span class="sxs-lookup"><span data-stu-id="5cbb6-343">![Browsing to the new web site](aspnet-mvc-4-custom-action-filters/_static/image20.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="5cbb6-344">*새 웹 사이트를 검색합니다.*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-344">*Browsing to the new web site*</span></span>

    <span data-ttu-id="5cbb6-345">![실행 중인 웹 사이트](aspnet-mvc-4-custom-action-filters/_static/image21.png "실행 중인 웹 사이트")</span><span class="sxs-lookup"><span data-stu-id="5cbb6-345">![Web site running](aspnet-mvc-4-custom-action-filters/_static/image21.png "Web site running")</span></span>

    <span data-ttu-id="5cbb6-346">*실행 중인 웹 사이트*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-346">*Web site running*</span></span>
6. <span data-ttu-id="5cbb6-347">포털로 돌아가서 아래에서 웹 사이트의 이름을 클릭는 **이름** 관리 페이지를 표시 하는 열입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-347">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="5cbb6-348">![웹 사이트 관리 페이지 열기](aspnet-mvc-4-custom-action-filters/_static/image22.png "웹 사이트 관리 페이지 열기")</span><span class="sxs-lookup"><span data-stu-id="5cbb6-348">![Opening the web site management pages](aspnet-mvc-4-custom-action-filters/_static/image22.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="5cbb6-349">*웹 사이트 관리 페이지 열기*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-349">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="5cbb6-350">에 **대시보드** 페이지의 **눈에 보는** 섹션에서 클릭는 **게시 프로필 다운로드** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-350">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5cbb6-351">*게시 프로필* 각각의 활성화 된 게시 방법에 대 한 Windows Azure 웹 사이트에 웹 응용 프로그램을 게시 하는 데 필요한 정보가 모두 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-351">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="5cbb6-352">게시 프로필에는 Url, 사용자 자격 증명 및 연결 하 고 각 게시 메서드를 사용할 수 있는 끝점에 대해 인증 하는 데 필요한 데이터베이스 문자열이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-352">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="5cbb6-353">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** 및 **Microsoft Visual Studio 2012** 읽는 지원 하기 위해 게시 프로필에 대 한 이러한 프로그램의 구성을 자동화 Windows Azure 웹 사이트에 웹 응용 프로그램을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-353">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="5cbb6-354">![게시 프로필 다운로드 웹 사이트](aspnet-mvc-4-custom-action-filters/_static/image23.png "게시 프로필 다운로드 웹 사이트")</span><span class="sxs-lookup"><span data-stu-id="5cbb6-354">![Downloading the web site publish profile](aspnet-mvc-4-custom-action-filters/_static/image23.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="5cbb6-355">*게시 프로필 다운로드 웹 사이트*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-355">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="5cbb6-356">알려진된 위치에 게시 프로필 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-356">Download the publish profile file to a known location.</span></span> <span data-ttu-id="5cbb6-357">더 이상이 연습에서는 Visual Studio에서 웹 응용 프로그램 Windows Azure 웹 사이트를 게시 하려면이 파일을 사용 하는 방법을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-357">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="5cbb6-358">![게시 프로필 파일을 저장](aspnet-mvc-4-custom-action-filters/_static/image24.png "게시 프로필 저장")</span><span class="sxs-lookup"><span data-stu-id="5cbb6-358">![Saving the publish profile file](aspnet-mvc-4-custom-action-filters/_static/image24.png "Saving the publish profile")</span></span>

    <span data-ttu-id="5cbb6-359">*게시 프로필 파일을 저장합니다.*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-359">*Saving the publish profile file*</span></span>

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="5cbb6-360">작업 2-데이터베이스 서버 구성</span><span class="sxs-lookup"><span data-stu-id="5cbb6-360">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="5cbb6-361">응용 프로그램에서 SQL Server를 활용 하는 경우 데이터베이스를 SQL 데이터베이스 서버 만들기 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-361">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="5cbb6-362">SQL Server를 사용 하지 않는 간단한 응용 프로그램을 배포 하려는 경우이 태스크를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-362">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="5cbb6-363">응용 프로그램 데이터베이스를 저장 하기 위해 SQL 데이터베이스 서버를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-363">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="5cbb6-364">Windows Azure 관리 포털에서 구독의 SQL 데이터베이스 서버를 볼 수 있습니다 **Sql 데이터베이스** | **서버** | **서버 대시보드**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-364">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="5cbb6-365">만든 서버 없는 경우 수행 하 여 만들 수 있습니다는 **추가** 명령 모음에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-365">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="5cbb6-366">기록해는 **서버 이름 및 URL, 관리자 로그인 이름 및 암호**, 다음 작업에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-366">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="5cbb6-367">만들지 마십시오 데이터베이스 아직 대로 이후 단계에서 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-367">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="5cbb6-368">![SQL 데이터베이스 서버 대시보드](aspnet-mvc-4-custom-action-filters/_static/image25.png "SQL 데이터베이스 서버 대시보드")</span><span class="sxs-lookup"><span data-stu-id="5cbb6-368">![SQL Database Server Dashboard](aspnet-mvc-4-custom-action-filters/_static/image25.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="5cbb6-369">*SQL 데이터베이스 서버 대시보드*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-369">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="5cbb6-370">다음 태스크에서는 서버 목록에 사용자의 로컬 IP 주소를 포함 해야 이러한 이유로 Visual Studio에서 데이터베이스 연결을 테스트 **허용 IP 주소**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-370">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="5cbb6-371">작업을 수행 하려면 **구성**에서 IP 주소를 선택 **현재 클라이언트 IP 주소** 에 붙여넣습니다는 **시작 IP 주소** 및 **끝IP주소** 클릭 하 고 텍스트 상자는 ![add-client-ip-address-ok-button](aspnet-mvc-4-custom-action-filters/_static/image26.png) 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-371">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](aspnet-mvc-4-custom-action-filters/_static/image26.png) button.</span></span>

    ![클라이언트 IP 주소를 추가합니다.](aspnet-mvc-4-custom-action-filters/_static/image27.png)

    <span data-ttu-id="5cbb6-373">*클라이언트 IP 주소를 추가합니다.*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-373">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="5cbb6-374">한 번는 **클라이언트 IP 주소** 허용된 된 IP 주소에 추가 됩니다 목록에서 클릭 **저장** 하 여 변경 사항을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-374">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![변경 확인](aspnet-mvc-4-custom-action-filters/_static/image28.png)

    <span data-ttu-id="5cbb6-376">*변경 확인*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-376">*Confirm Changes*</span></span>

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="5cbb6-377">작업 3-웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="5cbb6-377">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="5cbb6-378">ASP.NET MVC 4 솔루션으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-378">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="5cbb6-379">에 **솔루션 탐색기**웹 사이트 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-379">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="5cbb6-380">![응용 프로그램을 게시](aspnet-mvc-4-custom-action-filters/_static/image29.png "응용 프로그램을 게시")</span><span class="sxs-lookup"><span data-stu-id="5cbb6-380">![Publishing the Application](aspnet-mvc-4-custom-action-filters/_static/image29.png "Publishing the Application")</span></span>

    <span data-ttu-id="5cbb6-381">*웹 사이트를 게시*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-381">*Publishing the web site*</span></span>
2. <span data-ttu-id="5cbb6-382">첫 번째 작업에서 저장 한 게시 프로필을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-382">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="5cbb6-383">![게시 프로필 가져오기](aspnet-mvc-4-custom-action-filters/_static/image30.png "게시 프로필 가져오기")</span><span class="sxs-lookup"><span data-stu-id="5cbb6-383">![Importing the publish profile](aspnet-mvc-4-custom-action-filters/_static/image30.png "Importing the publish profile")</span></span>

    <span data-ttu-id="5cbb6-384">*게시 프로필 가져오기*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-384">*Importing publish profile*</span></span>
3. <span data-ttu-id="5cbb6-385">클릭 **연결 확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-385">Click **Validate Connection**.</span></span> <span data-ttu-id="5cbb6-386">유효성 검사가 완료 되 면 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-386">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5cbb6-387">연결 유효성 검사 단추 옆에 표시 녹색 확인 표시가 표시 되 면 유효성 검사가 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-387">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="5cbb6-388">![연결 유효성 검사](aspnet-mvc-4-custom-action-filters/_static/image31.png "연결 유효성 검사")</span><span class="sxs-lookup"><span data-stu-id="5cbb6-388">![Validating connection](aspnet-mvc-4-custom-action-filters/_static/image31.png "Validating connection")</span></span>

    <span data-ttu-id="5cbb6-389">*연결 유효성 검사*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-389">*Validating connection*</span></span>
4. <span data-ttu-id="5cbb6-390">에 **설정** 페이지의 **데이터베이스** 섹션에서 데이터베이스 연결의 텍스트 상자 옆의 단추 클릭 (즉, **DefaultConnection**).</span><span class="sxs-lookup"><span data-stu-id="5cbb6-390">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="5cbb6-391">![웹 배포 구성](aspnet-mvc-4-custom-action-filters/_static/image32.png "웹 배포 구성")</span><span class="sxs-lookup"><span data-stu-id="5cbb6-391">![Web deploy configuration](aspnet-mvc-4-custom-action-filters/_static/image32.png "Web deploy configuration")</span></span>

    <span data-ttu-id="5cbb6-392">*웹 배포 구성*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-392">*Web deploy configuration*</span></span>
5. <span data-ttu-id="5cbb6-393">다음과 같이 데이터베이스 연결을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-393">Configure the database connection as follows:</span></span>

    - <span data-ttu-id="5cbb6-394">에 **서버 이름** SQL 데이터베이스 서버 URL 사용 하 여 입력 된 *tcp:* 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-394">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
    - <span data-ttu-id="5cbb6-395">**사용자 이름** 서버 관리자 로그인 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-395">In **User name** type your server administrator login name.</span></span>
    - <span data-ttu-id="5cbb6-396">**암호** 서버 관리자 로그인 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-396">In **Password** type your server administrator login password.</span></span>
    - <span data-ttu-id="5cbb6-397">새 데이터베이스 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-397">Type a new database name.</span></span>

    <span data-ttu-id="5cbb6-398">![대상 연결 문자열 구성](aspnet-mvc-4-custom-action-filters/_static/image33.png "대상 연결 문자열 구성")</span><span class="sxs-lookup"><span data-stu-id="5cbb6-398">![Configuring destination connection string](aspnet-mvc-4-custom-action-filters/_static/image33.png "Configuring destination connection string")</span></span>

    <span data-ttu-id="5cbb6-399">*대상 연결 문자열 구성*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-399">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="5cbb6-400">그런 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-400">Then click **OK**.</span></span> <span data-ttu-id="5cbb6-401">데이터베이스를 만들려는 대화 상자가 나타나면 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-401">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="5cbb6-402">![데이터베이스를 만드는](aspnet-mvc-4-custom-action-filters/_static/image34.png "데이터베이스 문자열 만들기")</span><span class="sxs-lookup"><span data-stu-id="5cbb6-402">![Creating the database](aspnet-mvc-4-custom-action-filters/_static/image34.png "Creating the database string")</span></span>

    <span data-ttu-id="5cbb6-403">*데이터베이스를 만드는 중*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-403">*Creating the database*</span></span>
7. <span data-ttu-id="5cbb6-404">Windows azure에서 SQL 데이터베이스에 연결 하기 위해 사용할 연결 문자열은 기본 연결 텍스트 상자 내에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-404">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="5cbb6-405">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-405">Then click **Next**.</span></span>

    <span data-ttu-id="5cbb6-406">![SQL 데이터베이스를 가리키는 연결 문자열](aspnet-mvc-4-custom-action-filters/_static/image35.png "SQL 데이터베이스를 가리키는 연결 문자열")</span><span class="sxs-lookup"><span data-stu-id="5cbb6-406">![Connection string pointing to SQL Database](aspnet-mvc-4-custom-action-filters/_static/image35.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="5cbb6-407">*SQL 데이터베이스를 가리키는 연결 문자열*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-407">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="5cbb6-408">에 **미리 보기** 페이지 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-408">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="5cbb6-409">![웹 응용 프로그램을 게시](aspnet-mvc-4-custom-action-filters/_static/image36.png "웹 응용 프로그램 게시")</span><span class="sxs-lookup"><span data-stu-id="5cbb6-409">![Publishing the web application](aspnet-mvc-4-custom-action-filters/_static/image36.png "Publishing the web application")</span></span>

    <span data-ttu-id="5cbb6-410">*웹 응용 프로그램 게시*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-410">*Publishing the web application*</span></span>
9. <span data-ttu-id="5cbb6-411">게시 프로세스가 완료 되 면 게시 된 웹 사이트 기본 브라우저가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-411">Once the publishing process finishes, your default browser will open the published web site.</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a><span data-ttu-id="5cbb6-412">부록 c: 코드 조각을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="5cbb6-412">Appendix C: Using Code Snippets</span></span>

<span data-ttu-id="5cbb6-413">코드 조각 바로 쉽게 얻습니다 필요한 코드를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-413">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="5cbb6-414">랩 문서는 알려 정확 하 게 사용 가능 시기, 다음 그림에 나와 있는 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-414">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="5cbb6-415">![Visual Studio 코드 조각을 프로젝트에 코드 삽입을 사용 하 여](aspnet-mvc-4-custom-action-filters/_static/image37.png "Visual Studio를 사용 하 여 코드 조각을 프로젝트에 코드를 삽입 하려면")</span><span class="sxs-lookup"><span data-stu-id="5cbb6-415">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-custom-action-filters/_static/image37.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="5cbb6-416">*Visual Studio 코드 조각을 프로젝트에 코드 삽입을 사용 하 여*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-416">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="5cbb6-417">***키보드 (C#만)를 사용 하 여 코드 조각을 추가 하려면***</span><span class="sxs-lookup"><span data-stu-id="5cbb6-417">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="5cbb6-418">코드를 삽입 하려는 위치에 커서를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-418">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="5cbb6-419">공백 또는 하이픈만) (없이 코드 조각 이름을 입력 하기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-419">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="5cbb6-420">IntelliSense 표시 조각 이름과 일치 하는 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-420">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="5cbb6-421">올바른 코드 조각 선택 (또는 전체 코드 조각이 이름이 선택 될 때까지 입력 유지).</span><span class="sxs-lookup"><span data-stu-id="5cbb6-421">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="5cbb6-422">커서 위치에 코드 조각을 삽입 하려면 두 번 탭 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-422">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="5cbb6-423">![코드 조각 이름을 입력 하기 시작](aspnet-mvc-4-custom-action-filters/_static/image38.png "조각 이름을 입력 하기 시작")</span><span class="sxs-lookup"><span data-stu-id="5cbb6-423">![Start typing the snippet name](aspnet-mvc-4-custom-action-filters/_static/image38.png "Start typing the snippet name")</span></span>

<span data-ttu-id="5cbb6-424">*코드 조각 이름을 입력 하기 시작*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-424">*Start typing the snippet name*</span></span>

<span data-ttu-id="5cbb6-425">![Tab 키를 눌러 강조 표시 된 코드 조각 선택](aspnet-mvc-4-custom-action-filters/_static/image39.png "Tab 키를 눌러 강조 표시 된 코드 조각 선택")</span><span class="sxs-lookup"><span data-stu-id="5cbb6-425">![Press Tab to select the highlighted snippet](aspnet-mvc-4-custom-action-filters/_static/image39.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="5cbb6-426">*Tab 키를 눌러 강조 표시 된 코드 조각 선택*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-426">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="5cbb6-427">![확장 하 고 Tab 키를 눌러 다시 코드 조각](aspnet-mvc-4-custom-action-filters/_static/image40.png "확장 하 고 Tab 키를 눌러 다시 코드 조각")</span><span class="sxs-lookup"><span data-stu-id="5cbb6-427">![Press Tab again and the snippet will expand](aspnet-mvc-4-custom-action-filters/_static/image40.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="5cbb6-428">*확장 하 고 Tab 키를 눌러 다시 코드 조각*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-428">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="5cbb6-429">***마우스 (C#, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가 하려면*** 1입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-429">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="5cbb6-430">코드 조각을 삽입 하려면 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-430">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="5cbb6-431">선택 **조각 삽입** 이어서 **내 코드 조각**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-431">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="5cbb6-432">클릭 하 여 목록에서 관련 조각을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbb6-432">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="5cbb6-433">![코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추로 클릭](aspnet-mvc-4-custom-action-filters/_static/image41.png "코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추 클릭")</span><span class="sxs-lookup"><span data-stu-id="5cbb6-433">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-custom-action-filters/_static/image41.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="5cbb6-434">*코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추로 클릭*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-434">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="5cbb6-435">![클릭 하 여 목록에서 관련 조각을 선택](aspnet-mvc-4-custom-action-filters/_static/image42.png "클릭 하 여 목록에서 관련 조각을 선택")</span><span class="sxs-lookup"><span data-stu-id="5cbb6-435">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-custom-action-filters/_static/image42.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="5cbb6-436">*클릭 하 여 목록에서 관련 조각을 선택합니다*</span><span class="sxs-lookup"><span data-stu-id="5cbb6-436">*Pick the relevant snippet from the list, by clicking on it*</span></span>
