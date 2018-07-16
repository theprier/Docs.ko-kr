---
title: ASP.NET Core 앱에서 생성된 페이지 업데이트
author: rick-anderson
description: ASP.NET Core 앱에서 생성된 페이지를 업데이트하는 방법을 알아봅니다.
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.date: 05/30/2018
uid: tutorials/razor-pages/da1
ms.openlocfilehash: 55ff98712da314e28e50a1b1b1e04530d5b3fedd
ms.sourcegitcommit: b8a2f14bf8dd346d7592977642b610bbcb0b0757
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38186233"
---
# <a name="update-the-generated-pages-in-an-aspnet-core-app"></a><span data-ttu-id="7246f-103">ASP.NET Core 앱에서 생성된 페이지 업데이트</span><span class="sxs-lookup"><span data-stu-id="7246f-103">Update the generated pages in an ASP.NET Core app</span></span>

<span data-ttu-id="7246f-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="7246f-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="7246f-105">동영상 앱을 적절하게 시작했지만 프레젠테이션은 이상적이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7246f-105">We have a good start to the movie app, but the presentation isn't ideal.</span></span> <span data-ttu-id="7246f-106">시간(아래 이미지에서 오전 12시)을 표시하지 않으려 하고 **ReleaseDate**는 **Release Date**(두 단어)이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7246f-106">We don't want to see the time (12:00:00 AM in the image below) and **ReleaseDate** should be **Release Date** (two words).</span></span>

![동영상 데이터를 표시하는 크롬에서 열린 동영상 응용 프로그램](sql/_static/m55.png)

## <a name="update-the-generated-code"></a><span data-ttu-id="7246f-108">생성된 코드 업데이트</span><span class="sxs-lookup"><span data-stu-id="7246f-108">Update the generated code</span></span>

<span data-ttu-id="7246f-109">*Models/Movie.cs* 파일을 열고 다음 코드에 표시된 강조 표시된 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7246f-109">Open the *Models/Movie.cs* file and add the highlighted lines shown in the following code:</span></span>

::: moniker range="= aspnetcore-2.0"
[!code-csharp[](~/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Models/MovieDate.cs?name=snippet_1&highlight=10-11)]
::: moniker-end

::: moniker range=">= aspnetcore-2.1"
[!code-csharp[](~/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie21/Models/MovieDate.cs?name=snippet_1&highlight=10-11,15)]
::: moniker-end

<span data-ttu-id="7246f-110">빨간색 물결선 > **빠른 작업 및 리팩터링**을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7246f-110">Right click on a red squiggly line > **Quick Actions and Refactorings**.</span></span>

  ![바로 가기 메뉴는 **> 빠른 작업 및 리팩터링**을 표시합니다.](da1/qa.png)

<span data-ttu-id="7246f-112">`using System.ComponentModel.DataAnnotations;`를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7246f-112">Select `using System.ComponentModel.DataAnnotations;`</span></span>

  ![목록 위쪽의 System.ComponentModel.DataAnnotations 사용](da1/da.png)

  <span data-ttu-id="7246f-114">Visual Studio는 `using System.ComponentModel.DataAnnotations;`를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7246f-114">Visual studio adds `using System.ComponentModel.DataAnnotations;`.</span></span>

[!INCLUDE [model1](~/includes/RP/da2.md)]

> [!div class="step-by-step"]
> <span data-ttu-id="7246f-115">[이전: SQL Server LocalDB 작업](xref:tutorials/razor-pages/sql)
> [검색 추가](xref:tutorials/razor-pages/search)</span><span class="sxs-lookup"><span data-stu-id="7246f-115">[Previous: Working with SQL Server LocalDB](xref:tutorials/razor-pages/sql)
[Add search](xref:tutorials/razor-pages/search)</span></span>
