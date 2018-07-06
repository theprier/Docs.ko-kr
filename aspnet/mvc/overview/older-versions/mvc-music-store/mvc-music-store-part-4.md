---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4
title: '4 부: 모델 및 데이터 액세스 | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 4 부에서는 모델 및 데이터 액세스에 설명 합니다.
ms.author: aspnetcontent
ms.date: 04/21/2011
ms.assetid: ab55ca81-ab9b-44a0-8700-dc6da2599335
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4
msc.type: authoredcontent
ms.openlocfilehash: 023350e882afe049ce3800921825b1b2bec8e415
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37818955"
---
<a name="part-4-models-and-data-access"></a><span data-ttu-id="4bc7d-104">4 부: 모델 및 데이터 액세스</span><span class="sxs-lookup"><span data-stu-id="4bc7d-104">Part 4: Models and Data Access</span></span>
====================
<span data-ttu-id="4bc7d-105">[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="4bc7d-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="4bc7d-106">MVC Music Store 자습서 응용 프로그램을 소개 하 고 웹 개발을 위한 ASP.NET MVC 및 Visual Studio를 사용 하는 방법을 단계별로 설명 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="4bc7d-107">MVC Music Store는 온라인 음악 앨범을 판매 하 고 기본 사이트 관리, 사용자 로그인 및 장바구니 기능을 구현 하는 간단한 샘플 저장소 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>
> 
> <span data-ttu-id="4bc7d-108">이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="4bc7d-109">4 부에서는 모델 및 데이터 액세스에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-109">Part 4 covers Models and Data Access.</span></span>


<span data-ttu-id="4bc7d-110">지금 우리 했습니다 되었습니다 전달 하기만 "더미 데이터"는 컨트롤러에서 우리의 보기 템플릿에 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-110">So far, we've just been passing "dummy data" from our Controllers to our View templates.</span></span> <span data-ttu-id="4bc7d-111">이제 실제 데이터베이스를 연결할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-111">Now we're ready to hook up a real database.</span></span> <span data-ttu-id="4bc7d-112">이 자습서는 데이터베이스 엔진으로 SQL Server Compact Edition (SQL CE 라고도 함)를 사용 하는 방법을 다루는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-112">In this tutorial we'll be covering how to use SQL Server Compact Edition (often called SQL CE) as our database engine.</span></span> <span data-ttu-id="4bc7d-113">SQL CE는 무료, 임베디드, 파일 기반 데이터베이스를 설치 및 구성으로 로컬 개발 매우 편리 하 게 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-113">SQL CE is a free, embedded, file based database that doesn't require any installation or configuration, which makes it really convenient for local development.</span></span>

## <a name="database-access-with-entity-framework-code-first"></a><span data-ttu-id="4bc7d-114">데이터베이스 액세스와 엔터티 프레임 워크 코드 중심</span><span class="sxs-lookup"><span data-stu-id="4bc7d-114">Database access with Entity Framework Code-First</span></span>

<span data-ttu-id="4bc7d-115">ASP.NET MVC 3 프로젝트를 쿼리하고 데이터베이스 업데이트에 포함 된 EF (Entity Framework) 지원을 사용 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-115">We'll use the Entity Framework (EF) support that is included in ASP.NET MVC 3 projects to query and update the database.</span></span> <span data-ttu-id="4bc7d-116">EF는 유연한 개체 관계형 매핑 (ORM) 데이터 개발자를 개체 지향 방식으로 데이터베이스에 저장 된 데이터를 쿼리하고 업데이트 된 API.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-116">EF is a flexible object relational mapping (ORM) data API that enables developers to query and update data stored in a database in an object-oriented way.</span></span>

<span data-ttu-id="4bc7d-117">Entity Framework 버전 4에는 호출 코드 중심 개발 패러다임을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-117">Entity Framework version 4 supports a development paradigm called code-first.</span></span> <span data-ttu-id="4bc7d-118">코드 중심 간단한 클래스 라고도 POCO ("plain old CLR object에서)를 작성 하 여 모델 개체를 만들 수 있습니다 및 데이터베이스 클래스에서 즉석에서 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-118">Code-first allows you to create model object by writing simple classes (also known as POCO from "plain-old" CLR objects), and can even create the database on the fly from your classes.</span></span>

### <a name="changes-to-our-model-classes"></a><span data-ttu-id="4bc7d-119">모델 클래스 변경</span><span class="sxs-lookup"><span data-stu-id="4bc7d-119">Changes to our Model Classes</span></span>

<span data-ttu-id="4bc7d-120">것을 활용 하는 Entity Framework에서 데이터베이스 만들기 기능이 자습서에서입니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-120">We will be leveraging the database creation feature in Entity Framework in this tutorial.</span></span> <span data-ttu-id="4bc7d-121">작업을 수행 하기 전에 만들어 보겠습니다 몇 가지만 변경에서 나중에 사용 하는 몇 가지 추가 모델 클래스.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-121">Before we do that, though, let's make a few minor changes to our model classes to add in some things we'll be using later on.</span></span>

#### <a name="adding-the-artist-model-classes"></a><span data-ttu-id="4bc7d-122">Artist 모델 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="4bc7d-122">Adding the Artist Model Classes</span></span>

<span data-ttu-id="4bc7d-123">우리의 앨범 아티스트를 설명 하는 간단한 모델 클래스를 추가 해 보겠습니다 아티스트를 사용 하 여 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-123">Our Albums will be associated with Artists, so we'll add a simple model class to describe an Artist.</span></span> <span data-ttu-id="4bc7d-124">아래 표시 된 코드를 사용 하 여 Artist.cs 모델 폴더에 새 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-124">Add a new class to the Models folder named Artist.cs using the code shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample1.cs)]

#### <a name="updating-our-model-classes"></a><span data-ttu-id="4bc7d-125">모델 클래스를 업데이트 하는 중</span><span class="sxs-lookup"><span data-stu-id="4bc7d-125">Updating our Model Classes</span></span>

<span data-ttu-id="4bc7d-126">아래와 같이 Album 클래스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-126">Update the Album class as shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample2.cs)]

<span data-ttu-id="4bc7d-127">다음으로, 장르 클래스에 다음 업데이트를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-127">Next, make the following updates to the Genre class.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample3.cs)]

### <a name="adding-the-appdata-folder"></a><span data-ttu-id="4bc7d-128">앱 추가\_데이터 폴더</span><span class="sxs-lookup"><span data-stu-id="4bc7d-128">Adding the App\_Data folder</span></span>

<span data-ttu-id="4bc7d-129">앱 추가\_데이터 디렉터리를 프로젝트는 SQL Server Express 데이터베이스 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-129">We'll add an App\_Data directory to our project to hold our SQL Server Express database files.</span></span> <span data-ttu-id="4bc7d-130">앱\_데이터가 데이터베이스 액세스에 대 한 올바른 보안 권한이 이미 있는 ASP.NET의 특수 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-130">App\_Data is a special directory in ASP.NET which already has the correct security access permissions for database access.</span></span> <span data-ttu-id="4bc7d-131">프로젝트 메뉴에서 선택한 ASP.NET 폴더 추가 앱\_데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-131">From the Project menu, select Add ASP.NET Folder, then App\_Data.</span></span>

![](mvc-music-store-part-4/_static/image1.png)

### <a name="creating-a-connection-string-in-the-webconfig-file"></a><span data-ttu-id="4bc7d-132">Web.config 파일에서 연결 문자열 만들기</span><span class="sxs-lookup"><span data-stu-id="4bc7d-132">Creating a Connection String in the web.config file</span></span>

<span data-ttu-id="4bc7d-133">Entity Framework에는 데이터베이스에 연결 하는 방법을 알 수 있도록 웹 사이트의 구성 파일에 몇 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-133">We will add a few lines to the website's configuration file so that Entity Framework knows how to connect to our database.</span></span> <span data-ttu-id="4bc7d-134">프로젝트의 루트에 있는 Web.config 파일을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-134">Double-click on the Web.config file located in the root of the project.</span></span>

![](mvc-music-store-part-4/_static/image2.png)

<span data-ttu-id="4bc7d-135">이 파일의 아래쪽으로 스크롤하여 추가 된 &lt;connectionStrings&gt; 아래와 같이 마지막 줄 바로 위에 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-135">Scroll to the bottom of this file and add a &lt;connectionStrings&gt; section directly above the last line, as shown below.</span></span>

[!code-xml[Main](mvc-music-store-part-4/samples/sample4.xml)]

### <a name="adding-a-context-class"></a><span data-ttu-id="4bc7d-136">컨텍스트 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="4bc7d-136">Adding a Context Class</span></span>

<span data-ttu-id="4bc7d-137">Models 폴더를 마우스 오른쪽 단추로 클릭 하 고 MusicStoreEntities.cs 라는 새 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-137">Right-click the Models folder and add a new class named MusicStoreEntities.cs.</span></span>

![](mvc-music-store-part-4/_static/image3.png)

<span data-ttu-id="4bc7d-138">이 클래스는 Entity Framework 데이터베이스 컨텍스트를 나타내는 및는 우리의 만들기를 처리, 읽기, 업데이트 및 삭제 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-138">This class will represent the Entity Framework database context, and will handle our create, read, update, and delete operations for us.</span></span> <span data-ttu-id="4bc7d-139">이 클래스에 대 한 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-139">The code for this class is shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample5.cs)]

<span data-ttu-id="4bc7d-140">이것이-없는 다른 구성, 특별 한 인터페이스, 등입니다. DbContext 기본 클래스를 확장 하 여 MusicStoreEntities 클래스는 우리 회사에 데이터베이스 작업을 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-140">That's it - there's no other configuration, special interfaces, etc. By extending the DbContext base class, our MusicStoreEntities class is able to handle our database operations for us.</span></span> <span data-ttu-id="4bc7d-141">이제 했으므로 후크 하는, 몇 가지 자세한 속성이 데이터베이스에 일부 추가 정보를 활용 하 여 모델 클래스를 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-141">Now that we've got that hooked up, let's add a few more properties to our model classes to take advantage of some of the additional information in our database.</span></span>

### <a name="adding-our-store-catalog-data"></a><span data-ttu-id="4bc7d-142">저장소 카탈로그 데이터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-142">Adding our store catalog data</span></span>

<span data-ttu-id="4bc7d-143">"초기값" 데이터는 새로 만든된 데이터베이스를 추가 하는 Entity Framework의 기능 활용을 걸립니다 했습니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-143">We will take advantage of a feature in Entity Framework which adds "seed" data to a newly created database.</span></span> <span data-ttu-id="4bc7d-144">이 저장소 카탈로그를 장르와 예술가, 앨범의 목록으로 미리 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-144">This will pre-populate our store catalog with a list of Genres, Artists, and Albums.</span></span> <span data-ttu-id="4bc7d-145">MvcMusicStore Assets.zip 다운로드-이 자습서의 앞부분에서 사용 하 여 사이트 디자인 파일에 포함 된-Code 라는 폴더에 있는이 시드 데이터를 사용 하 여 클래스 파일을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-145">The MvcMusicStore-Assets.zip download - which included our site design files used earlier in this tutorial - has a class file with this seed data, located in a folder named Code.</span></span>

<span data-ttu-id="4bc7d-146">코드 내에서 / Models 폴더 SampleData.cs 파일을 찾아 아래와 같이 프로젝트에서 Models 폴더에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-146">Within the Code / Models folder, locate the SampleData.cs file and drop it into the Models folder in our project, as shown below.</span></span>

![](mvc-music-store-part-4/_static/image4.png)

<span data-ttu-id="4bc7d-147">이제 해당 SampleData 클래스에 대 한 Entity Framework를 코드 한 줄을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-147">Now we need to add one line of code to tell Entity Framework about that SampleData class.</span></span> <span data-ttu-id="4bc7d-148">응용 프로그램 맨 위에 다음 줄을 추가 하 고 열어서 프로젝트의 루트에서 Global.asax 파일을 두 번 클릭\_메서드를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-148">Double-click on the Global.asax file in the root of the project to open it and add the following line to the top the Application\_Start method.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample6.cs)]

<span data-ttu-id="4bc7d-149">이 시점에서 프로젝트에 대 한 Entity Framework를 구성 하는 데 필요한 작업을 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-149">At this point, we've completed the work necessary to configure Entity Framework for our project.</span></span>

## <a name="querying-the-database"></a><span data-ttu-id="4bc7d-150">데이터베이스 쿼리</span><span class="sxs-lookup"><span data-stu-id="4bc7d-150">Querying the Database</span></span>

<span data-ttu-id="4bc7d-151">이제 "더미 데이터"를 사용 하는 대신 대신 호출 모든 해당 정보를 쿼리 하는 데이터베이스에는 StoreController를 업데이트 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-151">Now let's update our StoreController so that instead of using "dummy data" it instead calls into our database to query all of its information.</span></span> <span data-ttu-id="4bc7d-152">에 필드를 선언 하 여 먼저 합니다 **StoreController** storeDB 라는 MusicStoreEntities 클래스의 인스턴스를 보관할:</span><span class="sxs-lookup"><span data-stu-id="4bc7d-152">We'll start by declaring a field on the **StoreController** to hold an instance of the MusicStoreEntities class, named storeDB:</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample7.cs)]

### <a name="updating-the-store-index-to-query-the-database"></a><span data-ttu-id="4bc7d-153">데이터베이스에서 쿼리 저장소 인덱스를 업데이트 하는 중</span><span class="sxs-lookup"><span data-stu-id="4bc7d-153">Updating the Store Index to query the database</span></span>

<span data-ttu-id="4bc7d-154">MusicStoreEntities 클래스는 Entity Framework에서 유지 관리 하 고 데이터베이스의 각 테이블에 대해 컬렉션 속성을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-154">The MusicStoreEntities class is maintained by the Entity Framework and exposes a collection property for each table in our database.</span></span> <span data-ttu-id="4bc7d-155">데이터베이스에서 모든 장르를 검색 하 여 StoreController 인덱스 작업을 업데이트 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-155">Let's update our StoreController's Index action to retrieve all Genres in our database.</span></span> <span data-ttu-id="4bc7d-156">이전에 수행한 것이 문자열 데이터를 하드 코딩 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-156">Previously we did this by hard-coding string data.</span></span> <span data-ttu-id="4bc7d-157">이제 우리가 대신 방금 컨텍스트를 사용할 수는 Entity Framework Generes 컬렉션:</span><span class="sxs-lookup"><span data-stu-id="4bc7d-157">Now we can instead just use the Entity Framework context Generes collection:</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample8.cs)]

<span data-ttu-id="4bc7d-158">변경이 필요 하지 않은 데이터베이스에서 라이브 데이터 이제 반환 방금 전에-반환 하는 것 같은 StoreIndexViewModel 여전히 반환 되므로 보기 템플릿은에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-158">No changes need to happen to our View template since we're still returning the same StoreIndexViewModel we returned before - we're just returning live data from our database now.</span></span>

<span data-ttu-id="4bc7d-159">프로젝트를 다시 실행 하 고 "/ 저장" url, 데이터베이스에서 모든 장르 목록을 이제 표시 됩니다 했습니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-159">When we run the project again and visit the "/Store" URL, we'll now see a list of all Genres in our database:</span></span>

![](mvc-music-store-part-4/_static/image1.jpg)

### <a name="updating-store-browse-and-details-to-use-live-data"></a><span data-ttu-id="4bc7d-160">라이브 데이터를 사용 하려면 저장소 찾아보기 및 세부 정보를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-160">Updating Store Browse and Details to use live data</span></span>

<span data-ttu-id="4bc7d-161">사용 하 여/저장소/찾아보기? 장르 =*[일부 장르]* 작업 메서드를 검색 하는 장르 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-161">With the /Store/Browse?genre=*[some-genre]* action method, we're searching for a Genre by name.</span></span> <span data-ttu-id="4bc7d-162">두 항목이 동일한 장르 이름에 대 한 적이 없어야 했습니다 없으므로 사용할 수 있도록 하나의 결과 필요 합니다. LINQ에서 다음과 같은 적절 한 장르 개체에 대 한 쿼리 Single() 확장 (입력 하지이 아직):</span><span class="sxs-lookup"><span data-stu-id="4bc7d-162">We only expect one result, since we shouldn't ever have two entries for the same Genre name, and so we can use the .Single() extension in LINQ to query for the appropriate Genre object like this (don't type this yet):</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample9.cs)]

<span data-ttu-id="4bc7d-163">단일 메서드를 사용 한다고 단일 장르 개체 이름과 정의한 값과 일치 되도록 지정 하는 매개 변수로 람다 식입니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-163">The Single method takes a Lambda expression as a parameter, which specifies that we want a single Genre object such that its name matches the value we've defined.</span></span> <span data-ttu-id="4bc7d-164">위의 예에서 로드 하 고 단일 장르 개체 Disco를 일치 하는 이름 값을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-164">In the case above, we are loading a single Genre object with a Name value matching Disco.</span></span>

<span data-ttu-id="4bc7d-165">장르 개체를 검색할 때도 로드 하려고 하는 다른 관련된 엔터티를 나타낼 수 있도록 하는 Entity Framework 기능을 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-165">We'll take advantage of an Entity Framework feature that allows us to indicate other related entities we want loaded as well when the Genre object is retrieved.</span></span> <span data-ttu-id="4bc7d-166">이 기능은 쿼리 결과 셰이핑 하는 데 라고 하며 모든 필요한 정보를 검색 하려면 데이터베이스에 액세스 해야 하는 횟수를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-166">This feature is called Query Result Shaping, and enables us to reduce the number of times we need to access the database to retrieve all of the information we need.</span></span> <span data-ttu-id="4bc7d-167">관련된 앨범도 한다고 나타내려면 Genres.Include("Albums")에서 포함 하는 쿼리 업데이트에서는 장르를 검색에 대 한 앨범을 사전 인출 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-167">We want to pre-fetch the Albums for Genre we retrieve, so we'll update our query to include from Genres.Include("Albums") to indicate that we want related albums as well.</span></span> <span data-ttu-id="4bc7d-168">이 단일 데이터베이스 요청에는 장르 및 앨범 데이터를 검색 하는 것 이므로 더 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-168">This is more efficient, since it will retrieve both our Genre and Album data in a single database request.</span></span>

<span data-ttu-id="4bc7d-169">를 방해가 설명을 사용 하 여 다음과 같습니다.이 업데이트 된 찾아보기 컨트롤러 동작 표시 하는 방법</span><span class="sxs-lookup"><span data-stu-id="4bc7d-169">With the explanations out of the way, here's how our updated Browse controller action looks:</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample10.cs)]

<span data-ttu-id="4bc7d-170">이제 각 장르에서 사용할 수 있는 앨범을 표시 하려면 저장소 찾아보기 보기를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-170">We can now update the Store Browse View to display the albums which are available in each Genre.</span></span> <span data-ttu-id="4bc7d-171">템플릿 보기 (있는 /Views/Store/Browse.cshtml)을 열고 아래와 같이 앨범의 글머리 기호 목록을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-171">Open the view template (found in /Views/Store/Browse.cshtml) and add a bulleted list of Albums as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-4/samples/sample11.cshtml)]

<span data-ttu-id="4bc7d-172">응용 프로그램을 실행 하 고 이동/저장소/찾아보기? 장르 = 데이터베이스에는 선택한 장르에 모든 앨범 표시에서 결과 가져오는 이제는 Jazz 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-172">Running our application and browsing to /Store/Browse?genre=Jazz shows that our results are now being pulled from the database, displaying all albums in our selected Genre.</span></span>

![](mvc-music-store-part-4/_static/image2.jpg)

<span data-ttu-id="4bc7d-173">에서는에서는 동일 하 게 ID를 가진 매개 변수 값과 일치 하는 앨범을 로드 하는 데이터베이스 쿼리를 사용 하 여 더미 데이터를 바꾸고 /Store/세부 정보 / [id] URL을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-173">We'll make the same change to our /Store/Details/[id] URL, and replace our dummy data with a database query which loads an Album whose ID matches the parameter value.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample12.cs)]

<span data-ttu-id="4bc7d-174">응용 프로그램을 실행 하 고 /Store/Details/1 이동 결과 이제 데이터베이스에서 가져온 콘텐츠만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-174">Running our application and browsing to /Store/Details/1 shows that our results are now being pulled from the database.</span></span>

![](mvc-music-store-part-4/_static/image5.png)

<span data-ttu-id="4bc7d-175">저장소 세부 정보 페이지는 앨범 앨범 ID로 표시할를 설정 했으므로 업데이트 해 보겠습니다 합니다 **찾아보기** 자세히 보기를 연결 하는 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-175">Now that our Store Details page is set up to display an album by the Album ID, let's update the **Browse** view to link to the Details view.</span></span> <span data-ttu-id="4bc7d-176">연결할 저장소 인덱스에서 저장소 찾아보기 이전 섹션의 끝에 했던 것 처럼 정확히 Html.ActionLink에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-176">We will use Html.ActionLink, exactly as we did to link from Store Index to Store Browse at the end of the previous section.</span></span> <span data-ttu-id="4bc7d-177">브라우저 보기에 대 한 전체 소스 아래에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-177">The complete source for the Browse view appears below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-4/samples/sample13.cshtml)]

<span data-ttu-id="4bc7d-178">우리는 지금 사용할 수 있는 앨범을 나열 하는 장르 페이지에는 스토어 페이지에서 찾을 수 및 앨범을 클릭 하 여 해당 앨범에 대 한 자세한 내용은 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bc7d-178">We're now able to browse from our Store page to a Genre page, which lists the available albums, and by clicking on an album we can view details for that album.</span></span>

![](mvc-music-store-part-4/_static/image6.png)

> [!div class="step-by-step"]
> <span data-ttu-id="4bc7d-179">[이전](mvc-music-store-part-3.md)
> [다음](mvc-music-store-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="4bc7d-179">[Previous](mvc-music-store-part-3.md)
[Next](mvc-music-store-part-5.md)</span></span>
