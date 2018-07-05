---
title: ASP.NET Core MVC 앱에 검색 추가
author: rick-anderson
description: 간단한 ASP.NET Core MVC 앱에 검색을 추가하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 04/07/2017
uid: tutorials/first-mvc-app-xplat/search
ms.openlocfilehash: cf4fe3806b45008f48bf5f0598057552bdcfae7c
ms.sourcegitcommit: 356c8d394aaf384c834e9c90cabab43bfe36e063
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2018
ms.locfileid: "36961440"
---
[!INCLUDE [adding-model](../../includes/mvc-intro/search1.md)]

참고: SQLlite는 대소문자를 구분하기 때문에 "ghost"가 아닌 "Ghost"에 대해 검색해야 합니다.

[!INCLUDE [adding-model](../../includes/mvc-intro/search2.md)]

*Views\movie\Index.cshtml* Razor 보기에서 `<form>` 태그를 `method="get"`을 지정하도록 변경합니다.

```html
<form asp-controller="Movies" asp-action="Index" method="get">
```

[!INCLUDE [adding-model](../../includes/mvc-intro/search3.md)]

> [!div class="step-by-step"]
> [이전 - 컨트롤러 메서드 및 보기](controller-methods-views.md)
> [다음 - 필드 추가](new-field.md)  
