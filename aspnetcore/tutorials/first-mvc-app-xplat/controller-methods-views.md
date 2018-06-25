---
title: ASP.NET Core의 컨트롤러 메서드 및 보기
author: rick-anderson
description: ASP.NET Core에서 컨트롤러 메서드, 보기 및 DataAnnotations를 사용하는 방법을 배웁니다.
ms.author: riande
ms.date: 04/07/2017
uid: tutorials/first-mvc-app-xplat/controller-methods-views
ms.openlocfilehash: 7cf42807eaba356cd090a08bba9357c3ec237087
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36278442"
---
# <a name="controller-methods-and-views-in-aspnet-core"></a><span data-ttu-id="0bfde-103">ASP.NET Core의 컨트롤러 메서드 및 보기</span><span class="sxs-lookup"><span data-stu-id="0bfde-103">Controller methods and views in ASP.NET Core</span></span>

<span data-ttu-id="0bfde-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="0bfde-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="0bfde-105">동영상 앱을 적절하게 시작했지만 프레젠테이션은 이상적이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0bfde-105">We have a good start to the movie app, but the presentation isn't ideal.</span></span> <span data-ttu-id="0bfde-106">시간(아래 이미지에서 오전 12시)을 표시하지 않으려 하고 **ReleaseDate**는 두 단어이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bfde-106">We don't want to see the time (12:00:00 AM in the image below) and **ReleaseDate** should be two words.</span></span>

![인덱스 뷰: 릴리스 날짜는 한 단어(공백 없음)이며 모든 동영상 릴리스 날짜는 오전 12시를 표시합니다.](../../tutorials/first-mvc-app/working-with-sql/_static/m55.png)

<span data-ttu-id="0bfde-108">*Models/Movie.cs* 파일을 열고 아래 표시된 강조 표시된 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0bfde-108">Open the *Models/Movie.cs* file and add the highlighted lines shown below:</span></span>

[!code-csharp[](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Models/MovieDate.cs?name=snippet_1&highlight=2,11-12)]

<span data-ttu-id="0bfde-109">앱을 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0bfde-109">Build and run the app.</span></span>

<!-- include start
![MVC Movie application open browser showing movie data](../../tutorials/first-mvc-app/working-with-sql/_static/m55.png)

 -->

[!INCLUDE [adding-model](../../includes/mvc-intro/controller-methods-views.md)]

> [!div class="step-by-step"]
> <span data-ttu-id="0bfde-110">[이전 - SQLite 작업](working-with-sql.md)
> [다음 - 검색 추가](search.md)</span><span class="sxs-lookup"><span data-stu-id="0bfde-110">[Previous - Working with SQLite](working-with-sql.md)
[Next - Add search](search.md)</span></span>  
