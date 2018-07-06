---
uid: single-page-application/overview/templates/breezeangular-template
title: Breeze/Angular 템플릿 | Microsoft Docs
author: madskristensen
description: Breeze/Angular 단일 페이지 응용 프로그램 템플릿
ms.author: aspnetcontent
ms.date: 03/08/2013
ms.assetid: db31e909-563a-4516-aadd-62aa210ac7e4
msc.legacyurl: /single-page-application/overview/templates/breezeangular-template
msc.type: authoredcontent
ms.openlocfilehash: 3799c891625b28312b54ed33628748dcc1b74925
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37811752"
---
<a name="breezeangular-template"></a><span data-ttu-id="a5ed0-103">Breeze/Angular 템플릿</span><span class="sxs-lookup"><span data-stu-id="a5ed0-103">Breeze/Angular template</span></span>
====================
<span data-ttu-id="a5ed0-104">[제작: Mads Kristensen](https://github.com/madskristensen)</span><span class="sxs-lookup"><span data-stu-id="a5ed0-104">by [Mads Kristensen](https://github.com/madskristensen)</span></span>

> <span data-ttu-id="a5ed0-105">Breeze/Angular MVC 템플릿 Ward 벨에 의해 작성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-105">The Breeze/Angular MVC Template was written by Ward Bell</span></span>
> 
> [<span data-ttu-id="a5ed0-106">Breeze/Angular MVC 템플릿 다운로드</span><span class="sxs-lookup"><span data-stu-id="a5ed0-106">Download the Breeze/Angular MVC Template</span></span>](https://go.microsoft.com/fwlink/?LinkId=286437)


<span data-ttu-id="a5ed0-107">[AngularJS](http://angularjs.org) 는 단일 페이지 응용 프로그램 (Spa) 빌드에 대 한 Google에서 오픈 소스 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-107">[AngularJS](http://angularjs.org) is an open source library from Google for building Single Page Applications (SPAs).</span></span> <span data-ttu-id="a5ed0-108">데이터 바인딩, 종속성 주입 및 화면 관리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-108">It offers data binding, dependency injection, and screen management.</span></span> <span data-ttu-id="a5ed0-109">와 함께 [BreezeJS](http://www.breezejs.com/?utm_source=ms-spa), 데이터 모델링 및 데이터 관리에 대 한 다른 오픈 소스 라이브러리가 훌륭한 HTML/JavaScript 클라이언트 앱을 위한 기본적인 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-109">Combine it with [BreezeJS](http://www.breezejs.com/?utm_source=ms-spa), another open source library for data modeling and data management, and you have the essential ingredients for a great HTML/JavaScript client app.</span></span>

<span data-ttu-id="a5ed0-110">Breeze/Angular SPA 템플릿 변형 켜져 합니다 [KnockoutJS SPA 템플릿](../introduction/knockoutjs-template.md) ASP.NET 및 Web Tools 2012.2 업데이트에 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-110">The Breeze/Angular SPA template is a variation on the [KnockoutJS SPA template](../introduction/knockoutjs-template.md) included in the ASP.NET and Web Tools 2012.2 Update.</span></span> <span data-ttu-id="a5ed0-111">Visual Studio 있다면 해야 예로 SPA를 실행 60 초 이내에 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-111">If you've got Visual Studio, you'll have an example SPA up and running in less than 60 seconds.</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/NgRunningTodoPage.png)

<span data-ttu-id="a5ed0-112">외부적으로, 응용 프로그램에서는 KnockoutJS SPA 템플릿 매우 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-112">Outwardly, the application looks the very similar to the KnockoutJS SPA template.</span></span> <span data-ttu-id="a5ed0-113">하지만 내부적 상당히 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-113">But it's quite different under the hood.</span></span> <span data-ttu-id="a5ed0-114">KnockoutJS 템플릿 Knockout을 사용 하 여 데이터 바인딩 및 데이터 액세스에 대 한 원시 AJAX에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-114">The KnockoutJS template uses Knockout for data binding and raw AJAX for data access.</span></span> <span data-ttu-id="a5ed0-115">Breeze/Angular 템플릿 데이터 액세스에 대 한 데이터 바인딩 및 설치에 대 한 Angular를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-115">The Breeze/Angular template uses Angular for data binding and Breeze for data access.</span></span> <span data-ttu-id="a5ed0-116">이러한 libaries 페이지 탐색 및 기록을 비롯 한 추가 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-116">These libaries enable additional capabilities, including page navigation and history.</span></span>

<span data-ttu-id="a5ed0-117">응용 프로그램에 대 한 페이지는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-117">Here is the application's About page:</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/NgRunningAboutPage.png)

<span data-ttu-id="a5ed0-118">이 페이지는 현재 사용자 세션 중 실행 로그의 이벤트를 표시 합니다. 포함 하 여:</span><span class="sxs-lookup"><span data-stu-id="a5ed0-118">This page displays a running log of events during the current user session, including:</span></span>

- <span data-ttu-id="a5ed0-119">페이징 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-119">Paging.</span></span> <span data-ttu-id="a5ed0-120"># 2와 # 7에서 Todo 컨트롤러 만들기를 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-120">Note the Todo controller creation at #2 and #7.</span></span>
- <span data-ttu-id="a5ed0-121">원격 쿼리 (3) 및 로컬 캐시 쿼리 (7).</span><span class="sxs-lookup"><span data-stu-id="a5ed0-121">Remote queries (#3) and local cache queries (#7).</span></span>
- <span data-ttu-id="a5ed0-122">새 저장 (5, 6) 및 (4) 엔터티를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-122">Saving new (#5, #6) and modified (#4) entities.</span></span>
- <span data-ttu-id="a5ed0-123">유효성 검사 (#9), 클라이언트에서 변경 내용을 커밋하기 전에 사용자 실수를 수정할 수 있도록 데이터베이스에 변경 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-123">Changes validated on the client (#9), so the user can correct mistakes before committing changes to the database.</span></span>

<span data-ttu-id="a5ed0-124">이 템플릿에서 탐색을 더 포함:</span><span class="sxs-lookup"><span data-stu-id="a5ed0-124">There's more to explore in this template, including:</span></span>

- <span data-ttu-id="a5ed0-125">HTML 보기 템플릿의 동적으로 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-125">Dynamic loading of HTML view templates.</span></span>
- <span data-ttu-id="a5ed0-126">Angular "지시문입니다."를 통해 사용자 지정 데이터 바인딩</span><span class="sxs-lookup"><span data-stu-id="a5ed0-126">Custom data binding through Angular "directives."</span></span>
- <span data-ttu-id="a5ed0-127">모듈성 및 종속성 주입 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-127">Modularity and dependency injection.</span></span>
- <span data-ttu-id="a5ed0-128">쿼리 필터, 정렬, 페이징, 프로젝션 및 관련된 엔터티를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-128">Query filters, sorts, paging, projections, and inclusion of related entities.</span></span>
- <span data-ttu-id="a5ed0-129">여러 화면에 걸쳐 데이터를 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-129">Sharing data across multiple screens.</span></span>
- <span data-ttu-id="a5ed0-130">단일 트랜잭션으로 여러 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-130">Saving multiple changes as a single transaction.</span></span>
- <span data-ttu-id="a5ed0-131">유효성 검사 규칙을 JavaScript 클라이언트는 서버에서 자동으로 전파 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-131">Validation rules propagated automatically from the server to the JavaScript client.</span></span>

<span data-ttu-id="a5ed0-132">이제 시작해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-132">Let's get started.</span></span>

## <a name="create-a-breezeangular-template-project"></a><span data-ttu-id="a5ed0-133">Breeze/Angular 템플릿 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="a5ed0-133">Create a Breeze/Angular Template Project</span></span>

<span data-ttu-id="a5ed0-134">다운로드 하 고 위의 다운로드 단추를 클릭 하 여 템플릿을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-134">Download and install the template by clicking the Download button above.</span></span> <span data-ttu-id="a5ed0-135">서식 파일은 Visual Studio 확장 (VSIX) 파일로 패키지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-135">The template is packaged as a Visual Studio Extension (VSIX) file.</span></span> <span data-ttu-id="a5ed0-136">Visual Studio를 다시 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-136">You might need to restart Visual Studio.</span></span>

<span data-ttu-id="a5ed0-137">에 **템플릿** 창 **설치 된 템플릿** 확장 하 고는 **Visual C#** 노드.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-137">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="a5ed0-138">아래 **Visual C#** 를 선택 **웹**합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-138">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="a5ed0-139">프로젝트 템플릿 목록에서 선택 **ASP.NET MVC 4 웹 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-139">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="a5ed0-140">프로젝트 이름을 지정 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-140">Name the project and click **OK**.</span></span>

<span data-ttu-id="a5ed0-141">에 **새 프로젝트** 마법사 **Breeze Angular SPA**합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-141">In the **New Project** wizard, select **Breeze Angular SPA**.</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/SelectBreezeNgSpaTemplate.png)

<span data-ttu-id="a5ed0-142">Ctrl-F5 키를 눌러 빌드하고 디버깅 하지 않고 응용 프로그램을 실행 또는 디버깅 실행 하려면 F5 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-142">Press Ctrl-F5 to build and run the application without debugging, or press F5 to run with debugging.</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/ZephyrLogin.png)

<span data-ttu-id="a5ed0-143">응용 프로그램을 처음 실행 하면 로그인 화면을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-143">When the application first runs, it displays a login screen.</span></span> <span data-ttu-id="a5ed0-144">"등록" 링크를 클릭 하 고 사용자 이름과 암호를 입력할 수 있는 보기에 새 페이지 glides 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-144">Click the "Sign up" link and a new page glides into view, where you can enter a username and password.</span></span> <span data-ttu-id="a5ed0-145">(로그인 및 등록 페이지 빌드됩니다 ASP.NET MVC를 사용 하 여.) 등록 양식을 제출 하면 계정에 대 한 두 개의 항목을 사용 하 여 TodoList 서버에 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-145">(The login and registration pages are built using ASP.NET MVC.) When you submit the registration form, the server generates a TodoList with two items for your account.</span></span> <span data-ttu-id="a5ed0-146">그런 다음 표시 하는 노란색에서.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-146">Then it presents them to you on a yellow note.</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/TodoList.png)

<span data-ttu-id="a5ed0-147">이제 사용자는 SPA land 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-147">Now you are in the land of SPA.</span></span> <span data-ttu-id="a5ed0-148">모든 표시를 렌더링 되며 Knockout 및 쉽게 활용 하 여 클라이언트에서 관리 되는 todo 항목을 조작 하는 동안 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-148">Everything you see and experience while manipulating Todos is rendered and managed on the client with the help of Knockout and Breeze.</span></span> <span data-ttu-id="a5ed0-149">사용자로 앱을 탐색 하는 중...</span><span class="sxs-lookup"><span data-stu-id="a5ed0-149">Explore the app as a user …</span></span> <span data-ttu-id="a5ed0-150">하지만 개발자의 눈 모양입니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-150">but with a developer's eye.</span></span> <span data-ttu-id="a5ed0-151">브라우저에서 개발자 도구를 사용 하 여 네트워크 트래픽 캡처.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-151">Use the developer tools in your browser to capture the network traffic.</span></span> <span data-ttu-id="a5ed0-152">(Internet Explorer에서: F12 키를 눌러 선택 합니다 **네트워크** 탭을 클릭 **캡처하기 시작할**.) 이제 다음과 같이 하십시오.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-152">(In Internet Explorer: Press F12, select the **Network** tab, and click **Start capturing**.) Now try the following:</span></span>

- <span data-ttu-id="a5ed0-153">새 Todo 항목을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-153">Add a new Todo item.</span></span>
- <span data-ttu-id="a5ed0-154">레이블을 클릭 하 고 Todo 항목 제목 편집</span><span class="sxs-lookup"><span data-stu-id="a5ed0-154">Click the label and edit the Todo item title</span></span>
- <span data-ttu-id="a5ed0-155">표시 항목 완료 하는 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-155">Check a checkbox to mark the item done.</span></span> <span data-ttu-id="a5ed0-156">제목을 편집할 수 없게 됩니다 있도록 textbox가 비활성화 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-156">Notice that the textbox is disabled, so the title is no longer editable.</span></span>
- <span data-ttu-id="a5ed0-157">레이블의 오른쪽에 있는 'x'를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-157">Click the ‘x' to the right of the label.</span></span> <span data-ttu-id="a5ed0-158">항목 사라지고 데이터베이스에서 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-158">The item disappears and is deleted from the database.</span></span>
- <span data-ttu-id="a5ed0-159">다른 항목을 선택 하 고 제목을 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-159">Pick another item and clear its title.</span></span> <span data-ttu-id="a5ed0-160">제목은 필수 유효성 검사 오류를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-160">You'll get a validation error that the title is required.</span></span> <span data-ttu-id="a5ed0-161">잠시 후에 이전 제목 복원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-161">After a brief pause, the previous title is restored.</span></span>
- <span data-ttu-id="a5ed0-162">터무니 없이 긴 제목을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-162">Type in a ridiculously long title.</span></span> <span data-ttu-id="a5ed0-163">제목이 너무 깁니다 서로 다른 유효성 검사 오류를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-163">You'll get a different validation error that the title is too long.</span></span>
- <span data-ttu-id="a5ed0-164">"할 일 목록에 추가" 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-164">Click the "Add Todo List" button.</span></span> <span data-ttu-id="a5ed0-165">왼쪽 위 목록에 새 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-165">A new list appears to the left of the previous list.</span></span>
- <span data-ttu-id="a5ed0-166">TodoList 타이틀을 요구 하는 트리거 및 길이 유효성 검사를 사용 하 여 재생 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-166">Play with the TodoList title, triggering its required and length validations.</span></span>
- <span data-ttu-id="a5ed0-167">오류 메시지를 지우려면 제목 텍스트 상자를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-167">Click in the title textbox to clear the error message.</span></span>
- <span data-ttu-id="a5ed0-168">TodoList 및 해당 todo 항목을 삭제 하려면 오른쪽 위 모서리에서 원에 있는 "x"를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-168">Click the "x" in the circle in the upper right corner to delete the TodoList and its todos.</span></span>
- <span data-ttu-id="a5ed0-169">이러한 작업의 로그를 보려면 오른쪽 위에 있는 "정보" 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-169">Click the "About" link in the upper right to see a log of these activities.</span></span>

<span data-ttu-id="a5ed0-170">유효성 검사 논리는 간단 하 여 클라이언트 쪽 수행된.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-170">The validation logic is performed client-side by Breeze.</span></span> <span data-ttu-id="a5ed0-171">서버 모델 클래스에 유효성 검사 특성은 클라이언트에 전파 하 고 클라이언트는 서버에 연결 하기 전에 자동으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-171">Validation attributes on the server model classes are propagated to the client and executed automatically before the client contacts the server.</span></span>

<span data-ttu-id="a5ed0-172">네트워크 트래픽을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-172">Review the network traffic.</span></span> <span data-ttu-id="a5ed0-173">설치 오류를 검색 하는 경우 서버에 대 한 호출 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-173">Notice that there were no calls to the server when Breeze detected an error.</span></span> <span data-ttu-id="a5ed0-174">"/ Api/Todo/SaveChanges"로 POST 요청에 유효한 각 변경이 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-174">Each valid change resulted in a POST request to "/api/Todo/SaveChanges".</span></span> <span data-ttu-id="a5ed0-175">Breeze 변경 내용을 번들 및 보내 함께 단일 요청으로 Web API 컨트롤러에 `SaveChanges` 메서드.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-175">Breeze bundles the changes and sends them together as a single request to the Web API controller's `SaveChanges` method.</span></span> <span data-ttu-id="a5ed0-176">PUT, POST 및 각 항목에 대 한 요청을 개별적으로 삭제 합니다. 그러면 KockoutJS SPA 템플릿에서 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-176">That's different from KockoutJS SPA template, which makes PUT, POST, and DELETE requests for each item individually.</span></span>

<span data-ttu-id="a5ed0-177">또한 페이지에 대 한를 TodoList 사이 전환 하는 경우 네트워크 트래픽이 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-177">Also, notice there is no network traffic when you switch between the TodoList and About pages.</span></span> <span data-ttu-id="a5ed0-178">로컬 설치 캐시 하도록 제한 된 쿼리 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-178">That's because the query has been constrained to the local Breeze cache.</span></span>

## <a name="peek-inside"></a><span data-ttu-id="a5ed0-179">내 보기</span><span class="sxs-lookup"><span data-stu-id="a5ed0-179">Peek inside</span></span>

<span data-ttu-id="a5ed0-180">이 응용 프로그램에는 클라이언트 쪽 및 서버 쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-180">This application has a client side and a server side.</span></span> <span data-ttu-id="a5ed0-181">클라이언트 쪽 스택 ("Scripts" 폴더에 있음)에서 타사 JavaScript 라이브러리와 조금 HTML 및 응용 프로그램 JavaScript 모듈 ("앱" 폴더에 있음)의 조합으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-181">The client-side stack consists of a little HTML and a combination of application JavaScript modules (in the "app" folder) plus third-party JavaScript libraries (in the "Scripts" folder).</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/NgClientArchitecture2.png)

<span data-ttu-id="a5ed0-182">UI 아키텍처 컨트롤러에서 지 원하는 프레젠테이션 코드에서 뷰의 HTML 위젯이 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-182">The UI architecture separates the HTML widgets of the views from the supporting presentation code in the controllers.</span></span> <span data-ttu-id="a5ed0-183">Angular 데이터 바인딩 시스템 각 지식이 없어도 다른 작업을 수행할 수 있도록 뷰 및 컨트롤러를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-183">The Angular data-binding system coordinates views and controllers so that each can do its job without intimate knowledge of the other.</span></span>

<span data-ttu-id="a5ed0-184">컨트롤러 요청 데이터 컨텍스트를 가져와서 모델 엔터티를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-184">The controller asks the data context to acquire and save the model entities.</span></span> <span data-ttu-id="a5ed0-185">데이터 컨텍스트 Breeze JSON 쿼리 결과에서 자동 추적 모델 개체를 생성 하는 작업의 대부분을 위임 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-185">The data context delegates most of the work to Breeze, which constructs self-tracking model objects from JSON query results.</span></span>

<span data-ttu-id="a5ed0-186">서버 쪽 스택의 일부 개발자 코드 및 라이브러리로 구성 되며 세 가지 원칙.NET: Web API, Entity Framework 및 Breeze.NET:</span><span class="sxs-lookup"><span data-stu-id="a5ed0-186">The server-side stack consists of some developer code and three principle .NET libraries: Web API, Entity Framework, and Breeze.NET:</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/ServerArchitecture.png)

<span data-ttu-id="a5ed0-187">기본 아키텍처 KockoutJS SPA 템플릿와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-187">The basic architecture is the same as the KockoutJS SPA template.</span></span> <span data-ttu-id="a5ed0-188">하지만 구현은 훨씬 더 간단: The Dto 삭제 및 Entity Framework 세부 정보를 대부분 Breeze.NET에 게 위임 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-188">However, the implementation is much simpler: The DTOs were deleted, and most of the Entity Framework details have been delegated to Breeze.NET.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5ed0-189">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a5ed0-189">Next Steps</span></span>

<span data-ttu-id="a5ed0-190">여는 코드를 탐색 하는 것이 좋습니다 합니다 [광범위 한 토론](http://www.breezejs.com/ng-spa-template?utm_source=ms-spa) 클라이언트와 서버 스택 손쉽게 웹 사이트의.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-190">We suggest that you explore the code, guided by the [extensive discussion](http://www.breezejs.com/ng-spa-template?utm_source=ms-spa) of both the client and the server stacks on the Breeze website.</span></span>

<span data-ttu-id="a5ed0-191">Breeze 클라이언트 쪽 쿼리를 다루기를 시도해 볼 수 있습니다. 일부 필터 및 정렬을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-191">You might try playing with Breeze client-side query; add some filters and sorts.</span></span> <span data-ttu-id="a5ed0-192">자세한 모델 속성과 엔드-투-엔드 SPA 개발을 위한 더 나은 이해할 수 있도록 더 많은 엔터티를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-192">You might add more model properties and more entities to get a better feel for end-to-end SPA development.</span></span> <span data-ttu-id="a5ed0-193">디자인의 확신할 경우 Todo 기능을 사용해 삭제 수 있으며 사용자 고유의로 교체할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5ed0-193">When you are confident of the design, you can tear out the Todo features and replace them with your own.</span></span>

<span data-ttu-id="a5ed0-194">즐거운 코딩을 경험하시기 바랍니다!</span><span class="sxs-lookup"><span data-stu-id="a5ed0-194">Happy coding!</span></span>
