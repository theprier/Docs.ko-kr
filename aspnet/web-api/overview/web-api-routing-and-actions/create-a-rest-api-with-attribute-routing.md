---
uid: web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
title: ASP.NET Web API 2에서에서 특성 라우팅을 사용 하 여 REST API 만들기 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/26/2013
ms.assetid: 23fc77da-2725-4434-99a0-ff872d96336b
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
msc.type: authoredcontent
ms.openlocfilehash: da3ca8f89f823fcb2c4ab74af6ddf4f61d4e663a
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41831562"
---
<a name="create-a-rest-api-with-attribute-routing-in-aspnet-web-api-2"></a>ASP.NET Web API 2에서에서 특성 라우팅을 사용 하 여 REST API 만들기
====================
[Mike Wasson](https://github.com/MikeWasson)

Web API 2에는 새 형식을 지 원하는 라우팅의 호출 *특성 라우팅은*합니다. 특성 라우팅의 일반적인 개요를 참조 하세요 [Web API 2에서 특성 라우팅](attribute-routing-in-web-api-2.md)합니다. 이 자습서에서는 사용할지 특성 라우팅은 컬렉션에 대 한 REST API를 만드는 합니다. API에는 다음 작업을 지원 해야 합니다.

| 작업 | URI 예제 |
| --- | --- |
| 모든 책 목록을 가져옵니다. | api 설명서 |
| 책 id 가져오기 | /api/books/1 |
| 책의 세부 정보를 가져옵니다. | /api/books/1/details |
| 장르별 책 목록을 가져옵니다. | /api/books/fantasy |
| 게시 날짜별으로 책 목록을 가져옵니다. | /api/books/date/2013-02-16 /api/books/date/2013/02/16 (대체 형식) |
| 특정 작성자가 발행 한 책 목록을 가져옵니다. | /api/authors/1/books |

모든 메서드는 읽기 전용 (HTTP GET 요청 수)입니다.

데이터 계층에 대 한 Entity Framework를 사용 하겠습니다. 책 레코드에는 다음 필드가 포함 됩니다.

- ID
- 제목
- 장르
- 게시 날짜
- 가격
- 설명
- AuthorID (작성자가 테이블에 외래 키)

그러나 대부분의 요청에 대 한 API (title, author 및 장르)이이 데이터의 하위 집합을 반환 됩니다. 전체 레코드, 클라이언트 요청을 가져오려면 `/api/books/{id}/details`합니다.

## <a name="prerequisites"></a>전제 조건

[Visual Studio 2017](https://www.visualstudio.com/vs/) Community, Professional 또는 Enterprise edition.

## <a name="create-the-visual-studio-project"></a>Visual Studio 프로젝트 만들기

Visual Studio를 실행 하 여 시작 합니다. **파일** 메뉴에서 **새로 만들기** 선택한 후 **프로젝트**합니다.

에 **템플릿** 창 **설치 된 템플릿** 확장 하 고는 **Visual C#** 노드. 아래 **Visual C#** 를 선택 **웹**합니다. 프로젝트 템플릿 목록에서 선택 **ASP.NET MVC 4 웹 응용 프로그램**합니다. 프로젝트 이름을 &quot;BooksAPI&quot;합니다.

![](create-a-rest-api-with-attribute-routing/_static/image1.png)

에 **새 ASP.NET 프로젝트** 대화 상자에서 선택 합니다 **빈** 템플릿. "폴더를 추가 및 코어에 대 한 참조"를 선택 합니다 **Web API** 확인란을 선택 합니다. 클릭 **프로젝트를 만들**합니다.

![](create-a-rest-api-with-attribute-routing/_static/image2.png)

이 Web API 기능에 대해 구성 된 기본 프로젝트를 만듭니다.

### <a name="domain-models"></a>도메인 모델

다음으로 도메인 모델에 대 한 클래스를 추가 합니다. 솔루션 탐색기에서 Models 폴더를 마우스 오른쪽 단추로 클릭 합니다. 선택 **추가**을 선택한 후 **클래스**합니다. 클래스 이름을 `Author`로 지정합니다.

![](create-a-rest-api-with-attribute-routing/_static/image3.png)

Author.cs에서 코드를 다음으로 바꿉니다.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample1.cs)]

이제 라는 또 다른 클래스를 추가할 `Book`합니다.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample2.cs)]

### <a name="add-a-web-api-controller"></a>웹 API 컨트롤러 추가

이 단계에서는 데이터 계층으로 Entity Framework를 사용 하는 웹 API 컨트롤러를 추가 합니다.

Ctrl+Shift+B를 눌러 프로젝트를 빌드합니다. Entity Framework 리플렉션을 사용 하 여 컴파일된 어셈블리를 데이터베이스 스키마를 만들어야 하므로 모델의 속성을 검색 합니다.

솔루션 탐색기에서 컨트롤러 폴더를 마우스 오른쪽 단추로 클릭 합니다. 선택 **추가**을 선택한 후 **컨트롤러**합니다.

![](create-a-rest-api-with-attribute-routing/_static/image4.png)

에 **스 캐 폴드 추가** 대화 상자에서 "Web API 2 Entity Framework를 사용 하 여 읽기/쓰기 동작이 포함 된 컨트롤러입니다."

[![](create-a-rest-api-with-attribute-routing/_static/image6.png)](create-a-rest-api-with-attribute-routing/_static/image5.png)

에 **컨트롤러 추가** 대화 상자에서에 대 한 **컨트롤러 이름**를 입력 &quot;BooksController&quot;합니다. 선택 된 &quot;비동기 컨트롤러 동작을 사용 하 여&quot; 확인란을 선택 합니다. 에 대 한 **모델 클래스**를 선택 &quot;책&quot;합니다. (표시 되지 않는 경우는 `Book` 드롭다운에 나열 된 클래스, 프로젝트를 빌드할 수 있는지 확인 합니다.) "+" 단추를 클릭 합니다.

![](create-a-rest-api-with-attribute-routing/_static/image7.png)

클릭 **추가** 에 **새 데이터 컨텍스트에** 대화 합니다.

![](create-a-rest-api-with-attribute-routing/_static/image8.png)

클릭 **추가** 에 **컨트롤러 추가** 대화 합니다. 라는 클래스를 추가 하는 스 캐 폴딩을 `BooksController` API 컨트롤러를 정의 하는 합니다. 라는 클래스도 추가 `BooksAPIContext` 데이터 컨텍스트 Entity Framework에 대 한 정의 Models 폴더에 있습니다.

![](create-a-rest-api-with-attribute-routing/_static/image9.png)

### <a name="seed-the-database"></a>데이터베이스 시드

도구 메뉴에서 선택 **라이브러리 패키지 관리자**를 선택한 후 **패키지 관리자 콘솔**합니다.

패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample3.ps1)]

이 명령은 마이그레이션 폴더를 만들고 Configuration.cs 라는 새 코드 파일을 추가 합니다. 이 파일을 열고 다음 코드를 추가 합니다 `Configuration.Seed` 메서드.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample4.cs)]

패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample5.ps1)]

이러한 명령은 로컬 데이터베이스를 만들고 데이터베이스를 채우는 데 시드 메서드를 호출 합니다.

![](create-a-rest-api-with-attribute-routing/_static/image10.png)

## <a name="add-dto-classes"></a>DTO 클래스를 추가 합니다.

이제 응용 프로그램을 실행 하 고 /api/books/1 GET 요청을 보낼 응답은 다음과 비슷합니다. (읽기 쉽도록 들여쓰기 추가 했습니다.)

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample6.json)]

대신,이 요청을 필드의 하위 집합을 반환 합니다. 또한 원하는 작성자 ID 대신 작성자의 이름을 반환 합니다. 이를 위해 반환 하는 컨트롤러 메서드가 수정 된 *데이터 전송 개체* (DTO) EF 모델 대신 합니다. DTO는만 데이터를 전송 하도록 설계 하는 개체입니다.

솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가** | **새 폴더**합니다. 폴더의 이름을 &quot;Dto&quot;합니다. 라는 클래스를 추가 `BookDto` Dto 폴더로 다음 정의 사용 하 여:

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample7.cs)]

라는 다른 클래스를 추가 `BookDetailDto`합니다.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample8.cs)]

다음으로 업데이트 합니다 `BooksController` 반환할 클래스 `BookDto` 인스턴스. 사용 하 여 합니다 [Queryable.Select](https://msdn.microsoft.com/library/system.linq.queryable.select.aspx) 프로젝트 방법 `Book` 인스턴스를 `BookDto` 인스턴스. 컨트롤러 클래스에 대 한 업데이트 된 코드는 다음과 같습니다.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample9.cs)]

> [!NOTE]
> 삭제 합니다 `PutBook`, `PostBook`, 및 `DeleteBook` 메서드를이 자습서에 필요 하지 않은 때문에 합니다.


이제 응용 프로그램을 실행 하 고 /api/books/1 요청 응답 본문 다음과 같이 표시 됩니다.

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample10.json)]

## <a name="add-route-attributes"></a>경로 특성 추가

다음으로, 특성 라우팅을 사용 하도록 컨트롤러를 변환 합니다. 먼저 추가 하는 **RoutePrefix** 컨트롤러 특성입니다. 이 특성은이 컨트롤러에서 모든 메서드에 대 한 초기 URI 세그먼트를 정의 합니다.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample11.cs?highlight=1)]

추가한 **[Route]** 컨트롤러 작업에 특성을 다음과 같이 합니다.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample12.cs?highlight=1,7)]

각 컨트롤러 메서드에 대 한 경로 템플릿에 접두사와 문자열에 지정 된 **경로** 특성입니다. 에 대 한 합니다 `GetBook` 매개 변수가 있는 문자열을 포함 하는 메서드를 경로 템플릿에 &quot;{id: int}&quot;와 일치 하는 URI 세그먼트를 정수 값을 포함 하는 경우.

| 메서드 | 경로 템플릿 | URI 예제 |
| --- | --- | --- |
| `GetBooks` | "api/books" | `http://localhost/api/books` |
| `GetBook` | "api/books/{id:int}" | `http://localhost/api/books/5` |

## <a name="get-book-details"></a>책 세부 정보 가져오기

클라이언트는 GET 요청을 전송 하는 데 책 세부 정보를 가져오려면 `/api/books/{id}/details`, 여기서 *{id}* 책의 ID입니다.

다음 메서드를 `BooksController` 클래스에 추가합니다.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample13.cs)]

요청 하는 경우 `/api/books/1/details`, 응답은 다음과 같습니다.

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample14.json)]

## <a name="get-books-by-genre"></a>장르별 책 가져오기

클라이언트는 GET 요청을 전송 하는 데 특정 장르에 책 목록을 가져오려고 `/api/books/genre`, 여기서 *장르* 장르의 이름입니다. `/api/books/fantasy` 등을 예로 들 수 있습니다.

다음 메서드를 추가 `BooksController`합니다.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample15.cs)]

다음 URI 템플릿에서 {장르} 매개 변수를 포함 하는 경로 정의 합니다. 웹 API는 이러한 두 Uri를 구분 하 고 다른 메서드로 라우팅할 수 있는지 확인 합니다.

`/api/books/1`

`/api/books/fantasy`

있기 때문입니다는 `GetBook` 메서드 "id" 세그먼트를 정수 값 이어야 하는 제약 조건이 포함 되어 있습니다.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample16.cs?highlight=1)]

/Api/books/fantasy를 요청 하는 경우 응답은 다음과 같습니다.

`[ { "Title": "Midnight Rain", "Author": "Ralls, Kim", "Genre": "Fantasy" }, { "Title": "Maeve Ascendant", "Author": "Corets, Eva", "Genre": "Fantasy" }, { "Title": "The Sundered Grail", "Author": "Corets, Eva", "Genre": "Fantasy" } ]`

## <a name="get-books-by-author"></a>작성자가 발행 한 책 가져오기

클라이언트는 GET 요청을 전송 하는 데 특정 작성자에 대 한는 책 목록을 가져오려고 `/api/authors/id/books`, 여기서 *id* 작성자의 ID입니다.

다음 메서드를 추가 `BooksController`합니다.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample17.cs)]

이 예제는 흥미로운 때문 &quot;책&quot; 는의 자식 리소스를 처리 &quot;작성자&quot;합니다. 이 패턴은 RESTful Api에 매우 일반적입니다.

경로 템플릿에 물결표 (~)의 경로 접두사를 재정의 합니다 **RoutePrefix** 특성입니다.

## <a name="get-books-by-publication-date"></a>온라인 설명서를 게시 날짜별으로 가져오기

클라이언트는 GET 요청을 전송 하는 데 책의 목록이 게시 날짜별으로 가져오려는 `/api/books/date/yyyy-mm-dd`, 여기서 *yyyy-월-일* 날짜입니다.

이 작업을 수행 하는 한 가지 방법은 다음과 같습니다.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample18.cs)]

합니다 `{pubdate:datetime}` 매개 변수가 일치 하도록 제한 되는 **DateTime** 값입니다. 이 방법이 작동 하지만 보다 실제로 더 허용 되는 것입니다. 예를 들어, 다음이 Uri 경로 일치 합니다.

`/api/books/date/Thu, 01 May 2008`

`/api/books/date/2000-12-16T00:00:00`

이러한 Uri를 허용 합니다. 문제가 없습니다. 그러나 특정 형식으로 경로 경로 템플릿에 정규식 제약 조건을 추가 하 여 제한할 수 있습니다.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample19.cs?highlight=1)]

이제 날짜만 형태로 &quot;yyyy-월-일&quot; 일치 합니다. 실제 날짜 했습니다 유효성을 검사 하는 regex 사용 하지는 알 수 있습니다. Web API에 URI 세그먼트 변환 하려고 할 때 처리 하는 **날짜/시간** 인스턴스. 잘못 된 날짜와 같은 ' 2012-47-99' 변환에 실패 하 고 클라이언트는 404 오류를 가져옵니다.

슬래시로 구분 기호를 지원할 수도 있습니다 (`/api/books/date/yyyy/mm/dd`) 다른 더하여 **[Route]** 다른 regex 사용 하 여 특성입니다.

[!code-html[Main](create-a-rest-api-with-attribute-routing/samples/sample20.html)]

작지만 중요 한 내용이 여기 포함 되어 있습니다. 두 번째 경로 템플릿은 와일드 카드 문자 (\*) {pubdate} 매개 변수의 시작 합니다.

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample21.json)]

이렇게 하면 라우팅 엔진이 해당 {pubdate} URI의 나머지와 일치 해야 합니다. 기본적으로 템플릿 매개 변수는 단일 URI 세그먼트를 찾습니다. 이 경우 여러 URI 세그먼트에 걸쳐 {pubdate} 하려면:

`/api/books/date/2013/06/17`

## <a name="controller-code"></a>컨트롤러 코드

BooksController 클래스에 대 한 전체 코드는 다음과 같습니다.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample22.cs)]

## <a name="summary"></a>요약

특성 라우팅을 사용 하면 더 많은 제어와 유연성 API에 대 한 Uri를 디자인 하는 경우.
