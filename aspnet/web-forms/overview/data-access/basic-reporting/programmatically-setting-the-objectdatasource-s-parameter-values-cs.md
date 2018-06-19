---
uid: web-forms/overview/data-access/basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-cs
title: ObjectDataSource의 매개 변수 값 (C#)를 프로그래밍 방식으로 설정 | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 DAL 및 BLL 단일 입력된 매개 변수를 허용 하 고 데이터를 반환 하는 메서드를 추가 하는 방법을 살펴보겠습니다. 이 예제에서는이 매개 변수를 설정 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/31/2010
ms.topic: article
ms.assetid: 1c4588bb-255d-4088-b319-5208da756f4d
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-cs
msc.type: authoredcontent
ms.openlocfilehash: 1bd1fd63e5aae74459675d45dd399e449d7897b8
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30875684"
---
<a name="programmatically-setting-the-objectdatasources-parameter-values-c"></a>ObjectDataSource의 매개 변수 값 (C#)를 프로그래밍 방식으로 설정
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_6_CS.exe) 또는 [PDF 다운로드](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/datatutorial06cs1.pdf)

> 이 자습서에서는 DAL 및 BLL 단일 입력된 매개 변수를 허용 하 고 데이터를 반환 하는 메서드를 추가 하는 방법을 살펴보겠습니다. 이 예제에서는 프로그래밍 방식으로이 매개 변수를 설정 합니다.


## <a name="introduction"></a>소개

설명한 것 처럼는 [이전 자습서](declarative-parameters-cs.md), 다양 한 옵션을 선언적으로 ObjectDataSource의 메서드에 매개 변수 값을 전달 하기 위해 사용할 수 있습니다. 페이지에서 웹 컨트롤에서 제공 되는지, 아니면 데이터 원본에서 읽을 수 있는 다른 모든 소스에 매개 변수 값은 하드 코딩 된 경우 `Parameter` 개체, 예를 들어 코드 줄도 작성 하지 않고 값 입력된 매개 변수에 바인딩할 수 있습니다.

그러나 기본 제공 데이터 원본 중 하나에서 담당 하 게 아직 일부 소스에서 매개 변수 값이 되 면 경우가 있을 수 있습니다 `Parameter` 개체입니다. 사이트에 사용자 계정을 지원 되는 경우 하고자 할 수 있습니다는 현재 로그인 id입니다. 방문자의 사용자에 따라 매개 변수 설정 또는 ObjectDataSource의 기본 개체의 메서드에 따라 보내기 전에 매개 변수 값을 사용자 지정 해야 합니다.

때마다 ObjectDataSource의 `Select` 메서드가 호출 되는 ObjectDataSource 먼저 발생 합니다. 해당 [Selecting 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selecting%28VS.80%29.aspx)합니다. 그런 다음 ObjectDataSource의 기본 개체의 메서드를 호출 합니다. ObjectDataSource의 완료 되 면 [선택한 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selected%28VS.80%29.aspx) (그림 1에서는이 이벤트의이 시퀀스를 설명)에 발생 합니다. ObjectDataSource의 기본 개체의 메서드에 전달 된 매개 변수 값을 설정 하거나에 대 한 이벤트 처리기에서 사용자 지정할 수는 `Selecting` 이벤트입니다.


[![ObjectDataSource의 선택 항목 및 선택 하면 이벤트 화재 전과 후 해당 기본 개체의 메서드 호출](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image2.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image1.png)

**그림 1**: The ObjectDataSource `Selected` 및 `Selecting` 이벤트 화재 전과 후 해당 기본 개체의 메서드가 호출 됩니다 ([전체 크기 이미지를 보려면 클릭](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image3.png))


이 자습서에서는 DAL 및 BLL 단일 입력된 매개 변수를 허용 하는 메서드를 추가 살펴보겠습니다 `Month`, 형식의 `int` 반환는 `EmployeesDataTable` 로 지정 된 채용 기념일이 있는 직원 `Month`. 예에서 사용 하는 프로그래밍 방식으로 기반으로 현재 월, "직원 기념일 이번 달입니다." 목록을 보여 주는이 매개 변수를 설정 합니다.

이제 시작 하겠습니다.

## <a name="step-1-adding-a-method-toemployeestableadapter"></a>1 단계:에 메서드 추가`EmployeesTableAdapter`

이러한 직원을 검색 하는 수단을 추가 해야 하는 첫 번째 예제에 대 한 해당 `HireDate` 지정 된 월에서 발생 했습니다. 메서드를 먼저 만들어야 하는 아키텍처에 따라이 기능을 제공 하려면 `EmployeesTableAdapter` 적절 한 SQL 문을에 매핑되는 합니다. 이를 위해 Northwind 형식화 된 데이터 집합을 열어 시작 합니다. 마우스 오른쪽 단추로 클릭는 `EmployeesTableAdapter` 레이블 지정 및 Query 추가 선택 합니다.


[![EmployeesTableAdapter에 새 쿼리 추가](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image5.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image4.png)

**그림 2**: 새 쿼리를 추가 `EmployeesTableAdapter` ([전체 크기 이미지를 보려면 클릭](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image6.png))


행을 반환 하는 SQL 문을 추가 하려면 선택 합니다. 지정 나타나면는 `SELECT` 문 기본 화면 `SELECT` 문을 `EmployeesTableAdapter` 이미 로드 됩니다. 에 추가 하면는 `WHERE` 절: `WHERE DATEPART(m, HireDate) = @Month`합니다. [DATEPART](https://msdn.microsoft.com/library/ms174420.aspx) 의 특정 날짜 부분을 반환 하는 T-SQL 함수는 `datetime` 형식;을 사용 하 여이 예제의 `DATEPART` 의 월을 반환 하는 `HireDate` 열입니다.


[![반환 된 행 위치 HireDate 열만 보다 작거나 같음는 @HiredBeforeDate 매개 변수](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image8.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image7.png)

**그림 3**: 반환만 해당 행에는 `HireDate` 열 보다 작거나 같음는 `@HiredBeforeDate` 매개 변수 ([전체 크기 이미지를 보려면 클릭](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image9.png))


마지막으로 변경 된 `FillBy` 및 `GetDataBy` 메서드 이름 `FillByHiredDateMonth` 및 `GetEmployeesByHiredDateMonth`각각.


[![FillBy GetDataBy 보다 더 적절 한 메서드 이름을 선택 합니다.](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image11.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image10.png)

**그림 4**: 선택 더 적절 한 메서드 이름 보다 `FillBy` 및 `GetDataBy` ([전체 크기 이미지를 보려면 클릭](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image12.png))


마법사를 완료 하는 데이터 집합의 디자인 화면으로 돌아갑니다 마침을 클릭 합니다. `EmployeesTableAdapter` 새 지정 된 월에 고용 된 직원에 액세스 하기 위한 메서드 집합을 포함 해야 합니다.


[![새 메서드가 데이터 집합의 디자인 화면에 표시](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image14.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image13.png)

**그림 5**: The 새 메서드가에 표시 된 데이터 집합 디자인 화면 ([전체 크기 이미지를 보려면 클릭](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image15.png))


## <a name="step-2-adding-thegetemployeesbyhireddatemonthmonthmethod-to-the-business-logic-layer"></a>2 단계: 추가 된`GetEmployeesByHiredDateMonth(month)`비즈니스 논리 계층 메서드

이 응용 프로그램 아키텍처는 별도 계층 비즈니스 논리 및 데이터에 대 한 액세스 논리를 지정된 된 날짜 전에 고용 된 직원을 검색에 대 한 호출 DAL 아래로 우리의 BLL에 메서드를 추가 해야 합니다. 열기는 `EmployeesBLL.cs` 파일을 다음 메서드를 추가 합니다.


[!code-csharp[Main](programmatically-setting-the-objectdatasource-s-parameter-values-cs/samples/sample1.cs)]

이 클래스에는 다른 메서드의 경우와 마찬가지로 `GetEmployeesByHiredDateMonth(month)` DAL 단순히 호출 하 고 결과 반환 합니다.

## <a name="step-3-displaying-employees-whose-hiring-anniversary-is-this-month"></a>3 단계: 직원 채용 된 기념일은 이번 달 표시

이 예제에 대 한 마지막 단계 인 채용 기념일은 이번 달의 직원을 표시 하는 것입니다. GridView에 추가 하 여 시작는 `ProgrammaticParams.aspx` 페이지에 `BasicReporting` 폴더 새 ObjectDataSource 데이터 원본으로 추가 합니다. ObjectDataSource 사용 하도록 구성 된 `EmployeesBLL` 클래스와 `SelectMethod` 로 설정 `GetEmployeesByHiredDateMonth(month)`합니다.


[![EmployeesBLL 클래스를 사용 하 여](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image17.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image16.png)

**그림 6**: 사용 된 `EmployeesBLL` 클래스 ([전체 크기 이미지를 보려면 클릭](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image18.png))


[![GetEmployeesByHiredDateMonth(month)에서 선택 메서드](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image20.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image19.png)

**그림 7**: Select From는 `GetEmployeesByHiredDateMonth(month)` 메서드 ([전체 크기 이미지를 보려면 클릭](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image21.png))


마지막 화면 요청 제공 하는 `month` 매개 변수 값의 소스입니다. 하므로이 값을 프로그래밍 방식으로 설정 합니다 없음 기본 매개 변수 소스 설정한 두십시오 옵션 하 고 마침을 클릭 합니다.


[![None으로 매개 변수 원본 집합을 그대로 둡니다.](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image23.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image22.png)

**그림 8**: None으로 매개 변수가 소스 설정 유지 ([전체 크기 이미지를 보려면 클릭](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image24.png))


이렇게 하면 만들어집니다는 `Parameter` ObjectDataSource의에서 개체 `SelectParameters` 지정 된 값이 없는 컬렉션입니다.


[!code-aspx[Main](programmatically-setting-the-objectdatasource-s-parameter-values-cs/samples/sample2.aspx)]

이 값을 프로그래밍 방식으로 설정 하려면 ObjectDataSource의에 대 한 이벤트 처리기를 만들고 해야 `Selecting` 이벤트입니다. 이를 위해 디자인 보기로 이동 하 고는 ObjectDataSource를 두 번 클릭 합니다. 또는 ObjectDataSource를 선택 하 고 속성 창으로 이동 번개 모양 아이콘을 클릭 합니다. 다음으로, 하나에서 두 번 클릭 하 고 입력란 옆에 `Selecting` 이벤트 또는 이벤트 처리기는 데 사용할 이름을 입력 합니다.


![웹 컨트롤의 이벤트를 나열 하려면 속성 창에서 번개 모양 아이콘 클릭](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image25.png)

**그림 9**: 웹 컨트롤의 이벤트를 나열 하려면 속성 창에서 번개 모양 아이콘 클릭


ObjectDataSource의에 대 한 새 이벤트 처리기를 추가 하는 두 방법 모두 `Selecting` 페이지의 코드 숨김 클래스에는 이벤트입니다. 이 이벤트 처리기에서 우리 읽고 쓸 수를 사용 하 여 매개 변수 값에 `e.InputParameters[parameterName]`여기서 *`parameterName`* 의 값이는 `Name` 특성에 `<asp:Parameter>` 태그 (의 `InputParameters` 컬렉션 수도 있습니다 서 수에서 같이 인덱싱된 `e.InputParameters[index]`). 설정 하는 `month` 현재 월을 매개 변수는 다음을 추가 `Selecting` 이벤트 처리기.


[!code-csharp[Main](programmatically-setting-the-objectdatasource-s-parameter-values-cs/samples/sample3.cs)]

브라우저를 통해이 페이지를 방문 하는 경우 해당 하나만 직원 고용 이번 달 (년 3 월) 볼 수 있습니다 숙 선하라 1994 년 이후 회사로 연결 된 했습니다.


[![이번 달에 표시 된 해당 연주기 직원](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image27.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image26.png)

**그림 10**: 된 직원이 있는 기념일이 월 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image28.png))


## <a name="summary"></a>요약

코드 줄을 요구 하지 않고 ObjectDataSource의 매개 변수 값, 선언적 설정할 일반적으로 수도 있지만 매개 변수 값을 프로그래밍 방식으로 설정 하기 쉽습니다. ObjectDataSource의에 대 한 이벤트 처리기를 만들고가 해야 할 모든 `Selecting` 기본 개체의 메서드 호출 및 하나 이상의 매개 변수를 통해에 대 한 값을 수동으로 설정 되기 전에 발생 하는 이벤트는 `InputParameters` 컬렉션입니다.

이 자습서에는 기본 보고 섹션으로를 마칩니다. [다음 자습서](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md) 필터링 및 마스터-세부 시나리오 섹션은 데이터를 필터링 하는 방문자를 허용 하기 위한 기술을 살펴볼 알아보고 세부 정보 보고서에는 마스터 보고서에서 드릴 다운 하겠습니다를 시작 합니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Hilton Giesenow 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](declarative-parameters-cs.md)
> [다음](displaying-data-with-the-objectdatasource-vb.md)
