---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/updating-data
title: Introducing ASP.NET 웹 페이지-데이터베이스 데이터 업데이트 | Microsoft Docs
author: tfitzmac
description: 이 자습서에서는 ASP.NET 웹 페이지 (Razor)를 사용 하는 경우 (변경) 기존 데이터베이스 항목을 업데이트 하는 방법을 보여 줍니다. 계열을 완료 한 것으로 가정 번째...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/02/2018
ms.topic: article
ms.assetid: ac86ec9c-6b69-485b-b9e0-8b9127b13e6b
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/updating-data
msc.type: authoredcontent
ms.openlocfilehash: e889cd27e2267a08f7b6ea708c92e35edbdd7a1a
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="introducing-aspnet-web-pages---updating-database-data"></a><span data-ttu-id="538bb-104">Introducing ASP.NET 웹 페이지-데이터베이스 데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="538bb-104">Introducing ASP.NET Web Pages - Updating Database Data</span></span>
====================
<span data-ttu-id="538bb-105">으로 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="538bb-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="538bb-106">이 자습서에서는 ASP.NET 웹 페이지 (Razor)를 사용 하는 경우 (변경) 기존 데이터베이스 항목을 업데이트 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-106">This tutorial shows you how to update (change) an existing database entry when you use ASP.NET Web Pages (Razor).</span></span> <span data-ttu-id="538bb-107">통해 시리즈를 완료 한 것으로 가정 [데이터 입력 하 여 사용 하 여 양식을 사용 하 여 ASP.NET 웹 페이지](entering-data.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-107">It assumes you have completed the series through [Entering Data by Using Forms Using ASP.NET Web Pages](entering-data.md).</span></span>
> 
> <span data-ttu-id="538bb-108">학습 내용:</span><span class="sxs-lookup"><span data-stu-id="538bb-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="538bb-109">개별 레코드를 선택 하는 방법의 `WebGrid` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-109">How to select an individual record in the `WebGrid` helper.</span></span>
> - <span data-ttu-id="538bb-110">데이터베이스에서 단일 레코드를 읽을 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="538bb-110">How to read a single record from a database.</span></span>
> - <span data-ttu-id="538bb-111">데이터베이스 레코드의 값을 포함 하는 폼을 미리 로드 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="538bb-111">How to preload a form with values from the database record.</span></span>
> - <span data-ttu-id="538bb-112">데이터베이스의 기존 레코드를 업데이트 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-112">How to update an existing record in a database.</span></span>
> - <span data-ttu-id="538bb-113">페이지에 표시 하지 않고 정보를 저장 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="538bb-113">How to store information in the page without displaying it.</span></span>
> - <span data-ttu-id="538bb-114">정보를 저장 하 여 숨겨진된 필드를 사용 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-114">How to use a hidden field to store information.</span></span>
>   
> 
> <span data-ttu-id="538bb-115">기능/기술을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-115">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="538bb-116">`WebGrid` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-116">The `WebGrid` helper.</span></span>
> - <span data-ttu-id="538bb-117">SQL `Update` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-117">The SQL `Update` command.</span></span>
> - <span data-ttu-id="538bb-118">`Database.Execute` 메서드</span><span class="sxs-lookup"><span data-stu-id="538bb-118">The `Database.Execute` method.</span></span>
> - <span data-ttu-id="538bb-119">숨겨진 필드 (`<input type="hidden">`).</span><span class="sxs-lookup"><span data-stu-id="538bb-119">Hidden fields (`<input type="hidden">`).</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="538bb-120">만들 것인지</span><span class="sxs-lookup"><span data-stu-id="538bb-120">What You'll Build</span></span>

<span data-ttu-id="538bb-121">이전 자습서에서는 데이터베이스에 레코드를 추가 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-121">In the previous tutorial, you learned how to add a record to a database.</span></span> <span data-ttu-id="538bb-122">여기에서는 편집을 위해 레코드를 표시 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-122">Here, you'll learn how to display a record for editing.</span></span> <span data-ttu-id="538bb-123">에 *동영상* 업데이트 합니다 페이지는 `WebGrid` 도우미를 표시 하도록는 **편집** 각 영화 옆에 있는 링크:</span><span class="sxs-lookup"><span data-stu-id="538bb-123">In the *Movies* page, you'll update the `WebGrid` helper so that it displays an **Edit** link next to each movie:</span></span>

![WebGrid 각 동영상에 대 한 '편집' 링크를 포함 하 여 표시](updating-data/_static/image1.png)

<span data-ttu-id="538bb-125">클릭는 **편집** 링크를 걸리는 다른 페이지로 영화 정보를 양식에 이미 여기서:</span><span class="sxs-lookup"><span data-stu-id="538bb-125">When you click the **Edit** link, it takes you to a different page, where the movie information is already in a form:</span></span>

![동영상을 편집할 수를 보여 주는 동영상 페이지 편집](updating-data/_static/image2.png)

<span data-ttu-id="538bb-127">값 중 하나를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-127">You can change any of the values.</span></span> <span data-ttu-id="538bb-128">변경 내용을 제출 하면 코드 페이지에는 데이터베이스가 업데이트 되 고 영화 목록으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-128">When you submit the changes, the code in the page updates the database and takes you back to the movie listing.</span></span>

<span data-ttu-id="538bb-129">이 부분의 프로세스와 거의 정확 하 게 작동는 *AddMovie.cshtml* 익숙할 것이 자습서의 많은 하므로 이전 자습서에서 만든 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-129">This part of the process works almost exactly like the *AddMovie.cshtml* page you created in the previous tutorial, so much of this tutorial will be familiar.</span></span>

<span data-ttu-id="538bb-130">여러 가지 방법으로 개별 영화를 편집 하는 기능을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-130">There are several ways you could implement a way to edit an individual movie.</span></span> <span data-ttu-id="538bb-131">보여준 방식은 구현 하기 쉽고 이해 하기 쉬운 이기 때문에 선택 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-131">The approach shown was chosen because it's easy to implement and easy to understand.</span></span>

## <a name="adding-an-edit-link-to-the-movie-listing"></a><span data-ttu-id="538bb-132">편집 링크가 영화 목록에 추가</span><span class="sxs-lookup"><span data-stu-id="538bb-132">Adding an Edit Link to the Movie Listing</span></span>

<span data-ttu-id="538bb-133">를 시작 하려면 업데이트 합니다는 *동영상* 도 나열 하는 각 영화 포함 되도록 페이지는 **편집** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-133">To begin, you'll update the *Movies* page so that each movie listing also contains an **Edit** link.</span></span>

<span data-ttu-id="538bb-134">열기는 *Movies.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-134">Open the *Movies.cshtml* file.</span></span>

<span data-ttu-id="538bb-135">페이지 본문에서 변경 된 `WebGrid` 열을 추가 하 여는 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-135">In the body of the page, change the `WebGrid` markup by adding a column.</span></span> <span data-ttu-id="538bb-136">수정 된 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-136">Here's the modified markup:</span></span>

[!code-html[Main](updating-data/samples/sample1.html?highlight=6)]

<span data-ttu-id="538bb-137">새 열이이 하나가:</span><span class="sxs-lookup"><span data-stu-id="538bb-137">The new column is this one:</span></span>

[!code-html[Main](updating-data/samples/sample2.html)]

<span data-ttu-id="538bb-138">이 열의 지점 한 링크를 표시 하는 것 (`<a>` 요소) 이라고 표시 된 "편집"입니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-138">The point of this column is to show a link (`<a>` element) whose text says "Edit".</span></span> <span data-ttu-id="538bb-139">이 페이지를 실행 하는 경우 다음과 같이 표시 하는 링크를 만드는 것 후 우리가와 `id` 각 동영상에 대 한 다른 값:</span><span class="sxs-lookup"><span data-stu-id="538bb-139">What we're after is to create a link that looks like the following when the page runs, with the `id` value different for each movie:</span></span>

[!code-css[Main](updating-data/samples/sample3.css)]

<span data-ttu-id="538bb-140">이 링크는 라는 페이지 호출 *EditMovie*, 쿼리 문자열을 전달 합니다 `?id=7` 해당 페이지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-140">This link will invoke a page named *EditMovie*, and it will pass the query string `?id=7` to that page.</span></span>

<span data-ttu-id="538bb-141">새 열에 대 한 구문 약간 복잡 하 게 보일 수 있지만 몇 가지 요소가 함께 배치 하기 때문에.</span><span class="sxs-lookup"><span data-stu-id="538bb-141">The syntax for the new column might look a bit complex, but that's only because it puts together several elements.</span></span> <span data-ttu-id="538bb-142">각 개별 요소는 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-142">Each individual element is straightforward.</span></span> <span data-ttu-id="538bb-143">에 집중 하는 경우 테이블만 `<a>` 요소를이 태그를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-143">If you concentrate on just the `<a>` element, you see this markup:</span></span>

[!code-html[Main](updating-data/samples/sample4.html)]

<span data-ttu-id="538bb-144">눈금의 작동 방법에 대 한 배경 지식이: 각 필드에 대 한 열 데이터베이스 레코드에 표시 되며 표에 각 데이터베이스 레코드에 대 한 행이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-144">Some background about how the grid works: the grid displays rows, one for each database record, and it displays columns for each field in the database record.</span></span> <span data-ttu-id="538bb-145">각 표 형태 창의 행 생성 되는 동안는 `item` 해당 행에 대해 데이터베이스 레코드 (항목)를 포함 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-145">While each grid row is being constructed, the `item` object contains the database record (item) for that row.</span></span> <span data-ttu-id="538bb-146">이 정렬에 해당 행에 대 한 데이터를 가져오려고 코드에는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-146">This arrangement gives you a way in code to get at the data for that row.</span></span> <span data-ttu-id="538bb-147">즉, 여기: 식 `item.ID` 은 현재 데이터베이스 항목의 ID 값을 가져오는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-147">That's what you see here: the expression `item.ID` is getting the ID value of the current database item.</span></span> <span data-ttu-id="538bb-148">나타날 수 있습니다 (제목, genre 또는 년) 데이터베이스 값이 하나라도 같은 방법으로 사용 하 여 `item.Title`, `item.Genre`, 또는 `item.Year`합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-148">You could get any of the database values (title, genre, or year) the same way by using `item.Title`, `item.Genre`, or `item.Year`.</span></span>

<span data-ttu-id="538bb-149">식 `"~/EditMovie?id=@item.ID` 대상 URL의 하드 코드 된 부분을 결합 (`~/EditMovie?id=`)이 동적으로 파생 id</span><span class="sxs-lookup"><span data-stu-id="538bb-149">The expression `"~/EditMovie?id=@item.ID` combines the hard-coded part of the target URL (`~/EditMovie?id=`) with this dynamically derived ID.</span></span> <span data-ttu-id="538bb-150">(언급 했 듯이 `~` 이전 자습서; 연산자는 현재 웹 사이트 루트를 나타내는 ASP.NET 연산자입니다.)</span><span class="sxs-lookup"><span data-stu-id="538bb-150">(You saw the `~` operator in the previous tutorial; it's an ASP.NET operator that represents the current website root.)</span></span>

<span data-ttu-id="538bb-151">그 결과 열에는 태그의이 부분 하기만 하면 다음 태그와 같은 런타임에 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-151">The result is that this part of the markup in the column simply produces something like the following markup at run time:</span></span>

[!code-xml[Main](updating-data/samples/sample5.xml)]

<span data-ttu-id="538bb-152">실제 값 당연히 `id` 각 행에 대해 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-152">Naturally, the actual value of `id` will be different for each row.</span></span>

## <a name="creating-a-custom-display-for-a-grid-column"></a><span data-ttu-id="538bb-153">표 형태 창의 열에 대 한 디스플레이 사용자 지정 만들기</span><span class="sxs-lookup"><span data-stu-id="538bb-153">Creating a Custom Display for a Grid Column</span></span>

<span data-ttu-id="538bb-154">표 형태 창의 열에 다시 이제입니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-154">Now back to the grid column.</span></span> <span data-ttu-id="538bb-155">세 개의 열 원래 표가 표시 된 데이터 값만 (제목, genre 및 년)에 했습니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-155">The three columns you originally had in the grid displayed only data values (title, genre, and year).</span></span> <span data-ttu-id="538bb-156">이 표시는 데이터베이스 열의 이름을 전달 하 여 지정한 &mdash; 예를 들어 `grid.Column("Title")`합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-156">You specified this display by passing the name of the database column &mdash; for example, `grid.Column("Title")`.</span></span>

<span data-ttu-id="538bb-157">이 새로운 **편집** 링크 열은 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-157">This new **Edit** link column is different.</span></span> <span data-ttu-id="538bb-158">열 이름을 지정 하는 대신 전달 된 `format` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-158">Instead of specifying a column name, you're passing a `format` parameter.</span></span> <span data-ttu-id="538bb-159">이 매개 변수를 사용 하면 태그를 정의할 수 있는 `WebGrid` 도우미와 함께 렌더링 합니다는 `item` 굵게 또는 녹색 열 데이터를 표시 하거나 원하는 원하는 형식으로 해당 값을 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-159">This parameter lets you define markup that the `WebGrid` helper will render along with the `item` value to display the column data as bold or green or in whatever format that you want.</span></span> <span data-ttu-id="538bb-160">예를 들어 제목을 굵게 표시 하려는 경우이 예제에서와 같이 열을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-160">For example, if you wanted the title to appear bold, you could create a column like this example:</span></span>

[!code-html[Main](updating-data/samples/sample6.html)]

<span data-ttu-id="538bb-161">(다양 한 `@` 문자에서 참조 된 `format` 속성의 전환 태그 및 코드 값을 표시 합니다.)</span><span class="sxs-lookup"><span data-stu-id="538bb-161">(The various `@` characters you see in the `format` property mark the transition between markup and a code value.)</span></span>

<span data-ttu-id="538bb-162">에 대 한 것을 알고 있다면는 `format` 은 쉽게 이해할 수 있도록 속성을 어떻게 새 **편집** 링크 열이 함께 저장 됩니다:</span><span class="sxs-lookup"><span data-stu-id="538bb-162">Once you know about the `format` property, it's easier to understand how the new **Edit** link column is put together:</span></span>

[!code-html[Main](updating-data/samples/sample7.html)]

<span data-ttu-id="538bb-163">열 구성 *만* 의 링크를 렌더링 하는 태그를 몇 가지 정보 (ID)와 하에서 추출 되는 행에 대 한 데이터베이스 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-163">The column consists *only* of the markup that renders the link, plus some information (the ID) that's extracted from the database record for the row.</span></span>

> [!TIP]
> 
> <span data-ttu-id="538bb-164">**명명 된 매개 변수 및 메서드에 대 한 위치 매개 변수**</span><span class="sxs-lookup"><span data-stu-id="538bb-164">**Named Parameters and Positional Parameters for a Method**</span></span>
> 
> <span data-ttu-id="538bb-165">여러 번 메서드 호출을 매개 변수 전달, 단순히 나열 쉼표로 구분 하 여 매개 변수 값입니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-165">Many times when you've called a method and passed parameters to it, you've simply listed the parameter values separated by commas.</span></span> <span data-ttu-id="538bb-166">몇 가지 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-166">Here are a couple of examples:</span></span>
> 
> `db.Execute(insertCommand, title, genre, year)`
> 
> `Validation.RequireField("title", "You must enter a title")`
> 
> <span data-ttu-id="538bb-167">먼저이 코드를 표시 하지만 각각의 경우에서에 특정 순서로 관계 매개 변수를 전달 하는 경우 문제가 언급 하지 않은 &mdash; 메서드에 정의 되어 있는 매개 변수 순서 즉, 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-167">We didn't mention the issue when you first saw this code, but in each case, you're passing parameters to the methods in a specific order &mdash; namely, the order in which the parameters are defined in that method.</span></span> <span data-ttu-id="538bb-168">에 대 한 `db.Execute` 및 `Validation.RequireFields`, 페이지를 실행할 때 오류 메시지가 나타나거나 이상한 결과 이상 얻을 전달 하는 값의 순서를 혼합 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="538bb-168">For `db.Execute` and `Validation.RequireFields`, if you mixed up the order of the values you pass, you'd get an error message when the page runs, or at least some strange results.</span></span> <span data-ttu-id="538bb-169">명확 하 게 매개 변수를 전달 하는 순서를 파악 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-169">Clearly, you have to know the order to pass the parameters in.</span></span> <span data-ttu-id="538bb-170">(WebMatrix에서 IntelliSense 문의할 수 있습니다 이름, 형식 및 매개 변수의 순서를 확인 합니다.)</span><span class="sxs-lookup"><span data-stu-id="538bb-170">(In WebMatrix, IntelliSense can help you learn figure out the name, type, and order of the parameters.)</span></span>
> 
> <span data-ttu-id="538bb-171">을 순서 대로 값을 전달 하는 대신 사용 하 여 *명명 된 매개 변수*합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-171">As an alternative to passing values in order, you can use *named parameters*.</span></span> <span data-ttu-id="538bb-172">(사용 하 여 라고 순서로 매개 변수를 전달 *위치 매개 변수*.) 명명 된 매개 변수에 대 한 명시적으로 포함 매개 변수 이름을 해당 값을 전달 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="538bb-172">(Passing parameters in order is known as using *positional parameters*.) For named parameters, you explicitly include the name of the parameter when passing its value.</span></span> <span data-ttu-id="538bb-173">명명 된 매개 변수가 이미 여러 번에서에서 사용한 이러한 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-173">You've used named parameters already a number of times in these tutorials.</span></span> <span data-ttu-id="538bb-174">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="538bb-174">For example:</span></span>
> 
> [!code-csharp[Main](updating-data/samples/sample8.cs)]
> 
> <span data-ttu-id="538bb-175">를 갖는</span><span class="sxs-lookup"><span data-stu-id="538bb-175">and</span></span>
> 
> [!code-css[Main](updating-data/samples/sample9.css)]
> 
> <span data-ttu-id="538bb-176">명명 된 매개 변수는 메서드가 많은 매개 변수를 사용 하는 경우에 특히는 몇 가지 상황에서 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-176">Named parameters are handy for a couple of situations, especially when a method takes many parameters.</span></span> <span data-ttu-id="538bb-177">한 개나 두 개의 매개 변수를 전달 하려면 하지만 전달 하려는 값이 매개 변수 목록에서 첫 번째 위치 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-177">One is when you want to pass only one or two parameters, but the values you want to pass are not among the first positions in the parameter list.</span></span> <span data-ttu-id="538bb-178">가장 적합 하는 순서로 매개 변수를 전달 하 여 코드를 더 쉽게 읽을 수 있도록 하려면 다른 상황이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-178">Another situation is when you want to make your code more readable by passing the parameters in the order that makes the most sense to you.</span></span>
> 
> <span data-ttu-id="538bb-179">물론, 명명 된 매개 변수를 사용 해야 매개 변수 이름을 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-179">Obviously, to use named parameters, you have to know the names of the parameters.</span></span> <span data-ttu-id="538bb-180">WebMatrix IntelliSense 수 *표시* 의 이름, 하지만 없습니다 현재 양식으로 있습니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-180">WebMatrix IntelliSense can *show* you the names, but it cannot currently fill them in for you.</span></span>


## <a name="creating-the-edit-page"></a><span data-ttu-id="538bb-181">편집 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="538bb-181">Creating the Edit Page</span></span>

<span data-ttu-id="538bb-182">이제 만들 수는 *EditMovie* 페이지.</span><span class="sxs-lookup"><span data-stu-id="538bb-182">Now you can create the *EditMovie* page.</span></span> <span data-ttu-id="538bb-183">사용자가 클릭 하면는 **편집** 링크를 합니다 결국이 페이지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-183">When users click the **Edit** link, they'll end up on this page.</span></span>

<span data-ttu-id="538bb-184">*EditMovie.cshtml* 바꾸고 다음 태그를 사용 하 여 파일에 포함 된 내용:</span><span class="sxs-lookup"><span data-stu-id="538bb-184">Create a page named *EditMovie.cshtml* and replace what's in the file with the following markup:</span></span>

[!code-cshtml[Main](updating-data/samples/sample10.cshtml)]

<span data-ttu-id="538bb-185">이 태그와 코드에 있는 것과 비슷합니다는 *AddMovie* 페이지.</span><span class="sxs-lookup"><span data-stu-id="538bb-185">This markup and code is similar to what you have in the *AddMovie* page.</span></span> <span data-ttu-id="538bb-186">제출 단추에 대 한 텍스트에 약간의 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-186">There's a small difference in the text for the submit button.</span></span> <span data-ttu-id="538bb-187">과 마찬가지로 *AddMovie* 페이지, 즉는 `Html.ValidationSummary` 되어 있는 경우 유효성 검사 오류를 표시 하는 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-187">As with the *AddMovie* page, there's an `Html.ValidationSummary` call that will display validation errors if there are any.</span></span> <span data-ttu-id="538bb-188">에 대 한 호출을 제외 하는 것이 시간 `Validation.Message`이므로 유효성 검사 요약에 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-188">This time we're leaving out calls to `Validation.Message`, since errors will be displayed in the validation summary.</span></span> <span data-ttu-id="538bb-189">이전 자습서에서 설명한 대로, 다양 한 조합에서 유효성 검사 요약 및 개별 오류 메시지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-189">As noted in the previous tutorial, you can use the validation summary and the individual error messages in various combinations.</span></span>

<span data-ttu-id="538bb-190">다시 확인 하는 `method` 특성에는 `<form>` 로 설정 된 `post`합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-190">Notice again that the `method` attribute of the `<form>` element is set to `post`.</span></span> <span data-ttu-id="538bb-191">과 마찬가지로 *AddMovie.cshtml* 페이지에서이 페이지를 수정 하는 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-191">As with the *AddMovie.cshtml* page, this page makes changes to the database.</span></span> <span data-ttu-id="538bb-192">따라서이 폼을 수행 해야는 `POST` 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-192">Therefore, this form should perform a `POST` operation.</span></span> <span data-ttu-id="538bb-193">(간의 차이 대 한 자세한 `GET` 및 `POST` 작업의 경우 참조는 [GET, POST 및 HTTP 동사 안전](form-basics.md#GET,_POST,_and_HTTP_Verb_Safety) HTML 폼에 대 한 자습서에서 사이드바.)</span><span class="sxs-lookup"><span data-stu-id="538bb-193">(For more about the difference between `GET` and `POST` operations, see the [GET, POST, and HTTP Verb Safety](form-basics.md#GET,_POST,_and_HTTP_Verb_Safety) sidebar in the tutorial on HTML forms.)</span></span>

<span data-ttu-id="538bb-194">이전 자습서에서 볼 수 있듯이 `value` 텍스트 상자의 특성을 미리 설치 하기 위해 Razor 코드로 설정 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-194">As you saw in an earlier tutorial, the `value` attributes of the text boxes are being set with Razor code in order to preload them.</span></span> <span data-ttu-id="538bb-195">이 시간 하지만 사용 하는 같은 변수 `title` 및 `genre` 대신 해당 작업에 대해 `Request.Form["title"]`:</span><span class="sxs-lookup"><span data-stu-id="538bb-195">This time, though, you're using variables like `title` and `genre` for that task instead of `Request.Form["title"]`:</span></span>

`<input type="text" name="title" value="@title" />`

<span data-ttu-id="538bb-196">로 이전에이 태그는 미리 로드 하는 텍스트 상자 값과 영화 값.</span><span class="sxs-lookup"><span data-stu-id="538bb-196">As before, this markup will preload the text box values with the movie values.</span></span> <span data-ttu-id="538bb-197">사용 하는 대신이 시간 변수를 사용 하는 편리한 이유는 잠시 후에 표시 됩니다는 `Request` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-197">You'll see in a moment why it's handy to use variables this time instead of using the `Request` object.</span></span>

<span data-ttu-id="538bb-198">또한 한 `<input type="hidden">` 이 페이지의 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-198">There's also a `<input type="hidden">` element on this page.</span></span> <span data-ttu-id="538bb-199">이 요소는 페이지에 표시 하지 영화 ID를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-199">This element stores the movie ID without making it visible on the page.</span></span> <span data-ttu-id="538bb-200">ID가 처음 페이지에 전달 하 여 쿼리 문자열 값을 사용 하 여 (`?id=7` 또는 유사한 URL에).</span><span class="sxs-lookup"><span data-stu-id="538bb-200">The ID is initially passed to the page by using a query string value (`?id=7` or similar in the URL).</span></span> <span data-ttu-id="538bb-201">숨겨진된 필드에는 ID 값을 설정 하 여 사용할 수 있는지 가능 페이지로 호출 되었으므로 원래 URL에 대 한 액세스를 더 이상 있는 경우에, 폼 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-201">By putting the ID value into a hidden field, you can make sure that it's available when the form is submitted, even if you no longer have access to the original URL that the page was invoked with.</span></span>

<span data-ttu-id="538bb-202">와 달리는 *AddMovie* 에 대 한 코드 페이지는 *EditMovie* 페이지에 두 가지 고유 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-202">Unlike the *AddMovie* page, the code for the *EditMovie* page has two distinct functions.</span></span> <span data-ttu-id="538bb-203">첫 번째 함수는 페이지가 처음으로 표시 될 때 (및 *만* 후), 코드 쿼리 문자열에서 영화 ID를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-203">The first function is that when the page is displayed for the first time (and *only* then), the code gets the movie ID from the query string.</span></span> <span data-ttu-id="538bb-204">다음 코드를 사용 하 여 ID 데이터베이스에서 해당 영화를 읽고 표시 하 (미리 로드)이 있는 텍스트 상자에.</span><span class="sxs-lookup"><span data-stu-id="538bb-204">The code then uses the ID to read the corresponding movie out of the database and display (preload) it in the text boxes.</span></span>

<span data-ttu-id="538bb-205">두 번째 함수는 사용자가 클릭 하 여 **변경 내용 전송** 단추를 코드에는 입력란의 값을 읽고의 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-205">The second function is that when the user clicks the **Submit Changes** button, the code has to read the values of the text boxes and validate them.</span></span> <span data-ttu-id="538bb-206">코드는 또한 데이터베이스 항목을 새 값으로 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-206">The code also has to update the database item with the new values.</span></span> <span data-ttu-id="538bb-207">이 방법은 레코드를 증가 시킬에서 볼 수 있듯이 *AddMovie*합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-207">This technique is similar to adding a record, as you saw in *AddMovie*.</span></span>

## <a name="adding-code-to-read-a-single-movie"></a><span data-ttu-id="538bb-208">단일 영화를 읽는 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-208">Adding Code to Read a Single Movie</span></span>

<span data-ttu-id="538bb-209">첫 번째 함수를 수행 하려면이 코드 페이지의 맨 위에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-209">To perform the first function, add this code to the top of the page:</span></span>

[!code-cshtml[Main](updating-data/samples/sample11.cshtml)]

<span data-ttu-id="538bb-210">이 코드의 대부분은 시작 되는 블록 안에 `if(!IsPost)`합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-210">Most of this code is inside a block that starts `if(!IsPost)`.</span></span> <span data-ttu-id="538bb-211">`!` 연산자 의미 "not" 식 의미 하므로 *이 요청이 post 제출 없으면*, 방법도 간접 방법 *이 요청은 처음으로이 페이지를 실행 하는 경우*합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-211">The `!` operator means "not," so the expression means *if this request is not a post submission*, which is an indirect way of saying *if this request is the first time that this page has been run*.</span></span> <span data-ttu-id="538bb-212">이 코드를 실행 해야 듯이 *만* 처음으로 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-212">As noted earlier, this code should run *only* the first time the page runs.</span></span> <span data-ttu-id="538bb-213">코드를 포함 하지 않은 경우 `if(!IsPost)`, 페이지가 호출 될 때마다, 여부 처음으로 실행 거 나 단추에 대 한 응답에서를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-213">If you didn't enclose the code in `if(!IsPost)`, it would run every time the page is invoked, whether the first time or in response to a button click.</span></span>

<span data-ttu-id="538bb-214">코드에는 `else` 이 시간을 차단 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-214">Notice that the code includes an `else` block this time.</span></span> <span data-ttu-id="538bb-215">도입 여기서 설명한 것 처럼 `if` 경우도 테스트 하는 조건이 true 없는 경우 대체 코드를 실행 하려면 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-215">As we said when we introduced `if` blocks, sometimes you want to run alternative code if the condition you're testing isn't true.</span></span> <span data-ttu-id="538bb-216">여기서입니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-216">That's the case here.</span></span> <span data-ttu-id="538bb-217">조건 (즉, 경우 페이지에 전달 된 ID 확인)를 통과 하면 데이터베이스에서 행을 읽을 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-217">If the condition passes (that is, if the ID passed to the page is ok), you read a row from the database.</span></span> <span data-ttu-id="538bb-218">그러나 조건을 통과 하지 못한 경우는 `else` 블록 실행 및 코드 오류 메시지를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-218">However, if the condition doesn't pass, the `else` block runs and the code sets an error message.</span></span>

## <a name="validating-a-value-passed-to-the-page"></a><span data-ttu-id="538bb-219">페이지에 전달 되는 값의 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="538bb-219">Validating a Value Passed to the Page</span></span>

<span data-ttu-id="538bb-220">코드를 사용 하 여 `Request.QueryString["id"]` 페이지에 전달 되는 ID를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-220">The code uses `Request.QueryString["id"]` to get the ID that's passed to the page.</span></span> <span data-ttu-id="538bb-221">코드를 통해 ID에 대 한 값을 전달 된 실제로</span><span class="sxs-lookup"><span data-stu-id="538bb-221">The code makes sure that a value was actually passed for the ID.</span></span> <span data-ttu-id="538bb-222">값이 전달 된 경우 코드 유효성 검사 오류를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-222">If no value was passed, the code sets a validation error.</span></span>

<span data-ttu-id="538bb-223">이 코드에 정보의 유효성을 검사 하는 다른 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-223">This code shows a different way to validate information.</span></span> <span data-ttu-id="538bb-224">이전 자습서에서 사용한는 `Validation` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-224">In the previous tutorial, you worked with the `Validation` helper.</span></span> <span data-ttu-id="538bb-225">확인을 위해 필드를 등록 하 고 ASP.NET에서 자동으로 유효성 검사를가 하 고 사용 하 여 오류를 표시 `Html.ValidationMessage` 및 `Html.ValidationSummary`합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-225">You registered fields to validate, and ASP.NET automatically did the validation and displayed errors by using `Html.ValidationMessage` and `Html.ValidationSummary`.</span></span> <span data-ttu-id="538bb-226">그러나이 경우 있습니다 하는 것은 아닙니다 사용자 입력 유효성 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-226">In this case, however, you're not really validating user input.</span></span> <span data-ttu-id="538bb-227">대신, 다른 위치에서 페이지에 전달 된 값의 유효성 검사 중인 있습니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-227">Instead, you're validating a value that was passed to the page from elsewhere.</span></span> <span data-ttu-id="538bb-228">`Validation` 도우미 하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-228">The `Validation` helper doesn't do that for you.</span></span>

<span data-ttu-id="538bb-229">따라서 체크 값을 직접 사용 하 여 테스트 하 여 `if(!Request.QueryString["ID"].IsEmpty()`).</span><span class="sxs-lookup"><span data-stu-id="538bb-229">Therefore, you check the value yourself, by testing it with `if(!Request.QueryString["ID"].IsEmpty()`).</span></span> <span data-ttu-id="538bb-230">문제가 있는 경우 사용 하 여 오류를 표시할 수 있습니다 `Html.ValidationSummary`에서와 마찬가지로는 `Validation` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-230">If there's a problem, you can display the error by using `Html.ValidationSummary`, as you did with the `Validation` helper.</span></span> <span data-ttu-id="538bb-231">이러한 파일을 호출 하면 `Validation.AddFormError` 표시할 메시지를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-231">To do that, you call `Validation.AddFormError` and pass it a message to display.</span></span> <span data-ttu-id="538bb-232">`Validation.AddFormError` 익숙한 이미 유효성 검사 시스템을 사용 하 여 일치 하는 사용자 지정 메시지를 정의할 수 있도록 하는 기본 제공 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-232">`Validation.AddFormError` is a built-in method that lets you define custom messages that tie in with the validation system you're already familiar with.</span></span> <span data-ttu-id="538bb-233">(이 자습서의 뒷부분에 나오는 알아보겠습니다이 유효성 검사 프로세스를 좀 더 강력 하 게 하는 방법에 대 한.)</span><span class="sxs-lookup"><span data-stu-id="538bb-233">(Later in this tutorial we'll talk about how to make this validation process a little more robust.)</span></span>

<span data-ttu-id="538bb-234">동영상에 대 한 ID가 있는지에 확인 한 후 코드는 단일 데이터베이스 항목을 찾는 데이터베이스를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-234">After making sure that there's an ID for the movie, the code reads the database, looking for only a single database item.</span></span> <span data-ttu-id="538bb-235">(아마도 데이터베이스 작업에 대 한 일반적인 패턴 보았을: 데이터베이스를 열고 SQL 문을 정의 하는 문을 실행 합니다.) 이 이번에는 SQL `Select` 문에 포함 `WHERE ID = @0`합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-235">(You probably have noticed the general pattern for database operations: open the database, define a SQL statement, and run the statement.) This time, the SQL `Select` statement includes `WHERE ID = @0`.</span></span> <span data-ttu-id="538bb-236">ID가 고유 하므로 하나의 레코드를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-236">Because the ID is unique, only one record can be returned.</span></span>

<span data-ttu-id="538bb-237">쿼리를 사용 하 여 수행할 `db.QuerySingle` (하지 `db.Query`영화 목록에 사용한 것과,), 코드 결과를 하 고는 `row` 변수.</span><span class="sxs-lookup"><span data-stu-id="538bb-237">The query is performed by using `db.QuerySingle` (not `db.Query`, as you used for the movie listing), and the code puts the result into the `row` variable.</span></span> <span data-ttu-id="538bb-238">이름 `row` 는 임의로 지정; 변수를 원하는 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-238">The name `row` is arbitrary; you can name the variables anything you like.</span></span> <span data-ttu-id="538bb-239">변수를 위쪽에 초기화 이러한 값 텍스트 상자에 표시 될 수 있도록 다음 영화 세부 정보로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-239">The variables initialized at the top are then filled with the movie details so that these values can be displayed in the text boxes.</span></span>

## <a name="testing-the-edit-page-so-far"></a><span data-ttu-id="538bb-240">테스트 편집 페이지 (지금까지)</span><span class="sxs-lookup"><span data-stu-id="538bb-240">Testing the Edit Page (So Far)</span></span>

<span data-ttu-id="538bb-241">페이지를 테스트 하려는 경우 실행는 *동영상* 이제 페이지 클릭 하 여 프로그램 **편집** 모든 동영상 옆에 있는 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-241">If you'd like to test your page, run the *Movies* page now and click an **Edit** link next to any movie.</span></span> <span data-ttu-id="538bb-242">표시는 *EditMovie* 선택한 영화 세부 정보를 사용 하는 페이지 시간이 입력:</span><span class="sxs-lookup"><span data-stu-id="538bb-242">You'll see the *EditMovie* page with the details filled in for the movie you selected:</span></span>

![동영상을 편집할 수를 보여 주는 동영상 페이지 편집](updating-data/_static/image3.png)

<span data-ttu-id="538bb-244">페이지의 URL 같이 `?id=10` (또는 다른 몇 가지 번호)입니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-244">Notice that the URL of the page includes something like `?id=10` (or some other number).</span></span> <span data-ttu-id="538bb-245">테스트 했지만 지금까지 **편집** 에서는 정적으로 연결의 *영화* 작업 시간, 페이지 ID는 쿼리 문자열에서 읽고 단일 동영상 레코드를 가져올 데이터베이스 쿼리 한다고 되어 작동 하 고 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-245">So far you've tested that **Edit** links in the *Movie* page work, that your page is reading the ID from the query string, and that the database query to get a single movie record is working.</span></span>

<span data-ttu-id="538bb-246">영화 정보를 변경할 수 있지만 클릭할 때 아무 작업도 수행 **변경 내용 전송**합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-246">You can change the movie information, but nothing happens when you click **Submit Changes**.</span></span>

## <a name="adding-code-to-update-the-movie-with-the-users-changes"></a><span data-ttu-id="538bb-247">동영상 사용자의 변경 내용으로 업데이트 하는 코드 추가</span><span class="sxs-lookup"><span data-stu-id="538bb-247">Adding Code to Update the Movie with the User's Changes</span></span>

<span data-ttu-id="538bb-248">에 *EditMovie.cshtml* 파일, 두 번째 함수 (변경 내용 저장)을 구현 하려면 추가 바로의 닫는 중괄호 안에 다음 코드는 `@` 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-248">In the *EditMovie.cshtml* file, to implement the second function (saving changes), add the following code just inside the closing brace of the `@` block.</span></span> <span data-ttu-id="538bb-249">(정확한 위치 코드를 잘 모르는 경우에 볼 수 있습니다는 [영화 편집 페이지에 대 한 전체 코드](#Complete_Page_Listing_for_EditMovie) 이 자습서의 끝에 나타나는.)</span><span class="sxs-lookup"><span data-stu-id="538bb-249">(If you're not sure exactly where to put the code, you can look at the [complete code listing for the Edit Movie page](#Complete_Page_Listing_for_EditMovie) that appears at the end of this tutorial.)</span></span>

[!code-csharp[Main](updating-data/samples/sample12.cs)]

<span data-ttu-id="538bb-250">이 태그와 코드 역시의 코드와 유사한 *AddMovie*합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-250">Again, this markup and code is similar to the code in *AddMovie*.</span></span> <span data-ttu-id="538bb-251">코드는는 `if(IsPost)` 이 코드는 사용자가 클릭할 때만 실행 되므로 차단는 **변경 내용 전송** 단추 &mdash; 즉 때 (및 경우에만) 폼이 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-251">The code is in an `if(IsPost)` block, because this code runs only when the user clicks the **Submit Changes** button &mdash; that is, when (and only when) the form has been posted.</span></span> <span data-ttu-id="538bb-252">이 경우 같은 테스트를 사용 하지 않는 `if(IsPost && Validation.IsValid())`-즉, 하지 통합할 두 테스트 모두 사용 하 여 and가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-252">In this case, you're not using a test like `if(IsPost && Validation.IsValid())`— that is, you're not combining both tests by using AND.</span></span> <span data-ttu-id="538bb-253">이 페이지에 먼저 생각 양식을 제출 하 여 인지 (`if(IsPost)`)만 다음 유효성 검사에 대 한 필드를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-253">In this page, you first determine whether there's a form submission (`if(IsPost)`), and only then register the fields for validation.</span></span> <span data-ttu-id="538bb-254">다음 유효성 검사 결과 테스트할 수 있습니다 (`if(Validation.IsValid()`).</span><span class="sxs-lookup"><span data-stu-id="538bb-254">Then you can test the validation results (`if(Validation.IsValid()`).</span></span> <span data-ttu-id="538bb-255">흐름은 약간 변경 된 *AddMovie.cshtml* 페이지 다르지만 효과 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-255">The flow is slightly different than in the *AddMovie.cshtml* page, but the effect is the same.</span></span>

<span data-ttu-id="538bb-256">사용 하 여 텍스트 상자의 값을 가져올 `Request.Form["title"]` 와 비슷한 코드를 다른 `<input>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-256">You get the values of the text boxes by using `Request.Form["title"]` and similar code for the other `<input>` elements.</span></span> <span data-ttu-id="538bb-257">이 이번에는 코드 가져옴을 영화 ID 숨겨진된 필드에서 확인할 수 (`<input type="hidden">`).</span><span class="sxs-lookup"><span data-stu-id="538bb-257">Notice that this time, the code gets the movie ID out of the hidden field (`<input type="hidden">`).</span></span> <span data-ttu-id="538bb-258">페이지에 처음으로 실행 하는 경우 코드 쿼리 문자열에서 ID를 가져왔습니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-258">When the page ran the first time, the code got the ID out of the query string.</span></span> <span data-ttu-id="538bb-259">쿼리 문자열 조금 이라도 그 이후에 변경 된 경우 원래 표시 된 동영상의 ID를 가져오는 중인 되도록 숨겨진된 필드의 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-259">You get the value from the hidden field to make sure that you're getting the ID of the movie that was originally displayed, in case the query string was somehow altered since then.</span></span>

<span data-ttu-id="538bb-260">실제로 중요 한 차이점은 *AddMovie* 코드 및이 코드는이 코드에서 사용 하는 SQL `Update` 문 대신는 `Insert Into` 문.</span><span class="sxs-lookup"><span data-stu-id="538bb-260">The really important difference between the *AddMovie* code and this code is that in this code you use the SQL `Update` statement instead of the `Insert Into` statement.</span></span> <span data-ttu-id="538bb-261">다음 예제에서는 SQL 구문의 `Update` 문:</span><span class="sxs-lookup"><span data-stu-id="538bb-261">The following example shows the syntax of the SQL `Update` statement:</span></span>

`UPDATE table SET col1="value", col2="value", col3="value" ... WHERE ID = value`

<span data-ttu-id="538bb-262">순서에 관계 없이 모든 열을 지정할 수 있습니다 및 업데이트 하는 동안 모든 열 반드시 없는 `Update` 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-262">You can specify any columns in any order, and you don't necessarily have to update every column during an `Update` operation.</span></span> <span data-ttu-id="538bb-263">(을 업데이트할 수 없습니다 자체 ID로 새 레코드를 레코드를 저장 하는 적용는 및에 허용 되지 않습니다는 `Update` 작업 합니다.)</span><span class="sxs-lookup"><span data-stu-id="538bb-263">(You cannot update the ID itself, because that would in effect save the record as a new record, and that's not allowed for an `Update` operation.)</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="538bb-264">**중요 한** 는 `Where` 데이터베이스는 데이터베이스를 인식 하는 방법 이기 때문에 ID 가진 절이 매우 중요 레코드 업데이트 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-264">**Important** The `Where` clause with the ID is very important, because that's how the database knows which database record you want to update.</span></span> <span data-ttu-id="538bb-265">중단 된 경우는 `Where` 절, 데이터베이스를 업데이트 합니다 *모든* 데이터베이스에 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-265">If you left off the `Where` clause, the database would update *every* record in the database.</span></span> <span data-ttu-id="538bb-266">대부분의 경우에서 재해 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-266">In most cases, that would be a disaster.</span></span>


<span data-ttu-id="538bb-267">코드에서 자리 표시자를 사용 하 여 업데이트할 값을 SQL 문에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-267">In the code, the values to update are passed to the SQL statement by using placeholders.</span></span> <span data-ttu-id="538bb-268">반복 하기 전에 말한 것 무엇: 보안상의 이유로 *만* 자리 표시자를 사용 하 여 SQL 문을에 값을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-268">To repeat what we've said before: for security reasons, *only* use placeholders to pass values to a SQL statement.</span></span>

<span data-ttu-id="538bb-269">코드에서는 사용 후 `db.Execute` 실행 하는 `Update` 변경 내용을 볼 수 있는 목록 페이지를 다시 리디렉션합니다. 문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-269">After the code uses `db.Execute` to run the `Update` statement, it redirects back to the listing page, where you can see the changes.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="538bb-270">**다른 SQL 문을 여러 가지 방법**</span><span class="sxs-lookup"><span data-stu-id="538bb-270">**Different SQL Statements, Different Methods**</span></span>
> 
> <span data-ttu-id="538bb-271">약간 다른 방법을 사용 하 여 다른 SQL 문을 실행할 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-271">You might have noticed that you use slightly different methods to run different SQL statements.</span></span> <span data-ttu-id="538bb-272">실행 하는 `Select` 쿼리에서 잠재적으로 반환 여러 레코드를 사용 하는 `Query` 메서드.</span><span class="sxs-lookup"><span data-stu-id="538bb-272">To run a `Select` query that potentially returns multiple records, you use the `Query` method.</span></span> <span data-ttu-id="538bb-273">실행 하는 `Select` 쿼리를 하나의 데이터베이스 항목을 반환 합니다를 사용 하는 `QuerySingle` 메서드.</span><span class="sxs-lookup"><span data-stu-id="538bb-273">To run a `Select` query that you know will return only one database item, you use the `QuerySingle` method.</span></span> <span data-ttu-id="538bb-274">변경 하지만 데이터베이스 항목을 반환 하지 않는 하는 명령은 실행 하려면 사용 된 `Execute` 메서드.</span><span class="sxs-lookup"><span data-stu-id="538bb-274">To run commands that make changes but that don't return database items, you use the `Execute` method.</span></span>
> 
> <span data-ttu-id="538bb-275">차집합에 이미 본 것 처럼 각각 서로 다른 결과 반환 하기 때문에 다양 한 방법이 있어야 `Query` 및 `QuerySingle`합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-275">You have to have different methods because each of them returns different results, as you saw already in the difference between `Query` and `QuerySingle`.</span></span> <span data-ttu-id="538bb-276">(의 `Execute` 메서드 실제로 반환 값도 &mdash; 명령에 의해 영향을 받는 데이터베이스 행 수가 즉, &mdash; 있습니다 한 되었습니다 무시 하는 지금까지 하지만.)</span><span class="sxs-lookup"><span data-stu-id="538bb-276">(The `Execute` method actually returns a value also &mdash; namely, the number of database rows that were affected by the command &mdash; but you've been ignoring that so far.)</span></span>
> 
> <span data-ttu-id="538bb-277">물론,는 `Query` 메서드는 데이터베이스 행을 하나만 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-277">Of course, the `Query` method might return only one database row.</span></span> <span data-ttu-id="538bb-278">그러나 ASP.NET의 결과 항상 처리는 `Query` 메서드 컬렉션으로.</span><span class="sxs-lookup"><span data-stu-id="538bb-278">However, ASP.NET always treats the results of the `Query` method as a collection.</span></span> <span data-ttu-id="538bb-279">메서드가 하나의 행을 반환 하는 경우에 컬렉션에서 단일 행에는 추출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-279">Even if the method returns just one row, you have to extract that single row from the collection.</span></span> <span data-ttu-id="538bb-280">경우에 따라서 여기서 있습니다 *알고* 얻을 다시 행을 하나만, 사용 하는 편리한 방법을 다소 `QuerySingle`합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-280">Therefore, in situations where you *know* you'll get back only one row, it's a bit more convenient to use `QuerySingle`.</span></span>
> 
> <span data-ttu-id="538bb-281">특정 유형의 데이터베이스 작업을 수행 하는 다른 메서드를 몇 개 있습니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-281">There are a few other methods that perform specific types of database operations.</span></span> <span data-ttu-id="538bb-282">데이터베이스 메서드 목록을 찾을 수 있습니다는 [ASP.NET Web Pages API 빠른 참조](../../api-reference/asp-net-web-pages-api-reference.md#Data)합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-282">You can find a listing of database methods in the [ASP.NET Web Pages API Quick Reference](../../api-reference/asp-net-web-pages-api-reference.md#Data).</span></span>


## <a name="making-validation-for-the-id-more-robust"></a><span data-ttu-id="538bb-283">강력한 ID 등에 대 한 유효성 검사를 수행</span><span class="sxs-lookup"><span data-stu-id="538bb-283">Making Validation for the ID More Robust</span></span>

<span data-ttu-id="538bb-284">페이지를 실행 하는 처음으로 얻게 영화 ID는 쿼리 문자열에서 데이터베이스에서 해당 동영상 가져오기 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-284">The first time that the page runs, you get the movie ID from the query string so that you can go get that movie from the database.</span></span> <span data-ttu-id="538bb-285">실제로 했음을 검색할 이동 하려면이 코드를 사용 하 여 수행한 값 있는지 했습니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-285">You made sure that there actually was a value to go look for, which you did by using this code:</span></span>

[!code-csharp[Main](updating-data/samples/sample13.cs)]

<span data-ttu-id="538bb-286">되도록 하는 사용자가을 하는 경우이 코드를 사용는 *EditMovies* 에서 동영상을 먼저 선택 하지 않으면 페이지는 *영화* 페이지에서 페이지 친숙 한 오류 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-286">You used this code to make sure that if a user gets to the *EditMovies* page without first selecting a movie in the *Movies* page, the page would display a user-friendly error message.</span></span> <span data-ttu-id="538bb-287">(이렇게 하지 않으면 사용자가 오류를 볼 수 혼동 있을 것는 것입니다.)</span><span class="sxs-lookup"><span data-stu-id="538bb-287">(Otherwise, users would see an error that would probably just confuse them.)</span></span>

<span data-ttu-id="538bb-288">그러나이 유효성 검사는 매우 강력 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-288">However, this validation isn't very robust.</span></span> <span data-ttu-id="538bb-289">이러한 오류와 함께 페이지를 호출할 수도 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-289">The page might also be invoked with these errors:</span></span>

- <span data-ttu-id="538bb-290">ID 번호를 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-290">The ID isn't a number.</span></span> <span data-ttu-id="538bb-291">같은 URL을 사용 하 여 페이지 수 호출 하는 예를 들어 `http://localhost:nnnnn/EditMovie?id=abc`합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-291">For example, the page could be invoked with a URL like `http://localhost:nnnnn/EditMovie?id=abc`.</span></span>
- <span data-ttu-id="538bb-292">ID는 숫자, 존재 하지 않는 동영상을 참조 하지만 (예를 들어 `http://localhost:nnnnn/EditMovie?id=100934`).</span><span class="sxs-lookup"><span data-stu-id="538bb-292">The ID is a number, but it references a movie that doesn't exist (for example, `http://localhost:nnnnn/EditMovie?id=100934`).</span></span>

<span data-ttu-id="538bb-293">실행이 Url에서 발생 하는 오류를 보려면 내용은 *동영상* 페이지.</span><span class="sxs-lookup"><span data-stu-id="538bb-293">If you're curious to see the errors that result from these URLs, run the *Movies* page.</span></span> <span data-ttu-id="538bb-294">동영상을 편집 하려면 선택 하 고 다음의 URL을 변경는 *EditMovie* 알파벳 포함 된 URL로 페이지 ID 또는 존재 하지 않는 동영상의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-294">Select a movie to edit, and then change the URL of the *EditMovie* page to a URL that contains an alphabetic ID or the ID of a non-existent movie.</span></span>

<span data-ttu-id="538bb-295">따라서 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="538bb-295">So what should you do?</span></span> <span data-ttu-id="538bb-296">첫 번째 해결 방법은 뿐만 아니라 ID 전달 되도록 페이지에 있지만 ID는 정수에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-296">The first fix is to make sure that not only is an ID passed to the page, but that the ID is an integer.</span></span> <span data-ttu-id="538bb-297">에 대 한 코드를 변경는 `!IsPost` 테스트를이 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-297">Change the code for the `!IsPost` test to look like this example:</span></span>

[!code-csharp[Main](updating-data/samples/sample14.cs)]

<span data-ttu-id="538bb-298">두 번째 조건을 추가 `IsEmpty` 로 연결 된 테스트 `&&` (논리적 AND):</span><span class="sxs-lookup"><span data-stu-id="538bb-298">You've added a second condition to the `IsEmpty` test, linked with `&&` (logical AND):</span></span>

[!code-csharp[Main](updating-data/samples/sample15.cs)]

<span data-ttu-id="538bb-299">기억 수는 [ASP.NET 웹 페이지 프로그래밍 소개](../introducing-razor-syntax-c.md) 자습서와 같은 메서드를 통해 `AsBool` 는 `AsInt` 문자열 일부 다른 데이터 형식으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-299">You might remember from the [Introduction to ASP.NET Web Pages Programming](../introducing-razor-syntax-c.md) tutorial that methods like `AsBool` an `AsInt` convert a character string to some other data type.</span></span> <span data-ttu-id="538bb-300">`IsInt` 메서드 (다음과 같은 기타 상자에서는 `IsBool` 및 `IsDateTime`) 권장 사항과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-300">The `IsInt` method (and others, like `IsBool` and `IsDateTime`) are similar.</span></span> <span data-ttu-id="538bb-301">그러나만 테스트 여부 있습니다 *수* 실제로 변환을 수행 하지 않고 문자열을 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-301">However, they test only whether you *can* convert the string, without actually performing the conversion.</span></span> <span data-ttu-id="538bb-302">여기 있습니다 하는 명시적으로 *쿼리 문자열 값을 정수로 변환할 수 있는 경우...* .</span><span class="sxs-lookup"><span data-stu-id="538bb-302">So here you're essentially saying *If the query string value can be converted to an integer ...*.</span></span>

<span data-ttu-id="538bb-303">다른 잠재적 문제가 존재 하지 않는 동영상을 찾고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-303">The other potential problem is looking for a movie that doesn't exist.</span></span> <span data-ttu-id="538bb-304">이 코드와 비슷합니다 동영상을 가져오는 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-304">The code to get a movie looks like this code:</span></span>

[!code-csharp[Main](updating-data/samples/sample16.cs)]

<span data-ttu-id="538bb-305">전달 하는 경우는 `movieId` 값을 `QuerySingle` 실제 동영상에 해당 하지 않는 메서드를 아무 것도 반환 하 고 문의 따르는 (예를 들어 `title=row.Title`) 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-305">If you pass a `movieId` value to the `QuerySingle` method that doesn't correspond to an actual movie, nothing is returned and the statements that follow (for example, `title=row.Title`) result in errors.</span></span>

<span data-ttu-id="538bb-306">다시 쉽게 고칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-306">Again there's an easy fix.</span></span> <span data-ttu-id="538bb-307">경우는 `db.QuerySingle` 없는 결과 반환 하는 메서드는 `row` 변수는 null이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-307">If the `db.QuerySingle` method returns no results, the `row` variable will be null.</span></span> <span data-ttu-id="538bb-308">체크 인할 수 있는지 여부를 `row` 여기에서 값 가져오기 하려고 하기 전에 변수는 null입니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-308">So you can check whether the `row` variable is null before you try to get values from it.</span></span> <span data-ttu-id="538bb-309">다음 코드에서는 추가 `if` 블록의 값을 가져오는 문에 `row` 개체:</span><span class="sxs-lookup"><span data-stu-id="538bb-309">The following code adds an `if` block around the statements that get the values out of the `row` object:</span></span>

[!code-csharp[Main](updating-data/samples/sample17.cs)]

<span data-ttu-id="538bb-310">이러한 두 개의 추가 유효성 검사 테스트 페이지 글머리 기호 성능을 입증 됩니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-310">With these two additional validation tests, the page becomes more bullet-proof.</span></span> <span data-ttu-id="538bb-311">에 대 한 전체 코드는 `!IsPost` 분기 이제이 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-311">The complete code for the `!IsPost` branch now looks like this example:</span></span>

[!code-csharp[Main](updating-data/samples/sample18.cs)]

<span data-ttu-id="538bb-312">म 점을 한 번 더이 작업에 대 한 적절 하 게 사용 인지는 `else` 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-312">We'll note once more that this task is a good use for an `else` block.</span></span> <span data-ttu-id="538bb-313">테스트에 통과 하지 않는 경우는 `else` 블록 오류 메시지를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-313">If the tests don't pass, the `else` blocks set error messages.</span></span>

## <a name="adding-a-link-to-return-to-the-movies-page"></a><span data-ttu-id="538bb-314">영화 페이지로 돌아가려면 링크 추가</span><span class="sxs-lookup"><span data-stu-id="538bb-314">Adding a Link to Return to the Movies Page</span></span>

<span data-ttu-id="538bb-315">최종 하 고 유용한 정보 링크를 추가 하는 것으로 다시는 *동영상* 페이지.</span><span class="sxs-lookup"><span data-stu-id="538bb-315">A final and helpful detail is to add a link back to the *Movies* page.</span></span> <span data-ttu-id="538bb-316">사용자가 시작 이벤트의 일반 흐름에서는 *동영상* 페이지를 클릭 하 고는 **편집** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-316">In the ordinary flow of events, users will start at the *Movies* page and click an **Edit** link.</span></span> <span data-ttu-id="538bb-317">제공 하는 *EditMovie* 페이지에서 며 수 영화를 편집 하 고 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-317">That brings them to the *EditMovie* page, where they can edit the movie and click the button.</span></span> <span data-ttu-id="538bb-318">다시 리디렉션합니다. 변경 내용을 처리 하는 코드는 *동영상* 페이지.</span><span class="sxs-lookup"><span data-stu-id="538bb-318">After the code processes the change, it redirects back to the *Movies* page.</span></span>

<span data-ttu-id="538bb-319">그러나:</span><span class="sxs-lookup"><span data-stu-id="538bb-319">However:</span></span>

- <span data-ttu-id="538bb-320">사용자 아무 것도 변경 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-320">The user might decide not to change anything.</span></span>
- <span data-ttu-id="538bb-321">사용자는 클릭 하지 않고이 페이지에 수신는 **편집** 연결에 *영화* 페이지.</span><span class="sxs-lookup"><span data-stu-id="538bb-321">The user might have gotten to this page without first clicking an **Edit** link in the *Movies* page.</span></span>

<span data-ttu-id="538bb-322">기본 목록으로 돌아가려면를 쉽게 확인 하려는 어떤 방법을 사용 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-322">Either way, you want to make it easy for them to return to the main listing.</span></span> <span data-ttu-id="538bb-323">쉽게 수정 되었기 &mdash; 닫는 바로 뒤에 다음 태그에 추가 `</form>` 태그에 태그:</span><span class="sxs-lookup"><span data-stu-id="538bb-323">It's an easy fix &mdash; add the following markup just after the closing `</form>` tag in the markup:</span></span>

[!code-html[Main](updating-data/samples/sample19.html)]

<span data-ttu-id="538bb-324">이 태그에 대 한 동일한 구문을 사용 하 여 프로그램 `<a>` 다른 곳에서 보았을 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-324">This markup uses the same syntax for an `<a>` element that you've seen elsewhere.</span></span> <span data-ttu-id="538bb-325">URL에 포함 `~` 을 "웹 사이트의 루트입니다."를 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-325">The URL includes `~` to mean "root of the website."</span></span>

## <a name="testing-the-movie-update-process"></a><span data-ttu-id="538bb-326">영화 업데이트 프로세스를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-326">Testing the Movie Update Process</span></span>

<span data-ttu-id="538bb-327">이제 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-327">Now you can test.</span></span> <span data-ttu-id="538bb-328">실행 된 *동영상* 페이지를 클릭 하 여 **편집** 동영상 옆에 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-328">Run the *Movies* page, and click **Edit** next to a movie.</span></span> <span data-ttu-id="538bb-329">경우는 *EditMovie* 동영상 및 클릭을 변경할 페이지가 표시 되 면 **변경 내용 전송**합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-329">When the *EditMovie* page appears, make changes to the movie and click **Submit Changes**.</span></span> <span data-ttu-id="538bb-330">영화 목록이 표시 되 면 하는 경우 변경 내용을 표시 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-330">When the movie listing appears, make sure that your changes are shown.</span></span>

<span data-ttu-id="538bb-331">유효성 검사가 작동 하려면 클릭 **편집** 다른 동영상에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-331">To make sure that validation is working, click **Edit** for another movie.</span></span> <span data-ttu-id="538bb-332">도달 하면는 *EditMovie* 선택을 취소 페이지는 **장르** 필드 (또는 **연도** 필드 또는 둘 다) 하 고 변경 내용을 전송 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-332">When you get to the *EditMovie* page, clear the **Genre** field (or **Year** field, or both) and try to submit your changes.</span></span> <span data-ttu-id="538bb-333">오류를 예상 대로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-333">You'll see an error, as you'd expect:</span></span>

![유효성 검사 오류를 보여 주는 동영상 페이지 편집](updating-data/_static/image4.png)

<span data-ttu-id="538bb-335">클릭는 **영화 목록으로 반환** 링크 변경 내용을 취소 하 고 반환 하는 *영화* 페이지.</span><span class="sxs-lookup"><span data-stu-id="538bb-335">Click the **Return to movie listing** link to abandon your changes and return to the *Movies* page.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="538bb-336">다음에 나오는</span><span class="sxs-lookup"><span data-stu-id="538bb-336">Coming Up Next</span></span>

<span data-ttu-id="538bb-337">다음 자습서에서는 영화 레코드를 삭제 하는 방법을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="538bb-337">In the next tutorial, you'll see how to delete a movie record.</span></span>

## <a name="complete-listing-for-movie-page-updated-with-edit-links"></a><span data-ttu-id="538bb-338">동영상 페이지 (편집 링크와 함께 업데이트)에 대 한 전체 목록을 보려면</span><span class="sxs-lookup"><span data-stu-id="538bb-338">Complete Listing for Movie Page (Updated with Edit Links)</span></span>

[!code-cshtml[Main](updating-data/samples/sample20.cshtml)]

<a id="Complete_Page_Listing_for_EditMovie"></a>
## <a name="complete-page-listing-for-edit-movie-page"></a><span data-ttu-id="538bb-339">전체 동영상 페이지 편집에 대 한 목록 페이지</span><span class="sxs-lookup"><span data-stu-id="538bb-339">Complete Page Listing for Edit Movie Page</span></span>

[!code-cshtml[Main](updating-data/samples/sample21.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="538bb-340">추가 자료</span><span class="sxs-lookup"><span data-stu-id="538bb-340">Additional Resources</span></span>

- [<span data-ttu-id="538bb-341">Razor 구문을 사용 하 여 ASP.NET 웹 프로그래밍 소개</span><span class="sxs-lookup"><span data-stu-id="538bb-341">Introduction to ASP.NET Web Programming by Using the Razor Syntax</span></span>](../../getting-started/introducing-razor-syntax-c.md)
- <span data-ttu-id="538bb-342">[SQL UPDATE 문을](http://www.w3schools.com/sql/sql_update.asp) W3Schools 사이트</span><span class="sxs-lookup"><span data-stu-id="538bb-342">[SQL UPDATE Statement](http://www.w3schools.com/sql/sql_update.asp) on the W3Schools site</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="538bb-343">[이전](entering-data.md)
> [다음](deleting-data.md)</span><span class="sxs-lookup"><span data-stu-id="538bb-343">[Previous](entering-data.md)
[Next](deleting-data.md)</span></span>
