---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
title: 데이터 표시 항목 및 세부 정보 | Microsoft Docs
author: Erikre
description: 이 자습서 시리즈에서는 ASP.NET 4.7 및 Microsoft Visual Studio 2017을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항
ms.author: riande
ms.date: 1/04/2019
ms.assetid: 64a491a8-0ed6-4c2f-9c1c-412962eb6006
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
msc.type: authoredcontent
ms.openlocfilehash: acc2f8e78375ef0455d467e2af750ecbee623224
ms.sourcegitcommit: 184ba5b44d1c393076015510ac842b77bc9d4d93
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2019
ms.locfileid: "54396227"
---
<a name="display-data-items-and-details"></a>데이터 항목 및 세부 정보
====================
[Erik Reitan](https://github.com/Erikre)

> 이 자습서 시리즈에서는 ASP.NET 4.7 및 Microsoft Visual Studio 2017을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 합니다.

이 자습서에서는 데이터 항목 및 ASP.NET Web Forms 및 Entity Framework Code First를 사용 하 여 데이터 항목 세부 정보를 표시 하는 방법에 알아봅니다. 이 자습서 Wingtip 장난감 자습서 시리즈의 일부로 이전 "UI 및 탐색" 자습서를 기반으로 합니다. 이 자습서를 완료 한 후에 제품이 표시 됩니다는 *ProductsList.aspx* 페이지 및 제품의 세부 정보에는 *ProductDetails.aspx* 페이지입니다.

## <a name="youll-learn-how-to"></a>다음을 수행하는 방법을 알아봅니다.

- 데이터베이스에서 제품을 전시 하기 데이터 컨트롤 추가
- 데이터 컨트롤을 선택한 데이터에 연결
- 데이터베이스에서 제품 세부 정보를 표시 하는 데이터 컨트롤 추가
- 쿼리 문자열에서 값을 검색 하 고 해당 값을 사용 하 여 데이터베이스에서 검색 되는 데이터 제한

### <a name="features-introduced-in-this-tutorial"></a>이 자습서에 도입 된 기능:

- 모델 바인딩
- 값 공급자

## <a name="add-a-data-control"></a>데이터 컨트롤 추가

서버 컨트롤에 데이터를 바인딩할 몇 가지 다른 옵션을 사용할 수 있습니다. 가장 일반적인 다음과 같습니다.

 * 데이터 소스 컨트롤 추가
 * 코드를 직접 추가
 * 모델 바인딩을 사용 하 여

### <a name="use-a-data-source-control-to-bind-data"></a>데이터 소스 컨트롤을 사용 하 여 데이터를 바인딩할

데이터 소스 컨트롤을 추가 데이터를 표시 하는 컨트롤에 데이터 소스 컨트롤을 연결할 수 있습니다. 이 접근 방식 대신 수 있습니다 선언적으로 프로그래밍 방식으로 데이터 원본에 서버 쪽 컨트롤을 연결 합니다.

### <a name="code-by-hand-to-bind-data"></a>직접 데이터를 바인딩하는 코드

직접 코딩 하는 작업에 포함 됩니다.

1. 값 읽기
2. Null 인지 확인
3. 적절 한 형식으로 변환
4. 변환이 성공 확인
5. 쿼리에서 값을 사용 하 여 

이 방법을 사용 하면 데이터 액세스 논리를 완벽히 제어할 수 있습니다.

### <a name="use-model-binding-to-bind-data"></a>모델 바인딩을 사용 하 여 데이터 바인딩

모델 바인딩 훨씬 적은 코드를 사용 하 여 결과 바인딩할 수 있습니다. 및 기능을 응용 프로그램 전체에서 재사용할 수 있는 기능을 제공 합니다. 풍부 하 고 데이터 바인딩 프레임 워크를 제공 하면서 코드에 초점을 맞춘 데이터 액세스 논리를 사용 하 여 작업을 간소화 합니다.

## <a name="display-products"></a>제품 표시

이 자습서에서는 데이터를 바인딩할 모델 바인딩을 사용할 수 있습니다. 컨트롤의 모델 바인딩을 사용 하 여 데이터를 선택 하도록 데이터 컨트롤을 구성 하려면 설정 `SelectMethod` 속성 페이지의 코드에 메서드 이름입니다. 데이터 컨트롤의 페이지 수명 주기의 적절 한 시간에 메서드를 호출 하 고 자동으로 반환된 된 데이터를 바인딩합니다. 명시적으로 호출 하지 않아도 됩니다는 `DataBind` 메서드.

1. **솔루션 탐색기**오픈 *ProductList.aspx*합니다.
2. 이 태그를 사용 하 여 기존 태그를 바꿉니다.   

    [!code-aspx-csharp[Main](display_data_items_and_details/samples/sample1.aspx)]

이 코드를 사용 하는 **ListView** 라는 컨트롤 `productList` 제품을 전시 하기.

[!code-aspx-csharp[Main](display_data_items_and_details/samples/sample2.aspx)]

템플릿 및 스타일을 사용 하 여 정의 하는 방법을 **ListView** 컨트롤 데이터를 표시 합니다. 모든 반복 구조에서 데이터에 대 한 두는 것이 유용합니다. 하지만 이렇게 **ListView** 데이터베이스 데이터를 단순히 표시 하는 예제, 코드를 편집, 삽입 및 데이터를 삭제 하 고 정렬 및 데이터 페이지를 사용 하면 사용자가 없이 할 수도 있습니다.

설정 하 여는 `ItemType` 속성에는 **ListView** 컨트롤을 데이터 바인딩 식을 `Item` 수 컨트롤은 강력한 형식의. 이전 자습서에서 설명 했 듯이 지정 하는 등, IntelliSense 사용 하 여 개체 정보 항목을 선택할 수 있습니다는 `ProductName`:

![데이터를 표시할 항목 및 세부 정보-IntelliSense](display_data_items_and_details/_static/image1.png)

모델 바인딩을 지정 하 여도 되는 `SelectMethod` 값입니다. 이 값 (`GetProducts`) 코드에 추가 된 메서드에 해당 하는 다음 단계에서 제품을 전시 하기 지연 합니다.

### <a name="add-code-to-display-products"></a>제품을 표시 하는 코드를 추가 합니다.

이 단계에서는 채우는 코드를 추가 합니다 **ListView** 데이터베이스에서 제품 데이터를 사용 하 여 제어 합니다. 코드는 모든 제품 및 개별 범주 제품 표시를 지원 합니다.

1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 *ProductList.aspx* 선택한 후 **코드 보기**합니다.
2. 기존 코드를 대체 합니다 *ProductList.aspx.cs* 이 사용 하 여 파일:   

    [!code-csharp[Main](display_data_items_and_details/samples/sample3.cs)]

보여 주는이 코드를 `GetProducts` 메서드는 합니다 **ListView** 컨트롤의 `ItemType` 속성에서 참조를 *ProductList.aspx* 페이지. 특정 데이터베이스 범주에 결과 제한 하려면이 코드는 다음과 같이 설정 됩니다.는 `categoryId` 전달할 쿼리 문자열 값에서 값을 *ProductList.aspx* 때 페이지를 *ProductList.aspx* 페이지 탐색 됩니다. 합니다 `QueryStringAttribute` 클래스를 `System.Web.ModelBinding` 네임 스페이스는 쿼리 문자열 변수의 값을 검색 하는 `id`합니다. 이렇게 하면 모델 바인딩을에 쿼리 문자열에서 값을 바인딩하려는 `categoryId` 런타임에 매개 변수입니다.

유효한 범주를이 페이지에 쿼리 문자열로 전달 되 면 쿼리 결과가 일치 하는 데이터베이스에서 해당 제품에만 국한 된 `categoryId` 값입니다. 예를 들어 경우는 *ProductsList.aspx* 이것이 페이지 URL:


[!code-console[Main](display_data_items_and_details/samples/sample4.cmd)]

페이지에는 제품 데이터만 표시 됩니다. 여기서는 `categoryId` equals `1`합니다.

쿼리 문자열이 없으면이 포함 된 모든 제품 표시 되는 *ProductList.aspx* 페이지 라고 합니다.

이러한 메서드에 대 한 값의 소스 라고 *공급자 값* (같은 *QueryString*)를 사용 하는 값 공급자를 나타내는 매개 변수 특성 라고하고*공급자 특성 값* (같은 `id`). ASP.NET은 Web Forms 응용 프로그램의 쿼리 문자열, 쿠키, 폼 값, 컨트롤와 같은 뷰 상태, 세션 상태 프로필 속성에서 값 공급자 및 모든 사용자 입력의 일반적인 원본에 대 한 해당 특성을 포함합니다. 또한 사용자 지정 값 공급자를 작성할 수 있습니다.

### <a name="run-the-application"></a>애플리케이션 실행

모든 제품 또는 범주의 제품을 보려면 응용 프로그램을 실행 합니다.

1. 키를 눌러 **F5** 응용 프로그램을 실행 하려면 Visual Studio에서 합니다.  
   브라우저가 열리고 표시 합니다 *Default.aspx* 페이지입니다.

2. 선택 **자동차** 제품 범주 탐색 합니다.  
   합니다 *ProductList.aspx* 페이지에 표시만 표시 됩니다 **자동차** 범주 제품입니다. 이 자습서의 뒷부분에서 제품 세부 정보를 표시할 수 있습니다.  

    ![데이터를 표시할 항목 및 세부 정보-자동차](display_data_items_and_details/_static/image2.png)

3. 선택 **제품** 맨 위에 있는 탐색 메뉴에서.  
   하지만 마찬가지로 합니다 *ProductList.aspx* 이 이번 제품의 전체 목록을 표시 페이지가 표시 됩니다.   

    ![데이터를 표시할 항목 및 세부 정보-제품](display_data_items_and_details/_static/image3.png)

4. 브라우저를 닫고 Visual Studio로 돌아갑니다.

### <a name="add-a-data-control-to-display-product-details"></a>제품 세부 정보를 표시 하는 데이터 컨트롤 추가

다음으로 태그를 수정 합니다 *ProductDetails.aspx* 특정 제품 정보를 표시 하려면 이전 자습서에서 추가한 페이지입니다.

1. **솔루션 탐색기**오픈 *ProductDetails.aspx*합니다.

2. 이 태그를 사용 하 여 기존 태그를 바꿉니다.

    [!code-aspx-csharp[Main](display_data_items_and_details/samples/sample5.aspx)] 

    이 코드를 사용 하는 **FormView** 특정 제품 세부 정보를 표시 하는 컨트롤입니다. 이 태그에 데이터를 표시 하는 데 사용 하는 메서드와 마찬가지로 메서드를 사용 합니다 *ProductList.aspx* 페이지입니다. 합니다 **FormView** 컨트롤은 데이터 원본에서 한 번에 하나의 레코드를 표시 하는 데 사용 합니다. 사용 하는 경우는 **FormView** 컨트롤을 만든 템플릿을 표시 하 고 데이터 바인딩된 값을 편집 합니다. 이러한 템플릿에 컨트롤에 바인딩 식에 포함 하 고 폼의 모양 및 기능 정의 서식 지정 합니다.

데이터베이스에 이전 태그 연결 추가 코드가 필요 합니다.

1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 *ProductDetails.aspx* 을 클릭 한 다음 **코드 보기**합니다.  
   합니다 *ProductDetails.aspx.cs* 파일이 표시 됩니다.

2. 기존 코드를이 코드로 바꿉니다.   

    [!code-csharp[Main](display_data_items_and_details/samples/sample6.cs)]

이 코드는 검사는 "`productID`" 쿼리 문자열 값입니다. 유효한 쿼리 문자열 값이 있으면 일치 하는 제품이 표시 됩니다. 쿼리 문자열을 찾을 수 없으면 경우 해당 값에는 유효 하지 않습니다. 제품이 표시 됩니다.

### <a name="run-the-application"></a>애플리케이션 실행

제품 ID를 기반으로 이제 표시 된 개별 제품을 보려면 응용 프로그램을 실행할 수 있습니다.

1. 키를 눌러 **F5** 응용 프로그램을 실행 하려면 Visual Studio에서 합니다.  
   브라우저가 열리고 표시 합니다 *Default.aspx* 페이지입니다.

2. 선택 **배** 범주 탐색 합니다.  
   합니다 *ProductList.aspx* 페이지가 표시 됩니다.

3. 선택 **용지 재벌** 제품 목록에서.
   합니다 *ProductDetails.aspx* 페이지가 표시 됩니다.

    ![데이터를 표시할 항목 및 세부 정보-제품](display_data_items_and_details/_static/image4.png)
    
4. 브라우저를 닫습니다.


## <a name="additional-resources"></a>추가 자료

[모델 바인딩 및 web forms를 사용 하 여 데이터 검색 및 표시](../../presenting-and-managing-data/model-binding/retrieving-data.md)

## <a name="next-steps"></a>다음 단계

이 자습서에서는 태그 및 제품 및 제품 세부 정보를 표시 하는 코드를 추가 합니다. 강력한 형식의 데이터 컨트롤, 모델 바인딩 및 값 공급자에 대해 알아보았습니다. 다음 자습서에서는 Wingtip Toys 샘플 응용 프로그램에 쇼핑 카트에 추가 합니다. 

> [!div class="step-by-step"]
> [이전](ui_and_navigation.md)
> [다음](shopping-cart.md)
