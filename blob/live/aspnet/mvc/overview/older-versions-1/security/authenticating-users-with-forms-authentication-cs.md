---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-cs
title: "사용자를 인증 하는 것 폼 인증 (C#) | Microsoft Docs"
author: microsoft
description: "[Authorize] 특성을 사용 하는 방법에 알아봅니다 암호로 보호 하는 MVC 응용 프로그램의 특정 페이지입니다. 관리 웹 사이트도 사용 하는 방법을 알아봅니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/27/2009
ms.topic: article
ms.assetid: 239fd3ca-5630-4b8d-bc4b-2f906b1d3504
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-cs
msc.type: authoredcontent
ms.openlocfilehash: 17bcf02e1351587d64b72ee2b40393e0f748f23e
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="authenticating-users-with-forms-authentication-c"></a><span data-ttu-id="0502e-104">폼 인증 (C#)는 사용자 인증</span><span class="sxs-lookup"><span data-stu-id="0502e-104">Authenticating Users with Forms Authentication (C#)</span></span>
====================
<span data-ttu-id="0502e-105">여 [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="0502e-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="0502e-106">[Authorize] 특성을 사용 하는 방법에 알아봅니다 암호로 보호 하는 MVC 응용 프로그램의 특정 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-106">Learn how to use the [Authorize] attribute to password protect particular pages in your MVC application.</span></span> <span data-ttu-id="0502e-107">만들고 사용자 및 역할 관리 웹 사이트 관리 도구를 사용 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-107">You learn how to use the Web Site Administration Tool to create and manage users and roles.</span></span> <span data-ttu-id="0502e-108">또한 사용자 계정과 역할 정보를 저장 하는 구성 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-108">You also learn how to configure where user account and role information is stored.</span></span>


<span data-ttu-id="0502e-109">이 자습서의 목표는 폼을 사용 하는 방법을 설명 하는 ASP.NET MVC 응용 프로그램에서 뷰를 보호 하는 암호를 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-109">The goal of this tutorial is to explain how you can use Forms authentication to password protect the views in your ASP.NET MVC applications.</span></span> <span data-ttu-id="0502e-110">사용자 및 역할을 만들려는 웹 사이트 관리 도구를 사용 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-110">You learn how to use the Web Site Administration Tool to create users and roles.</span></span> <span data-ttu-id="0502e-111">또한 권한이 없는 사용자가 컨트롤러 작업을 호출 하지 못하게 방지 하는 방법에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-111">You also learn how to prevent unauthorized users from invoking controller actions.</span></span> <span data-ttu-id="0502e-112">마지막으로, 사용자 이름 및 암호 저장 되는 위치를 구성 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-112">Finally, you learn how to configure where user names and passwords are stored.</span></span>

#### <a name="using-the-web-site-administration-tool"></a><span data-ttu-id="0502e-113">웹 사이트 관리 도구를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="0502e-113">Using the Web Site Administration Tool</span></span>

<span data-ttu-id="0502e-114">다른 작업을 수행 하기 전 일부 사용자 및 역할을 만들어 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-114">Before we do anything else, we should start by creating some users and roles.</span></span> <span data-ttu-id="0502e-115">새 사용자 및 역할을 만드는 가장 쉬운 방법은 Visual Studio 2008 웹 사이트 관리 도구를 활용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-115">The easiest way to create new users and roles is to take advantage of the Visual Studio 2008 Web Site Administration Tool.</span></span> <span data-ttu-id="0502e-116">메뉴 옵션을 선택 하 여이 도구를 시작할 수 **프로젝트, ASP.NET 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-116">You can launch this tool by selecting the menu option **Project, ASP.NET Configuration**.</span></span> <span data-ttu-id="0502e-117">또는 솔루션 탐색기 창 위쪽에 표시 되는 전 세계에 도달 해머의 (다소 무시 무시) 아이콘을 클릭 하 여 웹 사이트 관리 도구를 시작할 수 있습니다 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="0502e-117">Alternatively, you can launch the Web Site Administration Tool by clicking the (somewhat scary) icon of the hammer hitting the world that appears at the top of the Solution Explorer window (see Figure 1).</span></span>

<span data-ttu-id="0502e-118">**그림 1-웹 사이트 관리 도구를 시작 합니다.**</span><span class="sxs-lookup"><span data-stu-id="0502e-118">**Figure 1 – Launching the Web Site Administration Tool**</span></span>

![clip_image002](authenticating-users-with-forms-authentication-cs/_static/image1.jpg)

<span data-ttu-id="0502e-120">웹 사이트 관리 도구 내에서 만들면 새 사용자 및 역할 보안 탭을 선택 하 여 합니다. 클릭는 **사용자 만들기** Stephen 라는 새 사용자를 만들려면 링크 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="0502e-120">Within the Web Site Administration Tool, you create new users and roles by selecting the Security tab. Click the **Create user** link to create a new user named Stephen (see Figure 2).</span></span> <span data-ttu-id="0502e-121">Stephen 사용자에 게 모든 암호를 제공 (예를 들어 *비밀*).</span><span class="sxs-lookup"><span data-stu-id="0502e-121">Provide the Stephen user with any password that you want (for example, *secret*).</span></span>

<span data-ttu-id="0502e-122">**그림 2 – 새 사용자 만들기**</span><span class="sxs-lookup"><span data-stu-id="0502e-122">**Figure 2 – Creating a new user**</span></span>

![clip_image004](authenticating-users-with-forms-authentication-cs/_static/image2.jpg)

<span data-ttu-id="0502e-124">역할을 활성화 한 다음 하나 이상의 역할을 정의 하 여 새 역할을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-124">You create new roles by first enabling roles and defining one or more roles.</span></span> <span data-ttu-id="0502e-125">클릭 하 여 역할을 사용 하도록 설정 된 **역할을 사용 하도록** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-125">Enable roles by clicking the **Enable roles** link.</span></span> <span data-ttu-id="0502e-126">다음으로 명명 된 역할을 만들 *관리자* 클릭 하 여는 **역할 만들기 또는 관리** (그림 3 참조)를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-126">Next, create a role named *Administrators* by clicking the **Create or Manage roles** link (see Figure 3).</span></span>

<span data-ttu-id="0502e-127">**그림 3 –는 새 역할 만들기**</span><span class="sxs-lookup"><span data-stu-id="0502e-127">**Figure 3 – Creating a new role**</span></span>

![clip_image006](authenticating-users-with-forms-authentication-cs/_static/image3.jpg)

<span data-ttu-id="0502e-129">마지막으로, Sally 라는 새 사용자를 만들고 사용자 만들기 링크를 클릭 하 고 Sally를 만들 때 관리자를 선택 하 여 관리자 역할 Sally 연결 (그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="0502e-129">Finally, create a new user named Sally and associate Sally with the Administrators role by clicking the Create User link and selecting Administrators when creating Sally (see Figure 4).</span></span>

<span data-ttu-id="0502e-130">**그림 4 – 역할에 사용자 추가**</span><span class="sxs-lookup"><span data-stu-id="0502e-130">**Figure 4 – Adding a user to a role**</span></span>

![clip_image008](authenticating-users-with-forms-authentication-cs/_static/image4.jpg)

<span data-ttu-id="0502e-132">모두 수행 하 고 나면 때 Stephen 및 Sally 라는 두 개의 새 사용자가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-132">When all is said and done, you should have two new users named Stephen and Sally.</span></span> <span data-ttu-id="0502e-133">또한 관리자 라는 새 역할이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-133">You should also have a new role named Administrators.</span></span> <span data-ttu-id="0502e-134">Sally 관리자 역할의 구성원 이므로 Stephen 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-134">Sally is a member of the Administrators role and Stephen is not.</span></span>

#### <a name="requiring-authorization"></a><span data-ttu-id="0502e-135">권한 부여를 요구</span><span class="sxs-lookup"><span data-stu-id="0502e-135">Requiring Authorization</span></span>

<span data-ttu-id="0502e-136">사용자 동작을 [Authorize] 특성을 추가 하 여 컨트롤러 작업을 호출 하는 사용자 인증을 요구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-136">You can require a user to be authenticated before the user invokes a controller action by adding the [Authorize] attribute to the action.</span></span> <span data-ttu-id="0502e-137">개별 컨트롤러의 액션 [Authorize] 특성을 적용할 수 있습니다 또는 전체 컨트롤러 클래스에이 특성을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-137">You can apply the [Authorize] attribute to an individual controller action or you can apply this attribute to an entire controller class.</span></span>

<span data-ttu-id="0502e-138">예를 들어 목록 1의 컨트롤러 CompanySecrets() 라는 동작을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-138">For example, the controller in Listing 1 exposes an action named CompanySecrets().</span></span> <span data-ttu-id="0502e-139">이 작업은 [Authorize] 특성으로 데코레이팅, 사용자가 인증 하지 않는 한이 작업을 호출할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-139">Because this action is decorated with the [Authorize] attribute, this action cannot be invoked unless a user is authenticated.</span></span>

<span data-ttu-id="0502e-140">**1 – Controllers\HomeController.cs 나열**</span><span class="sxs-lookup"><span data-stu-id="0502e-140">**Listing 1 – Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](authenticating-users-with-forms-authentication-cs/samples/sample1.cs)]

<span data-ttu-id="0502e-141">URL /Home/CompanySecrets 브라우저의 주소 표시줄에 입력 하 여 CompanySecrets() 작업을 호출 인증된 된 사용자에 없는 경우 자동으로 로그인 보기로 이동 될 합니다 (그림 5 참조).</span><span class="sxs-lookup"><span data-stu-id="0502e-141">If you invoke the CompanySecrets() action by entering the URL /Home/CompanySecrets in the address bar of your browser, and you are not an authenticated user, then you will be redirected to the Login view automatically (see Figure 5).</span></span>

<span data-ttu-id="0502e-142">**그림 5-로그인 보기**</span><span class="sxs-lookup"><span data-stu-id="0502e-142">**Figure 5 – The Login view**</span></span>

![clip_image010](authenticating-users-with-forms-authentication-cs/_static/image5.jpg)

<span data-ttu-id="0502e-144">로그인 뷰를 사용 하 여 사용자 이름 및 암호를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-144">You can use the Login view to enter your user name and password.</span></span> <span data-ttu-id="0502e-145">등록 된 사용자 모를 경우 클릭할 수 있는 **등록** 링크 레지스터로 이동할 수 (그림 6 참조)를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-145">If you are not a registered user then you can click the **register** link to navigate to the Register view (see Figure 6).</span></span> <span data-ttu-id="0502e-146">레지스터 뷰를 사용 하 여 사용자 계정을 새로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-146">You can use the Register view to create a new user account.</span></span>

<span data-ttu-id="0502e-147">**그림 6 – 레지스터 보기**</span><span class="sxs-lookup"><span data-stu-id="0502e-147">**Figure 6 – The Register view**</span></span>

![clip_image012](authenticating-users-with-forms-authentication-cs/_static/image6.jpg)

<span data-ttu-id="0502e-149">에 성공적으로 로그인 한 후 (그림 7 참조)를 보려면 CompanySecrets 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-149">After you successfully log in, you can see the CompanySecrets view (see Figure 7).</span></span> <span data-ttu-id="0502e-150">기본적으로 브라우저 창의 닫을 때까지 로그인 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-150">By default, you will continue to be logged in until you close your browser window.</span></span>

<span data-ttu-id="0502e-151">**그림 7-CompanySecrets 보기**</span><span class="sxs-lookup"><span data-stu-id="0502e-151">**Figure 7 – The CompanySecrets view**</span></span>

![clip_image014](authenticating-users-with-forms-authentication-cs/_static/image7.jpg)

#### <a name="authorizing-by-user-name-or-user-role"></a><span data-ttu-id="0502e-153">사용자 이름 또는 사용자 역할 권한 부여</span><span class="sxs-lookup"><span data-stu-id="0502e-153">Authorizing by User Name or User Role</span></span>

<span data-ttu-id="0502e-154">사용자 또는 사용자 역할의 특정 집합의 특정 집합에는 컨트롤러 작업에 대 한 액세스를 제한 하려면 [Authorize] 특성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-154">You can use the [Authorize] attribute to restrict access to a controller action to a particular set of users or a particular set of user roles.</span></span> <span data-ttu-id="0502e-155">예를 들어 목록 2의 수정 된 Home 컨트롤러 StephenSecrets() 및 AdministratorSecrets() 라는 두 개의 새 작업이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-155">For example, the modified Home controller in Listing 2 contains two new actions named StephenSecrets() and AdministratorSecrets().</span></span>

<span data-ttu-id="0502e-156">**2 – Controllers\HomeController.cs 나열**</span><span class="sxs-lookup"><span data-stu-id="0502e-156">**Listing 2 – Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](authenticating-users-with-forms-authentication-cs/samples/sample2.cs)]

<span data-ttu-id="0502e-157">사용자 이름 Stephen 있는 사용자만 StephenSecrets() 동작을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-157">Only a user with the user name Stephen can invoke the StephenSecrets() action.</span></span> <span data-ttu-id="0502e-158">다른 모든 사용자가 로그인 뷰로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-158">All other users get redirected to the Login view.</span></span> <span data-ttu-id="0502e-159">사용자가 속성에는 사용자 계정 이름의 쉼표로 구분 된 목록을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-159">The Users property accepts a comma separated list of user account names.</span></span>

<span data-ttu-id="0502e-160">관리자 역할에 사용자만 AdministratorSecrets() 작업을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-160">Only users in the Administrators role can invoke the AdministratorSecrets() action.</span></span> <span data-ttu-id="0502e-161">예를 들어 Sally Administrators 그룹의 구성원이 아니어서 AdministratorSecrets() 작업을 호출할 수 그녀.</span><span class="sxs-lookup"><span data-stu-id="0502e-161">For example, because Sally is a member of the Administrators group, she can invoke the AdministratorSecrets() action.</span></span> <span data-ttu-id="0502e-162">다른 모든 사용자가 로그인 뷰로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-162">All other users get redirected to the Login view.</span></span> <span data-ttu-id="0502e-163">역할 속성에는 역할 이름의 쉼표로 구분 된 목록을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-163">The Roles property accepts a comma separated list of role names.</span></span>

#### <a name="configuring-authentication"></a><span data-ttu-id="0502e-164">인증 구성</span><span class="sxs-lookup"><span data-stu-id="0502e-164">Configuring Authentication</span></span>

<span data-ttu-id="0502e-165">이 시점에서 하는지에 대해 사용자 계정과 역할 정보를 저장 되는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-165">At this point, you might be wondering where the user account and role information is being stored.</span></span> <span data-ttu-id="0502e-166">기본적으로 정보 MVC 응용 프로그램의 앱에 있는 명명 된 ASPNETDB.mdf (RANU) SQL Express 데이터베이스에 저장\_데이터 폴더.</span><span class="sxs-lookup"><span data-stu-id="0502e-166">By default, the information is stored in a (RANU) SQL Express database named ASPNETDB.mdf located in your MVC application's App\_Data folder.</span></span> <span data-ttu-id="0502e-167">이 데이터베이스 멤버 자격을 사용 하 여 시작 하는 경우 ASP.NET 프레임 워크에 의해 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-167">This database is generated by the ASP.NET framework automatically when you start using membership.</span></span>

<span data-ttu-id="0502e-168">솔루션 탐색기 창에서 ASPNETDB.mdf 데이터베이스를 보기 위해서는 먼저 모든 파일 표시 메뉴 옵션 프로젝트를 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-168">In order to see the ASPNETDB.mdf database in the Solution Explorer window, you first need to select the menu option Project, Show All Files.</span></span>

<span data-ttu-id="0502e-169">응용 프로그램을 개발 하는 경우 기본 SQL Express 데이터베이스를 사용 하는 문제가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-169">Using the default SQL Express database is fine when developing an application.</span></span> <span data-ttu-id="0502e-170">대부분의 경우, 없습니다 하려는 프로덕션 응용 프로그램에 대 한 기본 ASPNETDB.mdf 데이터베이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-170">Most likely, however, you won't want to use the default ASPNETDB.mdf database for a production application.</span></span> <span data-ttu-id="0502e-171">이 경우 다음 두 단계를 완료 하 여 사용자 계정 정보를 저장 하는 위치를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-171">In that case, you can change where user account information is stored by completing the following two steps:</span></span>

1. <span data-ttu-id="0502e-172">프로덕션 데이터베이스 응용 프로그램 서비스 데이터베이스 개체를 추가-프로덕션 데이터베이스를 가리키도록 연결 문자열을 응용 프로그램 변경</span><span class="sxs-lookup"><span data-stu-id="0502e-172">Add the Application Services database objects to your production database - Change your application connection string to point to your production database</span></span>

<span data-ttu-id="0502e-173">첫 번째 단계 프로덕션 데이터베이스의 모든 필요한 데이터베이스 개체 (테이블 및 저장된 프로시저)를 추가 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-173">The first step is to add all of the necessary database objects (tables and stored procedures) to your production database.</span></span> <span data-ttu-id="0502e-174">ASP.NET SQL Server 설치 마법사를 활용 하는 새 데이터베이스에 이러한 개체를 추가 하는 가장 쉬운 방법은 (그림 8 참조).</span><span class="sxs-lookup"><span data-stu-id="0502e-174">The easiest way to add these objects to a new database is to take advantage of the ASP.NET SQL Server Setup Wizard (see Figure 8).</span></span> <span data-ttu-id="0502e-175">Microsoft Visual Studio 2008 프로그램 그룹에서 Visual Studio 2008 명령 프롬프트를 연 명령 프롬프트에서 다음 명령을 실행 하 여이 도구를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-175">You can launch this tool by opening the Visual Studio 2008 Command Prompt from the Microsoft Visual Studio 2008 program group and executing the following command from the command prompt:</span></span>

<span data-ttu-id="0502e-176">aspnet\_regsql</span><span class="sxs-lookup"><span data-stu-id="0502e-176">aspnet\_regsql</span></span>

<span data-ttu-id="0502e-177">**그림 8 – ASP.NET SQL Server 설치 마법사**</span><span class="sxs-lookup"><span data-stu-id="0502e-177">**Figure 8 – The ASP.NET SQL Server Setup Wizard**</span></span>

![clip_image016](authenticating-users-with-forms-authentication-cs/_static/image8.jpg)

<span data-ttu-id="0502e-179">ASP.NET SQL Server 설치 마법사를 사용 하면 네트워크에서 SQL Server 데이터베이스를 선택 하 고 ASP.NET 응용 프로그램 서비스에 필요한 데이터베이스 개체의 모든 설치 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-179">The ASP.NET SQL Server Setup Wizard enables you to select a SQL Server database on your network and install all of the database objects required by the ASP.NET application services.</span></span> <span data-ttu-id="0502e-180">데이터베이스 서버 로컬 컴퓨터에 있는 것으로 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-180">The database server is not required to be located on your local machine.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="0502e-181">ASP.NET SQL Server 설치 마법사를 사용 하지 않음 하는 경우 다음 폴더에 응용 프로그램 서비스 데이터베이스 개체를 추가 하기 위한 SQL 스크립트를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-181">If you don't want to use the ASP.NET SQL Server Setup Wizard, then you can find SQL scripts for adding the application services database objects in the following folder:</span></span>
> 
> > <span data-ttu-id="0502e-182">C:\Windows\Microsoft.NET\Framework\v2.0.50727</span><span class="sxs-lookup"><span data-stu-id="0502e-182">C:\Windows\Microsoft.NET\Framework\v2.0.50727</span></span>


<span data-ttu-id="0502e-183">필요한 데이터베이스 개체를 만든 후에 MVC 응용 프로그램에서 사용 하는 데이터베이스 연결을 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-183">After you create the necessary database objects, you need to modify the database connection used by your MVC application.</span></span> <span data-ttu-id="0502e-184">프로덕션 데이터베이스를 가리키도록 웹 구성 파일 (web.config) 파일에서 ApplicationServices 연결 문자열을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-184">Modify the ApplicationServices connection string in your web configuration (web.config) file so that it points to the production database.</span></span> <span data-ttu-id="0502e-185">예를 들어 목록 3에서 수정 된 연결 (원래 ApplicationServices 연결 문자열이 주석 처리 되었습니다) MyProductionDB 라는 데이터베이스를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-185">For example, the modified connection in Listing 3 points to a database named MyProductionDB (the original ApplicationServices connection string has been commented out).</span></span>

<span data-ttu-id="0502e-186">**3 – Web.config를 나열합니다.**</span><span class="sxs-lookup"><span data-stu-id="0502e-186">**Listing 3 – Web.config**</span></span>

[!code-xml[Main](authenticating-users-with-forms-authentication-cs/samples/sample3.xml)]

#### <a name="configuring-database-permissions"></a><span data-ttu-id="0502e-187">데이터베이스 사용 권한 구성</span><span class="sxs-lookup"><span data-stu-id="0502e-187">Configuring Database Permissions</span></span>

<span data-ttu-id="0502e-188">통합 보안을 사용 하 여 데이터베이스에 연결할 경우 데이터베이스에 로그인으로 올바른 Windows 사용자 계정을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-188">If you use Integrated Security to connect to your database then you will need to add the correct Windows user account as a login to your database.</span></span> <span data-ttu-id="0502e-189">올바른 계정을 사용 여부는 ASP.NET 개발 서버 또는 인터넷 정보 서비스 웹 서버와에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-189">The correct account depends on whether you are using the ASP.NET Development Server or Internet Information Services as your web server.</span></span> <span data-ttu-id="0502e-190">올바른 사용자 계정 운영 체제에 따라서도 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-190">The correct user account also depends on your operating system.</span></span>

<span data-ttu-id="0502e-191">ASP.NET Development Server (Visual Studio에서 사용 되는 기본 웹 서버)를 사용 하는 응용 프로그램 Windows 사용자 계정의 컨텍스트 내에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-191">If you are using the ASP.NET Development Server (the default web server used by Visual Studio) then your application executes within the context of your Windows user account.</span></span> <span data-ttu-id="0502e-192">이 경우 데이터베이스 서버 로그인으로 Windows 사용자 계정을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-192">In that case, you need to add your Windows user account as a database server login.</span></span>

<span data-ttu-id="0502e-193">또는 인터넷 정보 서비스를 사용 하는 경우 다음 해야 데이터베이스 서버 로그인으로 ASPNET 계정 또는 NT 기관/네트워크 서비스 계정을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-193">Alternatively, if you are using Internet Information Services then you need to add either the ASPNET account or the NT AUTHORITY/NETWORK SERVICE account as a database server login.</span></span> <span data-ttu-id="0502e-194">Windows XP를 사용 하는 다음 데이터베이스에 로그인으로 ASPNET 계정을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-194">If you are using Windows XP then add the ASPNET account as a login to your database.</span></span> <span data-ttu-id="0502e-195">Windows Vista 또는 Windows Server 2008 같은 최신 운영 체제를 사용 하는 경우 NT 기관/네트워크 서비스 계정으로 데이터베이스 로그인을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-195">If you are using a more recent operating system, such as Windows Vista or Windows Server 2008, then add the NT AUTHORITY/NETWORK SERVICE account as the database login.</span></span>

<span data-ttu-id="0502e-196">Microsoft SQL Server Management Studio를 사용 하 여 데이터베이스에 새 사용자 계정을 추가할 수 있습니다 (그림 9 참조).</span><span class="sxs-lookup"><span data-stu-id="0502e-196">You can add a new user account to your database by using Microsoft SQL Server Management Studio (see Figure 9).</span></span>

<span data-ttu-id="0502e-197">**그림 9-새 Microsoft SQL Server 로그인 만들기**</span><span class="sxs-lookup"><span data-stu-id="0502e-197">**Figure 9 – Creating a new Microsoft SQL Server login**</span></span>

![clip_image018](authenticating-users-with-forms-authentication-cs/_static/image9.jpg)

<span data-ttu-id="0502e-199">필요한 로그인을 만든 후 올바른 데이터베이스 역할을 가진 데이터베이스 사용자로 로그인을 매핑해야 할 합니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-199">After you create the required login, you need to map the login to a database user with the right database roles.</span></span> <span data-ttu-id="0502e-200">로그인을 두 번 클릭 하 고 사용자 매핑 탭을 선택 합니다. 하나 이상의 응용 프로그램 서비스 데이터베이스 역할을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-200">Double-click the login and select the User Mapping tab. Select one or more application services database roles.</span></span> <span data-ttu-id="0502e-201">예를 들어 사용자를 인증 하기 위해 있게 해야 aspnet\_구성원\_BasicAccess 데이터베이스 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-201">For example, in order to authenticate users, you need to enable the aspnet\_Membership\_BasicAccess database role.</span></span> <span data-ttu-id="0502e-202">새 사용자를 만들기 위해 aspnet를 사용 하도록 설정 해야\_구성원\_FullAccess 데이터베이스 역할 (그림 10 참조).</span><span class="sxs-lookup"><span data-stu-id="0502e-202">In order to create new users, you need to enable the aspnet\_Membership\_FullAccess database role (see Figure 10).</span></span>

<span data-ttu-id="0502e-203">**그림 10-응용 프로그램 서비스 데이터베이스 역할 추가**</span><span class="sxs-lookup"><span data-stu-id="0502e-203">**Figure 10 – Adding Application Services database roles**</span></span>

![clip_image020](authenticating-users-with-forms-authentication-cs/_static/image10.jpg)

#### <a name="summary"></a><span data-ttu-id="0502e-205">요약</span><span class="sxs-lookup"><span data-stu-id="0502e-205">Summary</span></span>

<span data-ttu-id="0502e-206">이 자습서에서는 ASP.NET MVC 응용 프로그램을 빌드하는 경우 폼 인증을 사용 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-206">In this tutorial, you learned how to use Forms authentication when building an ASP.NET MVC application.</span></span> <span data-ttu-id="0502e-207">첫째, 웹 사이트 관리 도구를 이용 하 여 새 사용자 및 역할을 만드는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-207">First, you learned how to create new users and roles by taking advantage of the Web Site Administration Tool.</span></span> <span data-ttu-id="0502e-208">다음으로, [Authorize] 특성에서 컨트롤러 작업 호출 권한이 없는 사용자가 방지 하기 위해 사용 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-208">Next, you learned how to use the [Authorize] attribute to prevent unauthorized users from invoking controller actions.</span></span> <span data-ttu-id="0502e-209">마지막으로, 프로덕션 데이터베이스에 사용자 및 역할 정보를 저장 하 여 MVC 응용 프로그램을 구성 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="0502e-209">Finally, you learned how to configure your MVC application to store user and role information in a production database.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="0502e-210">다음</span><span class="sxs-lookup"><span data-stu-id="0502e-210">Next</span></span>](authenticating-users-with-windows-authentication-cs.md)
