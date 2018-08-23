---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
title: ASP.NET Web API 사용 하 여 OData v4의는 개방형 형식만 | Microsoft Docs
author: microsoft
description: OData v4의 개방형 형식 stuctured 있는 형식인 형식 정의에서 선언 된 속성 외에 동적 속성을 포함 합니다. 열기...
ms.author: riande
ms.date: 09/15/2014
ms.assetid: f25f5ac5-4800-4950-abe5-c97750a27fc6
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 77771d85532b8b622c2ad4ca219a38990e474c9c
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41838743"
---
<a name="open-types-in-odata-v4-with-aspnet-web-api"></a>ASP.NET Web API 사용 하 여 OData v4의 종류를 열려면
====================
[Microsoft](https://github.com/microsoft)

> OData v4의는 *형식을 열* stuctured 형식이 형식 정의에서 선언 된 속성 외에 동적 속성을 포함 하는 합니다. 개방형 형식 데이터 모델에 유연성을 추가할 수 있습니다. 이 자습서에서는 ASP.NET Web API OData의 개방형 형식을 사용 하는 방법을 보여 줍니다.
> 
> 이 자습서에서는 ASP.NET Web API에서 OData 끝점을 만드는 방법을 이미 알고 있다고 가정 합니다. 그렇지 않은 경우 먼저 읽으십시오 [OData v4 엔드포인트 만들기](create-an-odata-v4-endpoint.md) 첫 번째입니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
> 
> 
> - Web API OData 5.3
> - OData v4


먼저 몇 가지 OData 용어:

- 엔터티 형식: 키를 사용 하 여 구조화 된 형식입니다.
- 복합 형식: 키가 없는 구조적된 형식입니다.
- Open 형식: 동적 속성을 사용 하 여 형식입니다. 엔터티 형식 및 복합 형식 모두 열 수 있습니다.

기본 형식, 복합 형식 또는 열거형 형식; 동적 속성의 값 수 있습니다. 또는 이러한 형식의 컬렉션입니다. 개방형 형식에 대 한 자세한 내용은 참조는 [OData v4 사양을](http://www.odata.org/documentation/odata-version-4-0/)합니다.

## <a name="install-the-web-odata-libraries"></a>웹 OData 라이브러리 설치

NuGet 패키지 관리자를 사용 하 여 최신 Web API OData 라이브러리를 설치 합니다. 패키지 관리자 콘솔 창:

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a>CLR 유형 정의

CLR 형식과 EDM 모델을 정의 하 여 시작 합니다.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

(EDM (엔터티 데이터 모델) 만들어질 때

- `Category` 열거형 형식이입니다.
- `Address` 복합 형식이입니다. (이 없으므로 키를 엔터티 형식이 아닙니다.)
- `Customer` 엔터티 형식이입니다. (키가 있습니다.)
- `Press` 열기 복합 형식이입니다.
- `Book` 개방형 엔터티 형식이입니다.

만들려면 개방형 형식, CLR 형식 있어야 형식의 속성 `IDictionary<string, object>`, 동적 속성을 보유 합니다.

## <a name="build-the-edm-model"></a>EDM 모델 빌드

사용 하는 경우 **ODataConventionModelBuilder** EDM을 만들려면 `Press` 하 고 `Book` 의 유무에 따라 열기 형식으로 자동으로 추가 됩니다을 `IDictionary<string, object>` 속성입니다.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

빌드할 수도 있습니다 EDM 명시적으로 사용 하 여 **된 ODataModelBuilder**합니다.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a>OData 컨트롤러 추가

다음으로, OData 컨트롤러를 추가 합니다. 이 자습서에서는 지원 가져오기 및 게시를 요청 하는 메모리 내 목록을 사용 하 여 엔터티를 저장 하는 간소화 된 컨트롤러를 사용 하겠습니다.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

첫 번째 `Book` 인스턴스에 동적 속성이 없습니다. 두 번째 `Book` 인스턴스는 동적 속성은:

- "게시 됨": 기본 형식
- "작성자": 기본 형식의 컬렉션
- "OtherCategories": 열거형 형식의 컬렉션입니다.

또한 합니다 `Press` 속성의 `Book` 인스턴스는 동적 속성은:

- "Blog": 기본 형식
- "Address": 복합 형식

## <a name="query-the-metadata"></a>메타 데이터를 쿼리 합니다.

OData 메타 데이터 문서를 가져오려면에 GET 요청을 보냄 `~/$metadata`합니다. 응답 본문은 다음과 유사 하 게 같아야 합니다.

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

메타 데이터 문서에서 볼 수 있습니다.

- 에 대 한는 `Book` 및 `Press` 형식의 경우 값을 `OpenType` 특성은 true입니다. 합니다 `Customer` 및 `Address` 형식을이 특성이 없습니다.
- `Book` 엔터티 형식은 세 가지 선언 된 속성: ISBN, 제목 및 키를 누릅니다. OData 메타 데이터를 포함 하지 않습니다는 `Book.Properties` CLR 클래스에서 속성입니다.
- 마찬가지로,는 `Press` 복합 형식에 선언 된 두 개의 속성만: 이름 및 범주입니다. 메타 데이터가 포함 되지 않습니다는 `Press.DynamicProperties` CLR 클래스에서 속성입니다.

## <a name="query-an-entity"></a>엔터티 쿼리

책 ISBN 사용 하 여 "978-7356-7942-0-9" 같음를 가져오려면에 GET 요청을 보냄 `~/Books('978-0-7356-7942-9')`합니다. 응답 본문은 다음과 유사 합니다. (더 쉽게 읽을 수 있도록 들여씁니다).

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

동적 속성에 선언 된 속성을 사용 하 여 인라인에 포함된 되는지 확인 합니다.

## <a name="post-an-entity"></a>엔터티를 게시 합니다.

책 엔터티를 추가 하려면 POST 요청을 보낼 `~/Books`합니다. 클라이언트 요청 페이로드의 동적 속성을 설정할 수 있습니다.

요청 예제는 다음과 같습니다. "Price" 및 "게시 됨" 속성을 note 합니다.

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

컨트롤러 메서드에서 중단점을 설정 하는 경우 Web API에 이러한 속성을 추가 되었음을 확인할 수 있습니다는 `Properties` 사전입니다.

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a>추가 리소스

[OData 오픈 형식 샘플](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)
