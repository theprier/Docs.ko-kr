---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-4
title: '4 부: 관리 보기 추가 | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/04/2012
ms.topic: article
ms.assetid: 792f4513-a508-4d14-a0dd-1a2fe282c7bb
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-4
msc.type: authoredcontent
ms.openlocfilehash: 599f684ba200821d7fcd33819937c5a5b5a29ce8
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37371053"
---
<a name="part-4-adding-an-admin-view"></a><span data-ttu-id="8d65f-102">4 부: 관리 보기 추가</span><span class="sxs-lookup"><span data-stu-id="8d65f-102">Part 4: Adding an Admin View</span></span>
====================
<span data-ttu-id="8d65f-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="8d65f-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="8d65f-104">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="8d65f-104">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-an-admin-view"></a><span data-ttu-id="8d65f-105">관리 보기 추가</span><span class="sxs-lookup"><span data-stu-id="8d65f-105">Add an Admin View</span></span>

<span data-ttu-id="8d65f-106">이제에서는 클라이언트 쪽으로 설정 하 고 관리 컨트롤러에서 데이터를 사용할 수 있는 페이지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d65f-106">Now we'll turn to the client side, and add a page that can consume data from the Admin controller.</span></span> <span data-ttu-id="8d65f-107">페이지 만들기, 편집 또는 컨트롤러에 AJAX 요청을 전송 하 여 제품을 삭제 하는 사용자를 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d65f-107">The page will allow users to create, edit, or delete products, by sending AJAX requests to the controller.</span></span>

<span data-ttu-id="8d65f-108">솔루션 탐색기에서 컨트롤러 폴더를 확장 하 고 HomeController.cs 라는 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8d65f-108">In Solution Explorer, expand the Controllers folder and open the file named HomeController.cs.</span></span> <span data-ttu-id="8d65f-109">이 파일에는 MVC 컨트롤러를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8d65f-109">This file contains an MVC controller.</span></span> <span data-ttu-id="8d65f-110">라는 메서드를 추가 `Admin`:</span><span class="sxs-lookup"><span data-stu-id="8d65f-110">Add a method named `Admin`:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample1.cs)]

<span data-ttu-id="8d65f-111">합니다 **HttpRouteUrl** 메서드 웹 API에 대 한 URI를 만들고 나중에 대 한 뷰 모음에 저장이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d65f-111">The **HttpRouteUrl** method creates the URI to the web API, and we store this in the view bag for later.</span></span>

<span data-ttu-id="8d65f-112">다음으로 내에 텍스트 커서를 배치 합니다 `Admin` 동작 메서드를 마우스 오른쪽 단추로 **뷰 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="8d65f-112">Next, position the text cursor within the `Admin` action method, then right-click and select **Add View**.</span></span> <span data-ttu-id="8d65f-113">그러면 합니다 **뷰 추가** 대화 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d65f-113">This will bring up the **Add View** dialog.</span></span>

![](using-web-api-with-entity-framework-part-4/_static/image1.png)

<span data-ttu-id="8d65f-114">에 **뷰 추가** 대화 상자에서 이름 "Admin" 보기.</span><span class="sxs-lookup"><span data-stu-id="8d65f-114">In the **Add View** dialog, name the view "Admin".</span></span> <span data-ttu-id="8d65f-115">라는 레이블이 있는 확인란을 선택 **강력한 형식의 뷰를 만들**합니다.</span><span class="sxs-lookup"><span data-stu-id="8d65f-115">Select the check box labeled **Create a strongly-typed view**.</span></span> <span data-ttu-id="8d65f-116">아래 **모델 클래스**, "Product (ProductStore.Models)"를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d65f-116">Under **Model Class**, select "Product (ProductStore.Models)".</span></span> <span data-ttu-id="8d65f-117">다른 모든 옵션을 기본값으로 그대로입니다.</span><span class="sxs-lookup"><span data-stu-id="8d65f-117">Leave all the other options as their default values.</span></span>

![](using-web-api-with-entity-framework-part-4/_static/image2.png)

<span data-ttu-id="8d65f-118">클릭 **추가** Views/Home 아래 Admin.cshtml 라는 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d65f-118">Clicking **Add** adds a file named Admin.cshtml under Views/Home.</span></span> <span data-ttu-id="8d65f-119">이 파일을 열고 다음 HTML을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d65f-119">Open this file and add the following HTML.</span></span> <span data-ttu-id="8d65f-120">이 HTML 페이지의 구조를 정의 하지만 기능이 없습니다 아직 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d65f-120">This HTML defines the structure of the page, but no functionality is wired up yet.</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-4/samples/sample2.cshtml)]

## <a name="create-a-link-to-the-admin-page"></a><span data-ttu-id="8d65f-121">관리 페이지에 대 한 링크 만들기</span><span class="sxs-lookup"><span data-stu-id="8d65f-121">Create a Link to the Admin Page</span></span>

<span data-ttu-id="8d65f-122">솔루션 탐색기에서 Views 폴더를 확장 한 다음 공유 폴더를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d65f-122">In Solution Explorer, expand the Views folder and then expand the Shared folder.</span></span> <span data-ttu-id="8d65f-123">라는 파일을 열고 \_Layout.cshtml 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d65f-123">Open the file named \_Layout.cshtml.</span></span> <span data-ttu-id="8d65f-124">찾을 합니다 **ul** 요소 id 사용 하 여 = "메뉴" 및 관리 뷰에 대 한 작업 링크:</span><span class="sxs-lookup"><span data-stu-id="8d65f-124">Locate the **ul** element with id = "menu", and an action link for the Admin view:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-4/samples/sample3.cshtml)]

> [!NOTE]
> <span data-ttu-id="8d65f-125">샘플 프로젝트와 몇 가지 디자인과 같은 다른 변경 "사용자 로고는 여기" 문자열을 대체에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d65f-125">In the sample project, I made a few other cosmetic changes, such as replacing the string "Your logo here".</span></span> <span data-ttu-id="8d65f-126">이러한 응용 프로그램의 기능에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8d65f-126">These don't affect the functionality of the application.</span></span> <span data-ttu-id="8d65f-127">프로젝트를 다운로드 하 고 파일을 비교할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d65f-127">You can download the project and compare the files.</span></span>


<span data-ttu-id="8d65f-128">응용 프로그램을 실행 하 고 홈페이지의 위쪽에 표시 되는 "Admin" 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d65f-128">Run the application and click the "Admin" link that appears at the top of the home page.</span></span> <span data-ttu-id="8d65f-129">관리 페이지는 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d65f-129">The Admin page should look like the following:</span></span>

![](using-web-api-with-entity-framework-part-4/_static/image3.png)

<span data-ttu-id="8d65f-130">오른쪽 이제 페이지 작업 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8d65f-130">Right now, the page doesn't do anything.</span></span> <span data-ttu-id="8d65f-131">다음 섹션에서는 동적 UI를 만들기 위해 Knockout.js 사용 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8d65f-131">In the next section, we'll use Knockout.js to create a dynamic UI.</span></span>

## <a name="add-authorization"></a><span data-ttu-id="8d65f-132">권한 부여 추가</span><span class="sxs-lookup"><span data-stu-id="8d65f-132">Add Authorization</span></span>

<span data-ttu-id="8d65f-133">관리 페이지는 현재 사이트를 방문 하는 모든 사용자에 게 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d65f-133">The Admin page is currently accessible to anyone visiting the site.</span></span> <span data-ttu-id="8d65f-134">관리자에 게 사용 권한을 제한 하려면이 옵션을 변경해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8d65f-134">Let's change this to restrict permission to administrators.</span></span>

<span data-ttu-id="8d65f-135">"관리자" 역할 및 관리자 사용자를 추가 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d65f-135">Start by adding an "Administrator" role and an administrator user.</span></span> <span data-ttu-id="8d65f-136">솔루션 탐색기에서 필터 폴더를 확장 하 고 InitializeSimpleMembershipAttribute.cs 라는 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8d65f-136">In Solution Explorer, expand the Filters folder and open the file named InitializeSimpleMembershipAttribute.cs.</span></span> <span data-ttu-id="8d65f-137">찾을 `SimpleMembershipInitializer` 생성자입니다.</span><span class="sxs-lookup"><span data-stu-id="8d65f-137">Locate the `SimpleMembershipInitializer` constructor.</span></span> <span data-ttu-id="8d65f-138">호출한 후 **WebSecurity.InitializeDatabaseConnection**, 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d65f-138">After the call to **WebSecurity.InitializeDatabaseConnection**, add the following code:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample4.cs)]

<span data-ttu-id="8d65f-139">이 간단한 방법은 "Administrator" 역할을 추가 하 고 역할에 대 한 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8d65f-139">This is a quick-and-dirty way to add the "Administrator" role and create a user for the role.</span></span>

<span data-ttu-id="8d65f-140">솔루션 탐색기에서 컨트롤러 폴더를 확장 하 고 HomeController.cs 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8d65f-140">In Solution Explorer, expand the Controllers folder and open the HomeController.cs file.</span></span> <span data-ttu-id="8d65f-141">추가 된 **권한 부여** 특성을 `Admin` 메서드.</span><span class="sxs-lookup"><span data-stu-id="8d65f-141">Add the **Authorize** attribute to the `Admin` method.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample5.cs)]

<span data-ttu-id="8d65f-142">AdminController.cs 파일을 열고 추가 된 **권한 부여** 전체 특성 `AdminController` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="8d65f-142">Open the AdminController.cs file and add the **Authorize** attribute to the entire `AdminController` class.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample6.cs)]

> [!NOTE]
> <span data-ttu-id="8d65f-143">MVC 및 Web API 모두 정의 **권한 부여** 특성을 다른 네임 스페이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d65f-143">MVC and Web API both define **Authorize** attributes, in different namespaces.</span></span> <span data-ttu-id="8d65f-144">MVC를 사용 **System.Web.Mvc.AuthorizeAttribute**반면 웹 API를 사용 하 여 **System.Web.Http.AuthorizeAttribute**합니다.</span><span class="sxs-lookup"><span data-stu-id="8d65f-144">MVC uses **System.Web.Mvc.AuthorizeAttribute**, while Web API uses **System.Web.Http.AuthorizeAttribute**.</span></span>


<span data-ttu-id="8d65f-145">이제 관리자만 관리 페이지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d65f-145">Now only administrators can view the Admin page.</span></span> <span data-ttu-id="8d65f-146">또한 관리 컨트롤러에 HTTP 요청을 보낼 경우 요청 된 인증 쿠키를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d65f-146">Also, if you send an HTTP request to the Admin controller, the request must contain an authentication cookie.</span></span> <span data-ttu-id="8d65f-147">그렇지 않은 경우 서버는 HTTP 401 (권한 없음) 응답을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="8d65f-147">If not, the server sends an HTTP 401 (Unauthorized) response.</span></span> <span data-ttu-id="8d65f-148">GET 요청을 전송 하 여 Fiddler이을 볼 수 있습니다 `http://localhost:*port*/api/admin`합니다.</span><span class="sxs-lookup"><span data-stu-id="8d65f-148">You can see this in Fiddler by sending a GET request to `http://localhost:*port*/api/admin`.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8d65f-149">[이전](using-web-api-with-entity-framework-part-3.md)
> [다음](using-web-api-with-entity-framework-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="8d65f-149">[Previous](using-web-api-with-entity-framework-part-3.md)
[Next](using-web-api-with-entity-framework-part-5.md)</span></span>
