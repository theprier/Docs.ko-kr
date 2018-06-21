---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
title: HTML 양식 기본 ASP.NET 웹 페이지-소개 | Microsoft Docs
author: tfitzmac
description: 이 자습서는 기본적인 입력된 폼을 만드는 방법 및 ASP.NET 웹 페이지 (Razor)를 사용 하는 경우 사용자의 입력을 처리 하는 방법을 보여 줍니다. 및 이제 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/28/2015
ms.topic: article
ms.assetid: 81ed82bf-b940-44f1-b94a-555d0cb7cc98
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
msc.type: authoredcontent
ms.openlocfilehash: 6f44f74774c2fa6338524987779e15f3940d1830
ms.sourcegitcommit: 9a35906446af7ffd4ccfc18daec38874b5abbef7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "30898923"
---
<a name="introducing-aspnet-web-pages---html-form-basics"></a>HTML 양식 기본 ASP.NET 웹 페이지-소개
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 자습서는 기본적인 입력된 폼을 만드는 방법 및 ASP.NET 웹 페이지 (Razor)를 사용 하는 경우 사용자의 입력을 처리 하는 방법을 보여 줍니다. 및 데이터베이스를가지고 했으므로 사용 하 여 폼에 대 한 이해가 사용자가 데이터베이스에서 특정 영화를 찾을 수 있도록 합니다. 통해 시리즈를 완료 한 것으로 가정 [소개에 표시할 데이터를 사용 하 여 ASP.NET 웹 페이지](/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data)합니다.
> 
> 학습 내용:
> 
> - 표준 HTML 요소를 사용 하 여 폼을 만드는 방법.
> - 사용자를 읽지 하는 방법의 폼에 입력 합니다.
> - 선택적으로 검색을 사용 하 여 데이터를 가져오면 용어는 사용자는 SQL 쿼리를 만드는 방법을 제공 합니다.
> - 페이지에서 "기억" 사용자의 입력 필드가 포함 하는 방법.
>   
> 
> 기능/기술을 설명 합니다.
> 
> - `Request` 개체
> - SQL `Where` 절.


## <a name="what-youll-build"></a>만들 것인지

이전 자습서에서는 데이터베이스, 데이터 추가 만들고 그런 다음 사용 하 여 `WebGrid` 데이터를 표시 하는 도우미입니다. 이 자습서에서는 입력 하면 모든 단어를 포함 하는 제목이 또는의 특정 한 장르의 영화를 찾을 수 있도록 하는 검색 상자를 추가 합니다. (예를 들어 수 있습니다 인 모든 "Action" 또는 "해리" 또는 "Adventure" 제목이 포함 된 모든 동영상을 찾을 수)

이 자습서와 함께 마친 경우이 이와 같은 페이지를 해야 합니다.

![동영상 페이지 Genre 및 제목 검색](form-basics/_static/image1.png)

페이지의 목록 일부는 지난 자습서 동일 &mdash; 표입니다. 차이 눈금 나타납니다 영화만 검색 한 됩니다.

## <a name="about-html-forms"></a>HTML 폼에 대 한

(HTML 폼 만들기 및 간의 차이점은 경험 정답 `GET` 및 `POST`,이 섹션을 건너뛸 수 있습니다.)

폼에는 사용자 입력된 요소의 &mdash; 텍스트 상자, 단추, 라디오 단추, 확인란, 드롭 다운 목록 및 등입니다. 사용자가 이러한 컨트롤의 채우기 또는 항목 선택 하 고 단추를 클릭 하 여 폼을 제출 합니다.

이 예제에서는 폼의 기본 HTML 구문은 보여 줍니다.

[!code-html[Main](form-basics/samples/sample1.html)]

이 태그는 페이지를 실행 하면 다음이 그림 처럼 보이는 간단한 양식을 만듭니다.

![기본 HTML 양식으로 브라우저에서 렌더링 된](form-basics/_static/image2.png)

`<form>` 요소를 전송할 HTML 요소를 포함 합니다. (확인 하는 간단한 실수를 페이지에 요소를 추가 하지만 다음 잊은 내에 배치 하는 한 `<form>` 요소입니다. 이런 경우에서 아무 것도 전송 됩니다.) `method` 특성 브라우저 사용자 입력을 전송 하는 방법을 알립니다. 로 설정 하면 `post` 또는 서버에 업데이트를 수행 하는 경우 `get` 서버에서 바로 데이터를 인출 하는 경우.

<a id="GET,_POST,_and_HTTP_Verb_Safety"></a>

> [!TIP] 
> 
> **GET, POST 및 HTTP 동사 안전**
> 
> HTTP, 브라우저 및 서버 사용 정보를 교환 하는 프로토콜은 기본 작업에 매우 간단 합니다. 몇 가지 동사만 서버로 요청을 사용 하는 브라우저. 웹에 대 한 코드를 작성할 때 이러한 동사와 브라우저와 서버 사용 하는 방법 이해 하는 것이 좋습니다. 멀리 떨어져 가장 일반적으로 사용된 되는 동사는 다음과 같습니다.
> 
> - `GET`. 브라우저가이 동사를 사용 하 여 서버에서 항목을 가져옵니다. 예를 들어 브라우저에 URL을 입력할 때 브라우저 수행는 `GET` 원하는 페이지를 요청 하는 작업입니다. 페이지 그래픽을 포함 하는 경우 브라우저 수행 추가 `GET` 작업에는 이미지입니다. 경우는 `GET` 서버로 정보를 전달 해야 하는 작업, 정보가 쿼리 문자열에 대 한 URL의 일부분으로 전달 됩니다.
> - `POST`. 브라우저에서 보내는 `POST` 를 추가 하거나 서버에서 변경 데이터를 전송 하기 위해 요청 합니다. 예를 들어는 `POST` 동사는 데이터베이스의 레코드를 만들거나 기존 변경 하는 데 사용 됩니다. 대부분의 시간, 폼에 입력 고 전송 단추를 클릭, 브라우저 수행는 `POST` 작업 합니다. 에 `POST` 페이지의 본문 작업이, 서버에 전달 되는 데이터입니다.
> 
> 이러한 동사의 중요 한 차이 `GET` 작업 서버에 아무 것도 변경 하지 않는-약간 더 추상적인 방식으로 전환할 수는 `GET` 작업 서버에서 상태가 변경 되지 않습니다. 수행할 수 있습니다는 `GET` 횟수 만큼 있으며 이러한 리소스를 변경 하지 않습니다. 동일한 리소스에 대 한 작업이 있습니다. (A `GET` 작업 "안전" 하거나 기술 용어를 사용 하려면 말은 *idempotent*.) 반대로, 물론,는 `POST` 요청을 변경 작업을 수행 될 때마다 서버에 있는 항목입니다.
> 
> 두 가지 예는이 차이 설명 하는 데 도움이 됩니다. 검색을 수행 하는 경우 하나의 텍스트 상자에 구성 된 폼에 정보를 입력 하 고 검색 단추를 클릭 한 다음 Bing 이나 Google, 같은 엔진을 사용 하 여 합니다. 수행 하는 브라우저는 `GET` URL의 일부로 전달 하 여 상자에 입력 한 값으로 작업 합니다. 사용 하는 `GET` 작업 정보 검색 작업에는 서버의 리소스에 변경 되지 않습니다 때문에 이러한 종류의 양식 제대로 방금 인출 합니다.
> 
> 이제 온라인 작업 주문 과정을 살펴보겠습니다. 주문 세부 정보를 입력 하 고 전송 단추를 클릭 합니다. 이 작업을 됩니다는 `POST` 아마도 다른 여러 변경을 새 주문 레코드, 계정 정보를 변경 등 서버에서 변경 작업을 됩니다 있기 때문에 요청 합니다. 와 달리는 `GET` 반복할 수 없습니다 작업, 프로그램 `POST` 요청-에서 요청을 다시 전송 될 때마다 경우에 서버에 새 주문을 생성 합니다. (이와 같은 경우, 웹 사이트에서 종종 경고 메시지가 두 번 이상 전송 단추를 클릭 또는 실수로 폼을 다시 제출 하지 않는 있도록 제출 단추를 비활성화 합니다.)
> 
> 이 자습서에서는 과정에서 사용 하 여 둘 다는 `GET` 작업 및 `POST` HTML 양식을 사용 하는 작업입니다. 각 사례 이유 사용 되는 동사는 적절 한 설명 합니다.
> 
> (HTTP 동사에 대 한 자세한 내용은 참조는 [메서드 정의](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) W3C 사이트 문서.)


대부분의 사용자 입력된 요소는 HTML `<input>` 요소입니다. 같이 `<input type="type" name="name">,` 여기서 *형식* 원하는 사용자 입력된 컨트롤의 종류를 나타냅니다. 이러한 요소는 자주 이벤트:

- 텍스트 상자: `<input type="text">`
- 확인란: `<input type="check">`
- 라디오 단추: `<input type="radio">`
- button: `<input type="button">`
- 전송 단추: `<input type="submit">`

사용할 수도 있습니다는 `<textarea>` 요소를 여러 줄 텍스트 상자 만들기 및 `<select>` 만들 드롭 다운 목록 또는 스크롤할 수 있는 목록 요소를 합니다. (요소를 구성 하는 HTML에 대 한 자세한 참조 [HTML 폼 및 입력](http://www.w3schools.com/html/html_forms.asp) W3Schools 사이트에 있습니다.)

`name` 이름이 없으므로 나중 요소의 값을 어떻게 얻게 됩니다 곧 알게 특성은 매우 중요 합니다.

재미 있는 사용자의 입력으로 수행할 페이지 개발자입니다. 이러한 요소와 연결 된 기본 제공 동작은 없습니다. 대신, 사용자가 입력 하거나 선택 하는 값을 가져오는 한 사람과 작업을 수행 해야 할 수도 있습니다. 이 자습서의 학습 내용입니다.

> [!TIP] 
> 
> **HTML5 및 입력된 양식 처럼**
> 
> 아시다시피, HTML 전환 중인 및 최신 버전 (HTML5) 정보를 입력 하는 사용자에 대 한 보다 직관적인 방법에 대 한 지원을 포함 합니다. 예를 들어, HTML5에 (페이지 개발자) 알 수 있습니다 페이지 날짜를 입력 하면 되도록 합니다. 브라우저 그런 다음 자동으로 표시할 수 달력 필요 없이 사용자를 수동으로 날짜를 입력 합니다. 그러나 HTML5 새로운 기능이 며 아직 모든 브라우저에서 지원 되지 않습니다.
> 
> ASP.NET 웹 페이지에 입력 하는 사용자의 브라우저에서 HTML5 지원 합니다. 에 대 한 새 특성의 예측에 대 한는 `<input>` HTML5 요소 참조 [HTML &lt;입력&gt; type 특성을](http://www.w3schools.com/html/html_form_input_types.asp) W3Schools 사이트에 있습니다.


## <a name="creating-the-form"></a>폼 만들기

WebMatrix에서에서 **파일** 작업 영역을 열고는 *Movies.cshtml* 페이지.

닫은 후 `</h1>` 태그와 여 `<div>` 의 태그는 `grid.GetHtml` 호출, 다음 태그를 추가 합니다.

[!code-html[Main](form-basics/samples/sample2.html)]

이 태그에는 텍스트 상자가 라는 양식을 만듭니다 `searchGenre` 및 전송 단추가 있습니다. 텍스트 상자 및 단추에 포함 된 제출는 `<form>` 요소 인 `method` 특성이로 설정 된 `get`합니다. (텍스트 상자를 입력 하 고 전송 단추 내 하지 않는 경우는 `<form>` 요소인 아무 단추를 클릭할 때 제출할.) 사용 하면는 `GET` 동사 여기 폼을 작성 하는 동안에 변경 하지 않습니다 모든 서버에서-방금 검색에서 발생 합니다. (이전 자습서에서 사용 되는 `post` 메서드를 서버에 변경 내용을 전송 하는 방법입니다. 볼 수 있는 다음 자습서에서 다시 있습니다.)

페이지를 실행 합니다. 폼에 대 한 모든 동작을 정의 하지 않은 모양을 확인할 수 있습니다.

![검색 상자 장르에 대 한 동영상 페이지](form-basics/_static/image3.png)

"코미디."와 같은 텍스트 상자에 값을 입력 합니다. 클릭 **검색 장르**합니다.

페이지의 URL을 기록해 둡니다. 설정할 수 때문에 `<form>` 요소의 `method` 특성을 `get`, 입력 한 값은 다음과 같이 URL에 쿼리 문자열의 일부:

`http://localhost:45661/Movies.cshtml?searchGenre=Comedy`

## <a name="reading-form-values"></a>폼 값 읽기

페이지는 이미 존재 하지 않는 데이터베이스 데이터를 가져오고 결과 표에 표시 하는 일부 코드를 포함 합니다. 이제 검색 단어를 포함 하는 SQL 쿼리를 실행할 수 있도록 입력란의 값을 읽을 수 있는 일부 코드를 추가 해야 합니다.

폼의로 설정 하기 때문에 `get`, 다음과 같은 코드를 사용 하 여 텍스트 상자에 입력 한 값을 읽을 수 있습니다.

`var searchTerm = Request.QueryString["searchGenre"];`

`Request.QueryString` 개체 (의 `QueryString` 속성은 `Request` 개체)의 일부로 제출 된 요소의 값이 포함 됩니다는 `GET` 작업 합니다. `Request.QueryString` 속성 포함는 *컬렉션* (목록)의 형태로 전송 된 값입니다. 개별 값을 가져오려면 원하는 요소의 이름을 지정 합니다. 바로 이러한 이유로을 보유 해야는 `name` 특성을 `<input>` 요소 (`searchTerm`) 텍스트 상자를 만듭니다. (에 대 한 자세한는 `Request` 개체, 참조는 [사이드바](#BKMK_TheRequestObject) 나중.)

것은 입력란의 값을 읽을 수 있을 만큼 간단 합니다. 하지만 사용자를 입력 하지 않았습니다 아무 것도 전혀 텍스트 상자에 있지만 클릭 하면 **검색** 유효함을 검색 하는 것 이므로 해당 클릭 무시할 수 있습니다.

다음 코드는 이러한 조건을 구현 하는 방법을 보여 주는 예제입니다. (아직이 코드를 추가할 필요가 없습니다; 잠시 후에 작업입니다)입니다.

[!code-csharp[Main](form-basics/samples/sample3.cs)]

테스트는 이러한 방식으로 나눕니다.

- 값을 가져올 `Request.QueryString["searchGenre"]`, 즉에 입력 한 값은 `<input>` 라는 요소 `searchGenre`합니다.
- 비어 있는지를 사용 하 여 확인 된 `IsEmpty` 메서드. 이 메서드는 값이 포함 된 항목 (예를 들어 폼 요소) 여부를 결정 하는 표준 방법입니다. 실제로, 경우에 주의 하지만 *하지* 빈, 따라서...
- 추가 `!` 앞의 연산자는 `IsEmpty` 테스트 합니다. (의 `!` 연산자 의미 논리적 NOT).

전체 간단한 영어로 `if` 조건 다음으로 변환: *다음 폼의 searchGenre 요소를 비어 있지 않은 경우...*

이 블록 검색 단어를 사용 하는 쿼리를 만들기 위한 단계를 설정 합니다. 다음 섹션에 있는 수행 합니다.

<a id="BKMK_TheRequestObject"></a>

> [!TIP] 
> 
> **요청 개체**
> 
> `Request` 개체 브라우저 페이지 요청 또는 제출 하는 경우 응용 프로그램에 보내는 모든 정보를 포함 합니다. 이 개체는 텍스트 상자의 값 또는 업로드할 파일을와 같은 사용자가 제공 하는 모든 정보를 포함 합니다. 모든 종류의 값 (있는 경우) URL 쿼리 문자열에 쿠키와 같은 추가 정보에도 실행 중인 브라우저에 설정 된 언어 목록에 사용자를 사용 하 여 브라우저의 유형은 해당 페이지의 파일 경로 를 훨씬 더 많은 하 고 있습니다.
> 
> `Request` 개체가 *컬렉션* (목록)의 값입니다. 이름을 지정 하 여 컬렉션에서 개별 값을 가져옵니다.
> 
> `var someValue = Request["name"];`
> 
> `Request` 개체는 실제로 여러 가지 하위 집합을 제공 합니다. 예를 들어:
> 
> - `Request.Form` 제출 된 내의 요소에서 값을 제공 `<form>` 요청인 경우 요소는 `POST` 요청 합니다.
> - `Request.QueryString` 사용 하면 값만의 URL의 쿼리 문자열입니다. (같은 URL에서 `http://mysite/myapp/page?searchGenre=action&page=2`, `?searchGenre=action&page=2` URL의 섹션은 쿼리 문자열입니다.)
> - `Request.Cookies` 컬렉션은 브라우저에 보내지는 쿠키에 액세스할 수 있습니다.
> 
> 사용자가 알고 있는 값을 얻으려면는 제출 된 형태로 사용할 수 있습니다, `Request["name"]`합니다. 또는 특정 버전을 사용할 수 `Request.Form["name"]` (에 대 한 `POST` 요청) 또는 `Request.QueryString["name"]` (에 대 한 `GET` 요청)입니다. 물론, *이름* 가져올 항목의 이름입니다.
> 
> 가져올 항목의 이름을를 사용 하는 컬렉션 내에서 고유 해야 합니다. 바로 이러한 이유로 `Request` 개체는 하위 집합을와 같은 제공 `Request.Form` 및 `Request.QueryString`합니다. 이라는 폼 요소를 페이지에 있다고 가정 `userName` 및 *도* 라는 쿠키가 포함 `userName`합니다. 발생 하는 경우 `Request["userName"]`, 것 모호 합니다. 폼 값 또는 쿠키 삭제할지 합니다. 그러나 발생 하는 경우 `Request.Form["userName"]` 또는 `Request.Cookie["userName"]`, 어떤 값을 가져올 방법에 대 한 명시적 예요.
> 
> 특정 수의 하위 집합을 사용 하는 것이 좋습니다 `Request` 관심 같은 하 `Request.Form` 또는 `Request.QueryString`합니다. 이 자습서에서 만드는 간단한 페이지에 대 한 것 아마도 하지 않는 실제로 사항이 적용 합니다. 그러나 더 복잡 한 페이지를 만들 버전을 사용 하는 명시적 `Request.Form` 또는 `Request.QueryString` 폼 (또는 여러 개의 폼) 페이지에 포함 되어 있는 경우 발생할 수 있는 문제를 방지 하는 데 도움이 쿠키, 쿼리 문자열 값, 및 등입니다.


## <a name="creating-a-query-by-using-a-search-term"></a>검색 단어를 사용 하 여 쿼리 만들기

사용자가 입력 한 검색 용어를 가져오는 방법을 배웠으므로를 사용 하는 쿼리를 만들 수 있습니다. 데이터베이스에서 모든 동영상 항목을 가져오려면 사용 하는 경우이 문은 같은 SQL 쿼리를 고려 하세요.

`SELECT * FROM Movies`

포함 하는 쿼리를 사용 해야만 특정 영화를 얻기 위해는 `Where` 절. 이 절은 쿼리에 의해 반환 된 행에는 조건을 설정할 수 있습니다. 예를 들면 다음과 같습니다.

`SELECT * FROM Movies WHERE Genre = 'Action'`

기본 형식은 `WHERE column = value`합니다. Just 외에 다른 연산자를 사용할 수 있습니다 `=`처럼 `>` (보다 큼), `<` (보다 작음), `<>` (같지 않음), `<=` (작거나 같음), 원하는 항목에 따라 등입니다.

SQL 문은 본다면, 하는 경우 대/소문자 구분 하지 않습니다 &mdash; `SELECT` 동일 `Select` (또는 심지어 `select`). 그러나 사용자 종종 대문자로 SQL 문에 키워드 같은 `SELECT` 및 `WHERE`, 보다 쉽게 읽을 수 있도록 합니다.

### <a name="passing-the-search-term-as-a-parameter"></a>검색 단어를 매개 변수로 전달

특정 장르는 아주 쉽게 검색 (`WHERE Genre = 'Action'`), 사용자가 입력 하는 모든 장르를 검색 하려고 합니다. 이렇게 하려면으로 검색 하는 값에 대 한 자리 표시자를 포함 하는 SQL 쿼리를 만듭니다. 이 명령은 같이 것이 보입니다.

`SELECT * FROM Movies WHERE Genre = @0`

자리 표시자는는 `@` 문자 다음에 0 개 있습니다. 쿼리에는 여러 자리 표시 자가 포함 될 수 있으며 이라는 짐작할 수 `@0`, `@1`, `@2`등입니다.

쿼리를 설정 하 고 실제로 값을 전달 하려면 다음과 같은 코드 사용.

[!code-sql[Main](form-basics/samples/sample4.sql)]

이 코드까지 이미 작업 한 내용을 모눈에 데이터를 표시 하는 것과 비슷합니다. 유일한 차이점은:

- 자리 표시자를 포함 하는 쿼리 (`WHERE Genre = @0"`).
- 쿼리를 변수로 저장 됩니다 (`selectCommand`)으로 직접 쿼리를 전달 하기 전에;는 `db.Query` 메서드.
- 호출 하는 경우는 `db.Query` 메서드를 전달 하면 쿼리와 자리 표시자 사용할 값입니다. (에 전달는 쿼리가 여러 자리 표시 자가 있으면 모두 메서드에 별도 값으로.)

이러한 모든 요소를 함께 배치 하면 다음 코드를 얻습니다.

[!code-csharp[Main](form-basics/samples/sample5.cs)]

> [!NOTE] 
> 
> **중요!** 자리 표시자를 사용 하 여 (같은 `@0`)는 SQL 명령에 값을 전달할 *매우 중요* 보안에 대 한 합니다. 변수 데이터에 대 한 자리 표시자와 여기에서 보이는 방식은 유일한 방법은 SQL 명령 생성 해야 합니다.
> 
> (연결) 리터럴 텍스트와 사용자에 게 서 얻을 값을 함께 배치 하 여 SQL 문을 생성 하지 않습니다. 사이트를 열고 SQL 문으로 사용자 입력을 연결 하는 *SQL 주입 공격* 악의적인 사용자 페이지에 데이터베이스 hack 하는 값을 제출 하는 경우. (읽어볼 수 있는 문서에 [SQL 주입](https://msdn.microsoft.com/library/ms161953.aspx) MSDN 웹 사이트입니다.)


## <a name="updating-the-movies-page-with-search-code"></a>검색 코드와 함께 동영상 페이지를 업데이트합니다.

코드를 업데이트할 수 이제는 *Movies.cshtml* 파일입니다. 를 시작 하려면 페이지 맨 위에 있는 코드 블록의 코드를이 코드로 바꿉니다.

[!code-csharp[Main](form-basics/samples/sample6.cs)]

차이점은에 쿼리를 준비 했습니다는 `selectCommand` 변수와를 전송 하는 `db.Query` 나중입니다. 변수에 SQL 문을 배치 검색을 수행 하려면 수행할 수 있는 문을 변경할 수 있습니다.

나중에 다시 배치 것이 두 줄을도 제거 했습니다.

[!code-csharp[Main](form-basics/samples/sample7.cs)]

아직 쿼리를 실행 하려면 (즉, 호출 `db.Query`) 초기화 하지 않으려면는 `WebGrid` 도우미 아직 중 하나입니다. SQL 문을 실행 하는 결정 한 후 작업을 수행 합니다.

다시 작성된이 블록 다음 검색을 처리 하기 위한 새 논리를 추가할 수 있습니다. 완성 된 코드는 다음과 같이 표시 됩니다. 이 예제와 일치 하도록 페이지에 코드를 업데이트 합니다.

[!code-cshtml[Main](form-basics/samples/sample8.cshtml)]

페이지는 이제 다음과 같이 작동합니다. 페이지 실행 될 때마다 코드가 데이터베이스와 `selectCommand` 변수에서 레코드를 모두 가져온 하는 SQL 문을로 설정 됩니다는 `Movies` 테이블입니다. 초기화 코드는 `searchTerm` 변수입니다.

그러나 현재 요청에 대 한 값을 포함 하는 경우는 `searchGenre` 요소, 코드 집합 `selectCommand` 다른 쿼리를-포함 하려면 즉,는 `Where` 절 장르를 찾으려고 합니다. 또한 설정 `searchTerm` (nothing 일 수) 있는 검색 상자에 대 한 전달 되는 항목에 있습니다.

SQL에 관계 없이 문이에 `selectCommand`, 호출 `db.Query` 쿼리를 실행 하려면 전달 어떤 중인 `searchTerm`합니다. 없으면 `searchTerm`, 뿐 아니라,이 경우 값을 전달 하려면 매개 변수가 있기 때문에 `selectCommand` 그래도 합니다.

코드를 초기화 하는 마지막으로 `WebGrid` 마찬가지로 전에 쿼리 결과 사용 하 여 도우미입니다.

변수로 검색어 유연성에 추가한 코드 및 있는 SQL 문을 배치 하 여 확인할 수 있습니다. 이 자습서의 뒷부분에 나오는 하겠지만이 기본 프레임 워크를 사용할 수 및 다양 한 유형의 검색에 대 한 논리를 계속 추가 합니다.

## <a name="testing-the-search-by-genre-feature"></a>테스트 장르 하 여 검색 기능

WebMatrix에서 실행 된 *Movies.cshtml* 페이지. 페이지가 장르에 대 한 텍스트 상자를 표시합니다.

사용자 테스트 레코드 중 하나에 대해 입력 한 다음 클릭 장르 입력 **검색**합니다. 이 시간 해당 장르의 일치 하는 동영상 방금 목록이 표시 됩니다.

![동영상 페이지 장르 'Comedies'에 대 한 검색 후 나열](form-basics/_static/image4.png)

다른 장르를 입력 하 고 다시 검색 합니다. 검색은 대/소문자 구분을 볼 수 있도록 대 / 소문자 모두에 대 한 모든 문자를 사용 하 여 장르를 입력 하십시오.

## <a name="remembering-what-the-user-entered"></a>사용자 입력 한 "기억"

알 수 있습니다는 장르를 입력 하 고 클릭 한 후 **검색 장르**, 해당 장르의 목록을 표시 합니다. 그러나 검색 텍스트 상자 비어 &mdash; 것 즉,에 입력 했다고 기억 하지 않았습니다.

이 문제가 발생 하는 이유를 이해 하는 것이 유용 합니다. 페이지를 전송한 브라우저 요청을 웹 서버에 보냅니다. ASP.NET 요청을 수신할 때 페이지의 새 인스턴스를 만듭니다, 그리고에서 코드를 실행 하 고 브라우저에 페이지를 다시 렌더링 합니다. 실제로 하지만 페이지가 모릅니다는 작업 중이 던 자체의 이전 버전입니다. it 요청을 받았지만 일부를 알고 모두에 데이터를 형성 합니다.

페이지 요청 될 때마다 &mdash; 처음으로 또는 전송 &mdash; 새 페이지를 가져오는 합니다. 웹 서버에 마지막 요청이의 메모리가 없습니다. ASP.NET, 없으며도 브라우저를 수행 합니다. 페이지의 이러한 별도 인스턴스 간의 유일한 연결이 서로 전송 하는 데이터가 있습니다. 페이지를 전송한 경우 예를 들어 새 페이지 인스턴스 데이터를 가져올 수는 양식 이전 인스턴스에서 보낸 합니다. (페이지 간에 데이터를 전달 하는 다른 방법은 쿠키를 사용 합니다.)

이러한 상황을 설명 하는 정식 방식 웹 페이지에는 여기서 협력 이란 *상태 비저장*합니다. 웹 서버와 페이지 자체 및 페이지의 요소에는 페이지의 이전 상태에 대 한 정보를 유지 하지 않습니다. 웹 개별 요청에 대 한 상태를 유지 관리 신속 하 게 소모 하 게 리소스 종종 수천, 어쩌면 처리 하는 웹 서버에도 수십만 개의 초 당 요청 때문에 이러한 방식으로 설계 되었습니다.

그렇기 때문 텍스트 상자가 비어 있습니다. 페이지에 제출 ASP.NET 페이지의 새 인스턴스를 생성 하 고 코드 및 태그를 통해 실행 합니다. 텍스트 상자에 값을 배치 하기 위해 ASP.NET에 지시 하는 해당 코드에서 nothing 있었습니다. 따라서 ASP.NET 작동 하지 않습니다, 그리고 및 텍스트 상자에 값이 없는 렌더링 되었습니다.

실제로이 문제를 해결 하는 쉬운 방법이 있습니다. 텍스트 상자에 입력 한 장르 *은* 코드에서 사용할 수 있는 &mdash; 중인 `Request.QueryString["searchGenre"]`합니다.

텍스트 상자에 대 한 태그를 업데이트 하는 `value` 특성에서 값을 가져오는 `searchTerm`,이 예제에서와 같이:

[!code-html[Main](form-basics/samples/sample9.html?highlight=1)]

이 페이지에는 설정할 수도 있습니다는 `value` 특성을 `searchTerm` 해당 변수는 장르 포함 되어 있으므로 변수를 입력 합니다. 하지만 사용 하 여는 `Request` 설정 하는 개체는 `value` 특성와 같이이 작업을 수행 하는 표준 방법은 다음과 같습니다. (도이 작업을 수행 하려는 경우 &mdash; 페이지를 렌더링 하려는 경우에 따라 *없이* 필드의 값입니다. 이것은 모두 응용 프로그램 진행 상황입니다.)

> [!NOTE]
> 기억할 수 없으면 "" 암호에 사용 되는 입력란의 값입니다. 코드를 사용 하 여 암호 필드에 입력할 수 있도록 보안 문제가 됩니다.


페이지를 다시 실행는 장르를 입력 하 고, 클릭 **검색 장르**합니다. 이 시간 뿐만 아니라 수행 하면 검색 결과가 표시 되는데 텍스트 상자의 마지막으로 입력을 기억:

![페이지에 텍스트 상자에 ' 저장 ' 이전 항목](form-basics/_static/image5.png)

## <a name="searching-for-any-word-in-the-title"></a>제목에 단어 검색

모든 장르 이제 검색할 수 있지만 한 title을 검색할 수도 있습니다. 가져오려는 제목을 정확 하 게 검색 하는 경우, 대신 제목을 안쪽 아무 곳 이나 표시 되는 단어를 검색할 수 있습니다는 것이 어렵습니다. SQL에서 그렇게 하려면 사용는 `LIKE` 연산자 및 구문에는 다음과 같습니다.

`SELECT * FROM Movies WHERE Title LIKE '%adventure%'`

이 명령은 제목에 해당 어구가 포함 "adventure" 모든 동영상을 가져옵니다. 사용 하는 경우는 `LIKE` 와일드 카드 문자를 포함 하면 연산자를 `%` 검색 단어의 일환으로 합니다. 검색 `LIKE 'adventure%'` "'adventure'로 시작"을 의미 합니다. (기술적으로 "는 문자열 'adventure' 뒤에 나오는" 의미) 마찬가지로, 검색 단어 `LIKE '%adventure'` "모든 항목을 의미 다음 문자열 'adventure'", "'adventure'로 끝나는" 말 하는 다른 방법입니다.

검색어 `LIKE '%adventure%'` "adventure'는 제목에." 사용 "을 의미 하므로 (기술적으로 "모든 제목, 뒤에 나오는 'adventure' 뒤에.")

내에서 `<form>` 요소를 닫기 바로 아래에서 다음 태그를 추가 `</div>` 장르 검색에 대 한 태그 (닫는 직전 `</form>` 요소):

[!code-html[Main](form-basics/samples/sample10.html)]

이 검색을 처리 하는 코드는 장르 검색에 대 한 코드를 제외 하으로 만들어 준비는 `LIKE` 검색 합니다. 추가 페이지 맨 위에 있는 코드 블록 안에 `if` 블록 바로 뒤의 `if` 장르 검색에 대 한 블록:

[!code-csharp[Main](form-basics/samples/sample11.cs)]

제외 하 고 검색에 사용 하 여이 코드에서는 앞에서 언급 했 동일한 논리를 사용는 `LIKE` 연산자와 코드 넣습니다 "`%`" 검색어 전후.

다른 검색 페이지에 추가할 쉬웠지만 방법을 확인 합니다. 모든 지 작업을 수행 하는 다음과 같습니다.

- 만들기는 `if` 블록 관련 검색 상자에 값이 있는지 여부를 확인 하려면 테스트 합니다.
- 설정의 `selectCommand` 새 SQL 문을 변수입니다.
- 설정의 `searchTerm` 변수를 쿼리에 전달 하는 값입니다.

다음은 제목 검색에 대 한 새 논리를 포함 하는 전체 코드 블록이입니다.

[!code-cshtml[Main](form-basics/samples/sample12.cshtml)]

다음은이 코드에서 수행 하는 작업의 요약이입니다.

- 변수 `searchTerm` 및 `selectCommand` 위쪽에 초기화 됩니다. 이러한 변수를 적절 한 검색 단어 (있는 경우)으로 설정 하려고 하 고 적절 한 SQL 명령 페이지에서 사용자가 기반 키를 누릅니다. 기본 검색은 간단한 형태는 데이터베이스에서 모든 동영상을 가져오는입니다.
- 에 대 한 테스트에 `searchGenre` 및 `searchTitle`, 코드 집합 `searchTerm` 에 대 한 검색 하려는 값입니다. 이러한 코드 블록을 설정할 수도 `selectCommand` 해당 검색에 대 한 적절 한 SQL 명령에 대 한 합니다.
- `db.Query` 메서드를 한 번만 사용 하 여 모든 SQL 명령이 `selectedCommand` 값 이며 `searchTerm`합니다. (없음 genre 및 없는 제목 단어) 검색 단어가 없는 경우의 값 `searchTerm` 은 빈 문자열입니다. 그러나 문제가 되지 경우 쿼리 매개 변수가 필요 없으므로 합니다.

## <a name="testing-the-title-search-feature"></a>제목 검색 기능 테스트

이제 완료 된 검색 페이지를 테스트할 수 있습니다. 실행 *Movies.cshtml*합니다.

장르를 입력 하 고 클릭 **검색 장르**합니다. 모눈 전에 등의 해당 장르의 영화를 표시합니다.

제목 단어를 입력 하 고 클릭 **제목 검색**합니다. 표 제목에 해당 단어가 포함 된 동영상을 표시 합니다.

![동영상 페이지 제목에 '는'에 대 한 검색 후 나열](form-basics/_static/image6.png)

두 텍스트 상자를 비워 두고 단추 중 하나를 클릭 합니다. 표에 모든 영화 표시 됩니다.

## <a name="combining-the-queries"></a>쿼리를 결합합니다.

검색을 수행할 수는 없습니다 것을 확인할 수 있습니다. 두 검색 상자에 해당 값이 있는 경우에 제목과 장르 같은 시간에 검색할 수 없습니다. 예를 들어 제목이 "Adventure"를 포함 하는 모든 작업 동영상을 검색할 수 없습니다. (페이지는 장르와 제목에 대 한 값을 입력 한 경우 이제 코딩 된,으로 제목을 검색이 가져옵니다 우선 순위를.) 조건을 결합 하는 검색을 만들려면 다음과 같은 구문이 있는 SQL 쿼리를 만들려면 해야 합니다.

`SELECT * FROM Movies WHERE Genre = @0 AND Title LIKE @1`

다음과 같은 문을 사용 하 여 쿼리를 실행 해야 합니다 (약 말하기):

`var selectedData = db.Query(selectCommand, searchGenre, searchTitle);`

검색 조건의 많은 순열 수 있도록 논리를 만드는 볼 수 있듯이 약간 관련 된 가져올 수 있습니다. 따라서 여기 중지 합니다.

## <a name="coming-up-next"></a>다음에 나오는

다음 자습서에서는 사용자가 동영상 데이터베이스에 추가할 수 있도록 폼을 사용 하는 페이지를 만듭니다.

## <a name="complete-listing-for-movie-page-updated-with-search"></a>동영상 페이지 (검색으로 업데이트 됨)에 대 한 전체 목록을 보려면

[!code-cshtml[Main](form-basics/samples/sample13.cshtml)]

## <a name="additional-resources"></a>추가 리소스

- [Razor 구문을 사용 하 여 ASP.NET 웹 프로그래밍 소개](https://go.microsoft.com/fwlink/?LinkID=202890)
- [SQL WHERE 절](http://www.w3schools.com/sql/sql_where.asp) W3Schools 사이트
- [메서드 정의](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) W3C 사이트 문서

> [!div class="step-by-step"]
> [이전](displaying-data.md)
> [다음](entering-data.md)
