---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
title: "데이터 표시 항목 및 세부 정보 | Microsoft Docs"
author: Erikre
description: "이 자습서 시리즈 것에 대 한 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 구축 하는 기초 알려 드리겠습니다 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/08/2014
ms.topic: article
ms.assetid: 64a491a8-0ed6-4c2f-9c1c-412962eb6006
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
msc.type: authoredcontent
ms.openlocfilehash: 809d7a9c21a3ddf5dfd07d079eb8fe0d1d81712d
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="display-data-items-and-details"></a>데이터 표시 항목 및 세부 정보
====================
으로 [Erik Reitan](https://github.com/Erikre)

[Wingtip Toys 샘플 프로젝트 (C#)를 다운로드](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자책 (PDF)를 다운로드 합니다.](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 이 자습서 시리즈 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 웹에 대 한 ASP.NET Web Forms 응용 프로그램을 구축 하는 기초 알려 드리겠습니다. Visual Studio 2013 [C# 소스 코드를 사용 하 여 프로젝트](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 이 자습서 시리즈를 함께 사용할 수 있습니다.


이 자습서에서는 데이터 항목 및 ASP.NET Web Forms 및 Entity Framework Code First를 사용 하 여 데이터 항목 정보를 표시 하는 방법을 설명 합니다. 이 자습서에서는 이전 자습서 "UI 및 탐색"를 바탕으로 하며 Wingtip 장난감 저장소 자습서 시리즈의 일부입니다. 이 자습서를 완료 하면 수에 제품을 볼 수는 *ProductsList.aspx* 페이지 및 개별 제품에 대 한 세부 정보는 *ProductDetails.aspx* 페이지.

## <a name="what-youll-learn"></a>학습 내용:

- 데이터베이스에서 제품을 표시 하는 데이터 컨트롤을 추가 하는 방법입니다.
- 선택한 데이터에 데이터 컨트롤을 연결 하는 방법.
- 데이터베이스에서 제품 세부 정보를 표시 하는 데이터 컨트롤을 추가 하는 방법입니다.
- 쿼리 문자열에서 값을 검색 값을 사용 하는 데이터베이스에서 검색 된 데이터를 제한 하는 방법.

### <a name="these-are-the-features-introduced-in-the-tutorial"></a>다음은 자습서에 도입 된 기능입니다.

- 모델 바인딩
- 값 공급자

## <a name="adding-a-data-control-to-display-products"></a>제품을 전시 하기 데이터 컨트롤 추가

서버 컨트롤에 데이터를 바인딩할 때 사용할 수는 몇 가지 옵션이 있습니다. 가장 일반적인 옵션에는 데이터 소스 컨트롤을 추가, 코드를 수동으로 추가 또는 모델 바인딩을 사용 하 여 포함 됩니다.

### <a name="using-a-data-source-control-to-bind-data"></a>데이터 소스 제어를 사용 하 여 데이터를 바인딩합니다.

데이터 소스 제어에 추가 데이터를 표시 하는 컨트롤에 데이터 소스 제어를 연결할 수 있습니다. 이 방법을 프로그래밍 방식을 사용 하지 않고 데이터 원본에 직접 서버 쪽 컨트롤을 선언적으로 연결할 수 있도록 합니다.

### <a name="coding-by-hand-to-bind-data"></a>데이터를 바인딩하려면 직접 코딩

추가 코드가 직접 관련 값을 읽기, null 값을 확인, 적절 한 형식으로 변환 하는 동안은 변환이 성공 했는지 여부를 확인 및 마지막으로, 쿼리에서 값을 사용 하 합니다. 데이터 액세스 논리에 대 한 모든 권한을 유지 해야 할 경우이 방법을 사용 합니다.

### <a name="using-model-binding-to-bind-data"></a>데이터를 바인딩하려면 바인딩 모델을 사용 하 여

모델 바인딩을 사용 하 여 훨씬 더 적은 코드를 사용 하 여 결과 바인딩할 수 있도록 하 고 응용 프로그램 전체에서 기능을 다시 사용할 수 있는 제공 합니다. 모델 바인딩은 풍부한, 데이터 바인딩 프레임 워크의 혜택을 유지 하면서 데이터 액세스 코드 중심 논리로 작업을 단순화 시키기 위한 것입니다.

## <a name="displaying-products"></a>제품 표시

이 자습서에서는 데이터를 바인딩할 모델 바인딩을 사용 합니다. 컨트롤의 데이터를 선택 하려면 모델 바인딩을 사용 하도록 데이터 제어를 구성 하려면 설정 `SelectMethod` 속성 페이지의 코드에 있는 메서드의 이름입니다. 데이터 컨트롤 페이지 수명 주기의 적절 한 시간에 메서드를 호출 하 고 자동으로 반환된 된 데이터를 바인딩합니다. 명시적으로 호출할 필요가 없습니다는 `DataBind` 메서드.

다음 단계를 사용 하 여에서 태그를 수정 합니다는 *ProductList.aspx* 페이지의 페이지는 제품을 표시할 수 있습니다.

1. **솔루션 탐색기**열고는 *ProductList.aspx* 페이지.
2. 기존 태그를 다음 태그로 바꿉니다.   

    [!code-aspx[Main](display_data_items_and_details/samples/sample1.aspx)]

사용 하 여이 코드는 **ListView** 는 제품을 전시 하기 "productList" 라는 컨트롤입니다.

[!code-aspx[Main](display_data_items_and_details/samples/sample2.aspx)]

**ListView** 컨트롤 템플릿 및 스타일을 사용 하 여 정의 하는 형식에 데이터를 표시 합니다. 모든 반복 구조에서 데이터에는 것이 유용합니다. 하지만이 **ListView** 예제 데이터는 데이터베이스, 사용자가 편집, 삽입 및 데이터를 삭제 하 고 정렬에 사용할 수 있습니다 및 코드 없이 모두 페이지 데이터를 보여 줍니다.

설정 하 여는 `ItemType` 속성에는 **ListView** 제어, 데이터 바인딩 식을 `Item` ´ ï ´ 컨트롤은 강력한 형식의 합니다. 이전 자습서에서 설명 했 듯이 IntelliSense를 사용 하 여 지정 하는 등 항목 개체의 세부 정보를 선택할 수 있습니다는 `ProductName`:

![데이터 표시 항목 및 세부 정보-IntelliSense](display_data_items_and_details/_static/image1.png)

모델 바인딩을 사용 하 여 지정할 수는 또한는 `SelectMethod` 값입니다. 이 값 (`GetProducts`) 메서드를 다음 단계에서 제품을 표시 하는 코드 숨김에 추가 합니다에 해당 됩니다.

### <a name="adding-code-to-display-products"></a>제품을 표시 하는 코드를 추가 합니다.

이 단계에서는 채우는 코드를 추가 합니다는 **ListView** 컨트롤에 데이터베이스에서 제품 데이터. 코드는 모든 제품을 표시 뿐만 아니라 개별 범주에서 보여 주는 제품을 지원 합니다.

1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 *ProductList.aspx* 클릭 하 고 **코드 보기**합니다.
2. 기존 코드는 *ProductList.aspx.cs* 를 다음 코드로 파일:   

    [!code-csharp[Main](display_data_items_and_details/samples/sample3.cs)]

보여 주는이 코드는 `GetProducts` 에서 참조 되는 메서드는 `ItemType` 의 속성은 **ListView** 컨트롤에 *ProductList.aspx* 페이지. 데이터베이스의 특정 범주에 결과 제한 하려면이 코드는 다음과 같이 설정 됩니다.는 `categoryId` 전달 되는 쿼리 문자열 값의 값은 *ProductList.aspx* 때 페이지는 *ProductList.aspx* 페이지는 이동 하 게 합니다. `QueryStringAttribute` 클래스에 `System.Web.ModelBinding` 네임 스페이스는 쿼리 문자열 변수 id의 값을 검색 하는 데 사용 됩니다. 이렇게 하면 모델을 쿼리 문자열에서 값을 연결할 하려고을 바인딩하는 `categoryId` 실행 시 매개 변수입니다.

쿼리 결과 일치 하는 데이터베이스에서 해당 제품으로 제한 됩니다 올바른 범주에는 페이지에 쿼리 문자열로 전달 되는 `categoryId` 값입니다. 예를 들어, 하는 경우 URL은 *ProductsList.aspx* 페이지는 다음:

[!code-console[Main](display_data_items_and_details/samples/sample4.cmd)]

페이지에는 제품의 데이터만 표시 됩니다. 여기서는 `category` equals `1`합니다.

탐색 하는 경우 포함 된 쿼리 문자열이 없는 경우는 *ProductList.aspx* 페이지, 모든 제품을 표시 됩니다.

이러한 방법에 대 한 값의 소스는 라고 *값 공급자* (같은 *QueryString*)를 사용 하는 값 공급자를 나타내는 매개 변수 특성 값으로 참조 되 고 공급자 특성 (예: "`id`"). ASP.NET은 Web Forms 응용 프로그램의 쿼리 문자열, 쿠키, 폼 값, 컨트롤와 같은 뷰 상태, 세션 상태 프로필 속성에 값 공급자 및 모든 사용자 입력의 일반적인 원본에 대 한 해당 특성을 포함합니다. 사용자 지정 값 공급자를 작성할 수 있습니다.

### <a name="running-the-application"></a>응용 프로그램 실행

모든 제품 또는 제품 범주별으로 제한 된 집합에만 볼 수는 어떻게 볼 수 있는 지금 응용 프로그램을 실행 합니다.

1. 에 **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 *Default.aspx* 페이지로 돌아간 후 선택 **브라우저에서 보기**합니다.  
 브라우저가 열리고 표시는 *Default.aspx* 페이지.
2. 선택 **자동차** 제품 범주 탐색 메뉴에서 합니다.  
 *ProductList.aspx* "Cars" 범주에 포함 된 제품만 표시 페이지가 표시 됩니다. 이 자습서의 뒷부분에 나오는 제품 세부 정보를 표시 합니다.  

    ![데이터 표시 항목 및 세부 정보-자동차](display_data_items_and_details/_static/image2.png)
3. 선택 **제품** 위쪽에 있는 탐색 메뉴에서 합니다.  
 다시,는 *ProductList.aspx* 페이지가 표시 되어 있지만이 현재 제품의 전체 목록을 보여 줍니다.   

    ![데이터 표시 항목 및 세부 정보-제품](display_data_items_and_details/_static/image3.png)
4. 브라우저를 닫고 Visual Studio로 돌아갑니다.

### <a name="adding-a-data-control-to-display-product-details"></a>제품 세부 정보를 표시 하는 데이터 컨트롤 추가

태그를 수정 하면서 간단한 다음으로 *ProductDetails.aspx* 페이지 개별 제품에 대 한 정보를 표시할 수 있도록 이전 자습서에서 추가한 페이지입니다.

1. **솔루션 탐색기**열고는 *ProductDetails.aspx* 페이지.
2. 기존 태그를 다음 태그로 바꿉니다.   

    [!code-aspx[Main](display_data_items_and_details/samples/sample5.aspx)]

이 코드에서는 사용 된 **FormView** 컨트롤을 개별 제품에 대 한 세부 정보를 표시 합니다. 에 데이터를 표시 하는 데 사용 되는 것과 같은 메서드를 사용 하는이 태그는 *ProductList.aspx* 페이지. **FormView** 컨트롤은 데이터 원본에서 한 번에 하나의 레코드를 표시 하는 데 사용 합니다. 사용 하는 경우는 **FormView** 컨트롤을 만들면 템플릿을 표시 하 고 데이터 바인딩된 값을 편집 합니다. 템플릿을 컨트롤을 포함할 바인딩 식 및 서식을 모양 및 폼의 기능을 정의 하는.

위의 태그를 데이터베이스에 연결 하려면 추가 코드를 추가 해야는 *ProductDetails.aspx* 코드입니다.

1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 *ProductDetails.aspx* 클릭 하 고 **코드 보기**합니다.  
 *ProductDetails.aspx.cs* 파일이 표시 됩니다.
2. 기존 코드를 다음 코드로 바꿉니다.   

    [!code-csharp[Main](display_data_items_and_details/samples/sample6.cs)]

이 코드는 검사는 "`productID`" 쿼리 문자열 값입니다. 올바른 쿼리 문자열 값이 있으면 일치 하는 제품이 표시 됩니다. 쿼리 문자열이 없으면 찾거나 쿼리 문자열 값이 올바르지 않습니다, 제품이 없으므로에 표시 됩니다는 *ProductDetails.aspx* 페이지.

### <a name="running-the-application"></a>응용 프로그램 실행

이제 표시 개별 제품을 확인 하려면 응용 프로그램을 실행할 수 있습니다는 제품의 id를 기반 합니다.

1. 키를 눌러 **F5** 응용 프로그램을 실행 하려면 Visual Studio에 있는 동안 합니다.  
 브라우저가 열리고 표시는 *Default.aspx* 페이지.
2. 범주 탐색 메뉴에서 "배"를 선택 합니다.  
 *ProductList.aspx* 페이지가 표시 됩니다.
3. 제품 목록에서 "용지 보트" 제품을 선택 합니다.  
 *ProductDetails.aspx* 페이지가 표시 됩니다.   

    ![데이터 표시 항목 및 세부 정보-제품](display_data_items_and_details/_static/image4.png)
4. 브라우저를 닫습니다.

## <a name="summary"></a>요약

이 자습서 시리즈의 태그 및 제품 목록을 표시 하 고 제품 세부 정보를 표시 하는 코드를 추가할 필요 합니다. 이 프로세스 중 강력한 형식의 데이터 컨트롤, 모델 바인딩 및 값 공급자에 대해 배웠습니다. 다음 자습서에서는 쇼핑 카트 Wingtip Toys 샘플 응용 프로그램에 추가 합니다.

## <a name="additional-resources"></a>추가 리소스

[검색 및 모델 바인딩 및 web forms를 사용 하 여 데이터를 표시 합니다.](../../presenting-and-managing-data/model-binding/retrieving-data.md)

>[!div class="step-by-step"]
[이전](ui_and_navigation.md)
[다음](shopping-cart.md)
