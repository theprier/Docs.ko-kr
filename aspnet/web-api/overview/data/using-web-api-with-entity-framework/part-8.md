---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-8
title: 항목 세부 정보를 표시 합니다. | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/16/2014
ms.topic: article
ms.assetid: 75ef94b1-bbec-4681-9210-452dba816144
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-8
msc.type: authoredcontent
ms.openlocfilehash: 94863e94f2a8b3f1ce8a8fb85d877bc0768f3d8a
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30868089"
---
<a name="display-item-details"></a><span data-ttu-id="9573e-102">항목 세부 정보를 표시</span><span class="sxs-lookup"><span data-stu-id="9573e-102">Display Item Details</span></span>
====================
<span data-ttu-id="9573e-103">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="9573e-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="9573e-104">완료 된 프로젝트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="9573e-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="9573e-105">이 섹션에서는 각 책에 대 한 세부 정보를 볼 수 있는 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9573e-105">In this section, you will add the ability to view details for each book.</span></span> <span data-ttu-id="9573e-106">App.js의 보기 모델에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9573e-106">In app.js, add to the following code to the view model:</span></span>

[!code-javascript[Main](part-8/samples/sample1.js)]

<span data-ttu-id="9573e-107">Views/Home/Index.cshtml에서 세부 정보 링크에는 데이터를 바인딩 요소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9573e-107">In Views/Home/Index.cshtml, add a data-bind element to the Details link:</span></span>

[!code-html[Main](part-8/samples/sample2.html?highlight=5)]

<span data-ttu-id="9573e-108">이 대 한 클릭 처리기를 바인딩하는 &lt;는&gt; 요소를는 `getBookDetail` 의 보기 모델에 대해 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="9573e-108">This binds the click handler for the &lt;a&gt; element to the `getBookDetail` function on the view model.</span></span>

<span data-ttu-id="9573e-109">동일한 파일에서 다음과 같은 마크업을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9573e-109">In the same file, replace the following mark-up:</span></span>

[!code-html[Main](part-8/samples/sample3.html)]

<span data-ttu-id="9573e-110">다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9573e-110">with this:</span></span>

[!code-html[Main](part-8/samples/sample4.html)]

<span data-ttu-id="9573e-111">이 태그의 속성에 데이터 바인딩된 하는 테이블을 만듭니다는 `detail` 보기 모델에 예측 가능한 합니다.</span><span class="sxs-lookup"><span data-stu-id="9573e-111">This markup creates a table that is data-bound to the properties of the `detail` observable in the view model.</span></span>

<span data-ttu-id="9573e-112">"&lt;!-ko-&gt; &quot; 구문을 사용 하면 DOM 요소의 외부 Knockout 바인딩을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9573e-112">The "&lt;!-- ko --&gt;&quot; syntax lets you include a Knockout binding outside of a DOM element.</span></span> <span data-ttu-id="9573e-113">이 경우에 `if` 바인딩 표시 되는 태그의이 섹션에서는 경우에만 `details` null입니다.</span><span class="sxs-lookup"><span data-stu-id="9573e-113">In this case, the `if` binding causes this section of markup to be displayed only when `details` is non-null.</span></span>

[!code-html[Main](part-8/samples/sample5.html)]

<span data-ttu-id="9573e-114">응용 프로그램을 실행 중 하나를 클릭 하는 경우 이제는 &quot;세부&quot; 링크, 응용 프로그램에는 책 세부 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9573e-114">Now if you run the app and click one of the &quot;Detail&quot; links, the app will display the book details.</span></span>

[![](part-8/_static/image2.png)](part-8/_static/image1.png)

> [!div class="step-by-step"]
> <span data-ttu-id="9573e-115">[이전](part-7.md)
> [다음](part-9.md)</span><span class="sxs-lookup"><span data-stu-id="9573e-115">[Previous](part-7.md)
[Next](part-9.md)</span></span>
