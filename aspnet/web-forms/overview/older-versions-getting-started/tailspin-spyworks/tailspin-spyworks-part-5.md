---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-5
title: '5 부: 비즈니스 논리 | Microsoft Docs'
author: JoeStagner
description: 이 자습서 시리즈 모든 Tailspin Spyworks 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 5 부 일부 비즈니스 논리를 추가합니다.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: eaef475a-ca91-47ea-a4a7-d074005ed80c
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-5
msc.type: authoredcontent
ms.openlocfilehash: e18acb66dbdb3bd3e0dfa21193f617dad82afc74
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41835543"
---
<a name="part-5-business-logic"></a>5 부: 비즈니스 논리
====================
[Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks.NET 플랫폼에 대 한 강력 하 고 확장 가능한 응용 프로그램을 생성 하는 방법을 매우 단순 하는 방법을 보여 줍니다. 해제 쇼핑, 체크 아웃 및 관리를 포함 하는 온라인 상점을 만들려고 ASP.NET 4에서 강력한 새 기능을 사용 하는 방법을 보여 줍니다.
> 
> 이 자습서 시리즈 모든 Tailspin Spyworks 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 5 부 일부 비즈니스 논리를 추가합니다.


## <a id="_Toc260221671"></a>  일부 비즈니스 논리 추가

웹 사이트를 방문 하는 사람이 될 때마다 사용할 수 있는 쇼핑 경험을 합니다. 방문자 찾아 등록 하거나 로그인 하지 않더라도 장바구니에 항목을 추가 하는 일을 할 수 있습니다. 체크 아웃할 준비 되 면 부여 됩니다 인증 하는 옵션 및 하지 않은 경우 아직 멤버 됩니다 계정을 만들지 못했습니다.

즉, 익명 상태에서 "등록 된 사용자" 상태로 쇼핑 카트를 변환 하는 논리를 구현 해야 합니다.

보겠습니다 "클래스" 라는 디렉터리를 만들려면 다음 마우스 오른쪽 단추로 클릭 폴더 MyShoppingCart.cs 라는 새 "Class" 파일을 만듭니다

![](tailspin-spyworks-part-5/_static/image1.jpg)

![](tailspin-spyworks-part-5/_static/image1.png)

앞서 언급 했 듯이 MyShoppingCart.aspx 페이지를 구현 하는 클래스 확장 해 보겠습니다 하 고 사용 하 여 수행 됩니다 것입니다. NET의 강력한 "부분 클래스" 구문입니다.

MyShoppingCart.aspx.cf 파일에 생성된 호출이 다음과 같이 표시 됩니다.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample1.cs)]

Note "부분" 키워드를 사용 합니다.

방금 생성 하는 클래스 파일을 다음과 같이 표시 됩니다.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample2.cs)]

이 구현도이 파일에 partial 키워드를 추가 하 여 병합 합니다.

이제이 새 클래스 파일은 다음과 같습니다.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample3.cs)]

클래스를 추가 하는 첫 번째 메서드는 "AddItem" 메서드입니다. 이것이 사용자의 제품 목록 및 제품 정보 페이지의 "아트를 추가" 링크를 클릭할 때 궁극적으로 호출 되는 방법입니다.

다음을 사용 하 여 추가 페이지의 맨 위에 있는 문.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample4.cs)]

및 MyShoppingCart 클래스에 다음이 메서드를 추가 합니다.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample5.cs)]

항목이 바구니에 이미 인지 확인 하려면 LINQ to Entities 사용 하는 것입니다. 따라서 항목의 주문 수량과 업데이트를 하는 경우이 고, 그렇지을 만들겠습니다. 선택한 항목에 대 한 새 항목

이 메서드를 호출 하기 위해이 메서드를 클래스 뿐만 아니라 다음 항목을 추가한 후 = 장바구니 현재 표시 되는 AddToCart.aspx 페이지를 구현 합니다.

솔루션 탐색기에서 솔루션 이름을 마우스 오른쪽 단추로 클릭 하 고 추가 하 고 이전에 수행한 대로 AddToCart.aspx 라는 새 페이지입니다.

이 페이지를 사용 하 여 구현에서 재고 부족 문제 등과 같은 중간 결과 표시할 수 없습니다 것를 페이지 실제로 렌더링 하지만 대신 "추가" 논리를 호출 되며 리디렉션.

이렇게 하려면 페이지에 다음 코드를 추가 하겠습니다\_Load 이벤트입니다.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample6.cs)]

쿼리 문자열 매개 변수 및 클래스의 AddItem 메서드를 호출 하 고 쇼핑 카트에 추가 제품 검색 되는 note 합니다.

발생 한 오류가 없다고 가정할 경우 다음 구현 완전히는 SHoppingCart.aspx 페이지로 제어가 전달 됩니다. 오류가 없어야 하는 경우 예외를 throw 했습니다.

현재 구현 하지 않았기 아직 전역 오류 처리기를이 예외는 응용 프로그램에서 처리 되지 않은 이동 하지만이 곧 해결할 것입니다.

또한 Debug.Fail() (통해 사용 가능 문의 사용 `using System.Diagnostics;)`

응용 프로그램 디버거 내에서 실행 되,이 메서드는 지정 하는 오류 메시지와 함께 응용 프로그램 상태에 대 한 정보를 사용 하 여 자세한 대화 상자가 표시 됩니다.

경우 Debug.Fail() 문 프로덕션에서 실행 되는 무시 됩니다.

당사의 쇼핑 카트 클래스 이름과 "GetShoppingCartId" 메서드를 호출 하는 위의 코드에 기록 됩니다.

다음과 같이 메서드를 구현 하는 코드를 추가 합니다.

Note는 또한 추가한 업데이트 및 체크 아웃 단추 및 레이블을 카트 "합계"를 표시할 수 있습니다.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample7.cs)]

이제 항목 당사의 쇼핑 카트를 추가할 수 있지만 제품을 추가한 후 카트를 표시 하는 논리를 구현 하지 않았습니다.

따라서 MyShoppingCart.aspx 페이지에서에서는 추가 EntityDataSource 컨트롤을 GridVire 컨트롤을 다음과 같이 합니다.

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample8.aspx)]

업데이트 카트 단추를 두 번 클릭 하 고 태그에 선언에 지정 된 클릭 이벤트 처리기를 생성할 수 있도록 디자이너에서 폼을 호출 합니다.

나중에 세부 정보 구현 하겠습니다 하지만 이렇게 보겠습니다 빌드하고 오류 없이 응용 프로그램을 실행 합니다.

응용 프로그램을 실행 하 고 장바구니에 항목을 추가 하는 경우이 표시 됩니다.

![](tailspin-spyworks-part-5/_static/image2.jpg)

것에서 벗어난 "default" 표 형태 창 표시 세 개의 사용자 지정 열을 구현 하 여 참고 합니다.

즉 수량에 대 한 "바인딩된" 필드를 편집 가능 합니다.

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample9.aspx)]

다음은 품목 합계가 (항목 시간을 정렬할 수량으로 비용)를 표시 하는 "계산된" 열:

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample10.aspx)]

마지막으로 사용자가 항목을 쇼핑 차트에서 제거할 수 있는지를 나타내는 데 사용할 CheckBox 컨트롤을 포함 하는 사용자 지정 열이 있는 합니다.

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample11.aspx)]

![](tailspin-spyworks-part-5/_static/image3.jpg)

알 수 있듯이 총 줄이 비어 있으므로 순서 주문 총액을 계산 하려면 일부 논리를 추가 합니다.

먼저 MyShoppingCart 클래스 "GetTotal" 메서드를 구현 하겠습니다.

MyShoppingCart.cs 파일에 다음 코드를 추가 합니다.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample12.cs)]

페이지에서 다음\_Load 이벤트 처리기는 GetTotal 메서드 호출 수입니다. 동시에 쇼핑 카트가 비어 있는지 있으면 표시를 적절 하 게 조정 하는 테스트를 추가 하겠습니다.

쇼핑 카트 비어 있는 경우이 시작 합니다.

![](tailspin-spyworks-part-5/_static/image4.jpg)

및이 합계 그렇지 않은 경우.

![](tailspin-spyworks-part-5/_static/image5.jpg)

그러나이 페이지 아직 완전 하지 않습니다.

일부 바뀐 것 같습니다 표의 대로 새 수량 값을 확인 하 고 제거 하도록 표시 된 항목을 제거 하 여 쇼핑 카트를 다시 계산 하려면 추가 논리가 필요 합니다.

사용자 제거에 대 한 항목을 표시 하는 경우 사례를 처리 하는 MyShoppingCart.cs에서 당사의 쇼핑 카트 클래스 "RemoveItem" 메서드를 추가할 수 있습니다.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample13.cs)]

이제 보겠습니다 ad 사용자를 GridView에 품질을 간단히 변경 될 때 상황을 처리 하는 메서드.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample14.cs)]

현재 위치에서 기본 제거 및 업데이트 기능을 사용 하 여 실제로 데이터베이스에서 쇼핑 카트를 업데이트 하는 논리를 구현할 수 있습니다. (에서 MyShoppingCart.cs)

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample15.cs)]

두 개의 매개 변수를 필요로 하이 메서드는 사실을 알 수 있습니다. 하나는 쇼핑 카트 Id 이며 다른 사용자 정의 형식인 개체의 배열입니다.

사용자 인터페이스 세부 사항에서이 논리의 종속성을 최소화 하기 위해 사용할 메서드 GridView 컨트롤에 직접 액세스할 필요 없이 코드에 쇼핑 카트에 항목을 전달할 수 있는 데이터 구조를 정의한 합니다.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample16.cs)]

MyShoppingCart.aspx.cs 파일의 것이 구조 업데이트 단추 클릭 이벤트 처리기에 다음과 같이 사용할 수 있습니다. 카트를 업데이트 하는 것 외에도 카트 합계도 업데이트할 것 note 합니다.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample17.cs)]

이 코드 줄을 사용 하 여 관심 있는 특정 note:

[!code-javascript[Main](tailspin-spyworks-part-5/samples/sample18.js)]

GetValues()는 MyShoppingCart.aspx.cs에서 다음과 같이 구현 하는 특수 한 도우미 함수입니다.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample19.cs)]

이 GridView 컨트롤의 바인딩된 요소 값에 액세스 하는 방법은 제공 합니다. 우리의 "항목 제거" CheckBox 컨트롤에 바인딩되지 않은 하므로 FindControl() 메서드를 통해 액세스 됩니다 것입니다.

이 프로젝트의 개발 단계 조만간 체크 아웃 프로세스를 구현 하도록 합니다.

보겠습니다 이렇게 하려면 먼저 멤버 자격 데이터베이스를 생성 하 고 사용자 멤버 자격 리포지토리를 추가 하려면 Visual Studio를 사용 합니다.

> [!div class="step-by-step"]
> [이전](tailspin-spyworks-part-4.md)
> [다음](tailspin-spyworks-part-6.md)
