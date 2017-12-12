---
uid: single-page-application/overview/templates/emberjs-template
title: "EmberJS 템플릿 | Microsoft Docs"
author: xqiu
description: "EmberJS 서식 파일"
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/30/2013
ms.topic: article
ms.assetid: 04d5f142-5f62-494a-b5ea-4f3d068d34cb
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /single-page-application/overview/templates/emberjs-template
msc.type: authoredcontent
ms.openlocfilehash: 1fb7633aee288be648d4f9681b43c8911b7dbab9
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="emberjs-template"></a>EmberJS 서식 파일
====================
으로 [Xinyang Qiu](https://github.com/xqiu)

> EmberJS MVC 템플릿에서 Nathan Totten, Thiago Santos 및 Xinyang Qiu 작성 됩니다.
> 
> [EmberJS MVC 템플릿 다운로드](https://go.microsoft.com/fwlink/?LinkId=282647)


EmberJS SPA 템플릿은 EmberJS를 사용 하 여 대화형 클라이언트 쪽 웹 앱을 빠르게 빌드할 시작 하도록 설계 되었습니다.

"단일 페이지 응용 프로그램" (SPA)은 하나의 HTML 페이지를 로드 하 고 다음 새 페이지를 로드 하는 대신 해당 페이지를 동적으로 업데이트 하는 웹 응용 프로그램에 대 한 일반적인 용어입니다. 초기 로드 이후에 SPA AJAX 요청을 통해 서버와 통신 합니다.

![](emberjs-template/_static/image1.png)

AJAX 새로 만들었거나, nothing 하지만 오늘 쉽게 작성 하 고 대형 정교한 SPA 응용 프로그램을 관리 하는 JavaScript 프레임 워크 있습니다. 또한 HTML 5 및 CSS3는 보다 쉽게 풍부한 Ui를 만들 합니다.

EmberJS SPA 템플릿을 사용 하 여는 [불씨](http://emberjs.com/) JavaScript 라이브러리에서 AJAX 요청 페이지 업데이트를 처리 하도록 합니다. Ember.js는 데이터 바인딩을 사용 하 여 최신 데이터로 페이지를 동기화 합니다. 이런 방식으로 없는 JSON 데이터를 안내 하 고 DOM을 업데이트 하는 코드 작성 대신, 선언적 특성을 Ember.js 데이터를 표시 하는 방법을 알려 주는 HTML에 넣습니다.

서버 쪽에서 EmberJS 서식 파일은 거의 동일 하지만 [KnockoutJS SPA 템플릿](../introduction/knockoutjs-template.md)합니다. ASP.NET MVC를 사용 하 여 HTML 문서 및 클라이언트에서 AJAX 요청을 처리 하는 ASP.NET Web API를 제공 합니다. 서식 파일의 이러한 측면에 대 한 자세한 내용은 참조는 [KnockoutJS 템플릿](../introduction/knockoutjs-template.md) 설명서입니다. 이 항목 Knockout 템플릿과 EmberJS 서식 파일 간의 차이점에 중점을 둡니다.

## <a name="create-an-emberjs-spa-template-project"></a>EmberJS SPA 서식 파일 프로젝트 만들기

다운로드 하 고 위의 다운로드 단추를 클릭 하 여 서식 파일을 설치 합니다. Visual Studio를 다시 시작 해야 합니다.

에 **템플릿** 창 선택 **설치 된 템플릿** 확장는 **Visual C#** 노드. 아래 **Visual C#**선택, **웹**합니다. 프로젝트 템플릿 목록에서 선택 **ASP.NET MVC 4 웹 응용 프로그램**합니다. 프로젝트 이름을 지정 하 고 클릭 **확인**합니다.

![](emberjs-template/_static/image2.png)

에 **새 프로젝트** 선택 마법사 **Ember.js SPA 프로젝트**합니다.

![](emberjs-template/_static/image4.png)

## <a name="emberjs-spa-template-overview"></a>EmberJS SPA 템플릿 개요

EmberJS 템플릿은 jQuery, Ember.js, 부드러운, 대화형 UI를 만들려면 Handlebars.js의 조합을 사용 합니다.

Ember.js는 클라이언트 쪽 MVC 패턴을 사용 하는 JavaScript 라이브러리입니다.

- A *템플릿*핸들 템플릿 언어로 작성 된 응용 프로그램 사용자 인터페이스에 설명 합니다. 릴리스 모드에서의 [핸들 컴파일러](https://github.com/Myslik/csharp-ember-handlebars) 묶고 핸들 템플릿을 하는 데 사용 됩니다.
- A *모델* (할 일 목록 및 할 일 항목)는 서버에서 가져오는 응용 프로그램 데이터를 저장 합니다.
- A *컨트롤러* 응용 프로그램 상태를 저장 합니다. 컨트롤러는 종종 해당 템플릿에 모델 데이터를 제공합니다.
- A *보기* 응용 프로그램의 기본 이벤트를 변환 하 고 컨트롤러에 전달 합니다.
- A *라우터* 동기화 Url 및 서식 파일을 유지 하는 응용 프로그램 상태를 관리 합니다.

또한 동기화 (RESTful API를 통해 서버에서 얻은) JSON 개체와 클라이언트 모델 불씨 데이터 라이브러리를 사용할 수 있습니다.

EmberJS SPA 서식 파일에서는 스크립트는 8 개의 계층으로 구분 합니다.

- webapi\_adapter.js, webapi\_serializer.js:는 ASP.NET Web API를 사용 하려면 불씨 데이터 라이브러리를 확장 합니다.
- Scripts/helpers.js: 새 불씨 핸들 도우미를 정의합니다.
- Scripts/app.js: 응용 프로그램을 만들고 어댑터 및 serializer를 구성 합니다.
- 스크립트/응용프로그램/모델/\*.js: 모델을 정의 합니다.
- 스크립트/응용프로그램/뷰/\*.js: 뷰를 정의 합니다.
- 스크립트/응용프로그램/컨트롤러/\*.js: 컨트롤러를 정의 합니다.
- 스크립트/응용 프로그램/경로, Scripts/app/router.js:는 경로 정의 합니다.
- 템플릿 /\*.hbs: 핸들 템플릿을 정의 합니다.

이러한 스크립트를 보다 자세히 살펴보겠습니다.

## <a name="models"></a>모델

스크립트/응용 프로그램/models 폴더에는 모델 정의 됩니다. 모델 파일이 두 개: todoItem.js 및 todoList.js 합니다.

**todo.model.js** 할 일 목록에 대 한 클라이언트 쪽 (브라우저) 모델을 정의 합니다. 모델 클래스: todoItem 및 todoList 합니다. 불씨, 모델 DS의 서브 클래스를은입니다. 모델입니다. 모델 속성에 특성을 가질 수 있습니다.

[!code-javascript[Main](emberjs-template/samples/sample1.js)]

모델은 다른 모델에 관계를 정의할 수 있습니다.

[!code-css[Main](emberjs-template/samples/sample2.css)]

모델 다른 속성에 바인딩하는 속성 계산 있을 수 있습니다.

[!code-javascript[Main](emberjs-template/samples/sample3.js)]

모델은 관찰 된 속성이 변경 될 때 호출 되는 관찰자 함수를 가질 수 있습니다.

[!code-javascript[Main](emberjs-template/samples/sample4.js)]

## <a name="views"></a>보기

스크립트/응용 프로그램/views 폴더에는 뷰 정의 됩니다. 뷰 이벤트를 응용 프로그램 UI로 변환합니다. 이벤트 처리기는 컨트롤러 기능을 다시 호출할 하거나 단순히 데이터 컨텍스트를 직접 호출할 수 있습니다.

예를 들어 다음 코드에서 views/TodoItemEditView.js입니다. 입력된 텍스트 필드에 대 한 처리 이벤트를 정의 합니다.

[!code-javascript[Main](emberjs-template/samples/sample5.js)]

## <a name="controller"></a>컨트롤러

컨트롤러는 스크립트/응용 프로그램/controllers 폴더에 정의 됩니다. 단일 모델을 나타내기 위해 확장 `Ember.ObjectController`:

[!code-javascript[Main](emberjs-template/samples/sample6.js)]

컨트롤러를 확장 하 여 모델의 컬렉션을 나타낼 수도 있습니다 `Ember.ArrayController`합니다. 예를 들어는 TodoListController 나타내는 배열을 `todoList` 개체입니다. 컨트롤러를 todoList ID 내림차순으로 정렬 합니다.

[!code-javascript[Main](emberjs-template/samples/sample7.js)]

라는 함수를 정의 하는 컨트롤러 `addTodoList`, 새 todoList 되 고 배열에 추가 합니다. 이 함수는 호출 하는 방법을 알아보려면 todoListTemplate.html 템플릿 폴더에 라는 템플릿 파일을 엽니다. 다음 템플릿 코드는 단추를 바인딩하는 `addTodoList` 함수:

[!code-html[Main](emberjs-template/samples/sample8.html)]

컨트롤러도 포함 되어는 `error` 오류 메시지를 보유 하는 속성입니다. (또한 todoListTemplate.html)에서 오류 메시지를 표시 하는 템플릿 코드는 다음과 같습니다.

[!code-html[Main](emberjs-template/samples/sample9.html)]

## <a name="routes"></a>경로

경로 및 응용 프로그램 상태를 집합을 표시 하려면 기본 서식 파일을 정의 하 고 경로에 Url을 일치 하는 Router.js:

[!code-javascript[Main](emberjs-template/samples/sample10.js)]

TodoListRoute.js는 setupController 함수를 재정의 하 여는 TodoListRoute에 대 한 데이터를 로드 합니다.

[!code-javascript[Main](emberjs-template/samples/sample11.js)]

불씨는 Url, 경로 이름, 컨트롤러 및 서식 파일에 맞게 명명 규칙을 사용 합니다. 자세한 내용은 참조 [http://emberjs.com/guides/routing/defining-your-routes/](http://emberjs.com/guides/routing/defining-your-routes/) EmberJS 설명서입니다.

## <a name="templates"></a>템플릿

템플릿 폴더에는 4 개의 템플릿이 있습니다.

- application.hbs: 응용 프로그램이 시작 될 때 렌더링 되는 기본 서식 파일입니다.
- about.hbs: "/ 약" 경로 대 한 서식 파일입니다.
- index.hbs: 루트에 대 한 서식 파일 "/" 경로입니다.
- todoList.hbs:에 대 한 서식 파일은 "/ todo" 경로입니다.
- \_navbar.hbs: 템플릿은 탐색 메뉴를 정의 합니다.

응용 프로그램 템플릿에서 마스터 페이지 처럼 작동합니다. 여기에 머리글, 바닥글 및 "{{콘센트}}" 경로 따라 다른 서식 파일에 삽입 하려면 포함 됩니다. 불씨의 응용 프로그램 템플릿에 대 한 자세한 내용은 참조 [http://guides.emberjs.com/v1.10.0/templates/the-application-template//](http://guides.emberjs.com/v1.10.0/templates/the-application-template/)합니다.

"/ todoList" 서식 파일에는 두 루프 식이 포함 되어 있습니다. 외부 루프는 `{{#each controller}}`와 안쪽 루프는 `{{#each todos}}`합니다. 다음 코드에서는 기본 제공 `Ember.Checkbox` 보고, 사용자 지정 `App.TodoItemEditView`, 및와 링크는 `deleteTodo` 동작 합니다.

[!code-html[Main](emberjs-template/samples/sample12.html)]

`HtmlHelperExtensions` Controllers/HtmlHelperExensions.cs에 정의 된 클래스 정의 도우미 함수를 캐시 하 고 템플릿 삽입 시 파일 **디버그** 로 설정 되어 **true** Web.config 파일에 있습니다. 이 함수는 Views/Home/App.cshtml에 정의 된 ASP.NET MVC 뷰 파일에서 호출 됩니다.

[!code-cshtml[Main](emberjs-template/samples/sample13.cshtml)]

함수는 템플릿 폴더에 있는 템플릿 파일의 모든 렌더링 인수 없이 호출 합니다. 또한 하위 폴더 또는 특정 서식 파일을 지정할 수 있습니다.

때 **디버그** 은 **false** web.config에서 응용 프로그램 번들 항목 "~/bundles/templates"를 포함 합니다. 이 번들 항목 핸들 컴파일러 라이브러리를 사용 하 여 BundleConfig.cs에 추가 됩니다.

[!code-csharp[Main](emberjs-template/samples/sample14.cs)]
