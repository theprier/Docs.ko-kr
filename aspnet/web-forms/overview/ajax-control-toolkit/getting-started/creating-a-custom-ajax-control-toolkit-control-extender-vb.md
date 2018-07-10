---
uid: web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-vb
title: 도구 키트 컨트롤 Extender (VB)를 제어 하는 사용자 지정 AJAX 만들기 | Microsoft Docs
author: microsoft
description: 사용자 지정 Extender를 사용 하 여 사용자 지정 하 고 새 클래스를 만들 필요 없이 ASP.NET 컨트롤의 기능을 확장할 수 있습니다.
ms.author: aspnetcontent
ms.date: 05/12/2009
ms.assetid: 18b29834-c991-4e0c-b533-44d358fbfc9c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-vb
msc.type: authoredcontent
ms.openlocfilehash: b44918cff161088e98f7baaca7714348b0b6a8de
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37814620"
---
<a name="creating-a-custom-ajax-control-toolkit-control-extender-vb"></a><span data-ttu-id="4eb61-103">사용자 지정 AJAX 컨트롤 도구 키트 컨트롤 Extender (VB) 만들기</span><span class="sxs-lookup"><span data-stu-id="4eb61-103">Creating a Custom AJAX Control Toolkit Control Extender (VB)</span></span>
====================
<span data-ttu-id="4eb61-104">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="4eb61-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="4eb61-105">사용자 지정 Extender를 사용 하 여 사용자 지정 하 고 새 클래스를 만들 필요 없이 ASP.NET 컨트롤의 기능을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-105">Custom Extenders enable you to customize and extend the capabilities of ASP.NET controls without having to create new classes.</span></span>


<span data-ttu-id="4eb61-106">이 자습서에서는 사용자 지정 AJAX 컨트롤 도구 키트 컨트롤 extender를 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-106">In this tutorial, you learn how to create a custom AJAX Control Toolkit control extender.</span></span> <span data-ttu-id="4eb61-107">텍스트 상자에 텍스트를 입력할 때 사용 안 함 상태에서 단추의 상태를 변경 하는 extender 유용 하 고 새 하지만 단순 하 고 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-107">We create a simple, but useful, new extender that changes the state of a Button from disabled to enabled when you type text into a TextBox.</span></span> <span data-ttu-id="4eb61-108">이 자습서를 읽은 후 사용자 고유의 컨트롤 extender 사용 하 여 ASP.NET AJAX Toolkit를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-108">After reading this tutorial, you will be able to extend the ASP.NET AJAX Toolkit with your own control extenders.</span></span>

<span data-ttu-id="4eb61-109">Visual Studio 또는 Visual Web Developer를 사용 하 여 사용자 지정 컨트롤 extender를 만들 수 있습니다 (Visual Web Developer의 최신 버전이 있는지 확인).</span><span class="sxs-lookup"><span data-stu-id="4eb61-109">You can create custom control extenders using either Visual Studio or Visual Web Developer (make sure that you have the latest version of Visual Web Developer).</span></span>

## <a name="overview-of-the-disabledbutton-extender"></a><span data-ttu-id="4eb61-110">DisabledButton Extender의 개요</span><span class="sxs-lookup"><span data-stu-id="4eb61-110">Overview of the DisabledButton Extender</span></span>

<span data-ttu-id="4eb61-111">이 새 컨트롤 extender DisabledButton extender를 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-111">Our new control extender is named the DisabledButton extender.</span></span> <span data-ttu-id="4eb61-112">이 extender에는 세 가지 속성이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-112">This extender will have three properties:</span></span>

- <span data-ttu-id="4eb61-113">TargetControlID-컨트롤을 확장 하는 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-113">TargetControlID - The TextBox that the control extends.</span></span>
- <span data-ttu-id="4eb61-114">TargetButtonIID-단추를 비활성화 하거나 활성화입니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-114">TargetButtonIID - The Button that is disabled or enabled.</span></span>
- <span data-ttu-id="4eb61-115">DisabledText-단추를 처음 표시 되는 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-115">DisabledText - The text that is initially displayed in the Button.</span></span> <span data-ttu-id="4eb61-116">입력을 시작 하는 경우 단추 텍스트 속성의 값을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-116">When you start typing, the Button displays the value of the Button Text property.</span></span>

<span data-ttu-id="4eb61-117">TextBox와 Button 컨트롤에 DisabledButton extender에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-117">You hook the DisabledButton extender to a TextBox and Button control.</span></span> <span data-ttu-id="4eb61-118">모든 텍스트를 입력 하기 전에 단추가 비활성화 되 고 TextBox와 Button 다음과 같이 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-118">Before you type any text, the Button is disabled and the TextBox and Button look like this:</span></span>


[![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image2.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image1.png)

<span data-ttu-id="4eb61-119">([클릭 하 여 큰 이미지 보기](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="4eb61-119">([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image3.png))</span></span>


<span data-ttu-id="4eb61-120">텍스트 입력을 시작 하면이 단추가 활성화 됩니다 후 TextBox와 Button 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-120">After you start typing text, the Button is enabled and the TextBox and Button look like this:</span></span>


[![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image5.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image4.png)

<span data-ttu-id="4eb61-121">([클릭 하 여 큰 이미지 보기](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="4eb61-121">([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image6.png))</span></span>


<span data-ttu-id="4eb61-122">이 컨트롤 extender를 만들려면 다음 세 가지 파일을 만드는 데 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-122">To create our control extender, we need to create the following three files:</span></span>

- <span data-ttu-id="4eb61-123">DisabledButtonExtender.vb-이 파일은 프로그램 extender 만들기 관리 되며 디자인 타임에 속성을 설정할 수 있도록 하는 서버 쪽 컨트롤 클래스.</span><span class="sxs-lookup"><span data-stu-id="4eb61-123">DisabledButtonExtender.vb - This file is the server-side control class that will manage creating your extender and allow you to set the properties at design-time.</span></span> <span data-ttu-id="4eb61-124">또한 extender의 설정할 수 있는 속성을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-124">It also defines the properties that can be set on your extender.</span></span> <span data-ttu-id="4eb61-125">이러한 속성은 코드를 통해 및 디자인 타임에 액세스할 수 및 DisableButtonBehavior.js 파일에 정의 된 속성과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-125">These properties are accessible via code and at design time and match properties defined in the DisableButtonBehavior.js file.</span></span>
- <span data-ttu-id="4eb61-126">DisabledButtonBehavior.js-이 파일은 모든 클라이언트 스크립트 논리에 추가할 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-126">DisabledButtonBehavior.js -- This file is where you will add all of your client script logic.</span></span>
- <span data-ttu-id="4eb61-127">DisabledButtonDesigner.vb-이 클래스를 사용 하면 디자인 타임 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-127">DisabledButtonDesigner.vb - This class enables design-time functionality.</span></span> <span data-ttu-id="4eb61-128">Visual Studio/Visual Web Developer 디자이너를 사용 하 여 제대로 작동 하려면 컨트롤 extender를 하려는 경우이 클래스가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-128">You need this class if you want the control extender to work correctly with the Visual Studio/Visual Web Developer Designer.</span></span>

<span data-ttu-id="4eb61-129">따라서 컨트롤 extender를 서버 쪽 컨트롤, 동작을 클라이언트 쪽 및 서버 쪽 디자이너 클래스 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-129">So a control extender consists of a server-side control, a client-side behavior, and a server-side designer class.</span></span> <span data-ttu-id="4eb61-130">다음 섹션에서 이러한 파일의 세 가지 모두를 만드는 방법에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-130">You learn how to create all three of these files in the following sections.</span></span>

## <a name="creating-the-custom-extender-website-and-project"></a><span data-ttu-id="4eb61-131">사용자 지정 Extender 웹 사이트 및 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="4eb61-131">Creating the Custom Extender Website and Project</span></span>

<span data-ttu-id="4eb61-132">먼저 Visual Studio/Visual Web Developer에서 클래스 라이브러리 프로젝트 및 웹 사이트를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-132">The first step is to create a class library project and website in Visual Studio/Visual Web Developer.</span></span> <span data-ttu-id="4eb61-133">에서는 ll 클래스 라이브러리 프로젝트에서 사용자 지정 extender를 만들고 웹 사이트에서 사용자 지정 extender를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-133">We�ll create the custom extender in the class library project and test the custom extender in the website.</span></span>

<span data-ttu-id="4eb61-134">S를 웹 사이트를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-134">Let�s start with the website.</span></span> <span data-ttu-id="4eb61-135">웹 사이트를 만들려면 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-135">Follow these steps to create the website:</span></span>

1. <span data-ttu-id="4eb61-136">메뉴 옵션을 선택 **파일, 새 웹 사이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-136">Select the menu option **File, New Web Site**.</span></span>
2. <span data-ttu-id="4eb61-137">선택 된 **ASP.NET 웹 사이트** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="4eb61-137">Select the **ASP.NET Web Site** template.</span></span>
3. <span data-ttu-id="4eb61-138">새 웹 사이트 이름을 *Website1*합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-138">Name the new website *Website1*.</span></span>
4. <span data-ttu-id="4eb61-139">클릭 합니다 **확인** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-139">Click the **OK** button.</span></span>

<span data-ttu-id="4eb61-140">다음으로, 컨트롤 extender에 대 한 코드를 포함 하는 클래스 라이브러리 프로젝트를 만들려면 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-140">Next, we need to create the class library project that will contain the code for the control extender:</span></span>

1. <span data-ttu-id="4eb61-141">메뉴 옵션을 선택 **파일을 추가, 새 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-141">Select the menu option **File, Add, New Project**.</span></span>
2. <span data-ttu-id="4eb61-142">선택 된 **클래스 라이브러리** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="4eb61-142">Select the **Class Library** template.</span></span>
3. <span data-ttu-id="4eb61-143">이름의 새 클래스 라이브러리의 이름을 **CustomExtenders**합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-143">Name the new class library with the name **CustomExtenders**.</span></span>
4. <span data-ttu-id="4eb61-144">클릭 합니다 **확인** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-144">Click the **OK** button.</span></span>

<span data-ttu-id="4eb61-145">다음이 단계를 완료 한 후 솔루션 탐색기 창 그림 1과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-145">After you complete these steps, your Solution Explorer window should look like Figure 1.</span></span>


<span data-ttu-id="4eb61-146">[![웹 사이트 및 클래스 라이브러리 프로젝트를 사용 하 여 솔루션](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image8.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="4eb61-146">[![Solution with website and class library project](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image8.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image7.png)</span></span>

<span data-ttu-id="4eb61-147">**그림 01**: 웹 사이트 및 클래스 라이브러리 프로젝트를 사용 하 여 솔루션 ([큰 이미지를 보려면 클릭](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="4eb61-147">**Figure 01**: Solution with website and class library project([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image9.png))</span></span>


<span data-ttu-id="4eb61-148">다음으로, 모든 클래스 라이브러리 프로젝트에 필요한 어셈블리 참조를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-148">Next, you need to add all of the necessary assembly references to the class library project:</span></span>

1. <span data-ttu-id="4eb61-149">CustomExtenders 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **참조 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-149">Right-click the CustomExtenders project and select the menu option **Add Reference**.</span></span>
2. <span data-ttu-id="4eb61-150">.NET 탭을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-150">Select the .NET tab.</span></span>
3. <span data-ttu-id="4eb61-151">다음 어셈블리에 대한 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-151">Add references to the following assemblies:</span></span>

    1. <span data-ttu-id="4eb61-152">System.Web.dll</span><span class="sxs-lookup"><span data-stu-id="4eb61-152">System.Web.dll</span></span>
    2. <span data-ttu-id="4eb61-153">System.Web.Extensions.dll</span><span class="sxs-lookup"><span data-stu-id="4eb61-153">System.Web.Extensions.dll</span></span>
    3. <span data-ttu-id="4eb61-154">System.Design.dll</span><span class="sxs-lookup"><span data-stu-id="4eb61-154">System.Design.dll</span></span>
    4. <span data-ttu-id="4eb61-155">System.Web.Extensions.Design.dll</span><span class="sxs-lookup"><span data-stu-id="4eb61-155">System.Web.Extensions.Design.dll</span></span>
4. <span data-ttu-id="4eb61-156">찾아보기 탭을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-156">Select the Browse tab.</span></span>
5. <span data-ttu-id="4eb61-157">AjaxControlToolkit.dll 어셈블리에 대 한 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-157">Add a reference to the AjaxControlToolkit.dll assembly.</span></span> <span data-ttu-id="4eb61-158">이 어셈블리는 AJAX Control Toolkit을 다운로드 한 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-158">This assembly is located in the folder where you downloaded the AJAX Control Toolkit.</span></span>

<span data-ttu-id="4eb61-159">추가한 모든 올바른 참조 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 속성을 선택 하면 참조 탭을 클릭 하 여 확인할 수 있습니다 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="4eb61-159">You can verify that you have added all of the right references by right-clicking your project, selecting Properties, and clicking the References tab (see Figure 2).</span></span>


<span data-ttu-id="4eb61-160">[![필요한 참조를 사용 하 여 참조 폴더](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image11.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="4eb61-160">[![References folder with required references](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image11.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image10.png)</span></span>

<span data-ttu-id="4eb61-161">**그림 02**: 필요한 참조를 사용 하 여 참조 폴더 ([큰 이미지를 보려면 클릭](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="4eb61-161">**Figure 02**: References folder with required references([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image12.png))</span></span>


## <a name="creating-the-custom-control-extender"></a><span data-ttu-id="4eb61-162">사용자 지정 컨트롤 Extender 만들기</span><span class="sxs-lookup"><span data-stu-id="4eb61-162">Creating the Custom Control Extender</span></span>

<span data-ttu-id="4eb61-163">클래스 라이브러리 만들었으므로 extender 컨트롤 작성을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-163">Now that we have our class library, we can start building our extender control.</span></span> <span data-ttu-id="4eb61-164">사용자 지정 extender 컨트롤 클래스 (참조 목록 1)의 bare 뼈 시작 s 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-164">Let�s start with the bare bones of a custom extender control class (see Listing 1).</span></span>

<span data-ttu-id="4eb61-165">**1-MyCustomExtender.vb 나열**</span><span class="sxs-lookup"><span data-stu-id="4eb61-165">**Listing 1 - MyCustomExtender.vb**</span></span>

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample1.vb)]

<span data-ttu-id="4eb61-166">목록 1에서 extender 컨트롤 클래스에 대 한 확인 하는 몇 가지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-166">There are several things that you notice about the control extender class in Listing 1.</span></span> <span data-ttu-id="4eb61-167">먼저 기본 ExtenderControlBase 클래스에서 클래스를 상속 함을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-167">First, notice that the class inherits from the base ExtenderControlBase class.</span></span> <span data-ttu-id="4eb61-168">모든 AJAX Control Toolkit extender 컨트롤은이 기본 클래스에서 파생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-168">All AJAX Control Toolkit extender controls derive from this base class.</span></span> <span data-ttu-id="4eb61-169">예를 들어, 기본 클래스 TargetID 속성 모든 컨트롤 extender의 필수 속성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-169">For example, the base class includes the TargetID property that is a required property of every control extender.</span></span>

<span data-ttu-id="4eb61-170">다음으로, 클라이언트 스크립트와 관련 된 다음 두 특성 클래스에 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-170">Next, notice that the class includes the following two attributes related to client script:</span></span>

- <span data-ttu-id="4eb61-171">WebResource-파일을 어셈블리에 포함 리소스로 포함 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-171">WebResource - Causes a file to be included as an embedded resource in an assembly.</span></span>
- <span data-ttu-id="4eb61-172">ClientScriptResource-어셈블리에서 검색 해야 하는 스크립트 리소스를 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-172">ClientScriptResource - Causes a script resource to be retrieved from an assembly.</span></span>

<span data-ttu-id="4eb61-173">웹 리소스의 특성을 사용자 지정 extender 컴파일될 때 MyControlBehavior.js JavaScript 파일을 어셈블리에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-173">The WebResource attribute is used to embed the MyControlBehavior.js JavaScript file into the assembly when the custom extender is compiled.</span></span> <span data-ttu-id="4eb61-174">웹 페이지에서 사용자 지정 extender를 사용 하면 어셈블리에서 MyControlBehavior.js 스크립트를 검색 하려면 ClientScriptResource 특성이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-174">The ClientScriptResource attribute is used to retrieve the MyControlBehavior.js script from the assembly when the custom extender is used in a web page.</span></span>


<span data-ttu-id="4eb61-175">작동 하려면 WebResource 및 ClientScriptResource 특성에 대 한 순서 대로 포함 리소스로 JavaScript 파일을 컴파일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-175">In order for the WebResource and ClientScriptResource attributes to work, you must compile the JavaScript file as an embedded resource.</span></span> <span data-ttu-id="4eb61-176">솔루션 탐색기 창에서 파일을 선택 하 고, 속성 시트를 열고, 값을 할당 *포함 리소스* 에 **빌드 작업** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-176">Select the file in the Solution Explorer window, open the property sheet, and assign the value *Embedded Resource* to the **Build Action** property.</span></span>


<span data-ttu-id="4eb61-177">컨트롤 extender에도 TargetControlType 특성을 포함 하는 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-177">Notice that the control extender also includes a TargetControlType attribute.</span></span> <span data-ttu-id="4eb61-178">이 특성은 컨트롤 extender에 의해 확장 된 컨트롤의 형식을 지정 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-178">This attribute is used to specify the type of control that is extended by the control extender.</span></span> <span data-ttu-id="4eb61-179">목록 1의 경우 컨트롤 extender는 텍스트 상자를 확장 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-179">In the case of Listing 1, the control extender is used to extend a TextBox.</span></span>

<span data-ttu-id="4eb61-180">마지막으로, 사용자 지정 extender MyProperty 라는 속성에 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-180">Finally, notice that the custom extender includes a property named MyProperty.</span></span> <span data-ttu-id="4eb61-181">속성은 ExtenderControlProperty 특성으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-181">The property is marked with the ExtenderControlProperty attribute.</span></span> <span data-ttu-id="4eb61-182">GetPropertyValue() 메서드와 SetPropertyValue() 클라이언트 쪽 동작을 서버 쪽 컨트롤 extender 속성 값을 전달 하기 위해 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-182">The GetPropertyValue() and SetPropertyValue() methods are used to pass the property value from the server-side control extender to the client-side behavior.</span></span>

<span data-ttu-id="4eb61-183">가 계속 해 서 우리의 DisabledButton extender에 대 한 코드를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-183">Let�s go ahead and implement the code for our DisabledButton extender.</span></span> <span data-ttu-id="4eb61-184">이 extender에 대 한 코드 목록 2에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-184">The code for this extender can be found in Listing 2.</span></span>

<span data-ttu-id="4eb61-185">**2-DisabledButtonExtender.vb 나열**</span><span class="sxs-lookup"><span data-stu-id="4eb61-185">**Listing 2 - DisabledButtonExtender.vb**</span></span>

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample2.vb)]

<span data-ttu-id="4eb61-186">목록 2에서 DisabledButton extender TargetButtonID 및 DisabledText 라는 두 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-186">The DisabledButton extender in Listing 2 has two properties named TargetButtonID and DisabledText.</span></span> <span data-ttu-id="4eb61-187">TargetButtonID 속성에 적용할 IDReferenceProperty이이 속성에 할당 하는 단추 컨트롤의 ID 이외의 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-187">The IDReferenceProperty applied to the TargetButtonID property prevents you from assigning anything other than the ID of a Button control to this property.</span></span>

<span data-ttu-id="4eb61-188">WebResource 및 ClientScriptResource 특성은이 extender를 사용 하 여 DisabledButtonBehavior.js 라는 파일에 있는 클라이언트 쪽 동작을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-188">The WebResource and ClientScriptResource attributes associate a client-side behavior located in a file named DisabledButtonBehavior.js with this extender.</span></span> <span data-ttu-id="4eb61-189">이 JavaScript 파일의 다음 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-189">We discuss this JavaScript file in the next section.</span></span>

## <a name="creating-the-custom-extender-behavior"></a><span data-ttu-id="4eb61-190">사용자 지정 Extender 동작 만들기</span><span class="sxs-lookup"><span data-stu-id="4eb61-190">Creating the Custom Extender Behavior</span></span>

<span data-ttu-id="4eb61-191">컨트롤 extender의 클라이언트 쪽 구성 요소를 동작을 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-191">The client-side component of a control extender is called a behavior.</span></span> <span data-ttu-id="4eb61-192">사용 하지 않도록 설정 하 고 단추를 사용 하도록 설정 하는 실제 논리 DisabledButton 동작이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-192">The actual logic for disabling and enabling the Button is contained in the DisabledButton behavior.</span></span> <span data-ttu-id="4eb61-193">동작에 대 한 JavaScript 코드는 목록 3에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-193">The JavaScript code for the behavior is included in Listing 3.</span></span>

<span data-ttu-id="4eb61-194">**3-DisabledButton.js 나열**</span><span class="sxs-lookup"><span data-stu-id="4eb61-194">**Listing 3 - DisabledButton.js**</span></span>

[!code-javascript[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample3.js)]

<span data-ttu-id="4eb61-195">보기 3의 JavaScript 파일 DisabledButtonBehavior 클라이언트 쪽 클래스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-195">The JavaScript file in Listing 3 contains a client-side class named DisabledButtonBehavior.</span></span> <span data-ttu-id="4eb61-196">TargetButtonID 라는 두 속성을 포함 하는이 클래스는 서버 쪽 쌍 가져오고 사용 하 여 액세스할 수 있는 DisabledText\_TargetButtonID/set\_TargetButtonID 받고\_DisabledText/set\_ DisabledText 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-196">This class, like its server-side twin, includes two properties named TargetButtonID and DisabledText which you can access using get\_TargetButtonID/set\_TargetButtonID and get\_DisabledText/set\_DisabledText.</span></span>

<span data-ttu-id="4eb61-197">Initialize () 메서드는 동작에 대 한 대상 요소를 사용 하 여 keyup 이벤트 처리기를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-197">The initialize() method associates a keyup event handler with the target element for the behavior.</span></span> <span data-ttu-id="4eb61-198">이 동작과 연결 된 텍스트 상자에 문자를 입력할 때마다 keyup 처리기를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-198">Each time you type a letter into the TextBox associated with this behavior, the keyup handler executes.</span></span> <span data-ttu-id="4eb61-199">Keyup 처리기를 사용 하도록 설정 또는 동작과 연결 된 텍스트 상자에서 모든 텍스트를 포함 하는 여부에 따라 단추를 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-199">The keyup handler either enables or disables the Button depending on whether the TextBox associated with the behavior contains any text.</span></span>

<span data-ttu-id="4eb61-200">JavaScript 파일 목록 3에 포함 리소스로 컴파일해야 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-200">Remember that you must compile the JavaScript file in Listing 3 as an embedded resource.</span></span> <span data-ttu-id="4eb61-201">솔루션 탐색기 창에서 파일을 선택 하 고, 속성 시트를 열고, 값을 할당 *포함 리소스* 에 **빌드 작업** 속성 (그림 3 참조).</span><span class="sxs-lookup"><span data-stu-id="4eb61-201">Select the file in the Solution Explorer window, open the property sheet, and assign the value *Embedded Resource* to the **Build Action** property (see Figure 3).</span></span> <span data-ttu-id="4eb61-202">이 옵션은 Visual Studio 및 Visual Web Developer에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-202">This option is available in both Visual Studio and Visual Web Developer.</span></span>


<span data-ttu-id="4eb61-203">[![JavaScript 파일을 포함 리소스로 추가](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image14.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="4eb61-203">[![Adding a JavaScript file as an embedded resource](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image14.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image13.png)</span></span>

<span data-ttu-id="4eb61-204">**그림 03**: 포함된 리소스와 JavaScript 파일을 추가 ([큰 이미지를 보려면 클릭](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image15.png))</span><span class="sxs-lookup"><span data-stu-id="4eb61-204">**Figure 03**: Adding a JavaScript file as an embedded resource([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image15.png))</span></span>


## <a name="creating-the-custom-extender-designer"></a><span data-ttu-id="4eb61-205">사용자 지정 Extender 디자이너 만들기</span><span class="sxs-lookup"><span data-stu-id="4eb61-205">Creating the Custom Extender Designer</span></span>

<span data-ttu-id="4eb61-206">이 extender를 완료 하려면 만들어야 하는 하나의 마지막 클래스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-206">There is one last class that we need to create to complete our extender.</span></span> <span data-ttu-id="4eb61-207">목록 4에서 디자이너 클래스를 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-207">We need to create the designer class in Listing 4.</span></span> <span data-ttu-id="4eb61-208">이 클래스는 Visual Studio/Visual Web Developer 디자이너를 사용 하 여 올바르게 작동 하는 extender를 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-208">This class is required to make the extender behave correctly with the Visual Studio/Visual Web Developer Designer.</span></span>

<span data-ttu-id="4eb61-209">**4-DisabledButtonDesigner.vb 나열**</span><span class="sxs-lookup"><span data-stu-id="4eb61-209">**Listing 4 - DisabledButtonDesigner.vb**</span></span>

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample4.vb)]

<span data-ttu-id="4eb61-210">Designer 특성을 사용 하 여 DisabledButton extender 4에서 디자이너를 연결합니다. 이와 같은 DisabledButtonExtender 클래스에 Designer 특성을 적용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-210">You associate the designer in Listing 4 with the DisabledButton extender with the Designer attribute.You need to apply the Designer attribute to the DisabledButtonExtender class like this:</span></span>

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample5.vb)]

## <a name="using-the-custom-extender"></a><span data-ttu-id="4eb61-211">사용자 지정 Extender를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="4eb61-211">Using the Custom Extender</span></span>

<span data-ttu-id="4eb61-212">이제 DisabledButton 컨트롤 extender 만들기를 마친 것, ASP.NET 웹 사이트에서 사용 하는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-212">Now that we have finished creating the DisabledButton control extender, it is time to use it in our ASP.NET website.</span></span> <span data-ttu-id="4eb61-213">먼저, 도구 상자에 사용자 지정 extender를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-213">First, we need to add the custom extender to the toolbox.</span></span> <span data-ttu-id="4eb61-214">아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-214">Follow these steps:</span></span>

1. <span data-ttu-id="4eb61-215">솔루션 탐색기 창에서 페이지를 두 번 클릭 하 여 ASP.NET 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-215">Open an ASP.NET page by double-clicking the page in the Solution Explorer window.</span></span>
2. <span data-ttu-id="4eb61-216">도구 상자를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **선택 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-216">Right-click the toolbox and select the menu option **Choose Items**.</span></span>
3. <span data-ttu-id="4eb61-217">도구 상자 항목 선택 대화 상자에서 CustomExtenders.dll 어셈블리를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-217">In the Choose Toolbox Items dialog, browse to the CustomExtenders.dll assembly.</span></span>
4. <span data-ttu-id="4eb61-218">클릭 합니다 **확인** 단추를 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-218">Click the **OK** button to close the dialog.</span></span>

<span data-ttu-id="4eb61-219">다음이 단계를 완료 하면 DisabledButton 컨트롤 extender 도구 상자에 나타납니다 (그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="4eb61-219">After you complete these steps, the DisabledButton control extender should appear in the toolbox (see Figure 4).</span></span>


<span data-ttu-id="4eb61-220">[![도구 상자에서 DisabledButton](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image17.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="4eb61-220">[![DisabledButton in the toolbox](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image17.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image16.png)</span></span>

<span data-ttu-id="4eb61-221">**그림 04**: 도구 상자에서 DisabledButton ([큰 이미지를 보려면 클릭](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="4eb61-221">**Figure 04**: DisabledButton in the toolbox([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image18.png))</span></span>


<span data-ttu-id="4eb61-222">그런 다음 새 ASP.NET 페이지를 만들 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-222">Next, we need to create a new ASP.NET page.</span></span> <span data-ttu-id="4eb61-223">아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-223">Follow these steps:</span></span>

1. <span data-ttu-id="4eb61-224">ShowDisabledButton.aspx 라는 새로운 ASP.NET 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-224">Create a new ASP.NET page named ShowDisabledButton.aspx.</span></span>
2. <span data-ttu-id="4eb61-225">ScriptManager를 페이지로 끌어옵니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-225">Drag a ScriptManager onto the page.</span></span>
3. <span data-ttu-id="4eb61-226">TextBox 컨트롤을 페이지로 끌어옵니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-226">Drag a TextBox control onto the page.</span></span>
4. <span data-ttu-id="4eb61-227">단추 컨트롤을 페이지로 끌어옵니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-227">Drag a Button control onto the page.</span></span>
5. <span data-ttu-id="4eb61-228">속성 창에서 단추 ID 속성 값을 변경 <em>btnSave</em> 및 텍스트 속성을 값 *저장할\** 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-228">In the Properties window, change the Button ID property to the value <em>btnSave</em> and the Text property to the value *Save\**.</span></span>
  

<span data-ttu-id="4eb61-229">표준 ASP.NET TextBox와 Button 컨트롤을 사용 하 여 페이지를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-229">We created a page with a standard ASP.NET TextBox and Button control.</span></span>

<span data-ttu-id="4eb61-230">다음으로, DisabledButton extender 사용 하 여 텍스트 상자 컨트롤을 확장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-230">Next, we need to extend the TextBox control with the DisabledButton extender:</span></span>

1. <span data-ttu-id="4eb61-231">선택 된 **Extender 추가** 작업 옵션 Extender 마법사 대화 상자를 엽니다 (그림 5 참조).</span><span class="sxs-lookup"><span data-stu-id="4eb61-231">Select the **Add Extender** task option to open the Extender Wizard dialog (see Figure 5).</span></span> <span data-ttu-id="4eb61-232">대화 상자에 사용자 지정 DisabledButton extender는 포함 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-232">Notice that the dialog includes our custom DisabledButton extender.</span></span>
2. <span data-ttu-id="4eb61-233">DisabledButton extender를 선택 하 고 클릭 합니다 **확인** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-233">Select the DisabledButton extender and click the **OK** button.</span></span>


<span data-ttu-id="4eb61-234">[![Extender 마법사 대화 상자](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image20.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="4eb61-234">[![The Extender Wizard dialog](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image20.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image19.png)</span></span>

<span data-ttu-id="4eb61-235">**그림 05**: Extender 마법사 대화 상자 ([큰 이미지를 보려면 클릭](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image21.png))</span><span class="sxs-lookup"><span data-stu-id="4eb61-235">**Figure 05**: The Extender Wizard dialog([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image21.png))</span></span>


<span data-ttu-id="4eb61-236">마지막으로, DisabledButton extender의 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-236">Finally, we can set the properties of the DisabledButton extender.</span></span> <span data-ttu-id="4eb61-237">TextBox 컨트롤의 속성을 수정 하 여 DisabledButton extender의 속성을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-237">You can modify the properties of the DisabledButton extender by modifying the properties of the TextBox control:</span></span>

1. <span data-ttu-id="4eb61-238">디자이너에서 텍스트 상자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-238">Select the TextBox in the Designer.</span></span>
2. <span data-ttu-id="4eb61-239">속성 창에서 Extender 노드를 확장 (그림 6 참조).</span><span class="sxs-lookup"><span data-stu-id="4eb61-239">In the Properties window, expand the Extenders node (see Figure 6).</span></span>
3. <span data-ttu-id="4eb61-240">값을 할당 *저장할* DisabledText 속성 및 값에 *btnSave* TargetButtonID 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-240">Assign the value *Save* to the DisabledText property and the value *btnSave* to the TargetButtonID property.</span></span>


<span data-ttu-id="4eb61-241">[![Extender 속성 설정](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image23.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image22.png)</span><span class="sxs-lookup"><span data-stu-id="4eb61-241">[![Setting extender properties](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image23.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image22.png)</span></span>

<span data-ttu-id="4eb61-242">**그림 06**: extender 속성을 설정 ([큰 이미지를 보려면 클릭](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image24.png))</span><span class="sxs-lookup"><span data-stu-id="4eb61-242">**Figure 06**: Setting extender properties([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image24.png))</span></span>


<span data-ttu-id="4eb61-243">페이지 (F5를 눌러)를 실행 하면 단추 컨트롤은 처음에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-243">When you run the page (by hitting F5), the Button control is initially disabled.</span></span> <span data-ttu-id="4eb61-244">입력란에 텍스트 입력을 시작 하는 즉시 컨트롤은 단추 (그림 7 참조)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-244">As soon as you start entering text into the TextBox, the Button control is enabled (see Figure 7).</span></span>


<span data-ttu-id="4eb61-245">[![실행 중인 DisabledButton extender](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image26.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="4eb61-245">[![The DisabledButton extender in action](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image26.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image25.png)</span></span>

<span data-ttu-id="4eb61-246">**그림 07**: 작업의 The DisabledButton extender ([큰 이미지를 보려면 클릭](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image27.png))</span><span class="sxs-lookup"><span data-stu-id="4eb61-246">**Figure 07**: The DisabledButton extender in action([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image27.png))</span></span>


## <a name="summary"></a><span data-ttu-id="4eb61-247">요약</span><span class="sxs-lookup"><span data-stu-id="4eb61-247">Summary</span></span>

<span data-ttu-id="4eb61-248">이 자습서의 목표는 AJAX Control Toolkit 사용자 지정 extender 컨트롤을 사용 하 여 확장 하는 방법을 설명 하는 것 이었습니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-248">The goal of this tutorial was to explain how you can extend the AJAX Control Toolkit with custom extender controls.</span></span> <span data-ttu-id="4eb61-249">이 자습서에서는 간단한 DisabledButton 컨트롤 extender를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-249">In this tutorial, we created a simple DisabledButton control extender.</span></span> <span data-ttu-id="4eb61-250">DisabledButtonExtender 클래스, DisabledButtonBehavior JavaScript 동작 및 DisabledButtonDesigner 클래스를 만들어이 extender를 구현 했습니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-250">We implemented this extender by creating a DisabledButtonExtender class, a DisabledButtonBehavior JavaScript behavior, and a DisabledButtonDesigner class.</span></span> <span data-ttu-id="4eb61-251">사용자 지정 컨트롤 extender를 만들 때마다 비슷한 일련의 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="4eb61-251">You follow a similar set of steps whenever you create a custom control extender.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="4eb61-252">이전</span><span class="sxs-lookup"><span data-stu-id="4eb61-252">Previous</span></span>](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)
