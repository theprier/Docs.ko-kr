---
uid: single-page-application/overview/introduction/knockoutjs-template
title: '단일 페이지 응용 프로그램: KnockoutJS 템플릿 | Microsoft Docs'
author: MikeWasson
description: Knockout 템플릿
ms.author: aspnetcontent
ms.date: 01/30/2013
ms.assetid: f9c07af0-4b20-4b08-af8f-47fc3df169a2
msc.legacyurl: /single-page-application/overview/introduction/knockoutjs-template
msc.type: authoredcontent
ms.openlocfilehash: 9e48c7033cefe8b6e4c456577b7a6448f9815d0b
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37832531"
---
<a name="single-page-application-knockoutjs-template"></a>단일 페이지 응용 프로그램: KnockoutJS 템플릿
====================
[Mike Wasson](https://github.com/MikeWasson)

> ASP.NET 및 웹 도구 2012.2의 일부인 Knockout MVC 템플릿
> 
> [ASP.NET 및 Web Tools 2012.2 다운로드](https://go.microsoft.com/fwlink/?LinkId=282650)


ASP.NET MVC 4에 대 한 단일 페이지 응용 프로그램 (SPA) 템플릿을 포함 하는 ASP.NET 및 웹 도구 2012.2 업데이트 합니다. 이 템플릿은 신속 하 게 대화형 클라이언트 쪽 웹 앱을 빌드하기 시작할 수 있도록 설계 되었습니다.

"단일 페이지 응용 프로그램" (SPA)은 하나의 HTML 페이지를 로드 하 고 그런 다음 새 페이지를 로드 하는 대신 페이지를 동적으로 업데이트 하는 웹 응용 프로그램에 대 한 일반 용어입니다. 초기 페이지 로드 후 SPA AJAX 요청을 통해 서버를 사용 하 여 설명합니다.

![](knockoutjs-template/_static/image1.png)

AJAX 새 nothing 하지만 현재 있다는 쉽게 구축 하 고 대형 정교한 SPA 응용 프로그램을 관리 하는 JavaScript 프레임 워크입니다. 또한 html5 및 CSS3는 쉽게 다양 한 Ui를 만듭니다.

시작 하기, SPA 템플릿 샘플 "할 일 모음" 응용 프로그램을 만듭니다. 이 자습서에서는 템플릿의 둘러보기를 알아보겠습니다. 먼저에서는 할 일 목록 응용 프로그램 자체를 확인 하 고 작동 하는 기술 구성 요소를 검사 합니다.

## <a name="create-a-new-spa-template-project"></a>새 SPA 템플릿 프로젝트 만들기

요구 사항:

- Visual Studio 2012 또는 Visual Studio Express 2012 for Web
- ASP.NET Web Tools 2012.2 업데이트합니다. 업데이트를 설치할 수 있습니다 [여기](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2)합니다.

Visual Studio를 시작 하 고 선택 **새 프로젝트** 시작 페이지에서. 또는에서 **파일** 메뉴에서 **새로 만들기** 차례로 **프로젝트**합니다.

에 **템플릿** 창 **설치 된 템플릿** 확장 하 고는 **Visual C#** 노드. 아래 **Visual C#** 를 선택 **웹**합니다. 프로젝트 템플릿 목록에서 선택 **ASP.NET MVC 4 웹 응용 프로그램**합니다. 프로젝트 이름을 지정 하 고 클릭 **확인**합니다.

![](knockoutjs-template/_static/image2.png)

에 **새 프로젝트** 마법사 **단일 페이지 응용 프로그램**합니다.

![](knockoutjs-template/_static/image3.png)

F5 키를 눌러 응용 프로그램을 빌드하고 실행합니다. 응용 프로그램을 처음 실행 하면 로그인 화면을 표시 합니다.

![](knockoutjs-template/_static/image4.png)

클릭 합니다 &quot;등록&quot; 연결 하 고 새 사용자를 만듭니다.

![](knockoutjs-template/_static/image5.png)

로그인 하면 응용 프로그램 기본 할 일 목록을 항목 두 개를 사용 하 여 만듭니다. "할 일 목록 추가" 클릭 수 새 목록을 추가 합니다.

![](knockoutjs-template/_static/image6.png)

목록 이름 바꾸기, 목록에 항목 추가 및 확인 하 합니다. 항목을 삭제 하거나 전체 목록을 삭제할 수도 있습니다. 변경 내용을 서버의 데이터베이스에 자동으로 유지 됩니다 (실제로 LocalDB이 시점에서 로컬로 실행 하는 응용 프로그램 때문에).

![](knockoutjs-template/_static/image7.png)

## <a name="architecture-of-the-spa-template"></a>SPA 템플릿의 아키텍처

이 다이어그램에서는 응용 프로그램에 대 한 기본 구성 요소를 보여 줍니다.

![](knockoutjs-template/_static/image8.png)

서버 쪽에서 ASP.NET MVC는 HTML을 사용 하 고도 폼 기반 인증을 처리 합니다.

ASP.NET Web API ToDoLists 및 ToDoItems, 가져오기, 만들기, 업데이트 및 삭제를 포함 하 여와 관련 된 모든 요청을 처리 합니다. 클라이언트는 JSON 형식으로 웹 API를 사용 하 여 데이터를 교환합니다.

EF (entity Framework)는 O/RM 계층입니다. ASP.NET의 개체 지향 환경 및 기본 데이터베이스 간을 중재 하는 것입니다. 데이터베이스에서 LocalDB를 사용 하지만 Web.config 파일에서이 변경할 수 있습니다. 일반적으로 LocalDB를 사용 하 여 로컬 개발 하는 서버에서 SQL database에 배포 후 EF 코드 중심 마이그레이션을 사용 하 여 합니다.

클라이언트 쪽에서 Knockout.js 라이브러리 AJAX 요청에서 페이지 업데이트를 처리합니다. Knockout은 데이터 바인딩의 사용 하 여 최신 데이터를 사용 하 여 페이지를 동기화 합니다. JSON 데이터를 안내 하 고 DOM을 업데이트 하는 코드를 작성할 필요가 이런 방식으로 대신, Knockout 데이터를 표시 하는 방법을 알려 주는 HTML의 선언적 특성을 배치할 수 있습니다.

이 아키텍처의 가장 큰 장점은 응용 프로그램 논리에서 프레젠테이션 계층을 분리 하는 합니다. 웹 페이지에 어떻게 보이는지에 대 한 지식이 없어도 웹 API 부분을 만들 수 있습니다. 클라이언트 쪽에서 모델을 만든 "보기"를 해당 데이터를 나타내고 보기 모델은 HTML 바인딩할 Knockout을 사용 합니다. 뷰 모델을 변경 하지 않고 HTML을 쉽게 변경할 수 있습니다. (살펴보겠습니다 Knockout 잠시.)

## <a name="models"></a>모델

Visual Studio 프로젝트에서 Models 폴더 서버 쪽에서 사용 되는 모델을 포함 합니다. (클라이언트 쪽에서 모델도 됩니다;으로 다룰 예정입니다.)

![](knockoutjs-template/_static/image9.png)

**TodoItem, TodoList**

이들은 Entity Framework Code First에 대 한 데이터베이스 모델입니다. 이러한 모델에 서로를 가리키는 속성이 있는지 확인 합니다. `ToDoList` ToDoItems, 및 각 컬렉션을 포함 `ToDoItem` 다시 ToDoList 부모에 대 한 참조가 있습니다. 이러한 속성에는 탐색 속성 이라고 하 고 할 일 목록 및 해당 할 일 항목에 일 대 다 관계를 나타냅니다.

`ToDoItem` 클래스도 사용 합니다 **[ForeignKey]** 지정 하는 특성 `ToDoListId` 에 외래 키를 `ToDoList` 테이블. 이렇게 하면 EF 데이터베이스에 외래 키 제약 조건을 추가 합니다.

[!code-csharp[Main](knockoutjs-template/samples/sample1.cs)]

**TodoItemDto, TodoListDto**

이러한 클래스는 클라이언트에 전송 될 데이터를 정의 합니다. "DTO"는 "데이터 전송 개체입니다." DTO는 엔터티를 JSON으로 serialize 될 하는 방법을 정의 합니다. 일반적으로 Dto를 사용 하는 몇 가지 이유는

- 제어 하는 속성이 serialize 됩니다. DTO는 도메인 모델에서 속성의 하위 집합을 포함할 수 있습니다. 이렇게 하면 수 있습니다 (중요 한 데이터 숨기려면) 보안상의 이유로 또는 간단 하 게 보내는 데이터의 양을 줄일 수.
- 예를 들어 데이터의 셰이프를 변경 하려면를 더 복잡 한 데이터 구조를 평면화 할 수 있습니다.
- 유지 하기 위해 DTO (중요 한 부분의 분리)에서 모든 비즈니스 논리.
- 어떤 이유로 도메인 모델을 직렬화 할 수 없습니다 하는 경우. 예를 들어 순환 참조 문제가 발생할 수 있습니다 가지 개체를 serialize 할 때 웹 API에서이 문제를 처리 하는 방법 (참조 [개체 순환 참조가 처리](../../../web-api/overview/formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references)); DTO를 사용 하 여 간단히 문제를 피할 수 모두 있지만.

SPA 템플릿 Dto는 동일한 도메인 모델 데이터를 포함 합니다. 그러나 이들은 여전히 유용 하므로 탐색 속성에서 순환 참조 방지 및 일반 DTO 패턴을 보여 줍니다.

**AccountModels.cs**

이 파일에 사이트 멤버 자격에 대 한 모델을 포함 합니다. `UserProfile` 클래스 멤버 자격 DB에서에서 사용자 프로필에 대 한 스키마를 정의 합니다. (이 예제의 경우 정보만 경우 사용자 이름과 사용자 ID) 이 파일의 다른 모델 클래스는 사용자 등록 및 로그인 forms를 만드는 데 사용 됩니다.

## <a name="entity-framework"></a>Entity Framework

SPA 템플릿 EF Code First를 사용 합니다. Code First 개발에서 코드에서 먼저 모델을 정의 하 고 EF가 데이터베이스를 만들 모델을 사용 하는 다음. 기존 데이터베이스를 사용 하 여 EF를 사용할 수도 있습니다 ([Database First](https://msdn.microsoft.com/data/jj206878.aspx)).

합니다 `TodoItemContext` Models 폴더에는 클래스에서 파생 되며 **DbContext**합니다. 이 클래스는 EF 모델 사이의 "접착제"를 제공합니다. `TodoItemContext` 보유 한 `ToDoItem` 컬렉션 및 `TodoList` 컬렉션입니다. 데이터베이스를 쿼리하려면 단순히 이러한 컬렉션에 대해 LINQ 쿼리를 작성 합니다. 예를 들어 다음과 같습니다. 모든 사용자 "Alice"에 대 한 일 목록을 선택할 수는 방법

[!code-csharp[Main](knockoutjs-template/samples/sample2.cs)]

도 컬렉션에 새 항목을 추가, 항목을 업데이트 또는 컬렉션에서 항목을 삭제 하 수 데이터베이스에 변경 내용을 유지 합니다.

## <a name="aspnet-web-api-controllers"></a>ASP.NET Web API 컨트롤러

ASP.NET Web API 컨트롤러에는 HTTP 요청을 처리 하는 개체입니다. 웹 API를 사용 하 여에서 CRUD 작업을 사용 하도록 설정 하려면 SPA 템플릿을 언급 했 듯이 `ToDoList` 고 `ToDoItem` 인스턴스. 컨트롤러는 솔루션의 컨트롤러 폴더에 있습니다.

![](knockoutjs-template/_static/image10.png)

- `TodoController`:-할 일 항목에 대 한 HTTP 요청을 처리 하는 중
- `TodoListController`: 할 일 목록에 대 한 HTTP 요청을 처리 합니다.

이러한 이름은 Web API 컨트롤러 이름에 대 한 URI 경로 일치 하므로 중요 합니다. (Web API 컨트롤러에 HTTP 요청을 라우팅하 하는 방법에 대해 알아보려면 [ASP.NET Web API에서 라우팅](../../../web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api.md).)

살펴보겠습니다는 `ToDoListController` 클래스입니다. 단일 데이터 멤버를 포함합니다.

[!code-csharp[Main](knockoutjs-template/samples/sample3.cs)]

`TodoItemContext` 앞에서 설명한 대로 EF를 사용 하 여 통신 하는 데 사용 됩니다. 컨트롤러의 메서드에 CRUD 작업을 구현합니다. Web API 컨트롤러 메서드에 클라이언트로부터 HTTP 요청을 다음과 같이 매핑합니다.

| HTTP 요청 | 컨트롤러 메서드 | 설명 |
| --- | --- | --- |
| GET /api/todo | `GetTodoLists` | 할 일 목록 컬렉션을 가져옵니다. |
| GET/a pi/todo/*id* | `GetTodoList` | ID 별로 할 일 목록 가져오기 |
| PUT/a pi/todo/*id* | `PutTodoList` | 할 일 목록을 업데이트합니다. |
| POST /api/todo | `PostTodoList` | 새 할 일 목록을 만듭니다. |
| 삭제/a pi/todo/*id* | `DeleteTodoList` | 할 일 목록을 삭제합니다. |

일부 작업에 대 한 Uri는 ID 값에 대 한 자리 표시 자가 포함 되어 있는지 확인 합니다. 예를 들어 목록을 삭제 하려면에-42 ID 사용 하 여, URI가 `/api/todo/42`합니다.

CRUD 작업에 대 한 Web API를 사용 하는 방법에 대 한 자세한 내용은 참조 하세요 [Web API에서는 CRUD 작업을 만드는](../../../web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations.md)합니다. 이 컨트롤러에 대 한 코드는 매우 간단 합니다. 몇 가지 흥미로운 요소는 다음과 같습니다.

- `GetTodoLists` 메서드는 LINQ 쿼리를 사용 하 여 로그인 한 사용자의 ID로 결과 필터링 합니다. 이런 방식으로 사용자 님에 속하는 데이터를만 표시 됩니다. 또한 변환 하는 Select 문을 사용 하는 확인 합니다 `ToDoList` 인스턴스를 `TodoListDto` 인스턴스.
- PUT 및 POST 메서드는 데이터베이스를 수정 하기 전에 모델 상태를 확인 합니다. 하는 경우 **ModelState.IsValid** 이 false 인 경우 이러한 메서드는 HTTP 400 잘못 된 요청을 반환 합니다. 웹 API의 모델 유효성 검사에 대해 자세히 알아보세요 [모델 유효성 검사](../../../web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api.md)합니다.
- 컨트롤러 클래스는 또한 데코 레이트 합니다 **[Authorize]** 특성입니다. 이 특성은 HTTP 요청이 인증 되었는지 여부를 확인 합니다. 요청이 인증 되지 않은 클라이언트는 HTTP 401 권한 없음. 인증에 자세히 읽어보세요 [인증 및 권한 부여 ASP.NET Web API에서](../../../web-api/overview/security/authentication-and-authorization-in-aspnet-web-api.md)합니다.

합니다 `TodoController` 클래스는 매우 비슷합니다 `TodoListController`합니다. 가장 큰 차이점 이므로 모든 GET 메서드를 정의 하지 않는 클라이언트는 각 할 일 목록 함께 할 일 항목을 가져옵니다.

## <a name="mvc-controllers-and-views"></a>MVC 컨트롤러 및 보기

MVC 컨트롤러도 솔루션의 컨트롤러 폴더에 있습니다. `HomeController` 응용 프로그램에 대 한 기본 HTML을 렌더링합니다. 홈 컨트롤러에 대 한 보기 Views/Home/Index.cshtml에서 정의 됩니다. 홈 보기 사용자 로그인 여부에 따라 다른 콘텐츠를 렌더링 합니다.

[!code-cshtml[Main](knockoutjs-template/samples/sample4.cshtml)]

사용자가 로그인 하면 기본 UI를 표시 됩니다. 그렇지 않으면 로그인 패널에 표시 됩니다. 서버 쪽에서이 조건부 렌더링을 수행 하는 참고 합니다. 클라이언트 쪽에서 중요 한 콘텐츠를 숨기 제거해 서는 안 & #8212anything HTTP 응답에 보내는 원시 HTTP 메시지를 감시 하는 사람에 게 표시 됩니다.

## <a name="client-side-javascript-and-knockoutjs"></a>클라이언트 쪽 JavaScript 및 Knockout.js

이제 클라이언트 응용 프로그램의 서버 쪽에서 보겠습니다. SPA 템플릿 원활 하 고 대화형 UI를 만들기 위해 jQuery 및 Knockout.js 조합을 사용 합니다. Knockout.js에 쉽게 HTML 데이터를 바인딩할 수 있도록 하는 JavaScript 라이브러리입니다. Knockout.js "모델-뷰-ViewModel입니다." 이라는 패턴을 사용 하 여

- 모델은 도메인 데이터 (할 일 목록 및 할 일 항목).
- 보기는 HTML 문서입니다.
- 보기-모델에는 모델 데이터를 보유 하는 JavaScript 개체입니다. 보기-모델은 ui 코드 추상화 합니다. 이 HTML 표현의 알지 못합니다. 대신 "할 일 항목을 목록"와 같은 뷰의 추상 기능을 나타냅니다.

뷰는 데이터 바인딩된 뷰 모델입니다. 보기-모델에 대 한 업데이트 보기에서 자동으로 반영 됩니다. 바인딩을 다른 방향으로도 작동합니다. 이벤트 (예: 클릭)를 DOM에는 데이터 바인딩된 함수 뷰 모델에서 AJAX 호출을 트리거하는 합니다.

세 가지 계층으로 클라이언트 쪽 JavaScript를 구성 하는 SPA 템플릿:

- todo.datacontext.js: AJAX 요청을 보냅니다.
- todo.model.js: 모델을 정의 합니다.
- todo.viewmodel.js: 보기 모델을 정의 합니다.

![](knockoutjs-template/_static/image11.png)

이러한 스크립트 파일은 솔루션의 스크립트/앱 폴더에 있습니다.

![](knockoutjs-template/_static/image12.png)

**todo.datacontext** Web API 컨트롤러에 대 한 모든 AJAX 호출을 처리 합니다. (로그인에 대 한 AJAX 호출에에서 정의 된 다른 곳에서 ajaxlogin.js.)

**todo.model.js** 할 일 목록에 대 한 클라이언트 쪽 (브라우저) 모델을 정의 합니다. 두 모델 클래스: todoItem 및 todoList 합니다.

모델 클래스의 속성 중 상당수는 "ko.observable" 유형입니다. 관찰 가능 개체는 Knockout 있을까요는 핵심입니다. [Knockout 설명서](http://knockoutjs.com/documentation/introduction.html):는 관찰 가능 개체는 "JavaScript 개체 변경 내용에 대 한 구독자에 알릴 수 있는." 관찰 가능 개체의 값이 변경 되 면 Knockout 해당 관찰 가능 개체에 바인딩된 모든 HTML 요소를 업데이트 합니다. 예를 들어 todoItem 제목과 수행 속성에 대 한 관찰 가능 개체에 있습니다.

[!code-javascript[Main](knockoutjs-template/samples/sample5.js)]

코드에서 관찰 가능 개체를 구독할 수도 있습니다. 예를 들어, "수행" 및 "title" 속성의 변경 내용에 todoItem 클래스 구독:

[!code-javascript[Main](knockoutjs-template/samples/sample6.js)]

**뷰 모델**

뷰 모델 todo.viewmodel.js에서 정의 됩니다. 뷰 모델은 중앙 위치를 응용 프로그램 도메인 데이터를 HTML 페이지 요소에 바인딩합니다. SPA 템플릿 뷰 모델은 observable 배열의 todoLists 포함 합니다. 보기 모델에 다음 코드를 지시 Knockout 바인딩을 적용 하려면:

[!code-javascript[Main](knockoutjs-template/samples/sample7.js)]

## <a name="html-and-data-binding"></a>HTML 및 데이터 바인딩

페이지에 대 한 기본 HTML Views/Home/Index.cshtml에서 정의 됩니다. 데이터 바인딩을 사용 하기 때문에 HTML에 렌더링할 실제로 무엇에 대 한 템플릿일 뿐입니다. 다음을 사용 하 여 knockout *선언적* 바인딩. 데이터 요소에 "데이터 바인딩" 특성을 추가 하 여 페이지 요소를 바인딩합니다. Knockout 설명서에서 가져온는 매우 간단한 예제는 다음과 같습니다.

[!code-html[Main](knockoutjs-template/samples/sample8.html)]

이 예제에서는 Knockout 업데이트의 콘텐츠를 **&lt;s p a n&gt;** 의 값을 가진 요소가 `myItems.count()`합니다. 이 값이 변경 될 때마다 Knockout 문서를 업데이트 합니다.

Knockout 다양 한 다른 바인딩 유형 제공합니다. SPA 템플릿에서 사용 하는 바인딩이 다음과 같습니다.

- **foreach**: 루프를 반복 하 고 목록의 각 항목에 동일한 태그를 적용할 수 있습니다. 이 작업은 할 일 목록 및 할 일 항목 렌더링에 사용 됩니다. 내 합니다 **foreach**, 바인딩이 목록의 요소에 적용 됩니다.
- **표시**: 표시 설정/해제 하는 데 사용 합니다. 오류 메시지를 표시 되도록 하거나 컬렉션이 비어 있을 때 태그를 숨깁니다.
- **값**: 양식 값을 채우는 데 사용 합니다.
- **클릭**: 클릭 이벤트를 뷰 모델에서 함수에 바인딩합니다.

## <a name="anti-csrf-protection"></a>CSRF 방지 보호

교차 사이트 요청 위조 (CSRF)은 악성 사이트 보내는 요청에 있는 사용자가 현재 로그인 한 취약 한 사이트를 공격 합니다. ASP.NET MVC에서 CSRF 공격을 방지 하려면 다음을 사용 합니다. *위조 방지 토큰*, 요청 확인 토큰 라고도 합니다. 서버 웹 페이지에 임의로 생성 된 토큰을 배치 하는 합니다. 서버로 데이터를 전송 하는 클라이언트를이 요청 메시지의이 값이 포함 되어야 합니다.

위조 방지 토큰에는 악의적인 페이지 동일 원본 정책으로 인해 사용자의 토큰을 읽을 수 없으므로 작동 합니다. (동일 원본 정책에서 다른 사용자의 콘텐츠에 액세스 하는 두 개의 다른 사이트에 호스트 된 문서를 방지 합니다.)

ASP.NET MVC를 통해 위조 방지 토큰에 대 한 기본 제공 지원을 제공 합니다 [AntiForgery](https://msdn.microsoft.com/library/system.web.helpers.antiforgery.aspx) 클래스와 [[ValidateAntiForgeryToken]](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute.aspx) 특성입니다. 현재이 기능에 포함 되어 있지 Web API입니다. 그러나 SPA 템플릿을 웹 API에 대 한 사용자 지정 구현을 포함합니다. 이 코드에 정의 된는 `ValidateHttpAntiForgeryTokenAttribute` 솔루션의 필터 폴더에 있는 클래스입니다. Web API에서 CSRF 방지 하는 방법에 대 한 자세한 내용은 참조 하세요 [교차 사이트 요청 위조 (CSRF) 공격](../../../web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks.md)합니다.

## <a name="conclusion"></a>결론

최신, 대화형 웹 응용 프로그램을 신속 하 게 작성을 시작 하는 데 SPA 템플릿을 디자인 합니다. Knockout.js 라이브러리를 사용 하 여 구분 하는 데이터 및 응용 프로그램 논리에서 프레젠테이션 (HTML 태그). 하지만 Knockout SPA를 만드는 데 사용할 수 있는 유일한 JavaScript 라이브러리를 아닙니다. 몇 가지 다른 옵션 탐색 하려는 경우 잠시 살펴 합니다 [커뮤니티에서 만든 SPA 템플릿을](../templates/index.md)합니다.
