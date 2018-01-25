---
uid: web-pages/overview/testing-and-debugging/aspnet-web-pages-razor-troubleshooting-guide
title: "ASP.NET 웹 페이지 (Razor) 문제 해결 가이드 | Microsoft Docs"
author: tfitzmac
description: "이 문서에서는 ASP.NET Web Pages (Razor) 및 제안 된 일부 솔루션을 작업할 때 발생할 수 있는 문제를 설명 합니다. 소프트웨어 버전 ASP.NET 웹 페이지 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/10/2014
ms.topic: article
ms.assetid: 2a2c1833-0bfe-4e2e-9cc0-341b52c7b121
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/testing-and-debugging/aspnet-web-pages-razor-troubleshooting-guide
msc.type: authoredcontent
ms.openlocfilehash: 72c49ed8b76b5fb5eb15bf01f57980b382607496
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="aspnet-web-pages-razor-troubleshooting-guide"></a><span data-ttu-id="df9aa-104">ASP.NET 웹 페이지 (Razor) 문제 해결 가이드</span><span class="sxs-lookup"><span data-stu-id="df9aa-104">ASP.NET Web Pages (Razor) Troubleshooting Guide</span></span>
====================
<span data-ttu-id="df9aa-105">으로 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="df9aa-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="df9aa-106">이 문서에서는 ASP.NET Web Pages (Razor) 및 제안 된 일부 솔루션을 작업할 때 발생할 수 있는 문제를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-106">This article describes issues that you might have when working with ASP.NET Web Pages (Razor) and some suggested solutions.</span></span>
> 
> ## <a name="software-versions"></a><span data-ttu-id="df9aa-107">소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="df9aa-107">Software versions</span></span>
> 
> 
> - <span data-ttu-id="df9aa-108">ASP.NET 웹 페이지 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="df9aa-108">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="df9aa-109">이 자습서에서는 ASP.NET 웹 페이지 2에서 ASP.NET 웹 페이지 1.0 에서도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-109">This tutorial also works with ASP.NET Web Pages 2 and ASP.NET Web Pages 1.0.</span></span>


<span data-ttu-id="df9aa-110">이 항목에는 다음과 같은 단원이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-110">This topic contains the following sections:</span></span>

- [<span data-ttu-id="df9aa-111">페이지 실행 문제</span><span class="sxs-lookup"><span data-stu-id="df9aa-111">Issues with Running Pages</span></span>](#Issues_Running_.cshtml_Pages)
- [<span data-ttu-id="df9aa-112">Razor 코드 문제</span><span class="sxs-lookup"><span data-stu-id="df9aa-112">Issues with Razor Code</span></span>](#IssuesWithRazorCode)
- [<span data-ttu-id="df9aa-113">멤버 자격 및 보안 문제</span><span class="sxs-lookup"><span data-stu-id="df9aa-113">Issues with Security and Membership</span></span>](#membership)
- [<span data-ttu-id="df9aa-114">전자 메일 문제</span><span class="sxs-lookup"><span data-stu-id="df9aa-114">Issues with Sending Email</span></span>](#email)
- [<span data-ttu-id="df9aa-115">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="df9aa-115">Additional Resources</span></span>](#AdditionalResources)

<span data-ttu-id="df9aa-116">일반적인 질문에 대 한 참조 [ASP.NET 웹 페이지 (Razor) FAQ](https://go.microsoft.com/fwlink/?LinkId=253000)합니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-116">For general questions, see [ASP.NET Web Pages (Razor) FAQ](https://go.microsoft.com/fwlink/?LinkId=253000).</span></span>

<a id="Issues_Running_.cshtml_Pages"></a>
## <a name="issues-with-running-pages"></a><span data-ttu-id="df9aa-117">페이지 실행 문제</span><span class="sxs-lookup"><span data-stu-id="df9aa-117">Issues with Running Pages</span></span>

<span data-ttu-id="df9aa-118">다양 한 문제를 방지할 수 *.cshtml* 및 *.vbhtml* 제대로 실행 되는 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-118">A variety of issues can prevent *.cshtml* and *.vbhtml* pages from running properly.</span></span> <span data-ttu-id="df9aa-119">이 섹션에는 일반적인 오류 메시지 목록과 가능한 원인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-119">This section lists common error messages and likely causes.</span></span>

### <a name="http-error-403---forbidden-access-is-denied"></a><span data-ttu-id="df9aa-120">HTTP 오류 403-사용할 수 없음: 액세스가 거부 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-120">HTTP Error 403 - Forbidden: Access is denied</span></span>

<span data-ttu-id="df9aa-121">*이 디렉터리 또는 사용자가 제공한 자격 증명을 사용 하 여 페이지를 볼 수 있는 권한이 없습니다.*</span><span class="sxs-lookup"><span data-stu-id="df9aa-121">*You do not have permission to view this directory or page using the credentials that you supplied.*</span></span>

<span data-ttu-id="df9aa-122">이 오류는 서버는 올바른 버전의.NET Framework를 실행 하지 않는 경우에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-122">This error can occur if the server is not running the correct version of the .NET Framework.</span></span> <span data-ttu-id="df9aa-123">(로컬 또는 원격) 서버를 실행 중인 컴퓨터에 설치 된.NET Framework 4 이상 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-123">Make sure that the computer that's running the server (locally or remotely) has at least the .NET Framework 4 installed.</span></span> <span data-ttu-id="df9aa-124">또한 응용 프로그램 자체 올바른 버전을 실행 하도록 구성 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-124">Also make sure that the application itself is configured to run the right version.</span></span>

<span data-ttu-id="df9aa-125">WebMatrix에서 작업 하는 동안이 문제를 로컬로 표시를 클릭는 **사이트** 작업 영역에서 클릭 하 여 treeview에서 다음 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-125">If you see this problem locally while working in WebMatrix, click the **Site** workspace, and then in the treeview click **Settings**.</span></span> <span data-ttu-id="df9aa-126">에 **.NET Framework 버전 선택** 목록에서 선택 **.NET 4 (통합)**합니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-126">In the **Select .NET Framework Version** list, select **.NET 4 (Integrated)**.</span></span> <span data-ttu-id="df9aa-127">이 버전은 이미 설정 된 경우 관리자 권한으로 WebMatrix를 실행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="df9aa-127">If this version is already set, try running WebMatrix as an administrator.</span></span>

<span data-ttu-id="df9aa-128">웹 사이트의 루트에 하나 이상 있는지 확인 *.cshtml* 파일이 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-128">Make sure that the root of your website has at least one *.cshtml* file in it.</span></span>

<span data-ttu-id="df9aa-129">웹 서버가 원격 서버에 있으면이 오류를 표시 되 면 서버 관리자를 게 문의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="df9aa-129">If you see this error when the web server is on a remote server, contact the server administrator.</span></span> <span data-ttu-id="df9aa-130">서버에.NET Framework 4 이상을 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-130">Make sure that the server has the .NET Framework 4 or later installed.</span></span> <span data-ttu-id="df9aa-131">또한.net Framework의 해당 버전을 사용 하도록 구성 된 응용 프로그램 풀에서 응용 프로그램이 실행 되 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-131">Also make sure that the application is running in an application pool that's configured to use that version of the.NET Framework.</span></span>

<span data-ttu-id="df9aa-132">서버에 대 한 제어를 사용 하는 경우 올바른 버전의.NET Framework 실행 중인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-132">If you have control over the server, make sure it's running the correct version of the .NET Framework.</span></span> <span data-ttu-id="df9aa-133">실행 하 여 설치를 복구 해 보십시오는 `aspnet_regiis -iru` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-133">You might also try repairing the installation by running the `aspnet_regiis -iru` command.</span></span> <span data-ttu-id="df9aa-134">(예를 들어.NET Framework를 설치한 후 IIS를 설치한 경우 IIS 구성 되지 않습니다 수 올바르게 ASP.NET 페이지를 실행 하도록.) 자세한 내용은 참조 [ASP.NET IIS 등록 도구 (Aspnet\_regiis.exe)](https://msdn.microsoft.com/library/k6h9cz8h(v=vs.100).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-134">(For example, if you install IIS after you install the .NET Framework, IIS will not be correctly configured to run ASP.NET pages.) For more information, see [ASP.NET IIS Registration Tool (Aspnet\_regiis.exe)](https://msdn.microsoft.com/library/k6h9cz8h(v=vs.100).aspx).</span></span>

### <a name="http-error-40314---forbidden"></a><span data-ttu-id="df9aa-135">HTTP 오류 403.14-사용 권한 없음</span><span class="sxs-lookup"><span data-stu-id="df9aa-135">HTTP Error 403.14 - Forbidden</span></span>

<span data-ttu-id="df9aa-136">*웹 서버가이 디렉터리의 콘텐츠를 표시 하지 못하도록 구성 됩니다.*</span><span class="sxs-lookup"><span data-stu-id="df9aa-136">*The Web server is configured to not list the contents of this directory.*</span></span>

<span data-ttu-id="df9aa-137">보호 되는 리소스를 요청 하는 경우이 오류가 발생할 수 있습니다 (같은 *Web.config* 파일)가 있는 보호 되는 폴더 또는 (같은 *앱\_데이터* 또는 *앱\_코드*).</span><span class="sxs-lookup"><span data-stu-id="df9aa-137">This error can occur if you request a resource that's protected (like the *Web.config* file) or that's in a folder that's protected (like *App\_Data* or *App\_Code*).</span></span>

### <a name="http-error-40417---not-found"></a><span data-ttu-id="df9aa-138">HTTP 오류 404.17-찾을 수 없습니다</span><span class="sxs-lookup"><span data-stu-id="df9aa-138">HTTP Error 404.17 - Not Found</span></span>

<span data-ttu-id="df9aa-139">*요청한 콘텐츠가 스크립트로 표시 되 및 정적 파일 처리기에서 처리 되지 않습니다.*</span><span class="sxs-lookup"><span data-stu-id="df9aa-139">*The requested content appears to be script and will not be served by the static file handler.*</span></span>

<span data-ttu-id="df9aa-140">서버에.NET Framework 4를 사용 하도록 올바르게 구성 되지 않은 또는 일부 이므로 나중에 코드를 인식 하지 않으므로 경우이 오류가 발생할 수 `@{ }` 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-140">This error can occur if the server is not configured correctly to use the .NET Framework 4 or later, and therefore does not recognize the code in `@{ }` blocks.</span></span> <span data-ttu-id="df9aa-141">이전 버전에 대 한 설명을 참조 *HTTP 오류 403-사용할 수 없음: 액세스가 거부 되었습니다*합니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-141">See the description earlier for *HTTP Error 403 - Forbidden: Access is denied*.</span></span>

### <a name="http-error-4047---not-found"></a><span data-ttu-id="df9aa-142">HTTP 오류 404.7-찾을 수 없습니다</span><span class="sxs-lookup"><span data-stu-id="df9aa-142">HTTP Error 404.7 - Not Found</span></span>

<span data-ttu-id="df9aa-143">*파일 확장명을 거부 하도록 요청 필터링 모듈이 구성 되어*</span><span class="sxs-lookup"><span data-stu-id="df9aa-143">*The request filtering module is configured to deny the file extension*</span></span>

<span data-ttu-id="df9aa-144">이 오류는 경우에 발생할 수 있습니다 *.cshtml* 또는 *.vbhtml* 확장 서버에 명시적으로 차단 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-144">This error can occur if *.cshtml* or *.vbhtml* extensions have been explicitly blocked on the server.</span></span> <span data-ttu-id="df9aa-145">이 문제의 증상 확장 이지만 포함 하는 Url 포함 하지 않는 경우 작동 하는 Url은 *.cshtml* 또는 *.vbhtml* 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-145">A symptom of this problem is that URLs work when they do not include the extension, but URLs that include *.cshtml* or *.vbhtml* do not work.</span></span> <span data-ttu-id="df9aa-146">사이트의 확장을 다시 사용 가능한 솔루션은 *Web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-146">A possible solution is to re-enable the extensions in the site's *Web.config* file.</span></span> <span data-ttu-id="df9aa-147">다음 예제를 사용 하도록 설정 하는 방법의 *.cshtml* 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-147">The following example shows how to enable the *.cshtml* extension.</span></span>

[!code-xml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample1.xml?highlight=5-6)]

### <a name="http-error-4048---not-found"></a><span data-ttu-id="df9aa-148">HTTP 오류 404.8-찾을 수 없습니다</span><span class="sxs-lookup"><span data-stu-id="df9aa-148">HTTP Error 404.8 - Not Found</span></span>

<span data-ttu-id="df9aa-149">*HiddenSegment 섹션을 포함 하는 URL의 경로 거부 하도록 요청 필터링 모듈이 구성 됩니다.*</span><span class="sxs-lookup"><span data-stu-id="df9aa-149">*The request filtering module is configured to deny a path in the URL that contains a hiddenSegment section.*</span></span>

<span data-ttu-id="df9aa-150">보호 되는 리소스를 요청 하는 경우이 오류가 발생할 수 있습니다 (같은 *Web.config* 파일)가 있는 보호 되는 폴더 또는 (같은 *앱\_데이터* 또는 *앱\_코드*).</span><span class="sxs-lookup"><span data-stu-id="df9aa-150">This error can occur if you request a resource that's protected (like the *Web.config* file) or that's in a folder that's protected (like *App\_Data* or *App\_Code*).</span></span>

### <a name="this-type-of-page-is-not-served-server-error-in--application"></a><span data-ttu-id="df9aa-151">이런이 종류의 페이지 ('/' 응용 프로그램에서 오류 서버) 처리 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-151">This type of page is not served (Server Error in '/' Application)</span></span>

<span data-ttu-id="df9aa-152">HTTP 오류 404.17에 대 한 이전 설명을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="df9aa-152">See the description earlier for HTTP Error 404.17.</span></span>

<a id="IssuesWithRazorCode"></a>
## <a name="issues-with-razor-code"></a><span data-ttu-id="df9aa-153">Razor 코드 문제</span><span class="sxs-lookup"><span data-stu-id="df9aa-153">Issues with Razor code</span></span>

### <a name="the-name-class-does-not-exist-in-the-current-context"></a><span data-ttu-id="df9aa-154">이름 '*클래스*' 현재 컨텍스트에 존재 하지 않습니다</span><span class="sxs-lookup"><span data-stu-id="df9aa-154">The name '*class*' does not exist in the current context</span></span>

<span data-ttu-id="df9aa-155">대개이 오류를 참조 하는 이유는는 `class` 참조 도우미를 있지만 도우미 설치 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-155">Often, a reason you see this error is that `class` references a helper, but the helper is not installed.</span></span> <span data-ttu-id="df9aa-156">예를 들어 도우미를 사용 하려고 하지만에서 NuGet 패키지를 설치 하지 않은 경우이 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-156">For example, if you try to use a helper, but if you haven't installed the package from NuGet, you'll see this error.</span></span> <span data-ttu-id="df9aa-157">WebMatrix의 갤러리를 사용 하 여 찾아서 도우미를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-157">Use the Gallery in WebMatrix to find and install the helper.</span></span>

<span data-ttu-id="df9aa-158">도우미를 설치 했지만 페이지 여전히 인식 하지 않는 것, 추가 시도 추가 `using` 코드에 문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-158">If the helper is installed, but the page still doesn't recognize it, try adding add a `using` statement to the code.</span></span> <span data-ttu-id="df9aa-159">에 `using` 문, 참조 도우미를 포함 하는 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-159">In the `using` statement, reference the namespace that includes the helper.</span></span> <span data-ttu-id="df9aa-160">ASP.NET 웹 도우미 패키지에 있는 기본 도우미는 예를 들어는 `System.Web.Helpers` 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-160">For example, the basic helpers that are in the ASP.NET Web Helpers package are in the `System.Web.Helpers` namespace.</span></span> <span data-ttu-id="df9aa-161">도우미를 사용 하려면 페이지의 위쪽이 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-161">At the top of the page where you want to use the helper, add this line:</span></span>

`@using Microsoft.Web.Helpers;`

<a id="membership"></a>
## <a name="issues-with-security-and-membership"></a><span data-ttu-id="df9aa-162">멤버 자격 및 보안 문제</span><span class="sxs-lookup"><span data-stu-id="df9aa-162">Issues with Security and Membership</span></span>

<span data-ttu-id="df9aa-163">기본 제공 보안 (membership) 시스템 ASP.NET 웹 페이지 (Razor)에서 사용 중인 경우에 다음과 같은 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-163">If you are using the built-in security (membership) system in ASP.NET Web Pages (Razor), you might encounter the following issues.</span></span>

### <a name="to-call-this-method-the-membershipprovider-property-must-be-an-instance-of-extendedmembershipprovider"></a><span data-ttu-id="df9aa-164">이 메서드를 호출 하려면 "Membership.Provider" 속성 "ExtendedMembershipProvider"의 인스턴스를 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-164">To call this method, the "Membership.Provider" property must be an instance of "ExtendedMembershipProvider"</span></span>

<span data-ttu-id="df9aa-165">이 오류를 나타낼 수 없는 `AspNetSqlMembershipProvider` 클래스가 구성 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-165">This error can indicate that no `AspNetSqlMembershipProvider` class is configured.</span></span> <span data-ttu-id="df9aa-166">(으로 이루어졌다는 징후가 사이트 로컬로 제대로 작동 하지만 호스팅 공급자의 서버에 게시할 때이 오류가 발생 합니다.) 이 문제에 대 한 수정이 사이트의 다음을 추가 하 여 간단한 멤버 자격을 명시적으로 활성화 하는 *Web.config* 파일:</span><span class="sxs-lookup"><span data-stu-id="df9aa-166">(A symptom is that the site works fine locally but throws this error when you publish it to a hosting provider's server.) One fix for this problem is to explicitly enable simple membership by adding the following to the site's *Web.config* file:</span></span>

[!code-xml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample2.xml?highlight=6)]

<a id="email"></a>
## <a name="issues-with-sending-email"></a><span data-ttu-id="df9aa-167">전자 메일 문제</span><span class="sxs-lookup"><span data-stu-id="df9aa-167">Issues with Sending Email</span></span>

<span data-ttu-id="df9aa-168">전자 메일 보내기 관련 디버깅 하기 어려울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-168">Problems with sending email can be challenging to debug.</span></span> <span data-ttu-id="df9aa-169">SMTP 서버에 연결할 수는 초기 문제 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-169">An initial problem can be that you can't connect to the SMTP server.</span></span> <span data-ttu-id="df9aa-170">연결이 성공 하는 경우 ASP.NET에 전달한 메시지에서 SMTP 서버에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-170">If the connection is successful, ASP.NET hands the message off to the SMTP server.</span></span> <span data-ttu-id="df9aa-171">그러나 메시지 자체를 보내는 SMTP 서버 수 없는 문제가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-171">However, there can be problems with the message itself that prevents the SMTP server from sending it.</span></span>

<span data-ttu-id="df9aa-172">응용 프로그램이 성공적으로 전자 메일을 보내지 않으면를 다음과 같이 하세요.</span><span class="sxs-lookup"><span data-stu-id="df9aa-172">If your application does not successfully send email, try the following:</span></span>

- <span data-ttu-id="df9aa-173">SMTP 서버 이름을 방식은 다음과 같이 `smtp.provider.com` 또는 `smtp.provider.net`합니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-173">The SMTP server name is often something like `smtp.provider.com` or `smtp.provider.net`.</span></span> <span data-ttu-id="df9aa-174">그러나 사이트를 호스팅 공급자에 게시 하는 경우 SMTP 서버 이름을 해당 지점에서 않을 `localhost`합니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-174">However, if you publish your site to a hosting provider, the SMTP server name at that point might be `localhost`.</span></span> <span data-ttu-id="df9aa-175">이 경우 게시 한 후 사이트 공급자의 서버에서 실행 되는 SMTP 서버 응용 프로그램의 관점에서 로컬 수 있기 때문에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-175">This situation occurs because after you've published and your site is running on the provider's server, the SMTP server might be local from the perspective of your application.</span></span> <span data-ttu-id="df9aa-176">서버 이름에 이러한 변경 의미를 게시 프로세스의 일부로 SMTP 서버 이름을 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-176">This change in server names might mean that you have to change the SMTP server name as part of your publishing process.</span></span>
- <span data-ttu-id="df9aa-177">포트 번호는 일반적으로 25입니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-177">The port number is usually 25.</span></span> <span data-ttu-id="df9aa-178">그러나 일부 공급자 사용 해야 할 포트 587 또는 일부 다른 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-178">However, some providers require you to use port 587 or some other port.</span></span> <span data-ttu-id="df9aa-179">소유자를 확인 하는 SMTP 서버의 포트 번호도 기대 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-179">Check with the owner of the SMTP server what port number they expect you to use.</span></span>
- <span data-ttu-id="df9aa-180">올바른 자격 증명을 사용 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-180">Make sure that you use the right credentials.</span></span> <span data-ttu-id="df9aa-181">사이트를 호스팅 공급자에 게시 한 경우 특별히 설정 된 공급자가 전자 메일에 대 한 자격 증명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-181">If you've published your site to a hosting provider, use the credentials that the provider has specifically indicated are for email.</span></span> <span data-ttu-id="df9aa-182">이러한 자격 증명을 게시 하는 데 자격 증명과 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-182">These credentials might be different from the credentials you use to publish.</span></span>
- <span data-ttu-id="df9aa-183">경우에 따라 자격 증명을 전혀 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-183">Sometimes you don't need credentials at all.</span></span> <span data-ttu-id="df9aa-184">개인 ISP를 사용 하 여 전자 메일을 보내는 경우 전자 메일 공급자에 자격 증명 이미 알고 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-184">If you're sending email by using your personal ISP, your email provider might already know your credentials.</span></span> <span data-ttu-id="df9aa-185">를 게시 한 후 로컬 컴퓨터에서 테스트 아니라 다른 자격 증명을 사용 하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-185">After you publish, you might need to use different credentials than when you test on your local computer.</span></span>
- <span data-ttu-id="df9aa-186">전자 메일 공급자가 암호화를 사용 하는 경우 설정 `WebMail.EnableSsl` 를 `true`합니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-186">If your email provider uses encryption, set `WebMail.EnableSsl` to `true`.</span></span>

<span data-ttu-id="df9aa-187">전자 메일을 보내는 중 오류가 발생 하는 경우 다음과 같이 표시 하는 표준 ASP.NET 오류 메시지가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-187">If there is an error sending email, you might see a standard ASP.NET error message, which looks like this:</span></span>

![전자 메일에 문제가 있을 경우 ASP.NET 오류 메시지](aspnet-web-pages-razor-troubleshooting-guide/_static/image1.png)

<span data-ttu-id="df9aa-189">사용 하 여 전자 메일을 보내는 문제를 디버깅할 수도 있습니다는 `try-catch` 다음 예제와 같이 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-189">You can also debug problems with sending email by using a `try-catch` block, as in the following example.</span></span> <span data-ttu-id="df9aa-190">사용 하는 경우는 `try-catch` ASP.NET 블록의 표준 오류 메시지를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-190">When you use a `try-catch` block, ASP.NET does not display its standard error messages.</span></span> <span data-ttu-id="df9aa-191">대신,에서 오류를 캡처할 수 있습니다는 `catch` 블록의 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-191">Instead, you can capture the error in the `catch` portion of the block.</span></span>

[!code-cshtml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample3.cshtml)]

<span data-ttu-id="df9aa-192">에 대 한 적절 한 값으로 대체 `your-SMTP-server-name`등입니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-192">Substitute the appropriate values for `your-SMTP-server-name`, and so on.</span></span> <span data-ttu-id="df9aa-193">이러한 방식으로 표시 될 수 있는 오류 메시지는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-193">Some of the error messages you might see this way include the following:</span></span>

- <span data-ttu-id="df9aa-194">*메일을 보내지 못했습니다.*</span><span class="sxs-lookup"><span data-stu-id="df9aa-194">*Failure sending mail.*</span></span>

    <span data-ttu-id="df9aa-195">또는</span><span class="sxs-lookup"><span data-stu-id="df9aa-195">-or-</span></span>

    <span data-ttu-id="df9aa-196">*연결 된 구성원 시간 또는 연결 된 호스트에서 응답 하지 없어 연결 기간 후 올바르게 응답 하지 않아 연결 시도가 실패*</span><span class="sxs-lookup"><span data-stu-id="df9aa-196">*A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond*</span></span>

    <span data-ttu-id="df9aa-197">이 오류는 일반적으로 응용 프로그램에서 SMTP 서버에 연결할 수 없습니다 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-197">This error usually means that the application could not connect to the SMTP server.</span></span> <span data-ttu-id="df9aa-198">서버 이름을 확인 하 고 포트 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-198">Check the server name and port number.</span></span>
- <span data-ttu-id="df9aa-199">*사서함을 사용할 수 없습니다. 서버 응답: 5.1.0 &lt; someuser@invaliddomain &gt; 거부 보낸 사람: 잘못 된 보낸 도메인*</span><span class="sxs-lookup"><span data-stu-id="df9aa-199">*Mailbox unavailable. The server response was: 5.1.0 &lt;someuser@invaliddomain&gt; sender rejected : invalid sender domain*</span></span>

    <span data-ttu-id="df9aa-200">이 메시지는 되었음을 나타낼 수 있습니다는 `From` 주소가 잘못 되었거나 없습니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-200">This message can indicate that the `From` address is not correct or is missing.</span></span>
- <span data-ttu-id="df9aa-201">*지정된 된 문자열에 전자 메일 주소 형식이 없는 경우*</span><span class="sxs-lookup"><span data-stu-id="df9aa-201">*The specified string is not in the form required for an e-mail address.*</span></span>

    <span data-ttu-id="df9aa-202">이 오류를 나타낼 수 있습니다의 값은 `To` 또는 `From` 전자 메일 주소로 서 속성을 인식할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-202">This error might indicate that the value of the `To` or `From` properties are not recognized as email addresses.</span></span> <span data-ttu-id="df9aa-203">(ASP.NET 확인할 수 없습니다. 전자 메일 주소가 올바른지 한다는 원하는 올바른 형식으로의  *name@domain.com* .)</span><span class="sxs-lookup"><span data-stu-id="df9aa-203">(ASP.NET cannot check that the email address is valid, only that it's in the correct format, like *name@domain.com*.)</span></span>

> [!NOTE]
> <span data-ttu-id="df9aa-204">이 오류를 표시 하는 태그를 제거 (`@errorMessage`) 페이지를 라이브 사이트에 게시 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="df9aa-204">Remove the markup that displays the error (`@errorMessage`) before you publish the page to a live site.</span></span> <span data-ttu-id="df9aa-205">하지 사용자가 서버에서 얻을 수 있는 오류 메시지를 볼 수 있도록 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="df9aa-205">It's not a good idea to let users see error messages that you get from a server.</span></span>


<a id="AdditionalResources"></a>
## <a name="additional-resources"></a><span data-ttu-id="df9aa-206">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="df9aa-206">Additional Resources</span></span>

[<span data-ttu-id="df9aa-207">ASP.NET 웹 페이지(Razor) FAQ</span><span class="sxs-lookup"><span data-stu-id="df9aa-207">ASP.NET Web Pages (Razor) FAQ</span></span>](https://go.microsoft.com/fwlink/?LinkId=253000)

<span data-ttu-id="df9aa-208">[WebMatrix 및 ASP.NET 웹 페이지](https://forums.asp.net/1224.aspx/1?WebMatrix) ASP.NET 웹 사이트에 대 한 포럼</span><span class="sxs-lookup"><span data-stu-id="df9aa-208">[WebMatrix and ASP.NET Web Pages](https://forums.asp.net/1224.aspx/1?WebMatrix) forum on the ASP.NET website</span></span>
