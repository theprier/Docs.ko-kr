---
uid: web-api/overview/advanced/dependency-injection
title: ASP.NET Web API 2에서에서 종속성 주입 | Microsoft Docs
author: MikeWasson
description: 이 자습서에서는 ASP.NET Web API 컨트롤러에 종속성을 주입 하는 방법을 보여줍니다. 자습서 웹 API 2 Unity Application Block에 사용 되는 소프트웨어 버전 중...
ms.author: aspnetcontent
ms.date: 01/20/2014
ms.assetid: e3d3e7ba-87f0-4032-bdd3-31f3c1aa9d9c
msc.legacyurl: /web-api/overview/advanced/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: a470c778fd5998006a0bf8edb08b62a75d72c48c
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37802677"
---
<a name="dependency-injection-in-aspnet-web-api-2"></a><span data-ttu-id="c621a-104">ASP.NET Web API 2에서에서 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="c621a-104">Dependency Injection in ASP.NET Web API 2</span></span>
====================
<span data-ttu-id="c621a-105">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="c621a-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="c621a-106">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="c621a-106">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-468ee148)

> <span data-ttu-id="c621a-107">이 자습서에서는 ASP.NET Web API 컨트롤러에 종속성을 주입 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-107">This tutorial shows how to inject dependencies into your ASP.NET Web API controller.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="c621a-108">이 자습서에 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="c621a-108">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="c621a-109">Web API 2</span><span class="sxs-lookup"><span data-stu-id="c621a-109">Web API 2</span></span>
> - [<span data-ttu-id="c621a-110">Unity Application Block</span><span class="sxs-lookup"><span data-stu-id="c621a-110">Unity Application Block</span></span>](https://www.nuget.org/packages/Unity/)
> - <span data-ttu-id="c621a-111">Entity Framework 6 (버전 5 에서도 작동)</span><span class="sxs-lookup"><span data-stu-id="c621a-111">Entity Framework 6 (version 5 also works)</span></span>


## <a name="what-is-dependency-injection"></a><span data-ttu-id="c621a-112">종속성 주입 이란?</span><span class="sxs-lookup"><span data-stu-id="c621a-112">What is Dependency Injection?</span></span>

<span data-ttu-id="c621a-113">A *종속성* 다른 개체는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-113">A *dependency* is any object that another object requires.</span></span> <span data-ttu-id="c621a-114">예를 들어 정의에 공통적으로 적용 되는 [리포지토리](http://martinfowler.com/eaaCatalog/repository.html) 데이터 액세스를 처리 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-114">For example, it's common to define a [repository](http://martinfowler.com/eaaCatalog/repository.html) that handles data access.</span></span> <span data-ttu-id="c621a-115">예를 들어 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-115">Let's illustrate with an example.</span></span> <span data-ttu-id="c621a-116">첫째, 도메인 모델을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-116">First, we'll define a domain model:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

<span data-ttu-id="c621a-117">Entity Framework를 사용 하 여 데이터베이스에서 항목을 저장 하는 간단한 저장소 클래스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-117">Here is a simple repository class that stores items in a database, using Entity Framework.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

<span data-ttu-id="c621a-118">이제 Web API 컨트롤러에 대 한 GET 요청을 지를 정의 하겠습니다 `Product` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="c621a-118">Now let's define a Web API controller that supports GET requests for `Product` entities.</span></span> <span data-ttu-id="c621a-119">(겠다 게시물 및 단순성에 대 한 다른 방법을.) 첫 번째 시도 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-119">(I'm leaving out POST and other methods for simplicity.) Here is a first attempt:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

<span data-ttu-id="c621a-120">컨트롤러 클래스에 따라 달라 집니다 `ProductRepository`를 만들 컨트롤러는 우리가 하는 `ProductRepository` 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="c621a-120">Notice that the controller class depends on `ProductRepository`, and we are letting the controller create the `ProductRepository` instance.</span></span> <span data-ttu-id="c621a-121">그러나 여러 가지 이유로 이러한 방식으로 종속성 하드 코드 하는 것은입니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-121">However, it's a bad idea to hard code the dependency in this way, for several reasons.</span></span>

- <span data-ttu-id="c621a-122">바꾸려는 경우 `ProductRepository` 를 다른 구현 해야 컨트롤러 클래스를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-122">If you want to replace `ProductRepository` with a different implementation, you also need to modify the controller class.</span></span>
- <span data-ttu-id="c621a-123">경우는 `ProductRepository` 종속성에 컨트롤러 내에서 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-123">If the `ProductRepository` has dependencies, you must configure these inside the controller.</span></span> <span data-ttu-id="c621a-124">여러 컨트롤러를 사용 하 여 대규모 프로젝트에 대 한 구성 코드 프로젝트에 분산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-124">For a large project with multiple controllers, your configuration code becomes scattered across your project.</span></span>
- <span data-ttu-id="c621a-125">하기 어렵습니다 단위 테스트, 컨트롤러 데이터베이스를 쿼리하고도 하드 코딩 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-125">It is hard to unit test, because the controller is hard-coded to query the database.</span></span> <span data-ttu-id="c621a-126">단위 테스트의 경우와 두고 디자인 가능 하지는 mock 또는 스텁 리포지토리를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-126">For a unit test, you should use a mock or stub repository, which is not possible with the currect design.</span></span>

<span data-ttu-id="c621a-127">이러한 문제를 처리할 수 있었습니다 *삽입* 저장소 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-127">We can address these problems by *injecting* the repository into the controller.</span></span> <span data-ttu-id="c621a-128">첫째, 리팩터링는 `ProductRepository` 인터페이스 클래스:</span><span class="sxs-lookup"><span data-stu-id="c621a-128">First, refactor the `ProductRepository` class into an interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

<span data-ttu-id="c621a-129">제공 된 `IProductRepository` 생성자 매개 변수로:</span><span class="sxs-lookup"><span data-stu-id="c621a-129">Then provide the `IProductRepository` as a constructor parameter:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

<span data-ttu-id="c621a-130">이 예제에서는 [생성자 주입](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection)합니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-130">This example uses [constructor injection](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection).</span></span> <span data-ttu-id="c621a-131">사용할 수도 있습니다 *setter 주입*setter 메서드 또는 속성을 통해 종속성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-131">You can also use *setter injection*, where you set the dependency through a setter method or property.</span></span>

<span data-ttu-id="c621a-132">하지만 이제 문제가 있어 응용 프로그램 컨트롤러를 직접 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-132">But now there is a problem, because your application doesn't create the controller directly.</span></span> <span data-ttu-id="c621a-133">Web API 요청을 라우팅하고 Web API는 모든 것을 인식 하지 못합니다 때 컨트롤러를 만듭니다 `IProductRepository`합니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-133">Web API creates the controller when it routes the request, and Web API doesn't know anything about `IProductRepository`.</span></span> <span data-ttu-id="c621a-134">Web API 종속성 확인자 제공 되는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-134">This is where the Web API dependency resolver comes in.</span></span>

## <a name="the-web-api-dependency-resolver"></a><span data-ttu-id="c621a-135">웹 API 종속성 확인자</span><span class="sxs-lookup"><span data-stu-id="c621a-135">The Web API Dependency Resolver</span></span>

<span data-ttu-id="c621a-136">웹 API를 정의 합니다 **IDependencyResolver** 종속성 확인에 대 한 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-136">Web API defines the **IDependencyResolver** interface for resolving dependencies.</span></span> <span data-ttu-id="c621a-137">인터페이스의 정의 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-137">Here is the definition of the interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

<span data-ttu-id="c621a-138">합니다 **IDependencyScope** 인터페이스에 두 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-138">The **IDependencyScope** interface has two methods:</span></span>

- <span data-ttu-id="c621a-139">**GetService** 는 형식의 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-139">**GetService** creates one instance of a type.</span></span>
- <span data-ttu-id="c621a-140">**GetServices** 지정 된 형식의 개체의 컬렉션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-140">**GetServices** creates a collection of objects of a specified type.</span></span>

<span data-ttu-id="c621a-141">합니다 **IDependencyResolver** 메서드를 상속 **IDependencyScope** 추가 합니다 **BeginScope** 메서드.</span><span class="sxs-lookup"><span data-stu-id="c621a-141">The **IDependencyResolver** method inherits **IDependencyScope** and adds the **BeginScope** method.</span></span> <span data-ttu-id="c621a-142">이 자습서의 뒷부분에서 범위에 대 한 이야기 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-142">I'll talk about scopes later in this tutorial.</span></span>

<span data-ttu-id="c621a-143">Web API 컨트롤러 인스턴스를 만드는 경우 먼저 호출한 **IDependencyResolver.GetService**컨트롤러 형식에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-143">When Web API creates a controller instance, it first calls **IDependencyResolver.GetService**, passing in the controller type.</span></span> <span data-ttu-id="c621a-144">모든 종속성을 확인할 컨트롤러를 만들려면이 확장성 후크를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-144">You can use this extensibility hook to create the controller, resolving any dependencies.</span></span> <span data-ttu-id="c621a-145">하는 경우 **GetService** null을 반환, Web API 컨트롤러 클래스에 있는 매개 변수가 없는 생성자를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-145">If **GetService** returns null, Web API looks for a parameterless constructor on the controller class.</span></span>

## <a name="dependency-resolution-with-the-unity-container"></a><span data-ttu-id="c621a-146">Unity 컨테이너를 사용 하 여 종속성 확인</span><span class="sxs-lookup"><span data-stu-id="c621a-146">Dependency Resolution with the Unity Container</span></span>

<span data-ttu-id="c621a-147">전체를 작성할 수 있지만 **IDependencyResolver** Web API와 기존 IoC 컨테이너 간의 브리지 역할을 실제로부터 인터페이스를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-147">Although you could write a complete **IDependencyResolver** implementation from scratch, the interface is really designed to act as bridge between Web API and existing IoC containers.</span></span>

<span data-ttu-id="c621a-148">IoC 컨테이너는 종속성을 관리 하는 일을 담당 하는 소프트웨어 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-148">An IoC container is a software component that is responsible for managing dependencies.</span></span> <span data-ttu-id="c621a-149">컨테이너로 형식을 등록 하 고이 정보를 개체를 만드는 컨테이너를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-149">You register types with the container, and then use the container to create objects.</span></span> <span data-ttu-id="c621a-150">컨테이너는 자동으로 종속성 관계를 파악합니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-150">The container automatically figures out the dependency relations.</span></span> <span data-ttu-id="c621a-151">많은 IoC 컨테이너를 사용 하면 개체 수명 및 범위와 같은 항목을 제어할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-151">Many IoC containers also allow you to control things like object lifetime and scope.</span></span>

> [!NOTE]
> <span data-ttu-id="c621a-152">"IoC"는 "제어 반전"에 대 한 일반적인 패턴을 설정 하는 프레임 워크 응용 프로그램 코드를 호출 하는 경우이 합니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-152">"IoC" stands for "inversion of control", which is a general pattern where a framework calls into application code.</span></span> <span data-ttu-id="c621a-153">IoC 컨테이너 생성 개체를 "반전" 컨트롤의 일반적인 흐름입니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-153">An IoC container constructs your objects for you, which "inverts" the usual flow of control.</span></span>


<span data-ttu-id="c621a-154">이 자습서에서는 [Unity](https://msdn.microsoft.com/library/ff647202.aspx) 에서 Microsoft Patterns &amp; 사례입니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-154">For this tutorial, we'll use [Unity](https://msdn.microsoft.com/library/ff647202.aspx) from Microsoft Patterns &amp; Practices.</span></span> <span data-ttu-id="c621a-155">(다른 인기 있는 라이브러리 포함 [Castle Windsor](http://www.castleproject.org/)를 [Spring.Net](http://www.springframework.net/)를 [Autofac](https://code.google.com/p/autofac/)를 [Ninject](http://www.ninject.org/), 및 [StructureMap ](http://docs.structuremap.net/).) Unity를 설치 하려면 NuGet 패키지 관리자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-155">(Other popular libraries include [Castle Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Ninject](http://www.ninject.org/), and [StructureMap](http://docs.structuremap.net/).) You can use NuGet Package Manager to install Unity.</span></span> <span data-ttu-id="c621a-156">**도구** Visual Studio에서 메뉴 **라이브러리 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-156">From the **Tools** menu in Visual Studio, select **Library Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="c621a-157">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-157">In the Package Manager Console window, type the following command:</span></span>

[!code-console[Main](dependency-injection/samples/sample7.cmd)]

<span data-ttu-id="c621a-158">여기의 구현인 **IDependencyResolver** Unity 컨테이너를 래핑합니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-158">Here is an implementation of **IDependencyResolver** that wraps a Unity container.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample8.cs)]

> [!NOTE]
> <span data-ttu-id="c621a-159">경우는 **GetService** 메서드는 형식을 확인할 수 없습니다, 반환할 **null**합니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-159">If the **GetService** method cannot resolve a type, it should return **null**.</span></span> <span data-ttu-id="c621a-160">경우는 **GetServices** 메서드는 형식을 확인할 수 없습니다, 빈 컬렉션 개체를 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-160">If the **GetServices** method cannot resolve a type, it should return an empty collection object.</span></span> <span data-ttu-id="c621a-161">알 수 없는 형식에 대 한 예외를 throw 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="c621a-161">Don't throw exceptions for unknown types.</span></span>


## <a name="configuring-the-dependency-resolver"></a><span data-ttu-id="c621a-162">종속성 확인자를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-162">Configuring the Dependency Resolver</span></span>

<span data-ttu-id="c621a-163">종속성 확인자를 설정 합니다 **DependencyResolver** 은 전역 **HttpConfiguration** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-163">Set the dependency resolver on the **DependencyResolver** property of the global **HttpConfiguration** object.</span></span>

<span data-ttu-id="c621a-164">다음 코드는 등록 된 `IProductRepository` Unity를 사용 하 여 인터페이스를 만듭니다를 `UnityResolver`합니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-164">The following code registers the `IProductRepository` interface with Unity and then creates a `UnityResolver`.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

## <a name="dependency-scope-and-controller-lifetime"></a><span data-ttu-id="c621a-165">종속성 범위 및 컨트롤러 수명</span><span class="sxs-lookup"><span data-stu-id="c621a-165">Dependency Scope and Controller Lifetime</span></span>

<span data-ttu-id="c621a-166">컨트롤러는 요청에 따라 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-166">Controllers are created per request.</span></span> <span data-ttu-id="c621a-167">개체 수명 관리 **IDependencyResolver** 개념을 사용 하는 *범위*합니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-167">To manage object lifetimes, **IDependencyResolver** uses the concept of a *scope*.</span></span>

<span data-ttu-id="c621a-168">종속성 확인자에 연결 합니다 **HttpConfiguration** 개체에 전역 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-168">The dependency resolver attached to the **HttpConfiguration** object has global scope.</span></span> <span data-ttu-id="c621a-169">Web API 컨트롤러를 만들 때 호출한 **BeginScope**합니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-169">When Web API creates a controller, it calls **BeginScope**.</span></span> <span data-ttu-id="c621a-170">이 메서드는 **IDependencyScope** 자식 범위를 나타내는입니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-170">This method returns an **IDependencyScope** that represents a child scope.</span></span>

<span data-ttu-id="c621a-171">웹 API 호출 **GetService** 컨트롤러를 만들려면 자식 범위에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-171">Web API then calls **GetService** on the child scope to create the controller.</span></span> <span data-ttu-id="c621a-172">Web API를 호출 하는 요청이 완료 되 면 **Dispose** 자식 범위에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-172">When request is complete, Web API calls **Dispose** on the child scope.</span></span> <span data-ttu-id="c621a-173">사용 된 **Dispose** 컨트롤러의 종속성을 삭제 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-173">Use the **Dispose** method to dispose of the controller's dependencies.</span></span>

<span data-ttu-id="c621a-174">구현 하는 방법을 **BeginScope** IoC 컨테이너에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-174">How you implement **BeginScope** depends on the IoC container.</span></span> <span data-ttu-id="c621a-175">Unity에 대 한 범위는 자식 컨테이너에 해당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-175">For Unity, scope corresponds to a child container:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample10.cs)]

<span data-ttu-id="c621a-176">대부분의 IoC 컨테이너에 유사한 상응 합니다.</span><span class="sxs-lookup"><span data-stu-id="c621a-176">Most IoC containers have similar equivalents.</span></span>
