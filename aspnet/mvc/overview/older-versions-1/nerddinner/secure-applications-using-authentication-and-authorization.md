---
uid: mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
title: 인증 및 권한 부여를 사용 하 여 응용 프로그램 보안 | Microsoft Docs
author: microsoft
description: 9 단계에는 사용자를 등록 해야 합니다. 추가할 인증 및 권한 부여 NerdDinner 응용 프로그램을 보호 하는 방법을 보여 줍니다 만들려는 사이트에 로그인 하는 중...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 9e4d5cac-b071-440c-b044-20b6d0c964fb
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
msc.type: authoredcontent
ms.openlocfilehash: d5f1b26312f11fd6d4ab500c7f24a4d89d428e38
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41839135"
---
<a name="secure-applications-using-authentication-and-authorization"></a><span data-ttu-id="2dc7f-103">인증 및 권한 부여를 사용 하 여 응용 프로그램 보안</span><span class="sxs-lookup"><span data-stu-id="2dc7f-103">Secure Applications Using Authentication and Authorization</span></span>
====================
<span data-ttu-id="2dc7f-104">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="2dc7f-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="2dc7f-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="2dc7f-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="2dc7f-106">이 무료의 9 단계 ["NerdDinner" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 는 안내를 통한 작은 빌드 하지만 ASP.NET MVC 1을 사용 하 여 웹 응용 프로그램을 완료 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-106">This is step 9 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="2dc7f-107">9 단계에는 사용자를 등록 해야 합니다. 추가할 인증 및 권한 부여 NerdDinner 응용 프로그램을 보호 하는 방법을 보여 줍니다 새 dinners 만들고를 저녁 식사를 호스트 하는 사용자만 사이트에 로그인 나중에 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-107">Step 9 shows how to add authentication and authorization to secure our NerdDinner application, so that users need to register and login to the site to create new dinners, and only the user who is hosting a dinner can edit it later.</span></span>
> 
> <span data-ttu-id="2dc7f-108">ASP.NET MVC 3을 사용 하는 경우 수행 하는 것이 좋습니다 합니다 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 하거나 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-step-9-authentication-and-authorization"></a><span data-ttu-id="2dc7f-109">NerdDinner 9 단계: 인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="2dc7f-109">NerdDinner Step 9: Authentication and Authorization</span></span>

<span data-ttu-id="2dc7f-110">지금 바로 누구나 응용 프로그램 부여는 NerdDinner 만들고 모든 dinner의 세부 정보를 편집 하는 기능 사이트를 방문 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-110">Right now our NerdDinner application grants anyone visiting the site the ability to create and edit the details of any dinner.</span></span> <span data-ttu-id="2dc7f-111">사용자가 등록할 필요가 해 보겠습니다 변경 새 dinners 만들고를 저녁 식사를 호스트 하는 사용자만 나중에 편집할 수 있도록 제한을 추가 하는 사이트에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-111">Let's change this so that users need to register and login to the site to create new dinners, and add a restriction so that only the user who is hosting a dinner can edit it later.</span></span>

<span data-ttu-id="2dc7f-112">이렇게 하려면 인증 및 권한 부여 응용 프로그램 보안을 사용 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-112">To enable this we'll use authentication and authorization to secure our application.</span></span>

### <a name="understanding-authentication-and-authorization"></a><span data-ttu-id="2dc7f-113">이해 인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="2dc7f-113">Understanding Authentication and Authorization</span></span>

<span data-ttu-id="2dc7f-114">*인증* 식별 하 고 응용 프로그램에 액세스 하는 클라이언트의 id 유효성을 검사 하는 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-114">*Authentication* is the process of identifying and validating the identity of a client accessing an application.</span></span> <span data-ttu-id="2dc7f-115">간단히 말해 "인 최종 사용자 웹 사이트를 방문할 때" 식별 하는 방법에 대 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-115">Put more simply, it is about identifying "who" the end-user is when they visit a website.</span></span> <span data-ttu-id="2dc7f-116">ASP.NET은 브라우저 사용자를 인증 하는 여러 방법을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-116">ASP.NET supports multiple ways to authenticate browser users.</span></span> <span data-ttu-id="2dc7f-117">인터넷 웹 응용 프로그램에 대 한 가장 일반적인 인증 방법은 사용 되는 "폼 인증" 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-117">For Internet web applications, the most common authentication approach used is called "Forms Authentication".</span></span> <span data-ttu-id="2dc7f-118">Forms 인증을 사용 하면 개발자가 해당 응용 프로그램 내에서 HTML 로그인 폼을 작성 한 다음 데이터베이스 또는 다른 암호 자격 증명 저장소에 대 한 최종 사용자가 제출 하는 사용자 이름/암호 유효성 검사를 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-118">Forms Authentication enables a developer to author an HTML login form within their application, and then validate the username/password an end-user submits against a database or other password credential store.</span></span> <span data-ttu-id="2dc7f-119">사용자 이름/암호 조합이 올바른 경우 개발자는 이후 요청에서 사용자를 식별 하 여 암호화 된 HTTP 쿠키를 발급 하는 ASP.NET 다음 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-119">If the username/password combination is correct, the developer can then ask ASP.NET to issue an encrypted HTTP cookie to identify the user across future requests.</span></span> <span data-ttu-id="2dc7f-120">NerdDinner 응용 프로그램을 사용 하 여 폼 인증을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-120">We'll by using forms authentication with our NerdDinner application.</span></span>

<span data-ttu-id="2dc7f-121">*권한 부여* 인증된 된 사용자가 특정 URL/리소스에 액세스 하거나 일부 작업을 수행할 권한이 있는지 여부를 결정 하는 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-121">*Authorization* is the process of determining whether an authenticated user has permission to access a particular URL/resource or to perform some action.</span></span> <span data-ttu-id="2dc7f-122">예를 들어, NerdDinner 응용 프로그램 내에서 하고자에 로그인 한 사용자만 액세스할 수 있도록 권한을 부여 합니다 *Dinners/만들기* URL 새 Dinners를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-122">For example, within our NerdDinner application we'll want to authorize that only users who are logged in can access the */Dinners/Create* URL and create new Dinners.</span></span> <span data-ttu-id="2dc7f-123">에서는 또한 하려고를 저녁 식사를 호스트 하는 사용자만 편집할 하 고 다른 모든 사용자에 대 한 편집 액세스를 거부할 수 있도록 권한 부여 논리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-123">We'll also want to add authorization logic so that only the user who is hosting a dinner can edit it – and deny edit access to all other users.</span></span>

### <a name="forms-authentication-and-the-accountcontroller"></a><span data-ttu-id="2dc7f-124">폼 인증 및는 AccountController</span><span class="sxs-lookup"><span data-stu-id="2dc7f-124">Forms Authentication and the AccountController</span></span>

<span data-ttu-id="2dc7f-125">ASP.NET MVC에 대 한 기본 Visual Studio 프로젝트 템플릿을 새 ASP.NET MVC 응용 프로그램을 만들 때 자동으로 폼 인증을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-125">The default Visual Studio project template for ASP.NET MVC automatically enables forms authentication when new ASP.NET MVC applications are created.</span></span> <span data-ttu-id="2dc7f-126">자동으로 미리 작성된 된 계정 로그인 페이지 구현 용이 하다는 실제로 사이트 내에서 보안을 통합 하는 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-126">It also automatically adds a pre-built account login page implementation to the project – which makes it really easy to integrate security within a site.</span></span>

<span data-ttu-id="2dc7f-127">이 액세스 하는 사용자가 인증 되지 않은 경우 사이트의 오른쪽 위에 있는 "Log On" 링크를 표시 하는 기본 Site.master 마스터 페이지:</span><span class="sxs-lookup"><span data-stu-id="2dc7f-127">The default Site.master master page displays a "Log On" link at the top-right of the site when the user accessing it is not authenticated:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image1.png)

<span data-ttu-id="2dc7f-128">사용자는 "Log On" 링크를 클릭 하 여 */계정/로그온* URL:</span><span class="sxs-lookup"><span data-stu-id="2dc7f-128">Clicking the "Log On" link takes a user to the */Account/LogOn* URL:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image2.png)

<span data-ttu-id="2dc7f-129">방문자에 게 등록 하지 않은 이렇게 – 하도록 걸립니다 "등록" 링크를 클릭 하 여 */계정/등록* URL 계정 세부 정보를 입력 하 고:</span><span class="sxs-lookup"><span data-stu-id="2dc7f-129">Visitors who haven't registered can do so by clicking the "Register" link – which will take them to the */Account/Register* URL and allow them to enter account details:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image3.png)

<span data-ttu-id="2dc7f-130">"등록" 단추를 클릭 하면 ASP.NET 멤버 자격 시스템 내에서 새 사용자를 만들고 폼 인증을 사용 하 여 사이트에 사용자를 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-130">Clicking the "Register" button will create a new user within the ASP.NET Membership system, and authenticate the user onto the site using forms authentication.</span></span>

<span data-ttu-id="2dc7f-131">Site.master 변경 출력을 "Welcome [username]!" 페이지의 오른쪽 위에 사용자에 로그인 한 경우</span><span class="sxs-lookup"><span data-stu-id="2dc7f-131">When a user is logged-in, the Site.master changes the top-right of the page to output a "Welcome [username]!"</span></span> <span data-ttu-id="2dc7f-132">메시지 및 렌더링을 "로그 오프" 연결을 "로그온" 하나 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-132">message and renders a "Log Off" link instead of a "Log On" one.</span></span> <span data-ttu-id="2dc7f-133">"로그 오프" 링크를 클릭 하면 사용자를 로그 아웃 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-133">Clicking the "Log Off" link logs out the user:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image4.png)

<span data-ttu-id="2dc7f-134">위의 로그인, 로그 아웃 및 등록 기능을 프로젝트를 만들 때 Visual Studio에서 프로젝트에 추가 된 AccountController 클래스 내에서 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-134">The above login, logout, and registration functionality is implemented within the AccountController class that was added to our project by Visual Studio when it created the project.</span></span> <span data-ttu-id="2dc7f-135">UI는 AccountController \Views\Account 디렉터리 내에서 템플릿 보기를 사용 하 여 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-135">The UI for the AccountController is implemented using view templates within the \Views\Account directory:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image5.png)

<span data-ttu-id="2dc7f-136">AccountController 클래스 암호화 된 인증 쿠키 및 저장 하 고 사용자 이름/암호의 유효성을 검사 하는 ASP.NET 멤버 자격 API를 실행 하는 ASP.NET 폼 인증 시스템을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-136">The AccountController class uses the ASP.NET Forms Authentication system to issue encrypted authentication cookies, and the ASP.NET Membership API to store and validate usernames/passwords.</span></span> <span data-ttu-id="2dc7f-137">ASP.NET 멤버 자격 API를 확장할 수 있는 이며 모든 암호 자격 증명 저장소로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-137">The ASP.NET Membership API is extensible and enables any password credential store to be used.</span></span> <span data-ttu-id="2dc7f-138">ASP.NET는 Active Directory 또는 SQL database 내에서 사용자 이름/암호를 저장 하는 기본 제공 멤버 자격 공급자 구현으로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-138">ASP.NET ships with built-in membership provider implementations that store username/passwords within a SQL database, or within Active Directory.</span></span>

<span data-ttu-id="2dc7f-139">NerdDinner 응용 프로그램 프로젝트의 루트에 "web.config" 파일을 열고 찾고 여 사용 해야 하는 멤버 자격 공급자를 구성할 수 있습니다 합니다 &lt;멤버 자격&gt; 내의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-139">We can configure which membership provider our NerdDinner application should use by opening the "web.config" file at the root of the project and looking for the &lt;membership&gt; section within it.</span></span> <span data-ttu-id="2dc7f-140">프로젝트를 만들 때 추가 기본 web.config SQL 멤버 자격 공급자를 등록 하 고 "ApplicationServices" 라는 연결 문자열을 사용 하도록 구성 데이터베이스 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-140">The default web.config added when the project was created registers the SQL membership provider, and configures it to use a connection-string named "ApplicationServices" to specify the database location.</span></span>

<span data-ttu-id="2dc7f-141">기본 "ApplicationServices" 연결 문자열 (내에서 지정 된 합니다 &lt;connectionStrings&gt; web.config 파일의 섹션) SQL Express를 사용 하도록 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-141">The default "ApplicationServices" connection string (which is specified within the &lt;connectionStrings&gt; section of the web.config file) is configured to use SQL Express.</span></span> <span data-ttu-id="2dc7f-142">"ASPNETDB 명명 된 SQL Express 데이터베이스를 가리키도록. MDF"응용 프로그램의" 앱\_Data "디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-142">It points to a SQL Express database named "ASPNETDB.MDF" under the application's "App\_Data" directory.</span></span> <span data-ttu-id="2dc7f-143">이 데이터베이스 멤버 자격 API를 사용 하 여 응용 프로그램 내에서 처음으로 존재 하지 않는 경우 ASP.NET 자동으로 데이터베이스를 만들고 그 안에 적절 한 멤버 자격 데이터베이스 스키마를 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-143">If this database doesn't exist the first time the Membership API is used within the application, ASP.NET will automatically create the database and provision the appropriate membership database schema within it:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image6.png)

<span data-ttu-id="2dc7f-144">web.config 파일 내에 있는 "ApplicationServices" 연결 문자열 업데이트 되었는지 확인 해야 하는 경우 SQL Express에 방문 하셔서 전체 SQL Server 인스턴스를 사용 하 여 (또는 원격 데이터베이스에 연결)를 사용 하는 대신 모든는 할 일은 적절 한 멤버 자격 스키마 이 가리키는 데이터베이스에 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-144">If instead of using SQL Express we wanted to use a full SQL Server instance (or connect to a remote database), all we'd need to-do is to update the "ApplicationServices" connection string within the web.config file and make sure that the appropriate membership schema has been added to the database it points at.</span></span> <span data-ttu-id="2dc7f-145">실행할 수 있습니다는 "aspnet\_regsql.exe" 데이터베이스에 멤버 자격 및 다른 ASP.NET 응용 프로그램 서비스에 대 한 적절 한 스키마를 추가 하려면 \Windows\Microsoft.NET\Framework\v2.0.50727\ 디렉터리 내에서 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-145">You can run the "aspnet\_regsql.exe" utility within the \Windows\Microsoft.NET\Framework\v2.0.50727\ directory to add the appropriate schema for membership and the other ASP.NET application services to a database.</span></span>

### <a name="authorizing-the-dinnerscreate-url-using-the-authorize-filter"></a><span data-ttu-id="2dc7f-146">[Authorize] 필터를 사용 하 여 Dinners/만들기 URL 권한 부여</span><span class="sxs-lookup"><span data-stu-id="2dc7f-146">Authorizing the /Dinners/Create URL using the [Authorize] filter</span></span>

<span data-ttu-id="2dc7f-147">보안 인증 및 계정 관리 구현 NerdDinner 응용 프로그램을 사용 하도록 설정 하려면 코드를 작성할 필요가 없었습니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-147">We didn't have to write any code to enable a secure authentication and account management implementation for the NerdDinner application.</span></span> <span data-ttu-id="2dc7f-148">사용자가 응용 프로그램 및 사이트의 로그인/로그 아웃 사용 하 여 새 계정을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-148">Users can register new accounts with our application, and login/logout of the site.</span></span>

<span data-ttu-id="2dc7f-149">이제 응용 프로그램에 권한 부여 논리를 추가 하 고 인증 상태 및 방문자의 사용자 이름을 사용 하 여 어떤 수 하며 사이트 내에서 수행할 수 없습니다를 제어할 수 있습니다 했습니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-149">Now we can add authorization logic to the application, and use the authentication status and username of visitors to control what they can and can't do within the site.</span></span> <span data-ttu-id="2dc7f-150">"만들기" 작업 메서드에 DinnersController 클래스의 권한 부여 논리를 추가 하 여 시작 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-150">Let's begin by adding authorization logic to the "Create" action methods of our DinnersController class.</span></span> <span data-ttu-id="2dc7f-151">특히 우리가 해야 하는 액세스 하는 사용자를 *Dinners/만들기* URL 로그인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-151">Specifically, we will require that users accessing the */Dinners/Create* URL must be logged in.</span></span> <span data-ttu-id="2dc7f-152">로그인 하지 않은 경우 있도록 수에 로그인 할 로그인 페이지로 리디렉션됩니다 됩니다 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-152">If they aren't logged in we'll redirect them to the login page so that they can sign-in.</span></span>

<span data-ttu-id="2dc7f-153">이 논리를 구현 하는 것은 매우 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-153">Implementing this logic is pretty easy.</span></span> <span data-ttu-id="2dc7f-154">해야 할 일이 만들기 작업 메서드에 [Authorize] 필터 특성을 추가 하는 것 같이:</span><span class="sxs-lookup"><span data-stu-id="2dc7f-154">All we need to-do is to add an [Authorize] filter attribute to our Create action methods like so:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample1.cs)]

<span data-ttu-id="2dc7f-155">ASP.NET MVC 작업 메서드에 선언적으로 적용할 수 있는 재사용 가능한 논리를 구현 하는 "작업 필터"를 만드는 기능을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-155">ASP.NET MVC supports the ability to create "action filters" that can be used to implement re-usable logic that can be declaratively applied to action methods.</span></span> <span data-ttu-id="2dc7f-156">[Authorize] 필터를 ASP.NET MVC에서 제공 하는 기본 제공 작업 필터 중 하나 이며 개발자 작업 메서드와 컨트롤러 클래스에 권한 부여 규칙을 선언적으로 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-156">The [Authorize] filter is one of the built-in action filters provided by ASP.NET MVC, and it enables a developer to declaratively apply authorization rules to action methods and controller classes.</span></span>

<span data-ttu-id="2dc7f-157">위에서 같이 매개 변수 없이 적용 될 때 동작 메서드가 요청 하는 사용자에서 로그인 해야 하 고 자동으로 리디렉션됩니다 브라우저를 로그인 url 그렇지 않은 경우 [Authorize] 필터를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-157">When applied without any parameters (like above) the [Authorize] filter enforces that the user making the action method request must be logged in – and it will automatically redirect the browser to the login URL if they aren't.</span></span> <span data-ttu-id="2dc7f-158">처음에 요청한 URL 쿼리 문자열 인수로 전달 되는이 리디렉션을 수행할 때 (예: / 계정/로그온? ReturnUrl = %2fDinners %2fCreate).</span><span class="sxs-lookup"><span data-stu-id="2dc7f-158">When doing this redirect the originally requested URL is passed as a querystring argument (for example: /Account/LogOn?ReturnUrl=%2fDinners%2fCreate).</span></span> <span data-ttu-id="2dc7f-159">AccountController 로그인 되 면 사용자를 원래 요청 된 URL로 다시 리디렉션합니다 다음 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-159">The AccountController will then redirect the user back to the originally requested URL once they login.</span></span>

<span data-ttu-id="2dc7f-160">[Authorize] 필터는 필요에 따라 사용자는 모두 로그온에 허용 된 사용자 또는 허용 된 보안 역할의 멤버 목록을 내에서 할 수 있는 "사용자" 또는 "역할" 속성을 지정 하는 기능을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-160">The [Authorize] filter optionally supports the ability to specify a "Users" or "Roles" property that can be used to require that the user is both logged in and within a list of allowed users or a member of an allowed security role.</span></span> <span data-ttu-id="2dc7f-161">예를 들어 아래 코드 허용 두 개의 특정 사용자, "scottgu" 및 "billg" Dinners/만들기 URL에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-161">For example, the code below only allows two specific users, "scottgu" and "billg", to access the /Dinners/Create URL:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample2.cs)]

<span data-ttu-id="2dc7f-162">코드 내에서 특정 사용자 이름을 포함 하지만 매우 되지 않은 intainable 수는 경향이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-162">Embedding specific user names within code tends to be pretty un-maintainable though.</span></span> <span data-ttu-id="2dc7f-163">상위 수준 "역할"을 정의 하는 것이 좋습니다를 기준으로 코드를 검사 하 고 데이터베이스 또는 active directory 시스템 (활성화 코드에서 외부적으로 저장 될 실제 사용자 매핑 목록)을 사용 하 여 역할에 사용자를 매핑할 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-163">A better approach is to define higher-level "roles" that the code checks against, and then to map users into the role using either a database or active directory system (enabling the actual user mapping list to be stored externally from the code).</span></span> <span data-ttu-id="2dc7f-164">ASP.NET이 사용자/역할 매핑을 수행 하는 데 도움이 되는 역할 공급자 (비롯 하 여 SQL 및 Active Directory)의 기본 제공 집합 뿐만 아니라 기본 제공 역할 관리 API 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-164">ASP.NET includes a built-in role management API as well as a built-in set of role providers (including ones for SQL and Active Directory) that can help perform this user/role mapping.</span></span> <span data-ttu-id="2dc7f-165">그런 다음 Dinners/만들기 URL에 액세스 하는 특정 "관리" 역할 내의 사용자만 사용할 수 있도록 코드 업데이트 수 있습니다.:</span><span class="sxs-lookup"><span data-stu-id="2dc7f-165">We could then update the code to only allow users within a specific "admin" role to access the /Dinners/Create URL:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample3.cs)]

### <a name="using-the-useridentityname-property-when-creating-dinners"></a><span data-ttu-id="2dc7f-166">만들 때 User.Identity.Name 속성을 사용 하 여 Dinners</span><span class="sxs-lookup"><span data-stu-id="2dc7f-166">Using the User.Identity.Name property when Creating Dinners</span></span>

<span data-ttu-id="2dc7f-167">컨트롤러 기본 클래스에서 노출 User.Identity.Name 속성을 사용 하 여 요청에 현재 로그인 한 사용자의 사용자 이름을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-167">We can retrieve the username of the currently logged-in user of a request using the User.Identity.Name property exposed on the Controller base class.</span></span>

<span data-ttu-id="2dc7f-168">이전 create () 작업 메서드는 HTTP POST 버전을 구현한 경우 했습니다 하드 코드 된 정적 문자열로 Dinner "HostedBy" 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-168">Earlier when we implemented the HTTP-POST version of our Create() action method we had hardcoded the "HostedBy" property of the Dinner to a static string.</span></span> <span data-ttu-id="2dc7f-169">Dinner 만드는 호스트는 RSVP를 자동으로 추가 수 있을 뿐만 아니라 이제 대신 User.Identity.Name 속성을 사용 하 여이 코드를 업데이트할 수 있습니다 것:</span><span class="sxs-lookup"><span data-stu-id="2dc7f-169">We can now update this code to instead use the User.Identity.Name property, as well as automatically add an RSVP for the host creating the Dinner:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample4.cs)]

<span data-ttu-id="2dc7f-170">Create () 메서드에 [Authorize] 특성을 추가 했지만, 때문에 ASP.NET MVC는 작업 메서드에서 Dinners/만들기 URL을 방문 하는 사용자가 사이트에 로그인 하는 경우에 실행 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-170">Because we have added an [Authorize] attribute to the Create() method, ASP.NET MVC ensures that the action method only executes if the user visiting the /Dinners/Create URL is logged in on the site.</span></span> <span data-ttu-id="2dc7f-171">따라서 User.Identity.Name 속성 값을 올바른 사용자 이름을 항상 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-171">As such, the User.Identity.Name property value will always contain a valid username.</span></span>

### <a name="using-the-useridentityname-property-when-editing-dinners"></a><span data-ttu-id="2dc7f-172">편집할 때 User.Identity.Name 속성을 사용 하 여 Dinners</span><span class="sxs-lookup"><span data-stu-id="2dc7f-172">Using the User.Identity.Name property when Editing Dinners</span></span>

<span data-ttu-id="2dc7f-173">이제 호스트 자체가 dinners의 속성을 편집할 수만 있도록 사용자를 제한 하는 일부 권한 부여 논리를 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-173">Let's now add some authorization logic that restricts users so that they can only edit the properties of dinners they themselves are hosting.</span></span>

<span data-ttu-id="2dc7f-174">이 돕기 위해 "IsHostedBy(username)" 도우미 메서드를 (내에서 앞서 작성 Dinner.cs 부분 클래스)은 Dinner 개체에 추가 됩니다 했습니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-174">To help with this, we'll first add an "IsHostedBy(username)" helper method to our Dinner object (within the Dinner.cs partial class we built earlier).</span></span> <span data-ttu-id="2dc7f-175">이 도우미 메서드는 제공 된 사용자 이름을 Dinner HostedBy 속성과 일치 하 여부와 그 중 대/소문자 구분 문자열 비교를 수행 하는 데 필요한 논리를 캡슐화 따라 true 또는 false를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-175">This helper method returns true or false depending on whether a supplied username matches the Dinner HostedBy property, and encapsulates the logic necessary to perform a case-insensitive string comparison of them:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample5.cs)]

<span data-ttu-id="2dc7f-176">그런 다음 DinnersController 클래스 내에서 되 작업 메서드에 [Authorize] 특성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-176">We'll then add an [Authorize] attribute to the Edit() action methods within our DinnersController class.</span></span> <span data-ttu-id="2dc7f-177">그러면는 사용자가 로그인 해야 요청에는 */Dinners/편집 / [id]* URL입니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-177">This will ensure that users must be logged in to request a */Dinners/Edit/[id]* URL.</span></span>

<span data-ttu-id="2dc7f-178">다음 코드 Dinner.IsHostedBy(username) 도우미 메서드를 사용 하 여 로그인 한 사용자 Dinner 호스트와 일치 하는지 확인 하는 편집 메서드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-178">We can then add code to our Edit methods that uses the Dinner.IsHostedBy(username) helper method to verify that the logged-in user matches the Dinner host.</span></span> <span data-ttu-id="2dc7f-179">사용자 호스트 없는 경우에서는 "InvalidOwner" 보기를 표시 하 고 해당 요청을 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-179">If the user is not the host, we'll display an "InvalidOwner" view and terminate the request.</span></span> <span data-ttu-id="2dc7f-180">이 작업을 수행 하는 코드는 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-180">The code to do this looks like below:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample6.cs)]

<span data-ttu-id="2dc7f-181">\Views\Dinners 디렉터리를 마우스 오른쪽 단추로 클릭 한 다음를 선택 하 고 추가-에서는&gt;새 "InvalidOwner" 보기를 만들려면 메뉴 명령을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-181">We can then right-click on the \Views\Dinners directory and choose the Add-&gt;View menu command to create a new "InvalidOwner" view.</span></span> <span data-ttu-id="2dc7f-182">사용 하 여 채웁니다 것은 오류 메시지가 아래:</span><span class="sxs-lookup"><span data-stu-id="2dc7f-182">We'll populate it with the below error message:</span></span>

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample7.aspx)]

<span data-ttu-id="2dc7f-183">이제 사용자가 자신이 소유 하지 않는 저녁 식사를 편집 하려고 하는 경우 해당 오류 메시지가 표시 됩니다는</span><span class="sxs-lookup"><span data-stu-id="2dc7f-183">And now when a user attempts to edit a dinner they don't own, they'll get an error message:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image7.png)

<span data-ttu-id="2dc7f-184">Dinners도 삭제의 저녁 식사 호스트만 삭제할 수 있는지 확인 하는 권한 잠글 컨트롤러 내에서 delete () 작업 메서드에 대 한 동일한 단계를 반복할 수 했습니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-184">We can repeat the same steps for the Delete() action methods within our controller to lock down permission to delete Dinners as well, and ensure that only the host of a Dinner can delete it.</span></span>

### <a name="showinghiding-edit-and-delete-links"></a><span data-ttu-id="2dc7f-185">표시/숨기기 편집 및 삭제 링크</span><span class="sxs-lookup"><span data-stu-id="2dc7f-185">Showing/Hiding Edit and Delete Links</span></span>

<span data-ttu-id="2dc7f-186">정보 URL에서 DinnersController 클래스의 편집 및 삭제 동작 메서드에 연결 되어 했습니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-186">We are linking to the Edit and Delete action method of our DinnersController class from our Details URL:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image8.png)

<span data-ttu-id="2dc7f-187">현재 세부 정보 URL로 방문자의를 저녁 식사 호스트 인지에 관계 없이 편집 및 삭제 작업 링크가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-187">Currently we are showing the Edit and Delete action links regardless of whether the visitor to the details URL is the host of the dinner.</span></span> <span data-ttu-id="2dc7f-188">보겠습니다이 되도록 변경 링크는 방문한 사용자 dinner의 소유자 인 경우에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-188">Let's change this so that the links are only displayed if the visiting user is the owner of the dinner.</span></span>

<span data-ttu-id="2dc7f-189">저녁 식사 개체를 검색 하 고 보기 템플릿은를 모델 개체로 전달 하는 우리의 DinnersController 내의 Details() 작업 메서드:</span><span class="sxs-lookup"><span data-stu-id="2dc7f-189">The Details() action method within our DinnersController retrieves a Dinner object and then passes it as the model object to our view template:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample8.cs)]

<span data-ttu-id="2dc7f-190">보기 템플릿은 조건부로 표시/숨기기 편집 및 삭제 링크를 아래와 같은 도우미 메서드 Dinner.IsHostedBy()를 사용 하 여 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-190">We can update our view template to conditionally show/hide the Edit and Delete links by using the Dinner.IsHostedBy() helper method like below:</span></span>

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample9.aspx)]

#### <a name="next-steps"></a><span data-ttu-id="2dc7f-191">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2dc7f-191">Next Steps</span></span>

<span data-ttu-id="2dc7f-192">이제 살펴보겠습니다 참석 여부 회신 하기 dinners AJAX를 사용 하 여 인증 된 사용자가 사용할 수 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="2dc7f-192">Let's now look at how we can enable authenticated users to RSVP for dinners using AJAX.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2dc7f-193">[이전](implement-efficient-data-paging.md)
> [다음](use-ajax-to-deliver-dynamic-updates.md)</span><span class="sxs-lookup"><span data-stu-id="2dc7f-193">[Previous](implement-efficient-data-paging.md)
[Next](use-ajax-to-deliver-dynamic-updates.md)</span></span>
