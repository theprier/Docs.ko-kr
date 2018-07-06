---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/entering-data
title: ASP.NET 웹 페이지 소개-Forms를 사용 하 여 데이터베이스 데이터를 입력 합니다. | Microsoft Docs
author: tfitzmac
description: 이 자습서 입력 폼을 만들고 다음 얻을 수 있는 폼에서 데이터베이스 테이블에 ASP.NET 웹 페이지 (...를 사용할 때 데이터를 입력 하는 방법을 보여 줍니다.
ms.author: aspnetcontent
ms.date: 05/28/2015
ms.assetid: d37c93fc-25fd-4e94-8671-0d437beef206
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/entering-data
msc.type: authoredcontent
ms.openlocfilehash: 313fd6ff70af540d4dd749734f50e3fc24be0d29
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37835763"
---
<a name="introducing-aspnet-web-pages---entering-database-data-by-using-forms"></a>ASP.NET 웹 페이지 소개-Forms를 사용 하 여 데이터베이스 데이터를 입력 합니다.
====================
[Tom FitzMacken](https://github.com/tfitzmac)

> 이 자습서에서는 입력 폼을 만들고 다음 얻을 수 있는 폼에서 데이터베이스 테이블에 ASP.NET Web Pages (Razor)를 사용 하는 경우 데이터를 입력 하는 방법을 보여 줍니다. 통해 시리즈를 완료 했다고 가정 하 [기본 사항의 HTML 폼 ASP.NET 웹 페이지에서](https://go.microsoft.com/fwlink/?LinkId=251581)합니다.
> 
> 학습할 내용:
> 
> - 입력 폼을 처리 하는 방법에 대해 자세히 살펴보겠습니다.
> - 데이터베이스의 데이터 (삽입)를 추가 하는 방법입니다.
> - 사용자 (사용자 입력의 유효성을 검사 하는 방법) 형태로 필요한 값을 입력 하 고 있는지 확인 하는 방법.
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


## <a name="what-youll-build"></a>만들 내용

자습서 이전 데이터베이스를 만드는 방법에 알아보았습니다는 WebMatrix에서 작업에서 직접 데이터베이스를 편집 하 여 데이터베이스 데이터 입력을 **데이터베이스** 작업 영역입니다. 대부분의 앱에 없는 하지만 데이터베이스에 데이터를 저장 하는 실용적인 방법이 있습니다. 따라서이 자습서에서는 모든 사용자 데이터를 입력 하 고 데이터베이스에 저장할 수 있는 웹 기반 인터페이스를 만듭니다.

새 영화를 입력할 수 있는 페이지를 만들어야 합니다. 페이지 입력 폼을 영화 제목, genre 및 연도 입력할 수 있는 필드 (입력란)가 포함 됩니다. 페이지는이 페이지와 같습니다.

![브라우저에서 페이지 동영상 추가'](entering-data/_static/image1.png)

텍스트 상자에는 HTML 됩니다 `<input>` 요소를 찾는 등이 태그:

`<input type="text" name="genre" value="" />`

## <a name="creating-the-basic-entry-form"></a>기본 입력 양식 만들기

라는 페이지를 만듭니다 *AddMovie.cshtml*합니다.

다음 태그를 사용 하 여 파일에 포함 된 내용으로 바꿉니다. 모든; 덮어쓰기 맨 위에 있는 코드 블록을 곧 추가 합니다.

[!code-cshtml[Main](entering-data/samples/sample1.cshtml)]

이 예제에서는 일반적인 HTML 양식 만들기 사용 하 여 `<input>` 제출 단추 및 텍스트 상자에 대 한 요소입니다. 텍스트 상자에 대 한 캡션을 standard를 사용 하 여 만들어진 `<label>` 요소입니다. 합니다 `<fieldset>` 및 `<legend>` 요소 폼 주위에 유용한 상자를 배치 합니다.

이 페이지에서의 `<form>` 요소를 사용 하 여 `post` 값으로는 `method` 특성입니다. 이전 자습서에서 사용 하는 양식을 만든를 `get` 메서드. 양식이 제출 값을 서버에 있지만 요청 변경 하지 않았으면 모든 때문에 올바른 했습니다. 수행한 모든 다양 한 방법으로 데이터를 가져오고 했습니다. 그러나이 페이지 *는* 변경-새 데이터베이스 레코드를 추가 하려고 합니다. 따라서이 양식을 사용 해야는 `post` 메서드. (간의 차이점에 대 한 자세한 `GET` 및 `POST` 작업을 참조 하세요 합니다[GET, POST 및 HTTP 동사 안전](https://go.microsoft.com/fwlink/?LinkId=251581#GET,_POST,_and_HTTP_Verb_Safety) 이전 자습서에서 세로 막대입니다.)

각 텍스트 상자에는 한 `name` 요소 (`title`를 `genre`, `year`). 이전 자습서에서 살펴본 것 처럼 사용자의 입력을 나중에 받을 수 있도록 해당 이름이 있어야 하기 때문에 이러한 이름을 중요 합니다. 모든 이름을 사용할 수 있습니다. 하는 것이 좋습니다 도움이 되는 의미 있는 이름을 사용 하 여 작업할 때 어떤 데이터를 저장 합니다.

합니다 `value` 각각의 특성 `<input>` Razor 코드의 비트를 포함 하는 요소 (예를 들어 `Request.Form["title"]`). 양식이 제출 되 면 (있는 경우) 텍스트 상자에 입력 한 값을 보존 하려면 이전 자습서에서이 방법의 버전을 배웠습니다.

## <a name="getting-the-form-values"></a>폼 값 가져오기

그런 다음 양식을 처리는 코드를 추가 합니다. 개요에서 다음을 수행할 수 있습니다.

1. 페이지가 게시 되 고 있는지 여부를 확인 (제출). 코드를 실행 하려는 페이지를 처음 실행할 때가 아니라 사용자가 단추를 클릭 하는 경우에 합니다.
2. 사용자가 텍스트 상자에 입력 한 값을 가져옵니다. 이 경우 폼 사용 중이기 때문에 `POST` 에서 양식 값을 얻으려면 동사는 `Request.Form` 컬렉션입니다.
3. 값에서 새 레코드를 삽입 합니다 *영화* 데이터베이스 테이블입니다.

파일의 맨 위에 있는 다음 코드를 추가 합니다.

[!code-cshtml[Main](entering-data/samples/sample2.cshtml)]

처음 몇 줄 변수를 만듭니다 (`title`, `genre`, 및 `year`) 텍스트 상자에서 값을 보유 하 합니다. 줄 `if(IsPost)` 변수 설정 되어 있는지를 사용 하면 *만* 사용자가 클릭 하면는 **동영상 추가** 단추-즉, 경우 폼이 게시 된 합니다.

와 같은 식을 사용 하 여 입력란의 값을 가져올 이전 자습서에서 살펴본 것 처럼 `Request.Form["name"]`여기서 *이름* 이름인는 `<input>` 요소입니다.

변수 이름 (`title`, `genre`, 및 `year`)는 임의로 결정 합니다. 에 할당 하는 이름이 마음에 `<input>` 요소를 원하는 대로 호출할 수 있습니다. (이름 특성에 맞게 변수 이름이 없는 `<input>` 폼에서 요소가.) 하지만와 마찬가지로 `<input>` 요소인 것이 포함 된 데이터를 반영 하는 변수 이름을 사용 하는 것이 좋습니다. 코드를 작성할 때 일관 된 이름을 쉽게 사용 하는 데이터를 기억할 수 있습니다.

## <a name="adding-data-to-the-database"></a>데이터베이스에 데이터 추가

코드에서 차단 하면 방금 추가한 *내* 닫는 중괄호 ( `}` )의 `if` 다음 코드를 추가 합니다 (뿐 아니라 코드 블록) 내에서 차단:

[!code-csharp[Main](entering-data/samples/sample3.cs)]

이 예제에서는 데이터를 인출 하 고 표시 하는 이전 자습서에서 사용 되는 코드와 비슷합니다. 로 시작 하는 줄 `db =` 열립니다 이전과 같은 데이터베이스 및 다음 줄으로 SQL 문을 다시 정의 하기 전에 확인 합니다. 그러나이 이번 정의 SQL `Insert Into` 문입니다. 다음 예제에서는 일반 구문을 보여 줍니다는 `Insert Into` 문:

`INSERT INTO table (column1, column2, column3, ...) VALUES (value1, value2, value3, ...)`

즉, 다음을 삽입할 열을 나열 하 고 다음 삽입할 값에를 나열 하는 테이블에 삽입을 지정 합니다. (앞에서 설명한 것 처럼 SQL 대/소문자 구분 되지 않지만 쉽게 명령을 읽을 수 있도록 키워드를 활용 하는 사람도.)

열에 삽입 하는 명령에 이미 나열 된- `(Title, Genre, Year)`합니다. 흥미로운 부분은에 텍스트 상자에서 값을 얻는 방법의 `VALUES` 명령의 일부입니다. 실제 값 대신 참조 하세요 `@0`, `@1`, 및 `@2`는 물론 자리 표시자입니다. 명령을 실행 하는 경우 (에 `db.Execute` 줄), 텍스트 상자에서 가져온 값을 전달 합니다.

**중요!** 다음과 같이 온라인 SQL 문에서 사용자가 입력 한 데이터를 그 어느 때 포함 해야 하는 유일한 방법은 자리 표시자를 사용 하는 (`VALUES(@0, @1, @2)`). SQL 문으로 사용자 입력을 연결 하면 열면 직접 SQL 주입 공격을 하려면에 설명 된 대로 [양식 기본 ASP.NET 웹 페이지에서](https://go.microsoft.com/fwlink/?LinkId=251581) (이전 자습서).

여전히 내 합니다 `if` 차단, 뒤에 다음 줄을 추가 합니다 `db.Execute` 줄:

[!code-css[Main](entering-data/samples/sample4.css)]

새 영화 데이터베이스에 삽입 한 후이 줄 이동 (리디렉션) 하는 *영화* 방금 입력 한 영화를 볼 수 있도록 페이지입니다. `~` 연산자 "웹 사이트의 루트입니다."를 의미 합니다. (의 `~` 연산자 일반적으로 HTML에 없는 ASP.NET 페이지 에서만에서 작동 합니다.)

전체 코드 블록을이 예제와 비슷합니다.

[!code-cshtml[Main](entering-data/samples/sample5.cshtml)]

## <a name="testing-the-insert-command-so-far"></a>Insert 명령이 (지금) 테스트

아직 완료 되지 않은 하지만 이제 좋습니다를 테스트할 수 있습니다.

WebMatrix에는 파일의 트리 뷰에서 마우스 오른쪽 단추로 클릭 합니다 *AddMovie.cshtml* 페이지를 클릭 한 다음 **브라우저에서 시작**합니다.

![브라우저에서 페이지 동영상 추가'](entering-data/_static/image2.png)

(브라우저에서 다른 페이지를 사용 하 여 결국 경우 URL이 있는지 확인 `http://localhost:nnnnn/AddMovie`), 여기서 *nnnnn* 사용 중인 포트 번호입니다.)

오류 페이지 했나요? 그렇다면 신중 하 게 읽고 앞에 나열 된 어떤 코드를 정확히 표시 되는지 확인 합니다.

동영상 형태로 입력 &mdash; 예를 들어, "시민 마 창", "드라마" 및 "1941"를 사용 합니다. (또는 모든) 누른 **영화 추가**합니다.

로 리디렉션됩니다 정상적으로 작동 하는 경우는 *영화* 페이지입니다. 새 동영상 표시 되어 있는지 확인 합니다.

![동영상 페이지 새로 보여 주는 동영상 추가](entering-data/_static/image3.png)

## <a name="validating-user-input"></a>사용자 입력 유효성 검사

로 다시 이동 합니다 *AddMovie* 페이지 또는 다시 실행 합니다. 다른 영화 이번 입력만 제목을 입력 합니다 &mdash; 예를 들어, "Rain에서 시스템을 사용해 봅시다 '"을 입력 합니다. 누른 **영화 추가**합니다.

로 리디렉션됩니다 합니다 *영화* 페이지를 다시 합니다. 새 동영상을 찾을 수 있지만 완전 하지 않습니다.

![영화 없거나 일부 값을 보여 주는 새 동영상 페이지](entering-data/_static/image4.png)

만들 때 합니다 *영화* 테이블을 명시적으로 말씀 하 신 null 수 필드 없음. 여기 새 영화에 대 한 입력 폼 있고 필드를 비워 두면 하 고 있습니다. 오류입니다.

이 경우 데이터베이스 실제로 발생 하지 않은 (또는 *throw*) 오류가 발생 합니다. 장르 또는 연도 따라서 제공 하지 않은 코드를 *AddMovie* 페이지 소위로 해당 값을 처리 *빈 문자열*합니다. 때 SQL `Insert Into` 명령 실행, genre 및 year 필드에 유용한 데이터가 들어 있지 않은 되었지만 null 되지 않았습니다.

물론 사용자가 데이터베이스에 절반 빈 영화 정보를 입력할 수 있도록 원하지입니다. 솔루션은 사용자 입력의 유효성을 검사 하는 것입니다. 처음에 유효성 검사는 단순히 해야 사용자가 모든 필드에 대 한 값을 입력 했는지 (즉, 않은 빈 문자열을 포함).

> [!TIP]
> 
> **Null 및 빈 문자열**
> 
> 프로그래밍에는 "값이 없습니다." 다른 개념 구분 값은 일반적으로 *null* 설정 하거나 어떤 방식으로든에서 초기화할 되지 한 경우. 반면 문자 데이터 (문자열)를 필요로 하는 변수를 설정할 수 있습니다는 *빈 문자열*합니다. 이런 경우 값 null이 아닙니다. 이 방금 명시적으로 설정 된 길이가 0 인 문자의 문자열로. 다음 두 문은 차이 보여 줍니다.
> 
> [!code-csharp[Main](entering-data/samples/sample6.cs)]
> 
> 이보다 더 복잡 약간 이지만 중요 한 점은 `null` 일종의 결정 되지 않은 상태를 나타냅니다.
> 
> 값이 null 및 빈 문자열만 때 정확 하 게 이해 해야 하는 고 합니다. 코드에 *AddMovie* 페이지에서 얻게 입력란의 값을 사용 하 여 `Request.Form["title"]` 등. 경우 페이지 처음 (되기 전에 실행 단추를 클릭 하면), 값 `Request.Form["title"]` null입니다. 폼을 제출 하지만 `Request.Form["title"]` 의 값을 가져옵니다는 `title` 입력란입니다. 당연 하 게 되지 않지만 빈 입력란 isnotnull; 방금에 빈 문자열을 포함 합니다. 단추에 대 한 응답에서 코드를 실행할 때, 클릭 `Request.Form["title"]` 에 빈 문자열을 포함 합니다.
> 
> 이러한 차이점으로이 인해 중요 한 이유는 무엇입니까? 만들 때 합니다 *영화* 테이블을 명시적으로 말씀 하 신 null 수 필드 없음. 하지만 여기 새 영화에 대 한 입력 폼 있고 필드를 비워 두면 하 고 있습니다. 장르 또는 연도 대 한 값이 있는 하지 않은 새 동영상을 저장 하려고 할 때 불만을 데이터베이스 합리적으로 예상할 수 있습니다. 점 이지만 &mdash; 빈 문자열 이기 때문에 해당 텍스트 상자를 비워 두면 하는 경우에 값을 null 되지 않습니다. 빈 이러한 열을 사용 하 여 데이터베이스에 새 영화를 저장할 수는 결과적으로, &mdash; 있지만 null이 아님! &mdash; 값 따라서 사용자가 사용자 입력의 유효성을 검사 하 여 수행할 수 있는 빈 문자열인 경우를 제출 하지 있는지 확인 해야 합니다.


### <a name="the-validation-helper"></a>유효성 검사 도우미

ASP.NET 웹 페이지 도우미가 포함 됩니다 &mdash; 는 `Validation` 도우미 &mdash; 사용자 입력 요구 사항을 충족 하는 데이터를 사용할 수 있습니다. `Validation` 도우미에서 빌드하는 ASP.NET 웹 페이지에 이전 자습서에서 Gravatar 도우미를 설치 하는 방법은 NuGet을 사용 하 여 패키지로 설치할 필요가 도우미 중 하나입니다.

사용자 입력의 유효성을 검사 하려면 다음을 수행 합니다.

- 코드를 사용 하 여 페이지의 입력란에 필요한 값이 되도록 지정 합니다.
- 모든 항목이 제대로 확인 하는 경우에 동영상 정보가 데이터베이스에 추가 됩니다 있도록 코드에 테스트를 배치 합니다.
- 오류 메시지를 표시 하는 태그에 코드를 추가 합니다.

코드 블록에는 *AddMovie* 페이지에서 오른쪽 위 변수 선언 앞 맨 위에 있는 다음 코드를 추가 합니다.

[!code-csharp[Main](entering-data/samples/sample7.cs)]

문의할 `Validation.RequireField` 각 필드에 한 번씩 (`<input>` 요소)를 입력 해야 하는 하려는 합니다. 또한 다음과 같은 각 호출에 대 한 사용자 지정 오류 메시지를 추가할 수 있습니다. (에서는 다양 한 메시지를 저장할 수 원하는 것을 보여 줍니다.)

문제가 있으면 새 동영상 정보가 데이터베이스에 삽입 되지 않도록 하려고 합니다. 에 `if(IsPost)` 블록에서 사용 하 여 `&&` (논리적 AND) 테스트 하는 다른 조건을 추가 하려면 `Validation.IsValid()`합니다. 완료 되 면, 전체 `if(IsPost)` 블록이이 코드와 같습니다.

[!code-csharp[Main](entering-data/samples/sample8.cs)]

사용 하 여 등록 하는 필드 중 하나를 사용 하 여 유효성 검사 오류가 있을 경우 합니다 `Validation` 도우미를 `Validation.IsValid` 메서드에서 false를 반환 합니다. 및 이런 경우 해당 블록의 코드 없음은 실행, 되므로 잘못 된 영화 항목이 없는 데이터베이스에 삽입 됩니다. 물론 하지로 리디렉션됩니다 및 합니다 *영화* 페이지입니다.

유효성 검사 코드를 포함 한 전체 코드 블록은 이제이 예제와 비슷합니다.

[!code-cshtml[Main](entering-data/samples/sample9.cshtml?highlight=10)]

## <a name="displaying-validation-errors"></a>유효성 검사 오류를 표시합니다.

마지막 단계는 모든 오류 메시지를 표시 하는 것입니다. 각 유효성 검사 오류에 대 한 개별 메시지를 표시할 수 있습니다 또는 요약 하자면, 또는 둘 다 표시할 수 있습니다. 이 자습서에서는 수행 둘 다 작동 방식을 볼 수 있도록 합니다.

각 옆에 있는 `<input>` 유효성을 검사 하는 요소를 호출 합니다 `Html.ValidationMessage` 메서드의 이름을 전달 하 고는 `<input>` 유효성을 검사 하는 요소입니다. 배치는 `Html.ValidationMessage` 오류 메시지를 표시 하려는 메서드를 오른쪽입니다. 페이지를 실행 하는 경우, `Html.ValidationMessage` 메서드 렌더링을 `<span>` 유효성 검사 오류를 어디로 요소입니다. (오류가 없는 경우는 `<span>` 요소가 렌더링 하지만에 텍스트가 없습니다.)

페이지의 태그를 포함 하도록 변경를 `Html.ValidationMessage` 메서드는 세 가지에 대 한 `<input>` 이 예제에서와 같이 페이지의 요소:

[!code-cshtml[Main](entering-data/samples/sample10.cshtml?highlight=3,8,13)]

요약의 작동 원리를 보려면도 다음 태그를 추가 하 고 바로 뒤에 있는 코드는 `<h1>Add a Movie</h1>` 페이지의 요소:

[!code-cshtml[Main](entering-data/samples/sample11.cshtml)]

기본적으로 `Html.ValidationSummary` 목록의 모든 유효성 검사 메시지를 표시 하는 메서드 (을 `<ul>` 내에 있는 요소를 `<div>` 요소). 와 마찬가지로 `Html.ValidationMessage` 메서드는 항상 유효성 검사 요약에 대 한 태그를 렌더링; 오류가 없는 경우에 목록 항목이 렌더링 됩니다.

요약을 사용 하 여 대신 유효성 검사 메시지를 표시 하는 다른 방법은 수는 `Html.ValidationMessage` 각 필드 관련 오류를 표시 하는 방법입니다. 또는 요약 및 세부 정보를 모두 사용할 수 있습니다. 또는 사용할 수 있습니다는 `Html.ValidationSummary` 메서드를 일반 오류를 표시 하 고 사용 하 여 개별 `Html.ValidationMessage` 호출 세부 정보를 표시 합니다.

완료 페이지는 이제이 예제와 비슷합니다.

[!code-cshtml[Main](entering-data/samples/sample12.cshtml)]

이제 이제 영화를 추가 하지만 하나 이상의 필드에서 페이지를 테스트할 수 있습니다. 이렇게 하면 다음 오류가 표시 표시:

![유효성 검사 오류 메시지를 보여 주는 동영상 페이지 추가](entering-data/_static/image5.png)

## <a name="styling-the-validation-error-messages"></a>유효성 검사 오류 메시지의 스타일 지정

오류 메시지, 있지만 이러한 없는 소개할 잘 볼 수 있습니다. 하지만 오류 메시지의 스타일을 지정 하는 쉬운 방법이 있습니다.

개별 오류 메시지에 표시 되는 스타일을 지정 하려면 `Html.ValidationMessage`, 명명 된 CSS 스타일 클래스를 만듭니다 `field-validation-error`합니다. 유효성 검사 요약에 대 한 모양을 정의 만들려면 CSS 스타일 클래스가 `validation-summary-errors`합니다.

이 기술은 작동 방식을 확인 하려면 추가 `<style>` 내부 요소는 `<head>` 페이지의 섹션입니다. 그런 다음 이라는 스타일 클래스를 정의 `field-validation-error` 고 `validation-summary-errors` 다음 규칙을 포함 하는:

[!code-cshtml[Main](entering-data/samples/sample13.cshtml?highlight=4-17)]

일반적으로 추가할 수 있습니다를 별도의 스타일 정보 *.css* 파일을 간단 하 게 배치할 수 있는 페이지에 이제 있지만. (이 자습서 집합의 뒷부분에 나오는 별도의 CSS 규칙 이동해 봅니다 *.css* 파일입니다.)

유효성 검사 오류가 있을 경우는 `Html.ValidationMessage` 렌더링 메서드를 `<span>` 요소를 포함 하는 `class="field-validation-error"`합니다. 해당 클래스에 대 한 스타일 정의 추가 하 여 메시지 모양을 구성할 수 있습니다. 오류가 있을 경우 합니다 `ValidationSummary` 메서드는 동적으로 마찬가지로 특성을 렌더링 `class="validation-summary-errors"`합니다.

페이지를 다시 실행 하 고 몇 가지 필드를 의도적으로 생략 합니다. 오류를 좀 더 눈에 띄는 됩니다. (실제로 overdone 하 고, 이지만 수행할 수 있는 작업을 보여 줍니다.)

![스타일을 지정 하는 유효성 검사 오류를 보여 주는 동영상 페이지 추가](entering-data/_static/image6.png)

## <a name="adding-a-link-to-the-movies-page"></a>Movies 페이지로 링크를 추가합니다.

마지막 단계는 이동에 편리 하 게 합니다 *AddMovie* 원래 영화 목록에서 페이지입니다.

엽니다는 *영화* 페이지를 다시 합니다. 닫은 후 `</div>` 뒤에 오는 태그의 `WebGrid` 도우미, 다음 태그를 추가 합니다.

[!code-cshtml[Main](entering-data/samples/sample14.cshtml)]

ASP.NET 해석 하기 전에 살펴본 것 처럼는 `~` 연산자 웹 사이트의 루트 라고 합니다. 사용할 필요가 없습니다 합니다 `~` 연산자; 태그를 사용할 수 있습니다 `<a href="./AddMovie">Add a movie</a>` 또는 HTML 이해 하는 경로 정의 하는 다른 방법이 있습니다. 하지만 `~` 연산자는 좋은 일반 방법 Razor 페이지에 대 한 링크를 만들 때 사이트를 보다 유연 하므로-하위 폴더에 현재 페이지를 이동 하는 경우 링크도 계속 이동 합니다 *AddMovie* 페이지입니다. (유의 해야 합니다 `~` 연산자만 *.cshtml* 페이지. ASP.NET 이해 하지만 표준 HTML 아닙니다.)

완료 되 면 실행 합니다 *영화* 페이지입니다. 이 페이지 처럼 표시 됩니다.

![추가 동영상 페이지 링크를 사용 하 여 동영상 페이지](entering-data/_static/image7.png)

클릭 합니다 **동영상 추가** 이동 하는지 확인 하는 링크는 *AddMovie* 페이지입니다.

## <a name="coming-up-next"></a>다음에 나오는

다음 자습서에서는 사용자가 데이터베이스에 이미 있는 데이터를 편집할 수 있도록 하는 방법에 알아봅니다.

## <a name="complete-listing-for-addmovie-page"></a>AddMovie 페이지에 대 한 전체 목록

[!code-cshtml[Main](entering-data/samples/sample15.cshtml)]

## <a name="additional-resources"></a>추가 리소스

- [Razor 구문을 사용 하 여 ASP.NET 웹 프로그래밍 소개](https://go.microsoft.com/fwlink/?LinkID=202890)
- [SQL 삽입에 문을](http://www.w3schools.com/sql/sql_insert.asp) W3Schools 사이트
- [Asp.net에서 사용자 입력 유효성 검사 페이지 사이트](https://go.microsoft.com/fwlink/?LinkId=253002)합니다. 작업에 대 한 자세한 정보는 `Validation` 도우미입니다.

> [!div class="step-by-step"]
> [이전](form-basics.md)
> [다음](updating-data.md)
