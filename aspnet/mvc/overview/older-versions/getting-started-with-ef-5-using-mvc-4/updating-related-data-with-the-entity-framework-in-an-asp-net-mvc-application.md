---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: (6 / 10) ASP.NET MVC 응용 프로그램에서 Entity Framework와 관련된 데이터를 업데이트 합니다. | Microsoft Docs
author: tdykstra
description: Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 5 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/30/2013
ms.topic: article
ms.assetid: 7871dc05-2750-470f-8b4c-3a52511949bc
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 227a7fed0ced884db591f0375454d6d0a62518f5
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="updating-related-data-with-the-entity-framework-in-an-aspnet-mvc-application-6-of-10"></a>(6 / 10) ASP.NET MVC 응용 프로그램에서 Entity Framework와 관련된 데이터를 업데이트합니다.
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

[완료 된 프로젝트를 다운로드 합니다.](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 5 Code First 및 Visual Studio 2012를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대한 정보는 [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조하세요. 시작 부분에서 자습서 시리즈를 시작할 수 있습니다 또는 [이 장의 대 한 시작 프로젝트 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 여기에서 시작 하 고 있습니다.
> 
> > [!NOTE] 
> > 
> > 해결할 수 없는 문제에 직면 하는 경우 [완료 장 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 문제를 재현 하려고 합니다. 일반적으로 코드 완성 된 코드를 비교 하 여 문제에 솔루션을 찾을 수 있습니다. 몇 가지 일반적인 오류 및 해결 하는 방법에 대 한 참조 [오류 및 해결 방법입니다.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)


관련된 데이터; 이전 자습서에서 표시 이 자습서에서는 관련된 데이터를 업데이트 합니다. 대부분의 관계에 대 한 적절 한 외래 키 필드를 업데이트 하 여 수행할 수 있습니다. 다 대 다 관계에 대 한 Entity Framework 노출 되는 것 조인 테이블을 직접 하므로 명시적으로 추가 하 고 엔터티 하 고 해당 탐색 속성에서 제거 해야 합니다.

다음 그림에서는 사용할 페이지를 보여 줍니다.

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="customize-the-create-and-edit-pages-for-courses"></a>강좌에 대한 만들기 및 편집 페이지 사용자 지정

새 강좌 엔터티가 만들어질 때 기존 부서에 대한 관계가 있어야 합니다. 이를 수행하기 위해 스캐폴드 코드는 컨트롤러 메서드 및 부서를 선택하기 위한 드롭다운 목록을 포함하는 만들기 및 편집 보기를 포함합니다. 드롭다운 목록에서 집합은 `Course.DepartmentID` 외래 키 속성 및 Entity Framework를 로드 하는 데 필요한 모든는 `Department` 는 적절 한 탐색 속성 `Department` 엔터티. 스캐폴드 코드를 사용하지만 오류 처리를 추가하고 드롭다운 목록을 정렬하도록 약간 변경합니다.

*CourseController.cs*, 4 개의 삭제 `Edit` 및 `Create` 메서드를 다음 코드로 바꿉니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,10,13-14,21-27,34,41,44-45,52-58,62-68)]

`PopulateDepartmentsDropDownList` 메서드 이름을 기준으로 정렬 하는 모든 부서의 목록을 가져옵니다, 만듭니다는 `SelectList` 드롭 다운 목록에 대 한 컬렉션 뷰 컬렉션을 전달 하 고는 `ViewBag` 속성입니다. 메서드는 호출 코드가 드롭다운 목록이 렌더링될 때 선택될 항목을 지정하도록 허용하는 선택적 `selectedDepartment` 매개 변수를 허용합니다. 뷰 이름을 전달 됩니다 `DepartmentID` 를 [는 `DropDownList` 도우미](../working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md), 도우미를 찾는 다음 알고는 `ViewBag` 개체에 대 한는 `SelectList` 라는 `DepartmentID`합니다.

`HttpGet` `Create` 메서드 호출의 `PopulateDepartmentsDropDownList` 새 과정에 대 한 부서 설정 되지 않으며 아직 때문에 선택한 항목을 설정 하지 않고 메서드:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

`HttpGet` `Edit` 메서드 편집 중인 과정에 이미 할당 되어 있는 분야의 ID에 따라 선택한 항목을 설정 합니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

`HttpPost` 메서드 모두에 대 한 `Create` 및 `Edit` 도 오류가 발생 한 후 페이지를 다시 표시 될 때 선택한 항목을 설정 하는 코드를 포함 합니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

이 코드는 오류 메시지를 표시 하기 페이지 다시 표시 됩니다 때 어떤 부서 선택한 선택 된 상태로 유지 되도록 합니다.

*Views\Course\Create.cshtml*, 강조 표시 된 코드를 추가 하기 전에 새 과정 숫자 필드를 만들어는 **제목** 필드입니다. 기본적으로 기본 키 필드가 아닌 스 캐 폴드 된 이전 자습서에서 설명 했 듯이 하지만이 기본 키 이므로 의미 있는 사용자 키 값을 입력할 수 있게 하려면 원하는 합니다.

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=17-23)]

*Views\Course\Edit.cshtml*, *Views\Course\Delete.cshtml*, 및 *Views\Course\Details.cshtml*를 추가 하기 전에 과정 숫자 필드는 **제목**  필드입니다. 기본 키 이기 때문에 표시 되지만 변경할 수 없습니다.

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml)]

실행의 **만들기** 페이지 (과정 인덱스 페이지를 표시 하 고 클릭 **새로 만들기**) 새 과정에 대 한 데이터를 입력 합니다.

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

**만들기**를 클릭합니다. 과정 인덱스 페이지가 목록에 추가 된 새 과정으로 표시 됩니다. 인덱스 페이지 목록의 부서 이름은 관계가 올바르게 설정되었음을 표시하는 탐색 속성에서 제공됩니다.

![Course_Index_page_showing_new_course](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

실행 된 **편집** 페이지 (과정 인덱스 페이지를 표시 하 고 클릭 **편집** 는 과정에).

![Course_edit_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

페이지에서 데이터를 변경하고 **저장**을 클릭합니다. 과정 인덱스 페이지가 업데이트 과정 데이터와 함께 표시 됩니다.

## <a name="adding-an-edit-page-for-instructors"></a>강사에 대 한 편집 페이지를 추가합니다.

강사 레코드를 편집할 때 강사의 사무실 할당을 업데이트할 수 있습니다. `Instructor` 엔터티 간의 관계가 0 또는 1을 하나는 `OfficeAssignment` 엔터티는 다음과 같은 경우를 처리 해야 합니다.

- 사용자 선택을 사무실 할당을 취소 하는 경우 원래 값을 제거 하 고 삭제 해야 합니다는 `OfficeAssignment` 엔터티.
- 사용자가 office 할당 값을 입력 하 고 원래 비어 있던 경우 새 만들어 해야 `OfficeAssignment` 엔터티.
- 기존 값을 변경 해야 사용자가 사무실 할당의 값을 변경 해도 경우 `OfficeAssignment` 엔터티.

열기 *InstructorController.cs* 살펴보세요는 `HttpGet` `Edit` 메서드:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

여기에 스 캐 폴드 코드 원하는 결과가 아닙니다. 데이터를 설정할 수 있지만 드롭 다운 목록에 대 한 텍스트 상자 방법이 필요 합니다. 이 메서드를 다음 코드로 바꿉니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

이 코드는 `ViewBag` 문을 즉시 로드 관련 된 추가 `OfficeAssignment` 엔터티. 즉시 로드를 수행할 수 없습니다는 `Find` 메서드를 하므로 `Where` 및 `Single` 메서드가 강의 선택 하려면 대신 사용 됩니다.

대체는 `HttpPost` `Edit` 메서드를 다음 코드로 합니다. office 할당 업데이트를 처리 합니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

코드는 다음을 수행합니다.

- `OfficeAssignment` 탐색 속성에 대한 즉시 로드를 사용하여 데이터베이스에서 현재 `Instructor` 엔터티를 가져옵니다. 이에서 수행한 것과 동일는 `HttpGet` `Edit` 메서드.
- 모델 바인더의 값으로 검색된 `Instructor` 엔터티를 업데이트합니다. [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx) 사용 된 오버 로드를 사용 하면 *화이트 리스트* 포함할 속성입니다. 이렇게 하면 과도 하 게 게시에 설명 된 대로 [두 번째 자습서](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)합니다.

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]
- 사무실 위치 비어 있으면 설정 하는 `Instructor.OfficeAssignment` 속성을 null로 되도록 관련된 행에는 `OfficeAssignment` 테이블은 삭제 됩니다.

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]
- 변경 내용을 데이터베이스에 저장합니다.

*Views\Instructor\Edit.cshtml*이후에 `div` 에 대 한 요소는 **Hire Date** 필드를 사무실 위치를 편집 하기 위해 새 필드 추가:

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml)]

페이지 실행 (선택 된 **강사** 탭을 클릭 한 다음 **편집** 강사에). **사무실 위치**를 변경하고 **저장**을 클릭합니다.

![Changing_the_office_location](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

## <a name="adding-course-assignments-to-the-instructor-edit-page"></a>강사에 대 한 추가 과정 할당 편집 페이지

강사는 강좌 수에 관계 없이 가르칠 수 있습니다. 이제 다음 스크린샷에 표시된 것처럼 확인란 그룹을 사용하여 강좌 할당을 변경하는 기능을 추가하여 강사 편집 페이지를 향상시킵니다.

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

간의 관계는 `Course` 및 `Instructor` 은 다 대 다 조인 테이블에 직접 액세스할 수 없는 의미 합니다. 대신 추가 하 고에서 엔터티를 제거는 `Instructor.Courses` 탐색 속성입니다.

강사에게 할당된 강좌를 변경할 수 있도록 하는 UI는 확인란의 그룹입니다. 데이터베이스의 모든 강좌에 대한 확인란이 표시되고 강사에게 현재 할당되어 있는 것이 선택됩니다. 사용자는 확인란을 선택하거나 선택 취소하여 강좌 할당을 변경할 수 있습니다. Courses 수가 된 훨씬 큰을 뷰에서 데이터를 제공 합니다. 다른 방법을 사용 하 고 싶을 것 하지만 관계 만들기 또는 삭제 하려면 탐색 속성을 조작 하는 동일한 방법을 사용 합니다.

확인란의 목록에 대한 보기에 데이터를 제공하려면 보기 모델 클래스를 사용합니다. 만들 *AssignedCourseData.cs* 에 *Viewmodel* 폴더와 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

*InstructorController.cs*, 대체 된 `HttpGet` `Edit` 메서드를 다음 코드로 합니다. 변경 내용은 강조 표시되어 있습니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs?highlight=5,8,12-27)]

코드는 `Courses` 탐색 속성에 대해 즉시 로드를 추가하고 새 `PopulateAssignedCourseData` 메서드를 호출하여 `AssignedCourseData` 보기 모델 클래스를 사용하여 확인란 배열에 대한 정보를 제공합니다.

코드는 `PopulateAssignedCourseData` 메서드를 모두 읽습니다 `Course` 보기를 사용 하는 과정의 목록을 로드 하기 위해 엔터티 모델 클래스입니다. 각 강좌의 경우 코드는 강좌가 강사의 `Courses` 탐색 속성에 있는지 여부를 확인합니다. 효율적인 조회를 만들려면 과정에서 강사에 할당 되었는지 여부를 확인할 때 강사에 할당 하는 과정에 저장 됩니다는 [HashSet](https://msdn.microsoft.com/library/bb359438.aspx) 컬렉션입니다. `Assigned` 속성이 `true` courses 강사 할당 됩니다. 보기는 이 속성을 사용하여 선택된 것으로 표시되어야 하는 확인란을 결정합니다. 목록 보기에 전달 되는 마지막으로, 한 `ViewBag` 속성입니다.

다음으로 사용자가 **저장**을 클릭할 때 실행되는 코드를 추가합니다. 대체는 `HttpPost` `Edit` 메서드를 업데이트 하는 새 메서드를 호출 하는 다음 코드로 `Courses` 의 탐색 속성은 `Instructor` 엔터티. 변경 내용은 강조 표시되어 있습니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs?highlight=3,7,20,33,37-65)]

보기의 컬렉션인 없으므로 `Course` 엔터티, 모델 바인더 자동으로 업데이트할 수는 `Courses` 탐색 속성입니다. Courses 탐색 속성을 업데이트 하려면 모델 바인더를 사용 하는 대신 작업입니다 새 `UpdateInstructorCourses` 메서드. 따라서 모델 바인딩에서 `Courses` 속성을 제외해야 합니다. 호출 하는 코드를 변경 하지 않아도이 [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx) 사용 중 이므로 *허용 목록이* 오버 로드 및 `Courses` include 목록에 있지 않습니다.

경우 없는 확인란이 선택 된을의 코드 `UpdateInstructorCourses` 초기화는 `Courses` 는 빈 컬렉션 탐색 속성:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs)]

그런 다음, 코드는 데이터베이스의 모든 강좌를 반복하고 현재 강사에게 할당된 것과 보기에서 선택되었던 것에 대해 각 강좌를 확인합니다. 효율적인 조회를 수행하기 위해 후자의 두 컬렉션은 `HashSet` 개체에 저장됩니다.

강좌에 대한 확인란이 선택됐지만 강좌가 `Instructor.Courses` 탐색 속성에 없는 경우 강좌는 탐색 속성의 컬렉션에 추가됩니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs)]

강좌에 대한 확인란이 선택되지 않았지만 강좌가 `Instructor.Courses` 탐색 속성에 있는 경우 강좌는 탐색 속성에서 제거됩니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

*Views\Instructor\Edit.cshtml*, 추가 **Courses** 강조 표시 하는 다음을 추가 하 여 확인란의 배열을 사용 하 여 필드 바로 다음 코드는 `div` 에 대 한 요소는 `OfficeAssignment` 필드:

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml?highlight=51-73)]

이 코드는 세 개의 열이 있는 HTML 테이블을 만듭니다. 각 열은 강좌 번호 및 제목으로 구성된 캡션이 뒤에 오는 확인란입니다. 모든 확인란 있어야 그룹으로 처리 해야 하는 모델 바인더에 게 동일한 이름 ("selectedCourses"). `value` 각 확인란의 특성의 값으로 설정 되어 `CourseID.` 모델 바인더 구성 된 컨트롤러에 배열을 전달 페이지가 게시 될 때는 `CourseID` 확인란만 선택 되에 대 한 값입니다.

강사에 할당 하는 과정에 사용 되는 것이 확인란은 처음 렌더링 됩니다 때 사용할 `checked` 특성 (에 확인 표시)을 선택 합니다.

사이트에 반환 될 때 변경 내용을 확인할 수 싶어하는 과정 할당을 변경한 후는 `Index` 페이지. 따라서 해당 페이지에 있는 테이블에 열을 추가 해야 합니다. 이 경우 있습니다 사용할 필요가 없습니다는 `ViewBag` 개체를 표시 하려는 정보를 이미 있으므로 `Courses` 의 탐색 속성은 `Instructor` 엔터티 모델로 페이지에 전달 하는 합니다.

*Views\Instructor\Index.cshtml*, 추가 **Courses** 제목 바로 다음에 **Office** 다음 예제와 같이 제목:

[!code-html[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.html?highlight=7)]

사무실 위치 정보 셀 바로 뒤에 새 세부 셀에 추가 합니다.

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml?highlight=19,50-57)]

실행 된 **강사 인덱스** 각 강사에 할당 된 과정을 보려면 페이지를:

![Instructor_index_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

클릭 **편집** 에서 강사 편집 페이지를 볼 수 있습니다.

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

일부 과정 할당을 변경 하 고 클릭 **저장**합니다. 변경 내용은 인덱스 페이지에 반영됩니다.

 참고: 강사 과정 데이터를 편집 하려면 적용 되는 방법을 제한 된 수의 과목 필요한 경우에 작동 합니다. 훨씬 큰 컬렉션의 경우 다른 UI 및 다른 업데이트 메서드가 필요합니다.  
 

## <a name="update-the-delete-method"></a>Delete 메서드를 업데이트 합니다.

강사 삭제 될 때 (있는 경우)에 해당 office 할당 레코드는 삭제 하므로 HttpPost Delete 메서드의 코드를 변경 합니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs?highlight=6,10)]


관리자 권한으로 부서에 배정 된 강사를 삭제 하려고 하면 참조 무결성 오류를 얻게 됩니다. 참조 [이 자습서의 현재 버전](../../getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) 추가 코드 강사 모든 부서 강사 관리자로 할당 된 위치에서 자동으로 제거 됩니다.

## <a name="summary"></a>요약

이제이 소개 관련 데이터로 작업을 완료 했습니다. 지금까지 전체 CRUD 작업을 완료 했으면이 자습서에 있지만 동시성 문제를 처리 하지 않았습니다. 다음 자습서 동시성의 주제를 소개 하 고, 처리 옵션을 설명 하 고 동시성 처리 이미 작성 한 엔터티 형식에 대 한 CRUD 코드를 추가 합니다.

다른 Entity Framework 리소스에 대 한 링크의 끝에서 찾을 수 있습니다 [이 시리즈의 마지막 자습서](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)합니다.

> [!div class="step-by-step"]
> [이전](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [다음](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
