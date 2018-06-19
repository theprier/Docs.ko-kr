---
uid: web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
title: ASP.NET Web API 2 (C#) 시작
author: MikeWasson
description: HTTP 웹 페이지를 제공 데 사용 되지 않습니다. 서비스 및 데이터를 노출 하는 Api를 구축 하기 위한 강력한 플랫폼 이기도 합니다. HTTP에는 단순, 유연 하 고, 및 ubiq는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/28/2017
ms.topic: article
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
msc.type: authoredcontent
ms.openlocfilehash: d881563cdb6449aada444ef0528061581113a925
ms.sourcegitcommit: 493a215355576cfa481773365de021bcf04bb9c7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
ms.locfileid: "29905038"
---
<a name="get-started-with-aspnet-web-api-2-c"></a>ASP.NET Web API 2 (C#) 시작
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트를 다운로드 합니다.](https://code.msdn.microsoft.com/Sample-code-of-Getting-c56ccb28)

HTTP 웹 페이지를 제공 데 사용 되지 않습니다. HTTP은 서비스 및 데이터를 노출 하는 Api를 구축 하기 위한 강력한 플랫폼 이기도 합니다. HTTP 쉽고 유연 하 고, 어디서 나 쉽게는입니다. 상상할 수 있는 거의 모든 플랫폼에는 HTTP 라이브러리를 HTTP 서비스에는 다양 한 브라우저, 모바일 장치 및 기존 데스크톱 응용 프로그램을 포함 한 클라이언트를 연결할 수 있으므로 합니다.
 
ASP.NET Web API는 웹 Api는.NET Framework를 기반으로 구축 하기 위한 프레임 워크. 이 자습서에서는 웹 제품 목록을 반환 하는 API를 만드는 데 ASP.NET Web API를 사용 합니다.

 
 ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
  
 - [Visual Studio 2017](https://www.visualstudio.com/downloads/)
 - Web API 2

참조 [ASP.NET Core와 Visual Studio for Windows는 web API를 만드는](https://docs.microsoft.com/aspnet/core/tutorials/first-web-api) 이 자습서의 최신 버전에 대 한 합니다.

## <a name="create-a-web-api-project"></a>웹 API 프로젝트 만들기

이 자습서에서는 웹 제품 목록을 반환 하는 API를 만드는 데 ASP.NET Web API를 사용 합니다. 프런트 엔드 웹 페이지 jQuery를 사용 하 여 결과 표시 합니다.

![](tutorial-your-first-web-api/_static/image1.png)

Visual Studio를 시작 하 고 선택 **새 프로젝트** 에서 **시작** 페이지. 또는에서 **파일** 메뉴 선택 **새로** 차례로 **프로젝트**합니다.

에 **템플릿** 창 선택 **설치 된 템플릿** 확장는 **Visual C#** 노드. 아래 **Visual C#** 선택, **웹**합니다. 프로젝트 템플릿 목록에서 선택 **ASP.NET 웹 응용 프로그램**합니다. "ProductsApp" 프로젝트 이름을 지정 하 고 클릭 **확인**합니다.

![](tutorial-your-first-web-api/_static/image2.png)

에 **새 ASP.NET 프로젝트** 대화 상자에서는 **빈** 서식 파일입니다. 아래 &quot;폴더 추가 및에 대 한 참조를 핵심&quot;, 확인 **웹 API**합니다. **확인**을 클릭합니다.

![](tutorial-your-first-web-api/_static/image3.png)

> [!NOTE]
> 사용 하 여 웹 API 프로젝트를 만들 수도 있습니다는 &quot;웹 API&quot; 템플릿. 웹 API 템플릿은 ASP.NET MVC를 사용 하 여 API 도움말 페이지를 제공 하기. MVC 없이 웹 API를 표시 하려는 때문에이 자습서에 빈 템플릿을 사용 합니다. 일반적으로 웹 API를 사용 하는 ASP.NET MVC 알 필요가 없습니다.


## <a name="adding-a-model"></a>모델 추가

*모델*은 응용 프로그램에서 데이터를 나타내는 개체입니다. ASP.NET Web API 자동으로 JSON, XML, 또는 다른 형식으로 모델을 직렬화 하 고 HTTP 응답 메시지의 본문에 serialize 된 데이터를 쓸 수 있습니다. 클라이언트에는 serialization 형식을 읽을 수,으로 개체를 역직렬화 할 수 있습니다. 대부분의 클라이언트에는 XML 또는 JSON 구문 분석할 수 있습니다. 또한 클라이언트는 HTTP 요청 메시지의 Accept 헤더를 설정 하 여 원하는 어떤 형식을 나타낼 수 있습니다.

제품을 나타내는 간단한 모델을 만들어 보겠습니다.

솔루션 탐색기 표시 되지 않는 경우 클릭는 **보기** 메뉴와 선택 **솔루션 탐색기**합니다. 솔루션 탐색기에서 모델 폴더를 마우스 오른쪽 단추로 클릭 합니다. 상황에 맞는 메뉴에서 선택 **추가** 다음 선택 **클래스**합니다.

![](tutorial-your-first-web-api/_static/image4.png)

클래스의 이름을 &quot;제품&quot;합니다. 다음 속성을 추가 `Product` 클래스입니다.

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample1.cs)]

## <a name="adding-a-controller"></a>컨트롤러 추가

웹 API에는 *컨트롤러* 는 HTTP 요청을 처리 하는 개체입니다. 제품 목록 또는 ID로 지정 된 단일 제품 중 하나를 반환할 수 있는 컨트롤러 추가

> [!NOTE]
> ASP.NET MVC를 사용한 경우 이미 잘 알고 있다면 컨트롤러입니다. Web API 컨트롤러 MVC 컨트롤러 유사 하지만 상속 된 **ApiController** 클래스 대신는 **컨트롤러** 클래스입니다.

**솔루션 탐색기**, Controllers 폴더를 마우스 오른쪽 단추로 클릭 합니다. 선택 **추가** 선택한 후 **컨트롤러**합니다.

![](tutorial-your-first-web-api/_static/image5.png)

에 **추가 스 캐 폴드** 대화 상자에서 **웹 API 컨트롤러-비어 있지**합니다. **추가**를 클릭합니다.

![](tutorial-your-first-web-api/_static/image6.png)

에 **컨트롤러 추가** 대화 상자에서 컨트롤러 이름 &quot;ProductsController&quot;합니다. **추가**를 클릭합니다.

![](tutorial-your-first-web-api/_static/image7.png)

스 캐 폴딩을 ProductsController.cs Controllers 폴더의 명명 된 파일을 만듭니다.

![](tutorial-your-first-web-api/_static/image8.png)

> [!NOTE]
> 컨트롤러에 컨트롤러 이라는 폴더에 넣이 필요가 없습니다. 폴더 이름은 원본 파일을 구성 하는 편리한 방법인을입니다.


이 파일이 열려 있지 않으면 이미 열려는 파일을 두 번 클릭 합니다. 이 파일에 코드를 다음으로 바꿉니다.

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample2.cs)]

예를 간단히 유지 하기 위해 제품 컨트롤러 클래스의 내부 고정된 배열에 저장 됩니다. 물론, 실제 응용 프로그램에서 데이터베이스를 쿼리 또는 다른 외부 데이터 소스를 사용 하 여가 있습니다.

컨트롤러는 제품을 반환 하는 두 개의 메서드를 정의 합니다.

- `GetAllProducts` 메서드로 제품의 전체 목록을 반환는 **IEnumerable&lt;제품&gt;**  유형입니다.
- `GetProduct` 단일 제품의 id를 조회 메서드

정말 간단하죠. 작업 중인 웹 API 해야합니다. 컨트롤러의 각 메서드에 하나 이상의 Uri에 해당합니다.

| 컨트롤러 메서드 | URI |
| --- | --- |
| GetAllProducts | / api/제품 |
| GetProduct | /api/products/*id* |

에 대 한는 `GetProduct` 메서드는 *id* URI에 자리 표시자입니다. 예를 들어 ID 5 인 제품을 가져오려면 URI는 `api/products/5`합니다.

Web API 컨트롤러 메서드를 HTTP 요청을 라우팅하 하는 방법에 대 한 자세한 내용은 참조 [ASP.NET Web API에서 라우팅](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)합니다.

## <a name="calling-the-web-api-with-javascript-and-jquery"></a>Javascript 및 jQuery를 사용 하 여 웹 API를 호출합니다.

이 섹션에서는 AJAX를 사용 하 여 web API를 호출 하는 HTML 페이지를 추가 합니다. JQuery AJAX 호출을 수행 하 고 결과 페이지를 업데이트 하려면 사용 합니다.

솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가**을 선택한 후 **새 항목**합니다.

![](tutorial-your-first-web-api/_static/image9.png)

에 **새 항목 추가** 대화 상자에서는 **웹** 노드 아래의 **Visual C#** 를 선택한 후는 **HTML 페이지** 항목입니다. 페이지 이름을 &quot;index.html&quot;합니다.

![](tutorial-your-first-web-api/_static/image10.png)

이 파일의 모든 개체를 다음과 같이 바꿉니다.

[!code-html[Main](tutorial-your-first-web-api/samples/sample3.html)]

여러 가지 방법으로 jQuery를 가져올 수 있습니다. 이 예에서 사용 된 [Microsoft Ajax CDN](../../../ajax/cdn/overview.md)합니다. 다운로드할 수도 있습니다 [ http://jquery.com/ ](http://jquery.com/), 및 "웹 API" ASP.NET 프로젝트 템플릿에 jQuery도 포함 됩니다.

### <a name="getting-a-list-of-products"></a>제품 목록 가져오기

제품 목록이 받으려면 다음으로 HTTP GET 요청을 보내 &quot;/api/제품&quot;합니다.

JQuery [getJSON](http://api.jquery.com/jQuery.getJSON/) 함수 AJAX 요청을 보냅니다. 응답에 대 한 JSON 개체 배열을 포함합니다. `done` 함수 요청이 성공 하면 호출 되는 콜백을 지정 합니다. 콜백에서 제품 정보 DOM 업데이트 됩니다.

[!code-html[Main](tutorial-your-first-web-api/samples/sample4.html)]

### <a name="getting-a-product-by-id"></a>ID 별로 제품 가져오기

ID 별로 제품을 받으려면 다음으로 HTTP GET 요청을 보내 &quot;/api/제품/*id*&quot;여기서 *id* 제품 ID입니다.

[!code-javascript[Main](tutorial-your-first-web-api/samples/sample5.js)]

여전히 호출 `getJSON` AJAX 요청 하지만이 이번에 보내도록 요청 URI의에서 ID 입력 합니다. 이 요청은 응답에는 단일 제품의 JSON 표현입니다.

## <a name="running-the-application"></a>응용 프로그램 실행

F5 키를 눌러 응용 프로그램 디버깅을 시작 합니다. 웹 페이지는 다음과 같이 표시 됩니다.

![](tutorial-your-first-web-api/_static/image11.png)

제품 id를 얻으려면 ID를 입력 하 고 선택은 취소:

![](tutorial-your-first-web-api/_static/image12.png)

잘못 된 ID를 입력 하면 서버에서 HTTP 오류를 반환 합니다.

![](tutorial-your-first-web-api/_static/image13.png)

## <a name="using-f12-to-view-the-http-request-and-response"></a>F12 키를 사용 하 여 HTTP 요청 및 응답을 보려면

HTTP 서비스를 사용 하는 경우에 HTTP 요청을 보고 요청 메시지에 매우 유용할 수 있습니다. Internet Explorer 9의 F12 개발자 도구를 사용 하 여이 수행할 수 있습니다. Internet Explorer 9에서 누릅니다 **F12** 는 도구를 엽니다. 클릭는 **네트워크** 탭 및 키를 눌러 **캡처 시작**합니다. 웹 페이지 및 키를 눌러로 돌아가서 이제 **F5** 웹 페이지를 다시 로드 합니다. Internet Explorer 브라우저와 웹 서버 사이의 HTTP 트래픽을 캡처합니다. 요약 보기에는 페이지에 대 한 모든 네트워크 트래픽을 표시합니다.

![](tutorial-your-first-web-api/_static/image14.png)

상대 URI에 대 한 항목을 찾습니다 "api/제품 /"입니다. 이 항목을 선택 하 고 클릭 **자세히 보기로 이동**합니다. 세부 정보 뷰에서 요청 및 응답 헤더 및 본문을 보려면 탭이 있습니다. 예를 들어, 클릭는 **요청 헤더** 탭에서 클라이언트 요청 됨을 확인할 수 있습니다 &quot;응용 프로그램/json&quot; Accept 헤더에 있습니다.

![](tutorial-your-first-web-api/_static/image15.png)

응답 본문 탭을 클릭 하면 JSON으로 제품 목록을 serialize 하는 방법을 확인할 수 있습니다. 다른 브라우저에 비슷한 기능이 있습니다. 또 다른 유용한 도구는 [Fiddler](http://www.fiddler2.com/fiddler2/), 웹 디버깅 프록시입니다. 사용할 수 있습니다 Fiddler HTTP 트래픽을 볼 수 및 HTTP 요청을 작성 하 요청에 HTTP 헤더에 대 한 모든 권한을 제공.

## <a name="see-this-app-running-on-azure"></a>Azure에서 실행 되는이 응용 프로그램 참조

실시간 웹 앱으로 실행 하는 완료 된 사이트를 참조 하 시겠습니까? 다음 단추 클릭 하 여 Azure 계정에 완전 한 버전의 앱을 배포할 수 있습니다.

[![](http://azuredeploy.net/deploybutton.png)](https://deploy.azure.com/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebAPI-ProductsApp#/form/setup)

Azure에이 솔루션을 배포 하려면 Azure 계정이 필요 합니다. 계정이 아직 없는 경우 다음 옵션:

- [무료 Azure 계정을 개설](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) -크레딧을 얻게 유료 Azure 서비스를 실행 해 사용할 수 있으며, 사용 후에 최대 계정 등에 사용 가능한 Azure 서비스입니다.
- [MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) -Your MSDN을 구독 하면 크레딧 매달 유료 Azure 서비스에 사용할 수 있습니다.

## <a name="next-steps"></a>다음 단계

- POST, PUT 및 DELETE 작업을 지원 하 고 데이터베이스에 기록 하는 HTTP 서비스의 자세한 예제를 참조 하십시오. [Entity Framework 6와 Web API 2를 사용 하 여](../data/using-web-api-with-entity-framework/part-1.md)합니다.
- HTTP 서비스를 기반으로 유동성 및 응답성이 뛰어난 웹 응용 프로그램을 만드는 방법에 대 한 자세한 내용은 [ASP.NET 단일 페이지 응용 프로그램](../../../single-page-application/index.md)합니다.
- Azure 앱 서비스를 Visual Studio 웹 프로젝트를 배포 하는 방법에 대 한 정보를 참조 하십시오. [Azure 앱 서비스에서 ASP.NET 웹 앱을 만들](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)합니다.
