---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/debugging-stored-procedures-cs
title: 저장된 프로시저 (C#) 디버깅 | Microsoft Docs
author: rick-anderson
description: Visual Studio Professional 및 Team System edition 저장 디버깅 중단점을 설정 하 여 SQL Server 내에서 저장 프로시저의 단계를 허용 하는 중...
ms.author: riande
ms.date: 08/03/2007
ms.assetid: c655c324-2ffa-4c21-8265-a254d79a693d
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/debugging-stored-procedures-cs
msc.type: authoredcontent
ms.openlocfilehash: a377dde0c4ed25aed549ca1f3b8eeeecece79517
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41836345"
---
<a name="debugging-stored-procedures-c"></a>저장된 프로시저 디버깅 (C#)
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_74_CS.zip) 또는 [PDF 다운로드](debugging-stored-procedures-cs/_static/datatutorial74cs1.pdf)

> Visual Studio Professional 및 Team System edition 응용 프로그램 코드를 디버깅 하는 것 만큼 쉽습니다 저장된 프로시저를 디버깅 중단점을 설정 하 고 SQL Server 내에서 저장된 프로시저에 단계에서 할 수 있습니다. 이 자습서는 직접 데이터베이스 디버깅 및 응용 프로그램 저장된 프로시저의 디버깅 방법을 보여 줍니다.


## <a name="introduction"></a>소개

Visual Studio에는 다양 한 디버깅 환경을 제공 합니다. 몇 가지 키 입력 이나 마우스 클릭을 사용 하 여 해당 프로그램의 실행을 중지 하 고 해당 상태 및 제어 흐름을 검사 하려면 중단점을 사용 하 합니다. 응용 프로그램 코드를 디버깅 하는 함께 Visual Studio는 SQL Server 내에서 저장된 프로시저를 디버깅 하는 것에 대 한 지원을 제공 합니다. ASP.NET 코드 숨김 클래스 또는 비즈니스 논리 계층 클래스의 코드 내에서 중단점을 설정 하는 것 처럼 하므로 너무 이러한 내에 배치할 수 저장된 프로시저입니다.

이 자습서를 한 단계씩 실행할 저장된 프로시저 내 Visual Studio 서버 탐색기에서도 적중 되는 중단점을 설정 하려면 저장된 프로시저가 호출 될 때 실행 중인 ASP.NET 응용 프로그램에서 방법과 하는 방법을 살펴보겠습니다.

> [!NOTE]
> 그러나 저장된 프로시저 수만 한 단계씩 하 고 Visual Studio의 Professional 버전과 Team 시스템을 통해 디버깅 합니다. 표준 버전의 Visual Studio 또는 Visual Web Developer를 사용 하는 경우에 따라 읽기에서는 저장된 프로시저를 디버깅 하는 데 필요한 단계를 안내 하지만 컴퓨터에 이러한 단계를 복제할 수 없습니다 시작 수 있습니다.


## <a name="sql-server-debugging-concepts"></a>SQL Server 디버깅 개념

Microsoft SQL Server 2005와의 통합을 제공 하도록 설계 되었습니다 합니다 [공용 언어 런타임 (CLR)](https://msdn.microsoft.com/netframework/aa497266.aspx), 하는 모든.NET 어셈블리에서 사용 하는 런타임입니다. 따라서 SQL Server 2005는 관리 되는 데이터베이스 개체를 지원합니다. 즉, C# 클래스의 메서드로 저장된 프로시저 및 사용자 정의 함수 (Udf)와 같은 데이터베이스 개체를 만들 수 있습니다. 이렇게 하면 이러한 저장된 프로시저 및 Udf.NET framework에서 및 사용자 고유의 사용자 지정 클래스에서 기능을 활용할 수 있습니다. 물론, SQL Server 2005는 또한 T-SQL 데이터베이스 개체에 대 한 지원을 제공합니다.

SQL Server 2005에는 T-SQL 및 관리 되는 데이터베이스 개체에 대 한 디버깅 지원을 제공합니다. 그러나 이러한 개체를 통해 팀 시스템과 Visual Studio 2005 Professional edition만 디버깅할 수 있습니다. 이 자습서에서는 T-SQL 데이터베이스 개체를 디버깅을 살펴보겠습니다. 후속 자습서는 관리 되는 데이터베이스 개체 디버깅 살펴봅니다.

[개요의 T-SQL 및 SQL Server 2005의 CLR 디버깅](https://blogs.msdn.com/sqlclr/archive/2006/06/29/651644.aspx) 에서 블로그 항목은 [SQL Server 2005 CLR 통합 팀](https://blogs.msdn.com/sqlclr/default.aspx) Visual Studio에서 SQL Server 2005 개체를 디버깅 하는 세 가지 방법으로 강조 표시 합니다.

- **직접 데이터베이스 디버깅 (DDD)** -서버 탐색기 저장된 프로시저 및 Udf와 같은 T-SQL 데이터베이스 개체를 한 단계씩 실행할 수 있습니다. 1 단계에서에서 DDD를 살펴보겠습니다.
- **응용 프로그램 디버깅** -데이터베이스 개체 내에서 중단점을 설정 하 고 ASP.NET 응용 프로그램을 실행 한 다음 수 있습니다. 데이터베이스 개체를 실행 하면 중단점이 적중 됩니다 및 디버거를 제어를 설정 합니다. 응용 프로그램 디버깅에서는 실행할 수 없습니다는 데이터베이스 개체에 응용 프로그램 코드에서 참고 합니다. 에서는 명시적으로 설정 해야 중단점 해당 저장된 프로시저 또는 Udf에서 디버거가 중지 되도록 하려고 합니다. 응용 프로그램 디버깅 2 단계부터이 검사 됩니다.
- **SQL Server 프로젝트에서 디버깅** -Visual Studio Professional 및 Team 시스템 버전 관리 되는 데이터베이스 개체를 만드는 데 흔히 사용 되는 SQL Server 프로젝트 유형을 포함 합니다. SQL Server 프로젝트를 사용 하 여 살펴보겠습니다 및 다음 자습서에서 해당 콘텐츠를 디버깅 합니다.

Visual Studio는 로컬 및 원격 SQL Server 인스턴스에서 저장된 프로시저를 디버깅할 수 있습니다. 로컬 SQL Server 인스턴스를 Visual Studio와 동일한 컴퓨터에 설치 되어 있는 경우 사용 중인 SQL Server 데이터베이스 개발 컴퓨터에 없는 경우, 원격 인스턴스를 간주 됩니다. 이 자습서에 대 한 사용 중인 로컬 SQL Server 인스턴스. 원격 SQL server 인스턴스에서 저장된 프로시저를 디버깅할 때 로컬 인스턴스에서 저장된 프로시저를 디버깅 하는 보다 자세한 구성 단계 필요 합니다.

로컬 SQL Server 인스턴스를 사용 하는 경우 1 단계부터 시작 하 고 끝에이 자습서를 통해 작업 수 있습니다. 그러나 원격 SQL Server 인스턴스를 사용 하는 경우 하면 디버깅 하는 경우 확인 하는 첫 번째 필요가 원격 인스턴스에 있는 SQL Server 로그인이 Windows 사용자 계정 사용 하 여 개발 컴퓨터에 기록 됩니다. Moveover,이 데이터베이스 로그인 및 실행 중인 ASP.NET 응용 프로그램에서 데이터베이스에 연결할 때 사용할 데이터베이스 로그인을 둘 다의 구성원 이어야는 `sysadmin` 역할입니다. 원격 인스턴스에 섹션에서 Visual Studio 및 SQL Server 원격 인스턴스를 디버그 구성에 대 한 자세한 내용은이 자습서의 끝에서 T-SQL 디버깅 데이터베이스 개체를 참조 하십시오.

마지막으로 디버깅 T-SQL 데이터베이스 개체에 대 한 지원 되지 않음을 디버깅.NET 응용 프로그램에 대 한 지원으로 다양 한 기능으로 이해 합니다. 예를 들어, 중단점 조건 및 필터가 지원 되지 않으며, 디버깅 창의 하위 집합을 사용할 수 있습니다. 편집 하며 계속 하기를 사용할 수 없습니다, 유효 하지 않게 등 직접 실행 창 렌더링 됩니다. 참조 [디버거 명령 및 기능에 대 한 제한](https://msdn.microsoft.com/library/ms165035(VS.80).aspx) 자세한 내용은 합니다.

## <a name="step-1-directly-stepping-into-a-stored-procedure"></a>1 단계: 직접 저장된 프로시저를 한 단계씩 실행

Visual Studio를 사용 하면 쉽게 데이터베이스 개체를 직접 디버그할 수입니다. 한 단계씩 코드 실행에 직접 데이터베이스 디버깅 (DDD) 기능을 사용 하는 방법에 대해 s는 `Products_SelectByCategoryID` Northwind 데이터베이스의 저장 프로시저입니다. 이름에서 알 수 있듯이 `Products_SelectByCategoryID` ; 특정 범주에 대 한 정보를 반환에서 생성 된 것을 [를 사용 하 여 기존 저장 프로시저는 입력 데이터 집합의 Tableadapter에 대 한](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md) 자습서입니다. 서버 탐색기로 이동 하 여 시작 하 고 Northwind 데이터베이스 노드를 확장 합니다. 다음으로, 드릴 다운 Stored Procedures 폴더를 마우스 오른쪽 단추로 클릭는 `Products_SelectByCategoryID` 저장 프로시저 및 상황에 맞는 메뉴에서 저장 프로시저 한 단계씩 코드 실행 옵션을 선택 합니다. 디버거가 시작 됩니다.

이후 합니다 `Products_SelectByCategoryID` 저장된 프로시저에 필요한를 `@CategoryID` 입력된 매개 변수를 만들라는 요청도 받습니다이 값을 제공 합니다. 음료에 대 한 정보를 반환 하는 1을 입력 합니다.


![에 값 1을 사용 합니다 @CategoryID 매개 변수](debugging-stored-procedures-cs/_static/image1.png)

**그림 1**:에 값 1을 사용 합니다 `@CategoryID` 매개 변수


에 대 한 값을 입력 한 후의 `@CategoryID` 매개 변수를 저장된 프로시저 실행 됩니다. 하지만 완료 될 때까지 실행 하는 대신 디버거가 첫 번째 문에서 실행을 중단 합니다. 저장된 프로시저의 현재 위치를 나타내는 여백에 있는 노란색 화살표는 note 합니다. 확인 및 조사식 창을 통해 또는 저장된 프로시저의 매개 변수 이름을 마우스로 매개 변수 값을 편집할 수 있습니다.


[![저장 프로시저의 첫 번째 문에서 디버거 중지](debugging-stored-procedures-cs/_static/image3.png)](debugging-stored-procedures-cs/_static/image2.png)

**그림 2**: 디버거가 저장 프로시저의 첫 번째 문에서 중지 ([큰 이미지를 보려면 클릭](debugging-stored-procedures-cs/_static/image4.png))


를 한 번에 문 하나씩 저장된 프로시저를 단계별로 실행 하려면 도구 모음에서 프로시저 단위 실행 단추를 클릭 하거나 F10 키를 누릅니다. 합니다 `Products_SelectByCategoryID` 하나를 포함 하는 저장된 프로시저 `SELECT` 문을 단일 문으로 건너뛰기는 F10에 도달 하 고 저장된 프로시저의 실행을 완료 합니다. 저장된 프로시저가 완료 되 면 해당 출력이 출력 창에 표시 됩니다 하 고 디버거를 종료 합니다.

> [!NOTE]
> 문 수준에서 발생 T-SQL 디버깅 단계씩 실행할 수 없습니다는 `SELECT` 문입니다.


## <a name="step-2-configuring-the-website-for-application-debugging"></a>2 단계: 응용 프로그램 디버깅에 대 한 웹 사이트 구성

서버 탐색기에서 직접 저장된 프로시저를 디버깅 하는 것은 유용한, 대부분의 시나리오에서 더에 관심이 ASP.NET 응용 프로그램에서 호출 될 때 저장된 프로시저를 디버깅 합니다. Visual Studio 내에서 저장된 프로시저에 중단점을 추가 하 고 ASP.NET 응용 프로그램 디버깅을 시작할 수 있습니다. 응용 프로그램에서 중단점을 사용 하 여 저장된 프로시저를 호출 하면 실행이 중단점에서 중단 됩니다 및 수 보기 및 저장된 프로시저 s 매개 변수 값을 변경 하 고 1 단계에서에서 수행한 것 처럼 해당 문을 단계별로 실행 합니다.

응용 프로그램에서 호출한 저장된 프로시저를 디버깅을 시작할 수 있습니다, 전에 SQL Server 디버거를 사용 하 여 통합을 ASP.NET 웹 응용 프로그램에 지시 해야 합니다. 솔루션 탐색기에서 웹 사이트 이름을 마우스 오른쪽 단추로 클릭 하 여 시작 (`ASPNET_Data_Tutorial_74_CS`). 상황에 맞는 메뉴에서 속성 페이지 옵션을 선택 하 고, 왼쪽에서 시작 옵션 항목 선택, 디버거 섹션에서 SQL Server 확인란 (그림 3 참조).


[![응용 프로그램의 속성 페이지에서 SQL Server 확인란](debugging-stored-procedures-cs/_static/image6.png)](debugging-stored-procedures-cs/_static/image5.png)

**그림 3**: 응용 프로그램의 속성 페이지에서에서 SQL Server 확인란 ([큰 이미지를 보려면 클릭](debugging-stored-procedures-cs/_static/image7.png))


또한 연결 풀링을 사용 하지 않도록 설정 하는 응용 프로그램에서 사용 하는 데이터베이스 연결 문자열을 업데이트 해야 합니다. 데이터베이스에 대 한 연결을 닫으면 해당 `SqlConnection` 개체의 사용 가능한 연결 풀에 배치 됩니다. 데이터베이스에 연결을 설정할 때 사용 가능한 연결이이 풀에서 검색할 수 있습니다 보다는 개체 만들기 및 새 연결을 설정 하지 않아도 됩니다. 이 풀링을 연결 개체는 성능을 향상 하 고 기본적으로 활성화 됩니다. 그러나 디버그할 때 디버깅 인프라 풀에서 만든 연결으로 작업 하는 경우 올바르게 다시 설정 하지 있으므로 연결 풀링을 해제 하려고 합니다.

비활성된 연결 풀링, 업데이트 합니다 `NORTHWNDConnectionString` 에 `Web.config` 설정을 포함 하도록 `Pooling=false` 합니다.


[!code-xml[Main](debugging-stored-procedures-cs/samples/sample1.xml)]

> [!NOTE]
> 마친 후 ASP.NET 응용 프로그램을 통해 SQL Server 디버깅 해야 연결 풀링을 제거 하 여 다시 시작 합니다 `Pooling` 연결 문자열에서 설정 (또는로 설정 하 여 `Pooling=true` ).


이 시점에서 ASP.NET 응용 프로그램에 웹 응용 프로그램을 통해 호출 되 면 SQL Server 데이터베이스 개체를 디버깅 하려면 Visual Studio를 허용 하도록 구성한 합니다. 이제 남아 있는 모든 저장된 프로시저에 중단점을 추가 하 고 디버깅을 시작 하는 것!

## <a name="step-3-adding-a-breakpoint-and-debugging"></a>중단점을 추가 하 고 디버깅 하는 3 단계:

열기는 `Products_SelectByCategoryID` 의 시작 부분에 중단점을 설정 하 고 저장 프로시저는 `SELECT` 적절 한 위치에서 여백을 클릭 하 여 문이나의 시작 부분에 커서를 배치 하 여는 `SELECT` 문과 f9입니다. 그림 4에서 알 수 있듯이, 중단점 여백에 빨간색 원으로 표시 합니다.


[![Products_SelectByCategoryID에 중단점을 설정 저장 프로시저](debugging-stored-procedures-cs/_static/image9.png)](debugging-stored-procedures-cs/_static/image8.png)

**그림 4**:에서 중단점을 설정 합니다 `Products_SelectByCategoryID` 저장 프로시저 ([클릭 하 여 큰 이미지 보기](debugging-stored-procedures-cs/_static/image10.png))


클라이언트 응용 프로그램을 통해 디버그 해야 하는 SQL 데이터베이스 개체에 대 한 순서 대로 반드시 해당 데이터베이스 응용 프로그램 디버깅을 지원 하도록 구성 합니다. 먼저 중단점을 설정 하는 경우이 설정에 자동으로 전환 해야 하지만 다시 확인 하는 것이 좋습니다. 마우스 오른쪽 단추로 클릭는 `NORTHWND.MDF` 서버 탐색기에서 노드. 상황에 맞는 메뉴 선택된 이라는 메뉴 항목이 응용 프로그램 디버깅을 포함 해야 합니다.


![응용 프로그램 디버깅 옵션이 설정 되어 있는지 확인](debugging-stored-procedures-cs/_static/image11.png)

**그림 5**: 응용 프로그램 디버깅 옵션이 설정 되어 있는지 확인


중단점 집합을 사용 하도록 설정 하는 응용 프로그램 디버깅 옵션을 사용 하 여 ASP.NET 응용 프로그램에서 호출할 경우 저장된 프로시저를 디버깅 하려면 준비가 됩니다. 디버그 메뉴에 이동 하 여 디버거를 시작 하 고 도구 모음에서 재생 아이콘 f5 키를 눌러 또는 녹색을 클릭 하 여 디버깅 시작을 선택 합니다. 디버거가 시작 되 고 웹 사이트 시작 됩니다.

합니다 `Products_SelectByCategoryID` 저장된 프로시저에서 만든 합니다 [사용 하 여 기존 저장 프로시저는 입력 데이터 집합의 Tableadapter에 대 한](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md) 자습서입니다. 해당 하는 웹 페이지 (`~/AdvancedDAL/ExistingSprocs.aspx`)이 저장된 프로시저에서 반환 된 결과 표시 하는 GridView를 포함 합니다. 브라우저를 통해이 페이지를 방문 합니다. 페이지의 중단점에 도달 하면는 `Products_SelectByCategoryID` 저장된 프로시저 소진 하 고 Visual Studio에 제어를 반환 합니다. 마찬가지로 1 단계에서에서 s 문 저장된 프로시저 및 뷰를 통해 단계를 매개 변수 값을 수정 합니다.


[![ExistingSprocs.aspx 페이지에는 처음에 음료 표시](debugging-stored-procedures-cs/_static/image13.png)](debugging-stored-procedures-cs/_static/image12.png)

**그림 6**: 합니다 `ExistingSprocs.aspx` 페이지에는 처음에 Beverages 표시 됩니다 ([클릭 하 여 큰 이미지 보기](debugging-stored-procedures-cs/_static/image14.png))


[![저장 프로시저의 중단점에 도달 했습니다.](debugging-stored-procedures-cs/_static/image16.png)](debugging-stored-procedures-cs/_static/image15.png)

**그림 7**: 중단점에 도달 하는 저장 프로시저는 s ([큰 이미지를 보려면 클릭](debugging-stored-procedures-cs/_static/image17.png))


그림 7 표시 값의에서 조사식 창으로는 `@CategoryID` 매개 변수는 1입니다. 때문에 이것이 합니다 `ExistingSprocs.aspx` 페이지 있는 음료 범주에서 제품을 처음에 표시를 `CategoryID` 값이 1입니다. 드롭다운 목록에서 다른 범주를 선택 합니다. 이렇게 포스트백 하 고 다시 실행 된 `Products_SelectByCategoryID` 저장 프로시저입니다. 마찬가지로 이번 중단점에 도달 합니다 `@CategoryID` s 선택한 드롭다운 목록에서 항목을 반영 하는 매개 변수의 값 `CategoryID`합니다.


[![드롭다운 목록에서 다른 범주를 선택 합니다.](debugging-stored-procedures-cs/_static/image19.png)](debugging-stored-procedures-cs/_static/image18.png)

**그림 8**: 드롭다운 목록에서 다른 범주를 선택 ([큰 이미지를 보려면 클릭](debugging-stored-procedures-cs/_static/image20.png))


[![@CategoryID 웹 페이지에서 선택한 범주를 반영 하는 매개 변수](debugging-stored-procedures-cs/_static/image22.png)](debugging-stored-procedures-cs/_static/image21.png)

**그림 9**: 합니다 `@CategoryID` 매개 변수 반영 웹 페이지에서 범주를 선택 합니다 ([클릭 하 여 큰 이미지 보기](debugging-stored-procedures-cs/_static/image23.png))


> [!NOTE]
> 경우에 중단점을 `Products_SelectByCategoryID` 저장된 프로시저를 방문할 때 적중 되지 않는 `ExistingSprocs.aspx` 페이지, ASP.NET 응용 프로그램의 속성 페이지의 디버거 섹션을 SQL Server 확인란을 체크 인 된 연결 풀링이 되었는지 있는지 확인 사용 안 함과 데이터베이스 s 응용 프로그램 디버깅 옵션 활성화 되어 있습니다. 계속 다시 표시 되 면 문제가 Visual Studio를 다시 시작 하 고 다시 시도 하세요.


## <a name="debugging-t-sql-database-objects-on-remote-instances"></a>원격 인스턴스에서 T-SQL 데이터베이스 개체 디버깅

SQL Server 데이터베이스 인스턴스를 Visual Studio와 동일한 컴퓨터에 있으면 Visual Studio를 통해 데이터베이스 개체를 디버깅 하는 것은 매우 간단 합니다. 그러나 서로 다른 컴퓨터에서 SQL Server 및 Visual Studio에 있는 경우 다음 몇 가지 신중 하 게 하기 위해 구성할 사항은 모든 기능을 제대로 사용 합니다. 두 가지 핵심 작업 직면 하는 것:

- ADO.NET 통해 데이터베이스에 연결할 때 사용할 로그인에 속해 있는지 확인 합니다 `sysadmin` 역할입니다.
- 개발 컴퓨터에서 Visual Studio에서 사용 된 Windows 사용자 계정에 속하는 올바른 SQL Server 로그인 계정 인지 확인 합니다 `sysadmin` 역할입니다.

첫 번째 단계는 비교적 간단 합니다. 먼저 ASP.NET 응용 프로그램에서 데이터베이스에 연결 하 고 그런 다음 SQL Server Management Studio에서 해당 로그인 계정을 추가 하는 데 사용 하는 사용자 계정 식별 된 `sysadmin` 역할입니다.

두 번째 작업은 응용 프로그램을 디버그 사용 하는 Windows 사용자 계정이 원격 데이터베이스에서 유효한 로그인 해야 합니다. 그러나 가능성에는 Windows 계정을 사용 하 여 워크스테이션에 로그온 하면 SQL Server에서 유효한 로그인 하지 않습니다. 특정 로그인 계정에 SQL Server를 추가 하는 대신 SQL Server 디버깅 계정으로 일부 Windows 사용자 계정을 지정 하는 것이 좋습니다 것입니다. 그런 다음 원격 SQL Server 인스턴스의 데이터베이스 개체를 디버깅 하려면 Visual Studio는 Windows 로그인 계정 s 자격 증명을 사용 하 여 실행 합니다.

예제는 작업을 명확 하 게 하는 데 도움이 됩니다. Windows 계정인은 imagine `SQLDebug` Windows 도메인 내에서. 이 계정은 원격 SQL Server 인스턴스에 올바른 로그인 및 멤버로 추가할 해야는 `sysadmin` 역할입니다. 그런 다음 Visual Studio에서 원격 SQL Server 인스턴스를 디버깅 하려면 해야으로 Visual Studio를 실행 합니다 `SQLDebug` 사용자입니다. 로 다시 로그인 하 여 워크스테이션에서 로그인 하 여이 작업을 수행할 수 없습니다 `SQLDebug`에 고유한 자격 증명을 사용 하 여 워크스테이션에 로그인 한 다음 사용 하는 것을 간단 하지만 Visual Studio를 실행 하 고 `runas.exe` 으로 Visual Studio를 시작 하는 `SQLDebug` 사용자입니다. `runas.exe` 특정 응용 프로그램을 다른 사용자 계정 가장 하 여 상태에서 실행할 수 있습니다. Visual Studio를 시작 하려면 `SQLDebug`, 명령줄에서 다음 문을 입력할 수 있습니다.


[!code-console[Main](debugging-stored-procedures-cs/samples/sample2.cmd)]

에 대 한 자세한 내용은이 프로세스를 참조 하세요 [William R. Vaughn](http://betav.com/BLOG/billva/) s *Hitchhiker s Visual Studio 및 SQL Server, 일곱 번째 개정판 가이드* 뿐만 [방법: SQL Server 사용 권한 설정 디버깅을 위해](https://msdn.microsoft.com/library/w1bhybwz(VS.80).aspx)합니다.

> [!NOTE]
> 개발 컴퓨터에서 Windows XP 서비스 팩 2를 실행 중인 경우 인터넷 연결 방화벽이 원격 디버깅을 허용 하도록 구성 해야 합니다. [하는 방법에: SQL Server 2005 디버깅 사용](https://msdn.microsoft.com/library/s0fk6z6e(VS.80).aspx) 문서는이 두 단계 정보: (a) Visual Studio 호스트 컴퓨터를 추가 해야 합니다 `Devenv.exe` 열어야 예외 목록에는 TCP 135 포트 열기 및 (b) 원격 컴퓨터의 (SQL) TCP 135 포트 및 추가 `sqlservr.exe` 예외 목록에 있습니다. 도메인 정책에 따라 IPSec을 통해 수행 해야 하는 네트워크 통신에 필요한 경우에 UDP 4500 및 UDP 500 포트를 열어야 합니다.


## <a name="summary"></a>요약

.NET 응용 프로그램 코드에 대 한 디버깅 지원을 제공 하는 것 외에도 Visual Studio 또한 다양 한 디버깅 SQL Server 2005에 대 한 옵션을 제공 합니다. 이러한 옵션 중에서 살펴본이 자습서: 직접 데이터베이스 디버깅 및 응용 프로그램 디버깅 합니다. T-SQL 데이터베이스 개체를 직접 디버깅 하려면 서버 탐색기를 통해 개체를 찾을를 마우스 오른쪽 단추로 클릭 하 고 단계를 선택 합니다. 이 디버거를 시작 및 데이터베이스 개체, 이때 개체의 문 및 보기를 단계별로 실행 하 고 수정할 수 매개 변수 값의에서 첫 번째 문에서 중지 합니다. 1 단계에서에서 우리가 하는 데이 방법은 한 단계씩 코드 실행을 `Products_SelectByCategoryID` 저장 프로시저입니다.

응용 프로그램 디버깅 중단점을 데이터베이스 개체 내에서 직접 설정할 수 있습니다. 중단점을 사용 하 여 데이터베이스 개체 (예: ASP.NET 웹 응용 프로그램)는 클라이언트 응용 프로그램에서 호출 되 면 디버거는으로 프로그램을 중단 합니다. 응용 프로그램 디버깅 어떤 응용 프로그램 동작은 호출할 특정 데이터베이스 개체를 보다 명확 하 게 표시 하므로 유용 합니다. 그러나 조금 더 구성과 직접 데이터베이스 디버깅 보다 설치 해야합니다.

SQL Server 프로젝트를 통해 데이터베이스 개체를 디버깅할 수도 있습니다. SQL Server 프로젝트를 사용 하 여 살펴보겠습니다 및 다음 자습서에서 관리 되는 데이터베이스 개체 작성 및 디버깅을 사용 하는 방법입니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

> [!div class="step-by-step"]
> [이전](protecting-connection-strings-and-other-configuration-information-cs.md)
> [다음](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs.md)
