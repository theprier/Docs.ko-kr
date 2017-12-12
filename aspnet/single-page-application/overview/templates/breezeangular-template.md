---
uid: single-page-application/overview/templates/breezeangular-template
title: "간편/각 템플릿 | Microsoft Docs"
author: madskristensen
description: "간편/각 단일 페이지 응용 프로그램 템플릿"
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/08/2013
ms.topic: article
ms.assetid: db31e909-563a-4516-aadd-62aa210ac7e4
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /single-page-application/overview/templates/breezeangular-template
msc.type: authoredcontent
ms.openlocfilehash: faf28a510a83b7fa07585904344176601c2e1f34
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="breezeangular-template"></a><span data-ttu-id="311c1-103">간편/각 서식 파일</span><span class="sxs-lookup"><span data-stu-id="311c1-103">Breeze/Angular template</span></span>
====================
<span data-ttu-id="311c1-104">여 [Kristensen Mads](https://github.com/madskristensen)</span><span class="sxs-lookup"><span data-stu-id="311c1-104">by [Mads Kristensen](https://github.com/madskristensen)</span></span>

> <span data-ttu-id="311c1-105">간편/각 MVC 템플릿에서 워드 벨에 의해 작성 되었으므로</span><span class="sxs-lookup"><span data-stu-id="311c1-105">The Breeze/Angular MVC Template was written by Ward Bell</span></span>
> 
> [<span data-ttu-id="311c1-106">간편/각도 MVC 템플릿 다운로드</span><span class="sxs-lookup"><span data-stu-id="311c1-106">Download the Breeze/Angular MVC Template</span></span>](https://go.microsoft.com/fwlink/?LinkId=286437)


<span data-ttu-id="311c1-107">[AngularJS](http://angularjs.org) 단일 페이지 응용 프로그램 (SPAs)는 Google에서 오픈 소스 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-107">[AngularJS](http://angularjs.org) is an open source library from Google for building Single Page Applications (SPAs).</span></span> <span data-ttu-id="311c1-108">데이터 바인딩, 종속성 주입 및 관리 화면을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-108">It offers data binding, dependency injection, and screen management.</span></span> <span data-ttu-id="311c1-109">와 함께 사용할 [BreezeJS](http://www.breezejs.com/?utm_source=ms-spa), 데이터 모델링 및 데이터 관리에 대 한 다른 오픈 소스 라이브러리 뛰어난 HTML/JavaScript 클라이언트 앱에 대 한 필수 구성 요소가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-109">Combine it with [BreezeJS](http://www.breezejs.com/?utm_source=ms-spa), another open source library for data modeling and data management, and you have the essential ingredients for a great HTML/JavaScript client app.</span></span>

<span data-ttu-id="311c1-110">간편/각 SPA 서식 파일은 한 변형에는 [KnockoutJS SPA 템플릿](../introduction/knockoutjs-template.md) ASP.NET 및 Web Tools 2012.2 업데이트에 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-110">The Breeze/Angular SPA template is a variation on the [KnockoutJS SPA template](../introduction/knockoutjs-template.md) included in the ASP.NET and Web Tools 2012.2 Update.</span></span> <span data-ttu-id="311c1-111">Visual Studio 있다면 해야 SPA 예 실행 되 고 60 초 이내에 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-111">If you've got Visual Studio, you'll have an example SPA up and running in less than 60 seconds.</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/NgRunningTodoPage.png)

<span data-ttu-id="311c1-112">외부적으로, 응용 프로그램에서는 KnockoutJS SPA 템플릿에 매우 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-112">Outwardly, the application looks the very similar to the KnockoutJS SPA template.</span></span> <span data-ttu-id="311c1-113">하지만 내부에서 매우 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-113">But it's quite different under the hood.</span></span> <span data-ttu-id="311c1-114">KnockoutJS 템플릿은 데이터 바인딩 및 데이터 액세스에 대 한 원시 AJAX Knockout를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-114">The KnockoutJS template uses Knockout for data binding and raw AJAX for data access.</span></span> <span data-ttu-id="311c1-115">간편/각 템플릿은 데이터 액세스에 대 한 데이터 바인딩 및 옵션에 대 한 각을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-115">The Breeze/Angular template uses Angular for data binding and Breeze for data access.</span></span> <span data-ttu-id="311c1-116">이러한 libaries 페이지 탐색 및 기록을 포함 하 여 추가 기능을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-116">These libaries enable additional capabilities, including page navigation and history.</span></span>

<span data-ttu-id="311c1-117">응용 프로그램에 대 한 페이지는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-117">Here is the application's About page:</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/NgRunningAboutPage.png)

<span data-ttu-id="311c1-118">이 페이지는 현재 사용자 세션 동안 실행 로그의 이벤트를 표시 합니다. 포함 하 여:</span><span class="sxs-lookup"><span data-stu-id="311c1-118">This page displays a running log of events during the current user session, including:</span></span>

- <span data-ttu-id="311c1-119">페이징 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-119">Paging.</span></span> <span data-ttu-id="311c1-120">Note # 2와 # 7에 Todo 컨트롤러 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-120">Note the Todo controller creation at #2 and #7.</span></span>
- <span data-ttu-id="311c1-121">원격 쿼리 (3) 및 로컬 캐시 쿼리 (7).</span><span class="sxs-lookup"><span data-stu-id="311c1-121">Remote queries (#3) and local cache queries (#7).</span></span>
- <span data-ttu-id="311c1-122">새로 저장 (5, 6) (#4) 엔터티를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-122">Saving new (#5, #6) and modified (#4) entities.</span></span>
- <span data-ttu-id="311c1-123">변경 내용을 데이터베이스에 변경 내용을 커밋하기 전에 사용자의 실수를 수정할 수 있으므로 (#9), 클라이언트에서 검증 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-123">Changes validated on the client (#9), so the user can correct mistakes before committing changes to the database.</span></span>

<span data-ttu-id="311c1-124">이 서식 파일에서 탐색을 자세히 포함 하 여:</span><span class="sxs-lookup"><span data-stu-id="311c1-124">There's more to explore in this template, including:</span></span>

- <span data-ttu-id="311c1-125">HTML 보기 템플릿 동적 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-125">Dynamic loading of HTML view templates.</span></span>
- <span data-ttu-id="311c1-126">각 "지시문"를 통해 사용자 지정 데이터 바인딩</span><span class="sxs-lookup"><span data-stu-id="311c1-126">Custom data binding through Angular "directives."</span></span>
- <span data-ttu-id="311c1-127">모듈 및 종속성 주입 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-127">Modularity and dependency injection.</span></span>
- <span data-ttu-id="311c1-128">쿼리 필터, 정렬, 페이징, 프로젝션 및 관련된 엔터티를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-128">Query filters, sorts, paging, projections, and inclusion of related entities.</span></span>
- <span data-ttu-id="311c1-129">여러 화면에 걸쳐 데이터를 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-129">Sharing data across multiple screens.</span></span>
- <span data-ttu-id="311c1-130">단일 트랜잭션으로 여러 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-130">Saving multiple changes as a single transaction.</span></span>
- <span data-ttu-id="311c1-131">유효성 검사 규칙 JavaScript 클라이언트는 서버에서 자동으로 전파 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-131">Validation rules propagated automatically from the server to the JavaScript client.</span></span>

<span data-ttu-id="311c1-132">이제 시작해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-132">Let's get started.</span></span>

## <a name="create-a-breezeangular-template-project"></a><span data-ttu-id="311c1-133">간편/각도 템플릿 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="311c1-133">Create a Breeze/Angular Template Project</span></span>

<span data-ttu-id="311c1-134">다운로드 하 고 위의 다운로드 단추를 클릭 하 여 서식 파일을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-134">Download and install the template by clicking the Download button above.</span></span> <span data-ttu-id="311c1-135">서식 파일은 확장 VSIX (Visual Studio) 파일로 패키지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-135">The template is packaged as a Visual Studio Extension (VSIX) file.</span></span> <span data-ttu-id="311c1-136">Visual Studio를 다시 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-136">You might need to restart Visual Studio.</span></span>

<span data-ttu-id="311c1-137">에 **템플릿** 창 선택 **설치 된 템플릿** 확장는 **Visual C#** 노드.</span><span class="sxs-lookup"><span data-stu-id="311c1-137">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="311c1-138">아래 **Visual C#**선택, **웹**합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-138">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="311c1-139">프로젝트 템플릿 목록에서 선택 **ASP.NET MVC 4 웹 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-139">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="311c1-140">프로젝트 이름을 지정 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-140">Name the project and click **OK**.</span></span>

<span data-ttu-id="311c1-141">에 **새 프로젝트** 선택 마법사 **간편 각도 SPA**합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-141">In the **New Project** wizard, select **Breeze Angular SPA**.</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/SelectBreezeNgSpaTemplate.png)

<span data-ttu-id="311c1-142">빌드하고 디버깅 하지 않고 응용 프로그램을 실행 하려면 Ctrl + f 5를 누르거나 f5 키를 눌러 디버깅이 설정 된 상태로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-142">Press Ctrl-F5 to build and run the application without debugging, or press F5 to run with debugging.</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/ZephyrLogin.png)

<span data-ttu-id="311c1-143">응용 프로그램을 처음 실행할 때 로그인 화면을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-143">When the application first runs, it displays a login screen.</span></span> <span data-ttu-id="311c1-144">사용자 이름 및 암호를 입력할 수 있는 새 페이지를 glides 고 "등록" 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-144">Click the "Sign up" link and a new page glides into view, where you can enter a username and password.</span></span> <span data-ttu-id="311c1-145">(로그인 및 등록 페이지 빌드됩니다 ASP.NET MVC를 사용 하 여.) 등록 양식을 제출 하면 서버 계정에 대해 두 개의 항목과 TodoList를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-145">(The login and registration pages are built using ASP.NET MVC.) When you submit the registration form, the server generates a TodoList with two items for your account.</span></span> <span data-ttu-id="311c1-146">그런 다음 표시에 노란색으로 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-146">Then it presents them to you on a yellow note.</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/TodoList.png)

<span data-ttu-id="311c1-147">이제 SPA 토지 위치는입니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-147">Now you are in the land of SPA.</span></span> <span data-ttu-id="311c1-148">모든 항목을 보고 있습니다 Todos 조작 렌더링 되 고 서버의 Knockout 및 간편 도움을 사용 하 여 클라이언트에서 관리 하는 동안 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-148">Everything you see and experience while manipulating Todos is rendered and managed on the client with the help of Knockout and Breeze.</span></span> <span data-ttu-id="311c1-149">응용 프로그램 사용자로 탐색 중...</span><span class="sxs-lookup"><span data-stu-id="311c1-149">Explore the app as a user …</span></span> <span data-ttu-id="311c1-150">하지만 개발자의 눈 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-150">but with a developer's eye.</span></span> <span data-ttu-id="311c1-151">브라우저에서 개발자 도구를 사용 하 여 네트워크 트래픽을 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-151">Use the developer tools in your browser to capture the network traffic.</span></span> <span data-ttu-id="311c1-152">(Internet Explorer에서: F12 키를 눌러 선택 된 **네트워크** 탭을 클릭 **를 캡처하기 시작**.) 이제 다음과 같이 하세요.</span><span class="sxs-lookup"><span data-stu-id="311c1-152">(In Internet Explorer: Press F12, select the **Network** tab, and click **Start capturing**.) Now try the following:</span></span>

- <span data-ttu-id="311c1-153">새 할 일 항목을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-153">Add a new Todo item.</span></span>
- <span data-ttu-id="311c1-154">레이블을 클릭 하 고 할 일 항목 제목을 편집합니다</span><span class="sxs-lookup"><span data-stu-id="311c1-154">Click the label and edit the Todo item title</span></span>
- <span data-ttu-id="311c1-155">완료 항목을 표시 하는 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-155">Check a checkbox to mark the item done.</span></span> <span data-ttu-id="311c1-156">공지는 textbox를 사용할 수 없으므로 제목을 편집할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-156">Notice that the textbox is disabled, so the title is no longer editable.</span></span>
- <span data-ttu-id="311c1-157">레이블의 오른쪽에 있는 'x'를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-157">Click the ‘x' to the right of the label.</span></span> <span data-ttu-id="311c1-158">항목 사라지고 데이터베이스에서 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-158">The item disappears and is deleted from the database.</span></span>
- <span data-ttu-id="311c1-159">다른 항목을 선택 하 고 제목을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-159">Pick another item and clear its title.</span></span> <span data-ttu-id="311c1-160">제목은 필요 유효성 검사 오류를 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-160">You'll get a validation error that the title is required.</span></span> <span data-ttu-id="311c1-161">잠깐 일시 중지 된 후 이전 제목 복원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-161">After a brief pause, the previous title is restored.</span></span>
- <span data-ttu-id="311c1-162">긴 터무니 없이 제목을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-162">Type in a ridiculously long title.</span></span> <span data-ttu-id="311c1-163">제목이 너무 깁니다 서로 다른 유효성 검사 오류를 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-163">You'll get a different validation error that the title is too long.</span></span>
- <span data-ttu-id="311c1-164">"할 일 목록 추가" 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-164">Click the "Add Todo List" button.</span></span> <span data-ttu-id="311c1-165">왼쪽 위 목록에 표시 된 새 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-165">A new list appears to the left of the previous list.</span></span>
- <span data-ttu-id="311c1-166">TodoList 제목, 필요한 트리거와 길이 유효성 검사를 재생 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-166">Play with the TodoList title, triggering its required and length validations.</span></span>
- <span data-ttu-id="311c1-167">오류 메시지의 선택을 취소 하 고 제목 입력란을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-167">Click in the title textbox to clear the error message.</span></span>
- <span data-ttu-id="311c1-168">TodoList 및 해당 todos 삭제 하려면 오른쪽 위 모서리의 원 안에 있는 "x"를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-168">Click the "x" in the circle in the upper right corner to delete the TodoList and its todos.</span></span>
- <span data-ttu-id="311c1-169">이러한 활동의 한 로그를 보려면 오른쪽 위에 있는 "정보" 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-169">Click the "About" link in the upper right to see a log of these activities.</span></span>

<span data-ttu-id="311c1-170">유효성 검사 논리는 간단 하 여 수행된 된 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-170">The validation logic is performed client-side by Breeze.</span></span> <span data-ttu-id="311c1-171">서버 모델 클래스에 유효성 검사 특성 클라이언트에 전파 하 고 클라이언트는 서버에 연결 하기 전에 자동으로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-171">Validation attributes on the server model classes are propagated to the client and executed automatically before the client contacts the server.</span></span>

<span data-ttu-id="311c1-172">네트워크 소통량을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-172">Review the network traffic.</span></span> <span data-ttu-id="311c1-173">옵션에 오류가 발생 하는 경우 서버에 대 한 호출 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-173">Notice that there were no calls to the server when Breeze detected an error.</span></span> <span data-ttu-id="311c1-174">각 올바른 변경 내용에 "/ api/Todo/SaveChanges" POST 요청에서 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-174">Each valid change resulted in a POST request to "/api/Todo/SaveChanges".</span></span> <span data-ttu-id="311c1-175">옵션 변경 내용을 함께 묶는 하 고 보냅니다 함께 단일 요청으로 Web API 컨트롤러에 `SaveChanges` 메서드.</span><span class="sxs-lookup"><span data-stu-id="311c1-175">Breeze bundles the changes and sends them together as a single request to the Web API controller's `SaveChanges` method.</span></span> <span data-ttu-id="311c1-176">PUT, POST 및 각 항목에 대 한 요청을 개별적으로 삭제를 낮추는 KockoutJS SPA 템플릿에서 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-176">That's different from KockoutJS SPA template, which makes PUT, POST, and DELETE requests for each item individually.</span></span>

<span data-ttu-id="311c1-177">또한는 TodoList 사이 및 페이지에 대 한 전환 하는 경우 네트워크 트래픽이 없음 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-177">Also, notice there is no network traffic when you switch between the TodoList and About pages.</span></span> <span data-ttu-id="311c1-178">쿼리 옵션의 로컬 캐시 제한 된 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-178">That's because the query has been constrained to the local Breeze cache.</span></span>

## <a name="peek-inside"></a><span data-ttu-id="311c1-179">내 보기</span><span class="sxs-lookup"><span data-stu-id="311c1-179">Peek inside</span></span>

<span data-ttu-id="311c1-180">이 응용 프로그램에 클라이언트 쪽 및 서버 쪽 있습니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-180">This application has a client side and a server side.</span></span> <span data-ttu-id="311c1-181">클라이언트 쪽 스택 ("Scripts" 폴더)에서 공급 업체 JavaScript 라이브러리와 약간 HTML과 응용 프로그램 JavaScript 모듈 ("app" 폴더에 있음)의 조합으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-181">The client-side stack consists of a little HTML and a combination of application JavaScript modules (in the "app" folder) plus third-party JavaScript libraries (in the "Scripts" folder).</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/NgClientArchitecture2.png)

<span data-ttu-id="311c1-182">UI 아키텍처 컨트롤러에서 지 원하는 프레젠테이션 코드에서 뷰의 HTML 위젯을 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-182">The UI architecture separates the HTML widgets of the views from the supporting presentation code in the controllers.</span></span> <span data-ttu-id="311c1-183">각 데이터 바인딩 시스템과 각 작업은 다른 알지 못하면 작업을 수행할 수 있도록 뷰 및 컨트롤러를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-183">The Angular data-binding system coordinates views and controllers so that each can do its job without intimate knowledge of the other.</span></span>

<span data-ttu-id="311c1-184">컨트롤러에는 데이터 컨텍스트를 획득 하 고 모델 엔터티에 저장를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-184">The controller asks the data context to acquire and save the model entities.</span></span> <span data-ttu-id="311c1-185">데이터 컨텍스트는 대부분의 JSON 쿼리 결과에서 자체 추적 모델 개체를 생성 하는 옵션을 작업을 위임 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-185">The data context delegates most of the work to Breeze, which constructs self-tracking model objects from JSON query results.</span></span>

<span data-ttu-id="311c1-186">서버 쪽 스택 일부 개발자 코드 및 세 가지 원칙.NET 라이브러리 구성: Web API, Entity Framework 및 Breeze.NET:</span><span class="sxs-lookup"><span data-stu-id="311c1-186">The server-side stack consists of some developer code and three principle .NET libraries: Web API, Entity Framework, and Breeze.NET:</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/ServerArchitecture.png)

<span data-ttu-id="311c1-187">기본 아키텍처 KockoutJS SPA 템플릿으로 같습니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-187">The basic architecture is the same as the KockoutJS SPA template.</span></span> <span data-ttu-id="311c1-188">하지만 구현이 훨씬 더 간단: The Dto 삭제 된 및 Entity Framework의 대부분을 Breeze.NET에 게 위임 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-188">However, the implementation is much simpler: The DTOs were deleted, and most of the Entity Framework details have been delegated to Breeze.NET.</span></span>

## <a name="next-steps"></a><span data-ttu-id="311c1-189">다음 단계</span><span class="sxs-lookup"><span data-stu-id="311c1-189">Next Steps</span></span>

<span data-ttu-id="311c1-190">여는 코드를 확인 하는 것이 좋습니다는 [광범위 한 토론](http://www.breezejs.com/ng-spa-template?utm_source=ms-spa) 클라이언트와 서버 스택 쉽게 웹 사이트에서의 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-190">We suggest that you explore the code, guided by the [extensive discussion](http://www.breezejs.com/ng-spa-template?utm_source=ms-spa) of both the client and the server stacks on the Breeze website.</span></span>

<span data-ttu-id="311c1-191">재생 옵션 클라이언트 쪽 쿼리로; 해 볼 수도 있습니다. 일부 필터 및 정렬을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-191">You might try playing with Breeze client-side query; add some filters and sorts.</span></span> <span data-ttu-id="311c1-192">더 많은 모델 속성 및 종단 간 SPA 개발을 위한 더 나은 이해할 수 있도록 더 많은 엔터티를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="311c1-192">You might add more model properties and more entities to get a better feel for end-to-end SPA development.</span></span> <span data-ttu-id="311c1-193">디자인의 확신할 경우 Todo 기능을 사용해 중지할 수 있으며 사용자의 정보로 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="311c1-193">When you are confident of the design, you can tear out the Todo features and replace them with your own.</span></span>

<span data-ttu-id="311c1-194">즐거운 코딩을 경험하시기 바랍니다!</span><span class="sxs-lookup"><span data-stu-id="311c1-194">Happy coding!</span></span>
