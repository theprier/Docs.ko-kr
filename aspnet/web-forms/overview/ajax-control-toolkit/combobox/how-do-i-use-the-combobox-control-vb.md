---
uid: web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-vb
title: ComboBox 컨트롤을 사용 하는 방법 (VB) | Microsoft Docs
author: microsoft
description: 콤보 상자에 사용자가 선택할 수 있는 옵션의 목록을 사용 하 여 텍스트의 유연성을 결합 하는 ASP.NET AJAX 컨트롤입니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/12/2009
ms.topic: article
ms.assetid: e887e7b2-a6e7-4a28-a134-ba334494badb
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 3241641b3e136b24c8cff75026e496ddf8eb04ac
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37371910"
---
<a name="how-do-i-use-the-combobox-control-vb"></a><span data-ttu-id="92253-104">ComboBox 컨트롤을 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="92253-104">How do I use the ComboBox Control?</span></span> <span data-ttu-id="92253-105">(VB)</span><span class="sxs-lookup"><span data-stu-id="92253-105">(VB)</span></span>
====================
<span data-ttu-id="92253-106">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="92253-106">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="92253-107">콤보 상자에 사용자가 선택할 수 있는 옵션의 목록을 사용 하 여 텍스트의 유연성을 결합 하는 ASP.NET AJAX 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="92253-107">ComboBox is an ASP.NET AJAX control that combines the flexibility of a TextBox with a list of options from which users can choose.</span></span>


<span data-ttu-id="92253-108">이 자습서의 목표는 AJAX Control Toolkit ComboBox 컨트롤을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="92253-108">The goal of this tutorial is to explain the AJAX Control Toolkit ComboBox control.</span></span> <span data-ttu-id="92253-109">ComboBox는 표준 ASP.NET DropDownList 컨트롤과 TextBox 컨트롤 간의 조합 처럼 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="92253-109">The ComboBox works like a combination between a standard ASP.NET DropDownList control and a TextBox control.</span></span> <span data-ttu-id="92253-110">기존 항목 목록에서 선택 하거나 새 항목을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="92253-110">You can either select from a pre-existing list of items or enter a new item.</span></span>

<span data-ttu-id="92253-111">콤보 상자 자동 완성 컨트롤 extender 유사 하지만 컨트롤은 다양 한 시나리오에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92253-111">The ComboBox is similar to the AutoComplete control extender, but the controls are used in different scenarios.</span></span> <span data-ttu-id="92253-112">AutoComplete extender를 가져오도록 웹 서비스에 일치 하는 항목을 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="92253-112">The AutoComplete extender queries a web service to get matching entries.</span></span> <span data-ttu-id="92253-113">반면, 콤보 상자 컨트롤을 항목 집합을 사용 하 여 초기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92253-113">The ComboBox control, in contrast, is initialized with a set of items.</span></span> <span data-ttu-id="92253-114">AutoComplete extender는 사용 하 여 콤보 상자 컨트롤을 사용 하는 동안 다양 한 데이터 (자동차 부품의 수백만 개)를 사용 하 여 작업할 경우 적합 한 데이터의 작은 집합으로 작업 (자동차 부품의 수십 개).</span><span class="sxs-lookup"><span data-stu-id="92253-114">Using the AutoComplete extender makes sense when you are working with a large set of data (millions of car parts) while using the ComboBox control makes sense when working with a small set of data (dozens of car parts).</span></span>

## <a name="selecting-from-a-static-list-of-items"></a><span data-ttu-id="92253-115">항목의 정적 목록에서 선택</span><span class="sxs-lookup"><span data-stu-id="92253-115">Selecting from a Static List of Items</span></span>

<span data-ttu-id="92253-116">ComboBox 컨트롤을 사용 하는 간단한 예제 시작 s 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92253-116">Let�s start with a simple sample of using the ComboBox control.</span></span> <span data-ttu-id="92253-117">드롭다운 목록에서 항목 목록을 정적 표시 한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="92253-117">Imagine that you want to display a static list of items in a dropdown list.</span></span> <span data-ttu-id="92253-118">그러나 목록이 완성 되는 가능성 열어 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="92253-118">However, you want to leave open the possibility that the list is not complete.</span></span> <span data-ttu-id="92253-119">사용자 목록에 사용자 지정 값 입력을 허용 하려면.</span><span class="sxs-lookup"><span data-stu-id="92253-119">You want to allow a user to enter a custom value into the list.</span></span>

<span data-ttu-id="92253-120">에서는 ll 새 ASP.NET Web Forms 페이지를 만들고 페이지에서 ComboBox 컨트롤을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="92253-120">We�ll create a new ASP.NET Web Forms page and use the ComboBox control in the page.</span></span> <span data-ttu-id="92253-121">프로젝트에 새 ASP.NET 페이지를 추가 하 고 디자인 뷰로 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="92253-121">Add the new ASP.NET page to your project and switch to Design view.</span></span>

<span data-ttu-id="92253-122">페이지의 콤보 상자 컨트롤을 사용 하려는 경우 페이지에 ScriptManager 컨트롤을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="92253-122">If you want to use the ComboBox control in the page then you must add a ScriptManager control to the page.</span></span> <span data-ttu-id="92253-123">AJAX 확장명 탭 아래 ScriptManager 컨트롤을 디자이너 화면으로 끕니다.</span><span class="sxs-lookup"><span data-stu-id="92253-123">Drag the ScriptManager control from beneath the AJAX Extensions tab onto the Designer surface.</span></span> <span data-ttu-id="92253-124">페이지의 맨 위에 있는 ScriptManager 컨트롤을 추가 해야 즉시 열기 서버 쪽 아래에 추가할 수 있습니다 &lt;폼&gt; 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="92253-124">You should add the ScriptManager control at the top of the page; you can add it immediately below the opening server-side &lt;form&gt; tag.</span></span>

<span data-ttu-id="92253-125">그런 다음 ComboBox 컨트롤을 페이지로 끌어옵니다.</span><span class="sxs-lookup"><span data-stu-id="92253-125">Next, drag the ComboBox control onto the page.</span></span> <span data-ttu-id="92253-126">다른 AJAX Control Toolkit 컨트롤 및 컨트롤 extenders 사용 (그림 1 참조)를 사용 하 여 도구 상자에서 콤보 상자 컨트롤을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92253-126">You can find the ComboBox control in the Toolbox with the other AJAX Control Toolkit controls and control extenders (see figure1).</span></span>


<span data-ttu-id="92253-127">[![명함을 만들기 위한 간단한 폼](how-do-i-use-the-combobox-control-vb/_static/image1.jpg)](how-do-i-use-the-combobox-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="92253-127">[![Simple form for creating a business card](how-do-i-use-the-combobox-control-vb/_static/image1.jpg)](how-do-i-use-the-combobox-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="92253-128">**그림 01**: 도구 상자에서 콤보 상자 컨트롤을 선택 하면 ([큰 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="92253-128">**Figure 01**: Selecting the ComboBox control from the toolbox ([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image2.png))</span></span>


<span data-ttu-id="92253-129">에서는 ll ComboBox 컨트롤을 사용 하 여 선택 항목의 정적 목록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="92253-129">We�ll use the ComboBox control to display a static list of choices.</span></span> <span data-ttu-id="92253-130">사용자는 세 가지 선택 목록에서 특정 수준의 해당 음식에 대 한 spiciness 선택할 수 있습니다:가, 미디어 및 핫 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="92253-130">The user can select a particular level of spiciness for their food from a list of three choices: Mild, Medium, and Hot (see Figure 2).</span></span>


<span data-ttu-id="92253-131">[![항목의 정적 목록에서 선택](how-do-i-use-the-combobox-control-vb/_static/image2.jpg)](how-do-i-use-the-combobox-control-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="92253-131">[![Selecting from a static list of items](how-do-i-use-the-combobox-control-vb/_static/image2.jpg)](how-do-i-use-the-combobox-control-vb/_static/image3.png)</span></span>

<span data-ttu-id="92253-132">**그림 02**: 항목의 정적 목록에서 선택 ([큰 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="92253-132">**Figure 02**: Selecting from a static list of items([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image4.png))</span></span>


<span data-ttu-id="92253-133">두 가지 방법으로 이러한 선택 콤보 상자 컨트롤에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92253-133">There are two ways that you can add these choices to the ComboBox control.</span></span> <span data-ttu-id="92253-134">디자인 뷰에서 컨트롤을 마우스로 가리키면 옵션 편집 작업 옵션을 선택 및 항목 편집기를 열려면 먼저 (그림 3 참조).</span><span class="sxs-lookup"><span data-stu-id="92253-134">First, you select the Edit Options task option when hovering your mouse over the control in Design view and open the Item Editor (see Figure 3).</span></span>


<span data-ttu-id="92253-135">[![ComboBox 항목 편집](how-do-i-use-the-combobox-control-vb/_static/image3.jpg)](how-do-i-use-the-combobox-control-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="92253-135">[![Editing ComboBox items](how-do-i-use-the-combobox-control-vb/_static/image3.jpg)](how-do-i-use-the-combobox-control-vb/_static/image5.png)</span></span>

<span data-ttu-id="92253-136">**그림 03**: 콤보 상자 편집 항목 ([큰 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="92253-136">**Figure 03**: Editing ComboBox items([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image6.png))</span></span>


<span data-ttu-id="92253-137">두 번째 옵션은 열기 및 닫기 사이 항목 목록에 추가할 &lt;asp: 콤보 상자&gt; 소스 뷰에서 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="92253-137">The second option is to add the list of items in between the opening and closing &lt;asp:ComboBox&gt; tags in Source view.</span></span> <span data-ttu-id="92253-138">목록 1에서 페이지 항목 목록이 있는 업데이트 된 콤보 상자를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="92253-138">The page in Listing 1 contains the updated ComboBox that has the list of items.</span></span>

<span data-ttu-id="92253-139">**1-Static.aspx 나열**</span><span class="sxs-lookup"><span data-stu-id="92253-139">**Listing 1 - Static.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-combobox-control-vb/samples/sample1.aspx)]

<span data-ttu-id="92253-140">목록 1에서 페이지를 열면 콤보 상자에서 기존 옵션 중 하나를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92253-140">When you open the page in Listing 1, you can select one of the pre-existing options from the ComboBox.</span></span> <span data-ttu-id="92253-141">즉, ComboBox DropDownList 컨트롤과 마찬가지로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="92253-141">In other words, the ComboBox works just like a DropDownList control.</span></span>

<span data-ttu-id="92253-142">그러나 해야 하는 새 선택 (예를 들어, 슈퍼 매운) 기존 목록에 입력 하는 옵션.</span><span class="sxs-lookup"><span data-stu-id="92253-142">However, you also have the option of entering a new choice (for example, Super Spicy) that is not in the existing list.</span></span> <span data-ttu-id="92253-143">따라서 콤보 상자는 또한 TextBox 컨트롤 처럼 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="92253-143">So, the ComboBox also works like a TextBox control.</span></span>

<span data-ttu-id="92253-144">기존 선택 여부에 관계 없이 항목 또는 사용자 입력 항목을 사용자 지정 폼을 제출 하면 선택한 레이블 컨트롤에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92253-144">Regardless of whether you pick a pre-existing item or you enter a custom item, when you submit the form, your choice appears in the label control.</span></span> <span data-ttu-id="92253-145">btnSubmit 폼을 제출할 때\_클릭 처리기를 실행 하 고 레이블을 업데이트 합니다 (그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="92253-145">When you submit the form, the btnSubmit\_Click handler executes and updates the label (see Figure 4).</span></span>


<span data-ttu-id="92253-146">[![선택한 항목 표시](how-do-i-use-the-combobox-control-vb/_static/image4.jpg)](how-do-i-use-the-combobox-control-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="92253-146">[![Displaying the selected item](how-do-i-use-the-combobox-control-vb/_static/image4.jpg)](how-do-i-use-the-combobox-control-vb/_static/image7.png)</span></span>

<span data-ttu-id="92253-147">**그림 04**: 선택한 항목 표시 ([큰 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="92253-147">**Figure 04**: Displaying the selected item([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image8.png))</span></span>


<span data-ttu-id="92253-148">콤보 상자 폼 제출 되 면 선택한 항목을 검색 하기 위한 DropDownList 컨트롤과 같은 속성을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="92253-148">The ComboBox supports the same properties as the DropDownList control for retrieving the selected item after a form is submitted:</span></span>

- <span data-ttu-id="92253-149">SelectedItem.Text-선택한 항목의 Text 속성의 값을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="92253-149">SelectedItem.Text - Displays the value of the Text property of the selected item.</span></span>
- <span data-ttu-id="92253-150">SelectedItem.Value-선택한 항목의 Value 속성의 값 또는 콤보 상자에 입력 한 텍스트를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="92253-150">SelectedItem.Value - Displays the value of the Value property of the selected item or displays the text typed into the ComboBox.</span></span>
- <span data-ttu-id="92253-151">SelectedValue-동일 하지만 SelectedItem.Value이이 속성을 사용 하면 기본 (초기) 선택된 항목을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92253-151">SelectedValue - Same as SelectedItem.Value except that this property enables you to specify the default (initial) selected item.</span></span>

<span data-ttu-id="92253-152">입력 한 다음 사용자 지정 선택 콤보 상자에 사용자 지정 선택 SelectedItem.Text와 SelectedItem.Value 속성에 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92253-152">If you type a custom choice into the ComboBox then the custom choice is assigned to both the SelectedItem.Text and SelectedItem.Value properties.</span></span>

## <a name="selecting-the-list-of-items-from-the-database"></a><span data-ttu-id="92253-153">데이터베이스에서 항목 목록을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="92253-153">Selecting the List of Items from the Database</span></span>

<span data-ttu-id="92253-154">데이터베이스에서 콤보 상자를 표시 하는 항목 목록을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92253-154">You can retrieve the list of items that the ComboBox displays from a database.</span></span> <span data-ttu-id="92253-155">예를 들어, SqlDataSource 컨트롤, ObjectDataSource 컨트롤, LinqDataSource, 또는 EntityDataSource ComboBox를 바인딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92253-155">For example, you can bind the ComboBox to a SqlDataSource control, an ObjectDataSource control, a LinqDataSource, or an EntityDataSource.</span></span>

<span data-ttu-id="92253-156">ComboBox에 동영상 목록을 표시할 한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="92253-156">Imagine that you want to display a list of movies in a ComboBox.</span></span> <span data-ttu-id="92253-157">영화 목록에 영화 데이터베이스 테이블에서 검색 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="92253-157">You want to retrieve the list of movies from the Movies database table.</span></span> <span data-ttu-id="92253-158">아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="92253-158">Follow these steps:</span></span>

1. <span data-ttu-id="92253-159">Movies.aspx 라는 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="92253-159">Create a page named Movies.aspx</span></span>
2. <span data-ttu-id="92253-160">AJAX 확장명 탭에서 ScriptManager 페이지 도구 상자에서 끌어 페이지에 ScriptManager 컨트롤을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="92253-160">Add a ScriptManager control to the page by dragging the ScriptManager from under the AJAX Extensions tab in the Toolbox onto the page.</span></span>
3. <span data-ttu-id="92253-161">콤보 상자를 페이지로 끌어 페이지에는 ComboBox 컨트롤을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="92253-161">Add a ComboBox control to the page by dragging the ComboBox onto the page.</span></span>
4. <span data-ttu-id="92253-162">선택한 디자인 뷰에서 ComboBox 컨트롤 위로 마우스를 가져가서 합니다 **데이터 소스 선택** 작업 옵션 (그림 5 참조).</span><span class="sxs-lookup"><span data-stu-id="92253-162">In Design view, hover your mouse over the ComboBox control and select the **Choose Data Source** task option (see Figure 5).</span></span> <span data-ttu-id="92253-163">데이터 소스 구성 마법사가 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92253-163">The Data Source Configuration Wizard is launched.</span></span>
5. <span data-ttu-id="92253-164">에 **데이터 원본을 선택** 단계를 선택 합니다 &lt;새 데이터 원본을&gt; 옵션.</span><span class="sxs-lookup"><span data-stu-id="92253-164">In the **Choose a Data Source** step, select the &lt;New data source�&gt; option.</span></span>
6. <span data-ttu-id="92253-165">에 **데이터 소스 형식 선택** 단계에서 데이터베이스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="92253-165">In the **Choose a Data Source Type** step, select Database.</span></span>
7. <span data-ttu-id="92253-166">에 **데이터 연결 선택** 단계 (예를 들어 MoviesDB.mdf) 데이터베이스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="92253-166">In the **Choose Your Data Connection** step, select your database (for example, MoviesDB.mdf).</span></span>
8. <span data-ttu-id="92253-167">에 **응용 프로그램 구성 파일에 연결 문자열 저장** 단계, 연결 문자열을 저장 하는 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="92253-167">In the **Save the Connection String to the Application Configuration File** step, select the option to save your connection string.</span></span>
9. <span data-ttu-id="92253-168">에 **Select 문 구성** 단계 영화 데이터베이스 테이블을 선택 하 고 모든 열을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="92253-168">In the **Configure the Select Statement** step, select the Movies database table and select all of the columns.</span></span>
10. <span data-ttu-id="92253-169">에 **테스트 쿼리** 단계, "마침" 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="92253-169">In the **Test Query** step, click the Finish button.</span></span>
11. <span data-ttu-id="92253-170">에 **데이터 소스 선택** 단계 선택 표시할 필드에 대 한 제목 열 및 데이터에 대 한 Id 열 필드 (그림 참조).</span><span class="sxs-lookup"><span data-stu-id="92253-170">Back in the **Choose Data Source** step, select the Title column for the field to display and the Id column for the data field (see Figure).</span></span>
12. <span data-ttu-id="92253-171">마법사를 닫으려면 확인 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="92253-171">Click the OK button to close the wizard.</span></span>


<span data-ttu-id="92253-172">[![데이터 원본 선택](how-do-i-use-the-combobox-control-vb/_static/image5.jpg)](how-do-i-use-the-combobox-control-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="92253-172">[![Choosing a data source](how-do-i-use-the-combobox-control-vb/_static/image5.jpg)](how-do-i-use-the-combobox-control-vb/_static/image9.png)</span></span>

<span data-ttu-id="92253-173">**그림 05**: 데이터 원본 선택 ([큰 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="92253-173">**Figure 05**: Choosing a data source([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image10.png))</span></span>


<span data-ttu-id="92253-174">[![데이터 값 및 텍스트 필드를 선택합니다.](how-do-i-use-the-combobox-control-vb/_static/image6.jpg)](how-do-i-use-the-combobox-control-vb/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="92253-174">[![Choosing the data text and value fields](how-do-i-use-the-combobox-control-vb/_static/image6.jpg)](how-do-i-use-the-combobox-control-vb/_static/image11.png)</span></span>

<span data-ttu-id="92253-175">**그림 06**: 데이터 값 및 텍스트 필드를 선택 ([큰 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-vb/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="92253-175">**Figure 06**: Choosing the data text and value fields([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image12.png))</span></span>


<span data-ttu-id="92253-176">위의 단계를 완료 한 후에 콤보 상자 영화 데이터베이스 테이블에서 영화를 나타내는 SqlDataSource 컨트롤에 바인딩되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92253-176">After you complete the steps above, the ComboBox is bound to a SqlDataSource control that represents the movies from the Movies database table.</span></span> <span data-ttu-id="92253-177">페이지에 대 한 원본 (I 정리 서식을 약간) 목록 2와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="92253-177">The source for the page looks like Listing 2 (I cleaned up the formatting a little bit).</span></span>

<span data-ttu-id="92253-178">**2-Movies.aspx 나열**</span><span class="sxs-lookup"><span data-stu-id="92253-178">**Listing 2 - Movies.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-combobox-control-vb/samples/sample2.aspx)]

<span data-ttu-id="92253-179">ComboBox 컨트롤에 SqlDataSource 컨트롤을 가리키는 DataSourceID 속성이 있음을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92253-179">Notice that the ComboBox control has a DataSourceID property that points to the SqlDataSource control.</span></span> <span data-ttu-id="92253-180">브라우저에서 페이지를 열 때 데이터베이스에서 영화 목록에 표시 됩니다 (그림 7 참조).</span><span class="sxs-lookup"><span data-stu-id="92253-180">When you open the page in a browser, the list of movies from the database is displayed (see Figure 7).</span></span> <span data-ttu-id="92253-181">선택 목록에서 동영상을 수 있습니다 또는 동영상 콤보 상자에 입력 하 여 새 동영상을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="92253-181">You can either a pick a movie from the list or enter a new movie by typing the movie into the ComboBox.</span></span>


<span data-ttu-id="92253-182">[![동영상 목록을 표시합니다.](how-do-i-use-the-combobox-control-vb/_static/image7.jpg)](how-do-i-use-the-combobox-control-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="92253-182">[![Displaying a list of movies](how-do-i-use-the-combobox-control-vb/_static/image7.jpg)](how-do-i-use-the-combobox-control-vb/_static/image13.png)</span></span>

<span data-ttu-id="92253-183">**그림 07**: 영화 목록 표시 ([큰 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-vb/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="92253-183">**Figure 07**: Displaying a list of movies([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image14.png))</span></span>


## <a name="setting-the-dropdownstyle"></a><span data-ttu-id="92253-184">dropdownstyle은 설정</span><span class="sxs-lookup"><span data-stu-id="92253-184">Setting the DropDownStyle</span></span>

<span data-ttu-id="92253-185">ComboBox의 동작을 변경 하려면 ComboBox dropdownstyle은 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92253-185">You can use the ComboBox DropDownStyle property to change the behavior of the ComboBox.</span></span> <span data-ttu-id="92253-186">이 속성은 있는 허용 가능한 값:</span><span class="sxs-lookup"><span data-stu-id="92253-186">This property accepts there possible values:</span></span>

- <span data-ttu-id="92253-187">드롭다운-드롭다운 화살표를 클릭할 때 목록 (기본값)은 ComboBox 표시 사용자 지정 값을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92253-187">DropDown - (default value) The ComboBox displays a dropdown list when you click the arrow and you can enter a custom value.</span></span>
- <span data-ttu-id="92253-188">단순-콤보 상자 드롭다운 목록을 자동으로 표시 되 고 사용자 지정 값을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92253-188">Simple - The ComboBox displays a dropdown list automatically and you can enter a custom value.</span></span>
- <span data-ttu-id="92253-189">DropDownList-ComboBox DropDownList 컨트롤과 마찬가지로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="92253-189">DropDownList - The ComboBox works just like a DropDownList control.</span></span>

<span data-ttu-id="92253-190">다른 드롭다운 사이 고 간단한 경우 항목의 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92253-190">The different between DropDown and Simple is when the list of items is displayed.</span></span> <span data-ttu-id="92253-191">간단한 경우 ComboBox에 포커스를 이동 하는 즉시 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92253-191">In the case of Simple, the list is displayed immediately when you move focus to the ComboBox.</span></span> <span data-ttu-id="92253-192">드롭다운의 경우 항목의 목록을 보려면 화살표를 클릭 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="92253-192">In the case of DropDown, you must click the arrow to see the list of items.</span></span>

<span data-ttu-id="92253-193">DropDownList 값 콤보 상자 컨트롤을 표준 DropDownList 컨트롤 처럼 사용 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92253-193">The DropDownList value causes the ComboBox control to work just like a standard DropDownList control.</span></span> <span data-ttu-id="92253-194">그러나 여기서 중요 한 차이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92253-194">However, there is an important difference here.</span></span> <span data-ttu-id="92253-195">이전 버전의 Internet Explorer 컨트롤 앞에 배치 되는 모든 컨트롤 앞에 나타납니다. 무한 z-인덱스를 사용 하 여 DropDownList 컨트롤을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="92253-195">Older versions of Internet Explorer display a DropDownList control with an infinite z-index so the control will appear in front of any control placed in front of it.</span></span> <span data-ttu-id="92253-196">콤보 상자의 HTML을 렌더링 하기 때문에 &lt;div&gt; HTML 대신 태그 &lt;선택&gt; 태그 ComboBox 올바르게는 z 순서입니다.</span><span class="sxs-lookup"><span data-stu-id="92253-196">Because the ComboBox renders an HTML &lt;div&gt; tag instead of an HTML &lt;select&gt; tag, the ComboBox correctly respects z-ordering.</span></span>

## <a name="setting-the-autocompletemode"></a><span data-ttu-id="92253-197">AutoCompleteMode 설정</span><span class="sxs-lookup"><span data-stu-id="92253-197">Setting the AutoCompleteMode</span></span>

<span data-ttu-id="92253-198">콤보 상자 AutoCompleteMode 속성을 사용 하 여 콤보 상자에 텍스트를 입력할 때 적용할 결과 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="92253-198">You use the ComboBox AutoCompleteMode property to specify what happens when someone types text into the ComboBox.</span></span> <span data-ttu-id="92253-199">이 속성은 다음의 가능한 값을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="92253-199">This property accepts the following possible values:</span></span>

- <span data-ttu-id="92253-200">None-(기본값) 콤보 상자는 자동 완성 동작을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="92253-200">None - (default value) The ComboBox does not provide any auto-complete behavior.</span></span>
- <span data-ttu-id="92253-201">제안-콤보 상자 목록을 표시 하 고 목록에서 일치 하는 항목 강조 표시 (그림 8 참조).</span><span class="sxs-lookup"><span data-stu-id="92253-201">Suggest - The ComboBox displays the list and it highlights the matching item in the list (see Figure 8).</span></span>
- <span data-ttu-id="92253-202">추가-콤보 상자 목록 표시 되지 않습니다 하 고 목록에서 입력 한 (그림 9 참조)으로 일치 하는 항목을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="92253-202">Append - The ComboBox does not display the list and it appends the matching item from the list onto what you have typed (see Figure 9).</span></span>
- <span data-ttu-id="92253-203">SuggestAppend-콤보 상자 목록 표시 및 입력 한 (그림 10 참조) 목록에서 일치 하는 항목을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="92253-203">SuggestAppend - The ComboBox both displays the list and appends the matching item from the list onto what you have typed (see Figure 10).</span></span>


<span data-ttu-id="92253-204">[![콤보 상자는 제안](how-do-i-use-the-combobox-control-vb/_static/image8.jpg)](how-do-i-use-the-combobox-control-vb/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="92253-204">[![The ComboBox makes a suggestion](how-do-i-use-the-combobox-control-vb/_static/image8.jpg)](how-do-i-use-the-combobox-control-vb/_static/image15.png)</span></span>

<span data-ttu-id="92253-205">**그림 08**: The 콤보 상자는 제안 ([큰 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-vb/_static/image16.png))</span><span class="sxs-lookup"><span data-stu-id="92253-205">**Figure 08**: The ComboBox makes a suggestion([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image16.png))</span></span>


<span data-ttu-id="92253-206">[![일치 하는 텍스트를 추가 하는 콤보 상자](how-do-i-use-the-combobox-control-vb/_static/image9.jpg)](how-do-i-use-the-combobox-control-vb/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="92253-206">[![ComboBox appends matching text](how-do-i-use-the-combobox-control-vb/_static/image9.jpg)](how-do-i-use-the-combobox-control-vb/_static/image17.png)</span></span>

<span data-ttu-id="92253-207">**그림 09**: 일치 하는 텍스트를 추가 하는 콤보 상자 ([큰 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-vb/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="92253-207">**Figure 09**: ComboBox appends matching text([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image18.png))</span></span>


<span data-ttu-id="92253-208">[![콤보 상자에서 제안 하 고 추가](how-do-i-use-the-combobox-control-vb/_static/image10.jpg)](how-do-i-use-the-combobox-control-vb/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="92253-208">[![The ComboBox suggests and appends](how-do-i-use-the-combobox-control-vb/_static/image10.jpg)](how-do-i-use-the-combobox-control-vb/_static/image19.png)</span></span>

<span data-ttu-id="92253-209">**그림 10**: The 콤보 상자에서 제안 하 고 추가 ([큰 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-vb/_static/image20.png))</span><span class="sxs-lookup"><span data-stu-id="92253-209">**Figure 10**: The ComboBox suggests and appends([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image20.png))</span></span>


## <a name="summary"></a><span data-ttu-id="92253-210">요약</span><span class="sxs-lookup"><span data-stu-id="92253-210">Summary</span></span>

<span data-ttu-id="92253-211">이 자습서에서는 ComboBox 컨트롤을 사용 하 여 고정된 된 항목 집합을 표시 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="92253-211">In this tutorial, you learned how to use the ComboBox control to display a fixed set of items.</span></span> <span data-ttu-id="92253-212">에서는 ComboBox 컨트롤을 정적 항목 집합을 데이터베이스 테이블에 모두 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="92253-212">We bound the ComboBox control both to a static set of items and to a database table.</span></span> <span data-ttu-id="92253-213">마지막으로, 해당 dropdownstyle 및 AutoCompleteMode 속성을 설정 하 여 ComboBox의 동작을 수정 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="92253-213">Finally, you learned how to modify the behavior of the ComboBox by setting its DropDownStyle and AutoCompleteMode properties.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="92253-214">이전</span><span class="sxs-lookup"><span data-stu-id="92253-214">Previous</span></span>](how-do-i-use-the-combobox-control-cs.md)
