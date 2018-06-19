---
uid: web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/using-parameterized-queries-with-the-sqldatasource-vb
title: SqlDataSource (VB)와 매개 변수가 있는 쿼리를 사용 하 여 | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 SqlDataSource 컨트롤에서 모양 계속 하 고 매개 변수가 있는 쿼리를 정의 하는 방법을 알아봅니다. 매개 변수를 지정할 수 있습니다 모두 decla...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2007
ms.topic: article
ms.assetid: e322f34c-83b7-41ea-ab65-ab1e0bdcc609
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/using-parameterized-queries-with-the-sqldatasource-vb
msc.type: authoredcontent
ms.openlocfilehash: a7442ef3bebb2742cc36d695914b745aa2dfa721
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30878141"
---
<a name="using-parameterized-queries-with-the-sqldatasource-vb"></a>SqlDataSource (VB)와 매개 변수가 있는 쿼리를 사용 하 여
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_48_VB.exe) 또는 [PDF 다운로드](using-parameterized-queries-with-the-sqldatasource-vb/_static/datatutorial48vb1.pdf)

> 이 자습서에서는 SqlDataSource 컨트롤에서 모양 계속 하 고 매개 변수가 있는 쿼리를 정의 하는 방법을 알아봅니다. 매개 변수 모두 선언적으로 또는 프로그래밍 방식으로 지정할 수 있으며 많은 쿼리 문자열, 세션 상태, 다른 컨트롤 등과 같은 위치에서 끌어올 수 있습니다.


## <a name="introduction"></a>소개

이전 자습서에서 데이터를 검색 하는 데이터베이스에서 직접 SqlDataSource 컨트롤을 사용 하는 방법에 살펴보았습니다. 데이터 소스 구성 마법사를 사용 하 여 우리 선택할 수는 데이터베이스를 선택한 다음: 테이블 또는 뷰의; 반환할 열을 선택 합니다. 사용자 지정 SQL 문;를 입력 합니다. 또는 저장된 프로시저를 사용 합니다. 여부를 테이블 또는 뷰의 열을 선택 하는 사용자 지정 SQL 문을 입력, SqlDataSource 컨트롤을 반환 하거나 s `SelectCommand` 속성 결과 임시 SQL에 할당 되 `SELECT` 문이 되며이 `SELECT` 문이 될 때 실행 되는 SqlDataSource의 `Select()` 메서드 (프로그래밍 방식으로 또는 자동으로 데이터 웹 컨트롤에서에서).

SQL `SELECT` 없었습니다 이전 자습서의 데모에 사용 되는 문의 `WHERE` 절. 에 `SELECT` 문에서 `WHERE` 반환 된 결과 제한 하려면 절을 사용할 수 있습니다. 예를 들어 $50.00 이상 비용 계산과 제품 이름의 표시 하려면 다음 쿼리를 사용 있습니다.


[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample1.sql)]

사용 되는 값에 일반적으로 `WHERE` 절 querystring 값, 세션 변수 또는 페이지에서 웹 컨트롤에서 사용자 입력 등의 일부 외부 소스에 의해 결정 됩니다. 이러한 입력을 사용 하 여 지정 된 것이 이상적 *매개 변수*합니다. Microsoft SQL Server와 함께 매개 변수를 사용 하 여 표시 하는 `@parameterName`에서 같이:


[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample2.sql)]

SqlDataSource 지원에 대 한 매개 변수가 있는 쿼리 `SELECT` 문 및 `INSERT`, `UPDATE`, 및 `DELETE` 문. 또한 매개 변수 값 수 자동으로 다양 한 원본에서에서 쿼리 문자열, 세션 상태, 페이지에 컨트롤 및 등 기다리거나 프로그래밍 방식으로 할당할 수 있습니다. 이 자습서에서는 선언적 방법과 프로그래밍 방식으로 값 매개 변수를 지정 하는 방법에 매개 변수가 있는 쿼리를 정의 하는 방법을 살펴보겠습니다.

> [!NOTE]
> 이전 자습서에서의 개념적 유사성 주목할 SqlDataSource와 처음 46 자습서를 통해 선택한 자사 도구로 였던 ObjectDataSource 비교 했습니다. 이러한 공통 작업 매개 변수를 확장할 수도 있습니다. ObjectDataSource s 매개 변수는 비즈니스 논리 계층에 있는 메서드의 입력된 매개 변수에 매핑됩니다. SqlDataSource를 매개 변수에 SQL 쿼리 내에서 직접 정의 합니다. 두 컨트롤에 대 한 매개 변수 컬렉션에는 해당 `Select()`, `Insert()`, `Update()`, 및 `Delete()` 메서드 및 둘 다 채워집니다 (쿼리 문자열 값, 세션 변수 및 등 미리 정의 된 소스에서 이러한 매개 변수 값을 가질 수 ) 또는 프로그래밍 방식으로 할당 합니다.


## <a name="creating-a-parameterized-query"></a>매개 변수가 있는 쿼리 만들기

SqlDataSource 컨트롤의 데이터 소스 구성 마법사는 데이터베이스 레코드를 검색 하려면 실행할 명령을 정의 하기 위한 세 가지 방식을 제공 합니다.

- 기존 테이블 또는 보기에서 열을 선택 하 여
- 사용자 지정 SQL 문을 입력 하 여 또는
- 저장된 프로시저를 선택 하 여

기존 테이블 또는 뷰에 대 한 매개 변수에서 열을 선택할 때의 `WHERE` 추가 통해 절을 지정 해야 `WHERE` 절 대화 상자. 그러나 사용자 지정 SQL 문을 만들 때 입력할 수 있는에 직접 매개 변수는 `WHERE` 절 (사용 하 여 `@parameterName` 각 매개 변수를 나타내기 위해). A [저장 프로시저](http://www.awprofessional.com/articles/article.asp?p=25288&amp;rl=1) 하나 이상의 SQL 문을 구성 하 고 이러한 문을 매개 변수화 할 수 있습니다. 그러나 SQL 문에 사용 되는 매개 변수 전달 되어야 합니다에 입력된 매개 변수로 저장된 프로시저에.

매개 변수가 있는 쿼리를 만드는 방법에 의존 하므로 SqlDataSource의 `SelectCommand` 는 지정 된, let s 살펴보겠습니다 전혀 세 가지 방법입니다. 시작 하려면 열기는 `ParameterizedQueries.aspx` 페이지에 `SqlDataSource` 폴더를 디자이너에 도구 상자에서 SqlDataSource 컨트롤을 끌어서 설정 해당 `ID` 를 `Products25BucksAndUnderDataSource`합니다. 컨트롤 s 스마트 태그에서 데이터 소스 구성 링크를 클릭 합니다. 사용할 데이터베이스를 선택 (`NORTHWINDConnectionString`) 하 고을 클릭 합니다.

## <a name="step-1-adding-awhereclause-when-picking-the-columns-from-a-table-or-view"></a>1 단계: 추가 된`WHERE`절에서 테이블 또는 뷰의 열을 선택할 때

SqlDataSource 컨트롤을 사용 하 여 데이터베이스에서 반환할 데이터를 선택할 경우 데이터 소스 구성 마법사에서 기존 테이블을 반환 하거나 (그림 1 참조)을 보려면 열을 선택 하기만 하면를 수 있습니다. 자동으로 수행 하는 sql 빌드 `SELECT` 문을 데이터베이스로 전달 됩니다 때 SqlDataSource의 `Select()` 메서드가 호출 됩니다. 이전 자습서에서 수행한 것 처럼 드롭 다운 목록에서 Products 테이블을 선택 하 고 확인 된 `ProductID`, `ProductName`, 및 `UnitPrice` 열입니다.


[![반환할 테이블 또는 뷰의 열을 선택 합니다.](using-parameterized-queries-with-the-sqldatasource-vb/_static/image1.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image1.png)

**그림 1**: return 테이블 또는 뷰의 열을 선택 ([전체 크기 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image2.png))


포함 하도록는 `WHERE` 절에는 `SELECT` 문, 클릭는 `WHERE` 단추 추가 되면서 `WHERE` 절 대화 상자 (그림 2 참조). 반환 된 결과 제한 하려면 매개 변수를 추가 하는 `SELECT` 쿼리를 처음 사용 하 여 데이터를 필터링 할 열을 선택 합니다. 필터링에 사용할 연산자를 선택 합니다 (=, &lt;, &lt;=, &gt;등). 마지막으로 쿼리 문자열 또는 세션 상태에서와 같은 매개 변수의 값의 소스를 선택 합니다. 매개 변수를 구성한 후에 기능을 포함 하는 추가 단추를 클릭는 `SELECT` 쿼리 합니다.

예를 들어 s let 이러한 결과만 반환할 위치는 `UnitPrice` 값이 $25.00 보다 작습니다. 따라서 선택 `UnitPrice` 열 드롭다운 목록에서 및 &lt;연산자 드롭다운 목록에서 = 합니다. 하드 코딩 된 매개 변수 값 (예: $25.00)를 사용 하는 경우 또는 매개 변수 값은 프로그래밍 방식으로 지정 해야 하는 경우 소스 드롭 다운 목록에서 없음을 선택 합니다. 다음을 25.00 값 텍스트 상자에 하드 코딩 된 매개 변수 값을 입력 하 고 추가 단추를 클릭 하 여 프로세스를 완료 합니다.


[![반환 된 결과 제한 된 추가 WHERE 절 대화 상자](using-parameterized-queries-with-the-sqldatasource-vb/_static/image2.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image3.png)

**그림 2**: 추가에서 반환 된 결과 제한 `WHERE` 절 대화 상자 ([전체 크기 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image4.png))


매개 변수를 추가한 후 데이터 소스 구성 마법사로 돌아가려면 확인을 클릭 합니다. `SELECT` 마법사의 맨 아래에 문에 이제 포함할 수는 `WHERE` 라는 매개 변수가 포함 된 절 `@UnitPrice`:


[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample3.sql)]

> [!NOTE]
> 여러 조건을 지정 하는 경우는 `WHERE` 추가에서 절 `WHERE` 를 사용 하 여 절 대화 상자 마법사 조인는 `AND` 연산자입니다. 포함 해야 하는 경우는 `OR` 에 `WHERE` 절 (같은 `WHERE UnitPrice <= @UnitPrice OR Discontinued = 1`)을 작성 해야 합니다는 `SELECT` 문을 사용자 지정 SQL 문 화면을 통해.


SqlDataSource (다음으로, 다음 마침)을 구성을 완료 하 고 SqlDataSource s 선언적 태그를 검사 합니다. 태그에 포함 되어 이제는 `<SelectParameters>` 컬렉션에서 매개 변수에 대 한 소스 줄이지 않고는 `SelectCommand`합니다.


[!code-aspx[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample4.aspx)]

때 SqlDataSource s `Select()` 메서드가 호출 되는 `UnitPrice` 매개 변수 값 (25.00)에 적용 됩니다는 `@UnitPrice` 에서 매개 변수는 `SelectCommand` 데이터베이스에 전송 되기 전에 합니다. 결과에서 반환 되는 $25.00 보다 작거나 같은 제품에만 `Products` 테이블입니다. 확인 하려면이 추가 GridView 페이지에,이 데이터 원본에 연결 하 고 브라우저를 통해 페이지를 봅니다. 나열 된 그림 3에서 확인 된 $25.00, 보다 작거나 같으면 해당 제품은 표시 됩니다.


[![이러한 제품 보다 작음 또는 $25.00 같음에만 표시 됩니다.](using-parameterized-queries-with-the-sqldatasource-vb/_static/image3.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image5.png)

**그림 3**:만 해당 제품 보다 작음 또는 $25.00 같음 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image6.png))


## <a name="step-2-adding-parameters-to-a-custom-sql-statement"></a>2 단계: 사용자 지정 SQL 문에 매개 변수 추가

사용자 지정 SQL 문을 추가할 때 입력 된 `WHERE` 절 명시적으로 하거나 쿼리 작성기의 필터 셀에 값을 지정 합니다. 이 증명 하려면 특정 임계값 보다 작은 가격은 GridView에만 해당 제품을 표시 하는 s를 사용 합니다. 입력란을 추가 하 여 시작는 `ParameterizedQueries.aspx` 이 임계값 사용자 로부터 수집 하는 페이지입니다. TextBox s 설정 `ID` 속성을 `MaxPrice`합니다. Button 웹 컨트롤을 추가 하 고 설정 해당 `Text` 속성을 일치 하는 제품을 표시 합니다.

다음으로 GridView를 페이지로 끌어 및 스마트 태그에서를 작성 하기로 라는 새 SqlDataSource `ProductsFilteredByPriceDataSource`합니다. 데이터 소스 구성 마법사에서 진행 지정 하는 사용자 지정 SQL 문 또는 저장된 프로시저 화면 (그림 4 참조) 다음과 같은 쿼리를 입력 합니다.


[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample5.sql)]

쿼리 (수동으로 또는 쿼리 작성기를 통해)를 입력 한 후 다음을 클릭 합니다.


[![매개 변수 값 보다 작거나 제품만 반환](using-parameterized-queries-with-the-sqldatasource-vb/_static/image4.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image7.png)

**그림 4**: 반환만 해당 제품 보다 작음 또는 매개 변수 값을 같음 ([전체 크기 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image8.png))


쿼리 매개 변수가 포함 하므로 마법사의 다음 화면 매개 변수 값의 원본에 대 한 우리 묻습니다. 매개 변수 소스 드롭 다운 목록에서 컨트롤을 선택 하 고 `MaxPrice` (TextBox 컨트롤의 `ID` 값) ControlID 드롭 다운 목록에서 합니다. 사용자가 모든 텍스트를 입력 하지 하는 경우에 사용할 선택적 기본값을 입력할 수도 있습니다는 `MaxPrice` 텍스트 상자에 붙여넣습니다. 항상에 대 한 기본값을 입력 하지 마십시오.


[![Text 속성 매개 변수 원본으로 사용 되는 MaxPrice TextBox s](using-parameterized-queries-with-the-sqldatasource-vb/_static/image5.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image9.png)

**그림 5**:는 `MaxPrice` TextBox s `Text` 속성은 매개 변수 원본으로 사용 ([전체 크기 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image10.png))


다음으로, 클릭 하 여 데이터 소스 구성 마법사를 완료 한 다음 완료 합니다. GridView, 텍스트 상자, 단추 및 SqlDataSource에 대 한 선언적 태그 다음과 같습니다.


[!code-aspx[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample6.aspx)]

SqlDataSource s 내 매개 변수의 `<SelectParameters>` 섹션은는 `ControlParameter`, 같은 추가 속성을 포함 하 `ControlID` 및 `PropertyName`합니다. 때 SqlDataSource s `Select()` 메서드가 호출 되는 `ControlParameter` 지정된 된 웹 컨트롤 속성의 값을 가져와 만들어에서 해당 매개 변수에 할당는 `SelectCommand`합니다. 이 예제는 `MaxPrice` s Text 속성으로 사용 되는 `@MaxPrice` 매개 변수 값입니다.

브라우저를 통해이 페이지를 보려면 잠시를 살펴보겠습니다. 페이지를 처음 방문할 때 또는 때마다는 `MaxPrice` 텍스트 상자에 GridView에는 없는 레코드가 표시 값이 없는 합니다.


[![표시 되는 경우의 MaxPrice TextBox 비어 있는 레코드가 없습니다.](using-parameterized-queries-with-the-sqldatasource-vb/_static/image6.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image11.png)

**그림 6**: 레코드가 없을 때 표시 되는 `MaxPrice` 텍스트 상자가 비어 있지 않습니다 ([전체 크기 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image12.png))


기본적으로 매개 변수 값에 대 한 빈 문자열을 데이터베이스로 변환 하기 때문에 제품이 표시 되는 이유는 `NULL` 값입니다. 비교의 이후 `[UnitPrice] <= NULL` 항상 평가 결과가 False로 반환 됩니다.

5.00 같은 입력란에 값을 입력 하 고 일치 하는 제품 표시 단추를 클릭 합니다. 다시 게시 될 SqlDataSource GridView 매개 변수 소스 중 하나는 변경 된 알립니다. 따라서 GridView $5.00에 게 해당 제품 작은 보다 짧거나 표시 SqlDataSource에 다시 바인딩합니다.


[![제품 보다 작음 또는 $5.00 같음 표시](using-parameterized-queries-with-the-sqldatasource-vb/_static/image7.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image13.png)

**그림 7**: 제품 보다 작음 또는 $5.00 같음 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image14.png))


## <a name="initially-displaying-all-products"></a>모든 제품을 처음 표시

페이지가 처음 로드 될 때 제품이 표시 하는 대신 표시 하려면 수행할 *모든* 제품입니다. 모든 제품을 나열 하는 한 가지 방법은 때마다는 `MaxPrice` TextBox 비어 있습니다. 일부 insanely 높은 값으로 s 매개 변수 기본값을 설정 하는 1000000에 같은 이후 s는 Northwind Traders 적이 있는 인벤토리가 작성 됩니다 단가 나 가능성이 초과 $1000000입니다. 그러나이 방법은 근시안적 이며 다른 상황에서는 작동 하지 않을 수 있습니다.

이전 자습서- [선언적 매개 변수](../basic-reporting/declarative-parameters-vb.md) 및 [마스터/세부 정보 필터링 된 정도 DropDownList](../masterdetail/master-detail-filtering-with-a-dropdownlist-vb.md) 유사한 문제를 처리 된 것입니다. 이 논리는 비즈니스 논리 계층에 넣을 수 있는 솔루션이 했습니다. BLL 들어오는 값을 검사 하는 구체적으로, 여부와 `NULL` 또는 일부 예약 값, 호출 모든 레코드를 반환 하는 DAL 메서드에 라우팅 되었습니다. 호출에 사용 되는 매개 변수가 있는 SQL 문을 실행 하는 DAL 메서드가 호출 들어오는 값 정상 필터링 값을 되었으면 `WHERE` 절 제공 된 값을 사용 합니다.

안타깝게도, SqlDataSource를 사용 하는 경우 아키텍처를 무시 했습니다. 대신, SQL 문을 자동으로 조정 하는 경우 모든 레코드를 가져올 사용자 지정 해야는 `@MaximumPrice` 매개 변수는 `NULL` 또는 기타 예약 된 값입니다. 이 연습에서는 let s 하 게 되므로 되는 경우는 `@MaximumPrice` 매개 변수와 같으면 `-1.0`, 다음 *모든* 반환 되는 레코드 (`-1.0` 제품이 없으므로 음수를가질수있으므로예약된값으로작동`UnitPrice`값). 이렇게 하려면 다음 SQL 문을 사용할 수 있습니다.


[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample7.sql)]

이 `WHERE` 절 반환 *모든* 기록 하는 경우는 `@MaximumPrice` 매개 변수와 같으면 `-1.0`합니다. 매개 변수 값이 `-1.0`, 제품만 인 `UnitPrice` 보다 작거나 같음는 `@MaximumPrice` 매개 변수 값이 반환 됩니다. 기본값을 설정 하 여는 `@MaximumPrice` 매개 변수를 `-1.0`, 첫 번째 페이지 로드 시 (또는 때마다는 `MaxPrice` TextBox 비어 있습니다.), `@MaximumPrice` 의 값은 `-1.0` 모든 제품을 표시 됩니다.


[![이제 모든 제품이 표시 되는 경우의 MaxPrice TextBox 비어 있습니다.](using-parameterized-queries-with-the-sqldatasource-vb/_static/image8.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image15.png)

**그림 8**: 이제 모든 제품 때 표시 되는 `MaxPrice` 텍스트 상자가 비어 있지 않습니다 ([전체 크기 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image16.png))


이 접근 방식에 유의 하 여 주의 사항이의 두 가지가 있습니다. 첫째, 매개 변수의 데이터 형식에서 유추 됩니다을 실제로 SQL 쿼리에 s 사용 합니다. 변경 하는 경우는 `WHERE` 절에서 `@MaximumPrice = -1.0` 를 `@MaximumPrice = -1`, 런타임에서 매개 변수는 정수로 처리 합니다. 그런 다음 할당할 하려고 하는 경우는 `MaxPrice` 10 진수 값 (예: 5.00) 하는 입력란, 5.00는 정수를 변환할 수 때문에 오류가 발생 합니다. 이 해결 하려면 사용 하는 않았는지 확인 `@MaximumPrice = -1.0` 에 `WHERE` 절 또는 그 이상 아직 설정는 `ControlParameter` 개체의 `Type` 속성을 10 진수입니다.

추가 하 여 두 번째로,는 `OR @MaximumPrice = -1.0` 에 `WHERE` 절, 쿼리 엔진에 인덱스를 사용할 수 없습니다 `UnitPrice` (발생), 그 결과로 테이블 검색 합니다. 이 성능에 미치는 영향에 있는 레코드의 충분히 큰 수의 `Products` 테이블입니다. 더 나은 방법은 저장된 프로시저에이 논리를 이동 하는 것에 `IF` 문 중 하나를 수행 합니다는 `SELECT` 에서 쿼리는 `Products` 없이 테이블는 `WHERE` 절 모든 레코드를 반환 해야 하는 경우 또는 하나 인 `WHERE` 절만 포함 되어 있으면는 `UnitPrice` 조건, 인덱스를 사용할 수 있도록 합니다.

## <a name="step-3-creating-and-using-parameterized-stored-procedures"></a>3 단계: 만들기 및 매개 변수가 있는 저장된 프로시저를 사용 합니다.

저장된 프로시저는 저장된 프로시저 내에 정의 된 SQL 문을 지정에 사용할 수 있는 입력된 매개 변수 집합이 포함할 수 있습니다. 입력된 매개 변수를 허용 하는 저장된 프로시저를 사용 하도록 SqlDataSource를 구성할 때 이러한 매개 변수 값을 임시 SQL 문이와 마찬가지로 동일한 기술을 사용 하 여 지정할 수 있습니다.

Let s 라는 Northwind 데이터베이스의 새 저장된 프로시저 만들기를 설명 하기 위해 저장된 프로시저를 사용 하 여 SqlDataSource에서 `GetProductsByCategory`, 라는 매개 변수를 허용 하는 `@CategoryID` 모든 제품의 열을 반환 하 고 해당 `CategoryID` 열이 일치 `@CategoryID`합니다. 저장된 프로시저를 만들려면 서버 탐색기로 이동 하 고 드릴 다운은 `NORTHWND.MDF` 데이터베이스입니다. (T don 서버 탐색기를 나타나면 상태로 보기 메뉴 하 고 서버 탐색기 옵션을 선택 하 여.)

`NORTHWND.MDF` 데이터베이스에서 저장 프로시저 폴더를 마우스 오른쪽 단추로 클릭 새 저장 프로시저 추가 선택한 다음 구문을 입력 합니다.


[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample8.sql)]

저장된 프로시저를 저장 하려면 저장 아이콘 (또는 Ctrl + S)를 클릭 합니다. Stored Procedures 폴더에서 마우스 오른쪽 단추로 클릭 하 고 실행을 선택 하 여 저장된 프로시저를 테스트할 수 있습니다. 묻는 메시지가 나타납니다 s 저장된 프로시저 매개 변수의 (`@CategoryID`,이 인스턴스의), 후 출력 창에는 결과 표시 됩니다.


[![GetProductsByCategory 저장 프로시저를 실행 한 @CategoryID 1](using-parameterized-queries-with-the-sqldatasource-vb/_static/image9.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image17.png)

**그림 9**:는 `GetProductsByCategory` 저장 프로시저를 실행 한 `@CategoryID` 1 ([전체 크기 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image18.png))


이 저장된 프로시저를 사용 하 여 음료 범주는 GridView에 모든 제품을 전시 하기 s 사용 수 있습니다. 새 GridView 페이지에 추가 하 고 라는 새 SqlDataSource 바인딩할 `BeverageProductsDataSource`합니다. 사용자 지정 SQL 문 또는 저장된 프로시저 화면 지정 계속, 저장 프로시저 라디오 단추를 선택 하 고, 선택는 `GetProductsByCategory` 드롭 다운 목록에서 저장 프로시저입니다.


[![GetProductsByCategory 선택 드롭다운 목록에서 저장 프로시저](using-parameterized-queries-with-the-sqldatasource-vb/_static/image10.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image19.png)

**그림 10**: 선택 된 `GetProductsByCategory` 드롭 다운 목록에서 저장 프로시저 ([전체 크기 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image20.png))


저장된 프로시저 입력된 매개 변수를 허용 하므로 (`@CategoryID`),이 매개 변수의 값에 대 한 원본을 지정 하 라는 메시지가 표시 다음을 클릭 합니다. 음료 `CategoryID` 은 1 이므로 매개 변수 소스 드롭 다운 목록 none 두고 DefaultValue 텍스트 상자에 1을 입력 합니다.


[![하드 코드 된 값이 1 사용 하 여 음료 범주에는 제품을 반환 합니다.](using-parameterized-queries-with-the-sqldatasource-vb/_static/image11.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image21.png)

**그림 11**: Hard-Coded 값 1 사용 하 여 음료 범주에는 제품을 반환할 ([전체 크기 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image22.png))


SqlDataSource s 저장된 프로시저를 사용 하는 경우 다음 선언 태그와 같이 `SelectCommand` 저장된 프로시저의 이름 속성 및 [ `SelectCommandType` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.selectcommandtype.aspx) 로 설정 된 `StoredProcedure`한다는 표시 이므로 하 여 `SelectCommand` 임시 SQL 문이 아닌 저장된 프로시저의 이름입니다.


[!code-aspx[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample9.aspx)]

브라우저에서 페이지를 테스트 합니다. 음료 범주에 속해 있는 제품만 표시 하지만 *모든* 이후 제품의 필드가 표시 됩니다는 `GetProductsByCategory` 저장된 프로시저가 반환의 모든 열에서는 `Products` 테이블입니다. 수 없습니다, 그리고 물론 제한할 하거나 GridView의 열 편집 대화 상자에서 GridView에 표시 되는 필드를 사용자 지정 합니다.


[![음료 모두 표시](using-parameterized-queries-with-the-sqldatasource-vb/_static/image12.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image23.png)

**그림 12**: 음료는의 모든 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image24.png))


## <a name="step-4-programmatically-invoking-a-sqldatasource-sselectstatement"></a>4 단계: SqlDataSource s를 프로그래밍 방식으로 호출 하`Select()`문

예제에서는 이전 자습서와이 자습서에서 지금까지 나온 했습니다 SqlDataSource 컨트롤은 GridView에 직접 바인딩한 합니다. 그러나 SqlDataSource 컨트롤의 데이터 프로그래밍 방식으로 액세스 하 고 수 코드에 열거 합니다. 이 데이터를 쿼리, 검사를 하지만 안 것을 표시 해야 하는 경우 특히 유용 합니다. 모든 데이터베이스에 연결 하 여 명령을 지정 하 고 결과 검색 하는 ADO.NET 코드 상용구 작성 하는 대신 SqlDataSource이 되풀이 되 코드를 처리 하도록 할 수 있습니다.

SqlDataSource의 작업을 설명 하기 위해 데이터는 상사에 도달 하면 임의로 선택 된 범주와 관련 된 제품 이름을 표시 하는 웹 페이지 생성 요청으로 프로그래밍 방식으로 가정 합니다. 즉, 사용자가이 페이지를 방문 하려고에서 범주를 임의로 선택 된 `Categories` 테이블, 범주 이름을 표시 한 다음 해당 범주에 속하는 제품을 나열 합니다.

SqlDataSource 컨트롤을 두 개 하나에서 임의 범주를 선택 해야이를 위해는 `Categories` 테이블과 다른 범주를 가져올 s 제품입니다. 이 단계에 임의 범주 레코드를 검색 하는 SqlDataSource 빌드합니다. 5 단계 범주의 제품을 검색 하는 SqlDataSource 프 살펴 봅니다.

SqlDataSource를 추가 하 여 시작 `ParameterizedQueries.aspx` 설정 하 고 해당 `ID` 를 `RandomCategoryDataSource`합니다. 에 다음 SQL 쿼리를 사용 하도록 구성 합니다.


[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample10.sql)]

`ORDER BY NEWID()` 임의의 순서로 정렬 된 레코드를 반환 합니다 (참조 [Using `NEWID()` 임의로 정렬 레코드를](http://www.sqlteam.com/item.asp?ItemID=8747)). `SELECT TOP 1` 결과 집합에서 첫 번째 레코드를 반환합니다. 이 쿼리는 반환 종합적으로 `CategoryID` 및 `CategoryName` 단일, 임의로 선택 된 범주에서 열 값입니다.

S 범주 표시 하려면 `CategoryName` 값, 페이지로 Label 웹 컨트롤을 추가 하 고, 설정 해당 `ID` 속성을 `CategoryNameLabel`를 제거 하 고 해당 `Text` 속성입니다. 호출 하도록 설정 해야 SqlDataSource 컨트롤에서 데이터를 프로그래밍 방식으로 검색, 해당 `Select()` 메서드. [ `Select()` 메서드](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.select.aspx) 형식의 단일 입력 매개 변수 [ `DataSourceSelectArguments` ](https://msdn.microsoft.com/library/system.web.ui.datasourceselectarguments.aspx)를 반환 하기 전에 데이터를 이와 하는 방법을 지정 합니다. 이 데이터를 정렬 및 필터링에 대 한 지침을 포함할 수 있습니다 및 웹 컨트롤을 정렬 하거나 SqlDataSource 컨트롤에서 데이터를 통한 페이징을 할 데이터에 사용 합니다. 이 예에서는 그러나 우리 않는 t 필요가 데이터를 반환 하기 전에 수정할 수 및에서 통과 합니다는 `DataSourceSelectArguments.Empty` 개체입니다.

`Select()` 메서드를 구현 하는 개체를 반환 `IEnumerable`합니다. 정확한 형식의 SqlDataSource 컨트롤 값에 따라 반환 [ `DataSourceMode` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.datasourcemode.aspx)합니다. 이 속성의 값으로 설정할 수 있습니다 이전 자습서에서 설명 했 듯이 `DataSet` 또는 `DataReader`합니다. 경우로 설정 `DataSet`, `Select()` 메서드가 반환 되는 [DataView](https://msdn.microsoft.com/library/01s96x0z.aspx) 개체;로 설정 하는 경우 `DataReader`를 구현 하는 개체를 반환 [ `IDataReader` ](https://msdn.microsoft.com/library/system.data.idatareader.aspx)합니다. 이후는 `RandomCategoryDataSource` SqlDataSource가 해당 `DataSourceMode` 속성이로 설정 `DataSet` (기본값) 사용할 DataView 개체를 사용 합니다.

다음 코드에는 레코드를 검색 하는 방법을 보여 줍니다.는 `RandomCategoryDataSource` DataView로 SqlDataSource를 읽는 방법을 뿐만 아니라는 `CategoryName` 첫 번째 DataView 행의 열 값:


[!code-vb[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample11.vb)]

`randomCategoryView(0)` 첫 번째 개체가 반환 `DataRowView` DataView의 합니다. `randomCategoryView(0)("CategoryName")` 값을 반환 된 `CategoryName` 이 첫 번째 행의 열입니다. DataView 느슨한 형 인지 note 합니다. 특정 열 값을 참조 하려면 (이 경우 CategoryName) 문자열 열 이름을 전달 해야 합니다. 그림 13에 표시 되는 메시지를 보여 줍니다.는 `CategoryNameLabel` 페이지를 볼 때. 물론, 표시 되는 실제 범주 이름은 임의로 선택 하 여는 `RandomCategoryDataSource` (포스트백 포함) 페이지를 각 방문할 SqlDataSource 합니다.


[![임의로 선택 된 범주의 이름이 표시 됩니다](using-parameterized-queries-with-the-sqldatasource-vb/_static/image13.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image25.png)

**그림 13**: 다음 임의로 선택 된 범주의 이름이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image26.png))


> [!NOTE]
> SqlDataSource 컨트롤 s `DataSourceMode` 속성 설정 된 `DataReader`, 반환 값을는 `Select()` 방법 들에 게로 캐스팅할 수 `IDataReader`합니다. 읽을 수는 `CategoryName` d에서는 첫 번째 행의 열 값이 같은 코드를 사용 하세요.


[!code-vb[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample12.vb)]

SqlDataSource를 임의로 선택 하는 범주를 범주의 제품을 나열 하 여 GridView를 추가 하려면 준비 된 것입니다.

> [!NOTE]
> 범주의 이름을 표시 하는 Label 웹 컨트롤을 사용 하지 않고 수 추가 했습니다 FormView 또는 DetailsView의 페이지 SqlDataSource에 바인딩. 그러나 수 SqlDataSource s 프로그래밍 방식으로 호출 하는 방법을 탐색할 레이블을 사용 하 여, `Select()` 문과 코드의 결과 데이터와 함께 작업 합니다.


## <a name="step-5-assigning-parameter-values-programmatically"></a>5 단계: 매개 변수 값을 프로그래밍 방식으로 할당

모든 예제에서는 하드 코드 된 매개 변수 값 또는 미리 정의 된 매개 변수 원본 (querystring 값 웹, 컨트롤, 페이지, 및 등) 중 하나에서 가져오지를 사용한 있어야이 자습서에서 지금까지 본 적입니다. 그러나 SqlDataSource 컨트롤 s 매개 변수를 프로그래밍 방식으로 설정할 수도 있습니다. 현재 예제를 완료 하려면 모든 지정된 된 범주에 속하는 제품을 반환 하는 SqlDataSource 필요 합니다. 이 SqlDataSource 갖습니다는 `CategoryID` 에 따라 값을 설정 해야 하는 매개 변수는 `CategoryID` 에서 반환 된 열 값의 `RandomCategoryDataSource` SqlDataSource에서는 `Page_Load` 이벤트 처리기.

페이지에는 GridView를 추가 하 여 시작 하 고 라는 새 SqlDataSource 바인딩할 `ProductsByCategoryDataSource`합니다. 3 단계에서에서 했던와 비슷하게를 호출 하도록 SqlDataSource 구성한는 `GetProductsByCategory` 저장 프로시저입니다. 매개 변수 소스 드롭 다운 목록 집합 없음, 나가는 프로그래밍 방식으로이 기본값은 설정으로 기본값을 입력 하지 않으면 됩니다.


[![매개 변수 소스 또는 기본값을 지정 하지 않으면](using-parameterized-queries-with-the-sqldatasource-vb/_static/image14.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image27.png)

**그림 14**: 매개 변수 소스 또는 기본값을 지정 하지 않으면 ([전체 크기 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image28.png))


SqlDataSource 마법사를 완료 한 후 결과 선언적 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample13.aspx)]

할당 수의 `DefaultValue` 의 `CategoryID` 프로그래밍 방식으로 매개 변수는 `Page_Load` 이벤트 처리기:


[!code-vb[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample14.vb)]

이 추가 페이지 임의로 선택 된 범주와 관련 된 제품이 표시 되는 GridView가 포함 됩니다.


[![매개 변수 소스 또는 기본값을 지정 하지 않으면](using-parameterized-queries-with-the-sqldatasource-vb/_static/image15.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image29.png)

**그림 15**: 매개 변수 소스 또는 기본값을 지정 하지 않으면 ([전체 크기 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image30.png))


## <a name="summary"></a>요약

SqlDataSource는 페이지 개발자가을 매개 변수 값을 가진 하드 코드 된, 미리 정의 된 매개 변수 원본에서 가져온 하거나 프로그래밍 방식으로 지정할 수는 매개 변수가 있는 쿼리를 정의할 수 있습니다. 이 자습서에서는 임시 SQL 쿼리 및 저장된 프로시저 모두에 대 한 데이터 소스 구성 마법사에서 매개 변수가 있는 쿼리를 작성할 하는 방법에 살펴보았습니다. 또한 살펴보았습니다 원본 하드 코딩 된 매개 변수, 매개 변수 원본으로 웹 컨트롤을 사용 하 고 프로그래밍 방식으로 매개 변수 값을 지정 합니다.

마찬가지로 ObjectDataSource를 SqlDataSource도 제공 원본 데이터를 수정 하는 기능 합니다. 다음 자습서에서에서 살펴보게 정의 하는 방법을 `INSERT`, `UPDATE`, 및 `DELETE` SqlDataSource 문입니다. 이러한 문은 추가 되 면 기본 제공 삽입, 편집 및 삭제 기능 GridView, DetailsView, FormView 컨트롤에 내재 이용 하면 합니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자가 Scott와 클라이드, Randell Schmidt 및 켄 Pespisa 합니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](querying-data-with-the-sqldatasource-control-vb.md)
> [다음](inserting-updating-and-deleting-data-with-the-sqldatasource-vb.md)
