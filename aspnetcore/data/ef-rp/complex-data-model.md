---
title: "EF 코어-8의 5-데이터 모델을 사용 하 여 razor 페이지"
author: rick-anderson
description: "이 자습서에서는 더 많은 엔터티 및 관계를 추가 및 서식 지정, 유효성 검사 및 데이터베이스 매핑 규칙을 지정 하 여 데이터 모델을 사용자 지정 합니다."
keywords: "ASP.NET Core, Entity Framework Core 데이터 주석"
ms.author: riande
manager: wpickett
ms.date: 10/25/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: data/ef-rp/complex-data-model
ms.openlocfilehash: c2761f79fa4836d29541526782969bb0fd47778b
ms.sourcegitcommit: 6e46abd65973dea796d364a514de9ec2e3e1c1ed
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/02/2017
---
# <a name="creating-a-complex-data-model---ef-core-with-razor-pages-tutorial-5-of-8"></a>복잡 한 데이터 모델-EF 코어 Razor 페이지 자습서 (8 5)와 함께 만들기

여 [Tom Dykstra](https://github.com/tdykstra) 및 [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE[about the series](../../includes/RP-EF/intro.md)]

이전 자습서의 세 가지 엔터티 작성 된 기본 데이터 모델이 들어 있는 작업. 이 자습서:

* 더 많은 엔터티 및 관계 추가 됩니다.
* 서식 지정, 유효성 검사 및 데이터베이스 매핑 규칙을 지정 하 여 데이터 모델 사용자 지정 됩니다.

완성 된 데이터 모델에 대 한 엔터티 클래스는 다음 그림에 표시 됩니다.

![엔터티 다이어그램](complex-data-model/_static/diagram.png)

문제를 해결할 수 없는를 실행 하는 경우 다운로드는 [이 단계에 대 한 완성 된 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part5-complex)합니다.

## <a name="customize-the-data-model-with-attributes"></a>특성을 가진 데이터 모델 사용자 지정

이 섹션에서는 데이터 모델 사용자 특성을 사용 하 여 지정 됩니다.

### <a name="the-datatype-attribute"></a>데이터 형식 특성

학생 페이지는 현재 등록 날짜의 시간을 표시 합니다. 일반적으로 날짜 필드에 날짜 및 시간이 아닌 나타납니다.

업데이트 *Models/Student.cs* 를 다음으로 코드를 강조 표시 합니다.

[!code-csharp[Main](intro/samples/cu/Models/Student.cs?name=snippet_DataType&highlight=3,12-13)]

[DataType](https://docs.microsoft.com/dotnet/api/system.componentmodel.dataannotations.datatypeattribute?view=netframework-4.7.1) 특성 데이터베이스 내장 형식 보다 구체적인 데이터 형식을 지정 합니다. 이 경우에는 날짜를 표시할지 날짜 및 시간입니다. [DataType 열거형](https://docs.microsoft.com/dotnet/api/system.componentmodel.dataannotations.datatype?view=netframework-4.7.1) 날짜, 시간, 전화 번호, 통화, EmailAddress 등과 같은 많은 데이터 형식에 대 한 제공 합니다. `DataType` 특성 응용 프로그램에서 특정 형식의 기능을 제공 하는 자동으로 활성화할 수도 있습니다. 예:

* `mailto:` 에 대 한 링크가 자동으로 만들어집니다 `DataType.EmailAddress`합니다.
* 날짜 선택 ´ ë ç `DataType.Date` 대부분의 브라우저에서 합니다.

`DataType` 특성 내보냅니다 HTML 5 `data-` HTML 5 브라우저를 사용 하는 (커맨드 데이터 대시) 특성입니다. `DataType` 특성 유효성 검사를 제공 하지 않습니다.

`DataType.Date`는 표시되는 날짜의 서식을 지정하지 않습니다. 기본적으로 날짜 필드는 서버에 따라 기본 형식에 따라 표시 [CultureInfo](https://docs.microsoft.com/aspnet/core/fundamentals/localization#provide-localized-resources-for-the-languages-and-cultures-you-support)합니다.

`DisplayFormat` 특성은 날짜 형식을 명시적으로 지정하는 데 사용됩니다.

```csharp
[DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
```

`ApplyFormatInEditMode` 설정은 서식을 적용 해야 하는지도 편집 UI에 지정 합니다. 일부 필드를 사용 하지 않아야 `ApplyFormatInEditMode`합니다. 예를 들어, 통화 기호는 일반적으로 나타나지 편집 텍스트 상자에.

`DisplayFormat` 특성 단독으로 사용할 수 있습니다. 일반적으로 사용 하는 `DataType` 특성이 `DisplayFormat` 특성입니다. `DataType` 특성의 데이터를 화면에 렌더링 하는 방법 전송할 의미 체계를 전달 합니다. `DataType` 특성에서 사용할 수 있는 다음과 같은 이점을 제공 `DisplayFormat`:

* 브라우저는 HTML5 기능을 활성화할 수 있습니다. 예를 들어 calendar 컨트롤, 로캘에 적합 한 통화 기호, 전자 메일 링크, 클라이언트 쪽 입력된 유효성 검사, 등을 표시 합니다.
* 기본적으로 브라우저는 로캘을 기반으로 올바른 형식을 사용 하 여 데이터를 렌더링 합니다.

자세한 내용은 참조는 [ \<입력 > 태그 도우미 설명서](xref:mvc/views/working-with-forms#the-input-tag-helper)합니다.

앱을 실행합니다. 학생 인덱스 페이지로 이동 합니다. 시간이 더 이상 표시 됩니다. 사용 하는 모든 보기는 `Student` 모델에는 시간을 제외한 날짜가 표시 됩니다.

![학생 인덱스 페이지 시간 없이 날짜를 표시 합니다.](complex-data-model/_static/dates-no-times.png)

### <a name="the-stringlength-attribute"></a>StringLength 특성

데이터 유효성 검사 규칙 및 유효성 검사 오류 메시지를 특성으로 지정할 수 있습니다. [StringLength](https://docs.microsoft.com/dotnet/api/system.componentmodel.dataannotations.stringlengthattribute?view=netframework-4.7.1) 특성 문자 데이터 필드에는 사용할 수 있는 최소 및 최대 길이 지정 합니다. `StringLength` 특성은 또한 클라이언트 쪽 및 서버 쪽 유효성 검사를 제공 합니다. 최소 값은 데이터베이스 스키마에 대해 영향이 없습니다.

업데이트는 `Student` 를 다음 코드로 모델:

[!code-csharp[Main](intro/samples/cu/Models/Student.cs?name=snippet_StringLength&highlight=10,12)]

위의 코드 이름을 최대 50 자로 제한 됩니다. `StringLength` 특성 이름에 공백을 입력에서 사용자를 방지 하지 않습니다. [정규식으로](https://docs.microsoft.com/dotnet/api/system.componentmodel.dataannotations.regularexpressionattribute?view=netframework-4.7.1) 특성 입력에 제한을 적용 하는 데 사용 됩니다. 예를 들어 다음 코드는 첫 번째 문자를 대문자로 변환 하 고 나머지 문자를 사전순으로 필요 합니다.

```csharp
[RegularExpression(@"^[A-Z]+[a-zA-Z''-'\s]*$")]
```

응용 프로그램을 실행 합니다.

* 학생 페이지로 이동 합니다.
* 선택 **새로 만들기**, 50 자 보다 긴 이름을 입력 합니다.
* 선택 **만들기**, 클라이언트 쪽 유효성 검사 오류 메시지를 표시 합니다.

![학생 인덱스 문자열 길이 오류를 보여주는 페이지](complex-data-model/_static/string-length-errors.png)

**SQL Server 개체 탐색기** (SSOX) 두 번 클릭 하 여 학생 테이블 디자이너를 열고는 **학생** 테이블입니다.

![마이그레이션 전에 SSOX에 students 테이블](complex-data-model/_static/ssox-before-migration.png)

위 그림에 대 한 스키마를 보여 줍니다.는 `Student` 테이블입니다. 이름 필드 형식이 있어야 `nvarchar(MAX)` 마이그레이션 DB에서 실행 되지 않은 때문에 있습니다. 이름 필드 됩니다 마이그레이션이 시작 되 면이 자습서의 뒷부분에 나오는, `nvarchar(50)`합니다.

### <a name="the-column-attribute"></a>Column 특성

특성은 클래스 및 속성을 데이터베이스에 매핑되는 방식을 제어할 수 있습니다. 이 섹션에서는 `Column` 특성의 이름에 매핑할 때 사용 되는 `FirstMidName` 속성을 "FirstName" DB에 있습니다.

모델에 속성 이름이 열 이름에 사용 됩니다 DB를 만들면 (경우는 제외의 `Column` 특성은 사용).

`Student` 사용 하 여 모델 `FirstMidName` 첫 번째 이름에 대 한 필드 중간 이름 포함도 될 수 있으므로 필드입니다.

업데이트는 *Student.cs* 다음 강조 표시 된 코드로 파일:

[!code-csharp[Main](intro/samples/cu/Models/Student.cs?name=snippet_Column&highlight=4,14)]

이전 변경으로 인해 `Student.FirstMidName` 응용 프로그램에 매핑되는 `FirstName` 의 열은 `Student` 테이블입니다.

추가 `Column` 특성이 변경 모델이 고 `SchoolContext`합니다. 모델이 고 `SchoolContext` 데이터베이스와 일치 하지 않습니다. 마이그레이션 적용 하기 전에 앱이 실행 되는 경우 다음과 같은 예외가 생성 됩니다.

```SQL
SqlException: Invalid column name 'FirstName'.
```
DB 업데이트:

* 프로젝트를 빌드합니다.
* 프로젝트 폴더에서 명령 창을 엽니다. 새 마이그레이션 만들고 DB 업데이트 하려면 다음 명령을 입력 합니다.

    ```console
    dotnet ef migrations add ColumnFirstName
    dotnet ef database update
    ```

`dotnet ef migrations add ColumnFirstName` 명령은 다음과 같은 경고 메시지를 생성 합니다.

```text
An operation was scaffolded that may result in the loss of data.
Please review the migration for accuracy.
```

경고가 실제로 생성 되는 이름 필드는 이제 때문에 50 자로 제한 됩니다. Db에서 이름 50 개 이상의 문자가 있으면 마지막 문자까지 51 손실 됩니다.

* 응용 프로그램을 테스트 합니다.

학생 테이블을 SSOX을 엽니다.

![마이그레이션 후에 SSOX 학생 테이블](complex-data-model/_static/ssox-after-migration.png)

이름 열 형식의 된 마이그레이션을 적용 하기 전에 [nvarchar (max)](https://docs.microsoft.com/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql)합니다. 이름 열은 이제 `nvarchar(50)`합니다. 열 이름이 바뀐 `FirstMidName` 를 `FirstName`합니다.

> [!Note]
> 다음 섹션의 일부 단계에는 응용 프로그램 작성과 컴파일러 오류를 생성 합니다. 지침에는 응용 프로그램을 빌드하려면 시기를 지정 하십시오.

## <a name="student-entity-update"></a>학생의 엔터티 업데이트

![학생 엔터티](complex-data-model/_static/student-entity.png)

업데이트 *Models/Student.cs* 를 다음 코드로:

[!code-csharp[Main](intro/samples/cu/Models/Student.cs?name=snippet_BeforeInheritance&highlight=11,13,15,18,22,24-31)]

### <a name="the-required-attribute"></a>필수 특성

`Required` 특성 필드에 필수 이름 속성을 사용 합니다. `Required` nullable이 아닌 형식 예: 값 형식에 대 한 특성은 필요 하지 않습니다 (`DateTime`, `int`, `double`등.). Null 일 수 없는 형식 필수 필드로 자동으로 처리 됩니다.

`Required` 특성의 최소 길이 매개 변수를 대체할 수 있습니다는 `StringLength` 특성:

```csharp
[Display(Name = "Last Name")]
[StringLength(50, MinimumLength=1)]
public string LastName { get; set; }
```

### <a name="the-display-attribute"></a>표시 특성

`Display` 특성 캡션 텍스트 상자에 대 한 "이름", "Last Name", "전체 Name" 및 "등록 날짜입니다." 해야 함을 지정 기본 캡션을 예를 들어 "Lastname. 가" 단어를 분할 하지 공간이

### <a name="the-fullname-calculated-property"></a>계산 FullName 속성

`FullName`다른 두 개의 속성을 연결 하 여 생성 하는 값을 반환 하는 계산 된 속성이입니다. `FullName`get 접근자만에 설정할 수 없습니다. 더 `FullName` 열이 데이터베이스에 생성 됩니다.

## <a name="create-the-instructor-entity"></a>Instructor 엔터티 만들기

![Instructor 엔터티](complex-data-model/_static/instructor-entity.png)

만들 *Models/Instructor.cs* 를 다음 코드로:

[!code-csharp[Main](intro/samples/cu/Models/Instructor.cs?name=snippet_BeforeInheritance)]

여러 속성을 가지에서 동일는 `Student` 및 `Instructor` 엔터티. 이 시리즈의 뒷부분에 나오는 상속 구현 자습서에서는이 코드는 중복 제거를 리팩터링 되었습니다.

한 줄에 특성이 여러 개 있을 수 있습니다. `HireDate` 특성을 다음과 같이 작성할 수 있습니다.

```csharp
[DataType(DataType.Date),Display(Name = "Hire Date"),DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
```

### <a name="the-courseassignments-and-officeassignment-navigation-properties"></a>CourseAssignments 및 OfficeAssignment 탐색 속성

`CourseAssignments` 및 `OfficeAssignment` 속성은 탐색 속성입니다.

강사 courses 개수에 관계 없이 배울 수 하므로 `CourseAssignments` 컬렉션으로 정의 합니다.

```csharp
public ICollection<CourseAssignment> CourseAssignments { get; set; }
```

여러 엔터티를 보유 하는 탐색 속성 하는 경우:

* 에 항목 추가, 삭제 하 고 업데이트할 수는 목록 형식 이어야 합니다.

탐색 속성 유형은 다음과 같습니다.

* `ICollection<T>`
*  `List<T>`
*  `HashSet<T>`

경우 `ICollection<T>` 지정, EF 코어 만듭니다는 `HashSet<T>` 기본적으로 컬렉션입니다.

`CourseAssignment` 엔터티는 다 대 다 관계에 섹션에 설명 되어 있습니다.

Contoso 대학 비즈니스 규칙 강사 최대 하나의 office 포함 될 수 있는 상태입니다. `OfficeAssignment` 속성에는 단일 저장 `OfficeAssignment` 엔터티. `OfficeAssignment`없는 사무실 할당 된 경우 null입니다.

```csharp
public OfficeAssignment OfficeAssignment { get; set; }
```

## <a name="create-the-officeassignment-entity"></a>OfficeAssignment 엔터티 만들기

![OfficeAssignment 엔터티](complex-data-model/_static/officeassignment-entity.png)

만들 *Models/OfficeAssignment.cs* 를 다음 코드로:

[!code-csharp[Main](intro/samples/cu/Models/OfficeAssignment.cs)]

### <a name="the-key-attribute"></a>키 특성

`[Key]` 식별 하는 속성의 기본 키 (PK)로 속성 이름을 어질 때 classnameID 또는 ID가 아닌 다른 특성은 사용

사이 관계가 0 또는 1을 하나는 `Instructor` 및 `OfficeAssignment` 엔터티. 에 할당 된 강사 관련 하 여 사무실 할당만 존재 합니다. `OfficeAssignment` PK 이기도 해당 외래 키 (FK)에 `Instructor` 엔터티. EF 코어 자동으로 인식할 수 없습니다 `InstructorID` 의 PK로 `OfficeAssignment` 때문에:

* `InstructorID`ID 또는 classnameID 명명 규칙을 따르지 않는 합니다.

따라서는 `Key` 특성을 식별 하는 데 사용 됩니다 `InstructorID` 는 PK로:

```csharp
[Key]
public int InstructorID { get; set; }
```

기본적으로 EF 코어 확인 관계에 대 한 열이 때문에 데이터베이스 생성 된으로 키를 처리 합니다.

### <a name="the-instructor-navigation-property"></a>강사 탐색 속성

`OfficeAssignment` 탐색 속성에는 `Instructor` 엔터티는 null을 허용 하기 때문에:

* 참조 형식 (예: 클래스는 null을 허용)
* 강사는 사무실 할당이 없을 수 있습니다.


`OfficeAssignment` 엔터티에 비 nullable `Instructor` 탐색 속성 이므로:

* `InstructorID`null을 허용 하지입니다.
* 사무실 할당 강사 없이 존재할 수 없습니다.

경우는 `Instructor` 엔터티에 포함 된 관련 `OfficeAssignment` 엔터티에, 각 엔터티에 탐색 속성에 다른 하나에 대 한 참조입니다.

`[Required]` 특성에 적용할 수는 `Instructor` 탐색 속성:

```csharp
[Required]
public Instructor Instructor { get; set; }
```

위의 코드 관련된 강사 같아야 함을 지정 합니다. 위의 코드 필요 하지 않습니다. 때문에 `InstructorID` 외래 키 (PK는 이기도 함)은 nullable이 아닌 합니다.

## <a name="modify-the-course-entity"></a>과정 엔터티 수정

![과정 엔터티](complex-data-model/_static/course-entity.png)

업데이트 *Models/Course.cs* 를 다음 코드로:

[!code-csharp[Main](intro/samples/cu/Models/Course.cs?name=snippet_Final&highlight=2,10,13,16,19,21,23)]

`Course` 엔터티에 포함 된 외래 키 (FK) 속성 `DepartmentID`합니다. `DepartmentID`관련 가리키는 `Department` 엔터티. `Course` 엔터티에 `Department` 탐색 속성입니다.

EF 코어는 모델에 관련된 엔터티에 대 한 탐색 속성을 포함 하는 경우 데이터 모델에 대 한 외래 키 속성이 필요 하지 않습니다.

EF 코어 자동으로 만듭니다 FKs 데이터베이스에는 필요할 때마다. EF 코어 만듭니다 [숨기](https://docs.microsoft.com/ef/core/modeling/shadow-properties) 자동으로 만들어진된 FKs에 대 한 합니다. 쉽고 효율적으로 데이터 모델에는 외래 키를 포함 합니다. 업데이트를 수행할 수 있습니다. 예를 들어 모델에 외래 키 속성 `DepartmentID` 은 *하지* 포함 합니다. 때 과정 엔터티는 편집 하려면 인출 됩니다.

* `Department` 엔터티는 명시적으로 로드 된 경우 null입니다.
* 과정 엔터티를 업데이트 하려면는 `Department` 엔터티 먼저 가져와야 합니다.

때 외래 키 속성 `DepartmentID` 포함 된 데이터 모델에는 가져올 필요가 없습니다는 `Department` 업데이트 하기 전에 엔터티.

### <a name="the-databasegenerated-attribute"></a>DatabaseGenerated 특성

`[DatabaseGenerated(DatabaseGeneratedOption.None)]` 는 PK는 응용 프로그램에서 제공 하지 않고 하는 데이터베이스에서 생성 된 특성을 지정 합니다.

```csharp
[DatabaseGenerated(DatabaseGeneratedOption.None)]
[Display(Name = "Number")]
public int CourseID { get; set; }
```

기본적으로 EF 코어 PK 값 DB에 의해 생성 되어 가정 합니다. DB PK 생성 된 값은 일반적으로 가장 좋은 방법이 있습니다. 에 대 한 `Course` 사용자 엔터티는 PK. 지정 예를 들어 수학 부서에 대 한 1000 시리즈, 영어 부서에 대 한 2000 시리즈와 같은 과정 번호입니다.

`DatabaseGenerated` 특성 기본 값을 생성 하려면 사용할 수도 있습니다. 예를 들어 DB 날짜 필드는 행이 만들어지거나 업데이트 날짜를 기록 하려면 자동으로 생성할 수 있습니다. 자세한 내용은 참조 [속성 생성](https://docs.microsoft.com/ef/core/modeling/generated-properties)합니다.

### <a name="foreign-key-and-navigation-properties"></a>외래 키와 탐색 속성입니다.

외래 키 (FK) 속성 및 탐색 속성을는 `Course` 엔터티는 다음과 같은 관계를 반영 합니다.

이므로 과정 한 부서에 할당 된는 `DepartmentID` FK 및 `Department` 탐색 속성입니다.

```csharp
public int DepartmentID { get; set; }
public Department Department { get; set; }
```

과정을 학생을 등록 여러 개가 있을 수 있으므로 `Enrollments` 탐색 속성은 컬렉션:

```csharp
public ICollection<Enrollment> Enrollments { get; set; }
```

여러 강사 하 여 과정을 배울 수 있습니다 하므로 `CourseAssignments` 탐색 속성은 컬렉션:

```csharp
public ICollection<CourseAssignment> CourseAssignments { get; set; }
```

`CourseAssignment`설명 [나중](#many-to-many-relationships)합니다.

## <a name="create-the-department-entity"></a>부서 엔터티 만들기

![Department 엔터티](complex-data-model/_static/department-entity.png)

만들 *Models/Department.cs* 를 다음 코드로:

[!code-csharp[Main](intro/samples/cu/Models/Department.cs?name=snippet_Begin)]

### <a name="the-column-attribute"></a>Column 특성

이전에 `Column` 특성은 열 이름 매핑을 변경 하는 데 사용 되었습니다. 에 대 한 코드에는 `Department` 엔터티에 `Column` 특성 SQL 데이터 형식 매핑을 변경 하는 데 사용 됩니다. `Budget` 열은 SQL Server money 형식을 사용 하 여 DB에 정의 됩니다.

```csharp
[Column(TypeName="money")]
public decimal Budget { get; set; }
```

열 매핑은 일반적으로 필요 하지 않습니다. EF 코어에는 일반적으로 속성에 대 한 CLR 형식에 따라 적절 한 SQL Server 데이터 형식을 선택 합니다. CLR `decimal` SQL Server에 매핑됩니다 `decimal` 유형입니다. `Budget`통화에 대 한이 고 money 데이터 형식이 통화에 대 한 더 적합 합니다.

### <a name="foreign-key-and-navigation-properties"></a>외래 키와 탐색 속성입니다.

외래 키 및 탐색 속성은 다음과 같은 관계 반영 됩니다.

* 부서 수도 있습니다 관리자를 사용할 수 없습니다.
* 관리자는 항상 강사입니다. 따라서는 `InstructorID` 속성에 외래 키로 포함 되어는 `Instructor` 엔터티.

탐색 속성이 명명 `Administrator` 보유 하지만 `Instructor` 엔터티:

```csharp
public int? InstructorID { get; set; }
public Instructor Administrator { get; set; }
```

위의 코드에서 물음표 (?) 속성은 null을 허용을 지정 합니다.

부서는 Courses 탐색 속성 이므로 많은 과목을 포함할 수 있습니다.

```csharp
public ICollection<Course> Courses { get; set; }
```

참고: 일반적으로 EF 코어 모두 삭제를 하 고 다 대 다 관계에 대 한 nullable이 아닌 FKs에 대 한 있습니다. 연계 delete 순환 cascade 규칙 삭제 될 수 있습니다. 순환 모두 마이그레이션하는 추가 될 때 예외가 규칙 원인을 삭제 합니다.

예를 들어 경우는 `Department.InstructorID` 속성 nullable로 정의 되지 않았습니다.

* EF 코어 부서 삭제 될 때 강의 삭제 하는 cascade delete 규칙을 구성 합니다.
* 의도 된 동작 않습니다 부서 삭제 될 때 강의 삭제 합니다.

비즈니스 규칙이 요구 하는 경우는 `InstructorID` 속성을 허용 하지 않는 수 다음 fluent API 문을 사용 합니다.

 ```csharp
 modelBuilder.Entity<Department>()
    .HasOne(d => d.Administrator)
    .WithMany()
    .OnDelete(DeleteBehavior.Restrict)
 ```

위의 코드는 부서 강사 관계에 cascade delete를 해제합니다.

## <a name="update-the-enrollment-entity"></a>등록 엔터티 업데이트

등록 레코드가 한 과정을 학생 별로 수행 한 과정입니다.

![등록 엔터티](complex-data-model/_static/enrollment-entity.png)

업데이트 *Models/Enrollment.cs* 를 다음 코드로:

[!code-csharp[Main](intro/samples/cu/Models/Enrollment.cs?name=snippet_Final&highlight=1-2,16)]

### <a name="foreign-key-and-navigation-properties"></a>외래 키와 탐색 속성입니다.

외래 키 속성 및 탐색 속성은 다음과 같은 관계 반영 됩니다.

이므로 한 과정에 대 한 등록 레코드는 한 `CourseID` 외래 키 속성 및 `Course` 탐색 속성:

```csharp
public int CourseID { get; set; }
public Course Course { get; set; }
```

등록 레코드는 한 학생 있기 때문에 `StudentID` 외래 키 속성 및 `Student` 탐색 속성:

```csharp
public int StudentID { get; set; }
public Student Student { get; set; }
```

## <a name="many-to-many-relationships"></a>다 대 다 관계

사이 다 대 다 관계가 있는 `Student` 및 `Course` 엔터티. `Enrollment` 엔터티 역할 다 대 다 조인 테이블을 *페이로드를 사용한* 데이터베이스에 있습니다. "페이로드" 의미 하는 `Enrollment` 조인 된 테이블에 대 한 FKs 외에도 추가 데이터를 포함 하는 테이블 (이 경우는 PK 및 `Grade`).

다음 그림은 엔터티 다이어그램에서 이러한 관계 모양을 보여 줍니다. (이 다이어그램 EF에 대 한 EF 파워 도구를 사용 하 여 생성 된 6.x 합니다. 다이어그램 만들기의 일부가 아닌 자습서입니다.)

![학생 과정 다 대 다 관계](complex-data-model/_static/student-course.png)

각 관계 한쪽 끝에 별표 (*)부터 1에서 형식이 다른 경우 일 대 다 관계를 나타내는입니다.

경우는 `Enrollment` 테이블 등급 정보를 포함 하지 않은, 두 개의 FKs 포함 시키기만 하면 (`CourseID` 및 `StudentID`). 페이로드 없는 다 대 다 조인 테이블에는 순수 조인 테이블 (pjt가) 라고도 합니다.

`Instructor` 및 `Course` 엔터티 순수 조인 테이블을 사용 하 여 다 대 다 관계가 설정 되어 있습니다.

참고: EF 6.x 지원 다 대 다 관계가 되지만 EF 코어에 대 한 암시적 조인 테이블은 그렇지 않습니다. 자세한 내용은 참조 [다 대 다 관계 EF 코어 2.0에서](https://blog.oneunicorn.com/2017/09/25/many-to-many-relationships-in-ef-core-2-0-part-1-the-basics/)합니다.

## <a name="the-courseassignment-entity"></a>CourseAssignment 엔터티

![CourseAssignment 엔터티](complex-data-model/_static/courseassignment-entity.png)

만들 *Models/CourseAssignment.cs* 를 다음 코드로:

[!code-csharp[Main](intro/samples/cu/Models/CourseAssignment.cs)]

### <a name="instructor-to-courses"></a>강사 교육 과정-

![강사-Courses m:M](complex-data-model/_static/courseassignment.png)

강사 교육 과정 다 대 다 관계:

* 엔터티 집합으로 표현 되어야 하는 조인 테이블이 필요 합니다.
* 순수 조인 테이블 (페이로드 없는 테이블)입니다.

일반적으로 조인 엔터티 이름을 `EntityName1EntityName2`합니다. 예를 들어이 패턴을 사용 하 여 강사-Courses 조인 테이블은 `CourseInstructor`합니다. 그러나 관계를 설명 하는 이름을 사용 하는 것이 좋습니다.

데이터 모델은 단순 시작 및 증가 합니다. No 페이로드 조인 (PJTs) 자주 페이로드를 포함 하도록 개선 합니다. 설명이 포함 된 엔터티 이름을 사용 하 여 이름을 조인 테이블에 변경 될 때 변경 필요가 없습니다. 것이 가장 좋습니다, 조인 엔터티 자체 자연 (가능한 한 단어) 이름을 비즈니스 도메인에 있습니다. 예를 들어 설명서 및 고객 등급을 호출 하는 조인 엔터티와 연결할 수 없습니다. 강사 교육 과정 다 대 다 관계에 대 한 `CourseAssignment` 보다 선호 `CourseInstructor`합니다.

### <a name="composite-key"></a>복합 키

FKs는 null을 허용 하지 않습니다. 두 개의 FKs `CourseAssignment` (`InstructorID` 및 `CourseID`) 함께의 각 행을 고유 하 게 식별 된 `CourseAssignment` 테이블입니다. `CourseAssignment`전용된 PK. 필요 하지 않습니다. `InstructorID` 및 `CourseID` 복합 PK.로 기능 속성 복합 PKs EF 코어로 지정 하는 유일한 방법은 *fluent API*합니다. 다음 섹션에서는 복합 PK.를 구성 하는 방법을 보여 줍니다.

복합 키를 확인합니다.

* 여러 행을 하나의 과정에 대 한 사용할 수 있습니다.
* 여러 행은 하나의 강사에 허용 됩니다.
* 동일한 강사 및 과정에 대 한 여러 행을 사용할 수 없습니다.

`Enrollment` 이러한 종류의 중복이 가능 하므로 조인 엔터티 자체 PK을 정의 합니다. 방지 하려면 이러한 중복 항목:

* 외래 키 필드에 고유 인덱스를 추가 하거나
* 구성 `Enrollment` 비슷합니다 복합 기본 키가 있는 `CourseAssignment`합니다. 자세한 내용은 참조 [인덱스](https://docs.microsoft.com/ef/core/modeling/indexes)합니다.

## <a name="update-the-db-context"></a>DB 컨텍스트를 업데이트 합니다.

다음 강조 표시 된 코드를 추가 *Data/SchoolContext.cs*:

[!code-csharp[Main](intro/samples/cu/Data/SchoolContext.cs?name=snippet_BeforeInheritance&highlight=15-18,25-31)]

새 엔터티를 추가 하 고 구성 하는 위의 코드는 `CourseAssignment` 엔터티의 복합 PK.

## <a name="fluent-api-alternative-to-attributes"></a>특성에 대 한 fluent API 대안

`OnModelCreating` 코드에서는 앞의 메서드는 *fluent API* EF 핵심 동작을 구성할 수 있습니다. API는 일련의 단일 문으로 함께 메서드 호출을 가설에서 많이 사용 하기 때문에 "fluent" 라고 합니다. [코드 다음](https://docs.microsoft.com/ef/core/modeling/#methods-of-configuration) 은 fluent API의 예:

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Blog>()
        .Property(b => b.Url)
        .IsRequired();
}
```

이 자습서에서는 fluent API는 특성으로 수행할 수 없는 DB 매핑을 위해서만 사용 됩니다. 그러나 fluent API 서식, 유효성 검사 및 매핑 규칙 특성으로 수행할 수 있는 대부분을 지정할 수 있습니다.

와 같은 일부 특성 `MinimumLength` fluent API를 통해 적용할 수 없습니다. `MinimumLength`스키마를 변경 하지 않는 최소 길이 유효성 검사 규칙에만 적용 됩니다.

일부 개발자가 단독으로 보관할 수 있는 엔터티 클래스 "정리 합니다." fluent API를 사용 하는 것을 선호합니다 특성 및 fluent API를 함께 사용할 수 있습니다. 일부 구성만 수행할 수 있는 fluent api (복합 PK 지정) 있습니다. 특성에 수행할 수 있는 몇 가지 구성이 (`MinimumLength`). Fluent API 또는 특성을 사용 하기 위한 권장된 방식:

* 이 두 가지 방법 중 하나를 선택 합니다.
* 가능한 한 계속 선택한 방법을 사용 합니다.

이 사용 되는 특성 중 일부 자습서에 사용 됩니다.

* 유효성 검사에만 (예를 들어 `MinimumLength`).
* EF 핵심 구성만 (예를 들어 `HasKey`).
* 유효성 검사 및 EF 핵심 구성 (예를 들어 `[StringLength(50)]`).

Fluent API와 비교 하는 특성에 대 한 자세한 내용은 참조 [구성 방법이](https://docs.microsoft.com/ef/core/modeling/#methods-of-configuration)합니다.

## <a name="entity-diagram-showing-relationships"></a>관계를 보여 주는 엔터티 다이어그램

다음 그림 EF 파워 도구 만드는 완성 School 모델 다이어그램을 보여줍니다.

![엔터티 다이어그램](complex-data-model/_static/diagram.png)

위 다이어그램을 보여 줍니다.

* 일 대 다 관계의 여러 줄 (1 ~ \*).
* 사이 0 또는 1을 한 관계 선을 (1 0..1)에 `Instructor` 및 `OfficeAssignment` 엔터티.
* 0-또는---일대다 관계 선을 (0..1 대 *) 사이 `Instructor` 및 `Department` 엔터티.

## <a name="seed-the-db-with-test-data"></a>테스트 데이터로 DB 초기값

코드를 업데이트 *Data/DbInitializer.cs*:

[!code-csharp[Main](intro/samples/cu/Data/DbInitializer.cs?name=snippet_Final)]

위의 코드는 새 엔터티에 대 한 데이터를 제공합니다. 이 코드의 대부분을 새 엔터티 개체를 만들고 예제 데이터를 로드 합니다. 샘플 데이터는 테스트를 위해 사용 됩니다. 위의 코드는 다음과 같은 다 대 다 관계를 만듭니다.

* `Enrollments`
* `CourseAssignment`

참고: [EF 코어 2.1](https://github.com/aspnet/EntityFrameworkCore/wiki/Roadmap) 지원할 [데이터 시드는](https://github.com/aspnet/EntityFrameworkCore/issues/629)합니다.

## <a name="add-a-migration"></a>추가 마이그레이션

프로젝트를 빌드합니다. 프로젝트 폴더에 명령 창을 열고 다음 명령을 입력 합니다.

```console
dotnet ef migrations add ComplexDataModel
```

위의 명령은 가능한 데이터 손실에 대 한 경고를 표시 합니다.

```text
An operation was scaffolded that may result in the loss of data.
Please review the migration for accuracy.
Done. To undo this action, use 'ef migrations remove'
```

경우는 `database update` 명령이 실행, 다음과 같은 오류가 생성 됩니다.

```text
The ALTER TABLE statement conflicted with the FOREIGN KEY constraint "FK_dbo.Course_dbo.Department_DepartmentID". The conflict occurred in
database "ContosoUniversity", table "dbo.Department", column 'DepartmentID'.
```

마이그레이션이 시작 되 면 기존 데이터와, 기존 데이터와 충족 되지 않은 외래 키 제약 조건이 있을 수 있습니다. 이 자습서에서는 새 DB 만들어지면 외래 키 제약 조건을 위반 하지 않도록 합니다. 참조 [레거시 데이터와 foreign key 제약 조건을 수정](#fk) 현재 데이터베이스에서 외래 키 위반을 해결 하는 방법에 대 한 지침은 합니다.

## <a name="change-the-connection-string-and-update-the-db"></a>연결 문자열을 변경 하 고 DB 업데이트

업데이트 된 코드 `DbInitializer` 새 엔터티에 대 한 데이터를 추가 합니다. 새 빈 DB를 만들려면 EF 코어를 강제로:

* DB 연결 문자열 이름을 변경 *appsettings.json* ContosoUniversity3를 합니다. 새 이름에는 컴퓨터에서 사용 되지 않을 수 있는 이름 이어야 합니다.

    ```json
    {
      "ConnectionStrings": {
        "DefaultConnection": "Server=(localdb)\\mssqllocaldb;Database=ContosoUniversity3;Trusted_Connection=True;MultipleActiveResultSets=true"
      },
    ```

* 또는 사용 하 여 DB 삭제:

    * **SQL Server 개체 탐색기** (SSOX).
    * `database drop` CLI 명령을:

   ```console
   dotnet ef database drop
   ```

실행 `database update` 명령 창에서:

```console
dotnet ef database update
```

위의 명령은 모든 마이그레이션 실행 됩니다.

앱을 실행합니다. 실행 응용 프로그램 실행은 `DbInitializer.Initialize` 메서드. `DbInitializer.Initialize` 새 DB 채웁니다.

SSOX DB를 엽니다.

* 확장 된 **테이블** 노드. 생성된 된 테이블이 표시 됩니다.
* SSOX 이전에 열려 있으면 클릭는 **새로 고침** 단추입니다.

![SSOX의 테이블](complex-data-model/_static/ssox-tables.png)

검사는 **CourseAssignment** 테이블:

* 마우스 오른쪽 단추로 클릭는 **CourseAssignment** 테이블을 선택한 **데이터 보기**합니다.
* 확인 된 **CourseAssignment** 테이블 데이터가 포함 되어 있습니다.

![SSOX의 CourseAssignment 데이터](complex-data-model/_static/ssox-ci-data.png)

<a name="fk"></a>

## <a name="fixing-foreign-key-constraints-with-legacy-data"></a>레거시 데이터와 foreign key 제약 조건 수정

이 섹션은 선택 사항입니다.

마이그레이션이 시작 되 면 기존 데이터와, 기존 데이터와 충족 되지 않은 외래 키 제약 조건이 있을 수 있습니다. 프로덕션 데이터와 함께 기존 데이터를 마이그레이션하기에 단계를 수행 해야 합니다. 이 섹션에서는 외래 키 제약 조건 위반을 해결 하는 예제를 제공 합니다. 이러한 코드 변경 내용 백업 없이 만들지 못합니다. 항목도 변경 하지 않습니다 이러한 코드는 이전 단원을 완료 하 고 데이터베이스를 업데이트 합니다.

*{timestamp}_ComplexDataModel.cs* 파일 다음 코드를 포함 합니다.

[!code-csharp[Main](intro/samples/cu/Migrations/20171027005808_ComplexDataModel.cs?name=snippet_DepartmentID)]

위의 코드는 nullable이 아닌 추가 `DepartmentID` 외래 키에는 `Course` 테이블입니다. 행을 포함 하는 이전 자습서에서 DB `Course`, 마이그레이션 하 여 해당 테이블을 업데이트할 수 없습니다.

확인 하 고 `ComplexDataModel` 기존 데이터와 마이그레이션 작업:

* 새 열을 지정 하는 코드를 변경 (`DepartmentID`) 기본값입니다.
* 기본 부서 프록시로 "Temp" 라는 가짜 부서를 만듭니다.

### <a name="fix-the-foreign-key-constraints"></a>Foreign key 제약 조건 수정

업데이트는 `ComplexDataModel` 클래스 `Up` 메서드:

* 열기는 *{timestamp}_ComplexDataModel.cs* 파일입니다.
* 주석 줄을 추가 하는 코드는 `DepartmentID` 열을는 `Course` 테이블입니다.

[!code-csharp[Main](intro/samples/cu/Migrations/20171027005808_ComplexDataModel.cs?name=snippet_CommentOut&highlight=9-13)]

다음 강조 표시 된 코드를 추가 합니다. 새 코드 후로 이동 된 `.CreateTable( name: "Department"` 블록:[!code-csharp[Main](intro/samples/cu/Migrations/20171027005808_ComplexDataModel.cs?name=snippet_CreateDefaultValue&highlight=22-32)]

이전 변경 내용이 기존와 `Course` 행 후 "Temp" 부서에 관련 되도록는 `ComplexDataModel` `Up` 메서드를 실행 합니다.

프로덕션 응용 프로그램은:

* 코드 또는 추가 하는 스크립트가 포함 `Department` 행 및 관련 `Course` 행을 새 `Department` 행.
* "Temp" 부서 또는 기본값을 사용 하지 않을 `Course.DepartmentID `합니다.

다음 자습서에서는 관련된 데이터에 설명 합니다.

>[!div class="step-by-step"]
[이전](xref:data/ef-rp/migrations)
[다음](xref:data/ef-rp/read-related-data)