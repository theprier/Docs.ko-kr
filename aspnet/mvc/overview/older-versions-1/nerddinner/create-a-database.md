---
uid: mvc/overview/older-versions-1/nerddinner/create-a-database
title: 데이터베이스 만들기 | Microsoft Docs
author: microsoft
description: 2 단계를 모두 dinner 보유 하는 데이터베이스를 만들고 RSVP 업그레이드 되었으며 수정 응용 프로그램에 대 한 데이터 단계를 보여 줍니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: 983f3ffa-08b8-4868-b8c9-aa34593fc683
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-database
msc.type: authoredcontent
ms.openlocfilehash: ba28d671bf13ec54b83b876462e2c23f90310037
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30869142"
---
<a name="create-a-database"></a><span data-ttu-id="0f437-103">데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="0f437-103">Create a Database</span></span>
====================
<span data-ttu-id="0f437-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="0f437-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="0f437-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="0f437-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="0f437-106">이 무료의 2 단계 ["업그레이드 되었으며 수정" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 하는 워크 쓰루는 작고 빌드만 ASP.NET MVC 1을 사용 하 여 웹 응용 프로그램을 완료 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-106">This is step 2 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="0f437-107">2 단계를 모두 dinner 보유 하는 데이터베이스를 만들고 RSVP 업그레이드 되었으며 수정 응용 프로그램에 대 한 데이터 단계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-107">Step 2 shows the steps to create the database holding all of the dinner and RSVP data for our NerdDinner application.</span></span>
> 
> <span data-ttu-id="0f437-108">ASP.NET MVC 3을 사용 하는 경우 수행한 것이 좋습니다는 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-step-2-creating-the-database"></a><span data-ttu-id="0f437-109">업그레이드 되었으며 수정 2 단계: 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="0f437-109">NerdDinner Step 2: Creating the Database</span></span>

<span data-ttu-id="0f437-110">업그레이드 되었으며 수정 응용 프로그램에 대 한 모든 Dinner 및 RSVP 데이터를 저장 하는 데이터베이스를 사용해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-110">We'll be using a database to store all of the Dinner and RSVP data for our NerdDinner application.</span></span>

<span data-ttu-id="0f437-111">무료 SQL Server Express edition을 사용 하 여 데이터베이스를 만드는 다음 단계 표시 (v 2의를 사용 하 여 쉽게 설치할 수 있는 [Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)).</span><span class="sxs-lookup"><span data-stu-id="0f437-111">The steps below show creating the database using the free SQL Server Express edition (which you can easily install using V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)).</span></span> <span data-ttu-id="0f437-112">SQL Server Express 및 SQL Server 전체와 작동 하는 모든 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-112">All of the code we'll write works with both SQL Server Express and the full SQL Server.</span></span>

### <a name="creating-a-new-sql-server-express-database"></a><span data-ttu-id="0f437-113">새 SQL Server Express 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="0f437-113">Creating a new SQL Server Express database</span></span>

<span data-ttu-id="0f437-114">이 웹 프로젝트를 마우스 오른쪽 단추로 클릭 하 여 시작 알아보고 선택 하겠습니다는 **추가-&gt;새 항목** 메뉴 명령:</span><span class="sxs-lookup"><span data-stu-id="0f437-114">We'll begin by right-clicking on our web project, and then select the **Add-&gt;New Item** menu command:</span></span>

![](create-a-database/_static/image1.png)

<span data-ttu-id="0f437-115">이 Visual Studio의 "새 항목 추가" 대화 상자를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-115">This will bring up Visual Studio's "Add New Item" dialog.</span></span> <span data-ttu-id="0f437-116">"데이터" 범주별으로 필터링 알아보고 "SQL Server 데이터베이스" 항목 템플릿을 선택 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-116">We'll filter by the "Data" category and select the "SQL Server Database" item template:</span></span>

![](create-a-database/_static/image2.png)

<span data-ttu-id="0f437-117">여기서 "NerdDinner.mdf" 만들고 적중 확인 하려는 SQL Server Express 데이터베이스를 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-117">We'll name the SQL Server Express database we want to create "NerdDinner.mdf" and hit ok.</span></span> <span data-ttu-id="0f437-118">Visual Studio는 다음 문의 우리의 \App에이 파일에 추가 되기를 원하는\_데이터 디렉터리 (디렉터리가 이미 있는 모두 읽기 설정 및 보안 Acl 쓰기):</span><span class="sxs-lookup"><span data-stu-id="0f437-118">Visual Studio will then ask us if we want to add this file to our \App\_Data directory (which is a directory already setup with both read and write security ACLs):</span></span>

![](create-a-database/_static/image3.png)

<span data-ttu-id="0f437-119">"Yes"를 클릭 합니다 및 우리의 새 데이터베이스가 생성 되 고 우리의 솔루션 탐색기에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-119">We'll click "Yes" and our new database will be created and added to our Solution Explorer:</span></span>

![](create-a-database/_static/image4.png)

### <a name="creating-tables-within-our-database"></a><span data-ttu-id="0f437-120">데이터베이스 내에서 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="0f437-120">Creating Tables within our Database</span></span>

<span data-ttu-id="0f437-121">비어 있는 새 데이터베이스를 했습니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-121">We now have a new empty database.</span></span> <span data-ttu-id="0f437-122">일부 테이블을 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-122">Let's add some tables to it.</span></span>

<span data-ttu-id="0f437-123">이렇게 하려면 데이터베이스 및 서버를 관리할 수 있게 하는 Visual Studio 내에서 "서버 탐색기" 탭 창으로 이동 됩니다 했습니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-123">To do this we'll navigate to the "Server Explorer" tab window within Visual Studio, which enables us to manage databases and servers.</span></span> <span data-ttu-id="0f437-124">SQL Server Express 데이터베이스는 \App에 저장 된\_응용 프로그램 데이터 폴더 서버 탐색기 내 표시 자동으로 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-124">SQL Server Express databases stored in the \App\_Data folder of our application will automatically show up within the Server Explorer.</span></span> <span data-ttu-id="0f437-125">추가 SQL Server 데이터베이스 (로컬 및 원격 모두)도 목록에 추가 하려면 "서버 탐색기" 창 맨 위에 있는 "데이터베이스에 연결" 아이콘을 사용 필요에 따라 했습니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-125">We can optionally use the "Connect to Database" icon on the top of the "Server Explorer" window to add additional SQL Server databases (both local and remote) to the list as well:</span></span>

![](create-a-database/_static/image5.png)

<span data-ttu-id="0f437-126">두 테이블을 저장 하 여 Dinners 고 다른 RSVP 통용 추적 하 여 업그레이드 되었으며 수정 데이터베이스에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-126">We will add two tables to our NerdDinner database – one to store our Dinners, and the other to track RSVP acceptances to them.</span></span> <span data-ttu-id="0f437-127">데이터베이스 내에서 "Tables" 폴더를 마우스 오른쪽 단추로 클릭 하 고 "새 테이블 추가" 메뉴 명령을 선택 하 여 새 테이블을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-127">We can create new tables by right-clicking on the "Tables" folder within our database and choosing the "Add New Table" menu command:</span></span>

![](create-a-database/_static/image6.png)

<span data-ttu-id="0f437-128">예제 테이블의 스키마를 구성할 수 있도록 하는 테이블 디자이너를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-128">This will open up a table designer that allows us to configure the schema of our table.</span></span> <span data-ttu-id="0f437-129">"Dinners" 테이블에 대 한 데이터의 10 개의 열을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-129">For our "Dinners" table we will add 10 columns of data:</span></span>

![](create-a-database/_static/image7.png)

<span data-ttu-id="0f437-130">"DinnerID" 열을 테이블에 대 한 고유 기본 키를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-130">We want the "DinnerID" column to be a unique primary key for the table.</span></span> <span data-ttu-id="0f437-131">"DinnerID" 열을 마우스 오른쪽 단추로 클릭 하 고 "기본 키 설정" 메뉴 항목을 선택 하 여이 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-131">We can configure this by right-clicking on the "DinnerID" column and choosing the "Set Primary Key" menu item:</span></span>

![](create-a-database/_static/image8.png)

<span data-ttu-id="0f437-132">에 이외에 DinnerID 기본 키도 원하는 값을 가진 새 데이터 행을 테이블에 추가 되는 자동 증가 "id" 열으로 구성 (첫 번째 삽입 된 Dinner 행 1 DinnerID 갖습니다 합니다. 즉, 두 번째 삽입 된 행 DinnerID 갖습니다 2, 등).</span><span class="sxs-lookup"><span data-stu-id="0f437-132">In addition to making DinnerID a primary key, we also want configure it as an "identity" column whose value is automatically incremented as new rows of data are added to the table (meaning the first inserted Dinner row will have a DinnerID of 1, the second inserted row will have a DinnerID of 2, etc).</span></span>

<span data-ttu-id="0f437-133">म "DinnerID" 열을 선택 하 여이 작업을 수행 하 고 "열 속성" 편집기를 사용 하 여 "예"로 열에 "(Identity는)" 속성을 설정 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-133">We can do this by selecting the "DinnerID" column and then use the "Column Properties" editor to set the "(Is Identity)" property on the column to "Yes".</span></span> <span data-ttu-id="0f437-134">표준 id 기본값을 사용 합니다 (1부터 시작 하 고 각 새 Dinner 행에 1를 증가 시키는):</span><span class="sxs-lookup"><span data-stu-id="0f437-134">We will use the standard identity defaults (start at 1 and increment 1 on each new Dinner row):</span></span>

![](create-a-database/_static/image9.png)

<span data-ttu-id="0f437-135">Ctrl + S를 입력 하 여 또는 사용 하 여 테이블을 저장 한 다음 하겠습니다는 **파일-&gt;저장** 메뉴 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-135">We'll then save our table by typing Ctrl-S or by using the **File-&gt;Save** menu command.</span></span> <span data-ttu-id="0f437-136">테이블의 이름을 지정 하는 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-136">This will prompt us to name the table.</span></span> <span data-ttu-id="0f437-137">이름을 것 "Dinners":</span><span class="sxs-lookup"><span data-stu-id="0f437-137">We'll name it "Dinners":</span></span>

![](create-a-database/_static/image10.png)

<span data-ttu-id="0f437-138">서버 탐색기에서 데이터베이스 내에서 새 Dinners 테이블 표시 한 다음 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-138">Our new Dinners table will then show up within our database in the server explorer.</span></span>

<span data-ttu-id="0f437-139">그런 다음 위의 단계를 반복 알아보고 "RSVP" 테이블을 만들 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-139">We'll then repeat the above steps and create a "RSVP" table.</span></span> <span data-ttu-id="0f437-140">와이 테이블 3 개의 열이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-140">This table with have 3 columns.</span></span> <span data-ttu-id="0f437-141">RsvpID 열을 기본 키로 설정 하 고 또한 id 열인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-141">We will setup the RsvpID column as the primary key, and also make it an identity column:</span></span>

![](create-a-database/_static/image11.png)

<span data-ttu-id="0f437-142">저장 알아보고 "RSVP" 이름을 지정 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-142">We'll save it and give it the name "RSVP".</span></span>

### <a name="setting-up-a-foreign-key-relationship-between-tables"></a><span data-ttu-id="0f437-143">테이블 간 외래 키 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-143">Setting up a Foreign Key Relationship between Tables</span></span>

<span data-ttu-id="0f437-144">했습니다 두 테이블 데이터베이스 내에서.</span><span class="sxs-lookup"><span data-stu-id="0f437-144">We now have two tables within our database.</span></span> <span data-ttu-id="0f437-145">각 Dinner 행에 적용 되는 0 개 이상의 RSVP 행 연결 수 있도록 우리의 마지막 스키마 디자인 단계 – 이러한 두 테이블 간에 "일대다" 관계를 설정 하 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-145">Our last schema design step will be to setup a "one-to-many" relationship between these two tables – so that we can associate each Dinner row with zero or more RSVP rows that apply to it.</span></span> <span data-ttu-id="0f437-146">"Dinners" 테이블의 "DinnerID" 열에 외래 키 관계에 RSVP 테이블의 "DinnerID" 열을 구성 하 여 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-146">We will do this by configuring the RSVP table's "DinnerID" column to have a foreign-key relationship to the "DinnerID" column in the "Dinners" table.</span></span>

<span data-ttu-id="0f437-147">이렇게 하려면 서버 탐색기에서 두 번 클릭 하 여 테이블 디자이너에서는 RSVP 테이블을 엽니다 했습니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-147">To do this we'll open up the RSVP table within the table designer by double-clicking it in the server explorer.</span></span> <span data-ttu-id="0f437-148">그 안의 "DinnerID" 열 선택 다음 마우스 오른쪽 단추로 클릭 하 고 "Relationshps..."를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-148">We'll then select the "DinnerID" column within it, right-click, and choose the "Relationshps…"</span></span> <span data-ttu-id="0f437-149">상황에 맞는 메뉴 명령:</span><span class="sxs-lookup"><span data-stu-id="0f437-149">context menu command:</span></span>

![](create-a-database/_static/image12.png)

<span data-ttu-id="0f437-150">그러면 म 테이블 간의 관계를 설정 하는 데 사용할 수 있는 대화 상자를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-150">This will bring up a dialog that we can use to setup relationships between tables:</span></span>

![](create-a-database/_static/image13.png)

<span data-ttu-id="0f437-151">대화 상자에 새 관계를 추가 하려면 "추가" 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-151">We'll click the "Add" button to add a new relationship to the dialog.</span></span> <span data-ttu-id="0f437-152">관계 추가 되 면에 대화 상자에서 오른쪽에 속성 표 내에서 "테이블 및 열 사양" 트리 뷰 노드를 확장 하 고 열의 오른쪽에 있는 "..." 단추를 클릭 합니다 했습니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-152">Once a relationship has been added, we'll expand the "Tables and Column Specification" tree-view node within the property grid to the right of the dialog, and then click the "…" button to the right of it:</span></span>

![](create-a-database/_static/image14.png)

<span data-ttu-id="0f437-153">"..." 단추를 클릭 하면 테이블 및 열, 관계에 참여 한다고 뿐만 아니라 관계의 이름을 하기 수를 지정할 수 있도록 하는 또 다른 대화 상자를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-153">Clicking the "…" button will bring up another dialog that allows us to specify which tables and columns are involved in the relationship, as well as allow us to name the relationship.</span></span>

<span data-ttu-id="0f437-154">"Dinners" 되도록 기본 키 테이블을 변경 하 고 기본 키로 Dinners 테이블 내에서 "DinnerID" 열을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-154">We will change the Primary Key Table to be "Dinners", and select the "DinnerID" column within the Dinners table as the primary key.</span></span> <span data-ttu-id="0f437-155">외래 키 테이블 및 RSVP RSVP 테이블이 됩니다. DinnerID 열이 외래 키로 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-155">Our RSVP table will be the foreign-key table, and the RSVP.DinnerID column will be associated as the foreign-key:</span></span>

![](create-a-database/_static/image15.png)

<span data-ttu-id="0f437-156">이제 RSVP 테이블의 각 행은 Dinner 테이블의 행과 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-156">Now each row in the RSVP table will be associated with a row in the Dinner table.</span></span> <span data-ttu-id="0f437-157">SQL Server 소중에 대 한 참조 무결성을 유지 되며에서 올바른 Dinner 행을 가리키지 않을 경우 새 RSVP 행을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-157">SQL Server will maintain referential integrity for us – and prevent us from adding a new RSVP row if it does not point to a valid Dinner row.</span></span> <span data-ttu-id="0f437-158">또한 예방할 우리에서 참조 하는 행을 RSVP 여전히 없으면 Dinner 행을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-158">It will also prevent us from deleting a Dinner row if there are still RSVP rows referring to it.</span></span>

### <a name="adding-data-to-our-tables"></a><span data-ttu-id="0f437-159">이 코드에서는 테이블에 데이터 추가</span><span class="sxs-lookup"><span data-stu-id="0f437-159">Adding Data to our Tables</span></span>

<span data-ttu-id="0f437-160">Dinners 테이블에 몇 가지 샘플 데이터를 추가 하 여 완료 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-160">Let's finish by adding some sample data to our Dinners table.</span></span> <span data-ttu-id="0f437-161">에 서버 탐색기 내에서 마우스 오른쪽 단추로 클릭 하 고 "테이블 데이터 표시" 명령을 선택 하 여 테이블에 데이터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-161">We can add data to a table by right-clicking on it within the Server Explorer and choosing the "Show Table Data" command:</span></span>

![](create-a-database/_static/image16.png)

<span data-ttu-id="0f437-162">나중에 응용 프로그램을 구현 하는 때 사용할 수 있는 Dinner 데이터 행을 몇 개 추가 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-162">We'll add a few rows of Dinner data that we can use later as we start implementing the application:</span></span>

![](create-a-database/_static/image17.png)

### <a name="next-step"></a><span data-ttu-id="0f437-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0f437-163">Next Step</span></span>

<span data-ttu-id="0f437-164">이 데이터베이스를 만드는 하는 작업을 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-164">We've finished creating our database.</span></span> <span data-ttu-id="0f437-165">이제 쿼리 하 고 업데이트를 사용할 수 있는 모델 클래스를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0f437-165">Let's now create model classes that we can use to query and update it.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0f437-166">[이전](create-a-new-aspnet-mvc-project.md)
> [다음](build-a-model-with-business-rule-validations.md)</span><span class="sxs-lookup"><span data-stu-id="0f437-166">[Previous](create-a-new-aspnet-mvc-project.md)
[Next](build-a-model-with-business-rule-validations.md)</span></span>
