---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-8
title: 항목 세부 정보를 표시 합니다. | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 75ef94b1-bbec-4681-9210-452dba816144
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-8
msc.type: authoredcontent
ms.openlocfilehash: 83f291326307a4964afdd5e8b50f2c375348ed0e
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41827757"
---
<a name="display-item-details"></a><span data-ttu-id="13fb9-102">항목 세부 정보 표시</span><span class="sxs-lookup"><span data-stu-id="13fb9-102">Display Item Details</span></span>
====================
<span data-ttu-id="13fb9-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="13fb9-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="13fb9-104">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="13fb9-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="13fb9-105">이 섹션에서는 각 책에 대 한 세부 정보를 확인 하는 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="13fb9-105">In this section, you will add the ability to view details for each book.</span></span> <span data-ttu-id="13fb9-106">App.js에서 뷰 모델에는 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="13fb9-106">In app.js, add to the following code to the view model:</span></span>

[!code-javascript[Main](part-8/samples/sample1.js)]

<span data-ttu-id="13fb9-107">Views/Home/Index.cshtml에서 데이터를 바인딩 요소를 세부 정보 링크를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="13fb9-107">In Views/Home/Index.cshtml, add a data-bind element to the Details link:</span></span>

[!code-html[Main](part-8/samples/sample2.html?highlight=5)]

<span data-ttu-id="13fb9-108">이 대 한 클릭 처리기를 바인딩하는 &lt;는&gt; 요소를 `getBookDetail` 뷰 모델에서 함수.</span><span class="sxs-lookup"><span data-stu-id="13fb9-108">This binds the click handler for the &lt;a&gt; element to the `getBookDetail` function on the view model.</span></span>

<span data-ttu-id="13fb9-109">동일한 파일에서 다음 마크업을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="13fb9-109">In the same file, replace the following mark-up:</span></span>

[!code-html[Main](part-8/samples/sample3.html)]

<span data-ttu-id="13fb9-110">다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="13fb9-110">with this:</span></span>

[!code-html[Main](part-8/samples/sample4.html)]

<span data-ttu-id="13fb9-111">이 태그의 속성과 데이터 바인딩된 테이블을 만듭니다는 `detail` 보기 모델의 observable입니다.</span><span class="sxs-lookup"><span data-stu-id="13fb9-111">This markup creates a table that is data-bound to the properties of the `detail` observable in the view model.</span></span>

<span data-ttu-id="13fb9-112">"&lt;!-코-&gt; &quot; 구문 DOM 요소를 외부 Knockout 바인딩을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13fb9-112">The "&lt;!-- ko --&gt;&quot; syntax lets you include a Knockout binding outside of a DOM element.</span></span> <span data-ttu-id="13fb9-113">이 경우에 `if` 바인딩을 사용 하면 표시 되는 태그의이 섹션에서는 경우에만 `details` null이 아닌 합니다.</span><span class="sxs-lookup"><span data-stu-id="13fb9-113">In this case, the `if` binding causes this section of markup to be displayed only when `details` is non-null.</span></span>

[!code-html[Main](part-8/samples/sample5.html)]

<span data-ttu-id="13fb9-114">이제 앱을 실행 하 고 중 하나를 클릭 합니다 &quot;세부 정보&quot; 링크를 앱에는 책 세부 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="13fb9-114">Now if you run the app and click one of the &quot;Detail&quot; links, the app will display the book details.</span></span>

[![](part-8/_static/image2.png)](part-8/_static/image1.png)

> [!div class="step-by-step"]
> <span data-ttu-id="13fb9-115">[이전](part-7.md)
> [다음](part-9.md)</span><span class="sxs-lookup"><span data-stu-id="13fb9-115">[Previous](part-7.md)
[Next](part-9.md)</span></span>
