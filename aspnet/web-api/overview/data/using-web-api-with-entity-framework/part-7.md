---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-7
title: Create View (UI) | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/16/2014
ms.topic: article
ms.assetid: b2445062-a1fe-4133-8994-f510280f6d9a
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-7
msc.type: authoredcontent
ms.openlocfilehash: 5052d7cca4a5c12a9ea56eb929d4794b19e82603
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30878804"
---
<a name="create-the-view-ui"></a><span data-ttu-id="2dd75-102">Create View (UI)</span><span class="sxs-lookup"><span data-stu-id="2dd75-102">Create the View (UI)</span></span>
====================
<span data-ttu-id="2dd75-103">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="2dd75-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="2dd75-104">완료 된 프로젝트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd75-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="2dd75-105">이 섹션에서는 응용 프로그램에 대 한 HTML를 정의 하 고 HTML 및 보기 모델 간의 데이터 바인딩을 추가할 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd75-105">In this section, you will start to define the HTML for the app, and add data binding between the HTML and the view model.</span></span>

<span data-ttu-id="2dd75-106">Views/Home/Index.cshtml 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2dd75-106">Open the file Views/Home/Index.cshtml.</span></span> <span data-ttu-id="2dd75-107">해당 파일의 전체 내용을 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2dd75-107">Replace the entire contents of that file with the following.</span></span>

[!code-cshtml[Main](part-7/samples/sample1.cshtml)]

<span data-ttu-id="2dd75-108">대부분의 `div` 요소에 대 한 사항이 [부트스트랩](http://getbootstrap.com/) 스타일을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd75-108">Most of the `div` elements are there for [Bootstrap](http://getbootstrap.com/) styling.</span></span> <span data-ttu-id="2dd75-109">중요 한 요소가 동작은 `data-bind` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="2dd75-109">The important elements are the ones with `data-bind` attributes.</span></span> <span data-ttu-id="2dd75-110">이 특성의 보기 모델에 HTML을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd75-110">This attribute links the HTML to the view model.</span></span>

<span data-ttu-id="2dd75-111">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="2dd75-111">For example:</span></span>

[!code-html[Main](part-7/samples/sample2.html)]

<span data-ttu-id="2dd75-112">이 예제는 &quot; `text` &quot; 원인을 바인딩는 `<p>` 의 값을 표시 하는 요소는 `error` 의 보기 모델에서 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="2dd75-112">In this example, the &quot;`text`&quot; binding causes the `<p>` element to show the value of the `error` property from the view model.</span></span> <span data-ttu-id="2dd75-113">이전에 설명한 대로 `error` 선언 되었습니다. 한 `ko.observable`:</span><span class="sxs-lookup"><span data-stu-id="2dd75-113">Recall that `error` was declared as a `ko.observable`:</span></span>

[!code-javascript[Main](part-7/samples/sample3.js)]

<span data-ttu-id="2dd75-114">에 새 값이 할당 될 때마다 `error`, Knockout 텍스트를 업데이트는 `<p>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="2dd75-114">Whenever a new value is assigned to `error`, Knockout updates the text in the `<p>` element.</span></span>

<span data-ttu-id="2dd75-115">`foreach` 바인딩 지시 Knockout의 내용을 반복 하는 `books` 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="2dd75-115">The `foreach` binding tells Knockout to loop through the contents of the `books` array.</span></span> <span data-ttu-id="2dd75-116">배열의 각 항목에 대 한 Knockout에서는 새 &lt;li&gt; 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="2dd75-116">For each item in the array, Knockout creates a new &lt;li&gt; element.</span></span> <span data-ttu-id="2dd75-117">바인딩 컨텍스트 내부의 `foreach` 배열 항목에서 속성을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="2dd75-117">Bindings inside the context of the `foreach` refer to properties on the array item.</span></span> <span data-ttu-id="2dd75-118">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="2dd75-118">For example:</span></span>

[!code-html[Main](part-7/samples/sample4.html)]

<span data-ttu-id="2dd75-119">여기에서 `text` 바인딩 각도 서의 작성자 속성을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="2dd75-119">Here the `text` binding reads the Author property of each book.</span></span>

<span data-ttu-id="2dd75-120">지금 응용 프로그램을 실행 하는 경우 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2dd75-120">If you run the application now, it should look like this:</span></span>

![](part-7/_static/image1.png)

<span data-ttu-id="2dd75-121">책 목록을 페이지가 로드 된 후 비동기적으로 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd75-121">The list of books loads asynchronously, after the page loads.</span></span> <span data-ttu-id="2dd75-122">지금 바로 &quot;세부 정보&quot; 링크는 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2dd75-122">Right now, the &quot;Details&quot; links are not functional.</span></span> <span data-ttu-id="2dd75-123">다음 섹션에서이 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd75-123">We'll add this functionality in the next section.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2dd75-124">[이전](part-6.md)
> [다음](part-8.md)</span><span class="sxs-lookup"><span data-stu-id="2dd75-124">[Previous](part-6.md)
[Next](part-8.md)</span></span>
