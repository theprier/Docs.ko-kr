---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/adding-a-new-category-to-the-dropdownlist-using-jquery-ui
title: JQuery UI를 사용 하 여 드롭다운 목록에 새 범주를 추가 합니다. | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2012
ms.topic: article
ms.assetid: 44aa1ac4-6ea2-48a2-972d-52710c48eae5
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/adding-a-new-category-to-the-dropdownlist-using-jquery-ui
msc.type: authoredcontent
ms.openlocfilehash: 16f7af1d679aace24fff86abb19740beebafe785
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="adding-a-new-category-to-the-dropdownlist-using-jquery-ui"></a><span data-ttu-id="0f380-102">JQuery UI를 사용 하 여 드롭다운 목록에 새 범주를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-102">Adding a New Category to the DropDownList using jQuery UI</span></span>
====================
<span data-ttu-id="0f380-103">으로 [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="0f380-103">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

<span data-ttu-id="0f380-104">HTML `Select` 태그는 고정된 범주 데이터의 목록을 표시할 적합 하지만 새 범주를 추가 해야 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-104">The HTML `Select` tag is ideal for presenting a list of fixed category data, but often times you need to add a new category.</span></span> <span data-ttu-id="0f380-105">Genre "Opera" 데이터베이스에는 각 범주에 추가 하려는 가정?</span><span class="sxs-lookup"><span data-stu-id="0f380-105">Suppose we want to add the genre "Opera" to the categories in our database?</span></span> <span data-ttu-id="0f380-106">이 섹션에서는 새 범주를 추가할 사용 하 여 대화 상자를 추가 하려면 jQuery UI 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-106">In this section, we will use jQuery UI to add a dialog box we can use to add a new category.</span></span> <span data-ttu-id="0f380-107">아래 이미지는 브라우저의 UI를 표시 합니다 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-107">The image below shows how the UI will present in the browser.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image1.png)

<span data-ttu-id="0f380-108">사용자가 선택할 때는 **새 장르 추가** 링크를 팝업 대화 상자 라는 새 장르 이름 (및 필요에 따라 설명)에 대 한 사용자 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-108">When a user selects the **Add New Genre** link, a pop-up dialog box prompts the user for a new genre name (and optionally a description).</span></span> <span data-ttu-id="0f380-109">표시 아래 이미지는 **추가 장르** 팝업 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="0f380-109">The image below show the **Add Genre** pop-up dialog.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image2.png)

<span data-ttu-id="0f380-110">새 장르 이름을 입력 하는 경우 및 **저장** 단추를 누르면 다음이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-110">When a new genre name is entered and the **Save** button is pushed, the following happens:</span></span>

1. <span data-ttu-id="0f380-111">AJAX 호출 데이터를 데이터베이스에 새 장르를 저장 한 JSON으로 새 장르 정보 (장르 이름 및 ID)를 반환 장르 컨트롤러의 Create 메서드를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-111">An AJAX call posts the data to the Create method of the Genre Controller, which saves the new genre to the database and returns the new genre information (genre name and ID) as JSON.</span></span>
2. <span data-ttu-id="0f380-112">JavaScript는 select 목록에 새 장르 데이터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-112">JavaScript adds the new genre data to the select list.</span></span>
3. <span data-ttu-id="0f380-113">JavaScript 새 장르 선택한 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-113">JavaScript makes the new genre the selected item.</span></span>

   <span data-ttu-id="0f380-114">아래 이미지에 **Opera** 가 데이터베이스에 추가 되 고에서 선택한는 **장르** 드롭다운 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-114">In the image below, **Opera** was added to the database and selected in the **Genre** drop down list.</span></span> 

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image3.png)

<span data-ttu-id="0f380-115">열기는 *Views\StoreManager\Create.cshtml* 파일을 장르 태그를 다음과 같이 바꿉니다 다음 코드:</span><span class="sxs-lookup"><span data-stu-id="0f380-115">Open the *Views\StoreManager\Create.cshtml* file and replace the genre markup with the following the following code:</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample1.cshtml)]

<span data-ttu-id="0f380-116">`_ChooseGenre` 부분 뷰는 JavaScript 및 jQuery 새로운 장르 추가 기능을 구현 하는 데 후크 모든 논리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-116">The `_ChooseGenre` partial view will contain all the logic to hook up the JavaScript and jQuery used to implement the add new genre feature.</span></span> <span data-ttu-id="0f380-117">코드 작업을 완료 했습니다 간단 하 게 아티스트 UI와 동일 하 게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-117">Once we have completed the code it will be simple to do the same with the artist UI.</span></span>

<span data-ttu-id="0f380-118">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 하 고 *Views\StoreManager* 폴더를 선택 **추가**, 다음 **보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-118">In Solution Explorer, right click the *Views\StoreManager* folder and select **Add**, then **View**.</span></span> <span data-ttu-id="0f380-119">에 **뷰 이름** 입력, 입력 `_ChooseGenre` 다음 선택 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-119">In the **View name** input, enter `_ChooseGenre` then select **Add**.</span></span> <span data-ttu-id="0f380-120">태그에 바꿉니다는 *Views\StoreManager\\_ChooseGenre.cshtml* 다음 파일:</span><span class="sxs-lookup"><span data-stu-id="0f380-120">Replace the markup in the *Views\StoreManager\\_ChooseGenre.cshtml* file with the following:</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample2.cshtml)]

<span data-ttu-id="0f380-121">첫 번째 줄 선언에 전달 하는 `Album` 예제의 모델에서는으로 Create view 문이 모델 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-121">The first line declares that we are passing in an `Album` as our model, exactly the same model statement found in the Create view.</span></span> <span data-ttu-id="0f380-122">다음 몇 줄은는 **레이블** 도우미 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-122">The next few lines are the **Label** helper markup.</span></span> <span data-ttu-id="0f380-123">다음 줄은는 **DropDownList** 도우미 호출 원래 Create view와 정확히 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-123">The next line is the **DropDownList** helper call, exactly the same as in the original Create view.</span></span> <span data-ttu-id="0f380-124">다음 줄 추가 이름의 링크 `Add New Genre`, 단추 처럼 스타일입니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-124">The next line adds a link with the name `Add New Genre`, and styles it like a button.</span></span> <span data-ttu-id="0f380-125">포함 하는 줄 `ValidationMessageFor` 는 만들기 뷰로부터 직접 복사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-125">The line containing `ValidationMessageFor` is copied directly from the Create view.</span></span> <span data-ttu-id="0f380-126">다음 줄:</span><span class="sxs-lookup"><span data-stu-id="0f380-126">The following lines:</span></span>

[!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample3.html)]

<span data-ttu-id="0f380-127">ID를 사용 하 여 숨겨진된 div 만듭니다 `genreDialog`합니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-127">creates a hidden div, with the ID of `genreDialog`.</span></span> <span data-ttu-id="0f380-128">JQuery를 연결 하는 데 사용할 우리의 **추가 장르** ID와 대화 상자 `genreDialog` 이 div.에서</span><span class="sxs-lookup"><span data-stu-id="0f380-128">We will use jQuery to hook up our **Add Genre** dialog box with the ID `genreDialog` in this div.</span></span> <span data-ttu-id="0f380-129">마지막 두 개의 스크립트 태그를 사용 하면 새 장르 추가 기능을 구현 하는 데 사용할 JavaScript 파일에 링크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-129">The last two script tags contain links to the JavaScript files we will use to implement the add new genre feature.</span></span> <span data-ttu-id="0f380-130">*/Scripts/chooseGenre.js* 파일은 프로젝트에 자동으로 살펴보겠습니다이 자습서의 뒷부분에 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-130">The */Scripts/chooseGenre.js* file is provided for you in the project, we will examine it later in the tutorial.</span></span>

<span data-ttu-id="0f380-131">응용 프로그램을 실행 하 고 클릭는 **새 장르 추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-131">Run the application and click on the **Add New Genre** button.</span></span> <span data-ttu-id="0f380-132">에 **추가 장르** 대화 상자에 입력 **Opera** 에 **이름** 입력된 상자.</span><span class="sxs-lookup"><span data-stu-id="0f380-132">In the **Add Genre** dialog box, enter **Opera** in the **Name** input box.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image4.png)

<span data-ttu-id="0f380-133">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-133">Click the **Save** button.</span></span> <span data-ttu-id="0f380-134">AJAX 호출 Opera 범주를 만듭니다 하 고 속성을 사용 하 여 드롭다운 목록 채우고 Opera 선택한 장르로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-134">An AJAX call creates the Opera category and then populates the dropdown list with Opera, and sets Opera as the selected genre.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image5.png)

<span data-ttu-id="0f380-135">아티스트, 제목 및 가격을 입력 한 다음 선택에서 **만들기** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-135">Enter an artist, title and price, then select the **Create** button.</span></span> <span data-ttu-id="0f380-136">$8.99 보다 작은 가격을 입력 하면 새 앨범 인덱스 보기의 맨 위쪽에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-136">If you enter a price less than $8.99, the new album will appear at the top of the Index view.</span></span> <span data-ttu-id="0f380-137">데이터베이스에 저장 된 새 앨범 항목을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-137">Verify the new album entry was saved in the database.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image6.png)

<span data-ttu-id="0f380-138">하나의 문자를 가진 새 장르를 만들어 보십시오.</span><span class="sxs-lookup"><span data-stu-id="0f380-138">Try creating a new genre with only one letter.</span></span> <span data-ttu-id="0f380-139">다음 코드는 *Models\Genre.cs* 파일 장르 이름의 최소 및 최대 길이 가져오거나 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-139">The following code in the *Models\Genre.cs* file sets the minimum and maximum length of the genre name.</span></span>

[!code-csharp[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample4.cs)]

<span data-ttu-id="0f380-140">클라이언트 쪽 유효성 검사 보고 2 ~ 20 자 사이의 문자열을 입력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-140">Client side validation reports you must enter a string between 2 and 20 characters.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image7.png)

### <a name="examining-how-a-new-genre-is-added-to-the-database-and-the-select-list"></a><span data-ttu-id="0f380-141">어떻게 정도 새 장르를 검사 하는 데이터베이스 및 선택 목록에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-141">Examining How a New Genre is Added to the Database and the Select List.</span></span>

<span data-ttu-id="0f380-142">열기는 *Scripts\chooseGenre.js* 파일 및 코드를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-142">Open the *Scripts\chooseGenre.js* file and examine the code.</span></span>

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample5.js)]

<span data-ttu-id="0f380-143">두 번째 줄은 ID를 사용 하 여 `genreDialog` 에 div 태그에는 대화 상자를 만들려면는 *Views\StoreManager\\_ChooseGenre.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-143">The second line uses the ID `genreDialog` to create a dialog box on the div tag in the *Views\StoreManager\\_ChooseGenre.cshtml* file.</span></span> <span data-ttu-id="0f380-144">대부분의 명명 된 매개 변수는 자체 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-144">Most of the named parameters are self explanatory.</span></span> <span data-ttu-id="0f380-145">`autoOpen` 매개 변수가 false로 설정 된 선택 하는 **만들 장르** 버튼을 클릭 하면 대화 상자가 명시적으로 열리며 됩니다 (이 설명에).</span><span class="sxs-lookup"><span data-stu-id="0f380-145">The `autoOpen` parameter is set to false, selecting the **Create Genre** button will open the dialogue explicitly (this is described latter on).</span></span> <span data-ttu-id="0f380-146">해당 대화 상자에 두 개의 단추 **저장** 및 **취소**합니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-146">The dialog has two buttons, **Save** and **Cancel**.</span></span> <span data-ttu-id="0f380-147">**취소** 단추 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-147">The **Cancel** button closes the dialog.</span></span> <span data-ttu-id="0f380-148">다음 코드는 **저장** 함수를 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-148">The following code shows the **Save** button function.</span></span>

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample6.js)]

<span data-ttu-id="0f380-149">`var createGenreForm` 에서 선택 된 `createGenreForm` id입니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-149">The `var createGenreForm` is selected from the `createGenreForm` ID.</span></span> <span data-ttu-id="0f380-150">`createGenreForm` 에 다음 코드에 설정 된 ID는 *Views\Genre\\_CreateGenre.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-150">The `createGenreForm` ID was set in the following code found in the *Views\Genre\\_CreateGenre.cshtml* file.</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample7.cshtml)]

<span data-ttu-id="0f380-151">[Html.BeginForm](https://msdn.microsoft.com/library/dd492714.aspx) 도우미 오버 로드에 사용 되는 *Views\Genre\\_CreateGenre.cshtml* 파일에서는 양식을 제출 URL이 포함 된 동작 특성을 가진 HTML을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-151">The [Html.BeginForm](https://msdn.microsoft.com/library/dd492714.aspx) helper overload used in the *Views\Genre\\_CreateGenre.cshtml* file generates HTML with an action attribute containing the URL to submit the form.</span></span> <span data-ttu-id="0f380-152">브라우저에서 만들기 앨범 페이지를 표시 하 고 브라우저에 표시 소스를 선택 하 여이 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-152">You can see this by displaying the create album page in a browser and selecting show source in the browser.</span></span> <span data-ttu-id="0f380-153">다음 태그는 form 태그를 포함 하는 생성 된 HTML을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-153">The following markup shows the generated HTML containing the form tag.</span></span>

[!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample8.html)]

<span data-ttu-id="0f380-154">JQuery `$.post` 선이 작업 특성에 대 한 AJAX 호출 (`/StoreManager/Create`) 하 고 데이터를 전달는 **만들 장르** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="0f380-154">The jQuery `$.post` line makes an AJAX call to the action attribute (`/StoreManager/Create`) and passes in the data from the **Create Genre** dialog box.</span></span> <span data-ttu-id="0f380-155">데이터 새 genre 및 선택적 설명을 대 한 이름으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-155">The data consists of the name for the new genre and an optional description.</span></span> <span data-ttu-id="0f380-156">AJAX 호출 되 면 하는 경우에 새 장르 이름 및 값 Select 태그에 추가 되 고 새 장르 선택한 값으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-156">If the AJAX call is successful, the new genre name and value are added to the Select markup, and the new genre is set to the selected value.</span></span> <span data-ttu-id="0f380-157">동적으로 생성 된 태그 이기 때문에 브라우저에 소스를 확인 하 여 새 선택 옵션을 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-157">Because this is dynamically generated markup, you can't see the new select option by viewing the source in the browser.</span></span> <span data-ttu-id="0f380-158">IE 9 F12 개발자 도구를 사용 하 여 새 HTML을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-158">You can see the new HTML with the IE 9 F12 developer tools.</span></span> <span data-ttu-id="0f380-159">Internet Explorer 9에서 새로운 선택 옵션을 보려면 F12 개발자 도구를 시작 하려면 F12 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-159">To view the new select option, in Internet Explorer 9, hit the F12 key to start the F12 developer tools.</span></span> <span data-ttu-id="0f380-160">만들기 페이지로 이동한 다음 새 장르 장르 select 목록에서 선택 되어 있으므로 새 장르를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-160">Navigate to the Create page and add a new genre so the new genre is selected in the genre select list.</span></span> <span data-ttu-id="0f380-161">F12 개발자 도구:</span><span class="sxs-lookup"><span data-stu-id="0f380-161">In the F12 developer tools:</span></span>

1. <span data-ttu-id="0f380-162">HTML 탭을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-162">Select the HTML tab.</span></span>
2. <span data-ttu-id="0f380-163">새로 고침 아이콘에 도달 했습니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-163">Hit the refresh icon.</span></span>  
    ![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image8.png)
3. <span data-ttu-id="0f380-164">검색 상자에 GenreID를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-164">In the search box, enter GenreID.</span></span>
4. <span data-ttu-id="0f380-165">다음 아이콘을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="0f380-165">Using the next icon,</span></span>   
    ![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image9.png)  
   <span data-ttu-id="0f380-166">다음 select 태그를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-166">navigate to the following select tag:</span></span>

    [!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample9.html)]
5. <span data-ttu-id="0f380-167">마지막 옵션 값을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-167">Expand the last option value.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image10.png)

<span data-ttu-id="0f380-168">다음 코드는 *Scripts\chooseGenre.js* 파일에서는 **새 장르 추가** 단추 클릭 이벤트에 연결 방식 **새 장르 추가** 대화 상자는 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-168">The following code in the *Scripts\chooseGenre.js* file shows the how the **Add New Genre** button gets connected to the click event, and how the **Add New Genre** dialog box is created.</span></span>

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample10.js)]

<span data-ttu-id="0f380-169">첫 번째 줄에 연결 하는 클릭 함수를 만듭니다는 **새 장르 추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-169">The first line creates a click function attached to the **Add New Genre** button.</span></span> <span data-ttu-id="0f380-170">다음 태그는 Views\StoreManager에서\\_ChooseGenre.cshtml 파일 표시 방법을 **새 장르 추가** 단추를 만들:</span><span class="sxs-lookup"><span data-stu-id="0f380-170">The following markup from the Views\StoreManager\\_ChooseGenre.cshtml file shows how the **Add New Genre** button is created:</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample11.cshtml)]

<span data-ttu-id="0f380-171">Load 메서드 및 장르 추가 대화 상자를 엽니다 만들고 호출 jQuery `parse` 메서드 클라이언트 유효성 검사 대화 상자에 입력 된 데이터에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-171">The load method creates and opens the Add Genre dialog and calls the jQuery `parse` method so client validation occurs on data entered in the dialog.</span></span>

<span data-ttu-id="0f380-172">이 섹션에서는 select 목록에 새 범주 데이터를 추가 하는 데 사용할 수 있는 대화를 만드는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-172">In this section you have learned how to create a dialog that can be used to add new category data to a select list.</span></span> <span data-ttu-id="0f380-173">새 아티스트 아티스트 select 목록에 추가 하는 UI를 만들려면 동일한 절차를 따르면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-173">You can follow the same procedure to create UI to add a new artist to the artist select list.</span></span> <span data-ttu-id="0f380-174">이 자습서에서는 ASP.NET MVC HTML 도우미와 작업 개요 ¡° ô **DropDownList**합니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-174">This tutorial has given an overview of working with the ASP.NET MVC HTML helper **DropDownList**.</span></span> <span data-ttu-id="0f380-175">작업에 대 한 자세한 내용은 **DropDownList**, 아래 추가 참조 섹션을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-175">For additional information on working with the **DropDownList**, see the addition references section below.</span></span> <span data-ttu-id="0f380-176">알려 주시면이 자습서 도움이 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-176">Please let us know if this tutorial has been helpful.</span></span>

<span data-ttu-id="0f380-177">Rick.Anderson[at]Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="0f380-177">Rick.Anderson[at]Microsoft.com</span></span>

### <a name="additional-references"></a><span data-ttu-id="0f380-178">추가 참조</span><span class="sxs-lookup"><span data-stu-id="0f380-178">Additional References</span></span>

- <span data-ttu-id="0f380-179">[자습서를 나열 하는 ASP.NET MVC – 계단식 드롭다운](https://weblogs.asp.net/raduenuca/archive/2011/03/06/asp-net-mvc-cascading-dropdown-lists-tutorial-part-1-defining-the-problem-and-the-context.aspx) 여 [Radu Enuca](https://weblogs.asp.net/raduenuca/default.aspx)</span><span class="sxs-lookup"><span data-stu-id="0f380-179">[ASP.NET MVC–Cascading Dropdown Lists Tutorial](https://weblogs.asp.net/raduenuca/archive/2011/03/06/asp-net-mvc-cascading-dropdown-lists-tutorial-part-1-defining-the-problem-and-the-context.aspx) by [Radu Enuca](https://weblogs.asp.net/raduenuca/default.aspx)</span></span>
- <span data-ttu-id="0f380-180">[선택한](http://harvesthq.github.com/chosen/) JavaScript 플러그 인을 여러 개 선택 및 필터링을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f380-180">[Chosen](http://harvesthq.github.com/chosen/) A JavaScript plugin that support multi-select and filtering.</span></span>

### <a name="contributors"></a><span data-ttu-id="0f380-181">참가자</span><span class="sxs-lookup"><span data-stu-id="0f380-181">Contributors</span></span>

- [<span data-ttu-id="0f380-182">Radu Enuca</span><span class="sxs-lookup"><span data-stu-id="0f380-182">Radu Enuca</span></span>](https://weblogs.asp.net/raduenuca/default.aspx)
- <span data-ttu-id="0f380-183">장 Sébastien Goupil</span><span class="sxs-lookup"><span data-stu-id="0f380-183">Jean-Sébastien Goupil</span></span>
- [<span data-ttu-id="0f380-184">Brad Wilson</span><span class="sxs-lookup"><span data-stu-id="0f380-184">Brad Wilson</span></span>](http://bradwilson.typepad.com/)

### <a name="reviewers"></a><span data-ttu-id="0f380-185">검토자</span><span class="sxs-lookup"><span data-stu-id="0f380-185">Reviewers</span></span>

- <span data-ttu-id="0f380-186">장 Sébastien Goupil</span><span class="sxs-lookup"><span data-stu-id="0f380-186">Jean-Sébastien Goupil</span></span>
- [<span data-ttu-id="0f380-187">Brad Wilson</span><span class="sxs-lookup"><span data-stu-id="0f380-187">Brad Wilson</span></span>](http://bradwilson.typepad.com/)
- <span data-ttu-id="0f380-188">Mike 서</span><span class="sxs-lookup"><span data-stu-id="0f380-188">Mike Pope</span></span>
- <span data-ttu-id="0f380-189">Tom Dykstra</span><span class="sxs-lookup"><span data-stu-id="0f380-189">Tom Dykstra</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="0f380-190">이전</span><span class="sxs-lookup"><span data-stu-id="0f380-190">Previous</span></span>](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper.md)
