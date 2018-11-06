---
uid: aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
title: 프로그래밍 ASP.NET 웹 페이지 (Razor)를 사용 하 여 Visual Studio | Microsoft Docs
author: Rick-Anderson
description: 이 부록에서는 ASP.NET 웹 페이지 Razor 구문 사용 하 여 프로그램을 Visual Studio 2010 또는 Visual Web Developer 2010 Express를 사용 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 02/13/2014
ms.assetid: 0acfec5a-48f2-4766-a801-a0f426966f0a
msc.legacyurl: /web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: 5b8df17ec1021d133579e23cb4f5b0d0f67d4c7c
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51020457"
---
<a name="programming-aspnet-web-pages-razor-using-visual-studio"></a><span data-ttu-id="3eec4-103">Visual Studio를 사용 하 여 ASP.NET 웹 페이지 (Razor) 프로그래밍</span><span class="sxs-lookup"><span data-stu-id="3eec4-103">Programming ASP.NET Web Pages (Razor) Using Visual Studio</span></span>
====================
<span data-ttu-id="3eec4-104">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="3eec4-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="3eec4-105">이 문서에서는 프로그램 ASP.NET Web Pages (Razor) 웹 사이트에 Visual Studio 또는 Visual Web Developer Express를 사용 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-105">This article explains how you can use Visual Studio or Visual Web Developer Express to program ASP.NET Web Pages (Razor) websites.</span></span>
>
> <span data-ttu-id="3eec4-106">학습할 내용</span><span class="sxs-lookup"><span data-stu-id="3eec4-106">What you'll learn</span></span>
>
> - <span data-ttu-id="3eec4-107">ASP.NET 웹 페이지를 사용 하 여 Visual Studio 버전에서 작동 하도록 (내용이 있는 경우)를 설치 해야 할 항목.</span><span class="sxs-lookup"><span data-stu-id="3eec4-107">What you need to install (if anything) to work with ASP.NET Web Pages in your version of Visual Studio.</span></span>
> - <span data-ttu-id="3eec4-108">Visual Web Developer 2010 Express에 ASP.NET 웹 페이지에 대 한 지원을 추가 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-108">How to add support for ASP.NET Web Pages to Visual Web Developer 2010 Express.</span></span>
> - <span data-ttu-id="3eec4-109">ASP.NET Razor 페이지, IntelliSense 등의 디버거를 사용 하려면 Visual Studio의 기능을 사용 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="3eec4-109">How to use features in Visual Studio to work with ASP.NET Razor pages, including IntelliSense and the debugger.</span></span>
>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="3eec4-110">이 자습서에 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="3eec4-110">Software versions used in the tutorial</span></span>
>
>
> - <span data-ttu-id="3eec4-111">ASP.NET Web Pages (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="3eec4-111">ASP.NET Web Pages (Razor) 3</span></span>
> - <span data-ttu-id="3eec4-112">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="3eec4-112">Visual Studio 2013</span></span>
> - <span data-ttu-id="3eec4-113">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="3eec4-113">WebMatrix 3</span></span>
>
>
> <span data-ttu-id="3eec4-114">이 자습서는 ASP.NET 웹 페이지 2, Visual Studio 2012, Visual Studio 2010 및 WebMatrix 2 에서도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-114">This tutorial also works with ASP.NET Web Pages 2, Visual Studio 2012, Visual Studio 2010, and WebMatrix 2.</span></span>


<span data-ttu-id="3eec4-115">WebMatrix 또는 다른 여러 코드 편집기를 사용 하 여 Razor 구문이 있는 ASP.NET 웹 페이지를 프로그래밍할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-115">You can program ASP.NET Web pages with Razor syntax using WebMatrix or many other code editors.</span></span> <span data-ttu-id="3eec4-116">또한 Microsoft Visual Studio는 다양 한 유형의 응용 프로그램 (뿐 아니라 웹 사이트)를 만들기 위한 강력한 도구 집합을 제공 하는 모든 기능을 갖춘 통합된 개발 환경 (IDE)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-116">You can also use Microsoft Visual Studio which is a full-featured integrated development environment (IDE) that provides a powerful set of tools for creating many types of applications (not just websites).</span></span> <span data-ttu-id="3eec4-117">ASP.NET Razor 페이지를 사용 하려면 사용할 수 있습니다 [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)합니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-117">To work with ASP.NET Razor pages, you can use [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span>

<span data-ttu-id="3eec4-118">두 특히 유용한 Visual Studio는 ASP.NET Razor 웹 페이지를 사용 하 여 프로그래밍 하는 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-118">Two particularly useful features that Visual Studio provides for programming with ASP.NET Razor web pages are:</span></span>

- <span data-ttu-id="3eec4-119">*IntelliSense*합니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-119">*IntelliSense*.</span></span> <span data-ttu-id="3eec4-120">Visual Studio에 기본 제공 IntelliSense 기능은 WebMatrix에서 IntelliSense 보다 더 포괄적입니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-120">The IntelliSense feature built into Visual Studio is more comprehensive than IntelliSense in WebMatrix.</span></span>
- <span data-ttu-id="3eec4-121">*디버거*합니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-121">*Debugger*.</span></span> <span data-ttu-id="3eec4-122">디버거를 사용 하면 코드 실행, 변수 검사를 한 줄씩 코드를 단계별로 실행 하면 프로그램을 중지 하 여 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-122">The debugger lets you troubleshoot your code by stopping a program while it's running, examining variables, and stepping through the code line by line.</span></span>

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a><span data-ttu-id="3eec4-123">Visual Studio를 사용 하 여 다른 버전의 ASP.NET 웹 페이지를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="3eec4-123">Using Visual Studio with Different Versions of ASP.NET Web Pages</span></span>

<span data-ttu-id="3eec4-124">Visual Studio 2017에 ASP.NET 웹 앱을 개발 하려면 다음을 설치 합니다 **ASP.NET 및 웹 개발** 워크 로드.</span><span class="sxs-lookup"><span data-stu-id="3eec4-124">To develop ASP.NET web apps in Visual Studio 2017, install the **ASP.NET and web development** workload.</span></span>

<span data-ttu-id="3eec4-125">Visual Studio 2012 및 Visual Studio 2013에는 ASP.NET 웹 페이지에 대 한 지원이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-125">Visual Studio 2012 and Visual Studio 2013 include support for ASP.NET Web Pages.</span></span> <span data-ttu-id="3eec4-126">(ASP.NET 웹 페이지를 지원 하기 위해 필요한 패키지 설치 되어 Visual Studio를 설치 합니다.)</span><span class="sxs-lookup"><span data-stu-id="3eec4-126">(The packages that are required in order to support ASP.NET Web Pages are installed when you install Visual Studio.)</span></span>

<span data-ttu-id="3eec4-127">Visual Studio 2010 지원이 포함 되지 않습니다 기본적으로 ASP.NET 웹 페이지에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-127">Visual Studio 2010 does not include support by default for ASP.NET Web Pages.</span></span> <span data-ttu-id="3eec4-128">Visual Studio 2010을 사용 하 여 ASP.NET 웹 페이지를 사용 하려면 ASP.NET MVC 패키지를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-128">To use ASP.NET Web Pages with Visual Studio 2010, you must install the ASP.NET MVC package.</span></span> <span data-ttu-id="3eec4-129">ASP.NET 웹 페이지 2를 가져오려면 ASP.NET MVC 4를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-129">To get ASP.NET Web Pages 2, you install ASP.NET MVC 4.</span></span>

<span data-ttu-id="3eec4-130">다음 표에서 서로 다른 버전의 Visual Studio에서 ASP.NET 웹 페이지에 대 한 지원.</span><span class="sxs-lookup"><span data-stu-id="3eec4-130">The following table summarizes the support for ASP.NET Web Pages in different versions of Visual Studio.</span></span>

|  | <span data-ttu-id="3eec4-131">Visual Studio 2010</span><span class="sxs-lookup"><span data-stu-id="3eec4-131">Visual Studio 2010</span></span> | <span data-ttu-id="3eec4-132">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="3eec4-132">Visual Studio 2012</span></span> | <span data-ttu-id="3eec4-133">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="3eec4-133">Visual Studio 2013</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3eec4-134">**ASP.NET 웹 페이지 2**</span><span class="sxs-lookup"><span data-stu-id="3eec4-134">**ASP.NET Web Pages 2**</span></span> | <span data-ttu-id="3eec4-135">ASP.NET MVC 4를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-135">Install ASP.NET MVC 4</span></span> | <span data-ttu-id="3eec4-136">(포함)</span><span class="sxs-lookup"><span data-stu-id="3eec4-136">(Included)</span></span> | <span data-ttu-id="3eec4-137">(포함)</span><span class="sxs-lookup"><span data-stu-id="3eec4-137">(Included)</span></span> |
| <span data-ttu-id="3eec4-138">**ASP.NET 웹 페이지 3**</span><span class="sxs-lookup"><span data-stu-id="3eec4-138">**ASP.NET Web Pages 3**</span></span> |  | <span data-ttu-id="3eec4-139">업데이트를 ASP.NET 웹 페이지를 통해 NuGet 3</span><span class="sxs-lookup"><span data-stu-id="3eec4-139">Update to ASP.NET Web Pages 3 through NuGet</span></span> | <span data-ttu-id="3eec4-140">(포함)</span><span class="sxs-lookup"><span data-stu-id="3eec4-140">(Included)</span></span> |

<span data-ttu-id="3eec4-141">Visual Studio 2010을 사용 하려면 참조 [Visual Studio 2010에서 ASP.NET 웹 페이지에 대 한 지원 설치](#vs2010support)합니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-141">To work with Visual Studio 2010, see [Installing Support for ASP.NET Web Pages in Visual Studio 2010](#vs2010support).</span></span>

## <a name="launching-visual-studio-from-webmatrix"></a><span data-ttu-id="3eec4-142">WebMatrix에서 Visual Studio를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-142">Launching Visual Studio from WebMatrix</span></span>

<span data-ttu-id="3eec4-143">WebMatrix에서 프로젝트를 시작 하 고 Visual Studio로 전환 하려고 할 경우 WebMatrix는 Visual Studio에서 프로젝트를 쉽게 여는 단추를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-143">If you have started a project in WebMatrix and want to switch to Visual Studio, WebMatrix provides a button to easily open the project in Visual Studio.</span></span> <span data-ttu-id="3eec4-144">사용 하도록 Visual Studio이이 단추에 대 한 컴퓨터에 설치 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-144">You must have Visual Studio installed on your computer for this button to be enabled.</span></span> <span data-ttu-id="3eec4-145">다음 이미지는 WebMatrix에서 단추를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-145">The following image shows the button in WebMatrix.</span></span>

![Visual Studio를 시작 합니다.](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

<span data-ttu-id="3eec4-147">단추를 클릭 하면 프로젝트를 Visual Studio에서 열려 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-147">When you click the button, the project is opened in Visual Studio.</span></span> <span data-ttu-id="3eec4-148">전환할 수 있습니다 앞뒤로 WebMatrix 및 Visual Studio 간에 아무 문제 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-148">You can switch back and forth between WebMatrix and Visual Studio without any problems.</span></span> <span data-ttu-id="3eec4-149">모든 파일에서 다른 환경에서 변경 되었습니다. 최신 변경 내용을 가져오는 다시 로드 해야 하는 경우 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-149">You will be notified if any files have changed in the other environment and need to be reloaded to get the latest changes.</span></span>

## <a name="creating-aspnet-razor-site-in-visual-studio"></a><span data-ttu-id="3eec4-150">Visual Studio에서 ASP.NET Razor 사이트 만들기</span><span class="sxs-lookup"><span data-stu-id="3eec4-150">Creating ASP.NET Razor Site in Visual Studio</span></span>

<span data-ttu-id="3eec4-151">Visual Studio에서 ASP.NET Razor 웹 사이트를 만들려면:</span><span class="sxs-lookup"><span data-stu-id="3eec4-151">To create an ASP.NET Razor website in Visual Studio:</span></span>

1. <span data-ttu-id="3eec4-152">Visual Studio를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-152">Open Visual Studio.</span></span>
2. <span data-ttu-id="3eec4-153">에 **파일** 메뉴에서 클릭 **새 웹 사이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-153">In the **File** menu, click **New Web Site**.</span></span>

    ![새 웹 사이트 만들기](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. <span data-ttu-id="3eec4-155">에 **새 웹 사이트** 대화 상자 (Visual C# 또는 Visual Basic)를 사용할 언어를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-155">In the **New Web Site** dialog box, select the language to use (Visual C# or Visual Basic).</span></span>
4. <span data-ttu-id="3eec4-156">선택 된 **ASP.NET 웹 사이트 (Razor)** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="3eec4-156">Select the **ASP.NET Web Site (Razor)** template.</span></span>

    ![razor 사이트](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. <span data-ttu-id="3eec4-158">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-158">Click **OK**.</span></span>

<span data-ttu-id="3eec4-159">새 프로젝트가 존재 하며 시작 하는 데 몇 가지 기본 웹 페이지를 사용 하 여 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-159">Your new project exists and is populated with some default web pages to help you get started.</span></span>

### <a name="using-intellisense"></a><span data-ttu-id="3eec4-160">IntelliSense 사용</span><span class="sxs-lookup"><span data-stu-id="3eec4-160">Using IntelliSense</span></span>

<span data-ttu-id="3eec4-161">사이트를 만들었으므로 이제 Visual Studio에서 IntelliSense는 작동 하는 방법을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-161">Now that you've created a site, you can see how IntelliSense works in Visual Studio.</span></span>

1. <span data-ttu-id="3eec4-162">방금 만든 웹 사이트에서 엽니다는 *Default.cshtml* 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-162">In the website you just created, open the *Default.cshtml* page.</span></span>
2. <span data-ttu-id="3eec4-163">후 합니다 `<h3>` 페이지에서 태그 입력 `@ServerInfo.` (마침표 포함).</span><span class="sxs-lookup"><span data-stu-id="3eec4-163">After the `<h3>` tags in the page, type `@ServerInfo.` (including the dot).</span></span> <span data-ttu-id="3eec4-164">IntelliSense에 대 한 사용 가능한 메서드를 표시 하는 방법의 `ServerInfo` 드롭 다운 목록에서 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-164">Notice how IntelliSense displays the available methods for the `ServerInfo` helper in a drop-down list.</span></span>

    ![intellisense](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. <span data-ttu-id="3eec4-166">선택 된 `GetHtml` 메서드 목록에서 한 다음 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-166">Select the `GetHtml` method from the list and then press Enter.</span></span> <span data-ttu-id="3eec4-167">IntelliSense 메서드를 자동으로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-167">IntelliSense automatically fills in the method.</span></span> <span data-ttu-id="3eec4-168">(C#의 모든 메서드를 추가 해야 하는 대로 `()` 메서드 이후에 문자입니다.) 에 대 한 완성 된 코드는 `GetHtml` 메서드는 다음 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-168">(As with any method in C#, you must add `()` characters after the method.) The completed code for the `GetHtml` method looks like the following example:</span></span>

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. <span data-ttu-id="3eec4-169">페이지를 실행 하려면 Ctrl + F5 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-169">Press Ctrl+F5 to run the page.</span></span> <span data-ttu-id="3eec4-170">다음은 같은 브라우저에 표시 하면 페이지 모양이입니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-170">This is what the page looks like when displayed in a browser:</span></span>

    ![브라우저의 기본 페이지](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. <span data-ttu-id="3eec4-172">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-172">Close the browser.</span></span>

### <a name="using-the-debugger"></a><span data-ttu-id="3eec4-173">디버거를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="3eec4-173">Using the Debugger</span></span>

1. <span data-ttu-id="3eec4-174">맨 위에 있는 *Default.cshtml* 페이지에서 시작 하는 줄 뒤 `Page.Title`, 코드의 다음 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-174">At the top of the *Default.cshtml* page, after the line that begins with `Page.Title`, add the following line of code:</span></span>

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. <span data-ttu-id="3eec4-175">왼쪽의 코드 편집기의 회색 여백에 클릭이 새 줄을 추가 하기 위해 한 *중단점*합니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-175">In the gray margin of the editor to the left of the code, click next to this new line in order to add a *breakpoint*.</span></span> <span data-ttu-id="3eec4-176">중단점 상황을 볼 수 있도록 해당 지점에서 프로그램 실행을 중지 하도록 디버거에 지시 하는 마커를입니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-176">A breakpoint is a marker that tells the debugger to stop running the program at that point so you can see what's happening.</span></span>

    ![중단점 설정](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. <span data-ttu-id="3eec4-178">호출을 제거 합니다 `ServerInfo.GetHtml` 메서드를 호출을 추가 하 고는 `@myTime` 그 자리에 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-178">Remove the call to the `ServerInfo.GetHtml` method, and add a call to the `@myTime` variable in its place.</span></span> <span data-ttu-id="3eec4-179">이 호출은 코드의 새 줄에 의해 반환 되는 현재 시간 값을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-179">This call displays the current time value that's returned by the new line of code.</span></span>
4. <span data-ttu-id="3eec4-180">F5 키를 눌러 디버거에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-180">Press F5 to run the page in the debugger.</span></span> <span data-ttu-id="3eec4-181">페이지는 사용자가 설정한 중단점에서 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-181">The page stops on the breakpoint that you set.</span></span> <span data-ttu-id="3eec4-182">다음 이미지는 페이지 모양을 편집기 (노란색)에서 중단점을 사용 하 여 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-182">The following image shows what the page looks like in the editor with the breakpoint (in yellow).</span></span>

    ![디버그 중단점](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. <span data-ttu-id="3eec4-184">디버그 도구 모음에서 클릭 합니다 **한 단계씩 코드 실행** 단추 (또는 F11 키를 눌러) 코드의 다음 줄을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-184">In the Debug toolbar, click the **Step Into** button (or press F11) to run the next line of code.</span></span> <span data-ttu-id="3eec4-185">이 단추를 클릭할 때마다 코드의 다음 줄으로 실행을 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-185">Each time you click this button, you advance the execution to the next line of code.</span></span>

    ![단추를 한 단계씩](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. <span data-ttu-id="3eec4-187">값을 검사 합니다 `myTime` 위로 마우스 포인터를 보유 하 여 또는에서 표시 되는 값을 검사 하 여 변수를 **지역** 및 **호출 스택** windows.</span><span class="sxs-lookup"><span data-stu-id="3eec4-187">Examine the value of the `myTime` variable by holding your mouse pointer over it or by inspecting the values displayed in the **Locals** and **Call Stack** windows.</span></span> <span data-ttu-id="3eec4-188">Visual Studio 변수의 값을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-188">Visual Studio display the value of the variable.</span></span>

    ![시간 표시 값](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. <span data-ttu-id="3eec4-190">변수를 검사 하 고 단계별 코드 실행을 마친 경우 f5 키를 눌러 각 줄에서 중지 하지 않고 페이지 실행을 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-190">When you're done examining the variable and stepping through code, press F5 to continue running the page without stopping at each line.</span></span> <span data-ttu-id="3eec4-191">모든 코드를 단계별로 마쳤으면 브라우저 페이지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-191">When you've finished stepping through all the code, the browser displays the page.</span></span>

<span data-ttu-id="3eec4-192">디버거 및 Visual Studio에서 코드를 디버깅 하는 방법에 대 한 자세한 내용은 참조 하세요 [연습: Visual Web Developer에서 웹 페이지 디버깅](https://msdn.microsoft.com/library/z9e7w6cs.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-192">To learn more about the debugger and about how to debug code in Visual Studio, see [Walkthrough: Debugging Web Pages in Visual Web Developer](https://msdn.microsoft.com/library/z9e7w6cs.aspx).</span></span>

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a><span data-ttu-id="3eec4-193">Razor를 사용 하 여 Visual Studio를 사용 하 여 ASP.NET MVC 프로젝트에서</span><span class="sxs-lookup"><span data-stu-id="3eec4-193">Using Razor in ASP.NET MVC projects with Visual Studio</span></span>

<span data-ttu-id="3eec4-194">ASP.NET MVC 프로젝트에서 Razor 구문은 광범위 하 게도 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-194">The Razor syntax is also used extensively in ASP.NET MVC projects.</span></span> <span data-ttu-id="3eec4-195">MVC는 강력한 패턴 기반 방식으로 동적 웹 사이트를 빌드하는입니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-195">MVC is a powerful, patterns-based way to build dynamic websites.</span></span> <span data-ttu-id="3eec4-196">ASP.NET Web Pages 사이트 유지 관리 하기가 되 면 ASP.NET MVC 응용 프로그램을 변환 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-196">If your ASP.NET Web Pages site becomes difficult to maintain, you might want to consider converting it to an ASP.NET MVC application.</span></span> <span data-ttu-id="3eec4-197">MVC 응용 프로그램을 만드는 예제를 보려면 [ASP.NET MVC 5 시작](../../../mvc/overview/getting-started/introduction/getting-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-197">For an example of creating an MVC application, see [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a><span data-ttu-id="3eec4-198">Visual Studio 2010에서 ASP.NET 웹 페이지에 대 한 지원 설치</span><span class="sxs-lookup"><span data-stu-id="3eec4-198">Installing Support for ASP.NET Web Pages in Visual Studio 2010</span></span>

<span data-ttu-id="3eec4-199">이 섹션에서는 Visual Studio에 대 한 Visual Web Developer Express 2010 및 ASP.NET 웹 페이지 도구를 설치 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-199">This section shows how to install Visual Web Developer Express 2010 and the ASP.NET Web Pages Tools for Visual Studio.</span></span>

1. <span data-ttu-id="3eec4-200">웹 플랫폼 설치 관리자를 아직 없는 경우 다음 URL에서 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-200">If you don't already have the Web Platform Installer, download it from the following URL:</span></span>

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. <span data-ttu-id="3eec4-201">웹 플랫폼 설치 관리자를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-201">Run the Web Platform Installer.</span></span>
3. <span data-ttu-id="3eec4-202">클릭 합니다 **제품** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-202">Click the **Products** tab.</span></span>

    ![WebPI 제품 탭](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. <span data-ttu-id="3eec4-204">검색할 **ASP.NET MVC 4** (ASP.NET 웹 페이지 2)에 대 한 다음 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-204">Search for **ASP.NET MVC 4** (for ASP.NET Web Pages 2) and then click **Add**.</span></span> <span data-ttu-id="3eec4-205">이러한 제품에는 ASP.NET Razor 웹 사이트를 구축 하기 위한 Visual Studio 도구가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-205">These products include Visual Studio tools for building ASP.NET Razor websites.</span></span>

    ![WebPi 설치 옵션](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. <span data-ttu-id="3eec4-207">클릭 **설치** 설치를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="3eec4-207">Click **Install** to complete the installation.</span></span>
