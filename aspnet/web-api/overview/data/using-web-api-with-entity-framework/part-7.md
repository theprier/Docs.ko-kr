---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-7
title: 보기 (UI) 만들기 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
ms.date: 06/16/2014
ms.assetid: b2445062-a1fe-4133-8994-f510280f6d9a
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-7
msc.type: authoredcontent
ms.openlocfilehash: eeaa36ede45b82afd112a270acf68105d1ae6dbc
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37820988"
---
<a name="create-the-view-ui"></a><span data-ttu-id="32993-102">보기 (UI) 만들기</span><span class="sxs-lookup"><span data-stu-id="32993-102">Create the View (UI)</span></span>
====================
<span data-ttu-id="32993-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="32993-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="32993-104">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="32993-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="32993-105">이 섹션에서는 앱에 대 한 HTML을 정의 하 고 HTML 및 보기 모델 간의 데이터 바인딩을 추가를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="32993-105">In this section, you will start to define the HTML for the app, and add data binding between the HTML and the view model.</span></span>

<span data-ttu-id="32993-106">Views/Home/Index.cshtml 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="32993-106">Open the file Views/Home/Index.cshtml.</span></span> <span data-ttu-id="32993-107">해당 파일의 전체 내용을 다음으로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="32993-107">Replace the entire contents of that file with the following.</span></span>

[!code-cshtml[Main](part-7/samples/sample1.cshtml)]

<span data-ttu-id="32993-108">대부분의 합니다 `div` 요소에 대 한 사항이 [부트스트랩](http://getbootstrap.com/) 스타일을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="32993-108">Most of the `div` elements are there for [Bootstrap](http://getbootstrap.com/) styling.</span></span> <span data-ttu-id="32993-109">중요 한 요소는 사용 하 여 `data-bind` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="32993-109">The important elements are the ones with `data-bind` attributes.</span></span> <span data-ttu-id="32993-110">이 특성을 뷰 모델로 HTML을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="32993-110">This attribute links the HTML to the view model.</span></span>

<span data-ttu-id="32993-111">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="32993-111">For example:</span></span>

[!code-html[Main](part-7/samples/sample2.html)]

<span data-ttu-id="32993-112">이 예제에서는 합니다 &quot; `text` &quot; 원인 바인딩를 `<p>` 값을 표시 하는 요소는 `error` 뷰 모델에서 속성.</span><span class="sxs-lookup"><span data-stu-id="32993-112">In this example, the &quot;`text`&quot; binding causes the `<p>` element to show the value of the `error` property from the view model.</span></span> <span data-ttu-id="32993-113">이전에 설명한 대로 `error` 로 선언 된 `ko.observable`:</span><span class="sxs-lookup"><span data-stu-id="32993-113">Recall that `error` was declared as a `ko.observable`:</span></span>

[!code-javascript[Main](part-7/samples/sample3.js)]

<span data-ttu-id="32993-114">새 값을 할당할 때마다 `error`, Knockout 텍스트를 업데이트 합니다 `<p>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="32993-114">Whenever a new value is assigned to `error`, Knockout updates the text in the `<p>` element.</span></span>

<span data-ttu-id="32993-115">합니다 `foreach` 바인딩 지시 Knockout의 내용을 반복 하는 `books` 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="32993-115">The `foreach` binding tells Knockout to loop through the contents of the `books` array.</span></span> <span data-ttu-id="32993-116">Knockout 배열의 각 항목에 대해 새로 만들고 &lt;li&gt; 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="32993-116">For each item in the array, Knockout creates a new &lt;li&gt; element.</span></span> <span data-ttu-id="32993-117">컨텍스트 내에서 바인딩에 `foreach` 배열 항목의 속성을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="32993-117">Bindings inside the context of the `foreach` refer to properties on the array item.</span></span> <span data-ttu-id="32993-118">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="32993-118">For example:</span></span>

[!code-html[Main](part-7/samples/sample4.html)]

<span data-ttu-id="32993-119">여기서는 `text` 바인딩 각 책의 저자 속성을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="32993-119">Here the `text` binding reads the Author property of each book.</span></span>

<span data-ttu-id="32993-120">이제 응용 프로그램을 실행 하는 경우 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32993-120">If you run the application now, it should look like this:</span></span>

![](part-7/_static/image1.png)

<span data-ttu-id="32993-121">책의 목록이 페이지가 로드 된 후 비동기적으로 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="32993-121">The list of books loads asynchronously, after the page loads.</span></span> <span data-ttu-id="32993-122">지금 바로 합니다 &quot;세부 정보&quot; 링크는 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="32993-122">Right now, the &quot;Details&quot; links are not functional.</span></span> <span data-ttu-id="32993-123">다음 섹션에서이 기능을 추가 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="32993-123">We'll add this functionality in the next section.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="32993-124">[이전](part-6.md)
> [다음](part-8.md)</span><span class="sxs-lookup"><span data-stu-id="32993-124">[Previous](part-6.md)
[Next](part-8.md)</span></span>
