---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part4
title: 데이터베이스 만들기 | Microsoft Docs
author: shanselman
description: ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 읽기 및 쓰기는 데이터베이스에서 단순 웹 응용 프로그램을 만듭니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/14/2010
ms.topic: article
ms.assetid: 742df67f-484d-4ef3-af6b-8c791e556b43
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part4
msc.type: authoredcontent
ms.openlocfilehash: ff2a41803cd31ce50bbf79e630d827b6de441ba3
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="creating-a-database"></a><span data-ttu-id="1ee71-104">데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="1ee71-104">Creating a Database</span></span>
====================
<span data-ttu-id="1ee71-105">으로 [Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="1ee71-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="1ee71-106">ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="1ee71-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="1ee71-107">읽기 및 쓰기는 데이터베이스에서 단순 웹 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ee71-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="1ee71-108">방문는 [ASP.NET MVC 학습 센터](../../../index.md) 자습서 및 예제에는 다른 ASP.NET MVC를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ee71-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>


<span data-ttu-id="1ee71-109">이 섹션에서는 하겠습니다 우리의 동영상 데이터 저장 및 검색을 사용 해야 하는 새로운 SQL Express 데이터베이스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ee71-109">In this section we are going to create a new SQL Express database that we'll use to store and retrieve our movie data.</span></span> <span data-ttu-id="1ee71-110">Visual Web Developer IDE 내에서 보기를 선택 | 서버 탐색기입니다.</span><span class="sxs-lookup"><span data-stu-id="1ee71-110">From within the Visual Web Developer IDE, select View | Server Explorer.</span></span> <span data-ttu-id="1ee71-111">데이터 연결을 마우스 오른쪽 단추로 클릭 하 고 연결 추가...</span><span class="sxs-lookup"><span data-stu-id="1ee71-111">Right click on Data Connections and click Add Connection...</span></span>

![AddConnection](getting-started-with-mvc-part4/_static/image1.png)

<span data-ttu-id="1ee71-113">데이터 소스 선택 대화 상자에서 Microsoft SQL Server를 선택 하 고 계속을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee71-113">In the Choose Data Source dialog, select Microsoft SQL Server and select Continue.</span></span>

![](getting-started-with-mvc-part4/_static/image2.png)

<span data-ttu-id="1ee71-114">연결 추가 대화 상자에 입력 ". \SQLEXPRESS" 서버 이름에 대 한 새 데이터베이스 이름으로 "영화"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee71-114">In the Add Connection dialog, enter ".\SQLEXPRESS" for your Server Name, and enter "Movies" as the name for your new database.</span></span>

<span data-ttu-id="1ee71-115">[![연결 대화 상자를 추가 합니다.](getting-started-with-mvc-part4/_static/image4.png)](getting-started-with-mvc-part4/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="1ee71-115">[![Add Connection dialog](getting-started-with-mvc-part4/_static/image4.png)](getting-started-with-mvc-part4/_static/image3.png)</span></span>

<span data-ttu-id="1ee71-116">확인을 클릭 하면 해당 데이터베이스를 만들려는 경우 라는 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="1ee71-116">Click OK and you'll be asked if you want to create that database.</span></span> <span data-ttu-id="1ee71-117">예를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee71-117">Select yes.</span></span>

<span data-ttu-id="1ee71-118">[![영화를 만드시겠습니까?](getting-started-with-mvc-part4/_static/image6.png)](getting-started-with-mvc-part4/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="1ee71-118">[![Create Movies?](getting-started-with-mvc-part4/_static/image6.png)](getting-started-with-mvc-part4/_static/image5.png)</span></span>

<span data-ttu-id="1ee71-119">서버 탐색기에서 빈 데이터베이스를 완성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1ee71-119">Now you've got an empty database in Server Explorer.</span></span>

![새 테이블 추가](getting-started-with-mvc-part4/_static/image7.png)

<span data-ttu-id="1ee71-121">테이블을 마우스 오른쪽 단추로 클릭 하 고 테이블 추가 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee71-121">Right click on Tables and click Add Table.</span></span> <span data-ttu-id="1ee71-122">테이블 디자이너에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ee71-122">The Table Designer will appear.</span></span> <span data-ttu-id="1ee71-123">Id, 제목, ReleaseDate, Genre 및 가격에 대 한 열을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee71-123">Add columns for Id, Title, ReleaseDate, Genre, and Price.</span></span> <span data-ttu-id="1ee71-124">ID 열을 마우스 오른쪽 단추로 클릭 하 고 클릭 하 여 기본 키를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee71-124">Right click on the ID column and click set Primary Key.</span></span> <span data-ttu-id="1ee71-125">다음과 같은 내 디자인 영역에는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1ee71-125">Here's what my design areas looks like.</span></span>

<span data-ttu-id="1ee71-126">[![데이터베이스 테이블 편집기](getting-started-with-mvc-part4/_static/image9.png)](getting-started-with-mvc-part4/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="1ee71-126">[![Database Table Editor](getting-started-with-mvc-part4/_static/image9.png)](getting-started-with-mvc-part4/_static/image8.png)</span></span>

<span data-ttu-id="1ee71-127">또한 Id 열을 선택 하 고 열 속성 아래에서 "Id 사양"을 "Yes"로 변경</span><span class="sxs-lookup"><span data-stu-id="1ee71-127">Also, select the Id column and under Column Properties below change "Identity Specification" to "Yes."</span></span>

<span data-ttu-id="1ee71-128">[![IsIdentity-열 속성](getting-started-with-mvc-part4/_static/image11.png)](getting-started-with-mvc-part4/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="1ee71-128">[![IsIdentity - Column Properties](getting-started-with-mvc-part4/_static/image11.png)](getting-started-with-mvc-part4/_static/image10.png)</span></span>

<span data-ttu-id="1ee71-129">도구 모음에 저장 아이콘을 클릭 하거나 파일을 선택 였음을 완료를 하는 경우 | 메뉴에서 저장 하 고 테이블 이름을 "**영화**" (단 수)입니다.</span><span class="sxs-lookup"><span data-stu-id="1ee71-129">When you've got it done, click the Save icon in the toolbar or select File | Save from the menu, and name your table "**Movie**" (singular).</span></span> <span data-ttu-id="1ee71-130">데이터베이스와 테이블 설명 했습니다!</span><span class="sxs-lookup"><span data-stu-id="1ee71-130">We've got a database and a table!</span></span>

<span data-ttu-id="1ee71-131">[![이름 선택](getting-started-with-mvc-part4/_static/image13.png)](getting-started-with-mvc-part4/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="1ee71-131">[![Choose Name](getting-started-with-mvc-part4/_static/image13.png)](getting-started-with-mvc-part4/_static/image12.png)</span></span>

<span data-ttu-id="1ee71-132">서버 탐색기로 다시 이동 하 영화 테이블을 마우스 오른쪽 단추로 클릭 한 다음 "테이블 데이터 표시 합니다."를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee71-132">Go back to Server Explorer and right click the Movie table, then select "Show Table Data."</span></span> <span data-ttu-id="1ee71-133">몇 가지 영화를 입력 하 여 데이터베이스에 일부 데이터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ee71-133">Enter a few movies so our database has some data.</span></span>

<span data-ttu-id="1ee71-134">[![데이터베이스 테이블 편집](getting-started-with-mvc-part4/_static/image15.png)](getting-started-with-mvc-part4/_static/image14.png)</span><span class="sxs-lookup"><span data-stu-id="1ee71-134">[![Database Table Editing](getting-started-with-mvc-part4/_static/image15.png)](getting-started-with-mvc-part4/_static/image14.png)</span></span>

## <a name="creating-a-model"></a><span data-ttu-id="1ee71-135">모델 만들기</span><span class="sxs-lookup"><span data-stu-id="1ee71-135">Creating a Model</span></span>

<span data-ttu-id="1ee71-136">이제 IDE의 오른쪽에 솔루션 탐색기로 다시 전환 하 고 모델 폴더를 마우스 오른쪽 단추로 클릭 고 추가 선택 | 새 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="1ee71-136">Now, switch back to the Solution Explorer on the right hand side of the IDE and right-click on the Models folder and select Add | New Item.</span></span>

<span data-ttu-id="1ee71-137">[![addnewmodelitem](getting-started-with-mvc-part4/_static/image17.png)](getting-started-with-mvc-part4/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="1ee71-137">[![addnewmodelitem](getting-started-with-mvc-part4/_static/image17.png)](getting-started-with-mvc-part4/_static/image16.png)</span></span>

<span data-ttu-id="1ee71-138">새 데이터베이스에서 엔터티 모델을 만들 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1ee71-138">We're going to create an Entity Model from our new database.</span></span> <span data-ttu-id="1ee71-139">이렇게 하면 클래스 집합을 쿼리하고 데이터베이스 내에서 데이터를 조작 하기 위해 활용할 수 있는 프로젝트에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ee71-139">This will add a set of classes to our project that makes it easy for us to query and manipulate the data within our database.</span></span> <span data-ttu-id="1ee71-140">대화 상자에서 왼쪽의 데이터 노드를 선택 하 고 ADO.NET 엔터티 데이터 모델 항목 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee71-140">Select the Data node on the left-hand side of the dialog, and then select the ADO.NET Entity Data Model item template.</span></span> <span data-ttu-id="1ee71-141">Movies.edmx 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee71-141">Name it Movies.edmx.</span></span>

<span data-ttu-id="1ee71-142">[![AddNewDataModel](getting-started-with-mvc-part4/_static/image19.png)](getting-started-with-mvc-part4/_static/image18.png)</span><span class="sxs-lookup"><span data-stu-id="1ee71-142">[![AddNewDataModel](getting-started-with-mvc-part4/_static/image19.png)](getting-started-with-mvc-part4/_static/image18.png)</span></span>

<span data-ttu-id="1ee71-143">"추가" 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee71-143">Click the "Add" button.</span></span> <span data-ttu-id="1ee71-144">그런 다음 "엔터티 데이터 모델 마법사" 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ee71-144">This will then launch the "Entity Data Model Wizard".</span></span>

<span data-ttu-id="1ee71-145">새 대화 상자가 나타나면 데이터베이스에서 생성을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee71-145">In the new dialog that pops up, select Generate from Database.</span></span> <span data-ttu-id="1ee71-146">데이터베이스를 방금 만든 이후 Entity Framework에 새 데이터베이스 및 해당 테이블에 대 한 해야만 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee71-146">Since we've just made a database, we'll only need to tell the Entity Framework about our new database and its table.</span></span> <span data-ttu-id="1ee71-147">이제 웹 응용 프로그램의 구성에서 데이터베이스 연결 우리의 저장 옆에 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee71-147">Click Next to save our database connection in our web application's configuration.</span></span> <span data-ttu-id="1ee71-148">이제, 테이블 및 동영상을 확인 확인란을 선택 하 고 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee71-148">Now, check the Tables and Movie checkbox and click Finish.</span></span>

<span data-ttu-id="1ee71-149">[![엔터티 데이터 모델 마법사](getting-started-with-mvc-part4/_static/image21.png)](getting-started-with-mvc-part4/_static/image20.png)</span><span class="sxs-lookup"><span data-stu-id="1ee71-149">[![Entity Data Model Wizard](getting-started-with-mvc-part4/_static/image21.png)](getting-started-with-mvc-part4/_static/image20.png)</span></span>

<span data-ttu-id="1ee71-150">이제 Entity Framework Designer에서 새 동영상 테이블 표시 되 고 코드에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ee71-150">Now we can see our new Movie table in the Entity Framework Designer and access it from code.</span></span>

<span data-ttu-id="1ee71-151">[![동영상-Microsoft Visual Developer 2010 Express를 웹](getting-started-with-mvc-part4/_static/image23.png)](getting-started-with-mvc-part4/_static/image22.png)</span><span class="sxs-lookup"><span data-stu-id="1ee71-151">[![Movies - Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part4/_static/image23.png)](getting-started-with-mvc-part4/_static/image22.png)</span></span>

<span data-ttu-id="1ee71-152">디자인 화면에서 "영화" 클래스를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ee71-152">On the design surface you can see a "Movie" class.</span></span> <span data-ttu-id="1ee71-153">이 클래스는 데이터베이스에 "영화" 테이블에 매핑되고 내에 각 속성 테이블을 가진 열에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ee71-153">This class maps to the "Movie" table in our database, and each property within it maps to a column with the table.</span></span> <span data-ttu-id="1ee71-154">"영화" 클래스의 각 인스턴스는 "영화" 테이블 내의 행에 대응 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ee71-154">Each instance of a "Movie" class will correspond to a row within the "Movie" table.</span></span>

<span data-ttu-id="1ee71-155">기본 이름 지정 및 Entity Framework에서 사용 되는 규칙을 매핑, 마음에 들지 않으면를 변경 하거나 사용자 지정 하는 Entity Framework 디자이너를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ee71-155">If you don't like the default naming and mapping conventions used by the Entity Framework, you can use the Entity Framework designer to change or customize them.</span></span> <span data-ttu-id="1ee71-156">이 응용 프로그램에 대 한 기본값을 사용 하 여 알아보고 방금로 파일을 저장 하겠습니다-됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ee71-156">For this application we'll use the defaults and just save the file as-is.</span></span>

<span data-ttu-id="1ee71-157">이제 몇 가지 실제 데이터로 확인해 보겠습니다!</span><span class="sxs-lookup"><span data-stu-id="1ee71-157">Now, let's work with some real data!</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1ee71-158">[이전](getting-started-with-mvc-part3.md)
> [다음](getting-started-with-mvc-part5.md)</span><span class="sxs-lookup"><span data-stu-id="1ee71-158">[Previous](getting-started-with-mvc-part3.md)
[Next](getting-started-with-mvc-part5.md)</span></span>
