---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/deleting-data
title: Introducing ASP.NET 웹 페이지-데이터베이스 데이터를 삭제 합니다. | Microsoft Docs
author: tfitzmac
description: 이 자습서는 개별 데이터베이스 항목을 삭제 하는 방법을 보여 줍니다. ASP.NET 웹 Pa.에서 데이터베이스 데이터 업데이트를 통해 시리즈를 완료 했습니다.. 가정
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/02/2018
ms.topic: article
ms.assetid: 75b5c1cf-84bd-434f-8a86-85c568eb5b09
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/deleting-data
msc.type: authoredcontent
ms.openlocfilehash: 146199e862cd6fa2607671d31633476b1cb67021
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30897438"
---
<a name="introducing-aspnet-web-pages---deleting-database-data"></a>Introducing ASP.NET 웹 페이지-데이터베이스 데이터 삭제
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 자습서는 개별 데이터베이스 항목을 삭제 하는 방법을 보여 줍니다. 통해 시리즈를 완료 한 것으로 가정 [ASP.NET 웹 페이지에서 데이터베이스 데이터 업데이트](updating-data.md)합니다.
> 
> 학습 내용:
> 
> - 레코드의 목록에서 개별 레코드를 선택 하는 방법.
> - 데이터베이스에서 단일 레코드를 삭제 하는 방법.
> - 폼에 특정 단추가 클릭 되었습니다 있는지 확인 하는 방법입니다.
>   
> 
> 기능/기술을 설명 합니다.
> 
> - `WebGrid` 도우미입니다.
> - SQL `Delete` 명령입니다.
> - `Database.Execute` SQL 실행할 메서드를 `Delete` 명령입니다.


## <a name="what-youll-build"></a>만들 것인지

이전 자습서에서는 기존 데이터베이스 레코드를 업데이트 하는 방법을 알아보았습니다. 이 자습서는, 제외 하는 레코드를 업데이트 하는 대신 있습니다 삭제 하겠습니다. 프로세스는 동일 하며 점을 제외 하 고 삭제는이 자습서에서는 간단한 하므로 더 간단 합니다.

에 *동영상* 업데이트 합니다 페이지는 `WebGrid` 도우미를 표시 하도록는 **삭제** 함께 각 동영상 옆에 있는 링크는 **편집** 이전에 추가한 링크 합니다.

![각 동영상에 대 한 삭제 링크를 보여 주는 동영상 페이지](deleting-data/_static/image1.png)

편집와 마찬가지로 클릭할 때는 **삭제** 링크를 걸리는 다른 페이지로 영화 정보를 양식에 이미 여기서:

![표시 동영상으로 동영상 페이지 삭제](deleting-data/_static/image2.png)

레코드를 영구적으로 삭제 하는 단추를 클릭 수 있습니다.

## <a name="adding-a-delete-link-to-the-movie-listing"></a>영화 목록 삭제 링크를 추가합니다.

추가 하 여 시작 합니다는 **삭제** 연결할는 `WebGrid` 도우미입니다. 이 링크는 비슷합니다는 **편집** 이전 자습서에서 추가 된 링크.

열기는 *Movies.cshtml* 파일입니다.

변경 된 `WebGrid` 열을 추가 하 여 페이지의 본문에는 태그입니다. 수정 된 태그는 다음과 같습니다.

[!code-html[Main](deleting-data/samples/sample1.html?highlight=9-10)]

새 열이이 하나가:

[!code-html[Main](deleting-data/samples/sample2.html)]

눈금 구성 된 방식은 **편집** 눈금에서 가장 왼쪽 열을 및 **삭제** 맨 오른쪽 열이 있습니다. (뒤에 쉼표가 없는 `Year` 열 이제는 확인 하지 않은 경우.) 이러한 링크 열으로 이동 하는 방법에 대 한 특별 하 고 서로 인접 쉽게 넣을 수 없습니다. 이 경우 어려울 혼합 해 서 가져올 수 있도록 별도 일입니다.

![서로 인접 하지 있는 표시 하도록 편집 및 세부 정보 링크와 함께 동영상 페이지 표시](deleting-data/_static/image3.png)

새 열에 있는 링크 표시 (`<a>` 요소) 이라고 표시 된 "Delete"입니다. 링크의 대상 (해당 `href` 특성)는 궁극적으로와 같이이 URL을 확인 하는 코드는 `id` 각 동영상에 대 한 다른 값:

[!code-css[Main](deleting-data/samples/sample3.css)]

이 링크는 라는 페이지 호출 *DeleteMovie* 선택한 동영상의 ID를 전달 합니다.

이 자습서는 거의 동일 하기 때문에이 링크 생성 방법에 대 한 정보를 확인할 다루지는 않겠습니다.는 **편집** 이전 자습서의 링크 ([ASP.NET 웹 페이지에서 데이터베이스 데이터 업데이트](updating-data.md)).

## <a name="creating-the-delete-page"></a>Delete 페이지 만들기

이제의 대상이 될 페이지를 만들 수는 **삭제** 눈금에 링크 합니다.

> [!NOTE] 
> 
> **중요 한** 먼저 삭제할 레코드를 선택 하 고 다음 프로세스를 확인 하는 별도 페이지와 단추를 사용 하는 방법에는 보안에 매우 중요 합니다. 이전 자습서에서 읽은으로 만드는 *모든* 종류의 웹 사이트를 변경 해야 *항상* 수행할 수는 양식을 사용 하 여 &mdash; 즉, HTTP POST 작업을 사용 하 합니다. 변경한 (사용 하 여 가져오기 작업) 링크를 클릭 하 여 사이트를 변경할 수, 하는 경우 사용자 수 간단한 요청 사이트에 만들고 데이터를 삭제 합니다. 검색 엔진 크롤러도 사이트 인덱싱 되는 링크를 따라 데이터를 실수로 삭제 수 없습니다.
> 
> 응용 프로그램을 통해 사용자는 레코드를 변경 때 사용자에 게 계속 편집을 위해 레코드를 표시 해야 합니다. 하지만이 단계는 레코드를 삭제 하기 위한 시도할 수 있습니다. 그러나 해당 단계를 건너뛸 하지 마십시오. (이기도 한 레코드를 보고 확인 레코드를 의도 한 것을 삭제 하는 사용자에 유용 합니다.)
> 
> 이후의 자습서 집합에는 사용자가 레코드를 삭제 하기 전에 로그인 해야 하므로 로그인 기능을 추가 하는 방법을 표시 됩니다.


*DeleteMovie.cshtml* 바꾸고 다음 태그를 사용 하 여 파일에 포함 된 내용:

[!code-cshtml[Main](deleting-data/samples/sample4.cshtml)]

이 태그는 같은 *EditMovie* 텍스트 상자를 사용 하는 대신 점을 제외 하 고 페이지 (`<input type="text">`), 태그를 포함 `<span>` 요소입니다. 여기에 아무 것 편집할 수 있습니다. 사용자가 오른쪽 동영상을 삭제 하는 되는지 확인할 수 영화 세부 정보를 표시 하면 됩니다.

태그에는 이미 사용자가 동영상 목록 페이지로 돌아가 수 있는 링크가 포함 됩니다.

와 같이 *EditMovie* 페이지에서 선택한 동영상의 ID는 숨겨진된 필드에 저장 됩니다. (로 전달 됩니다 페이지에 처음에 쿼리 문자열 값입니다.) 한 `Html.ValidationSummary` 유효성 검사 오류를 표시 하는 호출 합니다. 이 경우 오류 영화 ID가 없습니다. 페이지에 전달 된 또는 영화 ID가 올바르지 않습니다 수 있습니다. 다른 사용자의 동영상을 선택 하지 않고이 페이지를 실행 한 경우이 상황이 발생할 수는 *동영상* 페이지.

단추 캡션이 **삭제 영화**, 해당 이름 특성은로 설정 하 고 `buttonDelete`합니다. `name` 특성은 양식을 제출 단추를 나타내는 코드에 사용 됩니다.

1)는 영화 세부 정보를 읽어 페이지를 처음 표시할 때 코드를 작성 하 고 2) 실제로 단추를 클릭할 때 영화를 삭제 해야 합니다.

## <a name="adding-code-to-read-a-single-movie"></a>단일 영화를 읽는 코드를 추가 합니다.

맨 위에 있는 *DeleteMovie.cshtml* 페이지에서 다음 코드 블록을 추가 합니다.

[!code-cshtml[Main](deleting-data/samples/sample5.cshtml)]

이 태그에 해당 하는 코드와 같습니다는 *EditMovie* 페이지. 쿼리 문자열에서 영화 ID를 가져오고 ID를 사용 하 여 데이터베이스에서 레코드를 읽을 수 있습니다. 코드에 유효성 검사 테스트 (`IsInt()` 및 `row != null`)를 페이지에 전달 되 고 영화 ID가 유효한 지 확인 합니다.

이 코드 페이지가 실행 되는 처음으로 실행 해야 함을 기억 합니다. 사용자가 데이터베이스에서 영화 레코드를 다시 읽을 않으려면는 **영화 삭제** 단추입니다. 따라서 테스트 라는 내부 동영상을 읽을 수 코드 `if(!IsPost)` &mdash; 즉, *요청이 post 작업 (양식 전송) 없으면*합니다.

## <a name="adding-code-to-delete-the-selected-movie"></a>선택한 동영상을 삭제 하는 코드를 추가 합니다.

사용자가 단추를 클릭할 때 영화를 삭제 하려면 바로의 닫는 중괄호 안에 다음 코드를 추가 `@` 블록:

[!code-csharp[Main](deleting-data/samples/sample6.cs)]

이 코드는 기존 레코드를 업데이트 하기 위한 코드와 유사 하지만 더 간단 합니다. 이 코드는 기본적으로 SQL 실행 `Delete` 문.

 와 같이 *EditMovie* 코드는 페이지는 `if(IsPost)` 블록입니다. 이 이번에는 `if()` 조건이 약간 더 복잡 합니다. 

[!code-csharp[Main](deleting-data/samples/sample7.cs)]

두 조건을 여기 있습니다. 첫 번째 페이지가 제출 되는 하기 전에 지금까지 살펴본 대로 &mdash; `if(IsPost)`합니다.

두 번째 조건은 `!Request["buttonDelete"].IsEmpty()`, 요청 라는 개체에 의미 `buttonDelete`합니다. 물론, 어떤 단추가 양식을 제출 테스트의 간접 방법입니다. 여러 전송 단추를 포함 하는 경우 요청에서 클릭 된 단추의의 이름만이 나타납니다. 따라서, 논리적으로 경우 요청에는 특정 단추 이름이 표시 &mdash; 해당 단추의 비어 있지 않은 경우에 코드에 명시 된 대로 또는 &mdash; 양식을 제출 하는 단추입니다.

`&&` 연산자 수단 "및" (논리적 AND). 따라서 전체 `if` 조건이...

*이 요청은 post (처음 요청 될 수는 없음)*  
  
 AND  
  
 `buttonDelete` *단추가 있던 양식을 제출 하는 단추입니다.*

(사실,이 페이지)이이 폼에는 단추 하나만 있으므로 대 한 추가 테스트 `buttonDelete` 기술적으로 필요 하지 않습니다. 아직도 하려는 데이터를 영구적으로 제거 하는 작업을 수행 합니다. 따라서 사용자가 요청 명시적으로 하는 경우에 작업을 수행 하는 가능한 반드시 하려고 합니다. 예를 들어 나중에이 페이지를 확장 하 고 여기에 다른 단추 추가 가정 합니다. 경우에 동영상을 삭제 하는 코드가 실행 되는는 `buttonDelete` 단추가 클릭 되었습니다.

와 같이 *EditMovie* 페이지 있습니다 ID에서 숨겨진된 필드를 가져오고 다음 SQL 명령을 실행 합니다. 에 대 한 구문에서 `Delete` 문이:

`DELETE FROM table WHERE ID = value`

포함을 `WHERE` 절과 id입니다. WHERE 절을 지정 하지 않을 경우 *삭제할 테이블의 모든 레코드가*합니다. 위에서 설명한 것 처럼 전달 ID 값은 SQL 명령 자리 표시자를 사용 하 여 합니다.

## <a name="testing-the-movie-delete-process"></a>영화 삭제 프로세스를 테스트합니다.

이제 테스트할 수 있습니다. 실행 된 *동영상* 페이지를 클릭 하 여 **삭제** 동영상 옆에 있는 합니다. 경우는 *DeleteMovie* 페이지에 표시 되 면 클릭 **삭제 동영상**합니다.

![영화 삭제 단추가 강조 표시 된 동영상 페이지 삭제](deleting-data/_static/image4.png)

단추를 클릭할 때 코드는 영화를 삭제 하 고 동영상 목록으로 반환 합니다. 삭제 된 영화를 검색할 수 있습니다는 삭제 된 확인 합니다.

## <a name="coming-up-next"></a>다음에 나오는

다음 자습서에서는 일반적인 모양과 레이아웃 사이트에서 모든 페이지를 제공 하는 방법을 보여 줍니다.

## <a name="complete-listing-for-movie-page-updated-with-delete-links"></a>동영상 페이지 (삭제 링크와 함께 업데이트)에 대 한 전체 목록을 보려면

[!code-cshtml[Main](deleting-data/samples/sample8.cshtml)]

## <a name="complete-listing-for-deletemovie-page"></a>DeleteMovie 페이지에 대 한 전체 목록을 보려면

[!code-cshtml[Main](deleting-data/samples/sample9.cshtml)]

## <a name="additional-resources"></a>추가 자료

- [Razor 구문을 사용 하 여 ASP.NET 웹 프로그래밍 소개](../introducing-razor-syntax-c.md)
- [SQL DELETE 문을](http://www.w3schools.com/sql/sql_delete.asp) W3Schools 사이트

> [!div class="step-by-step"]
> [이전](updating-data.md)
> [다음](layouts.md)
