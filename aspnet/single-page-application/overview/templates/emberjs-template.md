---
uid: single-page-application/overview/templates/emberjs-template
title: EmberJS 템플릿 | Microsoft Docs
author: xqiu
description: EmberJS 템플릿
ms.author: riande
ms.date: 01/30/2013
ms.assetid: 04d5f142-5f62-494a-b5ea-4f3d068d34cb
msc.legacyurl: /single-page-application/overview/templates/emberjs-template
msc.type: authoredcontent
ms.openlocfilehash: fbc3b1d299ace27d38d895e42b8e3bb3b51b36f8
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41838182"
---
<a name="emberjs-template"></a><span data-ttu-id="88563-103">EmberJS 템플릿</span><span class="sxs-lookup"><span data-stu-id="88563-103">EmberJS template</span></span>
====================
<span data-ttu-id="88563-104">[Xinyang Qiu](https://github.com/xqiu)</span><span class="sxs-lookup"><span data-stu-id="88563-104">by [Xinyang Qiu](https://github.com/xqiu)</span></span>

> <span data-ttu-id="88563-105">EmberJS MVC 템플릿 Nathan Totten, Thiago Santos Xinyang Qiu로 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88563-105">The EmberJS MVC Template is written by Nathan Totten, Thiago Santos, and Xinyang Qiu.</span></span>
> 
> [<span data-ttu-id="88563-106">EmberJS MVC 템플릿 다운로드</span><span class="sxs-lookup"><span data-stu-id="88563-106">Download the EmberJS MVC Template</span></span>](https://go.microsoft.com/fwlink/?LinkId=282647)


<span data-ttu-id="88563-107">EmberJS SPA 템플릿은 신속 하 게 EmberJS를 사용 하 여 대화형 클라이언트 쪽 웹 앱을 빌드하기 시작할 수 있도록 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="88563-107">The EmberJS SPA template is designed to get you started quickly building interactive client-side web apps using EmberJS.</span></span>

<span data-ttu-id="88563-108">"단일 페이지 응용 프로그램" (SPA)은 하나의 HTML 페이지를 로드 하 고 그런 다음 새 페이지를 로드 하는 대신 페이지를 동적으로 업데이트 하는 웹 응용 프로그램에 대 한 일반 용어입니다.</span><span class="sxs-lookup"><span data-stu-id="88563-108">"Single-page application" (SPA) is the general term for a web application that loads a single HTML page and then updates the page dynamically, instead of loading new pages.</span></span> <span data-ttu-id="88563-109">초기 페이지 로드 후 SPA AJAX 요청을 통해 서버를 사용 하 여 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-109">After the initial page load, the SPA talks with the server through AJAX requests.</span></span>

![](emberjs-template/_static/image1.png)

<span data-ttu-id="88563-110">AJAX 새 nothing 하지만 현재 있다는 쉽게 구축 하 고 대형 정교한 SPA 응용 프로그램을 관리 하는 JavaScript 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="88563-110">AJAX is nothing new, but today there are JavaScript frameworks that make it easier to build and maintain a large sophisticated SPA application.</span></span> <span data-ttu-id="88563-111">또한 html5 및 CSS3는 쉽게 다양 한 Ui를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="88563-111">Also, HTML 5 and CSS3 are making it easier to create rich UIs.</span></span>

<span data-ttu-id="88563-112">EmberJS SPA 템플릿을 사용 하는 [Ember](http://emberjs.com/) AJAX 요청에서 페이지 업데이트를 처리 하는 JavaScript 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="88563-112">The EmberJS SPA Template uses the [Ember](http://emberjs.com/) JavaScript library to handle page updates from AJAX requests.</span></span> <span data-ttu-id="88563-113">Ember.js는 데이터 바인딩의 사용 하 여 최신 데이터를 사용 하 여 페이지를 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-113">Ember.js uses data binding to synchronize the page with the latest data.</span></span> <span data-ttu-id="88563-114">JSON 데이터를 안내 하 고 DOM을 업데이트 하는 코드를 작성할 필요가 이런 방식으로</span><span class="sxs-lookup"><span data-stu-id="88563-114">That way, you don't have to write any of the code that walks through the JSON data and updates the DOM.</span></span> <span data-ttu-id="88563-115">대신, Ember.js 데이터를 표시 하는 방법을 알려 주는 HTML의 선언적 특성을 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88563-115">Instead, you put declarative attributes in the HTML that tell Ember.js how to present the data.</span></span>

<span data-ttu-id="88563-116">서버 쪽에서 EmberJS 템플릿은 거의 동일 합니다 [KnockoutJS SPA 템플릿](../introduction/knockoutjs-template.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-116">On the server side, the EmberJS template is almost identical to the [KnockoutJS SPA template](../introduction/knockoutjs-template.md).</span></span> <span data-ttu-id="88563-117">ASP.NET MVC를 사용 하 여 HTML 문서 및 클라이언트에서 AJAX 요청을 처리 하는 ASP.NET Web API를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-117">It uses ASP.NET MVC to serve HTML documents, and ASP.NET Web API to handle AJAX requests from the client.</span></span> <span data-ttu-id="88563-118">서식 파일의 이러한 측면에 대 한 자세한 내용은 참조는 [KnockoutJS 템플릿](../introduction/knockoutjs-template.md) 설명서.</span><span class="sxs-lookup"><span data-stu-id="88563-118">For more information about those aspects of the template, refer to the [KnockoutJS template](../introduction/knockoutjs-template.md) documentation.</span></span> <span data-ttu-id="88563-119">이 항목에서는 Knockout 템플릿 및 EmberJS 템플릿 간의 차이점에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="88563-119">This topic focuses on the differences between the Knockout template and the EmberJS template.</span></span>

## <a name="create-an-emberjs-spa-template-project"></a><span data-ttu-id="88563-120">EmberJS SPA 템플릿 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="88563-120">Create an EmberJS SPA Template Project</span></span>

<span data-ttu-id="88563-121">다운로드 하 고 위의 다운로드 단추를 클릭 하 여 템플릿을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-121">Download and install the template by clicking the Download button above.</span></span> <span data-ttu-id="88563-122">Visual Studio를 다시 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-122">You might need to restart Visual Studio.</span></span>

<span data-ttu-id="88563-123">에 **템플릿** 창 **설치 된 템플릿** 확장 하 고는 **Visual C#** 노드.</span><span class="sxs-lookup"><span data-stu-id="88563-123">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="88563-124">아래 **Visual C#** 를 선택 **웹**합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-124">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="88563-125">프로젝트 템플릿 목록에서 선택 **ASP.NET MVC 4 웹 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-125">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="88563-126">프로젝트 이름을 지정 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-126">Name the project and click **OK**.</span></span>

![](emberjs-template/_static/image2.png)

<span data-ttu-id="88563-127">에 **새 프로젝트** 마법사 **Ember.js SPA 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-127">In the **New Project** wizard, select **Ember.js SPA Project**.</span></span>

![](emberjs-template/_static/image4.png)

## <a name="emberjs-spa-template-overview"></a><span data-ttu-id="88563-128">EmberJS SPA 템플릿 개요</span><span class="sxs-lookup"><span data-stu-id="88563-128">EmberJS SPA Template Overview</span></span>

<span data-ttu-id="88563-129">EmberJS 템플릿 jQuery, Ember.js, 부드러운, 대화형 UI를 만들기 위해 Handlebars.js의 조합을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-129">The EmberJS template uses a combination of jQuery, Ember.js, Handlebars.js to create a smooth, interactive UI.</span></span>

<span data-ttu-id="88563-130">Ember.js는 클라이언트 쪽 MVC 패턴을 사용 하는 JavaScript 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="88563-130">Ember.js is a JavaScript library that uses a client-side MVC pattern.</span></span>

- <span data-ttu-id="88563-131">A *템플릿*, Handlebars 템플릿 언어로 작성 된 응용 프로그램 사용자 인터페이스를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-131">A *template*, written in the Handlebars templating language, describes the application user interface.</span></span> <span data-ttu-id="88563-132">릴리스 모드에서의 [Handlebars 컴파일러](https://github.com/Myslik/csharp-ember-handlebars) 번들 handlebars 템플릿을 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88563-132">In release mode, the [Handlebars compiler](https://github.com/Myslik/csharp-ember-handlebars) is used to bundle and compile the handlebars template.</span></span>
- <span data-ttu-id="88563-133">A *모델* (할 일 목록 및 할 일 항목) 서버에서 가져온 응용 프로그램 데이터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-133">A *model* stores the application data that it gets from the server (ToDo lists and ToDo items).</span></span>
- <span data-ttu-id="88563-134">A *컨트롤러* 응용 프로그램 상태를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-134">A *controller* stores application state.</span></span> <span data-ttu-id="88563-135">컨트롤러는 종종 해당 템플릿에 모델 데이터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-135">Controllers often present model data to the corresponding templates.</span></span>
- <span data-ttu-id="88563-136">A *보기* 응용 프로그램에서 기본 이벤트를 변환 하 고 컨트롤러에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-136">A *view* translates primitive events from the application and passes these to the controller.</span></span>
- <span data-ttu-id="88563-137">A *라우터* Url 템플릿과 동기화 상태로 유지 되는 응용 프로그램 상태를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-137">A *router* manages application state, keeping URLs and templates in sync.</span></span>

<span data-ttu-id="88563-138">또한 JSON 개체 (RESTful API를 통해 서버에서 가져옴) 및 클라이언트 모델을 동기화 하는 Ember 데이터 라이브러리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88563-138">In addition, the Ember Data library can be used to synchronize JSON objects (obtained from the server through a RESTful API) and the client models.</span></span>

<span data-ttu-id="88563-139">EmberJS SPA 템플릿 8 레이어로 스크립트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-139">The EmberJS SPA template organizes the scripts into eight layers:</span></span>

- <span data-ttu-id="88563-140">webapi\_adapter.js, webapi\_serializer.js: ASP.NET Web API를 사용 하려면 Ember 데이터 라이브러리를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-140">webapi\_adapter.js, webapi\_serializer.js: Extends the Ember Data library to work with ASP.NET Web API.</span></span>
- <span data-ttu-id="88563-141">Scripts/helpers.js: 새 Ember Handlebars 도우미를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-141">Scripts/helpers.js: Defines new Ember Handlebars helpers.</span></span>
- <span data-ttu-id="88563-142">Scripts/app.js: 앱을 만들고 어댑터 및 serializer를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-142">Scripts/app.js: Creates the app and configures the adapter and serializer.</span></span>
- <span data-ttu-id="88563-143">스크립트/app/모델/\*.js: 모델을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-143">Scripts/app/models/\*.js: Defines the models.</span></span>
- <span data-ttu-id="88563-144">스크립트/app/뷰/\*.js: 뷰를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-144">Scripts/app/views/\*.js: Defines the views.</span></span>
- <span data-ttu-id="88563-145">스크립트/app/컨트롤러/\*.js: 컨트롤러를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-145">Scripts/app/controllers/\*.js: Defines the controllers.</span></span>
- <span data-ttu-id="88563-146">스크립트/app/routes, Scripts/app/router.js: 경로 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-146">Scripts/app/routes, Scripts/app/router.js: Defines the routes.</span></span>
- <span data-ttu-id="88563-147">템플릿 /\*.hbs: handlebars 템플릿을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-147">Templates/\*.hbs: Defines the handlebars templates.</span></span>

<span data-ttu-id="88563-148">자세한 세부 정보에서 이러한 스크립트 중 일부에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="88563-148">Let's look at some of these scripts in more detail.</span></span>

## <a name="models"></a><span data-ttu-id="88563-149">모델</span><span class="sxs-lookup"><span data-stu-id="88563-149">Models</span></span>

<span data-ttu-id="88563-150">모델은 스크립트/app/models 폴더에 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88563-150">The models are defined in the Scripts/app/models folder.</span></span> <span data-ttu-id="88563-151">모델 파일이 두 개: todoItem.js 및 todoList.js 합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-151">There are two model files: todoItem.js and todoList.js.</span></span>

<span data-ttu-id="88563-152">**todo.model.js** 할 일 목록에 대 한 클라이언트 쪽 (브라우저) 모델을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-152">**todo.model.js** defines the client-side (browser) models for the to-do lists.</span></span> <span data-ttu-id="88563-153">두 모델 클래스: todoItem 및 todoList 합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-153">There are two model classes: todoItem and todoList.</span></span> <span data-ttu-id="88563-154">Ember와, 모델에는 DS의 서브 클래스입니다. 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="88563-154">In Ember, models are subclasses of DS.Model.</span></span> <span data-ttu-id="88563-155">모델 속성에 특성을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88563-155">A model can have properties with attributes:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample1.js)]

<span data-ttu-id="88563-156">모델은 다른 모델에 관계를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88563-156">Models can define relationships to other models:</span></span>

[!code-css[Main](emberjs-template/samples/sample2.css)]

<span data-ttu-id="88563-157">모델을 다른 속성에 바인딩하는 속성 계산 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88563-157">Models can have computed properties that bind to other properties:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample3.js)]

<span data-ttu-id="88563-158">모델에는 관찰 된 속성이 변경 될 때 호출 되는 관찰자 함수를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88563-158">Models can have observer functions, which are invoked when an observed property changes:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample4.js)]

## <a name="views"></a><span data-ttu-id="88563-159">보기</span><span class="sxs-lookup"><span data-stu-id="88563-159">Views</span></span>

<span data-ttu-id="88563-160">뷰는 스크립트/app/views 폴더에 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88563-160">The views are defined in the Scripts/app/views folder.</span></span> <span data-ttu-id="88563-161">뷰는 응용 프로그램 UI에서에서 이벤트를 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-161">A view translates events from the application UI.</span></span> <span data-ttu-id="88563-162">이벤트 처리기 다시 컨트롤러 함수를 호출 하거나 단순히 데이터 컨텍스트를 직접 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88563-162">An event handler can call back to controller functions, or simply call the data context directly.</span></span>

<span data-ttu-id="88563-163">예를 들어, 다음 코드는 views/TodoItemEditView.js에서.</span><span class="sxs-lookup"><span data-stu-id="88563-163">For example, the following code is from views/TodoItemEditView.js.</span></span> <span data-ttu-id="88563-164">입력된 텍스트 필드에 대 한 처리 이벤트를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-164">It defines the event handling for an input text field.</span></span>

[!code-javascript[Main](emberjs-template/samples/sample5.js)]

## <a name="controller"></a><span data-ttu-id="88563-165">컨트롤러</span><span class="sxs-lookup"><span data-stu-id="88563-165">Controller</span></span>

<span data-ttu-id="88563-166">컨트롤러는 스크립트/app/controllers 폴더에서 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88563-166">The controllers are defined in the Scripts/app/controllers folder.</span></span> <span data-ttu-id="88563-167">단일 모델을 나타내기 위해 확장 `Ember.ObjectController`:</span><span class="sxs-lookup"><span data-stu-id="88563-167">To represent a single model, extend `Ember.ObjectController`:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample6.js)]

<span data-ttu-id="88563-168">컨트롤러를 확장 하 여 모델의 컬렉션을 나타낼 수도 있습니다 `Ember.ArrayController`합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-168">A controller can also represent a collection of models by extending `Ember.ArrayController`.</span></span> <span data-ttu-id="88563-169">예를 들어 TodoListController 나타내는의 배열 `todoList` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="88563-169">For example, the TodoListController represents an array of `todoList` objects.</span></span> <span data-ttu-id="88563-170">컨트롤러 내림차순 todoList ID를 기준으로 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-170">The controller sorts by todoList ID, in descending order:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample7.js)]

<span data-ttu-id="88563-171">명명 된 함수를 정의 하는 컨트롤러 `addTodoList`, 새 todoList 생성 되 고 배열에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-171">The controller defines a function named `addTodoList`, which creates a new todoList and adds it to the array.</span></span> <span data-ttu-id="88563-172">이 함수는 호출 하는 방법을 보려는 Templates 폴더에 todoListTemplate.html 라는 템플릿 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="88563-172">To see how this function gets called, open the template file named todoListTemplate.html, in the Templates folder.</span></span> <span data-ttu-id="88563-173">다음 템플릿 코드는 단추를 바인딩하는 `addTodoList` 함수:</span><span class="sxs-lookup"><span data-stu-id="88563-173">The following template code binds a button to the `addTodoList` function:</span></span>

[!code-html[Main](emberjs-template/samples/sample8.html)]

<span data-ttu-id="88563-174">컨트롤러도 포함 되어 있습니다를 `error` 오류 메시지를 보유 하는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="88563-174">The controller also contains an `error` property, which holds an error message.</span></span> <span data-ttu-id="88563-175">(또한 todoListTemplate.html)에서 오류 메시지를 표시 하는 템플릿 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="88563-175">Here is the template code to display the error message (also in todoListTemplate.html):</span></span>

[!code-html[Main](emberjs-template/samples/sample9.html)]

## <a name="routes"></a><span data-ttu-id="88563-176">경로</span><span class="sxs-lookup"><span data-stu-id="88563-176">Routes</span></span>

<span data-ttu-id="88563-177">경로 및 응용 프로그램 상태 집합을 표시 하려면 기본 템플릿을 정의 하 고 Url 경로 일치 하는 Router.js:</span><span class="sxs-lookup"><span data-stu-id="88563-177">Router.js defines the routes and the default template to display, sets up application state, and matches URLs to routes:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample10.js)]

<span data-ttu-id="88563-178">TodoListRoute.js는 setupController 함수를 재정의 하 여는 TodoListRoute에 대 한 데이터를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-178">TodoListRoute.js loads data for the TodoListRoute by overriding the setupController function:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample11.js)]

<span data-ttu-id="88563-179">Ember와 Url, 경로 이름, 컨트롤러 및 템플릿을 일치 하도록 명명 규칙을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-179">Ember uses naming conventions to match URLs, route names, controllers, and templates.</span></span> <span data-ttu-id="88563-180">자세한 내용은 [ http://emberjs.com/guides/routing/defining-your-routes/ ](http://emberjs.com/guides/routing/defining-your-routes/) EmberJS 설명서.</span><span class="sxs-lookup"><span data-stu-id="88563-180">For more information, see [http://emberjs.com/guides/routing/defining-your-routes/](http://emberjs.com/guides/routing/defining-your-routes/) at the EmberJS documentation.</span></span>

## <a name="templates"></a><span data-ttu-id="88563-181">템플릿</span><span class="sxs-lookup"><span data-stu-id="88563-181">Templates</span></span>

<span data-ttu-id="88563-182">템플릿 폴더에 4 개의 템플릿이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88563-182">The Templates folder contains four templates:</span></span>

- <span data-ttu-id="88563-183">application.hbs: 응용 프로그램이 시작 될 때 렌더링 되는 기본 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="88563-183">application.hbs: The default template that is rendered when the application is started.</span></span>
- <span data-ttu-id="88563-184">about.hbs: "/ 정보" 경로 대 한 템플릿.</span><span class="sxs-lookup"><span data-stu-id="88563-184">about.hbs: The template for the "/about" route.</span></span>
- <span data-ttu-id="88563-185">index.hbs: 루트에 대 한 템플릿 경로 "/"입니다.</span><span class="sxs-lookup"><span data-stu-id="88563-185">index.hbs: The template for the root "/" route.</span></span>
- <span data-ttu-id="88563-186">todoList.hbs:에 대 한 서식 파일은 "/ todo" 경로.</span><span class="sxs-lookup"><span data-stu-id="88563-186">todoList.hbs: The template for the "/todo" route.</span></span>
- <span data-ttu-id="88563-187">\_navbar.hbs: 템플릿을 탐색 메뉴를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-187">\_navbar.hbs: The template defines the navigation menu.</span></span>

<span data-ttu-id="88563-188">응용 프로그램 템플릿은 마스터 페이지 처럼 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-188">The application template acts like a master page.</span></span> <span data-ttu-id="88563-189">머리글, 바닥글 및 "{{출 선}}" 경로 따라 다른 템플릿을에서 삽입할 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-189">It contains a header, a footer, and an "{{outlet}}" to insert other templates in depending on the route.</span></span> <span data-ttu-id="88563-190">Ember와의 응용 프로그램 템플릿에 대 한 자세한 내용은 참조 하세요. [ http://guides.emberjs.com/v1.10.0/templates/the-application-template// ](http://guides.emberjs.com/v1.10.0/templates/the-application-template/)합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-190">For more information about application templates in Ember, see [http://guides.emberjs.com/v1.10.0/templates/the-application-template//](http://guides.emberjs.com/v1.10.0/templates/the-application-template/).</span></span>

<span data-ttu-id="88563-191">"/ todoList" 템플릿 두 루프 식을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-191">The "/todoList" template contains two loop expressions.</span></span> <span data-ttu-id="88563-192">외부 루프 `{{#each controller}}`, 및 내부 루프는 `{{#each todos}}`합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-192">The outside loop is `{{#each controller}}`, and the inside loop is `{{#each todos}}`.</span></span> <span data-ttu-id="88563-193">다음 코드에서는 기본 제공 `Ember.Checkbox` 보고, 사용자 지정 `App.TodoItemEditView`, 및 사용 하 여 링크를 `deleteTodo` 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-193">The following code shows a built-in `Ember.Checkbox` view, a customized `App.TodoItemEditView`, and a link with a `deleteTodo` action.</span></span>

[!code-html[Main](emberjs-template/samples/sample12.html)]

<span data-ttu-id="88563-194">합니다 `HtmlHelperExtensions` Controllers/HtmlHelperExensions.cs에에서 정의 된 클래스 도우미를 정의 할 때 파일을 캐시 하 고 템플릿 삽입 함수 **디버그** 로 설정 되어 **true** Web.config 파일에서.</span><span class="sxs-lookup"><span data-stu-id="88563-194">The `HtmlHelperExtensions` class, defined in Controllers/HtmlHelperExensions.cs, defines a helper function to cache and insert template files when **debug** is set to **true** in the Web.config file.</span></span> <span data-ttu-id="88563-195">이 함수는 Views/Home/App.cshtml에 정의 된 ASP.NET MVC 뷰 파일에서 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88563-195">This function is called from the ASP.NET MVC view file defined in Views/Home/App.cshtml:</span></span>

[!code-cshtml[Main](emberjs-template/samples/sample13.cshtml)]

<span data-ttu-id="88563-196">함수는 템플릿 폴더에 템플릿 파일의 모든 렌더링 인수 없이 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="88563-196">Called with no arguments, the function renders all of the template files in the Templates folder.</span></span> <span data-ttu-id="88563-197">하위 폴더 또는 특정 템플릿 파일을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88563-197">You can also specify a subfolder or a specific template file.</span></span>

<span data-ttu-id="88563-198">때 **디버그** 됩니다 **false** Web.config에서 응용 프로그램에는 번들 항목 "~/bundles/templates"이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88563-198">When **debug** is **false** in Web.config, the application includes the bundle item "~/bundles/templates".</span></span> <span data-ttu-id="88563-199">이 번들 항목 BundleConfig.cs, Handlebars 컴파일러 라이브러리를 사용 하 여에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88563-199">This bundle item is added in BundleConfig.cs, using the Handlebars compiler library:</span></span>

[!code-csharp[Main](emberjs-template/samples/sample14.cs)]
