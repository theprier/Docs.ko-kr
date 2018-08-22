---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started
title: 'Entity Framework 4.0 및 ObjectDataSource 컨트롤을 사용 하 여, 파트 1: 시작 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈의 Entity Framework 자습서 시리즈를 사용 하 여 시작 하 여 만든 Contoso University 웹 응용 프로그램 기반으로 합니다. 경우 yo...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: 244278c1-fec8-4255-8a8a-13bde491c4f5
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started
msc.type: authoredcontent
ms.openlocfilehash: 5eaeaa0aa474e1aed86954e6c10dd1703b938944
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41829753"
---
<a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-1-getting-started"></a>Entity Framework 4.0 및 ObjectDataSource 컨트롤을 사용 하 여, 파트 1: 시작
====================
[Tom Dykstra](https://github.com/tdykstra)

> 이 자습서 시리즈에서 만든 Contoso University 웹 응용 프로그램 빌드를 [Entity Framework 4.0을 사용 하 여 시작](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md) 자습서 시리즈입니다. 이전 자습서를 완료 하지 않은 경우이 자습서에 대 한 시작 지점으로 할 수 있습니다 [응용 프로그램을 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) 만들어졌을 것입니다. 할 수도 있습니다 [응용 프로그램을 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) 전체 자습서 시리즈에서 만들어집니다.
> 
> Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 4.0 및 Visual Studio 2010을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 샘플 응용 프로그램은 가상 Contoso University의 웹 사이트입니다. 학생 입학, 강좌 개설 및 강사 할당과 같은 기능이 있습니다.
> 
> 자습서에서 C# 예제를 보여 줍니다. 합니다 [다운로드할 수 있는 샘플](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) C# 및 Visual Basic 코드를 포함 합니다.
> 
> ## <a name="database-first"></a>먼저 데이터베이스
> 
> 세 가지 방법으로 Entity Framework에서 데이터로 작업할 수 있습니다: *Database First*를 *Model First*, 및 *Code First*합니다. Database First에 대 한이 자습서가입니다. 시나리오에 가장 적합 한 선택 하는 방법은 이러한 워크플로 및 지침 간의 차이점에 대 한 정보를 참조 하세요 [Entity Framework 개발 워크플로](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)합니다.
> 
> ## <a name="web-forms"></a>Web Forms
> 
> 입문 시리즈와 같은이 자습서 시리즈는 ASP.NET Web Forms 모델을 사용 하 고 Visual Studio에서 ASP.NET Web Forms를 사용 하는 방법을 알고 있다고 가정 합니다. 를 찾을 수 없으면 [Getting Started with ASP.NET 4.5 Web Forms](../../getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)합니다. ASP.NET MVC 프레임 워크를 사용 하 여 작업 하려는 경우 참조 [Getting Started with ASP.NET MVC를 사용 하 여 Entity Framework](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다.
> 
> ## <a name="software-versions"></a>소프트웨어 버전
> 
> | **자습서에 표시** | **역시** |
> | --- | --- |
> | Windows 7 | Windows 8 |
> | Visual Studio 2010 | Visual Studio 2010 Express for Web입니다. 자습서는 뒷부분에 나오는 버전의 Visual Studio를 사용 하 여 거치지 않았습니다. 메뉴 선택, 대화 상자 및 템플릿에서 다음과 같은 많은 차이가 있습니다. |
> | .NET 4 | .NET 4.5는.NET 4와 역방향 호환이 가능 하지만.NET 4.5를 사용 하 여 자습서를 거치지 않았습니다. |
> | Entity Framework 4 | 자습서는 뒷부분에 나오는 버전의 Entity Framework를 사용 하 여 거치지 않았습니다. Entity Framework 5 부터는 EF는 기본적으로 `DbContext API` 는 EF 4.1에서 도입 되었습니다. EntityDataSource 컨트롤을 사용 하도록 설계 되었습니다는 `ObjectContext` API. 컨트롤의 EntityDataSource를 사용 하는 방법에 대 한 자세한 합니다 `DbContext` API 참조 [이 블로그 게시물](https://blogs.msdn.com/b/webdev/archive/2012/09/13/how-to-use-the-entitydatasource-control-with-entity-framework-code-first.aspx)합니다. |
> 
> ## <a name="questions"></a>질문
> 
> 에 자습서로 직접 관련 되지 않은 질문이 있을 수를 게시할 수 있습니다 합니다 [ASP.NET Entity Framework 포럼](https://forums.asp.net/1227.aspx)서 [Entity Framework 및 LINQ to Entities 포럼](https://social.msdn.microsoft.com/forums/adodotnetentityframework/threads/), 또는 [ StackOverflow.com](http://stackoverflow.com/)합니다.


합니다 `EntityDataSource` 컨트롤을 사용 하면 응용 프로그램을 매우 신속 하 게 만들 수 있지만 일반적으로 필요 상당한 양의 비즈니스 논리 및 데이터 액세스 논리를 유지할 수 있습니다 하 *.aspx* 페이지입니다. 복잡성이 증가 하는 데 필요한 지속적인 유지 관리 응용 프로그램을 원하는 경우 투자할 수 있습니다 더 많은 개발 시간을 미리 만들려면는 *다계층* 하거나 *계층화 된* 응용 프로그램 구조 유지 관리가 더 쉬워집니다. 이 아키텍처를 구현 하려면 비즈니스 논리 계층 (BLL) 및 (DAL)의 데이터 액세스 계층에서 프레젠테이션 계층을 구분 합니다. 이 구조를 구현 하는 한 가지 방법은 사용 하는 것은 `ObjectDataSource` 컨트롤 대신는 `EntityDataSource` 제어 합니다. 사용 하는 경우는 `ObjectDataSource` 컨트롤을 사용자 고유의 데이터 액세스 코드를 구현 하 고 다음에 호출할 *.aspx* 대부분 동일 하는 컨트롤을 사용 하 여 페이지 기능을 다른 데이터 소스 컨트롤입니다. 이렇게 하면 데이터 액세스를 위한 Web Forms 컨트롤을 사용 하는 이점은 n 계층 접근 방식의 장점을 결합할 수 있습니다.

`ObjectDataSource` 컨트롤을 사용 하면 보다 유연 하 게 다른 방식에서입니다. 사용자 고유의 데이터 액세스 코드를 작성 하기 때문에 쉽습니다 수행 이상의 읽기, 삽입, 업데이트 또는 삭제는 특정 엔터티 형식에는 작업을 하는 `EntityDataSource` 컨트롤 수행 하도록 설계 되었습니다. 예를 들어, 엔터티 업데이트 될 때마다 로깅을 수행 하, 엔터티가 삭제 될 때마다 자동으로 확인 하 고 업데이트 관련 데이터를 외래 키 값을 가진 행을 삽입할 때 필요에 따라 데이터를 보관할 수 있습니다.

## <a name="business-logic-and-repository-classes"></a>비즈니스 논리 및 리포지토리 클래스

`ObjectDataSource` 만든 클래스를 호출 하 여 작동을 제어 합니다. 클래스를 검색 하 고 데이터를 업데이트 하는 메서드를 포함 하 고 해당 메서드의 이름을 제공 하는 `ObjectDataSource` 태그에서 제어 합니다. 렌더링 또는 포스트백 처리 하는 동안는 `ObjectDataSource` 지정한 메서드를 호출 합니다.

기본 CRUD 작업을 사용 하기 위해 만든 클래스 외에도 합니다 `ObjectDataSource` 컨트롤 비즈니스 논리를 실행 해야 합니다. 때를 `ObjectDataSource` 읽거나 데이터를 업데이트 합니다. 예를 들어 부서를 업데이트할 때에 없는 다른 학부는 동일한 관리자 두 명 이상의 부서의 관리자 수 없기 때문에 유효성을 검사 해야 합니다.

일부 `ObjectDataSource` 설명서와 같은 합니다 [ObjectDataSource 클래스 개요](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.aspx), 라고 하는 클래스를 호출 하는 컨트롤을 *비즈니스 개체* 비즈니스 논리와 데이터 액세스 논리를 포함 하는 . 이 자습서에서는 데이터 액세스 논리 및 비즈니스 논리에 대 한 별도 클래스를 만듭니다. 데이터 액세스 논리를 캡슐화 하는 클래스에서 호출 되는 *리포지토리*합니다. 비즈니스 논리 클래스가 비즈니스 논리 메서드 및 데이터 액세스 메서드를 모두 포함 하지만 데이터 액세스 메서드를 호출 데이터 액세스 작업을 수행 하는 저장소입니다.

BLL 및 DAL 자동화 된 단위를 원활 하 게 간에 추상화 계층도 만들려는 bll 테스트 합니다. 이 추상화 레이어는 인터페이스를 만들고 비즈니스 논리 클래스에서 리포지토리를 인스턴스화할 때 인터페이스를 사용 하 여 구현 됩니다. 이렇게 하면 리포지토리 인터페이스를 구현 하는 개체에 대 한 참조를 사용 하 여 비즈니스 논리 클래스를 제공할 수 있습니다. 일반 작업에 대 한 Entity Framework와 함께 작동 하는 리포지토리 개체를 제공할 수 있습니다. 테스트에 대 한 컬렉션으로 정의 된 클래스 변수와 같은 쉽게 조작할 수 있는 방식으로 저장 된 데이터를 사용 하 여 작동 하는 리포지토리 개체를 제공할 수 있습니다.

다음 그림에서는 저장소 없이 데이터 액세스 논리를 포함 하는 비즈니스 논리 클래스 및 리포지토리를 사용 하는 것의 차이 보여 줍니다.

[![Image05](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image1.png)

웹 페이지를 만들어 시작 합니다 `ObjectDataSource` 만 기본 데이터 액세스 작업을 수행 하므로 저장소에 직접 바인딩된 컨트롤입니다. 다음 자습서에서 비즈니스 논리 클래스가 유효성 검사 논리를 사용 하 여 만들고 바인딩하는 `ObjectDataSource` 리포지토리 클래스 대신 해당 클래스를 제어 합니다. 유효성 검사 논리에 대 한 단위 테스트도 만듭니다. 이 시리즈의 세 번째 자습서에서 정렬 및 필터링 기능 응용 프로그램에 추가 합니다.

이 자습서에서 만든 페이지를 사용 합니다 `Departments` 에서 만든 데이터 모델의 엔터티 집합을 [자습서 시리즈 시작](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)합니다.

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image3.png)

[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image5.png)

## <a name="updating-the-database-and-the-data-model"></a>데이터베이스 및 데이터 모델 업데이트

이 자습서에서 만든 데이터 모델 변경 해야 할 두 데이터베이스에 대 한 두 가지 변경 하 여 시작 합니다 [Entity Framework 및 Web Forms 시작](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md) 자습서입니다. 이러한 자습서 중 하나에서 데이터베이스 변경 된 후 데이터베이스를 사용 하 여 데이터 모델을 동기화 하려면 수동으로 디자이너에 변경 내용이 있습니다. 이 자습서에서는 디자이너를 사용할지 **데이터베이스에서 모델 업데이트** 데이터 모델을 자동으로 업데이트 하는 도구입니다.

### <a name="adding-a-relationship-to-the-database"></a>데이터베이스 관계 추가

Visual Studio에서에서 만든 Contoso University 웹 응용 프로그램을 엽니다는 [Entity Framework 및 Web Forms를 사용 하 여 시작](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md) 자습서 시리즈를 연 다음의 `SchoolDiagram` 데이터베이스 다이어그램.

보면 합니다 `Department` 테이블 데이터베이스 다이어그램에 표시 됩니다 있는지를 `Administrator` 열입니다. 이 열이 외래 키를 `Person` 테이블 있지만 외래 키 관계가 없는 데이터베이스에 정의 됩니다. 관계 만들기 및 Entity Framework이이 관계를 자동으로 처리할 수 있도록 데이터 모델을 업데이트 해야 합니다.

데이터베이스 다이어그램에서 마우스 오른쪽 단추로 클릭 합니다 `Department` 테이블을 마우스 선택 **관계**합니다.

[![Image80](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image7.png)

에 **Foreign Key Relationships** 상자 **추가**에 대 한 줄임표를 클릭 **테이블 및 열 사양**합니다.

[![Image81](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image10.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image9.png)

에 **테이블 및 열** 대화 상자 기본 키 테이블을 설정 하 고 필드를 `Person` 및 `PersonID`, 및 외래 키 테이블을 설정 하 고 필드를 `Department` 및 `Administrator`합니다. (이렇게 하면 관계 이름에서 변경 됩니다 `FK_Department_Department` 에 `FK_Department_Person`.)

[![Image82](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image12.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image11.png)

클릭 **확인** 에 **테이블 및 열** 상자를 클릭 합니다 **닫기** 에 **외래 키 관계** 상자 하 고 변경 내용을 저장 합니다. 저장 하려는 경우이 요청 되 면 합니다 `Person` 하 고 `Department` 테이블을 **예**합니다.

> [!NOTE]
> 삭제 한 경우 `Person` 에 이미 있는 데이터에 해당 하는 행을 `Administrator` 열 수 없게 됩니다이 변경 내용을 저장 합니다. 이런 경우에 테이블 편집기를 사용 하 여 **서버 탐색기** 되도록 하는 `Administrator` 값 모든 `Department` 에 실제로 존재 하는 레코드의 ID를 포함 하는 행을 `Person` 테이블.
> 
> 변경 내용을 저장 한 후 됩니다의 행을 삭제할 수는 `Person` 사용자는 부서 관리자는 테이블입니다. 프로덕션 응용 프로그램에서는 데이터베이스 제약 조건 삭제를 방지 하거나 계단식 삭제를 지정 하는 경우 특정 오류 메시지를 제공할 것 있습니다. 계단식 삭제를 지정 하는 방법의 예제를 참조 하세요 [Entity Framework 및 ASP.NET – 가져오기 시작 2 부](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-2.md)합니다.


### <a name="adding-a-view-to-the-database"></a>데이터베이스에 뷰 추가

새 *Departments.aspx* 사용자 부서 관리자를 선택할 수 있도록 "성, 이름" 형식에서 이름의 드롭다운 목록이 강사를 제공 하려는 경우를 만들어야 하는 페이지입니다. 이렇게 좀 더 쉽게 데이터베이스에서 뷰를 만들어집니다. 뷰 드롭다운 목록에서 필요한 데이터만으로 구성 됩니다. (서식이) 전체 이름 및 레코드 키입니다.

**서버 탐색기**, 확장 *School.mdf*를 마우스 오른쪽 단추로 클릭 합니다 **뷰** 폴더를 선택한 **새 뷰 추가**합니다.

[![Image06](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image14.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image13.png)

클릭 **닫기** 때 합니다 **테이블 추가** 대화 상자가 나타나고 다음 SQL 문은 SQL 창에 붙여 넣습니다.

[!code-sql[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample1.sql)]

뷰로 저장 `vInstructorName`합니다.

### <a name="updating-the-data-model"></a>데이터 모델 업데이트

에 *DAL* 폴더를 열고 합니다 *SchoolModel.edmx* 파일, 디자인 화면을 마우스 오른쪽 단추로 **데이터베이스에서 모델 업데이트**합니다.

[![Image07](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image16.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image15.png)

에 **데이터베이스 개체 선택** 대화 상자를 선택 합니다 **추가** 탭 하 고 방금 만든 보기를 선택 합니다.

[![Image08](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image18.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image17.png)

**마침**을 클릭합니다.

디자이너에서 생성 된 볼 수는 도구를 `vInstructorName` 엔터티와 간에 새 연결을 합니다 `Department` 및 `Person` 엔터티.

[![Image13](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image20.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image19.png)

> [!NOTE]
> 에 **출력** 하 고 **오류 목록** 새 도구에 자동으로 기본 생성 여부를 알리는 경고 메시지가 표시 될 수 있습니다 windows 키 `vInstructorName` 보기. 이는 예상된 동작입니다.


새 참조 하는 경우 `vInstructorName` 코드에서 엔터티를 하지 않을를 소문자 "v"를 접두사의 데이터베이스 규칙을 사용 합니다. 따라서 엔터티 및 모델의 엔터티 집합 이름을 바꿀가 있습니다.

엽니다는 **브라우저 모델**합니다. 표시 `vInstructorName` 뷰와 엔터티 형식으로 나열 합니다.

[![Image14](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image22.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image21.png)

아래 **SchoolModel** (없습니다 **SchoolModel.Store**)를 마우스 오른쪽 단추로 클릭 **vInstructorName** 선택 **속성**합니다. 에 **속성** 창에서 변경을 **이름** 속성을 변경 하 고 "InstructorName"를 **Entity Set Name** "InstructorNames" 속성입니다.

[![Image15](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image24.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image23.png)

저장 하 고 데이터 모델을 닫은 다음 프로젝트를 다시 빌드하십시오.

## <a name="using-a-repository-class-and-an-objectdatasource-control"></a>저장소 클래스 및 ObjectDataSource 컨트롤을 사용 하 여

새 클래스 파일을 만듭니다는 *DAL* 폴더 이름을 *SchoolRepository.cs*, 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample2.cs)]

이 코드에서는 단일 `GetDepartments` 모두의 엔터티를 반환 하는 메서드는 `Departments` 엔터티 집합입니다. 수에 액세스 하는 것이 알고 있으므로 합니다 `Person` 탐색 속성이 모든 행에 대해 반환 지정할 즉시 사용 하 여 해당 속성에 대 한 로드를 `Include` 메서드. 클래스도 구현 합니다 `IDisposable` 개체가 삭제 될 때 데이터베이스 연결 해제 되도록 하는 인터페이스입니다.

> [!NOTE]
> 일반적인 방법은 각 엔터티 형식에 대 한 리포지토리 클래스를 만드는 것입니다. 이 자습서에서는 여러 엔터티 형식에 대 한 하나의 리포지토리 클래스를 사용 합니다. 리포지토리 패턴에 대 한 자세한 내용은 게시물을 참조 하세요 [Entity Framework 팀의 블로그](https://blogs.msdn.com/b/adonet/archive/2009/06/16/using-repository-and-unit-of-work-patterns-with-entity-framework-4-0.aspx) 하 고 [Julie Lerman의 블로그](http://thedatafarm.com/blog/data-access/agile-ef4-repository-part-3-fine-tuning-the-repository/)합니다.


`GetDepartments` 메서드가 반환 되는 `IEnumerable` 개체 아닌 `IQueryable` 개체 리포지토리 개체 자체를 삭제 한 후에 반환 된 컬렉션에 사용할 수 있도록 합니다. `IQueryable` 개체에 액세스할 때마다 데이터 바인딩된 컨트롤에서 데이터를 렌더링 하려고 하는 시간을 기준으로 리포지토리 개체를 삭제 될 수 있습니다 데이터베이스 액세스 될 수 있습니다. 와 같은 다른 컬렉션 형식을 반환할 수 있습니다는 `IList` 개체 대신는 `IEnumerable` 개체입니다. 그러나 반환를 `IEnumerable` 개체와 같은 일반적인 읽기 전용 목록 처리 작업을 수행할 수 확인 `foreach` 루프 하며 LINQ 쿼리를 추가할 수 없습니다 또는 이러한 변경 내용은 것을 의미 하는 컬렉션에서 항목을 제거 합니다. 데이터베이스에 저장 합니다.

만들기는 *Departments.aspx* 페이지를 사용 하는 *Site.Master* 마스터 페이지, 및에서 다음 태그를 추가 합니다 `Content` 라는 컨트롤 `Content2`:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample3.aspx)]

이 태그를 만듭니다는 `ObjectDataSource` 방금 만든 리포지토리 클래스를 사용 하는 컨트롤 및 `GridView` 컨트롤 데이터를 표시 합니다. `GridView` 컨트롤을 지정 **편집** 하 고 **삭제** 명령을 있지만 아직 지 원하는 코드를 추가 하지 않은 합니다.

열이 여러 개 사용 하 여 `DynamicField` 자동 데이터 서식 지정 및 유효성 검사 기능을 수행할 수 있도록 제어 합니다. 이러한 작업을 호출 해야 합니다 `EnableDynamicData` 에서 메서드는 `Page_Init` 이벤트 처리기입니다. (`DynamicControl` 컨트롤에서 사용 되지 않습니다는 `Administrator` 탐색 속성을 사용 하 여 작동 하지 되므로 필드입니다.)

합니다 `Vertical-Align="Top"` 특성 중요 하 게 나중에 중첩된 된 열을 추가 하면 `GridView` 그리드 컨트롤입니다.

엽니다는 *Departments.aspx.cs* 파일을 추가한 다음 `using` 문:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample4.cs)]

다음 페이지의 처리기를 추가한 `Init` 이벤트:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample5.cs)]

에 *DAL* 폴더를 라는 새 클래스 파일을 만듭니다 *Department.cs* 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample6.cs)]

이 코드는 데이터 모델에 메타 데이터를 추가합니다. 지정는 `Budget` 의 속성을 `Department` 데이터 형식이 있지만 실제로 통화를 나타내는 엔터티 `Decimal`, 값을 0에서 1000 달러, 000.00 사이의 되도록 지정 합니다. 지정 된 `StartDate` mm/dd/yyyy 형식의 날짜로 속성의 서식을 지정 합니다.

실행 합니다 *Departments.aspx* 페이지입니다.

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image26.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image25.png)

형식 문자열을 지정 하지 않은 되었지만 *Departments.aspx* 에 대 한 페이지 태그는 **예산** 또는 **시작 날짜** 통화 및 날짜 열을 기본 서식 지정을 적용 합니다 `DynamicField` 컨트롤에 제공 된 메타 데이터를 사용 하 여 합니다 *Department.cs* 파일.

## <a name="adding-insert-and-delete-functionality"></a>추가 삽입 및 삭제 기능

오픈 *SchoolRepository.cs*를 만들기 위해 다음 코드를 추가 `Insert` 메서드 및 `Delete` 메서드. 코드에는 또한 라는 메서드 `GenerateDepartmentID` 사용에 대 한 다음 사용 가능한 레코드 키 값을 계산 하는 `Insert` 메서드. 데이터베이스에 대해 자동으로이 계산 하도록 구성 되지 않은 때문에 이것이 필요 합니다 `Department` 테이블입니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample7.cs)]

### <a name="the-attach-method"></a>Attach 메서드

합니다 `DeleteDepartment` 메서드 호출을 `Attach` 메모리에서 엔터티 및 데이터베이스 간의 개체 컨텍스트의 개체 상태 관리자에서 유지 관리 되는 연결을 다시 설정 하기 위해 메서드를 나타냅니다가 행 합니다. 메서드 호출 앞에 있어야이 `SaveChanges` 메서드.

용어 *개체 컨텍스트에* 에서 파생 되는 Entity Framework 클래스를 참조는 `ObjectContext` 엔터티 및 엔터티 집합에 액세스 하는 데 사용할 클래스입니다. 이 프로젝트에 대 한 코드에서 클래스 이름은 `SchoolEntities`, 인스턴스 이름은 항상 및 `context`합니다. 개체 컨텍스트의 *개체 상태 관리자* 에서 파생 된 클래스는 `ObjectStateManager` 클래스입니다. 개체 연락처 엔터티 개체를 저장 하 고 각각 해당 테이블 행 이나 행에서 데이터베이스와 동기화 되어 있는지 여부를 추적 하는 개체 상태 관리자를 사용 합니다.

엔터티를 읽을 때 개체 컨텍스트에 개체 상태 관리자에 저장 하 고 개체의 해당 표현은 데이터베이스와 동기화 여부를 추적 합니다. 예를 들어 속성 값을 변경한 경우 플래그는 변경한 속성은 데이터베이스와 동기화 이상 임을 설정 됩니다. 다음 호출 하는 경우는 `SaveChanges` 메서드를 개체 컨텍스트에 개체 상태 관리자 엔터티의 현재 상태와 데이터베이스의 상태 간에 다른 란 정확히 알고 있기 때문에 데이터베이스를 위해 인식할 수 있습니다.

그러나이 프로세스 일반적으로 작동 하지 않습니다 웹 응용 프로그램에서 해당 개체 상태 관리자의 모든 항목이 함께 엔터티를 읽는 개체 컨텍스트 인스턴스 페이지를 렌더링 한 후 삭제 됩니다. 변경 내용을 적용 해야 하는 개체 컨텍스트 인스턴스 새로 포스트백 처리를 위해 인스턴스화되는 경우 경우는 `DeleteDepartment` 메서드를 `ObjectDataSource` 컨트롤 다시 원래 버전의 엔터티를 보기에 상태 값에서 만들지만이 다시 생성 `Department` 엔터티 개체 상태 관리자에 존재 하지 않습니다. 호출 하면는 `DeleteObject` 다시 생성된이 엔터티에 대해 메서드를 개체 컨텍스트에 엔터티 데이터베이스와 동기화 되어 있는지 여부를 알지 못하므로 호출이 실패 합니다. 그러나 호출 된 `Attach` 메서드 이전 인스턴스의 개체 컨텍스트에 엔터티를 읽을 때 자동으로 수행 된 원래 데이터베이스에 다시 만들어진된 엔터티 값과 동일한 추적을 다시 설정 합니다.

개체 컨텍스트의 개체 상태 관리자에서 엔터티를 추적 하지 않으려면 그렇게 하지 못하도록 하는 플래그를 설정할 수 있습니다 시점과 경우가 있습니다. 이 예제는이 시리즈의 뒷부분에 나오는 자습서에 표시 됩니다.

### <a name="the-savechanges-method"></a>SaveChanges 메서드

이 간단한 리포지토리 클래스 CRUD 작업을 수행 하는 방법의 기본 원칙을 보여 줍니다. 이 예제는 `SaveChanges` 각 업데이트 직후 호출 됩니다. 프로덕션 응용 프로그램에서 호출 하려는 `SaveChanges` 메서드에서 별도 메서드를 통해 데이터베이스 업데이트 될 때 제어할 수 있습니다. (다음 자습서의 끝에 있습니다 관련된 업데이트를 조정 하는 방법 중 하나는 작업 패턴 단위에 설명 하는 백서에 대 한 링크를입니다.) 또한 예에서 `DeleteDepartment` 메서드는 동시성 충돌 처리에 대 한 코드를 포함 하지 않으면이 시리즈의 자습서의 뒷부분에서 작업을 수행 하는 코드가 추가 됩니다.

### <a name="retrieving-instructor-names-to-select-when-inserting"></a>강사 이름을 삽입 하는 경우 선택 검색

사용자는 새 부서를 만들 때 관리자 드롭 다운 목록에서 강사 목록을 선택할 수 있어야 합니다. 따라서 다음 코드를 추가 합니다 *SchoolRepository.cs* 앞에서 만든 보기를 사용 하 여 강사 목록을 검색 하는 메서드를 만들려면:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample8.cs)]

### <a name="creating-a-page-for-inserting-departments"></a>부서를 삽입 하기 위한 페이지 만들기

만들기를 *DepartmentsAdd.aspx* 페이지를 사용 하는 *Site.Master* 페이지에서 다음 태그를 추가 및 합니다 `Content` 라는 컨트롤 `Content2`:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample9.aspx)]

이 태그 두 개를 만듭니다 `ObjectDataSource` 새 삽입에 대 한 제어 `Department` 엔터티와 강사 이름을 검색 하기 위한 하나는 `DropDownList` 부서 관리자를 선택할 때 사용 되는 컨트롤입니다. 태그 만듭니다는 `DetailsView` 컨트롤에 대 한 처리기를 지정 하며 새 부서를 입력에 대 한 제어 `ItemInserting` 이벤트 설정할 수 있도록는 `Administrator` 외래 키 값입니다. 끝에는 `ValidationSummary` 오류 메시지를 표시 하는 컨트롤입니다.

오픈 *DepartmentsAdd.aspx.cs* 추가한 다음 `using` 문:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample10.cs)]

다음 클래스 변수 및 메서드를 추가 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample11.cs)]

`Page_Init` 메서드 Dynamic Data 기능을 활성화 합니다. 에 대 한 처리기를 `DropDownList` 컨트롤의 `Init` 이벤트에 대 한 처리기를 컨트롤에 대 한 참조를 저장 합니다 `DetailsView` 컨트롤의 `Inserting` 이벤트 해당 참조를 사용 하 여 가져옵니다는 `PersonID` 값이 선택한 강사 및 업데이트 합니다 `Administrator` 의 외래 키 속성은 `Department` 엔터티.

페이지 실행을 새 부서에 대 한 정보를 추가 하 고 클릭 합니다 **삽입** 링크 합니다.

[![Image04](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image28.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image27.png)

다른 새 학과 대 한 값을 입력 합니다. 1000, 000.00 보다 큰 숫자를 입력 합니다 **예산** 필드 및 다음 필드를 탭 합니다. 필드에 별표를 표시 하 고 위로 마우스 포인터를 놓으면 해당 필드에 대 한 메타 데이터에서 입력 한 오류 메시지를 볼 수 있습니다.

[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image30.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image29.png)

클릭 **삽입**에서 표시 되는 오류 메시지를 표시 하 고는 `ValidationSummary` 페이지의 맨 위에 있는 컨트롤입니다.

[![Image12](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image32.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image31.png)

그런 다음 브라우저를 닫고 엽니다는 *Departments.aspx* 페이지입니다. 삭제 기능을 추가 합니다 *Departments.aspx* 추가 하 여 페이지를 `DeleteMethod` 특성을 `ObjectDataSource` 컨트롤 및 `DataKeyNames` 특성을 `GridView` 컨트롤. 이러한 컨트롤에 대 한 태그는 이제 다음 예와 유사 합니다.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample12.aspx)]

페이지를 실행 합니다.

[![Image09](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image34.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image33.png)

실행할 때 추가한 부서를 삭제 합니다 *DepartmentsAdd.aspx* 페이지입니다.

## <a name="adding-update-functionality"></a>업데이트 기능 추가

오픈 *SchoolRepository.cs* 추가한 다음 `Update` 메서드:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample13.cs)]

클릭 하면 **업데이트** 에 *Departments.aspx* 페이지를 `ObjectDataSource` 컨트롤 두 개를 만듭니다 `Department` 전달할 엔터티는 `UpdateDepartment` 메서드. 뷰 상태에 저장 된 원래 값을 포함 하 고에 입력 한 새 값을 포함 합니다 `GridView` 제어 합니다. 코드를 `UpdateDepartment` 메서드가 전달 합니다 `Department` 에 원래 값이 있는 엔터티는 `Attach` 엔터티 및 데이터베이스의 새로운 기능 간에 추적을 설정 하기 위해 메서드. 코드를 전달 합니다 `Department` 에 새 값이 있는 엔터티는 `ApplyCurrentValues` 메서드. 개체 컨텍스트는 이전 및 새 값을 비교합니다. 새 값을 이전 값에서 다른 경우 개체 컨텍스트 속성 값을 변경 합니다. `SaveChanges` 메서드는 다음 데이터베이스에서 변경 된 열만 업데이트 합니다. 그러나 (이 엔터티에 대 한 업데이트 함수 된 저장된 프로시저에 매핑된 경우 전체 행을 업데이트 됩니다에 관계 없이 열 변경 되었습니다.)

엽니다는 *Departments.aspx* 파일을 다음과 같은 특성을 추가 합니다 `DepartmentsObjectDataSource` 컨트롤:

- `UpdateMethod="UpdateDepartment"`
- `ConflictDetection="CompareAllValues"`   
 새 값과 비교할 수 있도록이 원인 이전 값을 저장 상태 보기에 `Update` 메서드.
- `OldValuesParameterFormatString="orig{0}"`   
 원래 값 매개 변수 이름은 컨트롤에 알립니다. `origDepartment` 합니다.

여는 태그에 대 한 태그는 `ObjectDataSource` 컨트롤에는 이제 다음 예제와 유사 합니다.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample14.aspx)]

추가 된 `OnRowUpdating="DepartmentsGridView_RowUpdating"` 특성을 `GridView` 컨트롤입니다. 설정 하려면이 사용할지는 `Administrator` 드롭 다운 목록에서 선택할 행을 기반으로 하는 속성 값입니다. `GridView` 다음 예제와 유사한 이제 여는 태그:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample15.aspx)]

추가 `EditItemTemplate` 제어 하는 데는 `Administrator` 열을 `GridView` 컨트롤을 즉시는 `ItemTemplate` 해당 열에 대 한 제어:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample16.aspx)]

이 `EditItemTemplate` 제어는 비슷합니다는 `InsertItemTemplate` 에서 제어 합니다 *DepartmentsAdd.aspx* 페이지. 차이점은 컨트롤의 초기 값을 사용 하 여이 설정 되어 있는지를 `SelectedValue` 특성입니다.

전에 `GridView` 컨트롤에 추가 합니다는 `ValidationSummary` 에서 같이 제어를 *DepartmentsAdd.aspx* 페이지입니다.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample17.aspx)]

오픈 *Departments.aspx.cs* partial 클래스 선언 바로 뒤를 참조 하는 개인 필드를 만들려면 다음 코드를 추가 하 고는 `DropDownList` 제어:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample18.cs)]

다음에 대 한 처리기를 추가 합니다 `DropDownList` 컨트롤의 `Init` 이벤트와 `GridView` 컨트롤의 `RowUpdating` 이벤트:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample19.cs)]

에 대 한 처리기를 `Init` 이벤트에 대 한 참조를 저장 합니다 `DropDownList` 클래스 필드의 컨트롤입니다. 에 대 한 처리기를 `RowUpdating` 이벤트는 참조를 사용 하 여 사용자가 입력 한 값을 얻으려면를 적용 하는 `Administrator` 의 속성을 `Department` 엔터티.

사용 하 여는 *DepartmentsAdd.aspx* 새 학과 추가 하려면 페이지를 실행 합니다 *Departments.aspx* 페이지를 클릭 **편집** 추가한 행입니다.

> [!NOTE]
> 추가 하지 않은 행을 편집할 수 없습니다 (즉, 데이터베이스에 이미 있었던), 데이터베이스에서 잘못 된 데이터로 인해 데이터베이스를 사용 하 여 생성 된 행에 대 한 관리자는 학생. 그 중 하나를 편집 하려고 하면 같은 오류가 보고 된 오류 페이지가 표시 됩니다. `'InstructorsDropDownList' has a SelectedValue which is invalid because it does not exist in the list of items.`


[![Image10](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image36.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image35.png)

잘못 된 입력 하면 **예산** amount 및 클릭 **업데이트**, 동일한 별표와의 오류 메시지를 표시 합니다 *Departments.aspx* 페이지.

필드 값을 변경 하거나 다른 관리자를 선택 하 고, 클릭 **업데이트**합니다. 변경 내용이 표시 됩니다.

[![Image09](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image38.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image37.png)

사용 하 여에 대 한 소개를 완료를 `ObjectDataSource` 컨트롤에 대 한 기본 CRUD (만들기, 읽기, 업데이트, 삭제) Entity Framework를 사용 하 여 작업 합니다. 간단한 n 계층 응용 프로그램을 구축 했으므로 하지만 비즈니스 논리 계층은 여전히 밀접 하 게 데이터 액세스 계층을 자동화 된 단위 테스트를 까다롭게 합니다. 다음 자습서의 단위 테스트를 용이 하 게 리포지토리 패턴을 구현 하는 방법을 배웁니다.

> [!div class="step-by-step"]
> [다음](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
