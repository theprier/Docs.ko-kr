---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
title: Web API 2 OData v3 엔드포인트 만들기 | Microsoft Docs
author: MikeWasson
description: Open Data Protocol (OData)는 웹에 대 한 데이터 액세스 프로토콜. OData는 데이터 구조, 데이터를 쿼리 및 데이터를 조작 하는 일관 된 방식을 제공 하는 중...
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 262843d6-43a2-4f1c-82d9-0b90ae6df0cf
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
msc.type: authoredcontent
ms.openlocfilehash: 2e0d3b45fd51192d227d852dc2f05b45ca42944c
ms.sourcegitcommit: a4dcca4f1cb81227c5ed3c92dc0e28be6e99447b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2018
ms.locfileid: "48910917"
---
<a name="creating-an-odata-v3-endpoint-with-web-api-2"></a>Web API 2 OData v3 엔드포인트 만들기
====================
[Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트 다운로드](http://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> 합니다 [개방형 데이터 프로토콜](http://www.odata.org/) 는 웹에 대 한 데이터 액세스 프로토콜 (OData). OData는 데이터 구조, 데이터를 쿼리하고, CRUD 작업을 통해 데이터 집합을 조작 하는 일관 된 방식을 제공 (만들기, 읽기, 업데이트 및 삭제). OData는 AtomPub (XML) 및 JSON 형식 모두를 지원합니다. OData는 데이터에 대 한 메타 데이터를 노출 하는 방법을 정의 합니다. 클라이언트 메타 데이터를 사용 하 여 형식 정보 및 데이터 집합에 대 한 관계를 검색할 수 있습니다.
>
> ASP.NET Web API 쉽게 데이터 집합에 대 한 OData 끝점을 만듭니다. 끝점이 지 원하는 OData 작업 정확 하 게 제어할 수 있습니다. 비 OData 끝점와 함께 여러 OData 끝점을 호스트할 수 있습니다. 데이터 모델, 백 엔드 비즈니스 논리 및 데이터 계층을 통해 전체 제어를 해야합니다.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - Web API 2
> - OData 버전 3
> - Entity Framework 6
> - [Fiddler 웹 디버깅 프록시 (선택 사항)](http://www.fiddler2.com)
>
> Web API OData 지원에서 추가한 [ASP.NET 및 Web Tools 2012.2 업데이트](https://go.microsoft.com/fwlink/?LinkId=282650)합니다. 그러나이 자습서에서는 Visual Studio 2013에 추가 된 스 캐 폴딩 합니다.


이 자습서에서는 클라이언트가 쿼리할 수 있는 간단한 OData 끝점을 만들게 됩니다. 또한 끝점에 대 한 C# 클라이언트를 만듭니다. 이 자습서를 완료 한 후 다음 일련의 자습서 엔터티 관계 작업을 포함 하 여 더 많은 기능을 추가 하는 방법을 표시 하 고 확장 하 고 $/ $선택 합니다.

- [Visual Studio 프로젝트 만들기](#create-project)
- [엔터티 모델 추가](#add-model)
- [OData 컨트롤러 추가](#add-controller)
- [EDM 및 경로 추가 합니다.](#edm)
- [(선택 사항) 데이터베이스 시드](#seed-db)
- [OData 끝점을 탐색](#explore)
- [OData 직렬화 형식](#formats)

<a id="create-project"></a>
## <a name="create-the-visual-studio-project"></a>Visual Studio 프로젝트 만들기

이 자습서에서는 기본 CRUD 작업을 지 원하는 OData 끝점에 만들어집니다. 끝점에는 제품 목록을 단일 리소스를 노출 합니다. 나중에 자습서 더 많은 기능을 추가 합니다.

Visual Studio를 시작 하 고 선택 **새 프로젝트** 시작 페이지에서. 또는에서 **파일** 메뉴에서 **새로 만들기** 차례로 **프로젝트**합니다.

에 **템플릿을** 창 **설치 된 템플릿** Visual C# 노드를 확장 합니다. 아래 **Visual C#** 를 선택 **웹**합니다. 선택 **ASP.NET 웹 응용 프로그램** 템플릿.

![](creating-an-odata-endpoint/_static/image1.png)

에 **새 ASP.NET 프로젝트** 대화 상자에서 선택 합니다 **빈** 템플릿. 아래 &quot;폴더를 추가 하 고 핵심에 대 한 참조 하는 중... &quot;를 확인 **Web API**합니다. **확인**을 클릭합니다.

![](creating-an-odata-endpoint/_static/image2.png)

<a id="add-model"></a>
## <a name="add-an-entity-model"></a>엔터티 모델 추가

*모델*은 응용 프로그램에서 데이터를 나타내는 개체입니다. 이 자습서에서는 제품을 나타내는 모델이 필요 합니다. 모델 형식에 해당 하는 OData 엔터티.

솔루션 탐색기에서 Models 폴더를 마우스 오른쪽 단추로 클릭 합니다. 상황에 맞는 메뉴에서 선택 **추가** 선택한 **클래스**합니다.

![](creating-an-odata-endpoint/_static/image3.png)

에 **새로 추가** 항목 대화 상자, 클래스의 이름을 &quot;제품&quot;합니다.

![](creating-an-odata-endpoint/_static/image4.png)

> [!NOTE]
> 규칙에 따라 모델 클래스는 Models 폴더에 배치 됩니다. 사용자의 프로젝트에서이 규칙을 따르는 없지만이 자습서로 사용 됩니다.


Product.cs 파일에서 다음 클래스 정의 추가 합니다.

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample1.cs)]

ID 속성이 엔터티 키가 됩니다. 클라이언트 ID로 제품을 쿼리할 수 있습니다. 이 필드는 백 엔드 데이터베이스의 기본 키 수도 있습니다.

이제 프로젝트를 빌드하십시오. 다음 단계에서는 제품 형식을 찾기 위해 리플렉션을 사용 하는 몇 가지 Visual Studio 스 캐 폴딩을 사용 하겠습니다.

<a id="add-controller"></a>
## <a name="add-an-odata-controller"></a>OData 컨트롤러 추가

A *컨트롤러* 는 HTTP 요청을 처리 하는 클래스입니다. OData 서비스에서 설정 하는 각 엔터티에 대해 별도 컨트롤러를 정의 합니다. 이 자습서에서는 단일 컨트롤러를 만들겠습니다.

솔루션 탐색기에서 컨트롤러 폴더를 마우스 오른쪽 단추로 클릭 합니다. 선택 **추가** 선택한 후 **컨트롤러**합니다.

![](creating-an-odata-endpoint/_static/image5.png)

에 **스 캐 폴드 추가** 대화 상자에서 &quot;Web API 2 OData 컨트롤러 작업을 사용 하 여 Entity Framework를 사용 하 여&quot;입니다.

![](creating-an-odata-endpoint/_static/image6.png)

에 **컨트롤러 추가** 대화 상자에서 이름 "ProductsController" 컨트롤러입니다. 선택 된 &quot;비동기 컨트롤러 동작을 사용 하 여&quot; 확인란을 선택 합니다. 에 **모델** 드롭 다운 목록에서 Product 클래스를 선택 합니다.

![](creating-an-odata-endpoint/_static/image7.png)

클릭 된 **새 데이터 컨텍스트...**  단추입니다. 데이터 컨텍스트 형식에 대 한 기본 이름을 그대로 두고 클릭 **추가**합니다.

![](creating-an-odata-endpoint/_static/image8.png)

컨트롤러를 추가 하려면 컨트롤러 추가 대화 상자에서 추가 클릭 합니다.

![](creating-an-odata-endpoint/_static/image9.png)

참고: 라는 오류 메시지가 표시 &quot;형식을 가져오는 동안 오류가 발생 했습니다... &quot;, Product 클래스를 추가한 후 Visual Studio 프로젝트를 빌드 되었는지 확인 합니다. 스 캐 폴딩의 리플렉션을 사용 하 여 클래스를 찾습니다.

![](creating-an-odata-endpoint/_static/image10.png)

스 캐 폴딩을 프로젝트에 두 개의 코드 파일을 추가 합니다.

- Products.cs는 OData 끝점을 구현 하는 Web API 컨트롤러를 정의 합니다.
- ProductServiceContext.cs는 Entity Framework를 사용 하 여 기본 데이터베이스를 쿼리 하는 메서드를 제공 합니다.

![](creating-an-odata-endpoint/_static/image11.png)

<a id="edm"></a>
## <a name="add-the-edm-and-route"></a>EDM 및 경로 추가 합니다.

솔루션 탐색기에서 앱 확장\_폴더를 시작 하 고 WebApiConfig.cs 파일을 엽니다. 이 클래스는 웹 API에 대 한 구성 코드를 포함합니다. 이 코드를 다음으로 바꿉니다.

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample2.cs)]

이 코드는 두 가지를 수행합니다.

- OData 끝점에 대 한 엔터티 데이터 모델 (EDM)를 만듭니다.
- 끝점에 대 한 경로 추가합니다.

EDM은 데이터의 추상적 모델입니다. EDM 메타 데이터 문서를 만들고 서비스에 대 한 Uri를 정의 됩니다. 합니다 **ODataConventionModelBuilder** EDM 기본 명명 규칙의 집합을 사용 하 여 EDM을 만듭니다. 이 방법은 최소한의 코드에 필요합니다. EDM 통해 더 많은 제어를 원하는 경우 사용할 수 있습니다 합니다 **된 ODataModelBuilder** 속성, 키 및 탐색 속성을 명시적으로 추가 하 여 EDM을 만들려면 클래스입니다.

합니다 **EntitySet** 메서드는 엔터티 집합 EDM을 추가 합니다.

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample3.cs)]

문자열 "제품" 엔터티 집합의 이름을 정의합니다. 컨트롤러의 이름에는 엔터티 집합의 이름과 일치 해야 합니다. 이 자습서에서는 엔터티 집합 이름은 "제품" 및 컨트롤러 라는 `ProductsController`합니다. 명명 된 엔터티 집합 "ProductSet", 컨트롤러 이름을 `ProductSetController`입니다. 끝점에 여러 엔터티 집합에 있을 수 있음을 참고 합니다. 호출 **EntitySet&lt;T&gt;**  각 엔터티에 대 한 설정 및 해당 컨트롤러를 정의 합니다.

합니다 **MapODataRoute** 메서드 OData 끝점에 대 한 경로 추가 합니다.

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample4.cs)]

첫 번째 매개 변수는 경로의 이름입니다. 서비스의 클라이언트가이 이름은 표시 되지 않습니다. 두 번째 매개 변수는 끝점에 대 한 URI 접두사입니다. 이 코드를 지정 하는, Products 엔터티 집합에 대 한 URI가 http://<em>hostname</em>odata/제품입니다. 응용 프로그램에 OData 끝점을 둘 이상 있을 수 있습니다. 각 끝점에 대 한 호출 <strong>MapODataRoute</strong> 고유 경로 이름 및 고유한 URI 접두사를 제공 합니다.

<a id="seed-db"></a>
## <a name="seed-the-database-optional"></a>(선택 사항) 데이터베이스 시드

이 단계에서는 일부 테스트 데이터를 사용 하 여 데이터베이스를 시드하려면 Entity Framework를 사용 합니다. 이 단계는 선택 사항이 있지만 OData 끝점을 즉시 테스트할 수 있습니다.

**도구** 메뉴에서 **NuGet 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다. 패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

[!code-console[Main](creating-an-odata-endpoint/samples/sample5.cmd)]

이 마이그레이션 및 Configuration.cs 라는 코드 파일 이라는 폴더를 추가 합니다.

![](creating-an-odata-endpoint/_static/image12.png)

이 파일을 열고 다음 코드를 추가 합니다 `Configuration.Seed` 메서드.

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample6.cs)]

패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

[!code-console[Main](creating-an-odata-endpoint/samples/sample7.cmd)]

이러한 명령은 데이터베이스를 만들고 다음 코드를 실행 하는 코드를 생성 합니다.

<a id="explore"></a>
## <a name="exploring-the-odata-endpoint"></a>OData 끝점을 탐색

이 섹션에서는 사용 된 [Fiddler Web Debugging Proxy](http://www.fiddler2.com) 끝점에 요청을 보내고 응답 메시지를 검토 하 합니다. OData 끝점의 기능을 이해 하는 데 도움이 됩니다.

Visual Studio에서 f5 키를 눌러 디버깅을 시작 합니다. 기본적으로 Visual Studio는 브라우저를 엽니다 `http://localhost:*port*`, 여기서 *포트* 프로젝트 설정에 구성 된 포트 번호입니다.

프로젝트 설정에서 포트 번호를 변경할 수 있습니다. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **속성**합니다. 속성 창에서 선택 **웹**합니다. 아래의 포트 번호를 입력 **프로젝트 Url**합니다.

### <a name="service-document"></a>서비스 문서

합니다 *서비스 문서* OData 끝점에 대 한 엔터티 집합의 목록을 포함 합니다. 서비스 문서를 가져오려면 서비스의 루트 URI에 GET 요청을 보냅니다.

Fiddler를 사용 하 여의 다음 URI를 입력 합니다 **작성기** 탭: `http://localhost:port/odata/`여기서 *포트* 포트 번호입니다.

![](creating-an-odata-endpoint/_static/image13.png)

클릭 합니다 **Execute** 단추입니다. Fiddler는 응용 프로그램에 HTTP GET 요청을 보냅니다. 웹 세션 목록의 응답이 표시 됩니다. 모든 것이 작동 하는 경우 상태 코드 200 됩니다.

![](creating-an-odata-endpoint/_static/image14.png)

Inspectors 탭에서 응답 메시지의 세부 정보를 보려면 웹 세션 목록의 응답을 두 번 클릭 합니다.

![](creating-an-odata-endpoint/_static/image15.png)

원시 HTTP 응답 메시지는 다음과 비슷하게 표시 됩니다.

[!code-console[Main](creating-an-odata-endpoint/samples/sample8.cmd)]

기본적으로 웹 API는 AtomPub 형식에서 서비스 문서를 반환합니다. JSON을 요청 하려면 HTTP 요청에 다음 헤더를 추가 합니다.

`Accept: application/json`

![](creating-an-odata-endpoint/_static/image16.png)

이제 HTTP 응답에 JSON 페이로드를 포함 되어 있습니다.

[!code-console[Main](creating-an-odata-endpoint/samples/sample9.cmd)]

### <a name="service-metadata-document"></a>서비스 메타 데이터 문서

합니다 *서비스 메타 데이터 문서* 개념적 스키마 정의 언어 (CSDL) 이라는 XML 언어를 사용 하 여 서비스의 데이터 모델을 설명 합니다. 메타 데이터 문서를 서비스에서 데이터의 구조를 표시 및 사용 하 여 클라이언트 코드를 생성할 수 있습니다.

메타 데이터 문서를 가져오려면에 GET 요청을 보냄 `http://localhost:port/odata/$metadata`합니다. 이 자습서에 표시 된 끝점에 대 한 메타 데이터는 다음과 같습니다.

[!code-console[Main](creating-an-odata-endpoint/samples/sample10.cmd)]

### <a name="entity-set"></a>엔터티 집합

Products 엔터티 집합을 가져오려면에 GET 요청을 보냄 `http://localhost:port/odata/Products`합니다.

[!code-console[Main](creating-an-odata-endpoint/samples/sample11.cmd)]

### <a name="entity"></a>엔터티

개별 제품을 가져오려면에 GET 요청을 보냄 `http://localhost:port/odata/Products(1)`, 여기서 "1"은 제품 id입니다.

[!code-console[Main](creating-an-odata-endpoint/samples/sample12.cmd)]

<a id="formats"></a>
## <a name="odata-serialization-formats"></a>OData 직렬화 형식

OData는 몇 가지 직렬화 형식을 지원합니다.

- Atom Pub (XML)
- JSON "light" (OData v3에 도입 됨)
- JSON "verbose" (OData v2)

기본적으로 웹 API AtomPubJSON "light" 형식을 사용합니다.

AtomPub 형식을 가져오려고 Accept 헤더를 "application/atom + xml"로 설정 합니다. 예제 응답 본문은 다음과 같습니다.

[!code-console[Main](creating-an-odata-endpoint/samples/sample13.cmd)]

Atom 형식의 가지 명백한 단점이 볼 수 있습니다: JSON light 보다 훨씬 더 자세 합니다. 그러나 AtomPub에서 인식할 수 있는 클라이언트에 있는 경우 클라이언트는 JSON을 통해 해당 형식의 선호할 수 있습니다.

다음은 동일한 엔터티의 JSON 라이트 버전이입니다.

[!code-console[Main](creating-an-odata-endpoint/samples/sample14.cmd)]

JSON light 형식 OData 프로토콜의 버전 3에에서 도입 되었습니다. 이전 버전과 호환성을 위해 클라이언트는 이전 "verbose" JSON 형식으로 요청할 수 있습니다. 상세 JSON을 요청 하려면 Accept 헤더를 설정할 `application/json;odata=verbose`합니다. 자세한 정보 버전은 다음과 같습니다.

[!code-console[Main](creating-an-odata-endpoint/samples/sample15.cmd)]

이 형식은 전체 세션을 통해 상당한 오버 헤드를 추가할 수 있는 응답 본문에 더 많은 메타 데이터를 전달 합니다. 또한 "d" 라는 속성에서 개체를 래핑하여 간접 참조 수준을 추가 합니다.

## <a name="next-steps"></a>다음 단계

- [엔터티 관계 추가](working-with-entity-relations.md)
- [OData 작업 추가](odata-actions.md)
- [.NET 클라이언트에서 OData 서비스를 호출 합니다.](calling-an-odata-service-from-a-net-client.md)
