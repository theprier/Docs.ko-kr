---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/deleting-data
title: Introducing ASP.NET 웹 페이지-데이터베이스 데이터를 삭제 합니다. | Microsoft Docs
author: tfitzmac
description: 이 자습서는 개별 데이터베이스 항목을 삭제 하는 방법을 보여 줍니다. ASP.NET 웹 Pa.에서 데이터베이스 데이터 업데이트를 통해 시리즈를 완료 했습니다.. 가정
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/02/2018
ms.topic: article
ms.assetid: 75b5c1cf-84bd-434f-8a86-85c568eb5b09
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/deleting-data
msc.type: authoredcontent
ms.openlocfilehash: 146199e862cd6fa2607671d31633476b1cb67021
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30897438"
---
<a name="introducing-aspnet-web-pages---deleting-database-data"></a><span data-ttu-id="35271-104">Introducing ASP.NET 웹 페이지-데이터베이스 데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="35271-104">Introducing ASP.NET Web Pages - Deleting Database Data</span></span>
====================
<span data-ttu-id="35271-105">으로 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="35271-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="35271-106">이 자습서는 개별 데이터베이스 항목을 삭제 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="35271-106">This tutorial shows you how to delete an individual database entry.</span></span> <span data-ttu-id="35271-107">통해 시리즈를 완료 한 것으로 가정 [ASP.NET 웹 페이지에서 데이터베이스 데이터 업데이트](updating-data.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="35271-107">It assumes you have completed the series through [Updating Database Data in ASP.NET Web Pages](updating-data.md).</span></span>
> 
> <span data-ttu-id="35271-108">학습 내용:</span><span class="sxs-lookup"><span data-stu-id="35271-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="35271-109">레코드의 목록에서 개별 레코드를 선택 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="35271-109">How to select an individual record from a listing of records.</span></span>
> - <span data-ttu-id="35271-110">데이터베이스에서 단일 레코드를 삭제 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="35271-110">How to delete a single record from a database.</span></span>
> - <span data-ttu-id="35271-111">폼에 특정 단추가 클릭 되었습니다 있는지 확인 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="35271-111">How to check that a specific button was clicked in a form.</span></span>
>   
> 
> <span data-ttu-id="35271-112">기능/기술을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="35271-112">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="35271-113">`WebGrid` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="35271-113">The `WebGrid` helper.</span></span>
> - <span data-ttu-id="35271-114">SQL `Delete` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="35271-114">The SQL `Delete` command.</span></span>
> - <span data-ttu-id="35271-115">`Database.Execute` SQL 실행할 메서드를 `Delete` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="35271-115">The `Database.Execute` method to run a SQL `Delete` command.</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="35271-116">만들 것인지</span><span class="sxs-lookup"><span data-stu-id="35271-116">What You'll Build</span></span>

<span data-ttu-id="35271-117">이전 자습서에서는 기존 데이터베이스 레코드를 업데이트 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="35271-117">In the previous tutorial, you learned how to update an existing database record.</span></span> <span data-ttu-id="35271-118">이 자습서는, 제외 하는 레코드를 업데이트 하는 대신 있습니다 삭제 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="35271-118">This tutorial is similar, except that instead of updating the record, you'll delete it.</span></span> <span data-ttu-id="35271-119">프로세스는 동일 하며 점을 제외 하 고 삭제는이 자습서에서는 간단한 하므로 더 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="35271-119">The processes are much the same, except that deleting is simpler, so this tutorial will be short.</span></span>

<span data-ttu-id="35271-120">에 *동영상* 업데이트 합니다 페이지는 `WebGrid` 도우미를 표시 하도록는 **삭제** 함께 각 동영상 옆에 있는 링크는 **편집** 이전에 추가한 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="35271-120">In the *Movies* page, you'll update the `WebGrid` helper so that it displays a **Delete** link next to each movie to accompany the **Edit** link you added earlier.</span></span>

![각 동영상에 대 한 삭제 링크를 보여 주는 동영상 페이지](deleting-data/_static/image1.png)

<span data-ttu-id="35271-122">편집와 마찬가지로 클릭할 때는 **삭제** 링크를 걸리는 다른 페이지로 영화 정보를 양식에 이미 여기서:</span><span class="sxs-lookup"><span data-stu-id="35271-122">As with editing, when you click the **Delete** link, it takes you to a different page, where the movie information is already in a form:</span></span>

![표시 동영상으로 동영상 페이지 삭제](deleting-data/_static/image2.png)

<span data-ttu-id="35271-124">레코드를 영구적으로 삭제 하는 단추를 클릭 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35271-124">You can then click the button to delete the record permanently.</span></span>

## <a name="adding-a-delete-link-to-the-movie-listing"></a><span data-ttu-id="35271-125">영화 목록 삭제 링크를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="35271-125">Adding a Delete Link to the Movie Listing</span></span>

<span data-ttu-id="35271-126">추가 하 여 시작 합니다는 **삭제** 연결할는 `WebGrid` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="35271-126">You'll start by adding a **Delete** link to the `WebGrid` helper.</span></span> <span data-ttu-id="35271-127">이 링크는 비슷합니다는 **편집** 이전 자습서에서 추가 된 링크.</span><span class="sxs-lookup"><span data-stu-id="35271-127">This link is similar to the **Edit** link you added in a previous tutorial.</span></span>

<span data-ttu-id="35271-128">열기는 *Movies.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="35271-128">Open the *Movies.cshtml* file.</span></span>

<span data-ttu-id="35271-129">변경 된 `WebGrid` 열을 추가 하 여 페이지의 본문에는 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="35271-129">Change the `WebGrid` markup in the body of the page by adding a column.</span></span> <span data-ttu-id="35271-130">수정 된 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="35271-130">Here's the modified markup:</span></span>

[!code-html[Main](deleting-data/samples/sample1.html?highlight=9-10)]

<span data-ttu-id="35271-131">새 열이이 하나가:</span><span class="sxs-lookup"><span data-stu-id="35271-131">The new column is this one:</span></span>

[!code-html[Main](deleting-data/samples/sample2.html)]

<span data-ttu-id="35271-132">눈금 구성 된 방식은 **편집** 눈금에서 가장 왼쪽 열을 및 **삭제** 맨 오른쪽 열이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35271-132">The way the grid is configured, the **Edit** column is leftmost in the grid and the **Delete** column is rightmost.</span></span> <span data-ttu-id="35271-133">(뒤에 쉼표가 없는 `Year` 열 이제는 확인 하지 않은 경우.) 이러한 링크 열으로 이동 하는 방법에 대 한 특별 하 고 서로 인접 쉽게 넣을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="35271-133">(There's a comma after the `Year` column now, in case you didn't notice that.) There's nothing special about where these link columns go, and you could as easily put them next to each other.</span></span> <span data-ttu-id="35271-134">이 경우 어려울 혼합 해 서 가져올 수 있도록 별도 일입니다.</span><span class="sxs-lookup"><span data-stu-id="35271-134">In this case, they're separate to make them harder to get mixed up.</span></span>

![서로 인접 하지 있는 표시 하도록 편집 및 세부 정보 링크와 함께 동영상 페이지 표시](deleting-data/_static/image3.png)

<span data-ttu-id="35271-136">새 열에 있는 링크 표시 (`<a>` 요소) 이라고 표시 된 "Delete"입니다.</span><span class="sxs-lookup"><span data-stu-id="35271-136">The new column shows a link (`<a>` element) whose text says "Delete".</span></span> <span data-ttu-id="35271-137">링크의 대상 (해당 `href` 특성)는 궁극적으로와 같이이 URL을 확인 하는 코드는 `id` 각 동영상에 대 한 다른 값:</span><span class="sxs-lookup"><span data-stu-id="35271-137">The target of the link (its `href` attribute) is code that ultimately resolves to something like this URL, with the `id` value different for each movie:</span></span>

[!code-css[Main](deleting-data/samples/sample3.css)]

<span data-ttu-id="35271-138">이 링크는 라는 페이지 호출 *DeleteMovie* 선택한 동영상의 ID를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="35271-138">This link will invoke a page named *DeleteMovie* and pass it the ID of the movie you've selected.</span></span>

<span data-ttu-id="35271-139">이 자습서는 거의 동일 하기 때문에이 링크 생성 방법에 대 한 정보를 확인할 다루지는 않겠습니다.는 **편집** 이전 자습서의 링크 ([ASP.NET 웹 페이지에서 데이터베이스 데이터 업데이트](updating-data.md)).</span><span class="sxs-lookup"><span data-stu-id="35271-139">This tutorial won't go into detail about how this link is constructed, because it's almost identical to the **Edit** link from the previous tutorial ([Updating Database Data in ASP.NET Web Pages](updating-data.md)).</span></span>

## <a name="creating-the-delete-page"></a><span data-ttu-id="35271-140">Delete 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="35271-140">Creating the Delete Page</span></span>

<span data-ttu-id="35271-141">이제의 대상이 될 페이지를 만들 수는 **삭제** 눈금에 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="35271-141">Now you can create the page that will be the target for the **Delete** link in the grid.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="35271-142">**중요 한** 먼저 삭제할 레코드를 선택 하 고 다음 프로세스를 확인 하는 별도 페이지와 단추를 사용 하는 방법에는 보안에 매우 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="35271-142">**Important** The technique of first selecting a record to delete and then using a separate page and button to confirm the process is extremely important for security.</span></span> <span data-ttu-id="35271-143">이전 자습서에서 읽은으로 만드는 *모든* 종류의 웹 사이트를 변경 해야 *항상* 수행할 수는 양식을 사용 하 여 &mdash; 즉, HTTP POST 작업을 사용 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="35271-143">As you've read in previous tutorials, making *any* sort of change to your website should *always* be done using a form &mdash; that is, using an HTTP POST operation.</span></span> <span data-ttu-id="35271-144">변경한 (사용 하 여 가져오기 작업) 링크를 클릭 하 여 사이트를 변경할 수, 하는 경우 사용자 수 간단한 요청 사이트에 만들고 데이터를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="35271-144">If you made it possible to change the site just by clicking a link (that is, using a GET operation), people could make simple requests to your site and delete your data.</span></span> <span data-ttu-id="35271-145">검색 엔진 크롤러도 사이트 인덱싱 되는 링크를 따라 데이터를 실수로 삭제 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="35271-145">Even a search-engine crawler that's indexing your site could inadvertently delete data just by following links.</span></span>
> 
> <span data-ttu-id="35271-146">응용 프로그램을 통해 사용자는 레코드를 변경 때 사용자에 게 계속 편집을 위해 레코드를 표시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35271-146">When your app lets people change a record, you have to present the record to the user for editing anyway.</span></span> <span data-ttu-id="35271-147">하지만이 단계는 레코드를 삭제 하기 위한 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35271-147">But you might be tempted to skip this step for deleting a record.</span></span> <span data-ttu-id="35271-148">그러나 해당 단계를 건너뛸 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="35271-148">Don't skip that step, though.</span></span> <span data-ttu-id="35271-149">(이기도 한 레코드를 보고 확인 레코드를 의도 한 것을 삭제 하는 사용자에 유용 합니다.)</span><span class="sxs-lookup"><span data-stu-id="35271-149">(It's also helpful for users to see the record and confirm that they're deleting the record that they intended.)</span></span>
> 
> <span data-ttu-id="35271-150">이후의 자습서 집합에는 사용자가 레코드를 삭제 하기 전에 로그인 해야 하므로 로그인 기능을 추가 하는 방법을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="35271-150">In a subsequent tutorial set, you'll see how to add login functionality so a user would have to log in before deleting a record.</span></span>


<span data-ttu-id="35271-151">*DeleteMovie.cshtml* 바꾸고 다음 태그를 사용 하 여 파일에 포함 된 내용:</span><span class="sxs-lookup"><span data-stu-id="35271-151">Create a page named *DeleteMovie.cshtml* and replace what's in the file with the following markup:</span></span>

[!code-cshtml[Main](deleting-data/samples/sample4.cshtml)]

<span data-ttu-id="35271-152">이 태그는 같은 *EditMovie* 텍스트 상자를 사용 하는 대신 점을 제외 하 고 페이지 (`<input type="text">`), 태그를 포함 `<span>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="35271-152">This markup is like the *EditMovie* pages, except that instead of using text boxes (`<input type="text">`), the markup includes `<span>` elements.</span></span> <span data-ttu-id="35271-153">여기에 아무 것 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35271-153">There's nothing here to edit.</span></span> <span data-ttu-id="35271-154">사용자가 오른쪽 동영상을 삭제 하는 되는지 확인할 수 영화 세부 정보를 표시 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="35271-154">All you have to do is display the movie details so that users can make sure that they're deleting the right movie.</span></span>

<span data-ttu-id="35271-155">태그에는 이미 사용자가 동영상 목록 페이지로 돌아가 수 있는 링크가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="35271-155">The markup already contains a link that lets the user return to the movie listing page.</span></span>

<span data-ttu-id="35271-156">와 같이 *EditMovie* 페이지에서 선택한 동영상의 ID는 숨겨진된 필드에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="35271-156">As in the *EditMovie* page, the ID of the selected movie is stored in a hidden field.</span></span> <span data-ttu-id="35271-157">(로 전달 됩니다 페이지에 처음에 쿼리 문자열 값입니다.) 한 `Html.ValidationSummary` 유효성 검사 오류를 표시 하는 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="35271-157">(It's passed into the page in the first place as a query string value.) There's an `Html.ValidationSummary` call that will display validation errors.</span></span> <span data-ttu-id="35271-158">이 경우 오류 영화 ID가 없습니다. 페이지에 전달 된 또는 영화 ID가 올바르지 않습니다 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35271-158">In this case, the error might be that no movie ID was passed to the page or that the movie ID is invalid.</span></span> <span data-ttu-id="35271-159">다른 사용자의 동영상을 선택 하지 않고이 페이지를 실행 한 경우이 상황이 발생할 수는 *동영상* 페이지.</span><span class="sxs-lookup"><span data-stu-id="35271-159">This situation could occur if someone ran this page without first selecting a movie in the *Movies* page.</span></span>

<span data-ttu-id="35271-160">단추 캡션이 **삭제 영화**, 해당 이름 특성은로 설정 하 고 `buttonDelete`합니다.</span><span class="sxs-lookup"><span data-stu-id="35271-160">The button caption is **Delete Movie**, and its name attribute is set to `buttonDelete`.</span></span> <span data-ttu-id="35271-161">`name` 특성은 양식을 제출 단추를 나타내는 코드에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="35271-161">The `name` attribute will be used in the code to identify the button that submitted the form.</span></span>

<span data-ttu-id="35271-162">1)는 영화 세부 정보를 읽어 페이지를 처음 표시할 때 코드를 작성 하 고 2) 실제로 단추를 클릭할 때 영화를 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35271-162">You'll have to write code to 1) read the movie details when the page is first displayed and 2) actually delete the movie when the user clicks the button.</span></span>

## <a name="adding-code-to-read-a-single-movie"></a><span data-ttu-id="35271-163">단일 영화를 읽는 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="35271-163">Adding Code to Read a Single Movie</span></span>

<span data-ttu-id="35271-164">맨 위에 있는 *DeleteMovie.cshtml* 페이지에서 다음 코드 블록을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="35271-164">At the top of the *DeleteMovie.cshtml* page, add the following code block:</span></span>

[!code-cshtml[Main](deleting-data/samples/sample5.cshtml)]

<span data-ttu-id="35271-165">이 태그에 해당 하는 코드와 같습니다는 *EditMovie* 페이지.</span><span class="sxs-lookup"><span data-stu-id="35271-165">This markup is the same as the corresponding code in the *EditMovie* page.</span></span> <span data-ttu-id="35271-166">쿼리 문자열에서 영화 ID를 가져오고 ID를 사용 하 여 데이터베이스에서 레코드를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35271-166">It gets the movie ID out of the query string and uses the ID to read a record from the database.</span></span> <span data-ttu-id="35271-167">코드에 유효성 검사 테스트 (`IsInt()` 및 `row != null`)를 페이지에 전달 되 고 영화 ID가 유효한 지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="35271-167">The code includes the validation test (`IsInt()` and `row != null`) to make sure that the movie ID being passed to the page is valid.</span></span>

<span data-ttu-id="35271-168">이 코드 페이지가 실행 되는 처음으로 실행 해야 함을 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="35271-168">Remember that this code should only run the first time the page runs.</span></span> <span data-ttu-id="35271-169">사용자가 데이터베이스에서 영화 레코드를 다시 읽을 않으려면는 **영화 삭제** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="35271-169">You don't want to re-read the movie record from the database when the user clicks the **Delete Movie** button.</span></span> <span data-ttu-id="35271-170">따라서 테스트 라는 내부 동영상을 읽을 수 코드 `if(!IsPost)` &mdash; 즉, *요청이 post 작업 (양식 전송) 없으면*합니다.</span><span class="sxs-lookup"><span data-stu-id="35271-170">Therefore, code to read the movie is inside a test that says `if(!IsPost)` &mdash; that is, *if the request is not a post operation (form submission)*.</span></span>

## <a name="adding-code-to-delete-the-selected-movie"></a><span data-ttu-id="35271-171">선택한 동영상을 삭제 하는 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="35271-171">Adding Code to Delete the Selected Movie</span></span>

<span data-ttu-id="35271-172">사용자가 단추를 클릭할 때 영화를 삭제 하려면 바로의 닫는 중괄호 안에 다음 코드를 추가 `@` 블록:</span><span class="sxs-lookup"><span data-stu-id="35271-172">To delete the movie when the user clicks the button, add the following code just inside the closing brace of the `@` block:</span></span>

[!code-csharp[Main](deleting-data/samples/sample6.cs)]

<span data-ttu-id="35271-173">이 코드는 기존 레코드를 업데이트 하기 위한 코드와 유사 하지만 더 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="35271-173">This code is similar to the code for updating an existing record, but simpler.</span></span> <span data-ttu-id="35271-174">이 코드는 기본적으로 SQL 실행 `Delete` 문.</span><span class="sxs-lookup"><span data-stu-id="35271-174">The code basically runs a SQL `Delete` statement.</span></span>

 <span data-ttu-id="35271-175">와 같이 *EditMovie* 코드는 페이지는 `if(IsPost)` 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="35271-175">As in the *EditMovie* page, the code is in an `if(IsPost)` block.</span></span> <span data-ttu-id="35271-176">이 이번에는 `if()` 조건이 약간 더 복잡 합니다.</span><span class="sxs-lookup"><span data-stu-id="35271-176">This time, the `if()` condition is a little more complicated:</span></span> 

[!code-csharp[Main](deleting-data/samples/sample7.cs)]

<span data-ttu-id="35271-177">두 조건을 여기 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35271-177">There are two conditions here.</span></span> <span data-ttu-id="35271-178">첫 번째 페이지가 제출 되는 하기 전에 지금까지 살펴본 대로 &mdash; `if(IsPost)`합니다.</span><span class="sxs-lookup"><span data-stu-id="35271-178">The first is that the page is being submitted, as you've seen before &mdash; `if(IsPost)`.</span></span>

<span data-ttu-id="35271-179">두 번째 조건은 `!Request["buttonDelete"].IsEmpty()`, 요청 라는 개체에 의미 `buttonDelete`합니다.</span><span class="sxs-lookup"><span data-stu-id="35271-179">The second condition is `!Request["buttonDelete"].IsEmpty()`, meaning that the request has an object named `buttonDelete`.</span></span> <span data-ttu-id="35271-180">물론, 어떤 단추가 양식을 제출 테스트의 간접 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="35271-180">Admittedly, it's an indirect way of testing which button submitted the form.</span></span> <span data-ttu-id="35271-181">여러 전송 단추를 포함 하는 경우 요청에서 클릭 된 단추의의 이름만이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="35271-181">If a form contains multiple submit buttons, only the name of the button that was clicked appears in the request.</span></span> <span data-ttu-id="35271-182">따라서, 논리적으로 경우 요청에는 특정 단추 이름이 표시 &mdash; 해당 단추의 비어 있지 않은 경우에 코드에 명시 된 대로 또는 &mdash; 양식을 제출 하는 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="35271-182">Therefore, logically, if the name of a particular button appears in the request &mdash; or as stated in the code, if that button isn't empty &mdash; that's the button that submitted the form.</span></span>

<span data-ttu-id="35271-183">`&&` 연산자 수단 "및" (논리적 AND).</span><span class="sxs-lookup"><span data-stu-id="35271-183">The `&&` operator means "and" (logical AND).</span></span> <span data-ttu-id="35271-184">따라서 전체 `if` 조건이...</span><span class="sxs-lookup"><span data-stu-id="35271-184">Therefore the entire `if` condition is ...</span></span>

<span data-ttu-id="35271-185">*이 요청은 post (처음 요청 될 수는 없음)*</span><span class="sxs-lookup"><span data-stu-id="35271-185">*This request is a post (not a first-time request)*</span></span>  
  
 <span data-ttu-id="35271-186">AND</span><span class="sxs-lookup"><span data-stu-id="35271-186">AND</span></span>  
  
<span data-ttu-id="35271-187"> `buttonDelete` *단추가 있던 양식을 제출 하는 단추입니다.*</span><span class="sxs-lookup"><span data-stu-id="35271-187">*The* `buttonDelete`*button was the button that submitted the form.*</span></span>

<span data-ttu-id="35271-188">(사실,이 페이지)이이 폼에는 단추 하나만 있으므로 대 한 추가 테스트 `buttonDelete` 기술적으로 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="35271-188">This form (in fact, this page) contains only one button, so the additional test for `buttonDelete` is technically not required.</span></span> <span data-ttu-id="35271-189">아직도 하려는 데이터를 영구적으로 제거 하는 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="35271-189">Still, you're about to perform an operation that will permanently remove data.</span></span> <span data-ttu-id="35271-190">따라서 사용자가 요청 명시적으로 하는 경우에 작업을 수행 하는 가능한 반드시 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="35271-190">So you want to be as sure as possible that you're performing the operation only when the user has explicitly requested it.</span></span> <span data-ttu-id="35271-191">예를 들어 나중에이 페이지를 확장 하 고 여기에 다른 단추 추가 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="35271-191">For example, suppose that you expanded this page later and added other buttons to it.</span></span> <span data-ttu-id="35271-192">경우에 동영상을 삭제 하는 코드가 실행 되는는 `buttonDelete` 단추가 클릭 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="35271-192">Even then, the code that deletes the movie will run only if the `buttonDelete` button was clicked.</span></span>

<span data-ttu-id="35271-193">와 같이 *EditMovie* 페이지 있습니다 ID에서 숨겨진된 필드를 가져오고 다음 SQL 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="35271-193">As in the *EditMovie* page, you get the ID from the hidden field and then run the SQL command.</span></span> <span data-ttu-id="35271-194">에 대 한 구문에서 `Delete` 문이:</span><span class="sxs-lookup"><span data-stu-id="35271-194">The syntax for the `Delete` statement is:</span></span>

`DELETE FROM table WHERE ID = value`

<span data-ttu-id="35271-195">포함을 `WHERE` 절과 id입니다.</span><span class="sxs-lookup"><span data-stu-id="35271-195">It's vital to include the `WHERE` clause and the ID.</span></span> <span data-ttu-id="35271-196">WHERE 절을 지정 하지 않을 경우 *삭제할 테이블의 모든 레코드가*합니다.</span><span class="sxs-lookup"><span data-stu-id="35271-196">If you leave out the WHERE clause, *all the records in the table will be deleted*.</span></span> <span data-ttu-id="35271-197">위에서 설명한 것 처럼 전달 ID 값은 SQL 명령 자리 표시자를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="35271-197">As you have seen, you pass the ID value to the SQL command by using a placeholder.</span></span>

## <a name="testing-the-movie-delete-process"></a><span data-ttu-id="35271-198">영화 삭제 프로세스를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="35271-198">Testing the Movie Delete Process</span></span>

<span data-ttu-id="35271-199">이제 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35271-199">Now you can test.</span></span> <span data-ttu-id="35271-200">실행 된 *동영상* 페이지를 클릭 하 여 **삭제** 동영상 옆에 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="35271-200">Run the *Movies* page, and click **Delete** next to a movie.</span></span> <span data-ttu-id="35271-201">경우는 *DeleteMovie* 페이지에 표시 되 면 클릭 **삭제 동영상**합니다.</span><span class="sxs-lookup"><span data-stu-id="35271-201">When the *DeleteMovie* page appears, click **Delete Movie**.</span></span>

![영화 삭제 단추가 강조 표시 된 동영상 페이지 삭제](deleting-data/_static/image4.png)

<span data-ttu-id="35271-203">단추를 클릭할 때 코드는 영화를 삭제 하 고 동영상 목록으로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="35271-203">When you click the button, the code deletes the movies and returns to the movie listing.</span></span> <span data-ttu-id="35271-204">삭제 된 영화를 검색할 수 있습니다는 삭제 된 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="35271-204">There you can search for the deleted movie and confirm that it's been deleted.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="35271-205">다음에 나오는</span><span class="sxs-lookup"><span data-stu-id="35271-205">Coming Up Next</span></span>

<span data-ttu-id="35271-206">다음 자습서에서는 일반적인 모양과 레이아웃 사이트에서 모든 페이지를 제공 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="35271-206">The next tutorial shows you how to give all the pages on your site a common look and layout.</span></span>

## <a name="complete-listing-for-movie-page-updated-with-delete-links"></a><span data-ttu-id="35271-207">동영상 페이지 (삭제 링크와 함께 업데이트)에 대 한 전체 목록을 보려면</span><span class="sxs-lookup"><span data-stu-id="35271-207">Complete Listing for Movie Page (Updated with Delete Links)</span></span>

[!code-cshtml[Main](deleting-data/samples/sample8.cshtml)]

## <a name="complete-listing-for-deletemovie-page"></a><span data-ttu-id="35271-208">DeleteMovie 페이지에 대 한 전체 목록을 보려면</span><span class="sxs-lookup"><span data-stu-id="35271-208">Complete Listing for DeleteMovie Page</span></span>

[!code-cshtml[Main](deleting-data/samples/sample9.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="35271-209">추가 자료</span><span class="sxs-lookup"><span data-stu-id="35271-209">Additional Resources</span></span>

- [<span data-ttu-id="35271-210">Razor 구문을 사용 하 여 ASP.NET 웹 프로그래밍 소개</span><span class="sxs-lookup"><span data-stu-id="35271-210">Introduction to ASP.NET Web Programming by Using the Razor Syntax</span></span>](../introducing-razor-syntax-c.md)
- <span data-ttu-id="35271-211">[SQL DELETE 문을](http://www.w3schools.com/sql/sql_delete.asp) W3Schools 사이트</span><span class="sxs-lookup"><span data-stu-id="35271-211">[SQL DELETE Statement](http://www.w3schools.com/sql/sql_delete.asp) on the W3Schools site</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="35271-212">[이전](updating-data.md)
> [다음](layouts.md)</span><span class="sxs-lookup"><span data-stu-id="35271-212">[Previous](updating-data.md)
[Next](layouts.md)</span></span>
