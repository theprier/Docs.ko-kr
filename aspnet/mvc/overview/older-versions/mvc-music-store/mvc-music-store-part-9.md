---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-9
title: '9 단계: 등록 및 체크 아웃 | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 9 부에서는 등록 및 체크 아웃에 설명 합니다.
ms.author: aspnetcontent
ms.date: 04/21/2011
ms.assetid: d65c5c2b-a039-463f-ad29-25cf9fb7a1ba
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-9
msc.type: authoredcontent
ms.openlocfilehash: e521e30cb820d834d57c87538b869861a536657b
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37812875"
---
<a name="part-9-registration-and-checkout"></a>9 단계: 등록 및 체크 아웃
====================
[Jon Galloway](https://github.com/jongalloway)

> MVC Music Store 자습서 응용 프로그램을 소개 하 고 웹 개발을 위한 ASP.NET MVC 및 Visual Studio를 사용 하는 방법을 단계별로 설명 됩니다.  
>   
> MVC Music Store는 온라인 음악 앨범을 판매 하 고 기본 사이트 관리, 사용자 로그인 및 장바구니 기능을 구현 하는 간단한 샘플 저장소 구현입니다.  
>   
> 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 9 부에서는 등록 및 체크 아웃에 설명 합니다.


이 섹션에서는 만들 것을 CheckoutController 구매자의 주소 및 결제 정보를 수집 합니다. 에서는 사용자가이 컨트롤러는 권한 부여가 필요 하므로, 체크 인하기 전에 먼저 사이트를 사용 하 여 등록 해야 합니다.

사용자는 "체크 아웃" 단추를 클릭 하 여 시장 바구니에서 체크 아웃 프로세스에 이동 됩니다.

![](mvc-music-store-part-9/_static/image1.jpg)

사용자가 로그인 하지 않았습니다가 하 라는 메시지가 표시 됩니다.

![](mvc-music-store-part-9/_static/image1.png)

로그인에 성공 하면 사용자 후 주소 및 결제 보기에 표시 됩니다.

![](mvc-music-store-part-9/_static/image2.png)

폼 입력 있고 주문 제출, 되 면 주문 확인 화면이 표시 되며 합니다.

![](mvc-music-store-part-9/_static/image3.png)

존재 하지 않는 순서 또는 주문 수에 속하지 않는 보려고 하면 오류 보기가 표시 됩니다.

![](mvc-music-store-part-9/_static/image4.png)

## <a name="migrating-the-shopping-cart"></a>장바구니 마이그레이션

사용자가 체크 아웃 단추를 클릭할 때 익명으로 쇼핑 프로세스 중일 해야 등록 및 로그인 합니다. 사용자가 해당 쇼핑 카드 정보가 방문할: 등록 또는 로그인을 완료 될 때 사용자를 사용 하 여 쇼핑 카드 정보가 연결 해야 하므로 유지는 필요 합니다.

이 ShoppingCart 클래스에는 이미 사용자 이름으로 현재 장바구니에 있는 모든 항목을 연결 하는 하는 방법을 실제로 매우 간단 하 게 수행 합니다. 방금 등록 또는 로그인 사용자 완료 되 면이 메서드를 호출 해야 합니다.

엽니다는 **AccountController** 클래스에서는 멤버 자격 및 권한 부여 설정 된 경우 추가 합니다. 추가 된 다음 MigrateShoppingCart 메서드를 추가한 MvcMusicStore.Models를 참조 하는 문을 사용 하 여:

[!code-csharp[Main](mvc-music-store-part-9/samples/sample1.cs)]

다음으로 아래와 같이 사용자를 확인 한 후 MigrateShoppingCart를 호출 하는 로그온 후 작업을 수정 합니다.

[!code-csharp[Main](mvc-music-store-part-9/samples/sample2.cs)]

동일 하 게 변경 등록 후 사용자 계정을 성공적으로 만든 후에 즉시 작업을 확인 합니다.

[!code-csharp[Main](mvc-music-store-part-9/samples/sample3.cs)]

이것이-이제 성공적인 등록 또는 로그인 시 사용자 계정에는 익명 쇼핑 카트를 자동으로 전송 됩니다.

## <a name="creating-the-checkoutcontroller"></a>CheckoutController 만들기

Controllers 폴더에서 마우스 CheckoutController 빈 컨트롤러 템플릿을 사용 하 여 프로젝트에 새 컨트롤러를 추가 합니다.

![](mvc-music-store-part-9/_static/image5.png)

먼저, 사용자가 체크 아웃 하기 전에 등록 해야 컨트롤러 클래스 선언 위에 Authorize 특성을 추가 합니다.

[!code-csharp[Main](mvc-music-store-part-9/samples/sample4.cs)]

*참고:이 변경에서는 이전에 StoreManagerController 비슷합니다 있지만 Authorize 특성의 관리자 역할에서 사용자는 필요한 경우. 체크 아웃 컨트롤러에서에서는 요구는 사용자가 로그인 하지만 관리자가 되도록 요구 되지 않습니다.*

편의상이 자습서의 결제 정보를 사용 하 여 처리에서는 없습니다. 대신, 프로 모션 코드를 사용 하 여 확인 하는 작업을 할 수 있습니다. 이 프로 모션 코드 PromoCode를 명명 된 상수를 사용 하 여 저장 됩니다.

StoreController에서와 같이 storeDB 라는 MusicStoreEntities 클래스의 인스턴스를 보관할 필드를 선언 했습니다. 있도록 MusicStoreEntities 클래스의 사용, 추가 하 여 해야 MvcMusicStore.Models 네임 스페이스에 대 한 문입니다. 체크 아웃 컨트롤러의 맨 아래에 나타납니다.

[!code-csharp[Main](mvc-music-store-part-9/samples/sample5.cs)]

CheckoutController 다음 컨트롤러 작업을 해야 합니다.

**(GET 메서드) AddressAndPayment** 해당 정보를 입력할 수 있도록 폼에 표시 됩니다.

**(POST 메서드) AddressAndPayment** 입력의 유효성을 검사 하 고 주문을 처리 됩니다.

**전체** 사용자 체크 아웃 프로세스를 완료 한 후 표시 됩니다. 이 보기는 사용자의 주문 번호를 확인으로 포함 됩니다.

먼저 AddressAndPayment 위해 (하는 컨트롤러를 만들 때 생성 된) 인덱스 컨트롤러 작업의 이름을 합니다. 이 컨트롤러 작업 모델 정보 필요 하지 않도록 체크 아웃 폼만을 표시 됩니다.

[!code-csharp[Main](mvc-music-store-part-9/samples/sample6.cs)]

우리의 AddressAndPayment POST 메서드는 StoreManagerController에서 사용한 동일한 패턴을 따릅니다: 폼 제출을 수락 하 고 순서를 완료 하려고 하며 실패할 경우 폼을 다시 표시 됩니다.

폼 입력 유효성 검사는 주문에 대 한이 유효성 검사 요구 사항을 충족 한 후 직접 PromoCode 형식 값을 확인 됩니다. 주문 프로세스를 완료 하 고 작업 완료를 리디렉션할 하도록 ShoppingCart 개체에 알리는 가정 하 고 모든 항목이 올바르면는 순서를 사용 하 여 업데이트 된 정보를 저장 합니다.

[!code-csharp[Main](mvc-music-store-part-9/samples/sample7.cs)]

체크 아웃 프로세스를 성공적으로 완료 하면 사용자가 전체 컨트롤러 작업으로 리디렉션됩니다. 이 작업 순서는 실제로 속한 로그인 한 사용자 확인으로 주문 번호를 표시 하기 전에 유효성을 검사 하려면 간단한 검사를 수행 하 합니다.

[!code-csharp[Main](mvc-music-store-part-9/samples/sample8.cs)]

*참고: 오류 보기에 자동으로 만들어진 우리 /Views/Shared 폴더에 프로젝트를 시작할 때입니다.*

전체 CheckoutController 코드는 다음과 같습니다.

[!code-csharp[Main](mvc-music-store-part-9/samples/sample9.cs)]

## <a name="adding-the-addressandpayment-view"></a>AddressAndPayment 뷰 추가

이제 AddressAndPayment 보기를 만들어 보겠습니다. AddressAndPayment 컨트롤러 작업 중 하나를 마우스 오른쪽 단추로 클릭 하 고 아래와 같이 AddressAndPayment 주문으로 강력한 형식 이므로 편집 템플릿을 사용 하는 명명 된 뷰를 추가 합니다.

![](mvc-music-store-part-9/_static/image6.png)

이 보기 하 게 StoreManagerEdit 보기를 빌드하는 동안 살펴보았습니다 기술 중 두 개를 사용 합니다.

- Html.EditorForModel() 순서 모델에 대 한 양식 필드를 표시 하는 데 사용 하는
- 유효성 검사 규칙을 Order 클래스를 사용 하 여 유효성 검사 특성을 사용 하 여 활용 하 게

Html.EditorForModel(), 프로 모션 코드는 추가 텍스트 상자를 차례로 사용 하 여 폼 코드를 업데이트 하 여 시작 하겠습니다. AddressAndPayment 뷰에 대 한 전체 코드는 다음과 같습니다.

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample10.cshtml)]

## <a name="defining-validation-rules-for-the-order"></a>순서에 대 한 유효성 검사 규칙을 정의합니다.

보기를 설정 했으므로에서는 설정 유효성 검사 규칙 순서 모델에 대 한 앨범 모델에 대 한 이전에 수행한 것 처럼 합니다. Models 폴더에서 마우스 오른쪽 순서 라는 클래스를 추가 합니다. 유효성 검사 특성, 앨범에 대 한 이전에 사용 되는 것 외에 사용 합니다 정규식을 사용자의 전자 메일 주소의 유효성을 검사 하려면.

[!code-csharp[Main](mvc-music-store-part-9/samples/sample11.cs)]

누락 된 양식을 제출 하거나 잘못 된 정보는 이제 클라이언트 쪽 유효성 검사를 사용 하 여 오류 메시지를 표시 합니다.

![](mvc-music-store-part-9/_static/image7.png)

이제 대부분의 복잡 한 작업이 체크 아웃 프로세스를 수행한 방금 완료 하려면 몇 가지 홀수 and 종료 했습니다. 두 개의 간단한 뷰를 추가 해야 하 고 로그인 프로세스 중 카트 정보의 핸드 오프 주의 해야 합니다.

## <a name="adding-the-checkout-complete-view"></a>체크 아웃 전체 뷰를 추가합니다.

체크 아웃 전체 뷰는 id입니다. 순서를 표시 해야 하는 대로 꽤 간단 합니다. 전체 컨트롤러 작업 단추로 클릭 하 고 강력한 int 형식으로 형식화 된 완료 라는 뷰를 추가 합니다.

![](mvc-music-store-part-9/_static/image8.png)

이제 아래와 같이 주문 ID를 표시 하는 보기 코드를 업데이트 됩니다.

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample12.cshtml)]

## <a name="updating-the-error-view"></a>업데이트는 오류 보기

기본 템플릿은 될 수 있도록 다시 사용 되는 다른 곳에서 사이트에 공유 views 폴더에는 오류 보기를 포함 합니다. 이 오류 뷰는 매우 간단한 오류를 포함 하 고 업데이트 하 고 있으므로 사이트 레이아웃을 사용 하지 않습니다.

일반 오류 페이지 이므로, 콘텐츠를 매우 간단 합니다. 사용자가 해당 작업을 다시 시도 하려는 경우에 기록의 이전 페이지를 이동할 수는 메시지 및 링크 포함 됩니다.

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample13.cshtml)]


> [!div class="step-by-step"]
> [이전](mvc-music-store-part-8.md)
> [다음](mvc-music-store-part-10.md)
