---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-2
title: 먼저 Entity Framework 4.0 Database를 사용 하 여 시작 및 ASP.NET 4 Web Forms-2 부 | Microsoft Docs
author: tdykstra
description: Contoso University 샘플 웹 응용 프로그램에는 Entity Framework를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 샘플 응용 프로그램은...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: fb63a326-a4ae-4b0c-a4f5-412327197216
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-2
msc.type: authoredcontent
ms.openlocfilehash: a0b4acca93deee4fb514fa1bc3e2bd13490cf10e
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41837667"
---
<a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-2"></a>먼저 Entity Framework 4.0 Database를 사용 하 여 시작 및 ASP.NET 4 Web Forms-2 부
====================
[Tom Dykstra](https://github.com/tdykstra)

> Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 4.0 및 Visual Studio 2010을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대 한 정보를 참조 하세요. [시리즈의 첫 번째 자습서](the-entity-framework-and-aspnet-getting-started-part-1.md)


## <a name="the-entitydatasource-control"></a>EntityDataSource 컨트롤

이전 자습서에서 웹 사이트, 데이터베이스 및 데이터 모델을 만들었습니다. 이 자습서에서 사용 하 여 작업을 `EntityDataSource` ASP.NET Entity Framework 데이터 모델을 작업할 수 있도록 하기 위해 제공 하는 컨트롤입니다. 만든를 `GridView` 학생 데이터 표시 및 편집에 대 한 제어를 `DetailsView` 새 학생을 추가 하는 것에 대 한 제어 및 `DropDownList` (나중에 사용할 관련된 과정을 표시 하기 위한)는 부서를 선택 하는 컨트롤입니다.

[![Image20](the-entity-framework-and-aspnet-getting-started-part-2/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image1.png)

[![Image09](the-entity-framework-and-aspnet-getting-started-part-2/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image3.png)

[![Image18](the-entity-framework-and-aspnet-getting-started-part-2/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image5.png)

이 응용 프로그램에서 있습니다 없습니다 입력된 유효성 검사를 추가할 데이터베이스를 업데이트 하는 페이지를 프로덕션 응용 프로그램에 필요한 대로 강력한 됩니다 오류 처리의 일부 note 합니다. Entity Framework에 초점을 맞춘이 자습서를 계속을 너무 길어져서에서 유지 합니다. 응용 프로그램에 이러한 기능을 추가 하는 방법에 대 한 자세한 내용은 참조 하세요 [ASP.NET 웹 페이지에서 사용자 입력 유효성 검사](https://msdn.microsoft.com/library/7kh55542.aspx) 하 고 [ASP.NET 페이지 및 응용 프로그램의 오류 처리](https://msdn.microsoft.com/library/w16865z6.aspx)합니다.

## <a name="adding-and-configuring-the-entitydatasource-control"></a>EntityDataSource 컨트롤 추가 및 구성

구성 하 여 먼저를 `EntityDataSource` 읽을 컨트롤 `Person` 엔터티는 `People` 엔터티 집합입니다.

Visual Studio가 열려 있는 있는지 확인 하 고 1 부에서 만든 프로젝트를 사용 하 여 작업할 합니다. 에 대 한 마지막 변경 이후 또는 데이터 모델을 만든 후 프로젝트를 빌드한 하지 않은 경우 이제 프로젝트를 빌드하십시오. 데이터 모델에 대 한 변경 내용은 사용할 수 없습니다 디자이너에는 프로젝트가 빌드될 때까지 합니다.

사용 하 여 새 웹 페이지의 **웹 폼 마스터 페이지를 사용 하 여** 템플릿을 하 고 이름을 *Students.aspx*합니다.

[![Image23](the-entity-framework-and-aspnet-getting-started-part-2/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image7.png)

지정할 *Site.Master* 마스터 페이지입니다. 이 자습서에 대 한 만들기 페이지의 모든이 마스터 페이지를 사용 합니다.

[![Image24](the-entity-framework-and-aspnet-getting-started-part-2/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image9.png)

**소스** 보기, 추가 `h2` 제목에 `Content` 라는 컨트롤 `Content2`다음 예제에서와 같이:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample1.aspx)]

**데이터** 탭을 **도구 상자**을 끌어는 `EntityDataSource` 컨트롤을 페이지 머리글 아래에 놓습니다 하 고 ID를 변경 `StudentsEntityDataSource`:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample2.aspx)]

전환할 **디자인** 보기, 데이터 소스 컨트롤의 스마트 태그를 클릭 한 다음 클릭 **데이터 소스 구성** 시작 하는 **데이터 소스 구성** 마법사.

[![Image01](the-entity-framework-and-aspnet-getting-started-part-2/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image11.png)

에 **ObjectContext 구성** 마법사 단계 **SchoolEntities** 값으로 **명명 된 연결**를 선택한 **SchoolEntities**으로 **DefaultContainerName** 값입니다. **다음**을 클릭합니다.

[![Image02](the-entity-framework-and-aspnet-getting-started-part-2/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image13.png)

참고:이 시점에서 다음 대화 상자를 표시 하는 경우 해야 계속 진행 하기 전에 프로젝트를 빌드합니다.

[![Image25](the-entity-framework-and-aspnet-getting-started-part-2/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image15.png)

에 **데이터 선택 구성** 단계 선택 **사람** 값으로 **EntitySetName**합니다. 아래 **선택**, 있는지 확인 합니다 **선택** ll 확인란을 선택 합니다. 업데이트 설정 및 삭제 하 고 옵션을 선택 합니다. 완료 되 면 **완료**합니다.

[![Image03](the-entity-framework-and-aspnet-getting-started-part-2/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image17.png)

## <a name="configuring-database-rules-to-allow-deletion"></a>데이터베이스 삭제를 허용 하는 규칙 구성

사용자의 학생 들을 삭제할 수 있는 페이지를 만들 합니다 `Person` 세 가지 다른 테이블과 관계가 있는 테이블 (`Course`, `StudentGrade`, 및 `OfficeAssignment`). 기본적으로 데이터베이스 못합니다 수의 행을 삭제 `Person` 관련된 행에 대 한 다른 테이블의 경우. 관련된 행을 먼저 삭제 수동으로 또는 삭제 하는 경우 자동으로 삭제 하려면 데이터베이스를 구성할 수는 `Person` 행입니다. 이 자습서에서는 학생 레코드에 대 한 관련된 데이터를 자동으로 삭제할 데이터베이스를 구성 합니다. 학생에 게는 관련 행 수 있으므로 에서만 `StudentGrade` 세 관계 중 하나만 구성 해야 하는 테이블입니다.

사용 중인 경우는 *School.mdf* 이 자습서를 사용 하 여 이동 하는 프로젝트에서 다운로드 한 파일에 이러한 구성 변경 내용을 수행한 이미 있으므로이 섹션을 건너뛸 수 있습니다. 스크립트를 실행 하 여 데이터베이스를 만든 경우 다음 절차를 수행 하 여 데이터베이스를 구성 합니다.

**서버 탐색기**, 1 부에서 만든 데이터베이스 다이어그램을 엽니다. 간의 관계를 마우스 오른쪽 단추로 클릭 `Person` 하 고 `StudentGrade` (테이블 사이의 선)를 선택한 후 **속성**합니다.

[![Image04](the-entity-framework-and-aspnet-getting-started-part-2/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image19.png)

에 **속성** 창 확장 **INSERT 및 UPDATE 사양** 설정 하 고는 **DeleteRule** 속성을 **Cascade**.

[![Image05](the-entity-framework-and-aspnet-getting-started-part-2/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image21.png)

저장 하 고 다이어그램을 닫습니다. 데이터베이스를 업데이트 하는 것인지 클릭 묻는 **예**합니다.

모델 유지 동기화 데이터베이스 수행 하는 메모리에 있는 엔터티는 했는지를 데이터 모델의 해당 규칙을 설정 해야 합니다. 열기 *SchoolModel.edmx*, 간에 연결 선을 마우스 오른쪽 단추로 클릭 `Person` 하 고 `StudentGrade`를 선택한 후 **속성**합니다.

[![Image21](the-entity-framework-and-aspnet-getting-started-part-2/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image23.png)

에 **속성** 창에서 **End1 OnDelete** 에 **Cascade**.

[![Image22](the-entity-framework-and-aspnet-getting-started-part-2/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image25.png)

저장 후 닫기 합니다 *SchoolModel.edmx* 파일과 프로젝트를 다시 빌드합니다.

일반적으로 데이터베이스 변경 되 면 몇 가지 옵션이 있습니다 모델을 동기화 하는 방법에 대 한 합니다.

- 특정 종류의 변경은 (예: 추가 하거나 테이블, 뷰 또는 저장된 프로시저를 새로 고침)를 마우스 오른쪽 단추로 클릭는 디자이너 및 선택 **데이터베이스에서 모델 업데이트** 디자이너 make 변경 내용을 자동으로 있어야 합니다.
- 데이터 모델을 다시 생성 합니다.
- 이 이와 같은 수동 업데이트를 확인 합니다.

다시 필드 이름을 변경 해야 하는 다음 다시 모델 생성 또는 관계 변경의 영향을 받는 테이블을 새로 고칠 수 있지만 경우 (에서 `FirstName` 에 `FirstMidName`).

## <a name="using-a-gridview-control-to-read-and-update-entities"></a>GridView 컨트롤을 사용 하 여 읽기 및 엔터티를 업데이트 합니다.

이 섹션에서는 `GridView` 표시, 업데이트 또는 학생을 삭제 하는 컨트롤입니다.

열거나 전환할 *Students.aspx* 으로 전환 **디자인** 보기. **데이터** 탭 합니다 **도구 상자**, 끌어를 `GridView` 컨트롤의 오른쪽에는 `EntityDataSource` 제어 하 고 이름을 `StudentsGridView`, 스마트 태그를 클릭 하 고 선택한  **StudentsEntityDataSource** 데이터 원본으로 합니다.

[![Image06](the-entity-framework-and-aspnet-getting-started-part-2/_static/image28.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image27.png)

클릭 **스키마 새로 고침** (클릭 **예** 것인지 묻는)를 클릭 한 다음 **페이징 사용**를 **정렬 사용**를 **편집 사용**, 및 **삭제 사용**합니다.

클릭 **열을 편집할**합니다.

[![Image10](the-entity-framework-and-aspnet-getting-started-part-2/_static/image30.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image29.png)

에 **선택한 필드** 상자에서 삭제 **PersonID**를 **LastName**, 및 **HireDate**합니다. 일반적으로 사용자에 게 레코드 키를 표시 안 함, 고용 날짜는 관련이 없습니다 학생 및만 이름 필드 중 하나가 필요 하므로 두 부분 이름 하나의 필드에 배치 합니다.)

[![Image11](the-entity-framework-and-aspnet-getting-started-part-2/_static/image32.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image31.png)

선택 된 **FirstMidName** 필드를 클릭 한 다음 **이 필드를 TemplateField로 변환**합니다.

에 대 한 동일한 작업을 수행할 **EnrollmentDate**합니다.

[![Image13](the-entity-framework-and-aspnet-getting-started-part-2/_static/image34.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image33.png)

클릭 **확인** 한 다음으로 전환 **원본** 보기. 나머지 변경 내용을 태그에서 직접 작업을 수행 하기가 됩니다. `GridView` 다음 예와 같이 태그 이제 같습니다를 제어 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample3.aspx)]

명령 필드 템플릿을 필드를 현재 되 면 첫 번째 열 이름을 표시 합니다. 다음 예제와 같이이 서식 파일 필드에 대 한 태그를 변경 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample4.aspx)]

디스플레이 모드에 두 `Label` 컨트롤의 첫 번째 및 마지막 이름을 표시 합니다. 편집 모드에 두 개의 텍스트 상자에 성과 이름을 변경할 수 있도록 제공 됩니다. 와 마찬가지로 합니다 `Label` 컨트롤의 디스플레이 모드를 사용 합니다 `Bind` 및 `Eval` 데이터베이스에 직접 연결 하는 ASP.NET 데이터 소스 컨트롤을 사용 하 여 식 대로 정확 하 게 됩니다. 유일한 차이점은 데이터베이스 열 대신 엔터티 속성을 지정 하는 합니다.

마지막 열에는 등록 날짜를 표시 하는 템플릿 필드입니다. 다음 예제와 같이이 필드에 대 한 태그를 변경 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample5.aspx)]

모두 표시 하 고 모드 편집 형식 문자열 "{0, d}" 날짜 "간단한 날짜" 형식으로 표시를 사용 하면 됩니다. (이 자습서에 표시 된 화면 이미지에서 다르게 형식이으로 표시 하려면 시스템을 구성할 수 있습니다.)

이러한 템플릿 필드의 각 디자이너를 사용 하는 `Bind` 변경한 수 있지만 기본적으로 식에는 `Eval` 식에는 `ItemTemplate` 요소. 합니다 `Bind` 식의 데이터에 사용할 수 있도록 `GridView` 코드에서 데이터에 액세스 해야 하는 경우 속성을 제어 합니다. 이 페이지에서 사용할 수 있도록 코드에서이 데이터에 액세스할 필요가 `Eval`를 더 효율적입니다. 자세한 내용은 [데이터 컨트롤에서 데이터를 가져오는](https://weblogs.asp.net/davidfowler/archive/2008/12/12/getting-your-data-out-of-the-data-controls.aspx)합니다.

## <a name="revising-entitydatasource-control-markup-to-improve-performance"></a>성능 향상을 위해 EntityDataSource 컨트롤 태그를 수정 합니다.

태그에는 `EntityDataSource` 컨트롤을 제거 합니다 `ConnectionString` 및 `DefaultContainerName` 특성 및 바꿀를 `ContextTypeName="ContosoUniversity.DAL.SchoolEntities"` 특성입니다. 이 만들 때마다 해야 변경은 `EntityDataSource` 개체 컨텍스트 클래스에서 하드 코딩 된 것과에서 다른 연결을 사용 하려면 필요 하지 않은 경우를 제어 합니다. 사용 하는 `ContextTypeName` 특성은 다음과 같은 이점을 제공 합니다.

- 성능 향상. 경우는 `EntityDataSource` 제어를 사용 하 여 데이터 모델을 초기화 합니다 `ConnectionString` 및 `DefaultContainerName` 특성인 모든 요청에 대 한 메타 데이터를 로드 하기 위해 추가 작업 수행 합니다. 지정 하는 경우에 필요 하지 않습니다는 `ContextTypeName` 특성입니다.
- 생성 된 개체 컨텍스트 클래스에는 기본적으로 지연 로딩 상태에서 (같은 `SchoolEntities` 이 자습서에서는) Entity Framework 4.0에서 합니다. 이 탐색 속성은 로드 관련된 데이터를 사용 하 여 자동으로 필요할 때 바로 것을 의미 합니다. 지연 로드는이 자습서의 뒷부분에서 자세히 설명 합니다.
- 개체 컨텍스트 클래스에 적용 한 모든 사용자 지정 (이 경우에 `SchoolEntities` 클래스)를 사용 하는 컨트롤에 사용할 수는 `EntityDataSource` 제어 합니다. 개체 컨텍스트 클래스를 사용자 지정 하는 것은이 자습서 시리즈에서 다루지 않는 고급 항목입니다. 자세한 내용은 [Entity Framework 생성 형식 확장](https://msdn.microsoft.com/library/dd456844.aspx)합니다.

태그는 이제 다음 예와 유사 합니다 (속성의 순서는 다른 수 있음):

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample6.aspx)]

`EnableFlattening` 특성이 있는 외래 키 열 된 엔터티 속성으로 노출 되지 않으므로 이전 버전의 Entity Framework에 필요한 기능을 참조 합니다. 현재 버전을 사용 하면 사용할 수 *외래 키 연결*를 제외한 모든 다 대 다 연결에 대 한 노출 된 외래 키 속성 의미 합니다. 엔터티에 외래 키 속성 및 없는 경우 [복합 형식](https://msdn.microsoft.com/library/bb738472.aspx)로이 특성을 두면 `False`. 기본값 이므로 태그에서 특성을 제거 하지 `True`합니다. 자세한 내용은 [평면화 개체 (EntityDataSource)](https://msdn.microsoft.com/library/ee404746.aspx)합니다.

페이지를 실행 하 고 학생과 직원 (필터링만 학생을 위한 다음 자습서에서)의 목록을 표시 합니다. 첫 번째 이름과 마지막 이름 함께 표시 됩니다.

[![Image07](the-entity-framework-and-aspnet-getting-started-part-2/_static/image36.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image35.png)

표시를 정렬 하려면 열 이름을 클릭 합니다.

클릭 **편집** 모든 행에 있습니다. 텍스트 상자에 첫 번째 및 마지막 이름을 변경할 수 있는 표시 됩니다.

[![Image08](the-entity-framework-and-aspnet-getting-started-part-2/_static/image38.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image37.png)

합니다 **삭제** 단추가 작동 합니다. 등록 날짜를 행에 대 한 삭제를 클릭 하 고 행 사라집니다. (등록 날짜 없이 행 나타내는 강사 및 참조 무결성 오류가 발생할 수 있습니다. 다음 자습서에서에서는이 목록을 필터링 할 뿐 학생을 포함 하도록 합니다.)

## <a name="displaying-data-from-a-navigation-property"></a>탐색 속성에서 데이터를 표시합니다.

이제 얼마나 많은 분야의 교육 알아야 한다고 가정 합시다 각 학생에 등록 됩니다. Entity Framework에서 해당 정보를 제공 합니다 `StudentGrades` 의 탐색 속성은 `Person` 엔터티. 데이터베이스 디자인에서 할당 되는 등급 필요 없이 강좌에 등록할 수는 학생을 허용 하지 않으므로,이 자습서에 대 한 가정할 수 있습니다에 해당 있으면 행을 `StudentGrade` 강좌와 연결 된 테이블 행 과정에 등록 되 고와 같습니다. (의 `Courses` 탐색 속성은 강사에 대해서만 합니다.)

사용 하는 경우는 `ContextTypeName` 특성을 `EntityDataSource` 컨트롤, Entity Framework 자동으로 검색 탐색 속성에 대 한 정보는 속성에 액세스 하면 합니다. 이 이라고 *지연 로드*합니다. 그러나이 비효율적일 수 있습니다, 각 시간 추가 정보가 필요한 데이터베이스에 대 한 별도 호출에 있기 때문입니다. 반환 된 모든 엔터티에 대 한 탐색 속성의 데이터를 해야 하는 경우는 `EntityDataSource` 컨트롤 것이 데이터베이스에 대 한 단일 호출에서 엔터티 자체와 함께 관련된 데이터를 검색 하는 것이 효율적입니다. 이것을 *선행 로딩과*를 설정 하 여 탐색 속성에 대해 즉시 로드를 지정 하 고는 `Include` 의 속성을 `EntityDataSource` 컨트롤입니다.

*Students.aspx*모든 학생의 코스 수를 표시 하려면, 따라서 즉시 로드는 것이 좋습니다. 모든 학생 들이 표시 되었다가 과정의 수를 보여 주는 경우 몇 가지 (해야 하는 태그 외에도 몇 가지 코드 작성)에 대해서만 지연 로드를 더 적합할 수 있습니다.

열거나으로 전환 *Students.aspx*, 전환할 **디자인** 뷰의 `StudentsEntityDataSource`, 및를 **속성** 창 집합은 **포함**속성을 **StudentGrades**합니다. (여러 탐색 속성을 구현 하려고 하는 경우 쉼표로 구분 하 여 해당 이름을 지정할 수 있습니다-예를 들어 **StudentGrades, 교육 코스**.)

[![Image19](the-entity-framework-and-aspnet-getting-started-part-2/_static/image40.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image39.png)

전환할 **원본** 보기. 에 `StudentsGridView` 마지막 컨트롤 `asp:TemplateField` 요소를 추가한 다음 서식 파일 필드:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample7.aspx)]

에 `Eval` 식에 탐색 속성을 참조할 수 있습니다 `StudentGrades`합니다. 이 속성 컬렉션에 포함 되어 있으므로 있기를 `Count` 학생이 등록 된 강좌의 번호가 표시 하는 데 사용할 수 있는 속성입니다. 자습서의 뒷부분에서 컬렉션 대신 단일 엔터티를 포함 하는 탐색 속성에서 데이터를 표시 하는 방법을 배웁니다. (사용할 수 없습니다는 `BoundField` 탐색 속성에서 데이터를 표시 하는 요소입니다.)

페이지를 실행 하 고 각 강좌 수 학생에 등록 되어 표시 됩니다.

[![Image20](the-entity-framework-and-aspnet-getting-started-part-2/_static/image42.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image41.png)

## <a name="using-a-detailsview-control-to-insert-entities"></a>DetailsView 컨트롤을 사용 하 여 엔터티를 삽입 합니다.

이 페이지를 만들려면 다음 단계는는 `DetailsView` 새 학생을 추가할 수 있도록 컨트롤입니다. 브라우저를 닫고 만든 다음 사용 하 여 새 웹 페이지의 *Site.Master* 마스터 페이지입니다. 페이지의 이름을 *StudentsAdd.aspx*, 한 다음으로 전환 **원본** 보기.

에 대 한 기존 태그를 바꾸려면 다음 태그를 추가 합니다 `Content` 제어 라는 `Content2`:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample8.aspx)]

이 태그를 만듭니다는 `EntityDataSource` 컨트롤에서 만든 것과 비슷한입니다 *Students.aspx*삽입 수 있도록 제외 하 고 있습니다. 와 마찬가지로 합니다 `GridView` 컨트롤의 바인딩된 필드는 `DetailsView` 엔터티 속성을 참조 하는 점을 제외 하 고 데이터베이스에 직접 연결 하는 데이터 컨트롤에 대 한 것 처럼 정확 하 게 제어 코딩 됩니다. 이 경우에 `DetailsView` 컨트롤은 기본 모드를 설정한 경우 있도록 행 삽입에 사용 `Insert`합니다.

페이지를 실행 하 고 새 학생을 추가 합니다.

[![Image09](the-entity-framework-and-aspnet-getting-started-part-2/_static/image44.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image43.png)

하지만 이제 실행 하는 경우 새 학생을 삽입 하면 아무 작업도 *Students.aspx*, 새로운 학생 정보를 표시 합니다.

## <a name="displaying-data-in-a-drop-down-list"></a>드롭다운 목록에서 데이터를 표시합니다.

Databind 살펴볼 다음 단계에는 `DropDownList` 컨트롤을 사용 하 여 설정 하는 엔터티는 `EntityDataSource` 컨트롤입니다. 자습서의이 부분에서는이 목록을 사용 하 여 많은 수행할 없습니다. 다음 부분 그러나 있습니다를 사용 하 여 목록 사용자가 부서와 관련 된 강의 표시 하려면 부서를 선택할 수 있습니다.

라는 새 웹 페이지를 만듭니다 *Courses.aspx*합니다. **소스** 보기에서 머리글을 추가 합니다 `Content` 라는 컨트롤을 `Content2`:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample9.aspx)]

**디자인** 보기에서 추가 `EntityDataSource` 컨트롤을 페이지 이전에 수행한 것 처럼이 시간을 제외 하 고 이름을 `DepartmentsEntityDataSource`입니다. 선택 **부서** 으로 **EntitySetName** 값을 선택 합니다 **DepartmentID** 및 **이름** 속성입니다.

[![Image15](the-entity-framework-and-aspnet-getting-started-part-2/_static/image46.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image45.png)

**표준** 탭의 **도구 상자**, 끌어를 `DropDownList` 페이지로 컨트롤을 이름을 `DepartmentsDropDownList`, 스마트 태그를 클릭 하 고 선택 **데이터 소스 선택** 를 시작 합니다 **데이터 소스 구성 마법사**합니다.

[![Image16](the-entity-framework-and-aspnet-getting-started-part-2/_static/image48.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image47.png)

에 **데이터 원본 선택** 단계 선택 **DepartmentsEntityDataSource** 데이터 원본으로 클릭 **스키마 새로 고침**를 선택한 후 **이름** 표시할 데이터 필드와 **DepartmentID** 값 데이터 필드입니다. **확인**을 클릭합니다.

[![Image17](the-entity-framework-and-aspnet-getting-started-part-2/_static/image50.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image49.png)

Entity Framework를 사용 하 여 컨트롤 데이터 바인딩에 사용 하는 방법은 다른 ASP.NET 데이터 소스 컨트롤 온다는 점만 다릅니다 지정 하는 엔터티 및 엔터티 속성으로 동일 합니다.

전환할 **원본** 보기 및 추가 "부서 선택:" 직전는 `DropDownList` 컨트롤.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample10.aspx)]

참고로, 변경에 대 한 태그를 `EntityDataSource` 대체 하 여이 시점에 컨트롤을 `ConnectionString` 및 `DefaultContainerName` 특성을 `ContextTypeName="ContosoUniversity.DAL.SchoolEntities"` 특성. 것이 좋습니다 변경 하기 전에 데이터 소스 컨트롤에 연결 된 데이터 바인딩된 컨트롤을 만든 후 될 때까지 대기 하는 `EntityDataSource` 변경을 수행한 후 디자이너를 제공 하지 않으므로으로 태그를 제어는 **새로 고침 스키마** 데이터 바인딩된 컨트롤에서 옵션입니다.

페이지를 실행 하 고 드롭다운 목록에서 부서를 선택할 수 있습니다.

[![Image18](the-entity-framework-and-aspnet-getting-started-part-2/_static/image52.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image51.png)

사용 하 여에 대 한 소개를 완료 합니다 `EntityDataSource` 제어 합니다. 이 컨트롤을 사용 하 여 작업은 일반적으로 다르지 않습니다 다른 ASP.NET 데이터 소스 컨트롤을 작업 제외 하 고 엔터티와 테이블 및 열 대신 속성을 참조 합니다. 유일한 예외는 탐색 속성에 액세스 하려는 경우에 합니다. 다음 자습서에서 보면 사용 하는 구문을 사용 하 여 `EntityDataSource` 컨트롤 필터링, 그룹화 및 데이터를 정렬 하는 경우에 다른 데이터 소스 컨트롤에서 달라질 수 있습니다.

> [!div class="step-by-step"]
> [이전](the-entity-framework-and-aspnet-getting-started-part-1.md)
> [다음](the-entity-framework-and-aspnet-getting-started-part-3.md)
