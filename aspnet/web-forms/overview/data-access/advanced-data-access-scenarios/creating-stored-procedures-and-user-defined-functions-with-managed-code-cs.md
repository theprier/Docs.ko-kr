---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/creating-stored-procedures-and-user-defined-functions-with-managed-code-cs
title: "관리 코드 (C#)를 저장된 프로시저 및 사용자 정의 함수 만들기 | Microsoft Docs"
author: rick-anderson
description: "Microsoft SQL Server 2005 개발자가 관리 되는 코드를 통해 데이터베이스 개체를 만들 수 있도록.NET 공용 언어 런타임 통합 합니다. 이 자습서 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/03/2007
ms.topic: article
ms.assetid: 213eea41-1ab4-4371-8b24-1a1a66c515de
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/creating-stored-procedures-and-user-defined-functions-with-managed-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 653c8303691de28b7619c30e773473ffb37f2a61
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="creating-stored-procedures-and-user-defined-functions-with-managed-code-c"></a>저장 프로시저와 관리 코드 (C#)와 사용자 정의 함수 만들기
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_75_CS.zip) 또는 [PDF 다운로드](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/datatutorial75cs1.pdf)

> Microsoft SQL Server 2005 개발자가 관리 되는 코드를 통해 데이터베이스 개체를 만들 수 있도록.NET 공용 언어 런타임 통합 합니다. 이 자습서에서는 관리 되는 저장된 프로시저를 만드는 방법을 보여 줍니다 및 Visual Basic 또는 C# 코드와 사용자 정의 함수를 관리 합니다. 또한 이러한 버전의 Visual Studio 이러한 관리 되는 데이터베이스 개체를 디버깅할 수 있도록 방법을 알아봅니다.


## <a name="introduction"></a>소개

Microsoft SQL Server 2005 s와 같은 데이터베이스 사용은 [Transact-Structured 쿼리 언어 (T-SQL)](http://en.wikipedia.org/wiki/Transact-SQL) 삽입, 수정 및 데이터 검색에 대 한 합니다. 대부분의 데이터베이스 시스템에는 일련의 다시 사용할 수 있는 단일 단위로 실행 될 수 있는 SQL 문 그룹화 하기 위한 구문을 포함 됩니다. 저장된 프로시저는 한 가지 예입니다. 다른 스냅숏이 *사용자 정의 함수*(Udf) 9 단계에서에서 더 자세히 검사 하는 구문입니다.

본질적으로 데이터 집합으로 작업 하기 위한 SQL 설계 되었습니다. `SELECT`, `UPDATE`, 및 `DELETE` 문을 기본적으로 해당 테이블의 모든 레코드에 적용 되 고 뿐 해당 `WHERE` 절. 아직 설계 하 고 스칼라 데이터를 조작 하기 위해 한 번에 하나의 레코드를 사용 하기 위한 언어 기능이 많이 있습니다. [`CURSOR`s](http://www.sqlteam.com/item.asp?ItemID=553) 레코드 집합을 통해 한 번에 하나씩 반복 될 수 있습니다. 문자열 조작 함수 같은 `LEFT`, `CHARINDEX`, 및 `PATINDEX` 스칼라 데이터와 함께 작동 합니다. SQL에도 같은 제어 흐름 문의 `IF` 및 `WHILE`합니다.

Microsoft SQL Server 2005 이전 저장된 프로시저 및 Udf 수로 정의 될 T-SQL 문 모음입니다. 그러나 SQL Server 2005와의 통합을 제공 하도록 디자인 된는 [공용 언어 런타임 (CLR)](https://msdn.microsoft.com/en-us/netframework/aa497266.aspx), 하는 모든.NET 어셈블리에서 사용 하는 런타임입니다. 따라서 저장된 프로시저 및 Udf는 SQL Server 2005 데이터베이스에 만들 수 있습니다 관리 코드를 사용 하 여 합니다. 즉, 저장된 프로시저 또는 UDF를 C# 클래스의 메서드로 만들 수 있습니다. 이렇게 하면 이러한 저장된 프로시저 및 사용자 지정 클래스와.NET Framework의 기능을 활용 하는 Udf 수 있습니다.

이 자습서에 살펴보겠습니다 관리 되는 만드는 방법을 저장 프로시저 및 사용자 정의 함수 및 Northwind 데이터베이스에 통합 하는 방법. Let s가 시작 되었습니다.

> [!NOTE]
> 관리 되는 데이터베이스 개체에는 SQL 대응에 비해 몇 가지 이점을 제공 합니다. 언어 풍부 하 고 친숙 하 고 기존 코드와 논리를 다시 사용할 수 있는 가지 주요 이점이 있습니다. 하지만 관리 되는 데이터베이스 개체의 절차적 논리 없이 많은 관련 되지 않은 데이터 집합으로 작업할 때 효율성이 떨어지는 일 수 있습니다. 관리 되는 코드와 T-SQL을 사용 하 여의 장점에 보다 철저 한 논의 체크 아웃의 [장점의를 사용 하 여 관리 코드를 데이터베이스 개체를 만드는](https://msdn.microsoft.com/en-us/library/k2e1fb36(VS.80).aspx)합니다.


## <a name="step-1-moving-the-northwind-database-out-ofappdata"></a>1 단계: 부재 중 Northwind 데이터베이스를 이동합니다.`App_Data`

웹 응용 프로그램 s의 Microsoft SQL Server 2005 Express Edition 데이터베이스 파일 사용 지금까지 자습서의 모든 `App_Data` 폴더입니다. 데이터베이스에 배치할 `App_Data` 간체 배포 하 고 한 디렉터리 내에서 찾은 것 인터페이스와 자습서를 테스트 하려면 추가 구성 단계가 없는 필요한 모든 파일이으로 이러한 자습서를 실행 합니다.

그러나이 자습서에서는 let s Northwind 데이터베이스 이동 중 `App_Data` 명시적으로 SQL Server 2005 Express Edition 데이터베이스 인스턴스를 등록 합니다. 이 자습서의 데이터베이스에 대 한 단계를 수행할 수 있습니다 하는 동안는 `App_Data` 폴더를 다양 한 단계에서 수행 하는 보다 간단 하 게 명시적으로 SQL Server 2005 Express Edition 데이터베이스 인스턴스와 데이터베이스를 등록 합니다.

이 자습서에 대 한 다운로드에는 두 데이터베이스 파일- `NORTHWND.MDF` 및 `NORTHWND_log.LDF` 폴더에 배치 된- `DataFiles`합니다. 이 자습서의 사용자 지정 구현을 함께 따르는 경우 Visual Studio를 닫고 이동는 `NORTHWND.MDF` 및 `NORTHWND_log.LDF` s 웹 사이트에서 파일 `App_Data` 폴더 외부 웹 사이트에서 폴더입니다. 데이터베이스 파일을 다른 폴더로 이동 된 후 Northwind 데이터베이스는 SQL Server 2005 Express Edition 데이터베이스 인스턴스를 등록 해야 합니다. SQL Server Management Studio에서이 작업을 수행할 수 있습니다. 비-Express Edition의 SQL Server 2005 컴퓨터에 설치 되어 있는 경우 다음 가능성이 이미 Management Studio가 설치 되어 있습니다. 만 컴퓨터에 SQL Server 2005 Express Edition 설치 되어 다음 다운로드 하 고 설치 잠시 시간이 걸릴 경우 [Microsoft SQL Server Management Studio Express](https://www.microsoft.com/downloads/details.aspx?displaylang=en&amp;FamilyID=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796)합니다.

SQL Server Management Studio를 시작 합니다. 그림 1에서 볼 수 있듯이 Management Studio에 연결할 서버를 요청 하 여 시작 합니다. 서버 이름에 대 한 localhost\SQLExpress를 입력 하 고 인증 드롭 다운 목록에서 Windows 인증을 선택한 다음 연결을 클릭 합니다.


![적절 한 데이터베이스 인스턴스에 연결](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image1.png)

**그림 1**: 적절 한 데이터베이스 인스턴스에 연결


적 연결 되 면 개체 탐색기 창에는 데이터베이스, 보안 정보, 관리 옵션 및 등을 포함 하 여 SQL Server 2005 Express Edition 데이터베이스 인스턴스에 대 한 정보를 나열 됩니다.

Northwind 데이터베이스에 연결할 필요는 `DataFiles` 폴더 (또는 아무 곳에 나 있습니다 옮기지) SQL Server 2005 Express Edition 데이터베이스 인스턴스를 합니다. 데이터베이스 폴더 단추로 클릭 하 고 상황에 맞는 메뉴에서 연결 옵션을 선택 합니다. 이 데이터베이스 연결 대화 상자를 표시 합니다. 추가 단추 클릭, 드릴 다운 적절 한 `NORTHWND.MDF` 파일과 확인을 클릭 합니다. 이 시점에서 화면 그림 2 비슷해야 합니다.


[![적절 한 데이터베이스 인스턴스에 연결](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image3.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image2.png)

**그림 2**: 해당 데이터베이스 인스턴스에 연결 ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image4.png))


> [!NOTE]
> Management Studio를 통해 SQL Server 2005 Express Edition 인스턴스를 연결할 경우 데이터베이스 연결 대화 상자 내 문서와 같은 사용자 프로필 디렉터리 드릴 다운 하면 허용 되지 않습니다. 따라서 배치를 확인는 `NORTHWND.MDF` 및 `NORTHWND_log.LDF` 비 사용자 프로필 디렉터리의 파일입니다.


데이터베이스를 연결 하려면 확인 단추를 클릭 합니다. 데이터베이스 연결 대화 상자가 닫히고 개체 탐색기에서 이제 적시에 연결 된 데이터베이스를 나열 해야 합니다. Northwind 데이터베이스에 같은 이름이 될 확률이 `9FE54661B32FDD967F51D71D0D5145CC_LINE ARTICLES\DATATUTORIALS\VOLUME 3\CSHARP\73\ASPNET_DATA_TUTORIAL_75_CS\APP_DATA\NORTHWND.MDF`합니다. 데이터베이스를 마우스 오른쪽 단추로 클릭 하 고 이름 바꾸기를 선택 하 여 데이터베이스를 Northwind로 이름을 바꿉니다.


![Northwind 데이터베이스 이름을 바꾸려면](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image5.png)

**그림 3**: northwind 데이터베이스 이름을 바꾸려면


## <a name="step-2-creating-a-new-solution-and-sql-server-project-in-visual-studio"></a>2 단계: Visual Studio에서 새 솔루션 및 SQL Server 프로젝트 만들기

SQL Server 2005에서 관리 되는 저장된 프로시저 또는 Udf 만들 저장된 프로시저 및 UDF 논리 클래스의 C# 코드를 작성 하 합니다. 코드를 쓴 후이 클래스를 어셈블리로 컴파일할 해야 합니다 (한 `.dll` 파일), SQL Server 데이터베이스와 어셈블리를 등록 한 다음에 해당 하는 메서드를 가리키는 데이터베이스에서 저장된 프로시저 또는 UDF 개체를 만듭니다 어셈블리입니다. 다음이 단계 수 모두 수동으로 수행 합니다. 편집기 텍스트의 코드를 작성, C# 컴파일러를 사용 하 여 명령줄에서 컴파일할 수 우리 ([`csc.exe`](https://msdn.microsoft.com/en-us/library/ms379563(vs.80).aspx))를 사용 하 여 데이터베이스에 등록는 [ `CREATE ASSEMBLY` ](https://msdn.microsoft.com/en-us/library/ms189524.aspx) 명령 또는 관리 Studio, 저장된 프로시저 또는 UDF 개체 비슷한 방법으로 추가 합니다. 다행히 팀 시스템 및 Professional 버전의 Visual Studio는 이러한 작업을 자동화 하는 SQL Server 프로젝트 유형을 포함 합니다. 이 자습서에서 살펴보게 될 것을 통해 관리 되는 저장된 프로시저 및 UDF를 만드는 SQL Server 프로젝트 형식을 사용 하 여 합니다.

> [!NOTE]
> 표준 버전의 Visual Studio 또는 Visual Web Developer를 사용 하는 경우 수동 접근을 대신 사용 해야 합니다. 13 단계는 수동으로 이러한 단계를 수행 하기 위한 자세한 지침을 제공 합니다. 확인해부터 12까지이 단계는 사용 중인 Visual Studio의 어떤 버전에 관계 없이 적용 해야 하는 중요 한 SQL Server 구성 지침이 포함 되어 있으므로 13 단계를 읽기 전에 단계 2를 읽을 수 있습니다.


Visual Studio를 열어 시작 합니다. 파일 메뉴에서 새 프로젝트 대화 상자를 표시 하는 새 프로젝트를 선택 상자 (그림 4 참조). 데이터베이스 프로젝트 형식을 다운 드릴 하 여 다음 오른쪽에 나열 된 템플릿에서 새 SQL Server 프로젝트를 만들려면 선택 합니다. 이 프로젝트의 이름을 하기로 `ManagedDatabaseConstructs` 라는 솔루션 내에 배치 하 고 `Tutorial75`합니다.


[![새 SQL Server 프로젝트 만들기](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image7.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image6.png)

**그림 4**: 새 SQL Server 프로젝트를 만듭니다 ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image8.png))


솔루션 및 SQL Server 프로젝트를 만드는 새 프로젝트 대화 상자에서 확인 단추를 클릭 합니다.

SQL Server 프로젝트는 특정 데이터베이스에 연결 됩니다. 따라서 새 SQL Server 프로젝트를 만든 후 즉시 라는 요청이 정보를 지정 합니다. 그림 5는 SQL Server 2005 Express Edition 데이터베이스 인스턴스의 1 단계에서 다시 등록에서는 Northwind 데이터베이스를 가리키도록 작성 되는 새 데이터베이스 참조 대화 상자를 보여 줍니다.


![Northwind 데이터베이스와 연관 된 SQL Server 프로젝트](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image9.png)

**그림 5**: Northwind 데이터베이스와 연관 된 SQL Server 프로젝트


관리 되는 저장된 프로시저 및 Udf이이 프로젝트 내에서 만들겠습니다를 디버깅 하려면 SQL/CLR 디버깅 연결에 대 한 지원을 사용 하도록 설정 해야 합니다. (에서 같이 그림 5)는 SQL Server 프로젝트를 새 데이터베이스와 연결 될 때마다, Visual Studio 요청 우리는 연결에 SQL/CLR 디버깅을 사용 하도록 설정 하려면 원하는 (그림 6 참조). 예를 클릭 합니다.


![SQL/CLR 디버깅을 사용 하도록 설정](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image10.png)

**그림 6**: SQL/CLR 디버깅을 사용 하도록 설정


이 시점에서 새 SQL Server 프로젝트를 솔루션에 추가 되었습니다. 라는 폴더를 포함 `Test Scripts` 라는 파일로 `Test.sql`, 프로젝트에서 만든 관리 되는 데이터베이스 개체 디버깅에 사용 되는 합니다. 12 단계에서에서 디버깅 살펴보겠습니다.

이 프로젝트에 새 관리 되는 저장된 프로시저 및 Udf 이제 추가할 수 있습니다 하지만 게 수행 하기 전에 먼저 포함 되어 기존 웹 응용 프로그램 솔루션에. 파일 메뉴에서 추가 옵션을 선택 하 고 기존 웹 사이트를 선택 합니다. 적절 한 웹 사이트 폴더를 찾아 확인을 클릭 합니다. 그림 7에서 볼 수 있듯이 두 개의 프로젝트를 포함 하도록 솔루션 업데이트 됩니다: 웹 사이트 및 `ManagedDatabaseConstructs` SQL Server 프로젝트.


![솔루션 탐색기에는 이제 두 개의 프로젝트가 포함](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image11.png)

**그림 7**: 솔루션 탐색기에는 이제 두 개의 프로젝트가 포함


`NORTHWNDConnectionString` 값 `Web.config` 현재 참조는 `NORTHWND.MDF` 파일에 `App_Data` 폴더입니다. 이 데이터베이스를 제거 했으므로 `App_Data` 및 명시적으로 등록 하 고 SQL Server 2005 Express Edition 데이터베이스 인스턴스에서 업데이트까지 해야는 `NORTHWNDConnectionString` 값입니다. 열기는 `Web.config` 변경 및 웹 사이트에서 파일의 `NORTHWNDConnectionString` 연결 문자열을 읽을 수 있도록 값: `Data Source=localhost\SQLExpress;Initial Catalog=Northwind;Integrated Security=True`합니다. 이렇게 변경 하면 `<connectionStrings>` 섹션 `Web.config` 다음과 비슷해야 합니다.


[!code-xml[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample1.xml)]

> [!NOTE]
> 에 설명 된 대로 [이전 자습서](debugging-stored-procedures-cs.md)클라이언트 응용 프로그램에서 SQL Server 개체를 디버깅할 때, ASP.NET 웹 사이트와 같은 연결 풀링을 사용 하지 않도록 설정 해야 합니다. 위에 표시 된 연결 문자열은 연결 풀링 비활성화 ( `Pooling=false` ). ASP.NET 웹 사이트에서 관리 되는 저장된 프로시저 및 Udf를 디버깅 하지 않으려는 경우 연결 풀링이 사용 하도록 설정 합니다.


## <a name="step-3-creating-a-managed-stored-procedure"></a>3 단계: 관리 되는 만드는 저장 프로시저

Northwind 데이터베이스에 관리 되는 저장된 프로시저를 추가 하려면 먼저 SQL Server 프로젝트에서 메서드로 저장된 프로시저를 생성 해야 합니다. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭는 `ManagedDatabaseConstructs` 프로젝트 이름 및 새 항목을 추가 하려면 선택 합니다. 이 프로젝트에 추가할 수 있는 관리 되는 데이터베이스 개체 유형을 나열 하는 새 항목 추가 대화 상자를 표시 됩니다. 그림 8에서 볼 수 있듯이 여기에 저장된 프로시저 및 사용자 정의 함수 등입니다.

모든 사용이 중단 된 제품을 반환 하는 저장된 프로시저를 추가 하 여 시작 s를 사용 합니다. 새 저장된 프로시저 파일 이름을 `GetDiscontinuedProducts.cs`합니다.


[![GetDiscontinuedProducts.cs 새 저장된 프로시저를 추가 합니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image13.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image12.png)

**그림 8**: 라는 추가 하는 새 저장 프로시저 `GetDiscontinuedProducts.cs` ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image14.png))


다음 내용을 사용 하 여 새로운 C# 클래스 파일이 만들어집니다.


[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample2.cs)]

저장된 프로시저는로 구현 하는 `static` 내에서 메서드는 `partial` 라는 클래스 파일 `StoredProcedures`합니다. 또한는 `GetDiscontinuedProducts` 로 데코레이팅된 메서드는 `SqlProcedure attribute`, 저장 프로시저로 메서드를 표시 하는입니다.

다음 코드에서는 `SqlCommand` 개체 및 집합 해당 `CommandText` 에 `SELECT` 의 모든 열에서 반환 하는 쿼리는 `Products` 인 제품에 대 한 테이블 `Discontinued` 1 필드입니다. 다음 명령을 실행 하 고 클라이언트 응용 프로그램에 다시 결과 보냅니다. 이 코드를 추가 하는 `GetDiscontinuedProducts` 메서드.


[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample3.cs)]

모든 관리 되는 데이터베이스 개체에 대 한 액세스는는 [ `SqlContext` 개체](https://msdn.microsoft.com/en-us/library/ms131108.aspx) 호출자의 컨텍스트를 나타내는입니다. `SqlContext` 에 액세스할 수는 [ `SqlPipe` 개체](https://msdn.microsoft.com/en-us/library/microsoft.sqlserver.server.sqlpipe.aspx) 를 통해 해당 [ `Pipe` 속성](https://msdn.microsoft.com/en-us/library/microsoft.sqlserver.server.sqlcontext.pipe.aspx)합니다. 이 `SqlPipe` 개체는 SQL Server 데이터베이스 및 호출 응용 프로그램 간에 정보를 ferry 하는 데 사용 됩니다. 이름에서 알 수 있듯이 [ `ExecuteAndSend` 메서드](https://msdn.microsoft.com/en-us/library/microsoft.sqlserver.server.sqlpipe.executeandsend.aspx) 는 전달 기능을 실행 `SqlCommand` 개체와 클라이언트 응용 프로그램에 결과 다시 보냅니다.

> [!NOTE]
> 관리 되는 데이터베이스 개체는 저장된 프로시저 및 집합 기반 논리 보다는 절차적 논리를 사용 하는 Udf에 가장 적합 합니다. 절차적 논리 없이-행 단위에서 작업 데이터 집합으로 스칼라 데이터 작업을 작업이 포함 됩니다. 그러나 `GetDiscontinuedProducts` 방금 만든, 방법은 절차적 논리 없이 없습니다. 따라서 그 구현 하는 것이 가장 좋습니다 T-SQL 저장 프로시저입니다. 저장된 프로시저를 관리 하는 관리 되는 저장된 프로시저를 만들고 배포 하는 데 필요한 단계를 설명 하기 위해 구현 됩니다.


## <a name="step-4-deploying-the-managed-stored-procedure"></a>4 단계: 배포 관리 되는 저장 프로시저

전체이 코드를 통해 Northwind 데이터베이스에 배포할 준비가 됩니다. SQL Server 프로젝트를 배포는 코드를 어셈블리로 컴파일하, 데이터베이스에 어셈블리를 등록 하 고 어셈블리의 적절 한 방법에 연결 하는 데이터베이스에서 해당 개체를 만듭니다. 배포 옵션으로 수행 하는 작업의 정확한 집합은 보다 정확 하 게 13 단계에서에서 명시 됩니다. 마우스 오른쪽 단추로 클릭는 `ManagedDatabaseConstructs` 프로젝트 솔루션 탐색기에서 이름 및 배포 옵션을 선택 합니다. 그러나 배포는 다음 오류와 함께 실패: '외부' 근처의 구문이 잘못 되었습니다. 이 기능을 사용 하려면 더 높은 값으로 현재 데이터베이스의 호환성 수준을 설정 해야 합니다. 참조 된 저장된 프로시저에 대 한 도움말 `sp_dbcmptlevel`합니다.

이 오류 메시지에는 Northwind 데이터베이스에 어셈블리를 등록 하려고 할 때 발생 합니다. 어셈블리에는 SQL Server 2005 데이터베이스를 등록 하기 위해 데이터베이스의 호환성 수준이 90으로 설정 되어야 합니다. 기본적으로 새 SQL Server 2005 데이터베이스 호환성 수준이 90 적용 합니다. 그러나 Microsoft SQL Server 2000을 사용 하 여 만든 데이터베이스의 기본 호환성 수준을 80의 경우. Northwind 데이터베이스를 처음에 Microsoft SQL Server 2000 데이터베이스를 이후의 호환성 수준이 현재 80으로 설정 되어 하며 따라서 관리 되는 데이터베이스 개체를 등록 하기 위해 90로 늘려야 합니다.

데이터베이스의 호환성 수준을 업데이트 하려면 Management Studio에서 새 쿼리 창을 열고을 입력 합니다.


[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample4.sql)]

위의 쿼리를 실행 하려면 도구 모음에 있는 Execute 아이콘을 클릭 합니다.


[![Northwind 데이터베이스의 호환성 수준을 업데이트합니다](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image16.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image15.png)

**그림 9**: Northwind 데이터베이스 호환성 수준을 s 업데이트 ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image17.png))


호환성 수준이 업데이트 한 후 SQL Server 프로젝트를 다시 배포 합니다. 이 이번 배포 오류 없이 완료 해야 합니다.

SQL Server Management Studio로 돌아가서, 개체 탐색기에서 Northwind 데이터베이스를 마우스 오른쪽 단추로 클릭 하 고 새로 고침을 선택 합니다. 그런 다음 프로그래밍 기능 폴더 드릴 다운 하 고 어셈블리 폴더를 확장 합니다. Northwind 데이터베이스에 의해 생성 된 어셈블리를 이제 포함 그림 10과 같이 `ManagedDatabaseConstructs` 프로젝트.


![ManagedDatabaseConstructs 어셈블리는 이제 Northwind 데이터베이스에 등록](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image18.png)

**그림 10**:는 `ManagedDatabaseConstructs` 어셈블리는 이제 Northwind 데이터베이스에 등록


또한 저장 프로시저 폴더를 확장 합니다. 저장된 프로시저 이름이 표시 됩니다 있습니다 `GetDiscontinuedProducts`합니다. 이 저장된 프로시저를 가리키 및 배포 프로세스에 의해 만들어진는 `GetDiscontinuedProducts` 에서 메서드는 `ManagedDatabaseConstructs` 어셈블리입니다. 경우는 `GetDiscontinuedProducts` 저장된 프로시저가 실행 되 면, 차례로 실행 하는 `GetDiscontinuedProducts` 메서드. 이 관리 되는 저장된 프로시저는 Management Studio를 통해 편집할 수 없습니다 (따라서 저장된 프로시저 이름 옆에 있는 자물쇠 아이콘).


![GetDiscontinuedProducts 저장 프로시저는 저장 프로시저 폴더에 나열 된](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image19.png)

**그림 11**:는 `GetDiscontinuedProducts` 저장 프로시저는 저장 프로시저 폴더에 나열 된


관리 되는 저장된 프로시저를 호출할 수 있습니다를 극복 하 게 해야 또 하나의 장애물은 여전히: 관리 코드의 실행을 방지 하기 위해 구성 된 데이터베이스입니다. 새 쿼리 창을 열고 실행 하 여이 확인은 `GetDiscontinuedProducts` 저장 프로시저입니다. 다음과 같은 오류 메시지가 표시 됩니다:.NET Framework에서 사용자 코드의 실행을 사용할 수 없습니다. Clr enabled 구성 옵션을 사용 하도록 설정 합니다.

Northwind 데이터베이스의 구성 정보를 검사할 입력 하 고 명령을 실행 하려면 `exec sp_configure` 쿼리 창에서. 0으로 설정 하는 활성화 clr 현재 설정 되어 있는지 표시 합니다.


[![Clr 사용 되도록 설정 되어 현재 설정 0](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image21.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image20.png)

**그림 12**: clr 활성화 되도록 설정 되어 현재 설정 0 ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image22.png))


그림 12에서 각 구성 설정에 나열 된 4 개의 값: 최소값 및 최 댓 값 구성 및 실행된 값입니다. 사용 하도록 설정 하는 clr 설정에 대 한 구성 값을 업데이트 하려면 다음 명령을 실행 합니다.


[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample5.sql)]

다시 실행 하는 경우는 `exec sp_configure` 위의 문은 사용 하도록 설정 하는 clr 설정 s config 값 1로 업데이트 되도록 하지만 실행된 값을 0으로 여전히 설정 되어 있는지 표시 됩니다. 이 구성 변경 내용을 적용 하려면을 실행 해야는 [ `RECONFIGURE` 명령](https://msdn.microsoft.com/en-us/library/ms176069.aspx), 현재 구성 값으로 실행된 값이 설정 됩니다입니다. 단순히 입력 `RECONFIGURE` 쿼리 창에서 도구 모음에서 실행 아이콘을 클릭 합니다. 실행 하는 경우 `exec sp_configure` 이제 사용 하도록 설정 하는 clr 설정의 구성에 대 한 1의 값이 표시 하 고 값을 실행 해야 합니다.

사용 하도록 설정 하는 clr 구성이 완료 하는 관리 되는 실행할 준비가 `GetDiscontinuedProducts` 저장 프로시저입니다. 쿼리 창에서를 입력 하 고 다음 명령을 실행 `exec` `GetDiscontinuedProducts`합니다. 관리 되는 해당 코드가 사용 하면 저장된 프로시저를 호출 하는 `GetDiscontinuedProducts` 메서드를 실행 합니다. 이 코드를 발급 한 `SELECT` 제공이 중단 된이 인스턴스의 SQL Server Management Studio는 호출 응용 프로그램에이 데이터를 반환 하는 모든 제품을 반환 하도록 쿼리 합니다. Management Studio는 이러한 결과 수신 하 고 결과 창에 표시 합니다.


[![모든 저장된 프로시저 반환 GetDiscontinuedProducts 중단 제품](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image24.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image23.png)

**그림 13**:는 `GetDiscontinuedProducts` 저장 프로시저 반환 모든 지원 되지 않는 제품 ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image25.png))


## <a name="step-5-creating-managed-stored-procedures-that-accept-input-parameters"></a>5 단계: 관리 되는 만들기는 저장 프로시저 입력된 매개 변수를 허용

대부분의 쿼리 및 이러한 자습서 전체에서 만든 저장된 프로시저 사용 *매개 변수*합니다. 예를 들어는 [새 저장 프로시저 만들기 형식의 DataSet s Tableadapter에 대 한](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md) 라는 저장된 프로시저를 만들었습니다 자습서 `GetProductsByCategoryID` 라는 입력된 매개 변수를 허용 하는 `@CategoryID`합니다. 저장된 프로시저에는 다음 모든 제품을 반환 된 `CategoryID` 필드에 제공 된 값과 일치 `@CategoryID` 매개 변수입니다.

입력된 매개 변수를 허용 하는 관리 되는 저장된 프로시저를 만들려면 s 메서드 정의의 해당 매개 변수를 지정 하면 됩니다. 이 설명 하기 let s 추가 하는 다른 관리 되는 저장된 프로시저는 `ManagedDatabaseConstructs` 라는 프로젝트 `GetProductsWithPriceLessThan`합니다. 관리 되는이 저장된 프로시저는 가격을 지정 하는 입력된 매개 변수를 수락 하 고 모든 제품을 반환 합니다 인 `UnitPrice` 필드가 매개 변수의 값 보다 작으면 메시지를 표시 합니다.

프로젝트에 새 저장된 프로시저를 추가 하려면 마우스 오른쪽 단추로 클릭는 `ManagedDatabaseConstructs` 프로젝트 이름 및 새 저장된 프로시저를 추가 하려면 선택 합니다. 파일 이름을 `GetProductsWithPriceLessThan.cs`로 지정합니다. 3 단계에서에서 설명한 것 처럼 새 C# 클래스 파일이 라는 메서드가 있는 만들어집니다 `GetProductsWithPriceLessThan` 내에 배치 된 `partial` 클래스 `StoredProcedures`합니다.

업데이트는 `GetProductsWithPriceLessThan` s 메서드 정의 허용 하도록는 [ `SqlMoney` ](https://msdn.microsoft.com/en-us/library/system.data.sqltypes.sqlmoney.aspx) 라는 입력된 매개 변수 `price` 고 실행 하 고 쿼리 결과 반환 코드를 작성 합니다.


[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample6.cs)]

`GetProductsWithPriceLessThan` 정 및 코드의 유사한 s 메서드 정 및 코드는 `GetDiscontinuedProducts` 3 단계에서에서 만든 메서드. 유일한 차이점은 각 하는 `GetProductsWithPriceLessThan` 메서드에 입력된 매개 변수로 (`price`), `SqlCommand` s 쿼리 매개 변수를 포함 (`@MaxPrice`)에 매개 변수가 추가 됩니다는 `SqlCommand` s `Parameters` 컬렉션은 및 값이 할당은 `price` 변수입니다.

이 코드를 추가한 후 SQL Server 프로젝트를 다시 배포 합니다. 다음으로, SQL Server Management Studio로 돌아가서 하 고 저장 프로시저 폴더를 새로 고칩니다. 새 항목이 표시 되어야 `GetProductsWithPriceLessThan`합니다. 쿼리 창에서를 입력 하 고 다음 명령을 실행 `exec GetProductsWithPriceLessThan 25`이며 그림 14 볼 수 있듯이 달러에서 25 미만의 모든 제품 목록 됩니다.


[![제품에서 25 달러 표시 됩니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image27.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image26.png)

**그림 14**: 제품에서 25 달러 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image28.png))


## <a name="step-6-calling-the-managed-stored-procedure-from-the-data-access-layer"></a>6 단계: 데이터 액세스 계층에서 관리 되는 저장된 프로시저를 호출합니다.

추가한이 시점에서 `GetDiscontinuedProducts` 및 `GetProductsWithPriceLessThan` 저장된 프로시저를 관리 하는 `ManagedDatabaseConstructs` 프로젝트 및 Northwind SQL Server 데이터베이스를 등록 한 합니다. 또한 SQL Server Management Studio에서 이러한 관리 되는 저장된 프로시저를 호출 했습니다 (13 및 14의 그림 참조). 이 사용 하 여 응용 프로그램의 ASP.NET에 대 한 순서 대로 저장된 프로시저를 관리, 이때 데이터 액세스 및 아키텍처에서 비즈니스 논리 계층에 추가 해야 합니다. 이 단계에서는 두 개의 새 메서드를 추가 합니다는 `ProductsTableAdapter` 에 `NorthwindWithSprocs` 형식화 된 데이터 집합에서 처음으로 만든는 [새 저장 프로시저 만들기 형식의 DataSet s Tableadapter에 대 한](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md) 자습서입니다. 7 단계에서에서 BLL에 해당 메서드를 추가 합니다.

열기는 `NorthwindWithSprocs` Visual Studio 및 시작 하는 새로운 방법도 추가 하 여 형식화 된 데이터 집합은 `ProductsTableAdapter` 라는 `GetDiscontinuedProducts`합니다. TableAdapter에 새 메서드를 추가 하려면 디자이너에서 TableAdapter의 이름을 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 추가 쿼리 옵션을 선택 합니다.

> [!NOTE]
> Northwind 데이터베이스를 이동 하므로 `App_Data` SQL Server 2005 Express Edition 데이터베이스 인스턴스에 폴더를 반드시 Web.config에서 해당 연결 문자열이 변경 내용을 반영 하도록 업데이트 되 합니다. 2 단계에서에서에서 설명한 업데이트는 `NORTHWNDConnectionString` 값 `Web.config`합니다. 이 업데이트를 더욱 잊은 경우 쿼리를 추가 하려면 못했습니다 오류 메시지가 표시 됩니다. 연결을 찾을 수 없습니다 `NORTHWNDConnectionString` 개체에 대 한 `Web.config` TableAdapter에 새 메서드를 추가 하려고 할 때 대화 상자에서. 이 오류를 해결 하려면 확인을 클릭 하 고 다음으로 이동 `Web.config` 하 고 업데이트는 `NORTHWNDConnectionString` 2 단계에서에서 설명 했 듯이 값입니다. 그런 다음 다시 TableAdapter에 메서드를 추가 해 보십시오. 이 시간 오류 없이 작동 해야 합니다.


새 메서드 추가 지난 자습서에서 여러 번 사용 하는 TableAdapter 쿼리 구성 마법사를 시작 합니다. 첫 번째 단계에서는 TableAdapter는 데이터베이스에 액세스 하는 방법을 지정 하려면: 기존 또는 새 저장된 프로시저를 통해 또는 임시 SQL 문을 통해 합니다. 에서는 이미 만들고 등록 한 후의 `GetDiscontinuedProducts` 프로시저 옵션을 저장 하 고 다음 적중 사용 하 여 기존 데이터베이스와 관리 되는 저장된 프로시저를 선택 합니다.


[![기존 저장된 프로시저 옵션 사용](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image30.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image29.png)

**그림 15**: 저장 된 프로시저 옵션을 사용 하 여 기존 선택 ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image31.png))


다음 화면에서 메서드를 호출 합니다 저장된 프로시저에 대 한 라는 메시지가 나타납니다. 선택 된 `GetDiscontinuedProducts` 드롭 다운 목록에서 저장된 프로시저를 관리 하 고 다음에 도달 합니다.


[![관리 되는 저장된 프로시저는 GetDiscontinuedProducts 선택](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image33.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image32.png)

**그림 16**: 선택 된 `GetDiscontinuedProducts` 관리 되는 저장 프로시저 ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image34.png))


그런 다음 저장된 프로시저가 행, 단일 값 또는 아무 것도 반환 하는지 여부를 지정 하 라는 요청입니다. 이후 `GetDiscontinuedProducts` 집합을 반환 지원 되지 않는 제품 행의 첫 번째 옵션 (테이블 형식 데이터)을 선택 하 고 다음을 클릭 합니다.


[![테이블 형식 데이터 옵션을 선택 합니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image36.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image35.png)

**그림 17**: 테이블 형식 데이터 옵션을 선택 ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image37.png))


마법사의 마지막 화면에 사용 되는 데이터 액세스 패턴 및 결과 메서드의 이름을 지정할 수 있습니다. 확인 확인란 및 이름을 모두 메서드 둡니다 `FillByDiscontinued` 및 `GetDiscontinuedProducts`합니다. 마법사를 완료 하려면 마침을 클릭 합니다.


[![메서드 FillByDiscontinued 이름과 GetDiscontinuedProducts](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image39.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image38.png)

**그림 18**: 메서드 이름을 `FillByDiscontinued` 및 `GetDiscontinuedProducts` ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image40.png))


라는 메서드를 만들려면 이러한 단계를 반복 `FillByPriceLessThan` 및 `GetProductsWithPriceLessThan` 에 `ProductsTableAdapter` 에 대 한는 `GetProductsWithPriceLessThan` 관리 되는 저장된 프로시저입니다.

그림 19 메서드를 추가한 후 데이터 집합 디자이너의 스크린샷이 나와 `ProductsTableAdapter` 에 대 한는 `GetDiscontinuedProducts` 및 `GetProductsWithPriceLessThan` 저장된 프로시저를 관리 합니다.


[![이 단계에서 추가한 새 메서드를 포함 하는 ProductsTableAdapter](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image42.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image41.png)

**그림 19**:는 `ProductsTableAdapter` 이 단계에서는 새 메서드가 추가 포함 ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image43.png))


## <a name="step-7-adding-corresponding-methods-to-the-business-logic-layer"></a>비즈니스 논리 계층에 해당 메서드를 추가 하는 7 단계:

4-5 단계에서 추가한 관리 되는 저장된 프로시저를 호출 하기 위한 메서드를 포함 하도록 데이터 액세스 계층을 업데이트 했으므로 해당 메서드는 비즈니스 논리 계층에 추가 해야 합니다. 다음 두 가지 메서드를 추가 `ProductsBLLWithSprocs` 클래스:


[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample7.cs)]

두 방법 모두에서 단순히 해당 DAL 메서드를 호출 하 고 반환 된 `ProductsDataTable` 인스턴스. `DataObjectMethodAttribute` 각 메서드 위에 태그 하면 이러한 메서드를 ObjectDataSource의 데이터 소스 구성 마법사의 선택 탭의 드롭다운 목록에 포함 되어야 합니다.

## <a name="step-8-invoking-the-managed-stored-procedures-from-the-presentation-layer"></a>8 단계: 관리 되는 호출에서 저장 프로시저는 프레젠테이션 계층

비즈니스 논리 및 데이터 액세스 계층으로 호출에 대 한 지원을 포함 하도록 확장는 `GetDiscontinuedProducts` 및 `GetProductsWithPriceLessThan` 저장된 프로시저를 관리 되는 이러한 이제 표시 수는 ASP.NET 페이지를 통해 프로시저 결과 저장 합니다.

열기는 `ManagedFunctionsAndSprocs.aspx` 페이지에 `AdvancedDAL` 폴더 및 도구 상자에서는 GridView 디자이너로 끌어 옵니다. GridView s 설정 `ID` 속성을 `DiscontinuedProducts` 및 스마트 태그를 바인딩할 라는 새 ObjectDataSource `DiscontinuedProductsDataSource`합니다. 구성에서 해당 데이터를 가져오도록 ObjectDataSource는 `ProductsBLLWithSprocs` s 클래스 `GetDiscontinuedProducts` 메서드.


[![ObjectDataSource ProductsBLLWithSprocs 클래스를 사용 하도록 구성](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image45.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image44.png)

**그림 20**: 구성에 사용 하 여 ObjectDataSource는 `ProductsBLLWithSprocs` 클래스 ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image46.png))


[![GetDiscontinuedProducts 메서드 선택 탭의 드롭다운 목록에서 선택](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image48.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image47.png)

**그림 21**: 선택 된 `GetDiscontinuedProducts` SELECT 탭에서 드롭 다운 목록에서 메서드 ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image49.png))


이 표를 표시 제품 정보에 사용 되므로 UPDATE, INSERT에서에서 드롭 다운 목록을 설정 하 고 각 탭 (없음)을 삭제 하 고 마침을 클릭.

마법사를 완료 되 면 Visual Studio는 자동으로 BoundField 또는 추가 CheckBoxField에서 각 데이터 필드에 대 한는 `ProductsDataTable`합니다. 이 필드를 제외 하 고 제거 하 `ProductName` 및 `Discontinued`입니다 프로그램 GridView 가리키고 ObjectDataSource s 선언 태그는 다음과 같아야 합니다.:


[!code-aspx[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample8.aspx)]

브라우저를 통해이 페이지를 보려면 잠시 시간. 해당 페이지를 방문 하는 경우, ObjectDataSource 호출은 `ProductsBLLWithSprocs` s 클래스 `GetDiscontinuedProducts` 메서드. 7 단계에서에서 설명한 것 처럼이 메서드 호출 DAL s `ProductsDataTable` s 클래스 `GetDiscontinuedProducts` 메서드를 호출 하는 `GetDiscontinuedProducts` 저장 프로시저입니다. 이 저장된 프로시저 이며 관리 되는 저장 프로시저는 지원 되지 않는 제품을 반환 합니다. 3 단계에서에서 만든 코드를 실행 합니다.

으로 관리 되는 저장된 프로시저에 의해 반환 된 결과 패키지 됩니다는 `ProductsDataTable` dal GridView에 바인딩된 및 표시 되는 프레젠테이션 계층으로 되돌립니다 BLL에 다음 반환 합니다. 예상 대로 표에 사용이 중단 된 해당 제품을 나열 합니다.


[![지원 되지 않는 제품 나와](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image51.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image50.png)

**그림 22**: The 단종 된 제품 나열 됩니다 ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image52.png))


자세한 연습에 대 한 페이지에 텍스트 상자와 다른 GridView를 추가 합니다. 호출 하 여 텍스트 상자에 입력 한 크기 보다 작은 제품을 표시 하는이 GridView가는 `ProductsBLLWithSprocs` s 클래스 `GetProductsWithPriceLessThan` 메서드.

## <a name="step-9-creating-and-calling-t-sql-udfs"></a>9 단계: 만들기 및 T-SQL Udf를 호출 합니다.

사용자 정의 함수 또는 Udf 데이터베이스 개체를 유사 하 게 모방할 프로그래밍 언어의 함수의 의미 체계 간주 됩니다. C#의 함수 처럼 Udf 가변 개수의 입력된 매개 변수를 포함 하 고 특정 형식의 값을 반환할 수 있습니다. UDF는 스칼라 데이터-string, integer, 및 등-또는 표 형식 데이터를 반환할 수 있습니다. 스칼라 데이터 형식을 반환 하는 UDF로 시작 되는 udf 두 유형 모두에 빠르게 확인 하는 s를 사용 합니다.

다음 UDF는 특정 제품에 대 한 인벤토리의 예상된 값을 계산합니다. 이 작업을 수행 하 여 세 개의 입력된 매개 변수-에 `UnitPrice`, `UnitsInStock`, 및 `Discontinued` -특정 제품에 대 한 값 형식의 값을 반환 하 `money`합니다. 재고의 예상된 값을 곱하여 계산는 `UnitPrice` 여는 `UnitsInStock`합니다. 이 값은 지원 되지 않는 항목에 대 한 절반이 됩니다.


[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample9.sql)]

데이터베이스에이 UDF 추가한 다음에 프로그래밍 기능 폴더 다음 함수와 다음 스칼라 반환 함수를 확장 하 여 Management Studio를 통해 찾을 수 있습니다. 사용할 수는 `SELECT` 같이 쿼리:


[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample10.sql)]

추가 했 고 `udf_ComputeInventoryValue` UDF를 Northwind 데이터베이스입니다. 그림 23 위의 출력을 보여 줍니다. `SELECT` Management Studio를 통해 볼 때을 쿼리 합니다. 또한 참고가 UDF은 개체 탐색기에서 스칼라 값 함수 폴더 아래에 나열 됩니다.


[![각 제품 재고 값 s 나열 됩니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image54.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image53.png)

**그림 23**: 재고 값 나열 된 각 제품 s ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image55.png))


Udf는 테이블 형식 데이터를 반환할 수도 있습니다. 예를 들어 특정 범주에 속하는 제품을 반환 하는 UDF를 만들 수 있습니다.


[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample11.sql)]

`udf_GetProductsByCategoryID` UDF 허용는 `@CategoryID` 입력된 매개 변수 및 반환 결과 지정 된 `SELECT` 쿼리 합니다. 이 UDF를 만든 후에서 참조할 수 있습니다는 `FROM` (또는 `JOIN`) 절을 `SELECT` 쿼리 합니다. 다음 예제에서는 반환 된 `ProductID`, `ProductName`, 및 `CategoryID` 각 여 음료에 대 한 값.


[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample12.sql)]

추가 했 고 `udf_GetProductsByCategoryID` UDF를 Northwind 데이터베이스입니다. 그림 24 위의 출력을 보여 줍니다. `SELECT` Management Studio를 통해 볼 때을 쿼리 합니다. 개체 탐색기의 테이블 값 함수 폴더에서 테이블 형식 데이터를 반환 하는 Udf는 찾을 수 있습니다.


[![Each 음료에 대 한 ProductID, ProductName, 및 CategoryID 같습니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image57.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image56.png)

**그림 24**:는 `ProductID`, `ProductName`, 및 `CategoryID` Each 음료에 대해 나열 된 ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image58.png))


> [!NOTE]
> 체크 아웃 만들고 Udf를 사용 하 여에 대 한 자세한 내용은 [사용자 정의 함수를 소개](http://www.sqlteam.com/item.asp?ItemID=1955)합니다. 또한 체크 아웃 [장점과 Drawbacks of User-Defined 함수](http://www.samspublishing.com/articles/article.asp?p=31724&amp;rl=1)합니다.


## <a name="step-10-creating-a-managed-udf"></a>10 단계: 관리 되는 UDF 만들기

`udf_ComputeInventoryValue` 및 `udf_GetProductsByCategoryID` 위 예제에서 만든 Udf는 T-SQL 데이터베이스 개체입니다. SQL Server 2005에서는에 추가할 수 있는 관리 되는 Udf는 `ManagedDatabaseConstructs` 관리 되는 저장 프로시저에서 3 단계와 5 처럼 프로젝트입니다. 이 단계에 대 한 s 구현할 수는 `udf_ComputeInventoryValue` 관리 코드에서 UDF 합니다.

관리 되는 UDF를 추가 하는 `ManagedDatabaseConstructs` 프로젝트에서 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 새 항목을 추가 하려면 선택 합니다. 새 항목 추가 대화 상자에서 사용자 정의 템플릿을 선택 하 고 새 UDF 파일 이름을 `udf_ComputeInventoryValue_Managed.cs`합니다.


[![새 관리 되는 UDF ManagedDatabaseConstructs 프로젝트에 추가](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image60.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image59.png)

**그림 25**: 추가 하는 새 관리 되는 UDF는 `ManagedDatabaseConstructs` 프로젝트 ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image61.png))


사용자 정의 함수 템플릿은 만듭니다는 `partial` 라는 클래스 `UserDefinedFunctions` 클래스의 파일 이름과 동일한 이름이 메서드로 (`udf_ComputeInventoryValue_Managed`,이 인스턴스의). 이 메서드를 사용 하 여 데코 레이트 된 [ `SqlFunction` 특성](https://msdn.microsoft.com/en-us/library/microsoft.sqlserver.server.sqlfunctionattribute.aspx), 메서드는 관리 되는 UDF로 플래그입니다.


[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample13.cs)]

`udf_ComputeInventoryValue` 현재 메서드는 [ `SqlString` 개체](https://msdn.microsoft.com/en-us/library/system.data.sqltypes.sqlstring.aspx) 는 입력 매개 변수를 허용 하지 않습니다. 받아들이도록 세 개의 입력 매개 변수-메서드 정의 업데이트 해야 `UnitPrice`, `UnitsInStock`, 및 `Discontinued` -반환는 `SqlMoney` 개체입니다. 재고 현황 값을 계산 하기 위한 논리는 T-SQL와 동일 `udf_ComputeInventoryValue` UDF 합니다.


[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample14.cs)]

UDF의 메서드에 입력된 매개 변수는 해당 SQL 형식의: `SqlMoney` 에 대 한는 `UnitPrice` 필드 [ `SqlInt16` ](https://msdn.microsoft.com/en-us/library/system.data.sqltypes.sqlint16.aspx) 에 대 한 `UnitsInStock`, 및 [ `SqlBoolean` ](https://msdn.microsoft.com/en-us/library/system.data.sqltypes.sqlboolean.aspx) 에 대 한 `Discontinued`합니다. 이러한 데이터 형식에 정의 된 형식을 반영는 `Products` 테이블:는 `UnitPrice` 형식의 열이 `money`, `UnitsInStock` 형식의 열 `smallint`, 및 `Discontinued` 형식의 열 `bit`합니다.

만들어서 시작 하는 코드는 `SqlMoney` 명명 된 인스턴스 `inventoryValue` 할당 된 값이 0입니다. `Products` 데이터베이스에 대 한 테이블을 사용 하면 `NULL` 값에 `UnitsInPrice` 및 `UnitsInStock` 열입니다. 따라서 해야 첫 번째 확인이 값이 들어 `NULL` s를 통해 수행 하는 `SqlMoney` 개체 s [ `IsNull` 속성](https://msdn.microsoft.com/en-us/library/system.data.sqltypes.sqlmoney.isnull.aspx)합니다. 모두 `UnitPrice` 및 `UnitsInStock` 포함 비-`NULL` 에서는 계산 값는 `inventoryValue` 두 제품 되도록 합니다. 그런 다음 if `Discontinued` 가 true 이면 값 절반으로 줄일 했습니다.

> [!NOTE]
> `SqlMoney` 만 개체를 두 개 사용 하면 `SqlMoney` 함께 곱할 인스턴스. 허용 하지 않습니다는 `SqlMoney` 인스턴스를 리터럴 부동 소수점 숫자를 곱합니다. 따라서를 절반으로 줄일 `inventoryValue` 를 새 것을 곱하면 `SqlMoney` 값이 0.5 된 인스턴스.


## <a name="step-11-deploying-the-managed-udf"></a>11 단계: 관리 되는 UDF를 배포합니다.

이제 관리 되는 UDF를 만든, Northwind 데이터베이스에 배포할 준비가 됩니다. 4 단계에서에서 설명한 것 처럼 SQL Server 프로젝트에서 관리 되는 개체에서 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 배포 옵션을 선택 하 여 배포 됩니다.

프로젝트를 배포한 후에 SQL Server Management Studio로 반환 하 고 스칼라 반환 함수 폴더를 새로 고칩니다. 이제 두 개의 항목이 나타납니다.

- `dbo.udf_ComputeInventoryValue`-9 단계에서에서 만든 T-SQL UDF 및
- `dbo.udf ComputeInventoryValue_Managed`-관리 되는 UDF 방금 배포 된 10 단계에서에서 생성 합니다.

이 관리 되는 UDF를 테스트 하려면 Management Studio 내에서 다음 쿼리를 실행 합니다.


[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample15.sql)]

이 명령은 관리 되는 사용 하 여 `udf ComputeInventoryValue_Managed` T-SQL 대신 UDF `udf_ComputeInventoryValue` UDF 다르지만 출력은 동일 합니다. 그림 23 UDF의 출력의 스크린샷을 보려면 다시 참조 합니다.

## <a name="step-12-debugging-the-managed-database-objects"></a>12 단계: 관리 되는 데이터베이스 개체 디버깅

에 [저장 프로시저 디버깅](debugging-stored-procedures-cs.md) 디버깅 Visual Studio를 통해 SQL Server에 대 한 자습서 설명한 세 가지 옵션: 데이터베이스를 직접 디버깅할 응용 프로그램 디버깅 및 SQL Server 프로젝트에서 디버깅 합니다. 클라이언트 응용 프로그램에서 및 SQL Server 프로젝트에서 직접 데이터베이스 개체를 통해 직접 데이터베이스 디버깅 디버깅할 수 없습니다 되지만 디버그할 수 있습니다를 관리 합니다. 하지만 디버깅을 수행 하려면, SQL Server 2005 데이터베이스 허용 되어야 SQL/CLR 디버깅 합니다. 처음 만들 때 회수는 `ManagedDatabaseConstructs` 프로젝트를 Visual Studio 요청 SQL/CLR 디버깅 (2 단계에서에서 그림 6 참조)를 사용 하도록 설정 하려는 여부. 서버 탐색기 창에서 데이터베이스를 마우스 오른쪽 단추로 클릭 하 여이 설정을 수정할 수 있습니다.


![데이터베이스 SQL/CLR 디버깅을 허용 하는지 확인 하십시오.](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image62.png)

**그림 26**: 데이터베이스 SQL/CLR 디버깅을 허용 하는지 확인 하십시오.


디버깅 하 려 한다고 가정은 `GetProductsWithPriceLessThan` 관리 되는 저장된 프로시저입니다. 코드 내에서 중단점을 설정 하 여 먼저는 `GetProductsWithPriceLessThan` 메서드.


[![GetProductsWithPriceLessThan 메서드에서 중단점을 설정 합니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image64.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image63.png)

**그림 27**:에 중단점을 설정는 `GetProductsWithPriceLessThan` 메서드 ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image65.png))


SQL Server 프로젝트에서 관리 되는 데이터베이스 개체 디버깅 조사 s를 사용 합니다. 솔루션에 두 개의 프로젝트-포함 되므로 `ManagedDatabaseConstructs` Visual Studio를 시작 하도록 지시 해야 SQL Server 프로젝트에서 디버깅 하는 데-웹 사이트와 함께 SQL Server 프로젝트는 `ManagedDatabaseConstructs` SQL Server 프로젝트 디버깅을 시작 합니다. 마우스 오른쪽 단추로 클릭는 `ManagedDatabaseConstructs` 솔루션 탐색기에서 프로젝트를 하 고 상황에 맞는 메뉴에서 시작 프로젝트 옵션으로 집합을 선택 합니다.

경우는 `ManagedDatabaseConstructs` 에서 SQL 문을 실행 하는 디버거에서 프로젝트를 시작 하는 `Test.sql` 파일에 있는 `Test Scripts` 폴더입니다. 예를 들어, 테스트 하는 `GetProductsWithPriceLessThan` 관리 되는 저장된 프로시저는 기존 항목 바꾸기 `Test.sql` 호출 하는 다음 문 사용 하 여 콘텐츠 파일의 `GetProductsWithPriceLessThan` 관리 되는 저장된 프로시저에 전달는 `@CategoryID` 14.95의 값:


[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample16.sql)]

적 위의 스크립트를 입력 한 후 `Test.sql`, 디버그 메뉴에 이동 하 고 디버깅 시작을 선택 하거나 f5 키를 눌러 디버깅을 시작 또는 도구 모음에서 녹색 재생 아이콘입니다. 이 솔루션 내의 프로젝트, Northwind 데이터베이스에 관리 되는 데이터베이스 개체 배포 빌드하고 실행 한 다음는 `Test.sql` 스크립트입니다. 이 시점에서 중단점이 적중 됩니다 하 고 단계별로 실행할 수 있습니다는 `GetProductsWithPriceLessThan` 메서드 입력된 매개 변수의 값을 확인 및 등입니다.


[![GetProductsWithPriceLessThan 메서드에서 중단점에 도달 했는지](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image67.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image66.png)

**그림 28**:에서 중단점은 `GetProductsWithPriceLessThan` 메서드 적중 되었음을 ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image68.png))


클라이언트 응용 프로그램을 통해 디버그 해야 하는 SQL 데이터베이스 개체에 대 한 순서로 데이터베이스 응용 프로그램 디버깅을 지원 하도록 구성 되어야 합니다. 서버 탐색기에서 데이터베이스 단추로 클릭 하 고 응용 프로그램 디버깅 옵션이 선택 되어 있는지 확인 합니다. 또한 SQL 디버거 통합 하 고 연결 풀링을 사용 하지 않으려면 ASP.NET 응용 프로그램을 구성 해야 합니다. 2 단계에서에서 자세히 설명한 다음이 단계는 [저장 프로시저 디버깅](debugging-stored-procedures-cs.md) 자습서입니다.

ASP.NET 응용 프로그램 및 데이터베이스를 구성한 후 ASP.NET 웹 사이트를 시작 프로젝트로 설정 하 고 디버깅을 시작 합니다. 중단점을 가진 관리 되는 개체 중 하나를 호출 하는 페이지를 방문 하는 경우 응용 프로그램이 중단 됩니다 및 컨트롤은 선택할 수 하 고 디버거를 단계별로 실행할 수 있습니다 코드 그림 28에 나와 있는 것 처럼 합니다.

## <a name="step-13-manually-compiling-and-deploying-managed-database-objects"></a>13 단계: 수동으로 컴파일 및 배포 관리 되는 데이터베이스 개체

SQL Server 프로젝트를 확인을 작성, 컴파일 및 관리 되는 데이터베이스 개체를 배포 합니다. 안타깝게도, SQL Server 프로젝트는 Visual studio 팀 시스템 및 Professional edition에서 사용할 수만 있습니다. 표준 버전의 Visual Studio 또는 Visual Web Developer를 사용 하는 관리 되는 데이터베이스 개체를 사용 하려는 하는 경우 수동으로 작성 하 고 배포 해야 합니다. 이 네 가지 단계가 포함 됩니다.

1. 관리 되는 데이터베이스 개체에 대 한 소스 코드를 포함 하는 파일 만들기
2. 개체를 어셈블리로 컴파일합니다
3. SQL Server 2005 데이터베이스와 어셈블리를 등록 하 고
4. 어셈블리의 적절 한 메서드를 가리키는 SQL Server에서 데이터베이스 개체를 만듭니다.

관리 되는 해당 제품을 반환 하는 저장된 프로시저를 이러한 작업을 설명, 새 s 인 `UnitPrice` 지정된 된 값 보다 큽니다. 라는 컴퓨터에서 새 파일을 만들 `GetProductsWithPriceGreaterThan.cs` 를 파일에 다음 코드를 입력 하 고 (사용할 수 있습니다 Visual Studio, 메모장 또는 다른 텍스트 편집기가를 위해):


[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample17.cs)]

이 코드는 거의 동일 합니다는 `GetProductsWithPriceLessThan` 5 단계에서에서 만든 메서드. 유일한 차이점은 각 메서드 이름은 `WHERE` 절 및 쿼리에 사용 된 매개 변수 이름입니다. 에 `GetProductsWithPriceLessThan` 메서드를는 `WHERE` 읽기 절: `WHERE UnitPrice < @MaxPrice`합니다. 여기에 `GetProductsWithPriceGreaterThan`, 사용: `WHERE UnitPrice > @MinPrice` 합니다.

이제이 클래스를 어셈블리로 컴파일할 해야 합니다. 명령줄에서 저장 디렉터리로 이동 된 `GetProductsWithPriceGreaterThan.cs` 파일을 C# 컴파일러를 사용 하 여 (`csc.exe`) 클래스 파일을 어셈블리로 컴파일하려면:


[!code-console[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample18.cmd)]

경우 포함 된 폴더로 `csc.exe` 에서 s 시스템에 없는 `PATH`를 완벽 하 게 해당 경로 참조 해야 하며 `%WINDOWS%\Microsoft.NET\Framework\version\`, 같이:


[!code-console[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample19.cmd)]


[![GetProductsWithPriceGreaterThan.cs를 어셈블리로 컴파일합니다](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image70.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image69.png)

**그림 29**: 컴파일 `GetProductsWithPriceGreaterThan.cs` 에 어셈블리 ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image71.png))


`/t` 플래그는 DLL (실행 파일 아님)에 C# 클래스 파일 컴파일되어야 함을 지정 합니다. `/out` 플래그 결과 어셈블리의 이름을 지정 합니다.

> [!NOTE]
> 컴파일하는 대신는 `GetProductsWithPriceGreaterThan.cs` 있습니다 수 또는 사용 하 여 명령줄에서 클래스 파일 [Visual C# Express Edition](https://msdn.microsoft.com/vstudio/express/visualcsharp/) 또는 Visual Studio Standard Edition에서 별도 클래스 라이브러리 프로젝트를 만듭니다. S ren 야곱의 Lauritsen는에 대 한 코드를 사용 하 여 이러한 Visual C# Express Edition 프로젝트를 제공 하십시오는 `GetProductsWithPriceGreaterThan` 3, 5, 10 단계에서 만든 UDF와 저장된 프로시저와 두 개의 저장된 프로시저를 관리 합니다. S ren s 프로젝트에 해당 하는 데이터베이스 개체를 추가 하는 데 필요한 T-SQL 명령을 포함 됩니다.


어셈블리로 컴파일된 코드와 함께 SQL Server 2005 데이터베이스 내에서 어셈블리를 등록할 준비가 됩니다. 이 명령을 사용 하 여 T-SQL을 통해 수행할 수 있습니다 `CREATE ASSEMBLY`, SQL Server Management Studio 나 합니다. Management Studio를 사용 하 여 s 포커스에 남아 있습니다.

Management Studio에서 Northwind 데이터베이스의 프로그래밍 기능 폴더를 확장 합니다. 하위 폴더 중 하나에 어셈블리입니다. 새 어셈블리를 데이터베이스를 수동으로 추가 하려면 어셈블리 폴더를 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 새 어셈블리를 선택 합니다. 새 어셈블리 대화 상자 (그림 30 참조)이 표시 됩니다. 찾아보기 단추를 클릭 하 고 `ManuallyCreatedDBObjects.dll` 어셈블리 방금 컴파일된 하 고 데이터베이스에 어셈블리를 추가 하려면 확인을 클릭 합니다. 보아서는 안는 `ManuallyCreatedDBObjects.dll` 개체 탐색기에서 어셈블리입니다.


[![데이터베이스에 ManuallyCreatedDBObjects.dll 어셈블리를 추가 합니다.](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image73.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image72.png)

**그림 30**: 추가 된 `ManuallyCreatedDBObjects.dll` 데이터베이스에 어셈블리 ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image74.png))


![ManuallyCreatedDBObjects.dll 개체 탐색기에 나열 된](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image75.png)

**그림 31**:는 `ManuallyCreatedDBObjects.dll` 개체 탐색기에 나열


Northwind 데이터베이스에 어셈블리를 추가 했으므로 하는 동안 아직 저장된 프로시저를 연결 하는 `GetProductsWithPriceGreaterThan` 어셈블리의 메서드입니다. 이를 위해 새 쿼리 창을 열고 다음 스크립트를 실행 합니다.


[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample20.sql)]

명명 된 Northwind 데이터베이스에 새 저장된 프로시저를 만들어집니다 `GetProductsWithPriceGreaterThan` 관리 되는 메서드를 연결 하 고 `GetProductsWithPriceGreaterThan` (클래스에 `StoredProcedures`, 어셈블리에 `ManuallyCreatedDBObjects`).

위의 스크립트를 실행 한 후 개체 탐색기에서 저장 프로시저 폴더를 새로 고칩니다. 새 저장된 프로시저 입력-나타납니다 `GetProductsWithPriceGreaterThan` -옆에 있는 잠금 아이콘이 있는입니다. 이 저장된 프로시저를 테스트 하려면 입력 하 고 쿼리 창에서 다음 스크립트를 실행 합니다.


[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample21.sql)]

위의 명령은와 해당 제품에 대 한 정보를 표시 그림 32에서 볼 수 있듯이 `UnitPrice` $24.95 보다 큽니다.


[![ManuallyCreatedDBObjects.dll 개체 탐색기에 나열 된](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image77.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image76.png)

**그림 32**:는 `ManuallyCreatedDBObjects.dll` 개체 탐색기에 나열 됩니다 ([전체 크기 이미지를 보려면 클릭](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image78.png))


## <a name="summary"></a>요약

Microsoft SQL Server 2005 제공 통합으로는 공용 언어 런타임 (CLR), 데이터베이스 개체를 관리 코드를 사용 하 여 만들 수 있습니다. 이전에 T-SQL을 사용 하 여이 데이터베이스 개체 들을 만들 수만 있지만 이제.NET C#과 같은 언어 프로그래밍을 사용 하 여 이러한 개체를 만들 수 있습니다. 만든이 자습서에서는 두 개의 관리 되는 저장된 프로시저 및 관리 되는 사용자 정의 함수입니다.

Visual Studio의 SQL Server 프로젝트 형식 만들기, 컴파일 및 관리 되는 데이터베이스 개체 배포를 지원 합니다. 또한 다양 한 디버깅 지원 기능을 제공합니다. 그러나 SQL Server 프로젝트 유형은의 Visual Studio 팀 시스템 및 Professional edition에서 사용할 수만 있습니다. 교환과 Visual Web Developer 또는 표준 버전의 Visual Studio, 생성, 컴파일 및 배포 단계를 사용 하 여 수행 해야 수동으로 13 단계에서에서 설명한 것 처럼 합니다.

만족도 매우 프로그래밍!

## <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [장점 및 단점 사용자 정의 함수](http://www.samspublishing.com/articles/article.asp?p=31724&amp;rl=1)
- [관리 코드에서 SQL Server 2005 개체 만들기](https://channel9.msdn.com/Showpost.aspx?postid=142413)
- [SQL Server 2005의에서 관리 되는 코드를 사용 하 여 트리거를 만드는 중](http://www.15seconds.com/issue/041006.htm)
- [방법: 만들기 및 실행 CLR SQL Server 저장 프로시저](https://msdn.microsoft.com/en-us/library/5czye81z(VS.80).aspx)
- [방법: 만들기 및 CLR SQL Server 사용자 정의 함수 실행](https://msdn.microsoft.com/en-us/library/w2kae45k(VS.80).aspx)
- [방법: 편집는 `Test.sql` SQL 개체를 실행 하는 스크립트](https://msdn.microsoft.com/en-us/library/ms233682(VS.80).aspx)
- [소개 사용자 정의 함수](http://www.sqlteam.com/item.asp?ItemID=1955)
- [관리 코드와 SQL Server 2005 (비디오)](https://channel9.msdn.com/Showpost.aspx?postid=142413)
- [TRANSACT-SQL 참조](https://msdn.microsoft.com/en-us/library/aa299742(SQL.80).aspx)
- [연습: 관리 코드에서 저장된 프로시저 만들기](https://msdn.microsoft.com/en-us/library/zxsa8hkf(VS.80).aspx)

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 S ren 야곱의 Lauritsen 했습니다. 이 문서, S ren도 검토 하는 것 외에도 관리 되는 데이터베이스 개체를 수동으로 컴파일하기 위해이 문서의 다운로드에 포함 된 Visual C# Express Edition 프로젝트를 만들었습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

>[!div class="step-by-step"]
[이전](debugging-stored-procedures-cs.md)
[다음](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)
