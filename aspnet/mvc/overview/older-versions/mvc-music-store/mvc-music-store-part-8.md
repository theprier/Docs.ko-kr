---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-8
title: '8 단계: 쇼핑 카트 Ajax 업데이트 | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다. 8 부 쇼핑 카트 Ajax 업데이트를 설명합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/21/2011
ms.topic: article
ms.assetid: 26b2f55e-ed42-4277-89b0-c941eb754145
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-8
msc.type: authoredcontent
ms.openlocfilehash: 195c01ff0d71b2bfd0c00e71244d47a166330921
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30871287"
---
<a name="part-8-shopping-cart-with-ajax-updates"></a>Ajax 업데이트와 8 단계: 쇼핑 카트
====================
으로 [Jon Galloway](https://github.com/jongalloway)

> MVC Music Store는 소개 하 고 웹 개발에 대 한 ASP.NET MVC와 Visual Studio를 사용 하는 방법을 단계별로 설명 하는 자습서 응용 프로그램.  
>   
> MVC Music Store는 온라인 음악 앨범 판매 및 기본 사이트 관리, 사용자 로그인 및 장바구니 기능을 구현 하는 간단한 샘플 저장소 구현입니다.  
>   
> 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다. 8 부 쇼핑 카트 Ajax 업데이트를 설명합니다.


등록을 하지 않고 카트에 앨범을 배치 하도록 사용자 허용 합니다 하지만 게스트는 완료 체크 아웃으로 등록 해야 합니다. 두 컨트롤러에 쇼핑 및 체크 아웃 프로세스를 구분 됩니다: 익명으로 장바구니에 항목을 추가 하도록 허용 하는 ShoppingCart 컨트롤러 및 체크 아웃 프로세스를 처리 하는 체크 아웃 컨트롤러입니다. 이 섹션에서는 쇼핑 카트로 시작 그런 다음 다음 섹션에는 체크 아웃 프로세스를 작성 합니다.

## <a name="adding-the-cart-order-and-orderdetail-model-classes"></a>카트, 순서 및 OrderDetail 모델 클래스를 추가합니다.

프로세스 당사의 쇼핑 카트 및 체크 아웃 하면 몇 가지 새로운 클래스를 사용 합니다. 모델 폴더를 마우스 오른쪽 단추로 클릭 하 고 다음 코드로 카트 클래스 (Cart.cs)를 추가 합니다.

[!code-csharp[Main](mvc-music-store-part-8/samples/sample1.cs)]

이 클래스는 사용한 지금까지 RecordId 속성에 대 한 [Key] 특성을 제외 하 고 다른 사용자에 게 매우 유사 합니다. 우리의 카트에 항목 라는 CartID 익명 쇼핑 수 있도록 하는 문자열 식별자 하지만 테이블 RecordId 라는 정수 기본 키가 포함 되어 있습니다. 규칙에 따라 엔터티 프레임 워크 코드 중심 CartId 또는 ID, 카트 라는 테이블에 대 한 기본 키 됩니다 하지만 म 쉽게 재정의할 수 있는 주석 또는 코드를 통해 원하는 경우 필요 합니다. 사용 하는 방법을 간단한 규칙에서 Entity Framework 코드 중심 us, 맞게 될 때의 예 이지만 우리는 제한 되지 않으며 타인이 경우에 합니다.

다음으로, 다음 코드와 함께 Order 클래스 (Order.cs)를 추가 합니다.

[!code-csharp[Main](mvc-music-store-part-8/samples/sample2.cs)]

이 클래스는 주문에 대 한 요약 및 배달 정보를 추적 합니다. **아직 컴파일되지**는 아직 만들지 클래스에 종속 되어 있는 OrderDetails 탐색 속성에 있기 때문에, 합니다. 이제 추가 하 여 라는 클래스는 다음 코드를 추가 OrderDetail.cs 문제 해결 하겠습니다.

[!code-csharp[Main](mvc-music-store-part-8/samples/sample3.cs)]

또한 한 DbSet을 포함 하 여 이러한 새 모델 클래스를 표시 하는 DbSets 포함 하도록 MusicStoreEntities 클래스를 마지막 업데이트 한 개 만들면 되&lt;아티스트&gt;합니다. 로 표시 된 업데이트 된 MusicStoreEntities 클래스 아래 합니다.

[!code-csharp[Main](mvc-music-store-part-8/samples/sample4.cs)]

## <a name="managing-the-shopping-cart-business-logic"></a>쇼핑 카트 비즈니스 논리를 관리합니다.

다음으로, ShoppingCart 클래스를 모델 폴더에서 만들겠습니다. ShoppingCart 모델 카트 테이블에 대 한 데이터 액세스를 처리합니다. 또한 것은 추가 및 쇼핑 카트에서 항목을 제거 하기 위한 비즈니스 논리를 처리 합니다.

사용자가 장바구니에 항목 추가를 계정에 등록 하도록 요구 하 않도록, 하기는 할당 사용자가 임시 고유 식별자 (GUID 또는 전역 고유 식별자를 사용 하 여) 쇼핑 카트를 액세스할 때. ASP.NET 세션 클래스를 사용 하 여이 ID 저장 합니다.

*참고: ASP.NET 세션은 사이트를 벗어난 후에 만료 되는 사용자 관련 정보를 저장 하는 편리한 장소입니다. 세션 상태를 잘못 사용 하면 대규모 사이트 성능에 미치는 영향을 있을 수 있지만, 밝은 사용 예시 목적을 위한 잘 작동 합니다.*

ShoppingCart 클래스는 다음 메서드를 노출 합니다.

**AddToCart** 앨범 매개 변수로 사용 하 고 사용자의 장바구니에 추가 합니다. 카트 테이블 각 앨범에 대 한 수량을 추적 하므로 필요한 경우 새 행을 만들 또는 사용자가 이미는 앨범의 복사본이 두 개를 정렬 하는 경우 수량이 증가 하는 논리가 포함 됩니다.

**RemoveFromCart** 앨범 ID를 사용 하 고 사용자의 카트에서 제거 합니다. 사용자는 앨범의 복사본이 두 개 카트에 만으로는, 행이 제거 됩니다.

**EmptyCart** 사용자의 쇼핑 카트에서 모든 항목을 제거 합니다.

**GetCartItems** 표시 또는 처리를 위해 CartItems 목록을 검색 합니다.

**GetCount** 검색 한 앨범을 사용자가 장바구니의 총 수입니다.

**GetTotal** 바구니에 모든 항목의 총 비용을 계산 합니다.

**CreateOrder** 체크 아웃 단계 동안 쇼핑 카트 주문으로 변환 합니다.

**GetCart** 카트 개체를 가져오려면 우리의 컨트롤러 수 있는 정적 메서드입니다. 사용 하 여는 **GetCartId** 는 CartId 사용자의 세션에서 읽기를 처리 하는 메서드. 사용자의 CartId 사용자의 세션에서 읽을 수 있도록 GetCartId 메서드 HttpContextBase를 필요 합니다.

다음 전체은 **ShoppingCart 클래스**:

[!code-csharp[Main](mvc-music-store-part-8/samples/sample5.cs)]

## <a name="viewmodels"></a>ViewModels

당사의 쇼핑 카트 컨트롤러는 모델 개체에 완전히 매핑되지 않으면 해당 보기에 복잡 한 일부 정보를 전달 해야 합니다. 우리의 뷰만 맞게이 모델을 수정 하지는 않을 모델 클래스는 도메인의 사용자 인터페이스를 나타내야 합니다. 한 가지 해결 정보를 관리 하기 어려운 가져옵니다 ViewBag을 통해 많은 정보를 전달 하지만 저장소 관리자 드롭다운 정보와 동일한 방식으로 ViewBag 클래스를 사용 하 여이 뷰를 전달할 수 있습니다.

이 해결 방법은 사용 하 여 *ViewModel* 패턴입니다. 이 패턴을 사용 하는 경우 강력한 형식의 클래스의 특정 보기 시나리오에 최적화 된 및 우리의 템플릿 보기에 필요한 동적 값/콘텐츠에 대 한 속성을 노출 합니다 만듭니다. 컨트롤러 클래스 다음 이러한 보기 액세스에 최적화 된 클래스 우리의 뷰 템플릿을 사용 하려면에 전달을 채울 수 있습니다. 이렇게 하면 형식 안전성, 컴파일 타임 검사 및 IntelliSense 템플릿 보기 내에서 편집기.

쇼핑 카트 컨트롤러에서 사용 하기 위해 두 개의 뷰 모델을 만들겠습니다: ShoppingCartViewModel는 사용자의 쇼핑 카트의 내용을 보유 하 고는 ShoppingCartRemoveViewModel에서 사용자 항목을 제거할 때 확인 정보를 표시 하는 데 사용 됩니다 자신의 카트에 합니다.

정보 구성 하는 프로젝트의 루트에서 새 Viewmodel 폴더를 만들어 보겠습니다. 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 추가 선택 합니다 / 새 폴더입니다.

![](mvc-music-store-part-8/_static/image1.jpg)

Viewmodel 폴더를 이름을 지정 합니다.

![](mvc-music-store-part-8/_static/image1.png)

다음으로 ShoppingCartViewModel 클래스 Viewmodel 폴더에 추가 합니다. 다음 두 가지 속성이: 카트 항목과 카트에서 모든 항목에 대 한 총 가격 유지 하기 위해 10 진수 값의 목록입니다.

[!code-csharp[Main](mvc-music-store-part-8/samples/sample6.cs)]

이제 다음 네 가지 속성을 가진 Viewmodel 폴더에는 ShoppingCartRemoveViewModel를 추가 합니다.

[!code-csharp[Main](mvc-music-store-part-8/samples/sample7.cs)]

## <a name="the-shopping-cart-controller"></a>쇼핑 카트 컨트롤러

쇼핑 카트 컨트롤러는 세 가지 주요 목적은:을 카트에 항목을 추가, 항목을 카트에서 제거 및 바구니에 항목을 표시 합니다. 세 개의 클래스에서는 사용 하면 방금 만든: ShoppingCartViewModel, ShoppingCartRemoveViewModel, 및 ShoppingCart 합니다. StoreController 및 StoreManagerController, MusicStoreEntities의 인스턴스를 포함 하는 필드를 추가 합니다.

빈 컨트롤러 템플릿을 사용 하 여 프로젝트에 새 쇼핑 카트 컨트롤러를 추가 합니다.

![](mvc-music-store-part-8/_static/image2.png)

다음은 전체 ShoppingCart 컨트롤러입니다. 인덱스 및 컨트롤러 추가 작업 친숙 하 게 표시 됩니다. 제거 및 CartSummary 컨트롤러 작업에는 다음 섹션에서 설명 하겠지만 두 가지 특별 한 경우 처리 합니다.

[!code-csharp[Main](mvc-music-store-part-8/samples/sample8.cs)]

## <a name="ajax-updates-with-jquery"></a>JQuery 사용 하 여 Ajax 업데이트

쇼핑 카트 인덱스 페이지는 ShoppingCartViewModel에 강력한 형식의 하 앞으로 동일한 메서드를 사용 하 여 목록 보기 템플릿을 사용 하 여 다음 만들겠습니다.

![](mvc-music-store-part-8/_static/image3.png)

그러나 카트에서 항목을 제거 하는 Html.ActionLink를 사용 하는 대신 사용 합니다 jQuery "를 연결 하" RemoveLink HTML 클래스를 포함 하는이 보기에 있는 모든 연결에 대 한 click 이벤트. 폼 게시, 대신이 click 이벤트 처리기 설정 됩니다. 바로 AJAX 콜백을에 우리의 RemoveFromCart 컨트롤러 동작 합니다. RemoveFromCart는 JSON으로 직렬화 된 결과 반환 jQuery 콜백이 다음 구문 분석 하 고 jQuery를 사용 하 여 페이지에 대 한 네 가지 빠른 업데이트를 수행 합니다.

- 1. 목록에서 삭제 된 앨범을 제거합니다.
- 2. 헤더에 카트 개수를 업데이트
- 3. 사용자에 게 업데이트 메시지를 표시합니다.
- 4. 카트 총 가격을 업데이트합니다.

제거 시나리오는 Ajax 콜백을 인덱스 뷰 내에서 처리 되는, 이후 추가 뷰 RemoveFromCart 동작에 대 한 필요 하지 않습니다. /ShoppingCart/Index 보기에 대 한 전체 코드는 다음과 같습니다.

[!code-cshtml[Main](mvc-music-store-part-8/samples/sample9.cshtml)]

Out이 르 테스트 하려면 당사의 쇼핑 카트에 항목을 추가할 수 해야 합니다. 업데이트 하는 중 우리의 **저장소 세부 정보** "카트에 추가" 단추를 포함 하는 보기입니다. 추가한 있는 앨범 추가 정보 중 일부 포함 시키려면 현재, 그 동안이 보기에서는 마지막 업데이트 이후: 장르, 아티스트, 가격 및 앨범 아트. 업데이트 된 코드 저장소 세부 정보 보기에는 다음과 같이 나타납니다.

[!code-cshtml[Main](mvc-music-store-part-8/samples/sample10.cshtml)]

이제 스토어를 통해 클릭 하 고 및 추가 / 제거 앨범을 당사의 쇼핑 카트에서 테스트할 수 했습니다. 응용 프로그램을 실행 하 고 저장소 인덱스를 찾습니다.

![](mvc-music-store-part-8/_static/image4.png)

다음으로 장르 앨범의 목록을 보려면 클릭 합니다.

![](mvc-music-store-part-8/_static/image5.png)

이제 앨범 제목 클릭 하면 "카트에 추가" 단추를 포함 하 여이 업데이트 된 앨범 자세히 보기를 표시 합니다.

![](mvc-music-store-part-8/_static/image6.png)

"카트에 추가" 단추를 클릭 하면 쇼핑 카트 요약 목록 함께 당사의 쇼핑 카트 인덱스 뷰가 표시 됩니다.

![](mvc-music-store-part-8/_static/image7.png)

쇼핑 카트에 로드 쇼핑 카트에 Ajax 업데이트 카트 링크에서 제거를 클릭할 수 있습니다.

![](mvc-music-store-part-8/_static/image8.png)

쇼핑 카트 등록 되지 않은 사용자가 자신의 카트에 항목을 추가할 수 있는 작업으로 구성 합니다. 다음 섹션에 등록 하 고 체크 아웃 프로세스를 완료 하도록 허용 합니다.


> [!div class="step-by-step"]
> [이전](mvc-music-store-part-7.md)
> [다음](mvc-music-store-part-9.md)
