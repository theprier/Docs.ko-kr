---
uid: web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
title: ColorPicker 컨트롤 Extender (VB)를 사용 하 여 | Microsoft Docs
author: microsoft
description: ColorPicker는 popup 컨트롤의 UI를 사용한 클라이언트 쪽 색 선택 기능을 제공 하는 ASP.NET AJAX extender입니다. 모든 ASP.NET에는 연결할 수 있습니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/12/2009
ms.topic: article
ms.assetid: 577ae07b-a872-4818-a804-bca489b40ad0
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
msc.type: authoredcontent
ms.openlocfilehash: 3411119f85d7f5c26703b7df40cff24fdf30b81d
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30874527"
---
<a name="using-the-colorpicker-control-extender-vb"></a><span data-ttu-id="55cca-104">ColorPicker 컨트롤 Extender (VB)를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="55cca-104">Using the ColorPicker Control Extender (VB)</span></span>
====================
<span data-ttu-id="55cca-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="55cca-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="55cca-106">ColorPicker는 popup 컨트롤의 UI를 사용한 클라이언트 쪽 색 선택 기능을 제공 하는 ASP.NET AJAX extender입니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-106">ColorPicker is an ASP.NET AJAX extender that provides client-side color-picking functionality with UI in a popup control.</span></span> <span data-ttu-id="55cca-107">ASP.NET TextBox 컨트롤에 연결 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-107">It can be attached to any ASP.NET TextBox control.</span></span> <span data-ttu-id="55cca-108">It.</span><span class="sxs-lookup"><span data-stu-id="55cca-108">It.</span></span>


<span data-ttu-id="55cca-109">이 자습서의 목표 AJAX 컨트롤 Toolkit ColorPicker 컨트롤 extender를 사용 하는 방법을 설명 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-109">The goal of this tutorial is to explain how you can use the AJAX Control Toolkit ColorPicker control extender.</span></span> <span data-ttu-id="55cca-110">ColorPicker 컨트롤 extender 색을 선택할 수 있는 팝업 대화 상자를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-110">The ColorPicker control extender displays a popup dialog that enables you to select a color.</span></span> <span data-ttu-id="55cca-111">ColorPicker 색을 선택 하는 사용자에 대 한 직관적인 사용자 인터페이스를 제공 하려는 경우 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-111">The ColorPicker is useful whenever you want to provide an intuitive user interface for a user to pick a color.</span></span>

## <a name="extending-a-textbox-control-with-the-colorpicker-control-extender"></a><span data-ttu-id="55cca-112">ColorPicker 컨트롤 Extender 있는 TextBox 컨트롤을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-112">Extending a TextBox Control with the ColorPicker Control Extender</span></span>

<span data-ttu-id="55cca-113">예를 들어 방문자가 사용자 지정 된 비즈니스 명함을 만들 수 있는 웹 사이트를 만들 것인지 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-113">Imagine, for example, that you want to create a website that enables visitors to create customized business cards.</span></span> <span data-ttu-id="55cca-114">방문자는 비즈니스 카드에 대 한 텍스트를 입력 하 고 색을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-114">Visitors can enter the text for a business card and pick the color.</span></span> <span data-ttu-id="55cca-115">목록 1에서 ASP.NET 페이지 txtCardText 및 txtCardColor 라는 두 개의 TextBox 컨트롤을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-115">The ASP.NET page in Listing 1 contains two TextBox controls named txtCardText and txtCardColor.</span></span> <span data-ttu-id="55cca-116">폼을 제출 하면 선택 된 값이 표시 됩니다 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="55cca-116">When you submit the form, the selected values are displayed (see Figure 1).</span></span>


<span data-ttu-id="55cca-117">[![명함을 만들기 위한 단순 양식](using-the-colorpicker-control-extender-vb/_static/image1.jpg)](using-the-colorpicker-control-extender-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="55cca-117">[![Simple form for creating a business card](using-the-colorpicker-control-extender-vb/_static/image1.jpg)](using-the-colorpicker-control-extender-vb/_static/image1.png)</span></span>

<span data-ttu-id="55cca-118">**그림 01**: 명함을 만들기 위한 간단한 형태 ([전체 크기 이미지를 보려면 클릭](using-the-colorpicker-control-extender-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="55cca-118">**Figure 01**: Simple form for creating a business card ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image2.png))</span></span>


<span data-ttu-id="55cca-119">**1-CreateCard.aspx 나열**</span><span class="sxs-lookup"><span data-stu-id="55cca-119">**Listing 1 - CreateCard.aspx**</span></span>

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample1.aspx)]

<span data-ttu-id="55cca-120">폼 목록 1의 작동에는 뛰어난 사용자 환경을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-120">The form in Listing 1 works, but it does not provide a great user experience.</span></span> <span data-ttu-id="55cca-121">사용자는 색 입력란에 입력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-121">The user has to type a color into the textbox.</span></span> <span data-ttu-id="55cca-122">사용자가 특수 색상-예를 들어 pea 녹색-다음 사용자의 오른쪽 음영 방금 알아내야 모든 도움 없이 HTML 색상 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-122">If the user wants a specialized color - for example, just the right shade of pea green - then the user must figure out the HTML color code without any help.</span></span>

<span data-ttu-id="55cca-123">더 나은 사용자 환경을 만드는 ColorPicker 컨트롤 extender를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-123">You can use the ColorPicker control extender to create a better user experience.</span></span> <span data-ttu-id="55cca-124">ColorPicker TextBox 컨트롤에 포커스를 이동 하면 색 대화 상자를 표시 합니다 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="55cca-124">The ColorPicker displays a color dialog when you move focus to a TextBox control (see Figure 2).</span></span>


<span data-ttu-id="55cca-125">[![ColorPicker 컨트롤 Extender](using-the-colorpicker-control-extender-vb/_static/image2.jpg)](using-the-colorpicker-control-extender-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="55cca-125">[![The ColorPicker Control Extender](using-the-colorpicker-control-extender-vb/_static/image2.jpg)](using-the-colorpicker-control-extender-vb/_static/image3.png)</span></span>

<span data-ttu-id="55cca-126">**그림 02**: The ColorPicker 컨트롤 Extender ([전체 크기 이미지를 보려면 클릭](using-the-colorpicker-control-extender-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="55cca-126">**Figure 02**: The ColorPicker Control Extender ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image4.png))</span></span>


<span data-ttu-id="55cca-127">목록 1 양식을 사용 하 여 ColorPicker 컨트롤 extender를 사용 하는 두 단계를 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-127">You need to complete two steps to use the ColorPicker control extender with the form in Listing 1:</span></span>

1. <span data-ttu-id="55cca-128">페이지에 ScriptManager 컨트롤 추가</span><span class="sxs-lookup"><span data-stu-id="55cca-128">Add a ScriptManager control to the page</span></span>
2. <span data-ttu-id="55cca-129">ColorPicker 컨트롤 extender 페이지에 추가</span><span class="sxs-lookup"><span data-stu-id="55cca-129">Add the ColorPicker control extender to the page</span></span>

<span data-ttu-id="55cca-130">ColorPicker를 사용 하려면 먼저 페이지에 ScriptManager를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-130">Before you can use the ColorPicker, you must add a ScriptManager to your page.</span></span> <span data-ttu-id="55cca-131">여는 서버 쪽 바로 아래 ScriptManager를 추가 하는 데는 &lt;양식&gt; 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-131">A good place to add the ScriptManager is right below the opening server-side &lt;form&gt; tag.</span></span> <span data-ttu-id="55cca-132">(ScriptManager AJAX 확장 탭에 있습니다.)를 도구 상자에서 ScriptManager 페이지 끌 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-132">You can drag the ScriptManager onto the page from the toolbox (the ScriptManager is located under the AJAX Extensions tab).</span></span> <span data-ttu-id="55cca-133">또는 여는 서버측 form 태그 아래에 있는 소스 보기에는 다음과 같은 태그를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-133">Alternatively, you can type the following tag into Source View beneath the opening server-side form tag:</span></span>

<span data-ttu-id="55cca-134">&lt;asp:ScriptManager ID="ScriptManager1" runat="server" /&gt;</span><span class="sxs-lookup"><span data-stu-id="55cca-134">&lt;asp:ScriptManager ID="ScriptManager1" runat="server" /&gt;</span></span>

<span data-ttu-id="55cca-135">디자인 뷰에서 페이지로 ColorPicker 컨트롤 extender를 추가 하는 가장 쉬운 방법은 됩니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-135">The easiest way to add the ColorPicker control extender to the page is in Design View.</span></span> <span data-ttu-id="55cca-136">스마트 작업 옵션을 사용 하면 표시 TextBox txtCardColor 위로 마우스를 가져가면 extender를 추가할 수 있습니다 (그림 3 참조).</span><span class="sxs-lookup"><span data-stu-id="55cca-136">If you hover your mouse over the txtCardColor TextBox, a smart task option appears the enables you to add an extender (see Figure 3).</span></span> <span data-ttu-id="55cca-137">이 옵션을 선택 하면 Extender 마법사 (그림 4 참조)가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-137">If you pick this option, the Extender Wizard appears (see Figure 4).</span></span>


<span data-ttu-id="55cca-138">[![Extender를 추가합니다.](using-the-colorpicker-control-extender-vb/_static/image3.jpg)](using-the-colorpicker-control-extender-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="55cca-138">[![Adding an extender](using-the-colorpicker-control-extender-vb/_static/image3.jpg)](using-the-colorpicker-control-extender-vb/_static/image5.png)</span></span>

<span data-ttu-id="55cca-139">**그림 03**: extender 추가 ([전체 크기 이미지를 보려면 클릭](using-the-colorpicker-control-extender-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="55cca-139">**Figure 03**: Adding an extender ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image6.png))</span></span>


<span data-ttu-id="55cca-140">[![Extender 마법사로 컨트롤 extender를 선택합니다.](using-the-colorpicker-control-extender-vb/_static/image4.jpg)](using-the-colorpicker-control-extender-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="55cca-140">[![Selecting a control extender with the Extender Wizard](using-the-colorpicker-control-extender-vb/_static/image4.jpg)](using-the-colorpicker-control-extender-vb/_static/image7.png)</span></span>

<span data-ttu-id="55cca-141">**그림 04**: Extender 마법사로 컨트롤 extender를 선택 하면 ([전체 크기 이미지를 보려면 클릭](using-the-colorpicker-control-extender-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="55cca-141">**Figure 04**: Selecting a control extender with the Extender Wizard ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image8.png))</span></span>


<span data-ttu-id="55cca-142">ColorPicker extender ColorPicker 확장기에 텍스트 상자에 붙여넣습니다 txtCardColor 확장를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-142">You can pick the ColorPicker extender to extend the txtCardColor TextBox with the ColorPicker extender.</span></span> <span data-ttu-id="55cca-143">확인 대화 상자를 닫으려면 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-143">Click OK to close the dialog.</span></span>

<span data-ttu-id="55cca-144">이러한 변경을 수행한 후 페이지에 대 한 소스 목록 2와 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-144">After you make these changes, the source for the page looks like Listing 2.</span></span>

<span data-ttu-id="55cca-145">**2-(ColorPicker)와 CreateCard.aspx 나열**</span><span class="sxs-lookup"><span data-stu-id="55cca-145">**Listing 2 - CreateCard.aspx (with ColorPicker)**</span></span>

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample2.aspx)]

<span data-ttu-id="55cca-146">페이지 이제 txtCardColor TextBox 컨트롤 바로 아래에 나타나는 ColorPickerExtender 컨트롤에 포함 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-146">Notice that the page now contains a ColorPickerExtender control that appears directly below the txtCardColor TextBox control.</span></span> <span data-ttu-id="55cca-147">색 선택 대화 상자 표시 되도록 ColorPickerExtender 컨트롤 txtCardColor 컨트롤을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-147">The ColorPickerExtender control extends the txtCardColor control so that it displays a color picker dialog.</span></span>

## <a name="using-a-button-to-launch-the-color-picker-dialog"></a><span data-ttu-id="55cca-148">단추를 사용 하 여 색 선택 대화 상자를 시작 하려면</span><span class="sxs-lookup"><span data-stu-id="55cca-148">Using a Button to Launch the Color Picker Dialog</span></span>

<span data-ttu-id="55cca-149">ColorPicker extender는 다음 속성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-149">The ColorPicker extender supports the following properties:</span></span>

- <span data-ttu-id="55cca-150">PopupButtonId-단추의 색 선택 대화 상자를 표시 하는 페이지의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-150">PopupButtonId - The ID of a button on the page that causes the color picker dialog to appear.</span></span>
- <span data-ttu-id="55cca-151">PopupPosition-대상 컨트롤의 색 선택 대화 상자에 상대적인 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-151">PopupPosition - The position, relative to the target control, of the color picker dialog.</span></span> <span data-ttu-id="55cca-152">가능한 값에는 절대, 가운데, 왼쪽 맨 아래 오른쪽 맨 아래, 왼쪽 맨 위, 오른쪽, 오른쪽 맨 위 및 왼쪽 (기본값인 왼쪽 맨 아래)은 합니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-152">Possible values are Absolute, Center, BottomLeft, BottomRight, TopLeft, TopRight, Right, and Left (the default is BottomLeft).</span></span>
- <span data-ttu-id="55cca-153">SampleControlId-선택한 색을 표시 하는 컨트롤의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-153">SampleControlId - The ID of a control that displays the selected color.</span></span>
- <span data-ttu-id="55cca-154">SelectedColor-는 ColorPicker가 선택한 초기 색입니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-154">SelectedColor - The initial color selected by the ColorPicker.</span></span>

<span data-ttu-id="55cca-155">색 선택 대화 상자 표시 되는 방식 및 선택한 색 표시 되는 방식을 사용자 지정 하려면 이러한 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-155">You can use these properties to customize how the color picker dialog is displayed and how the selected color is displayed.</span></span> <span data-ttu-id="55cca-156">페이지 보기 3에서 이러한 속성 중 몇 가지를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-156">The page in Listing 3 illustrates how you can use several of these properties.</span></span>

<span data-ttu-id="55cca-157">**3-CreateCardButton.aspx 나열**</span><span class="sxs-lookup"><span data-stu-id="55cca-157">**Listing 3 - CreateCardButton.aspx**</span></span>

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample3.aspx)]

<span data-ttu-id="55cca-158">보기 3의 페이지에 색 선택 단추 (그림 5 참조).</span><span class="sxs-lookup"><span data-stu-id="55cca-158">The page in Listing 3 includes a Pick Color button (see Figure 5).</span></span> <span data-ttu-id="55cca-159">이 단추를 클릭 하 고 입력란 위 색 선택 대화 상자 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-159">When you click this button, the color picker dialog appears above the TextBox.</span></span> <span data-ttu-id="55cca-160">대화 상자에서 색을 선택 하면 선택한 색 lblSample 레이블 컨트롤의 배경색으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-160">If you select a color from the dialog then the selected color appears as the background color of the lblSample Label control.</span></span>

<span data-ttu-id="55cca-161">ColorPicker PopupButtonID 속성 ColorPicker 확장기에 색 선택 단추를 연결할 때 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-161">The ColorPicker PopupButtonID property is used to associate the Pick Color button with the ColorPicker extender.</span></span> <span data-ttu-id="55cca-162">PopupButtonID 속성에 대 한 값을 제공 하는 경우 대상 컨트롤에 포커스가 있을 때가 더 이상 색 선택 대화 상자에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-162">When you supply a value for the PopupButtonID property, the color picker dialog no longer appears when the target control has focus.</span></span> <span data-ttu-id="55cca-163">대화 상자를 표시 하려면 단추를 클릭 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-163">You must click the button to display the dialog.</span></span>

<span data-ttu-id="55cca-164">SampleControlID 속성은 ColorPicker와 선택한 색을 표시 하는 컨트롤을 연결할 때 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-164">The SampleControlID property is used to associate a control that displays the selected color with the ColorPicker.</span></span> <span data-ttu-id="55cca-165">ColorPicker 현재 선택 된 색이 컨트롤의 배경색을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-165">The ColorPicker changes the background color of this control to the currently selected color.</span></span>


<span data-ttu-id="55cca-166">[![단추 색 선택 대화 상자를 표시합니다.](using-the-colorpicker-control-extender-vb/_static/image5.jpg)](using-the-colorpicker-control-extender-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="55cca-166">[![Displaying the color picker dialog with a button](using-the-colorpicker-control-extender-vb/_static/image5.jpg)](using-the-colorpicker-control-extender-vb/_static/image9.png)</span></span>

<span data-ttu-id="55cca-167">**그림 05**: 단추 색 선택 대화 상자 표시 ([전체 크기 이미지를 보려면 클릭](using-the-colorpicker-control-extender-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="55cca-167">**Figure 05**: Displaying the color picker dialog with a button ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image10.png))</span></span>


## <a name="summary"></a><span data-ttu-id="55cca-168">요약</span><span class="sxs-lookup"><span data-stu-id="55cca-168">Summary</span></span>

<span data-ttu-id="55cca-169">이 자습서에서는 팝업 색 선택 대화 상자를 표시 하려면 ColorPicker 컨트롤 extender를 사용 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-169">In this tutorial, you learned how to use the ColorPicker control extender to display a popup color picker dialog.</span></span> <span data-ttu-id="55cca-170">첫째, TextBox 컨트롤에 포커스를 이동할 때 대화 상자에 표시 하는 방법을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-170">First, we examined how you can display the dialog when focus is moved to a TextBox control.</span></span> <span data-ttu-id="55cca-171">다음으로 단추를 클릭 하면 색 선택 대화 상자를 표시 하는 단추를 만드는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="55cca-171">Next, you learned how to create a button that displays the color picker dialog when the button is clicked.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="55cca-172">이전</span><span class="sxs-lookup"><span data-stu-id="55cca-172">Previous</span></span>](using-the-colorpicker-control-extender-cs.md)
