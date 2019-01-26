---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: '자습서: ASP.NET MVC 앱에서 EF 사용 하 여 관련된 데이터 읽기'
description: 이 자습서에서는 읽기 및 관련된 데이터 표시 됩니다-즉, Entity Framework는 탐색 속성으로 로드 하는 데이터입니다.
author: tdykstra
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: 18cdd896-8ed9-4547-b143-114711e3eafb
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: e4f23dbdb604dd513e42b7b8ff7b727245b9b637
ms.sourcegitcommit: d5223cf6a2cf80b4f5dc54169b0e376d493d2d3a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54889966"
---
# <a name="tutorial-read-related-data-with-ef-in-an-aspnet-mvc-app"></a>자습서: ASP.NET MVC 앱에서 EF 사용 하 여 관련된 데이터 읽기

이전 자습서에서 School 데이터 모델을 완료 했습니다. 이 자습서에서는 읽기 및 관련된 데이터 표시 됩니다-즉, Entity Framework는 탐색 속성으로 로드 하는 데이터입니다.

다음 그림에서는 사용할 페이지를 보여 줍니다.

![](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

이 자습서에서는 다음을 수행했습니다.

> [!div class="checklist"]
> * 관련된 데이터를 로드 하는 방법 알아보기
> * 강좌 페이지 만들기
> * 강사 페이지 만들기

## <a name="prerequisites"></a>전제 조건

* [더 복잡 한 데이터 모델 만들기](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)

## <a name="learn-how-to-load-related-data"></a>관련된 데이터를 로드 하는 방법 알아보기

Entity Framework 관련된 데이터를 엔터티의 탐색 속성으로 로드할 수는 여러 가지가 있습니다.

- *지연 로드*. 엔터티를 처음 읽을 때 관련된 데이터가 검색되지 않습니다. 그러나 탐색 속성에 처음으로 액세스하려고 할 때 해당 탐색 속성에 필요한 데이터가 자동으로 검색됩니다. 이 인해 여러 쿼리가 데이터베이스로 전송-엔터티 자체 및 각 시간 관련 엔터티에 대 한 데이터를 검색 해야 합니다. `DbContext` 클래스는 기본적으로 지연 로드를 사용 합니다.

    ![Lazy_loading_example](https://asp.net/media/2577850/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Lazy_loading_example_2c44eabb-5fd3-485a-837d-8e3d053f2c0c.png)
- *즉시 로드*. 엔터티를 읽을 때 관련된 데이터가 함께 검색됩니다. 이는 일반적으로 필요한 데이터를 모두 검색하는 단일 조인 쿼리를 발생시킵니다. 즉시 로드를 사용 하 여 지정 된 `Include` 메서드.

    ![Eager_loading_example](https://asp.net/media/2577856/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Eager_loading_example_33f907ff-f0b0-4057-8e75-05a8cacac807.png)
- *명시적 로드*. 이 지연 로드를 제외 하 코드에서 관련된 데이터를 명시적으로 검색 탐색 속성에 액세스할 때 자동으로 발생 하지 않습니다. 관련된 데이터를 수동으로 로드 하는 엔터티 및 호출에 대 한 개체 상태 관리자 항목을 가져와서 합니다 [Collection.Load](https://msdn.microsoft.com/library/gg696220(v=vs.103).aspx) 컬렉션에 대 한 메서드 또는 [Reference.Load](https://msdn.microsoft.com/library/gg679166(v=vs.103).aspx) 포함 하는 속성에 대 한 메서드는 단일 엔터티입니다. (다음 예제에서는 관리자 탐색 속성을 로드 하려는 경우 바꿔서 `Collection(x => x.Courses)` 사용 하 여 `Reference(x => x.Administrator)`.) 일반적으로 지연 오프 로드를 설정한 경우에 명시적 로드를 사용할 수 있습니다.

    ![Explicit_loading_example](https://asp.net/media/2577862/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Explicit_loading_example_79d8c368-6d82-426f-be9a-2b443644ab15.png)

속성 값을 즉시 검색 하지 않으므로 지연 로드 및 명시적 로딩은 둘 다 라고도 *지연 된 로드*합니다.

### <a name="performance-considerations"></a>성능 고려 사항

검색된 모든 엔터티에 대해 관련된 데이터가 필요한 경우 데이터베이스에 전송된 단일 쿼리는 검색된 각 엔터티에 대한 별도 쿼리보다 일반적으로 더 효율적이므로 즉시 로드는 종종 최상의 성능을 제공합니다. 예를 들어, 위의 예에서 각 부서에 10 개의 관련 된 강좌가 가정 합니다. 즉시 로드 예제는 데이터베이스에 왕복만 단일 (조인) 쿼리 및 단일으로 반환 됩니다. 지연 로드 하 고 명시적 로드 예제는 둘 다 11 개의 쿼리 및 11 개 왕복으로 인해 데이터베이스. 데이터베이스에 대한 추가 왕복은 대기 시간이 길 때 성능에 특히 악영향을 줍니다.

반면에 일부 시나리오에서는 지연 로딩을 더 효율적입니다. 즉시 로드는 SQL Server를 효율적으로 처리할 수 없습니다는 매우 복잡 한 조인이 생성 될 발생할 수 있습니다. 또는 처리 하는 엔터티 집합의 하위 집합에 대해서만 엔터티의 탐색 속성에 액세스 해야 할 경우, 지연 로드는 즉시 로드는 필요한 것 보다 더 많은 데이터를 검색 하므로 더 잘 수행할 수 있습니다. 성능이 중요한 경우 최상의 선택을 위해 두 가지 방식으로 성능을 테스트하는 것이 가장 좋습니다.

지연 로드 성능 문제를 일으키는 코드를 숨길 수 있습니다. 예를 들어, 즉시 또는 명시적 로드를 지정 하지 않으면 하지만 대량의 엔터티를 처리 하 고, 각 반복에서 여러 탐색 속성을 사용 하는 코드 않을 매우 효율적인 (때문에 데이터베이스에 여러 번 왕복). 온-프레미스 SQL server를 사용 하 여 개발에서 효율적으로 작동 하는 응용 프로그램 대기 시간이 증가 및 지연 로드로 인해 Azure SQL Database를 이동할 때 성능 문제가 있을 수 있습니다. 현실적인 테스트 부하를 사용 하 여 데이터베이스 쿼리를 프로 파일링 지연 로딩은 적절 한 경우를 결정 하는 데 도움이 됩니다. 자세한 내용은 참조 하세요. [Entity Framework 전략 익히기: 관련된 데이터 로드](https://msdn.microsoft.com/magazine/hh205756.aspx) 하 고 [SQL Azure 네트워크 대기 시간을 줄이기 위해 Entity Framework를 사용 하 여](https://msdn.microsoft.com/magazine/gg309181.aspx)입니다.

### <a name="disable-lazy-loading-before-serialization"></a>Serialization 전에 지연 로딩을 사용 하지 않도록 설정

지연 로드 사용 직렬화 하는 동안를 두면 의도 한 것 보다 훨씬 더 많은 데이터를 쿼리 될 수 있습니다. 직렬화 된 형식의 인스턴스에서 각 속성에 액세스 하 여 일반적으로 작동 합니다. 속성 액세스는 지연 로드를 트리거하고 지연 로드 된 엔터티 serialize 됩니다. Serialization 프로세스에는 다음 지연 로드 하는 엔터티를 잠재적으로 더 많은 지연 로드 및 serialization을 일으키는의 각 속성에 액세스 합니다. 런어웨이 연쇄 반응을이 방지 하려면 지연 엔터티를 serialize 하기 전에 오프 로드를 설정 합니다.

에 설명 된 대로 직렬화 Entity Framework를 사용 하는 프록시 클래스에 의해 복잡 수도 있습니다는 [고급 시나리오 자습서](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#proxies)합니다.

에 표시 된 대로 serialization 문제를 방지 하는 한 가지 방법은 데이터 전송 개체 (Dto) 대신 엔터티 개체를 serialize 하는 것은 [Entity Framework를 사용 하 여 웹 API를 사용 하 여](../../../../web-api/overview/data/using-web-api-with-entity-framework/part-5.md) 자습서입니다.

Dto를 사용 하지 않는 경우 지연 로드를 사용 하지 않도록 설정 하 여 프록시 문제를 방지 [프록시 생성을 사용 하지 않도록 설정](https://msdn.microsoft.com/data/jj592886.aspx)합니다.

다른 일부는 다음과 같습니다 [지연 로드를 사용 하지 않도록 설정 하는 방법을](https://msdn.microsoft.com/data/jj574232):

- 특정 탐색 속성에 대 한 생략 된 `virtual` 키워드는 속성을 선언 하는 경우.
- 모든 탐색 속성을 설정 `LazyLoadingEnabled` 를 `false`, 컨텍스트 클래스의 생성자에 다음 코드를 입력 합니다.

    [!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

## <a name="create-a-courses-page"></a>강좌 페이지 만들기

합니다 `Course` 엔터티를 포함 하는 탐색 속성을 포함 합니다 `Department` 강좌에 할당 된 부서 엔터티. 가져오기 과정의 목록에 할당 된 부서의 이름을 표시할 해야는 `Name` 속성을를 `Department` 에 있는 엔터티는 `Course.Department` 탐색 속성.

라는 컨트롤러를 만듭니다 `CourseController` (없습니다 CoursesController)에 대 한 합니다 `Course` 엔터티 형식에 대 한 동일한 옵션을 사용 하는 **Entity Framework를 사용 하 여 뷰를 사용 하 여 MVC 5 컨트롤러** 스 캐 폴더는 이전 합니다 `Student` 컨트롤러:

| 설정 | 값 |
| ------- | ----- |
| 모델 클래스 | 선택 **코스 (ContosoUniversity.Models)** 합니다. |
| 데이터 컨텍스트 클래스 | 선택 **SchoolContext (ContosoUniversity.DAL)** 합니다. |
| 컨트롤러 이름 | 입력 *CourseController*합니다. 마찬가지로 되지 *CoursesController* 사용 하 여는 *s*입니다. 선택 했 **코스 (ContosoUniversity.Models)** 의 **컨트롤러 이름** 값 자동으로 채워진 합니다. 값을 변경 해야 합니다. |

다른 기본값을 그대로 적용 하 고 컨트롤러를 추가 합니다.

오픈 *Controllers\CourseController.cs* 확인을 `Index` 메서드:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

자동 스캐폴딩은 `Include` 메서드를 사용하여 `Department` 탐색 속성에 대해 즉시 로드를 지정했습니다.

오픈 *Views\Course\Index.cshtml* 템플릿 코드를 다음 코드로 바꿉니다. 변경 내용은 강조 표시되어 있습니다.

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=4,7,14-16,23-25,31-33,40-42)]

스캐폴드 코드에 다음 변경 내용을 만들었습니다.

- 제목을 변경 **인덱스** 하 **과정**합니다.
- `CourseID` 속성 값을 보여 주는 **Number** 열을 추가했습니다. 기본적으로 기본 키 이므로 일반적으로 최종 사용자에 게 의미가 스 캐 폴드 되지 않습니다. 그러나 이 경우 기본 키는 의미가 있으며 표시하길 원합니다.
- 이동 합니다 **부서** 오른쪽에 열의 제목을 변경 합니다. 스 캐 폴더는 올바르게 표시 하도록 선택한를 `Name` 속성을 `Department` 엔터티에 하지만 열 머리글 해야 강좌 페이지에서 **부서** 대신 **이름**.

Department 열에 대 한 스 캐 폴드 된 코드를 표시 하는 `Name` 의 속성을 `Department` 로드 되는 엔터티는 `Department` 탐색 속성:

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml?highlight=2)]

페이지를 실행 합니다 (선택 된 **과정** Contoso University 홈페이지 탭) 부서 이름의 목록을 보려면.

## <a name="create-an-instructors-page"></a>강사 페이지 만들기

이 섹션의 컨트롤러를 만들고에 대 한 보기를 `Instructor` 강사 페이지를 표시 하기 위해 엔터티. 이 페이지는 다음과 같은 방법으로 관련된 데이터를 읽고 표시합니다.

- 강사 목록은의 관련된 데이터를 표시 합니다 `OfficeAssignment` 엔터티. `Instructor` 및 `OfficeAssignment` 엔터티는 일대영 또는 일 관계에 있습니다. 에 대 한 즉시 로드를 사용 하 여 `OfficeAssignment` 엔터티. 이전에 설명한 대로 기본 테이블의 검색된 모든 행에 관련된 데이터가 필요한 경우 즉시 로드는 일반적으로 더 효율적입니다. 이 경우 표시된 모든 강사에 대한 사무실 할당을 표시하길 원합니다.
- 사용자가 관련 강사를 선택 하는 경우 `Course` 엔터티가 표시 됩니다. `Instructor` 및 `Course` 엔터티는 다대다 관계에 있습니다. 에 대 한 즉시 로드를 사용 하 여 `Course` 엔터티 및 해당 관련 `Department` 엔터티. 이 경우 선택한 강사에 대해서만 강좌가 필요 하기 때문에 지연 로드 더 효율적일 수 있습니다. 그러나 이 예제에서는 탐색 속성에 있는 엔터티 내에서 탐색 속성에 대한 즉시 로드를 사용하는 방법을 보여 줍니다.
- 사용자가 강좌를 선택 하면 관련 된 데이터가 `Enrollments` 엔터티 집합에 표시 됩니다. `Course` 및 `Enrollment` 엔터티는 일대다 관계에 있습니다. 에 대 한 명시적 로드를 추가할 `Enrollment` 엔터티 및 해당 관련 `Student` 엔터티. (명시적 로드 필요는 없습니다 지연 로딩을 사용 하지만 명시적 로드를 수행 하는 방법을 보여 줍니다.)

### <a name="create-a-view-model-for-the-instructor-index-view"></a>강사 인덱스 뷰에 대 한 뷰 모델 만들기

강사 페이지는 서로 다른 세 테이블을 표시 합니다. 따라서 각각이 테이블 중 하나에 대한 데이터를 보유하는 세 가지 속성을 포함하는 보기 모델을 만듭니다.

에 *Viewmodel* 폴더를 만들기 *InstructorIndexData.cs* 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

### <a name="create-the-instructor-controller-and-views"></a>강사 컨트롤러 및 뷰 만들기

만들기는 `InstructorController` (없습니다 InstructorsController) EF 읽기/쓰기 작업을 사용 하 여 컨트롤러:

| 설정 | 값 |
| ------- | ----- |
| 모델 클래스 | 선택 **강사 (ContosoUniversity.Models)** 합니다. |
| 데이터 컨텍스트 클래스 | 선택 **SchoolContext (ContosoUniversity.DAL)** 합니다. |
| 컨트롤러 이름 | 입력 *InstructorController*합니다. 마찬가지로 되지 *InstructorsController* 사용 하 여는 *s*입니다. 선택 했 **코스 (ContosoUniversity.Models)** 의 **컨트롤러 이름** 값 자동으로 채워진 합니다. 값을 변경 해야 합니다. |

다른 기본값을 그대로 적용 하 고 컨트롤러를 추가 합니다.

오픈 *Controllers\InstructorController.cs* 추가한를 `using` 방침을 `ViewModels` 네임 스페이스:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

스 캐 폴드 된 코드를 `Index` 동안만 즉시 로드를 지정 하는 메서드는 `OfficeAssignment` 탐색 속성:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

대체는 `Index` 메서드를 다음 코드로 추가 로드 관련 데이터 및 보기 모델에 넣습니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

메서드에서 선택적 경로 데이터 (`id`) 및 쿼리 문자열 매개 변수 (`courseID`)는 선택한 강사 및 선택한 과정의 ID 값을 제공 하 고 뷰에 모든 필요한 데이터를 전달 합니다. 매개 변수는 페이지의 **선택** 하이퍼링크에서 제공됩니다.

코드는 보기 모델의 인스턴스를 만들고 강사 목록에 배치하여 시작합니다. 코드에 대 한 즉시 로드를 지정 합니다 `Instructor.OfficeAssignment` 하며 `Instructor.Courses` 탐색 속성입니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs?highlight=3-4)]

두 번째 `Include` 메서드는 교육 코스를 로드 및 로드 되는 각 과정에 적용 되는 즉시 로드는 `Course.Department` 탐색 속성입니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

이전에 설명한 대로 선행 로딩은 필요 하지 않지만 성능 향상을 위해 수행 됩니다. 뷰를 항상 필요 하므로 `OfficeAssignment` 효율적으로 동일한 쿼리에서 인출 하는 것이 엔터티를 합니다. `Course` 엔터티는 선행 로딩과 지연 로드 페이지가 없이 선택 된 강좌를 사용 하 여 더 자주 표시 되는 경우에 보다 이므로 웹 페이지에는 강사가 선택 된 경우에 필요 합니다.

강사의 ID를 선택한 경우 선택한 강사는 뷰 모델의 강사 목록에서 검색 됩니다. 보기 모델의 `Courses` 속성으로 로드 합니다 `Course` 해당 강사 엔터티 `Courses` 탐색 속성입니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

합니다 `Where` 메서드는 컬렉션을 반환 하지만 조건 하나만 발생 하는 메서드를 전달 하는 예제의 `Instructor` 반환 되는 엔터티. 합니다 `Single` 메서드는 단일 컬렉션 변환 `Instructor` 해당 엔터티에 액세스할 수 있는 엔터티 `Courses` 속성입니다.

사용 된 [단일](https://msdn.microsoft.com/library/system.linq.enumerable.single.aspx) 메서드 컬렉션을 아는 경우 컬렉션에서 항목을 하나만 갖습니다. `Single` 메서드에서 전달 된 컬렉션이 비어 있거나 둘 이상의 항목 경우 예외가 throw 됩니다. 대안은 [SingleOrDefault](https://msdn.microsoft.com/library/bb342451.aspx), 기본 값을 반환 하는 (`null` 여기서) 컬렉션이 비어 있는 경우. 그러나이 경우 여전히 결과적으로 예외 (찾으려는 시도에서 `Courses` 속성을 `null` 참조), 예외 메시지에서 문제의 원인을 덜 명확 하 게 477860 및 합니다. 호출 하는 경우는 `Single` 메서드를 전달할 수도 있습니다에 `Where` 호출 하는 대신 조건은 `Where` 메서드 개별적으로:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs)]

위 코드를 아래 코드 대신 사용합니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

다음으로 강좌를 선택한 경우 선택한 강좌가 보기 모델의 강좌 목록에서 검색됩니다. 보기 모델의 `Enrollments` 속성으로 로드 되는 `Enrollment` 해당 과정에서 엔터티 `Enrollments` 탐색 속성입니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

### <a name="modify-the-instructor-index-view"></a>강사 인덱스 뷰 수정

*Views\Instructor\Index.cshtml*, 템플릿 코드를 다음 코드로 바꿉니다. 변경 내용은 강조 표시되어 있습니다.

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1,4,14-18,21,23-28,38-43,45)]

기존 코드에 다음 변경 내용을 만들었습니다.

- 모델 클래스를 `InstructorIndexData`로 변경했습니다.
- 페이지 제목을 **인덱스**에서 **강사**로 변경했습니다.
- 추가 된 **Office** 표시 하는 열 `item.OfficeAssignment.Location` 경우에만 `item.OfficeAssignment` null이 아닙니다. (--0-또는-일대일 관계 이기 때문에 있을 수 없습니다 관련 `OfficeAssignment` 엔터티.)

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]
- 동적으로 추가 하는 추가 코드 `class="success"` 에 `tr` 선택한 강사의 요소입니다. 이 사용 하 여 선택한 행의 배경색을 설정 하는 [부트스트랩](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap) 클래스입니다.

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]
- 새로 추가 `ActionLink` 레이블이 지정 된 **선택** 보낼 선택한 강사의 ID에 이르게 각 행에 있는 다른 링크를 바로 앞의 `Index` 메서드.

응용 프로그램을 실행 하 고 선택 합니다 **강사** 탭 합니다. 페이지에 표시 됩니다는 `Location` 관련 된 속성 `OfficeAssignment` 엔터티와 빈 테이블 셀 있을 때 관련 없는 `OfficeAssignment` 엔터티.

에 *Views\Instructor\Index.cshtml* 파일을 닫은 후 `table` (끝에 있는 요소 파일의), 다음 코드를 추가 합니다. 이 코드는 강사가 선택된 경우 강사와 관련된 강좌의 목록을 표시합니다.

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml)]

이 코드는 보기 모델의 `Courses` 속성을 읽어 강좌의 목록을 표시합니다. 또한 제공을 `Select` 의 선택된 된 강좌의 ID를 전송 하는 하이퍼링크를 `Index` 작업 메서드.

페이지를 실행 하 고 강사를 선택 합니다. 이제 선택된 강사에 할당된 강좌를 표시하는 표가 표시되고 각 강좌에 대해 할당된 부서의 이름이 표시됩니다.

방금 추가한 코드 블록 뒤에 다음 코드를 추가합니다. 해당 강좌가 선택된 경우에 강좌에 등록된 학생의 목록을 표시합니다.

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]

이 코드를 읽기는 `Enrollments` 과정에 등록 된 학생의 목록을 표시 하기 위해 보기 모델의 속성입니다.

페이지를 실행 하 고 강사를 선택 합니다. 그런 다음, 강좌를 선택하여 등록된 학생 및 해당 등급의 목록을 봅니다.

### <a name="adding-explicit-loading"></a>명시적 로드를 추가합니다.

오픈 *InstructorController.cs* 하는 방법을 확인 `Index` 메서드는 선택한 과정에 대 한 등록의 목록을 가져옵니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs)]

에 대 한 즉시 로드를 지정 하는 강사 목록을 검색할 때 합니다 `Courses` 탐색 속성 및는 `Department` 각 코스의 속성입니다. 추가한 다음 합니다 `Courses` 컬렉션 뷰 모델에 액세스 하려면 이제는 `Enrollments` 해당 컬렉션에 하나의 엔터티에서 탐색 속성입니다. 에 대해 즉시 로드를 지정 하지 않으므로 `Course.Enrollments` 탐색 속성이 해당 속성의 데이터를 지연 로드의 결과로 페이지에 표시 되 합니다.

다른 방법으로 코드를 변경 하지 않고 지연 로드를 사용 하지 않도록 설정한 경우는 `Enrollments` 속성 개수 등록 과정 없었습니다에 관계 없이 null이 될 것입니다. 로드 하는 경우에는 `Enrollments` 즉시 로드 또는 명시적 로드를 지정 해야 속성입니다. 즉시 로드를 수행 하는 방법을 이미 살펴보았습니다. 명시적 로드의 예를 보려면 대체 합니다 `Index` 명시적으로 로드 되는 다음 코드를 사용 하 여 메서드를 `Enrollments` 속성입니다. 변경 된 코드를 강조 표시 됩니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs?highlight=20-31)]

선택한 후 `Course` 엔터티를 새 코드는 과정을 명시적으로 로드 `Enrollments` 탐색 속성:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

다음 사용자가 명시적으로 각 로드 하기 `Enrollment` 엔터티 관련 `Student` 엔터티:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cs)]

사용 하는 `Collection` 컬렉션 속성을 로드 하는 방법 엔터티 하나만 포함 하는 속성을 사용 하지만 `Reference` 메서드.

강사 인덱스 페이지를 이제 실행 하 고 데이터를 검색 하는 방법을 변경 했더라도 페이지에 표시 되는 항목의 차이가 표시 됩니다.

## <a name="get-the-code"></a>코드 가져오기

[완료 된 프로젝트 다운로드](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>추가 자료

다른 Entity Framework 리소스에 대 한 링크에서 찾을 수 있습니다 합니다 [ASP.NET 데이터 액세스-권장 리소스](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음을 수행했습니다.

> [!div class="checklist"]
> * 관련된 데이터를 로드 하는 방법
> * 강좌 페이지를 생성합니다.
> * 강사 페이지를 생성합니다.

관련된 데이터를 업데이트 하는 방법을 알아보려면 다음 문서로 계속 진행 하세요.

> [!div class="nextstepaction"]
> [관련 데이터 업데이트](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)