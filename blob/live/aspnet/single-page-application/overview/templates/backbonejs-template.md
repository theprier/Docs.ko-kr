---
uid: single-page-application/overview/templates/backbonejs-template
title: "Backbone 템플릿 | Microsoft Docs"
author: madskristensen
description: "Backbone.js SPA 서식 파일"
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/04/2013
ms.topic: article
ms.assetid: 00aca413-f067-4108-9bd1-cf21e64a2646
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /single-page-application/overview/templates/backbonejs-template
msc.type: authoredcontent
ms.openlocfilehash: 3b8eabd3cefcb96dc40bbf6cc6e3ee81accb0d7c
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="backbone-template"></a><span data-ttu-id="591e5-103">Backbone 서식 파일</span><span class="sxs-lookup"><span data-stu-id="591e5-103">Backbone Template</span></span>
====================
<span data-ttu-id="591e5-104">여 [Kristensen Mads](https://github.com/madskristensen)</span><span class="sxs-lookup"><span data-stu-id="591e5-104">by [Mads Kristensen](https://github.com/madskristensen)</span></span>

> <span data-ttu-id="591e5-105">Backbone SPA 템플릿 Kazi Manzur Rashid에 의해 작성 되었으므로</span><span class="sxs-lookup"><span data-stu-id="591e5-105">The Backbone SPA Template was written by Kazi Manzur Rashid</span></span>
> 
> [<span data-ttu-id="591e5-106">Backbone.js SPA 템플릿 다운로드</span><span class="sxs-lookup"><span data-stu-id="591e5-106">Download the Backbone.js SPA Template</span></span>](https://go.microsoft.com/fwlink/?LinkId=293631)


<span data-ttu-id="591e5-107">Backbone.js SPA 템플릿을 신속 하 게 사용 하 여 대화형 클라이언트 쪽 웹 앱 작성을 시작 하기 위한 디자인 [Backbone.js 합니다.](http://backbonejs.org/)</span><span class="sxs-lookup"><span data-stu-id="591e5-107">The Backbone.js SPA template is designed to get you started quickly building interactive client-side web apps using [Backbone.js.](http://backbonejs.org/)</span></span>

<span data-ttu-id="591e5-108">템플릿은 ASP.NET MVC에서 Backbone.js 응용 프로그램을 개발 하기 위한 초기 구조를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-108">The template provides an initial skeleton for developing a Backbone.js application in ASP.NET MVC.</span></span> <span data-ttu-id="591e5-109">즉시 사용자 등록, 로그인, 암호 다시 설정 및 사용자에 게 기본 전자 메일 템플릿으로 확인을 포함 한 기본 사용자 로그인 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-109">Out of the box it provides basic user login functionality, including user sign-up, sign-in, password reset, and user confirmation with basic email templates.</span></span>

<span data-ttu-id="591e5-110">요구 사항:</span><span class="sxs-lookup"><span data-stu-id="591e5-110">Requirements:</span></span>

- [<span data-ttu-id="591e5-111">ASP.NET 및 웹 도구 2012.2 업데이트</span><span class="sxs-lookup"><span data-stu-id="591e5-111">ASP.NET and Web Tools 2012.2 update</span></span>](https://go.microsoft.com/fwlink/?LinkId=282650)

## <a name="create-a-backbone-template-project"></a><span data-ttu-id="591e5-112">Backbone 템플릿 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="591e5-112">Create a Backbone Template Project</span></span>

<span data-ttu-id="591e5-113">다운로드 하 고 위의 다운로드 단추를 클릭 하 여 서식 파일을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-113">Download and install the template by clicking the Download button above.</span></span> <span data-ttu-id="591e5-114">서식 파일은 확장 VSIX (Visual Studio) 파일로 패키지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-114">The template is packaged as a Visual Studio Extension (VSIX) file.</span></span> <span data-ttu-id="591e5-115">Visual Studio를 다시 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-115">You might need to restart Visual Studio.</span></span>

<span data-ttu-id="591e5-116">에 **템플릿** 창 선택 **설치 된 템플릿** 확장는 **Visual C#** 노드.</span><span class="sxs-lookup"><span data-stu-id="591e5-116">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="591e5-117">아래 **Visual C#**선택, **웹**합니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-117">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="591e5-118">프로젝트 템플릿 목록에서 선택 **ASP.NET MVC 4 웹 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-118">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="591e5-119">프로젝트 이름을 지정 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-119">Name the project and click **OK**.</span></span>

![](backbonejs-template/_static/image1.png)

<span data-ttu-id="591e5-120">에 **새 프로젝트** Backbone.js SPA 프로젝트 마법사, 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-120">In the **New Project** wizard, select Backbone.js SPA Project.</span></span>

![](backbonejs-template/_static/image2.png)

<span data-ttu-id="591e5-121">빌드하고 디버깅 하지 않고 응용 프로그램을 실행 하려면 Ctrl + f 5를 누르거나 f5 키를 눌러 디버깅이 설정 된 상태로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-121">Press Ctrl-F5 to build and run the application without debugging, or press F5 to run with debugging.</span></span>

![](backbonejs-template/_static/image3.png)

<span data-ttu-id="591e5-122">로그인 페이지 "내 계정"을 클릭 하면 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-122">Clicking "My Account" brings up the login page:</span></span>

![](backbonejs-template/_static/image4.png)

## <a name="walkthrough-client-code"></a><span data-ttu-id="591e5-123">연습: 클라이언트 코드</span><span class="sxs-lookup"><span data-stu-id="591e5-123">Walkthrough: Client Code</span></span>

<span data-ttu-id="591e5-124">클라이언트 쪽으로 시작 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-124">Let's starts with the client side.</span></span> <span data-ttu-id="591e5-125">클라이언트 응용 프로그램 스크립트 ~/Scripts/application 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-125">The client application scripts are located in the ~/Scripts/application folder.</span></span> <span data-ttu-id="591e5-126">응용 프로그램은 작성 된 [TypeScript](http://www.typescriptlang.org/) (.ts 파일) (.js 파일) JavaScript로 컴파일되는입니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-126">The application is written in [TypeScript](http://www.typescriptlang.org/) (.ts files) which are compiled into JavaScript (.js files).</span></span>

<span data-ttu-id="591e5-127">**응용 프로그램**</span><span class="sxs-lookup"><span data-stu-id="591e5-127">**Application**</span></span>

<span data-ttu-id="591e5-128">`Application`application.ts에 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-128">`Application` is defined in application.ts.</span></span> <span data-ttu-id="591e5-129">이 개체는 응용 프로그램을 초기화 하 고 역할을 루트 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-129">This object initializes the application and acts as the root namespace.</span></span> <span data-ttu-id="591e5-130">사용자 로그인 여부와 같은 응용 프로그램에서 공유 되는 구성 및 상태 정보를 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-130">It maintains configuration and state information that is shared across the application, such as whether the user is signed in.</span></span>

<span data-ttu-id="591e5-131">`application.start` 메서드가 모달 뷰가 생성 되 고 사용자 로그인 등의 응용 프로그램 수준 이벤트에 대 한 이벤트 처리기를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-131">The `application.start` method creates the modal views and attaches event handlers for application-level events, such as user sign-in.</span></span> <span data-ttu-id="591e5-132">다음으로 기본 라우터 만들고 모든 클라이언트 쪽 URL 지정 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-132">Next, it creates the default router and checks whether any client-side URL is specified.</span></span> <span data-ttu-id="591e5-133">기본 url를 리디렉션합니다. 그렇지 않은 경우 (#! /).</span><span class="sxs-lookup"><span data-stu-id="591e5-133">If not, it redirects to the default url (#!/).</span></span>

<span data-ttu-id="591e5-134">**이벤트**</span><span class="sxs-lookup"><span data-stu-id="591e5-134">**Events**</span></span>

<span data-ttu-id="591e5-135">이벤트는 구성 요소를 결합 된 느슨하게 개발 하는 경우에 항상 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-135">Events are always important when developing loosely coupled components.</span></span> <span data-ttu-id="591e5-136">응용 프로그램 사용자 작업에 대 한 응답으로 여러 작업을 수행 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-136">Applications often perform multiple operations in response to a user action.</span></span> <span data-ttu-id="591e5-137">Backbone 모델, 컬렉션 및 보기와 같은 구성 요소와 기본 제공 이벤트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-137">Backbone provides built-in events with components such as Model, Collection, and View.</span></span> <span data-ttu-id="591e5-138">이러한 구성 요소 간의 상호 종속성을 만드는 대신 템플릿을 사용 하 여 "pub/sub" 모델:는 `events` events.ts에 정의 된 개체를 게시 하 고 응용 프로그램 이벤트를 구독에 대 한 이벤트 허브 역할도 합니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-138">Instead of creating inter-dependencies among these components, the template uses a "pub/sub" model: The `events` object, defined in events.ts, acts as an event hub for publishing and subscribing to application events.</span></span> <span data-ttu-id="591e5-139">`events` 개체는 singleton입니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-139">The `events` object is a singleton.</span></span> <span data-ttu-id="591e5-140">다음 코드에는 이벤트를 구독 하 고 다음 이벤트가 발생 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-140">The following code shows how to subscribe to an event and then trigger the event:</span></span>

[!code-csharp[Main](backbonejs-template/samples/sample1.cs)]

<span data-ttu-id="591e5-141">**라우터**</span><span class="sxs-lookup"><span data-stu-id="591e5-141">**Router**</span></span>

<span data-ttu-id="591e5-142">Backbone.js, 라우터 라우팅 클라이언트 쪽 페이지 및 동작 및 이벤트에 연결 하는 메서드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-142">In Backbone.js, a router provides methods for routing client-side pages and connecting them to actions and events.</span></span> <span data-ttu-id="591e5-143">서식 파일 router.ts에는 단일 라우터를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-143">The template defines a single router, in router.ts.</span></span> <span data-ttu-id="591e5-144">라우터 activable 뷰를 만들고이 보기를 전환할 때 상태를 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-144">The router creates the activable views and maintains the state when switching views.</span></span> <span data-ttu-id="591e5-145">(Activable 뷰 다음 섹션에 설명 되어 있습니다.) 처음에 프로젝트에는 두 개의 더미 뷰가 가정 및에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-145">(Activable views are described in the next section.) Initially, the project has two dummy views, Home and About.</span></span> <span data-ttu-id="591e5-146">경로 알 수 없는 경우 표시 되는 NotFound 보기를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-146">It also has a NotFound view, which is displayed if the route is not known.</span></span>

<span data-ttu-id="591e5-147">**뷰**</span><span class="sxs-lookup"><span data-stu-id="591e5-147">**Views**</span></span>

<span data-ttu-id="591e5-148">~/Scripts/application/뷰는 뷰에 정의 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-148">The views are defined in ~/Scripts/application/views.</span></span> <span data-ttu-id="591e5-149">보기, activable 뷰 및 모달 대화 뷰는 다음과 같은 두 종류가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-149">There are two kinds of views, activable views and modal dialog views.</span></span> <span data-ttu-id="591e5-150">Activable 뷰는 라우터에 의해 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-150">Activable views are invoked by the router.</span></span> <span data-ttu-id="591e5-151">Activable 보기 표시 될 때 다른 activable 보기에서는 모두 비활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-151">When an activable view is shown, all other activable views become inactive.</span></span> <span data-ttu-id="591e5-152">Activable 뷰를 만들려면 사용 하 여 뷰를 확장의 `Activable` 개체:</span><span class="sxs-lookup"><span data-stu-id="591e5-152">To create an activable view, extend the view with the `Activable` object:</span></span>

[!code-javascript[Main](backbonejs-template/samples/sample2.js)]

<span data-ttu-id="591e5-153">사용한 확장 `Activable` 으로 보기에 두 개의 새 메서드 추가 `activate` 및 `deactivate`합니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-153">Extending with `Activable` adds two new methods to the view, `activate` and `deactivate`.</span></span> <span data-ttu-id="591e5-154">라우터를 활성화 및 비활성화할 보기 이러한 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-154">The router calls these methods to activate and deactive the view.</span></span>

<span data-ttu-id="591e5-155">모달 뷰가으로 구현 된 [Twitter 부트스트랩](http://twitter.github.com/bootstrap/) 모달 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="591e5-155">Modal views are implemented as [Twitter Bootstrap](http://twitter.github.com/bootstrap/) modal dialogs.</span></span> <span data-ttu-id="591e5-156">`Membership` 및 `Profile` 뷰는 모달 뷰가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-156">The `Membership` and `Profile` views are modal views.</span></span> <span data-ttu-id="591e5-157">모델 뷰는 모든 응용 프로그램 이벤트에서 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-157">Model views can be invoked by any application events.</span></span> <span data-ttu-id="591e5-158">예를 들어는 `Navigation` 보기, "내 계정" 링크를 클릭 하면 표시는 `Membership` 보기 또는 `Profile` 사용자 로그인 여부에 따라 보기.</span><span class="sxs-lookup"><span data-stu-id="591e5-158">For example, in the `Navigation` view, clicking the "My Account" link shows either the `Membership` view or the `Profile` view, depending on whether the user is logged in.</span></span> <span data-ttu-id="591e5-159">`Navigation` 연결 클릭 이벤트 처리기에 있는 모든 자식 요소는 `data-command` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-159">The `Navigation` attaches click event handlers to any child elements that have the `data-command` attribute.</span></span> <span data-ttu-id="591e5-160">HTML 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-160">Here is the HTML markup:</span></span>

[!code-html[Main](backbonejs-template/samples/sample3.html)]

<span data-ttu-id="591e5-161">이벤트를 후크 navigation.ts의 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-161">Here is the code in navigation.ts to hook up the events:</span></span>

[!code-csharp[Main](backbonejs-template/samples/sample4.cs)]

<span data-ttu-id="591e5-162">**모델**</span><span class="sxs-lookup"><span data-stu-id="591e5-162">**Models**</span></span>

<span data-ttu-id="591e5-163">모델은 ~/Scripts/application/모델에 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-163">The models are defined in ~/Scripts/application/models.</span></span> <span data-ttu-id="591e5-164">모든 모델은 다음 세 가지 기본적인 작업: 기본 속성, 유효성 검사 규칙 및 서버 쪽 끝 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-164">The models all have three basic things: default attributes, validation rules, and a server-side end point.</span></span> <span data-ttu-id="591e5-165">일반적인 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-165">Here is a typical example:</span></span>

[!code-javascript[Main](backbonejs-template/samples/sample5.js)]

<span data-ttu-id="591e5-166">**플러그 인**</span><span class="sxs-lookup"><span data-stu-id="591e5-166">**Plug-ins**</span></span>

<span data-ttu-id="591e5-167">~/Scripts/application/lib 폴더는 몇 가지 유용한 jQuery 플러그 인을 포함합니다. Form.ts 파일 양식 데이터로 작업 하기 위한 플러그 인을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-167">The ~/Scripts/application/lib folder contains a few handy jQuery plug-ins. The form.ts file defines a plug-in for working with form data.</span></span> <span data-ttu-id="591e5-168">종종 serialize 또는 deserialize 양식 데이터 및 모델 유효성 검사 오류를 표시 해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-168">Often you need to serialize or deserialize form data and show any model validation errors.</span></span> <span data-ttu-id="591e5-169">플러그 인 form.ts에 메서드가 같은 `serializeFields`, `deserializeFields`, 및 `showFieldErrors`합니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-169">The form.ts plug-in has methods such as `serializeFields`, `deserializeFields`, and `showFieldErrors`.</span></span> <span data-ttu-id="591e5-170">다음 예에서는 모델에 폼을 serialize 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-170">The following example shows how to serialize a form to a model.</span></span>

[!code-javascript[Main](backbonejs-template/samples/sample6.js)]

<span data-ttu-id="591e5-171">플러그 인 flashbar.ts 사용자에 게 다양 한 종류의 피드백 메시지를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-171">The flashbar.ts plug-in gives various kinds of feedback messages to the user.</span></span> <span data-ttu-id="591e5-172">메서드는 `$.showSuccessbar`, `$.showErrorbar` 및 `$.showInfobar`합니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-172">The methods are `$.showSuccessbar`, `$.showErrorbar` and `$.showInfobar`.</span></span> <span data-ttu-id="591e5-173">내부적으로 사용 하 여 Twitter 부트스트랩 경고 애니메이션된 원활 하 게 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-173">Behind the scenes, it uses Twitter Bootstrap alerts to show nicely animated messages.</span></span>

<span data-ttu-id="591e5-174">플러그 인 confirm.ts 브라우저의 대체 API 어느 정도 차이가 있지만 대화 상자에서 확인:</span><span class="sxs-lookup"><span data-stu-id="591e5-174">The confirm.ts plug-in replaces the browser's confirm dialog, although the API is somewhat different:</span></span>

[!code-javascript[Main](backbonejs-template/samples/sample7.js)]

## <a name="walkthrough-server-code"></a><span data-ttu-id="591e5-175">연습: 서버 코드</span><span class="sxs-lookup"><span data-stu-id="591e5-175">Walkthrough: Server Code</span></span>

<span data-ttu-id="591e5-176">이제 서버 쪽에서 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-176">Now let's look at the server side.</span></span>

<span data-ttu-id="591e5-177">**컨트롤러**</span><span class="sxs-lookup"><span data-stu-id="591e5-177">**Controllers**</span></span>

<span data-ttu-id="591e5-178">단일 페이지 응용 프로그램 서버가 사용자 인터페이스에서 작은 역할만 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-178">In a single page application, the server plays only a small role in the user interface.</span></span> <span data-ttu-id="591e5-179">일반적으로 서버 초기 페이지를 렌더링 하 고 보내고 JSON 데이터를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-179">Typically, the server renders the initial page and then sends and receives JSON data.</span></span>

<span data-ttu-id="591e5-180">서식 파일에 두 명의 MVC 컨트롤러: `HomeController` 초기 페이지를 렌더링 하 고 `SupportsController` 새 사용자 계정을 확인 하 고 암호 다시 설정 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-180">The template has two MVC controllers: `HomeController` renders the initial page, and `SupportsController` is used to confirm new user accounts and reset passwords.</span></span> <span data-ttu-id="591e5-181">서식 파일에서 다른 모든 컨트롤러는 송신 및 JSON 데이터를 수신 하는 ASP.NET Web API 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-181">All other controllers in the template are ASP.NET Web API controllers, which send and receive JSON data.</span></span> <span data-ttu-id="591e5-182">기본적으로는 컨트롤러 사용 하 여 새 `WebSecurity` 사용자 관련 작업을 수행 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-182">By default, the controllers use the new `WebSecurity` class to perform user-related tasks.</span></span> <span data-ttu-id="591e5-183">그러나 이러한 작업에 대 한 대리자에 전달할 수 있는 선택적 생성자도 가집니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-183">However, they also have optional constructors that let you pass in delegates for these tasks.</span></span> <span data-ttu-id="591e5-184">더 쉽게 테스트할 수 있습니다.이 고 바꿀 수 있습니다 `WebSecurity` IoC 컨테이너를 사용 하 여 다른 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-184">This makes testing easier, and lets you replace `WebSecurity` with something else, by using an IoC Container.</span></span> <span data-ttu-id="591e5-185">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-185">Here is an example:</span></span>

[!code-csharp[Main](backbonejs-template/samples/sample8.cs)]

## <a name="views"></a><span data-ttu-id="591e5-186">보기</span><span class="sxs-lookup"><span data-stu-id="591e5-186">Views</span></span>

<span data-ttu-id="591e5-187">뷰는 모듈식 하도록 설계 되었습니다: 페이지의 각 부분에 자체 전용된 뷰가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-187">The views are designed to be modular: Each section of a page has its own dedicated view.</span></span> <span data-ttu-id="591e5-188">이 단일 페이지 응용 프로그램에서 모든 해당 컨트롤러를 갖지 않는 뷰를 포함 하도록 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-188">In a single page application, it is common to include views that do not have any corresponding controller.</span></span> <span data-ttu-id="591e5-189">호출 하 여 뷰를 포함할 수 있습니다 `@Html.Partial('myView')`, 번거로운이 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-189">You can include a view by calling `@Html.Partial('myView')`, but this gets tedious.</span></span> <span data-ttu-id="591e5-190">간단 하 게 하려면이 템플릿에 도우미 메서드를 정의 `IncludeClientViews`, 모든 지정된 된 폴더의 뷰를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-190">To make this easier, the template defines a helper method, `IncludeClientViews`, that renders all of the views in a specified folder:</span></span>

[!code-cshtml[Main](backbonejs-template/samples/sample9.cshtml)]

<span data-ttu-id="591e5-191">폴더 이름을 지정 하지 않으면 기본 폴더 이름에 "ClientViews" 됩니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-191">If the folder name is not specified, the default folder name is "ClientViews".</span></span> <span data-ttu-id="591e5-192">클라이언트 보기 부분 뷰를 사용 하면 이름에 밑줄 문자를 사용 하 여 부분 뷰 (예를 들어 `_SignUp`).</span><span class="sxs-lookup"><span data-stu-id="591e5-192">If your client view also uses partial views, name the partial view with an underscore character (for example, `_SignUp`).</span></span> <span data-ttu-id="591e5-193">`IncludeClientViews` 메서드 이름이 밑줄로 시작 하는 모든 뷰는 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-193">The `IncludeClientViews` method excludes any views whose name starts with an underscore.</span></span> <span data-ttu-id="591e5-194">클라이언트 보기에 부분 뷰를 포함 하려면 호출 `Html.ClientView('SignUp')` 대신 `Html.Partial('_SignUp')`합니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-194">To include a partial view in the client view, call `Html.ClientView('SignUp')` instead of `Html.Partial('_SignUp')`.</span></span>

<span data-ttu-id="591e5-195">**메일을 보내는 중**</span><span class="sxs-lookup"><span data-stu-id="591e5-195">**Sending Email**</span></span>

<span data-ttu-id="591e5-196">템플릿을 사용 하 여 전자 메일을 보내려면 [Postal](http://aboutcode.net/postal)합니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-196">To send email, the template uses [Postal](http://aboutcode.net/postal).</span></span> <span data-ttu-id="591e5-197">사용 하 여 코드의 나머지 부분과에서 Postal 추출 하는 반면는 `IMailer` 인터페이스, 다른 구현으로 쉽게 바꿀 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-197">However, Postal is abstracted from the rest of the code with the `IMailer` interface, so you can easily replace it with another implementation.</span></span> <span data-ttu-id="591e5-198">전자 메일 템플릿은 뷰/메일 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-198">The email templates are located in the Views/Emails folder.</span></span> <span data-ttu-id="591e5-199">web.config 파일에 보낸 사람의 전자 메일 주소가 지정 되어는 `sender.email` 의 키에서 **appSettings** 섹션.</span><span class="sxs-lookup"><span data-stu-id="591e5-199">The sender's email address is specified in the web.config file, in the `sender.email` key of the **appSettings** section.</span></span> <span data-ttu-id="591e5-200">또한, `debug="true"` 응용 프로그램 web.config에서 개발 속도 향상을 위한 사용자 전자 메일 확인이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-200">Also, when `debug="true"` in web.config, the application does not require user email confirmation, to speed up development.</span></span>

## <a name="github"></a><span data-ttu-id="591e5-201">GitHub</span><span class="sxs-lookup"><span data-stu-id="591e5-201">GitHub</span></span>

<span data-ttu-id="591e5-202">Backbone.js SPA 서식 파일을 찾을 수도 [GitHub](https://github.com/kazimanzurrashid/AspNetMvcBackboneJsSpa)합니다.</span><span class="sxs-lookup"><span data-stu-id="591e5-202">You can also find the Backbone.js SPA template on [GitHub](https://github.com/kazimanzurrashid/AspNetMvcBackboneJsSpa).</span></span>
