---
title: "컨트롤러 메서드 및 보기"
author: rick-anderson
description: "컨트롤러 메서드, 보기 및 DataAnnotations 작업"
manager: wpickett
ms.author: riande
ms.date: 03/07/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: tutorials/first-mvc-app/controller-methods-views
ms.openlocfilehash: 200f02f9815966653b3b46918737c60d11f11d5a
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="controller-methods-and-views"></a><span data-ttu-id="3890b-103">컨트롤러 메서드 및 보기</span><span class="sxs-lookup"><span data-stu-id="3890b-103">Controller methods and views</span></span>

<span data-ttu-id="3890b-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="3890b-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="3890b-105">동영상 앱을 적절하게 시작했지만 프레젠테이션은 이상적이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3890b-105">We have a good start to the movie app, but the presentation isn't ideal.</span></span> <span data-ttu-id="3890b-106">시간(아래 이미지에서 오전 12시)을 표시하지 않으려 하고 **ReleaseDate**는 두 단어이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3890b-106">We don't want to see the time (12:00:00 AM in the image below) and **ReleaseDate** should be two words.</span></span>

![인덱스 뷰: 릴리스 날짜는 한 단어(공백 없음)이며 모든 동영상 릴리스 날짜는 오전 12시를 표시합니다.](working-with-sql/_static/m55.png)

<span data-ttu-id="3890b-108">*Models/Movie.cs* 파일을 열고 아래 표시된 강조 표시된 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3890b-108">Open the *Models/Movie.cs* file and add the highlighted lines shown below:</span></span>

[!code-csharp[Main](start-mvc/sample/MvcMovie/Models/MovieDateWithExtraUsings.cs?name=snippet_1&highlight=13-14)]

<span data-ttu-id="3890b-109">빨간색 물결선 **> 빠른 작업 및 리팩터링**을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3890b-109">Right click on a red squiggly line **> Quick Actions and Refactorings**.</span></span>

  ![바로 가기 메뉴는 **> 빠른 작업 및 리팩터링**을 표시합니다.](controller-methods-views/_static/qa.png)


<span data-ttu-id="3890b-111">`using System.ComponentModel.DataAnnotations;` 누르기</span><span class="sxs-lookup"><span data-stu-id="3890b-111">Tap `using System.ComponentModel.DataAnnotations;`</span></span>

  ![목록 위쪽의 System.ComponentModel.DataAnnotations 사용](controller-methods-views/_static/da.png)

  <span data-ttu-id="3890b-113">Visual Studio는 `using System.ComponentModel.DataAnnotations;`를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3890b-113">Visual studio adds `using System.ComponentModel.DataAnnotations;`.</span></span>

<span data-ttu-id="3890b-114">필요하지 않는 `using` 문을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="3890b-114">Let's remove the `using` statements that are not needed.</span></span> <span data-ttu-id="3890b-115">기본적으로 밝은 회색 글꼴로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3890b-115">They show up by default in a light grey font.</span></span> <span data-ttu-id="3890b-116">*Movie.cs* 파일에서 마우스 오른쪽 단추로 **> 제거 및 using 정렬**의 아무 위치나 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3890b-116">Right click anywhere in the *Movie.cs* file **> Remove and Sort Usings**.</span></span>

![제거 및 using 정렬](controller-methods-views/_static/rm.png)

<span data-ttu-id="3890b-118">업데이트된 코드:</span><span class="sxs-lookup"><span data-stu-id="3890b-118">The updated code:</span></span>

[!code-csharp[Main](./start-mvc/sample/MvcMovie/Models/MovieDate.cs?name=snippet_1)]

<!-- include start -->

[!INCLUDE[adding-model](../../includes/mvc-intro/controller-methods-views.md)]

>[!div class="step-by-step"]
<span data-ttu-id="3890b-119">[이전](working-with-sql.md)
[다음](search.md)</span><span class="sxs-lookup"><span data-stu-id="3890b-119">[Previous](working-with-sql.md)
[Next](search.md)</span></span>  
