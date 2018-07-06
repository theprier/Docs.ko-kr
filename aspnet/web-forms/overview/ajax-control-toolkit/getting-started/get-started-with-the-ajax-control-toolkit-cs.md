---
uid: web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
title: AJAX Control Toolkit (C#)를 사용 하 여 시작 | Microsoft Docs
author: microsoft
description: AJAX Control Toolkit를 사용 하 여 시작 하려면 알아야 할 모든에 대해 알아봅니다.
ms.author: aspnetcontent
ms.date: 05/12/2009
ms.assetid: 16dc5c11-65be-4eae-a818-9fad7f8259c6
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
msc.type: authoredcontent
ms.openlocfilehash: 3682af50eb2b9052ac0b15c2cec084deec10031d
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37832161"
---
<a name="get-started-with-the-ajax-control-toolkit-c"></a><span data-ttu-id="8f79d-103">AJAX Control Toolkit (C#)를 사용 하 여 시작</span><span class="sxs-lookup"><span data-stu-id="8f79d-103">Get Started with the AJAX Control Toolkit (C#)</span></span>
====================
<span data-ttu-id="8f79d-104">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="8f79d-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="8f79d-105">AJAX Control Toolkit를 사용 하 여 시작 하려면 알아야 할 모든에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8f79d-105">Learn all you need to know to get started using the AJAX Control Toolkit.</span></span>


<span data-ttu-id="8f79d-106">AJAX Control Toolkit에는 ASP.NET 응용 프로그램에서 사용할 수 있는 30 개 이상의 무료 컨트롤이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f79d-106">The AJAX Control Toolkit contains more than 30 free controls that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="8f79d-107">이 자습서에서는 AJAX Control Toolkit을 다운로드 하 고 Visual Studio/Visual Web Developer Express 도구 상자에 도구 키트 컨트롤을 추가 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8f79d-107">In this tutorial, you learn how to download the AJAX Control Toolkit and add the toolkit controls to your Visual Studio/Visual Web Developer Express toolbox.</span></span>

## <a name="downloading-the-ajax-control-toolkit"></a><span data-ttu-id="8f79d-108">AJAX Control Toolkit 다운로드</span><span class="sxs-lookup"><span data-stu-id="8f79d-108">Downloading the AJAX Control Toolkit</span></span>

<span data-ttu-id="8f79d-109">합니다 [AJAX Control Toolkit](http://devexpress.com/act) ASP.NET 커뮤니티 및 ASP.NET 팀 멤버에 의해 개발 된 오픈 소스 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="8f79d-109">The [AJAX Control Toolkit](http://devexpress.com/act) is an open source project developed by the members of the ASP.NET community and the ASP.NET team.</span></span> 


<span data-ttu-id="8f79d-110">[![AJAX Control Toolkit 다운로드](get-started-with-the-ajax-control-toolkit-cs/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8f79d-110">[![Downloading the AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-cs/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image1.png)</span></span>

<span data-ttu-id="8f79d-111">**그림 01**: AJAX Control Toolkit를 다운로드 ([큰 이미지를 보려면 클릭](get-started-with-the-ajax-control-toolkit-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="8f79d-111">**Figure 01**: Downloading the AJAX Control Toolkit([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image2.png))</span></span>


<span data-ttu-id="8f79d-112">파일을 다운로드 한 후에 파일의 차단을 해제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f79d-112">After you download the file, you need to unblock the file.</span></span> <span data-ttu-id="8f79d-113">파일, 속성을 선택 합니다. 마우스 오른쪽 단추로 클릭 합니다 **차단 해제** 단추 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="8f79d-113">Right-click the file, select Properties, and click the **Unblock** button (see Figure 2).</span></span>


<span data-ttu-id="8f79d-114">[![AJAX 컨트롤 도구 키트 ZIP 파일을 차단 해제](get-started-with-the-ajax-control-toolkit-cs/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="8f79d-114">[![Unblocking the AJAX Control Toolkit ZIP file](get-started-with-the-ajax-control-toolkit-cs/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image3.png)</span></span>

<span data-ttu-id="8f79d-115">**그림 02**: AJAX 컨트롤 도구 키트 ZIP 파일을 차단 해제 ([큰 이미지를 보려면 클릭](get-started-with-the-ajax-control-toolkit-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="8f79d-115">**Figure 02**: Unblocking the AJAX Control Toolkit ZIP file([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image4.png))</span></span>


<span data-ttu-id="8f79d-116">파일의 차단을 해제 한 후 압축 파일: 파일을 마우스 오른쪽 단추로 클릭 하 고 선택 합니다 **풀기** 메뉴 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="8f79d-116">After you unblock the file, you can unzip the file: Right-click the file and select the **Extract All** menu option.</span></span> <span data-ttu-id="8f79d-117">이제 Visual Studio/Visual Web Developer 도구 상자에 도구 키트를 추가할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8f79d-117">Now, we are ready to add the toolkit to the Visual Studio/Visual Web Developer toolbox.</span></span>

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a><span data-ttu-id="8f79d-118">AJAX Control Toolkit의 도구 상자에 추가</span><span class="sxs-lookup"><span data-stu-id="8f79d-118">Adding the AJAX Control Toolkit to the Toolbox</span></span>

<span data-ttu-id="8f79d-119">AJAX Control Toolkit을 사용 하는 가장 쉬운 방법은 Visual Studio/Visual Web Developer 도구 상자에 도구 키트를 추가 하는 것 (그림 3 참조).</span><span class="sxs-lookup"><span data-stu-id="8f79d-119">The easiest way to use the AJAX Control Toolkit is to add the toolkit to your Visual Studio/Visual Web Developer toolbox (see Figure 3).</span></span> <span data-ttu-id="8f79d-120">이런 방식으로 수 단순히 끌면 도구 키트 컨트롤 페이지를 사용 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="8f79d-120">That way, you can simply drag a toolkit control onto a page when you want to use it.</span></span>


<span data-ttu-id="8f79d-121">[![AJAX Control Toolkit 도구 상자에 표시 됩니다.](get-started-with-the-ajax-control-toolkit-cs/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="8f79d-121">[![AJAX Control Toolkit appears in toolbox](get-started-with-the-ajax-control-toolkit-cs/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image5.png)</span></span>

<span data-ttu-id="8f79d-122">**그림 03**: 도구 상자에 표시 되는 AJAX Control Toolkit ([큰 이미지를 보려면 클릭](get-started-with-the-ajax-control-toolkit-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="8f79d-122">**Figure 03**: AJAX Control Toolkit appears in toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image6.png))</span></span>


<span data-ttu-id="8f79d-123">첫째, 도구 상자에는 AJAX Control Toolkit 탭 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f79d-123">First, you need to add an AJAX Control Toolkit tab to the toolbox.</span></span> <span data-ttu-id="8f79d-124">다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f79d-124">Follow these steps.</span></span>

1. <span data-ttu-id="8f79d-125">메뉴 옵션 파일을 새 웹 사이트를 선택 하 여 새 ASP.NET 웹 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8f79d-125">Create a new ASP.NET Website by selecting the menu option File, New Website.</span></span> <span data-ttu-id="8f79d-126">편집기에서 파일을 열려면 솔루션 탐색기 창에서 Default.aspx를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f79d-126">Double-click the Default.aspx in the Solution Explorer window to open the file in the editor.</span></span>
2. <span data-ttu-id="8f79d-127">일반 탭 아래에 있는 도구 상자를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **추가 탭** (그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="8f79d-127">Right-click the Toolbox beneath the General Tab and select the menu option **Add Tab** (see Figure 4).</span></span>
3. <span data-ttu-id="8f79d-128">AJAX Control Toolkit 이라는 새 탭을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f79d-128">Enter a new tab named AJAX Control Toolkit.</span></span>


<span data-ttu-id="8f79d-129">[![새 탭 추가](get-started-with-the-ajax-control-toolkit-cs/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="8f79d-129">[![Adding a new tab](get-started-with-the-ajax-control-toolkit-cs/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image7.png)</span></span>

<span data-ttu-id="8f79d-130">**그림 04**: 새 탭 추가 ([큰 이미지를 보려면 클릭](get-started-with-the-ajax-control-toolkit-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="8f79d-130">**Figure 04**: Adding a new tab([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image8.png))</span></span>


<span data-ttu-id="8f79d-131">다음으로, 새 탭에는 AJAX Control Toolkit 컨트롤을 추가 해야 합니다. 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8f79d-131">Next, you need to add the AJAX Control Toolkit controls to the new tab. Follow these steps:</span></span>

- <span data-ttu-id="8f79d-132">AJAX Control Toolkit 탭 아래에 있는 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **(그림 5 참조)는 선택 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="8f79d-132">Right-click beneath the AJAX Control Toolkit tab and select the menu option **Choose Items (see Figure 5)**.</span></span>
- <span data-ttu-id="8f79d-133">위치로 이동 하는 AJAX Control Toolkit 압축을 해제 하 고 AjaxControlToolkit.dll 어셈블리를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f79d-133">Browse to the location where you unzipped the AJAX Control Toolkit and select the AjaxControlToolkit.dll assembly.</span></span>


<span data-ttu-id="8f79d-134">[![도구 상자에 추가할 항목 선택](get-started-with-the-ajax-control-toolkit-cs/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="8f79d-134">[![Choose items to add to the toolbox](get-started-with-the-ajax-control-toolkit-cs/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image9.png)</span></span>

<span data-ttu-id="8f79d-135">**그림 05**: 도구 상자에 추가할 항목 선택 ([큰 이미지를 보려면 클릭](get-started-with-the-ajax-control-toolkit-cs/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="8f79d-135">**Figure 05**: Choose items to add to the toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image10.png))</span></span>


<span data-ttu-id="8f79d-136">다음이 단계를 완료 한 후 도구 상자에는 모든 도구 키트 컨트롤이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="8f79d-136">After you complete these steps, all of the toolkit controls will appear in your toolbox.</span></span>

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a><span data-ttu-id="8f79d-137">도구 키트의 새 버전으로 업그레이드</span><span class="sxs-lookup"><span data-stu-id="8f79d-137">Upgrading to a New Version of the Toolkit</span></span>

<span data-ttu-id="8f79d-138">도구 키트의 이전 버전을 사용 하 고 이제 이동 해야 하는 경우 권장 되는 단계는 다음과 이상 버전.</span><span class="sxs-lookup"><span data-stu-id="8f79d-138">If you were using an older release of the Toolkit and now need to move to a later version here are the recommended steps:</span></span>

- <span data-ttu-id="8f79d-139">이진 파일-웹 사이트 Bin 폴더에서 AjaxControlToolkit.dll 어셈블리의 이전 버전을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f79d-139">Binaries - Delete the old version of the AjaxControlToolkit.dll assembly from your website Bin folder.</span></span>
- <span data-ttu-id="8f79d-140">도구 상자 항목-AJAX Control Toolkit 탭 삭제 및 다시 탭을 만드는 AjaxControlToolkit.dll 어셈블리의 새 버전을 사용 하 여 위의 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f79d-140">Toolbox Items - Delete the AJAX Control Toolkit tab and follow the steps above to re-create the tab with the new version of the AjaxControlToolkit.dll assembly.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="8f79d-141">다음</span><span class="sxs-lookup"><span data-stu-id="8f79d-141">Next</span></span>](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)
