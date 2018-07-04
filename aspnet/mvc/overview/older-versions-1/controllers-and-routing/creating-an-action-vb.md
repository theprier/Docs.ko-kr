---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
title: 작업 (VB) 만들기 | Microsoft Docs
author: microsoft
description: ASP.NET MVC 컨트롤러에 새 작업을 추가 하는 방법에 알아봅니다. 작업 메서드에 대 한 요구 사항에 알아봅니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/02/2009
ms.topic: article
ms.assetid: c8d93e11-ef78-4a30-afbc-f30419000a60
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
msc.type: authoredcontent
ms.openlocfilehash: 64bc75eaccdd71ebff59f34a824c9b6c520a27ef
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37367870"
---
<a name="creating-an-action-vb"></a><span data-ttu-id="1ec34-104">작업 (VB) 만들기</span><span class="sxs-lookup"><span data-stu-id="1ec34-104">Creating an Action (VB)</span></span>
====================
<span data-ttu-id="1ec34-105">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="1ec34-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="1ec34-106">ASP.NET MVC 컨트롤러에 새 작업을 추가 하는 방법에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1ec34-106">Learn how to add a new action to an ASP.NET MVC controller.</span></span> <span data-ttu-id="1ec34-107">작업 메서드에 대 한 요구 사항에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1ec34-107">Learn about the requirements for a method to be an action.</span></span>


<span data-ttu-id="1ec34-108">이 자습서의 목표는 새 컨트롤러 작업을 만드는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec34-108">The goal of this tutorial is to explain how you can create a new controller action.</span></span> <span data-ttu-id="1ec34-109">동작 메서드의 요구 사항에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1ec34-109">You learn about the requirements of an action method.</span></span> <span data-ttu-id="1ec34-110">메서드를 작업으로 노출 되지 않도록 방지 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="1ec34-110">You also learn how to prevent a method from being exposed as an action.</span></span>

## <a name="adding-an-action-to-a-controller"></a><span data-ttu-id="1ec34-111">컨트롤러에 작업 추가</span><span class="sxs-lookup"><span data-stu-id="1ec34-111">Adding an Action to a Controller</span></span>

<span data-ttu-id="1ec34-112">컨트롤러에 새 메서드를 추가 하 여 새 작업 컨트롤러에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec34-112">You add a new action to a controller by adding a new method to the controller.</span></span> <span data-ttu-id="1ec34-113">예를 들어 목록 1의 컨트롤러는 index () 라는 작업 및 sayhello () 라는 작업을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec34-113">For example, the controller in Listing 1 contains an action named Index() and an action named SayHello().</span></span> <span data-ttu-id="1ec34-114">두 방법 모두 작업으로 노출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ec34-114">Both methods are exposed as actions.</span></span>

<span data-ttu-id="1ec34-115">**1-Controllers\HomeController.vb 나열**</span><span class="sxs-lookup"><span data-stu-id="1ec34-115">**Listing 1 - Controllers\HomeController.vb**</span></span>

[!code-vb[Main](creating-an-action-vb/samples/sample1.vb)]

<span data-ttu-id="1ec34-116">메서드는 동작으로 universe를 노출 하기 위해 특정 요구 사항을 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec34-116">In order to be exposed to the universe as an action, a method must meet certain requirements:</span></span>

- <span data-ttu-id="1ec34-117">메서드는 public 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec34-117">The method must be public.</span></span>
- <span data-ttu-id="1ec34-118">메서드는 정적 메서드 일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1ec34-118">The method cannot be a static method.</span></span>
- <span data-ttu-id="1ec34-119">메서드는 확장 메서드를 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1ec34-119">The method cannot be an extension method.</span></span>
- <span data-ttu-id="1ec34-120">생성자, getter 또는 setter 메서드 일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1ec34-120">The method cannot be a constructor, getter, or setter.</span></span>
- <span data-ttu-id="1ec34-121">메서드는 개방형 제네릭 형식은 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1ec34-121">The method cannot have open generic types.</span></span>
- <span data-ttu-id="1ec34-122">메서드는 컨트롤러의 기본 클래스의 메서드가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="1ec34-122">The method is not a method of the controller base class.</span></span>
- <span data-ttu-id="1ec34-123">메서드를 포함할 수 없습니다 **ref** 하거나 **out** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="1ec34-123">The method cannot contain **ref** or **out** parameters.</span></span>

<span data-ttu-id="1ec34-124">컨트롤러 동작의 반환 형식에 제한이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec34-124">Notice that there are no restrictions on the return type of a controller action.</span></span> <span data-ttu-id="1ec34-125">컨트롤러 작업을 string, DateTime, void 또는 Random 클래스의 인스턴스를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ec34-125">A controller action can return a string, a DateTime, an instance of the Random class, or void.</span></span> <span data-ttu-id="1ec34-126">ASP.NET MVC 프레임 워크는 작업 결과 문자열에 없는 모든 반환 형식을 변환 되며 브라우저에 문자열을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec34-126">The ASP.NET MVC framework will convert any return type that is not an action result into a string and render the string to the browser.</span></span>

<span data-ttu-id="1ec34-127">컨트롤러에 이러한 요구 사항을 위반 하지 않는 모든 메서드를 추가 하는 경우 메서드는 컨트롤러 작업으로 노출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ec34-127">When you add any method that does not violate these requirements to a controller, the method is exposed as a controller action.</span></span> <span data-ttu-id="1ec34-128">까다로우므로 주의 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec34-128">Be careful here.</span></span> <span data-ttu-id="1ec34-129">컨트롤러 작업을 인터넷에 연결 하는 누구나 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ec34-129">A controller action can be invoked by anyone connected to the Internet.</span></span> <span data-ttu-id="1ec34-130">예를 들어 만들지 DeleteMyWebsite() 컨트롤러 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec34-130">Do not, for example, create a DeleteMyWebsite() controller action.</span></span>

## <a name="preventing-a-public-method-from-being-invoked"></a><span data-ttu-id="1ec34-131">공용 메서드 호출에서 방지</span><span class="sxs-lookup"><span data-stu-id="1ec34-131">Preventing a Public Method from Being Invoked</span></span>

<span data-ttu-id="1ec34-132">컨트롤러 클래스의 public 메서드를 생성 해야 하 고 컨트롤러 작업으로 메서드를 노출 하지 않으려는 경우를 사용 하 여 호출 되는 메서드를 방지할 수 있습니다 합니다 &lt;NonAction&gt; 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="1ec34-132">If you need to create a public method in a controller class and you don't want to expose the method as a controller action then you can prevent the method from being invoked by using the &lt;NonAction&gt; attribute.</span></span> <span data-ttu-id="1ec34-133">목록 2에서 컨트롤러를 사용 하 여 데코 레이트 된 CompanySecrets() 라는 public 메서드를 포함 하는 예를 들어 합니다 &lt;NonAction&gt; 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="1ec34-133">For example, the controller in Listing 2 contains a public method named CompanySecrets() that is decorated with the &lt;NonAction&gt; attribute.</span></span>

<span data-ttu-id="1ec34-134">**Listing 2 - Controllers\WorkController.vb**</span><span class="sxs-lookup"><span data-stu-id="1ec34-134">**Listing 2 - Controllers\WorkController.vb**</span></span>

[!code-vb[Main](creating-an-action-vb/samples/sample2.vb)]

<span data-ttu-id="1ec34-135">/Work/CompanySecrets 브라우저의 주소 표시줄에 입력 하 여 CompanySecrets() 컨트롤러 작업을 호출 하려고 하면 그림 1에서 오류 메시지를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ec34-135">If you attempt to invoke the CompanySecrets() controller action by typing /Work/CompanySecrets into the address bar of your browser then you'll get the error message in Figure 1.</span></span>


<span data-ttu-id="1ec34-136">[![NonAction 메서드 호출](creating-an-action-vb/_static/image1.jpg)](creating-an-action-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="1ec34-136">[![Invoking a NonAction method](creating-an-action-vb/_static/image1.jpg)](creating-an-action-vb/_static/image1.png)</span></span>

<span data-ttu-id="1ec34-137">**그림 01**: NonAction 메서드 호출 ([큰 이미지를 보려면 클릭](creating-an-action-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="1ec34-137">**Figure 01**: Invoking a NonAction method([Click to view full-size image](creating-an-action-vb/_static/image2.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1ec34-138">[이전](creating-a-controller-vb.md)
> [다음](aspnet-mvc-controllers-overview-cs.md)</span><span class="sxs-lookup"><span data-stu-id="1ec34-138">[Previous](creating-a-controller-vb.md)
[Next](aspnet-mvc-controllers-overview-cs.md)</span></span>
