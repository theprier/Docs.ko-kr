---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/deleting-data
title: ASP.NET 웹 페이지 소개-데이터베이스 데이터를 삭제 합니다. | Microsoft Docs
author: tfitzmac
description: 이 자습서에서는 개별 데이터베이스 항목을 삭제 하는 방법을 보여 줍니다. 이 ASP.NET 웹 Pa.에서 데이터베이스 데이터 업데이트를 통해 시리즈를 완료 했다고 가정...
ms.author: riande
ms.date: 01/02/2018
ms.assetid: 75b5c1cf-84bd-434f-8a86-85c568eb5b09
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/deleting-data
msc.type: authoredcontent
ms.openlocfilehash: 3b759a5c88b066640005c823ce0cc3cc3ac89bc2
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41838783"
---
<a name="introducing-aspnet-web-pages---deleting-database-data"></a>ASP.NET 웹 페이지 소개-데이터베이스 데이터 삭제
====================
[Tom FitzMacken](https://github.com/tfitzmac)

> 이 자습서에서는 개별 데이터베이스 항목을 삭제 하는 방법을 보여 줍니다. 통해 시리즈를 완료 했다고 가정 하 [ASP.NET 웹 페이지에서 데이터베이스 데이터 업데이트](updating-data.md)합니다.
> 
> 학습할 내용:
> 
> - 레코드의 목록에서 개별 레코드를 선택 하는 방법입니다.
> - 데이터베이스에서 단일 레코드를 삭제 하는 방법.
> - 형태로 특정 단추 클릭을 확인 하는 방법입니다.
>   
> 
> 기능/기술을 설명 합니다.
> 
> - `WebGrid` 도우미입니다.
> - SQL `Delete` 명령입니다.
> - 합니다 `Database.Execute` SQL을 실행 하는 방법 `Delete` 명령입니다.


## <a name="what-youll-build"></a>만들 내용

이전 자습서에서는 기존 데이터베이스 레코드를 업데이트 하는 방법을 알아보았습니다. 이 자습서는 마찬가지로 점을 제외 하 고 레코드를 업데이트 하는 대신 하면 삭제 됩니다. 프로세스는 동일 하며 점을 제외 하 고 삭제 하는이 자습서 짧은 이므로 더 간단 합니다.

에 *영화* 에서는 업데이트 페이지는 `WebGrid` 도우미를 표시 하도록를 **삭제** 함께 각 영화 옆에 있는 링크를 **편집** 이전에 추가한 링크.

![각 영화에 대 한 삭제 링크를 보여 주는 동영상 페이지](deleting-data/_static/image1.png)

편집 마찬가지로 클릭할 때 합니다 **삭제** 링크 걸리는 다른 페이지에 있는 영화 정보를 이미 형식에서:

![영화 표시를 사용 하 여 동영상 페이지 삭제](deleting-data/_static/image2.png)

레코드를 영구적으로 삭제 단추를 클릭할 수 있습니다.

## <a name="adding-a-delete-link-to-the-movie-listing"></a>영화 목록에 삭제 링크를 추가합니다.

추가 하 여 먼저를 **삭제할** 연결할를 `WebGrid` 도우미입니다. 이 링크는 비슷합니다는 **편집** 이전 자습서에서 추가한 링크 합니다.

엽니다는 *Movies.cshtml* 파일입니다.

변경 된 `WebGrid` 열을 추가 하 여 페이지의 본문에는 태그입니다. 수정 된 태그는 다음과 같습니다.

[!code-html[Main](deleting-data/samples/sample1.html?highlight=9-10)]

새 열이이 같습니다.

[!code-html[Main](deleting-data/samples/sample2.html)]

표를 구성 하는 방법은 합니다 **편집** 열은 표의 맨 왼쪽 및 **삭제** 열이 오른쪽에 있는 합니다. (뒤에 나오는 쉼표는는 `Year` 열 이제는 확인 하지 않은 경우.) 이러한 링크 열으로 이동 하는 방법에 대 한 특별 하 고 서로 옆에 쉽게 배치할 수 있습니다. 이 경우 혼합 하기가 있도록 별도 일입니다.

![편집 및 세부 정보 링크를 사용 하 여 영화 페이지가 표시 되지 않았다고 서로 옆에 표시 하려면](deleting-data/_static/image3.png)

새 열의 링크를 보여 줍니다 (`<a>` 요소) "삭제" 이라고 표시 된 합니다. 링크의 대상 (해당 `href` 특성)은 사용 하 여이 URL 같이 궁극적으로 확인 되는 코드는 `id` 각 영화에 대 한 다른 값:

[!code-css[Main](deleting-data/samples/sample3.css)]

이 링크는 라는 페이지를 호출 *DeleteMovie* 선택한 영화 ID를 전달 합니다.

이 자습서 다루지는이 링크를 생성 하는 방법에 대 한 정보는 거의 동일 하기 때문에 합니다 **편집** 이전 자습서에서 링크 ([ASP.NET 웹 페이지에서 데이터베이스 데이터 업데이트](updating-data.md)).

## <a name="creating-the-delete-page"></a>삭제 페이지 만들기

이제의 대상이 될 페이지를 만들 수는 **삭제** 표에 링크 합니다.

> [!NOTE] 
> 
> **중요 한** 을 먼저 삭제할 레코드를 선택 하 고 다음 단추를 별도 페이지 확인 프로세스를 사용 하는 방법은 보안을 위해 매우 중요 합니다. 이전 자습서에서 읽었다고으로 만드는 *모든* 종류의 웹 사이트를 변경 해야 *항상* 수행 폼을 사용 하 여 &mdash; 즉, HTTP POST 작업을 사용 하 여 합니다. 변경한 링크 (사용 하 여 가져오기 작업을)를 클릭 하 여 사이트를 변경할 수, 사용자 사이트에 대 한 간단한 요청할 수 고 데이터를 삭제 합니다. 가 사이트를 인덱싱하는 검색 엔진 크롤러도 다음 링크 하 여 데이터를 실수로 삭제할 수 없습니다.
> 
> 레코드를 변경 하는 사람에 게 앱을 계속 편집에 대 한 사용자에 게 레코드를 표시 해야 합니다. 하지만 단일 레코드 삭제에 대해이 단계를 건너뛸 수 있습니다. 그러나 해당 단계를 건너뜁니다 하지 마십시오. (유용도 사용자가 레코드를 참조 하 여 이러한 레코드를 삭제 하는 것을 확인 합니다.)
> 
> 후속 자습서 집합에서 사용자가 레코드를 삭제 하기 전에 로그인 해야 하므로 로그인 기능을 추가 하는 방법을 배웁니다.


라는 페이지를 만듭니다 *DeleteMovie.cshtml* 다음 태그를 사용 하 여 파일에 포함 된 내용으로 바꿉니다.

[!code-cshtml[Main](deleting-data/samples/sample4.cshtml)]

이 태그와 비슷합니다는 *EditMovie* 텍스트 상자를 사용 하는 대신 페이지 (`<input type="text">`), 태그 `<span>` 요소입니다. 아무것도 편집할 수 있습니다. 사용자는 오른쪽 동영상을 삭제 하는 않는지 확인 수 있도록 영화 세부 정보를 표시 하면 됩니다.

태그는 사용자가 영화 목록 페이지에 반환할 수 있는 링크가 이미 있습니다.

에서처럼 합니다 *EditMovie* 페이지에서 선택한 동영상의 ID는 숨겨진된 필드에 저장 됩니다. (전달 됩니다 페이지에 처음에 쿼리 문자열 값으로.) `Html.ValidationSummary` 유효성 검사 오류를 표시 하는 호출 합니다. 이 경우 오류는 영화 ID가 없습니다. 페이지에 전달한 또는 영화 ID 올바르지 않습니다 수 있습니다. 누군가가에서 동영상을 먼저 선택 하지 않고이 페이지를 실행 하는 경우이 상황이 발생할 수는 *영화* 페이지입니다.

단추 캡션이 **삭제 영화**, 해당 이름 특성은로 설정 하 고 `buttonDelete`입니다. `name` 특성은 양식을 제출 하는 단추를 식별 하는 코드에서 사용 됩니다.

1) 페이지를 처음 표시할 때 영화 세부 정보를 읽는 코드를 작성 하 고 2) 실제로 사용자가 단추를 클릭할 때 동영상을 삭제 해야 합니다.

## <a name="adding-code-to-read-a-single-movie"></a>단일 동영상을 읽는 코드를 추가 합니다.

맨 위에 있는 합니다 *DeleteMovie.cshtml* 페이지에서 다음 코드 블록을 추가 합니다.

[!code-cshtml[Main](deleting-data/samples/sample5.cshtml)]

이 태그에 해당 하는 코드와 동일 합니다 *EditMovie* 페이지입니다. 쿼리 문자열에서 영화 ID를 가져옵니다 하 고 ID를 사용 하 여 데이터베이스에서 레코드를 읽을 수 있습니다. 유효성 검사 테스트를 포함 하는 코드 (`IsInt()` 및 `row != null`) 페이지에 전달 되는 영화 ID가 올바른지 확인 합니다.

이 코드 페이지 실행 처음으로 실행 해야만 기억 합니다. 클릭할 때 데이터베이스에서 동영상 레코드를 다시 읽을 않으려는 합니다 **영화 삭제** 단추입니다. 테스트 라는 내부 영화를 읽을 수 있으므로 코드 `if(!IsPost)` &mdash; 이므로 *요청은 post 작업이 (폼 제출) 하는 경우*합니다.

## <a name="adding-code-to-delete-the-selected-movie"></a>선택한 동영상을 삭제 하는 코드를 추가 합니다.

파일을 사용자가 단추를 클릭할 때 동영상을 삭제 하려면의 닫는 중괄호 바로 안에 다음 코드를 추가 합니다 `@` 블록:

[!code-csharp[Main](deleting-data/samples/sample6.cs)]

이 코드는 기존 레코드를 업데이트 하는 것에 대 한 코드와 유사 하지만 더 간단 합니다. 이 코드는 기본적으로 SQL 실행 `Delete` 문입니다.

 에서처럼 합니다 *EditMovie* 코드는 페이지는 `if(IsPost)` 블록입니다. 이 이번에는 `if()` 조건은 좀 더 복잡 합니다. 

[!code-csharp[Main](deleting-data/samples/sample7.cs)]

두 조건을 여기 있습니다. 첫 번째 페이지가 제출 되는 전에 살펴본 것 처럼 됩니다 &mdash; `if(IsPost)`합니다.

두 번째 조건은 `!Request["buttonDelete"].IsEmpty()`, 즉 요청 라는 개체에 `buttonDelete`입니다. 사실 어떤 단추 양식을 제출 테스트는 간접 방법입니다. 여러 전송 단추를 포함 하는 경우 요청에서 클릭 된 단추의 이름만 표시 됩니다. 따라서, 논리적으로 특정 단추의 이름을 요청 하는 경우 나타나는 &mdash; 단추를 비어 있지 않은 경우 코드에 명시 된 대로 또는 &mdash; 양식을 제출 하는 단추입니다.

`&&` 연산자 의미 "및" (논리적 AND). 따라서 전체 `if` 조건은...

*이 요청은 post (처음 요청 될 수는 없음)*  
  
 AND  
  
*합니다* `buttonDelete` *단추 된 양식을 제출 하는 단추가 있습니다.*

(사실,이 페이지)이이 폼에는 단추 하나만 있으므로 대 한 추가 테스트 `buttonDelete` 기술적으로 필요 하지 않습니다. 그러나 하려는 데이터를 영구적으로 제거 하는 작업을 수행 합니다. 따라서 사용자가 명시적으로 요청 하는 경우에 작업을 수행 하는 가능한 해야 하려고 합니다. 예를 들어 나중에이 페이지를 확장 하 여 다른 단추를 추가 합니다. 경우에 동영상을 삭제 하는 코드를 실행 하는 경우에는 `buttonDelete` 단추를 클릭 합니다.

에서처럼 합니다 *EditMovie* 페이지 ID에서 숨겨진된 필드를 얻고 다음 SQL 명령을 실행 합니다. 구문은 `Delete` 문은:

`DELETE FROM table WHERE ID = value`

포함 하는 중요 한 것은 `WHERE` 절 및 ID WHERE 절을 생략 하면 *테이블의 모든 레코드가 삭제 됩니다*합니다. 앞에서 설명한 것 처럼 전달 ID 값을 SQL 명령 자리 표시자를 사용 하 여 합니다.

## <a name="testing-the-movie-delete-process"></a>영화 삭제 프로세스를 테스트합니다.

이제 테스트할 수 있습니다. 실행 합니다 *영화* 페이지 및 클릭 **삭제** 동영상 옆에 있는 합니다. 경우는 *DeleteMovie* 페이지에 표시 되 면 클릭 **영화 삭제**합니다.

![영화 삭제 단추가 강조 표시 된 동영상 페이지 삭제](deleting-data/_static/image4.png)

단추를 클릭 하면 코드는 영화를 삭제 하 고 동영상 목록을 반환 합니다. 삭제 된 영화를 검색할 수 있는 삭제 되었는지 확인 합니다.

## <a name="coming-up-next"></a>다음에 나오는

다음 자습서는 일반적인 모양과 레이아웃 사이트에서 모든 페이지를 제공 하는 방법을 보여 줍니다.

## <a name="complete-listing-for-movie-page-updated-with-delete-links"></a>동영상 페이지 (삭제 링크를 사용 하 여 업데이트)에 대 한 전체 목록

[!code-cshtml[Main](deleting-data/samples/sample8.cshtml)]

## <a name="complete-listing-for-deletemovie-page"></a>DeleteMovie 페이지에 대 한 전체 목록

[!code-cshtml[Main](deleting-data/samples/sample9.cshtml)]

## <a name="additional-resources"></a>추가 리소스

- [Razor 구문을 사용 하 여 ASP.NET 웹 프로그래밍 소개](../introducing-razor-syntax-c.md)
- [SQL DELETE 문을](http://www.w3schools.com/sql/sql_delete.asp) W3Schools 사이트

> [!div class="step-by-step"]
> [이전](updating-data.md)
> [다음](layouts.md)
