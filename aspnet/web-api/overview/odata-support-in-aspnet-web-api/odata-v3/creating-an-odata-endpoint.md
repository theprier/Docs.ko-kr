---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
title: Web API 2 OData v3 끝점 만들기 | Microsoft Docs
author: MikeWasson
description: 개방형 데이터 프로토콜 (OData)는 웹에 대 한 데이터 액세스 프로토콜입니다. OData는 데이터, 데이터를 쿼리 및 데이터를 조작 하는 일관 된 방식으로 제공...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/25/2014
ms.topic: article
ms.assetid: 262843d6-43a2-4f1c-82d9-0b90ae6df0cf
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
msc.type: authoredcontent
ms.openlocfilehash: 227faacd3f42731e08a4cd2b71075776309961b6
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="creating-an-odata-v3-endpoint-with-web-api-2"></a>Web API 2 OData v3 끝점 만들기
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트를 다운로드 합니다.](http://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> [개방형 데이터 프로토콜](http://www.odata.org/) 는 웹에 대 한 데이터 액세스 프로토콜 (OData). OData는 일관 된 방식으로 구조 데이터는 데이터를 쿼리하고 조작 CRUD 작업을 통해 데이터 집합을 제공 (만들기, 읽기, 업데이트 및 삭제) 합니다. OData는 AtomPub (XML) 및 JSON 형식 둘 다 지원합니다. OData는 데이터에 대 한 메타 데이터를 노출 하는 방법을 정의 합니다. 형식 정보 및 데이터 집합에 대 한 관계를 검색 하도록 클라이언트 메타 데이터를 사용할 수 있습니다.
> 
> ASP.NET Web API를 사용 하면 손쉽게 데이터 집합에 대 한 OData 끝점을 만듭니다. 끝점이 지 원하는 어떤 OData 작업을 정확 하 게 제어할 수 있습니다. 비 OData 끝점와 함께 여러 OData 끝점을 호스팅할 수 있습니다. 데이터 모델, 백 엔드 비즈니스 논리 및 데이터 계층을 통해 모든 권한이 있습니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - Web API 2
> - OData 버전 3
> - Entity Framework 6
> - [Fiddler 웹 프록시 (선택 사항) 디버깅](http://www.fiddler2.com)
> 
> Web API OData 지원에 추가 된 [ASP.NET 및 Web Tools 2012.2 업데이트](https://go.microsoft.com/fwlink/?LinkId=282650)합니다. 그러나이 자습서에서는 Visual Studio 2013에서 추가 된 스 캐 폴딩을 사용 합니다.


이 자습서에서는 클라이언트가 쿼리할 수 있는 간단한 OData 끝점을 만들게 됩니다. 또한 C# 클라이언트를 끝점에 대해 만들어집니다. 이 자습서를 완료 한 후 자습서의 다음 집합에 엔터티 관계 작업을 포함 하 여 더 많은 기능을 추가 하는 방법을 표시 하 고 확장 하 고 $/ $선택 합니다.

- [Visual Studio 프로젝트 만들기](#create-project)
- [엔터티 모델 추가](#add-model)
- [OData 컨트롤러 추가](#add-controller)
- [EDM 및 경로 추가 합니다.](#edm)
- [시드 데이터베이스 (옵션)](#seed-db)
- [OData 끝점을 탐색합니다.](#explore)
- [OData Serialization 형식](#formats)

<a id="create-project"></a>
## <a name="create-the-visual-studio-project"></a>Visual Studio 프로젝트 만들기

이 자습서에서는 기본 CRUD 작업을 지 원하는 OData 끝점에 만들어집니다. 끝점에는 단일 리소스, 제품의 목록을 제공 합니다. 이후의 자습서 더 많은 기능을 추가 합니다.

Visual Studio를 시작 하 고 선택 **새 프로젝트** 시작 페이지에서. 또는에서 **파일** 메뉴 선택 **새로** 차례로 **프로젝트**합니다.

에 **템플릿** 창 선택 **설치 된 템플릿** Visual C# 노드를 확장 합니다. 아래 **Visual C#**선택, **웹**합니다. 선택 **ASP.NET 웹 응용 프로그램** 템플릿.

![](creating-an-odata-endpoint/_static/image1.png)

에 **새 ASP.NET 프로젝트** 대화 상자에서는 **빈** 서식 파일입니다. &quot;폴더 추가 및에 대 한 참조를 핵심... &quot;, 확인 **웹 API**합니다. **확인**을 클릭합니다.

![](creating-an-odata-endpoint/_static/image2.png)

<a id="add-model"></a>
## <a name="add-an-entity-model"></a>엔터티 모델 추가

*모델*은 응용 프로그램에서 데이터를 나타내는 개체입니다. 이 자습서에 대 한 제품을 나타내는 모델이 필요 합니다. 모델의 OData 엔터티 형식에 해당합니다.

솔루션 탐색기에서 모델 폴더를 마우스 오른쪽 단추로 클릭 합니다. 상황에 맞는 메뉴에서 선택 **추가** 다음 선택 **클래스**합니다.

![](creating-an-odata-endpoint/_static/image3.png)

에 **새로 추가** 항목 대화 상자, 클래스의 이름을 &quot;제품&quot;합니다.

![](creating-an-odata-endpoint/_static/image4.png)

> [!NOTE]
> 규칙에 따라 모델 클래스 모델 폴더에 배치 됩니다. 사용자의 프로젝트에서이 규칙을 따르는 필요가 없습니다 하지만이 자습서에 대 한 때 사용 해야 합니다.


Product.cs 파일에서 다음 클래스 정의 추가 합니다.

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample1.cs)]

ID 속성은 엔터티 키를 됩니다. 클라이언트 id는 제품을 쿼리할 수 있습니다. 이 필드는 백 엔드 데이터베이스의 기본 키 수도 있습니다.

지금 프로젝트를 빌드하십시오. 다음 단계에서는 리플렉션을 사용 하 여 제품 종류를 찾을 수 있는 일부 Visual Studio 스 캐 폴딩을 사용 합니다.

<a id="add-controller"></a>
## <a name="add-an-odata-controller"></a>OData 컨트롤러 추가

A *컨트롤러* 는 HTTP 요청을 처리 하는 클래스입니다. OData 서비스에서 설정 하는 각 엔터티에 대 한 별도 컨트롤러를 정의 합니다. 이 자습서에서는 단일 컨트롤러를 만들겠습니다.

솔루션 탐색기에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭 합니다. 선택 **추가** 선택한 후 **컨트롤러**합니다.

![](creating-an-odata-endpoint/_static/image5.png)

에 **추가 스 캐 폴드** 대화 상자에서 &quot;Web API 2 OData 컨트롤러와 동작을 Entity Framework를 사용 하 여&quot;합니다.

![](creating-an-odata-endpoint/_static/image6.png)

에 **컨트롤러 추가** 대화 상자에서 "ProductsController" 컨트롤러 이름입니다. 선택 된 &quot;비동기 컨트롤러 동작을 사용 하 여&quot; 확인란을 선택 합니다. 에 **모델** 드롭 다운 목록에서 Product 클래스를 선택 합니다.

![](creating-an-odata-endpoint/_static/image7.png)

클릭는 **새 데이터 컨텍스트에...**  단추입니다. 데이터 컨텍스트 형식에 대 한 기본 이름을 클릭 **추가**합니다.

![](creating-an-odata-endpoint/_static/image8.png)

컨트롤러 추가 하는 컨트롤러 추가 대화 상자에서 [추가]를 클릭 합니다.

![](creating-an-odata-endpoint/_static/image9.png)

참고: 라는 오류 메시지가 나타날 경우 &quot;형식을 가져오는 동안 오류가 발생 했습니다. &quot;, Product 클래스에 추가한 후 Visual Studio 프로젝트를 빌드 되었는지 확인 합니다. 스 캐 폴딩의 리플렉션을 사용 하 여 클래스를 찾고 있습니다.

![](creating-an-odata-endpoint/_static/image10.png)

스 캐 폴딩을 두 코드 파일을 프로젝트에 추가합니다.

- Products.cs는 OData 끝점을 구현 하는 Web API 컨트롤러를 정의 합니다.
- ProductServiceContext.cs는 Entity Framework를 사용 하 여 기본 데이터베이스를 쿼리 하는 메서드를 제공 합니다.

![](creating-an-odata-endpoint/_static/image11.png)

<a id="edm"></a>
## <a name="add-the-edm-and-route"></a>EDM 및 경로 추가 합니다.

솔루션 탐색기에서 응용 프로그램을 확장\_폴더를 시작 하 고 WebApiConfig.cs 라는 파일을 엽니다. 이 클래스는 웹 API에 대 한 구성 코드를 포함합니다. 이 코드를 다음으로 바꿉니다.

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample2.cs)]

이 코드는 두 가지 작업을 수행합니다.

- 데이터 모델 EDM (엔터티)에 대 한 OData 끝점을 만듭니다.
- 끝점에 대 한 경로 추가합니다.

EDM은 데이터의 추상 모델입니다. 메타 데이터 문서를 만들고 서비스에 대 한 Uri를 정의 하는 EDM 사용 됩니다. **ODataConventionModelBuilder** EDM EDM 기본 명명 규칙의 집합을 사용 하 여 만듭니다. 이 방법을 사용 하려면 최소 코드가 필요 합니다. EDM 통해 더 많은 제어를 원하는 경우 사용할 수 있습니다는 **된** EDM 속성, 키 및 탐색 속성을 명시적으로 추가 하 여 만들 클래스입니다.

**EntitySet** 메서드는 엔터티 집합 EDM을 추가 합니다.

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample3.cs)]

문자열 "Products" 엔터티 집합의 이름을 정의합니다. 컨트롤러의 이름에는 엔터티 집합의 이름을 일치 해야 합니다. 이 자습서에서는 엔터티 집합의 이름은 "Products" 및 컨트롤러 라는 `ProductsController`합니다. 엔터티 집합 "ProductSet"의 이름을, 컨트롤러 이름을 `ProductSetController`합니다. 끝점 여러 엔터티 집합에 포함 될 수 있는 참고 합니다. 호출 **EntitySet&lt;T&gt;**  각 엔터티에 대 한 설정, 한 다음 해당 컨트롤러를 정의 합니다.

**MapODataRoute** 메서드 OData 끝점에 대 한 경로 추가 합니다.

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample4.cs)]

첫 번째 매개 변수는 경로의 이름입니다. 서비스의 클라이언트가이 이름을 볼 수 없습니다. 두 번째 매개 변수는 끝점에 대 한 URI 접두사입니다. 이 코드를 매개 변수로 받아 Products 엔터티 집합에 대 한 URI은 http://<em>hostname</em>  /odata/제품입니다. 응용 프로그램에 OData 끝점을 여러 개 있을 수 있습니다. 각 끝점에 대 한 호출 <strong>MapODataRoute</strong> 고유 경로 이름 및 고유 URI 접두사를 제공 합니다.

<a id="seed-db"></a>
## <a name="seed-the-database-optional"></a>시드 데이터베이스 (옵션)

이 단계에서는 일부 테스트 데이터가 포함 된 데이터베이스를 시드하고를 Entity Framework를 사용 합니다. 이 단계는 옵션 이지만 OData 끝점 테스트 지금 즉시 실행할 수 있습니다.

**도구** 메뉴 선택 **라이브러리 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다. 패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

[!code-console[Main](creating-an-odata-endpoint/samples/sample5.cmd)]

이 마이그레이션 및 Configuration.cs 라는 코드 파일 라는 폴더를 추가 합니다.

![](creating-an-odata-endpoint/_static/image12.png)

이 파일을 열고 다음 코드를 추가 하는 `Configuration.Seed` 메서드.

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample6.cs)]

패키지 관리자 콘솔 창에 다음 명령을 입력 합니다.

[!code-console[Main](creating-an-odata-endpoint/samples/sample7.cmd)]

이 명령은 데이터베이스가 생성 한 다음 해당 코드를 실행 하는 코드를 생성 합니다.

<a id="explore"></a>
## <a name="exploring-the-odata-endpoint"></a>OData 끝점을 탐색합니다.

이 섹션에서는 [Fiddler 웹 디버깅 프록시](http://www.fiddler2.com) 를 끝점에 요청을 보내고 응답 메시지를 검토 합니다. OData 끝점의 기능을 이해 하는 데 도움이 됩니다.

Visual Studio에서 f5 키를 눌러 디버깅을 시작 합니다. 기본적으로 Visual Studio는 브라우저를 열고 `http://localhost:*port*`여기서 *포트* 프로젝트 설정에 구성 된 포트 번호입니다.

프로젝트 설정에서 포트 번호를 변경할 수 있습니다. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **속성**합니다. 속성 창에서 선택 **웹**합니다. 포트 번호를 입력 **프로젝트 Url**합니다.

### <a name="service-document"></a>서비스 문서

*서비스 문서* OData 끝점에 대 한 엔터티 집합의 목록을 포함 합니다. 서비스 문서를 얻기 위해 서비스의 루트 URI에 GET 요청을 보냅니다.

Fiddler를 사용 하 여 입력에 다음 URI는 **작성기** 탭: `http://localhost:port/odata/`여기서 *포트* 포트 번호입니다.

![](creating-an-odata-endpoint/_static/image13.png)

클릭는 **Execute** 단추입니다. Fiddler는 응용 프로그램에 HTTP GET 요청을 보냅니다. 응답 웹 세션 목록에 표시 됩니다. 모든 기능이 작동 하는 경우 상태 코드 200 됩니다.

![](creating-an-odata-endpoint/_static/image14.png)

관리자 탭에서 응답 메시지의 세부 정보를 웹 세션 목록에 응답을 두 번 클릭 합니다.

![](creating-an-odata-endpoint/_static/image15.png)

원시 HTTP 응답 메시지는 다음과 비슷하게 표시 됩니다.

[!code-console[Main](creating-an-odata-endpoint/samples/sample8.cmd)]

기본적으로 웹 API AtomPub 형태로 서비스 문서를 반환합니다. JSON을 요청 하려면 HTTP 요청에 다음 헤더를 추가 합니다.

`Accept: application/json`

![](creating-an-odata-endpoint/_static/image16.png)

이제는 HTTP 응답에 JSON 페이로드를 포함 되어 있습니다.

[!code-console[Main](creating-an-odata-endpoint/samples/sample9.cmd)]

### <a name="service-metadata-document"></a>서비스 메타 데이터 문서

*서비스 메타 데이터 문서* 개념 스키마 정의 언어 (CSDL) 이라는 XML 언어를 사용 하 여 서비스의 데이터 모델을 설명 합니다. 메타 데이터 문서 데이터의 구조를 나타내고 서비스에서 클라이언트 코드를 생성 하기 위해 사용할 수 있습니다.

메타 데이터 문서를 가져오려면에 GET 요청을 보내고 `http://localhost:port/odata/$metadata`합니다. 이 자습서에 표시 된 끝점에 대 한 메타 데이터는 다음과 같습니다.

[!code-console[Main](creating-an-odata-endpoint/samples/sample10.cmd)]

### <a name="entity-set"></a>엔터티 집합

Products 엔터티 집합을 가져오려면에 GET 요청을 보내고 `http://localhost:port/odata/Products`합니다.

[!code-console[Main](creating-an-odata-endpoint/samples/sample11.cmd)]

### <a name="entity"></a>엔터티

에 GET 요청을 보내고 개별 제품을 가져오려면 `http://localhost:port/odata/Products(1)`, 여기서 "1"이 제품 id입니다.

[!code-console[Main](creating-an-odata-endpoint/samples/sample12.cmd)]

<a id="formats"></a>
## <a name="odata-serialization-formats"></a>OData Serialization 형식

OData는 몇 가지 직렬화 형식을 지원합니다.

- Atom Pub (XML)
- JSON "light" (OData v 3에 도입 된)
- JSON "verbose" (OData v2)

기본적으로 웹 API AtomPubJSON "light" 형식을 사용합니다. 

AtomPub 형식을 가져오려면 Accept 헤더가 "application/atom + xml"로 설정 합니다. 다음은 예제 응답 본문이입니다.

[!code-console[Main](creating-an-odata-endpoint/samples/sample13.cmd)]

Atom 형식의 가지 명백한 단점이 볼 수 있습니다: JSON light 보다 훨씬 세부적입니다. 그러나 AtomPub를 이해할 수 있는 클라이언트를 설정한 경우 클라이언트 수도 해당 형식을 JSON을 통해.

다음은 동일한 엔터티의 JSON 라이트 버전이입니다.

[!code-console[Main](creating-an-odata-endpoint/samples/sample14.cmd)]

JSON light 형식 OData 프로토콜의 버전 3에에서 도입 되었습니다. 이전 버전과 호환성을 위해 클라이언트는 이전 "verbose" JSON 형식을 요청할 수 있습니다. 상세 JSON을 요청 하려면 Accept 헤더를 설정할 `application/json;odata=verbose`합니다. 다음은 자세한 정보 표시 버전이입니다.

[!code-console[Main](creating-an-odata-endpoint/samples/sample15.cmd)]

이 형식은 전체 세션을 통해 상당한 오버 헤드를 추가할 수 있는 응답 본문에 더 많은 메타 데이터를 전달 합니다. 또한, "d" 라는 속성에 개체를 래핑하여 간접 참조 수준을 추가 합니다.

## <a name="next-steps"></a>다음 단계

- [엔터티 관계 추가](working-with-entity-relations.md)
- [OData 작업 추가](odata-actions.md)
- [.NET 클라이언트에서 OData 서비스를 호출 합니다.](calling-an-odata-service-from-a-net-client.md)
