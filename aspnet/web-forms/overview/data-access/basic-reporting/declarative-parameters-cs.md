---
uid: web-forms/overview/data-access/basic-reporting/declarative-parameters-cs
title: 선언적 매개 변수 (C#) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 DetailsView 컨트롤에서 표시할 데이터를 선택 하려면 하드 코드 된 값으로 설정 하는 매개 변수를 사용 하는 방법을 설명할 것입니다.
ms.author: aspnetcontent
ms.date: 03/31/2010
ms.assetid: 603c9bd3-b895-4ec6-853b-0c81ff36d580
msc.legacyurl: /web-forms/overview/data-access/basic-reporting/declarative-parameters-cs
msc.type: authoredcontent
ms.openlocfilehash: 06577628d2b502df2854a83af564a0c0d402e9bd
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37839427"
---
<a name="declarative-parameters-c"></a>선언적 매개 변수 (C#)
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_5_CS.exe) 또는 [PDF 다운로드](declarative-parameters-cs/_static/datatutorial05cs1.pdf)

> 이 자습서에서는 DetailsView 컨트롤에서 표시할 데이터를 선택 하려면 하드 코드 된 값으로 설정 하는 매개 변수를 사용 하는 방법을 설명할 것입니다.


## <a name="introduction"></a>소개

에 [마지막 자습서](displaying-data-with-the-objectdatasource-cs.md) 호출한 ObjectDataSource 컨트롤에 바인딩된 컨트롤을 GridView, FormView DetailsView를 사용 하 여 데이터 표시에 대해 살펴보았습니다 합니다 `GetProducts()` 메서드에서 `ProductsBLL` 클래스. 합니다 `GetProducts()` 메서드는 Northwind 데이터베이스에서 레코드를 모두 채워집니다 강력한 형식화 된 DataTable을 반환 `Products` 테이블입니다. 합니다 `ProductsBLL` 제품-반환 단순히 하위 집합에 대 한 추가 메서드를 포함 하는 클래스 `GetProductByProductID(productID)`를 `GetProductsByCategoryID(categoryID)`, 및 `GetProductsBySupplierID(supplierID)`합니다. 이러한 세 가지 메서드는 반환 된 제품 정보를 필터링 하는 방법을 나타내는 입력된 매개 변수를 기대 합니다.

입력된 매개 변수를 예상 하는 메서드를 호출할 수 있지만 이러한 매개 변수 값에서 발생 한 위치 지정 해야 하므로 작업을 수행 하려면 ObjectDataSource는 사용할 수 있습니다. 매개 변수 값을 하드 코딩 될 수 있습니다 또는 다양 한를 비롯 한 동적 원본에서에서 가져올 수 있습니다: 쿼리 문자열 값으로 세션 변수 페이지 또는 다른 웹 컨트롤의 속성 값입니다.

이 자습서에 대 한 하드 코드 된 값으로 설정 하는 매개 변수를 사용 하는 방법을 보여 주는를 시작 하겠습니다. 특정 제품, 즉 Chef 한 100% 파인애플 조합에 대 한 정보를 표시 하는 페이지에는 DetailsView 추가 살펴보겠습니다 구체적으로 `ProductID` 5입니다. 다음으로, 웹 컨트롤을 기반으로 매개 변수 값을 설정 하는 방법을 살펴보겠습니다. 특히 사용자가 입력 되는 국가에 상주 하는 공급 업체의 목록을 보려면 단추를 클릭 한 국가에서 텍스트 상자를 사용 하겠습니다.

## <a name="using-a-hard-coded-parameter-value"></a>하드 코드 된 매개 변수 값을 사용 하 여

첫 번째 예를 들어 DetailsView 컨트롤을 추가 하 여 시작 합니다 `DeclarativeParams.aspx` 페이지에 `BasicReporting` 폴더입니다. DetailsView의 스마트 태그에서 선택 &lt;새 데이터 원본을&gt; 드롭다운 목록에서 나열 하 고 ObjectDataSource를 추가 하려면 선택 합니다.


[![ObjectDataSource를 페이지에 추가 합니다.](declarative-parameters-cs/_static/image2.png)](declarative-parameters-cs/_static/image1.png)

**그림 1**: 페이지에는 ObjectDataSource 추가 ([큰 이미지를 보려면 클릭](declarative-parameters-cs/_static/image3.png))


ObjectDataSource 컨트롤의 데이터 소스 선택 마법사가 자동으로 시작 됩니다. 선택 된 `ProductsBLL` 마법사의 첫 번째 화면에서 클래스입니다.


[![ProductsBLL 클래스를 선택 합니다.](declarative-parameters-cs/_static/image5.png)](declarative-parameters-cs/_static/image4.png)

**그림 2**: 선택 된 `ProductsBLL` 클래스 ([클릭 하 여 큰 이미지 보기](declarative-parameters-cs/_static/image6.png))


사용 하려는 특정 제품에 대 한 정보를 표시 하려고 하므로 `GetProductByProductID(productID)` 메서드.


[![GetProductByProductID(productID) 메서드를 선택 합니다.](declarative-parameters-cs/_static/image8.png)](declarative-parameters-cs/_static/image7.png)

**그림 3**: 선택 된 `GetProductByProductID(productID)` 메서드 ([클릭 하 여 큰 이미지 보기](declarative-parameters-cs/_static/image9.png))


선택한 메서드 매개 변수를 포함 하므로 매개 변수에 사용할 값을 정의 하는 질문 하는 마법사에 대 한 자세한 화면씩 방법이 있습니다. 왼쪽의 목록에 선택한 메서드에 대 한 매개 변수를 모두 나타납니다. 에 대 한 `GetProductByProductID(productID)` 하나만 `productID`합니다. 오른쪽에 선택한 매개 변수의 값을 지정할 수 있습니다. 매개 변수 원본 드롭다운 목록에 매개 변수 값에 대 한 가능한 다양 한 원본을 열거합니다. 5에 대 한 하드 코드 된 값을 지정 하려고 하므로 `productID` 매개 변수를 None으로 매개 변수 원본을 그대로 두려면 enter 5 DefaultValue 텍스트 상자에 붙여넣습니다.


[![Hard-Coded 매개 변수 값의 5에 사용할 매개 변수 productID](declarative-parameters-cs/_static/image11.png)](declarative-parameters-cs/_static/image10.png)

**그림 4**: A Hard-Coded 매개 변수 값의 5에 사용할 합니다 `productID` 매개 변수 ([클릭 하 여 큰 이미지 보기](declarative-parameters-cs/_static/image12.png))


ObjectDataSource 컨트롤의 선언적 태그 데이터 소스 구성 마법사를 완료 한 후에 포함 되어는 `Parameter` 개체를 `SelectParameters` 컬렉션에 정의 된 메서드에 필요한 입력된 매개 변수의 각는 `SelectMethod` 속성입니다. 이 예제에서는 메서드에서 방금 단일 입력된 매개 변수를 예상 하므로 `parameterID`, 여기에 하나의 항목이 있습니다. 합니다 `SelectParameters` 컬렉션에서 파생 되는 모든 클래스를 포함할 수는 `Parameter` 클래스를 `System.Web.UI.WebControls` 네임 스페이스입니다. 하드 코드 된 매개 변수 값은 기본에 대 한 `Parameter` 클래스를 사용 하지만 다른 매개 변수에 대 한 원본 옵션 파생 `Parameter` 클래스는; 만들 수도 있습니다 고유한 [사용자 지정 매개 변수 형식](http://www.leftslipper.com/ShowFaq.aspx?FaqId=11), 필요한 경우.

[!code-aspx[Main](declarative-parameters-cs/samples/sample1.aspx)]

> [!NOTE]
> 자신의 컴퓨터에 선언적 태그 따라 했다면 보면이 시점에 대 한 값을 포함할 수 있습니다는 `InsertMethod`, `UpdateMethod`, 및 `DeleteMethod` 속성인 뿐만 `DeleteParameters`합니다. ObjectDataSource의 데이터 소스 선택 마법사에서 메서드를 자동으로 지정 된 `ProductBLL` 아웃 된 명시적으로 지울 수 하지 않는 한 이러한에서는에 포함 될 있도록 위의 태그 삽입, 업데이트 및 삭제에 사용할 합니다.


데이터 웹 컨트롤은 ObjectDataSource의이 페이지를 방문 하는 경우 호출 `Select` 메서드를 호출 합니다 `ProductsBLL` 클래스의 `GetProductByProductID(productID)` 5에 대 한 하드 코드 된 값을 사용 하는 메서드를 `productID` 입력된 매개 변수. 강력한 형식의 메서드는 반환 `ProductDataTable` Chef 한 100% 파인애플 조합에 대 한 정보를 사용 하 여 단일 행이 들어 있는 개체 (사용 하 여 제품 `ProductID` 5).


[![정보에 대 한 Chef 한 100 수프 표시 됩니다.](declarative-parameters-cs/_static/image14.png)](declarative-parameters-cs/_static/image13.png)

**그림 5**: 정보에 대 한 Chef 한 100 수프 표시 됩니다 ([큰 이미지를 보려면 클릭](declarative-parameters-cs/_static/image15.png))


## <a name="setting-the-parameter-value-to-the-property-value-of-a-web-control"></a>웹 컨트롤의 속성 값을 매개 변수 값 설정

페이지의 웹 컨트롤의 값을 기준으로 ObjectDataSource의 매개 변수 값을 설정할 수도 있습니다. 이 예의 사용자가 지정한 국가에 있는 공급 업체를 모두 나열 하는 GridView 보겠습니다. 사용자 국가 이름을 입력할 수 있는 페이지에 텍스트를 추가 하 여이 시작을 수행 합니다. 이 텍스트 상자 컨트롤을 설정 `ID` 속성을 `CountryName`입니다. 또한 단추 웹 컨트롤을 추가 합니다.


[![페이지 ID CountryName에 입력란을 추가 합니다.](declarative-parameters-cs/_static/image17.png)](declarative-parameters-cs/_static/image16.png)

**그림 6**: 텍스트 상자를 사용 하 여 페이지에 추가 `ID` `CountryName` ([클릭 하 여 큰 이미지 보기](declarative-parameters-cs/_static/image18.png))


다음으로, 페이지 및 스마트 태그에서 GridView를 추가할 새 ObjectDataSource를 추가 하려면 선택 합니다. 공급 업체 정보 선택 표시 하려고 하므로 `SuppliersBLL` 마법사의 첫 번째 화면에서 클래스입니다. 두 번째 화면에서 선택 된 `GetSuppliersByCountry(country)` 메서드.


[![GetSuppliersByCountry(country) 메서드를 선택 합니다.](declarative-parameters-cs/_static/image20.png)](declarative-parameters-cs/_static/image19.png)

**그림 7**: 선택 된 `GetSuppliersByCountry(country)` 메서드 ([클릭 하 여 큰 이미지 보기](declarative-parameters-cs/_static/image21.png))


이후를 `GetSuppliersByCountry(country)` 메서드는 입력된 매개 변수, 마법사는 매개 변수 값을 선택 하기 위한 최종 화면에 다시 한 번 포함 되어 있습니다. 이 이번에는 컨트롤에 매개 변수 소스를 설정 합니다. 이 페이지에서 컨트롤의 이름 사용 하 여 ControlID 드롭다운 목록을 채우는합니다 선택 된 `CountryName` 목록에서 제어 합니다. 해당 페이지를 처음으로 방문 합니다 `CountryName` 결과가 반환 되 고 아무 것도 표시 되므로 텍스트 상자를 비어 있게 됩니다. 기본적으로 일부 결과 표시 하려는 경우 DefaultValue 입력란을 적절 하 게 설정 합니다.


[![CountryName 컨트롤 값 매개 변수 값을 설정 합니다.](declarative-parameters-cs/_static/image23.png)](declarative-parameters-cs/_static/image22.png)

**그림 8**: 매개 변수 값을 설정 합니다 `CountryName` 제어 값 ([클릭 하 여 큰 이미지 보기](declarative-parameters-cs/_static/image24.png))


ObjectDataSource의 선언 태그를 첫 번째 예제에서 약간 다릅니다.를 사용 하는 [ControlParameter](https://msdn.microsoft.com/library/system.web.ui.webcontrols.controlparameter.aspx) 표준 대신 `Parameter` 개체입니다. A `ControlParameter` 지정 하는 추가 속성에는 `ID` 웹 컨트롤 및 속성 값을 매개 변수로 사용 (`PropertyName`). 데이터 소스 구성 마법사가 정도로 장치가 지능적이 지 결정 하는 텍스트 상자에 대 한 됩니다 것를 사용 하 여 `Text` 매개 변수 값에 대 한 속성. 그러나 웹 컨트롤의 다른 속성 값을 사용 하려는 경우 변경할 수 있습니다는 `PropertyName` 여기 또는 마법사에서 "고급 속성 표시" 링크를 클릭 하 여 값입니다.

[!code-aspx[Main](declarative-parameters-cs/samples/sample2.aspx)]

처음으로 페이지를 방문할 때를 `CountryName` 텍스트 상자가 비어 있습니다. ObjectDataSource의 `Select` 메서드를 여전히 호출한 GridView 있지만 `null` 에 전달 되는 `GetSuppliersByCountry(country)` 메서드. TableAdapter 변환 합니다 `null` 데이터베이스로 `NULL` 값 (`DBNull.Value`)를 하지만 사용 하는 쿼리를 `GetSuppliersByCountry(country)` 메서드는 반환 되지 않는 모든 기록 됩니다 때 값을 `NULL` 값을 지정 합니다 `@CategoryID`매개 변수입니다. 즉, 공급 업체 반환 됩니다.

그러나 방문자 한 국가에서 입력 하 고, 다시 게시 ObjectDataSource의 시킬 공급자 표시 단추를 클릭 `Select` 메서드는 다시 쿼리되어, TextBox 컨트롤의 전달 `Text` 값을 `country` 매개 변수입니다.


[![캐나다에서 해당 공급 업체 나와 있습니다.](declarative-parameters-cs/_static/image26.png)](declarative-parameters-cs/_static/image25.png)

**그림 9**: 이러한 Suppliers 캐나다에서 표시 됩니다 ([큰 이미지를 보려면 클릭](declarative-parameters-cs/_static/image27.png))


## <a name="showing-all-suppliers-by-default"></a>기본적으로 모든 공급자를 표시합니다.

대신 보다 먼저 페이지를 볼 때 공급자 하나도 표시 하려는 경우 표시 *모든* 를 국가 이름 텍스트 상자에 입력 하 여 목록을 줄이려면 사용자가 처음에 공급 합니다. 텍스트 비어 있는 경우는 `SuppliersBLL` 클래스의 `GetSuppliersByCountry(country)` 메서드에 전달 되는 `null` 값 해당 *`country`* 입력된 매개 변수. 이 `null` 값은 전달 DAL의에 `GetSupplierByCountry(country)` 메서드를 데이터베이스로 변환 됩니다 `NULL` 에 대 한 값을 `@Country` 다음 쿼리에서 매개 변수:

[!code-sql[Main](declarative-parameters-cs/samples/sample3.sql)]

식을 `Country = NULL` 항상 False를 반환 레코드에 대해서도 갖는 `Country` 열에는 `NULL` 값; 따라서 레코드가 반환 됩니다.

반환할 *모든* 국가 TextBox 비어 있는 경우 공급 업체 수 살펴보면서 합니다 `GetSuppliersByCountry(country)` 메서드를 호출 하는 BLL에는 `GetSuppliers()` 해당 국가 매개 변수가 메서드 `null` 는 DAL을 호출할 수 `GetSuppliersByCountry(country)` 그렇지 않으면 사용 되는 메서드. 이 효과 국가 매개 변수가 포함 된 경우 없는 국가 지정 하는 모든 공급 업체 및 공급 업체의 적절 한 하위 집합을 반환 해야 합니다.

변경 된 `GetSuppliersByCountry(country)` 의 메서드는 `SuppliersBLL` 다음 클래스:

[!code-csharp[Main](declarative-parameters-cs/samples/sample4.cs)]

이 변경 합니다 `DeclarativeParams.aspx` 처음 방문한 경우 공급 업체의 모든 페이지에 표시 (또는 때마다를 `CountryName` TextBox 비어 있습니다.).


[![모든 공급 업체는 이제 기본적으로 표시](declarative-parameters-cs/_static/image29.png)](declarative-parameters-cs/_static/image28.png)

**그림 10**: 모든 공급 업체는 이제 기본적으로 표시 됩니다 ([큰 이미지를 보려면 클릭](declarative-parameters-cs/_static/image30.png))


## <a name="summary"></a>요약

입력된 매개 변수를 사용 하 여 메서드를 사용 하려면에서 ObjectDataSource의 매개 변수 값을 지정 해야 `SelectParameters` 컬렉션입니다. 다른 형식의 매개 변수를 다양 한 원본에서 가져올 매개 변수 값을 허용 합니다. 기본 매개 변수 형식이 하드 코드 된 값을 사용 하지만 (하지 않고 쉽게 코드 줄) 처럼 매개 변수 값에서 얻을 수 있습니다 쿼리 문자열, 세션 변수, 쿠키 및 웹 컨트롤을 페이지에도 사용자가 입력 한 값입니다.

이 자습서에서 살펴본 예제에서는 선언적 매개 변수 값을 사용 하는 방법을 보여 줍니다. 그러나 경우 현재 날짜 및 시간을 사용할 수 없는 매개 변수 소스를 사용 해야 하는 경우가 아니면, 사이트 멤버 자격, 방문자의 사용자 ID를 사용한 있습니다. 이러한 시나리오에 대해 설정할 수 있습니다 ObjectDataSource 전에 프로그래밍 방식으로 매개 변수 값을 해당 기본 개체의 메서드를 호출 합니다. 이 수행 하는 방법을 살펴보겠습니다 합니다 [다음 자습서](programmatically-setting-the-objectdatasource-s-parameter-values-cs.md)합니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Hilton giesenow와 함께 했습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](displaying-data-with-the-objectdatasource-cs.md)
> [다음](programmatically-setting-the-objectdatasource-s-parameter-values-cs.md)
