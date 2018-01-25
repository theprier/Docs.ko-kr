---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-dependency-injection
title: "ASP.NET MVC 4 종속성 주입 | Microsoft Docs"
author: rick-anderson
description: "참고:이 실습 랩 ASP.NET MVC 4 및 ASP.NET MVC 필터에 대 한 기본 지식이 있다고 가정 합니다. ASP.NET MVC 4 필터 하기 전에 사용 하지 않은 rec... 하는 경우"
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: 84c7baca-1c54-4c44-8f52-4282122d6acb
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: 48a7d7fdb670aebb72450fc4eb12a364ef595c53
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="aspnet-mvc-4-dependency-injection"></a><span data-ttu-id="c61a6-104">ASP.NET MVC 4 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="c61a6-104">ASP.NET MVC 4 Dependency Injection</span></span>
====================
<span data-ttu-id="c61a6-105">으로 [웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="c61a6-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> [!NOTE]
> <span data-ttu-id="c61a6-106">이 실습 랩 대 한 기본 지식이 있다고 가정 하 고 **ASP.NET MVC** 및 **필터링 하는 ASP.NET MVC 4**합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-106">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC** and **ASP.NET MVC 4 filters**.</span></span> <span data-ttu-id="c61a6-107">사용 하지 않은 경우 **필터링 하는 ASP.NET MVC 4** 를 권장 앞, **ASP.NET MVC 사용자 지정 작업 필터** 실습 랩입니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-107">If you have not used **ASP.NET MVC 4 filters** before, we recommend you to go over **ASP.NET MVC Custom Action Filters** Hands-on Lab.</span></span>
> 
> <span data-ttu-id="c61a6-108">모든 샘플 코드와 코드 조각을 웹 캠프 교육 키트에서 사용할 수에 포함 된 [https://www.microsoft.com/download/29843](https://www.microsoft.com/download/29843)합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-108">All sample code and snippets are included in the Web Camps Training Kit, available at [https://www.microsoft.com/download/29843](https://www.microsoft.com/download/29843).</span></span>


<span data-ttu-id="c61a6-109">**개체 지향 프로그래밍** 패러다임을 개체가 함께 동작 하는 공동 작업 모델에 없는 다음 참가자와 소비자입니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-109">In **Object Oriented Programming** paradigm, objects work together in a collaboration model where there are contributors and consumers.</span></span> <span data-ttu-id="c61a6-110">당연히이 통신 모델 개체 및 복잡성이 증가 하는 경우 관리 하기 어려운 되 고 구성 요소 간의 종속성을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-110">Naturally, this communication model generates dependencies between objects and components, becoming difficult to manage when complexity increases.</span></span>

<span data-ttu-id="c61a6-111">![종속성 클래스 및 복잡성을 모델링](aspnet-mvc-4-dependency-injection/_static/image1.png "종속성 클래스 및 복잡성을 모델링")</span><span class="sxs-lookup"><span data-stu-id="c61a6-111">![Class dependencies and model complexity](aspnet-mvc-4-dependency-injection/_static/image1.png "Class dependencies and model complexity")</span></span>

<span data-ttu-id="c61a6-112">*모델의 복잡성 및 클래스 종속성*</span><span class="sxs-lookup"><span data-stu-id="c61a6-112">*Class dependencies and model complexity*</span></span>

<span data-ttu-id="c61a6-113">에 대 한 들어보았을는 **팩터리 패턴** 및 인터페이스와 서비스를 사용 하 여 클라이언트 개체가 서비스 위치에 대 한 책임 많습니다 구현 간의 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-113">You have probably heard about the **Factory Pattern** and the separation between the interface and the implementation using services, where the client objects are often responsible for service location.</span></span>

<span data-ttu-id="c61a6-114">종속성 주입 패턴은 Inversion of Control의 특정 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-114">The Dependency Injection pattern is a particular implementation of Inversion of Control.</span></span> <span data-ttu-id="c61a6-115">**(IoC) 제어** 개체 정상적인 작업 수행에 기초가 되는 다른 개체를 만들지 않는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-115">**Inversion of Control (IoC)** means that objects do not create other objects on which they rely to do their work.</span></span> <span data-ttu-id="c61a6-116">대신, (예를 들어 xml 구성 파일)를 외부 소스에서 필요한 개체를 가져올 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-116">Instead, they get the objects that they need from an outside source (for example, an xml configuration file).</span></span>

<span data-ttu-id="c61a6-117">**DI (dependency Injection)** 은 있음을 나타내고이 수행한 개체 개입 없이 일반적으로 생성자 매개 변수를 전달 하는 프레임 워크 구성 요소 속성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-117">**Dependency Injection (DI)** means that this is done without the object intervention, usually by a framework component that passes constructor parameters and set properties.</span></span>

<a id="The_Dependency_Injection_DI_Design_Pattern"></a>
### <a name="the-dependency-injection-di-design-pattern"></a><span data-ttu-id="c61a6-118">종속성 주입 (DI) 디자인 패턴</span><span class="sxs-lookup"><span data-stu-id="c61a6-118">The Dependency Injection (DI) Design Pattern</span></span>

<span data-ttu-id="c61a6-119">종속성 주입의 목표는 하는 상위 수준에서 클라이언트 클래스 (예: *는 골퍼*) 필요한 인터페이스를 충족 하는 항목 (예: *IClub*).</span><span class="sxs-lookup"><span data-stu-id="c61a6-119">At a high level, the goal of Dependency Injection is that a client class (e.g. *the golfer*) needs something that satisfies an interface (e.g. *IClub*).</span></span> <span data-ttu-id="c61a6-120">구체적인 유형 이란 신경 쓰지 않습니다 (예: *WoodClub, IronClub, WedgeClub* 또는 *PutterClub*), 부에서는 문제를 해결 하려면 다른 사용자 (좋은 예: *caddy*).</span><span class="sxs-lookup"><span data-stu-id="c61a6-120">It doesn't care what the concrete type is (e.g. *WoodClub, IronClub, WedgeClub* or *PutterClub*), it wants someone else to handle that (e.g. a good *caddy*).</span></span> <span data-ttu-id="c61a6-121">ASP.NET MVC의 종속성 확인자를 사용 하면 종속성 논리를 다른 곳에 등록할 수 있습니다 (예: 컨테이너 또는 *클럽 모음*).</span><span class="sxs-lookup"><span data-stu-id="c61a6-121">The Dependency Resolver in ASP.NET MVC can allow you to register your dependency logic somewhere else (e.g. a container or a *bag of clubs*).</span></span>

<span data-ttu-id="c61a6-122">![종속성 주입 다이어그램](aspnet-mvc-4-dependency-injection/_static/image2.png "종속성 주입 그림")</span><span class="sxs-lookup"><span data-stu-id="c61a6-122">![Dependency Injection diagram](aspnet-mvc-4-dependency-injection/_static/image2.png "Dependency Injection illustration")</span></span>

<span data-ttu-id="c61a6-123">*종속성 주입-골프 유추*</span><span class="sxs-lookup"><span data-stu-id="c61a6-123">*Dependency Injection - Golf analogy*</span></span>

<span data-ttu-id="c61a6-124">종속성 주입 패턴 및 Inversion of Control을 사용 하는 이점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-124">The advantages of using Dependency Injection pattern and Inversion of Control are the following:</span></span>

- <span data-ttu-id="c61a6-125">클래스 결합을 감소</span><span class="sxs-lookup"><span data-stu-id="c61a6-125">Reduces class coupling</span></span>
- <span data-ttu-id="c61a6-126">코드 다시 사용 증가</span><span class="sxs-lookup"><span data-stu-id="c61a6-126">Increases code reusing</span></span>
- <span data-ttu-id="c61a6-127">코드 유지 관리를 향상 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-127">Improves code maintainability</span></span>
- <span data-ttu-id="c61a6-128">응용 프로그램 테스트 향상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-128">Improves application testing</span></span>

> [!NOTE]
> <span data-ttu-id="c61a6-129">종속성 주입은 경우에 따라 추상 팩터리 디자인 패턴을 비교 하 하지만 두 방법 모두 간에 약간의 차이가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-129">Dependency Injection is sometimes compared with Abstract Factory Design Pattern, but there is a slight difference between both approaches.</span></span> <span data-ttu-id="c61a6-130">DI는 팩터리는 및에서 등록 된 서비스를 호출 하 여 종속성을 해결 하기 위해 뒤에서 작업 하는 프레임 워크를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-130">DI has a Framework working behind to solve dependencies by calling the factories and the registered services.</span></span>


<span data-ttu-id="c61a6-131">종속성 주입 패턴 이해 했으므로 배웁니다이 랩을 통해 ASP.NET MVC 4의 적용 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="c61a6-131">Now that you understand the Dependency Injection Pattern, you will learn throughout this lab how to apply it in ASP.NET MVC 4.</span></span> <span data-ttu-id="c61a6-132">종속성 주입을 사용 하 여 먼저는 **컨트롤러** 데이터베이스 액세스 서비스를 포함 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-132">You will start using Dependency Injection in the **Controllers** to include a database access service.</span></span> <span data-ttu-id="c61a6-133">종속성 주입을 적용 하는 다음으로 **뷰** 서비스를 사용 하 여 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-133">Next, you will apply Dependency Injection to the **Views** to consume a service and show information.</span></span> <span data-ttu-id="c61a6-134">마지막으로 확장 합니다는 DI ASP.NET MVC 4 필터를 솔루션에 사용자 지정 작업 필터를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-134">Finally, you will extend the DI to ASP.NET MVC 4 Filters, injecting a custom action filter in the solution.</span></span>

<span data-ttu-id="c61a6-135">이 실습 랩에서 배우게 됩니다 하는 방법:</span><span class="sxs-lookup"><span data-stu-id="c61a6-135">In this Hands-on Lab, you will learn how to:</span></span>

- <span data-ttu-id="c61a6-136">NuGet 패키지를 사용 하 여 종속성 주입을 위한 ASP.NET MVC 4 Unity와 통합</span><span class="sxs-lookup"><span data-stu-id="c61a6-136">Integrate ASP.NET MVC 4 with Unity for Dependency Injection using NuGet Packages</span></span>
- <span data-ttu-id="c61a6-137">ASP.NET MVC 컨트롤러 내의 종속성 주입을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="c61a6-137">Use Dependency Injection inside an ASP.NET MVC Controller</span></span>
- <span data-ttu-id="c61a6-138">ASP.NET MVC 뷰 내 종속성 주입을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="c61a6-138">Use Dependency Injection inside an ASP.NET MVC View</span></span>
- <span data-ttu-id="c61a6-139">ASP.NET MVC 작업 필터 내부 종속성 주입을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="c61a6-139">Use Dependency Injection inside an ASP.NET MVC Action Filter</span></span>

> [!NOTE]
> <span data-ttu-id="c61a6-140">이 랩에서 Unity.Mvc3 NuGet 패키지를 사용 하는 종속성 확인에 대 한 하지만 ASP.NET MVC 4를 사용 하는 종속성 주입 프레임 워크에 맞게 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-140">This Lab is using Unity.Mvc3 NuGet Package for dependency resolution, but it is possible to adapt any Dependency Injection Framework to work with ASP.NET MVC 4.</span></span>


<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="c61a6-141">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="c61a6-141">Prerequisites</span></span>

<span data-ttu-id="c61a6-142">이 랩을 완료 하려면 다음 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-142">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="c61a6-143">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) 하거나 그 보다 뛰어난 (읽기 [부록 A](#AppendixA) 설치 하는 방법에 대 한 지침은).</span><span class="sxs-lookup"><span data-stu-id="c61a6-143">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="c61a6-144">설정</span><span class="sxs-lookup"><span data-stu-id="c61a6-144">Setup</span></span>

<span data-ttu-id="c61a6-145">**설치 하는 코드 조각**</span><span class="sxs-lookup"><span data-stu-id="c61a6-145">**Installing Code Snippets**</span></span>

<span data-ttu-id="c61a6-146">편의 위해는이 랩에 따라 관리 코드의 대부분 Visual Studio 코드 조각 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-146">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="c61a6-147">실행 코드 조각을 설치 하려면 **.\Source\Setup\CodeSnippets.vsi** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-147">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="c61a6-148">이 문서에서 부록을 참조할 수 사용 하는 방법에 알아봅니다 사용 하 고 Visual Studio 코드 조각에 익숙한 경우 &quot; [부록 b:를 사용 하 여 코드 조각을](#AppendixB)&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-148">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix B: Using Code Snippets](#AppendixB)&quot;.</span></span>

* * *

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="c61a6-149">연습</span><span class="sxs-lookup"><span data-stu-id="c61a6-149">Exercises</span></span>

<span data-ttu-id="c61a6-150">이 실습 랩에서 다음 연습으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-150">This Hands-On Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="c61a6-151">연습 1: 한 컨트롤러를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-151">Exercise 1: Injecting a Controller</span></span>](#Exercise1)
2. [<span data-ttu-id="c61a6-152">연습 2: 뷰를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-152">Exercise 2: Injecting a View</span></span>](#Exercise2)
3. [<span data-ttu-id="c61a6-153">연습 3: 필터를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-153">Exercise 3: Injecting Filters</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="c61a6-154">각 연습 동반 되는 **끝** 연습을 완료 한 후 가져와야 생성 되는 솔루션에 포함 된 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-154">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="c61a6-155">연습을 통해 작업 하는 추가 도움이 필요한 경우이 솔루션 가이드로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-155">You can use this solution as a guide if you need additional help working through the exercises.</span></span>


<span data-ttu-id="c61a6-156">예상 소요 시간: **30 분**합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-156">Estimated time to complete this lab: **30 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Injecting_a_Controller"></a>
### <a name="exercise-1-injecting-a-controller"></a><span data-ttu-id="c61a6-157">연습 1: 한 컨트롤러를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-157">Exercise 1: Injecting a Controller</span></span>

<span data-ttu-id="c61a6-158">이 연습에서는 NuGet 패키지를 사용 하 여 Unity를 통합 하 여 ASP.NET MVC 컨트롤러의 종속성 주입을 사용 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-158">In this exercise, you will learn how to use Dependency Injection in ASP.NET MVC Controllers by integrating Unity using a NuGet Package.</span></span> <span data-ttu-id="c61a6-159">이러한 이유로, 데이터 액세스에서 논리를 분리 하 여 MvcMusicStore 컨트롤러에 서비스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-159">For that reason, you will include services into your MvcMusicStore controllers to separate the logic from the data access.</span></span> <span data-ttu-id="c61a6-160">서비스의 도움을 받아 종속성 주입을 사용 하 여 확인 될 컨트롤러 생성자에서 새 종속성이 생성 됩니다 **Unity**합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-160">The services will create a new dependency in the controller constructor, which will be resolved using Dependency Injection with the help of **Unity**.</span></span>

<span data-ttu-id="c61a6-161">이 방법은 덜 결합 하는 응용 프로그램은 보다 유연 하 고 쉽게 유지 관리 및 테스트를 생성 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-161">This approach will show you how to generate less coupled applications, which are more flexible and easier to maintain and test.</span></span> <span data-ttu-id="c61a6-162">또한 ASP.NET MVC Unity와 통합 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-162">You will also learn how to integrate ASP.NET MVC with Unity.</span></span>

<a id="About_StoreManager_Service"></a>
#### <a name="about-storemanager-service"></a><span data-ttu-id="c61a6-163">StoreManager 서비스에 대 한</span><span class="sxs-lookup"><span data-stu-id="c61a6-163">About StoreManager Service</span></span>

<span data-ttu-id="c61a6-164">라는 저장소 컨트롤러 데이터를 관리 하는 서비스를 포함 하는 이제 begin 솔루션에서 제공 하는 MVC Music Store **StoreService**합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-164">The MVC Music Store provided in the begin solution now includes a service that manages the Store Controller data named **StoreService**.</span></span> <span data-ttu-id="c61a6-165">다음 저장소 서비스 구현을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-165">Below you will find the Store Service implementation.</span></span> <span data-ttu-id="c61a6-166">참고 메서드를 모두 모델 엔터티를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-166">Note that all the methods return Model entities.</span></span>

[!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample1.cs)]

<span data-ttu-id="c61a6-167">**StoreController** 는 begin에서 솔루션 이제 소비 **StoreService**합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-167">**StoreController** from the begin solution now consumes **StoreService**.</span></span> <span data-ttu-id="c61a6-168">모든 데이터 참조에서 제거 된 **StoreController**, 및 현재 데이터 액세스 공급자를 사용 하는 모든 방법을 변경 하지 않고 수정 하는 현재 사용 가능한 **StoreService**합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-168">All the data references were removed from **StoreController**, and now possible to modify the current data access provider without changing any method that consumes **StoreService**.</span></span>

<span data-ttu-id="c61a6-169">아래에 있습니다는 **StoreController** 구현 인 종속성에 **StoreService** 클래스 생성자 내부 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-169">You will find below that the **StoreController** implementation has a dependency with **StoreService** inside the class constructor.</span></span>

> [!NOTE]
> <span data-ttu-id="c61a6-170">이 연습에 도입 된 종속성은 관련이 **Inversion of Control** (IoC).</span><span class="sxs-lookup"><span data-stu-id="c61a6-170">The dependency introduced in this exercise is related to **Inversion of Control** (IoC).</span></span>
> 
> <span data-ttu-id="c61a6-171">**StoreController** 클래스 생성자 수신는 **IStoreService** 클래스 내에서 서비스를 호출을 수행 하는 데 필수적인 형식 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-171">The **StoreController** class constructor receives an **IStoreService** type parameter, which is essential to perform service calls from inside the class.</span></span> <span data-ttu-id="c61a6-172">그러나 **StoreController** 모든 컨트롤러는 ASP.NET MVC와 함께 작동 하도록 되어 있어야 합니다 (매개 변수 없이)와 기본 생성자를 구현 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-172">However, **StoreController** does not implement the default constructor (with no parameters) that any controller must have to work with ASP.NET MVC.</span></span>
> 
> <span data-ttu-id="c61a6-173">종속성을 해결 하려면 (지정 된 형식의 모든 개체를 반환 하는 클래스)는 추상 팩터리에서 생성 하는 컨트롤러에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-173">To resolve the dependency, the controller has to be created by an abstract factory (a class that returns any object of the specified type).</span></span>


[!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample2.cs)]

> [!NOTE]
> <span data-ttu-id="c61a6-174">클래스 선언 된 매개 변수가 없는 생성자가 없습니다 그대로 서비스 개체를 전송 하지 않고는 StoreController 만들려고 시도 하는 경우 오류를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-174">You will get an error when the class tries to create the StoreController without sending the service object, as there is no parameterless constructor declared.</span></span>


<a id="Ex1Task1"></a>

<a id="Task_1_-_Running_the_Application"></a>
#### <a name="task-1---running-the-application"></a><span data-ttu-id="c61a6-175">작업 1-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="c61a6-175">Task 1 - Running the Application</span></span>

<span data-ttu-id="c61a6-176">이 태스크에서는 응용 프로그램 논리에서 데이터 액세스를 구분 하는 저장소 컨트롤러에 서비스를 포함 하는 Begin 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-176">In this task, you will run the Begin application, which includes the service into the Store Controller that separates the data access from the application logic.</span></span>

<span data-ttu-id="c61a6-177">응용 프로그램을 실행할 때 컨트롤러 서비스가 기본적으로 매개 변수로 전달 하지 때 예외가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-177">When running the application, you will receive an exception, as the controller service is not passed as a parameter by default:</span></span>

1. <span data-ttu-id="c61a6-178">열기는 **시작** 솔루션에 있는 **Source\Ex01 주입 Controller\Begin**합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-178">Open the **Begin** solution located in **Source\Ex01-Injecting Controller\Begin**.</span></span>

    1. <span data-ttu-id="c61a6-179">일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 전에 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-179">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="c61a6-180">이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-180">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="c61a6-181">에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="c61a6-181">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
    3. <span data-ttu-id="c61a6-182">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-182">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c61a6-183">NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-183">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="c61a6-184">NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-184">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="c61a6-185">이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-185">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="c61a6-186">키를 눌러 **Ctrl + f 5를 눌러** 디버깅 하지 않고 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-186">Press **Ctrl + F5** to run the application without debugging.</span></span> <span data-ttu-id="c61a6-187">오류 메시지를 받아볼 수 &quot; **이 개체에 대해 정의 된 매개 변수가 없는 생성자가 없습니다**&quot;:</span><span class="sxs-lookup"><span data-stu-id="c61a6-187">You will get the error message &quot;**No parameterless constructor defined for this object**&quot;:</span></span>

    <span data-ttu-id="c61a6-188">![ASP.NET MVC 시작 응용 프로그램을 실행 하는 동안 오류가 발생 했습니다](aspnet-mvc-4-dependency-injection/_static/image3.png "ASP.NET MVC 시작 응용 프로그램을 실행 하는 동안 오류가 발생 했습니다")</span><span class="sxs-lookup"><span data-stu-id="c61a6-188">![Error while running ASP.NET MVC Begin Application](aspnet-mvc-4-dependency-injection/_static/image3.png "Error while running ASP.NET MVC Begin Application")</span></span>

    <span data-ttu-id="c61a6-189">*ASP.NET MVC 시작 응용 프로그램을 실행 하는 동안 오류가 발생 했습니다*</span><span class="sxs-lookup"><span data-stu-id="c61a6-189">*Error while running ASP.NET MVC Begin Application*</span></span>
3. <span data-ttu-id="c61a6-190">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-190">Close the browser.</span></span>

<span data-ttu-id="c61a6-191">다음 단계에서 음악 스토어 솔루션이 컨트롤러에서 필요로 하는 종속성 주입을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-191">In the following steps you will work on the Music Store Solution to inject the dependency this controller needs.</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Including_Unity_into_MvcMusicStore_Solution"></a>
#### <a name="task-2---including-unity-into-mvcmusicstore-solution"></a><span data-ttu-id="c61a6-192">작업 2-MvcMusicStore 솔루션에 포함 하 여 Unity</span><span class="sxs-lookup"><span data-stu-id="c61a6-192">Task 2 - Including Unity into MvcMusicStore Solution</span></span>

<span data-ttu-id="c61a6-193">이 작업에서는 포함 됩니다 **Unity.Mvc3** NuGet 패키지를 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-193">In this task, you will include **Unity.Mvc3** NuGet Package to the solution.</span></span>

> [!NOTE]
> <span data-ttu-id="c61a6-194">Unity.Mvc3 패키지는 ASP.NET MVC 3 용 하는데 ASP.NET MVC 4 완벽 하 게 호환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-194">Unity.Mvc3 package was designed for ASP.NET MVC 3, but it is fully compatible with ASP.NET MVC 4.</span></span>
> 
> <span data-ttu-id="c61a6-195">Unity 인스턴스에 대 한 선택적으로 지원 하 고 확장 가능한 경량 종속성 주입 컨테이너는 하 고 인터 셉 션을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-195">Unity is a lightweight, extensible dependency injection container with optional support for instance and type interception.</span></span> <span data-ttu-id="c61a6-196">그는 모든 유형의.NET 응용 프로그램에서 사용 하기 위해 범용 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-196">It is a general-purpose container for use in any type of .NET application.</span></span> <span data-ttu-id="c61a6-197">포함 하는 종속성 주입 메커니즘에 모든 일반적인 기능을 제공: 개체 만들기, 컨테이너에 구성 요소 구성을 연기 하 여 런타임 및 유연성을에서 종속성을 지정 하 여 요구 사항의 추상화 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-197">It provides all the common features found in dependency injection mechanisms including: object creation, abstraction of requirements by specifying dependencies at runtime and flexibility, by deferring the component configuration to the container.</span></span>


1. <span data-ttu-id="c61a6-198">설치 **Unity.Mvc3** 에서 NuGet 패키지는 **MvcMusicStore** 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="c61a6-198">Install **Unity.Mvc3** NuGet Package in the **MvcMusicStore** project.</span></span> <span data-ttu-id="c61a6-199">이 작업을 수행 하려면 엽니다는 **패키지 관리자 콘솔** 에서 **보기** | **다른 창**합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-199">To do this, open the **Package Manager Console** from **View** | **Other Windows**.</span></span>
2. <span data-ttu-id="c61a6-200">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-200">Run the following command.</span></span>

    <span data-ttu-id="c61a6-201">PMC</span><span class="sxs-lookup"><span data-stu-id="c61a6-201">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-dependency-injection/samples/sample3.ps1)]

    <span data-ttu-id="c61a6-202">![Unity.Mvc3 NuGet 패키지 설치](aspnet-mvc-4-dependency-injection/_static/image4.png "Unity.Mvc3 NuGet 패키지 설치")</span><span class="sxs-lookup"><span data-stu-id="c61a6-202">![Installing Unity.Mvc3 NuGet Package](aspnet-mvc-4-dependency-injection/_static/image4.png "Installing Unity.Mvc3 NuGet Package")</span></span>

    <span data-ttu-id="c61a6-203">*Unity.Mvc3 NuGet 패키지 설치*</span><span class="sxs-lookup"><span data-stu-id="c61a6-203">*Installing Unity.Mvc3 NuGet Package*</span></span>
3. <span data-ttu-id="c61a6-204">한 번의 **Unity.Mvc3** 패키지를 설치, 파일 및 Unity 구성을 단순화 하기 위해 자동으로 추가 하는 폴더를 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-204">Once the **Unity.Mvc3** package is installed, explore the files and folders it automatically adds in order to simplify Unity configuration.</span></span>

    <span data-ttu-id="c61a6-205">![Unity.Mvc3 패키지가 설치](aspnet-mvc-4-dependency-injection/_static/image5.png "Unity.Mvc3 패키지 설치")</span><span class="sxs-lookup"><span data-stu-id="c61a6-205">![Unity.Mvc3 package installed](aspnet-mvc-4-dependency-injection/_static/image5.png "Unity.Mvc3 package installed")</span></span>

    <span data-ttu-id="c61a6-206">*Unity.Mvc3 패키지 설치*</span><span class="sxs-lookup"><span data-stu-id="c61a6-206">*Unity.Mvc3 package installed*</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Registering_Unity_in_Globalasaxcs_Application_Start"></a>
#### <a name="task-3---registering-unity-in-globalasaxcs-applicationstart"></a><span data-ttu-id="c61a6-207">작업 3-Global.asax.cs 응용 프로그램에서 등록 Unity\_시작</span><span class="sxs-lookup"><span data-stu-id="c61a6-207">Task 3 - Registering Unity in Global.asax.cs Application\_Start</span></span>

<span data-ttu-id="c61a6-208">이 태스크에서는 업데이트 됩니다는 **응용 프로그램\_시작** 메서드에 있는 **Global.asax.cs** Unity 부트스트래퍼 이니셜라이저를 호출 하 고 그런 다음 부트스트래퍼 파일 등록을 업데이트 하려면 서비스와 컨트롤러에는 종속성 주입을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-208">In this task, you will update the **Application\_Start** method located in **Global.asax.cs** to call the Unity Bootstrapper initializer and then, update the Bootstrapper file registering the Service and Controller you will use for Dependency Injection.</span></span>

1. <span data-ttu-id="c61a6-209">이제 Unity 컨테이너를 초기화 하는 파일인 부트스트래퍼 및 종속성 확인자를 후크 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-209">Now, you will hook up the Bootstrapper which is the file that initializes the Unity container and Dependency Resolver.</span></span> <span data-ttu-id="c61a6-210">이 위해 열고 **Global.asax.cs** 내에서 강조 표시 된 다음 코드를 추가 하 고는 **응용 프로그램\_시작** 메서드.</span><span class="sxs-lookup"><span data-stu-id="c61a6-210">To do this, open **Global.asax.cs** and add the following highlighted code within the **Application\_Start** method.</span></span>

    <span data-ttu-id="c61a6-211">(코드 조각- *ASP.NET 종속성 주입 랩-Ex01-Unity 초기화*)</span><span class="sxs-lookup"><span data-stu-id="c61a6-211">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex01 - Initialize Unity*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample4.cs)]
2. <span data-ttu-id="c61a6-212">열기 **Bootstrapper.cs** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-212">Open **Bootstrapper.cs** file.</span></span>
3. <span data-ttu-id="c61a6-213">네임 스페이스를 포함: **MvcMusicStore.Services** 및 **MusicStore.Controllers**합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-213">Include the following namespaces: **MvcMusicStore.Services** and **MusicStore.Controllers**.</span></span>

    <span data-ttu-id="c61a6-214">(코드 조각- *ASP.NET 종속성 주입-Ex01-랩 부트스트래퍼 네임 스페이스 추가*)</span><span class="sxs-lookup"><span data-stu-id="c61a6-214">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex01 - Bootstrapper Adding Namespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample5.cs)]
4. <span data-ttu-id="c61a6-215">대체 **BuildUnityContainer** 메서드의 저장소 컨트롤러 및 저장소 서비스를 등록 하는 다음 코드를 사용 하 여 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-215">Replace **BuildUnityContainer** method's content with the following code that registers Store Controller and Store Service.</span></span>

    <span data-ttu-id="c61a6-216">(코드 조각- *ASP.NET 종속성 주입-Ex01-랩 레지스터 저장소 컨트롤러와 서비스*)</span><span class="sxs-lookup"><span data-stu-id="c61a6-216">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex01 - Register Store Controller and Service*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample6.cs)]

<a id="Ex1Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="c61a6-217">작업 4-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="c61a6-217">Task 4 - Running the Application</span></span>

<span data-ttu-id="c61a6-218">이 태스크에서는 해당 로드할 수 있는지 이제 Unity를 포함 한 후 확인 하려면 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-218">In this task, you will run the application to verify that it can now be loaded after including Unity.</span></span>

1. <span data-ttu-id="c61a6-219">키를 눌러 **F5** 응용 프로그램을 실행 하려면 응용 프로그램이 모든 오류 메시지를 표시 하지 않고 로드 이제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-219">Press **F5** to run the application, the application should now load without showing any error message.</span></span>

    <span data-ttu-id="c61a6-220">![종속성 주입 된 응용 프로그램을 실행](aspnet-mvc-4-dependency-injection/_static/image6.png "종속성 주입 된 응용 프로그램을 실행 합니다.")</span><span class="sxs-lookup"><span data-stu-id="c61a6-220">![Running Application with Dependency Injection](aspnet-mvc-4-dependency-injection/_static/image6.png "Running Application with Dependency Injection")</span></span>

    <span data-ttu-id="c61a6-221">*종속성 주입 된 응용 프로그램을 실행합니다.*</span><span class="sxs-lookup"><span data-stu-id="c61a6-221">*Running Application with Dependency Injection*</span></span>
2. <span data-ttu-id="c61a6-222">찾아 **/저장소**합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-222">Browse to **/Store**.</span></span> <span data-ttu-id="c61a6-223">이렇게 하면 **StoreController**를 사용 하 여 이제 만들어지는 **Unity**합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-223">This will invoke **StoreController**, which is now created using **Unity**.</span></span>

    <span data-ttu-id="c61a6-224">![MVC Music Store](aspnet-mvc-4-dependency-injection/_static/image7.png "MVC Music Store")</span><span class="sxs-lookup"><span data-stu-id="c61a6-224">![MVC Music Store](aspnet-mvc-4-dependency-injection/_static/image7.png "MVC Music Store")</span></span>

    <span data-ttu-id="c61a6-225">*MVC Music Store*</span><span class="sxs-lookup"><span data-stu-id="c61a6-225">*MVC Music Store*</span></span>
3. <span data-ttu-id="c61a6-226">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-226">Close the browser.</span></span>

<span data-ttu-id="c61a6-227">다음 연습에서는 ASP.NET MVC 뷰 및 작업 필터 내 사용 하는 종속성 주입 범위를 확장 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-227">In the following exercises you will learn how to extend the Dependency Injection scope to use it inside ASP.NET MVC Views and Action Filters.</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Injecting_a_View"></a>
### <a name="exercise-2-injecting-a-view"></a><span data-ttu-id="c61a6-228">연습 2: 뷰를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-228">Exercise 2: Injecting a View</span></span>

<span data-ttu-id="c61a6-229">이 연습에서는 ASP.NET MVC 4의 새로운 기능으로 보기에서 Unity 통합에 대 한 종속성 주입을 사용 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-229">In this exercise, you will learn how to use Dependency Injection in a view with the new features of ASP.NET MVC 4 for Unity integration.</span></span> <span data-ttu-id="c61a6-230">파일을 수집 하려면 메시지와 아래 이미지를 보여 주는 저장소 찾아보기 보기 내에서 사용자 지정 서비스를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-230">In order to do that, you will call a custom service inside the Store Browse View, which will show a message and an image below.</span></span>

<span data-ttu-id="c61a6-231">그런 다음 프로젝트를 Unity로 통합를 종속성 삽입 하는 사용자 지정 종속성 확인자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-231">Then, you will integrate the project with Unity and create a custom dependency resolver to inject the dependencies.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Creating_a_View_that_Consumes_a_Service"></a>
#### <a name="task-1---creating-a-view-that-consumes-a-service"></a><span data-ttu-id="c61a6-232">작업 1-서비스를 사용 하는 보기를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="c61a6-232">Task 1 - Creating a View that Consumes a Service</span></span>

<span data-ttu-id="c61a6-233">이 태스크에서는 새 종속성을 생성 하는 서비스 호출을 수행 하는 뷰를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-233">In this task, you will create a view that performs a service call to generate a new dependency.</span></span> <span data-ttu-id="c61a6-234">이 솔루션에 포함 된 간단한 메시징 서비스에서 서비스 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-234">The service consists in a simple messaging service included in this solution.</span></span>

1. <span data-ttu-id="c61a6-235">열기는 **시작** 솔루션에 있는 **Source\Ex02 주입 View\Begin** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-235">Open the **Begin** solution located in the **Source\Ex02-Injecting View\Begin** folder.</span></span> <span data-ttu-id="c61a6-236">그렇지 않은 경우 계속 사용할 수도 있습니다는 **끝** 솔루션, 이전 연습을 완료 하 여 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-236">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

    1. <span data-ttu-id="c61a6-237">제공 된 연 경우 **시작** 를 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 솔루션을 계속 하려면.</span><span class="sxs-lookup"><span data-stu-id="c61a6-237">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="c61a6-238">이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-238">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="c61a6-239">에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="c61a6-239">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
    3. <span data-ttu-id="c61a6-240">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-240">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c61a6-241">NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-241">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="c61a6-242">NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-242">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="c61a6-243">이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-243">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
    > 
    > <span data-ttu-id="c61a6-244">자세한 내용은이 문서를 참조 하십시오.: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-244">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="c61a6-245">포함 된 **MessageService.cs** 및 **IMessageService.cs** 클래스에 배치는 **\Assets 원본** 폴더에 **/서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-245">Include the **MessageService.cs** and the **IMessageService.cs** classes located in the **Source \Assets** folder in **/Services**.</span></span> <span data-ttu-id="c61a6-246">이렇게 하려면 마우스 오른쪽 단추로 클릭 **서비스** 폴더와 선택 **기존 항목 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-246">To do this, right-click **Services** folder and select **Add Existing Item**.</span></span> <span data-ttu-id="c61a6-247">파일의 위치를 찾아를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-247">Browse to the files' location and include them.</span></span>

    <span data-ttu-id="c61a6-248">![메시지 서비스 및 서비스 인터페이스 추가](aspnet-mvc-4-dependency-injection/_static/image8.png "메시지 서비스 및 서비스 인터페이스 추가")</span><span class="sxs-lookup"><span data-stu-id="c61a6-248">![Adding Message Service and Service Interface](aspnet-mvc-4-dependency-injection/_static/image8.png "Adding Message Service and Service Interface")</span></span>

    <span data-ttu-id="c61a6-249">*추가 메시지 서비스 및 서비스 인터페이스*</span><span class="sxs-lookup"><span data-stu-id="c61a6-249">*Adding Message Service and Service Interface*</span></span>

    > [!NOTE]
    > <span data-ttu-id="c61a6-250">**IMessageService** 인터페이스에 의해 구현 되는 두 개의 속성을 정의 합니다.는 **MessageService** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-250">The **IMessageService** interface defines two properties implemented by the **MessageService** class.</span></span> <span data-ttu-id="c61a6-251">이러한 속성-**메시지** 및 **ImageUrl**-표시 되는 메시지와 이미지의 URL을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-251">These properties -**Message** and **ImageUrl**- store the message and the URL of the image to be displayed.</span></span>
3. <span data-ttu-id="c61a6-252">폴더 만들기 **페이지/** 프로젝트의 루트 폴더를 한 다음 기존 클래스를 추가 **MyBasePage.cs** 에서 **Source\Assets**합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-252">Create the folder **/Pages** in the project's root folder, and then add the existing class **MyBasePage.cs** from **Source\Assets**.</span></span> <span data-ttu-id="c61a6-253">상속 하는 기본 페이지는 다음과 같은 구조를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-253">The base page you will inherit from has the following structure.</span></span>

    <span data-ttu-id="c61a6-254">![페이지 폴더](aspnet-mvc-4-dependency-injection/_static/image9.png "페이지 폴더")</span><span class="sxs-lookup"><span data-stu-id="c61a6-254">![Pages folder](aspnet-mvc-4-dependency-injection/_static/image9.png "Pages folder")</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample7.cs)]
4. <span data-ttu-id="c61a6-255">열기 **Browse.cshtml** 에서 보려는 **/뷰/저장** 폴더에서 상속 하는 것을 확인 하 고 **MyBasePage.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-255">Open **Browse.cshtml** view from **/Views/Store** folder, and make it inherit from **MyBasePage.cs**.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-dependency-injection/samples/sample8.cshtml)]
5. <span data-ttu-id="c61a6-256">에 **찾아보기** 보기에서 호출을 추가 **MessageService** 이미지 및 서비스에서 검색 메시지를 표시 하려면.</span><span class="sxs-lookup"><span data-stu-id="c61a6-256">In the **Browse** view, add a call to **MessageService** to display an image and a message retrieved by the service.</span></span>
<span data-ttu-id="c61a6-257">(C#)</span><span class="sxs-lookup"><span data-stu-id="c61a6-257">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-dependency-injection/samples/sample9.cshtml)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Including_a_Custom_Dependency_Resolver_and_a_Custom_View_Page_Activator"></a>
#### <a name="task-2---including-a-custom-dependency-resolver-and-a-custom-view-page-activator"></a><span data-ttu-id="c61a6-258">작업 2-사용자 지정 종속성 해결 프로그램 및 사용자 지정 뷰 페이지 활성기를 포함 하 여</span><span class="sxs-lookup"><span data-stu-id="c61a6-258">Task 2 - Including a Custom Dependency Resolver and a Custom View Page Activator</span></span>

<span data-ttu-id="c61a6-259">이전 태스크에서 내부 서비스 호출을 수행 하는 뷰 내 새 종속성을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-259">In the previous task, you injected a new dependency inside a view to perform a service call inside it.</span></span> <span data-ttu-id="c61a6-260">ASP.NET MVC 종속성 주입 인터페이스를 구현 하 여 해당 종속성을 확인 되는 이제 **IViewPageActivator** 및 **되며 IDependencyResolver**합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-260">Now, you will resolve that dependency by implementing the ASP.NET MVC Dependency Injection interfaces **IViewPageActivator** and **IDependencyResolver**.</span></span> <span data-ttu-id="c61a6-261">구현 솔루션에 포함 됩니다 **되며 IDependencyResolver** Unity를 사용 하 여 서비스 검색이 처리 됩니다입니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-261">You will include in the solution an implementation of **IDependencyResolver** that will deal with the service retrieval by using Unity.</span></span> <span data-ttu-id="c61a6-262">다른 사용자 지정 구현을 포함 됩니다는 그런 다음 **IViewPageActivator** 인터페이스 보기 만들기를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-262">Then, you will include another custom implementation of **IViewPageActivator** interface that will solve the creation of the views.</span></span>

> [!NOTE]
> <span data-ttu-id="c61a6-263">ASP.NET MVC 3 이후 종속성 주입을 위한 구현 서비스 등록에 대 한 인터페이스를 간소화 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-263">Since ASP.NET MVC 3, the implementation for Dependency Injection had simplified the interfaces to register services.</span></span> <span data-ttu-id="c61a6-264">**되며 IDependencyResolver** 및 **IViewPageActivator** 종속성 주입을 위한 ASP.NET MVC 3 기능의 일부인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-264">**IDependencyResolver** and **IViewPageActivator** are part of ASP.NET MVC 3 features for Dependency Injection.</span></span>
> 
> <span data-ttu-id="c61a6-265">**-되며 IDependencyResolver** 인터페이스 이전 IMvcServiceLocator를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-265">**- IDependencyResolver** interface replaces the previous IMvcServiceLocator.</span></span> <span data-ttu-id="c61a6-266">되며 IDependencyResolver의 구현자는 서비스나 서비스 컬렉션의 인스턴스를 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-266">Implementers of IDependencyResolver must return an instance of the service or a service collection.</span></span>
>
> 
> [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample10.cs)]
> 
> <span data-ttu-id="c61a6-267">**-IViewPageActivator** 인터페이스는 종속성 주입을 통해 페이지 보기를 인스턴스화하기 하는 방법을 보다 세부적으로 제어를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-267">**- IViewPageActivator** interface provides more fine-grained control over how view pages are instantiated via dependency injection.</span></span> <span data-ttu-id="c61a6-268">구현 하는 클래스 **IViewPageActivator** 인터페이스는 인스턴스 컨텍스트 정보를 사용 하 여 보기를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-268">The classes that implement **IViewPageActivator** interface can create view instances using context information.</span></span>
> 
> 
> [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample11.cs)]


1. <span data-ttu-id="c61a6-269">만들기는 /**팩터리** 프로젝트의 루트 폴더에는 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-269">Create the /**Factories** folder in the project's root folder.</span></span>
2. <span data-ttu-id="c61a6-270">포함 **CustomViewPageActivator.cs** 에서 솔루션에 **원본/자산 / /** 를 **팩터리** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-270">Include **CustomViewPageActivator.cs** to your solution from **/Sources/Assets/** to **Factories** folder.</span></span> <span data-ttu-id="c61a6-271">이렇게 하려면 마우스 오른쪽 단추로 클릭는 **/Factories** 폴더를 **추가 | 기존 항목** 선택한 후 **CustomViewPageActivator.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-271">To do that, right-click the **/Factories** folder, select **Add | Existing Item** and then select **CustomViewPageActivator.cs**.</span></span> <span data-ttu-id="c61a6-272">이 클래스가 구현 하는 **IViewPageActivator** Unity 컨테이너를 보유 하는 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-272">This class implements the **IViewPageActivator** interface to hold the Unity Container.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample12.cs)]

    > [!NOTE]
    > <span data-ttu-id="c61a6-273">**CustomViewPageActivator** Unity 컨테이너를 사용 하 여 뷰 만들기를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-273">**CustomViewPageActivator** is responsible for managing the creation of a view by using a Unity container.</span></span>
3. <span data-ttu-id="c61a6-274">포함 **UnityDependencyResolver.cs** 에서 파일을 **/소스/자산** 를 **/Factories** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-274">Include **UnityDependencyResolver.cs** file from **/Sources/Assets** to **/Factories** folder.</span></span> <span data-ttu-id="c61a6-275">이렇게 하려면 마우스 오른쪽 단추로 클릭는 **/Factories** 폴더를 **추가 | 기존 항목** 선택한 후 **UnityDependencyResolver.cs** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-275">To do that, right-click the **/Factories** folder, select **Add | Existing Item** and then select **UnityDependencyResolver.cs** file.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample13.cs)]

    > [!NOTE]
    > <span data-ttu-id="c61a6-276">**UnityDependencyResolver** 클래스는 Unity에 대 한 사용자 지정 DependencyResolver 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-276">**UnityDependencyResolver** class is a custom DependencyResolver for Unity.</span></span> <span data-ttu-id="c61a6-277">Unity 컨테이너 내 서비스를 찾을 수 없는 경우 기본 해결 프로그램 invocated 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-277">When a service cannot be found inside the Unity container, the base resolver is invocated.</span></span>

<span data-ttu-id="c61a6-278">다음 태스크에서 모델 뷰와 서비스의 위치를 알 수 있도록 두 구현 모두 등록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-278">In the following task both implementations will be registered to let the model know the location of the services and the views.</span></span>

<a id="Ex2Task3"></a>

<a id="Task_3_-_Registering_for_Dependency_Injection_within_Unity_container"></a>
#### <a name="task-3---registering-for-dependency-injection-within-unity-container"></a><span data-ttu-id="c61a6-279">작업 3-Unity 컨테이너 내에서 종속성 주입을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-279">Task 3 - Registering for Dependency Injection within Unity container</span></span>

<span data-ttu-id="c61a6-280">이 작업을 함께 작동 하는 종속성 주입을 확인 하는 모든 이전 것을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-280">In this task, you will put all the previous things together to make Dependency Injection work.</span></span>

<span data-ttu-id="c61a6-281">지금까지 솔루션에 다음과 같은 요소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-281">Up to now your solution has the following elements:</span></span>

- <span data-ttu-id="c61a6-282">A **찾아보기** 에서 상속 되는 보기 **MyBaseClass** 소비 및 **MessageService**합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-282">A **Browse** View that inherits from **MyBaseClass** and consumes **MessageService**.</span></span>
- <span data-ttu-id="c61a6-283">중간 클래스-**MyBaseClass**-이 서비스 인터페이스에 대 한 선언 하는 종속성 주입 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-283">An intermediate class -**MyBaseClass**- that has dependency injection declared for the service interface.</span></span>
- <span data-ttu-id="c61a6-284">서비스-A **MessageService** -및 해당 인터페이스 **IMessageService**합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-284">A service - **MessageService** - and its interface **IMessageService**.</span></span>
- <span data-ttu-id="c61a6-285">-Unity에 대 한 사용자 지정 종속성 확인자 **UnityDependencyResolver** -서비스 검색을 다루는입니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-285">A custom dependency resolver for Unity - **UnityDependencyResolver** - that deals with service retrieval.</span></span>
- <span data-ttu-id="c61a6-286">뷰 페이지 활성기- **CustomViewPageActivator** -하는 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-286">A View Page activator - **CustomViewPageActivator** - that creates the page.</span></span>

<span data-ttu-id="c61a6-287">삽입할 **찾아보기** 보기는 이제 등록 사용자 지정 종속성 확인자 Unity 컨테이너에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-287">To inject **Browse** View, you will now register the custom dependency resolver in the Unity container.</span></span>

1. <span data-ttu-id="c61a6-288">열기 **Bootstrapper.cs** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-288">Open **Bootstrapper.cs** file.</span></span>
2. <span data-ttu-id="c61a6-289">인스턴스 등록 **MessageService** Unity 컨테이너 서비스를 초기화할 수에:</span><span class="sxs-lookup"><span data-stu-id="c61a6-289">Register an instance of **MessageService** into the Unity container to initialize the service:</span></span>

    <span data-ttu-id="c61a6-290">(코드 조각- *ASP.NET 종속성 주입-Ex02-랩 레지스터 메시지 서비스*)</span><span class="sxs-lookup"><span data-stu-id="c61a6-290">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex02 - Register Message Service*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample14.cs)]
3. <span data-ttu-id="c61a6-291">에 대 한 참조를 추가 **MvcMusicStore.Factories** 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-291">Add a reference to **MvcMusicStore.Factories** namespace.</span></span>

    <span data-ttu-id="c61a6-292">(코드 조각- *ASP.NET 종속성 주입-Ex02-랩 팩터리 Namespace*)</span><span class="sxs-lookup"><span data-stu-id="c61a6-292">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex02 - Factories Namespace*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample15.cs)]
4. <span data-ttu-id="c61a6-293">등록 **CustomViewPageActivator** Unity 컨테이너로 뷰 페이지 활성기를로:</span><span class="sxs-lookup"><span data-stu-id="c61a6-293">Register **CustomViewPageActivator** as a View Page activator into the Unity container:</span></span>

    <span data-ttu-id="c61a6-294">(코드 조각- *ASP.NET 종속성 주입-Ex02-랩 레지스터 CustomViewPageActivator*)</span><span class="sxs-lookup"><span data-stu-id="c61a6-294">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex02 - Register CustomViewPageActivator*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample16.cs)]
5. <span data-ttu-id="c61a6-295">ASP.NET MVC 4 기본 종속성 확인자의 인스턴스로 대체 **UnityDependencyResolver**합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-295">Replace ASP.NET MVC 4 default dependency resolver with an instance of **UnityDependencyResolver**.</span></span> <span data-ttu-id="c61a6-296">이 작업을 수행 하려면 대체 **Initialise** 메서드를 다음 코드로 콘텐츠:</span><span class="sxs-lookup"><span data-stu-id="c61a6-296">To do this, replace **Initialise** method content with the following code:</span></span>

    <span data-ttu-id="c61a6-297">(코드 조각- *ASP.NET 종속성 주입-Ex02-랩 업데이트 종속성 확인자*)</span><span class="sxs-lookup"><span data-stu-id="c61a6-297">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex02 - Update Dependency Resolver*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample17.cs)]

    > [!NOTE]
    > <span data-ttu-id="c61a6-298">ASP.NET MVC는 기본 종속성 확인자 클래스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-298">ASP.NET MVC provides a default dependency resolver class.</span></span> <span data-ttu-id="c61a6-299">Unity에 작성 한 것으로 사용자 지정 종속성 확인자를 사용 하려면이 확인자 교체에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-299">To work with custom dependency resolvers as the one we have created for unity, this resolver has to be replaced.</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="c61a6-300">작업 4-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="c61a6-300">Task 4 - Running the Application</span></span>

<span data-ttu-id="c61a6-301">이 작업에서는 저장소 브라우저 서비스를 사용 하 고 이미지와 검색 한 메시지를 표시 합니다. 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-301">In this task, you will run the application to verify that the Store Browser consumes the service and shows the image and the message retrieved:</span></span>

1. <span data-ttu-id="c61a6-302">**F5** 키를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-302">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="c61a6-303">클릭 **록** 참조 고 장르 메뉴 내에서 방법을 **MessageService** 뷰에 삽입 된 고 환영 메시지와 이미지를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-303">Click **Rock** within the Genres Menu and see how the **MessageService** was injected to the view and loaded the welcome message and the image.</span></span> <span data-ttu-id="c61a6-304">이 예제에 진입 하 고 &quot; **록**&quot;:</span><span class="sxs-lookup"><span data-stu-id="c61a6-304">In this example, we are entering to &quot;**Rock**&quot;:</span></span>

    <span data-ttu-id="c61a6-305">![MVC Music Store 보기 주입](aspnet-mvc-4-dependency-injection/_static/image10.png "MVC Music Store 보기 삽입")</span><span class="sxs-lookup"><span data-stu-id="c61a6-305">![MVC Music Store - View Injection](aspnet-mvc-4-dependency-injection/_static/image10.png "MVC Music Store - View Injection")</span></span>

    <span data-ttu-id="c61a6-306">*MVC Music Store 보기 삽입*</span><span class="sxs-lookup"><span data-stu-id="c61a6-306">*MVC Music Store - View Injection*</span></span>
3. <span data-ttu-id="c61a6-307">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-307">Close the browser.</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Injecting_Action_Filters"></a>
### <a name="exercise-3-injecting-action-filters"></a><span data-ttu-id="c61a6-308">연습 3: 작업 필터를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-308">Exercise 3: Injecting Action Filters</span></span>

<span data-ttu-id="c61a6-309">이전 실습 랩에서 **사용자 지정 작업 필터** 사용자 지정 필터 및 삽입 작업을 수행한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-309">In the previous Hands-On lab **Custom Action Filters** you have worked with filters customization and injection.</span></span> <span data-ttu-id="c61a6-310">이 연습에서는 Unity 컨테이너를 사용 하 여 종속성 주입으로 필터를 삽입 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-310">In this exercise, you will learn how to inject filters with Dependency Injection by using the Unity container.</span></span> <span data-ttu-id="c61a6-311">이렇게 하려면 추가 합니다 Music Store 솔루션에 사용자 지정 작업 필터를 사이트의 활동을 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-311">To do that, you will add to the Music Store solution a custom action filter that will trace the activity of the site.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Including_the_Tracking_Filter_in_the_Solution"></a>
#### <a name="task-1---including-the-tracking-filter-in-the-solution"></a><span data-ttu-id="c61a6-312">1-추적 필터를 포함 하 여 솔루션의 작업</span><span class="sxs-lookup"><span data-stu-id="c61a6-312">Task 1 - Including the Tracking Filter in the Solution</span></span>

<span data-ttu-id="c61a6-313">이 작업에 포함할 음악 스토어 추적 이벤트에 사용자 지정 작업 필터.</span><span class="sxs-lookup"><span data-stu-id="c61a6-313">In this task, you will include in the Music Store a custom action filter to trace events.</span></span> <span data-ttu-id="c61a6-314">사용자 지정 작업 필터도 개념 이미에서 처리 되는 이전 랩 &quot;사용자 지정 작업 필터&quot;,에서는 바로이 랩의 자산 폴더에서 필터 클래스를 포함 하 고 다음 Unity에 대 한 필터 공급자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-314">As custom action filter concepts are already treated in the previous Lab &quot;Custom Action Filters&quot;, you will just include the filter class from the Assets folder of this lab, and then create a Filter Provider for Unity:</span></span>

1. <span data-ttu-id="c61a6-315">열기는 **시작** 솔루션에 있는 **Source\Ex03-삽입 작업 Filter\Begin** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-315">Open the **Begin** solution located in the **Source\Ex03 - Injecting Action Filter\Begin** folder.</span></span> <span data-ttu-id="c61a6-316">그렇지 않은 경우 계속 사용할 수도 있습니다는 **끝** 솔루션, 이전 연습을 완료 하 여 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-316">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

    1. <span data-ttu-id="c61a6-317">제공 된 연 경우 **시작** 를 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 솔루션을 계속 하려면.</span><span class="sxs-lookup"><span data-stu-id="c61a6-317">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="c61a6-318">이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-318">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="c61a6-319">에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="c61a6-319">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
    3. <span data-ttu-id="c61a6-320">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-320">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c61a6-321">NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-321">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="c61a6-322">NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-322">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="c61a6-323">이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-323">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
    > 
    > <span data-ttu-id="c61a6-324">자세한 내용은이 문서를 참조 하십시오.: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-324">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="c61a6-325">포함 **TraceActionFilter.cs** 에서 파일을 **/소스/자산** 를 **필터링/** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-325">Include **TraceActionFilter.cs** file from **/Sources/Assets** to **/Filters** folder.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample18.cs)]

    > [!NOTE]
    > <span data-ttu-id="c61a6-326">이 사용자 지정 작업 필터는 ASP.NET 추적을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-326">This custom action filter performs ASP.NET tracing.</span></span> <span data-ttu-id="c61a6-327">확인할 수 있습니다 &quot;로컬 ASP.NET MVC 4 및 작업 필터를 동적&quot; 추가 참조에 대 한 랩입니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-327">You can check &quot;ASP.NET MVC 4 local and Dynamic Action Filters&quot; Lab for more reference.</span></span>
3. <span data-ttu-id="c61a6-328">빈 클래스 추가 **FilterProvider.cs** 프로젝트 폴더에   **/필터링 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c61a6-328">Add the empty class **FilterProvider.cs** to the project in the folder **/Filters.**</span></span>
4. <span data-ttu-id="c61a6-329">추가 **System.Web.Mvc** 및 **Microsoft.Practices.Unity** 네임 스페이스에 **FilterProvider.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-329">Add the **System.Web.Mvc** and **Microsoft.Practices.Unity** namespaces in **FilterProvider.cs**.</span></span>

    <span data-ttu-id="c61a6-330">(코드 조각- *ASP.NET 종속성 주입-Ex03-랩 필터 공급자 네임 스페이스 추가*)</span><span class="sxs-lookup"><span data-stu-id="c61a6-330">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Filter Provider Adding Namespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample19.cs)]
5. <span data-ttu-id="c61a6-331">클래스에서 상속 **IFilterProvider** 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-331">Make the class inherit from **IFilterProvider** Interface.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample20.cs)]
6. <span data-ttu-id="c61a6-332">추가 **IUnityContainer** 속성에는 **FilterProvider** 클래스, 한 다음 컨테이너를 할당 하는 클래스 생성자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-332">Add a **IUnityContainer** property in the **FilterProvider** class, and then create a class constructor to assign the container.</span></span>

    <span data-ttu-id="c61a6-333">(코드 조각- *ASP.NET 종속성 주입-Ex03-랩 필터 공급자 생성자*)</span><span class="sxs-lookup"><span data-stu-id="c61a6-333">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Filter Provider Constructor*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample21.cs)]

    > [!NOTE]
    > <span data-ttu-id="c61a6-334">필터 공급자 클래스 생성자를 만들지는 **새** 내부의 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-334">The filter provider class constructor is not creating a **new** object inside.</span></span> <span data-ttu-id="c61a6-335">컨테이너를 매개 변수로 전달 하 고 Unity 종속성 해결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-335">The container is passed as a parameter, and the dependency is solved by Unity.</span></span>
7. <span data-ttu-id="c61a6-336">에 **FilterProvider** 클래스, 메서드를 구현 **GetFilters** 에서 **IFilterProvider** 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-336">In the **FilterProvider** class, implement the method **GetFilters** from **IFilterProvider** interface.</span></span>

    <span data-ttu-id="c61a6-337">(코드 조각- *ASP.NET 종속성 주입-Ex03-랩 필터 공급자 GetFilters*)</span><span class="sxs-lookup"><span data-stu-id="c61a6-337">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Filter Provider GetFilters*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample22.cs)]

<a id="Ex3Task2"></a>

<a id="Task_2_-_Registering_and_Enabling_the_Filter"></a>
#### <a name="task-2---registering-and-enabling-the-filter"></a><span data-ttu-id="c61a6-338">작업 2-등록 및 필터 사용</span><span class="sxs-lookup"><span data-stu-id="c61a6-338">Task 2 - Registering and Enabling the Filter</span></span>

<span data-ttu-id="c61a6-339">이 태스크에서는 사이트 관리를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-339">In this task, you will enable site tracking.</span></span> <span data-ttu-id="c61a6-340">이렇게 하려면 필터를 등록 합니다 **Bootstrapper.cs BuildUnityContainer** 메서드 추적을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-340">To do that, you will register the filter in **Bootstrapper.cs BuildUnityContainer** method to start tracing:</span></span>

1. <span data-ttu-id="c61a6-341">열기 **Web.config** System.Web 그룹에서 사용 추적 추적 및 프로젝트 루트에 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-341">Open **Web.config** located in the project root and enable trace tracking at System.Web group.</span></span>

    [!code-xml[Main](aspnet-mvc-4-dependency-injection/samples/sample23.xml)]
2. <span data-ttu-id="c61a6-342">열기 **Bootstrapper.cs** 프로젝트 루트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-342">Open **Bootstrapper.cs** at project root.</span></span>
3. <span data-ttu-id="c61a6-343">에 대 한 참조 추가 **MvcMusicStore.Filters** 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-343">Add a reference to the **MvcMusicStore.Filters** namespace.</span></span>

    <span data-ttu-id="c61a6-344">(코드 조각- *ASP.NET 종속성 주입-Ex03-랩 부트스트래퍼 네임 스페이스 추가*)</span><span class="sxs-lookup"><span data-stu-id="c61a6-344">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Bootstrapper Adding Namespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample24.cs)]
4. <span data-ttu-id="c61a6-345">선택 된 **BuildUnityContainer** 메서드와 Unity 컨테이너에 있는 필터를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-345">Select the **BuildUnityContainer** method and register the filter in the Unity Container.</span></span> <span data-ttu-id="c61a6-346">작업 필터와 필터 공급자를 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-346">You will have to register the filter provider as well as the action filter.</span></span>

    <span data-ttu-id="c61a6-347">(코드 조각- *ASP.NET 종속성 주입-Ex03-랩 레지스터 FilterProvider 및 ActionFilter*)</span><span class="sxs-lookup"><span data-stu-id="c61a6-347">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Register FilterProvider and ActionFilter*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample25.cs)]

<a id="Ex3Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="c61a6-348">작업 3-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="c61a6-348">Task 3 - Running the Application</span></span>

<span data-ttu-id="c61a6-349">이 태스크에서는 응용 프로그램을 실행 하 고 사용자 지정 작업 필터는 활동을 추적는 테스트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-349">In this task, you will run the application and test that the custom action filter is tracing the activity:</span></span>

1. <span data-ttu-id="c61a6-350">**F5** 키를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-350">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="c61a6-351">클릭 **록** 장르 메뉴 내에서.</span><span class="sxs-lookup"><span data-stu-id="c61a6-351">Click **Rock** within the Genres Menu.</span></span> <span data-ttu-id="c61a6-352">하려면 더 많은 장르를 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-352">You can browse to more genres if you want to.</span></span>

    <span data-ttu-id="c61a6-353">![Music Store](aspnet-mvc-4-dependency-injection/_static/image11.png "음악 스토어")</span><span class="sxs-lookup"><span data-stu-id="c61a6-353">![Music Store](aspnet-mvc-4-dependency-injection/_static/image11.png "Music Store")</span></span>

    <span data-ttu-id="c61a6-354">*Music Store*</span><span class="sxs-lookup"><span data-stu-id="c61a6-354">*Music Store*</span></span>
3. <span data-ttu-id="c61a6-355">찾아 **/Trace.axd** 을 클릭 한 다음 응용 프로그램 추적을 보려면 **세부 정보 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-355">Browse to **/Trace.axd** to see the Application Trace page, and then click **View Details**.</span></span>

    <span data-ttu-id="c61a6-356">![응용 프로그램 추적 로그](aspnet-mvc-4-dependency-injection/_static/image12.png "응용 프로그램 추적 로그")</span><span class="sxs-lookup"><span data-stu-id="c61a6-356">![Application Trace Log](aspnet-mvc-4-dependency-injection/_static/image12.png "Application Trace Log")</span></span>

    <span data-ttu-id="c61a6-357">*응용 프로그램 추적 로그*</span><span class="sxs-lookup"><span data-stu-id="c61a6-357">*Application Trace Log*</span></span>

    <span data-ttu-id="c61a6-358">![응용 프로그램 추적-요청 정보](aspnet-mvc-4-dependency-injection/_static/image13.png "응용 프로그램 추적-요청 정보")</span><span class="sxs-lookup"><span data-stu-id="c61a6-358">![Application Trace - Request Details](aspnet-mvc-4-dependency-injection/_static/image13.png "Application Trace - Request Details")</span></span>

    <span data-ttu-id="c61a6-359">*응용 프로그램 추적-요청 세부 정보*</span><span class="sxs-lookup"><span data-stu-id="c61a6-359">*Application Trace - Request Details*</span></span>
4. <span data-ttu-id="c61a6-360">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-360">Close the browser.</span></span>

* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="c61a6-361">요약</span><span class="sxs-lookup"><span data-stu-id="c61a6-361">Summary</span></span>

<span data-ttu-id="c61a6-362">이 실습 랩을 완료 하 여 NuGet 패키지를 사용 하 여 Unity를 통합 하 여 ASP.NET MVC 4의 종속성 주입을 사용 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-362">By completing this Hands-On Lab you have learned how to use Dependency Injection in ASP.NET MVC 4 by integrating Unity using a NuGet Package.</span></span> <span data-ttu-id="c61a6-363">이 위해 컨트롤러, 뷰 및 작업 필터 내부 종속성 주입을 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-363">To achieve that, you have used Dependency Injection inside controllers, views and action filters.</span></span>

<span data-ttu-id="c61a6-364">다음과 같은 개념 포함 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-364">The following concepts were covered:</span></span>

- <span data-ttu-id="c61a6-365">ASP.NET MVC 4 종속성 주입 기능</span><span class="sxs-lookup"><span data-stu-id="c61a6-365">ASP.NET MVC 4 Dependency Injection features</span></span>
- <span data-ttu-id="c61a6-366">Unity 통합 Unity.Mvc3 NuGet 패키지를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="c61a6-366">Unity integration using Unity.Mvc3 NuGet Package</span></span>
- <span data-ttu-id="c61a6-367">컨트롤러의 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="c61a6-367">Dependency Injection in Controllers</span></span>
- <span data-ttu-id="c61a6-368">보기의 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="c61a6-368">Dependency Injection in Views</span></span>
- <span data-ttu-id="c61a6-369">작업 필터의 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="c61a6-369">Dependency injection of Action Filters</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="c61a6-370">부록 a: 설치 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="c61a6-370">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="c61a6-371">설치할 수 있습니다 **Microsoft Visual Studio Express 2012 for Web** 또는 다른 &quot;Express&quot; 버전을 사용 하 여  **[Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)** .</span><span class="sxs-lookup"><span data-stu-id="c61a6-371">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="c61a6-372">다음 지침을 설치 하는 데 필요한 단계를 안내 하 *Visual studio Express 2012 for Web* 를 사용 하 여 *Microsoft 웹 플랫폼 설치 관리자*합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-372">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="c61a6-373">로 이동 [ [https://go.microsoft.com/? linkid = 9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-373">Go to [[https://go.microsoft.com/? linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="c61a6-374">또는 이미 설치 된 웹 플랫폼 설치 관리자를 열 수 있습니다 및 제품에 대 한 검색 &quot; *Visual Studio Express 2012 for Web Windows Azure SDK와*&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-374">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;*Visual Studio Express 2012 for Web with Windows Azure SDK*&quot;.</span></span>
2. <span data-ttu-id="c61a6-375">클릭 **지금 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-375">Click on **Install Now**.</span></span> <span data-ttu-id="c61a6-376">없는 경우 **웹 플랫폼 설치 관리자** 를 다운로드 하 여 앱을 먼저 설치 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-376">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="c61a6-377">한 번 **웹 플랫폼 설치 관리자** 열려 클릭 **설치** 는 설치 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-377">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="c61a6-378">![Visual Studio Express 설치](aspnet-mvc-4-dependency-injection/_static/image14.png "Visual Studio Express 설치")</span><span class="sxs-lookup"><span data-stu-id="c61a6-378">![Install Visual Studio Express](aspnet-mvc-4-dependency-injection/_static/image14.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="c61a6-379">*Visual Studio Express 설치*</span><span class="sxs-lookup"><span data-stu-id="c61a6-379">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="c61a6-380">모든 제품의 라이선스 및 용어를 읽고 클릭 **동의** 를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-380">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![사용 조건 동의](aspnet-mvc-4-dependency-injection/_static/image15.png)

    <span data-ttu-id="c61a6-382">*사용 조건 동의*</span><span class="sxs-lookup"><span data-stu-id="c61a6-382">*Accepting the license terms*</span></span>
5. <span data-ttu-id="c61a6-383">다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-383">Wait until the downloading and installation process completes.</span></span>

    ![설치 진행률](aspnet-mvc-4-dependency-injection/_static/image16.png)

    <span data-ttu-id="c61a6-385">*설치 진행률*</span><span class="sxs-lookup"><span data-stu-id="c61a6-385">*Installation progress*</span></span>
6. <span data-ttu-id="c61a6-386">설치가 완료 되 면 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-386">When the installation completes, click **Finish**.</span></span>

    ![설치 완료](aspnet-mvc-4-dependency-injection/_static/image17.png)

    <span data-ttu-id="c61a6-388">*설치 완료*</span><span class="sxs-lookup"><span data-stu-id="c61a6-388">*Installation completed*</span></span>
7. <span data-ttu-id="c61a6-389">클릭 **종료** 를 웹 플랫폼 설치 관리자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-389">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="c61a6-390">Visual Studio Express for Web을 열려면로 이동는 **시작** 화면를 쓰기 시작할 &quot; **VS Express**&quot;, 클릭는 **VS Express for Web** 바둑판식 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-390">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![웹 타일에 대 한 VS Express](aspnet-mvc-4-dependency-injection/_static/image18.png)

    <span data-ttu-id="c61a6-392">*웹 타일에 대 한 VS Express*</span><span class="sxs-lookup"><span data-stu-id="c61a6-392">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a><span data-ttu-id="c61a6-393">부록 b: 코드 조각을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="c61a6-393">Appendix B: Using Code Snippets</span></span>

<span data-ttu-id="c61a6-394">코드 조각 바로 쉽게 얻습니다 필요한 코드를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-394">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="c61a6-395">랩 문서는 알려 정확 하 게 사용 가능 시기, 다음 그림에 나와 있는 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-395">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="c61a6-396">![Visual Studio 코드 조각을 프로젝트에 코드 삽입을 사용 하 여](aspnet-mvc-4-dependency-injection/_static/image19.png "Visual Studio를 사용 하 여 코드 조각을 프로젝트에 코드를 삽입 하려면")</span><span class="sxs-lookup"><span data-stu-id="c61a6-396">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-dependency-injection/_static/image19.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="c61a6-397">*Visual Studio 코드 조각을 프로젝트에 코드 삽입을 사용 하 여*</span><span class="sxs-lookup"><span data-stu-id="c61a6-397">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="c61a6-398">***키보드 (C#만)를 사용 하 여 코드 조각을 추가 하려면***</span><span class="sxs-lookup"><span data-stu-id="c61a6-398">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="c61a6-399">코드를 삽입 하려는 위치에 커서를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-399">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="c61a6-400">공백 또는 하이픈만) (없이 코드 조각 이름을 입력 하기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-400">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="c61a6-401">IntelliSense 표시 조각 이름과 일치 하는 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-401">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="c61a6-402">올바른 코드 조각 선택 (또는 전체 코드 조각이 이름이 선택 될 때까지 입력 유지).</span><span class="sxs-lookup"><span data-stu-id="c61a6-402">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="c61a6-403">커서 위치에 코드 조각을 삽입 하려면 두 번 탭 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-403">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="c61a6-404">![코드 조각 이름을 입력 하기 시작](aspnet-mvc-4-dependency-injection/_static/image20.png "조각 이름을 입력 하기 시작")</span><span class="sxs-lookup"><span data-stu-id="c61a6-404">![Start typing the snippet name](aspnet-mvc-4-dependency-injection/_static/image20.png "Start typing the snippet name")</span></span>

<span data-ttu-id="c61a6-405">*코드 조각 이름을 입력 하기 시작*</span><span class="sxs-lookup"><span data-stu-id="c61a6-405">*Start typing the snippet name*</span></span>

<span data-ttu-id="c61a6-406">![Tab 키를 눌러 강조 표시 된 코드 조각 선택](aspnet-mvc-4-dependency-injection/_static/image21.png "Tab 키를 눌러 강조 표시 된 코드 조각 선택")</span><span class="sxs-lookup"><span data-stu-id="c61a6-406">![Press Tab to select the highlighted snippet](aspnet-mvc-4-dependency-injection/_static/image21.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="c61a6-407">*Tab 키를 눌러 강조 표시 된 코드 조각 선택*</span><span class="sxs-lookup"><span data-stu-id="c61a6-407">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="c61a6-408">![확장 하 고 Tab 키를 눌러 다시 코드 조각](aspnet-mvc-4-dependency-injection/_static/image22.png "확장 하 고 Tab 키를 눌러 다시 코드 조각")</span><span class="sxs-lookup"><span data-stu-id="c61a6-408">![Press Tab again and the snippet will expand](aspnet-mvc-4-dependency-injection/_static/image22.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="c61a6-409">*확장 하 고 Tab 키를 눌러 다시 코드 조각*</span><span class="sxs-lookup"><span data-stu-id="c61a6-409">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="c61a6-410">***마우스 (C#, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가 하려면*** 1입니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-410">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="c61a6-411">코드 조각을 삽입 하려면 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-411">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="c61a6-412">선택 **조각 삽입** 이어서 **내 코드 조각**합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-412">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="c61a6-413">클릭 하 여 목록에서 관련 조각을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c61a6-413">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="c61a6-414">![코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추로 클릭](aspnet-mvc-4-dependency-injection/_static/image23.png "코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추 클릭")</span><span class="sxs-lookup"><span data-stu-id="c61a6-414">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-dependency-injection/_static/image23.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="c61a6-415">*코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추로 클릭*</span><span class="sxs-lookup"><span data-stu-id="c61a6-415">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="c61a6-416">![클릭 하 여 목록에서 관련 조각을 선택](aspnet-mvc-4-dependency-injection/_static/image24.png "클릭 하 여 목록에서 관련 조각을 선택")</span><span class="sxs-lookup"><span data-stu-id="c61a6-416">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-dependency-injection/_static/image24.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="c61a6-417">*클릭 하 여 목록에서 관련 조각을 선택합니다*</span><span class="sxs-lookup"><span data-stu-id="c61a6-417">*Pick the relevant snippet from the list, by clicking on it*</span></span>
