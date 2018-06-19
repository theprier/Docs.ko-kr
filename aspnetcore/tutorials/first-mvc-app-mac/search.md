---
title: ASP.NET Core MVC 앱에 검색 추가
author: rick-anderson
description: 간단한 ASP.NET Core MVC 앱에 검색을 추가하는 방법을 보여 줍니다.
manager: wpickett
ms.author: riande
ms.date: 04/07/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: tutorials/first-mvc-app-mac/search
ms.openlocfilehash: 3f648bc6c6d095b9fe8b6ac65bf5f51741938ed1
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30894790"
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
