---
uid: aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
title: 프로그래밍 ASP.NET 웹 페이지 (Razor)를 사용 하 여 Visual Studio | Microsoft Docs
author: tfitzmac
description: 이 부록에서는 Razor 구문이 있는 ASP.NET 웹 페이지 프로그램에 Visual Studio 2010 또는 Visual Web Developer 2010 Express를 사용 하는 방법을 설명 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/13/2014
ms.topic: article
ms.assetid: 0acfec5a-48f2-4766-a801-a0f426966f0a
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: eb17c8cc1fab5b552c8495e74bb86ae9dbc5b972
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30896586"
---
<a name="programming-aspnet-web-pages-razor-using-visual-studio"></a><span data-ttu-id="25826-103">Visual Studio를 사용 하 여 ASP.NET 웹 페이지 (Razor) 프로그래밍</span><span class="sxs-lookup"><span data-stu-id="25826-103">Programming ASP.NET Web Pages (Razor) Using Visual Studio</span></span>
====================
<span data-ttu-id="25826-104">으로 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="25826-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="25826-105">이 문서에서는 프로그램 ASP.NET 웹 페이지 (Razor) 웹 사이트에 Visual Studio 또는 Visual Web Developer Express를 사용 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="25826-105">This article explains how you can use Visual Studio or Visual Web Developer Express to program ASP.NET Web Pages (Razor) websites.</span></span>
> 
> <span data-ttu-id="25826-106">학습 내용</span><span class="sxs-lookup"><span data-stu-id="25826-106">What you'll learn</span></span>
> 
> - <span data-ttu-id="25826-107">ASP.NET 웹 페이지를 Visual Studio 버전에서 작동 하도록 (내용이 있는 경우)를 설치 해야 할 기능.</span><span class="sxs-lookup"><span data-stu-id="25826-107">What you need to install (if anything) to work with ASP.NET Web Pages in your version of Visual Studio.</span></span>
> - <span data-ttu-id="25826-108">Visual Web Developer 2010 Express에 ASP.NET 웹 페이지에 대 한 지원을 추가 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="25826-108">How to add support for ASP.NET Web Pages to Visual Web Developer 2010 Express.</span></span>
> - <span data-ttu-id="25826-109">IntelliSense와 디버거를 포함 하 여 ASP.NET Razor 페이지를 사용 하려면 Visual Studio의 기능을 사용 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="25826-109">How to use features in Visual Studio to work with ASP.NET Razor pages, including IntelliSense and the debugger.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="25826-110">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="25826-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="25826-111">ASP.NET 웹 페이지 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="25826-111">ASP.NET Web Pages (Razor) 3</span></span>
> - <span data-ttu-id="25826-112">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="25826-112">Visual Studio 2013</span></span>
> - <span data-ttu-id="25826-113">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="25826-113">WebMatrix 3</span></span>
>   
> 
> <span data-ttu-id="25826-114">이 자습서에서는 ASP.NET 웹 페이지 2, Visual Studio 2012, Visual Studio 2010 및 WebMatrix 2 에서도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="25826-114">This tutorial also works with ASP.NET Web Pages 2, Visual Studio 2012, Visual Studio 2010, and WebMatrix 2.</span></span>


<span data-ttu-id="25826-115">WebMatrix 또는 다른 많은 코드 편집기를 사용 하 여 Razor 구문이 있는 ASP.NET 웹 페이지를 프로그래밍할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25826-115">You can program ASP.NET Web pages with Razor syntax using WebMatrix or many other code editors.</span></span> <span data-ttu-id="25826-116">여러 유형의 응용 프로그램 (뿐 아니라 웹 사이트)를 만들기 위한 강력한 여러 도구를 제공 하는 모든 기능을 갖춘 통합된 개발 환경 (IDE) 인 Microsoft Visual Studio를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25826-116">You can also use Microsoft Visual Studio which is a full-featured integrated development environment (IDE) that provides a powerful set of tools for creating many types of applications (not just websites).</span></span> <span data-ttu-id="25826-117">ASP.NET Razor 페이지를 사용 하려면 Visual Studio의 전체 버전 중 하나를 사용 하거나 무료 [Visual Studio Express for Web](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-2013-express) 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="25826-117">To work with ASP.NET Razor pages, you can either use one of the full editions of Visual Studio or the free [Visual Studio Express for Web](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-2013-express) edition.</span></span>

<span data-ttu-id="25826-118">ASP.NET Razor 웹 페이지를 사용 하 여 프로그래밍에 대 한 Visual Studio에서 제공 하는 두 개의 특히 유용한 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="25826-118">Two particularly useful features that Visual Studio provides for programming with ASP.NET Razor web pages are:</span></span>

- <span data-ttu-id="25826-119">*IntelliSense*합니다.</span><span class="sxs-lookup"><span data-stu-id="25826-119">*IntelliSense*.</span></span> <span data-ttu-id="25826-120">IntelliSense 기능은 Visual Studio에 빌드됩니다 WebMatrix에서 IntelliSense 보다 더 포괄적입니다.</span><span class="sxs-lookup"><span data-stu-id="25826-120">The IntelliSense feature built into Visual Studio is more comprehensive than IntelliSense in WebMatrix.</span></span>
- <span data-ttu-id="25826-121">*디버거*합니다.</span><span class="sxs-lookup"><span data-stu-id="25826-121">*Debugger*.</span></span> <span data-ttu-id="25826-122">디버거를 사용 하면 코드 실행, 변수를 검사 하 고 여 한 줄씩 코드를 단계별로 실행 하면 프로그램을 중지 하 여 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25826-122">The debugger lets you troubleshoot your code by stopping a program while it's running, examining variables, and stepping through the code line by line.</span></span>

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a><span data-ttu-id="25826-123">ASP.NET 웹 페이지의 서로 다른 버전의 Visual Studio 사용</span><span class="sxs-lookup"><span data-stu-id="25826-123">Using Visual Studio with Different Versions of ASP.NET Web Pages</span></span>

<span data-ttu-id="25826-124">Visual Studio 2012 및 Visual Studio 2013에는 ASP.NET 웹 페이지에 대 한 지원이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="25826-124">Visual Studio 2012 and Visual Studio 2013 include support for ASP.NET Web Pages.</span></span> <span data-ttu-id="25826-125">(ASP.NET 웹 페이지를 지원 하기 위해 필요한 패키지가 설치 되어 Visual Studio를 설치 합니다.)</span><span class="sxs-lookup"><span data-stu-id="25826-125">(The packages that are required in order to support ASP.NET Web Pages are installed when you install Visual Studio.)</span></span>

<span data-ttu-id="25826-126">Visual Studio 2010 지원을 포함 하지 않습니다 기본적으로 ASP.NET 웹 페이지에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="25826-126">Visual Studio 2010 does not include support by default for ASP.NET Web Pages.</span></span> <span data-ttu-id="25826-127">ASP.NET 웹 페이지에서 Visual Studio 2010을 사용 하려면 ASP.NET MVC 패키지를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25826-127">To use ASP.NET Web Pages with Visual Studio 2010, you must install the ASP.NET MVC package.</span></span> <span data-ttu-id="25826-128">ASP.NET 웹 페이지 2를 얻기 위해 ASP.NET MVC 4를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="25826-128">To get ASP.NET Web Pages 2, you install ASP.NET MVC 4.</span></span>

<span data-ttu-id="25826-129">다음 표에서 다양 한 버전의 Visual Studio에서 ASP.NET 웹 페이지에 대 한 지원이 요약 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25826-129">The following table summarizes the support for ASP.NET Web Pages in different versions of Visual Studio.</span></span>

|  | <span data-ttu-id="25826-130">Visual Studio 2010</span><span class="sxs-lookup"><span data-stu-id="25826-130">Visual Studio 2010</span></span> | <span data-ttu-id="25826-131">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="25826-131">Visual Studio 2012</span></span> | <span data-ttu-id="25826-132">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="25826-132">Visual Studio 2013</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="25826-133">**ASP.NET 웹 페이지 2**</span><span class="sxs-lookup"><span data-stu-id="25826-133">**ASP.NET Web Pages 2**</span></span> | <span data-ttu-id="25826-134">ASP.NET MVC 4를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="25826-134">Install ASP.NET MVC 4</span></span> | <span data-ttu-id="25826-135">(포함)</span><span class="sxs-lookup"><span data-stu-id="25826-135">(Included)</span></span> | <span data-ttu-id="25826-136">(포함)</span><span class="sxs-lookup"><span data-stu-id="25826-136">(Included)</span></span> |
| <span data-ttu-id="25826-137">**ASP.NET 웹 페이지 3**</span><span class="sxs-lookup"><span data-stu-id="25826-137">**ASP.NET Web Pages 3**</span></span> |  | <span data-ttu-id="25826-138">ASP.NET 웹에 업데이트 3부터 NuGet 페이지</span><span class="sxs-lookup"><span data-stu-id="25826-138">Update to ASP.NET Web Pages 3 through NuGet</span></span> | <span data-ttu-id="25826-139">(포함)</span><span class="sxs-lookup"><span data-stu-id="25826-139">(Included)</span></span> |

<span data-ttu-id="25826-140">Visual Studio 2010을 사용 하려면 참조 [Visual Studio 2010의 ASP.NET 웹 페이지에 대 한 지원 설치](#vs2010support)합니다.</span><span class="sxs-lookup"><span data-stu-id="25826-140">To work with Visual Studio 2010, see [Installing Support for ASP.NET Web Pages in Visual Studio 2010](#vs2010support).</span></span>

## <a name="launching-visual-studio-from-webmatrix"></a><span data-ttu-id="25826-141">WebMatrix에서 Visual Studio를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="25826-141">Launching Visual Studio from WebMatrix</span></span>

<span data-ttu-id="25826-142">WebMatrix에서 프로젝트를 시작 하 고 Visual Studio로 전환 하려고 할 경우 WebMatrix를 쉽게 Visual Studio에서 프로젝트를 열 수 있는 단추를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="25826-142">If you have started a project in WebMatrix and want to switch to Visual Studio, WebMatrix provides a button to easily open the project in Visual Studio.</span></span> <span data-ttu-id="25826-143">사용 하도록 Visual Studio이이 단추에 대 한 컴퓨터에 설치 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25826-143">You must have Visual Studio installed on your computer for this button to be enabled.</span></span> <span data-ttu-id="25826-144">다음 이미지는 WebMatrix에서 단추를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="25826-144">The following image shows the button in WebMatrix.</span></span>

![Visual Studio 시작](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

<span data-ttu-id="25826-146">단추를 클릭할 때 Visual Studio에서 프로젝트를 열입니다.</span><span class="sxs-lookup"><span data-stu-id="25826-146">When you click the button, the project is opened in Visual Studio.</span></span> <span data-ttu-id="25826-147">전환할 수 있습니다 간에 WebMatrix 및 Visual Studio 간의 문제 없이.</span><span class="sxs-lookup"><span data-stu-id="25826-147">You can switch back and forth between WebMatrix and Visual Studio without any problems.</span></span> <span data-ttu-id="25826-148">모든 파일에 있는 다른 환경에서 변경 되 고 최신 변경 내용을 다시 로드 해야 하는 경우 알림이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="25826-148">You will be notified if any files have changed in the other environment and need to be reloaded to get the latest changes.</span></span>

## <a name="creating-aspnet-razor-site-in-visual-studio"></a><span data-ttu-id="25826-149">Visual Studio에서 ASP.NET Razor 사이트 만들기</span><span class="sxs-lookup"><span data-stu-id="25826-149">Creating ASP.NET Razor Site in Visual Studio</span></span>

<span data-ttu-id="25826-150">Visual Studio에는 ASP.NET Razor 웹 사이트를 만들려면</span><span class="sxs-lookup"><span data-stu-id="25826-150">To create an ASP.NET Razor website in Visual Studio:</span></span>

1. <span data-ttu-id="25826-151">Visual Studio 또는 Visual Web Developer를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="25826-151">Start Visual Studio or Visual Web Developer.</span></span>
2. <span data-ttu-id="25826-152">에 **파일** 메뉴를 클릭 하 여 **새 웹 사이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="25826-152">In the **File** menu, click **New Web Site**.</span></span>

    ![새 웹 사이트 만들기](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. <span data-ttu-id="25826-154">에 **새 웹 사이트** 대화 상자 (Visual C# 또는 Visual Basic)를 사용할 언어를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="25826-154">In the **New Web Site** dialog box, select the language to use (Visual C# or Visual Basic).</span></span>
4. <span data-ttu-id="25826-155">선택 된 **ASP.NET 웹 사이트 (Razor)** 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="25826-155">Select the **ASP.NET Web Site (Razor)** template.</span></span>

    ![razor 사이트](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. <span data-ttu-id="25826-157">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="25826-157">Click **OK**.</span></span>

<span data-ttu-id="25826-158">새 프로젝트에 존재 하 고 시작할 수 있도록 몇 가지 기본 웹 페이지와 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="25826-158">Your new project exists and is populated with some default web pages to help you get started.</span></span>

### <a name="using-intellisense"></a><span data-ttu-id="25826-159">IntelliSense 사용</span><span class="sxs-lookup"><span data-stu-id="25826-159">Using IntelliSense</span></span>

<span data-ttu-id="25826-160">사이트를 만들었으므로 이제 IntelliSense Visual Studio에서 작동 하는 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25826-160">Now that you've created a site, you can see how IntelliSense works in Visual Studio.</span></span>

1. <span data-ttu-id="25826-161">방금 만든 웹 사이트를 열고는 *Default.cshtml* 페이지.</span><span class="sxs-lookup"><span data-stu-id="25826-161">In the website you just created, open the *Default.cshtml* page.</span></span>
2. <span data-ttu-id="25826-162">이후에 `<h3>` 는 페이지의 태그에에서 입력 `@ServerInfo.` (점 포함).</span><span class="sxs-lookup"><span data-stu-id="25826-162">After the `<h3>` tags in the page, type `@ServerInfo.` (including the dot).</span></span> <span data-ttu-id="25826-163">IntelliSense를 사용할 수 있는 메서드를 표시 하는 방법을 확인할 수는 `ServerInfo` 드롭 다운 목록에서 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="25826-163">Notice how IntelliSense displays the available methods for the `ServerInfo` helper in a drop-down list.</span></span> 

    ![intellisense](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. <span data-ttu-id="25826-165">선택 된 `GetHtml` 메서드 목록 및 다음 Enter 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="25826-165">Select the `GetHtml` method from the list and then press Enter.</span></span> <span data-ttu-id="25826-166">IntelliSense는 자동으로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="25826-166">IntelliSense automatically fills in the method.</span></span> <span data-ttu-id="25826-167">(C#에서 어떤 방법으로 추가 해야 하는 대로 `()` 메서드 뒤의 문자가 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="25826-167">(As with any method in C#, you must add `()` characters after the method.)</span></span>  
   <span data-ttu-id="25826-168">에 대 한 완성 된 코드는 `GetHtml` 메서드는 다음 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="25826-168">The completed code for the `GetHtml` method looks like the following example:</span></span>  

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. <span data-ttu-id="25826-169">페이지를 실행 하려면 Ctrl + f 5를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="25826-169">Press Ctrl+F5 to run the page.</span></span> <span data-ttu-id="25826-170">다음은 브라우저에 표시 된 때 같이 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="25826-170">This is what the page looks like when displayed in a browser:</span></span> 

    ![브라우저에서 기본 페이지](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. <span data-ttu-id="25826-172">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="25826-172">Close the browser.</span></span>

### <a name="using-the-debugger"></a><span data-ttu-id="25826-173">디버거를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="25826-173">Using the Debugger</span></span>

1. <span data-ttu-id="25826-174">맨 위에 있는 *Default.cshtml* 로 시작 하는 줄 뒤의 페이지 `Page.Title`, 코드의 다음 줄 추가:</span><span class="sxs-lookup"><span data-stu-id="25826-174">At the top of the *Default.cshtml* page, after the line that begins with `Page.Title`, add the following line of code:</span></span> 

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. <span data-ttu-id="25826-175">편집기에는 코드 왼쪽의 회색 여백을 클릭 하 여이 새 줄 옆에 있는 추가 *중단점*합니다.</span><span class="sxs-lookup"><span data-stu-id="25826-175">In the gray margin of the editor to the left of the code, click next to this new line in order to add a *breakpoint*.</span></span> <span data-ttu-id="25826-176">중단점이 발생 하는 작업을 볼 수 있도록 해당 지점에서 프로그램 실행을 중지 하도록 디버거에 지시는 표식입니다.</span><span class="sxs-lookup"><span data-stu-id="25826-176">A breakpoint is a marker that tells the debugger to stop running the program at that point so you can see what's happening.</span></span>

    ![설정 된 중단점](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. <span data-ttu-id="25826-178">호출을 제거는 `ServerInfo.GetHtml` 메서드를 호출을 추가 하 고는 `@myTime` 그 자리에 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="25826-178">Remove the call to the `ServerInfo.GetHtml` method, and add a call to the `@myTime` variable in its place.</span></span> <span data-ttu-id="25826-179">이 호출은 새 코드 줄에서 반환 되는 현재 시간 값을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="25826-179">This call displays the current time value that's returned by the new line of code.</span></span>
4. <span data-ttu-id="25826-180">F5 키를 눌러 디버거에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="25826-180">Press F5 to run the page in the debugger.</span></span> <span data-ttu-id="25826-181">페이지는 설정한 중단점에서 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="25826-181">The page stops on the breakpoint that you set.</span></span> <span data-ttu-id="25826-182">다음 이미지 모양을 보여 줍니다 페이지 편집기에서 (노란색)에 있는 중단점.</span><span class="sxs-lookup"><span data-stu-id="25826-182">The following image shows what the page looks like in the editor with the breakpoint (in yellow).</span></span> 

    ![디버그 중단점](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. <span data-ttu-id="25826-184">디버그 도구 모음에서을 클릭는 **한 단계씩 코드 실행** 단추 (또는 F11 키를 눌러) 코드의 다음 줄을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="25826-184">In the Debug toolbar, click the **Step Into** button (or press F11) to run the next line of code.</span></span> <span data-ttu-id="25826-185">코드의 다음 줄 실행을 진행 하면이 단추를 클릭할 때마다 합니다.</span><span class="sxs-lookup"><span data-stu-id="25826-185">Each time you click this button, you advance the execution to the next line of code.</span></span>

    ![단추를 한 단계씩](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. <span data-ttu-id="25826-187">값을 검사는 `myTime` 위로 마우스 포인터를 보유 하거나에 표시 된 값을 검사 하 여 변수는 **지역** 및 **호출 스택** windows 합니다.</span><span class="sxs-lookup"><span data-stu-id="25826-187">Examine the value of the `myTime` variable by holding your mouse pointer over it or by inspecting the values displayed in the **Locals** and **Call Stack** windows.</span></span> <span data-ttu-id="25826-188">Visual Studio는 변수의 값을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="25826-188">Visual Studio display the value of the variable.</span></span>

    ![시간 표시 값](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. <span data-ttu-id="25826-190">완료 하면 변수를 검사 하 고 코드를 단계별로 페이지를 실행 하면 각 줄에서 중지 하지 않고 계속 하려면 F5 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="25826-190">When you're done examining the variable and stepping through code, press F5 to continue running the page without stopping at each line.</span></span> <span data-ttu-id="25826-191">모든 코드를 단계별로 했으면 브라우저의 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="25826-191">When you've finished stepping through all the code, the browser displays the page.</span></span>

<span data-ttu-id="25826-192">디버거 Visual Studio에서 코드를 디버깅 하는 방법에 대 한 자세한 내용은 참조 [연습: Visual Web Developer에서 웹 페이지 디버깅](https://msdn.microsoft.com/library/z9e7w6cs.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="25826-192">To learn more about the debugger and about how to debug code in Visual Studio, see [Walkthrough: Debugging Web Pages in Visual Web Developer](https://msdn.microsoft.com/library/z9e7w6cs.aspx).</span></span>

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a><span data-ttu-id="25826-193">Razor를 사용 하 여 Visual Studio를 사용 하 여 ASP.NET MVC 프로젝트의</span><span class="sxs-lookup"><span data-stu-id="25826-193">Using Razor in ASP.NET MVC projects with Visual Studio</span></span>

<span data-ttu-id="25826-194">ASP.NET MVC 프로젝트에는 Razor 구문은 광범위 하 게도 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="25826-194">The Razor syntax is also used extensively in ASP.NET MVC projects.</span></span> <span data-ttu-id="25826-195">MVC는 동적 웹 사이트를 구축 하는 기능을 강력한 패턴 기반의 방법을입니다.</span><span class="sxs-lookup"><span data-stu-id="25826-195">MVC is a powerful, patterns-based way to build dynamic websites.</span></span> <span data-ttu-id="25826-196">ASP.NET 웹 페이지 사이트를 관리 하기 어려울 경우 ASP.NET MVC 응용 프로그램을 변환 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="25826-196">If your ASP.NET Web Pages site becomes difficult to maintain, you might want to consider converting it to an ASP.NET MVC application.</span></span> <span data-ttu-id="25826-197">MVC 응용 프로그램을 만드는 예제를 보려면 [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="25826-197">For an example of creating an MVC application, see [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a><span data-ttu-id="25826-198">Visual Studio 2010의 ASP.NET 웹 페이지에 대 한 지원 기능을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="25826-198">Installing Support for ASP.NET Web Pages in Visual Studio 2010</span></span>

<span data-ttu-id="25826-199">이 섹션에는 Visual Studio 용 Visual Web Developer Express 2010 및 ASP.NET 웹 페이지 도구를 설치 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="25826-199">This section shows how to install Visual Web Developer Express 2010 and the ASP.NET Web Pages Tools for Visual Studio.</span></span>

1. <span data-ttu-id="25826-200">웹 플랫폼 설치 관리자를 아직 없는 경우 다음 URL에서 다운로드:</span><span class="sxs-lookup"><span data-stu-id="25826-200">If you don't already have the Web Platform Installer, download it from the following URL:</span></span>

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. <span data-ttu-id="25826-201">웹 플랫폼 설치 관리자를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="25826-201">Run the Web Platform Installer.</span></span>
3. <span data-ttu-id="25826-202">클릭는 **제품** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="25826-202">Click the **Products** tab.</span></span>

    ![WebPI 제품 탭](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. <span data-ttu-id="25826-204">검색할 **ASP.NET MVC 4** (ASP.NET 웹 페이지 2)에 대 한 다음를 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="25826-204">Search for **ASP.NET MVC 4** (for ASP.NET Web Pages 2) and then click **Add**.</span></span> <span data-ttu-id="25826-205">이러한 제품에는 ASP.NET Razor 웹 사이트를 구축 하기 위한 Visual Studio 도구가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="25826-205">These products include Visual Studio tools for building ASP.NET Razor websites.</span></span>

    ![WebPi 설치 옵션](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. <span data-ttu-id="25826-207">클릭 **설치** 설치를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="25826-207">Click **Install** to complete the installation.</span></span>
