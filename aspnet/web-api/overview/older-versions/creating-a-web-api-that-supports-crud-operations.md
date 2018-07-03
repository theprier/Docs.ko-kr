---
uid: web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations
title: ASP.NET Web API 1에서에서 CRUD 작업을 사용 하도록 설정 | Microsoft Docs
author: MikeWasson
description: 이 자습서에서는 ASP.NET Web API를 사용 하 여 HTTP 서비스에서 CRUD 작업을 지 원하는 방법을 보여 줍니다. 소프트웨어 버전 자습서 Visual Studio 2012 웹 AP에서 사용 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/28/2012
ms.topic: article
ms.assetid: c125ca47-606a-4d6f-a1fc-1fc62928af93
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations
msc.type: authoredcontent
ms.openlocfilehash: 1658e120225cd3c9425168238981133c96ff398a
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37402930"
---
<a name="enabling-crud-operations-in-aspnet-web-api-1"></a>ASP.NET Web API 1에서에서 CRUD 작업을 사용 하도록 설정
====================
[Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트 다운로드](http://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-c4761894)

> 이 자습서에서는 ASP.NET Web API를 사용 하 여 HTTP 서비스에서 CRUD 작업을 지 원하는 방법을 보여 줍니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
> 
> 
> - Visual Studio 2012
> - Web API 1 (또한 Web API 2를 사용 하 여 작동)


CRUD &quot;만들기, 읽기, 업데이트 및 삭제,&quot; 는 4 개의 기본 데이터베이스 작업입니다. 많은 HTTP 서비스는도 비슷한 REST Api 또는 REST를 통해 CRUD 작업을 모델링합니다.

이 자습서에서는 매우 간단한 web API 제품 목록을 관리를 빌드합니다. 각 제품 이름, 가격 및 범주에 포함 됩니다 (같은 &quot;toys&quot; 하거나 &quot;하드웨어&quot;), plus 제품 id입니다.

제품 API는 다음 메서드 노출 합니다.

| 작업 | HTTP 메서드 | 상대 URI |
| --- | --- | --- |
| 모든 제품의 목록 가져오기 | 가져오기 | api 제품 |
| 제품 ID 별로 가져오기 | 가져오기 | /api/products/*id* |
| 제품 범주별으로 가져오기 | 가져오기 | /api/products?category=*category* |
| 새 제품 만들기 | 올리기 | api 제품 |
| 제품 업데이트 | PUT | /api/products/*id* |
| 제품 삭제 | Delete | /api/products/*id* |

경로 있는 제품 ID를 포함 된 Uri의 일부를 확인 합니다. 예를 들어, 제품 ID가 28을 가져오려면 클라이언트에서 보냅니다 GET 요청에 대 한 `http://hostname/api/products/28`합니다.

### <a name="resources"></a>자료

API 제품 두 리소스 유형에 대 한 Uri를 정의 합니다.

| 리소스 | URI |
| --- | --- |
| 모든 제품의 목록입니다. | api 제품 |
| 개별 제품입니다. | /api/products/*id* |

### <a name="methods"></a>메서드

네 가지 주요 HTTP 메서드 (GET, PUT, POST 및 DELETE)는 다음과 같은 CRUD 작업에 매핑할 수 있습니다.

- 가져오기에 지정된 된 URI에서 리소스의 표현을 검색합니다. GET 서버에 파생 작업이 있어야 합니다.
- PUT은 지정된 된 URI에서 리소스를 업데이트합니다. 이 서버에 새 Uri를 지정 하는 클라이언트에서는 PUT 지정된 된 URI에 새 리소스를 만드는 데도 사용할 수 있습니다. 이 자습서에서는 API는 PUT 통해 만들기를 지원 하지 않습니다.
- 게시물에는 새 리소스를 만듭니다. 서버는 새 개체에 대 한 URI를 할당 하 고 응답 메시지의 일부로이 URI를 반환 합니다.
- 삭제 지정된 된 URI에서 리소스를 삭제합니다.

참고: PUT 메서드는 전체 제품 엔터티를 바꿉니다. 즉, 클라이언트는 업데이트 된 제품의 완전 한 표현이 전송 해야 합니다. 부분 업데이트를 지원 하려는 경우 PATCH 메서드를 사용 하는 것이 좋습니다. 이 자습서는 패치를 구현 하지 않습니다.

## <a name="create-a-new-web-api-project"></a>새 웹 API 프로젝트 만들기

선택한 Visual Studio를 실행 하 여 시작 **새 프로젝트** 에서 합니다 **시작** 페이지입니다. 또는에서 **파일** 메뉴에서 **새로 만들기** 차례로 **프로젝트**합니다.

에 **템플릿** 창 **설치 된 템플릿** 확장 하 고는 **Visual C#** 노드. 아래 **Visual C#** 를 선택 **웹**합니다. 프로젝트 템플릿 목록에서 선택 **ASP.NET MVC 4 웹 응용 프로그램**합니다. 프로젝트 이름을 &quot;ProductStore&quot; 누릅니다 **확인**합니다.

![](creating-a-web-api-that-supports-crud-operations/_static/image1.png)

에 **새 ASP.NET MVC 4 프로젝트** 대화 상자에서 **Web API** 클릭 **확인**합니다.

![](creating-a-web-api-that-supports-crud-operations/_static/image2.png)

## <a name="adding-a-model"></a>모델 추가

*모델*은 응용 프로그램에서 데이터를 나타내는 개체입니다. ASP.NET Web API에서 강력한 형식의 CLR 개체로 사용 하 여 모델을 하 고 이러한을 자동으로 직렬화할지 XML 또는 JSON을 클라이언트에 대 한 합니다.

ProductStore API에 대 한 데이터 제품 구성, 라는 새 클래스를 만들어 보겠습니다 `Product`합니다.

솔루션 탐색기 표시 되지 않으면 클릭 합니다 **뷰** 선택한 메뉴 **솔루션 탐색기**합니다. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 합니다 **모델** 폴더입니다. 상황에 맞는 맞는 선택할 **추가**을 선택한 후 **클래스**합니다. 클래스의 이름을 &quot;제품&quot;합니다.

![](creating-a-web-api-that-supports-crud-operations/_static/image3.png)

다음 속성을 추가 합니다 `Product` 클래스입니다.

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample1.cs)]

## <a name="adding-a-repository"></a>리포지토리 추가

제품의 컬렉션을 저장 해야 합니다. 서비스 구현에서 컬렉션을 분리 하는 것이 좋습니다. 이런 방식으로 백업 저장소 서비스 클래스를 다시 작성 하지 않고 변경할 수 있습니다. 이러한 유형의 설계 라고 합니다 *리포지토리* 패턴입니다. 리포지토리에 대 한 제네릭 인터페이스를 정의 하 여 시작 합니다.

솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 합니다 **모델** 폴더입니다. 선택 **추가**을 선택한 후 **새 항목**합니다.

![](creating-a-web-api-that-supports-crud-operations/_static/image4.png)

에 **템플릿을** 창 **설치 된 템플릿** C# 노드를 확장 합니다. C#에서 선택 **코드**합니다. 코드 템플릿 목록에서 선택 **인터페이스**합니다. 인터페이스의 이름을 &quot;IProductRepository&quot;합니다.

![](creating-a-web-api-that-supports-crud-operations/_static/image5.png)

다음 구현을 추가 합니다.

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample2.cs)]

이제 다른 클래스 라는 Models 폴더를 추가 &quot;ProductRepository 합니다.&quot; 이 클래스는 `IProductRespository` 인터페이스를 구현합니다. 다음 구현을 추가 합니다.

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample3.cs)]

로컬 메모리에 유지 하는 저장소입니다. 이 자습서의 경우 되지만 실제 응용 프로그램에서 데이터를 외부에서 두 데이터베이스를 저장할 수 있습니다 또는 클라우드 저장소입니다. 리포지토리 패턴 구현을 변경 합니다. 나중에 쉽게 됩니다.

## <a name="adding-a-web-api-controller"></a>웹 API 컨트롤러 추가

ASP.NET MVC를 사용 하 여 보았다면 다음 이미 잘 알고 있다면 컨트롤러를 사용 하 여 합니다. ASP.NET Web API에는 *컨트롤러* 클라이언트로부터 HTTP 요청을 처리 하는 클래스입니다. 새 프로젝트 마법사는 프로젝트를 만들 때 두 컨트롤러를 만들었습니다. 이러한 작업을 확인 하려면 솔루션 탐색기에서 컨트롤러 폴더를 확장 합니다.

- HomeController는 기존 ASP.NET MVC 컨트롤러입니다. 사이트에 대 한 HTML 페이지를 제공 하는 일을 담당 하며 웹 API 직접 관련이 없습니다.
- ValuesController 예제 WebAPI 컨트롤러를 경우

계속 해 서 ValuesController, 솔루션 탐색기에서 파일을 마우스 오른쪽 단추로 클릭 하 고 선택 하 여 삭제 **삭제 합니다.** 이제 다음과 같이 새 컨트롤러를 추가 합니다.

**솔루션 탐색기**, Controllers 폴더를 마우스 오른쪽 단추로 클릭 합니다. 선택 **추가** 선택한 후 **컨트롤러**합니다.

![](creating-a-web-api-that-supports-crud-operations/_static/image6.png)

에 **컨트롤러 추가** 마법사에서 컨트롤러 이름 &quot;ProductsController&quot;합니다. 에 **템플릿을** 드롭 다운 목록에서 **빈 API 컨트롤러**합니다. **추가**를 클릭합니다.

![](creating-a-web-api-that-supports-crud-operations/_static/image7.png)

> [!NOTE]
> 프로그램 contollers 컨트롤러 라는 폴더에 배치 하는 데 필요한 것입니다. 폴더 이름은 중요 하지 않습니다. 원본 파일을 구성 하려면 편리한 방법일 뿐 이며


합니다 **컨트롤러 추가** Controllers 폴더에서 ProductsController.cs 라는 파일을 자동으로 만들어집니다. 이 파일이 열려 있지 않으면 이미를 열려는 파일을 두 번 클릭 합니다. 다음을 추가 합니다 **를 사용 하 여** 문:

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample4.cs)]

보유 하는 필드를 추가 하는 **IProductRepository** 인스턴스.

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample5.cs)]

> [!NOTE]
> 호출 `new ProductRepository()` 컨트롤러의 아니므로 가장 적합 한 디자인의 특정 구현에 컨트롤러 통제 `IProductRepository`합니다. 더 나은 방법은 참조 하세요 [웹 API 종속성 확인자를 사용 하 여](../advanced/dependency-injection.md)입니다.


## <a name="getting-a-resource"></a>리소스 가져오기

여러 ProductStore API 노출 &quot;읽을&quot; HTTP GET 메서드를 사용 하 여 작업 합니다. 각 작업의 메서드에 해당 합니다 `ProductsController` 클래스입니다.

| 작업 | HTTP 메서드 | 상대 URI |
| --- | --- | --- |
| 모든 제품의 목록 가져오기 | 가져오기 | api 제품 |
| 제품 ID 별로 가져오기 | 가져오기 | /api/products/*id* |
| 제품 범주별으로 가져오기 | 가져오기 | /api/products?category=*category* |

모든 제품의 목록을 가져오려면이 메서드를 추가 합니다 `ProductsController` 클래스:

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample6.cs)]

메서드 이름을 사용 하 여 시작 &quot;가져올&quot;이므로 규칙에 따라 GET 요청에 매핑됩니다. 또한 메서드 매개 변수가 없으면 때문에 매핑될 없는 URI는 *&quot;id&quot;* 경로의 세그먼트입니다.

제품 ID 가져오려면이 메서드를 추가 합니다 `ProductsController` 클래스:

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample7.cs)]

이 메서드 이름을 사용 하 여 시작 &quot;가져옵니다&quot;, 메서드 라는 매개 변수를 되었지만 *id*합니다. 이 매개 변수에 매핑되는 &quot;id&quot; URI 경로의 세그먼트입니다. ASP.NET Web API 프레임 워크를 자동으로 ID는 올바른 데이터 형식으로 변환 (**int**) 매개 변수입니다.

GetProduct 메서드 형식의 예외를 throw **HttpResponseException** 하는 경우 *id* 올바르지 않습니다. 이 예외는 404 (찾을 수 없음) 오류가 프레임 워크에 의해 변환 됩니다.

마지막으로 범주별으로 제품을 검색 하는 메서드를 추가 합니다.

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample8.cs)]

요청 URI 쿼리 문자열에 있으면 웹 API 컨트롤러 메서드에 매개 변수가 쿼리 매개 변수를 찾으려고 합니다. 따라서 폼의 URI "api/제품? category =*범주*"이 메서드에 매핑됩니다.

## <a name="creating-a-resource"></a>리소스 만들기

다음으로 메서드를 추가한는 `ProductsController` 새 제품을 만드는 클래스입니다. 메서드의 간단한 구현을 다음과 같습니다.

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample9.cs)]

이 메서드에 대 한 두 참고 사항은 다음과 같습니다.

- 메서드 이름을 사용 하 여 시작 &quot;게시 하는 중... &quot;. 클라이언트는 새 제품을 만들려면 HTTP POST 요청을 보냅니다.
- 메서드는 제품 형식의 매개 변수를 사용 합니다. Web API에서 복합 형식으로 매개 변수는 요청 본문에서 deserialize 됩니다. 따라서 제품 개체의 serialize 된 표현에 XML 또는 JSON 형식으로 보내도록 클라이언트를 기대 합니다.

이 구현에서 작동 하지만 매우 완전 하지 않습니다. 이상적으로 다음과 같습니다에 대 한 HTTP 응답을 싶습니다.

- **응답 코드:** 응답 상태 코드 200 (정상)를 Web API 프레임 워크 기본적으로 설정 합니다. 하지만 HTTP/1.1 프로토콜에 따라 리소스를 만드는 POST 요청을 생성 하는 경우 서버 회신 해야 함 상태 201 (만들어짐).
- **위치:** 응답의 Location 헤더에 새 리소스의 URI를 포함 해야 서버 리소스를 만들 때.

ASP.NET Web API 쉽게 HTTP 응답 메시지를 조작할 수 있습니다. 향상 된 구현은 다음과 같습니다.

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample10.cs)]

메서드 반환 형식을 이제는 **HttpResponseMessage**합니다. 반환 하 여는 **HttpResponseMessage** 제품을 대신 상태 코드 및 Location 헤더를 포함 하 여 HTTP 응답 메시지의 세부 정보를 제어할 수 있습니다.

합니다 **CreateResponse** 메서드를 만듭니다를 **HttpResponseMessage** 자동으로 본문에 직렬화 된 표현을 Product 개체를 작성 및 fo 응답 메시지입니다.

> [!NOTE]
> 이 예제에서는 유효성을 검사 하지 않습니다는 `Product`합니다. 모델 유효성 검사에 대 한 자세한 내용은 [ASP.NET Web API의 모델 유효성 검사](../formats-and-model-binding/model-validation-in-aspnet-web-api.md)합니다.


## <a name="updating-a-resource"></a>리소스 업데이트

PUT을 사용 하 여 제품을 업데이트 하는 것은 간단 합니다.

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample11.cs)]

메서드 이름을 사용 하 여 시작 &quot;배치 하는 중... &quot;이므로 PUT 요청에 Web API와 일치 합니다. 메서드는 두 개의 매개 변수, 제품 ID 및 업데이트 된 제품입니다. 합니다 *id* 매개 변수는 URI 경로에서 가져온 것 하며 *제품* 요청 본문에서 deserialize 되는 매개 변수입니다. 기본적으로 ASP.NET Web API 프레임 워크는 경로에서 간단한 매개 변수 형식 및 요청 본문에서 복합 형식을 사용 합니다.

## <a name="deleting-a-resource"></a>리소스를 삭제합니다.

resourse를 삭제 하려면 "삭제 중..." 메서드를 정의 합니다.

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample12.cs)]

삭제 요청에 성공 하면; 상태를 설명 하는 엔터티 본문을 사용 하 여 200 (정상) 상태를 반환할 수 것 상태 202 (수락)를 삭제 하는 여전히 보류 중이면 또는 상태 엔터티 본문 없이 204 (내용 없음). 이 경우에 `DeleteProduct` 메서드가 `void` 반환 형식, 하므로 ASP.NET Web API 자동으로 변환이 상태 코드 204 (내용 없음).
