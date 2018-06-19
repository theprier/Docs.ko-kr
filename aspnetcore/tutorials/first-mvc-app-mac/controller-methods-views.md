---
title: ASP.NET Core MVC 앱에서 컨트롤러 메서드 및 보기
author: rick-anderson
description: 컨트롤러 메서드, 보기 및 DataAnnotations 작업
manager: wpickett
ms.author: riande
ms.date: 04/07/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: tutorials/first-mvc-app-mac/controller-methods-views
ms.openlocfilehash: 7a6a965d99742e7e06e6da82999dc60264cac6c8
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30897880"
---
# <a name="controller-methods-and-views-in-an-aspnet-core-mvc-app"></a>ASP.NET Core MVC 앱에서 컨트롤러 메서드 및 보기

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)

동영상 앱을 적절하게 시작했지만 프레젠테이션은 이상적이지 않습니다. 시간(다음 이미지에서 오전 12시)을 표시하지 않으려 하고 **ReleaseDate**는 두 단어이어야 합니다.

![인덱스 뷰: 릴리스 날짜는 한 단어(공백 없음)이며 모든 동영상 릴리스 날짜는 오전 12시를 표시합니다.](../../tutorials/first-mvc-app/working-with-sql/_static/m55.png)

*Models/Movie.cs* 파일을 열고 아래 표시된 강조 표시된 줄을 추가합니다.

[!code-csharp[](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Models/MovieDate.cs?name=snippet_1&highlight=2,11-12)]

앱을 빌드하고 실행합니다.

<!-- include start
![MVC Movie application open browser showing movie data](../../tutorials/first-mvc-app/working-with-sql/_static/m55.png)

 -->

[!INCLUDE [adding-model](../../includes/mvc-intro/controller-methods-views.md)]

> [!div class="step-by-step"]
> [이전 - SQLite 작업](working-with-sql.md)
> [다음 - 검색 추가](search.md)
