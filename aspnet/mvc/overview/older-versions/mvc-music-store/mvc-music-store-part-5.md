---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
title: '5 부: 폼 편집 및 템플릿 | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 5 부에서는 폼 편집 및 템플릿 설명합니다.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 6b09413a-6d6a-425a-87c9-629f91b91b28
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
msc.type: authoredcontent
ms.openlocfilehash: c1065dcb45b6d28672edba32b95c7fc476c8b944
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41838874"
---
<a name="part-5-edit-forms-and-templating"></a><span data-ttu-id="eb213-104">5 부: 폼 편집 및 템플릿</span><span class="sxs-lookup"><span data-stu-id="eb213-104">Part 5: Edit Forms and Templating</span></span>
====================
<span data-ttu-id="eb213-105">[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="eb213-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="eb213-106">MVC Music Store 자습서 응용 프로그램을 소개 하 고 웹 개발을 위한 ASP.NET MVC 및 Visual Studio를 사용 하는 방법을 단계별로 설명 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="eb213-107">MVC Music Store는 온라인 음악 앨범을 판매 하 고 기본 사이트 관리, 사용자 로그인 및 장바구니 기능을 구현 하는 간단한 샘플 저장소 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>
> 
> <span data-ttu-id="eb213-108">이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="eb213-109">5 부에서는 폼 편집 및 템플릿 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-109">Part 5 covers Edit Forms and Templating.</span></span>


<span data-ttu-id="eb213-110">이전 장에서 된 데이터베이스에서 데이터를 로드 하 고 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-110">In the past chapter, we were loading data from our database and displaying it.</span></span> <span data-ttu-id="eb213-111">이 챕터에서는 또한 데이터를 편집 지원할 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-111">In this chapter, we'll also enable editing the data.</span></span>

## <a name="creating-the-storemanagercontroller"></a><span data-ttu-id="eb213-112">StoreManagerController 만들기</span><span class="sxs-lookup"><span data-stu-id="eb213-112">Creating the StoreManagerController</span></span>

<span data-ttu-id="eb213-113">라는 새 컨트롤러 만들기부터 시작 합니다 **StoreManagerController**합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-113">We'll begin by creating a new controller called **StoreManagerController**.</span></span> <span data-ttu-id="eb213-114">이 컨트롤러에 대 한을 받겠습니다 ASP.NET MVC 3 도구 업데이트에서 사용할 수 있는 스 캐 폴딩 기능을 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-114">For this controller, we will be taking advantage of the Scaffolding features available in the ASP.NET MVC 3 Tools Update.</span></span> <span data-ttu-id="eb213-115">아래와 같이 컨트롤러 추가 대화 상자에 대 한 옵션을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-115">Set the options for the Add Controller dialog as shown below.</span></span>

![](mvc-music-store-part-5/_static/image1.png)

<span data-ttu-id="eb213-116">추가 단추를 클릭 하면 ASP.NET MVC 3 스 캐 폴딩 메커니즘을 적절 한 작업을 수행 하는 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-116">When you click the Add button, you'll see that the ASP.NET MVC 3 scaffolding mechanism does a good amount of work for you:</span></span>

- <span data-ttu-id="eb213-117">Entity Framework 지역 변수를 사용 하 여 새 StoreManagerController 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-117">It creates the new StoreManagerController with a local Entity Framework variable</span></span>
- <span data-ttu-id="eb213-118">프로젝트의 Views 폴더에 StoreManager 폴더 추가</span><span class="sxs-lookup"><span data-stu-id="eb213-118">It adds a StoreManager folder to the project's Views folder</span></span>
- <span data-ttu-id="eb213-119">Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml, 및 Index.cshtml 보기를 강력한 앨범 클래스에 추가</span><span class="sxs-lookup"><span data-stu-id="eb213-119">It adds Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml, and Index.cshtml view, strongly typed to the Album class</span></span>

![](mvc-music-store-part-5/_static/image2.png)

<span data-ttu-id="eb213-120">StoreManager 컨트롤러 클래스가 새로 포함 CRUD (만들기, 읽기, 업데이트, 삭제) 앨범을 사용 하는 방법을 알고 있는 컨트롤러 작업 모델 클래스 및 데이터베이스 액세스에는 Entity Framework 컨텍스트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-120">The new StoreManager controller class includes CRUD (create, read, update, delete) controller actions which know how to work with the Album model class and use our Entity Framework context for database access.</span></span>

## <a name="modifying-a-scaffolded-view"></a><span data-ttu-id="eb213-121">스 캐 폴드 된 뷰를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-121">Modifying a Scaffolded View</span></span>

<span data-ttu-id="eb213-122">이 코드에 우리 회사에 생성 되었습니다.이이 자습서 전체에서 작성 하는 것 처럼 표준 ASP.NET MVC 코드를 기억 하는 것이 반드시 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-122">It's important to remember that, while this code was generated for us, it's standard ASP.NET MVC code, just like we've been writing throughout this tutorial.</span></span> <span data-ttu-id="eb213-123">상용구 컨트롤러 코드를 작성 하 고 강력한 형식의 뷰를 수동으로 만드는 방법는 데 필요한 시간을 저장 하는 것 하지만 변화 하는 방법에 대 한 주석에서 심각한 경고를 사용 하 여 앞 나타날가 생성 된 코드의 종류를 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-123">It's intended to save you the time you'd spend on writing boilerplate controller code and creating the strongly typed views manually, but this isn't the kind of generated code you may have seen prefaced with dire warnings in comments about how you mustn't change the code.</span></span> <span data-ttu-id="eb213-124">코드 이며 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-124">This is your code, and you're expected to change it.</span></span>

<span data-ttu-id="eb213-125">따라서 StoreManager 인덱스 뷰에 빠른 편집을 사용 하 여 시작 해 보겠습니다 (/ Views/StoreManager/Index.cshtml).</span><span class="sxs-lookup"><span data-stu-id="eb213-125">So, let's start with a quick edit to the StoreManager Index view (/Views/StoreManager/Index.cshtml).</span></span> <span data-ttu-id="eb213-126">이 보기에는 편집을 사용 하 여 스토어에서 앨범을 나열 하는 테이블 표시 됩니다 / 세부 정보 / 링크를 삭제 하 고 앨범의 공용 속성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-126">This view will display a table which lists the Albums in our store with Edit / Details / Delete links, and includes the Album's public properties.</span></span> <span data-ttu-id="eb213-127">이 표시에서는 유용 하지 않으므로 AlbumArtUrl 필드를 제거 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-127">We'll remove the AlbumArtUrl field, as it's not very useful in this display.</span></span> <span data-ttu-id="eb213-128">&lt;테이블&gt; 섹션의 코드 보기를 제거 합니다 &lt;번째&gt; 및 &lt;td&gt; 아래 강조 표시 된 줄에 표시 된 대로 AlbumArtUrl 참조, 주변 요소:</span><span class="sxs-lookup"><span data-stu-id="eb213-128">In &lt;table&gt; section of the view code, remove the &lt;th&gt; and &lt;td&gt; elements surrounding AlbumArtUrl references, as indicated by the highlighted lines below:</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample1.cshtml)]

<span data-ttu-id="eb213-129">코드 수정 된 보기는 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-129">The modified view code will appear as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample2.cshtml)]

## <a name="a-first-look-at-the-store-manager"></a><span data-ttu-id="eb213-130">저장소 관리자 소개</span><span class="sxs-lookup"><span data-stu-id="eb213-130">A first look at the Store Manager</span></span>

<span data-ttu-id="eb213-131">이제 응용 프로그램을 실행 하 고 StoreManager은 /로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-131">Now run the application and browse to /StoreManager/.</span></span> <span data-ttu-id="eb213-132">방금 수정한, 세부 정보를 편집 및 삭제에 대 한 링크를 사용 하 여 저장소에는 앨범의 목록을 보여 주는 저장 Manager 인덱스 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-132">This displays the Store Manager Index we just modified, showing a list of the albums in the store with links to Edit, Details, and Delete.</span></span>

![](mvc-music-store-part-5/_static/image3.png)

<span data-ttu-id="eb213-133">편집 링크를 클릭 하면 앨범, Genre 및 아티스트에 대 한 드롭다운을 포함 하 여 필드를 사용 하 여 편집 양식을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-133">Clicking the Edit link displays an edit form with fields for the Album, including dropdowns for Genre and Artist.</span></span>

![](mvc-music-store-part-5/_static/image4.png)

<span data-ttu-id="eb213-134">아래쪽에서 "목록으로 돌아가기" 링크를 클릭 하 고 앨범에 대 한 세부 정보 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-134">Click the "Back to List" link at the bottom, then click on the Details link for an Album.</span></span> <span data-ttu-id="eb213-135">그러면 개별 앨범에 대 한 세부 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-135">This displays the detail information for an individual Album.</span></span>

![](mvc-music-store-part-5/_static/image5.png)

<span data-ttu-id="eb213-136">마찬가지로 목록 링크를 다시 클릭 삭제 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-136">Again, click the Back to List link, then click on a Delete link.</span></span> <span data-ttu-id="eb213-137">앨범 세부 정보를 표시 하 고 삭제 하려고 하는지 우리가 하는 경우 요청을 확인 대화 상자에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-137">This displays a confirmation dialog, showing the album details and asking if we're sure we want to delete it.</span></span>

![](mvc-music-store-part-5/_static/image6.png)

<span data-ttu-id="eb213-138">맨 아래에서 삭제 단추를 클릭 하면 앨범은 삭제 되며 삭제 앨범을 보여 주는 인덱스 페이지로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-138">Clicking the Delete button at the bottom will delete the album and return you to the Index page, which shows the album deleted.</span></span>

<span data-ttu-id="eb213-139">저장소 관리자를 사용 하 여 완료 되지 있지만 컨트롤러 및 보기 코드부터 CRUD 작업에 대 한 작업을 했습니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-139">We're not done with the Store Manager, but we have working controller and view code for the CRUD operations to start from.</span></span>

## <a name="looking-at-the-store-manager-controller-code"></a><span data-ttu-id="eb213-140">저장소 관리자 컨트롤러 코드를 살펴보면</span><span class="sxs-lookup"><span data-stu-id="eb213-140">Looking at the Store Manager Controller code</span></span>

<span data-ttu-id="eb213-141">저장소 관리자 컨트롤러가 적절 한 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-141">The Store Manager Controller contains a good amount of code.</span></span> <span data-ttu-id="eb213-142">살펴보겠습니다이 위쪽에서에서 아래쪽입니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-142">Let's go through this from top to bottom.</span></span> <span data-ttu-id="eb213-143">컨트롤러는 MVC 컨트롤러 뿐만 아니라 모델 네임 스페이스에 대 한 참조에 대 한 몇 가지 표준 네임 스페이스를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-143">The controller includes some standard namespaces for an MVC controller, as well as a reference to our Models namespace.</span></span> <span data-ttu-id="eb213-144">컨트롤러에 MusicStoreEntities, 데이터 액세스를 위해 각 컨트롤러 작업에서 사용의 전용 인스턴스</span><span class="sxs-lookup"><span data-stu-id="eb213-144">The controller has a private instance of MusicStoreEntities, used by each of the controller actions for data access.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample3.cs)]

### <a name="store-manager-index-and-details-actions"></a><span data-ttu-id="eb213-145">작업 관리자 인덱스 및 세부 정보를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-145">Store Manager Index and Details actions</span></span>

<span data-ttu-id="eb213-146">인덱스 보기에는 저장소 찾아보기 메서드에서 작업할 때 이전에 설명한 것 처럼 각 앨범 참조 장르 및 음악가 정보를 포함 한 앨범의 목록을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-146">The index view retrieves a list of Albums, including each album's referenced Genre and Artist information, as we previously saw when working on the Store Browse method.</span></span> <span data-ttu-id="eb213-147">인덱스 보기 컨트롤러는 효율적이 고 원래 요청에서이 정보에 대 한 쿼리 중인 하므로 각 앨범 장르 이름 및 Artist 이름을 표시할 수 있습니다이 연결된 된 개체에 대 한 참조를 다음 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-147">The Index view is following the references to the linked objects so that it can display each album's Genre name and Artist name, so the controller is being efficient and querying for this information in the original request.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample4.cs)]

<span data-ttu-id="eb213-148">StoreManager 컨트롤러의 세부 정보 컨트롤러 작업 정확히 동일 하 게 작동 우리가 작성 한 이전에-앨범에 대 한 쿼리 저장소 컨트롤러 세부 정보 작업 find () 메서드를 사용 하는 ID를 기준으로 다음이 보기로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-148">The StoreManager Controller's Details controller action works exactly the same as the Store Controller Details action we wrote previously - it queries for the Album by ID using the Find() method, then returns it to the view.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample5.cs)]

### <a name="the-create-action-methods"></a><span data-ttu-id="eb213-149">작업 메서드 만들기</span><span class="sxs-lookup"><span data-stu-id="eb213-149">The Create Action Methods</span></span>

<span data-ttu-id="eb213-150">만들기 작업 메서드는 양식 입력을 처리 하기 때문에 지금까지 살펴본 것과 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-150">The Create action methods are a little different from ones we've seen so far, because they handle form input.</span></span> <span data-ttu-id="eb213-151">사용자가 먼저 방문 /StoreManager/만들기/빈 폼을 표시 되며 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-151">When a user first visits /StoreManager/Create/ they will be shown an empty form.</span></span> <span data-ttu-id="eb213-152">이 HTML 페이지에 포함 됩니다는 &lt;폼&gt; 드롭다운 및 텍스트를 포함 하는 요소는 앨범의 세부 정보를 입력할 수 있는 요소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-152">This HTML page will contain a &lt;form&gt; element that contains dropdown and textbox input elements where they can enter the album's details.</span></span>

<span data-ttu-id="eb213-153">앨범 폼 값에 입력을 한 후에 데이터베이스 내에 저장할 응용 프로그램에 이러한 변경 내용을 다시 제출 하려면 "저장" 단추를 눌러 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-153">After the user fills in the Album form values, they can press the "Save" button to submit these changes back to our application to save within the database.</span></span> <span data-ttu-id="eb213-154">"저장" 단추를 누를 때 합니다 &lt;폼&gt; /StoreManager/만들기/URL로 다시 HTTP POST를 수행 하 고 제출 됩니다 합니다 &lt;폼&gt; HTTP POST의 일부로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-154">When the user presses the "save" button the &lt;form&gt; will perform an HTTP-POST back to the /StoreManager/Create/ URL and submit the &lt;form&gt; values as part of the HTTP-POST.</span></span>

<span data-ttu-id="eb213-155">ASP.NET MVC를 사용 하면 이러한 두 URL 호출 시나리오의 논리는 /StoreManager/Create 초기 HTTP GET 탐색을 처리 하는 StoreManagerController 클래스 – 내에서 두 개의 별도 "만들기" 작업 메서드를 구현 하도록 함으로써 쉽게 분할할 수 / URL 및 다른 전송된 된 변경 내용이의 HTTP POST를 처리 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-155">ASP.NET MVC allows us to easily split up the logic of these two URL invocation scenarios by enabling us to implement two separate "Create" action methods within our StoreManagerController class – one to handle the initial HTTP-GET browse to the /StoreManager/Create/ URL, and the other to handle the HTTP-POST of the submitted changes.</span></span>

### <a name="passing-information-to-a-view-using-viewbag"></a><span data-ttu-id="eb213-156">ViewBag을 사용 하 여 보기에 정보 전달</span><span class="sxs-lookup"><span data-stu-id="eb213-156">Passing information to a View using ViewBag</span></span>

<span data-ttu-id="eb213-157">이 자습서의 앞부분에서 ViewBag을 사용한 하지만 해에 대 한 별로 설명 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-157">We've used the ViewBag earlier in this tutorial, but haven't talked much about it.</span></span> <span data-ttu-id="eb213-158">ViewBag을 사용 하면 강력한 형식의 모델 개체를 사용 하지 않고 보기에 정보를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-158">The ViewBag allows us to pass information to the view without using a strongly typed model object.</span></span> <span data-ttu-id="eb213-159">이 경우이 편집 HTTP-GET 컨트롤러 작업 두 목록을 전달 장르 및 아티스트가를 폼에 드롭다운을 채우는 하며 작업을 수행 하는 가장 간단한 방법은 ViewBag 항목으로 반환 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-159">In this case, our Edit HTTP-GET controller action needs to pass both a list of Genres and Artists to the form to populate the dropdowns, and the simplest way to do that is to return them as ViewBag items.</span></span>

<span data-ttu-id="eb213-160">ViewBag는 동적 개체를 해당 속성을 정의 하는 코드를 작성 하지 않고도 ViewBag.Foo 또는 ViewBag.YourNameHere는 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-160">The ViewBag is a dynamic object, meaning that you can type ViewBag.Foo or ViewBag.YourNameHere without writing code to define those properties.</span></span> <span data-ttu-id="eb213-161">이 경우 컨트롤러 코드 사용 ViewBag.GenreId 및 ViewBag.ArtistId GenreId 및 ArtistId, 설정 수는 앨범 속성 폼을 제출 하는 드롭다운 값 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-161">In this case, the controller code uses ViewBag.GenreId and ViewBag.ArtistId so that the dropdown values submitted with the form will be GenreId and ArtistId, which are the Album properties they will be setting.</span></span>

<span data-ttu-id="eb213-162">이러한 드롭다운 값 위에 빌드되는 용도 위해 SelectList 개체를 사용 하 여 폼에 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-162">These dropdown values are returned to the form using the SelectList object, which is built just for that purpose.</span></span> <span data-ttu-id="eb213-163">이것은 다음과 같은 코드를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="eb213-163">This is done using code like this:</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample6.cs)]

<span data-ttu-id="eb213-164">작업 메서드 코드에서 보듯이이 개체를 만들 세 개의 매개 변수를 사용 중인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-164">As you can see from the action method code, three parameters are being used to create this object:</span></span>

- <span data-ttu-id="eb213-165">드롭다운을 표시할 수는 항목의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-165">The list of items the dropdown will be displaying.</span></span> <span data-ttu-id="eb213-166">Note는 문자열일 뿐 이것이-장르 목록을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-166">Note that this isn't just a string - we're passing a list of Genres.</span></span>
- <span data-ttu-id="eb213-167">다음 매개 변수는 SelectList에 전달 되 고 선택한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-167">The next parameter being passed to the SelectList is the Selected Value.</span></span> <span data-ttu-id="eb213-168">이 SelectList 미리 목록의 항목을 선택 하는 방법을 인식 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-168">This how the SelectList knows how to pre-select an item in the list.</span></span> <span data-ttu-id="eb213-169">이 매우 비슷하지만 편집 양식의 보면 이해 하기 쉬운 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-169">This will be easier to understand when we look at the Edit form, which is pretty similar.</span></span>
- <span data-ttu-id="eb213-170">마지막 매개 변수는 표시할 수 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-170">The final parameter is the property to be displayed.</span></span> <span data-ttu-id="eb213-171">이 경우 사용자에 게 표시 됩니다 Genre.Name 속성 임을 나타내는이 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-171">In this case, this is indicating that the Genre.Name property is what will be shown to the user.</span></span>

<span data-ttu-id="eb213-172">이 점을 염두에서 그런 다음 HTTP-GET 만들기 작업은 매우 간단-두 SelectLists ViewBag을에 추가 되 고 모델 개체가 없습니다 전달 됩니다 폼 (아직 생성 되지 않은) 때문.</span><span class="sxs-lookup"><span data-stu-id="eb213-172">With that in mind, then, the HTTP-GET Create action is pretty simple - two SelectLists are added to the ViewBag, and no model object is passed to the form (since it hasn't been created yet).</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample7.cs)]

### <a name="html-helpers-to-display-the-drop-downs-in-the-create-view"></a><span data-ttu-id="eb213-173">삭제 목록 보기 만들기 표시할 HTML 도우미</span><span class="sxs-lookup"><span data-stu-id="eb213-173">HTML Helpers to display the Drop Downs in the Create View</span></span>

<span data-ttu-id="eb213-174">드롭다운 값 목록 보기에 전달 하는 방법을 소개한에 있으므로 해당 값이 표시 되는 방식을 확인 하려면 뷰를 빠르게 확인을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-174">Since we've talked about how the drop down values are passed to the view, let's take a quick look at the view to see how those values are displayed.</span></span> <span data-ttu-id="eb213-175">코드 보기에서에서 (/ Views/StoreManager/Create.cshtml), 장르 드롭다운을 표시 하도록 다음 호출을 보면 다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-175">In the view code (/Views/StoreManager/Create.cshtml), you'll see the following call is made to display the Genre drop down.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample8.cshtml)]

<span data-ttu-id="eb213-176">이 HTML 도우미-일반적인 보기 작업을 수행 하는 유틸리티 메서드 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-176">This is known as an HTML Helper - a utility method which performs a common view task.</span></span> <span data-ttu-id="eb213-177">HTML 도우미 간결 하 고 읽을 수 있는 뷰 코드 유지에 매우 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-177">HTML Helpers are very useful in keeping our view code concise and readable.</span></span> <span data-ttu-id="eb213-178">Html.DropDownList 도우미 ASP.NET MVC에서 제공 하는 이지만 나중으로 코드 보기에서는 응용 프로그램에서 다시 사용에 대 한 고유한 도우미를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-178">The Html.DropDownList helper is provided by ASP.NET MVC, but as we'll see later it's possible to create our own helpers for view code we'll reuse in our application.</span></span>

<span data-ttu-id="eb213-179">위치를 표시할 목록 가져오기 및 값 (있는 경우)는 미리 선택 해야 합니다. 두 가지-누르세요 Html.DropDownList 호출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-179">The Html.DropDownList call just needs to be told two things - where to get the list to display, and what value (if any) should be pre-selected.</span></span> <span data-ttu-id="eb213-180">첫 번째 매개 변수, GenreId 모델 또는 ViewBag GenreId 라는 값을 검색할 DropDownList를 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-180">The first parameter, GenreId, tells the DropDownList to look for a value named GenreId in either the model or ViewBag.</span></span> <span data-ttu-id="eb213-181">두 번째 매개 변수는 표시할 값을 나타내는 드롭다운 목록에서에서 선택한 처음으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-181">The second parameter is used to indicate the value to show as initially selected in the drop down list.</span></span> <span data-ttu-id="eb213-182">이 폼 만들기 양식을 이므로 값이 없는 미리 선택 된 되도록 하 고 String.Empty 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-182">Since this form is a Create form, there's no value to be preselected and String.Empty is passed.</span></span>

### <a name="handling-the-posted-form-values"></a><span data-ttu-id="eb213-183">게시 된 양식 값 처리</span><span class="sxs-lookup"><span data-stu-id="eb213-183">Handling the Posted Form values</span></span>

<span data-ttu-id="eb213-184">전에 설명한 대로 각 폼에 연결 된 두 개의 작업 메서드 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-184">As we discussed before, there are two action methods associated with each form.</span></span> <span data-ttu-id="eb213-185">첫 번째는 HTTP GET 요청을 처리 하 고 폼을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-185">The first handles the HTTP-GET request and displays the form.</span></span> <span data-ttu-id="eb213-186">제출 된 양식 값을 포함 하는 HTTP POST 요청을 처리 하는 두 번째입니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-186">The second handles the HTTP-POST request, which contains the submitted form values.</span></span> <span data-ttu-id="eb213-187">컨트롤러 작업에 HTTP POST 요청에만 응답 해야 ASP.NET MVC에 지시 하는 [HttpPost] 특성을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-187">Notice that controller action has an [HttpPost] attribute, which tells ASP.NET MVC that it should only respond to HTTP-POST requests.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample9.cs)]

<span data-ttu-id="eb213-188">이 작업에는 네 가지 책임에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-188">This action has four responsibilities:</span></span>

- 1. <span data-ttu-id="eb213-189">폼 값 읽기</span><span class="sxs-lookup"><span data-stu-id="eb213-189">Read the form values</span></span>
- 2. <span data-ttu-id="eb213-190">폼 값 유효성 검사 규칙을 전달 하는 경우 확인</span><span class="sxs-lookup"><span data-stu-id="eb213-190">Check if the form values pass any validation rules</span></span>
- 3. <span data-ttu-id="eb213-191">폼 제출을 유효한 경우 데이터를 저장 하 고 업데이트 된 목록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-191">If the form submission is valid, save the data and display the updated list</span></span>
- 4. <span data-ttu-id="eb213-192">폼 제출을 올바르지 않으면 유효성 검사 오류가 있는 양식을 다시 표시</span><span class="sxs-lookup"><span data-stu-id="eb213-192">If the form submission is not valid, redisplay the form with validation errors</span></span>

#### <a name="reading-form-values-with-model-binding"></a><span data-ttu-id="eb213-193">모델 바인딩 사용 하 여 폼 값 읽기</span><span class="sxs-lookup"><span data-stu-id="eb213-193">Reading Form Values with Model Binding</span></span>

<span data-ttu-id="eb213-194">컨트롤러 작업 제목, 가격 및 AlbumArtUrl GenreId 및 ArtistId (드롭다운 목록에서 목록) 값 및 텍스트 상자 값을 포함 하는 폼 제출을 처리 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-194">The controller action is processing a form submission that includes values for GenreId and ArtistId (from the drop down list) and textbox values for Title, Price, and AlbumArtUrl.</span></span> <span data-ttu-id="eb213-195">폼 값에 직접 액세스할 수 있지만, ASP.NET MVC에 기본 제공 모델 바인딩 기능을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-195">While it's possible to directly access form values, a better approach is to use the Model Binding capabilities built into ASP.NET MVC.</span></span> <span data-ttu-id="eb213-196">매개 변수로 모델 형식을 사용 하는 컨트롤러 작업을 하는 경우 ASP.NET MVC 양식 입력 (뿐만 아니라 경로 및 쿼리 문자열 값)를 사용 하 여 해당 형식의 개체를 채우는 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-196">When a controller action takes a model type as a parameter, ASP.NET MVC will attempt to populate an object of that type using form inputs (as well as route and querystring values).</span></span> <span data-ttu-id="eb213-197">즉, 이름이 모델 개체의 속성을 예를 들어 일치 하는 값에 대 한 확인 하 여 새 앨범 개체 GenreId 값을 설정할 때 찾습니다 GenreId 이름의 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-197">It does this by looking for values whose names match properties of the model object, e.g. when setting the new Album object's GenreId value, it looks for an input with the name GenreId.</span></span> <span data-ttu-id="eb213-198">표준 메서드를 사용 하 여 ASP.NET MVC에서 뷰를 만들 때 폼 항상 렌더링 됩니다이 필드 이름과 일치 하도록 속성 이름 입력된 필드 이름으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-198">When you create views using the standard methods in ASP.NET MVC, the forms will always be rendered using property names as input field names, so this the field names will just match up.</span></span>

#### <a name="validating-the-model"></a><span data-ttu-id="eb213-199">모델 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="eb213-199">Validating the Model</span></span>

<span data-ttu-id="eb213-200">모델은 ModelState.IsValid에 대 한 간단한 호출을 사용 하 여 유효성이 검사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-200">The model is validated with a simple call to ModelState.IsValid.</span></span> <span data-ttu-id="eb213-201">앨범 클래스에 유효성 검사 규칙을 추가 하지 않은 것 아직이 검사 관련이 없는에 대해서는 조금-그럼 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-201">We haven't added any validation rules to our Album class yet - we'll do that in a bit - so right now this check doesn't have much to do.</span></span> <span data-ttu-id="eb213-202">중요 한 점은이 ModelStat.IsValid 확인 유효성 검사 규칙에 대 한 후속 변경 컨트롤러 작업 코드에 대 한 업데이트가 필요 하지 않습니다, 모델에 입력 유효성 검사 규칙에 따라 조정 됩니다는입니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-202">What's important is that this ModelStat.IsValid check will adapt to the validation rules we put on our model, so future changes to validation rules won't require any updates to the controller action code.</span></span>

#### <a name="saving-the-submitted-values"></a><span data-ttu-id="eb213-203">제출 된 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-203">Saving the submitted values</span></span>

<span data-ttu-id="eb213-204">폼 제출을 유효성 검사를 통과 인지 시간 값을 데이터베이스에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-204">If the form submission passes validation, it's time to save the values to the database.</span></span> <span data-ttu-id="eb213-205">앨범 컬렉션에 모델을 추가 하 고 SaveChanges를 호출 해 서 연결 해야 하는 Entity Framework를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="eb213-205">With Entity Framework, that just requires adding the model to the Albums collection and calling SaveChanges.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample10.cs)]

<span data-ttu-id="eb213-206">Entity Framework에는 값을 유지 하려면 적절 한 SQL 명령을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-206">Entity Framework generates the appropriate SQL commands to persist the value.</span></span> <span data-ttu-id="eb213-207">데이터를 저장 한 후 우리 컴퓨터에서는 업데이트를 알 수 있도록 앨범의 목록으로 다시 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-207">After saving the data, we redirect back to the list of Albums so we can see our update.</span></span> <span data-ttu-id="eb213-208">이렇게 RedirectToAction 표시 하고자 컨트롤러 작업의 이름으로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-208">This is done by returning RedirectToAction with the name of the controller action we want displayed.</span></span> <span data-ttu-id="eb213-209">이 경우에 경우 Index 메서드</span><span class="sxs-lookup"><span data-stu-id="eb213-209">In this case, that's the Index method.</span></span>

#### <a name="displaying-invalid-form-submissions-with-validation-errors"></a><span data-ttu-id="eb213-210">잘못 된 양식 제출 유효성 검사 오류를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-210">Displaying invalid form submissions with Validation Errors</span></span>

<span data-ttu-id="eb213-211">잘못 된 양식 입력의 경우 드롭다운 값 (HTTP GET 예:) ViewBag에 추가 됩니다 하 고 바인딩된 모델 값 표시에 대 한 보기로 다시 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-211">In the case of invalid form input, the dropdown values are added to the ViewBag (as in the HTTP-GET case) and the bound model values are passed back to the view for display.</span></span> <span data-ttu-id="eb213-212">유효성 검사 오류를 사용 하 여 자동으로 표시 되는 @Html.ValidationMessageFor HTML 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-212">Validation errors are automatically displayed using the @Html.ValidationMessageFor HTML Helper.</span></span>

#### <a name="testing-the-create-form"></a><span data-ttu-id="eb213-213">테스트 폼 만들기</span><span class="sxs-lookup"><span data-stu-id="eb213-213">Testing the Create Form</span></span>

<span data-ttu-id="eb213-214">이 out, 실행 및 테스트에 응용 프로그램 이동 /StoreManager/만들기 /-이 표시 됩니다 StoreController 만드는 HTTP GET 메서드에 의해 반환 된 빈 양식.</span><span class="sxs-lookup"><span data-stu-id="eb213-214">To test this out, run the application and browse to /StoreManager/Create/ - this will show you the blank form which was returned by the StoreController Create HTTP-GET method.</span></span>

<span data-ttu-id="eb213-215">일부 값 입력 하 고 양식을 전송할 만들기 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-215">Fill in some values and click the Create button to submit the form.</span></span>

![](mvc-music-store-part-5/_static/image7.png)

![](mvc-music-store-part-5/_static/image8.png)

### <a name="handling-edits"></a><span data-ttu-id="eb213-216">편집 내용을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-216">Handling Edits</span></span>

<span data-ttu-id="eb213-217">방금 살펴본 만들기 작업 방법에 편집 작업 쌍 (HTTP-GET 및 HTTP-POST) 매우 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-217">The Edit action pair (HTTP-GET and HTTP-POST) are very similar to the Create action methods we just looked at.</span></span> <span data-ttu-id="eb213-218">편집 시나리오에서는 기존 앨범, 편집 HTTP-GET 메서드 로드 앨범 "id" 매개 변수를 기반으로 사용 하므로 경로 통해 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-218">Since the edit scenario involves working with an existing album, the Edit HTTP-GET method loads the Album based on the "id" parameter, passed in via the route.</span></span> <span data-ttu-id="eb213-219">이 코드 앨범 AlbumId 검색 하는 것에 대 한 이전에 살펴보았습니다 세부 정보 컨트롤러 작업에서와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-219">This code for retrieving an album by AlbumId is the same as we've previously looked at in the Details controller action.</span></span> <span data-ttu-id="eb213-220">만들기와 마찬가지로 HTTP GET 메서드 값 드롭다운 ViewBag을 통해 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-220">As with the Create / HTTP-GET method, the drop down values are returned via the ViewBag.</span></span> <span data-ttu-id="eb213-221">이렇게 하면 돌아가려면 앨범은 모델 개체를 뷰 (Album 클래스에 강력한 형식인) ViewBag을 통해 추가 데이터 (예: 장르 목록)을 전달 하는 동안.</span><span class="sxs-lookup"><span data-stu-id="eb213-221">This allows us to return an Album as our model object to the view (which is strongly typed to the Album class) while passing additional data (e.g. a list of Genres) via the ViewBag.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample11.cs)]

<span data-ttu-id="eb213-222">HTTP POST 편집 작업을 만드는 HTTP POST 작업을 매우 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-222">The Edit HTTP-POST action is very similar to the Create HTTP-POST action.</span></span> <span data-ttu-id="eb213-223">유일한 차이점은는 db에 새 앨범이 추가 하는 대신 합니다. 앨범 컬렉션에서는 찾는 앨범의 현재 인스턴스 db를 사용 하 여 합니다. Entry(album) 및 해당 상태를 Modified로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-223">The only difference is that instead of adding a new album to the db.Albums collection, we're finding the current instance of the Album using db.Entry(album) and setting its state to Modified.</span></span> <span data-ttu-id="eb213-224">새로 만드는 대신 기존 앨범 수정 엔터티 프레임 워크에 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-224">This tells Entity Framework that we are modifying an existing album as opposed to creating a new one.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample12.cs)]

<span data-ttu-id="eb213-225">이 응용 프로그램을 실행 하 고 이동/StoreManger/앨범에 대 한 편집 링크를 클릭 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-225">We can test this out by running the application and browsing to /StoreManger/, then clicking the Edit link for an album.</span></span>

![](mvc-music-store-part-5/_static/image9.png)

<span data-ttu-id="eb213-226">HTTP GET 편집 메서드에 의해 표시 된 편집 양식을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-226">This displays the Edit form shown by the Edit HTTP-GET method.</span></span> <span data-ttu-id="eb213-227">일부 값 입력 하 고 저장 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-227">Fill in some values and click the Save button.</span></span>

![](mvc-music-store-part-5/_static/image10.png)

<span data-ttu-id="eb213-228">이 폼 게시, 값을 저장 및 앨범 목록에 표시 된 값이 업데이트 되었습니다 us를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-228">This posts the form, saves the values, and returns us to the Album list, showing that the values were updated.</span></span>

![](mvc-music-store-part-5/_static/image11.png)

### <a name="handling-deletion"></a><span data-ttu-id="eb213-229">삭제를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-229">Handling Deletion</span></span>

<span data-ttu-id="eb213-230">삭제는 편집 및 만들기, 확인을 표시 하려면 하나의 컨트롤러 작업과 폼 제출을 처리 하는 다른 컨트롤러 작업을 사용 하 여 동일한 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-230">Deletion follows the same pattern as Edit and Create, using one controller action to display the confirmation form, and another controller action to handle the form submission.</span></span>

<span data-ttu-id="eb213-231">컨트롤러 HTTP-GET 삭제 작업에서는 이전 저장소 관리자 세부 정보 컨트롤러 작업으로 정확히 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-231">The HTTP-GET Delete controller action is exactly the same as our previous Store Manager Details controller action.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample13.cs)]

<span data-ttu-id="eb213-232">삭제 뷰 콘텐츠 템플릿을 사용 하 여 앨범 형식에 강력한 형식이 있는 양식이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-232">We display a form that's strongly typed to an Album type, using the Delete view content template.</span></span>

![](mvc-music-store-part-5/_static/image12.png)

<span data-ttu-id="eb213-233">Delete 템플릿 모델에 대 한 모든 필드를 보여주지만, 해당 하위 상당히 간소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-233">The Delete template shows all the fields for the model, but we can simplify that down quite a bit.</span></span> <span data-ttu-id="eb213-234">다음과 /Views/StoreManager/Delete.cshtml에서 코드 보기를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-234">Change the view code in /Views/StoreManager/Delete.cshtml to the following.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample14.cshtml)]

<span data-ttu-id="eb213-235">간소화 된 삭제 확인 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-235">This displays a simplified Delete confirmation.</span></span>

![](mvc-music-store-part-5/_static/image13.png)

<span data-ttu-id="eb213-236">삭제 단추를 클릭 하면 폼이 DeleteConfirmed 동작을 실행 하는 서버에 다시 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-236">Clicking the Delete button causes the form to be posted back to the server, which executes the DeleteConfirmed action.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample15.cs)]

<span data-ttu-id="eb213-237">다음 작업을 수행 하는 우리의 HTTP-POST 삭제 컨트롤러 작업:</span><span class="sxs-lookup"><span data-stu-id="eb213-237">Our HTTP-POST Delete Controller Action takes the following actions:</span></span>

- 1. <span data-ttu-id="eb213-238">ID 별로 앨범 로드</span><span class="sxs-lookup"><span data-stu-id="eb213-238">Loads the Album by ID</span></span>
- 2. <span data-ttu-id="eb213-239">앨범을 삭제 하 고 변경 내용을 저장</span><span class="sxs-lookup"><span data-stu-id="eb213-239">Deletes it the album and save changes</span></span>
- 3. <span data-ttu-id="eb213-240">앨범이 목록에서 제거 되었는지 보여 주는 인덱스에 리디렉션</span><span class="sxs-lookup"><span data-stu-id="eb213-240">Redirects to the Index, showing that the Album was removed from the list</span></span>

<span data-ttu-id="eb213-241">이 테스트 하려면 응용 프로그램을 실행 하 고 /StoreManager 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-241">To test this, run the application and browse to /StoreManager.</span></span> <span data-ttu-id="eb213-242">목록에서 앨범을 선택 하 고 삭제 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-242">Select an album from the list and click the Delete link.</span></span>

![](mvc-music-store-part-5/_static/image14.png)

<span data-ttu-id="eb213-243">이 삭제 확인 화면이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-243">This displays our Delete confirmation screen.</span></span>

![](mvc-music-store-part-5/_static/image15.png)

<span data-ttu-id="eb213-244">삭제 단추를 클릭 하면 앨범을 제거 하 고 앨범 삭제 된 것을 보여 주는 Store Manager 인덱스 페이지로 돌아옵니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-244">Clicking the Delete button removes the album and returns us to the Store Manager Index page, which shows that the album has been deleted.</span></span>

![](mvc-music-store-part-5/_static/image16.png)

### <a name="using-a-custom-html-helper-to-truncate-text"></a><span data-ttu-id="eb213-245">사용자 지정 HTML 도우미를 사용 하 여 텍스트를 잘라내려면</span><span class="sxs-lookup"><span data-stu-id="eb213-245">Using a custom HTML Helper to truncate text</span></span>

<span data-ttu-id="eb213-246">저장소 관리자 인덱스 페이지를 사용 하 여 잠재적인 문제 하나 밀집 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-246">We've got one potential issue with our Store Manager Index page.</span></span> <span data-ttu-id="eb213-247">Artist 이름과 앨범 제목 속성 수 둘 다 충분히 길게 우리의 표 서식을 해제 throw 할 수는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-247">Our Album Title and Artist Name properties can both be long enough that they could throw off our table formatting.</span></span> <span data-ttu-id="eb213-248">이 보기에서 여러 속성을 쉽게 자를 해도 된다고 허락 하는 사용자 지정 HTML 도우미를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-248">We'll create a custom HTML Helper to allow us to easily truncate these and other properties in our Views.</span></span>

![](mvc-music-store-part-5/_static/image17.png)

<span data-ttu-id="eb213-249">Razor의 @helper 구문에 매우 쉽게 해 주었다 보기에서 사용할 사용자 고유의 도우미 함수를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-249">Razor's @helper syntax has made it pretty easy to create your own helper functions for use in your views.</span></span> <span data-ttu-id="eb213-250">/Views/StoreManager/Index.cshtml 뷰를 연 후 바로 다음 코드를 추가 합니다 @model 줄.</span><span class="sxs-lookup"><span data-stu-id="eb213-250">Open the /Views/StoreManager/Index.cshtml view and add the following code directly after the @model line.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample16.cshtml)]

<span data-ttu-id="eb213-251">이 도우미 메서드는 문자열과 수 있도록 최대 길이 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-251">This helper method takes a string and a maximum length to allow.</span></span> <span data-ttu-id="eb213-252">도우미 출력으로 제공 된 텍스트를 지정 된 길이 보다 짧은 경우-됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-252">If the text supplied is shorter than the length specified, the helper outputs it as-is.</span></span> <span data-ttu-id="eb213-253">긴 경우 다음 텍스트를 잘라냅니다 하 고 나머지 부분에서는 "..."를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-253">If it is longer, then it truncates the text and renders "…" for the remainder.</span></span>

<span data-ttu-id="eb213-254">이제 앨범 제목 및 Artist 이름 속성이 모두 25 자 미만 되는지 확인 하는 잘라내기 도우미를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-254">Now we can use our Truncate helper to ensure that both the Album Title and Artist Name properties are less than 25 characters.</span></span> <span data-ttu-id="eb213-255">이 새 자르기 도우미를 사용 하 여 전체적인 코드를 아래에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-255">The complete view code using our new Truncate helper appears below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample17.cshtml)]

<span data-ttu-id="eb213-256">이제 /StoreManager/ URL를 살펴봅니다 albums 및 제목 아래 최대 길이 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-256">Now when we browse the /StoreManager/ URL, the albums and titles are kept below our maximum lengths.</span></span>

![](mvc-music-store-part-5/_static/image18.png)

<span data-ttu-id="eb213-257">참고: 만들고 도우미를 사용 하 여 10to8의 간단한 경우가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb213-257">Note: This shows the simple case of creating and using a helper in one view.</span></span> <span data-ttu-id="eb213-258">사이트 전체에서 사용할 수 있는 도우미 만들기에 대 한 자세한 내용은 필자의 블로그 게시물을 참조 하세요. [http://bit.ly/mvc3-helper-options](http://bit.ly/mvc3-helper-options)</span><span class="sxs-lookup"><span data-stu-id="eb213-258">To learn more about creating helpers that you can use throughout your site, see my blog post: [http://bit.ly/mvc3-helper-options](http://bit.ly/mvc3-helper-options)</span></span>


> [!div class="step-by-step"]
> <span data-ttu-id="eb213-259">[이전](mvc-music-store-part-4.md)
> [다음](mvc-music-store-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="eb213-259">[Previous](mvc-music-store-part-4.md)
[Next](mvc-music-store-part-6.md)</span></span>
