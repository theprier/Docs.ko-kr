---
uid: web-forms/overview/getting-started/creating-a-basic-web-forms-page
title: "기본 ASP.NET 4.5 Web Forms 만들기 페이지 Visual Studio 2013에서 | Microsoft Docs"
author: Erikre
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/03/2014
ms.topic: article
ms.assetid: a2f1c635-0817-4a9a-8c13-d5b5d29727c0
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/getting-started/creating-a-basic-web-forms-page
msc.type: authoredcontent
ms.openlocfilehash: 6b699cc939292b7ab0167dba7cfa6a00b681ef3a
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="creating-a-basic-aspnet-45-web-forms-page-in-visual-studio-2013"></a><span data-ttu-id="ec560-102">기본 ASP.NET 4.5 Web Forms 만들기 페이지에서 Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="ec560-102">Creating a Basic ASP.NET 4.5 Web Forms Page in Visual Studio 2013</span></span>
====================
<span data-ttu-id="ec560-103">으로 [Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="ec560-103">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="ec560-104">이 연습에서 웹 개발 환경에 대 한 소개를 제공 [Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) 및 [Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web)합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-104">This walkthrough provides you with an introduction to the Web development environment in [Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) and in [Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span> <span data-ttu-id="ec560-105">이 연습에서는 간단한 ASP.NET Web Forms 페이지를 만드는 과정을 안내 하 고 새 페이지를 만드는 컨트롤을 추가 하 고 코드를 작성 하는 기본적인 기술을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-105">This walkthrough guides you through creating a simple ASP.NET Web Forms page and illustrates the basic techniques of creating a new page, adding controls, and writing code.</span></span>

<span data-ttu-id="ec560-106">이 연습에서 설명하는 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-106">Tasks illustrated in this walkthrough include:</span></span>

- <span data-ttu-id="ec560-107">파일 시스템 Web Forms 응용 프로그램 프로젝트를 만드는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-107">Creating a file system Web Forms application project.</span></span>
- <span data-ttu-id="ec560-108">Visual Studio와 함께 파악 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-108">Familiarizing yourself with Visual Studio.</span></span>
- <span data-ttu-id="ec560-109">ASP.NET 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-109">Creating an ASP.NET page.</span></span>
- <span data-ttu-id="ec560-110">컨트롤을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-110">Adding controls.</span></span>
- <span data-ttu-id="ec560-111">이벤트 처리기를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-111">Adding event handlers.</span></span>
- <span data-ttu-id="ec560-112">실행 하 고 Visual Studio에서 페이지를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-112">Running and testing a page from Visual Studio.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ec560-113">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="ec560-113">Prerequisites</span></span>


<span data-ttu-id="ec560-114">이 연습을 완료하려면 다음 사항이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-114">In order to complete this walkthrough, you will need:</span></span>

- <span data-ttu-id="ec560-115">[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) 또는 [Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web)합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-115">[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) or [Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span> <span data-ttu-id="ec560-116">.NET Framework는 자동으로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-116">The .NET Framework is installed automatically.</span></span> 

    > [!NOTE] 
    > 
    > <span data-ttu-id="ec560-117">Microsoft Visual Studio 2013 및 Microsoft Visual Studio Express 2013 for Web은 종종로 간주 Visual Studio이 자습서 시리즈 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-117">Microsoft Visual Studio 2013 and Microsoft Visual Studio Express 2013 for Web will often be referred to as Visual Studio throughout this tutorial series.</span></span>  
    >   
    > <span data-ttu-id="ec560-118">이 연습에서는 선택 했다고 가정 Visual Studio를 사용 하는 경우는 **웹 개발** 설정의 컬렉션 처음으로 Visual Studio를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-118">If you are using Visual Studio, this walkthrough assumes that you selected the **Web Development** collection of settings the first time that you started Visual Studio.</span></span> <span data-ttu-id="ec560-119">자세한 내용은 참조 [하는 방법: 웹 개발 환경 설정 선택](https://msdn.microsoft.com/library/ff521558.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-119">For more information, see [How to: Select Web Development Environment Settings](https://msdn.microsoft.com/library/ff521558.aspx).</span></span>


## <a name="creating-a-web-application-project-and-a-page"></a><span data-ttu-id="ec560-120">웹 응용 프로그램 프로젝트 및 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="ec560-120">Creating a Web application project and a Page</span></span>

<a id="sectionToggle0"></a>

<span data-ttu-id="ec560-121">이 연습 부분에서는 웹 응용 프로그램 프로젝트를 만들고 새 페이지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-121">In this part of the walkthrough, you will create a Web application project and add a new page to it.</span></span> <span data-ttu-id="ec560-122">HTML 텍스트를 추가 및 브라우저에서 페이지를 실행도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-122">You will also add HTML text and run the page in your browser.</span></span>

### <a name="to-create-a-web-application-project"></a><span data-ttu-id="ec560-123">웹 응용 프로그램 프로젝트를 만들려면</span><span class="sxs-lookup"><span data-stu-id="ec560-123">To create a Web application project</span></span>

1. <span data-ttu-id="ec560-124">Microsoft Visual Studio를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-124">Open Microsoft Visual Studio.</span></span>
2. <span data-ttu-id="ec560-125">**파일** 메뉴에서 **새 프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-125">On the **File** menu, select **New Project**.</span></span>  
    <span data-ttu-id="ec560-126">![파일 메뉴](creating-a-basic-web-forms-page/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ec560-126">![File Menu](creating-a-basic-web-forms-page/_static/image1.png)</span></span>

    <span data-ttu-id="ec560-127">**새 프로젝트** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-127">The **New Project** dialog box appears.</span></span>
3. <span data-ttu-id="ec560-128">선택 된 **템플릿**  - &gt; **Visual C#**  - &gt; **웹** 왼쪽의 템플릿 그룹.</span><span class="sxs-lookup"><span data-stu-id="ec560-128">Select the **Templates** -&gt; **Visual C#** -&gt; **Web** templates group on the left.</span></span>
4. <span data-ttu-id="ec560-129">선택 된 **ASP.NET 웹 응용 프로그램** 가운데 열에서 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-129">Choose the **ASP.NET Web Application** template in the center column.</span></span>
5. <span data-ttu-id="ec560-130">프로젝트 이름을 ***BasicWebApp*** 클릭는 **확인** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-130">Name your project ***BasicWebApp*** and click the **OK** button.</span></span>   
<span data-ttu-id="ec560-131">![새 프로젝트 대화 상자](creating-a-basic-web-forms-page/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="ec560-131">![New Project dialog box](creating-a-basic-web-forms-page/_static/image2.png)</span></span>
6. <span data-ttu-id="ec560-132">다음으로, 선택는 **Web Forms** 템플릿과 클릭은 **확인** 단추 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-132">Next, select the **Web Forms** template and click the **OK** button to create the project.</span></span>  
<span data-ttu-id="ec560-133">![새 ASP.NET 프로젝트 대화 상자](creating-a-basic-web-forms-page/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="ec560-133">![New ASP.NET Project dialog box](creating-a-basic-web-forms-page/_static/image3.png)</span></span>  

    <span data-ttu-id="ec560-134">Visual Studio Web Forms 템플릿을 기반으로 하는 미리 작성 된 기능을 포함 하는 새 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-134">Visual Studio creates a new project that includes prebuilt functionality based on the Web Forms template.</span></span> <span data-ttu-id="ec560-135">뿐만 아니라 제공 하는 *Home.aspx* 페이지는 *About.aspx* 페이지는 *Contact.aspx* 페이지 하지만 사용자가 등록 하 고 저장 하는 멤버 자격 기능을 포함 자격 증명 웹 사이트에 로그인 할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-135">It not only provides you with a *Home.aspx* page, an *About.aspx* page, a *Contact.aspx* page, but also includes membership functionality that registers users and saves their credentials so that they can log in to your website.</span></span> <span data-ttu-id="ec560-136">새 페이지를 만들면 기본적으로 Visual Studio 표시에 있는 페이지 **소스** 페이지의 HTML 요소를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-136">When a new page is created, by default Visual Studio displays the page in **Source** view, where you can see the page's HTML elements.</span></span> <span data-ttu-id="ec560-137">다음 그림에 표시 되는 것에 나와 **소스** 라는 새 웹 페이지를 만들면 볼 *BasicWebApp.aspx*합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-137">The following illustration shows what you would see in **Source** view if you created a new Web page named *BasicWebApp.aspx*.</span></span>  
    <span data-ttu-id="ec560-138">![소스 뷰](creating-a-basic-web-forms-page/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="ec560-138">![Source View](creating-a-basic-web-forms-page/_static/image4.png)</span></span>


### <a name="a-tour-of-the-visual-studio-web-development-environment"></a><span data-ttu-id="ec560-139">Visual Studio 웹 개발 환경의 둘러보기</span><span class="sxs-lookup"><span data-stu-id="ec560-139">A Tour of the Visual Studio Web Development Environment</span></span>


<span data-ttu-id="ec560-140">페이지를 수정 하 여 계속 진행 하기 전에 Visual Studio 개발 환경에 익숙해질 수는 것이 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-140">Before you proceed by modifying the page, it is useful to familiarize yourself with the Visual Studio development environment.</span></span> <span data-ttu-id="ec560-141">다음 그림에는 windows 및 Visual Studio 및 Visual Studio Express for Web에서 사용할 수 있는 도구를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-141">The following illustration shows you the windows and tools that are available in Visual Studio and Visual Studio Express for Web.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="ec560-142">이 다이어그램에서는 기본 창 및 창 위치를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-142">This diagram shows default windows and window locations.</span></span> <span data-ttu-id="ec560-143">**보기** 메뉴 추가 창을 표시할 다시 정렬 하 고 windows 사용자 기본 설정에 맞게 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-143">The **View** menu allows you to display additional windows, and to rearrange and resize windows to suit your preferences.</span></span> <span data-ttu-id="ec560-144">변경 내용이 이미 창 정렬에 적용 된 경우 나타나는 일치 하지 않습니다는 그림입니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-144">If changes have already been made to the window arrangement, what you see will not match the illustration.</span></span>


 <span data-ttu-id="ec560-145">Visual Studio 환경</span><span class="sxs-lookup"><span data-stu-id="ec560-145">The Visual Studio environment</span></span>

![Visual Studio Environment](creating-a-basic-web-forms-page/_static/image5.png)

### <a name="familiarize-yourself-with-the-web-designer"></a><span data-ttu-id="ec560-147">웹 디자이너를 파악</span><span class="sxs-lookup"><span data-stu-id="ec560-147">Familiarize yourself with the Web designer</span></span>

<span data-ttu-id="ec560-148">위의 그림을 검토 하 고 다음 목록을 텍스트와 일치 한 창과 도구에 사용 되는 가장 일반적으로 설명 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-148">Examine the above illustration and match the text to the following list, which describes the most commonly used windows and tools.</span></span> <span data-ttu-id="ec560-149">(모든 창과 도구는 다음과 같은 볼 수 있는 표시 된 것만 앞의 그림에서입니다.)</span><span class="sxs-lookup"><span data-stu-id="ec560-149">(Not all windows and tools that you see are listed here, only those marked in the preceding illustration.)</span></span>

- <span data-ttu-id="ec560-150">도구 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-150">Toolbars.</span></span> <span data-ttu-id="ec560-151">텍스트, 텍스트 찾기 및에 서식을 지정 하기 위한 명령을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-151">Provide commands for formatting text, finding text, and so on.</span></span> <span data-ttu-id="ec560-152">일부 도구 모음은에서 작업 하는 경우에 사용할 수 있는 **디자인** 보기.</span><span class="sxs-lookup"><span data-stu-id="ec560-152">Some toolbars are available only when you are working in **Design** view.</span></span>
- <span data-ttu-id="ec560-153">**솔루션 탐색기** 창.</span><span class="sxs-lookup"><span data-stu-id="ec560-153">**Solution Explorer** window.</span></span> <span data-ttu-id="ec560-154">웹 응용 프로그램에서 파일 및 폴더를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-154">Displays the files and folders in your Web application.</span></span>
- <span data-ttu-id="ec560-155">문서 창입니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-155">Document window.</span></span> <span data-ttu-id="ec560-156">탭된 창에서 작업 하는 문서가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-156">Displays the documents you are working on in tabbed windows.</span></span> <span data-ttu-id="ec560-157">탭을 클릭 하 여 문서 간에 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-157">You can switch between documents by clicking tabs.</span></span>
- <span data-ttu-id="ec560-158">**속성** 창.</span><span class="sxs-lookup"><span data-stu-id="ec560-158">**Properties** window.</span></span> <span data-ttu-id="ec560-159">페이지, HTML 요소, 컨트롤 및 기타 개체에 대 한 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-159">Allows you to change settings for the page, HTML elements, controls, and other objects.</span></span>
- <span data-ttu-id="ec560-160">보기 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-160">View tabs.</span></span> <span data-ttu-id="ec560-161">같은 문서에 대해 서로 다른 뷰를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-161">Present you with different views of the same document.</span></span> <span data-ttu-id="ec560-162">**디자인** 뷰는 WYSIWYG 편집 화면입니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-162">**Design** view is a near-WYSIWYG editing surface.</span></span> <span data-ttu-id="ec560-163">**소스** 보기는 HTML 편집기의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-163">**Source** view is the HTML editor for the page.</span></span> <span data-ttu-id="ec560-164">**분할** 모두 뷰의 표시는 **디자인** 보기 및 **소스** 문서에 대 한 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-164">**Split** view displays both the **Design** view and the **Source** view for the document.</span></span> <span data-ttu-id="ec560-165">작업을 수행는 **디자인** 및 **소스** 이 연습의 뒷부분에서 뷰.</span><span class="sxs-lookup"><span data-stu-id="ec560-165">You will work with the **Design** and **Source** views later in this walkthrough.</span></span> <span data-ttu-id="ec560-166">웹 페이지를 열려면 선호 하는 경우 **디자인** 를 보려면는 **도구** 메뉴를 클릭 하 여 **옵션**을 선택는 **HTML 디자이너** 노드와 변경은 **에 페이지 시작** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-166">If you prefer to open Web pages in **Design** view, on the **Tools** menu, click **Options**, select the **HTML Designer** node, and change the **Start Pages In** option.</span></span>
- <span data-ttu-id="ec560-167">**도구 상자**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-167">**ToolBox**.</span></span> <span data-ttu-id="ec560-168">컨트롤 및 페이지로 끌어올 수 있는 HTML 요소를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-168">Provides controls and HTML elements that you can drag onto your page.</span></span> <span data-ttu-id="ec560-169">**도구 상자** 요소 공통 기능에 따라 그룹화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-169">**Toolbox** elements are grouped by common function.</span></span>
- <span data-ttu-id="ec560-170">S **erver 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-170">S **erver Explorer**.</span></span> <span data-ttu-id="ec560-171">데이터베이스 연결을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-171">Displays database connections.</span></span> <span data-ttu-id="ec560-172">서버 탐색기가 표시 되지 않는 경우 보기 메뉴에서 서버 탐색기를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-172">If Server Explorer is not visible, on the View menu, click Server Explorer.</span></span>


### <a name="creating-a-new-aspnet-web-forms-page"></a><span data-ttu-id="ec560-173">새 ASP.NET Web Forms 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="ec560-173">Creating a new ASP.NET Web Forms Page</span></span>


<span data-ttu-id="ec560-174">사용 하 여 새 Web Forms 응용 프로그램을 만들 때는 **ASP.NET 웹 응용 프로그램** 프로젝트 템플릿을 Visual Studio 추가 라는 ASP.NET 페이지 (Web Forms 페이지) *Default.aspx*다른 여러 파일 외에, 및 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-174">When you create a new Web Forms application using the **ASP.NET Web Application** project template, Visual Studio adds an ASP.NET page (Web Forms page) named *Default.aspx*, as well as several other files and folders.</span></span> <span data-ttu-id="ec560-175">사용할 수는 *Default.aspx* 웹 응용 프로그램에 대 한 홈 페이지와 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-175">You can use the *Default.aspx* page as the home page for your Web application.</span></span> <span data-ttu-id="ec560-176">그러나이 연습에서는 만들고 새 페이지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-176">However, for this walkthrough, you will create and work with a new page.</span></span>

### <a name="to-add-a-page-to-the-web-application"></a><span data-ttu-id="ec560-177">웹 응용 프로그램 페이지를 추가 하려면</span><span class="sxs-lookup"><span data-stu-id="ec560-177">To add a page to the Web application</span></span>


1. <span data-ttu-id="ec560-178">닫기는 *Default.aspx* 페이지.</span><span class="sxs-lookup"><span data-stu-id="ec560-178">Close the *Default.aspx* page.</span></span> <span data-ttu-id="ec560-179">이렇게 하려면 파일 이름을 표시 하는 탭을 클릭 하 고 닫기 옵션을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-179">To do this, click the tab that displays the file name and then click the close option.</span></span>
2. <span data-ttu-id="ec560-180">**솔루션 탐색기**, 웹 응용 프로그램 이름을 마우스 오른쪽 단추로 클릭 (응용 프로그램 이름이이 자습서에서는 **BasicWebSite**)를 클릭 하 고 **추가**  - &gt; **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-180">In **Solution Explorer**, right-click the Web application name (in this tutorial the application name is **BasicWebSite**), and then click **Add** -&gt; **New Item**.</span></span>   
<span data-ttu-id="ec560-181">**새 항목 추가** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-181">The **Add New Item** dialog box is displayed.</span></span>
3. <span data-ttu-id="ec560-182">선택 된 **Visual C#**  - &gt; **웹** 왼쪽의 템플릿 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-182">Select the **Visual C#** -&gt; **Web** templates group on the left.</span></span> <span data-ttu-id="ec560-183">그런 다음 선택 **Web Form** 중간에서 나열 하 고 이름을 *FirstWebPage.aspx*합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-183">Then, select **Web Form** from the middle list and name it *FirstWebPage.aspx*.</span></span>   
    <span data-ttu-id="ec560-184">![새 항목 추가 대화 상자](creating-a-basic-web-forms-page/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="ec560-184">![Add New Item dialog box](creating-a-basic-web-forms-page/_static/image6.png)</span></span>
4. <span data-ttu-id="ec560-185">클릭 **추가** 를 웹 페이지 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-185">Click **Add** to add the web page to your project.</span></span>  
<span data-ttu-id="ec560-186">Visual Studio에 새 페이지에 만들어지고 열립니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-186">Visual Studio creates the new page and opens it.</span></span>


### <a name="adding-html-to-the-page"></a><span data-ttu-id="ec560-187">페이지에 HTML 추가</span><span class="sxs-lookup"><span data-stu-id="ec560-187">Adding HTML to the Page</span></span>


<span data-ttu-id="ec560-188">이 연습 부분에서는 페이지에 몇 가지 정적 텍스트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-188">In this part of the walkthrough, you will add some static text to the page.</span></span>

### <a name="to-add-text-to-the-page"></a><span data-ttu-id="ec560-189">페이지에 텍스트를 추가 하려면</span><span class="sxs-lookup"><span data-stu-id="ec560-189">To add text to the page</span></span>


1. <span data-ttu-id="ec560-190">문서 창의 아래쪽을 클릭는 **디자인** 진행 **디자인** 보기.</span><span class="sxs-lookup"><span data-stu-id="ec560-190">At the bottom of the document window, click the **Design** tab to switch to **Design** view.</span></span>

    <span data-ttu-id="ec560-191">디자인 뷰는 WYSIWYG와 유사한 방식으로 현재 페이지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-191">Design view displays the current page in a WYSIWYG-like way.</span></span> <span data-ttu-id="ec560-192">이 시점에서 텍스트 또는 페이지의 컨트롤에 없으므로 파선 사각형의 윤곽선을 제외 하 고 페이지가 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-192">At this point, you do not have any text or controls on the page, so the page is blank except for a dashed line that outlines a rectangle.</span></span> <span data-ttu-id="ec560-193">이 사각형이 나타내는 **div** 페이지에서 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-193">This rectangle represents a **div** element on the page.</span></span>
2. <span data-ttu-id="ec560-194">점선으로 둘러싸여 사각형 내부를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-194">Click inside the rectangle that is outlined by a dashed line.</span></span>
3. <span data-ttu-id="ec560-195">형식 **Visual Web Developer 시작** 누릅니다 **ENTER** 두 번입니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-195">Type **Welcome to Visual Web Developer** and press **ENTER** twice.</span></span>

    <span data-ttu-id="ec560-196">다음 그림에 입력 한 텍스트를 보여 줍니다. **디자인** 보기.</span><span class="sxs-lookup"><span data-stu-id="ec560-196">The following illustration shows the text you typed in **Design** view.</span></span>

    <span data-ttu-id="ec560-197">![디자인 뷰의 환영 텍스트](creating-a-basic-web-forms-page/_static/image7.png "디자인 뷰의 환영 텍스트")</span><span class="sxs-lookup"><span data-stu-id="ec560-197">![Welcome text in Design view](creating-a-basic-web-forms-page/_static/image7.png "Welcome text in Design view")</span></span>
4. <span data-ttu-id="ec560-198">로 전환 **소스** 보기.</span><span class="sxs-lookup"><span data-stu-id="ec560-198">Switch to **Source** view.</span></span>

    <span data-ttu-id="ec560-199">HTML을 볼 수 **소스** 에 입력할 때 만든 보기 **디자인** 보기.</span><span class="sxs-lookup"><span data-stu-id="ec560-199">You can see the HTML in **Source** view that you created when you typed in **Design** view.</span></span>  
    <span data-ttu-id="ec560-200">![정적 텍스트와 웹 페이지](creating-a-basic-web-forms-page/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="ec560-200">![Web Page with Static Text](creating-a-basic-web-forms-page/_static/image8.png)</span></span>


### <a name="running-the-page"></a><span data-ttu-id="ec560-201">페이지를 실행 하면</span><span class="sxs-lookup"><span data-stu-id="ec560-201">Running the Page</span></span>


<span data-ttu-id="ec560-202">페이지에 컨트롤을 추가 하 여 계속 진행 하기 전에 먼저 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-202">Before you proceed by adding controls to the page, you can first run it.</span></span>

### <a name="to-run-the-page"></a><span data-ttu-id="ec560-203">페이지를 실행 하려면</span><span class="sxs-lookup"><span data-stu-id="ec560-203">To run the page</span></span>


1. <span data-ttu-id="ec560-204">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 *FirstWebPage.aspx* 선택 **시작 페이지로 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-204">In **Solution Explorer**, right-click *FirstWebPage.aspx* and select **Set as Start Page**.</span></span>
2. <span data-ttu-id="ec560-205">키를 눌러 **CTRL + f 5** 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-205">Press **CTRL+F5** to run the page.</span></span>

    <span data-ttu-id="ec560-206">페이지는 브라우저에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-206">The page is displayed in the browser.</span></span> <span data-ttu-id="ec560-207">만든 페이지의 파일 이름 확장자가 있지만 *.aspx*, HTML 페이지 처럼 현재 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-207">Although the page you created has a file-name extension of *.aspx*, it currently runs like any HTML page.</span></span>

    <span data-ttu-id="ec560-208">브라우저에서 페이지를 표시 하려면 스키마에 있는 페이지 **솔루션 탐색기** 선택 **브라우저에서 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-208">To display a page in the browser you can also right-click the page in **Solution Explorer** and select **View in Browser**.</span></span>
3. <span data-ttu-id="ec560-209">웹 응용 프로그램을 중지 하려면 브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-209">Close the browser to stop the Web application.</span></span>


## <a name="adding-and-programming-controls"></a><span data-ttu-id="ec560-210">컨트롤 추가 및 프로그래밍</span><span class="sxs-lookup"><span data-stu-id="ec560-210">Adding and Programming Controls</span></span>


<a id="sectionToggle1"></a>

<span data-ttu-id="ec560-211">이제 페이지에 서버 컨트롤을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-211">You will now add server controls to the page.</span></span> <span data-ttu-id="ec560-212">서버 컨트롤 단추, 레이블, 입력란 및 기타 친숙 한 컨트롤 같은 Web Forms 페이지에 대 한 일반적인 양식 처리 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-212">Server controls, such as buttons, labels, text boxes, and other familiar controls, provide typical form-processing capabilities for your Web Forms pages.</span></span> <span data-ttu-id="ec560-213">그러나 클라이언트가 아닌 서버에서 실행 되는 코드를 사용 하 여 컨트롤을 프로그래밍할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-213">However, you can program the controls with code that runs on the server, rather than the client.</span></span>

<span data-ttu-id="ec560-214">추가 합니다는 [단추](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) 컨트롤은 [텍스트 상자에 붙여넣습니다](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) 컨트롤 및 [레이블](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) 처리할 코드를 작성 하 고 컨트롤을 페이지는 [클릭](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) 에 대 한 이벤트 [단추](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-214">You will add a [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control, a [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) control, and a [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) control to the page and write code to handle the [Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) event for the [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control.</span></span>

### <a name="to-add-controls-to-the-page"></a><span data-ttu-id="ec560-215">페이지에 컨트롤을 추가 하려면</span><span class="sxs-lookup"><span data-stu-id="ec560-215">To add controls to the page</span></span>


1. <span data-ttu-id="ec560-216">클릭는 **디자인** 진행 **디자인** 보기.</span><span class="sxs-lookup"><span data-stu-id="ec560-216">Click the **Design** tab to switch to **Design** view.</span></span>
2. <span data-ttu-id="ec560-217">끝에 삽입 포인터를 놓습니다는 **Visual Web Developer 시작** 텍스트와 키를 눌러 **ENTER** 공간을 확보의 5 배는 **div** 요소 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-217">Put the insertion point at the end of the **Welcome to Visual Web Developer** text and press **ENTER** five or more times to make some room in the **div** element box.</span></span>
3. <span data-ttu-id="ec560-218">에 **도구 상자**를 확장 하 고는 **표준** 확장 되어 있지 않은 경우 그룹화 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-218">In the **Toolbox**, expand the **Standard** group if it is not already expanded.</span></span>  
<span data-ttu-id="ec560-219">확장 해야 할 수는 **도구 상자** 볼 왼쪽 창.</span><span class="sxs-lookup"><span data-stu-id="ec560-219">Note that you may need to expand the **Toolbox** window on the left to view it.</span></span>
4. <span data-ttu-id="ec560-220">끌어서는 [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) 컨트롤을 페이지로 끌어서 가운데는 **div** 가 있는 요소 상자 **Visual Web Developer를 시작** 첫 번째 줄에서.</span><span class="sxs-lookup"><span data-stu-id="ec560-220">Drag a [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) control onto the page and drop it in the middle of the **div** element box that has **Welcome to Visual Web Developer** in the first line.</span></span>
5. <span data-ttu-id="ec560-221">끌어서는 [단추](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) 컨트롤을 페이지로 오른쪽에 놓습니다는 [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-221">Drag a [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control onto the page and drop it to the right of the [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) control.</span></span>
6. <span data-ttu-id="ec560-222">끌어서는 [레이블](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) 컨트롤을 페이지로 별도 줄 아래에 놓습니다는 [단추](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-222">Drag a [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) control onto the page and drop it on a separate line below the [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control.</span></span>
7. <span data-ttu-id="ec560-223">위의 삽입 지점을 [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) 컨트롤을 선택한 다음 입력 **이름 입력:** 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-223">Put the insertion point above the [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) control, and then type **Enter your name:** .</span></span>

    <span data-ttu-id="ec560-224">이 정적 HTML 텍스트에 대 한 기본값은는 [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-224">This static HTML text is the caption for the [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) control.</span></span> <span data-ttu-id="ec560-225">정적 HTML과 같은 페이지에 서버 컨트롤을 혼합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-225">You can mix static HTML and server controls on the same page.</span></span> <span data-ttu-id="ec560-226">다음 그림에 세 개의 컨트롤이 표시 하는 방법을 보여 줍니다. **디자인** 보기.</span><span class="sxs-lookup"><span data-stu-id="ec560-226">The following illustration shows how the three controls appear in **Design** view.</span></span>

    <span data-ttu-id="ec560-227">![디자인 뷰에서 세 가지 컨트롤](creating-a-basic-web-forms-page/_static/image9.png "디자인 보기에서 세 가지 컨트롤")</span><span class="sxs-lookup"><span data-stu-id="ec560-227">![Three controls in Design view](creating-a-basic-web-forms-page/_static/image9.png "Three controls in Design view")</span></span>


### <a name="setting-control-properties"></a><span data-ttu-id="ec560-228">컨트롤 속성 설정</span><span class="sxs-lookup"><span data-stu-id="ec560-228">Setting Control Properties</span></span>


<span data-ttu-id="ec560-229">Visual Studio는 페이지에 있는 컨트롤의 속성을 설정 하는 다양 한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-229">Visual Studio offers you various ways to set the properties of controls on the page.</span></span> <span data-ttu-id="ec560-230">이 연습 부분에서는 모두에서 속성을 설정 합니다 **디자인** 보기 및 **소스** 보기.</span><span class="sxs-lookup"><span data-stu-id="ec560-230">In this part of the walkthrough, you will set properties in both **Design** view and **Source** view.</span></span>

### <a name="to-set-control-properties"></a><span data-ttu-id="ec560-231">컨트롤 속성을 설정 하려면</span><span class="sxs-lookup"><span data-stu-id="ec560-231">To set control properties</span></span>


1. <span data-ttu-id="ec560-232">먼저, 표시 된 **속성** 에서 선택 하 여 windows는 **보기** 메뉴-&gt; **다른 창**  - &gt; **속성 창**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-232">First, display the **Properties** windows by selecting from the **View** menu -&gt; **Other Windows** -&gt; **Properies Window**.</span></span> <span data-ttu-id="ec560-233">또는 선택할 수 있습니다 **F4** 표시 하는 **속성** 창.</span><span class="sxs-lookup"><span data-stu-id="ec560-233">You could alternatively select **F4** to display the **Properties** window.</span></span>
2. <span data-ttu-id="ec560-234">선택의 [단추](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) 컨트롤을 선택한 다음는 **속성** 창의 설정의 값 **텍스트** 를 **표시 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-234">Select the [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control, and then in the **Properties** window, set the value of **Text** to **Display Name**.</span></span> <span data-ttu-id="ec560-235">다음 그림에 나와 있는 것 처럼 입력 한 텍스트는 디자이너의 단추에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-235">The text you entered appears on the button in the designer, as shown in the following illustration.</span></span>

    <span data-ttu-id="ec560-236">![단추 텍스트 설정](creating-a-basic-web-forms-page/_static/image10.png "설정 단추 텍스트")</span><span class="sxs-lookup"><span data-stu-id="ec560-236">![Set Button text](creating-a-basic-web-forms-page/_static/image10.png "Set Button text")</span></span>
3. <span data-ttu-id="ec560-237">로 전환 **소스** 보기.</span><span class="sxs-lookup"><span data-stu-id="ec560-237">Switch to **Source** view.</span></span>

    <span data-ttu-id="ec560-238">**소스** 보기에는 HTML 서버 컨트롤에 대 한 Visual Studio가 생성 하는 요소를 포함 하 여 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-238">**Source** view displays the HTML for the page, including the elements that Visual Studio has created for the server controls.</span></span> <span data-ttu-id="ec560-239">컨트롤이 선언 된 HTML과 유사한 구문을 사용 하 여 태그 접두사를 사용 하는 점을 제외 하 고 **asp:** 특성을 포함 하 고 **runat =&quot;서버&quot;**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-239">Controls are declared using HTML-like syntax, except that the tags use the prefix **asp:** and include the attribute **runat=&quot;server&quot;**.</span></span>

    <span data-ttu-id="ec560-240">컨트롤 속성은 특성으로 선언 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-240">Control properties are declared as attributes.</span></span> <span data-ttu-id="ec560-241">설정한 경우에 예를 들어는 [텍스트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.text.aspx) 속성에 대 한는 [단추](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) 제어 하 고, 1 단계에서 실제로 설정할는 **텍스트** 컨트롤의 태그에 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-241">For example, when you set the [Text](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.text.aspx) property for the [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control, in step 1, you were actually setting the **Text** attribute in the control's markup.</span></span>

    > [!NOTE] 
    > 
    > <span data-ttu-id="ec560-242">내 모든 컨트롤은 한 **양식** 특성도 포함 하는 요소를 **runat =&quot;서버&quot;**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-242">All the controls are inside a **form** element, which also has the attribute **runat=&quot;server&quot;**.</span></span> <span data-ttu-id="ec560-243">**runat =&quot;서버&quot;**  특성 및 **asp:** 접두사 컨트롤 태그 페이지를 실행할 때 서버에서 ASP.NET에서 처리 되기 있도록 컨트롤을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-243">The **runat=&quot;server&quot;** attribute and the **asp:** prefix for control tags mark the controls so that they are processed by ASP.NET on the server when the page runs.</span></span> <span data-ttu-id="ec560-244">외부 코드  **&lt;runat =&quot;서버&quot; &gt;**  및  **&lt;스크립트 runat =&quot;서버&quot; &gt;**  요소를 브라우저에도 때문에 ASP.NET 코드는 여는 태그를 포함 하는 요소 내부에 있어야 합니다. 변경 되지 않은 전송 되는 **runat =&quot;서버&quot;**  특성입니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-244">Code outside of **&lt;form runat=&quot;server&quot;&gt;** and **&lt;script runat=&quot;server&quot;&gt;** elements is sent unchanged to the browser, which is why the ASP.NET code must be inside an element whose opening tag contains the **runat=&quot;server&quot;** attribute.</span></span>
4. <span data-ttu-id="ec560-245">다음을 추가 속성을 추가 합니다는 [레이블](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-245">Next, you will add an additional property to the [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)  control.</span></span> <span data-ttu-id="ec560-246">후 직접 삽입 지점을 **p: Label** 에  **&lt;p: Label&gt;**  태그, 및 키를 누릅니다 **스페이스바**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-246">Put the insertion point directly after **asp:Label** in the **&lt;asp:Label&gt;** tag, and then press **SPACEBAR**.</span></span>

    <span data-ttu-id="ec560-247">설정할 수 있는 사용 가능한 속성의 목록을 표시 하는 드롭다운 목록이 나타납니다는 [레이블](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-247">A drop-down list appears that displays the list of available properties you can set for a [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) control.</span></span> <span data-ttu-id="ec560-248">이 기능으로 이라고 **IntelliSense**에서 사용 하면 **소스** 페이지에 서버 컨트롤, HTML 요소 및 기타 항목의 구문 보기.</span><span class="sxs-lookup"><span data-stu-id="ec560-248">This feature, referred to as **IntelliSense**, helps you in **Source** view with the syntax of server controls, HTML elements, and other items on the page.</span></span> <span data-ttu-id="ec560-249">다음 그림에서는 **IntelliSense** 에 대 한 드롭다운 목록에서 [레이블](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-249">The following illustration shows the **IntelliSense** drop-down list for the [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) control.</span></span>

    <span data-ttu-id="ec560-250">![IntelliSense 특성](creating-a-basic-web-forms-page/_static/image11.png "IntelliSense 특성")</span><span class="sxs-lookup"><span data-stu-id="ec560-250">![IntelliSense attributes](creating-a-basic-web-forms-page/_static/image11.png "IntelliSense attributes")</span></span>
5. <span data-ttu-id="ec560-251">선택 **ForeColor** 등호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-251">Select **ForeColor** and then type an equal sign.</span></span>

    <span data-ttu-id="ec560-252">IntelliSense의 색상 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-252">IntelliSense displays a list of colors.</span></span>

    > [!NOTE] 
    > 
    > <span data-ttu-id="ec560-253">표시할 수 있습니다는 **IntelliSense** 드롭다운 목록에서 키를 눌러 언제 든 **CTRL + J** 코드를 볼 때.</span><span class="sxs-lookup"><span data-stu-id="ec560-253">You can display an **IntelliSense** drop-down list at any time by pressing **CTRL+J** when viewing code.</span></span>
6. <span data-ttu-id="ec560-254">색을 선택 된  **[레이블](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)**  컨트롤의 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-254">Select a color for the **[Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)** control's text.</span></span> <span data-ttu-id="ec560-255">흰색 배경에서 읽을 수 있도록 어두운 색을 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-255">Make sure you select a color that is dark enough to read against a white background.</span></span>

    <span data-ttu-id="ec560-256">**ForeColor** 특성 닫는 따옴표를 포함 하 여, 선택 된 색으로 완료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-256">The **ForeColor** attribute is completed with the color that you have selected, including the closing quotation mark.</span></span>


### <a name="programming-the-button-control"></a><span data-ttu-id="ec560-257">Button 컨트롤 프로그래밍</span><span class="sxs-lookup"><span data-stu-id="ec560-257">Programming the Button Control</span></span>


<span data-ttu-id="ec560-258">이 연습에서는 사용자가 텍스트 상자에 입력 하 고 다음의 이름을 표시 이름을 읽는 코드를 작성 합니다는 [레이블](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-258">For this walkthrough, you will write code that reads the name that the user enters into the text box and then displays the name in the [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) control.</span></span>

### <a name="add-a-default-button-event-handler"></a><span data-ttu-id="ec560-259">기본 단추 이벤트 처리기를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-259">Add a default button event handler</span></span>


1. <span data-ttu-id="ec560-260">로 전환 **디자인** 보기.</span><span class="sxs-lookup"><span data-stu-id="ec560-260">Switch to **Design** view.</span></span>
2. <span data-ttu-id="ec560-261">두 번 클릭 하 여 [단추](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-261">Double-click the [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control.</span></span>

    <span data-ttu-id="ec560-262">기본적으로 Visual Studio 코드 숨김 파일을 전환 하 고에 대 한 기본 이벤트 처리기를 만듭니다는 [단추](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) 컨트롤의 기본 이벤트는 [클릭](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-262">By default, Visual Studio switches to a code-behind file and creates a skeleton event handler for the [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control's default event, the [Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) event.</span></span> <span data-ttu-id="ec560-263">코드 숨김 파일 (예: C#) 서버 코드에서 UI 태그 (예: HTML)를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-263">The code-behind file separates your UI markup (such as HTML) from your server code (such as C#).</span></span>   
<span data-ttu-id="ec560-264">이 이벤트 처리기에 대 한 코드를 추가 하는 커서에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-264">The cursor is positioned to added code for this event handler.</span></span>

    > [!NOTE] 
    > 
    > <span data-ttu-id="ec560-265">에 컨트롤을 두 번 클릭 하면 **디자인** 보기는 이벤트 처리기를 만들 수는 몇 가지 방법 중 하나일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-265">Double-clicking a control in **Design** view is just one of several ways you can create event handlers.</span></span>
3. <span data-ttu-id="ec560-266">내에서 **Button1\_클릭** 이벤트 처리기, 형식 **Label1** 뒤에 마침표 (**.**).</span><span class="sxs-lookup"><span data-stu-id="ec560-266">Inside the **Button1\_Click** event handler, type **Label1** followed by a period (**.**).</span></span>

    <span data-ttu-id="ec560-267">뒤에 마침표를 입력할 경우는 **ID** 레이블 (**Label1**), Visual Studio에 대 한 사용 가능한 구성원 목록이 표시 됩니다는 [레이블](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) 다음에 표시 된 대로 제어 그림입니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-267">When you type the period after the **ID** of the label (**Label1**), Visual Studio displays a list of available members for the [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) control, as shown in the following illustration.</span></span> <span data-ttu-id="ec560-268">멤버 속성에 일반적으로, 메서드 또는 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-268">A member commonly a property, method, or event.</span></span>

    <span data-ttu-id="ec560-269">![코드 보기의 IntelliSense](creating-a-basic-web-forms-page/_static/image12.png "코드 보기의 IntelliSense")</span><span class="sxs-lookup"><span data-stu-id="ec560-269">![IntelliSense in Code view](creating-a-basic-web-forms-page/_static/image12.png "IntelliSense in Code view")</span></span>
4. <span data-ttu-id="ec560-270">완료 된 **클릭** 다음 코드 예제와 같이 표시 되도록 단추에 대 한 이벤트 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-270">Finish the **Click** event handler for the button so that it reads as shown in the following code example.</span></span>

    [!code-csharp[Main](creating-a-basic-web-forms-page/samples/sample1.cs?highlight=3)]

    [!code-vb[Main](creating-a-basic-web-forms-page/samples/sample2.vb?highlight=2)]
5. <span data-ttu-id="ec560-271">보기로 다시 전환는 **소스** 마우스 오른쪽 단추로 클릭 하 여 HTML 태그의 보기 *FirstWebPage.aspx* 에 **솔루션 탐색기** 선택 하 고 **보기 태그**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-271">Switch back to viewing the **Source** view of your HTML markup by right-clicking *FirstWebPage.aspx* in the **Solution Explorer** and selecting **View Markup**.</span></span>
6. <span data-ttu-id="ec560-272">스크롤하여는  **&lt;p: Button&gt;**  요소입니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-272">Scroll to the **&lt;asp:Button&gt;** element.</span></span> <span data-ttu-id="ec560-273">**&lt;p: Button&gt;**  이제 특성이 요소 **onclick =&quot;Button1\_클릭&quot;**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-273">Note that the **&lt;asp:Button&gt;** element now has the attribute **onclick=&quot;Button1\_Click&quot;**.</span></span>

    <span data-ttu-id="ec560-274">이 특성 단추의 바인딩합니다 [클릭](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) 이전 단계에서 코딩 된 처리기 메서드를 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-274">This attribute binds the button's [Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) event to the handler method you coded in the previous step.</span></span>

    <span data-ttu-id="ec560-275">이벤트 처리기 메서드 이름에는 제한이 있습니다. 표시 되는 이름에는 Visual Studio에서 만든 기본 이름이입니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-275">Event handler methods can have any name; the name you see is the default name created by Visual Studio.</span></span> <span data-ttu-id="ec560-276">중요 한 점은 이름을 사용 하는 **OnClick** html에서 특성 코드 숨김에 정의 된 메서드의 이름과 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-276">The important point is that the name used for the **OnClick** attribute in the HTML must match the name of a method defined in the code-behind.</span></span>


### <a name="running-the-page"></a><span data-ttu-id="ec560-277">페이지를 실행 하면</span><span class="sxs-lookup"><span data-stu-id="ec560-277">Running the Page</span></span>


<span data-ttu-id="ec560-278">이제 페이지에서 서버 컨트롤을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-278">You can now test the server controls on the page.</span></span>

### <a name="to-run-the-page"></a><span data-ttu-id="ec560-279">페이지를 실행 하려면</span><span class="sxs-lookup"><span data-stu-id="ec560-279">To run the page</span></span>


1. <span data-ttu-id="ec560-280">키를 눌러 **CTRL + f 5** 브라우저에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-280">Press **CTRL+F5** to run the page in the browser.</span></span> <span data-ttu-id="ec560-281">오류가 발생 하는 경우 위의 단계를 다시 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-281">If an error occurs, recheck the steps above.</span></span>
2. <span data-ttu-id="ec560-282">텍스트 상자에 이름을 입력 하 고 클릭 하 고 **표시 이름** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-282">Enter a name into the text box and click the **Display Name** button.</span></span>

    <span data-ttu-id="ec560-283">입력 한 이름이 표시 됩니다는 [레이블](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-283">The name you entered is displayed in the [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) control.</span></span> <span data-ttu-id="ec560-284">참고 단추를 클릭할 때 페이지는 웹 서버에 게시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-284">Note that when you click the button, the page is posted to the Web server.</span></span> <span data-ttu-id="ec560-285">그런 다음 ASP.NET 페이지를 다시 만듭니다, 코드를 실행 (이 경우는 [단추](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) 컨트롤의 [클릭](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) 이벤트 처리기가 실행), 한 다음 새 페이지를 브라우저에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-285">ASP.NET then recreates the page, runs your code (in this case, the [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control's [Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) event handler runs), and then sends the new page to the browser.</span></span> <span data-ttu-id="ec560-286">브라우저에서 상태 표시줄을 시청 하는 경우에 페이지는 라운드트립이 수행 웹 서버에 단추를 클릭할 때마다 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-286">If you watch the status bar in the browser, you can see that the page is making a round trip to the Web server each time you click the button.</span></span>
3. <span data-ttu-id="ec560-287">브라우저에서 페이지를 마우스 오른쪽 단추로 클릭 하 고 선택 하 여 실행 중인 페이지의 소스를 보려면 **소스 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-287">In the browser, view the source of the page you are running by right-clicking on the page and selecting **View source**.</span></span>

    <span data-ttu-id="ec560-288">페이지 소스 코드에 서버 코드 없이 HTML을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-288">In the page source code, you see HTML without any server code.</span></span> <span data-ttu-id="ec560-289">특히, 표시 되지 않으면는  **&lt;asp:&gt;**  에서 작업 하는 요소 **소스** 보기.</span><span class="sxs-lookup"><span data-stu-id="ec560-289">Specifically, you do not see the **&lt;asp:&gt;** elements that you were working with in **Source** view.</span></span> <span data-ttu-id="ec560-290">페이지를 실행 하는 경우 ASP.NET 서버 컨트롤을 처리 하 고 컨트롤을 나타내는 기능을 수행 하는 페이지에 HTML 요소를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-290">When the page runs, ASP.NET processes the server controls and renders HTML elements to the page that perform the functions that represent the control.</span></span> <span data-ttu-id="ec560-291">예를 들어는  **&lt;p: Button&gt;**  컨트롤이 HTML로 렌더링 되는지  **&lt;입력 형식 =&quot;제출&quot; &gt;**  요소입니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-291">For example, the **&lt;asp:Button&gt;** control is rendered as the HTML **&lt;input type=&quot;submit&quot;&gt;** element.</span></span>
4. <span data-ttu-id="ec560-292">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-292">Close the browser.</span></span>


## <a name="working-with-additional-controls"></a><span data-ttu-id="ec560-293">추가 컨트롤 작업</span><span class="sxs-lookup"><span data-stu-id="ec560-293">Working with Additional Controls</span></span>

<a id="sectionToggle2"></a>

<span data-ttu-id="ec560-294">이 연습 부분에서는을 사용 합니다는 [달력](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) 컨트롤을 한 번에 한 달의 날짜를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-294">In this part of the walkthrough, you will work with the [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control, which displays dates a month at a time.</span></span> <span data-ttu-id="ec560-295">[달력](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) 컨트롤은 작업 중인 단추, 텍스트 상자 및 레이블을 보다 더 복잡 한 컨트롤 하 고 서버 컨트롤의 몇 가지 추가 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-295">The [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control is a more complex control than the button, text box, and label you have been working with and illustrates some further capabilities of server controls.</span></span>

<span data-ttu-id="ec560-296">이 섹션에서는 추가 됩니다 한 [System.Web.UI.WebControls.Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) 페이지를 제어 하 고 서식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-296">In this section, you will add a [System.Web.UI.WebControls.Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control to the page and format it.</span></span>

### <a name="to-add-a-calendar-control"></a><span data-ttu-id="ec560-297">달력 컨트롤을 추가 하려면</span><span class="sxs-lookup"><span data-stu-id="ec560-297">To add a Calendar control</span></span>


1. <span data-ttu-id="ec560-298">Visual Studio로 전환 **디자인** 보기.</span><span class="sxs-lookup"><span data-stu-id="ec560-298">In Visual Studio, switch to **Design** view.</span></span>
2. <span data-ttu-id="ec560-299">**표준** 의 섹션은 **도구 상자**를 끌어는 [달력](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) 컨트롤을 페이지로 아래로 끌어다 놓습니다는 **div** 요소는 다른 컨트롤을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-299">From the **Standard** section of the **Toolbox**, drag a [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control onto the page and drop it below the **div** element that contains the other controls.</span></span>

    <span data-ttu-id="ec560-300">달력의 스마트 태그 패널이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-300">The calendar's smart tag panel is displayed.</span></span> <span data-ttu-id="ec560-301">패널에는 쉽게 선택된 된 컨트롤에 대 한 가장 일반적인 작업을 수행할 수 있는 명령이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-301">The panel displays commands that make it easy for you to perform the most common tasks for the selected control.</span></span> <span data-ttu-id="ec560-302">다음 그림에서는 [달력](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) 에서 렌더링 된 제어 **디자인** 보기.</span><span class="sxs-lookup"><span data-stu-id="ec560-302">The following illustration shows the [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control as rendered in **Design** view.</span></span>

    <span data-ttu-id="ec560-303">![디자인 뷰에서 컨트롤 달력](creating-a-basic-web-forms-page/_static/image13.png "디자인 뷰에서 컨트롤 달력")</span><span class="sxs-lookup"><span data-stu-id="ec560-303">![Calendar control in Design view](creating-a-basic-web-forms-page/_static/image13.png "Calendar control in Design view")</span></span>
3. <span data-ttu-id="ec560-304">스마트 태그 패널에서 선택 **자동 서식**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-304">In the smart tag panel, choose **Auto Format**.</span></span>

    <span data-ttu-id="ec560-305">**자동 서식** 달력에 대 한 서식 구성표를 선택할 수 있는 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-305">The **Auto Format** dialog box is displayed, which allows you to select a formatting scheme for the calendar.</span></span> <span data-ttu-id="ec560-306">다음 그림에서는 **자동 서식** 에 대 한 대화 상자는 [달력](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-306">The following illustration shows the **Auto Format** dialog box for the [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control.</span></span>

    <span data-ttu-id="ec560-307">![자동 서식 대화 상자 (Calendar 컨트롤)](creating-a-basic-web-forms-page/_static/image14.png "자동 서식 대화 상자 (Calendar 컨트롤)")</span><span class="sxs-lookup"><span data-stu-id="ec560-307">![Auto Format dialog box (Calendar control)](creating-a-basic-web-forms-page/_static/image14.png "Auto Format dialog box (Calendar control)")</span></span>
4. <span data-ttu-id="ec560-308">**구성표 선택** 목록에서 선택 **간단한** 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-308">From the **Select a scheme** list, select **Simple** and then click **OK**.</span></span>
5. <span data-ttu-id="ec560-309">로 전환 **소스** 보기.</span><span class="sxs-lookup"><span data-stu-id="ec560-309">Switch to **Source** view.</span></span>

    <span data-ttu-id="ec560-310">볼 수는  **&lt;asp: 달력&gt;**  요소입니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-310">You can see the **&lt;asp:Calendar&gt;** element.</span></span> <span data-ttu-id="ec560-311">이 요소는 요소 앞에서 만든 단순 컨트롤에 대 한 보다 훨씬 깁니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-311">This element is much longer than the elements for the simple controls you created earlier.</span></span> <span data-ttu-id="ec560-312">도 하위 요소와 같은  **&lt;WeekEndDayStyle&gt;**, 있으며 다양 한 서식 설정을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-312">It also includes subelements, such as **&lt;WeekEndDayStyle&gt;**, which represent various formatting settings.</span></span> <span data-ttu-id="ec560-313">다음 그림에서는 [달력](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) 제어 **소스** 보기.</span><span class="sxs-lookup"><span data-stu-id="ec560-313">The following illustration shows the [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control in **Source** view.</span></span> <span data-ttu-id="ec560-314">(에 표시 되는 실제 태그 **소스** 뷰 그림에서 약간 달라질 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="ec560-314">(The exact markup that you see in **Source** view might differ slightly from the illustration.)</span></span>

    <span data-ttu-id="ec560-315">![소스 뷰에서 컨트롤 달력](creating-a-basic-web-forms-page/_static/image15.png "소스 뷰에서 컨트롤 달력")</span><span class="sxs-lookup"><span data-stu-id="ec560-315">![Calendar control in Source view](creating-a-basic-web-forms-page/_static/image15.png "Calendar control in Source view")</span></span>


### <a name="programming-the-calendar-control"></a><span data-ttu-id="ec560-316">Calendar 컨트롤 프로그래밍</span><span class="sxs-lookup"><span data-stu-id="ec560-316">Programming the Calendar Control</span></span>


<span data-ttu-id="ec560-317">이 섹션에서는 프로그래밍 합니다는 [달력](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) 컨트롤에 현재 선택 된 날짜를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-317">In this section, you will program the [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control to display the currently selected date.</span></span>

### <a name="to-program-the-calendar-control"></a><span data-ttu-id="ec560-318">달력 컨트롤을 프로그래밍 하려면</span><span class="sxs-lookup"><span data-stu-id="ec560-318">To program the Calendar control</span></span>


1. <span data-ttu-id="ec560-319">**디자인** 보기에서 두 번 클릭은 [달력](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-319">In **Design** view, double-click the [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control.</span></span>

    <span data-ttu-id="ec560-320">새 이벤트 처리기를 생성 하 라는 코드 숨김 파일에 표시 *FirstWebPage.aspx.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-320">A new event handler is created and displayed in the code-behind file named *FirstWebPage.aspx.cs*.</span></span>
2. <span data-ttu-id="ec560-321">완료 된 [SelectionChanged](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.selectionchanged.aspx) 이벤트 처리기를 다음 코드로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-321">Finish the [SelectionChanged](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.selectionchanged.aspx) event handler with the following code.</span></span>


    [!code-csharp[Main](creating-a-basic-web-forms-page/samples/sample3.cs?highlight=3)]


    [!code-vb[Main](creating-a-basic-web-forms-page/samples/sample4.vb?highlight=2)]

 <span data-ttu-id="ec560-322">위의 코드는 달력 컨트롤에서 선택한 날짜에 레이블 컨트롤의 텍스트를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-322">The above code sets the text of the label control to the selected date of the calendar control.</span></span>


### <a name="running-the-page"></a><span data-ttu-id="ec560-323">페이지를 실행 하면</span><span class="sxs-lookup"><span data-stu-id="ec560-323">Running the Page</span></span>


<span data-ttu-id="ec560-324">이제 달력을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-324">You can now test the calendar.</span></span>

### <a name="to-run-the-page"></a><span data-ttu-id="ec560-325">페이지를 실행 하려면</span><span class="sxs-lookup"><span data-stu-id="ec560-325">To run the page</span></span>


1. <span data-ttu-id="ec560-326">키를 눌러 **CTRL + f 5** 브라우저에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-326">Press **CTRL+F5** to run the page in the browser.</span></span>
2. <span data-ttu-id="ec560-327">달력에서 날짜를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-327">Click a date in the calendar.</span></span>

    <span data-ttu-id="ec560-328">에 클릭 한 날짜가 표시 됩니다는 [레이블](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-328">The date you clicked is displayed in the [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) control.</span></span>
3. <span data-ttu-id="ec560-329">브라우저에서 페이지에 대 한 소스 코드를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-329">In the browser, view the source code for the page.</span></span>

    <span data-ttu-id="ec560-330">[달력](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) 컨트롤이 페이지에 렌더링 된는 **테이블**, 각 날짜는 **td** 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-330">Note that the [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control has been rendered to the page as a **table**, with each day as a **td** element.</span></span>
4. <span data-ttu-id="ec560-331">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-331">Close the browser.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ec560-332">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ec560-332">Next Steps</span></span>


<a id="nextStepsToggle"></a>

<span data-ttu-id="ec560-333">이 연습에서는 Visual Studio 페이지 디자이너의 기본 기능에 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-333">This walkthrough has illustrated the basic features of the Visual Studio page designer.</span></span> <span data-ttu-id="ec560-334">만들기 및 Visual Studio에서 Web Forms 페이지를 편집 하는 방법을 이해 했으므로 다른 기능을 탐색 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-334">Now that you understand how to create and edit a Web Forms page in Visual Studio, you might want to explore other features.</span></span> <span data-ttu-id="ec560-335">예를 들어 다음을 수행 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-335">For example, you might want to do the following:</span></span>

- <span data-ttu-id="ec560-336">ASP.NET Web Forms에 대 한 자세한 단계별 자습서 시리즈를 수행 하 여 자세한 [ASP.NET 4.5 Web Forms 및 Visual Studio 2013 시작](getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-336">Learn more about ASP.NET Web Forms by following the step-by-step tutorial series [Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013](getting-started-with-aspnet-45-web-forms/introduction-and-overview.md).</span></span>
- <span data-ttu-id="ec560-337">Cascading 스타일 시트 (CSS)에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="ec560-337">Learn more about Cascading style sheets (CSS).</span></span> <span data-ttu-id="ec560-338">자세한 내용은 참조 [작업 CSS 개요](https://msdn.microsoft.com/library/bb398931.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="ec560-338">For details, see [Working with CSS Overview](https://msdn.microsoft.com/library/bb398931.aspx).</span></span>
