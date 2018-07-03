---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
title: 모델에 열 추가 | Microsoft Docs
author: shanselman
description: ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 읽기 및 쓰기 데이터베이스에서 간단한 웹 응용 프로그램을 만듭니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/14/2010
ms.topic: article
ms.assetid: 7ae696b9-348f-4993-8ebb-a838acbe0c28
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
msc.type: authoredcontent
ms.openlocfilehash: 241f9108394561fecb15db5b6efa2661fdb128d6
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37361762"
---
<a name="adding-a-column-to-the-model"></a><span data-ttu-id="b50d6-104">모델에 열 추가</span><span class="sxs-lookup"><span data-stu-id="b50d6-104">Adding a Column to the Model</span></span>
====================
<span data-ttu-id="b50d6-105">[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="b50d6-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="b50d6-106">ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="b50d6-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="b50d6-107">읽기 및 쓰기 데이터베이스는 간단한 웹 응용 프로그램을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d6-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="b50d6-108">방문 합니다 [ASP.NET MVC 학습 센터](../../../index.md) 자습서 및 샘플 다른 ASP.NET MVC를 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b50d6-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>


<span data-ttu-id="b50d6-109">이 섹션에서는 수는 데이터베이스의 스키마 변경 및 응용 프로그램 내에서 변경 내용을 처리 하는 방법을 안내 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d6-109">In this section we are going to walk through how we can make changes to the schema of our database, and handle the changes within our application.</span></span>

<span data-ttu-id="b50d6-110">동영상 테이블에 "등급" 열을 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b50d6-110">Let's add a "Rating" Colum to the Movie table.</span></span> <span data-ttu-id="b50d6-111">IDE로 돌아가서 데이터베이스 탐색기를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d6-111">Go back to the IDE and click the Database Explorer.</span></span> <span data-ttu-id="b50d6-112">Movie 테이블을 마우스 오른쪽 단추로 클릭 하 고 테이블 정의 열기를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d6-112">Right click the Movie table and select Open Table Definition.</span></span>

<span data-ttu-id="b50d6-113">아래와 같이 "Rating" 열을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d6-113">Add a "Rating" column as seen below.</span></span> <span data-ttu-id="b50d6-114">이제 모든 등급 않아도, 되므로 null 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b50d6-114">Since we don't have any Ratings now, the column can allow nulls.</span></span> <span data-ttu-id="b50d6-115">저장을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d6-115">Click Save.</span></span>

<span data-ttu-id="b50d6-116">[![동영상 테이블 편집](getting-started-with-mvc-part8/_static/image2.png)](getting-started-with-mvc-part8/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b50d6-116">[![Editing Movies Table](getting-started-with-mvc-part8/_static/image2.png)](getting-started-with-mvc-part8/_static/image1.png)</span></span>

<span data-ttu-id="b50d6-117">다음으로, 솔루션 탐색기에 반환 하 고 (상태인 \Models 폴더) Movies.edmx 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b50d6-117">Next, return to the Solution Explorer and open up the Movies.edmx file (which is in the \Models folder).</span></span> <span data-ttu-id="b50d6-118">디자인 화면 (흰색 영역)을 마우스 오른쪽 단추로 클릭 하 고 데이터베이스에서 모델 업데이트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d6-118">Right click on the design surface (the white area) and select Update Model from Database.</span></span>

<span data-ttu-id="b50d6-119">[![동영상-Microsoft Visual Web Developer 2010 Express (11)](getting-started-with-mvc-part8/_static/image4.png)](getting-started-with-mvc-part8/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="b50d6-119">[![Movies - Microsoft Visual Web Developer 2010 Express (11)](getting-started-with-mvc-part8/_static/image4.png)](getting-started-with-mvc-part8/_static/image3.png)</span></span>

<span data-ttu-id="b50d6-120">"업데이트 마법사" 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b50d6-120">This will launch the "Update Wizard".</span></span> <span data-ttu-id="b50d6-121">에 새로 고침 탭을 클릭 하 고 마침을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d6-121">Click the Refresh tab within it and click Finish.</span></span> <span data-ttu-id="b50d6-122">영화 모델 클래스는 새 열을 사용 하 여 다음 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b50d6-122">Our Movie model class will then be updated with the new column.</span></span>

![업데이트 마법사 (2)](getting-started-with-mvc-part8/_static/image5.png)

<span data-ttu-id="b50d6-124">완료를 클릭 하면 영화 엔터티 모델에 추가한 새 등급 열을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b50d6-124">After clicking Finish, you can see the new Rating Column has been added to the Movie Entity in our model.</span></span>

<span data-ttu-id="b50d6-125">[![영화 엔터티](getting-started-with-mvc-part8/_static/image7.png)](getting-started-with-mvc-part8/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="b50d6-125">[![Movie Entity](getting-started-with-mvc-part8/_static/image7.png)](getting-started-with-mvc-part8/_static/image6.png)</span></span>

<span data-ttu-id="b50d6-126">데이터베이스 모델에서 열을 추가한 보기 모 르에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d6-126">We've added a column in the database model, but the Views don't know about it.</span></span>

## <a name="update-views-with-model-changes"></a><span data-ttu-id="b50d6-127">뷰 모델 변경 내용으로 업데이트</span><span class="sxs-lookup"><span data-stu-id="b50d6-127">Update Views with Model Changes</span></span>

<span data-ttu-id="b50d6-128">새 등급 열을 반영 하도록 템플릿 보기를 사용 하는 업데이트 수는 몇 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b50d6-128">There are a few ways we could update our view templates to reflect the new Rating column.</span></span> <span data-ttu-id="b50d6-129">뷰 추가 대화 상자를 통해이 생성 하 여 이러한 뷰를 만들었기 때문 없습니다 삭제 하 고 다시 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b50d6-129">Since we created these Views by generating them via the Add View dialog, we could delete them and recreate them again.</span></span> <span data-ttu-id="b50d6-130">그러나 일반적으로 사용자는 이미 수정 템플릿 해당 보기를 스 캐 폴드 된 초기 생성에서 및 추가 또는 만들기에 대 한 ID 필드를 사용 하 여 했던 것 처럼 수동으로, 방금 필드를 삭제 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d6-130">However, typically people will have already made modifications to their View templates from the initial scaffolded generation and will want to add or delete fields manually, just as we did with the ID field for Create.</span></span>

<span data-ttu-id="b50d6-131">\Views\Movies\Index.aspx 템플릿을 열고 추가 &lt;th&gt;등급&lt;/th&gt; Movie 테이블의 머리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b50d6-131">Open up the \Views\Movies\Index.aspx template and add a &lt;th&gt;Rating&lt;/th&gt; to the head of the Movie table.</span></span> <span data-ttu-id="b50d6-132">장르 후 마이닝를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b50d6-132">I added mine after Genre.</span></span> <span data-ttu-id="b50d6-133">그런 다음 동일한 열 위치에 있지만 아래의 새 등급을 출력 하는 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d6-133">Then, in the same column position but lower down, add a line to output our new Rating.</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample1.aspx)]

<span data-ttu-id="b50d6-134">최종 Index.aspx 템플릿은 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b50d6-134">Our final Index.aspx template will look like this:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample2.aspx)]

<span data-ttu-id="b50d6-135">보겠습니다 다음 \Views\Movies\Create.aspx 템플릿을 열고 새 등급 속성에 대 한 레이블 및 텍스트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d6-135">Let's then open up the \Views\Movies\Create.aspx template and add a Label and Textbox for our new Rating property:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample3.aspx)]

<span data-ttu-id="b50d6-136">최종 Create.aspx 템플릿은 이렇게 확인 하 고 브라우저의 제목 및 보조 데이터베이스를 변경해 보겠습니다 &lt;h2&gt; "만들기는 영화" 여기에 있는 동안 같이 제목!</span><span class="sxs-lookup"><span data-stu-id="b50d6-136">Our final Create.aspx template will look like this, and let's change our browser's title and secondary &lt;h2&gt; title to something like "Create a Movie" while we're in here!</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample4.aspx)]

<span data-ttu-id="b50d6-137">앱을 실행 하 고 만들기 페이지에 추가 된 데이터베이스에 새 필드를 완성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b50d6-137">Run your app and now you've got a new field in the database that's been added to the Create page.</span></span> <span data-ttu-id="b50d6-138">등급-이 이번-새 동영상을 추가 하 고 만들기를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d6-138">Add a new Movie - this time with a Rating - and click Create.</span></span>

<span data-ttu-id="b50d6-139">[![Windows Internet Explorer 동영상-만들기](getting-started-with-mvc-part8/_static/image9.png)](getting-started-with-mvc-part8/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="b50d6-139">[![Create a Movie - Windows Internet Explorer](getting-started-with-mvc-part8/_static/image9.png)](getting-started-with-mvc-part8/_static/image8.png)</span></span>

<span data-ttu-id="b50d6-140">인덱스 페이지에 전송 하 고 만들기를 클릭 하면 새 영화는와 함께 나열 하는 경우 데이터베이스에 새 등급 열</span><span class="sxs-lookup"><span data-stu-id="b50d6-140">After you click Create, you're sent to the Index page where you new Movie is listed with the new Rating Column in the database</span></span>

<span data-ttu-id="b50d6-141">[![영화 목록-Windows Internet Explorer (12)](getting-started-with-mvc-part8/_static/image11.png)](getting-started-with-mvc-part8/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="b50d6-141">[![Movie List - Windows Internet Explorer (12)](getting-started-with-mvc-part8/_static/image11.png)](getting-started-with-mvc-part8/_static/image10.png)</span></span>

<span data-ttu-id="b50d6-142">이 기본 자습서를 가져온 컨트롤러 뷰를 사용 하 여 연결 하 고 하드 코드 된 데이터를 전달 하기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d6-142">This basic tutorial got you started making Controllers, associating them with Views and passing around hard-coded data.</span></span> <span data-ttu-id="b50d6-143">생성 및 데이터베이스를 설계 하 고 일부 데이터를 저장 한 다음에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d6-143">Then we created and designed a Database and put some data it in.</span></span> <span data-ttu-id="b50d6-144">데이터베이스에서 데이터를 검색 하 고 HTML 테이블에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d6-144">We retrieved the data from the database and displayed it in an HTML table.</span></span> <span data-ttu-id="b50d6-145">그런 다음 데이터를 추가 데이터베이스 자체에서 웹 응용 프로그램 내에서 사용자는 양식 만들기를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b50d6-145">Then we added a Create form that let the user add data to the database themselves from within the Web Application.</span></span> <span data-ttu-id="b50d6-146">유효성 검사를 추가 하 고 JavaScript를 사용 하 여 클라이언트 쪽에서 유효성 검사를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d6-146">We added validation, then made the validation use JavaScript on the client-side.</span></span> <span data-ttu-id="b50d6-147">마지막으로 데이터를 새 열을 포함 하도록 데이터베이스를 변경 하 고 만들고이 새 데이터를 표시 하는 두 페이지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d6-147">Finally, we changed the database to include a new column of data, then updated our two pages to create and display this new data.</span></span>

<span data-ttu-id="b50d6-148">이 중급 자습서를 진행 이제 바랍니다 "[MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)" 다양 한 비디오 및 리소스 뿐만 아니라 [ https://asp.net/mvc ](https://asp.net/mvc) ASP.NET MVC에 대 한 더 자세한!</span><span class="sxs-lookup"><span data-stu-id="b50d6-148">I now encourage you to move on to our intermediate-level tutorial "[MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)" as well as the many videos and resources at [https://asp.net/mvc](https://asp.net/mvc) to learn even more about ASP.NET MVC!</span></span>

<span data-ttu-id="b50d6-149">즐겨보세요!</span><span class="sxs-lookup"><span data-stu-id="b50d6-149">Enjoy!</span></span>

- <span data-ttu-id="b50d6-150">-Scott Hanselman [ http://hanselman.com ](http://hanselman.com) 하 고 [ @shanselman ](http://twitter.com/shanselman) Twitter에서.</span><span class="sxs-lookup"><span data-stu-id="b50d6-150">Scott Hanselman - [http://hanselman.com](http://hanselman.com) and [@shanselman](http://twitter.com/shanselman) on Twitter.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="b50d6-151">이전</span><span class="sxs-lookup"><span data-stu-id="b50d6-151">Previous</span></span>](getting-started-with-mvc-part7.md)
