---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/entering-data
title: ASP.NET 웹 페이지를 소개-양식을 사용 하 여 데이터베이스 데이터를 입력 합니다. | Microsoft Docs
author: tfitzmac
description: 이 자습서에서는 입력 폼을 만들고 다음에서 얻을 수 있는 폼을 데이터베이스 테이블에 ASP.NET 웹 페이지 (...를 사용 하는 경우 데이터를 입력 하는 방법을 보여 줍니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/28/2015
ms.topic: article
ms.assetid: d37c93fc-25fd-4e94-8671-0d437beef206
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/entering-data
msc.type: authoredcontent
ms.openlocfilehash: bbccf8134e90c19e29efaa5afe1e46e15320c189
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="introducing-aspnet-web-pages---entering-database-data-by-using-forms"></a>ASP.NET 웹 페이지를 소개-양식을 사용 하 여 데이터베이스 데이터를 입력 합니다.
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 자습서에서는 입력 폼을 만들고 다음에서 얻을 수 있는 폼을 데이터베이스 테이블에 ASP.NET 웹 페이지 (Razor)를 사용 하는 경우 데이터를 입력 하는 방법을 보여 줍니다. 통해 시리즈를 완료 한 것으로 가정 [기본 사항의 HTML 폼 ASP.NET 웹 페이지에서](https://go.microsoft.com/fwlink/?LinkId=251581)합니다.
> 
> 학습 내용:
> 
> - 입력 폼을 처리 하는 방법에 대 한 자세히 살펴보겠습니다.
> - (삽입) 데이터는 데이터베이스에 추가 하는 방법입니다.
> - 사용자가 형태로 (사용자 입력의 유효성을 검사 하는 방법)에 필요한 값으로 입력 했는지 확인 하는 방법.
> - 유효성 검사 오류를 표시 하는 방법입니다.
> - 현재 페이지에서 다른 페이지로 이동 하는 방법.
>   
> 
> 기능/기술을 설명 합니다.
> 
> - `Database.Execute` 메서드
> - SQL `Insert Into` 문
> - `Validation` 도우미입니다.
> - `Response.Redirect` 메서드


## <a name="what-youll-build"></a>만들 것인지

자습서의 이전 버전 데이터베이스를 만드는 방법을 살펴보았습니다를 입력 한 데이터베이스 데이터는 데이터베이스에서 작업 하는 WebMatrix에서 직접 편집 하 여는 **데이터베이스** 작업 영역입니다. 대부분의 응용 프로그램 없는에 있지만 데이터베이스에 데이터를 저장 하는 실용적인 방법이 있습니다. 따라서이 자습서에서는 모든 사용자 데이터를 입력 하 고 데이터베이스에 저장할 수 있는 웹 기반 인터페이스를 만듭니다.

새 동영상을 입력할 수 있는 페이지를 만듭니다. 페이지 입력 폼에 영화 제목, genre 및 연도 입력할 수 있는 필드가 (텍스트 상자)을 포함 됩니다. 페이지는이 페이지와 같습니다.

![브라우저에서 영화 추가' 페이지](entering-data/_static/image1.png)

텍스트 상자에는 HTML 됩니다 `<input>` 조회 하는 요소에는이 태그와 같은:

`<input type="text" name="genre" value="" />`

## <a name="creating-the-basic-entry-form"></a>기본 입력 양식 만들기

*AddMovie.cshtml*합니다.

다음 태그를 사용 하 여 파일에 무엇이 대체 합니다. 모든; 덮어쓰기 맨 위에 있는 코드 블록 곧 추가 합니다.

[!code-cshtml[Main](entering-data/samples/sample1.cshtml)]

이 예제에서는 일반적인 HTML 양식 만들기 사용 하 여 `<input>` 전송 단추 및 텍스트 상자에 대 한 요소입니다. 텍스트 상자에 대 한 캡션의 표준을 사용 하 여 만들어진 `<label>` 요소입니다. `<fieldset>` 및 `<legend>` 요소 좋은 상자 폼 주위에 배치 합니다.

이 페이지에서는 `<form>` 요소 사용 하 여 `post` 에 대 한 값으로는 `method` 특성입니다. 이전 자습서에서 사용 하는 폼 만들었습니다는 `get` 메서드. 그건 정확한 값을 서버, 폼 전송 있지만 요청 하지 변경한 내용이 때문에. 수행한 모든 다른 방법으로 데이터를 가져오고 했습니다. 그러나이 사용자에 게 알려줍니다 *됩니다* 변경-새 데이터베이스 레코드를 추가 하려고 합니다. 따라서이 양식을 사용 해야는 `post` 메서드. (간의 차이 대 한 자세한 `GET` 및 `POST` 작업의 경우 참조는[GET, POST 및 HTTP 동사 안전](https://go.microsoft.com/fwlink/?LinkId=251581#GET,_POST,_and_HTTP_Verb_Safety) 이전 자습서에서 사이드바.)

각 텍스트 상자에는 한 `name` 요소 (`title`, `genre`, `year`). 이전 자습서에서 살펴본 것 처럼 사용자의 입력을 나중에 가져올 수 있도록 이러한 이름을 해야 하기 때문에 이러한 이름은 중요 합니다. 모든 이름을 사용할 수 있습니다. 하는 것이 좋습니다 수 있는 의미 있는 이름을 사용 하 여 작업할 때 데이터를 기억 합니다.

`value` 각 특성 `<input>` Razor 코드의 비트를 포함 하는 요소 (예를 들어 `Request.Form["title"]`). 폼 전송한 후이 트릭의 버전 (있는 경우) 텍스트 상자에 입력 한 값을 보존 하려면 이전 자습서에서 배웠습니다.

## <a name="getting-the-form-values"></a>폼 값 가져오기

다음으로 양식을 처리 하는 코드를 추가 합니다. 개요에서는 다음을 수행 합니다.

1. 페이지가 게시 되 고 있는지 여부를 확인 하십시오 (전송) 합니다. 코드를 실행 하려면 페이지를 처음 실행할 때가 아니라 사용자가 단추를 클릭 한 경우에 합니다.
2. 사용자가 텍스트 상자에 입력 한 값을 가져옵니다. 이 경우 폼 사용 중이기 때문에 `POST` 양식 값을 가져올 동사는 `Request.Form` 컬렉션입니다.
3. 값에서 새 레코드를 삽입는 *동영상* 데이터베이스 테이블입니다.

파일 맨 위에 있는 다음 코드를 추가 합니다.

[!code-cshtml[Main](entering-data/samples/sample2.cshtml)]

처음 몇 줄 변수를 만듭니다 (`title`, `genre`, 및 `year`) 텍스트 상자에서 값을 보유 하도록 합니다. 줄 `if(IsPost)` 변수 설정 되어 있는지를 사용 하면 *만* 사용자가 클릭 하면는 **동영상 추가** 단추-즉 때 폼 게시 되었습니다.

와 같은 식을 사용 하 여 입력란의 값을 가져올 이전 자습서에서 살펴본 것 처럼 `Request.Form["name"]`여기서 *이름* 의 이름인는 `<input>` 요소입니다.

변수 이름 (`title`, `genre`, 및 `year`) 임의적입니다. 에 할당 된 이름이 같은 `<input>` 요소를 호출할 수 있습니다 필요 하면 합니다. (Name 특성을 일치 시키기 않아도 변수 이름 `<input>` 폼에서 요소가 있습니다.) 하지만과 마찬가지로 `<input>` 요소 것이 포함 된 데이터를 반영 하는 변수 이름을 사용 하는 것이 좋습니다. 코드를 작성할 때 일관 된 이름을 쉽게 작업할 때 데이터를 기억 하기.

## <a name="adding-data-to-the-database"></a>데이터베이스에 데이터 추가

코드에서 방금 추가한, 정당한 차단 *내* 닫는 중괄호 ( `}` )의 `if` (뿐 아니라 코드 블록) 블록을 다음 코드를 추가 합니다.

[!code-csharp[Main](entering-data/samples/sample3.cs)]

이 예에서는 데이터를 인출 하 고 표시 하기 위해 이전 자습서에 사용 되는 코드와 비슷합니다. 로 시작 하는 줄 `db =` 이전과 같은 데이터베이스가 고 다음 줄으로 SQL 문을 다시 정의 열립니다 앞입니다. 그러나이 이번 정의 SQL `Insert Into` 문. 다음 예제에서는 일반 구문은 `Insert Into` 문:

`INSERT INTO table (column1, column2, column3, ...) VALUES (value1, value2, value3, ...)`

즉, 테이블에 삽입할 다음을 삽입할 열을 나열 한 다음 삽입할 값을 나열 지정 합니다. (앞에서 설명한 것 처럼 SQL은 대/소문자 구분 하지 않지만 어떤 사람들 쉽게 명령을 읽을 수 있도록 키워드를 대문자로 바꿉니다.)

열에 삽입 하기에 이미 명령에 나열- `(Title, Genre, Year)`합니다. 재미 있는 것으로 텍스트 상자에서 값을 얻는 방법의 `VALUES` 명령에 포함 합니다. 실제 값 대신 참조 `@0`, `@1`, 및 `@2`은 물론 자리 표시자입니다. 명령을 실행 하는 경우 (에 `db.Execute` 줄)을 텍스트 상자에서 가져온 값을 전달 합니다.

**중요!** 여기에 표시 된 대로 SQL 문에서 사용자가 온라인 입력 데이터도 포함 해야 하는 유일한 방법은 자리 표시자를 사용 하는 (`VALUES(@0, @1, @2)`). SQL 문으로 사용자 입력을 연결 하면 열면 사용자가 직접 SQL 주입 공격에에 설명 된 대로 [양식 기본 ASP.NET 웹 페이지에서](https://go.microsoft.com/fwlink/?LinkId=251581) (이전 자습서).

내부 여전히는 `if` 블록을 뒤에 다음 줄 추가 `db.Execute` 줄:

[!code-css[Main](entering-data/samples/sample4.css)]

새 동영상 데이터베이스에 삽입 한 후이 선 점프 있습니다 (리디렉션을)는 *동영상* 페이지 방금 입력 한 동영상을 볼 수 있도록 합니다. `~` 연산자 의미 "웹 사이트의 루트입니다." (의 `~` 연산자 일반적으로 HTML에 없는 ASP.NET 페이지 에서만에서 작동 합니다.)

이 예제와 같이 전체 코드 블록:

[!code-cshtml[Main](entering-data/samples/sample5.cshtml)]

## <a name="testing-the-insert-command-so-far"></a>Insert 명령 (지금까지) 테스트

아직 완료 되지 않았음을 하지만 이제는 것이 테스트할 수 있습니다.

WebMatrix에 있는 파일의 트리 뷰에서 마우스 오른쪽 단추로 클릭는 *AddMovie.cshtml* 페이지 한 다음 클릭 **브라우저에서 시작**합니다.

![브라우저에서 영화 추가' 페이지](entering-data/_static/image2.png)

(브라우저에서 다른 페이지와 /fd 경우 URL이 있는지 확인 `http://localhost:nnnnn/AddMovie`) 여기서 *nnnnn* 사용 중인 포트 번호입니다.)

오류 페이지 어? 그렇다면 읽어 주십시오. 하 고 앞에 나열 된 어떤 코드 정확 하 게 표시 되는지 확인 합니다.

동영상 형식으로 입력 &mdash; 예를 들어 "시민 마 창", "드라마" 및 "1941"를 사용 합니다. 키나 합니다. 클릭 **동영상 추가**합니다.

때로 리디렉션되 하는 모든 코드가 정상적으로 작동 하는 경우는 *동영상* 페이지. 새 동영상 표시 되어 있는지 확인 합니다.

![동영상 페이지 새로 보여 주는 동영상 추가](entering-data/_static/image3.png)

## <a name="validating-user-input"></a>사용자 입력 유효성 검사

로 돌아가기는 *AddMovie* 페이지 또는 다시 실행 합니다. 제목을 입력, 다른 동영상 하지만이 이번 입력 &mdash; 예를 들어 "비에서 시스템을 사용해 봅시다 '"을 입력 합니다. 클릭 **동영상 추가**합니다.

리디렉션됩니다 하는 *동영상* 페이지를 다시 합니다. 새 동영상을 찾을 수 있지만 완료 되지 않았습니다.

![특정 값이 없는 동영상 페이지 보여 주는 새 동영상](entering-data/_static/image4.png)

만들 때의 *동영상* 테이블을 명시적으로 라고 하는 필드는 null 일 수 있습니다. 여기서 새 동영상에 대 한 입력 양식 있고 있습니다 하는 필드를 비워 있습니다. 가 오류가 발생 합니다.

이 경우 데이터베이스 실제로 발생 하지 않은 (또는 *throw*) 오류가 발생 합니다. 장르 또는 연도별로 하므로 제공 하지 않은 코드에는 *AddMovie* 페이지 소위으로 해당 값을 처리 *빈 문자열과*합니다. 때 SQL `Insert Into` 명령이 실행, genre 및 year 필드에 유용한 데이터가 포함 되어 있지 않습니다 되지만 null 되지 않았습니다.

물론, 사용자가 데이터베이스에 비어 있지 절반 영화 정보를 입력 하지 않으려면입니다. 솔루션은 사용자의 입력을 확인 하는 것입니다. 처음에 유효성 검사는 단순히 있는지 확인은 사용자가 모든 필드에 대 한 값을 입력 했는지 (즉, 않은 빈 문자열을 포함).

> [!TIP]
> 
> **Null 및 빈 문자열**
> 
> 프로그래밍에서 다른 개념 "값이 없습니다."의 구별 값은 일반적으로 *null* 설정 하거나 어떤 방식으로든에서 초기화 되지 한 경우. 반면 문자 데이터 (문자열)를 필요로 하는 변수를 설정할 수 있습니다는 *빈 문자열*합니다. 값이 null입니다;이 경우 것은 바로 명시적으로 설정 되어 길이가 0 인 자의 문자열입니다. 다음 두 문은 차이 보여 줍니다.
> 
> [!code-csharp[Main](entering-data/samples/sample6.cs)]
> 
> 이보다 더 복잡 약간 하지만 중요 한 점은 `null` 결정 되지 않은 상태로의 종류를 나타냅니다.
> 
> 값이 null 및 빈 문자열이 방금 때 정확히 이해 해야 하는 합니다. 에 대 한 코드에는 *AddMovie* 를 사용 하 여 텍스트 상자의 값을 가져오기 페이지 `Request.Form["title"]` 등입니다. 값 때 페이지를 처음 실행할 (단추를 클릭) 전에 `Request.Form["title"]` null입니다. 폼을 제출 하면 하지만 `Request.Form["title"]` 의 값을 가져옵니다는 `title` 입력란. 확실 하지는 않지만 빈 입력란; null이 아닌 방금를 빈 문자열을 받았습니다. 따라서 단추에 대 한 응답에서 코드를 실행할 때 클릭, `Request.Form["title"]` 에 빈 문자열입니다.
> 
> 이러한 차이점으로이 인해 중요 한 이유는 무엇입니까? 만들 때의 *동영상* 테이블을 명시적으로 라고 하는 필드는 null 일 수 있습니다. 새 동영상에 대 한 항목 양식이 있는 여기 있고 있습니다 하는 필드를 비워 합니다. 장르 또는 연도 대 한 값이 없는 새 동영상을 저장 하려고 할 때 불만을 제기 데이터베이스 합리적인 기대 합니다. 내용이 충분 하지만 &mdash; 는 값이 null 않은 텍스트 상자를 비워 두면 하는 경우에로 빈 문자열을 수 있습니다. 새 동영상 빈 이러한 열이 있는 데이터베이스에 저장할 수는 결과적으로, &mdash; 있지만 null이 아님! &mdash; 값 따라서 사용자가 사용자의 입력을 확인 하 여 수행할 수 있는 빈 문자열을 제출 하지 않으면 있는지 확인 해야 합니다.


### <a name="the-validation-helper"></a>유효성 검사 도우미

도우미 메서드를 포함 하는 ASP.NET 웹 페이지 &mdash; 는 `Validation` 도우미 &mdash; 사용자가 입력 요구 사항을 충족 하는 데이터를 사용할 수 있습니다. `Validation` 도우미에 기본 제공 되 ASP.NET 웹 페이지를 하므로 이전 자습서에서 Gravatar 도우미를 설치 하는 방법을 NuGet을 사용 하 여 패키지도 설치할 필요가 없습니다 도우미 중 하나입니다.

사용자 입력의 유효성을 검사 하려면 다음을 수행 합니다.

- 코드를 사용 하 여 페이지에 텍스트 상자에 필요한 값이 되도록 지정 합니다.
- 모든 항목이 제대로 확인 하는 경우에 데이터베이스에 동영상 정보를 추가 하는 테스트 코드에 들어가는 합니다.
- 오류 메시지를 표시 하는 태그에 코드를 추가 합니다.

에 있는 코드 블록에는 *AddMovie* 페이지에서 오른쪽 위 위쪽 변수 선언 앞에 다음 코드를 추가 합니다.

[!code-csharp[Main](entering-data/samples/sample7.cs)]

호출 하면 `Validation.RequireField` 각 필드에 대해 한 번씩 (`<input>` 요소)는 입력을 요구 하려면. 여기에서 보는 것 처럼 각 호출에 대 한 사용자 지정 오류 메시지를 추가할 수 있습니다. (여기서 다양 한 메시지 수를 두는 원하는 있습니다 보여 주기 위해 있습니다.)

문제가 있는 경우 새 동영상 정보가 데이터베이스에 삽입 되지 않도록 하려면. 에 `if(IsPost)` 블록을 사용 하 여 `&&` 테스트 하는 다른 조건을 추가 하려면 (논리적 AND) `Validation.IsValid()`합니다. 완료 하면, 전체 `if(IsPost)` 블록이이 코드와 비슷합니다.

[!code-csharp[Main](entering-data/samples/sample8.cs)]

사용 하 여 등록 하는 필드를 사용 하 여 유효성 검사 오류가 있는 경우는 `Validation` 도우미에는 `Validation.IsValid` 메서드에서 false를 반환 합니다. 및이 경우 해당 블록의 코드 중를 실행 하므로 잘못 된 동영상 항목이 없습니다. 데이터베이스에 삽입 됩니다. 에 하지 리디렉션 됨 물론 및는 *동영상* 페이지.

이제 유효성 검사 코드를 포함 한 전체 코드 블록을이 예제에서와 같이 표시 됩니다.

[!code-cshtml[Main](entering-data/samples/sample9.cshtml?highlight=10)]

## <a name="displaying-validation-errors"></a>유효성 검사 오류 표시

오류 메시지를 표시 하는 마지막 단계가입니다. 각 유효성 검사 오류에 대 한 개별 메시지를 나타내거나, 요약 또는 둘 모두를 표시할 수 있습니다. 이 자습서에서 수행 합니다 둘 다 어떻게 작동 하는지 확인할 수 있도록 합니다.

각 옆에 있는 `<input>` 유효성을 검사 하는 요소, 호출의 `Html.ValidationMessage` 메서드의 이름을 전달 하 고는 `<input>` 유효성을 검사 하는 요소입니다. 배치는 `Html.ValidationMessage` 오류 메시지를 표시 하려는 메서드를 오른쪽입니다. 페이지 실행 하는 경우, `Html.ValidationMessage` 메서드 렌더링은 `<span>` 요소 유효성 검사 오류가 이동 됩니다. (오류가 없는 경우는 `<span>` 요소가 렌더링 하지만에 텍스트가 없습니다.)

포함 되도록 페이지의 태그를 변경는 `Html.ValidationMessage` 세 개의 각 방법을 `<input>` 이 예제에서와 같이 요소 페이지에서:

[!code-cshtml[Main](entering-data/samples/sample10.cshtml?highlight=3,8,13)]

요약 작동 하는 방법을 보려면, 또한 다음 태그를 추가 및 코드 바로 뒤의 `<h1>Add a Movie</h1>` 페이지에서 요소:

[!code-cshtml[Main](entering-data/samples/sample11.cshtml)]

기본적으로는 `Html.ValidationSummary` 메서드 목록에 모든 유효성 검사 메시지를 표시 합니다 (한 `<ul>` 내에 있는 요소는 `<div>` 요소). 과 마찬가지로 `Html.ValidationMessage` 메서드를 유효성 검사 요약에 대 한 태그는 항상 렌더링; 오류가 경우 목록 항목이 렌더링 됩니다.

요약을 사용 하 여 대신 유효성 검사 메시지를 표시 하는 다른 방법으로 일 수 있습니다는 `Html.ValidationMessage` 메서드를 각 필드 관련 오류를 표시 합니다. 또는 요약 및 세부 정보를 모두 사용할 수 있습니다. 또는 사용할 수 있습니다는 `Html.ValidationSummary` 메서드를 일반 오류를 표시 한 다음 개별 사용 하 여 `Html.ValidationMessage` 호출 정보를 표시 합니다.

이제 완료 페이지이 예제에서와 같이 표시 됩니다.

[!code-cshtml[Main](entering-data/samples/sample12.cshtml)]

이제 이제 필드 중 하나 이상 그대로 동영상을 추가 하 여 페이지를 테스트할 수 있습니다. 이렇게 하면 다음과 같은 오류가 표시 참조:

![유효성 검사 오류 메시지를 보여 주는 동영상 페이지 추가](entering-data/_static/image5.png)

## <a name="styling-the-validation-error-messages"></a>유효성 검사 오류 메시지의 스타일 지정

오류 메시지, 있지만 하지 실제로 서식을 상태일 때 잘 확인할 수 있습니다. 그러나 오류 메시지, 스타일을 지정 하는 쉬운 방법이 있습니다.

개별 오류 메시지에 표시 되는 스타일을 지정 하려면 `Html.ValidationMessage`, 이라는 CSS 스타일 클래스를 만들 `field-validation-error`합니다. 유효성 검사 요약에 대 한 보기를 정의 하려면 이라는 CSS 스타일 클래스를 만들 `validation-summary-errors`합니다.

이 기술은 작동 방식을 보려면 추가 `<style>` 요소 안에 `<head>` 페이지의 섹션입니다. 그런 다음 명명 된 스타일 클래스를 정의 `field-validation-error` 및 `validation-summary-errors` 다음 규칙을 포함 하는 합니다.

[!code-cshtml[Main](entering-data/samples/sample13.cshtml?highlight=4-17)]

일반적으로 추가할 수 있습니다를 별도의 스타일 정보 *.css* 파일인 편의상 배치할 수 있는 페이지에 지금은 하지만 합니다. (이 자습서 집합의 뒷부분에 나오는 이동 CSS 규칙은 별도의 *.css* 파일입니다.)

유효성 검사 오류가 있는 경우는 `Html.ValidationMessage` 메서드 렌더링 되는 `<span>` 포함 된 요소 `class="field-validation-error"`합니다. 해당 클래스에 대 한 스타일 정의 추가 하 여 메시지 모양을 구성할 수 있습니다. 오류가 있는 경우는 `ValidationSummary` 메서드 특성을 동적으로 마찬가지로 렌더링 `class="validation-summary-errors"`합니다.

페이지를 다시 실행 하 고 필드의 두 의도적으로 그대로 둡니다. 오류 정보에서 더욱 분명 하 게 됩니다. (실제로 이러한 overdone 하는, 수 있지만 수행할 수 있는 작업을 보여 주기 위해.)

![스타일을 지정 하는 유효성 검사 오류를 보여 주는 동영상 페이지 추가](entering-data/_static/image6.png)

## <a name="adding-a-link-to-the-movies-page"></a>동영상 페이지의 링크를 추가합니다.

하나의 마지막 단계를 편리 하 게 하는 *AddMovie* 원래 영화 목록에서 페이지입니다.

열기는 *동영상* 페이지를 다시 합니다. 닫은 후 `</div>` 태그 뒤에 오는 `WebGrid` 도우미에 다음 태그를 추가 합니다.

[!code-cshtml[Main](entering-data/samples/sample14.cshtml)]

ASP.NET을 해석 하기 전에 본 것 처럼는 `~` 연산자는 웹 사이트의 루트 라고 합니다. 사용할 필요가 없습니다는 `~` 연산자;는 태그를 사용할 수 있습니다 `<a href="./AddMovie">Add a movie</a>` 또는 HTML 이해할 수 있는 경로 정의 하는 다른 방법이 있습니다. 하지만 `~` 연산자는 일반적인 접근 방식이 효과적 Razor 페이지에 대 한 링크를 만들 때 사이트를 보다 유연한 만들므로-하위 폴더에 현재 페이지를 이동 하는 경우 링크가 여전히 들어가는지는 *AddMovie* 페이지. (에 유의 해야는 `~` 연산자만 작동 *.cshtml* 페이지입니다. ASP.NET에 대 한 이해를 있지만 표준 HTML 아닙니다.)

완료 되 면 실행는 *동영상* 페이지. 이이 페이지와 같습니다.

![동영상 추가 ' 페이지에는 링크가 포함 된 동영상 페이지](entering-data/_static/image7.png)

클릭는 **동영상 추가** 이동 하는지 확인 하는 링크는 *AddMovie* 페이지.

## <a name="coming-up-next"></a>다음에 나오는

다음 자습서에서는 사용자가 데이터베이스에 이미 있는 데이터를 편집할 수 있도록 하는 방법을 설명 합니다.

## <a name="complete-listing-for-addmovie-page"></a>AddMovie 페이지에 대 한 전체 목록을 보려면

[!code-cshtml[Main](entering-data/samples/sample15.cshtml)]

## <a name="additional-resources"></a>추가 자료

- [Razor 구문을 사용 하 여 ASP.NET 웹 프로그래밍 소개](https://go.microsoft.com/fwlink/?LinkID=202890)
- [INTO 문을 SQL 삽입](http://www.w3schools.com/sql/sql_insert.asp) W3Schools 사이트
- [사이트 페이지에서 ASP.NET 웹 사용자 입력 유효성 검사](https://go.microsoft.com/fwlink/?LinkId=253002)합니다. 작업에 대 한 자세한 정보는 `Validation` 도우미입니다.

> [!div class="step-by-step"]
> [이전](form-basics.md)
> [다음](updating-data.md)
