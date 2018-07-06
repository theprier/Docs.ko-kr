---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper
title: ASP.NET MVC DropDownList 도우미를 스 캐 폴딩 하는 방법을 검사 | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: aspnetcontent
ms.date: 01/12/2012
ms.assetid: 8921d7f2-21f0-427a-8b27-2df7251174b0
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper
msc.type: authoredcontent
ms.openlocfilehash: 8e407d5426ed93388b3c6f7bdb125be5356c002c
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37837132"
---
<a name="examining--how--aspnet-mvc-scaffolds-the-dropdownlist-helper"></a><span data-ttu-id="bba9f-102">ASP.NET MVC DropDownList 도우미를 스 캐 폴딩 하는 방법 검사</span><span class="sxs-lookup"><span data-stu-id="bba9f-102">Examining  how  ASP.NET MVC scaffolds the DropDownList Helper</span></span>
====================
<span data-ttu-id="bba9f-103">[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="bba9f-103">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

<span data-ttu-id="bba9f-104">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 *컨트롤러* 폴더를 선택 하 고 **컨트롤러 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-104">In **Solution Explorer**, right-click the *Controllers* folder and then select **Add Controller**.</span></span> <span data-ttu-id="bba9f-105">컨트롤러 이름을 **StoreManagerController**합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-105">Name the controller **StoreManagerController**.</span></span> <span data-ttu-id="bba9f-106">에 대 한 옵션을 설정 합니다 **컨트롤러 추가** 아래 그림과에서 같이 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="bba9f-106">Set the options for the **Add Controller** dialog as shown in the image below.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image1.png)

<span data-ttu-id="bba9f-107">편집 된 *StoreManager\Index.cshtml* 하 고 제거 `AlbumArtUrl`합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-107">Edit the *StoreManager\Index.cshtml* view and remove `AlbumArtUrl`.</span></span> <span data-ttu-id="bba9f-108">제거 `AlbumArtUrl` 프레젠테이션 가독성을 향상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-108">Removing `AlbumArtUrl` will make the presentation more readable.</span></span> <span data-ttu-id="bba9f-109">완성된 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-109">The completed code is shown below.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample1.cshtml)]

<span data-ttu-id="bba9f-110">엽니다는 *Controllers\StoreManagerController.cs* 파일을 찾을 `Index` 메서드.</span><span class="sxs-lookup"><span data-stu-id="bba9f-110">Open the *Controllers\StoreManagerController.cs* file and find the `Index` method.</span></span> <span data-ttu-id="bba9f-111">추가 된 `OrderBy` 절을 변경 앨범 가격에 따라 정렬 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-111">Add the `OrderBy` clause so the albums will be sorted by price.</span></span> <span data-ttu-id="bba9f-112">전체 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-112">The complete code is shown below.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample2.cs)]

<span data-ttu-id="bba9f-113">가격으로 정렬 됩니다 쉽게 데이터베이스에 변경 내용을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-113">Sorting by price will make it easier to test changes to the database.</span></span> <span data-ttu-id="bba9f-114">메서드를 만들고 편집을 테스트 하는 경우 저장된 된 데이터는 첫 번째 나타납니다 낮은 가격을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-114">When you are testing the edit and create methods, you can use a low price so the saved data will appear first.</span></span>

<span data-ttu-id="bba9f-115">엽니다는 *StoreManager\Edit.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-115">Open the *StoreManager\Edit.cshtml* file.</span></span> <span data-ttu-id="bba9f-116">범례 태그 바로 뒤에 다음 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-116">Add the following line just after the legend tag.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample3.cshtml)]

<span data-ttu-id="bba9f-117">다음 코드에서는이 변경의 컨텍스트를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-117">The following code shows the context of this change:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample4.cshtml)]

<span data-ttu-id="bba9f-118">`AlbumId` 앨범 레코드를 변경 하려면 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-118">The `AlbumId` is required to make changes to an album record.</span></span>

<span data-ttu-id="bba9f-119">Ctrl+F5를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-119">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="bba9f-120">선택 합니다 **관리자** 링크를 클릭 합니다 **새로 만들기** 앨범에 연결할.</span><span class="sxs-lookup"><span data-stu-id="bba9f-120">Select to the **Admin** link, then select the **Create New** link to create a new album.</span></span> <span data-ttu-id="bba9f-121">앨범 정보 저장을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-121">Verify the album information was saved.</span></span> <span data-ttu-id="bba9f-122">앨범을 편집 하 고 변경 내용을 유지 됩니다 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-122">Edit an album and verify the changes you made are persisted.</span></span>

### <a name="the-album-schema"></a><span data-ttu-id="bba9f-123">앨범 스키마</span><span class="sxs-lookup"><span data-stu-id="bba9f-123">The Album Schema</span></span>

<span data-ttu-id="bba9f-124">`StoreManager` MVC 스 캐 폴딩 메커니즘을 통해 만든 컨트롤러 music store 데이터베이스를 참여 앨범 CRUD (만들기, 읽기, 업데이트, 삭제) 액세스를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-124">The `StoreManager` controller created by the MVC scaffolding mechanism allows CRUD (Create, Read, Update, Delete) access to the albums in the music store database.</span></span> <span data-ttu-id="bba9f-125">앨범 정보에 대 한 스키마는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-125">The schema for album information is shown below:</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image2.png)

<span data-ttu-id="bba9f-126">합니다 `Albums` 앨범 장르 및 설명 테이블 저장 하지 않습니다, 외래 키를 저장 합니다 `Genres` 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-126">The `Albums` table does not store the album genre and description, it stores a foreign key to the `Genres` table.</span></span> <span data-ttu-id="bba9f-127">`Genres` 테이블 장르 이름 및 설명을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-127">The `Genres` table contains the genre name and description.</span></span> <span data-ttu-id="bba9f-128">마찬가지로 합니다 `Albums` 테이블은 앨범 artist 이름은 같지만 외래 키를 포함 하지 않습니다는 `Artists` 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-128">Likewise, the `Albums` table doesn't contain the album artists name, but a foreign key to the `Artists` table.</span></span> <span data-ttu-id="bba9f-129">`Artists` 테이블 artist's 이름을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-129">The `Artists` table contains the artist's name.</span></span> <span data-ttu-id="bba9f-130">데이터를 검사 하는 경우는 `Albums` 테이블에 외래 키를 포함 하는 각 행을 볼 수 있습니다 합니다 `Genres` 테이블과 외래 키를를 `Artists` 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-130">If you examine the data in the `Albums` table, you can see each row contains a foreign key to the `Genres` table and a foreign key to the `Artists` table.</span></span> <span data-ttu-id="bba9f-131">아래 이미지에서 일부 테이블 데이터를 표시 합니다 `Albums` 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-131">The image below show some table data from the `Albums` table.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image3.png)

### <a name="the-html-select-tag"></a><span data-ttu-id="bba9f-132">HTML 태그</span><span class="sxs-lookup"><span data-stu-id="bba9f-132">The HTML Select Tag</span></span>

<span data-ttu-id="bba9f-133">HTML `<select>` 요소 (HTML에서 만든 [DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) 도우미) 값 (예: 장르 목록)의 전체 목록을 표시 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-133">The HTML `<select>` element (created by the HTML [DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) helper) is used to display a complete list of values (such as the list of genres).</span></span> <span data-ttu-id="bba9f-134">폼 편집에 대 한 select 목록에 현재 값을 확인 하면 현재 값을를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-134">For edit forms, when the current value is known, the select list can display the current value.</span></span> <span data-ttu-id="bba9f-135">본 것이 이전에 선택한 값을 설정 했습니다 **코미디**합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-135">We saw this previously when we set the selected value to **Comedy**.</span></span> <span data-ttu-id="bba9f-136">Select 목록 범주 또는 외래 키 데이터를 표시 하거나 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-136">The select list is ideal for displaying category or foreign key data.</span></span> <span data-ttu-id="bba9f-137">`<select>` 장르 외래 키에 대 한 요소 표시 가능한 장르 이름 목록을 하지만 장르 속성이 장르 외래 키 값을 표시 하는 장르 이름이 아니라으로 업데이트 됩니다 폼을 저장 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="bba9f-137">The `<select>` element for the Genre foreign key displays the list of possible genre names, but when you save the form the Genre property is updated with the Genre foreign key value, not the displayed genre name.</span></span> <span data-ttu-id="bba9f-138">아래 이미지에서는 선택한 장르 됩니다 **Disco** 음악가 이며 **Donna 여름**합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-138">In the image below, the genre selected is **Disco** and the artist is **Donna Summer**.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image4.png)

### <a name="examining-the-aspnet-mvc-scaffolded-code"></a><span data-ttu-id="bba9f-139">코드 스 캐 폴드 된 ASP.NET MVC를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-139">Examining the ASP.NET MVC Scaffolded Code</span></span>

<span data-ttu-id="bba9f-140">엽니다는 *Controllers\StoreManagerController.cs* 파일을 찾을 `HTTP GET Create` 메서드.</span><span class="sxs-lookup"><span data-stu-id="bba9f-140">Open the *Controllers\StoreManagerController.cs* file and find the `HTTP GET Create` method.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample5.cs)]

<span data-ttu-id="bba9f-141">`Create` 메서드 두 개를 더한 [SelectList](https://msdn.microsoft.com/library/system.web.mvc.selectlist.aspx) 개체를 `ViewBag`, artist 정보를 포함 하도록 여러 개 있는 장르 정보를 포함 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-141">The `Create` method adds two [SelectList](https://msdn.microsoft.com/library/system.web.mvc.selectlist.aspx) objects to the `ViewBag`, one to contain the genre information, and one to contain the artist information.</span></span> <span data-ttu-id="bba9f-142">합니다 [SelectList](https://msdn.microsoft.com/library/dd505286.aspx) 위에서 사용 하는 생성자 오버 로드는 세 가지 인수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-142">The [SelectList](https://msdn.microsoft.com/library/dd505286.aspx) constructor overload used above takes three arguments:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample6.cs)]

1. <span data-ttu-id="bba9f-143">*항목*:를 [IEnumerable](https://msdn.microsoft.com/library/system.collections.ienumerable.aspx) 목록의 항목을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-143">*items*: An [IEnumerable](https://msdn.microsoft.com/library/system.collections.ienumerable.aspx) containing the items in the list.</span></span> <span data-ttu-id="bba9f-144">장르 목록을 반환한 위의 예에서 `db.Genres`합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-144">In the example above, the list of genres returned by `db.Genres`.</span></span>
2. <span data-ttu-id="bba9f-145">*dataValueField*: 속성의 이름을 합니다 **IEnumerable** 키 값이 포함 된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-145">*dataValueField*: The name of the property in the **IEnumerable** list that contains the key value.</span></span> <span data-ttu-id="bba9f-146">위의 예에서 `GenreId` 고 `ArtistId`입니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-146">In the example above, `GenreId` and `ArtistId`.</span></span>
3. <span data-ttu-id="bba9f-147">*dataTextField*: 속성의 이름을 합니다 **IEnumerable** 표시할 정보를 포함 하는 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-147">*dataTextField*: The name of the property in the **IEnumerable** list that contains the information to display.</span></span> <span data-ttu-id="bba9f-148">음악가 장르 테이블에는 `name` 필드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-148">In both the artists and genre table, the `name` field is used.</span></span>

<span data-ttu-id="bba9f-149">열기는 *Views\StoreManager\Create.cshtml* 파일을 검사 합니다 `Html.DropDownList` genre 필드에 대 한 도우미 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-149">Open the *Views\StoreManager\Create.cshtml* file and examine the `Html.DropDownList` helper markup for the genre field.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample7.cshtml)]

<span data-ttu-id="bba9f-150">만들기 뷰는 첫 번째 줄에는 표시를 `Album` 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-150">The first line shows that the create view takes an `Album` model.</span></span> <span data-ttu-id="bba9f-151">에 `Create` 위에 표시 된 모델이 전달 된 뷰에 하므로 메서드는 **null** `Album` 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-151">In the `Create` method shown above, no model was passed, so the view gets a **null** `Album` model.</span></span> <span data-ttu-id="bba9f-152">이 시점에 만들기 새 앨범이 때문 모든 없었습니다 `Album` 에 대 한 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-152">At this point we are creating a new album so we don't have any `Album` data for it.</span></span>

<span data-ttu-id="bba9f-153">합니다 [Html.DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) 위에 표시 된 오버 로드를 모델로 바인딩할 필드의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-153">The [Html.DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) overload shown above takes the name of the field to bind to the model.</span></span> <span data-ttu-id="bba9f-154">또한 사용 하 여이 이름에 대 한 확인을 **ViewBag** 개체를 포함 하는 [SelectList](https://msdn.microsoft.com/library/dd505286.aspx) 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-154">It also uses this name to look for a **ViewBag** object containing a [SelectList](https://msdn.microsoft.com/library/dd505286.aspx) object.</span></span> <span data-ttu-id="bba9f-155">이 오버 로드를 사용 해야 하는 이름 합니다 **ViewBag SelectList** 개체 `GenreId`합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-155">Using this overload, you are required to name the **ViewBag SelectList** object `GenreId`.</span></span> <span data-ttu-id="bba9f-156">두 번째 매개 변수 (`String.Empty`) 없는 항목이 선택 될 때 표시할 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-156">The second parameter (`String.Empty`) is the text to display when no item is selected.</span></span> <span data-ttu-id="bba9f-157">이것이 우리가 원하는 새 앨범이 만들 때입니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-157">This is exactly what we want when creating a new album.</span></span> <span data-ttu-id="bba9f-158">두 번째 매개 변수를 제거 하 고 다음 코드를 사용:</span><span class="sxs-lookup"><span data-stu-id="bba9f-158">If you removed the second parameter and used the following code:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample8.cshtml)]

<span data-ttu-id="bba9f-159">Select 목록에는 샘플에서 기본적으로 첫 번째 요소 또는 Rock 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-159">The select list would default to the first element, or Rock in our sample.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image5.png)

<span data-ttu-id="bba9f-160">검사는 `HTTP POST Create` 메서드.</span><span class="sxs-lookup"><span data-stu-id="bba9f-160">Examining the `HTTP POST Create` method.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample9.cs)]

<span data-ttu-id="bba9f-161">이 오버 로드는 `Create` 메서드는 `album` 게시 된 양식 값에서 ASP.NET MVC 모델 바인딩 시스템에서 만든 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-161">This overload of the `Create` method takes an `album` object, created by the ASP.NET MVC model binding system from the form values posted.</span></span> <span data-ttu-id="bba9f-162">모델 상태가 유효 하 고 데이터베이스 오류가 없는 경우 새 앨범을 제출 하면 새 앨범에 데이터베이스를 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-162">When you submit a new album, if model state is valid and there are no database errors, the new album is added the database.</span></span> <span data-ttu-id="bba9f-163">다음 이미지는 새 앨범이 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-163">The following image shows the creation of a new album.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image6.png)

<span data-ttu-id="bba9f-164">사용할 수는 [fiddler 도구](http://www.fiddler2.com/fiddler2/) 게시 된 양식 값을 검사할 앨범 개체를 만드는 ASP.NET MVC 모델 바인딩에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-164">You can use the [fiddler tool](http://www.fiddler2.com/fiddler2/) to examine the posted form values that ASP.NET MVC model binding uses to create the album object.</span></span>

<span data-ttu-id="bba9f-165">![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image7.png).</span><span class="sxs-lookup"><span data-stu-id="bba9f-165">![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image7.png).</span></span>

### <a name="refactoring-the-viewbag-selectlist-creation"></a><span data-ttu-id="bba9f-166">ViewBag SelectList 생성 리팩터링</span><span class="sxs-lookup"><span data-stu-id="bba9f-166">Refactoring the ViewBag SelectList Creation</span></span>

<span data-ttu-id="bba9f-167">모두를 `Edit` 메서드 및 `HTTP POST Create` 메서드는 동일한 코드를 설정 하는 **SelectList** 에 **ViewBag**합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-167">Both the `Edit` methods and the `HTTP POST Create` method have identical code to set up the **SelectList** in the **ViewBag**.</span></span> <span data-ttu-id="bba9f-168">티에서 [DRY](http://en.wikipedia.org/wiki/Don't_repeat_yourself),이 코드 리팩터링 했습니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-168">In the spirit of [DRY](http://en.wikipedia.org/wiki/Don't_repeat_yourself), we will refactor this code.</span></span> <span data-ttu-id="bba9f-169">드리겠습니다이 사용 하 여 나중에 코드를 리팩터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-169">We'll make use of this refactored code later.</span></span>

<span data-ttu-id="bba9f-170">장르 및 artist를 추가 하는 새 메서드를 만듭니다 **SelectList** 에 **ViewBag**합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-170">Create a new method to add a genre and artist **SelectList** to the **ViewBag**.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample10.cs)]

<span data-ttu-id="bba9f-171">설정 두 줄을 `ViewBag` 각를 `Create` 및 `Edit` 메서드를 호출 하 여는 `SetGenreArtistViewBag` 메서드.</span><span class="sxs-lookup"><span data-stu-id="bba9f-171">Replace the two lines setting the `ViewBag` in each of the `Create` and `Edit` methods with a call to the `SetGenreArtistViewBag` method.</span></span> <span data-ttu-id="bba9f-172">완성된 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-172">The completed code is shown below.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample11.cs)]

<span data-ttu-id="bba9f-173">새 앨범이 만들고 작동 하는 변경 내용을 확인 하려면 앨범을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-173">Create a new album and edit an album to verify the changes work.</span></span>

### <a name="explicitly-passing-the-selectlist-to-the-dropdownlist"></a><span data-ttu-id="bba9f-174">DropDownList를 SelectList 명시적으로 전달</span><span class="sxs-lookup"><span data-stu-id="bba9f-174">Explicitly Passing the SelectList to the DropDownList</span></span>

<span data-ttu-id="bba9f-175">다음 ASP.NET MVC 스 캐 폴딩 사용 하 여 만들기 및 편집 보기 생성 **DropDownList** 오버 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-175">The create and edit views created by the ASP.NET MVC scaffolding use the following **DropDownList** overload:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample12.cs)]

<span data-ttu-id="bba9f-176">`DropDownList` 뷰 만들기에 대 한 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-176">The `DropDownList` markup for the create view is shown below.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample13.cshtml)]

<span data-ttu-id="bba9f-177">때문에 `ViewBag` 속성에 대 한는 `SelectList` 이름은 `GenreId`, **DropDownList** 도우미를 사용 하 여를 `GenreId` **SelectList** 에 **ViewBag** .</span><span class="sxs-lookup"><span data-stu-id="bba9f-177">Because the `ViewBag` property for the `SelectList` is named `GenreId`, the **DropDownList** helper will use the `GenreId`**SelectList** in the **ViewBag**.</span></span> <span data-ttu-id="bba9f-178">다음과에서 **DropDownList** 오버 로드는 `SelectList` 명시적으로 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-178">In the following **DropDownList** overload, the `SelectList` is explicitly passed in.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample14.cs)]

<span data-ttu-id="bba9f-179">열기는 *Views\StoreManager\Edit.cshtml* 파일을 열고 변경를 **DropDownList** 호출에 명시적으로 전달 합니다 **SelectList**, 위의 오버 로드를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-179">Open the *Views\StoreManager\Edit.cshtml* file, and change the **DropDownList** call to explicitly pass in the **SelectList**, using the overload above.</span></span> <span data-ttu-id="bba9f-180">장르 범주에 대해이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-180">Do this for the Genre category.</span></span> <span data-ttu-id="bba9f-181">완료 된 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-181">The completed code is shown below:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample15.cshtml)]

<span data-ttu-id="bba9f-182">응용 프로그램을 실행 하 고 클릭 합니다 **관리자** 링크를 Jazz 앨범에 이동 하 고 선택 합니다 **편집** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-182">Run the application and click the **Admin** link, then navigate to a Jazz album and select the **Edit** link.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image8.png)

<span data-ttu-id="bba9f-183">현재 선택한 장르가으로 Jazz를 표시 하는 대신 Rock 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-183">Instead of showing Jazz as the currently selected genre, Rock is displayed.</span></span> <span data-ttu-id="bba9f-184">때 문자열 인수 (바인딩할 속성) 및 **SelectList** 개체 이름이 같은, 선택한 값이 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-184">When the string argument (the property to bind) and the **SelectList** object have the same name, the selected value is not used.</span></span> <span data-ttu-id="bba9f-185">브라우저의 첫 번째 요소에 기본 제공 선택한 값의 경우는 **SelectList**(즉 **Rock** 위의 예제에서).</span><span class="sxs-lookup"><span data-stu-id="bba9f-185">When there is no selected value provided, browsers default to the first element in the **SelectList**(which is **Rock** in the example above).</span></span> <span data-ttu-id="bba9f-186">알려진 제한 사항 합니다 **DropDownList** 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-186">This is a known limitation of the **DropDownList** helper.</span></span>

<span data-ttu-id="bba9f-187">열기는 *Controllers\StoreManagerController.cs* 파일을 변경 합니다 **SelectList** 개체 이름을 `Genres` 및 `Artists`합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-187">Open the *Controllers\StoreManagerController.cs* file and change the **SelectList** object names to `Genres` and `Artists`.</span></span> <span data-ttu-id="bba9f-188">완료 된 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-188">The completed code is shown below:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample16.cs)]

<span data-ttu-id="bba9f-189">장르 및 아티스트가 이름을 각 범주의 ID 이상만 포함 하는 범주에 대 한 더 나은 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-189">The names Genres and Artists are better names for the categories, as they contain more than just the ID of each category.</span></span> <span data-ttu-id="bba9f-190">앞서 수행한 리팩터링 결실을 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-190">The refactoring we did earlier paid off.</span></span> <span data-ttu-id="bba9f-191">변경 하는 대신 합니다 **ViewBag** 네 가지 방법에는 변경 내용이 격리는 `SetGenreArtistViewBag` 메서드.</span><span class="sxs-lookup"><span data-stu-id="bba9f-191">Instead of changing the **ViewBag** in four methods, our changes were isolated to the `SetGenreArtistViewBag` method.</span></span>

<span data-ttu-id="bba9f-192">변경 된 **DropDownList** 호출 만들기에서 및 편집 보기를 사용 하도록 **SelectList** 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-192">Change the **DropDownList** call in the create and edit views to use the new **SelectList** names.</span></span> <span data-ttu-id="bba9f-193">편집 보기에 대 한 새 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-193">The new markup for the edit view is shown below:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample17.cshtml)]

<span data-ttu-id="bba9f-194">Create view는 SelectList 첫 번째 항목은 표시 되지 않도록 방지 하기 위해 빈 문자열이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-194">The Create view requires an empty string to prevent the first item in the SelectList from being displayed.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample18.cshtml)]

<span data-ttu-id="bba9f-195">새 앨범이 만들고 작동 하는 변경 내용을 확인 하려면 앨범을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-195">Create a new album and edit an album to verify the changes work.</span></span> <span data-ttu-id="bba9f-196">앨범 Rock 이외의 장르를 사용 하 여 선택 하 여 편집 코드를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-196">Test the edit code by selecting an album with a genre other than Rock.</span></span>

### <a name="using-a-view-model-with-the-dropdownlist-helper"></a><span data-ttu-id="bba9f-197">보기 모델을 사용 하 여 DropDownList 도우미를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="bba9f-197">Using a View Model with the DropDownList Helper</span></span>

<span data-ttu-id="bba9f-198">ViewModels 폴더에서 새 클래스를 만들고 `AlbumSelectListViewModel`합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-198">Create a new class in the ViewModels folder named `AlbumSelectListViewModel`.</span></span> <span data-ttu-id="bba9f-199">코드는 `AlbumSelectListViewModel` 클래스를 다음으로:</span><span class="sxs-lookup"><span data-stu-id="bba9f-199">Replace the code in the `AlbumSelectListViewModel` class with the following:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample19.cs)]

<span data-ttu-id="bba9f-200">합니다 `AlbumSelectListViewModel` 생성자는 album, 아티스트, 장르 목록을 만들고 앨범을 포함 하는 개체 및 `SelectList` 장르 및 아티스트가 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-200">The `AlbumSelectListViewModel` constructor takes an album, a list of artists and genres and creates an object containing the album and a `SelectList` for genres and artists.</span></span>

<span data-ttu-id="bba9f-201">프로젝트를 빌드 하므로 `AlbumSelectListViewModel` 사용할 수 있는 경우 다음 단계에서는 보기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-201">Build the project so the `AlbumSelectListViewModel` is available when we create a view in the next step.</span></span>

<span data-ttu-id="bba9f-202">추가 된 `EditVM` 메서드를는 `StoreManagerController`합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-202">Add an `EditVM` method to the `StoreManagerController`.</span></span> <span data-ttu-id="bba9f-203">완성된 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-203">The completed code is shown below.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample20.cs)]

<span data-ttu-id="bba9f-204">마우스 오른쪽 단추로 클릭 `AlbumSelectListViewModel`을 선택 **해결**, 한 다음 **MvcMusicStore.ViewModels;를 사용 하 여**입니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-204">Right click `AlbumSelectListViewModel`, select **Resolve**, then **using MvcMusicStore.ViewModels;**.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image9.png)

<span data-ttu-id="bba9f-205">다음을 추가할 수 또는 문을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="bba9f-205">Alternatively, you can add the following using statement:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample21.cs)]

<span data-ttu-id="bba9f-206">마우스 오른쪽 단추로 클릭 `EditVM` 선택한 **뷰 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-206">Right click `EditVM` and select **Add View**.</span></span> <span data-ttu-id="bba9f-207">아래 표시 된 옵션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-207">Use the options shown below.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image10.png)

<span data-ttu-id="bba9f-208">선택 **추가**, 그런 다음 내용의 합니다 *Views\StoreManager\EditVM.cshtml* 다음을 사용 하 여 파일:</span><span class="sxs-lookup"><span data-stu-id="bba9f-208">Select **Add**, then replace the contents of the *Views\StoreManager\EditVM.cshtml* file with the following:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample22.cshtml)]

<span data-ttu-id="bba9f-209">합니다 `EditVM` 원래 태그 매우 비슷합니다. `Edit` 다음 예외를 사용 하 여 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-209">The `EditVM` markup is very similar to the original `Edit` markup with the following exceptions.</span></span>

- <span data-ttu-id="bba9f-210">모델의 속성을 `Edit` 뷰는 형식입니다. `model.property`(예를 들어 `model.Title` ).</span><span class="sxs-lookup"><span data-stu-id="bba9f-210">Model properties in the `Edit` view are of the form `model.property`(for example, `model.Title` ).</span></span> <span data-ttu-id="bba9f-211">모델의 속성을 `EditVm` 뷰는 형식입니다. `model.Album.property`(예를 들어 `model.Album.Title`).</span><span class="sxs-lookup"><span data-stu-id="bba9f-211">Model properties in the `EditVm` view are of the form `model.Album.property`(for example, `model.Album.Title`).</span></span> <span data-ttu-id="bba9f-212">있기 때문입니다 합니다 `EditVM` 보기에 대 한 컨테이너를 전달 되는 `Album`아니라는 `Album` 에서처럼를 `Edit` 보기.</span><span class="sxs-lookup"><span data-stu-id="bba9f-212">That's because the `EditVM` view is passed a container for an `Album`, not an `Album` as in the `Edit` view.</span></span>
- <span data-ttu-id="bba9f-213">합니다 **DropDownList** 하지 뷰 모델에서 가져온 두 번째 매개 변수를 **ViewBag**합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-213">The **DropDownList** second parameter comes from the view model, not the **ViewBag**.</span></span>
- <span data-ttu-id="bba9f-214">**BeginForm** 도우미에는 `EditVM` 보기에 다시 명시적으로 게시를 `Edit` 작업 메서드.</span><span class="sxs-lookup"><span data-stu-id="bba9f-214">The **BeginForm** helper in the `EditVM` view explicitly posts back to the `Edit` action method.</span></span> <span data-ttu-id="bba9f-215">다시 게시 하 여는 `Edit` 작업에서는 작성할 필요가 `HTTP POST EditVM` 작업 다시 사용할 수 있습니다 합니다 `HTTP POST` `Edit` 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-215">By posting back to the `Edit` action, we don't have to write an `HTTP POST EditVM` action and can reuse the `HTTP POST` `Edit` action.</span></span>

<span data-ttu-id="bba9f-216">응용 프로그램을 실행 하 고 앨범을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-216">Run the application and edit an album.</span></span> <span data-ttu-id="bba9f-217">URL을 사용 하 여 변경 `EditVM`합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-217">Change the URL to use `EditVM`.</span></span> <span data-ttu-id="bba9f-218">필드를 변경 하 고 적중 합니다 **저장** 코드가 작동 중인지 확인 하는 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-218">Change a field and hit the **Save** button to verify the code is working.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image11.png)

### <a name="which-approach-should-you-use"></a><span data-ttu-id="bba9f-219">어떤 방법을 언제 사용 하나요?</span><span class="sxs-lookup"><span data-stu-id="bba9f-219">Which Approach Should You Use?</span></span>

<span data-ttu-id="bba9f-220">표시 된 세 방법 모두 acceptible 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-220">All three approaches shown are acceptible.</span></span> <span data-ttu-id="bba9f-221">대부분의 개발자 explictily 전달 하려는 합니다 `SelectList` 에 `DropDownList` 를 사용 하 여를 `ViewBag`합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-221">Many developers prefer to explictily pass the `SelectList` to the `DropDownList` using the `ViewBag`.</span></span> <span data-ttu-id="bba9f-222">이 방법은 컬렉션에 대 한 적합 한 이름을 사용 하 여 유연성을 제공 하는 추가 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-222">This approach has the added advantage of giving you the flexibility of using a more appropriate name for the collection.</span></span> <span data-ttu-id="bba9f-223">중요 한 점은 이름을 지정할 수 없습니다는 `ViewBag SelectList` 모델 속성 이름이 같은 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-223">The one caveat is you cannot name the `ViewBag SelectList` object the same name as the model property.</span></span>

<span data-ttu-id="bba9f-224">일부 개발자는 ViewModel 접근을 선호 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-224">Some developers prefer the ViewModel approach.</span></span> <span data-ttu-id="bba9f-225">다른 자세한 태그를 고려 하 고 HTML ViewModel 방식의 단점은 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-225">Others consider the more verbose markup and generated HTML of the ViewModel approach a disadvantage.</span></span>

<span data-ttu-id="bba9f-226">이 섹션의 세 가지 방법을 사용 하 여 확보 합니다 **DropDownList** 범주 데이터를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-226">In this section we have learned three approaches to using the **DropDownList** with category data.</span></span> <span data-ttu-id="bba9f-227">다음 섹션에서는 새 범주를 추가 하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="bba9f-227">In the next section, we'll show how to add a new category.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="bba9f-228">[이전](using-the-dropdownlist-helper-with-aspnet-mvc.md)
> [다음](adding-a-new-category-to-the-dropdownlist-using-jquery-ui.md)</span><span class="sxs-lookup"><span data-stu-id="bba9f-228">[Previous](using-the-dropdownlist-helper-with-aspnet-mvc.md)
[Next](adding-a-new-category-to-the-dropdownlist-using-jquery-ui.md)</span></span>
