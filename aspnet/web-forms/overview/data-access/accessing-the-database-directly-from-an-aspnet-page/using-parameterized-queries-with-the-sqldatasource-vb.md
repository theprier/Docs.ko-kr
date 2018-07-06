---
uid: web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/using-parameterized-queries-with-the-sqldatasource-vb
title: SqlDataSource (VB)를 사용 하 여 매개 변수가 있는 쿼리를 사용 하 여 | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 살펴보겠습니다 SqlDataSource 컨트롤을 계속 하 고 매개 변수가 있는 쿼리를 정의 하는 방법을 알아봅니다. 매개 변수를 지정할 수 있습니다 모두 선언 하는 중...
ms.author: aspnetcontent
ms.date: 02/20/2007
ms.assetid: e322f34c-83b7-41ea-ab65-ab1e0bdcc609
msc.legacyurl: /web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/using-parameterized-queries-with-the-sqldatasource-vb
msc.type: authoredcontent
ms.openlocfilehash: fd4964bbdfe7662513025086a6cc3a59a6d63782
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37813817"
---
<a name="using-parameterized-queries-with-the-sqldatasource-vb"></a>SqlDataSource (VB)를 사용 하 여 매개 변수가 있는 쿼리를 사용 하 여
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_48_VB.exe) 또는 [PDF 다운로드](using-parameterized-queries-with-the-sqldatasource-vb/_static/datatutorial48vb1.pdf)

> 이 자습서에서는 살펴보겠습니다 SqlDataSource 컨트롤을 계속 하 고 매개 변수가 있는 쿼리를 정의 하는 방법을 알아봅니다. 매개 변수를 선언적으로 프로그래밍 방식으로 지정할 수 있으며 많은 쿼리 문자열, 세션 상태, 기타 컨트롤 등과 같은 위치에서 가져올 수 있습니다.


## <a name="introduction"></a>소개

이전 자습서에서 SqlDataSource 컨트롤을 사용 하 여 데이터베이스에서 직접 데이터를 검색 하는 방법에 살펴보았습니다. 데이터 소스 구성 마법사를 사용 하 여 선택할 수 있습니다 데이터베이스 및 다음: 테이블 또는 뷰에서; 반환할 열을 선택 합니다. 사용자 지정 SQL 문;를 입력 합니다. 또는 저장된 프로시저를 사용 합니다. 테이블 또는 뷰에서 열을 선택 하는 사용자 지정 SQL 문 입력, SqlDataSource s를 제어 하는지 여부를 `SelectCommand` 속성은 결과 임시 SQL 할당 `SELECT` 문과 것 입니까 `SELECT` 있는 문에 될 때 실행 되는 SqlDataSource의 `Select()` 메서드 (프로그래밍 방식으로 또는 자동으로 데이터 웹 컨트롤에서에서).

SQL `SELECT` 없었습니다 이전 자습서의 데모에 사용 된 문이 `WHERE` 절. 에 `SELECT` 문에서 `WHERE` 반환 된 결과 제한 하려면 절을 사용할 수 있습니다. 예를 들어 비용 $50.00 이상 제품의 이름을 표시할 다음 쿼리를 사용할 수 했습니다.


[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample1.sql)]

에 사용 된 값으로는 `WHERE` 절 querystring 값, 세션 변수 또는 페이지의 웹 컨트롤에서 사용자 입력 등 일부 외부 소스에 의해 결정 됩니다. 사용 하 여 이러한 입력을 지정 하는 것이 좋습니다 *매개 변수*합니다. Microsoft SQL Server를 사용 하 여 매개 변수를 사용 하 여 표시 됩니다 `@parameterName`에서처럼:


[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample2.sql)]

SqlDataSource 둘 다에 대 한 매개 변수가 있는 쿼리를 지 원하는 `SELECT` 문 및 `INSERT`, `UPDATE`, 및 `DELETE` 문. 또한 매개 변수 값을 끌어올 수 있습니다 자동으로 다양 한 원본에서에서 쿼리 문자열, 세션 상태 페이지의 컨트롤 등 있고 프로그래밍 방식으로 할당할 수 있습니다. 이 자습서에서는 선언적 및 프로그래밍 방식으로 값 매개 변수를 지정 하는 방법 뿐만 아니라 매개 변수가 있는 쿼리를 정의 하는 방법을 살펴보겠습니다.

> [!NOTE]
> 이전 자습서에서 해당 개념적 유사성 주목할 SqlDataSource 사용 하 여 먼저 46 자습서를 통해 원하는 도구인 된 ObjectDataSource 비교 했습니다. 이러한 유사성 매개 변수를 확장할 수도 있습니다. ObjectDataSource s 매개 변수는 비즈니스 논리 계층에서 메서드에 대 한 입력된 매개 변수에 매핑됩니다. SqlDataSource를 사용 하 여 매개 변수는 SQL 쿼리 내에서 직접 정의 됩니다. 두 컨트롤의 매개 변수 컬렉션에는 해당 `Select()`, `Insert()`를 `Update()`, 및 `Delete()` 메서드 및 모두 채워집니다 (querystring 값, 세션 변수 및 등 미리 정의 된 원본에서 이러한 매개 변수 값을 가질 수 ) 또는 프로그래밍 방식으로 할당 합니다.


## <a name="creating-a-parameterized-query"></a>매개 변수가 있는 쿼리 만들기

SqlDataSource 컨트롤의 데이터 소스 구성 마법사는 데이터베이스 레코드를 검색 하기 위해 실행 하는 명령을 정의 하는 세 가지 방법을 제공 합니다.

- 기존 테이블 또는 보기에서 열을 선택 하 여
- 사용자 지정 SQL 문을 입력 하 여 또는
- 저장된 프로시저를 선택 하 여

기존 테이블 또는 뷰, 매개 변수에서 열을 선택할 때 합니다 `WHERE` 추가 통해 절을 지정 해야 `WHERE` 절 대화 상자. 그러나 사용자 지정 SQL 문을 만들 때 입력할 수 있습니다에 직접 매개 변수를 `WHERE` 절 (사용 하 여 `@parameterName` 각 매개 변수를 나타내기 위해). A [저장 프로시저](http://www.awprofessional.com/articles/article.asp?p=25288&amp;rl=1) 하나 이상의 SQL 문 구성 및 이러한 문을 매개 변수화 할 수 있습니다. 그러나 SQL 문에서 사용 된 매개 변수에 전달 되어야 합니다에서 입력된 매개 변수로 저장 프로시저.

매개 변수가 있는 쿼리를 만드는 방법에 따라 다릅니다 하므로 SqlDataSource의 `SelectCommand` 는 지정 된, s 살펴보겠습니다 전혀 세 가지 방법입니다. 시작 하려면 열기를 `ParameterizedQueries.aspx` 페이지에 `SqlDataSource` 폴더, SqlDataSource 컨트롤을 디자이너 도구 상자에서 끌어서 설정 해당 `ID` 에 `Products25BucksAndUnderDataSource`합니다. 다음으로, 컨트롤 s 스마트 태그의 데이터 소스 구성 링크를 클릭 합니다. 데이터베이스를 사용 하 여 선택 (`NORTHWINDConnectionString`) 다음을 클릭 합니다.

## <a name="step-1-adding-awhereclause-when-picking-the-columns-from-a-table-or-view"></a>1 단계: 추가 된`WHERE`절에서 테이블 또는 뷰의 열을 선택할 때

SqlDataSource 컨트롤을 사용 하 여 데이터베이스에서 반환할 데이터를 선택할 때 데이터 소스 구성 마법사를 단순히 기존 테이블에서 반환 하거나 (그림 1 참조)을 보려면 열을 선택할 수 있습니다. 자동으로 수행 하는 sql 작성 `SELECT` 문을 데이터베이스로 전달 되는 내용 때 SqlDataSource의 `Select()` 메서드가 실행 됩니다. 이전 자습서에서 했던 것 처럼 드롭 다운 목록에서 Products 테이블을 선택 하 고 확인 합니다 `ProductID`, `ProductName`, 및 `UnitPrice` 열입니다.


[![테이블 또는 보기에서 반환할 열을 선택 합니다.](using-parameterized-queries-with-the-sqldatasource-vb/_static/image1.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image1.png)

**그림 1**: 테이블 또는 뷰를 반환 하는 열을 선택 ([큰 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image2.png))


포함 하는 `WHERE` 절을 `SELECT` 문을 클릭를 `WHERE` 추가을 표시 하는 단추를 `WHERE` 절 대화 상자 (그림 2 참조). 반환한 결과 제한 하려면 매개 변수를는 `SELECT` 쿼리 먼저 열을 선택 하 여 데이터를 필터링 합니다. 그런 다음 필터링에 사용할 연산자를 선택 (=, &lt;, &lt;=, &gt;등). 마지막으로, 쿼리 문자열 또는 세션 상태에서 같은 매개 변수의 값의 소스를 선택 합니다. 매개 변수를 구성한 후에 포함할 추가 단추를 클릭 합니다 `SELECT` 쿼리 합니다.

예를 들어 let s 해당 결과만 반환 위치는 `UnitPrice` $25.00 보다 작거나 같은 값이 있습니다. 따라서 선택할 `UnitPrice` 열의 드롭다운 목록에서 및 &lt;연산자 드롭다운 목록에서 =. 하드 코드 된 매개 변수 값 (예: $25.00)를 사용 하는 경우 또는 매개 변수 값을 프로그래밍 방식으로 지정할 경우 원본 드롭다운 목록에서 없음를 선택 합니다. 다음으로, 25.00 값 텍스트 상자에 하드 코드 된 매개 변수 값을 입력 하 고 추가 단추를 클릭 하 여 프로세스를 완료 합니다.


[![반환 된 결과 제한 합니다 추가 WHERE 절 대화 상자](using-parameterized-queries-with-the-sqldatasource-vb/_static/image2.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image3.png)

**그림 2**: 추가에서 반환 된 결과 제한할 `WHERE` 절 대화 상자 ([클릭 하 여 큰 이미지 보기](using-parameterized-queries-with-the-sqldatasource-vb/_static/image4.png))


매개 변수를 추가한 후 확인을 클릭 하 고 데이터 소스 구성 마법사로 돌아갑니다. 합니다 `SELECT` 마법사의 맨 아래에 문을 포함할지 이제는 `WHERE` 라는 매개 변수를 사용 하 여 절 `@UnitPrice`:


[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample3.sql)]

> [!NOTE]
> 여러 조건을 지정 하는 경우는 `WHERE` 추가 절 `WHERE` 절 대화 상자에서 마법사를 조인 하는 `AND` 연산자입니다. 포함 해야 하는 경우는 `OR` 에 `WHERE` 절 (같은 `WHERE UnitPrice <= @UnitPrice OR Discontinued = 1`) 작성 해야 합니다는 `SELECT` 문을 사용자 지정 SQL 문 화면을 통해.


(클릭이 어 마침을) SqlDataSource 구성 완료 하 고 SqlDataSource s 선언적 태그를 검사 합니다. 태그 이제는 `<SelectParameters>` 매개 변수는 원본을 확인 하는 컬렉션을 `SelectCommand`합니다.


[!code-aspx[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample4.aspx)]

때 SqlDataSource s `Select()` 메서드가 호출 되는 `UnitPrice` 매개 변수 값 (25.00)에 적용 됩니다는 `@UnitPrice` 의 매개 변수는 `SelectCommand` 데이터베이스로 전송 되기 전에 합니다. 결과 $25.00 작거나에서 반환 된 제품에만 `Products` 테이블입니다. 확인이 페이지에 GridView를 추가,이 데이터 원본에 바인딩하지 한 다음 브라우저를 통해 페이지를 봅니다. 그림 3에서 확인 된 $25.00, 보다 작거나 같은 나열 된 제품만 표시 됩니다.


[![이러한 제품 보다 작음 또는 $25.00 같음만 표시 됩니다.](using-parameterized-queries-with-the-sqldatasource-vb/_static/image3.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image5.png)

**그림 3**:만 해당 제품 보다 작음 또는 $25.00 같음 표시 됩니다 ([큰 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image6.png))


## <a name="step-2-adding-parameters-to-a-custom-sql-statement"></a>2 단계: 사용자 지정 SQL 문에 매개 변수 추가

사용자 지정 SQL 문을 추가 하는 때를 입력 합니다 `WHERE` 절 명시적으로 하거나 쿼리 작성기의 필터 셀에 값을 지정 합니다. 이 보여 주기 위해 s를 특정 임계값 보다 작은 가격은 GridView에 이러한 제품에만 표시할 수 있습니다. 입력란을 추가 하 여 시작 합니다 `ParameterizedQueries.aspx` 임계값이 사용자 로부터 수집 하는 페이지입니다. 집합 TextBox s `ID` 속성을 `MaxPrice`입니다. 단추 웹 컨트롤을 추가 하 고 설정 해당 `Text` 표시와 일치 하는 제품에는 속성입니다.

다음으로 GridView를 페이지로 끌어 및 스마트 태그에서를 작성 하기로 라는 새 SqlDataSource `ProductsFilteredByPriceDataSource`합니다. 데이터 소스 구성 마법사에서 지정 된 사용자 지정 SQL 문 또는 저장된 프로시저 화면 이동 됩니다. (그림 4 참조) 다음 쿼리를 입력 합니다.


[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample5.sql)]

쿼리 (직접 또는 쿼리 작성기를 통해)을 입력 한 후 다음을 클릭 합니다.


[![매개 변수 값 보다 작은 제품만 반환](using-parameterized-queries-with-the-sqldatasource-vb/_static/image4.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image7.png)

**그림 4**: 반환할만 해당 제품 보다 작음 또는 매개 변수 값을 같음 ([큰 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image8.png))


쿼리 매개 변수를 포함 하므로 마법사의 다음 화면 매개 변수 값의 원본에 대 한 요청입니다. 매개 변수 원본 드롭다운 목록에서 컨트롤을 선택 하 고 `MaxPrice` (s 텍스트 상자 컨트롤 `ID` 값) ControlID 드롭 다운 목록에서. 사용자가 모든 텍스트를 입력 하지 경우에서 사용 하는 선택적 기본 값을 입력할 수도 있습니다는 `MaxPrice` 텍스트 상자에 붙여넣습니다. 당분간, 기본 값을 입력 하지 마십시오.


[![텍스트 속성은 매개 변수 원본으로 사용 MaxPrice TextBox s](using-parameterized-queries-with-the-sqldatasource-vb/_static/image5.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image9.png)

**그림 5**: 합니다 `MaxPrice` 텍스트 상자 s `Text` 속성은 매개 변수 원본으로 사용 ([클릭 하 여 큰 이미지 보기](using-parameterized-queries-with-the-sqldatasource-vb/_static/image10.png))


다음을 클릭 하 여 데이터 소스 구성 마법사를 완료 한 다음 완료 합니다. GridView, 텍스트, 단추 및 SqlDataSource에 대 한 선언적 태그는 다음과 같습니다.


[!code-aspx[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample6.aspx)]

SqlDataSource s 내에서 매개 변수 `<SelectParameters>` 섹션은는 `ControlParameter`와 같은 추가적인 속성도 포함 `ControlID` 및 `PropertyName`합니다. 때 SqlDataSource s `Select()` 메서드가 호출 되는 `ControlParameter` 지정된 된 웹 컨트롤 속성의 값을 가져와 하 고 해당 매개 변수에 할당 합니다 `SelectCommand`합니다. 이 예제에서는 합니다 `MaxPrice` s 텍스트 속성으로 사용 되는 `@MaxPrice` 매개 변수 값입니다.

브라우저를 통해이 페이지를 보려면 1 분이 걸립니다. 먼저 페이지를 방문 하는 경우 또는 때마다는 `MaxPrice` 텍스트 상자에 GridView에 레코드가 표시 됩니다 값이 없는 합니다.


[![표시 되는 경우는 MaxPrice 텍스트 상자에 비어 있는 레코드가 없습니다.](using-parameterized-queries-with-the-sqldatasource-vb/_static/image6.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image11.png)

**그림 6**: 아니요 레코드는 경우 표시 합니다 `MaxPrice` 텍스트 상자가 비어 있지 않습니다 ([전체 크기 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image12.png))


제품이 표시 되는 이유는 기본적으로 매개 변수 값에 대 한 빈 문자열을 데이터베이스로 변환 하기 때문에 `NULL` 값입니다. 비교 이후 `[UnitPrice] <= NULL` 항상 평가 결과가 False로 반환 됩니다.

5.00 같은 텍스트 상자에 값을 입력 하 고 일치 하는 제품 표시 단추를 클릭 합니다. 포스트백에서 SqlDataSource GridView 해당 매개 변수 원본 중 하나는 변경에 알립니다. 따라서 GridView 제품 작거나 같거나 $5.00를 표시, SqlDataSource에 다시 바인딩합니다.


[![제품 보다 작음 또는 $5.00 같음 표시](using-parameterized-queries-with-the-sqldatasource-vb/_static/image7.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image13.png)

**그림 7**: 제품 보다 작음 또는 $5.00 같음 표시 됩니다 ([큰 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image14.png))


## <a name="initially-displaying-all-products"></a>처음에 모든 제품을 표시

페이지가 처음 로드 될 때 없는 제품을 표시 하는 대신 표시 해야 할 수도 있으므로 *모든* 제품입니다. 모든 제품을 나열 하는 한 가지 방법은 때마다는 `MaxPrice` TextBox 비어 있습니다. 일부 만드세요 높은 값으로 s 매개 변수 기본값을 설정 하는 것, 1000000 같은 있으므로 s는 Northwind Traders는 적이 있는 인벤토리 단가 가능성이 초과 1,000,000 달러를 초과 합니다. 그러나이 방법은 근시안적 이며 다른 상황에서 작동 하지 않을 수 있습니다.

이전 자습서- [선언적 매개 변수](../basic-reporting/declarative-parameters-vb.md) 하 고 [마스터/세부 정보 필터링으로 DropDownList](../masterdetail/master-detail-filtering-with-a-dropdownlist-vb.md) 유사한 문제에 직면 했습니다 했습니다. 우리의 솔루션 비즈니스 논리 계층에서이 논리를 배치 하는 것 이었습니다. BLL 들어오는 값을 검사 하는 특히 및 있었다면 `NULL` 또는 일부 예약 값, 호출 라우팅된 모든 레코드를 반환 하는 DAL 메서드. 매개 변수가 있는 SQL 문을 실행 하는 DAL 메서드를 호출 했습니다 들어오는 값이 일반 필터링 값이 었을 경우 `WHERE` 절 제공 된 값을 사용 하 여 합니다.

아쉽게도 SqlDataSource를 사용 하는 경우 아키텍처를 무시 했습니다. 대신 SQL 문을 지능적으로 하는 경우 모든 레코드를 가져오는 사용자 지정 해야 합니다 `@MaximumPrice` 매개 변수는 `NULL` 또는 예약 된 값입니다. 이 연습에서는 s 수 있습니다 따라서 경우는 `@MaximumPrice` 매개 변수 값과 같음 `-1.0`, 한 다음 *모든* 반환 되는 레코드의 (`-1.0` 제품이 없습니다 음수 있을수있으므로예약된값으로작동`UnitPrice`값). 이 작업을 수행한 다음 SQL 문을 사용할 수 있습니다.


[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample7.sql)]

이 `WHERE` 절에서 반환 *모든* 경우 기록 합니다 `@MaximumPrice` 매개 변수와 같으면 `-1.0`합니다. 매개 변수 값에는 없는 경우 `-1.0`, 제품만입니다 `UnitPrice` 보다 작거나 같음는 `@MaximumPrice` 매개 변수 값이 반환 됩니다. 기본값을 설정 하 여는 `@MaximumPrice` 매개 변수를 `-1.0`, 첫 번째 페이지 로드 시 (또는 때마다를 `MaxPrice` TextBox 비어 있습니다.), `@MaximumPrice` 의 값이 포함 됩니다 `-1.0` 모든 제품이 표시 됩니다.


[![이제 모든 제품이 표시 때 the MaxPrice 텍스트 상자가 비어 있는](using-parameterized-queries-with-the-sqldatasource-vb/_static/image8.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image15.png)

**그림 8**: 이제 모든 제품은 때 표시 되는 `MaxPrice` 텍스트 상자가 비어 있지 않습니다 ([전체 크기 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image16.png))


이 방법을 사용 하 여 주의 사항이 몇 가지 있습니다. 먼저, 매개 변수의 데이터 형식에 의해 유추는 실현 SQL 쿼리에서 사용량입니다. 변경 하는 경우는 `WHERE` 절 `@MaximumPrice = -1.0` 를 `@MaximumPrice = -1`, 런타임 정수 매개 변수를 처리 합니다. 그런 다음 할당 하려는 경우는 `MaxPrice` 텍스트 상자에 붙여넣습니다 (예: 5.00) 10 진수 값으로 5.00 정수로 변환할 수 없는 때문에 오류가 발생 합니다. 이 해결 하려면 하나를 사용 해야 `@MaximumPrice = -1.0` 에 `WHERE` 절 또는 아직 설정 합니다 `ControlParameter` s 개체 `Type` 10 진수로 속성.

추가 하 여 둘째, 합니다 `OR @MaximumPrice = -1.0` 에 `WHERE` 절, 쿼리 엔진에서 인덱스를 사용할 수 없습니다 `UnitPrice` (가정 하나가 있는) 테이블 검색에서는 그 결과로 합니다. 충분히 많은 수의 레코드의 경우 성능에 영향이 `Products` 테이블입니다. 더 나은 방법은 저장된 프로시저에이 논리를 이동 하는 것 위치는 `IF` 문을 수행 하거나를 `SELECT` 에서 쿼리를 `Products` 하지 않고 테이블을 `WHERE` 하나 또는 모든 레코드를 반환 해야 하는 경우 절입니다 `WHERE` 절만 포함 된 `UnitPrice` 조건을 인덱스를 사용할 수 있도록 합니다.

## <a name="step-3-creating-and-using-parameterized-stored-procedures"></a>3 단계: 만들기 및 매개 변수가 있는 저장된 프로시저를 사용 합니다.

저장된 프로시저는 저장된 프로시저 내에 정의 된 SQL 문을 지정에 사용할 수 있는 입력된 매개 변수 집합을 포함할 수 있습니다. 입력된 매개 변수를 받아들이는 저장된 프로시저를 사용 하 여 SqlDataSource를 구성할 때 이러한 매개 변수 값을 임시 SQL 문이 마찬가지로 동일한 기술을 사용 하 여 지정할 수 있습니다.

S let 라는 Northwind 데이터베이스의 새 저장된 프로시저 만들기를 설명 하기 위해 SqlDataSource에서 저장된 프로시저를 사용 하 여 `GetProductsByCategory`, 라는 매개 변수를 받아들이는 `@CategoryID` 모든 제품의 열을 반환 하 고 해당 `CategoryID` 열이 일치 `@CategoryID`합니다. 저장된 프로시저를 만들려면 서버 탐색기로 이동 하 고 드릴 다운을 `NORTHWND.MDF` 데이터베이스입니다. (서버 탐색기에 표시 하는 t don 가동 시킵니다 보기 메뉴로 이동 하 고 서버 탐색기 옵션을 선택 하 여.)

`NORTHWND.MDF` 데이터베이스, Stored Procedures 폴더를 마우스 오른쪽 단추로 클릭 하 고, 새 저장 프로시저 추가 선택 하 고 다음 구문을 입력 합니다.


[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample8.sql)]

저장된 프로시저를 저장 하려면 저장 아이콘 (또는 Ctrl + S)를 클릭 합니다. Stored Procedures 폴더에서 마우스 오른쪽 단추로 클릭 하 고 실행을 선택 하 여 저장된 프로시저를 테스트할 수 있습니다. 묻는 메시지가 나타납니다 s 저장된 프로시저 매개 변수에 대 한 (`@CategoryID`, 이런에서), 후 출력 창에는 결과 표시 되어야 합니다.


[![GetProductsByCategory 저장 프로시저를 사용 하 여 실행 하는 경우는 @CategoryID 1](using-parameterized-queries-with-the-sqldatasource-vb/_static/image9.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image17.png)

**그림 9**: 합니다 `GetProductsByCategory` 사용 하 여 실행 하는 경우 저장 프로시저를 `@CategoryID` 1 ([전체 크기 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image18.png))


이 저장된 프로시저를 사용 하 여 음료 범주를 GridView에 모든 제품을 전시 하기 s 수 있습니다. 페이지에 새 GridView를 추가 하 고 명명 된 새 SqlDataSource에 바인딩할 `BeverageProductsDataSource`합니다. 사용자 지정 SQL 문 또는 저장된 프로시저 화면 지정 계속, 저장 프로시저 라디오 단추를 선택 하 고, 선택는 `GetProductsByCategory` 드롭 다운 목록에서 프로시저를 저장 합니다.


[![GetProductsByCategory 선택 드롭다운 목록에서 프로시저를 저장 합니다.](using-parameterized-queries-with-the-sqldatasource-vb/_static/image10.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image19.png)

**그림 10**: 선택 된 `GetProductsByCategory` 드롭 다운 목록에서 저장 프로시저 ([클릭 하 여 큰 이미지 보기](using-parameterized-queries-with-the-sqldatasource-vb/_static/image20.png))


저장된 프로시저 입력된 매개 변수를 허용 하므로 (`@CategoryID`),이 매개 변수의 값에 대 한 원본을 지정 하도록 요청 다음을 클릭 합니다. 음료 `CategoryID` 1 이므로 매개 변수 원본 드롭다운 목록에 없음 두고 DefaultValue 텍스트 상자에 1을 입력 합니다.


[![하드 코드 된 값이 1 사용 하 여 음료 범주에서 제품을 반환 하려면](using-parameterized-queries-with-the-sqldatasource-vb/_static/image11.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image21.png)

**그림 11**: Hard-Coded 값 1 사용 하 여 음료 범주에서 제품을 반환할 ([큰 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image22.png))


저장된 프로시저, SqlDataSource s를 사용 하는 경우 다음 선언적 태그와 같이 `SelectCommand` 저장된 프로시저의 이름 속성 및 [ `SelectCommandType` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.selectcommandtype.aspx) 로 설정 된 `StoredProcedure`나타내는 `SelectCommand` 를 임시 SQL 문이 아니라 저장된 프로시저의 이름입니다.


[!code-aspx[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample9.aspx)]

브라우저에서 페이지를 테스트 합니다. 하지만 음료 범주에 속하는 제품만 표시 됩니다 *모든* 이후 제품의 필드가 표시 됩니다는 `GetProductsByCategory` 에서 열의 모든 저장된 프로시저 반환을 `Products` 테이블입니다. 수 없습니다, 그리고 물론 제한 하거나 GridView가의 열 편집 대화 상자에서 GridView에 표시 되는 필드를 사용자 지정 합니다.


[![음료 모두 표시](using-parameterized-queries-with-the-sqldatasource-vb/_static/image12.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image23.png)

**그림 12**: 모든는 음료 표시 됩니다 ([큰 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image24.png))


## <a name="step-4-programmatically-invoking-a-sqldatasource-sselectstatement"></a>4 단계: 프로그래밍 방식으로 SqlDataSource의`Select()`문

예제에서는 이전 자습서와이 자습서를 지금 나온 ve SqlDataSource 컨트롤을 GridView에 직접 바인딩한 합니다. 그러나 SqlDataSource 컨트롤의 데이터 프로그래밍 방식으로 액세스 하 고 수 코드에 열거 합니다. 이 기능은, 검사 데이터를 쿼리할 해야 하지만 안 표시 해야 하는 경우에 특히 유용할 수 있습니다. 모든 데이터베이스에 연결 하 여 명령을 지정 하 고 결과 검색 하는 ADO.NET 코드 상용구를 작성 하는 대신 SqlDataSource 단조로운이 코드를 처리 하도록 할 수 있습니다.

SqlDataSource s 사용 하 여 작업을 설명 하기 위해 데이터는 상사에 도달 하면 임의로 선택 된 범주 및 관련된 제품의 이름을 표시 하는 웹 페이지를 만들기 위한 요청을 사용 하 여 프로그래밍 방식으로, imagine. 즉, 사용자가이 페이지를 방문 하면 원하는 임의로에서 범주를 선택 하 여 `Categories` 테이블, 범주 이름을 표시 한 다음 해당 범주에 속하는 제품을 나열 합니다.

SqlDataSource 컨트롤을 두 개 하나에서 임의 범주를 선택 해야이 작업을 수행 하는 `Categories` 테이블과 다른 s 제품 범주를 가져옵니다. 이 단계에 임의 범주 레코드를 검색 하는 SqlDataSource를 구축해 보겠습니다. 5 단계 SqlDataSource 범주의 제품을 검색 하는 과정에 대해 살펴봅니다.

SqlDataSource를 추가 하 여 시작 `ParameterizedQueries.aspx` 설정 및 해당 `ID` 에 `RandomCategoryDataSource`입니다. 다음 SQL 쿼리를 사용할 수 있도록 구성 합니다.


[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample10.sql)]

`ORDER BY NEWID()` 임의 순서로 정렬 하는 레코드를 반환 합니다 (참조 [사용 하 여 `NEWID()` 임의로 정렬 레코드](http://www.sqlteam.com/item.asp?ItemID=8747)). `SELECT TOP 1` 결과 집합에서 첫 번째 레코드를 반환합니다. 종합적으로이 쿼리는 반환 합니다 `CategoryID` 및 `CategoryName` 단일, 임의로 선택 된 범주에서 열 값입니다.

S 범주를 표시할 `CategoryName` 값, 페이지 레이블 웹 컨트롤을 추가 하 고, 설정 해당 `ID` 속성을 `CategoryNameLabel`를 지울 및 해당 `Text` 속성입니다. SqlDataSource 컨트롤에서 데이터를 프로그래밍 방식으로 검색을 하려면 호출 해야 해당 `Select()` 메서드. [ `Select()` 메서드](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.select.aspx) 형식의 단일 입력 매개 변수 [ `DataSourceSelectArguments` ](https://msdn.microsoft.com/library/system.web.ui.datasourceselectarguments.aspx), 반환 되기 전에 4kb 되어 데이터를 해야 하는 방법을 지정 합니다. 이 데이터를 정렬 및 필터링에 대 한 지침을 포함할 수 있습니다 하 고 데이터 정렬 또는 SqlDataSource 컨트롤에서 데이터를 페이징 하는 경우 웹 컨트롤에 의해 사용 됩니다. 예를 들어 하지만 반환 되기 전에 수정할 데이터 t 필요 하지 하 고 있으므로 전달 된 `DataSourceSelectArguments.Empty` 개체입니다.

합니다 `Select()` 메서드를 구현 하는 개체를 반환 합니다. `IEnumerable`합니다. 정확한 형식이 반환 SqlDataSource 컨트롤 s의 값에 따라 달라 집니다 [ `DataSourceMode` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.datasourcemode.aspx)합니다. 이전 자습서에서 설명 했 듯이이 속성의 값으로 설정할 수 있습니다 `DataSet` 또는 `DataReader`합니다. 경우로 `DataSet`, `Select()` 메서드가 반환 되는 [DataView](https://msdn.microsoft.com/library/01s96x0z.aspx) 로 설정 하면 개체 `DataReader`, 구현 하는 개체를 반환 [ `IDataReader` ](https://msdn.microsoft.com/library/system.data.idatareader.aspx)합니다. 있으므로 합니다 `RandomCategoryDataSource` SqlDataSource에 해당 `DataSourceMode` 속성이로 설정 `DataSet` (기본값), 우리가 사용할 DataView 개체입니다.

다음 코드에서 레코드를 검색 하는 방법을 보여 줍니다 합니다 `RandomCategoryDataSource` SqlDataSource DataView로 읽는 방법 뿐만 아니라는 `CategoryName` DataView의 첫 번째 행의 열 값:


[!code-vb[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample11.vb)]

`randomCategoryView(0)` 첫 번째 개체가 반환 `DataRowView` DataView에 있습니다. `randomCategoryView(0)("CategoryName")` 값을 반환 합니다 `CategoryName` 이 첫 번째 행의 열입니다. DataView는 느슨한 형 note 합니다. 특정 열 값을 참조 하는 열 이름 (이 경우 CategoryName) 문자열로 전달 해야 합니다. 그림 13에 표시 되는 메시지를 표시 합니다 `CategoryNameLabel` 페이지를 보고 하는 경우. 표시 되는 실제 범주 이름에서 임의로 선택은 물론,는 `RandomCategoryDataSource` 포스트백 등 페이지를 방문할 때마다에서 SqlDataSource 합니다.


[![이름은 임의로 선택한 범주 s](using-parameterized-queries-with-the-sqldatasource-vb/_static/image13.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image25.png)

**그림 13**: The 임의로 선택한 범주의 이름이 표시 됩니다 ([큰 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image26.png))


> [!NOTE]
> SqlDataSource가 제어 하는 경우 `DataSourceMode` 속성으로 설정 된 `DataReader`의 반환 값을 `Select()` 메서드를 캐스팅 해야 `IDataReader`합니다. 읽을 수는 `CategoryName` d에서는 첫 번째 행의 열 값이 같은 코드를 사용 합니다.


[!code-vb[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample12.vb)]

SqlDataSource와 함께 무작위로 선택할 범주를 범주의 제품을 나열 하는 GridView를 추가 하려면 준비 된 것입니다.

> [!NOTE]
> 범주의 이름에 표시할 레이블 웹 컨트롤을 사용 하는 대신 수에 추가 했습니다 FormView 또는 DetailsView 페이지 SqlDataSource에 바인딩하지 합니다. 그러나 수 SqlDataSource s를 프로그래밍 방식으로 호출 하는 방법에 대해 레이블을 사용 하 여, `Select()` 문 및 코드에서 결과 데이터를 사용 하 여 작업 합니다.


## <a name="step-5-assigning-parameter-values-programmatically"></a>5 단계: 매개 변수 값을 프로그래밍 방식으로 할당

모든 예제에서는이 자습서에서는 지금까지 본 ve 하드 코드 된 매개 변수 값 또는 미리 정의 된 매개 변수 원본 (고 페이지의 웹 컨트롤, querystring 값) 중 하나에서 가져온 하나 사용 합니다. 그러나 SqlDataSource 컨트롤 s 매개 변수를 프로그래밍 방식으로 설정할 수도 있습니다. 현재 예제를 완료 하려면 모든 지정된 된 범주에 속하는 제품을 반환 하는 SqlDataSource 필요 합니다. 이 SqlDataSource 해야는 `CategoryID` 기반으로 하는 매개 변수 값을 설정 해야 합니다 `CategoryID` 에서 반환 된 열 값을 `RandomCategoryDataSource` SqlDataSource에서를 `Page_Load` 이벤트 처리기.

페이지에 GridView를 추가 하 여 시작 하 고 명명 된 새 SqlDataSource에 바인딩할 `ProductsByCategoryDataSource`합니다. 3 단계에서에서 수행한 마찬가지로, SqlDataSource 호출 하도록 구성 된 `GetProductsByCategory` 저장 프로시저입니다. None, 매개 변수 원본 드롭다운 목록에서 설정 된 채로 하지만 프로그래밍 방식으로 기본 값이 설정으로 기본 값을 입력 하지 않으면.


[![매개 변수 원본 또는 기본 값을 지정 하지 않으면](using-parameterized-queries-with-the-sqldatasource-vb/_static/image14.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image27.png)

**그림 14**: 매개 변수 원본 또는 기본 값을 지정 하지 않으면 ([큰 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image28.png))


SqlDataSource 마법사를 완료 한 후 결과 선언적 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample13.aspx)]

할당할 수 있습니다 합니다 `DefaultValue` 의 합니다 `CategoryID` 프로그래밍 방식으로 매개 변수는 `Page_Load` 이벤트 처리기:


[!code-vb[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample14.vb)]

이 또한을 사용 하 여 페이지를 임의로 선택 된 범주와 관련 된 제품이 표시 되는 GridView를 포함 합니다.


[![매개 변수 원본 또는 기본 값을 지정 하지 않으면](using-parameterized-queries-with-the-sqldatasource-vb/_static/image15.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image29.png)

**그림 15**: 매개 변수 원본 또는 기본 값을 지정 하지 않으면 ([큰 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image30.png))


## <a name="summary"></a>요약

SqlDataSource는 페이지 개발자가 매개 변수 값을 가진 하드 코드 된, 미리 정의 된 매개 변수 원본에서 가져온 하거나 수 할당을 프로그래밍 방식으로 매개 변수가 있는 쿼리를 정의할 수 있습니다. 이 자습서에서는 임시 SQL 쿼리 및 저장된 프로시저 모두에 대 한 데이터 소스 구성 마법사에서 매개 변수가 있는 쿼리를 작성 하는 방법에 살펴보았습니다. 또한 살펴보았습니다 하드 코드 된 매개 변수 원본에 매개 변수 원본으로 웹 컨트롤을 사용 하 고 프로그래밍 방식으로 매개 변수 값을 지정 합니다.

같은 ObjectDataSource를 사용 하 여 SqlDataSource 또한 기능을 제공 해당 기본 데이터를 수정 합니다. 다음 자습서에서 살펴보겠습니다 정의 하는 방법 `INSERT`, `UPDATE`, 및 `DELETE` SqlDataSource 사용 하 여 문입니다. 이러한 문은 추가한 후 삽입, 편집 및 삭제 기능 GridView, DetailsView 및 FormView 컨트롤에 내재 된 기본 제공을 활용 하 여 수 있습니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Scott와을 클라이드, Randell Schmidt 및 박 단은 Pespisa 되었습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](querying-data-with-the-sqldatasource-control-vb.md)
> [다음](inserting-updating-and-deleting-data-with-the-sqldatasource-vb.md)
