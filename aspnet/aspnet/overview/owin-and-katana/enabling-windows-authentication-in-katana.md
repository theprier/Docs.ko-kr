---
uid: aspnet/overview/owin-and-katana/enabling-windows-authentication-in-katana
title: Katana에서 Windows 인증을 사용 하도록 설정 | Microsoft Docs
author: MikeWasson
description: '이 문서에서는 Katana에서 Windows 인증을 사용 하는 방법을 보여 줍니다. 두 가지 시나리오를 다룹니다: Katana 호스트에 IIS를 사용 하 여 및 자체 호스트 하는 캐 탈 HttpListener를 사용 하는 중...'
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 82324ef0-3b75-4f63-a217-76ef4036ec93
msc.legacyurl: /aspnet/overview/owin-and-katana/enabling-windows-authentication-in-katana
msc.type: authoredcontent
ms.openlocfilehash: 0aa578020a1f02fa68c74e758014c642219b4265
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41837839"
---
<a name="enabling-windows-authentication-in-katana"></a><span data-ttu-id="e1950-104">Katana에서 Windows 인증 사용</span><span class="sxs-lookup"><span data-stu-id="e1950-104">Enabling Windows Authentication in Katana</span></span>
====================
<span data-ttu-id="e1950-105">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="e1950-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="e1950-106">이 문서에서는 Katana에서 Windows 인증을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e1950-106">This article shows how to enable Windows Authentication in Katana.</span></span> <span data-ttu-id="e1950-107">두 가지 시나리오를 다룹니다: Katana 호스트에 IIS를 사용 하 고 HttpListener를 사용 하 여 자체 사용자 지정 프로세스에서 Katana를 호스트 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1950-107">It covers two scenarios: Using IIS to host Katana, and using HttpListener to self-host Katana in a custom process.</span></span> <span data-ttu-id="e1950-108">Barry Dorrans, David Matson Chris Ross를이 문서를 검토에 참여해 주셔서 감사 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1950-108">Thanks to Barry Dorrans, David Matson, and Chris Ross for reviewing this article.</span></span>


<span data-ttu-id="e1950-109">Katana는 Microsoft에서 구현한 [OWIN](http://owin.org/), Open Web Interface for.NET.</span><span class="sxs-lookup"><span data-stu-id="e1950-109">Katana is Microsoft's implementation of [OWIN](http://owin.org/), the Open Web Interface for .NET.</span></span> <span data-ttu-id="e1950-110">OWIN 및 Katana 소개를 읽어보세요 [여기](an-overview-of-project-katana.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e1950-110">You can read an introduction to OWIN and Katana [here](an-overview-of-project-katana.md).</span></span> <span data-ttu-id="e1950-111">OWIN 아키텍처에는 여러 계층에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1950-111">The OWIN architecture has several layers:</span></span>

- <span data-ttu-id="e1950-112">호스트: OWIN 파이프라인을 실행 하는 프로세스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1950-112">Host: Manages the process in which the OWIN pipeline runs.</span></span>
- <span data-ttu-id="e1950-113">서버: 네트워크 소켓을 열고 요청을 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1950-113">Server: Opens a network socket and listens for requests.</span></span>
- <span data-ttu-id="e1950-114">미들웨어: HTTP 요청 및 응답을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="e1950-114">Middleware: Processes the HTTP request and response.</span></span>

<span data-ttu-id="e1950-115">Katana에는 현재 Windows 통합 인증을 모두 지 원하는 두 서버를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1950-115">Katana currently provides two servers, both of which support Windows Integrated Authentication:</span></span>

- <span data-ttu-id="e1950-116">**Microsoft.Owin.Host.SystemWeb**.</span><span class="sxs-lookup"><span data-stu-id="e1950-116">**Microsoft.Owin.Host.SystemWeb**.</span></span> <span data-ttu-id="e1950-117">ASP.NET 파이프라인을 사용 하 여 IIS를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e1950-117">Uses IIS with the ASP.NET pipeline.</span></span>
- <span data-ttu-id="e1950-118">**Microsoft.Owin.Host.HttpListener**.</span><span class="sxs-lookup"><span data-stu-id="e1950-118">**Microsoft.Owin.Host.HttpListener**.</span></span> <span data-ttu-id="e1950-119">사용 하 여 [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="e1950-119">Uses [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx).</span></span> <span data-ttu-id="e1950-120">자체 호스팅하는 경우이 서버는 현재 기본 옵션 Katana 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1950-120">This server is currently the default option when self-hosting Katana.</span></span>

> [!NOTE]
> <span data-ttu-id="e1950-121">Katana 제공 하지 않습니다 현재 OWIN 미들웨어입니다. Windows 인증을 위해 때문이 기능은 이미 서버에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1950-121">Katana does not currently provide OWIN middleware for Windows Authentication, because this functionality is already available in the servers.</span></span>


## <a name="windows-authentication-in-iis"></a><span data-ttu-id="e1950-122">IIS에서 Windows 인증</span><span class="sxs-lookup"><span data-stu-id="e1950-122">Windows Authentication in IIS</span></span>

<span data-ttu-id="e1950-123">Microsoft.Owin.Host.SystemWeb를 사용 하 여 IIS에서 Windows 인증 간단히 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1950-123">Using Microsoft.Owin.Host.SystemWeb, you can simply enable Windows Authentication in IIS.</span></span>

<span data-ttu-id="e1950-124">새 ASP.NET 응용 프로그램을 만들어, "ASP.NET 빈 웹 응용 프로그램" 프로젝트 템플릿을 사용 하 여 시작 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e1950-124">Let's start by creating a new ASP.NET application, using the "ASP.NET Empty Web Application" project template.</span></span>

![](enabling-windows-authentication-in-katana/_static/image1.png)

<span data-ttu-id="e1950-125">그런 다음 NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1950-125">Next, add NuGet packages.</span></span> <span data-ttu-id="e1950-126">**도구** 메뉴에서 **라이브러리 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="e1950-126">From the **Tools** menu, select **Library Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="e1950-127">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1950-127">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample1.cmd)]

<span data-ttu-id="e1950-128">이제 라는 클래스를 추가 `Startup` 다음 코드를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="e1950-128">Now add a class named `Startup` with the following code:</span></span>

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample2.cs)]

<span data-ttu-id="e1950-129">이것이 전부 owin을 IIS에서 실행 되는 "Hello world" 응용 프로그램을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1950-129">That's all you need to create a "Hello world" application for OWIN, running on IIS.</span></span> <span data-ttu-id="e1950-130">F5 키를 눌러 응용 프로그램을 디버깅합니다.</span><span class="sxs-lookup"><span data-stu-id="e1950-130">Press F5 to debug the application.</span></span> <span data-ttu-id="e1950-131">"Hello World!" 표시</span><span class="sxs-lookup"><span data-stu-id="e1950-131">You should see "Hello World!"</span></span> <span data-ttu-id="e1950-132">브라우저 창에서.</span><span class="sxs-lookup"><span data-stu-id="e1950-132">in the browser window.</span></span>

![](enabling-windows-authentication-in-katana/_static/image2.png)

<span data-ttu-id="e1950-133">다음으로, IIS Express에서 Windows 인증을 지원할 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="e1950-133">Next, we'll enable Windows Authentication in IIS Express.</span></span> <span data-ttu-id="e1950-134">**뷰** 메뉴에서 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="e1950-134">From the **View** menu, select **Properties**.</span></span> <span data-ttu-id="e1950-135">프로젝트 속성을 보려면 솔루션 탐색기에서 프로젝트 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1950-135">Click on the project name in Solution Explorer to view the project properties.</span></span>

<span data-ttu-id="e1950-136">에 **속성** 창에서 **익명 인증** 에 **사용 안 함** 설정 하 고 **Windows 인증** 를  **사용 하도록 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="e1950-136">In the **Properties** window, set **Anonymous Authentication** to **Disabled** and set **Windows Authentication** to **Enabled**.</span></span>

![](enabling-windows-authentication-in-katana/_static/image3.png)

<span data-ttu-id="e1950-137">Visual Studio에서 응용 프로그램을 실행 하는 경우 IIS Express는 사용자의 Windows 자격 증명이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1950-137">When you run the application from Visual Studio, IIS Express will require the user's Windows credentials.</span></span> <span data-ttu-id="e1950-138">사용 하 여이 확인할 수 있습니다 [Fiddler](http://fiddler2.com/home) 또는 다른 HTTP 디버깅 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="e1950-138">You can see this by using [Fiddler](http://fiddler2.com/home) or another HTTP debugging tool.</span></span> <span data-ttu-id="e1950-139">HTTP 응답 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e1950-139">Here is an example HTTP response:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample3.cmd?highlight=1,5-6)]

<span data-ttu-id="e1950-140">이 응답에 Www-authenticate 헤더를 서버에서 지원 되는지 나타냅니다 합니다 [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) Kerberos 또는 NTLM을 사용 하는 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="e1950-140">The WWW-Authenticate headers in this response indicate that the server supports the [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) protocol, which uses either Kerberos or NTLM.</span></span>

<span data-ttu-id="e1950-141">서버에 응용 프로그램을 배포한 경우에 따라 나중 [이 단계](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication) 해당 서버의 IIS에서 Windows 인증을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1950-141">Later, when you deploy the application to a server, follow [these steps](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication) to enable Windows Authentication in IIS on that server.</span></span>

## <a name="windows-authentication-in-httplistener"></a><span data-ttu-id="e1950-142">HttpListener에서 Windows 인증</span><span class="sxs-lookup"><span data-stu-id="e1950-142">Windows Authentication in HttpListener</span></span>

<span data-ttu-id="e1950-143">Microsoft.Owin.Host.HttpListener Katana를 자체 호스트를 사용 하는 경우에 직접 Windows 인증을 사용할 수 있습니다 합니다 **HttpListener** 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="e1950-143">If you are using Microsoft.Owin.Host.HttpListener to self-host Katana, you can enable Windows Authentication directly on the **HttpListener** instance.</span></span>

<span data-ttu-id="e1950-144">먼저 새 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e1950-144">First, create a new console application.</span></span> <span data-ttu-id="e1950-145">그런 다음 NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1950-145">Next, add NuGet packages.</span></span> <span data-ttu-id="e1950-146">**도구** 메뉴에서 **라이브러리 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="e1950-146">From the **Tools** menu, select **Library Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="e1950-147">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1950-147">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample4.cmd)]

<span data-ttu-id="e1950-148">이제 라는 클래스를 추가 `Startup` 다음 코드를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="e1950-148">Now add a class named `Startup` with the following code:</span></span>

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample5.cs)]

<span data-ttu-id="e1950-149">이 클래스는 이전에 동일한 "Hello world" 예제에서 구현 되지만 인증 체계로 한 Windows 인증을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1950-149">This class implements the same "Hello world" example from before, but it also sets Windows Authentication as the authentication scheme.</span></span>

<span data-ttu-id="e1950-150">내부는 `Main` 함수, OWIN 파이프라인을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1950-150">Inside the `Main` function, start the OWIN pipeline:</span></span>

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample6.cs)]

<span data-ttu-id="e1950-151">응용 프로그램이 Windows 인증을 사용 하 고 있음을 확인 하는 Fiddler에서 요청을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1950-151">You can send a request in Fiddler to confirm that the application is using Windows Authentication:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample7.cmd?highlight=1,4-5)]

## <a name="related-topics"></a><span data-ttu-id="e1950-152">관련 항목</span><span class="sxs-lookup"><span data-stu-id="e1950-152">Related Topics</span></span>

[<span data-ttu-id="e1950-153">프로젝트 Katana 개요</span><span class="sxs-lookup"><span data-stu-id="e1950-153">An Overview of Project Katana</span></span>](an-overview-of-project-katana.md)

[<span data-ttu-id="e1950-154">System.Net.HttpListener</span><span class="sxs-lookup"><span data-stu-id="e1950-154">System.Net.HttpListener</span></span>](https://msdn.microsoft.com/library/system.net.httplistener.aspx)

[<span data-ttu-id="e1950-155">MVC 5의에서 OWIN Forms 인증 이해</span><span class="sxs-lookup"><span data-stu-id="e1950-155">Understanding OWIN Forms Authentication in MVC 5</span></span>](https://blogs.msdn.com/b/webdev/archive/2013/07/03/understanding-owin-forms-authentication-in-mvc-5.aspx)
