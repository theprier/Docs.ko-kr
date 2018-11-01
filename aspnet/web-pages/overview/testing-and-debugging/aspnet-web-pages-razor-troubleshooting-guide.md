---
uid: web-pages/overview/testing-and-debugging/aspnet-web-pages-razor-troubleshooting-guide
title: ASP.NET 웹 페이지 (Razor) 문제 해결 가이드 | Microsoft Docs
author: tfitzmac
description: 이 문서에서는 ASP.NET Web Pages (Razor) 및 몇 가지 제안 된 솔루션을 작업할 때 발생할 수 있는 문제를 설명 합니다. 소프트웨어 버전 ASP.NET 웹 페이지...
ms.author: riande
ms.date: 02/10/2014
ms.assetid: 2a2c1833-0bfe-4e2e-9cc0-341b52c7b121
msc.legacyurl: /web-pages/overview/testing-and-debugging/aspnet-web-pages-razor-troubleshooting-guide
msc.type: authoredcontent
ms.openlocfilehash: c27139a720decd34a4ab89e6f93e71c97d123b45
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41838734"
---
<a name="aspnet-web-pages-razor-troubleshooting-guide"></a><span data-ttu-id="0938d-104">ASP.NET 웹 페이지 (Razor) 문제 해결 가이드</span><span class="sxs-lookup"><span data-stu-id="0938d-104">ASP.NET Web Pages (Razor) Troubleshooting Guide</span></span>
====================
<span data-ttu-id="0938d-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="0938d-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="0938d-106">이 문서에서는 ASP.NET Web Pages (Razor) 및 몇 가지 제안 된 솔루션을 작업할 때 발생할 수 있는 문제를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-106">This article describes issues that you might have when working with ASP.NET Web Pages (Razor) and some suggested solutions.</span></span>
> 
> ## <a name="software-versions"></a><span data-ttu-id="0938d-107">소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="0938d-107">Software versions</span></span>
> 
> 
> - <span data-ttu-id="0938d-108">ASP.NET Web Pages (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="0938d-108">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="0938d-109">이 자습서는 또한 ASP.NET 웹 페이지 2 및 ASP.NET 웹 페이지 1.0과 함께 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-109">This tutorial also works with ASP.NET Web Pages 2 and ASP.NET Web Pages 1.0.</span></span>


<span data-ttu-id="0938d-110">이 항목에는 다음과 같은 단원이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-110">This topic contains the following sections:</span></span>

- [<span data-ttu-id="0938d-111">페이지를 실행 하는 문제</span><span class="sxs-lookup"><span data-stu-id="0938d-111">Issues with Running Pages</span></span>](#Issues_Running_.cshtml_Pages)
- [<span data-ttu-id="0938d-112">Razor 코드 문제</span><span class="sxs-lookup"><span data-stu-id="0938d-112">Issues with Razor Code</span></span>](#IssuesWithRazorCode)
- [<span data-ttu-id="0938d-113">멤버 자격 및 보안 문제</span><span class="sxs-lookup"><span data-stu-id="0938d-113">Issues with Security and Membership</span></span>](#membership)
- [<span data-ttu-id="0938d-114">전자 메일을 보내 문제</span><span class="sxs-lookup"><span data-stu-id="0938d-114">Issues with Sending Email</span></span>](#email)
- [<span data-ttu-id="0938d-115">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="0938d-115">Additional Resources</span></span>](#AdditionalResources)

<span data-ttu-id="0938d-116">일반적인 질문에 대 한 참조 [ASP.NET Web Pages (Razor) FAQ](https://go.microsoft.com/fwlink/?LinkId=253000)합니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-116">For general questions, see [ASP.NET Web Pages (Razor) FAQ](https://go.microsoft.com/fwlink/?LinkId=253000).</span></span>

<a id="Issues_Running_.cshtml_Pages"></a>
## <a name="issues-with-running-pages"></a><span data-ttu-id="0938d-117">페이지를 실행 하는 문제</span><span class="sxs-lookup"><span data-stu-id="0938d-117">Issues with Running Pages</span></span>

<span data-ttu-id="0938d-118">다양 한 문제를 방지할 수 있습니다 *.cshtml* 하 고 *.vbhtml* 올바르게 실행 하는 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-118">A variety of issues can prevent *.cshtml* and *.vbhtml* pages from running properly.</span></span> <span data-ttu-id="0938d-119">이 섹션에서는 일반적인 오류 메시지를 나열 하 고 원인입니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-119">This section lists common error messages and likely causes.</span></span>

### <a name="http-error-403---forbidden-access-is-denied"></a><span data-ttu-id="0938d-120">HTTP 오류 403-사용할 수 없음: 액세스가 거부 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-120">HTTP Error 403 - Forbidden: Access is denied</span></span>

<span data-ttu-id="0938d-121">*이 디렉터리 또는 사용자가 제공한 자격 증명을 사용 하 여 페이지를 볼 수 있는 권한이 없습니다.*</span><span class="sxs-lookup"><span data-stu-id="0938d-121">*You do not have permission to view this directory or page using the credentials that you supplied.*</span></span>

<span data-ttu-id="0938d-122">이 오류는 서버가 올바른 버전의.NET Framework를 실행 하지 않는 경우에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-122">This error can occur if the server is not running the correct version of the .NET Framework.</span></span> <span data-ttu-id="0938d-123">(로컬 또는 원격) 서버를 실행 하는 컴퓨터에 설치 된.NET Framework 4 이상 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-123">Make sure that the computer that's running the server (locally or remotely) has at least the .NET Framework 4 installed.</span></span> <span data-ttu-id="0938d-124">또한 응용 프로그램 자체 올바른 버전을 실행 하도록 구성 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-124">Also make sure that the application itself is configured to run the right version.</span></span>

<span data-ttu-id="0938d-125">WebMatrix에서 작업 하는 동안 로컬로이 문제를 표시 하는 경우 클릭 합니다 **사이트** 작업 영역 및 클릭 한 다음 트리 뷰에서 **설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-125">If you see this problem locally while working in WebMatrix, click the **Site** workspace, and then in the treeview click **Settings**.</span></span> <span data-ttu-id="0938d-126">에 **.NET Framework 버전 선택** 목록에서 선택 **(통합).NET 4**합니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-126">In the **Select .NET Framework Version** list, select **.NET 4 (Integrated)**.</span></span> <span data-ttu-id="0938d-127">이 버전은 이미 설정 된 경우 관리자 권한으로 WebMatrix를 실행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="0938d-127">If this version is already set, try running WebMatrix as an administrator.</span></span>

<span data-ttu-id="0938d-128">웹 사이트의 루트에 하나 이상 있는지 *.cshtml* 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-128">Make sure that the root of your website has at least one *.cshtml* file in it.</span></span>

<span data-ttu-id="0938d-129">웹 서버가 원격 서버에 있으면이 오류를 표시 하는 경우 서버 관리자에 게 문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-129">If you see this error when the web server is on a remote server, contact the server administrator.</span></span> <span data-ttu-id="0938d-130">서버에.NET Framework 4 또는 이상이 설치 되어 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-130">Make sure that the server has the .NET Framework 4 or later installed.</span></span> <span data-ttu-id="0938d-131">또한 응용 프로그램이.net Framework의 해당 버전을 사용 하도록 구성 된 응용 프로그램 풀에서 실행 되 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-131">Also make sure that the application is running in an application pool that's configured to use that version of the.NET Framework.</span></span>

<span data-ttu-id="0938d-132">서버에 대 한 제어를 사용 하는 경우 올바른 버전의.NET Framework 실행 중인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-132">If you have control over the server, make sure it's running the correct version of the .NET Framework.</span></span> <span data-ttu-id="0938d-133">사용할 수 있습니다 실행 하 여 설치를 복구 합니다 `aspnet_regiis -iru` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-133">You might also try repairing the installation by running the `aspnet_regiis -iru` command.</span></span> <span data-ttu-id="0938d-134">(예를 들어.NET Framework를 설치한 후 IIS를 설치한 경우 IIS 구성 되지 않습니다 올바르게 ASP.NET 페이지를 실행 합니다.) 자세한 내용은 [ASP.NET IIS 등록 도구 (Aspnet\_regiis.exe)](https://msdn.microsoft.com/library/k6h9cz8h(v=vs.100).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-134">(For example, if you install IIS after you install the .NET Framework, IIS will not be correctly configured to run ASP.NET pages.) For more information, see [ASP.NET IIS Registration Tool (Aspnet\_regiis.exe)](https://msdn.microsoft.com/library/k6h9cz8h(v=vs.100).aspx).</span></span>

### <a name="http-error-40314---forbidden"></a><span data-ttu-id="0938d-135">HTTP 오류 403.14-사용 권한 없음</span><span class="sxs-lookup"><span data-stu-id="0938d-135">HTTP Error 403.14 - Forbidden</span></span>

<span data-ttu-id="0938d-136">*웹 서버는이 디렉터리의 내용을 표시 하지 하도록 구성 됩니다.*</span><span class="sxs-lookup"><span data-stu-id="0938d-136">*The Web server is configured to not list the contents of this directory.*</span></span>

<span data-ttu-id="0938d-137">보호 되는 리소스를 요청 하는 경우이 오류가 발생할 수 있습니다 (같은 합니다 *Web.config* 파일) 또는 보호 되는 폴더에는 (같은 *앱\_데이터* 또는 *앱\_코드*).</span><span class="sxs-lookup"><span data-stu-id="0938d-137">This error can occur if you request a resource that's protected (like the *Web.config* file) or that's in a folder that's protected (like *App\_Data* or *App\_Code*).</span></span>

### <a name="http-error-40417---not-found"></a><span data-ttu-id="0938d-138">HTTP 오류 404.17-찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="0938d-138">HTTP Error 404.17 - Not Found</span></span>

<span data-ttu-id="0938d-139">*요청 된 콘텐츠를 스크립트로 및 정적 파일 처리기에서 처리 되지 않습니다.*</span><span class="sxs-lookup"><span data-stu-id="0938d-139">*The requested content appears to be script and will not be served by the static file handler.*</span></span>

<span data-ttu-id="0938d-140">.NET Framework 4를 사용 하도록 올바르게 구성 되지 않은 서버나 있어 나중에 코드를 인식 하지 않습니다 하는 경우이 오류가 발생할 수 있습니다 `@{ }` 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-140">This error can occur if the server is not configured correctly to use the .NET Framework 4 or later, and therefore does not recognize the code in `@{ }` blocks.</span></span> <span data-ttu-id="0938d-141">이전에 대 한 설명을 참조 하세요 *HTTP 오류 403-사용할 수 없음: 액세스가 거부 되었습니다.* 합니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-141">See the description earlier for *HTTP Error 403 - Forbidden: Access is denied*.</span></span>

### <a name="http-error-4047---not-found"></a><span data-ttu-id="0938d-142">HTTP 오류 404.7-찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="0938d-142">HTTP Error 404.7 - Not Found</span></span>

<span data-ttu-id="0938d-143">*요청 필터링 모듈 파일 확장명을 거부 하도록 구성 된*</span><span class="sxs-lookup"><span data-stu-id="0938d-143">*The request filtering module is configured to deny the file extension*</span></span>

<span data-ttu-id="0938d-144">이 오류가 발생할 수 있습니다 *.cshtml* 또는 *.vbhtml* 확장 서버에 명시적으로 차단 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-144">This error can occur if *.cshtml* or *.vbhtml* extensions have been explicitly blocked on the server.</span></span> <span data-ttu-id="0938d-145">이 문제의 증상 확장 이지만 포함 하는 Url 포함 되지 않은 경우 작동 하는 Url은 *.cshtml* 하거나 *.vbhtml* 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-145">A symptom of this problem is that URLs work when they do not include the extension, but URLs that include *.cshtml* or *.vbhtml* do not work.</span></span> <span data-ttu-id="0938d-146">가능한 솔루션을 다시 사이트의 확장을 사용 하도록 설정 하는 것 *Web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-146">A possible solution is to re-enable the extensions in the site's *Web.config* file.</span></span> <span data-ttu-id="0938d-147">다음 예제에서는 사용 하도록 설정 하는 방법을 보여 줍니다 합니다 *.cshtml* 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-147">The following example shows how to enable the *.cshtml* extension.</span></span>

[!code-xml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample1.xml?highlight=5-6)]

### <a name="http-error-4048---not-found"></a><span data-ttu-id="0938d-148">HTTP 오류 404.8-찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="0938d-148">HTTP Error 404.8 - Not Found</span></span>

<span data-ttu-id="0938d-149">*요청 필터링 모듈 hiddenSegment 섹션을 포함 하는 URL 경로 거부 하도록 구성 됩니다.*</span><span class="sxs-lookup"><span data-stu-id="0938d-149">*The request filtering module is configured to deny a path in the URL that contains a hiddenSegment section.*</span></span>

<span data-ttu-id="0938d-150">보호 되는 리소스를 요청 하는 경우이 오류가 발생할 수 있습니다 (같은 합니다 *Web.config* 파일) 또는 보호 되는 폴더에는 (같은 *앱\_데이터* 또는 *앱\_코드*).</span><span class="sxs-lookup"><span data-stu-id="0938d-150">This error can occur if you request a resource that's protected (like the *Web.config* file) or that's in a folder that's protected (like *App\_Data* or *App\_Code*).</span></span>

### <a name="this-type-of-page-is-not-served-server-error-in--application"></a><span data-ttu-id="0938d-151">이 형식의 페이지 ('/' 응용 프로그램의 오류 서버)를 제공 하지는</span><span class="sxs-lookup"><span data-stu-id="0938d-151">This type of page is not served (Server Error in '/' Application)</span></span>

<span data-ttu-id="0938d-152">HTTP 오류 404.17에 대 한 이전 설명을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="0938d-152">See the description earlier for HTTP Error 404.17.</span></span>

<a id="IssuesWithRazorCode"></a>
## <a name="issues-with-razor-code"></a><span data-ttu-id="0938d-153">Razor 코드 문제</span><span class="sxs-lookup"><span data-stu-id="0938d-153">Issues with Razor code</span></span>

### <a name="the-name-class-does-not-exist-in-the-current-context"></a><span data-ttu-id="0938d-154">이름 '*클래스*' 현재 컨텍스트에 존재 하지 않습니다</span><span class="sxs-lookup"><span data-stu-id="0938d-154">The name '*class*' does not exist in the current context</span></span>

<span data-ttu-id="0938d-155">종종이 오류를 표시 하는 이유는 `class` 참조 도우미를 하지만 도우미 설치 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-155">Often, a reason you see this error is that `class` references a helper, but the helper is not installed.</span></span> <span data-ttu-id="0938d-156">예를 들어 도우미를 사용 하려고 하지만 NuGet에서 패키지를 설치 하지 않은 경우이 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-156">For example, if you try to use a helper, but if you haven't installed the package from NuGet, you'll see this error.</span></span> <span data-ttu-id="0938d-157">찾기 및 설치 도우미를 WebMatrix의 갤러리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-157">Use the Gallery in WebMatrix to find and install the helper.</span></span>

<span data-ttu-id="0938d-158">경우에 도우미 설치 되어 있지만 페이지도 인식 하지 않는, 시도 추가 `using` 코드 문을 합니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-158">If the helper is installed, but the page still doesn't recognize it, try adding add a `using` statement to the code.</span></span> <span data-ttu-id="0938d-159">에 `using` 문, 참조 도우미를 포함 하는 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-159">In the `using` statement, reference the namespace that includes the helper.</span></span> <span data-ttu-id="0938d-160">예를 들어, ASP.NET 웹 도우미 패키지에 있는 기본 도우미에는 `System.Web.Helpers` 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-160">For example, the basic helpers that are in the ASP.NET Web Helpers package are in the `System.Web.Helpers` namespace.</span></span> <span data-ttu-id="0938d-161">도우미를 사용 하려는 페이지의 맨 위에 있는이 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-161">At the top of the page where you want to use the helper, add this line:</span></span>

`@using Microsoft.Web.Helpers;`

<a id="membership"></a>
## <a name="issues-with-security-and-membership"></a><span data-ttu-id="0938d-162">멤버 자격 및 보안 문제</span><span class="sxs-lookup"><span data-stu-id="0938d-162">Issues with Security and Membership</span></span>

<span data-ttu-id="0938d-163">ASP.NET Web Pages (Razor)에 기본 제공 보안 (멤버 자격) 시스템에 사용 하는, 경우에 다음과 같은 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-163">If you are using the built-in security (membership) system in ASP.NET Web Pages (Razor), you might encounter the following issues.</span></span>

### <a name="to-call-this-method-the-membershipprovider-property-must-be-an-instance-of-extendedmembershipprovider"></a><span data-ttu-id="0938d-164">이 메서드를 호출 하려면 "Membership.Provider" 속성 "ExtendedMembershipProvider" 인스턴스의 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-164">To call this method, the "Membership.Provider" property must be an instance of "ExtendedMembershipProvider"</span></span>

<span data-ttu-id="0938d-165">이 오류를 나타낼 수 없는 `AspNetSqlMembershipProvider` 클래스가 구성 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-165">This error can indicate that no `AspNetSqlMembershipProvider` class is configured.</span></span> <span data-ttu-id="0938d-166">(증상에는 사이트 로컬로 정상적으로 작동 하지만를 호스팅 공급자의 서버에 게시할 때이 오류를 throw 하는입니다.) 이 문제에 대 한 하나의 수정 사이트의 다음을 추가 하 여 간단한 멤버 자격을 명시적으로 사용 하는 것 *Web.config* 파일:</span><span class="sxs-lookup"><span data-stu-id="0938d-166">(A symptom is that the site works fine locally but throws this error when you publish it to a hosting provider's server.) One fix for this problem is to explicitly enable simple membership by adding the following to the site's *Web.config* file:</span></span>

[!code-xml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample2.xml?highlight=6)]

<a id="email"></a>
## <a name="issues-with-sending-email"></a><span data-ttu-id="0938d-167">전자 메일을 보내 문제</span><span class="sxs-lookup"><span data-stu-id="0938d-167">Issues with Sending Email</span></span>

<span data-ttu-id="0938d-168">전자 메일을 보내 문제 디버그 하기 어려울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-168">Problems with sending email can be challenging to debug.</span></span> <span data-ttu-id="0938d-169">문제를 초기에 SMTP 서버에 연결할 수 없습니다 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-169">An initial problem can be that you can't connect to the SMTP server.</span></span> <span data-ttu-id="0938d-170">연결이 성공 하면 ASP.NET 전달한 메시지 SMTP 서버에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-170">If the connection is successful, ASP.NET hands the message off to the SMTP server.</span></span> <span data-ttu-id="0938d-171">그러나 메시지 자체 SMTP 서버 전송 하지 못하도록 하는 문제가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-171">However, there can be problems with the message itself that prevents the SMTP server from sending it.</span></span>

<span data-ttu-id="0938d-172">응용 프로그램에서 성공적으로 전자 메일을 보내지 않으면 다음과 같이 하세요.</span><span class="sxs-lookup"><span data-stu-id="0938d-172">If your application does not successfully send email, try the following:</span></span>

- <span data-ttu-id="0938d-173">SMTP 서버 이름을 같습니다 종종 `smtp.provider.com` 또는 `smtp.provider.net`합니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-173">The SMTP server name is often something like `smtp.provider.com` or `smtp.provider.net`.</span></span> <span data-ttu-id="0938d-174">그러나 사이트를 호스팅 공급자에 게시할 경우 SMTP 서버 이름을 이때 않을 `localhost`합니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-174">However, if you publish your site to a hosting provider, the SMTP server name at that point might be `localhost`.</span></span> <span data-ttu-id="0938d-175">이 경우 게시 한 후 사이트 공급자의 서버에서 실행 되는 SMTP 서버 응용 프로그램의 관점에서 로컬 수 있기 때문에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-175">This situation occurs because after you've published and your site is running on the provider's server, the SMTP server might be local from the perspective of your application.</span></span> <span data-ttu-id="0938d-176">서버 이름에서이 변경 내용을 게시 하는 과정의 일부로 SMTP 서버 이름을 변경 해야 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-176">This change in server names might mean that you have to change the SMTP server name as part of your publishing process.</span></span>
- <span data-ttu-id="0938d-177">포트 번호는 일반적으로 25입니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-177">The port number is usually 25.</span></span> <span data-ttu-id="0938d-178">그러나 일부 공급자 포트를 사용 하 여 587 또는 일부 다른 포트가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-178">However, some providers require you to use port 587 or some other port.</span></span> <span data-ttu-id="0938d-179">어떤 포트 번호가 기대 사용 하 여 SMTP 서버 소유자를 사용 하 여 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-179">Check with the owner of the SMTP server what port number they expect you to use.</span></span>
- <span data-ttu-id="0938d-180">올바른 자격 증명을 사용 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-180">Make sure that you use the right credentials.</span></span> <span data-ttu-id="0938d-181">사이트를 호스팅 공급자을 게시 하는 경우 특별히 설정 된 공급자가 전자 메일에 대 한 자격 증명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-181">If you've published your site to a hosting provider, use the credentials that the provider has specifically indicated are for email.</span></span> <span data-ttu-id="0938d-182">이러한 자격 증명을 사용 하 여 게시 자격 증명에서 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-182">These credentials might be different from the credentials you use to publish.</span></span>
- <span data-ttu-id="0938d-183">경우에 따라 전혀 자격 증명이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-183">Sometimes you don't need credentials at all.</span></span> <span data-ttu-id="0938d-184">개인 ISP를 사용 하 여 전자 메일 보내는 경우 전자 메일 공급자 자격 증명 이미 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-184">If you're sending email by using your personal ISP, your email provider might already know your credentials.</span></span> <span data-ttu-id="0938d-185">를 게시 한 후에 로컬 컴퓨터에 테스트 하는 경우 다른 자격 증명을 사용 하는 것이 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-185">After you publish, you might need to use different credentials than when you test on your local computer.</span></span>
- <span data-ttu-id="0938d-186">전자 메일 공급자에서 암호화를 사용 하는 경우 설정 `WebMail.EnableSsl` 에 `true`입니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-186">If your email provider uses encryption, set `WebMail.EnableSsl` to `true`.</span></span>

<span data-ttu-id="0938d-187">전자 메일을 보내는 동안 오류가 발생 하는 경우 다음과 같이 표시 됩니다는 표준 ASP.NET 오류 메시지가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-187">If there is an error sending email, you might see a standard ASP.NET error message, which looks like this:</span></span>

![전자 메일을 사용 하 여 문제가 있으면 ASP.NET 오류 메시지](aspnet-web-pages-razor-troubleshooting-guide/_static/image1.png)

<span data-ttu-id="0938d-189">사용 하 여 전자 메일을 보내 문제를 디버깅할 수도 있습니다는 `try-catch` 다음 예제와 같이 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-189">You can also debug problems with sending email by using a `try-catch` block, as in the following example.</span></span> <span data-ttu-id="0938d-190">사용 하는 경우는 `try-catch` 블록, ASP.NET의 표준 오류 메시지를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-190">When you use a `try-catch` block, ASP.NET does not display its standard error messages.</span></span> <span data-ttu-id="0938d-191">대신 오류를 캡처할 수 있습니다는 `catch` 블록의 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-191">Instead, you can capture the error in the `catch` portion of the block.</span></span>

[!code-cshtml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample3.cshtml)]

<span data-ttu-id="0938d-192">에 대 한 적절 한 값으로 대체 `your-SMTP-server-name`등입니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-192">Substitute the appropriate values for `your-SMTP-server-name`, and so on.</span></span> <span data-ttu-id="0938d-193">이러한 방식으로 표시 될 수 있습니다 하는 오류 메시지 중 일부는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-193">Some of the error messages you might see this way include the following:</span></span>

- <span data-ttu-id="0938d-194">*메일을 보내지 못했습니다.*</span><span class="sxs-lookup"><span data-stu-id="0938d-194">*Failure sending mail.*</span></span>

    <span data-ttu-id="0938d-195">또는</span><span class="sxs-lookup"><span data-stu-id="0938d-195">-or-</span></span>

    <span data-ttu-id="0938d-196">*연결 된 파티 시간 또는 연결 된 호스트에서 응답 하지 못했기 때문에 실패 했습니다. 연결이 기간 후 올바르게 응답 하지 않아서 연결 시도가 실패 했습니다.*</span><span class="sxs-lookup"><span data-stu-id="0938d-196">*A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond*</span></span>

    <span data-ttu-id="0938d-197">이 오류는 일반적으로 응용 프로그램에서 SMTP 서버에 연결할 수 없습니다 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-197">This error usually means that the application could not connect to the SMTP server.</span></span> <span data-ttu-id="0938d-198">서버 이름을 확인 하 고 포트 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-198">Check the server name and port number.</span></span>
- <span data-ttu-id="0938d-199"><em>사서함을 사용할 수 없습니다. 서버 응답: 5.1.0 &lt; someuser@invaliddomain &gt; 거부 하는 보낸 사람: 잘못 된 보낸 사람 도메인</em></span><span class="sxs-lookup"><span data-stu-id="0938d-199"><em>Mailbox unavailable. The server response was: 5.1.0 &lt;someuser@invaliddomain&gt; sender rejected : invalid sender domain</em></span></span>

    <span data-ttu-id="0938d-200">이 메시지는 되었음을 나타낼 수 있습니다는 `From` 주소가 잘못 되었거나 누락 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-200">This message can indicate that the `From` address is not correct or is missing.</span></span>
- <span data-ttu-id="0938d-201">*지정된 된 문자열 전자 메일 주소 형식이 아닙니다.*</span><span class="sxs-lookup"><span data-stu-id="0938d-201">*The specified string is not in the form required for an email address.*</span></span>

    <span data-ttu-id="0938d-202">이 오류를 나타낼 수의 값을 `To` 또는 `From` 전자 메일 주소로 속성을 인식할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-202">This error might indicate that the value of the `To` or `From` properties are not recognized as email addresses.</span></span> <span data-ttu-id="0938d-203">(ASP.NET 한다는 같은 올바른 형식으로 유효한 전자 메일 주소 인지 확인할 수 없습니다 *name@domain.com*.)</span><span class="sxs-lookup"><span data-stu-id="0938d-203">(ASP.NET cannot check that the email address is valid, only that it's in the correct format, like *name@domain.com*.)</span></span>

> [!NOTE]
> <span data-ttu-id="0938d-204">오류를 표시 하는 태그를 제거 (`@errorMessage`) 페이지는 라이브 사이트에 게시 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-204">Remove the markup that displays the error (`@errorMessage`) before you publish the page to a live site.</span></span> <span data-ttu-id="0938d-205">사용자가 서버에서 얻을 수 있는 오류 메시지를 볼 수 있도록 좋은 방법이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="0938d-205">It's not a good idea to let users see error messages that you get from a server.</span></span>


<a id="AdditionalResources"></a>
## <a name="additional-resources"></a><span data-ttu-id="0938d-206">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="0938d-206">Additional Resources</span></span>

[<span data-ttu-id="0938d-207">ASP.NET 웹 페이지(Razor) FAQ</span><span class="sxs-lookup"><span data-stu-id="0938d-207">ASP.NET Web Pages (Razor) FAQ</span></span>](https://go.microsoft.com/fwlink/?LinkId=253000)

<span data-ttu-id="0938d-208">[WebMatrix 및 ASP.NET Web Pages](https://forums.asp.net/1224.aspx/1?WebMatrix) ASP.NET 웹 사이트에 대 한 포럼</span><span class="sxs-lookup"><span data-stu-id="0938d-208">[WebMatrix and ASP.NET Web Pages](https://forums.asp.net/1224.aspx/1?WebMatrix) forum on the ASP.NET website</span></span>
