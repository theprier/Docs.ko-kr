---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-a-more-complex-data-model-for-an-asp-net-mvc-application
title: "ASP.NET MVC 응용 프로그램 (4 / 10)에 대 한 보다 복잡 한 데이터 모델을 만드는 | Microsoft Docs"
author: tdykstra
description: "Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 5 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/30/2013
ms.topic: article
ms.assetid: f81f3d80-3674-4d8e-a9b1-87feed1a93c9
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-a-more-complex-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 5283da2786d41c0ae06607185dd416aeb7d2b62a
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
<a name="creating-a-more-complex-data-model-for-an-aspnet-mvc-application-4-of-10"></a>ASP.NET MVC 응용 프로그램 (4 / 10)의 더 복잡 한 데이터 모델 만들기
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

[완료 된 프로젝트를 다운로드 합니다.](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 5 Code First 및 Visual Studio 2012를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대 한 정보를 참조 하십시오. [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다. 시작 부분에서 자습서 시리즈를 시작할 수 있습니다 또는 [이 장의 대 한 시작 프로젝트 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 여기에서 시작 하 고 있습니다.
> 
> > [!NOTE] 
> > 
> > 해결할 수 없는 문제에 직면 하는 경우 [완료 장 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 문제를 재현 하려고 합니다. 일반적으로 코드 완성 된 코드를 비교 하 여 문제에 솔루션을 찾을 수 있습니다. 몇 가지 일반적인 오류 및 해결 하는 방법에 대 한 참조 [오류 및 해결 방법입니다.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)


이전 자습서에서 사용한 세 가지 엔터티 작성 된 간단한 데이터 모델입니다. 이 자습서에서는 더 많은 엔터티 및 관계를 추가 합니다 및 서식 지정, 유효성 검사 및 데이터베이스 매핑 규칙을 지정 하 여 데이터 모델을 사용자 지정 합니다. 데이터 모델 사용자 지정 하는 두 가지 방법으로 표시 됩니다: 엔터티 클래스에 및 데이터베이스 컨텍스트 클래스에 코드를 추가 하 여 특성을 추가 하 여 합니다.

완료 되 면, 엔터티 클래스는 다음 그림에 표시 되는 완성 된 데이터 모델을 구성 하는:

![School_class_diagram](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image1.png)

## <a name="customize-the-data-model-by-using-attributes"></a>특성을 사용 하 여 데이터 모델을 사용자 지정

이 섹션의 서식, 유효성 검사 및 데이터베이스 매핑 규칙을 지정 하는 특성을 사용 하 여 데이터 모델을 사용자 지정 하는 방법을 배웁니다. 다음 섹션 중 몇 개에 대 한 자세한 만들게 한 후 `School` 추가 하 여 데이터 모델 특성 클래스에 이미 모델의 나머지 엔터티 형식에 대해 생성 되 고 만드는 새 클래스입니다.

### <a name="the-datatype-attribute"></a>데이터 형식 특성

학생 등록 날짜에 대 한 모든 웹 페이지의 현재 시간을 표시, 날짜와 함께 날짜는이 필드에 대 한 필요 하므로. 데이터 주석 특성을 사용 하 여 하나 만들 수 있습니다 코드는 데이터를 표시 하는 모든 보기에서 표시 형식을 해결 하는 변경 합니다. 특성을 추가 합니다 즉, 작업을 수행 하는 방법의 예를 보려면는 `EnrollmentDate` 속성에는 `Student` 클래스입니다.

*Models\Student.cs*, 추가 `using` 문에 `System.ComponentModel.DataAnnotations` 네임 스페이스 추가 `DataType` 및 `DisplayFormat` 특성을 `EnrollmentDate` 속성을 다음 예제와 같이:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,13-14)]

[DataType](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.datatypeattribute.aspx) 특성 데이터베이스 내장 형식 보다 구체적인 데이터 형식을 지정 하는 데 사용 됩니다. 이 경우에 포함 하려고 날짜와 시간에서 날짜를 추적 하 합니다. [DataType 열거형](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.datatype.aspx) 와 같은 대부분의 데이터 형식이에 제공 *날짜 "," 시간 "," PhoneNumber "," 통화 "," EmailAddress* 등입니다. `DataType` 특성을 통해 응용 프로그램에서 자동으로 유형별 기능을 제공하도록 설정할 수도 있습니다. 예를 들어 한 `mailto:` 에 대 한 링크를 만들 수 [DataType.EmailAddress](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.datatype.aspx), 날짜 선택 기가 제공 될 수 있습니다 및 [DataType.Date](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.datatype.aspx) 지 원하는 브라우저에서 [HTML5](http://html5.org/). [DataType](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.datatypeattribute.aspx) 특성 내보냅니다 HTML 5 [데이터-](http://ejohn.org/blog/html-5-data-attributes/) (발음 *데이터 대시*) HTML 5 브라우저 이해할 수 있는 특성입니다. [DataType](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.datatypeattribute.aspx) 특성 유효성을 검사 하지 않습니다.

`DataType.Date`는 표시되는 날짜의 서식을 지정하지 않습니다. 기본적으로 데이터 필드에서 서버에 따라 기본 형식에 따라 표시 [CultureInfo](https://msdn.microsoft.com/en-us/library/vstudio/system.globalization.cultureinfo(v=vs.110).aspx)합니다.

`DisplayFormat` 특성은 날짜 형식을 명시적으로 지정하는 데 사용됩니다.


[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample2.cs)]


`ApplyFormatInEditMode` 설정은 지정 된 형식에서 적용 해야 하는지도 값 편집을 위해 텍스트 상자에 표시 되 면을 지정 합니다. (않을 수 있는 일부 필드에 대 한-예를 들어 통화 값에 대 한 있습니다 하지 않을 텍스트 상자에 통화 기호 편집 합니다.)

사용할 수는 [DisplayFormat](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.displayformatattribute.aspx) 하지만 자체를 기준으로 특성은 일반적으로 사용 하는 것이 좋습니다는 [DataType](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.datatypeattribute.aspx) 도 특성입니다. `DataType` 특성에 전달 된 *의미 체계* 데이터의 화면에 렌더링 하는 방법을 반대로과를으로 볼 수 없는 다음과 같은 이점을 제공 `DisplayFormat`:

- 브라우저 (예: calendar 컨트롤, 로캘에 적합 한 통화 기호, 전자 메일 링크, 등을 표시 합니다.) HTML5 기능을 활성화할 수 있습니다.
- 기본적으로 브라우저에 따라 올바른 형식을 사용 하 여 데이터를 렌더링 합니다 프로그램 [로캘](https://msdn.microsoft.com/en-us/library/vstudio/wyzd2bce.aspx)합니다.
- [DataType](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.datatypeattribute.aspx) 특성 데이터를 렌더링 하는 오른쪽 필드 템플릿을 선택 하는 MVC 사용 하도록 설정할 수 (의 [DisplayFormat](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.displayformatattribute.aspx) 자체 문자열 서식 파일을 사용 하 여 사용 하는 경우). 자세한 내용은 Brad Wilson의을 참조 하십시오. [ASP.NET MVC 2 Templates](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html)합니다. (하지만 MVC 2 용으로 작성 된,이 문서 여전히에 적용 됩니다 ASP.NET MVC의 현재 버전입니다.)

사용 하는 경우는 `DataType` 특성을 지정 해야 날짜 필드와는 `DisplayFormat` 필드 Chrome 브라우저에서 올바르게 렌더링 하려면 또한 특성입니다. 자세한 내용은 참조 [이 StackOverflow 스레드](http://stackoverflow.com/questions/12633471/mvc4-datatype-date-editorfor-wont-display-date-value-in-chrome-fine-in-ie)합니다.

학생 인덱스 페이지를 다시 실행 하 고 등록 날짜에 대 한 번 더 이상 표시 됩니다. 동일한을 사용 하는 다른 보기에 대 한 거짓일는 `Student` 모델입니다.

![Students_index_page_with_formatted_date](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image2.png)

### <a name="the-stringlengthattribute"></a>StringLengthAttribute

데이터 유효성 검사 규칙 및 특성을 사용 하 여 메시지를 지정할 수도 있습니다. 사용자가을 이름에 대 한 50 개 이상의 문자를 입력 하지 마세요 되도록 한다고 가정 합니다. 이 제한 사항은 추가 하려면 추가 [StringLength](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) 특성에 `LastName` 및 `FirstMidName` 다음 예제와 같이 속성:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample3.cs?highlight=10,12)]

[StringLength](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) 특성 이름에 공백을 입력에서 사용자를 금지 되지는 않습니다. 사용할 수는 [정규식으로](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx) 특성을 입력에 제한을 적용 합니다. 예를 들어 다음 코드는 첫 번째 문자를 대문자로 변환 하 고 나머지 문자를 사전순으로 필요 합니다.

`[RegularExpression(@"^[A-Z]+[a-zA-Z""'\s-]*$")]`

[MaxLength](https://msdn.microsoft.com/en-us/library/System.ComponentModel.DataAnnotations.MaxLengthAttribute.aspx) 특성은 유사한 기능을 제공는 [StringLength](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) 특성 하지만 클라이언트 쪽을 제공 하지 않는 유효성 검사 합니다.

응용 프로그램을 실행 하 고 클릭는 **학생** 탭 합니다. 다음과 같은 오류가 있습니다.

*'SchoolContext' 컨텍스트를 백업 하는 모델 데이터베이스를 만든 후에 변경 되었습니다. Code First 마이그레이션을 사용 하 여 데이터베이스를 업데이트 하는 것이 좋습니다 ([https://go.microsoft.com/fwlink/?LinkId=238269](https://go.microsoft.com/fwlink/?LinkId=238269)).*

데이터베이스 모델 데이터베이스 스키마를 변경 해야 하는 방식으로 변경 되었습니다 및 Entity Framework에서 검색 되었습니다. UI를 사용 하 여 데이터베이스에 추가 하는 데이터 손실 없이 스키마를 업데이트 하려면 마이그레이션을 사용 합니다. 만들어진 데이터를 변경한 경우에 `Seed` 때문에 원래 상태로 변경할 수 있는 메서드는 [AddOrUpdate](https://msdn.microsoft.com/en-us/library/hh846520(v=vs.103).aspx) 에서 사용 하는 메서드는 `Seed` 메서드. ([AddOrUpdate](https://msdn.microsoft.com/en-us/library/hh846520(v=vs.103).aspx) 데이터베이스 용어에서는 "upsert" 작업에 해당 합니다.)

패키지 관리자 콘솔 (PMC)에서 다음 명령을 입력 합니다.

[!code-console[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample4.cmd)]

`add-migration MaxLengthOnNames` 명령 라는 파일을 만듭니다  *&lt;타임 스탬프&gt;\_MaxLengthOnNames.cs*합니다. 이 파일에는 현재 데이터 모델과 일치 하도록 데이터베이스를 업데이트 하는 코드가 들어 있습니다. 마이그레이션 파일 이름 앞에 타임 스탬프를 마이그레이션 요청 Entity Framework에서 사용 됩니다. 데이터베이스를 삭제 하는 경우 마이그레이션을 여러 건을 만든 후 또는 마이그레이션을 사용 하 여 프로젝트를 배포 하는 경우는 마이그레이션의 모든 생성 된 순서에 적용 됩니다.

실행 된 **만들기** 페이지 및 50 자 보다 긴 이름 중 하나를 입력 합니다. 50 자를 초과 하면 되는 즉시 클라이언트 쪽 유효성 검사 오류 메시지를 즉시 표시 합니다.

![클라이언트 쪽 val 오류](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image3.png)

### <a name="the-column-attribute"></a>Column 특성

클래스 및 속성을 데이터베이스에 매핑되는 방법을 제어 하려면 특성을 사용할 수도 있습니다. 이름을 사용한 경우를 가정해 볼 `FirstMidName` 첫 번째 이름에 대 한 필드 중간 이름 포함도 될 수 있으므로 필드입니다. 이름을 지정 하는 데이터베이스 열을 원하는 하지만 `FirstName`해당 이름에는 데이터베이스에 대 한 임시 쿼리를 작성 하는 사용자는 대개 때문에 있습니다. 이 매핑은를 사용할 수 있습니다는 `Column` 특성입니다.

`Column` 특성을 지정 하는 데이터베이스를 만들 때의 열은 `Student` 테이블에 매핑되는 `FirstMidName` 속성 이름이 지정 됩니다 `FirstName`합니다. 즉 때 코드 참조 `Student.FirstMidName`, 데이터에서 옵니다 또는에서 업데이트할 수는 `FirstName` 의 열은 `Student` 테이블입니다. 열 이름을 지정 하지 않으면, 속성 이름과 같은 이름이 주어 집니다.

사용 하 여 추가 대해 문을 [System.ComponentModel.DataAnnotations.Schema](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.schema.aspx) 및 열 이름 특성을는 `FirstMidName` 속성을 다음 강조 표시 된 코드에 나와 있는 것 처럼:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample5.cs?highlight=4,14)]

추가 [열 특성](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.schema.columnattribute.aspx) 하므로 데이터베이스 일치 하지 않습니다는 SchoolContext 백업 모델을 변경 합니다. 다른 마이그레이션 만들려면 PMC에서 다음 명령을 입력 합니다.

[!code-console[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample6.cmd)]

**서버 탐색기** (**데이터베이스 탐색기** for Web Express를 사용 하는 경우)을 두 번 클릭은 *학생* 테이블입니다.

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image4.png)

다음 이미지는 처음 두 마이그레이션 적용 되기 전의 원래 열 이름을 표시 합니다. 변경 하려면 열 이름 뿐만 아니라 `FirstMidName` 를 `FirstName`, 두 개의 이름 열에서 변경 `MAX` 길이를 50 자로 합니다.

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image5.png)

만들 수도 있습니다 데이터베이스를 사용 하 여 매핑 변경 시에만 [Fluent API](https://msdn.microsoft.com/en-us/data/jj591617)와이 자습서의 뒷부분에 나오는 표시 됩니다.

> [!NOTE]
> 이러한 엔터티 클래스의 모든 만들기를 완료 하기 전에 컴파일 하려고 하면 컴파일러 오류가 발생할 수 있습니다.


## <a name="create-the-instructor-entity"></a>Instructor 엔터티 만들기

![Instructor_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image6.png)

만들 *Models\Instructor.cs*, 템플릿 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample7.cs)]

여러 속성을 가지에서 동일는 `Student` 및 `Instructor` 엔터티. 에 [상속 구현](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md) 이 시리즈의 뒷부분에 나오는 자습서에서는이 중복 제거를 상속을 사용 하 여을 리팩터링 합니다 있습니다.

### <a name="the-required-and-display-attributes"></a>필수 특성을 표시 하 고

특성에는 `LastName` 속성 텍스트 상자에 대 한 캡션 (속성 이름 대신를 만드는 것이 "LastName" 공백 없이), "Last Name"를 해야 함을 값 50 자를 초과할 수 없습니다 및 필수 필드 임을 지정 합니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample8.cs)]

[StringLength 특성](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) 데이터베이스의 최대 길이 설정 하 고 클라이언트측 및 서버측 제공 ASP.NET MVC에 대 한 유효성을 검사 합니다. 이 특성에는 최소 문자열 길이 지정할 수도 있습니다 수 있지만 최소값 데이터베이스 스키마에 대 한 영향을 주지 않습니다. [필수 특성](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.requiredattribute.aspx) float 및 double, DateTime, int, 예: 값 형식에 필요 하지 않습니다. 값 형식은 기본적으로 필요 하므로 null 값을 할당할 수 없습니다. 제거할 수는 [필수 특성](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.requiredattribute.aspx) 하 고 교체에 대 한 최소 길이 매개 변수는 `StringLength` 특성:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample9.cs?highlight=2)]

강사 클래스를 다음과 같이 작성할 수도 수 있으므로 여러 특성을 한 줄에 넣을 수 있습니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample10.cs)]

### <a name="the-fullname-calculated-property"></a>FullName 계산 속성

`FullName`다른 두 개의 속성을 연결 하 여 생성 하는 값을 반환 하는 계산 된 속성이입니다. 만 따라서는 `get` 접근자와 아니요 `FullName` 열이 데이터베이스에 생성 됩니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

### <a name="the-courses-and-officeassignment-navigation-properties"></a>과정 및 OfficeAssignment 탐색 속성

`Courses` 및 `OfficeAssignment` 속성은 탐색 속성입니다. 가 이전에 설명한 대로 일반적으로 정의 된 [가상](https://msdn.microsoft.com/en-us/library/9fkccyh4(v=vs.110).aspx) 를 호출 하는 Entity Framework 기능을 가지도록 수 [한 지연 로딩이](https://msdn.microsoft.com/en-us/magazine/hh205756.aspx)합니다. 또한 탐색 속성에는 여러 엔터티 보유할 수, 하는 경우 해당 형식이 구현 해야 합니다는 [ICollection&lt;T&gt; ](https://msdn.microsoft.com/en-us/library/92t2ye13.aspx) 인터페이스입니다. (예를 들어 [IList&lt;T&gt; ](https://msdn.microsoft.com/en-us/library/5y536ey6.aspx) 잘못 한정 [a b l e&lt;T&gt; ](https://msdn.microsoft.com/en-us/library/9eekhta0.aspx) 때문에 `IEnumerable<T>` 구현 하지 않는 [추가 ](https://msdn.microsoft.com/en-us/library/63ywd54z.aspx).

강사 courses 개수에 관계 없이 배울 수 하므로 `Courses` 의 컬렉션으로 정의 `Course` 엔터티. 비즈니스 규칙 상태 강사 하나만 사용할 수 있습니다 하나 office 최대 하므로 `OfficeAssignment` 단일 정의 `OfficeAssignment` 엔터티 (발생할 수 있는 `null` 없는 사무실 할당 된 경우).

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

## <a name="create-the-officeassignment-entity"></a>OfficeAssignment 엔터티 만들기

![OfficeAssignment_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image7.png)

만들 *Models\OfficeAssignment.cs* 를 다음 코드로:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample13.cs)]

변경 내용을 저장 하 고 복사본을 수행 하지 않은 확인 하는 프로젝트를 빌드하고 붙여넣기 오류 컴파일러 catch 할 수 있습니다.

### <a name="the-key-attribute"></a>키 특성

사이 관계가 0 또는 1을 하나는 `Instructor` 및 `OfficeAssignment` 엔터티. 따라서 해당 기본 키가 해당 외래 키를 및 사무실 할당만 할당 된 강사를 기준으로 존재는 `Instructor` 엔터티. Entity Framework 자동으로 인식할 수 없습니다 하지만 `InstructorID` 주 데이터베이스의 이름이 때문에이 엔터티의 키는 `ID` 또는 *classname* `ID` 명명 규칙입니다. 따라서는 `Key` 특성 키로 식별 하는 데 사용 됩니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample14.cs)]

사용할 수도 있습니다는 `Key` 특성 엔터티의 기본 키가 있지만 다른 값 속성의 이름을 지정 하는 경우 `classnameID` 또는 `ID`합니다. 기본적으로 EF 확인 관계에 대 한 열이 때문에 데이터베이스 생성 된으로 키를 처리 합니다.

### <a name="the-foreignkey-attribute"></a>ForeignKey 특성

0 또는 1을 한 관계 또는 두 엔터티 간의 한 일 관계 없을 때 (사이 이러한 `OfficeAssignment` 및 `Instructor`), EF 관계의 끝은 주 서버와 종속 끝 작동 하지 않습니다. 한 일 관계에서 각 클래스는 다른 클래스를 참조 탐색 속성을 가집니다. [ForeignKey 특성](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx) 관계를 설정 하는 종속 클래스에 적용할 수 있습니다. 생략 하면는 [ForeignKey 특성](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx), 마이그레이션을 만들려고 할 때 다음과 같은 오류가:

'ContosoUniversity.Models.OfficeAssignment' 'ContosoUniversity.Models.Instructor' 형식 간 연결의 주 끝을 확인할 수 없습니다. 이 연결의 주 끝 관계 fluent API 나 데이터 주석을 사용 하 여 명시적으로 구성 되어야 합니다.

이 자습서의 뒷부분에 나오는 fluent API와이 관계를 구성 하는 방법을 보여줍니다.

### <a name="the-instructor-navigation-property"></a>강사 탐색 속성

`Instructor` 엔터티에 null을 허용 `OfficeAssignment` 탐색 속성 (하기 때문에 강사 사무실 할당 되지 않았을), 및 `OfficeAssignment` 엔터티에 비 nullable `Instructor` 탐색 속성 (이므로 사무실 할당 수 없습니다. 강사-없이 존재할 `InstructorID` 은 nullable이 아닌). 경우는 `Instructor` 엔터티에 포함 된 관련 `OfficeAssignment` 엔터티, 각 엔터티는 탐색 속성에 다른 하나에 대 한 참조를 갖습니다.

빠뜨릴 수는 `[Required]` 관련된 강사 있어야 하지만 (이 또한이 테이블에 키) InstructorID 외래 키가 null을 허용 하지 않아서 그럴 필요가 없습니다 지정 하려면 강사 탐색 속성에는 특성입니다.

## <a name="modify-the-course-entity"></a>과정 엔터티 수정

![Course_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image8.png)

*Models\Course.cs*, 추가한 코드를 이전를 다음 코드로 바꿉니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample15.cs)]

과정 엔터티에 포함 된 외래 키 속성이 `DepartmentID` 관련를 가리키는 `Department` 엔터티와 것에 `Department` 탐색 속성입니다. Entity Framework 관련된 엔터티에 대 한 탐색 속성을 사용 하는 경우 데이터 모델에 외래 키 속성을 추가할 수 필요 하지 않습니다. EF 자동으로 만듭니다 외래 키는 데이터베이스에는 필요할 때마다. 하지만 데이터 모델에 외래 키가 있는 업데이트를 수행할 수 쉽고 효율적으로. 을 편집 하려면 과정 엔터티를 가져올 때 예를 들어는 `Department` 엔터티는 null을 로드 하지 않는 하므로 과정 엔터티를 업데이트할 때 해야를 먼저 가져오지는 `Department` 엔터티. 때 외래 키 속성 `DepartmentID` 포함 된 데이터 모델에 가져올 필요가 없습니다는 `Department` 엔터티를 업데이트 하기 전에.

### <a name="the-databasegenerated-attribute"></a>DatabaseGenerated 특성

[DatabaseGenerated 특성](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.schema.databasegeneratedattribute.aspx) 와 [None](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.schema.databasegeneratedoption(v=vs.110).aspx) 에 매개 변수는 `CourseID` 기본 키 값은 사용자가 제공 하지 않고 하는 데이터베이스에서 생성 된 속성을 지정 합니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample16.cs)]

기본적으로 Entity Framework에서는 기본 키 값이 데이터베이스에서 생성 된을 가정 합니다. 즉, 대부분의 시나리오에서 원하는 합니다. 그러나 `Course` 엔터티를 다른 부서에 대 한 2000 계열 하나의 부서에 대 한 1000 계열과 같이 사용자가 지정한 과정 번호를 사용 하 고 등 합니다.

### <a name="foreign-key-and-navigation-properties"></a>외래 키 속성 및 탐색 속성

외래 키 속성 및 탐색 속성을는 `Course` 엔터티는 다음과 같은 관계를 반영 합니다.

- 이므로 과정 한 부서에 할당 된는 `DepartmentID` 외래 키와 `Department` 위에서 언급 한 이유는 탐색 속성입니다. 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample17.cs)]
- 과정을 학생을 등록 여러 개가 있을 수 있으므로 `Enrollments` 탐색 속성은 컬렉션: 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample18.cs)]
- 여러 강사 하 여 과정을 배울 수 있습니다 하므로 `Instructors` 탐색 속성은 컬렉션: 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample19.cs)]

## <a name="creating-the-department-entity"></a>Department 엔터티 만들기

![Department_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image9.png)

만들 *Models\Department.cs* 를 다음 코드로:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample20.cs)]

### <a name="the-column-attribute"></a>Column 특성

사용 하는 이전는 [열 특성](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.schema.columnattribute.aspx) 열 이름 매핑을 변경할 수 있습니다. 에 대 한 코드에서는 `Department` 엔터티에 `Column` 특성은 SQL 데이터 형식 매핑 SQL Server를 사용 하 여 열 정의할 수 있도록 변경 하는 데 사용 되 고 [money](https://msdn.microsoft.com/en-us/library/ms179882.aspx) 데이터베이스:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample21.cs)]

열 매핑 일반적으로 필요 하지 않은, Entity Framework는 일반적으로 속성에 대해 정의 하는 CLR 형식에 따라 적절 한 SQL Server 데이터 형식을 선택 합니다. CLR `decimal` SQL Server에 매핑됩니다 `decimal` 유형입니다. 하지만,이 경우 있습니다 열 통화 금액 보유 수 및 [money](https://msdn.microsoft.com/en-us/library/ms179882.aspx) 데이터 형식이 하는 데 보다 적합 합니다.

### <a name="foreign-key-and-navigation-properties"></a>외래 키 속성 및 탐색 속성

외래 키와 탐색 속성은 다음과 같은 관계 반영 됩니다.

- 부서 수도, 관리자가 없을 수 있습니다 및 관리자는 항상 강사 합니다. 따라서는 `InstructorID` 속성은 포함 하는 외래 키로는 `Instructor` 엔터티와 매개 변수 뒤에 추가 됩니다는 `int` 지정 null 허용으로 속성을 표시 하려면를 입력 합니다. 탐색 속성이 명명 `Administrator` 보유 하지만 `Instructor` 엔터티: 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample22.cs)]
- 부서 이므로 많은 과목 있을 수 있습니다는 `Courses` 탐색 속성: 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample23.cs)]

 > [!NOTE]
 > 규칙에 따라 Entity Framework에는 null을 허용 하지는 외래 키 및 다 대 다 관계에 대 한 하위 삭제를 수 있습니다. 따라서 이니셜라이저 코드 실행 하면 예외가 발생 하는 순환 cascade delete 규칙을 수 있습니다. 예를 들어 정의 하지는 `Department.InstructorID` null 허용으로 속성을 다음과 같은 예외 메시지가 때 얻는 이니셜라이저 실행: "참조 관계는 허용 되지 않는 순환 참조가 발생 합니다." 비즈니스 규칙에 필요한 경우 `InstructorID` 관계에 cascade delete를 사용 하지 않도록 설정 하려면 다음 fluent API를 사용 해야으로 nullable이 아닌 속성: 

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample24.cs)]


## <a name="modifying-the-student-entity"></a>학생 엔터티 수정

![Student_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image10.png)

*Models\Student.cs*, 추가한 코드를 이전를 다음 코드로 바꿉니다. 변경 내용은 강조 표시 됩니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample25.cs?highlight=12,15,24-27)]

## <a name="the-enrollment-entity"></a>등록 엔터티

 *Models\Enrollment.cs*를 다음 코드로 추가한 코드를 이전 대체

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample26.cs?highlight=16)]

### <a name="foreign-key-and-navigation-properties"></a>외래 키 속성 및 탐색 속성

외래 키 속성 및 탐색 속성은 다음과 같은 관계 반영 됩니다.

- 이므로 단일 과정에 대 한 등록 레코드는 한 `CourseID` 외래 키 속성 및 `Course` 탐색 속성: 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample27.cs)]
- 이므로 단일 학생에 대 한 등록 레코드는 한 `StudentID` 외래 키 속성 및 `Student` 탐색 속성: 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample28.cs)]

### <a name="many-to-many-relationships"></a>다 대 다 관계

간의 다 대 다 관계가 `Student` 및 `Course` 엔터티, 및 `Enrollment` 엔터티 역할 다 대 다 조인 테이블을 *페이로드를 사용한* 데이터베이스에 있습니다. 즉는 `Enrollment` 조인 된 테이블에 대 한 외래 키 외에도 추가 데이터를 포함 하는 테이블 (이 경우 기본 키에는 및 `Grade` 속성).

다음 그림은 엔터티 다이어그램에서 이러한 관계 모양을 보여 줍니다. (이 다이어그램을 사용 하 여 만들어졌습니다는 [Entity Framework 파워 도구](https://visualstudiogallery.msdn.microsoft.com/72a60b14-1581-4b9b-89f2-846072eff19d); 자습서의 일부가 아닌는 다이어그램을 만들어만 사용 되 고로 보여 줍니다.)

![Student-Course_many-to-many_relationship](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image11.png)

각 관계 선을 값은 1에서 한쪽 끝에 별표 (\*)에, 일 대 다 관계를 나타내는입니다.

경우는 `Enrollment` 테이블 등급 정보를 포함 하지 않은, 두 개의 외래 키를 포함 시키기만 하면 `CourseID` 및 `StudentID`합니다. 다 대 다 조인 테이블에 해당 하는 경우 *페이로드 없이* (또는 *순수 조인 테이블*) 데이터베이스에 전혀에 대 한 모델 클래스를 만들 필요가 없게 되 고 있습니다. `Instructor` 및 `Course` 엔터티에 이러한 종류의 다 대 다 관계 및 간에 엔터티 클래스가 없습니다.이 볼 수 있습니다.

![Instructor-Course_many-to-many_relationship](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image12.png)

그러나 조인 테이블에는 데이터베이스 필요는 다음 데이터베이스 다이어그램에 표시 된 것 처럼:

![Instructor-Course_many-to-many_relationship_tables](https://asp.net/media/2577802/Windows-Live-Writer_Creating-a.NET-MVC-Application-4-of-10h1_B662_Instructor-Course_many-to-many_relationship_tables_03e042cf-db89-4b4c-985a-e458351ada76.png)

Entity Framework를 자동으로 만듭니다는 `CourseInstructor` 테이블 및 있습니다 읽고 하지 직접 하 여 업데이트를 읽고 업데이트는 `Instructor.Courses` 및 `Course.Instructors` 탐색 속성입니다.

## <a name="entity-diagram-showing-relationships"></a>관계를 보여 주는 엔터티 다이어그램

다음은 Entity Framework 파워 도구 만들기 완료 된 School 모델 다이어그램입니다.

![School_data_model_diagram](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image13.png)

다 대 다 관계 선이 외에도 (\* 를 \*)와 일 대 다 관계 선 (1 ~ \*), 여기에서 볼 수는 0 또는 1을 하나 관계 선을 (1를 0..1) 사이 `Instructor` 및 `OfficeAssignment` 엔터티 및 0-또는---일대다 관계 선 (0..1 대 \*) 강사 및 Department 엔터티 간의 합니다.

## <a name="customize-the-data-model-by-adding-code-to-the-database-context"></a>데이터베이스 컨텍스트를 코드를 추가 하 여 데이터 모델을 사용자 지정

다음에 새 엔터티 추가 `SchoolContext` 클래스 및 일부 사용 하 여 매핑을 사용자 지정할 [fluent API](https://msdn.microsoft.com/en-us/data/jj591617) 호출 합니다. (API 이므로 "fluent" 가설 일련의 단일 문으로 함께 메서드 호출에서 주로 사용 됩니다.)

이 자습서에서는 특성으로 작업할 수 없는 데이터베이스 매핑을 위해서만 fluent API를 사용 합니다. 그러나 대부분의 서식, 유효성 검사 및 특성을 사용 하 여 수행할 수 있습니다는 매핑 규칙을 지정 하려면 fluent API를 사용할 수도 있습니다. 와 같은 일부 특성 `MinimumLength` fluent API를 통해 적용할 수 없습니다. 앞에서 설명한 대로 `MinimumLength` 는 스키마를 변경 하지 않는 클라이언트 및 서버 쪽 유효성 검사 규칙에만 적용 됩니다

일부 개발자가 단독으로 보관할 수 있는 엔터티 클래스 "정리 합니다." fluent API를 사용 하는 것을 선호합니다 원하는 되어만 fluent API를 사용 하 여 수행할 수 있는 몇 가지 사용자 지정 특성 및 fluent API를 함께 사용할 수 있습니다 하지만 일반적 방법이 권장된이 두 가지 방법 중 하나를 선택 하 고 가능한 한를 일관 되 게 사용 합니다.

새 엔터티 데이터 모델 및 특성을 사용 하 여 수행 하지 않은 데이터베이스 매핑을 수행를 추가 하려면 코드를 바꿉니다 *DAL\SchoolContext.cs* 를 다음 코드로:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample29.cs)]

새 문을 [OnModelCreating](https://msdn.microsoft.com/en-us/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx) 다 대 다 조인 테이블을 구성 하는 메서드:

- 다 대 다 관계에 대 한는 `Instructor` 및 `Course` 엔터티를 코드 조인 테이블에 대 한 테이블 및 열 이름을 지정 합니다. 코드 먼저 다 대 다 관계에 대해 구성할 수 있습니다이 코드를 사용 하지 않고 있지만 호출 하지 않는 경우 기본 이름을 같은 `InstructorInstructorID` 에 대 한는 `InstructorID` 열입니다.

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample30.cs)]

다음 코드에서는 방법 수를 사용 하 여 fluent API 특성 대신 간의 관계를 지정 하는의 예는 `Instructor` 및 `OfficeAssignment` 엔터티:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample31.cs)]

"Fluent API" 문을 수행 하는 백그라운드 방법은 참조는 [Fluent API](https://blogs.msdn.com/b/aspnetue/archive/2011/05/04/entity-framework-code-first-tutorial-supplement-what-is-going-on-in-a-fluent-api-call.aspx) 블로그 게시물입니다.

## <a name="seed-the-database-with-test-data"></a>테스트 데이터로 데이터베이스를 시드하십시오

코드는 *Migrations\Configuration.cs* 만든 새 엔터티에 대 한 데이터를 제공 하기 위해 다음 코드가 포함 된 파일입니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample32.cs)]

첫 번째 자습서에서 볼 수 있듯이이 코드의 대부분을 단순히 업데이트 하거나 새 엔터티 개체를 만들고 테스트를 위해 필요에 따라 속성에 샘플 데이터를 로드 합니다. 그러나 방법을 `Course` 다 대 다 관계가 있는 엔터티를와 `Instructor` 엔터티를 처리 됩니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample33.cs)]

만들 때 한 `Course` 개체를 초기화 하면는 `Instructors` 코드를 사용 하는 빈 컬렉션 탐색 속성 `Instructors = new List<Instructor>()`합니다. 그러면 추가할 수 `Instructor` 를이 관련 된 엔터티 `Course` 를 사용 하 여는 `Instructors.Add` 메서드. 빈 목록을 만들지 않은 경우 하는지 됩니다 이러한 관계를 추가할 수 있으므로 `Instructors` 속성은 null 되며 하지 않았던는 `Add` 메서드. 목록 초기화 생성자에 추가할 수도 있습니다.

## <a name="add-a-migration-and-update-the-database"></a>마이그레이션을 추가 하 고 데이터베이스를 업데이트 합니다.

PMC에서 입력 된 `add-migration` 명령:

`PM> add-Migration Chap4`

이 시점에서 데이터베이스를 업데이트 하려고 하면 다음과 같은 오류가 얻게 됩니다.

*ALTER TABLE 문을 FOREIGN KEY 제약 조건 충돌 "FK\_dbo입니다. 과정\_dbo입니다. 부서\_DepartmentID "입니다. 데이터베이스 "ContosoUniversity" 테이블 "dbo에에서 충돌이 발생 했습니다. 부서 ", 열 'DepartmentID'입니다.*

편집 된 &lt; *타임 스탬프&gt;\_Chap4.cs* 파일을 선택한 다음 코드를 변경 (SQL 문을 추가 하 고 수정는 `AddColumn` 문):

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample34.cs?highlight=14-18)]

(주석으로 처리 하거나 기존 삭제 `AddColumn` 새 대시보드를 추가 하거나 입력 하면 오류가 발생할 수 있습니다 때 줄는 `update-database` 명령입니다.)

마이그레이션에 기존 데이터를 실행할 때 외래 키 제약 조건을 만족 하려면 데이터베이스에 스텁 데이터를 삽입 해야 및 무엇 이제입니다. 생성 된 코드는 nullable이 아닌 추가 `DepartmentID` 외래 키에서 `Course` 테이블입니다. 이미 있을 경우에 행의 `Course` 는 코드를 실행 하는 경우 테이블의 `AddColumn` 값을 null이 될 수 없는 열에 SQL Server 알 없기 때문에 작업은 실패 합니다. 따라서 기본값을 새 열을 제공 하는 코드를 변경한 및 역할을 기본 부서를 "Temp" 라는 스텁 부서를 만들었습니다. 기존 경우 결과적으로 `Course` 경우 행은 모두에 연결 됩니다 "Temp" 부서,이 코드를 실행 합니다.

때는 `Seed` 메서드를 실행의 행을 삽입 합니다는 `Department` 기존 테이블과 것은 관련 `Course` 행이 해당 새 `Department` 행. UI에서 모든 과정을 추가 하지 않았다면, 다음 더 이상 해야 "Temp" 부서 또는 기본값에는 `Course.DepartmentID` 열입니다. 사용자 추가 과정 응용 프로그램을 사용 하 여 가능성을 허용 하려면 것도 업데이트 하려는 `Seed` 메서드 코드를 확인 하는 모든 `Course` 행 (의 이전 실행을 통해 삽입 하는 것 뿐 아니라는 `Seed` 메서드)가 유효한 `DepartmentID` 기본값을 제거 하기 전에 값 열에서 값과 "Temp" 부서를 삭제 합니다.

편집을 완료 한 후의 &lt; *타임 스탬프&gt;\_Chap4.cs* 파일, 입력는 `update-database` 마이그레이션을 실행 하는 PMC 명령을 합니다.

> [!NOTE]
> 스키마 변경 하므로 및 데이터를 마이그레이션하는 경우 다른 오류를 가져오려는 것 같습니다. 마이그레이션 오류를 해결할 수 없으면 발생 하는 경우 연결 문자열을 하거나 변경할 수 있습니다는 *Web.config* 파일 또는 데이터베이스를 삭제 합니다. 가장 간단한 방법은 데이터베이스의 이름을 바꾸려면 *Web.config* 파일입니다. 예를 들어 데이터베이스 이름을 CU로 변경\_는 다음과 같이 테스트 합니다.
> 
> [!code-xml[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample35.xml?highlight=1-2)]
> 
>  새 데이터베이스에서는 데이터가 없는 마이그레이션하려면 및 `update-database` 명령 작업이 오류 없이 완료 하는 것입니다. 데이터베이스를 삭제 하는 방법에 지침은 [Visual Studio 2012에서 데이터베이스를 삭제 하는 방법을](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/)합니다.


데이터베이스를 열 **서버 탐색기** , 예전 하 고 확장 하 고는 **테이블** 노드에서 모든 테이블 생성을 볼 수 있습니다. (있는 경우 **서버 탐색기** 이전 시점에서 열을 클릭는 **새로 고침** 단추입니다.)

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image14.png)

에 대 한 모델 클래스를 만들지 않은 `CourseInstructor` 테이블입니다. 이 테이블은 조인 테이블 간에 다 대 다 관계에 대 한 이전에 설명한 대로 `Instructor` 및 `Course` 엔터티.

마우스 오른쪽 단추로 클릭는 `CourseInstructor` 테이블을 선택한 **테이블 데이터 표시** 의 결과로 데이터가 있는지 확인 하는 `Instructor` 에 추가 하는 엔터티는 `Course.Instructors` 탐색 속성입니다.

![Table_data_in_CourseInstructor_table](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image15.png)

## <a name="summary"></a>요약

이제 더 복잡 한 데이터 모델 및 해당 데이터베이스 만들어졌습니다. 다음 자습서에서 관련된 데이터에 액세스 하는 다른 방법에 대해 자세히 설명 합니다.

다른 Entity Framework 리소스에 대 한 링크에서 확인할 수 있습니다는 [ASP.NET 데이터 액세스 콘텐츠 맵](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.

>[!div class="step-by-step"]
[이전](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[다음](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
