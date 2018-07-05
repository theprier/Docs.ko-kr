---
uid: single-page-application/overview/templates/emberjs-template
title: EmberJS 템플릿 | Microsoft Docs
author: xqiu
description: EmberJS 템플릿
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/30/2013
ms.topic: article
ms.assetid: 04d5f142-5f62-494a-b5ea-4f3d068d34cb
ms.technology: ''
msc.legacyurl: /single-page-application/overview/templates/emberjs-template
msc.type: authoredcontent
ms.openlocfilehash: 1f5b005180fed15c51b36417cdcd6acc98123c9a
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37374168"
---
<a name="emberjs-template"></a>EmberJS 템플릿
====================
[Xinyang Qiu](https://github.com/xqiu)

> EmberJS MVC 템플릿 Nathan Totten, Thiago Santos Xinyang Qiu로 기록 됩니다.
> 
> [EmberJS MVC 템플릿 다운로드](https://go.microsoft.com/fwlink/?LinkId=282647)


EmberJS SPA 템플릿은 신속 하 게 EmberJS를 사용 하 여 대화형 클라이언트 쪽 웹 앱을 빌드하기 시작할 수 있도록 설계 되었습니다.

"단일 페이지 응용 프로그램" (SPA)은 하나의 HTML 페이지를 로드 하 고 그런 다음 새 페이지를 로드 하는 대신 페이지를 동적으로 업데이트 하는 웹 응용 프로그램에 대 한 일반 용어입니다. 초기 페이지 로드 후 SPA AJAX 요청을 통해 서버를 사용 하 여 설명합니다.

![](emberjs-template/_static/image1.png)

AJAX 새 nothing 하지만 현재 있다는 쉽게 구축 하 고 대형 정교한 SPA 응용 프로그램을 관리 하는 JavaScript 프레임 워크입니다. 또한 html5 및 CSS3는 쉽게 다양 한 Ui를 만듭니다.

EmberJS SPA 템플릿을 사용 하는 [Ember](http://emberjs.com/) AJAX 요청에서 페이지 업데이트를 처리 하는 JavaScript 라이브러리입니다. Ember.js는 데이터 바인딩의 사용 하 여 최신 데이터를 사용 하 여 페이지를 동기화 합니다. JSON 데이터를 안내 하 고 DOM을 업데이트 하는 코드를 작성할 필요가 이런 방식으로 대신, Ember.js 데이터를 표시 하는 방법을 알려 주는 HTML의 선언적 특성을 배치할 수 있습니다.

서버 쪽에서 EmberJS 템플릿은 거의 동일 합니다 [KnockoutJS SPA 템플릿](../introduction/knockoutjs-template.md)합니다. ASP.NET MVC를 사용 하 여 HTML 문서 및 클라이언트에서 AJAX 요청을 처리 하는 ASP.NET Web API를 제공 합니다. 서식 파일의 이러한 측면에 대 한 자세한 내용은 참조는 [KnockoutJS 템플릿](../introduction/knockoutjs-template.md) 설명서. 이 항목에서는 Knockout 템플릿 및 EmberJS 템플릿 간의 차이점에 중점을 둡니다.

## <a name="create-an-emberjs-spa-template-project"></a>EmberJS SPA 템플릿 프로젝트 만들기

다운로드 하 고 위의 다운로드 단추를 클릭 하 여 템플릿을 설치 합니다. Visual Studio를 다시 시작 해야 합니다.

에 **템플릿** 창 **설치 된 템플릿** 확장 하 고는 **Visual C#** 노드. 아래 **Visual C#** 를 선택 **웹**합니다. 프로젝트 템플릿 목록에서 선택 **ASP.NET MVC 4 웹 응용 프로그램**합니다. 프로젝트 이름을 지정 하 고 클릭 **확인**합니다.

![](emberjs-template/_static/image2.png)

에 **새 프로젝트** 마법사 **Ember.js SPA 프로젝트**합니다.

![](emberjs-template/_static/image4.png)

## <a name="emberjs-spa-template-overview"></a>EmberJS SPA 템플릿 개요

EmberJS 템플릿 jQuery, Ember.js, 부드러운, 대화형 UI를 만들기 위해 Handlebars.js의 조합을 사용 합니다.

Ember.js는 클라이언트 쪽 MVC 패턴을 사용 하는 JavaScript 라이브러리입니다.

- A *템플릿*, Handlebars 템플릿 언어로 작성 된 응용 프로그램 사용자 인터페이스를 설명 합니다. 릴리스 모드에서의 [Handlebars 컴파일러](https://github.com/Myslik/csharp-ember-handlebars) 번들 handlebars 템플릿을 하는 데 사용 됩니다.
- A *모델* (할 일 목록 및 할 일 항목) 서버에서 가져온 응용 프로그램 데이터를 저장 합니다.
- A *컨트롤러* 응용 프로그램 상태를 저장 합니다. 컨트롤러는 종종 해당 템플릿에 모델 데이터를 제공합니다.
- A *보기* 응용 프로그램에서 기본 이벤트를 변환 하 고 컨트롤러에 전달 합니다.
- A *라우터* Url 템플릿과 동기화 상태로 유지 되는 응용 프로그램 상태를 관리 합니다.

또한 JSON 개체 (RESTful API를 통해 서버에서 가져옴) 및 클라이언트 모델을 동기화 하는 Ember 데이터 라이브러리를 사용할 수 있습니다.

EmberJS SPA 템플릿 8 레이어로 스크립트를 구성 합니다.

- webapi\_adapter.js, webapi\_serializer.js: ASP.NET Web API를 사용 하려면 Ember 데이터 라이브러리를 확장 합니다.
- Scripts/helpers.js: 새 Ember Handlebars 도우미를 정의합니다.
- Scripts/app.js: 앱을 만들고 어댑터 및 serializer를 구성 합니다.
- 스크립트/app/모델/\*.js: 모델을 정의 합니다.
- 스크립트/app/뷰/\*.js: 뷰를 정의 합니다.
- 스크립트/app/컨트롤러/\*.js: 컨트롤러를 정의 합니다.
- 스크립트/app/routes, Scripts/app/router.js: 경로 정의합니다.
- 템플릿 /\*.hbs: handlebars 템플릿을 정의 합니다.

자세한 세부 정보에서 이러한 스크립트 중 일부에 대해 살펴보겠습니다.

## <a name="models"></a>모델

모델은 스크립트/app/models 폴더에 정의 됩니다. 모델 파일이 두 개: todoItem.js 및 todoList.js 합니다.

**todo.model.js** 할 일 목록에 대 한 클라이언트 쪽 (브라우저) 모델을 정의 합니다. 두 모델 클래스: todoItem 및 todoList 합니다. Ember와, 모델에는 DS의 서브 클래스입니다. 모델입니다. 모델 속성에 특성을 포함할 수 있습니다.

[!code-javascript[Main](emberjs-template/samples/sample1.js)]

모델은 다른 모델에 관계를 정의할 수 있습니다.

[!code-css[Main](emberjs-template/samples/sample2.css)]

모델을 다른 속성에 바인딩하는 속성 계산 수 있습니다.

[!code-javascript[Main](emberjs-template/samples/sample3.js)]

모델에는 관찰 된 속성이 변경 될 때 호출 되는 관찰자 함수를 포함할 수 있습니다.

[!code-javascript[Main](emberjs-template/samples/sample4.js)]

## <a name="views"></a>보기

뷰는 스크립트/app/views 폴더에 정의 됩니다. 뷰는 응용 프로그램 UI에서에서 이벤트를 변환합니다. 이벤트 처리기 다시 컨트롤러 함수를 호출 하거나 단순히 데이터 컨텍스트를 직접 호출할 수 있습니다.

예를 들어, 다음 코드는 views/TodoItemEditView.js에서. 입력된 텍스트 필드에 대 한 처리 이벤트를 정의 합니다.

[!code-javascript[Main](emberjs-template/samples/sample5.js)]

## <a name="controller"></a>컨트롤러

컨트롤러는 스크립트/app/controllers 폴더에서 정의 됩니다. 단일 모델을 나타내기 위해 확장 `Ember.ObjectController`:

[!code-javascript[Main](emberjs-template/samples/sample6.js)]

컨트롤러를 확장 하 여 모델의 컬렉션을 나타낼 수도 있습니다 `Ember.ArrayController`합니다. 예를 들어 TodoListController 나타내는의 배열 `todoList` 개체입니다. 컨트롤러 내림차순 todoList ID를 기준으로 정렬 합니다.

[!code-javascript[Main](emberjs-template/samples/sample7.js)]

명명 된 함수를 정의 하는 컨트롤러 `addTodoList`, 새 todoList 생성 되 고 배열에 추가 합니다. 이 함수는 호출 하는 방법을 보려는 Templates 폴더에 todoListTemplate.html 라는 템플릿 파일을 엽니다. 다음 템플릿 코드는 단추를 바인딩하는 `addTodoList` 함수:

[!code-html[Main](emberjs-template/samples/sample8.html)]

컨트롤러도 포함 되어 있습니다를 `error` 오류 메시지를 보유 하는 속성입니다. (또한 todoListTemplate.html)에서 오류 메시지를 표시 하는 템플릿 코드는 다음과 같습니다.

[!code-html[Main](emberjs-template/samples/sample9.html)]

## <a name="routes"></a>경로

경로 및 응용 프로그램 상태 집합을 표시 하려면 기본 템플릿을 정의 하 고 Url 경로 일치 하는 Router.js:

[!code-javascript[Main](emberjs-template/samples/sample10.js)]

TodoListRoute.js는 setupController 함수를 재정의 하 여는 TodoListRoute에 대 한 데이터를 로드 합니다.

[!code-javascript[Main](emberjs-template/samples/sample11.js)]

Ember와 Url, 경로 이름, 컨트롤러 및 템플릿을 일치 하도록 명명 규칙을 사용 합니다. 자세한 내용은 [ http://emberjs.com/guides/routing/defining-your-routes/ ](http://emberjs.com/guides/routing/defining-your-routes/) EmberJS 설명서.

## <a name="templates"></a>템플릿

템플릿 폴더에 4 개의 템플릿이 포함 되어 있습니다.

- application.hbs: 응용 프로그램이 시작 될 때 렌더링 되는 기본 서식 파일입니다.
- about.hbs: "/ 정보" 경로 대 한 템플릿.
- index.hbs: 루트에 대 한 템플릿 경로 "/"입니다.
- todoList.hbs:에 대 한 서식 파일은 "/ todo" 경로.
- \_navbar.hbs: 템플릿을 탐색 메뉴를 정의 합니다.

응용 프로그램 템플릿은 마스터 페이지 처럼 작동합니다. 머리글, 바닥글 및 "{{출 선}}" 경로 따라 다른 템플릿을에서 삽입할 포함 합니다. Ember와의 응용 프로그램 템플릿에 대 한 자세한 내용은 참조 하세요. [ http://guides.emberjs.com/v1.10.0/templates/the-application-template// ](http://guides.emberjs.com/v1.10.0/templates/the-application-template/)합니다.

"/ todoList" 템플릿 두 루프 식을 포함 합니다. 외부 루프 `{{#each controller}}`, 및 내부 루프는 `{{#each todos}}`합니다. 다음 코드에서는 기본 제공 `Ember.Checkbox` 보고, 사용자 지정 `App.TodoItemEditView`, 및 사용 하 여 링크를 `deleteTodo` 작업 합니다.

[!code-html[Main](emberjs-template/samples/sample12.html)]

합니다 `HtmlHelperExtensions` Controllers/HtmlHelperExensions.cs에에서 정의 된 클래스 도우미를 정의 할 때 파일을 캐시 하 고 템플릿 삽입 함수 **디버그** 로 설정 되어 **true** Web.config 파일에서. 이 함수는 Views/Home/App.cshtml에 정의 된 ASP.NET MVC 뷰 파일에서 호출 됩니다.

[!code-cshtml[Main](emberjs-template/samples/sample13.cshtml)]

함수는 템플릿 폴더에 템플릿 파일의 모든 렌더링 인수 없이 호출 합니다. 하위 폴더 또는 특정 템플릿 파일을 지정할 수 있습니다.

때 **디버그** 됩니다 **false** Web.config에서 응용 프로그램에는 번들 항목 "~/bundles/templates"이 포함 됩니다. 이 번들 항목 BundleConfig.cs, Handlebars 컴파일러 라이브러리를 사용 하 여에 추가 됩니다.

[!code-csharp[Main](emberjs-template/samples/sample14.cs)]
