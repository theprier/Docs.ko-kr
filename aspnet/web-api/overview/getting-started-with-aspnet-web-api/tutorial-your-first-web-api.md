---
uid: web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
title: ASP.NET Web API 2 (C#)를 사용 하 여 시작
author: MikeWasson
description: HTTP를 단순히 웹 페이지를 제공 합니다. 서비스 및 데이터를 노출 하는 Api를 빌드하기 위한 강력한 플랫폼 이기도 합니다. HTTP에는 단순 하 고 유연 하 고 ubiq는 중...
ms.author: riande
ms.date: 11/28/2017
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
msc.type: authoredcontent
ms.openlocfilehash: 7bec95af4532535f0d620bfe6862958907466874
ms.sourcegitcommit: 728f4e47be91e1c87bb7c0041734191b5f5c6da3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/22/2019
ms.locfileid: "54444261"
---
<a name="get-started-with-aspnet-web-api-2-c"></a>ASP.NET Web API 2 (C#)를 사용 하 여 시작
====================
[Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트 다운로드](https://code.msdn.microsoft.com/Sample-code-of-Getting-c56ccb28)

HTTP를 단순히 웹 페이지를 제공 합니다. HTTP은 서비스 및 데이터를 노출 하는 Api를 빌드하기 위한 강력한 플랫폼 이기도 합니다. HTTP는 간단 하 고 유연 하며 유비쿼터스는입니다. 생각할 수 있는 거의 모든 플랫폼에서 HTTP 라이브러리도 있으므로 HTTP 서비스는 광범위 한 브라우저, 모바일 장치 및 기존 데스크톱 응용 프로그램 등의 클라이언트를 확보할 수 있습니다.

ASP.NET Web API는 web Api는.NET Framework를 빌드하기 위한 프레임 워크입니다. 이 자습서에서는 제품의 목록을 반환 하는 web API를 만들려면 ASP.NET Web API를 사용 합니다.

## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전

- [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
- Web API 2

참조 [ASP.NET Core 및 Windows에 대 한 Visual Studio를 사용 하 여 web API 만들기](https://docs.microsoft.com/aspnet/core/tutorials/first-web-api) 이 자습서의 최신 버전입니다.

## <a name="create-a-web-api-project"></a>웹 API 프로젝트 만들기

이 자습서에서는 제품의 목록을 반환 하는 web API를 만들려면 ASP.NET Web API를 사용 합니다. 프런트 엔드 웹 페이지 결과 표시 하려면 jQuery를 사용 합니다.

![](tutorial-your-first-web-api/_static/image1.png)

Visual Studio를 시작 하 고 선택 **새 프로젝트** 에서 합니다 **시작** 페이지입니다. 또는에서 **파일** 메뉴에서 **새로 만들기** 차례로 **프로젝트**합니다.

에 **템플릿** 창 **설치 된 템플릿** 확장 하 고는 **Visual C#** 노드. 아래 **Visual C#** 를 선택 **웹**합니다. 프로젝트 템플릿 목록에서 선택 **ASP.NET 웹 응용 프로그램**합니다. "ProductsApp" 프로젝트 이름을 지정 하 고 클릭 **확인**합니다.

![](tutorial-your-first-web-api/_static/image2.png)

에 **새 ASP.NET 프로젝트** 대화 상자에서 선택 합니다 **빈** 템플릿. 아래 &quot;폴더를 추가 하 고에 대 한 참조를 핵심&quot;, 확인 **Web API**합니다. **확인**을 클릭합니다.

![](tutorial-your-first-web-api/_static/image3.png)

> [!NOTE]
> 사용 하 여 Web API 프로젝트를 만들 수도 있습니다는 &quot;Web API&quot; 템플릿. Web API 템플릿에서 ASP.NET MVC를 사용 하 여 API 도움말 페이지를 제공 합니다. MVC 사용 하지 않고 웹 API를 표시 하려고 하기 때문에 빈 템플릿에이 자습서에 사용 합니다. 일반적으로 ASP.NET MVC로 웹 API를 사용 하 여 알 필요가 없습니다.


## <a name="adding-a-model"></a>모델 추가

*모델*은 애플리케이션에서 데이터를 나타내는 개체입니다. ASP.NET Web API는 자동으로 JSON, XML 또는 다른 형식으로 모델을 직렬화 하 고 HTTP 응답 메시지의 본문으로 serialize 된 데이터를 쓸 수 있습니다. 클라이언트는 serialization 형식을 읽을 수 있습니다,으로 개체를 deserialize 할 수 있습니다. 대부분의 클라이언트에는 XML 또는 JSON 구문 분석할 수 있습니다. 또한 클라이언트는 HTTP 요청 메시지의 Accept 헤더를 설정 하 여 하려고 하는 형식을 나타낼 수 있습니다.

제품을 나타내는 간단한 모델을 만들어 보겠습니다.

솔루션 탐색기 표시 되지 않으면 클릭 합니다 **뷰** 선택한 메뉴 **솔루션 탐색기**합니다. 솔루션 탐색기에서 Models 폴더를 마우스 오른쪽 단추로 클릭 합니다. 상황에 맞는 메뉴에서 선택 **추가** 선택한 **클래스**합니다.

![](tutorial-your-first-web-api/_static/image4.png)

클래스의 이름을 &quot;제품&quot;합니다. 다음 속성을 추가 합니다 `Product` 클래스입니다.

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample1.cs)]

## <a name="adding-a-controller"></a>컨트롤러 추가

Web API에는 *컨트롤러* 는 HTTP 요청을 처리 하는 개체입니다. Id로 지정 된 단일 제품 또는 제품의 목록을 반환할 수 있는 컨트롤러 추가

> [!NOTE]
> ASP.NET MVC를 사용한 경우 이미 잘 알고 있다면 컨트롤러를 사용 하 여 합니다. Web API 컨트롤러는 MVC 컨트롤러 유사 하지만 상속 된 **ApiController** 클래스 대신 합니다 **컨트롤러** 클래스입니다.

**솔루션 탐색기**, Controllers 폴더를 마우스 오른쪽 단추로 클릭 합니다. 선택 **추가** 선택한 후 **컨트롤러**합니다.

![](tutorial-your-first-web-api/_static/image5.png)

에 **스 캐 폴드 추가** 대화 상자에서 **Web API 컨트롤러-비어 있음**합니다. **추가**를 클릭합니다.

![](tutorial-your-first-web-api/_static/image6.png)

에 **컨트롤러 추가** 대화 상자에서 컨트롤러 이름 &quot;ProductsController&quot;합니다. **추가**를 클릭합니다.

![](tutorial-your-first-web-api/_static/image7.png)

스 캐 폴딩을 ProductsController.cs Controllers 폴더에서 파일을 만듭니다.

![](tutorial-your-first-web-api/_static/image8.png)

> [!NOTE]
> 컨트롤러 라는 폴더에는 컨트롤러 넣이 필요가 없습니다. 폴더 이름은 원본 파일을 구성 하는 편리한 방법입니다.


이 파일이 열려 있지 않으면 이미를 열려는 파일을 두 번 클릭 합니다. 이 파일의 코드를 다음으로 바꿉니다.

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample2.cs)]

예제를 단순하게 유지 하기 제품 고정 된 배열을 컨트롤러 클래스 내에 저장 됩니다. 물론 실제 응용 프로그램에서 데이터베이스 쿼리 하거나를 일부 기타 외부 데이터 원본을 사용 합니다.

제품을 반환 하는 두 메서드를 정의 하는 컨트롤러:

- 합니다 `GetAllProducts` 제품의 전체 목록을 반환는 **IEnumerable&lt;제품&gt;**  형식입니다.
- `GetProduct` 메서드를 해당 ID로 단일 제품 조회

정말 간단하죠. Web API 작업 해야합니다. 컨트롤러에서 각 메서드는 하나 이상의 Uri에 해당 됩니다.

| 컨트롤러 메서드 | URI |
| --- | --- |
| GetAllProducts | api 제품 |
| GetProduct | /api/products/*id* |

에 대 한 합니다 `GetProduct` 메서드를 *id* URI에는 자리 표시자입니다. 예를 들어, ID가 5 인 제품을 얻으려면 URI는 `api/products/5`합니다.

Web API 컨트롤러 메서드를 HTTP 요청을 라우팅하 하는 방법에 대 한 자세한 내용은 참조 하세요. [ASP.NET Web API에서 라우팅](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)합니다.

## <a name="calling-the-web-api-with-javascript-and-jquery"></a>Javascript와 jQuery를 사용한 Web API를 호출합니다.

이 섹션에서는 AJAX를 사용 하 여 web API를 호출 하는 HTML 페이지를 추가 합니다. AJAX 호출을 수행 하 고 결과 사용 하 여 페이지를 업데이트 하려면 jQuery를 사용 하겠습니다.

솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가**을 선택한 후 **새 항목**합니다.

![](tutorial-your-first-web-api/_static/image9.png)

에 **새 항목 추가** 대화 상자에서를 **웹** 노드에서 **Visual C#** 를 선택한 후는 **HTML 페이지** 항목. 페이지의 이름을 &quot;index.html&quot;합니다.

![](tutorial-your-first-web-api/_static/image10.png)

다음을 사용 하 여이 파일의 모든 항목을 바꿉니다.

[!code-html[Main](tutorial-your-first-web-api/samples/sample3.html)]

여러 가지 방법으로 jQuery를 가져올 수 있습니다. 이 예에서 사용 된 [Microsoft Ajax CDN](../../../ajax/cdn/overview.md)합니다. 다운로드할 수도 있습니다 [ http://jquery.com/ ](http://jquery.com/), 및 "웹 API" ASP.NET 프로젝트 템플릿에 jQuery도 포함 되어 있습니다.

### <a name="getting-a-list-of-products"></a>제품의 목록 가져오기

제품 목록을 가져오려고로 HTTP GET 요청을 보낼 &quot;/api/제품&quot;합니다.

JQuery [getJSON](http://api.jquery.com/jQuery.getJSON/) 함수 AJAX 요청을 보냅니다. 응답에 대 한 JSON 개체 배열을 포함합니다. `done` 함수 요청이 성공 하는 경우 호출 되는 콜백을 지정 합니다. 콜백 DOM 제품 정보를 사용 하 여 업데이트 합니다.

[!code-html[Main](tutorial-your-first-web-api/samples/sample4.html)]

### <a name="getting-a-product-by-id"></a>제품 ID 별로 가져오기

제품 ID 가져오려면로 HTTP GET 요청을 보낼 &quot;/a p i/제품/*id*&quot;여기서 *id* 제품 ID입니다.

[!code-javascript[Main](tutorial-your-first-web-api/samples/sample5.js)]

여전히 호출 `getJSON` AJAX 요청이 이번에 보낼 요청 URI에서에서 ID를 입력 합니다. 이 요청의 응답에는 단일 제품의 JSON 표현입니다.

## <a name="running-the-application"></a>응용 프로그램 실행

F5 키를 눌러 응용 프로그램 디버깅을 시작 합니다. 웹 페이지는 다음과 같이 표시 됩니다.

![](tutorial-your-first-web-api/_static/image11.png)

제품 ID 별로 가져오기 ID를 입력 하 고 검색을 클릭 합니다.

![](tutorial-your-first-web-api/_static/image12.png)

잘못 된 ID를 입력 하면 서버에 HTTP 오류를 반환 합니다.

![](tutorial-your-first-web-api/_static/image13.png)

## <a name="using-f12-to-view-the-http-request-and-response"></a>F12 키를 사용 하 여 HTTP 요청 및 응답을 보려면

HTTP 서비스를 사용 하 여 작업 하는 경우 HTTP 요청 및 요청 메시지에 매우 유용할 수 있습니다. Internet Explorer 9의 F12 개발자 도구를 사용 하 여이 수행할 수 있습니다. Internet Explorer 9에서 누릅니다 **F12** 는 도구를 엽니다. 클릭 합니다 **네트워크** 누릅니다 탭 **캡처 시작**합니다. 이제 돌아가서 웹 페이지 및 키를 눌러 **F5** 웹 페이지를 다시 로드 합니다. Internet Explorer는 브라우저와 웹 서버 간에 HTTP 트래픽을 캡처합니다. 요약 보기 페이지의 모든 네트워크 트래픽을 보여 줍니다.

![](tutorial-your-first-web-api/_static/image14.png)

상대 URI에 대 한 항목을 찾습니다 "api/제품 /"입니다. 이 항목을 선택 하 고 클릭 **자세한 보기로 이동**합니다. 세부 정보 뷰에서 요청 및 응답 헤더 및 본문을 보려면 탭이 있습니다. 예를 들어를 클릭 하면 합니다 **요청 헤더** 탭에는 클라이언트 요청을 볼 수 있습니다 &quot;application/json&quot; Accept 헤더에 있습니다.

![](tutorial-your-first-web-api/_static/image15.png)

응답 본문 탭을 클릭 하면 제품 목록을 JSON으로 serialize 된 방법을 볼 수 있습니다. 다른 브라우저에 비슷한 기능이 있습니다. 또 다른 유용한 도구는 [Fiddler](http://www.fiddler2.com/fiddler2/), 웹 디버깅 프록시입니다. 사용할 수 있습니다 Fiddler HTTP 트래픽의 보려는 및 HTTP 요청을 작성 요청에서 HTTP 헤더에 대 한 모든 권한을 제공 하는.

## <a name="see-this-app-running-on-azure"></a>Azure에서 실행 되는이 앱 참조

라이브 웹 앱으로 실행 하는 완성 된 사이트를 참조 하 시겠습니까? 다음 단추를 클릭 하 여 Azure 계정에 앱의 전체 버전을 배포할 수 있습니다.

[![](https://azuredeploy.net/deploybutton.png)](https://deploy.azure.com/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebAPI-ProductsApp#/form/setup)

이 솔루션을 Azure에 배포 하려면 Azure 계정이 필요 합니다. 계정이 아직 없는 경우 다음 옵션:

- [Azure 계정을 무료로 개설](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) -크레딧을 받게 사용 하면 유료 Azure 서비스를 사용해볼 수 있습니다 하 고 사용한 후에 계정을 유지 하면 최대 사용 하 여 무료 Azure 서비스입니다.
- [MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) -MSDN 구독은 크레딧을 매달 제공 유료 Azure 서비스에 사용할 수 있는 합니다.

## <a name="next-steps"></a>다음 단계

- POST, PUT 및 DELETE 작업을 지원 하 고 데이터베이스에 기록 하는 HTTP 서비스의 자세한 예제를 보려면 [Entity Framework 6을 사용 하 여 Web API 2를 사용 하 여](../data/using-web-api-with-entity-framework/part-1.md)입니다.
- HTTP 서비스를 기반으로 유동성 및 응답성이 뛰어난 웹 응용 프로그램 만들기에 대 한 자세한 내용은 참조 하십시오 [ASP.NET 단일 페이지 응용 프로그램](../../../single-page-application/index.md)합니다.
- Azure App Service에 Visual Studio 웹 프로젝트를 배포 하는 방법에 대 한 정보를 참조 하세요 [Azure App Service에서 ASP.NET 웹 앱 만들기](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)합니다.
