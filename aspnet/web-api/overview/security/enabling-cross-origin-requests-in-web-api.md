---
uid: web-api/overview/security/enabling-cross-origin-requests-in-web-api
title: ASP.NET Web API 2에서에서 크로스-원본 요청을 사용 하도록 설정 | Microsoft Docs
author: MikeWasson
description: ASP.NET Web API에서 크로스-원본 자원 공유 (CORS)를 지 원하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 01/29/2019
ms.assetid: 9b265a5a-6a70-4a82-adce-2d7c56ae8bdd
msc.legacyurl: /web-api/overview/security/enabling-cross-origin-requests-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 97a0027194b019b09e220493dcb593e682027fe3
ms.sourcegitcommit: d22b3c23c45a076c4f394a70b1c8df2fbcdf656d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2019
ms.locfileid: "55428449"
---
<a name="enable-cross-origin-requests-in-aspnet-web-api-2"></a><span data-ttu-id="c0c09-103">ASP.NET Web API 2에서 크로스-원본 요청을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="c0c09-103">Enable cross-origin requests in ASP.NET Web API 2</span></span>
====================
<span data-ttu-id="c0c09-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="c0c09-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="c0c09-105">브라우저의 보안 기능은 웹 페이지에서 다른 도메인으로 AJAX 요청을 전송하는 것을 막습니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-105">Browser security prevents a web page from making AJAX requests to another domain.</span></span> <span data-ttu-id="c0c09-106">이 제약 사항을 *동일 원본 정책(Same-Origin Policy)* 이라고 부르며, 악의적인 사이트가 다른 사이트의 민감한 데이터를 무차별적으로 읽는 것을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-106">This restriction is called the *same-origin policy*, and prevents a malicious site from reading sensitive data from another site.</span></span> <span data-ttu-id="c0c09-107">그러나 하려는 경우가 있습니다 수 다른 사이트에 web API를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-107">However, sometimes you might want to let other sites call your web API.</span></span>
>
> <span data-ttu-id="c0c09-108">[교차 원본 자원 공유](http://www.w3.org/TR/cors/) (CORS, Cross Origin Resource Sharing)는 서버 측에서 동일 원본 정책을 완화할 수 있게 해주는 W3C 표준입니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-108">[Cross Origin Resource Sharing](http://www.w3.org/TR/cors/) (CORS) is a W3C standard that allows a server to relax the same-origin policy.</span></span> <span data-ttu-id="c0c09-109">CORS를 사용하면 서버가 명시적으로 특정 교차 원본 요청만 허용하고, 다른 요청은 거부할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-109">Using CORS, a server can explicitly allow some cross-origin requests while rejecting others.</span></span> <span data-ttu-id="c0c09-110">CORS는 [JSONP](http://en.wikipedia.org/wiki/JSONP) 같은 기존의 다른 기술보다 안전하고 유연합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-110">CORS is safer and more flexible than earlier techniques such as [JSONP](http://en.wikipedia.org/wiki/JSONP).</span></span> <span data-ttu-id="c0c09-111">이 자습서에는 Web API 응용 프로그램에서 CORS를 사용 하도록 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-111">This tutorial shows how to enable CORS in your Web API application.</span></span>
>
> ## <a name="software-used-in-the-tutorial"></a><span data-ttu-id="c0c09-112">이 자습서에서 사용 되는 소프트웨어</span><span class="sxs-lookup"><span data-stu-id="c0c09-112">Software used in the tutorial</span></span>
>
> - [<span data-ttu-id="c0c09-113">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c0c09-113">Visual Studio</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - <span data-ttu-id="c0c09-114">Web API 2.2</span><span class="sxs-lookup"><span data-stu-id="c0c09-114">Web API 2.2</span></span>

## <a name="introduction"></a><span data-ttu-id="c0c09-115">소개</span><span class="sxs-lookup"><span data-stu-id="c0c09-115">Introduction</span></span>

<span data-ttu-id="c0c09-116">이 자습서에서는 ASP.NET Web API에서 CORS 지원 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-116">This tutorial demonstrates CORS support in ASP.NET Web API.</span></span> <span data-ttu-id="c0c09-117">하나의 호출된 "웹 서비스", Web API 컨트롤러를 호스트 하는 다른 호출된 "WebClient", 웹 서비스를 호출 하는 두 개의 ASP.NET 프로젝트-만들어 시작 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-117">We'll start by creating two ASP.NET projects – one called "WebService", which hosts a Web API controller, and the other called "WebClient", which calls WebService.</span></span> <span data-ttu-id="c0c09-118">두 응용 프로그램은 서로 다른 도메인에서 호스트 되므로 WebService에 WebClient에서 AJAX 요청을 한 크로스-원본 요청이입니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-118">Because the two applications are hosted at different domains, an AJAX request from WebClient to WebService is a cross-origin request.</span></span>

![](enabling-cross-origin-requests-in-web-api/_static/image1.png)

### <a name="what-is-same-origin"></a><span data-ttu-id="c0c09-119">"동일 원본"이란?</span><span class="sxs-lookup"><span data-stu-id="c0c09-119">What is "same origin"?</span></span>

<span data-ttu-id="c0c09-120">두 URL의 스키마, 호스트 및 포트가 모두 동일한 경우, 두 URL의 원본이 동일하다고 말합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-120">Two URLs have the same origin if they have identical schemes, hosts, and ports.</span></span> <span data-ttu-id="c0c09-121">([RFC 6454](http://tools.ietf.org/html/rfc6454))</span><span class="sxs-lookup"><span data-stu-id="c0c09-121">([RFC 6454](http://tools.ietf.org/html/rfc6454))</span></span>

<span data-ttu-id="c0c09-122">다음 두 URL은 동일한 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-122">These two URLs have the same origin:</span></span>

- `http://example.com/foo.html`
- `http://example.com/bar.html`

<span data-ttu-id="c0c09-123">반면, 다음 URL들은 위의 두 URL과는 다른 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-123">These URLs have different origins than the previous two:</span></span>

- <span data-ttu-id="c0c09-124">`http://example.net` -도메인이 다릅니다</span><span class="sxs-lookup"><span data-stu-id="c0c09-124">`http://example.net` - Different domain</span></span>
- <span data-ttu-id="c0c09-125">`http://example.com:9000/foo.html` -포트가 다릅니다</span><span class="sxs-lookup"><span data-stu-id="c0c09-125">`http://example.com:9000/foo.html` - Different port</span></span>
- <span data-ttu-id="c0c09-126">`https://example.com/foo.html` -스키마가 다릅니다</span><span class="sxs-lookup"><span data-stu-id="c0c09-126">`https://example.com/foo.html` - Different scheme</span></span>
- <span data-ttu-id="c0c09-127">`http://www.example.com/foo.html` -하위 도메인이 다릅니다</span><span class="sxs-lookup"><span data-stu-id="c0c09-127">`http://www.example.com/foo.html` - Different subdomain</span></span>

> [!NOTE]
> <span data-ttu-id="c0c09-128">Internet Explorer 원본을 비교 하는 경우 포트를 고려 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-128">Internet Explorer does not consider the port when comparing origins.</span></span>

## <a name="create-the-webservice-project"></a><span data-ttu-id="c0c09-129">웹 서비스 프로젝트를 만들려면</span><span class="sxs-lookup"><span data-stu-id="c0c09-129">Create the WebService project</span></span>

> [!NOTE]
> <span data-ttu-id="c0c09-130">이 섹션에서는 Web API 프로젝트를 만드는 방법을 이미 알고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-130">This section assumes you already know how to create Web API projects.</span></span> <span data-ttu-id="c0c09-131">그렇지 않은 경우 [ASP.NET Web API를 사용 하 여 시작](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-131">If not, see [Getting Started with ASP.NET Web API](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span></span>

1. <span data-ttu-id="c0c09-132">Visual Studio를 시작 하 고 새 **ASP.NET 웹 응용 프로그램 (.NET Framework)** 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-132">Start Visual Studio and create a new **ASP.NET Web Application (.NET Framework)** project.</span></span>
2. <span data-ttu-id="c0c09-133">**새 ASP.NET 웹 응용 프로그램** 대화 상자를 선택 합니다 **빈** 프로젝트 템플릿.</span><span class="sxs-lookup"><span data-stu-id="c0c09-133">In the **New ASP.NET Web Application** dialog box, select the **Empty** project template.</span></span> <span data-ttu-id="c0c09-134">아래 **폴더를 추가 하 고 핵심에 대 한 참조**를 선택 합니다 **Web API** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-134">Under **Add folders and core references for**, select the **Web API** checkbox.</span></span>

   ![Visual Studio에서 새 ASP.NET 프로젝트 대화 상자](enabling-cross-origin-requests-in-web-api/_static/new-web-app-dialog.png)

3. <span data-ttu-id="c0c09-136">명명 된 Web API 컨트롤러 추가 `TestController` 다음 코드를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="c0c09-136">Add a Web API controller named `TestController` with the following code:</span></span>

   [!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample1.cs)]

4. <span data-ttu-id="c0c09-137">응용 프로그램을 로컬로 실행할 수도 있고 Azure에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-137">You can run the application locally or deploy to Azure.</span></span> <span data-ttu-id="c0c09-138">(이 자습서의 스크린샷에서, 앱 배포에 Azure App Service Web Apps입니다.) Web API가 작동 하는지 확인 하려면로 이동 `http://hostname/api/test/`여기서 *호스트 이름* 응용 프로그램을 배포한 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-138">(For the screenshots in this tutorial, the app deploys to Azure App Service Web Apps.) To verify that the web API is working, navigate to `http://hostname/api/test/`, where *hostname* is the domain where you deployed the application.</span></span> <span data-ttu-id="c0c09-139">응답 텍스트가 &quot;가져오기: 테스트 메시지&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-139">You should see the response text, &quot;GET: Test Message&quot;.</span></span>

   ![웹 브라우저 보여 주는 테스트 메시지](enabling-cross-origin-requests-in-web-api/_static/image4.png)

## <a name="create-the-webclient-project"></a><span data-ttu-id="c0c09-141">WebClient 프로젝트를 만들려면</span><span class="sxs-lookup"><span data-stu-id="c0c09-141">Create the WebClient project</span></span>

1. <span data-ttu-id="c0c09-142">만들면 **ASP.NET 웹 응용 프로그램 (.NET Framework)** 프로젝트를 마우스 합니다 **MVC** 프로젝트 템플릿.</span><span class="sxs-lookup"><span data-stu-id="c0c09-142">Create another **ASP.NET Web Application (.NET Framework)** project and select the **MVC** project template.</span></span> <span data-ttu-id="c0c09-143">필요에 따라 선택할 **인증 변경** > **인증 안 함**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-143">Optionally, select **Change Authentication** > **No Authentication**.</span></span> <span data-ttu-id="c0c09-144">이 자습서에 대 한 인증이 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-144">You don't need authentication for this tutorial.</span></span>

   ![Visual Studio에서 새 ASP.NET 프로젝트 대화 상자에서 MVC 템플릿](enabling-cross-origin-requests-in-web-api/_static/new-web-app-dialog-mvc.png)

2. <span data-ttu-id="c0c09-146">**솔루션 탐색기**, 파일을 열고 *Views/Home/Index.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-146">In **Solution Explorer**, open the file *Views/Home/Index.cshtml*.</span></span> <span data-ttu-id="c0c09-147">이 파일의 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-147">Replace the code in this file with the following:</span></span>

   [!code-cshtml[Main](enabling-cross-origin-requests-in-web-api/samples/sample2.cshtml?highlight=13)]

   <span data-ttu-id="c0c09-148">에 대 한 합니다 *serviceUrl* 변수를 웹 서비스 응용 프로그램의 URI를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-148">For the *serviceUrl* variable, use the URI of the WebService app.</span></span>

3. <span data-ttu-id="c0c09-149">WebClient 앱을 로컬로 실행 하거나 다른 웹 사이트에 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-149">Run the WebClient app locally or publish it to another website.</span></span>

<span data-ttu-id="c0c09-150">"Try It" 단추를 클릭 하면 AJAX 요청에 나열 된 HTTP 메서드를 사용 하 여 웹 서비스 앱에 전송 됩니다 (GET, POST 또는 PUT) 드롭다운 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-150">When you click the "Try It" button, an AJAX request is submitted to the WebService app using the HTTP method listed in the dropdown box (GET, POST, or PUT).</span></span> <span data-ttu-id="c0c09-151">이렇게 하면 다양 한 원본 간 요청을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-151">This lets you examine different cross-origin requests.</span></span> <span data-ttu-id="c0c09-152">현재 웹 서비스 응용 프로그램 단추를 클릭 하면 오류가 발생 하므로 CORS를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-152">Currently, the WebService app does not support CORS, so if you click the button you'll get an error.</span></span>

![브라우저에서 오류 '평가판 사용해 보기'](enabling-cross-origin-requests-in-web-api/_static/image7.png)

> [!NOTE]
> <span data-ttu-id="c0c09-154">와 같은 도구에서 HTTP 트래픽을 시청 하는 경우 [Fiddler](https://www.telerik.com/fiddler), 브라우저는 GET 요청을 보내지 및 요청이 성공 하면 있지만 AJAX 호출이 오류를 반환 합니다. 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-154">If you watch the HTTP traffic in a tool like [Fiddler](https://www.telerik.com/fiddler), you'll see that the browser does send the GET request, and the request succeeds, but the AJAX call returns an error.</span></span> <span data-ttu-id="c0c09-155">동일 원본 정책에서 브라우저 해도 알아야 할 것 *보내는* 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-155">It's important to understand that same-origin policy does not prevent the browser from *sending* the request.</span></span> <span data-ttu-id="c0c09-156">대신 보지 못하도록 응용 프로그램을 방지 합니다 *응답*합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-156">Instead, it prevents the application from seeing the *response*.</span></span>

![웹 요청을 보여 주는 fiddler 웹 디버거](enabling-cross-origin-requests-in-web-api/_static/image8.png)

## <a name="enable-cors"></a><span data-ttu-id="c0c09-158">CORS를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="c0c09-158">Enable CORS</span></span>

<span data-ttu-id="c0c09-159">이제 웹 서비스 앱에서 CORS를 사용 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-159">Now let's enable CORS in the WebService app.</span></span> <span data-ttu-id="c0c09-160">첫째, CORS NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-160">First, add the CORS NuGet package.</span></span> <span data-ttu-id="c0c09-161">Visual Studio에서에서 합니다 **도구** 메뉴에서 **NuGet 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-161">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="c0c09-162">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-162">In the Package Manager Console window, type the following command:</span></span>

[!code-powershell[Main](enabling-cross-origin-requests-in-web-api/samples/sample3.ps1)]

<span data-ttu-id="c0c09-163">이 명령은 최신 패키지를 설치 하 고 core Web API 라이브러리를 포함 한 모든 종속성을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-163">This command installs the latest package and updates all dependencies, including the core Web API libraries.</span></span> <span data-ttu-id="c0c09-164">사용 된 `-Version` 특정 버전을 대상으로 하는 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-164">Use the `-Version` flag to target a specific version.</span></span> <span data-ttu-id="c0c09-165">CORS 패키지에는 Web API 2.0 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-165">The CORS package requires Web API 2.0 or later.</span></span>

<span data-ttu-id="c0c09-166">파일을 엽니다 *앱\_Start/WebApiConfig.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-166">Open the file *App\_Start/WebApiConfig.cs*.</span></span> <span data-ttu-id="c0c09-167">다음 코드를 추가 합니다 **WebApiConfig.Register** 메서드:</span><span class="sxs-lookup"><span data-stu-id="c0c09-167">Add the following code to the **WebApiConfig.Register** method:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample4.cs?highlight=9)]

<span data-ttu-id="c0c09-168">다음을 추가 합니다 **[EnableCors]** 특성을 `TestController` 클래스:</span><span class="sxs-lookup"><span data-stu-id="c0c09-168">Next, add the **[EnableCors]** attribute to the `TestController` class:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample5.cs?highlight=3,7)]

<span data-ttu-id="c0c09-169">에 대 한 합니다 *원본을* 매개 변수를 WebClient 응용 프로그램을 배포한 URI를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-169">For the *origins* parameter, use the URI where you deployed the WebClient application.</span></span> <span data-ttu-id="c0c09-170">따라서 크로스-원본 요청에서 WebClient는 여전히 다른 모든 도메인 간 요청을 허용 하는 동안.</span><span class="sxs-lookup"><span data-stu-id="c0c09-170">This allows cross-origin requests from WebClient, while still disallowing all other cross-domain requests.</span></span> <span data-ttu-id="c0c09-171">나중에 대 한 매개 변수를 설명할 **[EnableCors]** 자세히입니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-171">Later, I'll describe the parameters for **[EnableCors]** in more detail.</span></span>

<span data-ttu-id="c0c09-172">끝에 슬래시를 포함 하지 않는 합니다 *원본을* URL입니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-172">Do not include a forward slash at the end of the *origins* URL.</span></span>

<span data-ttu-id="c0c09-173">업데이트 된 웹 서비스 응용 프로그램을 다시 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-173">Redeploy the updated WebService application.</span></span> <span data-ttu-id="c0c09-174">WebClient를 업데이트할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-174">You don't need to update WebClient.</span></span> <span data-ttu-id="c0c09-175">이제 WebClient에서 AJAX 요청이 성공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-175">Now the AJAX request from WebClient should succeed.</span></span> <span data-ttu-id="c0c09-176">GET, PUT 및 POST 메서드가 모두 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-176">The GET, PUT, and POST methods are all allowed.</span></span>

![웹 브라우저 표시 성공적인 테스트 메시지](enabling-cross-origin-requests-in-web-api/_static/image9.png)

## <a name="how-cors-works"></a><span data-ttu-id="c0c09-178">CORS의 작동 원리</span><span class="sxs-lookup"><span data-stu-id="c0c09-178">How CORS Works</span></span>

<span data-ttu-id="c0c09-179">이 섹션에서는 HTTP 메시지 수준에서 CORS 요청에서 어떻게 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-179">This section describes what happens in a CORS request, at the level of the HTTP messages.</span></span> <span data-ttu-id="c0c09-180">구성할 수 있도록 CORS의 작동 방식을 이해 해야 합니다 **[EnableCors]** 올바르게 특성 및 예상 대로 작동 되지 않으면 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-180">It's important to understand how CORS works, so that you can configure the **[EnableCors]** attribute correctly and troubleshoot if things don't work as you expect.</span></span>

<span data-ttu-id="c0c09-181">CORS 명세에서는 교차 원본 요청을 활성화시키기 위한 용도로 몇 가지 새로운 HTTP 헤더들이 도입되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-181">The CORS specification introduces several new HTTP headers that enable cross-origin requests.</span></span> <span data-ttu-id="c0c09-182">브라우저에서 CORS를 지 원하는 경우 크로스-원본 요청에 대해 자동으로 이러한 헤더 설정 모든 JavaScript 코드에 특별 한 작업을 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-182">If a browser supports CORS, it sets these headers automatically for cross-origin requests; you don't need to do anything special in your JavaScript code.</span></span>

<span data-ttu-id="c0c09-183">크로스-원본 요청 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-183">Here is an example of a cross-origin request.</span></span> <span data-ttu-id="c0c09-184">"원본" 헤더를 요청 하는 사이트의 도메인을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-184">The "Origin" header gives the domain of the site that is making the request.</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample6.cmd?highlight=5)]

<span data-ttu-id="c0c09-185">서버 요청을 허용 하면, 액세스 제어-허용-원본 헤더를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-185">If the server allows the request, it sets the Access-Control-Allow-Origin header.</span></span> <span data-ttu-id="c0c09-186">이 헤더의 값 또는 원본 헤더와 일치 하는 와일드 카드 값 "\*", 즉 모든 원본을 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-186">The value of this header either matches the Origin header, or is the wildcard value "\*", meaning that any origin is allowed.</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample7.cmd?highlight=5)]

<span data-ttu-id="c0c09-187">응답에서 액세스 제어-허용-원본 헤더를 포함 하지 않습니다, AJAX 요청이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-187">If the response does not include the Access-Control-Allow-Origin header, the AJAX request fails.</span></span> <span data-ttu-id="c0c09-188">특히 브라우저 요청을 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-188">Specifically, the browser disallows the request.</span></span> <span data-ttu-id="c0c09-189">서버 응답에 성공 하면 반환 하는 경우에 브라우저 해도 응답 클라이언트 응용 프로그램에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-189">Even if the server returns a successful response, the browser does not make the response available to the client application.</span></span>

<span data-ttu-id="c0c09-190">**실행 전 요청**</span><span class="sxs-lookup"><span data-stu-id="c0c09-190">**Preflight Requests**</span></span>

<span data-ttu-id="c0c09-191">브라우저는 일부 CORS 요청에 대 한 리소스에 대 한 실제 요청을 보내기 전에 "실행 전 요청을" 라는 추가 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-191">For some CORS requests, the browser sends an additional request, called a "preflight request", before it sends the actual request for the resource.</span></span>

<span data-ttu-id="c0c09-192">다음 조건이 true 인 경우 브라우저가 실행 전 요청을 건너뛸 수 있습니다.:</span><span class="sxs-lookup"><span data-stu-id="c0c09-192">The browser can skip the preflight request if the following conditions are true:</span></span>

- <span data-ttu-id="c0c09-193">요청 메서드는 GET, HEAD 또는 POST *및*</span><span class="sxs-lookup"><span data-stu-id="c0c09-193">The request method is GET, HEAD, or POST, *and*</span></span>
- <span data-ttu-id="c0c09-194">응용 프로그램 동의 수용-언어 Content-language 이외의 모든 요청 헤더를 설정 하지 않습니다 Content-type, 또는 마지막-이벤트-ID *및*</span><span class="sxs-lookup"><span data-stu-id="c0c09-194">The application does not set any request headers other than Accept, Accept-Language, Content-Language, Content-Type, or Last-Event-ID, *and*</span></span>
- <span data-ttu-id="c0c09-195">Content-type 헤더 (하는 경우 설정) 다음 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-195">The Content-Type header (if set) is one of the following:</span></span>

    - <span data-ttu-id="c0c09-196">application/x-www-form-urlencoded</span><span class="sxs-lookup"><span data-stu-id="c0c09-196">application/x-www-form-urlencoded</span></span>
    - <span data-ttu-id="c0c09-197">다중 파트/폼 데이터</span><span class="sxs-lookup"><span data-stu-id="c0c09-197">multipart/form-data</span></span>
    - <span data-ttu-id="c0c09-198">텍스트/일반</span><span class="sxs-lookup"><span data-stu-id="c0c09-198">text/plain</span></span>

<span data-ttu-id="c0c09-199">요청 헤더에 대 한 규칙을 호출 하 여 응용 프로그램을 설정 하는 헤더 적용할 **setRequestHeader** 에 **XMLHttpRequest** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-199">The rule about request headers applies to headers that the application sets by calling **setRequestHeader** on the **XMLHttpRequest** object.</span></span> <span data-ttu-id="c0c09-200">(CORS 사양 이러한 "작성자 요청 헤더"를 호출 합니다.) 헤더에 규칙이 적용 되지 않습니다 합니다 *브라우저* 사용자 에이전트, 호스트 또는 콘텐츠-길이 같은 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-200">(The CORS specification calls these "author request headers".) The rule does not apply to headers the *browser* can set, such as User-Agent, Host, or Content-Length.</span></span>

<span data-ttu-id="c0c09-201">실행 전 요청의 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-201">Here is an example of a preflight request:</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample8.cmd?highlight=4-5)]

<span data-ttu-id="c0c09-202">HTTP OPTIONS 메서드를 사용 하는 사전 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-202">The pre-flight request uses the HTTP OPTIONS method.</span></span> <span data-ttu-id="c0c09-203">두 가지 특수 헤더를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-203">It includes two special headers:</span></span>

- <span data-ttu-id="c0c09-204">액세스-컨트롤-요청-방법: 실제 요청에 사용 될 HTTP 메서드.</span><span class="sxs-lookup"><span data-stu-id="c0c09-204">Access-Control-Request-Method: The HTTP method that will be used for the actual request.</span></span>
- <span data-ttu-id="c0c09-205">Access-Control-Request-Headers: 요청 헤더의 목록을 하는 *응용 프로그램* 실제 요청을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-205">Access-Control-Request-Headers: A list of request headers that the *application* set on the actual request.</span></span> <span data-ttu-id="c0c09-206">(마찬가지로이 브라우저 설정 하는 헤더)</span><span class="sxs-lookup"><span data-stu-id="c0c09-206">(Again, this does not include headers that the browser sets.)</span></span>

<span data-ttu-id="c0c09-207">예제 응답, 서버 요청을 허용 하는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-207">Here is an example response, assuming that the server allows the request:</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample9.cmd?highlight=6-7)]

<span data-ttu-id="c0c09-208">허용 된 메서드를 나열 하는 액세스-컨트롤-허용-메서드 헤더 및 필요에 따라 허용 되는 헤더를 나열 하는 액세스 제어-허용-헤더 헤더를 응답에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-208">The response includes an Access-Control-Allow-Methods header that lists the allowed methods, and optionally an Access-Control-Allow-Headers header, which lists the allowed headers.</span></span> <span data-ttu-id="c0c09-209">실행 전 요청이 성공 하면 브라우저 앞에서 설명한 대로 실제 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-209">If the preflight request succeeds, the browser sends the actual request, as described earlier.</span></span>

<span data-ttu-id="c0c09-210">실행 전 OPTIONS 요청을 사용 하 여 끝점을 테스트 하려면 일반적으로 사용 되는 도구 (예를 들어 [Fiddler](https://www.telerik.com/fiddler) 하 고 [Postman](https://www.getpostman.com/)) 기본적으로 필수 옵션 헤더를 보내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-210">Tools commonly used to test endpoints with preflight OPTIONS requests (for example, [Fiddler](https://www.telerik.com/fiddler) and [Postman](https://www.getpostman.com/)) don't send the required OPTIONS headers by default.</span></span> <span data-ttu-id="c0c09-211">있는지 확인 합니다 `Access-Control-Request-Method` 및 `Access-Control-Request-Headers` 헤더 요청과 함께 전송 되 고 옵션 헤더 IIS 통해 앱에 도달 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-211">Confirm that the `Access-Control-Request-Method` and `Access-Control-Request-Headers` headers are sent with the request and that OPTIONS headers reach the app through IIS.</span></span>

<span data-ttu-id="c0c09-212">ASP.NET 앱을 받고 옵션 요청을 처리 하도록 IIS를 구성 하려면 앱의 다음 구성을 추가 *web.config* 파일을 `<system.webServer><handlers>` 섹션:</span><span class="sxs-lookup"><span data-stu-id="c0c09-212">To configure IIS to allow an ASP.NET app to receive and handle OPTION requests, add the following configuration to the app's *web.config* file in the `<system.webServer><handlers>` section:</span></span>

```xml
<system.webServer>
  <handlers>
    <remove name="ExtensionlessUrlHandler-Integrated-4.0" />
    <remove name="OPTIONSVerbHandler" />
    <add name="ExtensionlessUrlHandler-Integrated-4.0" path="*." verb="*" type="System.Web.Handlers.TransferRequestHandler" preCondition="integratedMode,runtimeVersionv4.0" />
  </handlers>
</system.webServer>
```

<span data-ttu-id="c0c09-213">제거 `OPTIONSVerbHandler` IIS OPTIONS 요청을 처리 하는 것을 금지 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-213">The removal of `OPTIONSVerbHandler` prevents IIS from handling OPTIONS requests.</span></span> <span data-ttu-id="c0c09-214">대체 `ExtensionlessUrlHandler-Integrated-4.0` OPTIONS 요청 기본 모듈 등록 확장명 없는 Url 사용 하 여 GET, HEAD, POST 및 디버그 요청만 허용 하기 때문에 앱을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-214">The replacement of `ExtensionlessUrlHandler-Integrated-4.0` allows OPTIONS requests to reach the app because the default module registration only allows GET, HEAD, POST, and DEBUG requests with extensionless URLs.</span></span>

## <a name="scope-rules-for-enablecors"></a><span data-ttu-id="c0c09-215">[EnableCors]에 대 한 범위 규칙</span><span class="sxs-lookup"><span data-stu-id="c0c09-215">Scope Rules for [EnableCors]</span></span>

<span data-ttu-id="c0c09-216">응용 프로그램에서 작업당: 컨트롤러 당 또는 모든 Web API 컨트롤러에 대 한 전역적으로 CORS를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-216">You can enable CORS per action, per controller, or globally for all Web API controllers in your application.</span></span>

<span data-ttu-id="c0c09-217">**작업당**</span><span class="sxs-lookup"><span data-stu-id="c0c09-217">**Per Action**</span></span>

<span data-ttu-id="c0c09-218">단일 작업에 대 한 CORS를 사용 하도록 설정 합니다 **[EnableCors]** 동작 메서드에 대 한 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-218">To enable CORS for a single action, set the **[EnableCors]** attribute on the action method.</span></span> <span data-ttu-id="c0c09-219">다음 예제에서는 CORS는 `GetItem` 방법만 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-219">The following example enables CORS for the `GetItem` method only.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample10.cs)]

<span data-ttu-id="c0c09-220">**컨트롤러당**</span><span class="sxs-lookup"><span data-stu-id="c0c09-220">**Per Controller**</span></span>

<span data-ttu-id="c0c09-221">설정 하는 경우 **[EnableCors]** 컨트롤러 클래스에 대해 컨트롤러에서 모든 작업에 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-221">If you set **[EnableCors]** on the controller class, it applies to all the actions on the controller.</span></span> <span data-ttu-id="c0c09-222">CORS를 사용 하지 않으려면 작업을 추가 합니다 **[DisableCors]** 특성 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-222">To disable CORS for an action, add the **[DisableCors]** attribute to the action.</span></span> <span data-ttu-id="c0c09-223">다음 예제에서는 제외한 모든 방법에 대 한 CORS를 사용 하면 `PutItem`합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-223">The following example enables CORS for every method except `PutItem`.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample11.cs)]

<span data-ttu-id="c0c09-224">**전 세계**</span><span class="sxs-lookup"><span data-stu-id="c0c09-224">**Globally**</span></span>

<span data-ttu-id="c0c09-225">CORS를 사용 하도록 응용 프로그램에서 모든 Web API 컨트롤러에 대 한 전달를 **EnableCorsAttribute** 인스턴스를 **EnableCors** 메서드:</span><span class="sxs-lookup"><span data-stu-id="c0c09-225">To enable CORS for all Web API controllers in your application, pass an **EnableCorsAttribute** instance to the **EnableCors** method:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample12.cs)]

<span data-ttu-id="c0c09-226">둘 이상의 범위에서 특성을 설정 하는 경우 우선 순위가 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-226">If you set the attribute at more than one scope, the order of precedence is:</span></span>

1. <span data-ttu-id="c0c09-227">작업</span><span class="sxs-lookup"><span data-stu-id="c0c09-227">Action</span></span>
2. <span data-ttu-id="c0c09-228">컨트롤러</span><span class="sxs-lookup"><span data-stu-id="c0c09-228">Controller</span></span>
3. <span data-ttu-id="c0c09-229">Global</span><span class="sxs-lookup"><span data-stu-id="c0c09-229">Global</span></span>

## <a name="set-the-allowed-origins"></a><span data-ttu-id="c0c09-230">허용되는 원본 설정하기</span><span class="sxs-lookup"><span data-stu-id="c0c09-230">Set the allowed origins</span></span>

<span data-ttu-id="c0c09-231">*원본을* 의 매개 변수를 **[EnableCors]** 특성 리소스에 액세스할 수 있는 원본 허용 되는지 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-231">The *origins* parameter of the **[EnableCors]** attribute specifies which origins are allowed to access the resource.</span></span> <span data-ttu-id="c0c09-232">값은 허용 되는 원본의 쉼표로 구분 된 목록.</span><span class="sxs-lookup"><span data-stu-id="c0c09-232">The value is a comma-separated list of the allowed origins.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample13.cs)]

<span data-ttu-id="c0c09-233">와일드 카드 값을 사용할 수도 있습니다 "\*" 요청을 모든 원본을 허용 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-233">You can also use the wildcard value "\*" to allow requests from any origins.</span></span>

<span data-ttu-id="c0c09-234">모든 원본의 요청을 허용하기 전에 신중히 고민하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-234">Consider carefully before allowing requests from any origin.</span></span> <span data-ttu-id="c0c09-235">말 그대로 모든 웹 사이트에 web API에 대 한 AJAX 호출을 설정할 수 있는지를 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-235">It means that literally any website can make AJAX calls to your web API.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample14.cs)]

## <a name="set-the-allowed-http-methods"></a><span data-ttu-id="c0c09-236">허용되는 HTTP 메서드 설정하기</span><span class="sxs-lookup"><span data-stu-id="c0c09-236">Set the allowed HTTP methods</span></span>

<span data-ttu-id="c0c09-237">합니다 *메서드* 의 매개 변수를 **[EnableCors]** 리소스에 액세스할 수 있는 HTTP 메서드 특성 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-237">The *methods* parameter of the **[EnableCors]** attribute specifies which HTTP methods are allowed to access the resource.</span></span> <span data-ttu-id="c0c09-238">모든 메서드를 허용 하려면 와일드 카드 값을 사용 하 여 "\*"입니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-238">To allow all methods, use the wildcard value "\*".</span></span> <span data-ttu-id="c0c09-239">다음 예제에서는 GET 및 POST 요청만 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-239">The following example allows only GET and POST requests.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample15.cs)]

## <a name="set-the-allowed-request-headers"></a><span data-ttu-id="c0c09-240">허용되는 요청 헤더 설정하기</span><span class="sxs-lookup"><span data-stu-id="c0c09-240">Set the allowed request headers</span></span>

<span data-ttu-id="c0c09-241">이 문서에서는 실행 전 요청을 응용 프로그램에 의해 설정 된 HTTP 헤더를 나열 하는 액세스 제어-요청 헤더 헤더에 포함 될 수 있습니다 이전 하는 방법을 설명 (소위 "요청 헤더 author").</span><span class="sxs-lookup"><span data-stu-id="c0c09-241">This article described earlier how a preflight request might include an Access-Control-Request-Headers header, listing the HTTP headers set by the application (the so-called "author request headers").</span></span> <span data-ttu-id="c0c09-242">합니다 *헤더* 의 매개 변수를 **[EnableCors]** 특성은 만든 요청 헤더를 허용 하도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-242">The *headers* parameter of the **[EnableCors]** attribute specifies which author request headers are allowed.</span></span> <span data-ttu-id="c0c09-243">모든 헤더를 허용 하려면 설정 *헤더* 에 "\*"입니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-243">To allow any headers, set *headers* to "\*".</span></span> <span data-ttu-id="c0c09-244">허용 목록에 추가할 특정 헤더를 설정 *헤더* 허용 되는 헤더의 쉼표로 구분 된 목록에:</span><span class="sxs-lookup"><span data-stu-id="c0c09-244">To whitelist specific headers, set *headers* to a comma-separated list of the allowed headers:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample16.cs)]

<span data-ttu-id="c0c09-245">그러나 브라우저에 대 한 액세스 제어-요청 헤더는 설정 하는 방법을 완전히 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-245">However, browsers are not entirely consistent in how they set Access-Control-Request-Headers.</span></span> <span data-ttu-id="c0c09-246">예를 들어, Chrome는 현재 "원본"을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-246">For example, Chrome currently includes "origin".</span></span> <span data-ttu-id="c0c09-247">FireFox 응용 프로그램이 스크립트를 설정 하는 경우에 "Accept"와 같은 표준 헤더를 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-247">FireFox does not include standard headers such as "Accept", even when the application sets them in script.</span></span>

<span data-ttu-id="c0c09-248">설정 하는 경우 *헤더* 이외의 값으로 "\*"를 포함 해야 적어도 "수락", "콘텐츠-유형" 및 "원본"을 지원 하려는 모든 사용자 지정 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-248">If you set *headers* to anything other than "\*", you should include at least "accept", "content-type", and "origin", plus any custom headers that you want to support.</span></span>

## <a name="set-the-allowed-response-headers"></a><span data-ttu-id="c0c09-249">허용 되는 응답 헤더 설정</span><span class="sxs-lookup"><span data-stu-id="c0c09-249">Set the allowed response headers</span></span>

<span data-ttu-id="c0c09-250">기본적으로 브라우저 노출 하지 않습니다 모든 응용 프로그램에 대 한 응답 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-250">By default, the browser does not expose all of the response headers to the application.</span></span> <span data-ttu-id="c0c09-251">기본적으로 사용 가능한 응답 헤더들은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-251">The response headers that are available by default are:</span></span>

- <span data-ttu-id="c0c09-252">Cache-Control</span><span class="sxs-lookup"><span data-stu-id="c0c09-252">Cache-Control</span></span>
- <span data-ttu-id="c0c09-253">콘텐츠 언어</span><span class="sxs-lookup"><span data-stu-id="c0c09-253">Content-Language</span></span>
- <span data-ttu-id="c0c09-254">콘텐츠 형식</span><span class="sxs-lookup"><span data-stu-id="c0c09-254">Content-Type</span></span>
- <span data-ttu-id="c0c09-255">Expires</span><span class="sxs-lookup"><span data-stu-id="c0c09-255">Expires</span></span>
- <span data-ttu-id="c0c09-256">Last-Modified</span><span class="sxs-lookup"><span data-stu-id="c0c09-256">Last-Modified</span></span>
- <span data-ttu-id="c0c09-257">Pragma</span><span class="sxs-lookup"><span data-stu-id="c0c09-257">Pragma</span></span>

<span data-ttu-id="c0c09-258">CORS 명세에서는 이 헤더들을 [단순 응답 헤더(Simple Response Header)](https://dvcs.w3.org/hg/cors/raw-file/tip/Overview.html#simple-response-header) 라고 부릅니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-258">The CORS spec calls these [simple response headers](https://dvcs.w3.org/hg/cors/raw-file/tip/Overview.html#simple-response-header).</span></span> <span data-ttu-id="c0c09-259">다른 헤더에서 응용 프로그램에 사용할 수 있도록 설정 합니다 *exposedHeaders* 의 매개 변수 **[EnableCors]** 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-259">To make other headers available to the application, set the *exposedHeaders* parameter of **[EnableCors]**.</span></span>

<span data-ttu-id="c0c09-260">다음 예제에서는 컨트롤러의에서 `Get` 메서드 ' X 사용자 지정 헤더 ' 라는 사용자 지정 헤더를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-260">In the following example, the controller's `Get` method sets a custom header named ‘X-Custom-Header'.</span></span> <span data-ttu-id="c0c09-261">기본적으로 브라우저는 크로스-원본 요청에서이 헤더를 노출 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-261">By default, the browser will not expose this header in a cross-origin request.</span></span> <span data-ttu-id="c0c09-262">헤더에서 사용할 수 있도록 하려면에 ' X 사용자 지정 헤더 '를 포함 *exposedHeaders*합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-262">To make the header available, include ‘X-Custom-Header' in *exposedHeaders*.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample17.cs)]

## <a name="pass-credentials-in-cross-origin-requests"></a><span data-ttu-id="c0c09-263">크로스-원본 요청에 자격 증명을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-263">Pass credentials in cross-origin requests</span></span>

<span data-ttu-id="c0c09-264">CORS 요청에서 자격 증명(Credentials)은 특별한 처리를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-264">Credentials require special handling in a CORS request.</span></span> <span data-ttu-id="c0c09-265">기본적으로 브라우저는 크로스-원본 요청을 사용 하 여 자격 증명을 보내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-265">By default, the browser does not send any credentials with a cross-origin request.</span></span> <span data-ttu-id="c0c09-266">여기에서 말하는 자격 증명에는 쿠키뿐만 아니라 HTTP 인증 스킴도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-266">Credentials include cookies as well as HTTP authentication schemes.</span></span> <span data-ttu-id="c0c09-267">크로스-원본 요청을 사용 하 여 자격 증명을 보내려면 클라이언트 설정 해야 합니다 **XMLHttpRequest.withCredentials** true로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-267">To send credentials with a cross-origin request, the client must set **XMLHttpRequest.withCredentials** to true.</span></span>

<span data-ttu-id="c0c09-268">사용 하 여 **XMLHttpRequest** 직접.</span><span class="sxs-lookup"><span data-stu-id="c0c09-268">Using **XMLHttpRequest** directly:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample18.cs)]

<span data-ttu-id="c0c09-269">jQuery를 사용할 경우:</span><span class="sxs-lookup"><span data-stu-id="c0c09-269">In jQuery:</span></span>

[!code-javascript[Main](enabling-cross-origin-requests-in-web-api/samples/sample19.js)]

<span data-ttu-id="c0c09-270">또한 서버에서도 자격 증명을 허용해야만 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-270">In addition, the server must allow the credentials.</span></span> <span data-ttu-id="c0c09-271">Web API에서 크로스-원본 자격 증명을 허용 하려면 설정 합니다 **SupportsCredentials** 속성에서 true로 합니다 **[EnableCors]** 특성:</span><span class="sxs-lookup"><span data-stu-id="c0c09-271">To allow cross-origin credentials in Web API, set the **SupportsCredentials** property to true on the **[EnableCors]** attribute:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample20.cs)]

<span data-ttu-id="c0c09-272">이 속성이 true 이면 HTTP 응답에 대 한 액세스 제어-허용-자격 증명 헤더가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-272">If this property is true, the HTTP response will include an Access-Control-Allow-Credentials header.</span></span> <span data-ttu-id="c0c09-273">이 헤더는 서버를 크로스-원본 요청에 대 한 자격 증명을 허용 하는지 브라우저를 알립니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-273">This header tells the browser that the server allows credentials for a cross-origin request.</span></span>

<span data-ttu-id="c0c09-274">브라우저에서 자격 증명을 보내는 응답을 유효한 액세스-컨트롤--자격 증명 허용 헤더를 포함 하지 않습니다 하지만 브라우저 응용 프로그램에 대 한 응답을 노출 하지 않습니다 고 AJAX 요청이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-274">If the browser sends credentials, but the response does not include a valid Access-Control-Allow-Credentials header, the browser will not expose the response to the application, and the AJAX request fails.</span></span>

<span data-ttu-id="c0c09-275">설정에 대 한 주의 **SupportsCredentials** 다른 도메인에서 웹 사이트 사용자가 인식 하지 않고 사용자 대신 Web API에는 로그인 한 사용자의 자격 증명에 보낼 수 있기 때문에 true로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-275">Be careful about setting **SupportsCredentials** to true, because it means a website at another domain can send a logged-in user's credentials to your Web API on the user's behalf, without the user being aware.</span></span> <span data-ttu-id="c0c09-276">CORS 사양에는 또한 해당 설정 상태 *원본을* 에 &quot; \* &quot; 올바르지 경우 **SupportsCredentials** 그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-276">The CORS spec also states that setting *origins* to &quot;\*&quot; is invalid if **SupportsCredentials** is true.</span></span>

## <a name="custom-cors-policy-providers"></a><span data-ttu-id="c0c09-277">사용자 지정 CORS 정책 공급자</span><span class="sxs-lookup"><span data-stu-id="c0c09-277">Custom CORS policy providers</span></span>

<span data-ttu-id="c0c09-278">합니다 **[EnableCors]** 구현 특성을 **ICorsPolicyProvider** 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-278">The **[EnableCors]** attribute implements the **ICorsPolicyProvider** interface.</span></span> <span data-ttu-id="c0c09-279">파생 되는 클래스를 만들어 사용자 지정 구현을 제공할 수 있습니다 **특성** 구현 **ICorsProlicyProvider**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-279">You can provide your own implementation by creating a class that derives from **Attribute** and implements **ICorsProlicyProvider**.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample21.cs)]

<span data-ttu-id="c0c09-280">이제 배치 하는 위치 특성을 적용할 수 있습니다 **[EnableCors]** 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-280">Now you can apply the attribute any place that you would put **[EnableCors]**.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample22.cs)]

<span data-ttu-id="c0c09-281">예를 들어, 사용자 지정 CORS 정책 공급자를 구성 파일에서 설정을 읽을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-281">For example, a custom CORS policy provider could read the settings from a configuration file.</span></span>

<span data-ttu-id="c0c09-282">특성을 사용 하는 대신,으로 등록할 수 있습니다는 **ICorsPolicyProviderFactory** 개체를 만드는 **ICorsPolicyProvider** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-282">As an alternative to using attributes, you can register an **ICorsPolicyProviderFactory** object that creates **ICorsPolicyProvider** objects.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample23.cs)]

<span data-ttu-id="c0c09-283">설정 하는 **ICorsPolicyProviderFactory**를 호출 합니다 **SetCorsPolicyProviderFactory** 같이 시작 시 확장 메서드:</span><span class="sxs-lookup"><span data-stu-id="c0c09-283">To set the **ICorsPolicyProviderFactory**, call the **SetCorsPolicyProviderFactory** extension method at startup, as follows:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample24.cs)]

## <a name="browser-support"></a><span data-ttu-id="c0c09-284">브라우저 지원</span><span class="sxs-lookup"><span data-stu-id="c0c09-284">Browser support</span></span>

<span data-ttu-id="c0c09-285">Web API CORS 패키지에는 서버 쪽 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-285">The Web API CORS package is a server-side technology.</span></span> <span data-ttu-id="c0c09-286">사용자의 브라우저는 또한 CORS를 지원 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-286">The user's browser also needs to support CORS.</span></span> <span data-ttu-id="c0c09-287">다행 스럽게도 모든 주요 브라우저의 현재 버전 포함 [CORS에 대 한 지원](http://caniuse.com/cors)합니다.</span><span class="sxs-lookup"><span data-stu-id="c0c09-287">Fortunately, the current versions of all major browsers include [support for CORS](http://caniuse.com/cors).</span></span>
