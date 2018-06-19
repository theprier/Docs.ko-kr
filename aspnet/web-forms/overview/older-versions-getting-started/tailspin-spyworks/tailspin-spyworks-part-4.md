---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
title: '4 단계: 제품을 나열 하 | Microsoft Docs'
author: JoeStagner
description: 이 자습서 시리즈 모든 Tailspin Spyworks 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다. 4 부 GridView contr. 제품 목록 설명...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/21/2010
ms.topic: article
ms.assetid: 4fab47d5-a6ec-4fdc-91f0-651a093a24b9
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
msc.type: authoredcontent
ms.openlocfilehash: 69b26344e6dcdbf27e94da90ad5d6cd79f27ccd3
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30881066"
---
<a name="part-4-listing-products"></a>4 단계: 목록 제품
====================
으로 [Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks.NET 플랫폼에 대해 강력 하 고 확장 가능한 응용 프로그램을 만드는 방법을 매우 간단한는 하는 방법을 보여 줍니다. Off 쇼핑, 체크 아웃, 및 관리를 포함 하 여 온라인 상점에서는 만들려는 ASP.NET 4에서 멋진 새로운 기능을 사용 하는 방법을 보여 줍니다.
> 
> 이 자습서 시리즈 모든 Tailspin Spyworks 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다. 4 부 목록 제품 GridView 컨트롤을 설명합니다.


## <a id="_Toc260221670"></a>  GridView 컨트롤에서 제품을 나열

"추가" 및 "새 항목"을 선택 하 고 솔루션에 "마우스 오른쪽 단추로 클릭" 가격 ProductsList.aspx 페이지 구현를 시작 해 보겠습니다.

![](tailspin-spyworks-part-4/_static/image1.jpg)

"웹 폼 마스터 페이지 사용"을 선택 하 고 페이지 이름을 입력 ProductsList.aspx의 "입니다.

"추가"를 클릭 합니다.

![](tailspin-spyworks-part-4/_static/image2.jpg)

다음 Site.Master 페이지를 배치 했습니다 "스타일" 폴더를 선택 하 고 "폴더의 내용" 창에서 선택 합니다.

![](tailspin-spyworks-part-4/_static/image3.jpg)

"확인" 페이지를 만들려면 클릭 합니다.

아래와 같이 데이터베이스에 제품 데이터가 채워집니다.

![](tailspin-spyworks-part-4/_static/image4.jpg)

가격 페이지 만든 후 해당 제품 데이터에 액세스 하는 엔터티 데이터 원본에서는 다시 하지만이 인스턴스의 제품 엔터티를 선택 해야 하 고 선택한 범주에 대 한 레코드만 반환 되는 항목을 제한 해야 합니다.

이렇게 하려면 WHERE 절을 자동으로 생성할 EntityDataSource에 대해 알아봅니다 및는 WhereParameter로 지정 합니다.

"제품 범주 메뉴" 우리의에 메뉴 항목을 만들 때에서는 동적으로 작성 된 링크는 CatagoryID 각 링크에 대 한 QueryString을 추가 하 여를 회수할 수 있습니다. 에서는 엔터티 데이터 소스 위치 매개 변수는 쿼리 문자열 매개 변수에서 상속할를 알 수 있습니다.

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample1.aspx)]

다음으로, 제품의 목록을 표시 하려면 ListView 컨트롤을 구성 합니다. 우리의 ListVew에 나타나는 각 개별 제품으로 간결 하 게 몇 가지 기능을 압축 합니다 म 쇼핑 겪을 만들기

- 제품 이름을 제품의 세부 정보 보기에 대 한 링크 됩니다.
- 제품의 가격을 표시 됩니다.
- 제품의 이미지 표시 되 고이 응용 프로그램에서 카탈로그 이미지 디렉터리에서 이미지를 동적으로 선택 됩니다 म 합니다.
- 즉시 특정 제품 쇼핑 카트에 추가에 대 한 링크를 포함 됩니다.

ListView 컨트롤 인스턴스에 대 한 태그는 다음과 같습니다.

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample2.aspx)]

표시 된 각 제품에 대 한 몇 가지 링크 동적으로 작성 합니다.

또한 전에 새 페이지를 직접 테스트 해야 카탈로그 이미지는 제품에 대 한 디렉터리 구조를 다음과 같이 만듭니다.

![](tailspin-spyworks-part-4/_static/image1.png)

우리의 제품 이미지에 액세스할 수 있는 한 번 가격 제품 목록 페이지를 테스트할 수 있습니다.

![](tailspin-spyworks-part-4/_static/image5.jpg)

사이트의 홈 페이지에서 범주 목록 링크 중 하나를 클릭 합니다.

![](tailspin-spyworks-part-4/_static/image6.jpg)

이제 ProductDetials.apsx 페이지 및 AddToCart 기능을 구현 해야 합니다.

사용 하 여 파일-&gt;새로운 페이지 이름을 ProductDetails.aspx 이전에 수행한 것 처럼 사이트 마스터 페이지를 사용 하 여 만들 수 있습니다.

EntityDataSource 컨트롤 데이터베이스의 특정 제품 레코드에 액세스 하는 데 사용할 다시과 제품 데이터를 다음과 같이 표시 ASP.NET FormView 컨트롤을 사용 합니다.

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample3.aspx)]

사용자에 게 거 든 표시 서식을 경우 걱정 하지 마십시오. 위의 태그 몇 가지 나중에 구현 하는 기능에 대 한 디스플레이 레이아웃에서 공간을 유지 합니다.

쇼핑 카트는이 응용 프로그램에서 더 복잡 한 논리를 나타냅니다. 시작 하려면 사용 하 여 파일-&gt;MyShoppingCart.aspx 라는 페이지를 만들려면 새로 만들기.

ShoppingCart.aspx 이름을 선택 하지 않으면는 것을 참고 합니다.

데이터베이스 "ShoppingCart" 라는 테이블을 포함 합니다. 엔터티 데이터 모델을 생성할 때 클래스는 데이터베이스의 각 테이블에 대해 만들었습니다. 따라서 엔터티 데이터 모델에는 "ShoppingCart" 라는 엔터티 클래스가 생성 합니다. 하지만을 단순히 선택 하 여 충돌을 방지 하는 이름 대신 옵트인 됩니다 म 쇼핑 카트 구현에 해당 이름을 사용할 수 없습니다. 하거나, 요구 사항에 대 한 확장 모델을 편집 수 없습니다.

것도 알아두는 것을 만드는데 간단한 쇼핑 카트 주목할 및 쇼핑 카트 표시와 함께 쇼핑 카트 논리를 포함 합니다. 완전히 별개의 비즈니스 계층에서 당사의 쇼핑 카트를 구현 하 선택할 수도 있습니다.

> [!div class="step-by-step"]
> [이전](tailspin-spyworks-part-3.md)
> [다음](tailspin-spyworks-part-5.md)
