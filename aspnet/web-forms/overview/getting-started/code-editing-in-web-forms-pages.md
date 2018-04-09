---
uid: web-forms/overview/getting-started/code-editing-in-web-forms-pages
title: 코드를 Visual Studio 2013에서 ASP.NET Web Forms 편집 | Microsoft Docs
author: Erikre
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/03/2014
ms.topic: article
ms.assetid: 5344b74e-b888-479a-92bc-601a33bd61a2
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/getting-started/code-editing-in-web-forms-pages
msc.type: authoredcontent
ms.openlocfilehash: 79b10df04432490d6338dadb8f7ddd36192beb3e
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="code-editing-aspnet-web-forms-in-visual-studio-2013"></a><span data-ttu-id="a40c7-102">Visual Studio 2013에서 코드 편집 ASP.NET Web Forms</span><span class="sxs-lookup"><span data-stu-id="a40c7-102">Code Editing ASP.NET Web Forms in Visual Studio 2013</span></span>
====================
<span data-ttu-id="a40c7-103">으로 [Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="a40c7-103">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="a40c7-104">많은 ASP.NET Web Form 페이지에서 Visual Basic, C# 또는 다른 언어의 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-104">In many ASP.NET Web Form pages, you write code in Visual Basic, C#, or another language.</span></span> <span data-ttu-id="a40c7-105">Visual Studio에서 코드 편집기를 사용 하면 오류를 방지 하면서 코드를 빠르게 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-105">The code editor in Visual Studio can help you write code quickly while helping you avoid errors.</span></span> <span data-ttu-id="a40c7-106">또한 편집기는 수행 해야 하는 작업의 양을 줄이는 데 도움을 재사용 가능한 코드를 만들 수 있습니다 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-106">In addition, the editor provides ways for you to create reusable code to help reduce the amount of work you need to do.</span></span>

<span data-ttu-id="a40c7-107">이 연습에서는 Visual Studio code 편집기의 다양 한 기능을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-107">This walkthrough illustrates various features of the Visual Studio code editor.</span></span>

<span data-ttu-id="a40c7-108">이 연습에서는 다음 작업을 수행하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-108">During this walkthrough, you will learn how to:</span></span>

- <span data-ttu-id="a40c7-109">인라인 코딩 오류를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-109">Correct inline coding errors.</span></span>
- <span data-ttu-id="a40c7-110">코드 리팩터링을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-110">Refactor and rename code.</span></span>
- <span data-ttu-id="a40c7-111">변수 및 개체의 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-111">Rename variables and objects.</span></span>
- <span data-ttu-id="a40c7-112">코드 조각을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-112">Insert code snippets.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a40c7-113">전제 조건</span><span class="sxs-lookup"><span data-stu-id="a40c7-113">Prerequisites</span></span>


<span data-ttu-id="a40c7-114">이 연습을 완료하려면 다음 사항이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-114">In order to complete this walkthrough, you will need:</span></span>

- <span data-ttu-id="a40c7-115">[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) 또는 [Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web)합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-115">[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) or [Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span> <span data-ttu-id="a40c7-116">.NET Framework는 자동으로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-116">The .NET Framework is installed automatically.</span></span> 

    > [!NOTE] 
    > 
    > <span data-ttu-id="a40c7-117">Microsoft Visual Studio 2013 및 Microsoft Visual Studio Express 2013 for Web은 종종로 간주 Visual Studio이 자습서 시리즈 합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-117">Microsoft Visual Studio 2013 and Microsoft Visual Studio Express 2013 for Web will often be referred to as Visual Studio throughout this tutorial series.</span></span>  
    >   
    > <span data-ttu-id="a40c7-118">이 연습에서는 선택 했다고 가정 Visual Studio를 사용 하는 경우는 **웹 개발** 설정의 컬렉션 처음으로 Visual Studio를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-118">If you are using Visual Studio, this walkthrough assumes that you selected the **Web Development** collection of settings the first time that you started Visual Studio.</span></span> <span data-ttu-id="a40c7-119">자세한 내용은 참조 [하는 방법: 웹 개발 환경 설정 선택](https://msdn.microsoft.com/library/ff521558.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-119">For more information, see [How to: Select Web Development Environment Settings](https://msdn.microsoft.com/library/ff521558.aspx).</span></span>

  <span data-ttu-id="a40c7-120">Visual Studio 및 ASP.NET에 대 한 소개를 참조 하십시오. [Visual Studio 2013에서 기본 ASP.NET 4.5 Web Forms 페이지를 만드는](creating-a-basic-web-forms-page.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-120">For an introduction to Visual Studio and ASP.NET, see [Creating a basic ASP.NET 4.5 Web Forms page in Visual Studio 2013](creating-a-basic-web-forms-page.md).</span></span>   
 

## <a name="creating-a-web-application-project-and-a-page"></a><span data-ttu-id="a40c7-121">웹 응용 프로그램 프로젝트 및 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="a40c7-121">Creating a Web application project and a Page</span></span>

<a id="sectionToggle0"></a>

<span data-ttu-id="a40c7-122">이 연습 부분에서는 웹 응용 프로그램 프로젝트를 만들고 새 페이지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-122">In this part of the walkthrough, you will create a Web application project and add a new page to it.</span></span>

### <a name="to-create-a-web-application-project"></a><span data-ttu-id="a40c7-123">웹 응용 프로그램 프로젝트를 만들려면</span><span class="sxs-lookup"><span data-stu-id="a40c7-123">To create a Web application project</span></span>

1. <span data-ttu-id="a40c7-124">Microsoft Visual Studio를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-124">Open Microsoft Visual Studio.</span></span>
2. <span data-ttu-id="a40c7-125">**파일** 메뉴에서 **새 프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-125">On the **File** menu, select **New Project**.</span></span>  
    <span data-ttu-id="a40c7-126">![파일 메뉴](code-editing-in-web-forms-pages/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a40c7-126">![File Menu](code-editing-in-web-forms-pages/_static/image1.png)</span></span>

    <span data-ttu-id="a40c7-127">**새 프로젝트** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-127">The **New Project** dialog box appears.</span></span>
3. <span data-ttu-id="a40c7-128">선택 된 **템플릿**  - &gt; **Visual C#**  - &gt; **웹** 왼쪽의 템플릿 그룹.</span><span class="sxs-lookup"><span data-stu-id="a40c7-128">Select the **Templates** -&gt; **Visual C#** -&gt; **Web** templates group on the left.</span></span>
4. <span data-ttu-id="a40c7-129">선택 된 **ASP.NET 웹 응용 프로그램** 가운데 열에서 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-129">Choose the **ASP.NET Web Application** template in the center column.</span></span>
5. <span data-ttu-id="a40c7-130">프로젝트 이름을 ***BasicWebApp*** 클릭는 **확인** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-130">Name your project ***BasicWebApp*** and click the **OK** button.</span></span>   
<span data-ttu-id="a40c7-131">![새 프로젝트 대화 상자](code-editing-in-web-forms-pages/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="a40c7-131">![New Project dialog box](code-editing-in-web-forms-pages/_static/image2.png)</span></span>
6. <span data-ttu-id="a40c7-132">다음으로, 선택는 **Web Forms** 템플릿과 클릭은 **확인** 단추 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-132">Next, select the **Web Forms** template and click the **OK** button to create the project.</span></span>  
<span data-ttu-id="a40c7-133">![새 ASP.NET 프로젝트 대화 상자](code-editing-in-web-forms-pages/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="a40c7-133">![New ASP.NET Project dialog box](code-editing-in-web-forms-pages/_static/image3.png)</span></span>  

    <span data-ttu-id="a40c7-134">Visual Studio Web Forms 템플릿을 기반으로 하는 미리 작성 된 기능을 포함 하는 새 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-134">Visual Studio creates a new project that includes prebuilt functionality based on the Web Forms template.</span></span>


## <a name="creating-a-new-aspnet-web-forms-page"></a><span data-ttu-id="a40c7-135">새 ASP.NET Web Forms 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="a40c7-135">Creating a new ASP.NET Web Forms Page</span></span>


<span data-ttu-id="a40c7-136">사용 하 여 새 Web Forms 응용 프로그램을 만들 때는 **ASP.NET 웹 응용 프로그램** 프로젝트 템플릿을 Visual Studio 추가 라는 ASP.NET 페이지 (Web Forms 페이지) *Default.aspx*다른 여러 파일 외에, 및 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-136">When you create a new Web Forms application using the **ASP.NET Web Application** project template, Visual Studio adds an ASP.NET page (Web Forms page) named *Default.aspx*, as well as several other files and folders.</span></span> <span data-ttu-id="a40c7-137">사용할 수는 *Default.aspx* 웹 응용 프로그램에 대 한 홈 페이지와 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-137">You can use the *Default.aspx* page as the home page for your Web application.</span></span> <span data-ttu-id="a40c7-138">그러나이 연습에서는 만들고 새 페이지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-138">However, for this walkthrough, you will create and work with a new page.</span></span>

### <a name="to-add-a-page-to-the-web-application"></a><span data-ttu-id="a40c7-139">웹 응용 프로그램 페이지를 추가 하려면</span><span class="sxs-lookup"><span data-stu-id="a40c7-139">To add a page to the Web application</span></span>


1. <span data-ttu-id="a40c7-140">**솔루션 탐색기**, 웹 응용 프로그램 이름을 마우스 오른쪽 단추로 클릭 (응용 프로그램 이름이이 자습서에서는 **BasicWebSite**)를 클릭 하 고 **추가**  - &gt; **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-140">In **Solution Explorer**, right-click the Web application name (in this tutorial the application name is **BasicWebSite**), and then click **Add** -&gt; **New Item**.</span></span>   
<span data-ttu-id="a40c7-141">**새 항목 추가** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-141">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="a40c7-142">선택 된 **Visual C#**  - &gt; **웹** 왼쪽의 템플릿 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-142">Select the **Visual C#** -&gt; **Web** templates group on the left.</span></span> <span data-ttu-id="a40c7-143">그런 다음 선택 **Web Form** 중간에서 나열 하 고 이름을 *FirstWebPage.aspx*합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-143">Then, select **Web Form** from the middle list and name it *FirstWebPage.aspx*.</span></span>   
    <span data-ttu-id="a40c7-144">![새 항목 추가 대화 상자](code-editing-in-web-forms-pages/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="a40c7-144">![Add New Item dialog box](code-editing-in-web-forms-pages/_static/image4.png)</span></span>
3. <span data-ttu-id="a40c7-145">클릭 **추가** Web Forms 페이지 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-145">Click **Add** to add the Web Forms page to your project.</span></span>  
 <span data-ttu-id="a40c7-146">Visual Studio에 새 페이지에 만들어지고 열립니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-146">Visual Studio creates the new page and opens it.</span></span>
4. <span data-ttu-id="a40c7-147">다음으로이 새 페이지의 기본 시작 페이지로 설정.</span><span class="sxs-lookup"><span data-stu-id="a40c7-147">Next, set this new page as the default startup page.</span></span> <span data-ttu-id="a40c7-148">**솔루션 탐색기**, 명명 된 새 페이지를 마우스 오른쪽 단추로 클릭 *FirstWebPage.aspx* 선택 **시작 페이지로 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-148">In **Solution Explorer**, right-click the new page named *FirstWebPage.aspx* and select **Set As Start Page**.</span></span> <span data-ttu-id="a40c7-149">다음에 진행률을 테스트 하려면이 응용 프로그램을 실행할 때 자동으로 브라우저에서이 새 페이지를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-149">The next time you run this application to test our progress, you will automatically see this new page in the browser.</span></span>


## <a name="correcting-inline-coding-errors"></a><span data-ttu-id="a40c7-150">인라인 코딩 오류를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-150">Correcting Inline Coding Errors</span></span>


<span data-ttu-id="a40c7-151">Visual Studio의 코드 편집기를 사용 하면 코드를 작성 하 고 오류를 변경한 경우 코드 편집기를 사용 하면 오류를 수정 하려면 오류를 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-151">The code editor in Visual Studio helps you to avoid errors as you write code, and if you have made an error, the code editor helps you to correct the error.</span></span> <span data-ttu-id="a40c7-152">이 연습 부분에서는 편집기의 오류 수정 기능을 설명 하는 코드 줄을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-152">In this part of the walkthrough, you will write a line of code that illustrate the error correction features in the editor.</span></span>

### <a name="to-correct-simple-coding-errors-in-visual-studio"></a><span data-ttu-id="a40c7-153">Visual Studio에서 간단한 코드 오류를 해결 하려면</span><span class="sxs-lookup"><span data-stu-id="a40c7-153">To correct simple coding errors in Visual Studio</span></span>


1. <span data-ttu-id="a40c7-154">**디자인** 보기에 대 한 처리기를 만들 빈 페이지를 두 번 클릭은 **부하** 페이지에 대 한 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-154">In **Design** view, double-click the blank page to create a handler for the **Load** event for the page.</span></span>   
   <span data-ttu-id="a40c7-155">일부 코드를 작성 하는 장소로 이벤트 처리기를 사용 하는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-155">You are using the event handler only as a place to write some code.</span></span>
2. <span data-ttu-id="a40c7-156">처리기를 내는 오류 메시지와 키를 눌러를 포함 하는 다음 줄을 입력 **ENTER**:</span><span class="sxs-lookup"><span data-stu-id="a40c7-156">Inside the handler, type the following line that contains an error and press **ENTER**:</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample1.cs)]

   <span data-ttu-id="a40c7-157">누를 때 **ENTER**, 코드 편집기 놓이는 녹색 또는 빨간색 밑줄 (일반적으로 호출 &quot;구불구불한&quot; 줄)에서 문제가 있는 코드의 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-157">When you press **ENTER**, the code editor places green and red underlines (commonly call &quot;squiggly&quot; lines) under areas of the code that have issues.</span></span> <span data-ttu-id="a40c7-158">녹색 밑줄 경고를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-158">A green underline indicates a warning.</span></span> <span data-ttu-id="a40c7-159">빨간색 밑줄 수정 해야 하는 오류를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-159">A red underline indicates an error that you must fix.</span></span> 

    <span data-ttu-id="a40c7-160">위로 마우스 포인터를 가져가면 `myStr` 경고에 대 한를 알려 주는 도구 설명이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-160">Hold the mouse pointer over `myStr` to see a tooltip that tells you about the warning.</span></span> <span data-ttu-id="a40c7-161">또한 오류 메시지가 빨간색 밑줄 위로 마우스 포인터를 보유 합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-161">Also, hold your mouse pointer over the red underline to see the error message.</span></span>

    <span data-ttu-id="a40c7-162">다음 이미지는 밑줄을 사용 하 여 코드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-162">The following image shows the code with the underlines.</span></span>

    <span data-ttu-id="a40c7-163">![디자인 뷰의 환영 텍스트](code-editing-in-web-forms-pages/_static/image5.png "디자인 뷰의 환영 텍스트")</span><span class="sxs-lookup"><span data-stu-id="a40c7-163">![Welcome text in Design view](code-editing-in-web-forms-pages/_static/image5.png "Welcome text in Design view")</span></span>  
   <span data-ttu-id="a40c7-164">세미콜론을 추가 하 여 오류를 수정 해야 `;` 줄의 끝에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-164">The error must be fixed by adding a semicolon `;` to the end of the line.</span></span> <span data-ttu-id="a40c7-165">경고 단순히 알리는 사용 하지 않은 `myStr` 아직 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-165">The warning simply notifies you that you haven't used the `myStr` variable yet.</span></span>  

    > [!NOTE] 
    > 
    > <span data-ttu-id="a40c7-166">Visual Studio에서 설정을 선택 하 여 서식을 현재 코드를 볼 **도구**  - &gt; **옵션**  - &gt; **글꼴 및 색**합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-166">You view your current code formatting settings in Visual Studio by selecting **Tools** -&gt; **Options** -&gt; **Fonts and Colors**.</span></span>


## <a name="refactoring-and-renaming"></a><span data-ttu-id="a40c7-167">리팩터링 및 이름 바꾸기</span><span class="sxs-lookup"><span data-stu-id="a40c7-167">Refactoring and Renaming</span></span>

<span data-ttu-id="a40c7-168">리팩터링 쉽게 이해 하 고 해당 기능을 유지 하면서 유지 하기 위해 코드를 재구성을 포함 하는 소프트웨어 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-168">Refactoring is a software methodology that involves restructuring your code to make it easier to understand and to maintain, while preserving its functionality.</span></span> <span data-ttu-id="a40c7-169">간단한 예는 데이터베이스에서 데이터를 가져오는 이벤트 처리기에서 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-169">A simple example might be that you write code in an event handler to get data from a database.</span></span> <span data-ttu-id="a40c7-170">페이지를 개발할 때 여러 다른 처리기의 데이터에 액세스 할 경우 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-170">As you develop your page, you discover that you need to access the data from several different handlers.</span></span> <span data-ttu-id="a40c7-171">따라서 페이지에서 데이터 액세스 메서드를 만들어 처리기에서 메서드 호출을 삽입 하 여 페이지의 코드를 리팩터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-171">Therefore, you refactor the page's code by creating a data-access method in the page and inserting calls to the method in the handlers.</span></span>

<span data-ttu-id="a40c7-172">코드 편집기에는 다양 한 리팩터링 작업을 수행할 수 있도록 도구가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-172">The code editor includes tools to help you perform various refactoring tasks.</span></span> <span data-ttu-id="a40c7-173">이 연습에서는 두 가지 리팩터링 기법을 사용 합니다: 변수 이름을 바꾸고 메서드 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-173">In this walkthrough, you will work with two refactoring techniques: renaming variables and extracting methods.</span></span> <span data-ttu-id="a40c7-174">리팩터링 있습니다 필드 캡슐화, 메서드 매개 변수를 지역 변수 승격 및 메서드 매개 변수를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-174">Other refactoring options include encapsulating fields, promoting local variables to method parameters, and managing method parameters.</span></span> <span data-ttu-id="a40c7-175">이러한 리팩터링 옵션의 가용성을 코드에서의 위치에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-175">The availability of these refactoring options depends on the location in the code.</span></span>

### <a name="refactoring-code"></a><span data-ttu-id="a40c7-176">코드 리팩터링</span><span class="sxs-lookup"><span data-stu-id="a40c7-176">Refactoring Code</span></span>

<span data-ttu-id="a40c7-177">일반적인 리팩터링 시나리오 만들거나 추출 하는 메서드와 같은 다른 멤버 내에 있는 코드에서 메서드를 합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-177">A common refactoring scenario is to create (extract) a method from code that is inside another member, such as a method.</span></span> <span data-ttu-id="a40c7-178">이 원래 멤버의 크기를 줄이는 고 추출 된 코드 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-178">This reduces the size of the original member and makes the extracted code reusable.</span></span>

<span data-ttu-id="a40c7-179">이 연습 부분에서는 몇 가지 간단한 코드를 작성 한 다음 여기에서 한 메서드를 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-179">In this part of the walkthrough, you will write some simple code, and then extract a method from it.</span></span> <span data-ttu-id="a40c7-180">리팩터링 대해서는 C#, C# 프로그래밍 언어로 사용 하는 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-180">Refactoring is supported for C#, so you will create a page that uses C# as its programming language.</span></span>

### <a name="to-extract-a-method-in-a-c-page"></a><span data-ttu-id="a40c7-181">C# 페이지의 메서드를 추출 하려면</span><span class="sxs-lookup"><span data-stu-id="a40c7-181">To extract a method in a C# page</span></span>

1. <span data-ttu-id="a40c7-182">로 전환 **디자인** 보기.</span><span class="sxs-lookup"><span data-stu-id="a40c7-182">Switch to **Design** view.</span></span>
2. <span data-ttu-id="a40c7-183">에 **도구 상자**에서 **표준** 탭을 끌어는 [단추](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) 컨트롤을 페이지로 끌어옵니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-183">In the **Toolbox**, from the **Standard** tab, drag a [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control onto the page.</span></span>
3. <span data-ttu-id="a40c7-184">두 번 클릭은 **단추** 에 대 한 처리기를 만들 컨트롤을 해당 [클릭](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) 이벤트를 다음 강조 표시 된 코드를 추가:</span><span class="sxs-lookup"><span data-stu-id="a40c7-184">Double-click the **Button** control to create a handler for its [Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) event, and then add the following highlighted code:</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample2.cs?highlight=3-16)]

   <span data-ttu-id="a40c7-185">코드는 만듭니다는 **ArrayList** 개체 값을 사용 하 여이 로드 하는 루프를 사용 하 여 및 다음 다른 루프를 사용 하 여의 내용을 표시 하는 **ArrayList** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-185">The code creates an **ArrayList** object, uses a loop to load it with values, and then uses another loop to display the contents of the **ArrayList** object.</span></span>
4. <span data-ttu-id="a40c7-186">키를 눌러 **CTRL + f 5** 페이지를 실행 한 다음 클릭는 **단추** 되도록 다음과 같은 출력을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="a40c7-186">Press **CTRL+F5** to run the page, and then click the **button** to make sure that you see the following output:</span></span>   

    [!code-html[Main](code-editing-in-web-forms-pages/samples/sample3.html)]
5. <span data-ttu-id="a40c7-187">코드 편집기로 돌아가서 다음 이벤트 처리기에 다음 줄을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-187">Return to the code editor, and then select the following lines in the event handler.</span></span>   

    [!code-html[Main](code-editing-in-web-forms-pages/samples/sample4.html)]
6. <span data-ttu-id="a40c7-188">선택 영역을 마우스 오른쪽 단추로 클릭 합니다. **리팩터링**를 선택한 후 **메서드 추출**합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-188">Right-click the selection, click **Refactor**, and then choose **Extract Method**.</span></span> 

    <span data-ttu-id="a40c7-189">**메서드 추출** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-189">The **Extract Method** dialog box appears.</span></span>
7. <span data-ttu-id="a40c7-190">에 **새 메서드 이름** 상자에 입력 합니다 **DisplayArray**, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-190">In the **New Method Name** box, type **DisplayArray**, and then click **OK**.</span></span> 

    <span data-ttu-id="a40c7-191">코드 편집기에는 명명 된 새 메서드가 작성 `DisplayArray`에서 새 메서드를 호출 하 고는 **클릭** 원래 루프 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-191">The code editor creates a new method named `DisplayArray`, and puts a call to the new method in the **Click** handler where the loop was originally.</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample5.cs?highlight=12)]
8. <span data-ttu-id="a40c7-192">키를 눌러 **CTRL + f 5** 페이지를 다시 실행 하 고 클릭 하 고 **단추**합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-192">Press **CTRL+F5** to run the page again, and click the **button**.</span></span>

    <span data-ttu-id="a40c7-193">페이지 작동 하기 전과 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-193">The page functions the same as it did before.</span></span> <span data-ttu-id="a40c7-194">`DisplayArray` 메서드 어디에서 나 호출 될 수 있습니다 page 클래스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-194">The `DisplayArray` method can now be call from anywhere in the page class.</span></span>

## <a name="renaming-variables"></a><span data-ttu-id="a40c7-195">변수 이름 바꾸기</span><span class="sxs-lookup"><span data-stu-id="a40c7-195">Renaming Variables</span></span>

<span data-ttu-id="a40c7-196">변수 뿐 아니라 개체를 사용 하는 경우에 코드에서 이미 참조 이름으로 변경는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-196">When you work with variables, as well as objects, you might want to rename them after they are already referenced in your code.</span></span> <span data-ttu-id="a40c7-197">그러나 변수 및 개체 이름을 바꾸는 코드 참조 중 하나의 이름을 바꾸지 되 면 중단를 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-197">However, renaming variables and objects can cause the code to break if you miss renaming one of the references.</span></span> <span data-ttu-id="a40c7-198">따라서 리팩터링 옵션을 사용 하 여 이름을 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-198">Therefore, you can use refactoring to perform the renaming.</span></span>

### <a name="to-use-refactoring-to-rename-a-variable"></a><span data-ttu-id="a40c7-199">리팩터링을 사용 하는 변수 이름을 바꾸려면</span><span class="sxs-lookup"><span data-stu-id="a40c7-199">To use refactoring to rename a variable</span></span>


1. <span data-ttu-id="a40c7-200">에 **클릭** 이벤트 처리기를 다음 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-200">In the **Click** event handler, locate the following line:</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample6.cs)]
2. <span data-ttu-id="a40c7-201">변수 이름을 마우스 오른쪽 단추로 클릭 `alist`, 선택 **리팩터링**를 선택한 후 **이름 바꾸기**합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-201">Right-click the variable name `alist`, choose **Refactor**, and then choose **Rename**.</span></span>

    <span data-ttu-id="a40c7-202">**이름 바꾸기** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-202">The **Rename** dialog box appears.</span></span>
3. <span data-ttu-id="a40c7-203">에 **새 이름을** 상자에 입력 합니다 **ArrayList1** 있는지 확인 하 고는 **참조 변경 내용 미리 보기** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-203">In the **New name** box, type **ArrayList1** and make sure the **Preview reference changes** checkbox has been selected.</span></span> <span data-ttu-id="a40c7-204">그런 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-204">Then click **OK**.</span></span>

    <span data-ttu-id="a40c7-205">**변경 내용 미리 보기** 대화 상자가 나타나고 바꾸려는 변수에 대 한 모든 참조를 포함 하는 트리를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-205">The **Preview Changes** dialog box appears, and displays a tree that contains all references to the variable that you are renaming.</span></span>
4. <span data-ttu-id="a40c7-206">클릭 **적용** 를 닫으려면는 **변경 내용 미리 보기** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="a40c7-206">Click **Apply** to close the **Preview Changes** dialog box.</span></span>

    <span data-ttu-id="a40c7-207">선택한 인스턴스를 구체적으로 참조 하는 변수 이름이 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-207">The variables that refer specifically to the instance that you selected are renamed.</span></span> <span data-ttu-id="a40c7-208">그러나 하는 변수 `alist` 다음 줄에서 바뀌지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-208">Note, however, that the variable `alist` in the following line is not renamed.</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample7.cs)]

    <span data-ttu-id="a40c7-209">변수 `alist` 이 줄에서 변경 하지 않으면 같은 값으로 변수를 표시 하지 않기 때문에 `alist` 이름을 바꾼 합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-209">The variable `alist` in this line is not renamed because it does not represent the same value as the variable `alist` that you renamed.</span></span> <span data-ttu-id="a40c7-210">변수 `alist` 에 `DisplayArray` 는 해당 메서드에 대 한 지역 변수를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-210">The variable `alist` in the `DisplayArray` declaration is a local variable for that method.</span></span> <span data-ttu-id="a40c7-211">리팩터링을 사용 하 여 변수를 바꾸려면 단순히; 편집기에서 찾기 및 바꾸기 작업을 수행할 때 보다 다른는 들 작동 하는 변수의 의미를 사용 하 여 리팩터링 이름 바꾸기 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-211">This illustrates that using refactoring to rename variables is different than simply performing a find-and-replace action in the editor; refactoring renames variables with knowledge of the semantics of the variable that it is working with.</span></span>


## <a name="inserting-snippets"></a><span data-ttu-id="a40c7-212">조각 삽입</span><span class="sxs-lookup"><span data-stu-id="a40c7-212">Inserting Snippets</span></span>

<span data-ttu-id="a40c7-213">Web Forms 개발자가 자주 수행 해야 하는 많은 코딩 작업 때문에 코드 편집기의 코드 조각, 또는 미리 작성 된 코드 블록을 라이브러리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-213">Because there are many coding tasks that Web Forms developers frequently need to perform, the code editor provides a library of snippets, or blocks of prewritten code.</span></span> <span data-ttu-id="a40c7-214">페이지에 이러한 조각을 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-214">You can insert these snippets into your page.</span></span>

<span data-ttu-id="a40c7-215">Visual Studio에서 사용 하는 각 언어에 코드 조각을 삽입 하는 방법에 약간의 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-215">Each language that you use in Visual Studio has slight differences in the way you insert code snippets.</span></span> <span data-ttu-id="a40c7-216">코드 조각을 삽입 하는 방법에 대 한 정보를 참조 하십시오. [Visual Basic IntelliSense 코드 조각](https://msdn.microsoft.com/library/18yz4be4.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-216">For information about inserting snippets, see [Visual Basic IntelliSense Code Snippets](https://msdn.microsoft.com/library/18yz4be4.aspx).</span></span> <span data-ttu-id="a40c7-217">코드 조각을 Visual C#에서 삽입 하는 방법에 대 한 정보를 참조 하십시오. [Visual C# 코드 조각](https://msdn.microsoft.com/library/z41h7fat.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-217">For information about inserting snippets in Visual C#, see [Visual C# Code Snippets](https://msdn.microsoft.com/library/z41h7fat.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a40c7-218">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a40c7-218">Next Steps</span></span>

<span data-ttu-id="a40c7-219">이 연습에서는 코드에서 오류를 수정, 리팩터링 코드, 변수, 이름 바꾸기 및 코드에 코드 조각을 삽입에 대 한 Visual Studio 2010 코드 편집기의 기본 기능에 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-219">This walkthrough has illustrated the basic features of the Visual Studio 2010 code editor for correcting errors in your code, refactoring code, renaming variables, and inserting code snippets into your code.</span></span> <span data-ttu-id="a40c7-220">편집기에서 추가 기능 응용 프로그램을 쉽고 빠르게 개발을 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-220">Additional features in the editor can make application development fast and easy.</span></span> <span data-ttu-id="a40c7-221">예를 들어, 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-221">For example, you might want to:</span></span>

- <span data-ttu-id="a40c7-222">IntelliSense 옵션 수정, 코드 조각, 관리 및 코드 조각을 온라인 검색 같은 IntelliSense의 기능에 대해 알아보십시오.</span><span class="sxs-lookup"><span data-stu-id="a40c7-222">Learn more about the features of IntelliSense, such as modifying IntelliSense options, managing code snippets, and searching for code snippets online.</span></span> <span data-ttu-id="a40c7-223">자세한 내용은 [IntelliSense 사용](https://msdn.microsoft.com/library/hcw1s69b.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a40c7-223">For more information, see [Using IntelliSense](https://msdn.microsoft.com/library/hcw1s69b.aspx).</span></span>
- <span data-ttu-id="a40c7-224">사용자 고유의 코드 조각을 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-224">Learn how to create your own code snippets.</span></span> <span data-ttu-id="a40c7-225">자세한 내용은 참조 [만들기 및 사용 하 여 IntelliSense 코드 조각](https://msdn.microsoft.com/library/ms165392.aspx)</span><span class="sxs-lookup"><span data-stu-id="a40c7-225">For more information, see [Creating and Using IntelliSense Code Snippets](https://msdn.microsoft.com/library/ms165392.aspx)</span></span>
- <span data-ttu-id="a40c7-226">IntelliSense 코드 조각, 코드 조각은 사용자 지정 하 고 문제 해결 등의 Visual Basic 관련 기능에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="a40c7-226">Learn more about the Visual Basic-specific features of IntelliSense code snippets, such as customizing the snippets and troubleshooting.</span></span> <span data-ttu-id="a40c7-227">자세한 내용은 참조 [Visual Basic IntelliSense 코드 조각](https://msdn.microsoft.com/library/18yz4be4.aspx)</span><span class="sxs-lookup"><span data-stu-id="a40c7-227">For more information, see [Visual Basic IntelliSense Code Snippets](https://msdn.microsoft.com/library/18yz4be4.aspx)</span></span>
- <span data-ttu-id="a40c7-228">C#에 대 한 자세한-리팩터링 및 코드 조각 같은 IntelliSense의 특정 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-228">Learn more about the C#-specific features of IntelliSense, such as refactoring and code snippets.</span></span> <span data-ttu-id="a40c7-229">자세한 내용은 참조 [Visual C# IntelliSense](https://msdn.microsoft.com/library/43f44291.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="a40c7-229">For more information, see [Visual C# IntelliSense](https://msdn.microsoft.com/library/43f44291.aspx).</span></span>
