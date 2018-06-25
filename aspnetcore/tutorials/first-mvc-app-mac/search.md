---
title: ASP.NET Core MVC 앱에 검색 추가
author: rick-anderson
description: 간단한 ASP.NET Core MVC 앱에 검색을 추가하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 04/07/2017
uid: tutorials/first-mvc-app-mac/search
ms.openlocfilehash: 4175d4dfd03d173f7025aff3b51d255bb1c213ee
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36274484"
---
[!INCLUDE [adding-model](../../includes/mvc-intro/search1.md)]

<span data-ttu-id="4728b-103">참고: SQLlite는 대소문자를 구분하기 때문에 "ghost"가 아닌 "Ghost"에 대해 검색해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4728b-103">Note: SQLlite is case sensitive, so you'll need to search for "Ghost" and not "ghost".</span></span>

[!INCLUDE [adding-model](../../includes/mvc-intro/search2.md)]

<span data-ttu-id="4728b-104">*Views\movie\Index.cshtml* Razor 보기에서 `<form>` 태그를 `method="get"`을 지정하도록 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="4728b-104">Change the `<form>` tag in the *Views\movie\Index.cshtml* Razor view to specify `method="get"`:</span></span>

```html
<form asp-controller="Movies" asp-action="Index" method="get">
```

[!INCLUDE [adding-model](../../includes/mvc-intro/search3.md)]

> [!div class="step-by-step"]
> <span data-ttu-id="4728b-105">[이전 - 컨트롤러 메서드 및 보기](controller-methods-views.md)
> [다음 - 필드 추가](new-field.md)</span><span class="sxs-lookup"><span data-stu-id="4728b-105">[Previous - Controller methods and views](controller-methods-views.md)
[Next - Add a field](new-field.md)</span></span>
