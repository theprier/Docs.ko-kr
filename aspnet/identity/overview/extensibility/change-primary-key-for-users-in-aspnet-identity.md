---
uid: identity/overview/extensibility/change-primary-key-for-users-in-aspnet-identity
title: ASP.NET Id에서 사용자에 대 한 기본 키 변경 | Microsoft Docs
author: Rick-Anderson
description: Visual Studio 2013의 기본 웹 응용 프로그램 사용자 계정에 대 한 키에 대 한 문자열 값을 사용합니다. ASP.NET Id를 사용 하면의 형식을 변경 하는 중...
ms.author: riande
ms.date: 09/30/2014
ms.assetid: 44925849-5762-4504-a8cd-8f0cd06f6dc3
msc.legacyurl: /identity/overview/extensibility/change-primary-key-for-users-in-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: d2856ce1ca61a29e091bfbd16647b673e6fc659b
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51021107"
---
<a name="change-primary-key-for-users-in-aspnet-identity"></a><span data-ttu-id="cee52-104">ASP.NET Id에서 사용자에 대 한 기본 키 변경</span><span class="sxs-lookup"><span data-stu-id="cee52-104">Change Primary Key for Users in ASP.NET Identity</span></span>
====================
<span data-ttu-id="cee52-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="cee52-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="cee52-106">Visual Studio 2013의 기본 웹 응용 프로그램 사용자 계정에 대 한 키에 대 한 문자열 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-106">In Visual Studio 2013, the default web application uses a string value for the key for user accounts.</span></span> <span data-ttu-id="cee52-107">ASP.NET Id를 사용 하면 데이터 요구 사항에 맞게 키의 형식을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-107">ASP.NET Identity enables you to change the type of the key to meet your data requirements.</span></span> <span data-ttu-id="cee52-108">예를 들어, 키의 형식 문자열에서 정수로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-108">For example, you can change the type of the key from a string to an integer.</span></span>
> 
> <span data-ttu-id="cee52-109">이 항목에서는 기본 웹 응용 프로그램 및 사용자 계정 키를 정수로 변경 시작 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-109">This topic shows how to start with the default web application and change the user account key to an integer.</span></span> <span data-ttu-id="cee52-110">프로젝트에서 모든 유형의 키를 구현 하는 동일한 수정 사항이 적용을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-110">You can use the same modifications to implement any type of key in your project.</span></span> <span data-ttu-id="cee52-111">기본 웹 응용 프로그램에서 이러한 변경을 수행 하는 방법을 보여주지만 사용자 지정된 응용 프로그램에 비슷한 수정을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-111">It shows how to make these changes in the default web application, but you could apply similar modifications to a customized application.</span></span> <span data-ttu-id="cee52-112">MVC 또는 Web Forms를 사용 하 여 작업 하는 경우 필요한 변경 내용을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-112">It shows the changes needed when working with MVC or Web Forms.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="cee52-113">이 자습서에 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="cee52-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="cee52-114">Visual Studio 2013 업데이트 2를 사용 하 여 (또는 이상)</span><span class="sxs-lookup"><span data-stu-id="cee52-114">Visual Studio 2013 with Update 2 (or later)</span></span>
> - <span data-ttu-id="cee52-115">ASP.NET Id 2.1 이상</span><span class="sxs-lookup"><span data-stu-id="cee52-115">ASP.NET Identity 2.1 or later</span></span>


<span data-ttu-id="cee52-116">이 자습서의 단계를 수행 하려면 Visual Studio 2013 업데이트 2 (또는 이상) 및 ASP.NET 웹 응용 프로그램 템플릿에서 만든 웹 응용 프로그램을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-116">To perform the steps in this tutorial, you must have Visual Studio 2013 Update 2 (or later), and a web application created from the ASP.NET Web Application template.</span></span> <span data-ttu-id="cee52-117">업데이트 3에서 변경 하는 템플릿.</span><span class="sxs-lookup"><span data-stu-id="cee52-117">The template changed in Update 3.</span></span> <span data-ttu-id="cee52-118">이 항목에는 업데이트 2와 업데이트 3에서 템플릿을 변경 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-118">This topic shows how to change the template in Update 2 and Update 3.</span></span>

<span data-ttu-id="cee52-119">이 항목에는 다음과 같은 단원이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-119">This topic contains the following sections:</span></span>

- [<span data-ttu-id="cee52-120">Identity 사용자 클래스에 있는 키의 형식 변경</span><span class="sxs-lookup"><span data-stu-id="cee52-120">Change the type of the key in the Identity user class</span></span>](#userclass)
- [<span data-ttu-id="cee52-121">추가 키 유형을 사용 하는 사용자 지정된 Id 클래스</span><span class="sxs-lookup"><span data-stu-id="cee52-121">Add customized Identity classes that use the key type</span></span>](#customclass)
- [<span data-ttu-id="cee52-122">키 형식을 사용 하는 컨텍스트 클래스 및 사용자 관리자 변경</span><span class="sxs-lookup"><span data-stu-id="cee52-122">Change the context class and user manager to use the key type</span></span>](#context)
- [<span data-ttu-id="cee52-123">키 유형을 사용 하 여 시작 구성 변경</span><span class="sxs-lookup"><span data-stu-id="cee52-123">Change start-up configuration to use the key type</span></span>](#startup)
- [<span data-ttu-id="cee52-124">업데이트 2를 사용 하 여 MVC에 대 한 키 형식을 전달 AccountController 변경</span><span class="sxs-lookup"><span data-stu-id="cee52-124">For MVC with Update 2, change the AccountController to pass the key type</span></span>](#mvcupdate2)
- [<span data-ttu-id="cee52-125">업데이트 3을 사용 하 여 MVC에 대 한 키 형식을 전달 AccountController 및 ManageController 변경</span><span class="sxs-lookup"><span data-stu-id="cee52-125">For MVC with Update 3, change the AccountController and ManageController to pass the key type</span></span>](#mvcupdate3)
- [<span data-ttu-id="cee52-126">업데이트 2를 사용 하 여 Web Forms에 대 한 키 형식을 전달 계정 페이지를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-126">For Web Forms with Update 2, change Account pages to pass the key type</span></span>](#webformsupdate2)
- [<span data-ttu-id="cee52-127">업데이트 3을 사용 하 여 Web Forms에 대 한 키 형식을 전달 계정 페이지를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-127">For Web Forms with Update 3, change Account pages to pass the key type</span></span>](#webformsupdate3)
- [<span data-ttu-id="cee52-128">응용 프로그램 실행된</span><span class="sxs-lookup"><span data-stu-id="cee52-128">Run application</span></span>](#run)
- [<span data-ttu-id="cee52-129">기타 리소스</span><span class="sxs-lookup"><span data-stu-id="cee52-129">Other resources</span></span>](#other)

<a id="userclass"></a>
## <a name="change-the-type-of-the-key-in-the-identity-user-class"></a><span data-ttu-id="cee52-130">Identity 사용자 클래스에 있는 키의 형식 변경</span><span class="sxs-lookup"><span data-stu-id="cee52-130">Change the type of the key in the Identity user class</span></span>

<span data-ttu-id="cee52-131">ASP.NET 웹 응용 프로그램 템플릿에서 만든 프로젝트에서 ApplicationUser 클래스는 사용자 계정에 대 한 키에 대 한 정수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-131">In your project created from the ASP.NET Web Application template, specify that the ApplicationUser class uses an integer for the key for user accounts.</span></span> <span data-ttu-id="cee52-132">IdentityModels.cs, 변경의 형식을 갖는 IdentityUser 상속할 ApplicationUser 클래스 **int** TKey 제네릭 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-132">In IdentityModels.cs, change the ApplicationUser class to inherit from IdentityUser that has a type of **int** for the TKey generic parameter.</span></span> <span data-ttu-id="cee52-133">아직 구현 하지는 세 가지 사용자 지정된 클래스의 이름을 전달할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-133">You also pass the names of three customized class which you have not implemented yet.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample1.cs?highlight=1-2)]

<span data-ttu-id="cee52-134">키의 형식을 변경한 않지만, 기본적으로 응용 프로그램의 나머지 여전히 가정 키는 문자열 합니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-134">You have changed the type of the key, but, by default, the rest of the application still assumes the key is a string.</span></span> <span data-ttu-id="cee52-135">문자열을 가정 하는 코드에서 키의 형식을 명시적으로 나타내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-135">You must explicitly indicate the type of the key in code that assumes a string.</span></span>

<span data-ttu-id="cee52-136">에 **ApplicationUser** 클래스를 변경 합니다 **GenerateUserIdentityAsync** 아래 강조 표시 된 코드에 나와 있는 것 처럼 int를 포함 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-136">In the **ApplicationUser** class, change the **GenerateUserIdentityAsync** method to include int, as shown in the highlighted code below.</span></span> <span data-ttu-id="cee52-137">이 변경은 업데이트 3 템플릿 사용 하 여 Web Forms 프로젝트에 대 한 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-137">This change is not necessary for Web Forms projects with the Update 3 template.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample2.cs?highlight=2)]

<a id="customclass"></a>
## <a name="add-customized-identity-classes-that-use-the-key-type"></a><span data-ttu-id="cee52-138">추가 키 유형을 사용 하는 사용자 지정된 Id 클래스</span><span class="sxs-lookup"><span data-stu-id="cee52-138">Add customized Identity classes that use the key type</span></span>

<span data-ttu-id="cee52-139">여전히 문자열 키를 사용 하는 Identity와 같은 다른 클래스 IdentityUserRole IdentityUserClaim, IdentityUserLogin, IdentityRole, UserStore, RoleStore에 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-139">The other Identity classes, such as IdentityUserRole, IdentityUserClaim, IdentityUserLogin, IdentityRole, UserStore, RoleStore, are still set up to use a string key.</span></span> <span data-ttu-id="cee52-140">키에 대 한 정수를 지정 하는 이러한 클래스의 새 버전을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-140">Create new versions of these classes that specify an integer for the key.</span></span> <span data-ttu-id="cee52-141">이러한 클래스의 구현 코드를 제공할 필요가 없습니다, 주로 방금 int 키로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-141">You do not need to provide much implementation code in these classes, you are primarily just setting int as the key.</span></span>

<span data-ttu-id="cee52-142">IdentityModels.cs 파일에 다음 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-142">Add the following classes to your IdentityModels.cs file.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample3.cs)]

<a id="context"></a>
## <a name="change-the-context-class-and-user-manager-to-use-the-key-type"></a><span data-ttu-id="cee52-143">키 형식을 사용 하는 컨텍스트 클래스 및 사용자 관리자 변경</span><span class="sxs-lookup"><span data-stu-id="cee52-143">Change the context class and user manager to use the key type</span></span>

<span data-ttu-id="cee52-144">IdentityModels.cs의 정의 변경 합니다 **ApplicationDbContext** 클래스를 사용 하 여 새 클래스를 사용자 지정 및 **int** 강조 표시 된 코드에 표시 된 대로 키에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-144">In IdentityModels.cs, change the definition of the **ApplicationDbContext** class to use your new customized classes and an **int** for the key, as shown in the highlighted code.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample4.cs?highlight=1-2)]

<span data-ttu-id="cee52-145">ThrowIfV1Schema 매개 변수는 생성자에서 더 이상 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-145">The ThrowIfV1Schema parameter is no longer valid in the constructor.</span></span> <span data-ttu-id="cee52-146">생성자를 변경 하 여 ThrowIfV1Schema 값을 전달 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-146">Change the constructor so it does not pass a ThrowIfV1Schema value.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample5.cs)]

<span data-ttu-id="cee52-147">IdentityConfig.cs를 열고 변경 합니다 **ApplicationUserManger** 데이터 유지를 위한 클래스를 저장 하는 새 사용자를 사용 하는 클래스와 **int** 키에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-147">Open IdentityConfig.cs, and change the **ApplicationUserManger** class to use your new user store class for persisting data and an **int** for the key.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample6.cs?highlight=1,3,12,14,32,37,48)]

<span data-ttu-id="cee52-148">업데이트 3 템플릿에서 ApplicationSignInManager 클래스를 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-148">In the Update 3 template, you must change the ApplicationSignInManager class.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample7.cs?highlight=1)]

<a id="startup"></a>
## <a name="change-start-up-configuration-to-use-the-key-type"></a><span data-ttu-id="cee52-149">키 유형을 사용 하 여 시작 구성 변경</span><span class="sxs-lookup"><span data-stu-id="cee52-149">Change start-up configuration to use the key type</span></span>

<span data-ttu-id="cee52-150">Startup.Auth.cs에서 아래 강조 표시 된 대로 OnValidateIdentity 코드를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-150">In Startup.Auth.cs, replace the OnValidateIdentity code, as highlighted below.</span></span> <span data-ttu-id="cee52-151">GetUserIdCallback 정의 문자열 값을 구문 분석 하는 정수를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-151">Notice that the getUserIdCallback definition, parses the string value into an integer.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample8.cs?highlight=7-12)]

<span data-ttu-id="cee52-152">프로젝트의 제네릭 구현을 인식 하지 못합니다 합니다 **GetUserId** 버전 2.1에는 ASP.NET Identity NuGet 패키지를 업데이트 해야 메서드</span><span class="sxs-lookup"><span data-stu-id="cee52-152">If your project does not recognize the generic implementation of the **GetUserId** method, you may need to update the ASP.NET Identity NuGet package to version 2.1</span></span>

<span data-ttu-id="cee52-153">ASP.NET Id로 사용 하는 인프라 클래스를 많이 변경 했습니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-153">You have made a lot of changes to the infrastructure classes used by ASP.NET Identity.</span></span> <span data-ttu-id="cee52-154">프로젝트 컴파일 시도 하면 많은 오류를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-154">If you try compiling the project, you will notice a lot of errors.</span></span> <span data-ttu-id="cee52-155">다행 스럽게도 나머지 오류 모두 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-155">Fortunately, the remaining errors are all similar.</span></span> <span data-ttu-id="cee52-156">Id 클래스는 정수 키에 대 한 예상 하지만 컨트롤러 (또는 Web Form)는 문자열 값을 전달 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-156">The Identity class expects an integer for the key, but the controller (or Web Form) is passing a string value.</span></span> <span data-ttu-id="cee52-157">각각의 경우에서 호출 하 여 문자열 및 정수에서 변환 해야 **GetUserId&lt;int&gt;** 합니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-157">In each case, you need to convert from a string to and integer by calling **GetUserId&lt;int&gt;**.</span></span> <span data-ttu-id="cee52-158">컴파일에서 오류 목록을 통해 작업 하거나 아래 변경 내용에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-158">You can either work through the error list from compilation or follow the changes below.</span></span>

<span data-ttu-id="cee52-159">나머지 변경 내용을 Visual Studio에서 설치한 업데이트를 만드는 중 이며 프로젝트의 유형에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-159">The remaining changes depend on the type of project you are creating and which update you have installed in Visual Studio.</span></span> <span data-ttu-id="cee52-160">다음 링크를 통해 해당 섹션으로 직접 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-160">You can go directly to the relevant section through the following links</span></span>

- [<span data-ttu-id="cee52-161">업데이트 2를 사용 하 여 MVC에 대 한 키 형식을 전달 AccountController 변경</span><span class="sxs-lookup"><span data-stu-id="cee52-161">For MVC with Update 2, change the AccountController to pass the key type</span></span>](#mvcupdate2)
- [<span data-ttu-id="cee52-162">업데이트 3을 사용 하 여 MVC에 대 한 키 형식을 전달 AccountController 및 ManageController 변경</span><span class="sxs-lookup"><span data-stu-id="cee52-162">For MVC with Update 3, change the AccountController and ManageController to pass the key type</span></span>](#mvcupdate3)
- [<span data-ttu-id="cee52-163">업데이트 2를 사용 하 여 Web Forms에 대 한 키 형식을 전달 계정 페이지를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-163">For Web Forms with Update 2, change Account pages to pass the key type</span></span>](#webformsupdate2)
- [<span data-ttu-id="cee52-164">업데이트 3을 사용 하 여 Web Forms에 대 한 키 형식을 전달 계정 페이지를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-164">For Web Forms with Update 3, change Account pages to pass the key type</span></span>](#webformsupdate3)

<a id="mvcupdate2"></a>
## <a name="for-mvc-with-update-2-change-the-accountcontroller-to-pass-the-key-type"></a><span data-ttu-id="cee52-165">업데이트 2를 사용 하 여 MVC에 대 한 키 형식을 전달 AccountController 변경</span><span class="sxs-lookup"><span data-stu-id="cee52-165">For MVC with Update 2, change the AccountController to pass the key type</span></span>

<span data-ttu-id="cee52-166">AccountController.cs 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-166">Open the AccountController.cs file.</span></span> <span data-ttu-id="cee52-167">다음 메서드를 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-167">You need to change the following methods.</span></span>

<span data-ttu-id="cee52-168">**ConfirmEmail** 메서드</span><span class="sxs-lookup"><span data-stu-id="cee52-168">**ConfirmEmail** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample9.cs?highlight=1,3)]

<span data-ttu-id="cee52-169">**한 연결을 끊을** 메서드</span><span class="sxs-lookup"><span data-stu-id="cee52-169">**Disassociate** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample10.cs?highlight=5,9)]

<span data-ttu-id="cee52-170">**Manage(ManageUserViewModel)** 메서드</span><span class="sxs-lookup"><span data-stu-id="cee52-170">**Manage(ManageUserViewModel)** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample11.cs?highlight=11,17,41)]

<span data-ttu-id="cee52-171">**LinkLoginCallback** 메서드</span><span class="sxs-lookup"><span data-stu-id="cee52-171">**LinkLoginCallback** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample12.cs?highlight=10)]

<span data-ttu-id="cee52-172">**RemoveAccountList** 메서드</span><span class="sxs-lookup"><span data-stu-id="cee52-172">**RemoveAccountList** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample13.cs?highlight=3)]

<span data-ttu-id="cee52-173">**HasPassword** 메서드</span><span class="sxs-lookup"><span data-stu-id="cee52-173">**HasPassword** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample14.cs?highlight=3)]

<span data-ttu-id="cee52-174">이제 [응용 프로그램을 실행](#run) 하 고 새 사용자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-174">You can now [run the application](#run) and register a new user.</span></span>

<a id="mvcupdate3"></a>
## <a name="for-mvc-with-update-3-change-the-accountcontroller-and-managecontroller-to-pass-the-key-type"></a><span data-ttu-id="cee52-175">업데이트 3을 사용 하 여 MVC에 대 한 키 형식을 전달 AccountController 및 ManageController 변경</span><span class="sxs-lookup"><span data-stu-id="cee52-175">For MVC with Update 3, change the AccountController and ManageController to pass the key type</span></span>

<span data-ttu-id="cee52-176">AccountController.cs 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-176">Open the AccountController.cs file.</span></span> <span data-ttu-id="cee52-177">다음 메서드를 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-177">You need to change the following method.</span></span>

<span data-ttu-id="cee52-178">**ConfirmEmail** 메서드</span><span class="sxs-lookup"><span data-stu-id="cee52-178">**ConfirmEmail** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample15.cs?highlight=1,3)]

<span data-ttu-id="cee52-179">**SendCode** 메서드</span><span class="sxs-lookup"><span data-stu-id="cee52-179">**SendCode** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample16.cs?highlight=4)]

<span data-ttu-id="cee52-180">ManageController.cs 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-180">Open the ManageController.cs file.</span></span> <span data-ttu-id="cee52-181">다음 메서드를 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-181">You need to change the following methods.</span></span>

<span data-ttu-id="cee52-182">**인덱스** 메서드</span><span class="sxs-lookup"><span data-stu-id="cee52-182">**Index** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample17.cs?highlight=15-17)]

<span data-ttu-id="cee52-183">**RemoveLogin** 메서드</span><span class="sxs-lookup"><span data-stu-id="cee52-183">**RemoveLogin** methods</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample18.cs?highlight=3,13,17)]

<span data-ttu-id="cee52-184">**AddPhoneNumber** 메서드</span><span class="sxs-lookup"><span data-stu-id="cee52-184">**AddPhoneNumber** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample19.cs?highlight=9)]

<span data-ttu-id="cee52-185">**EnableTwoFactorAuthentication** 메서드</span><span class="sxs-lookup"><span data-stu-id="cee52-185">**EnableTwoFactorAuthentication** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample20.cs?highlight=3-4)]

<span data-ttu-id="cee52-186">**DisableTwoFactorAuthentication** 메서드</span><span class="sxs-lookup"><span data-stu-id="cee52-186">**DisableTwoFactorAuthentication** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample21.cs?highlight=3-4)]

<span data-ttu-id="cee52-187">**VerifyPhoneNumber** 메서드</span><span class="sxs-lookup"><span data-stu-id="cee52-187">**VerifyPhoneNumber** methods</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample22.cs?highlight=4,18,21)]

<span data-ttu-id="cee52-188">**RemovePhoneNumber** 메서드</span><span class="sxs-lookup"><span data-stu-id="cee52-188">**RemovePhoneNumber** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample23.cs?highlight=3,8)]

<span data-ttu-id="cee52-189">**ChangePassword** 메서드</span><span class="sxs-lookup"><span data-stu-id="cee52-189">**ChangePassword** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample24.cs?highlight=10,13)]

<span data-ttu-id="cee52-190">**SetPassword** 메서드</span><span class="sxs-lookup"><span data-stu-id="cee52-190">**SetPassword** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample25.cs?highlight=5,8)]

<span data-ttu-id="cee52-191">**ManageLogins** 메서드</span><span class="sxs-lookup"><span data-stu-id="cee52-191">**ManageLogins** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample26.cs?highlight=7,12)]

<span data-ttu-id="cee52-192">**LinkLoginCallback** 메서드</span><span class="sxs-lookup"><span data-stu-id="cee52-192">**LinkLoginCallback** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample27.cs?highlight=8)]

<span data-ttu-id="cee52-193">**HasPassword** 메서드</span><span class="sxs-lookup"><span data-stu-id="cee52-193">**HasPassword** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample28.cs?highlight=3)]

<span data-ttu-id="cee52-194">**HasPhoneNumber** 메서드</span><span class="sxs-lookup"><span data-stu-id="cee52-194">**HasPhoneNumber** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample29.cs?highlight=3)]

<span data-ttu-id="cee52-195">이제 [응용 프로그램을 실행](#run) 하 고 새 사용자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-195">You can now [run the application](#run) and register a new user.</span></span>

<a id="webformsupdate2"></a>
## <a name="for-web-forms-with-update-2-change-account-pages-to-pass-the-key-type"></a><span data-ttu-id="cee52-196">업데이트 2를 사용 하 여 Web Forms에 대 한 키 형식을 전달 계정 페이지를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-196">For Web Forms with Update 2, change Account pages to pass the key type</span></span>

<span data-ttu-id="cee52-197">업데이트 2를 사용 하 여 Web Forms에 대 한 다음 페이지를 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-197">For Web Forms with Update 2, you need to change the following pages.</span></span>

<span data-ttu-id="cee52-198">**Confirm.aspx.cx**</span><span class="sxs-lookup"><span data-stu-id="cee52-198">**Confirm.aspx.cx**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample30.cs?highlight=8)]

<span data-ttu-id="cee52-199">**RegisterExternalLogin.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="cee52-199">**RegisterExternalLogin.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample31.cs?highlight=36)]

<span data-ttu-id="cee52-200">**Manage.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="cee52-200">**Manage.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample32.cs?highlight=3,22,47,52,69,85,93,98)]

<span data-ttu-id="cee52-201">이제 [응용 프로그램을 실행](#run) 하 고 새 사용자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-201">You can now [run the application](#run) and register a new user.</span></span>

<a id="webformsupdate3"></a>
## <a name="for-web-forms-with-update-3-change-account-pages-to-pass-the-key-type"></a><span data-ttu-id="cee52-202">업데이트 3을 사용 하 여 Web Forms에 대 한 키 형식을 전달 계정 페이지를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-202">For Web Forms with Update 3, change Account pages to pass the key type</span></span>

<span data-ttu-id="cee52-203">업데이트 3을 사용 하 여 Web Forms에 대 한 다음 페이지를 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-203">For Web Forms with Update 3, you need to change the following pages.</span></span>

<span data-ttu-id="cee52-204">**Confirm.aspx.cx**</span><span class="sxs-lookup"><span data-stu-id="cee52-204">**Confirm.aspx.cx**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample33.cs?highlight=8)]

<span data-ttu-id="cee52-205">**RegisterExternalLogin.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="cee52-205">**RegisterExternalLogin.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample34.cs?highlight=36)]

<span data-ttu-id="cee52-206">**Manage.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="cee52-206">**Manage.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample35.cs?highlight=11,27,32,34,82,87,99,108)]

<span data-ttu-id="cee52-207">**VerifyPhoneNumber.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="cee52-207">**VerifyPhoneNumber.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample36.cs?highlight=8,23,27)]

<span data-ttu-id="cee52-208">**AddPhoneNumber.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="cee52-208">**AddPhoneNumber.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample37.cs?highlight=7)]

<span data-ttu-id="cee52-209">**ManagePassword.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="cee52-209">**ManagePassword.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample38.cs?highlight=11,47,50,68)]

<span data-ttu-id="cee52-210">**ManageLogins.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="cee52-210">**ManageLogins.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample39.cs?highlight=16,23,32,41,45)]

<span data-ttu-id="cee52-211">**TwoFactorAuthenticationSignIn.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="cee52-211">**TwoFactorAuthenticationSignIn.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample40.cs?highlight=14-15,29,53)]

<a id="run"></a>
## <a name="run-application"></a><span data-ttu-id="cee52-212">응용 프로그램 실행된</span><span class="sxs-lookup"><span data-stu-id="cee52-212">Run application</span></span>

<span data-ttu-id="cee52-213">모든 기본 웹 응용 프로그램 템플릿에 필요한 변경 작업을 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-213">You have finished all of the required changes to the default Web Application template.</span></span> <span data-ttu-id="cee52-214">응용 프로그램을 실행 하 고 새 사용자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-214">Run the application and register a new user.</span></span> <span data-ttu-id="cee52-215">사용자를 등록 한 후 AspNetUsers 테이블에는 정수 Id 열에 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-215">After registering the user, you will notice that the AspNetUsers table has an Id column that is an integer.</span></span>

![새 기본 키](change-primary-key-for-users-in-aspnet-identity/_static/image1.png)

<span data-ttu-id="cee52-217">이전에 만든 ASP.NET Id 테이블 기본 키를 사용 하 여 일부 추가 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-217">If you have previously created the ASP.NET Identity tables with a different primary key, you need to make some additional changes.</span></span> <span data-ttu-id="cee52-218">가능 하면 기존 데이터베이스를 삭제 하기만 합니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-218">If possible, just delete the existing database.</span></span> <span data-ttu-id="cee52-219">웹 응용 프로그램을 실행 하 고 새 사용자를 추가 하는 경우 데이터베이스와 정확한 디자인 다시 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-219">The database will be re-created with the correct design when you run the web application and add a new user.</span></span> <span data-ttu-id="cee52-220">삭제 수 없는 경우, 테이블을 변경 하도록 code first 마이그레이션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-220">If deletion is not possible, run code first migrations to change the tables.</span></span> <span data-ttu-id="cee52-221">그러나 새 정수 기본 키를 됩니다 하지 수 설정 데이터베이스에서 SQL ID 속성으로.</span><span class="sxs-lookup"><span data-stu-id="cee52-221">However, the new integer primary key will not be set up as a SQL IDENTITY property in the database.</span></span> <span data-ttu-id="cee52-222">Id 열의 ID로 수동으로 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cee52-222">You must manually set the Id column as an IDENTITY.</span></span>

<a id="other"></a>
## <a name="other-resources"></a><span data-ttu-id="cee52-223">기타 리소스</span><span class="sxs-lookup"><span data-stu-id="cee52-223">Other resources</span></span>

- [<span data-ttu-id="cee52-224">ASP.NET ID에 대한 사용자 지정 저장소 공급자 개요</span><span class="sxs-lookup"><span data-stu-id="cee52-224">Overview of Custom Storage Providers for ASP.NET Identity</span></span>](overview-of-custom-storage-providers-for-aspnet-identity.md)
- [<span data-ttu-id="cee52-225">기존 웹 사이트를 SQL 멤버 자격에서 ASP.NET ID로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="cee52-225">Migrating an Existing Website from SQL Membership to ASP.NET Identity</span></span>](../migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md)
- [<span data-ttu-id="cee52-226">멤버 자격 및 ASP.NET Id로 사용자 프로필에 대 한 범용 공급자 데이터 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="cee52-226">Migrating Universal Provider Data for Membership and User Profiles to ASP.NET Identity</span></span>](../migrations/migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity.md)
- <span data-ttu-id="cee52-227">[샘플 응용 프로그램](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/ChangePK/readme.txt) 변경 된 기본 키를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="cee52-227">[Sample application](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/ChangePK/readme.txt) with changed primary key</span></span>
