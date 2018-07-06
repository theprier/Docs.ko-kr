---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-7
title: '7 부: 추가 기능 | Microsoft Docs'
author: JoeStagner
description: 이 자습서 시리즈 모든 Tailspin Spyworks 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 7 부 계정 revie 등의 추가 기능을 추가 하는 중...
ms.author: aspnetcontent
ms.date: 07/21/2010
ms.assetid: 50223ee9-11b9-4cf3-bca2-e2f10bf471f3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-7
msc.type: authoredcontent
ms.openlocfilehash: 47402ccdfb702dc1bb1bdb4e634a7cd6f5ebc235
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37831650"
---
<a name="part-7-adding-features"></a>7 부: 추가 기능
====================
[Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks.NET 플랫폼에 대 한 강력 하 고 확장 가능한 응용 프로그램을 생성 하는 방법을 매우 단순 하는 방법을 보여 줍니다. 해제 쇼핑, 체크 아웃 및 관리를 포함 하는 온라인 상점을 만들려고 ASP.NET 4에서 강력한 새 기능을 사용 하는 방법을 보여 줍니다.
> 
> 이 자습서 시리즈 모든 Tailspin Spyworks 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 7 부 계정 검토, 제품 사용 후기, 및 "인기 있는 항목" 및 "도 구매한" 사용자 정의 컨트롤 등의 추가 기능을 추가합니다.


## <a id="_Toc260221673"></a>  추가 기능

사용자 카탈로그 찾아보기, 장바구니의 항목을 배치할 및 체크 아웃 프로세스를 완료 하지만 가지 다양 한 지원 기능 사이트를 개선 하기 위해 포함 됩니다.

1. 계정 검토 (목록 주문 배치 및 세부 정보를 확인 합니다.)
2. 프런트 페이지에 몇 가지 상황에 맞는 특정 콘텐츠를 추가 합니다.
3. 카탈로그에는 기능을 사용자가 검토 제품을 추가 합니다.
4. 프런트 페이지에서 제어 하는 인기 있는 항목 및 위치를 표시 하려면 사용자 컨트롤을 만듭니다.
5. "구입" 사용자 정의 컨트롤을 만들고 제품 정보 페이지에 추가 합니다.
6. 연락처 추가 페이지입니다.
7. 추가 페이지에 대 한 합니다.
8. 전역 오류

## <a id="_Toc260221674"></a>  계정 검토

"Account" 폴더에 하나의 명명 된 OrderList.aspx와는 다른 명명 된 OrderDetails.aspx 두.aspx 페이지 만들기

이전에 것 만큼 OrderList.aspx는 GridView 및 EntityDataSoure 컨트롤을 활용 합니다.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample1.aspx)]

EntityDataSoure 사용자 이름을 필터링 하는 Orders 테이블에서 레코드를 선택 합니다 (참조는 WhereParameter) 사용자 로그의 경우 세션 변수에 설정 하는 것입니다.

GridView의 HyperlinkField에서 이러한 매개 변수를 또한 note:

[!code-xml[Main](tailspin-spyworks-part-7/samples/sample2.xml)]

이러한 OrderDetails.aspx 페이지에 쿼리 문자열 매개 변수로 OrderID 필드를 지정 하는 각 제품에 대 한 주문 세부 정보 보기에 대 한 링크를 지정 합니다.

## <a id="_Toc260221675"></a>  OrderDetails.aspx

주문을 표시 하는 FormView 주문 데이터 및 GridView 사용 하 여 다른 EntityDataSource 주문의 모든 품목을 표시 하려면 액세스를 EntityDataSource 컨트롤을 사용 하 여 됩니다.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample3.aspx)]

코드 숨김 파일 (OrderDetails.aspx.cs)의 두 가지 작은 비트 했습니다.

먼저 OrderDetails에 항상 OrderId 가져옵니다 있는지 확인 해야 합니다.

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample4.cs)]

또한 계산 되어 총 품목에서 순서를 표시 해야 합니다.

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample5.cs)]

## <a id="_Toc260221676"></a>  홈 페이지

Default.aspx 페이지에 몇 가지 정적 콘텐츠를 추가 해 보겠습니다.

먼저 "콘텐츠" 폴더를 만들겠습니다 및 그 안에 이미지 폴더 (및 홈 페이지에서 사용 될 이미지가 포함 됩니다.)

Default.aspx 페이지의 아래쪽 자리 표시자에 다음 태그를 추가 합니다.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample6.aspx)]

## <a id="_Toc260221677"></a>  제품 검토

먼저 링크를 사용 하 여 단추에서는 제품 검토를 입력 하는 데 사용할 수 있는 폼에 추가 합니다.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample7.aspx)]

![](tailspin-spyworks-part-7/_static/image1.jpg)

쿼리 문자열에는 ProductID 전달 하는 참고

다음 ReviewAdd.aspx 라는 페이지를 추가 해 보겠습니다

이 페이지는 ASP.NET AJAX Control Toolkit을 사용 합니다. 경우 이미 않았다면에서 다운로드할 수 있도록 [DevExpress](http://devexpress.com/act) 사용 하 여 Visual Studio를 사용 하 여 여기에 대 한 도구 키트 설정 지침 이며 [ https://www.asp.net/learn/ajax-videos/video-76.aspx ](../../../videos/ajax-control-toolkit/how-do-i-get-started-with-the-aspnet-ajax-control-toolkit.md)합니다.

디자인 모드에서 컨트롤 및 유효성 검사기 도구 상자에서 끌어서 아래와 같은 양식을 작성 합니다.

![](tailspin-spyworks-part-7/_static/image2.jpg)

태그는 다음과 비슷합니다.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample8.aspx)]

검토를 입력할 수 있습니다 했으므로 제품 페이지에서 해당 검토를 표시할 수 있습니다.

ProductDetails.aspx 페이지로이 태그를 추가 합니다.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample9.aspx)]

이제 응용 프로그램을 실행 하 고 제품 탐색 고객 검토를 비롯 한 제품 정보를 보여 줍니다.

![](tailspin-spyworks-part-7/_static/image3.jpg)

## <a id="_Toc260221678"></a>  인기 있는 항목 컨트롤 (사용자 정의 컨트롤 만들기)

웹 사이트의 판매를 늘리기 위해 몇 가지 기능이 "추천 판매" 많이 사용 되거나 관련 제품에 추가 합니다.

이러한 기능 중 첫 번째 제품 카탈로그에 더 인기 있는 제품의 목록이 됩니다.

응용 프로그램의 홈 페이지에서 항목을 판매 맨 위에 표시 하려면 "사용자 컨트롤"을 만들겠습니다. 되므로이 컨트롤을 간단히 끌어서 우리는 모든 페이지에 Visual Studio의 디자이너에서 컨트롤을 삭제 하 여 모든 페이지에서 사용할 수 있습니다.

Visual Studio의 솔루션 탐색기에서 솔루션 이름을 마우스 오른쪽 단추로 클릭 하 고 "컨트롤" 라는 새 디렉터리를 만듭니다. 이렇게 하는 데 필요한 상태인 동안 "컨트롤" 디렉터리에는 모든 사용자 정의 컨트롤을 만들어서 구성 하는 프로젝트를 유지할 수 것입니다.

Controls 폴더 단추로 클릭 하 고 "새 항목"을 선택 합니다.

![](tailspin-spyworks-part-7/_static/image4.jpg)

"PopularItems"의 컨트롤에 대 한 이름을 지정 합니다. 사용자 컨트롤에 대 한 파일 확장명은.ascx.aspx 하지는 참고 합니다.

인기 항목 사용자 제어권을 다음과 같이 정의 됩니다.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample10.aspx)]

여기에서는 아직이 응용 프로그램에 사용 하지 않은 메서드를 사용 하는 것입니다. Repeater 컨트롤을 사용 하는 것을 데이터 소스 컨트롤을 사용 하는 대신는 linq to Entities 쿼리 결과에 Repeater 컨트롤을 바인딩하는 것입니다.

이 컨트롤의 코드 숨김에 수행 하는 다음과 같이 합니다.

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample11.cs)]

Note는 컨트롤의 태그의 맨 위에 있는 중요 한 줄도 합니다.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample12.aspx)]

분당 기준 가장 인기 있는 항목을 변경 하지 않으므로 하므로 응용 프로그램의 성능을 향상 시키기 위해 고통의 지시문을 추가할 수 있습니다. 이 지시어를 사용 하면 컨트롤의 출력 캐시를 만료 될 때만 실행 될 컨트롤 코드가 있습니다. 그렇지 않은 경우 컨트롤의 출력 캐시 된 버전이 사용 됩니다.

작업을 수행 해야 모든는 이제 Default.aspc 페이지에는 새 컨트롤을 포함 합니다.

사용 하 여 끌어서 열기 열의 기본 폼에 컨트롤의 인스턴스를 놓습니다.

![](tailspin-spyworks-part-7/_static/image5.jpg)

이제 응용 프로그램을 실행할 때 홈 페이지에 가장 인기 있는 항목이 표시 됩니다.

![](tailspin-spyworks-part-7/_static/image6.jpg)

## <a id="_Toc260221679"></a>  (매개 변수를 사용 하 여 사용자 정의 컨트롤) 제어 "구입"

두 번째 사용자 컨트롤을 만들어 다음 수준에 판매 하는 상황에 맞는 구체적인 정도 추가 하 여 추천 걸립니다.

상위 "구입" 항목을 계산 하는 논리는 어렵습니다.

"구입" 제어권 현재 선택 된 ProductID에 대 한 (이전에 구매한 경우) OrderDetails 레코드를 선택한 있는 고유한 각 주문의 Orderid를 잡고 됩니다.

그런 다음 선택 al 제품에서 이러한 모든 Orders와 구매 수량 합계입니다. 제품 수량 합계 하 여 정렬 하 고 상위 5 개 항목 표시 됩니다.

이 논리의 복잡성을 지정 했습니다 저장 프로시저로이 알고리즘을 구현 합니다.

저장된 프로시저에 대 한 T-SQL은 다음과 같습니다.

[!code-sql[Main](tailspin-spyworks-part-7/samples/sample13.sql)]

테이블 및 엔터티 데이터 모델에서는 필요한 뷰 외에 지정한 엔터티 데이터 모델을 생성할 때 및 응용 프로그램에에서는 포함 하는 경우이 저장된 프로시저 (SelectPurchasedWithProducts) 데이터베이스에 있었음을 note합니다 이 저장된 프로시저를 포함 해야 합니다.

엔터티 데이터 모델에서 저장된 프로시저에 액세스 하는 함수 가져오기 해야 합니다.

엔터티 데이터 모델 디자이너에서 열고 Model 브라우저를 열고 솔루션 탐색기에서 두 번 클릭 한 다음 디자이너에서 마우스 오른쪽 단추로 클릭 하 고 "Function Import 추가"를 선택 합니다.

![](tailspin-spyworks-part-7/_static/image1.png)

그러면이 대화 상자가 열립니다.

![](tailspin-spyworks-part-7/_static/image2.png)

"SelectPurchasedWithProducts"를 선택 하면 위에 표시 된 대로 필드 입력 하 고이 가져온 함수의 이름에 대 한 프로시저 이름을 사용 합니다.

"확인"을 클릭 합니다.

에서는 모델의 다른 항목 수 것으로 간단히 저장된 프로시저에 대해 프로그래밍할 수이 위해서입니다.

따라서이 "컨트롤" 폴더에 AlsoPurchased.ascx 라는 새 사용자 컨트롤을 만듭니다.

이 컨트롤에 대 한 태그 PopularItems 컨트롤에 매우 익숙할 것입니다.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample14.aspx)]

주목할 만한 차이점은 캐싱하지 않으면 출력 항목의 렌더링 되어야 하는 제품에서 달라 집니다 때문입니다.

ProductId는 컨트롤에 "property" 됩니다.

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample15.cs)]

컨트롤의 PreRender 이벤트 처리기에서에서는 eed 다음 세 가지 작업을 수행 합니다.

1. ProductID 설정 되어 있는지 확인 합니다.
2. 현재는 구매한 모든 제품 있는지 확인 합니다.
3. 2 단계에서에서 결정 된 대로 일부 항목을 출력 합니다.

모델을 통해 저장된 프로시저를 호출 하려면 얼마나 쉬운지 note 합니다.

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample16.cs)]

없습니다 "도 구매"를 확인 한 후 쿼리에서 반환 된 결과에 반복기를 바인딩할 단순히 수 있습니다.

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample17.cs)]

"구입" 항목이 없는 경우 카탈로그에서 다른 인기 있는 항목만 단순히 표시 됩니다.

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample18.cs)]

"구입" 항목을 보려면 ProductDetails.aspx 페이지를 열려면 끌어서 AlsoPurchased 컨트롤 솔루션 탐색기에서 태그의이 위치에 표시 되도록 합니다.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample19.aspx)]

이렇게 세부 내용 페이지의 맨 위에 있는 컨트롤에 대 한 참조가 만들어집니다.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample20.aspx)]

AlsoPurchased 사용자 정의 컨트롤에는 ProductId 숫자로 필요 하므로 페이지의 현재 데이터 모델 항목에 대해 Eval 문과 사용 하 여이 컨트롤의 ProductID 속성을 설정 됩니다.

![](tailspin-spyworks-part-7/_static/image3.png)

빌드 및 지금 실행 하 고 제품으로 이동 "구입" 항목을 볼 했습니다.

![](tailspin-spyworks-part-7/_static/image7.jpg)

> [!div class="step-by-step"]
> [이전](tailspin-spyworks-part-6.md)
> [다음](tailspin-spyworks-part-8.md)
