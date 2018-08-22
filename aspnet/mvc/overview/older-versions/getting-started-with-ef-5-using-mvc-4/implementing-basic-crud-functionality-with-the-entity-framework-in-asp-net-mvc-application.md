---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application
title: ASP.NET MVC 응용 프로그램 (2 / 10)에서 Entity Framework 사용 하 여 기본 CRUD 기능 구현 | Microsoft Docs
author: tdykstra
description: Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 5 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: f7bace3f-b85a-47ff-b5fe-49e81441cdf9
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 999a598b6f9c9a16c596cb6c8d7bb46439876f01
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41827988"
---
<a name="implementing-basic-crud-functionality-with-the-entity-framework-in-aspnet-mvc-application-2-of-10"></a>ASP.NET MVC 응용 프로그램 (2 / 10)에서 Entity Framework 사용 하 여 기본 CRUD 기능 구현
====================
[Tom Dykstra](https://github.com/tdykstra)

[완료 된 프로젝트 다운로드](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 5 Code First 및 Visual Studio 2012를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대한 정보는 [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조하세요. 시작 부분에서 자습서 시리즈를 시작할 수 있습니다 또는 [이 장이에 대 한 시작 프로젝트 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 여기에서 시작 하 고 있습니다.
> 
> > [!NOTE] 
> > 
> > 해결할 수 없는 문제가 발생 하는 경우 [완성 된 장 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 문제를 재현 하려고 합니다. 일반적으로 코드의 완성 된 코드를 비교 하 여 문제에 솔루션을 찾을 수 있습니다. 몇 가지 일반적인 오류 및 해결 하는 방법에 대 한 참조 [오류 및 해결 방법입니다.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)


이전 자습서에서 저장 하 고 Entity Framework 및 SQL Server LocalDB를 사용 하 여 데이터를 표시 하는 MVC 응용 프로그램을 만들었습니다. 이 자습서를 검토 및 CRUD 사용자 지정 됩니다 (만들기, 읽기, 업데이트, 삭제) MVC 스 캐 폴딩 자동으로 만드는 코드를 컨트롤러 및 보기에서 합니다.

> [!NOTE]
> 컨트롤러와 데이터 액세스 계층 간에 추상화 계층을 만들기 위해 리포지토리 패턴을 구현하는 일반적인 사례입니다. 이러한 자습서를 간단히 유지 하기까지이 시리즈의 뒷부분에 나오는 자습서 리포지토리를 구현할 없습니다.


이 자습서에서는 다음 웹 페이지를 만듭니다.

![Student_Details_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image1.png)

![Student_Edit_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image2.png)

![Student_Create_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image3.png)

![Student_delete_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image4.png)

## <a name="creating-a-details-page"></a>세부 정보 페이지 만들기

학생을 위한 스 캐 폴드 된 코드 `Index` 생략 된 페이지는 `Enrollments` 속성을 속성 컬렉션을 보유 하기 때문에 합니다. 에 `Details` 페이지 HTML 테이블에 컬렉션의 콘텐츠를 표시 합니다.

 *Controllers\StudentController.cs*에 대 한 작업 메서드는 `Details` 사용 하 여 볼를 `Find` 단일 검색 방법 `Student` 엔터티. 

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample1.cs)]

 키 값으로 메서드에 전달 됩니다는 `id` 매개 변수에서 경로 데이터에서 제공 하 고는 **세부 정보** 인덱스 페이지의 하이퍼링크입니다. 

1. 오픈 *Views\Student\Details.cshtml*합니다. 사용 하 여 각 필드가 표시 되는 `DisplayFor` 다음 예와에서 같이 도우미: 

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample2.cshtml)]
2. 후 합니다 `EnrollmentDate` 필드 및 닫기 직전 `fieldset` 태그를 다음 예제에서와 같이 등록의 경우 목록을 표시 하는 코드를 추가 합니다.

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample3.cshtml?highlight=4-22)]

    이 코드는 `Enrollments` 탐색 속성의 엔터티를 통해 반복됩니다. 각 `Enrollment` 엔터티 속성의이 강좌 제목과 등급을 표시 합니다. 강좌 제목은에서 검색 되는 `Course` 에 저장 된 엔터티는 `Course` 의 탐색 속성은 `Enrollments` 엔터티. 이 데이터를 모두 검색 됩니다 데이터베이스에서 자동으로 필요할 때. (즉, 사용 하는 지연 로드 여기 있습니다. 지정 하지 않았습니다 *로딩과* 에 대 한는 `Courses` 탐색 속성을 해당 속성에 액세스 하려고 하면 처음으로 하므로, 쿼리는 데이터베이스로 전송 데이터를 검색 합니다. 알아볼 수 있습니다 지연 로드 및 즉시 로드 하는 방법에 대 한 합니다 [관련 데이터를 읽는](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) 이 시리즈의 뒷부분에 나오는 자습서입니다.)
3. 선택 하 여 페이지를 실행 합니다 **학생** 탭을 클릭 하는 **세부 정보** Alexander Carson에 대 한 링크입니다. 선택한 학생에 대한 강좌 및 등급의 목록이 표시됩니다.

    ![Student_Details_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image5.png)

## <a name="updating-the-create-page"></a>만들기 페이지 업데이트

1. *Controllers\StudentController.cs*, 대체를 `HttpPost``Create` 추가 하는 다음 코드를 사용 하 여 동작 메서드를 `try-catch` 블록 및 [바인딩 특성](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx) 스 캐 폴드 된 방법: 

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample4.cs?highlight=4,7-8,14-20)]

    이 코드를 추가 합니다 `Student` ASP.NET MVC 모델 바인더에서 만든 엔터티를 `Students` 엔터티 집합 및 데이터베이스에 변경 내용을 저장 합니다. (*바인더 모델* 양식에서 전송한 데이터로 작업 하기 쉽도록; 모델 바인더는 게시 하는 변환 양식 값을 CLR 형식 및 매개 변수의 동작 메서드에 전달 하는 ASP.NET MVC 기능을 가리킵니다. 이 경우, 모델 바인더를 인스턴스화하는 `Student` 에서 엔터티 속성을 사용 하 여 값을 `Form` 컬렉션.)

    합니다 `ValidateAntiForgeryToken` 특성을 방지할 수 있습니다 [교차 사이트 요청 위조](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) 공격입니다.

<a id="overpost"></a>

    > [!WARNING]
    > Security - The `Bind` attribute is added to protect against *over-posting*. For example, suppose the `Student` entity includes a `Secret` property that you don't want this web page to update.
    > 
    > [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample5.cs?highlight=7)]
    > 
    > Even if you don't have a `Secret` field on the web page, a hacker could use a tool such as [fiddler](http://fiddler2.com/home), or write some JavaScript, to post a `Secret` form value. Without the [Bind](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx) attribute limiting the fields that the model binder uses when it creates a `Student` instance*,* the model binder would pick up that `Secret` form value and use it to update the `Student` entity instance. Then whatever value the hacker specified for the `Secret` form field would be updated in your database. The following image shows the fiddler tool adding the `Secret` field (with the value "OverPost") to the posted form values.
    > 
    > ![](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image6.png)  
    > 
    > The value "OverPost" would then be successfully added to the `Secret` property of the inserted row, although you never intended that the web page be able to update that property.
    > 
    > It's a security best practice to use the `Include` parameter with the `Bind` attribute to *whitelist* fields. It's also possible to use the `Exclude` parameter to *blacklist* fields you want to exclude. The reason `Include` is more secure is that when you add a new property to the entity, the new field is not automatically protected by an `Exclude` list.
    > 
    > Another alternative approach, and one preferred by many, is to use only view models with model binding. The view model contains only the properties you want to bind. Once the MVC model binder has finished, you copy the view model properties to the entity instance.

    Other than the `Bind` attribute, the `try-catch` block is the only change you've made to the scaffolded code. If an exception that derives from [DataException](https://msdn.microsoft.com/library/system.data.dataexception.aspx) is caught while the changes are being saved, a generic error message is displayed. [DataException](https://msdn.microsoft.com/library/system.data.dataexception.aspx) exceptions are sometimes caused by something external to the application rather than a programming error, so the user is advised to try again. Although not implemented in this sample, a production quality application would log the exception (and non-null inner exceptions ) with a logging mechanism such as [ELMAH](https://code.google.com/p/elmah/).

    The code in *Views\Student\Create.cshtml* is similar to what you saw in *Details.cshtml*, except that `EditorFor` and `ValidationMessageFor` helpers are used for each field instead of `DisplayFor`. The following example shows the relevant code:

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample6.cshtml)]

    *Create.chstml* also includes `@Html.AntiForgeryToken()`, which works with the `ValidateAntiForgeryToken` attribute in the controller to help prevent [cross-site request forgery](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) attacks.

    No changes are required in *Create.cshtml*.
2. 선택 하 여 페이지를 실행 합니다 **학생** 탭을 클릭 하 고 **새로 만들기**합니다.

    ![Student_Create_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image7.png)

    데이터 유효성 검사는 기본적으로 작동합니다. 이름 및 잘못 된 날짜를 입력 하 고 클릭 **만들기** 오류 메시지를 확인 합니다.

    ![Students_Create_page_error_message](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image8.png)

    다음 강조 표시 된 코드는 모델 유효성 검사를 보여 줍니다.

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample7.cs?highlight=5)]

    2005 년 9 월 1 일 등 유효한 값으로 날짜를 변경 하 고 클릭 **만들기** 나타나는 새 학생을 참조 하는 **인덱스** 페이지.

    ![Students_Index_page_with_new_student](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image9.png)

## <a name="updating-the-edit-post-page"></a>편집 후 페이지를 업데이트 하는 중

*Controllers\StudentController.cs*, `HttpGet` `Edit` 메서드 (없는 것을 `HttpPost` 특성) 사용 하 여를 `Find` 선택한 검색 하는 방법 `Student` 본 때 엔터티를 에 `Details` 메서드. 이 메서드를 변경할 필요가 없습니다.

그러나 대체 합니다 `HttpPost` `Edit` 추가 하려면 다음 코드를 사용 하 여 동작 메서드는 `try-catch` 블록 및 [바인딩 특성](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx):

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample8.cs)]

이 코드에서 살펴본 내용과 비슷합니다는 `HttpPost` `Create` 메서드. 그러나 엔터티 집합에 모델 바인더에서 만든 엔터티를 추가 하는 대신이 코드에 플래그를 설정 변경 되었음을 나타내는 엔터티. 경우는 [SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx) 메서드를 호출 합니다 [Modified](https://msdn.microsoft.com/library/system.data.entitystate.aspx) 플래그를 사용 하면 데이터베이스 행을 업데이트 하는 SQL 문을 만들려면 Entity Framework. 데이터베이스 행의 모든 열은 업데이트를 포함 하 여 사용자를 변경 하지 않은 되 고 동시성 충돌은 무시 됩니다. (이 시리즈의 자습서의 뒷부분에서 동시성을 처리 하는 방법을 알아봅니다 있습니다.)

### <a name="entity-states-and-the-attach-and-savechanges-methods"></a>엔터티 상태 연결 및 SaveChanges 메서드

데이터베이스 컨텍스트는 메모리의 엔터티가 데이터베이스의 해당 열과 동기화 상태인지 여부의 추적을 유지하고 이 정보는 `SaveChanges` 메서드를 호출할 때 발생하는 작업을 결정합니다. 예를 들어 새 엔터티를 전달할 때 합니다 [추가](https://msdn.microsoft.com/library/system.data.entity.dbset.add(v=vs.103).aspx) 엔터티의 상태를로 설정 하는 메서드를 `Added`입니다. 호출 하는 [SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx) 메서드를 데이터베이스 컨텍스트 문제는 SQL `INSERT` 명령입니다.

엔터티 중 하나가 될 수 있습니다 합니다[상태를 다음](https://msdn.microsoft.com/library/system.data.entitystate.aspx):

- `Added`. 엔터티가는 데이터베이스에 아직 존재 하지 않습니다. 합니다 `SaveChanges` 메서드를 실행 해야 합니다는 `INSERT` 문입니다.
- `Unchanged`. `SaveChanges` 메서드에서 이 엔터티로 아무 작업도 수행할 필요가 없습니다. 데이터베이스에서 엔터티를 읽을 때 엔터티는 이 상태로 시작합니다.
- `Modified`. 일부 또는 모든 엔터티의 속성 값이 수정되었습니다. 합니다 `SaveChanges` 메서드를 실행 해야 합니다는 `UPDATE` 문입니다.
- `Deleted`. 엔터티가 삭제되도록 표시되었습니다. 합니다 `SaveChanges` 메서드를 실행 해야 합니다는 `DELETE` 문입니다.
- `Detached`. 엔터티가 데이터베이스 컨텍스트에 의해 추적되지 않습니다.

데스크톱 응용 프로그램에서는 일반적으로 상태 변경 내용이 자동으로 설정됩니다. 데스크톱 응용 프로그램 유형, 엔터티를 읽을 하 고 해당 속성 값의 일부를 변경 합니다. 이렇게 하면 해당 엔터티 상태가 자동으로 `Modified`로 변경됩니다. 호출 하면 `SaveChanges`, Entity Framework는 SQL 생성 `UPDATE` 변경한 실제 속성만 업데이트 하는 문이 있습니다.

이 연속 시퀀스에 대 한 웹 앱의 연결이 끊긴된 특성을 허용 하지 않습니다. 합니다 [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx) 읽는 엔터티 페이지를 렌더링 한 후 삭제 됩니다. 경우는 `HttpPost` `Edit` 동작 메서드는, 새 요청은 및의 새 인스턴스를 갖습니다 합니다 [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx)이므로 엔터티 상태를 수동으로 설정 해야 `Modified.` 호출 하는 경우 다음 `SaveChanges`, Entity Framework는 컨텍스트에서 변경한 속성을 알 수 있는 방법이 있으므로 데이터베이스 행의 모든 열을 업데이트 합니다.

SQL을 사용 하려는 경우 `Update` 사용자가 실제로 변경한 필드만 업데이트 문을 수 있도록 사용 가능한 경우 (예: 숨겨진된 필드) 어떤 방식으로든에서 원래 값을 저장할 수 있습니다 합니다 `HttpPost` `Edit` 메서드가 호출 됩니다. 만들 수 있습니다는 `Student` 원래 값이 호출을 사용 하 여 엔터티를 `Attach` 메서드는 엔터티의 해당 원래 버전을 사용 하 여 새 값을 엔터티의 값으로 업데이트 한 다음 호출 `SaveChanges.` 자세한 내용은 참조 하세요. [ 엔터티 상태 및 SaveChanges](https://msdn.microsoft.com/data/jj592676) 하 고 [로컬 데이터](https://msdn.microsoft.com/data/jj592872) MSDN 데이터 개발자 센터에서.

코드 *Views\Student\Edit.cshtml* 에서 살펴본 내용과 비슷합니다 *Create.cshtml*, 및 변경이 필요 하지 않습니다.

선택 하 여 페이지를 실행 합니다 **학생** 탭을 클릭 한 다음는 **편집** 하이퍼링크입니다.

![Student_Edit_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image10.png)

데이터의 일부를 변경하고 **저장**을 클릭합니다. 인덱스 페이지의 변경 된 데이터가 표시 됩니다.

![Students_Index_page_after_edit](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image11.png)

## <a name="updating-the-delete-page"></a>삭제 페이지 업데이트

*Controllers\StudentController.cs*에 대 한 템플릿 코드를 `HttpGet` `Delete` 메서드를 `Find` 메서드를 선택한 `Student` 엔터티에 것에서 본는 `Details` 및 `Edit` 메서드. 그러나 `SaveChanges`에 대한 호출이 실패하는 경우 사용자 지정 오류 메시지를 구현하려면 이 메서드 및 해당 보기에 일부 기능을 추가합니다.

업데이트 및 만들기 작업에 대해 본 것과 같이 삭제 작업에는 두 개의 작업 메서드가 필요합니다. GET 요청에 대 한 응답에서 호출 되는 메서드는 사용자 승인 또는 삭제 작업을 취소할 수 있는 기회를 제공 하는 보기를 표시 합니다. 사용자가 승인하는 경우 POST 요청이 생성됩니다. 이 경우는 `HttpPost` `Delete` 메서드가 호출 되 고 해당 메서드 삭제 작업을 실제로 수행 되는 다음입니다.

추가 `try-catch` 차단 합니다 `HttpPost` `Delete` 데이터베이스 업데이트 될 때 발생할 수 있는 오류를 처리 하는 방법. 오류가 발생 하는 경우는 `HttpPost` `Delete` 메서드 호출을 `HttpGet` `Delete` 메서드, 오류가 발생 했음을 나타내는 매개 변수를 전달 합니다. `HttpGet Delete` 메서드는 다음 사용자에 게 취소 또는 다시 시도 하는 기회를 제공 하는 오류 메시지와 함께 확인 페이지를 다시 표시 합니다.

1. 대체는 `HttpGet` `Delete` 오류 보고를 관리 하는 다음 코드를 사용 하 여 동작 메서드: 

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample9.cs)]

    이 코드는 허용 된 [선택적](https://msdn.microsoft.com/library/dd264739.aspx) 변경 내용을 저장 하는 오류가 발생 한 후 호출 되었는지 여부를 나타내는 부울 매개 변수입니다. 이 매개 변수가 `false` 때 합니다 `HttpGet` `Delete` 이전 실패 없이 호출 됩니다. 호출 되는 경우는 `HttpPost` `Delete` 는 데이터베이스 업데이트 오류에 대 한 응답에서 메서드를 매개 변수는 `true` 오류 메시지가 보기에 전달 됩니다.
2. 대체는 `HttpPost` `Delete` 동작 메서드 (라는 `DeleteConfirmed`) 다음 코드를 사용 하 여 실제 삭제 작업을 수행 하며 모든 데이터베이스 업데이트 오류를 catch 합니다.

     [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample10.cs)]

     이 코드는 선택한 엔터티를 검색 한 다음 호출을 [제거](https://msdn.microsoft.com/library/system.data.entity.dbset.remove(v=vs.103).aspx) 엔터티의 상태를 설정 하는 방법 `Deleted`. 때 `SaveChanges` 호출 되는 SQL `DELETE` 명령이 생성 됩니다. 또한 `DeleteConfirmed`에서 `Delete`로 작업 메서드 이름을 변경했습니다. 명명 된 스 캐 폴드 된 코드를 `HttpPost` `Delete` 메서드 `DeleteConfirmed` 제공 하는 `HttpPost` 메서드에 고유한 서명 합니다. (CLR에는 오버 로드 된 메서드가 다른 메서드 매개 변수를 가질 수 필요 합니다.) 이제 서명 되는 고유 수 MVC 규칙을 사용 하 여 계속 사용 하는 동일한 이름을 합니다 `HttpPost` 및 `HttpGet` 메서드를 삭제 합니다.

     호출 하는 코드 줄을 대체 하 여 행을 검색 하는 불필요 한 SQL 쿼리를 피할 수 경우 대규모 응용 프로그램에서 성능 향상을 우선 순위를 `Find` 및 `Remove` 노란색으로 표시 된 것 처럼 다음 코드를 사용 하 여 메서드 강조 표시 합니다.

     [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample11.cs)]

     이 코드를 인스턴스화하는 `Student` 기본 키 값을 사용 하 여 엔터티 다음 엔터티 상태를 설정 하 고 `Deleted`입니다. Entity Framework에서 엔터티를 삭제하기 위해 필요한 모든 것입니다.

     언급 했 듯이 합니다 `HttpGet` `Delete` 메서드 데이터를 삭제 하지 않습니다. GET에 대 한 응답에서 delete 작업 수행 요청 (또는 편집 작업을 수행 하는 문제에 대 한 만들기 작업이 나 데이터를 변경 하는 다른 모든 작업) 보안 위험이 생깁니다. 자세한 내용은 [ASP.NET MVC 팁 #46-보안 허점을 만들기 때문에 삭제 링크를 사용 하지 않는](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx) Stephen Walther의 블로그입니다.
3. *Views\Student\Delete.cshtml*, 사이는 오류 메시지를 추가 합니다 `h2` 제목 및 `h3` 다음 예제에서와 같이 제목:

     [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample12.cshtml?highlight=2)]

     선택 하 여 페이지를 실행 합니다 **학생** 탭을 클릭 하는 **삭제** 하이퍼링크:

     ![Student_Delete_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image12.png)
4. **삭제**를 클릭합니다. 삭제된 학생 없이 인덱스 페이지가 표시됩니다. (오류 처리에서 실행 중인 코드의 예를 볼 수는 [동시성 처리](../../getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md) 이 시리즈의 뒷부분에 나오는 자습서입니다.)

## <a name="ensuring-that-database-connections-are-not-left-open"></a>데이터베이스 연결 열기 남아 있지 않습니다을 보장 합니다.

데이터베이스 연결이 제대로 닫혀 있고 보유를 해제 하 여 리소스를 표시 되도록 컨텍스트 인스턴스가 삭제 되는 있는지 확인 하십시오. 스 캐 폴드 된 코드는 제공 이유 즉를 [Dispose](https://msdn.microsoft.com/library/system.idisposable.dispose(v=vs.110).aspx) 메서드 끝에 `StudentController` 클래스 *StudentController.cs*다음 예제에서와 같이:

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample13.cs)]

기본 `Controller` 클래스가 이미 구현 하는 `IDisposable` 인터페이스를이 코드는 재정의 추가 하기만 하면 되므로 `Dispose(bool)` 컨텍스트 인스턴스를 명시적으로 삭제 하는 방법입니다.

## <a name="summary"></a>요약

이제 대 한 간단한 CRUD 작업을 수행 하는 페이지의 전체 집합 `Student` 엔터티. 데이터 필드에 대 한 UI 요소를 생성 하려면 MVC 도우미를 사용 합니다. MVC 도우미에 대 한 자세한 내용은 참조 하세요. [양식을 사용 하 여 HTML 도우미 렌더링](https://msdn.microsoft.com/library/dd410596(v=VS.98).aspx) (페이지는 MVC 3와 이지만 여전히 MVC 4 관련 된에 대 한).

다음 자습서에서 정렬 및 페이징을 추가 하 여 인덱스 페이지의 기능을 확장할 수 있습니다.

다른 Entity Framework 리소스에 대 한 링크에서 찾을 수 있습니다 합니다 [ASP.NET 데이터 액세스 콘텐츠 맵](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.

> [!div class="step-by-step"]
> [이전](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)
> [다음](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)
