---
uid: mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
title: 새 ASP.NET MVC 프로젝트 만들기 | Microsoft Docs
author: microsoft
description: 1 단계 기본 업그레이드 되었으며 수정 응용 프로그램 구조 제 자리에 배치 하는 방법을 보여 줍니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: 7e0e9928-8fdc-4b74-9882-55fac0976628
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
msc.type: authoredcontent
ms.openlocfilehash: d15ca67f0ddd8db6842bc5112996ae2dee433536
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30869259"
---
<a name="create-a-new-aspnet-mvc-project"></a><span data-ttu-id="4d66b-103">새 ASP.NET MVC 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="4d66b-103">Create a New ASP.NET MVC Project</span></span>
====================
<span data-ttu-id="4d66b-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="4d66b-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="4d66b-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="4d66b-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="4d66b-106">이 무료의 1 단계 ["업그레이드 되었으며 수정" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 하는 워크 쓰루는 작고 빌드만 ASP.NET MVC 1을 사용 하 여 웹 응용 프로그램을 완료 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="4d66b-106">This is step 1 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="4d66b-107">1 단계 기본 업그레이드 되었으며 수정 응용 프로그램 구조 제 자리에 배치 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4d66b-107">Step 1 shows you how to put the basic NerdDinner application structure in place.</span></span>
> 
> <span data-ttu-id="4d66b-108">ASP.NET MVC 3을 사용 하는 경우 수행한 것이 좋습니다는 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="4d66b-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-step-1-file-gtnew-project"></a><span data-ttu-id="4d66b-109">업그레이드 되었으며 수정 1 단계: 파일-&gt;새 프로젝트</span><span class="sxs-lookup"><span data-stu-id="4d66b-109">NerdDinner Step 1: File-&gt;New Project</span></span>

<span data-ttu-id="4d66b-110">먼저 업그레이드 되었으며 수정 응용 프로그램을 선택 하 여는 **파일-&gt;새 프로젝트** Visual Studio 2008 또는 무료 Visual Web Developer 2008 Express 내에서 메뉴 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="4d66b-110">We'll begin our NerdDinner application by selecting the **File-&gt;New Project** menu item within either Visual Studio 2008 or the free Visual Web Developer 2008 Express.</span></span>

<span data-ttu-id="4d66b-111">이 "새 프로젝트" 대화 상자를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d66b-111">This will bring up the "New Project" dialog.</span></span> <span data-ttu-id="4d66b-112">새 ASP.NET MVC 응용 프로그램을 만들려면 대화 상자의 왼쪽에 "웹" 노드를 선택 하 고 한 다음 오른쪽에서 "ASP.NET MVC 웹 응용 프로그램" 프로젝트 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d66b-112">To create a new ASP.NET MVC application, we'll select the "Web" node on the left-hand side of the dialog and then choose the "ASP.NET MVC Web Application" project template on the right:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image1.png)

<span data-ttu-id="4d66b-113">*중요: 다운로드 하 고 ASP.NET MVC-그렇지 않으면 새 프로젝트 대화 상자에는 나타나지 않습니다 설치 되어 있는지 확인 합니다. V2를 사용할 수는 [Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx) 아직 설치 하지 않은 경우 (ASP.NET MVC는 내에서 사용할 수는 "웹 플랫폼-&gt;프레임 워크 및 런타임" 섹션).*</span><span class="sxs-lookup"><span data-stu-id="4d66b-113">*Important: Make sure you've downloaded and installed ASP.NET MVC - otherwise it won't show up in the New Project dialog. You can use V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) if you haven't installed it yet (ASP.NET MVC is available within the "Web Platform-&gt;Frameworks and Runtimes" section).*</span></span>

<span data-ttu-id="4d66b-114">"업그레이드 되었으며 수정" 만들고을 만드는 "확인" 단추를 클릭 한 다음을 새 프로젝트의 이름을 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d66b-114">We'll name the new project we are going to create "NerdDinner" and then click the "ok" button to create it.</span></span>

<span data-ttu-id="4d66b-115">"확인"을 클릭 하는 경우 Visual Studio도 새 응용 프로그램에 대 한 단위 테스트 프로젝트를 만들고 필요에 따라 요청 하는 추가 대화 상자를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d66b-115">When we click "ok" Visual Studio will bring up an additional dialog that prompts us to optionally create a unit test project for the new application as well.</span></span> <span data-ttu-id="4d66b-116">이 단위 테스트 프로젝트를 사용 하면 기능 및 응용 프로그램의 동작을 확인 하는 자동화 된 테스트를 만들 수 있습니다 (다룰 것 문제가 어떻게이 자습서의 뒷부분에 나오는 할 일)입니다.</span><span class="sxs-lookup"><span data-stu-id="4d66b-116">This unit test project enables us to create automated tests that verify the functionality and behavior of our application (something we'll cover how to-do later in this tutorial).</span></span>

![](create-a-new-aspnet-mvc-project/_static/image2.png)

<span data-ttu-id="4d66b-117">위의 대화 상자에 있는 "테스트 프레임 워크" 드롭다운에서 모든 사용 가능한 ASP.NET MVC 단위 테스트 프로젝트 템플릿이 함께 제공 된 컴퓨터에 설치 되어 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="4d66b-117">The "Test framework" dropdown in the above dialog is populated with all available ASP.NET MVC unit test project templates installed on the machine.</span></span> <span data-ttu-id="4d66b-118">MBUnit, NUnit, XUnit 버전을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d66b-118">Versions can be downloaded for NUnit, MBUnit, and XUnit.</span></span> <span data-ttu-id="4d66b-119">기본 제공 Visual Studio 단위 테스트 프레임 워크 에서도 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d66b-119">The built-in Visual Studio Unit Test framework is also supported.</span></span>

<span data-ttu-id="4d66b-120">*참고: Visual Studio 단위 테스트 프레임 워크는 Visual Studio 2008 Professional 및 이상 버전을 사용할 수만 있습니다. VS 2008 Standard Edition 또는 Visual Web Developer 2008 Express를 사용 하는 경우 다운로드 하 고이 대화 상자 표시 되도록 하려면에서 ASP.NET MVC에 대 한 NUnit, MBUnit 또는 XUnit 확장을 설치 해야 합니다. 모든 테스트 프레임 워크를 설치 하지 않은 경우에 대화 상자 표시 되지 않습니다.*</span><span class="sxs-lookup"><span data-stu-id="4d66b-120">*Note: The Visual Studio Unit Test Framework is only available with Visual Studio 2008 Professional and higher versions. If you are using VS 2008 Standard Edition or Visual Web Developer 2008 Express you will need to download and install the NUnit, MBUnit or XUnit extensions for ASP.NET MVC in order for this dialog to be shown. The dialog will not display if there aren't any test frameworks installed.*</span></span>

<span data-ttu-id="4d66b-121">"Visual Studio 단위 테스트" 프레임 워크 옵션을 사용 하 여 알아보고 만듭니다, 테스트 프로젝트에 대 한 기본 "NerdDinner.Tests" 이름을 사용 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4d66b-121">We'll use the default "NerdDinner.Tests" name for the test project we create, and use the "Visual Studio Unit Test" framework option.</span></span> <span data-ttu-id="4d66b-122">클릭 하면 Visual Studio "확인" 단추는을 수행해 줍니다 솔루션을에-웹 응용 프로그램 및 단위 테스트 프로젝트를 두 개를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d66b-122">When we click the "ok" button Visual Studio will create a solution for us with two projects in it - one for our web application and one for our unit tests:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image3.png)

### <a name="examining-the-nerddinner-directory-structure"></a><span data-ttu-id="4d66b-123">업그레이드 되었으며 수정 디렉터리 구조 검사</span><span class="sxs-lookup"><span data-stu-id="4d66b-123">Examining the NerdDinner directory structure</span></span>

<span data-ttu-id="4d66b-124">Visual Studio와 함께 새 ASP.NET MVC 응용 프로그램을 만들면 프로젝트에 자동으로 다양 한 파일 및 디렉터리 추가:</span><span class="sxs-lookup"><span data-stu-id="4d66b-124">When you create a new ASP.NET MVC application with Visual Studio, it automatically adds a number of files and directories to the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image4.png)

<span data-ttu-id="4d66b-125">기본적으로 ASP.NET MVC 프로젝트는 6 개의 최상위 디렉터리:</span><span class="sxs-lookup"><span data-stu-id="4d66b-125">ASP.NET MVC projects by default have six top-level directories:</span></span>

| <span data-ttu-id="4d66b-126">**Directory**</span><span class="sxs-lookup"><span data-stu-id="4d66b-126">**Directory**</span></span> | <span data-ttu-id="4d66b-127">**용도**</span><span class="sxs-lookup"><span data-stu-id="4d66b-127">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="4d66b-128">**/Controllers**</span><span class="sxs-lookup"><span data-stu-id="4d66b-128">**/Controllers**</span></span> | <span data-ttu-id="4d66b-129">URL 요청을 처리 하는 컨트롤러 클래스를 배치 하는 위치</span><span class="sxs-lookup"><span data-stu-id="4d66b-129">Where you put Controller classes that handle URL requests</span></span> |
| <span data-ttu-id="4d66b-130">**/Models**</span><span class="sxs-lookup"><span data-stu-id="4d66b-130">**/Models**</span></span> | <span data-ttu-id="4d66b-131">나타내고 데이터를 조작 하는 클래스를 배치 하는 위치</span><span class="sxs-lookup"><span data-stu-id="4d66b-131">Where you put classes that represent and manipulate data</span></span> |
| <span data-ttu-id="4d66b-132">**/Views**</span><span class="sxs-lookup"><span data-stu-id="4d66b-132">**/Views**</span></span> | <span data-ttu-id="4d66b-133">렌더링 출력과 담당 하는 UI 템플릿 파일을 저장할 위치</span><span class="sxs-lookup"><span data-stu-id="4d66b-133">Where you put UI template files that are responsible for rendering output</span></span> |
| <span data-ttu-id="4d66b-134">**/Scripts**</span><span class="sxs-lookup"><span data-stu-id="4d66b-134">**/Scripts**</span></span> | <span data-ttu-id="4d66b-135">JavaScript 라이브러리 파일 및 스크립트 (.js)을 저장할 위치</span><span class="sxs-lookup"><span data-stu-id="4d66b-135">Where you put JavaScript library files and scripts (.js)</span></span> |
| <span data-ttu-id="4d66b-136">**/Content**</span><span class="sxs-lookup"><span data-stu-id="4d66b-136">**/Content**</span></span> | <span data-ttu-id="4d66b-137">CSS 및 이미지 파일 및 기타 비-동적/비-JavaScript 콘텐츠를 배치 하는 위치</span><span class="sxs-lookup"><span data-stu-id="4d66b-137">Where you put CSS and image files, and other non-dynamic/non-JavaScript content</span></span> |
| <span data-ttu-id="4d66b-138">**/App\_Data**</span><span class="sxs-lookup"><span data-stu-id="4d66b-138">**/App\_Data**</span></span> | <span data-ttu-id="4d66b-139">데이터 파일을 저장 하는 경우 읽기/쓰기 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d66b-139">Where you store data files you want to read/write.</span></span> |

<span data-ttu-id="4d66b-140">ASP.NET MVC는이 구조를 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4d66b-140">ASP.NET MVC does not require this structure.</span></span> <span data-ttu-id="4d66b-141">사실, 대규모 응용 프로그램에서 작업 하는 개발자는 일반적으로 분할 응용 프로그램을 보다 잘 관리할 수 있도록 여러 프로젝트 (예: 데이터 모델 클래스 것으로 서 별도 클래스 라이브러리 프로젝트에서 웹 응용 프로그램에서).</span><span class="sxs-lookup"><span data-stu-id="4d66b-141">In fact, developers working on large applications will typically partition the application up across multiple projects to make it more manageable (for example: data model classes often go in a separate class library project from the web application).</span></span> <span data-ttu-id="4d66b-142">그러나 기본 프로젝트 구조 म 새로 우리의 응용 프로그램 문제를 유지 하는 데 사용할 수 있는 좋은 기본 디렉터리 규칙을 제공지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4d66b-142">The default project structure, however, does provide a nice default directory convention that we can use to keep our application concerns clean.</span></span>

<span data-ttu-id="4d66b-143">/Controllers 디렉터리 확장 하는 경우는 Visual Studio-HomeController 및 AccountController – 두 컨트롤러 클래스 기본적으로 프로젝트에 추가 소요 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d66b-143">When we expand the /Controllers directory we'll find that Visual Studio added two controller classes – HomeController and AccountController – by default to the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image5.png)

<span data-ttu-id="4d66b-144">/Views 디렉터리 확장을 다음과 같은 세 가지 하위 디렉터리-/Home, /Account /Shared – 뿐 아니라 여러 템플릿 폴더 내의 파일 기본적으로 프로젝트에 추가 된도 찾을 수 했습니다.</span><span class="sxs-lookup"><span data-stu-id="4d66b-144">When we expand the /Views directory, we'll find three sub-directories – /Home, /Account and /Shared – as well as several template files within them were also added to the project by default:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image6.png)

<span data-ttu-id="4d66b-145">/Content 및 /Scripts 디렉터리를 확장 하는 경우 응용 프로그램 내에서 지원 되는 사이트의 모든 HTML 스타일을 지정 하는 데 사용 하는 Site.css 파일 뿐만 아니라 ASP.NET AJAX 및 jQuery 사용 하도록 설정할 수 있는 JavaScript 라이브러리 소요 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d66b-145">When we expand the /Content and /Scripts directories, we'll find a Site.css file that is used to style all HTML on the site, as well as JavaScript libraries that can enable ASP.NET AJAX and jQuery support within the application:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image7.png)

<span data-ttu-id="4d66b-146">NerdDinner.Tests 프로젝트 확장 다음과 같은 컨트롤러 클래스에 대 한 단위 테스트를 포함 하는 두 개의 클래스 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d66b-146">When we expand the NerdDinner.Tests project we'll find two classes that contain unit tests for our controller classes:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image8.png)

<span data-ttu-id="4d66b-147">이러한 기본 파일을 Visual Studio에서 추가를 입력 하는 기본 구조 작업 응용 프로그램-완료 되었으나 페이지, 계정 등록/로그인/로그 아웃 페이지 및 (모든 유선 접속 이며 작동 하 고 즉시) 처리 되지 않은 오류 페이지에 대 한 홈 페이지에 대 한.</span><span class="sxs-lookup"><span data-stu-id="4d66b-147">These default files added by Visual Studio provide us with a basic structure for a working application - complete with home page, about page, account login/logout/registration pages, and an unhandled error page (all wired-up and working out of the box).</span></span>

### <a name="running-the-nerddinner-application"></a><span data-ttu-id="4d66b-148">업그레이드 되었으며 수정 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="4d66b-148">Running the NerdDinner Application</span></span>

<span data-ttu-id="4d66b-149">선택 하 여 프로젝트를 실행할 수 있습니다는 **디버그-&gt;디버깅 시작** 또는 **디버그-&gt;디버깅 하지 않고 시작** 메뉴 항목:</span><span class="sxs-lookup"><span data-stu-id="4d66b-149">We can run the project by choosing either the **Debug-&gt;Start Debugging** or **Debug-&gt;Start Without Debugging** menu items:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image9.png)

<span data-ttu-id="4d66b-150">기본 제공 ASP.NET 웹 서버 Visual Studio와 함께 제공 되는 실행 되 고 응용 프로그램을 실행:</span><span class="sxs-lookup"><span data-stu-id="4d66b-150">This will launch the built-in ASP.NET Web-server that comes with Visual Studio, and run our application:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image10.png)

<span data-ttu-id="4d66b-151">다음은 새 프로젝트 진행에 대 한 홈 페이지 (URL: "/")를 실행할 때:</span><span class="sxs-lookup"><span data-stu-id="4d66b-151">Below is the home page for our new project (URL: "/") when it runs:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image11.png)

<span data-ttu-id="4d66b-152">"정보" 탭을 클릭 하면 표시 됩니다는 페이지에 대 한 (URL: "홈/곧 /"):</span><span class="sxs-lookup"><span data-stu-id="4d66b-152">Clicking the "About" tab displays an about page (URL: "/Home/About"):</span></span>

![](create-a-new-aspnet-mvc-project/_static/image12.png)

<span data-ttu-id="4d66b-153">로그인 페이지에는 오른쪽 위에 "Log On" 링크를 클릭 하면 (URL: "/ 계정/로그온")</span><span class="sxs-lookup"><span data-stu-id="4d66b-153">Clicking the "Log On" link on the top-right takes us to a Login page (URL: "/Account/LogOn")</span></span>

![](create-a-new-aspnet-mvc-project/_static/image13.png)

<span data-ttu-id="4d66b-154">등록 링크를 클릭 하는 로그인 계정을 아직 경우 (URL: "/ 계정/레지스터") 새로 만들려면:</span><span class="sxs-lookup"><span data-stu-id="4d66b-154">If we don't have a login account we can click the register link (URL: "/Account/Register") to create one:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image14.png)

<span data-ttu-id="4d66b-155">에 대 한 위의 홈을 구현 하는 코드 및 로그 아웃 /register 우리의 새 프로젝트를 만들 때 기본적으로 기능이 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4d66b-155">The code to implement the above home, about, and logout/ register functionality was added by default when we created our new project.</span></span> <span data-ttu-id="4d66b-156">응용 프로그램의 시작 지점으로 때 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d66b-156">We'll use it as the starting point of our application.</span></span>

### <a name="testing-the-nerddinner-application"></a><span data-ttu-id="4d66b-157">업그레이드 되었으며 수정 응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="4d66b-157">Testing the NerdDinner Application</span></span>

<span data-ttu-id="4d66b-158">Professional Edition 또는 더 높은 버전의 Visual Studio 2008을 사용 하는 기본 제공 단위 IDE 지원 Visual Studio 내에서 테스트 프로젝트 테스트 하 여 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="4d66b-158">If we are using the Professional Edition or higher version of Visual Studio 2008, we can use the built-in unit testing IDE support within Visual Studio to test the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image15.png)

<span data-ttu-id="4d66b-159">위의 옵션 중 하나를 선택 IDE 내에서 "테스트 결과" 창을 열고를 기본 제공 기능을 포괄 하는 새 프로젝트에 포함 된 27 단위 테스트에 통과/실패 상태와 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d66b-159">Choosing one of the above options will open the "Test Results" pane within the IDE and provide us with pass/fail status on the 27 unit tests included in our new project that cover the built-in functionality:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image16.png)

<span data-ttu-id="4d66b-160">이 자습서의 뒷부분에 대해서는 자동화 된 테스트에 대 한 자세히 알아보고 구현 하는 응용 프로그램 기능을 포괄 하는 추가 단위 테스트를 추가 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4d66b-160">Later in this tutorial we'll talk more about automated testing and add additional unit tests that cover the application functionality we implement.</span></span>

### <a name="next-step"></a><span data-ttu-id="4d66b-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4d66b-161">Next Step</span></span>

<span data-ttu-id="4d66b-162">이제 접수 했습니다 기본 응용 프로그램 구조 위치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d66b-162">We've now got a basic application structure in place.</span></span> <span data-ttu-id="4d66b-163">이제 보겠습니다 [응용 프로그램 데이터를 저장 하도록 데이터베이스를 만들](create-a-database.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4d66b-163">Let's now [create a database to store our application data](create-a-database.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4d66b-164">[이전](introducing-the-nerddinner-tutorial.md)
> [다음](create-a-database.md)</span><span class="sxs-lookup"><span data-stu-id="4d66b-164">[Previous](introducing-the-nerddinner-tutorial.md)
[Next](create-a-database.md)</span></span>
