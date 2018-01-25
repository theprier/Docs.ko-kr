---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: "ASP.NET MVC 응용 프로그램에서 Entity Framework와 관련 된 데이터 읽기 | Microsoft Docs"
author: tdykstra
description: /ajax/tutorials/using-ajax-control-toolkit-controls-and-control-extenders-vb
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/07/2014
ms.topic: article
ms.assetid: 18cdd896-8ed9-4547-b143-114711e3eafb
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 7a74d01f306abeeac5ac28c942f03001e0fe00f8
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="reading-related-data-with-the-entity-framework-in-an-aspnet-mvc-application"></a>ASP.NET MVC 응용 프로그램에서 Entity Framework 사용 하 여 데이터를 관련 읽기
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

[완료 된 프로젝트를 다운로드](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8) 또는 [PDF 다운로드](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20Entity%20Framework%206%20Code%20First%20using%20MVC%205.pdf)

> Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 6 Code First 및 Visual Studio 2013을 사용 하 여 ASP.NET MVC 5 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대 한 정보를 참조 하십시오. [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다.


이전 자습서에서 School 데이터 모델을 완료 합니다. 이 자습서에서는 읽기 및 관련된 데이터를 표시 합니다-즉, 데이터 탐색 속성에는 Entity Framework를 로드 합니다.

다음 그림에서는 보여 페이지와 협력 합니다.

![](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="lazy-eager-and-explicit-loading-of-related-data"></a>지연, 신속 하 게, 및 명시적 관련된 데이터 로드

여러 가지 방법으로 Entity Framework가 엔터티의 탐색 속성에 관련된 데이터를 로드할 수 있습니다.

- *지연 로드*합니다. 먼저 엔터티를 읽으면 관련된 데이터가 검색 되지 않습니다. 그러나는 탐색 속성에 액세스 하려고 처음으로 해당 탐색 속성에 필요한 데이터가 자동으로 검색 됩니다. 이 인해 데이터베이스에 전송 하는 여러 개의 쿼리-엔터티 자체에 대 한 개와 때마다 관련 엔터티에 대 한 데이터를 검색 해야 합니다. `DbContext` 클래스에서는 기본적으로 지연 로드 합니다. 

    ![Lazy_loading_example](https://asp.net/media/2577850/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Lazy_loading_example_2c44eabb-5fd3-485a-837d-8e3d053f2c0c.png)
- *즉시 로드*합니다. 엔터티를 읽을 때 함께 관련된 데이터가 검색 됩니다. 일반적으로 필요한 데이터를 모두 검색 하는 단일 조인 쿼리에서 발생 합니다. 즉시 로드를 사용 하 여 지정 된 `Include` 메서드.

    ![Eager_loading_example](https://asp.net/media/2577856/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Eager_loading_example_33f907ff-f0b0-4057-8e75-05a8cacac807.png)
- *명시적 로드*합니다. 이 지연 로드를 제외 하 코드에서 관련된 데이터를 명시적으로 검색 탐색 속성에 액세스할 때 자동으로 발생 하지 않습니다. 엔터티 및 호출에 대 한 개체 상태 관리자 항목을 가져오는 하 여 수동으로 관련된 데이터를 로드 하면는 [Collection.Load](https://msdn.microsoft.com/library/gg696220(v=vs.103).aspx) 컬렉션에 대 한 메서드 또는 [Reference.Load](https://msdn.microsoft.com/library/gg679166(v=vs.103).aspx) 포함 하는 속성에 대 한 메서드는 단일 엔터티입니다. (다음 예제에서는 관리자 탐색 속성을 로드 하려는 경우 바꿨을 것 `Collection(x => x.Courses)` 와 `Reference(x => x.Administrator)`.) 일반적으로 지연 오프 로드 설정 하는 경우에 명시적으로 로드를 사용 합니다.

    ![Explicit_loading_example](https://asp.net/media/2577862/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Explicit_loading_example_79d8c368-6d82-426f-be9a-2b443644ab15.png)

속성 값을 즉시 검색 하지 않으므로 지연 로드 및 명시적 로딩 둘 다 라고도 *지연 된 로드*합니다.

### <a name="performance-considerations"></a>성능 고려 사항

검색 된 모든 엔터티 관련된 데이터가 필요할 경우, 데이터베이스에 전송 하는 단일 쿼리를 검색할 각 엔터티에 대 한 별개의 쿼리와 보다 일반적으로 더 효율적 이므로 최상의 성능을 제공 종종 즉시 로드 합니다. 예를 들어 위의 예제에서 각 부서에는 10 개의 관련된 과정을 가정 합니다. 즉시 로드 예는 데이터베이스에 왕복만 단일 (조인) 쿼리 및 단일으로 반환 됩니다. 지연 로드 하 고 명시적 로딩 예는 모두 유발 11 개의 쿼리 및 11 개의 왕복 데이터베이스에 합니다. 데이터베이스에 추가 왕복 성능이 저하 때는 대기 시간이 깁니다.

반면에 일부 시나리오에서는 한 지연 로딩이 더 효율적입니다. 즉시 로드에는 SQL Server 없습니다 효율적으로 처리 하는 생성 될 매우 복잡 한 조인이 될 수 있습니다. 또는 엔터티 집합의 하위 집합에 대 한 엔터티 탐색 속성에 액세스 해야 하는 경우 처리 하는, 즉시 로드 필요한 것 보다 더 많은 데이터를 검색 하기 때문에 한 지연 로딩이 향상 될 수도 있습니다. 성능이 중요 한 경우에 최상의 선택을 하기 위해 두 가지 방식으로 성능을 테스트 하는 가장 좋습니다.

지연 로드로 인해 성능 문제가 발생 하는 코드를 마스킹할 수 있습니다. 예를 들어 eager 또는 명시적 로드를 지정 하지 않으면 하지만 많은 양의 엔터티를 처리 하 고 각 반복에서 몇 가지 탐색 속성을 사용 하 여 코드를 수 없습니다 효율적이 지 (때문에 데이터베이스에 여러 번 왕복). 온-프레미스 SQL server를 사용 하 여 개발을 수행 하는 응용 프로그램에는 대기 시간이 증가 및 지연 로드로 인해 Azure SQL 데이터베이스를 이동할 때 성능 문제가 있을 수 있습니다. 데이터베이스 쿼리는 실제 테스트 한 부하를 프로 파일링 한 지연 로딩이 적합 한지 결정 하는 데 도움이 됩니다. 자세한 내용은 참조 [Entity Framework 전략 제공: 관련 데이터를 로드](https://msdn.microsoft.com/magazine/hh205756.aspx) 및 [SQL Azure로 네트워크 대기 시간 줄이기를 Entity Framework를 사용 하 여](https://msdn.microsoft.com/magazine/gg309181.aspx)합니다.

### <a name="disable-lazy-loading-before-serialization"></a>Serialization 전에 지연 로드 사용 안 함

지연 로드 사용 직렬화 하는 동안를 두면 의도 한 것 보다 훨씬 더 많은 데이터를 쿼리 될 수 있습니다. 직렬화는 일반적으로 각 속성에는 형식의 인스턴스로 액세스 하 여 작동 합니다. 속성 액세스 지연 로드를 트리거하며 지연 로드 된 엔터티를 serialize 됩니다. Serialization 프로세스의 지연 로드 된 엔터티를 잠재적으로 더 많은 지연 로드 및 직렬화를 일으키는 각 속성을 액세스 합니다. 런어웨이 연쇄 반응을이 방지 하려면 지연 엔터티를 serialize 하기 전에 오프 로딩을 설정 합니다.

에 설명 된 대로 직렬화 하는 프록시 클래스는 Entity Framework를 사용 하 여 복잡도 수는 [고급 시나리오 자습서](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#proxies)합니다.

에 표시 된 것 처럼 serialization 문제를 방지 하는 한 가지 방법은 데이터 전송 개체 (Dto) 대신 엔터티 개체를 serialize 하는 것은 [Entity Framework를 사용 하 여 웹 API를 사용 하 여](../../../../web-api/overview/data/using-web-api-with-entity-framework/part-5.md) 자습서입니다.

지연 로드를 사용 하지 않도록 설정 하 고 하 여 프록시 문제를 방지할 수 Dto를 사용 하지 않는 경우 [프록시 생성을 사용 하지 않도록 설정](https://msdn.microsoft.com/data/jj592886.aspx)합니다.

다음은 몇 가지 다른 [지연 로드를 사용 하지 않도록 설정 하는 방법을](https://msdn.microsoft.com/data/jj574232):

- 특정 탐색 속성에 대 한 생략 된 `virtual` 키워드는 속성을 선언 하는 경우.
- 모든 탐색 속성에 대 한 설정 `LazyLoadingEnabled` 를 `false`, 컨텍스트 클래스의 생성자에 다음 코드를 입력 합니다. 

    [!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

## <a name="create-a-courses-page-that-displays-department-name"></a>해당 표시 부서 이름 과정 페이지 만들기

`Course` 엔터티를 포함 하는 탐색 속성에 포함 되어는 `Department` 엔터티 과정에 할당 된 부서입니다. 가져오기 과정의 목록에 할당 된 부서 이름을 표시 하려면 해야는 `Name` 속성에서는 `Department` 에 있는 엔터티의 `Course.Department` 탐색 속성입니다.

라는 컨트롤러를 만들고 `CourseController` (하지 CoursesController)에 대 한는 `Course` 엔터티 형식에 대 한 동일한 옵션을 사용 하는 **Entity Framework를 사용 하 여 뷰를 포함 된 MVC 5 컨트롤러** 는 에대한예전scaffolder`Student` 다음 그림에 나와 있는 것 처럼 컨트롤러:

![Add_Controller_dialog_box_for_Course_controller](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

열기 *Controllers\CourseController.cs* 살펴보세요는 `Index` 메서드:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

자동 스 캐 폴딩이에 대 한 즉시 로드 지정는 `Department` 를 사용 하 여 탐색 속성에서 `Include` 메서드.

열기 *Views\Course\Index.cshtml* 템플릿 코드를 다음 코드로 바꿉니다. 변경 내용은 강조 표시 됩니다.

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=4,7,14-16,23-25,31-33,40-42)]

스 캐 폴드 코드를 다음과 같이 변경을 했습니다.

- 제목을 변경 **인덱스** 를 **Courses**합니다.
- 추가 **번호** 보여 주는 열은 `CourseID` 속성 값입니다. 기본적으로 기본 키 이므로 일반적으로 최종 사용자에 게 의미가 스 캐 폴드 되지 않습니다. 그러나이 경우 기본 키 의미 이며 하려는 표시할지를 기준으로 합니다.
- 이동의 **부서** 오른쪽에 열 머리글을 변경 합니다. scaffolder 올바르게 표시 하도록 선택한는 `Name` 속성에서는 `Department` 엔터티, 하지만 여기서 과정 페이지 열 제목 있어야에 **부서** 대신 **이름**합니다.

Department 열에 대 한 스 캐 폴드 코드 표시 됩니다는 `Name` 의 속성은 `Department` 에 로드 된 엔터티는 `Department` 탐색 속성:

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml?highlight=2)]

페이지를 실행 (선택 된 **Courses** Contoso 대학 홈 페이지 탭) 부서 이름의 목록을 보려면 합니다.

![Courses_index_page_with_department_names](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

## <a name="create-an-instructors-page-that-shows-courses-and-enrollments"></a>만들기 과정 및 등록을 보여 주는 강사 페이지

이 섹션에서는 가상 랩에서 컨트롤러를 만들고에 대 한 보기 된 `Instructor` 엔터티 강사 페이지를 표시 하려면:

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

이 페이지를 읽고 다음과 같이 관련된 데이터를 표시 합니다.

- 강사 목록은의 관련된 데이터 표시는 `OfficeAssignment` 엔터티. `Instructor` 및 `OfficeAssignment` 엔터티는 0 또는 1을 한 관계에 있습니다. 에 대 한 즉시 로드를 사용 하 여는 `OfficeAssignment` 엔터티. 이전에 설명한 대로 기본 테이블의 모든 검색 된 행에 관련된 데이터를 필요로 하는 경우 즉시 로드 일반적으로 더 효율적입니다. 이 경우에 표시 된 모든 강사에 게 사무실 할당을 표시 하려면.
- 사용자가 관련 강사를 선택할 때 `Course` 엔터티 표시 됩니다. `Instructor` 및 `Course` 엔터티가 서로 다 대 다 관계에 있습니다. 에 대 한 즉시 로드를 사용 하 여는 `Course` 엔터티 및 관련 `Department` 엔터티. 이 경우 선택한 강사에 대해서만 courses 필요 하기 때문에 한 지연 로딩이 더 효율적일 수 있습니다. 그러나이 예제에는 자체 탐색 속성에 있는 엔터티 내에서 탐색 속성에 대 한 즉시 로드를 사용 하는 방법을 보여 줍니다.
- 관련 된 데이터를 사용자가 과정을 선택 하는 경우는 `Enrollments` 엔터티 집합이 표시 됩니다. `Course` 및 `Enrollment` 엔터티가 서로 일 대 다 관계에 있습니다. 명시적 로드에 대 한 추가 `Enrollment` 엔터티 및 관련 `Student` 엔터티. (명시적 로딩 필요 하지 않습니다 지연 로드를 사용 하도록 설정 되었지만 명시적 로딩 작업을 수행 하는 방법을 보여 줍니다.)

### <a name="create-a-view-model-for-the-instructor-index-view"></a>강사 인덱스 보기에 대 한 뷰 모델 만들기

강사 페이지에는 서로 다른 세 테이블 표시 됩니다. 따라서 각 테이블 중 하나에 대 한 데이터를 보유으로 세 가지 속성을 포함 하는 보기 모델을 만들어야 합니다.

에 *Viewmodel* 폴더를 만들 *InstructorIndexData.cs* 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

### <a name="create-the-instructor-controller-and-views"></a>강사 컨트롤러 및 뷰 만들기

만들기는 `InstructorController` (하지 InstructorsController) 다음 그림에 나와 있는 것 처럼 EF 읽기/쓰기 동작이 포함 된 컨트롤러:

![Add_Controller_dialog_box_for_Instructor_controller](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

열기 *Controllers\InstructorController.cs* 추가 `using` 문에 `ViewModels` 네임 스페이스:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

스 캐 폴드 코드에는 `Index` 메서드 지정에 대해서만 즉시 로드는 `OfficeAssignment` 탐색 속성:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

대체는 `Index` 메서드 추가 로드를 다음 코드로 관련 데이터의 보기 모델에 저장 합니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

메서드에 선택적 경로 데이터 (`id`) 및 쿼리 문자열 매개 변수 (`courseID`) 선택한 강사 및 선택한 과정의 ID 값을 제공 하 고 필요한 데이터의 모든 보기를 전달 합니다. 매개 변수에서 제공 되는 **선택** 페이지의 하이퍼링크입니다.

코드의 보기 모델의 인스턴스를 만들고 강사 목록에 배치 하 여 시작 합니다. 에 대 한 즉시 로드를 지정 하는 코드는 `Instructor.OfficeAssignment` 및 `Instructor.Courses` 탐색 속성입니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs?highlight=3-4)]

두 번째 `Include` 메서드 과정을를 로드 하 고 로드 된 각 과정에 대 한에 적용 되는 즉시 로드는 `Course.Department` 탐색 속성입니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

앞에서 설명한 대로 즉시 로드는 필요 하지 않지만 성능을 향상 시키기 위해서입니다. 보기 항상 필요 하므로 `OfficeAssignment` 엔터티에 것이 더 효율적을 같은 쿼리에서 인출 합니다. `Course`엔터티는 즉시 로드 하지 않고 보다 선택 하는 과정에 페이지를 더 자주 표시할 경우에 지연 로드 보다 더 나은 이므로 웹 페이지에서 강사를 선택한 경우에 필요 합니다.

강사 ID를 선택한 경우 선택한 강사 강사 보기 모델에 있는 목록에서 검색 됩니다. 뷰 모델 `Courses` 속성으로 로드는 `Course` 해당 강사에서 엔터티에 `Courses` 탐색 속성입니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

`Where` 메서드 컬렉션을 반환 하지만 조건 하나만에서 해당 메서드 결과에 전달 되는 경우 `Instructor` 엔터티를 반환 합니다. `Single` 메서드 컬렉션을 단일 `Instructor` 해당 엔터티에 액세스할 수 있는 엔터티 `Courses` 속성입니다.

사용 된 [단일](https://msdn.microsoft.com/library/system.linq.enumerable.single.aspx) 메서드 컬렉션을 알고 있는 경우 컬렉션에 항목을 하나만 갖습니다. `Single` 메서드는 전달 된 컬렉션은 비어 있거나 둘 이상의 항목이 없는 경우 예외를 throw 합니다. 대신 [SingleOrDefault](https://msdn.microsoft.com/library/bb342451.aspx), 기본 값을 반환 하 (`null` 이 예제의) 컬렉션이 비어 있는 경우. 그러나이 경우에 여전히 초래 예외 (찾으려고 시도에서 `Courses` 속성에는 `null` 참조), 예외 메시지는 문제의 원인을 477860 덜 명확 하 게 하 고 있습니다. 호출 하는 경우는 `Single` 메서드를 전달할 수도 있습니다에 `Where` 조건을 호출 하는 대신는 `Where` 메서드 별도로:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs)]

위 코드를 아래 코드 대신 사용합니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

다음으로 과정을 선택한 경우 선택한 과정의 보기 모델에는 과정의 목록에서 검색 됩니다. 다음 뷰 모델의 `Enrollments` 속성으로 로드 되는 `Enrollment` 해당 과정에서 엔터티 `Enrollments` 탐색 속성입니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

### <a name="modify-the-instructor-index-view"></a>강사 인덱스 뷰를 수정 합니다.

*Views\Instructor\Index.cshtml*, 템플릿 코드를 다음 코드로 바꿉니다. 변경 내용은 강조 표시 됩니다.

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1,4,14-18,21,23-28,38-43,45)]

기존 코드를 다음과 같이 변경을 했습니다.

- 모델 클래스를 변경 `InstructorIndexData`합니다.
- 페이지 제목을 변경 **인덱스** 를 **강사**합니다.
- 추가 **Office** 표시 하는 열 `item.OfficeAssignment.Location` 경우에만 `item.OfficeAssignment` null입니다. (0 또는 1을 한 관계 이므로 수 없는 경우 관련 `OfficeAssignment` 엔터티.) 

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]
- 추가 된 코드를 동적으로 추가 됩니다 `class="success"` 에 `tr` 선택한 강사의 요소입니다. 이 사용 하 여 선택한 행에 대 한 배경색을 설정 하는 [부트스트랩](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap) 클래스입니다. 

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]
- 새 추가 `ActionLink` 레이블이 **선택** 를 보내도록 선택한 강사 ID 때문에 있는 다른 각 행에 링크 바로 앞의 `Index` 메서드.

응용 프로그램을 실행 하 고 선택 된 **강사** 탭 합니다. 페이지에 표시 됩니다는 `Location` 속성 관련된 `OfficeAssignment` 엔터티 및 빈 테이블 셀이 있으면 관련 no `OfficeAssignment` 엔터티.

![Instructors_index_page_with_nothing_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

에 *Views\Instructor\Index.cshtml* 파일을 닫은 후 `table` (끝에 요소 파일의), 다음 코드를 추가 합니다. 이 코드는 강사가 강사 선택 된 경우와 관련 된 과정의 목록이 표시 됩니다.

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml)]

이 코드를 읽고는 `Courses` 과정의 목록을 표시 하려면 보기 모델의 속성입니다. 또한 제공는 `Select` 하이퍼링크에 선택한 과정의 ID를 전송 하는 `Index` 동작 메서드.

페이지를 실행 하 고 강사를 선택 합니다. 이제 선택한 강사에 할당 하는 과정을 표시 하는 표를 표시 및 각 과정에 대 한 할당 된 부서 이름을 표시 합니다.

![Instructors_index_page_with_instructor_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

방금 추가한 코드 블록을 한 후 다음 코드를 추가 합니다. 해당 과정을 선택한 경우에 과정에서 등록 된 학생의 목록을 표시 합니다.

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]

이 코드를 읽고는 `Enrollments` 과정에 학생의 목록을 표시 하려면 보기 모델의 속성 등록 합니다.

페이지를 실행 하 고 강사를 선택 합니다. 그런 다음 등록 된 학생 자신의 등급의 목록을 보려면 과정을 선택 합니다.

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

### <a name="adding-explicit-loading"></a>명시적 로드를 추가합니다.

열기 *InstructorController.cs* 방법을 확인 하 고 `Index` 메서드 선택한 과정에 대 한 등록의 목록을 가져옵니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs)]

즉시 로드에 대 한 지정한 강사 목록을 검색 하는 경우는 `Courses` 탐색 속성 및에 대 한는 `Department` 각 과정의 속성입니다. 배치 하는 다음의 `Courses` 고 컬렉션의 보기 모델에 액세스 하는 이제는 `Enrollments` 해당 컬렉션의 엔터티 간에 탐색 속성입니다. 에 대 한 즉시 로드를 지정 하지 않은 때문에 `Course.Enrollments` 지연 로드의 결과로 페이지에서 해당 속성의 데이터가 나타나는지 탐색 속성입니다.

다른 방법으로 코드를 변경 하지 않고 지연 로드를 사용 하지 않도록 설정한 경우는 `Enrollments` 속성 개수 등록 과정 되었습니다에 관계 없이 null이 될 것입니다. 로드할 경우에서는 `Enrollments` 속성을 즉시 로드 또는 명시적 로드 중 하나를 지정 해야 할 것 있습니다. 즉시 로드를 수행 하는 방법을 이미 살펴보았습니다. 명시적 로드의 예를 보려면 대체는 `Index` 메서드를 명시적으로 로드 하는 다음 코드는 `Enrollments` 속성입니다. 변경 된 코드를 강조 표시 됩니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs?highlight=20-31)]

선택한 받은 후 `Course` 엔터티를 새 코드는 해당 과정을 명시적으로 로드 `Enrollments` 탐색 속성:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

명시적으로 각 로드 후 `Enrollment` 엔터티의 관련 `Student` 엔터티:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cs)]

공지를 사용 하는 `Collection` 개체 컬렉션 속성에 대 한 하나의 엔터티를 포함 하는 속성을 사용 하 여 있습니다 하지만 `Reference` 메서드.

강사 인덱스 페이지를 지금 실행를 한 데이터를 검색 하는 방법을 변경 하지만 페이지에 표시 되는 내용에 차이가 없어야을 나타납니다.

## <a name="summary"></a>요약

이제 모든 세 가지 방법으로 (지연, 신속 하 게, 및 명시적) 탐색 속성에 관련된 데이터를 로드를 사용 했습니다. 다음 자습서에서 관련된 데이터를 업데이트 하는 방법을 설명 합니다.

이 자습서를 연결 하는 방법 및 향상 될 수 있습니다에 의견을 남겨 주세요. 새 항목을 요청할 수도 있습니다 [Me 방법으로 코드 보기](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code)합니다.

다른 Entity Framework 리소스에 대 한 링크에서 확인할 수 있습니다는 [ASP.NET 데이터 액세스-권장 리소스](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.

>[!div class="step-by-step"]
[이전](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)
[다음](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
