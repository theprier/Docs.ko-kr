---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/creating-stored-procedures-and-user-defined-functions-with-managed-code-vb
title: 관리 되는 코드 (VB) 저장된 프로시저 및 사용자 정의 함수 만들기 | Microsoft Docs
author: rick-anderson
description: Microsoft SQL Server 2005 개발자는 관리 되는 코드를 통해 데이터베이스 개체를 만들 수 있도록.NET 공용 언어 런타임 통합 됩니다. 이 자습서는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/03/2007
ms.topic: article
ms.assetid: 8be9a51b-ea6b-46c7-bfa2-476d9b14c24c
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/creating-stored-procedures-and-user-defined-functions-with-managed-code-vb
msc.type: authoredcontent
ms.openlocfilehash: a2a4042303fe507af449e83e36f67f4624f579cc
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37371845"
---
<a name="creating-stored-procedures-and-user-defined-functions-with-managed-code-vb"></a>저장 프로시저 및 관리 코드 (VB)를 사용 하 여 사용자 정의 함수 만들기
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_75_VB.zip) 또는 [PDF 다운로드](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/datatutorial75vb1.pdf)

> Microsoft SQL Server 2005 개발자는 관리 되는 코드를 통해 데이터베이스 개체를 만들 수 있도록.NET 공용 언어 런타임 통합 됩니다. 이 자습서는 관리 되는 저장된 프로시저를 만드는 방법을 보여 줍니다 하 고 관리 되는 Visual Basic 또는 C# 코드를 사용 하 여 사용자 정의 함수. 이러한 버전의 Visual Studio 이러한 관리 되는 데이터베이스 개체를 디버깅 하는 데 허용 하는 방법을 표시 합니다.


## <a name="introduction"></a>소개

Microsoft가의 SQL Server 2005와 같은 데이터베이스를 사용 합니다 [Transact-Structured 쿼리 언어 (T-SQL)](http://en.wikipedia.org/wiki/Transact-SQL) 삽입, 수정 및 데이터 검색에 대 한 합니다. 대부분의 데이터베이스 시스템에는 일련의 재사용 가능한 단일 단위로 실행 될 수 있는 SQL 문 그룹화 구문이 포함 됩니다. 저장된 프로시저는 한 가지 예입니다. 다른 *사용자 정의 함수*(Udf)는 구문 9 단계에서에서 더 자세히 검토할 것입니다.

핵심 SQL는 데이터 집합을 사용 하 여 작업에 대 한 설계 되었습니다. 합니다 `SELECT`, `UPDATE`, 및 `DELETE` 기본적으로 해당 테이블에서 모든 레코드를 적용 문과 의해서만 제한 됩니다 해당 `WHERE` 절. 아직 스칼라 데이터 조작 및 한 번에 하나의 레코드를 사용 하 여 작업에 대 한 디자인 언어 기능이 많이 있습니다. [`CURSOR` s](http://www.sqlteam.com/item.asp?ItemID=553) 레코드 집합이 한 번에 하나를 통해 반복 될 수 있습니다. 문자열 조작 함수 등 `LEFT`, `CHARINDEX`, 및 `PATINDEX` 스칼라 데이터와 함께 작동 합니다. SQL과 같은 제어 흐름 문의 포함 되어 있습니다 `IF` 고 `WHILE`입니다.

Microsoft SQL Server 2005 이전 저장된 프로시저 및 Udf만 정의할 수 있습니다 T-SQL 문 컬렉션으로. 그러나 SQL Server 2005와의 통합을 제공 하도록 설계 되었습니다 합니다 [공용 언어 런타임 (CLR)](https://msdn.microsoft.com/netframework/aa497266.aspx), 하는 모든.NET 어셈블리에서 사용 하는 런타임입니다. 따라서 저장된 프로시저 및 Udf는 SQL Server 2005 데이터베이스에서를 만들 수 있습니다 관리 되는 코드를 사용 하 여. 즉, 저장된 프로시저 또는 UDF를 Visual Basic 클래스의 메서드로 만들 수 있습니다. 이렇게 하면 이러한 저장된 프로시저 및 Udf.NET framework에서 및 사용자 고유의 사용자 지정 클래스에서 기능을 활용할 수 있습니다.

살펴보겠습니다이 자습서에서 만드는 관리 되는 방법을 저장 프로시저 및 사용자 정의 함수 및 Northwind 데이터베이스에 통합 하는 방법. Let s 시작!

> [!NOTE]
> 관리 되는 데이터베이스 개체에는 SQL 대응을 통해 몇 가지 이점을 제공합니다. 언어의 다양 한 기능 및 친숙 하 고 기존 코드 및 논리를 재사용할 수는 주요 이점이 있습니다. 하지만 관리 되는 데이터베이스 개체 절차적 논리 없이 많은 관련이 없는 데이터 집합으로 작업 하는 경우 효율성이 떨어지는 일 수 있습니다. T-SQL 및 관리 되는 코드를 사용 하는 이점에 더 상세히 논의 체크 아웃 합니다 [장점의를 사용 하 여 관리 코드를 데이터베이스 개체를 만드는](https://msdn.microsoft.com/library/k2e1fb36(VS.80).aspx)합니다.


## <a name="step-1-moving-the-northwind-database-out-ofappdata"></a>1 단계: Out of Northwind 데이터베이스를 이동합니다.`App_Data`

웹 응용 프로그램에서에서 Microsoft SQL Server 2005 Express Edition 데이터베이스 파일을 사용한 지금이 자습서의 모든 `App_Data` 폴더입니다. 데이터베이스를 배치 `App_Data` 된 디렉터리 내에 모든 파일 및 자습서를 테스트 하려면 추가 구성 단계가 없는 필요한 대로 이러한 자습서를 실행 하 고 배포를 간소화 합니다.

그러나이 자습서에서는 let s Northwind 데이터베이스 이동 개 `App_Data` 하 고 SQL Server 2005 Express Edition 데이터베이스 인스턴스를 사용 하 여 명시적으로 등록 합니다. 데이터베이스를 사용 하 여이 자습서의 단계를 수행할 수 있습니다 하는 동안는 `App_Data` 폴더 단계의 숫자로 내용이 훨씬 간단 하 게 명시적으로 SQL Server 2005 Express Edition 데이터베이스 인스턴스를 사용 하 여 데이터베이스를 등록 합니다.

이 자습서에 대 한 다운로드에는 두 데이터베이스 파일- `NORTHWND.MDF` 하 고 `NORTHWND_log.LDF` 라는 폴더에 배치- `DataFiles`합니다. 자습서의 고유한 구현을 함께 수행 하는 경우 Visual Studio를 닫고 이동 합니다 `NORTHWND.MDF` 및 `NORTHWND_log.LDF` s 웹 사이트에서 파일 `App_Data` 외부 웹 사이트의 폴더에 폴더입니다. 데이터베이스 파일이 다른 폴더로 이동한 후 SQL Server 2005 Express Edition 데이터베이스 인스턴스를 사용 하 여 Northwind 데이터베이스를 등록 해야 합니다. SQL Server Management Studio에서이 작업을 수행할 수 있습니다. 비-Express Edition의 SQL Server 2005 컴퓨터에 설치 되어 있는 경우 다음 있을 가능성이 높습니다 이미 Management Studio를 설치 합니다. 만 있는 경우 SQL Server 2005 Express Edition 컴퓨터에 다운로드 하 고 설치 잠시 [Microsoft SQL Server Management Studio Express](https://www.microsoft.com/downloads/details.aspx?displaylang=en&amp;FamilyID=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796)합니다.

SQL Server Management Studio를 시작 합니다. 그림 1에서 알 수 있듯이, Management Studio에 연결할 서버를 요청 하 여 시작 합니다. 서버 이름에 대 한 localhost\SQLExpress를 입력 하 고 인증 드롭다운 목록에서 Windows 인증을 선택한 다음 연결을 클릭 합니다.


![해당 데이터베이스 인스턴스에 연결](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image1.png)

**그림 1**: 적절 한 데이터베이스 인스턴스에 연결


적 연결 되 면 개체 탐색기 창에는 해당 데이터베이스, 보안 정보, 관리 옵션 등을 포함 하 여 SQL Server 2005 Express Edition 데이터베이스 인스턴스의 대 한 정보를 나열 됩니다.

Northwind 데이터베이스에 연결 해야 합니다 `DataFiles` 폴더 (또는 아무 곳에 나 있습니다 옮기지) SQL Server 2005 Express Edition 데이터베이스 인스턴스에 있습니다. 데이터베이스 폴더 단추로 클릭 하 고 상황에 맞는 메뉴에서 연결 옵션을 선택 합니다. 데이터베이스 연결 대화 상자가 표시 됩니다. 추가 단추 클릭, 적절 한 드릴다운할지 `NORTHWND.MDF` 파일과 확인을 클릭 합니다. 이 시점에서 화면은 그림 2와 비슷하게 표시 됩니다.


[![해당 데이터베이스 인스턴스에 연결](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image3.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image2.png)

**그림 2**: 해당 데이터베이스 인스턴스에 연결 ([큰 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image4.png))


> [!NOTE]
> Management Studio를 통해 SQL Server 2005 Express Edition 인스턴스에 연결할 때 데이터베이스 연결 대화 상자는 내 문서와 같은 사용자 프로필 디렉터리를 드릴 다운 수 없습니다. 따라서 배치 해야 합니다 `NORTHWND.MDF` 및 `NORTHWND_log.LDF` 비 사용자 프로필 디렉터리에 있는 파일입니다.


데이터베이스를 연결 하려면 확인 단추를 클릭 합니다. 데이터베이스 연결 대화 상자를 닫히고 개체 탐색기에 바로 연결 된 데이터베이스를 나열할 해야 합니다. 가능성은 Northwind 데이터베이스에 같은 이름을 `9FE54661B32FDD967F51D71D0D5145CC_LINE ARTICLES\DATATUTORIALS\VOLUME 3\CSHARP\73\ASPNET_DATA_TUTORIAL_75_CS\APP_DATA\NORTHWND.MDF`입니다. 데이터베이스를 마우스 오른쪽 단추로 클릭 하 고 이름 바꾸기를 선택 하 여 데이터베이스를 이름을 Northwind로 바꿉니다.


![Northwind 데이터베이스 이름 바꾸기](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image5.png)

**그림 3**: northwind 데이터베이스 이름 바꾸기


## <a name="step-2-creating-a-new-solution-and-sql-server-project-in-visual-studio"></a>2 단계: Visual Studio에서 새 솔루션 및 SQL Server 프로젝트를 만들기

SQL Server 2005에서 관리 되는 저장된 프로시저 또는 Udf를 만드는 저장된 프로시저 및 UDF 논리 클래스에서 Visual Basic 코드로 작성 됩니다. 이 클래스를 어셈블리로 컴파일할 해야 코드를 작성 한 후 (한 `.dll` 파일), SQL Server 데이터베이스를 사용 하 여 어셈블리를 등록을 만든 다음에 해당 하는 메서드를 가리키는 데이터베이스에 저장된 프로시저 또는 UDF 개체 어셈블리입니다. 이러한 단계 수 모두 수동으로 수행 합니다. 편집기 텍스트의 코드를 작성, Visual Basic 컴파일러를 사용 하 여 명령줄에서 컴파일할 수 것 (`vbc.exe`)를 사용 하 여 데이터베이스에 등록 합니다 [ `CREATE ASSEMBLY` ](https://msdn.microsoft.com/library/ms189524.aspx) 명령 또는 Management Studio에서 저장 된 추가 프로시저 또는 이와 유사한 수단을 통해 UDF 개체입니다. 다행 스럽게도 Visual studio Professional 및 Team 시스템 버전에는 이러한 작업을 자동화 하는 SQL Server 프로젝트 형식을 포함 됩니다. 이 자습서에서는 살펴보겠습니다 SQL Server 프로젝트 형식을 사용해 서 관리 되는 저장된 프로시저 및 UDF를 만듭니다.

> [!NOTE]
> Visual studio Standard edition 또는 Visual Web Developer를 사용 하는 경우 대신 수동 방법을 사용 하 여 해야 합니다. 13 단계 수동으로 이러한 단계를 수행 하기 위한 자세한 지침을 제공 합니다. 이러한 단계는 사용 중인 Visual Studio의 어떤 버전에 관계 없이 적용 해야 하는 중요 한 SQL Server 구성 지침을 포함 하므로 13 단계를 읽기 전에 12 단계 2를 읽을 수 하시기 바랍니다.


Visual Studio를 열어 시작 합니다. 파일 메뉴에서 새 프로젝트 대화 상자를 표시 하는 새 프로젝트를 선택 상자 (그림 4 참조). 데이터베이스 프로젝트 유형으로 드릴 하 고 그런 다음 오른쪽에 나열 된 템플릿에서 새 SQL Server 프로젝트를 만들려면 선택 합니다. 이 프로젝트의 이름을 하기로 `ManagedDatabaseConstructs` 이라는 솔루션 내에 배치 하 고 `Tutorial75`입니다.


[![새 SQL Server 프로젝트 만들기](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image7.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image6.png)

**그림 4**: 새 SQL Server 프로젝트를 만듭니다 ([큰 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image8.png))


솔루션 및 SQL Server 프로젝트를 만들려면 새 프로젝트 대화 상자에서 확인 단추를 클릭 합니다.

SQL Server 프로젝트는 특정 데이터베이스에 연결 됩니다. 따라서 새 SQL Server 프로젝트를 만든 후 즉시 만들라는 요청도 받습니다이 정보를 지정 합니다. 그림 5 1 단계에서 다시 SQL Server 2005 Express Edition 데이터베이스 인스턴스의 등록 Northwind 데이터베이스를 가리키도록 작성 되는 새 데이터베이스 참조 대화 상자를 보여 줍니다.


![Northwind 데이터베이스를 사용 하 여 SQL Server 프로젝트 연결](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image9.png)

**그림 5**: Northwind 데이터베이스를 사용 하 여 SQL Server 프로젝트 연결


관리 되는 저장된 프로시저 및 Udf를이 프로젝트에 만들겠습니다를 디버그 하기 위해 SQL/CLR 디버깅 연결에 대 한 지원을 사용 하도록 설정 해야 합니다. (그림 5에서 수행한 것)으로 SQL Server 프로젝트를 새 데이터베이스를 사용 하 여 연결 될 때마다, Visual Studio에서는 연결에서 SQL/CLR 디버깅을 사용할 수 있게 하고자 하는 경우 (그림 6 참조). 예를 클릭 합니다.


![SQL/CLR 디버깅을 사용 하도록 설정](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image10.png)

**그림 6**: SQL/CLR 디버깅을 사용 하도록 설정


이 시점에서 새 SQL Server 프로젝트를 솔루션에 추가 되었습니다. 라는 폴더를 포함 `Test Scripts` 라는 파일을 사용 하 여 `Test.sql`, 프로젝트에서 만든 관리 되는 데이터베이스 개체 디버깅에 사용 됩니다. 12 단계에서에서 디버깅 살펴보겠습니다.

이 프로젝트에 새 관리 되는 저장된 프로시저 및 Udf 이제 추가할 수 있습니다. 그러나 s 솔루션에서 기존 웹 응용 프로그램을 먼저 포함 하도록 수행 하기 전에 합니다. 파일 메뉴에서 추가 옵션을 선택 하 고 기존 웹 사이트를 선택 합니다. 적절 한 웹 사이트 폴더를 찾아 확인을 클릭 합니다. 그림 7에서 알 수 있듯이,이 솔루션을 업데이트 하 두 프로젝트를 포함 합니다: 웹 사이트 및 `ManagedDatabaseConstructs` SQL Server 프로젝트입니다.


![솔루션 탐색기는 이제 두 프로젝트가 포함](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image11.png)

**그림 7**: 솔루션 탐색기는 이제 두 프로젝트가 포함


`NORTHWNDConnectionString` 값 `Web.config` 현재 참조 합니다 `NORTHWND.MDF` 파일을 `App_Data` 폴더. 이 데이터베이스를 제거 했으므로 `App_Data` 명시적으로 등록 및 SQL Server 2005 Express Edition 데이터베이스 인스턴스에서 마찬가지로 업데이트 해야 합니다 `NORTHWNDConnectionString` 값입니다. 열기를 `Web.config` 변경 확인 하 고 웹 사이트에서 파일을 `NORTHWNDConnectionString` 연결 문자열을 읽을 수 있도록 값: `Data Source=localhost\SQLExpress;Initial Catalog=Northwind;Integrated Security=True`합니다. 이렇게이 변경한 후에 `<connectionStrings>` 섹션 `Web.config` 다음과 유사 합니다.


[!code-xml[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample1.xml)]

> [!NOTE]
> 에 설명 된 대로 합니다 [이전 자습서](debugging-stored-procedures-vb.md)클라이언트 응용 프로그램에서 SQL Server 개체를 디버깅 하는 경우는 ASP.NET 웹 사이트와 같은 연결 풀링을 사용 하지 않도록 설정 해야 합니다. 위에 표시 된 연결 문자열 연결 풀링 비활성화 ( `Pooling=false` ). ASP.NET 웹 사이트에서 관리 되는 저장된 프로시저 및 Udf를 디버깅 하지 않으려는 경우 연결 풀링이 사용 하도록 설정 합니다.


## <a name="step-3-creating-a-managed-stored-procedure"></a>3 단계: 관리 되는 만드는 저장 프로시저

Northwind 데이터베이스에 관리 되는 저장된 프로시저를 추가 하려면 먼저 SQL Server 프로젝트에서 메서드로 저장된 프로시저를 생성 해야 합니다. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭는 `ManagedDatabaseConstructs` 프로젝트 이름 및 새 항목을 추가 하려면 선택 합니다. 이 유형의 프로젝트에 추가할 수 있는 관리 되는 데이터베이스 개체를 나열 하는 새 항목 추가 대화 상자에 표시 됩니다. 그림 8에서 알 수 있듯이, 여기에 저장된 프로시저 및 사용자 정의 함수 중 일부입니다.

S를 모든 단종 된 제품을 반환 하는 저장된 프로시저를 추가 하 여 시작할 수 있습니다. 새 저장된 프로시저 파일의 이름을 `GetDiscontinuedProducts.vb`입니다.


[![GetDiscontinuedProducts.vb 라는 새 저장된 프로시저를 추가 합니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image13.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image12.png)

**그림 8**: 라는 추가 하는 새 저장 프로시저 `GetDiscontinuedProducts.vb` ([클릭 하 여 큰 이미지 보기](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image14.png))


다음과 같은 내용으로 새 Visual Basic 클래스 파일을 만들어집니다.


[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample2.vb)]

저장된 프로시저도 구현 되는 `Shared` 내에서 메서드를 `Partial` 라는 클래스 파일 `StoredProcedures`합니다. 또한 합니다 `GetDiscontinuedProducts` 으로 데코 레이트 된 메서드를 [ `SqlProcedure` 특성](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlprocedureattribute.aspx), 저장 프로시저로 메서드를 표시 하는입니다.

다음 코드에서는 `SqlCommand` 개체 집합과 해당 `CommandText` 에 `SELECT` 의 모든 열에서 반환 하는 쿼리를 `Products` 제품에 대 한 테이블로 `Discontinued` 1 필드. 다음 명령을 실행 하 고 클라이언트 응용 프로그램에 다시 결과 보냅니다. 이 코드를 추가 하 여 `GetDiscontinuedProducts` 메서드.


[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample3.vb)]

새 쿼리 창을 열고 실행 하 여이 확인 된 [ 저장 프로시저입니다. 다음 오류 메시지를 받게 됩니다..NET Framework에서 사용자 코드의 실행이 비활성화 됩니다. Clr 사용 구성 옵션을 사용 하도록 설정 합니다. 검사 Northwind의 데이터베이스 구성 정보를 입력 하 고 명령을 실행 [ 쿼리 창에서.

> [!NOTE]
> 이 설정을 사용 하도록 설정 하는 clr 현재 0으로 설정 되어 있는지 보여 줍니다. Clr 사용 되도록 설정 되어 현재 설정 0 그림 12: clr 활성화 되도록 설정 되어 현재 설정 0 (큰 이미지를 보려면 클릭) 그림 12에 각 구성 설정에 나열 된 4 개의 값: 최소 및 최대 값과 구성 및 실행된 값입니다. Clr 사용 설정에 대 한 구성 값을 업데이트 하려면 다음 명령을 실행 합니다.


## <a name="step-4-deploying-the-managed-stored-procedure"></a>다시 실행 하는 경우는  위의 문은 1을 사용 하도록 설정 하는 clr 설정의 구성 값을 업데이트 하는 하지만 실행된 값을 0으로 계속 설정 되어 있는지 표시 됩니다.

이 구성 변경 내용을 적용 하려면 실행 해야 합니다   명령, 실행된 값을 현재 구성 값으로 설정 됩니다는 합니다. 단순히 입력  쿼리 창에서 도구 모음에서 실행 아이콘을 클릭 합니다. 실행 하는 경우  이제 clr 설정의 구성에 대 한 1의 값이 표시 하 고 값을 실행 해야 합니다. Clr 사용 구성 완료를 사용 하 여 관리 되는 실행 준비가 기꺼이 `ManagedDatabaseConstructs` 저장 프로시저입니다. 쿼리 창에서 입력 하 고 명령을 실행 합니다  합니다. 해당 관리 되는 코드를 사용 하면 저장된 프로시저를 호출 합니다  메서드를 실행 합니다. 이 코드가 실행을 `sp_dbcmptlevel` 쿼리 지원 및 SQL Server Management Studio에서이 인스턴스는 호출 응용 프로그램에이 데이터를 반환 하는 모든 제품을 반환 합니다.

Management Studio는 이러한 결과 수신 및 결과 창에 표시 합니다. 모든 저장된 프로시저 반환 GetDiscontinuedProducts 단종 된 제품만 그림 13: 합니다  저장 프로시저 반환 모든 지원 되지 않는 제품 (클릭 하 여 큰 이미지 보기) 5 단계: 관리 되는 만들기는 저장 프로시저 입력된 매개 변수를 수락 합니다. 다양 한 쿼리 및이 자습서 전체에서 만든 저장된 프로시저를 사용한 매개 변수합니다.

예를 들어 합니다 새 저장 프로시저 만들기 형식화 된 데이터 집합의 Tableadapter에 대 한 자습서 라는 저장된 프로시저를 만들었습니다  라는 입력된 매개 변수를 수락 하는 합니다.


[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample4.sql)]

저장된 프로시저가 반환한 모든 제품입니다  필드에 제공 된 값과 일치  매개 변수입니다.


[![입력된 매개 변수를 허용 하는 관리 되는 저장된 프로시저를 만들려면 s 메서드 정의에서 이러한 매개 변수를 지정 하면 됩니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image16.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image15.png)

**예를 들어 let s 다른 관리 되는 저장된 프로시저를 추가 합니다 **라는 프로젝트**합니다.


이 관리 되는 저장된 프로시저는 가격을 지정 하는 입력된 매개 변수를 수락 하 고 모든 제품을 반환 합니다 인  필드를 사용 하면 매개 변수의 값 보다 작습니다. 프로젝트에 새 저장된 프로시저를 추가 하려면 마우스 오른쪽 단추로 클릭는  프로젝트 이름 및 새 저장된 프로시저를 추가 하려면 선택 합니다.

3 단계에서에서 보았듯이 라는 메서드를 사용 하 여 새 C# 클래스 파일을 만들기는이  내에 배치 합니다  클래스 합니다. 업데이트를  허용 하도록 s 메서드 정의    라는 입력된 매개 변수  실행 하 고 쿼리 결과 반환 하는 코드를 작성 및: 합니다 `ManagedDatabaseConstructs` 정 및 코드의 유사한 메서드의 정 및 코드는  3 단계에서에서 만든 메서드.


![마법사의 마지막 화면을 사용 하면 사용 되는 데이터 액세스 패턴 및 결과 메서드의 이름을 지정할 수 있습니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image18.png)

**메서드를 확인 하는 확인란 및 이름을 모두를 둡니다 **고**입니다.


마법사를 완료 하려면 마침을 클릭 합니다. 메서드 FillByDiscontinued 이름과 GetDiscontinuedProducts 그림 18`ManagedDatabaseConstructs`: 메서드 이름을  하 고  (클릭 하 여 큰 이미지 보기) 라는 메서드를 만들려면 다음이 단계를 반복 `GetDiscontinuedProducts` 및 `GetDiscontinuedProducts` 에  에 대 한는  저장된 프로시저를 관리 합니다. 그림 19 메서드를 추가한 후 데이터 집합 디자이너의 스크린샷이 나와 합니다  에 대 한 합니다  및  저장된 프로시저를 관리 합니다.


![ProductsTableAdapter이이 단계에서 추가한 새 메서드를 포함 합니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image19.png)

**그림 19**: 합니다 `GetDiscontinuedProducts` 이 단계에서는 새 메서드 추가 포함 (클릭 하 여 큰 이미지 보기)


비즈니스 논리 계층에 해당 메서드를 추가 하는 7 단계: 4-5 단계에서 추가한 관리 되는 저장된 프로시저를 호출 하는 것에 대 한 메서드를 포함 하도록 데이터 액세스 계층을 업데이트 했으므로 해당 하는 메서드가 비즈니스 논리 계층에 추가 해야 합니다. 다음 두 가지 메서드를 추가 합니다  클래스: 두 메서드는 단순히 해당 DAL 메서드 호출 및 반환 된  인스턴스.

`exec sp_configure` 각 메서드 위의 태그 하면 이러한 메서드를 ObjectDataSource가의 데이터 소스 구성 마법사의 선택 탭의 드롭다운 목록에 포함 되어야 합니다. 8 단계: 관리 되는 호출에서 저장 프로시저는 프레젠테이션 계층


[![비즈니스 논리 및 데이터 액세스 계층을 사용 하 여 호출에 대 한 지원을 포함 하도록 확장 합니다 [ 및 ![ 저장된 프로시저를 관리 되는 이러한 이제 표시할 수 있습니다 ASP.NET 페이지를 통해 프로시저 결과 저장 합니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image21.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image20.png)

**엽니다는 **페이지에서** 폴더 및 도구 상자에서 GridView를 디자이너로 끌어 옵니다.


집합 GridView s  속성을  및 스마트 태그를 바인딩할 라는 새로운 ObjectDataSource는 합니다. ObjectDataSource에서 해당 데이터를 가져오도록 구성 합니다  s 클래스  메서드.


[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample5.sql)]

그림 20: ObjectDataSource 사용 하도록 구성 된  클래스 (클릭 하 여 큰 이미지 보기) GetDiscontinuedProducts 메서드 선택 탭의 드롭다운 목록에서 선택 그림 21: 선택 된  선택 탭의 드롭다운 목록에서 메서드 (클릭 하 여 큰 이미지 보기) 이 표는 표시 제품 정보만 데, 때문에 UPDATE, INSERT에서에서 드롭 다운 목록을 설정 한 탭 (없음)을 삭제 하 고 마침을 클릭 키를 누릅니다.

마법사를 완료 하면 Visual Studio는 자동으로 추가 BoundField 또는 CheckBoxField에서 각 데이터 필드에 대 한는 `GetDiscontinuedProducts`합니다. 잠시 시간을 제외 하 고이 필드를 제거할 `exec` 및 `GetDiscontinuedProducts`, 하는 시점에 GridView 및 ObjectDataSource가 선언적 태그는 다음과 유사 합니다. 브라우저를 통해이 페이지를 보려면 잠시 시간이 소요 됩니다. 해당 페이지를 방문 하는 경우, ObjectDataSource 호출을 `SELECT` s 클래스  메서드. 이 메서드는 DAL에 호출 7 단계에서에서 보았듯이  s 클래스  메서드를 호출 하는  저장 프로시저입니다.


[![이 저장된 프로시저 되어 관리 되는 저장 프로시저는 지원 되지 않는 제품을 반환 합니다. 3 단계에서에서 만든 코드를 실행 합니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image24.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image23.png)

**관리 되는 저장된 프로시저에서 반환 된 결과에 패키지 되는 ** dal 다음 GridView에 바인딩됩니다 및 표시 되는 프레젠테이션 계층으로 반환 하는 BLL을 하기 위해 반환한 합니다.


## <a name="step-5-creating-managed-stored-procedures-that-accept-input-parameters"></a>예상 대로 표 단종 된 제품을 나열 합니다.

지원 되지 않는 제품 나와 있습니다. 사용자 정의 함수의 장단점 관리 코드에서 SQL Server 2005 개체 만들기

SQL Server 2005의에서 관리 되는 코드를 사용 하 여 트리거를 만드는 중 방법: 만들기 및 실행 CLR SQL Server 저장 프로시저 방법: 만들기 및 CLR SQL Server 사용자 정의 함수를 실행 합니다.

방법: 편집 된  SQL 개체를 실행 하는 스크립트 파일 이름을 `GetProductsWithPriceLessThan.vb`로 지정합니다. 3 단계에서에서 보았듯이 라는 메서드를 사용 하 여 새 Visual Basic 클래스 파일을 만들기는이 `GetProductsWithPriceLessThan` 내에 배치 합니다 `Partial` 클래스 `StoredProcedures`합니다.

관리 코드와 SQL Server 2005 (비디오)


[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample6.vb)]

TRANSACT-SQL 참조 연습: 관리 코드에서 저장된 프로시저 만들기

이 자습서에 대 한 선행 검토자가 ren Jacob Lauritsen 했습니다. 이 문서에서는, S ren도 검토 하는 것 외에도 수동으로 관리 되는 데이터베이스 개체를 컴파일하는 데이 아티클의 다운로드에 포함 된 Visual C# Express Edition 프로젝트를 만들었습니다. 새 항목을 표시 해야 `GetProductsWithPriceLessThan`합니다. 쿼리 창에서 입력 하 고 명령을 실행 `exec GetProductsWithPriceLessThan 25`는 그림 14와 같이 $25 미만의 모든 제품 목록 됩니다.


[![제품에서 25 달러 표시 됩니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image27.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image26.png)

**그림 14**: 제품 25 달러에서 표시 됩니다 ([큰 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image28.png))


## <a name="step-6-calling-the-managed-stored-procedure-from-the-data-access-layer"></a>6 단계: 데이터 액세스 계층에서 관리 되는 저장된 프로시저를 호출합니다.

추가한 이때 합니다 `GetDiscontinuedProducts` 및 `GetProductsWithPriceLessThan` 저장된 프로시저를 관리 되는 `ManagedDatabaseConstructs` 프로젝트 및 Northwind SQL Server 데이터베이스를 사용 하 여 등록 한 합니다. 또한 SQL Server Management Studio에서 이러한 관리 되는 저장된 프로시저를 호출 했습니다 (그림 13 및 14 참조). 그러나이 ASP.NET에서 응용 프로그램을 사용 하 여 관리 되는 저장된 프로시저, 데이터 액세스 및 비즈니스 논리 계층 아키텍처에서에 추가 해야 합니다. 이 단계에서는 두 개의 새 메서드를 추가 합니다 `ProductsTableAdapter` 에 `NorthwindWithSprocs` 형식화 된 데이터 집합에서 처음에 만든를 [새 저장 프로시저 만들기 형식화 된 데이터 집합의 Tableadapter에 대 한](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md) 자습서. 7 단계에서에서 BLL에 해당 하는 메서드가 추가 하겠습니다.

엽니다는 `NorthwindWithSprocs` Visual Studio에서 시작 하는 새 메서드를 추가 하 여 형식화 된 데이터 집합을 `ProductsTableAdapter` 라는 `GetDiscontinuedProducts`. 새 메서드가 TableAdapter에 추가할 디자이너의 TableAdapter의 이름을 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 추가 쿼리 옵션을 선택 합니다.

> [!NOTE]
> Northwind 데이터베이스를 이동 하므로 `App_Data` SQL Server 2005 Express Edition 데이터베이스 인스턴스 폴더를 반드시이 변경 내용을 반영 하기 위해 Web.config에서 해당 연결 문자열 업데이트 한다는 합니다. 업데이트 설명한 2 단계에에서는 `NORTHWNDConnectionString` 값 `Web.config`합니다. 이 업데이트를 확인 하는 것을 잊어버린 경우 다음 메시지가 표시 됩니다는 오류 실패 쿼리를 추가 합니다. 연결을 찾을 수 없습니다 `NORTHWNDConnectionString` 개체에 대 한 `Web.config` TableAdapter에 새 메서드를 추가 하려고 할 때 대화 상자에서. 이 오류를 해결 하려면 확인을 클릭 하 고 이동 `Web.config` 업데이트는 `NORTHWNDConnectionString` 2 단계에서에서 설명 했 듯이 값입니다. TableAdapter 추가 메서드를 다시 시도 합니다. 이 오류 없이 작동 해야 합니다.


새 메서드 추가 이전 자습서에서 많이 사용 했습니다는 TableAdapter 쿼리 구성 마법사를 시작 합니다. 첫 번째 단계에서는 TableAdapter는 데이터베이스에 액세스 해야 하는 방법을 지정 하려면: 기존 또는 새 저장된 프로시저 또는 임시 SQL 문을 통해. 이미 생성 하 고 등록 하므로 `GetDiscontinuedProducts` 프로시저 옵션을 저장 하 고 다음을 누릅니다 사용 하 여 기존 데이터베이스를 사용 하 여 관리 되는 저장된 프로시저를 선택 합니다.


[![기존 저장된 프로시저 옵션 사용 선택](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image30.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image29.png)

**그림 15**: 사용 하 여 기존 프로시저 옵션을 선택 ([큰 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image31.png))


다음 화면 메서드가 호출할 저장된 프로시저에 대 한 요청입니다. 선택 된 `GetDiscontinuedProducts` 드롭 다운 목록에서 저장된 프로시저를 관리 하 고 다음을 누릅니다.


[![GetDiscontinuedProducts 관리 저장된 프로시저 선택](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image33.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image32.png)

**그림 16**: 선택 된 `GetDiscontinuedProducts` 관리 되는 저장 프로시저 ([클릭 하 여 큰 이미지 보기](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image34.png))


우리는 다음 저장된 프로시저가 행, 단일 값 또는 nothing을 반환 하는지 여부를 지정 하 라는 메시지가 표시 됩니다. 이후 `GetDiscontinuedProducts` 집합을 반환 합니다 지원 되지 않는 제품 행의 첫 번째 옵션 (테이블 형식 데이터)를 선택 하 고 다음을 클릭 합니다.


[![테이블 형식 데이터 옵션을 선택 합니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image36.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image35.png)

**그림 17**: 테이블 형식 데이터 옵션을 선택 ([큰 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image37.png))


마법사의 마지막 화면을 사용 하면 사용 되는 데이터 액세스 패턴 및 결과 메서드의 이름을 지정할 수 있습니다. 메서드를 확인 하는 확인란 및 이름을 모두를 둡니다 `FillByDiscontinued` 고 `GetDiscontinuedProducts`입니다. 마법사를 완료 하려면 마침을 클릭 합니다.


[![메서드 FillByDiscontinued 이름과 GetDiscontinuedProducts](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image39.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image38.png)

**그림 18**: 메서드 이름을 `FillByDiscontinued` 하 고 `GetDiscontinuedProducts` ([클릭 하 여 큰 이미지 보기](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image40.png))


라는 메서드를 만들려면 다음이 단계를 반복 `FillByPriceLessThan` 및 `GetProductsWithPriceLessThan` 에 `ProductsTableAdapter` 에 대 한는 `GetProductsWithPriceLessThan` 저장된 프로시저를 관리 합니다.

그림 19 메서드를 추가한 후 데이터 집합 디자이너의 스크린샷이 나와 합니다 `ProductsTableAdapter` 에 대 한 합니다 `GetDiscontinuedProducts` 및 `GetProductsWithPriceLessThan` 저장된 프로시저를 관리 합니다.


[![ProductsTableAdapter이이 단계에서 추가한 새 메서드를 포함 합니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image42.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image41.png)

**그림 19**: 합니다 `ProductsTableAdapter` 이 단계에서는 새 메서드 추가 포함 ([클릭 하 여 큰 이미지 보기](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image43.png))


## <a name="step-7-adding-corresponding-methods-to-the-business-logic-layer"></a>비즈니스 논리 계층에 해당 메서드를 추가 하는 7 단계:

4-5 단계에서 추가한 관리 되는 저장된 프로시저를 호출 하는 것에 대 한 메서드를 포함 하도록 데이터 액세스 계층을 업데이트 했으므로 해당 하는 메서드가 비즈니스 논리 계층에 추가 해야 합니다. 다음 두 가지 메서드를 추가 합니다 `ProductsBLLWithSprocs` 클래스:


[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample7.vb)]

두 메서드는 단순히 해당 DAL 메서드 호출 및 반환 된 `ProductsDataTable` 인스턴스. `DataObjectMethodAttribute` 각 메서드 위의 태그 하면 이러한 메서드를 ObjectDataSource가의 구성 데이터 원본 마법사의 선택 탭의 드롭다운 목록에 포함 되어야 합니다.

## <a name="step-8-invoking-the-managed-stored-procedures-from-the-presentation-layer"></a>8 단계: 관리 되는 호출에서 저장 프로시저는 프레젠테이션 계층

비즈니스 논리 및 데이터 액세스 계층을 사용 하 여 호출에 대 한 지원을 포함 하도록 확장 합니다 `GetDiscontinuedProducts` 및 `GetProductsWithPriceLessThan` 저장된 프로시저를 관리 되는 이러한 이제 표시할 수 있습니다 ASP.NET 페이지를 통해 프로시저 결과 저장 합니다.

엽니다는 `ManagedFunctionsAndSprocs.aspx` 페이지에서 `AdvancedDAL` 폴더 및 도구 상자에서 GridView를 디자이너로 끌어 옵니다. 집합 GridView s `ID` 속성을 `DiscontinuedProducts` 및 스마트 태그를 바인딩할 라는 새로운 ObjectDataSource는 `DiscontinuedProductsDataSource`합니다. ObjectDataSource에서 해당 데이터를 가져오도록 구성 합니다 `ProductsBLLWithSprocs` s 클래스 `GetDiscontinuedProducts` 메서드.


[![ProductsBLLWithSprocs 클래스를 사용 하는 ObjectDataSource 구성](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image45.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image44.png)

**그림 20**: ObjectDataSource 사용 하도록 구성 된 `ProductsBLLWithSprocs` 클래스 ([클릭 하 여 큰 이미지 보기](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image46.png))


[![GetDiscontinuedProducts 메서드 선택 탭의 드롭다운 목록에서 선택](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image48.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image47.png)

**그림 21**: 선택 된 `GetDiscontinuedProducts` 선택 탭의 드롭다운 목록에서 메서드 ([클릭 하 여 큰 이미지 보기](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image49.png))


이 표는 표시 제품 정보만 데, 때문에 UPDATE, INSERT에서에서 드롭 다운 목록을 설정 한 탭 (없음)을 삭제 하 고 마침을 클릭 키를 누릅니다.

마법사를 완료 하면 Visual Studio는 자동으로 추가 BoundField 또는 CheckBoxField에서 각 데이터 필드에 대 한는 `ProductsDataTable`합니다. 잠시 시간을 제외 하 고이 필드를 제거할 `ProductName` 및 `Discontinued`, 하는 시점에 GridView 및 ObjectDataSource가 선언적 태그는 다음과 유사 합니다.


[!code-aspx[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample8.aspx)]

브라우저를 통해이 페이지를 보려면 잠시 시간이 소요 됩니다. 해당 페이지를 방문 하는 경우, ObjectDataSource 호출을 `ProductsBLLWithSprocs` s 클래스 `GetDiscontinuedProducts` 메서드. 이 메서드는 DAL에 호출 7 단계에서에서 보았듯이 `ProductsDataTable` s 클래스 `GetDiscontinuedProducts` 메서드를 호출 하는 `GetDiscontinuedProducts` 저장 프로시저입니다. 이 저장된 프로시저 되어 관리 되는 저장 프로시저는 지원 되지 않는 제품을 반환 합니다. 3 단계에서에서 만든 코드를 실행 합니다.

관리 되는 저장된 프로시저에서 반환 된 결과에 패키지 되는 `ProductsDataTable` dal 다음 GridView에 바인딩됩니다 및 표시 되는 프레젠테이션 계층으로 반환 하는 BLL을 하기 위해 반환한 합니다. 예상 대로 표 단종 된 제품을 나열 합니다.


[![지원 되지 않는 제품 나와 있습니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image51.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image50.png)

**그림 22**:은 지원 되지 않는 제품 나열 됩니다 ([큰 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image52.png))


자세한 연습을 위해 페이지에 텍스트 상자와 다른 GridView를 추가 합니다. 가이 GridView를 호출 하 여 텍스트 상자에 입력 크기 보다 작은 제품을 표시 합니다 `ProductsBLLWithSprocs` s 클래스 `GetProductsWithPriceLessThan` 메서드.

## <a name="step-9-creating-and-calling-t-sql-udfs"></a>9 단계: 만들기 및 T-SQL Udf를 호출 합니다.

사용자 정의 함수 또는 Udf 데이터베이스 개체를 유사 하 게 모방할 프로그래밍 언어에서 함수의 의미 체계는입니다. Visual Basic의 함수 처럼 Udf는 가변 개수의 입력된 매개 변수를 포함 하 고 특정 형식의 값을 반환할 수 있습니다. UDF는 스칼라 데이터-문자열, 정수 및 등-또는 테이블 형식 데이터를 반환할 수 있습니다. 두 유형의 스칼라 데이터 형식을 반환 하는 UDF를 사용 하 여 시작 하는 Udf 간단히 살펴보십시오 s 수 있습니다.

다음 UDF는 특정 제품 재고의 예상된 값을 계산합니다. 세 개의 입력된 매개 변수에서 수행 하 여 수행 합니다 `UnitPrice`, `UnitsInStock`, 및 `Discontinued` 형식의 값을 반환 하는 특정 제품에 대 한 값 `money`합니다. 재고의 예상된 값을 곱하여 계산 합니다 `UnitPrice` 여는 `UnitsInStock`합니다. 지원 되지 않는 항목에 대 한이 값을 사용 하는 50% 감소 합니다.


[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample9.sql)]

이 UDF를 데이터베이스에 추가한 후 Management Studio를 통해 프로그래밍 기능 폴더에 다음 함수를 및 다음 스칼라 반환 함수를 확장 하 여 찾을 수 있습니다. 사용할 수는 `SELECT` 같이 쿼리:


[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample10.sql)]

추가한는 `udf_ComputeInventoryValue` Northwind 데이터베이스에 대 한 UDF 그림 23 위의 출력을 보여 줍니다. `SELECT` Management Studio를 통해 볼 때를 쿼리 합니다. 개체 탐색기에서 해당 스칼라 반환 함수 폴더 아래에 UDF 나열 되어 있는지 참고도 합니다.


[![각 제품 재고 값이 나열 됩니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image54.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image53.png)

**그림 23**: 인벤토리 값은 나열 된 각 제품 s ([큰 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image55.png))


Udf는 테이블 형식 데이터를 반환할 수도 있습니다. 예를 들어 특정 범주에 속하는 제품을 반환 하는 UDF를 만들 수 있습니다.


[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample11.sql)]

합니다 `udf_GetProductsByCategoryID` UDF 허용을 `@CategoryID` 입력된 매개 변수 및 반환 된 결과 `SELECT` 쿼리 합니다. 이 UDF를 만든 후에 참조할 수 있습니다 합니다 `FROM` (또는 `JOIN`) 절을 `SELECT` 쿼리 합니다. 다음 예제에서는 반환 된 `ProductID`, `ProductName`, 및 `CategoryID` 각 여 음료에 대 한 값입니다.


[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample12.sql)]

추가한는 `udf_GetProductsByCategoryID` Northwind 데이터베이스에 대 한 UDF 그림 24 위의 출력을 보여 줍니다. `SELECT` Management Studio를 통해 볼 때를 쿼리 합니다. 개체 탐색기가의 테이블 반환 함수 폴더에 표 형식 데이터를 반환 하는 Udf는 찾을 수 있습니다.


[![각 음료에 대 한 ProductID, ProductName, 및 CategoryID 나와](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image57.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image56.png)

**그림 24**: 합니다 `ProductID`, `ProductName`, 및 `CategoryID` 각 Beverage 나열 됩니다 ([클릭 하 여 큰 이미지 보기](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image58.png))


> [!NOTE]
> 작성 및 Udf를 사용 하 여에 대 한 자세한 내용은 체크 아웃 [사용자 정의 함수에 대 한 소개](http://www.sqlteam.com/item.asp?ItemID=1955)합니다. 또한 체크 아웃 [장점과 Drawbacks of User-Defined 함수](http://www.samspublishing.com/articles/article.asp?p=31724&amp;rl=1)합니다.


## <a name="step-10-creating-a-managed-udf"></a>10 단계: 관리 되는 UDF 만들기

합니다 `udf_ComputeInventoryValue` 고 `udf_GetProductsByCategoryID` 위의 예제에서 만든 Udf는 T-SQL 데이터베이스 개체입니다. SQL Server 2005에서는 추가할 수 있는 관리 되는 Udf를 `ManagedDatabaseConstructs` 관리 되는 저장 프로시저 단계 3에서 및 5와 마찬가지로 프로젝트입니다. 이 단계를 구현 하는 s 하도록는 `udf_ComputeInventoryValue` 관리 코드에서 UDF 합니다.

관리 되는 UDF를 추가 하는 `ManagedDatabaseConstructs` 프로젝트, 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 새 항목을 추가 하려면 선택 합니다. 새 항목 추가 대화 상자에서 사용자 정의 템플릿을 선택 하 고 새 UDF 파일의 이름을 `udf_ComputeInventoryValue_Managed.vb`입니다.


[![새 관리 되는 UDF ManagedDatabaseConstructs 프로젝트에 추가](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image60.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image59.png)

**그림 25**: 새 관리 되는 UDF를 추가 합니다 `ManagedDatabaseConstructs` 프로젝트 ([클릭 하 여 큰 이미지 보기](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image61.png))


사용자 정의 함수 템플릿은 만듭니다는 `Partial` 라는 클래스 `UserDefinedFunctions` 클래스의 파일 이름과 동일한 이름이 메서드를 사용 하 여 (`udf_ComputeInventoryValue_Managed`, 이런에서). 이 메서드를 사용 하 여 데코 레이트 된 합니다 [ `SqlFunction` 특성](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlfunctionattribute.aspx), 관리 되는 UDF 메서드로 플래그입니다.


[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample13.vb)]

합니다 `udf_ComputeInventoryValue` 현재 메서드는 [ `SqlString` 개체](https://msdn.microsoft.com/library/system.data.sqltypes.sqlstring.aspx) 이며 입력 매개 변수를 수락 하지 않습니다. 에 세 개의 매개 변수 입력을 허용 하도록 메서드 정의 업데이트 해야 `UnitPrice`, `UnitsInStock`, 및 `Discontinued` -반환을 `SqlMoney` 개체입니다. 재고 현황 값을 계산 하기 위한 논리는 T-SQL에서 동일한 `udf_ComputeInventoryValue` UDF 합니다.


[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample14.vb)]

UDF의 메서드에 입력된 매개 변수는 해당 SQL 형식 참고: `SqlMoney` 에 대 한 합니다 `UnitPrice` 필드 [ `SqlInt16` ](https://msdn.microsoft.com/library/system.data.sqltypes.sqlint16.aspx) 에 대 한 `UnitsInStock`, 및 [ `SqlBoolean` ](https://msdn.microsoft.com/library/system.data.sqltypes.sqlboolean.aspx) 에 대 한 `Discontinued`합니다. 이러한 데이터 형식에 정의 된 형식을 반영 합니다 `Products` 테이블: 합니다 `UnitPrice` 형식의 열이 `money`, `UnitsInStock` 형식의 열 `smallint`, 및 `Discontinued` 형식의 열 `bit`.

만들어 시작 하는 코드를 `SqlMoney` 명명 된 인스턴스 `inventoryValue` 할당 된 값이 0입니다. 합니다 `Products` 데이터베이스에 대 한 테이블을 사용 하면 `NULL` 값을 `UnitsInPrice` 및 `UnitsInStock` 열입니다. 이러한 값이 들어 있는지 확인 하려면 첫 번째 확인 해야 하므로 `NULL` s를 통해 합니다 `SqlMoney` s 개체 [ `IsNull` 속성](https://msdn.microsoft.com/library/system.data.sqltypes.sqlmoney.isnull.aspx)합니다. 모두 `UnitPrice` 및 `UnitsInStock` 포함 이외`NULL` 계산 값을 `inventoryValue` 두 제품 수를 합니다. 그런 다음 경우 `Discontinued` true 이면 값을 절반으로 줄일 것입니다.

> [!NOTE]
> 합니다 `SqlMoney` 만 개체를 두 개 사용 하면 `SqlMoney` 함께 곱할 인스턴스. 허용 하지 않습니다는 `SqlMoney` 인스턴스 리터럴 부동 소수점 숫자를 곱합니다. 따라서를 절반으로 줄일 `inventoryValue` 새으로 곱하는 것 `SqlMoney` 값이 0.5 이거나 된 인스턴스.


## <a name="step-11-deploying-the-managed-udf"></a>11 단계: 관리 되는 UDF를 배포합니다.

이제 만든 관리 되는 UDF를 Northwind 데이터베이스에 배포 해야 합니다. 4 단계에서에서 살펴본 것 처럼 SQL Server 프로젝트의 관리 되는 개체는 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 배포 옵션을 선택 하 여 배포 됩니다.

프로젝트를 배포한 후에 SQL Server Management Studio로 돌아가서 하 고 스칼라 반환 함수 폴더를 새로 고칩니다. 이제 두 개의 항목이 표시 됩니다.

- `dbo.udf_ComputeInventoryValue` -9 단계에서에서 만든 T-SQL UDF 및
- `dbo.udf ComputeInventoryValue_Managed` -관리 되는 UDF 방금 배포한 10 단계에서에서 생성 합니다.

이 관리 되는 UDF를 테스트 하려면 Management Studio 내에서 다음 쿼리를 실행 합니다.


[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample15.sql)]

이 명령은 관리 되는 `udf ComputeInventoryValue_Managed` T-SQL 대신 UDF `udf_ComputeInventoryValue` UDF 되지만 출력은 동일 합니다. 그림 23 UDF가의 출력의 스크린샷을 볼를 다시 가리킵니다.

## <a name="step-12-debugging-the-managed-database-objects"></a>12 단계: 관리 되는 데이터베이스 개체 디버깅

에 [저장 프로시저 디버깅](debugging-stored-procedures-vb.md) 디버깅 Visual Studio를 통해 SQL Server에 대 한 옵션을 설명한 세 가지 자습서: 직접 데이터베이스 디버깅, 응용 프로그램 디버깅 및 SQL Server 프로젝트에서 디버깅 합니다. 클라이언트 응용 프로그램에서 SQL Server 프로젝트에서 직접 관리 되는 database 개체를 통해 직접 데이터베이스 디버깅 디버깅할 수 없습니다 있지만 디버깅할 수 있습니다. 그러나 디버깅을 수행 하려면, SQL Server 2005 데이터베이스 허용 되어야 SQL/CLR 디버깅 합니다. 처음 만들 때 회수 하는 `ManagedDatabaseConstructs` 프로젝트 Visual Studio 질문 여부 SQL/CLR 디버깅 (2 단계에서에서 그림 6 참조)를 사용 하도록 설정 하려고 했습니다. 서버 탐색기 창에서 데이터베이스를 마우스 오른쪽 단추로 클릭 하 여이 설정을 수정할 수 있습니다.


![데이터베이스 SQL/CLR 디버깅을 허용 하는지 확인](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image62.png)

**그림 26**: 데이터베이스 SQL/CLR 디버깅을 허용 하는지 확인


디버깅 하 려 한다고 가정 합니다 `GetProductsWithPriceLessThan` 저장된 프로시저를 관리 합니다. 코드 내에서 중단점을 설정 하 여 먼저는 `GetProductsWithPriceLessThan` 메서드.


[![GetProductsWithPriceLessThan 메서드에서 중단점을 설정 합니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image64.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image63.png)

**그림 27**:에서 중단점을 설정 합니다 `GetProductsWithPriceLessThan` 메서드 ([클릭 하 여 큰 이미지 보기](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image65.png))


SQL Server 프로젝트에서 관리 되는 데이터베이스 개체 디버깅 소개가 있습니다. 솔루션 프로젝트가-를 포함 하므로 합니다 `ManagedDatabaseConstructs` Visual Studio를 시작 하도록 지시 해야 SQL Server 프로젝트에서 디버그 하기 위해 웹 사이트-와 함께 SQL Server 프로젝트는 `ManagedDatabaseConstructs` SQL Server 프로젝트 디버깅을 시작 했습니다. 마우스 오른쪽 단추로 클릭는 `ManagedDatabaseConstructs` 솔루션 탐색기에서 프로젝트 및 상황에 맞는 메뉴에서 시작 프로젝트 옵션으로 집합을 선택 합니다.

경우는 `ManagedDatabaseConstructs` 프로젝트에서 SQL 문 실행이 디버거에서 시작 되는 `Test.sql` 파일에 있는 `Test Scripts` 폴더입니다. 예를 들어, 테스트 하는 `GetProductsWithPriceLessThan` 저장된 프로시저를 관리 되는 기존 `Test.sql` 파일 콘텐츠를 호출 하는 다음 문 사용 하 여 합니다 `GetProductsWithPriceLessThan` 전달 하는 저장된 프로시저를 관리 되는 `@CategoryID` 14.95 값:


[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample16.sql)]

적 위의 스크립트를 입력 한 후 `Test.sql`, 디버그 메뉴로 이동 하 고 디버깅 시작을 선택 하거나 F5를 눌러 디버깅을 시작 또는 도구 모음에서 녹색 재생 아이콘입니다. 솔루션 내의 프로젝트를 빌드, Northwind 데이터베이스를 관리 되는 데이터베이스 개체를 배포 및 실행 하는이 `Test.sql` 스크립트입니다. 이 시점에서 중단점에 도달 하 고 단계별로 실행할 수 있습니다는 `GetProductsWithPriceLessThan` 메서드의 입력된 매개 변수의 값을 확인 및 등입니다.


[![GetProductsWithPriceLessThan 메서드의 중단점에 도달](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image67.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image66.png)

**그림 28**:에서 중단점 합니다 `GetProductsWithPriceLessThan` 메서드 적중 되었음을 ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image68.png))


클라이언트 응용 프로그램을 통해 디버그 해야 하는 SQL 데이터베이스 개체에 대 한 순서 대로 반드시 해당 데이터베이스 응용 프로그램 디버깅을 지원 하도록 구성 합니다. 서버 탐색기에서 데이터베이스 단추로 클릭 하 고 응용 프로그램 디버깅 옵션이 선택 되어 있는지 확인 합니다. 또한 SQL 디버거를 사용 하 여 통합 하 고 연결 풀링을 사용 하지 않도록 설정 하려면 ASP.NET 응용 프로그램을 구성 해야 합니다. 이 단계의 2 단계에서에서 자세히 설명한 합니다 [저장 프로시저 디버깅](debugging-stored-procedures-vb.md) 자습서입니다.

ASP.NET 응용 프로그램 및 데이터베이스를 구성한 후에 ASP.NET 웹 사이트를 시작 프로젝트로 설정 및 디버깅을 시작 합니다. 중단점을 관리 되는 개체 중 하나를 호출 하는 페이지를 방문 하는 경우 응용 프로그램이 중단 됩니다 및 컨트롤 설정 됩니다 하 고 디버거를 단계별로 실행할 수 있습니다 코드 그림 28 에서처럼 합니다.

## <a name="step-13-manually-compiling-and-deploying-managed-database-objects"></a>13 단계: 수동으로 컴파일 및 배포 관리 되는 데이터베이스 개체

SQL Server 프로젝트를 사용 하면 쉽게 생성, 컴파일 및 관리 되는 데이터베이스 개체를 배포에 있습니다. 그러나 SQL Server 프로젝트 에서만 사용할 Visual Studio Professional 및 Team 시스템 버전입니다. 표준 버전의 Visual Studio 또는 Visual Web Developer를 사용 하는 관리 되는 데이터베이스 개체를 사용 하려는 경우를 수동으로 만들고 배포 해야 합니다. 여기에 네 가지 단계가 포함 됩니다.

1. 관리 되는 데이터베이스 개체에 대 한 소스 코드를 포함 하는 파일 만들기
2. 개체를 어셈블리로 컴파일
3. SQL Server 2005 데이터베이스를 사용 하 여 어셈블리를 등록 하 고
4. 어셈블리의 적절 한 메서드를 가리키는 SQL Server에서 데이터베이스 개체를 만듭니다.

관리 되는 이러한 제품을 반환 하는 저장된 프로시저를 이러한 작업을 설명, 만든 새 인 `UnitPrice` 지정된 된 값 보다 큽니다. 라는 컴퓨터에서 새 파일을 만들 `GetProductsWithPriceGreaterThan.vb` 파일에 다음 코드를 입력 하 고 (사용할 수 있습니다 Visual Studio, 메모장 또는 원하는 텍스트 편집기 그러려면):


[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample17.vb)]

이 코드는 거의 동일 합니다는 `GetProductsWithPriceLessThan` 5 단계에서에서 만든 메서드. 유일한 차이점은 메서드 이름을 `WHERE` 절 및 쿼리에 사용 되는 매개 변수 이름입니다. 다시는 `GetProductsWithPriceLessThan` 메서드를 `WHERE` 절을 읽을: `WHERE UnitPrice < @MaxPrice`합니다. 여기에서 `GetProductsWithPriceGreaterThan`를 사용 하 여: `WHERE UnitPrice > @MinPrice` 합니다.

이제이 클래스를 어셈블리로 컴파일할 해야 합니다. 명령줄에서 저장 한 디렉터리로 이동 합니다 `GetProductsWithPriceGreaterThan.vb` 파일을 C# 컴파일러를 사용 하 여 (`csc.exe`) 어셈블리에 클래스 파일을 컴파일하려면:


[!code-console[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample18.cmd)]

경우 v가 있는 폴더로 `bc.exe` 에서 s 시스템에 없는 `PATH`, 완벽 하 게 해당 경로 참조 해야 `%WINDOWS%\Microsoft.NET\Framework\version\`, 다음과 같이:


[!code-console[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample19.cmd)]


[![GetProductsWithPriceGreaterThan.vb 어셈블리로 컴파일](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image70.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image69.png)

**그림 29**: 컴파일 `GetProductsWithPriceGreaterThan.vb` 에 어셈블리 ([클릭 하 여 큰 이미지 보기](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image71.png))


`/t` Visual Basic 클래스 파일을 DLL (실행 파일 대신)으로 컴파일되어야 함을 지정 하는 플래그입니다. `/out` 결과 어셈블리의 이름을 지정 하는 플래그입니다.

> [!NOTE]
> 컴파일하는 대신 합니다 `GetProductsWithPriceGreaterThan.vb` 사용 하 여 또는 명령줄에서 클래스 파일 [Visual Basic Express Edition](https://msdn.microsoft.com/vstudio/express/vb/) 하거나 Visual Studio Standard Edition에서는 별도 클래스 라이브러리 프로젝트를 만듭니다. S ren Jacob Lauritsen에 대 한 코드를 사용 하 여 이러한 Visual Basic Express Edition 프로젝트를 제공한 내용이 `GetProductsWithPriceGreaterThan` 저장된 프로시저와 두 개의 저장된 프로시저 관리 되며, 3, 5, 10 단계에서 만든 UDF 합니다. S ren s 프로젝트에는 해당 데이터베이스 개체를 추가 하는 데 필요한 T-SQL 명령을 포함 됩니다.


어셈블리로 컴파일되는 코드를에서는 SQL Server 2005 데이터베이스 내에서 어셈블리를 등록할 준비가 된 것입니다. 를 사용 하 여 T-SQL 명령을 통해 수행할 수 있습니다 `CREATE ASSEMBLY`, 또는 SQL Server Management Studio를 통해. Management Studio를 사용 하 여 s 포커스를 있습니다.

Management Studio에서 Northwind 데이터베이스의 프로그래밍 기능 폴더를 확장 합니다. 해당 하위 폴더 중 하나에 어셈블리입니다. 데이터베이스에 새 어셈블리를 수동으로 추가 하려면 어셈블리 폴더를 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 새 어셈블리를 선택 합니다. 새 어셈블리 대화 상자 (그림 30 참조)이 표시 됩니다. 찾아보기 단추를 클릭 합니다 `ManuallyCreatedDBObjects.dll` 어셈블리 방금 컴파일한 하 고 데이터베이스에 어셈블리를 추가 하려면 확인을 클릭 합니다. 표시 되지 않아야 합니다 `ManuallyCreatedDBObjects.dll` 개체 탐색기에서 어셈블리입니다.


[![데이터베이스에 ManuallyCreatedDBObjects.dll 어셈블리 추가](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image73.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image72.png)

**그림 30**: 추가 된 `ManuallyCreatedDBObjects.dll` 데이터베이스에 어셈블리 ([클릭 하 여 큰 이미지 보기](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image74.png))


![개체 탐색기에는 ManuallyCreatedDBObjects.dll 나열 됩니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image75.png)

**그림 31**:는 `ManuallyCreatedDBObjects.dll` 개체 탐색기에 나열 됩니다


Northwind 데이터베이스에 어셈블리를 추가 했지만, 아직 사용 하 여 저장된 프로시저를 연결 하는 `GetProductsWithPriceGreaterThan` 어셈블리의 메서드입니다. 이렇게 하려면 새 쿼리 창을 열고 다음 스크립트를 실행 합니다.


[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample20.sql)]

이 명명 된 Northwind 데이터베이스에 새 저장된 프로시저를 만듭니다 `GetProductsWithPriceGreaterThan` 관리 되는 메서드를 사용 하 여 연결 `GetProductsWithPriceGreaterThan` (클래스에는 `StoredProcedures`, 어셈블리에 `ManuallyCreatedDBObjects`).

위의 스크립트를 실행 한 후 개체 탐색기에서 저장 프로시저 폴더를 새로 고칩니다. 새 저장된 프로시저 항목을 표시 해야 `GetProductsWithPriceGreaterThan` -옆에 자물쇠 아이콘이 있는 합니다. 이 저장된 프로시저를 테스트 하려면 입력 하 고 쿼리 창에서 다음 스크립트를 실행 합니다.


[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample21.sql)]

그림 32에서 알 수 있듯이, 위의 명령을 사용 하 여 해당 제품에 대 한 정보를 표시 하는 한 `UnitPrice` $24.95 보다 큽니다.


[![개체 탐색기에는 ManuallyCreatedDBObjects.dll 나열 됩니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image77.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image76.png)

**그림 32**: 합니다 `ManuallyCreatedDBObjects.dll` 개체 탐색기에 나열 됩니다 ([클릭 하 여 큰 이미지 보기](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image78.png))


## <a name="summary"></a>요약

Microsoft SQL Server 2005와 언어 런타임 (CLR (공용), 데이터베이스 개체를 관리 되는 코드를 사용 하 여 만들 수를 허용 하는 통합을 제공 합니다. 이전에 T-SQL을 사용 하 여 이러한 데이터베이스 개체를 만들 수 있었습니다 했지만 이제는.NET 프로그래밍 Visual Basic과 같은 언어를 사용 하 여 이러한 개체 만들 수 있습니다. 이 자습서에서 만든 두 개의 관리 되는 저장된 프로시저 및 관리 되는 사용자 정의 함수.

Visual Studio가의 SQL Server 프로젝트 형식 만들기, 컴파일 및 관리 되는 데이터베이스 개체 배포를 지원 합니다. 또한 다양 한 디버깅 지원을 제공합니다. 그러나 SQL Server 프로젝트 형식은 Visual Studio Professional 및 Team 시스템 버전에서 사용할 수 있습니다만 합니다. Visual Web Developer 또는 표준 버전의 Visual Studio, 생성, 컴파일 및 배포 단계를 사용 하 여 수동으로 수행 해야, 13 단계에서에서 보았듯이 합니다.

즐거운 프로그래밍!

## <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [사용자 정의 함수의 장단점](http://www.samspublishing.com/articles/article.asp?p=31724&amp;rl=1)
- [관리 코드에서 SQL Server 2005 개체 만들기](https://channel9.msdn.com/Showpost.aspx?postid=142413)
- [SQL Server 2005의에서 관리 되는 코드를 사용 하 여 트리거를 만드는 중](http://www.15seconds.com/issue/041006.htm)
- [방법: 만들기 및 실행 CLR SQL Server 저장 프로시저](https://msdn.microsoft.com/library/5czye81z(VS.80).aspx)
- [방법: 만들기 및 CLR SQL Server 사용자 정의 함수를 실행 합니다.](https://msdn.microsoft.com/library/w2kae45k(VS.80).aspx)
- [방법: 편집 된 `Test.sql` SQL 개체를 실행 하는 스크립트](https://msdn.microsoft.com/library/ms233682(VS.80).aspx)
- [소개 사용자 정의 함수](http://www.sqlteam.com/item.asp?ItemID=1955)
- [관리 코드와 SQL Server 2005 (비디오)](https://channel9.msdn.com/Showpost.aspx?postid=142413)
- [TRANSACT-SQL 참조](https://msdn.microsoft.com/library/aa299742(SQL.80).aspx)
- [연습: 관리 코드에서 저장된 프로시저 만들기](https://msdn.microsoft.com/library/zxsa8hkf(VS.80).aspx)

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자가 ren Jacob Lauritsen 했습니다. 이 문서에서는, S ren도 검토 하는 것 외에도 수동으로 관리 되는 데이터베이스 개체를 컴파일하는 데이 아티클의 다운로드에 포함 된 Visual C# Express Edition 프로젝트를 만들었습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](debugging-stored-procedures-vb.md)
