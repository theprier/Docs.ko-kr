---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/shopping-cart
title: 쇼핑 카트 | Microsoft Docs
author: Erikre
description: 이 자습서 시리즈는 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 것에 대 한 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항 설명 하는 중...
ms.author: aspnetcontent
ms.date: 09/08/2014
ms.assetid: 6898c601-6c31-432f-8388-e6843f8a17cb
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/shopping-cart
msc.type: authoredcontent
ms.openlocfilehash: 00fd00778477bea21add76c799dbfe24dfdec1dc
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37817004"
---
<a name="shopping-cart"></a>쇼핑 카트
====================
[Erik Reitan](https://github.com/Erikre)

[Wingtip Toys 샘플 프로젝트 (C#)를 다운로드](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자책 (PDF) 다운로드](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 이 자습서 시리즈는 ASP.NET 4.5와 Microsoft Visual Studio Express 2013 for Web 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 합니다. Visual Studio 2013 [C# 소스 코드를 사용 하 여 프로젝트](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 이 자습서 시리즈를 함께 사용할 수 있습니다.


이 자습서에서는 Wingtip Toys 샘플 ASP.NET Web Forms 응용 프로그램에 쇼핑 카트에 추가 하는 데 필요한 비즈니스 논리를 설명 합니다. 이 자습서는 이전 자습서 "데이터 항목 및 세부 정보를 표시" 빌드하고 Wingtip 장난감 자습서 시리즈의 일부입니다. 이 자습서를 완료 하면 샘플 앱의 사용자 추가, 제거 및 시장 바구니의 제품을 수정 하는 일을 할 됩니다.

## <a name="what-youll-learn"></a>학습할 내용:

1. 웹 응용 프로그램의 쇼핑 카트를 만드는 방법입니다.
2. 사용자가 장바구니에 항목을 추가 하는 방법입니다.
3. 추가 하는 방법에 [GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview(v=vs.110).aspx#introduction) 쇼핑 카트 세부 정보를 표시 하는 컨트롤입니다.
4. 계산 및 주문 합계를 표시 하는 방법.
5. 제거 하 고 장바구니에 항목을 업데이트 하는 방법.
6. 쇼핑 카트 카운터를 포함 하는 방법입니다.

## <a name="code-features-in-this-tutorial"></a>이 자습서의 코드 기능:

1. Entity Framework Code First
2. 데이터 주석
3. 강력한 형식의 데이터 컨트롤
4. 모델 바인딩

## <a name="creating-a-shopping-cart"></a>쇼핑 카트 만들기

이 자습서 시리즈의 앞부분에 나오는 페이지와 데이터베이스에서 제품 데이터를 보려면 코드를 추가 합니다. 이 자습서에서는 제품을 관리 하는 쇼핑 카트를 만든 사용자가 구매 관심 합니다. 사용자는 수를 찾아서 등록 하거나 로그인 하지 않더라도 장바구니에 항목을 추가할 수 있습니다. 쇼핑 카트 액세스를 관리 하려면 할당할 예정 이므로 사용자가 고유한 `ID` 처음 카트에 쇼핑을 사용자가 액세스 하는 경우에 전역적으로 고유 식별자 (GUID)를 사용 하 여 합니다. 이 저장 `ID` ASP.NET 세션 상태를 사용 하 여 합니다.

> [!NOTE] 
> 
> ASP.NET 세션 상태가 사용자 사이트를 퇴사 만료 되는 사용자 관련 정보를 저장 하는 편리한 장소입니다. 세션 상태를 잘못 사용 하면 대규모 사이트에 성능에 미치는 영향을 미칠 수 있습니다, 있지만 light 세션 상태 작동 데모 용도로 사용 합니다. Wingtip Toys 샘플 프로젝트에 세션 상태가 저장된-프로세스에서 사이트를 호스팅하는 웹 서버에 있는 외부 공급자로 없이 세션 상태를 사용 하는 방법을 보여 줍니다. 응용 프로그램의 여러 인스턴스를 제공 하는 대규모 사이트 또는 다른 서버에서 응용 프로그램의 여러 인스턴스를 실행 하는 사이트에 대 한 사용을 고려 **Windows Azure Cache Service**합니다. 이 캐시 서비스는 외부 웹 사이트에 있으며 in-process 세션 상태를 사용 하 여 문제를 해결 하는 분산된 캐싱 서비스를 제공 합니다. 자세한 내용은 참조 하십시오 [사용 하 여 ASP.NET 세션 상태 Windows Azure 웹 사이트와 방법](https://docs.microsoft.com/azure/redis-cache/cache-aspnet-session-state-provider)합니다.


### <a name="add-cartitem-as-a-model-class"></a>CartItem 모델 클래스 추가

이 자습서 시리즈의 앞부분에서 만들어 범주 및 제품 데이터에 대 한 스키마를 정의 합니다 `Category` 하 고 `Product` 의 클래스를 *모델* 폴더. 이제 장바구니에 대 한 스키마를 정의 하는 새 클래스를 추가 합니다. 이 자습서의 뒷부분에서 추가한 데이터에 대 한 액세스를 처리 하는 클래스는 `CartItem` 테이블입니다. 이 클래스에는 추가, 제거 및 시장 바구니에 항목을 업데이트 하는 비즈니스 논리가 제공 됩니다.

1. 마우스 오른쪽 단추로 클릭 합니다 *모델* 선택한 폴더 **추가**  - &gt; **새 항목**합니다. 

    ![쇼핑 카트-새 항목](shopping-cart/_static/image1.png)
2. **새 항목 추가** 대화 상자가 표시됩니다. 선택 **코드**를 선택한 후 **클래스**합니다. 

    ![쇼핑 카트-새 항목 추가 대화 상자](shopping-cart/_static/image2.png)
3. 이 새 클래스 이름을 *CartItem.cs*합니다.
4. **추가**를 클릭합니다.  
   새 클래스 파일을 편집기에 표시 됩니다.
5. 기본 코드를 다음 코드로 바꿉니다.   

    [!code-csharp[Main](shopping-cart/samples/sample1.cs)]

`CartItem` 사용자 쇼핑 카트에 추가 하는 각 제품에 정의한 스키마를 포함 하는 클래스입니다. 이 클래스는이 자습서 시리즈의 앞부분에서 만든 다른 스키마 클래스와 비슷합니다. 규칙에 따라 Entity Framework Code First 예상 하는 기본 키를 `CartItem` 테이블 중 하나가 됩니다 `CartItemId` 또는 `ID`합니다. 코드 데이터 주석을 사용 하 여 기본 동작을 재정의 하는 반면 `[Key]` 특성입니다. `Key` ItemId 속성의 특성을 지정 하는 `ItemID` 속성이 기본 키입니다.

합니다 `CartId` 속성을 지정 합니다 `ID` 구매 항목과 연결 된 사용자의 합니다. 이 사용자를 만드는 코드를 추가할 `ID` 사용자가 장바구니를 액세스 하는 경우. 이 `ID` 도 ASP.NET 세션 변수로 저장 됩니다.

### <a name="update-the-product-context"></a>제품 컨텍스트 업데이트

추가 하는 것 외에도 `CartItem` 엔터티 클래스를 관리 하 고 데이터베이스에 대 한 데이터 액세스를 제공 하는 데이터베이스 컨텍스트 클래스를 업데이트 해야 클래스입니다. 이렇게 하려면 새로 만든 추가 합니다 `CartItem` 모델에 클래스는 `ProductContext` 클래스입니다.

1. **솔루션 탐색기**, 찾기 및 열기를 *ProductContext.cs* 파일을 *모델* 폴더입니다.
2. 강조 표시 된 코드를 추가 합니다 *ProductContext.cs* 다음과 같이 파일:  

    [!code-csharp[Main](shopping-cart/samples/sample2.cs?highlight=14)]

이 자습서 시리즈의 코드에서 이전에 설명한 것 처럼 합니다 *ProductContext.cs* 파일 추가 `System.Data.Entity` 네임 스페이스 Entity Framework의 모든 핵심 기능에 액세스할 수 있도록 합니다. 이 기능은 쿼리, 삽입, 업데이트 및 강력한 형식의 개체를 사용 하 여 데이터를 삭제 하는 기능을 포함 합니다. 합니다 `ProductContext` 하 고 새로 추가한 액세스를 추가 하는 클래스 `CartItem` 모델 클래스입니다.

### <a name="managing-the-shopping-cart-business-logic"></a>쇼핑 카트 비즈니스 논리를 관리합니다.

만든 다음에 `ShoppingCart` 클래스의 새 *논리* 폴더입니다. 합니다 `ShoppingCart` 에 대 한 데이터 액세스를 처리 하는 클래스는 `CartItem` 테이블입니다. 클래스 추가, 제거 및 시장 바구니에 항목을 업데이트 하는 비즈니스 논리가 포함 됩니다.

쇼핑 카트 하는 논리를 추가한 다음 작업을 관리 하는 기능을 포함 됩니다.

1. 쇼핑 카트에 항목 추가
2. 장바구니에서 항목 제거
3. 쇼핑 카트 ID 가져오기
4. 장바구니에서 항목을 가져오는 중
5. 모든 쇼핑 카트 항목의 크기를 합계 해
6. 쇼핑 카트 데이터를 업데이트 하는 중

쇼핑 카트 페이지 (*ShoppingCart.aspx*) 쇼핑 카트 데이터를 액세스 하려면 쇼핑 카트 클래스를 함께 사용 됩니다. 쇼핑 카트 페이지에는 사용자가 장바구니에 추가 항목을 모두 표시 됩니다. 쇼핑 카트에서 페이지 및 클래스 외에 페이지를 만듭니다 (*AddToCart.aspx*) 하 고 쇼핑 카트에 제품을 추가 합니다. 코드를 추가 합니다는 *ProductList.aspx* 페이지 및 *ProductDetails.aspx* 링크를 제공 하는 페이지를 *AddToCart.aspx* 사용자를 추가할 수 있도록 페이지 쇼핑 카트에 제품입니다.

다음 다이어그램은 사용자 쇼핑 카트에 제품을 추가할 때 발생 하는 기본 프로세스를 보여 줍니다.

![쇼핑 카트-쇼핑 카트에 추가](shopping-cart/_static/image3.png)

클릭할 때 합니다 **Add To Cart** 링크에는 *ProductList.aspx* 페이지 또는 *ProductDetails.aspx* 페이지에서 응용 프로그램 이동 합니다 *AddToCart.aspx* 페이지 다음에 자동으로 *ShoppingCart.aspx* 페이지입니다. 합니다 *AddToCart.aspx* 페이지 ShoppingCart 클래스에서 메서드를 호출 하 여 쇼핑 카트에 제품 선택에 추가 합니다. 합니다 *ShoppingCart.aspx* 쇼핑 카트에 추가 된 제품 페이지에 표시 됩니다.

#### <a name="creating-the-shopping-cart-class"></a>쇼핑 카트 클래스 만들기

`ShoppingCart` 클래스가 응용 프로그램에서 별도 폴더에 추가 되는 모델 (모델 폴더), 페이지 (루트 폴더) 및 (논리 폴더)에 논리를 명확히 구분 될 수 있도록 합니다.

1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **WingtipToys**프로젝트를 마우스 **추가**-&gt;**새 폴더**. 새 폴더의 이름을 *논리*합니다.
2. 마우스 오른쪽 단추로 클릭 합니다 *논리* 한 다음 선택한 폴더 **추가**  - &gt; **새 항목**합니다.
3. 라는 새 클래스 파일을 추가 *ShoppingCartActions.cs*합니다.
4. 기본 코드를 다음 코드로 바꿉니다.   

    [!code-csharp[Main](shopping-cart/samples/sample3.cs)]

합니다 `AddToCart` 메서드를 사용 하면 제품에 따라 장바구니에 포함할 개별 제품 `ID`합니다. 제품 장바구니에 더하거나 카트 해당 제품에 대 한 항목이 이미 있으면 수량 증가 됩니다.

합니다 `GetCartId` 반환 카트 `ID` 사용자에 대 한 합니다. 카트 `ID` 사용자가 장바구니에 있는 항목을 추적 하는 데 사용 됩니다. 사용자는 기존 카트 없으면 `ID`, 새 카트 `ID` 만들어집니다. 등록 된 사용자의 카트 사용자가 로그인 하는 경우 `ID` 자신의 사용자 이름으로 설정 됩니다. 그러나 사용자가 바구니에 서명 되지 않은 경우 `ID` 고유 값 (GUID)로 설정 됩니다. 해당 하나만 카트가 세션에 따라 각 사용자에 대해 생성을 확인 하는 GUID입니다.

`GetCartItems` 메서드 쇼핑 카트 항목 사용자에 대 한 목록을 반환 합니다. 이 자습서의 뒷부분에서 보면 모델 바인딩을 사용 하 여 쇼핑 카트 카트에 항목을 표시를 사용 하 여 `GetCartItems` 메서드.

### <a name="creating-the-add-to-cart-functionality"></a>카트 추가 기능 만들기

라는 처리 페이지 앞에서 설명한 대로 만들어집니다 *AddToCart.aspx* 하는 데 사용할 사용자의 쇼핑 카트에 새 제품을 추가 합니다. 이 페이지는 호출을 `AddToCart` 의 메서드는 `ShoppingCart` 방금 만든 클래스. 합니다 *AddToCart.aspx* 페이지는 것을 예상 하는 제품 `ID` 에 전달 됩니다. 이 제품 `ID` 호출할 때 사용할 합니다 `AddToCart` 에서 메서드를 `ShoppingCart` 클래스입니다.

> [!NOTE] 
> 
> 관련 코드를 수정 합니다 (*AddToCart.aspx.cs*)이 페이지는 페이지 UI (*AddToCart.aspx*).


#### <a name="to-create-the-add-to-cart-functionality"></a>카트에 추가를 만들려면 기능:

1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **WingtipToys**프로젝트 **추가**  - &gt; **새 항목**합니다.  
   **새 항목 추가** 대화 상자가 표시됩니다.
2. 표준 새 페이지 (Web Form) 라는 응용 프로그램에 추가 *AddToCart.aspx*합니다. 

    ![쇼핑 카트-Web Form 추가](shopping-cart/_static/image4.png)
3. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 *AddToCart.aspx* 페이지를 클릭 한 다음 **코드 보기**합니다. 합니다 *AddToCart.aspx.cs* 편집기에서 코드 숨김 파일이 열립니다.
4. 기존 코드를 대체 합니다 *AddToCart.aspx.cs* 코드 숨김 다음을 사용 하 여:   

    [!code-csharp[Main](shopping-cart/samples/sample4.cs)]

경우는 *AddToCart.aspx* 페이지가 로드 되는 제품 `ID` 쿼리 문자열에서 검색 됩니다. 다음으로, 쇼핑 카트 클래스의 인스턴스 생성 되어 호출 하는 데는 `AddToCart` 이 자습서의 앞부분에서 추가한 메서드. 합니다 `AddToCart` 에 포함 된 메서드를 *ShoppingCartActions.cs* 파일, 선택한 제품을 장바구니에 추가 하거나 선택한 제품의 제품 수량 증가 하는 논리를 포함 합니다. 제품을 장바구니에 추가 되지 않은, 경우에 제품에 추가 됩니다는 `CartItem` 데이터베이스의 테이블입니다. 제품 수량 증가 제품이 쇼핑 카트에 이미 추가 되었습니다. 동일한 제품의 추가 항목을 추가 하는 사용자를는 `CartItem` 테이블입니다. 마지막으로, 페이지를 다시 리디렉션합니다 합니다 *ShoppingCart.aspx* 페이지를 사용자에 게 바구니에 항목의 업데이트 된 목록을 표시 하는 다음 단계에 추가 합니다.

앞서 언급 했 듯이 사용자 `ID` 특정 사용자와 연관 된 제품을 식별 하는 데 사용 됩니다. 이 `ID` 의 행에 추가 되는 `CartItem` 사용자 쇼핑 카트에 제품을 추가할 때마다 테이블입니다.

### <a name="creating-the-shopping-cart-ui"></a>쇼핑 카트 UI 만들기

합니다 *ShoppingCart.aspx* 페이지는 사용자가 해당 쇼핑 카트에 추가 하는 제품을 표시 합니다. 또한 추가, 제거 및 시장 바구니에 항목을 업데이트 하는 기능을 제공 됩니다.

1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 **WingtipToys**, 클릭 **추가**  - &gt; **새 항목**합니다.  
   **새 항목 추가** 대화 상자가 표시됩니다.
2. 선택 하 여 마스터 페이지를 포함 하는 새 페이지 (Web Form)를 추가 **웹 폼 마스터 페이지를 사용 하 여**입니다. 새 페이지의 이름을 *ShoppingCart.aspx*합니다.
3. 선택 **Site.Master** 마스터 페이지를 새로 만든 연결할 *.aspx* 페이지입니다.
4. 에 *ShoppingCart.aspx* 페이지에서 기존 태그를 다음 태그로 바꿉니다.   

    [!code-aspx[Main](shopping-cart/samples/sample5.aspx)]

*ShoppingCart.aspx* 페이지에는 **GridView** 라는 컨트롤 `CartList`합니다. 이 컨트롤을 데이터베이스에서 쇼핑 카트 데이터를 바인딩할 모델 바인딩을 사용 하 여 **GridView** 제어 합니다. 설정한 경우는 `ItemType` 의 속성을 **GridView** 컨트롤을 데이터 바인딩 식을 `Item` 에서 사용할 수 있습니다 컨트롤 및 컨트롤의 태그를 강력 하 게 형식화 됩니다. 이 자습서 시리즈의 앞부분에서 설명 했 듯이의 세부 정보를 선택할 수 있습니다는 `Item` IntelliSense를 사용 하 여 개체입니다. 모델 바인딩을 사용 하 여 데이터를 선택 하도록 데이터 컨트롤을 구성 하려면 설정의 `SelectMethod` 컨트롤의 속성입니다. 위의 태그에서 설정 합니다 `SelectMethod` 목록을 반환 하는 GetShoppingCartItems 메서드를 사용 하 `CartItem` 개체입니다. 합니다 **GridView** 데이터 컨트롤의 페이지 수명 주기의 적절 한 시간에 메서드를 호출 하 고 자동으로 반환된 된 데이터를 바인딩합니다. `GetShoppingCartItems` 메서드 추가 해야 합니다.

#### <a name="retrieving-the-shopping-cart-items"></a>쇼핑 카트 항목 검색

다음으로 코드를 추가 합니다 *ShoppingCart.aspx.cs* 검색 하 고 쇼핑 카트 UI를 채우는 코드 숨김입니다.

1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 *ShoppingCart.aspx* 페이지를 클릭 한 다음 **코드 보기**합니다. 합니다 *ShoppingCart.aspx.cs* 편집기에서 코드 숨김 파일이 열립니다.
2. 기존 코드를 다음으로 바꿉니다.  

    [!code-csharp[Main](shopping-cart/samples/sample6.cs)]

위에서 설명한 대로 합니다 `GridView` 데이터 컨트롤을 호출 합니다 `GetShoppingCartItems` 페이지의 적절 한 시간 주기 메서드와 반환된 된 데이터를 자동으로 바인딩합니다. 합니다 `GetShoppingCartItems` 메서드는 인스턴스를 만듭니다를 `ShoppingCartActions` 개체입니다. 코드를 호출 하 여 바구니에 항목을 반환 하는 인스턴스를 사용 하는 다음을 `GetCartItems` 메서드.

### <a name="adding-products-to-the-shopping-cart"></a>쇼핑 카트에 추가 제품

경우 중 하나는 *ProductList.aspx* 또는 *ProductDetails.aspx* 페이지가 표시 되 면 사용자 링크를 사용 하 여 쇼핑 카트에 제품을 추가할 수 있습니다. 응용 프로그램 이라는 처리 페이지를 탐색 링크를 클릭 하면 *AddToCart.aspx*합니다. *AddToCart.aspx* 페이지는 호출을 `AddToCart` 에서 메서드는 `ShoppingCart` 이 자습서의 앞부분에서 추가한 클래스.

이제를 추가 합니다는 **카트에 추가** 둘 다에 대 한 링크는 *ProductList.aspx* 페이지와 *ProductDetails.aspx* 페이지입니다. 이 링크는 제품을 포함 하는 `ID` 는 데이터베이스에서 검색 됩니다.

1. **솔루션 탐색기**찾아 라는 페이지를 열려면 *ProductList.aspx*합니다.
2. 노란색으로 강조 표시 된 태그를 추가 합니다 *ProductList.aspx* 전체 페이지는 다음과 같이 표시 되도록 페이지:  

    [!code-aspx[Main](shopping-cart/samples/sample7.aspx?highlight=50-54)]

### <a name="testing-the-shopping-cart"></a>쇼핑 카트를 테스트합니다.

쇼핑 카트에 제품을 추가 하는 방법을 확인 하려면 응용 프로그램을 실행 합니다.

1. **F5** 키를 눌러 응용 프로그램을 실행합니다.  
 후 프로젝트 데이터베이스를 다시 만듭니다, 브라우저를 열고 표시 합니다 *Default.aspx* 페이지입니다.
2. 선택 **자동차** 범주 탐색 합니다.  
 합니다 *ProductList.aspx* "자동차" 범주에 포함 된 제품만 보여 주는 페이지가 표시 됩니다. 

    ![쇼핑 카트-자동차](shopping-cart/_static/image5.png)
3. 클릭 합니다 **카트에 추가** 첫 번째 제품 옆에 있는 링크 (변환할 자동차)을 나열 합니다.   
 합니다 *ShoppingCart.aspx* 쇼핑 카트에 선택 영역을 보여 주는 페이지가 표시 됩니다. 

    ![쇼핑 카트-카트](shopping-cart/_static/image6.png)
4. 추가 제품을 선택 하 여 볼 **평면** 범주 탐색 합니다.
5. 클릭 합니다 **카트에 추가** 나열 된 첫 번째 제품 옆에 있는 링크입니다.  
 합니다 *ShoppingCart.aspx* 페이지가 추가 항목으로 표시 됩니다.
6. 브라우저를 닫습니다.

### <a name="calculating-and-displaying-the-order-total"></a>계산 및 주문 합계를 표시 합니다.

제품을 장바구니에 추가 하는 것 외에도 추가 합니다는 `GetTotal` 메서드를는 `ShoppingCart` 클래스 및 총 주문 금액이 쇼핑 카트 페이지에 표시 합니다.

1. **솔루션 탐색기**오픈를 *ShoppingCartActions.cs* 파일을 *논리* 폴더.
2. 다음을 추가 합니다 `GetTotal` 에 노란색으로 강조 표시 하는 메서드는 `ShoppingCart` 클래스는 다음과 같이 표시 되도록 클래스:   

    [!code-csharp[Main](shopping-cart/samples/sample8.cs?highlight=85-97)]

첫 번째는 `GetTotal` 메서드는 사용자에 대 한 장바구니의 ID를 가져옵니다. 다음 메서드는 장바구니에 나열 된 각 제품에 대 한 제품 수량 제품 가격을 곱하여 총 카트를 가져옵니다.

> [!NOTE] 
> 
> 위의 코드에서는 nullable 형식 "`int?`"입니다. Nullable 형식은 기본 형식 및 null 값으로 모든 값을 나타낼 수 있습니다. 자세한 내용은 참조 하십시오 [Nullable 형식 사용](https://msdn.microsoft.com/library/2cf62fcy(v=vs.110).aspx)합니다.


### <a name="modify-the-shopping-cart-display"></a>쇼핑 카트 표시 수정

다음의 코드를 수정 합니다 *ShoppingCart.aspx* 를 호출 하는 페이지는 `GetTotal` 메서드와 해당에서 합계를 표시를 *ShoppingCart.aspx* 페이지가 페이지가 로드 될 때.

1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 *ShoppingCart.aspx* 페이지를 선택 **코드 보기**합니다.
2. 에 *ShoppingCart.aspx.cs* 파일을 업데이트 합니다 `Page_Load` 노란색으로 강조 표시 하는 다음 코드를 추가 하 여 처리기:   

    [!code-csharp[Main](shopping-cart/samples/sample9.cs?highlight=16-31)]

경우는 *ShoppingCart.aspx* 페이지 로드, 쇼핑 카트 개체를 로드 하 고 호출 하 여 쇼핑 카트 합계를 검색 한 다음 해당 합니다 `GetTotal` 메서드의 `ShoppingCart` 클래스. 쇼핑 카트 비어 있는 경우 메시지를 그 결과 표시 됩니다.

### <a name="testing-the-shopping-cart-total"></a>쇼핑 카트 합계를 테스트합니다.

응용 프로그램이 이제 어떻게 추가할 수 없습니다만 제품을 장바구니를 실행 하지만 쇼핑 카트 합계를 볼 수 있습니다.

1. **F5** 키를 눌러 응용 프로그램을 실행합니다.  
 브라우저를 열고 표시 합니다 *Default.aspx* 페이지입니다.
2. 선택 **자동차** 범주 탐색 합니다.
3. 클릭 합니다 **Add To Cart** 첫 번째 제품 옆에 있는 링크입니다.   
 합니다 *ShoppingCart.aspx* 주문 합계를 사용 하 여 페이지가 표시 됩니다. 

    ![쇼핑 카트-카트 합계](shopping-cart/_static/image7.png)
4. 일부 다른 제품 (예를 들어, 평면) 카트에 추가 합니다.
5. 합니다 *ShoppingCart.aspx* 추가한 다음 모든 제품에 대 한 업데이트 된 합계를 사용 하 여 페이지가 표시 됩니다. 

    ![쇼핑 카트-여러 제품](shopping-cart/_static/image8.png)
6. 브라우저 창을 닫아 실행 중인 앱을 중지 합니다.

### <a name="adding-update-and-checkout-buttons-to-the-shopping-cart"></a>시장 바구니에 업데이트 및 체크 아웃 단추 추가

쇼핑 카트를 수정 하려면 사용자를 허용 하려면 추가 **업데이트** 단추와 **체크 아웃** 쇼핑 카트 페이지에는 단추입니다. 합니다 **체크 아웃** 이 자습서 시리즈에서는 나중까지 단추가 사용 되지 않습니다.

1. **솔루션 탐색기**엽니다는 *ShoppingCart.aspx* 웹 응용 프로그램 프로젝트의 루트에는 페이지입니다.
2. 추가할 합니다 **업데이트** 단추 및 **체크 아웃** 단추를 *ShoppingCart.aspx* 페이지에 표시 된 대로 기존 태그에는 노란색으로 강조 표시 태그를 추가 합니다는 코드를 다음과 같습니다.   

    [!code-aspx[Main](shopping-cart/samples/sample10.aspx?highlight=36-45)]

클릭할 때 합니다 **업데이트** 단추를 `UpdateBtn_Click` 이벤트 처리기가 호출 됩니다. 이 이벤트 처리기는 다음 단계에서 추가 하는 코드를 호출 합니다.

다음으로, 포함 된 코드를 업데이트할 수 있습니다 합니다 *ShoppingCart.aspx.cs* 카트 항목 및 호출을 반복 하는 파일을 `RemoveItem` 및 `UpdateItem` 메서드.

1. **솔루션 탐색기**오픈 합니다 *ShoppingCart.aspx.cs* 웹 응용 프로그램 프로젝트의 루트에 있는 파일입니다.
2. 다음 코드 섹션에는 노란색으로 강조 표시를 추가 합니다 *ShoppingCart.aspx.cs* 파일:   

    [!code-csharp[Main](shopping-cart/samples/sample11.cs?highlight=9-11,33,44-89)]

클릭할 때 합니다 **업데이트** 단추를 *ShoppingCart.aspx* 페이지 UpdateCartItems 메서드를 호출 합니다. UpdateCartItems 메서드 쇼핑 카트의 각 항목에 대 한 업데이트 된 값을 가져옵니다. UpdateCartItems 메서드를 호출 하는 다음을 `UpdateShoppingCartDatabase` 메서드 (추가 및 다음 단계에서 설명) 추가 하거나 장바구니에서 항목을 제거 합니다. 데이터베이스를 업데이트 하 고 쇼핑 카트에 반영 하도록 업데이트 하면를 **GridView** 컨트롤이 호출 하 여 쇼핑 카트 페이지에서 업데이트 됩니다는 `DataBind` 에 대 한 메서드를 **GridView**합니다. 또한 주문 총액 쇼핑 카트 페이지에서 업데이트 된 항목 목록을 반영 하도록 업데이트 됩니다.

### <a name="updating-and-removing-shopping-cart-items"></a>업데이트 및 쇼핑 카트 항목 제거

에 *ShoppingCart.aspx* 페이지 항목의 수량을 업데이트 하 고 항목을 제거 하는 것에 대 한 추가 된 컨트롤을 볼 수 있습니다. 이제 이러한 컨트롤을 작동 하 게 하는 코드를 추가 합니다.

1. **솔루션 탐색기**오픈를 *ShoppingCartActions.cs* 파일을 *논리* 폴더.
2. 노란색으로 강조 표시 된 다음 코드를 추가 합니다 *ShoppingCartActions.cs* 클래스 파일:   

    [!code-csharp[Main](shopping-cart/samples/sample12.cs?highlight=99-213)]

`UpdateShoppingCartDatabase` 에서 호출 된 메서드를 `UpdateCartItems` 메서드는 *ShoppingCart.aspx.cs* 페이지, 업데이트 또는 장바구니에서 항목을 제거 하기 위한 논리가 포함 합니다. `UpdateShoppingCartDatabase` 메서드 쇼핑 카트 목록 내에서 모든 행을 반복 합니다. 쇼핑 카트에 항목을 제거 하려면 표시 된 수량은 1 보다 작은 경우는 `RemoveItem` 메서드가 호출 됩니다. 쇼핑 카트 항목에 대 한 확인란이 고, 그렇지 경우 업데이트는 `UpdateItem` 메서드가 호출 됩니다. 쇼핑 카트 항목 제거 되거나 업데이트 된 후 데이터베이스 변경 내용이 저장 됩니다.

`ShoppingCartUpdates` 구조에 쇼핑 카트에 항목을 모두를 포함할 수 있습니다. 합니다 `UpdateShoppingCartDatabase` 메서드는 `ShoppingCartUpdates` 구조를 업데이트 하거나 제거 해야 항목을 확인 합니다.

다음 자습서에서는 사용 하 여는 `EmptyCart` 제품을 구매한 후 카트에 쇼핑의 선택을 취소 하는 방법입니다. 이제 사용 하지만 합니다 `GetCount` 에 방금 추가한 메서드를 *ShoppingCartActions.cs* 시장 바구니에 있는 항목 수를 결정 하는 파일입니다.

### <a name="adding-a-shopping-cart-counter"></a>쇼핑 카트 카운터 추가

시장 바구니에 항목의 총 수를 볼 수 있도록 하는 카운터를 추가 합니다 *Site.Master* 페이지입니다. 이 카운터는 장바구니에 대 한 링크 처럼도 작동 합니다.

1. **솔루션 탐색기**오픈 합니다 *Site.Master* 페이지입니다.
2. 다음과 같이 표시 되도록 탐색 섹션에는 노란색으로 표시 된 것 처럼 쇼핑 카트 카운터 링크를 추가 하 여 태그를 수정 합니다.  

    [!code-html[Main](shopping-cart/samples/sample13.html?highlight=6)]
3. 다음으로 업데이트 하는 코드 숨김 합니다 *Site.Master.cs* 같이 노란색으로 강조 표시 된 코드를 추가 하 여 파일:  

    [!code-csharp[Main](shopping-cart/samples/sample14.cs?highlight=11,77-84)]

페이지가 HTML로 렌더링 되기 전에 `Page_PreRender` 이벤트가 발생 합니다. 에 `Page_PreRender` 쇼핑 카트 총 처리기를 호출 하 여 결정 됩니다는 `GetCount` 메서드. 반환 된 값을 추가 합니다 `cartCount` 의 태그에 포함 된 범위를 *Site.Master* 페이지. `<span>` 태그 올바르게 렌더링 되어야 하 고 내부 요소를 사용 하도록 설정 합니다. 사이트의 모든 페이지가 표시 되 면 쇼핑 카트 합계 표시 됩니다. 또한 쇼핑 카트를 표시 하려면 쇼핑 카트 합계 클릭할 수 있습니다.

## <a name="testing-the-completed-shopping-cart"></a>완료 된 쇼핑 카트를 테스트합니다.

시장 바구니에 추가 하는 방법을 확인 하려면 지금를 응용 프로그램, 삭제 및 업데이트 항목을 실행할 수 있습니다. 쇼핑 카트 합계에는 시장 바구니에 있는 모든 항목의 총 비용은 반영 됩니다.

1. **F5** 키를 눌러 응용 프로그램을 실행합니다.  
 브라우저가 열리고 표시 합니다 *Default.aspx* 페이지입니다.
2. 선택 **자동차** 범주 탐색 합니다.
3. 클릭 합니다 **Add To Cart** 첫 번째 제품 옆에 있는 링크입니다.   
 합니다 *ShoppingCart.aspx* 주문 합계를 사용 하 여 페이지가 표시 됩니다.
4. 선택 **평면** 범주 탐색 합니다.
5. 클릭 합니다 **Add To Cart** 첫 번째 제품 옆에 있는 링크입니다.
6. 첫 번째 항목의 수량을 3으로 시장 바구니에 설정 하 고 선택 합니다 **항목 제거** 두 번째 항목의 확인란 합니다.<a id="a"></a>
7. 클릭 합니다 **업데이트** 단추 쇼핑 카트 페이지를 업데이트 하 고 새 주문 합계를 표시 합니다. 

    ![쇼핑 카트-장바구니 업데이트](shopping-cart/_static/image9.png)

## <a name="summary"></a>요약

이 자습서에서는 Wingtip Toys Web Forms 샘플 응용 프로그램의 쇼핑 카트를 만든 것입니다. 이 자습서에서 Entity Framework Code First, 데이터 주석, 강력한 형식의 데이터 컨트롤 및 모델 바인딩을 사용 했습니다.

쇼핑 카트는 추가, 삭제 및 구매에 대 한 사용자가 선택한 항목 업데이트를 지원 합니다. 쇼핑 카트 기능을 구현 하는 것 외에도 장바구니 품목을 표시 하는 방법을 익 혔는 **GridView** 제어 하 고 주문 합계를 계산 합니다.

## <a name="addition-information"></a>추가 정보

[ASP.NET 세션 상태 개요](https://msdn.microsoft.com/library/ms178581.aspx)

> [!div class="step-by-step"]
> [이전](display_data_items_and_details.md)
> [다음](checkout-and-payment-with-paypal.md)
