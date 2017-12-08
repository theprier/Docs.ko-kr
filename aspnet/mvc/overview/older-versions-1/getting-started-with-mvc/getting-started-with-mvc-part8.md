---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
title: "모델에 열 추가 | Microsoft Docs"
author: shanselman
description: "ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 읽기 및 쓰기는 데이터베이스에서 단순 웹 응용 프로그램을 만들 수 있습니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/14/2010
ms.topic: article
ms.assetid: 7ae696b9-348f-4993-8ebb-a838acbe0c28
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
msc.type: authoredcontent
ms.openlocfilehash: 4a4fc144dcbed8ad14411332df7acccc032ddf46
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="adding-a-column-to-the-model"></a><span data-ttu-id="131ce-104">모델에 열 추가</span><span class="sxs-lookup"><span data-stu-id="131ce-104">Adding a Column to the Model</span></span>
====================
<span data-ttu-id="131ce-105">으로 [Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="131ce-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="131ce-106">ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="131ce-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="131ce-107">읽기 및 쓰기는 데이터베이스에서 단순 웹 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="131ce-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="131ce-108">방문는 [ASP.NET MVC 학습 센터](../../../index.md) 자습서 및 예제에는 다른 ASP.NET MVC를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="131ce-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>


<span data-ttu-id="131ce-109">이 섹션에서는 하겠습니다를 데이터베이스의 스키마를 변경할를 응용 프로그램 내에서 변경 내용을 처리할 수 있습니다 어떻게 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="131ce-109">In this section we are going to walk through how we can make changes to the schema of our database, and handle the changes within our application.</span></span>

<span data-ttu-id="131ce-110">영화 테이블에 "등급" 열을 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="131ce-110">Let's add a "Rating" Colum to the Movie table.</span></span> <span data-ttu-id="131ce-111">IDE로 다시 이동 하 고 데이터베이스 탐색기를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="131ce-111">Go back to the IDE and click the Database Explorer.</span></span> <span data-ttu-id="131ce-112">영화 테이블을 마우스 오른쪽 단추로 클릭 하 고 테이블 정의 열기를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="131ce-112">Right click the Movie table and select Open Table Definition.</span></span>

<span data-ttu-id="131ce-113">아래와 같이 "등급" 열을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="131ce-113">Add a "Rating" column as seen below.</span></span> <span data-ttu-id="131ce-114">이제 모든 등급 않아도, 되므로 열 수 null을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="131ce-114">Since we don't have any Ratings now, the column can allow nulls.</span></span> <span data-ttu-id="131ce-115">저장을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="131ce-115">Click Save.</span></span>

<span data-ttu-id="131ce-116">[![영화 테이블 편집](getting-started-with-mvc-part8/_static/image2.png)](getting-started-with-mvc-part8/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="131ce-116">[![Editing Movies Table](getting-started-with-mvc-part8/_static/image2.png)](getting-started-with-mvc-part8/_static/image1.png)</span></span>

<span data-ttu-id="131ce-117">다음으로, 솔루션 탐색기로 반환 하 고 (즉 \Models 폴더에) Movies.edmx 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="131ce-117">Next, return to the Solution Explorer and open up the Movies.edmx file (which is in the \Models folder).</span></span> <span data-ttu-id="131ce-118">디자인 화면 (흰색 영역)을 마우스 오른쪽 단추로 클릭 하 고 데이터베이스에서 모델 업데이트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="131ce-118">Right click on the design surface (the white area) and select Update Model from Database.</span></span>

<span data-ttu-id="131ce-119">[![동영상-Microsoft Visual 웹 Developer 2010 Express (11)](getting-started-with-mvc-part8/_static/image4.png)](getting-started-with-mvc-part8/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="131ce-119">[![Movies - Microsoft Visual Web Developer 2010 Express (11)](getting-started-with-mvc-part8/_static/image4.png)](getting-started-with-mvc-part8/_static/image3.png)</span></span>

<span data-ttu-id="131ce-120">"업데이트 마법사" 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="131ce-120">This will launch the "Update Wizard".</span></span> <span data-ttu-id="131ce-121">내에서 새로 고침 탭을 클릭 하 고 마침을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="131ce-121">Click the Refresh tab within it and click Finish.</span></span> <span data-ttu-id="131ce-122">영화 모델 클래스는 새 열이 포함 된 다음 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="131ce-122">Our Movie model class will then be updated with the new column.</span></span>

![업데이트 마법사 (2)](getting-started-with-mvc-part8/_static/image5.png)

<span data-ttu-id="131ce-124">마침을 클릭 한 후이 모델 영화 엔터티에 추가한 새 등급 열을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="131ce-124">After clicking Finish, you can see the new Rating Column has been added to the Movie Entity in our model.</span></span>

<span data-ttu-id="131ce-125">[![영화 엔터티](getting-started-with-mvc-part8/_static/image7.png)](getting-started-with-mvc-part8/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="131ce-125">[![Movie Entity](getting-started-with-mvc-part8/_static/image7.png)](getting-started-with-mvc-part8/_static/image6.png)</span></span>

<span data-ttu-id="131ce-126">데이터베이스 모델에서 열을 추가 했습니다 있지만 보기 항목에 대 한 알 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="131ce-126">We've added a column in the database model, but the Views don't know about it.</span></span>

## <a name="update-views-with-model-changes"></a><span data-ttu-id="131ce-127">뷰 모델 변경 내용으로 업데이트</span><span class="sxs-lookup"><span data-stu-id="131ce-127">Update Views with Model Changes</span></span>

<span data-ttu-id="131ce-128">몇 가지 방법으로 새 등급 열을 반영 하기 위해 템플릿 보기를 사용 하 여 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="131ce-128">There are a few ways we could update our view templates to reflect the new Rating column.</span></span> <span data-ttu-id="131ce-129">뷰 추가 대화 상자를 통해이 생성 하 여 이러한 보기를 만든 후 삭제할 하 고 다시 다시 만드십시오 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="131ce-129">Since we created these Views by generating them via the Add View dialog, we could delete them and recreate them again.</span></span> <span data-ttu-id="131ce-130">그러나 일반적으로 초기 스 캐 폴드 생성에서 해당 템플릿 보기 수정을 이미 작성지 것입니다 사람과 추가 하 여 만들기에 대 한 ID 필드와 했던 것 처럼 마찬가지로 수동으로 필드를 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="131ce-130">However, typically people will have already made modifications to their View templates from the initial scaffolded generation and will want to add or delete fields manually, just as we did with the ID field for Create.</span></span>

<span data-ttu-id="131ce-131">\Views\Movies\Index.aspx 서식 파일을 열고 추가 &lt;번째&gt;등급&lt;/th&gt; 영화 테이블의 머리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="131ce-131">Open up the \Views\Movies\Index.aspx template and add a &lt;th&gt;Rating&lt;/th&gt; to the head of the Movie table.</span></span> <span data-ttu-id="131ce-132">Genre 후 마이닝를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="131ce-132">I added mine after Genre.</span></span> <span data-ttu-id="131ce-133">그런 다음 동일한 열 위치에 있지만 더 낮은 선을 추가 하 여이 새 등급을 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="131ce-133">Then, in the same column position but lower down, add a line to output our new Rating.</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample1.aspx)]

<span data-ttu-id="131ce-134">우리의 마지막 Index.aspx 서식 파일은 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="131ce-134">Our final Index.aspx template will look like this:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample2.aspx)]

<span data-ttu-id="131ce-135">보겠습니다 다음 \Views\Movies\Create.aspx 서식 파일을 열고 새 등급 속성이 대 한 레이블 및 텍스트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="131ce-135">Let's then open up the \Views\Movies\Create.aspx template and add a Label and Textbox for our new Rating property:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample3.aspx)]

<span data-ttu-id="131ce-136">우리의 마지막 Create.aspx 서식 파일을 다음과 같이 표시 되며 바꿔보겠습니다 브라우저의 제목 및 보조 &lt;h2&gt; "만들기는 영화" 여기에 있을 때와 같은 값으로 제목!</span><span class="sxs-lookup"><span data-stu-id="131ce-136">Our final Create.aspx template will look like this, and let's change our browser's title and secondary &lt;h2&gt; title to something like "Create a Movie" while we're in here!</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample4.aspx)]

<span data-ttu-id="131ce-137">응용 프로그램을 실행 하 고 만들기 페이지에 추가 된은 데이터베이스에 새 필드가 완성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="131ce-137">Run your app and now you've got a new field in the database that's been added to the Create page.</span></span> <span data-ttu-id="131ce-138">이 이번에는 등급--새 동영상을 추가 하 고 만들기를 클릭 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="131ce-138">Add a new Movie - this time with a Rating - and click Create.</span></span>

<span data-ttu-id="131ce-139">[![동영상-Windows Internet Explorer 만들기](getting-started-with-mvc-part8/_static/image9.png)](getting-started-with-mvc-part8/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="131ce-139">[![Create a Movie - Windows Internet Explorer](getting-started-with-mvc-part8/_static/image9.png)](getting-started-with-mvc-part8/_static/image8.png)</span></span>

<span data-ttu-id="131ce-140">인덱스 페이지에 전송 하는 만들기를 클릭 하면 새 동영상이 함께 나열 하는 경우 데이터베이스에 새 등급 열</span><span class="sxs-lookup"><span data-stu-id="131ce-140">After you click Create, you're sent to the Index page where you new Movie is listed with the new Rating Column in the database</span></span>

<span data-ttu-id="131ce-141">[![영화 목록-Windows Internet Explorer (12)](getting-started-with-mvc-part8/_static/image11.png)](getting-started-with-mvc-part8/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="131ce-141">[![Movie List - Windows Internet Explorer (12)](getting-started-with-mvc-part8/_static/image11.png)](getting-started-with-mvc-part8/_static/image10.png)</span></span>

<span data-ttu-id="131ce-142">이 기본 자습서 보기와 연결 하 고 하드 코드 된 데이터에 대 한 전달 컨트롤러를 만들기 시작 했습니다.</span><span class="sxs-lookup"><span data-stu-id="131ce-142">This basic tutorial got you started making Controllers, associating them with Views and passing around hard-coded data.</span></span> <span data-ttu-id="131ce-143">에서는 데이터베이스 디자인 하 고 만들고 일부 데이터를 저장 한 다음에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="131ce-143">Then we created and designed a Database and put some data it in.</span></span> <span data-ttu-id="131ce-144">데이터베이스에서 데이터를 검색 하 고 HTML 테이블에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="131ce-144">We retrieved the data from the database and displayed it in an HTML table.</span></span> <span data-ttu-id="131ce-145">그런 다음 데이터를 추가할 데이터베이스 자체에서 웹 응용 프로그램의 사용자 수 있는 폼 만들기를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="131ce-145">Then we added a Create form that let the user add data to the database themselves from within the Web Application.</span></span> <span data-ttu-id="131ce-146">유효성 검사를 추가 합니다. 그런 다음 JavaScript를 사용 하 여 클라이언트 쪽 유효성 검사를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="131ce-146">We added validation, then made the validation use JavaScript on the client-side.</span></span> <span data-ttu-id="131ce-147">마지막으로의 데이터를 새 열을 포함 하도록 데이터베이스를 변경 하 후 만들고 이러한 새 데이터를 표시 하는 두 개의 페이지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="131ce-147">Finally, we changed the database to include a new column of data, then updated our two pages to create and display this new data.</span></span>

<span data-ttu-id="131ce-148">이제 확인해이 중간 수준 자습서로 이동할 수 있습니다 "[MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)" 뿐 아니라 많은 비디오 및 리소스에 [https://asp.net/mvc](https://asp.net/mvc) ASP.NET MVC에 대해 훨씬 더 자세한!</span><span class="sxs-lookup"><span data-stu-id="131ce-148">I now encourage you to move on to our intermediate-level tutorial "[MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)" as well as the many videos and resources at [https://asp.net/mvc](https://asp.net/mvc) to learn even more about ASP.NET MVC!</span></span>

<span data-ttu-id="131ce-149">원하는 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="131ce-149">Enjoy!</span></span>

- <span data-ttu-id="131ce-150">Scott Hanselman- [http://hanselman.com](http://hanselman.com) 및 [ @shanselman ](http://twitter.com/shanselman) Twitter에서.</span><span class="sxs-lookup"><span data-stu-id="131ce-150">Scott Hanselman - [http://hanselman.com](http://hanselman.com) and [@shanselman](http://twitter.com/shanselman) on Twitter.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="131ce-151">이전</span><span class="sxs-lookup"><span data-stu-id="131ce-151">Previous</span></span>](getting-started-with-mvc-part7.md)
