---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-cs
title: "유효성 검사 컨트롤 (C#) TextBoxWatermark 사용 | Microsoft Docs"
author: wenz
description: "들어에서 TextBoxWatermark 컨트롤 텍스트 상자 내에서 표시 되도록 입력란을 확장 합니다. 상자에는 사용자가 클릭할 때 그 i..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: d49940cb-d38c-456a-b800-5f0eb705d09f
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-cs
msc.type: authoredcontent
ms.openlocfilehash: 61fa55c8c4580800de1097b7242c7077cda27115
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="using-textboxwatermark-with-validation-controls-c"></a><span data-ttu-id="3e690-104">TextBoxWatermark를 사용 하 여 유효성 검사 컨트롤 (C#)</span><span class="sxs-lookup"><span data-stu-id="3e690-104">Using TextBoxWatermark With Validation Controls (C#)</span></span>
====================
<span data-ttu-id="3e690-105">으로 [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="3e690-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="3e690-106">[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="3e690-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2CS.pdf)</span></span>

> <span data-ttu-id="3e690-107">들어에서 TextBoxWatermark 컨트롤 텍스트 상자 내에서 표시 되도록 입력란을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e690-107">The TextBoxWatermark control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="3e690-108">상자에 사용자가 클릭, 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e690-108">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="3e690-109">사용자가 상자 텍스트를 입력 하지 않고를 완료 하는 경우에 미리 채워진된 텍스트 다시 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="3e690-109">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="3e690-110">ASP.NET 유효성 검사 컨트롤 같은 페이지에이 충돌할 수 있습니다 하지만 이러한 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e690-110">This may collide with ASP.NET Validation Controls on the same page, but these issues may be overcome.</span></span>


## <a name="overview"></a><span data-ttu-id="3e690-111">개요</span><span class="sxs-lookup"><span data-stu-id="3e690-111">Overview</span></span>

<span data-ttu-id="3e690-112">`TextBoxWatermark` 들어에서 컨트롤 텍스트 상자 내에서 표시 되도록 입력란을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e690-112">The `TextBoxWatermark` control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="3e690-113">상자에 사용자가 클릭, 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e690-113">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="3e690-114">사용자가 상자 텍스트를 입력 하지 않고를 완료 하는 경우에 미리 채워진된 텍스트 다시 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="3e690-114">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="3e690-115">ASP.NET 유효성 검사 컨트롤 같은 페이지에이 충돌할 수 있습니다 하지만 이러한 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e690-115">This may collide with ASP.NET Validation Controls on the same page, but these issues may be overcome.</span></span>

## <a name="steps"></a><span data-ttu-id="3e690-116">단계</span><span class="sxs-lookup"><span data-stu-id="3e690-116">Steps</span></span>

<span data-ttu-id="3e690-117">샘플의 기본 설정에는 다음과 같습니다:는 `TextBox` 제어를 사용 하 여 워터은 `TextBoxWatermarkExtender` 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e690-117">The basic setup of the sample is the following: a `TextBox` control is watermarked using a `TextBoxWatermarkExtender` control.</span></span> <span data-ttu-id="3e690-118">다시 게시를 트리거한 다음 단추는 나중에 트리거하는 데 사용할 페이지에서 유효성 검사 컨트롤.</span><span class="sxs-lookup"><span data-stu-id="3e690-118">A button triggers a postback and will later be used to trigger the validation controls on the page.</span></span> <span data-ttu-id="3e690-119">또한 한 `ScriptManager` 컨트롤은 ASP.NET AJAX를 초기화 하는 데 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e690-119">Also, a `ScriptManager` control is required to initialize ASP.NET AJAX:</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample1.aspx)]

<span data-ttu-id="3e690-120">이제 추가 `RequiredFieldValidator` 있는지 여부를 확인 텍스트 필드에 폼이 전송 될 때 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e690-120">Now add a `RequiredFieldValidator` control that checks whether there is text in the field when the form is submitted.</span></span> <span data-ttu-id="3e690-121">`InitialValue` 유효성 검사기의 속성에 사용 되는 동일한 값으로 설정 해야 합니다는 `TextBoxWatermarkExtender` 제어: 폼이 전송 변경 되지 않은 입력란의 값은 그 안에 워터 마크 값:</span><span class="sxs-lookup"><span data-stu-id="3e690-121">The `InitialValue` property of the validator must be set to the same value that is used in the `TextBoxWatermarkExtender` control: When the form is submitted, the value of an unchanged textbox is the watermark value within it:</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample2.aspx)]

<span data-ttu-id="3e690-122">그러나이 방법을 사용 하는 한 가지 문제는: 클라이언트는 JavaScript를 비활성화, 텍스트 필드 하지 미리 채워지는 워터 마크 텍스트로 따라서는 `RequiredFieldValidator` 오류 메시지를 트리거하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3e690-122">However there is one problem with this approach: If the client disables JavaScript, the text field is not prefilled with the watermark text, therefore the `RequiredFieldValidator` does not trigger an error message.</span></span> <span data-ttu-id="3e690-123">따라서 두 번째 `RequiredFieldValidator` 컨트롤입니다. 필요한 빈 텍스트 상자에 대 한 확인 (생략 된 `InitialValue` 특성).</span><span class="sxs-lookup"><span data-stu-id="3e690-123">Therefore, a second `RequiredFieldValidator` control is required which checks for an empty text box (omitting the `InitialValue` attribute).</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample3.aspx)]

<span data-ttu-id="3e690-124">두 유효성 검사기를 사용 하므로 `Display` = `"Dynamic"`, 최종 사용자는 두 명의 유효성 검사기 중 어떤 발생 시각적 모양에서 구분할 수 없습니다; 대신, 것 같습니다. 둘 중 하나만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e690-124">Since both validators use `Display`=`"Dynamic"`, the end user cannot distinguish from the visual appearance which of the two validators was fired; instead, it looks like there was only one of them.</span></span>

<span data-ttu-id="3e690-125">마지막으로 없는 유효성 검사기는 오류 메시지를 발급 하는 경우 필드의 텍스트를 출력 하는 서버 쪽 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e690-125">Finally, add some server-side code to output the text in the field if no validator issued an error message:</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample4.aspx)]


<span data-ttu-id="3e690-126">[![유효성 검사기 불만 없는 텍스트 필드에 있다는 것을 표시합니다](using-textboxwatermark-with-validation-controls-cs/_static/image2.png)](using-textboxwatermark-with-validation-controls-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3e690-126">[![The validator complains that there is no text in the field](using-textboxwatermark-with-validation-controls-cs/_static/image2.png)](using-textboxwatermark-with-validation-controls-cs/_static/image1.png)</span></span>

<span data-ttu-id="3e690-127">유효성 검사기 필드에 텍스트가 불만 ([전체 크기 이미지를 보려면 클릭](using-textboxwatermark-with-validation-controls-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="3e690-127">The validator complains that there is no text in the field ([Click to view full-size image](using-textboxwatermark-with-validation-controls-cs/_static/image3.png))</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="3e690-128">[이전](using-textboxwatermark-in-a-formview-cs.md)
[다음](using-textboxwatermark-in-a-formview-vb.md)</span><span class="sxs-lookup"><span data-stu-id="3e690-128">[Previous](using-textboxwatermark-in-a-formview-cs.md)
[Next](using-textboxwatermark-in-a-formview-vb.md)</span></span>
