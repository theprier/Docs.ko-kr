---
uid: web-forms/overview/data-access/basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-vb
title: 프로그래밍 방식으로 ObjectDataSource의 매개 변수 값 (VB)를 설정 | Microsoft Docs
author: rick-anderson
description: 이 자습서는 단일 입력된 매개 변수를 수락 하 고 데이터를 반환 하는 BLL 및 DAL에 메서드를 추가 하는 방법을 살펴보겠습니다. 이 예제에서는이 매개 변수를 설정 하 고...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/31/2010
ms.topic: article
ms.assetid: 0ecb03b6-52a0-4731-8c7a-436391d36838
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-vb
msc.type: authoredcontent
ms.openlocfilehash: e2d0afa6616d936d2c8a2c76ca51ee1995040644
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37396269"
---
<a name="programmatically-setting-the-objectdatasources-parameter-values-vb"></a>ObjectDataSource의 매개 변수 값 (VB)를 프로그래밍 방식으로 설정
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_6_VB.exe) 또는 [PDF 다운로드](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/datatutorial06vb1.pdf)

> 이 자습서는 단일 입력된 매개 변수를 수락 하 고 데이터를 반환 하는 BLL 및 DAL에 메서드를 추가 하는 방법을 살펴보겠습니다. 이 예제에서는이 매개 변수를 프로그래밍 방식으로 설정 됩니다.


## <a name="introduction"></a>소개

설명한 것 처럼 합니다 [이전 자습서](declarative-parameters-vb.md), 여러 옵션을 선언적으로 ObjectDataSource의 메서드에 매개 변수 값을 전달 하는 데 사용할 수 있습니다. 매개 변수 값을 하드 코딩 된 경우 페이지의 웹 컨트롤에서 제공 하거나 데이터 원본에서 읽을 수 있는 다른 원본에 `Parameter` 개체, 예를 들어, 코드 줄도 작성 하지 않고 값 입력된 매개 변수를 바인딩할 수 있습니다.

그러나 기본 제공 데이터 원본 중 하나에 의해 아직 고려 출처 로부터 매개 변수 값을 제공 하는 경우 경우가 있을 수 있습니다 `Parameter` 개체입니다. 현재 로그온 된 방문자의 사용자 id에 따라 매개 변수를 설정 해야 사이트 사용자 계정을 지원 되는 경우 또는 ObjectDataSource의 기본 개체의 메서드에 따라 보내기 전에 매개 변수 값을 사용자 지정 해야 할 수 있습니다.

때마다 ObjectDataSource의 `Select` 메서드가 호출 되는 ObjectDataSource 먼저 발생 합니다. 해당 [선택 하면 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selecting%28VS.80%29.aspx). ObjectDataSource의 기본 개체의 메서드에 다음 호출 됩니다. ObjectDataSource의 완료 되 면 [선택한 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selected%28VS.80%29.aspx) 발생 합니다 (그림 1에서는이 이벤트 순서는을 설명 하는 데 사용). ObjectDataSource의 기본 개체의 메서드에 전달 된 매개 변수 값을 설정 하거나에 대 한 이벤트 처리기에서 사용자 지정할 수는 `Selecting` 이벤트입니다.


[![ObjectDataSource의 선택 및 선택 하면 이벤트 발생 하기 전과 후 해당 기본 개체의 메서드는 호출](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image2.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image1.png)

**그림 1**: The ObjectDataSource `Selected` 하 고 `Selecting` 이벤트 실행 전과 후 해당 기본 개체의 메서드가 호출 됩니다 ([전체 크기 이미지를 보려면 클릭](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image3.png))


이 자습서에서는 단일 입력된 매개 변수를 허용 하는 BLL 및 DAL에 메서드 추가 살펴보겠습니다 `Month`, 형식 `Integer` 반환는 `EmployeesDataTable` 가 채용 연주기 일에 지정 된 해당 직원이 데이터로 채운 개체 `Month`. 이 예제는 현재 월에 따라 프로그래밍 방식으로 "직원 기념일 이번 달 합니다." 목록을 보여 주는이 매개 변수 설정

이제 시작 하겠습니다.

## <a name="step-1-adding-a-method-toemployeestableadapter"></a>1 단계: 추가 방법`EmployeesTableAdapter`

이러한 직원을 검색 하는 수단을 추가 해야 하는 첫 번째 예제에 대 한 해당 `HireDate` 지정된 된 월에 발생 합니다. 메서드를 먼저 만들어야 하는 아키텍처에 따라이 기능을 제공 하도록 `EmployeesTableAdapter` 적절 한 SQL 문이 매핑되는 합니다. 이 작업을 수행 하려면 Northwind 형식화 된 데이터 집합을 열어 시작 합니다. 마우스 오른쪽 단추로 클릭는 `EmployeesTableAdapter` 레이블을 지정 하 고 쿼리 추가 선택 합니다.


[![새 쿼리를 EmployeesTableAdapter 추가](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image5.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image4.png)

**그림 2**: 새 쿼리를 추가 합니다 `EmployeesTableAdapter` ([클릭 하 여 큰 이미지 보기](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image6.png))


행을 반환 하는 SQL 문을 추가 하려면 선택 합니다. 지정 도달 하면를 `SELECT` 문의 기본 화면 `SELECT` 문을 `EmployeesTableAdapter` 이미 로드 됩니다. 에 추가 합니다 `WHERE` 절: `WHERE DATEPART(m, HireDate) = @Month`합니다. [DATEPART](https://msdn.microsoft.com/library/ms174420.aspx) 는 특정 날짜 부분을 반환 하는 T-SQL 함수는 `datetime` 형식에 사용 하 고이 경우 `DATEPART` 월을 반환 하는 `HireDate` 열입니다.


[![반환 된 행 위치의 HireDate 열만 보다 작거나 같음는 @HiredBeforeDate 매개 변수](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image8.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image7.png)

**그림 3**: 반환만 해당 행 위치를 `HireDate` 열이 보다 작거나 같음 합니다 `@HiredBeforeDate` 매개 변수 ([클릭 하 여 큰 이미지 보기](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image9.png))


마지막으로 변경 합니다 `FillBy` 하 고 `GetDataBy` 메서드 이름을 `FillByHiredDateMonth` 및 `GetEmployeesByHiredDateMonth`, 각각.


[![FillBy GetDataBy 보다 더 적절 한 메서드 이름 선택](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image11.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image10.png)

**그림 4**: 선택 더 적절 한 메서드 이름을 보다 `FillBy` 하 고 `GetDataBy` ([클릭 하 여 큰 이미지 보기](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image12.png))


데이터 집합의 디자인 화면으로 돌아와 마법사를 완료 하려면 마침을 클릭 합니다. `EmployeesTableAdapter` 이제 지정된 된 월에 고용 된 직원에 액세스 하기 위한 메서드 집합을 새 포함 됩니다.


[![새 메서드가 데이터 집합의 디자인 화면에 표시](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image14.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image13.png)

**그림 5**:의 새 메서드가 표시 된 데이터 집합의 디자인 화면에서 ([큰 이미지를 보려면 클릭](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image15.png))


## <a name="step-2-adding-thegetemployeesbyhireddatemonthmonthmethod-to-the-business-logic-layer"></a>2 단계: 추가 된`GetEmployeesByHiredDateMonth(month)`비즈니스 논리 계층 방법

이 응용 프로그램 아키텍처는 별도 계층 비즈니스 논리 및 데이터 액세스 논리를 있으므로 지정된 된 날짜 전에 고용 된 직원을 검색 하는 DAL까지 호출 하는 BLL에 메서드를 추가 해야 합니다. 열기는 `EmployeesBLL.vb` 파일과 다음 메서드를 추가 합니다.


[!code-vb[Main](programmatically-setting-the-objectdatasource-s-parameter-values-vb/samples/sample1.vb)]

이 클래스에서 다른 메서드 마찬가지로 `GetEmployeesByHiredDateMonth(month)` 간단히 DAL에를 호출 하 고 결과 반환 합니다.

## <a name="step-3-displaying-employees-whose-hiring-anniversary-is-this-month"></a>3 단계: 직원 채용 된 연주기 일은 이번 달 표시

이 예제에 대 한 마지막 단계 직원 채용 된 연주기 일이 월이 표시 됩니다. 하기 위한 GridView를 추가 하 여 시작 합니다 `ProgrammaticParams.aspx` 페이지를 `BasicReporting` 폴더 새 ObjectDataSource 데이터 원본으로 추가 합니다. ObjectDataSource를 사용 하 여 구성 합니다 `EmployeesBLL` 클래스를 `SelectMethod` 로 `GetEmployeesByHiredDateMonth(month)`합니다.


[![EmployeesBLL 클래스 사용](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image17.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image16.png)

**그림 6**: 사용 된 `EmployeesBLL` 클래스 ([클릭 하 여 큰 이미지 보기](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image18.png))


[![The GetEmployeesByHiredDateMonth(month)에서 선택 메서드](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image20.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image19.png)

**그림 7**: Select From 합니다 `GetEmployeesByHiredDateMonth(month)` 메서드 ([클릭 하 여 큰 이미지 보기](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image21.png))


최종 화면에서는 제공 하는 `month` 매개 변수 값의 원본입니다. 하므로이 값을 프로그래밍 방식으로 설정 됩니다 None 기본 매개 변수 원본 설정 된 채로 두고 옵션 하 고 마침을 클릭 합니다.


[![매개 변수 원본 집합을 None으로 유지](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image23.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image22.png)

**그림 8**: none 매개 변수 원본 집합을 그대로 둡니다 ([큰 이미지를 보려면 클릭](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image24.png))


이 만들어집니다.는 `Parameter` 개체는 ObjectDataSource에 `SelectParameters` 값이 지정 되지 않은 컬렉션입니다.


[!code-aspx[Main](programmatically-setting-the-objectdatasource-s-parameter-values-vb/samples/sample2.aspx)]

이 값을 프로그래밍 방식으로 설정 하려면 ObjectDataSource의에 대 한 이벤트 처리기를 생성 해야 `Selecting` 이벤트입니다. 이를 위해 디자인 보기로 이동 하 고 ObjectDataSource를 두 번 클릭 합니다. 또는 ObjectDataSource를 선택 하 고 속성 창으로 이동 하 고 번개 모양 아이콘을 클릭 합니다. 다음으로 두 번 클릭 하는 텍스트 상자 옆에 `Selecting` 이벤트 또는 이벤트 처리기는 데 사용할 이름을 입력 합니다. 세 번째 옵션으로 ObjectDataSource를 선택 하 여 이벤트 처리기를 만들 수 있습니다 및 해당 `Selecting` 페이지의 코드 숨김 클래스의 맨 위에 있는 두 개의 드롭다운 목록에서 이벤트입니다.


![웹 컨트롤의 이벤트를 나열 하려면 속성 창의 번개 모양 아이콘 클릭](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image25.png)

**그림 9**: 웹 컨트롤의 이벤트를 나열 하려면 속성 창의 번개 모양 아이콘 클릭


세 방법 모두 ObjectDataSource의에 대 한 새 이벤트 처리기를 추가 `Selecting` 페이지의 코드 숨김 클래스에는 이벤트입니다. 이 이벤트 처리기에서는 읽고 쓸 수 있습니다 사용 하 여 매개 변수 값 `e.InputParameters(parameterName)`여기서 *`parameterName`* 의 값인는 `Name` 특성을 `<asp:Parameter>` 태그 (는 `InputParameters` 컬렉션 일 수도 있습니다 서 수에서 같이 인덱싱된 `e.InputParameters(index)`). 설정 하는 `month` 은 현재 월, 매개 변수는 다음을 추가 합니다 `Selecting` 이벤트 처리기:


[!code-vb[Main](programmatically-setting-the-objectdatasource-s-parameter-values-vb/samples/sample3.vb)]

브라우저를 통해이 페이지를 방문할 때 보면 하나만 해당 직원 (3 월) 이번 달에 고용 된 회사 1994 되었으며는 Laura Callahan 합니다.


[![해당 기념일 이번 달 나와 직원](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image27.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image26.png)

**그림 10**: 이러한 직원 있는 기념일이 월 표시 됩니다 ([큰 이미지를 보려면 클릭](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image28.png))


## <a name="summary"></a>요약

ObjectDataSource의 매개 변수 값 일반적으로 설정할 수 있습니다 선언적으로 코드 줄을 요구 하지 않고 하는 동안 매개 변수 값을 프로그래밍 방식으로 설정 하기 쉽습니다. 수행 해야 됩니다 ObjectDataSource의에 대 한 이벤트 처리기를 만듭니다 `Selecting` 기본 개체의 메서드 호출 및 하나 이상의 매개 변수를 통해 값을 수동으로 설정 되기 전에 발생 하는 이벤트를 `InputParameters` 컬렉션입니다.

이 자습서에는 기본 보고 섹션으로를 마칩니다. 합니다 [다음 자습서](../masterdetail/master-detail-filtering-with-a-dropdownlist-vb.md) 는에서는 데이터를 필터링 하는 방문자를 허용 하는 기술을 확인 하 고 세부 정보 보고서로 마스터 보고서에서 드릴 다운 필터링 및 마스터-세부 시나리오 섹션을 시작 합니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Hilton giesenow와 함께 했습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](declarative-parameters-vb.md)
