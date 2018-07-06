---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
title: '4 부: 제품 나열 | Microsoft Docs'
author: JoeStagner
description: 이 자습서 시리즈 모든 Tailspin Spyworks 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 4 부에서는 GridView contr. 제품 목록 설명...
ms.author: aspnetcontent
ms.date: 07/21/2010
ms.assetid: 4fab47d5-a6ec-4fdc-91f0-651a093a24b9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
msc.type: authoredcontent
ms.openlocfilehash: ec349a2564a63fd950ca5f6a171e6ffd1199c28a
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37813077"
---
<a name="part-4-listing-products"></a>4 부: 제품 나열
====================
[Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks.NET 플랫폼에 대 한 강력 하 고 확장 가능한 응용 프로그램을 생성 하는 방법을 매우 단순 하는 방법을 보여 줍니다. 해제 쇼핑, 체크 아웃 및 관리를 포함 하는 온라인 상점을 만들려고 ASP.NET 4에서 강력한 새 기능을 사용 하는 방법을 보여 줍니다.
> 
> 이 자습서 시리즈 모든 Tailspin Spyworks 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 4 부에서는 GridView 컨트롤을 사용 하 여 제품을 나열 합니다.


## <a id="_Toc260221670"></a>  GridView 컨트롤을 사용 하 여 제품을 나열

솔루션 선택 하 고 "Add" 및 "새 항목"에서 "마우스 오른쪽 단추로 클릭" ProductsList.aspx 페이지 구현를 시작 해 보겠습니다.

![](tailspin-spyworks-part-4/_static/image1.jpg)

"웹 폼 마스터 페이지 사용"을 선택 하 고 ProductsList.aspx 페이지 이름을 입력 "입니다.

"추가"를 클릭 합니다.

![](tailspin-spyworks-part-4/_static/image2.jpg)

다음 Site.Master 페이지에서는 배치할 "스타일" 폴더를 선택 하 고 "폴더의 내용" 창에서 선택 합니다.

![](tailspin-spyworks-part-4/_static/image3.jpg)

"확인" 페이지를 만들려면 클릭 합니다.

아래와 같이 데이터베이스에 제품 데이터가 채워집니다.

![](tailspin-spyworks-part-4/_static/image4.jpg)

가격 페이지 만들어진 후 다시 사용 하 여 엔터티 데이터 소스를 해당 제품 데이터에 액세스 하지만 Product 엔터티를 선택 해야이 인스턴스 및 선택한 범주에 대 한 레코드만 반환 되는 항목을 제한 해야 합니다.

이렇게 하려면 자동 생성 EntityDataSource WHERE 절에 대해 알아봅니다 및 WhereParameter를 지정 합니다.

이 "제품 범주 메뉴에서 메뉴 항목을 만들었을 때 동적으로 구축한 링크는 CatagoryID 각 링크에 대 한 QueryString을 추가 하 여 설명한 내용을 기억하실 겁니다. 위치 매개 변수는 쿼리 문자열 매개 변수에서 파생 엔터티 데이터 소스를 알려줍니다.

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample1.aspx)]

다음으로 제품 목록을 표시할 ListView 컨트롤을 구성 됩니다. 우리의 ListVew에 나타나는 각 개별 제품에 몇 가지 간단한 기능을 압축 됩니다에서는 최적의 쇼핑 환경을 만듭니다.

- 제품 이름을 제품의 세부 정보 뷰에 대 한 링크 됩니다.
- 제품의 가격이 표시 됩니다.
- 제품의 이미지가 표시 되 고 응용 프로그램에서 카탈로그 images 디렉터리에서 이미지를 동적으로 선택 됩니다 것입니다.
- 즉시 특정 제품을 쇼핑 카트에 추가에 대 한 링크를 포함 합니다.

ListView 컨트롤 인스턴스에 대 한 태그는 다음과 같습니다.

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample2.aspx)]

표시 된 각 제품에 대 한 몇 가지 링크에 동적으로 빌드합니다.

또한 직접 새 페이지 테스트 전에 해야 카탈로그 이미지 제품에 대 한 디렉터리 구조를 다음과 같이 만듭니다.

![](tailspin-spyworks-part-4/_static/image1.png)

제품 이미지에 액세스할 수 면 당사의 제품 목록 페이지를 테스트할 수 있습니다.

![](tailspin-spyworks-part-4/_static/image5.jpg)

사이트의 홈 페이지에서 범주 목록 링크 중 하나를 클릭 합니다.

![](tailspin-spyworks-part-4/_static/image6.jpg)

이제 ProductDetials.apsx 페이지 및 AddToCart 기능을 구현 해야 합니다.

사용 하 여 파일-&gt;새 페이지 이름을 ProductDetails.aspx 이전에 수행한 것 처럼 사이트 마스터 페이지를 사용 하 여 만들 수 있습니다.

다시 사용 하 여 EntityDataSource 컨트롤을 데이터베이스에서 특정 제품 레코드에 액세스 하 고 ASP.NET FormView 컨트롤을 사용 하 여 제품 데이터를 다음과 같이 표시 합니다.

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample3.aspx)]

서식 지정을 거 든 보이는 경우 걱정 하지 마세요. 위의 태그를 둡니다 표시 레이아웃의 몇 가지 기능이 나중에 구현 합니다.

쇼핑 카트는 응용 프로그램에서 더 복잡 한 논리를 나타냅니다. 시작 하려면 사용 하 여 파일-&gt;MyShoppingCart.aspx 라는 페이지를 만들려면 새로 만들기.

이름을 ShoppingCart.aspx 선택 하지 않습니다 것을 참고 합니다.

데이터베이스 "ShoppingCart" 라는 테이블을 포함 합니다. 엔터티 데이터 모델을 생성할 때 데이터베이스의 각 테이블에 대 한 클래스를 만들었습니다. 따라서 엔터티 데이터 모델 "ShoppingCart" 라는 엔터티 클래스가 생성 됩니다. 하지만 대신 않고 단순히 충돌을 방지 하는 이름 선택 하려면 쇼핑 카트 구현에 해당 이름을 사용할 수 없습니다 하거나, 요구 사항에 대 한 확장 모델을 편집할 수 없습니다.

쇼핑 카트 표시를 사용 하 여 쇼핑 카트 논리를 포함 하는 우리가 만들 간단한 쇼핑 카트 주목할 만한 이기도 합니다. 우리는 완전히 별개의 비즈니스 계층에서 당사의 쇼핑 카트를 구현 하는 선택할 수도 있습니다.

> [!div class="step-by-step"]
> [이전](tailspin-spyworks-part-3.md)
> [다음](tailspin-spyworks-part-5.md)
