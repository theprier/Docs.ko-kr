---
uid: web-pages/overview/getting-started/aspnet-web-pages-razor-faq
title: ASP.NET 웹 페이지 (Razor) FAQ | Microsoft Docs
author: tfitzmac
description: 이 문서에서는 ASP.NET Web Pages (Razor) 및 WebMatrix에 대 한 몇 가지 질문과 대답을 나열합니다. 소프트웨어 버전을 사용 하는 자습서 ASP.NET 웹 페이지에서 (R...
ms.author: aspnetcontent
ms.date: 02/07/2014
ms.assetid: b137bd04-25e1-47cb-9d96-ef2e179ecf1f
msc.legacyurl: /web-pages/overview/getting-started/aspnet-web-pages-razor-faq
msc.type: authoredcontent
ms.openlocfilehash: 1f97056c952757ea2d009eaca57d904791e80ca3
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37814238"
---
<a name="aspnet-web-pages-razor-faq"></a><span data-ttu-id="d621d-104">ASP.NET 웹 페이지 (Razor) FAQ</span><span class="sxs-lookup"><span data-stu-id="d621d-104">ASP.NET Web Pages (Razor) FAQ</span></span>
====================
<span data-ttu-id="d621d-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="d621d-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> > [!NOTE] 
> > <span data-ttu-id="d621d-106">WebMatrix는 더 이상 권장 통합된 개발 환경으로 ASP.NET 웹 페이지에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-106">WebMatrix is no longer recommended as an integrated development environment for ASP.NET Web Pages.</span></span> <span data-ttu-id="d621d-107">사용 하 여 [Visual Studio](xref:aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio) 하거나 [Visual Studio Code](https://code.visualstudio.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-107">Use [Visual Studio](xref:aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio) or [Visual Studio Code](https://code.visualstudio.com/).</span></span>
>
> <span data-ttu-id="d621d-108">이 문서에서는 ASP.NET Web Pages (Razor) 및 WebMatrix에 대 한 몇 가지 질문과 대답을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-108">This article lists some frequently asked questions about ASP.NET Web Pages (Razor) and WebMatrix.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="d621d-109">이 자습서에 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="d621d-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="d621d-110">ASP.NET Web Pages (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="d621d-110">ASP.NET Web Pages (Razor) 3</span></span>
> - <span data-ttu-id="d621d-111">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="d621d-111">Visual Studio 2013</span></span>
> - <span data-ttu-id="d621d-112">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="d621d-112">WebMatrix 3</span></span>
>   
> 
> <span data-ttu-id="d621d-113">이 자습서는 ASP.NET 웹 페이지 2, WebMatrix 2 및 Visual Studio 2012 에서도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-113">This tutorial also works with ASP.NET Web Pages 2, WebMatrix 2, and Visual Studio 2012.</span></span>


- [<span data-ttu-id="d621d-114">ASP.NET 웹 페이지, ASP.NET Web Forms 및 ASP.NET MVC의 차이 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="d621d-114">What's the difference between ASP.NET Web Pages, ASP.NET Web Forms, and ASP.NET MVC?</span></span>](#Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC)
- [<span data-ttu-id="d621d-115">WebMatrix 웹 페이지를 사용 하기 위해 필요 합니까?</span><span class="sxs-lookup"><span data-stu-id="d621d-115">Do I need WebMatrix in order to work with Web Pages?</span></span>](#Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages)
- [<span data-ttu-id="d621d-116">ASP.NET Web Forms 페이지의 컨트롤을 웹 페이지를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="d621d-116">Can I use ASP.NET Web Forms controls on a Web Pages page?</span></span>](#Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page)
- [<span data-ttu-id="d621d-117">WebMatrix를 사용 하지 않고 ASP.NET 웹 페이지 사이트를 배포할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="d621d-117">Can I deploy an ASP.NET Web Pages site without using WebMatrix?</span></span>](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix)
- [<span data-ttu-id="d621d-118">로그인을 지원 하기 위해 WebSecurity 도우미를 사용 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="d621d-118">Do I have to use the WebSecurity helper to support logins?</span></span>](#Do_I_have_to_use_the_WebSecurity_helper_to_support_logins)
- [<span data-ttu-id="d621d-119">ASP.NET 웹 페이지에 HTML5 지원 하나요?</span><span class="sxs-lookup"><span data-stu-id="d621d-119">Does ASP.NET Web Pages support HTML5?</span></span>](#Does_ASP.NET_Web_Pages_support_HTML5)
- [<span data-ttu-id="d621d-120">JavaScript 및 jQuery 웹 페이지를 사용 하 여 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="d621d-120">Can I use JavaScript and jQuery with Web Pages?</span></span>](#Can_I_use_JavaScript_and_jQuery_with_Web_Pages)
- [<span data-ttu-id="d621d-121">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="d621d-121">Additional Resources</span></span>](#AdditionalResources)

<span data-ttu-id="d621d-122">오류 및 기타 문제에 대 한 질문에 대 한 참조를 [ASP.NET Web Pages (Razor) 문제 해결 가이드](https://go.microsoft.com/fwlink/?LinkId=253001)합니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-122">For questions about errors and other issues, see the [ASP.NET Web Pages (Razor) Troubleshooting Guide](https://go.microsoft.com/fwlink/?LinkId=253001).</span></span>

<a id="Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC"></a>
## <a name="whats-the-difference-between-aspnet-web-pages-aspnet-web-forms-and-aspnet-mvc"></a><span data-ttu-id="d621d-123">ASP.NET 웹 페이지, ASP.NET Web Forms 및 ASP.NET MVC의 차이 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="d621d-123">What's the difference between ASP.NET Web Pages, ASP.NET Web Forms, and ASP.NET MVC?</span></span>

<span data-ttu-id="d621d-124">세 가지 모두 동적 웹 응용 프로그램을 만들기 위한 ASP.NET 기술을 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-124">All three are ASP.NET technologies for creating dynamic web applications:</span></span>

- <span data-ttu-id="d621d-125">ASP.NET 웹 페이지에 HTML 페이지 및 기능 간단 하 고 간단한 구문 동적 (서버 쪽) 코드 및 데이터베이스 액세스 추가에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-125">ASP.NET Web Pages focuses on adding dynamic (server-side) code and database access to HTML pages, and features simple and lightweight syntax.</span></span>
- <span data-ttu-id="d621d-126">ASP.NET Web Forms는 페이지 개체 모델 및 기존 창 형식 컨트롤 (예: 단추, 목록)을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-126">ASP.NET Web Forms is based on a page object model and traditional window-type controls (buttons, lists, etc.).</span></span> <span data-ttu-id="d621d-127">Web Forms (Windows forms) 클라이언트 기반 개발 작업을 했었다면 모든 사람에 게 익숙한 이벤트 기반 모델을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-127">Web Forms uses an event-based model that's familiar to those who've worked with client-based (Windows forms) development.</span></span>
- <span data-ttu-id="d621d-128">ASP.NET MVC는 ASP.NET에 대 한 모델-뷰-컨트롤러 패턴을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-128">ASP.NET MVC implements the model-view-controller pattern for ASP.NET.</span></span> <span data-ttu-id="d621d-129">중요 한 점은 "문제의 분리"에 (처리, 데이터 및 UI 레이어).</span><span class="sxs-lookup"><span data-stu-id="d621d-129">The emphasis is on "separation of concerns" (processing, data, and UI layers).</span></span>

<span data-ttu-id="d621d-130">모든 세 가지 프레임 워크는 완전히 지원 되며 계속 ASP.NET 팀에서 개발 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-130">All three frameworks are fully supported and continue to be developed by the ASP.NET team.</span></span> <span data-ttu-id="d621d-131">배경에 따라 사용 하는 프레임 워크의 선택 되는 일반적으로 ASP.NET을 사용 하 여 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-131">In general, the choice of which framework to use depends on your background and experience with ASP.NET.</span></span>

<span data-ttu-id="d621d-132">특히 ASP.NET 웹 페이지를 쉽게 서버 처리 해당 페이지를 추가 하는 HTML을 이미 알고 있는 사람들을 위해 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-132">ASP.NET Web Pages in particular was designed to make it easy for people who already know HTML to add server processing to their pages.</span></span> <span data-ttu-id="d621d-133">학생, 취미 개발자, 처음으로 프로그래밍 인 일반적 사용자에 대 한 적합 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-133">It's a good choice for students, hobbyists, people in general who are new to programming.</span></span> <span data-ttu-id="d621d-134">비 ASP.NET 웹 기술 사용 하 여 경험이 있는 개발자를 위한 좋은 선택 일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-134">It can also be a good choice for developers who have experience with non-ASP.NET web technologies.</span></span>

<a id="Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages"></a>
## <a name="do-i-need-webmatrix-in-order-to-work-with-web-pages"></a><span data-ttu-id="d621d-135">WebMatrix 웹 페이지를 사용 하기 위해 필요 합니까?</span><span class="sxs-lookup"><span data-stu-id="d621d-135">Do I need WebMatrix in order to work with Web Pages?</span></span>

<span data-ttu-id="d621d-136">아니요.</span><span class="sxs-lookup"><span data-stu-id="d621d-136">No.</span></span> <span data-ttu-id="d621d-137">WebMatrix는 더 이상 권장 통합된 개발 환경으로 ASP.NET 웹 페이지에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-137">WebMatrix is no longer recommended as an integrated development environment for ASP.NET Web Pages.</span></span> <span data-ttu-id="d621d-138">사용 하 여 [Visual Studio](program-asp-net-web-pages-in-visual-studio.md) 하거나 [Visual Studio Code](https://code.visualstudio.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-138">Use [Visual Studio](program-asp-net-web-pages-in-visual-studio.md) or [Visual Studio Code](https://code.visualstudio.com/).</span></span>

<span data-ttu-id="d621d-139">Visual Studio 또는 Visual Studio Code를 사용 하지 않으려는 경우에 개별적으로 사용 하 여 구성 요소 제품을 설치할 수 있습니다 [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-139">If you don't want to use either Visual Studio or Visual Studio Code, you can install the component products individually using [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span></span> <span data-ttu-id="d621d-140">다음 제품이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-140">You need the following products:</span></span>

- <span data-ttu-id="d621d-141">Microsoft .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="d621d-141">Microsoft .NET Framework 4.5</span></span>
- <span data-ttu-id="d621d-142">ASP.NET MVC 5 (설치 하는 ASP.NET Web Pages 프레임 워크에도)</span><span class="sxs-lookup"><span data-stu-id="d621d-142">ASP.NET MVC 5 (which installs the ASP.NET Web Pages framework as well)</span></span>
- <span data-ttu-id="d621d-143">IIS Express (웹 서버)</span><span class="sxs-lookup"><span data-stu-id="d621d-143">IIS Express (the web server)</span></span>
- <span data-ttu-id="d621d-144">Microsoft SQL Server Compact 4.0 (데이터베이스)</span><span class="sxs-lookup"><span data-stu-id="d621d-144">Microsoft SQL Server Compact 4.0 (the database)</span></span>

<span data-ttu-id="d621d-145">텍스트 편집기를 사용 하 여 편집할 *.cshtml* (또는 *.vbhtml*) 페이지.</span><span class="sxs-lookup"><span data-stu-id="d621d-145">You can use a text editor to edit *.cshtml* (or *.vbhtml*) pages.</span></span>

<span data-ttu-id="d621d-146">SQL Server Compact 데이터베이스 관리 (*.sdf* 파일) 없이 도구는 다소 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-146">Managing SQL Server Compact databases (*.sdf* files) without a tool is a bit harder.</span></span> <span data-ttu-id="d621d-147">관리에 대 한 visual studio containds *.sdf* 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-147">Visual Studio containds tools for managing *.sdf* databases.</span></span> <span data-ttu-id="d621d-148">또한 다양 한 SQL Server 관리 작업을 수행 하는 코드에서 SQL 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-148">You can also run SQL commands in code to perform many SQL Server management tasks.</span></span>

<span data-ttu-id="d621d-149">테스트할 *.cshtml* 통합된 개발 환경 (IDE)를 사용 하지 않고 페이지를 배포할 수 있습니다 라이브 서버.</span><span class="sxs-lookup"><span data-stu-id="d621d-149">To test *.cshtml* pages without using an integrated development environment (IDE), you can deploy them to a live server.</span></span> <span data-ttu-id="d621d-150">(참조 [WebMatrix를 사용 하지 않고는 ASP.NET Web Pages 사이트를 배포할 수 있습니까?](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix))</span><span class="sxs-lookup"><span data-stu-id="d621d-150">(See [Can I deploy an ASP.NET Web Pages site without using WebMatrix?](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix))</span></span>

### <a name="running-iis-express-without-using-an-ide"></a><span data-ttu-id="d621d-151">IIS Express를 실행 하는 IDE를 사용 하지 않고</span><span class="sxs-lookup"><span data-stu-id="d621d-151">Running IIS Express without using an IDE</span></span>

<span data-ttu-id="d621d-152">웹 서버 컴퓨터에서 IIS Express를 설치 하는 경우 페이지를 테스트 하는 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-152">If you install IIS Express on your computer as a web server, you can use that to test the pages.</span></span> <span data-ttu-id="d621d-153">명령줄에서 IIS Express를 실행 하 고 특정 포트 번호를 사용 하 여 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-153">You can run IIS Express from the command line and associate it with a specific port number.</span></span> <span data-ttu-id="d621d-154">요청 하는 경우 다음 포트를 지정 *.cshtml* 브라우저에서 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-154">You then specify that port when you request *.cshtml* files in your browser.</span></span>

<span data-ttu-id="d621d-155">Windows에서 관리자 권한으로 명령 프롬프트를 열고 및 변경 *C:\Program Files\IIS Express입니다.*</span><span class="sxs-lookup"><span data-stu-id="d621d-155">In Windows, open a command prompt with administrator privileges and change to *C:\Program Files\IIS Express.*</span></span> <span data-ttu-id="d621d-156">(64 비트 시스템에 대 한 폴더를 사용 하 여 *C:\Program Files (x86) \IIS Express.)* 다음 사이트의 실제 경로 사용 하 여 다음 명령을 입력:</span><span class="sxs-lookup"><span data-stu-id="d621d-156">(For 64-bit systems, use the folder *C:\Program Files (x86)\IIS Express.)* Then enter the following command, using the actual path to your site:</span></span>

`iisexpress.exe /port:35896 /path:C:\BasicWebSite`

<span data-ttu-id="d621d-157">다른 프로세스에 의해 이미 예약 되지 않는 어떤 포트 번호도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-157">You can use any port number that isn't already reserved by some other process.</span></span> <span data-ttu-id="d621d-158">(1024 위의 포트 번호는 일반적으로 무료입니다.) 에 대 한 합니다 `path` 값, 웹 사이트 폴더의 경로 사용 하 여 위치를 *.cshtml* 파일이 합니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-158">(Port numbers above 1024 are typically free.) For the `path` value, use the path of the website folder where the *.cshtml* files are.</span></span>

<span data-ttu-id="d621d-159">이 명령은 IIS Express 페이지를 사용 하도록 설정 하려면를 실행 한 후에 브라우저를 열고 고를 찾아볼 수 있습니다는 *.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-159">After you run this command to set up IIS Express to serve your pages, you can open a browser and browse to a *.cshtml* file.</span></span> <span data-ttu-id="d621d-160">다음과 같은 URL을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-160">Use a URL like the following:</span></span>

`http://localhost:35896/default.cshtml`

<span data-ttu-id="d621d-161">IIS Express 명령줄 옵션을 사용 하 여 도움말에 대 한 입력 `iisexpress.exe /?` 명령줄에서.</span><span class="sxs-lookup"><span data-stu-id="d621d-161">For help with IIS Express command line options, enter `iisexpress.exe /?` at the command line.</span></span>

<a id="Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page"></a>
## <a name="can-i-use-aspnet-web-forms-controls-on-a-web-pages-page"></a><span data-ttu-id="d621d-162">ASP.NET Web Forms 페이지의 컨트롤을 웹 페이지를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="d621d-162">Can I use ASP.NET Web Forms controls on a Web Pages page?</span></span>

<span data-ttu-id="d621d-163">아니요.</span><span class="sxs-lookup"><span data-stu-id="d621d-163">No.</span></span> <span data-ttu-id="d621d-164">Web Forms 컨트롤 같은 합니다 [확인란을 선택](https://msdn.microsoft.com/library/system.web.ui.webcontrols.checkbox) 컨트롤을 [유효성 검사 컨트롤](https://msdn.microsoft.com/library/bwd43d0x), 및 [GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview) Web Forms 페이지에만 작동을 제어 (*.aspx* 파일).</span><span class="sxs-lookup"><span data-stu-id="d621d-164">Web Forms controls like the [CheckBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.checkbox) control, the [validation controls](https://msdn.microsoft.com/library/bwd43d0x), and the [GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview) control only work in Web Forms pages (*.aspx* files).</span></span> <span data-ttu-id="d621d-165">이러한 컨트롤에는 Web Forms 페이지 프레임 워크가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-165">These controls require the Web Forms page framework.</span></span>

<a id="Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix"></a>
## <a name="can-i-deploy-an-aspnet-web-pages-site-without-using-webmatrix"></a><span data-ttu-id="d621d-166">WebMatrix를 사용 하지 않고 ASP.NET 웹 페이지 사이트를 배포할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="d621d-166">Can I deploy an ASP.NET Web Pages site without using WebMatrix?</span></span>

<span data-ttu-id="d621d-167">예.</span><span class="sxs-lookup"><span data-stu-id="d621d-167">Yes.</span></span> <span data-ttu-id="d621d-168">(일반적으로 사용 하 여 FTP) 서버에 웹 사이트 파일을 수동으로 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-168">You can manually copy website files to a server (typically by using FTP).</span></span> <span data-ttu-id="d621d-169">수동 복사를 수행 하는 경우에 또한 SQL Server Compact (데이터베이스) 지 원하는 파일을 복사 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-169">If you perform a manual copy, you also have to copy the files that support SQL Server Compact (the database).</span></span> <span data-ttu-id="d621d-170">자세한 내용은 블로그 항목을 참조 하세요 [웹 페이지 배포 응용 프로그램 도구 없이](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2317)합니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-170">For details, see the blog entry [Deploying Web Pages applications without a tool](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2317).</span></span>

<a id="Do_I_have_to_use_the_WebSecurity_helper_to_support_logins"></a>
## <a name="do-i-have-to-use-the-websecurity-helper-to-support-logins"></a><span data-ttu-id="d621d-171">로그인을 지원 하기 위해 WebSecurity 도우미를 사용 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="d621d-171">Do I have to use the WebSecurity helper to support logins?</span></span>

<span data-ttu-id="d621d-172">아니요.</span><span class="sxs-lookup"><span data-stu-id="d621d-172">No.</span></span> <span data-ttu-id="d621d-173">`SimpleMembership` ASP.NET 웹 페이지에 포함 된 공급자 옵션 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-173">The `SimpleMembership` provider that is part of ASP.NET Web Pages is one option.</span></span> <span data-ttu-id="d621d-174">(하는 ASP.NET Web Forms에서 사용 하는 데 사용 될 수 있습니다)의 일부인 보안 공급자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-174">The security providers that are part of ASP.NET (that you might be used to working with in Web Forms) are also available.</span></span> <span data-ttu-id="d621d-175">예를 들어 사용할 수 있습니다 폼 인증 ASP.NET 웹 페이지에서 Web Forms에서와 마찬가지로.</span><span class="sxs-lookup"><span data-stu-id="d621d-175">For example, you can use forms authentication in ASP.NET Web Pages just as you would in Web Forms.</span></span> <span data-ttu-id="d621d-176">폼 인증을 사용 하는 방법의 예로, Microsoft 지원 문서 참조 [를 사용 하 여 C#.NET에서 ASP.NET 응용 프로그램에서 How To Implement Forms-Based 인증](https://support.microsoft.com/kb/301240)합니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-176">For one example of how to use forms authentication, see the Microsoft Support article [How To Implement Forms-Based Authentication in Your ASP.NET Application by Using C#.NET](https://support.microsoft.com/kb/301240).</span></span> <span data-ttu-id="d621d-177">간단한 예제를 다운로드 하려면 [ASP.NET 버전의 "로그인 &amp; 암호](http://www.codeguru.com/csharp/.net/net_asp/scripting/article.php/c19295/ASPNET-version-of-Login--Password.htm)합니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-177">To download a simple example, see [ASP.NET version of "Login &amp; Password](http://www.codeguru.com/csharp/.net/net_asp/scripting/article.php/c19295/ASPNET-version-of-Login--Password.htm).</span></span>

<span data-ttu-id="d621d-178">Windows 인증을 사용 하는 방법에 대 한 자세한 내용은 블로그 게시물을 참조 하세요 [를 사용 하 여 Windows 인증 ASP.NET 웹 페이지에서](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2298)합니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-178">For information about how to use Windows authentication, see the blog post [Using Windows authentication in ASP.NET Web Pages](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2298).</span></span>

<a id="Does_ASP.NET_Web_Pages_support_HTML5"></a>
## <a name="does-aspnet-web-pages-support-html5"></a><span data-ttu-id="d621d-179">ASP.NET 웹 페이지에 HTML5 지원 하나요?</span><span class="sxs-lookup"><span data-stu-id="d621d-179">Does ASP.NET Web Pages support HTML5?</span></span>

<span data-ttu-id="d621d-180">예.</span><span class="sxs-lookup"><span data-stu-id="d621d-180">Yes.</span></span> <span data-ttu-id="d621d-181">ASP.NET 웹 페이지를 사용 하 여 만든 페이지 (*.cshtml* 하거나 *.vbhtml* 페이지)는 기본적으로 페이지를 렌더링 하기 전에 서버에서 실행 되는 코드를 포함 하는 HTML 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-181">The pages you create with ASP.NET Web Pages (*.cshtml* or *.vbhtml* pages) are essentially HTML pages that also contain code that runs on the server, before the page is rendered.</span></span> <span data-ttu-id="d621d-182">사용자의 브라우저에서 HTML5를 지 원하는으로에서 HTML5 요소를 사용할 수 있습니다는 *.cshtml* 하거나 *.vbhtml* 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-182">As long as the user's browser supports HTML5, you can use HTML5 elements in a *.cshtml* or *.vbhtml* page.</span></span>

<a id="Can_I_use_JavaScript_and_jQuery_with_Web_Pages"></a>
## <a name="can-i-use-javascript-and-jquery-with-web-pages"></a><span data-ttu-id="d621d-183">JavaScript 및 jQuery 웹 페이지를 사용 하 여 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="d621d-183">Can I use JavaScript and jQuery with Web Pages?</span></span>

<span data-ttu-id="d621d-184">물론입니다!</span><span class="sxs-lookup"><span data-stu-id="d621d-184">Absolutely.</span></span> <span data-ttu-id="d621d-185">ASP.NET 웹 페이지를 사용 하 여 만든 페이지 (*.cshtml* 또는 *.vbhtml* 페이지)에서 서버 코드를 사용 하 여 HTML 페이지 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-185">The pages you create with ASP.NET Web Pages (*.cshtml* or *.vbhtml* pages) are just HTML pages with server code in them.</span></span> <span data-ttu-id="d621d-186">따라서 모든 JavaScript 또는 jQuery를 사용 하 여 일반 HTML 페이지에서 수행할 수 있습니다 에서도 수행할 수는 *.cshtml* 하거나 *.vbhtml* 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-186">Therefore, anything you can do in a normal HTML page by using JavaScript or jQuery you can also do in a *.cshtml* or *.vbhtml* page.</span></span>

<span data-ttu-id="d621d-187">합니다 **시작 사이트** WebMatrix에서 템플릿에 jQuery 라이브러리의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-187">The **Starter Site** template in WebMatrix contains a number of jQuery libraries.</span></span> <span data-ttu-id="d621d-188">해당 템플릿을 사용 하 여 사이트를 만든 경우 합니다 *스크립트* 폴더에는 jQuery core 라이브러리가 포함 되어 (*jquery 1.6.2.js)* 및 jQuery 유효성 검사에 대 한 라이브러리 (*jquery.validate.js*등.).</span><span class="sxs-lookup"><span data-stu-id="d621d-188">If you create a site by using that template, the *Scripts* folder contains a jQuery core library (*jquery-1.6.2.js)* and libraries for jQuery validation (*jquery.validate.js*, etc.).</span></span>

<span data-ttu-id="d621d-189">ASP.NET 웹 페이지를 사용 하 여 jQuery를 사용 하는 방법을 보여 주는 몇 가지 블로그 게시물 보기는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d621d-189">Here are some blog posts that illustrate ways to use jQuery with ASP.NET Web Pages:</span></span>

- <span data-ttu-id="d621d-190">[JQuery의 유용한 기능을 ASP.NET 웹 페이지 추가 WebMatrix를 사용 하 여](http://rachelappel.com/jquery/adding-jquery-goodness-to-asp-net-web-pages-using-webmatrix/) 여 Rachel Appel</span><span class="sxs-lookup"><span data-stu-id="d621d-190">[Adding jQuery Goodness to ASP.NET Web Pages using WebMatrix](http://rachelappel.com/jquery/adding-jquery-goodness-to-asp-net-web-pages-using-webmatrix/) by Rachel Appel</span></span>
- <span data-ttu-id="d621d-191">[5 분: WebMatrix의 jQuery UI + json + jQuery 템플릿](http://joeriks.com/2011/01/30/5-min-webmatrix-jquery-ui-json-jquery-templates/) Jonas Eriksson 여</span><span class="sxs-lookup"><span data-stu-id="d621d-191">[5 min: WebMatrix + jQuery UI + json + jQuery templates](http://joeriks.com/2011/01/30/5-min-webmatrix-jquery-ui-json-jquery-templates/) by Jonas Eriksson</span></span>
- <span data-ttu-id="d621d-192">[WebMatrix 및 jQuery Forms](http://mikesdotnetting.com/Article/155/WebMatrix-And-jQuery-Forms) Mike Brind 여</span><span class="sxs-lookup"><span data-stu-id="d621d-192">[WebMatrix And jQuery Forms](http://mikesdotnetting.com/Article/155/WebMatrix-And-jQuery-Forms) by Mike Brind</span></span>

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a><span data-ttu-id="d621d-193">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="d621d-193">Additional Resources</span></span>


[<span data-ttu-id="d621d-194">ASP.NET 웹 페이지(Razor) 문제 해결 가이드</span><span class="sxs-lookup"><span data-stu-id="d621d-194">ASP.NET Web Pages (Razor) Troubleshooting Guide</span></span>](https://go.microsoft.com/fwlink/?LinkId=253001)

<span data-ttu-id="d621d-195">[WebMatrix 및 ASP.NET Web Pages 포럼](https://forums.asp.net/1224.aspx/1?WebMatrix) ASP.NET 웹 사이트</span><span class="sxs-lookup"><span data-stu-id="d621d-195">[WebMatrix and ASP.NET Web Pages forum](https://forums.asp.net/1224.aspx/1?WebMatrix) on the ASP.NET website</span></span>
