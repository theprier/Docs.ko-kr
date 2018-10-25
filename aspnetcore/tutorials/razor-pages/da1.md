---
title: ASP.NET Core 앱에서 생성된 페이지 업데이트
author: rick-anderson
description: ASP.NET Core 앱에서 생성된 페이지를 업데이트하는 방법을 알아봅니다.
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.date: 05/30/2018
uid: tutorials/razor-pages/da1
ms.openlocfilehash: 7633c0a40764cc18a656f0497e3280e4067cb59f
ms.sourcegitcommit: 317f9be24db600499e79d25872d743af74bd86c0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48045577"
---
# <a name="update-the-generated-pages-in-an-aspnet-core-app"></a>ASP.NET Core 앱에서 생성된 페이지 업데이트

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)

동영상 앱을 적절하게 시작했지만 프레젠테이션은 이상적이지 않습니다. 시간(아래 이미지에서 오전 12시)을 표시하지 않으려 하고 **ReleaseDate**는 **Release Date**(두 단어)이어야 합니다.

![동영상 데이터를 표시하는 크롬에서 열린 동영상 응용 프로그램](sql/_static/m55.png)

## <a name="update-the-generated-code"></a>생성된 코드 업데이트

*Models/Movie.cs* 파일을 열고 다음 코드에 표시된 강조 표시된 줄을 추가합니다.

::: moniker range="= aspnetcore-2.0"

[!code-csharp[](~/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Models/MovieDate.cs?name=snippet_1&highlight=10-11)]

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](~/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie21/Models/MovieDate.cs?name=snippet_1&highlight=10-11,15)]

::: moniker-end

빨간색 물결선 > **빠른 작업 및 리팩터링**을 마우스 오른쪽 단추로 클릭합니다.

  ![바로 가기 메뉴는 **> 빠른 작업 및 리팩터링**을 표시합니다.](da1/qa.png)

`using System.ComponentModel.DataAnnotations;`를 선택합니다.

  ![목록 위쪽의 System.ComponentModel.DataAnnotations 사용](da1/da.png)

  Visual Studio는 `using System.ComponentModel.DataAnnotations;`를 추가합니다.

[!INCLUDE [model1](~/includes/RP/da2.md)]

> [!div class="step-by-step"]
> [이전: SQL Server LocalDB 작업](xref:tutorials/razor-pages/sql)
> [검색 추가](xref:tutorials/razor-pages/search)
