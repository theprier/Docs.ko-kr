---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/entering-data
title: ASP.NET 웹 페이지 소개-Forms를 사용 하 여 데이터베이스 데이터를 입력 합니다. | Microsoft Docs
author: tfitzmac
description: 이 자습서 입력 폼을 만들고 다음 얻을 수 있는 폼에서 데이터베이스 테이블에 ASP.NET 웹 페이지 (...를 사용할 때 데이터를 입력 하는 방법을 보여 줍니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/28/2015
ms.topic: article
ms.assetid: d37c93fc-25fd-4e94-8671-0d437beef206
ms.technology: dotnet-webpages
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/entering-data
msc.type: authoredcontent
ms.openlocfilehash: 41122b3bca5a3d3162a66be163642610b8349cc5
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37386409"
---
<a name="introducing-aspnet-web-pages---entering-database-data-by-using-forms"></a><span data-ttu-id="7b61f-103">ASP.NET 웹 페이지 소개-Forms를 사용 하 여 데이터베이스 데이터를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-103">Introducing ASP.NET Web Pages - Entering Database Data by Using Forms</span></span>
====================
<span data-ttu-id="7b61f-104">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="7b61f-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="7b61f-105">이 자습서에서는 입력 폼을 만들고 다음 얻을 수 있는 폼에서 데이터베이스 테이블에 ASP.NET Web Pages (Razor)를 사용 하는 경우 데이터를 입력 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-105">This tutorial shows you how to create an entry form and then enter the data that you get from the form into a database table when you use ASP.NET Web Pages (Razor).</span></span> <span data-ttu-id="7b61f-106">통해 시리즈를 완료 했다고 가정 하 [기본 사항의 HTML 폼 ASP.NET 웹 페이지에서](https://go.microsoft.com/fwlink/?LinkId=251581)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-106">It assumes you have completed the series through [Basics of HTML Forms in ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251581).</span></span>
> 
> <span data-ttu-id="7b61f-107">학습할 내용:</span><span class="sxs-lookup"><span data-stu-id="7b61f-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="7b61f-108">입력 폼을 처리 하는 방법에 대해 자세히 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-108">More about how to process entry forms.</span></span>
> - <span data-ttu-id="7b61f-109">데이터베이스의 데이터 (삽입)를 추가 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-109">How to add (insert) data in a database.</span></span>
> - <span data-ttu-id="7b61f-110">사용자 (사용자 입력의 유효성을 검사 하는 방법) 형태로 필요한 값을 입력 하 고 있는지 확인 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="7b61f-110">How to make sure that users have entered a required value in a form (how to validate user input).</span></span>
> - <span data-ttu-id="7b61f-111">유효성 검사 오류를 표시 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-111">How to display validation errors.</span></span>
> - <span data-ttu-id="7b61f-112">현재 페이지에서 다른 페이지로 이동 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="7b61f-112">How to jump to another page from the current page.</span></span>
>   
> 
> <span data-ttu-id="7b61f-113">기능/기술을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-113">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="7b61f-114">`Database.Execute` 메서드</span><span class="sxs-lookup"><span data-stu-id="7b61f-114">The `Database.Execute` method.</span></span>
> - <span data-ttu-id="7b61f-115">SQL `Insert Into` 문</span><span class="sxs-lookup"><span data-stu-id="7b61f-115">The SQL `Insert Into` statement</span></span>
> - <span data-ttu-id="7b61f-116">`Validation` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-116">The `Validation` helper.</span></span>
> - <span data-ttu-id="7b61f-117">`Response.Redirect` 메서드</span><span class="sxs-lookup"><span data-stu-id="7b61f-117">The `Response.Redirect` method.</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="7b61f-118">만들 내용</span><span class="sxs-lookup"><span data-stu-id="7b61f-118">What You'll Build</span></span>

<span data-ttu-id="7b61f-119">자습서 이전 데이터베이스를 만드는 방법에 알아보았습니다는 WebMatrix에서 작업에서 직접 데이터베이스를 편집 하 여 데이터베이스 데이터 입력을 **데이터베이스** 작업 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-119">In the tutorial earlier that showed you how to create a database, you entered database data by editing the database directly in WebMatrix, working in the **Database** workspace.</span></span> <span data-ttu-id="7b61f-120">대부분의 앱에 없는 하지만 데이터베이스에 데이터를 저장 하는 실용적인 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-120">In most apps, that's not a practical way to put data into the database, though.</span></span> <span data-ttu-id="7b61f-121">따라서이 자습서에서는 모든 사용자 데이터를 입력 하 고 데이터베이스에 저장할 수 있는 웹 기반 인터페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-121">So in this tutorial, you'll create a web-based interface that lets you or anyone enter data and save it to the database.</span></span>

<span data-ttu-id="7b61f-122">새 영화를 입력할 수 있는 페이지를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-122">You'll create a page where you can enter new movies.</span></span> <span data-ttu-id="7b61f-123">페이지 입력 폼을 영화 제목, genre 및 연도 입력할 수 있는 필드 (입력란)가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-123">The page will contain an entry form that has fields (text boxes) where you can enter a movie title, genre, and year.</span></span> <span data-ttu-id="7b61f-124">페이지는이 페이지와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-124">The page will look like this page:</span></span>

![브라우저에서 페이지 동영상 추가'](entering-data/_static/image1.png)

<span data-ttu-id="7b61f-126">텍스트 상자에는 HTML 됩니다 `<input>` 요소를 찾는 등이 태그:</span><span class="sxs-lookup"><span data-stu-id="7b61f-126">The text boxes will be HTML `<input>` elements that will look like this markup:</span></span>

`<input type="text" name="genre" value="" />`

## <a name="creating-the-basic-entry-form"></a><span data-ttu-id="7b61f-127">기본 입력 양식 만들기</span><span class="sxs-lookup"><span data-stu-id="7b61f-127">Creating the Basic Entry Form</span></span>

<span data-ttu-id="7b61f-128">라는 페이지를 만듭니다 *AddMovie.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-128">Create a page named *AddMovie.cshtml*.</span></span>

<span data-ttu-id="7b61f-129">다음 태그를 사용 하 여 파일에 포함 된 내용으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-129">Replace what's in the file with the following markup.</span></span> <span data-ttu-id="7b61f-130">모든; 덮어쓰기 맨 위에 있는 코드 블록을 곧 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-130">Overwrite everything; you'll add a code block at the top shortly.</span></span>

[!code-cshtml[Main](entering-data/samples/sample1.cshtml)]

<span data-ttu-id="7b61f-131">이 예제에서는 일반적인 HTML 양식 만들기</span><span class="sxs-lookup"><span data-stu-id="7b61f-131">This example shows typical HTML for creating a form.</span></span> <span data-ttu-id="7b61f-132">사용 하 여 `<input>` 제출 단추 및 텍스트 상자에 대 한 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-132">It uses `<input>` elements for the text boxes and for the submit button.</span></span> <span data-ttu-id="7b61f-133">텍스트 상자에 대 한 캡션을 standard를 사용 하 여 만들어진 `<label>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-133">The captions for the text boxes are created by using standard `<label>` elements.</span></span> <span data-ttu-id="7b61f-134">합니다 `<fieldset>` 및 `<legend>` 요소 폼 주위에 유용한 상자를 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-134">The `<fieldset>` and `<legend>` elements put a nice box around the form.</span></span>

<span data-ttu-id="7b61f-135">이 페이지에서의 `<form>` 요소를 사용 하 여 `post` 값으로는 `method` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-135">Notice that in this page, the `<form>` element uses `post` as the value for the `method` attribute.</span></span> <span data-ttu-id="7b61f-136">이전 자습서에서 사용 하는 양식을 만든를 `get` 메서드.</span><span class="sxs-lookup"><span data-stu-id="7b61f-136">In the previous tutorial, you created a form that used the `get` method.</span></span> <span data-ttu-id="7b61f-137">양식이 제출 값을 서버에 있지만 요청 변경 하지 않았으면 모든 때문에 올바른 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-137">That was correct, because although the form submitted values to the server, the request did not make any changes.</span></span> <span data-ttu-id="7b61f-138">수행한 모든 다양 한 방법으로 데이터를 가져오고 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-138">All it did was fetch data in different ways.</span></span> <span data-ttu-id="7b61f-139">그러나이 페이지 *는* 변경-새 데이터베이스 레코드를 추가 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-139">However, in this page you *will* make changes—you're going to add new database records.</span></span> <span data-ttu-id="7b61f-140">따라서이 양식을 사용 해야는 `post` 메서드.</span><span class="sxs-lookup"><span data-stu-id="7b61f-140">Therefore, this form should use the `post` method.</span></span> <span data-ttu-id="7b61f-141">(간의 차이점에 대 한 자세한 `GET` 및 `POST` 작업을 참조 하세요 합니다[GET, POST 및 HTTP 동사 안전](https://go.microsoft.com/fwlink/?LinkId=251581#GET,_POST,_and_HTTP_Verb_Safety) 이전 자습서에서 세로 막대입니다.)</span><span class="sxs-lookup"><span data-stu-id="7b61f-141">(For more about the difference between `GET` and `POST` operations, see the[GET, POST, and HTTP Verb Safety](https://go.microsoft.com/fwlink/?LinkId=251581#GET,_POST,_and_HTTP_Verb_Safety) sidebar in the previous tutorial.)</span></span>

<span data-ttu-id="7b61f-142">각 텍스트 상자에는 한 `name` 요소 (`title`를 `genre`, `year`).</span><span class="sxs-lookup"><span data-stu-id="7b61f-142">Note that each text box has a `name` element (`title`, `genre`, `year`).</span></span> <span data-ttu-id="7b61f-143">이전 자습서에서 살펴본 것 처럼 사용자의 입력을 나중에 받을 수 있도록 해당 이름이 있어야 하기 때문에 이러한 이름을 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-143">As you saw in the previous tutorial, these names are important because you must have those names so you can get the user's input later.</span></span> <span data-ttu-id="7b61f-144">모든 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-144">You can use any names.</span></span> <span data-ttu-id="7b61f-145">하는 것이 좋습니다 도움이 되는 의미 있는 이름을 사용 하 여 작업할 때 어떤 데이터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-145">It's helpful to use meaningful names that help you remember what data you're working with.</span></span>

<span data-ttu-id="7b61f-146">합니다 `value` 각각의 특성 `<input>` Razor 코드의 비트를 포함 하는 요소 (예를 들어 `Request.Form["title"]`).</span><span class="sxs-lookup"><span data-stu-id="7b61f-146">The `value` attribute of each `<input>` element contains a bit of Razor code (for example, `Request.Form["title"]`).</span></span> <span data-ttu-id="7b61f-147">양식이 제출 되 면 (있는 경우) 텍스트 상자에 입력 한 값을 보존 하려면 이전 자습서에서이 방법의 버전을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-147">You learned a version of this trick in the previous tutorial to preserve the value entered into the text box (if any) after the form has been submitted.</span></span>

## <a name="getting-the-form-values"></a><span data-ttu-id="7b61f-148">폼 값 가져오기</span><span class="sxs-lookup"><span data-stu-id="7b61f-148">Getting the Form Values</span></span>

<span data-ttu-id="7b61f-149">그런 다음 양식을 처리는 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-149">Next, you add code that processes the form.</span></span> <span data-ttu-id="7b61f-150">개요에서 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-150">In outline, you'll do the following:</span></span>

1. <span data-ttu-id="7b61f-151">페이지가 게시 되 고 있는지 여부를 확인 (제출).</span><span class="sxs-lookup"><span data-stu-id="7b61f-151">Check whether the page is being posted (was submitted).</span></span> <span data-ttu-id="7b61f-152">코드를 실행 하려는 페이지를 처음 실행할 때가 아니라 사용자가 단추를 클릭 하는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-152">You want to your code to run only when users have clicked the button, not when the page first runs.</span></span>
2. <span data-ttu-id="7b61f-153">사용자가 텍스트 상자에 입력 한 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-153">Get the values that the user entered into the text boxes.</span></span> <span data-ttu-id="7b61f-154">이 경우 폼 사용 중이기 때문에 `POST` 에서 양식 값을 얻으려면 동사는 `Request.Form` 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-154">In this case, because the form is using the `POST` verb, you get the form values from the `Request.Form` collection.</span></span>
3. <span data-ttu-id="7b61f-155">값에서 새 레코드를 삽입 합니다 *영화* 데이터베이스 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-155">Insert the values as a new record in the *Movies* database table.</span></span>

<span data-ttu-id="7b61f-156">파일의 맨 위에 있는 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-156">At the top of the file, add the following code:</span></span>

[!code-cshtml[Main](entering-data/samples/sample2.cshtml)]

<span data-ttu-id="7b61f-157">처음 몇 줄 변수를 만듭니다 (`title`, `genre`, 및 `year`) 텍스트 상자에서 값을 보유 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-157">The first few lines create variables (`title`, `genre`, and `year`) to hold the values from the text boxes.</span></span> <span data-ttu-id="7b61f-158">줄 `if(IsPost)` 변수 설정 되어 있는지를 사용 하면 *만* 사용자가 클릭 하면는 **동영상 추가** 단추-즉, 경우 폼이 게시 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-158">The line `if(IsPost)` makes sure that the variables are set *only* when users click the **Add Movie** button — that is, when the form has been posted.</span></span>

<span data-ttu-id="7b61f-159">와 같은 식을 사용 하 여 입력란의 값을 가져올 이전 자습서에서 살펴본 것 처럼 `Request.Form["name"]`여기서 *이름* 이름인는 `<input>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-159">As you saw in an earlier tutorial, you get the value of a text box by using an expression like `Request.Form["name"]`, where *name* is the name of the `<input>` element.</span></span>

<span data-ttu-id="7b61f-160">변수 이름 (`title`, `genre`, 및 `year`)는 임의로 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-160">The names of the variables (`title`, `genre`, and `year`) are arbitrary.</span></span> <span data-ttu-id="7b61f-161">에 할당 하는 이름이 마음에 `<input>` 요소를 원하는 대로 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-161">Like the names that you assign to `<input>` elements, you can call them anything you like.</span></span> <span data-ttu-id="7b61f-162">(이름 특성에 맞게 변수 이름이 없는 `<input>` 폼에서 요소가.) 하지만와 마찬가지로 `<input>` 요소인 것이 포함 된 데이터를 반영 하는 변수 이름을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-162">(The names of the variables don't have to match the name attributes of `<input>` elements on the form.) But as with the `<input>` elements, it's a good idea to use variable names that reflect the data that they contain.</span></span> <span data-ttu-id="7b61f-163">코드를 작성할 때 일관 된 이름을 쉽게 사용 하는 데이터를 기억할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-163">When you write code, consistent names make it easier for you to remember what data you're working with.</span></span>

## <a name="adding-data-to-the-database"></a><span data-ttu-id="7b61f-164">데이터베이스에 데이터 추가</span><span class="sxs-lookup"><span data-stu-id="7b61f-164">Adding Data to the Database</span></span>

<span data-ttu-id="7b61f-165">코드에서 차단 하면 방금 추가한 *내* 닫는 중괄호 ( `}` )의 `if` 다음 코드를 추가 합니다 (뿐 아니라 코드 블록) 내에서 차단:</span><span class="sxs-lookup"><span data-stu-id="7b61f-165">In the code block you just added, just *inside* the closing brace ( `}` ) of the `if` block (not just inside the code block), add the following code:</span></span>

[!code-csharp[Main](entering-data/samples/sample3.cs)]

<span data-ttu-id="7b61f-166">이 예제에서는 데이터를 인출 하 고 표시 하는 이전 자습서에서 사용 되는 코드와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-166">This example is similar to the code you used in a previous tutorial to fetch and display data.</span></span> <span data-ttu-id="7b61f-167">로 시작 하는 줄 `db =` 열립니다 이전과 같은 데이터베이스 및 다음 줄으로 SQL 문을 다시 정의 하기 전에 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-167">The line that starts with `db =` opens the database, like before, and the next line defines a SQL statement, again as you saw before.</span></span> <span data-ttu-id="7b61f-168">그러나이 이번 정의 SQL `Insert Into` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-168">However, this time it defines a SQL `Insert Into` statement.</span></span> <span data-ttu-id="7b61f-169">다음 예제에서는 일반 구문을 보여 줍니다는 `Insert Into` 문:</span><span class="sxs-lookup"><span data-stu-id="7b61f-169">The following example shows the general syntax of the `Insert Into` statement:</span></span>

`INSERT INTO table (column1, column2, column3, ...) VALUES (value1, value2, value3, ...)`

<span data-ttu-id="7b61f-170">즉, 다음을 삽입할 열을 나열 하 고 다음 삽입할 값에를 나열 하는 테이블에 삽입을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-170">In other words, you specify the table to insert into, then list the columns to insert into, and then list the values to insert.</span></span> <span data-ttu-id="7b61f-171">(앞에서 설명한 것 처럼 SQL 대/소문자 구분 되지 않지만 쉽게 명령을 읽을 수 있도록 키워드를 활용 하는 사람도.)</span><span class="sxs-lookup"><span data-stu-id="7b61f-171">(As noted before, SQL is not case sensitive but some people capitalize the keywords to make it easier to read the command.)</span></span>

<span data-ttu-id="7b61f-172">열에 삽입 하는 명령에 이미 나열 된- `(Title, Genre, Year)`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-172">The columns that you're inserting into are already listed in the command — `(Title, Genre, Year)`.</span></span> <span data-ttu-id="7b61f-173">흥미로운 부분은에 텍스트 상자에서 값을 얻는 방법의 `VALUES` 명령의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-173">The interesting part is how you get the values from the text boxes into the `VALUES` part of the command.</span></span> <span data-ttu-id="7b61f-174">실제 값 대신 참조 하세요 `@0`, `@1`, 및 `@2`는 물론 자리 표시자입니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-174">Instead of actual values, you see `@0`, `@1`, and `@2`, which are of course placeholders.</span></span> <span data-ttu-id="7b61f-175">명령을 실행 하는 경우 (에 `db.Execute` 줄), 텍스트 상자에서 가져온 값을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-175">When you run the command (on the `db.Execute` line), you pass the values that you got from the text boxes.</span></span>

<span data-ttu-id="7b61f-176">**중요!**</span><span class="sxs-lookup"><span data-stu-id="7b61f-176">**Important!**</span></span> <span data-ttu-id="7b61f-177">다음과 같이 온라인 SQL 문에서 사용자가 입력 한 데이터를 그 어느 때 포함 해야 하는 유일한 방법은 자리 표시자를 사용 하는 (`VALUES(@0, @1, @2)`).</span><span class="sxs-lookup"><span data-stu-id="7b61f-177">Remember that the only way you should ever include data entered online by a user in a SQL statement is to use placeholders, as you see here (`VALUES(@0, @1, @2)`).</span></span> <span data-ttu-id="7b61f-178">SQL 문으로 사용자 입력을 연결 하면 열면 직접 SQL 주입 공격을 하려면에 설명 된 대로 [양식 기본 ASP.NET 웹 페이지에서](https://go.microsoft.com/fwlink/?LinkId=251581) (이전 자습서).</span><span class="sxs-lookup"><span data-stu-id="7b61f-178">If you concatenate user input into a SQL statement, you open yourself to a SQL injection attack, as explained in [Form Basics in ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251581) (the previous tutorial).</span></span>

<span data-ttu-id="7b61f-179">여전히 내 합니다 `if` 차단, 뒤에 다음 줄을 추가 합니다 `db.Execute` 줄:</span><span class="sxs-lookup"><span data-stu-id="7b61f-179">Still inside the `if` block, add the following line after the `db.Execute` line:</span></span>

[!code-css[Main](entering-data/samples/sample4.css)]

<span data-ttu-id="7b61f-180">새 영화 데이터베이스에 삽입 한 후이 줄 이동 (리디렉션) 하는 *영화* 방금 입력 한 영화를 볼 수 있도록 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-180">After the new movie has been inserted into the database, this line jumps you (redirects) to the *Movies* page so you can see the movie you just entered.</span></span> <span data-ttu-id="7b61f-181">`~` 연산자 "웹 사이트의 루트입니다."를 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-181">The `~` operator means "root of the website."</span></span> <span data-ttu-id="7b61f-182">(의 `~` 연산자 일반적으로 HTML에 없는 ASP.NET 페이지 에서만에서 작동 합니다.)</span><span class="sxs-lookup"><span data-stu-id="7b61f-182">(The `~` operator works only in ASP.NET pages, not in HTML generally.)</span></span>

<span data-ttu-id="7b61f-183">전체 코드 블록을이 예제와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-183">The complete code block looks like this example:</span></span>

[!code-cshtml[Main](entering-data/samples/sample5.cshtml)]

## <a name="testing-the-insert-command-so-far"></a><span data-ttu-id="7b61f-184">Insert 명령이 (지금) 테스트</span><span class="sxs-lookup"><span data-stu-id="7b61f-184">Testing the Insert Command (So Far)</span></span>

<span data-ttu-id="7b61f-185">아직 완료 되지 않은 하지만 이제 좋습니다를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-185">You're not done yet, but now is a good time to test.</span></span>

<span data-ttu-id="7b61f-186">WebMatrix에는 파일의 트리 뷰에서 마우스 오른쪽 단추로 클릭 합니다 *AddMovie.cshtml* 페이지를 클릭 한 다음 **브라우저에서 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-186">In the tree view of files in WebMatrix, right-click the *AddMovie.cshtml* page and then click **Launch in browser**.</span></span>

![브라우저에서 페이지 동영상 추가'](entering-data/_static/image2.png)

<span data-ttu-id="7b61f-188">(브라우저에서 다른 페이지를 사용 하 여 결국 경우 URL이 있는지 확인 `http://localhost:nnnnn/AddMovie`), 여기서 *nnnnn* 사용 중인 포트 번호입니다.)</span><span class="sxs-lookup"><span data-stu-id="7b61f-188">(If you end up with a different page in the browser, make sure that the URL is `http://localhost:nnnnn/AddMovie`), where *nnnnn* is the port number that you're using.)</span></span>

<span data-ttu-id="7b61f-189">오류 페이지 했나요?</span><span class="sxs-lookup"><span data-stu-id="7b61f-189">Did you get an error page?</span></span> <span data-ttu-id="7b61f-190">그렇다면 신중 하 게 읽고 앞에 나열 된 어떤 코드를 정확히 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-190">If so, read it carefully and make sure that the code looks exactly what was listed earlier.</span></span>

<span data-ttu-id="7b61f-191">동영상 형태로 입력 &mdash; 예를 들어, "시민 마 창", "드라마" 및 "1941"를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-191">Enter a movie in the form &mdash; for example, use "Citizen Kane", "Drama", and "1941".</span></span> <span data-ttu-id="7b61f-192">(또는 모든) 누른 **영화 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-192">(Or whatever.) Then click **Add Movie**.</span></span>

<span data-ttu-id="7b61f-193">로 리디렉션됩니다 정상적으로 작동 하는 경우는 *영화* 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-193">If all goes well, you're redirected to the *Movies* page.</span></span> <span data-ttu-id="7b61f-194">새 동영상 표시 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-194">Make sure that your new movie is listed.</span></span>

![동영상 페이지 새로 보여 주는 동영상 추가](entering-data/_static/image3.png)

## <a name="validating-user-input"></a><span data-ttu-id="7b61f-196">사용자 입력 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="7b61f-196">Validating User Input</span></span>

<span data-ttu-id="7b61f-197">로 다시 이동 합니다 *AddMovie* 페이지 또는 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-197">Go back to the *AddMovie* page, or run it again.</span></span> <span data-ttu-id="7b61f-198">다른 영화 이번 입력만 제목을 입력 합니다 &mdash; 예를 들어, "Rain에서 시스템을 사용해 봅시다 '"을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-198">Enter another movie, but this time, enter only the title &mdash; for example, enter "Singin' in the Rain".</span></span> <span data-ttu-id="7b61f-199">누른 **영화 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-199">Then click **Add Movie**.</span></span>

<span data-ttu-id="7b61f-200">로 리디렉션됩니다 합니다 *영화* 페이지를 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-200">You're redirected to the *Movies* page again.</span></span> <span data-ttu-id="7b61f-201">새 동영상을 찾을 수 있지만 완전 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-201">You can find the new movie, but it's incomplete.</span></span>

![영화 없거나 일부 값을 보여 주는 새 동영상 페이지](entering-data/_static/image4.png)

<span data-ttu-id="7b61f-203">만들 때 합니다 *영화* 테이블을 명시적으로 말씀 하 신 null 수 필드 없음.</span><span class="sxs-lookup"><span data-stu-id="7b61f-203">When you created the *Movies* table, you explicitly said that none of the fields could be null.</span></span> <span data-ttu-id="7b61f-204">여기 새 영화에 대 한 입력 폼 있고 필드를 비워 두면 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-204">Here you have an entry form for new movies, and you're leaving fields blank.</span></span> <span data-ttu-id="7b61f-205">오류입니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-205">That's an error.</span></span>

<span data-ttu-id="7b61f-206">이 경우 데이터베이스 실제로 발생 하지 않은 (또는 *throw*) 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-206">In this case, the database didn't actually raise (or *throw*) an error.</span></span> <span data-ttu-id="7b61f-207">장르 또는 연도 따라서 제공 하지 않은 코드를 *AddMovie* 페이지 소위로 해당 값을 처리 *빈 문자열*합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-207">You didn't supply a genre or year, so the code in the *AddMovie* page treated those values as so-called *empty strings*.</span></span> <span data-ttu-id="7b61f-208">때 SQL `Insert Into` 명령 실행, genre 및 year 필드에 유용한 데이터가 들어 있지 않은 되었지만 null 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-208">When the SQL `Insert Into` command ran, the genre and year fields didn't have useful data in them, but they weren't null.</span></span>

<span data-ttu-id="7b61f-209">물론 사용자가 데이터베이스에 절반 빈 영화 정보를 입력할 수 있도록 원하지입니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-209">Obviously, you don't want to let users enter half-empty movie information into the database.</span></span> <span data-ttu-id="7b61f-210">솔루션은 사용자 입력의 유효성을 검사 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-210">The solution is to validate the user's input.</span></span> <span data-ttu-id="7b61f-211">처음에 유효성 검사는 단순히 해야 사용자가 모든 필드에 대 한 값을 입력 했는지 (즉, 않은 빈 문자열을 포함).</span><span class="sxs-lookup"><span data-stu-id="7b61f-211">Initially, the validation will simply make sure that the user has entered a value for all of the fields (that is, that none of them contains an empty string).</span></span>

> [!TIP]
> 
> <span data-ttu-id="7b61f-212">**Null 및 빈 문자열**</span><span class="sxs-lookup"><span data-stu-id="7b61f-212">**Null and Empty Strings**</span></span>
> 
> <span data-ttu-id="7b61f-213">프로그래밍에는 "값이 없습니다." 다른 개념 구분</span><span class="sxs-lookup"><span data-stu-id="7b61f-213">In programming, there's a distinction between different notions of "no value."</span></span> <span data-ttu-id="7b61f-214">값은 일반적으로 *null* 설정 하거나 어떤 방식으로든에서 초기화할 되지 한 경우.</span><span class="sxs-lookup"><span data-stu-id="7b61f-214">In general, a value is *null* if it has never been set or initialized in any way.</span></span> <span data-ttu-id="7b61f-215">반면 문자 데이터 (문자열)를 필요로 하는 변수를 설정할 수 있습니다는 *빈 문자열*합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-215">In contrast, a variable that expects character data (strings) can be set to an *empty string*.</span></span> <span data-ttu-id="7b61f-216">이런 경우 값 null이 아닙니다. 이 방금 명시적으로 설정 된 길이가 0 인 문자의 문자열로.</span><span class="sxs-lookup"><span data-stu-id="7b61f-216">In that case, the value is not null; it's just been explicitly set to a string of characters whose length is zero.</span></span> <span data-ttu-id="7b61f-217">다음 두 문은 차이 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-217">These two statements show the difference:</span></span>
> 
> [!code-csharp[Main](entering-data/samples/sample6.cs)]
> 
> <span data-ttu-id="7b61f-218">이보다 더 복잡 약간 이지만 중요 한 점은 `null` 일종의 결정 되지 않은 상태를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-218">It's a little more complicated than that, but the important point is that `null` represents a sort of undetermined state.</span></span>
> 
> <span data-ttu-id="7b61f-219">값이 null 및 빈 문자열만 때 정확 하 게 이해 해야 하는 고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-219">Now and then it's important to understand exactly when a value is null and when it's just an empty string.</span></span> <span data-ttu-id="7b61f-220">코드에 *AddMovie* 페이지에서 얻게 입력란의 값을 사용 하 여 `Request.Form["title"]` 등.</span><span class="sxs-lookup"><span data-stu-id="7b61f-220">In the code for the *AddMovie* page, you get the values of the text boxes by using `Request.Form["title"]` and so on.</span></span> <span data-ttu-id="7b61f-221">경우 페이지 처음 (되기 전에 실행 단추를 클릭 하면), 값 `Request.Form["title"]` null입니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-221">When the page first runs (before you click the button), the value of `Request.Form["title"]` is null.</span></span> <span data-ttu-id="7b61f-222">폼을 제출 하지만 `Request.Form["title"]` 의 값을 가져옵니다는 `title` 입력란입니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-222">But when you submit the form, `Request.Form["title"]` gets the value of the `title` text box.</span></span> <span data-ttu-id="7b61f-223">당연 하 게 되지 않지만 빈 입력란 isnotnull; 방금에 빈 문자열을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-223">It's not obvious, but an empty text box is not null; it just has an empty string in it.</span></span> <span data-ttu-id="7b61f-224">단추에 대 한 응답에서 코드를 실행할 때, 클릭 `Request.Form["title"]` 에 빈 문자열을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-224">So when the code runs in response to the button click, `Request.Form["title"]` has an empty string in it.</span></span>
> 
> <span data-ttu-id="7b61f-225">이러한 차이점으로이 인해 중요 한 이유는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="7b61f-225">Why is this distinction important?</span></span> <span data-ttu-id="7b61f-226">만들 때 합니다 *영화* 테이블을 명시적으로 말씀 하 신 null 수 필드 없음.</span><span class="sxs-lookup"><span data-stu-id="7b61f-226">When you created the *Movies* table, you explicitly said that none of the fields could be null.</span></span> <span data-ttu-id="7b61f-227">하지만 여기 새 영화에 대 한 입력 폼 있고 필드를 비워 두면 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-227">But here you have an entry form for new movies, and you're leaving fields blank.</span></span> <span data-ttu-id="7b61f-228">장르 또는 연도 대 한 값이 있는 하지 않은 새 동영상을 저장 하려고 할 때 불만을 데이터베이스 합리적으로 예상할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-228">You would reasonably expect the database to complain when you tried to save new movies that didn't have values for genre or year.</span></span> <span data-ttu-id="7b61f-229">점 이지만 &mdash; 빈 문자열 이기 때문에 해당 텍스트 상자를 비워 두면 하는 경우에 값을 null 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-229">But that's the point &mdash; even if you leave those text boxes blank, the values aren't null; they're empty strings.</span></span> <span data-ttu-id="7b61f-230">빈 이러한 열을 사용 하 여 데이터베이스에 새 영화를 저장할 수는 결과적으로, &mdash; 있지만 null이 아님!</span><span class="sxs-lookup"><span data-stu-id="7b61f-230">As a result, you're able to save new movies to the database with these columns empty &mdash; but not null!</span></span> <span data-ttu-id="7b61f-231">&mdash; 값</span><span class="sxs-lookup"><span data-stu-id="7b61f-231">&mdash; values.</span></span> <span data-ttu-id="7b61f-232">따라서 사용자가 사용자 입력의 유효성을 검사 하 여 수행할 수 있는 빈 문자열인 경우를 제출 하지 있는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-232">Therefore, you have to make sure that users don't submit an empty string, which you can do by validating the user's input.</span></span>


### <a name="the-validation-helper"></a><span data-ttu-id="7b61f-233">유효성 검사 도우미</span><span class="sxs-lookup"><span data-stu-id="7b61f-233">The Validation Helper</span></span>

<span data-ttu-id="7b61f-234">ASP.NET 웹 페이지 도우미가 포함 됩니다 &mdash; 는 `Validation` 도우미 &mdash; 사용자 입력 요구 사항을 충족 하는 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-234">ASP.NET Web Pages includes a helper &mdash; the `Validation` helper &mdash; that you can use to make sure that users enter data that meets your requirements.</span></span> <span data-ttu-id="7b61f-235">`Validation` 도우미에서 빌드하는 ASP.NET 웹 페이지에 이전 자습서에서 Gravatar 도우미를 설치 하는 방법은 NuGet을 사용 하 여 패키지로 설치할 필요가 도우미 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-235">The `Validation` helper is one of the helpers that's built in to ASP.NET Web Pages, so you don't have to install it as a package by using NuGet, the way you installed the Gravatar helper in an earlier tutorial.</span></span>

<span data-ttu-id="7b61f-236">사용자 입력의 유효성을 검사 하려면 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-236">To validate the user's input, you'll do the following:</span></span>

- <span data-ttu-id="7b61f-237">코드를 사용 하 여 페이지의 입력란에 필요한 값이 되도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-237">Use code to specify that you want to require values in the text boxes on the page.</span></span>
- <span data-ttu-id="7b61f-238">모든 항목이 제대로 확인 하는 경우에 동영상 정보가 데이터베이스에 추가 됩니다 있도록 코드에 테스트를 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-238">Put a test into the code so that the movie information is added to the database only if everything validates properly.</span></span>
- <span data-ttu-id="7b61f-239">오류 메시지를 표시 하는 태그에 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-239">Add code into the markup to display error messages.</span></span>

<span data-ttu-id="7b61f-240">코드 블록에는 *AddMovie* 페이지에서 오른쪽 위 변수 선언 앞 맨 위에 있는 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-240">In the code block in the *AddMovie* page, right up at the top before the variable declarations, add the following code:</span></span>

[!code-csharp[Main](entering-data/samples/sample7.cs)]

<span data-ttu-id="7b61f-241">문의할 `Validation.RequireField` 각 필드에 한 번씩 (`<input>` 요소)를 입력 해야 하는 하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-241">You call `Validation.RequireField` once for each field (`<input>` element) where you want to require an entry.</span></span> <span data-ttu-id="7b61f-242">또한 다음과 같은 각 호출에 대 한 사용자 지정 오류 메시지를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-242">You can also add a custom error message for each call, like you see here.</span></span> <span data-ttu-id="7b61f-243">(에서는 다양 한 메시지를 저장할 수 원하는 것을 보여 줍니다.)</span><span class="sxs-lookup"><span data-stu-id="7b61f-243">(We varied the messages just to show that you can put anything you like there.)</span></span>

<span data-ttu-id="7b61f-244">문제가 있으면 새 동영상 정보가 데이터베이스에 삽입 되지 않도록 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-244">If there's a problem, you want to prevent the new movie information from being inserted into the database.</span></span> <span data-ttu-id="7b61f-245">에 `if(IsPost)` 블록에서 사용 하 여 `&&` (논리적 AND) 테스트 하는 다른 조건을 추가 하려면 `Validation.IsValid()`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-245">In the `if(IsPost)` block, use `&&` (logical AND) to add another condition that tests `Validation.IsValid()`.</span></span> <span data-ttu-id="7b61f-246">완료 되 면, 전체 `if(IsPost)` 블록이이 코드와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-246">When you're done, the whole `if(IsPost)` block looks like this code:</span></span>

[!code-csharp[Main](entering-data/samples/sample8.cs)]

<span data-ttu-id="7b61f-247">사용 하 여 등록 하는 필드 중 하나를 사용 하 여 유효성 검사 오류가 있을 경우 합니다 `Validation` 도우미를 `Validation.IsValid` 메서드에서 false를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-247">If there's a validation error with any of the fields that you registered by using the `Validation` helper, the `Validation.IsValid` method returns false.</span></span> <span data-ttu-id="7b61f-248">및 이런 경우 해당 블록의 코드 없음은 실행, 되므로 잘못 된 영화 항목이 없는 데이터베이스에 삽입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-248">And in that case, none of the code in that block will run, so no invalid movie entries will be inserted into the database.</span></span> <span data-ttu-id="7b61f-249">물론 하지로 리디렉션됩니다 및 합니다 *영화* 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-249">And of course you're not redirected to the *Movies* page.</span></span>

<span data-ttu-id="7b61f-250">유효성 검사 코드를 포함 한 전체 코드 블록은 이제이 예제와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-250">The complete code block, including the validation code, now looks like this example:</span></span>

[!code-cshtml[Main](entering-data/samples/sample9.cshtml?highlight=10)]

## <a name="displaying-validation-errors"></a><span data-ttu-id="7b61f-251">유효성 검사 오류를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-251">Displaying Validation Errors</span></span>

<span data-ttu-id="7b61f-252">마지막 단계는 모든 오류 메시지를 표시 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-252">The last step is to display any error messages.</span></span> <span data-ttu-id="7b61f-253">각 유효성 검사 오류에 대 한 개별 메시지를 표시할 수 있습니다 또는 요약 하자면, 또는 둘 다 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-253">You can display individual messages for each validation error, or you can display a summary, or both.</span></span> <span data-ttu-id="7b61f-254">이 자습서에서는 수행 둘 다 작동 방식을 볼 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-254">For this tutorial, you'll do both so that you can see how it works.</span></span>

<span data-ttu-id="7b61f-255">각 옆에 있는 `<input>` 유효성을 검사 하는 요소를 호출 합니다 `Html.ValidationMessage` 메서드의 이름을 전달 하 고는 `<input>` 유효성을 검사 하는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-255">Next to each `<input>` element that you're validating, call the `Html.ValidationMessage` method and pass it the name of the `<input>` element you're validating.</span></span> <span data-ttu-id="7b61f-256">배치는 `Html.ValidationMessage` 오류 메시지를 표시 하려는 메서드를 오른쪽입니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-256">You put the `Html.ValidationMessage` method right where you want the error message to appear.</span></span> <span data-ttu-id="7b61f-257">페이지를 실행 하는 경우, `Html.ValidationMessage` 메서드 렌더링을 `<span>` 유효성 검사 오류를 어디로 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-257">When the page runs, the `Html.ValidationMessage` method renders a `<span>` element where the validation error will go.</span></span> <span data-ttu-id="7b61f-258">(오류가 없는 경우는 `<span>` 요소가 렌더링 하지만에 텍스트가 없습니다.)</span><span class="sxs-lookup"><span data-stu-id="7b61f-258">(If there's no error, the `<span>` element is rendered, but there's no text in it.)</span></span>

<span data-ttu-id="7b61f-259">페이지의 태그를 포함 하도록 변경를 `Html.ValidationMessage` 메서드는 세 가지에 대 한 `<input>` 이 예제에서와 같이 페이지의 요소:</span><span class="sxs-lookup"><span data-stu-id="7b61f-259">Change the markup in the page so that it includes an `Html.ValidationMessage` method for each of the three `<input>` elements on the page, like this example:</span></span>

[!code-cshtml[Main](entering-data/samples/sample10.cshtml?highlight=3,8,13)]

<span data-ttu-id="7b61f-260">요약의 작동 원리를 보려면도 다음 태그를 추가 하 고 바로 뒤에 있는 코드는 `<h1>Add a Movie</h1>` 페이지의 요소:</span><span class="sxs-lookup"><span data-stu-id="7b61f-260">To see how the summary works, also add the following markup and code right after the `<h1>Add a Movie</h1>` element on the page:</span></span>

[!code-cshtml[Main](entering-data/samples/sample11.cshtml)]

<span data-ttu-id="7b61f-261">기본적으로 `Html.ValidationSummary` 목록의 모든 유효성 검사 메시지를 표시 하는 메서드 (을 `<ul>` 내에 있는 요소를 `<div>` 요소).</span><span class="sxs-lookup"><span data-stu-id="7b61f-261">By default, the `Html.ValidationSummary` method displays all the validation messages in a list (a `<ul>` element that's inside a `<div>` element).</span></span> <span data-ttu-id="7b61f-262">와 마찬가지로 `Html.ValidationMessage` 메서드는 항상 유효성 검사 요약에 대 한 태그를 렌더링; 오류가 없는 경우에 목록 항목이 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-262">As with the `Html.ValidationMessage` method, the markup for the validation summary is always rendered; if there are no errors, no list items are rendered.</span></span>

<span data-ttu-id="7b61f-263">요약을 사용 하 여 대신 유효성 검사 메시지를 표시 하는 다른 방법은 수는 `Html.ValidationMessage` 각 필드 관련 오류를 표시 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-263">The summary can be an alternative way to display validation messages instead of by using the `Html.ValidationMessage` method to display each field-specific error.</span></span> <span data-ttu-id="7b61f-264">또는 요약 및 세부 정보를 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-264">Or you can use both a summary and the details.</span></span> <span data-ttu-id="7b61f-265">또는 사용할 수 있습니다는 `Html.ValidationSummary` 메서드를 일반 오류를 표시 하 고 사용 하 여 개별 `Html.ValidationMessage` 호출 세부 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-265">Or you can use the `Html.ValidationSummary` method to display a generic error and then use individual `Html.ValidationMessage` calls to display details.</span></span>

<span data-ttu-id="7b61f-266">완료 페이지는 이제이 예제와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-266">The complete page now looks like this example:</span></span>

[!code-cshtml[Main](entering-data/samples/sample12.cshtml)]

<span data-ttu-id="7b61f-267">이제</span><span class="sxs-lookup"><span data-stu-id="7b61f-267">That's it.</span></span> <span data-ttu-id="7b61f-268">이제 영화를 추가 하지만 하나 이상의 필드에서 페이지를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-268">You can now test the page by adding a movie but leaving out one or more of the fields.</span></span> <span data-ttu-id="7b61f-269">이렇게 하면 다음 오류가 표시 표시:</span><span class="sxs-lookup"><span data-stu-id="7b61f-269">When you do, you see the following error display:</span></span>

![유효성 검사 오류 메시지를 보여 주는 동영상 페이지 추가](entering-data/_static/image5.png)

## <a name="styling-the-validation-error-messages"></a><span data-ttu-id="7b61f-271">유효성 검사 오류 메시지의 스타일 지정</span><span class="sxs-lookup"><span data-stu-id="7b61f-271">Styling the Validation Error Messages</span></span>

<span data-ttu-id="7b61f-272">오류 메시지, 있지만 이러한 없는 소개할 잘 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-272">You can see that there are error messages, but they don't really stand out very well.</span></span> <span data-ttu-id="7b61f-273">하지만 오류 메시지의 스타일을 지정 하는 쉬운 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-273">There's an easy way to style the error messages, though.</span></span>

<span data-ttu-id="7b61f-274">개별 오류 메시지에 표시 되는 스타일을 지정 하려면 `Html.ValidationMessage`, 명명 된 CSS 스타일 클래스를 만듭니다 `field-validation-error`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-274">To style the individual error messages that are displayed by `Html.ValidationMessage`, create a CSS style class named `field-validation-error`.</span></span> <span data-ttu-id="7b61f-275">유효성 검사 요약에 대 한 모양을 정의 만들려면 CSS 스타일 클래스가 `validation-summary-errors`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-275">To define the look for the validation summary, create a CSS style class named `validation-summary-errors`.</span></span>

<span data-ttu-id="7b61f-276">이 기술은 작동 방식을 확인 하려면 추가 `<style>` 내부 요소는 `<head>` 페이지의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-276">To see how this technique works, add a `<style>` element inside the `<head>` section of the page.</span></span> <span data-ttu-id="7b61f-277">그런 다음 이라는 스타일 클래스를 정의 `field-validation-error` 고 `validation-summary-errors` 다음 규칙을 포함 하는:</span><span class="sxs-lookup"><span data-stu-id="7b61f-277">Then define style classes named `field-validation-error` and `validation-summary-errors` that contain the following rules:</span></span>

[!code-cshtml[Main](entering-data/samples/sample13.cshtml?highlight=4-17)]

<span data-ttu-id="7b61f-278">일반적으로 추가할 수 있습니다를 별도의 스타일 정보 *.css* 파일을 간단 하 게 배치할 수 있는 페이지에 이제 있지만.</span><span class="sxs-lookup"><span data-stu-id="7b61f-278">Normally you'd probably put style information into a separate *.css* file, but for simplicity you can put them in the page for now.</span></span> <span data-ttu-id="7b61f-279">(이 자습서 집합의 뒷부분에 나오는 별도의 CSS 규칙 이동해 봅니다 *.css* 파일입니다.)</span><span class="sxs-lookup"><span data-stu-id="7b61f-279">(Later in this tutorial set, you'll move the CSS rules to a separate *.css* file.)</span></span>

<span data-ttu-id="7b61f-280">유효성 검사 오류가 있을 경우는 `Html.ValidationMessage` 렌더링 메서드를 `<span>` 요소를 포함 하는 `class="field-validation-error"`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-280">If there's a validation error, the `Html.ValidationMessage` method renders a `<span>` element that includes `class="field-validation-error"`.</span></span> <span data-ttu-id="7b61f-281">해당 클래스에 대 한 스타일 정의 추가 하 여 메시지 모양을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-281">By adding a style definition for that class, you can configure what the message looks like.</span></span> <span data-ttu-id="7b61f-282">오류가 있을 경우 합니다 `ValidationSummary` 메서드는 동적으로 마찬가지로 특성을 렌더링 `class="validation-summary-errors"`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-282">If there are errors, the `ValidationSummary` method likewise dynamically renders the attribute `class="validation-summary-errors"`.</span></span>

<span data-ttu-id="7b61f-283">페이지를 다시 실행 하 고 몇 가지 필드를 의도적으로 생략 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-283">Run the page again and deliberately leave out a couple of the fields.</span></span> <span data-ttu-id="7b61f-284">오류를 좀 더 눈에 띄는 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-284">The errors are now more noticeable.</span></span> <span data-ttu-id="7b61f-285">(실제로 overdone 하 고, 이지만 수행할 수 있는 작업을 보여 줍니다.)</span><span class="sxs-lookup"><span data-stu-id="7b61f-285">(In fact, they're overdone, but that's just to show what you can do.)</span></span>

![스타일을 지정 하는 유효성 검사 오류를 보여 주는 동영상 페이지 추가](entering-data/_static/image6.png)

## <a name="adding-a-link-to-the-movies-page"></a><span data-ttu-id="7b61f-287">Movies 페이지로 링크를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-287">Adding a Link to the Movies Page</span></span>

<span data-ttu-id="7b61f-288">마지막 단계는 이동에 편리 하 게 합니다 *AddMovie* 원래 영화 목록에서 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-288">One final step is to make it convenient to get to the *AddMovie* page from the original movie listing.</span></span>

<span data-ttu-id="7b61f-289">엽니다는 *영화* 페이지를 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-289">Open the *Movies* page again.</span></span> <span data-ttu-id="7b61f-290">닫은 후 `</div>` 뒤에 오는 태그의 `WebGrid` 도우미, 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-290">After the closing `</div>` tag that follows the `WebGrid` helper, add the following markup:</span></span>

[!code-cshtml[Main](entering-data/samples/sample14.cshtml)]

<span data-ttu-id="7b61f-291">ASP.NET 해석 하기 전에 살펴본 것 처럼는 `~` 연산자 웹 사이트의 루트 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-291">As you saw before, ASP.NET interprets the `~` operator as the root of the website.</span></span> <span data-ttu-id="7b61f-292">사용할 필요가 없습니다 합니다 `~` 연산자; 태그를 사용할 수 있습니다 `<a href="./AddMovie">Add a movie</a>` 또는 HTML 이해 하는 경로 정의 하는 다른 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-292">You don't have to use the `~` operator; you could use the markup `<a href="./AddMovie">Add a movie</a>` or some other way to define the path that HTML understands.</span></span> <span data-ttu-id="7b61f-293">하지만 `~` 연산자는 좋은 일반 방법 Razor 페이지에 대 한 링크를 만들 때 사이트를 보다 유연 하므로-하위 폴더에 현재 페이지를 이동 하는 경우 링크도 계속 이동 합니다 *AddMovie* 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-293">But the `~` operator is a good general approach when you create links for Razor pages, because it makes the site more flexible — if you move the current page to a subfolder, the link will still go to the *AddMovie* page.</span></span> <span data-ttu-id="7b61f-294">(유의 해야 합니다 `~` 연산자만 *.cshtml* 페이지.</span><span class="sxs-lookup"><span data-stu-id="7b61f-294">(Remember that the `~` operator only works in *.cshtml* pages.</span></span> <span data-ttu-id="7b61f-295">ASP.NET 이해 하지만 표준 HTML 아닙니다.)</span><span class="sxs-lookup"><span data-stu-id="7b61f-295">ASP.NET understands it, but it's not standard HTML.)</span></span>

<span data-ttu-id="7b61f-296">완료 되 면 실행 합니다 *영화* 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-296">When you're done, run the *Movies* page.</span></span> <span data-ttu-id="7b61f-297">이 페이지 처럼 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-297">It will look like this page:</span></span>

![추가 동영상 페이지 링크를 사용 하 여 동영상 페이지](entering-data/_static/image7.png)

<span data-ttu-id="7b61f-299">클릭 합니다 **동영상 추가** 이동 하는지 확인 하는 링크는 *AddMovie* 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-299">Click the **Add a movie** link to make sure that it goes to the *AddMovie* page.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="7b61f-300">다음에 나오는</span><span class="sxs-lookup"><span data-stu-id="7b61f-300">Coming Up Next</span></span>

<span data-ttu-id="7b61f-301">다음 자습서에서는 사용자가 데이터베이스에 이미 있는 데이터를 편집할 수 있도록 하는 방법에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-301">In the next tutorial, you'll learn how to let users edit data that's already in the database.</span></span>

## <a name="complete-listing-for-addmovie-page"></a><span data-ttu-id="7b61f-302">AddMovie 페이지에 대 한 전체 목록</span><span class="sxs-lookup"><span data-stu-id="7b61f-302">Complete Listing for AddMovie Page</span></span>

[!code-cshtml[Main](entering-data/samples/sample15.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="7b61f-303">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="7b61f-303">Additional Resources</span></span>

- [<span data-ttu-id="7b61f-304">Razor 구문을 사용 하 여 ASP.NET 웹 프로그래밍 소개</span><span class="sxs-lookup"><span data-stu-id="7b61f-304">Introduction to ASP.NET Web Programming Using the Razor Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkID=202890)
- <span data-ttu-id="7b61f-305">[SQL 삽입에 문을](http://www.w3schools.com/sql/sql_insert.asp) W3Schools 사이트</span><span class="sxs-lookup"><span data-stu-id="7b61f-305">[SQL INSERT INTO Statement](http://www.w3schools.com/sql/sql_insert.asp) on the W3Schools site</span></span>
- <span data-ttu-id="7b61f-306">[Asp.net에서 사용자 입력 유효성 검사 페이지 사이트](https://go.microsoft.com/fwlink/?LinkId=253002)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-306">[Validating User Input in ASP.NET Web Pages Sites](https://go.microsoft.com/fwlink/?LinkId=253002).</span></span> <span data-ttu-id="7b61f-307">작업에 대 한 자세한 정보는 `Validation` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="7b61f-307">More information about working with the `Validation` helper.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7b61f-308">[이전](form-basics.md)
> [다음](updating-data.md)</span><span class="sxs-lookup"><span data-stu-id="7b61f-308">[Previous](form-basics.md)
[Next](updating-data.md)</span></span>
