---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/entering-data
title: "ASP.NET 웹 페이지를 소개-양식을 사용 하 여 데이터베이스 데이터를 입력 합니다. | Microsoft Docs"
author: tfitzmac
description: "이 자습서에서는 입력 폼을 만들고 다음에서 얻을 수 있는 폼을 데이터베이스 테이블에 ASP.NET 웹 페이지 (...를 사용 하는 경우 데이터를 입력 하는 방법을 보여 줍니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/28/2015
ms.topic: article
ms.assetid: d37c93fc-25fd-4e94-8671-0d437beef206
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/entering-data
msc.type: authoredcontent
ms.openlocfilehash: b74eecb16b2c4695bb417816b90f701f724cc9d0
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="introducing-aspnet-web-pages---entering-database-data-by-using-forms"></a><span data-ttu-id="ac7c9-103">ASP.NET 웹 페이지를 소개-양식을 사용 하 여 데이터베이스 데이터를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-103">Introducing ASP.NET Web Pages - Entering Database Data by Using Forms</span></span>
====================
<span data-ttu-id="ac7c9-104">으로 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="ac7c9-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="ac7c9-105">이 자습서에서는 입력 폼을 만들고 다음에서 얻을 수 있는 폼을 데이터베이스 테이블에 ASP.NET 웹 페이지 (Razor)를 사용 하는 경우 데이터를 입력 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-105">This tutorial shows you how to create an entry form and then enter the data that you get from the form into a database table when you use ASP.NET Web Pages (Razor).</span></span> <span data-ttu-id="ac7c9-106">통해 시리즈를 완료 한 것으로 가정 [기본 사항의 HTML 폼 ASP.NET 웹 페이지에서](https://go.microsoft.com/fwlink/?LinkId=251581)합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-106">It assumes you have completed the series through [Basics of HTML Forms in ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251581).</span></span>
> 
> <span data-ttu-id="ac7c9-107">학습 내용:</span><span class="sxs-lookup"><span data-stu-id="ac7c9-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="ac7c9-108">입력 폼을 처리 하는 방법에 대 한 자세히 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-108">More about how to process entry forms.</span></span>
> - <span data-ttu-id="ac7c9-109">(삽입) 데이터는 데이터베이스에 추가 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-109">How to add (insert) data in a database.</span></span>
> - <span data-ttu-id="ac7c9-110">사용자가 형태로 (사용자 입력의 유효성을 검사 하는 방법)에 필요한 값으로 입력 했는지 확인 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-110">How to make sure that users have entered a required value in a form (how to validate user input).</span></span>
> - <span data-ttu-id="ac7c9-111">유효성 검사 오류를 표시 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-111">How to display validation errors.</span></span>
> - <span data-ttu-id="ac7c9-112">현재 페이지에서 다른 페이지로 이동 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-112">How to jump to another page from the current page.</span></span>
>   
> 
> <span data-ttu-id="ac7c9-113">기능/기술을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-113">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="ac7c9-114">`Database.Execute` 메서드</span><span class="sxs-lookup"><span data-stu-id="ac7c9-114">The `Database.Execute` method.</span></span>
> - <span data-ttu-id="ac7c9-115">SQL `Insert Into` 문</span><span class="sxs-lookup"><span data-stu-id="ac7c9-115">The SQL `Insert Into` statement</span></span>
> - <span data-ttu-id="ac7c9-116">`Validation` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-116">The `Validation` helper.</span></span>
> - <span data-ttu-id="ac7c9-117">`Response.Redirect` 메서드</span><span class="sxs-lookup"><span data-stu-id="ac7c9-117">The `Response.Redirect` method.</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="ac7c9-118">만들 것인지</span><span class="sxs-lookup"><span data-stu-id="ac7c9-118">What You'll Build</span></span>

<span data-ttu-id="ac7c9-119">자습서의 이전 버전 데이터베이스를 만드는 방법을 살펴보았습니다를 입력 한 데이터베이스 데이터는 데이터베이스에서 작업 하는 WebMatrix에서 직접 편집 하 여는 **데이터베이스** 작업 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-119">In the tutorial earlier that showed you how to create a database, you entered database data by editing the database directly in WebMatrix, working in the **Database** workspace.</span></span> <span data-ttu-id="ac7c9-120">대부분의 응용 프로그램 없는에 있지만 데이터베이스에 데이터를 저장 하는 실용적인 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-120">In most apps, that's not a practical way to put data into the database, though.</span></span> <span data-ttu-id="ac7c9-121">따라서이 자습서에서는 모든 사용자 데이터를 입력 하 고 데이터베이스에 저장할 수 있는 웹 기반 인터페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-121">So in this tutorial, you'll create a web-based interface that lets you or anyone enter data and save it to the database.</span></span>

<span data-ttu-id="ac7c9-122">새 동영상을 입력할 수 있는 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-122">You'll create a page where you can enter new movies.</span></span> <span data-ttu-id="ac7c9-123">페이지 입력 폼에 영화 제목, genre 및 연도 입력할 수 있는 필드가 (텍스트 상자)을 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-123">The page will contain an entry form that has fields (text boxes) where you can enter a movie title, genre, and year.</span></span> <span data-ttu-id="ac7c9-124">페이지는이 페이지와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-124">The page will look like this page:</span></span>

![브라우저에서 영화 추가' 페이지](entering-data/_static/image1.png)

<span data-ttu-id="ac7c9-126">텍스트 상자에는 HTML 됩니다 `<input>` 조회 하는 요소에는이 태그와 같은:</span><span class="sxs-lookup"><span data-stu-id="ac7c9-126">The text boxes will be HTML `<input>` elements that will look like this markup:</span></span>

`<input type="text" name="genre" value="" />`

## <a name="creating-the-basic-entry-form"></a><span data-ttu-id="ac7c9-127">기본 입력 양식 만들기</span><span class="sxs-lookup"><span data-stu-id="ac7c9-127">Creating the Basic Entry Form</span></span>

<span data-ttu-id="ac7c9-128">*AddMovie.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-128">Create a page named *AddMovie.cshtml*.</span></span>

<span data-ttu-id="ac7c9-129">다음 태그를 사용 하 여 파일에 무엇이 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-129">Replace what's in the file with the following markup.</span></span> <span data-ttu-id="ac7c9-130">모든; 덮어쓰기 맨 위에 있는 코드 블록 곧 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-130">Overwrite everything; you'll add a code block at the top shortly.</span></span>

[!code-cshtml[Main](entering-data/samples/sample1.cshtml)]

<span data-ttu-id="ac7c9-131">이 예제에서는 일반적인 HTML 양식 만들기</span><span class="sxs-lookup"><span data-stu-id="ac7c9-131">This example shows typical HTML for creating a form.</span></span> <span data-ttu-id="ac7c9-132">사용 하 여 `<input>` 전송 단추 및 텍스트 상자에 대 한 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-132">It uses `<input>` elements for the text boxes and for the submit button.</span></span> <span data-ttu-id="ac7c9-133">텍스트 상자에 대 한 캡션의 표준을 사용 하 여 만들어진 `<label>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-133">The captions for the text boxes are created by using standard `<label>` elements.</span></span> <span data-ttu-id="ac7c9-134">`<fieldset>` 및 `<legend>` 요소 좋은 상자 폼 주위에 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-134">The `<fieldset>` and `<legend>` elements put a nice box around the form.</span></span>

<span data-ttu-id="ac7c9-135">이 페이지에서는 `<form>` 요소 사용 하 여 `post` 에 대 한 값으로는 `method` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-135">Notice that in this page, the `<form>` element uses `post` as the value for the `method` attribute.</span></span> <span data-ttu-id="ac7c9-136">이전 자습서에서 사용 하는 폼 만들었습니다는 `get` 메서드.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-136">In the previous tutorial, you created a form that used the `get` method.</span></span> <span data-ttu-id="ac7c9-137">그건 정확한 값을 서버, 폼 전송 있지만 요청 하지 변경한 내용이 때문에.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-137">That was correct, because although the form submitted values to the server, the request did not make any changes.</span></span> <span data-ttu-id="ac7c9-138">수행한 모든 다른 방법으로 데이터를 가져오고 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-138">All it did was fetch data in different ways.</span></span> <span data-ttu-id="ac7c9-139">그러나이 사용자에 게 알려줍니다 *됩니다* 변경-새 데이터베이스 레코드를 추가 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-139">However, in this page you *will* make changes—you're going to add new database records.</span></span> <span data-ttu-id="ac7c9-140">따라서이 양식을 사용 해야는 `post` 메서드.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-140">Therefore, this form should use the `post` method.</span></span> <span data-ttu-id="ac7c9-141">(간의 차이 대 한 자세한 `GET` 및 `POST` 작업의 경우 참조는[GET, POST 및 HTTP 동사 안전](https://go.microsoft.com/fwlink/?LinkId=251581#GET,_POST,_and_HTTP_Verb_Safety) 이전 자습서에서 사이드바.)</span><span class="sxs-lookup"><span data-stu-id="ac7c9-141">(For more about the difference between `GET` and `POST` operations, see the[GET, POST, and HTTP Verb Safety](https://go.microsoft.com/fwlink/?LinkId=251581#GET,_POST,_and_HTTP_Verb_Safety) sidebar in the previous tutorial.)</span></span>

<span data-ttu-id="ac7c9-142">각 텍스트 상자에는 한 `name` 요소 (`title`, `genre`, `year`).</span><span class="sxs-lookup"><span data-stu-id="ac7c9-142">Note that each text box has a `name` element (`title`, `genre`, `year`).</span></span> <span data-ttu-id="ac7c9-143">이전 자습서에서 살펴본 것 처럼 사용자의 입력을 나중에 가져올 수 있도록 이러한 이름을 해야 하기 때문에 이러한 이름은 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-143">As you saw in the previous tutorial, these names are important because you must have those names so you can get the user's input later.</span></span> <span data-ttu-id="ac7c9-144">모든 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-144">You can use any names.</span></span> <span data-ttu-id="ac7c9-145">하는 것이 좋습니다 수 있는 의미 있는 이름을 사용 하 여 작업할 때 데이터를 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-145">It's helpful to use meaningful names that help you remember what data you're working with.</span></span>

<span data-ttu-id="ac7c9-146">`value` 각 특성 `<input>` Razor 코드의 비트를 포함 하는 요소 (예를 들어 `Request.Form["title"]`).</span><span class="sxs-lookup"><span data-stu-id="ac7c9-146">The `value` attribute of each `<input>` element contains a bit of Razor code (for example, `Request.Form["title"]`).</span></span> <span data-ttu-id="ac7c9-147">폼 전송한 후이 트릭의 버전 (있는 경우) 텍스트 상자에 입력 한 값을 보존 하려면 이전 자습서에서 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-147">You learned a version of this trick in the previous tutorial to preserve the value entered into the text box (if any) after the form has been submitted.</span></span>

## <a name="getting-the-form-values"></a><span data-ttu-id="ac7c9-148">폼 값 가져오기</span><span class="sxs-lookup"><span data-stu-id="ac7c9-148">Getting the Form Values</span></span>

<span data-ttu-id="ac7c9-149">다음으로 양식을 처리 하는 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-149">Next, you add code that processes the form.</span></span> <span data-ttu-id="ac7c9-150">개요에서는 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-150">In outline, you'll do the following:</span></span>

1. <span data-ttu-id="ac7c9-151">페이지가 게시 되 고 있는지 여부를 확인 하십시오 (전송) 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-151">Check whether the page is being posted (was submitted).</span></span> <span data-ttu-id="ac7c9-152">코드를 실행 하려면 페이지를 처음 실행할 때가 아니라 사용자가 단추를 클릭 한 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-152">You want to your code to run only when users have clicked the button, not when the page first runs.</span></span>
2. <span data-ttu-id="ac7c9-153">사용자가 텍스트 상자에 입력 한 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-153">Get the values that the user entered into the text boxes.</span></span> <span data-ttu-id="ac7c9-154">이 경우 폼 사용 중이기 때문에 `POST` 양식 값을 가져올 동사는 `Request.Form` 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-154">In this case, because the form is using the `POST` verb, you get the form values from the `Request.Form` collection.</span></span>
3. <span data-ttu-id="ac7c9-155">값에서 새 레코드를 삽입는 *동영상* 데이터베이스 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-155">Insert the values as a new record in the *Movies* database table.</span></span>

<span data-ttu-id="ac7c9-156">파일 맨 위에 있는 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-156">At the top of the file, add the following code:</span></span>

[!code-cshtml[Main](entering-data/samples/sample2.cshtml)]

<span data-ttu-id="ac7c9-157">처음 몇 줄 변수를 만듭니다 (`title`, `genre`, 및 `year`) 텍스트 상자에서 값을 보유 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-157">The first few lines create variables (`title`, `genre`, and `year`) to hold the values from the text boxes.</span></span> <span data-ttu-id="ac7c9-158">줄 `if(IsPost)` 변수 설정 되어 있는지를 사용 하면 *만* 사용자가 클릭 하면는 **동영상 추가** 단추-즉 때 폼 게시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-158">The line `if(IsPost)` makes sure that the variables are set *only* when users click the **Add Movie** button — that is, when the form has been posted.</span></span>

<span data-ttu-id="ac7c9-159">와 같은 식을 사용 하 여 입력란의 값을 가져올 이전 자습서에서 살펴본 것 처럼 `Request.Form["name"]`여기서 *이름* 의 이름인는 `<input>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-159">As you saw in an earlier tutorial, you get the value of a text box by using an expression like `Request.Form["name"]`, where *name* is the name of the `<input>` element.</span></span>

<span data-ttu-id="ac7c9-160">변수 이름 (`title`, `genre`, 및 `year`) 임의적입니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-160">The names of the variables (`title`, `genre`, and `year`) are arbitrary.</span></span> <span data-ttu-id="ac7c9-161">에 할당 된 이름이 같은 `<input>` 요소를 호출할 수 있습니다 필요 하면 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-161">Like the names that you assign to `<input>` elements, you can call them anything you like.</span></span> <span data-ttu-id="ac7c9-162">(Name 특성을 일치 시키기 않아도 변수 이름 `<input>` 폼에서 요소가 있습니다.) 하지만과 마찬가지로 `<input>` 요소 것이 포함 된 데이터를 반영 하는 변수 이름을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-162">(The names of the variables don't have to match the name attributes of `<input>` elements on the form.) But as with the `<input>` elements, it's a good idea to use variable names that reflect the data that they contain.</span></span> <span data-ttu-id="ac7c9-163">코드를 작성할 때 일관 된 이름을 쉽게 작업할 때 데이터를 기억 하기.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-163">When you write code, consistent names make it easier for you to remember what data you're working with.</span></span>

## <a name="adding-data-to-the-database"></a><span data-ttu-id="ac7c9-164">데이터베이스에 데이터 추가</span><span class="sxs-lookup"><span data-stu-id="ac7c9-164">Adding Data to the Database</span></span>

<span data-ttu-id="ac7c9-165">코드에서 방금 추가한, 정당한 차단 *내* 닫는 중괄호 ( `}` )의 `if` (뿐 아니라 코드 블록) 블록을 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-165">In the code block you just added, just *inside* the closing brace ( `}` ) of the `if` block (not just inside the code block), add the following code:</span></span>

[!code-csharp[Main](entering-data/samples/sample3.cs)]

<span data-ttu-id="ac7c9-166">이 예에서는 데이터를 인출 하 고 표시 하기 위해 이전 자습서에 사용 되는 코드와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-166">This example is similar to the code you used in a previous tutorial to fetch and display data.</span></span> <span data-ttu-id="ac7c9-167">로 시작 하는 줄 `db =` 이전과 같은 데이터베이스가 고 다음 줄으로 SQL 문을 다시 정의 열립니다 앞입니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-167">The line that starts with `db =` opens the database, like before, and the next line defines a SQL statement, again as you saw before.</span></span> <span data-ttu-id="ac7c9-168">그러나이 이번 정의 SQL `Insert Into` 문.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-168">However, this time it defines a SQL `Insert Into` statement.</span></span> <span data-ttu-id="ac7c9-169">다음 예제에서는 일반 구문은 `Insert Into` 문:</span><span class="sxs-lookup"><span data-stu-id="ac7c9-169">The following example shows the general syntax of the `Insert Into` statement:</span></span>

`INSERT INTO table (column1, column2, column3, ...) VALUES (value1, value2, value3, ...)`

<span data-ttu-id="ac7c9-170">즉, 테이블에 삽입할 다음을 삽입할 열을 나열 한 다음 삽입할 값을 나열 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-170">In other words, you specify the table to insert into, then list the columns to insert into, and then list the values to insert.</span></span> <span data-ttu-id="ac7c9-171">(앞에서 설명한 것 처럼 SQL은 대/소문자 구분 하지 않지만 어떤 사람들 쉽게 명령을 읽을 수 있도록 키워드를 대문자로 바꿉니다.)</span><span class="sxs-lookup"><span data-stu-id="ac7c9-171">(As noted before, SQL is not case sensitive but some people capitalize the keywords to make it easier to read the command.)</span></span>

<span data-ttu-id="ac7c9-172">열에 삽입 하기에 이미 명령에 나열- `(Title, Genre, Year)`합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-172">The columns that you're inserting into are already listed in the command — `(Title, Genre, Year)`.</span></span> <span data-ttu-id="ac7c9-173">재미 있는 것으로 텍스트 상자에서 값을 얻는 방법의 `VALUES` 명령에 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-173">The interesting part is how you get the values from the text boxes into the `VALUES` part of the command.</span></span> <span data-ttu-id="ac7c9-174">실제 값 대신 참조 `@0`, `@1`, 및 `@2`은 물론 자리 표시자입니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-174">Instead of actual values, you see `@0`, `@1`, and `@2`, which are of course placeholders.</span></span> <span data-ttu-id="ac7c9-175">명령을 실행 하는 경우 (에 `db.Execute` 줄)을 텍스트 상자에서 가져온 값을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-175">When you run the command (on the `db.Execute` line), you pass the values that you got from the text boxes.</span></span>

<span data-ttu-id="ac7c9-176">**기억해 야 합니다.**</span><span class="sxs-lookup"><span data-stu-id="ac7c9-176">**Important!**</span></span> <span data-ttu-id="ac7c9-177">여기에 표시 된 대로 SQL 문에서 사용자가 온라인 입력 데이터도 포함 해야 하는 유일한 방법은 자리 표시자를 사용 하는 (`VALUES(@0, @1, @2)`).</span><span class="sxs-lookup"><span data-stu-id="ac7c9-177">Remember that the only way you should ever include data entered online by a user in a SQL statement is to use placeholders, as you see here (`VALUES(@0, @1, @2)`).</span></span> <span data-ttu-id="ac7c9-178">SQL 문으로 사용자 입력을 연결 하면 열면 사용자가 직접 SQL 주입 공격에에 설명 된 대로 [양식 기본 ASP.NET 웹 페이지에서](https://go.microsoft.com/fwlink/?LinkId=251581) (이전 자습서).</span><span class="sxs-lookup"><span data-stu-id="ac7c9-178">If you concatenate user input into a SQL statement, you open yourself to a SQL injection attack, as explained in [Form Basics in ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251581) (the previous tutorial).</span></span>

<span data-ttu-id="ac7c9-179">내부 여전히는 `if` 블록을 뒤에 다음 줄 추가 `db.Execute` 줄:</span><span class="sxs-lookup"><span data-stu-id="ac7c9-179">Still inside the `if` block, add the following line after the `db.Execute` line:</span></span>

[!code-css[Main](entering-data/samples/sample4.css)]

<span data-ttu-id="ac7c9-180">새 동영상 데이터베이스에 삽입 한 후이 선 점프 있습니다 (리디렉션을)는 *동영상* 페이지 방금 입력 한 동영상을 볼 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-180">After the new movie has been inserted into the database, this line jumps you (redirects) to the *Movies* page so you can see the movie you just entered.</span></span> <span data-ttu-id="ac7c9-181">`~` 연산자 의미 "웹 사이트의 루트입니다."</span><span class="sxs-lookup"><span data-stu-id="ac7c9-181">The `~` operator means "root of the website."</span></span> <span data-ttu-id="ac7c9-182">(의 `~` 연산자 일반적으로 HTML에 없는 ASP.NET 페이지 에서만에서 작동 합니다.)</span><span class="sxs-lookup"><span data-stu-id="ac7c9-182">(The `~` operator works only in ASP.NET pages, not in HTML generally.)</span></span>

<span data-ttu-id="ac7c9-183">이 예제와 같이 전체 코드 블록:</span><span class="sxs-lookup"><span data-stu-id="ac7c9-183">The complete code block looks like this example:</span></span>

[!code-cshtml[Main](entering-data/samples/sample5.cshtml)]

## <a name="testing-the-insert-command-so-far"></a><span data-ttu-id="ac7c9-184">Insert 명령 (지금까지) 테스트</span><span class="sxs-lookup"><span data-stu-id="ac7c9-184">Testing the Insert Command (So Far)</span></span>

<span data-ttu-id="ac7c9-185">아직 완료 되지 않았음을 하지만 이제는 것이 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-185">You're not done yet, but now is a good time to test.</span></span>

<span data-ttu-id="ac7c9-186">WebMatrix에 있는 파일의 트리 뷰에서 마우스 오른쪽 단추로 클릭는 *AddMovie.cshtml* 페이지 한 다음 클릭 **브라우저에서 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-186">In the tree view of files in WebMatrix, right-click the *AddMovie.cshtml* page and then click **Launch in browser**.</span></span>

![브라우저에서 영화 추가' 페이지](entering-data/_static/image2.png)

<span data-ttu-id="ac7c9-188">(브라우저에서 다른 페이지와 /fd 경우 URL이 있는지 확인 `http://localhost:nnnnn/AddMovie`) 여기서  *nnnnn*  사용 중인 포트 번호입니다.)</span><span class="sxs-lookup"><span data-stu-id="ac7c9-188">(If you end up with a different page in the browser, make sure that the URL is `http://localhost:nnnnn/AddMovie`), where *nnnnn* is the port number that you're using.)</span></span>

<span data-ttu-id="ac7c9-189">오류 페이지 어?</span><span class="sxs-lookup"><span data-stu-id="ac7c9-189">Did you get an error page?</span></span> <span data-ttu-id="ac7c9-190">그렇다면 읽어 주십시오. 하 고 앞에 나열 된 어떤 코드 정확 하 게 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-190">If so, read it carefully and make sure that the code looks exactly what was listed earlier.</span></span>

<span data-ttu-id="ac7c9-191">동영상 형식으로 입력 &mdash; 예를 들어 "시민 마 창", "드라마" 및 "1941"를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-191">Enter a movie in the form &mdash; for example, use "Citizen Kane", "Drama", and "1941".</span></span> <span data-ttu-id="ac7c9-192">키나 합니다. 클릭 **동영상 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-192">(Or whatever.) Then click **Add Movie**.</span></span>

<span data-ttu-id="ac7c9-193">때로 리디렉션되 하는 모든 코드가 정상적으로 작동 하는 경우는 *동영상* 페이지.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-193">If all goes well, you're redirected to the *Movies* page.</span></span> <span data-ttu-id="ac7c9-194">새 동영상 표시 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-194">Make sure that your new movie is listed.</span></span>

![동영상 페이지 새로 보여 주는 동영상 추가](entering-data/_static/image3.png)

## <a name="validating-user-input"></a><span data-ttu-id="ac7c9-196">사용자 입력 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="ac7c9-196">Validating User Input</span></span>

<span data-ttu-id="ac7c9-197">로 돌아가기는 *AddMovie* 페이지 또는 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-197">Go back to the *AddMovie* page, or run it again.</span></span> <span data-ttu-id="ac7c9-198">제목을 입력, 다른 동영상 하지만이 이번 입력 &mdash; 예를 들어 "비에서 시스템을 사용해 봅시다 '"을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-198">Enter another movie, but this time, enter only the title &mdash; for example, enter "Singin' in the Rain".</span></span> <span data-ttu-id="ac7c9-199">클릭 **동영상 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-199">Then click **Add Movie**.</span></span>

<span data-ttu-id="ac7c9-200">리디렉션됩니다 하는 *동영상* 페이지를 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-200">You're redirected to the *Movies* page again.</span></span> <span data-ttu-id="ac7c9-201">새 동영상을 찾을 수 있지만 완료 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-201">You can find the new movie, but it's incomplete.</span></span>

![특정 값이 없는 동영상 페이지 보여 주는 새 동영상](entering-data/_static/image4.png)

<span data-ttu-id="ac7c9-203">만들 때의 *동영상* 테이블을 명시적으로 라고 하는 필드는 null 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-203">When you created the *Movies* table, you explicitly said that none of the fields could be null.</span></span> <span data-ttu-id="ac7c9-204">여기서 새 동영상에 대 한 입력 양식 있고 있습니다 하는 필드를 비워 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-204">Here you have an entry form for new movies, and you're leaving fields blank.</span></span> <span data-ttu-id="ac7c9-205">가 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-205">That's an error.</span></span>

<span data-ttu-id="ac7c9-206">이 경우 데이터베이스 실제로 발생 하지 않은 (또는 *throw*) 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-206">In this case, the database didn't actually raise (or *throw*) an error.</span></span> <span data-ttu-id="ac7c9-207">장르 또는 연도별로 하므로 제공 하지 않은 코드에는 *AddMovie* 페이지 소위으로 해당 값을 처리 *빈 문자열과*합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-207">You didn't supply a genre or year, so the code in the *AddMovie* page treated those values as so-called *empty strings*.</span></span> <span data-ttu-id="ac7c9-208">때 SQL `Insert Into` 명령이 실행, genre 및 year 필드에 유용한 데이터가 포함 되어 있지 않습니다 되지만 null 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-208">When the SQL `Insert Into` command ran, the genre and year fields didn't have useful data in them, but they weren't null.</span></span>

<span data-ttu-id="ac7c9-209">물론, 사용자가 데이터베이스에 비어 있지 절반 영화 정보를 입력 하지 않으려면입니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-209">Obviously, you don't want to let users enter half-empty movie information into the database.</span></span> <span data-ttu-id="ac7c9-210">솔루션은 사용자의 입력을 확인 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-210">The solution is to validate the user's input.</span></span> <span data-ttu-id="ac7c9-211">처음에 유효성 검사는 단순히 있는지 확인은 사용자가 모든 필드에 대 한 값을 입력 했는지 (즉, 않은 빈 문자열을 포함).</span><span class="sxs-lookup"><span data-stu-id="ac7c9-211">Initially, the validation will simply make sure that the user has entered a value for all of the fields (that is, that none of them contains an empty string).</span></span>

> [!TIP] 
> 
> <span data-ttu-id="ac7c9-212">**Null 및 빈 문자열**</span><span class="sxs-lookup"><span data-stu-id="ac7c9-212">**Null and Empty Strings**</span></span>
> 
> <span data-ttu-id="ac7c9-213">프로그래밍에서 다른 개념 "값이 없습니다."의 구별</span><span class="sxs-lookup"><span data-stu-id="ac7c9-213">In programming, there's a distinction between different notions of "no value."</span></span> <span data-ttu-id="ac7c9-214">값은 일반적으로 *null* 설정 하거나 어떤 방식으로든에서 초기화 되지 한 경우.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-214">In general, a value is *null* if it has never been set or initialized in any way.</span></span> <span data-ttu-id="ac7c9-215">반면 문자 데이터 (문자열)를 필요로 하는 변수를 설정할 수 있습니다는 *빈 문자열*합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-215">In contrast, a variable that expects character data (strings) can be set to an *empty string*.</span></span> <span data-ttu-id="ac7c9-216">값이 null입니다;이 경우 것은 바로 명시적으로 설정 되어 길이가 0 인 자의 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-216">In that case, the value is not null; it's just been explicitly set to a string of characters whose length is zero.</span></span> <span data-ttu-id="ac7c9-217">다음 두 문은 차이 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-217">These two statements show the difference:</span></span>
> 
> [!code-csharp[Main](entering-data/samples/sample6.cs)]
> 
> <span data-ttu-id="ac7c9-218">이보다 더 복잡 약간 하지만 중요 한 점은 `null` 결정 되지 않은 상태로의 종류를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-218">It's a little more complicated than that, but the important point is that `null` represents a sort of undetermined state.</span></span>
> 
> <span data-ttu-id="ac7c9-219">값이 null 및 빈 문자열이 방금 때 정확히 이해 해야 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-219">Now and then it's important to understand exactly when a value is null and when it's just an empty string.</span></span> <span data-ttu-id="ac7c9-220">에 대 한 코드에는 *AddMovie* 를 사용 하 여 텍스트 상자의 값을 가져오기 페이지 `Request.Form["title"]` 등입니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-220">In the code for the *AddMovie* page, you get the values of the text boxes by using `Request.Form["title"]` and so on.</span></span> <span data-ttu-id="ac7c9-221">값 때 페이지를 처음 실행할 (단추를 클릭) 전에 `Request.Form["title"]` null입니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-221">When the page first runs (before you click the button), the value of `Request.Form["title"]` is null.</span></span> <span data-ttu-id="ac7c9-222">폼을 제출 하면 하지만 `Request.Form["title"]` 의 값을 가져옵니다는 `title` 입력란.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-222">But when you submit the form, `Request.Form["title"]` gets the value of the `title` text box.</span></span> <span data-ttu-id="ac7c9-223">확실 하지는 않지만 빈 입력란; null이 아닌 방금를 빈 문자열을 받았습니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-223">It's not obvious, but an empty text box is not null; it just has an empty string in it.</span></span> <span data-ttu-id="ac7c9-224">따라서 단추에 대 한 응답에서 코드를 실행할 때 클릭, `Request.Form["title"]` 에 빈 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-224">So when the code runs in response to the button click, `Request.Form["title"]` has an empty string in it.</span></span>
> 
> <span data-ttu-id="ac7c9-225">이러한 차이점으로이 인해 중요 한 이유는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="ac7c9-225">Why is this distinction important?</span></span> <span data-ttu-id="ac7c9-226">만들 때의 *동영상* 테이블을 명시적으로 라고 하는 필드는 null 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-226">When you created the *Movies* table, you explicitly said that none of the fields could be null.</span></span> <span data-ttu-id="ac7c9-227">새 동영상에 대 한 항목 양식이 있는 여기 있고 있습니다 하는 필드를 비워 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-227">But here you have an entry form for new movies, and you're leaving fields blank.</span></span> <span data-ttu-id="ac7c9-228">장르 또는 연도 대 한 값이 없는 새 동영상을 저장 하려고 할 때 불만을 제기 데이터베이스 합리적인 기대 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-228">You would reasonably expect the database to complain when you tried to save new movies that didn't have values for genre or year.</span></span> <span data-ttu-id="ac7c9-229">내용이 충분 하지만 &mdash; 는 값이 null 않은 텍스트 상자를 비워 두면 하는 경우에로 빈 문자열을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-229">But that's the point &mdash; even if you leave those text boxes blank, the values aren't null; they're empty strings.</span></span> <span data-ttu-id="ac7c9-230">새 동영상 빈 이러한 열이 있는 데이터베이스에 저장할 수는 결과적으로, &mdash; 있지만 null이 아님!</span><span class="sxs-lookup"><span data-stu-id="ac7c9-230">As a result, you're able to save new movies to the database with these columns empty &mdash; but not null!</span></span> <span data-ttu-id="ac7c9-231">&mdash; 값</span><span class="sxs-lookup"><span data-stu-id="ac7c9-231">&mdash; values.</span></span> <span data-ttu-id="ac7c9-232">따라서 사용자가 사용자의 입력을 확인 하 여 수행할 수 있는 빈 문자열을 제출 하지 않으면 있는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-232">Therefore, you have to make sure that users don't submit an empty string, which you can do by validating the user's input.</span></span>


### <a name="the-validation-helper"></a><span data-ttu-id="ac7c9-233">유효성 검사 도우미</span><span class="sxs-lookup"><span data-stu-id="ac7c9-233">The Validation Helper</span></span>

<span data-ttu-id="ac7c9-234">도우미 메서드를 포함 하는 ASP.NET 웹 페이지 &mdash; 는 `Validation` 도우미 &mdash; 사용자가 입력 요구 사항을 충족 하는 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-234">ASP.NET Web Pages includes a helper &mdash; the `Validation` helper &mdash; that you can use to make sure that users enter data that meets your requirements.</span></span> <span data-ttu-id="ac7c9-235">`Validation` 도우미에 기본 제공 되 ASP.NET 웹 페이지를 하므로 이전 자습서에서 Gravatar 도우미를 설치 하는 방법을 NuGet을 사용 하 여 패키지도 설치할 필요가 없습니다 도우미 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-235">The `Validation` helper is one of the helpers that's built in to ASP.NET Web Pages, so you don't have to install it as a package by using NuGet, the way you installed the Gravatar helper in an earlier tutorial.</span></span>

<span data-ttu-id="ac7c9-236">사용자 입력의 유효성을 검사 하려면 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-236">To validate the user's input, you'll do the following:</span></span>

- <span data-ttu-id="ac7c9-237">코드를 사용 하 여 페이지에 텍스트 상자에 필요한 값이 되도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-237">Use code to specify that you want to require values in the text boxes on the page.</span></span>
- <span data-ttu-id="ac7c9-238">모든 항목이 제대로 확인 하는 경우에 데이터베이스에 동영상 정보를 추가 하는 테스트 코드에 들어가는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-238">Put a test into the code so that the movie information is added to the database only if everything validates properly.</span></span>
- <span data-ttu-id="ac7c9-239">오류 메시지를 표시 하는 태그에 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-239">Add code into the markup to display error messages.</span></span>

<span data-ttu-id="ac7c9-240">에 있는 코드 블록에는 *AddMovie* 페이지에서 오른쪽 위 위쪽 변수 선언 앞에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-240">In the code block in the *AddMovie* page, right up at the top before the variable declarations, add the following code:</span></span>

[!code-csharp[Main](entering-data/samples/sample7.cs)]

<span data-ttu-id="ac7c9-241">호출 하면 `Validation.RequireField` 각 필드에 대해 한 번씩 (`<input>` 요소)는 입력을 요구 하려면.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-241">You call `Validation.RequireField` once for each field (`<input>` element) where you want to require an entry.</span></span> <span data-ttu-id="ac7c9-242">여기에서 보는 것 처럼 각 호출에 대 한 사용자 지정 오류 메시지를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-242">You can also add a custom error message for each call, like you see here.</span></span> <span data-ttu-id="ac7c9-243">(여기서 다양 한 메시지 수를 두는 원하는 있습니다 보여 주기 위해 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="ac7c9-243">(We varied the messages just to show that you can put anything you like there.)</span></span>

<span data-ttu-id="ac7c9-244">문제가 있는 경우 새 동영상 정보가 데이터베이스에 삽입 되지 않도록 하려면.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-244">If there's a problem, you want to prevent the new movie information from being inserted into the database.</span></span> <span data-ttu-id="ac7c9-245">에 `if(IsPost)` 블록을 사용 하 여 `&&` 테스트 하는 다른 조건을 추가 하려면 (논리적 AND) `Validation.IsValid()`합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-245">In the `if(IsPost)` block, use `&&` (logical AND) to add another condition that tests `Validation.IsValid()`.</span></span> <span data-ttu-id="ac7c9-246">완료 하면, 전체 `if(IsPost)` 블록이이 코드와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-246">When you're done, the whole `if(IsPost)` block looks like this code:</span></span>

[!code-csharp[Main](entering-data/samples/sample8.cs)]

<span data-ttu-id="ac7c9-247">사용 하 여 등록 하는 필드를 사용 하 여 유효성 검사 오류가 있는 경우는 `Validation` 도우미에는 `Validation.IsValid` 메서드에서 false를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-247">If there's a validation error with any of the fields that you registered by using the `Validation` helper, the `Validation.IsValid` method returns false.</span></span> <span data-ttu-id="ac7c9-248">및이 경우 해당 블록의 코드 중를 실행 하므로 잘못 된 동영상 항목이 없습니다. 데이터베이스에 삽입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-248">And in that case, none of the code in that block will run, so no invalid movie entries will be inserted into the database.</span></span> <span data-ttu-id="ac7c9-249">에 하지 리디렉션 됨 물론 및는 *동영상* 페이지.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-249">And of course you're not redirected to the *Movies* page.</span></span>

<span data-ttu-id="ac7c9-250">이제 유효성 검사 코드를 포함 한 전체 코드 블록을이 예제에서와 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-250">The complete code block, including the validation code, now looks like this example:</span></span>

[!code-cshtml[Main](entering-data/samples/sample9.cshtml?highlight=10)]

## <a name="displaying-validation-errors"></a><span data-ttu-id="ac7c9-251">유효성 검사 오류 표시</span><span class="sxs-lookup"><span data-stu-id="ac7c9-251">Displaying Validation Errors</span></span>

<span data-ttu-id="ac7c9-252">오류 메시지를 표시 하는 마지막 단계가입니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-252">The last step is to display any error messages.</span></span> <span data-ttu-id="ac7c9-253">각 유효성 검사 오류에 대 한 개별 메시지를 나타내거나, 요약 또는 둘 모두를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-253">You can display individual messages for each validation error, or you can display a summary, or both.</span></span> <span data-ttu-id="ac7c9-254">이 자습서에서 수행 합니다 둘 다 어떻게 작동 하는지 확인할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-254">For this tutorial, you'll do both so that you can see how it works.</span></span>

<span data-ttu-id="ac7c9-255">각 옆에 있는 `<input>` 유효성을 검사 하는 요소, 호출의 `Html.ValidationMessage` 메서드의 이름을 전달 하 고는 `<input>` 유효성을 검사 하는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-255">Next to each `<input>` element that you're validating, call the `Html.ValidationMessage` method and pass it the name of the `<input>` element you're validating.</span></span> <span data-ttu-id="ac7c9-256">배치는 `Html.ValidationMessage` 오류 메시지를 표시 하려는 메서드를 오른쪽입니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-256">You put the `Html.ValidationMessage` method right where you want the error message to appear.</span></span> <span data-ttu-id="ac7c9-257">페이지 실행 하는 경우, `Html.ValidationMessage` 메서드 렌더링은 `<span>` 요소 유효성 검사 오류가 이동 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-257">When the page runs, the `Html.ValidationMessage` method renders a `<span>` element where the validation error will go.</span></span> <span data-ttu-id="ac7c9-258">(오류가 없는 경우는 `<span>` 요소가 렌더링 하지만에 텍스트가 없습니다.)</span><span class="sxs-lookup"><span data-stu-id="ac7c9-258">(If there's no error, the `<span>` element is rendered, but there's no text in it.)</span></span>

<span data-ttu-id="ac7c9-259">포함 되도록 페이지의 태그를 변경는 `Html.ValidationMessage` 세 개의 각 방법을 `<input>` 이 예제에서와 같이 요소 페이지에서:</span><span class="sxs-lookup"><span data-stu-id="ac7c9-259">Change the markup in the page so that it includes an `Html.ValidationMessage` method for each of the three `<input>` elements on the page, like this example:</span></span>

[!code-cshtml[Main](entering-data/samples/sample10.cshtml?highlight=3,8,13)]

<span data-ttu-id="ac7c9-260">요약 작동 하는 방법을 보려면, 또한 다음 태그를 추가 및 코드 바로 뒤의 `<h1>Add a Movie</h1>` 페이지에서 요소:</span><span class="sxs-lookup"><span data-stu-id="ac7c9-260">To see how the summary works, also add the following markup and code right after the `<h1>Add a Movie</h1>` element on the page:</span></span>

[!code-cshtml[Main](entering-data/samples/sample11.cshtml)]

<span data-ttu-id="ac7c9-261">기본적으로는 `Html.ValidationSummary` 메서드 목록에 모든 유효성 검사 메시지를 표시 합니다 (한 `<ul>` 내에 있는 요소는 `<div>` 요소).</span><span class="sxs-lookup"><span data-stu-id="ac7c9-261">By default, the `Html.ValidationSummary` method displays all the validation messages in a list (a `<ul>` element that's inside a `<div>` element).</span></span> <span data-ttu-id="ac7c9-262">과 마찬가지로 `Html.ValidationMessage` 메서드를 유효성 검사 요약에 대 한 태그는 항상 렌더링; 오류가 경우 목록 항목이 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-262">As with the `Html.ValidationMessage` method, the markup for the validation summary is always rendered; if there are no errors, no list items are rendered.</span></span>

<span data-ttu-id="ac7c9-263">요약을 사용 하 여 대신 유효성 검사 메시지를 표시 하는 다른 방법으로 일 수 있습니다는 `Html.ValidationMessage` 메서드를 각 필드 관련 오류를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-263">The summary can be an alternative way to display validation messages instead of by using the `Html.ValidationMessage` method to display each field-specific error.</span></span> <span data-ttu-id="ac7c9-264">또는 요약 및 세부 정보를 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-264">Or you can use both a summary and the details.</span></span> <span data-ttu-id="ac7c9-265">또는 사용할 수 있습니다는 `Html.ValidationSummary` 메서드를 일반 오류를 표시 한 다음 개별 사용 하 여 `Html.ValidationMessage` 호출 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-265">Or you can use the `Html.ValidationSummary` method to display a generic error and then use individual `Html.ValidationMessage` calls to display details.</span></span>

<span data-ttu-id="ac7c9-266">이제 완료 페이지이 예제에서와 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-266">The complete page now looks like this example:</span></span>

[!code-cshtml[Main](entering-data/samples/sample12.cshtml)]

<span data-ttu-id="ac7c9-267">이제</span><span class="sxs-lookup"><span data-stu-id="ac7c9-267">That's it.</span></span> <span data-ttu-id="ac7c9-268">이제 필드 중 하나 이상 그대로 동영상을 추가 하 여 페이지를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-268">You can now test the page by adding a movie but leaving out one or more of the fields.</span></span> <span data-ttu-id="ac7c9-269">이렇게 하면 다음과 같은 오류가 표시 참조:</span><span class="sxs-lookup"><span data-stu-id="ac7c9-269">When you do, you see the following error display:</span></span>

![유효성 검사 오류 메시지를 보여 주는 동영상 페이지 추가](entering-data/_static/image5.png)

## <a name="styling-the-validation-error-messages"></a><span data-ttu-id="ac7c9-271">유효성 검사 오류 메시지의 스타일 지정</span><span class="sxs-lookup"><span data-stu-id="ac7c9-271">Styling the Validation Error Messages</span></span>

<span data-ttu-id="ac7c9-272">오류 메시지, 있지만 하지 실제로 서식을 상태일 때 잘 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-272">You can see that there are error messages, but they don't really stand out very well.</span></span> <span data-ttu-id="ac7c9-273">그러나 오류 메시지, 스타일을 지정 하는 쉬운 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-273">There's an easy way to style the error messages, though.</span></span>

<span data-ttu-id="ac7c9-274">개별 오류 메시지에 표시 되는 스타일을 지정 하려면 `Html.ValidationMessage`, 이라는 CSS 스타일 클래스를 만들 `field-validation-error`합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-274">To style the individual error messages that are displayed by `Html.ValidationMessage`, create a CSS style class named `field-validation-error`.</span></span> <span data-ttu-id="ac7c9-275">유효성 검사 요약에 대 한 보기를 정의 하려면 이라는 CSS 스타일 클래스를 만들 `validation-summary-errors`합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-275">To define the look for the validation summary, create a CSS style class named `validation-summary-errors`.</span></span>

<span data-ttu-id="ac7c9-276">이 기술은 작동 방식을 보려면 추가 `<style>` 요소 안에 `<head>` 페이지의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-276">To see how this technique works, add a `<style>` element inside the `<head>` section of the page.</span></span> <span data-ttu-id="ac7c9-277">그런 다음 명명 된 스타일 클래스를 정의 `field-validation-error` 및 `validation-summary-errors` 다음 규칙을 포함 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-277">Then define style classes named `field-validation-error` and `validation-summary-errors` that contain the following rules:</span></span>

[!code-cshtml[Main](entering-data/samples/sample13.cshtml?highlight=4-17)]

<span data-ttu-id="ac7c9-278">일반적으로 추가할 수 있습니다를 별도의 스타일 정보 *.css* 파일인 편의상 배치할 수 있는 페이지에 지금은 하지만 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-278">Normally you'd probably put style information into a separate *.css* file, but for simplicity you can put them in the page for now.</span></span> <span data-ttu-id="ac7c9-279">(이 자습서 집합의 뒷부분에 나오는 이동 CSS 규칙은 별도의 *.css* 파일입니다.)</span><span class="sxs-lookup"><span data-stu-id="ac7c9-279">(Later in this tutorial set, you'll move the CSS rules to a separate *.css* file.)</span></span>

<span data-ttu-id="ac7c9-280">유효성 검사 오류가 있는 경우는 `Html.ValidationMessage` 메서드 렌더링 되는 `<span>` 포함 된 요소 `class="field-validation-error"`합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-280">If there's a validation error, the `Html.ValidationMessage` method renders a `<span>` element that includes `class="field-validation-error"`.</span></span> <span data-ttu-id="ac7c9-281">해당 클래스에 대 한 스타일 정의 추가 하 여 메시지 모양을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-281">By adding a style definition for that class, you can configure what the message looks like.</span></span> <span data-ttu-id="ac7c9-282">오류가 있는 경우는 `ValidationSummary` 메서드 특성을 동적으로 마찬가지로 렌더링 `class="validation-summary-errors"`합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-282">If there are errors, the `ValidationSummary` method likewise dynamically renders the attribute `class="validation-summary-errors"`.</span></span>

<span data-ttu-id="ac7c9-283">페이지를 다시 실행 하 고 필드의 두 의도적으로 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-283">Run the page again and deliberately leave out a couple of the fields.</span></span> <span data-ttu-id="ac7c9-284">오류 정보에서 더욱 분명 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-284">The errors are now more noticeable.</span></span> <span data-ttu-id="ac7c9-285">(실제로 이러한 overdone 하는, 수 있지만 수행할 수 있는 작업을 보여 주기 위해.)</span><span class="sxs-lookup"><span data-stu-id="ac7c9-285">(In fact, they're overdone, but that's just to show what you can do.)</span></span>

![스타일을 지정 하는 유효성 검사 오류를 보여 주는 동영상 페이지 추가](entering-data/_static/image6.png)

## <a name="adding-a-link-to-the-movies-page"></a><span data-ttu-id="ac7c9-287">동영상 페이지의 링크를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-287">Adding a Link to the Movies Page</span></span>

<span data-ttu-id="ac7c9-288">하나의 마지막 단계를 편리 하 게 하는 *AddMovie* 원래 영화 목록에서 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-288">One final step is to make it convenient to get to the *AddMovie* page from the original movie listing.</span></span>

<span data-ttu-id="ac7c9-289">열기는 *동영상* 페이지를 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-289">Open the *Movies* page again.</span></span> <span data-ttu-id="ac7c9-290">닫은 후 `</div>` 태그 뒤에 오는 `WebGrid` 도우미에 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-290">After the closing `</div>` tag that follows the `WebGrid` helper, add the following markup:</span></span>

[!code-cshtml[Main](entering-data/samples/sample14.cshtml)]

<span data-ttu-id="ac7c9-291">ASP.NET을 해석 하기 전에 본 것 처럼는 `~` 연산자는 웹 사이트의 루트 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-291">As you saw before, ASP.NET interprets the `~` operator as the root of the website.</span></span> <span data-ttu-id="ac7c9-292">사용할 필요가 없습니다는 `~` 연산자;는 태그를 사용할 수 있습니다 `<a href="./AddMovie">Add a movie</a>` 또는 HTML 이해할 수 있는 경로 정의 하는 다른 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-292">You don't have to use the `~` operator; you could use the markup `<a href="./AddMovie">Add a movie</a>` or some other way to define the path that HTML understands.</span></span> <span data-ttu-id="ac7c9-293">하지만 `~` 연산자는 일반적인 접근 방식이 효과적 Razor 페이지에 대 한 링크를 만들 때 사이트를 보다 유연한 만들므로-하위 폴더에 현재 페이지를 이동 하는 경우 링크가 여전히 들어가는지는 *AddMovie* 페이지.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-293">But the `~` operator is a good general approach when you create links for Razor pages, because it makes the site more flexible — if you move the current page to a subfolder, the link will still go to the *AddMovie* page.</span></span> <span data-ttu-id="ac7c9-294">(에 유의 해야는 `~` 연산자만 작동 *.cshtml* 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-294">(Remember that the `~` operator only works in *.cshtml* pages.</span></span> <span data-ttu-id="ac7c9-295">ASP.NET에 대 한 이해를 있지만 표준 HTML 아닙니다.)</span><span class="sxs-lookup"><span data-stu-id="ac7c9-295">ASP.NET understands it, but it's not standard HTML.)</span></span>

<span data-ttu-id="ac7c9-296">완료 되 면 실행는 *동영상* 페이지.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-296">When you're done, run the *Movies* page.</span></span> <span data-ttu-id="ac7c9-297">이이 페이지와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-297">It will look like this page:</span></span>

![동영상 추가 ' 페이지에는 링크가 포함 된 동영상 페이지](entering-data/_static/image7.png)

<span data-ttu-id="ac7c9-299">클릭는 **동영상 추가** 이동 하는지 확인 하는 링크는 *AddMovie* 페이지.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-299">Click the **Add a movie** link to make sure that it goes to the *AddMovie* page.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="ac7c9-300">다음에 나오는</span><span class="sxs-lookup"><span data-stu-id="ac7c9-300">Coming Up Next</span></span>

<span data-ttu-id="ac7c9-301">다음 자습서에서는 사용자가 데이터베이스에 이미 있는 데이터를 편집할 수 있도록 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-301">In the next tutorial, you'll learn how to let users edit data that's already in the database.</span></span>

## <a name="complete-listing-for-addmovie-page"></a><span data-ttu-id="ac7c9-302">AddMovie 페이지에 대 한 전체 목록을 보려면</span><span class="sxs-lookup"><span data-stu-id="ac7c9-302">Complete Listing for AddMovie Page</span></span>

[!code-cshtml[Main](entering-data/samples/sample15.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="ac7c9-303">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="ac7c9-303">Additional Resources</span></span>

- [<span data-ttu-id="ac7c9-304">Razor 구문을 사용 하 여 ASP.NET 웹 프로그래밍 소개</span><span class="sxs-lookup"><span data-stu-id="ac7c9-304">Introduction to ASP.NET Web Programming Using the Razor Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkID=202890)
- <span data-ttu-id="ac7c9-305">[INTO 문을 SQL 삽입](http://www.w3schools.com/sql/sql_insert.asp) W3Schools 사이트</span><span class="sxs-lookup"><span data-stu-id="ac7c9-305">[SQL INSERT INTO Statement](http://www.w3schools.com/sql/sql_insert.asp) on the W3Schools site</span></span>
- <span data-ttu-id="ac7c9-306">[사이트 페이지에서 ASP.NET 웹 사용자 입력 유효성 검사](https://go.microsoft.com/fwlink/?LinkId=253002)합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-306">[Validating User Input in ASP.NET Web Pages Sites](https://go.microsoft.com/fwlink/?LinkId=253002).</span></span> <span data-ttu-id="ac7c9-307">작업에 대 한 자세한 정보는 `Validation` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="ac7c9-307">More information about working with the `Validation` helper.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="ac7c9-308">[이전](form-basics.md)
[다음](updating-data.md)</span><span class="sxs-lookup"><span data-stu-id="ac7c9-308">[Previous](form-basics.md)
[Next](updating-data.md)</span></span>
