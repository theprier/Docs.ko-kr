---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-8
title: '8 부: 쇼핑 카트 Ajax 업데이트를 사용 하 여 | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 8 부 Ajax 업데이트와 쇼핑 카트를 설명합니다.
ms.author: aspnetcontent
ms.date: 04/21/2011
ms.assetid: 26b2f55e-ed42-4277-89b0-c941eb754145
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-8
msc.type: authoredcontent
ms.openlocfilehash: 881d47b5b4df5a4d310a1b3a7eec6ee97b0d42ea
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37823841"
---
<a name="part-8-shopping-cart-with-ajax-updates"></a>Ajax 업데이트를 사용 하 여 8 부: 쇼핑 카트
====================
[Jon Galloway](https://github.com/jongalloway)

> MVC Music Store 자습서 응용 프로그램을 소개 하 고 웹 개발을 위한 ASP.NET MVC 및 Visual Studio를 사용 하는 방법을 단계별로 설명 됩니다.  
>   
> MVC Music Store는 온라인 음악 앨범을 판매 하 고 기본 사이트 관리, 사용자 로그인 및 장바구니 기능을 구현 하는 간단한 샘플 저장소 구현입니다.  
>   
> 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 8 부 Ajax 업데이트와 쇼핑 카트를 설명합니다.


등록 하지 않으면 카트에 앨범을 배치할 수 있게 될 것 이지만 전체를 체크 아웃 게스트로 등록 해야 합니다. 쇼핑 및 체크 아웃 프로세스를 두 명의 컨트롤러도 구분 됩니다: 익명으로 항목을 카트에 추가 허용 하는 ShoppingCart 컨트롤러 및 체크 아웃 프로세스를 처리 하는 체크 아웃 컨트롤러입니다. 이 섹션에서는 쇼핑 카트를 사용 하 여 시작 하 고 다음 섹션에서 체크 아웃 프로세스를 빌드 하겠습니다.

## <a name="adding-the-cart-order-and-orderdetail-model-classes"></a>카트, Order 및 OrderDetail 모델 클래스 추가

쇼핑 카트 및 체크 아웃 프로세스를 확인 하는 일부 새 클래스를 사용 합니다. Models 폴더를 마우스 오른쪽 단추로 클릭 하 고 다음 코드를 사용 하 여 카트 클래스 (Cart.cs)를 추가 합니다.

[!code-csharp[Main](mvc-music-store-part-8/samples/sample1.cs)]

이 클래스는 여기서 사용한 지금 RecordId 속성에 대 한 [키] 특성을 제외 하 고 다른 사용자에 게 매우 유사 합니다. 영구적인 카트 항목 익명 쇼핑 있도록 CartID 라는 문자열 식별자를 갖지만 테이블은 RecordId 라는 정수 기본 키를 포함 합니다. 규칙에 따라 Entity Framework 코드 중심 CartId 또는 ID, 카트 라는 테이블에 대 한 기본 키가 수는 있지만 재정의할 수 있습니다 쉽게 하는 주석 또는 코드를 통해 원하는 경우는 필요 합니다. 사용 하 여 간단한 규칙에서 Entity Framework Code-first, 우리에 부합 될 때의 예가 되었지만 우리는 제한 되지 이들에 의해 제공 하지 않는 경우.

다음으로, 다음 코드를 사용 하 여 프로그램 Order 클래스 (Order.cs)를 추가 합니다.

[!code-csharp[Main](mvc-music-store-part-8/samples/sample2.cs)]

이 클래스는 주문에 대 한 요약 및 배달 정보를 추적합니다. **아직 컴파일되지**이므로 해당 속성이 OrderDetails 탐색 아직 만들지 클래스에 따라 달라 집니다. 이제 추가 하 여 라는 클래스는 OrderDetail.cs, 다음 코드를 추가 수정 해 보겠습니다.

[!code-csharp[Main](mvc-music-store-part-8/samples/sample3.cs)]

한 번의 마지막 업데이트도 DbSet을 포함 하 여 이러한 새 모델 클래스를 노출 하는 Dbset 포함 MusicStoreEntities 클래스를 만들어 보겠습니다&lt;Artist&gt;합니다. 업데이트 된 MusicStoreEntities 클래스 요소로 아래.

[!code-csharp[Main](mvc-music-store-part-8/samples/sample4.cs)]

## <a name="managing-the-shopping-cart-business-logic"></a>쇼핑 카트 비즈니스 논리를 관리합니다.

다음으로 Models 폴더에서 ShoppingCart 클래스를 만듭니다. ShoppingCart 모델 카트 테이블에 대 한 데이터 액세스를 처리합니다. 또한이 추가 및 장바구니에서 항목을 제거 하기 위한 비즈니스 논리를 처리 합니다.

사용자가 해당 쇼핑 카트에 항목 추가 방금 계정을 등록 하도록 요구 하려고 하지 때문에 할당 됩니다 사용자 임시 고유 식별자 (GUID 또는 전역적으로 고유 식별자를 사용 하 여) 장바구니에 액세스 하면 됩니다. ASP.NET 세션 클래스를 사용 하 여이 ID 저장 됩니다.

*참고: ASP.NET 세션은 사이트를 떠난 후에 만료 되는 사용자 관련 정보를 저장 하는 편리한 장소입니다. 세션 상태를 잘못 사용 하면 대규모 사이트에 성능에 미치는 영향을 미칠 수 있습니다, 있지만 밝은 사용 데모 목적 잘 작동 합니다.*

ShoppingCart 클래스는 다음 메서드를 노출합니다.

**AddToCart** 매개 변수로 앨범을 가져오고 사용자의 장바구니에 추가 합니다. 카트 표에서 각 앨범에 대 한 수량을 추적 하므로 필요한 경우 새 행 만들기 또는 사용자가 이미 앨범의 사본 하나를 정렬 하는 경우 수량 증가 논리가 포함 되어 있습니다.

**RemoveFromCart** 앨범 ID를 가져오고 사용자의 카트에서 제거 합니다. 사용자만 앨범의 복사본 하나에 있으면 해당 카트, 행이 제거 됩니다.

**EmptyCart** 사용자의 쇼핑 카트에서 모든 항목을 제거 합니다.

**GetCartItems** 표시 또는 처리에 대 한 CartItems 목록을 검색 합니다.

**GetCount** 검색을 사용자가 해당 쇼핑 카트에에서 앨범의 총 수입니다.

**GetTotal** 바구니에 있는 모든 항목의 총 비용을 계산 합니다.

**CreateOrder** 체크 아웃 단계 동안 쇼핑 카트는 순서로 변환 합니다.

**GetCart** 카트 개체를 가져오려면이 컨트롤러를 허용 하는 정적 메서드입니다. 사용 합니다 **GetCartId** 는 CartId 사용자의 세션에서 읽기를 처리 하는 방법입니다. GetCartId 메서드 HttpContextBase 필요 하므로 사용자의 CartId 사용자의 세션에서 읽을 수 있습니다.

전체 다음과 같습니다 **ShoppingCart 클래스**:

[!code-csharp[Main](mvc-music-store-part-8/samples/sample5.cs)]

## <a name="viewmodels"></a>ViewModels

쇼핑 카트 컨트롤러는 모델 개체에 완전히 매핑되지 않으므로 해당 보기에 복잡 한 일부 정보를 전달 해야 합니다. 뷰에;에 맞게 모델을 수정 하려고 하지 않습니다. 모델 클래스에는 사용자 인터페이스가 아닌 도메인을 나타내야 합니다. 하나의 솔루션 정보 저장소 관리자 드롭다운 정보를 사용 하 여 수행한 있지만 ViewBag을 통해 많은 정보를 전달할 관리 하기가 가져옵니다 ViewBag 클래스를 사용 하 여 뷰를 전달할 수 있습니다.

이 솔루션을 사용 하는 것은 *ViewModel* 패턴입니다. 이 패턴을 사용 하는 경우 시나리오는 특정 보기에 최적화 된 및 우리의 보기 템플릿에서 필요한 동적 값/콘텐츠에 대 한 속성을 노출 하는 강력한 형식의 클래스 만듭니다. 다음 컨트롤러 클래스 채우고 이러한 보기에 최적화 된 클래스를 사용 하 여 보기 템플릿은 전달할 수 있습니다. 형식 안전성, 컴파일 시간 검사 및 편집기 IntelliSense 템플릿 보기 내에서이 수 있습니다.

쇼핑 카트 컨트롤러에서 모델 사용에 대 한 두 가지 보기를 만들겠습니다:는 ShoppingCartViewModel 사용자의 쇼핑 카트 내용의 보유할 및 사용자 항목을 제거 하는 경우 확인 정보를 표시 하는 ShoppingCartRemoveViewModel 됩니다 해당 카트에서 합니다.

구성 고침은 프로젝트의 루트에 새 ViewModels 폴더를 만들어 보겠습니다. 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 추가 선택 합니다 / 새 폴더입니다.

![](mvc-music-store-part-8/_static/image1.jpg)

ViewModels 폴더를 이름을 지정 합니다.

![](mvc-music-store-part-8/_static/image1.png)

다음으로, ViewModels 폴더에 ShoppingCartViewModel 클래스를 추가 합니다. 두 개의 속성이: 카트 항목 목록과 바구니에 모든 항목에 대 한 총 가격을 저장 하는 10 진수 값입니다.

[!code-csharp[Main](mvc-music-store-part-8/samples/sample6.cs)]

이제는 ShoppingCartRemoveViewModel 다음 네 가지 속성을 사용 하 여 ViewModels 폴더에 추가 합니다.

[!code-csharp[Main](mvc-music-store-part-8/samples/sample7.cs)]

## <a name="the-shopping-cart-controller"></a>쇼핑 카트 컨트롤러

쇼핑 카트 컨트롤러는 세 가지 주요 목적이: 항목을 카트에 추가에서 장바구니에 항목을 제거 및 바구니에 항목을 확인 합니다. 에서는 세 가지 클래스의 사용이 게 방금 만든: ShoppingCartViewModel, ShoppingCartRemoveViewModel, 및 ShoppingCart 합니다. StoreController, StoreManagerController MusicStoreEntities의 인스턴스를 보관할 필드를 추가 하겠습니다.

빈 컨트롤러 템플릿을 사용 하 여 프로젝트에 새 쇼핑 카트 컨트롤러를 추가 합니다.

![](mvc-music-store-part-8/_static/image2.png)

전체 ShoppingCart 컨트롤러는 다음과 같습니다. 인덱스 및 컨트롤러 추가 작업을 매우 친숙 해야 합니다. 제거 및 CartSummary 컨트롤러 작업에는 다음 섹션에서 설명 하겠지만 두 가지 특별 한 경우 처리 합니다.

[!code-csharp[Main](mvc-music-store-part-8/samples/sample8.cs)]

## <a name="ajax-updates-with-jquery"></a>JQuery 사용 하 여 Ajax 업데이트

쇼핑 카트 인덱스 페이지는 ShoppingCartViewModel를 강력한 형식 이므로 하기 전에 동일한 방법을 사용 하 여 목록 뷰 템플릿을 사용 하는 다음 만들겠습니다.

![](mvc-music-store-part-8/_static/image3.png)

그러나 대신 장바구니에서 항목을 제거 하는 Html.ActionLink 사용에서는 사용 하 여 jQuery "연결" RemoveLink HTML 클래스는이 보기에서 모든 링크의 click 이벤트입니다. 폼을 게시 하는 대신이 클릭 이벤트 처리기는 RemoveFromCart 컨트롤러 작업에는 AJAX 콜백만 확인 합니다. RemoveFromCart를 JSON으로 직렬화 된 결과 반환 합니다. jQuery 콜백이 다음 구문 분석 하 고 jQuery를 사용 하 여 네 가지 빠른 업데이트를 수행 합니다.

- 1. 목록에서 삭제 된 앨범을 제거합니다.
- 2. 헤더에 카트 개수를 업데이트합니다.
- 3. 업데이트 메시지를 사용자에 게 표시 됩니다.
- 4. 카트 총 가격 업데이트

제거 시나리오는 Ajax 콜백 인덱스 뷰 내에서 처리 되 고, 이후 RemoveFromCart 작업에 대 한 자세한 보기를 필요 하지 않습니다. /ShoppingCart/Index 뷰에 대 한 전체 코드는 다음과 같습니다.

[!code-cshtml[Main](mvc-music-store-part-8/samples/sample9.cshtml)]

이 테스트 하기 위해 당사의 쇼핑 카트에 항목을 추가할 수 해야 합니다. 업데이트할 예정 우리의 **저장소 세부 정보** "카트에 추가" 단추를 포함 하는 보기입니다. 우리가 하는 동안 일부 추가한는 앨범 추가 정보를 포함할 수 있습니다 것 이므로이 뷰를 마지막으로 업데이트 했습니다: 장르, Artist, 가격 및 앨범 아트. 업데이트 된 코드 저장소 세부 정보 보기에는 아래와 같이 표시 됩니다.

[!code-cshtml[Main](mvc-music-store-part-8/samples/sample10.cshtml)]

이제 수 스토어를 통해 클릭 하 고 테스트 추가 및 앨범 당사의 쇼핑 카트를 제거 합니다. 응용 프로그램을 실행 하 고 저장소 인덱스를 찾습니다.

![](mvc-music-store-part-8/_static/image4.png)

장르를 앨범의 목록을 보려면 다음을 클릭 합니다.

![](mvc-music-store-part-8/_static/image5.png)

이제는 앨범 제목 클릭 하면 "카트에 추가" 단추를 포함 하 여 업데이트 된 앨범 세부 정보 보기를 표시 합니다.

![](mvc-music-store-part-8/_static/image6.png)

"카트에 추가" 단추를 클릭 하면 쇼핑 카트 요약 목록 사용 하 여 당사의 쇼핑 카트 인덱스 뷰를 보여 줍니다.

![](mvc-music-store-part-8/_static/image7.png)

쇼핑 카트를 로드 한 후을 쇼핑 카트에 Ajax 업데이트 카트 링크에서 제거를 클릭할 수 있습니다.

![](mvc-music-store-part-8/_static/image8.png)

쇼핑 카트 등록 되지 않은 사용자가 자신의 카트에 항목을 추가할 수 있는 작업을 빌드 했습니다. 다음 섹션에서는 등록 및 체크 아웃 프로세스를 완료 하도록 수 됩니다.


> [!div class="step-by-step"]
> [이전](mvc-music-store-part-7.md)
> [다음](mvc-music-store-part-9.md)
