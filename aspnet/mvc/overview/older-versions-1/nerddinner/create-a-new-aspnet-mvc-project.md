---
uid: mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
title: 새 ASP.NET MVC 프로젝트 만들기 | Microsoft Docs
author: microsoft
description: 1 단계를에서 기본 NerdDinner 응용 프로그램 구조를 배치 하는 방법을 보여 줍니다.
ms.author: aspnetcontent
ms.date: 07/27/2010
ms.assetid: 7e0e9928-8fdc-4b74-9882-55fac0976628
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
msc.type: authoredcontent
ms.openlocfilehash: 88ef850503725cc57c92a11952729b4bd2205a69
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37835096"
---
<a name="create-a-new-aspnet-mvc-project"></a><span data-ttu-id="c9aa0-103">새 ASP.NET MVC 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="c9aa0-103">Create a New ASP.NET MVC Project</span></span>
====================
<span data-ttu-id="c9aa0-104">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="c9aa0-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="c9aa0-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="c9aa0-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="c9aa0-106">이 무료의 1 단계 ["NerdDinner" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 는 안내를 통한 작은 빌드 하지만 ASP.NET MVC 1을 사용 하 여 웹 응용 프로그램을 완료 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="c9aa0-106">This is step 1 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="c9aa0-107">1 단계를에서 기본 NerdDinner 응용 프로그램 구조를 배치 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c9aa0-107">Step 1 shows you how to put the basic NerdDinner application structure in place.</span></span>
> 
> <span data-ttu-id="c9aa0-108">ASP.NET MVC 3을 사용 하는 경우 수행 하는 것이 좋습니다 합니다 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 하거나 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="c9aa0-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-step-1-file-gtnew-project"></a><span data-ttu-id="c9aa0-109">NerdDinner 1 단계: 파일-&gt;새 프로젝트</span><span class="sxs-lookup"><span data-stu-id="c9aa0-109">NerdDinner Step 1: File-&gt;New Project</span></span>

<span data-ttu-id="c9aa0-110">NerdDinner 응용 프로그램을 선택 하 여 먼저 합니다 **파일-&gt;새 프로젝트** Visual Studio 2008 또는 무료 Visual Web Developer 2008 Express에서 메뉴 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="c9aa0-110">We'll begin our NerdDinner application by selecting the **File-&gt;New Project** menu item within either Visual Studio 2008 or the free Visual Web Developer 2008 Express.</span></span>

<span data-ttu-id="c9aa0-111">"새 프로젝트" 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9aa0-111">This will bring up the "New Project" dialog.</span></span> <span data-ttu-id="c9aa0-112">새 ASP.NET MVC 응용 프로그램을 만들려면 대화 상자의 왼쪽에서 "웹" 노드를 선택 하 고 선택한 다음 오른쪽의 "ASP.NET MVC 웹 응용 프로그램" 프로젝트 템플릿의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9aa0-112">To create a new ASP.NET MVC application, we'll select the "Web" node on the left-hand side of the dialog and then choose the "ASP.NET MVC Web Application" project template on the right:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image1.png)

<span data-ttu-id="c9aa0-113">*중요: 다운로드 하 고 ASP.NET MVC-그렇지 않은 경우 새 프로젝트 대화 상자에 나타나지 설치 되어 있는지 확인 합니다. V2의 사용할 수는 [Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx) 아직 설치 하지 않은 경우 (ASP.NET MVC는 내에서 사용할 수는 "웹 플랫폼-&gt;프레임 워크 및 런타임" 섹션).*</span><span class="sxs-lookup"><span data-stu-id="c9aa0-113">*Important: Make sure you've downloaded and installed ASP.NET MVC - otherwise it won't show up in the New Project dialog. You can use V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) if you haven't installed it yet (ASP.NET MVC is available within the "Web Platform-&gt;Frameworks and Runtimes" section).*</span></span>

<span data-ttu-id="c9aa0-114">에서는 하겠습니다 "NerdDinner"를 만들고 만들 "확인" 단추를 클릭 한 다음 새 프로젝트의 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9aa0-114">We'll name the new project we are going to create "NerdDinner" and then click the "ok" button to create it.</span></span>

<span data-ttu-id="c9aa0-115">"확인"를 클릭 하는 경우 Visual Studio는 필요에 따라도 새 응용 프로그램에 대 한 단위 테스트 프로젝트를 만들 요청 추가 대화 상자를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9aa0-115">When we click "ok" Visual Studio will bring up an additional dialog that prompts us to optionally create a unit test project for the new application as well.</span></span> <span data-ttu-id="c9aa0-116">이 단위 테스트 프로젝트 기능 및 응용 프로그램의 동작을 확인 하는 자동화 된 테스트를 만들 수 있습니다 (다루게 무언가 어떻게 할 일이이 자습서의 뒷부분에서).</span><span class="sxs-lookup"><span data-stu-id="c9aa0-116">This unit test project enables us to create automated tests that verify the functionality and behavior of our application (something we'll cover how to-do later in this tutorial).</span></span>

![](create-a-new-aspnet-mvc-project/_static/image2.png)

<span data-ttu-id="c9aa0-117">위 대화 상자에서 "테스트 프레임 워크" 드롭다운에서 모든 사용 가능한 ASP.NET MVC 단위 테스트 프로젝트 템플릿 컴퓨터에 설치를 사용 하 여 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="c9aa0-117">The "Test framework" dropdown in the above dialog is populated with all available ASP.NET MVC unit test project templates installed on the machine.</span></span> <span data-ttu-id="c9aa0-118">XUnit, NUnit 및 MBUnit에 버전을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9aa0-118">Versions can be downloaded for NUnit, MBUnit, and XUnit.</span></span> <span data-ttu-id="c9aa0-119">기본 제공 Visual Studio 단위 테스트 프레임 워크 에서도 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9aa0-119">The built-in Visual Studio Unit Test framework is also supported.</span></span>

<span data-ttu-id="c9aa0-120">*참고: Visual Studio 단위 테스트 프레임 워크는만 Visual Studio 2008 Professional 및 이상 버전을 사용 하 여 사용할 수 있습니다. VS 2008 Standard Edition 또는 Visual Web Developer 2008 Express를 사용 하는 경우 다운로드 하 고이 대화 상자 표시를 위해에서 ASP.NET MVC에 대 한 NUnit 이나 MBUnit XUnit 확장을 설치 해야 합니다. 모든 테스트 프레임 워크 설치 되지 않은 경우에 대화 상자가 표시 되지 않습니다.*</span><span class="sxs-lookup"><span data-stu-id="c9aa0-120">*Note: The Visual Studio Unit Test Framework is only available with Visual Studio 2008 Professional and higher versions. If you are using VS 2008 Standard Edition or Visual Web Developer 2008 Express you will need to download and install the NUnit, MBUnit or XUnit extensions for ASP.NET MVC in order for this dialog to be shown. The dialog will not display if there aren't any test frameworks installed.*</span></span>

<span data-ttu-id="c9aa0-121">을 만들어 테스트 프로젝트에 대 한 기본 "NerdDinner.Tests" 이름을 사용 하 고 "Visual Studio 단위 테스트" 프레임 워크 옵션을 사용 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c9aa0-121">We'll use the default "NerdDinner.Tests" name for the test project we create, and use the "Visual Studio Unit Test" framework option.</span></span> <span data-ttu-id="c9aa0-122">클릭 하면 "확인" 단추 Visual Studio 솔루션이 만들어집니다 한 것은 단위 테스트에 대 한 웹 응용 프로그램에 대 한 개와 두 프로젝트를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="c9aa0-122">When we click the "ok" button Visual Studio will create a solution for us with two projects in it - one for our web application and one for our unit tests:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image3.png)

### <a name="examining-the-nerddinner-directory-structure"></a><span data-ttu-id="c9aa0-123">NerdDinner 디렉터리 구조를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="c9aa0-123">Examining the NerdDinner directory structure</span></span>

<span data-ttu-id="c9aa0-124">Visual Studio를 사용 하 여 새 ASP.NET MVC 응용 프로그램을 만들 때 프로젝트에 파일 및 디렉터리의 숫자로 자동으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9aa0-124">When you create a new ASP.NET MVC application with Visual Studio, it automatically adds a number of files and directories to the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image4.png)

<span data-ttu-id="c9aa0-125">기본적으로 ASP.NET MVC 프로젝트에 6 개의 최상위 디렉터리</span><span class="sxs-lookup"><span data-stu-id="c9aa0-125">ASP.NET MVC projects by default have six top-level directories:</span></span>

| <span data-ttu-id="c9aa0-126">**디렉터리**</span><span class="sxs-lookup"><span data-stu-id="c9aa0-126">**Directory**</span></span> | <span data-ttu-id="c9aa0-127">**용도**</span><span class="sxs-lookup"><span data-stu-id="c9aa0-127">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="c9aa0-128">**/Controllers**</span><span class="sxs-lookup"><span data-stu-id="c9aa0-128">**/Controllers**</span></span> | <span data-ttu-id="c9aa0-129">URL 요청을 처리 하는 컨트롤러 클래스를 배치 하는 위치</span><span class="sxs-lookup"><span data-stu-id="c9aa0-129">Where you put Controller classes that handle URL requests</span></span> |
| <span data-ttu-id="c9aa0-130">**/Models**</span><span class="sxs-lookup"><span data-stu-id="c9aa0-130">**/Models**</span></span> | <span data-ttu-id="c9aa0-131">나타내는 데이터를 조작 하는 클래스를 배치 하는 위치</span><span class="sxs-lookup"><span data-stu-id="c9aa0-131">Where you put classes that represent and manipulate data</span></span> |
| <span data-ttu-id="c9aa0-132">**/ 뷰**</span><span class="sxs-lookup"><span data-stu-id="c9aa0-132">**/Views**</span></span> | <span data-ttu-id="c9aa0-133">렌더링 출력과 관련 된 UI 템플릿 파일을 배치 하는 위치</span><span class="sxs-lookup"><span data-stu-id="c9aa0-133">Where you put UI template files that are responsible for rendering output</span></span> |
| <span data-ttu-id="c9aa0-134">**/Scripts**</span><span class="sxs-lookup"><span data-stu-id="c9aa0-134">**/Scripts**</span></span> | <span data-ttu-id="c9aa0-135">JavaScript 라이브러리 파일 및 스크립트 (.js)을 배치 하는 위치</span><span class="sxs-lookup"><span data-stu-id="c9aa0-135">Where you put JavaScript library files and scripts (.js)</span></span> |
| <span data-ttu-id="c9aa0-136">**/Content**</span><span class="sxs-lookup"><span data-stu-id="c9aa0-136">**/Content**</span></span> | <span data-ttu-id="c9aa0-137">CSS 및 이미지 파일을 다른 비-동적/비-JavaScript 콘텐츠를 배치 하는 위치</span><span class="sxs-lookup"><span data-stu-id="c9aa0-137">Where you put CSS and image files, and other non-dynamic/non-JavaScript content</span></span> |
| <span data-ttu-id="c9aa0-138">**/ 앱\_데이터**</span><span class="sxs-lookup"><span data-stu-id="c9aa0-138">**/App\_Data**</span></span> | <span data-ttu-id="c9aa0-139">데이터 파일을 저장 하는 경우 읽기/쓰기 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9aa0-139">Where you store data files you want to read/write.</span></span> |

<span data-ttu-id="c9aa0-140">ASP.NET MVC는이 구조를 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c9aa0-140">ASP.NET MVC does not require this structure.</span></span> <span data-ttu-id="c9aa0-141">사실, 대규모 응용 프로그램에서 작업 하는 개발자는 일반적으로 분할 응용 프로그램을 보다 잘 관리할 수 있도록 여러 프로젝트에서 (예: 데이터 모델 클래스도 별도 클래스 라이브러리 프로젝트를 웹 응용 프로그램에서).</span><span class="sxs-lookup"><span data-stu-id="c9aa0-141">In fact, developers working on large applications will typically partition the application up across multiple projects to make it more manageable (for example: data model classes often go in a separate class library project from the web application).</span></span> <span data-ttu-id="c9aa0-142">그러나 기본 프로젝트 구조는 응용 프로그램 문제를 정리 되도록 사용할 수 있는 유용한 기본 디렉터리 규칙을 제공지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c9aa0-142">The default project structure, however, does provide a nice default directory convention that we can use to keep our application concerns clean.</span></span>

<span data-ttu-id="c9aa0-143">/Controllers 디렉터리 확장에서는 알는 Visual Studio – HomeController과 AccountController – 두 컨트롤러 클래스 기본적으로 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9aa0-143">When we expand the /Controllers directory we'll find that Visual Studio added two controller classes – HomeController and AccountController – by default to the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image5.png)

<span data-ttu-id="c9aa0-144">/Views 디렉터리를 확장 하는 경우 세 개의 하위 디렉터리가 – /Home, /Account /Shared – 뿐만 아니라 여러 템플릿 파일 내에 기본적으로 프로젝트에 추가 된도 알게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9aa0-144">When we expand the /Views directory, we'll find three sub-directories – /Home, /Account and /Shared – as well as several template files within them were also added to the project by default:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image6.png)

<span data-ttu-id="c9aa0-145">/Content 및 /Scripts 디렉터리를 확장 하는 경우 응용 프로그램 내에서 지 원하는 사이트의 모든 HTML 스타일을 지정 하는 데 사용 되는 Site.css 파일 뿐만 아니라 ASP.NET AJAX 및 jQuery 사용 하도록 설정할 수 있는 JavaScript 라이브러리를 찾을 수 것:</span><span class="sxs-lookup"><span data-stu-id="c9aa0-145">When we expand the /Content and /Scripts directories, we'll find a Site.css file that is used to style all HTML on the site, as well as JavaScript libraries that can enable ASP.NET AJAX and jQuery support within the application:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image7.png)

<span data-ttu-id="c9aa0-146">NerdDinner.Tests 프로젝트를 확장 하는 경우 컨트롤러 클래스에 대 한 단위 테스트를 포함 하는 두 개의 클래스를 찾을 수 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c9aa0-146">When we expand the NerdDinner.Tests project we'll find two classes that contain unit tests for our controller classes:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image8.png)

<span data-ttu-id="c9aa0-147">Visual Studio에서 추가 된 이러한 기본 파일 우리 기본 구조를 사용 하 여 작업 응용 프로그램을 제공-페이지, 계정 등록/로그인/로그 아웃 페이지와 처리 되지 않은 오류 페이지 (모든: 했으니 및 즉시 작업)에 대 한 홈 페이지를 사용 하 여 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9aa0-147">These default files added by Visual Studio provide us with a basic structure for a working application - complete with home page, about page, account login/logout/registration pages, and an unhandled error page (all wired-up and working out of the box).</span></span>

### <a name="running-the-nerddinner-application"></a><span data-ttu-id="c9aa0-148">NerdDinner 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="c9aa0-148">Running the NerdDinner Application</span></span>

<span data-ttu-id="c9aa0-149">프로젝트 중 하나를 선택 하 여 실행할 수 있습니다 합니다 **디버그-&gt;디버깅 시작** 하거나 **디버그-&gt;디버깅 하지 않고 시작** 메뉴 항목:</span><span class="sxs-lookup"><span data-stu-id="c9aa0-149">We can run the project by choosing either the **Debug-&gt;Start Debugging** or **Debug-&gt;Start Without Debugging** menu items:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image9.png)

<span data-ttu-id="c9aa0-150">이 기본 제공 ASP.NET 웹 서버에서 시작-Visual Studio와 함께 제공 되는 되며 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9aa0-150">This will launch the built-in ASP.NET Web-server that comes with Visual Studio, and run our application:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image10.png)

<span data-ttu-id="c9aa0-151">다음은 새 프로젝트의 홈 페이지 (URL: "/") 실행 시:</span><span class="sxs-lookup"><span data-stu-id="c9aa0-151">Below is the home page for our new project (URL: "/") when it runs:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image11.png)

<span data-ttu-id="c9aa0-152">"About" 탭을 클릭 하면 표시 됩니다는 페이지에 대 한 (URL: "/ Home/에 대 한"):</span><span class="sxs-lookup"><span data-stu-id="c9aa0-152">Clicking the "About" tab displays an about page (URL: "/Home/About"):</span></span>

![](create-a-new-aspnet-mvc-project/_static/image12.png)

<span data-ttu-id="c9aa0-153">로그인 페이지에는 오른쪽 상단에서 "Log On" 링크 (URL: "/ 계정/로그온")</span><span class="sxs-lookup"><span data-stu-id="c9aa0-153">Clicking the "Log On" link on the top-right takes us to a Login page (URL: "/Account/LogOn")</span></span>

![](create-a-new-aspnet-mvc-project/_static/image13.png)

<span data-ttu-id="c9aa0-154">에서는 등록 링크를 클릭할 수 있습니다 로그인 계정이 없는 경우 (URL: "/ 계정/등록") 새로 만들려면:</span><span class="sxs-lookup"><span data-stu-id="c9aa0-154">If we don't have a login account we can click the register link (URL: "/Account/Register") to create one:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image14.png)

<span data-ttu-id="c9aa0-155">에 대 한 위의 가정용을 구현 하는 코드 및 로그 아웃 등록 / 기능, 새 프로젝트를 만들 때 기본적으로 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c9aa0-155">The code to implement the above home, about, and logout/ register functionality was added by default when we created our new project.</span></span> <span data-ttu-id="c9aa0-156">이 응용 프로그램의 시작 점으로 사용 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c9aa0-156">We'll use it as the starting point of our application.</span></span>

### <a name="testing-the-nerddinner-application"></a><span data-ttu-id="c9aa0-157">NerdDinner 응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="c9aa0-157">Testing the NerdDinner Application</span></span>

<span data-ttu-id="c9aa0-158">Professional Edition 또는 더 높은 버전의 Visual Studio 2008을 사용 하는 것 테스트 IDE 지원을 Visual Studio 내에서 기본 제공 단위 테스트 프로젝트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9aa0-158">If we are using the Professional Edition or higher version of Visual Studio 2008, we can use the built-in unit testing IDE support within Visual Studio to test the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image15.png)

<span data-ttu-id="c9aa0-159">위의 옵션 중 하나를 선택 하면 IDE 내에서 "테스트 결과" 창을 엽니다 되며 기본 제공 기능을 포함 하는 새 프로젝트에 포함 된 27 단위 테스트에 통과/실패 상태를 사용 하 여 제공:</span><span class="sxs-lookup"><span data-stu-id="c9aa0-159">Choosing one of the above options will open the "Test Results" pane within the IDE and provide us with pass/fail status on the 27 unit tests included in our new project that cover the built-in functionality:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image16.png)

<span data-ttu-id="c9aa0-160">이 자습서의 뒷부분에 나오는에서는 자동화 된 테스트를 자세히 설명 하 고 구현 하는 응용 프로그램 기능을 포함 하는 추가 단위 테스트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9aa0-160">Later in this tutorial we'll talk more about automated testing and add additional unit tests that cover the application functionality we implement.</span></span>

### <a name="next-step"></a><span data-ttu-id="c9aa0-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c9aa0-161">Next Step</span></span>

<span data-ttu-id="c9aa0-162">현재 위치에서 이제 기본 응용 프로그램 구조에 답변이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9aa0-162">We've now got a basic application structure in place.</span></span> <span data-ttu-id="c9aa0-163">이제 보겠습니다 [응용 프로그램 데이터를 저장 하도록 데이터베이스를 만드는](create-a-database.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c9aa0-163">Let's now [create a database to store our application data](create-a-database.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c9aa0-164">[이전](introducing-the-nerddinner-tutorial.md)
> [다음](create-a-database.md)</span><span class="sxs-lookup"><span data-stu-id="c9aa0-164">[Previous](introducing-the-nerddinner-tutorial.md)
[Next](create-a-database.md)</span></span>
