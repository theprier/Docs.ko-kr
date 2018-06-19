---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
title: '7 단계: 멤버 자격 및 권한 부여 | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다. 7 부에서는 멤버 자격 및 권한 부여에 설명 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/13/2010
ms.topic: article
ms.assetid: c8511ebe-68bc-4240-87c3-d5ced84a3f37
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
msc.type: authoredcontent
ms.openlocfilehash: a0f599da4691c5bb7c8e6f01625fc0e94ce0eac8
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30879506"
---
<a name="part-7-membership-and-authorization"></a><span data-ttu-id="170d7-104">7 단계: 멤버 자격 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="170d7-104">Part 7: Membership and Authorization</span></span>
====================
<span data-ttu-id="170d7-105">으로 [Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="170d7-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="170d7-106">MVC Music Store는 소개 하 고 웹 개발에 대 한 ASP.NET MVC와 Visual Studio를 사용 하는 방법을 단계별로 설명 하는 자습서 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="170d7-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="170d7-107">MVC Music Store는 온라인 음악 앨범 판매 및 기본 사이트 관리, 사용자 로그인 및 장바구니 기능을 구현 하는 간단한 샘플 저장소 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="170d7-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="170d7-108">이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="170d7-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="170d7-109">7 부에서는 멤버 자격 및 권한 부여에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="170d7-109">Part 7 covers Membership and Authorization.</span></span>


<span data-ttu-id="170d7-110">이 저장소 관리자 컨트롤러는 사이트를 방문 하는 모든를 현재 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="170d7-110">Our Store Manager controller is currently accessible to anyone visiting our site.</span></span> <span data-ttu-id="170d7-111">사이트 관리자에 게 사용 권한을 제한 하려면이 옵션을 변경해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="170d7-111">Let's change this to restrict permission to site administrators.</span></span>

## <a name="adding-the-accountcontroller-and-views"></a><span data-ttu-id="170d7-112">AccountController 및 뷰 추가</span><span class="sxs-lookup"><span data-stu-id="170d7-112">Adding the AccountController and Views</span></span>

<span data-ttu-id="170d7-113">전체 ASP.NET MVC 3 웹 응용 프로그램 템플릿 및 ASP.NET MVC 3 빈 웹 응용 프로그램 템플릿은 간의 한 가지 차이점은 빈 템플릿 계정 컨트롤러를 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="170d7-113">One difference between the full ASP.NET MVC 3 Web Application template and the ASP.NET MVC 3 Empty Web Application template is that the empty template doesn't include an Account Controller.</span></span> <span data-ttu-id="170d7-114">계정 컨트롤러 전체 ASP.NET MVC 3 웹 응용 프로그램 템플릿에서 만들어진 새 ASP.NET MVC 응용 프로그램에서 일부 파일을 복사 하 여 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="170d7-114">We'll add an Account Controller by copying a few files from a new ASP.NET MVC application created from the full ASP.NET MVC 3 Web Application template.</span></span>

<span data-ttu-id="170d7-115">전체 ASP.NET MVC 3 웹 응용 프로그램 템플릿을 사용 하 여 새 ASP.NET MVC 응용 프로그램을 만들고 다음 파일을 프로젝트에 동일한 디렉터리에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="170d7-115">Create a new ASP.NET MVC application using the full ASP.NET MVC 3 Web Application template and copy the following files into the same directories in our project:</span></span>

1. <span data-ttu-id="170d7-116">AccountController.cs 컨트롤러 디렉터리에 복사</span><span class="sxs-lookup"><span data-stu-id="170d7-116">Copy AccountController.cs in the Controllers directory</span></span>
2. <span data-ttu-id="170d7-117">AccountModels 모델 디렉터리에 복사</span><span class="sxs-lookup"><span data-stu-id="170d7-117">Copy AccountModels in the Models directory</span></span>
3. <span data-ttu-id="170d7-118">Views 디렉터리 내에 계정 디렉터리를 만들고의 네 가지 보기를 모두 복사</span><span class="sxs-lookup"><span data-stu-id="170d7-118">Create an Account directory inside the Views directory and copy all four views in</span></span>

<span data-ttu-id="170d7-119">MvcMusicStore로 시작 하도록 컨트롤러와 모델 클래스에 대 한 네임 스페이스를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="170d7-119">Change the namespace for the Controller and Model classes so they begin with MvcMusicStore.</span></span> <span data-ttu-id="170d7-120">AccountController 클래스 MvcMusicStore.Controllers 네임 스페이스를 사용 해야 하 고 AccountModels 클래스 MvcMusicStore.Models 네임 스페이스를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="170d7-120">The AccountController class should use the MvcMusicStore.Controllers namespace, and the AccountModels class should use the MvcMusicStore.Models namespace.</span></span>

<span data-ttu-id="170d7-121">*참고: 이러한 파일 우리 복사해 올 사이트 디자인 파일 자습서의 시작 부분에서 MvcMusicStore Assets.zip 다운로드에 사용할 수도 있습니다. 멤버 자격 파일은 코드 디렉터리에 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="170d7-121">*Note: These files are also available in the MvcMusicStore-Assets.zip download from which we copied our site design files at the beginning of the tutorial. The Membership files are located in the Code directory.*</span></span>

<span data-ttu-id="170d7-122">업데이트 된 솔루션은 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="170d7-122">The updated solution should look like the following:</span></span>

![](mvc-music-store-part-7/_static/image1.png)

## <a name="adding-an-administrative-user-with-the-aspnet-configuration-site"></a><span data-ttu-id="170d7-123">ASP.NET 구성 사이트와 관리 사용자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="170d7-123">Adding an Administrative User with the ASP.NET Configuration site</span></span>

<span data-ttu-id="170d7-124">웹 사이트에서 권한 부여를 요구에서는 먼저 사용자를 만들려면 액세스할 수 있는 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="170d7-124">Before we require Authorization in our website, we'll need to create a user with access.</span></span> <span data-ttu-id="170d7-125">사용자를 만드는 가장 쉬운 방법은 기본 제공 ASP.NET 구성 웹 사이트를 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="170d7-125">The easiest way to create a user is to use the built-in ASP.NET Configuration website.</span></span>

<span data-ttu-id="170d7-126">다음 솔루션 탐색기에서 아이콘을 클릭 하 여 ASP.NET 구성 웹 사이트를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="170d7-126">Launch the ASP.NET Configuration website by clicking following the icon in the Solution Explorer.</span></span>

![](mvc-music-store-part-7/_static/image2.png)

<span data-ttu-id="170d7-127">그러면 웹 사이트 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="170d7-127">This launches a configuration website.</span></span> <span data-ttu-id="170d7-128">보안 탭의 홈 화면을 클릭 한 다음 화면 가운데의 "역할을 사용 하도록" 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="170d7-128">Click on the Security tab on the home screen, then click the "Enable roles" link in the center of the screen.</span></span>

![](mvc-music-store-part-7/_static/image3.png)

<span data-ttu-id="170d7-129">"역할 만들기 또는 관리" 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="170d7-129">Click the "Create or Manage roles" link.</span></span>

![](mvc-music-store-part-7/_static/image4.png)

<span data-ttu-id="170d7-130">역할 이름으로 "Administrator"를 입력 하 고 역할 추가 단추를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="170d7-130">Enter "Administrator" as the role name and press the Add Role button.</span></span>

![](mvc-music-store-part-7/_static/image5.png)

<span data-ttu-id="170d7-131">뒤로 단추를 클릭 한 다음 왼쪽에서 사용자 만들기 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="170d7-131">Click the Back button, then click on the Create user link on the left side.</span></span>

![](mvc-music-store-part-7/_static/image6.png)

<span data-ttu-id="170d7-132">다음 정보를 사용 하 여 왼쪽에 사용자 정보 필드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="170d7-132">Fill in the user information fields on the left using the following information:</span></span>

| <span data-ttu-id="170d7-133">**필드**</span><span class="sxs-lookup"><span data-stu-id="170d7-133">**Field**</span></span> | <span data-ttu-id="170d7-134">**값**</span><span class="sxs-lookup"><span data-stu-id="170d7-134">**Value**</span></span> |
| --- | --- |
| <span data-ttu-id="170d7-135">**사용자 이름**</span><span class="sxs-lookup"><span data-stu-id="170d7-135">**User Name**</span></span> | <span data-ttu-id="170d7-136">관리자</span><span class="sxs-lookup"><span data-stu-id="170d7-136">Administrator</span></span> |
| <span data-ttu-id="170d7-137">**암호**</span><span class="sxs-lookup"><span data-stu-id="170d7-137">**Password**</span></span> | <span data-ttu-id="170d7-138">password123!</span><span class="sxs-lookup"><span data-stu-id="170d7-138">password123!</span></span> |
| <span data-ttu-id="170d7-139">**암호 확인**</span><span class="sxs-lookup"><span data-stu-id="170d7-139">**Confirm Password**</span></span> | <span data-ttu-id="170d7-140">password123!</span><span class="sxs-lookup"><span data-stu-id="170d7-140">password123!</span></span> |
| <span data-ttu-id="170d7-141">**전자 메일**</span><span class="sxs-lookup"><span data-stu-id="170d7-141">**E-mail**</span></span> | <span data-ttu-id="170d7-142">(모든 전자 메일 주소는 동작)</span><span class="sxs-lookup"><span data-stu-id="170d7-142">(any email address will work)</span></span> |
| <span data-ttu-id="170d7-143">**보안 질문**</span><span class="sxs-lookup"><span data-stu-id="170d7-143">**Security Question**</span></span> | <span data-ttu-id="170d7-144">(원하는)</span><span class="sxs-lookup"><span data-stu-id="170d7-144">(whatever you like)</span></span> |
| <span data-ttu-id="170d7-145">**보안 대답**</span><span class="sxs-lookup"><span data-stu-id="170d7-145">**Security Answer**</span></span> | <span data-ttu-id="170d7-146">(원하는)</span><span class="sxs-lookup"><span data-stu-id="170d7-146">(whatever you like)</span></span> |

<span data-ttu-id="170d7-147">*참고: 원하는 모든 암호를 물론 사용할 수 있습니다. 기본 암호 보안 설정에는 7 자 이며 하나의 영숫자가 아닌 문자를 포함 하는 암호가 필요 합니다.*</span><span class="sxs-lookup"><span data-stu-id="170d7-147">*Note: You can of course use any password you'd like. The default password security settings require a password that is 7 characters long and contains one non-alphanumeric character.*</span></span>

<span data-ttu-id="170d7-148">이 사용자에 대 한 관리자 역할을 선택 하 고 사용자 만들기 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="170d7-148">Select the Administrator role for this user, and click the Create User button.</span></span>

![](mvc-music-store-part-7/_static/image7.png)

<span data-ttu-id="170d7-149">이 시점에서 사용자를 성공적으로 만들어졌는지 없다는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="170d7-149">At this point, you should see a message indicating that the user was created successfully.</span></span>

![](mvc-music-store-part-7/_static/image8.png)

<span data-ttu-id="170d7-150">이제 브라우저 창을 닫을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="170d7-150">You can now close the browser window.</span></span>

## <a name="role-based-authorization"></a><span data-ttu-id="170d7-151">역할 기반 권한 부여</span><span class="sxs-lookup"><span data-stu-id="170d7-151">Role-based Authorization</span></span>

<span data-ttu-id="170d7-152">이제 사용자 클래스에 있는 컨트롤러 작업에 액세스 하려면 관리자 역할에 되어야 함을 지정 하는 [Authorize] 특성을 사용 하 여 StoreManagerController에 액세스를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="170d7-152">Now we can restrict access to the StoreManagerController using the [Authorize] attribute, specifying that the user must be in the Administrator role to access any controller action in the class.</span></span>

[!code-csharp[Main](mvc-music-store-part-7/samples/sample1.cs)]

<span data-ttu-id="170d7-153">*참고: 특정 작업 메서드에 적용 뿐만 아니라 컨트롤러 클래스 수준에서 [Authorize] 특성에 배치할 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="170d7-153">*Note: The [Authorize] attribute can be placed on specific action methods as well as at the Controller class level.*</span></span>

<span data-ttu-id="170d7-154">로그온에 대화 상자를 불러오는 이제 /StoreManager로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="170d7-154">Now browsing to /StoreManager brings up a Log On dialog:</span></span>

![](mvc-music-store-part-7/_static/image9.png)

<span data-ttu-id="170d7-155">이 새 관리자 계정으로 로그온 한 후 we 're 전으로 앨범 편집 화면으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="170d7-155">After logging on with our new Administrator account, we're able to go to the Album Edit screen as before.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="170d7-156">[이전](mvc-music-store-part-6.md)
> [다음](mvc-music-store-part-8.md)</span><span class="sxs-lookup"><span data-stu-id="170d7-156">[Previous](mvc-music-store-part-6.md)
[Next](mvc-music-store-part-8.md)</span></span>
