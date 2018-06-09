---
uid: web-api/overview/security/enabling-cross-origin-requests-in-web-api
title: ASP.NET Web API 2의에서 교차 원본 요청을 사용 하도록 설정 | Microsoft Docs
author: MikeWasson
description: ASP.NET Web API에서 크로스-원본 자원 공유 (CORS)를 지 원하는 방법을 보여 줍니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/15/2014
ms.topic: article
ms.assetid: 9b265a5a-6a70-4a82-adce-2d7c56ae8bdd
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/security/enabling-cross-origin-requests-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 453ad29ff4f10f9660f3aa8bab358519b4cfd48b
ms.sourcegitcommit: 6784510cfb589308c3875ccb5113eb31031766b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2018
ms.locfileid: "26508382"
---
<a name="enabling-cross-origin-requests-in-aspnet-web-api-2"></a><span data-ttu-id="d4256-103">ASP.NET Web API 2의에서 교차 원본 요청을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="d4256-103">Enabling Cross-Origin Requests in ASP.NET Web API 2</span></span>
====================
<span data-ttu-id="d4256-104">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="d4256-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="d4256-105">브라우저의 보안 기능은 웹 페이지에서 다른 도메인으로 AJAX 요청을 전송하는 것을 막습니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-105">Browser security prevents a web page from making AJAX requests to another domain.</span></span> <span data-ttu-id="d4256-106">이 제약 사항을 *동일 원본 정책(Same-Origin Policy)* 이라고 부르며, 악의적인 사이트가 다른 사이트의 민감한 데이터를 무차별적으로 읽는 것을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-106">This restriction is called the *same-origin policy*, and prevents a malicious site from reading sensitive data from another site.</span></span> <span data-ttu-id="d4256-107">하지만, 경우에 따라 다른 사이트 web API를 호출할 수 있도록 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-107">However, sometimes you might want to let other sites call your web API.</span></span>
> 
> <span data-ttu-id="d4256-108">[교차 원본 자원 공유](http://www.w3.org/TR/cors/) (CORS, Cross Origin Resource Sharing)는 서버 측에서 동일 원본 정책을 완화할 수 있게 해주는 W3C 표준입니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-108">[Cross Origin Resource Sharing](http://www.w3.org/TR/cors/) (CORS) is a W3C standard that allows a server to relax the same-origin policy.</span></span> <span data-ttu-id="d4256-109">CORS를 사용하면 서버가 명시적으로 특정 교차 원본 요청만 허용하고, 다른 요청은 거부할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-109">Using CORS, a server can explicitly allow some cross-origin requests while rejecting others.</span></span> <span data-ttu-id="d4256-110">CORS는 [JSONP](http://en.wikipedia.org/wiki/JSONP) 같은 기존의 다른 기술보다 안전하고 유연합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-110">CORS is safer and more flexible than earlier techniques such as [JSONP](http://en.wikipedia.org/wiki/JSONP).</span></span> <span data-ttu-id="d4256-111">이 자습서에는 Web API 응용 프로그램에서 CORS를 사용 하도록 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-111">This tutorial shows how to enable CORS in your Web API application.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="d4256-112">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="d4256-112">Software versions used in the tutorial</span></span>
> 
> 
> - [<span data-ttu-id="d4256-113">Visual Studio 2013 업데이트 2</span><span class="sxs-lookup"><span data-stu-id="d4256-113">Visual Studio 2013 Update 2</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="d4256-114">Web API 2.2</span><span class="sxs-lookup"><span data-stu-id="d4256-114">Web API 2.2</span></span>


<a id="intro"></a>
## <a name="introduction"></a><span data-ttu-id="d4256-115">소개</span><span class="sxs-lookup"><span data-stu-id="d4256-115">Introduction</span></span>

<span data-ttu-id="d4256-116">이 자습서에서는 ASP.NET Web API에 CORS 지원이 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-116">This tutorial demonstrates CORS support in ASP.NET Web API.</span></span> <span data-ttu-id="d4256-117">하나의 호출된 "웹 서비스", Web API 컨트롤러를 호스트 하는 한 다른 호출된 "WebClient", 웹 서비스를 호출 하는 두 개의 ASP.NET 프로젝트 –를 만들어 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-117">We'll start by creating two ASP.NET projects – one called "WebService", which hosts a Web API controller, and the other called "WebClient", which calls WebService.</span></span> <span data-ttu-id="d4256-118">두 개의 응용 프로그램은 서로 다른 도메인에서 호스트 되므로, 웹 서비스를 웹 클라이언트에서 AJAX 요청 한 크로스-원본 요청이입니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-118">Because the two applications are hosted at different domains, an AJAX request from WebClient to WebService is a cross-origin request.</span></span>

![](enabling-cross-origin-requests-in-web-api/_static/image1.png)

### <a name="what-is-same-origin"></a><span data-ttu-id="d4256-119">"같은 출처" 이란?</span><span class="sxs-lookup"><span data-stu-id="d4256-119">What is "Same Origin"?</span></span>

<span data-ttu-id="d4256-120">두 URL의 스키마, 호스트 및 포트가 모두 동일한 경우, 두 URL의 원본이 동일하다고 말합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-120">Two URLs have the same origin if they have identical schemes, hosts, and ports.</span></span> <span data-ttu-id="d4256-121">([RFC 6454](http://tools.ietf.org/html/rfc6454))</span><span class="sxs-lookup"><span data-stu-id="d4256-121">([RFC 6454](http://tools.ietf.org/html/rfc6454))</span></span>

<span data-ttu-id="d4256-122">다음 두 URL은 동일한 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-122">These two URLs have the same origin:</span></span>

- `http://example.com/foo.html`
- `http://example.com/bar.html`

<span data-ttu-id="d4256-123">반면, 다음 URL들은 위의 두 URL과는 다른 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-123">These URLs have different origins than the previous two:</span></span>

- <span data-ttu-id="d4256-124">`http://example.net` -도메인이 다릅니다</span><span class="sxs-lookup"><span data-stu-id="d4256-124">`http://example.net` - Different domain</span></span>
- <span data-ttu-id="d4256-125">`http://example.com:9000/foo.html` -포트가 다릅니다</span><span class="sxs-lookup"><span data-stu-id="d4256-125">`http://example.com:9000/foo.html` - Different port</span></span>
- <span data-ttu-id="d4256-126">`https://example.com/foo.html` -스키마가 다릅니다</span><span class="sxs-lookup"><span data-stu-id="d4256-126">`https://example.com/foo.html` - Different scheme</span></span>
- <span data-ttu-id="d4256-127">`http://www.example.com/foo.html` -하위 도메인이 다릅니다</span><span class="sxs-lookup"><span data-stu-id="d4256-127">`http://www.example.com/foo.html` - Different subdomain</span></span>

> [!NOTE]
> <span data-ttu-id="d4256-128">Internet Explorer origin을 비교할 때 포트를 고려 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-128">Internet Explorer does not consider the port when comparing origins.</span></span>


<a id="create-webapi-project"></a>
## <a name="create-the-webservice-project"></a><span data-ttu-id="d4256-129">웹 서비스 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="d4256-129">Create the WebService Project</span></span>

> [!NOTE]
> <span data-ttu-id="d4256-130">이 섹션에서는 Web API 프로젝트를 만드는 방법을 이미 알고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-130">This section assumes you already know how to create Web API projects.</span></span> <span data-ttu-id="d4256-131">그렇지 않은 경우 [ASP.NET Web API 시작](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-131">If not, see [Getting Started with ASP.NET Web API](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span></span>


<span data-ttu-id="d4256-132">Visual Studio를 시작 하 고 새 **ASP.NET 웹 응용 프로그램** 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="d4256-132">Start Visual Studio and create a new **ASP.NET Web Application** project.</span></span> <span data-ttu-id="d4256-133">선택 된 **빈** 프로젝트 템플릿을 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-133">Select the **Empty** project template.</span></span> <span data-ttu-id="d4256-134">"폴더를 추가 및에 대 한 참조를 핵심" 아래에서 선택 된 **웹 API** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-134">Under "Add folders and core references for", select the **Web API** checkbox.</span></span> <span data-ttu-id="d4256-135">필요에 따라 Mircosoft Azure에 앱을 배포 하는 "클라우드에서 호스트" 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-135">Optionally, select the "Host in Cloud" option to deploy the app to Mircosoft Azure.</span></span> <span data-ttu-id="d4256-136">Microsoft에서 제공 하는 최대 10 개의 웹 사이트에 대해 무료 웹 호스팅는 [무료 Azure 평가판 계정](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-136">Microsoft offers free web hosting for up to 10 websites in a [free Azure trial account](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).</span></span>

[![](enabling-cross-origin-requests-in-web-api/_static/image3.png)](enabling-cross-origin-requests-in-web-api/_static/image2.png)

<span data-ttu-id="d4256-137">명명 된 Web API 컨트롤러 추가 `TestController` 다음 코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-137">Add a Web API controller named `TestController` with the following code:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample1.cs)]

<span data-ttu-id="d4256-138">응용 프로그램을 로컬로 실행 하거나 Azure에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-138">You can run the application locally or deploy to Azure.</span></span> <span data-ttu-id="d4256-139">(이 자습서에서 스크린 샷에 대 한 I에 배포 Azure 앱 서비스 웹 앱입니다.) Web API가 작동 하는지 확인 하려면 이동 `http://hostname/api/test/`여기서 *호스트 이름* 배포한 응용 프로그램 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-139">(For the screenshots in this tutorial, I deployed to Azure App Service Web Apps.) To verify that the web API is working, navigate to `http://hostname/api/test/`, where *hostname* is the domain where you deployed the application.</span></span> <span data-ttu-id="d4256-140">응답 텍스트가 &quot;가져오기: 테스트 메시지&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-140">You should see the response text, &quot;GET: Test Message&quot;.</span></span>

![](enabling-cross-origin-requests-in-web-api/_static/image4.png)

<a id="create-client"></a>
## <a name="create-the-webclient-project"></a><span data-ttu-id="d4256-141">WebClient 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="d4256-141">Create the WebClient Project</span></span>

<span data-ttu-id="d4256-142">다른 ASP.NET 웹 응용 프로그램 프로젝트를 만들고 선택 된 **MVC** 프로젝트 템플릿을 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-142">Create another ASP.NET Web Application project and select the **MVC** project template.</span></span> <span data-ttu-id="d4256-143">필요에 따라 선택 **인증 변경** > **인증 안 함**합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-143">Optionally, select **Change Authentication** > **No Authentication**.</span></span> <span data-ttu-id="d4256-144">이 자습서에 대 한 인증이 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-144">You don't need authentication for this tutorial.</span></span>

[![](enabling-cross-origin-requests-in-web-api/_static/image6.png)](enabling-cross-origin-requests-in-web-api/_static/image5.png)

<span data-ttu-id="d4256-145">솔루션 탐색기에서 Views/Home/Index.cshtml 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-145">In Solution Explorer, open the file Views/Home/Index.cshtml.</span></span> <span data-ttu-id="d4256-146">이 파일에 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-146">Replace the code in this file with the following:</span></span>

[!code-cshtml[Main](enabling-cross-origin-requests-in-web-api/samples/sample2.cshtml?highlight=13)]

<span data-ttu-id="d4256-147">에 대 한는 *serviceUrl* 변수를 웹 서비스 응용 프로그램의 URI를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-147">For the *serviceUrl* variable, use the URI of the WebService app.</span></span> <span data-ttu-id="d4256-148">이제 웹 클라이언트 응용 프로그램을 로컬로 실행 하거나 다른 웹 사이트에 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-148">Now run the WebClient app locally or publish it to another website.</span></span>

<span data-ttu-id="d4256-149">에 나열 된 HTTP 메서드를 사용 하 여 웹 서비스 응용 프로그램에 AJAX 요청을 제출 "시도 It" 단추를 클릭 하면 드롭다운 상자 (GET, POST 또는 PUT).</span><span class="sxs-lookup"><span data-stu-id="d4256-149">Clicking the "Try It" button submits an AJAX request to the WebService app, using the HTTP method listed in the dropdown box (GET, POST, or PUT).</span></span> <span data-ttu-id="d4256-150">이 통해 서로 다른 교차 원본 요청을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-150">This lets us examine different cross-origin requests.</span></span> <span data-ttu-id="d4256-151">지금 바로 사용, 웹 서비스 응용 프로그램은 CORS를 지원 하지 않습니다는 단추를 클릭 하면 오류가 발생 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-151">Right now, the WebService app does not support CORS, so if you click the button, you will get an error.</span></span>

![](enabling-cross-origin-requests-in-web-api/_static/image7.png)

> [!NOTE]
> <span data-ttu-id="d4256-152">다음과 같은 도구에는 HTTP 트래픽을 볼 경우 [Fiddler](http://www.telerik.com/fiddler), 브라우저는 GET 요청을 전송 하는 요청이 성공 하면 있지만 AJAX 호출 오류를 반환 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-152">If you watch the HTTP traffic in a tool like [Fiddler](http://www.telerik.com/fiddler), you will see that the browser does send the GET request, and the request succeeds, but the AJAX call returns an error.</span></span> <span data-ttu-id="d4256-153">동일 원본 정책에서 브라우저를 하지 않는 이해 해야 *보내는* 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-153">It's important to understand that same-origin policy does not prevent the browser from *sending* the request.</span></span> <span data-ttu-id="d4256-154">대신, 보지 못하도록 응용 프로그램을 하지 않습니다는 *응답*합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-154">Instead, it prevents the application from seeing the *response*.</span></span>


![](enabling-cross-origin-requests-in-web-api/_static/image8.png)

<a id="enable-cors"></a>
## <a name="enable-cors"></a><span data-ttu-id="d4256-155">CORS를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="d4256-155">Enable CORS</span></span>

<span data-ttu-id="d4256-156">이제 웹 서비스 응용 프로그램에서 CORS를 사용 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-156">Now let's enable CORS in the WebService app.</span></span> <span data-ttu-id="d4256-157">먼저, CORS NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-157">First, add the CORS NuGet package.</span></span> <span data-ttu-id="d4256-158">Visual Studio에서에서 **도구** 메뉴 선택 **라이브러리 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-158">In Visual Studio, from the **Tools** menu, select **Library Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="d4256-159">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-159">In the Package Manager Console window, type the following command:</span></span>

[!code-powershell[Main](enabling-cross-origin-requests-in-web-api/samples/sample3.ps1)]

<span data-ttu-id="d4256-160">이 명령은 최신 패키지를 설치 하 고 핵심 웹 API 라이브러리를 포함 한 모든 종속성을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-160">This command installs the latest package and updates all dependencies, including the core Web API libraries.</span></span> <span data-ttu-id="d4256-161">사용자-버전 플래그는 특정 버전을 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-161">User the -Version flag to target a specific version.</span></span> <span data-ttu-id="d4256-162">CORS 패키지에는 Web API 2.0 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-162">The CORS package requires Web API 2.0 or later.</span></span>

<span data-ttu-id="d4256-163">응용 프로그램 파일을 열고\_Start/WebApiConfig.cs 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-163">Open the file App\_Start/WebApiConfig.cs.</span></span> <span data-ttu-id="d4256-164">다음 코드를 추가 하는 **WebApiConfig.Register** 메서드.</span><span class="sxs-lookup"><span data-stu-id="d4256-164">Add the following code to the **WebApiConfig.Register** method.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample4.cs?highlight=9)]

<span data-ttu-id="d4256-165">다음으로 추가 된 **[EnableCors]** 특성을 `TestController` 클래스:</span><span class="sxs-lookup"><span data-stu-id="d4256-165">Next, add the **[EnableCors]** attribute to the `TestController` class:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample5.cs?highlight=3,7)]

<span data-ttu-id="d4256-166">에 대 한는 *origin* 매개 변수를 웹 클라이언트 응용 프로그램을 배포한 URI를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-166">For the *origins* parameter, use the URI where you deployed the WebClient application.</span></span> <span data-ttu-id="d4256-167">이렇게 하면 교차 원본 요청 WebClient에서 여전히 다른 모든 도메인 간 요청을 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-167">This allows cross-origin requests from WebClient, while still disallowing all other cross-domain requests.</span></span> <span data-ttu-id="d4256-168">나중에 대 한 매개 변수를 설명할 **[EnableCors]** 자세히 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-168">Later, I'll describe the parameters for **[EnableCors]** in more detail.</span></span>

<span data-ttu-id="d4256-169">끝에 슬래시를 포함 하지 않습니다는 *origin* URL입니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-169">Do not include a forward slash at the end of the *origins* URL.</span></span>

<span data-ttu-id="d4256-170">업데이트 된 웹 서비스 응용 프로그램을 다시 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-170">Redeploy the updated WebService application.</span></span> <span data-ttu-id="d4256-171">WebClient를 업데이트할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-171">You don't need to update WebClient.</span></span> <span data-ttu-id="d4256-172">이제 웹 클라이언트에서 AJAX 요청이 성공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-172">Now the AJAX request from WebClient should succeed.</span></span> <span data-ttu-id="d4256-173">GET, PUT 및 POST 메서드가 모두 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-173">The GET, PUT, and POST methods are all allowed.</span></span>

![](enabling-cross-origin-requests-in-web-api/_static/image9.png)

<a id="how-it-works"></a>
## <a name="how-cors-works"></a><span data-ttu-id="d4256-174">CORS가 작동 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d4256-174">How CORS Works</span></span>

<span data-ttu-id="d4256-175">이 섹션에서는 CORS 요청은 HTTP 메시지 수준에서 수행 되는 작업을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-175">This section describes what happens in a CORS request, at the level of the HTTP messages.</span></span> <span data-ttu-id="d4256-176">구성할 수 있도록 CORS의 작동 방식을 이해 해야는 **[EnableCors]** 올바르게 특성 및 작업은 예상 대로 작동 하지 않는 경우 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-176">It's important to understand how CORS works, so that you can configure the **[EnableCors]** attribute correctly, and troubleshoot if things don't work as you expect.</span></span>

<span data-ttu-id="d4256-177">CORS 명세에서는 교차 원본 요청을 활성화시키기 위한 용도로 몇 가지 새로운 HTTP 헤더들이 도입되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-177">The CORS specification introduces several new HTTP headers that enable cross-origin requests.</span></span> <span data-ttu-id="d4256-178">크로스-원본 요청;에 대 한 자동으로 이러한 헤더를 설정 브라우저 CORS를 지 원하는 경우 JavaScript 코드에 특수 한 어떤 작업도 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-178">If a browser supports CORS, it sets these headers automatically for cross-origin requests; you don't need to do anything special in your JavaScript code.</span></span>

<span data-ttu-id="d4256-179">크로스-원본 요청의 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-179">Here is an example of a cross-origin request.</span></span> <span data-ttu-id="d4256-180">"원본" 헤더는 요청을 수행 하는 사이트의 도메인을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-180">The "Origin" header gives the domain of the site that is making the request.</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample6.cmd?highlight=5)]

<span data-ttu-id="d4256-181">서버 요청을 허용 하는 경우 액세스 제어-허용-원본 헤더를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-181">If the server allows the request, it sets the Access-Control-Allow-Origin header.</span></span> <span data-ttu-id="d4256-182">이 헤더의 값 원본 헤더 또는 와일드 카드 값은 "\*", 모든 원본을 허용 되는 의미입니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-182">The value of this header either matches the Origin header, or is the wildcard value "\*", meaning that any origin is allowed.</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample7.cmd?highlight=5)]

<span data-ttu-id="d4256-183">응답에 대 한 액세스 제어-허용-원본 헤더 포함 되어 있지 않으면, AJAX 요청이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-183">If the response does not include the Access-Control-Allow-Origin header, the AJAX request fails.</span></span> <span data-ttu-id="d4256-184">특히, 브라우저 요청을 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-184">Specifically, the browser disallows the request.</span></span> <span data-ttu-id="d4256-185">성공적인 응답을 반환 하는 서버, 경우에 브라우저 수 없습니다 응답 클라이언트 응용 프로그램에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-185">Even if the server returns a successful response, the browser does not make the response available to the client application.</span></span>

<span data-ttu-id="d4256-186">**실행 전 요청**</span><span class="sxs-lookup"><span data-stu-id="d4256-186">**Preflight Requests**</span></span>

<span data-ttu-id="d4256-187">일부 CORS 요청에 대 한 브라우저의 리소스에 대 한 실제 요청을 보내기 전에 "실행 전 요청" 라는 추가 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-187">For some CORS requests, the browser sends an additional request, called a "preflight request", before it sends the actual request for the resource.</span></span>

<span data-ttu-id="d4256-188">다음 조건에 해당할 경우 브라우저에서 실행 전 요청을 건너뛸 수 있습니다.:</span><span class="sxs-lookup"><span data-stu-id="d4256-188">The browser can skip the preflight request if the following conditions are true:</span></span>

- <span data-ttu-id="d4256-189">요청 메서드는 GET, HEAD 또는 POST *및*</span><span class="sxs-lookup"><span data-stu-id="d4256-189">The request method is GET, HEAD, or POST, *and*</span></span>
- <span data-ttu-id="d4256-190">응용 프로그램 Accept, Accept-language, Content-language 이외의 모든 요청 헤더를 설정 하지 않는 콘텐츠 형식 또는 마지막-이벤트 ID, *및*</span><span class="sxs-lookup"><span data-stu-id="d4256-190">The application does not set any request headers other than Accept, Accept-Language, Content-Language, Content-Type, or Last-Event-ID, *and*</span></span>
- <span data-ttu-id="d4256-191">콘텐츠 형식 헤더 (하는 경우 설정) 다음 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-191">The Content-Type header (if set) is one of the following:</span></span> 

    - <span data-ttu-id="d4256-192">application/x-www-form-urlencoded</span><span class="sxs-lookup"><span data-stu-id="d4256-192">application/x-www-form-urlencoded</span></span>
    - <span data-ttu-id="d4256-193">multipart/폼 데이터</span><span class="sxs-lookup"><span data-stu-id="d4256-193">multipart/form-data</span></span>
    - <span data-ttu-id="d4256-194">텍스트/일반</span><span class="sxs-lookup"><span data-stu-id="d4256-194">text/plain</span></span>

<span data-ttu-id="d4256-195">요청 헤더에 대 한 규칙을 호출 하 여 응용 프로그램을 설정 하는 헤더 적용할 **setRequestHeader** 에 **XMLHttpRequest** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-195">The rule about request headers applies to headers that the application sets by calling **setRequestHeader** on the **XMLHttpRequest** object.</span></span> <span data-ttu-id="d4256-196">(이러한 작성자 요청 "헤더" CORS 사양을 호출합니다.) 헤더에 규칙이 적용 되지 않습니다는 *브라우저* 사용자 에이전트, 호스트 또는 Content-length 등 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-196">(The CORS specification calls these "author request headers".) The rule does not apply to headers the *browser* can set, such as User-Agent, Host, or Content-Length.</span></span>

<span data-ttu-id="d4256-197">실행 전 요청의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-197">Here is an example of a preflight request:</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample8.cmd?highlight=4-5)]

<span data-ttu-id="d4256-198">전 요청의 HTTP OPTIONS 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-198">The pre-flight request uses the HTTP OPTIONS method.</span></span> <span data-ttu-id="d4256-199">두 개의 특수 헤더를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-199">It includes two special headers:</span></span>

- <span data-ttu-id="d4256-200">액세스-컨트롤-요청-방법: 실제 요청에 사용할 HTTP 메서드.</span><span class="sxs-lookup"><span data-stu-id="d4256-200">Access-Control-Request-Method: The HTTP method that will be used for the actual request.</span></span>
- <span data-ttu-id="d4256-201">요청 헤더 목록이 액세스--요청-헤더 제어: 하는 *응용 프로그램* 실제 요청에 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-201">Access-Control-Request-Headers: A list of request headers that the *application* set on the actual request.</span></span> <span data-ttu-id="d4256-202">(다시이 헤더가 포함 되지 않습니다 브라우저 설정입니다.)</span><span class="sxs-lookup"><span data-stu-id="d4256-202">(Again, this does not include headers that the browser sets.)</span></span>

<span data-ttu-id="d4256-203">다음은 서버에서 요청을 허용 하는 것으로 가정 하는 예제 응답이입니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-203">Here is an example response, assuming that the server allows the request:</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample9.cmd?highlight=6-7)]

<span data-ttu-id="d4256-204">허용 되는 메서드를 나열 하는 액세스 제어-허용-방법 헤더 및 필요에 따라 허용된 된 헤더를 나열 하는 액세스 제어-허용-헤더만 헤더가 응답에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-204">The response includes an Access-Control-Allow-Methods header that lists the allowed methods, and optionally an Access-Control-Allow-Headers header, which lists the allowed headers.</span></span> <span data-ttu-id="d4256-205">실행 전 요청이 성공 하면 앞에서 설명한 대로 브라우저 실제 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-205">If the preflight request succeeds, the browser sends the actual request, as described earlier.</span></span>

<a id="scope"></a>
## <a name="scope-rules-for-enablecors"></a><span data-ttu-id="d4256-206">[EnableCors]에 대 한 범위 규칙</span><span class="sxs-lookup"><span data-stu-id="d4256-206">Scope Rules for [EnableCors]</span></span>

<span data-ttu-id="d4256-207">응용 프로그램에서 작업당: 컨트롤러 당 또는 전체적으로 모든 Web API 컨트롤러에 대해 CORS를 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-207">You can enable CORS per action, per controller, or globally for all Web API controllers in your application.</span></span>

<span data-ttu-id="d4256-208">**작업 마다**</span><span class="sxs-lookup"><span data-stu-id="d4256-208">**Per Action**</span></span>

<span data-ttu-id="d4256-209">한 번의 작업에 대 한 CORS를 사용 하도록 설정 된 **[EnableCors]** 작업 메서드에 특성을 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-209">To enable CORS for a single action, set the **[EnableCors]** attribute on the action method.</span></span> <span data-ttu-id="d4256-210">다음 예에서는 설정에 대 한 CORS는 `GetItem` 메서드만 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-210">The following example enables CORS for the `GetItem` method only.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample10.cs)]

<span data-ttu-id="d4256-211">**컨트롤러당**</span><span class="sxs-lookup"><span data-stu-id="d4256-211">**Per Controller**</span></span>

<span data-ttu-id="d4256-212">설정한 경우 **[EnableCors]** 컨트롤러 클래스에는 컨트롤러에 있는 모든 동작에 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-212">If you set **[EnableCors]** on the controller class, it applies to all the actions on the controller.</span></span> <span data-ttu-id="d4256-213">작업에 대 한 CORS를 해제 하려면 추가 **[DisableCors]** 특성 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-213">To disable CORS for an action, add the **[DisableCors]** attribute to the action.</span></span> <span data-ttu-id="d4256-214">다음 예에서는 제외한 모든 방법에 대 한 CORS를 사용 하면 `PutItem`합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-214">The following example enables CORS for every method except `PutItem`.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample11.cs)]

<span data-ttu-id="d4256-215">**전역으로**</span><span class="sxs-lookup"><span data-stu-id="d4256-215">**Globally**</span></span>

<span data-ttu-id="d4256-216">CORS를 사용 하도록 응용 프로그램에서 모든 Web API 컨트롤러에 대해 전달 된 **EnableCorsAttribute** 인스턴스는 **EnableCors** 메서드:</span><span class="sxs-lookup"><span data-stu-id="d4256-216">To enable CORS for all Web API controllers in your application, pass an **EnableCorsAttribute** instance to the **EnableCors** method:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample12.cs)]

<span data-ttu-id="d4256-217">둘 이상의 범위에서 특성을 설정 하는 경우의 우선 순위는:</span><span class="sxs-lookup"><span data-stu-id="d4256-217">If you set the attribute at more than one scope, the order of precedence is:</span></span>

1. <span data-ttu-id="d4256-218">작업</span><span class="sxs-lookup"><span data-stu-id="d4256-218">Action</span></span>
2. <span data-ttu-id="d4256-219">컨트롤러</span><span class="sxs-lookup"><span data-stu-id="d4256-219">Controller</span></span>
3. <span data-ttu-id="d4256-220">Global</span><span class="sxs-lookup"><span data-stu-id="d4256-220">Global</span></span>

<a id="allowed-origins"></a>
## <a name="set-the-allowed-origins"></a><span data-ttu-id="d4256-221">허용 되는 원본을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-221">Set the Allowed Origins</span></span>

<span data-ttu-id="d4256-222">*origin* 의 매개 변수는 **[EnableCors]** 특성 지정 리소스에 액세스 하는 원본이 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-222">The *origins* parameter of the **[EnableCors]** attribute specifies which origins are allowed to access the resource.</span></span> <span data-ttu-id="d4256-223">값은 허용 되는 원본의 쉼표로 구분 된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-223">The value is a comma-separated list of the allowed origins.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample13.cs)]

<span data-ttu-id="d4256-224">와일드 카드 값을 사용할 수 있습니다 "\*" 모든 원본에서 요청을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-224">You can also use the wildcard value "\*" to allow requests from any origins.</span></span>

<span data-ttu-id="d4256-225">모든 원본의 요청을 허용하기 전에 신중히 고민하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-225">Consider carefully before allowing requests from any origin.</span></span> <span data-ttu-id="d4256-226">모든 웹 사이트에 웹 API에 대 한 AJAX 호출을 만들 수 있음을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-226">It means that literally any website can make AJAX calls to your web API.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample14.cs)]

<a id="allowed-methods"></a>
## <a name="set-the-allowed-http-methods"></a><span data-ttu-id="d4256-227">허용 된 HTTP 메서드 설정</span><span class="sxs-lookup"><span data-stu-id="d4256-227">Set the Allowed HTTP Methods</span></span>

<span data-ttu-id="d4256-228">*메서드* 의 매개 변수는 **[EnableCors]** 특성 리소스에 액세스 하는 HTTP 메서드를 허용 하도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-228">The *methods* parameter of the **[EnableCors]** attribute specifies which HTTP methods are allowed to access the resource.</span></span> <span data-ttu-id="d4256-229">모든 메서드를 허용 하려면 와일드 카드 값을 사용 하 여 "\*"입니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-229">To allow all methods, use the wildcard value "\*".</span></span> <span data-ttu-id="d4256-230">다음 예제에서는 GET 및 POST 요청을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-230">The following example allows only GET and POST requests.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample15.cs)]

<a id="allowed-request-headers"></a>
## <a name="set-the-allowed-request-headers"></a><span data-ttu-id="d4256-231">허용 된 요청 헤더 설정</span><span class="sxs-lookup"><span data-stu-id="d4256-231">Set the Allowed Request Headers</span></span>

<span data-ttu-id="d4256-232">앞서 설명한 실행 전 요청 수는 액세스 제어-요청 헤더 헤더를 포함 하는 방법을 나열 하는 응용 프로그램에 의해 설정 된 HTTP 헤더 (이라는 "요청 헤더 author").</span><span class="sxs-lookup"><span data-stu-id="d4256-232">Earlier I described how a preflight request might include an Access-Control-Request-Headers header, listing the HTTP headers set by the application (the so-called "author request headers").</span></span> <span data-ttu-id="d4256-233">*헤더* 의 매개 변수는 **[EnableCors]** 특성 작성자 요청 헤더를 허용 되는지 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-233">The *headers* parameter of the **[EnableCors]** attribute specifies which author request headers are allowed.</span></span> <span data-ttu-id="d4256-234">모든 헤더를 허용 하려면 설정 *헤더* 를 "\*"입니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-234">To allow any headers, set *headers* to "\*".</span></span> <span data-ttu-id="d4256-235">화이트 리스트 특정 헤더를 설정 *헤더* 허용된 된 헤더의 쉼표로 구분 된 목록에:</span><span class="sxs-lookup"><span data-stu-id="d4256-235">To whitelist specific headers, set *headers* to a comma-separated list of the allowed headers:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample16.cs)]

<span data-ttu-id="d4256-236">그러나 브라우저 액세스 제어-요청 헤더를 설정 하는 방법에 완전히 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-236">However, browsers are not entirely consistent in how they set Access-Control-Request-Headers.</span></span> <span data-ttu-id="d4256-237">예를 들어 크롬에서는 현재 "출처"; 하지만 응용 프로그램이 스크립트를 설정 하는 경우에 FireFox "동의"와 같은 표준 헤더를 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-237">For example, Chrome currently includes "origin"; while FireFox does not include standard headers such as "Accept", even when the application sets them in script.</span></span>

<span data-ttu-id="d4256-238">설정한 경우 *헤더* 이외의 다른 값으로 "\*"를 포함 해야 이상 "동의", "콘텐츠 형식은" 및 "출처" + 지원 하 고 모든 사용자 지정 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-238">If you set *headers* to anything other than "\*", you should include at least "accept", "content-type", and "origin", plus any custom headers that you want to support.</span></span>

<a id="allowed-response-headers"></a>
## <a name="set-the-allowed-response-headers"></a><span data-ttu-id="d4256-239">허용 된 응답 헤더 설정</span><span class="sxs-lookup"><span data-stu-id="d4256-239">Set the Allowed Response Headers</span></span>

<span data-ttu-id="d4256-240">기본적으로 브라우저 노출 하지 않습니다 모든 응용 프로그램에 대 한 응답 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-240">By default, the browser does not expose all of the response headers to the application.</span></span> <span data-ttu-id="d4256-241">기본적으로 사용 가능한 응답 헤더들은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-241">The response headers that are available by default are:</span></span>

- <span data-ttu-id="d4256-242">캐시 제어</span><span class="sxs-lookup"><span data-stu-id="d4256-242">Cache-Control</span></span>
- <span data-ttu-id="d4256-243">Content-language</span><span class="sxs-lookup"><span data-stu-id="d4256-243">Content-Language</span></span>
- <span data-ttu-id="d4256-244">콘텐츠-유형</span><span class="sxs-lookup"><span data-stu-id="d4256-244">Content-Type</span></span>
- <span data-ttu-id="d4256-245">Expires</span><span class="sxs-lookup"><span data-stu-id="d4256-245">Expires</span></span>
- <span data-ttu-id="d4256-246">Last-Modified</span><span class="sxs-lookup"><span data-stu-id="d4256-246">Last-Modified</span></span>
- <span data-ttu-id="d4256-247">Pragma</span><span class="sxs-lookup"><span data-stu-id="d4256-247">Pragma</span></span>

<span data-ttu-id="d4256-248">CORS 명세에서는 이 헤더들을 [단순 응답 헤더(Simple Response Header)](https://dvcs.w3.org/hg/cors/raw-file/tip/Overview.html#simple-response-header) 라고 부릅니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-248">The CORS spec calls these [simple response headers](https://dvcs.w3.org/hg/cors/raw-file/tip/Overview.html#simple-response-header).</span></span> <span data-ttu-id="d4256-249">다른 헤더를 사용할 수 있도록 응용 프로그램, 설정 된 *exposedHeaders* 의 매개 변수 **[EnableCors]** 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-249">To make other headers available to the application, set the *exposedHeaders* parameter of **[EnableCors]**.</span></span>

<span data-ttu-id="d4256-250">다음 예제에서는 컨트롤러의에서 `Get` 메서드 ' X 사용자 지정 헤더 ' 라는 사용자 지정 헤더를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-250">In the following example, the controller's `Get` method sets a custom header named ‘X-Custom-Header'.</span></span> <span data-ttu-id="d4256-251">기본적으로 브라우저에 크로스-원본 요청에이 헤더가 노출 되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-251">By default, the browser will not expose this header in a cross-origin request.</span></span> <span data-ttu-id="d4256-252">헤더를 사용 하려면 ' X 사용자 지정 헤더 '에 포함 *exposedHeaders*합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-252">To make the header available, include ‘X-Custom-Header' in *exposedHeaders*.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample17.cs)]

<a id="credentials"></a>
## <a name="passing-credentials-in-cross-origin-requests"></a><span data-ttu-id="d4256-253">크로스-원본 요청에 자격 증명을 전달</span><span class="sxs-lookup"><span data-stu-id="d4256-253">Passing Credentials in Cross-Origin Requests</span></span>

<span data-ttu-id="d4256-254">CORS 요청에서 자격 증명(Credentials)은 특별한 처리를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-254">Credentials require special handling in a CORS request.</span></span> <span data-ttu-id="d4256-255">기본적으로 브라우저 크로스-원본 요청에 자격 증명을 보내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-255">By default, the browser does not send any credentials with a cross-origin request.</span></span> <span data-ttu-id="d4256-256">여기에서 말하는 자격 증명에는 쿠키뿐만 아니라 HTTP 인증 스킴도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-256">Credentials include cookies as well as HTTP authentication schemes.</span></span> <span data-ttu-id="d4256-257">크로스-원본 요청에 자격 증명을 보내려면 클라이언트 설정 해야 **XMLHttpRequest.withCredentials** true로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-257">To send credentials with a cross-origin request, the client must set **XMLHttpRequest.withCredentials** to true.</span></span>

<span data-ttu-id="d4256-258">사용 하 여 **XMLHttpRequest** 직접:</span><span class="sxs-lookup"><span data-stu-id="d4256-258">Using **XMLHttpRequest** directly:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample18.cs)]

<span data-ttu-id="d4256-259">jQuery를 사용할 경우:</span><span class="sxs-lookup"><span data-stu-id="d4256-259">In jQuery:</span></span>

[!code-javascript[Main](enabling-cross-origin-requests-in-web-api/samples/sample19.js)]

<span data-ttu-id="d4256-260">또한 서버에서도 자격 증명을 허용해야만 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-260">In addition, the server must allow the credentials.</span></span> <span data-ttu-id="d4256-261">Web API에서 크로스-원본 자격 증명을 허용 하려면 설정는 **SupportsCredentials** 속성을 true로는 **[EnableCors]** 특성:</span><span class="sxs-lookup"><span data-stu-id="d4256-261">To allow cross-origin credentials in Web API, set the **SupportsCredentials** property to true on the **[EnableCors]** attribute:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample20.cs)]

<span data-ttu-id="d4256-262">이 속성이 true 이면 HTTP 응답 액세스-컨트롤--자격 증명 허용 헤더를 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-262">If this property is true, the HTTP response will include an Access-Control-Allow-Credentials header.</span></span> <span data-ttu-id="d4256-263">이 헤더는 서버 크로스-원본 요청에 대 한 자격 증명을 허용 하는지 브라우저를 알립니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-263">This header tells the browser that the server allows credentials for a cross-origin request.</span></span>

<span data-ttu-id="d4256-264">브라우저에서 자격 증명을 보내는 응답에는 올바른 액세스-컨트롤--자격 증명 허용 헤더 표시 되지만 브라우저 응용 프로그램에 대 한 응답을 노출 되지는 않습니다 및 AJAX 요청이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-264">If the browser sends credentials, but the response does not include a valid Access-Control-Allow-Credentials header, the browser will not expose the response to the application, and the AJAX request fails.</span></span>

<span data-ttu-id="d4256-265">설정에 대 한 매우 조심 **SupportsCredentials** 다른 도메인에서 웹 사이트 사용자가 인식 하지 않고는 사용자 대신 웹 api에 로그인 한 사용자의 자격 증명에 보낼 수 있기 때문에 true입니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-265">Be very careful about setting **SupportsCredentials** to true, because it means a website at another domain can send a logged-in user's credentials to your Web API on the user's behalf, without the user being aware.</span></span> <span data-ttu-id="d4256-266">CORS 사양에 해당 설정을 설명과 함께 *origin* 를 &quot; \* &quot; 유효 하지 경우 **SupportsCredentials** 가 true입니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-266">The CORS spec also states that setting *origins* to &quot;\*&quot; is invalid if **SupportsCredentials** is true.</span></span>

<a id="cors-policy-providers"></a>
## <a name="custom-cors-policy-providers"></a><span data-ttu-id="d4256-267">사용자 지정 CORS 정책 공급자</span><span class="sxs-lookup"><span data-stu-id="d4256-267">Custom CORS Policy Providers</span></span>

<span data-ttu-id="d4256-268">**[EnableCors]** 구현 특성은 **ICorsPolicyProvider** 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-268">The **[EnableCors]** attribute implements the **ICorsPolicyProvider** interface.</span></span> <span data-ttu-id="d4256-269">파생 되는 클래스를 만들어 사용자 지정 구현을 제공할 수 있습니다 **특성** 구현 **ICorsProlicyProvider**합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-269">You can provide your own implementation by creating a class that derives from **Attribute** and implements **ICorsProlicyProvider**.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample21.cs)]

<span data-ttu-id="d4256-270">모든 위치를 추가 하면는 특성을 적용할 수 이제 **[EnableCors]** 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-270">Now you can apply the attribute any place that you would put **[EnableCors]**.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample22.cs)]

<span data-ttu-id="d4256-271">예를 들어 사용자 지정 CORS 정책 공급자는 구성 파일에서 설정을 읽을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-271">For example, a custom CORS policy provider could read the settings from a configuration file.</span></span>

<span data-ttu-id="d4256-272">특성을 사용 하는 대신를 등록할 수 있습니다는 **ICorsPolicyProviderFactory** 가 만드는 개체 **ICorsPolicyProvider** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-272">As an alternative to using attributes, you can register an **ICorsPolicyProviderFactory** object that creates **ICorsPolicyProvider** objects.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample23.cs)]

<span data-ttu-id="d4256-273">설정 하는 **ICorsPolicyProviderFactory**, 호출 된 **SetCorsPolicyProviderFactory** 확장 메서드가 다음과 같이 시작 시:</span><span class="sxs-lookup"><span data-stu-id="d4256-273">To set the **ICorsPolicyProviderFactory**, call the **SetCorsPolicyProviderFactory** extension method at startup, as follows:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample24.cs)]

<a id="browser-support"></a>
## <a name="browser-support"></a><span data-ttu-id="d4256-274">브라우저 지원</span><span class="sxs-lookup"><span data-stu-id="d4256-274">Browser Support</span></span>

<span data-ttu-id="d4256-275">Web API CORS 패키지는 서버 쪽 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-275">The Web API CORS package is a server-side technology.</span></span> <span data-ttu-id="d4256-276">CORS를 지원 하기 위해 사용자의 브라우저도 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-276">The user's browser also needs to support CORS.</span></span> <span data-ttu-id="d4256-277">모든 주요 브라우저의 현재 버전에 포함 다행히 [CORS에 대 한 지원](http://caniuse.com/cors)합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-277">Fortunately, the current versions of all major browsers include [support for CORS](http://caniuse.com/cors).</span></span>

<span data-ttu-id="d4256-278">Internet Explorer 8 및 Internet Explorer 9는 부분 지원 CORS 레거시 XDomainRequest 개체를 사용 하 여 XMLHttpRequest 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-278">Internet Explorer 8 and Internet Explorer 9 have partial support for CORS, using the legacy XDomainRequest object instead of XMLHttpRequest.</span></span> <span data-ttu-id="d4256-279">자세한 내용은 참조 [XDomainRequest-제한 사항, 제한 사항 및 해결 방법을](https://blogs.msdn.com/b/ieinternals/archive/2010/05/13/xdomainrequest-restrictions-limitations-and-workarounds.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="d4256-279">For more information, see [XDomainRequest - Restrictions, Limitations and Workarounds](https://blogs.msdn.com/b/ieinternals/archive/2010/05/13/xdomainrequest-restrictions-limitations-and-workarounds.aspx).</span></span>
