---
uid: mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-cs
title: 서비스 계층 (C#)를 사용 하 여 유효성 검사 | Microsoft Docs
author: StephenWalther
description: 사용자 유효성 검사 논리는 별도 서비스 계층 및 컨트롤러 작업에서 이동 하는 방법에 알아봅니다. 이 자습서에서는 Stephen walther가 설명 하는 방법을 있습니다...
ms.author: aspnetcontent
ms.date: 03/02/2009
ms.assetid: 4eabc535-b8a1-43f5-bb99-cfeb86db0fca
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-cs
msc.type: authoredcontent
ms.openlocfilehash: b0cea00ae59a15d5472e9cd9d91d86ca65f781e9
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37833713"
---
<a name="validating-with-a-service-layer-c"></a><span data-ttu-id="8a226-104">서비스 계층 (C#)를 사용 하 여 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="8a226-104">Validating with a Service Layer (C#)</span></span>
====================
<span data-ttu-id="8a226-105">[Stephen walther가](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="8a226-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="8a226-106">사용자 유효성 검사 논리는 별도 서비스 계층 및 컨트롤러 작업에서 이동 하는 방법에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-106">Learn how to move your validation logic out of your controller actions and into a separate service layer.</span></span> <span data-ttu-id="8a226-107">이 자습서에서는 Stephen walther가 컨트롤러 계층에서 서비스 계층을 격리 하 여 중요 한 부분의 분리를 선명 하 게 유지할 수 있습니다에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-107">In this tutorial, Stephen Walther explains how you can maintain a sharp separation of concerns by isolating your service layer from your controller layer.</span></span>


<span data-ttu-id="8a226-108">이 자습서의 목표는 ASP.NET MVC 응용 프로그램에서 유효성 검사를 수행 하는 하나의 메서드를 설명 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-108">The goal of this tutorial is to describe one method of performing validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="8a226-109">이 자습서에서는 사용자 유효성 검사 논리에는 컨트롤러를 별도 서비스 계층으로 이동 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-109">In this tutorial, you learn how to move your validation logic out of your controllers and into a separate service layer.</span></span>

## <a name="separating-concerns"></a><span data-ttu-id="8a226-110">문제를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-110">Separating Concerns</span></span>

<span data-ttu-id="8a226-111">ASP.NET MVC 응용 프로그램을 빌드하면 컨트롤러 작업 내에서 데이터베이스 논리를 배치 해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-111">When you build an ASP.NET MVC application, you should not place your database logic inside your controller actions.</span></span> <span data-ttu-id="8a226-112">데이터베이스 및 컨트롤러 논리를 혼합 하면 응용 프로그램 시간이 지남에 따라 유지 관리 하기가 더 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-112">Mixing your database and controller logic makes your application more difficult to maintain over time.</span></span> <span data-ttu-id="8a226-113">별도 저장소 계층의 모든 데이터베이스 논리를 배치 하는 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-113">The recommendation is that you place all of your database logic in a separate repository layer.</span></span>

<span data-ttu-id="8a226-114">예를 들어 목록 1은 ProductRepository 라는 간단한 리포지토리가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-114">For example, Listing 1 contains a simple repository named the ProductRepository.</span></span> <span data-ttu-id="8a226-115">제품 리포지토리에 모든 응용 프로그램에 대 한 데이터 액세스 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-115">The product repository contains all of the data access code for the application.</span></span> <span data-ttu-id="8a226-116">목록에는 제품 리포지토리를 구현 하는 IProductRepository 인터페이스도를 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-116">The listing also includes the IProductRepository interface that the product repository implements.</span></span>

<span data-ttu-id="8a226-117">**1--Models\ProductRepository.cs 나열**</span><span class="sxs-lookup"><span data-stu-id="8a226-117">**Listing 1 -- Models\ProductRepository.cs**</span></span>

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample1.cs)]

<span data-ttu-id="8a226-118">목록 2의 컨트롤러는 해당 index () 및 create () 작업에서 저장소 계층을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-118">The controller in Listing 2 uses the repository layer in both its Index() and Create() actions.</span></span> <span data-ttu-id="8a226-119">이 컨트롤러 데이터베이스 논리를 포함 하지 않습니다 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-119">Notice that this controller does not contain any database logic.</span></span> <span data-ttu-id="8a226-120">저장소 계층을 만드는 문제를 깔끔하게 분리를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-120">Creating a repository layer enables you to maintain a clean separation of concerns.</span></span> <span data-ttu-id="8a226-121">컨트롤러는 응용 프로그램 흐름 제어 논리를 담당 하 고 리포지토리는 데이터 액세스 논리를 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-121">Controllers are responsible for application flow control logic and the repository is responsible for data access logic.</span></span>

<span data-ttu-id="8a226-122">**2-Controllers\ProductController.cs 나열**</span><span class="sxs-lookup"><span data-stu-id="8a226-122">**Listing 2 - Controllers\ProductController.cs**</span></span>

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample2.cs)]

## <a name="creating-a-service-layer"></a><span data-ttu-id="8a226-123">서비스 레이어 만들기</span><span class="sxs-lookup"><span data-stu-id="8a226-123">Creating a Service Layer</span></span>

<span data-ttu-id="8a226-124">따라서 응용 프로그램 흐름 제어 논리는 컨트롤러에 속해 및 데이터 액세스 논리 저장소에 속해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-124">So, application flow control logic belongs in a controller and data access logic belongs in a repository.</span></span> <span data-ttu-id="8a226-125">이런 경우 여기서 배치 하나요 사용자 유효성 검사 논리?</span><span class="sxs-lookup"><span data-stu-id="8a226-125">In that case, where do you put your validation logic?</span></span> <span data-ttu-id="8a226-126">첫 번째 방법은 사용자 유효성 검사 논리에 배치 하는 *서비스 계층*합니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-126">One option is to place your validation logic in a *service layer*.</span></span>

<span data-ttu-id="8a226-127">서비스 계층은 리포지토리 계층과 컨트롤러 간의 통신을 중재 하는 ASP.NET MVC 응용 프로그램에서 레이어를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-127">A service layer is an additional layer in an ASP.NET MVC application that mediates communication between a controller and repository layer.</span></span> <span data-ttu-id="8a226-128">서비스 계층에는 비즈니스 논리가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-128">The service layer contains business logic.</span></span> <span data-ttu-id="8a226-129">특히 유효성 검사 논리를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-129">In particular, it contains validation logic.</span></span>

<span data-ttu-id="8a226-130">예를 들어 목록 3의 제품 서비스 계층은 CreateProduct() 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-130">For example, the product service layer in Listing 3 has a CreateProduct() method.</span></span> <span data-ttu-id="8a226-131">CreateProduct() 메서드는 새 제품을 제품 리포지토리에 제품을 전달 하기 전에 유효성을 검사 하려면 ValidateProduct() 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-131">The CreateProduct() method calls the ValidateProduct() method to validate a new product before passing the product to the product repository.</span></span>

<span data-ttu-id="8a226-132">**3-Models\ProductService.cs 나열**</span><span class="sxs-lookup"><span data-stu-id="8a226-132">**Listing 3 - Models\ProductService.cs**</span></span>

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample3.cs)]

<span data-ttu-id="8a226-133">제품 컨트롤러 목록 4 리포지토리 계층 대신 서비스 계층을 사용 하도록 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-133">The Product controller has been updated in Listing 4 to use the service layer instead of the repository layer.</span></span> <span data-ttu-id="8a226-134">컨트롤러 계층은 서비스 계층에 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-134">The controller layer talks to the service layer.</span></span> <span data-ttu-id="8a226-135">서비스 계층은 리포지토리 계층에 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-135">The service layer talks to the repository layer.</span></span> <span data-ttu-id="8a226-136">각 계층에는 별도 책임을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-136">Each layer has a separate responsibility.</span></span>

<span data-ttu-id="8a226-137">**4-Controllers\ProductController.cs 나열**</span><span class="sxs-lookup"><span data-stu-id="8a226-137">**Listing 4 - Controllers\ProductController.cs**</span></span>

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample4.cs)]

<span data-ttu-id="8a226-138">제품 서비스 제품 컨트롤러 생성자에서 만들어졌는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-138">Notice that the product service is created in the product controller constructor.</span></span> <span data-ttu-id="8a226-139">제품 서비스를 만들면 모델 상태 사전에서 서비스에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-139">When the product service is created, the model state dictionary is passed to the service.</span></span> <span data-ttu-id="8a226-140">제품 서비스 모델 상태를 사용 하 여 컨트롤러에 다시 유효성 검사 오류 메시지를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-140">The product service uses model state to pass validation error messages back to the controller.</span></span>

## <a name="decoupling-the-service-layer"></a><span data-ttu-id="8a226-141">서비스 계층을 분리</span><span class="sxs-lookup"><span data-stu-id="8a226-141">Decoupling the Service Layer</span></span>

<span data-ttu-id="8a226-142">에서는 컨트롤러와 한 서비스 계층을 격리 하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-142">We have failed to isolate the controller and service layers in one respect.</span></span> <span data-ttu-id="8a226-143">컨트롤러 및 서비스 계층에는 모델 상태를 통해 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-143">The controller and service layers communicate through model state.</span></span> <span data-ttu-id="8a226-144">즉, 서비스 계층 ASP.NET MVC 프레임 워크의 특정 기능에서 종속성을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-144">In other words, the service layer has a dependency on a particular feature of the ASP.NET MVC framework.</span></span>

<span data-ttu-id="8a226-145">가능한 한이 컨트롤러 계층에서 서비스 계층을 격리 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-145">We want to isolate the service layer from our controller layer as much as possible.</span></span> <span data-ttu-id="8a226-146">이론적으로 응용 프로그램 및 ASP.NET MVC 응용 프로그램 뿐만 아니라 모든 유형의 사용 하 여 서비스 계층을 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-146">In theory, we should be able to use the service layer with any type of application and not only an ASP.NET MVC application.</span></span> <span data-ttu-id="8a226-147">예를 들어, 앞으로 것이 좋습니다는 WPF 응용 프로그램에 대 한 프런트 엔드를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-147">For example, in the future, we might want to build a WPF front-end for our application.</span></span> <span data-ttu-id="8a226-148">이 서비스 계층에서 ASP.NET MVC에 대 한 종속성을 제거 하는 방법을 모델 상태를 찾을 해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-148">We should find a way to remove the dependency on ASP.NET MVC model state from our service layer.</span></span>

<span data-ttu-id="8a226-149">목록 5에서이 서비스 계층 모델 상태가 더 이상 사용할 수 있도록 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-149">In Listing 5, the service layer has been updated so that it no longer uses model state.</span></span> <span data-ttu-id="8a226-150">대신 IValidationDictionary 인터페이스를 구현 하는 클래스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-150">Instead, it uses any class that implements the IValidationDictionary interface.</span></span>

<span data-ttu-id="8a226-151">**5-Models\ProductService.cs (분리)를 나열 합니다.**</span><span class="sxs-lookup"><span data-stu-id="8a226-151">**Listing 5 - Models\ProductService.cs (decoupled)**</span></span>

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample5.cs)]

<span data-ttu-id="8a226-152">IValidationDictionary 인터페이스 목록 6에서 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-152">The IValidationDictionary interface is defined in Listing 6.</span></span> <span data-ttu-id="8a226-153">이 간단한 인터페이스는 단일 메서드와 단일 속성에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-153">This simple interface has a single method and a single property.</span></span>

<span data-ttu-id="8a226-154">**6-Models\IValidationDictionary.cs 나열**</span><span class="sxs-lookup"><span data-stu-id="8a226-154">**Listing 6 - Models\IValidationDictionary.cs**</span></span>

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample6.cs)]

<span data-ttu-id="8a226-155">나열 7에서는 ModelStateWrapper 클래스 라는 클래스 IValidationDictionary 인터페이스를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-155">The class in Listing 7, named the ModelStateWrapper class, implements the IValidationDictionary interface.</span></span> <span data-ttu-id="8a226-156">모델 상태 사전을 생성자에 전달 하 여 ModelStateWrapper 클래스를 인스턴스화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-156">You can instantiate the ModelStateWrapper class by passing a model state dictionary to the constructor.</span></span>

<span data-ttu-id="8a226-157">**7-Models\ModelStateWrapper.cs 나열**</span><span class="sxs-lookup"><span data-stu-id="8a226-157">**Listing 7 - Models\ModelStateWrapper.cs**</span></span>

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample7.cs)]

<span data-ttu-id="8a226-158">마지막으로 목록 8에서 업데이트 된 컨트롤러는 해당 생성자에서 서비스 계층을 만들면는 ModelStateWrapper를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-158">Finally, the updated controller in Listing 8 uses the ModelStateWrapper when creating the service layer in its constructor.</span></span>

<span data-ttu-id="8a226-159">**8-Controllers\ProductController.cs 나열**</span><span class="sxs-lookup"><span data-stu-id="8a226-159">**Listing 8 - Controllers\ProductController.cs**</span></span>

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample8.cs)]

<span data-ttu-id="8a226-160">IValidationDictionary 인터페이스 및 ModelStateWrapper 클래스 사용을 완전히 우리의 컨트롤러 계층에서이 서비스 계층을 분리할.</span><span class="sxs-lookup"><span data-stu-id="8a226-160">Using the IValidationDictionary interface and the ModelStateWrapper class enables us to completely isolate our service layer from our controller layer.</span></span> <span data-ttu-id="8a226-161">서비스 계층은 더 이상 모델 상태에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-161">The service layer is no longer dependent on model state.</span></span> <span data-ttu-id="8a226-162">서비스 계층에 IValidationDictionary 인터페이스를 구현 하는 클래스를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-162">You can pass any class that implements the IValidationDictionary interface to the service layer.</span></span> <span data-ttu-id="8a226-163">예를 들어 WPF 응용 프로그램을 간단한 컬렉션 클래스를 사용 하 여 IValidationDictionary 인터페이스를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-163">For example, a WPF application might implement the IValidationDictionary interface with a simple collection class.</span></span>

## <a name="summary"></a><span data-ttu-id="8a226-164">요약</span><span class="sxs-lookup"><span data-stu-id="8a226-164">Summary</span></span>

<span data-ttu-id="8a226-165">이 자습서의 목표는 ASP.NET MVC 응용 프로그램에서 유효성 검사를 수행 하는 한 가지 방법은 설명 하는 것 이었습니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-165">The goal of this tutorial was to discuss one approach to performing validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="8a226-166">이 자습서에서는 모든 유효성 검사 논리에 컨트롤러 및 별도 서비스 계층으로 이동 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-166">In this tutorial, you learned how to move all of your validation logic out of your controllers and into a separate service layer.</span></span> <span data-ttu-id="8a226-167">또한 ModelStateWrapper 클래스를 만들어 컨트롤러 계층에서 서비스 계층을 격리 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="8a226-167">You also learned how to isolate your service layer from your controller layer by creating a ModelStateWrapper class.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8a226-168">[이전](validating-with-the-idataerrorinfo-interface-cs.md)
> [다음](validation-with-the-data-annotation-validators-cs.md)</span><span class="sxs-lookup"><span data-stu-id="8a226-168">[Previous](validating-with-the-idataerrorinfo-interface-cs.md)
[Next](validation-with-the-data-annotation-validators-cs.md)</span></span>
