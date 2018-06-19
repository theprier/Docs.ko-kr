---
uid: web-forms/overview/data-access/basic-reporting/declarative-parameters-cs
title: 선언적 매개 변수 (C#) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 DetailsView 컨트롤에 표시할 데이터를 선택 하는 하드 코드 된 값으로 설정 하는 매개 변수를 사용 하는 방법을 설명 하겠습니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/31/2010
ms.topic: article
ms.assetid: 603c9bd3-b895-4ec6-853b-0c81ff36d580
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/basic-reporting/declarative-parameters-cs
msc.type: authoredcontent
ms.openlocfilehash: 840630852d28f49f4f4387f1d2cc6b275b468fc2
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30875941"
---
<a name="declarative-parameters-c"></a>선언적 매개 변수 (C#)
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_5_CS.exe) 또는 [PDF 다운로드](declarative-parameters-cs/_static/datatutorial05cs1.pdf)

> 이 자습서에서는 DetailsView 컨트롤에 표시할 데이터를 선택 하는 하드 코드 된 값으로 설정 하는 매개 변수를 사용 하는 방법을 설명 하겠습니다.


## <a name="introduction"></a>소개

에 [지난 자습서](displaying-data-with-the-objectdatasource-cs.md) 호출한 ObjectDataSource 컨트롤에 바인딩된 컨트롤을 GridView, DetailsView, 및 FormView를 사용 하 여 데이터 표시에서 `GetProducts()` 에서 메서드는 `ProductsBLL` 클래스입니다. `GetProducts()` Northwind 데이터베이스에서 레코드를 모두 입력 하는 강력한 형식의 DataTable을 반환 하는 메서드 `Products` 테이블입니다. `ProductsBLL` 제품-의 정당한 하위 집합을 반환 하기 위한 추가 메서드를 포함 하는 클래스 `GetProductByProductID(productID)`, `GetProductsByCategoryID(categoryID)`, 및 `GetProductsBySupplierID(supplierID)`합니다. 이러한 세 가지 메서드는 반환 된 제품 정보를 필터링 하는 방법을 나타내는 입력된 매개 변수를 기대 합니다.

입력된 매개 변수를 예상 하는 메서드를 호출할 수 있지만 이러한 매개 변수에 대 한 값에서 제공 하는 위치를 지정 해야 하므로 작업을 수행 하려면는 ObjectDataSource는 사용할 수 있습니다. 매개 변수 값을 하드 코딩할 수 있습니다 또는 다양 한 동적를 비롯 한 원본에서에서 가져올 수 있습니다: 쿼리 문자열 값, 세션 변수는 페이지 또는 다른 웹 컨트롤의 속성 값입니다.

이 자습서에 대 한 하드 코드 된 값으로 설정 하는 매개 변수를 사용 하는 방법을 설명 하 여 시작 하겠습니다. 특정 제품, 즉 Chef 한 100 수프를가 하는 방법에 대 한 정보를 표시 하는 페이지에는 DetailsView 추가에서 살펴보게 특히는 `ProductID` 5입니다. 다음으로, 웹 컨트롤에 따라 매개 변수 값을 설정 하는 방법을 살펴보겠습니다. 특히, 사용자는 해당 국가에 상주 하는 공급 업체의 목록을 보려면 단추를 클릭 하는 국가에 입력 텍스트 상자를 사용 합니다.

## <a name="using-a-hard-coded-parameter-value"></a>하드 코드 된 매개 변수 값을 사용 하 여

첫 번째 예에 대 한 DetailsView 컨트롤을 추가 하 여 시작 된 `DeclarativeParams.aspx` 페이지에 `BasicReporting` 폴더입니다. DetailsView의 스마트 태그에서 선택 &lt;새 데이터 원본을&gt; 드롭다운 목록에서 나열 하 고는 ObjectDataSource를 추가 하려면 선택 합니다.


[![페이지에는 ObjectDataSource 추가](declarative-parameters-cs/_static/image2.png)](declarative-parameters-cs/_static/image1.png)

**그림 1**: 페이지에는 ObjectDataSource 추가 ([전체 크기 이미지를 보려면 클릭](declarative-parameters-cs/_static/image3.png))


ObjectDataSource 컨트롤의 데이터 소스 선택 마법사가 자동으로 시작 됩니다. 선택 된 `ProductsBLL` 마법사의 첫 번째 화면에서 클래스입니다.


[![ProductsBLL 클래스 선택](declarative-parameters-cs/_static/image5.png)](declarative-parameters-cs/_static/image4.png)

**그림 2**: 선택 된 `ProductsBLL` 클래스 ([전체 크기 이미지를 보려면 클릭](declarative-parameters-cs/_static/image6.png))


사용 하려는 특정 제품에 대 한 정보를 표시 하는 데는 `GetProductByProductID(productID)` 메서드.


[![GetProductByProductID(productID) 방법을 선택 합니다.](declarative-parameters-cs/_static/image8.png)](declarative-parameters-cs/_static/image7.png)

**그림 3**: 선택 된 `GetProductByProductID(productID)` 메서드 ([전체 크기 이미지를 보려면 클릭](declarative-parameters-cs/_static/image9.png))


매개 변수를 포함 하는 선택한 메서드를 매개 변수에 사용할 값을 정의 하는 요청한 여기서 마법사에 대 한 자세한 화면은 합니다. 왼쪽의 목록은 모든 선택한 방법에 대 한 매개 변수입니다. 에 대 한 `GetProductByProductID(productID)` 하나만 `productID`합니다. 오른쪽에 선택한 매개 변수에 대 한 값을 지정할 수 있습니다. 매개 변수 소스 드롭 다운 목록에서 매개 변수 값에 대 한 가능한 다양 한 소스를 열거합니다. 5에 대 한 하드 코드 된 값을 지정 하는 데는 `productID` 매개 변수를 매개 변수 소스 없음로 그대로 두고 DefaultValue 텍스트 상자에 5를 입력 합니다.


[![Hard-Coded 매개 변수 값의 5에 사용할 매개 변수 productID](declarative-parameters-cs/_static/image11.png)](declarative-parameters-cs/_static/image10.png)

**그림 4**: A Hard-Coded 매개 변수 값의 5에 사용할는 `productID` 매개 변수 ([전체 크기 이미지를 보려면 클릭](declarative-parameters-cs/_static/image12.png))


ObjectDataSource 컨트롤의 선언적 태그 데이터 소스 구성 마법사를 완료 한 후에 포함 되어는 `Parameter` 개체는 `SelectParameters` 컬렉션에 정의 된 메서드에 필요한 입력된 매개 변수 마다는 `SelectMethod` 속성입니다. 이 예제에서는 메서드에 단일 입력된 매개 변수일 뿐, 이후 `parameterID`, 여기에 하나의 항목이 있습니다. `SelectParameters` 컬렉션에서 파생 되는 클래스를 포함할 수는 `Parameter` 클래스에 `System.Web.UI.WebControls` 네임 스페이스입니다. 하드 코딩 된 매개 변수는 기본 값에 대 한 `Parameter` 클래스를 사용 하지만 다른 매개 변수에 대 한 소스 옵션 파생 `Parameter` 클래스가 사용 됩니다; 만들 수도 있습니다 직접 [사용자 지정 매개 변수 형식](http://www.leftslipper.com/ShowFaq.aspx?FaqId=11), 필요한 경우.

[!code-aspx[Main](declarative-parameters-cs/samples/sample1.aspx)]

> [!NOTE]
> 컴퓨터에 선언 태그 따라 했다면 보면이 시점에서 년 5 월에 대 한 값이 포함는 `InsertMethod`, `UpdateMethod`, 및 `DeleteMethod` 속성으로 `DeleteParameters`합니다. ObjectDataSource의 데이터 소스 선택 마법사에서 메서드를 자동으로 지정 된 `ProductBLL` 를 사용 하 여 삽입, 업데이트 및 삭제에 대 한 명시적으로 취소 된 아웃 하지 않는 한 수에 포함 될 있습니다 위의 태그입니다.


이 페이지를 방문 데이터 웹 컨트롤 호출 하는 ObjectDataSource `Select` 메서드를 호출 합니다는 `ProductsBLL` 클래스의 `GetProductByProductID(productID)` 에 하드 코드 된 값에 대 한 5 사용 하 여 메서드는 `productID` 입력된 매개 변수입니다. 강력한 형식의 메서드는 반환 `ProductDataTable` 수프 Chef 한 100에 대 한 정보가 포함 된 단일 행을 포함 하는 개체 (인 제품 `ProductID` 5).


[![정보에 대 한 Chef 한 100 수프 표시 됩니다.](declarative-parameters-cs/_static/image14.png)](declarative-parameters-cs/_static/image13.png)

**그림 5**: 정보에 대 한 Chef 한 100 수프 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](declarative-parameters-cs/_static/image15.png))


## <a name="setting-the-parameter-value-to-the-property-value-of-a-web-control"></a>웹 컨트롤의 속성 값을 매개 변수 값 설정

페이지에서 웹 컨트롤의 값을 기준으로 ObjectDataSource의 매개 변수 값을 설정할 수도 있습니다. 이 설명 하기는 사용자가 지정한 국가에 있는 되는 공급자를 모두 나열 하는 GridView 죠. 사용자 국가 이름을 입력할 수 있는 페이지에 텍스트 상자를 추가 하 여이 시작을 수행 합니다. 이 텍스트 상자 컨트롤의 설정 `ID` 속성을 `CountryName`합니다. Button 웹 컨트롤을 추가할 수도 있습니다.


[![ID CountryName 사용 하 여 페이지에 텍스트 상자를 추가 합니다.](declarative-parameters-cs/_static/image17.png)](declarative-parameters-cs/_static/image16.png)

**그림 6**: 텍스트 상자를 사용 하 여 페이지에 추가 `ID` `CountryName` ([전체 크기 이미지를 보려면 클릭](declarative-parameters-cs/_static/image18.png))


다음으로, 페이지 및 스마트 태그에서 GridView 추가 새 ObjectDataSource를 추가 하려면 선택 합니다. 공급 업체 정보 선택 표시 하는 데는 `SuppliersBLL` 마법사의 첫 번째 화면에서 클래스입니다. 두 번째 화면에서 선택 된 `GetSuppliersByCountry(country)` 메서드.


[![GetSuppliersByCountry(country) 방법을 선택 합니다.](declarative-parameters-cs/_static/image20.png)](declarative-parameters-cs/_static/image19.png)

**그림 7**: 선택 된 `GetSuppliersByCountry(country)` 메서드 ([전체 크기 이미지를 보려면 클릭](declarative-parameters-cs/_static/image21.png))


이후는 `GetSuppliersByCountry(country)` 메서드에 입력된 매개 변수는, 마법사 매개 변수 값을 선택 하기 위한 최종 화면을 다시 한 번 포함 합니다. 이 이번에는 제어 매개 변수 소스를 설정 합니다. 이 페이지에 컨트롤의 이름으로 ControlID 드롭 다운 목록을 채울합니다 선택 된 `CountryName` 목록에서 제어 합니다. 해당 페이지를 처음으로 방문는 `CountryName` 결과가 반환 되 고 아무 것도 표시 되므로 TextBox 비어 있게 됩니다. 기본적으로 몇 가지 결과 표시 하려는 DefaultValue textbox를 적절 하 게 설정 합니다.


[![매개 변수 값 CountryName 컨트롤 값으로 설정](declarative-parameters-cs/_static/image23.png)](declarative-parameters-cs/_static/image22.png)

**그림 8**: 매개 변수 값으로 설정 된 `CountryName` 컨트롤 값 ([전체 크기 이미지를 보려면 클릭](declarative-parameters-cs/_static/image24.png))


ObjectDataSource의 선언적 태그는 첫 번째 예제에서 약간 다릅니다.를 사용 하는 [ControlParameter](https://msdn.microsoft.com/library/system.web.ui.webcontrols.controlparameter.aspx) 표준 대신 `Parameter` 개체입니다. A `ControlParameter` 추가 속성이 지정 하는 `ID` 웹 컨트롤 및 속성 값을 매개 변수로 사용 (`PropertyName`). 데이터 소스 구성 마법사가 하는 텍스트 상자에 대 한 म 합니다 가능성이를 사용할지 결정 하는 `Text` 매개 변수 값에 대 한 속성입니다. 그러나 웹 컨트롤의 다른 속성 값을 사용 하려는 경우 변경할 수 있습니다는 `PropertyName` 여기서 또는 마법사에 있는 "고급 속성 표시" 링크를 클릭 하 여 값입니다.

[!code-aspx[Main](declarative-parameters-cs/samples/sample2.aspx)]

처음으로 페이지를 방문 하는 경우는 `CountryName` TextBox 비어 있습니다. ObjectDataSource의 `Select` 메서드를 여전히 호출한 GridView 하지만 값 `null` 에 전달 되는 `GetSuppliersByCountry(country)` 메서드. TableAdapter 변환는 `null` 데이터베이스로 `NULL` 값 (`DBNull.Value`), 하지만 사용 하는 쿼리는 `GetSuppliersByCountry(country)` 메서드는 반환 되지 않는 작성 됩니다 때 값를 `NULL` 는 에대한값을지정`@CategoryID`매개 변수입니다. 즉, 공급 업체 반환 됩니다.

그러나 방문자 국가에 입력 하 고를 다시 게시는 ObjectDataSource의 공급 업체 표시 단추를 클릭 한 후 `Select` 전달 TextBox 컨트롤의 메서드는 고치거 `Text` 값는 `country` 매개 변수입니다.


[![캐나다에서 공급 업체에서 제공 같습니다.](declarative-parameters-cs/_static/image26.png)](declarative-parameters-cs/_static/image25.png)

**그림 9**: 캐나다에서 공급 하는 것이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](declarative-parameters-cs/_static/image27.png))


## <a name="showing-all-suppliers-by-default"></a>기본적으로 모든 공급자를 표시합니다.

대신 보다 먼저 페이지를 볼 때 공급 업체 중 없음 표시 하려는 표시 *모든* , 처음에 공급 업체 목록 국가 이름 텍스트 상자에 입력 하 여 축소 수 있도록 허용 합니다. TextBox 비어 있을 때는 `SuppliersBLL` 클래스의 `GetSuppliersByCountry(country)` 메서드에 전달 되는 `null` 값에 대 한 해당 *`country`* 입력된 매개 변수입니다. 이 `null` 다음 값이 전달에 DAL `GetSupplierByCountry(country)` 메서드를 데이터베이스로 변환 됩니다 `NULL` 에 대 한 값은 `@Country` 다음 쿼리에서 매개 변수:

[!code-sql[Main](declarative-parameters-cs/samples/sample3.sql)]

식 `Country = NULL` 항상 False를 반환 레코드에 대해서도 갖는 `Country` 열에는 `NULL` 값; 따라서 레코드가 반환 됩니다.

반환할 *모든* TextBox 국가 비어 있을 때 공급 업체 म을 강화할 수는 `GetSuppliersByCountry(country)` 메서드를 호출할 BLL에는 `GetSuppliers()` 메서드 해당 국가 매개 변수가 `null` 는 DAL을 호출 하 고 `GetSuppliersByCountry(country)` 그렇지 않으면 사용 되는 메서드. 아무런 영향의 국가 매개 변수가 포함 되는 경우 국가가 지정 하는 모든 공급 업체 및 공급 업체의 적절 한 하위 집합을 반환 합니다.

변경 된 `GetSuppliersByCountry(country)` 에서 메서드는 `SuppliersBLL` 다음과 클래스:

[!code-csharp[Main](declarative-parameters-cs/samples/sample4.cs)]

이러한 변경으로 인해는 `DeclarativeParams.aspx` 모든 공급 업체를 처음 방문할 때 페이지 표시 (또는 때마다는 `CountryName` TextBox 비어).


[![모든 공급 업체 이제 기본적으로 표시 됩니다.](declarative-parameters-cs/_static/image29.png)](declarative-parameters-cs/_static/image28.png)

**그림 10**: 모든 공급 업체는 이제 기본적으로 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](declarative-parameters-cs/_static/image30.png))


## <a name="summary"></a>요약

입력된 매개 변수가 있는 메서드를 사용 하려면 ObjectDataSource의에 매개 변수에 대 한 값을 지정 해야 `SelectParameters` 컬렉션입니다. 다른 형식의 매개 변수를 서로 다른 원본에서 가져올 매개 변수 값이 허용 됩니다. 하드 코드 된 값을 사용 하 여 기본 매개 변수 유형은 하지만 (쉽고 코드 줄을 없이)와 마찬가지로 매개 변수 값에서 얻을 수 있습니다 쿼리 문자열, 세션 변수, 쿠키 및 웹 컨트롤 페이지에도 사용자가 입력 한 값.

여기서이 자습서에서 살펴본 예에서는 선언적 매개 변수 값을 사용 하는 방법을 보여 줍니다. 그러나 경우 등에서 현재 날짜 및 시간을 사용할 수 없는 매개 변수 소스는 데 사용 해야 하는 경우가 또는 경우 사이트를 사용 하 여 멤버 자격, 방문자의 사용자 ID가 있습니다. 이러한 시나리오에 설정할 수 있습니다는 ObjectDataSource 하기 전에 프로그래밍 방식으로 매개 변수 값의 기본 개체의 메서드를 호출 합니다. 이 수행 하는 방법을 살펴보려는 [다음 자습서](programmatically-setting-the-objectdatasource-s-parameter-values-cs.md)합니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Hilton Giesenow 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](displaying-data-with-the-objectdatasource-cs.md)
> [다음](programmatically-setting-the-objectdatasource-s-parameter-values-cs.md)
