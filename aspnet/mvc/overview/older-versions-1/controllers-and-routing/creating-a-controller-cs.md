---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-cs
title: 컨트롤러 (C#) 만들기 | Microsoft Docs
author: StephenWalther
description: 이 자습서에서는 Stephen walther가 ASP.NET MVC 응용 프로그램에 컨트롤러를 추가할 수는 방법을 보여 줍니다.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 719d50d4-2305-454c-98b4-bae64937c48f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-cs
msc.type: authoredcontent
ms.openlocfilehash: 6fe880775a5d477aefcf0fe6cedb3e719760ed90
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41835550"
---
<a name="creating-a-controller-c"></a><span data-ttu-id="74bd5-103">컨트롤러 (C#) 만들기</span><span class="sxs-lookup"><span data-stu-id="74bd5-103">Creating a Controller (C#)</span></span>
====================
<span data-ttu-id="74bd5-104">[Stephen walther가](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="74bd5-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="74bd5-105">이 자습서에서는 Stephen walther가 ASP.NET MVC 응용 프로그램에 컨트롤러를 추가할 수는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="74bd5-105">In this tutorial, Stephen Walther demonstrates how you can add a controller to an ASP.NET MVC application.</span></span>


<span data-ttu-id="74bd5-106">이 자습서의 목표는 새 ASP.NET MVC 컨트롤러 만들 수는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="74bd5-106">The goal of this tutorial is to explain how you can create new ASP.NET MVC controllers.</span></span> <span data-ttu-id="74bd5-107">클래스 파일을 직접 만들어 및 Visual Studio 추가 컨트롤러 메뉴 옵션을 사용 하 여 컨트롤러를 만드는 방법에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="74bd5-107">You learn how to create controllers both by using the Visual Studio Add Controller menu option and by creating a class file by hand.</span></span>

### <a name="using-the-add-controller-menu-option"></a><span data-ttu-id="74bd5-108">사용 하 여 컨트롤러 메뉴 옵션 추가</span><span class="sxs-lookup"><span data-stu-id="74bd5-108">Using the Add Controller Menu Option</span></span>

<span data-ttu-id="74bd5-109">새 컨트롤러를 만드는 가장 쉬운 방법은 Visual Studio 솔루션 탐색기 창에서 컨트롤러 폴더를 마우스 오른쪽 단추로 클릭 하 고 선택 하는 것은 **추가, 컨트롤러** 메뉴 옵션 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="74bd5-109">The easiest way to create a new controller is to right-click the Controllers folder in the Visual Studio Solution Explorer window and select the **Add, Controller** menu option (see Figure 1).</span></span> <span data-ttu-id="74bd5-110">이 메뉴 옵션을 선택 하면 열립니다는 **컨트롤러 추가** 대화 상자 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="74bd5-110">Selecting this menu option opens the **Add Controller** dialog (see Figure 2).</span></span>


<span data-ttu-id="74bd5-111">[![새 프로젝트 대화 상자](creating-a-controller-cs/_static/image1.jpg)](creating-a-controller-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="74bd5-111">[![The New Project dialog box](creating-a-controller-cs/_static/image1.jpg)](creating-a-controller-cs/_static/image1.png)</span></span>

<span data-ttu-id="74bd5-112">**그림 01**: 새 컨트롤러 추가 ([큰 이미지를 보려면 클릭](creating-a-controller-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="74bd5-112">**Figure 01**: Adding a new controller([Click to view full-size image](creating-a-controller-cs/_static/image2.png))</span></span>


<span data-ttu-id="74bd5-113">[![새 프로젝트 대화 상자](creating-a-controller-cs/_static/image2.jpg)](creating-a-controller-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="74bd5-113">[![The New Project dialog box](creating-a-controller-cs/_static/image2.jpg)](creating-a-controller-cs/_static/image3.png)</span></span>

<span data-ttu-id="74bd5-114">**그림 02**: 컨트롤러 추가 대화 상자 ([큰 이미지를 보려면 클릭](creating-a-controller-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="74bd5-114">**Figure 02**: The Add Controller dialog ([Click to view full-size image](creating-a-controller-cs/_static/image4.png))</span></span>


<span data-ttu-id="74bd5-115">첫 번째 부분에서 컨트롤러 이름 강조 표시 하는 **컨트롤러 추가** 대화 합니다.</span><span class="sxs-lookup"><span data-stu-id="74bd5-115">Notice that the first part of the controller name is highlighted in the **Add Controller** dialog.</span></span> <span data-ttu-id="74bd5-116">모든 컨트롤러 이름을 접미사로 끝나야 *컨트롤러*합니다.</span><span class="sxs-lookup"><span data-stu-id="74bd5-116">Every controller name must end with the suffix *Controller*.</span></span> <span data-ttu-id="74bd5-117">예를 들어 라는 컨트롤러를 만들 수 있습니다 *ProductController* 있지만 라는 컨트롤러가 아닌 *제품*합니다.</span><span class="sxs-lookup"><span data-stu-id="74bd5-117">For example, you can create a controller named *ProductController* but not a controller named *Product*.</span></span>


<span data-ttu-id="74bd5-118">누락 된 컨트롤러를 만드는 경우 합니다 *컨트롤러* 접미사 컨트롤러를 호출할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="74bd5-118">If you create a controller that is missing the *Controller* suffix then you won't be able to invoke the controller.</span></span> <span data-ttu-id="74bd5-119">실행 하지 마십시오.--이 실수 후 위해 시간 필자의 인생을 불필요 하 게 했습니다.</span><span class="sxs-lookup"><span data-stu-id="74bd5-119">Don't do this -- I've wasted countless hours of my life after making this mistake.</span></span>


<span data-ttu-id="74bd5-120">**1-Controllers\ProductController.cs 나열**</span><span class="sxs-lookup"><span data-stu-id="74bd5-120">**Listing 1 - Controllers\ProductController.cs**</span></span>

[!code-csharp[Main](creating-a-controller-cs/samples/sample1.cs)]

<span data-ttu-id="74bd5-121">항상 Controllers 폴더에서 컨트롤러를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74bd5-121">You should always create controllers in the Controllers folder.</span></span> <span data-ttu-id="74bd5-122">이 고, 그렇지 ASP.NET MVC의 규칙 위반 수 및 다른 개발자가 좀 더 어려울 응용 프로그램을 이해 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74bd5-122">Otherwise, you'll be violating the conventions of ASP.NET MVC and other developers will have a more difficult time understanding your application.</span></span>

### <a name="scaffolding-action-methods"></a><span data-ttu-id="74bd5-123">스 캐 폴딩 작업 메서드</span><span class="sxs-lookup"><span data-stu-id="74bd5-123">Scaffolding Action Methods</span></span>

<span data-ttu-id="74bd5-124">만들기, 업데이트 및 정보 작업 메서드를 자동으로 생성 하는 옵션이 있는 컨트롤러를 만들 때 (그림 3 참조).</span><span class="sxs-lookup"><span data-stu-id="74bd5-124">When you create a controller, you have the option to generate Create, Update, and Details action methods automatically (see Figure 3).</span></span> <span data-ttu-id="74bd5-125">이 옵션을 선택 하는 경우에 목록 2의 컨트롤러 클래스가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="74bd5-125">If you select this option then the controller class in Listing 2 is generated.</span></span>


<span data-ttu-id="74bd5-126">[![작업 메서드를 자동으로 만들기](creating-a-controller-cs/_static/image3.jpg)](creating-a-controller-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="74bd5-126">[![Creating action methods automatically](creating-a-controller-cs/_static/image3.jpg)](creating-a-controller-cs/_static/image5.png)</span></span>

<span data-ttu-id="74bd5-127">**그림 03**: 작업 메서드를 자동으로 만들기 ([큰 이미지를 보려면 클릭](creating-a-controller-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="74bd5-127">**Figure 03**: Creating action methods automatically ([Click to view full-size image](creating-a-controller-cs/_static/image6.png))</span></span>


<span data-ttu-id="74bd5-128">**2-Controllers\CustomerController.cs 나열**</span><span class="sxs-lookup"><span data-stu-id="74bd5-128">**Listing 2 - Controllers\CustomerController.cs**</span></span>

[!code-csharp[Main](creating-a-controller-cs/samples/sample2.cs)]

<span data-ttu-id="74bd5-129">생성 된 이러한 메서드는 스텁 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="74bd5-129">These generated methods are stub methods.</span></span> <span data-ttu-id="74bd5-130">만들기, 업데이트 및 직접 고객에 대 한 세부 정보를 표시 하는 실제 논리를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74bd5-130">You must add the actual logic for creating, updating, and showing details for a customer yourself.</span></span> <span data-ttu-id="74bd5-131">그러나 스텁 메서드 유용한 시작점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="74bd5-131">But, the stub methods provide you with a nice starting point.</span></span>

### <a name="creating-a-controller-class"></a><span data-ttu-id="74bd5-132">컨트롤러 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="74bd5-132">Creating a Controller Class</span></span>

<span data-ttu-id="74bd5-133">ASP.NET MVC 컨트롤러가 클래스 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="74bd5-133">The ASP.NET MVC controller is just a class.</span></span> <span data-ttu-id="74bd5-134">원한다 면를 편리 하 게 Visual Studio 컨트롤러 스 캐 폴딩을 무시 하 고 컨트롤러 클래스를 직접 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74bd5-134">If you prefer, you can ignore the convenient Visual Studio controller scaffolding and create a controller class by hand.</span></span> <span data-ttu-id="74bd5-135">아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="74bd5-135">Follow these steps:</span></span>

1. <span data-ttu-id="74bd5-136">컨트롤러 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **추가, 새 항목** 선택 합니다 **클래스** 템플릿 (그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="74bd5-136">Right-click the Controllers folder and select the menu option **Add, New Item** and select the **Class** template (see Figure 4).</span></span>
2. <span data-ttu-id="74bd5-137">PersonController.cs 새 클래스 이름을 지정 하 고 클릭 합니다 **추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="74bd5-137">Name the new class PersonController.cs and click the **Add** button.</span></span>
3. <span data-ttu-id="74bd5-138">클래스는 기본 System.Web.Mvc.Controller 클래스 (참조 코드 3)에서 상속 되도록 생성 된 클래스 파일을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="74bd5-138">Modify the resulting class file so that the class inherits from the base System.Web.Mvc.Controller class (see Listing 3).</span></span>


<span data-ttu-id="74bd5-139">[![새 클래스 만들기](creating-a-controller-cs/_static/image4.jpg)](creating-a-controller-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="74bd5-139">[![Creating a new class](creating-a-controller-cs/_static/image4.jpg)](creating-a-controller-cs/_static/image7.png)</span></span>

<span data-ttu-id="74bd5-140">**그림 04**: 새 클래스 만들기 ([큰 이미지를 보려면 클릭](creating-a-controller-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="74bd5-140">**Figure 04**: Creating a new class([Click to view full-size image](creating-a-controller-cs/_static/image8.png))</span></span>


<span data-ttu-id="74bd5-141">**3-Controllers\PersonController.cs 나열**</span><span class="sxs-lookup"><span data-stu-id="74bd5-141">**Listing 3 - Controllers\PersonController.cs**</span></span>

[!code-csharp[Main](creating-a-controller-cs/samples/sample3.cs)]

<span data-ttu-id="74bd5-142">보기 3의 컨트롤러는 "Hello World!" 문자열을 반환 하는 index () 이라는 하나의 작업이 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="74bd5-142">The controller in Listing 3 exposes one action named Index() that returns the string "Hello World!".</span></span> <span data-ttu-id="74bd5-143">응용 프로그램을 실행 하 고 다음과 같은 URL을 요청 하 여이 컨트롤러 작업을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74bd5-143">You can invoke this controller action by running your application and requesting a URL like the following:</span></span>

`http://localhost:40071/Person`

> [!NOTE]
> 
> <span data-ttu-id="74bd5-144">ASP.NET Development Server는 임의의 포트 번호 (예를 들어 40071)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="74bd5-144">The ASP.NET Development Server uses a random port number (for example, 40071).</span></span> <span data-ttu-id="74bd5-145">컨트롤러를 호출 하는 URL을 입력 하는 경우 올바른 포트 번호를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74bd5-145">When entering a URL to invoke a controller, you'll need to supply the right port number.</span></span> <span data-ttu-id="74bd5-146">Windows 알림 영역 (아래쪽 오른쪽 화면)에서 ASP.NET 개발 서버에 대 한 아이콘 위로 마우스를 이동 하 여 포트 번호를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74bd5-146">You can determine the port number by hovering your mouse over the icon for the ASP.NET Development Server in the Windows Notification Area (bottom-right of your screen).</span></span>
> 
> [!div class="step-by-step"]
> <span data-ttu-id="74bd5-147">[이전](adding-dynamic-content-to-a-cached-page-cs.md)
> [다음](creating-an-action-cs.md)</span><span class="sxs-lookup"><span data-stu-id="74bd5-147">[Previous](adding-dynamic-content-to-a-cached-page-cs.md)
[Next](creating-an-action-cs.md)</span></span>
