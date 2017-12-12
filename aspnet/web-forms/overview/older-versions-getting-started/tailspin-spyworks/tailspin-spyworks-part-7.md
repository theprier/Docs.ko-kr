---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-7
title: "7 단계: 추가 기능 | Microsoft Docs"
author: JoeStagner
description: "이 자습서 시리즈 모든 Tailspin Spyworks 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다. 7 부 계정 revie 같은 추가 기능을 추가 하는 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/21/2010
ms.topic: article
ms.assetid: 50223ee9-11b9-4cf3-bca2-e2f10bf471f3
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-7
msc.type: authoredcontent
ms.openlocfilehash: 5280de44b3e75f9d1ae85e0248bc3ef6d5444f6d
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="part-7-adding-features"></a>7 단계: 추가 기능
====================
으로 [Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks.NET 플랫폼에 대해 강력 하 고 확장 가능한 응용 프로그램을 만드는 방법을 매우 간단한는 하는 방법을 보여 줍니다. Off 쇼핑, 체크 아웃, 및 관리를 포함 하 여 온라인 상점에서는 만들려는 ASP.NET 4에서 멋진 새로운 기능을 사용 하는 방법을 보여 줍니다.
> 
> 이 자습서 시리즈 모든 Tailspin Spyworks 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다. 7 부 계정 검토, 제품 검토 및 "인기 있는 항목" 및 "도 구매한" 사용자 정의 컨트롤 등의 추가 기능을 추가합니다.


## <a id="_Toc260221673"></a>기능 추가

사용자가 카탈로그를 찾아볼 수 있지만 장바구니의 항목을 배치 하 고 체크 아웃 과정을 완료는 다양 한 지원 기능 사이트를 개선 하기 위해 포함 될 것입니다.

1. 계정 검토 (목록 주문 배치 및 세부 정보를 확인 합니다.)
2. 기본 페이지 일부 상황에 맞는 특정 콘텐츠를 추가 합니다.
3. 카탈로그에 사용자가 검토 수 있도록 하는 기능이 제품을 추가 합니다.
4. 인기 있는 항목 및 위치를 제어 하는 첫 페이지에 표시 하려면 사용자 정의 컨트롤을 만듭니다.
5. "구입도"는 사용자 정의 컨트롤을 만들고 제품 세부 정보 페이지에 추가 합니다.
6. 연락처 추가 페이지.
7. 추가 한 페이지에 대 한 합니다.
8. 전역 오류

## <a id="_Toc260221674"></a>계정 검토

"계정" 폴더에서 명명된 한 OrderList.aspx 및 다른 명명 된 OrderDetails.aspx 두.aspx 페이지를 만듭니다

이전에 필요한 만큼 OrderList.aspx는 GridView 및 EntityDataSoure 컨트롤을 이용 합니다.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample1.aspx)]

EntityDataSoure 사용자 이름에 필터링 된 Orders 테이블에서 레코드를 선택 (참조는 WhereParameter) 사용자 로그의 경우 세션 변수에 설정입니다.

Note도 GridView HyperlinkField에 이러한 매개 변수:

[!code-xml[Main](tailspin-spyworks-part-7/samples/sample2.xml)]

이러한 OrderDetails.aspx 페이지의 쿼리 문자열 매개 변수로 OrderID 필드를 지정 하는 각 제품에 대 한 주문 세부 정보 보기에 대 한 링크를 지정 합니다.

## <a id="_Toc260221675"></a>OrderDetails.aspx

EntityDataSource 컨트롤에 모든 주문의 품목을 표시 하는 GridView와 다른 EntityDataSource 및 주문 데이터를 표시 하는 주문 및는 FormView 액세스 하려면 사용 합니다.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample3.aspx)]

코드 숨김 파일 (OrderDetails.aspx.cs)에 정리 작업의 거의 비트 두 개가 있습니다.

먼저 OrderDetails 항상 가져옴을 OrderId 있는지 확인 해야 합니다.

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample4.cs)]

또한 계산 하 고 주문 라인 항목에서 합계를 표시 해야 합니다.

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample5.cs)]

## <a id="_Toc260221676"></a>홈 페이지

Default.aspx 페이지에 몇 가지 정적 콘텐츠를 추가 해 보겠습니다.

먼저 "콘텐츠" 폴더를 만들겠습니다 그 안의 이미지 폴더 (및 홈 페이지에 사용할 이미지를 포함 합니다.)

Default.aspx 페이지의 아래쪽 개체 틀에 다음 태그를 추가 합니다.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample6.aspx)]

## <a id="_Toc260221677"></a>제품 평가

먼저 입력 한 제품 검토를 사용할 수 있는 형식으로 링크와 단추를 추가 합니다.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample7.aspx)]

![](tailspin-spyworks-part-7/_static/image1.jpg)

쿼리 문자열에는 ProductID 전달 하는 참고

다음 ReviewAdd.aspx 라는 페이지 추가

이 페이지는 ASP.NET AJAX 컨트롤 도구 키트를 사용 합니다. 하는 경우 수행 하지 않은 이미에서 다운로드할 수 있도록 [DevExpress](http://devexpress.com/act) 여기 Visual Studio와 함께 사용 하기 위해 도구 키트 설정 지침 이며 [https://www.asp.net/learn/ajax-videos/video-76.aspx](../../../videos/ajax-control-toolkit/how-do-i-get-started-with-the-aspnet-ajax-control-toolkit.md).

디자인 모드에서 컨트롤 및 유효성 검사기 도구 상자에서 끌어서 아래와 같은 양식을 작성 합니다.

![](tailspin-spyworks-part-7/_static/image2.jpg)

태그를 다음과 같이 표시 됩니다.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample8.aspx)]

검토를 입력할 수, 했으므로 해당 리뷰 제품 페이지에 표시할 수 있습니다.

이 태그 ProductDetails.aspx 페이지에 추가 합니다.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample9.aspx)]

이제 응용 프로그램 실행 및 제품에 탐색 고객 리뷰를 비롯 한 제품 정보를 보여 줍니다.

![](tailspin-spyworks-part-7/_static/image3.jpg)

## <a id="_Toc260221678"></a>인기 있는 컨트롤 (사용자 정의 컨트롤 만들기)

웹 사이트에서의 매출을 늘리기 위해 몇 가지 기능 "추천 판매" 인기 있는 하거나 관련 된 제품에 추가 합니다.

이러한 기능 중 첫 번째 회사 제품 카탈로그에서 더 많이 사용 되는 제품의 목록이 됩니다.

많이 판매 되는 응용 프로그램의 홈 페이지에서 항목을 표시 하려면 "사용자 정의 컨트롤"를 만듭니다. 있으므로이 컨트롤을 단순히 끌어서 좋아요 페이지로 Visual Studio의 디자이너에서 컨트롤을 삭제 하 여 모든 페이지에서 사용할 수 있습니다.

Visual Studio의 솔루션 탐색기에서 솔루션 이름을 마우스 오른쪽 단추로 클릭 하 고 "컨트롤" 라는 새 디렉터리를 만듭니다. 필요 없을 때 도움을 받을 "컨트롤" 디렉터리에 있는 모든 사용자 정의 컨트롤을 만들어 구성 하는 프로젝트를 유지 합니다.

컨트롤 폴더 단추로 클릭 하 고 "새 항목"를 선택 합니다.

![](tailspin-spyworks-part-7/_static/image4.jpg)

제어권 "PopularItems"의 이름을 지정 합니다. 사용자 정의 컨트롤에 대 한 파일 확장명이.ascx 하지.aspx가 있는지 확인 합니다.

인기 있는 항목 사용자 제어권을 다음과 같이 정의 됩니다.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample10.aspx)]

여기에서는 아직이 응용 프로그램에서 사용 하지 않은 메서드를 사용 하는 것입니다. 반복기 컨트롤 사용 및 데이터 소스 제어를 사용 하는 대신 LINQ to Entities 쿼리 결과에 반복기 컨트롤에 바인딩하는 것입니다.

이 컨트롤의 코드 숨김에 할까요 다음과 같습니다.

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample11.cs)]

Note 우리의 컨트롤의 태그의 위쪽에이 중요 한 줄도 합니다.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample12.aspx)]

분을 분 단위로 가장 인기 있는 항목을 변경 하지 않으므로 하므로 응용 프로그램의 성능을 향상 시키기 위해 고통의 지시문을 추가할 수 있습니다. 이 지시어 컨트롤 코드 컨트롤의 캐시 된 출력 만료 되 면 실행만 발생 합니다. 그렇지 않은 경우 컨트롤의 출력 캐시 된 버전이 사용 됩니다.

하기만 하면 됩니다 가격 Default.aspc 페이지에는 새 컨트롤을 포함 합니다.

사용 하 여 끌어서 기본 양식 열기 열에는 컨트롤의 인스턴스를 놓습니다.

![](tailspin-spyworks-part-7/_static/image5.jpg)

이제 응용 프로그램 실행에서는 홈 페이지 가장 인기 있는 항목이 표시 됩니다.

![](tailspin-spyworks-part-7/_static/image6.jpg)

## <a id="_Toc260221679"></a>(매개 변수가 있는 사용자 정의 컨트롤)를 제어 "구입 도"

두 번째 사용자 컨트롤 만들 것을 추천 상황에 맞는 구체적인 정도 추가 하 여 다음 수준으로 판매 소요 됩니다.

최상위 "구입도" 항목을 계산 하려면 논리는 특수 합니다.

"구입도" 제어권 현재 선택 된 제품 Id에 대 한 (이전에 구입) OrderDetails 레코드를 선택한 발견 된 고유한 각 주문에 대 한 Orderid 잡고 됩니다.

그런 다음 선택 합니다 al 제품 이러한 모든 주문 및 수량이 구입 합계입니다. 상위 5 개 항목을 표시 알아보고 그 수량 합계 하 여 제품을 정렬 하겠습니다.

이 논리의 복잡성 들어 म 저장 프로시저로이 알고리즘을 구현 합니다.

저장된 프로시저에 대 한 T-SQL은 다음과 같습니다.

[!code-sql[Main](tailspin-spyworks-part-7/samples/sample13.sql)]

엔터티 데이터 모델 테이블 및 엔터티 데이터 모델 필요 했습니다 뷰 외에도 지정한 기 하, 생성 된 시점과 응용 프로그램에서는 포함 하는 경우이 저장된 프로시저 (SelectPurchasedWithProducts) 데이터베이스에 있던 note 이 저장된 프로시저를 포함 해야 합니다.

엔터티 데이터 모델에서 저장된 프로시저에 액세스 하는 함수를 가져올 해야 합니다.

디자이너에서 열고 모델 브라우저를 열고 솔루션 탐색기에서 엔터티 데이터 모델을 두 번 클릭 한 다음 디자이너에서 마우스 오른쪽 단추로 클릭 하 고 "함수 가져오기 추가"를 선택 합니다.

![](tailspin-spyworks-part-7/_static/image1.png)

이렇게 하면이 대화 상자를 열립니다.

![](tailspin-spyworks-part-7/_static/image2.png)

필드 "SelectPurchasedWithProducts"을 선택 하면 위에 표시 된 대로 입력 하 고 가져온된 함수 이름에 대 한 프로시저 이름을 사용 합니다.

"확인"을 클릭 합니다.

에서는 모델의 다른 항목을 수 있습니다 단순히 저장된 프로시저에 대해 프로그래밍할 수이 위해서입니다.

따라서 우리의 "컨트롤" 폴더에서 AlsoPurchased.ascx 라는 새 사용자 정의 컨트롤을 만듭니다.

이 컨트롤에 대 한 태그 PopularItems 컨트롤에 아주 익숙할 것입니다.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample14.aspx)]

주목할 만한 차이점은 항목의 렌더링 해야 하는 제품에 의해 다르기 때문 출력 캐싱하지입니다.

ProductId는 컨트롤에는 "property" 됩니다.

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample15.cs)]

컨트롤의 PreRender 이벤트 처리기에서에서는 다음 세 가지 작업을 수행 하는 eed 합니다.

1. ProductID 설정 되어 있는지 확인 합니다.
2. 현재 인스턴스와 구매한 제품이 있는지 확인 합니다.
3. # 2에서 결정 된 대로 일부 항목을 출력 합니다.

모델을 통해 저장된 프로시저를 호출 하는 것이 얼마나 쉬운지 note 합니다.

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample16.cs)]

없습니다 "도 구매 하 는" 확인 한 후 쿼리에 의해 반환 된 결과에 반복기를 바인딩할 단순히 수 있습니다.

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample17.cs)]

"구입 도" 아무것도 없는 경우 카탈로그에서 다른 인기 있는 항목 단순히 표시 합니다.

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample18.cs)]

"구입도" 항목을 보려면 ProductDetails.aspx 페이지를 열고 태그의이 위치에 나타나도록 솔루션 탐색기에서 AlsoPurchased 컨트롤을 끌어 놓습니다.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample19.aspx)]

이렇게 세부 내용 페이지 맨 위에 있는 컨트롤에 대 한 참조가 만들어집니다.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample20.aspx)]

AlsoPurchased 사용자 정의 컨트롤에는 ProductId 정수가 필요 하므로 제어권의 ProductID 속성 페이지의 현재 데이터 모델 항목에 대해 Eval 문을 사용 하 여 설정 됩니다.

![](tailspin-spyworks-part-7/_static/image3.png)

빌드 및 지금 실행 고 제품 찾아보기 때는 "구입도" 항목 보면 됩니다.

![](tailspin-spyworks-part-7/_static/image7.jpg)

>[!div class="step-by-step"]
[이전](tailspin-spyworks-part-6.md)
[다음](tailspin-spyworks-part-8.md)
