---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
title: 동작 (C#) 만들기 | Microsoft Docs
author: microsoft
description: ASP.NET MVC 컨트롤러에 새 동작을 추가 하는 방법에 알아봅니다. 메서드는 작업에 대 한 요구 사항에 알아봅니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/02/2009
ms.topic: article
ms.assetid: cb33b28c-3025-4bd1-a1fa-eaa3af7bb56f
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
msc.type: authoredcontent
ms.openlocfilehash: 7c6145902db59b07e96a5563b138c1a6323946b2
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="creating-an-action-c"></a><span data-ttu-id="fdf8b-104">만들기 동작 (C#)</span><span class="sxs-lookup"><span data-stu-id="fdf8b-104">Creating an Action (C#)</span></span>
====================
<span data-ttu-id="fdf8b-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="fdf8b-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="fdf8b-106">ASP.NET MVC 컨트롤러에 새 동작을 추가 하는 방법에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="fdf8b-106">Learn how to add a new action to an ASP.NET MVC controller.</span></span> <span data-ttu-id="fdf8b-107">메서드는 작업에 대 한 요구 사항에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="fdf8b-107">Learn about the requirements for a method to be an action.</span></span>


<span data-ttu-id="fdf8b-108">이 자습서의 목표 새 컨트롤러 동작을 만드는 방법을 설명 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fdf8b-108">The goal of this tutorial is to explain how you can create a new controller action.</span></span> <span data-ttu-id="fdf8b-109">동작 메서드의 요구 사항에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="fdf8b-109">You learn about the requirements of an action method.</span></span> <span data-ttu-id="fdf8b-110">메서드는 작업으로 노출 되지 않도록 방지 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="fdf8b-110">You also learn how to prevent a method from being exposed as an action.</span></span>

## <a name="adding-an-action-to-a-controller"></a><span data-ttu-id="fdf8b-111">컨트롤러에 작업 추가</span><span class="sxs-lookup"><span data-stu-id="fdf8b-111">Adding an Action to a Controller</span></span>

<span data-ttu-id="fdf8b-112">컨트롤러에 새 메서드를 추가 하 여 컨트롤러에 새 동작을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdf8b-112">You add a new action to a controller by adding a new method to the controller.</span></span> <span data-ttu-id="fdf8b-113">예를 들어 컨트롤러 목록 1의 index ()는 작업 및 sayhello () 라는 동작을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdf8b-113">For example, the controller in Listing 1 contains an action named Index() and an action named SayHello().</span></span> <span data-ttu-id="fdf8b-114">두 방법 모두 작업으로 노출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fdf8b-114">Both methods are exposed as actions.</span></span>

<span data-ttu-id="fdf8b-115">**1-Controllers\HomeController.cs 나열**</span><span class="sxs-lookup"><span data-stu-id="fdf8b-115">**Listing 1 - Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](creating-an-action-cs/samples/sample1.cs)]

<span data-ttu-id="fdf8b-116">동작으로 universe에 게 노출 메서드는 특정 요구 사항을 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdf8b-116">In order to be exposed to the universe as an action, a method must meet certain requirements:</span></span>

- <span data-ttu-id="fdf8b-117">메서드는 공용 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdf8b-117">The method must be public.</span></span>
- <span data-ttu-id="fdf8b-118">메서드는 정적 메서드 일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fdf8b-118">The method cannot be a static method.</span></span>
- <span data-ttu-id="fdf8b-119">메서드가 확장 메서드 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fdf8b-119">The method cannot be an extension method.</span></span>
- <span data-ttu-id="fdf8b-120">생성자, getter 또는 setter 메서드 일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fdf8b-120">The method cannot be a constructor, getter, or setter.</span></span>
- <span data-ttu-id="fdf8b-121">메서드가 개방형 제네릭 형식은 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fdf8b-121">The method cannot have open generic types.</span></span>
- <span data-ttu-id="fdf8b-122">메서드는 컨트롤러의 기본 클래스의 메서드가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="fdf8b-122">The method is not a method of the controller base class.</span></span>
- <span data-ttu-id="fdf8b-123">메서드를 포함할 수 없습니다 **ref** 또는 **아웃** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="fdf8b-123">The method cannot contain **ref** or **out** parameters.</span></span>

<span data-ttu-id="fdf8b-124">컨트롤러 동작의 반환 형식에 제한이 없음을 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdf8b-124">Notice that there are no restrictions on the return type of a controller action.</span></span> <span data-ttu-id="fdf8b-125">컨트롤러 동작 문자열을 DateTime, void 또는 Random 클래스의 인스턴스를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdf8b-125">A controller action can return a string, a DateTime, an instance of the Random class, or void.</span></span> <span data-ttu-id="fdf8b-126">ASP.NET MVC 프레임 워크는 작업 결과 문자열로 하지 않은 모든 반환 형식을 변환 하 고 브라우저에 문자열을 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fdf8b-126">The ASP.NET MVC framework will convert any return type that is not an action result into a string and render the string to the browser.</span></span>

<span data-ttu-id="fdf8b-127">컨트롤러에 이러한 요구 사항을 위반 하지 않는 모든 메서드를 추가 하면 메서드는 컨트롤러 작업으로 노출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fdf8b-127">When you add any method that does not violate these requirements to a controller, the method is exposed as a controller action.</span></span> <span data-ttu-id="fdf8b-128">주의 여기 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdf8b-128">Be careful here.</span></span> <span data-ttu-id="fdf8b-129">인터넷에 연결 된 모든 사용자가 컨트롤러 작업을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdf8b-129">A controller action can be invoked by anyone connected to the Internet.</span></span> <span data-ttu-id="fdf8b-130">예를 들어 만들지 마십시오 DeleteMyWebsite() 컨트롤러 작업.</span><span class="sxs-lookup"><span data-stu-id="fdf8b-130">Do not, for example, create a DeleteMyWebsite() controller action.</span></span>

## <a name="preventing-a-public-method-from-being-invoked"></a><span data-ttu-id="fdf8b-131">호출 되는 공용 메서드를 방지</span><span class="sxs-lookup"><span data-stu-id="fdf8b-131">Preventing a Public Method from Being Invoked</span></span>

<span data-ttu-id="fdf8b-132">컨트롤러 클래스에는 공용 메서드를 만들어야 하 고 컨트롤러 작업으로 메서드를 노출 하지 않으려는 경우 [NonAction] 특성을 사용 하 여 호출 되지 메서드를 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdf8b-132">If you need to create a public method in a controller class and you don't want to expose the method as a controller action then you can prevent the method from being invoked by using the [NonAction] attribute.</span></span> <span data-ttu-id="fdf8b-133">예를 들어 목록 2에 있는 컨트롤러 [NonAction] 특성으로 데코레이팅되 어 CompanySecrets() 라는 공용 메서드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdf8b-133">For example, the controller in Listing 2 contains a public method named CompanySecrets() that is decorated with the [NonAction] attribute.</span></span>

<span data-ttu-id="fdf8b-134">**Listing 2 - Controllers\WorkController.cs**</span><span class="sxs-lookup"><span data-stu-id="fdf8b-134">**Listing 2 - Controllers\WorkController.cs**</span></span>

[!code-csharp[Main](creating-an-action-cs/samples/sample2.cs)]

<span data-ttu-id="fdf8b-135">/Work/CompanySecrets 브라우저의 주소 표시줄에 입력 하 여 CompanySecrets() 컨트롤러 작업을 호출 하려고 하면 그림 1에 오류 메시지가 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fdf8b-135">If you attempt to invoke the CompanySecrets() controller action by typing /Work/CompanySecrets into the address bar of your browser then you'll get the error message in Figure 1.</span></span>


<span data-ttu-id="fdf8b-136">[![NonAction 메서드 호출](creating-an-action-cs/_static/image1.jpg)](creating-an-action-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="fdf8b-136">[![Invoking a NonAction method](creating-an-action-cs/_static/image1.jpg)](creating-an-action-cs/_static/image1.png)</span></span>

<span data-ttu-id="fdf8b-137">**그림 01**: NonAction 메서드 호출 ([전체 크기 이미지를 보려면 클릭](creating-an-action-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="fdf8b-137">**Figure 01**: Invoking a NonAction method([Click to view full-size image](creating-an-action-cs/_static/image2.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="fdf8b-138">[이전](creating-a-controller-cs.md)
> [다음](asp-net-mvc-routing-overview-vb.md)</span><span class="sxs-lookup"><span data-stu-id="fdf8b-138">[Previous](creating-a-controller-cs.md)
[Next](asp-net-mvc-routing-overview-vb.md)</span></span>
