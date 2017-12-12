---
uid: web-forms/overview/data-access/introduction/creating-a-data-access-layer-cs
title: "데이터 액세스 계층 (C#)을 만들려면 | Microsoft Docs"
author: rick-anderson
description: "이 자습서에서는 처음부터 시작 알아보고 만들기 DAL 데이터 액세스 계층 (), 형식화 된 데이터 집합을 사용 하 여 데이터베이스의 정보에 액세스 하려면 하겠습니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/05/2010
ms.topic: article
ms.assetid: cfe2a6a0-1e56-4dc8-9537-c8ec76ba96a4
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/introduction/creating-a-data-access-layer-cs
msc.type: authoredcontent
ms.openlocfilehash: c610f84cfb82f38f9c67b757aa341c7a1497369c
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="creating-a-data-access-layer-c"></a>데이터 액세스 계층 (C#)을 만들려면
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_1_CS.exe) 또는 [PDF 다운로드](creating-a-data-access-layer-cs/_static/datatutorial01cs1.pdf)

> 이 자습서에서는 처음부터 시작 알아보고 만들기 DAL 데이터 액세스 계층 (), 형식화 된 데이터 집합을 사용 하 여 데이터베이스의 정보에 액세스 하려면 하겠습니다.


## <a name="introduction"></a>소개

웹 개발자로 우리 생활 편의 중심으로 데이터를 사용 합니다. 데이터를 검색 하 고, 및를 수집 하 여 요약할 웹 페이지를 수정 하는 코드를 저장 하는 데이터베이스를 만듭니다. ASP.NET 2.0에서 이와 같은 일반적인 패턴을 구현 하기 위한 기술을 살펴봅니다 긴 시리즈의 첫 번째 자습서입니다. 만들기 작업을 시작 합니다는 [소프트웨어 아키텍처](http://en.wikipedia.org/wiki/Software_architecture) 되는 프레젠테이션 계층의 ASP.NET 구성된 페이지 및 사용자 지정 비즈니스 규칙을 적용 하는의 액세스 DAL (데이터 계층) 형식화 된 데이터 집합, 한 BLL 비즈니스 논리 계층 ()를 사용 하 여 구성 일반 페이지 레이아웃을 공유 합니다. 이 백 엔드 기반이 살펴본 다음에, 보고로 이동 되 면, 표시 하는 방법을 보여 주는 요약, 수집 및 웹 응용 프로그램에서 데이터 유효성을 검사 합니다. 이러한 자습서를 간결 하 게 하는 프로세스를 통해 시각적으로 다량의 스크린 샷을 단계별 지침을 제공 하 게 조정 됩니다. 각 자습서 C# 및 Visual Basic 버전에서 사용할 수 있으며 사용 되는 전체 코드의 다운로드에 포함 됩니다. (이 첫 번째 자습서는 매우 긴 하지만 나머지 훨씬 더 많은 양이 청크에서 제공 됩니다.)

이 자습서에 사용할 예정에 배치 하 고 Northwind 데이터베이스의 Microsoft SQL Server 2005 Express Edition 버전은 **앱\_데이터** 디렉터리입니다. 데이터베이스 파일 외에 **앱\_데이터** 폴더는 데이터베이스를 만들기 위한 SQL 스크립트를 다른 데이터베이스 버전을 사용 하려는 경우에 포함 되어 있습니다. 이러한 스크립트는 또한 수 있습니다 [Microsoft에서 직접 다운로드](https://www.microsoft.com/downloads/details.aspx?FamilyID=06616212-0356-46a0-8da2-eebc53a68034&amp;DisplayLang=en)하려는 경우, 합니다. Northwind 데이터베이스의 다른 SQL Server 버전을 사용 하는 경우 업데이트 해야 합니다는 **NORTHWNDConnectionString** 응용 프로그램의 설정 **Web.config** 파일입니다. Visual Studio 2005 Professional Edition을 사용 하 여 파일 시스템 기반 웹 사이트 프로젝트와 웹 응용 프로그램 구축 되었습니다. 그러나이 자습서의 모든 작업은 Visual Studio 2005의 무료 버전에 잘 [Visual Web Developer](https://msdn.microsoft.com/vstudio/express/vwd/)합니다.  
  
이 자습서에서는 처음부터 시작 알아보고 DAL 데이터 액세스 계층 (), 뒤에 두 번째 자습서에서 비즈니스 논리 계층 (BLL)를 만들고 페이지 레이아웃 및 세 번째에서 탐색 작업을 만들 하겠습니다. 세 번째 기초 기반으로 구축 되며 후 자습서에서는 처음 3 개에 배치 합니다. 이 첫 번째 자습서에서 다루지 않으므로 Visual Studio를 시작 하 고 이제 시작 하겠습니다를 많은 접수 했습니다!

## <a name="step-1-creating-a-web-project-and-connecting-to-the-database"></a>1 단계: 웹 프로젝트 만들기 및 데이터베이스에 연결

우리의 액세스 DAL (데이터 계층)을 만들 수 있습니다, 전에 먼저 웹 사이트를 만들고 데이터베이스를 설치 하려면 필요 합니다. 먼저 새 파일 시스템 기반 ASP.NET 웹 사이트를 만듭니다. 이를 위해 파일 메뉴로 이동 하 고 새 웹 사이트 대화 상자를 표시 하는 새 웹 사이트를 선택 합니다. ASP.NET 웹 사이트 템플릿을 선택한, 위치 드롭 다운 목록 파일 시스템으로 설정, 웹 사이트를 배치할 폴더를 선택 및 언어는 C#로 설정 합니다.


[![새 파일 시스템 기반 웹 사이트 만들기](creating-a-data-access-layer-cs/_static/image2.png)](creating-a-data-access-layer-cs/_static/image1.png)

**그림 1**: New File System-Based 웹 사이트 만들기 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image3.png))


이렇게 하면 새 웹 사이트에 만들어집니다는 **Default.aspx** ASP.NET 페이지 및 **앱\_데이터** 폴더입니다.

만든 웹 사이트, Visual Studio 서버 탐색기에서 데이터베이스에 대 한 참조를 추가 하는 다음 단계가입니다. 서버 탐색기에 데이터베이스를 추가 하 여 테이블, 저장된 프로시저, 뷰 및 Visual Studio 내에서 온 모든을 추가할 수 있습니다. 테이블 데이터를 볼 하거나 쿼리 작성기를 통해 직접 또는 그래픽으로 사용자 고유의 쿼리를 만들 수도 있습니다. 또한 DAL에 대 한 형식화 된 데이터 집합을 구축 했습니다 형식화 된 데이터 집합을 생성 해야 하는 데이터베이스 지점 Visual Studio로 해야 합니다. 시간의 해당 지점에서이 연결 정보를 제공할 수 있습니다, 하는 동안 Visual Studio 서버 탐색기에 이미 등록 된 데이터베이스의 드롭 다운 목록을 자동으로 채웁니다.

서버 탐색기에 Northwind 데이터베이스를 추가 하기 위한 단계에서 SQL Server 2005 Express Edition 데이터베이스 사용 여부에 따라 달라 집니다는 **앱\_데이터** 폴더 또는 Microsoft SQL Server 2000 또는 2005 있는 경우 대신 사용 하려면 데이터베이스 서버 설정

## <a name="using-a-database-in-theappdatafolder"></a>데이터베이스를 사용 하 여 theApp에\_DataFolder

데이터베이스 서버에 데이터베이스를 추가할 필요가 없도록 하려면 SQL Server 2000 또는 2005 데이터베이스 서버를 연결할 수 없는 경우에 다운로드 한 websit에 있는 Northwind 데이터베이스의 SQL Server 2005 Express Edition 버전을 사용할 수 있습니다. e's **앱\_데이터** 폴더 (**NORTHWND 합니다. MDF**).

데이터베이스에 배치 된 **앱\_데이터** 폴더가 서버 탐색기에 자동으로 추가 됩니다. 사용자에 게 컴퓨터에 설치 하는 SQL Server 2005 Express Edition 가정 NORTHWND 라는 노드가 표시 됩니다. 서버 탐색기에서 MDF를 확장 하 고 해당 테이블, 뷰, 저장된 프로시저 및에 (그림 2 참조)를 탐색할 수 있습니다.

**앱\_데이터** 폴더 Microsoft Access 포함할 수 **.mdb** 처럼 SQL Server 대응 자동으로 추가 됩니다 서버 탐색기에 있는 파일입니다. SQL Server 옵션 중 하나를 사용 하지 않으려면 경우 언제 든 지 [Northwind 데이터베이스 파일의 Microsoft Access 버전을 다운로드](https://www.microsoft.com/downloads/details.aspx?FamilyID=C6661372-8DBE-422B-8676-C632D66C529C&amp;displaylang=EN) 빠져나와 **앱\_데이터** 디렉터리입니다. 그러나,으로 Access 데이터베이스에 없는 유지 풍부한 기능의 SQL Server와 및 웹 사이트 시나리오에 사용 하도록 설계 되지 않습니다. 또한 몇 가지 35 + 자습서는 Access에서 지원 되지 않는 특정 데이터베이스 수준 기능을 사용 합니다.

## <a name="connecting-to-the-database-in-a-microsoft-sql-server-2000-or-2005-database-server"></a>Microsoft SQL Server 2000 또는 2005 데이터베이스 서버에서 데이터베이스에 연결

데이터베이스 서버에 설치 된 Northwind 데이터베이스에 연결할 수 있습니다. 데이터베이스 서버에 아직 없는 경우 Northwind 데이터베이스를 설치, 먼저 추가 해야 데이터베이스 서버에 또는이 자습서 다운로드에 포함 된 설치 스크립트를 실행 하 여 [SQL Server 2000 버전의 Northwind 다운로드 합니다. 설치 스크립트 및](https://www.microsoft.com/downloads/details.aspx?FamilyID=06616212-0356-46a0-8da2-eebc53a68034&amp;DisplayLang=en) Microsoft 웹 사이트에서 직접 합니다.

설치 되어 있는 데이터베이스를 만든 후 이동 Visual Studio에서 서버 탐색기에 데이터 연결 노드 단추로 클릭 하 고 연결 추가 선택 합니다. 보기로 이동 하 여 서버 탐색기에 표시 되지 않는 경우 / 서버 탐색기 또는 적중된 Ctrl + Alt + S입니다. 그러면 인증 정보 및 데이터베이스 이름을 지정할 수 있는에 연결할 서버, 연결 추가 대화 상자를 표시 됩니다. 데이터베이스 연결 정보를 구성 하 고 확인 단추를 클릭 하면 성공적으로, 데이터베이스 노드 아래에 데이터 연결 노드로 추가 됩니다. 테이블, 뷰, 저장된 프로시저 및 등을 탐색 하는 데이터베이스 노드를 확장할 수 있습니다.


![데이터베이스 서버의 Northwind 데이터베이스에 대 한 연결 추가](creating-a-data-access-layer-cs/_static/image4.png)

**그림 2**: 데이터베이스 서버의 Northwind 데이터베이스에 대 한 연결 추가


## <a name="step-2-creating-the-data-access-layer"></a>2 단계: 데이터 액세스 계층을 만들려면

작업할 때는 데이터 하나의 옵션은 웹 응용 프로그램을 프레젠테이션 계층을 ASP.NET 페이지 확인) (에서 프레젠테이션 계층에 직접 데이터 관련 논리를 포함할입니다. ASP.NET 페이지의 코드 부분에서 ADO.NET 코드를 작성 하거나 SqlDataSource 컨트롤 태그 부분에서 사용 하 여 형식의 걸릴 수 있습니다. 두 경우 모두이 방법은 프레젠테이션 계층으로 데이터 액세스 논리 밀접 하 게 결합 합니다. 그러나 권장 하는 방법,입니다 프레젠테이션 계층과에서 데이터 액세스 논리를 분리 합니다. 이 별도 계층은 줄여서 DAL 데이터 액세스 계층으로 이라고 하며 일반적으로 별도 클래스 라이브러리 프로젝트로 구현 됩니다. 이 계층된 아키텍처의 이점 문서화 되어 (이러한 장점에 대 한 내용은이 자습서의 끝에 "추가 정보" 섹션 참조)이이 시리즈의 해당 메뉴로 이동 합니다는 하다 고 합니다.

데이터베이스에 대 한 연결을 만드는 등의 데이터 원본에만 적용 되는 모든 코드를 발급 **선택**, **삽입**, **업데이트**, 및  **삭제** 명령과 등 DAL에 배치 해야 합니다. 프레젠테이션 계층 이러한 데이터 액세스 코드에 대 한 참조를 포함 해야 하지만 대신 모든 데이터를 요청에 대 한 DAL 호출 해야 합니다. 데이터 액세스 계층에는 일반적으로 기본 데이터베이스 데이터에 액세스 하기 위한 메서드가 포함 되어 있습니다. Northwind 데이터베이스에 예를 들어 **제품** 및 **범주** 속한 범주 및 판매에 대 한 제품을 기록 하는 테이블입니다. 우리의 DAL에 같은 메서드는 됩니다.

- **GetCategories(),** 하는 모든 범주에 대 한 정보를 반환
- **GetProducts()**, 하는 모든 제품에 대 한 정보를 반환
- **GetProductsByCategoryID (*categoryID*) * *는 지정된 된 범주에 속하는 모든 제품을 반환 합니다
- **GetProductByProductID (*productID*) * *, 하는 특정 제품에 대 한 정보를 반환

이러한 메서드를 호출 하는 경우 데이터베이스에 연결 하 고 적절 한 쿼리를 실행 하 고 결과 반환 됩니다. 이러한 결과 반환 하는 것이 중요 합니다. 데이터 집합 또는 DataReader 데이터베이스 쿼리를 사용해 이러한 메서드를 반환 하기만 하면 수 있지만 이상적으로 이러한 결과 반환할지를 사용 하 여 *강력한 형식의 개체*합니다. 강력한 형식의 개체는 스키마는 컴파일 타임에 엄격 하 게 정의 된 반면 반대 자유로운 형식의 개체는 스키마 런타임이 될 때까지 알 수 없는 하나.

예를 들어 DataReader와 기본적으로 데이터 집합은 자유로운 형식의 개체 스키마를 채우는 데 사용 되는 데이터베이스 쿼리에서 반환 된 열에 의해 정의 된 이후입니다. 같은 구문을 사용 해야 하는 느슨한 형 DataTable에서 특정 열에 액세스 하려면:   ***DataTable*합니다. 행 [*인덱스*] ["*columnName*"]**합니다. 이 예에서 DataTable의 느슨한 입력 문자열 또는 서 수 인덱스를 사용 하 여 열 이름에 액세스 해야 하는 팩트에서 발생 합니다. 강력한 형식의 DataTable 반면에 갖습니다의 각 열 속성으로 구현 되기 때문에 다음과 같은 코드를:   ***DataTable*합니다. 행 [*인덱스*].* columnName** *입니다.

강력한 형식의 개체를 반환 하려면 개발자가 자신의 사용자 지정 비즈니스 개체를 만들 하거나 형식화 된 데이터 집합을 사용 합니다. 비즈니스 개체 속성은 일반적으로 비즈니스 개체의 기본 데이터베이스 테이블의 열을 반영 하는 클래스를 나타내는 대로 개발자가 구현 됩니다. 형식화 된 데이터 집합은 데이터베이스 스키마 및 해당 멤버는이 스키마에 따라 강력한 형식에 따라 Visual Studio에서 자동으로 생성 하는 클래스. ADO.NET DataSet, DataTable 및 DataRow 클래스를 확장 하는 클래스의 형식화 된 데이터 집합 자체 구성 됩니다. 뿐만 아니라 강력한 형식의 Datatable 형식화 된 데이터 집합 이제 포함 하는 데이터 집합의 Datatable 채우기 및 수정은 Datatable 내에서 데이터베이스에 다시 전파 하기 위한 메서드를 사용 하 여 클래스입니다.

> [!NOTE]
> 형식화 된 데이터 집합을 사용 하 여 사용자 지정 비즈니스 개체와의 장단점에 자세한 내용은를 참조 [데이터 계층 구성 요소를 디자인 하 고 계층 간 데이터 전달](https://msdn.microsoft.com/en-us/library/ms978496.aspx)합니다.


이 자습서의이 아키텍처에 대 한 강력한 형식의 데이터 집합을 사용 합니다. 그림 3에서는 형식화 된 데이터 집합을 사용 하는 응용 프로그램의 다른 계층 간에 워크플로 보여 줍니다.


[![모든 데이터 액세스 코드에는 dal과 있어는](creating-a-data-access-layer-cs/_static/image6.png)](creating-a-data-access-layer-cs/_static/image5.png)

**그림 3**:에 dal과 모든 데이터 액세스 코드는 있어 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image7.png))


## <a name="creating-a-typed-dataset-and-table-adapter"></a>형식화 된 데이터 집합 및 테이블 어댑터 만들기

우리의 DAL 만들기를 시작 하려면이 프로젝트에 형식화 된 데이터 집합을 추가 하 여 시작 합니다. 이렇게 하려면 솔루션 탐색기에서 프로젝트 노드를 마우스 오른쪽 단추로 클릭 하 고 새 항목 추가 선택 합니다. 템플릿 목록에서 데이터 집합 옵션을 선택 하 고 이름을 **Northwind.xsd**합니다.


[![프로젝트에 새 데이터 집합을 추가 하려면 선택 합니다.](creating-a-data-access-layer-cs/_static/image9.png)](creating-a-data-access-layer-cs/_static/image8.png)

**그림 4**: 프로젝트에 새 데이터 집합을 추가 하도록 선택 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image10.png))


데이터 집합을 추가 하 라는 메시지가 나타나면 추가 클릭 한 후의 **앱\_코드** 폴더를 예를 선택 합니다. 형식화 된 데이터 집합에 대 한 디자이너가 표시 됩니다, 그리고 및 TableAdapter 구성 마법사가 시작 형식화 된 데이터 집합에 첫 번째 여 TableAdapter를 추가할 수 있습니다.

데이터의 강력한 형식의 컬렉션으로 형식화 된 데이터 집합 사용 강력한 형식의 DataRow 인스턴스의 구성 되어 있으며 각 DataTable 인스턴스 강력한 형식으로 구성 됩니다. 이 자습서 시리즈의 작업할 해야 하는 기본 데이터베이스 테이블의 각 항목에 대 한 강력한 형식의 DataTable를 만듭니다. 에 대 한 데이터 테이블을 만드는 것부터 시작 하겠습니다는 **제품** 테이블입니다.

강력한 형식의 Datatable의 기본 데이터베이스 테이블에서 데이터에 액세스 하는 방법에는 정보를 포함 하지 않는 것을 명심 하십시오. DataTable을 채우는 데 데이터를 검색 하기 위해 데이터 액세스 계층으로 작동 하는 TableAdapter 클래스를 사용 합니다. 에 대 한 우리의 **제품** DataTable TableAdapter에는 메서드가 포함 됩니다 **GetProducts()**,  **GetProductByCategoryID (*categoryID*) * * 등 프레젠테이션 계층에서 호출한입니다. DataTable의 역할은 계층 간에 데이터를 전달 하는 데 사용 하는 강력한 형식의 개체 역할을 합니다.

TableAdapter 구성 마법사 사용 하는 데이터베이스를 선택 하 여 시작 합니다. 드롭 다운 목록 서버 탐색기에서 해당 데이터베이스에 나타납니다. 서버 탐색기에 Northwind 데이터베이스를 추가 하지 않은 경우 웹 페이지 그러려면이 이번에 새 연결 단추를 클릭 합니다.


[![드롭다운 목록에서 Northwind 데이터베이스를 선택 합니다.](creating-a-data-access-layer-cs/_static/image12.png)](creating-a-data-access-layer-cs/_static/image11.png)

**그림 5**: 드롭 다운 목록에서 Northwind 데이터베이스를 선택 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image13.png))


데이터베이스를 선택한 다음을 클릭 하 여, 후 묻는에서 연결 문자열을 저장 하려면는 **Web.config** 파일입니다. 연결 문자열을 저장 하 여 하드 코딩 된 TableAdapter 클래스에서를 연결 문자열 정보는 나중에 변경 되 면 작업을 간소화할 수 있는 것을 방지할 수 있습니다. 에 위치한 구성 파일에서 연결 문자열을 저장 하도록 선택할 경우는  **&lt;connectionStrings&gt;**  될 수 있는 섹션 [필요에 따라 암호화 된](http://aspnet.4guysfromrolla.com/articles/021506-1.aspx) 를 개선 하기 위해 보안 또는 관리자에 더 적합 하는 IIS GUI 관리 도구 내에서 새 ASP.NET 2.0 속성 페이지를 통해 나중에 수정 된 합니다.


[![Web.config에 연결 문자열 저장](creating-a-data-access-layer-cs/_static/image15.png)](creating-a-data-access-layer-cs/_static/image14.png)

**그림 6**:에 연결 문자열 저장 **Web.config** ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image16.png))


다음으로, 하 강력한 형식의 첫 번째 데이터 테이블에 대 한 스키마를 정의 하 고 강력한 형식의 DataSet을 채울 때 사용 하 여 TableAdapter 첫 번째 방법을 제공 해야 합니다. 이러한 두 단계는이 DataTable에 반영 한다고 테이블에서 열을 반환 하는 쿼리를 만들어 동시에 수행 됩니다. 마법사의 마지막에이 쿼리에 메서드 이름을 지정 하겠습니다. 된을 달성 되 면 우리의 프레젠테이션 계층에서이 메서드를 호출할 수 있습니다. 메서드는 정의 된 쿼리를 실행 하 고 강력한 형식의 DataTable을 채우는 됩니다.

SQL 쿼리를 정의 합니다. 시작 하려면 TableAdapter 쿼리를 실행 해야 원하는 먼저 지정 해야 했습니다. 임시 SQL 문을 사용 하 여, 새 저장된 프로시저를 만드는 하거나 수 기존 저장된 프로시저를 사용 합니다. 이 자습서에 대 한 임시 SQL 문을 사용 합니다. 참조 [Brian Noyes](http://briannoyes.net/)문서의 [Visual Studio 2005 데이터 집합 디자이너로 데이터 액세스 계층 빌드](http://www.theserverside.net/articles/showarticle.tss?id=DataSetDesigner) 저장된 프로시저를 사용 하는 예제에 대 한 합니다.


[![임시 SQL 문을 사용 하 여 데이터를 쿼리 합니다.](creating-a-data-access-layer-cs/_static/image18.png)](creating-a-data-access-layer-cs/_static/image17.png)

**그림 7**: 특별 SQL 문을 사용 하 여 데이터를 쿼리 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image19.png))


이 시점에서는 입력할 수 SQL 쿼리를 직접. TableAdapter의 첫 번째 메서드를 만들 때에 보통 쿼리를 해당 DataTable에 표현 되어야 하는 열을 반환 합니다. 모든 열과의 모든 행을 반환 하는 쿼리를 만들어이 작업을 수행할 수 있습니다는 **제품** 테이블:


[![입력란에 SQL 쿼리를 입력 합니다.](creating-a-data-access-layer-cs/_static/image21.png)](creating-a-data-access-layer-cs/_static/image20.png)

**그림 8**: SQL 쿼리에는 텍스트 입력 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image22.png))


또는 쿼리 작성기를 사용 하 고 그래픽으로 그림 9에 표시 된 것 처럼 쿼리를 작성 합니다.


[![쿼리 편집기를 통해 쿼리를 그래픽으로 만들기](creating-a-data-access-layer-cs/_static/image24.png)](creating-a-data-access-layer-cs/_static/image23.png)

**그림 9**:는 쿼리 그래픽으로 쿼리 편집기를 통해 만들기 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image25.png))


쿼리를 만든 후 다음 화면으로 이동 하기 전에 고급 옵션 버튼을 클릭 합니다. 웹 사이트 프로젝트에서는 "생성 Insert, Update 및 Delete 문을"는 유일 하 게 고급는 기본적으로 선택 옵션 클래스 라이브러리 또는 Windows 프로젝트에서이 마법사를 실행 하는 경우에 "낙관적 동시성 사용" 옵션 선택 됩니다. 현재 선택 되지 않은 "낙관적 동시성 사용" 옵션을 둡니다. 낙관적 동시성 이후 자습서에서 검토 합니다.


[![생성 Insert, Update 및 Delete 문 옵션을 선택 합니다.](creating-a-data-access-layer-cs/_static/image27.png)](creating-a-data-access-layer-cs/_static/image26.png)

**그림 10**: 생성 Insert, Update 및 Delete 문 옵션을 선택 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image28.png))


고급 옵션을 확인 한 후 최종 화면으로 이동 하려면 다음을 클릭 합니다. 여기 라는 요청 TableAdapter에 추가 하는 방법을 선택할 수 있습니다. 데이터를 채우기 위한 두 가지 패턴 가지가 있습니다.

- **DataTable 채우기** 쿼리 결과에 따라이 방법을 사용 하는 메서드가 만들어집니다을 받으며 매개 변수로 DataTable에 채웁니다. ADO.NET DataAdapter 클래스와 함께이 패턴을 구현 예를 들어 해당 **Fill()** 메서드.
- **DataTable 반환** 이 접근 방식 메서드 및 드립니다 DataTable을 채우는 만들어 메서드 반환 값으로 반환 합니다.

이러한 패턴 중 하나 또는 모두를 구현 하는 TableAdapter를 가질 수 있습니다. 여기에 제공 하는 메서드 이름을 변경할 수 있습니다. 만 사용할 예정 이러한 자습서 전체에서 후자의 패턴 하는 경우에 두 확인란이 모두 선택 옵션을 선택 떠나 자 합니다. 또한의 이름을 아니라 제네릭 **GetData** 메서드를 **GetProducts**합니다.

이 옵션을 선택 하는 경우 최종 확인란 "GenerateDBDirectMethods" 만듭니다 **했**, **update ()**, 및 **delete ()** TableAdapter에 대 한 메서드. 이 옵션을 선택 하는 경우 모든 업데이트 할 TableAdapter의 위한 유일한을 통해 수행할 수 **update ()** 메서드와 형식의 DataSet, DataTable, 단일 DataRow 또는 Datarow의 배열입니다. (선택한 경우이 확인란을 그림 9의 고급 속성에서 선택 되지 않은 "생성 Insert, Update 및 Delete 문을" 옵션 설정은 아무런 효과가 없습니다.) 이 확인란은 선택한 둡니다 보겠습니다.


[![GetData에서 GetProducts로 메서드 이름 변경](creating-a-data-access-layer-cs/_static/image30.png)](creating-a-data-access-layer-cs/_static/image29.png)

**그림 11**:에서 메서드 이름을 변경 **GetData** 를 **GetProducts** ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image31.png))


마침을 클릭 하 여 마법사를 완료 합니다. 마법사를 닫은 후 방금 만든 DataTable을 보여 주는 데이터 집합 디자이너도 돌아옵니다. 열 목록을 볼 수 있습니다는 **제품** DataTable (**ProductID**, **ProductName**등)의 메서드는  **ProductsTableAdapter** (**Fill()** 및 **GetProducts()**).


[![제품 DataTable 및 ProductsTableAdapter 형식화 된 데이터 집합에 추가 되었습니다.](creating-a-data-access-layer-cs/_static/image33.png)](creating-a-data-access-layer-cs/_static/image32.png)

**그림 12**:는 **제품** DataTable 및 **ProductsTableAdapter** 형식화 된 데이터 집합에 추가 되었습니다 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image34.png))


단일 DataTable로 형식화 된 DataSet 했으므로 시점에서 (**Northwind.Products**) 및 DataAdapter 강력한 형식의 클래스 (**NorthwindTableAdapters.ProductsTableAdapter**)와  **GetProducts()** 메서드. 모든 제품의 목록을 다음과 같은 코드에서 액세스 하 이러한 개체를 사용할 수 있습니다.

[!code-html[Main](creating-a-data-access-layer-cs/samples/sample1.html)]

이 코드에 쓴 다음 한 약간의 데이터 액세스 관련 코드가 필요 하지 않았습니다. 모든 ADO.NET 클래스를 인스턴스화할 수 없는, 연결 문자열, SQL 쿼리를 참조 하지 필요가 우리 또는 저장 프로시저. 대신, TableAdapter에 낮은 수준의 데이터 액세스 코드를 제공합니다.

이 예에서 사용 된 각 개체는 강력한 형식의 Visual Studio IntelliSense 및 컴파일 타임 형식 검사를 수행할 수 있도록 허용 합니다. 및 TableAdapter를 반환한 모든 Datatable의 ASP.NET 데이터 GridView, DetailsView, DropDownList, CheckBoxList, 등과 같은 여러 웹 컨트롤을 바인딩할 수 있습니다. 다음 예제에서 반환 된 DataTable을 바인딩하는 **GetProducts()** 방금 롤아웃할 세 줄의 코드 내에서 GridView 메서드는 **페이지\_부하** 이벤트 처리기입니다.

AllProducts.aspx

[!code-aspx[Main](creating-a-data-access-layer-cs/samples/sample2.aspx)]

AllProducts.aspx.cs

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample3.cs)]


[![제품 목록은 GridView에 표시 됩니다.](creating-a-data-access-layer-cs/_static/image36.png)](creating-a-data-access-layer-cs/_static/image35.png)

**그림 13**:는 GridView에 제품의 목록이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image37.png))


이 예제에서는 ASP.NET 페이지의 코드의 세 줄 작성 하는 데 필요한 반면 **페이지\_부하** 이벤트 처리기, 나중에 선언적으로의 데이터를 검색 하는 ObjectDataSource를 사용 하는 방법을 검토 하는 자습서는 DAL 합니다. 코드를 작성 해야 우리는 ObjectDataSource와도 페이징 및 정렬 지원을 받을 수 및!

## <a name="step-3-adding-parameterized-methods-to-the-data-access-layer"></a>3 단계: 추가 데이터 액세스 계층 하는 메서드를 매개 변수화

이 시점에서 우리의 **ProductsTableAdapter** 클래스에는 한 가지 방법은 하지만 **GetProducts()**, 데이터베이스의 모든 제품을 반환 하는입니다. 모든 제품을 사용 하기 위해서는 확실히 유용 하지만, 특정 제품 또는 특정 범주에 속하는 모든 제품에 대 한 정보를 검색할 하고자 하는 경우 경우가 있습니다. 데이터 액세스 계층에 이러한 기능을 추가 하려면 TableAdapter에 매개 변수가 있는 메서드를 추가할 수 있습니다.

추가  **GetProductsByCategoryID (*categoryID*) * * 메서드. 데이터 집합 디자이너 돌아가서 DAL에 새 메서드를 추가 하려면 마우스 오른쪽 단추로 클릭는 **ProductsTableAdapter** 섹션을 추가 하는 쿼리를 선택 합니다.


![TableAdapter를 마우스 오른쪽 단추로 클릭 하 고 선택 쿼리 추가](creating-a-data-access-layer-cs/_static/image38.png)

**그림 14**: TableAdapter를 마우스 오른쪽 단추로 클릭 하 고 선택 쿼리 추가


우리는 먼저 임시 SQL 문 또는 기존 또는 새 저장된 프로시저를 사용 하 여 데이터베이스에 액세스 하고자 하는 방법에 대 한 라는 메시지가 표시 됩니다. 임시 SQL 문을 다시 사용 하도록 선택할 보겠습니다. 다음으로 어떤 유형의 SQL 쿼리 사용 같은 요청 됩니다. 지정된 된 범주에 속하는 모든 제품을 반환할 할 것 이므로 작성 하려고는 **선택** 문이 행을 반환 합니다.


[![행을 반환 하는 SELECT 문을 만드는 선택](creating-a-data-access-layer-cs/_static/image40.png)](creating-a-data-access-layer-cs/_static/image39.png)

**그림 15**: 만들기 하기로 결정 한 **선택** 문에 반환 행 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image41.png))


다음 단계에서는 데이터에 액세스 하는 데 사용 하는 SQL 쿼리를 정의 하는 것입니다. 특정 범주에 속해 있는 제품만 반환할 할 것 이므로 동일한 사용 **선택** 에서 문을 **GetProducts()**, 다음 코드를 추가 하지만 **여기서** 절: **여기서 CategoryID = @CategoryID** 합니다.  **@CategoryID**  만들려는 메서드 (즉, nullable 정수)에서 해당 유형의 입력된 매개 변수는 매개 변수 TableAdapter 마법사를 나타냅니다.


[![만 지정된 된 범주에서 제품을 반환 하는 쿼리를 입력 합니다.](creating-a-data-access-layer-cs/_static/image43.png)](creating-a-data-access-layer-cs/_static/image42.png)

**그림 16**: 지정 된 범주에만 반환 제품에 쿼리를 입력 하십시오 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image44.png))


마지막 단계에서 선택할 수 있습니다 데이터 액세스를 사용할 수 있을 뿐만 아니라 생성 된 메서드 이름을 사용자 지정 하는 패턴입니다. 채우기 패턴에 대 한 바꿔보겠습니다 이름을 **FillByCategoryID** DataTable 반환에 대 한 패턴을 반환 하 고 (의  **가져오기*X** * 메서드), 사용 하 여 보겠습니다  **GetProductsByCategoryID**합니다.


[![TableAdapter 메서드는에 대 한 이름을 선택합니다](creating-a-data-access-layer-cs/_static/image46.png)](creating-a-data-access-layer-cs/_static/image45.png)

**그림 17**: TableAdapter 메서드는에 대 한 이름을 선택 합니다 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image47.png))


마법사를 완료 한 후 데이터 집합 디자이너에서 새 TableAdapter 메서드를 포함 합니다.


![제품 수 이제 범주별으로 쿼리할 수](creating-a-data-access-layer-cs/_static/image48.png)

**그림 18**:의 제품 수 이제 범주별으로 쿼리할 수


추가 하는  **GetProductByProductID (*productID*) * * 동일한 기법을 사용 하는 방법입니다.

데이터 집합 디자이너에서 직접 이러한 매개 변수가 있는 쿼리를 테스트할 수 있습니다. TableAdapter의 메서드에 단추로 클릭 하 고 데이터 미리 보기를 선택 합니다. 다음으로 매개 변수를 사용 하 고 미리 보기를 클릭 하는 값을 입력 합니다.


[![이러한 제품 속하는 음료 범주에 표시 됩니다.](creating-a-data-access-layer-cs/_static/image50.png)](creating-a-data-access-layer-cs/_static/image49.png)

**그림 19**: 음료 범주에 있는 제품 속하는 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image51.png))


와  **GetProductsByCategoryID (*categoryID*) * * 우리의 DAL에 메서드,에서는 지정 된 범주의 제품만 표시 하는 ASP.NET 페이지가 이제 만들 수 있습니다. 다음 예제를 포함 하는 음료 범주에 있는 모든 제품을 **CategoryID** 1입니다.

Beverages.asp

[!code-aspx[Main](creating-a-data-access-layer-cs/samples/sample4.aspx)]

Beverages.aspx.cs

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample5.cs)]


[![이러한 제품 음료 범주에 표시 됩니다.](creating-a-data-access-layer-cs/_static/image53.png)](creating-a-data-access-layer-cs/_static/image52.png)

**그림 20**: 음료 범주에서 제품 하는 것이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image54.png))


## <a name="step-4-inserting-updating-and-deleting-data"></a>4 단계: 삽입, 업데이트 및 데이터 삭제

일반적으로 삽입, 업데이트 및 데이터 삭제에 사용 하는 두 가지 패턴이 있습니다. 데이터베이스 직접 패턴 이라고 부르겠습니다의 첫 번째 패턴을 만들어야 메서드는 호출 되 면 문제는 **삽입**, **업데이트**, 또는 **삭제** 명령을에 단일 데이터베이스 레코드에 작동 하는 데이터베이스입니다. 이러한 메서드는 일반적으로 삽입, 업데이트 또는 삭제 된 값으로 일련의 해당 하는 스칼라 값 (정수, 문자열, 부울, Datetime, 및 등)에 전달 됩니다. 이 패턴에 대 한 사용 예를 들어는 **제품** delete 메서드는 정수 매개 변수에서 수행 되는 테이블을 나타내는 **ProductID** insert 메서드 수행 되는 동안 삭제할 레코드의는 에 대 한 문자열의 **ProductName**에 대 한 10 진수는 **UnitPrice**에 대 한 정수는 **UnitsOnStock**등입니다.


[![각 삽입, 업데이트 및 삭제 요청에 즉시 데이터베이스에 전송 됩니다.](creating-a-data-access-layer-cs/_static/image56.png)](creating-a-data-access-layer-cs/_static/image55.png)

**그림 21**: 각 삽입, 업데이트 및 삭제 요청에 즉시 데이터베이스에 전송 됩니다 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image57.png))


참조 업데이트 패턴에 따라 일괄 처리 하는 것을 다른 패턴은 전체 데이터 집합, DataTable, 또는 한 메서드 호출에서 Datarow의 컬렉션을 업데이트 하기 위해서입니다. 이 패턴으로 개발자 삭제, 삽입 및 수정 DataTable에 Datarow 하 고 update 메서드를 이러한 Datarow 또는 DataTable을 전달 합니다. 이 메서드를 다음에 전달 된 Datarow를 열거, 확인 여부은 한 수정, 추가 되거나 삭제 (DataRow의 통해 [RowState 속성](https://msdn.microsoft.com/en-us/library/system.data.datarow.rowstate.aspx) 값), 각 레코드에 대 한 적절 한 데이터베이스 요청을 실행 하 고 있습니다.


[![Update 메서드를 호출 하면 모든 변경 내용이 데이터베이스와 동기화](creating-a-data-access-layer-cs/_static/image59.png)](creating-a-data-access-layer-cs/_static/image58.png)

**그림 22**: Update 메서드를 호출 하면 모든 변경 내용이 데이터베이스와 동기화 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image60.png))


TableAdapter 일괄 처리 업데이트 패턴을 사용 하 여 기본적으로 지만 DB 직접 패턴을 지원 합니다. 우리의 TableAdapter를 만들 때 고급 속성에서 "생성 Insert, Update 및 Delete 문을" 옵션을 선택 했습니다 않아는 **ProductsTableAdapter** 포함는 **update ()** 메서드 일괄 처리 업데이트 패턴을 구현합니다. TableAdapter가 포함 된 특히는 **update ()** 형식화 된 데이터 집합, 강력한 형식의 데이터 테이블 또는 하나 이상의 Datarow 전달 될 수 있는 메서드. 두 었으 면 "GenerateDBDirectMethods" 확인란이 선택 때 먼저 DB 직접 패턴은 TableAdapter를 만들기도 구현 될 통해 **했**, **update ()**, 및 **delete)**  메서드.

두 데이터 수정 패턴을 사용 하 여 TableAdapter의 **InsertCommand**, **UpdateCommand**, 및 **DeleteCommand** 발급 하는 속성의 **삽입** , **업데이트**, 및 **삭제** 명령을 데이터베이스에 있습니다. 검사 및 수정할 수는 **InsertCommand**, **UpdateCommand**, 및 **DeleteCommand** 데이터 집합 디자이너의 TableAdapter에서 클릭 한 다음 이동 하 여 속성 속성 창. (및 TableAdapter를 선택 했는지 확인는 **ProductsTableAdapter** 이 개체는 속성 창에서 드롭 다운 목록에서 선택 합니다.)


[![TableAdapter에 InsertCommand, UpdateCommand, 및 DeleteCommand 속성](creating-a-data-access-layer-cs/_static/image62.png)](creating-a-data-access-layer-cs/_static/image61.png)

**그림 23**: The TableAdapter에 **InsertCommand**, **UpdateCommand**, 및 **DeleteCommand** 속성 ([을 보려면 클릭 전체 크기 이미지](creating-a-data-access-layer-cs/_static/image63.png))


클릭을 검사 하거나 이러한 데이터베이스 명령 속성을 수정 하려면는 **CommandText** 하위 속성은 쿼리 작성기를 표시 합니다.


[![쿼리 작성기에서 INSERT, UPDATE 및 DELETE 문이 구성](creating-a-data-access-layer-cs/_static/image65.png)](creating-a-data-access-layer-cs/_static/image64.png)

**그림 24**: 구성에서 **삽입**, **업데이트**, 및 **삭제** 쿼리 작성기에서 문 ([전체 크기 이미지를 보려면 클릭 ](creating-a-data-access-layer-cs/_static/image66.png))


다음 코드 예제에서는 단종 되지 고 25 단위 이내 재고에 있는 모든 제품의 가격을 두 배로 일괄 처리 업데이트 패턴을 사용 하는 방법을 보여 줍니다.

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample6.cs)]

아래 코드 DB 직접 패턴을 사용 하 여 프로그래밍 방식으로 특정 제품을 삭제 한 다음 하나를 업데이트 한 다음 새 복제본을 추가 하는 방법을 보여 줍니다.

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample7.cs)]

## <a name="creating-custom-insert-update-and-delete-methods"></a>만드는 사용자 지정 Insert, Update 및 Delete 메서드

**했**, **update ()**, 및 **delete ()** DB 직접 메서드에서 만든 메서드 특히 많은 열이 있는 테이블에 대 한 약간은 복잡할 수 있습니다. 이전 코드 예제에서는 IntelliSense의 명확 하지 않은 경우가 특히 무엇을 할 수 없이 살펴보면 **제품** 테이블 열에 각 입력된 매개 변수를 매핑하는 **update ()** 및 **insert)**  메서드. 때만 포함 하려고를 단일 열 또는 둘을 업데이트 하거나 원하는 사용자 지정 하는 경우가 있을 수 있습니다 **했** 메서드는, 새로 삽입된 된 레코드의 값을 반환 **IDENTITY** (자동 증분) 필드입니다.

사용자 지정 메서드를 만들려면 데이터 집합 디자이너를 반환 합니다. TableAdapter 고 TableAdapter 마법사를 반환 하는 추가 쿼리를 선택 합니다. 두 번째 화면에서 만들 쿼리의 형식을 나타낼 수 있습니다. 새 제품을 추가한 후 새로 추가 된 레코드의 값을 반환 하는 메서드를 만들어 보겠습니다 **ProductID**합니다. 따라서 만들도록 선택한는 **삽입** 쿼리 합니다.


[![Products 테이블에 새 행을 추가 하는 메서드 만들기](creating-a-data-access-layer-cs/_static/image68.png)](creating-a-data-access-layer-cs/_static/image67.png)

**그림 25**: 새 행을 추가 하는 메서드 만들기는 **제품** 테이블 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image69.png))


다음 화면에서의 **InsertCommand**의 **CommandText** 나타납니다. 추가 하 여이 쿼리를 보강할 **범위 선택\_IDENTITY()** 쿼리의 끝에 삽입 된 마지막 id 값을 반환 합니다는 **IDENTITY** 같은 범위에 있는 열입니다. (참조는 [기술 문서](https://msdn.microsoft.com/en-us/library/ms190315.aspx) 에 대 한 자세한 내용은 **범위\_IDENTITY()** 하고자 하는 이유 및 [범위를 사용 하 여\_대신 IDENTITY() @ @IDENTITY](http://weblogs.sqlteam.com/travisl/archive/2003/10/29/405.aspx).) 끝낼 때는 **삽입** 문을 세미콜론으로 추가 하기 전에 **선택** 문.


[![Scope_identity () 값을 반환 하도록 쿼리를 확장 합니다.](creating-a-data-access-layer-cs/_static/image71.png)](creating-a-data-access-layer-cs/_static/image70.png)

**그림 26**: 반환 하도록 쿼리를 확장 하 고 **범위\_IDENTITY()** 값 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image72.png))


새 메서드의 이름을 **InsertProduct**합니다.


[![새 메서드 이름을 InsertProduct로 설정](creating-a-data-access-layer-cs/_static/image74.png)](creating-a-data-access-layer-cs/_static/image73.png)

**그림 27**: 새 메서드 이름으로 설정 **InsertProduct** ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image75.png))


다시 방문 데이터 집합 디자이너 표시 됩니다는 **ProductsTableAdapter** 새 메서드가 포함 **InsertProduct**합니다. 이 새로운 방법을 각 열에 대 한 매개 변수 없는 경우는 **제품** 테이블 될 확률이 종료 하지 않았습니다 고 **삽입** 문을 세미콜론으로 합니다. 구성에서 **InsertProduct** 메서드 세미콜론으로 구분 해야 하 고는 **삽입** 및 **선택** 문.

기본적으로 삽입 메서드 문제 쿼리가 아닌 메서드, 즉 영향을 받는 행 수를 반환 합니다. 그러나 원하는 **InsertProduct** 영향을 받는 행 수가 아니라 쿼리에 의해 반환 되는 값을 반환 하는 메서드. 이를 위해 조정는 **InsertProduct** 메서드의 **ExecuteMode** 속성을 **스칼라**합니다.


[![스칼라 ExecuteMode 속성 변경](creating-a-data-access-layer-cs/_static/image77.png)](creating-a-data-access-layer-cs/_static/image76.png)

**그림 28**: 변경 된 **ExecuteMode** 속성을 **스칼라** ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image78.png))


다음 코드에서는 새로운 **InsertProduct** 메서드 실행에서:

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample8.cs)]

## <a name="step-5-completing-the-data-access-layer"></a>5 단계: 완료 데이터 액세스 계층

**ProductsTableAdapters** 반환 클래스는 **CategoryID** 및 **SupplierID** 에서 값의 **제품** 테이블 하지만 포함 되지 않습니다는 **CategoryName** 열에서는 **범주** 테이블 또는 **CompanyName** 열에서는 **Suppliers**이러한 변수는 가능성이 제품 정보를 표시 하는 때를 표시 하려는 열 이지만 테이블입니다. TableAdapter의 초기 메서드를 추가할 수 있습니다 **GetProducts()**, 둘 다 포함 하는 **CategoryName** 및 **CompanyName** 업데이트 하면 열 값은 이러한 새 열을 포함 하려면 강력한 형식의 DataTable입니다.

그러나이 수는 문제를 TableAdapter의 메서드를 삽입 하기 위한 같은 업데이트 시키며 삭제 데이터는이 초기 방법을 기반으로 합니다. 다행히 자동 생성 된 메서드를 삽입, 업데이트 및 삭제 하지 않은 영향을 받는의 하위 쿼리는 **선택** 절. 이 쿼리를 추가 하도록 하 여 **범주** 및 **공급 업체** 하위 쿼리로 대신 **조인** s, 우리 합니다 필요가 데이터 수정에 대 한 이러한 메서드를 다시 작성 합니다. 마우스 오른쪽 단추로 클릭는 **GetProducts()** 에서 메서드는 **ProductsTableAdapter** 구성을 선택 합니다. 그런 다음 조정 된 **선택** 절 표시 되도록 같은:

[!code-sql[Main](creating-a-data-access-layer-cs/samples/sample9.sql)]


[![SELECT 문은 GetProducts() 메서드에 대 한 업데이트](creating-a-data-access-layer-cs/_static/image80.png)](creating-a-data-access-layer-cs/_static/image79.png)

**그림 29**: 업데이트는 **선택** 문에 **GetProducts()** 메서드 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image81.png))


업데이트 한 후의 **GetProducts()** DataTable에는 두 개의 새 열이 새 쿼리를 사용 하는 메서드: **CategoryName** 및 **공급 업체 이름**합니다.


![제품 DataTable에 새 열 두 개](creating-a-data-access-layer-cs/_static/image82.png)

**그림 30**:는 **제품** DataTable에 새 열 두 개


업데이트 하는 **선택** 절에는  **GetProductsByCategoryID (*categoryID*) * * 메서드도 있습니다.

업데이트 하는 경우는 **GetProducts()** **선택** 를 사용 하 여 **조인** 데이터 집합 디자이너 구문을 삽입, 업데이트 및 삭제에 대 한 메서드를 자동으로 생성할 수 없습니다 DB를 사용 하 여 데이터베이스 데이터 직접 패턴입니다. 수동으로 만든 훨씬와 동일한 방식 처럼 해야 하는 대신,는 **InsertProduct** 이 자습서의 앞부분에 나오는 메서드. 또한 해야 합니다. 수동으로 제공 하는 **InsertCommand**, **UpdateCommand**, 및 **DeleteCommand** 패턴을 업데이트 하는 일괄 처리를 사용 하려는 값을 속성입니다.

## <a name="adding-the-remaining-tableadapters"></a>나머지 Tableadapter를 추가합니다.

지금까지 단일 데이터베이스 테이블에 대 한 단일 TableAdapter 작업 알아보았습니다만 합니다. 그러나 Northwind 데이터베이스는이 웹 응용 프로그램에서 작업할 해야 하는 여러 관련된 테이블을 포함 합니다. Datatable을 관련 형식화 된 데이터 집합을 여러 개 포함 될 수 있습니다. 따라서 우리의 DAL을 완료 하려면 추가 해야 Datatable이이 자습서에 사용할 다른 테이블에 대 한 합니다. 새 TableAdapter를 형식화 된 데이터 집합을 추가 하려면 데이터 집합 디자이너를 열려면 마우스 오른쪽 단추로 클릭 디자이너에서 추가 선택 / TableAdapter. 새 DataTable 및 TableAdapter를 만들고이 자습서의 앞부분에 나오는 검사 했습니다 마법사 과정을 안내 합니다.

몇 분 정도 걸릴 다음 Tableadapter와 다음 쿼리를 사용 하 여 메서드를 만듭니다. 쿼리는 **ProductsTableAdapter** 각 제품 범주와 공급 업체 이름을 가져올 하위 쿼리가 포함 됩니다. 또한 작업을 수행 했다면, 이미 추가한 경우는 **ProductsTableAdapter** 클래스의 **GetProducts()** 및  **GetProductsByCategoryID (*categoryID*) * * 메서드.

- **ProductsTableAdapter**

    - **GetProducts**: 

        [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample10.sql)]
    - **GetProductsByCategoryID**: 

        [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample11.sql)]
    - **GetProductsBySupplierID**: 

        [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample12.sql)]
    - **GetProductByProductID**: 

        [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample13.sql)]
- **CategoriesTableAdapter**

    - **GetCategories**: 

        [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample14.sql)]
    - **GetCategoryByCategoryID**: 

        [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample15.sql)]
- **SuppliersTableAdapter**

    - **GetSuppliers**: 

        [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample16.sql)]
    - **GetSuppliersByCountry**: 

        [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample17.sql)]
    - **GetSupplierBySupplierID**: 

        [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample18.sql)]
- **EmployeesTableAdapter**

    - **GetEmployees**: 

        [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample19.sql)]
    - **GetEmployeesByManager**: 

        [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample20.sql)]
    - **GetEmployeeByEmployeeID**: 

        [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample21.sql)]


[![4 개의 Tableadapter를 추가한 후 데이터 집합 디자이너](creating-a-data-access-layer-cs/_static/image84.png)](creating-a-data-access-layer-cs/_static/image83.png)

**그림 31**: The 데이터 집합 디자이너 후의 4 개 Tableadapter 추가 되었습니다 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image85.png))


## <a name="adding-custom-code-to-the-dal"></a>에 dal과 사용자 지정 코드 추가

Tableadapter 및 형식화 된 데이터 집합에 추가 Datatable XML 스키마 정의 파일에는로 표현 됩니다 (**Northwind.xsd**). 마우스 오른쪽 단추로 클릭 하 여이 스키마 정보를 볼 수 있습니다는 **Northwind.xsd** 솔루션 탐색기에서 파일 및 코드 보기를 선택 합니다.


[![형식화 된 데이터 집합의 Northwinds에 대 한 XML 스키마 정의 (XSD) 파일](creating-a-data-access-layer-cs/_static/image87.png)](creating-a-data-access-layer-cs/_static/image86.png)

**그림 32**: Northwinds 형식화 된 데이터 집합에 대 한 XML 스키마 정의 (XSD) 파일 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image88.png))


이 스키마 정보는 컴파일할 때 또는 런타임 시 (필요한 경우), 이때 단계별로 실행할 수 있습니다이 디버거에서 디자인 타임에 C# 또는 Visual Basic 코드로 변환 됩니다. 보려면이 자동으로 생성 된 코드 이동 클래스 뷰 및 드릴 TableAdapter 또는 형식화 된 데이터 집합 클래스에 있습니다. 화면에 클래스 뷰 보이지 않으면 보기 메뉴로 이동 하 고 여기에서 선택 하거나 Ctrl + Shift + c 합니다. 클래스 뷰에서 속성, 메서드 및 형식화 된 데이터 집합 및 TableAdapter 클래스의 이벤트를 볼 수 있습니다. 특정 방법에 대 한 코드를 보려면 클래스 뷰에서 메서드 이름을 두 번 클릭 하거나 마우스 오른쪽 정의로 이동 합니다.


![클래스 뷰에서 정의로 이동을 선택 하 여 자동으로 생성 된 코드를 검사 합니다.](creating-a-data-access-layer-cs/_static/image89.png)

**그림 33**: 클래스 뷰에서 정의에 Go를 선택 하 여 자동으로 생성 된 코드를 검사 합니다.


코드 자동 생성 된 시간을 많이 줄일 수 있지만, 코드는 종종 매우 일반적 이며 필요를 응용 프로그램의 고유한 요구 사항에 맞게 사용자 지정할 수 있습니다. 그러나이 자동으로 생성 된 코드를 확장 하는 위험 코드를 생성 하는 도구 사용자 지정을 덮어쓰고 "다시 생성"을 결정할 수입니다. .NET 2.0의 새로운 partial 클래스 개념을 여러 파일에 걸쳐 분할 하기 쉽습니다. 이 통해이 사용자 지정 항목을 덮어쓰지 Visual Studio에 대해 걱정할 필요 없이 자동으로 생성 된 클래스에 고유한 메서드, 속성 및 이벤트를 추가할 수 있습니다.

DAL을 사용자 지정 하는 방법을 보여 주는, 추가해보겠습니다는 **GetProducts()** 메서드를는 **SuppliersRow** 클래스입니다. **SuppliersRow** 클래스의 단일 레코드를 나타냅니다.는 **Suppliers** 테이블; 여러 제품에 각 공급 업체 수 있는 공급자 0 하므로 **GetProducts()** 하는 것을 반환 합니다 지정 된 공급 업체의 제품입니다. 새 클래스 파일을 만들이 수행 하는 **앱\_코드** 라는 폴더 **SuppliersRow.cs** 다음 코드를 추가 하 고:

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample22.cs)]

이 partial 클래스 컴파일러에 지시 때 작성 된 **Northwind.SuppliersRow** 포함 하도록 클래스는 **GetProducts()** 방금 정의한 메서드. 프로젝트를 빌드할 경우 한 후 클래스 보기로 돌아와서 표시 **GetProducts()** 의 메서드로 나열 **Northwind.SuppliersRow**합니다.


![GetProducts() 메서드는 Northwind.SuppliersRow 클래스의 일부 이제](creating-a-data-access-layer-cs/_static/image90.png)

**그림 34**:는 **GetProducts()** 메서드는 지금의 일부는 **Northwind.SuppliersRow** 클래스


**GetProducts()** 다음 코드와 같이 특정 공급 업체의 제품 집합을 열거 하 이제 메서드를 사용할 수 있습니다.

[!code-html[Main](creating-a-data-access-layer-cs/samples/sample23.html)]

이 데이터는 ASP 중 하나에 표시 수 있습니다. NET의 데이터 웹 컨트롤입니다. 다음 페이지에 두 필드는 GridView 컨트롤을 사용합니다.

- 각 공급 업체의 이름을 표시 하는 BoundField 및
- 반환 된 결과에 바인딩되는 BulletedList 컨트롤이 포함 된 TemplateField는 **GetProducts()** 각 공급 업체에 대 한 메서드.

이후 자습서에서 해당 마스터-세부 정보 보고서를 표시 하는 방법을 검토 합니다. 지금은이 예제는 설명에 추가 사용자 지정 메서드를 사용 하 여 **Northwind.SuppliersRow** 클래스입니다.

SuppliersAndProducts.aspx

[!code-aspx[Main](creating-a-data-access-layer-cs/samples/sample24.aspx)]

SuppliersAndProducts.aspx.cs

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample25.cs)]


[![왼쪽 열 오른쪽에 있는 해당 제품에에서 공급 업체의 회사 이름이 나열 됩니다.](creating-a-data-access-layer-cs/_static/image92.png)](creating-a-data-access-layer-cs/_static/image91.png)

**그림 35**: 왼쪽 열의 오른쪽에 있는 해당 제품의 공급 업체의 회사 이름이 나열 됩니다 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image93.png))


## <a name="summary"></a>요약

때 웹 응용 프로그램 만들기 DAL 프레젠테이션 계층 만들기를 시작 하기 전에 발생 하 여 첫 번째 단계 중 하나 여야 합니다. Visual Studio와 함께 만들기 형식화 된 데이터 집합에 따라 DAL은 코드 줄도 작성 하지 않고 10-15 분 후에 수행할 수 있는 작업입니다. 앞으로 이동 하는 자습서는이 DAL에 작성 합니다. 에 [다음 자습서](creating-a-business-logic-layer-cs.md) म 다양 한 비즈니스 규칙을 정의 하 고 별도 비즈니스 논리 계층에서이 구현 하는 방법을 참조 합니다.

만족도 매우 프로그래밍!

## <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [강력한 형식의 Tableadapter 및 Datatable VS 2005와 ASP.NET 2.0을 사용 하 여 DAL 작성](https://weblogs.asp.net/scottgu/435498)
- [데이터 계층 구성 요소를 디자인 하 고 계층을 통한 데이터 전달](https://msdn.microsoft.com/en-us/library/ms978496.aspx)
- [Visual Studio 2005 데이터 집합 디자이너로 데이터 액세스 계층을 구축](http://www.theserverside.net/articles/showarticle.tss?id=DataSetDesigner)
- [ASP.NET 2.0에서에서 구성 정보 암호화 응용 프로그램](http://aspnet.4guysfromrolla.com/articles/021506-1.aspx)
- [TableAdapter 개요](https://msdn.microsoft.com/en-us/library/bz9tthwx.aspx)
- [형식화 된 데이터 집합으로 작업](https://msdn.microsoft.com/en-us/library/esbykkzb.aspx)
- [Visual Studio 2005와 ASP.NET 2.0에서 강력한 형식의 데이터 액세스를 사용 하 여](http://aspnet.4guysfromrolla.com/articles/020806-1.aspx)
- [TableAdapter 메서드를 확장 하는 방법](https://blogs.msdn.com/vbteam/archive/2005/05/04/ExtendingTableAdapters.aspx)
- [저장된 프로시저에서 스칼라 데이터 검색](http://aspnet.4guysfromrolla.com/articles/062905-1.aspx)

### <a name="video-training-on-topics-contained-in-this-tutorial"></a>이 자습서에 포함 된 항목에 대 한 비디오 교육

- [ASP.NET 응용 프로그램에서 데이터 액세스 계층](../../../videos/data-access/adonet-data-services/data-access-layers-in-aspnet-applications.md)
- [수동으로 Datagrid에 데이터 집합을 바인딩하는 방법](../../../videos/data-access/adonet-data-services/how-to-manually-bind-a-dataset-to-a-datagrid.md)
- [ASP 응용 프로그램에서 데이터 집합 및 필터와 함께 작동 하는 방법](../../../videos/data-access/adonet-data-services/how-to-work-with-datasets-and-filters-from-an-asp-application.md)

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Ron 녹색, Hilton Giesenow, Dennis Patterson, Liz Shulok, Abel Gomez 및 Carlos Santos 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

>[!div class="step-by-step"]
[다음](creating-a-business-logic-layer-cs.md)
