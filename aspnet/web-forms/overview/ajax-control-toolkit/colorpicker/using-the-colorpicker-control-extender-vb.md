---
uid: web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
title: ColorPicker Control Extender (VB)를 사용 하 여 | Microsoft Docs
author: microsoft
description: ColorPicker 팝업 컨트롤의 UI를 사용 하 여 클라이언트 쪽 색 선택 기능을 제공 하는 ASP.NET AJAX extender입니다. 모든 ASP.NET에 연결할 수 있습니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/12/2009
ms.topic: article
ms.assetid: 577ae07b-a872-4818-a804-bca489b40ad0
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
msc.type: authoredcontent
ms.openlocfilehash: cad012dd1ce93714ecb127bf3543d5c65803aba9
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37374181"
---
<a name="using-the-colorpicker-control-extender-vb"></a><span data-ttu-id="acfd1-104">ColorPicker Control Extender (VB)를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="acfd1-104">Using the ColorPicker Control Extender (VB)</span></span>
====================
<span data-ttu-id="acfd1-105">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="acfd1-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="acfd1-106">ColorPicker 팝업 컨트롤의 UI를 사용 하 여 클라이언트 쪽 색 선택 기능을 제공 하는 ASP.NET AJAX extender입니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-106">ColorPicker is an ASP.NET AJAX extender that provides client-side color-picking functionality with UI in a popup control.</span></span> <span data-ttu-id="acfd1-107">모든 ASP.NET TextBox 컨트롤에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-107">It can be attached to any ASP.NET TextBox control.</span></span> <span data-ttu-id="acfd1-108">있습니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-108">It.</span></span>


<span data-ttu-id="acfd1-109">이 자습서의 목표는 AJAX Control Toolkit ColorPicker control extender를 사용 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-109">The goal of this tutorial is to explain how you can use the AJAX Control Toolkit ColorPicker control extender.</span></span> <span data-ttu-id="acfd1-110">ColorPicker control extender는 색을 선택할 수 있는 팝업 대화 상자를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-110">The ColorPicker control extender displays a popup dialog that enables you to select a color.</span></span> <span data-ttu-id="acfd1-111">ColorPicker는 색을 선택 하는 사용자에 대 한 직관적인 사용자 인터페이스를 제공 하려고 할 때마다 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-111">The ColorPicker is useful whenever you want to provide an intuitive user interface for a user to pick a color.</span></span>

## <a name="extending-a-textbox-control-with-the-colorpicker-control-extender"></a><span data-ttu-id="acfd1-112">ColorPicker Control Extender 사용 하 여 TextBox 컨트롤 확장</span><span class="sxs-lookup"><span data-stu-id="acfd1-112">Extending a TextBox Control with the ColorPicker Control Extender</span></span>

<span data-ttu-id="acfd1-113">예를 들어, 방문자가 사용자 지정된 비즈니스 카드를 만들 수 있는 웹 사이트를 만들려고 한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-113">Imagine, for example, that you want to create a website that enables visitors to create customized business cards.</span></span> <span data-ttu-id="acfd1-114">방문자는 비즈니스 카드에 대 한 텍스트를 입력 하 고 색을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-114">Visitors can enter the text for a business card and pick the color.</span></span> <span data-ttu-id="acfd1-115">목록 1의 ASP.NET 페이지 txtCardText 및 txtCardColor 라는 두 개의 텍스트 상자 컨트롤을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-115">The ASP.NET page in Listing 1 contains two TextBox controls named txtCardText and txtCardColor.</span></span> <span data-ttu-id="acfd1-116">폼을 제출 하면 선택한 값이 표시 됩니다 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="acfd1-116">When you submit the form, the selected values are displayed (see Figure 1).</span></span>


<span data-ttu-id="acfd1-117">[![명함을 만들기 위한 간단한 폼](using-the-colorpicker-control-extender-vb/_static/image1.jpg)](using-the-colorpicker-control-extender-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="acfd1-117">[![Simple form for creating a business card](using-the-colorpicker-control-extender-vb/_static/image1.jpg)](using-the-colorpicker-control-extender-vb/_static/image1.png)</span></span>

<span data-ttu-id="acfd1-118">**그림 01**: 명함을 만들기 위한 간단한 폼 ([큰 이미지를 보려면 클릭](using-the-colorpicker-control-extender-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="acfd1-118">**Figure 01**: Simple form for creating a business card ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image2.png))</span></span>


<span data-ttu-id="acfd1-119">**1-CreateCard.aspx 나열**</span><span class="sxs-lookup"><span data-stu-id="acfd1-119">**Listing 1 - CreateCard.aspx**</span></span>

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample1.aspx)]

<span data-ttu-id="acfd1-120">목록 1 작동 하지만 형태로 훌륭한 사용자 환경을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-120">The form in Listing 1 works, but it does not provide a great user experience.</span></span> <span data-ttu-id="acfd1-121">사용자는 색을 텍스트 상자에 입력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-121">The user has to type a color into the textbox.</span></span> <span data-ttu-id="acfd1-122">사용자가 특수 한 색-예를 들어 pea 녹색-사용자의 올바른 음영 방금 알아내야 도움이 없이 HTML 색 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-122">If the user wants a specialized color - for example, just the right shade of pea green - then the user must figure out the HTML color code without any help.</span></span>

<span data-ttu-id="acfd1-123">더 나은 사용자 환경을 만들려면 ColorPicker control extender를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-123">You can use the ColorPicker control extender to create a better user experience.</span></span> <span data-ttu-id="acfd1-124">ColorPicker는 TextBox 컨트롤에 포커스를 이동 하는 경우 색 대화 상자를 표시 합니다 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="acfd1-124">The ColorPicker displays a color dialog when you move focus to a TextBox control (see Figure 2).</span></span>


<span data-ttu-id="acfd1-125">[![ColorPicker Control Extender](using-the-colorpicker-control-extender-vb/_static/image2.jpg)](using-the-colorpicker-control-extender-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="acfd1-125">[![The ColorPicker Control Extender](using-the-colorpicker-control-extender-vb/_static/image2.jpg)](using-the-colorpicker-control-extender-vb/_static/image3.png)</span></span>

<span data-ttu-id="acfd1-126">**그림 02**: The ColorPicker Control Extender ([큰 이미지를 보려면 클릭](using-the-colorpicker-control-extender-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="acfd1-126">**Figure 02**: The ColorPicker Control Extender ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image4.png))</span></span>


<span data-ttu-id="acfd1-127">목록 1 양식을 사용 하 여 ColorPicker control extender를 사용 하는 두 단계를 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-127">You need to complete two steps to use the ColorPicker control extender with the form in Listing 1:</span></span>

1. <span data-ttu-id="acfd1-128">페이지에 ScriptManager 컨트롤을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-128">Add a ScriptManager control to the page</span></span>
2. <span data-ttu-id="acfd1-129">ColorPicker control extender를 페이지에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-129">Add the ColorPicker control extender to the page</span></span>

<span data-ttu-id="acfd1-130">ColorPicker를 사용 하려면 먼저 페이지에 ScriptManager를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-130">Before you can use the ColorPicker, you must add a ScriptManager to your page.</span></span> <span data-ttu-id="acfd1-131">열기 서버 쪽 바로 아래는 ScriptManager를 추가 하는 것이 좋습니다 &lt;폼&gt; 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-131">A good place to add the ScriptManager is right below the opening server-side &lt;form&gt; tag.</span></span> <span data-ttu-id="acfd1-132">(ScriptManager는 AJAX 확장명 탭 아래에 있습니다.)를 도구 상자에서 페이지로 ScriptManager를 끌 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-132">You can drag the ScriptManager onto the page from the toolbox (the ScriptManager is located under the AJAX Extensions tab).</span></span> <span data-ttu-id="acfd1-133">또는 서버 쪽 양식의 태그 아래에 있는 소스 뷰로 다음 태그를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-133">Alternatively, you can type the following tag into Source View beneath the opening server-side form tag:</span></span>

<span data-ttu-id="acfd1-134">&lt;asp:ScriptManager ID="ScriptManager1" runat="server" /&gt;</span><span class="sxs-lookup"><span data-stu-id="acfd1-134">&lt;asp:ScriptManager ID="ScriptManager1" runat="server" /&gt;</span></span>

<span data-ttu-id="acfd1-135">디자인 뷰에서 가장 쉬운 방법은 ColorPicker control extender를 페이지에 추가할 경우</span><span class="sxs-lookup"><span data-stu-id="acfd1-135">The easiest way to add the ColorPicker control extender to the page is in Design View.</span></span> <span data-ttu-id="acfd1-136">스마트 작업 옵션을 사용 하도록 설정 나타납니다 txtCardColor 텍스트 상자 위에 마우스를 놓으면 extender를 추가할 수 있습니다 (그림 3 참조).</span><span class="sxs-lookup"><span data-stu-id="acfd1-136">If you hover your mouse over the txtCardColor TextBox, a smart task option appears the enables you to add an extender (see Figure 3).</span></span> <span data-ttu-id="acfd1-137">이 옵션을 선택 하면 Extender 마법사 나타납니다 (그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="acfd1-137">If you pick this option, the Extender Wizard appears (see Figure 4).</span></span>


<span data-ttu-id="acfd1-138">[![Extender를 추가합니다.](using-the-colorpicker-control-extender-vb/_static/image3.jpg)](using-the-colorpicker-control-extender-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="acfd1-138">[![Adding an extender](using-the-colorpicker-control-extender-vb/_static/image3.jpg)](using-the-colorpicker-control-extender-vb/_static/image5.png)</span></span>

<span data-ttu-id="acfd1-139">**그림 03**: extender 추가 ([큰 이미지를 보려면 클릭](using-the-colorpicker-control-extender-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="acfd1-139">**Figure 03**: Adding an extender ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image6.png))</span></span>


<span data-ttu-id="acfd1-140">[![Extender 마법사를 사용 하 여 컨트롤 extender를 선택합니다.](using-the-colorpicker-control-extender-vb/_static/image4.jpg)](using-the-colorpicker-control-extender-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="acfd1-140">[![Selecting a control extender with the Extender Wizard](using-the-colorpicker-control-extender-vb/_static/image4.jpg)](using-the-colorpicker-control-extender-vb/_static/image7.png)</span></span>

<span data-ttu-id="acfd1-141">**그림 04**: Extender 마법사를 사용 하 여 컨트롤 extender를 선택 하면 ([큰 이미지를 보려면 클릭](using-the-colorpicker-control-extender-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="acfd1-141">**Figure 04**: Selecting a control extender with the Extender Wizard ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image8.png))</span></span>


<span data-ttu-id="acfd1-142">ColorPicker extender 사용 하 여 텍스트 상자 txtCardColor 확장할 ColorPicker extender를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-142">You can pick the ColorPicker extender to extend the txtCardColor TextBox with the ColorPicker extender.</span></span> <span data-ttu-id="acfd1-143">대화 상자를 닫으려면 확인을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-143">Click OK to close the dialog.</span></span>

<span data-ttu-id="acfd1-144">이러한 변경을 수행한 후 페이지에 대 한 원본 목록 2와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-144">After you make these changes, the source for the page looks like Listing 2.</span></span>

<span data-ttu-id="acfd1-145">**2-(사용 하 여 ColorPicker) CreateCard.aspx 나열**</span><span class="sxs-lookup"><span data-stu-id="acfd1-145">**Listing 2 - CreateCard.aspx (with ColorPicker)**</span></span>

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample2.aspx)]

<span data-ttu-id="acfd1-146">페이지에 이제 txtCardColor TextBox 컨트롤 바로 아래 표시 되는 ColorPickerExtender 컨트롤 포함 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-146">Notice that the page now contains a ColorPickerExtender control that appears directly below the txtCardColor TextBox control.</span></span> <span data-ttu-id="acfd1-147">색 선택 대화 상자가 표시 되도록 ColorPickerExtender 컨트롤 txtCardColor 컨트롤을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-147">The ColorPickerExtender control extends the txtCardColor control so that it displays a color picker dialog.</span></span>

## <a name="using-a-button-to-launch-the-color-picker-dialog"></a><span data-ttu-id="acfd1-148">단추를 사용 하 여 색 선택 대화 상자를 시작 하려면</span><span class="sxs-lookup"><span data-stu-id="acfd1-148">Using a Button to Launch the Color Picker Dialog</span></span>

<span data-ttu-id="acfd1-149">ColorPicker extender는 다음 속성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-149">The ColorPicker extender supports the following properties:</span></span>

- <span data-ttu-id="acfd1-150">PopupButtonId-ID 색 선택 대화 상자를 표시 하는 페이지의 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-150">PopupButtonId - The ID of a button on the page that causes the color picker dialog to appear.</span></span>
- <span data-ttu-id="acfd1-151">Popupposition 속성은-색 선택 대화 상자의 대상 컨트롤에 상대적인 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-151">PopupPosition - The position, relative to the target control, of the color picker dialog.</span></span> <span data-ttu-id="acfd1-152">가능한 값은 절대, Center, 왼쪽 맨 아래, 오른쪽 맨 아래, 왼쪽 맨 위, 오른쪽, 오른쪽 맨 위 및 왼쪽 (기본값인 왼쪽 맨 아래).</span><span class="sxs-lookup"><span data-stu-id="acfd1-152">Possible values are Absolute, Center, BottomLeft, BottomRight, TopLeft, TopRight, Right, and Left (the default is BottomLeft).</span></span>
- <span data-ttu-id="acfd1-153">SampleControlId-선택한 색을 표시 하는 컨트롤의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-153">SampleControlId - The ID of a control that displays the selected color.</span></span>
- <span data-ttu-id="acfd1-154">SelectedColor-는 ColorPicker 선택한 초기 색입니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-154">SelectedColor - The initial color selected by the ColorPicker.</span></span>

<span data-ttu-id="acfd1-155">색 선택 대화 상자가 표시 되는 방식 및 선택한 색이 표시 되는 방식을 사용자 지정 하려면 이러한 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-155">You can use these properties to customize how the color picker dialog is displayed and how the selected color is displayed.</span></span> <span data-ttu-id="acfd1-156">목록 3에서 페이지에서는 이러한 속성 중 일부를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-156">The page in Listing 3 illustrates how you can use several of these properties.</span></span>

<span data-ttu-id="acfd1-157">**3-CreateCardButton.aspx 나열**</span><span class="sxs-lookup"><span data-stu-id="acfd1-157">**Listing 3 - CreateCardButton.aspx**</span></span>

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample3.aspx)]

<span data-ttu-id="acfd1-158">목록 3에서 페이지 포함 색 선택 단추 (그림 5 참조).</span><span class="sxs-lookup"><span data-stu-id="acfd1-158">The page in Listing 3 includes a Pick Color button (see Figure 5).</span></span> <span data-ttu-id="acfd1-159">이 단추를 클릭할 때 텍스트 상자 위에 색 선택 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-159">When you click this button, the color picker dialog appears above the TextBox.</span></span> <span data-ttu-id="acfd1-160">대화 상자에서 색을 선택 하면 선택한 색 lblSample 레이블 컨트롤의 배경색으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-160">If you select a color from the dialog then the selected color appears as the background color of the lblSample Label control.</span></span>

<span data-ttu-id="acfd1-161">ColorPicker PopupButtonID 속성 ColorPicker extender를 사용 하 여 색 선택 단추를 연결할 때 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-161">The ColorPicker PopupButtonID property is used to associate the Pick Color button with the ColorPicker extender.</span></span> <span data-ttu-id="acfd1-162">PopupButtonID 속성에 대 한 값을 제공 하면 색 선택 대화 상자는 더 이상 대상 컨트롤에 포커스가 있을 때 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-162">When you supply a value for the PopupButtonID property, the color picker dialog no longer appears when the target control has focus.</span></span> <span data-ttu-id="acfd1-163">대화 상자를 표시 하려면 단추를 클릭 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-163">You must click the button to display the dialog.</span></span>

<span data-ttu-id="acfd1-164">ColorPicker 사용 하 여 선택한 색을 표시 하는 컨트롤을 연결할 SampleControlID 속성이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-164">The SampleControlID property is used to associate a control that displays the selected color with the ColorPicker.</span></span> <span data-ttu-id="acfd1-165">ColorPicker는 현재 선택한 색으로이 컨트롤의 배경색을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-165">The ColorPicker changes the background color of this control to the currently selected color.</span></span>


<span data-ttu-id="acfd1-166">[![단추를 사용 하 여 색 선택 대화 상자를 표시합니다.](using-the-colorpicker-control-extender-vb/_static/image5.jpg)](using-the-colorpicker-control-extender-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="acfd1-166">[![Displaying the color picker dialog with a button](using-the-colorpicker-control-extender-vb/_static/image5.jpg)](using-the-colorpicker-control-extender-vb/_static/image9.png)</span></span>

<span data-ttu-id="acfd1-167">**그림 05**: 단추를 사용 하 여 색 선택 대화 상자 표시 ([큰 이미지를 보려면 클릭](using-the-colorpicker-control-extender-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="acfd1-167">**Figure 05**: Displaying the color picker dialog with a button ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image10.png))</span></span>


## <a name="summary"></a><span data-ttu-id="acfd1-168">요약</span><span class="sxs-lookup"><span data-stu-id="acfd1-168">Summary</span></span>

<span data-ttu-id="acfd1-169">이 자습서에서는 ColorPicker control extender를 사용 하 여 팝업 색 선택 대화 상자를 표시 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-169">In this tutorial, you learned how to use the ColorPicker control extender to display a popup color picker dialog.</span></span> <span data-ttu-id="acfd1-170">먼저 포커스가 TextBox 컨트롤을 이동 하는 경우 대화 상자에 표시 하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-170">First, we examined how you can display the dialog when focus is moved to a TextBox control.</span></span> <span data-ttu-id="acfd1-171">다음으로 단추를 클릭 하면 색 선택 대화 상자를 표시 하는 단추를 만드는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="acfd1-171">Next, you learned how to create a button that displays the color picker dialog when the button is clicked.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="acfd1-172">이전</span><span class="sxs-lookup"><span data-stu-id="acfd1-172">Previous</span></span>](using-the-colorpicker-control-extender-cs.md)
