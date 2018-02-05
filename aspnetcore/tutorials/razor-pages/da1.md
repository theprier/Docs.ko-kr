---
title: "생성된 페이지 업데이트"
author: rick-anderson
description: "향상된 표시로 생성된 페이지를 업데이트합니다."
manager: wpickett
ms.author: riande
ms.date: 08/07/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: tutorials/razor-pages/da1
ms.openlocfilehash: a1bb1ab1e4fac9c634f4048947ac3f934af3d625
ms.sourcegitcommit: 18d1dc86770f2e272d93c7e1cddfc095c5995d9e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="update-the-generated-pages"></a>생성된 페이지 업데이트

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)

동영상 앱을 적절하게 시작했지만 프레젠테이션은 이상적이지 않습니다. 시간(아래 이미지에서 오전 12시)을 표시하지 않으려 하고 **ReleaseDate**는 **Release Date**(두 단어)이어야 합니다.

![동영상 데이터를 표시하는 크롬에서 열린 동영상 응용 프로그램](sql/_static/m55.png)

## <a name="update-the-generated-code"></a>생성된 코드 업데이트

*Models/Movie.cs* 파일을 열고 다음 코드에 표시된 강조 표시된 줄을 추가합니다.

[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie/Models/MovieDate.cs?name=snippet_1&highlight=10-11)]

빨간색 물결선 > ** 빠른 작업 및 리팩터링**을 마우스 오른쪽 단추로 클릭합니다.

  ![바로 가기 메뉴는 **> 빠른 작업 및 리팩터링**을 표시합니다.](da1/qa.png)

`using System.ComponentModel.DataAnnotations;`를 선택합니다.

  ![목록 위쪽의 System.ComponentModel.DataAnnotations 사용](da1/da.png)

  Visual Studio는 `using System.ComponentModel.DataAnnotations;`를 추가합니다.

[!INCLUDE[model1](../../includes/RP/da2.md)]

>[!div class="step-by-step"]
[이전: SQL Server LocalDB 사용](xref:tutorials/razor-pages/sql)
[검색 추가](xref:tutorials/razor-pages/search)
