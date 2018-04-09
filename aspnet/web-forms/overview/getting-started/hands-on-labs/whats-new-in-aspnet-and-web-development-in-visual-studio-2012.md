---
uid: web-forms/overview/getting-started/hands-on-labs/whats-new-in-aspnet-and-web-development-in-visual-studio-2012
title: ASP.NET 및 Visual Studio 2012에서 웹 개발의 새로운 기능 | Microsoft Docs
author: rick-anderson
description: 새 버전의 Visual Studio 웹 기술을 사용 하는 경우, 환경 및 성능 향상에 초점을 맞춘 향상 된 기능 소개 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: 6d40d276-1642-4a77-b6c9-02ac914f6805
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/whats-new-in-aspnet-and-web-development-in-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: 00b43cc548df44edded925521991a095ed856494
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="whats-new-in-aspnet-and-web-development-in-visual-studio-2012"></a><span data-ttu-id="45245-103">ASP.NET 및 Visual Studio 2012에서 웹 개발의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="45245-103">What's New in ASP.NET and Web Development in Visual Studio 2012</span></span>
====================
<span data-ttu-id="45245-104">으로 [웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="45245-104">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> <span data-ttu-id="45245-105">새 버전의 Visual Studio 웹 기술을 사용 하는 경우, 환경 및 성능 향상에 초점을 맞춘 향상 된 여러 가지를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-105">The new version of Visual Studio introduces a number of enhancements focused on improving the experience and performance when working with Web technologies.</span></span> <span data-ttu-id="45245-106">Visual Studio 편집기, CSS, JavaScript 및 HTML에 대 한 다양 한 IntelliSense 및 자동 들여쓰기 등 가장 많이 코드 보조 기능을 포함 하도록 완전히 새롭게 수정 되었습니다 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-106">Visual Studio Editors for CSS, JavaScript and HTML have been completely revamped to include many of the most in-demand code aids, such as IntelliSense and automatic indentation.</span></span> <span data-ttu-id="45245-107">성능과 관련 하 여 묶음 및 축소는 이제 처럼 통합 페이지를 쉽게 줄일 수 있는 기본 제공 기능도 로드 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-107">Regarding performance, bundling and minification are now integrated as built-in features to easily reduce page load time.</span></span>
> 
> <span data-ttu-id="45245-108">Visual Studio를 사용 하면 최신 웹 기술을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-108">Visual Studio enables you to work with the latest website technologies.</span></span> <span data-ttu-id="45245-109">사이트는 클라이언트 플랫폼에 관계 없이 새로운 HTML5 요소와 기능을 활용 하기 위해 하는 동안 작동 하는지 확인 하려면 브라우저 간 CSS3 코드 조각을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-109">You can use cross-browser CSS3 Snippets to make sure your site works regardless of the client platform while also taking advantage of the new HTML5 elements and features.</span></span>
> 
> <span data-ttu-id="45245-110">작성 하 고 JavaScript 코드 프로 파일링이 Visual Studio 버전 보다 쉽게 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-110">Writing and profiling JavaScript code should be easier with this Visual Studio version.</span></span> <span data-ttu-id="45245-111">IntelliSense 목록 통합 XML 설명서 및 탐색 기능은 이제 JavaScript 코드에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-111">IntelliSense lists, integrated XML documentation and navigation features are now available for JavaScript code.</span></span> <span data-ttu-id="45245-112">이제 손쉽게 JavaScript 카탈로그를 준비 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-112">You now have the JavaScript catalog at your fingertips.</span></span> <span data-ttu-id="45245-113">또한 스크립트에 ECMAScript5 준수 하는지 확인할 수 있으며 초기 단계에서 구문 오류를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-113">Additionally, you can check ECMAScript5 compliance with your scripts and detect syntax errors at an early stage.</span></span>
> 
> <span data-ttu-id="45245-114">마지막으로, 기본 제공 묶음 및 축소가 Visual Studio 버전을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-114">Last but not least, this Visual Studio version implements built-in bundling and minification.</span></span> <span data-ttu-id="45245-115">스크립트 파일 및 스타일 시트 압축 고 사이트를 더 빠르게 수행을 압축 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-115">Your script files and style sheets will be packed and compressed so that the site performs faster.</span></span>
> 
> <span data-ttu-id="45245-116">이 랩에서 원본 폴더에 제공 된 샘플 웹 응용 프로그램에 사소한 변경 내용을 적용 하 여 이전에 설명 된 새로운 기능 및 향상 된 기능을 통해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-116">This lab walks you through the enhancements and new features previously described by applying minor changes to a sample Web application provided in the Source folder.</span></span>
> 
> <span data-ttu-id="45245-117">모든 샘플 코드와 코드 조각을 웹 캠프 교육 키트에서 사용할 수에 포함 된 [ https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409 ](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-117">All sample code and snippets are included in the Web Camps Training Kit, available at [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).</span></span>


<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="45245-118">목표</span><span class="sxs-lookup"><span data-stu-id="45245-118">Objectives</span></span>

<span data-ttu-id="45245-119">이 바늘 랩에 설명 합니다 하는 방법:</span><span class="sxs-lookup"><span data-stu-id="45245-119">In this hands on lab, you will learn how to:</span></span>

- <span data-ttu-id="45245-120">CSS 편집기에서 새 기능과 향상 된 기능을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="45245-120">Use the new features and improvements in the CSS editor</span></span>
- <span data-ttu-id="45245-121">HTML 편집기에서 새 기능과 향상 된 기능을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="45245-121">Use the new features and improvements in the HTML editor</span></span>
- <span data-ttu-id="45245-122">새 기능과 향상 된 기능을 사용 하 여 JavaScript 편집기에서</span><span class="sxs-lookup"><span data-stu-id="45245-122">Use the new features and improvements in the JavaScript editor</span></span>
- <span data-ttu-id="45245-123">구성 하 고 묶음 및 축소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-123">Configure and use bundling and minification</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="45245-124">전제 조건</span><span class="sxs-lookup"><span data-stu-id="45245-124">Prerequisites</span></span>

- <span data-ttu-id="45245-125">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) 하거나 그 보다 뛰어난 (읽기 [부록 A](#AppendixA) 설치 하는 방법에 대 한 지침은).</span><span class="sxs-lookup"><span data-stu-id="45245-125">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>
- <span data-ttu-id="45245-126">[Windows PowerShell](https://support.microsoft.com/kb/968930/) (스크립트에 대 한 설치 프로그램-이미 Windows 8 및 Windows Server 2008 r 2에 설치)</span><span class="sxs-lookup"><span data-stu-id="45245-126">[Windows PowerShell](https://support.microsoft.com/kb/968930/) (for setup scripts - already installed on Windows 8 and Windows Server 2008 R2)</span></span>
- <span data-ttu-id="45245-127">[Internet Explorer 10](https://windows.microsoft.com/internet-explorer/products/ie/home) -또는 HTML5 호환 브라우저</span><span class="sxs-lookup"><span data-stu-id="45245-127">[Internet Explorer 10](https://windows.microsoft.com/internet-explorer/products/ie/home) - or an HTML5 compliant browser</span></span>

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="45245-128">연습</span><span class="sxs-lookup"><span data-stu-id="45245-128">Exercises</span></span>

<span data-ttu-id="45245-129">이 실습 랩 다음 연습에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45245-129">This hands on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="45245-130">CSS 편집기의 새로운 소식 연습 1:</span><span class="sxs-lookup"><span data-stu-id="45245-130">Exercise 1: What's New in the CSS Editor</span></span>](#Exercise1)
2. [<span data-ttu-id="45245-131">HTML 편집기의 새로운 소식 연습 2:</span><span class="sxs-lookup"><span data-stu-id="45245-131">Exercise 2: What's New in the HTML Editor</span></span>](#Exercise2)
3. [<span data-ttu-id="45245-132">JavaScript 편집기는의 새로운 소식 연습 3:</span><span class="sxs-lookup"><span data-stu-id="45245-132">Exercise 3: What's New in the JavaScript Editor</span></span>](#Exercise3)
4. [<span data-ttu-id="45245-133">연습 4: 묶음 및 축소</span><span class="sxs-lookup"><span data-stu-id="45245-133">Exercise 4: Bundling and Minification</span></span>](#Exercise4)

<span data-ttu-id="45245-134">예상 소요 시간: **60 분**합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-134">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Whats_New_in_the_CSS_Editor"></a>
### <a name="exercise-1-whats-new-in-the-css-editor"></a><span data-ttu-id="45245-135">CSS 편집기의 새로운 소식 연습 1:</span><span class="sxs-lookup"><span data-stu-id="45245-135">Exercise 1: What's New in the CSS Editor</span></span>

<span data-ttu-id="45245-136">웹 개발자 CSS 편집 관련 된 문제가 많이 잘 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-136">Web developers should be familiar with many of the difficulties related to CSS editing.</span></span> <span data-ttu-id="45245-137">CSS 스타일 지정의 가장 큰 문제 중 하나에 브라우저와 호환입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-137">One of the biggest issues of CSS styling is cross-browser compatibility.</span></span> <span data-ttu-id="45245-138">또한, 사이트에 스타일 적용 알게 달라 보입니다 다른 브라우저 또는 장치에서 열 경우 이러한 상황이 자주 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-138">It often happens that, after applying styles to your site, you notice that it looks different if you open it in another browser or device.</span></span> <span data-ttu-id="45245-139">따라서, 마지막으로 한 브라우저에서 작동을 만들면 나뉘어집니다은 다른 실현 하려면 이러한 시각적 문제 해결에 대 시간이 상당히를 소비할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-139">Therefore, you may spend a considerable time on fixing those visual issues to realize that, when you finally make it work in one browser, it is broken in the others.</span></span>

<span data-ttu-id="45245-140">이제 visual Studio에 기능을 액세스, 작업 및 CSS 스타일 시트를 효과적으로 구성 하는 개발자가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45245-140">Visual Studio now includes features that help developers access, work and organize CSS style sheets effectively.</span></span> <span data-ttu-id="45245-141">이 연습에서 유효한 조직 및 버전에 대 한 새로운 기능 뿐 아니라 다중 브라우저 호환성을 위해 CSS3 코드 조각을 회의 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-141">Throughout this exercise, you will meet the new features for an effective organization and edition, as well as the CSS3 Code Snippets for cross-browser compatibility.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_New_Editor_Features"></a>
#### <a name="task-1---new-editor-features"></a><span data-ttu-id="45245-142">작업 1-새 편집기 기능</span><span class="sxs-lookup"><span data-stu-id="45245-142">Task 1 - New Editor Features</span></span>

<span data-ttu-id="45245-143">이 작업에서 CSS 편집기의 새로운 기능을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-143">In this task, you will discover the new features of the CSS Editor.</span></span> <span data-ttu-id="45245-144">이 새 편집기를 사용 하는 새 스마트 들여쓰기, 향상 된 코드 주석을 및 향상 된 IntelliSense 목록 사용 하 여 생산성을 높일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-144">This new editor will help you increase your productivity by taking advantage of the new smart indentation, the improved code comments and the enhanced IntelliSense list.</span></span>

1. <span data-ttu-id="45245-145">시작 **Visual Studio** 엽니다는 **WhatsNewASPNET.sln** 솔루션에 있는 **Source\WhatsNewASPNET** 이 랩의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-145">Start **Visual Studio** and open the **WhatsNewASPNET.sln** solution located in the **Source\WhatsNewASPNET** folder of this lab.</span></span>
2. <span data-ttu-id="45245-146">솔루션 탐색기에서 열고는 **Site.css** 에 있는 파일에는 **스타일** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-146">In Solution Explorer, open the **Site.css** file located under the **Styles** folder.</span></span> <span data-ttu-id="45245-147">있는지 확인은 **텍스트 편집기** 도구 모음의 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45245-147">Make sure the **Text Editor** tools are visible on the toolbar.</span></span> <span data-ttu-id="45245-148">선택 하는 작업을 수행 하는 **보기** | **도구 모음** 메뉴 옵션을 확인 하 고는 **텍스트 편집기** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-148">To do that, select the **View** | **Toolbars** menu option, and check the **Text Editor** options.</span></span> <span data-ttu-id="45245-149">이 새 버전부터, 것을 확인할 수 있습니다는 **주석** 단추 (![주석 단추](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image1.png) ) 및 **주석 제거** 단추 (![주석 처리 제거 단추](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image2.png))도 CSS 편집기에 대 한 사용 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-149">You will notice that, since this new version, the **Comment** button (![comment-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image1.png) ) and the **Uncomment** button (![uncomment-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image2.png) ) are also enabled for the CSS editor.</span></span>

    <span data-ttu-id="45245-150">![편집기 및 CSS 도구를 사용 하도록 설정](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image3.png "편집기 및 CSS 도구를 사용 하도록 설정")</span><span class="sxs-lookup"><span data-stu-id="45245-150">![Enabling Editor and CSS Tools](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image3.png "Enabling Editor and CSS Tools")</span></span>

    <span data-ttu-id="45245-151">*편집기 및 CSS 도구를 사용 하도록 설정*</span><span class="sxs-lookup"><span data-stu-id="45245-151">*Enabling Editor and CSS Tools*</span></span>
3. <span data-ttu-id="45245-152">코드를 스크롤하여 모든 CSS 클래스 정의 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-152">Scroll the code and select any CSS class definition.</span></span> <span data-ttu-id="45245-153">클릭는 **주석** (![주석 단추](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image4.png) ) 단추를 선택한 줄을 주석 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-153">Click the **Comment** (![comment-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image4.png) ) button to comment the selected lines.</span></span> <span data-ttu-id="45245-154">클릭는 **주석 제거** (![주석 처리 제거 단추](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image5.png) )는 변경 내용을 취소 하는 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-154">Then, click the **Uncomment** (![uncomment-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image5.png) ) button to undo the changes.</span></span>
4. <span data-ttu-id="45245-155">클릭는 **축소** (![축소](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image6.png) ) 및 **확장** (![확장](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image7.png) ) 텍스트의 왼쪽된 여백에 단추가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-155">Click the **Collapse** (![collapse](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image6.png) ) and **Expand** (![expand](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image7.png) ) buttons located on the left margin of the text.</span></span> <span data-ttu-id="45245-156">알림 지금 사용 하지 않는 한 클리너 뷰 스타일 숨길 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-156">Notice that you can now hide the styles you don't use to have a cleaner view.</span></span>

    <span data-ttu-id="45245-157">![CSS 클래스 축소](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image8.png "축소 CSS 클래스")</span><span class="sxs-lookup"><span data-stu-id="45245-157">![Collapsing CSS classes](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image8.png "Collapsing CSS classes")</span></span>

    <span data-ttu-id="45245-158">*CSS 클래스를 축소합니다.*</span><span class="sxs-lookup"><span data-stu-id="45245-158">*Collapsing CSS classes*</span></span>
5. <span data-ttu-id="45245-159">스마트 들여쓰기 기능이 설정 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-159">Make sure that the smart indentation feature is enabled.</span></span> <span data-ttu-id="45245-160">선택 된 **도구** | **옵션** 메뉴 옵션을 선택한 후는 **텍스트 편집기** | **CSS**  |  **서식** 화면의 왼쪽된 창에서 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-160">Select the **Tools** | **Options** menu option, and then select the **Text Editor** | **CSS** | **Formatting** page in the left pane of the screen.</span></span> <span data-ttu-id="45245-161">확인 된 **계층적 들여쓰기** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-161">Check the **Hierarchical indentation** option.</span></span>

    <span data-ttu-id="45245-162">![계층적 들여쓰기를 사용 하도록 설정](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image9.png "계층적 들여쓰기를 사용 하도록 설정")</span><span class="sxs-lookup"><span data-stu-id="45245-162">![Enabling hierarchical indentation](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image9.png "Enabling hierarchical indentation")</span></span>

    <span data-ttu-id="45245-163">*계층적 들여쓰기를 사용 하도록 설정*</span><span class="sxs-lookup"><span data-stu-id="45245-163">*Enabling hierarchical indentation*</span></span>
6. <span data-ttu-id="45245-164">기본 클래스 정의 (.main)를 찾아서 div 요소에 스타일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-164">Locate the main class definition (.main) and append a style to the div elements.</span></span> <span data-ttu-id="45245-165">코드를 한 눈에 부모 클래스를 찾을 수 있도록 지 원하는 사용자가 자동으로 맞춥니다 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-165">You will notice that the code aligns automatically, helping users to find the parent classes at a glance.</span></span>

    <span data-ttu-id="45245-166">CSS</span><span class="sxs-lookup"><span data-stu-id="45245-166">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample1.css)]

    <span data-ttu-id="45245-167">![CSS에서 맞춤의 계층적](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image10.png "CSS에서 계층적 맞춤")</span><span class="sxs-lookup"><span data-stu-id="45245-167">![Hierarchical alignment in CSS](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image10.png "Hierarchical alignment in CSS")</span></span>

    <span data-ttu-id="45245-168">*CSS에서 계층적 맞춤*</span><span class="sxs-lookup"><span data-stu-id="45245-168">*Hierarchical alignment in CSS*</span></span>
7. <span data-ttu-id="45245-169">내부 **.main div** 클래스, 커서의 끝에 찾을 **테두리: 0px;** 한 키를 누릅니다 **Enter** IntelliSense 목록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-169">Inside **.main div** class, locate the cursor at the end of **border: 0px;** and press **Enter** to display the IntelliSense list.</span></span> <span data-ttu-id="45245-170">입력을 시작 **top** 을 입력할 때 목록이 필터링 되어 어떻게 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-170">Start typing **top** and notice how the list is filtered as you type.</span></span> <span data-ttu-id="45245-171">목록으로 포함 된 요소에 표시 됩니다 **위쪽** 단어의 모든 부분에서 (Visual Studio의 이전 버전에서 목록 항목에 의해 필터링 됩니다 하 *시작* 는 단어와 함께).</span><span class="sxs-lookup"><span data-stu-id="45245-171">The list will display the elements that contain **top** at any part of the word (In prior versions of Visual Studio, the list is filtered by the items that *begin* with the term).</span></span>

    <span data-ttu-id="45245-172">![Css에서 IntelliSense의 향상 된 기능](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image11.png "css에서 IntelliSense의 향상 된 기능")</span><span class="sxs-lookup"><span data-stu-id="45245-172">![IntelliSense enhancements in CSS](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image11.png "IntelliSense enhancements in CSS")</span></span>

    <span data-ttu-id="45245-173">*Css에서 IntelliSense의 향상 된 기능*</span><span class="sxs-lookup"><span data-stu-id="45245-173">*IntelliSense enhancements in CSS*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_The_Color_Picker"></a>
#### <a name="task-2---the-color-picker"></a><span data-ttu-id="45245-174">작업 2-색 선택</span><span class="sxs-lookup"><span data-stu-id="45245-174">Task 2 - The Color Picker</span></span>

<span data-ttu-id="45245-175">이 태스크에서는 Visual Studio IntelliSense에 통합 되어 새 CSS 색 선택에서 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-175">In this task, you will discover the new CSS Color Picker integrated into Visual Studio IntelliSense.</span></span>

1. <span data-ttu-id="45245-176">**Site.css,** 헤더 클래스 정의 (.header)를 찾아 옆에 커서를 놓고 **배경색** 특성 사이 &quot;:&quot; 및 &quot; # &quot; 해당 코드 줄에 있는 문자 **합니다.**</span><span class="sxs-lookup"><span data-stu-id="45245-176">In **Site.css,** locate the header class definition (.header) and place the cursor next to **background-color** attribute, between the &quot;:&quot; and &quot;#&quot; characters on that line of code **.**</span></span>

    <span data-ttu-id="45245-177">![커서를 찾기](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image12.png "커서 찾기")</span><span class="sxs-lookup"><span data-stu-id="45245-177">![Locating the cursor](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image12.png "Locating the cursor")</span></span>

    <span data-ttu-id="45245-178">*커서 찾기*</span><span class="sxs-lookup"><span data-stu-id="45245-178">*Locating the cursor*</span></span>
2. <span data-ttu-id="45245-179">삭제 된 **콜론** (:) 색 선택을 표시를 다시 써야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-179">Delete the **colon** (:) and write it again to display the color picker.</span></span> <span data-ttu-id="45245-180">그러면 첫 번째 색 사이트의 가장 일반적인 색 확인할.</span><span class="sxs-lookup"><span data-stu-id="45245-180">Notice that the first colors you will see are the most frequent colors of your site.</span></span> <span data-ttu-id="45245-181">흰색 색을 클릭 하는 경우 해당 HTML 색 코드가 (#fff) 스타일 시트에 현재 색 코드를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-181">If you click the white color, its HTML color code (#fff) will replace the current color code in the stylesheet.</span></span>

    <span data-ttu-id="45245-182">![색 선택](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image13.png "색 선택")</span><span class="sxs-lookup"><span data-stu-id="45245-182">![Color picker](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image13.png "Color picker")</span></span>

    <span data-ttu-id="45245-183">*색 선택*</span><span class="sxs-lookup"><span data-stu-id="45245-183">*Color picker*</span></span>
3. <span data-ttu-id="45245-184">키를 눌러는 **확장** (![com](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image14.png) ) 색 그라데이션을 표시 하 고 다음 서로 다른 색을 선택 하려면 그라데이션 커서를 끌어 색 선택 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-184">Press the **Expand** (![com](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image14.png) ) button on the color picker to display the color gradient, and then drag the gradient cursor to select a different color.</span></span> <span data-ttu-id="45245-185">그 이후에 클릭는 **스 포 이트** 단추 및 화면에서 색을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-185">After that, click the **Eyedropper** button and select any color from the screen.</span></span> <span data-ttu-id="45245-186">커서를 이동 하는 동안 배경색 값 동적으로 변경 됨을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-186">Notice that background color value changes dynamically while you move the cursor.</span></span>

    <span data-ttu-id="45245-187">![색 선택기 그라데이션](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image15.png "색 선택기 그라데이션")</span><span class="sxs-lookup"><span data-stu-id="45245-187">![Color picker gradient](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image15.png "Color picker gradient")</span></span>

    <span data-ttu-id="45245-188">*색 선택기 그라데이션*</span><span class="sxs-lookup"><span data-stu-id="45245-188">*Color picker gradient*</span></span>
4. <span data-ttu-id="45245-189">에 **불투명도** 슬라이더를 불투명도 줄이기 위해 막대의 중심에 선택기를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-189">In the **Opacity** slider, move the selector to the center of the bar to reduce the opacity.</span></span> <span data-ttu-id="45245-190">배경색 값 RGBA를 해당 눈금과 지금 변경 됨을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-190">Notice that background-color value now changes its scale to RGBA.</span></span>

    <span data-ttu-id="45245-191">![색 선택 불투명도](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image16.png "불투명도 색 선택")</span><span class="sxs-lookup"><span data-stu-id="45245-191">![Color picker Opacity](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image16.png "Color picker Opacity")</span></span>

    <span data-ttu-id="45245-192">*색 선택 불투명도*</span><span class="sxs-lookup"><span data-stu-id="45245-192">*Color picker Opacity*</span></span>

    > [!NOTE]
    > <span data-ttu-id="45245-193">CSS3에 RGBA (빨강, 녹색, 파란색, Alpha) 색 정의 사용 하면 단일 항목에 대 한 색 불투명도 값을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-193">The RGBA (Red, Green, Blue, Alpha) color definition in CSS3 enables you to define the color opacity value for a single item.</span></span> <span data-ttu-id="45245-194">와 달리 **불투명도-** 비슷한 CSS 특성 **-** RGBA 색 최신 브라우저와 호환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45245-194">Unlike **opacity -** a similar CSS attribute **-** RGBA colors are also compatible with the latest browsers.</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_CSS_Compatible_Code_Snippets"></a>
#### <a name="task-3---css-compatible-code-snippets"></a><span data-ttu-id="45245-195">작업 3-CSS 호환 되는 코드 조각</span><span class="sxs-lookup"><span data-stu-id="45245-195">Task 3 - CSS Compatible Code Snippets</span></span>

<span data-ttu-id="45245-196">이 태스크에서는 웹 사이트의 일부 기능을 구현 하기 위해 브라우저 간 호환 CSS3 코드 조각을 사용 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-196">In this task, you will learn how to use cross-browser compatible CSS3 snippets in order to implement some features in your website.</span></span>

1. <span data-ttu-id="45245-197">에 **Site.css** 파일을 찾아는 **헤더** CSS 클래스 정의 (.header) 및 아래에 커서를 배치는 **/ \*테두리 radius\* /** 새 코드 조각을 추가 하는 자리 표시자입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-197">In the **Site.css** file, locate the **header** CSS class definition (.header) and place the cursor below the **/\*border radius\*/** placeholder to add a new snippet.</span></span> <span data-ttu-id="45245-198">키를 눌러 **Enter** IntelliSense 목록 및 형식을 표시 하려면 **radius** 목록을 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-198">Press **Enter** to display the IntelliSense list and type **radius** to filter the list.</span></span> <span data-ttu-id="45245-199">선택 된 **테두리 radius** 두 번 클릭을 사용 하 여 목록에서 옵션 및 다음 키를 누릅니다는 **탭** 조각을 삽입할 키입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-199">Select the **border-radius** option from the list with a double click, and then press the **TAB** key to insert the snippet.</span></span> <span data-ttu-id="45245-200">그런 다음 누릅니다 픽셀에 radius 크기를 입력 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-200">Then, type a radius size in pixels and press **Enter**.</span></span> <span data-ttu-id="45245-201">예를 들어, 입력 **15px**합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-201">For instance, type **15px**.</span></span>

    <span data-ttu-id="45245-202">조각에 추가 된 CSS3 특성 Mozilla 및 WebKit를 기반으로 하는 브라우저를 비롯 한 대부분의 HTML5 준수 브라우저에서 모퉁이가 둥근된 테두리를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-202">The CSS3 attributes added by the snippet will render rounded borders in most HTML5 compliance browsers, including Mozilla and WebKit-based browsers.</span></span>

    <span data-ttu-id="45245-203">![테두리 radius 조각을 사용 하 여](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image17.png "테두리 radius 조각을 사용 하 여")</span><span class="sxs-lookup"><span data-stu-id="45245-203">![Using a border-radius snippet](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image17.png "Using a border-radius snippet")</span></span>

    <span data-ttu-id="45245-204">*테두리 radius 조각을 사용 하 여*</span><span class="sxs-lookup"><span data-stu-id="45245-204">*Using a border-radius snippet*</span></span>
2. <span data-ttu-id="45245-205">동일 하 게 적용 **테두리** 페이지 스타일 (.page)에서 코드 조각을 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-205">Apply the same **border** snippets in the page style (.page).</span></span>

    <span data-ttu-id="45245-206">CSS</span><span class="sxs-lookup"><span data-stu-id="45245-206">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample2.css)]
3. <span data-ttu-id="45245-207">키를 눌러 **F5** 솔루션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-207">Press **F5** to run the solution.</span></span> <span data-ttu-id="45245-208">각 페이지 이제 둥근 테두리를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-208">Notice that each page now has rounded borders.</span></span>

    <span data-ttu-id="45245-209">![모퉁이가 둥근](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image18.png "모서리가 둥근 모양")</span><span class="sxs-lookup"><span data-stu-id="45245-209">![Rounded corners](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image18.png "Rounded corners")</span></span>

    <span data-ttu-id="45245-210">*둥근된 모서리*</span><span class="sxs-lookup"><span data-stu-id="45245-210">*Rounded corners*</span></span>
4. <span data-ttu-id="45245-211">브라우저를 닫고 Visual Studio로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="45245-211">Close the browser and return to Visual Studio.</span></span>
5. <span data-ttu-id="45245-212">열기는 **Custom.css** 아래에 있는 파일의 **스타일** 폴더 안에 커서를 놓고 **div.images ul li img** 클래스 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-212">Open the **Custom.css** file located under the **Styles** folder and place the cursor inside **div.images ul li img** class definition.</span></span>
6. <span data-ttu-id="45245-213">IntelliSense 목록에 표시 하려면 enter 키를 눌러 형식 **상자 그림자** 누릅니다는 **탭** 키 클래스 정의 내 기본 그림자 코드 조각을 삽입할를 두 번 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-213">Press enter to display the IntelliSense list, type **box-shadow** and press the **TAB** key twice to insert the default shadow code snippet inside the class definition.</span></span> <span data-ttu-id="45245-214">그림자의 값으로 설정 **10px 10px 5px #888**합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-214">Set the shadow values to **10px 10px 5px #888**.</span></span> <span data-ttu-id="45245-215">그런 다음 입력 **테두리 radius** 코드 조각을 삽입 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-215">Then, type **border-radius** and insert the code snippet.</span></span> <span data-ttu-id="45245-216">형식 **15px** radius 크기와 키를 눌러 설정 하려면 **ENTER**합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-216">Type **15px** to set radius size and press **ENTER**.</span></span>

    <span data-ttu-id="45245-217">![그림자가 적용 된 모퉁이가 둥근](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image19.png "그림자가 적용 된 모퉁이가 둥근")</span><span class="sxs-lookup"><span data-stu-id="45245-217">![Rounded corners with shadow](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image19.png "Rounded corners with shadow")</span></span>

    <span data-ttu-id="45245-218">*그림자가 적용 된 둥근된 모서리*</span><span class="sxs-lookup"><span data-stu-id="45245-218">*Rounded corners with shadow*</span></span>

    > [!NOTE]
    > <span data-ttu-id="45245-219">이 시점에서 섀도 특성 (moz, webkit, o) Mozilla를 지원 하기 위해 해당 접두사 및 (Chrome, Safari, Konkeror) Webkit 브라우저와 함께 삽입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45245-219">At this moment, the shadow attribute is inserted with the corresponding prefix (moz, webkit, o) to support Mozilla and Webkit (Chrome, Safari, Konkeror) browsers.</span></span>
7. <span data-ttu-id="45245-220">새 클래스를 만듭니다 **div.images ul li img:hover** 아래는 **div.images ul li img** 클래스 정의 하 고 대괄호 안에 커서를 놓고 **합니다.**</span><span class="sxs-lookup"><span data-stu-id="45245-220">Create a new class **div.images ul li img:hover** below the **div.images ul li img** class definition and place the cursor inside the brackets **.**</span></span>

    <span data-ttu-id="45245-221">CSS</span><span class="sxs-lookup"><span data-stu-id="45245-221">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample3.css)]
8. <span data-ttu-id="45245-222">형식 **변환** 누릅니다는 **탭** 변환 코드 조각을 삽입 하려면 두 번 키입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-222">Type **transform** and press the **TAB** key twice in order to insert the transform snippet.</span></span> <span data-ttu-id="45245-223">그런 다음 입력 **rotate(-15deg)** 이미지는 가져갈 때 회전 각도 값을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-223">Then, enter **rotate(-15deg)** to change the rotation angle value when images are hovered.</span></span>

    <span data-ttu-id="45245-224">CSS</span><span class="sxs-lookup"><span data-stu-id="45245-224">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample4.css)]
9. <span data-ttu-id="45245-225">키를 눌러 **F5** 하는 솔루션을 실행 하 고 CSS3 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-225">Press **F5** to run the solution and browse to the CSS3 page.</span></span> <span data-ttu-id="45245-226">이미지를 둥글게 할지에 그림자를 상자 유의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="45245-226">Notice that the images have rounded corners and box shadows.</span></span> <span data-ttu-id="45245-227">이미지 위로 마우스를 가져가고를 회전 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-227">Hover the mouse over the images and watch them rotate.</span></span>

    <span data-ttu-id="45245-228">![코드 조각 이미지 회전을 변형](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image20.png "변환 조각 이미지 회전")</span><span class="sxs-lookup"><span data-stu-id="45245-228">![Transform snippet rotating an image](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image20.png "Transform snippet rotating an image")</span></span>

    <span data-ttu-id="45245-229">*이미지 회전 조각 변형*</span><span class="sxs-lookup"><span data-stu-id="45245-229">*Transform snippet rotating an image*</span></span>

    > [!NOTE]
    > <span data-ttu-id="45245-230">그림자를 볼 수 없는 경우 Internet Explorer 10을 사용 하는 문서 모드 IE10 표준으로 설정 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-230">If you are using Internet Explorer 10 and cannot see the shadows, make sure the document mode is set to IE10 standards.</span></span> <span data-ttu-id="45245-231">키를 눌러 **F12** 를 Internet Explorer 개발자 도구를 열고 클릭 **문서 모드** IE10 표준으로 변경 하려면.</span><span class="sxs-lookup"><span data-stu-id="45245-231">Press **F12** to open Internet Explorer developer tools and click **Document Mode** to change to IE10 standards.</span></span>

    ![에 대 한-주세요.](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image21.png)

<a id="Exercise2"></a>

<a id="Exercise_2_Whats_New_in_the_HTML_Editor"></a>
### <a name="exercise-2-whats-new-in-the-html-editor"></a><span data-ttu-id="45245-233">HTML 편집기의 새로운 소식 연습 2:</span><span class="sxs-lookup"><span data-stu-id="45245-233">Exercise 2: What's New in the HTML Editor</span></span>

<span data-ttu-id="45245-234">Visual Studio에는 향상 된 HTML 편집기.</span><span class="sxs-lookup"><span data-stu-id="45245-234">Visual Studio has an improved HTML editor.</span></span> <span data-ttu-id="45245-235">이 버전에 포함 된 향상 된 기능 중 일부는 HTML 문서, HTML5 조각, HTML 시작 및 끝 태그 일치 및 HTML 유효성 검사에서 스마트 들여쓰기입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-235">Some of the enhancements included in this version are smart indentation in HTML documents, HTML5 snippets, HTML start and end tag matching, and HTML validation.</span></span> <span data-ttu-id="45245-236">이 연습에서 웹 사이트 태그에서 작업 하는 경우 이러한 변경 내용은 프로그램 fluency을 향상 하는 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-236">Throughout this exercise, you will see how these changes improve your fluency when working in the website markup.</span></span>

<span data-ttu-id="45245-237">CSS 편집기와 같은 HTML 편집기도 향상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-237">Like the CSS editor, the HTML editor was also improved.</span></span> <span data-ttu-id="45245-238">이러한 향상 된이 기능은 대부분은 웹 개발자의 작업이 더 쉽게 하는 작은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-238">Most of these improvements are small ones that make the Web developer's life easier.</span></span> <span data-ttu-id="45245-239">HTML5, 스마트 들여쓰기, 편집 및 DOCTYPE HTML 문서를 대상으로 하는 유효성 검사가 이러한 향상 된이 기능 중 일부에 일치 하는 시작 및 끝 태그에 대 한 더 많은 코드 조각을 같이.</span><span class="sxs-lookup"><span data-stu-id="45245-239">Things like more code snippets for HTML5, smart indentation, matching start and end tags when editing and validation targeting the HTML document DOCTYPE are some of these improvements.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Improved_DOCTYPE_Validation"></a>
#### <a name="task-1---improved-doctype-validation"></a><span data-ttu-id="45245-240">작업 1-향상 된 DOCTYPE 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="45245-240">Task 1 - Improved DOCTYPE Validation</span></span>

<span data-ttu-id="45245-241">HTML 편집기 마스터 페이지에는 정의가 있을 수 있지만 페이지의 DOCTYPE을 확인 하는 기능을 이제에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-241">The HTML editor now has the ability to check the DOCTYPE of your page, even though the definition might be in the master page.</span></span> <span data-ttu-id="45245-242">페이지의 DOCTYPE에 따라 HTML 편집기는 올바른 규칙 집합이와 유효성을 검사 및 DOCTYPE 요소를 고려 IntelliSense 목록 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-242">Depending on the DOCTYPE of your page, the HTML editor will validate with the correct set of rules and will filter the IntelliSense list considering the DOCTYPE elements.</span></span>

<span data-ttu-id="45245-243">이 태스크에서는 페이지의 HTML 편집기 동작에 따라 어떻게 변경 되는지 DOCTYPE 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45245-243">In this task, you will change the DOCTYPE of a page to see how the HTML editor behavior changes accordingly.</span></span>

1. <span data-ttu-id="45245-244">열려 있지 않으면 시작 **Visual Studio** 엽니다는 **WhatsNewASPNET.sln** 솔루션에 있는 **Source\WhatsNewASPNET** 이 랩의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-244">If not already opened, start **Visual Studio** and open the **WhatsNewASPNET.sln** solution located in the **Source\WhatsNewASPNET** folder of this lab.</span></span>
2. <span data-ttu-id="45245-245">열기는 **Site.Master** 페이지.</span><span class="sxs-lookup"><span data-stu-id="45245-245">Open the **Site.Master** page.</span></span>
3. <span data-ttu-id="45245-246">유효성 검사 도구 모음에 대 한 대상 스키마를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-246">Notice the Target Schema for Validation Toolbar.</span></span> <span data-ttu-id="45245-247">HTML 편집기 (유효성 검사, IntelliSense, 등)를 작동 하는 방식을 선택 문서 종류에 맞게 올바르게 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45245-247">The way the HTML editor behaves (Validation, IntelliSense, etc.) will properly change to fit the Doctype selected.</span></span>

    <span data-ttu-id="45245-248">![문서 종류를 사용 하 여 HTML 소스 편집 도구 모음의](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image22.png "HTML 소스 편집 도구 모음에서 사용 하 여 Doctype")</span><span class="sxs-lookup"><span data-stu-id="45245-248">![Use Doctype in HTML Source Editing toolbar](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image22.png "Use Doctype in HTML Source Editing toolbar")</span></span>

    <span data-ttu-id="45245-249">*HTML 소스 편집 도구 모음의 문서 종류를 사용 합니다.*</span><span class="sxs-lookup"><span data-stu-id="45245-249">*Use Doctype in HTML Source Editing toolbar*</span></span>
4. <span data-ttu-id="45245-250">HTML 4.01 대상 스키마를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-250">Change the Target Schema to HTML 4.01.</span></span>

    <span data-ttu-id="45245-251">![Doctype HTML 소스 편집 도구 모음의 변경](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image23.png "HTML 소스 편집 도구 모음의 Doctype 변경")</span><span class="sxs-lookup"><span data-stu-id="45245-251">![Changing Doctype in HTML Source Editing toolbar](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image23.png "Changing Doctype in HTML Source Editing toolbar")</span></span>

    <span data-ttu-id="45245-252">*Doctype HTML 소스 편집 도구 모음의 변경*</span><span class="sxs-lookup"><span data-stu-id="45245-252">*Changing Doctype in HTML Source Editing toolbar*</span></span>
5. <span data-ttu-id="45245-253">커서를 놓고는 **본문** 요소 및 HTML5 요소의 이름을 입력 하기 시작 (예를 들어 **비디오**).</span><span class="sxs-lookup"><span data-stu-id="45245-253">Place the cursor under the **body** element, and start typing the name of an HTML5 element (for example, **video**).</span></span> <span data-ttu-id="45245-254">요소를 IntelliSense 목록에 사용할 수 있는지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-254">Notice that the element is not available in the IntelliSense list.</span></span>

    <span data-ttu-id="45245-255">![나열 되지 않은 HTML5 요소](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image24.png "나열 되지 않은 HTML5 요소")</span><span class="sxs-lookup"><span data-stu-id="45245-255">![HTML5 elements not listed](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image24.png "HTML5 elements not listed")</span></span>

    <span data-ttu-id="45245-256">*나열 되지 않은 HTML5 요소*</span><span class="sxs-lookup"><span data-stu-id="45245-256">*HTML5 elements not listed*</span></span>
6. <span data-ttu-id="45245-257">유효성 검사 도구 모음에서 DOCTYPE 선택에 대 한 대상 스키마의 변경 내용을 실행 취소: 드롭다운 목록에서 XHTML5 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-257">Undo the changes to the Target Schema for Validation Toolbar, picking DOCTYPE: XHTML5 from the dropdown list.</span></span>

    <span data-ttu-id="45245-258">![문서 종류를 사용 하 여 HTML 소스 편집 도구 모음의](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image25.png "HTML 소스 편집 도구 모음에서 사용 하 여 Doctype")</span><span class="sxs-lookup"><span data-stu-id="45245-258">![Use Doctype in HTML Source Editing toolbar](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image25.png "Use Doctype in HTML Source Editing toolbar")</span></span>

    <span data-ttu-id="45245-259">*Doctype HTML 소스 편집 도구 모음에서 다시 설정*</span><span class="sxs-lookup"><span data-stu-id="45245-259">*Reset Doctype in HTML Source Editing toolbar*</span></span>
7. <span data-ttu-id="45245-260">커서를 놓고는 **본문** 요소 및 HTML5 요소를 다시 입력 (예: like **비디오**).</span><span class="sxs-lookup"><span data-stu-id="45245-260">Place the cursor under the **body** element and start typing an HTML5 element again (For example, like **video**).</span></span> <span data-ttu-id="45245-261">HTML5 요소를 이제 IntelliSense 목록에 사용할 수 있는지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-261">Notice that the HTML5 elements are now available in the IntelliSense list.</span></span>

    <span data-ttu-id="45245-262">![목록에 표시 하는 HTML5 요소](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image26.png "나열 되 고 HTML5 요소")</span><span class="sxs-lookup"><span data-stu-id="45245-262">![HTML5 elements being listed](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image26.png "HTML5 elements being listed")</span></span>

    <span data-ttu-id="45245-263">*목록에 표시 하는 HTML5 요소*</span><span class="sxs-lookup"><span data-stu-id="45245-263">*HTML5 elements being listed*</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_-_StartEnd_Tags_Automatic_Update"></a>
#### <a name="task-2---startend-tags-automatic-update"></a><span data-ttu-id="45245-264">작업 2-시작/끝 태그를 자동 업데이트</span><span class="sxs-lookup"><span data-stu-id="45245-264">Task 2 - Start/End Tags Automatic Update</span></span>

<span data-ttu-id="45245-265">이제 visual Studio를 열거나 닫는 서로 일치 하도록 편집 하는 요소의 태그는 HTML을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-265">Visual Studio now updates the HTML opening or closing tags of the element that you are editing to match each other.</span></span> <span data-ttu-id="45245-266">이 새로운 기능 HTML 태그를 편집할 때 생산성을 향상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45245-266">This new feature will improve your productivity when editing HTML tags.</span></span>

1. <span data-ttu-id="45245-267">에 **Default.aspx** 페이지에서 추가 된 **H3** 제목 (예를 들어 Visual Studio 2012 돌!) 인 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-267">On the **Default.aspx** page, add an **H3** element with a title (for example, Visual Studio 2012 Rocks!).</span></span>


~~~
[!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample5.aspx)]
~~~
2. <span data-ttu-id="45245-268">변경 된 **H3** 태그 및 형식 **H2** 또는 **H1 합니다.**</span><span class="sxs-lookup"><span data-stu-id="45245-268">Change the **H3** tag and type **H2** or **H1.**</span></span>

    <span data-ttu-id="45245-269">끝 태그를 자동으로 업데이트 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-269">Notice that the end tag automatically updates.</span></span> <span data-ttu-id="45245-270">시작 태그 업데이트 하도록 적절 하 게 너무 보려면 끝 태그를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-270">You can also modify the end tag to see that the start tag updates accordingly too.</span></span>

    <span data-ttu-id="45245-271">![끝 태그를 자동으로 업데이트](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image27.png "끝 태그를 자동으로 업데이트")</span><span class="sxs-lookup"><span data-stu-id="45245-271">![Automatic update of the end tag](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image27.png "Automatic update of the end tag")</span></span>

    <span data-ttu-id="45245-272">*끝 태그를 자동으로 업데이트*</span><span class="sxs-lookup"><span data-stu-id="45245-272">*Automatic update of the end tag*</span></span>

<a id="Ex2Task3"></a>

<a id="Task_3_-_New_HTML5_Code_Snippets"></a>
#### <a name="task-3---new-html5-code-snippets"></a><span data-ttu-id="45245-273">작업 3-새 HTML5 코드 조각</span><span class="sxs-lookup"><span data-stu-id="45245-273">Task 3 - New HTML5 Code Snippets</span></span>

<span data-ttu-id="45245-274">이제 visual Studio에는 몇 가지 HTML5 코드 조각을 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45245-274">Visual Studio now includes several HTML5 code snippets.</span></span> <span data-ttu-id="45245-275">이 작업에서는 이러한 조각 중 일부를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-275">In this task, you will use some of these snippets.</span></span>

1. <span data-ttu-id="45245-276">라는 새 폴더 추가 **오디오** 웹 사이트 폴더의 루트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-276">Add a new folder named **audio** to the root of the web site folder.</span></span> <span data-ttu-id="45245-277">Windows 탐색기를 열고 모든 오디오 파일을 복사는 **오디오** 의 폴더는 **WhatsNewASPNET.sln** 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-277">Open Windows Explorer and copy any audio file into the **audio** folder of the **WhatsNewASPNET.sln** solution.</span></span>
2. <span data-ttu-id="45245-278">에 **Default.aspx** 페이지에서 찾은 Web11 돌에서 커서!!</span><span class="sxs-lookup"><span data-stu-id="45245-278">In the **Default.aspx** page, locate the cursor under the Web11 Rocks!!</span></span> <span data-ttu-id="45245-279">헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-279">Header.</span></span> <span data-ttu-id="45245-280">형식 **오디오** TAB 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="45245-280">Type **audio** and press the TAB key.</span></span>

    <span data-ttu-id="45245-281">새 HTML 편집기에는 HTML5 콘텐츠에 대 한 코드 조각을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-281">The new HTML editor includes code snippets for HTML5 content.</span></span> <span data-ttu-id="45245-282">HTML5 조각 수 있도록 적절 한 문서 종류 정의 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-282">Remember to use the proper DOCTYPE definition to enable the HTML5 snippets.</span></span>

    <span data-ttu-id="45245-283">![HTML5 코드 조각 삽입](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image28.png "HTML5 코드 조각 삽입")</span><span class="sxs-lookup"><span data-stu-id="45245-283">![Inserting HTML5 Code Snippets](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image28.png "Inserting HTML5 Code Snippets")</span></span>

    <span data-ttu-id="45245-284">*HTML5 코드 조각 삽입*</span><span class="sxs-lookup"><span data-stu-id="45245-284">*Inserting HTML5 Code Snippets*</span></span>
3. <span data-ttu-id="45245-285">기존 오디오 파일을 가리키도록 오디오 소스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-285">Update the audio source to point to an existing audio file.</span></span>


~~~
[!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample6.aspx)]

> [!NOTE]
> You will need to add the audio file to the solution.
~~~
4. <span data-ttu-id="45245-286">키를 눌러 **F5** 사이트를 실행 하 여 오디오를 재생 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-286">Press **F5** to run the site and play the audio.</span></span>

    <span data-ttu-id="45245-287">![실행 중인 오디오 컨트롤](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image29.png "실행 중인 오디오 컨트롤")</span><span class="sxs-lookup"><span data-stu-id="45245-287">![Running the audio control](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image29.png "Running the audio control")</span></span>

    <span data-ttu-id="45245-288">*실행 중인 오디오 컨트롤*</span><span class="sxs-lookup"><span data-stu-id="45245-288">*Running the audio control*</span></span>

    > [!NOTE]
    > <span data-ttu-id="45245-289">비디오, 그림 등의 Visual Studio에 포함 하는 더 많은 코드 조각을 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-289">You can also try more snippets included in Visual Studio, such as video, figure, etc.</span></span>
5. <span data-ttu-id="45245-290">이제 페이지의 특정 부분에 컨트롤을 삽입 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-290">Now, try to insert a control in some part of the page.</span></span> <span data-ttu-id="45245-291">예를 들어 삽입 하려고 한 **GridView** 컨트롤을 입력 하지 않고  **&lt;gri를 보고서 작성,** 입력을 시작  **&lt;GV**합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-291">For example, try to insert a **GridView** control, but instead of typing **&lt;Gri,** start typing **&lt;GV**.</span></span> <span data-ttu-id="45245-292">IntelliSense 목록 표시에 **asp: GridView** 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-292">Notice that the IntelliSense list shows the **asp:GridView** control.</span></span>

    <span data-ttu-id="45245-293">HTML 편집기에서 IntelliSense는 이제 부분 일치 하는 (검색 용어를 포함 하는 모든 요소) 뿐만 아니라 제목 대/소문자 구분 검색을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-293">IntelliSense in the HTML Editor now provides title-casing search, as well as partial matching (retrieving all elements that contains the term).</span></span>

    <span data-ttu-id="45245-294">![IntelliSense 목록 사용 하 여 GridView를 삽입](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image30.png "IntelliSense 목록 사용 하 여 GridView를 삽입 합니다.")</span><span class="sxs-lookup"><span data-stu-id="45245-294">![Inserting a GridView with IntelliSense lists](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image30.png "Inserting a GridView with IntelliSense lists")</span></span>

    <span data-ttu-id="45245-295">*IntelliSense 목록 사용 하 여 GridView를 삽입합니다.*</span><span class="sxs-lookup"><span data-stu-id="45245-295">*Inserting a GridView with IntelliSense lists*</span></span>

    <span data-ttu-id="45245-296">입력 하는 경우  **&lt;그리드** 용어와 일치 하는 모든 항목 받아볼 수 있지만 Visual Studio에서는 제안 된 **gridview** 제어:</span><span class="sxs-lookup"><span data-stu-id="45245-296">If you type **&lt;grid** you will get all the items that match the term, but Visual Studio will suggest the **gridview** control:</span></span>

    <span data-ttu-id="45245-297">![IntelliSense 목록 및 부분 일치를 GridView 삽입](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image31.png "IntelliSense 목록 및 부분 일치를 GridView 삽입")</span><span class="sxs-lookup"><span data-stu-id="45245-297">![Inserting a GridView with IntelliSense lists and partial matching](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image31.png "Inserting a GridView with IntelliSense lists and partial matching")</span></span>

    <span data-ttu-id="45245-298">*IntelliSense 목록 및 부분 일치를 GridView 삽입*</span><span class="sxs-lookup"><span data-stu-id="45245-298">*Inserting a GridView with IntelliSense lists and partial matching*</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_-_HTML_Editor_Smart_Tags"></a>
#### <a name="task-4---html-editor-smart-tags"></a><span data-ttu-id="45245-299">작업 4-스마트 태그를 HTML 편집기</span><span class="sxs-lookup"><span data-stu-id="45245-299">Task 4 - HTML Editor Smart Tags</span></span>

<span data-ttu-id="45245-300">HTML 편집기에서 개선 된 또 다른는 스마트 태그 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-300">Another improvement in the HTML Editor is the Smart Tags feature.</span></span> <span data-ttu-id="45245-301">스마트 태그 쉽게 컨트롤 마다 별로 일반 또는 반복 개발 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-301">Smart tags make it easy to perform common or repetitive development tasks on a per-control basis.</span></span> <span data-ttu-id="45245-302">이 기능은 이미 제공한 HTML 디자이너에서 하지만 HTML 편집기에서 없습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-302">This feature was already available in the HTML Designer, but not in the HTML Editor.</span></span>

1. <span data-ttu-id="45245-303">열기 **Site.Master** 찾습니다는 **asp: 메뉴** 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-303">Open **Site.Master** and locate the **asp:Menu** element.</span></span> <span data-ttu-id="45245-304">시작 태그와 통지는 요소-맨 아래에 표시 된 작은 문자 모양을 클릭 하 여 스마트 작업 메뉴를 열고에 커서를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-304">Place the cursor on the start tag and notice that the small glyph displayed at the bottom of the element - click it to open the smart tasks menu.</span></span> <span data-ttu-id="45245-305">메뉴 컨트롤에 관련 된 일부 작업에 빠르게 액세스할 수 있는지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-305">Notice that you have quick access to some tasks related to the Menu control.</span></span>

    <span data-ttu-id="45245-306">![작업 메뉴 컨트롤에 대 한 스마트](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image32.png "스마트 메뉴 컨트롤에 대 한 작업")</span><span class="sxs-lookup"><span data-stu-id="45245-306">![Smart tasks for the Menu control](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image32.png "Smart tasks for the Menu control")</span></span>

    <span data-ttu-id="45245-307">*메뉴 컨트롤에 대 한 스마트 작업*</span><span class="sxs-lookup"><span data-stu-id="45245-307">*Smart tasks for the Menu control*</span></span>

<a id="Ex2Task5"></a>

<a id="Task_5_-_Smart_Indentation"></a>
#### <a name="task-5---smart-indentation"></a><span data-ttu-id="45245-308">작업 5-스마트 들여쓰기</span><span class="sxs-lookup"><span data-stu-id="45245-308">Task 5 - Smart Indentation</span></span>

<span data-ttu-id="45245-309">중첩 된 요소는 코드를 읽을 수 있는 들여쓰기는 HTML의 모범 사례 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-309">One of the best practices in HTML is indenting the nested elements to keep the code readable.</span></span> <span data-ttu-id="45245-310">Visual Studio 2012에서 편집기의 코드를 작성 하는 동안 자동으로 요소를 들여씁니다 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-310">In Visual Studio 2012, you will notice that the editor automatically indents the elements while you are writing the code.</span></span>

> [!NOTE]
> <span data-ttu-id="45245-311">Visual Studio의 이전 버전에서 스마트 들여쓰기 제공한 XML 편집기에서 있지만 HTML 편집기에는 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-311">In previous version of Visual Studio, smart indentation was available in the XML editor but not in the HTML editor.</span></span>


1. <span data-ttu-id="45245-312">HTML 편집기에서 들여쓰기 구성 스마트 들여쓰기로 설정 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-312">Make sure that the Indenting configuration on the HTML Editor is set to Smart Indentation.</span></span> <span data-ttu-id="45245-313">이 위해 선택 된 **도구 | 옵션** 메뉴 옵션을 선택 합니다는 **텍스트 편집기 | HTML | 탭** 화면의 왼쪽된 창에서 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-313">To do that, select the **Tools | Options** menu option and then select the **Text Editor | HTML | Tabs** page in the left pane of the screen.</span></span> <span data-ttu-id="45245-314">스마트 들여쓰기 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-314">Select the Smart indentation option.</span></span>

    <span data-ttu-id="45245-315">![HTML 편집기 설정](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image33.png "HTML 편집기 설정")</span><span class="sxs-lookup"><span data-stu-id="45245-315">![HTML Editor settings](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image33.png "HTML Editor settings")</span></span>

    <span data-ttu-id="45245-316">*HTML 편집기 설정*</span><span class="sxs-lookup"><span data-stu-id="45245-316">*HTML Editor settings*</span></span>
2. <span data-ttu-id="45245-317">에 **Default.aspx** 페이지에서 오디오 요소 아래에서 모든 내용을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-317">On the **Default.aspx** page, remove all the content under the audio element.</span></span>
3. <span data-ttu-id="45245-318">여는의 끝에 커서를 놓고 **오디오** 요소 및 적중 **ENTER**합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-318">Place the cursor at the end of the opening **audio** element and hit **ENTER**.</span></span>

    <span data-ttu-id="45245-319">커서의 새 위치 추가 들여쓰기 수준에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-319">Notice that the new position of cursor has an additional indentation level.</span></span>

    <span data-ttu-id="45245-320">![HTML 편집기에서 들여쓰기를 스마트](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image34.png "스마트 들여쓰기 HTML 편집기에서")</span><span class="sxs-lookup"><span data-stu-id="45245-320">![Smart indentation in the HTML Editor](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image34.png "Smart indentation in the HTML Editor")</span></span>

    <span data-ttu-id="45245-321">*HTML 편집기에서 스마트 들여쓰기*</span><span class="sxs-lookup"><span data-stu-id="45245-321">*Smart indentation in the HTML Editor*</span></span>
4. <span data-ttu-id="45245-322">를 제거한 한 또는 닫기 내용 사용 하 여 오디오 태그 복원 **Default.aspx** 변경 내용을 저장 하지 않고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-322">Restore the audio tag with the content you have removed, or close **Default.aspx** without saving the changes.</span></span>

<a id="Ex2Task6"></a>

<a id="Task_6_-_Extract_to_User_Control"></a>
#### <a name="task-6---extract-to-user-control"></a><span data-ttu-id="45245-323">태스크 6-사용자 정의 컨트롤로 추출</span><span class="sxs-lookup"><span data-stu-id="45245-323">Task 6 - Extract to User Control</span></span>

<span data-ttu-id="45245-324">함수에 코드의 일부를 추출 하는 등의 Visual Studio에 들어 Refactoring 도구는 향상 및 리팩터링 기존 코드를 쉽게 수행할 수 있는 뛰어난 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-324">The Refactoring tools included in Visual Studio, such as extracting a portion of code to a function, are great features that facilitate the improvement and the refactoring the existing code.</span></span> <span data-ttu-id="45245-325">ASP.NET 페이지에 대 한 테이블에 해당 하는 HTML 코드를 사용자 정의 컨트롤로 추출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45245-325">The counterpart for ASP.NET pages would be the extraction of HTML code to a User Control.</span></span> <span data-ttu-id="45245-326">수동으로 수행 하는 새 사용자 정의 컨트롤 만들기, 이동 코드 섹션은 사용자 정의 컨트롤, 사용자 정의 컨트롤에 대 한 태그 접두사를 등록 하 고, 마지막으로, 여러 페이지에 사용자 컨트롤을 인스턴스화한 같은 몇 가지 단계를 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45245-326">Doing it manually would involve several steps, like creating a new User Control, moving the code section to the User Control, registering a tag prefix for the User Control, and, finally, instantiating the User Control on the pages.</span></span> <span data-ttu-id="45245-327">이제 새 *사용자 정의 컨트롤로 추출* 도구는 자동으로 이러한 모든 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-327">Now, the new *Extract to User Control* tool automatically performs all those steps for you.</span></span>

<span data-ttu-id="45245-328">이 태스크에서는 선택한 코드에서 새 사용자 정의 컨트롤을 생성 하려면 새 사용자 정의 컨트롤 상황에 맞는 작업 추출을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-328">In this task, you will use the new Extract to User Control contextual operation to generate a new user control from the selected code.</span></span>

1. <span data-ttu-id="45245-329">에 **Default.aspx** 선택 페이지는 **H2** 및 **오디오** 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-329">On the **Default.aspx** page, select the **H2** and **audio** elements.</span></span>
2. <span data-ttu-id="45245-330">마우스 오른쪽 단추로 클릭 하 고 선택 **사용자 정의 컨트롤로 추출**합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-330">Right click and select **Extract to User Control**.</span></span>

    <span data-ttu-id="45245-331">![사용자 정의 컨트롤 메뉴 옵션에 추출](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image35.png "사용자 정의 컨트롤 메뉴 옵션에 추출 합니다.")</span><span class="sxs-lookup"><span data-stu-id="45245-331">![Extract to User Control menu option](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image35.png "Extract to User Control menu option")</span></span>

    <span data-ttu-id="45245-332">*사용자 정의 컨트롤 메뉴 옵션을 추출 합니다.*</span><span class="sxs-lookup"><span data-stu-id="45245-332">*Extract to User Control menu option*</span></span>
3. <span data-ttu-id="45245-333">새 사용자 정의 컨트롤에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-333">Type a name for the new user control.</span></span> <span data-ttu-id="45245-334">예를 들어, **Jukebox.ascx**, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-334">For instance, **Jukebox.ascx**, and then click **OK**.</span></span>

    <span data-ttu-id="45245-335">![추출 된 사용자 정의 컨트롤을 저장](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image36.png "추출 된 사용자 정의 컨트롤을 저장 합니다.")</span><span class="sxs-lookup"><span data-stu-id="45245-335">![Saving the extracted user control](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image36.png "Saving the extracted user control")</span></span>

    <span data-ttu-id="45245-336">*추출 된 사용자 정의 컨트롤을 저장합니다.*</span><span class="sxs-lookup"><span data-stu-id="45245-336">*Saving the extracted user control*</span></span>
4. <span data-ttu-id="45245-337">선택한 코드를 사용자 정의 컨트롤로 추출 된 새 사용자 정의 컨트롤의 인스턴스로 바뀌었으면 선택한 코드의 원래 위치에 유의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="45245-337">Notice that the selected code was extracted to a user control and the original location of the selected code was replaced with an instance of the new user control.</span></span>

    <span data-ttu-id="45245-338">![페이지는 자동으로 새 사용자 정의 컨트롤을 사용 하도록 업데이트](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image37.png "페이지는 자동으로 새 사용자 정의 컨트롤을 사용 하도록 업데이트")</span><span class="sxs-lookup"><span data-stu-id="45245-338">![Page automatically updated to use the new user control](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image37.png "Page automatically updated to use the new user control")</span></span>

    <span data-ttu-id="45245-339">*페이지는 자동으로 새 사용자 정의 컨트롤을 사용 하도록 업데이트*</span><span class="sxs-lookup"><span data-stu-id="45245-339">*Page automatically updated to use the new user control*</span></span>
5. <span data-ttu-id="45245-340">키를 눌러 **F5** 하는 페이지를 실행 하 고 컨트롤 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-340">Press **F5** to run the page and verify that the control works.</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Whats_New_in_the_JavaScript_Editor"></a>
### <a name="exercise-3-whats-new-in-the-javascript-editor"></a><span data-ttu-id="45245-341">JavaScript 편집기는의 새로운 소식 연습 3:</span><span class="sxs-lookup"><span data-stu-id="45245-341">Exercise 3: What's New in the JavaScript Editor</span></span>

<span data-ttu-id="45245-342">작성 또는 편집용 JavaScript 코드는 쉬운 일, 특히 응용 프로그램 시작의 크기가 증가 하 라면 긴 파일을 처리 하 고 중요 한 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-342">Writing or editing JavaScript code is not an easy task, especially when your application starts to grow in size and you find yourself dealing with long files and hundreds of functions.</span></span> <span data-ttu-id="45245-343">스크립트 개발자는 일반적으로 몇 가지 추가 작업 코드 가독성을 유지 관리 하 고 파일 탐색을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-343">Script developers usually have to do some extra work to maintain code legibility and navigate across files.</span></span> <span data-ttu-id="45245-344">JQuery JavaScript 라이브러리 포함 된 스크립트 탐색 코드 길이 때문에 자체 challenge 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-344">With the inclusion of JavaScript libraries like jQuery, script navigation has become a challenge itself because of the code length.</span></span>

<span data-ttu-id="45245-345">Visual Studio JavaScript 편집기를 꼭 코드 액세스 가능 하 고 구성 된 프라미스를 갱신 했습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-345">Visual Studio has renewed the JavaScript editor with the promise to make the code mode accessible and organized.</span></span> <span data-ttu-id="45245-346">JavaScript 편집기에서 C# 또는 VB 편집기에 이미 존재 하는 많은 Visual Studio 기능이 구현 되어: 정의로 이동, 자동 들여쓰기, 설명서 및 작성 하는 경우 유효성 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-346">Many Visual Studio features that already existed in C# or VB editors are now implemented in the JavaScript editor: Go To Definition, automatic indentation, documentation and validation when you are writing.</span></span> <span data-ttu-id="45245-347">갱신 된 IntelliSense 목록으로 손쉽게 JavaScript 함수 카탈로그를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-347">With the renewed IntelliSense list you will have the JavaScript function catalog at your fingertips.</span></span>

<span data-ttu-id="45245-348">이 연습에서는 새로운 기능 중 일부 및 JavaScript 편집기의 향상 된 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="45245-348">In this exercise, you will learn some of the new features and improvements of JavaScript editor.</span></span> <span data-ttu-id="45245-349">샘플 파일 찾아보기 및 JavaScript 프로그래밍 내 Visual Studio 2012에서 더 효율적으로 인해 변경 되는 새로운 특성을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-349">You will browse sample files and discover each of the new characteristics that will make your JavaScript programming more efficient within Visual Studio 2012.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_JavaScript_Editor_New_Features"></a>
#### <a name="task-1---javascript-editor-new-features"></a><span data-ttu-id="45245-350">작업 1-JavaScript 편집기의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="45245-350">Task 1 - JavaScript Editor New Features</span></span>

<span data-ttu-id="45245-351">이 작업에서는 코드를 구성 하 고 더 나은 사용자 환경을 상태로 전환에 집중 된 새로운 JavaScript 편집기 기능 중 일부를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-351">This task will introduce you to some of the new JavaScript editor features, which focus on organizing your code and bringing a better user experience.</span></span>

1. <span data-ttu-id="45245-352">열려 있지 않으면 시작 **Visual Studio** 엽니다는 **WhatsNewASPNET.sln** 솔루션에 있는 **Source\WhatsNewASPNET** 이 랩의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-352">If not already opened, start **Visual Studio** and open the **WhatsNewASPNET.sln** solution located in the **Source\WhatsNewASPNET** folder of this lab.</span></span>
2. <span data-ttu-id="45245-353">키를 눌러 **F5** 응용 프로그램을 실행 하려면 탐색 모음에서 JavaScript 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-353">Press **F5** to run the application, then click the JavaScript link in the navigation bar.</span></span> <span data-ttu-id="45245-354">페이지를 여러 번 및 확인 방법을 새로 카운터가 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-354">Refresh the page several times and check how the counter increments.</span></span>

    <span data-ttu-id="45245-355">![페이지 카운터](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image38.png "페이지 카운터")</span><span class="sxs-lookup"><span data-stu-id="45245-355">![Page counter](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image38.png "Page counter")</span></span>

    <span data-ttu-id="45245-356">*페이지 카운터*</span><span class="sxs-lookup"><span data-stu-id="45245-356">*Page counter*</span></span>
3. <span data-ttu-id="45245-357">브라우저를 닫고 Visual Studio로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="45245-357">Close the browser and go back to Visual Studio.</span></span>
4. <span data-ttu-id="45245-358">열기는 **JavaScript.aspx** 페이지를 찾습니다는 **&lt;스크립트&gt;** 블록 (아래 참조).</span><span class="sxs-lookup"><span data-stu-id="45245-358">Open the **JavaScript.aspx** page and locate the **&lt;script&gt;** block (shown below).</span></span>

    <span data-ttu-id="45245-359">다음 코드 HTML5 로컬 저장소를 사용 하 여 저장 하는 *pageLoadCount* 현재 사용자가 페이지를 방문한 횟수를 저장 하는 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-359">The following code uses HTML5 local storage to store a *pageLoadCount* variable that stores the number of times the page has been visited by the current user.</span></span> <span data-ttu-id="45245-360">로컬 저장소는 HTML5 표준 도입 하는 클라이언트 쪽 키-값 데이터베이스.</span><span class="sxs-lookup"><span data-stu-id="45245-360">Local Storage is a client-side key-value database introduced with the HTML5 standard.</span></span> <span data-ttu-id="45245-361">데이터는 로컬 컴퓨터 사용자의 브라우저 내에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45245-361">The data is saved on the local machine, inside the user's browser.</span></span>

    [!code-html[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample7.html)]

    > [!NOTE]
    > <span data-ttu-id="45245-362">DOCTYPE 다음 단계를 진행 하기 전에 XHTML5로 설정 되어를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-362">Ensure the DOCTYPE is set to XHTML5 before proceeding with the next steps.</span></span>
5. <span data-ttu-id="45245-363">코드를 편집 하 고 JavaScript 용 IntelliSense의 내부 메서드 및 로컬 저장소와 같은 HTML5 기능을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-363">Edit the code and notice that IntelliSense for JavaScript includes HTML5 features, like local storage, and their inner methods.</span></span>

    <span data-ttu-id="45245-364">![JavaScript의 HTML5 JavaScript 기능](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image39.png "javascript에서 HTML5 JavaScript 기능")</span><span class="sxs-lookup"><span data-stu-id="45245-364">![HTML5 JavaScript features in JavaScript](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image39.png "HTML5 JavaScript features in JavaScript")</span></span>

    <span data-ttu-id="45245-365">*JavaScript의 HTML5 JavaScript 기능*</span><span class="sxs-lookup"><span data-stu-id="45245-365">*HTML5 JavaScript features in JavaScript*</span></span>
6. <span data-ttu-id="45245-366">모든 여는 대괄호 클릭 (**{**) 스크립트에서 코드 및 대괄호 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45245-366">Click any opening bracket (**{**) from the scripting code and notice that the brackets are highlighted.</span></span>

    <span data-ttu-id="45245-367">![대괄호는 강조 표시](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image40.png "대괄호 강조 표시 됩니다")</span><span class="sxs-lookup"><span data-stu-id="45245-367">![Brackets are highlighted](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image40.png "Brackets are highlighted")</span></span>

    <span data-ttu-id="45245-368">*대괄호는 강조 표시*</span><span class="sxs-lookup"><span data-stu-id="45245-368">*Brackets are highlighted*</span></span>
7. <span data-ttu-id="45245-369">함수를 주석 처리 제거 **testAutoAlign()** (세 줄을 선택 하 고 사용할 수 있습니다 **CTRL** + **K**; **CTRL** + **U**) 함수 코드 안에 커서를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-369">Uncomment the function **testAutoAlign()** (select the three lines and you can use **CTRL** + **K**; **CTRL** + **U**) and locate the cursor inside the function code.</span></span> <span data-ttu-id="45245-370">두 번째 줄을 추가 하려면 enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="45245-370">Press enter to append a second line.</span></span> <span data-ttu-id="45245-371">이제 코드는 사라졌는지 **정렬** 및 **자동 들여쓰기**합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-371">Notice that the code is now **aligned** and **auto-indented**.</span></span>

    <span data-ttu-id="45245-372">![JavaScript 코드는 자동 정렬](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image41.png "JavaScript 코드는 자동 정렬")</span><span class="sxs-lookup"><span data-stu-id="45245-372">![JavaScript code is auto aligned](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image41.png "JavaScript code is auto aligned")</span></span>

    <span data-ttu-id="45245-373">*JavaScript 코드는 자동 정렬*</span><span class="sxs-lookup"><span data-stu-id="45245-373">*JavaScript code is auto aligned*</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Validating_JavaScript"></a>
#### <a name="task-2---validating-javascript"></a><span data-ttu-id="45245-374">작업 2-JavaScript 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="45245-374">Task 2 - Validating JavaScript</span></span>

<span data-ttu-id="45245-375">이 작업에 ECMAScript5 표준에 대 한 새 JavaScript 유효성 검사에서 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-375">In this task, you will discover the new JavaScript validation for the ECMAScript5 standard.</span></span> <span data-ttu-id="45245-376">이 기능은 사이트를 배포 하기 전에 스크립팅 문제를 방지 하는 동안 규격 JavaScript 코드를 작성 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45245-376">This feature will help you to write compliant JavaScript code, while preventing scripting issues before site deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="45245-377">Visual Studio 2012 ECMAScript5 호환성을 제공 하지만 visual Studio 2010 ECMAStript3 규정 준수를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-377">Visual Studio 2010 implemented ECMAStript3 compliance, while Visual Studio 2012 provides ECMAScript5 compliance.</span></span>


1. <span data-ttu-id="45245-378">열기 **ECMA5script5.js** 아래에 **Scripts\custom** 프로젝트 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-378">Open **ECMA5script5.js** located under the **Scripts\custom** project folder.</span></span> <span data-ttu-id="45245-379">이제 ECMAScript5 표준에 대 한 유효성을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-379">You will now test validation for ECMAScript5 standard.</span></span>

    [!code-html[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample8.html)]

    <span data-ttu-id="45245-380">체크 아웃할 수는 &quot; **strict 사용** &quot; ECMAScript5 수 있도록 하는 파일의 첫 번째 줄에서 방향을 **strict 모드**합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-380">You can check out the &quot; **use strict** &quot; direction in the first line of the file, which enables ECMAScript5 **strict mode**.</span></span> <span data-ttu-id="45245-381">이 모드는 이전 버전에서 모호성을 명확 하 고 개체 속성에 getter 및 setter, JSON 및 자세한 리플렉션에 대 한 라이브러리 지원 같은 새로운 몇 가지 기능을 추가 하는 언어의 하위 집합에 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45245-381">This mode consists in a subset of the language that clarifies ambiguities from the past edition, and adds some new features, such as getters and setters, library support for JSON, and more complete reflection on object properties.</span></span>
2. <span data-ttu-id="45245-382">열기는 **오류 목록** 열려 있지 않으면 (**보기** 메뉴 | **오류 목록**).</span><span class="sxs-lookup"><span data-stu-id="45245-382">Open the **Error List** if not already opened (**View** menu | **Error List**).</span></span> <span data-ttu-id="45245-383">공지는 **함수** 선언에 밑줄이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45245-383">Notice the **function** declaration is underlined.</span></span> <span data-ttu-id="45245-384">즉, ECMA5 표준 함수 언어 구조 안에 중첩 될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-384">This is because in ECMA5 standard functions cannot be nested inside language structures.</span></span> <span data-ttu-id="45245-385">오류에 아래 목록에는 경고 세부 정보 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45245-385">In the error list below you will see the warning details.</span></span>

    <span data-ttu-id="45245-386">![JavaScript 유효성 검사 오류 메시지](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image42.png "JavaScript 유효성 검사 오류 메시지")</span><span class="sxs-lookup"><span data-stu-id="45245-386">![JavaScript validation error message](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image42.png "JavaScript validation error message")</span></span>

    <span data-ttu-id="45245-387">*JavaScript 유효성 검사 오류 메시지*</span><span class="sxs-lookup"><span data-stu-id="45245-387">*JavaScript validation error message*</span></span>
3. <span data-ttu-id="45245-388">주석으로 처리는 **&quot;strict 사용&quot;** 방향과 경고 상태로 유지 되지만 오류가 사라집니다.</span><span class="sxs-lookup"><span data-stu-id="45245-388">Comment out the **&quot;use strict&quot;** direction and notice that errors disappear, but the warnings remain.</span></span>
4. <span data-ttu-id="45245-389">파일의 마지막 줄에서 다음과 같은 모든 문자열을 작성 **&quot;테스트&quot;** (은 문자열로 나타내기 위해 따옴표를 포함).</span><span class="sxs-lookup"><span data-stu-id="45245-389">In the last line of the file, write any string like **&quot;test&quot;** (include the quotation marks to indicate it is as string).</span></span> <span data-ttu-id="45245-390">IntelliSense 목록에 표시 하 고 선택 문자열 옆에 있는 마침표 쓰기는 **trim** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-390">Write a period next to the string to display the IntelliSense list, and select the **trim** option.</span></span>

    <span data-ttu-id="45245-391">ECMAScript5 표준에서 문자열 값 및 변수도 정의 trim, 대문자, 찾기 및 바꾸기와 같은 문자열 처리 메서드는 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-391">In ECMAScript5 standard, string values and variables also have string methods defined, like trim, uppercase, search and replace.</span></span>

    <span data-ttu-id="45245-392">![JavaScript IntelliSense 목록](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image43.png "JavaScript IntelliSense 목록")</span><span class="sxs-lookup"><span data-stu-id="45245-392">![IntelliSense list in JavaScript](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image43.png "IntelliSense list in JavaScript")</span></span>

    <span data-ttu-id="45245-393">*JavaScript IntelliSense 목록*</span><span class="sxs-lookup"><span data-stu-id="45245-393">*IntelliSense list in JavaScript*</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_XML_Documentation_for_JavaScript"></a>
#### <a name="task-3---xml-documentation-for-javascript"></a><span data-ttu-id="45245-394">작업 3-JavaScript에 대 한 XML 설명서</span><span class="sxs-lookup"><span data-stu-id="45245-394">Task 3 - XML Documentation for JavaScript</span></span>

<span data-ttu-id="45245-395">이 태스크에서는 JavaScript에서 XML 문서에 대 한 Visual Studio 기능을 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-395">In this task, you will explore Visual Studio features for XML documentation in JavaScript.</span></span> <span data-ttu-id="45245-396">JavaScript IntelliSense 목록이 표시 됩니다. 각 함수의 XML 문서를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-396">You will see the JavaScript IntelliSense list now shows the XML documentation of each function.</span></span> <span data-ttu-id="45245-397">또한에서 javascript에서 탐색 기능을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-397">Additionally, you will discover the navigation feature in JavaScript.</span></span>

1. <span data-ttu-id="45245-398">열기 **XMLDoc.js** 에 있는 파일 **스크립트/사용자 지정** 프로젝트 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-398">Open **XMLDoc.js** file located in **Scripts/custom** project folder.</span></span> <span data-ttu-id="45245-399">이 파일에 JavaScript 함수는 각각 XML 문서를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-399">This file contains XML documentation on each of the JavaScript functions.</span></span>

    <span data-ttu-id="45245-400">![JavaScript XML 설명서를 IntelliSense에서 통합](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image44.png "JavaScript XML 설명서를 IntelliSense에서 통합")</span><span class="sxs-lookup"><span data-stu-id="45245-400">![JavaScript XML documentation integrated to IntelliSense](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image44.png "JavaScript XML documentation integrated to IntelliSense")</span></span>

    <span data-ttu-id="45245-401">*JavaScript XML 설명서를 IntelliSense에서 통합*</span><span class="sxs-lookup"><span data-stu-id="45245-401">*JavaScript XML documentation integrated to IntelliSense*</span></span>
2. <span data-ttu-id="45245-402">아래 **추가** 함수 **XMLDoc.js** 파일, 명명 된 새 함수를 만들고 **테스트**합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-402">Below **add** function in **XMLDoc.js** file, create a new function named **test**.</span></span>
3. <span data-ttu-id="45245-403">에 **테스트** 함수를 호출 하는 **곱하기** 두 개의 매개 변수를 수신 하는 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-403">In the **test** function, call the **multiply** function that receives two parameters.</span></span> <span data-ttu-id="45245-404">도구 설명 상자를 보여 주는 것을 알는 **곱하기** 설명서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-404">Notice the tooltip box is showing the **multiply** function documentation.</span></span>

    [!code-javascript[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample9.js)]

    <span data-ttu-id="45245-405">![JavaScript 함수에 대 한 XML 설명서](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image45.png "JavaScript 함수에 대 한 XML 설명서")</span><span class="sxs-lookup"><span data-stu-id="45245-405">![XML documentation for JavaScript functions](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image45.png "XML documentation for JavaScript functions")</span></span>

    <span data-ttu-id="45245-406">*JavaScript 함수에 대 한 XML 문서*</span><span class="sxs-lookup"><span data-stu-id="45245-406">*XML documentation for JavaScript functions*</span></span>
4. <span data-ttu-id="45245-407">함수 호출 문과 형식 완료는 *점* 반환된 값에서 IntelliSense 목록을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="45245-407">Complete the function call statement and type a *dot* to open the IntelliSense list on the returned value.</span></span> <span data-ttu-id="45245-408">Visual Studio 검색 하는 중에 **반환** 는 숫자 값을 처리 하는 문서에는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-408">Notice that Visual Studio is detecting the **return** value in the documentation, treating the value as a number.</span></span>

    <span data-ttu-id="45245-409">![반환 형식에 대 한 XML 설명서](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image46.png "반환 형식에 대 한 XML 설명서")</span><span class="sxs-lookup"><span data-stu-id="45245-409">![XML documentation for return types](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image46.png "XML documentation for return types")</span></span>

    <span data-ttu-id="45245-410">*반환 형식에 대 한 XML 설명서*</span><span class="sxs-lookup"><span data-stu-id="45245-410">*XML documentation for return types*</span></span>
5. <span data-ttu-id="45245-411">이제, 추가 기능에 대 한 호출을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-411">Now, insert a call to add function.</span></span> <span data-ttu-id="45245-412">JavaScript 편집기에서 이제 함수 오버 로드를 지원 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-412">Notice that the JavaScript editor now supports function overloads.</span></span> <span data-ttu-id="45245-413">함수 이름을 작성 하는 경우 설명서에 지정 된 사용 가능한 오버 로드 중 하나를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-413">When you write a function name, you will be able to select any of the available overloads specified in the documentation.</span></span>

    <span data-ttu-id="45245-414">![오버 로드에 대 한 XML 설명서](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image47.png "오버 로드에 대 한 XML 설명서")</span><span class="sxs-lookup"><span data-stu-id="45245-414">![XML documentation for overloads](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image47.png "XML documentation for overloads")</span></span>

    <span data-ttu-id="45245-415">*오버 로드에 대 한 XML 설명서*</span><span class="sxs-lookup"><span data-stu-id="45245-415">*XML documentation for overloads*</span></span>
6. <span data-ttu-id="45245-416">열기 **GotoDefinition.js** 파일를 찾습니다는 **$().html()** 함수 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-416">Open **GotoDefinition.js** file and locate the **$().html()** function call.</span></span> <span data-ttu-id="45245-417">커서를 찾습니다 **html**합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-417">Locate the cursor on **html**.</span></span>
7. <span data-ttu-id="45245-418">키를 눌러 **F12** 정의로 이동 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-418">Press **F12** and navigate to the definition.</span></span> <span data-ttu-id="45245-419">이제 액세스할 수 있으며 JavaScript 코드를 사용 하지 않고 찾아보기 공지는 **찾을** 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-419">Notice you can now access and browse your JavaScript code without using the **Find** tool.</span></span>
8. <span data-ttu-id="45245-420">코드 파일의 맨 아래에 있는 시그니처 블록 전에 jQuery 명령에 커서를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-420">Locate the cursor on the jQuery instruction prior to the signature block at the bottom of the code file.</span></span> <span data-ttu-id="45245-421">키를 눌러 **F12**합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-421">Press **F12**.</span></span> <span data-ttu-id="45245-422">JQuery 라이브러리 파일을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-422">You will navigate to the jQuery library file.</span></span> <span data-ttu-id="45245-423">사용 하 여 jQuery 파일 탐색할 수 있습니다 알 **F12**합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-423">Notice you can also navigate across the jQuery files using **F12**.</span></span>

    <span data-ttu-id="45245-424">![JQuery 정의로 이동](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image48.png "jQuery 정의로 이동")</span><span class="sxs-lookup"><span data-stu-id="45245-424">![Navigating to jQuery definitions](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image48.png "Navigating to jQuery definitions")</span></span>

    <span data-ttu-id="45245-425">*JQuery 정의로 이동*</span><span class="sxs-lookup"><span data-stu-id="45245-425">*Navigating to jQuery definitions*</span></span>

> [!NOTE]
> <span data-ttu-id="45245-426">GotoDefinition.js에 파일을 저장 하기 전에 구문 오류가 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-426">Make sure that GotoDefinition.js has no syntax errors before saving the file.</span></span>


<a id="Exercise4"></a>

<a id="Exercise_4_Bundling_and_Minification"></a>
### <a name="exercise-4-bundling-and-minification"></a><span data-ttu-id="45245-427">연습 4: 묶음 및 축소</span><span class="sxs-lookup"><span data-stu-id="45245-427">Exercise 4: Bundling and Minification</span></span>

<span data-ttu-id="45245-428">몇 번 수행 웹 사이트에 둘 이상의 JavaScript 또는 CSS 파일 포함?</span><span class="sxs-lookup"><span data-stu-id="45245-428">How many times do your websites include more than one JavaScript or CSS file?</span></span> <span data-ttu-id="45245-429">여기서 묶음 및 축소 시킬 수 있지만 파일 크기를 줄이고 성능을 향상 하는 사이트는 매우 일반적인 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-429">This is a very common scenario where bundling and minification can help to reduce the file size and make the site perform faster.</span></span> <span data-ttu-id="45245-430">ASP.NET 4.5의 새로운 묶는 것 기능 JS 또는 CSS 파일 집합을 단일 요소인 "압축"을 (즉, 필요 하지 않음 공백 제거, 메모 제거, 식별자 감소) 콘텐츠를 축소 하 여 해당 크기를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-430">The new bundling feature in ASP.NET 4.5 packs a set of JS or CSS files into a single element, and reduces its size by minifying the content ( i.e. removing not required blank spaces, removing comments, reducing identifiers ).</span></span>

<span data-ttu-id="45245-431">프로세스에서 사용자 에이전트 (예: IE, Mozilla, 등)를 식별 하 고 따라서 사용자 브라우저 (예를 들어, 제거 stuff Mozilla 특정를 대상으로 하 여 압축을 향상 시킬 수 있도록 묶음 및 축소 ASP.NET 4.5에서 런타임 시 수행 됩니다. 요청 되 면 IE에서).</span><span class="sxs-lookup"><span data-stu-id="45245-431">Bundling and minification in ASP.NET 4.5 is performed at runtime, so that the process can identify the user agent (for example IE, Mozilla, etc), and thus, improve the compression by targeting the user browser (for instance, removing stuff that is Mozilla specific when the request comes from IE).</span></span>

<span data-ttu-id="45245-432">이 연습에서는 ASP.NET 4.5에 다양 한 유형의 묶음 및 축소를 사용 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-432">In this exercise, you will learn how to enable and use the different types of bundling and minification in ASP.NET 4.5.</span></span>

<a id="Ex4Task1"></a>

<a id="Task_1_-_Installing_the_Bundling_and_Minification_Package_from_NuGet"></a>
#### <a name="task-1---installing-the-bundling-and-minification-package-from-nuget"></a><span data-ttu-id="45245-433">작업 1-번들로 설치 및 NuGet에서 축소 패키지</span><span class="sxs-lookup"><span data-stu-id="45245-433">Task 1 - Installing the Bundling and Minification Package from NuGet</span></span>

1. <span data-ttu-id="45245-434">열려 있지 않으면 시작 **Visual Studio** 엽니다는 **WhatsNewASPNET.sln** 솔루션에 있는 **Source\WhatsNewASPNET** 이 랩의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-434">If not already opened, start **Visual Studio** and open the **WhatsNewASPNET.sln** solution located in the **Source\WhatsNewASPNET** folder of this lab.</span></span>
2. <span data-ttu-id="45245-435">NuGet 패키지 관리자 콘솔을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="45245-435">Open the NuGet Package Manager Console.</span></span> <span data-ttu-id="45245-436">이 작업을 수행 하려면 메뉴 사용 **보기** | **다른 창** | **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-436">To do this, use the menu **View** | **Other Windows** | **Package Manager Console**.</span></span>

    <span data-ttu-id="45245-437">![패키지 관리자 file:///C:/Users/User/AppData/Local/Temp/Marker3744//media/44462/Multiple-Stylesheets-and-JavaScript-files-in-the-application.pngconsole 열기](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image49.png "패키지 관리자 콘솔을 열고")</span><span class="sxs-lookup"><span data-stu-id="45245-437">![Opening the package manager file:///C:/Users/User/AppData/Local/Temp/Marker3744//media/44462/Multiple-Stylesheets-and-JavaScript-files-in-the-application.pngconsole](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image49.png "Opening the package manager console")</span></span>

    <span data-ttu-id="45245-438">*패키지 관리자 콘솔 열기*</span><span class="sxs-lookup"><span data-stu-id="45245-438">*Opening the package manager console*</span></span>
3. <span data-ttu-id="45245-439">에 **패키지 관리자 콘솔** 형식 **Install-package Microsoft.Web.Optimization** 누릅니다 **ENTER**합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-439">In the **Package Manager Console,** type **Install-Package Microsoft.Web.Optimization** and press **ENTER**.</span></span>

<a id="Ex4Task2"></a>

<a id="Task_2_-_Default_Bundles"></a>
#### <a name="task-2---default-bundles"></a><span data-ttu-id="45245-440">작업 2-기본 번들</span><span class="sxs-lookup"><span data-stu-id="45245-440">Task 2 - Default Bundles</span></span>

<span data-ttu-id="45245-441">기본 번들을 사용 하도록 설정 하려면 묶음 및 축소를 사용 하는 가장 간단한 방법은 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45245-441">The simplest way to use bundling and minification is to enable the default bundles.</span></span> <span data-ttu-id="45245-442">이 메서드는 폴더의 JS 및 CSS 파일에 대 한 번들 및 축소 된 버전을 참조할 수 있도록 규칙을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-442">This method uses conventions to let you reference the bundled and minified version for the JS and CSS files in a folder.</span></span>

<span data-ttu-id="45245-443">이 태스크에서는 활성화 및 함께 제공 되 고 축소 된 CSS 및 JS 파일을 참조 하 고 결과 출력을 확인 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-443">In this task, you will learn how to enable and reference the bundled and minified JS and CSS files and view the resulting output.</span></span>

1. <span data-ttu-id="45245-444">열려 있지 않으면 시작 **Visual Studio** 엽니다는 **WhatsNewASPNET.sln** 솔루션에 있는 **Source\WhatsNewASPNET** 이 랩의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-444">If not already opened, start **Visual Studio** and open the **WhatsNewASPNET.sln** solution located in the **Source\WhatsNewASPNET** folder of this lab.</span></span>
2. <span data-ttu-id="45245-445">에 **솔루션 탐색기**를 확장 하 고는 **스타일**, **Scripts\custom** 및 **Scripts\bundle** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-445">In the **Solution Explorer**, expand the **Styles**, **Scripts\custom** and **Scripts\bundle** folders.</span></span>

    <span data-ttu-id="45245-446">응용 프로그램 둘 이상의 CSS 및 JS 파일을 사용 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-446">Notice that the application is using more than one CSS and JS file.</span></span>

    <span data-ttu-id="45245-447">![응용 프로그램에서 여러 스타일 시트 및 JavaScript 파일로](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image50.png "응용 프로그램에서 여러 스타일 시트 및 JavaScript 파일")</span><span class="sxs-lookup"><span data-stu-id="45245-447">![Multiple Stylesheets and JavaScript files in the application](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image50.png "Multiple Stylesheets and JavaScript files in the application")</span></span>

    <span data-ttu-id="45245-448">*응용 프로그램에서 여러 스타일 시트 및 JavaScript 파일*</span><span class="sxs-lookup"><span data-stu-id="45245-448">*Multiple Stylesheets and JavaScript files in the application*</span></span>
3. <span data-ttu-id="45245-449">열기는 **Global.asax.cs** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-449">Open the **Global.asax.cs** file.</span></span>

    <span data-ttu-id="45245-450">새 **Microsoft.Web.Optimization** 네임 스페이스는 파일의 시작 부분에서 주석으로 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-450">Notice that the new **Microsoft.Web.Optimization** namespace is commented out at the beginning of the file.</span></span> <span data-ttu-id="45245-451">사용 하는 주석 처리 제거 지시문 묶음 및 축소 기능을 포함 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-451">Uncomment the using directive to include the bundling and minification features.</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample10.cs)]
~~~
4. <span data-ttu-id="45245-452">찾을 **응용 프로그램\_시작** 메서드.</span><span class="sxs-lookup"><span data-stu-id="45245-452">Locate the **Application\_Start** method.</span></span>

    <span data-ttu-id="45245-453">이 방법에서는 아래 코드 조각에 나와 있는 것 처럼 EnableDefaultBundles 호출 주석 처리 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-453">In this method, uncomment the EnableDefaultBundles call as shown in the snippet below.</span></span> <span data-ttu-id="45245-454">이렇게 하면 폴더의 CSS 파일의 번들로 묶은 컬렉션에는 해당 폴더의 경로 사용 하 여 참조를 수와 &quot;CSS&quot; 또는 &quot;JS&quot; 접미사입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-454">This enables us to reference a bundled collection of CSS files in a folder by using the path to that folder, plus the &quot;CSS&quot; or the &quot;JS&quot; suffix.</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample11.cs)]
~~~
5. <span data-ttu-id="45245-455">열기는 **Optimization.aspx** 파일을 콘텐츠 컨트롤을 찾으십시오 **HeadContent**합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-455">Open the **Optimization.aspx** file and locate the content control for **HeadContent**.</span></span>

    <span data-ttu-id="45245-456">CSS 파일 참조는 단일 태그가 있어야 JS 파일을 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="45245-456">Notice the CSS files and the JS files have a single referenced tag.</span></span>


~~~
[!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample12.aspx)]

> [!NOTE]
> This code is for demo purposes. Ideally, you will reference the bundles in the Site.Master file. In this sample code, you will find that some of the bundled files are also being referenced by the Site.Master file, making this last reference redundant.
~~~
6. <span data-ttu-id="45245-457">링크의 번들 규칙에 사용 하는 것을 알는 **href** 스타일 및 Scripts\custom에서 모든 CSS 또는 JS 파일을 가져올 특성 폴더 각각.</span><span class="sxs-lookup"><span data-stu-id="45245-457">Notice that the links are using the bundling conventions in the **href** attribute to get all the CSS or JS files from the Styles and Scripts\custom folder respectively.</span></span>

    <span data-ttu-id="45245-458">경로 사용할 수 있습니다 **스크립트/사용자 지정/JS** 아래와 같이 축소할 내부에 있는 모든 JS 파일을 번들로 **스크립트/사용자 지정** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-458">You can use the path **Scripts/custom/JS** as shown below to bundle and minify all the JS files inside a **Scripts/custom** folder.</span></span> <span data-ttu-id="45245-459">이것이 기본 번들 기본 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-459">This is the default behavior with the default bundles.</span></span>


~~~
[!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample13.aspx)]
~~~
7. <span data-ttu-id="45245-460">열기는 **Styles\Site.css** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-460">Open the **Styles\Site.css** file.</span></span>

    <span data-ttu-id="45245-461">원래 CSS 파일 들여쓰기 된 코드, 공백 및 파일을 확대 하는 주석을 포함 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-461">Notice that the original CSS file contains indented code, blank spaces and comments that enlarge the file.</span></span> <span data-ttu-id="45245-462">(또한 JavaScript 파일에 빈 공간 및 주석).</span><span class="sxs-lookup"><span data-stu-id="45245-462">(Also the JavaScript file contains blank spaces and comments).</span></span>

    <span data-ttu-id="45245-463">![Scripts 폴더에서 파일의 원래 CSS 중 하나가](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image51.png "Scripts 폴더에서 파일의 원래 CSS 중 하나")</span><span class="sxs-lookup"><span data-stu-id="45245-463">![One of the original CSS files in the Scripts folder](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image51.png "One of the original CSS files in the Scripts folder")</span></span>

    <span data-ttu-id="45245-464">*스크립트 폴더에 원래 CSS 파일 중 하나*</span><span class="sxs-lookup"><span data-stu-id="45245-464">*One of the original CSS files in the Scripts folder*</span></span>
8. <span data-ttu-id="45245-465">키를 눌러 **F5** 탐색 응용 프로그램을 실행 하는 **최적화** 페이지.</span><span class="sxs-lookup"><span data-stu-id="45245-465">Press **F5** to run the application and navigate to the **Optimization** page.</span></span>
9. <span data-ttu-id="45245-466">클릭는 **CSS 번들** 링크를 다운로드 하 여 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="45245-466">Click on the **CSS Bundle** link to download and open the file.</span></span>

    <span data-ttu-id="45245-467">최소화 된 번들된 파일 확인해 보세요.</span><span class="sxs-lookup"><span data-stu-id="45245-467">Check out the minified bundled file.</span></span> <span data-ttu-id="45245-468">확인할 수 있습니다는 공백, 주석 및 들여쓰기 문자 제거 되었거나, 더 작은 파일을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-468">You will notice that all the blank spaces, comments and indentation characters have been removed, generating a smaller file.</span></span>

    <span data-ttu-id="45245-469">![CSS 파일을 번들로](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image52.png "Bundled CSS 파일")</span><span class="sxs-lookup"><span data-stu-id="45245-469">![Bundled CSS files](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image52.png "Bundled CSS files")</span></span>

    <span data-ttu-id="45245-470">*CSS 파일을 번들로 묶은*</span><span class="sxs-lookup"><span data-stu-id="45245-470">*Bundled CSS files*</span></span>
10. <span data-ttu-id="45245-471">이제 클릭는 **JS 번들** 링크를 번들로 제공 되는 JavaScript 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="45245-471">Now click the **JS Bundle** link to open the JavaScript bundled file.</span></span> <span data-ttu-id="45245-472">Warning 탐색기 안전 하 게 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-472">You can safely disregard the explorer warning.</span></span> <span data-ttu-id="45245-473">JavaScript 파일을 확인할 수는 **사용자 지정** 폴더도 번들로 제공 되며 축소 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-473">Notice the JavaScript files under the **custom** folder are also bundled and minified.</span></span>

    <span data-ttu-id="45245-474">![JavaScript 파일을 번들로](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image53.png "Bundled JavaScript 파일")</span><span class="sxs-lookup"><span data-stu-id="45245-474">![Bundled JavaScript files](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image53.png "Bundled JavaScript files")</span></span>

    <span data-ttu-id="45245-475">*번들로 묶은 JavaScript 파일*</span><span class="sxs-lookup"><span data-stu-id="45245-475">*Bundled JavaScript files*</span></span>

    <span data-ttu-id="45245-476">CSS 또는 JS 파일에 대 한 압축을 사용 하도록 설정 된 이전 ASP.NET 버전에서 훨씬 더 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-476">Enabling compression for CSS or JS files was much more complicated in previous ASP.NET version.</span></span> <span data-ttu-id="45245-477">이제, 위에서 설명한 것 처럼 하기만 하면에서 한 줄을 추가 하는 *Global.asax* 번들을 사용할 수 있도록 파일을 다음 사이트에서 번들된 파일을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-477">Now, as you have seen, you just need to add one line in the *Global.asax* file to enable bundling, and then reference the bundled files from your site.</span></span>

<a id="Ex4Task3"></a>

<a id="Task_3_-_Static_Bundles"></a>
#### <a name="task-3---static-bundles"></a><span data-ttu-id="45245-478">작업 3-정적 번들</span><span class="sxs-lookup"><span data-stu-id="45245-478">Task 3 - Static Bundles</span></span>

<span data-ttu-id="45245-479">정적 번들 접근 방식을 사용 하면 번들, 참조 및 축소 방법 사용 되는 파일의 집합을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-479">The static bundle approach allows you to customize the set of files to bundle, the reference and the minification method that will be used.</span></span>

<span data-ttu-id="45245-480">이 작업을 번들로 축소할 파일의 특정 집합을 정의 하는 정적 번들을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-480">In this task, you will configure a static bundle to define a specific set of files to bundle and minify.</span></span>

1. <span data-ttu-id="45245-481">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-481">Close the browser.</span></span>
2. <span data-ttu-id="45245-482">열기는 **Global.asax.cs** 파일를 찾습니다는 **응용 프로그램\_시작** 메서드.</span><span class="sxs-lookup"><span data-stu-id="45245-482">Open the **Global.asax.cs** file and locate the **Application\_Start** method.</span></span>
3. <span data-ttu-id="45245-483">아래 코드에 나와 있는 것 처럼 정적 번들 코드 주석 처리를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-483">Uncomment the static bundle code as shown in the code below.</span></span>

    <span data-ttu-id="45245-484">정적으로 참조 되는 번들을 정의 하는 &quot; **~/StaticBundle** &quot; 가상 경로 및 사용 하 여 **JsMinify** 와 지정 된 모든 파일의 축소에 대 한는 **AddFile** 메서드.</span><span class="sxs-lookup"><span data-stu-id="45245-484">You are defining a static bundle that will be referenced with the &quot;**~/StaticBundle**&quot; virtual path and use **JsMinify** for minification of all the specified files with the **AddFile** method.</span></span> <span data-ttu-id="45245-485">마지막으로 정적 번들을 추가 하는 **BundleTable** 및 설정 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-485">Finally, you are adding the static bundle to the **BundleTable** and enabling it.</span></span>

    <span data-ttu-id="45245-486">파일 위치;에 있지 공지 기본 번들을 통해 또 다른 이점은입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-486">Notice that the files are not located in the same place; this is another advantage over the default bundling.</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample14.cs)]
~~~
4. <span data-ttu-id="45245-487">열기는 **Optimization.aspx** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-487">Open the **Optimization.aspx** file.</span></span>

    <span data-ttu-id="45245-488">에 대 한 링크 **정적 JS 번들** Global.asax.cs 파일에는 정적 번들을 구성 하는 경우 사용자가 선언한 경로 사용 하는: **/StaticBundle**합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-488">Notice that the link to **Static JS Bundle** is using the path you have declared when you configured the static bundle in the Global.asax.cs file: **/StaticBundle**.</span></span>


~~~
[!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample15.aspx)]
~~~
5. <span data-ttu-id="45245-489">키를 눌러 **F5** 응용 프로그램을 실행 한 다음로 이동 하 여 **최적화** 페이지.</span><span class="sxs-lookup"><span data-stu-id="45245-489">Press **F5** to run the application, and then navigate to the **Optimization** page.</span></span>
6. <span data-ttu-id="45245-490">클릭는 **정적 JS 번들** 링크 파일을 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-490">Click on the **Static JS Bundle** link to open the file.</span></span>

    <span data-ttu-id="45245-491">하는 경우 bundled JavaScript 파일은 정적 번들 파일의 경로 아래에 구성 된 모든 JavaScript 파일에 대 한 출력 &quot;/StaticBundle&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-491">Notice that the minified bundled JavaScript file is the output for all the JavaScript files configured in the static bundle file under the path &quot;/StaticBundle&quot;.</span></span>

    <span data-ttu-id="45245-492">![정적 JavaScript 파일 번들](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image54.png "정적 JavaScript 파일 번들")</span><span class="sxs-lookup"><span data-stu-id="45245-492">![Static JavaScript files bundle](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image54.png "Static JavaScript files bundle")</span></span>

    <span data-ttu-id="45245-493">*정적 JavaScript 파일을 번들*</span><span class="sxs-lookup"><span data-stu-id="45245-493">*Static JavaScript files bundle*</span></span>
7. <span data-ttu-id="45245-494">브라우저를 닫고 Visual Studio로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="45245-494">Close the browser and return to Visual Studio.</span></span>

<a id="Ex4Task4"></a>

<a id="Task_4_-_Dynamic_Folder_Bundles"></a>
#### <a name="task-4---dynamic-folder-bundles"></a><span data-ttu-id="45245-495">작업 4-동적 폴더 번들</span><span class="sxs-lookup"><span data-stu-id="45245-495">Task 4 - Dynamic Folder Bundles</span></span>

<span data-ttu-id="45245-496">이 작업에서는 동적 폴더 번들을 구성 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-496">In this task, you will learn how to configure dynamic folder bundles.</span></span> <span data-ttu-id="45245-497">동적 번들의 이점은 JavaScript로 컴파일되는 언어의 정적 JavaScript 뿐만 아니라 다른 파일을 포함 하 고, 필요로 하기 때문에 번들로 실행 하기 전에 일부 처리 수입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-497">The power of dynamic bundling is that you can include static JavaScript, as well as other files in languages that compiles into JavaScript, and thus, require some processing before the bundling is executed.</span></span>

<span data-ttu-id="45245-498">이 예에서 사용 하는 방법을 배우게 됩니다는 **DynamicFolderBundle** 클래스 CofeeScript로 작성 된 파일에 대 한 동적 번들 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-498">In this example, you will learn how to use the **DynamicFolderBundle** class to create a dynamic bundle for files written in CofeeScript.</span></span> <span data-ttu-id="45245-499">CofeeScript는 JavaScript로 컴파일되 JavaScript 코드를 작성, JavaScript의 간결한 및 가독성 향상에 대 한 간단한 구문을 제공 하는 프로그래밍 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-499">CofeeScript is a programming language that compiles into JavaScript and provides a simpler syntax for writing JavaScript code, enhancing JavaScript's brevity and readability.</span></span>

1. <span data-ttu-id="45245-500">열기는 **Global.asax.cs** 파일를 찾습니다는 **응용 프로그램\_시작** 메서드.</span><span class="sxs-lookup"><span data-stu-id="45245-500">Open the **Global.asax.cs** file and locate the **Application\_Start** method.</span></span>
2. <span data-ttu-id="45245-501">다음 코드 에서처럼 동적 번들 코드 주석 처리를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-501">Uncomment the dynamic bundle code as shown in the code below.</span></span>

    <span data-ttu-id="45245-502">사용 하는 동적 폴더 번들을 정의 하는 **CoffeeMinify** 사용자 지정 축소 프로세서를 사용 하 여 파일에만 적용 됩니다는 &quot; **.coffee** &quot; 확장 드 ( CoffeeScript 파일)입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-502">You are defining a dynamic folder bundle that will use the **CoffeeMinify** custom minification processor that will only apply to the files with the &quot;**.coffee**&quot; extension (CoffeeScript files).</span></span> <span data-ttu-id="45245-503">파일 폴더 내의 같은 번들을 선택 하는 검색 패턴을 사용할 수 있는 알림 '\*.coffee'.</span><span class="sxs-lookup"><span data-stu-id="45245-503">Notice that you can use a search pattern to select the files to bundle within a folder, like '\*.coffee'.</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample16.cs)]
~~~
3. <span data-ttu-id="45245-504">NuGet 패키지 관리자 콘솔을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="45245-504">Open the NuGet Package Manager Console.</span></span> <span data-ttu-id="45245-505">이 작업을 수행 하려면 메뉴 사용 **보기** | **다른 창** | **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-505">To do this, use the menu **View** | **Other Windows** | **Package Manager Console**.</span></span>
4. <span data-ttu-id="45245-506">에 **패키지 관리자 콘솔** 형식 **Install-package CoffeeSharp** 누릅니다 **ENTER**합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-506">In the **Package Manager Console,** type **Install-Package CoffeeSharp** and press **ENTER**.</span></span>
5. <span data-ttu-id="45245-507">클릭는 **모든 파일 표시** 단추는 **솔루션 탐색기** 창</span><span class="sxs-lookup"><span data-stu-id="45245-507">Click the **Show All Files** button in the **Solution Explorer** window</span></span>

    <span data-ttu-id="45245-508">![모든 파일 표시](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image55.png "모든 파일 표시")</span><span class="sxs-lookup"><span data-stu-id="45245-508">![Showing all files](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image55.png "Showing all files")</span></span>

    <span data-ttu-id="45245-509">*모든 파일 표시*</span><span class="sxs-lookup"><span data-stu-id="45245-509">*Showing all files*</span></span>
6. <span data-ttu-id="45245-510">마우스 오른쪽 단추로 클릭는 **CoffeeMinify.cs** 파일에 **솔루션 탐색기** 선택 **프로젝트에 포함**</span><span class="sxs-lookup"><span data-stu-id="45245-510">Right click the **CoffeeMinify.cs** file in the **Solution Explorer** and select **Include in Project**</span></span>

    <span data-ttu-id="45245-511">![프로젝트에 CoffeeMinify.cs 파일 포함](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image56.png "CoffeeMinify.cs 파일은 프로젝트에 포함")</span><span class="sxs-lookup"><span data-stu-id="45245-511">![Include the CoffeeMinify.cs file in the project](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image56.png "Include the CoffeeMinify.cs file in the project")</span></span>

    <span data-ttu-id="45245-512">*프로젝트에 CoffeeMinify.cs 파일 포함*</span><span class="sxs-lookup"><span data-stu-id="45245-512">*Include the CoffeeMinify.cs file in the project*</span></span>
7. <span data-ttu-id="45245-513">열기는 **CoffeeMinify.cs** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-513">Open the **CoffeeMinify.cs** file.</span></span>

    <span data-ttu-id="45245-514">이 클래스에서 JsMinify 축소할 CoffeeScript 코드 컴파일 얻는 JavaScript 출력을 상속 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-514">This class inherits from JsMinify to minify the JavaScript output resulting from the CoffeeScript code compilation.</span></span> <span data-ttu-id="45245-515">먼저, JavaScript 코드를 생성 하려면 CoffeeScript 컴파일러를 호출 하 고에 전송할 JsMinify.Process 메서드 결과 코드 축소할를 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="45245-515">It calls the CoffeeScript compiler to generate the JavaScript code first, and then it sends it to the JsMinify.Process method to minify the resulting code.</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample17.cs)]
~~~
8. <span data-ttu-id="45245-516">열기는 **Script1.coffee** 및 **Script2.coffee** 에서 파일의 **스크립트/번들** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-516">Open the **Script1.coffee** and **Script2.coffee** files from the **Scripts/bundle** folder.</span></span>

    <span data-ttu-id="45245-517">이러한 파일 CoffeeMinify 클래스와 함께 번들로 수행 하는 동안 컴파일해야 할 CoffeScript 코드가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45245-517">These files will include the CoffeScript code to be compiled while performing the bundling with the CoffeeMinify class.</span></span>

    <span data-ttu-id="45245-518">단순성을 위해 제공 된 CoffeeScript 파일 CoffeeScript 샘플 코드만 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-518">For simplicity purposes, the CoffeeScript files provided are only including CoffeeScript sample code.</span></span> <span data-ttu-id="45245-519">주석은은 JsMinify 프로세스에 의해 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45245-519">The comments are excluded by the JsMinify process.</span></span>

    <span data-ttu-id="45245-520">![CoffeeScript 파일](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image57.png "CoffeeScript 파일")</span><span class="sxs-lookup"><span data-stu-id="45245-520">![CoffeeScript files](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image57.png "CoffeeScript files")</span></span>

    <span data-ttu-id="45245-521">*CoffeeScript 파일*</span><span class="sxs-lookup"><span data-stu-id="45245-521">*CoffeeScript files*</span></span>

    > [!NOTE]
    > <span data-ttu-id="45245-522">[CofeeScript](https://github.com/jashkenas/coffeescript/) JavaScript 코드를 작성, JavaScript의 간결한 및 가독성을 향상으로 배열 이해 및 패턴 일치와 같은 다른 기능을 추가 하는 간단한 구문을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-522">[CofeeScript](https://github.com/jashkenas/coffeescript/) provides a simpler syntax for writing JavaScript code, enhancing JavaScript's brevity and readability, as well as adding other features like array comprehension and pattern matching.</span></span>
9. <span data-ttu-id="45245-523">열기는 **Optimization.aspx** 파일을 번들 링크를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-523">Open the **Optimization.aspx** file and locate the bundle links.</span></span>

    <span data-ttu-id="45245-524">에 대 한 링크 **동적 JS 번들** 참조 하는 **스크립트/번들** 를 사용 하 여 폴더는 **커피/** 접미사 동적 폴더 번들에 대 한 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-524">Notice that the link to **Dynamic JS Bundle** is referencing the **Scripts/bundle** folder by using the **/Coffee** suffix you configured for the dynamic folder bundle.</span></span>


~~~
[!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample18.aspx)]
~~~
10. <span data-ttu-id="45245-525">키를 눌러 **F5** 응용 프로그램을 실행 한 다음로 이동 하 여 **최적화** 페이지.</span><span class="sxs-lookup"><span data-stu-id="45245-525">Press **F5** to run the application, and then navigate to the **Optimization** page.</span></span>
11. <span data-ttu-id="45245-526">클릭는 **동적 JS 번들** 링크를 생성된 된 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="45245-526">Click on the **Dynamic JS Bundle** link to open the generated file.</span></span>

    <span data-ttu-id="45245-527">이 번들에 포함 된 내용을 포함 하는 알림 **.coffee** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-527">Notice that the content that was included in this bundle only contains **.coffee** files.</span></span> <span data-ttu-id="45245-528">CoffeeScript 코드가 JavaScript로 컴파일 되었음을 않으며 주석 줄 삭제 되었습니다. 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-528">You can also see that the CoffeeScript code was compiled to JavaScript and the commented-out lines has been removed.</span></span>

    <span data-ttu-id="45245-529">![동적 JS 파일을 번들](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image58.png "동적 JS 파일 번들")</span><span class="sxs-lookup"><span data-stu-id="45245-529">![Dynamic JS files bundle](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image58.png "Dynamic JS files bundle")</span></span>

    <span data-ttu-id="45245-530">*동적 JS 파일을 번들*</span><span class="sxs-lookup"><span data-stu-id="45245-530">*Dynamic JS files bundle*</span></span>

> [!NOTE]
> <span data-ttu-id="45245-531">다음 Windows Azure 웹 사이트에이 응용 프로그램을 배포할 수는 또한 [부록 b: 게시 웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램](#AppendixB)합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-531">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>


<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="45245-532">요약</span><span class="sxs-lookup"><span data-stu-id="45245-532">Summary</span></span>

<span data-ttu-id="45245-533">이 랩에서 사용 하면 Visual Studio 2012에서 웹 개발 및 ASP.NET의 새로운 란 무엇이 고 Visual Studio 2012의 향상 된 기능이 다양 한 기능을 활용 하는 방법을 이해 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-533">This lab helps you to understand what New in ASP.NET and Web Development in Visual Studio 2012 is and how to take advantage of the variety of enhancements in Visual Studio 2012.</span></span>

<span data-ttu-id="45245-534">이 실습 랩을 완료 하면 Visual Studio 2012 편집기에서 CSS, JavaScript 및 HTML에 대 한 새로운 기능과 향상 된 기능을 사용 하는 방법을 배운 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-534">By completing this Hands-On Lab, you have learnt how to use the new features and improvements in Visual Studio 2012 Editors for CSS, JavaScript and HTML.</span></span> <span data-ttu-id="45245-535">또한 Visual Studio 2012에서 기본 제공 묶음 및 축소를 구현 하는 방법에 대해 배운 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-535">In addition, you have learnt how Visual Studio 2012 implements built-in bundling and minification.</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="45245-536">부록 a: 설치 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="45245-536">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="45245-537">설치할 수 있습니다 **Microsoft Visual Studio Express 2012 for Web** 또는 다른 &quot;Express&quot; 버전을 사용 하 여 **[Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="45245-537">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="45245-538">다음 지침을 설치 하는 데 필요한 단계를 안내 하 *Visual studio Express 2012 for Web* 를 사용 하 여 *Microsoft 웹 플랫폼 설치 관리자*합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-538">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="45245-539">로 이동 [ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169)합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-539">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="45245-540">또는 이미 설치 된 웹 플랫폼 설치 관리자를 열 수 있습니다 및 제품에 대 한 검색 &quot; <em>Visual Studio Express 2012 for Web Windows Azure SDK와</em>&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-540">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="45245-541">클릭 **지금 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-541">Click on **Install Now**.</span></span> <span data-ttu-id="45245-542">없는 경우 **웹 플랫폼 설치 관리자** 를 다운로드 하 여 앱을 먼저 설치 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-542">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="45245-543">한 번 **웹 플랫폼 설치 관리자** 열려 클릭 **설치** 는 설치 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-543">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="45245-544">![Visual Studio Express 설치](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image59.png "Visual Studio Express 설치")</span><span class="sxs-lookup"><span data-stu-id="45245-544">![Install Visual Studio Express](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image59.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="45245-545">*Visual Studio Express 설치*</span><span class="sxs-lookup"><span data-stu-id="45245-545">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="45245-546">모든 제품의 라이선스 및 용어를 읽고 클릭 **동의** 를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-546">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![사용 조건 동의](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image60.png)

    <span data-ttu-id="45245-548">*사용 조건 동의*</span><span class="sxs-lookup"><span data-stu-id="45245-548">*Accepting the license terms*</span></span>
5. <span data-ttu-id="45245-549">다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="45245-549">Wait until the downloading and installation process completes.</span></span>

    ![설치 진행률](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image61.png)

    <span data-ttu-id="45245-551">*설치 진행률*</span><span class="sxs-lookup"><span data-stu-id="45245-551">*Installation progress*</span></span>
6. <span data-ttu-id="45245-552">설치가 완료 되 면 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-552">When the installation completes, click **Finish**.</span></span>

    ![설치 완료](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image62.png)

    <span data-ttu-id="45245-554">*설치 완료*</span><span class="sxs-lookup"><span data-stu-id="45245-554">*Installation completed*</span></span>
7. <span data-ttu-id="45245-555">클릭 **종료** 를 웹 플랫폼 설치 관리자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-555">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="45245-556">Visual Studio Express for Web을 열려면로 이동는 **시작** 화면를 쓰기 시작할 &quot; **VS Express**&quot;, 클릭는 **VS Express for Web** 바둑판식 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-556">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![웹 타일에 대 한 VS Express](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image63.png)

    <span data-ttu-id="45245-558">*웹 타일에 대 한 VS Express*</span><span class="sxs-lookup"><span data-stu-id="45245-558">*VS Express for Web tile*</span></span>

* * *

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="45245-559">부록 b: 웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="45245-559">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="45245-560">이 부록에서는 Windows Azure 관리 포털에서 새 웹 사이트를 만들고 Windows Azure에서 제공 하는 웹 배포 게시 기능을 활용 하기 위해 랩에서 수행 하 여 가져온 응용 프로그램을 게시 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="45245-560">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="45245-561">작업 1-Windows에서 새 웹 사이트를 만드는 Azure 포털</span><span class="sxs-lookup"><span data-stu-id="45245-561">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="45245-562">이동 하 여 [Windows Azure 관리 포털](https://manage.windowsazure.com/) 구독에 연결 된 Microsoft 자격 증명을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-562">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="45245-563">Windows Azure를 무료로 10 개 ASP.NET 웹 사이트를 호스트 하 고 트래픽이 증가 됨을 확장 한 다음 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-563">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="45245-564">등록할 수 [여기](http://aka.ms/aspnet-hol-azure)합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-564">You can sign up [here](http://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="45245-565">![Windows Azure 포털에 로그온](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image64.png "Windows Azure 포털에 로그인")</span><span class="sxs-lookup"><span data-stu-id="45245-565">![Log on to Windows Azure portal](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image64.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="45245-566">*Windows Azure 관리 포털에 로그온*</span><span class="sxs-lookup"><span data-stu-id="45245-566">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="45245-567">클릭 **새로** 명령 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-567">Click **New** on the command bar.</span></span>

    <span data-ttu-id="45245-568">![새 웹 사이트를 만드는](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image65.png "새 웹 사이트 만들기")</span><span class="sxs-lookup"><span data-stu-id="45245-568">![Creating a new Web Site](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image65.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="45245-569">*새 웹 사이트 만들기*</span><span class="sxs-lookup"><span data-stu-id="45245-569">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="45245-570">클릭 **계산** | **웹 사이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-570">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="45245-571">그런 다음 선택 **빠른 생성** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-571">Then select **Quick Create** option.</span></span> <span data-ttu-id="45245-572">새 웹 사이트에 대 한 사용 가능한 URL을 입력 하 고 클릭 **웹 사이트 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-572">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="45245-573">Windows Azure 웹 사이트는 호스트를 제어 하 고 관리할 수 있는 클라우드에서 실행 되는 웹 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-573">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="45245-574">빨리 만들기 옵션을 사용 하면 완성 된 웹 응용 프로그램을 Windows Azure 웹 사이트에서 포털 외부에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-574">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="45245-575">데이터베이스를 설정 하기 위한 단계는 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-575">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="45245-576">![빠른 생성을 사용 하 여 새 웹 사이트를 만드는](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image66.png "빠른 생성을 사용 하 여 새 웹 사이트 만들기")</span><span class="sxs-lookup"><span data-stu-id="45245-576">![Creating a new Web Site using Quick Create](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image66.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="45245-577">*빠른 생성을 사용 하 여 새 웹 사이트 만들기*</span><span class="sxs-lookup"><span data-stu-id="45245-577">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="45245-578">새 될 때까지 기다렸다가 **웹 사이트** 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="45245-578">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="45245-579">웹 사이트가 만들어지면 아래 링크를 클릭 하 고 **URL** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-579">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="45245-580">새 웹 사이트가 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-580">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="45245-581">![새 웹 사이트를 찾아](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image67.png "새 웹 사이트를 검색 합니다.")</span><span class="sxs-lookup"><span data-stu-id="45245-581">![Browsing to the new web site](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image67.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="45245-582">*새 웹 사이트를 검색합니다.*</span><span class="sxs-lookup"><span data-stu-id="45245-582">*Browsing to the new web site*</span></span>

    <span data-ttu-id="45245-583">![실행 중인 웹 사이트](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image68.png "실행 중인 웹 사이트")</span><span class="sxs-lookup"><span data-stu-id="45245-583">![Web site running](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image68.png "Web site running")</span></span>

    <span data-ttu-id="45245-584">*실행 중인 웹 사이트*</span><span class="sxs-lookup"><span data-stu-id="45245-584">*Web site running*</span></span>
6. <span data-ttu-id="45245-585">포털로 돌아가서 아래에서 웹 사이트의 이름을 클릭는 **이름** 관리 페이지를 표시 하는 열입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-585">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="45245-586">![웹 사이트 관리 페이지 열기](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image69.png "웹 사이트 관리 페이지 열기")</span><span class="sxs-lookup"><span data-stu-id="45245-586">![Opening the web site management pages](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image69.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="45245-587">*웹 사이트 관리 페이지 열기*</span><span class="sxs-lookup"><span data-stu-id="45245-587">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="45245-588">에 **대시보드** 페이지의 **눈에 보는** 섹션에서 클릭는 **게시 프로필 다운로드** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-588">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="45245-589">*게시 프로필* 각각의 활성화 된 게시 방법에 대 한 Windows Azure 웹 사이트에 웹 응용 프로그램을 게시 하는 데 필요한 정보가 모두 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-589">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="45245-590">게시 프로필에는 Url, 사용자 자격 증명 및 연결 하 고 각 게시 메서드를 사용할 수 있는 끝점에 대해 인증 하는 데 필요한 데이터베이스 문자열이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-590">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="45245-591">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** 및 **Microsoft Visual Studio 2012** 읽는 지원 하기 위해 게시 프로필에 대 한 이러한 프로그램의 구성을 자동화 Windows Azure 웹 사이트에 웹 응용 프로그램을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-591">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="45245-592">![게시 프로필 다운로드 웹 사이트](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image70.png "게시 프로필 다운로드 웹 사이트")</span><span class="sxs-lookup"><span data-stu-id="45245-592">![Downloading the web site publish profile](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image70.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="45245-593">*게시 프로필 다운로드 웹 사이트*</span><span class="sxs-lookup"><span data-stu-id="45245-593">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="45245-594">알려진된 위치에 게시 프로필 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-594">Download the publish profile file to a known location.</span></span> <span data-ttu-id="45245-595">더 이상이 연습에서는 Visual Studio에서 웹 응용 프로그램 Windows Azure 웹 사이트를 게시 하려면이 파일을 사용 하는 방법을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45245-595">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="45245-596">![게시 프로필 파일을 저장](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image71.png "게시 프로필 저장")</span><span class="sxs-lookup"><span data-stu-id="45245-596">![Saving the publish profile file](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image71.png "Saving the publish profile")</span></span>

    <span data-ttu-id="45245-597">*게시 프로필 파일을 저장합니다.*</span><span class="sxs-lookup"><span data-stu-id="45245-597">*Saving the publish profile file*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="45245-598">작업 2-데이터베이스 서버 구성</span><span class="sxs-lookup"><span data-stu-id="45245-598">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="45245-599">응용 프로그램에서 SQL Server를 활용 하는 경우 데이터베이스를 SQL 데이터베이스 서버 만들기 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-599">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="45245-600">SQL Server를 사용 하지 않는 간단한 응용 프로그램을 배포 하려는 경우이 태스크를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-600">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="45245-601">응용 프로그램 데이터베이스를 저장 하기 위해 SQL 데이터베이스 서버를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-601">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="45245-602">Windows Azure 관리 포털에서 구독의 SQL 데이터베이스 서버를 볼 수 있습니다 **Sql 데이터베이스** | **서버** | **서버 대시보드**합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-602">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="45245-603">만든 서버 없는 경우 수행 하 여 만들 수 있습니다는 **추가** 명령 모음에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-603">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="45245-604">기록해는 **서버 이름 및 URL, 관리자 로그인 이름 및 암호**, 다음 작업에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45245-604">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="45245-605">만들지 마십시오 데이터베이스 아직 대로 이후 단계에서 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45245-605">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="45245-606">![SQL 데이터베이스 서버 대시보드](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image72.png "SQL 데이터베이스 서버 대시보드")</span><span class="sxs-lookup"><span data-stu-id="45245-606">![SQL Database Server Dashboard](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image72.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="45245-607">*SQL 데이터베이스 서버 대시보드*</span><span class="sxs-lookup"><span data-stu-id="45245-607">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="45245-608">다음 태스크에서는 서버 목록에 사용자의 로컬 IP 주소를 포함 해야 이러한 이유로 Visual Studio에서 데이터베이스 연결을 테스트 **허용 IP 주소**합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-608">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="45245-609">작업을 수행 하려면 **구성**에서 IP 주소를 선택 **현재 클라이언트 IP 주소** 에 붙여넣습니다는 **시작 IP 주소** 및 **끝IP주소** 텍스트 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-609">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes.</span></span> <span data-ttu-id="45245-610">규칙에 대 한 이름을 입력 하 고 클릭 하 고 ![add-client-ip-address-ok-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image73.png) 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-610">Enter a name for the rule and click the ![add-client-ip-address-ok-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image73.png) button.</span></span>

    ![클라이언트 IP 주소를 추가합니다.](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image74.png)

    <span data-ttu-id="45245-612">*클라이언트 IP 주소를 추가합니다.*</span><span class="sxs-lookup"><span data-stu-id="45245-612">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="45245-613">한 번는 **클라이언트 IP 주소** 허용된 된 IP 주소에 추가 됩니다 목록에서 클릭 **저장** 하 여 변경 사항을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-613">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![변경 확인](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image75.png)

    <span data-ttu-id="45245-615">*변경 확인*</span><span class="sxs-lookup"><span data-stu-id="45245-615">*Confirm Changes*</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="45245-616">작업 3-웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="45245-616">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="45245-617">ASP.NET MVC 4 솔루션으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="45245-617">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="45245-618">에 **솔루션 탐색기**웹 사이트 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-618">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="45245-619">![응용 프로그램을 게시](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image76.png "응용 프로그램을 게시")</span><span class="sxs-lookup"><span data-stu-id="45245-619">![Publishing the Application](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image76.png "Publishing the Application")</span></span>

    <span data-ttu-id="45245-620">*웹 사이트를 게시*</span><span class="sxs-lookup"><span data-stu-id="45245-620">*Publishing the web site*</span></span>
2. <span data-ttu-id="45245-621">첫 번째 작업에서 저장 한 게시 프로필을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="45245-621">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="45245-622">![게시 프로필 가져오기](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image77.png "게시 프로필 가져오기")</span><span class="sxs-lookup"><span data-stu-id="45245-622">![Importing the publish profile](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image77.png "Importing the publish profile")</span></span>

    <span data-ttu-id="45245-623">*게시 프로필 가져오기*</span><span class="sxs-lookup"><span data-stu-id="45245-623">*Importing publish profile*</span></span>
3. <span data-ttu-id="45245-624">클릭 **연결 확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-624">Click **Validate Connection**.</span></span> <span data-ttu-id="45245-625">유효성 검사가 완료 되 면 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-625">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="45245-626">연결 유효성 검사 단추 옆에 표시 녹색 확인 표시가 표시 되 면 유효성 검사가 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="45245-626">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="45245-627">![연결 유효성 검사](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image78.png "연결 유효성 검사")</span><span class="sxs-lookup"><span data-stu-id="45245-627">![Validating connection](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image78.png "Validating connection")</span></span>

    <span data-ttu-id="45245-628">*연결 유효성 검사*</span><span class="sxs-lookup"><span data-stu-id="45245-628">*Validating connection*</span></span>
4. <span data-ttu-id="45245-629">에 **설정** 페이지의 **데이터베이스** 섹션에서 데이터베이스 연결의 텍스트 상자 옆의 단추 클릭 (즉, **DefaultConnection**).</span><span class="sxs-lookup"><span data-stu-id="45245-629">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="45245-630">![웹 배포 구성](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image79.png "웹 배포 구성")</span><span class="sxs-lookup"><span data-stu-id="45245-630">![Web deploy configuration](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image79.png "Web deploy configuration")</span></span>

    <span data-ttu-id="45245-631">*웹 배포 구성*</span><span class="sxs-lookup"><span data-stu-id="45245-631">*Web deploy configuration*</span></span>
5. <span data-ttu-id="45245-632">다음과 같이 데이터베이스 연결을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-632">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="45245-633">에 **서버 이름** SQL 데이터베이스 서버 URL 사용 하 여 입력 된 *tcp:* 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="45245-633">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="45245-634">**사용자 이름** 서버 관리자 로그인 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-634">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="45245-635">**암호** 서버 관리자 로그인 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-635">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="45245-636">예를 들어 새 데이터베이스 이름 입력: *MVC4SampleDB*합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-636">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="45245-637">![대상 연결 문자열 구성](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image80.png "대상 연결 문자열 구성")</span><span class="sxs-lookup"><span data-stu-id="45245-637">![Configuring destination connection string](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image80.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="45245-638">*대상 연결 문자열 구성*</span><span class="sxs-lookup"><span data-stu-id="45245-638">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="45245-639">그런 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-639">Then click **OK**.</span></span> <span data-ttu-id="45245-640">데이터베이스를 만들려는 대화 상자가 나타나면 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-640">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="45245-641">![데이터베이스를 만드는](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image81.png "데이터베이스 문자열 만들기")</span><span class="sxs-lookup"><span data-stu-id="45245-641">![Creating the database](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image81.png "Creating the database string")</span></span>

    <span data-ttu-id="45245-642">*데이터베이스를 만드는 중*</span><span class="sxs-lookup"><span data-stu-id="45245-642">*Creating the database*</span></span>
7. <span data-ttu-id="45245-643">Windows azure에서 SQL 데이터베이스에 연결 하기 위해 사용할 연결 문자열은 기본 연결 텍스트 상자 내에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45245-643">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="45245-644">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-644">Then click **Next**.</span></span>

    <span data-ttu-id="45245-645">![SQL 데이터베이스를 가리키는 연결 문자열](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image82.png "SQL 데이터베이스를 가리키는 연결 문자열")</span><span class="sxs-lookup"><span data-stu-id="45245-645">![Connection string pointing to SQL Database](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image82.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="45245-646">*SQL 데이터베이스를 가리키는 연결 문자열*</span><span class="sxs-lookup"><span data-stu-id="45245-646">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="45245-647">에 **미리 보기** 페이지 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="45245-647">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="45245-648">![웹 응용 프로그램을 게시](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image83.png "웹 응용 프로그램 게시")</span><span class="sxs-lookup"><span data-stu-id="45245-648">![Publishing the web application](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image83.png "Publishing the web application")</span></span>

    <span data-ttu-id="45245-649">*웹 응용 프로그램 게시*</span><span class="sxs-lookup"><span data-stu-id="45245-649">*Publishing the web application*</span></span>
9. <span data-ttu-id="45245-650">게시 프로세스가 완료 되 면 게시 된 웹 사이트 기본 브라우저가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="45245-650">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="45245-651">![Windows Azure에 게시 된 응용 프로그램](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image84.png "Windows Azure에 게시 된 응용 프로그램")</span><span class="sxs-lookup"><span data-stu-id="45245-651">![Application published to Windows Azure](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image84.png "Application published to Windows Azure")</span></span>

    <span data-ttu-id="45245-652">*Windows Azure에 게시 된 응용 프로그램*</span><span class="sxs-lookup"><span data-stu-id="45245-652">*Application published to Windows Azure*</span></span>
