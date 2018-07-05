---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/updating-data
title: ASP.NET 웹 페이지 소개-데이터베이스 데이터를 업데이트 하는 중 | Microsoft Docs
author: tfitzmac
description: 이 자습서에서는 ASP.NET Web Pages (Razor)를 사용 하는 경우 기존 데이터베이스 (변경) 항목을 업데이트 하는 방법을 보여 줍니다. 시리즈를 완료 했다고 가정 하기 번째...
ms.author: aspnetcontent
ms.date: 01/02/2018
ms.assetid: ac86ec9c-6b69-485b-b9e0-8b9127b13e6b
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/updating-data
msc.type: authoredcontent
ms.openlocfilehash: 948f5b5933669a43bf37dc0317ad644660dc67e9
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37842904"
---
<a name="introducing-aspnet-web-pages---updating-database-data"></a><span data-ttu-id="18ac8-104">ASP.NET 웹 페이지 소개-데이터베이스 데이터를 업데이트 하는 중</span><span class="sxs-lookup"><span data-stu-id="18ac8-104">Introducing ASP.NET Web Pages - Updating Database Data</span></span>
====================
<span data-ttu-id="18ac8-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="18ac8-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="18ac8-106">이 자습서에서는 ASP.NET Web Pages (Razor)를 사용 하는 경우 기존 데이터베이스 (변경) 항목을 업데이트 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-106">This tutorial shows you how to update (change) an existing database entry when you use ASP.NET Web Pages (Razor).</span></span> <span data-ttu-id="18ac8-107">통해 시리즈를 완료 했다고 가정 하 [입력 데이터에서 사용 하 여 Forms를 사용 하 여 ASP.NET 웹 페이지](entering-data.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-107">It assumes you have completed the series through [Entering Data by Using Forms Using ASP.NET Web Pages](entering-data.md).</span></span>
> 
> <span data-ttu-id="18ac8-108">학습할 내용:</span><span class="sxs-lookup"><span data-stu-id="18ac8-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="18ac8-109">개별 레코드를 선택 하는 방법의 `WebGrid` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-109">How to select an individual record in the `WebGrid` helper.</span></span>
> - <span data-ttu-id="18ac8-110">데이터베이스에서 단일 레코드를 읽는 방법.</span><span class="sxs-lookup"><span data-stu-id="18ac8-110">How to read a single record from a database.</span></span>
> - <span data-ttu-id="18ac8-111">데이터베이스 레코드의 값을 사용 하 여 폼을 미리 로드 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-111">How to preload a form with values from the database record.</span></span>
> - <span data-ttu-id="18ac8-112">데이터베이스의 기존 레코드를 업데이트 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="18ac8-112">How to update an existing record in a database.</span></span>
> - <span data-ttu-id="18ac8-113">페이지에 표시 하지 않고 정보를 저장 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="18ac8-113">How to store information in the page without displaying it.</span></span>
> - <span data-ttu-id="18ac8-114">숨겨진된 필드를 사용 하 여 정보를 저장 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="18ac8-114">How to use a hidden field to store information.</span></span>
>   
> 
> <span data-ttu-id="18ac8-115">기능/기술을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-115">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="18ac8-116">`WebGrid` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-116">The `WebGrid` helper.</span></span>
> - <span data-ttu-id="18ac8-117">SQL `Update` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-117">The SQL `Update` command.</span></span>
> - <span data-ttu-id="18ac8-118">`Database.Execute` 메서드</span><span class="sxs-lookup"><span data-stu-id="18ac8-118">The `Database.Execute` method.</span></span>
> - <span data-ttu-id="18ac8-119">숨겨진 필드 (`<input type="hidden">`).</span><span class="sxs-lookup"><span data-stu-id="18ac8-119">Hidden fields (`<input type="hidden">`).</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="18ac8-120">만들 내용</span><span class="sxs-lookup"><span data-stu-id="18ac8-120">What You'll Build</span></span>

<span data-ttu-id="18ac8-121">이전 자습서에서는 데이터베이스에 레코드를 추가 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-121">In the previous tutorial, you learned how to add a record to a database.</span></span> <span data-ttu-id="18ac8-122">여기에서 편집에 대 한 레코드를 표시 하는 방법에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-122">Here, you'll learn how to display a record for editing.</span></span> <span data-ttu-id="18ac8-123">에 *영화* 에서는 업데이트 페이지는 `WebGrid` 도우미를 표시 하도록는 **편집** 각 영화 옆에 있는 링크:</span><span class="sxs-lookup"><span data-stu-id="18ac8-123">In the *Movies* page, you'll update the `WebGrid` helper so that it displays an **Edit** link next to each movie:</span></span>

![WebGrid 각 영화에 대 한 '편집' 링크를 포함 하 여 표시](updating-data/_static/image1.png)

<span data-ttu-id="18ac8-125">클릭할 때 합니다 **편집** 링크 걸리는 다른 페이지에 있는 영화 정보를 이미 형식에서:</span><span class="sxs-lookup"><span data-stu-id="18ac8-125">When you click the **Edit** link, it takes you to a different page, where the movie information is already in a form:</span></span>

![편집을 편집할 수는 동영상을 보여 주는 동영상 페이지](updating-data/_static/image2.png)

<span data-ttu-id="18ac8-127">값 중 하나를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-127">You can change any of the values.</span></span> <span data-ttu-id="18ac8-128">변경 내용을 제출 하면 코드 페이지에서 데이터베이스를 업데이트 하 고 영화 목록으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-128">When you submit the changes, the code in the page updates the database and takes you back to the movie listing.</span></span>

<span data-ttu-id="18ac8-129">이 부분의 프로세스와 거의 똑같이 작동 합니다 *AddMovie.cshtml* 되도록이 자습서의 대부분 친숙 한 이전 자습서에서 만든 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-129">This part of the process works almost exactly like the *AddMovie.cshtml* page you created in the previous tutorial, so much of this tutorial will be familiar.</span></span>

<span data-ttu-id="18ac8-130">여러 가지 방법으로 개별 영화를 편집 하는 기능을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-130">There are several ways you could implement a way to edit an individual movie.</span></span> <span data-ttu-id="18ac8-131">표시 된 접근 방식은 구현 하기 쉽고 이해 하기 쉬운 이기 때문에 선택 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-131">The approach shown was chosen because it's easy to implement and easy to understand.</span></span>

## <a name="adding-an-edit-link-to-the-movie-listing"></a><span data-ttu-id="18ac8-132">영화 목록에는 편집 링크 추가</span><span class="sxs-lookup"><span data-stu-id="18ac8-132">Adding an Edit Link to the Movie Listing</span></span>

<span data-ttu-id="18ac8-133">업데이트에서는 시작 하는 *영화* 각 영화 목록도 포함 되도록 페이지는 **편집** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-133">To begin, you'll update the *Movies* page so that each movie listing also contains an **Edit** link.</span></span>

<span data-ttu-id="18ac8-134">엽니다는 *Movies.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-134">Open the *Movies.cshtml* file.</span></span>

<span data-ttu-id="18ac8-135">페이지의 본문에서 변경 된 `WebGrid` 열을 추가 하 여는 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-135">In the body of the page, change the `WebGrid` markup by adding a column.</span></span> <span data-ttu-id="18ac8-136">수정 된 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-136">Here's the modified markup:</span></span>

[!code-html[Main](updating-data/samples/sample1.html?highlight=6)]

<span data-ttu-id="18ac8-137">새 열이이 같습니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-137">The new column is this one:</span></span>

[!code-html[Main](updating-data/samples/sample2.html)]

<span data-ttu-id="18ac8-138">이 칼럼의 지점 링크를 표시 하는 것 (`<a>` 요소) "편집" 이라고 표시 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-138">The point of this column is to show a link (`<a>` element) whose text says "Edit".</span></span> <span data-ttu-id="18ac8-139">연결 페이지를 실행 하는 경우 다음과 같이 표시 되는 링크를 만들 때 살펴볼 항목으로 `id` 각 영화에 대 한 다른 값:</span><span class="sxs-lookup"><span data-stu-id="18ac8-139">What we're after is to create a link that looks like the following when the page runs, with the `id` value different for each movie:</span></span>

[!code-css[Main](updating-data/samples/sample3.css)]

<span data-ttu-id="18ac8-140">이 링크는 라는 페이지를 호출 *EditMovie*, 및 쿼리 문자열을 전달 합니다 `?id=7` 해당 페이지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-140">This link will invoke a page named *EditMovie*, and it will pass the query string `?id=7` to that page.</span></span>

<span data-ttu-id="18ac8-141">새 열에 대 한 구문을 약간 복잡 한 보이지만 몇 가지 요소 모아놓은 때문에 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-141">The syntax for the new column might look a bit complex, but that's only because it puts together several elements.</span></span> <span data-ttu-id="18ac8-142">각 개별 요소는 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-142">Each individual element is straightforward.</span></span> <span data-ttu-id="18ac8-143">에 집중 하는 경우만 `<a>` 요소인이이 태그를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-143">If you concentrate on just the `<a>` element, you see this markup:</span></span>

[!code-html[Main](updating-data/samples/sample4.html)]

<span data-ttu-id="18ac8-144">눈금의 작동 원리에 대 한 몇 가지 배경 지식을: 표에 각 데이터베이스 레코드에 대해 하나의 행을 표시 하 고 데이터베이스 레코드의 각 필드에 대 한 열을 표시 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-144">Some background about how the grid works: the grid displays rows, one for each database record, and it displays columns for each field in the database record.</span></span> <span data-ttu-id="18ac8-145">각 표 형태 창의 행 생성 되는 동안는 `item` 개체에 해당 행에 대 한 데이터베이스 레코드가 (항목)를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-145">While each grid row is being constructed, the `item` object contains the database record (item) for that row.</span></span> <span data-ttu-id="18ac8-146">이 배열에서 해당 행에 대 한 데이터는 코드에서는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-146">This arrangement gives you a way in code to get at the data for that row.</span></span> <span data-ttu-id="18ac8-147">여기는: 식 `item.ID` 현재 데이터베이스 항목의 ID 값을 가져오고 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-147">That's what you see here: the expression `item.ID` is getting the ID value of the current database item.</span></span> <span data-ttu-id="18ac8-148">얻을 수 있습니다 (제목, 장르, 또는 연도) 데이터베이스 값 동일한 방식으로 사용 하 여 `item.Title`하십시오 `item.Genre`, 또는 `item.Year`합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-148">You could get any of the database values (title, genre, or year) the same way by using `item.Title`, `item.Genre`, or `item.Year`.</span></span>

<span data-ttu-id="18ac8-149">식을 `"~/EditMovie?id=@item.ID` 대상 URL 하드 코딩 된 부분을 결합 (`~/EditMovie?id=`)이 동적으로 파생 id</span><span class="sxs-lookup"><span data-stu-id="18ac8-149">The expression `"~/EditMovie?id=@item.ID` combines the hard-coded part of the target URL (`~/EditMovie?id=`) with this dynamically derived ID.</span></span> <span data-ttu-id="18ac8-150">(살펴보았습니다는 `~` 연산자는 이전 자습서에서 현재 웹 사이트 루트를 나타내는 ASP.NET 운영자는 것입니다.)</span><span class="sxs-lookup"><span data-stu-id="18ac8-150">(You saw the `~` operator in the previous tutorial; it's an ASP.NET operator that represents the current website root.)</span></span>

<span data-ttu-id="18ac8-151">결과 열에 있는 태그의이 부분 간단히 생성 한다는 다음 태그와 같이 런타임 시:</span><span class="sxs-lookup"><span data-stu-id="18ac8-151">The result is that this part of the markup in the column simply produces something like the following markup at run time:</span></span>

[!code-xml[Main](updating-data/samples/sample5.xml)]

<span data-ttu-id="18ac8-152">물론 실제 값 `id` 각 행에 대해 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-152">Naturally, the actual value of `id` will be different for each row.</span></span>

## <a name="creating-a-custom-display-for-a-grid-column"></a><span data-ttu-id="18ac8-153">표 형태 열에 대 한 표시를 사용자 지정 만들기</span><span class="sxs-lookup"><span data-stu-id="18ac8-153">Creating a Custom Display for a Grid Column</span></span>

<span data-ttu-id="18ac8-154">이제 표 형태의 열에 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-154">Now back to the grid column.</span></span> <span data-ttu-id="18ac8-155">세 열은 원래 표가 표시만 데이터 값 (title, genre 및 연도) 했습니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-155">The three columns you originally had in the grid displayed only data values (title, genre, and year).</span></span> <span data-ttu-id="18ac8-156">이 표시는 데이터베이스 열의 이름을 전달 하 여 지정한 &mdash; 예를 들어 `grid.Column("Title")`합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-156">You specified this display by passing the name of the database column &mdash; for example, `grid.Column("Title")`.</span></span>

<span data-ttu-id="18ac8-157">이 새로운 **편집** 링크 열 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-157">This new **Edit** link column is different.</span></span> <span data-ttu-id="18ac8-158">열 이름을 지정 하는 대신 전달 된 `format` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-158">Instead of specifying a column name, you're passing a `format` parameter.</span></span> <span data-ttu-id="18ac8-159">이 매개 변수를 사용 하면 태그를 정의할 수는 합니다 `WebGrid` 도우미와 함께 렌더링 됩니다는 `item` 열 데이터 굵게 또는 녹색으로 표시 하거나 원하는 형식으로 해당 값입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-159">This parameter lets you define markup that the `WebGrid` helper will render along with the `item` value to display the column data as bold or green or in whatever format that you want.</span></span> <span data-ttu-id="18ac8-160">예를 들어, 굵게 표시 하려면 제목, 원한다 면이 예제와 같이 열을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-160">For example, if you wanted the title to appear bold, you could create a column like this example:</span></span>

[!code-html[Main](updating-data/samples/sample6.html)]

<span data-ttu-id="18ac8-161">(다양 한 `@` 에 나오는 문자는 `format` 속성 태그 및 코드 값 간에 전환을 표시 합니다.)</span><span class="sxs-lookup"><span data-stu-id="18ac8-161">(The various `@` characters you see in the `format` property mark the transition between markup and a code value.)</span></span>

<span data-ttu-id="18ac8-162">에 대 한 알게 되 면 합니다 `format` 이해 하기 쉽습니다 속성을 어떻게 새 **편집** 링크 열 함께 취합 하는:</span><span class="sxs-lookup"><span data-stu-id="18ac8-162">Once you know about the `format` property, it's easier to understand how the new **Edit** link column is put together:</span></span>

[!code-html[Main](updating-data/samples/sample7.html)]

<span data-ttu-id="18ac8-163">열으로 구성 됩니다 *만* 의 링크를 렌더링 하는 태그를와 일부 정보가 (ID)는에서 추출 된 행에 대 한 데이터베이스 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-163">The column consists *only* of the markup that renders the link, plus some information (the ID) that's extracted from the database record for the row.</span></span>

> [!TIP]
> 
> <span data-ttu-id="18ac8-164">**명명 된 매개 변수 및 메서드에 대 한 위치 매개 변수**</span><span class="sxs-lookup"><span data-stu-id="18ac8-164">**Named Parameters and Positional Parameters for a Method**</span></span>
> 
> <span data-ttu-id="18ac8-165">여러 번 메서드를 호출 하 고 매개 변수 전달 했으므로 단순히 나열 된 쉼표로 구분 된 매개 변수 값입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-165">Many times when you've called a method and passed parameters to it, you've simply listed the parameter values separated by commas.</span></span> <span data-ttu-id="18ac8-166">몇 가지 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-166">Here are a couple of examples:</span></span>
> 
> `db.Execute(insertCommand, title, genre, year)`
> 
> `Validation.RequireField("title", "You must enter a title")`
> 
> <span data-ttu-id="18ac8-167">이 코드를 먼저 살펴본 하지만 각각의 경우에서 특정 순서로 메서드에 매개 변수를 전달 하는 경우 문제를 언급 하지 않았습니다에서는 &mdash; 즉, 메서드에 매개 변수 정의 되는 순서입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-167">We didn't mention the issue when you first saw this code, but in each case, you're passing parameters to the methods in a specific order &mdash; namely, the order in which the parameters are defined in that method.</span></span> <span data-ttu-id="18ac8-168">에 대 한 `db.Execute` 고 `Validation.RequireFields`, 페이지를 실행 하는 경우 오류 메시지 또는 이상한 결과 이상 얻게 전달 하는 값의 순서를 혼합 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="18ac8-168">For `db.Execute` and `Validation.RequireFields`, if you mixed up the order of the values you pass, you'd get an error message when the page runs, or at least some strange results.</span></span> <span data-ttu-id="18ac8-169">물론 매개 변수를 전달 하는 순서를 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-169">Clearly, you have to know the order to pass the parameters in.</span></span> <span data-ttu-id="18ac8-170">(WebMatrix에서 IntelliSense 도움이 될 수 있습니다 이름, 형식 및 매개 변수의 순서 확인에 알아봅니다.)</span><span class="sxs-lookup"><span data-stu-id="18ac8-170">(In WebMatrix, IntelliSense can help you learn figure out the name, type, and order of the parameters.)</span></span>
> 
> <span data-ttu-id="18ac8-171">를 순서 대로 값을 전달 하는 대신 사용할 수 있습니다 *명명 된 매개 변수*합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-171">As an alternative to passing values in order, you can use *named parameters*.</span></span> <span data-ttu-id="18ac8-172">(사용 하 여 이라고 순서로 매개 변수 전달 *위치 매개 변수*.) 명명 된 매개 변수에 대 한 명시적으로 포함 된 매개 변수의 이름을 해당 값을 전달 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="18ac8-172">(Passing parameters in order is known as using *positional parameters*.) For named parameters, you explicitly include the name of the parameter when passing its value.</span></span> <span data-ttu-id="18ac8-173">명명 된 매개 변수 이미 여러 번에서에서 사용한 이러한 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-173">You've used named parameters already a number of times in these tutorials.</span></span> <span data-ttu-id="18ac8-174">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="18ac8-174">For example:</span></span>
> 
> [!code-csharp[Main](updating-data/samples/sample8.cs)]
> 
> <span data-ttu-id="18ac8-175">를 갖는</span><span class="sxs-lookup"><span data-stu-id="18ac8-175">and</span></span>
> 
> [!code-css[Main](updating-data/samples/sample9.css)]
> 
> <span data-ttu-id="18ac8-176">명명 된 매개 변수는 메서드가 여러 매개 변수를 사용 하는 경우에 특히 몇 가지 상황에서 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-176">Named parameters are handy for a couple of situations, especially when a method takes many parameters.</span></span> <span data-ttu-id="18ac8-177">하나 이상의 매개 변수를 전달 하려는 하지만 경우 전달 하려는 값 매개 변수 목록의 첫 번째 위치 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-177">One is when you want to pass only one or two parameters, but the values you want to pass are not among the first positions in the parameter list.</span></span> <span data-ttu-id="18ac8-178">또 다른 상황은 매개 변수를 사용 하면 대부분의 적합 한 순서 대로 전달 하 여 코드를 더 읽기 쉽게 하려는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-178">Another situation is when you want to make your code more readable by passing the parameters in the order that makes the most sense to you.</span></span>
> 
> <span data-ttu-id="18ac8-179">물론 명명 된 매개 변수를 사용 하려면 해야 매개 변수의 이름을 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-179">Obviously, to use named parameters, you have to know the names of the parameters.</span></span> <span data-ttu-id="18ac8-180">WebMatrix IntelliSense 수 *표시* 이름, 하지만 현재을 채울 수 없습니다 하 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-180">WebMatrix IntelliSense can *show* you the names, but it cannot currently fill them in for you.</span></span>


## <a name="creating-the-edit-page"></a><span data-ttu-id="18ac8-181">편집 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="18ac8-181">Creating the Edit Page</span></span>

<span data-ttu-id="18ac8-182">이제 만들어야 합니다 *EditMovie* 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-182">Now you can create the *EditMovie* page.</span></span> <span data-ttu-id="18ac8-183">사용자가 클릭 하면 합니다 **편집** 링크는 최종적으로이 페이지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-183">When users click the **Edit** link, they'll end up on this page.</span></span>

<span data-ttu-id="18ac8-184">라는 페이지를 만듭니다 *EditMovie.cshtml* 다음 태그를 사용 하 여 파일에 포함 된 내용으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-184">Create a page named *EditMovie.cshtml* and replace what's in the file with the following markup:</span></span>

[!code-cshtml[Main](updating-data/samples/sample10.cshtml)]

<span data-ttu-id="18ac8-185">이 태그와 코드는에 있는 비슷합니다는 *AddMovie* 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-185">This markup and code is similar to what you have in the *AddMovie* page.</span></span> <span data-ttu-id="18ac8-186">제출 단추에 대 한 텍스트에 약간의 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-186">There's a small difference in the text for the submit button.</span></span> <span data-ttu-id="18ac8-187">와 마찬가지로 합니다 *AddMovie* 페이지, 즉는 `Html.ValidationSummary` 있는 경우 유효성 검사 오류를 표시 하는 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-187">As with the *AddMovie* page, there's an `Html.ValidationSummary` call that will display validation errors if there are any.</span></span> <span data-ttu-id="18ac8-188">에 대 한 호출을 생략 하는 것이 시간 `Validation.Message`유효성 검사 요약에 표시할 오류 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-188">This time we're leaving out calls to `Validation.Message`, since errors will be displayed in the validation summary.</span></span> <span data-ttu-id="18ac8-189">이전 자습서에서 설명한 대로, 다양 한 조합에 유효성 검사 요약 및 개별 오류 메시지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-189">As noted in the previous tutorial, you can use the validation summary and the individual error messages in various combinations.</span></span>

<span data-ttu-id="18ac8-190">다시 있음을 합니다 `method` 특성을 `<form>` 로 설정 된 `post`합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-190">Notice again that the `method` attribute of the `<form>` element is set to `post`.</span></span> <span data-ttu-id="18ac8-191">와 마찬가지로 합니다 *AddMovie.cshtml* 페이지에서이 페이지 변경 내용을 데이터베이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-191">As with the *AddMovie.cshtml* page, this page makes changes to the database.</span></span> <span data-ttu-id="18ac8-192">따라서이 폼을 수행할지를 `POST` 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-192">Therefore, this form should perform a `POST` operation.</span></span> <span data-ttu-id="18ac8-193">(간의 차이점에 대 한 자세한 `GET` 및 `POST` 작업을 참조 하세요 합니다 [GET, POST 및 HTTP 동사 안전성](form-basics.md#GET,_POST,_and_HTTP_Verb_Safety) 사이드바에서 HTML 폼에 대 한 자습서입니다.)</span><span class="sxs-lookup"><span data-stu-id="18ac8-193">(For more about the difference between `GET` and `POST` operations, see the [GET, POST, and HTTP Verb Safety](form-basics.md#GET,_POST,_and_HTTP_Verb_Safety) sidebar in the tutorial on HTML forms.)</span></span>

<span data-ttu-id="18ac8-194">이전 자습서에서 보았듯이 `value` 입력란의 특성을 미리 설치 하기 위해 Razor 코드를 사용 하 여 설정 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-194">As you saw in an earlier tutorial, the `value` attributes of the text boxes are being set with Razor code in order to preload them.</span></span> <span data-ttu-id="18ac8-195">이 시간을 사용 하는 같은 변수 `title` 하 고 `genre` 대신 해당 작업에 대 한 `Request.Form["title"]`:</span><span class="sxs-lookup"><span data-stu-id="18ac8-195">This time, though, you're using variables like `title` and `genre` for that task instead of `Request.Form["title"]`:</span></span>

`<input type="text" name="title" value="@title" />`

<span data-ttu-id="18ac8-196">로 이전에이 태그는 미리 로드 동영상 값을 사용 하 여 텍스트 상자 값입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-196">As before, this markup will preload the text box values with the movie values.</span></span> <span data-ttu-id="18ac8-197">편리 하 게 사용 하는 대신이 변수를 사용 하는 이유는 조금 뒤에 표시 된 `Request` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-197">You'll see in a moment why it's handy to use variables this time instead of using the `Request` object.</span></span>

<span data-ttu-id="18ac8-198">또한는 `<input type="hidden">` 이 페이지의 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-198">There's also a `<input type="hidden">` element on this page.</span></span> <span data-ttu-id="18ac8-199">이 요소는 표시 하지 않고 페이지의 영화 ID를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-199">This element stores the movie ID without making it visible on the page.</span></span> <span data-ttu-id="18ac8-200">ID는 처음에 페이지에 전달 하 여 쿼리 문자열 값을 사용 하 여 (`?id=7` 또는 유사한 URL에서).</span><span class="sxs-lookup"><span data-stu-id="18ac8-200">The ID is initially passed to the page by using a query string value (`?id=7` or similar in the URL).</span></span> <span data-ttu-id="18ac8-201">ID 값을 숨겨진된 필드를 넣어 할 수 없습니다는 페이지를 사용 하 여 호출 된 원래 URL에 대 한 액세스를 더 이상 있는 경우에, 양식이 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-201">By putting the ID value into a hidden field, you can make sure that it's available when the form is submitted, even if you no longer have access to the original URL that the page was invoked with.</span></span>

<span data-ttu-id="18ac8-202">와 달리 합니다 *AddMovie* 페이지에 대 한 코드를 *EditMovie* 페이지에는 두 가지 고유한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-202">Unlike the *AddMovie* page, the code for the *EditMovie* page has two distinct functions.</span></span> <span data-ttu-id="18ac8-203">첫 번째 함수는 페이지가 처음 표시 되는 경우 (및 *만* 다음), 코드 쿼리 문자열에서 영화 ID를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-203">The first function is that when the page is displayed for the first time (and *only* then), the code gets the movie ID from the query string.</span></span> <span data-ttu-id="18ac8-204">다음 코드를 사용 하 여 ID 데이터베이스에서 해당 영화를 읽고 표시 (미리 로드)이 텍스트 상자에 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-204">The code then uses the ID to read the corresponding movie out of the database and display (preload) it in the text boxes.</span></span>

<span data-ttu-id="18ac8-205">두 번째 함수는 사용자가 클릭할 때 합니다 **변경 내용 전송** 단추 코드는 입력란의 값을 읽고 유효성을 검사할 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-205">The second function is that when the user clicks the **Submit Changes** button, the code has to read the values of the text boxes and validate them.</span></span> <span data-ttu-id="18ac8-206">또한 코드를 새 값을 사용 하 여 데이터베이스 항목을 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-206">The code also has to update the database item with the new values.</span></span> <span data-ttu-id="18ac8-207">이 방법은 추가 레코드를 유사한에서 볼 수 있듯이 *AddMovie*합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-207">This technique is similar to adding a record, as you saw in *AddMovie*.</span></span>

## <a name="adding-code-to-read-a-single-movie"></a><span data-ttu-id="18ac8-208">단일 동영상을 읽는 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-208">Adding Code to Read a Single Movie</span></span>

<span data-ttu-id="18ac8-209">첫 번째 함수를 수행 하려면이 코드 페이지의 맨 위에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-209">To perform the first function, add this code to the top of the page:</span></span>

[!code-cshtml[Main](updating-data/samples/sample11.cshtml)]

<span data-ttu-id="18ac8-210">시작 블록 내에서이 코드의 대부분은 `if(!IsPost)`합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-210">Most of this code is inside a block that starts `if(!IsPost)`.</span></span> <span data-ttu-id="18ac8-211">`!` 연산자 의미 "not" 식 의미 하므로 *이 요청이 post 제출 되지 않으면*는 간접 방법 설명할 *이 요청은 처음으로이 페이지를 실행 하는 경우*합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-211">The `!` operator means "not," so the expression means *if this request is not a post submission*, which is an indirect way of saying *if this request is the first time that this page has been run*.</span></span> <span data-ttu-id="18ac8-212">이 코드를 실행 해야 앞에서 설명한 대로 *만* 처음으로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-212">As noted earlier, this code should run *only* the first time the page runs.</span></span> <span data-ttu-id="18ac8-213">코드를 포함 하지 않은 경우 `if(!IsPost)`는 페이지가 호출 될 때마다, 여부 처음으로 실행 또는 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-213">If you didn't enclose the code in `if(!IsPost)`, it would run every time the page is invoked, whether the first time or in response to a button click.</span></span>

<span data-ttu-id="18ac8-214">코드를 포함 하는 `else` 이 이번 차단 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-214">Notice that the code includes an `else` block this time.</span></span> <span data-ttu-id="18ac8-215">도입 했습니다 했 듯이 `if` 경우에 따라 테스트 하는 조건이 true 없으면 대체 코드를 실행 하려는 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-215">As we said when we introduced `if` blocks, sometimes you want to run alternative code if the condition you're testing isn't true.</span></span> <span data-ttu-id="18ac8-216">여기서입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-216">That's the case here.</span></span> <span data-ttu-id="18ac8-217">조건 (즉, 경우 페이지에 전달 하는 ID 확인)를 통과 하는 경우 데이터베이스에서 행을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-217">If the condition passes (that is, if the ID passed to the page is ok), you read a row from the database.</span></span> <span data-ttu-id="18ac8-218">그러나 조건을 통과 하지 못한 경우는 `else` 블록은 실행 및 코드 오류 메시지를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-218">However, if the condition doesn't pass, the `else` block runs and the code sets an error message.</span></span>

## <a name="validating-a-value-passed-to-the-page"></a><span data-ttu-id="18ac8-219">페이지에 전달 된 값의 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="18ac8-219">Validating a Value Passed to the Page</span></span>

<span data-ttu-id="18ac8-220">코드를 사용 하 여 `Request.QueryString["id"]` 페이지로 전달 되는 ID를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-220">The code uses `Request.QueryString["id"]` to get the ID that's passed to the page.</span></span> <span data-ttu-id="18ac8-221">코드에서는 id 값을 실제로 전달 된 되는지</span><span class="sxs-lookup"><span data-stu-id="18ac8-221">The code makes sure that a value was actually passed for the ID.</span></span> <span data-ttu-id="18ac8-222">값이 전달 된 경우 코드 유효성 검사 오류를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-222">If no value was passed, the code sets a validation error.</span></span>

<span data-ttu-id="18ac8-223">이 코드에 정보의 유효성을 검사 하는 다른 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-223">This code shows a different way to validate information.</span></span> <span data-ttu-id="18ac8-224">이전 자습서에서 사용한는 `Validation` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-224">In the previous tutorial, you worked with the `Validation` helper.</span></span> <span data-ttu-id="18ac8-225">유효성을 검사 하는 필드를 등록 하 고 ASP.NET에서 자동으로 유효성 검사를 않았습니다 하 고 사용 하 여 오류를 표시 `Html.ValidationMessage` 고 `Html.ValidationSummary`입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-225">You registered fields to validate, and ASP.NET automatically did the validation and displayed errors by using `Html.ValidationMessage` and `Html.ValidationSummary`.</span></span> <span data-ttu-id="18ac8-226">그러나이 경우 하는 것은 아닙니다 사용자 입력 유효성 검사.</span><span class="sxs-lookup"><span data-stu-id="18ac8-226">In this case, however, you're not really validating user input.</span></span> <span data-ttu-id="18ac8-227">대신 다른 곳에서 페이지에 전달 된 값의 유효성 검사 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-227">Instead, you're validating a value that was passed to the page from elsewhere.</span></span> <span data-ttu-id="18ac8-228">`Validation` 도우미를 재순환 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-228">The `Validation` helper doesn't do that for you.</span></span>

<span data-ttu-id="18ac8-229">따라서 값을 확인할 있습니다를 직접 사용 하 여 테스트 하 여 `if(!Request.QueryString["ID"].IsEmpty()`).</span><span class="sxs-lookup"><span data-stu-id="18ac8-229">Therefore, you check the value yourself, by testing it with `if(!Request.QueryString["ID"].IsEmpty()`).</span></span> <span data-ttu-id="18ac8-230">문제가 있으면 사용 하 여 오류를 표시할 수 있습니다 `Html.ValidationSummary`과 마찬가지로는 `Validation` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-230">If there's a problem, you can display the error by using `Html.ValidationSummary`, as you did with the `Validation` helper.</span></span> <span data-ttu-id="18ac8-231">이렇게 하려면 호출 `Validation.AddFormError` 표시할 메시지를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-231">To do that, you call `Validation.AddFormError` and pass it a message to display.</span></span> <span data-ttu-id="18ac8-232">`Validation.AddFormError` 익숙한 이미 유효성 검사 시스템 사용 하 여 연결 하는 사용자 지정 메시지를 정의할 수 있는 기본 제공 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-232">`Validation.AddFormError` is a built-in method that lets you define custom messages that tie in with the validation system you're already familiar with.</span></span> <span data-ttu-id="18ac8-233">(이 자습서의 뒷부분에서 설명이 유효성 검사 프로세스를 좀 더 강력 하 게 하는 방법에 대 한 합니다.)</span><span class="sxs-lookup"><span data-stu-id="18ac8-233">(Later in this tutorial we'll talk about how to make this validation process a little more robust.)</span></span>

<span data-ttu-id="18ac8-234">영화 ID 인지에 확인 한 후 코드는 단일 데이터베이스 항목만 찾고 데이터베이스를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-234">After making sure that there's an ID for the movie, the code reads the database, looking for only a single database item.</span></span> <span data-ttu-id="18ac8-235">(아마도 했을 데이터베이스 작업에 대 한 일반적인 패턴: 데이터베이스를 열고 SQL 문을 정의 하는 문을 실행 합니다.) 이 이번에는 SQL `Select` 문에 포함 되는 `WHERE ID = @0`합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-235">(You probably have noticed the general pattern for database operations: open the database, define a SQL statement, and run the statement.) This time, the SQL `Select` statement includes `WHERE ID = @0`.</span></span> <span data-ttu-id="18ac8-236">ID가 고유 하므로 하나의 레코드를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-236">Because the ID is unique, only one record can be returned.</span></span>

<span data-ttu-id="18ac8-237">쿼리를 사용 하 여 수행할 `db.QuerySingle` (되지 `db.Query`영화 목록에 사용한 것과,), 코드 결과를 넣습니다는 `row` 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-237">The query is performed by using `db.QuerySingle` (not `db.Query`, as you used for the movie listing), and the code puts the result into the `row` variable.</span></span> <span data-ttu-id="18ac8-238">이름을 `row` 임의로; 변수를 원하는 대로 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-238">The name `row` is arbitrary; you can name the variables anything you like.</span></span> <span data-ttu-id="18ac8-239">맨 위에 있는 초기화 변수 텍스트 상자에 이러한 값을 표시할 수 있도록 다음 영화 세부 정보로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-239">The variables initialized at the top are then filled with the movie details so that these values can be displayed in the text boxes.</span></span>

## <a name="testing-the-edit-page-so-far"></a><span data-ttu-id="18ac8-240">편집 페이지 (지금) 테스트</span><span class="sxs-lookup"><span data-stu-id="18ac8-240">Testing the Edit Page (So Far)</span></span>

<span data-ttu-id="18ac8-241">페이지를 테스트 하려는 경우 실행 합니다 *영화* 이제 페이지를 클릭는 **편집** 모든 동영상 옆에 있는 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-241">If you'd like to test your page, run the *Movies* page now and click an **Edit** link next to any movie.</span></span> <span data-ttu-id="18ac8-242">표시 된 *EditMovie* 선택한 영화에 대 한 세부 정보를 사용 하 여 페이지 입력:</span><span class="sxs-lookup"><span data-stu-id="18ac8-242">You'll see the *EditMovie* page with the details filled in for the movie you selected:</span></span>

![편집을 편집할 수는 동영상을 보여 주는 동영상 페이지](updating-data/_static/image3.png)

<span data-ttu-id="18ac8-244">페이지의 URL 같이 포함 `?id=10` (또는 다른 몇 가지 번호)입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-244">Notice that the URL of the page includes something like `?id=10` (or some other number).</span></span> <span data-ttu-id="18ac8-245">테스트 했으므로 지금 **편집** 에 연결 합니다 *영화* 페이지는 페이지 ID는 쿼리 문자열에서 읽고 되 고 단일 동영상 기록을 가져오는 데이터베이스 쿼리는 작업은 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-245">So far you've tested that **Edit** links in the *Movie* page work, that your page is reading the ID from the query string, and that the database query to get a single movie record is working.</span></span>

<span data-ttu-id="18ac8-246">영화 정보를 변경할 수 있지만 클릭할 때 아무 작업도 **변경 내용 전송**합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-246">You can change the movie information, but nothing happens when you click **Submit Changes**.</span></span>

## <a name="adding-code-to-update-the-movie-with-the-users-changes"></a><span data-ttu-id="18ac8-247">사용자의 변경 내용으로 동영상을 업데이트 하는 코드 추가</span><span class="sxs-lookup"><span data-stu-id="18ac8-247">Adding Code to Update the Movie with the User's Changes</span></span>

<span data-ttu-id="18ac8-248">에 *EditMovie.cshtml* 파일 (변경 내용 저장) 두 번째 함수를 구현 하려면 바로의 닫는 중괄호 안에 다음 코드를 추가 합니다는 `@` 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-248">In the *EditMovie.cshtml* file, to implement the second function (saving changes), add the following code just inside the closing brace of the `@` block.</span></span> <span data-ttu-id="18ac8-249">(보면 정확한 위치는 코드를 잘 모를 경우 합니다 [영화 편집 페이지에 대 한 목록 전체 코드](#Complete_Page_Listing_for_EditMovie) 이 자습서의 끝에 표시 되는.)</span><span class="sxs-lookup"><span data-stu-id="18ac8-249">(If you're not sure exactly where to put the code, you can look at the [complete code listing for the Edit Movie page](#Complete_Page_Listing_for_EditMovie) that appears at the end of this tutorial.)</span></span>

[!code-csharp[Main](updating-data/samples/sample12.cs)]

<span data-ttu-id="18ac8-250">이 태그와 코드 역시의 코드와 비슷하게 *AddMovie*합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-250">Again, this markup and code is similar to the code in *AddMovie*.</span></span> <span data-ttu-id="18ac8-251">코드는는 `if(IsPost)` 블록을 클릭 하는 경우에이 코드가 실행 되기 때문에 **변경 내용 전송** 단추 &mdash; 인 경우 (및 경우에만) 폼이 게시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-251">The code is in an `if(IsPost)` block, because this code runs only when the user clicks the **Submit Changes** button &mdash; that is, when (and only when) the form has been posted.</span></span> <span data-ttu-id="18ac8-252">이 경우 같은 테스트를 사용 하지 않는 `if(IsPost && Validation.IsValid())`-즉, 없습니다을 결합 하는 테스트를 모두 사용 하 여 and가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-252">In this case, you're not using a test like `if(IsPost && Validation.IsValid())`— that is, you're not combining both tests by using AND.</span></span> <span data-ttu-id="18ac8-253">에서는이 페이지에서는 먼저 확인 양식을 제출 하 여 인지 (`if(IsPost)`)에 다음 유효성 검사에 대 한 필드를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-253">In this page, you first determine whether there's a form submission (`if(IsPost)`), and only then register the fields for validation.</span></span> <span data-ttu-id="18ac8-254">다음 유효성 검사 결과 테스트할 수 있습니다 (`if(Validation.IsValid()`).</span><span class="sxs-lookup"><span data-stu-id="18ac8-254">Then you can test the validation results (`if(Validation.IsValid()`).</span></span> <span data-ttu-id="18ac8-255">흐름은 약간 변경 합니다 *AddMovie.cshtml* 페이지 다르지만 효과 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-255">The flow is slightly different than in the *AddMovie.cshtml* page, but the effect is the same.</span></span>

<span data-ttu-id="18ac8-256">사용 하 여 입력란의 값을 가져옵니다 `Request.Form["title"]` 및 다른 유사한 코드 `<input>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-256">You get the values of the text boxes by using `Request.Form["title"]` and similar code for the other `<input>` elements.</span></span> <span data-ttu-id="18ac8-257">이 이번에 코드를 가져옴을 영화 ID 숨겨진된 필드에서 확인할 수 있습니다 (`<input type="hidden">`).</span><span class="sxs-lookup"><span data-stu-id="18ac8-257">Notice that this time, the code gets the movie ID out of the hidden field (`<input type="hidden">`).</span></span> <span data-ttu-id="18ac8-258">페이지가 처음으로 실행 하는 경우 코드는 쿼리 문자열에서 ID를 가져왔습니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-258">When the page ran the first time, the code got the ID out of the query string.</span></span> <span data-ttu-id="18ac8-259">쿼리 문자열 조금 이라도 이후로 변경 된 경우 원래 표시 된 동영상 ID를 가져오는 중인 되도록 숨겨진된 필드의 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-259">You get the value from the hidden field to make sure that you're getting the ID of the movie that was originally displayed, in case the query string was somehow altered since then.</span></span>

<span data-ttu-id="18ac8-260">실제로 중요 한 차이점을 *AddMovie* 코드 및이 코드는이 코드에서 사용 하는 SQL `Update` 대신 문을 `Insert Into` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-260">The really important difference between the *AddMovie* code and this code is that in this code you use the SQL `Update` statement instead of the `Insert Into` statement.</span></span> <span data-ttu-id="18ac8-261">다음 예제에서는 SQL 구문의 `Update` 문:</span><span class="sxs-lookup"><span data-stu-id="18ac8-261">The following example shows the syntax of the SQL `Update` statement:</span></span>

`UPDATE table SET col1="value", col2="value", col3="value" ... WHERE ID = value`

<span data-ttu-id="18ac8-262">순서에 관계 없이 모든 열을 지정할 수 있습니다 및 중 모든 열을 업데이트할 필요가 반드시는 `Update` 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-262">You can specify any columns in any order, and you don't necessarily have to update every column during an `Update` operation.</span></span> <span data-ttu-id="18ac8-263">(적용 레코드 새 레코드로 저장 됩니다 및에 대 한 허용 되지 않는 때문에 자체 ID를 업데이트할 수 없습니다는 `Update` 작업 합니다.)</span><span class="sxs-lookup"><span data-stu-id="18ac8-263">(You cannot update the ID itself, because that would in effect save the record as a new record, and that's not allowed for an `Update` operation.)</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="18ac8-264">**중요** 는 `Where` 데이터베이스에서 데이터베이스를 인식 하는 방법 이기 때문에 ID 사용 하 여 절은 아주 중요 합니다을 업데이트 하려는 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-264">**Important** The `Where` clause with the ID is very important, because that's how the database knows which database record you want to update.</span></span> <span data-ttu-id="18ac8-265">중단 하는 경우는 `Where` 데이터베이스 업데이트 절 *모든* 데이터베이스의 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-265">If you left off the `Where` clause, the database would update *every* record in the database.</span></span> <span data-ttu-id="18ac8-266">대부분의 경우에서 재해가 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-266">In most cases, that would be a disaster.</span></span>


<span data-ttu-id="18ac8-267">코드에서 자리 표시자를 사용 하 여 값을 업데이트 하는 SQL 문에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-267">In the code, the values to update are passed to the SQL statement by using placeholders.</span></span> <span data-ttu-id="18ac8-268">전에 말한 새로운 반복: 보안상의 이유로 *만* 자리 표시자를 사용 하 여 SQL 문에 값을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-268">To repeat what we've said before: for security reasons, *only* use placeholders to pass values to a SQL statement.</span></span>

<span data-ttu-id="18ac8-269">코드를 사용한 후 `db.Execute` 실행 하는 `Update` 문을 변경 내용을 볼 수 있는 목록 페이지를 다시 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-269">After the code uses `db.Execute` to run the `Update` statement, it redirects back to the listing page, where you can see the changes.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="18ac8-270">**다른 SQL 문을 다른 메서드**</span><span class="sxs-lookup"><span data-stu-id="18ac8-270">**Different SQL Statements, Different Methods**</span></span>
> 
> <span data-ttu-id="18ac8-271">보았을 것 약간 다른 방법을 사용 하 여 다른 SQL 문을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-271">You might have noticed that you use slightly different methods to run different SQL statements.</span></span> <span data-ttu-id="18ac8-272">실행 하는 `Select` 쿼리에서 잠재적으로 반환 하며 여러 레코드를 사용 하는 `Query` 메서드.</span><span class="sxs-lookup"><span data-stu-id="18ac8-272">To run a `Select` query that potentially returns multiple records, you use the `Query` method.</span></span> <span data-ttu-id="18ac8-273">실행 하는 `Select` 알고 있는 쿼리는 데이터베이스 항목을 하나만 반환 합니다.를 사용 하는 `QuerySingle` 메서드.</span><span class="sxs-lookup"><span data-stu-id="18ac8-273">To run a `Select` query that you know will return only one database item, you use the `QuerySingle` method.</span></span> <span data-ttu-id="18ac8-274">사용할 데이터베이스 항목을 반환 하지는 않습니다 변경 하는 명령을 실행 하는 `Execute` 메서드.</span><span class="sxs-lookup"><span data-stu-id="18ac8-274">To run commands that make changes but that don't return database items, you use the `Execute` method.</span></span>
> 
> <span data-ttu-id="18ac8-275">간의 차이에 이미 본 것 처럼 각각 다른 결과 반환 하기 때문에 다른 메서드를 포함 해야 `Query` 고 `QuerySingle`입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-275">You have to have different methods because each of them returns different results, as you saw already in the difference between `Query` and `QuerySingle`.</span></span> <span data-ttu-id="18ac8-276">(합니다 `Execute` 실제로 반환 값도 &mdash; 명령에 의해 영향을 받는 데이터베이스 행의 수 즉, &mdash; 있습니다 했으므로 되었습니다 무시 하는 지금 있지만.)</span><span class="sxs-lookup"><span data-stu-id="18ac8-276">(The `Execute` method actually returns a value also &mdash; namely, the number of database rows that were affected by the command &mdash; but you've been ignoring that so far.)</span></span>
> 
> <span data-ttu-id="18ac8-277">물론는 `Query` 메서드는 하나의 데이터베이스 행을 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-277">Of course, the `Query` method might return only one database row.</span></span> <span data-ttu-id="18ac8-278">그러나 ASP.NET의 결과 항상 처리는 `Query` 컬렉션인 메서드.</span><span class="sxs-lookup"><span data-stu-id="18ac8-278">However, ASP.NET always treats the results of the `Query` method as a collection.</span></span> <span data-ttu-id="18ac8-279">메서드가 행을 하나만 반환 하는 경우에 컬렉션에서 단일 행을 추출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-279">Even if the method returns just one row, you have to extract that single row from the collection.</span></span> <span data-ttu-id="18ac8-280">상황에 따라서 여기서 있습니다 *알고* 얻게 하나의 행만, 사용 하는 편리한 다소 `QuerySingle`합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-280">Therefore, in situations where you *know* you'll get back only one row, it's a bit more convenient to use `QuerySingle`.</span></span>
> 
> <span data-ttu-id="18ac8-281">특정 유형의 데이터베이스 작업을 수행 하는 다른 몇 가지 방법 이며</span><span class="sxs-lookup"><span data-stu-id="18ac8-281">There are a few other methods that perform specific types of database operations.</span></span> <span data-ttu-id="18ac8-282">데이터베이스 메서드 목록을 찾을 수 있습니다 합니다 [ASP.NET Web Pages API 빠른 참조](../../api-reference/asp-net-web-pages-api-reference.md#Data)합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-282">You can find a listing of database methods in the [ASP.NET Web Pages API Quick Reference](../../api-reference/asp-net-web-pages-api-reference.md#Data).</span></span>


## <a name="making-validation-for-the-id-more-robust"></a><span data-ttu-id="18ac8-283">강력한 ID 더에 대 한 유효성 검사를 수행</span><span class="sxs-lookup"><span data-stu-id="18ac8-283">Making Validation for the ID More Robust</span></span>

<span data-ttu-id="18ac8-284">페이지를 실행 하는 처음으로 표시 된 동영상 ID를 쿼리 문자열에서 데이터베이스에서 해당 동영상 가져오기 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-284">The first time that the page runs, you get the movie ID from the query string so that you can go get that movie from the database.</span></span> <span data-ttu-id="18ac8-285">실제로 했습니다.이 코드를 사용 하 여 수행한 하는 값을 검색할 이동할 수 있게:</span><span class="sxs-lookup"><span data-stu-id="18ac8-285">You made sure that there actually was a value to go look for, which you did by using this code:</span></span>

[!code-csharp[Main](updating-data/samples/sample13.cs)]

<span data-ttu-id="18ac8-286">되도록 하는 사용자를 가져오는 경우이 코드를 사용 합니다 *EditMovies* 에서 동영상을 먼저 선택 하지 않고 페이지를 *영화* 페이지에서 페이지 친숙 한 오류 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-286">You used this code to make sure that if a user gets to the *EditMovies* page without first selecting a movie in the *Movies* page, the page would display a user-friendly error message.</span></span> <span data-ttu-id="18ac8-287">(이 고, 그렇지 사용자 오류를 볼 수는 있을 것 혼동할입니다.)</span><span class="sxs-lookup"><span data-stu-id="18ac8-287">(Otherwise, users would see an error that would probably just confuse them.)</span></span>

<span data-ttu-id="18ac8-288">그러나이 유효성 검사는 매우 강력 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-288">However, this validation isn't very robust.</span></span> <span data-ttu-id="18ac8-289">이러한 오류와 함께 페이지 호출할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-289">The page might also be invoked with these errors:</span></span>

- <span data-ttu-id="18ac8-290">ID 번호를 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-290">The ID isn't a number.</span></span> <span data-ttu-id="18ac8-291">예를 들어과 같은 URL을 사용 하 여 페이지를 호출할 수 없습니다 `http://localhost:nnnnn/EditMovie?id=abc`합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-291">For example, the page could be invoked with a URL like `http://localhost:nnnnn/EditMovie?id=abc`.</span></span>
- <span data-ttu-id="18ac8-292">ID는 숫자로 하지만 존재 하지 않는 동영상 참조 (예를 들어 `http://localhost:nnnnn/EditMovie?id=100934`).</span><span class="sxs-lookup"><span data-stu-id="18ac8-292">The ID is a number, but it references a movie that doesn't exist (for example, `http://localhost:nnnnn/EditMovie?id=100934`).</span></span>

<span data-ttu-id="18ac8-293">원하는 경우 이러한 Url을 실행에서 발생 하는 오류를 확인 하려면 합니다 *영화* 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-293">If you're curious to see the errors that result from these URLs, run the *Movies* page.</span></span> <span data-ttu-id="18ac8-294">동영상을 편집 하려면 선택 하 고 다음의 URL을 변경 합니다 *EditMovie* 알파벳을 포함 하는 URL로 페이지 ID 또는 존재 하지 않는 동영상의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-294">Select a movie to edit, and then change the URL of the *EditMovie* page to a URL that contains an alphabetic ID or the ID of a non-existent movie.</span></span>

<span data-ttu-id="18ac8-295">따라서 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="18ac8-295">So what should you do?</span></span> <span data-ttu-id="18ac8-296">첫 번째 해결 뿐만 아니라 ID 전달 되도록 페이지로 이지만 ID는 정수는 있는지 확인 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-296">The first fix is to make sure that not only is an ID passed to the page, but that the ID is an integer.</span></span> <span data-ttu-id="18ac8-297">코드를 변경 합니다 `!IsPost` 이 예제와 같이 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-297">Change the code for the `!IsPost` test to look like this example:</span></span>

[!code-csharp[Main](updating-data/samples/sample14.cs)]

<span data-ttu-id="18ac8-298">두 번째 조건을 추가한 합니다 `IsEmpty` 테스트를 사용 하 여 연결 된 `&&` (논리적 AND):</span><span class="sxs-lookup"><span data-stu-id="18ac8-298">You've added a second condition to the `IsEmpty` test, linked with `&&` (logical AND):</span></span>

[!code-csharp[Main](updating-data/samples/sample15.cs)]

<span data-ttu-id="18ac8-299">기억 될 수 있습니다 합니다 [ASP.NET 웹 페이지 프로그래밍 소개](../introducing-razor-syntax-c.md) 자습서와 같은 메서드는 `AsBool` 는 `AsInt` 문자열 일부 다른 데이터 형식으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-299">You might remember from the [Introduction to ASP.NET Web Pages Programming](../introducing-razor-syntax-c.md) tutorial that methods like `AsBool` an `AsInt` convert a character string to some other data type.</span></span> <span data-ttu-id="18ac8-300">`IsInt` 메서드 (다른 사용자와 `IsBool` 고 `IsDateTime`) 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-300">The `IsInt` method (and others, like `IsBool` and `IsDateTime`) are similar.</span></span> <span data-ttu-id="18ac8-301">그러나만 테스트 하는지 여부를 있습니다 *수* 실제로 변환을 수행 하지 않고 문자열을 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-301">However, they test only whether you *can* convert the string, without actually performing the conversion.</span></span> <span data-ttu-id="18ac8-302">기본적으로 이야기 여기 *쿼리 문자열 값을 정수로 변환할 수 있는 경우...* .</span><span class="sxs-lookup"><span data-stu-id="18ac8-302">So here you're essentially saying *If the query string value can be converted to an integer ...*.</span></span>

<span data-ttu-id="18ac8-303">존재 하지 않는 동영상은 다른 잠재적인 문제를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-303">The other potential problem is looking for a movie that doesn't exist.</span></span> <span data-ttu-id="18ac8-304">동영상 코드를이 코드와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-304">The code to get a movie looks like this code:</span></span>

[!code-csharp[Main](updating-data/samples/sample16.cs)]

<span data-ttu-id="18ac8-305">전달 하는 경우는 `movieId` 값을 `QuerySingle` 오는 문이 및 실제 동영상에 해당 하지 않는 메서드, 아무 것도 반환 (예를 들어 `title=row.Title`) 오류를 발생 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-305">If you pass a `movieId` value to the `QuerySingle` method that doesn't correspond to an actual movie, nothing is returned and the statements that follow (for example, `title=row.Title`) result in errors.</span></span>

<span data-ttu-id="18ac8-306">다시는 쉽게 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-306">Again there's an easy fix.</span></span> <span data-ttu-id="18ac8-307">경우는 `db.QuerySingle` 없는 결과 반환 하는 메서드는 `row` 변수는 null이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-307">If the `db.QuerySingle` method returns no results, the `row` variable will be null.</span></span> <span data-ttu-id="18ac8-308">확인할 수 있는지 여부를 `row` 에서 값을 가져오려고 시도 하기 전에 변수가 null 이면 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-308">So you can check whether the `row` variable is null before you try to get values from it.</span></span> <span data-ttu-id="18ac8-309">다음 코드를 추가 하는 `if` 블록의 값을 얻으려면 있는 문 주위를 `row` 개체:</span><span class="sxs-lookup"><span data-stu-id="18ac8-309">The following code adds an `if` block around the statements that get the values out of the `row` object:</span></span>

[!code-csharp[Main](updating-data/samples/sample17.cs)]

<span data-ttu-id="18ac8-310">이러한 두 가지 추가 유효성 검사 테스트를 사용 하 여 페이지에는 더 완벽 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-310">With these two additional validation tests, the page becomes more bullet-proof.</span></span> <span data-ttu-id="18ac8-311">에 대 한 전체 코드는 `!IsPost` 분기는 이제이 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-311">The complete code for the `!IsPost` branch now looks like this example:</span></span>

[!code-csharp[Main](updating-data/samples/sample18.cs)]

<span data-ttu-id="18ac8-312">했습니다 보면 번이 작업에 대 한 적절 하 게 사용 인지는 `else` 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-312">We'll note once more that this task is a good use for an `else` block.</span></span> <span data-ttu-id="18ac8-313">테스트에 전달 하지는 `else` 블록 오류 메시지를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-313">If the tests don't pass, the `else` blocks set error messages.</span></span>

## <a name="adding-a-link-to-return-to-the-movies-page"></a><span data-ttu-id="18ac8-314">Movies 페이지로 반환에 대 한 링크를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-314">Adding a Link to Return to the Movies Page</span></span>

<span data-ttu-id="18ac8-315">최종 하 고 유용한 세부 정보 링크를 추가 하는 것으로 *영화* 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-315">A final and helpful detail is to add a link back to the *Movies* page.</span></span> <span data-ttu-id="18ac8-316">이벤트의 일반 흐름에서 사용자에 시작 됩니다 합니다 *영화* 페이지를 **편집** 링크.</span><span class="sxs-lookup"><span data-stu-id="18ac8-316">In the ordinary flow of events, users will start at the *Movies* page and click an **Edit** link.</span></span> <span data-ttu-id="18ac8-317">제공 하는 합니다 *EditMovie* 페이지에서 동영상을 편집 하 고 단추를 클릭 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-317">That brings them to the *EditMovie* page, where they can edit the movie and click the button.</span></span> <span data-ttu-id="18ac8-318">코드 변경 내용을 처리 한 후 다시 리디렉션합니다 합니다 *영화* 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-318">After the code processes the change, it redirects back to the *Movies* page.</span></span>

<span data-ttu-id="18ac8-319">단,</span><span class="sxs-lookup"><span data-stu-id="18ac8-319">However:</span></span>

- <span data-ttu-id="18ac8-320">사용자는 아무 것도 변경할 필요가 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-320">The user might decide not to change anything.</span></span>
- <span data-ttu-id="18ac8-321">사용자 클릭 하지 않고이 페이지에 수신를 **편집할** 링크를 *영화* 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-321">The user might have gotten to this page without first clicking an **Edit** link in the *Movies* page.</span></span>

<span data-ttu-id="18ac8-322">기본 목록에 반환 하기 위해 쉽게 하려는 어느 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-322">Either way, you want to make it easy for them to return to the main listing.</span></span> <span data-ttu-id="18ac8-323">쉽게 해결할 수 있습니다 &mdash; 닫은 직후 다음 태그를 추가 `</form>` 태그에 태그:</span><span class="sxs-lookup"><span data-stu-id="18ac8-323">It's an easy fix &mdash; add the following markup just after the closing `</form>` tag in the markup:</span></span>

[!code-html[Main](updating-data/samples/sample19.html)]

<span data-ttu-id="18ac8-324">이 태그에 대 한 동일한 구문을 사용 하는 `<a>` 다른 곳에서 볼 수 있는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-324">This markup uses the same syntax for an `<a>` element that you've seen elsewhere.</span></span> <span data-ttu-id="18ac8-325">URL에 포함 `~` "웹 사이트의 루트입니다."를 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-325">The URL includes `~` to mean "root of the website."</span></span>

## <a name="testing-the-movie-update-process"></a><span data-ttu-id="18ac8-326">영화 업데이트 프로세스를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-326">Testing the Movie Update Process</span></span>

<span data-ttu-id="18ac8-327">이제 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-327">Now you can test.</span></span> <span data-ttu-id="18ac8-328">실행 합니다 *영화* 페이지 및 클릭 **편집** 동영상 옆에 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-328">Run the *Movies* page, and click **Edit** next to a movie.</span></span> <span data-ttu-id="18ac8-329">경우는 *EditMovie* 페이지가 표시 되 면 변경 하 고 영화 **변경 내용 전송**합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-329">When the *EditMovie* page appears, make changes to the movie and click **Submit Changes**.</span></span> <span data-ttu-id="18ac8-330">영화 목록에 표시 되 면 변경 내용을 표시 되는 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-330">When the movie listing appears, make sure that your changes are shown.</span></span>

<span data-ttu-id="18ac8-331">유효성 검사 작동 하는지 확인, 클릭 **편집** 다른 동영상에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-331">To make sure that validation is working, click **Edit** for another movie.</span></span> <span data-ttu-id="18ac8-332">에 표시 되는 경우는 *EditMovie* 페이지의 선택을 취소 합니다 **장르** 필드 (또는 **연도** 필드 또는 둘 다) 변경 내용을 제출 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-332">When you get to the *EditMovie* page, clear the **Genre** field (or **Year** field, or both) and try to submit your changes.</span></span> <span data-ttu-id="18ac8-333">예상한 대로 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-333">You'll see an error, as you'd expect:</span></span>

![유효성 검사 오류를 보여 주는 동영상 페이지 편집](updating-data/_static/image4.png)

<span data-ttu-id="18ac8-335">클릭 합니다 **영화 목록에 반환** 여 변경 내용을 반환 하는 링크는 *영화* 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-335">Click the **Return to movie listing** link to abandon your changes and return to the *Movies* page.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="18ac8-336">다음에 나오는</span><span class="sxs-lookup"><span data-stu-id="18ac8-336">Coming Up Next</span></span>

<span data-ttu-id="18ac8-337">다음 자습서에서는 영화 레코드를 삭제 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="18ac8-337">In the next tutorial, you'll see how to delete a movie record.</span></span>

## <a name="complete-listing-for-movie-page-updated-with-edit-links"></a><span data-ttu-id="18ac8-338">동영상 페이지 (편집 링크를 사용 하 여 업데이트)에 대 한 전체 목록</span><span class="sxs-lookup"><span data-stu-id="18ac8-338">Complete Listing for Movie Page (Updated with Edit Links)</span></span>

[!code-cshtml[Main](updating-data/samples/sample20.cshtml)]

<a id="Complete_Page_Listing_for_EditMovie"></a>
## <a name="complete-page-listing-for-edit-movie-page"></a><span data-ttu-id="18ac8-339">전체 페이지 목록 편집 동영상 페이지</span><span class="sxs-lookup"><span data-stu-id="18ac8-339">Complete Page Listing for Edit Movie Page</span></span>

[!code-cshtml[Main](updating-data/samples/sample21.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="18ac8-340">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="18ac8-340">Additional Resources</span></span>

- [<span data-ttu-id="18ac8-341">Razor 구문을 사용 하 여 ASP.NET 웹 프로그래밍 소개</span><span class="sxs-lookup"><span data-stu-id="18ac8-341">Introduction to ASP.NET Web Programming by Using the Razor Syntax</span></span>](../../getting-started/introducing-razor-syntax-c.md)
- <span data-ttu-id="18ac8-342">[SQL UPDATE 문을](http://www.w3schools.com/sql/sql_update.asp) W3Schools 사이트</span><span class="sxs-lookup"><span data-stu-id="18ac8-342">[SQL UPDATE Statement](http://www.w3schools.com/sql/sql_update.asp) on the W3Schools site</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="18ac8-343">[이전](entering-data.md)
> [다음](deleting-data.md)</span><span class="sxs-lookup"><span data-stu-id="18ac8-343">[Previous](entering-data.md)
[Next](deleting-data.md)</span></span>
