---
uid: aspnet/overview/owin-and-katana/enabling-windows-authentication-in-katana
title: "Katana에서 Windows 인증을 사용 하도록 설정 | Microsoft Docs"
author: MikeWasson
description: "이 문서에서는 Katana에서 Windows 인증을 사용 하도록 설정 하는 방법을 설명 합니다. 두 가지 시나리오를 다룹니다: Katana, 호스트에 IIS를 사용 하 고 HttpListener를 사용 하 여 캐 탈 자체 호스트 하 고 있습니다..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/30/2013
ms.topic: article
ms.assetid: 82324ef0-3b75-4f63-a217-76ef4036ec93
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/owin-and-katana/enabling-windows-authentication-in-katana
msc.type: authoredcontent
ms.openlocfilehash: 8a26d356f7abafba021199761f9a49dcb81765c5
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="enabling-windows-authentication-in-katana"></a><span data-ttu-id="8bdff-104">Katana에서 Windows 인증을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="8bdff-104">Enabling Windows Authentication in Katana</span></span>
====================
<span data-ttu-id="8bdff-105">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="8bdff-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="8bdff-106">이 문서에서는 Katana에서 Windows 인증을 사용 하도록 설정 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bdff-106">This article shows how to enable Windows Authentication in Katana.</span></span> <span data-ttu-id="8bdff-107">두 가지 시나리오를 다룹니다: Katana, 호스트에 IIS를 사용 하 고 HttpListener를 사용 하 여 사용자 지정 프로세스에서 Katana를 자체 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bdff-107">It covers two scenarios: Using IIS to host Katana, and using HttpListener to self-host Katana in a custom process.</span></span> <span data-ttu-id="8bdff-108">이 문서를 검토 하기 위한 Chris Ross Barry Dorrans, David Matson을 가져주셔서 감사 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bdff-108">Thanks to Barry Dorrans, David Matson, and Chris Ross for reviewing this article.</span></span>


<span data-ttu-id="8bdff-109">Katana은 Microsoft에서 구현한 [OWIN](http://owin.org/),.NET에 대 한 열린 웹 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="8bdff-109">Katana is Microsoft's implementation of [OWIN](http://owin.org/), the Open Web Interface for .NET.</span></span> <span data-ttu-id="8bdff-110">OWIN 및 Katana 소개를 읽을 수 [여기](an-overview-of-project-katana.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8bdff-110">You can read an introduction to OWIN and Katana [here](an-overview-of-project-katana.md).</span></span> <span data-ttu-id="8bdff-111">OWIN 아키텍처에 대 한 여러 계층에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bdff-111">The OWIN architecture has several layers:</span></span>

- <span data-ttu-id="8bdff-112">호스트: OWIN 파이프라인 실행 되는 프로세스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bdff-112">Host: Manages the process in which the OWIN pipeline runs.</span></span>
- <span data-ttu-id="8bdff-113">서버: 네트워크 소켓을 열고 요청을 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bdff-113">Server: Opens a network socket and listens for requests.</span></span>
- <span data-ttu-id="8bdff-114">미들웨어: HTTP 요청 및 응답을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="8bdff-114">Middleware: Processes the HTTP request and response.</span></span>

<span data-ttu-id="8bdff-115">Katana에는 현재 Windows 통합 인증을 모두 지 원하는 두 명의 서버를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bdff-115">Katana currently provides two servers, both of which support Windows Integrated Authentication:</span></span>

- <span data-ttu-id="8bdff-116">**Microsoft.Owin.Host.SystemWeb**.</span><span class="sxs-lookup"><span data-stu-id="8bdff-116">**Microsoft.Owin.Host.SystemWeb**.</span></span> <span data-ttu-id="8bdff-117">ASP.NET 파이프라인을 IIS를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8bdff-117">Uses IIS with the ASP.NET pipeline.</span></span>
- <span data-ttu-id="8bdff-118">**Microsoft.Owin.Host.HttpListener**.</span><span class="sxs-lookup"><span data-stu-id="8bdff-118">**Microsoft.Owin.Host.HttpListener**.</span></span> <span data-ttu-id="8bdff-119">사용 하 여 [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="8bdff-119">Uses [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx).</span></span> <span data-ttu-id="8bdff-120">자체 호스팅하는 경우이 서버는 현재 기본 옵션 Katana 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bdff-120">This server is currently the default option when self-hosting Katana.</span></span>

> [!NOTE]
> <span data-ttu-id="8bdff-121">Katana 현재 제공 하지 않습니다 OWIN 미들웨어입니다. Windows 인증을 위해 서버에서이 기능을 이미 있으므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bdff-121">Katana does not currently provide OWIN middleware for Windows Authentication, because this functionality is already available in the servers.</span></span>


## <a name="windows-authentication-in-iis"></a><span data-ttu-id="8bdff-122">IIS에서 Windows 인증</span><span class="sxs-lookup"><span data-stu-id="8bdff-122">Windows Authentication in IIS</span></span>

<span data-ttu-id="8bdff-123">Microsoft.Owin.Host.SystemWeb를 사용 하 여 단순히 IIS에서 Windows 인증을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bdff-123">Using Microsoft.Owin.Host.SystemWeb, you can simply enable Windows Authentication in IIS.</span></span>

<span data-ttu-id="8bdff-124">새 ASP.NET 응용 프로그램 "ASP.NET 빈 웹 응용 프로그램" 프로젝트 템플릿을 사용 하 여를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8bdff-124">Let's start by creating a new ASP.NET application, using the "ASP.NET Empty Web Application" project template.</span></span>

![](enabling-windows-authentication-in-katana/_static/image1.png)

<span data-ttu-id="8bdff-125">NuGet 패키지를 다음으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bdff-125">Next, add NuGet packages.</span></span> <span data-ttu-id="8bdff-126">**도구** 메뉴 선택 **라이브러리 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="8bdff-126">From the **Tools** menu, select **Library Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="8bdff-127">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bdff-127">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample1.cmd)]

<span data-ttu-id="8bdff-128">이제 라는 클래스를 추가 `Startup` 다음 코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bdff-128">Now add a class named `Startup` with the following code:</span></span>

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample2.cs)]

<span data-ttu-id="8bdff-129">즉 하기만 하면 IIS에서 실행 중인 OWIN에 대 한 "Hello world" 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8bdff-129">That's all you need to create a "Hello world" application for OWIN, running on IIS.</span></span> <span data-ttu-id="8bdff-130">F5 키를 눌러 응용 프로그램을 디버깅합니다.</span><span class="sxs-lookup"><span data-stu-id="8bdff-130">Press F5 to debug the application.</span></span> <span data-ttu-id="8bdff-131">"Hello World!"이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bdff-131">You should see "Hello World!"</span></span> <span data-ttu-id="8bdff-132">브라우저 창에서.</span><span class="sxs-lookup"><span data-stu-id="8bdff-132">in the browser window.</span></span>

![](enabling-windows-authentication-in-katana/_static/image2.png)

<span data-ttu-id="8bdff-133">다음으로, IIS Express에서 Windows 인증을 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bdff-133">Next, we'll enable Windows Authentication in IIS Express.</span></span> <span data-ttu-id="8bdff-134">**보기** 메뉴 선택 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="8bdff-134">From the **View** menu, select **Properties**.</span></span> <span data-ttu-id="8bdff-135">프로젝트 속성을 보려면 솔루션 탐색기에서 프로젝트 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bdff-135">Click on the project name in Solution Explorer to view the project properties.</span></span>

<span data-ttu-id="8bdff-136">에 **속성** 창의 설정 **익명 인증** 를 **비활성화** 설정 **Windows 인증** 를  **활성화**합니다.</span><span class="sxs-lookup"><span data-stu-id="8bdff-136">In the **Properties** window, set **Anonymous Authentication** to **Disabled** and set **Windows Authentication** to **Enabled**.</span></span>

![](enabling-windows-authentication-in-katana/_static/image3.png)

<span data-ttu-id="8bdff-137">Visual Studio에서 응용 프로그램을 실행 하는 경우 IIS Express는 사용자의 Windows 자격 증명이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bdff-137">When you run the application from Visual Studio, IIS Express will require the user's Windows credentials.</span></span> <span data-ttu-id="8bdff-138">사용 하 여 볼 수 있습니다 [Fiddler](http://fiddler2.com/home) 또는 다른 HTTP 디버깅 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="8bdff-138">You can see this by using [Fiddler](http://fiddler2.com/home) or another HTTP debugging tool.</span></span> <span data-ttu-id="8bdff-139">HTTP 응답 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8bdff-139">Here is an example HTTP response:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample3.cmd?highlight=1,5-6)]

<span data-ttu-id="8bdff-140">이 응답에 WWW 인증 헤더는 서버에서 지원 되는지 표시는 [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) Kerberos 또는 NTLM을 사용 하는 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="8bdff-140">The WWW-Authenticate headers in this response indicate that the server supports the [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) protocol, which uses either Kerberos or NTLM.</span></span>

<span data-ttu-id="8bdff-141">서버에 응용 프로그램을 배포 하는 경우에 따라 나중 [이러한 단계](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication) 해당 서버에 IIS에서 Windows 인증을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bdff-141">Later, when you deploy the application to a server, follow [these steps](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication) to enable Windows Authentication in IIS on that server.</span></span>

## <a name="windows-authentication-in-httplistener"></a><span data-ttu-id="8bdff-142">HttpListener에서 Windows 인증</span><span class="sxs-lookup"><span data-stu-id="8bdff-142">Windows Authentication in HttpListener</span></span>

<span data-ttu-id="8bdff-143">직접 Windows 인증을 사용할 수 Microsoft.Owin.Host.HttpListener를 자체 Katana 호스트를 사용 하는 경우는 **HttpListener** 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="8bdff-143">If you are using Microsoft.Owin.Host.HttpListener to self-host Katana, you can enable Windows Authentication directly on the **HttpListener** instance.</span></span>

<span data-ttu-id="8bdff-144">먼저 새 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8bdff-144">First, create a new console application.</span></span> <span data-ttu-id="8bdff-145">NuGet 패키지를 다음으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bdff-145">Next, add NuGet packages.</span></span> <span data-ttu-id="8bdff-146">**도구** 메뉴 선택 **라이브러리 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="8bdff-146">From the **Tools** menu, select **Library Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="8bdff-147">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bdff-147">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample4.cmd)]

<span data-ttu-id="8bdff-148">이제 라는 클래스를 추가 `Startup` 다음 코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bdff-148">Now add a class named `Startup` with the following code:</span></span>

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample5.cs)]

<span data-ttu-id="8bdff-149">이전에 동일한 "Hello world" 예제에서이 클래스를 구현 하지만 인증 체계로 Windows 인증을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bdff-149">This class implements the same "Hello world" example from before, but it also sets Windows Authentication as the authentication scheme.</span></span>

<span data-ttu-id="8bdff-150">내에서 `Main` 함수, OWIN 파이프라인을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bdff-150">Inside the `Main` function, start the OWIN pipeline:</span></span>

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample6.cs)]

<span data-ttu-id="8bdff-151">응용 프로그램이 Windows 인증을 사용 하 고 있는지 확인 하는 Fiddler에서 요청을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bdff-151">You can send a request in Fiddler to confirm that the application is using Windows Authentication:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample7.cmd?highlight=1,4-5)]

## <a name="related-topics"></a><span data-ttu-id="8bdff-152">관련 항목</span><span class="sxs-lookup"><span data-stu-id="8bdff-152">Related Topics</span></span>

[<span data-ttu-id="8bdff-153">프로젝트 Katana 개요</span><span class="sxs-lookup"><span data-stu-id="8bdff-153">An Overview of Project Katana</span></span>](an-overview-of-project-katana.md)

[<span data-ttu-id="8bdff-154">System.Net.HttpListener</span><span class="sxs-lookup"><span data-stu-id="8bdff-154">System.Net.HttpListener</span></span>](https://msdn.microsoft.com/library/system.net.httplistener.aspx)

[<span data-ttu-id="8bdff-155">MVC 5의에서 OWIN 폼 인증 이해</span><span class="sxs-lookup"><span data-stu-id="8bdff-155">Understanding OWIN Forms Authentication in MVC 5</span></span>](https://blogs.msdn.com/b/webdev/archive/2013/07/03/understanding-owin-forms-authentication-in-mvc-5.aspx)
