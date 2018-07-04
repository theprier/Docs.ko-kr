---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-a-more-complex-data-model-for-an-asp-net-mvc-application
title: (4 / 10) ASP.NET MVC 응용 프로그램을 위한 더 복잡 한 데이터 모델 만들기 | Microsoft Docs
author: tdykstra
description: Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 5 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/30/2013
ms.topic: article
ms.assetid: f81f3d80-3674-4d8e-a9b1-87feed1a93c9
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-a-more-complex-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: a7fbcf8dc41086764e1e8ba9055929bde132192a
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37375741"
---
<a name="creating-a-more-complex-data-model-for-an-aspnet-mvc-application-4-of-10"></a>(4 / 10) ASP.NET MVC 응용 프로그램을 위한 더 복잡 한 데이터 모델 만들기
====================
[Tom Dykstra](https://github.com/tdykstra)

[완료 된 프로젝트 다운로드](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 5 Code First 및 Visual Studio 2012를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대한 정보는 [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조하세요. 시작 부분에서 자습서 시리즈를 시작할 수 있습니다 또는 [이 장이에 대 한 시작 프로젝트 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 여기에서 시작 하 고 있습니다.
> 
> > [!NOTE] 
> > 
> > 해결할 수 없는 문제가 발생 하는 경우 [완성 된 장 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 문제를 재현 하려고 합니다. 일반적으로 코드의 완성 된 코드를 비교 하 여 문제에 솔루션을 찾을 수 있습니다. 몇 가지 일반적인 오류 및 해결 하는 방법에 대 한 참조 [오류 및 해결 방법입니다.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)


이전 자습서의 세 가지 엔터티로 구성 된 간단한 데이터 모델을 사용 하 여 작동 합니다. 이 자습서에서는 더 많은 엔터티 및 관계를 추가 합니다 및 서식 지정, 유효성 검사 및 데이터베이스 매핑 규칙을 지정 하 여 데이터 모델을 사용자 지정할 수 있습니다. 데이터 모델을 사용자 지정 하는 두 가지 방법 표시: 데이터베이스 컨텍스트 클래스에 코드를 추가 하 여 엔터티 클래스에 특성을 추가 하 여 합니다.

완료되면 엔터티 클래스는 다음 그림에 표시된 완성된 데이터 모델을 구성하게 됩니다.

![School_class_diagram](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image1.png)

## <a name="customize-the-data-model-by-using-attributes"></a>특성을 사용하여 데이터 모델 사용자 지정

이 섹션에서는 서식 지정, 유효성 검사 및 데이터베이스 매핑 규칙을 지정하는 특성을 사용하여 데이터 모델을 사용자 지정하는 방법을 배웁니다. 다음 섹션 중 일부에서는 전체 만듭니다 다음 `School` 추가 하 여 데이터 모델 특성 클래스에 이미 모델에 나머지 엔터티 형식에 대 한 새 클래스를 만들어 만들기.

### <a name="the-datatype-attribute"></a>DataType 특성

학생 등록 날짜의 경우, 이 필드에서 필요한 것은 날짜이지만 현재 모든 웹 페이지는 날짜와 함께 시간을 표시합니다. 데이터 주석 특성을 사용하면 데이터를 표시하는 모든 보기에서 표시 형식을 해결하는 하나의 코드 변경을 만들 수 있습니다. 수행 방법의 예제를 보려면 특성을 `Student` 클래스의 `EnrollmentDate` 속성에 추가합니다.

*Models\Student.cs*, 추가 `using` 문을 합니다 `System.ComponentModel.DataAnnotations` 네임 스페이스 추가 `DataType` 및 `DisplayFormat` 특성을 `EnrollmentDate` 속성을 다음 예와에서 같이:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,13-14)]

합니다 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) 특성은 데이터베이스 내장 형식 보다 구체적인 데이터 형식을 지정 하는 데 사용 됩니다. 이 경우에는 날짜 및 시간이 아닌 날짜만 추적하고자 합니다. 합니다 [DataType 열거형](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 와 같은 많은 데이터 형식을 제공 *날짜 "," 시간 "," PhoneNumber "," 통화 "," EmailAddress* 등입니다. `DataType` 특성을 통해 응용 프로그램에서 자동으로 유형별 기능을 제공하도록 설정할 수도 있습니다. 예를 들어, 한 `mailto:` 에 대 한 링크를 만들 수 있습니다 [DataType.EmailAddress](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx), 및 날짜 선택 기가 제공 될 수 있습니다 [DataType.Date](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 지 원하는 브라우저에서 [HTML5](http://html5.org/). [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) 특성에는 HTML 5 내보냅니다 [데이터](http://ejohn.org/blog/html-5-data-attributes/) (발음 *데이터 대시로*) HTML 5 브라우저가 인식할 수 있는 특성입니다. 합니다 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) 특성 유효성 검사를 제공 하지 않습니다.

`DataType.Date`는 표시되는 날짜의 서식을 지정하지 않습니다. 기본적으로 데이터 필드는 서버의 기본 형식에 따라 표시 됩니다 [CultureInfo](https://msdn.microsoft.com/library/vstudio/system.globalization.cultureinfo(v=vs.110).aspx)합니다.

`DisplayFormat` 특성은 날짜 형식을 명시적으로 지정하는 데 사용됩니다.


[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample2.cs)]


`ApplyFormatInEditMode` 설정은 지정 된 서식도 적용 되어야 함을 값 편집을 위해 텍스트 상자에 표시 되 면을 지정 합니다. (원하지 않을 수 있습니다 하는 일부 필드에 대 한-예를 들어 통화 값 하지 않을 텍스트 상자에 통화 기호 편집 합니다.)

사용할 수는 [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) 자체 하지만 특성은 일반적으로 사용 하는 것이 좋습니다는 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) 특성도 합니다. 합니다 `DataType` 특성에 전달 합니다 *의미 체계* 데이터의 화면에 렌더링 하는 방법과 반대로으로 가져올 수 없는 다음과 같은 이점을 제공 `DisplayFormat`:

- 브라우저는 HTML5 기능 (예: 달력 컨트롤, 로캘에 적합 한 통화 기호, 이메일 링크, 등을 표시 합니다.)를 설정할 수 있습니다.
- 기본적으로 브라우저에 따라 올바른 형식을 사용 하 여 데이터는 렌더링 프로그램 [로캘](https://msdn.microsoft.com/library/vstudio/wyzd2bce.aspx)합니다.
- [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) 특성에서 데이터를 렌더링할 올바른 필드 템플릿을 선택 하는 MVC를 설정할 수 있습니다. (합니다 [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) 에서 사용 하는 경우 자체 템플릿을 사용 하 여 문자열). 자세한 내용은 Brad Wilson의을 참조 하세요 [ASP.NET MVC 2 Templates](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html)합니다. (MVC 2 용으로 작성 된, 하지만이 문서에서는 여전히 적용를 ASP.NET MVC의 현재 버전)

사용 하는 경우는 `DataType` 특성 날짜 필드를 사용 하 여 지정 해야 합니다 `DisplayFormat` 필드 Chrome 브라우저에서 올바르게 렌더링 되도록 하기 위해도 특성입니다. 자세한 내용은 [이 StackOverflow 스레드](http://stackoverflow.com/questions/12633471/mvc4-datatype-date-editorfor-wont-display-date-value-in-chrome-fine-in-ie)합니다.

학생 인덱스 페이지를 다시 실행 하 고 등록 날짜에 대 한 번 이상 표시 됩니다. 동일 사용 하는 모든 보기에 대 한 true가 됩니다는 `Student` 모델입니다.

![Students_index_page_with_formatted_date](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image2.png)

### <a name="the-stringlengthattribute"></a>StringLengthAttribute

또한 데이터 유효성 검사 규칙 및 특성을 사용 하 여 메시지를 지정할 수 있습니다. 사용자가 이름을 50자 이하로 입력하였는지를 확인한다고 가정합니다. 이 제한에 추가 하려면 추가 [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) 특성을 합니다 `LastName` 및 `FirstMidName` 속성을 다음 예와에서 같이:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample3.cs?highlight=10,12)]

합니다 [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) 특성 이름에 공백을 입력에서 사용자를 방지 하지 못합니다. 사용할 수는 [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx) 입력에 제한을 적용 하는 특성입니다. 예를 들어 다음 코드는 첫 번째 문자를 대문자로를 사전순으로 나머지 문자는 필요 합니다.

`[RegularExpression(@"^[A-Z]+[a-zA-Z""'\s-]*$")]`

합니다 [MaxLength](https://msdn.microsoft.com/library/System.ComponentModel.DataAnnotations.MaxLengthAttribute.aspx) 특성은 유사한 기능을 제공 합니다 [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) 하지만 클라이언트 쪽을 제공 하지 않습니다 유효성 검사 합니다.

응용 프로그램을 실행 하 고 클릭 합니다 **학생** 탭 합니다. 다음 오류가 있습니다.

*'SchoolContext' 컨텍스트를 지 원하는 모델 데이터베이스를 만든 이후에 변경 되었습니다. Code First 마이그레이션을 사용 하 여 데이터베이스를 업데이트 하는 것이 좋습니다 ([https://go.microsoft.com/fwlink/?LinkId=238269](https://go.microsoft.com/fwlink/?LinkId=238269)).*

데이터베이스 스키마를 변경 해야 하는 방식으로 데이터베이스 모델이 변경 되었는지 및 Entity Framework 것을 감지 합니다. UI를 사용 하 여 데이터베이스에 추가 하는 데이터 손실 없이 스키마를 업데이트 하려면 마이그레이션을 사용 합니다. 가 만든 데이터를 변경한 경우는 `Seed` 때문에 원래 상태로 변경 되는 메서드를 [AddOrUpdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx) 에서 사용 하는 메서드를 `Seed` 메서드. ([AddOrUpdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx) 데이터베이스 용어에서 "upsert" 작업에 해당 합니다.)

PMC(패키지 관리자 콘솔)에서 다음 명령을 입력합니다.

[!code-console[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample4.cmd)]

합니다 `add-migration MaxLengthOnNames` 명령은 라는 파일을 만듭니다  *&lt;타임 스탬프&gt;\_MaxLengthOnNames.cs*합니다. 이 파일에 현재 데이터 모델과 일치 하도록 데이터베이스를 업데이트 하는 코드가 있습니다. 마이그레이션 파일 이름 앞에 타임 스탬프는 마이그레이션을 Entity Framework에서 사용 됩니다. 데이터베이스를 삭제 하는 경우 여러 마이그레이션을 만든 후 또는 마이그레이션을 사용 하 여 프로젝트를 배포 하는 경우, 모든 마이그레이션이 생성 된 순서 대로 적용 됩니다.

실행 합니다 **만들기** 페이지 및 50 자 보다 긴 이름을 입력 합니다. 50 자를 초과 하는 즉시 클라이언트 쪽 유효성 검사는 즉시 오류 메시지를 표시 합니다.

![클라이언트 쪽 val 오류](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image3.png)

### <a name="the-column-attribute"></a>열 특성

또한 특성을 사용하여 클래스 및 속성을 데이터베이스에 매핑하는 방법을 제어할 수 있습니다. 필드에 중간 이름이 포함될 수 있으므로 첫 번째 이름 필드에 이름 `FirstMidName`을 사용한 경우를 가정합니다. 하지만 데이터베이스에 임시 쿼리를 작성하는 사용자는 해당 이름이 익숙하기 때문에 데이터베이스 열 이름을 `FirstName`으로 하려고 합니다. 이 매핑을 수행하기 위해 `Column` 특성을 사용할 수 있습니다.

`Column` 특성은 데이터베이스를 만드는 시기를 지정하고 `FirstMidName` 속성에 매핑하는 `Student` 테이블의 열 이름은 `FirstName`이 됩니다. 즉, 코드가 `Student.FirstMidName`을 참조하는 경우 데이터는 `Student` 테이블의 `FirstName` 열에서 가져오거나 업데이트됩니다. 열 이름을 지정 하지 않으면, 속성 이름으로 동일한 이름을 제공 됩니다.

추가 하 여 문을 [System.ComponentModel.DataAnnotations.Schema](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.aspx) 열 이름 특성을 `FirstMidName` 속성을 다음 강조 표시 된 코드에 표시 된 대로:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample5.cs?highlight=4,14)]

추가 된 [열 특성](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx) 되므로 데이터베이스가 일치 하지 않습니다는 SchoolContext 백업 모델을 변경 합니다. 다른 마이그레이션을 만듭니다 PMC에서 다음 명령을 입력 합니다.

[!code-console[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample6.cmd)]

**서버 탐색기** (**데이터베이스 탐색기** for Web Express를 사용 하는 경우)를 두 번 클릭 합니다 *학생* 테이블입니다.

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image4.png)

다음 그림에서는 처음 두 마이그레이션을 적용 하기 전의 원래 열 이름을 보여 줍니다. 변경 된 열 이름 외에도 `FirstMidName` 하 `FirstName`, 두 개의 이름 열에서 변경 `MAX` 길이를 50 자로 합니다.

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image5.png)

변경할 수 있습니다도 데이터베이스 매핑을 사용 하는 [Fluent API](https://msdn.microsoft.com/data/jj591617)이 자습서의 뒷부분에서 살펴보겠지만, 합니다.

> [!NOTE]
> 이러한 엔터티 클래스의 모든 만들기를 완료 하기 전에 컴파일을 하려고 하면 컴파일러 오류가 발생할 수 있습니다.


## <a name="create-the-instructor-entity"></a>강사 엔터티 만들기

![Instructor_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image6.png)

만들 *Models\Instructor.cs*, 템플릿 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample7.cs)]

`Student` 및 `Instructor` 엔터티의 여러 속성은 동일합니다. 에 [상속 구현](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md) 이 시리즈의 뒷부분에 나오는 자습서를 리팩터링하여이 중복 제거를 상속을 사용 하 여 합니다.

### <a name="the-required-and-display-attributes"></a>필수 특성을 표시 하 고

특성을 `LastName` 속성 텍스트 상자에 대 한 캡션이 되도록 "Last Name" (속성 이름 대신 "LastName" 공백 없이 수), 및 값이 50 자 보다 길 수 없습니다는 필수 필드 임을 지정 합니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample8.cs)]

합니다 [StringLength 특성](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) 데이터베이스의 최대 길이 설정 하 고 클라이언트측 및 서버측 제공 ASP.NET MVC에 대 한 유효성을 검사 합니다. 이 특성의 최소 문자열 길이를 지정할 수도 있지만, 최소값은 데이터베이스 스키마에 영향을 주지 않습니다. 합니다 [필수 특성](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) float 및 double, DateTime, int, 같은 값 형식에 대 한 필요 하지 않습니다. 값 형식은 기본적으로 필요 하므로 null 값을 할당할 수 없습니다. 제거할 수도 있습니다는 [필수 특성](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) 에 대 한 최소 길이 매개 변수를 사용 하 여 대체 하 고는 `StringLength` 특성:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample9.cs?highlight=2)]

Instructor 클래스를 다음과 같이 작성할 수도 수 있도록 한 줄에 여러 특성을 넣을 수 있습니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample10.cs)]

### <a name="the-fullname-calculated-property"></a>FullName 계산 속성

`FullName`은 다른 두 개의 속성을 연결하여 생성되는 값을 반환하는 계산된 속성입니다. 만 있는 따라서를 `get` 접근자와 아니요 `FullName` 데이터베이스에 열이 생성 됩니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

### <a name="the-courses-and-officeassignment-navigation-properties"></a>과정 및 OfficeAssignment 탐색 속성

`Courses` 및 `OfficeAssignment` 속성은 탐색 속성입니다. 가 앞에서 설명한 대로 일반적으로 정의 됩니다 [가상](https://msdn.microsoft.com/library/9fkccyh4(v=vs.110).aspx) 를 호출 하는 Entity Framework 기능을 취할 수 있습니다 [지연 로드](https://msdn.microsoft.com/magazine/hh205756.aspx)합니다. 또한 탐색 속성이 여러 엔터티를 포함할 수, 하는 경우 해당 형식이 구현 해야 합니다 [ICollection&lt;T&gt; ](https://msdn.microsoft.com/library/92t2ye13.aspx) 인터페이스입니다. (예를 들어 [IList&lt;T&gt; ](https://msdn.microsoft.com/library/5y536ey6.aspx) 제외한 한정 [IEnumerable&lt;T&gt; ](https://msdn.microsoft.com/library/9eekhta0.aspx) 때문에 `IEnumerable<T>` 구현 하지 않는 [추가 ](https://msdn.microsoft.com/library/63ywd54z.aspx).

강사는 여러 강좌를 학습할 수 있습니다 이므로 `Courses` 컬렉션으로 정의 된 `Course` 엔터티. 비즈니스 규칙 상태는 강사가 최대 하나의 사무실 포함할 수 있습니다 따라서 `OfficeAssignment` 단일 정의 됩니다 `OfficeAssignment` entity (발생할 수 있는 `null` 사무실이 할당 되지 않은 경우).

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

## <a name="create-the-officeassignment-entity"></a>OfficeAssignment 엔터티 만들기

![OfficeAssignment_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image7.png)

만들 *Models\OfficeAssignment.cs* 다음 코드를 사용 하 여:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample13.cs)]

변경 내용을 저장 하 고 모든 복사를 수행 하지 않은 확인 하는 프로젝트를 빌드하고 붙여넣기 오류 컴파일러 catch 할 수 있습니다.

### <a name="the-key-attribute"></a>키 특성

-0-또는-일대일 관계가 없는 합니다 `Instructor` 및 `OfficeAssignment` 엔터티. 사무실 할당만 할당 된 강사에 관하여 존재 이므로 기본 키도 해당 외래 키를 `Instructor` 엔터티. Entity Framework 자동으로 인식할 수 없습니다. 하지만 `InstructorID` 주 이름과 따르지 때문에이 엔터티의 키를 `ID` 또는 *classname* `ID` 명명 규칙입니다. 따라서 `Key` 특성은 키로 식별하는 데 사용됩니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample14.cs)]

사용할 수도 있습니다는 `Key` 엔터티는 고유한 기본 키 수 있지만 다른 항목 속성의 이름을 하려는 경우 특성 `classnameID` 또는 `ID`합니다. 기본적으로 EF 식별 관계에 대 한 열이 때문에 비-데이터베이스에서 생성 된 키를 처리 합니다.

### <a name="the-foreignkey-attribute"></a>ForeignKey 특성

-0-또는-일대일 관계 나 두 엔터티 간에 일대일 관계가 있는 경우 (사이 이러한 `OfficeAssignment` 고 `Instructor`), EF는 관계의 끝은 주체 및 종속 끝은 사용할 수 없습니다. 한 일 관계 참조 탐색 속성을 다른 클래스에 각 클래스에 있습니다. 합니다 [ForeignKey 특성](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx) 관계를 설정 하는 종속 클래스에 적용할 수 있습니다. 생략 하면 합니다 [ForeignKey 특성](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx), 마이그레이션을 만들려고 할 때 다음 오류가 발생 하면:

형식 'ContosoUniversity.Models.OfficeAssignment' 및 'ContosoUniversity.Models.Instructor' 사이의 연결의 주 end을 확인할 수 없습니다. 이 연결의 주 끝 관계 fluent API 또는 데이터 주석을 사용 하 여 명시적으로 구성 되어야 합니다.

이 자습서의 뒷부분에 나오는 fluent API를 사용 하 여이 관계를 구성 하는 방법에 살펴보겠습니다.

### <a name="the-instructor-navigation-property"></a>강사 탐색 속성

합니다 `Instructor` 엔터티에 null을 허용 `OfficeAssignment` 탐색 속성 (강사는 사무실 할당 되지 않았을) 때문에 및 `OfficeAssignment` 엔터티에 허용 되지 않는 `Instructor` 탐색 속성 (사무실 할당 수 없습니다 때문에 강사 없이 존재할 `InstructorID` 는 nullable이 아닌). 경우는 `Instructor` 관련 된 `OfficeAssignment` 엔터티와 각 엔터티는 다른 하나는 해당 탐색 속성에서에 대 한 참조를 갖습니다.

배치할 수 있습니다는 `[Required]` 특성 강사 탐색 속성을 지정 하는 관련 된 강사가 있어야 합니다 (이 테이블에 키 이기도 함)는 InstructorID 외래 키를 nullable이 아닌 아니므로 그렇게 할 필요가 없습니다.

## <a name="modify-the-course-entity"></a>강좌 엔터티 수정

![Course_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image8.png)

*Models\Course.cs*, 다음 코드를 사용 하 여 앞서 추가한 코드를 대체 합니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample15.cs)]

강좌 엔터티 외래 키 속성이 `DepartmentID` 가리키는 관련 `Department` 엔터티와 것에 `Department` 탐색 속성입니다. Entity Framework는 관련된 엔터티에 대한 탐색 속성이 있는 경우 사용자가 외래 키 속성을 데이터 모델에 추가하지 않아도 됩니다. EF 자동으로 만듭니다 외래 키는 데이터베이스에는 필요할 때마다. 하지만 데이터 모델에 외래 키가 있으면 더 간단하고 더 효율적으로 업데이트를 수행할 수 있습니다. 편집할 강좌 엔터티를 가져올 경우에 예를 들어 합니다 `Department` 엔터티가 null 로드 하지 있으므로 강좌 엔터티를 업데이트할 때 있다면 먼저 가져올는 `Department` 엔터티. 때 외래 키 속성 `DepartmentID` 포함 된 데이터 모델에 가져올 필요가 없습니다를 `Department` 엔터티를 업데이트 하기 전에 합니다.

### <a name="the-databasegenerated-attribute"></a>DatabaseGenerated 특성

[DatabaseGenerated 특성](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedattribute.aspx) 사용 하 여를 [없음](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedoption(v=vs.110).aspx) 매개 변수는 `CourseID` 는 기본 키 값은 사용자가 제공한 보다는 데이터베이스에서 생성 된 속성을 지정 합니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample16.cs)]

기본적으로 Entity Framework는 기본 키 값이 데이터베이스에서 생성 되는 가정 합니다. 이는 대부분의 시나리오에서 사용자가 원하는 것입니다. 그러나 `Course` 엔터티를 다른 부서에 대 한 2000 시리즈 하나의 부서에 대 한 1000 시리즈와 같은 사용자 지정 강좌 번호를 사용 하 여 및 등 됩니다.

### <a name="foreign-key-and-navigation-properties"></a>외래 키 속성과 탐색

외래 키 속성과 탐색 속성을는 `Course` 엔터티는 다음과 같은 관계를 반영 합니다.

- 강좌는 한 부서에 할당되므로, 위에서 언급한 이유로 `DepartmentID` 외래 키와 `Department` 탐색 속성이 있습니다. 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample17.cs)]
- 강좌에는 등록된 학생이 여러 명 있을 수 있으므로 `Enrollments` 탐색 속성은 컬렉션입니다. 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample18.cs)]
- 여러 강사가 한 강좌를 수업할 수 있으므로 `Instructors` 탐색 속성은 컬렉션입니다. 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample19.cs)]

## <a name="creating-the-department-entity"></a>부서 엔터티를 만들기

![Department_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image9.png)

만들 *Models\Department.cs* 다음 코드를 사용 하 여:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample20.cs)]

### <a name="the-column-attribute"></a>열 특성

사용 하는 이전를 [열 특성](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx) 열 이름 매핑을 변경 합니다. 코드에서를 `Department` 엔터티는 `Column` SQL 데이터 형식 매핑 열은 SQL Server를 사용 하 여 정의할 수 있도록 변경 하려면 특성이 사용 되 [money](https://msdn.microsoft.com/library/ms179882.aspx) 데이터베이스:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample21.cs)]

열 매핑 아니므로 일반적으로 필요한 Entity Framework에는 일반적으로 속성에 대해 정의 하는 CLR 형식에 따라 적절 한 SQL Server 데이터 형식을 선택 합니다. CLR `decimal` 형식은 SQL Server `decimal` 유형에 매핑됩니다. 하지만 경우 열 통화 금액이 포함 되어야 하며 [money](https://msdn.microsoft.com/library/ms179882.aspx) 데이터 형식이 더 적합 합니다.

### <a name="foreign-key-and-navigation-properties"></a>외래 키 속성과 탐색

외래 키 및 탐색 속성은 다음과 같은 관계를 반영합니다.

- 부서는 관리자가 있을 수도 있고 없을 수도 있으며, 관리자는 항상 강사입니다. 따라서를 `InstructorID` 속성은 외래 키로 포함를 `Instructor` 엔터티와 물음표 뒤에 추가 됩니다는 `int` 지정 null 허용으로 속성을 표시 하려면를 입력 합니다. 탐색 속성의 이름은 `Administrator` 보유 하지만 `Instructor` 엔터티: 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample22.cs)]
- 부서 이므로 강좌가 많이 있을 수 있습니다는 `Courses` 탐색 속성: 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample23.cs)]

  > [!NOTE]
  > 규칙에 따라 Entity Framework는 null 비허용 외래 키 및 다대다 관계에 대한 하위 삭제를 사용하도록 허용합니다. 이 이니셜라이저 코드를 실행 하는 경우 예외가 발생 하는 순환 계단식 삭제 규칙이 발생할 수 있습니다. 예를 들어, 정의 되지 않은 경우는 `Department.InstructorID` null 허용으로 속성을 다음과 같은 예외 메시지가 때 얻는 이니셜라이저가 실행: "참조 관계는 허용 되지 않는 순환 참조가 발생 합니다." 비즈니스 규칙에 필요한 경우 `InstructorID` nullable이 아닌 속성을 해야 다음 흐름 API를 사용 하 여 관계에서 계단식 삭제를 사용 하지 않도록 설정 합니다. 

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample24.cs)]


## <a name="modifying-the-student-entity"></a>학생 엔터티를 수정합니다.

![Student_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image10.png)

*Models\Student.cs*, 다음 코드를 사용 하 여 앞서 추가한 코드를 대체 합니다. 변경 내용은 강조 표시되어 있습니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample25.cs?highlight=12,15,24-27)]

## <a name="the-enrollment-entity"></a>등록 엔터티

 *Models\Enrollment.cs*, 다음 코드를 사용 하 여 앞서 추가한 코드를 대체

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample26.cs?highlight=16)]

### <a name="foreign-key-and-navigation-properties"></a>외래 키 속성과 탐색

외래 키 속성 및 탐색 속성은 다음 관계를 반영합니다.

- 등록 레코드는 단일 강좌에 해당하므로 `CourseID` 외래 키 속성 및 `Course` 탐색 속성이 있습니다. 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample27.cs)]
- 등록 레코드는 단일 학생에 해당하므로 `StudentID` 외래 키 속성 및 `Student` 탐색 속성이 있습니다. 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample28.cs)]

### <a name="many-to-many-relationships"></a>다대다 관계

간에 다 대 다 관계가 있기를 `Student` 및 `Course` 엔터티, 및 `Enrollment` 엔터티-다대다 조인 테이블로 작동 *페이로드를 사용 하 여* 데이터베이스에서. 즉 합니다 `Enrollment` 테이블에 조인된 된 테이블에 대 한 외래 키 외에도 데이터가 추가 (이 경우 기본 키에서 및 `Grade` 속성).

다음 그림은 이러한 관계 모양을 엔터티 다이어그램으로 보여 줍니다. (이 다이어그램은 사용 하 여 생성 된 합니다 [Entity Framework 파워 도구가](https://visualstudiogallery.msdn.microsoft.com/72a60b14-1581-4b9b-89f2-846072eff19d)자습서의 일부가 아닌 다이어그램 만들기만 사용 되 고 그림 으로만.)

![Student-Course_many-to-many_relationship](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image11.png)

각 관계 줄에 하나의 끝과 별표에 1 (\*)에서 다른-다 관계를 나타내는입니다.

경우는 `Enrollment` 테이블에 등급 정보가 포함 되지 않은, 두 개의 외래 키를 포함 해야 `CourseID` 고 `StudentID`입니다. 다 대 다 조인 테이블에 해당 하는 경우 *페이로드 없는* (또는 *순수 조인 테이블*) 데이터베이스에 및 전혀에 대 한 모델 클래스를 만들 필요가 없습니다. 합니다 `Instructor` 고 `Course` 엔터티가 해당 종류의 다 대 다 관계에 있고이 서로 엔터티 클래스가 없습니다. 알 수 있듯이:

![Instructor-Course_many-to-many_relationship](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image12.png)

조인 테이블이 데이터베이스에 있지만 필요한 다음 데이터베이스 다이어그램에 표시 된 것 처럼:

![Instructor-Course_many-to-many_relationship_tables](https://asp.net/media/2577802/Windows-Live-Writer_Creating-a.NET-MVC-Application-4-of-10h1_B662_Instructor-Course_many-to-many_relationship_tables_03e042cf-db89-4b4c-985a-e458351ada76.png)

Entity Framework를 자동으로 만듭니다는 `CourseInstructor` 읽기 및 업데이트 직접 읽기 및 업데이트 하 여 테이블에 `Instructor.Courses` 고 `Course.Instructors` 탐색 속성입니다.

## <a name="entity-diagram-showing-relationships"></a>관계를 보여 주는 엔터티 다이어그램

다음 그림에는 Entity Framework 파워 도구가 완벽한 School 모델을 만드는 다이어그램이 나와 있습니다.

![School_data_model_diagram](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image13.png)

다 대 다 관계 줄 외에도 (\* 하 \*) 및-일대다 관계 줄 (1 \*), 여기 보이는--0-또는-일대일 관계 줄 (1 ~ 0..1) 간에 `Instructor` 및 `OfficeAssignment` 엔터티 및 0-또는--일대다 관계 줄 (0..1 ~ \*) 강사 및 부서 엔터티 간의 합니다.

## <a name="customize-the-data-model-by-adding-code-to-the-database-context"></a>데이터베이스 컨텍스트를 코드를 추가 하 여 데이터 모델을 사용자 지정

다음 새 엔터티를 추가 합니다 `SchoolContext` 클래스 및 일부를 사용 하 여 매핑을 사용자 지정할 [fluent API](https://msdn.microsoft.com/data/jj591617) 호출 합니다. (API 이므로 "흐름" 일련의 메서드 호출을 단일 명령문으로 함께 연결 하 여 자주 사용 됩니다.)

이 자습서에서는 특성을 사용 하 여 수행할 수 없는 데이터베이스 매핑에 대해서만 fluent API를 사용할 수 있습니다. 그러나 대부분의 서식 지정, 유효성 검사 및 매핑 규칙을 지정하는 데 흐름 API를 사용할 수 있습니다. `MinimumLength`와 같은 일부 특성은 흐름 API를 통해 적용할 수 없습니다. 앞서 설명한 대로 `MinimumLength` 스키마를 변경 하지는 클라이언트 및 서버 쪽 유효성 검사 규칙에만 적용 됩니다

일부 개발자는 흐름 API를 단독으로 사용하는 것을 선호하므로 자신의 엔터티 클래스를 “정리”할 수 있습니다. 원하는 경우 특성과 흐름 API를 섞을 수 있으며, 흐름 API를 사용해야만 수행할 수 있는 몇 가지 사용자 지정이 있습니다. 하지만 일반적으로 이러한 두 가지 방법 중 하나를 선택하여 가능한 한 일관되게 사용하는 것이 좋습니다.

새 엔터티 데이터 모델 및 특성을 사용 하 여 작업을 수행 하지 않은 데이터베이스 매핑을 수행을 추가 하려면 코드를 바꿉니다 *DAL\SchoolContext.cs* 다음 코드를 사용 하 여:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample29.cs)]

새 명령문을 [OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx) 다 대 다 조인 테이블을 구성 하는 메서드:

- 다 대 다 관계에 대 한 합니다 `Instructor` 및 `Course` 코드 엔터티를 조인 테이블에 대 한 테이블 및 열 이름을 지정 합니다. 코드 먼저 다 대 다 관계에 대해 구성할 수 있습니다이 코드를 사용 하지 않고 있지만 호출 하지 않으면 기본 이름이 같은 `InstructorInstructorID` 에 대 한는 `InstructorID` 열입니다.

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample30.cs)]

다음 코드를 어떻게 수는 데 흐름 API 특성 대신 간의 관계를 지정의 예를 제공 합니다 `Instructor` 및 `OfficeAssignment` 엔터티:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample31.cs)]

백그라운드에서 수행 하는 "fluent API" 명령문에 대 한 내용은 참조는 [Fluent API](https://blogs.msdn.com/b/aspnetue/archive/2011/05/04/entity-framework-code-first-tutorial-supplement-what-is-going-on-in-a-fluent-api-call.aspx) 블로그 게시물.

## <a name="seed-the-database-with-test-data"></a>테스트 데이터로 데이터베이스 시드

코드를 대체 합니다 *migrations\ configuration.cs* 만든 새 엔터티에 대 한 시드 데이터를 제공 하기 위해 다음 코드를 사용 하 여 파일입니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample32.cs)]

첫 번째 자습서에서 살펴본 것 처럼이 코드의 대부분은 단순히 업데이트 또는 새 엔터티 개체 만들고 테스트 하는 데 필요한 속성에 샘플 데이터를 로드 합니다. 그러나 하는 방법을 `Course` 다 대 다 관계가 있는 엔터티를 사용 하 여는 `Instructor` 엔터티를 처리 합니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample33.cs)]

만들 때를 `Course` 개체를 초기화 합니다 `Instructors` 코드를 사용 하 여 빈 컬렉션으로 탐색 속성 `Instructors = new List<Instructor>()`합니다. 따라서 추가할 `Instructor` 이 관련 된 엔터티 `Course` 사용 하 여를 `Instructors.Add` 메서드. 빈 목록을 만들지 않은 경우 수 이러한 관계를 추가 하기 때문에 합니다 `Instructors` 속성은 null 되며 부족할는 `Add` 메서드. 목록 초기화를 사용 하는 생성자에 추가할 수도 있습니다.

## <a name="add-a-migration-and-update-the-database"></a>마이그레이션을 추가 하 고 데이터베이스를 업데이트 합니다.

PMC에서 다음을 입력 합니다 `add-migration` 명령:

`PM> add-Migration Chap4`

이 시점에서 데이터베이스를 업데이트 하려고 하면 다음 오류가 표시 됩니다.

*ALTER TABLE 문이 FOREIGN KEY 제약 조건 충돌 "FK\_dbo입니다. 과정\_dbo입니다. 부서\_DepartmentID "입니다. 데이터베이스 "ContosoUniversity", "dbo 테이블에서에서 충돌이 발생 했습니다. 부서 ", 열 'DepartmentID'입니다.*

편집 된 &lt; *타임 스탬프&gt;\_Chap4.cs* 파일을 선택한 다음 코드를 변경 (SQL 문을 추가 하 고 수정는 `AddColumn` 문):

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample34.cs?highlight=14-18)]

(주석으로 처리 하거나 기존 삭제 해야 `AddColumn` 새 대시보드를 더하거나 입력할 때 오류를 얻게 하는 경우 줄을 `update-database` 명령입니다.)

기존 데이터와 마이그레이션을 실행 하는 경우에 따라 이제 하 고 계시는 및 foreign key 제약 조건을 만족 하도록 데이터베이스에 스텁 데이터를 삽입 해야 합니다. 생성 된 코드를 추가 하는 허용 되지 않는 `DepartmentID` 외래 키를 `Course` 테이블입니다. 행에 이미 있는 경우는 `Course` 코드를 실행 하는 경우 테이블을 `AddColumn` SQL Server null 일 수 없는 열에 삽입할 값을 알지 때문에 이러한 작업이 실패 합니다. 따라서 새 열에 기본값을 제공 하도록 코드를 변경한 및 기본 부서로 작동 하도록 "Temp" 라는 스텁 부서를 만들었습니다. 결과적으로 기존 있으면 `Course` 경우 행이 코드가 실행 되는 모든 수 관련 되므로 "Temp" 부서, 합니다.

경우는 `Seed` 메서드를 실행에서 행을 삽입 합니다 합니다 `Department` 테이블 하며 기존 관련 됩니다 `Course` 이러한 새 행 `Department` 행. UI에서 모든 강좌를 추가 하지 않았다면, 더 이상 해야 "Temp" 부서 또는 기본값에는 `Course.DepartmentID` 열입니다. 에 사용자 추가 과정 응용 프로그램을 사용 하 여 가능성에 대 한 허용 하려면 또한 하려는 업데이트를 `Seed` 되도록 메서드 코드 모든 `Course` 행 (뿐 아니라의 이전 실행으로 삽입 합니다 `Seed` 메서드)가 유효한 `DepartmentID` 값 기본값을 제거 하기 전에 열에서 값과 "Temp" 부서를 삭제 합니다.

편집을 마친 후는 &lt; *타임 스탬프&gt;\_Chap4.cs* 파일을 입력 합니다 `update-database` 마이그레이션을 실행 하는 PMC에서 명령을 합니다.

> [!NOTE]
> 스키마 변경 하므로 및 데이터를 마이그레이션하는 경우 다른 오류가 것이 가능 합니다. 하는 해결할 수 없는 마이그레이션 오류가 발생 하는 경우의 연결 문자열 하거나 변경할 수 있습니다 합니다 *Web.config* 파일 또는 데이터베이스를 삭제 합니다. 가장 간단한 방법은 데이터베이스의 이름을 바꾸려면 *Web.config* 파일입니다. 예를 들어, CU로 데이터베이스 이름을 변경\_다음과에서 같이 테스트 합니다.
> 
> [!code-xml[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample35.xml?highlight=1-2)]
> 
>  새 데이터베이스에 데이터가 없습니다. 마이그레이션할 및 `update-database` 명령은 오류 없이 완료 될 가능성이 훨씬 더 높습니다. 데이터베이스를 삭제 하는 방법에 지침은 [Visual Studio 2012에서 데이터베이스를 삭제 하는 방법](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/)합니다.


데이터베이스를 엽니다 **서버 탐색기** 을 이전 하 고 확장 합니다 **테이블** 모든 테이블이 만들어졌는지 확인 하려면 노드. (아직 있는 경우 **서버 탐색기** 이전 시점에서 열기를 클릭 합니다 **새로 고침** 단추입니다.)

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image14.png)

에 대 한 모델 클래스를 만들지 않은 `CourseInstructor` 테이블입니다. 이 테이블은 조인 테이블 간의 다 대 다 관계에 대해 앞에서 설명한 대로 합니다 `Instructor` 및 `Course` 엔터티.

마우스 오른쪽 단추로 클릭 합니다 `CourseInstructor` 선택한 테이블 **테이블 데이터 표시** 의 결과로 데이터가 있는지 확인 하는 `Instructor` 에 추가 된 엔터티는 `Course.Instructors` 탐색 속성.

![Table_data_in_CourseInstructor_table](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image15.png)

## <a name="summary"></a>요약

이제 더 복잡한 데이터 모델 및 해당 데이터베이스가 만들어졌습니다. 다음 자습서를 관련된 데이터에 액세스 하는 다른 방법에 대해 자세히 알아봅니다.

다른 Entity Framework 리소스에 대 한 링크에서 찾을 수 있습니다 합니다 [ASP.NET 데이터 액세스 콘텐츠 맵](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.

> [!div class="step-by-step"]
> [이전](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [다음](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
