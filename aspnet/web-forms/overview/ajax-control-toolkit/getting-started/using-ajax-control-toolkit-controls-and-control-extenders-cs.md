---
uid: web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
title: "AJAX 컨트롤 Toolkit 컨트롤 및 컨트롤 Extender (C#)를 사용 하 여 | Microsoft Docs"
author: microsoft
description: "ASP.NET 페이지 들어 컨트롤과 extender를 추가 하는 방법을 알아봅니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/12/2009
ms.topic: article
ms.assetid: c1e6b51c-3bc3-4bf7-9916-9991197af3dd
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
msc.type: authoredcontent
ms.openlocfilehash: 42a210ac41e83e2379aa64979f42ce66c843f878
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="using-ajax-control-toolkit-controls-and-control-extenders-c"></a><span data-ttu-id="0a016-103">AJAX 컨트롤 Toolkit 컨트롤 및 컨트롤 Extender (C#)를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="0a016-103">Using AJAX Control Toolkit Controls and Control Extenders (C#)</span></span>
====================
<span data-ttu-id="0a016-104">여 [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="0a016-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="0a016-105">ASP.NET 페이지 들어 컨트롤과 extender를 추가 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0a016-105">Learn how to add AJAX Control Toolkit controls and extenders to your ASP.NET pages.</span></span>


<span data-ttu-id="0a016-106">들어 컨트롤 및 컨트롤 extender 집합이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a016-106">The AJAX Control Toolkit contains a set of controls and control extenders.</span></span> <span data-ttu-id="0a016-107">이 간략 한 자습서를 ASP.NET 페이지에 컨트롤 및 컨트롤 extender를 모두 추가 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a016-107">In this brief tutorial, you learn how to add both controls and control extenders to an ASP.NET page.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="0a016-108">에 대 한 들어를 설치 하 고 Visual Studio/Visual Web Developer 도구 상자에 들어 추가 참조 자습서 [들어 시작](get-started-with-the-ajax-control-toolkit-cs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0a016-108">For instructions on installing the AJAX Control Toolkit and adding the AJAX Control Toolkit to the Visual Studio/Visual Web Developer toolbox, see the tutorial [Get Started with the AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-cs.md).</span></span>


## <a name="using-ajax-control-toolkit-controls"></a><span data-ttu-id="0a016-109">AJAX 컨트롤 Toolkit 컨트롤을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="0a016-109">Using AJAX Control Toolkit Controls</span></span>

<span data-ttu-id="0a016-110">들어 컨트롤은 일반적인 ASP.NET 제어와 마찬가지로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="0a016-110">An AJAX Control Toolkit control works just like a normal ASP.NET control.</span></span> <span data-ttu-id="0a016-111">ASP.NET 페이지 도구 상자에서 컨트롤을 끌 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a016-111">You can drag the control from the toolbox onto an ASP.NET page.</span></span> <span data-ttu-id="0a016-112">디자인 뷰 또는 소스 뷰 페이지에 컨트롤을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a016-112">You can add the control to the page in either Design view or Source view.</span></span>

<span data-ttu-id="0a016-113">들어에서 컨트롤을 사용 하는 경우 특별 한 요구 사항이 하나 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a016-113">There is one special requirement when using the controls from the AJAX Control Toolkit.</span></span> <span data-ttu-id="0a016-114">페이지에 ScriptManager 컨트롤을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a016-114">The page must contain a ScriptManager control.</span></span> <span data-ttu-id="0a016-115">ScriptManager 컨트롤은 모든 들어 컨트롤에 필요한 필요한 JavaScript를 포함 하는 것에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a016-115">The ScriptManager control is responsible for including all of the necessary JavaScript required by the AJAX Control Toolkit controls.</span></span>

<span data-ttu-id="0a016-116">예를 들어 들어 탭은 편집기 컨트롤 이라는 컨트롤을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a016-116">For example, the AJAX Control Toolkit tab includes a control named the Editor control.</span></span> <span data-ttu-id="0a016-117">이 컨트롤은 서식 있는 HTML 편집기를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a016-117">This control displays a rich HTML editor.</span></span> <span data-ttu-id="0a016-118">페이지에는 편집기 컨트롤을 추가 하려면 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a016-118">Follow these steps to add the Editor control to a page:</span></span>

1. <span data-ttu-id="0a016-119">ShowEditor.aspx 이라는 새 ASP.NET 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="0a016-119">Create a new ASP.NET page named ShowEditor.aspx</span></span>
2. <span data-ttu-id="0a016-120">도구 상자에서 AJAX 확장 탭 아래 ScriptManager 컨트롤을 선택 하 고 컨트롤을 페이지로 끕니다.</span><span class="sxs-lookup"><span data-stu-id="0a016-120">Select the ScriptManager control from beneath the AJAX Extensions tab in the toolbox and drag the control onto the page.</span></span>
3. <span data-ttu-id="0a016-121">도구 상자에서 들어 탭 아래 편집기 컨트롤을 선택 하 고 컨트롤을 페이지로 끌어 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="0a016-121">Select the Editor control from beneath the AJAX Control Toolkit tab in the toolbox and drag the control onto the page (see Figure 1).</span></span> <span data-ttu-id="0a016-122">디자이너는 그림 2와 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a016-122">The Designer should look like Figure 2.</span></span>
4. <span data-ttu-id="0a016-123">메뉴 옵션을 선택 하 여 웹 사이트를 실행 **디버그, 디버깅 시작** 또는 F5 키를 방문 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a016-123">Run the web site by selecting the menu option **Debug, Start Debugging** or hitting the F5 key.</span></span>
5. <span data-ttu-id="0a016-124">그림 3에 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0a016-124">You should see the page in Figure 3.</span></span>


<span data-ttu-id="0a016-125">[![HTML 편집기 컨트롤 선택](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="0a016-125">[![Selecting the HTML Editor control](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.png)</span></span>

<span data-ttu-id="0a016-126">**그림 01**: HTML 편집기 컨트롤을 선택 하면 ([전체 크기 이미지를 보려면 클릭](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="0a016-126">**Figure 01**: Selecting the HTML Editor control([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.png))</span></span>


<span data-ttu-id="0a016-127">[![ScriptManager 및 편집 컨트롤과 visual Studio 디자이너](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="0a016-127">[![Visual Studio Designer with ScriptManager and Edit control](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.png)</span></span>

<span data-ttu-id="0a016-128">**그림 02**: ScriptManager 및 편집 컨트롤과 Visual Studio 디자이너 ([전체 크기 이미지를 보려면 클릭](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="0a016-128">**Figure 02**: Visual Studio Designer with ScriptManager and Edit control([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.png))</span></span>


<span data-ttu-id="0a016-129">[![DisplayEditor.aspx 페이지](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="0a016-129">[![The DisplayEditor.aspx page](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.png)</span></span>

<span data-ttu-id="0a016-130">**그림 03**: The DisplayEditor.aspx 페이지 ([전체 크기 이미지를 보려면 클릭](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="0a016-130">**Figure 03**: The DisplayEditor.aspx page([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.png))</span></span>


## <a name="using-ajax-control-toolkit-control-extenders"></a><span data-ttu-id="0a016-131">AJAX 컨트롤 Toolkit 컨트롤 Extender를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="0a016-131">Using AJAX Control Toolkit Control Extenders</span></span>

<span data-ttu-id="0a016-132">또한 들어 extender 컨트롤을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="0a016-132">The AJAX Control Toolkit also contains control extenders.</span></span> <span data-ttu-id="0a016-133">해당 이름에서 알 수 있듯이 컨트롤 extender는 기존 컨트롤의 기능을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a016-133">As its name suggests, a control extender extends the functionality of an existing control.</span></span> <span data-ttu-id="0a016-134">예를 들어 ConfirmButton 컨트롤 extender 표준 ASP.NET Button 컨트롤을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="0a016-134">For example, the ConfirmButton control extender extends the standard ASP.NET Button control.</span></span> <span data-ttu-id="0a016-135">Extender는 단추 클릭 하면 확인 대화 상자를 표시 하도록 단추 컨트롤의 동작을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a016-135">The extender changes the Button control�s behavior so that the Button displays a confirmation dialog when you click it.</span></span>

<span data-ttu-id="0a016-136">들어 제어와 마찬가지로 컨트롤 extender에는 ScriptManager 컨트롤이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a016-136">A control extender, just like an AJAX Control Toolkit control, requires a ScriptManager control.</span></span> <span data-ttu-id="0a016-137">Extender 컨트롤을 사용 하 여 페이지에서를 시작 하기 전에 페이지에 ScriptManager 컨트롤을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a016-137">You must add a ScriptManager control to a page before you start using control extenders in the page.</span></span>

<span data-ttu-id="0a016-138">ConfirmButton 컨트롤 extender를 사용 하려면 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a016-138">Follow these steps to use the ConfirmButton control extender:</span></span>

1. <span data-ttu-id="0a016-139">ShowConfirmButton.aspx 이라는 새 ASP.NET 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="0a016-139">Create a new ASP.NET page named ShowConfirmButton.aspx</span></span>
2. <span data-ttu-id="0a016-140">AJAX 확장 탭 아래 페이지에 컨트롤을 끌어 페이지에 ScriptManager 컨트롤을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a016-140">Add a ScriptManager control to the page by dragging the control onto the page from beneath the AJAX Extensions tab.</span></span>
3. <span data-ttu-id="0a016-141">도구 상자는 디자이너 화면에서 표준 탭 아래 단추를 끌어 페이지에 표준 단추 컨트롤을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a016-141">Add a standard Button control to the page by dragging the Button from beneath the Standard tab in the toolbox onto the Designer surface.</span></span>
4. <span data-ttu-id="0a016-142">클릭는 **Extender 추가** 작업 옵션 (그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="0a016-142">Click the **Add Extender** task option (see Figure 4).</span></span>
5. <span data-ttu-id="0a016-143">Extender 선택 대화 상자에서 ConfirmButtonExtender 선택 (그림 5 참조) 확인 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a016-143">In the Choose Extender dialog, select ConfirmButtonExtender (see Figure 5) and click the OK button.</span></span>
6. <span data-ttu-id="0a016-144">디자이너에서 단추 컨트롤을 선택 하 고 Button1 Extender 확장\_속성 창에서 ConfirmButtonExtender 노드 (그림 6 참조).</span><span class="sxs-lookup"><span data-stu-id="0a016-144">Select the Button control in the Designer and expand the Extenders, Button1\_ConfirmButtonExtender node in the Properties window (see Figure 6).</span></span> <span data-ttu-id="0a016-145">값을 할당 *실제로?* ConfirmText 속성에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a016-145">Assign the value *�Really?�* to the ConfirmText property.</span></span>
7. <span data-ttu-id="0a016-146">메뉴 옵션을 선택 하 여 페이지를 실행 **디버그, 디버깅 시작** 또는 F5 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="0a016-146">Run the page by selecting the menu option **Debug, Start Debugging** or hit the F5 key.</span></span>


<span data-ttu-id="0a016-147">[![Extender 추가 작업 옵션](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="0a016-147">[![The Add Extender task option](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.png)</span></span>

<span data-ttu-id="0a016-148">**그림 04**: Extender 추가 작업 옵션 ([전체 크기 이미지를 보려면 클릭](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="0a016-148">**Figure 04**: The Add Extender task option([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image8.png))</span></span>


<span data-ttu-id="0a016-149">[![ConfirmButton 컨트롤 extender를 선택합니다.](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="0a016-149">[![Selecting the ConfirmButton control extender](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image9.png)</span></span>

<span data-ttu-id="0a016-150">**그림 05**: ConfirmButton 컨트롤 extender를 선택 하면 ([전체 크기 이미지를 보려면 클릭](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="0a016-150">**Figure 05**: Selecting the ConfirmButton control extender([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image10.png))</span></span>


<span data-ttu-id="0a016-151">[![ConfirmButton 속성 설정](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="0a016-151">[![Setting a ConfirmButton property](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image11.png)</span></span>

<span data-ttu-id="0a016-152">**그림 06**: ConfirmButton 속성 설정 ([전체 크기 이미지를 보려면 클릭](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="0a016-152">**Figure 06**: Setting a ConfirmButton property([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image12.png))</span></span>


<span data-ttu-id="0a016-153">페이지가 열릴 때 단추를 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a016-153">When the page opens, you should see a button.</span></span> <span data-ttu-id="0a016-154">단추를 클릭할 경우 그림 7에 확인 대화 상자를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0a016-154">When you click the button, you get the confirmation dialog in Figure 7.</span></span>


<span data-ttu-id="0a016-155">[![확인 대화 상자를 표시합니다.](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="0a016-155">[![Displaying the confirmation dialog](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image13.png)</span></span>

<span data-ttu-id="0a016-156">**그림 07**: 확인 대화 상자 표시 ([전체 크기 이미지를 보려면 클릭](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="0a016-156">**Figure 07**: Displaying the confirmation dialog([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image14.png))</span></span>


<span data-ttu-id="0a016-157">일반적으로 끌어 오지 않은 컨트롤 extender 페이지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a016-157">Notice that you normally do not drag a control extender onto a page.</span></span> <span data-ttu-id="0a016-158">대신, 사용 하 여는 **Extender 추가** extender 컨트롤을 추가 하는 페이지에 이미 추가 옵션을 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a016-158">Instead, you use the **Add Extender** task option to add an extender to a control that you have already added to a page.</span></span> <span data-ttu-id="0a016-159">또한 설정한 컨트롤 extender 속성을 확장 하 고 컨트롤에 대 한 속성 시트를 열어 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a016-159">Notice, furthermore, that you set control extender properties by opening the property sheet for the control being extended.</span></span>

<span data-ttu-id="0a016-160">여러 컨트롤 extender에서 단일 ASP.NET 컨트롤을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a016-160">A single ASP.NET control can be extended by multiple control extenders.</span></span> <span data-ttu-id="0a016-161">확장 하 고 컨트롤에 대 한 속성 시트 컨트롤에 연결 된 컨트롤 extender의 모든 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a016-161">The property sheet for the control being extended will list all of the control extenders associated with the control.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="0a016-162">[이전](get-started-with-the-ajax-control-toolkit-cs.md)
[다음](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)</span><span class="sxs-lookup"><span data-stu-id="0a016-162">[Previous](get-started-with-the-ajax-control-toolkit-cs.md)
[Next](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)</span></span>
