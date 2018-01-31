---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-9
title: "9 단계: 등록 및 체크아웃 | Microsoft Docs"
author: jongalloway
description: "이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다. 등록 및 체크아웃 9에 설명합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/21/2011
ms.topic: article
ms.assetid: d65c5c2b-a039-463f-ad29-25cf9fb7a1ba
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-9
msc.type: authoredcontent
ms.openlocfilehash: 71f87043be064d24bdfb203380fb6cf651527e30
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
<a name="part-9-registration-and-checkout"></a>9 단계: 등록 및 체크 아웃
====================
으로 [Jon Galloway](https://github.com/jongalloway)

> MVC Music Store는 소개 하 고 웹 개발에 대 한 ASP.NET MVC와 Visual Studio를 사용 하는 방법을 단계별로 설명 하는 자습서 응용 프로그램.  
>   
> MVC Music Store는 온라인 음악 앨범 판매 및 기본 사이트 관리, 사용자 로그인 및 장바구니 기능을 구현 하는 간단한 샘플 저장소 구현입니다.  
>   
> 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다. 등록 및 체크아웃 9에 설명합니다.


이 섹션에서는 고객의 주소 및 지불 정보를 수집 하는 CheckoutController 만드는데 합니다. 이 컨트롤러는 승인을 받아야 있도록 체크 아웃 하기 전에 사이트에 등록 하도록 해야 합니다.

사용자는 "체크 아웃" 단추를 클릭 하 여 쇼핑 카트의에서 결제 과정으로 이동 됩니다.

![](mvc-music-store-part-9/_static/image1.jpg)

사용자가 로그인 하지 있습니다 하 라는 메시지가 표시 됩니다.

![](mvc-music-store-part-9/_static/image1.png)

로그인을 하면 사용자 주소 및 지불 보기를 표시 한 다음 됩니다.

![](mvc-music-store-part-9/_static/image2.png)

폼에 채워진 있고 주문을 보낸를 일단 주문 확인 화면을 표시 될 있습니다.

![](mvc-music-store-part-9/_static/image3.png)

존재 하지 않는 순서나 소유 되는 순서를 보려고 하면 오류 보기가 표시 됩니다.

![](mvc-music-store-part-9/_static/image4.png)

## <a name="migrating-the-shopping-cart"></a>쇼핑 카트 마이그레이션

쇼핑 프로세스 상태인 동안 익명 사용자가 체크 아웃 단추를 클릭할 때 요구를 등록 하 고 로그인 합니다. 사용자가 기대 하의 쇼핑 카드 정보가 환자가 내 원 등록 또는 로그인을 완료 하는 경우 쇼핑 카드 정보가 사용자와 연결 하는 하므로 간에 유지 됩니다.

이 ShoppingCart 클래스에는 이미 사용자 이름으로 현재 장바구니에 있는 모든 항목을 연결 합니다 하는 방법을 실제로 매우 간단를입니다. 방금 등록 또는 로그인 사용자 완료 되 면이 메서드를 호출 해야 합니다.

열기는 **AccountController** 멤버 자격 및 권한 부여 설정 된 म 때 추가한 클래스입니다. 추가 된 다음 MigrateShoppingCart 메서드를 추가 다음 MvcMusicStore.Models를 참조 하는 문을 사용 하 여:

[!code-csharp[Main](mvc-music-store-part-9/samples/sample1.cs)]

다음으로 아래와 같이 사용자를 확인 한 후 MigrateShoppingCart를 호출 하려면 로그온 후 작업을 수정 합니다.

[!code-csharp[Main](mvc-music-store-part-9/samples/sample2.cs)]

동일 하 게 변경 레지스터에 사용자 계정이 성공적으로 생성 한 후에 즉시 작업을 게시 합니다.

[!code-csharp[Main](mvc-music-store-part-9/samples/sample3.cs)]

설정 작업이 완료-이제 성공적으로 등록 또는 로그인 시 사용자 계정에는 익명 쇼핑 카트를 자동으로 전송 됩니다.

## <a name="creating-the-checkoutcontroller"></a>CheckoutController 만들기

Controllers 폴더 고 CheckoutController 빈 컨트롤러 템플릿을 사용 하 여 프로젝트에 새 컨트롤러를 추가 합니다.

![](mvc-music-store-part-9/_static/image5.png)

먼저, 사용자가 체크 아웃 하기 전에 등록 해야 컨트롤러 클래스 선언 위에 Authorize 특성을 추가 합니다.

[!code-csharp[Main](mvc-music-store-part-9/samples/sample4.cs)]

*참고:이 변경에서는 이전에 StoreManagerController 비슷합니다 있지만 권한 부여 속성 관리자 역할에서 사용자는 필요한 경우. 체크 아웃 컨트롤러에서 우리는 필요한 사용자 로그인 하지만 관리자 수 하는 요구 되지 않습니다.*

간단한 설명을 위해가이 자습서에서는 지불 정보로 처리 했하지 않습니다. 대신, 사용자가을 체크 아웃 프로 모션 코드를 사용 하 여 수 있습니다. PromoCode 명명 된 상수를 사용 하 여이 프로 모션 코드를 저장 됩니다.

StoreController 에서처럼 storeDB 라는 MusicStoreEntities 클래스의 인스턴스를 보유 하는 필드를 선언 합니다. 있도록 MusicStoreEntities 클래스의 사용, 사용 하는 추가 해야 합니다 MvcMusicStore.Models 네임 스페이스에 대 한 문입니다. 체크 아웃 controller 맨 아래에 나타납니다.

[!code-csharp[Main](mvc-music-store-part-9/samples/sample5.cs)]

CheckoutController 다음 컨트롤러 작업에 적용 됩니다.

**AddressAndPayment (GET 메서드)** 사용자 정보를 입력할 수 있도록 폼에 표시 됩니다.

**AddressAndPayment (POST 메서드)** 입력의 유효성을 검사 하 고 주문을 처리 합니다.

**전체** 사용자 계산 절차를 완료 한 후 표시 됩니다. 이 보기는 사용자의 주문 번호 확인으로 포함 됩니다.

첫째, AddressAndPayment 위해 (있음 컨트롤러를 만들 때 생성 된) 인덱스 컨트롤러 동작의 이름을 합니다. 이 컨트롤러 동작 때문 모든 모델 정보가 필요 하지 않습니다 체크 아웃 폼이 방금 표시 됩니다.

[!code-csharp[Main](mvc-music-store-part-9/samples/sample6.cs)]

우리의 AddressAndPayment POST 메서드는 StoreManagerController에서 사용한 동일한 패턴을 따를 것: 하려고 시도 하는 순서를 완료 하 고 양식 전송에 동의 하 고 양식을 실패할 경우 다시 표시 됩니다.

유효성을 검사 하 여 양식 입력이 유효성 검사 요구 사항을 충족 하는 주문에 대 한 후 직접 PromoCode 폼 값을 확인 됩니다. 주문 프로세스를 완료 하 고 완료 된 작업으로 리디렉션 ShoppingCart 개체를 알려으로 가정 하 고 모든 올바른 순서와 업데이트 된 정보 저장 됩니다.

[!code-csharp[Main](mvc-music-store-part-9/samples/sample7.cs)]

결제 과정을 성공적으로 완료 되 면 사용자가 전체 컨트롤러 작업으로 이동 합니다. 이 작업을 확인 하는 주문 번호를 표시 하기 전에 순서는 로그인 한 사용자에 실제로 속하지 유효성을 검사 하는 간단한 검사를 수행 합니다.

[!code-csharp[Main](mvc-music-store-part-9/samples/sample8.cs)]

*참고: 오류 보기에 자동으로 만들어진 우리 /Views/Shared 폴더에 프로젝트를 시작할 때입니다.*

전체 CheckoutController 코드는 다음과 같습니다.

[!code-csharp[Main](mvc-music-store-part-9/samples/sample9.cs)]

## <a name="adding-the-addressandpayment-view"></a>AddressAndPayment 뷰 추가

이제 AddressAndPayment 보기를 만들어 보겠습니다. 중 하나를 마우스 오른쪽 단추로 클릭는 AddressAndPayment 컨트롤러 작업 하 고 아래와 같이 AddressAndPayment 순서로 강력한 형식이 며 편집 템플릿을 사용 하 여 명명 된 뷰를 추가 합니다.

![](mvc-music-store-part-9/_static/image6.png)

이 보기 하면 두 StoreManagerEdit 뷰를 작성 하는 동안 살펴보았습니다 기술을 사용 하 여:

- Html.EditorForModel() 순서 모델에 대 한 양식 필드를 표시 하려면 사용 합니다.
- 유효성 검사 규칙을 Order 클래스를 사용 하 여 유효성 검사 특성을 가진 활용 됩니다.

이 프로 모션 코드에 대 한 추가 텍스트 상자를 차례로 Html.EditorForModel() 사용 하도록 양식 코드를 업데이트 하 여 시작 합니다. AddressAndPayment 보기에 대 한 전체 코드는 다음과 같습니다.

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample10.cshtml)]

## <a name="defining-validation-rules-for-the-order"></a>순서에 대 한 유효성 검사 규칙을 정의합니다.

이 보기를 설정 했으므로 됩니다를 설정 유효성 검사 규칙 예제의 순서 모델에 대 한 앨범 모델에 대 한 이전에 수행한 것 처럼 합니다. 모델 폴더 단추로 클릭 하 고 Order 라는 클래스를 추가 합니다. 앨범에 대 한 이전에 사용 유효성 검사 특성 외에 사용 합니다 정규식 사용자의 전자 메일 주소 유효성을 검사 하 합니다.

[!code-csharp[Main](mvc-music-store-part-9/samples/sample11.cs)]

하려고 누락 된 양식을 제출 하거나 잘못 된 정보가 클라이언트 쪽 유효성 검사를 사용 하 여 오류 메시지가 표시 됩니다.

![](mvc-music-store-part-9/_static/image7.png)

대부분의 결제 과정;에 대 한 복잡 한 작업을 수행한 자, 방금 완료 하는 데 몇 가지 교차 and 종료 해야 합니다. 두 개의 간단한 뷰를 추가 해야 하 고 로그인 프로세스 동안 장바구니 정보 전달을 처리 해야 합니다.

## <a name="adding-the-checkout-complete-view"></a>체크 아웃 전체 뷰를 추가합니다.

Id입니다. 순서를 표시 하는 대로 체크 아웃 전체 뷰는 상당히 간단 전체 컨트롤러 동작 단추로 클릭 하 고 강력한 int 형식으로 형식화 된 Complete 라는 이름의 뷰 추가

![](mvc-music-store-part-9/_static/image8.png)

이제 다음과 같이 주문 ID를 표시 하는 보기 코드를 업데이트 됩니다.

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample12.cshtml)]

## <a name="updating-the-error-view"></a>오류를 발생 뷰 업데이트

기본 템플릿을 것 될 수 있도록 다시 사용할 다른 위치에서 사이트에 공유 views 폴더에는 오류 보기를 포함 합니다. 이 오류 뷰는 매우 간단한 오류를 포함 하 고 업데이트 하는 것 사이트 레이아웃을 사용 하지 않습니다.

일반 오류 페이지 이므로, 콘텐츠는 매우 간단 합니다. 사용자가 자신의 작업을 다시 시도 하려는 경우 기록의 이전 페이지로 이동 하는 메시지와 링크를 포함 합니다.

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample13.cshtml)]


>[!div class="step-by-step"]
[이전](mvc-music-store-part-8.md)
[다음](mvc-music-store-part-10.md)
