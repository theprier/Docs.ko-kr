---
uid: web-api/overview/security/enabling-cross-origin-requests-in-web-api
title: ASP.NET Web API 2에서에서 크로스-원본 요청을 사용 하도록 설정 | Microsoft Docs
author: MikeWasson
description: ASP.NET Web API에서 크로스-원본 자원 공유 (CORS)를 지 원하는 방법을 보여 줍니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/15/2014
ms.topic: article
ms.assetid: 9b265a5a-6a70-4a82-adce-2d7c56ae8bdd
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/security/enabling-cross-origin-requests-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 603eb55f8fa0b629d0287b66086b9495ef55faf7
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37381091"
---
<a name="enabling-cross-origin-requests-in-aspnet-web-api-2"></a><span data-ttu-id="9a15d-103">ASP.NET Web API 2에서에서 크로스-원본 요청을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="9a15d-103">Enabling Cross-Origin Requests in ASP.NET Web API 2</span></span>
====================
<span data-ttu-id="9a15d-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="9a15d-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="9a15d-105">브라우저의 보안 기능은 웹 페이지에서 다른 도메인으로 AJAX 요청을 전송하는 것을 막습니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-105">Browser security prevents a web page from making AJAX requests to another domain.</span></span> <span data-ttu-id="9a15d-106">이 제약 사항을 *동일 원본 정책(Same-Origin Policy)* 이라고 부르며, 악의적인 사이트가 다른 사이트의 민감한 데이터를 무차별적으로 읽는 것을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-106">This restriction is called the *same-origin policy*, and prevents a malicious site from reading sensitive data from another site.</span></span> <span data-ttu-id="9a15d-107">그러나 하려는 경우가 있습니다 수 다른 사이트에 web API를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-107">However, sometimes you might want to let other sites call your web API.</span></span>
> 
> <span data-ttu-id="9a15d-108">[교차 원본 자원 공유](http://www.w3.org/TR/cors/) (CORS, Cross Origin Resource Sharing)는 서버 측에서 동일 원본 정책을 완화할 수 있게 해주는 W3C 표준입니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-108">[Cross Origin Resource Sharing](http://www.w3.org/TR/cors/) (CORS) is a W3C standard that allows a server to relax the same-origin policy.</span></span> <span data-ttu-id="9a15d-109">CORS를 사용하면 서버가 명시적으로 특정 교차 원본 요청만 허용하고, 다른 요청은 거부할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-109">Using CORS, a server can explicitly allow some cross-origin requests while rejecting others.</span></span> <span data-ttu-id="9a15d-110">CORS는 [JSONP](http://en.wikipedia.org/wiki/JSONP) 같은 기존의 다른 기술보다 안전하고 유연합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-110">CORS is safer and more flexible than earlier techniques such as [JSONP](http://en.wikipedia.org/wiki/JSONP).</span></span> <span data-ttu-id="9a15d-111">이 자습서에는 Web API 응용 프로그램에서 CORS를 사용 하도록 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-111">This tutorial shows how to enable CORS in your Web API application.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="9a15d-112">이 자습서에 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="9a15d-112">Software versions used in the tutorial</span></span>
> 
> 
> - [<span data-ttu-id="9a15d-113">Visual Studio 2013 업데이트 2</span><span class="sxs-lookup"><span data-stu-id="9a15d-113">Visual Studio 2013 Update 2</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="9a15d-114">Web API 2.2</span><span class="sxs-lookup"><span data-stu-id="9a15d-114">Web API 2.2</span></span>


<a id="intro"></a>
## <a name="introduction"></a><span data-ttu-id="9a15d-115">소개</span><span class="sxs-lookup"><span data-stu-id="9a15d-115">Introduction</span></span>

<span data-ttu-id="9a15d-116">이 자습서에서는 ASP.NET Web API에서 CORS 지원 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-116">This tutorial demonstrates CORS support in ASP.NET Web API.</span></span> <span data-ttu-id="9a15d-117">하나의 호출된 "웹 서비스", Web API 컨트롤러를 호스트 하는 다른 호출된 "WebClient", 웹 서비스를 호출 하는 두 개의 ASP.NET 프로젝트-만들어 시작 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-117">We'll start by creating two ASP.NET projects – one called "WebService", which hosts a Web API controller, and the other called "WebClient", which calls WebService.</span></span> <span data-ttu-id="9a15d-118">두 응용 프로그램은 서로 다른 도메인에서 호스트 되므로 WebService에 WebClient에서 AJAX 요청을 한 크로스-원본 요청이입니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-118">Because the two applications are hosted at different domains, an AJAX request from WebClient to WebService is a cross-origin request.</span></span>

![](enabling-cross-origin-requests-in-web-api/_static/image1.png)

### <a name="what-is-same-origin"></a><span data-ttu-id="9a15d-119">"동일한 원본" 란?</span><span class="sxs-lookup"><span data-stu-id="9a15d-119">What is "Same Origin"?</span></span>

<span data-ttu-id="9a15d-120">두 URL의 스키마, 호스트 및 포트가 모두 동일한 경우, 두 URL의 원본이 동일하다고 말합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-120">Two URLs have the same origin if they have identical schemes, hosts, and ports.</span></span> <span data-ttu-id="9a15d-121">([RFC 6454](http://tools.ietf.org/html/rfc6454))</span><span class="sxs-lookup"><span data-stu-id="9a15d-121">([RFC 6454](http://tools.ietf.org/html/rfc6454))</span></span>

<span data-ttu-id="9a15d-122">다음 두 URL은 동일한 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-122">These two URLs have the same origin:</span></span>

- `http://example.com/foo.html`
- `http://example.com/bar.html`

<span data-ttu-id="9a15d-123">반면, 다음 URL들은 위의 두 URL과는 다른 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-123">These URLs have different origins than the previous two:</span></span>

- <span data-ttu-id="9a15d-124">`http://example.net` -도메인이 다릅니다</span><span class="sxs-lookup"><span data-stu-id="9a15d-124">`http://example.net` - Different domain</span></span>
- <span data-ttu-id="9a15d-125">`http://example.com:9000/foo.html` -포트가 다릅니다</span><span class="sxs-lookup"><span data-stu-id="9a15d-125">`http://example.com:9000/foo.html` - Different port</span></span>
- <span data-ttu-id="9a15d-126">`https://example.com/foo.html` -스키마가 다릅니다</span><span class="sxs-lookup"><span data-stu-id="9a15d-126">`https://example.com/foo.html` - Different scheme</span></span>
- <span data-ttu-id="9a15d-127">`http://www.example.com/foo.html` -하위 도메인이 다릅니다</span><span class="sxs-lookup"><span data-stu-id="9a15d-127">`http://www.example.com/foo.html` - Different subdomain</span></span>

> [!NOTE]
> <span data-ttu-id="9a15d-128">Internet Explorer 원본을 비교 하는 경우 포트를 고려 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-128">Internet Explorer does not consider the port when comparing origins.</span></span>


<a id="create-webapi-project"></a>
## <a name="create-the-webservice-project"></a><span data-ttu-id="9a15d-129">웹 서비스 프로젝트를 만들려면</span><span class="sxs-lookup"><span data-stu-id="9a15d-129">Create the WebService Project</span></span>

> [!NOTE]
> <span data-ttu-id="9a15d-130">이 섹션에서는 Web API 프로젝트를 만드는 방법을 이미 알고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-130">This section assumes you already know how to create Web API projects.</span></span> <span data-ttu-id="9a15d-131">그렇지 않은 경우 [ASP.NET Web API를 사용 하 여 시작](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-131">If not, see [Getting Started with ASP.NET Web API](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span></span>


<span data-ttu-id="9a15d-132">Visual Studio를 시작 하 고 새 **ASP.NET 웹 응용 프로그램** 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-132">Start Visual Studio and create a new **ASP.NET Web Application** project.</span></span> <span data-ttu-id="9a15d-133">선택 된 **빈** 프로젝트 템플릿.</span><span class="sxs-lookup"><span data-stu-id="9a15d-133">Select the **Empty** project template.</span></span> <span data-ttu-id="9a15d-134">"폴더를 추가 및 코어에 대 한 참조"를 선택 합니다 **Web API** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-134">Under "Add folders and core references for", select the **Web API** checkbox.</span></span> <span data-ttu-id="9a15d-135">필요에 따라 Mircosoft Azure에 앱을 배포 하는 "클라우드에서 호스트" 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-135">Optionally, select the "Host in Cloud" option to deploy the app to Mircosoft Azure.</span></span> <span data-ttu-id="9a15d-136">Microsoft에서 제공 하는 최대 10 개의 웹 사이트에 대해 무료 웹 호스트는 [무료 Azure 평가판 계정](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-136">Microsoft offers free web hosting for up to 10 websites in a [free Azure trial account](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).</span></span>

[![](enabling-cross-origin-requests-in-web-api/_static/image3.png)](enabling-cross-origin-requests-in-web-api/_static/image2.png)

<span data-ttu-id="9a15d-137">명명 된 Web API 컨트롤러 추가 `TestController` 다음 코드를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="9a15d-137">Add a Web API controller named `TestController` with the following code:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample1.cs)]

<span data-ttu-id="9a15d-138">응용 프로그램을 로컬로 실행할 수도 있고 Azure에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-138">You can run the application locally or deploy to Azure.</span></span> <span data-ttu-id="9a15d-139">(이 자습서의 스크린샷에서, 필자 배포 Azure App Service Web Apps에.) Web API가 작동 하는지 확인 하려면로 이동 `http://hostname/api/test/`여기서 *호스트 이름* 응용 프로그램을 배포한 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-139">(For the screenshots in this tutorial, I deployed to Azure App Service Web Apps.) To verify that the web API is working, navigate to `http://hostname/api/test/`, where *hostname* is the domain where you deployed the application.</span></span> <span data-ttu-id="9a15d-140">응답 텍스트가 &quot;가져오기: 테스트 메시지&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-140">You should see the response text, &quot;GET: Test Message&quot;.</span></span>

![](enabling-cross-origin-requests-in-web-api/_static/image4.png)

<a id="create-client"></a>
## <a name="create-the-webclient-project"></a><span data-ttu-id="9a15d-141">WebClient 프로젝트를 만들려면</span><span class="sxs-lookup"><span data-stu-id="9a15d-141">Create the WebClient Project</span></span>

<span data-ttu-id="9a15d-142">다른 ASP.NET 웹 응용 프로그램 프로젝트를 만들고 선택 합니다 **MVC** 프로젝트 템플릿.</span><span class="sxs-lookup"><span data-stu-id="9a15d-142">Create another ASP.NET Web Application project and select the **MVC** project template.</span></span> <span data-ttu-id="9a15d-143">필요에 따라 선택할 **인증 변경** > **인증 안 함**합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-143">Optionally, select **Change Authentication** > **No Authentication**.</span></span> <span data-ttu-id="9a15d-144">이 자습서에 대 한 인증이 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-144">You don't need authentication for this tutorial.</span></span>

[![](enabling-cross-origin-requests-in-web-api/_static/image6.png)](enabling-cross-origin-requests-in-web-api/_static/image5.png)

<span data-ttu-id="9a15d-145">솔루션 탐색기에서 Views/Home/Index.cshtml 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-145">In Solution Explorer, open the file Views/Home/Index.cshtml.</span></span> <span data-ttu-id="9a15d-146">이 파일의 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-146">Replace the code in this file with the following:</span></span>

[!code-cshtml[Main](enabling-cross-origin-requests-in-web-api/samples/sample2.cshtml?highlight=13)]

<span data-ttu-id="9a15d-147">에 대 한 합니다 *serviceUrl* 변수를 웹 서비스 응용 프로그램의 URI를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-147">For the *serviceUrl* variable, use the URI of the WebService app.</span></span> <span data-ttu-id="9a15d-148">이제 WebClient 앱을 로컬로 실행 하거나 다른 웹 사이트에 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-148">Now run the WebClient app locally or publish it to another website.</span></span>

<span data-ttu-id="9a15d-149">웹 서비스 앱에 나열 된 HTTP 메서드를 사용 하 여 AJAX 요청을 제출 "Try It" 단추를 클릭 하면 드롭다운 상자 (GET, POST 또는 PUT).</span><span class="sxs-lookup"><span data-stu-id="9a15d-149">Clicking the "Try It" button submits an AJAX request to the WebService app, using the HTTP method listed in the dropdown box (GET, POST, or PUT).</span></span> <span data-ttu-id="9a15d-150">이 통해 다양 한 원본 간 요청을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-150">This lets us examine different cross-origin requests.</span></span> <span data-ttu-id="9a15d-151">현재, 웹 서비스 앱에 CORS를 지원 하지 않습니다 단추를 클릭 하면 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-151">Right now, the WebService app does not support CORS, so if you click the button, you will get an error.</span></span>

![](enabling-cross-origin-requests-in-web-api/_static/image7.png)

> [!NOTE]
> <span data-ttu-id="9a15d-152">와 같은 도구에서 HTTP 트래픽을 시청 하는 경우 [Fiddler](http://www.telerik.com/fiddler)는 브라우저는 GET 요청을 보내지 및 요청이 성공 하지만 AJAX 호출이 오류를 반환 합니다. 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-152">If you watch the HTTP traffic in a tool like [Fiddler](http://www.telerik.com/fiddler), you will see that the browser does send the GET request, and the request succeeds, but the AJAX call returns an error.</span></span> <span data-ttu-id="9a15d-153">동일 원본 정책에서 브라우저 해도 알아야 할 것 *보내는* 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-153">It's important to understand that same-origin policy does not prevent the browser from *sending* the request.</span></span> <span data-ttu-id="9a15d-154">대신 보지 못하도록 응용 프로그램을 방지 합니다 *응답*합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-154">Instead, it prevents the application from seeing the *response*.</span></span>


![](enabling-cross-origin-requests-in-web-api/_static/image8.png)

<a id="enable-cors"></a>
## <a name="enable-cors"></a><span data-ttu-id="9a15d-155">CORS를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="9a15d-155">Enable CORS</span></span>

<span data-ttu-id="9a15d-156">이제 웹 서비스 앱에서 CORS를 사용 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-156">Now let's enable CORS in the WebService app.</span></span> <span data-ttu-id="9a15d-157">첫째, CORS NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-157">First, add the CORS NuGet package.</span></span> <span data-ttu-id="9a15d-158">Visual Studio에서에서 합니다 **도구** 메뉴에서 **라이브러리 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-158">In Visual Studio, from the **Tools** menu, select **Library Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="9a15d-159">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-159">In the Package Manager Console window, type the following command:</span></span>

[!code-powershell[Main](enabling-cross-origin-requests-in-web-api/samples/sample3.ps1)]

<span data-ttu-id="9a15d-160">이 명령은 최신 패키지를 설치 하 고 core Web API 라이브러리를 포함 한 모든 종속성을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-160">This command installs the latest package and updates all dependencies, including the core Web API libraries.</span></span> <span data-ttu-id="9a15d-161">사용자-버전 플래그는 특정 버전을 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-161">User the -Version flag to target a specific version.</span></span> <span data-ttu-id="9a15d-162">CORS 패키지에는 Web API 2.0 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-162">The CORS package requires Web API 2.0 or later.</span></span>

<span data-ttu-id="9a15d-163">앱 파일을 열고\_Start/WebApiConfig.cs 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-163">Open the file App\_Start/WebApiConfig.cs.</span></span> <span data-ttu-id="9a15d-164">다음 코드를 추가 합니다 **WebApiConfig.Register** 메서드.</span><span class="sxs-lookup"><span data-stu-id="9a15d-164">Add the following code to the **WebApiConfig.Register** method.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample4.cs?highlight=9)]

<span data-ttu-id="9a15d-165">다음을 추가 합니다 **[EnableCors]** 특성을 `TestController` 클래스:</span><span class="sxs-lookup"><span data-stu-id="9a15d-165">Next, add the **[EnableCors]** attribute to the `TestController` class:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample5.cs?highlight=3,7)]

<span data-ttu-id="9a15d-166">에 대 한 합니다 *원본을* 매개 변수를 WebClient 응용 프로그램을 배포한 URI를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-166">For the *origins* parameter, use the URI where you deployed the WebClient application.</span></span> <span data-ttu-id="9a15d-167">따라서 크로스-원본 요청에서 WebClient는 여전히 다른 모든 도메인 간 요청을 허용 하는 동안.</span><span class="sxs-lookup"><span data-stu-id="9a15d-167">This allows cross-origin requests from WebClient, while still disallowing all other cross-domain requests.</span></span> <span data-ttu-id="9a15d-168">나중에 대 한 매개 변수를 설명할 **[EnableCors]** 자세히입니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-168">Later, I'll describe the parameters for **[EnableCors]** in more detail.</span></span>

<span data-ttu-id="9a15d-169">끝에 슬래시를 포함 하지 않는 합니다 *원본을* URL입니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-169">Do not include a forward slash at the end of the *origins* URL.</span></span>

<span data-ttu-id="9a15d-170">업데이트 된 웹 서비스 응용 프로그램을 다시 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-170">Redeploy the updated WebService application.</span></span> <span data-ttu-id="9a15d-171">WebClient를 업데이트할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-171">You don't need to update WebClient.</span></span> <span data-ttu-id="9a15d-172">이제 WebClient에서 AJAX 요청이 성공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-172">Now the AJAX request from WebClient should succeed.</span></span> <span data-ttu-id="9a15d-173">GET, PUT 및 POST 메서드가 모두 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-173">The GET, PUT, and POST methods are all allowed.</span></span>

![](enabling-cross-origin-requests-in-web-api/_static/image9.png)

<a id="how-it-works"></a>
## <a name="how-cors-works"></a><span data-ttu-id="9a15d-174">CORS의 작동 원리</span><span class="sxs-lookup"><span data-stu-id="9a15d-174">How CORS Works</span></span>

<span data-ttu-id="9a15d-175">이 섹션에서는 HTTP 메시지 수준에서 CORS 요청에서 어떻게 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-175">This section describes what happens in a CORS request, at the level of the HTTP messages.</span></span> <span data-ttu-id="9a15d-176">구성할 수 있도록 CORS의 작동 방식을 이해 해야 합니다 **[EnableCors]** 올바르게 특성 및 예상 대로 작동 되지 않으면 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-176">It's important to understand how CORS works, so that you can configure the **[EnableCors]** attribute correctly, and troubleshoot if things don't work as you expect.</span></span>

<span data-ttu-id="9a15d-177">CORS 명세에서는 교차 원본 요청을 활성화시키기 위한 용도로 몇 가지 새로운 HTTP 헤더들이 도입되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-177">The CORS specification introduces several new HTTP headers that enable cross-origin requests.</span></span> <span data-ttu-id="9a15d-178">브라우저에서 CORS를 지 원하는 경우 크로스-원본 요청에 대해 자동으로 이러한 헤더 설정 모든 JavaScript 코드에 특별 한 작업을 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-178">If a browser supports CORS, it sets these headers automatically for cross-origin requests; you don't need to do anything special in your JavaScript code.</span></span>

<span data-ttu-id="9a15d-179">크로스-원본 요청 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-179">Here is an example of a cross-origin request.</span></span> <span data-ttu-id="9a15d-180">"원본" 헤더를 요청 하는 사이트의 도메인을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-180">The "Origin" header gives the domain of the site that is making the request.</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample6.cmd?highlight=5)]

<span data-ttu-id="9a15d-181">서버 요청을 허용 하면, 액세스 제어-허용-원본 헤더를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-181">If the server allows the request, it sets the Access-Control-Allow-Origin header.</span></span> <span data-ttu-id="9a15d-182">이 헤더의 값 또는 원본 헤더와 일치 하는 와일드 카드 값 "\*", 즉 모든 원본을 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-182">The value of this header either matches the Origin header, or is the wildcard value "\*", meaning that any origin is allowed.</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample7.cmd?highlight=5)]

<span data-ttu-id="9a15d-183">응답에서 액세스 제어-허용-원본 헤더를 포함 하지 않습니다, AJAX 요청이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-183">If the response does not include the Access-Control-Allow-Origin header, the AJAX request fails.</span></span> <span data-ttu-id="9a15d-184">특히 브라우저 요청을 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-184">Specifically, the browser disallows the request.</span></span> <span data-ttu-id="9a15d-185">서버 응답에 성공 하면 반환 하는 경우에 브라우저 해도 응답 클라이언트 응용 프로그램에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-185">Even if the server returns a successful response, the browser does not make the response available to the client application.</span></span>

<span data-ttu-id="9a15d-186">**실행 전 요청**</span><span class="sxs-lookup"><span data-stu-id="9a15d-186">**Preflight Requests**</span></span>

<span data-ttu-id="9a15d-187">브라우저는 일부 CORS 요청에 대 한 리소스에 대 한 실제 요청을 보내기 전에 "실행 전 요청을" 라는 추가 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-187">For some CORS requests, the browser sends an additional request, called a "preflight request", before it sends the actual request for the resource.</span></span>

<span data-ttu-id="9a15d-188">다음 조건이 true 인 경우 브라우저가 실행 전 요청을 건너뛸 수 있습니다.:</span><span class="sxs-lookup"><span data-stu-id="9a15d-188">The browser can skip the preflight request if the following conditions are true:</span></span>

- <span data-ttu-id="9a15d-189">요청 메서드는 GET, HEAD 또는 POST *및*</span><span class="sxs-lookup"><span data-stu-id="9a15d-189">The request method is GET, HEAD, or POST, *and*</span></span>
- <span data-ttu-id="9a15d-190">응용 프로그램 동의 수용-언어 Content-language 이외의 모든 요청 헤더를 설정 하지 않습니다 Content-type, 또는 마지막-이벤트-ID *및*</span><span class="sxs-lookup"><span data-stu-id="9a15d-190">The application does not set any request headers other than Accept, Accept-Language, Content-Language, Content-Type, or Last-Event-ID, *and*</span></span>
- <span data-ttu-id="9a15d-191">Content-type 헤더 (하는 경우 설정) 다음 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-191">The Content-Type header (if set) is one of the following:</span></span> 

    - <span data-ttu-id="9a15d-192">application/x-www-form-urlencoded</span><span class="sxs-lookup"><span data-stu-id="9a15d-192">application/x-www-form-urlencoded</span></span>
    - <span data-ttu-id="9a15d-193">다중 파트/폼 데이터</span><span class="sxs-lookup"><span data-stu-id="9a15d-193">multipart/form-data</span></span>
    - <span data-ttu-id="9a15d-194">텍스트/일반</span><span class="sxs-lookup"><span data-stu-id="9a15d-194">text/plain</span></span>

<span data-ttu-id="9a15d-195">요청 헤더에 대 한 규칙을 호출 하 여 응용 프로그램을 설정 하는 헤더 적용할 **setRequestHeader** 에 **XMLHttpRequest** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-195">The rule about request headers applies to headers that the application sets by calling **setRequestHeader** on the **XMLHttpRequest** object.</span></span> <span data-ttu-id="9a15d-196">(CORS 사양 이러한 "작성자 요청 헤더"를 호출 합니다.) 헤더에 규칙이 적용 되지 않습니다 합니다 *브라우저* 사용자 에이전트, 호스트 또는 콘텐츠-길이 같은 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-196">(The CORS specification calls these "author request headers".) The rule does not apply to headers the *browser* can set, such as User-Agent, Host, or Content-Length.</span></span>

<span data-ttu-id="9a15d-197">실행 전 요청의 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-197">Here is an example of a preflight request:</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample8.cmd?highlight=4-5)]

<span data-ttu-id="9a15d-198">HTTP OPTIONS 메서드를 사용 하는 사전 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-198">The pre-flight request uses the HTTP OPTIONS method.</span></span> <span data-ttu-id="9a15d-199">두 가지 특수 헤더를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-199">It includes two special headers:</span></span>

- <span data-ttu-id="9a15d-200">액세스-컨트롤-요청-방법: 실제 요청에 사용 될 HTTP 메서드.</span><span class="sxs-lookup"><span data-stu-id="9a15d-200">Access-Control-Request-Method: The HTTP method that will be used for the actual request.</span></span>
- <span data-ttu-id="9a15d-201">요청 헤더 목록은 컨트롤-요청-헤더에 액세스 합니다:는 *응용 프로그램* 실제 요청을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-201">Access-Control-Request-Headers: A list of request headers that the *application* set on the actual request.</span></span> <span data-ttu-id="9a15d-202">(마찬가지로이 브라우저 설정 하는 헤더)</span><span class="sxs-lookup"><span data-stu-id="9a15d-202">(Again, this does not include headers that the browser sets.)</span></span>

<span data-ttu-id="9a15d-203">예제 응답, 서버 요청을 허용 하는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-203">Here is an example response, assuming that the server allows the request:</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample9.cmd?highlight=6-7)]

<span data-ttu-id="9a15d-204">허용 된 메서드를 나열 하는 액세스-컨트롤-허용-메서드 헤더 및 필요에 따라 허용 되는 헤더를 나열 하는 액세스 제어-허용-헤더 헤더를 응답에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-204">The response includes an Access-Control-Allow-Methods header that lists the allowed methods, and optionally an Access-Control-Allow-Headers header, which lists the allowed headers.</span></span> <span data-ttu-id="9a15d-205">실행 전 요청이 성공 하면 브라우저 앞에서 설명한 대로 실제 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-205">If the preflight request succeeds, the browser sends the actual request, as described earlier.</span></span>

<a id="scope"></a>
## <a name="scope-rules-for-enablecors"></a><span data-ttu-id="9a15d-206">[EnableCors]에 대 한 범위 규칙</span><span class="sxs-lookup"><span data-stu-id="9a15d-206">Scope Rules for [EnableCors]</span></span>

<span data-ttu-id="9a15d-207">응용 프로그램에서 작업당: 컨트롤러 당 또는 모든 Web API 컨트롤러에 대 한 전역적으로 CORS를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-207">You can enable CORS per action, per controller, or globally for all Web API controllers in your application.</span></span>

<span data-ttu-id="9a15d-208">**작업당**</span><span class="sxs-lookup"><span data-stu-id="9a15d-208">**Per Action**</span></span>

<span data-ttu-id="9a15d-209">단일 작업에 대 한 CORS를 사용 하도록 설정 합니다 **[EnableCors]** 동작 메서드에 대 한 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-209">To enable CORS for a single action, set the **[EnableCors]** attribute on the action method.</span></span> <span data-ttu-id="9a15d-210">다음 예제에서는 CORS는 `GetItem` 방법만 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-210">The following example enables CORS for the `GetItem` method only.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample10.cs)]

<span data-ttu-id="9a15d-211">**컨트롤러당**</span><span class="sxs-lookup"><span data-stu-id="9a15d-211">**Per Controller**</span></span>

<span data-ttu-id="9a15d-212">설정 하는 경우 **[EnableCors]** 컨트롤러 클래스에 대해 컨트롤러에서 모든 작업에 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-212">If you set **[EnableCors]** on the controller class, it applies to all the actions on the controller.</span></span> <span data-ttu-id="9a15d-213">CORS를 사용 하지 않으려면 작업을 추가 합니다 **[DisableCors]** 특성 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-213">To disable CORS for an action, add the **[DisableCors]** attribute to the action.</span></span> <span data-ttu-id="9a15d-214">다음 예제에서는 제외한 모든 방법에 대 한 CORS를 사용 하면 `PutItem`합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-214">The following example enables CORS for every method except `PutItem`.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample11.cs)]

<span data-ttu-id="9a15d-215">**전 세계**</span><span class="sxs-lookup"><span data-stu-id="9a15d-215">**Globally**</span></span>

<span data-ttu-id="9a15d-216">CORS를 사용 하도록 응용 프로그램에서 모든 Web API 컨트롤러에 대 한 전달를 **EnableCorsAttribute** 인스턴스를 **EnableCors** 메서드:</span><span class="sxs-lookup"><span data-stu-id="9a15d-216">To enable CORS for all Web API controllers in your application, pass an **EnableCorsAttribute** instance to the **EnableCors** method:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample12.cs)]

<span data-ttu-id="9a15d-217">둘 이상의 범위에서 특성을 설정 하는 경우 우선 순위가 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-217">If you set the attribute at more than one scope, the order of precedence is:</span></span>

1. <span data-ttu-id="9a15d-218">작업</span><span class="sxs-lookup"><span data-stu-id="9a15d-218">Action</span></span>
2. <span data-ttu-id="9a15d-219">컨트롤러</span><span class="sxs-lookup"><span data-stu-id="9a15d-219">Controller</span></span>
3. <span data-ttu-id="9a15d-220">Global</span><span class="sxs-lookup"><span data-stu-id="9a15d-220">Global</span></span>

<a id="allowed-origins"></a>
## <a name="set-the-allowed-origins"></a><span data-ttu-id="9a15d-221">허용 되는 원본을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-221">Set the Allowed Origins</span></span>

<span data-ttu-id="9a15d-222">*원본을* 의 매개 변수를 **[EnableCors]** 특성 리소스에 액세스할 수 있는 원본 허용 되는지 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-222">The *origins* parameter of the **[EnableCors]** attribute specifies which origins are allowed to access the resource.</span></span> <span data-ttu-id="9a15d-223">값은 허용 되는 원본의 쉼표로 구분 된 목록.</span><span class="sxs-lookup"><span data-stu-id="9a15d-223">The value is a comma-separated list of the allowed origins.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample13.cs)]

<span data-ttu-id="9a15d-224">와일드 카드 값을 사용할 수도 있습니다 "\*" 요청을 모든 원본을 허용 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-224">You can also use the wildcard value "\*" to allow requests from any origins.</span></span>

<span data-ttu-id="9a15d-225">모든 원본의 요청을 허용하기 전에 신중히 고민하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-225">Consider carefully before allowing requests from any origin.</span></span> <span data-ttu-id="9a15d-226">말 그대로 모든 웹 사이트에 web API에 대 한 AJAX 호출을 설정할 수 있는지를 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-226">It means that literally any website can make AJAX calls to your web API.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample14.cs)]

<a id="allowed-methods"></a>
## <a name="set-the-allowed-http-methods"></a><span data-ttu-id="9a15d-227">허용 된 HTTP 메서드 설정</span><span class="sxs-lookup"><span data-stu-id="9a15d-227">Set the Allowed HTTP Methods</span></span>

<span data-ttu-id="9a15d-228">합니다 *메서드* 의 매개 변수를 **[EnableCors]** 리소스에 액세스할 수 있는 HTTP 메서드 특성 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-228">The *methods* parameter of the **[EnableCors]** attribute specifies which HTTP methods are allowed to access the resource.</span></span> <span data-ttu-id="9a15d-229">모든 메서드를 허용 하려면 와일드 카드 값을 사용 하 여 "\*"입니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-229">To allow all methods, use the wildcard value "\*".</span></span> <span data-ttu-id="9a15d-230">다음 예제에서는 GET 및 POST 요청만 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-230">The following example allows only GET and POST requests.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample15.cs)]

<a id="allowed-request-headers"></a>
## <a name="set-the-allowed-request-headers"></a><span data-ttu-id="9a15d-231">허용 된 요청 헤더를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-231">Set the Allowed Request Headers</span></span>

<span data-ttu-id="9a15d-232">앞서 설명 했 듯이 실행 전 요청 액세스-컨트롤-요청-헤더 헤더를 포함할 수 있습니다 하는 방법을 나열 하는 응용 프로그램에 의해 설정 된 HTTP 헤더 (소위 "요청 헤더 author").</span><span class="sxs-lookup"><span data-stu-id="9a15d-232">Earlier I described how a preflight request might include an Access-Control-Request-Headers header, listing the HTTP headers set by the application (the so-called "author request headers").</span></span> <span data-ttu-id="9a15d-233">합니다 *헤더* 의 매개 변수를 **[EnableCors]** 특성은 만든 요청 헤더를 허용 하도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-233">The *headers* parameter of the **[EnableCors]** attribute specifies which author request headers are allowed.</span></span> <span data-ttu-id="9a15d-234">모든 헤더를 허용 하려면 설정 *헤더* 에 "\*"입니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-234">To allow any headers, set *headers* to "\*".</span></span> <span data-ttu-id="9a15d-235">허용 목록에 추가할 특정 헤더를 설정 *헤더* 허용 되는 헤더의 쉼표로 구분 된 목록에:</span><span class="sxs-lookup"><span data-stu-id="9a15d-235">To whitelist specific headers, set *headers* to a comma-separated list of the allowed headers:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample16.cs)]

<span data-ttu-id="9a15d-236">그러나 브라우저에 대 한 액세스 제어-요청 헤더는 설정 하는 방법을 완전히 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-236">However, browsers are not entirely consistent in how they set Access-Control-Request-Headers.</span></span> <span data-ttu-id="9a15d-237">크롬이 "원본" 현재 포함 하는 예를 들어, 하지만 응용 프로그램이 스크립트를 설정 하는 경우에 FireFox "Accept"와 같은 표준 헤더를 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-237">For example, Chrome currently includes "origin"; while FireFox does not include standard headers such as "Accept", even when the application sets them in script.</span></span>

<span data-ttu-id="9a15d-238">설정 하는 경우 *헤더* 이외의 값으로 "\*"를 포함 해야 적어도 "수락", "콘텐츠-유형" 및 "원본"을 지원 하려는 모든 사용자 지정 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-238">If you set *headers* to anything other than "\*", you should include at least "accept", "content-type", and "origin", plus any custom headers that you want to support.</span></span>

<a id="allowed-response-headers"></a>
## <a name="set-the-allowed-response-headers"></a><span data-ttu-id="9a15d-239">허용 되는 응답 헤더 설정</span><span class="sxs-lookup"><span data-stu-id="9a15d-239">Set the Allowed Response Headers</span></span>

<span data-ttu-id="9a15d-240">기본적으로 브라우저 노출 하지 않습니다 모든 응용 프로그램에 대 한 응답 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-240">By default, the browser does not expose all of the response headers to the application.</span></span> <span data-ttu-id="9a15d-241">기본적으로 사용 가능한 응답 헤더들은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-241">The response headers that are available by default are:</span></span>

- <span data-ttu-id="9a15d-242">캐시 제어</span><span class="sxs-lookup"><span data-stu-id="9a15d-242">Cache-Control</span></span>
- <span data-ttu-id="9a15d-243">콘텐츠 언어</span><span class="sxs-lookup"><span data-stu-id="9a15d-243">Content-Language</span></span>
- <span data-ttu-id="9a15d-244">콘텐츠 형식</span><span class="sxs-lookup"><span data-stu-id="9a15d-244">Content-Type</span></span>
- <span data-ttu-id="9a15d-245">Expires</span><span class="sxs-lookup"><span data-stu-id="9a15d-245">Expires</span></span>
- <span data-ttu-id="9a15d-246">Last-Modified</span><span class="sxs-lookup"><span data-stu-id="9a15d-246">Last-Modified</span></span>
- <span data-ttu-id="9a15d-247">Pragma</span><span class="sxs-lookup"><span data-stu-id="9a15d-247">Pragma</span></span>

<span data-ttu-id="9a15d-248">CORS 명세에서는 이 헤더들을 [단순 응답 헤더(Simple Response Header)](https://dvcs.w3.org/hg/cors/raw-file/tip/Overview.html#simple-response-header) 라고 부릅니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-248">The CORS spec calls these [simple response headers](https://dvcs.w3.org/hg/cors/raw-file/tip/Overview.html#simple-response-header).</span></span> <span data-ttu-id="9a15d-249">다른 헤더에서 응용 프로그램에 사용할 수 있도록 설정 합니다 *exposedHeaders* 의 매개 변수 **[EnableCors]** 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-249">To make other headers available to the application, set the *exposedHeaders* parameter of **[EnableCors]**.</span></span>

<span data-ttu-id="9a15d-250">다음 예제에서는 컨트롤러의에서 `Get` 메서드 ' X 사용자 지정 헤더 ' 라는 사용자 지정 헤더를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-250">In the following example, the controller's `Get` method sets a custom header named ‘X-Custom-Header'.</span></span> <span data-ttu-id="9a15d-251">기본적으로 브라우저는 크로스-원본 요청에서이 헤더를 노출 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-251">By default, the browser will not expose this header in a cross-origin request.</span></span> <span data-ttu-id="9a15d-252">헤더에서 사용할 수 있도록 하려면에 ' X 사용자 지정 헤더 '를 포함 *exposedHeaders*합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-252">To make the header available, include ‘X-Custom-Header' in *exposedHeaders*.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample17.cs)]

<a id="credentials"></a>
## <a name="passing-credentials-in-cross-origin-requests"></a><span data-ttu-id="9a15d-253">크로스-원본 요청에 자격 증명 전달</span><span class="sxs-lookup"><span data-stu-id="9a15d-253">Passing Credentials in Cross-Origin Requests</span></span>

<span data-ttu-id="9a15d-254">CORS 요청에서 자격 증명(Credentials)은 특별한 처리를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-254">Credentials require special handling in a CORS request.</span></span> <span data-ttu-id="9a15d-255">기본적으로 브라우저는 크로스-원본 요청을 사용 하 여 자격 증명을 보내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-255">By default, the browser does not send any credentials with a cross-origin request.</span></span> <span data-ttu-id="9a15d-256">여기에서 말하는 자격 증명에는 쿠키뿐만 아니라 HTTP 인증 스킴도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-256">Credentials include cookies as well as HTTP authentication schemes.</span></span> <span data-ttu-id="9a15d-257">크로스-원본 요청을 사용 하 여 자격 증명을 보내려면 클라이언트 설정 해야 합니다 **XMLHttpRequest.withCredentials** true로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-257">To send credentials with a cross-origin request, the client must set **XMLHttpRequest.withCredentials** to true.</span></span>

<span data-ttu-id="9a15d-258">사용 하 여 **XMLHttpRequest** 직접.</span><span class="sxs-lookup"><span data-stu-id="9a15d-258">Using **XMLHttpRequest** directly:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample18.cs)]

<span data-ttu-id="9a15d-259">jQuery를 사용할 경우:</span><span class="sxs-lookup"><span data-stu-id="9a15d-259">In jQuery:</span></span>

[!code-javascript[Main](enabling-cross-origin-requests-in-web-api/samples/sample19.js)]

<span data-ttu-id="9a15d-260">또한 서버에서도 자격 증명을 허용해야만 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-260">In addition, the server must allow the credentials.</span></span> <span data-ttu-id="9a15d-261">Web API에서 크로스-원본 자격 증명을 허용 하려면 설정 합니다 **SupportsCredentials** 속성에서 true로 합니다 **[EnableCors]** 특성:</span><span class="sxs-lookup"><span data-stu-id="9a15d-261">To allow cross-origin credentials in Web API, set the **SupportsCredentials** property to true on the **[EnableCors]** attribute:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample20.cs)]

<span data-ttu-id="9a15d-262">이 속성이 true 이면 HTTP 응답에 대 한 액세스 제어-허용-자격 증명 헤더가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-262">If this property is true, the HTTP response will include an Access-Control-Allow-Credentials header.</span></span> <span data-ttu-id="9a15d-263">이 헤더는 서버를 크로스-원본 요청에 대 한 자격 증명을 허용 하는지 브라우저를 알립니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-263">This header tells the browser that the server allows credentials for a cross-origin request.</span></span>

<span data-ttu-id="9a15d-264">브라우저에서 자격 증명을 보내는 응답을 유효한 액세스-컨트롤--자격 증명 허용 헤더를 포함 하지 않습니다 하지만 브라우저 응용 프로그램에 대 한 응답을 노출 하지 않습니다 고 AJAX 요청이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-264">If the browser sends credentials, but the response does not include a valid Access-Control-Allow-Credentials header, the browser will not expose the response to the application, and the AJAX request fails.</span></span>

<span data-ttu-id="9a15d-265">설정에 대 한 매우 주의 **SupportsCredentials** 다른 도메인에서 웹 사이트 사용자가 인식 하지 않고 사용자 대신 Web API에는 로그인 한 사용자의 자격 증명에 보낼 수 있기 때문에 true로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-265">Be very careful about setting **SupportsCredentials** to true, because it means a website at another domain can send a logged-in user's credentials to your Web API on the user's behalf, without the user being aware.</span></span> <span data-ttu-id="9a15d-266">CORS 사양에는 또한 해당 설정 상태 *원본을* 에 &quot; \* &quot; 올바르지 경우 **SupportsCredentials** 그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-266">The CORS spec also states that setting *origins* to &quot;\*&quot; is invalid if **SupportsCredentials** is true.</span></span>

<a id="cors-policy-providers"></a>
## <a name="custom-cors-policy-providers"></a><span data-ttu-id="9a15d-267">사용자 지정 CORS 정책 공급자</span><span class="sxs-lookup"><span data-stu-id="9a15d-267">Custom CORS Policy Providers</span></span>

<span data-ttu-id="9a15d-268">합니다 **[EnableCors]** 구현 특성을 **ICorsPolicyProvider** 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-268">The **[EnableCors]** attribute implements the **ICorsPolicyProvider** interface.</span></span> <span data-ttu-id="9a15d-269">파생 되는 클래스를 만들어 사용자 지정 구현을 제공할 수 있습니다 **특성** 구현 **ICorsProlicyProvider**합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-269">You can provide your own implementation by creating a class that derives from **Attribute** and implements **ICorsProlicyProvider**.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample21.cs)]

<span data-ttu-id="9a15d-270">이제 배치 하는 위치 특성을 적용할 수 있습니다 **[EnableCors]** 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-270">Now you can apply the attribute any place that you would put **[EnableCors]**.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample22.cs)]

<span data-ttu-id="9a15d-271">예를 들어, 사용자 지정 CORS 정책 공급자를 구성 파일에서 설정을 읽을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-271">For example, a custom CORS policy provider could read the settings from a configuration file.</span></span>

<span data-ttu-id="9a15d-272">특성을 사용 하는 대신,으로 등록할 수 있습니다는 **ICorsPolicyProviderFactory** 개체를 만드는 **ICorsPolicyProvider** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-272">As an alternative to using attributes, you can register an **ICorsPolicyProviderFactory** object that creates **ICorsPolicyProvider** objects.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample23.cs)]

<span data-ttu-id="9a15d-273">설정 하는 **ICorsPolicyProviderFactory**를 호출 합니다 **SetCorsPolicyProviderFactory** 같이 시작 시 확장 메서드:</span><span class="sxs-lookup"><span data-stu-id="9a15d-273">To set the **ICorsPolicyProviderFactory**, call the **SetCorsPolicyProviderFactory** extension method at startup, as follows:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample24.cs)]

<a id="browser-support"></a>
## <a name="browser-support"></a><span data-ttu-id="9a15d-274">브라우저 지원</span><span class="sxs-lookup"><span data-stu-id="9a15d-274">Browser Support</span></span>

<span data-ttu-id="9a15d-275">Web API CORS 패키지에는 서버 쪽 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-275">The Web API CORS package is a server-side technology.</span></span> <span data-ttu-id="9a15d-276">사용자의 브라우저는 또한 CORS를 지원 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-276">The user's browser also needs to support CORS.</span></span> <span data-ttu-id="9a15d-277">다행 스럽게도 모든 주요 브라우저의 현재 버전 포함 [CORS에 대 한 지원](http://caniuse.com/cors)합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-277">Fortunately, the current versions of all major browsers include [support for CORS](http://caniuse.com/cors).</span></span>

<span data-ttu-id="9a15d-278">Internet Explorer 8 및 Internet Explorer 9 부분에 대 한 지원이 CORS XMLHttpRequest 대신 레거시 XDomainRequest 개체를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-278">Internet Explorer 8 and Internet Explorer 9 have partial support for CORS, using the legacy XDomainRequest object instead of XMLHttpRequest.</span></span> <span data-ttu-id="9a15d-279">자세한 내용은 [XDomainRequest-제한 사항, 제한 사항 및 해결 방법](https://blogs.msdn.com/b/ieinternals/archive/2010/05/13/xdomainrequest-restrictions-limitations-and-workarounds.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="9a15d-279">For more information, see [XDomainRequest - Restrictions, Limitations and Workarounds](https://blogs.msdn.com/b/ieinternals/archive/2010/05/13/xdomainrequest-restrictions-limitations-and-workarounds.aspx).</span></span>
