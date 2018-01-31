---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/shopping-cart
title: "쇼핑 카트 | Microsoft Docs"
author: Erikre
description: "이 자습서 시리즈 것에 대 한 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 구축 하는 기초 알려 드리겠습니다 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/08/2014
ms.topic: article
ms.assetid: 6898c601-6c31-432f-8388-e6843f8a17cb
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/shopping-cart
msc.type: authoredcontent
ms.openlocfilehash: 9fe6f28685d6a423b03f9c7abe753283b89344e1
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="shopping-cart"></a>쇼핑 카트
====================
으로 [Erik Reitan](https://github.com/Erikre)

[Wingtip Toys 샘플 프로젝트 (C#)를 다운로드](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자책 (PDF)를 다운로드 합니다.](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 이 자습서 시리즈 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 웹에 대 한 ASP.NET Web Forms 응용 프로그램을 구축 하는 기초 알려 드리겠습니다. Visual Studio 2013 [C# 소스 코드를 사용 하 여 프로젝트](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 이 자습서 시리즈를 함께 사용할 수 있습니다.


이 자습서에서는 쇼핑 카트 Wingtip Toys 샘플 ASP.NET Web Forms 응용 프로그램에 추가 하는 데 필요한 비즈니스 논리를 설명 합니다. 이 자습서에서는 이전 자습서 "디스플레이 데이터 항목 및" 세부 정보를 바탕으로 하며 Wingtip 장난감 저장소 자습서 시리즈의 일부입니다. 이 자습서를 완료 하면 샘플 응용 프로그램의 사용자를 추가, 제거 및 쇼핑 카트에 제품을 수정할 수 됩니다.

## <a name="what-youll-learn"></a>학습 내용:

1. 웹 응용 프로그램에 대 한 쇼핑 카트를 만드는 방법.
2. 사용자가 장바구니에 항목을 추가할 수 있도록 하는 방법.
3. 추가 하는 방법 한 [GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview(v=vs.110).aspx#introduction) 컨트롤 쇼핑 카트 세부 정보를 표시 합니다.
4. 계산 및 주문 합계를 표시 하는 방법.
5. 제거 하 고 장바구니에 항목을 업데이트 하는 방법.
6. 쇼핑 카트 카운터를 포함 하는 방법입니다.

## <a name="code-features-in-this-tutorial"></a>이 자습서의 코드 기능:

1. Entity Framework Code First
2. 데이터 주석
3. 강력한 형식의 데이터 컨트롤
4. 모델 바인딩

## <a name="creating-a-shopping-cart"></a>쇼핑 카트 만들기

이 자습서 시리즈의 앞부분에 나오는 페이지와 데이터베이스에서 제품 데이터를 보려면 코드를 추가 합니다. 이 자습서에서는 제품을 관리 하는 쇼핑 카트 만듭니다 사용자가 구매에 관심 있는 합니다. 사용자를 찾아보고 등록 되거나에 기록 되지 않을 경우에 장바구니에 항목을 추가할 수 있습니다. 쇼핑 카트 액세스를 관리 하려면 지정할 사용자는 고유한 `ID` 처음으로 카트에 전역 고유 식별자 (GUID)를 사용 하 여 사용자의 쇼핑가 액세스 합니다. 이 저장할 `ID` ASP.NET 세션 상태를 사용 합니다.

> [!NOTE] 
> 
> ASP.NET 세션 상태는 사용자가 사이트에 만료 되는 사용자 관련 정보를 저장 하는 편리한 장소입니다. 세션 상태를 잘못 사용 하면 대규모 사이트 성능에 미치는 영향을 있을 수 있지만, 예시 목적을 위한 잘 작동 하는 상태를 세션의 사용을 연한 합니다. Wingtip Toys 샘플 프로젝트에 세션 상태 저장된 in-process에 사이트를 호스팅하는 웹 서버에는 여기서 외부 공급자 없이 세션 상태를 사용 하는 방법을 보여 줍니다. 응용 프로그램의 여러 인스턴스를 제공 하는 대규모 사이트에 대 한 서로 다른 서버에 응용 프로그램의 여러 인스턴스를 실행 하는 사이트에 대 한 명확히를 사용 하 여 **Windows Azure 캐시 서비스**합니다. 이 캐시 서비스는 외부 웹 사이트에 in-process에 세션 상태를 사용 하 여 문제를 해결 하는 분산된 캐싱 서비스를 제공 합니다. 자세한 내용은 참조 하십시오 [ASP.NET 세션 상태 Windows Azure 웹 사이트를 사용 하는 방법을](https://docs.microsoft.com/azure/redis-cache/cache-aspnet-session-state-provider)합니다.


### <a name="add-cartitem-as-a-model-class"></a>모델 클래스로 CartItem 추가

이 자습서 시리즈의 앞부분에 나오는 만들어 범주 및 제품 데이터에 대 한 스키마를 정의 고 `Category` 및 `Product` 에 있는 클래스는 *모델* 폴더입니다. 이제 장바구니에 대 한 스키마를 정의 하는 새 클래스를 추가 합니다. 이 자습서의 뒷부분에 나오는 추가한 데이터에 대 한 액세스를 처리 하는 클래스는 `CartItem` 테이블입니다. 이 클래스는 추가, 제거 및 시장 바구니에 항목을 업데이트 하는 비즈니스 논리를 제공 합니다.

1. 마우스 오른쪽 단추로 클릭는 *모델* 폴더와 선택 **추가**  - &gt; **새 항목**합니다. 

    ![쇼핑 카트-새 항목](shopping-cart/_static/image1.png)
2. **새 항목 추가** 대화 상자가 표시됩니다. 선택 **코드**를 선택한 후 **클래스**합니다. 

    ![쇼핑 카트-새 항목 추가 대화 상자](shopping-cart/_static/image2.png)
3. 이 새 클래스 이름을 *CartItem.cs*합니다.
4. **추가**를 클릭합니다.  
 새 클래스 파일은 편집기에 표시 됩니다.
5. 기본 코드를 다음 코드로 바꿉니다.   

    [!code-csharp[Main](shopping-cart/samples/sample1.cs)]

`CartItem` 클래스는 사용자는 장바구니에 추가 하는 각 제품을 정의 하는 스키마를 포함 합니다. 이 클래스는이 자습서 시리즈의 앞부분에서 만든 다른 스키마 클래스와 유사 합니다. 규칙에 따라 Entity Framework Code First 예상 하는 기본 키에는 `CartItem` 테이블 중 하나가 됩니다 `CartItemId` 또는 `ID`합니다. 코드 데이터 주석을 사용 하 여 기본 동작을 재정의 하는 반면 `[Key]` 특성입니다. `Key` ItemId 속성의 특성을 지정 하는 `ItemID` 속성은 기본 키입니다.

`CartId` 속성 지정는 `ID` 구매 항목과 연결 된 사용자의 합니다. 이 사용자를 만드는 코드를 추가 `ID` 쇼핑 카트 액세스할 때. 이 `ID` 도 ASP.NET 세션 변수로 저장 됩니다.

### <a name="update-the-product-context"></a>제품 컨텍스트를 업데이트 합니다.

추가할 뿐 아니라는 `CartItem` 클래스를 엔터티 클래스를 관리 하 고 데이터베이스에 대 한 데이터 액세스를 제공 하는 데이터베이스 컨텍스트 클래스를 업데이트 해야 합니다. 이 위해 추가한 새로 만든 `CartItem` 모델에 클래스는 `ProductContext` 클래스입니다.

1. **솔루션 탐색기**찾기 및 열기는 *ProductContext.cs* 파일에 *모델* 폴더입니다.
2. 강조 표시 된 코드를 추가 하는 *ProductContext.cs* 다음과 같이 파일:  

    [!code-csharp[Main](shopping-cart/samples/sample2.cs?highlight=14)]

이 자습서 시리즈의 코드에서 설명한 것 처럼는 *ProductContext.cs* 파일을 사용 하면는 `System.Data.Entity` 네임 스페이스는 Entity Framework의 모든 핵심 기능에 액세스할 수 있도록 합니다. 이 기능은 쿼리, 삽입, 업데이트 및 강력한 형식의 개체를 사용 하 여 데이터를 삭제 하는 기능을 포함 합니다. `ProductContext` 클래스 액세스 새로 추가 된 추가 `CartItem` 모델 클래스입니다.

### <a name="managing-the-shopping-cart-business-logic"></a>쇼핑 카트 비즈니스 논리를 관리합니다.

다음을 만듭니다는 `ShoppingCart` 클래스를 새로운 *논리* 폴더입니다. `ShoppingCart` 클래스 처리에 대 한 데이터 액세스는 `CartItem` 테이블입니다. 클래스에는 비즈니스 논리를 추가, 제거 및 시장 바구니에 항목을 업데이트도 포함 됩니다.

쇼핑 카트 논리를 추가한 다음 작업을 관리 하는 기능을 포함 됩니다.

1. 쇼핑 카트에 항목 추가
2. 쇼핑 카트에서 항목 제거
3. 쇼핑 카트 ID 가져오기
4. 장바구니에서 항목을 검색합니다.
5. 모든 쇼핑 카트에 항목의 크기 합계
6. 쇼핑 카트 데이터 업데이트

쇼핑 카트 페이지 (*ShoppingCart.aspx*) 쇼핑 카트 데이터에 액세스 하는 쇼핑 카트 클래스를 함께 사용 됩니다. 쇼핑 카트 페이지에서는 사용자가 장바구니에 추가 하는 모든 항목에 표시 됩니다. 페이지 외에 쇼핑 카트 페이지 및 클래스를 만듭니다 (*AddToCart.aspx*) 쇼핑 카트에 제품을 추가 합니다. 또한 코드를 추가 합니다는 *ProductList.aspx* 페이지 및 *ProductDetails.aspx* 페이지에 대 한 링크를 제공 하는 *AddToCart.aspx* 사용자를 추가할 수 있도록 페이지 쇼핑 카트에 제품입니다.

다음 다이어그램에서는 사용자가 제품을 장바구니에 추가 될 때 발생 하는 기본 프로세스를 보여 줍니다.

![쇼핑 카트-쇼핑 카트에 추가](shopping-cart/_static/image3.png)

사용자가 클릭할 때는 **Add To Cart** 하나에 대 한 링크는 *ProductList.aspx* 페이지 또는 *ProductDetails.aspx* 페이지에서 응용 프로그램은 로이동되*AddToCart.aspx* 페이지 다음에 자동으로 *ShoppingCart.aspx* 페이지. *AddToCart.aspx* 페이지 ShoppingCart 클래스에서 메서드를 호출 하 여 쇼핑 카트에 제품 선택에 추가 합니다. *ShoppingCart.aspx* 장바구니에 추가 된 제품 페이지에 표시 됩니다.

#### <a name="creating-the-shopping-cart-class"></a>쇼핑 카트 클래스 만들기

`ShoppingCart` 클래스가 모델 (모델 폴더), 페이지 (루트 폴더) 및 논리 (논리 폴더) 명확히 구분할 수 있도록 응용 프로그램에서 별도 폴더에 추가 됩니다.

1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 **WingtipToys**프로젝트를 마우스 선택 **추가**-&gt;**새 폴더**. 새 폴더 이름을 *논리*합니다.
2. 마우스 오른쪽 단추로 클릭는 *논리* 폴더 및 다음 선택 **추가**  - &gt; **새 항목**합니다.
3. 라는 새 클래스 파일 추가 *ShoppingCartActions.cs*합니다.
4. 기본 코드를 다음 코드로 바꿉니다.   

    [!code-csharp[Main](shopping-cart/samples/sample3.cs)]

`AddToCart` 메서드를 사용 하면 개별 제품 기반 제품으로 시장 바구니에 포함 되도록 `ID`합니다. 제품 카트를 더하거나 카트 해당 제품에 대 한 항목이 이미 있으면 수량이 증가 됩니다.

`GetCartId` 메서드 반환 카트 `ID` 사용자에 대 한 합니다. 그러면 `ID` 는 사용자가 장바구니의 항목을 추적 하는 데 사용 됩니다. 사용자는 기존 카트 없으면 `ID`, 새 카트 `ID` 만들고 합니다. 그러면 등록 된 사용자 사용자가 로그인 하는 경우 `ID` 자신의 사용자 이름으로 설정 됩니다. 그러나 사용자 바구니에 서명 되지 않은 경우 `ID` 고유 값 (GUID)으로 설정 됩니다. GUID 하면 하나의 카트 해당 세션에 따라 각 사용자에 대해 생성 됩니다.

`GetCartItems` 메서드 쇼핑 카트에 항목에 대 한 사용자의 목록을 반환 합니다. 이 자습서의 뒷부분에 나오는 나타납니다 모델 바인딩을 사용 하 여 쇼핑 카트 카트에 항목으로 표시를 사용 하 여 `GetCartItems` 메서드.

### <a name="creating-the-add-to-cart-functionality"></a>카트에 추가 기능 만들기

라는 처리 페이지 만들면는 앞서 언급 했 듯이 *AddToCart.aspx* 신제품 사용자의 쇼핑 카트에 추가 하는 데 사용 될 됩니다. 이 페이지를 호출 합니다는 `AddToCart` 에서 메서드는 `ShoppingCart` 방금 만든 클래스입니다. *AddToCart.aspx* 페이지는 것을 예상 하는 제품 `ID` 전달 됩니다. 이 제품은 `ID` 호출할 때 사용할 수는 `AddToCart` 에서 메서드는 `ShoppingCart` 클래스입니다.

> [!NOTE] 
> 
> 코드 숨김 수정할 것입니다 (*AddToCart.aspx.cs*)이이 페이지에서는 페이지 UI에 대 한 (*AddToCart.aspx*).


#### <a name="to-create-the-add-to-cart-functionality"></a>만들려면 장바구니에 추가 기능:

1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 **WingtipToys**프로젝트를 클릭 하 여 **추가**  - &gt; **새 항목**합니다.  
 **새 항목 추가** 대화 상자가 표시됩니다.
2. 표준 새 페이지 (Web Form) 라는 응용 프로그램에 추가 *AddToCart.aspx*합니다. 

    ![쇼핑 카트-Web Form을 추가 합니다.](shopping-cart/_static/image4.png)
3. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 *AddToCart.aspx* 페이지 한 다음 클릭 **코드 보기**합니다. *AddToCart.aspx.cs* 코드 숨김 파일이 편집기에서 열립니다.
4. 기존 코드는 *AddToCart.aspx.cs* 코드 숨김 다음:   

    [!code-csharp[Main](shopping-cart/samples/sample4.cs)]

경우는 *AddToCart.aspx* 페이지가 로드 되는 제품 `ID` 쿼리 문자열에서 검색 됩니다. 쇼핑 카트 클래스의 인스턴스 만들고 호출 하는 데 다음으로 `AddToCart` 이 자습서의 앞부분에서 추가한 메서드. `AddToCart` 에 포함 된 메서드는 *ShoppingCartActions.cs* 파일, 선택한 제품 쇼핑 카트에 추가 나 선택된 된 제품의 제품 수량을 증가 하는 논리가 포함 됩니다. 제품을 장바구니에 추가 되지 않았거나, 제품에 추가 됩니다는 `CartItem` 데이터베이스의 테이블입니다. 제품 수량에 증가 제품 쇼핑 카트에 이미 추가 하는 경우 동일한 제품의 추가 항목을 추가 하는 사용자는 `CartItem` 테이블입니다. 마지막으로, 페이지로 리디렉션합니다는 *ShoppingCart.aspx* 페이지를 사용자에 게 바구니에 항목의 업데이트 된 목록을 표시 하는 다음 단계에 추가 합니다.

에서 설명한 대로 사용자 `ID` 특정 사용자와 관련 된 제품을 확인 하는 데 사용 됩니다. 이 `ID` 의 행에 추가 되는 `CartItem` 될 때마다 쇼핑 카트에 제품을 추가 하는 사용자 테이블.

### <a name="creating-the-shopping-cart-ui"></a>쇼핑 카트 UI 만들기

*ShoppingCart.aspx* 페이지는 사용자가 장바구니에 추가 하는 제품에 표시 됩니다. 또한 추가, 제거 및 시장 바구니에 항목을 업데이트 하는 기능을 제공 합니다.

1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 **WingtipToys**, 클릭 **추가**  - &gt; **새 항목**합니다.  
 **새 항목 추가** 대화 상자가 표시됩니다.
2. 마스터 페이지를 선택 하 여 포함 된 새 페이지 (Web Form) 추가 **웹 폼 마스터 페이지를 사용 하 여**합니다. 새 페이지 이름을 *ShoppingCart.aspx*합니다.
3. 선택 **Site.Master** 마스터 페이지를 새로 만든 연결할 *.aspx* 페이지.
4. 에 *ShoppingCart.aspx* 페이지에서 기존 태그를 다음 태그로 바꿉니다.   

    [!code-aspx[Main](shopping-cart/samples/sample5.aspx)]

*ShoppingCart.aspx* 페이지에 포함 되어는 **GridView** 라는 컨트롤 `CartList`합니다. 이 컨트롤을 데이터베이스에서의 쇼핑 카트 데이터를 바인딩할 모델 바인딩을 사용 하 여 **GridView** 제어 합니다. 설정 하는 경우는 `ItemType` 속성의는 **GridView** 제어, 데이터 바인딩 식을 `Item` 에서 사용할 수 컨트롤 및 컨트롤의 태그 강력한 형식이 지정 됩니다. 이 자습서 시리즈의 앞부분에 나오는 설명 했 듯이의 세부 정보를 선택할 수 있습니다는 `Item` IntelliSense를 사용 하 여 개체입니다. 모델 바인딩을 사용 하 여 데이터를 선택 하도록 데이터 컨트롤을 구성 하려면 설정는 `SelectMethod` 컨트롤의 속성입니다. 설정한 위의 태그에는 `SelectMethod` 의 목록을 반환 하는 GetShoppingCartItems 메서드를 사용 하 여 `CartItem` 개체입니다. **GridView** 데이터 컨트롤 페이지 수명 주기의 적절 한 시간에 메서드를 호출 하 고 반환된 된 데이터에 자동 바인딩됩니다. `GetShoppingCartItems` 메서드 추가 해야 합니다.

#### <a name="retrieving-the-shopping-cart-items"></a>쇼핑 카트에 항목을 가져오는 중

코드를 추가 하는 다음으로 *ShoppingCart.aspx.cs* 코드 숨김 검색 하는 쇼핑 카트 UI를 채웁니다.

1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 *ShoppingCart.aspx* 페이지 한 다음 클릭 **코드 보기**합니다. *ShoppingCart.aspx.cs* 코드 숨김 파일이 편집기에서 열립니다.
2. 기존 코드를 다음으로 바꿉니다.  

    [!code-csharp[Main](shopping-cart/samples/sample6.cs)]

위에서 설명 했 듯이 `GridView` 데이터 컨트롤을 호출은 `GetShoppingCartItems` 페이지의 적절 한 시간 주기 메서드와 반환된 된 데이터에 자동 바인딩됩니다. `GetShoppingCartItems` 메서드의 인스턴스를 만듭니다는 `ShoppingCartActions` 개체입니다. 그런 다음 코드를 사용 하 여 해당 인스턴스를 호출 하 여 바구니에 항목을 반환 된 `GetCartItems` 메서드.

### <a name="adding-products-to-the-shopping-cart"></a>쇼핑 카트에 제품 추가

경우 중 하나는 *ProductList.aspx* 또는 *ProductDetails.aspx* 페이지가 표시 되 면 사용자는 링크를 사용 하 고 쇼핑 카트에 제품을 추가할 수 있습니다. 응용 프로그램에서 라는 처리 페이지로 탐색 링크를 클릭 *AddToCart.aspx*합니다. *AddToCart.aspx* 페이지 호출 됩니다는 `AddToCart` 에서 메서드는 `ShoppingCart` 이 자습서의 앞부분에 나오는 추가 클래스를 합니다.

이제를 추가 합니다는 **카트에 추가** 둘 다에 대 한 링크는 *ProductList.aspx* 페이지 및 *ProductDetails.aspx* 페이지. 이 링크는 제품에 포함 됩니다 `ID` 하는 데이터베이스에서 검색 됩니다.

1. **솔루션 탐색기**, 찾기 및 명명 된 페이지를 열고 *ProductList.aspx*합니다.
2. 태그에 노란색으로 강조 표시에 추가 *ProductList.aspx* 페이지를 전체 페이지에는 다음과 같이 표시 됩니다.  

    [!code-aspx[Main](shopping-cart/samples/sample7.aspx?highlight=50-54)]

### <a name="testing-the-shopping-cart"></a>쇼핑 카트를 테스트합니다.

쇼핑 카트에 제품 추가 하는 방법을 확인 하려면 응용 프로그램을 실행 합니다.

1. **F5** 키를 눌러 응용 프로그램을 실행합니다.  
 프로젝트 데이터베이스를 다시 만들어, 한 후 브라우저 열리며 표시는 *Default.aspx* 페이지.
2. 선택 **자동차** 범주 탐색 메뉴에서 합니다.  
 *ProductList.aspx* "Cars" 범주에 포함 된 제품만 표시 페이지가 표시 됩니다. 

    ![쇼핑 카트-자동차](shopping-cart/_static/image5.png)
3. 클릭는 **카트에 추가** 첫 번째 제품 옆에 있는 링크 (변환할 자동차)를 나열 합니다.   
 *ShoppingCart.aspx* 쇼핑 카트에 선택 영역을 보여 주는 페이지가 표시 됩니다. 

    ![쇼핑 카트-카트](shopping-cart/_static/image6.png)
4. 추가 제품을 선택 하 여 볼 **평면** 범주 탐색 메뉴에서 합니다.
5. 클릭는 **카트에 추가** 나열 된 첫 번째 제품 옆에 있는 링크입니다.  
 *ShoppingCart.aspx* 페이지가 추가 항목과 함께 표시 됩니다.
6. 브라우저를 닫습니다.

### <a name="calculating-and-displaying-the-order-total"></a>계산 및 주문 합계를 표시 합니다.

쇼핑 카트에 제품을 추가 하는 것 외에도 추가 됩니다 한 `GetTotal` 메서드를는 `ShoppingCart` 클래스 및 총 주문 금액이 쇼핑 카트 페이지에 표시 합니다.

1. **솔루션 탐색기**열고는 *ShoppingCartActions.cs* 파일에 *논리* 폴더입니다.
2. 다음 추가 `GetTotal` 노란색으로 강조 표시 하는 메서드는 `ShoppingCart` 클래스는 다음과 같이 표시 되도록 클래스:   

    [!code-csharp[Main](shopping-cart/samples/sample8.cs?highlight=85-97)]

첫째, 고 `GetTotal` 메서드는 사용자에 대 한 쇼핑 카트의 ID를 가져옵니다. 다음 메서드는 장바구니에 나열 된 각 제품에 대 한 제품 수량 제품 가격을 곱하여 총 카트를 가져옵니다.

> [!NOTE] 
> 
> 위의 코드는 nullable 형식을 사용 하 여 "`int?`"입니다. Nullable 형식은 모든 값의 내부 형식 및 null 값으로 나타낼 수 있습니다. 자세한 내용은 참조 하십시오 [Nullable 형식을 사용 하 여](https://msdn.microsoft.com/library/2cf62fcy(v=vs.110).aspx)합니다.


### <a name="modify-the-shopping-cart-display"></a>쇼핑 카트 표시 수정

다음에 대 한 코드를 수정 합니다는 *ShoppingCart.aspx* 호출 하는 페이지는 `GetTotal` 메서드와에 있는 전체 표시는 *ShoppingCart.aspx* 페이지가 페이지가 로드 될 때입니다.

1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 *ShoppingCart.aspx* 페이지로 돌아간 후 선택 **코드 보기**합니다.
2. 에 *ShoppingCart.aspx.cs* 파일, 업데이트는 `Page_Load` 노란색으로 강조 표시 한 다음 코드를 추가 하 여 처리기:   

    [!code-csharp[Main](shopping-cart/samples/sample9.cs?highlight=16-31)]

경우는 *ShoppingCart.aspx* 쇼핑 카트 개체를 로드 하 고 호출 하 여 쇼핑 카트 합계를 검색 한 다음, 페이지 로드는 `GetTotal` 의 메서드는 `ShoppingCart` 클래스입니다. 쇼핑 카트 비어 있으면 메시지 그 결과 표시 됩니다.

### <a name="testing-the-shopping-cart-total"></a>쇼핑 카트 총 테스트

추가 하는 방법이 없습니다만 제품 쇼핑 카트를 볼 수 있는 이제 응용 프로그램을 실행 하지만 쇼핑 카트 합계를 볼 수 있습니다.

1. **F5** 키를 눌러 응용 프로그램을 실행합니다.  
 브라우저가 열리고 표시는 *Default.aspx* 페이지.
2. 선택 **자동차** 범주 탐색 메뉴에서 합니다.
3. 클릭는 **Add To Cart** 첫 번째 제품 옆에 있는 링크입니다.   
 *ShoppingCart.aspx* 주문 합계가 표시 됩니다. 

    ![쇼핑 카트-카트 합계](shopping-cart/_static/image7.png)
4. 일부 다른 제품 (예를 들어 평면) 카트에 추가 합니다.
5. *ShoppingCart.aspx* 사용자가 추가한 모든 제품에 대 한는 업데이트 된 합계가 표시 됩니다. 

    ![쇼핑 카트-여러 제품](shopping-cart/_static/image8.png)
6. 브라우저 창을 닫아 실행 중인 응용 프로그램을 중지 합니다.

### <a name="adding-update-and-checkout-buttons-to-the-shopping-cart"></a>업데이트 및 체크 아웃 단추 쇼핑 카트에 추가

사용자가 장바구니를 수정할 수 있도록 추가 **업데이트** 단추 및 **체크 아웃** 단추 쇼핑 카트 페이지를 합니다. **체크 아웃** 단추 자습서 시리즈가 나중에 사용 되지 않습니다.

1. **솔루션 탐색기**열고는 *ShoppingCart.aspx* 웹 응용 프로그램 프로젝트의 루트에는 페이지입니다.
2. 추가 하는 **업데이트** 단추와 **체크 아웃** 단추를 *ShoppingCart.aspx* 페이지에 표시 된 대로 기존 태그에 노란색으로 강조 표시 하는 태그를 추가 합니다는 다음 코드:   

    [!code-aspx[Main](shopping-cart/samples/sample10.aspx?highlight=36-45)]

사용자가 클릭할 때는 **업데이트** 단추는 `UpdateBtn_Click` 이벤트 처리기가 호출 됩니다. 이 이벤트 처리기는 다음 단계에서 추가할 코드를 호출 합니다.

에 포함 된 코드를 업데이트 하는 다음으로 *ShoppingCart.aspx.cs* 카트에 항목 및 호출을 반복 하는 파일의 `RemoveItem` 및 `UpdateItem` 메서드.

1. **솔루션 탐색기**열고는 *ShoppingCart.aspx.cs* 웹 응용 프로그램 프로젝트의 루트에 파일입니다.
2. 노란색으로 강조 표시 된 다음 코드 섹션에 추가 된 *ShoppingCart.aspx.cs* 파일:   

    [!code-csharp[Main](shopping-cart/samples/sample11.cs?highlight=9-11,33,44-89)]

사용자가 클릭할 때는 **업데이트** 단추는 *ShoppingCart.aspx* 페이지 UpdateCartItems 메서드를 호출 합니다. UpdateCartItems 메서드 장바구니의 각 항목에 대 한 업데이트 된 값을 가져옵니다. 그런 다음, UpdateCartItems 메서드 호출는 `UpdateShoppingCartDatabase` 메서드 (추가 하 고 다음 단계에서 설명) 추가 하거나 쇼핑 카트에서 항목을 제거 합니다. 데이터베이스에는 장바구니에 대 한 업데이트를 반영 하도록 업데이트 되 면는 **GridView** 컨트롤을 호출 하 여 쇼핑 카트 페이지에서 업데이트 하는 `DataBind` 에 대 한 메서드는 **GridView**합니다. 또한 총 주문 금액이 쇼핑 카트 페이지에는 업데이트 된 목록 항목에 반영 하도록 업데이트 됩니다.

### <a name="updating-and-removing-shopping-cart-items"></a>업데이트 및 쇼핑 카트 항목 제거

에 *ShoppingCart.aspx* 페이지에서 항목의 수량을 업데이트 하 고 항목을 제거에 대 한 추가 된 컨트롤을 볼 수 있습니다. 이제 작동 이러한 컨트롤에 있도록 코드를 추가 합니다.

1. **솔루션 탐색기**열고는 *ShoppingCartActions.cs* 파일에 *논리* 폴더입니다.
2. 다음 코드를 노란색으로 강조 표시를 추가 *ShoppingCartActions.cs* 클래스 파일:   

    [!code-csharp[Main](shopping-cart/samples/sample12.cs?highlight=99-213)]

`UpdateShoppingCartDatabase` 에서 호출할 메서드는 `UpdateCartItems` 에서 메서드는 *ShoppingCart.aspx.cs* 페이지에서 업데이트 하거나 쇼핑 카트에서 항목을 제거 하기 위한 논리가 포함 합니다. `UpdateShoppingCartDatabase` 메서드 쇼핑 카트 목록 내에서 모든 행을 반복 합니다. 쇼핑 카트에 항목을 제거할 표시가 된 또는 수량이 1 보다 작은 경우는 `RemoveItem` 메서드를 호출 합니다. 에 대 한 쇼핑 카트 항목이 선택 되는 그렇지 않은 경우 업데이트 하는 경우는 `UpdateItem` 메서드를 호출 합니다. 쇼핑 카트에 항목 제거 되거나 업데이트 된 후에 데이터베이스 변경 내용은 저장 됩니다.

`ShoppingCartUpdates` 구조는 모든 쇼핑 카트에 항목을 보유 하는 데 사용 됩니다. `UpdateShoppingCartDatabase` 메서드는 `ShoppingCartUpdates` 업데이트 하거나 제거 해야 할 항목을 확인 하는 구조입니다.

다음 자습서를 사용 하 여는 `EmptyCart` 메서드는 쇼핑 카트에 제품을 구매한 후 합니다. 지금은 사용할 하지만 `GetCount` 에 방금 추가한 메서드는 *ShoppingCartActions.cs* 시장 바구니에 있는 항목 수를 결정 하는 파일입니다.

### <a name="adding-a-shopping-cart-counter"></a>쇼핑 카트 카운터 추가

사용자가 장바구니에 항목의 총 수를 볼 수 있도록 하는 카운터를 추가 합니다는 *Site.Master* 페이지. 이 카운터는 장바구니에 대 한 링크 처럼도 작동 합니다.

1. **솔루션 탐색기**열고는 *Site.Master* 페이지.
2. 다음과 같이 나타나도록 노란색 탐색 섹션에 나와 있는 것 처럼 쇼핑 카트 카운터 링크를 추가 하 여 태그를 수정 합니다.  

    [!code-html[Main](shopping-cart/samples/sample13.html?highlight=6)]
3. 다음을 업데이트 하는 코드 숨김은 *Site.Master.cs* 다음과 같이 노란색으로 강조 표시 하는 코드를 추가 하 여 파일:  

    [!code-csharp[Main](shopping-cart/samples/sample14.cs?highlight=11,77-84)]

페이지가 HTML로 렌더링 되기 전에 `Page_PreRender` 이벤트가 발생 합니다. 에 `Page_PreRender` 처리기를 시장 바구니의 총 수를 호출 하 여 결정 됩니다는 `GetCount` 메서드. 반환 된 값에 추가 되는 `cartCount` 의 태그에 포함 된 범위는 *Site.Master* 페이지. `<span>` 태그 내부 요소를 제대로 렌더링할 수 있습니다. 사이트의 모든 페이지가 표시 되 면 쇼핑 카트 합계가 표시 됩니다. 사용자 쇼핑 카트를 표시 하려면 쇼핑 카트 총액 클릭할 수도 있습니다.

## <a name="testing-the-completed-shopping-cart"></a>완료 된 쇼핑 카트를 테스트합니다.

시장 바구니에 응용 프로그램을 지금 추가 하는 방법을 알아보려면, 삭제 및 업데이트 항목을 실행할 수 있습니다. 쇼핑 카트 총액 시장 바구니에 있는 모든 항목의 총 비용을 반영 합니다.

1. **F5** 키를 눌러 응용 프로그램을 실행합니다.  
 브라우저가 열리고 표시는 *Default.aspx* 페이지.
2. 선택 **자동차** 범주 탐색 메뉴에서 합니다.
3. 클릭는 **Add To Cart** 첫 번째 제품 옆에 있는 링크입니다.   
 *ShoppingCart.aspx* 주문 합계가 표시 됩니다.
4. 선택 **평면** 범주 탐색 메뉴에서 합니다.
5. 클릭는 **Add To Cart** 첫 번째 제품 옆에 있는 링크입니다.
6. 3으로 시장 바구니에 첫 번째 항목의 수량을 설정 하 고 선택 된 **항목 제거** 두 번째 항목의 확인란 합니다.<a id="a"></a>
7. 클릭는 **업데이트** 단추 쇼핑 카트 페이지를 업데이트 하 고 새 주문 합계를 표시 합니다. 

    ![쇼핑 카트-카트 업데이트](shopping-cart/_static/image9.png)

## <a name="summary"></a>요약

이 자습서에서는 Wingtip Toys Web Forms 샘플 응용 프로그램에 대 한 쇼핑 카트를 만들었습니다. 이 자습서에서 Entity Framework Code First, 데이터 주석, 강력한 형식의 데이터 컨트롤 및 모델 바인딩을 사용 했습니다.

쇼핑 카트는 추가, 삭제 및 구매에 대 한 사용자가 선택한 항목을 업데이트를 지원 합니다. 쇼핑 카트 기능을 구현 하는 것 외에도 쇼핑 카트에 항목을 표시 하는 방법을 배웠습니다는 **GridView** 제어 하 고 주문 합계를 계산 합니다.

## <a name="addition-information"></a>추가 정보

[ASP.NET 세션 상태 개요](https://msdn.microsoft.com/library/ms178581.aspx)

>[!div class="step-by-step"]
[이전](display_data_items_and_details.md)
[다음](checkout-and-payment-with-paypal.md)
