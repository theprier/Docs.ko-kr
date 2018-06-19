---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started
title: '1 부 Entity Framework 4.0 및 ObjectDataSource 컨트롤을 사용 하 여,: 시작 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈의 Entity Framework 자습서 시리즈 시작 하기에 의해 만들어진 Contoso 대학 웹 응용 프로그램 기반으로 합니다. 경우 yo...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/26/2011
ms.topic: article
ms.assetid: 244278c1-fec8-4255-8a8a-13bde491c4f5
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started
msc.type: authoredcontent
ms.openlocfilehash: 6584767418c898913777b3b1549a816679c8430d
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30892084"
---
<a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-1-getting-started"></a>1 부 Entity Framework 4.0 및 ObjectDataSource 컨트롤을 사용 하 여,: 시작 하기
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

> 에 의해 만들어진 Contoso 대학 웹 응용 프로그램을 기반으로 하는이 자습서 시리즈의 [Entity Framework 4.0이 있는 시작](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md) 자습서 시리즈 합니다. 이전 자습서를 완료 하지 않은 경우이 자습서에 대 한 시작 점으로 하면 [응용 프로그램을 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) 만들어졌을 것입니다. 수도 있습니다 [응용 프로그램을 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) 완료 하는 자습서 시리즈에서 만들어진 합니다.
> 
> Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 4.0 및 Visual Studio 2010을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 샘플 응용 프로그램은 가상의 Contoso 대학교에 대 한 웹 사이트입니다. 학생 입학, 강좌 개설 및 강사 할당과 같은 기능이 있습니다.
> 
> 이 자습서는 C#의 예를 보여줍니다. [다운로드 가능한 샘플](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) C# 및 Visual Basic 코드를 포함 합니다.
> 
> ## <a name="database-first"></a>먼저 데이터베이스
> 
> 세 가지 방법으로 데이터 Entity Framework에서 사용할 수 있습니다: *Database First*, *Model First*, 및 *Code First*합니다. 첫 번째 데이터베이스에 대 한이 자습서가입니다. 이러한 워크플로 지침 간의 차이점에 대 한 사용자 시나리오에 가장 적합 한 선택 하는 방법에 정보를 참조 하십시오. [Entity Framework 개발 워크플로에](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)합니다.
> 
> ## <a name="web-forms"></a>Web Forms
> 
> Getting Started 일련 것 처럼이 자습서 시리즈는 ASP.NET Web Forms 모델을 사용 하 고 Visual Studio에서 ASP.NET Web Forms를 사용 하는 방법을 알고 있다고 가정 합니다. 를 찾을 수 없으면 [ASP.NET 4.5 Web Forms 시작](../../getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)합니다. ASP.NET MVC 프레임 워크를 사용 하는 것을 선호 하는 경우 참조 [Getting Started with ASP.NET MVC를 사용 하 여 Entity Framework](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다.
> 
> ## <a name="software-versions"></a>소프트웨어 버전
> 
> | **이 자습서에 표시** | **또한에 사용할 수** |
> | --- | --- |
> | Windows 7 | Windows 8 |
> | Visual Studio 2010 | Visual Studio 2010 Express for Web입니다. 자습서과 최신 버전의 Visual Studio 테스트 되지 않은 합니다. 선택한 메뉴, 대화 상자 및 서식 파일에는 다음과 같은 많은 차이가 있습니다. |
> | .NET 4 | .NET 4.5는.NET 4와 역호환 있지만 자습서.NET 4.5가 설치 된 테스트 되지 않았습니다. |
> | Entity Framework 4 | 이후 버전의 Entity Framework 자습서 테스트 되지 않은 합니다. Entity Framework 5 부터는 EF는 기본적으로 사용 된 `DbContext API` 는 EF 4.1에서 도입 되었습니다. EntityDataSource 컨트롤은 사용 하도록 설계 된는 `ObjectContext` API입니다. EntityDataSource를 사용 하는 방법에 대 한 정보에 대 한 컨트롤의 `DbContext` API 참조 [이 블로그 게시물](https://blogs.msdn.com/b/webdev/archive/2012/09/13/how-to-use-the-entitydatasource-control-with-entity-framework-code-first.aspx)합니다. |
> 
> ## <a name="questions"></a>질문
> 
> 자습서를 직접 관련 되지 않는 질문 해야 하도록를 게시할 수 있습니다는 [ASP.NET Entity Framework 포럼](https://forums.asp.net/1227.aspx), [Entity Framework와 LINQ to Entities 포럼](https://social.msdn.microsoft.com/forums/adodotnetentityframework/threads/), 또는 [ StackOverflow.com](http://stackoverflow.com/)합니다.


`EntityDataSource` 컨트롤을 사용 하면 응용 프로그램을 매우 신속 하 게 만들 수 있지만 일반적으로 필요한 비즈니스 논리 및 데이터 액세스 논리에 상당한 양의 유지할 수 있습니다 프로그램 *.aspx* 페이지입니다. 복잡 하 고 지속적인 유지 관리를 요구 하려면 응용 프로그램의 예상 되는 경우 높여줍니다 더 많은 개발 시간을 미리 만들려면는 *n 계층* 또는 *계층화* 응용 프로그램 구조 더 쉽게 유지 관리할입니다. 이 아키텍처를 구현 하려면 BLL ()는 비즈니스 논리 계층 및 데이터 액세스 계층 (DAL)에서 프레젠테이션 계층을 구분 합니다. 이 구조를 구현 하는 한 가지 방법은 사용 하는 것은 `ObjectDataSource` 컨트롤 대신는 `EntityDataSource` 제어 합니다. 사용 하는 경우는 `ObjectDataSource` 컨트롤을 사용자 고유의 데이터 액세스 코드를 구현 하 고 다음 호출에서 *.aspx* 가 같은 많이 사용 하는 컨트롤을 사용 하 여 페이지 기능을 다른 데이터 소스 컨트롤입니다. 이 n 계층 접근 방식의 이점을 Web Forms 컨트롤을 사용 하 여 데이터 액세스의 장점을 함께 결합할 수 있습니다.

`ObjectDataSource` 컨트롤을 사용 하면 보다 융통성 있게의 다른 방법으로도 합니다. 사용자 고유의 데이터 액세스 코드를 작성 하기 때문에 쉽습니다 수행 보다 더 읽기, 삽입, 업데이트 또는 삭제는 특정 엔터티 형식에는 작업은 하는 `EntityDataSource` 컨트롤 수행 하도록 설계 되었습니다. 예를 들어 데이터를 보관 하는 엔터티를 삭제 하거나 자동으로 확인 하 고 업데이트 관련 데이터 외래 키 값이 있는 행을 삽입할 때 필요에 따라 때마다, 엔터티 업데이트 될 때마다 로깅 수행할 수 있습니다.

## <a name="business-logic-and-repository-classes"></a>비즈니스 논리 및 리포지토리 클래스

`ObjectDataSource` 만든 클래스를 호출 하 여 작동을 제어 합니다. 데이터를 검색 및 업데이트 하는 메서드를 포함 하는 클래스 및 해당 메서드 이름이 제공는 `ObjectDataSource` 태그에서 제어 합니다. 포스트백 처리 또는 렌더링 중는 `ObjectDataSource` 지정한는 메서드를 호출 합니다.

기본적인 CRUD 작업을 사용 하면 만든 클래스 외에도 `ObjectDataSource` 컨트롤 비즈니스 논리를 실행 해야 할 수 있습니다 때는 `ObjectDataSource` 읽거나 데이터를 업데이트 합니다. 예를 들어 한 부서를 업데이트할 때 다른 부서에서는 한 사람만 둘 이상의 부서의 관리자 수 없기 때문에 동일한 관리자 권한이 있는지 할 수 있습니다.

일부 `ObjectDataSource` 설명서와 같은 [ObjectDataSource 클래스 개요](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.aspx), 라고 하는 클래스를 호출 하는 컨트롤을 *비즈니스 개체* 비즈니스 논리와 데이터 액세스 논리를 포함 하는 . 이 자습서에서는 데이터 액세스 논리 및 비즈니스 논리에 대 한 별도 클래스를 만듭니다. 데이터 액세스 논리를 캡슐화 하는 클래스 라고는 *리포지토리*합니다. 비즈니스 논리 클래스 비즈니스 논리 메서드 및 데이터 액세스 메서드를 모두 포함 되어 있지만 데이터 액세스 메서드는 데이터 액세스 작업을 수행 하는 저장소를 호출 합니다.

자동화 된 단위를 용이 하 게 DAL 및 BLL 간의 추상화 계층 만들어집니다 BLL의 테스트 합니다. 인터페이스를 만들고 비즈니스 논리 클래스에서 리포지토리를 인스턴스화할 때 인터페이스를 사용 하 여이 추상화 계층 구현 됩니다. 이렇게 하면 비즈니스 논리 클래스 리포지토리 인터페이스를 구현 하는 개체에 대 한 참조로 제공할 수 있습니다. 일반 작업에 대 한 Entity Framework와 함께 사용할 수 있는 저장소 개체를 제공 합니다. 테스트를 위해 컬렉션으로 정의 된 클래스 변수 같은 쉽게 조작할 수 있는 방식으로 저장 된 데이터를 사용 하는 저장소 개체를 제공 합니다.

다음 그림에서는 저장소 없이 데이터 액세스 논리를 포함 하는 비즈니스 논리 클래스 하 고 다른 하나는 저장소 간의 차이 보여 줍니다.

[![Image05](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image1.png)

웹 페이지를 만들어 시작 됩니다는 `ObjectDataSource` 만 기본 데이터 액세스 작업을 수행 하기 때문에 저장소에 직접 바인딩된 컨트롤입니다. 다음 자습서의 비즈니스 논리 클래스 유효성 검사 논리를 만들고 바인딩하는 `ObjectDataSource` 저장소 클래스 대신 해당 클래스를 제어 합니다. 유효성 검사 논리에 대 한 단위 테스트도 만들어집니다. 이 시리즈의 세 번째 자습서에서 정렬 및 필터링 기능을 응용 프로그램을 추가 합니다.

이 자습서에서 만드는 페이지 작업할는 `Departments` 에서 만든 데이터 모델의 엔터티 집합의 [자습서 시리즈 시작](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)합니다.

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image3.png)

[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image5.png)

## <a name="updating-the-database-and-the-data-model"></a>데이터베이스 및 데이터 모델 업데이트

이 자습서를 시작 하는 데이터 모델에서 만든 변경 해야 할 두 데이터베이스에 대 한 두 가지 변경 하 여는 [Entity Framework와 Web Forms 시작](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md) 자습서입니다. 이러한 자습서 중 하나에서 데이터 모델을 데이터베이스와 데이터베이스 변경 후 동기화를 수동으로 디자이너에서 변경이 되었습니다. 이 자습서를 사용 하 여 디자이너의 **데이터베이스에서 모델 업데이트** 데이터 모델을 자동으로 업데이트 하는 도구입니다.

### <a name="adding-a-relationship-to-the-database"></a>관계를 데이터베이스에 추가

Visual Studio에서 만든 Contoso 대학 웹 응용 프로그램을 엽니다는 [Entity Framework와 Web Forms 시작](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md) 자습서 시리즈를 연 후는 `SchoolDiagram` 데이터베이스 다이어그램.

보면는 `Department` 테이블 데이터베이스 다이어그램에 표시 됩니다는 `Administrator` 열입니다. 이 열은 외래 키를는 `Person` 테이블 있지만 외래 키 관계가 없는 데이터베이스에 정의 됩니다. 관계 만들기 및 Entity Framework이이 관계를 자동으로 처리할 수 있도록 데이터 모델을 업데이트 해야 합니다.

데이터베이스 다이어그램에서 마우스 오른쪽 단추로 클릭는 `Department` 테이블을 마우스 선택 **관계**합니다.

[![Image80](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image7.png)

에 **외래 키 관계** 상자 클릭 **추가**에 대 한 줄임표를 클릭 한 다음 **테이블 및 열 사양**합니다.

[![Image81](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image10.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image9.png)

에 **테이블 및 열** 대화 상자, 기본 키 테이블을 설정 및 필드를 `Person` 및 `PersonID`, 외래 키 테이블을 설정 하 고 필드를 `Department` 및 `Administrator`합니다. (관계 이름에서 변경 됩니다. 이렇게 하면 `FK_Department_Department` 를 `FK_Department_Person`.)

[![Image82](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image12.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image11.png)

클릭 **확인** 에 **테이블 및 열** 상자 **닫기** 에 **외래 키 관계** 고 변경 내용을 저장 합니다. 저장할 것인지 묻는 `Person` 및 `Department` 테이블을 클릭 하 여 **예**합니다.

> [!NOTE]
> 삭제 한 경우 `Person` 에 이미 있는 데이터에 해당 하는 행의 `Administrator` 열이 변경이 내용을 저장 하지 못할 수 됩니다. 이 경우에 테이블 편집기를 사용 하 여 **서버 탐색기** 있는지 확인 하기는 `Administrator` 값 모든 `Department` 에 실제로 존재 하는 레코드의 ID를 포함 하는 행의 `Person` 테이블입니다.
> 
> 변경 내용을 저장 한 후 됩니다에서 행을 삭제할 수는 `Person` 테이블에 있으면 해당 사용자가 부서 관리자에 해당 합니다. 프로덕션 응용 프로그램에서는 데이터베이스 제약 조건으로 인해는 삭제 하거나 모두 삭제를 지정 하는 경우 특정 오류 메시지를 제공할 것 있습니다. 연계 delete를 지정 하는 방법의 예제를 보려면 [Entity Framework 및 ASP.NET – 하기 시작 2 부](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-2.md)합니다.


### <a name="adding-a-view-to-the-database"></a>데이터베이스에 뷰를 추가합니다.

새 *Departments.aspx* 사용자가 부서 관리자를 선택할 수 있도록 "성, 이름" 형식에서 이름의 교사, 드롭 다운 목록을 제공 하려는 페이지를 만듭니다. 그렇게 하려면 쉽게 데이터베이스에 뷰를 만들어집니다. 보기 드롭 다운 목록에서 필요한 데이터만으로 구성 됩니다: (형식 제대로) 전체 이름 및 레코드 키입니다.

**서버 탐색기**를 확장 하 고 *School.mdf*를 마우스 오른쪽 단추로 클릭는 **뷰** 폴더를 찾아 선택 **새 뷰 추가**합니다.

[![Image06](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image14.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image13.png)

클릭 **닫기** 때는 **테이블 추가** 대화 상자가 나타나고 다음 SQL 문은 SQL 창에 붙여 넣습니다.

[!code-sql[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample1.sql)]

뷰 저장 `vInstructorName`합니다.

### <a name="updating-the-data-model"></a>데이터 모델 업데이트

에 *DAL* 폴더를 엽니다는 *SchoolModel.edmx* 파일 디자인 화면을 마우스 오른쪽 단추로 클릭 하 고 선택 **데이터베이스에서 모델 업데이트**합니다.

[![Image07](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image16.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image15.png)

에 **데이터베이스 개체 선택** 대화 상자는 **추가** 탭 하 고 방금 만든 보기를 선택 합니다.

[![Image08](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image18.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image17.png)

**마침**을 클릭합니다.

디자이너에서 도구를 만들었음을 표시는 `vInstructorName` 엔터티와 사이 새 연결의 `Department` 및 `Person` 엔터티.

[![Image13](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image20.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image19.png)

> [!NOTE]
> 에 **출력** 및 **오류 목록** 새 도구에 자동으로 기본 생성 없다는 경고 메시지가 표시 될 수 있습니다 windows 키 `vInstructorName` 보기. 이는 예상된 동작입니다.


새 참조 하는 경우 `vInstructorName` 데이터베이스 규칙에 소문자 "v"을 접두사로 사용을 사용 하지 않으려는 코드에서 엔터티를 합니다. 따라서 엔터티 및 모델의 엔터티 집합 이름을 바꿀 됩니다.

열기는 **모델 브라우저**합니다. 표시 `vInstructorName` 뷰와 엔터티 형식으로 나열 합니다.

[![Image14](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image22.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image21.png)

아래 **SchoolModel** (하지 **SchoolModel.Store**)를 마우스 오른쪽 단추로 클릭 **vInstructorName** 선택 **속성**합니다. 에 **속성** 창에서 변경은 **이름** 속성을 변경 하 고 "InstructorName"는 **엔터티 집합 이름** 속성을 "InstructorNames"입니다.

[![Image15](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image24.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image23.png)

저장 하 고 데이터 모델을 닫은 다음 프로젝트를 다시 빌드하십시오.

## <a name="using-a-repository-class-and-an-objectdatasource-control"></a>저장소 클래스와 ObjectDataSource 컨트롤을 사용 하 여

새 클래스 파일을 만듭니다는 *DAL* 폴더를 이름을 *SchoolRepository.cs*, 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample2.cs)]

이 코드는 단일 제공 `GetDepartments` 의 엔터티를 모두 반환 하는 메서드는 `Departments` 엔터티 집합입니다. 사용자 액세스 하 알고 있으므로 `Person` 모든 행에 대해 탐색 속성 반환 지정 eager를 사용 하 여 해당 속성에 대 한 로드는 `Include` 메서드. 또한 구현 하는 클래스는 `IDisposable` 개체가 삭제 될 때 데이터베이스 연결 해제 되도록 하는 인터페이스입니다.

> [!NOTE]
> 일반적으로 각 엔터티 형식에 대 한 저장소 클래스를 만드는 것입니다. 이 자습서에서는 여러 엔터티 형식에 대해 하나의 저장소 클래스를 사용 합니다. 리포지토리 패턴에 대 한 자세한 내용은의 게시물을 참조 하십시오. [Entity Framework 팀 블로그](https://blogs.msdn.com/b/adonet/archive/2009/06/16/using-repository-and-unit-of-work-patterns-with-entity-framework-4-0.aspx) 및 [Julie Lerman 블로그](http://thedatafarm.com/blog/data-access/agile-ef4-repository-part-3-fine-tuning-the-repository/)합니다.


`GetDepartments` 메서드가 반환 되는 `IEnumerable` 개체 아닌 `IQueryable` 리포지토리 개체 자체를 삭제 한 후에 반환된 된 컬렉션을 사용할 수 있도록 하기 위해 개체입니다. `IQueryable` 개체 액세스 하는 번 데이터 바인딩된 컨트롤에서 데이터를 렌더링 하 여 저장소 개체를 삭제할 수 있습니다 때마다 데이터베이스 액세스 될 수 있습니다. 와 같은 다른 컬렉션 형식을 반환할 수 있습니다는 `IList` 개체가 아니라는 `IEnumerable` 개체입니다. 그러나 반환 된 `IEnumerable` 개체를 사용 하면 같은 일반적인 읽기 전용 목록 처리 작업을 수행할 수 `foreach` 루프 및 LINQ 쿼리 있지만에 추가할 수 없습니다 또는 이러한 변경 내용이 것을 의미 하는 컬렉션의 항목을 제거 데이터베이스에 저장 합니다.

만들기는 *Departments.aspx* 페이지를 사용 하 여 *Site.Master* 에 다음 태그를 추가 하 고 마스터 페이지는 `Content` 라는 컨트롤 `Content2`:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample3.aspx)]

이 태그를 만듭니다는 `ObjectDataSource` 방금 만든 저장소 클래스를 사용 하는 컨트롤 및 `GridView` 컨트롤에 데이터를 표시 합니다. `GridView` 컨트롤 지정 **편집** 및 **삭제** 명령을 있지만 아직 지 원하는 코드를 추가 하지 않았습니다.

열이 여러 개 사용 하 여 `DynamicField` 자동 데이터 서식 및 유효성 검사 기능을 사용할 수 있도록 합니다. 이러한 작업에 대 한 호출 해야 합니다는 `EnableDynamicData` 에서 메서드는 `Page_Init` 이벤트 처리기입니다. (`DynamicControl` 컨트롤에서 사용 되지 않습니다는 `Administrator` 필드 이므로 탐색 속성으로 작동 하지 않습니다.)

`Vertical-Align="Top"` 특성 중요 하 게 나중에 중첩 된 열을 추가 하면 `GridView` 표에 제어 합니다.

열기는 *Departments.aspx.cs* 파일을 다음 추가 `using` 문:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample4.cs)]

다음 페이지의에 대 한 다음 처리기를 추가 `Init` 이벤트:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample5.cs)]

에 *DAL* 폴더를 라는 새 클래스 파일을 만들 *Department.cs* 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample6.cs)]

이 코드는 데이터 모델에 메타 데이터를 추가합니다. 갖도록 지정는 `Budget` 의 속성은 `Department` 엔터티는 실제로 통화를 나타내는 해당 데이터 형식이 있지만 `Decimal`, 이며 지정 값 0에서 1000, 000.00 달러 사이 여야 합니다. 또한 지정 하는 `StartDate` mm/dd/yyyy 형식의 날짜 서식 속성을 지정 해야 합니다.

실행 된 *Departments.aspx* 페이지.

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image26.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image25.png)

에 형식 문자열을 지정 하지 않은 되지만 *Departments.aspx* 에 대 한 페이지 태그는 **예산** 또는 **시작 날짜** 열, 기본 통화 및 날짜 적용 된 서식을 `DynamicField` 제어에서 사용자가 입력 하는 메타 데이터를 사용 하 여는 *Department.cs* 파일입니다.

## <a name="adding-insert-and-delete-functionality"></a>추가 삽입 및 삭제 기능

열기 *SchoolRepository.cs*를 만들기 위해 다음 코드를 추가 `Insert` 메서드 및 `Delete` 메서드. 라는 메서드가 코드에도 포함 되어 `GenerateDepartmentID` 에서 사용 하기 위해 다음 레코드를 사용할 수 있는 키 값을 계산 하는 `Insert` 메서드. 데이터베이스에 대해 자동으로이 계산 하도록 구성 되지 않은 때문에 이것이 필요는 `Department` 테이블입니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample7.cs)]

### <a name="the-attach-method"></a>Attach 메서드

`DeleteDepartment` 메서드 호출에서 `Attach` 메서드 메모리에 있는 엔터티의 데이터베이스 간의 개체 컨텍스트의 개체 상태 관리자에서 유지 관리 되는 연결을 다시 설정 하기 위해 행 나타내는 것입니다. 이 메서드 호출 전에 발생 해야는 `SaveChanges` 메서드.

용어 *개체 컨텍스트에* 에서 파생 되는 Entity Framework 클래스를 참조 하는 `ObjectContext` 엔터티 집합과 엔터티 액세스에 사용 하는 클래스입니다. 이 프로젝트에 대 한 코드에서 클래스 이름은 `SchoolEntities`, 해당 형식의 인스턴스는 항상 명명 및 `context`합니다. 개체 컨텍스트의 *개체 상태 관리자* 에서 파생 되는 클래스는 `ObjectStateManager` 클래스입니다. 개체 연락처 개체 상태 관리자를 사용 하 여 엔터티 개체를 저장 하 고 각이 해당 테이블 행 이나 데이터베이스의 행와 동기화 여부를 추적 합니다.

엔터티를 읽을 때 개체 컨텍스트의 개체 상태 관리자에 저장 하 고 개체의 표현을 데이터베이스와 동기화 여부를 추적 합니다. 예를 들어, 속성 값을 변경 하는 경우 플래그는 변경한 속성은 데이터베이스와 동기화 더 이상 임을 나타내기 위해 설정 됩니다. 호출 하면는 `SaveChanges` 메서드를 개체 컨텍스트에 개체 상태 관리자 엔터티의 현재 상태 및 데이터베이스의 상태 간 란 정확히 알기 때문에 데이터베이스에서 수행할 작업을 알고 있습니다.

그러나이 프로세스 일반적으로 작동 하지 않습니다는 웹 응용 프로그램에서 페이지를 렌더링 한 다음 해당 개체 상태 관리자의 모든 항목이 함께 엔터티를 읽을 수 있는 개체 컨텍스트 인스턴스 삭제 되기 때문에. 변경 내용을 적용 해야 하는 개체 컨텍스트 인스턴스를 다시 게시 프로세스에 대 한 인스턴스화될 새로운 것입니다. 경우에 `DeleteDepartment` 메서드를는 `ObjectDataSource` 컨트롤 다시 원래 버전의 엔터티의 드립니다에서 뷰 상태 값을 만들지만 다시 생성 `Department` 엔터티 개체 상태 관리자에 없습니다. 호출 하는 경우는 `DeleteObject` 이 다시 만들어질 엔터티 메서드를 개체 컨텍스트에 엔터티를 데이터베이스와 동기화 하는지 여부를 알지 못하므로 호출이 실패 합니다. 그러나 호출의 `Attach` 메서드를 개체 컨텍스트에의 이전 인스턴스에 엔터티를 읽으면 자동으로 수행 된 원래 데이터베이스에 다시 생성된 되는 엔터티에 값과 동일한 추적을 다시 설정 합니다.

경우가 개체 상태 관리자의 엔터티를 추적 하는 개체 컨텍스트에 않을 시점과 작업을 수행 하지 못하도록 플래그를 설정할 수 있습니다. 이 예제는이 시리즈의 이후의 자습서에 나와 있습니다.

### <a name="the-savechanges-method"></a>SaveChanges 메서드

이 간단한 리포지토리 클래스 CRUD 작업을 수행 하는 방법의 기본 원칙을 보여 줍니다. 이 예제는 `SaveChanges` 메서드는 각 업데이트 후 바로 호출 됩니다. 프로덕션 응용 프로그램에서 호출 하려는 `SaveChanges` 제어할 수 있도록 하면 더 많은 데이터베이스를 업데이트 하는 경우 별도 메서드에서 메서드. (다음 자습서의 끝에 있습니다 관련된 업데이트를 조정 하는 방법 중 하나는 작업 패턴 단위에 설명 하는 백서에 대 한 링크를입니다.) 다음에 유의 예에서 `DeleteDepartment` 메서드는 동시성 충돌을 처리 하기 위한 코드를 포함 하지 않으면이 시리즈의 자습서의 뒷부분에서 작업을 수행 하는 코드가 추가 됩니다.

### <a name="retrieving-instructor-names-to-select-when-inserting"></a>삽입할 때 선택할 강사 이름을 검색 합니다.

사용자가 새 부서를 만들 때 관리자 드롭 다운 목록에서 강사 목록에서 선택할 수 있어야 합니다. 따라서 다음 코드를 추가 *SchoolRepository.cs* 강사 앞에서 만든 보기를 사용 하 여 목록을 검색 하는 메서드를 만듭니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample8.cs)]

### <a name="creating-a-page-for-inserting-departments"></a>부서를 삽입 하기 위한 페이지 만들기

만들기는 *DepartmentsAdd.aspx* 페이지를 사용 하는 *Site.Master* 페이지에 다음 태그를 추가 하 고는 `Content` 라는 컨트롤 `Content2`:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample9.aspx)]

이 태그에서는 두 개의 `ObjectDataSource` 새로운 삽입에 대 한 제어 `Department` 엔터티와 강사 이름에 대 한 검색에 대 한 하나는 `DropDownList` 부서 관리자를 선택 하기 위한 사용 되는 컨트롤입니다. 태그를 만듭니다는 `DetailsView` 컨트롤의에 대 한 처리기를 지정 하며 새 부서를 입력에 대 한 제어 `ItemInserting` 이벤트를 설정할 수 있습니다는 `Administrator` 외래 키 값입니다. 끝에 표시 됩니다는 `ValidationSummary` 컨트롤 오류 메시지를 표시 합니다.

열기 *DepartmentsAdd.aspx.cs* 다음 추가 `using` 문:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample10.cs)]

다음 클래스 변수 및 메서드를 추가 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample11.cs)]

`Page_Init` 메서드 Dynamic Data 기능을 활성화 합니다. 에 대 한 처리기는 `DropDownList` 컨트롤의 `Init` 컨트롤과 대 한 처리기에 대 한 참조를 저장 하는 이벤트는 `DetailsView` 컨트롤의 `Inserting` 을 사용 하 여 참조 하는 이벤트는 `PersonID` 선택한 강사 및 업데이트의 값 `Administrator` 의 외래 키 속성은 `Department` 엔터티.

페이지를 실행, 새 부서에 대 한 정보를 추가 하 고 클릭는 **삽입** 링크 합니다.

[![Image04](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image28.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image27.png)

다른 새 부서에 대 한 값을 입력 합니다. 1000, 000.00 보다 큰 숫자를 입력의 **예산** 필드 및 탭을 다음 필드로 이동 합니다. 필드에 별표를 표시 하 고 위로 마우스 포인터를 놓으면 해당 필드에 대 한 메타 데이터에서 입력 한 오류 메시지를 볼 수 있습니다.

[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image30.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image29.png)

클릭 **삽입**,으로 표시 되는 오류 메시지를 표시 하 고는 `ValidationSummary` 페이지의 맨 아래에 컨트롤입니다.

[![Image12](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image32.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image31.png)

그런 다음 브라우저를 닫고 엽니다는 *Departments.aspx* 페이지. 삭제 기능을 추가 *Departments.aspx* 추가 하 여 페이지는 `DeleteMethod` 특성을 `ObjectDataSource` 컨트롤 및 `DataKeyNames` 특성을 `GridView` 제어 합니다. 이제 이러한 컨트롤에 대 한 여는 태그 다음 예와 비슷하게 표시 됩니다.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample12.aspx)]

페이지를 실행 합니다.

[![Image09](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image34.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image33.png)

삭제를 실행 하면 추가 부서는 *DepartmentsAdd.aspx* 페이지.

## <a name="adding-update-functionality"></a>업데이트 기능 추가

열기 *SchoolRepository.cs* 다음 추가 `Update` 메서드:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample13.cs)]

클릭할 때 **업데이트** 에 *Departments.aspx* 페이지는 `ObjectDataSource` 컨트롤에서는 두 개의 `Department` 에 전달 하는 엔터티는 `UpdateDepartment` 메서드. 뷰 상태에 저장 된 원래 값을 포함 하나에 입력 한 새 값을 포함 하 고는 `GridView` 제어 합니다. 코드는 `UpdateDepartment` 메서드가 전달 된 `Department` 원래 값을 가진 엔터티가 `Attach` 엔터티 및 데이터베이스에 포함 된 내용 간에 추적을 설정 하기 위해 메서드. 다음 코드는 `Department` 새 값을 가진 엔터티가 `ApplyCurrentValues` 메서드. 개체 컨텍스트의 이전 및 새 값을 비교합니다. 새 값을 이전 값과에서 다른 경우 개체 컨텍스트 속성 값을 변경 합니다. `SaveChanges` 메서드는 데이터베이스에서 변경 된 열만을 업데이트 합니다. 그러나 (이 엔터티에 대 한 업데이트 함수, 저장된 프로시저에 매핑된 경우 전체 행 업데이트 됩니다 변경 된 열에 관계 없이.)

열기는 *Departments.aspx* 파일을 다음 특성을 추가 `DepartmentsObjectDataSource` 제어:

- `UpdateMethod="UpdateDepartment"`
- `ConflictDetection="CompareAllValues"`   
 새 값과 비교할 수 있도록 될 원인은 이전 값이 저장 상태 보기에 `Update` 메서드.
- `OldValuesParameterFormatString="orig{0}"`   
 이 통해 원래 값 매개 변수 이름은 컨트롤 알립니다 `origDepartment` 합니다.

여는 태그에 대 한 태그는 `ObjectDataSource` 컨트롤에는 이제 다음 예제와 유사 합니다.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample14.aspx)]

추가 `OnRowUpdating="DepartmentsGridView_RowUpdating"` 특성을 `GridView` 제어 합니다. 설정 하려면이 사용 합니다는 `Administrator` 드롭 다운 목록에서 선택한 행을 기반으로 하는 속성 값입니다. `GridView` 는 다음 예제와 여는 태그 이제:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample15.aspx)]

추가 `EditItemTemplate` 제어 하는 데는 `Administrator` 열에는 `GridView` 후 즉시 제어는 `ItemTemplate` 해당 열에 대 한 제어:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample16.aspx)]

이 `EditItemTemplate` 제어는 비슷합니다는 `InsertItemTemplate` 컨트롤에 *DepartmentsAdd.aspx* 페이지. 차이점은 사용 하 여 컨트롤의 초기 값은 설정 하는 `SelectedValue` 특성입니다.

전에 `GridView` 컨트롤을 추가 `ValidationSummary` 에서 같이 제어는 *DepartmentsAdd.aspx* 페이지.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample17.aspx)]

열기 *Departments.aspx.cs* partial 클래스 선언 바로 뒤를 참조 하는 private 필드를 만들려면 다음 코드를 추가 하 고는 `DropDownList` 제어:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample18.cs)]

다음에 대 한 처리기를 추가 `DropDownList` 컨트롤의 `Init` 이벤트 및 `GridView` 컨트롤의 `RowUpdating` 이벤트:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample19.cs)]

에 대 한 처리기는 `Init` 에 대 한 참조를 저장 하는 이벤트는 `DropDownList` 클래스 필드에서 제어 합니다. 에 대 한 처리기는 `RowUpdating` 이벤트는 참조를 사용 하 여 사용자가 입력 한 값을 가져올를 적용 하는 `Administrator` 의 속성은 `Department` 엔터티.

사용 하 여는 *DepartmentsAdd.aspx* 실행 한 다음 새 부서를 추가 하려면 페이지는 *Departments.aspx* 페이지 클릭 하 여 **편집** 추가한 행에 있습니다.

> [!NOTE]
> 추가 하지 않은 행을 편집할 수 없습니다 (즉, 데이터베이스에 이미 있었던), 데이터베이스;에 잘못 된 데이터로 인해 데이터베이스를 사용 하 여 만든 행에 대 한 관리자 학생 됩니다. 와 같은 오류가 보고 된 오류 페이지를 받아볼 수 그 중 하나를 편집 하려고 하면 `'InstructorsDropDownList' has a SelectedValue which is invalid because it does not exist in the list of items.`


[![Image10](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image36.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image35.png)

잘못 된 입력 하면 **예산** 해석 하 고 클릭 **업데이트**, 동일한 별표 및 오류 메시지에서 본 참조는 *Departments.aspx* 페이지.

필드 값을 변경 하거나 다른 관리자를 선택 하 고, 클릭 **업데이트**합니다. 변경 내용을 표시 됩니다.

[![Image09](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image38.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image37.png)

이 사용 하 여 소개 작업이 완료 되는 `ObjectDataSource` 컨트롤에 대 한 기본적인 CRUD (만들기, 읽기, 업데이트, 삭제) Entity Framework를 사용 하 여 작업 합니다. 간단한 n 계층 응용 프로그램을 작성할 하지만 비즈니스 논리 계층은 자동화 된 단위 테스트 복잡 하 게 하는 데이터 액세스 계층에 여전히 밀접 하 게 결합 됩니다. 다음 자습서에서는 단위 테스트가 용이 하도록 리포지토리 패턴을 구현 하는 방법을 볼 수 있습니다.

> [!div class="step-by-step"]
> [다음](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
