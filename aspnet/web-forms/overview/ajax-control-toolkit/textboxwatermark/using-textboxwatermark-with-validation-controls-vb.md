---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-vb
title: 유효성 검사 (VB) 컨트롤에 TextBoxWatermark 사용 | Microsoft Docs
author: wenz
description: AJAX Control Toolkit에서 TextBoxWatermark 컨트롤은 텍스트 상자 내에서 표시 되도록 입력란을 확장 합니다. 상자에 사용자가 클릭 하 고 있나요...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: e6c2cb98-f745-4bc8-973a-813879c8a891
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: 25a18bf4ad514fbeadd321f50d3b715b38d656cd
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37376580"
---
<a name="using-textboxwatermark-with-validation-controls-vb"></a><span data-ttu-id="95249-104">유효성 검사 (VB) 컨트롤에 TextBoxWatermark 사용</span><span class="sxs-lookup"><span data-stu-id="95249-104">Using TextBoxWatermark With Validation Controls (VB)</span></span>
====================
<span data-ttu-id="95249-105">[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="95249-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="95249-106">[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="95249-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2VB.pdf)</span></span>

> <span data-ttu-id="95249-107">AJAX Control Toolkit에서 TextBoxWatermark 컨트롤은 텍스트 상자 내에서 표시 되도록 입력란을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="95249-107">The TextBoxWatermark control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="95249-108">사용자가 상자에는 클릭, 비워집니다.</span><span class="sxs-lookup"><span data-stu-id="95249-108">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="95249-109">사용자는 텍스트를 입력 하지 않고 상자를 퇴사, 하는 경우에 미리 채워진된 텍스트 다시 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="95249-109">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="95249-110">이 동일한 페이지의 ASP.NET 유효성 검사 컨트롤 충돌할 수 있지만 이러한 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95249-110">This may collide with ASP.NET Validation Controls on the same page, but these issues may be overcome.</span></span>


## <a name="overview"></a><span data-ttu-id="95249-111">개요</span><span class="sxs-lookup"><span data-stu-id="95249-111">Overview</span></span>

<span data-ttu-id="95249-112">`TextBoxWatermark` AJAX Control Toolkit의 컨트롤을 텍스트 상자 내에서 표시 되도록 입력란을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="95249-112">The `TextBoxWatermark` control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="95249-113">사용자가 상자에는 클릭, 비워집니다.</span><span class="sxs-lookup"><span data-stu-id="95249-113">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="95249-114">사용자는 텍스트를 입력 하지 않고 상자를 퇴사, 하는 경우에 미리 채워진된 텍스트 다시 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="95249-114">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="95249-115">이 동일한 페이지의 ASP.NET 유효성 검사 컨트롤 충돌할 수 있지만 이러한 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95249-115">This may collide with ASP.NET Validation Controls on the same page, but these issues may be overcome.</span></span>

## <a name="steps"></a><span data-ttu-id="95249-116">단계</span><span class="sxs-lookup"><span data-stu-id="95249-116">Steps</span></span>

<span data-ttu-id="95249-117">샘플의 기본 설치는 다음:는 `TextBox` 제어를 사용 하 여 워터 마크 지정 되는 `TextBoxWatermarkExtender` 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="95249-117">The basic setup of the sample is the following: a `TextBox` control is watermarked using a `TextBoxWatermarkExtender` control.</span></span> <span data-ttu-id="95249-118">단추 포스트백을 트리거하고 나중에 트리거하는 데 사용할 페이지의 유효성 검사 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="95249-118">A button triggers a postback and will later be used to trigger the validation controls on the page.</span></span> <span data-ttu-id="95249-119">또한는 `ScriptManager` 컨트롤은 ASP.NET AJAX를 초기화 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95249-119">Also, a `ScriptManager` control is required to initialize ASP.NET AJAX:</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample1.aspx)]

<span data-ttu-id="95249-120">이제 추가 `RequiredFieldValidator` 있는지 텍스트 필드에는 양식이 제출 되 면 확인 하는 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="95249-120">Now add a `RequiredFieldValidator` control that checks whether there is text in the field when the form is submitted.</span></span> <span data-ttu-id="95249-121">합니다 `InitialValue` 유효성 검사기의 속성에 사용 되는 동일한 값으로 설정 해야 합니다는 `TextBoxWatermarkExtender` 컨트롤: 양식이 제출 되는 변경 되지 않은 텍스트의 값은 그 워터 마크 값을 합니다.</span><span class="sxs-lookup"><span data-stu-id="95249-121">The `InitialValue` property of the validator must be set to the same value that is used in the `TextBoxWatermarkExtender` control: When the form is submitted, the value of an unchanged textbox is the watermark value within it:</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample2.aspx)]

<span data-ttu-id="95249-122">그러나이 접근 방식의 한 가지 문제는: 클라이언트 JavaScript를 비활성화 하면, 텍스트 필드는 되지 않습니다 미리 채워진 워터 마크 텍스트를 따라서는 `RequiredFieldValidator` 오류 메시지를 트리거하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="95249-122">However there is one problem with this approach: If the client disables JavaScript, the text field is not prefilled with the watermark text, therefore the `RequiredFieldValidator` does not trigger an error message.</span></span> <span data-ttu-id="95249-123">따라서 두 번째 `RequiredFieldValidator` 컨트롤입니다. 필요한 빈 텍스트 상자에 대 한 확인 (생략 된 `InitialValue` 특성).</span><span class="sxs-lookup"><span data-stu-id="95249-123">Therefore, a second `RequiredFieldValidator` control is required which checks for an empty text box (omitting the `InitialValue` attribute).</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample3.aspx)]

<span data-ttu-id="95249-124">모두 유효성 검사기를 사용 하므로 `Display` = `"Dynamic"`, 최종 사용자는 두 유효성 검사기가 발생 하는 시각적 모양을에서 구분할 수 없습니다; 대신 것 같습니다. 둘 중 하나만 했습니다.</span><span class="sxs-lookup"><span data-stu-id="95249-124">Since both validators use `Display`=`"Dynamic"`, the end user cannot distinguish from the visual appearance which of the two validators was fired; instead, it looks like there was only one of them.</span></span>

<span data-ttu-id="95249-125">마지막으로, 없습니다 유효성 검사기 오류 메시지를 발급 하는 경우 필드의 텍스트를 출력 하도록 일부 서버 쪽 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="95249-125">Finally, add some server-side code to output the text in the field if no validator issued an error message:</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample4.aspx)]


<span data-ttu-id="95249-126">[![유효성 검사기에서 필드에 텍스트가 있는지](using-textboxwatermark-with-validation-controls-vb/_static/image2.png)](using-textboxwatermark-with-validation-controls-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="95249-126">[![The validator complains that there is no text in the field](using-textboxwatermark-with-validation-controls-vb/_static/image2.png)](using-textboxwatermark-with-validation-controls-vb/_static/image1.png)</span></span>

<span data-ttu-id="95249-127">유효성 검사기에서 필드에는 텍스트가 없습니다 있습니다 ([클릭 하 여 큰 이미지 보기](using-textboxwatermark-with-validation-controls-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="95249-127">The validator complains that there is no text in the field ([Click to view full-size image](using-textboxwatermark-with-validation-controls-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="95249-128">이전</span><span class="sxs-lookup"><span data-stu-id="95249-128">Previous</span></span>](using-textboxwatermark-in-a-formview-vb.md)
