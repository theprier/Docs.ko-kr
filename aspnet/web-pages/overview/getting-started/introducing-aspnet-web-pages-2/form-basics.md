---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
title: HTML 양식 기본 ASP.NET Web Pages-소개 | Microsoft Docs
author: tfitzmac
description: 이 자습서에서는 입력된 폼을 만드는 방법 및 ASP.NET Web Pages (Razor)를 사용 하는 경우 사용자의 입력을 처리 하는 방법의 기본 사항을 보여 줍니다. 그리고 이제...
ms.author: aspnetcontent
ms.date: 05/28/2015
ms.assetid: 81ed82bf-b940-44f1-b94a-555d0cb7cc98
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
msc.type: authoredcontent
ms.openlocfilehash: 609c1c06ed8f29db82b5dd565a935440d4430819
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37815397"
---
<a name="introducing-aspnet-web-pages---html-form-basics"></a>HTML 양식 기본 ASP.NET 웹 페이지 소개
====================
[Tom FitzMacken](https://github.com/tfitzmac)

> 이 자습서에서는 입력된 폼을 만드는 방법 및 ASP.NET Web Pages (Razor)를 사용 하는 경우 사용자의 입력을 처리 하는 방법의 기본 사항을 보여 줍니다. 및 데이터베이스에서 가져온 했으므로 폼 기술을 사용자 데이터베이스에서 특정 영화를 찾을 수 있도록 사용할지 합니다. 통해 시리즈를 완료 했다고 가정 하 [소개에 표시할 데이터를 사용 하 여 ASP.NET 웹 페이지](/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data)합니다.
> 
> 학습할 내용:
> 
> - 표준 HTML 요소를 사용 하 여 폼을 만드는 방법.
> - 사용자를 읽는 방법의 형태로 입력 합니다.
> - 선택적으로 검색을 사용 하 여 데이터를 가져오면 용어는 사용자는 SQL 쿼리를 만드는 방법을 제공 합니다.
> - 페이지에서 "기억"를 입력 한 필드가 포함 하는 방법.
>   
> 
> 기능/기술을 설명 합니다.
> 
> - `Request` 개체
> - SQL `Where` 절.


## <a name="what-youll-build"></a>만들 내용

이전 자습서에서 만들고 데이터베이스, 데이터를 추가한 다음 사용 하 여 `WebGrid` 데이터를 표시 하는 도우미입니다. 이 자습서에서는 해당 제목을 입력할 모든 단어를 포함 또는 동영상의 특정 장르를 찾을 수 있는 검색 상자를 추가 합니다. (예를 들어, 있습니다 수 장르가 "Action" 이거나 해당 제목 "Harry" 또는 "Adventure."를 포함 하는 모든 동영상 찾기)

이 자습서를 완료 하는 경우이 이와 유사를 해야 합니다.

![영화 장르 및 제목 검색 페이지](form-basics/_static/image1.png)

페이지의 목록 일부는 마지막 자습서 동일 &mdash; 표입니다. 차이 표에 나타납니다 영화만 검색 한 됩니다.

## <a name="about-html-forms"></a>HTML 폼에 대 한

(HTML 폼 만들기와 차이점을 사용 하 여 환경이 있다면 `GET` 고 `POST`,이 섹션을 건너뛸 수 있습니다.)

폼에는 사용자 입력된 요소의 &mdash; 텍스트 상자, 단추, 라디오 단추, 확인란, 드롭다운 목록 및 등입니다. 사용자 이러한 컨트롤 입력 또는 선택 하 고 단추를 클릭 하 여 폼을 제출 합니다.

이 예제에서 폼의 기본 HTML 구문은 보여 줍니다.

[!code-html[Main](form-basics/samples/sample1.html)]

이 태그 페이지에서 실행 되 면 다음 그림이에서는 같은 간단한 폼을 만듭니다.

![브라우저에서 렌더링으로 HTML 양식 기본](form-basics/_static/image2.png)

`<form>` 요소 전송할 HTML 요소를 포함 합니다. (있도록 쉬운 실수를 페이지에 요소를 추가 하지만 안에 배치 해야 하는 것을 `<form>` 요소입니다. 이런 경우, 아무 것도 제출 됩니다.) `method` 특성은 브라우저를 사용자 입력을 제출 하는 방법을 지시 합니다. 이 `post` 서버의 또는 업데이트를 수행 하는 경우 `get` 서버에서 데이터를 인출만 하는 경우.

<a id="GET,_POST,_and_HTTP_Verb_Safety"></a>

> [!TIP] 
> 
> **GET, POST 및 HTTP 동사 안전성**
> 
> HTTP, 브라우저 및 서버를 사용 하 여 정보를 교환 하는 프로토콜은 기본 작업에 매우 간단 합니다. 브라우저는 서버에 요청할만 몇 가지 동사를 사용 합니다. 웹에 대 한 코드를 작성할 때 이러한 동사와 브라우저 및 서버를 사용 하는 방법 이해에 도움이 됩니다. 멀리 떨어진 가장 자주 사용 되는 동사는 다음과 같습니다.
> 
> - `GET`. 브라우저는 서버에서 항목을이 동사를 사용 합니다. 예를 들어 브라우저에 URL을 입력 하면 브라우저 수행을 `GET` 원하는 페이지를 요청 하는 작업입니다. 브라우저 추가 수행 페이지 그래픽에 포함 된 경우 `GET` 이미지 작업 합니다. 경우는 `GET` 서버로 정보를 전달 해야 하는 작업, 정보를 쿼리 문자열에서 URL의 일부로 전달 됩니다.
> - `POST`. 브라우저에서 보내는 `POST` 추가 하거나 서버에서 변경 데이터를 제출 하기 위해 요청 합니다. 예를 들어를 `POST` 동사는 데이터베이스에서 레코드를 만들거나 기존 변경 하는 데 사용 됩니다. 대부분의 양식을 작성 및 제출 단추 클릭, 시간, 브라우저 수행을 `POST` 작업 합니다. 에 `POST` 작업 페이지의 본문에 서버로 전달 되는 데이터입니다.
> 
> 이러한 동사의 중요 한 차이를 `GET` 서버에 아무 것도 변경 하지 않는 작업-약간 더 추상적인 방식으로 전환할 수는 `GET` 작업 서버에서 상태가 변경 되지는지 않습니다. 수행할 수 있습니다는 `GET` 만큼 원하는 및 해당 리소스를 변경 하지 않습니다 동일한 리소스에 대 한 작업입니다. (A `GET` 작업은 말이 "안전한" 하거나 기술 용어를 사용 하는 *idempotent*.) 반대로, 물론는 `POST` 요청 변경 작업을 수행할 때마다 서버에서 작업 합니다.
> 
> 두 예제에서는 이러한 차이 설명 하는 데 도움이 됩니다. 검색을 수행할 때 텍스트 상자 하나가 구성 된 양식에서 입력 하 고 검색 단추를 클릭 한 다음 Bing 이나 Google 같은 엔진을 사용 하 합니다. 수행 하는 브라우저는 `GET` URL의 일부분으로 전달 하 고 상자에 입력 한 값을 사용 하 여 작업 합니다. 사용 하는 `GET` 작업 정보 검색 작업을 서버에서 모든 리소스를 변경 하지 않으므로 이러한 유형의 폼 것에 인출 합니다.
> 
> 이제 온라인 작업 주문 과정을 살펴보겠습니다. 주문 세부 정보를 입력 하 고이 정보를 제출 단추를 클릭 합니다. 이 작업 수를 `POST` 작업이 가장 많은 다른 변경 내용을 새 주문 레코드를, 계정 정보 변경 등 서버에서 변경 하면 때문에 요청 합니다. 달리 합니다 `GET` 를 반복할 수 작업에 `POST` 요청-수행한 경우, 요청을 다시 전송 될 때마다 서버에서 새 주문을 생성 있습니다. (다음과 같은 경우에 웹 사이트에서 종종 경고 메시지가 전송 단추를 두 번 이상 클릭 필요가 또는 실수로 폼을 다시 제출 하지 있도록 제출 단추를 사용 하지 않도록 설정 됩니다.)
> 
> 이 자습서에서는 과정에서 사용 하 여 모두를 `GET` 작업 및 `POST` HTML 양식을 사용 하는 작업입니다. 각 사례 때문에 사용 되는 동사는 적절 한 설명입니다.
> 
> (HTTP 동사에 대 한 자세한 내용은 참조는 [메서드 정의](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) W3C 사이트 문서.)


대부분의 사용자 입력된 요소의 HTML은 `<input>` 요소입니다. 와 같은 모양이 `<input type="type" name="name">,` 여기서 *형식* 원하는 사용자 입력된 컨트롤의 종류를 나타냅니다. 이러한 요소는 일반적으로:

- 텍스트 상자: `<input type="text">`
- 확인란: `<input type="check">`
- 라디오 단추: `<input type="radio">`
- 단추: `<input type="button">`
- 제출 단추: `<input type="submit">`

사용할 수도 있습니다는 `<textarea>` 요소를 여러 줄 텍스트 상자 만들기 및 `<select>` 드롭다운 목록에서 만들거나 스크롤 가능한 목록이 요소입니다. (HTML에 대 한 자세한 구성 요소를 참조 하세요 [HTML 양식 및 입력](http://www.w3schools.com/html/html_forms.asp) W3Schools 사이트의.)

`name` 이름이 나중에 요소 값을 어떻게 받게 됩니다 곧 알게 되었기 때문 특성은 매우 중요 합니다.

흥미로운 부분은, 페이지 개발자가 무엇을 할 사용자의 입력을 사용 하 여 보여 줍니다. 이러한 요소와 연결 된 기본 제공 동작은 없습니다. 대신, 사용자 입력 또는 선택 된 값을 얻으려면 한 사람과 작업을 수행 해야 할 수도 있습니다. 이 자습서의 학습 내용입니다.

> [!TIP] 
> 
> **HTML5 및 입력된 폼**
> 
> 아시다시피, HTML 전환 중에서 이며 최신 버전 (HTML5) 정보를 입력 하는 사용자에 대 한 보다 직관적인 방법에 대 한 지원이 포함 되어 있습니다. 예를 들어, html5로 (페이지 개발자) 할 수 있습니다 페이지 하려는 날짜를 입력 하는 사용자입니다. 사용자는 날짜를 수동으로 입력 하도록 요구 하는 것이 아니라 일정 브라우저는 자동으로 표시한 다음 수 있습니다. 그러나 HTML5는 새로운 클래스 이며 아직 모든 브라우저에서 지원 되지 않습니다.
> 
> ASP.NET 웹 페이지에 입력 하는 사용자의 브라우저는 HTML5 지원 합니다. 새 특성에 대 한 개념은 `<input>` html5로 요소를 참조 하세요 [HTML &lt;입력&gt; 특성을 입력](http://www.w3schools.com/html/html_form_input_types.asp) W3Schools 사이트입니다.


## <a name="creating-the-form"></a>폼 만들기

WebMatrix에서에 **파일** 작업 영역을 열고 합니다 *Movies.cshtml* 페이지입니다.

닫은 후 `</h1>` 태그와 여 `<div>` 태그를 `grid.GetHtml` 호출, 다음 태그를 추가 합니다.

[!code-html[Main](form-basics/samples/sample2.html)]

이 태그 라는 텍스트 상자가 포함 된 양식을 만듭니다 `searchGenre` 및 전송 단추가 있습니다. 텍스트 상자 및 단추 묶인 제출를 `<form>` 요소입니다 `method` 특성이로 설정 된 `get`합니다. (텍스트 상자를 입력 하 고 제출 단추 안에 없는 경우를 `<form>` 요소에 아무 것도 제출 됩니다. 단추를 클릭 합니다.) 사용할는 `GET` 동사 여기 양식을 만들 수 있으므로 해당 작업을 수행할 변경 내용을 서버의-검색에만 발생 합니다. (이전 자습서를 사용 하는 `post` 메서드를 서버에 변경 내용을 제출 하는 방법입니다. 표시 됩니다는 다음 자습서에서 다시.)

페이지를 실행 합니다. 폼에 대 한 모든 동작을 정의 하지 않은 모양을 확인할 수 있습니다.

![장르에 대 한 검색 상자를 사용 하 여 동영상 페이지](form-basics/_static/image3.png)

"코미디."와 같은 텍스트 상자에 값을 입력 합니다. 누른 **검색 장르**합니다.

페이지의 URL을 기록해 둡니다. 설정 된 `<form>` 요소의 `method` 특성을 `get`, 입력 값이 같은 URL에 쿼리 문자열의 일부가 되었습니다.:

`http://localhost:45661/Movies.cshtml?searchGenre=Comedy`

## <a name="reading-form-values"></a>읽기 폼 값

페이지는 이미 데이터베이스 데이터를 가져오고 결과 표로 표시 하는 일부 코드를 포함 합니다. 이제 검색 용어를 포함 하는 SQL 쿼리를 실행할 수 있도록 입력란의 값을 읽는 코드를 추가 해야 합니다.

폼의 메서드 설정 했으므로 `get`, 다음과 같은 코드를 사용 하 여 텍스트 상자에 입력 된 값을 읽을 수 있습니다.

`var searchTerm = Request.QueryString["searchGenre"];`

`Request.QueryString` 개체 (를 `QueryString` 의 속성을 `Request` 개체)의 일부로 전송 된 요소의 값이 포함 됩니다는 `GET` 작업. `Request.QueryString` 속성을 포함를 *컬렉션* (목록)의 형태로 전송 되는 값입니다. 모든 개별 값을 가져오려면 원하는 요소의 이름을 지정할 수 있습니다. 이유는 있어야를 `name` 특성을 `<input>` 요소 (`searchTerm`) 텍스트 상자를 만드는 합니다. (대 한 자세한 내용은 합니다 `Request` 개체를 참조 하십시오 합니다 [사이드바](#BKMK_TheRequestObject) 나중.)

간단 충분히 입력란의 값을 읽을 수 있습니다. 사용자 입력 하지 않았습니다 아무 것도 전혀 텍스트 상자에 있지만 클릭 하지만 **검색** 어쨌든 검색할 항목이 없으므로 해당 클릭 무시할 수 있습니다.

다음 코드는 이러한 조건을 구현 하는 방법을 보여 주는 예제입니다. (아직이 코드를 추가할 필요가 없습니다; 잠시 후에 로그인 할 수 있습니다)입니다.

[!code-csharp[Main](form-basics/samples/sample3.cs)]

테스트는 이러한 방식으로 나눕니다.

- 값을 가져옵니다 `Request.QueryString["searchGenre"]`, 즉에 입력 된 값을 `<input>` 라는 요소가 `searchGenre`합니다.
- 비어 있는지를 사용 하 여 확인 된 `IsEmpty` 메서드. 이 메서드는 표준 방법 항목 (예를 들어, 폼 요소)는 값이 들어 있는지 확인 합니다. 하지만 실제로 관심이 있는 경우에 *되지* 비어 있으므로...
- 추가 된 `!` 앞의 연산자는 `IsEmpty` 테스트 합니다. (의 `!` 연산자 의미 논리적 NOT).

전체 일반 영어로 `if` 조건이 다음 변환: *양식의 searchGenre 요소 비어 있지 않은 경우, 다음 중...*

이 블록에는 검색 용어를 사용 하는 쿼리를 만들기 위한 단계를 설정 합니다. 다음 섹션에서 할 수 있습니다.

<a id="BKMK_TheRequestObject"></a>

> [!TIP] 
> 
> **요청 개체**
> 
> `Request` 개체 브라우저 페이지를 요청 하거나 제출 하는 경우 응용 프로그램에 전송 하는 모든 정보를 포함 합니다. 이 개체에 텍스트 상자 값 또는 업로드할 파일을 같은 사용자 제공 하는 모든 정보가 포함 됩니다. 또한 모든 종류의 쿠키 (있는 경우) URL 쿼리 문자열의 값과 같은 추가 정보를 실행 중인 브라우저에 설정 된 언어 목록에 사용자를 사용 하는 브라우저의 종류는 페이지의 파일 경로 를 확인해 보십시오.
> 
> `Request` 개체를 *컬렉션* (목록) 값입니다. 해당 이름을 지정 하 여 컬렉션에서 개별 값을 가져옵니다.
> 
> `var someValue = Request["name"];`
> 
> `Request` 개체는 실제로 여러 하위 집합을 노출 합니다. 예를 들어:
> 
> - `Request.Form` 제출 된 내부 요소에서 값을 제공 `<form>` 요청인 경우 요소는 `POST` 요청 합니다.
> - `Request.QueryString` 제공 된 값만 URL의 쿼리 문자열에 합니다. (같은 URL에서 `http://mysite/myapp/page?searchGenre=action&page=2`, `?searchGenre=action&page=2` URL의 섹션은 쿼리 문자열.)
> - `Request.Cookies` 컬렉션은 브라우저에 보내지는 쿠키에 액세스할 수 있습니다.
> 
> 제출된 된 폼에는 사용자가 알고 있는 값을 가져오는 사용할 수 있습니다 `Request["name"]`합니다. 또는 특정 버전을 사용할 수 `Request.Form["name"]` (에 대 한 `POST` 요청) 또는 `Request.QueryString["name"]` (에 대 한 `GET` 요청). 물론 *이름을* 가져올 항목의 이름입니다.
> 
> 가져오려는 항목의 이름을 사용 하는 컬렉션 내에서 고유 해야 합니다. 때문에 합니다 `Request` 개체와 같은 하위 집합을 제공 `Request.Form` 고 `Request.QueryString`합니다. 페이지 라는 폼 요소를 포함 한다고 가정 `userName` 하 고 *수도* 이름이 포함 `userName`합니다. 표시 되 면 `Request["userName"]`, 모호 양식 값 또는 쿠키 것인지 합니다. 그러나 받게 되 면 `Request.Form["userName"]` 또는 `Request.Cookie["userName"]`를 가져오려고 하는 값에 대 한 명시적 예요.
> 
> 특정 수의 하위 집합을 사용 하는 것이 좋습니다 `Request` 원하는 같은 있다고 `Request.Form` 또는 `Request.QueryString`합니다. 이 자습서에서 만드는 간단한 페이지, 아마도 하지 않는 실제로 것 간 차이입니다. 그러나 더 복잡 한 페이지를 만들 때 버전을 사용 하는 명시적 `Request.Form` 또는 `Request.QueryString` 페이지 폼 (또는 여러 개의 폼)을 포함 하는 경우 발생할 수 있는 문제를 방지 하는 데 도움이 쿠키, 쿼리 문자열 값 및 등입니다.


## <a name="creating-a-query-by-using-a-search-term"></a>검색 용어를 사용 하 여 쿼리 만들기

사용자가 입력 한 검색어를 가져오는 방법을 배웠으므로를 사용 하는 쿼리를 만들 수 있습니다. 데이터베이스에서 모든 동영상 항목을 가져오려면 사용 하는 경우이 문은 같은 SQL 쿼리를 기억해 야 합니다.

`SELECT * FROM Movies`

포함 하는 쿼리를 사용 해야만 특정 영화를 가져오려면는 `Where` 절. 이 절을 쿼리에 의해 반환 된 행에는 조건을 설정할 수 있습니다. 예를 들면 다음과 같습니다.

`SELECT * FROM Movies WHERE Genre = 'Action'`

기본 형식은 `WHERE column = value`합니다. 방금 외에 다른 연산자를 사용할 수 있습니다 `=`과 같이 `>` (보다 큼), `<` (보다 작음), `<>` (같지 않음), `<=` (작거나 같음), 원하는 항목에 따라 등.

SQL 문은 궁금한 경우 대/소문자 구분 하지 않습니다 &mdash; `SELECT` 와 같습니다 `Select` (심지어 `select`). 그러나 사람들이 자주 활용 SQL 문에서 키워드와 같은 `SELECT` 고 `WHERE`, 쉽게 읽을 수 있도록 합니다.

### <a name="passing-the-search-term-as-a-parameter"></a>검색 용어를 매개 변수로 전달

특정 장르를 아주 쉽게 검색 (`WHERE Genre = 'Action'`), 하지만 사용자가 입력 하는 모든 장르를 검색할 수 있게 되기를 원하는 합니다. 이 작업을 수행 하려면 검색 하는 값에 대 한 자리 표시자를 포함 하는 SQL 쿼리를 만들어야 합니다. 이 명령은 같습니다.

`SELECT * FROM Movies WHERE Genre = @0`

자리 표시자는는 `@` 문자 뒤에 0 개 있습니다. 쿼리는 여러 자리 표시자를 포함할 수 있습니다 및 명명 된은 짐작할 수 `@0`, `@1`, `@2`등입니다.

쿼리를 설정 하 고 실제로 값을 전달 하려면 다음과 같은 코드를 사용할 수 있습니다.

[!code-sql[Main](form-basics/samples/sample4.sql)]

이 코드는 이미 작업 표에서 데이터를 표시할 비슷합니다. 유일한 차이점은:

- 자리 표시자를 포함 하는 쿼리 (`WHERE Genre = @0"`).
- 쿼리 변수에 배치 됩니다 (`selectCommand`)에 직접 쿼리를 전달 하기 전에;는 `db.Query` 메서드.
- 호출 하는 경우는 `db.Query` 메서드를 전달 하면 쿼리 및 자리 표시자에 사용할 값입니다. (전달는 쿼리가 여러 자리 표시자 있으면 메서드를 별도 값으로 모든.)

이러한 모든 요소를 결합 하는 경우 다음 코드를 가져옵니다.

[!code-csharp[Main](form-basics/samples/sample5.cs)]

> [!NOTE] 
> 
> **중요!** 자리 표시자를 사용 하 여 (같은 `@0`) 값을 SQL 명령에 전달 하는 *매우 중요 한* 보안에 대 한 합니다. 변수 데이터에 대 한 자리 표시자를 사용 하 여 여기에서 살펴본 방식에는 유일한 방법은 SQL 명령을 생성 해야 합니다.
> 
> 리터럴 텍스트 (연결) 및 사용자에서 가져온 값을 결합 하 여 SQL 문을 생성 하지 않습니다. 사이트를 열고 SQL 문으로 사용자 입력을 연결 하는 *SQL 주입 공격* 악의적인 사용자 데이터베이스를 해킹 하는 페이지에 대 한 값을 제출 하는 경우. (자세한 내용은 문서의 [SQL 주입](https://msdn.microsoft.com/library/ms161953.aspx) MSDN 웹 사이트.)


## <a name="updating-the-movies-page-with-search-code"></a>코드 검색을 사용 하 여 영화 페이지 업데이트

이제에서 코드를 업데이트 하는 *Movies.cshtml* 파일입니다. 시작 하려면 페이지의 맨 위에 있는 코드 블록의 코드를이 코드로 바꿉니다.

[!code-csharp[Main](form-basics/samples/sample6.cs)]

여기서 차이점은 쿼리를 배치한 합니다 `selectCommand` 에 전달 하는 변수 `db.Query` 나중입니다. SQL 문을 변수에 배치는 문을 검색 하는 데 수행할 수를 변경할 수 있습니다.

또한 나중에 다시 배치에서는이 두 줄을 제거 했습니다.

[!code-csharp[Main](form-basics/samples/sample7.cs)]

쿼리를 아직 실행 하지 않으려는 (즉, 호출 `db.Query`)를 초기화 하지는 `WebGrid` 도우미 아직 중 하나입니다. SQL 문을 실행 해야 파악 한 후 이러한 작업을 수행할 수 있습니다.

다시 작성된이 블록 뒤에 검색 처리에 대 한 새 논리를 추가할 수 있습니다. 완성 된 코드는 다음과 같이 표시 됩니다. 이 예제에서는 일치 하도록 페이지에서 코드를 업데이트 합니다.

[!code-cshtml[Main](form-basics/samples/sample8.cshtml)]

페이지는 이제 다음과 같이 작동합니다. 페이지 실행 될 때마다 코드가 데이터베이스 및 `selectCommand` 변수에서 모든 레코드를 가져오는 SQL 문을로 설정 됩니다는 `Movies` 테이블입니다. 초기화 코드는 `searchTerm` 변수입니다.

그러나 현재 요청에 대 한 값을 포함 하는 경우는 `searchGenre` 요소를 코드 집합 `selectCommand` 다른 쿼리를-하는 namely를 포함 하는 `Where` 장르를 검색 하는 절. 또한 설정 `searchTerm` (nothing 일 수 있음)는 검색 상자에 전달 되는 항목에 있습니다.

문을는 SQL에 관계 없이 `selectCommand`, 호출 `db.Query` 쿼리를 실행 하려면 전달 어떤 중인 `searchTerm`합니다. 내용이 없는 경우 `searchTerm`, 중요 하지 않습니다, 경우에 값을 전달 하려면 매개 변수가 있기 때문에 `selectCommand` 진행 합니다.

마지막으로 코드를 초기화 합니다 `WebGrid` 이전 처럼 쿼리 결과 사용 하 여 도우미입니다.

SQL 문을 배치 하 여 볼 수 있습니다 및 변수로 검색어 코드에 유연성이 추가 했습니다. 이 자습서의 뒷부분에서 살펴보겠지만이 필요한 기본적인 프레임 워크를 사용할 수 하 고 다양 한 검색에 대 한 논리를 계속 추가 합니다.

## <a name="testing-the-search-by-genre-feature"></a>장르 하 여 검색 기능을 테스트

WebMatrix를 실행 합니다 *Movies.cshtml* 페이지입니다. 장르에 대 한 텍스트 상자를 사용 하 여 페이지가 표시 됩니다.

사용자 테스트 레코드 중 하나에 대해 입력 한 다음 클릭는 장르를 입력 **검색**합니다. 이 이번에만 해당 장르와 일치 하는 영화 목록을 표시 됩니다.

![Comedies' genre'에 대 한 검색 후 나열 동영상 페이지](form-basics/_static/image4.png)

다른 장르를 입력 하 고 다시 검색 합니다. 검색은 대/소문자 구분을 볼 수 있도록 모든 소문자 또는 대문자로 문자를 사용 하 여 장르를 입력 하십시오.

## <a name="remembering-what-the-user-entered"></a>사용자가 입력 한 내용이 "기억"

보시는 장르를 입력 하 고 클릭 한 후 **검색 장르**, 해당 장르에 대 한 목록을 확인 합니다. 검색 텍스트 상자 비어 있지만 &mdash; 이 즉,에 입력 했다고 기억 하지 않았습니다.

이 동작이 발생 하는 이유를 이해 하는 것이 반드시 합니다. 페이지에 제출 하면 브라우저는 웹 서버에 요청을 보냅니다. ASP.NET 요청 가져오면이 페이지의 새 인스턴스를 만듭니다, 그리고 코드를 실행 및 브라우저 페이지를 다시 렌더링 합니다. 실제로 그러나 페이지 알지는 작업 중이 던 이전 버전의 자체를 사용 하 여 합니다. 일부 요청도 알고 모두에 데이터를 형성 합니다.

페이지를 요청 될 때마다 &mdash; 처음 아니면 모르니 까 &mdash; 새 페이지 보시기 합니다. 웹 서버에 마지막 요청 메모리가 없습니다. 모두 ASP.NET 않으며 브라우저도 않습니다. 페이지의 이러한 별도 인스턴스 간의 유일한 연결이 서로 전송 하는 모든 데이터입니다. 페이지에 제출 하면 예를 들어, 새 페이지 인스턴스 데이터를 가져올 수는 폼 이전 인스턴스에서 보낸 합니다. (페이지 간에 데이터를 전달 하는 또 다른 방법은 쿠키를 사용 합니다.)

이 상황을 설명 하는 정식 방법을 웹 페이지는 싶습니다 *상태 비저장*합니다. 웹 서버와 페이지 자체 및 페이지의 요소에는 페이지의 이전 상태에 대 한 정보를 유지 하지 않습니다. 웹 개별 요청에 대 한 상태를 유지 관리 신속 하 게 소모 하 게 종종 아마도 수천을 처리 하는 웹 서버의 리소스가 수십만, 초당 요청 때문에 이러한 방식으로 설계 되었습니다.

그렇기 때문 텍스트 상자가 비어 있습니다. 페이지를 제출한 후 ASP.NET 페이지의 새 인스턴스를 생성 하 고 코드와 태그를 통해 실행 합니다. 텍스트 상자에 값을 배치 하기 위해 ASP.NET에 지시 하는 해당 코드에서 nothing 있었습니다. 따라서 ASP.NET 하지 않은 모든 작업을 수행할 및 텍스트 상자에 값이 없는 렌더링 되었습니다.

실제로이 문제를 해결 하는 쉬운 방법이 있습니다. 텍스트 상자에 입력 한 장르 *됩니다* 코드에서 사용할 수 있습니다 &mdash; 있는 `Request.QueryString["searchGenre"]`합니다.

텍스트 상자에 대 한 태그를 업데이트 하는 `value` 특성에서 값을 가져옵니다 `searchTerm`,이 예제와 같이:

[!code-html[Main](form-basics/samples/sample9.html?highlight=1)]

이 페이지에서 설정할 수 있습니다도 합니다 `value` 특성을 `searchTerm` 입력 변수를 해당 변수에 장르를 포함 하기 때문입니다. 하지만 사용 하 여는 `Request` 설정 하는 개체를 `value` 같습니다.이 작업을 수행 하는 표준 방법은 표시 된 것 처럼 특성입니다. (이 작업을 수행 하려는 것으로 가정 &mdash; 상황에 따라 페이지를 렌더링 하려는 *없이* 필드의 값입니다. 모든 종속 응용 프로그램을 사용 하 여 것입니다.)

> [!NOTE]
> 기억할 수 없는 "" 암호에 사용 되는 입력란의 값입니다. 사람이 코드를 사용 하 여 암호 필드를 채울 수 있도록 보안 허점을 것입니다.


페이지를 다시 실행을 장르를 입력 한 다음 클릭 **검색 장르**합니다. 이 시간 뿐만 아니라 있습니다 볼 검색 결과 수 있지만 입력란 기억 마지막 입력:

![페이지를 보여 주는 텍스트 상자에 ' 저장 ' 이전 항목](form-basics/_static/image5.png)

## <a name="searching-for-any-word-in-the-title"></a>제목에 단어 검색

이제 모든 장르를 검색할 수 있습니다 하지만 제목을 검색할 수도 있습니다. 까다로웠습니다. 제목을 정확 하 게 검색 하는 경우, 대신 제목 내의 아무 곳 이나 표시 되는 단어를 검색할 수 있습니다 하는 것이 어렵습니다. SQL에서 이렇게 하려면 사용는 `LIKE` 연산자 및 구문을 다음과 같이 합니다.

`SELECT * FROM Movies WHERE Title LIKE '%adventure%'`

이 명령은 모든 영화를 제목에 해당 어구가 포함 "adventure"를 가져옵니다. 사용 하는 경우는 `LIKE` 와일드 카드 문자를 포함 하면 연산자 `%` 검색어의 일환으로 합니다. 검색 `LIKE 'adventure%'` "'a d v를 사용 하 여 시작"을 의미 합니다. (기술적으로 "문자열 뒤에 ' adventure'입니다." 의미) 검색어 마찬가지로 `LIKE '%adventure'` "모든 항목을 의미 'a d v 문자열 뒤에", "a d v e'로 끝나는"를 다른 방법으로 합니다.

검색어 `LIKE '%adventure%'` "a d v 제목에 있습니다." 사용 "을 의미 하므로 (기술적으로 "모든 항목에 제목 뒤에 'adventure' 뒤에.")

내 합니다 `<form>` 요소에 닫는 바로 아래에서 다음 태그를 추가 `</div>` 장르 검색에 대 한 태그 (닫기 전에 `</form>` 요소):

[!code-html[Main](form-basics/samples/sample10.html)]

이 검색을 처리 하는 코드는 조립 해야 한다는 장르 검색에 대 한 코드와 유사 합니다 `LIKE` 검색 합니다. 페이지의 맨 위에 있는 코드 블록 내에서이 추가 `if` 바로 뒤에 블록을 `if` 장르 검색에 대 한 블록:

[!code-csharp[Main](form-basics/samples/sample11.cs)]

이 코드는 이전에 본 것과 동일한 논리 제외 하 고 검색을 사용 하 여는 `LIKE` 연산자와 코드 넣습니다 "`%`" 검색어 전후.

쉽게 페이지 검색을 다시 추가 된 방식을 확인할 수 있습니다. 수행 했던 모든 했습니다.

- 만들기는 `if` 관련 검색 상자는 값을가지고 있는지 여부를 확인 하려면 테스트 하는 블록입니다.
- 설정 된 `selectCommand` 새 SQL 문에 변수입니다.
- 설정 된 `searchTerm` 쿼리에 전달할 값으로 변수입니다.

제목 검색에 대 한 새 논리를 포함 하는 전체 코드 블록을 다음과 같습니다.

[!code-cshtml[Main](form-basics/samples/sample12.cshtml)]

요약의이 코드의 용도 다음과 같습니다.

- 변수 `searchTerm` 고 `selectCommand` 맨 위에 있는 초기화 됩니다. 이러한 변수를 적절 한 검색 용어 (있는 경우)으로 설정 하려는 및 적절 한 SQL 명령에서 사용자가 페이지에 기반 합니다. 기본 검색 데이터베이스에서 모든 영화를 가져오는 간단한 경우입니다.
- 에 대 한 테스트 `searchGenre` 및 `searchTitle`, 코드 집합 `searchTerm` 검색 하려는 값입니다. 해당 코드 블록을 설정할 수도 `selectCommand` 해당 검색에 대 한 적절 한 SQL 명령에 있습니다.
- 합니다 `db.Query` 메서드를 한 번만 사용 하 여 모든 SQL 명령에 `selectedCommand` 값 이며 `searchTerm`합니다. (없음 장르 및 없습니다 제목 단어) 검색 용어가 없는 경우 값 `searchTerm` 은 빈 문자열입니다. 그러나 문제가 되지 경우 쿼리 매개 변수를 필요 하지 않으므로 합니다.

## <a name="testing-the-title-search-feature"></a>제목 검색 기능 테스트

이제 완성 된 검색 페이지를 테스트할 수 있습니다. 실행할 *Movies.cshtml*합니다.

장르를 입력 하 고 클릭 **검색 장르**합니다. 표에서 전에 등의 해당 장르의 영화를 표시합니다.

제목 단어를 입력 하 고 클릭 **검색 제목을**입니다. 표 제목에 해당 단어가 포함 된 영화를 표시 합니다.

![동영상 페이지 제목에 '는'에 대 한 검색 후 나열](form-basics/_static/image6.png)

두 텍스트 상자를 비워 두고 단추 중 하나를 클릭 합니다. 표의 모든 영화를 표시합니다.

## <a name="combining-the-queries"></a>쿼리를 결합합니다.

전용 검색을 수행할 수 있습니다는 확인할 수 있습니다. 두 검색 상자에 값을 포함 하는 경우에 제목과 장르를 동시에 검색할 수 없습니다. 예를 들어, 해당 제목 "Adventure"를 포함 하는 모든 작업 영화를 검색할 수 없습니다. (페이지는 코딩 된 대로 이제 장르와 제목에 대 한 값을 입력 하면 제목 검색이 가져옵니다 우선 순위를입니다.) 조건을 결합 하는 검색을 만들려면 다음과 같은 구문이 SQL 쿼리를 만들 해야 합니다.

`SELECT * FROM Movies WHERE Genre = @0 AND Title LIKE @1`

다음과 같은 문을 사용 하 여 쿼리를 실행 해야 하 고 (약 말하기):

`var selectedData = db.Query(selectCommand, searchGenre, searchTitle);`

알 수 있듯이 조건과 순열이 많이 수 있도록 논리를 만드는 약간 관련 된 가져올 수 있습니다. 따라서 여기서 중지 됩니다.

## <a name="coming-up-next"></a>다음에 나오는

다음 자습서에서는 사용자가 영화 데이터베이스에 추가할 수 있도록 폼을 사용 하는 페이지를 만들어야 합니다.

## <a name="complete-listing-for-movie-page-updated-with-search"></a>동영상 페이지 (검색을 사용 하 여 업데이트)에 대 한 전체 목록

[!code-cshtml[Main](form-basics/samples/sample13.cshtml)]

## <a name="additional-resources"></a>추가 리소스

- [Razor 구문을 사용 하 여 ASP.NET 웹 프로그래밍 소개](https://go.microsoft.com/fwlink/?LinkID=202890)
- [SQL WHERE 절](http://www.w3schools.com/sql/sql_where.asp) W3Schools 사이트
- [메서드 정의](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) W3C 사이트에 대 한 문서

> [!div class="step-by-step"]
> [이전](displaying-data.md)
> [다음](entering-data.md)
