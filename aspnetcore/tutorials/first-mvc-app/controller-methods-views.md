---
title: ASP.NET Core의 컨트롤러 메서드 및 보기
author: rick-anderson
description: ASP.NET Core에서 컨트롤러 메서드, 보기 및 DataAnnotations를 사용하는 방법을 배웁니다.
ms.author: riande
ms.date: 03/07/2017
uid: tutorials/first-mvc-app/controller-methods-views
ms.openlocfilehash: e94cb877576a68540a565225b2b3d79f9be53327
ms.sourcegitcommit: b8a2f14bf8dd346d7592977642b610bbcb0b0757
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38194016"
---
# <a name="controller-methods-and-views-in-aspnet-core"></a><span data-ttu-id="57cfb-103">ASP.NET Core의 컨트롤러 메서드 및 보기</span><span class="sxs-lookup"><span data-stu-id="57cfb-103">Controller methods and views in ASP.NET Core</span></span>

<span data-ttu-id="57cfb-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="57cfb-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="57cfb-105">동영상 앱을 적절하게 시작했지만 프레젠테이션은 이상적이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="57cfb-105">We have a good start to the movie app, but the presentation isn't ideal.</span></span> <span data-ttu-id="57cfb-106">시간(아래 이미지에서 오전 12시)을 표시하지 않으려 하고 **ReleaseDate**는 두 단어이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57cfb-106">We don't want to see the time (12:00:00 AM in the image below) and **ReleaseDate** should be two words.</span></span>

![인덱스 뷰: 릴리스 날짜는 한 단어(공백 없음)이며 모든 동영상 릴리스 날짜는 오전 12시를 표시합니다.](working-with-sql/_static/m55.png)

<span data-ttu-id="57cfb-108">*Models/Movie.cs* 파일을 열고 아래 표시된 강조 표시된 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="57cfb-108">Open the *Models/Movie.cs* file and add the highlighted lines shown below:</span></span>

::: moniker range=">= aspnetcore-2.1"
[!code-csharp[](start-mvc/sample/MvcMovie21/Models/MovieDateFixed.cs?name=snippet_1&highlight=2,3,12-13,17)]
::: moniker-end
::: moniker range="<= aspnetcore-2.0"
[!code-csharp[](start-mvc/sample/MvcMovie/Models/MovieDateWithExtraUsings.cs?name=snippet_1&highlight=13-14)]
::: moniker-end

[!INCLUDE [adding-model](~/includes/mvc-intro/controller-methods-views.md)]

> [!div class="step-by-step"]
> <span data-ttu-id="57cfb-109">[이전](working-with-sql.md)
> [다음](search.md)</span><span class="sxs-lookup"><span data-stu-id="57cfb-109">[Previous](working-with-sql.md)
[Next](search.md)</span></span>  
