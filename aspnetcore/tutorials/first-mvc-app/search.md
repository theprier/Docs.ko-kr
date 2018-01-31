---
title: "검색 추가"
author: rick-anderson
description: "간단한 ASP.NET Core MVC 앱에 검색을 추가하는 방법을 보여 줍니다."
manager: wpickett
ms.author: riande
ms.date: 03/07/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: tutorials/first-mvc-app/search
ms.openlocfilehash: 3ab9086275ec4c3651383c4c845e40db55f67f4c
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
[!INCLUDE[adding-model](../../includes/mvc-intro/search1.md)]

<span data-ttu-id="06cb5-103">**rename** 명령을 사용하여 `searchString` 매개 변수의 이름을 `id`로 신속하게 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06cb5-103">You can quickly rename the `searchString` parameter to `id` with the **rename** command.</span></span> <span data-ttu-id="06cb5-104">`searchString` **> Rename**을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="06cb5-104">Right click on `searchString` **> Rename**.</span></span>

![바로 가기 메뉴](search/_static/rename.png)

<span data-ttu-id="06cb5-106">이름 바꾸기 대상이 강조 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="06cb5-106">The rename targets are highlighted.</span></span>

![인덱스 ActionResult 메서드 전체에서 강조 표시된 변수를 보여 주는 코드 편집기](search/_static/rename2.png)

<span data-ttu-id="06cb5-108">매개 변수를 `id`로, `searchString`의 모든 항목을 `id`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="06cb5-108">Change the parameter to `id` and all occurrences of `searchString` change to `id`.</span></span>

![변수를 보여 주는 코드 편집기는 id로 변경되었습니다.](search/_static/rename3.png)

[!INCLUDE[adding-model](../../includes/mvc-intro/search2.md)]

<span data-ttu-id="06cb5-110">intelliSense에서 변경 내용 업데이트를 돕는 방법을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="06cb5-110">Notice how intelliSense helps us update the markup.</span></span>

![양식 요소에 대해 특성 목록에서 선택한 메서드가 있는 Intellisense 바로 가기 메뉴](search/_static/int_m.png)

![메서드 특성 목록에서 선택한 값이 있는 Intellisense 바로 가기 메뉴](search/_static/int_get.png)

<span data-ttu-id="06cb5-113">`<form>` 태그에서 눈에 띄는 글꼴을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="06cb5-113">Notice the distinctive font in the `<form>` tag.</span></span> <span data-ttu-id="06cb5-114">눈에 띄는 해당 글꼴은 [태그 도우미](../../mvc/views/tag-helpers/intro.md)에서 지원되는 태그를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="06cb5-114">That distinctive font indicates the tag is supported by [Tag Helpers](../../mvc/views/tag-helpers/intro.md).</span></span>

![자주색 텍스트가 있는 양식 태그](search/_static/th_font.png)

[!INCLUDE[adding-model](../../includes/mvc-intro/search3.md)]

>[!div class="step-by-step"]
<span data-ttu-id="06cb5-116">[이전](controller-methods-views.md)
[다음](new-field.md)</span><span class="sxs-lookup"><span data-stu-id="06cb5-116">[Previous](controller-methods-views.md)
[Next](new-field.md)</span></span>  
