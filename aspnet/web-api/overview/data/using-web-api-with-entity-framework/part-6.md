---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-6
title: JavaScript 클라이언트 만들기 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/16/2014
ms.topic: article
ms.assetid: 20360326-b123-4b1e-abae-1d350edf4ce4
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-6
msc.type: authoredcontent
ms.openlocfilehash: 29d50e448e6d282c7db06b9d1946ac221347e1ea
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="create-the-javascript-client"></a><span data-ttu-id="a3424-102">JavaScript 클라이언트 만들기</span><span class="sxs-lookup"><span data-stu-id="a3424-102">Create the JavaScript Client</span></span>
====================
<span data-ttu-id="a3424-103">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="a3424-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="a3424-104">완료 된 프로젝트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3424-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="a3424-105">이 섹션에서는 HTML, JavaScript를 사용 하 여 응용 프로그램에 대 한 클라이언트 만들어집니다 및 [Knockout.js](http://knockoutjs.com/) 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="a3424-105">In this section, you will create the client for the application, using HTML, JavaScript, and the [Knockout.js](http://knockoutjs.com/) library.</span></span> <span data-ttu-id="a3424-106">클라이언트 응용 프로그램을 단계별로 작성할 것:</span><span class="sxs-lookup"><span data-stu-id="a3424-106">We'll build the client app in stages:</span></span>

- <span data-ttu-id="a3424-107">책의 목록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3424-107">Showing a list of books.</span></span>
- <span data-ttu-id="a3424-108">책 자세한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3424-108">Showing a book detail.</span></span>
- <span data-ttu-id="a3424-109">새 책을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3424-109">Adding a new book.</span></span>

<span data-ttu-id="a3424-110">Knockout 라이브러리 모델-뷰-MVVM () 패턴을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a3424-110">The Knockout library uses the Model-View-ViewModel (MVVM) pattern:</span></span>

- <span data-ttu-id="a3424-111">**모델** (대/소문자에 책 저자) 비즈니스 도메인에 있는 데이터의 서버 쪽 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="a3424-111">The **model** is the server-side representation of the data in the business domain (in our case, books and authors).</span></span>
- <span data-ttu-id="a3424-112">**보기** 프레젠테이션 계층 (HTML)입니다.</span><span class="sxs-lookup"><span data-stu-id="a3424-112">The **view** is the presentation layer (HTML).</span></span>
- <span data-ttu-id="a3424-113">**뷰 모델** 은 모델을 포함 하는 JavaScript 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="a3424-113">The **view model** is a JavaScript object that holds the models.</span></span> <span data-ttu-id="a3424-114">뷰 모델은 UI의 코드 추상화입니다.</span><span class="sxs-lookup"><span data-stu-id="a3424-114">The view model is a code abstraction of the UI.</span></span> <span data-ttu-id="a3424-115">그는 HTML 표현의 알지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="a3424-115">It has no knowledge of the HTML representation.</span></span> <span data-ttu-id="a3424-116">대신, 나타내는 보기의 추상 기능와 같은 &quot;책의 목록이&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="a3424-116">Instead, it represents abstract features of the view, such as &quot;a list of books&quot;.</span></span>

<span data-ttu-id="a3424-117">뷰 데이터 바인딩된 보기 모델에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3424-117">The view is data-bound to the view model.</span></span> <span data-ttu-id="a3424-118">보기 모델에 대 한 업데이트는 자동으로 보기에 반영 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3424-118">Updates to the view model are automatically reflected in the view.</span></span> <span data-ttu-id="a3424-119">뷰 모델 이벤트도를 가져옵니다 보기에서 단추 클릭과 같은 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3424-119">The view model also gets events from the view, such as button clicks.</span></span>

![](part-6/_static/image1.png)

<span data-ttu-id="a3424-120">이 접근 방식을 쉽게 레이아웃 및 응용 프로그램의 UI를 변경 하려면 바인딩, 모든 코드를 다시 작성 하지 않고 변경할 수 있으므로 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3424-120">This approach makes it easy to change the layout and UI of your app, because you can change the bindings, without rewriting any code.</span></span> <span data-ttu-id="a3424-121">으로 항목 목록이 표시 될 수 있습니다는 예를 들어 한 `<ul>`, 나중에 변경할 테이블에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3424-121">For example, you might show a list of items as a `<ul>`, then change it later to a table.</span></span>

## <a name="add-the-knockout-library"></a><span data-ttu-id="a3424-122">Knockout 라이브러리 추가</span><span class="sxs-lookup"><span data-stu-id="a3424-122">Add the Knockout Library</span></span>

<span data-ttu-id="a3424-123">Visual Studio에서에서 **도구** 메뉴 선택 **라이브러리 패키지 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3424-123">In Visual Studio, from the **Tools** menu, select **Library Package Manager**.</span></span> <span data-ttu-id="a3424-124">그런 다음 선택 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3424-124">Then select **Package Manager Console**.</span></span> <span data-ttu-id="a3424-125">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3424-125">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](part-6/samples/sample1.cmd)]

<span data-ttu-id="a3424-126">이 명령은 스크립트 폴더에 Knockout 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a3424-126">This command adds the Knockout files to the Scripts folder.</span></span>

## <a name="create-the-view-model"></a><span data-ttu-id="a3424-127">뷰 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="a3424-127">Create the View Model</span></span>

<span data-ttu-id="a3424-128">라는 app.js 스크립트 폴더에 JavaScript 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3424-128">Add a JavaScript file named app.js to the Scripts folder.</span></span> <span data-ttu-id="a3424-129">(솔루션 탐색기에서 스크립트 폴더를 마우스 오른쪽 단추로 선택, **추가**을 선택한 후 **JavaScript 파일**.) 다음 코드에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="a3424-129">(In Solution Explorer, right-click the Scripts folder, select **Add**, then select **JavaScript File**.) Paste in the following code:</span></span>

[!code-javascript[Main](part-6/samples/sample2.js)]

<span data-ttu-id="a3424-130">Knockout에 `observable` 클래스를 사용 하면 데이터 바인딩.</span><span class="sxs-lookup"><span data-stu-id="a3424-130">In Knockout, the `observable` class enables data-binding.</span></span> <span data-ttu-id="a3424-131">Observable의 내용이 변경 될 경우 observable가 알립니다의 모든 데이터 바인딩된 컨트롤을 자체를 업데이트할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3424-131">When the contents of an observable change, the observable notifies all of the data-bound controls, so they can update themselves.</span></span> <span data-ttu-id="a3424-132">(의 `observableArray` 클래스는 배열 형식의 *observable*.) 시작 하 여 뷰 모델 두 관찰 가능 개체에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3424-132">(The `observableArray` class is the array version of *observable*.) To start with, our view model has two observables:</span></span>

- <span data-ttu-id="a3424-133">`books` 설명서의 목록을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3424-133">`books` holds the list of books.</span></span>
- <span data-ttu-id="a3424-134">`error` AJAX 호출이 실패 한 경우 오류 메시지를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3424-134">`error` contains an error message if an AJAX call fails.</span></span>

<span data-ttu-id="a3424-135">`getAllBooks` 메서드 책 목록을 AJAX 호출을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a3424-135">The `getAllBooks` method makes an AJAX call to get the list of books.</span></span> <span data-ttu-id="a3424-136">다음 결과를 푸시합니다는 `books` 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="a3424-136">Then it pushes the result onto the `books` array.</span></span>

<span data-ttu-id="a3424-137">`ko.applyBindings` 메서드는 Knockout 라이브러리의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="a3424-137">The `ko.applyBindings` method is part of the Knockout library.</span></span> <span data-ttu-id="a3424-138">매개 변수로 보기 모델을 사용 하 고 데이터 바인딩을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3424-138">It takes the view model as a parameter and sets up the data binding.</span></span>

## <a name="add-a-script-bundle"></a><span data-ttu-id="a3424-139">스크립트 번들 추가</span><span class="sxs-lookup"><span data-stu-id="a3424-139">Add a Script Bundle</span></span>

<span data-ttu-id="a3424-140">번들로 결합 하거나 단일 파일에 여러 파일을 번들로 쉽게 수 있도록 ASP.NET 4.5에서 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="a3424-140">Bundling is a feature in ASP.NET 4.5 that makes it easy to combine or bundle multiple files into a single file.</span></span> <span data-ttu-id="a3424-141">번들 페이지 로드 시간을 향상 시킬 수 있는 서버에 요청 수가 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="a3424-141">Bundling reduces the number of requests to the server, which can improve page load time.</span></span>

<span data-ttu-id="a3424-142">응용 프로그램 파일을 열고\_Start/BundleConfig.cs 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3424-142">Open the file App\_Start/BundleConfig.cs.</span></span> <span data-ttu-id="a3424-143">RegisterBundles 메서드에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3424-143">Add the following code to the RegisterBundles method.</span></span>

[!code-csharp[Main](part-6/samples/sample3.cs)]

> [!div class="step-by-step"]
> <span data-ttu-id="a3424-144">[이전](part-5.md)
> [다음](part-7.md)</span><span class="sxs-lookup"><span data-stu-id="a3424-144">[Previous](part-5.md)
[Next](part-7.md)</span></span>
