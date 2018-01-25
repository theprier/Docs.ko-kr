---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-2
title: "먼저 Entity Framework 4.0 데이터베이스와 시작 및 ASP.NET 4 Web Forms-2 부 | Microsoft Docs"
author: tdykstra
description: "Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 샘플 응용 프로그램은..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/03/2010
ms.topic: article
ms.assetid: fb63a326-a4ae-4b0c-a4f5-412327197216
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-2
msc.type: authoredcontent
ms.openlocfilehash: a549bd62bd78573c368784fd1529a830e009b0d4
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-2"></a>먼저 Entity Framework 4.0 데이터베이스와 시작 및 ASP.NET 4 Web Forms-2 부
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

> Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 4.0 및 Visual Studio 2010을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대 한 정보를 참조 하세요. [시리즈의 첫 번째 자습서](the-entity-framework-and-aspnet-getting-started-part-1.md)


## <a name="the-entitydatasource-control"></a>EntityDataSource 컨트롤

이전 자습서에서는 웹 사이트, 데이터베이스 및 데이터 모델을 만들었습니다. 이 자습서에서는 작업할는 `EntityDataSource` ASP.NET 쉽게 Entity Framework 데이터 모델을 작업할 수 있도록 하기 위해 제공 하는 컨트롤입니다. 만듭니다는 `GridView` 학생 데이터 표시 및 편집에 대 한 제어는 `DetailsView` 새 학생을 추가 하기 위한 컨트롤 및 `DropDownList` 부서 (나중에 사용할 연결된 과정을 표시 하기 위해)를 선택 하기 위한 제어 합니다.

[![Image20](the-entity-framework-and-aspnet-getting-started-part-2/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image1.png)

[![Image09](the-entity-framework-and-aspnet-getting-started-part-2/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image3.png)

[![Image18](the-entity-framework-and-aspnet-getting-started-part-2/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image5.png)

이 응용 프로그램에서 있하지 않습니다 수 입력된 유효성 검사 페이지에 추가 데이터베이스를 업데이트 하 고 프로덕션 응용 프로그램에 필요한 강력한 됩니다 오류 처리의 일부 note 합니다. Entity Framework에 집중 하는 자습서를 유지 하 고 너무 길거나에서 유지 합니다. 응용 프로그램에 이러한 기능을 추가 하는 방법에 대 한 세부 정보를 참조 하십시오. [ASP.NET 웹 페이지에서 사용자 입력 유효성 검사](https://msdn.microsoft.com/library/7kh55542.aspx) 및 [ASP.NET 페이지 및 응용 프로그램에서 오류 처리](https://msdn.microsoft.com/library/w16865z6.aspx)합니다.

## <a name="adding-and-configuring-the-entitydatasource-control"></a>EntityDataSource 컨트롤 추가 및 구성

구성 하 여 시작 합니다는 `EntityDataSource` 읽기 제어 `Person` 에서 엔터티는 `People` 엔터티 집합입니다.

Visual Studio가 열고 있는 있는지 확인 및 1 단계에서 만든 프로젝트 사용 하 고 있음을 합니다. 에 대 한 마지막 변경 이후 또는 데이터 모델을 만든 후 프로젝트를 빌드한 하지 않은 경우 지금 프로젝트를 빌드하십시오. 데이터 모델에 대 한 변경에 적용 되지 않습니다 사용할 수 있는 디자이너 프로젝트가 빌드될 때까지 합니다.

사용 하 여 새 웹 페이지 만들기는 **웹 폼 마스터 페이지를 사용 하 여** 서식 파일을 하 고 이름을 *Students.aspx*합니다.

[![Image23](the-entity-framework-and-aspnet-getting-started-part-2/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image7.png)

지정 *Site.Master* 마스터 페이지로 합니다. 이 자습서에 대해 만드는 페이지를 모두이 마스터 페이지를 사용 합니다.

[![Image24](the-entity-framework-and-aspnet-getting-started-part-2/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image9.png)

**소스** 보기, 추가 `h2` 머리글에 `Content` 라는 컨트롤 `Content2`다음 예제에 나온 것 처럼:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample1.aspx)]

**데이터** 탭은 **도구 상자**를 끌어 한 `EntityDataSource` 컨트롤을 페이지 머리글 아래에 놓습니다 하 고 ID를 변경 `StudentsEntityDataSource`:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample2.aspx)]

로 전환 **디자인** 보고, 데이터 소스 컨트롤의 스마트 태그를 클릭 한 다음 클릭 **데이터 소스 구성** 시작 하는 **데이터 소스 구성** 마법사.

[![Image01](the-entity-framework-and-aspnet-getting-started-part-2/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image11.png)

에 **구성 ObjectContext** 마법사 단계 **SchoolEntities** 에 대 한 값으로 **명명 된 연결**를 선택 하 고 **SchoolEntities**로 **DefaultContainerName** 값입니다. **다음**을 클릭합니다.

[![Image02](the-entity-framework-and-aspnet-getting-started-part-2/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image13.png)

참고:이 시점에서 다음과 같은 대화 상자가 나타나면 해야 계속 진행 하기 전에 프로젝트를 빌드합니다.

[![Image25](the-entity-framework-and-aspnet-getting-started-part-2/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image15.png)

에 **데이터 선택 구성** 단계에서는 **사람** 에 대 한 값으로 **EntitySetName**합니다. **선택**, 있는지 확인은 **선택** ll 확인란을 선택 합니다. 업데이트 설정 및 삭제 하 고 옵션을 선택 합니다. 완료 되 면 클릭 **마침**합니다.

[![Image03](the-entity-framework-and-aspnet-getting-started-part-2/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image17.png)

## <a name="configuring-database-rules-to-allow-deletion"></a>삭제를 허용 하도록 데이터베이스 규칙 구성

만들려는에서 학생을 삭제 하는 사용자가 수 있는 페이지는 `Person` 세 개의 다른 테이블과 관계가 있는 테이블 (`Course`, `StudentGrade`, 및 `OfficeAssignment`). 기본적으로 데이터베이스 수 없게 됩니다에서 행 삭제 `Person` 관련된 행이 다른 테이블 중 하나에 없는 경우. 관련된 행을 먼저 삭제 수동으로 하거나 삭제 하면 자동으로 삭제 하는 데이터베이스를 구성할 수 있습니다는 `Person` 행입니다. 이 자습서에서는 학생 레코드를 위한 관련된 데이터를 자동으로 삭제할 데이터베이스를 구성 합니다. 관련 행 학생에 수 있기 때문에는 `StudentGrade` 관계 3 중 하나에 구성 해야 하는 테이블입니다.

사용 중인 경우는 *School.mdf* 이 자습서와 함께 이동 하는 프로젝트에서 다운로드 한 파일, 이러한 구성 변경 내용을 이미 완료 된 때문에이 섹션을 건너뛸 수 있습니다. 스크립트를 실행 하 여 데이터베이스를 만든 경우 다음 절차를 수행 하 여 데이터베이스를 구성 합니다.

**서버 탐색기**, 1 단계에서 만든 데이터베이스 다이어그램을 엽니다. 간의 관계를 마우스 오른쪽 단추로 클릭 `Person` 및 `StudentGrade` (테이블 사이의 선에)을 선택한 후 **속성**합니다.

[![Image04](the-entity-framework-and-aspnet-getting-started-part-2/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image19.png)

에 **속성** 창 확장 **INSERT 및 UPDATE 사양** 설정 하 고는 **DeleteRule** 속성을 **Cascade**합니다.

[![Image05](the-entity-framework-and-aspnet-getting-started-part-2/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image21.png)

저장 하 고 다이어그램을 닫습니다. 클릭 하 여 데이터베이스를 업데이트 하려면 여부를 묻는 경우 **예**합니다.

모델 데이터베이스 수행 하는와 동기화 하는 메모리에 있는 엔터티를 유지 하려면 데이터 모델의 해당 규칙을 설정 해야 합니다. 열기 *SchoolModel.edmx*, 간에 연결 선을 마우스 오른쪽 단추로 클릭 `Person` 및 `StudentGrade`를 선택한 후 **속성**합니다.

[![Image21](the-entity-framework-and-aspnet-getting-started-part-2/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image23.png)

에 **속성** 창의 설정 **End1 OnDelete** 를 **Cascade**합니다.

[![Image22](the-entity-framework-and-aspnet-getting-started-part-2/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image25.png)

저장 하 고 닫습니다는 *SchoolModel.edmx* 파일을 선택한 다음 프로젝트를 다시 빌드합니다.

일반적으로 데이터베이스 변경 될 때 해당 모델을 동기화 하는 방법에 대 한 몇 가지 옵션이 있습니다.

- 특정 종류의 변경 (예: 추가 하거나 테이블, 뷰 또는 저장된 프로시저를 새로 고침)를 마우스 오른쪽 단추로 클릭 디자이너와 선택 **데이터베이스에서 모델 업데이트** 디자이너 만들기 변경 내용을 자동으로 있어야 합니다.
- 데이터 모델을 다시 생성 합니다.
- 이 이와 같은 수동 업데이트를 확인 합니다.

필드 이름 변경 작업을 다시 수행 해야 하는 다음 다시 모델 생성 또는 관계 변경의 영향을 받는 테이블을 새로 고칠 하지만 경우 (에서 `FirstName` 를 `FirstMidName`).

## <a name="using-a-gridview-control-to-read-and-update-entities"></a>GridView 컨트롤을 사용 하 여 읽기 및 엔터티를 업데이트 합니다.

이 섹션에서는 `GridView` 컨트롤을 표시, 업데이트 또는 학생을 삭제 합니다.

열거나 전환 *Students.aspx* 전환할 **디자인** 보기. **데이터** 탭은 **도구 상자**를 끌어는 `GridView` 컨트롤의 오른쪽에는 `EntityDataSource` 제어 하 고, 이름을 `StudentsGridView`, 스마트 태그를 클릭 한 다음 선택  **StudentsEntityDataSource** 데이터 원본으로 합니다.

[![Image06](the-entity-framework-and-aspnet-getting-started-part-2/_static/image28.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image27.png)

클릭 **스키마 새로 고침** (클릭 **예** 확인 로그인할지 묻는)를 클릭 한 다음 **페이징 사용**, **정렬 사용**, **편집 사용**, 및 **삭제 사용**합니다.

클릭 **열 편집**합니다.

[![Image10](the-entity-framework-and-aspnet-getting-started-part-2/_static/image30.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image29.png)

에 **선택한 필드** 상자가 **PersonID**, **LastName**, 및 **HireDate**합니다. 일반적으로 사용자에 게 레코드 키를 표시 하지 않습니다, 고용 날짜 학생에 관련이 없는 및 이름 필드 하나만 필요 하므로 한 필드의 이름의 두 파트를 배치 합니다.)

[![Image11](the-entity-framework-and-aspnet-getting-started-part-2/_static/image32.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image31.png)

선택 된 **FirstMidName** 필드를 클릭 한 다음 **이 필드를 TemplateField로 변환**합니다.

에 대 한 동일 하 게 수행 **EnrollmentDate**합니다.

[![Image13](the-entity-framework-and-aspnet-getting-started-part-2/_static/image34.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image33.png)

클릭 **확인** 한 다음 전환 **소스** 보기. 나머지 변경을 태그에 직접 작업을 수행 하는 보다 쉽게 됩니다. `GridView` 다음 예제와 같은 태그 지금 검색을 제어 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample3.aspx)]

현재 명령 필드는 서식 파일 필드 후 첫 번째 열 이름을 표시 합니다. 다음 예제와 같이이 서식 파일 필드에 대 한 태그를 변경 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample4.aspx)]

디스플레이 모드에 두 개의 `Label` 컨트롤 이름과 성을 표시 합니다. 편집 모드에 두 개의 텍스트 상자 성과 이름을 변경할 수 있도록 제공 됩니다. 과 마찬가지로 `Label` 컨트롤에 디스플레이 모드를 사용 하 `Bind` 및 `Eval` 식과 동일 하 게 데이터베이스에 직접 연결 하는 ASP.NET 데이터 소스 제어를 제공 하는 것입니다. 유일한 차이점은 데이터베이스 열 대신 엔터티 속성을 지정 하는 합니다.

마지막 열은 등록 날짜를 표시 하는 서식 파일 필드. 다음 예제와 같이이 필드에 대 한 태그를 변경 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample5.aspx)]

둘 다에서 표시 하 고 편집 모드를 형식 문자열 "{0, d}" 하면 날짜를 "간단한 날짜" 형식으로 표시 됩니다. (컴퓨터의 화면 이미지 등이 자습서의 예제에서 다르게이 형식을 표시 하도록 구성할 수 있습니다.)

각 템플릿 필드에 디자이너 사용는 `Bind` 기본적으로 식에는 변경는 `Eval` 식에는 `ItemTemplate` 요소입니다. `Bind` 식의 데이터에 사용할 수 있도록 `GridView` 경우 코드의 데이터에 액세스 하려면 속성을 제어 합니다. 이 페이지에 사용할 수 있도록 코드에서이 데이터에 액세스할 필요가 없습니다 `Eval`, 더 효율적인 합니다. 자세한 내용은 참조 [데이터 컨트롤에 데이터를 가져오는](https://weblogs.asp.net/davidfowler/archive/2008/12/12/getting-your-data-out-of-the-data-controls.aspx)합니다.

## <a name="revising-entitydatasource-control-markup-to-improve-performance"></a>성능 향상을 위해 EntityDataSource 컨트롤 태그를 수정 합니다.

에 대 한 태그에는 `EntityDataSource` 컨트롤을 제거는 `ConnectionString` 및 `DefaultContainerName` 특성 및를 사용 하 여 바꾸기는 `ContextTypeName="ContosoUniversity.DAL.SchoolEntities"` 특성입니다. 이것은 만들 때마다 수행 해야 하는 변경 된 `EntityDataSource` 제어 개체 컨텍스트 클래스의 하드 코드 된 것과에서 다른 연결을 사용 하는 제외 합니다. 사용 하 여 `ContextTypeName` 특성은 다음과 같은 이점을 제공 합니다.

- 성능 향상. 경우는 `EntityDataSource` 제어를 사용 하 여 데이터 모델을 초기화 합니다.는 `ConnectionString` 및 `DefaultContainerName` 특성의 경우 모든 요청에 대해 메타 데이터를 로드 하기 위해 추가적인 작업 수행 합니다. 이 지정 하는 경우에 필요 하지 않습니다는 `ContextTypeName` 특성입니다.
- 생성 된 개체 컨텍스트 클래스에서 기본적으로 지연 로드 상태에서 (같은 `SchoolEntities` 이 자습서에서는) Entity Framework 4.0의 합니다. 즉, 탐색 속성은 로드 관련된 데이터와 함께 자동으로 필요할 때 오른쪽입니다. 지연 로드는이 자습서의 뒷부분에서 자세히 설명 되어 있습니다.
- 개체 컨텍스트 클래스에 적용 한 모든 사용자 지정 (이 경우는 `SchoolEntities` 클래스)를 사용 하는 컨트롤에 사용할 수 있습니다는 `EntityDataSource` 제어 합니다. 개체 컨텍스트 클래스를 사용자 지정은 자습서이 계열에 적용 되지 않는 고급 항목입니다. 자세한 내용은 참조 [엔터티 프레임 워크 생성 형식 확장](https://msdn.microsoft.com/library/dd456844.aspx)합니다.

이제 태그 (속성의 순서 다를 수 있습니다) 다음 예와 비슷하게 표시 됩니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample6.aspx)]

`EnableFlattening` 특성이 외래 키 열 엔터티 속성으로 노출 되지 않은 이전 버전의 Entity Framework에 필요 하는 기능을 참조 합니다. 현재 버전을 사용 하면 사용 하 여 *외래 키 연결*를 제외한 모든 다 대 다 연결에 대해 노출 된 외래 키 속성을 의미 하는 합니다. 엔터티에 외래 키 속성 및 no 경우 [복합 형식을](https://msdn.microsoft.com/library/bb738472.aspx),이 특성이로 설정 그대로 둘 수 있습니다 `False`합니다. 기본값은 때문에 태그에서 특성을 제거 하지 마십시오 `True`합니다. 자세한 내용은 참조 [평면화 개체 (EntityDataSource)](https://msdn.microsoft.com/library/ee404746.aspx)합니다.

페이지를 실행 하 고 학생 (필터링 정당한 학생용 다음 자습서의) 직원의 목록이 표시 됩니다. 이름 및 성 함께 표시 됩니다.

[![Image07](the-entity-framework-and-aspnet-getting-started-part-2/_static/image36.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image35.png)

디스플레이 정렬 하려면 열 이름을 클릭 합니다.

클릭 **편집** 행에 있습니다. 성과 이름을 변경할 수 있는 텍스트 상자가 표시 됩니다.

[![Image08](the-entity-framework-and-aspnet-getting-started-part-2/_static/image38.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image37.png)

**삭제** 단추도 작동 합니다. 등록 날짜를 포함 하는 행에 대 한 삭제를 클릭 하 고 행 사라집니다. (행 등록 날짜 없이 강사 나타내고 참조 무결성 오류가 발생할 수 있습니다. 다음 자습서에서 필터링 합니다 정당한 학생을 포함 하도록이 목록을.)

## <a name="displaying-data-from-a-navigation-property"></a>탐색 속성에서 데이터 표시

이제 강좌 수를 알고 싶은 경우를 가정해 볼 각 학생에 등록 됩니다. Entity Framework에서 해당 정보를 제공는 `StudentGrades` 의 탐색 속성은 `Person` 엔터티. 데이터베이스 디자인을 등록 하는 과정에서 할당 된 등급 필요 없이 학생을 허용 하지 않으므로,이 자습서에 대 한 가정할 수 있습니다에 해당 있으면 행은 `StudentGrade` 과정와 연결 된 테이블 행은 등록 하는 과정에서와 동일 합니다. (의 `Courses` 탐색 속성 강사에만 적용 됩니다.)

사용 하는 경우는 `ContextTypeName` 특성에는 `EntityDataSource` 컨트롤을 Entity Framework 자동으로 정보를 검색 하는 탐색 속성에 대 한 해당 속성에 액세스할 때. 이 라고 *한 지연 로딩이*합니다. 그러나이 수 수, 각 시간 추가 정보가 필요한 데이터베이스에 대 한 별도 호출을 발생 시키므로. 반환 된 모든 엔터티는 탐색 속성에서 데이터가 필요할 경우는 `EntityDataSource` 컨트롤 것이 더 효율적 엔터티 자체를 데이터베이스에 단일 호출에서 함께 관련된 데이터를 검색 합니다. 라고 *즉시 로드*를 설정 하 여 탐색 속성에 대 한 즉시 로드를 지정 하 고는 `Include` 속성의는 `EntityDataSource` 제어 합니다.

*Students.aspx*, 모든 학생이 대 한 교육 과정의 수를 표시 하려면, 따라서 즉시 로드 것이 가장 좋습니다. 모든 학생 표시 되었다가 과정의 수를 보여 주는 경우만 일부만 (해야 하는 태그 외에 일부 코드 작성)을 지연 로드 될 수 있습니다 더 좋습니다.

열거나으로 전환 *Students.aspx*, 전환할 **디자인** 보기, `StudentsEntityDataSource`, 및는 **속성** 창 집합은 **Include**속성을 **StudentGrades**합니다. (여러 탐색 속성을 가져올 하려는 경우 쉼표로 구분 하 여 이름을 지정할 수 있습니다-예를 들어 **StudentGrades, Courses**.)

[![Image19](the-entity-framework-and-aspnet-getting-started-part-2/_static/image40.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image39.png)

로 전환 **소스** 보기. 에 `StudentsGridView` 마지막 뒤 컨트롤 `asp:TemplateField` 요소를 추가한 다음 서식 파일 필드:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample7.aspx)]

에 `Eval` 식 탐색 속성을 참조할 수 있습니다 `StudentGrades`합니다. 가이 속성 컬렉션에 포함 되어 있으므로 `Count` 학생을 등록 하는 과정의 수를 표시 하는 데 사용할 수 있는 속성입니다. 이후의 자습서에서 컬렉션 대신 단일 엔터티를 포함 하는 탐색 속성에서 데이터를 표시 하는 방법을 볼 수 있습니다. (사용할 수 없는 참고 `BoundField` 요소 탐색 속성의 데이터를 표시 합니다.)

페이지를 실행 하 고 개수 courses 학생에 등록 되어 표시 됩니다.

[![Image20](the-entity-framework-and-aspnet-getting-started-part-2/_static/image42.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image41.png)

## <a name="using-a-detailsview-control-to-insert-entities"></a>DetailsView 컨트롤을 사용 하 여 엔터티를 삽입 하려면

이 페이지를 만들려면 다음 단계는는 `DetailsView` 새 학생을 추가할 수 있는 컨트롤입니다. 브라우저를 닫고 다음 사용 하 여 새 웹 페이지를 만듭니다는 *Site.Master* 마스터 페이지입니다. 페이지 이름을 *StudentsAdd.aspx*, 한 다음 전환 **소스** 보기.

에 대 한 기존 태그의 이름을 바꾸려면 다음 태그를 추가 `Content` 라는 컨트롤 `Content2`:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample8.aspx)]

이 태그를 만듭니다는 `EntityDataSource` 에서 만든 것과 비슷한에 있는 컨트롤과 *Students.aspx*삽입 수는 제외 하 고 있습니다. 과 마찬가지로 `GridView` 컨트롤의 바인딩된 필드는 `DetailsView` 컨트롤은 제외 하 고 엔터티 속성을 참조 하는 데이터베이스에 직접 연결 하는 데이터 컨트롤에 대 한 것 처럼 정확 하 게 코딩 합니다. 이 경우에 `DetailsView` 컨트롤은 기본 모드를 설정한 경우 하므로 행 삽입에 사용 `Insert`합니다.

페이지를 실행 하 고 새 학생을 추가 합니다.

[![Image09](the-entity-framework-and-aspnet-getting-started-part-2/_static/image44.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image43.png)

하지만 새 학생을 삽입 한 후 실행 하면 아무 작업도 *Students.aspx*, 새 학생 정보가 표시 됩니다.

## <a name="displaying-data-in-a-drop-down-list"></a>드롭다운 목록에서 데이터 표시

다음 단계에서는 databind는 `DropDownList` 컨트롤을 사용 하 여 설정 하는 엔터티는 `EntityDataSource` 제어 합니다. 자습서의이 부분에서는이 목록을 사용 하 여 거의 수행 하지 않습니다. 다음 부분에서 하지만 합니다 목록을 사용 하면 사용자가 부서와 관련 된 과정을 표시 하려면 부서를 선택할 수 있도록 합니다.

라는 새 웹 페이지 생성 *Courses.aspx*합니다. **소스** 보기, 추가 머리글을는 `Content` 라는 컨트롤을 `Content2`:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample9.aspx)]

**디자인** 보기, 추가 `EntityDataSource` 컨트롤을 페이지 이전에 수행한 것 처럼이 시간 제외 하 고 이름을 `DepartmentsEntityDataSource`합니다. 선택 **부서** 로 **EntitySetName** 값을 선택 하는 **DepartmentID** 및 **이름** 속성입니다.

[![Image15](the-entity-framework-and-aspnet-getting-started-part-2/_static/image46.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image45.png)

**표준** 탭은 **도구 상자**를 끌어는 `DropDownList` 페이지를 제어 하 고, 이름을 `DepartmentsDropDownList`를 스마트 태그를 클릭 하 고 **데이터 소스 선택** 를 시작 된 **데이터 소스 구성 마법사**합니다.

[![Image16](the-entity-framework-and-aspnet-getting-started-part-2/_static/image48.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image47.png)

에 **데이터 원본을 선택** 단계에서는 **DepartmentsEntityDataSource** 데이터 원본으로 클릭 **스키마 새로 고침**를 선택한 후 **이름** 으로 표시할 데이터 필드 및 **DepartmentID** 값 데이터 필드와 합니다. **확인**을 클릭합니다.

[![Image17](the-entity-framework-and-aspnet-getting-started-part-2/_static/image50.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image49.png)

Entity Framework를 사용 하 여 컨트롤 데이터 바인딩에 사용 하는 방법은 다른 ASP.NET 데이터와 사용자를 제외 하 고 소스 컨트롤 지정 하는 엔터티 및 엔터티 속성와 같습니다.

로 전환 **소스** 보기 및 추가 "부서 선택:" 바로 앞의 `DropDownList` 제어 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample10.aspx)]

참고로 변경에 대 한 태그는 `EntityDataSource` 대체 하 여이 시점에서 제어는 `ConnectionString` 및 `DefaultContainerName` 특성을 `ContextTypeName="ContosoUniversity.DAL.SchoolEntities"` 특성입니다. 것이 가장 좋습니다 변경 하기 전에 데이터 소스 제어에 연결 되어 있는 데이터 바인딩된 컨트롤을 만든 후 될 때까지 대기 하는 `EntityDataSource` 변경을 수행한 후 디자이너는 제공 하지 않으므로 사용 하면 태그 컨트롤에 **새로 고침 스키마** 데이터 바인딩된 컨트롤에서 옵션입니다.

페이지를 실행 하 고 드롭다운 목록에서 부서를 선택할 수 있습니다.

[![Image18](the-entity-framework-and-aspnet-getting-started-part-2/_static/image52.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image51.png)

이 사용 하 여 소개 작업이 완료 되는 `EntityDataSource` 제어 합니다. 작업이 컨트롤과 하는 일반적으로 더 다른 ASP.NET 데이터 소스 제어 작업에서 제외 하 고 엔터티 및 테이블 및 열 대신 속성을 참조 합니다. 유일한 예외는 탐색 속성에 액세스 하려면 하는 경우. 다음 자습서 것을 알 구문을 사용 하는 `EntityDataSource` 제어 필터링, 그룹화 및 데이터를 정렬 하는 경우에 다른 데이터 소스 컨트롤에서 달라질 수 있습니다.

>[!div class="step-by-step"]
[이전](the-entity-framework-and-aspnet-getting-started-part-1.md)
[다음](the-entity-framework-and-aspnet-getting-started-part-3.md)
