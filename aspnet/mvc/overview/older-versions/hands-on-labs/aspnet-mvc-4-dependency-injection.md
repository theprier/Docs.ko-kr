---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-dependency-injection
title: ASP.NET MVC 4 종속성 주입 | Microsoft Docs
author: rick-anderson
description: 참고:이 실습 랩에서 ASP.NET MVC 및 ASP.NET MVC 4 필터에 대 한 기본 지식이 있다고 가정 합니다. ASP.NET MVC 4 필터 하기 전에 사용 하지 않은 rec... 하는 경우
ms.author: aspnetcontent
ms.date: 02/18/2013
ms.assetid: 84c7baca-1c54-4c44-8f52-4282122d6acb
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: 44c8f2055fb62d589e874683cbf43eed87a8c447
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37812345"
---
# <a name="aspnet-mvc-4-dependency-injection"></a><span data-ttu-id="f8da6-104">ASP.NET MVC 4 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="f8da6-104">ASP.NET MVC 4 Dependency Injection</span></span>

<span data-ttu-id="f8da6-105">[웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="f8da6-105">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="f8da6-106">웹 캠프 학습 키트 다운로드</span><span class="sxs-lookup"><span data-stu-id="f8da6-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="f8da6-107">이 실습 랩 기본 지식이 있다고 가정 **ASP.NET MVC** 하 고 **필터링 하는 ASP.NET MVC 4**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-107">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC** and **ASP.NET MVC 4 filters**.</span></span> <span data-ttu-id="f8da6-108">사용 하지 않은 경우 **ASP.NET MVC 4 필터링** 이전 좋습니다 이동해 **ASP.NET MVC 사용자 지정 작업 필터** 실습 랩입니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-108">If you have not used **ASP.NET MVC 4 filters** before, we recommend you to go over **ASP.NET MVC Custom Action Filters** Hands-on Lab.</span></span>

> [!NOTE]
> <span data-ttu-id="f8da6-109">웹 캠프 교육 키트에서에서 사용할 수 있는 모든 샘플 코드 및 코드 조각 포함 된 [Microsoft-웹/WebCampTrainingKit 릴리스](https://aka.ms/webcamps-training-kit)합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-109">All sample code and snippets are included in the Web Camps Training Kit, available from at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="f8da6-110">이 랩에 특정 프로젝트에서 제공 됩니다 [ASP.NET MVC 4 종속성 주입](https://github.com/Microsoft-Web/HOL-MVC4DependencyInjection)합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-110">The project specific to this lab is available at [ASP.NET MVC 4 Dependency Injection](https://github.com/Microsoft-Web/HOL-MVC4DependencyInjection).</span></span>

<span data-ttu-id="f8da6-111">**객체 지향 프로그래밍** 패러다임 개체가 함께 동작 공동 작업 모델 참가자와 소비자가 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-111">In **Object Oriented Programming** paradigm, objects work together in a collaboration model where there are contributors and consumers.</span></span> <span data-ttu-id="f8da6-112">물론이 통신 모델 개체 및 복잡성이 증가 하는 경우 관리 하기가 점점 구성 요소 간의 종속성을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-112">Naturally, this communication model generates dependencies between objects and components, becoming difficult to manage when complexity increases.</span></span>

<span data-ttu-id="f8da6-113">![종속성을 클래스 및 모델 복잡성](aspnet-mvc-4-dependency-injection/_static/image1.png "종속성 클래스 및 복잡성을 모델")</span><span class="sxs-lookup"><span data-stu-id="f8da6-113">![Class dependencies and model complexity](aspnet-mvc-4-dependency-injection/_static/image1.png "Class dependencies and model complexity")</span></span>

<span data-ttu-id="f8da6-114">*클래스 종속성 및 모델의 복잡성*</span><span class="sxs-lookup"><span data-stu-id="f8da6-114">*Class dependencies and model complexity*</span></span>

<span data-ttu-id="f8da6-115">에 대 한 번쯤은 들어봤을 겁니다 합니다 **팩터리 패턴** 및 인터페이스와 서비스를 사용 하 여 클라이언트 개체 서비스 위치에 대 한 책임 많습니다 구현 간의 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-115">You have probably heard about the **Factory Pattern** and the separation between the interface and the implementation using services, where the client objects are often responsible for service location.</span></span>

<span data-ttu-id="f8da6-116">종속성 주입 패턴은 Inversion of Control의 특정 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-116">The Dependency Injection pattern is a particular implementation of Inversion of Control.</span></span> <span data-ttu-id="f8da6-117">**반전 (IoC) 제어** 개체 들은 작업할 때 서로 다른 개체를 만들지 마십시오 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-117">**Inversion of Control (IoC)** means that objects do not create other objects on which they rely to do their work.</span></span> <span data-ttu-id="f8da6-118">대신 외부 소스 (예를 들어, xml 구성 파일)에서 필요한 개체를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-118">Instead, they get the objects that they need from an outside source (for example, an xml configuration file).</span></span>

<span data-ttu-id="f8da6-119">**DI (종속성 주입)** 은 있음을 나타내고이 수행한 개체 개입 없이 일반적으로 생성자 매개 변수를 전달 하는 프레임 워크 구성 요소 속성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-119">**Dependency Injection (DI)** means that this is done without the object intervention, usually by a framework component that passes constructor parameters and set properties.</span></span>

<a id="The_Dependency_Injection_DI_Design_Pattern"></a>
### <a name="the-dependency-injection-di-design-pattern"></a><span data-ttu-id="f8da6-120">종속성 주입 (DI) 디자인 패턴</span><span class="sxs-lookup"><span data-stu-id="f8da6-120">The Dependency Injection (DI) Design Pattern</span></span>

<span data-ttu-id="f8da6-121">높은 수준에서 종속성 주입의 목표는 클라이언트 클래스 (예: *는 골퍼*) 인터페이스를 충족 하는 것을 요구 (예: *IClub*).</span><span class="sxs-lookup"><span data-stu-id="f8da6-121">At a high level, the goal of Dependency Injection is that a client class (e.g. *the golfer*) needs something that satisfies an interface (e.g. *IClub*).</span></span> <span data-ttu-id="f8da6-122">구체적인 형식 이란를 고려 하지 않습니다 (예: *WoodClub, IronClub, WedgeClub* 또는 *PutterClub*), 문제를 해결 하려면 다른 사용자가 (좋은 예를 들어 *caddy*).</span><span class="sxs-lookup"><span data-stu-id="f8da6-122">It doesn't care what the concrete type is (e.g. *WoodClub, IronClub, WedgeClub* or *PutterClub*), it wants someone else to handle that (e.g. a good *caddy*).</span></span> <span data-ttu-id="f8da6-123">ASP.NET MVC의 종속성 확인자를 사용 하면 어딘가 다른 종속성 논리를 등록할 수 있습니다 (예: 컨테이너 또는 *클럽 모음*).</span><span class="sxs-lookup"><span data-stu-id="f8da6-123">The Dependency Resolver in ASP.NET MVC can allow you to register your dependency logic somewhere else (e.g. a container or a *bag of clubs*).</span></span>

<span data-ttu-id="f8da6-124">![종속성 주입 다이어그램](aspnet-mvc-4-dependency-injection/_static/image2.png "종속성 주입 그림")</span><span class="sxs-lookup"><span data-stu-id="f8da6-124">![Dependency Injection diagram](aspnet-mvc-4-dependency-injection/_static/image2.png "Dependency Injection illustration")</span></span>

<span data-ttu-id="f8da6-125">*종속성 주입-골프 비유*</span><span class="sxs-lookup"><span data-stu-id="f8da6-125">*Dependency Injection - Golf analogy*</span></span>

<span data-ttu-id="f8da6-126">종속성 주입 패턴 및 Inversion of Control을 사용 하는 이점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-126">The advantages of using Dependency Injection pattern and Inversion of Control are the following:</span></span>

- <span data-ttu-id="f8da6-127">클래스 결합을 줄일 수</span><span class="sxs-lookup"><span data-stu-id="f8da6-127">Reduces class coupling</span></span>
- <span data-ttu-id="f8da6-128">코드 재사용 증가</span><span class="sxs-lookup"><span data-stu-id="f8da6-128">Increases code reusing</span></span>
- <span data-ttu-id="f8da6-129">코드 유지 가능성 향상</span><span class="sxs-lookup"><span data-stu-id="f8da6-129">Improves code maintainability</span></span>
- <span data-ttu-id="f8da6-130">응용 프로그램 테스트 개선</span><span class="sxs-lookup"><span data-stu-id="f8da6-130">Improves application testing</span></span>

> [!NOTE]
> <span data-ttu-id="f8da6-131">종속성 주입 추상 팩터리 디자인 패턴을 따라 비교 되어 있지만 두 방법 간에 약간의 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-131">Dependency Injection is sometimes compared with Abstract Factory Design Pattern, but there is a slight difference between both approaches.</span></span> <span data-ttu-id="f8da6-132">DI는 프레임 워크는 팩터리 및 등록된 된 서비스를 호출 하 여 종속성을 해결 하기 위해 작업 뒤에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-132">DI has a Framework working behind to solve dependencies by calling the factories and the registered services.</span></span>


<span data-ttu-id="f8da6-133">종속성 주입 패턴을 이해 했으므로 배웁니다이 랩 전체 ASP.NET MVC 4에서 적용 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="f8da6-133">Now that you understand the Dependency Injection Pattern, you will learn throughout this lab how to apply it in ASP.NET MVC 4.</span></span> <span data-ttu-id="f8da6-134">종속성 주입을 사용 하 여 시작 합니다 **컨트롤러** 데이터베이스 액세스 서비스를 포함 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-134">You will start using Dependency Injection in the **Controllers** to include a database access service.</span></span> <span data-ttu-id="f8da6-135">다음으로, 종속성 주입에 적용할 합니다 **뷰** 서비스를 사용 하 여 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-135">Next, you will apply Dependency Injection to the **Views** to consume a service and show information.</span></span> <span data-ttu-id="f8da6-136">마지막으로 확장 하면는 DI를 ASP.NET MVC 4 필터에 솔루션의 사용자 지정 작업 필터를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-136">Finally, you will extend the DI to ASP.NET MVC 4 Filters, injecting a custom action filter in the solution.</span></span>

<span data-ttu-id="f8da6-137">이 실습 랩에서 학습할 방법:</span><span class="sxs-lookup"><span data-stu-id="f8da6-137">In this Hands-on Lab, you will learn how to:</span></span>

- <span data-ttu-id="f8da6-138">Unity를 사용 하 여 NuGet 패키지를 사용 하 여 종속성 주입을 위한 ASP.NET MVC 4를 통합</span><span class="sxs-lookup"><span data-stu-id="f8da6-138">Integrate ASP.NET MVC 4 with Unity for Dependency Injection using NuGet Packages</span></span>
- <span data-ttu-id="f8da6-139">ASP.NET MVC 컨트롤러 내에서 사용 하 여 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="f8da6-139">Use Dependency Injection inside an ASP.NET MVC Controller</span></span>
- <span data-ttu-id="f8da6-140">ASP.NET MVC 뷰 내에서 사용 하 여 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="f8da6-140">Use Dependency Injection inside an ASP.NET MVC View</span></span>
- <span data-ttu-id="f8da6-141">내 ASP.NET MVC 작업 필터를 사용 하 여 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="f8da6-141">Use Dependency Injection inside an ASP.NET MVC Action Filter</span></span>

> [!NOTE]
> <span data-ttu-id="f8da6-142">이 랩에서 Unity.Mvc3 NuGet 패키지를 사용 하 여 종속성 확인에 있지만 ASP.NET MVC 4를 사용 하는 종속성 주입 프레임 워크를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-142">This Lab is using Unity.Mvc3 NuGet Package for dependency resolution, but it is possible to adapt any Dependency Injection Framework to work with ASP.NET MVC 4.</span></span>


<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="f8da6-143">전제 조건</span><span class="sxs-lookup"><span data-stu-id="f8da6-143">Prerequisites</span></span>

<span data-ttu-id="f8da6-144">이 랩을 완료 하려면 다음 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-144">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="f8da6-145">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) 하거나 그 보다 뛰어난 (읽을 [부록 A](#AppendixA) 설치 하는 방법에 대 한 지침은).</span><span class="sxs-lookup"><span data-stu-id="f8da6-145">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="f8da6-146">설정</span><span class="sxs-lookup"><span data-stu-id="f8da6-146">Setup</span></span>

<span data-ttu-id="f8da6-147">**설치 코드 조각**</span><span class="sxs-lookup"><span data-stu-id="f8da6-147">**Installing Code Snippets**</span></span>

<span data-ttu-id="f8da6-148">편의 위해이 랩에서 함께 관리 하려는 코드의 대부분 제품은 Visual Studio 코드 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-148">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="f8da6-149">설치를 실행 하는 코드 조각 **.\Source\Setup\CodeSnippets.vsi** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-149">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="f8da6-150">이 문서의 부록 참조할 수 있습니다 사용 하는 방법을 알아보려면 원하는 고 Visual Studio 코드 조각을 사용 하 여 잘 모르는 경우 &quot; [부록 b:를 사용 하 여 코드 조각](#AppendixB)&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-150">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix B: Using Code Snippets](#AppendixB)&quot;.</span></span>

* * *

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="f8da6-151">연습</span><span class="sxs-lookup"><span data-stu-id="f8da6-151">Exercises</span></span>

<span data-ttu-id="f8da6-152">이 실습 랩에서 다음 연습으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-152">This Hands-On Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="f8da6-153">연습 1: 컨트롤러 삽입</span><span class="sxs-lookup"><span data-stu-id="f8da6-153">Exercise 1: Injecting a Controller</span></span>](#Exercise1)
2. [<span data-ttu-id="f8da6-154">연습 2: 보기 삽입</span><span class="sxs-lookup"><span data-stu-id="f8da6-154">Exercise 2: Injecting a View</span></span>](#Exercise2)
3. [<span data-ttu-id="f8da6-155">필터를 삽입 하는 연습 3:</span><span class="sxs-lookup"><span data-stu-id="f8da6-155">Exercise 3: Injecting Filters</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="f8da6-156">각 실습 동반 되는 **최종** 연습을 완료 한 후 가져와야 결과 솔루션이 포함 된 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-156">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="f8da6-157">이 연습을 진행 하는 추가 도움이 필요한 경우이 솔루션 가이드로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-157">You can use this solution as a guide if you need additional help working through the exercises.</span></span>


<span data-ttu-id="f8da6-158">이 랩을 완료 하기 위한 예상 시간: **30 분**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-158">Estimated time to complete this lab: **30 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Injecting_a_Controller"></a>
### <a name="exercise-1-injecting-a-controller"></a><span data-ttu-id="f8da6-159">연습 1: 컨트롤러 삽입</span><span class="sxs-lookup"><span data-stu-id="f8da6-159">Exercise 1: Injecting a Controller</span></span>

<span data-ttu-id="f8da6-160">이 연습에서는 Unity는 NuGet 패키지를 사용 하 여 통합 하 여 ASP.NET MVC 컨트롤러에서 종속성 주입을 사용 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-160">In this exercise, you will learn how to use Dependency Injection in ASP.NET MVC Controllers by integrating Unity using a NuGet Package.</span></span> <span data-ttu-id="f8da6-161">이런 이유로 서비스에서 데이터 액세스 논리를 분리 하기 위해 MvcMusicStore 컨트롤러에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-161">For that reason, you will include services into your MvcMusicStore controllers to separate the logic from the data access.</span></span> <span data-ttu-id="f8da6-162">서비스를 활용 하 여 종속성 주입을 사용 하 여 확인 될 컨트롤러 생성자에서 새 종속성을 만듭니다 **Unity**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-162">The services will create a new dependency in the controller constructor, which will be resolved using Dependency Injection with the help of **Unity**.</span></span>

<span data-ttu-id="f8da6-163">이 방법은 덜 결합 된 응용 프로그램을 보다 유연 하 고 유지 관리 하 고 테스트 하는 작업을 쉽게 생성 하는 방법을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-163">This approach will show you how to generate less coupled applications, which are more flexible and easier to maintain and test.</span></span> <span data-ttu-id="f8da6-164">Unity를 사용한 ASP.NET MVC를 통합 하는 방법 또한 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-164">You will also learn how to integrate ASP.NET MVC with Unity.</span></span>

<a id="About_StoreManager_Service"></a>
#### <a name="about-storemanager-service"></a><span data-ttu-id="f8da6-165">StoreManager 서비스에 대 한</span><span class="sxs-lookup"><span data-stu-id="f8da6-165">About StoreManager Service</span></span>

<span data-ttu-id="f8da6-166">이제 시작 솔루션에서 제공 하는 MVC Music Store 라는 저장소 컨트롤러 데이터를 관리 하는 서비스를 포함 **StoreService**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-166">The MVC Music Store provided in the begin solution now includes a service that manages the Store Controller data named **StoreService**.</span></span> <span data-ttu-id="f8da6-167">아래 저장소 서비스 구현을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-167">Below you will find the Store Service implementation.</span></span> <span data-ttu-id="f8da6-168">모든 메서드는 모델 엔터티를 반환 하는 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-168">Note that all the methods return Model entities.</span></span>

[!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample1.cs)]

<span data-ttu-id="f8da6-169">**StoreController** 시작에서 솔루션 이제 소비 **StoreService**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-169">**StoreController** from the begin solution now consumes **StoreService**.</span></span> <span data-ttu-id="f8da6-170">모든 데이터 참조에서 제거 되었습니다 **StoreController**, 및를 사용 하는 모든 메서드를 변경 하지 않고 현재 데이터 액세스 공급자를 수정 하는 현재 사용 가능한 **StoreService**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-170">All the data references were removed from **StoreController**, and now possible to modify the current data access provider without changing any method that consumes **StoreService**.</span></span>

<span data-ttu-id="f8da6-171">아래에 찾을 수 있습니다 합니다 **StoreController** 구현에 사용 하 여 종속성 **StoreService** 클래스 생성자 내에서.</span><span class="sxs-lookup"><span data-stu-id="f8da6-171">You will find below that the **StoreController** implementation has a dependency with **StoreService** inside the class constructor.</span></span>

> [!NOTE]
> <span data-ttu-id="f8da6-172">이 연습에 도입 된 종속성 관련이 **Inversion of Control** (IoC).</span><span class="sxs-lookup"><span data-stu-id="f8da6-172">The dependency introduced in this exercise is related to **Inversion of Control** (IoC).</span></span>
> 
> <span data-ttu-id="f8da6-173">합니다 **StoreController** 클래스 생성자를 받습니다는 **IStoreService** 클래스 내에서 서비스를 호출 하는 데 필수적인 형식 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-173">The **StoreController** class constructor receives an **IStoreService** type parameter, which is essential to perform service calls from inside the class.</span></span> <span data-ttu-id="f8da6-174">그러나 **StoreController** 를 기본 (매개 변수가 없는 생성자) 모든 컨트롤러는 ASP.NET MVC를 사용 하 여 작업을 포함 해야 하는 구현 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-174">However, **StoreController** does not implement the default constructor (with no parameters) that any controller must have to work with ASP.NET MVC.</span></span>
> 
> <span data-ttu-id="f8da6-175">종속성을 해결 하려면 컨트롤러 (지정 된 형식의 모든 개체를 반환 하는 클래스)는 추상 팩터리에서 만든 수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-175">To resolve the dependency, the controller has to be created by an abstract factory (a class that returns any object of the specified type).</span></span>


[!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample2.cs)]

> [!NOTE]
> <span data-ttu-id="f8da6-176">클래스에서 선언 된 매개 변수가 없는 생성자는 서비스 개체를 전송 하지 않고는 StoreController 만들 하려고 할 때 오류를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-176">You will get an error when the class tries to create the StoreController without sending the service object, as there is no parameterless constructor declared.</span></span>


<a id="Ex1Task1"></a>

<a id="Task_1_-_Running_the_Application"></a>
#### <a name="task-1---running-the-application"></a><span data-ttu-id="f8da6-177">작업 1-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="f8da6-177">Task 1 - Running the Application</span></span>

<span data-ttu-id="f8da6-178">이 태스크에서는 데이터 액세스 응용 프로그램 논리와 분리 하는 저장소 컨트롤러에 서비스를 포함 하는 시작 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-178">In this task, you will run the Begin application, which includes the service into the Store Controller that separates the data access from the application logic.</span></span>

<span data-ttu-id="f8da6-179">응용 프로그램을 실행할 때 컨트롤러 서비스를 기본적으로 매개 변수로 전달 하지는 예외를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-179">When running the application, you will receive an exception, as the controller service is not passed as a parameter by default:</span></span>

1. <span data-ttu-id="f8da6-180">엽니다는 **시작** 솔루션에 있는 **Controller\Begin Source\Ex01 삽입**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-180">Open the **Begin** solution located in **Source\Ex01-Injecting Controller\Begin**.</span></span>

   1. <span data-ttu-id="f8da6-181">일부 누락 된 NuGet 패키지를 다운로드 해야 하기 전에 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-181">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="f8da6-182">이 작업을 수행 하려면 클릭 합니다 **프로젝트** 선택한 메뉴 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-182">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="f8da6-183">에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="f8da6-183">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="f8da6-184">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-184">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="f8da6-185">NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-185">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="f8da6-186">NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-186">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="f8da6-187">이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-187">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="f8da6-188">키를 눌러 **ctrl+f5** 디버깅 하지 않고 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-188">Press **Ctrl + F5** to run the application without debugging.</span></span> <span data-ttu-id="f8da6-189">오류 메시지가 표시 됩니다 &quot; **이 개체에 대해 정의 된 매개 변수가 없는 생성자가 없습니다**&quot;:</span><span class="sxs-lookup"><span data-stu-id="f8da6-189">You will get the error message &quot;**No parameterless constructor defined for this object**&quot;:</span></span>

    <span data-ttu-id="f8da6-190">![ASP.NET MVC 시작 응용 프로그램을 실행 하는 동안 오류가 발생 했습니다](aspnet-mvc-4-dependency-injection/_static/image3.png "ASP.NET MVC 시작 응용 프로그램을 실행 하는 동안 오류가 발생 했습니다")</span><span class="sxs-lookup"><span data-stu-id="f8da6-190">![Error while running ASP.NET MVC Begin Application](aspnet-mvc-4-dependency-injection/_static/image3.png "Error while running ASP.NET MVC Begin Application")</span></span>

    <span data-ttu-id="f8da6-191">*ASP.NET MVC 시작 응용 프로그램을 실행 하는 동안 오류가 발생 했습니다*</span><span class="sxs-lookup"><span data-stu-id="f8da6-191">*Error while running ASP.NET MVC Begin Application*</span></span>
3. <span data-ttu-id="f8da6-192">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-192">Close the browser.</span></span>

<span data-ttu-id="f8da6-193">다음 단계를이 컨트롤러에 필요한 종속성을 주입할 음악 스토어 솔루션에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-193">In the following steps you will work on the Music Store Solution to inject the dependency this controller needs.</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Including_Unity_into_MvcMusicStore_Solution"></a>
#### <a name="task-2---including-unity-into-mvcmusicstore-solution"></a><span data-ttu-id="f8da6-194">작업 2-MvcMusicStore 솔루션에 포함 하 여 Unity</span><span class="sxs-lookup"><span data-stu-id="f8da6-194">Task 2 - Including Unity into MvcMusicStore Solution</span></span>

<span data-ttu-id="f8da6-195">이 작업에서는 포함 됩니다 **Unity.Mvc3** 솔루션에 NuGet 패키지.</span><span class="sxs-lookup"><span data-stu-id="f8da6-195">In this task, you will include **Unity.Mvc3** NuGet Package to the solution.</span></span>

> [!NOTE]
> <span data-ttu-id="f8da6-196">Unity.Mvc3 패키지 ASP.NET MVC 3에 대 한 디자인 되었지만 ASP.NET MVC 4를 사용 하 여 완전히 호환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-196">Unity.Mvc3 package was designed for ASP.NET MVC 3, but it is fully compatible with ASP.NET MVC 4.</span></span>
> 
> <span data-ttu-id="f8da6-197">Unity 지원 (옵션)를 사용 하 여 간단 하 고 확장 가능한 종속성 주입 컨테이너를 예를 들어 이며 인터 셉 션을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-197">Unity is a lightweight, extensible dependency injection container with optional support for instance and type interception.</span></span> <span data-ttu-id="f8da6-198">모든 유형의.NET 응용 프로그램에서 사용 하기 위해 범용 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-198">It is a general-purpose container for use in any type of .NET application.</span></span> <span data-ttu-id="f8da6-199">포함 하 여 종속성 주입 메커니즘에 있는 모든 일반적인 기능을 제공 합니다: 개체 만들기, 컨테이너에 구성 요소 구성 지연 하 여 런타임 및 유연성에 대 한 종속성을 지정 하 여 요구 사항의 추상화 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-199">It provides all the common features found in dependency injection mechanisms including: object creation, abstraction of requirements by specifying dependencies at runtime and flexibility, by deferring the component configuration to the container.</span></span>


1. <span data-ttu-id="f8da6-200">설치할 **Unity.Mvc3** NuGet 패키지에는 **MvcMusicStore** 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-200">Install **Unity.Mvc3** NuGet Package in the **MvcMusicStore** project.</span></span> <span data-ttu-id="f8da6-201">이 작업을 수행 하려면 엽니다는 **패키지 관리자 콘솔** 에서 **뷰** | **기타 Windows**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-201">To do this, open the **Package Manager Console** from **View** | **Other Windows**.</span></span>
2. <span data-ttu-id="f8da6-202">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-202">Run the following command.</span></span>

    <span data-ttu-id="f8da6-203">PMC</span><span class="sxs-lookup"><span data-stu-id="f8da6-203">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-dependency-injection/samples/sample3.ps1)]

    <span data-ttu-id="f8da6-204">![Unity.Mvc3 NuGet 패키지를 설치](aspnet-mvc-4-dependency-injection/_static/image4.png "Unity.Mvc3 NuGet 패키지를 설치 합니다.")</span><span class="sxs-lookup"><span data-stu-id="f8da6-204">![Installing Unity.Mvc3 NuGet Package](aspnet-mvc-4-dependency-injection/_static/image4.png "Installing Unity.Mvc3 NuGet Package")</span></span>

    <span data-ttu-id="f8da6-205">*Unity.Mvc3 NuGet 패키지를 설치합니다.*</span><span class="sxs-lookup"><span data-stu-id="f8da6-205">*Installing Unity.Mvc3 NuGet Package*</span></span>
3. <span data-ttu-id="f8da6-206">한 번 합니다 **Unity.Mvc3** 패키지를 설치, 파일 및 Unity 구성을 단순화 하기 위해 자동으로 추가 하는 폴더를 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-206">Once the **Unity.Mvc3** package is installed, explore the files and folders it automatically adds in order to simplify Unity configuration.</span></span>

    <span data-ttu-id="f8da6-207">![Unity.Mvc3 패키지 설치](aspnet-mvc-4-dependency-injection/_static/image5.png "Unity.Mvc3 패키지 설치")</span><span class="sxs-lookup"><span data-stu-id="f8da6-207">![Unity.Mvc3 package installed](aspnet-mvc-4-dependency-injection/_static/image5.png "Unity.Mvc3 package installed")</span></span>

    <span data-ttu-id="f8da6-208">*Unity.Mvc3 패키지 설치*</span><span class="sxs-lookup"><span data-stu-id="f8da6-208">*Unity.Mvc3 package installed*</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Registering_Unity_in_Globalasaxcs_Application_Start"></a>
#### <a name="task-3---registering-unity-in-globalasaxcs-applicationstart"></a><span data-ttu-id="f8da6-209">작업 3-Global.asax.cs 응용 프로그램에서 등록 Unity\_시작</span><span class="sxs-lookup"><span data-stu-id="f8da6-209">Task 3 - Registering Unity in Global.asax.cs Application\_Start</span></span>

<span data-ttu-id="f8da6-210">이 태스크에서는 업데이트를 **응용 프로그램\_시작** 에 있는 메서드 **Global.asax.cs** Unity 부트스트래퍼 이니셜라이저를 호출 하 고 그런 다음 등록 하는 부트스트래퍼 파일을 업데이트 하려면 서비스 및 종속성 주입을 위해 사용 하 여 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-210">In this task, you will update the **Application\_Start** method located in **Global.asax.cs** to call the Unity Bootstrapper initializer and then, update the Bootstrapper file registering the Service and Controller you will use for Dependency Injection.</span></span>

1. <span data-ttu-id="f8da6-211">이제 Unity 컨테이너를 초기화 하는 파일인 부트스트래퍼 및 종속성 확인자를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-211">Now, you will hook up the Bootstrapper which is the file that initializes the Unity container and Dependency Resolver.</span></span> <span data-ttu-id="f8da6-212">이 작업을 수행 하려면 엽니다 **Global.asax.cs** 내에서 다음 강조 표시 된 코드를 추가 합니다 **응용 프로그램\_시작** 메서드.</span><span class="sxs-lookup"><span data-stu-id="f8da6-212">To do this, open **Global.asax.cs** and add the following highlighted code within the **Application\_Start** method.</span></span>

    <span data-ttu-id="f8da6-213">(코드 조각- *ASP.NET 종속성 주입 랩-Ex01-Unity 초기화*)</span><span class="sxs-lookup"><span data-stu-id="f8da6-213">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex01 - Initialize Unity*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample4.cs)]
2. <span data-ttu-id="f8da6-214">오픈 **Bootstrapper.cs** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-214">Open **Bootstrapper.cs** file.</span></span>
3. <span data-ttu-id="f8da6-215">네임 스페이스를 포함 합니다. **MvcMusicStore.Services** 하 고 **MusicStore.Controllers**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-215">Include the following namespaces: **MvcMusicStore.Services** and **MusicStore.Controllers**.</span></span>

    <span data-ttu-id="f8da6-216">(코드 조각- *네임 스페이스를 추가 하는 ASP.NET 종속성 주입-Ex01-랩 부트스트래퍼*)</span><span class="sxs-lookup"><span data-stu-id="f8da6-216">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex01 - Bootstrapper Adding Namespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample5.cs)]
4. <span data-ttu-id="f8da6-217">바꿉니다 **BuildUnityContainer** 메서드의 저장소 컨트롤러 및 저장소 서비스를 등록 하는 다음 코드를 사용 하 여 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-217">Replace **BuildUnityContainer** method's content with the following code that registers Store Controller and Store Service.</span></span>

    <span data-ttu-id="f8da6-218">(코드 조각- *ASP.NET 종속성 주입-Ex01-랩 등록 저장소 컨트롤러 및 서비스*)</span><span class="sxs-lookup"><span data-stu-id="f8da6-218">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex01 - Register Store Controller and Service*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample6.cs)]

<a id="Ex1Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="f8da6-219">작업 4-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="f8da6-219">Task 4 - Running the Application</span></span>

<span data-ttu-id="f8da6-220">이 태스크는 이제 로드할 수 있습니다 Unity를 포함 한 후 확인 하려면 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-220">In this task, you will run the application to verify that it can now be loaded after including Unity.</span></span>

1. <span data-ttu-id="f8da6-221">키를 눌러 **F5** 응용 프로그램을 실행 하려면 응용 프로그램 오류 메시지를 표시 하지 않고 로드 이제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-221">Press **F5** to run the application, the application should now load without showing any error message.</span></span>

    <span data-ttu-id="f8da6-222">![종속성 주입을 사용 하 여 응용 프로그램을 실행](aspnet-mvc-4-dependency-injection/_static/image6.png "종속성 주입을 사용 하 여 응용 프로그램을 실행 합니다.")</span><span class="sxs-lookup"><span data-stu-id="f8da6-222">![Running Application with Dependency Injection](aspnet-mvc-4-dependency-injection/_static/image6.png "Running Application with Dependency Injection")</span></span>

    <span data-ttu-id="f8da6-223">*종속성 주입을 사용 하 여 응용 프로그램을 실행합니다.*</span><span class="sxs-lookup"><span data-stu-id="f8da6-223">*Running Application with Dependency Injection*</span></span>
2. <span data-ttu-id="f8da6-224">이동할 **스토어**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-224">Browse to **/Store**.</span></span> <span data-ttu-id="f8da6-225">이렇게 하면 **StoreController**를 사용 하 여 이제 만들어지는 **Unity**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-225">This will invoke **StoreController**, which is now created using **Unity**.</span></span>

    <span data-ttu-id="f8da6-226">![MVC Music Store](aspnet-mvc-4-dependency-injection/_static/image7.png "MVC Music Store")</span><span class="sxs-lookup"><span data-stu-id="f8da6-226">![MVC Music Store](aspnet-mvc-4-dependency-injection/_static/image7.png "MVC Music Store")</span></span>

    <span data-ttu-id="f8da6-227">*MVC Music Store*</span><span class="sxs-lookup"><span data-stu-id="f8da6-227">*MVC Music Store*</span></span>
3. <span data-ttu-id="f8da6-228">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-228">Close the browser.</span></span>

<span data-ttu-id="f8da6-229">다음 연습에서 ASP.NET MVC 뷰 및 작업 필터 내에서 사용 하는 종속성 주입 범위를 확장 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-229">In the following exercises you will learn how to extend the Dependency Injection scope to use it inside ASP.NET MVC Views and Action Filters.</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Injecting_a_View"></a>
### <a name="exercise-2-injecting-a-view"></a><span data-ttu-id="f8da6-230">연습 2: 보기 삽입</span><span class="sxs-lookup"><span data-stu-id="f8da6-230">Exercise 2: Injecting a View</span></span>

<span data-ttu-id="f8da6-231">이 연습에서는 Unity 통합에 대 한 ASP.NET MVC 4의 새로운 기능을 사용 하 여 보기에 종속성 주입을 사용 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-231">In this exercise, you will learn how to use Dependency Injection in a view with the new features of ASP.NET MVC 4 for Unity integration.</span></span> <span data-ttu-id="f8da6-232">이 작업을 수행 하기 위해 메시지 및 아래 이미지로 표시 되는 저장소 찾아보기 보기 내에서 사용자 지정 서비스를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-232">In order to do that, you will call a custom service inside the Store Browse View, which will show a message and an image below.</span></span>

<span data-ttu-id="f8da6-233">그런 다음 Unity를 사용 하 여 프로젝트를 통합 하 고 종속성을 삽입 하는 사용자 지정 종속성 확인자를 만듭니다 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-233">Then, you will integrate the project with Unity and create a custom dependency resolver to inject the dependencies.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Creating_a_View_that_Consumes_a_Service"></a>
#### <a name="task-1---creating-a-view-that-consumes-a-service"></a><span data-ttu-id="f8da6-234">작업 1-서비스를 사용 하는 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="f8da6-234">Task 1 - Creating a View that Consumes a Service</span></span>

<span data-ttu-id="f8da6-235">이 태스크에서는 새 종속성을 생성 하는 서비스 호출을 수행 하는 뷰를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-235">In this task, you will create a view that performs a service call to generate a new dependency.</span></span> <span data-ttu-id="f8da6-236">이 솔루션에 포함 된 간단한 메시징 서비스에서 서비스 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-236">The service consists in a simple messaging service included in this solution.</span></span>

1. <span data-ttu-id="f8da6-237">엽니다는 **시작** 솔루션에는 **View\Begin Source\Ex02 삽입** 폴더.</span><span class="sxs-lookup"><span data-stu-id="f8da6-237">Open the **Begin** solution located in the **Source\Ex02-Injecting View\Begin** folder.</span></span> <span data-ttu-id="f8da6-238">그렇지 않은 경우 계속 사용할 수도 있습니다는 **최종** 이전 연습을 완료 하 여 가져온 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-238">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="f8da6-239">제공 된를 열면 **시작** 일부 누락 된 NuGet 패키지를 다운로드 해야 솔루션을 계속 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-239">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="f8da6-240">이 작업을 수행 하려면 클릭 합니다 **프로젝트** 선택한 메뉴 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-240">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="f8da6-241">에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="f8da6-241">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="f8da6-242">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-242">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="f8da6-243">NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-243">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="f8da6-244">NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-244">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="f8da6-245">이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-245">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
      > 
      > <span data-ttu-id="f8da6-246">자세한 내용은이 문서를 참조 하세요. [ http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages ](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-246">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="f8da6-247">포함 합니다 **MessageService.cs** 및 **IMessageService.cs** 클래스에는 **\Assets 원본** 폴더에 **/서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-247">Include the **MessageService.cs** and the **IMessageService.cs** classes located in the **Source \Assets** folder in **/Services**.</span></span> <span data-ttu-id="f8da6-248">이렇게 하려면 마우스 오른쪽 단추로 클릭 **Services** 선택한 폴더 **기존 항목 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-248">To do this, right-click **Services** folder and select **Add Existing Item**.</span></span> <span data-ttu-id="f8da6-249">파일의 위치를 찾아 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-249">Browse to the files' location and include them.</span></span>

    <span data-ttu-id="f8da6-250">![메시지 서비스 및 서비스 인터페이스를 추가](aspnet-mvc-4-dependency-injection/_static/image8.png "메시지 서비스 및 서비스 인터페이스를 추가 합니다.")</span><span class="sxs-lookup"><span data-stu-id="f8da6-250">![Adding Message Service and Service Interface](aspnet-mvc-4-dependency-injection/_static/image8.png "Adding Message Service and Service Interface")</span></span>

    <span data-ttu-id="f8da6-251">*추가 메시지 서비스 및 서비스 인터페이스*</span><span class="sxs-lookup"><span data-stu-id="f8da6-251">*Adding Message Service and Service Interface*</span></span>

    > [!NOTE]
    > <span data-ttu-id="f8da6-252">**IMessageService** 인터페이스에 의해 구현 되는 두 속성을 정의 합니다 **MessageService** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-252">The **IMessageService** interface defines two properties implemented by the **MessageService** class.</span></span> <span data-ttu-id="f8da6-253">이러한 속성-**메시지** 하 고 **ImageUrl**-표시할 메시지 및 이미지의 URL을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-253">These properties -**Message** and **ImageUrl**- store the message and the URL of the image to be displayed.</span></span>
3. <span data-ttu-id="f8da6-254">폴더를 만듭니다 **/pages** 프로젝트의 루트 폴더를 추가한 다음 기존 클래스 **MyBasePage.cs** 에서 **Source\Assets**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-254">Create the folder **/Pages** in the project's root folder, and then add the existing class **MyBasePage.cs** from **Source\Assets**.</span></span> <span data-ttu-id="f8da6-255">상속 하는 기본 페이지는 다음 구조를 가집니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-255">The base page you will inherit from has the following structure.</span></span>

    <span data-ttu-id="f8da6-256">![페이지 폴더](aspnet-mvc-4-dependency-injection/_static/image9.png "페이지 폴더")</span><span class="sxs-lookup"><span data-stu-id="f8da6-256">![Pages folder](aspnet-mvc-4-dependency-injection/_static/image9.png "Pages folder")</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample7.cs)]
4. <span data-ttu-id="f8da6-257">오픈 **Browse.cshtml** 에서 확인할 **/뷰/저장** 폴더에서 상속 하 고 **MyBasePage.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-257">Open **Browse.cshtml** view from **/Views/Store** folder, and make it inherit from **MyBasePage.cs**.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-dependency-injection/samples/sample8.cshtml)]
5. <span data-ttu-id="f8da6-258">에 **찾아보기** 보기에서 호출을 추가 **MessageService** 이미지 및 서비스에서 검색 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-258">In the **Browse** view, add a call to **MessageService** to display an image and a message retrieved by the service.</span></span>
   <span data-ttu-id="f8da6-259">(C#)</span><span class="sxs-lookup"><span data-stu-id="f8da6-259">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-dependency-injection/samples/sample9.cshtml)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Including_a_Custom_Dependency_Resolver_and_a_Custom_View_Page_Activator"></a>
#### <a name="task-2---including-a-custom-dependency-resolver-and-a-custom-view-page-activator"></a><span data-ttu-id="f8da6-260">작업 2-사용자 지정 종속성 확인자 및 사용자 지정 뷰 페이지 활성기를 포함 하 여</span><span class="sxs-lookup"><span data-stu-id="f8da6-260">Task 2 - Including a Custom Dependency Resolver and a Custom View Page Activator</span></span>

<span data-ttu-id="f8da6-261">이전 작업에서 내부 서비스 호출을 수행 하려면 뷰 내에서 새 종속성을 주입 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-261">In the previous task, you injected a new dependency inside a view to perform a service call inside it.</span></span> <span data-ttu-id="f8da6-262">ASP.NET MVC 종속성 주입 인터페이스를 구현 하 여 해당 종속성을 확인 되는 이제 **IViewPageActivator** 하 고 **IDependencyResolver**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-262">Now, you will resolve that dependency by implementing the ASP.NET MVC Dependency Injection interfaces **IViewPageActivator** and **IDependencyResolver**.</span></span> <span data-ttu-id="f8da6-263">구현 솔루션에 포함 됩니다 **IDependencyResolver** 는 Unity를 사용 하 여 서비스 검색을 사용 하 여 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-263">You will include in the solution an implementation of **IDependencyResolver** that will deal with the service retrieval by using Unity.</span></span> <span data-ttu-id="f8da6-264">다른 사용자 지정 구현이 포함 됩니다 차례로 **IViewPageActivator** 뷰의 생성을 해결할 수 있는 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-264">Then, you will include another custom implementation of **IViewPageActivator** interface that will solve the creation of the views.</span></span>

> [!NOTE]
> <span data-ttu-id="f8da6-265">ASP.NET MVC 3부터 종속성 주입에 대 한 구현을 서비스 등록에 대 한 인터페이스를 간소화 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-265">Since ASP.NET MVC 3, the implementation for Dependency Injection had simplified the interfaces to register services.</span></span> <span data-ttu-id="f8da6-266">**IDependencyResolver** 하 고 **IViewPageActivator** 종속성 주입을 위한 ASP.NET MVC 3 기능의 일부인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-266">**IDependencyResolver** and **IViewPageActivator** are part of ASP.NET MVC 3 features for Dependency Injection.</span></span>
> 
> <span data-ttu-id="f8da6-267">**-IDependencyResolver** 인터페이스 이전 IMvcServiceLocator를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-267">**- IDependencyResolver** interface replaces the previous IMvcServiceLocator.</span></span> <span data-ttu-id="f8da6-268">IDependencyResolver의 구현자는 서비스나 서비스 컬렉션의 인스턴스를 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-268">Implementers of IDependencyResolver must return an instance of the service or a service collection.</span></span>
> 
> 
> [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample10.cs)]
> 
> <span data-ttu-id="f8da6-269">**-IViewPageActivator** 인터페이스는 종속성 주입을 통해 페이지 보기가 인스턴스화될 방법을 보다 세부적으로 제어를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-269">**- IViewPageActivator** interface provides more fine-grained control over how view pages are instantiated via dependency injection.</span></span> <span data-ttu-id="f8da6-270">구현 하는 클래스 **IViewPageActivator** 인터페이스 컨텍스트 정보를 사용 하 여 인스턴스 보기를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-270">The classes that implement **IViewPageActivator** interface can create view instances using context information.</span></span>
> 
> 
> [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample11.cs)]


1. <span data-ttu-id="f8da6-271">만들기는 /**팩터리** 프로젝트의 루트 폴더의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-271">Create the /**Factories** folder in the project's root folder.</span></span>
2. <span data-ttu-id="f8da6-272">포함 **CustomViewPageActivator.cs** 에서 솔루션 **/자산/원본/** 하 **팩터리** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-272">Include **CustomViewPageActivator.cs** to your solution from **/Sources/Assets/** to **Factories** folder.</span></span> <span data-ttu-id="f8da6-273">이렇게 하려면 마우스 오른쪽 단추로 클릭 합니다 **/Factories** 폴더 **추가 | 기존 항목** 선택한 후 **CustomViewPageActivator.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-273">To do that, right-click the **/Factories** folder, select **Add | Existing Item** and then select **CustomViewPageActivator.cs**.</span></span> <span data-ttu-id="f8da6-274">이 클래스에서 구현 된 **IViewPageActivator** Unity 컨테이너를 보유 하는 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-274">This class implements the **IViewPageActivator** interface to hold the Unity Container.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample12.cs)]

    > [!NOTE]
    > <span data-ttu-id="f8da6-275">**CustomViewPageActivator** Unity 컨테이너를 사용 하 여 뷰를 만드는 관리 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-275">**CustomViewPageActivator** is responsible for managing the creation of a view by using a Unity container.</span></span>
3. <span data-ttu-id="f8da6-276">포함 **UnityDependencyResolver.cs** 에서 파일 **/원본/자산** 하 **/Factories** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-276">Include **UnityDependencyResolver.cs** file from **/Sources/Assets** to **/Factories** folder.</span></span> <span data-ttu-id="f8da6-277">이렇게 하려면 마우스 오른쪽 단추로 클릭 합니다 **/Factories** 폴더 **추가 | 기존 항목** 선택한 후 **UnityDependencyResolver.cs** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-277">To do that, right-click the **/Factories** folder, select **Add | Existing Item** and then select **UnityDependencyResolver.cs** file.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample13.cs)]

    > [!NOTE]
    > <span data-ttu-id="f8da6-278">**UnityDependencyResolver** 클래스는 Unity에 대 한 사용자 지정 DependencyResolver 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-278">**UnityDependencyResolver** class is a custom DependencyResolver for Unity.</span></span> <span data-ttu-id="f8da6-279">Unity 컨테이너 내에서 서비스를 찾을 수 없는 경우 기본 확인자 invocated 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-279">When a service cannot be found inside the Unity container, the base resolver is invocated.</span></span>

<span data-ttu-id="f8da6-280">다음 태스크에서 두 구현 모두 모델 뷰와 서비스의 위치를 알 수 있도록 등록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-280">In the following task both implementations will be registered to let the model know the location of the services and the views.</span></span>

<a id="Ex2Task3"></a>

<a id="Task_3_-_Registering_for_Dependency_Injection_within_Unity_container"></a>
#### <a name="task-3---registering-for-dependency-injection-within-unity-container"></a><span data-ttu-id="f8da6-281">작업 3-Unity 컨테이너 내에서 종속성 주입에 등록</span><span class="sxs-lookup"><span data-stu-id="f8da6-281">Task 3 - Registering for Dependency Injection within Unity container</span></span>

<span data-ttu-id="f8da6-282">이 태스크에서는 작동 하는 종속성 주입 하기 위해 모든 이전 항목을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-282">In this task, you will put all the previous things together to make Dependency Injection work.</span></span>

<span data-ttu-id="f8da6-283">지금까지 솔루션에는 다음과 같은 요소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-283">Up to now your solution has the following elements:</span></span>

- <span data-ttu-id="f8da6-284">A **찾아보기** 에서 상속 되는 뷰 **MyBaseClass** 들고 **MessageService**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-284">A **Browse** View that inherits from **MyBaseClass** and consumes **MessageService**.</span></span>
- <span data-ttu-id="f8da6-285">중간 클래스-**MyBaseClass**-서비스 인터페이스에 대해 선언 된 종속성 주입 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-285">An intermediate class -**MyBaseClass**- that has dependency injection declared for the service interface.</span></span>
- <span data-ttu-id="f8da6-286">서비스-A **MessageService** -및 해당 인터페이스 **IMessageService**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-286">A service - **MessageService** - and its interface **IMessageService**.</span></span>
- <span data-ttu-id="f8da6-287">Unity-에 대 한 사용자 지정 종속성 확인자 **UnityDependencyResolver** -서비스 검색을 사용 하 여 처리 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-287">A custom dependency resolver for Unity - **UnityDependencyResolver** - that deals with service retrieval.</span></span>
- <span data-ttu-id="f8da6-288">뷰 페이지 활성기를- **CustomViewPageActivator** -는 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-288">A View Page activator - **CustomViewPageActivator** - that creates the page.</span></span>

<span data-ttu-id="f8da6-289">삽입할 **찾아보기** 보기에서는 이제 사용자 지정 종속성 확인자에서에서 등록 Unity 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-289">To inject **Browse** View, you will now register the custom dependency resolver in the Unity container.</span></span>

1. <span data-ttu-id="f8da6-290">오픈 **Bootstrapper.cs** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-290">Open **Bootstrapper.cs** file.</span></span>
2. <span data-ttu-id="f8da6-291">인스턴스를 등록할 **MessageService** Unity 컨테이너 서비스를 초기화할 수에 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-291">Register an instance of **MessageService** into the Unity container to initialize the service:</span></span>

    <span data-ttu-id="f8da6-292">(코드 조각- *ASP.NET 종속성 주입-Ex02-랩 등록 메시지 서비스*)</span><span class="sxs-lookup"><span data-stu-id="f8da6-292">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex02 - Register Message Service*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample14.cs)]
3. <span data-ttu-id="f8da6-293">에 대 한 참조를 추가 **MvcMusicStore.Factories** 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-293">Add a reference to **MvcMusicStore.Factories** namespace.</span></span>

    <span data-ttu-id="f8da6-294">(코드 조각- *ASP.NET 종속성 주입-Ex02-랩 팩터리 Namespace*)</span><span class="sxs-lookup"><span data-stu-id="f8da6-294">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex02 - Factories Namespace*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample15.cs)]
4. <span data-ttu-id="f8da6-295">등록할 **CustomViewPageActivator** Unity 컨테이너에 뷰 페이지 활성기를으로:</span><span class="sxs-lookup"><span data-stu-id="f8da6-295">Register **CustomViewPageActivator** as a View Page activator into the Unity container:</span></span>

    <span data-ttu-id="f8da6-296">(코드 조각- *ASP.NET 종속성 주입-Ex02-랩 등록 CustomViewPageActivator*)</span><span class="sxs-lookup"><span data-stu-id="f8da6-296">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex02 - Register CustomViewPageActivator*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample16.cs)]
5. <span data-ttu-id="f8da6-297">ASP.NET MVC 4 기본 종속성 확인자 인스턴스의 바꿉니다 **UnityDependencyResolver**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-297">Replace ASP.NET MVC 4 default dependency resolver with an instance of **UnityDependencyResolver**.</span></span> <span data-ttu-id="f8da6-298">이 작업을 수행 하려면 바꿉니다 **Initialise** 콘텐츠를 다음 코드로 메서드:</span><span class="sxs-lookup"><span data-stu-id="f8da6-298">To do this, replace **Initialise** method content with the following code:</span></span>

    <span data-ttu-id="f8da6-299">(코드 조각- *ASP.NET 종속성 주입-Ex02-랩 업데이트 종속성 확인자*)</span><span class="sxs-lookup"><span data-stu-id="f8da6-299">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex02 - Update Dependency Resolver*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample17.cs)]

    > [!NOTE]
    > <span data-ttu-id="f8da6-300">ASP.NET MVC 기본 종속성 확인자 클래스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-300">ASP.NET MVC provides a default dependency resolver class.</span></span> <span data-ttu-id="f8da6-301">사용자 지정 종속성 확인 자의 unity에 작성 한 것을 사용 하려면이 확인자를 교체 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-301">To work with custom dependency resolvers as the one we have created for unity, this resolver has to be replaced.</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="f8da6-302">작업 4-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="f8da6-302">Task 4 - Running the Application</span></span>

<span data-ttu-id="f8da6-303">이 태스크에서는 저장소 브라우저 서비스를 사용 하 고 이미지 및 검색 메시지를 표시 하는지 확인 하려면 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-303">In this task, you will run the application to verify that the Store Browser consumes the service and shows the image and the message retrieved:</span></span>

1. <span data-ttu-id="f8da6-304">**F5** 키를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-304">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="f8da6-305">클릭 **Rock** 장르 메뉴 및 참조 내에서 하는 방법을 **MessageService** 뷰에 삽입 된 및 환영 메시지 및 이미지를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-305">Click **Rock** within the Genres Menu and see how the **MessageService** was injected to the view and loaded the welcome message and the image.</span></span> <span data-ttu-id="f8da6-306">에 진입 하 고이 예에서 &quot; **Rock**&quot;:</span><span class="sxs-lookup"><span data-stu-id="f8da6-306">In this example, we are entering to &quot;**Rock**&quot;:</span></span>

    <span data-ttu-id="f8da6-307">![MVC Music Store-보기 주입](aspnet-mvc-4-dependency-injection/_static/image10.png "MVC Music Store-보기 주입")</span><span class="sxs-lookup"><span data-stu-id="f8da6-307">![MVC Music Store - View Injection](aspnet-mvc-4-dependency-injection/_static/image10.png "MVC Music Store - View Injection")</span></span>

    <span data-ttu-id="f8da6-308">*MVC Music Store-보기 주입*</span><span class="sxs-lookup"><span data-stu-id="f8da6-308">*MVC Music Store - View Injection*</span></span>
3. <span data-ttu-id="f8da6-309">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-309">Close the browser.</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Injecting_Action_Filters"></a>
### <a name="exercise-3-injecting-action-filters"></a><span data-ttu-id="f8da6-310">연습 3: 삽입 작업 필터</span><span class="sxs-lookup"><span data-stu-id="f8da6-310">Exercise 3: Injecting Action Filters</span></span>

<span data-ttu-id="f8da6-311">이전 실습 랩에서 **사용자 지정 작업 필터** 필터 사용자 지정 및 삽입 작업을 수행한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-311">In the previous Hands-On lab **Custom Action Filters** you have worked with filters customization and injection.</span></span> <span data-ttu-id="f8da6-312">이 연습에서는 Unity 컨테이너를 사용 하 여 종속성 주입을 사용 하 여 필터를 주입 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-312">In this exercise, you will learn how to inject filters with Dependency Injection by using the Unity container.</span></span> <span data-ttu-id="f8da6-313">이렇게 하려면 추가 Music Store 솔루션에는 사이트의 작업을 추적 하는 사용자 지정 작업 필터.</span><span class="sxs-lookup"><span data-stu-id="f8da6-313">To do that, you will add to the Music Store solution a custom action filter that will trace the activity of the site.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Including_the_Tracking_Filter_in_the_Solution"></a>
#### <a name="task-1---including-the-tracking-filter-in-the-solution"></a><span data-ttu-id="f8da6-314">작업 1-추적 필터를 포함 하 여 솔루션의</span><span class="sxs-lookup"><span data-stu-id="f8da6-314">Task 1 - Including the Tracking Filter in the Solution</span></span>

<span data-ttu-id="f8da6-315">이 태스크에서는 Music Store에서 사용자 지정 작업 필터 추적 이벤트를 포함할가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-315">In this task, you will include in the Music Store a custom action filter to trace events.</span></span> <span data-ttu-id="f8da6-316">사용자 지정 작업 필터로 개념 이미 처리할지 이전 랩에서 &quot;사용자 지정 작업 필터&quot;,에서는 바로이 랩의 자산 폴더에서 필터 클래스를 포함 하 고 다음 Unity에 대 한 필터 공급자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-316">As custom action filter concepts are already treated in the previous Lab &quot;Custom Action Filters&quot;, you will just include the filter class from the Assets folder of this lab, and then create a Filter Provider for Unity:</span></span>

1. <span data-ttu-id="f8da6-317">엽니다는 **시작** 솔루션에는 **Source\Ex03-삽입 작업 Filter\Begin** 폴더.</span><span class="sxs-lookup"><span data-stu-id="f8da6-317">Open the **Begin** solution located in the **Source\Ex03 - Injecting Action Filter\Begin** folder.</span></span> <span data-ttu-id="f8da6-318">그렇지 않은 경우 계속 사용할 수도 있습니다는 **최종** 이전 연습을 완료 하 여 가져온 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-318">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="f8da6-319">제공 된를 열면 **시작** 일부 누락 된 NuGet 패키지를 다운로드 해야 솔루션을 계속 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-319">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="f8da6-320">이 작업을 수행 하려면 클릭 합니다 **프로젝트** 선택한 메뉴 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-320">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="f8da6-321">에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="f8da6-321">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="f8da6-322">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-322">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="f8da6-323">NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-323">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="f8da6-324">NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-324">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="f8da6-325">이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-325">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
      > 
      > <span data-ttu-id="f8da6-326">자세한 내용은이 문서를 참조 하세요. [ http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages ](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-326">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="f8da6-327">포함 **TraceActionFilter.cs** 에서 파일 **/원본/자산** 하 **필터링/** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-327">Include **TraceActionFilter.cs** file from **/Sources/Assets** to **/Filters** folder.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample18.cs)]

    > [!NOTE]
    > <span data-ttu-id="f8da6-328">이 사용자 지정 작업 필터는 ASP.NET 추적을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-328">This custom action filter performs ASP.NET tracing.</span></span> <span data-ttu-id="f8da6-329">확인할 수 있습니다 &quot;ASP.NET MVC 4 로컬 및 동적 작업 필터&quot; 랩 더 많은 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-329">You can check &quot;ASP.NET MVC 4 local and Dynamic Action Filters&quot; Lab for more reference.</span></span>
3. <span data-ttu-id="f8da6-330">빈 클래스를 추가 **FilterProvider.cs** 에서 프로젝트 폴더에   **/필터링 합니다.**</span><span class="sxs-lookup"><span data-stu-id="f8da6-330">Add the empty class **FilterProvider.cs** to the project in the folder **/Filters.**</span></span>
4. <span data-ttu-id="f8da6-331">추가 합니다 **System.Web.Mvc** 하 고 **Microsoft.Practices.Unity** 네임 스페이스 **FilterProvider.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-331">Add the **System.Web.Mvc** and **Microsoft.Practices.Unity** namespaces in **FilterProvider.cs**.</span></span>

    <span data-ttu-id="f8da6-332">(코드 조각- *ASP.NET 종속성 주입-Ex03-랩 필터 공급자 네임 스페이스 추가*)</span><span class="sxs-lookup"><span data-stu-id="f8da6-332">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Filter Provider Adding Namespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample19.cs)]
5. <span data-ttu-id="f8da6-333">클래스에서 상속 **IFilterProvider** 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-333">Make the class inherit from **IFilterProvider** Interface.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample20.cs)]
6. <span data-ttu-id="f8da6-334">추가 **IUnityContainer** 속성에는 **FilterProvider** 클래스를 만든 다음 컨테이너를 할당 하기 위해 클래스 생성자입니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-334">Add a **IUnityContainer** property in the **FilterProvider** class, and then create a class constructor to assign the container.</span></span>

    <span data-ttu-id="f8da6-335">(코드 조각- *ASP.NET 종속성 주입-Ex03-랩 필터 공급자 생성자*)</span><span class="sxs-lookup"><span data-stu-id="f8da6-335">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Filter Provider Constructor*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample21.cs)]

    > [!NOTE]
    > <span data-ttu-id="f8da6-336">필터 공급자 클래스 생성자를 만들지는 **새** 내부 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-336">The filter provider class constructor is not creating a **new** object inside.</span></span> <span data-ttu-id="f8da6-337">컨테이너 매개 변수로 전달 하 고 Unity 종속성 해결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-337">The container is passed as a parameter, and the dependency is solved by Unity.</span></span>
7. <span data-ttu-id="f8da6-338">에 **FilterProvider** 클래스, 메서드를 구현 **GetFilters** 에서 **IFilterProvider** 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-338">In the **FilterProvider** class, implement the method **GetFilters** from **IFilterProvider** interface.</span></span>

    <span data-ttu-id="f8da6-339">(코드 조각- *ASP.NET 종속성 주입-Ex03-랩 필터 공급자 GetFilters*)</span><span class="sxs-lookup"><span data-stu-id="f8da6-339">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Filter Provider GetFilters*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample22.cs)]

<a id="Ex3Task2"></a>

<a id="Task_2_-_Registering_and_Enabling_the_Filter"></a>
#### <a name="task-2---registering-and-enabling-the-filter"></a><span data-ttu-id="f8da6-340">작업 2-등록 하 고 필터를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="f8da6-340">Task 2 - Registering and Enabling the Filter</span></span>

<span data-ttu-id="f8da6-341">이 태스크에서는 사이트 추적 사용 하도록 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-341">In this task, you will enable site tracking.</span></span> <span data-ttu-id="f8da6-342">이렇게 하려면 필터를 등록할 **Bootstrapper.cs BuildUnityContainer** 추적을 시작 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="f8da6-342">To do that, you will register the filter in **Bootstrapper.cs BuildUnityContainer** method to start tracing:</span></span>

1. <span data-ttu-id="f8da6-343">오픈 **Web.config** System.Web 그룹에서 사용 추적 추적 고 프로젝트 루트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-343">Open **Web.config** located in the project root and enable trace tracking at System.Web group.</span></span>

    [!code-xml[Main](aspnet-mvc-4-dependency-injection/samples/sample23.xml)]
2. <span data-ttu-id="f8da6-344">오픈 **Bootstrapper.cs** 프로젝트 루트에서.</span><span class="sxs-lookup"><span data-stu-id="f8da6-344">Open **Bootstrapper.cs** at project root.</span></span>
3. <span data-ttu-id="f8da6-345">에 대 한 참조를 추가 합니다 **MvcMusicStore.Filters** 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-345">Add a reference to the **MvcMusicStore.Filters** namespace.</span></span>

    <span data-ttu-id="f8da6-346">(코드 조각- *네임 스페이스를 추가 하는 ASP.NET 종속성 주입-Ex03-랩 부트스트래퍼*)</span><span class="sxs-lookup"><span data-stu-id="f8da6-346">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Bootstrapper Adding Namespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample24.cs)]
4. <span data-ttu-id="f8da6-347">선택 된 **BuildUnityContainer** 메서드 및 Unity 컨테이너에서 필터를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-347">Select the **BuildUnityContainer** method and register the filter in the Unity Container.</span></span> <span data-ttu-id="f8da6-348">작업 필터와 필터 공급자를 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-348">You will have to register the filter provider as well as the action filter.</span></span>

    <span data-ttu-id="f8da6-349">(코드 조각- *ASP.NET 종속성 주입-Ex03-랩 등록 FilterProvider 및 ActionFilter*)</span><span class="sxs-lookup"><span data-stu-id="f8da6-349">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Register FilterProvider and ActionFilter*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample25.cs)]

<a id="Ex3Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="f8da6-350">작업 3-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="f8da6-350">Task 3 - Running the Application</span></span>

<span data-ttu-id="f8da6-351">이 태스크에서는 응용 프로그램을 실행 하 고 사용자 지정 작업 필터는 활동 추적는 테스트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-351">In this task, you will run the application and test that the custom action filter is tracing the activity:</span></span>

1. <span data-ttu-id="f8da6-352">**F5** 키를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-352">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="f8da6-353">클릭 **Rock** 장르 메뉴 내에서.</span><span class="sxs-lookup"><span data-stu-id="f8da6-353">Click **Rock** within the Genres Menu.</span></span> <span data-ttu-id="f8da6-354">하려는 경우 자세한 장르를 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-354">You can browse to more genres if you want to.</span></span>

    <span data-ttu-id="f8da6-355">![Music Store](aspnet-mvc-4-dependency-injection/_static/image11.png "Music Store")</span><span class="sxs-lookup"><span data-stu-id="f8da6-355">![Music Store](aspnet-mvc-4-dependency-injection/_static/image11.png "Music Store")</span></span>

    <span data-ttu-id="f8da6-356">*Music Store*</span><span class="sxs-lookup"><span data-stu-id="f8da6-356">*Music Store*</span></span>
3. <span data-ttu-id="f8da6-357">이동할 **/Trace.axd** 페이지를 선택한 다음 클릭 응용 프로그램 추적을 보려는 **세부 정보 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-357">Browse to **/Trace.axd** to see the Application Trace page, and then click **View Details**.</span></span>

    <span data-ttu-id="f8da6-358">![응용 프로그램 추적 로그](aspnet-mvc-4-dependency-injection/_static/image12.png "응용 프로그램 추적 로그")</span><span class="sxs-lookup"><span data-stu-id="f8da6-358">![Application Trace Log](aspnet-mvc-4-dependency-injection/_static/image12.png "Application Trace Log")</span></span>

    <span data-ttu-id="f8da6-359">*응용 프로그램 추적 로그*</span><span class="sxs-lookup"><span data-stu-id="f8da6-359">*Application Trace Log*</span></span>

    <span data-ttu-id="f8da6-360">![응용 프로그램 추적-요청 세부 정보](aspnet-mvc-4-dependency-injection/_static/image13.png "응용 프로그램 추적-요청 정보")</span><span class="sxs-lookup"><span data-stu-id="f8da6-360">![Application Trace - Request Details](aspnet-mvc-4-dependency-injection/_static/image13.png "Application Trace - Request Details")</span></span>

    <span data-ttu-id="f8da6-361">*응용 프로그램 추적-요청 세부 정보*</span><span class="sxs-lookup"><span data-stu-id="f8da6-361">*Application Trace - Request Details*</span></span>
4. <span data-ttu-id="f8da6-362">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-362">Close the browser.</span></span>

* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="f8da6-363">요약</span><span class="sxs-lookup"><span data-stu-id="f8da6-363">Summary</span></span>

<span data-ttu-id="f8da6-364">이 실습을 완료 하 여 NuGet 패키지를 사용 하는 Unity를 통합 하 여 ASP.NET MVC 4에서 종속성 주입을 사용 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-364">By completing this Hands-On Lab you have learned how to use Dependency Injection in ASP.NET MVC 4 by integrating Unity using a NuGet Package.</span></span> <span data-ttu-id="f8da6-365">이 위해 컨트롤러, 보기 및 작업 필터 내에서 종속성 주입을 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-365">To achieve that, you have used Dependency Injection inside controllers, views and action filters.</span></span>

<span data-ttu-id="f8da6-366">다음 개념 적용 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-366">The following concepts were covered:</span></span>

- <span data-ttu-id="f8da6-367">ASP.NET MVC 4 종속성 주입 기능</span><span class="sxs-lookup"><span data-stu-id="f8da6-367">ASP.NET MVC 4 Dependency Injection features</span></span>
- <span data-ttu-id="f8da6-368">Unity 통합 Unity.Mvc3 NuGet 패키지를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="f8da6-368">Unity integration using Unity.Mvc3 NuGet Package</span></span>
- <span data-ttu-id="f8da6-369">컨트롤러에서 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="f8da6-369">Dependency Injection in Controllers</span></span>
- <span data-ttu-id="f8da6-370">뷰에 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="f8da6-370">Dependency Injection in Views</span></span>
- <span data-ttu-id="f8da6-371">작업 필터의 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="f8da6-371">Dependency injection of Action Filters</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="f8da6-372">부록 a: 설치 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="f8da6-372">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="f8da6-373">설치할 수 있습니다 **Microsoft Visual Studio Express 2012 for Web** 또는 다른 &quot;Express&quot; 사용 하 여 버전을 **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="f8da6-373">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="f8da6-374">다음 지침을 설치 하는 데 필요한 단계를 안내 *Visual studio Express 2012 for Web* 사용 하 여 *Microsoft Web Platform Installer*합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-374">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="f8da6-375">로 이동 [ [ https://go.microsoft.com/? linkid 9810169 =](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-375">Go to [[https://go.microsoft.com/? linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="f8da6-376">또는, 이미 설치한 경우 웹 플랫폼 설치 관리자를 열 수 있습니다 하 고 제품에 대 한 검색 &quot; <em>Visual Studio Express 2012 for Windows Azure SDK를 사용 하 여 Web</em>&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-376">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="f8da6-377">클릭할 **지금 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-377">Click on **Install Now**.</span></span> <span data-ttu-id="f8da6-378">없는 경우 **웹 플랫폼 설치 관리자** 를 다운로드 하 여 앱을 먼저 설치 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-378">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="f8da6-379">한 번 **웹 플랫폼 설치 관리자** 열려 있는 경우 클릭 **설치** 는 설치를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-379">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="f8da6-380">![Visual Studio Express를 설치](aspnet-mvc-4-dependency-injection/_static/image14.png "Visual Studio Express를 설치 합니다.")</span><span class="sxs-lookup"><span data-stu-id="f8da6-380">![Install Visual Studio Express](aspnet-mvc-4-dependency-injection/_static/image14.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="f8da6-381">*Visual Studio Express를 설치 합니다.*</span><span class="sxs-lookup"><span data-stu-id="f8da6-381">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="f8da6-382">모든 제품의 라이선스 및 용어를 읽고 클릭 **동의** 를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-382">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![사용 조건에 동의](aspnet-mvc-4-dependency-injection/_static/image15.png)

    <span data-ttu-id="f8da6-384">*사용 조건에 동의*</span><span class="sxs-lookup"><span data-stu-id="f8da6-384">*Accepting the license terms*</span></span>
5. <span data-ttu-id="f8da6-385">다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-385">Wait until the downloading and installation process completes.</span></span>

    ![설치 진행률](aspnet-mvc-4-dependency-injection/_static/image16.png)

    <span data-ttu-id="f8da6-387">*설치 진행률*</span><span class="sxs-lookup"><span data-stu-id="f8da6-387">*Installation progress*</span></span>
6. <span data-ttu-id="f8da6-388">설치가 완료 되 면 클릭 **완료**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-388">When the installation completes, click **Finish**.</span></span>

    ![설치 완료](aspnet-mvc-4-dependency-injection/_static/image17.png)

    <span data-ttu-id="f8da6-390">*설치 완료*</span><span class="sxs-lookup"><span data-stu-id="f8da6-390">*Installation completed*</span></span>
7. <span data-ttu-id="f8da6-391">클릭 **종료** 를 웹 플랫폼 설치 관리자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-391">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="f8da6-392">로 Visual Studio Express for Web을 열려면 합니다 **시작** 화면 및 쓰기를 시작 &quot; **VS Express**&quot;를 클릭 합니다 **VS Express for Web** 타일입니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-392">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 타일](aspnet-mvc-4-dependency-injection/_static/image18.png)

    <span data-ttu-id="f8da6-394">*VS Express for Web 타일*</span><span class="sxs-lookup"><span data-stu-id="f8da6-394">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a><span data-ttu-id="f8da6-395">부록 b: 코드 조각 사용</span><span class="sxs-lookup"><span data-stu-id="f8da6-395">Appendix B: Using Code Snippets</span></span>

<span data-ttu-id="f8da6-396">코드 조각을 사용 하 여 결정적인 순간에 필요한 모든 코드를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-396">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="f8da6-397">랩 문서가 알려줍니다 정확 하 게 사용할 수 있는 시기를 다음 그림과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-397">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="f8da6-398">![Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드를 삽입할](aspnet-mvc-4-dependency-injection/_static/image19.png "프로젝트에 코드를 삽입 하는 Visual Studio를 사용 하 여 코드 조각을")</span><span class="sxs-lookup"><span data-stu-id="f8da6-398">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-dependency-injection/_static/image19.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="f8da6-399">*프로젝트에 코드를 삽입 하려면 Visual Studio 코드 조각 사용*</span><span class="sxs-lookup"><span data-stu-id="f8da6-399">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="f8da6-400">***키보드 (C#만 해당)를 사용 하 여 코드 조각을 추가 하려면***</span><span class="sxs-lookup"><span data-stu-id="f8da6-400">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="f8da6-401">코드를 삽입 하려는 위치에 커서를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-401">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="f8da6-402">시작 (공백 없이 하이픈) 조각 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-402">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="f8da6-403">IntelliSense 표시 조각 이름과 일치 하는 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-403">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="f8da6-404">올바른 코드 조각을 선택 합니다 (또는 전체 코드 조각 이름을 선택 될 때까지 입력 유지).</span><span class="sxs-lookup"><span data-stu-id="f8da6-404">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="f8da6-405">커서 위치에 코드 조각을 삽입 하려면 두 번 탭 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-405">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="f8da6-406">![코드 조각 이름을 입력](aspnet-mvc-4-dependency-injection/_static/image20.png "조각 이름을 입력 하기 시작")</span><span class="sxs-lookup"><span data-stu-id="f8da6-406">![Start typing the snippet name](aspnet-mvc-4-dependency-injection/_static/image20.png "Start typing the snippet name")</span></span>

<span data-ttu-id="f8da6-407">*코드 조각 이름을 입력 하기 시작*</span><span class="sxs-lookup"><span data-stu-id="f8da6-407">*Start typing the snippet name*</span></span>

<span data-ttu-id="f8da6-408">![Tab 키를 눌러 강조 표시 된 코드 조각을](aspnet-mvc-4-dependency-injection/_static/image21.png "Tab 키를 눌러 강조 표시 된 코드 조각 선택")</span><span class="sxs-lookup"><span data-stu-id="f8da6-408">![Press Tab to select the highlighted snippet](aspnet-mvc-4-dependency-injection/_static/image21.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="f8da6-409">*Tab 키를 눌러 강조 표시 된 코드 조각 선택*</span><span class="sxs-lookup"><span data-stu-id="f8da6-409">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="f8da6-410">![Tab 키를 다시 코드 조각 확장 됩니다](aspnet-mvc-4-dependency-injection/_static/image22.png "다시 Tab 키를 누릅니다 하 고 코드 조각에서는 확장")</span><span class="sxs-lookup"><span data-stu-id="f8da6-410">![Press Tab again and the snippet will expand](aspnet-mvc-4-dependency-injection/_static/image22.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="f8da6-411">*Tab 키를 다시 및 코드 조각에서는 확장*</span><span class="sxs-lookup"><span data-stu-id="f8da6-411">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="f8da6-412">***마우스 (C#, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가할*** 1입니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-412">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="f8da6-413">코드 조각을 삽입 하려면 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-413">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="f8da6-414">선택 **코드 조각 삽입** 뒤 **내 코드 조각**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-414">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="f8da6-415">클릭 하 여 목록에서 관련 코드 조각을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8da6-415">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="f8da6-416">![코드 조각을 삽입 하 고 코드 조각 삽입을 선택 하려는 마우스 오른쪽 단추로 클릭](aspnet-mvc-4-dependency-injection/_static/image23.png "코드 조각을 삽입 하 고 코드 조각 삽입을 선택 하려는 마우스 오른쪽 단추로 클릭")</span><span class="sxs-lookup"><span data-stu-id="f8da6-416">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-dependency-injection/_static/image23.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="f8da6-417">*코드 조각을 삽입할 선택한 코드 조각 삽입 하려는 위치를 마우스 오른쪽 단추로 클릭*</span><span class="sxs-lookup"><span data-stu-id="f8da6-417">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="f8da6-418">![클릭 하 여 목록에서 관련 코드 조각 선택](aspnet-mvc-4-dependency-injection/_static/image24.png "클릭 하 여 목록에서 관련 코드 조각 선택")</span><span class="sxs-lookup"><span data-stu-id="f8da6-418">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-dependency-injection/_static/image24.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="f8da6-419">*클릭 하 여 목록에서 관련 코드 조각 선택*</span><span class="sxs-lookup"><span data-stu-id="f8da6-419">*Pick the relevant snippet from the list, by clicking on it*</span></span>
