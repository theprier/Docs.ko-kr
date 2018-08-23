---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/deleting-data
title: ASP.NET 웹 페이지 소개-데이터베이스 데이터를 삭제 합니다. | Microsoft Docs
author: tfitzmac
description: 이 자습서에서는 개별 데이터베이스 항목을 삭제 하는 방법을 보여 줍니다. 이 ASP.NET 웹 Pa.에서 데이터베이스 데이터 업데이트를 통해 시리즈를 완료 했다고 가정...
ms.author: riande
ms.date: 01/02/2018
ms.assetid: 75b5c1cf-84bd-434f-8a86-85c568eb5b09
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/deleting-data
msc.type: authoredcontent
ms.openlocfilehash: 3b759a5c88b066640005c823ce0cc3cc3ac89bc2
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41838783"
---
<a name="introducing-aspnet-web-pages---deleting-database-data"></a><span data-ttu-id="65fdc-104">ASP.NET 웹 페이지 소개-데이터베이스 데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="65fdc-104">Introducing ASP.NET Web Pages - Deleting Database Data</span></span>
====================
<span data-ttu-id="65fdc-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="65fdc-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="65fdc-106">이 자습서에서는 개별 데이터베이스 항목을 삭제 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-106">This tutorial shows you how to delete an individual database entry.</span></span> <span data-ttu-id="65fdc-107">통해 시리즈를 완료 했다고 가정 하 [ASP.NET 웹 페이지에서 데이터베이스 데이터 업데이트](updating-data.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-107">It assumes you have completed the series through [Updating Database Data in ASP.NET Web Pages](updating-data.md).</span></span>
> 
> <span data-ttu-id="65fdc-108">학습할 내용:</span><span class="sxs-lookup"><span data-stu-id="65fdc-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="65fdc-109">레코드의 목록에서 개별 레코드를 선택 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-109">How to select an individual record from a listing of records.</span></span>
> - <span data-ttu-id="65fdc-110">데이터베이스에서 단일 레코드를 삭제 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="65fdc-110">How to delete a single record from a database.</span></span>
> - <span data-ttu-id="65fdc-111">형태로 특정 단추 클릭을 확인 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-111">How to check that a specific button was clicked in a form.</span></span>
>   
> 
> <span data-ttu-id="65fdc-112">기능/기술을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-112">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="65fdc-113">`WebGrid` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-113">The `WebGrid` helper.</span></span>
> - <span data-ttu-id="65fdc-114">SQL `Delete` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-114">The SQL `Delete` command.</span></span>
> - <span data-ttu-id="65fdc-115">합니다 `Database.Execute` SQL을 실행 하는 방법 `Delete` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-115">The `Database.Execute` method to run a SQL `Delete` command.</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="65fdc-116">만들 내용</span><span class="sxs-lookup"><span data-stu-id="65fdc-116">What You'll Build</span></span>

<span data-ttu-id="65fdc-117">이전 자습서에서는 기존 데이터베이스 레코드를 업데이트 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-117">In the previous tutorial, you learned how to update an existing database record.</span></span> <span data-ttu-id="65fdc-118">이 자습서는 마찬가지로 점을 제외 하 고 레코드를 업데이트 하는 대신 하면 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-118">This tutorial is similar, except that instead of updating the record, you'll delete it.</span></span> <span data-ttu-id="65fdc-119">프로세스는 동일 하며 점을 제외 하 고 삭제 하는이 자습서 짧은 이므로 더 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-119">The processes are much the same, except that deleting is simpler, so this tutorial will be short.</span></span>

<span data-ttu-id="65fdc-120">에 *영화* 에서는 업데이트 페이지는 `WebGrid` 도우미를 표시 하도록를 **삭제** 함께 각 영화 옆에 있는 링크를 **편집** 이전에 추가한 링크.</span><span class="sxs-lookup"><span data-stu-id="65fdc-120">In the *Movies* page, you'll update the `WebGrid` helper so that it displays a **Delete** link next to each movie to accompany the **Edit** link you added earlier.</span></span>

![각 영화에 대 한 삭제 링크를 보여 주는 동영상 페이지](deleting-data/_static/image1.png)

<span data-ttu-id="65fdc-122">편집 마찬가지로 클릭할 때 합니다 **삭제** 링크 걸리는 다른 페이지에 있는 영화 정보를 이미 형식에서:</span><span class="sxs-lookup"><span data-stu-id="65fdc-122">As with editing, when you click the **Delete** link, it takes you to a different page, where the movie information is already in a form:</span></span>

![영화 표시를 사용 하 여 동영상 페이지 삭제](deleting-data/_static/image2.png)

<span data-ttu-id="65fdc-124">레코드를 영구적으로 삭제 단추를 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-124">You can then click the button to delete the record permanently.</span></span>

## <a name="adding-a-delete-link-to-the-movie-listing"></a><span data-ttu-id="65fdc-125">영화 목록에 삭제 링크를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-125">Adding a Delete Link to the Movie Listing</span></span>

<span data-ttu-id="65fdc-126">추가 하 여 먼저를 **삭제할** 연결할를 `WebGrid` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-126">You'll start by adding a **Delete** link to the `WebGrid` helper.</span></span> <span data-ttu-id="65fdc-127">이 링크는 비슷합니다는 **편집** 이전 자습서에서 추가한 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-127">This link is similar to the **Edit** link you added in a previous tutorial.</span></span>

<span data-ttu-id="65fdc-128">엽니다는 *Movies.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-128">Open the *Movies.cshtml* file.</span></span>

<span data-ttu-id="65fdc-129">변경 된 `WebGrid` 열을 추가 하 여 페이지의 본문에는 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-129">Change the `WebGrid` markup in the body of the page by adding a column.</span></span> <span data-ttu-id="65fdc-130">수정 된 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-130">Here's the modified markup:</span></span>

[!code-html[Main](deleting-data/samples/sample1.html?highlight=9-10)]

<span data-ttu-id="65fdc-131">새 열이이 같습니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-131">The new column is this one:</span></span>

[!code-html[Main](deleting-data/samples/sample2.html)]

<span data-ttu-id="65fdc-132">표를 구성 하는 방법은 합니다 **편집** 열은 표의 맨 왼쪽 및 **삭제** 열이 오른쪽에 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-132">The way the grid is configured, the **Edit** column is leftmost in the grid and the **Delete** column is rightmost.</span></span> <span data-ttu-id="65fdc-133">(뒤에 나오는 쉼표는는 `Year` 열 이제는 확인 하지 않은 경우.) 이러한 링크 열으로 이동 하는 방법에 대 한 특별 하 고 서로 옆에 쉽게 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-133">(There's a comma after the `Year` column now, in case you didn't notice that.) There's nothing special about where these link columns go, and you could as easily put them next to each other.</span></span> <span data-ttu-id="65fdc-134">이 경우 혼합 하기가 있도록 별도 일입니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-134">In this case, they're separate to make them harder to get mixed up.</span></span>

![편집 및 세부 정보 링크를 사용 하 여 영화 페이지가 표시 되지 않았다고 서로 옆에 표시 하려면](deleting-data/_static/image3.png)

<span data-ttu-id="65fdc-136">새 열의 링크를 보여 줍니다 (`<a>` 요소) "삭제" 이라고 표시 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-136">The new column shows a link (`<a>` element) whose text says "Delete".</span></span> <span data-ttu-id="65fdc-137">링크의 대상 (해당 `href` 특성)은 사용 하 여이 URL 같이 궁극적으로 확인 되는 코드는 `id` 각 영화에 대 한 다른 값:</span><span class="sxs-lookup"><span data-stu-id="65fdc-137">The target of the link (its `href` attribute) is code that ultimately resolves to something like this URL, with the `id` value different for each movie:</span></span>

[!code-css[Main](deleting-data/samples/sample3.css)]

<span data-ttu-id="65fdc-138">이 링크는 라는 페이지를 호출 *DeleteMovie* 선택한 영화 ID를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-138">This link will invoke a page named *DeleteMovie* and pass it the ID of the movie you've selected.</span></span>

<span data-ttu-id="65fdc-139">이 자습서 다루지는이 링크를 생성 하는 방법에 대 한 정보는 거의 동일 하기 때문에 합니다 **편집** 이전 자습서에서 링크 ([ASP.NET 웹 페이지에서 데이터베이스 데이터 업데이트](updating-data.md)).</span><span class="sxs-lookup"><span data-stu-id="65fdc-139">This tutorial won't go into detail about how this link is constructed, because it's almost identical to the **Edit** link from the previous tutorial ([Updating Database Data in ASP.NET Web Pages](updating-data.md)).</span></span>

## <a name="creating-the-delete-page"></a><span data-ttu-id="65fdc-140">삭제 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="65fdc-140">Creating the Delete Page</span></span>

<span data-ttu-id="65fdc-141">이제의 대상이 될 페이지를 만들 수는 **삭제** 표에 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-141">Now you can create the page that will be the target for the **Delete** link in the grid.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="65fdc-142">**중요 한** 을 먼저 삭제할 레코드를 선택 하 고 다음 단추를 별도 페이지 확인 프로세스를 사용 하는 방법은 보안을 위해 매우 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-142">**Important** The technique of first selecting a record to delete and then using a separate page and button to confirm the process is extremely important for security.</span></span> <span data-ttu-id="65fdc-143">이전 자습서에서 읽었다고으로 만드는 *모든* 종류의 웹 사이트를 변경 해야 *항상* 수행 폼을 사용 하 여 &mdash; 즉, HTTP POST 작업을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-143">As you've read in previous tutorials, making *any* sort of change to your website should *always* be done using a form &mdash; that is, using an HTTP POST operation.</span></span> <span data-ttu-id="65fdc-144">변경한 링크 (사용 하 여 가져오기 작업을)를 클릭 하 여 사이트를 변경할 수, 사용자 사이트에 대 한 간단한 요청할 수 고 데이터를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-144">If you made it possible to change the site just by clicking a link (that is, using a GET operation), people could make simple requests to your site and delete your data.</span></span> <span data-ttu-id="65fdc-145">가 사이트를 인덱싱하는 검색 엔진 크롤러도 다음 링크 하 여 데이터를 실수로 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-145">Even a search-engine crawler that's indexing your site could inadvertently delete data just by following links.</span></span>
> 
> <span data-ttu-id="65fdc-146">레코드를 변경 하는 사람에 게 앱을 계속 편집에 대 한 사용자에 게 레코드를 표시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-146">When your app lets people change a record, you have to present the record to the user for editing anyway.</span></span> <span data-ttu-id="65fdc-147">하지만 단일 레코드 삭제에 대해이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-147">But you might be tempted to skip this step for deleting a record.</span></span> <span data-ttu-id="65fdc-148">그러나 해당 단계를 건너뜁니다 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="65fdc-148">Don't skip that step, though.</span></span> <span data-ttu-id="65fdc-149">(유용도 사용자가 레코드를 참조 하 여 이러한 레코드를 삭제 하는 것을 확인 합니다.)</span><span class="sxs-lookup"><span data-stu-id="65fdc-149">(It's also helpful for users to see the record and confirm that they're deleting the record that they intended.)</span></span>
> 
> <span data-ttu-id="65fdc-150">후속 자습서 집합에서 사용자가 레코드를 삭제 하기 전에 로그인 해야 하므로 로그인 기능을 추가 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-150">In a subsequent tutorial set, you'll see how to add login functionality so a user would have to log in before deleting a record.</span></span>


<span data-ttu-id="65fdc-151">라는 페이지를 만듭니다 *DeleteMovie.cshtml* 다음 태그를 사용 하 여 파일에 포함 된 내용으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-151">Create a page named *DeleteMovie.cshtml* and replace what's in the file with the following markup:</span></span>

[!code-cshtml[Main](deleting-data/samples/sample4.cshtml)]

<span data-ttu-id="65fdc-152">이 태그와 비슷합니다는 *EditMovie* 텍스트 상자를 사용 하는 대신 페이지 (`<input type="text">`), 태그 `<span>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-152">This markup is like the *EditMovie* pages, except that instead of using text boxes (`<input type="text">`), the markup includes `<span>` elements.</span></span> <span data-ttu-id="65fdc-153">아무것도 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-153">There's nothing here to edit.</span></span> <span data-ttu-id="65fdc-154">사용자는 오른쪽 동영상을 삭제 하는 않는지 확인 수 있도록 영화 세부 정보를 표시 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-154">All you have to do is display the movie details so that users can make sure that they're deleting the right movie.</span></span>

<span data-ttu-id="65fdc-155">태그는 사용자가 영화 목록 페이지에 반환할 수 있는 링크가 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-155">The markup already contains a link that lets the user return to the movie listing page.</span></span>

<span data-ttu-id="65fdc-156">에서처럼 합니다 *EditMovie* 페이지에서 선택한 동영상의 ID는 숨겨진된 필드에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-156">As in the *EditMovie* page, the ID of the selected movie is stored in a hidden field.</span></span> <span data-ttu-id="65fdc-157">(전달 됩니다 페이지에 처음에 쿼리 문자열 값으로.) `Html.ValidationSummary` 유효성 검사 오류를 표시 하는 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-157">(It's passed into the page in the first place as a query string value.) There's an `Html.ValidationSummary` call that will display validation errors.</span></span> <span data-ttu-id="65fdc-158">이 경우 오류는 영화 ID가 없습니다. 페이지에 전달한 또는 영화 ID 올바르지 않습니다 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-158">In this case, the error might be that no movie ID was passed to the page or that the movie ID is invalid.</span></span> <span data-ttu-id="65fdc-159">누군가가에서 동영상을 먼저 선택 하지 않고이 페이지를 실행 하는 경우이 상황이 발생할 수는 *영화* 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-159">This situation could occur if someone ran this page without first selecting a movie in the *Movies* page.</span></span>

<span data-ttu-id="65fdc-160">단추 캡션이 **삭제 영화**, 해당 이름 특성은로 설정 하 고 `buttonDelete`입니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-160">The button caption is **Delete Movie**, and its name attribute is set to `buttonDelete`.</span></span> <span data-ttu-id="65fdc-161">`name` 특성은 양식을 제출 하는 단추를 식별 하는 코드에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-161">The `name` attribute will be used in the code to identify the button that submitted the form.</span></span>

<span data-ttu-id="65fdc-162">1) 페이지를 처음 표시할 때 영화 세부 정보를 읽는 코드를 작성 하 고 2) 실제로 사용자가 단추를 클릭할 때 동영상을 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-162">You'll have to write code to 1) read the movie details when the page is first displayed and 2) actually delete the movie when the user clicks the button.</span></span>

## <a name="adding-code-to-read-a-single-movie"></a><span data-ttu-id="65fdc-163">단일 동영상을 읽는 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-163">Adding Code to Read a Single Movie</span></span>

<span data-ttu-id="65fdc-164">맨 위에 있는 합니다 *DeleteMovie.cshtml* 페이지에서 다음 코드 블록을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-164">At the top of the *DeleteMovie.cshtml* page, add the following code block:</span></span>

[!code-cshtml[Main](deleting-data/samples/sample5.cshtml)]

<span data-ttu-id="65fdc-165">이 태그에 해당 하는 코드와 동일 합니다 *EditMovie* 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-165">This markup is the same as the corresponding code in the *EditMovie* page.</span></span> <span data-ttu-id="65fdc-166">쿼리 문자열에서 영화 ID를 가져옵니다 하 고 ID를 사용 하 여 데이터베이스에서 레코드를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-166">It gets the movie ID out of the query string and uses the ID to read a record from the database.</span></span> <span data-ttu-id="65fdc-167">유효성 검사 테스트를 포함 하는 코드 (`IsInt()` 및 `row != null`) 페이지에 전달 되는 영화 ID가 올바른지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-167">The code includes the validation test (`IsInt()` and `row != null`) to make sure that the movie ID being passed to the page is valid.</span></span>

<span data-ttu-id="65fdc-168">이 코드 페이지 실행 처음으로 실행 해야만 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-168">Remember that this code should only run the first time the page runs.</span></span> <span data-ttu-id="65fdc-169">클릭할 때 데이터베이스에서 동영상 레코드를 다시 읽을 않으려는 합니다 **영화 삭제** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-169">You don't want to re-read the movie record from the database when the user clicks the **Delete Movie** button.</span></span> <span data-ttu-id="65fdc-170">테스트 라는 내부 영화를 읽을 수 있으므로 코드 `if(!IsPost)` &mdash; 이므로 *요청은 post 작업이 (폼 제출) 하는 경우*합니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-170">Therefore, code to read the movie is inside a test that says `if(!IsPost)` &mdash; that is, *if the request is not a post operation (form submission)*.</span></span>

## <a name="adding-code-to-delete-the-selected-movie"></a><span data-ttu-id="65fdc-171">선택한 동영상을 삭제 하는 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-171">Adding Code to Delete the Selected Movie</span></span>

<span data-ttu-id="65fdc-172">파일을 사용자가 단추를 클릭할 때 동영상을 삭제 하려면의 닫는 중괄호 바로 안에 다음 코드를 추가 합니다 `@` 블록:</span><span class="sxs-lookup"><span data-stu-id="65fdc-172">To delete the movie when the user clicks the button, add the following code just inside the closing brace of the `@` block:</span></span>

[!code-csharp[Main](deleting-data/samples/sample6.cs)]

<span data-ttu-id="65fdc-173">이 코드는 기존 레코드를 업데이트 하는 것에 대 한 코드와 유사 하지만 더 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-173">This code is similar to the code for updating an existing record, but simpler.</span></span> <span data-ttu-id="65fdc-174">이 코드는 기본적으로 SQL 실행 `Delete` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-174">The code basically runs a SQL `Delete` statement.</span></span>

 <span data-ttu-id="65fdc-175">에서처럼 합니다 *EditMovie* 코드는 페이지는 `if(IsPost)` 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-175">As in the *EditMovie* page, the code is in an `if(IsPost)` block.</span></span> <span data-ttu-id="65fdc-176">이 이번에는 `if()` 조건은 좀 더 복잡 합니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-176">This time, the `if()` condition is a little more complicated:</span></span> 

[!code-csharp[Main](deleting-data/samples/sample7.cs)]

<span data-ttu-id="65fdc-177">두 조건을 여기 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-177">There are two conditions here.</span></span> <span data-ttu-id="65fdc-178">첫 번째 페이지가 제출 되는 전에 살펴본 것 처럼 됩니다 &mdash; `if(IsPost)`합니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-178">The first is that the page is being submitted, as you've seen before &mdash; `if(IsPost)`.</span></span>

<span data-ttu-id="65fdc-179">두 번째 조건은 `!Request["buttonDelete"].IsEmpty()`, 즉 요청 라는 개체에 `buttonDelete`입니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-179">The second condition is `!Request["buttonDelete"].IsEmpty()`, meaning that the request has an object named `buttonDelete`.</span></span> <span data-ttu-id="65fdc-180">사실 어떤 단추 양식을 제출 테스트는 간접 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-180">Admittedly, it's an indirect way of testing which button submitted the form.</span></span> <span data-ttu-id="65fdc-181">여러 전송 단추를 포함 하는 경우 요청에서 클릭 된 단추의 이름만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-181">If a form contains multiple submit buttons, only the name of the button that was clicked appears in the request.</span></span> <span data-ttu-id="65fdc-182">따라서, 논리적으로 특정 단추의 이름을 요청 하는 경우 나타나는 &mdash; 단추를 비어 있지 않은 경우 코드에 명시 된 대로 또는 &mdash; 양식을 제출 하는 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-182">Therefore, logically, if the name of a particular button appears in the request &mdash; or as stated in the code, if that button isn't empty &mdash; that's the button that submitted the form.</span></span>

<span data-ttu-id="65fdc-183">`&&` 연산자 의미 "및" (논리적 AND).</span><span class="sxs-lookup"><span data-stu-id="65fdc-183">The `&&` operator means "and" (logical AND).</span></span> <span data-ttu-id="65fdc-184">따라서 전체 `if` 조건은...</span><span class="sxs-lookup"><span data-stu-id="65fdc-184">Therefore the entire `if` condition is ...</span></span>

<span data-ttu-id="65fdc-185">*이 요청은 post (처음 요청 될 수는 없음)*</span><span class="sxs-lookup"><span data-stu-id="65fdc-185">*This request is a post (not a first-time request)*</span></span>  
  
 <span data-ttu-id="65fdc-186">AND</span><span class="sxs-lookup"><span data-stu-id="65fdc-186">AND</span></span>  
  
<span data-ttu-id="65fdc-187">*합니다* `buttonDelete` *단추 된 양식을 제출 하는 단추가 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="65fdc-187">*The* `buttonDelete`*button was the button that submitted the form.*</span></span>

<span data-ttu-id="65fdc-188">(사실,이 페이지)이이 폼에는 단추 하나만 있으므로 대 한 추가 테스트 `buttonDelete` 기술적으로 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-188">This form (in fact, this page) contains only one button, so the additional test for `buttonDelete` is technically not required.</span></span> <span data-ttu-id="65fdc-189">그러나 하려는 데이터를 영구적으로 제거 하는 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-189">Still, you're about to perform an operation that will permanently remove data.</span></span> <span data-ttu-id="65fdc-190">따라서 사용자가 명시적으로 요청 하는 경우에 작업을 수행 하는 가능한 해야 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-190">So you want to be as sure as possible that you're performing the operation only when the user has explicitly requested it.</span></span> <span data-ttu-id="65fdc-191">예를 들어 나중에이 페이지를 확장 하 여 다른 단추를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-191">For example, suppose that you expanded this page later and added other buttons to it.</span></span> <span data-ttu-id="65fdc-192">경우에 동영상을 삭제 하는 코드를 실행 하는 경우에는 `buttonDelete` 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-192">Even then, the code that deletes the movie will run only if the `buttonDelete` button was clicked.</span></span>

<span data-ttu-id="65fdc-193">에서처럼 합니다 *EditMovie* 페이지 ID에서 숨겨진된 필드를 얻고 다음 SQL 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-193">As in the *EditMovie* page, you get the ID from the hidden field and then run the SQL command.</span></span> <span data-ttu-id="65fdc-194">구문은 `Delete` 문은:</span><span class="sxs-lookup"><span data-stu-id="65fdc-194">The syntax for the `Delete` statement is:</span></span>

`DELETE FROM table WHERE ID = value`

<span data-ttu-id="65fdc-195">포함 하는 중요 한 것은 `WHERE` 절 및 ID</span><span class="sxs-lookup"><span data-stu-id="65fdc-195">It's vital to include the `WHERE` clause and the ID.</span></span> <span data-ttu-id="65fdc-196">WHERE 절을 생략 하면 *테이블의 모든 레코드가 삭제 됩니다*합니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-196">If you leave out the WHERE clause, *all the records in the table will be deleted*.</span></span> <span data-ttu-id="65fdc-197">앞에서 설명한 것 처럼 전달 ID 값을 SQL 명령 자리 표시자를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-197">As you have seen, you pass the ID value to the SQL command by using a placeholder.</span></span>

## <a name="testing-the-movie-delete-process"></a><span data-ttu-id="65fdc-198">영화 삭제 프로세스를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-198">Testing the Movie Delete Process</span></span>

<span data-ttu-id="65fdc-199">이제 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-199">Now you can test.</span></span> <span data-ttu-id="65fdc-200">실행 합니다 *영화* 페이지 및 클릭 **삭제** 동영상 옆에 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-200">Run the *Movies* page, and click **Delete** next to a movie.</span></span> <span data-ttu-id="65fdc-201">경우는 *DeleteMovie* 페이지에 표시 되 면 클릭 **영화 삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-201">When the *DeleteMovie* page appears, click **Delete Movie**.</span></span>

![영화 삭제 단추가 강조 표시 된 동영상 페이지 삭제](deleting-data/_static/image4.png)

<span data-ttu-id="65fdc-203">단추를 클릭 하면 코드는 영화를 삭제 하 고 동영상 목록을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-203">When you click the button, the code deletes the movies and returns to the movie listing.</span></span> <span data-ttu-id="65fdc-204">삭제 된 영화를 검색할 수 있는 삭제 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-204">There you can search for the deleted movie and confirm that it's been deleted.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="65fdc-205">다음에 나오는</span><span class="sxs-lookup"><span data-stu-id="65fdc-205">Coming Up Next</span></span>

<span data-ttu-id="65fdc-206">다음 자습서는 일반적인 모양과 레이아웃 사이트에서 모든 페이지를 제공 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="65fdc-206">The next tutorial shows you how to give all the pages on your site a common look and layout.</span></span>

## <a name="complete-listing-for-movie-page-updated-with-delete-links"></a><span data-ttu-id="65fdc-207">동영상 페이지 (삭제 링크를 사용 하 여 업데이트)에 대 한 전체 목록</span><span class="sxs-lookup"><span data-stu-id="65fdc-207">Complete Listing for Movie Page (Updated with Delete Links)</span></span>

[!code-cshtml[Main](deleting-data/samples/sample8.cshtml)]

## <a name="complete-listing-for-deletemovie-page"></a><span data-ttu-id="65fdc-208">DeleteMovie 페이지에 대 한 전체 목록</span><span class="sxs-lookup"><span data-stu-id="65fdc-208">Complete Listing for DeleteMovie Page</span></span>

[!code-cshtml[Main](deleting-data/samples/sample9.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="65fdc-209">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="65fdc-209">Additional Resources</span></span>

- [<span data-ttu-id="65fdc-210">Razor 구문을 사용 하 여 ASP.NET 웹 프로그래밍 소개</span><span class="sxs-lookup"><span data-stu-id="65fdc-210">Introduction to ASP.NET Web Programming by Using the Razor Syntax</span></span>](../introducing-razor-syntax-c.md)
- <span data-ttu-id="65fdc-211">[SQL DELETE 문을](http://www.w3schools.com/sql/sql_delete.asp) W3Schools 사이트</span><span class="sxs-lookup"><span data-stu-id="65fdc-211">[SQL DELETE Statement](http://www.w3schools.com/sql/sql_delete.asp) on the W3Schools site</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="65fdc-212">[이전](updating-data.md)
> [다음](layouts.md)</span><span class="sxs-lookup"><span data-stu-id="65fdc-212">[Previous](updating-data.md)
[Next](layouts.md)</span></span>
