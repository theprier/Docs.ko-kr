---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-vb
title: Windows 인증 (VB)를 사용 하 여 사용자 인증 | Microsoft Docs
author: microsoft
description: MVC 응용 프로그램의 컨텍스트에서 Windows 인증을 사용 하는 방법에 알아봅니다. 응용 프로그램의 웹 co 내에서 Windows 인증을 사용 하는 방법에 알아봅니다...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 532fa051-7d5c-4d6d-87f6-339ce4b84c44
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-vb
msc.type: authoredcontent
ms.openlocfilehash: e37508dedd4243dd1a1638e68760f6f4310e61a8
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41831602"
---
<a name="authenticating-users-with-windows-authentication-vb"></a><span data-ttu-id="7b155-104">Windows 인증 (VB)를 사용 하 여 사용자 인증</span><span class="sxs-lookup"><span data-stu-id="7b155-104">Authenticating Users with Windows Authentication (VB)</span></span>
====================
<span data-ttu-id="7b155-105">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="7b155-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="7b155-106">MVC 응용 프로그램의 컨텍스트에서 Windows 인증을 사용 하는 방법에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-106">Learn how to use Windows authentication in the context of an MVC application.</span></span> <span data-ttu-id="7b155-107">응용 프로그램의 웹 구성 파일 내에서 Windows 인증을 사용 하는 방법 및 IIS를 사용 하 여 인증을 구성 하는 방법에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-107">You learn how to enable Windows authentication within your application's web configuration file and how to configure authentication with IIS.</span></span> <span data-ttu-id="7b155-108">마지막으로, 특정 Windows 사용자나 그룹에 대 한 컨트롤러 작업에 대 한 액세스를 제한 하려면 [Authorize] 특성을 사용 하는 방법에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-108">Finally, you learn how to use the [Authorize] attribute to restrict access to controller actions to particular Windows users or groups.</span></span>


<span data-ttu-id="7b155-109">이 자습서의 목표를 사용할 수 있는 방법을 설명 하는 보안의 기본 제공 기능에 인터넷 정보 서비스 암호로 보호 MVC 응용 프로그램의 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-109">The goal of this tutorial is to explain how you can take advantage of the security features built into Internet Information Services to password protect the views in your MVC applications.</span></span> <span data-ttu-id="7b155-110">특정 Windows 사용자 또는 특정 Windows 그룹의 구성원 인 사용자에 의해서만 호출할 컨트롤러 작업을 허용 하는 방법에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-110">You learn how to allow controller actions to be invoked only by particular Windows users or users who are members of particular Windows groups.</span></span>

<span data-ttu-id="7b155-111">Windows 인증을 사용 하 여 합리적 내부 회사 웹 사이트 (인트라넷 사이트)를 작성 하는 웹 사이트에 액세스할 때 해당 표준 Windows 사용자 이름과 암호를 사용할 수 있도록 하려는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-111">Using Windows authentication makes sense when you are building an internal company website (an intranet site) and you want your users to be able to use their standard Windows user names and passwords when accessing the website.</span></span> <span data-ttu-id="7b155-112">웹 사이트 (인터넷 웹 사이트를) 연결 하는 그라데이션이 작성 하는 경우에 폼 인증을 대신 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-112">If you are building an outwards facing website (an Internet website) consider using Forms authentication instead.</span></span>

#### <a name="enabling-windows-authentication"></a><span data-ttu-id="7b155-113">Windows 인증을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="7b155-113">Enabling Windows Authentication</span></span>

<span data-ttu-id="7b155-114">새 ASP.NET MVC 응용 프로그램을 만들면 기본적으로 Windows 인증 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-114">When you create a new ASP.NET MVC application, Windows authentication is not enabled by default.</span></span> <span data-ttu-id="7b155-115">폼 인증에는 MVC 응용 프로그램에 대 한 설정 기본 인증 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-115">Forms authentication is the default authentication type enabled for MVC applications.</span></span> <span data-ttu-id="7b155-116">MVC 응용 프로그램의 웹 구성 (web.config) 파일을 수정 하 여 Windows 인증을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-116">You must enable Windows authentication by modifying your MVC application's web configuration (web.config) file.</span></span> <span data-ttu-id="7b155-117">찾을 합니다 &lt;인증&gt; 섹션 및 다음과 같은 폼 인증 대신 Windows를 사용 하도록 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-117">Find the &lt;authentication&gt; section and modify it to use Windows instead of Forms authentication like this:</span></span>

[!code-xml[Main](authenticating-users-with-windows-authentication-vb/samples/sample1.xml)]

<span data-ttu-id="7b155-118">Windows 인증을 사용 하도록 설정 하면 웹 서버는 사용자를 인증 하는 것에 대 한 책임을 집니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-118">When you enable Windows authentication, your web server becomes responsible for authenticating users.</span></span> <span data-ttu-id="7b155-119">일반적으로 웹 서버를 만들고 ASP.NET MVC 응용 프로그램을 배포할 때 사용 하는 두 가지 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-119">Typically, there are two different types of web servers that you use when creating and deploying an ASP.NET MVC application.</span></span>

<span data-ttu-id="7b155-120">먼저 MVC 응용 프로그램을 개발 하는 동안 Visual Studio에 포함 된 ASP.NET 개발 웹 서버를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-120">First, while developing an MVC application, you use the ASP.NET Development Web Server included with Visual Studio.</span></span> <span data-ttu-id="7b155-121">기본적으로 ASP.NET 개발 웹 서버는 현재 Windows 계정 (Windows에 로그온 할 때 사용한 모든 계정)의 컨텍스트에서 모든 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-121">By default, the ASP.NET Development Web Server executes all pages in the context of the current Windows account (whatever account you used to log into Windows).</span></span>

<span data-ttu-id="7b155-122">ASP.NET 개발 웹 서버에 NTLM 인증도 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-122">The ASP.NET Development Web Server also supports NTLM authentication.</span></span> <span data-ttu-id="7b155-123">솔루션 탐색기 창에서 프로젝트의 이름을 마우스 오른쪽 단추로 클릭 하 고 속성을 선택 하 여 NTLM 인증을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-123">You can enable NTLM authentication by right-clicking the name of your project in the Solution Explorer window and selecting Properties.</span></span> <span data-ttu-id="7b155-124">다음으로, 웹 탭을 선택 하 고 NTLM 확인란 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="7b155-124">Next, select the Web tab and check the NTLM checkbox (see Figure 1).</span></span>

<span data-ttu-id="7b155-125">**그림 1-사용 하도록 설정 하면 ASP.NET 개발 웹 서버에 대 한 NTLM 인증**</span><span class="sxs-lookup"><span data-stu-id="7b155-125">**Figure 1 – Enabling NTLM authentication for the ASP.NET Development Web Server**</span></span>

![clip_image002](authenticating-users-with-windows-authentication-vb/_static/image1.jpg)

<span data-ttu-id="7b155-127">프로덕션 웹 응용 프로그램에 손 모양 아이콘이 있습니다 사용 하 여 IIS 웹 서버로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-127">For a production web application, on the hand, you use IIS as your web server.</span></span> <span data-ttu-id="7b155-128">IIS 인증 등의 몇 가지 종류를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-128">IIS supports several types of authentication including:</span></span>

- <span data-ttu-id="7b155-129">기본 인증 – HTTP 1.0 프로토콜의 일부로 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-129">Basic Authentication – Defined as part of the HTTP 1.0 protocol.</span></span> <span data-ttu-id="7b155-130">인터넷을 통해 일반 텍스트로 (Base64로 인코딩된) 사용자 이름 및 암호를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-130">Sends user names and passwords in clear text (Base64 encoded) across the Internet.</span></span> <span data-ttu-id="7b155-131">다이제스트 인증 – 인터넷을 통해 자체 암호 대신 암호의 해시를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-131">- Digest Authentication – Sends a hash of a password, instead of the password itself, across the internet.</span></span> <span data-ttu-id="7b155-132">-통합형된 Windows (NTLM) 인증 – 가장 적합 한 유형의 windows를 사용 하 여 인트라넷 환경에서 사용할 인증입니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-132">- Integrated Windows (NTLM) Authentication – The best type of authentication to use in intranet environments using windows.</span></span> <span data-ttu-id="7b155-133">-인증서 인증-클라이언트 쪽 인증서를 사용 하 여 수 있도록 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-133">- Certificate Authentication – Enables authentication using a client-side certificate.</span></span> <span data-ttu-id="7b155-134">인증서는 Windows 사용자 계정에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-134">The certificate maps to a Windows user account.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="7b155-135">이러한 서로 다른 유형의 인증의 자세한 개요를 참조 하세요 [ https://msdn.microsoft.com/library/aa292114(VS.71).aspx ](https://msdn.microsoft.com/library/aa292114(VS.71).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-135">For a more detailed overview of these different types of authentication, see [https://msdn.microsoft.com/library/aa292114(VS.71).aspx](https://msdn.microsoft.com/library/aa292114(VS.71).aspx).</span></span>


<span data-ttu-id="7b155-136">특정 유형의 인증을 사용 하도록 설정 하려면 인터넷 정보 서비스 관리자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-136">You can use Internet Information Services Manager to enable a particular type of authentication.</span></span> <span data-ttu-id="7b155-137">모든 운영 체제의 경우 사용 가능한 모든 종류의 인증 되지 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-137">Be aware that all types of authentication are not available in the case of every operating system.</span></span> <span data-ttu-id="7b155-138">또한 Windows Vista를 사용 하 여 IIS 7.0을 사용 중인 경우 인터넷 정보 서비스 관리자에 나타나기까지 다양 한 Windows 인증을 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-138">Furthermore, if you are using IIS 7.0 with Windows Vista, you will need to enable the different types of Windows authentication before they appear in the Internet Information Services Manager.</span></span> <span data-ttu-id="7b155-139">오픈 **제어판, 프로그램, 프로그램 및 기능을 설정 하는 Windows 기능 사용 /**, 인터넷 정보 서비스 노드를 확장 하 고 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="7b155-139">Open **Control Panel, Programs, Programs and Features, Turn Windows features on or off**, and expand the Internet Information Services node (see Figure 2).</span></span>

<span data-ttu-id="7b155-140">**그림 2 – 사용 하도록 설정 하면 Windows IIS 기능**</span><span class="sxs-lookup"><span data-stu-id="7b155-140">**Figure 2 – Enabling Windows IIS features**</span></span>

![clip_image004](authenticating-users-with-windows-authentication-vb/_static/image2.jpg)

<span data-ttu-id="7b155-142">인터넷 정보 서비스를 사용 하 여 사용 하도록 설정 수도 있고 서로 다른 유형의 인증을 사용 하지 않도록 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-142">Using Internet Information Services, you can enable or disable different types of authentication.</span></span> <span data-ttu-id="7b155-143">예를 들어 그림 3에서는 익명 인증을 사용 하지 않도록 설정 하 고 통합 Windows (NTLM) 인증을 사용 하도록 설정 하면 IIS 7.0을 사용 하는 경우</span><span class="sxs-lookup"><span data-stu-id="7b155-143">For example, Figure 3 illustrates disabling anonymous authentication and enabling Integrated Windows (NTLM) authentication when using IIS 7.0.</span></span>

<span data-ttu-id="7b155-144">**그림 3-통합된 Windows 인증을 사용 하도록 설정**</span><span class="sxs-lookup"><span data-stu-id="7b155-144">**Figure 3 – Enabling Integrated Windows Authentication**</span></span>

![clip_image006](authenticating-users-with-windows-authentication-vb/_static/image3.jpg)

#### <a name="authorizing-windows-users-and-groups"></a><span data-ttu-id="7b155-146">Windows 인증 사용자 및 그룹</span><span class="sxs-lookup"><span data-stu-id="7b155-146">Authorizing Windows Users and Groups</span></span>

<span data-ttu-id="7b155-147">Windows 인증을 설정한 후 사용할 수 있습니다 합니다 &lt;권한 부여&gt; 컨트롤러 또는 컨트롤러 작업에 대 한 액세스를 제어 하는 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-147">After you enable Windows authentication, you can use the &lt;Authorize&gt; attribute to control access to controllers or controller actions.</span></span> <span data-ttu-id="7b155-148">이 특성은 MVC 컨트롤러를 전체 또는 특정 컨트롤러 작업에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-148">This attribute can be applied to an entire MVC controller or a particular controller action.</span></span>

<span data-ttu-id="7b155-149">예를 들어 Home 컨트롤러 목록 1의 index (), CompanySecrets(), 및 StephenSecrets() 라는 세 가지 작업을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-149">For example, the Home controller in Listing 1 exposes three actions named Index(), CompanySecrets(), and StephenSecrets().</span></span> <span data-ttu-id="7b155-150">Index () 작업을 호출할 수 누구나 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-150">Anyone can invoke the Index() action.</span></span> <span data-ttu-id="7b155-151">그러나 Windows 로컬 관리자 그룹의 구성원만 CompanySecrets() 동작을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-151">However, only members of the Windows local Managers group can invoke the CompanySecrets() action.</span></span> <span data-ttu-id="7b155-152">마지막으로, Stephen (Redmond에) 라는 Windows 도메인 사용자만 StephenSecrets() 동작을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-152">Finally, only the Windows domain user named Stephen (in the Redmond domain) can invoke the StephenSecrets() action.</span></span>

<span data-ttu-id="7b155-153">**1 – Controllers\HomeController.vb 나열**</span><span class="sxs-lookup"><span data-stu-id="7b155-153">**Listing 1 – Controllers\HomeController.vb**</span></span>

[!code-vb[Main](authenticating-users-with-windows-authentication-vb/samples/sample2.vb)]

> [!NOTE]
> <span data-ttu-id="7b155-154">인해 Windows 계정 컨트롤 (UAC (사용자), Windows Vista 또는 Windows Server 2008과 함께 작업 하는 경우, 로컬 관리자 그룹 다른 그룹 다르게 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-154">Because of Windows User Account Control (UAC), when working with Windows Vista or Windows Server 2008, the local Administrators group will behave differently than other groups.</span></span> <span data-ttu-id="7b155-155">합니다 &lt;권한 부여&gt; 컴퓨터의 UAC 설정을 수정 하지 않는 한 특성에서 로컬 Administrators 그룹의 멤버인 제대로 인식 하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-155">The &lt;Authorize&gt; attribute won't correctly recognize a member of the local Administrators group unless you modify your computer's UAC settings.</span></span>


<span data-ttu-id="7b155-156">정확 하 게 하는 경우 적절 한 권한이 없이 컨트롤러 작업을 호출 하려고 하면 사용 하도록 설정 하는 인증의 유형에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-156">Exactly what happens when you attempt to invoke a controller action without being the right permissions depends on the type of authentication enabled.</span></span> <span data-ttu-id="7b155-157">기본적으로 ASP.NET Development Server를 사용 하는 경우, 단순히 빈 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-157">By default, when using the ASP.NET Development Server, you simply get a blank page.</span></span> <span data-ttu-id="7b155-158">페이지가 사용 하 여 반환 되는 **401 권한이 없는** HTTP 응답 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-158">The page is served with a **401 Not Authorized** HTTP Response Status.</span></span>

<span data-ttu-id="7b155-159">다른 한편으로 사용 하지 않도록 설정 하는 익명 인증 및 사용 하도록 설정 하는 기본 인증을 사용 하 여 IIS를 사용 하는 경우 보호 되는 페이지를 요청할 때마다 로그인 대화 상자 프롬프트를 시작 유지 (그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="7b155-159">If, on the other hand, you are using IIS with Anonymous authentication disabled and Basic authentication enabled, then you keep getting a login dialog prompt each time you request the protected page (see Figure 4).</span></span>

<span data-ttu-id="7b155-160">**그림 4-기본 인증 로그인 대화 상자**</span><span class="sxs-lookup"><span data-stu-id="7b155-160">**Figure 4 – Basic authentication login dialog**</span></span>

![clip_image008](authenticating-users-with-windows-authentication-vb/_static/image4.jpg)

#### <a name="summary"></a><span data-ttu-id="7b155-162">요약</span><span class="sxs-lookup"><span data-stu-id="7b155-162">Summary</span></span>

<span data-ttu-id="7b155-163">이 자습서는 ASP.NET MVC 응용 프로그램의 컨텍스트에서 Windows 인증을 사용 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-163">This tutorial explained how you can use Windows authentication in the context of an ASP.NET MVC application.</span></span> <span data-ttu-id="7b155-164">IIS를 사용 하 여 인증을 구성 하는 방법과 응용 프로그램의 웹 구성 파일 내에서 Windows 인증을 사용 하도록 설정 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-164">You learned how to enable Windows authentication within your application's web configuration file and how to configure authentication with IIS.</span></span> <span data-ttu-id="7b155-165">마지막으로 사용 하는 방법을 알아보았습니다 합니다 &lt;권한 부여&gt; 특성을 특정 Windows 사용자나 그룹에 대 한 컨트롤러 작업에 대 한 액세스를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b155-165">Finally, you learned how to use the &lt;Authorize&gt; attribute to restrict access to controller actions to particular Windows users or groups.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7b155-166">[이전](authenticating-users-with-forms-authentication-vb.md)
> [다음](preventing-javascript-injection-attacks-vb.md)</span><span class="sxs-lookup"><span data-stu-id="7b155-166">[Previous](authenticating-users-with-forms-authentication-vb.md)
[Next](preventing-javascript-injection-attacks-vb.md)</span></span>
