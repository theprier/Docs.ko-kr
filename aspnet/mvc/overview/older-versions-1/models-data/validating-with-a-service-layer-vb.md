---
uid: mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-vb
title: 서비스 계층 (VB)으로 유효성 검사 | Microsoft Docs
author: StephenWalther
description: 사용자 유효성 검사 논리에서 컨트롤러 작업 및 별도 서비스 계층으로 이동 하는 방법에 알아봅니다. 이 자습서에서는 Stephen Walther 설명 방법을 있습니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/02/2009
ms.topic: article
ms.assetid: 344bb38e-4965-4c47-bda1-f6d29ae5b83a
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-vb
msc.type: authoredcontent
ms.openlocfilehash: bb1191b663f863bf881def620efab4f2f03edc56
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30868245"
---
<a name="validating-with-a-service-layer-vb"></a><span data-ttu-id="4e5ca-104">서비스 계층 (VB)으로 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="4e5ca-104">Validating with a Service Layer (VB)</span></span>
====================
<span data-ttu-id="4e5ca-105">으로 [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="4e5ca-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="4e5ca-106">사용자 유효성 검사 논리에서 컨트롤러 작업 및 별도 서비스 계층으로 이동 하는 방법에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-106">Learn how to move your validation logic out of your controller actions and into a separate service layer.</span></span> <span data-ttu-id="4e5ca-107">이 자습서에서는 Stephen Walther 컨트롤러 계층에서 사용자 서비스 계층을 격리 하 여 문제의 날카로운 분리 유지할 수 있습니다에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-107">In this tutorial, Stephen Walther explains how you can maintain a sharp separation of concerns by isolating your service layer from your controller layer.</span></span>


<span data-ttu-id="4e5ca-108">이 자습서의 목표는 ASP.NET MVC 응용 프로그램에 유효성 검사를 수행 하는 한 가지 방법은 설명 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-108">The goal of this tutorial is to describe one method of performing validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="4e5ca-109">이 자습서에서는 사용자 유효성 검사 논리에 컨트롤러와 별도 서비스 계층으로 이동 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-109">In this tutorial, you learn how to move your validation logic out of your controllers and into a separate service layer.</span></span>

## <a name="separating-concerns"></a><span data-ttu-id="4e5ca-110">문제를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-110">Separating Concerns</span></span>

<span data-ttu-id="4e5ca-111">ASP.NET MVC 응용 프로그램을 빌드할 때에 컨트롤러 작업 내 하지 데이터베이스 논리를 배치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-111">When you build an ASP.NET MVC application, you should not place your database logic inside your controller actions.</span></span> <span data-ttu-id="4e5ca-112">데이터베이스와 컨트롤러 논리를 혼합 하면 응용 프로그램 시간이 지날수록 관리 하기가 더 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-112">Mixing your database and controller logic makes your application more difficult to maintain over time.</span></span> <span data-ttu-id="4e5ca-113">별도 저장소 계층에 모든 데이터베이스 논리를 배치 하는 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-113">The recommendation is that you place all of your database logic in a separate repository layer.</span></span>

<span data-ttu-id="4e5ca-114">예를 들어 목록 1의 ProductRepository 라는 간단한 리포지토리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-114">For example, Listing 1 contains a simple repository named the ProductRepository.</span></span> <span data-ttu-id="4e5ca-115">제품 저장소는 모든 응용 프로그램에 대 한 데이터 액세스 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-115">The product repository contains all of the data access code for the application.</span></span> <span data-ttu-id="4e5ca-116">목록에는 제품 저장소 구현 하는 IProductRepository 인터페이스 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-116">The listing also includes the IProductRepository interface that the product repository implements.</span></span>

<span data-ttu-id="4e5ca-117">**Listing 1 - Models\ProductRepository.vb**</span><span class="sxs-lookup"><span data-stu-id="4e5ca-117">**Listing 1 - Models\ProductRepository.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample1.vb)]

<span data-ttu-id="4e5ca-118">목록 2에서 컨트롤러의 index () 및 create () 작업의 저장소 계층을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-118">The controller in Listing 2 uses the repository layer in both its Index() and Create() actions.</span></span> <span data-ttu-id="4e5ca-119">이 컨트롤러에는 데이터베이스 논리 없는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-119">Notice that this controller does not contain any database logic.</span></span> <span data-ttu-id="4e5ca-120">저장소 계층을 만드는 문제의 확실 하 게 구분을 유지 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-120">Creating a repository layer enables you to maintain a clean separation of concerns.</span></span> <span data-ttu-id="4e5ca-121">컨트롤러 응용 프로그램 흐름 제어 논리를 담당 하 고 저장소는 데이터 액세스 논리를 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-121">Controllers are responsible for application flow control logic and the repository is responsible for data access logic.</span></span>

<span data-ttu-id="4e5ca-122">**Listing 2 - Controllers\ProductController.vb**</span><span class="sxs-lookup"><span data-stu-id="4e5ca-122">**Listing 2 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample2.vb)]

## <a name="creating-a-service-layer"></a><span data-ttu-id="4e5ca-123">서비스 계층을 만들려면</span><span class="sxs-lookup"><span data-stu-id="4e5ca-123">Creating a Service Layer</span></span>

<span data-ttu-id="4e5ca-124">따라서 응용 프로그램 흐름 제어 논리는 컨트롤러에 속하며 저장소에서 데이터 액세스 논리 속하는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-124">So, application flow control logic belongs in a controller and data access logic belongs in a repository.</span></span> <span data-ttu-id="4e5ca-125">이 경우 않습니다를 배치할 유효성 검사 논리?</span><span class="sxs-lookup"><span data-stu-id="4e5ca-125">In that case, where do you put your validation logic?</span></span> <span data-ttu-id="4e5ca-126">첫 번째 방법은 유효성 검사 논리에 배치 하는 *서비스 계층*합니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-126">One option is to place your validation logic in a *service layer*.</span></span>

<span data-ttu-id="4e5ca-127">서비스 계층은 컨트롤러와 저장소 계층 간의 통신을 중재 하는 ASP.NET MVC 응용 프로그램에 있는 추가 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-127">A service layer is an additional layer in an ASP.NET MVC application that mediates communication between a controller and repository layer.</span></span> <span data-ttu-id="4e5ca-128">서비스 계층에는 비즈니스 논리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-128">The service layer contains business logic.</span></span> <span data-ttu-id="4e5ca-129">특히, 유효성 검사 논리를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-129">In particular, it contains validation logic.</span></span>

<span data-ttu-id="4e5ca-130">예를 들어 보기 3의 제품 서비스 계층에 CreateProduct() 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-130">For example, the product service layer in Listing 3 has a CreateProduct() method.</span></span> <span data-ttu-id="4e5ca-131">CreateProduct() 메서드는 새 제품을 제품 저장소에 제품을 전달 하기 전에 유효성을 검사 하려면 ValidateProduct() 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-131">The CreateProduct() method calls the ValidateProduct() method to validate a new product before passing the product to the product repository.</span></span>

<span data-ttu-id="4e5ca-132">**Listing 3 - Models\ProductService.vb**</span><span class="sxs-lookup"><span data-stu-id="4e5ca-132">**Listing 3 - Models\ProductService.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample3.vb)]

<span data-ttu-id="4e5ca-133">저장소 계층 대신 서비스 계층을 사용 하도록 목록 4에는 제품 컨트롤러 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-133">The Product controller has been updated in Listing 4 to use the service layer instead of the repository layer.</span></span> <span data-ttu-id="4e5ca-134">컨트롤러 계층의 서비스 계층으로 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-134">The controller layer talks to the service layer.</span></span> <span data-ttu-id="4e5ca-135">서비스 계층은 저장소 계층을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-135">The service layer talks to the repository layer.</span></span> <span data-ttu-id="4e5ca-136">각 레이어에 별도 책임입니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-136">Each layer has a separate responsibility.</span></span>

<span data-ttu-id="4e5ca-137">**Listing 4 - Controllers\ProductController.vb**</span><span class="sxs-lookup"><span data-stu-id="4e5ca-137">**Listing 4 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample4.vb)]

<span data-ttu-id="4e5ca-138">제품 서비스 제품 컨트롤러 생성자에서 만들어졌는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-138">Notice that the product service is created in the product controller constructor.</span></span> <span data-ttu-id="4e5ca-139">제품 서비스를 만들면 모델 상태 사전에서 서비스에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-139">When the product service is created, the model state dictionary is passed to the service.</span></span> <span data-ttu-id="4e5ca-140">제품 서비스 모델 상태를 사용 하 여 컨트롤러에 다시 유효성 검사 오류 메시지를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-140">The product service uses model state to pass validation error messages back to the controller.</span></span>

## <a name="decoupling-the-service-layer"></a><span data-ttu-id="4e5ca-141">서비스 계층을 분리</span><span class="sxs-lookup"><span data-stu-id="4e5ca-141">Decoupling the Service Layer</span></span>

<span data-ttu-id="4e5ca-142">우리는 컨트롤러 및 서비스 계층 한 격리 하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-142">We have failed to isolate the controller and service layers in one respect.</span></span> <span data-ttu-id="4e5ca-143">컨트롤러 및 서비스 계층에는 모델 상태를 통해 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-143">The controller and service layers communicate through model state.</span></span> <span data-ttu-id="4e5ca-144">즉, 서비스 계층 ASP.NET MVC 프레임 워크의 특정 기능에 종속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-144">In other words, the service layer has a dependency on a particular feature of the ASP.NET MVC framework.</span></span>

<span data-ttu-id="4e5ca-145">가능한 한 우리의 컨트롤러 레이어에서 서비스 계층을 분리 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-145">We want to isolate the service layer from our controller layer as much as possible.</span></span> <span data-ttu-id="4e5ca-146">이론적으로 모든 종류의 응용 프로그램 및 ASP.NET MVC 응용 프로그램 뿐만 아니라 서비스 계층을 사용할 수 했습니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-146">In theory, we should be able to use the service layer with any type of application and not only an ASP.NET MVC application.</span></span> <span data-ttu-id="4e5ca-147">예를 들어 나중에 수 하려고는 WPF 응용 프로그램에 대 한 프런트 엔드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-147">For example, in the future, we might want to build a WPF front-end for our application.</span></span> <span data-ttu-id="4e5ca-148">이 서비스 계층에서 ASP.NET MVC에 대 한 종속성을 제거 하는 방법을 모델 상태를 찾을 해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-148">We should find a way to remove the dependency on ASP.NET MVC model state from our service layer.</span></span>

<span data-ttu-id="4e5ca-149">목록 5에서이 서비스 계층에 모델 상태를 더 이상 사용 하도록 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-149">In Listing 5, the service layer has been updated so that it no longer uses model state.</span></span> <span data-ttu-id="4e5ca-150">대신, IValidationDictionary 인터페이스를 구현 하는 모든 클래스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-150">Instead, it uses any class that implements the IValidationDictionary interface.</span></span>

<span data-ttu-id="4e5ca-151">**5-Models\ProductService.vb (분리) 목록**</span><span class="sxs-lookup"><span data-stu-id="4e5ca-151">**Listing 5 - Models\ProductService.vb (decoupled)**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample5.vb)]

<span data-ttu-id="4e5ca-152">IValidationDictionary 인터페이스 목록 6에서 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-152">The IValidationDictionary interface is defined in Listing 6.</span></span> <span data-ttu-id="4e5ca-153">이 간단한 인터페이스에는 단일 메서드 및 단일 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-153">This simple interface has a single method and a single property.</span></span>

<span data-ttu-id="4e5ca-154">**6-Models\IValidationDictionary.cs 나열**</span><span class="sxs-lookup"><span data-stu-id="4e5ca-154">**Listing 6 - Models\IValidationDictionary.cs**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample6.vb)]

<span data-ttu-id="4e5ca-155">ModelStateWrapper 클래스의 이름을 나열 하는 7: 클래스 IValidationDictionary 인터페이스를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-155">The class in Listing 7, named the ModelStateWrapper class, implements the IValidationDictionary interface.</span></span> <span data-ttu-id="4e5ca-156">모델 상태 사전 생성자에 전달 하 여 ModelStateWrapper 클래스를 인스턴스화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-156">You can instantiate the ModelStateWrapper class by passing a model state dictionary to the constructor.</span></span>

<span data-ttu-id="4e5ca-157">**Listing 7 - Models\ModelStateWrapper.vb**</span><span class="sxs-lookup"><span data-stu-id="4e5ca-157">**Listing 7 - Models\ModelStateWrapper.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample7.vb)]

<span data-ttu-id="4e5ca-158">마지막으로, 목록 8의 업데이트 된 컨트롤러는 해당 생성자에서 서비스 계층을 만들 때는 ModelStateWrapper를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-158">Finally, the updated controller in Listing 8 uses the ModelStateWrapper when creating the service layer in its constructor.</span></span>

<span data-ttu-id="4e5ca-159">**Listing 8 - Controllers\ProductController.vb**</span><span class="sxs-lookup"><span data-stu-id="4e5ca-159">**Listing 8 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample8.vb)]

<span data-ttu-id="4e5ca-160">IValidationDictionary를 사용 하 여 인터페이스와 ModelStateWrapper 클래스 수 있습니다 완전히 우리의 컨트롤러 계층에서이 서비스 계층을 격리.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-160">Using the IValidationDictionary interface and the ModelStateWrapper class enables us to completely isolate our service layer from our controller layer.</span></span> <span data-ttu-id="4e5ca-161">서비스 계층은 더 이상 모델 상태에 의존 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-161">The service layer is no longer dependent on model state.</span></span> <span data-ttu-id="4e5ca-162">서비스 계층 IValidationDictionary 인터페이스를 구현 하는 모든 클래스를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-162">You can pass any class that implements the IValidationDictionary interface to the service layer.</span></span> <span data-ttu-id="4e5ca-163">예를 들어 WPF 응용 프로그램 단순 컬렉션 클래스와 IValidationDictionary 인터페이스를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-163">For example, a WPF application might implement the IValidationDictionary interface with a simple collection class.</span></span>

## <a name="summary"></a><span data-ttu-id="4e5ca-164">요약</span><span class="sxs-lookup"><span data-stu-id="4e5ca-164">Summary</span></span>

<span data-ttu-id="4e5ca-165">이 자습서의 목표 ASP.NET MVC 응용 프로그램에서 유효성 검사를 수행 하는 한 가지 방법을 설명 하는 것 이었습니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-165">The goal of this tutorial was to discuss one approach to performing validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="4e5ca-166">이 자습서에서는 모든 유효성 검사 논리에 컨트롤러와 별도 서비스 계층으로 이동 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-166">In this tutorial, you learned how to move all of your validation logic out of your controllers and into a separate service layer.</span></span> <span data-ttu-id="4e5ca-167">또한 ModelStateWrapper 클래스를 만들어 컨트롤러 계층에서 사용자 서비스 계층을 격리 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="4e5ca-167">You also learned how to isolate your service layer from your controller layer by creating a ModelStateWrapper class.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4e5ca-168">[이전](validating-with-the-idataerrorinfo-interface-vb.md)
> [다음](validation-with-the-data-annotation-validators-vb.md)</span><span class="sxs-lookup"><span data-stu-id="4e5ca-168">[Previous](validating-with-the-idataerrorinfo-interface-vb.md)
[Next](validation-with-the-data-annotation-validators-vb.md)</span></span>
