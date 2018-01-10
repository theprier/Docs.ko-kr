---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/updating-data
title: "Introducing ASP.NET 웹 페이지-데이터베이스 데이터 업데이트 | Microsoft Docs"
author: tfitzmac
description: "이 자습서에서는 ASP.NET 웹 페이지 (Razor)를 사용 하는 경우 (변경) 기존 데이터베이스 항목을 업데이트 하는 방법을 보여 줍니다. 계열을 완료 한 것으로 가정 번째..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/02/2018
ms.topic: article
ms.assetid: ac86ec9c-6b69-485b-b9e0-8b9127b13e6b
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/updating-data
msc.type: authoredcontent
ms.openlocfilehash: b016231975bf8d359f4c390b0b478edc383117d4
ms.sourcegitcommit: df2157ae9aeea0075772719c29784425c783e82a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/10/2018
---
<a name="introducing-aspnet-web-pages---updating-database-data"></a>Introducing ASP.NET 웹 페이지-데이터베이스 데이터 업데이트
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 자습서에서는 ASP.NET 웹 페이지 (Razor)를 사용 하는 경우 (변경) 기존 데이터베이스 항목을 업데이트 하는 방법을 보여 줍니다. 통해 시리즈를 완료 한 것으로 가정 [데이터 입력 하 여 사용 하 여 양식을 사용 하 여 ASP.NET 웹 페이지](entering-data.md)합니다.
> 
> 학습 내용:
> 
> - 개별 레코드를 선택 하는 방법의 `WebGrid` 도우미입니다.
> - 데이터베이스에서 단일 레코드를 읽을 하는 방법.
> - 데이터베이스 레코드의 값을 포함 하는 폼을 미리 로드 하는 방법.
> - 데이터베이스의 기존 레코드를 업데이트 하는 방법입니다.
> - 페이지에 표시 하지 않고 정보를 저장 하는 방법.
> - 정보를 저장 하 여 숨겨진된 필드를 사용 하는 방법입니다.
>   
> 
> 기능/기술을 설명 합니다.
> 
> - `WebGrid` 도우미입니다.
> - SQL `Update` 명령입니다.
> - `Database.Execute` 메서드
> - 숨겨진 필드 (`<input type="hidden">`).


## <a name="what-youll-build"></a>만들 것인지

이전 자습서에서는 데이터베이스에 레코드를 추가 하는 방법을 알아보았습니다. 여기에서는 편집을 위해 레코드를 표시 하는 방법을 설명 합니다. 에 *동영상* 업데이트 합니다 페이지는 `WebGrid` 도우미를 표시 하도록는 **편집** 각 영화 옆에 있는 링크:

![WebGrid 각 동영상에 대 한 '편집' 링크를 포함 하 여 표시](updating-data/_static/image1.png)

클릭는 **편집** 링크를 걸리는 다른 페이지로 영화 정보를 양식에 이미 여기서:

![동영상을 편집할 수를 보여 주는 동영상 페이지 편집](updating-data/_static/image2.png)

값 중 하나를 변경할 수 있습니다. 변경 내용을 제출 하면 코드 페이지에는 데이터베이스가 업데이트 되 고 영화 목록으로 돌아갑니다.

이 부분의 프로세스와 거의 정확 하 게 작동는 *AddMovie.cshtml* 익숙할 것이 자습서의 많은 하므로 이전 자습서에서 만든 페이지입니다.

여러 가지 방법으로 개별 영화를 편집 하는 기능을 구현할 수 있습니다. 보여준 방식은 구현 하기 쉽고 이해 하기 쉬운 이기 때문에 선택 되었습니다.

## <a name="adding-an-edit-link-to-the-movie-listing"></a>편집 링크가 영화 목록에 추가

를 시작 하려면 업데이트 합니다는 *동영상* 도 나열 하는 각 영화 포함 되도록 페이지는 **편집** 링크 합니다.

열기는 *Movies.cshtml* 파일입니다.

페이지 본문에서 변경 된 `WebGrid` 열을 추가 하 여는 태그입니다. 수정 된 태그는 다음과 같습니다.

[!code-html[Main](updating-data/samples/sample1.html?highlight=6)]

새 열이이 하나가:

[!code-html[Main](updating-data/samples/sample2.html)]

이 열의 지점 한 링크를 표시 하는 것 (`<a>` 요소) 이라고 표시 된 "편집"입니다. 이 페이지를 실행 하는 경우 다음과 같이 표시 하는 링크를 만드는 것 후 우리가와 `id` 각 동영상에 대 한 다른 값:

[!code-css[Main](updating-data/samples/sample3.css)]

이 링크는 라는 페이지 호출 *EditMovie*, 쿼리 문자열을 전달 합니다 `?id=7` 해당 페이지에 있습니다.

새 열에 대 한 구문 약간 복잡 하 게 보일 수 있지만 몇 가지 요소가 함께 배치 하기 때문에. 각 개별 요소는 간단 합니다. 에 집중 하는 경우 테이블만 `<a>` 요소를이 태그를 표시 합니다.

[!code-html[Main](updating-data/samples/sample4.html)]

눈금의 작동 방법에 대 한 배경 지식이: 각 필드에 대 한 열 데이터베이스 레코드에 표시 되며 표에 각 데이터베이스 레코드에 대 한 행이 표시 됩니다. 각 표 형태 창의 행 생성 되는 동안는 `item` 해당 행에 대해 데이터베이스 레코드 (항목)를 포함 하는 개체입니다. 이 정렬에 해당 행에 대 한 데이터를 가져오려고 코드에는 방법을 제공 합니다. 즉, 여기: 식 `item.ID` 은 현재 데이터베이스 항목의 ID 값을 가져오는 것입니다. 나타날 수 있습니다 (제목, genre 또는 년) 데이터베이스 값이 하나라도 같은 방법으로 사용 하 여 `item.Title`, `item.Genre`, 또는 `item.Year`합니다.

식 `"~/EditMovie?id=@item.ID` 대상 URL의 하드 코드 된 부분을 결합 (`~/EditMovie?id=`)이 동적으로 파생 id (언급 했 듯이 `~` 이전 자습서; 연산자는 현재 웹 사이트 루트를 나타내는 ASP.NET 연산자입니다.)

그 결과 열에는 태그의이 부분 하기만 하면 다음 태그와 같은 런타임에 생성 됩니다.

[!code-xml[Main](updating-data/samples/sample5.xml)]

실제 값 당연히 `id` 각 행에 대해 달라 집니다.

## <a name="creating-a-custom-display-for-a-grid-column"></a>표 형태 창의 열에 대 한 디스플레이 사용자 지정 만들기

표 형태 창의 열에 다시 이제입니다. 세 개의 열 원래 표가 표시 된 데이터 값만 (제목, genre 및 년)에 했습니다. 이 표시는 데이터베이스 열의 이름을 전달 하 여 지정한 &mdash; 예를 들어 `grid.Column("Title")`합니다.

이 새로운 **편집** 링크 열은 다릅니다. 열 이름을 지정 하는 대신 전달 된 `format` 매개 변수입니다. 이 매개 변수를 사용 하면 태그를 정의할 수 있는 `WebGrid` 도우미와 함께 렌더링 합니다는 `item` 굵게 또는 녹색 열 데이터를 표시 하거나 원하는 원하는 형식으로 해당 값을 합니다. 예를 들어 제목을 굵게 표시 하려는 경우이 예제에서와 같이 열을 만들 수 있습니다.

[!code-html[Main](updating-data/samples/sample6.html)]

(다양 한 `@` 문자에서 참조 된 `format` 속성의 전환 태그 및 코드 값을 표시 합니다.)

에 대 한 것을 알고 있다면는 `format` 은 쉽게 이해할 수 있도록 속성을 어떻게 새 **편집** 링크 열이 함께 저장 됩니다:

[!code-html[Main](updating-data/samples/sample7.html)]

열 구성 *만* 의 링크를 렌더링 하는 태그를 몇 가지 정보 (ID)와 하에서 추출 되는 행에 대 한 데이터베이스 레코드입니다.

> [!TIP] 
> 
> **명명 된 매개 변수 및 메서드에 대 한 위치 매개 변수**
> 
> 여러 번 메서드 호출을 매개 변수 전달, 단순히 나열 쉼표로 구분 하 여 매개 변수 값입니다. 몇 가지 예는 다음과 같습니다.
> 
> `db.Execute(insertCommand, title, genre, year)`
> 
> `Validation.RequireField("title", "You must enter a title")`
> 
> 먼저이 코드를 표시 하지만 각각의 경우에서에 특정 순서로 관계 매개 변수를 전달 하는 경우 문제가 언급 하지 않은 &mdash; 메서드에 정의 되어 있는 매개 변수 순서 즉, 합니다. 에 대 한 `db.Execute` 및 `Validation.RequireFields`, 페이지를 실행할 때 오류 메시지가 나타나거나 이상한 결과 이상 얻을 전달 하는 값의 순서를 혼합 하는 경우. 명확 하 게 매개 변수를 전달 하는 순서를 파악 해야 합니다. (WebMatrix에서 IntelliSense 문의할 수 있습니다 이름, 형식 및 매개 변수의 순서를 확인 합니다.)
> 
> 을 순서 대로 값을 전달 하는 대신 사용 하 여 *명명 된 매개 변수*합니다. (사용 하 여 라고 순서로 매개 변수를 전달 *위치 매개 변수*.) 명명 된 매개 변수에 대 한 명시적으로 포함 매개 변수 이름을 해당 값을 전달 하는 경우. 명명 된 매개 변수가 이미 여러 번에서에서 사용한 이러한 자습서입니다. 예:
> 
> [!code-csharp[Main](updating-data/samples/sample8.cs)]
> 
> 를 갖는
> 
> [!code-css[Main](updating-data/samples/sample9.css)]
> 
> 명명 된 매개 변수는 메서드가 많은 매개 변수를 사용 하는 경우에 특히는 몇 가지 상황에서 유용 합니다. 한 개나 두 개의 매개 변수를 전달 하려면 하지만 전달 하려는 값이 매개 변수 목록에서 첫 번째 위치 중 하나입니다. 가장 적합 하는 순서로 매개 변수를 전달 하 여 코드를 더 쉽게 읽을 수 있도록 하려면 다른 상황이 있습니다.
> 
> 물론, 명명 된 매개 변수를 사용 해야 매개 변수 이름을 알아야 합니다. WebMatrix IntelliSense 수 *표시* 의 이름, 하지만 없습니다 현재 양식으로 있습니다.


## <a name="creating-the-edit-page"></a>편집 페이지 만들기

이제 만들 수는 *EditMovie* 페이지. 사용자가 클릭 하면는 **편집** 링크를 합니다 결국이 페이지에 있습니다.

*EditMovie.cshtml* 바꾸고 다음 태그를 사용 하 여 파일에 포함 된 내용:

[!code-cshtml[Main](updating-data/samples/sample10.cshtml)]

이 태그와 코드에 있는 것과 비슷합니다는 *AddMovie* 페이지. 제출 단추에 대 한 텍스트에 약간의 차이가 있습니다. 과 마찬가지로 *AddMovie* 페이지, 즉는 `Html.ValidationSummary` 되어 있는 경우 유효성 검사 오류를 표시 하는 호출 합니다. 에 대 한 호출을 제외 하는 것이 시간 `Validation.Message`이므로 유효성 검사 요약에 오류가 표시 됩니다. 이전 자습서에서 설명한 대로, 다양 한 조합에서 유효성 검사 요약 및 개별 오류 메시지를 사용할 수 있습니다.

다시 확인 하는 `method` 특성에는 `<form>` 로 설정 된 `post`합니다. 과 마찬가지로 *AddMovie.cshtml* 페이지에서이 페이지를 수정 하는 데이터베이스입니다. 따라서이 폼을 수행 해야는 `POST` 작업 합니다. (간의 차이 대 한 자세한 `GET` 및 `POST` 작업의 경우 참조는 [GET, POST 및 HTTP 동사 안전](form-basics.md#GET,_POST,_and_HTTP_Verb_Safety) HTML 폼에 대 한 자습서에서 사이드바.)

이전 자습서에서 볼 수 있듯이 `value` 텍스트 상자의 특성을 미리 설치 하기 위해 Razor 코드로 설정 되 고 있습니다. 이 시간 하지만 사용 하는 같은 변수 `title` 및 `genre` 대신 해당 작업에 대해 `Request.Form["title"]`:

`<input type="text" name="title" value="@title" />`

로 이전에이 태그는 미리 로드 하는 텍스트 상자 값과 영화 값. 사용 하는 대신이 시간 변수를 사용 하는 편리한 이유는 잠시 후에 표시 됩니다는 `Request` 개체입니다.

또한 한 `<input type="hidden">` 이 페이지의 요소입니다. 이 요소는 페이지에 표시 하지 영화 ID를 저장 합니다. ID가 처음 페이지에 전달 하 여 쿼리 문자열 값을 사용 하 여 (`?id=7` 또는 유사한 URL에). 숨겨진된 필드에는 ID 값을 설정 하 여 사용할 수 있는지 가능 페이지로 호출 되었으므로 원래 URL에 대 한 액세스를 더 이상 있는 경우에, 폼 전송 됩니다.

와 달리는 *AddMovie* 에 대 한 코드 페이지는 *EditMovie* 페이지에 두 가지 고유 함수입니다. 첫 번째 함수는 페이지가 처음으로 표시 될 때 (및 *만* 후), 코드 쿼리 문자열에서 영화 ID를 가져옵니다. 다음 코드를 사용 하 여 ID 데이터베이스에서 해당 영화를 읽고 표시 하 (미리 로드)이 있는 텍스트 상자에.

두 번째 함수는 사용자가 클릭 하 여 **변경 내용 전송** 단추를 코드에는 입력란의 값을 읽고의 유효성을 검사 합니다. 코드는 또한 데이터베이스 항목을 새 값으로 업데이트할 수 있습니다. 이 방법은 레코드를 증가 시킬에서 볼 수 있듯이 *AddMovie*합니다.

## <a name="adding-code-to-read-a-single-movie"></a>단일 영화를 읽는 코드를 추가 합니다.

첫 번째 함수를 수행 하려면이 코드 페이지의 맨 위에 추가 합니다.

[!code-cshtml[Main](updating-data/samples/sample11.cshtml)]

이 코드의 대부분은 시작 되는 블록 안에 `if(!IsPost)`합니다. `!` 연산자 의미 "not" 식 의미 하므로 *이 요청이 post 제출 없으면*, 방법도 간접 방법 *이 요청은 처음으로이 페이지를 실행 하는 경우*합니다. 이 코드를 실행 해야 듯이 *만* 처음으로 페이지를 실행 합니다. 코드를 포함 하지 않은 경우 `if(!IsPost)`, 페이지가 호출 될 때마다, 여부 처음으로 실행 거 나 단추에 대 한 응답에서를 클릭 합니다.

코드에는 `else` 이 시간을 차단 합니다. 도입 여기서 설명한 것 처럼 `if` 경우도 테스트 하는 조건이 true 없는 경우 대체 코드를 실행 하려면 블록입니다. 여기서입니다. 조건 (즉, 경우 페이지에 전달 된 ID 확인)를 통과 하면 데이터베이스에서 행을 읽을 합니다. 그러나 조건을 통과 하지 못한 경우는 `else` 블록 실행 및 코드 오류 메시지를 설정 합니다.

## <a name="validating-a-value-passed-to-the-page"></a>페이지에 전달 되는 값의 유효성 검사

코드를 사용 하 여 `Request.QueryString["id"]` 페이지에 전달 되는 ID를 가져옵니다. 코드를 통해 ID에 대 한 값을 전달 된 실제로 값이 전달 된 경우 코드 유효성 검사 오류를 설정 합니다.

이 코드에 정보의 유효성을 검사 하는 다른 방법을 보여 줍니다. 이전 자습서에서 사용한는 `Validation` 도우미입니다. 확인을 위해 필드를 등록 하 고 ASP.NET에서 자동으로 유효성 검사를가 하 고 사용 하 여 오류를 표시 `Html.ValidationMessage` 및 `Html.ValidationSummary`합니다. 그러나이 경우 있습니다 하는 것은 아닙니다 사용자 입력 유효성 검사 합니다. 대신, 다른 위치에서 페이지에 전달 된 값의 유효성 검사 중인 있습니다. `Validation` 도우미 하지는 않습니다.

따라서 체크 값을 직접 사용 하 여 테스트 하 여 `if(!Request.QueryString["ID"].IsEmpty()`). 문제가 있는 경우 사용 하 여 오류를 표시할 수 있습니다 `Html.ValidationSummary`에서와 마찬가지로는 `Validation` 도우미입니다. 이러한 파일을 호출 하면 `Validation.AddFormError` 표시할 메시지를 전달 합니다. `Validation.AddFormError`익숙한 이미 유효성 검사 시스템을 사용 하 여 일치 하는 사용자 지정 메시지를 정의할 수 있도록 하는 기본 제공 메서드입니다. (이 자습서의 뒷부분에 나오는 알아보겠습니다이 유효성 검사 프로세스를 좀 더 강력 하 게 하는 방법에 대 한.)

동영상에 대 한 ID가 있는지에 확인 한 후 코드는 단일 데이터베이스 항목을 찾는 데이터베이스를 읽습니다. (아마도 데이터베이스 작업에 대 한 일반적인 패턴 보았을: 데이터베이스를 열고 SQL 문을 정의 하는 문을 실행 합니다.) 이 이번에는 SQL `Select` 문에 포함 `WHERE ID = @0`합니다. ID가 고유 하므로 하나의 레코드를 반환할 수 있습니다.

쿼리를 사용 하 여 수행할 `db.QuerySingle` (하지 `db.Query`영화 목록에 사용한 것과,), 코드 결과를 하 고는 `row` 변수. 이름 `row` 는 임의로 지정; 변수를 원하는 이름을 지정할 수 있습니다. 변수를 위쪽에 초기화 이러한 값 텍스트 상자에 표시 될 수 있도록 다음 영화 세부 정보로 채워집니다.

## <a name="testing-the-edit-page-so-far"></a>테스트 편집 페이지 (지금까지)

페이지를 테스트 하려는 경우 실행는 *동영상* 이제 페이지 클릭 하 여 프로그램 **편집** 모든 동영상 옆에 있는 링크입니다. 표시는 *EditMovie* 선택한 영화 세부 정보를 사용 하는 페이지 시간이 입력:

![동영상을 편집할 수를 보여 주는 동영상 페이지 편집](updating-data/_static/image3.png)

페이지의 URL 같이 `?id=10` (또는 다른 몇 가지 번호)입니다. 테스트 했지만 지금까지 **편집** 에서는 정적으로 연결의 *영화* 작업 시간, 페이지 ID는 쿼리 문자열에서 읽고 단일 동영상 레코드를 가져올 데이터베이스 쿼리 한다고 되어 작동 하 고 페이지입니다.

영화 정보를 변경할 수 있지만 클릭할 때 아무 작업도 수행 **변경 내용 전송**합니다.

## <a name="adding-code-to-update-the-movie-with-the-users-changes"></a>동영상 사용자의 변경 내용으로 업데이트 하는 코드 추가

에 *EditMovie.cshtml* 파일, 두 번째 함수 (변경 내용 저장)을 구현 하려면 추가 바로의 닫는 중괄호 안에 다음 코드는 `@` 블록입니다. (정확한 위치 코드를 잘 모르는 경우에 볼 수 있습니다는 [영화 편집 페이지에 대 한 전체 코드](#Complete_Page_Listing_for_EditMovie) 이 자습서의 끝에 나타나는.)

[!code-csharp[Main](updating-data/samples/sample12.cs)]

이 태그와 코드 역시의 코드와 유사한 *AddMovie*합니다. 코드는는 `if(IsPost)` 이 코드는 사용자가 클릭할 때만 실행 되므로 차단는 **변경 내용 전송** 단추 &mdash; 즉 때 (및 경우에만) 폼이 게시 합니다. 이 경우 같은 테스트를 사용 하지 않는 `if(IsPost && Validation.IsValid())`-즉, 하지 통합할 두 테스트 모두 사용 하 여 and가 있습니다. 이 페이지에 먼저 생각 양식을 제출 하 여 인지 (`if(IsPost)`)만 다음 유효성 검사에 대 한 필드를 등록 합니다. 다음 유효성 검사 결과 테스트할 수 있습니다 (`if(Validation.IsValid()`). 흐름은 약간 변경 된 *AddMovie.cshtml* 페이지 다르지만 효과 동일 합니다.

사용 하 여 텍스트 상자의 값을 가져올 `Request.Form["title"]` 와 비슷한 코드를 다른 `<input>` 요소입니다. 이 이번에는 코드 가져옴을 영화 ID 숨겨진된 필드에서 확인할 수 (`<input type="hidden">`). 페이지에 처음으로 실행 하는 경우 코드 쿼리 문자열에서 ID를 가져왔습니다. 쿼리 문자열 조금 이라도 그 이후에 변경 된 경우 원래 표시 된 동영상의 ID를 가져오는 중인 되도록 숨겨진된 필드의 값을 가져옵니다.

실제로 중요 한 차이점은 *AddMovie* 코드 및이 코드는이 코드에서 사용 하는 SQL `Update` 문 대신는 `Insert Into` 문. 다음 예제에서는 SQL 구문의 `Update` 문:

`UPDATE table SET col1="value", col2="value", col3="value" ... WHERE ID = value`

순서에 관계 없이 모든 열을 지정할 수 있습니다 및 업데이트 하는 동안 모든 열 반드시 없는 `Update` 작업 합니다. (을 업데이트할 수 없습니다 자체 ID로 새 레코드를 레코드를 저장 하는 적용는 및에 허용 되지 않습니다는 `Update` 작업 합니다.)

> [!NOTE] 
> 
> **중요 한** 는 `Where` 데이터베이스는 데이터베이스를 인식 하는 방법 이기 때문에 ID 가진 절이 매우 중요 레코드 업데이트 하려고 합니다. 중단 된 경우는 `Where` 절, 데이터베이스를 업데이트 합니다 *모든* 데이터베이스에 기록 합니다. 대부분의 경우에서 재해 될 것입니다.


코드에서 자리 표시자를 사용 하 여 업데이트할 값을 SQL 문에 전달 됩니다. 반복 하기 전에 말한 것 무엇: 보안상의 이유로 *만* 자리 표시자를 사용 하 여 SQL 문을에 값을 전달 합니다.

코드에서는 사용 후 `db.Execute` 실행 하는 `Update` 변경 내용을 볼 수 있는 목록 페이지를 다시 리디렉션합니다. 문의 합니다.

> [!TIP] 
> 
> **다른 SQL 문을 여러 가지 방법**
> 
> 약간 다른 방법을 사용 하 여 다른 SQL 문을 실행할 것을 알 수 있습니다. 실행 하는 `Select` 쿼리에서 잠재적으로 반환 여러 레코드를 사용 하는 `Query` 메서드. 실행 하는 `Select` 쿼리를 하나의 데이터베이스 항목을 반환 합니다를 사용 하는 `QuerySingle` 메서드. 변경 하지만 데이터베이스 항목을 반환 하지 않는 하는 명령은 실행 하려면 사용 된 `Execute` 메서드.
> 
> 차집합에 이미 본 것 처럼 각각 서로 다른 결과 반환 하기 때문에 다양 한 방법이 있어야 `Query` 및 `QuerySingle`합니다. (의 `Execute` 메서드 실제로 반환 값도 &mdash; 명령에 의해 영향을 받는 데이터베이스 행 수가 즉, &mdash; 있습니다 한 되었습니다 무시 하는 지금까지 하지만.)
> 
> 물론,는 `Query` 메서드는 데이터베이스 행을 하나만 반환할 수 있습니다. 그러나 ASP.NET의 결과 항상 처리는 `Query` 메서드 컬렉션으로. 메서드가 하나의 행을 반환 하는 경우에 컬렉션에서 단일 행에는 추출 해야 합니다. 경우에 따라서 여기서 있습니다 *알고* 얻을 다시 행을 하나만, 사용 하는 편리한 방법을 다소 `QuerySingle`합니다.
> 
> 특정 유형의 데이터베이스 작업을 수행 하는 다른 메서드를 몇 개 있습니다. 데이터베이스 메서드 목록을 찾을 수 있습니다는 [ASP.NET Web Pages API 빠른 참조](../../api-reference/asp-net-web-pages-api-reference.md#Data)합니다.


## <a name="making-validation-for-the-id-more-robust"></a>강력한 ID 등에 대 한 유효성 검사를 수행

페이지를 실행 하는 처음으로 얻게 영화 ID는 쿼리 문자열에서 데이터베이스에서 해당 동영상 가져오기 전환할 수 있습니다. 실제로 했음을 검색할 이동 하려면이 코드를 사용 하 여 수행한 값 있는지 했습니다.

[!code-csharp[Main](updating-data/samples/sample13.cs)]

되도록 하는 사용자가을 하는 경우이 코드를 사용는 *EditMovies* 에서 동영상을 먼저 선택 하지 않으면 페이지는 *영화* 페이지에서 페이지 친숙 한 오류 메시지를 표시 합니다. (이렇게 하지 않으면 사용자가 오류를 볼 수 혼동 있을 것는 것입니다.)

그러나이 유효성 검사는 매우 강력 하지 않습니다. 이러한 오류와 함께 페이지를 호출할 수도 수 있습니다.

- ID 번호를 하지 않습니다. 같은 URL을 사용 하 여 페이지 수 호출 하는 예를 들어 `http://localhost:nnnnn/EditMovie?id=abc`합니다.
- ID는 숫자, 존재 하지 않는 동영상을 참조 하지만 (예를 들어 `http://localhost:nnnnn/EditMovie?id=100934`).

실행이 Url에서 발생 하는 오류를 보려면 내용은 *동영상* 페이지. 동영상을 편집 하려면 선택 하 고 다음의 URL을 변경는 *EditMovie* 알파벳 포함 된 URL로 페이지 ID 또는 존재 하지 않는 동영상의 ID입니다.

따라서 어떻게 해야 합니까? 첫 번째 해결 방법은 뿐만 아니라 ID 전달 되도록 페이지에 있지만 ID는 정수에 있는지 확인 합니다. 에 대 한 코드를 변경는 `!IsPost` 테스트를이 예제와 같습니다.

[!code-csharp[Main](updating-data/samples/sample14.cs)]

두 번째 조건을 추가 `IsEmpty` 로 연결 된 테스트 `&&` (논리적 AND):

[!code-csharp[Main](updating-data/samples/sample15.cs)]

기억 수는 [ASP.NET 웹 페이지 프로그래밍 소개](../introducing-razor-syntax-c.md) 자습서와 같은 메서드를 통해 `AsBool` 는 `AsInt` 문자열 일부 다른 데이터 형식으로 변환 합니다. `IsInt` 메서드 (다음과 같은 기타 상자에서는 `IsBool` 및 `IsDateTime`) 권장 사항과 비슷합니다. 그러나만 테스트 여부 있습니다 *수* 실제로 변환을 수행 하지 않고 문자열을 변환 합니다. 여기 있습니다 하는 명시적으로 *쿼리 문자열 값을 정수로 변환할 수 있는 경우...* .

다른 잠재적 문제가 존재 하지 않는 동영상을 찾고 있습니다. 이 코드와 비슷합니다 동영상을 가져오는 코드입니다.

[!code-csharp[Main](updating-data/samples/sample16.cs)]

전달 하는 경우는 `movieId` 값을 `QuerySingle` 실제 동영상에 해당 하지 않는 메서드를 아무 것도 반환 하 고 문의 따르는 (예를 들어 `title=row.Title`) 오류가 발생 합니다.

다시 쉽게 고칠 수 있습니다. 경우는 `db.QuerySingle` 없는 결과 반환 하는 메서드는 `row` 변수는 null이 됩니다. 체크 인할 수 있는지 여부를 `row` 여기에서 값 가져오기 하려고 하기 전에 변수는 null입니다. 다음 코드에서는 추가 `if` 블록의 값을 가져오는 문에 `row` 개체:

[!code-csharp[Main](updating-data/samples/sample17.cs)]

이러한 두 개의 추가 유효성 검사 테스트 페이지 글머리 기호 성능을 입증 됩니다. 에 대 한 전체 코드는 `!IsPost` 분기 이제이 예제와 같습니다.

[!code-csharp[Main](updating-data/samples/sample18.cs)]

म 점을 한 번 더이 작업에 대 한 적절 하 게 사용 인지는 `else` 블록입니다. 테스트에 통과 하지 않는 경우는 `else` 블록 오류 메시지를 설정 합니다.

## <a name="adding-a-link-to-return-to-the-movies-page"></a>영화 페이지로 돌아가려면 링크 추가

최종 하 고 유용한 정보 링크를 추가 하는 것으로 다시는 *동영상* 페이지. 사용자가 시작 이벤트의 일반 흐름에서는 *동영상* 페이지를 클릭 하 고는 **편집** 링크 합니다. 제공 하는 *EditMovie* 페이지에서 며 수 영화를 편집 하 고 단추를 클릭 합니다. 다시 리디렉션합니다. 변경 내용을 처리 하는 코드는 *동영상* 페이지.

그러나:

- 사용자 아무 것도 변경 하지 않을 수 있습니다.
- 사용자는 클릭 하지 않고이 페이지에 수신는 **편집** 연결에 *영화* 페이지.

기본 목록으로 돌아가려면를 쉽게 확인 하려는 어떤 방법을 사용 하 합니다. 쉽게 수정 되었기 &mdash; 닫는 바로 뒤에 다음 태그에 추가 `</form>` 태그에 태그:

[!code-html[Main](updating-data/samples/sample19.html)]

이 태그에 대 한 동일한 구문을 사용 하 여 프로그램 `<a>` 다른 곳에서 보았을 요소입니다. URL에 포함 `~` 을 "웹 사이트의 루트입니다."를 의미 합니다.

## <a name="testing-the-movie-update-process"></a>영화 업데이트 프로세스를 테스트합니다.

이제 테스트할 수 있습니다. 실행 된 *동영상* 페이지를 클릭 하 여 **편집** 동영상 옆에 있는 합니다. 경우는 *EditMovie* 동영상 및 클릭을 변경할 페이지가 표시 되 면 **변경 내용 전송**합니다. 영화 목록이 표시 되 면 하는 경우 변경 내용을 표시 되어 있는지 확인 합니다.

유효성 검사가 작동 하려면 클릭 **편집** 다른 동영상에 대 한 합니다. 도달 하면는 *EditMovie* 선택을 취소 페이지는 **장르** 필드 (또는 **연도** 필드 또는 둘 다) 하 고 변경 내용을 전송 하려고 합니다. 오류를 예상 대로 표시 됩니다.

![유효성 검사 오류를 보여 주는 동영상 페이지 편집](updating-data/_static/image4.png)

클릭는 **영화 목록으로 반환** 링크 변경 내용을 취소 하 고 반환 하는 *영화* 페이지.

## <a name="coming-up-next"></a>다음에 나오는

다음 자습서에서는 영화 레코드를 삭제 하는 방법을 볼 수 있습니다.

## <a name="complete-listing-for-movie-page-updated-with-edit-links"></a>동영상 페이지 (편집 링크와 함께 업데이트)에 대 한 전체 목록을 보려면

[!code-cshtml[Main](updating-data/samples/sample20.cshtml)]

<a id="Complete_Page_Listing_for_EditMovie"></a>
## <a name="complete-page-listing-for-edit-movie-page"></a>전체 동영상 페이지 편집에 대 한 목록 페이지

[!code-cshtml[Main](updating-data/samples/sample21.cshtml)]

## <a name="additional-resources"></a>추가 리소스

- [Razor 구문을 사용 하 여 ASP.NET 웹 프로그래밍 소개](../../getting-started/introducing-razor-syntax-c.md)
- [SQL UPDATE 문을](http://www.w3schools.com/sql/sql_update.asp) W3Schools 사이트

>[!div class="step-by-step"]
[이전](entering-data.md)
[다음](deleting-data.md)
