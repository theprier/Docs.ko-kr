---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-authentication-and-profile-application-services
title: "ASP.NET AJAX 인증 및 프로필 응용 프로그램 서비스 이해 | Microsoft Docs"
author: scottcate
description: "인증 서비스 사용자가 인증 쿠키를 수신 하려면 자격 증명을 제공할 수 있도록 하 고는 사용자 지정을 허용 하도록 게이트웨이 서비스..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/14/2008
ms.topic: article
ms.assetid: 6ab4efb6-aab6-45ac-ad2c-bdec5848ef9e
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-authentication-and-profile-application-services
msc.type: authoredcontent
ms.openlocfilehash: 7e0ddc15fac9af40a0a20a99979a80517eb1b6a2
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="understanding-aspnet-ajax-authentication-and-profile-application-services"></a><span data-ttu-id="40717-103">ASP.NET AJAX 인증 및 프로필 응용 프로그램 서비스 이해</span><span class="sxs-lookup"><span data-stu-id="40717-103">Understanding ASP.NET AJAX Authentication and Profile Application Services</span></span>
====================
<span data-ttu-id="40717-104">으로 [Scott 인증서](https://github.com/scottcate)</span><span class="sxs-lookup"><span data-stu-id="40717-104">by [Scott Cate](https://github.com/scottcate)</span></span>

[<span data-ttu-id="40717-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="40717-105">Download PDF</span></span>](http://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial03_MSAjax_ASP.NET_Services_cs.pdf)

> <span data-ttu-id="40717-106">인증 서비스를 사용 하면 사용자가 인증 쿠키를 수신 하기 위해 자격 증명을 제공 하 고 ASP.NET에서 사용자 지정 사용자 프로필을 허용 하도록 게이트웨이 서비스가 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40717-106">The Authentication service allows users to provide credentials in order to receive an authentication cookie, and is the gateway service to allow custom user profiles provided by ASP.NET.</span></span> <span data-ttu-id="40717-107">ASP.NET AJAX 인증 서비스 사용은 표준 ASP.NET 폼 인증을 호환 폼 인증을 사용 하 여 현재 응용 프로그램 (예: 로그인 제어)는 분리할 수 없는 AJAX 인증 서비스를 업그레이드 하면 되므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-107">Use of the ASP.NET AJAX authentication service is compatible with standard ASP.NET Forms authentication, so applications currently using Forms authentication (such as with the Login control) will not be broken by upgrading to the AJAX authentication service.</span></span>


## <a name="introduction"></a><span data-ttu-id="40717-108">소개</span><span class="sxs-lookup"><span data-stu-id="40717-108">Introduction</span></span>

<span data-ttu-id="40717-109">Microsoft은.NET Framework 3.5의 일부로 하려면 많은 환경 업그레이드; 전달 뿐만 아니라 새로운 개발 환경을 사용할 수 있지만 새 LINQ (Language-Integrated Query) 기능 및 향상 된 다른 언어 곧 출시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40717-109">As part of the .NET Framework 3.5, Microsoft is delivering a sizable environment upgrade; not only is a new development environment available, but the new Language-Integrated Query (LINQ) features and other language enhancements are forthcoming.</span></span> <span data-ttu-id="40717-110">또한 다른 도구 집합, 특히 ASP.NET AJAX 확장에 대 한 일부 기능과.NET Framework 기본 클래스 라이브러리의 최상위 멤버로 포함 되 고 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40717-110">In addition, some familiar features of other toolsets, notably the ASP.NET AJAX Extensions, are being included as first-class members of the .NET Framework Base Class Library.</span></span> <span data-ttu-id="40717-111">이러한 확장 페이지의 부분 렌더링을 포함 하 여 전체 페이지 새로 고침 (프로 파일링 API는 ASP.NET 포함), 클라이언트 스크립트 및 광범위 한 클라이언트 쪽 API를 통해 웹 서비스에 액세스 하는 기능을 요구 하지 않고 새로운 많은 리치 클라이언트 기능을 사용 하도록 설정 다양 한 ASP.NET 서버측 컨트롤 집합에 표시 된 컨트롤 스키마를 반영 하도록 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="40717-111">These extensions enable many new rich client features, including partial rendering of pages without requiring a full page refresh, the ability to access Web Services via client script (including the ASP.NET profiling API), and an extensive client-side API designed to mirror many of the control schemes seen in the ASP.NET server-side control set.</span></span>

<span data-ttu-id="40717-112">이 백서에서는 ASP.NET 프로 파일링의 용도 및 구현 만들고 폼 인증 서비스 Microsoft ASP.NET AJAX ExtensionsThe AJAX 확장에 의해 노출 되는 대로 폼 인증을 지원 하기 위해 매우 쉽게 (으로 프로 파일링 서비스) 웹 서비스 프록시 스크립트를 통해 노출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40717-112">This whitepaper looks at the implementation and use of the ASP.NET Profiling and Forms Authentication services as they are exposed by the Microsoft ASP.NET AJAX ExtensionsThe AJAX Extensions make Forms authentication incredibly easy to support, as it (as well as the Profiling Service) is exposed through a Web Service proxy script.</span></span> <span data-ttu-id="40717-113">AJAX 확장에는 AuthenticationServiceManager 클래스를 통해 사용자 지정 인증도 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-113">The AJAX Extensions also support custom authentication through the AuthenticationServiceManager class.</span></span>

<span data-ttu-id="40717-114">이 백서는 Beta 2 버전의 Visual Studio 2008 및.NET Framework 3.5를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-114">This whitepaper is based on the Beta 2 release of the Visual Studio 2008 and the .NET Framework 3.5.</span></span> <span data-ttu-id="40717-115">이 백서는 Visual Studio 2008 베타 2, 하지 Visual Web Developer Express를 사용 하 고 Visual Studio의 사용자 인터페이스에 따라 연습을 제공 합니다 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-115">This whitepaper also assumes that you will be working with Visual Studio 2008 Beta 2, not Visual Web Developer Express, and will provide walkthroughs according to the user interface of Visual Studio.</span></span> <span data-ttu-id="40717-116">일부 코드 샘플은 Visual Web Developer Express에서 사용할 수 없는 프로젝트 템플릿을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40717-116">Some code samples may utilize project templates unavailable in Visual Web Developer Express.</span></span>

## <a name="profiles-and-authentication"></a><span data-ttu-id="40717-117">*프로필 및 인증*</span><span class="sxs-lookup"><span data-stu-id="40717-117">*Profiles and Authentication*</span></span>

<span data-ttu-id="40717-118">Microsoft ASP.NET 프로필 및 인증 서비스는 ASP.NET 폼 인증 시스템에 의해 제공 되 고는 ASP.NET의 표준 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-118">The Microsoft ASP.NET Profiles and Authentication services are provided by the ASP.NET Forms Authentication system, and are standard components of ASP.NET.</span></span> <span data-ttu-id="40717-119">ASP.NET AJAX Extensions 스크립트를 통해 스크립트 프록시 AJAX 클라이언트 라이브러리의 Sys.Services 네임 스페이스 아래의 매우 간단한 모델을 통해 이러한 서비스에 대 한 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-119">The ASP.NET AJAX Extensions provide script access to these services via script proxies, through a fairly straightforward model under the Sys.Services namespace of the client AJAX library.</span></span>

<span data-ttu-id="40717-120">인증 서비스를 사용 하면 사용자가 인증 쿠키를 수신 하기 위해 자격 증명을 제공 하 고 ASP.NET에서 사용자 지정 사용자 프로필을 허용 하도록 게이트웨이 서비스가 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40717-120">The Authentication service allows users to provide credentials in order to receive an authentication cookie, and is the gateway service to allow custom user profiles provided by ASP.NET.</span></span> <span data-ttu-id="40717-121">ASP.NET AJAX 인증 서비스 사용은 표준 ASP.NET 폼 인증을 호환 폼 인증을 사용 하 여 현재 응용 프로그램 (예: 로그인 제어)는 분리할 수 없는 AJAX 인증 서비스를 업그레이드 하면 되므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-121">Use of the ASP.NET AJAX authentication service is compatible with standard ASP.NET Forms authentication, so applications currently using Forms authentication (such as with the Login control) will not be broken by upgrading to the AJAX authentication service.</span></span>

<span data-ttu-id="40717-122">프로필 서비스를 자동으로 통합 및 멤버 자격에 따라 인증 서비스에서 제공 하는 사용자 데이터의 저장소를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40717-122">The Profile service allows the automatic integration and storage of user data based on membership as provided by the Authentication service.</span></span> <span data-ttu-id="40717-123">Web.config 파일에 저장 된 데이터는 지정 하 고 다양 한 프로 파일링 서비스 공급자, 데이터 관리를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-123">The stored data is specified by the web.config file, and the various profiling service providers handle the data management.</span></span> <span data-ttu-id="40717-124">인증 서비스와 마찬가지로 AJAX 프로필 서비스는 표준 ASP.NET 프로필 서비스와 호환 되므로 AJAX 지원을 포함 하 여 현재 ASP.NET 프로필 서비스의 기능을 통합 하는 페이지를 나눌 수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-124">As with the Authentication service, the AJAX Profile service is compatible with the standard ASP.NET profile service, so that pages currently incorporating features of the ASP.NET Profile service should not be broken by including AJAX support.</span></span>

<span data-ttu-id="40717-125">응용 프로그램에 ASP.NET 인증 및 자체 프로 파일링 서비스를 통합 하는이 백서의 범위를 벗어났습니다.</span><span class="sxs-lookup"><span data-stu-id="40717-125">Incorporating the ASP.NET Authentication and Profiling services themselves into an application is outside of the scope of this whitepaper.</span></span> <span data-ttu-id="40717-126">항목에 대 한 자세한 내용은 MSDN Library를 참조 하십시오. 참조 문서에서 멤버를 사용 하 여 사용자 관리 [https://msdn.microsoft.com/en-us/library/tw292whz.aspx](https://msdn.microsoft.com/en-us/library/tw292whz.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-126">For more information on the topic, see the MSDN Library reference article Managing Users by Using Membership at [https://msdn.microsoft.com/en-us/library/tw292whz.aspx](https://msdn.microsoft.com/en-us/library/tw292whz.aspx).</span></span> <span data-ttu-id="40717-127">또한 ASP.NET 멤버 자격 ASP.NET 멤버 자격에 대 한 기본 인증 서비스 공급자 인 SQL Server와 함께 자동으로 설정 하는 유틸리티를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-127">ASP.NET also includes a utility to automatically set up Membership with a SQL Server, which is the default authentication service provider for ASP.NET Membership.</span></span> <span data-ttu-id="40717-128">자세한 내용은 문서 ASP.NET SQL Server 등록 도구 참조 (Aspnet\_regsql.exe)에서 [https://msdn.microsoft.com/en-us/library/ms229862(vs.80).aspx](https://msdn.microsoft.com/en-us/library/ms229862(vs.80).aspx).</span><span class="sxs-lookup"><span data-stu-id="40717-128">For more information, see the article ASP.NET SQL Server Registration Tool (Aspnet\_regsql.exe) at [https://msdn.microsoft.com/en-us/library/ms229862(vs.80).aspx](https://msdn.microsoft.com/en-us/library/ms229862(vs.80).aspx).</span></span>

## <a name="using-the-aspnet-ajax-authentication-service"></a><span data-ttu-id="40717-129">*ASP.NET AJAX 인증 서비스를 사용 하 여*</span><span class="sxs-lookup"><span data-stu-id="40717-129">*Using the ASP.NET AJAX Authentication Service*</span></span>

<span data-ttu-id="40717-130">Web.config 파일에서 ASP.NET AJAX 인증 서비스를 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-130">The ASP.NET AJAX Authentication service must be enabled in the web.config file:</span></span>

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample1.xml)]

<span data-ttu-id="40717-131">인증 서비스를 사용 하도록 설정할 ASP.NET 폼 인증이 필요 하 고 (스크립트를 사용할 수 없습니다 쿠키 없는 세션 쿠키가 없는 세션 URL 매개 변수를 필요 하기 때문) 클라이언트 브라우저에서 사용 하는 쿠키를 필요로 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-131">The Authentication service requires ASP.NET Forms authentication to be enabled and requires cookies to be enabled on the client browser (a script cannot enable a cookieless session since cookieless sessions require URL parameters).</span></span>

<span data-ttu-id="40717-132">AJAX 인증 서비스는 사용 하도록 설정 하 고 구성 된 클라이언트 스크립트는 Sys.Services.AuthenticationService 개체를 즉시 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40717-132">Once the AJAX authentication service is enabled and configured, client script can immediately take advantage of the Sys.Services.AuthenticationService object.</span></span> <span data-ttu-id="40717-133">기본적으로, 클라이언트 스크립트는의 활용 하려고는 `login` 메서드 및 `isLoggedIn` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-133">Primarily, client script will want to take advantage of the `login` method and `isLoggedIn` property.</span></span> <span data-ttu-id="40717-134">여러 속성을 많은 수의 매개 변수를 받을 수 있는 로그인 메서드에 대 한 기본값을 제공 하기 위해 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-134">Several properties exist to provide defaults for the login method, which can accept a large number of parameters.</span></span>

<span data-ttu-id="40717-135">*Sys.Services.AuthenticationService 멤버*</span><span class="sxs-lookup"><span data-stu-id="40717-135">*Sys.Services.AuthenticationService members*</span></span>

<span data-ttu-id="40717-136">*로그인 방법:*</span><span class="sxs-lookup"><span data-stu-id="40717-136">*login method:*</span></span>

<span data-ttu-id="40717-137">Login() 메서드는 사용자의 자격 증명을 인증 하는 요청을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-137">The login() method begins a request to authenticate the user's credentials.</span></span> <span data-ttu-id="40717-138">이 메서드는 비동기적 이며 실행을 차단 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="40717-138">This method is asynchronous and does not block execution.</span></span>

<span data-ttu-id="40717-139">*매개 변수:*</span><span class="sxs-lookup"><span data-stu-id="40717-139">*Parameters:*</span></span>

| <span data-ttu-id="40717-140">**매개 변수 이름**</span><span class="sxs-lookup"><span data-stu-id="40717-140">**Parameter Name**</span></span> | <span data-ttu-id="40717-141">**의미**</span><span class="sxs-lookup"><span data-stu-id="40717-141">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="40717-142">사용자 이름</span><span class="sxs-lookup"><span data-stu-id="40717-142">userName</span></span> | <span data-ttu-id="40717-143">필수 요소.</span><span class="sxs-lookup"><span data-stu-id="40717-143">Required.</span></span> <span data-ttu-id="40717-144">사용자 이름 인증입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-144">The username to authenticate.</span></span> |
| <span data-ttu-id="40717-145">암호</span><span class="sxs-lookup"><span data-stu-id="40717-145">password</span></span> | <span data-ttu-id="40717-146">옵션 (기본값은 null)입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-146">Optional (defaults to null).</span></span> <span data-ttu-id="40717-147">사용자의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-147">The user's password.</span></span> |
| <span data-ttu-id="40717-148">isPersistent</span><span class="sxs-lookup"><span data-stu-id="40717-148">isPersistent</span></span> | <span data-ttu-id="40717-149">선택 사항 (기본값: false)입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-149">Optional (defaults to false).</span></span> <span data-ttu-id="40717-150">여부 사용자의 인증 쿠키는 세션 간에 유지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-150">Whether the user's authentication cookie should persist across sessions.</span></span> <span data-ttu-id="40717-151">False 인 경우, 사용자는 브라우저 종료 하거나 세션이 만료 되 면 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-151">If false, the user will log out when the browser is closed or the session expires.</span></span> |
| <span data-ttu-id="40717-152">redirectUrl</span><span class="sxs-lookup"><span data-stu-id="40717-152">redirectUrl</span></span> | <span data-ttu-id="40717-153">옵션 (기본값은 null)입니다. 인증 성공 시 브라우저를 리디렉션할 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-153">Optional (defaults to null).The URL to redirect the browser to upon successful authentication.</span></span> <span data-ttu-id="40717-154">이 매개 변수가 null 또는 빈 문자열인 경우 없습니다 리디렉션이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-154">If this parameter is null or an empty string, no redirection occurs.</span></span> |
| <span data-ttu-id="40717-155">customInfo</span><span class="sxs-lookup"><span data-stu-id="40717-155">customInfo</span></span> | <span data-ttu-id="40717-156">옵션 (기본값은 null)입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-156">Optional (defaults to null).</span></span> <span data-ttu-id="40717-157">이 매개 변수는 현재 사용 되지 않으며 나중에 사용 하기 위해 예약 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40717-157">This parameter is currently unused and is reserved for future use.</span></span> |
| <span data-ttu-id="40717-158">loginCompletedCallback</span><span class="sxs-lookup"><span data-stu-id="40717-158">loginCompletedCallback</span></span> | <span data-ttu-id="40717-159">옵션 (기본값은 null)입니다. 함수는 로그인 성공적으로 완료 되 면입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-159">Optional (defaults to null).The function to call when the login has successfully completed.</span></span> <span data-ttu-id="40717-160">를 지정 하는 경우이 매개 변수 defaultLoginCompleted 속성을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-160">If specified, this parameter overrides the defaultLoginCompleted property.</span></span> |
| <span data-ttu-id="40717-161">failedCallback</span><span class="sxs-lookup"><span data-stu-id="40717-161">failedCallback</span></span> | <span data-ttu-id="40717-162">옵션 (기본값은 null)입니다. 로그인에 실패 한 경우 호출 하는 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-162">Optional (defaults to null).The function to call when the login has failed.</span></span> <span data-ttu-id="40717-163">를 지정 하는 경우이 매개 변수 defaultFailedCallback 속성을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-163">If specified, this parameter overrides the defaultFailedCallback property.</span></span> |
| <span data-ttu-id="40717-164">userContext</span><span class="sxs-lookup"><span data-stu-id="40717-164">userContext</span></span> | <span data-ttu-id="40717-165">옵션 (기본값은 null)입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-165">Optional (defaults to null).</span></span> <span data-ttu-id="40717-166">콜백 함수에 전달 되어야 하는 사용자 지정 사용자 컨텍스트 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-166">Custom user context data that should be passed to the callback functions.</span></span> |

<span data-ttu-id="40717-167">*반환 값:*</span><span class="sxs-lookup"><span data-stu-id="40717-167">*Return Value:*</span></span>

<span data-ttu-id="40717-168">이 함수는 반환 값을 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="40717-168">This function does not include a return value.</span></span> <span data-ttu-id="40717-169">그러나 동작의 수를이 함수로 호출 완료 시 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40717-169">However, a number of behaviors are included upon completion of a call to this function:</span></span>

- <span data-ttu-id="40717-170">현재 페이지를 새로 고칠 수 있거나 또는 경우 변경할 수는 `redirectUrl` 매개 변수를 null 또는 빈 문자열이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="40717-170">The current page will either be refreshed or be changed if the `redirectUrl` parameter was neither null nor an empty string.</span></span>
- <span data-ttu-id="40717-171">그러나 매개 변수가 null 이거나 빈 문자열이 면 되었으면는 `loginCompletedCallback` 매개 변수 또는 `defaultLoginCompletedCallback` 속성이 호출 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="40717-171">However, if the parameter was null or an empty string, the `loginCompletedCallback` parameter, or `defaultLoginCompletedCallback` property is called.</span></span>
- <span data-ttu-id="40717-172">웹 서비스 호출에 실패 하는 경우는 `failedCallback` 의 매개 변수 `defaultFailedCallback` 속성이 호출 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="40717-172">If the call to the web service fails, the `failedCallback` parameter of `defaultFailedCallback` property is called.</span></span>

<span data-ttu-id="40717-173">*로그 아웃 방법:*</span><span class="sxs-lookup"><span data-stu-id="40717-173">*logout method:*</span></span>

<span data-ttu-id="40717-174">Logout() 메서드는 자격 증명 쿠키를 제거 하 고 웹 응용 프로그램에서 현재 사용자를 로그 아웃 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-174">The logout() method removes the credentials cookie and logs out the current user from the web application.</span></span>

<span data-ttu-id="40717-175">*매개 변수:*</span><span class="sxs-lookup"><span data-stu-id="40717-175">*Parameters:*</span></span>

| <span data-ttu-id="40717-176">**매개 변수 이름**</span><span class="sxs-lookup"><span data-stu-id="40717-176">**Parameter Name**</span></span> | <span data-ttu-id="40717-177">**의미**</span><span class="sxs-lookup"><span data-stu-id="40717-177">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="40717-178">redirectUrl</span><span class="sxs-lookup"><span data-stu-id="40717-178">redirectUrl</span></span> | <span data-ttu-id="40717-179">옵션 (기본값은 null)입니다. 인증 성공 시 브라우저를 리디렉션할 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-179">Optional (defaults to null).The URL to redirect the browser to upon successful authentication.</span></span> <span data-ttu-id="40717-180">이 매개 변수가 null 또는 빈 문자열인 경우 없습니다 리디렉션이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-180">If this parameter is null or an empty string, no redirection occurs.</span></span> |
| <span data-ttu-id="40717-181">logoutCompletedCallback</span><span class="sxs-lookup"><span data-stu-id="40717-181">logoutCompletedCallback</span></span> | <span data-ttu-id="40717-182">옵션 (기본값은 null)입니다. 함수는 로그 아웃 성공적으로 완료 되 면입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-182">Optional (defaults to null).The function to call when the logout has successfully completed.</span></span> <span data-ttu-id="40717-183">를 지정 하는 경우이 매개 변수 defaultLogoutCompleted 속성을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-183">If specified, this parameter overrides the defaultLogoutCompleted property.</span></span> |
| <span data-ttu-id="40717-184">failedCallback</span><span class="sxs-lookup"><span data-stu-id="40717-184">failedCallback</span></span> | <span data-ttu-id="40717-185">옵션 (기본값은 null)입니다. 로그인에 실패 한 경우 호출 하는 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-185">Optional (defaults to null).The function to call when the login has failed.</span></span> <span data-ttu-id="40717-186">를 지정 하는 경우이 매개 변수 defaultFailedCallback 속성을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-186">If specified, this parameter overrides the defaultFailedCallback property.</span></span> |
| <span data-ttu-id="40717-187">userContext</span><span class="sxs-lookup"><span data-stu-id="40717-187">userContext</span></span> | <span data-ttu-id="40717-188">옵션 (기본값은 null)입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-188">Optional (defaults to null).</span></span> <span data-ttu-id="40717-189">콜백 함수에 전달 되어야 하는 사용자 지정 사용자 컨텍스트 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-189">Custom user context data that should be passed to the callback functions.</span></span> |

<span data-ttu-id="40717-190">*반환 값:*</span><span class="sxs-lookup"><span data-stu-id="40717-190">*Return Value:*</span></span>

<span data-ttu-id="40717-191">이 함수는 반환 값을 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="40717-191">This function does not include a return value.</span></span> <span data-ttu-id="40717-192">그러나 동작의 수를이 함수로 호출 완료 시 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40717-192">However, a number of behaviors are included upon completion of a call to this function:</span></span>

- <span data-ttu-id="40717-193">현재 페이지를 새로 고칠 수 있거나 또는 경우 변경할 수는 `redirectUrl` 매개 변수를 null 또는 빈 문자열이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="40717-193">The current page will either be refreshed or be changed if the `redirectUrl` parameter was neither null nor an empty string.</span></span>
- <span data-ttu-id="40717-194">그러나 매개 변수가 null 이거나 빈 문자열이 면 되었으면는 `logoutCompletedCallback` 매개 변수 또는 `defaultLogoutCompletedCallback` 속성이 호출 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="40717-194">However, if the parameter was null or an empty string, the `logoutCompletedCallback` parameter, or `defaultLogoutCompletedCallback` property is called.</span></span>
- <span data-ttu-id="40717-195">웹 서비스 호출에 실패 하는 경우는 `failedCallback` 의 매개 변수 `defaultFailedCallback` 속성이 호출 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="40717-195">If the call to the web service fails, the `failedCallback` parameter of `defaultFailedCallback` property is called.</span></span>

<span data-ttu-id="40717-196">*defaultFailedCallback 속성 (get, set):*</span><span class="sxs-lookup"><span data-stu-id="40717-196">*defaultFailedCallback property (get, set):*</span></span>

<span data-ttu-id="40717-197">이 속성을 호출 해야 웹 서비스와 통신 하는 오류가 발생 하는 함수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-197">This property specifies a function that should be called if a failure to communicate with the web service occurs.</span></span> <span data-ttu-id="40717-198">대리자 (또는 함수 참조) 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-198">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="40717-199">이 속성에 지정 된 함수 참조에는 다음 서명이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-199">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample2.js)]

<span data-ttu-id="40717-200">*매개 변수:*</span><span class="sxs-lookup"><span data-stu-id="40717-200">*Parameters:*</span></span>

| <span data-ttu-id="40717-201">**매개 변수 이름**</span><span class="sxs-lookup"><span data-stu-id="40717-201">**Parameter Name**</span></span> | <span data-ttu-id="40717-202">**의미**</span><span class="sxs-lookup"><span data-stu-id="40717-202">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="40717-203">오류</span><span class="sxs-lookup"><span data-stu-id="40717-203">error</span></span> | <span data-ttu-id="40717-204">오류 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-204">Specifies the error information.</span></span> |
| <span data-ttu-id="40717-205">userContext</span><span class="sxs-lookup"><span data-stu-id="40717-205">userContext</span></span> | <span data-ttu-id="40717-206">로그인 또는 로그 아웃 함수를 호출할 때 제공 하는 사용자 컨텍스트 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-206">Specifies the user context information provided when the login or logout function was called.</span></span> |
| <span data-ttu-id="40717-207">MethodName</span><span class="sxs-lookup"><span data-stu-id="40717-207">methodName</span></span> | <span data-ttu-id="40717-208">호출 메서드의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-208">The name of the calling method.</span></span> |

<span data-ttu-id="40717-209">*defaultLoginCompletedCallback 속성 (get, set):*</span><span class="sxs-lookup"><span data-stu-id="40717-209">*defaultLoginCompletedCallback property (get, set):*</span></span>

<span data-ttu-id="40717-210">이 속성에서 로그인 웹 서비스 호출이 완료 하는 때를 호출 해야 하는 함수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-210">This property specifies a function that should be called when the login web service call has completed.</span></span> <span data-ttu-id="40717-211">대리자 (또는 함수 참조) 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-211">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="40717-212">이 속성에 지정 된 함수 참조에는 다음 서명이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-212">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample3.js)]

<span data-ttu-id="40717-213">*매개 변수:*</span><span class="sxs-lookup"><span data-stu-id="40717-213">*Parameters:*</span></span>

| <span data-ttu-id="40717-214">**매개 변수 이름**</span><span class="sxs-lookup"><span data-stu-id="40717-214">**Parameter Name**</span></span> | <span data-ttu-id="40717-215">**의미**</span><span class="sxs-lookup"><span data-stu-id="40717-215">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="40717-216">validCredentials</span><span class="sxs-lookup"><span data-stu-id="40717-216">validCredentials</span></span> | <span data-ttu-id="40717-217">사용자 올바른 자격 증명을 제공 하는지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-217">Specifies whether the user provided valid credentials.</span></span> <span data-ttu-id="40717-218">`true`사용자가 성공적으로;에 로그인 하는 경우 그렇지 않으면 `false`합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-218">`true` if the user successfully logged in; otherwise `false`.</span></span> |
| <span data-ttu-id="40717-219">userContext</span><span class="sxs-lookup"><span data-stu-id="40717-219">userContext</span></span> | <span data-ttu-id="40717-220">로그인 함수를 호출할 때 제공 하는 사용자 컨텍스트 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-220">Specifies the user context information provided when the login function was called.</span></span> |
| <span data-ttu-id="40717-221">MethodName</span><span class="sxs-lookup"><span data-stu-id="40717-221">methodName</span></span> | <span data-ttu-id="40717-222">호출 메서드의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-222">The name of the calling method.</span></span> |

<span data-ttu-id="40717-223">*defaultLogoutCompletedCallback 속성 (get, set):*</span><span class="sxs-lookup"><span data-stu-id="40717-223">*defaultLogoutCompletedCallback property (get, set):*</span></span>

<span data-ttu-id="40717-224">이 속성에서 로그 아웃 웹 서비스 호출이 완료 하는 때를 호출 해야 하는 함수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-224">This property specifies a function that should be called when the logout web service call has completed.</span></span> <span data-ttu-id="40717-225">대리자 (또는 함수 참조) 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-225">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="40717-226">이 속성에 지정 된 함수 참조에는 다음 서명이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-226">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample4.js)]

<span data-ttu-id="40717-227">*매개 변수:*</span><span class="sxs-lookup"><span data-stu-id="40717-227">*Parameters:*</span></span>

| <span data-ttu-id="40717-228">**매개 변수 이름**</span><span class="sxs-lookup"><span data-stu-id="40717-228">**Parameter Name**</span></span> | <span data-ttu-id="40717-229">**의미**</span><span class="sxs-lookup"><span data-stu-id="40717-229">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="40717-230">결과</span><span class="sxs-lookup"><span data-stu-id="40717-230">result</span></span> | <span data-ttu-id="40717-231">이 매개 변수는 항상 됩니다 `null`; 나중에 사용 하도록 예약 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40717-231">This parameter will always be `null`; it is reserved for future use.</span></span> |
| <span data-ttu-id="40717-232">userContext</span><span class="sxs-lookup"><span data-stu-id="40717-232">userContext</span></span> | <span data-ttu-id="40717-233">로그인 함수를 호출할 때 제공 하는 사용자 컨텍스트 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-233">Specifies the user context information provided when the login function was called.</span></span> |
| <span data-ttu-id="40717-234">MethodName</span><span class="sxs-lookup"><span data-stu-id="40717-234">methodName</span></span> | <span data-ttu-id="40717-235">호출 메서드의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-235">The name of the calling method.</span></span> |

<span data-ttu-id="40717-236">*isLoggedIn 속성 (get):*</span><span class="sxs-lookup"><span data-stu-id="40717-236">*isLoggedIn property (get):*</span></span>

<span data-ttu-id="40717-237">이 속성; 사용자의 현재 인증 상태를 가져옵니다. 페이지를 요청 하는 동안 ScriptManager 개체에 의해 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40717-237">This property gets the current authentication state of the user; it is set by the ScriptManager object during a page request.</span></span>

<span data-ttu-id="40717-238">이 속성은 반환 `true` 반환, 이상이 아니면 사용자가 로그인 한 현재, `false`합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-238">This property returns `true` if the user is currently logged in; otherwise, it returns `false`.</span></span>

<span data-ttu-id="40717-239">*경로 속성 (get, set):*</span><span class="sxs-lookup"><span data-stu-id="40717-239">*path property (get, set):*</span></span>

<span data-ttu-id="40717-240">이 속성은 프로그래밍 방식으로 인증 웹 서비스의 위치를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-240">This property programmatically determines the location of the authentication web service.</span></span> <span data-ttu-id="40717-241">기본 인증 공급자 뿐만 아니라 하나 재정의를 사용할 수 있습니다 ScriptManager 컨트롤 AuthenticationService 자식 노드의 경로 속성에서 선언적으로 설정 (자세한 내용은 참조는 사용 하 여 사용자 지정 인증 서비스 공급자 아래 항목)입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-241">It can be used to override the default authentication provider, as well as one set declaratively in the Path property of the ScriptManager control's AuthenticationService child node (for more information, see the Using a Custom Authentication Service Provider topic below).</span></span>

<span data-ttu-id="40717-242">기본 인증 서비스의 위치는 변경 되지 않는 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-242">Note that the location of the default authentication service does not change.</span></span> <span data-ttu-id="40717-243">그러나 ASP.NET AJAX를 사용 하는 ASP.NET AJAX 인증 서비스 프록시라고 동일한 클래스 인터페이스를 제공 하는 웹 서비스의 위치를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40717-243">However, ASP.NET AJAX allows you to specify the location of a web service that provides the same class interface as the ASP.NET AJAX authentication service proxy.</span></span>

<span data-ttu-id="40717-244">Note 또한이 속성을 현재 사이트에서 스크립트 요청 하도록 지시 하는 값으로 설정할 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-244">Note also that this property should not be set to a value that directs the script request off of the current site.</span></span> <span data-ttu-id="40717-245">현재 응용 프로그램은 인증 자격 증명을 수신 하지,는 것이 의미가 없습니다. 또한 기술 기본 AJAX 교차 사이트 요청을 게시 해야 하 고 클라이언트 브라우저에서 보안 예외를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40717-245">Because the current application would not receive the authentication credentials, it would be useless; also, the technology underlying AJAX should not post cross-site requests, and may generate a security exception in the client browser.</span></span>

<span data-ttu-id="40717-246">이 속성은 한 `String` 인증 웹 서비스에 경로 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-246">This property is a `String` object representing the path to the authentication web service.</span></span>

<span data-ttu-id="40717-247">*timeout 속성 (get, set):*</span><span class="sxs-lookup"><span data-stu-id="40717-247">*timeout property (get, set):*</span></span>

<span data-ttu-id="40717-248">이 속성 실패 인증 서비스에 대 한 로그인 요청 가정 하기 전에 대기 하는 시간 길이 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-248">This property determines the length of time to wait for the authentication service before assuming the login request has failed.</span></span> <span data-ttu-id="40717-249">호출이 완료 되기를 기다리는 동안 제한 시간이 만료 되 면 요청이 실패 한 콜백이 호출 수, 하 고 호출이 완료 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="40717-249">If the timeout expires while waiting for a call to complete, the request-failed callback will be called, and the call will not complete.</span></span>

<span data-ttu-id="40717-250">이 속성은 한 `Number` 인증 서비스에서 결과를 기다릴 밀리초 수를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-250">This property is a `Number` object representing the number of milliseconds to wait for results from the authentication service.</span></span>

<span data-ttu-id="40717-251">*인증 서비스에 로그인 하는 코드 샘플:*</span><span class="sxs-lookup"><span data-stu-id="40717-251">*Code Sample: Logging into the Authentication Service*</span></span>

<span data-ttu-id="40717-252">다음 태그는 간단한 스크립트 AuthenticationService 클래스의 로그인 및 로그 아웃 메서드 호출으로 예제 ASP.NET 페이지.</span><span class="sxs-lookup"><span data-stu-id="40717-252">The following markup is an example ASP.NET page with a simple script call to the login and logout methods of the AuthenticationService class.</span></span>

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample5.aspx)]

## <a name="accessing-aspnet-profiling-data-via-ajax"></a><span data-ttu-id="40717-253">ASP.NET AJAX 통한 데이터 프로 파일링에 액세스</span><span class="sxs-lookup"><span data-stu-id="40717-253">Accessing ASP.NET Profiling Data via AJAX</span></span>

<span data-ttu-id="40717-254">ASP.NET 서비스를 프로 파일링은 ASP.NET AJAX 확장을 통해 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40717-254">The ASP.NET profiling service is also exposed through the ASP.NET AJAX Extensions.</span></span> <span data-ttu-id="40717-255">사용자 데이터 저장 및 검색에 사용 되는 다양 하 고 세부적인 API를 제공 하는 ASP.NET 프로 파일링 서비스, 이후이 우수한 생산성 도구를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40717-255">Since the ASP.NET profiling service provides a rich, granular API by which to store and retrieve user data, this can be an excellent productivity tool.</span></span>

<span data-ttu-id="40717-256">Web.config; 프로필 서비스를 사용할 수 있어야 합니다. 기본적으로는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="40717-256">The profile service must be enabled in web.config; it is not by default.</span></span> <span data-ttu-id="40717-257">이렇게 하려면는 `profileService` 자식 요소를 사용 = true에 지정 된 web.config 및 읽거나 다음과 같이 작성 되는 속성 수를 지정 했는지:</span><span class="sxs-lookup"><span data-stu-id="40717-257">To do so, ensure that the `profileService` child element has enabled= true specified in web.config, and that you have specified which properties can be read or written as follows:</span></span>

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample6.xml)]

<span data-ttu-id="40717-258">프로필 서비스 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-258">The profile service must also be configured.</span></span> <span data-ttu-id="40717-259">이 백서 범위 밖에 서 프로 파일링 서비스의 구성 이지만, 구성 설정 프로필에에서 정의 된 그룹 그룹 이름의 하위 속성으로 액세스할 수 있는지 확인 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="40717-259">Although configuration of the profiling service is outside of the scope of this whitepaper, it is worthwhile to note that groups as defined in profile configuration settings will be accessible as sub-properties of the group name.</span></span> <span data-ttu-id="40717-260">예를 들어 지정 된 다음 프로필 섹션와:</span><span class="sxs-lookup"><span data-stu-id="40717-260">For example, with the following profile section specified:</span></span>

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample7.xml)]

<span data-ttu-id="40717-261">클라이언트 스크립트 ProfileService 클래스의 속성 필드의 속성으로 이름, Address.Line1, Address.Line2, Address.City, Address.State, Address.Zip, 및 BackgroundColor 액세스할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40717-261">Client script would be able to access Name, Address.Line1, Address.Line2, Address.City, Address.State, Address.Zip, and BackgroundColor as properties of the properties field of the ProfileService class.</span></span>

<span data-ttu-id="40717-262">AJAX 프로 파일링 서비스를 구성한 후 즉시; 페이지에서 사용할 수 있습니다. 그러나 사용 하기 전에 한 번 로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-262">Once the AJAX Profiling Service is configured, it will be immediately available in pages; however, it will have to be loaded once before use.</span></span>

<span data-ttu-id="40717-263">*Sys.Services.ProfileService 멤버*</span><span class="sxs-lookup"><span data-stu-id="40717-263">*Sys.Services.ProfileService members*</span></span>

<span data-ttu-id="40717-264">*속성 필드:*</span><span class="sxs-lookup"><span data-stu-id="40717-264">*properties field:*</span></span>

<span data-ttu-id="40717-265">속성 필드 점 연산자 이름 규칙에 의해 참조 될 수 있는 자식 속성으로 모든 구성 된 프로필 데이터를 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-265">The properties field exposes all configured profile data as child properties that can be referenced by the dot-operator-name convention.</span></span> <span data-ttu-id="40717-266">속성 그룹의 자식 속성은 GroupName.PropertyName 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-266">Properties that are children of property groups are referred to as GroupName.PropertyName.</span></span> <span data-ttu-id="40717-267">사용자의 상태를 가져오려면 위에서 설명한 예에서는 프로필 구성에서는 다음 식별자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40717-267">In the example profile configuration presented above, to get the state of the user, you could use the following identifier:</span></span>

[!code-csharp[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample8.cs)]

<span data-ttu-id="40717-268">*load 메서드:*</span><span class="sxs-lookup"><span data-stu-id="40717-268">*load method:*</span></span>

<span data-ttu-id="40717-269">서버에서 선택한 목록 또는 모든 속성을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-269">Loads a selected list or all properties from the server.</span></span>

<span data-ttu-id="40717-270">*매개 변수:*</span><span class="sxs-lookup"><span data-stu-id="40717-270">*Parameters:*</span></span>

| <span data-ttu-id="40717-271">**매개 변수 이름**</span><span class="sxs-lookup"><span data-stu-id="40717-271">**Parameter Name**</span></span> | <span data-ttu-id="40717-272">**의미**</span><span class="sxs-lookup"><span data-stu-id="40717-272">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="40717-273">propertyNames</span><span class="sxs-lookup"><span data-stu-id="40717-273">propertyNames</span></span> | <span data-ttu-id="40717-274">옵션 (기본값은 null)입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-274">Optional (defaults to null).</span></span> <span data-ttu-id="40717-275">서버에서 로드 되도록 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-275">The properties to be loaded from the server.</span></span> |
| <span data-ttu-id="40717-276">loadCompletedCallback</span><span class="sxs-lookup"><span data-stu-id="40717-276">loadCompletedCallback</span></span> | <span data-ttu-id="40717-277">옵션 (기본값은 null)입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-277">Optional (defaults to null).</span></span> <span data-ttu-id="40717-278">로드가 완료 되 면 호출할 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-278">The function to call when loading has completed.</span></span> |
| <span data-ttu-id="40717-279">failedCallback</span><span class="sxs-lookup"><span data-stu-id="40717-279">failedCallback</span></span> | <span data-ttu-id="40717-280">옵션 (기본값은 null)입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-280">Optional (defaults to null).</span></span> <span data-ttu-id="40717-281">오류가 발생 한 경우 호출 하는 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-281">The function to call if an error occurs.</span></span> |
| <span data-ttu-id="40717-282">userContext</span><span class="sxs-lookup"><span data-stu-id="40717-282">userContext</span></span> | <span data-ttu-id="40717-283">옵션 (기본값은 null)입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-283">Optional (defaults to null).</span></span> <span data-ttu-id="40717-284">콜백 함수에 전달 될 컨텍스트 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-284">Context information to be passed to the callback function.</span></span> |

<span data-ttu-id="40717-285">Load 함수에는 반환 값이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="40717-285">The load function does not have a return value.</span></span> <span data-ttu-id="40717-286">경우 호출이 성공적으로 완료를 호출 합니다 중 하나는 `loadCompletedCallback` 매개 변수 또는 `defaultLoadCompletedCallback` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-286">If the call completed successfully, it will call either the `loadCompletedCallback` parameter or `defaultLoadCompletedCallback` property.</span></span> <span data-ttu-id="40717-287">또는 호출이 실패 하거나 제한 시간이 만료 되는 경우는 `failedCallback` 매개 변수 또는 `defaultFailedCallback` 속성이 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-287">If the call failed, or the timeout expired, either the `failedCallback` parameter or `defaultFailedCallback` property will be called.</span></span>

<span data-ttu-id="40717-288">경우는 `propertyNames` 매개 변수가 제공 되지 않으면, 모든 읽기로 구성 된 속성은 서버에서 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-288">If the `propertyNames` parameter is not supplied, all read-configured properties are retrieved from the server.</span></span>

<span data-ttu-id="40717-289">*save 메서드:*</span><span class="sxs-lookup"><span data-stu-id="40717-289">*save method:*</span></span>

<span data-ttu-id="40717-290">Save () 메서드는 사용자의 ASP.NET 프로필에 지정 된 속성 목록 (또는 모든 속성)를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-290">The save() method saves the specified property list (or all properties) to the user's ASP.NET profile.</span></span>

<span data-ttu-id="40717-291">*매개 변수:*</span><span class="sxs-lookup"><span data-stu-id="40717-291">*Parameters:*</span></span>

| <span data-ttu-id="40717-292">**매개 변수 이름**</span><span class="sxs-lookup"><span data-stu-id="40717-292">**Parameter Name**</span></span> | <span data-ttu-id="40717-293">**의미**</span><span class="sxs-lookup"><span data-stu-id="40717-293">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="40717-294">propertyNames</span><span class="sxs-lookup"><span data-stu-id="40717-294">propertyNames</span></span> | <span data-ttu-id="40717-295">옵션 (기본값은 null)입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-295">Optional (defaults to null).</span></span> <span data-ttu-id="40717-296">속성은 서버에 저장할 수입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-296">The properties to be saved to the server.</span></span> |
| <span data-ttu-id="40717-297">saveCompletedCallback</span><span class="sxs-lookup"><span data-stu-id="40717-297">saveCompletedCallback</span></span> | <span data-ttu-id="40717-298">옵션 (기본값은 null)입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-298">Optional (defaults to null).</span></span> <span data-ttu-id="40717-299">저장할 때 호출할 함수를 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="40717-299">The function to call when saving has completed.</span></span> |
| <span data-ttu-id="40717-300">failedCallback</span><span class="sxs-lookup"><span data-stu-id="40717-300">failedCallback</span></span> | <span data-ttu-id="40717-301">옵션 (기본값은 null)입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-301">Optional (defaults to null).</span></span> <span data-ttu-id="40717-302">오류가 발생 한 경우 호출 하는 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-302">The function to call if an error occurs.</span></span> |
| <span data-ttu-id="40717-303">userContext</span><span class="sxs-lookup"><span data-stu-id="40717-303">userContext</span></span> | <span data-ttu-id="40717-304">옵션 (기본값은 null)입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-304">Optional (defaults to null).</span></span> <span data-ttu-id="40717-305">콜백 함수에 전달 될 컨텍스트 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-305">Context information to be passed to the callback function.</span></span> |

<span data-ttu-id="40717-306">저장 함수 반환 값이 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-306">The save function does not have a return value.</span></span> <span data-ttu-id="40717-307">호출이 성공적으로 완료 되는 호출 하는 것 중 하나는 `saveCompletedCallback` 매개 변수 또는 `defaultSaveCompletedCallback` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-307">If the call completes successfully, it will call either the `saveCompletedCallback` parameter or `defaultSaveCompletedCallback` property.</span></span> <span data-ttu-id="40717-308">또는 호출이 실패 하거나 제한 시간이 만료 되는 경우는 `failedCallback` 또는 `defaultFailedCallback` 속성이 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-308">If the call failed, or the timeout expired, either the `failedCallback` or `defaultFailedCallback` property will be called.</span></span>

<span data-ttu-id="40717-309">경우는 `propertyNames` 매개 변수는 null, 모든 프로필 속성은 서버에 전송 되 고 서버 속성을 저장할 수 있습니다 및 그렇지 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40717-309">If the `propertyNames` parameter is null, all profile properties will be sent to the server, and the server will decide which properties can be saved and which cannot.</span></span>

<span data-ttu-id="40717-310">*defaultFailedCallback 속성 (get, set):*</span><span class="sxs-lookup"><span data-stu-id="40717-310">*defaultFailedCallback property (get, set):*</span></span>

<span data-ttu-id="40717-311">이 속성을 호출 해야 웹 서비스와 통신 하는 오류가 발생 하는 함수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-311">This property specifies a function that should be called if a failure to communicate with the web service occurs.</span></span> <span data-ttu-id="40717-312">대리자 (또는 함수 참조) 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-312">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="40717-313">이 속성에 지정 된 함수 참조에는 다음 서명이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-313">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample9.js)]

<span data-ttu-id="40717-314">*매개 변수:*</span><span class="sxs-lookup"><span data-stu-id="40717-314">*Parameters:*</span></span>

| <span data-ttu-id="40717-315">**매개 변수 이름**</span><span class="sxs-lookup"><span data-stu-id="40717-315">**Parameter Name**</span></span> | <span data-ttu-id="40717-316">**의미**</span><span class="sxs-lookup"><span data-stu-id="40717-316">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="40717-317">오류</span><span class="sxs-lookup"><span data-stu-id="40717-317">Error</span></span> | <span data-ttu-id="40717-318">오류 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-318">Specifies the error information.</span></span> |
| <span data-ttu-id="40717-319">userContext</span><span class="sxs-lookup"><span data-stu-id="40717-319">userContext</span></span> | <span data-ttu-id="40717-320">될 때 제공 하는 사용자 컨텍스트 정보를 지정 합니다. 부하 저장 함수 호출 했습니다.</span><span class="sxs-lookup"><span data-stu-id="40717-320">Specifies the user context information provided when the load or save function was called.</span></span> |
| <span data-ttu-id="40717-321">MethodName</span><span class="sxs-lookup"><span data-stu-id="40717-321">methodName</span></span> | <span data-ttu-id="40717-322">호출 메서드의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-322">The name of the calling method.</span></span> |

<span data-ttu-id="40717-323">*defaultSaveCompleted 속성 (get, set):*</span><span class="sxs-lookup"><span data-stu-id="40717-323">*defaultSaveCompleted property (get, set):*</span></span>

<span data-ttu-id="40717-324">이 속성은 사용자의 프로필 데이터를 저장 완료 될 때 호출 해야 하는 함수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-324">This property specifies a function that should be called upon the completion of saving the user's profile data.</span></span> <span data-ttu-id="40717-325">대리자 (또는 함수 참조) 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-325">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="40717-326">이 속성에 지정 된 함수 참조에는 다음 서명이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-326">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample10.js)]

<span data-ttu-id="40717-327">*매개 변수:*</span><span class="sxs-lookup"><span data-stu-id="40717-327">*Parameters:*</span></span>

| <span data-ttu-id="40717-328">**매개 변수 이름**</span><span class="sxs-lookup"><span data-stu-id="40717-328">**Parameter Name**</span></span> | <span data-ttu-id="40717-329">**의미**</span><span class="sxs-lookup"><span data-stu-id="40717-329">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="40717-330">numPropsSaved</span><span class="sxs-lookup"><span data-stu-id="40717-330">numPropsSaved</span></span> | <span data-ttu-id="40717-331">저장 된 속성의 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-331">Specifies the number of properties that were saved.</span></span> |
| <span data-ttu-id="40717-332">userContext</span><span class="sxs-lookup"><span data-stu-id="40717-332">userContext</span></span> | <span data-ttu-id="40717-333">될 때 제공 하는 사용자 컨텍스트 정보를 지정 합니다. 부하 저장 함수 호출 했습니다.</span><span class="sxs-lookup"><span data-stu-id="40717-333">Specifies the user context information provided when the load or save function was called.</span></span> |
| <span data-ttu-id="40717-334">MethodName</span><span class="sxs-lookup"><span data-stu-id="40717-334">methodName</span></span> | <span data-ttu-id="40717-335">호출 메서드의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-335">The name of the calling method.</span></span> |

<span data-ttu-id="40717-336">*defaultLoadCompleted 속성 (get, set):*</span><span class="sxs-lookup"><span data-stu-id="40717-336">*defaultLoadCompleted property (get, set):*</span></span>

<span data-ttu-id="40717-337">이 속성에는 사용자의 프로필 데이터 로드가 완료 될 때 호출 해야 하는 함수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-337">This property specifies a function that should be called upon the completion of loading of the user's profile data.</span></span> <span data-ttu-id="40717-338">대리자 (또는 함수 참조) 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-338">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="40717-339">이 속성에 지정 된 함수 참조에는 다음 서명이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-339">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample11.js)]

<span data-ttu-id="40717-340">*매개 변수:*</span><span class="sxs-lookup"><span data-stu-id="40717-340">*Parameters:*</span></span>

| <span data-ttu-id="40717-341">**매개 변수 이름**</span><span class="sxs-lookup"><span data-stu-id="40717-341">**Parameter Name**</span></span> | <span data-ttu-id="40717-342">**의미**</span><span class="sxs-lookup"><span data-stu-id="40717-342">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="40717-343">numPropsLoaded</span><span class="sxs-lookup"><span data-stu-id="40717-343">numPropsLoaded</span></span> | <span data-ttu-id="40717-344">로드 되는 속성의 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-344">Specifies the number of properties loaded.</span></span> |
| <span data-ttu-id="40717-345">userContext</span><span class="sxs-lookup"><span data-stu-id="40717-345">userContext</span></span> | <span data-ttu-id="40717-346">될 때 제공 하는 사용자 컨텍스트 정보를 지정 합니다. 부하 저장 함수 호출 했습니다.</span><span class="sxs-lookup"><span data-stu-id="40717-346">Specifies the user context information provided when the load or save function was called.</span></span> |
| <span data-ttu-id="40717-347">MethodName</span><span class="sxs-lookup"><span data-stu-id="40717-347">methodName</span></span> | <span data-ttu-id="40717-348">호출 메서드의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-348">The name of the calling method.</span></span> |

<span data-ttu-id="40717-349">*경로 속성 (get, set):*</span><span class="sxs-lookup"><span data-stu-id="40717-349">*path property (get, set):*</span></span>

<span data-ttu-id="40717-350">프로그래밍 방식으로이 속성 프로필 웹 서비스의 위치를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-350">This property programmatically determines the location of the profile web service.</span></span> <span data-ttu-id="40717-351">기본 프로필 서비스 공급자 뿐만 아니라 하나 재정의를 사용할 수 있습니다 ScriptManager 컨트롤 ProfileService 자식 노드의 경로 속성에서 선언적으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-351">It can be used to override the default profile service provider, as well as one set declaratively in the Path property of the ScriptManager control's ProfileService child node.</span></span>

<span data-ttu-id="40717-352">기본 프로필 서비스의 위치는 변경 되지 않는 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-352">Note that the location of the default profile service does not change.</span></span> <span data-ttu-id="40717-353">그러나 ASP.NET AJAX를 사용 하는 ASP.NET AJAX 인증 서비스 프록시라고 동일한 클래스 인터페이스를 제공 하는 웹 서비스의 위치를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40717-353">However, ASP.NET AJAX allows you to specify the location of a web service that provides the same class interface as the ASP.NET AJAX authentication service proxy.</span></span>

<span data-ttu-id="40717-354">Note 또한이 속성을 현재 사이트에서 스크립트 요청 하도록 지시 하는 값으로 설정할 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-354">Note also that this property should not be set to a value that directs the script request off of the current site.</span></span> <span data-ttu-id="40717-355">기술 기본 AJAX 교차 사이트 요청을 (를) 게시할 해야 및 클라이언트 브라우저에서 보안 예외를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40717-355">The technology underlying AJAX should not post cross-site requests, and may generate a security exception in the client browser.</span></span>

<span data-ttu-id="40717-356">이 속성은 한 `String` 프로필 웹 서비스에 경로 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-356">This property is a `String` object representing the path to the profile web service.</span></span>

<span data-ttu-id="40717-357">*timeout 속성 (get, set):*</span><span class="sxs-lookup"><span data-stu-id="40717-357">*timeout property (get, set):*</span></span>

<span data-ttu-id="40717-358">이 속성 시간 프로필 서비스에 대 한 부하를 가정 하기 전에 기다리거나 요청 저장 실패를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-358">This property determines the length of time to wait for the profile service before assuming the load or save request has failed.</span></span> <span data-ttu-id="40717-359">호출이 완료 되기를 기다리는 동안 제한 시간이 만료 되 면 요청이 실패 한 콜백이 호출 수, 하 고 호출이 완료 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="40717-359">If the timeout expires while waiting for a call to complete, the request-failed callback will be called, and the call will not complete.</span></span>

<span data-ttu-id="40717-360">이 속성은 한 `Number` 프로필 서비스의 결과 기다릴 밀리초 수를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="40717-360">This property is a `Number` object representing the number of milliseconds to wait for results from the profile service.</span></span>

<span data-ttu-id="40717-361">*코드 샘플: 페이지가 로드 될 때 프로필 데이터를 로드 합니다.*</span><span class="sxs-lookup"><span data-stu-id="40717-361">*Code sample: Loading profile data at page load*</span></span>

<span data-ttu-id="40717-362">다음 코드는 사용자가 인증 여부를 확인 합니다 있으며이 경우는 페이지와 사용자의 기본 배경색을 로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40717-362">The following code will check to see whether a user is authenticated, and if so, will load the user's preferred background color as the page's.</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample12.js)]

## <a name="using-a-custom-authentication-service-provider"></a><span data-ttu-id="40717-363">*사용자 지정 인증 서비스 공급자를 사용 하 여*</span><span class="sxs-lookup"><span data-stu-id="40717-363">*Using a Custom Authentication Service Provider*</span></span>

<span data-ttu-id="40717-364">ASP.NET AJAX 확장을 사용 하 여 기능 사용자 지정 웹 서비스를 통해 노출 하 여 사용자 지정 스크립트 인증 서비스 공급자를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40717-364">The ASP.NET AJAX Extensions allow you to create a custom script authentication service provider by exposing your functionality through a custom web service.</span></span> <span data-ttu-id="40717-365">웹 서비스를 사용 하려면 두 메서드를 노출 해야 합니다 `Login` 및 `Logout`; 기본 ASP.NET AJAX 인증 웹 서비스와 동일한 메서드 서명을 사용 하 여 이러한 메서드를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-365">In order to be used, your web service must expose two methods, `Login` and `Logout`; and these methods must be specified with the same method signatures as the default ASP.NET AJAX Authentication web service.</span></span>

<span data-ttu-id="40717-366">사용자 지정 웹 서비스를 만든 후에 코드에서 프로그래밍 방식으로 또는 클라이언트 스크립트를 통해 페이지에서 선언적으로 것에 대 한 경로 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-366">Once you have created the custom web service, you will need to specify the path to it, either declaratively on your page, programmatically in code, or via the client script.</span></span>

<span data-ttu-id="40717-367">*선언적으로 경로 설정 하려면:*</span><span class="sxs-lookup"><span data-stu-id="40717-367">*To set the path declaratively:*</span></span>

<span data-ttu-id="40717-368">경로 선언적으로 설정 하려면 ASP.NET 페이지에 ScriptManager 개체의 AuthenticationService 자식 포함.</span><span class="sxs-lookup"><span data-stu-id="40717-368">To set the path declaratively, include the AuthenticationService child of the ScriptManager object on your ASP.NET page:</span></span>

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample13.aspx)]

<span data-ttu-id="40717-369">*코드에서 경로 설정 합니다.*</span><span class="sxs-lookup"><span data-stu-id="40717-369">*To set the path in code:*</span></span>

<span data-ttu-id="40717-370">경로 프로그래밍 방식으로 설정 하려면 스크립트 관리자의 인스턴스를 통해 경로 지정:</span><span class="sxs-lookup"><span data-stu-id="40717-370">To set the path programmatically, specify the path via the instance of your script manager:</span></span>

[!code-csharp[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample14.cs)]

<span data-ttu-id="40717-371">*스크립트에서 경로 설정 합니다 하:*</span><span class="sxs-lookup"><span data-stu-id="40717-371">*To set the path in script:*</span></span>

<span data-ttu-id="40717-372">경로 설정 하려면 프로그래밍 방식으로 스크립트에 사용 된 `path` AuthenticationService 클래스의 속성:</span><span class="sxs-lookup"><span data-stu-id="40717-372">To set the path programmatically in script, utilize the `path` property of the AuthenticationService class:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample15.js)]

<span data-ttu-id="40717-373">*사용자 지정 인증에 대 한 샘플 웹 서비스*</span><span class="sxs-lookup"><span data-stu-id="40717-373">*Sample Web Service for Custom Authentication*</span></span>

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample16.aspx)]

## <a name="summary"></a><span data-ttu-id="40717-374">요약</span><span class="sxs-lookup"><span data-stu-id="40717-374">Summary</span></span>

<span data-ttu-id="40717-375">ASP.NET 서비스-특히 프로 파일링, 구성원 자격 및 인증 서비스-클라이언트 브라우저에서 JavaScript에 쉽게 노출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40717-375">ASP.NET services - specifically the profiling, membership, and authentication services - are easily exposed to JavaScript on the client browser.</span></span> <span data-ttu-id="40717-376">따라서 개발자는 작업을 수행 하는 적어지므로 등의 컨트롤에 의존 하지 않고 인증 메커니즘으로 클라이언트 쪽 코드 원활 하 게 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40717-376">This allows developers to integrate their client-side code with the authentication mechanism seamlessly, without depending on controls such as UpdatePanels to do the heavy lifting.</span></span> <span data-ttu-id="40717-377">웹 구성 설정을; 활용 하 여 프로필 데이터도 클라이언트로부터 보호할 수 있습니다. 데이터를 사용할 수 기본적으로 개발자 해야에 옵트인 프로필 속성.</span><span class="sxs-lookup"><span data-stu-id="40717-377">Profile data can be protected from the client as well, by utilizing web configuration settings; no data is available by default, and developers must opt-in to profile properties.</span></span>

<span data-ttu-id="40717-378">또한 해당 하는 메서드 서명을 사용 하 여 간단한 웹 서비스 구현을 만들어서 개발자는 이러한 기본 ASP.NET 서비스에 대 한 사용자 지정 스크립트 공급자를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40717-378">Furthermore, by creating simplified web service implementations with equivalent method signatures, developers can create custom script providers for these intrinsic ASP.NET services.</span></span> <span data-ttu-id="40717-379">이러한 기술에 대 한 지원을 동시에 개발자가 다양 한 특정 요구 사항에 맞게 유연성에 제공할 리치 클라이언트 응용 프로그램의 배포를 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-379">Support for these techniques simplifies the development of rich client applications, while providing developers with a wide range of flexibility to meet specific needs.</span></span>

## <a name="bio"></a><span data-ttu-id="40717-380">*약력*</span><span class="sxs-lookup"><span data-stu-id="40717-380">*Bio*</span></span>

<span data-ttu-id="40717-381">Scott 인증서의 근무 기간이 Microsoft 웹 기술을 1997 년부터 이며 myKB.com 부서장 ([www.myKB.com](http://www.myKB.com)) ASP.NET 작성 i 여기서 기반 응용 프로그램 기술 자료 소프트웨어 솔루션에 집중 합니다.</span><span class="sxs-lookup"><span data-stu-id="40717-381">Scott Cate has been working with Microsoft Web technologies since 1997 and is the President of myKB.com ([www.myKB.com](http://www.myKB.com)) where he specializes in writing ASP.NET based applications focused on Knowledge Base Software solutions.</span></span> <span data-ttu-id="40717-382">Scott에 전자 메일을 통해 연결할 수 [ scott.cate@myKB.com ](mailto:scott.cate@myKB.com) 또는에서 그의 블로그 [ScottCate.com](http://ScottCate.com)</span><span class="sxs-lookup"><span data-stu-id="40717-382">Scott can be contacted via email at [scott.cate@myKB.com](mailto:scott.cate@myKB.com) or his blog at [ScottCate.com](http://ScottCate.com)</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="40717-383">[이전](understanding-asp-net-ajax-updatepanel-triggers.md)
[다음](understanding-asp-net-ajax-localization.md)</span><span class="sxs-lookup"><span data-stu-id="40717-383">[Previous](understanding-asp-net-ajax-updatepanel-triggers.md)
[Next](understanding-asp-net-ajax-localization.md)</span></span>
