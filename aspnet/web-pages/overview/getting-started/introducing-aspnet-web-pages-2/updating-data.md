---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/updating-data
title: ASP.NET 웹 페이지 소개-데이터베이스 데이터를 업데이트 하는 중 | Microsoft Docs
author: tfitzmac
description: 이 자습서에서는 ASP.NET Web Pages (Razor)를 사용 하는 경우 기존 데이터베이스 (변경) 항목을 업데이트 하는 방법을 보여 줍니다. 시리즈를 완료 했다고 가정 하기 번째...
ms.author: riande
ms.date: 01/02/2018
ms.assetid: ac86ec9c-6b69-485b-b9e0-8b9127b13e6b
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/updating-data
msc.type: authoredcontent
ms.openlocfilehash: 9d0da2eed9964e56a01f3c811d6a14c9d1735e10
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824145"
---
<a name="introducing-aspnet-web-pages---updating-database-data"></a>ASP.NET 웹 페이지 소개-데이터베이스 데이터를 업데이트 하는 중
====================
[Tom FitzMacken](https://github.com/tfitzmac)

> 이 자습서에서는 ASP.NET Web Pages (Razor)를 사용 하는 경우 기존 데이터베이스 (변경) 항목을 업데이트 하는 방법을 보여 줍니다. 통해 시리즈를 완료 했다고 가정 하 [입력 데이터에서 사용 하 여 Forms를 사용 하 여 ASP.NET 웹 페이지](entering-data.md)합니다.
> 
> 학습할 내용:
> 
> - 개별 레코드를 선택 하는 방법의 `WebGrid` 도우미입니다.
> - 데이터베이스에서 단일 레코드를 읽는 방법.
> - 데이터베이스 레코드의 값을 사용 하 여 폼을 미리 로드 하는 방법입니다.
> - 데이터베이스의 기존 레코드를 업데이트 하는 방법.
> - 페이지에 표시 하지 않고 정보를 저장 하는 방법.
> - 숨겨진된 필드를 사용 하 여 정보를 저장 하는 방법.
>   
> 
> 기능/기술을 설명 합니다.
> 
> - `WebGrid` 도우미입니다.
> - SQL `Update` 명령입니다.
> - `Database.Execute` 메서드
> - 숨겨진 필드 (`<input type="hidden">`).


## <a name="what-youll-build"></a>만들 내용

이전 자습서에서는 데이터베이스에 레코드를 추가 하는 방법을 알아보았습니다. 여기에서 편집에 대 한 레코드를 표시 하는 방법에 알아봅니다. 에 *영화* 에서는 업데이트 페이지는 `WebGrid` 도우미를 표시 하도록는 **편집** 각 영화 옆에 있는 링크:

![WebGrid 각 영화에 대 한 '편집' 링크를 포함 하 여 표시](updating-data/_static/image1.png)

클릭할 때 합니다 **편집** 링크 걸리는 다른 페이지에 있는 영화 정보를 이미 형식에서:

![편집을 편집할 수는 동영상을 보여 주는 동영상 페이지](updating-data/_static/image2.png)

값 중 하나를 변경할 수 있습니다. 변경 내용을 제출 하면 코드 페이지에서 데이터베이스를 업데이트 하 고 영화 목록으로 돌아갑니다.

이 부분의 프로세스와 거의 똑같이 작동 합니다 *AddMovie.cshtml* 되도록이 자습서의 대부분 친숙 한 이전 자습서에서 만든 페이지입니다.

여러 가지 방법으로 개별 영화를 편집 하는 기능을 구현할 수 있습니다. 표시 된 접근 방식은 구현 하기 쉽고 이해 하기 쉬운 이기 때문에 선택 되었습니다.

## <a name="adding-an-edit-link-to-the-movie-listing"></a>영화 목록에는 편집 링크 추가

업데이트에서는 시작 하는 *영화* 각 영화 목록도 포함 되도록 페이지는 **편집** 링크 합니다.

엽니다는 *Movies.cshtml* 파일입니다.

페이지의 본문에서 변경 된 `WebGrid` 열을 추가 하 여는 태그입니다. 수정 된 태그는 다음과 같습니다.

[!code-html[Main](updating-data/samples/sample1.html?highlight=6)]

새 열이이 같습니다.

[!code-html[Main](updating-data/samples/sample2.html)]

이 칼럼의 지점 링크를 표시 하는 것 (`<a>` 요소) "편집" 이라고 표시 된 합니다. 연결 페이지를 실행 하는 경우 다음과 같이 표시 되는 링크를 만들 때 살펴볼 항목으로 `id` 각 영화에 대 한 다른 값:

[!code-css[Main](updating-data/samples/sample3.css)]

이 링크는 라는 페이지를 호출 *EditMovie*, 및 쿼리 문자열을 전달 합니다 `?id=7` 해당 페이지에 있습니다.

새 열에 대 한 구문을 약간 복잡 한 보이지만 몇 가지 요소 모아놓은 때문에 합니다. 각 개별 요소는 간단 합니다. 에 집중 하는 경우만 `<a>` 요소인이이 태그를 표시 합니다.

[!code-html[Main](updating-data/samples/sample4.html)]

눈금의 작동 원리에 대 한 몇 가지 배경 지식을: 표에 각 데이터베이스 레코드에 대해 하나의 행을 표시 하 고 데이터베이스 레코드의 각 필드에 대 한 열을 표시 하는 것입니다. 각 표 형태 창의 행 생성 되는 동안는 `item` 개체에 해당 행에 대 한 데이터베이스 레코드가 (항목)를 포함 합니다. 이 배열에서 해당 행에 대 한 데이터는 코드에서는 방법을 제공 합니다. 여기는: 식 `item.ID` 현재 데이터베이스 항목의 ID 값을 가져오고 됩니다. 얻을 수 있습니다 (제목, 장르, 또는 연도) 데이터베이스 값 동일한 방식으로 사용 하 여 `item.Title`하십시오 `item.Genre`, 또는 `item.Year`합니다.

식을 `"~/EditMovie?id=@item.ID` 대상 URL 하드 코딩 된 부분을 결합 (`~/EditMovie?id=`)이 동적으로 파생 id (살펴보았습니다는 `~` 연산자는 이전 자습서에서 현재 웹 사이트 루트를 나타내는 ASP.NET 운영자는 것입니다.)

결과 열에 있는 태그의이 부분 간단히 생성 한다는 다음 태그와 같이 런타임 시:

[!code-xml[Main](updating-data/samples/sample5.xml)]

물론 실제 값 `id` 각 행에 대해 다릅니다.

## <a name="creating-a-custom-display-for-a-grid-column"></a>표 형태 열에 대 한 표시를 사용자 지정 만들기

이제 표 형태의 열에 백업 합니다. 세 열은 원래 표가 표시만 데이터 값 (title, genre 및 연도) 했습니다. 이 표시는 데이터베이스 열의 이름을 전달 하 여 지정한 &mdash; 예를 들어 `grid.Column("Title")`합니다.

이 새로운 **편집** 링크 열 다릅니다. 열 이름을 지정 하는 대신 전달 된 `format` 매개 변수입니다. 이 매개 변수를 사용 하면 태그를 정의할 수는 합니다 `WebGrid` 도우미와 함께 렌더링 됩니다는 `item` 열 데이터 굵게 또는 녹색으로 표시 하거나 원하는 형식으로 해당 값입니다. 예를 들어, 굵게 표시 하려면 제목, 원한다 면이 예제와 같이 열을 만들 수 있습니다.

[!code-html[Main](updating-data/samples/sample6.html)]

(다양 한 `@` 에 나오는 문자는 `format` 속성 태그 및 코드 값 간에 전환을 표시 합니다.)

에 대 한 알게 되 면 합니다 `format` 이해 하기 쉽습니다 속성을 어떻게 새 **편집** 링크 열 함께 취합 하는:

[!code-html[Main](updating-data/samples/sample7.html)]

열으로 구성 됩니다 *만* 의 링크를 렌더링 하는 태그를와 일부 정보가 (ID)는에서 추출 된 행에 대 한 데이터베이스 레코드입니다.

> [!TIP]
> 
> **명명 된 매개 변수 및 메서드에 대 한 위치 매개 변수**
> 
> 여러 번 메서드를 호출 하 고 매개 변수 전달 했으므로 단순히 나열 된 쉼표로 구분 된 매개 변수 값입니다. 몇 가지 예는 다음과 같습니다.
> 
> `db.Execute(insertCommand, title, genre, year)`
> 
> `Validation.RequireField("title", "You must enter a title")`
> 
> 이 코드를 먼저 살펴본 하지만 각각의 경우에서 특정 순서로 메서드에 매개 변수를 전달 하는 경우 문제를 언급 하지 않았습니다에서는 &mdash; 즉, 메서드에 매개 변수 정의 되는 순서입니다. 에 대 한 `db.Execute` 고 `Validation.RequireFields`, 페이지를 실행 하는 경우 오류 메시지 또는 이상한 결과 이상 얻게 전달 하는 값의 순서를 혼합 하는 경우. 물론 매개 변수를 전달 하는 순서를 알고 있어야 합니다. (WebMatrix에서 IntelliSense 도움이 될 수 있습니다 이름, 형식 및 매개 변수의 순서 확인에 알아봅니다.)
> 
> 를 순서 대로 값을 전달 하는 대신 사용할 수 있습니다 *명명 된 매개 변수*합니다. (사용 하 여 이라고 순서로 매개 변수 전달 *위치 매개 변수*.) 명명 된 매개 변수에 대 한 명시적으로 포함 된 매개 변수의 이름을 해당 값을 전달 하는 경우. 명명 된 매개 변수 이미 여러 번에서에서 사용한 이러한 자습서입니다. 예를 들어:
> 
> [!code-csharp[Main](updating-data/samples/sample8.cs)]
> 
> 를 갖는
> 
> [!code-css[Main](updating-data/samples/sample9.css)]
> 
> 명명 된 매개 변수는 메서드가 여러 매개 변수를 사용 하는 경우에 특히 몇 가지 상황에서 유용 합니다. 하나 이상의 매개 변수를 전달 하려는 하지만 경우 전달 하려는 값 매개 변수 목록의 첫 번째 위치 중 하나입니다. 또 다른 상황은 매개 변수를 사용 하면 대부분의 적합 한 순서 대로 전달 하 여 코드를 더 읽기 쉽게 하려는 경우입니다.
> 
> 물론 명명 된 매개 변수를 사용 하려면 해야 매개 변수의 이름을 알고 있어야 합니다. WebMatrix IntelliSense 수 *표시* 이름, 하지만 현재을 채울 수 없습니다 하 있습니다.


## <a name="creating-the-edit-page"></a>편집 페이지 만들기

이제 만들어야 합니다 *EditMovie* 페이지입니다. 사용자가 클릭 하면 합니다 **편집** 링크는 최종적으로이 페이지에 있습니다.

라는 페이지를 만듭니다 *EditMovie.cshtml* 다음 태그를 사용 하 여 파일에 포함 된 내용으로 바꿉니다.

[!code-cshtml[Main](updating-data/samples/sample10.cshtml)]

이 태그와 코드는에 있는 비슷합니다는 *AddMovie* 페이지입니다. 제출 단추에 대 한 텍스트에 약간의 차이가 있습니다. 와 마찬가지로 합니다 *AddMovie* 페이지, 즉는 `Html.ValidationSummary` 있는 경우 유효성 검사 오류를 표시 하는 호출 합니다. 에 대 한 호출을 생략 하는 것이 시간 `Validation.Message`유효성 검사 요약에 표시할 오류 때문입니다. 이전 자습서에서 설명한 대로, 다양 한 조합에 유효성 검사 요약 및 개별 오류 메시지를 사용할 수 있습니다.

다시 있음을 합니다 `method` 특성을 `<form>` 로 설정 된 `post`합니다. 와 마찬가지로 합니다 *AddMovie.cshtml* 페이지에서이 페이지 변경 내용을 데이터베이스에 있습니다. 따라서이 폼을 수행할지를 `POST` 작업 합니다. (간의 차이점에 대 한 자세한 `GET` 및 `POST` 작업을 참조 하세요 합니다 [GET, POST 및 HTTP 동사 안전성](form-basics.md#GET,_POST,_and_HTTP_Verb_Safety) 사이드바에서 HTML 폼에 대 한 자습서입니다.)

이전 자습서에서 보았듯이 `value` 입력란의 특성을 미리 설치 하기 위해 Razor 코드를 사용 하 여 설정 되 고 있습니다. 이 시간을 사용 하는 같은 변수 `title` 하 고 `genre` 대신 해당 작업에 대 한 `Request.Form["title"]`:

`<input type="text" name="title" value="@title" />`

로 이전에이 태그는 미리 로드 동영상 값을 사용 하 여 텍스트 상자 값입니다. 편리 하 게 사용 하는 대신이 변수를 사용 하는 이유는 조금 뒤에 표시 된 `Request` 개체입니다.

또한는 `<input type="hidden">` 이 페이지의 요소입니다. 이 요소는 표시 하지 않고 페이지의 영화 ID를 저장 합니다. ID는 처음에 페이지에 전달 하 여 쿼리 문자열 값을 사용 하 여 (`?id=7` 또는 유사한 URL에서). ID 값을 숨겨진된 필드를 넣어 할 수 없습니다는 페이지를 사용 하 여 호출 된 원래 URL에 대 한 액세스를 더 이상 있는 경우에, 양식이 전송 됩니다.

와 달리 합니다 *AddMovie* 페이지에 대 한 코드를 *EditMovie* 페이지에는 두 가지 고유한 기능입니다. 첫 번째 함수는 페이지가 처음 표시 되는 경우 (및 *만* 다음), 코드 쿼리 문자열에서 영화 ID를 가져옵니다. 다음 코드를 사용 하 여 ID 데이터베이스에서 해당 영화를 읽고 표시 (미리 로드)이 텍스트 상자에 합니다.

두 번째 함수는 사용자가 클릭할 때 합니다 **변경 내용 전송** 단추 코드는 입력란의 값을 읽고 유효성을 검사할 합니다. 또한 코드를 새 값을 사용 하 여 데이터베이스 항목을 업데이트 해야 합니다. 이 방법은 추가 레코드를 유사한에서 볼 수 있듯이 *AddMovie*합니다.

## <a name="adding-code-to-read-a-single-movie"></a>단일 동영상을 읽는 코드를 추가 합니다.

첫 번째 함수를 수행 하려면이 코드 페이지의 맨 위에 추가 합니다.

[!code-cshtml[Main](updating-data/samples/sample11.cshtml)]

시작 블록 내에서이 코드의 대부분은 `if(!IsPost)`합니다. `!` 연산자 의미 "not" 식 의미 하므로 *이 요청이 post 제출 되지 않으면*는 간접 방법 설명할 *이 요청은 처음으로이 페이지를 실행 하는 경우*합니다. 이 코드를 실행 해야 앞에서 설명한 대로 *만* 처음으로 실행 됩니다. 코드를 포함 하지 않은 경우 `if(!IsPost)`는 페이지가 호출 될 때마다, 여부 처음으로 실행 또는 단추를 클릭 합니다.

코드를 포함 하는 `else` 이 이번 차단 합니다. 도입 했습니다 했 듯이 `if` 경우에 따라 테스트 하는 조건이 true 없으면 대체 코드를 실행 하려는 블록입니다. 여기서입니다. 조건 (즉, 경우 페이지에 전달 하는 ID 확인)를 통과 하는 경우 데이터베이스에서 행을 읽습니다. 그러나 조건을 통과 하지 못한 경우는 `else` 블록은 실행 및 코드 오류 메시지를 설정 합니다.

## <a name="validating-a-value-passed-to-the-page"></a>페이지에 전달 된 값의 유효성 검사

코드를 사용 하 여 `Request.QueryString["id"]` 페이지로 전달 되는 ID를 가져옵니다. 코드에서는 id 값을 실제로 전달 된 되는지 값이 전달 된 경우 코드 유효성 검사 오류를 설정 합니다.

이 코드에 정보의 유효성을 검사 하는 다른 방법을 보여 줍니다. 이전 자습서에서 사용한는 `Validation` 도우미입니다. 유효성을 검사 하는 필드를 등록 하 고 ASP.NET에서 자동으로 유효성 검사를 않았습니다 하 고 사용 하 여 오류를 표시 `Html.ValidationMessage` 고 `Html.ValidationSummary`입니다. 그러나이 경우 하는 것은 아닙니다 사용자 입력 유효성 검사. 대신 다른 곳에서 페이지에 전달 된 값의 유효성 검사 하 고 있습니다. `Validation` 도우미를 재순환 하지 않습니다.

따라서 값을 확인할 있습니다를 직접 사용 하 여 테스트 하 여 `if(!Request.QueryString["ID"].IsEmpty()`). 문제가 있으면 사용 하 여 오류를 표시할 수 있습니다 `Html.ValidationSummary`과 마찬가지로는 `Validation` 도우미입니다. 이렇게 하려면 호출 `Validation.AddFormError` 표시할 메시지를 전달 합니다. `Validation.AddFormError` 익숙한 이미 유효성 검사 시스템 사용 하 여 연결 하는 사용자 지정 메시지를 정의할 수 있는 기본 제공 메서드입니다. (이 자습서의 뒷부분에서 설명이 유효성 검사 프로세스를 좀 더 강력 하 게 하는 방법에 대 한 합니다.)

영화 ID 인지에 확인 한 후 코드는 단일 데이터베이스 항목만 찾고 데이터베이스를 읽습니다. (아마도 했을 데이터베이스 작업에 대 한 일반적인 패턴: 데이터베이스를 열고 SQL 문을 정의 하는 문을 실행 합니다.) 이 이번에는 SQL `Select` 문에 포함 되는 `WHERE ID = @0`합니다. ID가 고유 하므로 하나의 레코드를 반환할 수 있습니다.

쿼리를 사용 하 여 수행할 `db.QuerySingle` (되지 `db.Query`영화 목록에 사용한 것과,), 코드 결과를 넣습니다는 `row` 변수입니다. 이름을 `row` 임의로; 변수를 원하는 대로 이름을 지정할 수 있습니다. 맨 위에 있는 초기화 변수 텍스트 상자에 이러한 값을 표시할 수 있도록 다음 영화 세부 정보로 채워집니다.

## <a name="testing-the-edit-page-so-far"></a>편집 페이지 (지금) 테스트

페이지를 테스트 하려는 경우 실행 합니다 *영화* 이제 페이지를 클릭는 **편집** 모든 동영상 옆에 있는 링크입니다. 표시 된 *EditMovie* 선택한 영화에 대 한 세부 정보를 사용 하 여 페이지 입력:

![편집을 편집할 수는 동영상을 보여 주는 동영상 페이지](updating-data/_static/image3.png)

페이지의 URL 같이 포함 `?id=10` (또는 다른 몇 가지 번호)입니다. 테스트 했으므로 지금 **편집** 에 연결 합니다 *영화* 페이지는 페이지 ID는 쿼리 문자열에서 읽고 되 고 단일 동영상 기록을 가져오는 데이터베이스 쿼리는 작업은 작업 합니다.

영화 정보를 변경할 수 있지만 클릭할 때 아무 작업도 **변경 내용 전송**합니다.

## <a name="adding-code-to-update-the-movie-with-the-users-changes"></a>사용자의 변경 내용으로 동영상을 업데이트 하는 코드 추가

에 *EditMovie.cshtml* 파일 (변경 내용 저장) 두 번째 함수를 구현 하려면 바로의 닫는 중괄호 안에 다음 코드를 추가 합니다는 `@` 블록입니다. (보면 정확한 위치는 코드를 잘 모를 경우 합니다 [영화 편집 페이지에 대 한 목록 전체 코드](#Complete_Page_Listing_for_EditMovie) 이 자습서의 끝에 표시 되는.)

[!code-csharp[Main](updating-data/samples/sample12.cs)]

이 태그와 코드 역시의 코드와 비슷하게 *AddMovie*합니다. 코드는는 `if(IsPost)` 블록을 클릭 하는 경우에이 코드가 실행 되기 때문에 **변경 내용 전송** 단추 &mdash; 인 경우 (및 경우에만) 폼이 게시 되었습니다. 이 경우 같은 테스트를 사용 하지 않는 `if(IsPost && Validation.IsValid())`-즉, 없습니다을 결합 하는 테스트를 모두 사용 하 여 and가 있습니다. 에서는이 페이지에서는 먼저 확인 양식을 제출 하 여 인지 (`if(IsPost)`)에 다음 유효성 검사에 대 한 필드를 등록 합니다. 다음 유효성 검사 결과 테스트할 수 있습니다 (`if(Validation.IsValid()`). 흐름은 약간 변경 합니다 *AddMovie.cshtml* 페이지 다르지만 효과 동일 합니다.

사용 하 여 입력란의 값을 가져옵니다 `Request.Form["title"]` 및 다른 유사한 코드 `<input>` 요소입니다. 이 이번에 코드를 가져옴을 영화 ID 숨겨진된 필드에서 확인할 수 있습니다 (`<input type="hidden">`). 페이지가 처음으로 실행 하는 경우 코드는 쿼리 문자열에서 ID를 가져왔습니다. 쿼리 문자열 조금 이라도 이후로 변경 된 경우 원래 표시 된 동영상 ID를 가져오는 중인 되도록 숨겨진된 필드의 값을 가져옵니다.

실제로 중요 한 차이점을 *AddMovie* 코드 및이 코드는이 코드에서 사용 하는 SQL `Update` 대신 문을 `Insert Into` 문입니다. 다음 예제에서는 SQL 구문의 `Update` 문:

`UPDATE table SET col1="value", col2="value", col3="value" ... WHERE ID = value`

순서에 관계 없이 모든 열을 지정할 수 있습니다 및 중 모든 열을 업데이트할 필요가 반드시는 `Update` 작업 합니다. (적용 레코드 새 레코드로 저장 됩니다 및에 대 한 허용 되지 않는 때문에 자체 ID를 업데이트할 수 없습니다는 `Update` 작업 합니다.)

> [!NOTE] 
> 
> **중요** 는 `Where` 데이터베이스에서 데이터베이스를 인식 하는 방법 이기 때문에 ID 사용 하 여 절은 아주 중요 합니다을 업데이트 하려는 레코드입니다. 중단 하는 경우는 `Where` 데이터베이스 업데이트 절 *모든* 데이터베이스의 레코드입니다. 대부분의 경우에서 재해가 될 것입니다.


코드에서 자리 표시자를 사용 하 여 값을 업데이트 하는 SQL 문에 전달 됩니다. 전에 말한 새로운 반복: 보안상의 이유로 *만* 자리 표시자를 사용 하 여 SQL 문에 값을 전달 합니다.

코드를 사용한 후 `db.Execute` 실행 하는 `Update` 문을 변경 내용을 볼 수 있는 목록 페이지를 다시 리디렉션합니다.

> [!TIP] 
> 
> **다른 SQL 문을 다른 메서드**
> 
> 보았을 것 약간 다른 방법을 사용 하 여 다른 SQL 문을 실행 합니다. 실행 하는 `Select` 쿼리에서 잠재적으로 반환 하며 여러 레코드를 사용 하는 `Query` 메서드. 실행 하는 `Select` 알고 있는 쿼리는 데이터베이스 항목을 하나만 반환 합니다.를 사용 하는 `QuerySingle` 메서드. 사용할 데이터베이스 항목을 반환 하지는 않습니다 변경 하는 명령을 실행 하는 `Execute` 메서드.
> 
> 간의 차이에 이미 본 것 처럼 각각 다른 결과 반환 하기 때문에 다른 메서드를 포함 해야 `Query` 고 `QuerySingle`입니다. (합니다 `Execute` 실제로 반환 값도 &mdash; 명령에 의해 영향을 받는 데이터베이스 행의 수 즉, &mdash; 있습니다 했으므로 되었습니다 무시 하는 지금 있지만.)
> 
> 물론는 `Query` 메서드는 하나의 데이터베이스 행을 반환할 수 있습니다. 그러나 ASP.NET의 결과 항상 처리는 `Query` 컬렉션인 메서드. 메서드가 행을 하나만 반환 하는 경우에 컬렉션에서 단일 행을 추출 해야 합니다. 상황에 따라서 여기서 있습니다 *알고* 얻게 하나의 행만, 사용 하는 편리한 다소 `QuerySingle`합니다.
> 
> 특정 유형의 데이터베이스 작업을 수행 하는 다른 몇 가지 방법 이며 데이터베이스 메서드 목록을 찾을 수 있습니다 합니다 [ASP.NET Web Pages API 빠른 참조](../../api-reference/asp-net-web-pages-api-reference.md#Data)합니다.


## <a name="making-validation-for-the-id-more-robust"></a>강력한 ID 더에 대 한 유효성 검사를 수행

페이지를 실행 하는 처음으로 표시 된 동영상 ID를 쿼리 문자열에서 데이터베이스에서 해당 동영상 가져오기 전환할 수 있습니다. 실제로 했습니다.이 코드를 사용 하 여 수행한 하는 값을 검색할 이동할 수 있게:

[!code-csharp[Main](updating-data/samples/sample13.cs)]

되도록 하는 사용자를 가져오는 경우이 코드를 사용 합니다 *EditMovies* 에서 동영상을 먼저 선택 하지 않고 페이지를 *영화* 페이지에서 페이지 친숙 한 오류 메시지를 표시 합니다. (이 고, 그렇지 사용자 오류를 볼 수는 있을 것 혼동할입니다.)

그러나이 유효성 검사는 매우 강력 하지 않습니다. 이러한 오류와 함께 페이지 호출할 수도 있습니다.

- ID 번호를 하지 않습니다. 예를 들어과 같은 URL을 사용 하 여 페이지를 호출할 수 없습니다 `http://localhost:nnnnn/EditMovie?id=abc`합니다.
- ID는 숫자로 하지만 존재 하지 않는 동영상 참조 (예를 들어 `http://localhost:nnnnn/EditMovie?id=100934`).

원하는 경우 이러한 Url을 실행에서 발생 하는 오류를 확인 하려면 합니다 *영화* 페이지입니다. 동영상을 편집 하려면 선택 하 고 다음의 URL을 변경 합니다 *EditMovie* 알파벳을 포함 하는 URL로 페이지 ID 또는 존재 하지 않는 동영상의 ID입니다.

따라서 어떻게 해야 합니까? 첫 번째 해결 뿐만 아니라 ID 전달 되도록 페이지로 이지만 ID는 정수는 있는지 확인 하는 것입니다. 코드를 변경 합니다 `!IsPost` 이 예제와 같이 테스트 합니다.

[!code-csharp[Main](updating-data/samples/sample14.cs)]

두 번째 조건을 추가한 합니다 `IsEmpty` 테스트를 사용 하 여 연결 된 `&&` (논리적 AND):

[!code-csharp[Main](updating-data/samples/sample15.cs)]

기억 될 수 있습니다 합니다 [ASP.NET 웹 페이지 프로그래밍 소개](../introducing-razor-syntax-c.md) 자습서와 같은 메서드는 `AsBool` 는 `AsInt` 문자열 일부 다른 데이터 형식으로 변환 합니다. `IsInt` 메서드 (다른 사용자와 `IsBool` 고 `IsDateTime`) 비슷합니다. 그러나만 테스트 하는지 여부를 있습니다 *수* 실제로 변환을 수행 하지 않고 문자열을 변환 합니다. 기본적으로 이야기 여기 *쿼리 문자열 값을 정수로 변환할 수 있는 경우...* .

존재 하지 않는 동영상은 다른 잠재적인 문제를 찾습니다. 동영상 코드를이 코드와 같습니다.

[!code-csharp[Main](updating-data/samples/sample16.cs)]

전달 하는 경우는 `movieId` 값을 `QuerySingle` 오는 문이 및 실제 동영상에 해당 하지 않는 메서드, 아무 것도 반환 (예를 들어 `title=row.Title`) 오류를 발생 시킵니다.

다시는 쉽게 해결할 수 있습니다. 경우는 `db.QuerySingle` 없는 결과 반환 하는 메서드는 `row` 변수는 null이 됩니다. 확인할 수 있는지 여부를 `row` 에서 값을 가져오려고 시도 하기 전에 변수가 null 이면 합니다. 다음 코드를 추가 하는 `if` 블록의 값을 얻으려면 있는 문 주위를 `row` 개체:

[!code-csharp[Main](updating-data/samples/sample17.cs)]

이러한 두 가지 추가 유효성 검사 테스트를 사용 하 여 페이지에는 더 완벽 됩니다. 에 대 한 전체 코드는 `!IsPost` 분기는 이제이 예제와 같습니다.

[!code-csharp[Main](updating-data/samples/sample18.cs)]

했습니다 보면 번이 작업에 대 한 적절 하 게 사용 인지는 `else` 블록입니다. 테스트에 전달 하지는 `else` 블록 오류 메시지를 설정 합니다.

## <a name="adding-a-link-to-return-to-the-movies-page"></a>Movies 페이지로 반환에 대 한 링크를 추가 합니다.

최종 하 고 유용한 세부 정보 링크를 추가 하는 것으로 *영화* 페이지입니다. 이벤트의 일반 흐름에서 사용자에 시작 됩니다 합니다 *영화* 페이지를 **편집** 링크. 제공 하는 합니다 *EditMovie* 페이지에서 동영상을 편집 하 고 단추를 클릭 있습니다. 코드 변경 내용을 처리 한 후 다시 리디렉션합니다 합니다 *영화* 페이지입니다.

단,

- 사용자는 아무 것도 변경할 필요가 결정할 수 있습니다.
- 사용자 클릭 하지 않고이 페이지에 수신를 **편집할** 링크를 *영화* 페이지입니다.

기본 목록에 반환 하기 위해 쉽게 하려는 어느 합니다. 쉽게 해결할 수 있습니다 &mdash; 닫은 직후 다음 태그를 추가 `</form>` 태그에 태그:

[!code-html[Main](updating-data/samples/sample19.html)]

이 태그에 대 한 동일한 구문을 사용 하는 `<a>` 다른 곳에서 볼 수 있는 요소입니다. URL에 포함 `~` "웹 사이트의 루트입니다."를 의미 합니다.

## <a name="testing-the-movie-update-process"></a>영화 업데이트 프로세스를 테스트합니다.

이제 테스트할 수 있습니다. 실행 합니다 *영화* 페이지 및 클릭 **편집** 동영상 옆에 있는 합니다. 경우는 *EditMovie* 페이지가 표시 되 면 변경 하 고 영화 **변경 내용 전송**합니다. 영화 목록에 표시 되 면 변경 내용을 표시 되는 있는지 확인 합니다.

유효성 검사 작동 하는지 확인, 클릭 **편집** 다른 동영상에 대 한 합니다. 에 표시 되는 경우는 *EditMovie* 페이지의 선택을 취소 합니다 **장르** 필드 (또는 **연도** 필드 또는 둘 다) 변경 내용을 제출 하려고 합니다. 예상한 대로 오류가 표시 됩니다.

![유효성 검사 오류를 보여 주는 동영상 페이지 편집](updating-data/_static/image4.png)

클릭 합니다 **영화 목록에 반환** 여 변경 내용을 반환 하는 링크는 *영화* 페이지입니다.

## <a name="coming-up-next"></a>다음에 나오는

다음 자습서에서는 영화 레코드를 삭제 하는 방법을 배웁니다.

## <a name="complete-listing-for-movie-page-updated-with-edit-links"></a>동영상 페이지 (편집 링크를 사용 하 여 업데이트)에 대 한 전체 목록

[!code-cshtml[Main](updating-data/samples/sample20.cshtml)]

<a id="Complete_Page_Listing_for_EditMovie"></a>
## <a name="complete-page-listing-for-edit-movie-page"></a>전체 페이지 목록 편집 동영상 페이지

[!code-cshtml[Main](updating-data/samples/sample21.cshtml)]

## <a name="additional-resources"></a>추가 리소스

- [Razor 구문을 사용 하 여 ASP.NET 웹 프로그래밍 소개](../../getting-started/introducing-razor-syntax-c.md)
- [SQL UPDATE 문을](http://www.w3schools.com/sql/sql_update.asp) W3Schools 사이트

> [!div class="step-by-step"]
> [이전](entering-data.md)
> [다음](deleting-data.md)
