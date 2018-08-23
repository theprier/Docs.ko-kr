---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
title: ASP.NET 및 Web Tools 2012.2 릴리스 정보 | Microsoft Docs
author: rick-anderson
description: ASP.NET 및 웹 도구 2012.2 릴리스 정보입니다.
ms.author: riande
ms.date: 02/14/2013
ms.assetid: 9534e58b-1d15-4f1d-b04c-10c79b9d8227
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
msc.type: content
ms.openlocfilehash: 0566a362b36f6cfb73b6479cd490e82c63455459
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41835502"
---
<a name="aspnet-and-web-tools-20122-release-notes"></a><span data-ttu-id="5ace0-103">ASP.NET 및 Web Tools 2012.2 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="5ace0-103">ASP.NET and Web Tools 2012.2 Release Notes</span></span>
====================
> <span data-ttu-id="5ace0-104">이 문서에서는 ASP.NET 및 웹 도구 2012.2 릴리스를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-104">This document describes the release of ASP.NET and Web Tools 2012.2.</span></span> <span data-ttu-id="5ace0-105">Visual Studio Web Tooling 및 ASP.NET에 대 한 업데이트는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-105">It is an update to Visual Studio Web Tooling and ASP.NET.</span></span>


- [<span data-ttu-id="5ace0-106">설치 참고 사항</span><span class="sxs-lookup"><span data-stu-id="5ace0-106">Installation Notes</span></span>](#_Installation)
- [<span data-ttu-id="5ace0-107">문서</span><span class="sxs-lookup"><span data-stu-id="5ace0-107">Documentation</span></span>](#_Documentation)
- [<span data-ttu-id="5ace0-108">지원</span><span class="sxs-lookup"><span data-stu-id="5ace0-108">Support</span></span>](#_Support)
- [<span data-ttu-id="5ace0-109">소프트웨어 요구 사항</span><span class="sxs-lookup"><span data-stu-id="5ace0-109">Software Requirements</span></span>](#_Software_Requirements)
- [<span data-ttu-id="5ace0-110">ASP.NET 및 Web Tools 2012.2의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="5ace0-110">New Features in ASP.NET and Web Tools 2012.2</span></span>](#_New_Features_in)

    - [<span data-ttu-id="5ace0-111">도구</span><span class="sxs-lookup"><span data-stu-id="5ace0-111">Tooling</span></span>](#_Tooling)
    - [<span data-ttu-id="5ace0-112">웹 게시</span><span class="sxs-lookup"><span data-stu-id="5ace0-112">Web Publishing</span></span>](#_Web_Publishing)
    - [<span data-ttu-id="5ace0-113">ASP.NET MVC 템플릿</span><span class="sxs-lookup"><span data-stu-id="5ace0-113">ASP.NET MVC Templates</span></span>](#_Templates)
    - [<span data-ttu-id="5ace0-114">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="5ace0-114">ASP.NET Web API</span></span>](#_ASP.NET_Web_API)

    - [<span data-ttu-id="5ace0-115">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="5ace0-115">ASP.NET SignalR</span></span>](#_ASP.NET_SignalR)
    - [<span data-ttu-id="5ace0-116">Asp.net Url</span><span class="sxs-lookup"><span data-stu-id="5ace0-116">ASP.NET Friendly URLs</span></span>](#_ASP.NET_Friendly_URLs)
- [<span data-ttu-id="5ace0-117">알려진된 문제 및 주요 변경 내용</span><span class="sxs-lookup"><span data-stu-id="5ace0-117">Known Issues and Breaking Changes</span></span>](#_Known_Issues_and)

<a id="_Installation"></a>
## <a name="installation-notes"></a><span data-ttu-id="5ace0-118">설치 참고 사항</span><span class="sxs-lookup"><span data-stu-id="5ace0-118">Installation Notes</span></span>

<span data-ttu-id="5ace0-119">ASP.NET 및 Visual Studio 2012 용 웹 도구 2012.2를 사용해 설치 가능 [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-119">ASP.NET and Web Tools 2012.2 for Visual Studio 2012 can be installed using [Web Platform installer](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2).</span></span> <span data-ttu-id="5ace0-120">이것이 Visual Studio 2012 또는 Visual Studio Express 2012 for Web, 필요한 업데이트입니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-120">This is an update to Visual Studio 2012 or Visual Studio Express 2012 for Web, which is required.</span></span> <span data-ttu-id="5ace0-121">설치 된 Visual Studio가 없는 경우 Visual Studio Express 2012 for Web이 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-121">If you do not have Visual Studio installed, Visual Studio Express 2012 for Web will be installed.</span></span>

<span data-ttu-id="5ace0-122">또한 수동으로 설치할 수 있습니다 ASP.NET 및 웹 도구 2012.2 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-122">You can also install ASP.NET and Web Tools 2012.2 manually.</span></span> <span data-ttu-id="5ace0-123">Visual Studio 2012 또는 Visual Studio Express 2012 for Web 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-123">You must have Visual Studio 2012 or Visual Studio Express 2012 for Web installed.</span></span> <span data-ttu-id="5ace0-124">다음 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="5ace0-124">Then use the following instructions:</span></span> 

1. <span data-ttu-id="5ace0-125">다운로드 [ASP.NET 및 Frameworks 2012.2 웹](https://download.microsoft.com/download/6/5/6/6562AFBE-9503-4E64-970C-1427133FCD73/AspNetWebTools2012Setup.exe) 다운로드 센터에서 설치 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-125">Download [ASP.NET and Web Frameworks 2012.2](https://download.microsoft.com/download/6/5/6/6562AFBE-9503-4E64-970C-1427133FCD73/AspNetWebTools2012Setup.exe) installer from Download Center.</span></span>
2. <span data-ttu-id="5ace0-126">경우 입력 정보를 요청 실행을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-126">When prompted click Run.</span></span> <span data-ttu-id="5ace0-127">또한 나중에 실행 파일을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-127">You can also save the file to run it later.</span></span>
3. <span data-ttu-id="5ace0-128">업데이트는 Visual Studio의 버전을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-128">Verify the version of Visual Studio you will update.</span></span> <span data-ttu-id="5ace0-129">업데이트 하려는 Visual Studio를 시작 하 여이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-129">You can do this by launching the Visual Studio you wish to update.</span></span> <span data-ttu-id="5ace0-130">도움말 메뉴 항목을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-130">Then click the Help menu item.</span></span>   
    ![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.jpg)
4. <span data-ttu-id="5ace0-131">메뉴 항목을 표시 하는 경우 &quot;에 대 한 Microsoft Visual Studio 2012 for Web&quot; 다운로드 한 다음 [Visual Studio Express 2012 for Web-웹 개발자 도구 2012.2](https://go.microsoft.com/fwlink/?LinkID=282228)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-131">If you see the menu item &quot;About Microsoft Visual Studio 2012 for Web&quot; then download [Web Developer Tools 2012.2 - Visual Studio Express 2012 for Web](https://go.microsoft.com/fwlink/?LinkID=282228).</span></span> <span data-ttu-id="5ace0-132">그렇지 않은 경우 다운로드할 [웹 개발자 도구 2012.2-Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282228)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-132">Otherwise download [Web Developer Tools 2012.2 - Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282228).</span></span>
5. <span data-ttu-id="5ace0-133">경우 입력 정보를 요청 실행을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-133">When prompted click Run.</span></span> <span data-ttu-id="5ace0-134">또한 나중에 실행 파일을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-134">You can also save the file to run it later.</span></span>

> [!NOTE]
> <span data-ttu-id="5ace0-135">ASP.NET 및 웹 도구 2012.2 릴리스는 SQL Server Data Tools를 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-135">ASP.NET and Web Tools 2012.2 release does not include SQL Server Data Tools.</span></span> <span data-ttu-id="5ace0-136">SQL Server 및 Windows Azure SQL Database는 다양 한 데이터베이스 오프 라인 프로젝트 기반의 개발, 스키마 비교 및 향상 된 데이터베이스 배포 기능을 포함 하 여 도구를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-136">SQL Server and Windows Azure SQL Databases provides a richer set of database tooling including offline project-backed development, schema comparison and enhanced database deployment capabilities.</span></span> <span data-ttu-id="5ace0-137">자세한 내용을 보거나 SQL Server Data Tools 설치를 방문 [ https://go.microsoft.com/fwlink/?LinkID=237127 ](https://go.microsoft.com/fwlink/?LinkID=237127)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-137">For more information or to install SQL Server Data Tools visit [https://go.microsoft.com/fwlink/?LinkID=237127](https://go.microsoft.com/fwlink/?LinkID=237127).</span></span>

<a id="_Documentation"></a>
## <a name="documentation"></a><span data-ttu-id="5ace0-138">설명서</span><span class="sxs-lookup"><span data-stu-id="5ace0-138">Documentation</span></span>

<span data-ttu-id="5ace0-139">ASP.NET 및 웹 도구 2012.2 정보 및 자습서는 ASP.NET 웹 사이트에서 사용할 수 있습니다 ( https://www.asp.net)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-139">Tutorials and other information about ASP.NET and Web Tools 2012.2 are available from ASP.NET web site ( https://www.asp.net).</span></span>

<a id="_Support"></a>
## <a name="support"></a><span data-ttu-id="5ace0-140">Support(지원)</span><span class="sxs-lookup"><span data-stu-id="5ace0-140">Support</span></span>

<span data-ttu-id="5ace0-141">ASP.NET 및 웹 도구 2012.2 릴리스 공식적으로 이며 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-141">ASP.NET and Web Tools 2012.2 is officially released and supported.</span></span> <span data-ttu-id="5ace0-142">일반적인 지원 채널을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-142">You can use your normal support channel.</span></span> <span data-ttu-id="5ace0-143">ASP.NET 포럼에 질문을 게시할 수도 있습니다 ([https://forums.asp.net/](https://forums.asp.net/)) ASP.NET 커뮤니티 회원이 비공식적인 지원을 제공 하기 위해 자주 수 있는, 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-143">You can also post questions to the ASP.NET forums ([https://forums.asp.net/](https://forums.asp.net/)), where members of the ASP.NET community are frequently able to provide informal support.</span></span>

<a id="_Software_Requirements"></a>
## <a name="software-requirements"></a><span data-ttu-id="5ace0-144">소프트웨어 요구 사항</span><span class="sxs-lookup"><span data-stu-id="5ace0-144">Software Requirements</span></span>

<span data-ttu-id="5ace0-145">ASP.NET 및 웹 도구 2012.2 Visual Studio 2012 또는 Visual Studio Express 2012 for Web 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-145">The ASP.NET and Web Tools 2012.2 requires Visual Studio 2012 or Visual Studio Express 2012 for Web.</span></span>

<a id="_New_Features_in"></a>
## <a name="new-features-in-aspnet-and-web-tools-20122"></a><span data-ttu-id="5ace0-146">ASP.NET 및 Web Tools 2012.2의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="5ace0-146">New Features in ASP.NET and Web Tools 2012.2</span></span>

<span data-ttu-id="5ace0-147">이 섹션에서는 ASP.NET 및 웹 도구 2012.2 릴리스에서 도입 된 기능을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-147">This section describes features that have been introduced in the ASP.NET and Web Tools 2012.2 release.</span></span>

<a id="_Tooling"></a>
### <a name="tooling"></a><span data-ttu-id="5ace0-148">도구</span><span class="sxs-lookup"><span data-stu-id="5ace0-148">Tooling</span></span>

- <span data-ttu-id="5ace0-149">페이지 검사기</span><span class="sxs-lookup"><span data-stu-id="5ace0-149">Page Inspector</span></span> 

    - <span data-ttu-id="5ace0-150">페이지 검사기에 페이지를 다시 해당 JavaScript 코드에 동적으로 추가 된 항목을 매핑할 수 있도록 하는 JavaScript 선택 매핑을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-150">Support JavaScript selection mapping allowing Page Inspector to map items that were dynamically added to the page back to the corresponding JavaScript code.</span></span>
    - <span data-ttu-id="5ace0-151">실시간 CSS 업데이트를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-151">The ability to see CSS updates in real-time.</span></span>
    - <span data-ttu-id="5ace0-152">자세한 내용은 [CSS 자동 동기화 및 페이지 검사기에서 JavaScript 선택 매핑](https://blogs.msdn.com/b/webdev/archive/2012/12/14/css-auto-sync-and-javascript-selection-mapping-in-page-inspector.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-152">For more information, read [CSS Auto-Sync and JavaScript Selection Mapping in Page Inspector](https://blogs.msdn.com/b/webdev/archive/2012/12/14/css-auto-sync-and-javascript-selection-mapping-in-page-inspector.aspx).</span></span>
- <span data-ttu-id="5ace0-153">편집기</span><span class="sxs-lookup"><span data-stu-id="5ace0-153">Editor</span></span> 

    - <span data-ttu-id="5ace0-154">CoffeeScript, Mustache, Handlebars, 및 JsRender에 대 한 구문 강조 표시를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-154">Support syntax highlighting for CoffeeScript, Mustache, Handlebars, and JsRender.</span></span>
    - <span data-ttu-id="5ace0-155">HTML 편집기 Knockout 바인딩에 대 한 Intellisense를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-155">The HTML editor provides Intellisense for Knockout bindings.</span></span>
    - <span data-ttu-id="5ace0-156">작은 편집 및 컴파일러 작은 사용 하 여 동적 CSS를 빌드할 수 있도록 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-156">LESS editing and compiler support to enable building dynamic CSS using LESS.</span></span>
    - <span data-ttu-id="5ace0-157">.NET 클래스로 JSON 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-157">Paste JSON as a .NET class.</span></span> <span data-ttu-id="5ace0-158">이 특수 붙여넣기 명령을 사용 하 여 C# 또는 VB.NET 코드 파일을 Visual Studio에 JSON를 붙여 넣습니다. JSON에서 유추 하는.NET 클래스를 자동으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-158">Using this Special Paste command to paste JSON into a C# or VB.NET code file, and Visual Studio will automatically generate .NET classes inferred from the JSON.</span></span>
- <span data-ttu-id="5ace0-159">VSIX로 타사 에뮬레이터를 설치할 수 있도록 확장성 후크를 추가 하는 모바일 에뮬레이터 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-159">Mobile Emulator support adds extensibility hooks so that third-party emulators can be installed as a VSIX.</span></span> <span data-ttu-id="5ace0-160">설치 된 에뮬레이터 나타납니다 F5 드롭다운 목록에서 개발자는 다양 한 모바일 장치에서 웹 사이트를 미리 볼 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-160">The installed emulators will show up in the F5 dropdown, so that developers can preview their websites on a variety of mobile devices.</span></span> <span data-ttu-id="5ace0-161">Scott Hanselman의 블로그 항목을이 기능에 대해 자세히 알아보세요 [Visual Studio를 사용 하 여 새 BrowserStack 통합](http://www.hanselman.com/blog/CrossBrowserDebuggingIntegratedIntoVisualStudioWithBrowserStack.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-161">Read more about this feature in Scott Hanselman's blog entry on [the new BrowserStack integration with Visual Studio](http://www.hanselman.com/blog/CrossBrowserDebuggingIntegratedIntoVisualStudioWithBrowserStack.aspx).</span></span>

<a id="_Web_Publishing"></a>
### <a name="web-publishing"></a><span data-ttu-id="5ace0-162">웹 게시</span><span class="sxs-lookup"><span data-stu-id="5ace0-162">Web Publishing</span></span>

- <span data-ttu-id="5ace0-163">웹 사이트 프로젝트는 이제 Windows Azure 웹 사이트에 게시를 포함 하 여 웹 응용 프로그램 프로젝트와 동일한 게시 환경을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-163">Web site projects now have the same publishing experience as Web Application projects including publishing to Windows Azure Web Sites.</span></span>
- <span data-ttu-id="5ace0-164">선택적 게시 &#8211; 하나 이상의 파일 (웹 배포 끝점에 게시) 한 후 다음 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-164">Selective publish &#8211; for one or more files you can perform the following actions (after publishing to a Web Deploy endpoint):</span></span> 

    - <span data-ttu-id="5ace0-165">선택한 파일을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-165">Publish selected files.</span></span>
    - <span data-ttu-id="5ace0-166">로컬 파일 및 원격 파일 간의 차이 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5ace0-166">See the difference between a local file and a remote file.</span></span>
    - <span data-ttu-id="5ace0-167">원격 파일을 사용 하 여 로컬 파일을 업데이트 하거나 로컬 파일을 사용 하 여 원격 파일을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-167">Update the local file with the remote file or update the remote file with the local file.</span></span>

<a id="_Templates"></a>
### <a name="aspnet-mvc-templates"></a><span data-ttu-id="5ace0-168">ASP.NET MVC 템플릿</span><span class="sxs-lookup"><span data-stu-id="5ace0-168">ASP.NET MVC Templates</span></span>

- <span data-ttu-id="5ace0-169">새 Facebook 응용 프로그램 템플릿 Facebook Canvas 응용 프로그램을 쉽게 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-169">The new Facebook Application template makes writing Facebook Canvas applications easy.</span></span> <span data-ttu-id="5ace0-170">몇 가지 간단한 단계에서 로그인된 한 사용자에서 데이터를 가져와서 해당 친구와 통합 되는 Facebook 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-170">In a few simple steps, you can create a Facebook application that gets data from a logged in user and integrates with their friends.</span></span> <span data-ttu-id="5ace0-171">템플릿에 인증, 사용 권한, Facebook 데이터 액세스를 포함 하 여 Facebook 응용 프로그램 작성과 관련 된 모든 배관을 처리 하기 위한 새 라이브러리가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-171">The template includes a new library to take care of all the plumbing involved in building a Facebook app, including authentication, permissions, accessing Facebook data and more.</span></span> <span data-ttu-id="5ace0-172">Facebook 응용 프로그램 템플릿을 사용 하 여 대 한 자세한 내용은 참조 하세요 [ https://go.microsoft.com/fwlink/?LinkID=269921 ](https://go.microsoft.com/fwlink/?LinkID=269921)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-172">For more information on using the Facebook Application template see [https://go.microsoft.com/fwlink/?LinkID=269921](https://go.microsoft.com/fwlink/?LinkID=269921).</span></span>
- <span data-ttu-id="5ace0-173">새 단일 페이지 응용 프로그램 MVC 템플릿을 HTML 5, CSS 3 및 Knockout 및 jQuery JavaScript 라이브러리를 ASP.NET Web API를 사용 하 여 대화형 클라이언트 쪽 웹 앱을 빌드하는 개발자를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-173">A new Single Page Application MVC template allows developers to build interactive client-side web apps using HTML 5, CSS 3, and the popular Knockout and jQuery JavaScript libraries, on top of ASP.NET Web API.</span></span> <span data-ttu-id="5ace0-174">템플릿은 RESTful 서버 API를 사용 하는 JavaScript HTML5 응용 프로그램을 작성 하기 위한 일반적인 방법을 보여 주는 "todo" 목록 응용 프로그램을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-174">The template includes a "todo" list application that demonstrates common practices for building a JavaScript HTML5 application that uses a RESTful server API.</span></span> <span data-ttu-id="5ace0-175">자세히 알아볼 수 있습니다 [ https://www.asp.net/single-page-application ](../../../single-page-application/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-175">You can read more at [https://www.asp.net/single-page-application](../../../single-page-application/index.md).</span></span>
- <span data-ttu-id="5ace0-176">이제 ASP.NET MVC 새 프로젝트 대화 상자에 새 템플릿을 추가 하는 VSIX를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-176">You can now create a VSIX that adds new templates to the ASP.NET MVC New Project dialog.</span></span> <span data-ttu-id="5ace0-177">여기에서 방법을 알아보세요. [https://go.microsoft.com/fwlink/?LinkId=275019](https://go.microsoft.com/fwlink/?LinkId=275019)</span><span class="sxs-lookup"><span data-stu-id="5ace0-177">Learn how here: [https://go.microsoft.com/fwlink/?LinkId=275019](https://go.microsoft.com/fwlink/?LinkId=275019)</span></span>
- <span data-ttu-id="5ace0-178">FixedDisplayModes 패키지 &#8211; MVC 프로젝트 템플릿은 MVC 4의 버그 해결을 포함 하는 새 'FixedDisplayModes' NuGet 패키지를 포함 하도록 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-178">FixedDisplayModes package &#8211; MVC project templates have been updated to include the new ‘FixedDisplayModes' NuGet package, which contains a workaround for a bug in MVC 4.</span></span> <span data-ttu-id="5ace0-179">패키지에 포함 된 수정에 대 한 자세한 내용은이 블로그 게시물을 참조 하세요 ([https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx)) MVC 팀에서.</span><span class="sxs-lookup"><span data-stu-id="5ace0-179">For more information on the fix contained in the package, refer to this blog post ([https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx)) from the MVC team.</span></span>

<a id="_ASP.NET_Web_API"></a>
### <a name="aspnet-web-api"></a><span data-ttu-id="5ace0-180">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="5ace0-180">ASP.NET Web API</span></span>

<span data-ttu-id="5ace0-181">ASP.NET Web API 몇 가지 새로운 기능을 사용 하 여 향상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-181">ASP.NET Web API has been enhanced with several new features:</span></span>

- <span data-ttu-id="5ace0-182">ASP.NET Web API OData</span><span class="sxs-lookup"><span data-stu-id="5ace0-182">ASP.NET Web API OData</span></span>
- <span data-ttu-id="5ace0-183">ASP.NET Web API 추적</span><span class="sxs-lookup"><span data-stu-id="5ace0-183">ASP.NET Web API Tracing</span></span>
- <span data-ttu-id="5ace0-184">ASP.NET Web API 도움말 페이지</span><span class="sxs-lookup"><span data-stu-id="5ace0-184">ASP.NET Web API Help Page</span></span>

#### <a name="aspnet-web-api-odata"></a><span data-ttu-id="5ace0-185">ASP.NET Web API OData</span><span class="sxs-lookup"><span data-stu-id="5ace0-185">ASP.NET Web API OData</span></span>

<span data-ttu-id="5ace0-186">ASP.NET Web API OData는 모든 데이터 원본에 대해 다양 한 비즈니스 논리를 사용 하 여 OData 끝점을 작성 하는 데 필요한 유연성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-186">ASP.NET Web API OData gives you the flexibility you need to build OData endpoints with rich business logic over any data source.</span></span> <span data-ttu-id="5ace0-187">ASP.NET Web API OData를 사용 하 여 OData 의미 체계를 노출 하려는 양을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-187">With ASP.NET Web API OData you control the amount of OData semantics that you want to expose.</span></span> <span data-ttu-id="5ace0-188">ASP.NET Web API OData는 ASP.NET MVC 4 프로젝트 템플릿이 포함 되어 있으며 NuGet에서 사용할 수 있습니다 ([http://www.nuget.org/packages/microsoft.aspnet.webapi.odata](http://www.nuget.org/packages/microsoft.aspnet.webapi.odata)).</span><span class="sxs-lookup"><span data-stu-id="5ace0-188">ASP.NET Web API OData is included with the ASP.NET MVC 4 project templates and is also available from NuGet ([http://www.nuget.org/packages/microsoft.aspnet.webapi.odata](http://www.nuget.org/packages/microsoft.aspnet.webapi.odata)).</span></span>

<span data-ttu-id="5ace0-189">ASP.NET Web API OData는 현재 다음과 같은 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-189">ASP.NET Web API OData currently supports the following features:</span></span>

- <span data-ttu-id="5ace0-190">[Queryable] 특성을 적용 하 여 OData 쿼리 의미 체계를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-190">Enable OData query semantics by applying the [Queryable] attribute.</span></span>
- <span data-ttu-id="5ace0-191">쉽게 OData 쿼리의 유효성을 검사 하 고 지원 되는 쿼리 옵션, 연산자 및 함수는 집합을 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-191">Easily validate OData queries and restrict the set of supported query options, operators and functions.</span></span>
- <span data-ttu-id="5ace0-192">매개 변수 다음의 유효성을 검사 하 고 수 IEnumerable 또는 IQueryable에 적용 하는 쿼리의 추상 구문 트리 표현을 가져오는에 직접 ODataQueryOptions에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-192">Parameter bind to ODataQueryOptions directly to get an abstract syntax tree representation of the query that can then be validated and applied to an IQueryable or IEnumerable.</span></span>
- <span data-ttu-id="5ace0-193">[Queryable] 특성에서 결과 한도 지정 하 여 서비스 기반 페이징 및 다음 페이지 링크 생성을 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-193">Enable service-driven paging and next page link generation by specifying result limits on [Queryable] attribute.</span></span>
- <span data-ttu-id="5ace0-194">총 $inlinecount을 사용 하 여 일치 하는 리소스에 대 한 인라인된 카운트를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-194">Request an inlined count of the total number of matching resources using $inlinecount.</span></span>
- <span data-ttu-id="5ace0-195">Null 전파를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-195">Control null propagation.</span></span>
- <span data-ttu-id="5ace0-196">$Filter에서 일부/모든 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-196">Any/All operators in $filter.</span></span>
- <span data-ttu-id="5ace0-197">규칙에 따라 엔터티 데이터 모델을 유추 하거나 명시적으로 유사한를 Entity Framework 코드 중심 방식으로 모델을 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-197">Infer an entity data model by convention or explicitly customize a model in a manner similar to Entity Framework Code-First.</span></span>
- <span data-ttu-id="5ace0-198">EntitySetController에서 파생 하 여 노출 엔터티 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-198">Expose entity sets by deriving from EntitySetController.</span></span>
- <span data-ttu-id="5ace0-199">탐색 속성을 노출 하 고 링크를 조작할 OData 작업 구현에 대 한 간단 하 고 사용자 지정 가능한 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-199">Simple, customizable conventions for exposing navigation properties, manipulating links and implementing OData actions.</span></span>
- <span data-ttu-id="5ace0-200">MapODataRoute 확장 메서드를 사용 하 여 라우팅 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-200">Simplified routing using the MapODataRoute extension method.</span></span>
- <span data-ttu-id="5ace0-201">여러 EDM 모델을 노출 하 여 버전 관리를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-201">Support for versioning by exposing multiple EDM models.</span></span>
- <span data-ttu-id="5ace0-202">서비스 문서 및 노출 $metadata 클라이언트 (.NET, Windows Phone, Windows 스토어 등)를 생성할 수 있습니다 웹 API에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-202">Expose service document and $metadata so you can generate clients (.NET, Windows Phone, Windows Store, etc.) for your Web API.</span></span>
- <span data-ttu-id="5ace0-203">OData Atom, JSON 및 JSON 자세한 정보 표시 형식에 대해 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-203">Support for the OData Atom, JSON, and JSON verbose formats.</span></span>
- <span data-ttu-id="5ace0-204">만들기, 업데이트, 부분적으로 업데이트 (PATCH) 및 엔터티를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-204">Create, update, partially update (PATCH) and delete entities.</span></span>
- <span data-ttu-id="5ace0-205">쿼리하고 엔터티 간의 관계를 조작 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-205">Query and manipulate relationships between entities.</span></span>
- <span data-ttu-id="5ace0-206">연결 하 여 경로 관계 링크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-206">Create relationship links that wire up to your routes.</span></span>
- <span data-ttu-id="5ace0-207">복합 형식</span><span class="sxs-lookup"><span data-stu-id="5ace0-207">Complex types.</span></span>
- <span data-ttu-id="5ace0-208">엔터티 형식 상속 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-208">Entity Type Inheritance.</span></span>
- <span data-ttu-id="5ace0-209">컬렉션 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-209">Collection properties.</span></span>
- <span data-ttu-id="5ace0-210">열거형입니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-210">Enums.</span></span>
- <span data-ttu-id="5ace0-211">OData 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-211">OData actions.</span></span>
- <span data-ttu-id="5ace0-212">동일한 기반 WCF Data Services, 즉 ODataLib 기반으로 ([http://www.nuget.org/packages/microsoft.data.odata](http://www.nuget.org/packages/microsoft.data.odata)).</span><span class="sxs-lookup"><span data-stu-id="5ace0-212">Built upon the same foundation as WCF Data Services, namely ODataLib ([http://www.nuget.org/packages/microsoft.data.odata](http://www.nuget.org/packages/microsoft.data.odata)).</span></span>

<span data-ttu-id="5ace0-213">ASP.NET Web API OData에 대 한 자세한 내용은 참조 하세요 [ https://go.microsoft.com/fwlink/?LinkId=271141 ](https://go.microsoft.com/fwlink/?LinkId=271141)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-213">For more information on ASP.NET Web API OData see [https://go.microsoft.com/fwlink/?LinkId=271141](https://go.microsoft.com/fwlink/?LinkId=271141).</span></span>

#### <a name="aspnet-web-api-tracing"></a><span data-ttu-id="5ace0-214">ASP.NET Web API 추적</span><span class="sxs-lookup"><span data-stu-id="5ace0-214">ASP.NET Web API Tracing</span></span>

<span data-ttu-id="5ace0-215">.NET 추적을 사용 하 여 web Api에서에서 추적 데이터를 통합 하는 ASP.NET Web API 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-215">ASP.NET Web API Tracing integrates tracing data from your web APIs with .NET Tracing.</span></span> <span data-ttu-id="5ace0-216">이제 Web API 프로젝트 템플릿에 기본적으로 활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-216">It is now enabled by default in the Web API project template.</span></span> <span data-ttu-id="5ace0-217">웹에 대 한 데이터를 추적 Api 출력 창에 전송 되 고 IntelliTrace를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-217">Tracing data for your web APIs is sent to the Output window and is made available through IntelliTrace.</span></span> <span data-ttu-id="5ace0-218">통합을 통해 Windows Azure에서 호스트 되는 경우 Web API에 대 한 정보를 추적 하면 ASP.NET 웹 API 추적 [Windows Azure 진단](https://msdn.microsoft.com/library/windowsazure/hh411529.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-218">ASP.NET Web API Tracing enables you to trace information about your Web API when hosted on Windows Azure through integration with [Windows Azure Diagnostics](https://msdn.microsoft.com/library/windowsazure/hh411529.aspx).</span></span> <span data-ttu-id="5ace0-219">또한 설치 하 고 ASP.NET 웹 API 추적 NuGet 패키지를 사용 하 여 모든 응용 프로그램에서 ASP.NET 웹 API 추적을 사용 수 있습니다 ([http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing](http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing)).</span><span class="sxs-lookup"><span data-stu-id="5ace0-219">You can also install and enable ASP.NET Web API Tracing in any application using the ASP.NET Web API Tracing NuGet package ([http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing](http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing)).</span></span>

<span data-ttu-id="5ace0-220">구성 및 ASP.NET Web API 추적 사용에 대 한 자세한 내용은 참조 하세요 [ https://go.microsoft.com/fwlink/?LinkID=269874 ](https://go.microsoft.com/fwlink/?LinkID=269874)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-220">For more information on configuring and using ASP.NET Web API Tracing see [https://go.microsoft.com/fwlink/?LinkID=269874](https://go.microsoft.com/fwlink/?LinkID=269874).</span></span>

#### <a name="aspnet-web-api-help-page"></a><span data-ttu-id="5ace0-221">ASP.NET Web API 도움말 페이지</span><span class="sxs-lookup"><span data-stu-id="5ace0-221">ASP.NET Web API Help Page</span></span>

<span data-ttu-id="5ace0-222">이제 ASP.NET Web API 도움말 페이지는 Web API 프로젝트 템플릿에 기본적으로 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-222">The ASP.NET Web API Help Page is now included by default in the Web API project template.</span></span> <span data-ttu-id="5ace0-223">ASP.NET Web API 도움말 페이지는 자동으로 웹 HTTP 끝점, 지원 되는 HTTP 메서드, 매개 변수 및 예제 요청 및 응답 메시지 페이로드를 포함 하 여 Api에 대 한 설명서를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-223">The ASP.NET Web API Help Page automatically generates documentation for web APIs including the HTTP endpoints, the supported HTTP methods, parameters and example request and response message payloads.</span></span> <span data-ttu-id="5ace0-224">문서를 자동으로 코드의 주석에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-224">Documentation is automatically pulled from comments in your code.</span></span> <span data-ttu-id="5ace0-225">ASP.NET Web API 도움말 페이지 NuGet 패키지를 사용 하 여 모든 응용 프로그램에 ASP.NET Web API 도움말 페이지를 추가할 수도 있습니다 ([http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage](http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage)).</span><span class="sxs-lookup"><span data-stu-id="5ace0-225">You can also add the ASP.NET Web API Help Page to any application using the ASP.NET Web API Help Page NuGet package ([http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage](http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage)).</span></span>

<span data-ttu-id="5ace0-226">설정 및 ASP.NET Web API 도움말 페이지 참조를 사용자 지정에 대 한 자세한 내용은 [ https://go.microsoft.com/fwlink/?LinkId=271140 ](https://go.microsoft.com/fwlink/?LinkId=271140)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-226">For more information on setting up and customizing the ASP.NET Web API Help Page see [https://go.microsoft.com/fwlink/?LinkId=271140](https://go.microsoft.com/fwlink/?LinkId=271140).</span></span>

<a id="_ASP.NET_SignalR"></a>
### <a name="aspnet-signalr"></a><span data-ttu-id="5ace0-227">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="5ace0-227">ASP.NET SignalR</span></span>

<span data-ttu-id="5ace0-228">ASP.NET SignalR을 간단히 ASP.NET 응용 프로그램에 실시간 웹 기능을 추가 및 가능 하면 Websocket을 사용 하 여 자동으로 대체 다른 기술 하지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="5ace0-228">ASP.NET SignalR makes it simple to add real-time web capabilities to your ASP.NET application, using WebSockets if available and automatically falling back to other techniques when it isn't.</span></span>

<span data-ttu-id="5ace0-229">ASP.NET SignalR을 사용 하 여 대 한 자세한 내용은 참조 하세요 [ https://go.microsoft.com/fwlink/?LinkId=271271 ](https://go.microsoft.com/fwlink/?LinkId=271271)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-229">For more information on using ASP.NET SignalR see [https://go.microsoft.com/fwlink/?LinkId=271271](https://go.microsoft.com/fwlink/?LinkId=271271).</span></span>

<a id="_ASP.NET_Friendly_URLs"></a>
### <a name="aspnet-friendly-urls"></a><span data-ttu-id="5ace0-230">Asp.net Url</span><span class="sxs-lookup"><span data-stu-id="5ace0-230">ASP.NET Friendly URLs</span></span>

<span data-ttu-id="5ace0-231">ASP.NET FriendlyURLs 매우 쉽게 웹 개발자에 게 forms (.aspx 확장명 없음) Url을 찾고 수행 되는 클리너를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-231">ASP.NET FriendlyURLs makes it very easy for web forms developers to generate cleaner looking URLs(without the .aspx extension).</span></span> <span data-ttu-id="5ace0-232">No로 적은 구성이 필요로 하 고 기존 ASP.NET v4.0 응용 프로그램과 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-232">It requires little to no configuration and can be used with existing ASP.NET v4.0 applications.</span></span> <span data-ttu-id="5ace0-233">FriendlyURLs 기능 또한 쉽게 지원 데스크톱 및 모바일 보기 간에 전환 하 여 해당 응용 프로그램에 모바일 지원을 추가 하는 개발자를 위한 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-233">The FriendlyURLs feature also makes it easier for developers to add mobile support to their applications, by supporting switching between desktop and mobile views.</span></span>

<span data-ttu-id="5ace0-234">설치 및 ASP.NET Url 사용에 대 한 자세한 내용은 참조 하세요 [ http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx ](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-234">For more information on installing and using ASP.NET Friendly URLs see [http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx).</span></span>

<a id="_Known_Issues_and"></a>
## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="5ace0-235">알려진된 문제 및 주요 변경 내용</span><span class="sxs-lookup"><span data-stu-id="5ace0-235">Known Issues and Breaking Changes</span></span>

<span data-ttu-id="5ace0-236">이 섹션에는 알려진된 문제 및 ASP.NET 및 웹 도구 2012.2 릴리스에 주요 변경 내용을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-236">This section describes known issues and breaking changes that are in the ASP.NET and Web Tools 2012.2 release.</span></span>

### <a name="installation-issues"></a><span data-ttu-id="5ace0-237">설치 문제</span><span class="sxs-lookup"><span data-stu-id="5ace0-237">Installation Issues</span></span>

#### <a name="out-of-order-installs-of-visual-studio-2012"></a><span data-ttu-id="5ace0-238">Visual Studio 2012의 순서가 설치</span><span class="sxs-lookup"><span data-stu-id="5ace0-238">Out of order installs of Visual Studio 2012</span></span>

<span data-ttu-id="5ace0-239">복구 작업을 해야 ASP.NET 및 웹 도구 2012.2 설치 후는 추가 SKU의 Visual Studio 2012를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-239">Installing an additional SKU of Visual Studio 2012 after installing the ASP.NET and Web Tools 2012.2 will require a repair operation.</span></span> <span data-ttu-id="5ace0-240">다음 시퀀스를 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-240">Consider the following sequence:</span></span>

1. <span data-ttu-id="5ace0-241">웹용 Visual Studio 2012 Express 설치</span><span class="sxs-lookup"><span data-stu-id="5ace0-241">Install Visual Studio 2012 Express for Web</span></span>
2. <span data-ttu-id="5ace0-242">ASP.NET 및 Web Tools 2012.2 설치</span><span class="sxs-lookup"><span data-stu-id="5ace0-242">Install ASP.NET and Web Tools 2012.2</span></span>
3. <span data-ttu-id="5ace0-243">Visual Studio 2012 Professional, Premium 또는 Ultimate를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-243">Install Visual Studio 2012 Professional, Premium or Ultimate</span></span>

<span data-ttu-id="5ace0-244">2 단계 Express for Web 용 업데이트 설치만 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-244">Step 2 would only result in installing updates for Express for Web.</span></span> <span data-ttu-id="5ace0-245">3 단계 중에 설치 하는 추가 SKU 업데이트를 포함 하도록 설치 하는 마지막 SKU에 대 한 업데이트를 설치 하려면 ASP.NET 및 웹 도구 2012.2 복구 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-245">To ensure that the additional SKU installed during step 3 contains the update you will need to repair the ASP.NET and Web Tools 2012.2 to install the updates for the last SKU installed.</span></span> <span data-ttu-id="5ace0-246">또한 1 단계에서에서 Sku 및 3 반대 하는 경우이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-246">This also applies if the SKUs in Step 1 and 3 are reversed.</span></span>

#### <a name="installing-microsoft-aspnet-and-web-tools-20122-when-visual-studio-is-open"></a><span data-ttu-id="5ace0-247">Visual Studio에 열려 있을 때 Microsoft ASP.NET 및 웹 도구 2012.2 설치</span><span class="sxs-lookup"><span data-stu-id="5ace0-247">Installing Microsoft ASP.NET and Web Tools 2012.2 when Visual Studio is open</span></span>

<span data-ttu-id="5ace0-248">Microsoft ASP.NET 및 웹 도구 2012.2 설치 하는 동안 VS가 열려 있으면 Visual Studio는 잘못 된 상태로 종료 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-248">If VS is open during installation of Microsoft ASP.NET and Web Tools 2012.2, Visual Studio might end up in a bad state.</span></span> <span data-ttu-id="5ace0-249">사용자 설치를 계속 하기 전에 Visual Studio의 모든 인스턴스를 닫고는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-249">It is recommended that users close all instances of Visual Studio before proceeding with install.</span></span>

#### <a name="canceling-aspnet-and-web-tools-20122-setup-in-the-middle-of-installation"></a><span data-ttu-id="5ace0-250">설치 도중 ASP.NET 및 웹 도구 2012.2 설치 취소</span><span class="sxs-lookup"><span data-stu-id="5ace0-250">Canceling ASP.NET and Web Tools 2012.2 setup in the middle of installation</span></span>

<span data-ttu-id="5ace0-251">ASP.NET 및 웹 도구 2012.2 취소 설치 도중 설치는 Visual Studio 잘못 된 상태에서 종료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-251">Canceling ASP.NET and Web Tools 2012.2 setup in the middle of installation will leave Visual Studio in a bad state.</span></span> <span data-ttu-id="5ace0-252">다음이 단계에 따라가 문제를 해결를:</span><span class="sxs-lookup"><span data-stu-id="5ace0-252">To address this problem follow these steps:</span></span> 

- <span data-ttu-id="5ace0-253">프로그램 추가/제거로 이동</span><span class="sxs-lookup"><span data-stu-id="5ace0-253">Go to Add Remove Programs</span></span>
- <span data-ttu-id="5ace0-254">있는 경우 Microsoft ASP.NET 및 웹 도구 2012.2를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-254">Uninstall Microsoft ASP.NET and Web Tools 2012.2, if present.</span></span>
- <span data-ttu-id="5ace0-255">Microsoft ASP.NET 및 Web Tools 2012.2 다시 설치</span><span class="sxs-lookup"><span data-stu-id="5ace0-255">Reinstall Microsoft ASP.NET and Web Tools 2012.2</span></span>

#### <a name="after-uninstalling-aspnet-and-web-tools-20122-the-aspnet-mvc-4-templates-and-razor-v2-web-site-templates-are-missing"></a><span data-ttu-id="5ace0-256">ASP.NET 및 웹 도구 2012.2 ASP.NET MVC 4를 제거한 후 템플릿 및 Razor v2 웹 사이트 템플릿이 없는</span><span class="sxs-lookup"><span data-stu-id="5ace0-256">After uninstalling ASP.NET and Web Tools 2012.2 the ASP.NET MVC 4 templates and Razor v2 Web Site templates are missing</span></span>

<span data-ttu-id="5ace0-257">ASP.NET 및 웹 도구 2012.2 제거 해도 Visual Studio 2012에서는 모든 ASP.NET MVC 4 및 Razor v2 웹 사이트 템플릿을 제거도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-257">Uninstalling ASP.NET and Web Tools 2012.2 will also uninstall all of ASP.NET MVC 4 and Razor v2 Web Site templates from Visual Studio 2012.</span></span>

<span data-ttu-id="5ace0-258">ASP.NET MVC 4 및 Razor v2 웹 사이트 템플릿 다시 설치 하려면 Visual Studio 2012 설치를 복구 하려면이 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-258">The workaround is to repair your Visual Studio 2012 installation to reinstall ASP.NET MVC 4 and Razor v2 Web Site templates.</span></span>

### <a name="tooling-issues"></a><span data-ttu-id="5ace0-259">도구 문제</span><span class="sxs-lookup"><span data-stu-id="5ace0-259">Tooling Issues</span></span>

#### <a name="nuget-error-reported-during-project-creation"></a><span data-ttu-id="5ace0-260">프로젝트를 만드는 동안 오류가 NuGet</span><span class="sxs-lookup"><span data-stu-id="5ace0-260">NuGet error reported during project creation</span></span>

<span data-ttu-id="5ace0-261">ASP.NET 및 웹 도구 2012.2를 설치한 후 표시 될 수 있는 MVC 4 프로젝트를 만들 때 다음 오류</span><span class="sxs-lookup"><span data-stu-id="5ace0-261">After installing ASP.NET and Web Tools 2012.2 you may see the following error when creating an MVC 4 project</span></span>

![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.png)

<span data-ttu-id="5ace0-262">ASP.NET 및 웹 도구 2012.2 NuGet 2.1을 함께 제공 되 고 Visual Studio 2012에서 확장을 업그레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-262">The ASP.NET and Web Tools 2012.2 ships NuGet 2.1 and will upgrade the extension in Visual Studio 2012.</span></span> <span data-ttu-id="5ace0-263">일부 경우에 VSIX 설치 관리자 VSIX를 올바르게 업데이트 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-263">In some cases, the VSIX installer will fail to correctly update the VSIX.</span></span> <span data-ttu-id="5ace0-264">다음 단계를 사용 하면이 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-264">The following steps will allow you to address this problem:</span></span>

1. <span data-ttu-id="5ace0-265">관리자 권한으로 Visual Studio 2012 시작</span><span class="sxs-lookup"><span data-stu-id="5ace0-265">Start Visual Studio 2012 as an Administrator</span></span>
2. <span data-ttu-id="5ace0-266">이동 도구-&gt;확장 및 업데이트 하 고 NuGet을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-266">Go to Tools-&gt;Extensions and Updates and uninstall NuGet.</span></span>
3. <span data-ttu-id="5ace0-267">Visual Studio를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-267">Close Visual Studio</span></span>
4. <span data-ttu-id="5ace0-268">ASP.NET 및 웹 도구 2012.2 설치 폴더로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-268">Navigate to the ASP.NET and Web Tools 2012.2 installation folder:</span></span>

    1. <span data-ttu-id="5ace0-269">Visual Studio 2012: **Files\Microsoft ASP.NET\ASP.NET 웹 Stack\Visual Studio 2012 프로그램**</span><span class="sxs-lookup"><span data-stu-id="5ace0-269">For Visual Studio 2012: **Program Files\Microsoft ASP.NET\ASP.NET Web Stack\Visual Studio 2012**</span></span>
    2. <span data-ttu-id="5ace0-270">Visual Studio 2012 Express for Web에 대 한: **Program Files\Microsoft ASP.NET\ASP.NET 웹 Stack\Visual Studio Express 2012 for Web**</span><span class="sxs-lookup"><span data-stu-id="5ace0-270">For Visual Studio 2012 Express for Web: **Program Files\Microsoft ASP.NET\ASP.NET Web Stack\Visual Studio Express 2012 for Web**</span></span>
5. <span data-ttu-id="5ace0-271">NuGet을 다시 설치 하려면 NuGet.Tools.vsix를 두 번 클릭</span><span class="sxs-lookup"><span data-stu-id="5ace0-271">Double click on the NuGet.Tools.vsix to reinstall NuGet</span></span>

### <a name="web-api-issues"></a><span data-ttu-id="5ace0-272">웹 API 문제</span><span class="sxs-lookup"><span data-stu-id="5ace0-272">Web API Issues</span></span>

#### <a name="parsing-issues-in-filter-and-datetime-literals"></a><span data-ttu-id="5ace0-273">구문 분석 문제 $filter 및 날짜/시간 리터럴</span><span class="sxs-lookup"><span data-stu-id="5ace0-273">Parsing issues in $filter and DateTime literals</span></span>

<span data-ttu-id="5ace0-274">OData URI 파서에서 부분 날짜/시간 리터럴을 올바르게 구문 분석 하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-274">The OData URI parser fails to parse partial datetime literals properly.</span></span> <span data-ttu-id="5ace0-275">예를 들어 $filter 시작 ' 2012 eq 날짜/시간 =-12-31T12:00' 올바르게 구문 분석 하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-275">For example, $filter=start eq datetime'2012-12-31T12:00' fails to parse properly.</span></span> <span data-ttu-id="5ace0-276">전체 리터럴 $filter를 사용 하는 해결 방법을 시작 ' 2012 eq 날짜/시간 =-12-31T12:00:00'.</span><span class="sxs-lookup"><span data-stu-id="5ace0-276">A workaround is to use the full literal, $filter=start eq datetime'2012-12-31T12:00:00'.</span></span>

#### <a name="odata-doesnt-support-case-insensitive-property-names"></a><span data-ttu-id="5ace0-277">OData는 대/소문자 속성 이름을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-277">OData doesn't support case-insensitive property names.</span></span>

<span data-ttu-id="5ace0-278">OData는 OData 쿼리 및 odata 경로에서 대/소문자 속성 이름을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-278">OData doesn't support case-insensitive property names in OData queries and odata path.</span></span> <span data-ttu-id="5ace0-279">작업 항목을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5ace0-279">See workitems:</span></span>

- [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)
- [http://aspnetwebstack.codeplex.com/workitem/704](http://aspnetwebstack.codeplex.com/workitem/704)

<span data-ttu-id="5ace0-280">사용자가 javascript 클라이언트 쪽 및 서버 쪽에서 대/소문자가는 것은이 문제가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-280">If users have different casing on javascript client side and server side, they probably will encounter this issue.</span></span> <span data-ttu-id="5ace0-281">이 문제는 odata 프로토콜의 의도적입니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-281">This issue is by design in odata protocol.</span></span> <span data-ttu-id="5ace0-282">그러나 많은 사용자가이 문제를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-282">However, many users reports this issue.</span></span> <span data-ttu-id="5ace0-283">이 해결 하려면 사용자의 경우 url에서을 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-283">To work around it, users have to correct their cases in URL.</span></span>

#### <a name="default-odata-routing-conventions-doesnt-support-postput-on-navigation-property"></a><span data-ttu-id="5ace0-284">기본 OData 라우팅 규칙은 탐색 속성에 대해 POST/PUT를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-284">Default OData routing conventions doesn't support POST/PUT on navigation property.</span></span>

<span data-ttu-id="5ace0-285">기본 OData 라우팅 규칙은 탐색 속성에 대해 POST/PUT를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-285">Default OData routing conventions doesn't support POST/PUT on navigation property.</span></span> <span data-ttu-id="5ace0-286">작업 항목을 참조 하세요 [ http://aspnetwebstack.codeplex.com/workitem/366 ](http://aspnetwebstack.codeplex.com/workitem/366)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-286">See workitem [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366).</span></span> <span data-ttu-id="5ace0-287">자주 사용 되는이 규칙이 기본 규칙에 누락 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-287">We are missing this commonly used convention in default conventions.</span></span>

<span data-ttu-id="5ace0-288">이 해결 하려면 사용자를 지원 하도록 새 라우팅 규칙을 확장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-288">To work around it, users need to extend new routing convention to support it.</span></span>

### <a name="facebook-template-issues"></a><span data-ttu-id="5ace0-289">Facebook 템플릿 문제</span><span class="sxs-lookup"><span data-stu-id="5ace0-289">Facebook Template Issues</span></span>

#### <a name="facebook-application-template-only-works-using-net-45"></a><span data-ttu-id="5ace0-290">.NET 4.5를 사용 하 여 Facebook 응용 프로그램 템플릿을 에서만 작동</span><span class="sxs-lookup"><span data-stu-id="5ace0-290">Facebook Application template only works using .NET 4.5</span></span>

<span data-ttu-id="5ace0-291">ASP.NET MVC 4에서 Facebook 응용 프로그램 템플릿을 참조 하는 새 프로젝트 대화 상자의 framework 드롭다운 목록에서.NET 4.5를 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-291">You must select .NET 4.5 in the framework dropdown list in the New Project dialog to see the Facebook Application template in ASP.NET MVC 4.</span></span>

#### <a name="real-time-update-controller"></a><span data-ttu-id="5ace0-292">컨트롤러 실시간 업데이트</span><span class="sxs-lookup"><span data-stu-id="5ace0-292">Real-time Update Controller</span></span>

<span data-ttu-id="5ace0-293">Facebook 응용 프로그램 템플릿을 쉽게 사용자 수 있도록 Facebook의 실시간 업데이트를 처리 하는 웹 API 컨트롤러를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-293">The Facebook Application template allows user easily create a Web API Controller to handle real-time updates from Facebook.</span></span> <span data-ttu-id="5ace0-294">NAT 뒤에 개발 컴퓨터 이면 컨트롤러 추가 네트워크 구성 없이 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-294">If your development machine is behind NAT, your Controller may not work without further network configuration.</span></span> <span data-ttu-id="5ace0-295">자세한 내용은 여기를 참조 하십시오. [http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook](http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook)</span><span class="sxs-lookup"><span data-stu-id="5ace0-295">See here for details: [http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook](http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook)</span></span>

#### <a name="query-string-values-conflict-with-facebook-oauth-parameters"></a><span data-ttu-id="5ace0-296">Facebook OAuth 매개 변수를 사용 하 여 문자열 값이 충돌 하는 쿼리</span><span class="sxs-lookup"><span data-stu-id="5ace0-296">Query string values conflict with Facebook OAuth parameters</span></span>

<span data-ttu-id="5ace0-297">다음 필드를 Facebook OAuth 대화의 호출을 사용 하 여 충돌 URL을 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-297">The following fields conflict with Facebook OAuth dialog's call back URL.</span></span> <span data-ttu-id="5ace0-298">같은 이름의 고유한 쿼리 문자열 값을 추가 하지 마십시오: 코드, 오류, 오류\_설명, 오류\_이유입니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-298">Do not add your own query string values with the following names: code, error, error\_description, error\_reason.</span></span>

#### <a name="using-page-inspector-with-facebook-template"></a><span data-ttu-id="5ace0-299">Facebook 템플릿을 사용 하 여 페이지 검사기 사용</span><span class="sxs-lookup"><span data-stu-id="5ace0-299">Using Page Inspector with Facebook Template</span></span>

<span data-ttu-id="5ace0-300">Facebook 응용 프로그램을 디버깅 하는 동안 Visual Studio 2012에서 페이지 검사기 기능을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-300">You can't use the Page Inspector feature in Visual Studio 2012 while debugging your Facebook Application.</span></span> <span data-ttu-id="5ace0-301">페이지 검사기는 iframes를 현재 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-301">The Page Inspector does not currently support iframes.</span></span>

### <a name="single-page-application-template-issues"></a><span data-ttu-id="5ace0-302">단일 페이지 응용 프로그램 템플릿 문제</span><span class="sxs-lookup"><span data-stu-id="5ace0-302">Single Page Application Template Issues</span></span>

#### <a name="with-jquery-19knockout-221-update-when-running-default-mvc-spa-project-new-todo-item-edit-enter-focus-event-is-not-handled-properly"></a><span data-ttu-id="5ace0-303">1.9/Knockout 2.2.1 업데이트, 기본 MVC SPA 프로젝트에 새 할 일 항목 편집을 실행 하는 경우 입력 JQuery를 사용 하 여 포커스 이벤트가 올바르게 처리 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-303">With JQuery 1.9/Knockout 2.2.1 update, when running default MVC SPA project, new todo item edit enter focus event is not handled properly.</span></span>

<span data-ttu-id="5ace0-304">JQuery 1.9/Knockout 2.2.1 사용 하 여 업데이트를 기본 MVC SPA 프로젝트를 실행 하는 경우 새 todo 항목 편집 입력 더 이상 포커스 새 todo 항목 편집 상자에 다시 할 일 목록에 새 할 일 항목을 입력 한 후.</span><span class="sxs-lookup"><span data-stu-id="5ace0-304">With JQuery 1.9/Knockout 2.2.1 update, when running default MVC SPA project, new todo item edit enter no longer focus back to the new todo item edit box after entering the new todo item to the todo list.</span></span>

<span data-ttu-id="5ace0-305">해결 방법 참조 [ http://knockoutjs.com/documentation/hasfocus-binding.html ](http://knockoutjs.com/documentation/hasfocus-binding.html), 다음 샘플 코드와 유사한 수정 하 고:</span><span class="sxs-lookup"><span data-stu-id="5ace0-305">To workaround reference [http://knockoutjs.com/documentation/hasfocus-binding.html](http://knockoutjs.com/documentation/hasfocus-binding.html), and make similar fix to the following sample code:</span></span>

<span data-ttu-id="5ace0-306">Todo.model.js 파일</span><span class="sxs-lookup"><span data-stu-id="5ace0-306">File todo.model.js</span></span>  
 <span data-ttu-id="5ace0-307">todolist(data) 함수를 추가 합니다. 다음:</span><span class="sxs-lookup"><span data-stu-id="5ace0-307">function todolist(data), add following:</span></span>  
 <span data-ttu-id="5ace0-308">**self.isSelected = ko.observable(false);**</span><span class="sxs-lookup"><span data-stu-id="5ace0-308">**self.isSelected = ko.observable(false);**</span></span>

<span data-ttu-id="5ace0-309">todoList.prototype.addTodo 함수, 다음 blacked 텍스트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-309">function todoList.prototype.addTodo, add the following blacked text:</span></span>  
 <span data-ttu-id="5ace0-310">**self.isSelected(true);**</span><span class="sxs-lookup"><span data-stu-id="5ace0-310">**self.isSelected(true);**</span></span>  
 <span data-ttu-id="5ace0-311">self.newTodoTitle(&quot;&quot;);</span><span class="sxs-lookup"><span data-stu-id="5ace0-311">self.newTodoTitle(&quot;&quot;);</span></span>

<span data-ttu-id="5ace0-312">Index.cshtml 파일 blacked 다음 텍스트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ace0-312">File index.cshtml, add the following blacked text:</span></span>  
 <span data-ttu-id="5ace0-313">&lt;데이터 바인딩 폼 =&quot;제출: addTodo&quot;&gt;</span><span class="sxs-lookup"><span data-stu-id="5ace0-313">&lt;form data-bind=&quot;submit: addTodo&quot;&gt;</span></span>  
 <span data-ttu-id="5ace0-314">&lt;input class=&quot;addTodo&quot; type=&quot;text&quot; data-bind=&quot;value: newTodoTitle, placeholder: 'Type here to add', blurOnEnter: true, **hasfocus: isSelected**, event: { blur: addTodo }&quot; /&gt;</span><span class="sxs-lookup"><span data-stu-id="5ace0-314">&lt;input class=&quot;addTodo&quot; type=&quot;text&quot; data-bind=&quot;value: newTodoTitle, placeholder: 'Type here to add', blurOnEnter: true, **hasfocus: isSelected**, event: { blur: addTodo }&quot; /&gt;</span></span>  
 <span data-ttu-id="5ace0-315">&lt;/form&gt;</span><span class="sxs-lookup"><span data-stu-id="5ace0-315">&lt;/form&gt;</span></span>
