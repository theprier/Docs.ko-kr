---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4
title: "4 부: 모델 및 데이터 액세스 | Microsoft Docs"
author: jongalloway
description: "이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다. 4 부에서는 모델 및 데이터 액세스에 설명 합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/21/2011
ms.topic: article
ms.assetid: ab55ca81-ab9b-44a0-8700-dc6da2599335
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4
msc.type: authoredcontent
ms.openlocfilehash: 727336344493b439130b2cf0ec6e7b5925dd5637
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="part-4-models-and-data-access"></a><span data-ttu-id="7ac4b-104">4 부: 모델 및 데이터 액세스</span><span class="sxs-lookup"><span data-stu-id="7ac4b-104">Part 4: Models and Data Access</span></span>
====================
<span data-ttu-id="7ac4b-105">으로 [Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="7ac4b-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="7ac4b-106">MVC Music Store는 소개 하 고 웹 개발에 대 한 ASP.NET MVC와 Visual Studio를 사용 하는 방법을 단계별로 설명 하는 자습서 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="7ac4b-107">MVC Music Store는 온라인 음악 앨범 판매 및 기본 사이트 관리, 사용자 로그인 및 장바구니 기능을 구현 하는 간단한 샘플 저장소 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>
> 
> <span data-ttu-id="7ac4b-108">이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="7ac4b-109">4 부에서는 모델 및 데이터 액세스에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-109">Part 4 covers Models and Data Access.</span></span>


<span data-ttu-id="7ac4b-110">"지금까지 म 했습니다 방금 되었습니다 더미 데이터" 우리의 컨트롤러에서를 전달 우리의 템플릿 보기.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-110">So far, we've just been passing "dummy data" from our Controllers to our View templates.</span></span> <span data-ttu-id="7ac4b-111">이제 실제 데이터베이스 연결 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-111">Now we're ready to hook up a real database.</span></span> <span data-ttu-id="7ac4b-112">이 자습서에서는 데이터베이스 엔진으로 SQL Server Compact Edition (SQL CE 라고도 함)를 사용 하는 방법을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-112">In this tutorial we'll be covering how to use SQL Server Compact Edition (often called SQL CE) as our database engine.</span></span> <span data-ttu-id="7ac4b-113">SQL CE는 무료 이며, 포함 된 파일 기반 데이터베이스를 설치 및 구성 하므로 불편 로컬 개발에 대 한 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-113">SQL CE is a free, embedded, file based database that doesn't require any installation or configuration, which makes it really convenient for local development.</span></span>

## <a name="database-access-with-entity-framework-code-first"></a><span data-ttu-id="7ac4b-114">데이터베이스 액세스와 Entity Framework 코드 중심</span><span class="sxs-lookup"><span data-stu-id="7ac4b-114">Database access with Entity Framework Code-First</span></span>

<span data-ttu-id="7ac4b-115">쿼리 및 데이터베이스를 업데이트 하도록 ASP.NET MVC 3 프로젝트에 포함 된 Entity Framework (EF) 지원을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-115">We'll use the Entity Framework (EF) support that is included in ASP.NET MVC 3 projects to query and update the database.</span></span> <span data-ttu-id="7ac4b-116">EF는 유연한 개체 관계형 매핑 (ORM) 데이터 개발자가 개체 지향 방식으로 데이터베이스에 저장 된 데이터를 쿼리하고 업데이트할 수 있는 API.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-116">EF is a flexible object relational mapping (ORM) data API that enables developers to query and update data stored in a database in an object-oriented way.</span></span>

<span data-ttu-id="7ac4b-117">Entity Framework 버전 4 라는 코드 중심 개발 패러다임을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-117">Entity Framework version 4 supports a development paradigm called code-first.</span></span> <span data-ttu-id="7ac4b-118">코드 중심 간단한 클래스 라고도 POCO ("old" CLR 개체에서)를 작성 하 여 모델 개체를 만들 수 있습니다 및를 사용 하 여 클래스에도 데이터베이스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-118">Code-first allows you to create model object by writing simple classes (also known as POCO from "plain-old" CLR objects), and can even create the database on the fly from your classes.</span></span>

### <a name="changes-to-our-model-classes"></a><span data-ttu-id="7ac4b-119">모델 클래스에 대 한 변경</span><span class="sxs-lookup"><span data-stu-id="7ac4b-119">Changes to our Model Classes</span></span>

<span data-ttu-id="7ac4b-120">Entity Framework에서 데이터베이스 만들기 기능이이 자습서에서는 활용 수 됩니다 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-120">We will be leveraging the database creation feature in Entity Framework in this tutorial.</span></span> <span data-ttu-id="7ac4b-121">그 전에 하지만 만들어 보겠습니다 몇 가지 사소한 변경 내용을 나중에 사용할 예정 일부의 원인에 추가할 모델 클래스.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-121">Before we do that, though, let's make a few minor changes to our model classes to add in some things we'll be using later on.</span></span>

#### <a name="adding-the-artist-model-classes"></a><span data-ttu-id="7ac4b-122">아티스트 모델 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-122">Adding the Artist Model Classes</span></span>

<span data-ttu-id="7ac4b-123">아티스트를 설명 하는 간단한 모델 클래스 추가 되므로 우리의 앨범 아티스트와 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-123">Our Albums will be associated with Artists, so we'll add a simple model class to describe an Artist.</span></span> <span data-ttu-id="7ac4b-124">아래 표시 된 코드를 사용 하 여 Artist.cs 라는 모델 폴더에 새 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-124">Add a new class to the Models folder named Artist.cs using the code shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample1.cs)]

#### <a name="updating-our-model-classes"></a><span data-ttu-id="7ac4b-125">모델 클래스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-125">Updating our Model Classes</span></span>

<span data-ttu-id="7ac4b-126">아래와 같이 앨범 클래스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-126">Update the Album class as shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample2.cs)]

<span data-ttu-id="7ac4b-127">다음으로 장르 클래스에 다음 업데이트를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-127">Next, make the following updates to the Genre class.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample3.cs)]

### <a name="adding-the-appdata-folder"></a><span data-ttu-id="7ac4b-128">앱 추가\_데이터 폴더</span><span class="sxs-lookup"><span data-stu-id="7ac4b-128">Adding the App\_Data folder</span></span>

<span data-ttu-id="7ac4b-129">앱 추가\_우리의 SQL Server Express 데이터베이스 파일을 저장 하는 프로젝트에 데이터 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-129">We'll add an App\_Data directory to our project to hold our SQL Server Express database files.</span></span> <span data-ttu-id="7ac4b-130">응용 프로그램\_데이터에 대 한 데이터베이스 액세스에 대 한 올바른 보안 액세스 권한을 이미 ASP.NET에서 특별 한 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-130">App\_Data is a special directory in ASP.NET which already has the correct security access permissions for database access.</span></span> <span data-ttu-id="7ac4b-131">프로젝트 메뉴에서 선택한 ASP.NET 폴더 추가 다음 앱\_데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-131">From the Project menu, select Add ASP.NET Folder, then App\_Data.</span></span>

![](mvc-music-store-part-4/_static/image1.png)

### <a name="creating-a-connection-string-in-the-webconfig-file"></a><span data-ttu-id="7ac4b-132">Web.config 파일에서 연결 문자열 만들기</span><span class="sxs-lookup"><span data-stu-id="7ac4b-132">Creating a Connection String in the web.config file</span></span>

<span data-ttu-id="7ac4b-133">Entity Framework 데이터베이스에 연결 하는 방법을 알 수 있도록 웹 사이트의 구성 파일에 몇 줄만 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-133">We will add a few lines to the website's configuration file so that Entity Framework knows how to connect to our database.</span></span> <span data-ttu-id="7ac4b-134">프로젝트의 루트에 있는 Web.config 파일을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-134">Double-click on the Web.config file located in the root of the project.</span></span>

![](mvc-music-store-part-4/_static/image2.png)

<span data-ttu-id="7ac4b-135">이 파일의 아래쪽으로 스크롤하여 추가 &lt;connectionStrings&gt; 다음과 같이 마지막 줄 바로 위에 섹션.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-135">Scroll to the bottom of this file and add a &lt;connectionStrings&gt; section directly above the last line, as shown below.</span></span>

[!code-xml[Main](mvc-music-store-part-4/samples/sample4.xml)]

### <a name="adding-a-context-class"></a><span data-ttu-id="7ac4b-136">컨텍스트 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-136">Adding a Context Class</span></span>

<span data-ttu-id="7ac4b-137">모델 폴더를 마우스 오른쪽 단추로 클릭 하 고 MusicStoreEntities.cs 라는 새 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-137">Right-click the Models folder and add a new class named MusicStoreEntities.cs.</span></span>

![](mvc-music-store-part-4/_static/image3.png)

<span data-ttu-id="7ac4b-138">이 클래스는 Entity Framework 데이터베이스 컨텍스트를 나타내는 및 됩니다 우리의 만들기 처리, 읽기, 업데이트, 및 삭제 작업을 수행해 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-138">This class will represent the Entity Framework database context, and will handle our create, read, update, and delete operations for us.</span></span> <span data-ttu-id="7ac4b-139">이 클래스에 대 한 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-139">The code for this class is shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample5.cs)]

<span data-ttu-id="7ac4b-140">이제 끝났습니다-없는 다른 구성, 특수 인터페이스 등이 있습니다. DbContext 기본 클래스를 확장 하 여 MusicStoreEntities 클래스가 우리의 데이터베이스 작업을 수행해 줍니다를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-140">That's it - there's no other configuration, special interfaces, etc. By extending the DbContext base class, our MusicStoreEntities class is able to handle our database operations for us.</span></span> <span data-ttu-id="7ac4b-141">연결 하는 작업을 두었습니다 이제 몇 가지 더 많은 속성 데이터베이스에는 추가 정보 중 일부를 활용 하려면 모델 클래스를 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-141">Now that we've got that hooked up, let's add a few more properties to our model classes to take advantage of some of the additional information in our database.</span></span>

### <a name="adding-our-store-catalog-data"></a><span data-ttu-id="7ac4b-142">스토어 카탈로그 데이터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-142">Adding our store catalog data</span></span>

<span data-ttu-id="7ac4b-143">"Seed" 데이터는 새로 만든된 데이터베이스를 추가 하는 Entity Framework에는 기능을 해당 메뉴로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-143">We will take advantage of a feature in Entity Framework which adds "seed" data to a newly created database.</span></span> <span data-ttu-id="7ac4b-144">이 스토어 카탈로그를 장르, 아티스트 및 앨범 목록이 미리 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-144">This will pre-populate our store catalog with a list of Genres, Artists, and Albums.</span></span> <span data-ttu-id="7ac4b-145">이 자습서의 앞부분에서 사용 되는 사이트 디자인 파일-포함 하는 MvcMusicStore Assets.zip 다운로드가 초기값 데이터로 명명 된 코드 폴더에 있는 클래스 파일을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-145">The MvcMusicStore-Assets.zip download - which included our site design files used earlier in this tutorial - has a class file with this seed data, located in a folder named Code.</span></span>

<span data-ttu-id="7ac4b-146">코드 내에서 / Models 폴더 SampleData.cs 파일을 찾은 다음 아래와 같이 취급 프로젝트에서 Models 폴더에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-146">Within the Code / Models folder, locate the SampleData.cs file and drop it into the Models folder in our project, as shown below.</span></span>

![](mvc-music-store-part-4/_static/image4.png)

<span data-ttu-id="7ac4b-147">이제 Entity Framework에 해당 SampleData 클래스에 대 한 정보를 코드 한 줄을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-147">Now we need to add one line of code to tell Entity Framework about that SampleData class.</span></span> <span data-ttu-id="7ac4b-148">열고 응용 프로그램 맨 위에 다음 줄을 추가 하는 프로젝트의 루트에 Global.asax 파일을 두 번 클릭\_메서드를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-148">Double-click on the Global.asax file in the root of the project to open it and add the following line to the top the Application\_Start method.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample6.cs)]

<span data-ttu-id="7ac4b-149">이 시점에서 프로젝트에 대 한 Entity Framework를 구성 하는 데 필요한 작업을 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-149">At this point, we've completed the work necessary to configure Entity Framework for our project.</span></span>

## <a name="querying-the-database"></a><span data-ttu-id="7ac4b-150">데이터베이스 쿼리</span><span class="sxs-lookup"><span data-stu-id="7ac4b-150">Querying the Database</span></span>

<span data-ttu-id="7ac4b-151">이제 "데이터는 dummy"를 사용 하는 대신 대신 호출 데이터베이스로 넘어가면 모든 정보를 쿼리할 수 있도록 보겠습니다 우리의 StoreController를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-151">Now let's update our StoreController so that instead of using "dummy data" it instead calls into our database to query all of its information.</span></span> <span data-ttu-id="7ac4b-152">에 필드를 선언 하 여 시작 합니다는 **StoreController** storeDB 라는 MusicStoreEntities 클래스의 인스턴스를 포함 하려면:</span><span class="sxs-lookup"><span data-stu-id="7ac4b-152">We'll start by declaring a field on the **StoreController** to hold an instance of the MusicStoreEntities class, named storeDB:</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample7.cs)]

### <a name="updating-the-store-index-to-query-the-database"></a><span data-ttu-id="7ac4b-153">데이터베이스에서 쿼리 저장소 인덱스 업데이트</span><span class="sxs-lookup"><span data-stu-id="7ac4b-153">Updating the Store Index to query the database</span></span>

<span data-ttu-id="7ac4b-154">MusicStoreEntities 클래스는 Entity Framework에 의해 유지 관리 및 데이터베이스의 각 테이블에 대 한 컬렉션 속성을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-154">The MusicStoreEntities class is maintained by the Entity Framework and exposes a collection property for each table in our database.</span></span> <span data-ttu-id="7ac4b-155">데이터베이스에 모든 장르 검색할 우리의 StoreController 인덱스 동작을 업데이트 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-155">Let's update our StoreController's Index action to retrieve all Genres in our database.</span></span> <span data-ttu-id="7ac4b-156">이전에 수행한 것이 문자열 데이터를 하드 코딩 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-156">Previously we did this by hard-coding string data.</span></span> <span data-ttu-id="7ac4b-157">이제 우리 대신 방금 context를 사용할 수 Entity Framework Generes 컬렉션:</span><span class="sxs-lookup"><span data-stu-id="7ac4b-157">Now we can instead just use the Entity Framework context Generes collection:</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample8.cs)]

<span data-ttu-id="7ac4b-158">변경 없이 이러한 문제가 발생할 우리의 보기 템플릿에 म 반환 전에-우리는 반환 라이브 데이터 데이터베이스에서 이제 동일한 StoreIndexViewModel 여전히 반환 하는 것 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-158">No changes need to happen to our View template since we're still returning the same StoreIndexViewModel we returned before - we're just returning live data from our database now.</span></span>

<span data-ttu-id="7ac4b-159">프로젝트를 다시 실행 하 고 "/ 저장" URL을 방문 하십시오에서는 모든 장르 목록 데이터베이스에으로 이제 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-159">When we run the project again and visit the "/Store" URL, we'll now see a list of all Genres in our database:</span></span>

![](mvc-music-store-part-4/_static/image1.jpg)

### <a name="updating-store-browse-and-details-to-use-live-data"></a><span data-ttu-id="7ac4b-160">라이브 데이터를 사용 하도록 스토어 찾아보기 및 세부 정보 업데이트</span><span class="sxs-lookup"><span data-stu-id="7ac4b-160">Updating Store Browse and Details to use live data</span></span>

<span data-ttu-id="7ac4b-161">/ 저장소/찾아보기로? 장르 =*[일부 장르]* 동작 메서드에 우리는 장르에 대 한 이름을 기준으로 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-161">With the /Store/Browse?genre=*[some-genre]* action method, we're searching for a Genre by name.</span></span> <span data-ttu-id="7ac4b-162">두 항목이 동일한 장르 이름에 대 한 적이 서는 안 있으므로 및 사용할 수 있도록 한 결과 라고만 생각는 합니다. 다음과 같이 적절 한 장르 개체에 대 한 쿼리를 LINQ에서 Single() 확장 (입력 하지 않은이 아직):</span><span class="sxs-lookup"><span data-stu-id="7ac4b-162">We only expect one result, since we shouldn't ever have two entries for the same Genre name, and so we can use the .Single() extension in LINQ to query for the appropriate Genre object like this (don't type this yet):</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample9.cs)]

<span data-ttu-id="7ac4b-163">단일 메서드 한다고 단일 장르 개체 이름이 정의 된 값과 일치 되도록 지정 하는 매개 변수로 람다 식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-163">The Single method takes a Lambda expression as a parameter, which specifies that we want a single Genre object such that its name matches the value we've defined.</span></span> <span data-ttu-id="7ac4b-164">앞의 경우에서 Disco를 일치 하는 이름 값이 있는 단일 장르 개체를 로드 하는 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-164">In the case above, we are loading a single Genre object with a Name value matching Disco.</span></span>

<span data-ttu-id="7ac4b-165">장르 개체를 검색할 때 로드도 원하는 다른 관련된 엔터티를 나타낼 수 있도록 하는 Entity Framework 기능을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-165">We'll take advantage of an Entity Framework feature that allows us to indicate other related entities we want loaded as well when the Genre object is retrieved.</span></span> <span data-ttu-id="7ac4b-166">이 기능은 쿼리 결과 셰이핑 라고 하 고 모든 필요한 정보를 검색 하는 데이터베이스에 액세스 해야 하는 횟수를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-166">This feature is called Query Result Shaping, and enables us to reduce the number of times we need to access the database to retrieve all of the information we need.</span></span> <span data-ttu-id="7ac4b-167">하므로 쿼리를 나타내는 관련된 앨범도 한다고 Genres.Include("Albums")에서 포함할를 업데이트 하는 장르, 검색에 대 한 앨범을 사전 인출 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-167">We want to pre-fetch the Albums for Genre we retrieve, so we'll update our query to include from Genres.Include("Albums") to indicate that we want related albums as well.</span></span> <span data-ttu-id="7ac4b-168">단일 데이터베이스 요청에서이 Genre 및 앨범 데이터를 검색 하므로 보다 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-168">This is more efficient, since it will retrieve both our Genre and Album data in a single database request.</span></span>

<span data-ttu-id="7ac4b-169">방해가 설명 같습니다 우리의 업데이트 된 찾아보기 컨트롤러 동작 표시 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-169">With the explanations out of the way, here's how our updated Browse controller action looks:</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample10.cs)]

<span data-ttu-id="7ac4b-170">이제 각 장르의 사용할 수 있는 앨범을 표시 하려면 저장소 찾아보기 보기를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-170">We can now update the Store Browse View to display the albums which are available in each Genre.</span></span> <span data-ttu-id="7ac4b-171">보기 템플릿 (에 /Views/Store/Browse.cshtml)를 열고 아래와 같이 글머리 기호 목록이 앨범을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-171">Open the view template (found in /Views/Store/Browse.cshtml) and add a bulleted list of Albums as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-4/samples/sample11.cshtml)]

<span data-ttu-id="7ac4b-172">응용 프로그램을 실행 하 고 탐색/저장소/찾아보기 하? 장르 = 우리의 선택한 장르에 모든 앨범 표시 하는 데이터베이스에서 결과 가져오는 이제 Jazz 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-172">Running our application and browsing to /Store/Browse?genre=Jazz shows that our results are now being pulled from the database, displaying all albums in our selected Genre.</span></span>

![](mvc-music-store-part-4/_static/image2.jpg)

<span data-ttu-id="7ac4b-173">म 우리의 /Store/세부 정보 / [id] URL로 변경 하 고이 매개 변수 값과 일치 하는 ID를 가진 앨범을 로드 합니다. 데이터베이스 쿼리를 더미 데이터 바꿉니다 동일 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-173">We'll make the same change to our /Store/Details/[id] URL, and replace our dummy data with a database query which loads an Album whose ID matches the parameter value.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample12.cs)]

<span data-ttu-id="7ac4b-174">결과 이제 데이터베이스에서 찾아볼 되 고 응용 프로그램을 실행 하 고 /Store/Details/1을 찾아를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-174">Running our application and browsing to /Store/Details/1 shows that our results are now being pulled from the database.</span></span>

![](mvc-music-store-part-4/_static/image5.png)

<span data-ttu-id="7ac4b-175">이제 업데이트 앨범 앨범 ID로 표시 하는 저장소 세부 정보 페이지를 설정 하는 **찾아보기** 자세히 보기에 연결 하는 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-175">Now that our Store Details page is set up to display an album by the Album ID, let's update the **Browse** view to link to the Details view.</span></span> <span data-ttu-id="7ac4b-176">이전 섹션의 끝에 저장소 인덱스를 저장소 찾아보기 연결 했던 것 처럼 정확 하 게 Html.ActionLink를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-176">We will use Html.ActionLink, exactly as we did to link from Store Index to Store Browse at the end of the previous section.</span></span> <span data-ttu-id="7ac4b-177">브라우저 보기에 대 한 전체 소스 아래에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-177">The complete source for the Browse view appears below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-4/samples/sample13.cshtml)]

<span data-ttu-id="7ac4b-178">이 스토어 페이지에서 사용할 수 있는 앨범을 나열 하는 장르 페이지로 탐색할 수 이제 및 앨범을 클릭 하 여 해당 앨범에 대 한 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ac4b-178">We're now able to browse from our Store page to a Genre page, which lists the available albums, and by clicking on an album we can view details for that album.</span></span>

![](mvc-music-store-part-4/_static/image6.png)

>[!div class="step-by-step"]
<span data-ttu-id="7ac4b-179">[이전](mvc-music-store-part-3.md)
[다음](mvc-music-store-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="7ac4b-179">[Previous](mvc-music-store-part-3.md)
[Next](mvc-music-store-part-5.md)</span></span>
