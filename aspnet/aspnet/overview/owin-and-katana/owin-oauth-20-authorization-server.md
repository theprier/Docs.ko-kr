---
uid: aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
title: OWIN OAuth 2.0 권한 부여 서버 | Microsoft Docs
author: hongyes
description: 이 자습서에서 OAuth OWIN 미들웨어를 사용 하 여 OAuth 2.0 권한 부여 서버를 구현 하는 방법을 안내 합니다. 이 고급 자습서는 해당만 outlin 됩니다...
ms.author: aspnetcontent
ms.date: 03/20/2014
ms.assetid: 20acee16-c70c-41e9-b38f-92bfcf9a4c1c
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
msc.type: authoredcontent
ms.openlocfilehash: e3b5b37b4f22f3c59d3c1f4043e9b52e46a8926b
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37828421"
---
<a name="owin-oauth-20-authorization-server"></a><span data-ttu-id="8f876-104">OWIN OAuth 2.0 권한 부여 서버</span><span class="sxs-lookup"><span data-stu-id="8f876-104">OWIN OAuth 2.0 Authorization Server</span></span>
====================
<span data-ttu-id="8f876-105">하 여 [Hongye Sun](https://github.com/hongyes)하십시오 [Praburaj Thiagarajan](https://github.com/Praburaj), [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="8f876-105">by [Hongye Sun](https://github.com/hongyes), [Praburaj Thiagarajan](https://github.com/Praburaj), [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="8f876-106">이 자습서에서 OAuth OWIN 미들웨어를 사용 하 여 OAuth 2.0 권한 부여 서버를 구현 하는 방법을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-106">This tutorial will guide you on how to implement an OAuth 2.0 Authorization Server using OWIN OAuth middleware.</span></span> <span data-ttu-id="8f876-107">만 OWIN OAuth 2.0 권한 부여 서버를 만드는 단계를 간략하게 설명 하는 고급 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-107">This is an advanced tutorial that only outlines the steps to create an OWIN OAuth 2.0 Authorization Server.</span></span> <span data-ttu-id="8f876-108">이것이 단계별 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-108">This is not a step by step tutorial.</span></span> <span data-ttu-id="8f876-109">[샘플 코드 다운로드](https://code.msdn.microsoft.com/OWIN-OAuth-20-Authorization-ba2b8783/file/114932/1/AuthorizationServer.zip)합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-109">[Download the sample code](https://code.msdn.microsoft.com/OWIN-OAuth-20-Authorization-ba2b8783/file/114932/1/AuthorizationServer.zip).</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="8f876-110">이 개요는 안전한 프로덕션 앱을 만드는 데 사용할 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-110">This outline should not be intended to be used for creating a secure production app.</span></span> <span data-ttu-id="8f876-111">이 자습서는 OAuth OWIN 미들웨어를 사용 하 여 OAuth 2.0 권한 부여 서버를 구현 하는 방법에만 개요를 제공 하도록 작성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-111">This tutorial is intended to provide only an outline on how to implement an OAuth 2.0 Authorization Server using OWIN OAuth middleware.</span></span>
> 
> 
> ## <a name="software-versions"></a><span data-ttu-id="8f876-112">소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="8f876-112">Software versions</span></span>
> 
> | <span data-ttu-id="8f876-113">**자습서에 표시**</span><span class="sxs-lookup"><span data-stu-id="8f876-113">**Shown in the tutorial**</span></span> | <span data-ttu-id="8f876-114">**역시**</span><span class="sxs-lookup"><span data-stu-id="8f876-114">**Also works with**</span></span> |
> | --- | --- |
> | <span data-ttu-id="8f876-115">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="8f876-115">Windows 8.1</span></span> | <span data-ttu-id="8f876-116">Windows 8, Windows 7</span><span class="sxs-lookup"><span data-stu-id="8f876-116">Windows 8, Windows 7</span></span> |
> | [<span data-ttu-id="8f876-117">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="8f876-117">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads) | <span data-ttu-id="8f876-118">[Visual Studio 2013 Express for Desktop](https://www.microsoft.com/visualstudio/eng/2013-downloads#d-2013-express)합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-118">[Visual Studio 2013 Express for Desktop](https://www.microsoft.com/visualstudio/eng/2013-downloads#d-2013-express).</span></span> <span data-ttu-id="8f876-119">최신 업데이트를 사용 하 여 visual Studio 2012에는 작동 하지만 자습서를 사용 하 여 테스트 되지 않았습니다 하 고 일부 메뉴 선택 및 대화 상자는 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-119">Visual Studio 2012 with the latest update should work, but the tutorial has not been tested with it, and some menu selections and dialog boxes are different.</span></span> |
> | <span data-ttu-id="8f876-120">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="8f876-120">.NET 4.5</span></span> |  |
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="8f876-121">질문이 나 의견이 있으면</span><span class="sxs-lookup"><span data-stu-id="8f876-121">Questions and Comments</span></span>
> 
> <span data-ttu-id="8f876-122">에 자습서로 직접 관련 되지 않은 질문이 있는 경우에서 게시할 수 있습니다 [Katana 프로젝트 github](https://github.com/aspnet/AspNetKatana/)합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-122">If you have questions that are not directly related to the tutorial, you can post them at [Katana Project on GitHub](https://github.com/aspnet/AspNetKatana/).</span></span> <span data-ttu-id="8f876-123">자습서 자체에 대 한 의견 및 질문에 대 한 페이지의 맨 아래에서 설명 섹션을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-123">For questions and comments regarding the tutorial itself, see the comments section at the bottom of the page.</span></span>


<span data-ttu-id="8f876-124">합니다 [OAuth 2.0 framework](http://tools.ietf.org/html/rfc6749) HTTP 서비스에 대 한 제한 된 권한을 얻지 타사 앱을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-124">The [OAuth 2.0 framework](http://tools.ietf.org/html/rfc6749) enables a third-party app to obtain limited access to an HTTP service.</span></span> <span data-ttu-id="8f876-125">클라이언트 리소스 소유자의 자격 증명을 사용 하 여 보호 된 리소스 액세스를 대신 액세스 토큰을 가져옵니다 (문자열인는 특정 범위, 수명 및 다른 액세스 특성을 나타내는).</span><span class="sxs-lookup"><span data-stu-id="8f876-125">Instead of using the resource owner's credentials to access a protected resource, the client obtains an access token (which is a string denoting a specific scope, lifetime, and other access attributes).</span></span> <span data-ttu-id="8f876-126">액세스 토큰 리소스 소유자의 승인이 있는 타사 클라이언트는 권한 부여 서버에서 발급 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-126">Access tokens are issued to third-party clients by an authorization server with the approval of the resource owner.</span></span>

<span data-ttu-id="8f876-127">이 자습서에는 다음 같은 내용을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-127">This tutorial will cover:</span></span>

- <span data-ttu-id="8f876-128">네 가지 권한 부여를 지원 하기 위해 권한 부여 서버를 만드는 방법 부여 유형 및 새로 고침 토큰:</span><span class="sxs-lookup"><span data-stu-id="8f876-128">How to create an authorization server to support four authorization grant types and refresh tokens:</span></span>
    - <span data-ttu-id="8f876-129">인증 코드 부여</span><span class="sxs-lookup"><span data-stu-id="8f876-129">Authorization code grant</span></span>
    - <span data-ttu-id="8f876-130">암시적 권한 부여</span><span class="sxs-lookup"><span data-stu-id="8f876-130">Implicit Grant</span></span>
    - <span data-ttu-id="8f876-131">리소스 소유자 암호 자격 증명을 권한 부여</span><span class="sxs-lookup"><span data-stu-id="8f876-131">Resource Owner Password Credentials Grant</span></span>
    - <span data-ttu-id="8f876-132">클라이언트 권한 부여 자격 증명</span><span class="sxs-lookup"><span data-stu-id="8f876-132">Client Credentials Grant</span></span>
- <span data-ttu-id="8f876-133">액세스 토큰으로 보호 되는 리소스 서버를 만드는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-133">Creating a resource server which is protected by an access token.</span></span>
- <span data-ttu-id="8f876-134">OAuth 2.0 클라이언트를 만드는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-134">Creating OAuth 2.0 clients.</span></span>

<a id="prerequisites"></a>
## <a name="prerequisites"></a><span data-ttu-id="8f876-135">전제 조건</span><span class="sxs-lookup"><span data-stu-id="8f876-135">Prerequisites</span></span>

- <span data-ttu-id="8f876-136">[Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-editions) 또는 무료 [Visual Studio Express 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-express)에 표시 된 대로 **소프트웨어 버전** 페이지의 맨 위에 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-136">[Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-editions) or the free [Visual Studio Express 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-express), as indicated in **Software Versions** at the top of the page.</span></span>
- <span data-ttu-id="8f876-137">OWIN 익숙해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-137">Familiarity with OWIN.</span></span> <span data-ttu-id="8f876-138">참조 [Katana 프로젝트를 시작 하기](https://msdn.microsoft.com/magazine/dn451439.aspx) 하 고 [OWIN 및 Katana의 새로운 기능](index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-138">See [Getting Started with the Katana Project](https://msdn.microsoft.com/magazine/dn451439.aspx) and [What's new in OWIN and Katana](index.md).</span></span>
- <span data-ttu-id="8f876-139">사용 경험 [OAuth](http://tools.ietf.org/html/rfc6749) 용어를 포함 하 여 [역할](http://tools.ietf.org/html/rfc6749#section-1.1)를 [프로토콜 흐름](http://tools.ietf.org/html/rfc6749#section-1.2), 및 [권한 부여](http://tools.ietf.org/html/rfc6749#section-1.3)합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-139">Familiarity with [OAuth](http://tools.ietf.org/html/rfc6749) terminology, including [Roles](http://tools.ietf.org/html/rfc6749#section-1.1), [Protocol Flow](http://tools.ietf.org/html/rfc6749#section-1.2), and [Authorization Grant](http://tools.ietf.org/html/rfc6749#section-1.3).</span></span> <span data-ttu-id="8f876-140">[OAuth 2.0 소개](http://tools.ietf.org/html/rfc6749#section-1) 잘 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-140">[OAuth 2.0 introduction](http://tools.ietf.org/html/rfc6749#section-1) provides a good introduction.</span></span>

## <a name="create-an-authorization-server"></a><span data-ttu-id="8f876-141">권한 부여 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="8f876-141">Create an Authorization Server</span></span>

<span data-ttu-id="8f876-142">이 자습서에서는 것은 거의 대략적으로 사용 하는 방법 [OWIN](https://msdn.microsoft.com/magazine/dn451439.aspx) 및 ASP.NET MVC 권한 부여 서버를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-142">In this tutorial, we will roughly sketch out how to use [OWIN](https://msdn.microsoft.com/magazine/dn451439.aspx) and ASP.NET MVC to create an authorization server.</span></span> <span data-ttu-id="8f876-143">이 자습서는 각 단계를 포함 하지 않는 곧 완료 된 샘플을 다운로드를 제공 하기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-143">We hope to soon provide a download for the completed sample, as this tutorial does not include each step.</span></span> <span data-ttu-id="8f876-144">먼저 빈 웹 앱을 만듭니다 *AuthorizationServer* 하 고 다음 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-144">First, create an empty web app named *AuthorizationServer* and install the following packages:</span></span>

- <span data-ttu-id="8f876-145">Microsoft.AspNet.Mvc</span><span class="sxs-lookup"><span data-stu-id="8f876-145">Microsoft.AspNet.Mvc</span></span>
- <span data-ttu-id="8f876-146">Microsoft.Owin.Host.SystemWeb</span><span class="sxs-lookup"><span data-stu-id="8f876-146">Microsoft.Owin.Host.SystemWeb</span></span>
- <span data-ttu-id="8f876-147">Microsoft.Owin.Security.OAuth</span><span class="sxs-lookup"><span data-stu-id="8f876-147">Microsoft.Owin.Security.OAuth</span></span>
- <span data-ttu-id="8f876-148">Microsoft.Owin.Security.Cookies</span><span class="sxs-lookup"><span data-stu-id="8f876-148">Microsoft.Owin.Security.Cookies</span></span>
- <span data-ttu-id="8f876-149">Microsoft.Owin.Security.Google (또는 다른 모든 소셜 로그인 Microsoft.Owin.Security.Facebook 같은 패키지)</span><span class="sxs-lookup"><span data-stu-id="8f876-149">Microsoft.Owin.Security.Google (Or any other social login package such as Microsoft.Owin.Security.Facebook)</span></span>

<span data-ttu-id="8f876-150">추가 된 [OWIN Startup 클래스](owin-startup-class-detection.md) 라는 프로젝트 루트 폴더 아래의 *시작*합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-150">Add an [OWIN Startup class](owin-startup-class-detection.md) under the project root folder named *Startup*.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample1.cs?highlight=8)]

<span data-ttu-id="8f876-151">만들기는 *앱\_시작* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-151">Create an *App\_Start* folder.</span></span> <span data-ttu-id="8f876-152">선택 된 *앱\_시작* 폴더 및 다운로드 가능한 버전의 추가 하려면 Shift + Alt + A를 사용 하 여 합니다 *AuthorizationServer\App\_Start\Startup.Auth.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-152">Select the *App\_Start* folder and use Shift+Alt+A to add the downloaded version of the *AuthorizationServer\App\_Start\Startup.Auth.cs* file.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample2.cs)]

<span data-ttu-id="8f876-153">위의 코드는 응용 프로그램/외부 로그인을 계정을 관리 하는 자체 권한 부여 서버에서 사용 되는 쿠키 및 Google 인증을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-153">The code above enables application/external sign in cookies and Google authentication, which are used by authorization server itself to manage accounts.</span></span>

<span data-ttu-id="8f876-154">`UseOAuthAuthorizationServer` 확장 메서드는 권한 부여 서버를 설정 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-154">The `UseOAuthAuthorizationServer` extension method is to setup the authorization server.</span></span> <span data-ttu-id="8f876-155">설치 옵션을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-155">The setup options are:</span></span>

- <span data-ttu-id="8f876-156">`AuthorizeEndpointPath`: 요청 경로 클라이언트 응용 프로그램 사용자를 가져오기 위해 사용자-에이전트를 리디렉션하는 동의 코드 또는 토큰을 발급 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-156">`AuthorizeEndpointPath`: The request path where client applications will redirect the user-agent in order to obtain the users consent to issue a token or code.</span></span> <span data-ttu-id="8f876-157">예를 들어 선행 슬래시로 시작 해야 합니다 "`/Authorize`"입니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-157">It must begin with a leading slash, for example, "`/Authorize`".</span></span>
- <span data-ttu-id="8f876-158">`TokenEndpointPath`: 요청 경로 클라이언트 응용 프로그램이 액세스 토큰을 가져오려면 직접 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-158">`TokenEndpointPath`: The request path client applications directly communicate to obtain the access token.</span></span> <span data-ttu-id="8f876-159">"/Token" 처럼 선행 슬래시로 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-159">It must begin with a leading slash, like "/Token".</span></span> <span data-ttu-id="8f876-160">클라이언트는 발급 된 경우는 [클라이언트\_비밀](http://tools.ietf.org/html/rfc6749#appendix-A.2),이 끝점에 제공 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-160">If the client is issued a [client\_secret](http://tools.ietf.org/html/rfc6749#appendix-A.2), it must be provided to this endpoint.</span></span>
- <span data-ttu-id="8f876-161">`ApplicationCanDisplayErrors`:로 설정 합니다. `true` 웹 응용 프로그램에서 클라이언트 유효성 검사 오류에 대 한 사용자 지정 오류 페이지를 생성 하려는 경우 `/Authorize` 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-161">`ApplicationCanDisplayErrors`: Set to `true` if the web application wants to generate a custom error page for the client validation errors on `/Authorize` endpoint.</span></span> <span data-ttu-id="8f876-162">예를 들어 클라이언트 응용 프로그램에 다시 브라우저 리디렉션되지 않습니다 하는 경우에만 필요 경우 합니다 `client_id` 또는 `redirect_uri` 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-162">This is only needed for cases where the browser is not redirected back to the client application, for example, when the `client_id` or `redirect_uri` are incorrect.</span></span> <span data-ttu-id="8f876-163">`/Authorize` 끝점 "oauth 볼 수 있어야 합니다. 오류 ","oauth입니다. ErrorDescription"및"oauth입니다. ErrorUri"속성은 OWIN 환경에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-163">The `/Authorize` endpoint should expect to see the "oauth.Error", "oauth.ErrorDescription", and "oauth.ErrorUri" properties are added to the OWIN environment.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="8f876-164">그렇지 않은 경우 true, 권한 부여 서버가 반환 하는 오류 세부 정보를 사용 하 여 기본 오류 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-164">If not true, the authorization server will return a default error page with the error details.</span></span>
- <span data-ttu-id="8f876-165">`AllowInsecureHttp`: 권한 부여 및 토큰 요청이 HTTP URI 주소에 도착 하 고 들어오는 수 있도록 허용 True를 `redirect_uri` 요청 매개 변수를 HTTP URI 주소에 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-165">`AllowInsecureHttp`: True to allow authorize and token requests to arrive on HTTP URI addresses, and to allow incoming `redirect_uri` authorize request parameters to have HTTP URI addresses.</span></span> 

    > [!WARNING]
    > <span data-ttu-id="8f876-166">개발 용도로 이것이 보안-입니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-166">Security - This is for development only.</span></span>
- <span data-ttu-id="8f876-167">`Provider`Authorization Server 미들웨어에서 발생 하는 프로세스 이벤트를 응용 프로그램을 제공한: 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-167">`Provider`: The object provided by the application to process events raised by the Authorization Server middleware.</span></span> <span data-ttu-id="8f876-168">응용 프로그램 인터페이스를 완전히 구현 하거나의 인스턴스를 만들 수 있습니다 `OAuthAuthorizationServerProvider` 이 서버는 지원 된 OAuth 흐름에 대 한 필요한 대리자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-168">The application may implement the interface fully, or it may create an instance of `OAuthAuthorizationServerProvider` and assign delegates necessary for the OAuth flows this server supports.</span></span>
- <span data-ttu-id="8f876-169">`AuthorizationCodeProvider`: 클라이언트 응용 프로그램에 반환할 단일 사용 권한 부여 코드를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-169">`AuthorizationCodeProvider`: Produces a single-use authorization code to return to the client application.</span></span> <span data-ttu-id="8f876-170">OAuth 서버의 수에 대 한 응용 프로그램을 보호할 **해야 합니다** 에 대 한 인스턴스를 제공 `AuthorizationCodeProvider` 하 여 토큰을 생성 하는 위치를 `OnCreate/OnCreateAsync` 이벤트는 한 번만 호출에 대 한 유효한 것으로 간주 `OnReceive/OnReceiveAsync`합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-170">For the OAuth server to be secure the application **MUST** provide an instance for `AuthorizationCodeProvider` where the token produced by the `OnCreate/OnCreateAsync` event is considered valid for only one call to `OnReceive/OnReceiveAsync`.</span></span>
- <span data-ttu-id="8f876-171">`RefreshTokenProvider`: 필요한 경우 새 액세스 토큰을 생성 하기 위해 사용할 수 있는 새로 고침 토큰을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-171">`RefreshTokenProvider`: Produces a refresh token which may be used to produce a new access token when needed.</span></span> <span data-ttu-id="8f876-172">제공 되지 권한 부여 서버는 반환 하지 않습니다에서 새로 고침 토큰을 `/Token` 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-172">If not provided the authorization server will not return refresh tokens from the `/Token` endpoint.</span></span>

## <a name="account-management"></a><span data-ttu-id="8f876-173">계정 관리</span><span class="sxs-lookup"><span data-stu-id="8f876-173">Account Management</span></span>

<span data-ttu-id="8f876-174">OAuth는 사용자 계정 정보를 관리 하는 방법 또는 위치를 고려 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-174">OAuth doesn't care where or how you manage your user account information.</span></span> <span data-ttu-id="8f876-175">있기 [ASP.NET Id](../../../identity/index.md) 담당 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-175">It's [ASP.NET Identity](../../../identity/index.md) which is responsible for it.</span></span> <span data-ttu-id="8f876-176">이 자습서에서는 계정 관리 코드를 단순화 하 고 해당 사용자는 OWIN 쿠키 미들웨어를 사용 하 여 로그인 할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-176">In this tutorial, we will simplify the account management code and just make sure that user can login using OWIN cookie middleware.</span></span> <span data-ttu-id="8f876-177">다음은 대 한 간소화 된 샘플 코드는 `AccountController`:</span><span class="sxs-lookup"><span data-stu-id="8f876-177">Here is the simplified sample code for the `AccountController`:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample3.cs)]

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample4.cs?highlight=1)]

<span data-ttu-id="8f876-178">`ValidateClientRedirectUri` 등록 된 리디렉션 URL 사용 하 여 클라이언트의 유효성을 검사 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-178">`ValidateClientRedirectUri` is used to validate the client with its registered redirect URL.</span></span> <span data-ttu-id="8f876-179">`ValidateClientAuthentication` 기본 구성표 헤더 및 클라이언트의 자격 증명을 가져오지 폼 본문을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-179">`ValidateClientAuthentication` checks the basic scheme header and form body to get the client's credentials.</span></span>

<span data-ttu-id="8f876-180">로그인 페이지는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-180">The login page is shown below:</span></span>

![](owin-oauth-20-authorization-server/_static/image1.png)

<span data-ttu-id="8f876-181">IETF의 OAuth 2를 검토 [권한 부여 코드 부여](http://tools.ietf.org/html/rfc6749#section-4.1) 이제 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-181">Review the IETF's OAuth 2 [Authorization Code Grant](http://tools.ietf.org/html/rfc6749#section-4.1) section now.</span></span> 

<span data-ttu-id="8f876-182">**공급자** (아래 표에서)은 [OAuthAuthorizationServerOptions](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserveroptions(v=vs.111).aspx)합니다. 공급자 형식의 `OAuthAuthorizationServerProvider`, 모든 OAuth 서버 이벤트를 포함 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-182">**Provider** (in the table below) is [OAuthAuthorizationServerOptions](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserveroptions(v=vs.111).aspx).Provider, which is of type `OAuthAuthorizationServerProvider`, which contains all OAuth server events.</span></span> 

| <span data-ttu-id="8f876-183">인증 코드 부여 섹션에서 흐름 단계</span><span class="sxs-lookup"><span data-stu-id="8f876-183">Flow steps from Authorization Code Grant section</span></span> | <span data-ttu-id="8f876-184">샘플 다운로드에는 이러한 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-184">Sample download performs these steps with:</span></span> |
| --- | --- |
|  |  |
| <span data-ttu-id="8f876-185">(A) 클라이언트는 리소스 소유자의 사용자-에이전트 권한 부여 끝점에 연결 하 여 흐름을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-185">(A) The client initiates the flow by directing the resource owner's user-agent to the authorization endpoint.</span></span> <span data-ttu-id="8f876-186">클라이언트는 클라이언트 식별자, 요청 된 범위, 로컬 상태 및를 보낼 리디렉션 URI를 하는 권한 부여 서버는 user-agent 액세스는 부여 되거나 거부 되 면 다시 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-186">The client includes its client identifier, requested scope, local state, and a redirection URI to which the authorization server will send the user-agent back once access is granted (or denied).</span></span> | <span data-ttu-id="8f876-187">Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint</span><span class="sxs-lookup"><span data-stu-id="8f876-187">Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint</span></span> |
|  |  |
| <span data-ttu-id="8f876-188">(B) 권한 부여 서버 (사용자 에이전트)를 통해 리소스 소유자를 인증 하 고 리소스 소유자 부여 클라이언트의 액세스 요청을 거부 하는지 여부를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-188">(B) The authorization server authenticates the resource owner (via the user-agent) and establishes whether the resource owner grants or denies the client's access request.</span></span> | <span data-ttu-id="8f876-189">**&lt;사용자 액세스 권한을 부여 하는 경우&gt;**  Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint AuthorizationCodeProvider.CreateAsync</span><span class="sxs-lookup"><span data-stu-id="8f876-189">**&lt;If user grants access&gt;** Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint AuthorizationCodeProvider.CreateAsync</span></span> |
|  |  |
| <span data-ttu-id="8f876-190">(권한 부여 서버 user-agent를 다시 리디렉션합니다 리디렉션을 제공 하는 URI를 사용 하는 클라이언트 액세스를 부여 C) 리소스 소유자를 가정 합니다. 이전 (요청 또는 클라이언트 등록 중).</span><span class="sxs-lookup"><span data-stu-id="8f876-190">(C) Assuming the resource owner grants access, the authorization server redirects the user-agent back to the client using the redirection URI provided earlier (in the request or during client registration).</span></span> <span data-ttu-id="8f876-191">...</span><span class="sxs-lookup"><span data-stu-id="8f876-191">...</span></span> |  |
|  |  |
| <span data-ttu-id="8f876-192">(D) 클라이언트를 사용 하면 권한 부여 서버의 토큰 끝점에서 액세스 토큰을 요청 하는 이전 단계에서 받은 인증 코드를 포함 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-192">(D) The client requests an access token from the authorization server's token endpoint by including the authorization code received in the previous step.</span></span> <span data-ttu-id="8f876-193">요청할 때 클라이언트는 권한 부여 서버를 사용 하 여 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-193">When making the request, the client authenticates with the authorization server.</span></span> <span data-ttu-id="8f876-194">클라이언트는 리디렉션 URI가 확인에 대 한 권한 부여 코드를 가져오는 데를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-194">The client includes the redirection URI used to obtain the authorization code for verification.</span></span> | <span data-ttu-id="8f876-195">Provider.MatchEndpoint Provider.ValidateClientAuthentication AuthorizationCodeProvider.ReceiveAsync Provider.ValidateTokenRequest Provider.GrantAuthorizationCode Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync</span><span class="sxs-lookup"><span data-stu-id="8f876-195">Provider.MatchEndpoint Provider.ValidateClientAuthentication AuthorizationCodeProvider.ReceiveAsync Provider.ValidateTokenRequest Provider.GrantAuthorizationCode Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync</span></span> |

<span data-ttu-id="8f876-196">에 대 한 샘플 구현을 `AuthorizationCodeProvider.CreateAsync` 고 `ReceiveAsync` 생성 및 권한 부여 코드의 유효성 검사를 제어 하려면 아래에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-196">A sample implementation for `AuthorizationCodeProvider.CreateAsync` and `ReceiveAsync` to control the creation and validation of authorization code is shown below.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample5.cs)]

<span data-ttu-id="8f876-197">위의 코드는 메모리 내 동시 사전을 사용 하 여 코드 및 id 티켓을 저장 하 고 코드를 받은 후 id를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-197">The code above uses an in-memory concurrent dictionary to store the code and identity ticket and restore the identity after receiving the code.</span></span> <span data-ttu-id="8f876-198">실제 응용 프로그램에서는 영구 데이터 저장소에서 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-198">In a real application, it would be replaced by a persistent data store.</span></span> <span data-ttu-id="8f876-199">권한 부여 끝점은 클라이언트에 게 액세스 권한을 부여할 리소스 소유자입니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-199">The authorization endpoint is for the resource owner to grant access to the client.</span></span> <span data-ttu-id="8f876-200">일반적으로 사용자 인터페이스를 사용자가 단추를 클릭 하 고 권한 부여를 확인 하도록 허용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-200">Usually, it needs a user interface to allow the user to click a button and confirm the grant.</span></span> <span data-ttu-id="8f876-201">OAuth OWIN 미들웨어는 권한 부여 끝점을 처리 하는 응용 프로그램 코드를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-201">OWIN OAuth middleware allows application code to handle the authorization endpoint.</span></span> <span data-ttu-id="8f876-202">샘플 앱을 사용 하 여 호출 하는 MVC 컨트롤러 `OAuthController` 를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-202">In our sample app, we use an MVC controller called `OAuthController` to handle it.</span></span> <span data-ttu-id="8f876-203">샘플 구현은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-203">Here is the sample implementation:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample6.cs?highlight=15)]

<span data-ttu-id="8f876-204">`Authorize` 작업 하는 경우 사용자가 로그인 권한 부여 서버를 먼저 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-204">The `Authorize` action will first check if the user has logged in to the authorization server.</span></span> <span data-ttu-id="8f876-205">그렇지 않은 경우 인증 미들웨어는 "Application" 쿠키를 사용 하 여 인증 하려면 호출자에 게 문제 및 로그인 페이지로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-205">If not, the authentication middleware challenges the caller to authenticate using the "Application" cookie and redirects to the login page.</span></span> <span data-ttu-id="8f876-206">(위의 강조 표시 된 코드 참조). 사용자가 로그인 하는 경우 아래와 같이 Authorize 뷰를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-206">(See highlighted code above.) If user has logged in, it will render the Authorize view, as shown below:</span></span>

![](owin-oauth-20-authorization-server/_static/image2.png)

<span data-ttu-id="8f876-207">경우는 **권한 부여** 단추를 선택 합니다 `Authorize` 작업에서 새 "Bearer" identity와 로그인 하기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-207">If the **Grant** button is selected, the `Authorize` action will create a new "Bearer" identity and sign in with it.</span></span> <span data-ttu-id="8f876-208">권한 부여 서버를 전달자 토큰을 생성 하 고 JSON 페이로드를 사용 하 여 클라이언트로 다시 보낼를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-208">It will trigger the authorization server to generate a bearer token and send it back to the client with JSON payload.</span></span> 

### <a name="implicit-grant"></a><span data-ttu-id="8f876-209">암시적 권한 부여</span><span class="sxs-lookup"><span data-stu-id="8f876-209">Implicit Grant</span></span>

<span data-ttu-id="8f876-210">IETF의 OAuth 2를 참조 하십시오 [암시적 권한 부여](http://tools.ietf.org/html/rfc6749#section-4.2) 이제 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-210">Refer to the IETF's OAuth 2 [Implicit Grant](http://tools.ietf.org/html/rfc6749#section-4.2) section now.</span></span>

 <span data-ttu-id="8f876-211">합니다 [암시적 권한 부여](http://tools.ietf.org/html/rfc6749#section-4.2) 그림 4에 표시 된 흐름은 흐름 및 미들웨어는 OWIN OAuth 매핑을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-211">The [Implicit Grant](http://tools.ietf.org/html/rfc6749#section-4.2) flow shown in Figure 4 is the flow and mapping which the OWIN OAuth middleware follows.</span></span>  

| <span data-ttu-id="8f876-212">암시적 권한 부여 섹션에서 흐름 단계</span><span class="sxs-lookup"><span data-stu-id="8f876-212">Flow steps from Implicit Grant section</span></span> | <span data-ttu-id="8f876-213">샘플 다운로드에는 이러한 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-213">Sample download performs these steps with:</span></span> |
| --- | --- |
|  |  |
| <span data-ttu-id="8f876-214">(A) 클라이언트는 리소스 소유자의 사용자-에이전트 권한 부여 끝점에 연결 하 여 흐름을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-214">(A) The client initiates the flow by directing the resource owner's user-agent to the authorization endpoint.</span></span> <span data-ttu-id="8f876-215">클라이언트는 클라이언트 식별자, 요청 된 범위, 로컬 상태 및를 보낼 리디렉션 URI를 하는 권한 부여 서버는 user-agent 액세스는 부여 되거나 거부 되 면 다시 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-215">The client includes its client identifier, requested scope, local state, and a redirection URI to which the authorization server will send the user-agent back once access is granted (or denied).</span></span> | <span data-ttu-id="8f876-216">Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint</span><span class="sxs-lookup"><span data-stu-id="8f876-216">Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint</span></span> |
|  |  |
| <span data-ttu-id="8f876-217">(B) 권한 부여 서버 (사용자 에이전트)를 통해 리소스 소유자를 인증 하 고 리소스 소유자 부여 클라이언트의 액세스 요청을 거부 하는지 여부를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-217">(B) The authorization server authenticates the resource owner (via the user-agent) and establishes whether the resource owner grants or denies the client's access request.</span></span> | <span data-ttu-id="8f876-218">**&lt;사용자 액세스 권한을 부여 하는 경우&gt;**  Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint AuthorizationCodeProvider.CreateAsync</span><span class="sxs-lookup"><span data-stu-id="8f876-218">**&lt;If user grants access&gt;** Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint AuthorizationCodeProvider.CreateAsync</span></span> |
|  |  |
| <span data-ttu-id="8f876-219">(권한 부여 서버 user-agent를 다시 리디렉션합니다 리디렉션을 제공 하는 URI를 사용 하는 클라이언트 액세스를 부여 C) 리소스 소유자를 가정 합니다. 이전 (요청 또는 클라이언트 등록 중).</span><span class="sxs-lookup"><span data-stu-id="8f876-219">(C) Assuming the resource owner grants access, the authorization server redirects the user-agent back to the client using the redirection URI provided earlier (in the request or during client registration).</span></span> <span data-ttu-id="8f876-220">...</span><span class="sxs-lookup"><span data-stu-id="8f876-220">...</span></span> |  |
|  |  |
| <span data-ttu-id="8f876-221">(D) 클라이언트를 사용 하면 권한 부여 서버의 토큰 끝점에서 액세스 토큰을 요청 하는 이전 단계에서 받은 인증 코드를 포함 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-221">(D) The client requests an access token from the authorization server's token endpoint by including the authorization code received in the previous step.</span></span> <span data-ttu-id="8f876-222">요청할 때 클라이언트는 권한 부여 서버를 사용 하 여 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-222">When making the request, the client authenticates with the authorization server.</span></span> <span data-ttu-id="8f876-223">클라이언트는 리디렉션 URI가 확인에 대 한 권한 부여 코드를 가져오는 데를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-223">The client includes the redirection URI used to obtain the authorization code for verification.</span></span> |  |

<span data-ttu-id="8f876-224">권한 부여 끝점을 이미 구현에서는 되므로 (`OAuthController.Authorize` 작업) 권한 부여 코드 부여를 위해 자동으로 활성화할도 암시적 흐름입니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-224">Since we already implemented the authorization endpoint (`OAuthController.Authorize` action) for authorization code grant, it automatically enables implicit flow as well.</span></span> <span data-ttu-id="8f876-225">참고: `Provider.ValidateClientRedirectUri` 액세스 토큰을 악의적인 클라이언트 전송에서 암시적 허용 흐름을 보호 하는 리디렉션 URL 사용 하 여 클라이언트 ID의 유효성을 검사 하는 데 사용 됩니다 ([중간자 개입 공격](https://www.owasp.org/index.php/Man-in-the-middle_attack)).</span><span class="sxs-lookup"><span data-stu-id="8f876-225">Note: `Provider.ValidateClientRedirectUri` is used to validate the client ID with its redirection URL, which protects the implicit grant flow from sending the access token to malicious clients ([Man-in-the-middle attack](https://www.owasp.org/index.php/Man-in-the-middle_attack)).</span></span>

### <a name="resource-owner-password-credentials-grant"></a><span data-ttu-id="8f876-226">리소스 소유자 암호 자격 증명을 권한 부여</span><span class="sxs-lookup"><span data-stu-id="8f876-226">Resource Owner Password Credentials Grant</span></span>

<span data-ttu-id="8f876-227">IETF의 OAuth 2를 참조 하십시오 [리소스 소유자 암호 자격 증명 부여](http://tools.ietf.org/html/rfc6749#section-4.3) 이제 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-227">Refer to the IETF's OAuth 2 [Resource Owner Password Credentials Grant](http://tools.ietf.org/html/rfc6749#section-4.3) section now.</span></span>

 <span data-ttu-id="8f876-228">합니다 [리소스 소유자 암호 자격 증명 부여](http://tools.ietf.org/html/rfc6749#section-4.3) 그림 5에 표시 된 흐름은 흐름 및 미들웨어는 OWIN OAuth 매핑을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-228">The [Resource Owner Password Credentials Grant](http://tools.ietf.org/html/rfc6749#section-4.3) flow shown in Figure 5 is the flow and mapping which the OWIN OAuth middleware follows.</span></span>  

| <span data-ttu-id="8f876-229">리소스 소유자 암호 자격 증명 권한 부여 섹션에서 흐름 단계</span><span class="sxs-lookup"><span data-stu-id="8f876-229">Flow steps from Resource Owner Password Credentials Grant section</span></span> | <span data-ttu-id="8f876-230">샘플 다운로드에는 이러한 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-230">Sample download performs these steps with:</span></span> |
| --- | --- |
|  |  |
| <span data-ttu-id="8f876-231">(A) 리소스 소유자의 사용자 이름 및 암호를 사용 하 여 클라이언트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-231">(A) The resource owner provides the client with its username and password.</span></span> |  |
|  |  |
| <span data-ttu-id="8f876-232">(B) 클라이언트를 사용 하면 권한 부여 서버의 토큰 끝점에서 액세스 토큰을 요청 하는 리소스 소유자 로부터 수신한 자격 증명을 포함 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-232">(B) The client requests an access token from the authorization server's token endpoint by including the credentials received from the resource owner.</span></span> <span data-ttu-id="8f876-233">요청할 때 클라이언트는 권한 부여 서버를 사용 하 여 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-233">When making the request, the client authenticates with the authorization server.</span></span> | <span data-ttu-id="8f876-234">Provider.MatchEndpoint Provider.ValidateClientAuthentication Provider.ValidateTokenRequest Provider.GrantResourceOwnerCredentials Provider.TokenEndpoint AccessToken Provider.CreateAsync RefreshTokenProvider.CreateAsync</span><span class="sxs-lookup"><span data-stu-id="8f876-234">Provider.MatchEndpoint Provider.ValidateClientAuthentication Provider.ValidateTokenRequest Provider.GrantResourceOwnerCredentials Provider.TokenEndpoint AccessToken Provider.CreateAsync RefreshTokenProvider.CreateAsync</span></span> |
|  |  |
| <span data-ttu-id="8f876-235">(권한 부여 서버 C) 리소스 소유자 자격 증명의 유효성을 검사 및 유효한 경우 액세스 토큰을 발급 합니다. 클라이언트를 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-235">(C) The authorization server authenticates the client and validates the resource owner credentials, and if valid, issues an access token.</span></span> |  |

<span data-ttu-id="8f876-236">에 대 한 샘플 구현은 같습니다 `Provider.GrantResourceOwnerCredentials`:</span><span class="sxs-lookup"><span data-stu-id="8f876-236">Here is the sample implementation for `Provider.GrantResourceOwnerCredentials`:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample7.cs)]

> [!NOTE]
> <span data-ttu-id="8f876-237">위의 코드는 자습서의이 섹션에서는 설명 되며 보안에서 사용할 수 없습니다 또는 프로덕션 앱.</span><span class="sxs-lookup"><span data-stu-id="8f876-237">The code above is intended to explain this section of the tutorial and should not be used in secure or production apps.</span></span> <span data-ttu-id="8f876-238">리소스 소유자 자격 증명을 확인 하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-238">It does not check the resource owners credentials.</span></span> <span data-ttu-id="8f876-239">모든 자격 증명이 유효 하 고 새 id를 만드는 것으로 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-239">It assumes every credential is valid and creates a new identity for it.</span></span> <span data-ttu-id="8f876-240">새 id 생성 액세스 토큰 및 새로 고침 토큰에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-240">The new identity will be used to generate the access token and refresh token.</span></span> <span data-ttu-id="8f876-241">사용자 고유의 보안 계정 관리 코드를 사용 하 여 코드를 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="8f876-241">Please replace the code with your own secure account management code.</span></span>


### <a name="client-credentials-grant"></a><span data-ttu-id="8f876-242">클라이언트 권한 부여 자격 증명</span><span class="sxs-lookup"><span data-stu-id="8f876-242">Client Credentials Grant</span></span>

<span data-ttu-id="8f876-243">IETF의 OAuth 2를 참조 하십시오 [클라이언트 자격 증명 부여](http://tools.ietf.org/html/rfc6749#section-4.4) 이제 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-243">Refer to the IETF's OAuth 2 [Client Credentials Grant](http://tools.ietf.org/html/rfc6749#section-4.4) section now.</span></span>

 <span data-ttu-id="8f876-244">합니다 [클라이언트 자격 증명 부여](http://tools.ietf.org/html/rfc6749#section-4.4) 그림 6에 표시 된 흐름은 흐름 및 미들웨어는 OWIN OAuth 매핑을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-244">The [Client Credentials Grant](http://tools.ietf.org/html/rfc6749#section-4.4) flow shown in Figure 6 is the flow and mapping which the OWIN OAuth middleware follows.</span></span>  

| <span data-ttu-id="8f876-245">클라이언트 자격 증명 권한 부여 섹션에서 흐름 단계</span><span class="sxs-lookup"><span data-stu-id="8f876-245">Flow steps from Client Credentials Grant section</span></span> | <span data-ttu-id="8f876-246">샘플 다운로드에는 이러한 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-246">Sample download performs these steps with:</span></span> |
| --- | --- |
|  |  |
| <span data-ttu-id="8f876-247">(A) 클라이언트가 권한 부여 서버를 사용 하 여 인증 하 고 토큰 끝점에서 액세스 토큰을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-247">(A) The client authenticates with the authorization server and requests an access token from the token endpoint.</span></span> | <span data-ttu-id="8f876-248">Provider.MatchEndpoint Provider.ValidateClientAuthentication Provider.ValidateTokenRequest Provider.GrantClientCredentials Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync</span><span class="sxs-lookup"><span data-stu-id="8f876-248">Provider.MatchEndpoint Provider.ValidateClientAuthentication Provider.ValidateTokenRequest Provider.GrantClientCredentials Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync</span></span> |
|  |  |
| <span data-ttu-id="8f876-249">(B) 권한 부여 서버 클라이언트를 인증 하 고 유효한 경우 액세스 토큰을 발급 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-249">(B) The authorization server authenticates the client, and if valid, issues an access token.</span></span> |  |

<span data-ttu-id="8f876-250">에 대 한 샘플 구현은 같습니다 `Provider.GrantClientCredentials`:</span><span class="sxs-lookup"><span data-stu-id="8f876-250">Here is the sample implementation for `Provider.GrantClientCredentials`:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample8.cs)]

> [!NOTE]
> <span data-ttu-id="8f876-251">위의 코드는 자습서의이 섹션에서는 설명 되며 보안에서 사용할 수 없습니다 또는 프로덕션 앱.</span><span class="sxs-lookup"><span data-stu-id="8f876-251">The code above is intended to explain this section of the tutorial and should not be used in secure or production apps.</span></span> <span data-ttu-id="8f876-252">사용자 고유의 보안 클라이언트 관리 코드를 사용 하 여 코드를 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="8f876-252">Please replace the code with your own secure client management code.</span></span>


### <a name="refresh-token"></a><span data-ttu-id="8f876-253">새로 고침 토큰</span><span class="sxs-lookup"><span data-stu-id="8f876-253">Refresh Token</span></span>

<span data-ttu-id="8f876-254">IETF의 OAuth 2를 참조 하십시오 [새로 고침 토큰](http://tools.ietf.org/html/rfc6749#section-1.5) 이제 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-254">Refer to the IETF's OAuth 2 [Refresh Token](http://tools.ietf.org/html/rfc6749#section-1.5) section now.</span></span>

 <span data-ttu-id="8f876-255">합니다 [새로 고침 토큰](http://tools.ietf.org/html/rfc6749#section-1.5) 그림 2에 표시 된 흐름은 흐름 및 미들웨어는 OWIN OAuth 매핑을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-255">The [Refresh Token](http://tools.ietf.org/html/rfc6749#section-1.5) flow shown in Figure 2 is the flow and mapping which the OWIN OAuth middleware follows.</span></span>  

| <span data-ttu-id="8f876-256">클라이언트 자격 증명 권한 부여 섹션에서 흐름 단계</span><span class="sxs-lookup"><span data-stu-id="8f876-256">Flow steps from Client Credentials Grant section</span></span> | <span data-ttu-id="8f876-257">샘플 다운로드에는 이러한 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-257">Sample download performs these steps with:</span></span> |
| --- | --- |
|  |  |
| <span data-ttu-id="8f876-258">(G) 클라이언트는 권한 부여 서버를 사용 하 여 인증 하 고 새로 고침 토큰을 제공 하 여 새 액세스 토큰을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-258">(G) The client requests a new access token by authenticating with the authorization server and presenting the refresh token.</span></span> <span data-ttu-id="8f876-259">클라이언트 인증 요구 사항은 클라이언트 형식에는 권한 부여 서버 정책에 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-259">The client authentication requirements are based on the client type and on the authorization server policies.</span></span> | <span data-ttu-id="8f876-260">Provider.MatchEndpoint Provider.ValidateClientAuthentication RefreshTokenProvider.ReceiveAsync Provider.ValidateTokenRequest Provider.GrantRefreshToken Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync</span><span class="sxs-lookup"><span data-stu-id="8f876-260">Provider.MatchEndpoint Provider.ValidateClientAuthentication RefreshTokenProvider.ReceiveAsync Provider.ValidateTokenRequest Provider.GrantRefreshToken Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync</span></span> |
|  |  |
| <span data-ttu-id="8f876-261">(H) 권한 부여 서버 새로 고침 토큰의 유효성을 검사 및 유효한 경우 문제는 새 액세스 토큰 (및 필요에 따라 새로운 새로 고침 토큰) 클라이언트를 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-261">(H) The authorization server authenticates the client and validates the refresh token, and if valid, issues a new access token (and, optionally, a new refresh token).</span></span> |  |

<span data-ttu-id="8f876-262">에 대 한 샘플 구현은 같습니다 `Provider.GrantRefreshToken`:</span><span class="sxs-lookup"><span data-stu-id="8f876-262">Here is the sample implementation for `Provider.GrantRefreshToken`:</span></span> 

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample9.cs)]

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample10.cs)]

## <a name="create-a-resource-server-which-is-protected-by-access-token"></a><span data-ttu-id="8f876-263">액세스 토큰으로 보호 되는 리소스 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="8f876-263">Create a Resource Server which is protected by Access Token</span></span>

<span data-ttu-id="8f876-264">빈 웹 앱 프로젝트를 만들고 다음 프로젝트에서 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-264">Create an empty web app project and install following packages in the project:</span></span>

- <span data-ttu-id="8f876-265">Microsoft.AspNet.WebApi.Owin</span><span class="sxs-lookup"><span data-stu-id="8f876-265">Microsoft.AspNet.WebApi.Owin</span></span>
- <span data-ttu-id="8f876-266">Microsoft.Owin.Host.SystemWeb</span><span class="sxs-lookup"><span data-stu-id="8f876-266">Microsoft.Owin.Host.SystemWeb</span></span>
- <span data-ttu-id="8f876-267">Microsoft.Owin.Security.OAuth</span><span class="sxs-lookup"><span data-stu-id="8f876-267">Microsoft.Owin.Security.OAuth</span></span>

<span data-ttu-id="8f876-268">Startup 클래스를 만들고 인증 및 Web API를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-268">Create a startup class and configure authentication and Web API.</span></span> <span data-ttu-id="8f876-269">참조 *AuthorizationServer\ResourceServer\Startup.cs* 샘플 다운로드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-269">See *AuthorizationServer\ResourceServer\Startup.cs* in the sample download.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample11.cs)]

<span data-ttu-id="8f876-270">참조 *AuthorizationServer\ResourceServer\App\_Start\Startup.Auth.cs* 샘플 다운로드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-270">See *AuthorizationServer\ResourceServer\App\_Start\Startup.Auth.cs* in the sample download.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample12.cs)]

<span data-ttu-id="8f876-271">참조 *AuthorizationServer\ResourceServer\App\_Start\Startup.WebApi.cs* 샘플 다운로드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-271">See *AuthorizationServer\ResourceServer\App\_Start\Startup.WebApi.cs* in the sample download.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample13.cs)]

- <span data-ttu-id="8f876-272">`UseCors` 메서드는 모든 도메인에 대 한 CORS를 사용 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-272">`UseCors` method allows CORS for all domains.</span></span>
- <span data-ttu-id="8f876-273">`UseOAuthBearerAuthentication` 메서드를 수신 하 고 권한 부여 요청 헤더에서 전달자 토큰의 유효성을 검사 하는 OAuth 전달자 토큰 인증 미들웨어를 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-273">`UseOAuthBearerAuthentication` method enables OAuth bearer token authentication middleware which will receive and validate bearer token from authorization header in the request.</span></span>
- <span data-ttu-id="8f876-274">`Config.SuppressDefaultHostAuthenticaiton` 기본 억제 하므로 모든 요청은 익명 이어야이 호출 후, 앱에서 인증 된 보안 주체를 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-274">`Config.SuppressDefaultHostAuthenticaiton` suppresses default host authenticated principal from the app, therefore all requests will be anonymous after this call.</span></span>
- <span data-ttu-id="8f876-275">`HostAuthenticationFilter` 지정된 된 인증 형식에 대해서만 인증을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-275">`HostAuthenticationFilter` enables authentication just for the specified authentication type.</span></span> <span data-ttu-id="8f876-276">이 경우 전달자 인증 유형을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-276">In this case, it's bearer authentication type.</span></span>

<span data-ttu-id="8f876-277">인증된 된 id를 보여 주기 위해 ApiController 출력 현재 사용자의 클레임을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-277">In order to demonstrate the authenticated identity, we create an ApiController to output current user's claims.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample14.cs)]

<span data-ttu-id="8f876-278">권한 부여 서버와 리소스 서버가 동일한 컴퓨터에 없는 경우 OAuth 미들웨어 다른 컴퓨터 키를 사용 하 여 암호화 하 고 전달자 액세스 토큰을 해독 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-278">If the authorization server and the resource server are not on the same computer, the OAuth middleware will use the different machine keys to encrypt and decrypt bearer access token.</span></span> <span data-ttu-id="8f876-279">두 프로젝트 간에 동일한 개인 키를 공유 하기 위해 추가 동일 `machinekey` 둘 다에서 설정 *web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-279">In order to share the same private key between both projects, we add the same `machinekey` setting in both *web.config* files.</span></span>

[!code-xml[Main](owin-oauth-20-authorization-server/samples/sample15.xml?highlight=8-10)]

## <a name="create-oauth-20-clients"></a><span data-ttu-id="8f876-280">OAuth 2.0 클라이언트 만들기</span><span class="sxs-lookup"><span data-stu-id="8f876-280">Create OAuth 2.0 Clients</span></span>

 <span data-ttu-id="8f876-281">사용 하 여 합니다 [DotNetOpenAuth.OAuth2.Client](http://www.nuget.org/packages/DotNetOpenAuth.OAuth2.Client) NuGet 패키지를 클라이언트 코드를 단순화 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-281">We use the [DotNetOpenAuth.OAuth2.Client](http://www.nuget.org/packages/DotNetOpenAuth.OAuth2.Client) NuGet package to simplify the client code.</span></span>

### <a name="authorization-code-grant-client"></a><span data-ttu-id="8f876-282">권한 부여 코드 부여 클라이언트</span><span class="sxs-lookup"><span data-stu-id="8f876-282">Authorization Code Grant Client</span></span>

 <span data-ttu-id="8f876-283">이 클라이언트는 MVC 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-283">This client is an MVC application.</span></span> <span data-ttu-id="8f876-284">백 엔드에서 액세스 토큰을 가져오는 인증 코드 부여 흐름을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-284">It will trigger an authorization code grant flow to get the access token from backend.</span></span> <span data-ttu-id="8f876-285">아래와 같이 단일 페이지를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-285">It has a single page as shown below:</span></span>

![](owin-oauth-20-authorization-server/_static/image3.png)

- <span data-ttu-id="8f876-286">합니다 **권한 부여** 단추는이 클라이언트에 대 한 액세스를 부여할 리소스 소유자에 게 알려야 권한 부여 서버에 브라우저를 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-286">The **Authorize** button will redirect browser to the authorization server to notify the resource owner to grant access to this client.</span></span>
- <span data-ttu-id="8f876-287">합니다 **새로 고침** 단추는 현재 새로 고침을 사용 하는 새 액세스 토큰 및 새로 고침 토큰 가져오기.</span><span class="sxs-lookup"><span data-stu-id="8f876-287">The **Refresh** button will get a new access token and refresh token using the current refresh token.</span></span>
- <span data-ttu-id="8f876-288">합니다 **리소스 API를 보호 하는 액세스** 단추를 현재 사용자의 클레임 데이터를 가져오고 페이지에 표시할 리소스 서버를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-288">The **Access Protected Resource API** button will call the resource server to get current user's claims data and show them on the page.</span></span>

<span data-ttu-id="8f876-289">다음은의 샘플 코드는 `HomeController` 클라이언트의 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-289">Here is the sample code of the `HomeController` of the client.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample16.cs)]

<span data-ttu-id="8f876-290">`DotNetOpenAuth` 기본적으로 SSL이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-290">`DotNetOpenAuth` requires SSL by default.</span></span> <span data-ttu-id="8f876-291">추가 해야 하는 데모는 HTTP를 사용 하므로 다음 구성 파일에 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-291">Since our demo is using HTTP, you need to add following setting in the config file:</span></span>

[!code-xml[Main](owin-oauth-20-authorization-server/samples/sample17.xml?highlight=4-6)]

> [!WARNING]
> <span data-ttu-id="8f876-292">보안-프로덕션 앱에서 SSL 해제 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-292">Security - Never disable SSL in a production app.</span></span> <span data-ttu-id="8f876-293">이제 로그인 자격 증명 네트워크를 통해 일반 텍스트로 전송 되 고 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-293">Your login credentials are now being sent in clear-text across the wire.</span></span> <span data-ttu-id="8f876-294">위의 코드 샘플 로컬 디버깅 및 탐색 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-294">The code above is just for local sample debugging and exploration.</span></span>


### <a name="implicit-grant-client"></a><span data-ttu-id="8f876-295">암시적 권한 부여 클라이언트</span><span class="sxs-lookup"><span data-stu-id="8f876-295">Implicit Grant Client</span></span>

<span data-ttu-id="8f876-296">이 클라이언트는 JavaScript를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-296">This client is using JavaScript to:</span></span>

1. <span data-ttu-id="8f876-297">새 창을 열고 권한 부여 서버의 권한 부여 끝점으로 리디렉션하십시오.</span><span class="sxs-lookup"><span data-stu-id="8f876-297">Open a new window and redirect to the authorize endpoint of the Authorization Server.</span></span>
2. <span data-ttu-id="8f876-298">액세스 토큰을 얻으려면 URL 조각에서 다시 리디렉션할 때.</span><span class="sxs-lookup"><span data-stu-id="8f876-298">Get the access token from URL fragments when it redirects back.</span></span>

<span data-ttu-id="8f876-299">다음 그림에서는이 프로세스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-299">The following image shows this process:</span></span>

![](owin-oauth-20-authorization-server/_static/image4.png)

<span data-ttu-id="8f876-300">클라이언트에 두 페이지 있어야 합니다.: 홈 페이지 및 콜백에 대 한 기타 하나입니다. 다음은 샘플 코드는 JavaScript는 *Index.cshtml* 파일:</span><span class="sxs-lookup"><span data-stu-id="8f876-300">The client should have two pages: one for home page and the other for callback.Here is the sample JavaScript code found in the *Index.cshtml* file:</span></span>

[!code-cshtml[Main](owin-oauth-20-authorization-server/samples/sample18.cshtml)]

<span data-ttu-id="8f876-301">다음은 처리 코드에 콜백 *SignIn.cshtml* 파일:</span><span class="sxs-lookup"><span data-stu-id="8f876-301">Here is the callback handling code in *SignIn.cshtml* file:</span></span>

[!code-cshtml[Main](owin-oauth-20-authorization-server/samples/sample19.cshtml)]

> [!NOTE]
> <span data-ttu-id="8f876-302">외부 파일에 JavaScript를 이동 하 고 Razor 태그를 사용 하 여 포함 되어 있지 않으므로 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-302">A best practice is to move the JavaScript to an external file and not embed it with the Razor markup.</span></span> <span data-ttu-id="8f876-303">간단히 유지 하기 위해이 샘플은 결합 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-303">To keep this sample simple, they have been combined.</span></span>


### <a name="resource-owner-password-credentials-grant-client"></a><span data-ttu-id="8f876-304">리소스 소유자 암호 권한 부여 클라이언트 자격 증명</span><span class="sxs-lookup"><span data-stu-id="8f876-304">Resource Owner Password Credentials Grant Client</span></span>

<span data-ttu-id="8f876-305">콘솔 앱을 사용 하 여이 클라이언트 데모 했습니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-305">We uses a console app to demo this client.</span></span> <span data-ttu-id="8f876-306">코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-306">Here is the code:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample20.cs)]

### <a name="client-credentials-grant-client"></a><span data-ttu-id="8f876-307">클라이언트 자격 증명 부여</span><span class="sxs-lookup"><span data-stu-id="8f876-307">Client Credentials Grant Client</span></span>

<span data-ttu-id="8f876-308">리소스 소유자 암호 자격 증명 부여와 마찬가지로, 콘솔 응용 프로그램 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8f876-308">Similar to the Resource Owner Password Credentials Grant, here is console app code:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample21.cs)]
