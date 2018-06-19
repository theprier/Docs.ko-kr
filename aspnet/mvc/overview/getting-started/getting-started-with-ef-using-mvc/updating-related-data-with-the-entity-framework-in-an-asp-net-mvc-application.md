---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: ASP.NET MVC 응용 프로그램에서 Entity Framework와 관련된 데이터를 업데이트 합니다. | Microsoft Docs
author: tdykstra
description: Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 6 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 5 응용 프로그램을 만드는 방법을 보여 줍니다 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/01/2015
ms.topic: article
ms.assetid: 7ba88418-5d0a-437d-b6dc-7c3816d4ec07
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: cf4a6183e068e8668eb706d9a9e311616649e863
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30875619"
---
<a name="updating-related-data-with-the-entity-framework-in-an-aspnet-mvc-application"></a>ASP.NET MVC 응용 프로그램에서 Entity Framework와 관련된 데이터를 업데이트합니다.
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

[완료 된 프로젝트를 다운로드](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8) 또는 [PDF 다운로드](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20Entity%20Framework%206%20Code%20First%20using%20MVC%205.pdf)

> Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 6 Code First 및 Visual Studio 2013을 사용 하 여 ASP.NET MVC 5 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대한 정보는 [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조하세요.


관련된 데이터; 이전 자습서에서 표시 이 자습서에서는 관련된 데이터를 업데이트 합니다. 대부분의 관계에 대 한 외래 키 필드 또는 탐색 속성 중 하나를 업데이트 하 여 수행할 수 있습니다. 다 대 다 관계에 대 한 Entity Framework 노출 되는 것 조인 테이블에 직접 추가 하 고 해당 탐색 속성에서 엔터티를 제거 하도록 합니다.

다음 그림에서는 사용할 일부 페이지를 보여 줍니다.

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

![과정을 사용 하 여 강사 편집](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

## <a name="customize-the-create-and-edit-pages-for-courses"></a>강좌에 대한 만들기 및 편집 페이지 사용자 지정

새 강좌 엔터티가 만들어질 때 기존 부서에 대한 관계가 있어야 합니다. 이를 수행하기 위해 스캐폴드 코드는 컨트롤러 메서드 및 부서를 선택하기 위한 드롭다운 목록을 포함하는 만들기 및 편집 보기를 포함합니다. 드롭다운 목록에서 집합은 `Course.DepartmentID` 외래 키 속성 및 Entity Framework를 로드 하는 데 필요한 모든는 `Department` 는 적절 한 탐색 속성 `Department` 엔터티. 스캐폴드 코드를 사용하지만 오류 처리를 추가하고 드롭다운 목록을 정렬하도록 약간 변경합니다.

*CourseController.cs*, 4 개의 삭제 `Create` 및 `Edit` 메서드를 다음 코드로 바꿉니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,11-12,19-25,40,44,46,48-78)]

다음 추가 `using` 파일의 시작 부분에 문의:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

`PopulateDepartmentsDropDownList` 메서드 이름을 기준으로 정렬 하는 모든 부서의 목록을 가져옵니다, 만듭니다는 `SelectList` 드롭 다운 목록에 대 한 컬렉션 뷰 컬렉션을 전달 하 고는 `ViewBag` 속성입니다. 메서드는 호출 코드가 드롭다운 목록이 렌더링될 때 선택될 항목을 지정하도록 허용하는 선택적 `selectedDepartment` 매개 변수를 허용합니다. 뷰 이름을 전달 됩니다 `DepartmentID` 에 [DropDownList](../../older-versions/working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md) 도우미 및 도우미를 찾는 다음 알고는 `ViewBag` 개체에 대 한는 `SelectList` 라는 `DepartmentID`합니다.

`HttpGet` `Create` 메서드 호출의 `PopulateDepartmentsDropDownList` 새 과정에 대 한 부서 설정 되지 않으며 아직 때문에 선택한 항목을 설정 하지 않고 메서드:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

`HttpGet` `Edit` 메서드 편집 중인 과정에 이미 할당 되어 있는 분야의 ID에 따라 선택한 항목을 설정 합니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=12)]

`HttpPost` 메서드 모두에 대 한 `Create` 및 `Edit` 도 오류가 발생 한 후 페이지를 다시 표시 될 때 선택한 항목을 설정 하는 코드를 포함 합니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=6)]

이 코드는 오류 메시지를 표시 하기 페이지 다시 표시 됩니다 때 어떤 부서 선택한 선택 된 상태로 유지 되도록 합니다.

과정 뷰는 이미 스 캐 폴드 된 부서 필드에 대 한 드롭다운 목록을 사용 하 여 않으려는 DepartmentID 캡션이이 필드에 대 한 강조 표시 된 다음 확인을 변경 하므로 *Views\Course\Create.cshtml* 파일을 캡션을 변경 합니다.

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml?highlight=43)]

에 동일한 변경 내용을 *Views\Course\Edit.cshtml*합니다.

일반적으로 scaffolder 키 값을 변경할 수 없습니다 및 사용자에 게 표시 하는 의미 있는 값이 아닌 데이터베이스에서 생성 하기 때문에 기본 키 스 캐 폴딩 하지 않습니다. scaffolder는에 있는 입력란을 포함 하는 데 과정 엔터티에 대 한는 `CourseID` 파악 하는 필드는 `DatabaseGeneratedOption.None` 특성 의미 사용자 수 있어야 합니다. 기본 키 값을 입력 합니다. 그러나 수는 의미가 있으므로 되도록를 수동으로 추가 해야 하므로 다른 보기의 참조 이해 하지 않습니다.

*Views\Course\Edit.cshtml*, 추가 하기 전에 과정 숫자 필드는 **제목** 필드입니다. 기본 키 이기 때문에 표시 되지만 변경할 수 없습니다.

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cshtml)]

이미 숨겨진된 필드 (`Html.HiddenFor` 도우미) 편집 보기에서 과정 번호에 대 한 합니다. 추가 *Html.LabelFor* 도우미를 클릭할 때 게시 된 데이터에 포함 되도록 과정 번호를 발생 하지 않는 되었기 때문에 숨겨진된 필드에 대 한 필요성을 제거 하지 않습니다 **저장** 편집 페이지에서.

*Views\Course\Delete.cshtml* 및 *Views\Course\Details.cshtml*부서 이름 캡션을 "이름"에서 "부서"를 변경 하 고 추가 하기 전에 과정 숫자 필드는 **제목**  필드입니다.

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cshtml?highlight=2,9-15)]

실행의 **만들기** 페이지 (과정 인덱스 페이지를 표시 하 고 클릭 **새로 만들기**) 새 과정에 대 한 데이터를 입력 합니다.

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

**만들기**를 클릭합니다. 과정 인덱스 페이지가 목록에 추가 된 새 과정으로 표시 됩니다. 인덱스 페이지 목록의 부서 이름은 관계가 올바르게 설정되었음을 표시하는 탐색 속성에서 제공됩니다.

![Course_Index_page_showing_new_course](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

실행 된 **편집** 페이지 (과정 인덱스 페이지를 표시 하 고 클릭 **편집** 는 과정에).

![Course_edit_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

페이지에서 데이터를 변경하고 **저장**을 클릭합니다. 과정 인덱스 페이지가 업데이트 과정 데이터와 함께 표시 됩니다.

## <a name="adding-an-edit-page-for-instructors"></a>강사에 대 한 편집 페이지를 추가합니다.

강사 레코드를 편집할 때 강사의 사무실 할당을 업데이트할 수 있습니다. `Instructor` 엔터티 간의 관계가 0 또는 1을 하나는 `OfficeAssignment` 엔터티는 다음과 같은 경우를 처리 해야 합니다.

- 사용자 선택을 사무실 할당을 취소 하는 경우 원래 값을 제거 하 고 삭제 해야 합니다는 `OfficeAssignment` 엔터티.
- 사용자가 office 할당 값을 입력 하 고 원래 비어 있던 경우 새 만들어 해야 `OfficeAssignment` 엔터티.
- 기존 값을 변경 해야 사용자가 사무실 할당의 값을 변경 해도 경우 `OfficeAssignment` 엔터티.

열기 *InstructorController.cs* 살펴보세요는 `HttpGet` `Edit` 메서드:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

여기에 스 캐 폴드 코드 원하는 결과가 아닙니다. 데이터를 설정할 수 있지만 드롭 다운 목록에 대 한 텍스트 상자 방법이 필요 합니다. 이 메서드를 다음 코드로 바꿉니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs?highlight=7-10)]

이 코드는 `ViewBag` 문을 즉시 로드 관련 된 추가 `OfficeAssignment` 엔터티. 즉시 로드를 수행할 수 없습니다는 `Find` 메서드를 하므로 `Where` 및 `Single` 메서드가 강의 선택 하려면 대신 사용 됩니다.

대체는 `HttpPost` `Edit` 메서드를 다음 코드로 합니다. office 할당 업데이트를 처리 합니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

에 대 한 참조 `RetryLimitExceededException` 필요는 `using` 추가 마우스 오른쪽 단추로 클릭 문과 `RetryLimitExceededException`, 클릭 하 고 **해결** - **System.Data.Entity.Infrastructure를사용하여**.

![다시 시도 예외를 해결 합니다.](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

코드는 다음을 수행합니다.

- 에 메서드 이름을 변경 하는 `EditPost` 서명이 이제와 동일 하기 때문에 `HttpGet` 메서드 (에서 `ActionName` 특성 지정 /Edit/ URL은 여전히 사용).
- `OfficeAssignment` 탐색 속성에 대한 즉시 로드를 사용하여 데이터베이스에서 현재 `Instructor` 엔터티를 가져옵니다. 이에서 수행한 것과 동일는 `HttpGet` `Edit` 메서드.
- 모델 바인더의 값으로 검색된 `Instructor` 엔터티를 업데이트합니다. [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx) 사용 된 오버 로드를 사용 하면 *화이트 리스트* 포함할 속성입니다. 이렇게 하면 과도 하 게 게시에 설명 된 대로 [두 번째 자습서](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)합니다.

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs)]
- 사무실 위치 비어 있으면 설정 하는 `Instructor.OfficeAssignment` 속성을 null로 되도록 관련된 행에는 `OfficeAssignment` 테이블은 삭제 됩니다.

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]
- 변경 내용을 데이터베이스에 저장합니다.

*Views\Instructor\Edit.cshtml*이후에 `div` 에 대 한 요소는 **Hire Date** 필드를 사무실 위치를 편집 하기 위해 새 필드 추가:

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml)]

페이지 실행 (선택 된 **강사** 탭을 클릭 한 다음 **편집** 강사에). **사무실 위치**를 변경하고 **저장**을 클릭합니다.

![Changing_the_office_location](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

## <a name="adding-course-assignments-to-the-instructor-edit-page"></a>강사에 대 한 추가 과정 할당 편집 페이지

강사는 강좌 수에 관계 없이 가르칠 수 있습니다. 이제 다음 스크린샷에 표시된 것처럼 확인란 그룹을 사용하여 강좌 할당을 변경하는 기능을 추가하여 강사 편집 페이지를 향상시킵니다.

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

간의 관계는 `Course` 및 `Instructor` 은 다 대 다 조인 테이블에 있는 외래 키 속성에 직접 액세스할 수 없는 의미 합니다. 추가 하 고에서 엔터티를 제거 하는 대신,는 `Instructor.Courses` 탐색 속성입니다.

강사에게 할당된 강좌를 변경할 수 있도록 하는 UI는 확인란의 그룹입니다. 데이터베이스의 모든 강좌에 대한 확인란이 표시되고 강사에게 현재 할당되어 있는 것이 선택됩니다. 사용자는 확인란을 선택하거나 선택 취소하여 강좌 할당을 변경할 수 있습니다. Courses 수가 된 훨씬 큰을 뷰에서 데이터를 제공 합니다. 다른 방법을 사용 하 고 싶을 것 하지만 관계 만들기 또는 삭제 하려면 탐색 속성을 조작 하는 동일한 방법을 사용 합니다.

확인란의 목록에 대한 보기에 데이터를 제공하려면 보기 모델 클래스를 사용합니다. 만들 *AssignedCourseData.cs* 에 *Viewmodel* 폴더와 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

*InstructorController.cs*, 대체 된 `HttpGet` `Edit` 메서드를 다음 코드로 합니다. 변경 내용은 강조 표시되어 있습니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs?highlight=9,12,20-35)]

코드는 `Courses` 탐색 속성에 대해 즉시 로드를 추가하고 새 `PopulateAssignedCourseData` 메서드를 호출하여 `AssignedCourseData` 보기 모델 클래스를 사용하여 확인란 배열에 대한 정보를 제공합니다.

코드는 `PopulateAssignedCourseData` 메서드를 모두 읽습니다 `Course` 보기를 사용 하는 과정의 목록을 로드 하기 위해 엔터티 모델 클래스입니다. 각 강좌의 경우 코드는 강좌가 강사의 `Courses` 탐색 속성에 있는지 여부를 확인합니다. 효율적인 조회를 만들려면 과정에서 강사에 할당 되었는지 여부를 확인할 때 강사에 할당 하는 과정에 저장 됩니다는 [HashSet](https://msdn.microsoft.com/library/bb359438.aspx) 컬렉션입니다. `Assigned` 속성이 `true` courses 강사 할당 됩니다. 보기는 이 속성을 사용하여 선택된 것으로 표시되어야 하는 확인란을 결정합니다. 목록 보기에 전달 되는 마지막으로, 한 `ViewBag` 속성입니다.

다음으로 사용자가 **저장**을 클릭할 때 실행되는 코드를 추가합니다. 대체는 `EditPost` 메서드를 업데이트 하는 새 메서드를 호출 하는 다음 코드로 `Courses` 의 탐색 속성은 `Instructor` 엔터티. 변경 내용은 강조 표시되어 있습니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs?highlight=3,11,25,37,40-68)]

메서드 서명 간에 차이가 이제는 `HttpGet` `Edit` 에서 메서드 이름을 변경 하므로 `EditPost` 다시 `Edit`합니다.

보기의 컬렉션인 없으므로 `Course` 엔터티, 모델 바인더 자동으로 업데이트할 수는 `Courses` 탐색 속성입니다. 모델 바인더를 사용 하 여 업데이트 하는 대신는 `Courses` 탐색 속성에서 새 작업입니다 `UpdateInstructorCourses` 메서드. 따라서 모델 바인딩에서 `Courses` 속성을 제외해야 합니다. 호출 하는 코드를 변경 하지 않아도이 [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx) 사용 중 이므로 *허용 목록이* 오버 로드 및 `Courses` include 목록에 있지 않습니다.

경우 없는 확인란이 선택 된을의 코드 `UpdateInstructorCourses` 초기화는 `Courses` 는 빈 컬렉션 탐색 속성:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

그런 다음, 코드는 데이터베이스의 모든 강좌를 반복하고 현재 강사에게 할당된 것과 보기에서 선택되었던 것에 대해 각 강좌를 확인합니다. 효율적인 조회를 수행하기 위해 후자의 두 컬렉션은 `HashSet` 개체에 저장됩니다.

강좌에 대한 확인란이 선택됐지만 강좌가 `Instructor.Courses` 탐색 속성에 없는 경우 강좌는 탐색 속성의 컬렉션에 추가됩니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

강좌에 대한 확인란이 선택되지 않았지만 강좌가 `Instructor.Courses` 탐색 속성에 있는 경우 강좌는 탐색 속성에서 제거됩니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs)]

*Views\Instructor\Edit.cshtml*, 추가 **Courses** 을 추가 하 여 확인란의 배열로 필드 바로 다음 코드는 `div` 에 대 한 요소는 `OfficeAssignment` 필드 및 전에 `div` 에 대 한 요소는 **저장** 단추:

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml)]

코드, 줄 바꿈 및 들여쓰기 여기 에서처럼 표시 되지 않는 붙여 넣은 후, 수동으로 모든 항목을 여기 같이 수정 합니다. 들여쓰기는 완벽할 필요가 없지만 `@</tr><tr>`, `@:<td>`, `@:</td>` 및 `@</tr>` 줄은 표시된 것처럼 각각 한 줄에 있어야 합니다. 그렇지 않으면 런타임 오류가 발생합니다.

이 코드는 세 개의 열이 있는 HTML 테이블을 만듭니다. 각 열은 강좌 번호 및 제목으로 구성된 캡션이 뒤에 오는 확인란입니다. 모든 확인란 있어야 그룹으로 처리 해야 하는 모델 바인더에 게 동일한 이름 ("selectedCourses"). `value` 각 확인란의 특성의 값으로 설정 되어 `CourseID.` 모델 바인더 구성 된 컨트롤러에 배열을 전달 페이지가 게시 될 때는 `CourseID` 확인란만 선택 되에 대 한 값입니다.

강사에 할당 하는 과정에 사용 되는 것이 확인란은 처음 렌더링 됩니다 때 사용할 `checked` 특성 (에 확인 표시)을 선택 합니다.

사이트에 반환 될 때 변경 내용을 확인할 수 싶어하는 과정 할당을 변경한 후는 `Index` 페이지. 따라서 해당 페이지에 있는 테이블에 열을 추가 해야 합니다. 이 경우 있습니다 사용할 필요가 없습니다는 `ViewBag` 개체를 표시 하려는 정보를 이미 있으므로 `Courses` 의 탐색 속성은 `Instructor` 엔터티 모델로 페이지에 전달 하는 합니다.

*Views\Instructor\Index.cshtml*, 추가 **Courses** 제목 바로 다음에 **Office** 다음 예제와 같이 제목:

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cshtml?highlight=6)]

사무실 위치 정보 셀 바로 뒤에 새 세부 셀에 추가 합니다.

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml?highlight=7-14)]

실행 된 **강사 인덱스** 각 강사에 할당 된 과정을 보려면 페이지를:

![Instructor_index_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

클릭 **편집** 에서 강사 편집 페이지를 볼 수 있습니다.

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image11.png)

일부 과정 할당을 변경 하 고 클릭 **저장**합니다. 변경 내용은 인덱스 페이지에 반영됩니다.

 참고: 강사 과정 데이터를 편집 하려면 여기에 적용 되는 방법을 제한 된 수의 과목 필요한 경우에 작동 합니다. 훨씬 큰 컬렉션의 경우 다른 UI 및 다른 업데이트 메서드가 필요합니다.  
 

## <a name="update-the-deleteconfirmed-method"></a>Update DeleteConfirmed 메서드

*InstructorController.cs*, 삭제는 `DeleteConfirmed` 다음 해당 위치에 코드 메서드 및 삽입 합니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample24.cs?highlight=5-8,12-18)]

이 코드에서는 다음과 같이 변경 합니다.

- 강사 모든 부서의 관리자로 할당 된 경우 해당 부서에서 강사 할당을 제거 합니다. 이 코드 없이 부서에 대 한 관리자 권한으로 배정 강사를 삭제 하려고 했습니다. 참조 무결성 오류가 발생 것 있습니다.

이 코드의 여러 부서에 대 한 관리자 권한으로 할당 한 강사 시나리오를 처리 하지 않습니다. 마지막 자습서에서 해당 시나리오 상황이 발생 하지 않도록 하는 코드를 추가 합니다.

## <a name="add-office-location-and-courses-to-the-create-page"></a>만들기 페이지에 사무실 위치 및 강좌 추가

*InstructorController.cs*, 삭제는 `HttpGet` 및 `HttpPost` `Create` 메서드를 그 자리에 다음 코드를 추가 합니다.


[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample25.cs)]

이 코드는 유사 확인 했던 편집 방법에 대 한 제외 하 고 처음 없는 courses 선택 됩니다. `HttpGet` `Create` 메서드 호출의 `PopulateAssignedCourseData` 에 빈 컬렉션을 제공 하기 위해 선택 하지만 courses 있을 수 있기 때문에 하지 메서드는 `foreach` (그렇지 않은 경우 코드 보기는는 null 참조 예외를 throw 하는 보기에서 루프 ).

HttpPost Create 메서드는 선택한 각 과정 템플릿 코드를 유효성 검사 오류를 확인 하 고 데이터베이스에 새 강사를 추가 하기 전에 Courses 탐색 속성에 추가 합니다. 모델 오류가 있는 경우에 추가 됩니다 되도록 (예를 들어 잘못 된 날짜는 키가 지정 된 사용자)에 대 한 모델 오류가 있을 때의 한 과정 선택 내용을 자동으로 복원 때 페이지는 오류 메시지가 다시 표시, 되도록 합니다.

`Courses` 탐색 속성에 강좌를 추가할 수 있도록 빈 컬렉션으로 속성을 초기화해야 합니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample26.cs)]

컨트롤러 코드에서 이 작업을 수행하는 대안으로 다음 예제와 같이 존재하지 않는 경우 자동으로 컬렉션을 만들도록 getter 속성을 변경하여 강사 모델에서 해당 작업을 수행할 수 있습니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample27.cs)]

이러한 방식으로 `Courses` 속성을 수정하는 경우 컨트롤러에서 명시적 속성 초기화 코드를 제거할 수 있습니다.

*Views\Instructor\Create.cshtml*, 사무실 위치 입력란을 추가 하 고는 고용 날짜 필드 후 및 하기 전에 확인란 과정은 **전송** 단추입니다.

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample28.cshtml)]

코드를 붙여 넣은 후 수정 줄 바꿈과 편집 페이지에 대 한 이전 처럼 합니다.

만들기 페이지를 실행 하 고 강사를 추가 합니다.

![강사 과정을 사용 하 여 만들기](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image12.png)

<a id="transactions"></a>
## <a name="handling-transactions"></a>트랜잭션 처리

에 설명 된 대로 [기본 CRUD 기능 자습서](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md), 기본적으로 Entity Framework 암시적으로 구현 트랜잭션을 합니다. 여기서 필요한 세부적으로 제어할 수-예를 들어 트랜잭션에서-Entity Framework 밖에 서 수행 하는 작업을 포함 하도록 하려는 경우 시나리오 참조 [트랜잭션 작업을](https://msdn.microsoft.com/data/dn456843) msdn 합니다.

## <a name="summary"></a>요약

이제이 소개 관련 데이터로 작업을 완료 했습니다. 지금까지이 자습서에 사용해 보았다면 동기 I/O를 수행 하는 코드입니다. 비동기 코드를 구현 하 여 웹 서버 리소스를 보다 효율적으로 사용할 응용 프로그램을 만들 수 있고 자습서에서 수행할 것입니다.

이 자습서를 연결 하는 방법 및 향상 될 수 있습니다에 의견을 남겨 주세요. 새 항목을 요청할 수도 있습니다 [Me 방법으로 코드 보기](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code)합니다.

다른 Entity Framework 리소스에 대 한 링크에서 확인할 수 있습니다 [ASP.NET 데이터 액세스-권장 리소스](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.

> [!div class="step-by-step"]
> [이전](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [다음](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application.md)
