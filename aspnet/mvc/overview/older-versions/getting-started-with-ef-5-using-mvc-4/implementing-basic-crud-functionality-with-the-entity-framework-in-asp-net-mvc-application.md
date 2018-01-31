---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application
title: "ASP.NET MVC 응용 프로그램 (2 / 10)에서 Entity Framework와 함께 기본 CRUD 기능 구현 | Microsoft Docs"
author: tdykstra
description: "Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 5 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/30/2013
ms.topic: article
ms.assetid: f7bace3f-b85a-47ff-b5fe-49e81441cdf9
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: d031cd760fb578d29626933eed39fe987ef796d7
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="implementing-basic-crud-functionality-with-the-entity-framework-in-aspnet-mvc-application-2-of-10"></a>ASP.NET MVC 응용 프로그램 (2 / 10)에서 Entity Framework와 함께 기본 CRUD 기능 구현
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

[완료 된 프로젝트를 다운로드 합니다.](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 5 Code First 및 Visual Studio 2012를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대 한 정보를 참조 하십시오. [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다. 시작 부분에서 자습서 시리즈를 시작할 수 있습니다 또는 [이 장의 대 한 시작 프로젝트 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 여기에서 시작 하 고 있습니다.
> 
> > [!NOTE] 
> > 
> > 해결할 수 없는 문제에 직면 하는 경우 [완료 장 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 문제를 재현 하려고 합니다. 일반적으로 코드 완성 된 코드를 비교 하 여 문제에 솔루션을 찾을 수 있습니다. 몇 가지 일반적인 오류 및 해결 하는 방법에 대 한 참조 [오류 및 해결 방법입니다.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)


이전 자습서에서 저장 하 고 Entity Framework 및 SQL Server LocalDB를 사용 하 여 데이터를 표시 하는 MVC 응용 프로그램을 만들었습니다. 이 자습서를 검토 하는 CRUD 사용자 지정 (만들기, 읽기, 업데이트, 삭제)는 MVC 기반 구조는 자동으로에 만드는 코드를 사용자에 대 한 컨트롤러와 뷰.

> [!NOTE]
> 컨트롤러와 데이터 액세스 계층 간에 추상화 계층을 만들기 위해 리포지토리 패턴을 구현 하는 일반적인이 좋습니다. 이 자습서를 간단히 유지 하기 위해이 시리즈의 이후 자습서 될 때까지 저장소를 구현 하지 않습니다.


이 자습서에서는 다음 웹 페이지를 생성 합니다.

![Student_Details_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image1.png)

![Student_Edit_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image2.png)

![Student_Create_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image3.png)

![Student_delete_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image4.png)

## <a name="creating-a-details-page"></a>세부 정보 페이지 만들기

학생 들에 대 한 스 캐 폴드 코드 `Index` 페이지 생략는 `Enrollments` 속성을 속성 컬렉션을 보유 하기 때문에 있습니다. 에 `Details` 페이지 HTML 테이블에 컬렉션의 내용을 표시 합니다.

 *Controllers\StudentController.cs*에 대 한 작업 메서드는 `Details` 사용 하 여 보기는 `Find` 를 단일 검색할 메서드 `Student` 엔터티. 

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample1.cs)]

 키 값으로 메서드에 전달 되는 `id` 매개 변수에서 경로 데이터에서 제공 하 고는 **세부 정보** 인덱스 페이지의 하이퍼링크를 합니다. 

1. 열기 *Views\Student\Details.cshtml*합니다. 사용 하 여 각 필드가 표시 되는 `DisplayFor` 도우미, 다음 예제와 같이: 

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample2.cshtml)]
2. 후는 `EnrollmentDate` 필드 및 닫기 바로 앞 `fieldset` 태그를 다음 예제와 같이 등록, 목록을 표시 하는 코드를 추가 합니다.

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample3.cshtml?highlight=4-22)]

    이 코드의 엔터티는 반복의 `Enrollments` 탐색 속성입니다. 각 `Enrollment` 엔터티 과정 제목과 등급은 표시, 속성에 있습니다. 과정 이름을 검색 하는 `Course` 에 저장 된 엔터티는 `Course` 의 탐색 속성은 `Enrollments` 엔터티. 이 데이터의 모든 데이터베이스에서 검색 됩니다는 자동으로 필요 합니다. (즉, 사용 하는 지연 로드 여기 합니다. 지정 하지 않은 *즉시 로드* 에 대 한는 `Courses` 해당 속성에 액세스 하려고 처음으로 탐색 속성, 쿼리 데이터베이스에 전송 되는 데이터를 검색 합니다. 자세한 내용은 지연 로드 및 즉시 로드에 대 한는 [관련 데이터를 읽는](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) 이 시리즈의 뒷부분에 나오는 자습서입니다.)
3. 페이지를 선택 하 여 실행는 **학생** 탭을 클릭 한 **세부 정보** Alexander Carson에 대 한 링크입니다. 선택한 학생 과정 및 등급의 목록이 표시:

    ![Student_Details_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image5.png)

## <a name="updating-the-create-page"></a>만들기 페이지를 업데이트합니다.

1. *Controllers\StudentController.cs*, 대체는 `HttpPost``Create` 동작 메서드를 추가 하려면 다음 코드는 `try-catch` 블록 및 [바인딩 특성](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx) 스 캐 폴드 메서드에: 

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample4.cs?highlight=4,7-8,14-20)]

    이 코드는 추가 `Student` ASP.NET MVC 모델 바인더를에서 만든 엔터티는 `Students` 엔터티 설정 하 고 데이터베이스에 변경 내용을 저장 합니다. (*모델 바인더* 하는 것 보다 쉽게 폼에서 전송한 데이터에 사용할 수 있습니다, 모델 바인더는 게시 하는 변환 양식 값을 CLR 형식 및 동작 메서드 매개 변수에서 전달 하는 ASP.NET MVC 기능입니다. 이, 모델 바인더를 인스턴스화하는 `Student` 에서 엔터티 속성을 사용 하 여 값의 `Form` 컬렉션입니다.)

    `ValidateAntiForgeryToken` 특성을 사용 하면 방지할 수 [교차 사이트 요청 위조](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) 공격입니다.

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
2. 페이지를 선택 하 여 실행 된 **학생** 탭을 클릭 하 고 **새로 만들기**합니다.

    ![Student_Create_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image7.png)

    일부 데이터 유효성 검사는 기본적으로 작동합니다. 이름 및 잘못 된 날짜를 입력 하 고 클릭 **만들기** 오류 메시지를 확인 합니다.

    ![Students_Create_page_error_message](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image8.png)

    강조 표시 된 다음 코드에서는 모델 유효성 검사를 보여 줍니다.

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample7.cs?highlight=5)]

    9/1/2005 등 유효한 값으로 날짜를 변경 하 고 클릭 **만들기** 새 학생에 표시를 볼 수는 **인덱스** 페이지.

    ![Students_Index_page_with_new_student](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image9.png)

## <a name="updating-the-edit-post-page"></a>편집 POST 페이지를 업데이트합니다.

*Controllers\StudentController.cs*, `HttpGet` `Edit` 메서드 (없이 하나는 `HttpPost` 특성) 사용 하 여는 `Find` 를 선택한 검색할 메서드 `Student` 엔터티에으로 보여 준다는 사실을 알았습니다 에 `Details` 메서드. 이 방법을 변경할 필요가 없습니다.

그러나 대체는 `HttpPost` `Edit` 동작 메서드를 추가 하려면 다음 코드는 `try-catch` 블록 및 [바인딩 특성](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx):

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample8.cs)]

이 코드에서 본 것과 비슷합니다는 `HttpPost` `Create` 메서드. 그러나 엔터티 집합에 모델 바인더에서 만든 엔터티를 추가 하는 대신이 코드에 플래그를 설정 변경 되었음을 나타내는 엔터티. 때는 [SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx) 메서드가 호출 되는 [Modified](https://msdn.microsoft.com/library/system.data.entitystate.aspx) 플래그를 사용 하면 Entity Framework 데이터베이스 행을 업데이트 하는 SQL 문을 만들 수 있습니다. 사용자 변경 되지 않은 포함 하 여 데이터베이스 행의 모든 열을 업데이트할지 및 동시성 충돌은 무시 됩니다. (이 시리즈의 자습서의 뒷부분에서 동시성을 처리 하는 방법을 설명 합니다.)

### <a name="entity-states-and-the-attach-and-savechanges-methods"></a>엔터티 상태 및 연결, SaveChanges 메서드

메모리에 엔터티는 해당 행에는 데이터베이스와 동기화 하 고이 정보를 호출할 때 수행 되는 작업을 결정 하는 여부를 추적 데이터베이스 컨텍스트는 `SaveChanges` 메서드. 예를 들어 전달 하는 경우에 새 엔터티는 [추가](https://msdn.microsoft.com/library/system.data.entity.dbset.add(v=vs.103).aspx) 메서드 엔터티의 상태로 설정 된 `Added`합니다. 호출 하면는 [SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx) 메서드, 데이터베이스 컨텍스트 발급 SQL `INSERT` 명령입니다.

엔터티 중 하나에 있을 수 있습니다는[상태 다음](https://msdn.microsoft.com/library/system.data.entitystate.aspx):

- `Added`. 엔터티는 데이터베이스에 아직 존재 하지 않습니다. `SaveChanges` 메서드 실행 해야 합니다는 `INSERT` 문.
- `Unchanged`. 하 여이 엔터티를 사용 하 여 수행 해야 하는 아무 것도 `SaveChanges` 메서드. 데이터베이스에서 엔터티를 읽을 때 엔터티가이 상태에 있는 시작 합니다.
- `Modified`. 엔터티의 속성 값의 일부 또는 모든 수정 되었습니다. `SaveChanges` 메서드 실행 해야 합니다는 `UPDATE` 문.
- `Deleted`. 엔터티 삭제 하도록 표시 되었습니다. `SaveChanges` 메서드 실행 해야 합니다는 `DELETE` 문.
- `Detached`. 엔터티는 데이터베이스 컨텍스트에서 추적 되 고 있지 않습니다.

데스크톱 응용 프로그램 상태 변경 내용이 일반적으로 자동으로 설정 됩니다. 데스크톱 응용 프로그램 형식에 엔터티 읽고 속성 값 일부 변경 해야 합니다. 이렇게 하면 해당 엔터티 상태를 자동으로 변경 해야 `Modified`합니다. 호출 하면 `SaveChanges`, Entity Framework는 SQL 생성 `UPDATE` 변경 하는 실제 속성만 업데이트 하는 문입니다.

이 연속 시퀀스에 대 한 웹 앱의 연결이 끊어진된 특성 허용 하지 않습니다. [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx) 읽는 엔터티 페이지를 렌더링 한 다음 삭제 됩니다. 경우는 `HttpPost` `Edit` 동작 메서드는, 새 요청이 있고의 새 인스턴스는 [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx)엔터티 상태를 수동으로 설정 해야 하므로 `Modified.` 호출 하는 경우 다음 `SaveChanges`, Entity Framework는 컨텍스트는 변경 되는 속성을 알 수 없기 때문에 데이터베이스 행의 모든 열을 업데이트 합니다.

SQL 하려는 경우 `Update` 사용자 실제로 변경 된 필드만 업데이트 하는 문을 사용할 수 있는 경우 되도록 (예: 숨겨진된 필드) 어떤 식으로든에서 원래 값을 저장할 수는 `HttpPost` `Edit` 메서드를 호출 합니다. 그러면 만들 수 있습니다는 `Student` 원래 값이 호출을 사용 하 여 엔터티는 `Attach` 메서드는 해당 원래 버전은 엔터티의 엔터티의 값을 새 값으로 업데이트 한 다음 호출 `SaveChanges.` 자세한 내용은 참조 [ 엔터티 상태 및 SaveChanges](https://msdn.microsoft.com/data/jj592676) 및 [로컬 데이터](https://msdn.microsoft.com/data/jj592872) MSDN 데이터 개발자 센터에서.

코드 *Views\Student\Edit.cshtml* 에서 본 것과 비슷합니다 *Create.cshtml*, 및 변경이 필요 없음.

페이지를 선택 하 여 실행 된 **학생** 탭을 클릭 한 다음는 **편집** 하이퍼링크입니다.

![Student_Edit_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image10.png)

클릭 하 여 확인 하 고 데이터의 일부 변경 **저장**합니다. 인덱스 페이지에 변경 된 데이터를 표시 합니다.

![Students_Index_page_after_edit](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image11.png)

## <a name="updating-the-delete-page"></a>업데이트 페이지 삭제

*Controllers\StudentController.cs*, 템플릿 코드에 대 한는 `HttpGet` `Delete` 메서드는 `Find` 를 선택한 검색할 메서드 `Student` 엔터티에으로 보여 준다는 사실을 알았습니다에 `Details` 및 `Edit` 메서드. 그러나을 구현 하는 사용자 지정 오류 메시지에 대 한 호출 `SaveChanges` 실패 하면이 메서드를 해당 보기의 일부 기능을 추가 합니다.

업데이트에 대 한 준다는 사실을 알았습니다 하 고 작업을 만드는 두 개의 작업 메서드 삭제 작업에 필요 합니다. GET 요청에 대 한 응답에서 호출 되는 메서드를 승인 하거나 삭제 작업을 취소 하는 사용자에 게 제공 하는 보기를 표시 합니다. 사용자가 승인 하는 경우 POST 요청 생성 됩니다. 이 경우는 `HttpPost` `Delete` 메서드가 호출 되 고 실제로 해당 메서드에 삭제 동작을 수행 합니다.

추가 `try-catch` 블록는 `HttpPost` `Delete` 데이터베이스를 업데이트할 때 발생할 수 있는 오류를 처리 하는 메서드. 오류가 발생 하는 경우는 `HttpPost` `Delete` 메서드 호출의 `HttpGet` `Delete` 메서드, 오류가 발생 했음을 나타내는 매개 변수를 전달 합니다. `HttpGet Delete` 메서드 다음 기회 취소 하거나 다시 시도를 사용자에 게 제공 하는 오류 메시지와 함께 확인 페이지를 다시 표시 합니다.

1. 대체는 `HttpGet` `Delete` 오류 보고를 관리 하는 다음 코드로 작업 메서드: 

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample9.cs)]

    이 코드가 허용는 [선택적](https://msdn.microsoft.com/library/dd264739.aspx) ब ा ळ 실패 한 후 호출 된 여부를 나타내는 부울 매개 변수입니다. 이 매개 변수는 `false` 때는 `HttpGet` `Delete` 이전에 실패 한 없이 메서드를 호출 합니다. 에 의해 호출 됩니다는 `HttpPost` `Delete` 데이터베이스 업데이트 오류에 대 한 응답에서 메서드를 매개 변수는 `true` 보기에 오류 메시지가 전달 됩니다.
- 대체는 `HttpPost` `Delete` 동작 메서드 (라는 `DeleteConfirmed`)를 다음 코드로 실제 삭제 동작을 수행 하 고이 한 데이터베이스 업데이트 오류를 catch 합니다.

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample10.cs)]

    이 코드에서는 선택된 된 엔터티를 검색 한 다음 호출는 [제거](https://msdn.microsoft.com/library/system.data.entity.dbset.remove(v=vs.103).aspx) 엔터티의 상태 설정 하는 방법은 `Deleted`합니다. 때 `SaveChanges` 호출 되는 SQL `DELETE` 명령이 생성 합니다. 작업 메서드 이름을 변경한 `DeleteConfirmed` 를 `Delete`합니다. 명명 된 스 캐 폴드 코드는 `HttpPost` `Delete` 메서드 `DeleteConfirmed` 제공 하는 `HttpPost` 메서드는 고유의 시그니처가 있습니다. (CLR 오버 로드 된 메서드를 다른 메서드에 매개 변수가 필요 합니다.) 이제는 서명 되는 고유 수는 MVC 규칙 집중 하에 동일한 이름을 사용 하 여는 `HttpPost` 및 `HttpGet` 메서드를 삭제 합니다.

    대규모 응용 프로그램의 성능을 개선 하는 것이 중요, 호출 하는 코드 줄을 대체 하 여 행을 검색 하는 불필요 한 SQL 쿼리를 방지할 수 있습니다는 `Find` 및 `Remove` 노란색으로 표시 된 것 처럼 다음 코드를 사용 하 여 메서드 강조 표시 합니다.

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample11.cs)]

    이 코드를 인스턴스화하는 `Student` 기본 키 값을 사용 하 여 엔터티 엔터티 상태를 설정 합니다 `Deleted`합니다. Entity Framework는 엔터티를 삭제 하는 데 필요한 모든입니다.

    에서 설명한 것 처럼는 `HttpGet` `Delete` 메서드 데이터를 삭제 하지 않습니다. GET에 대 한 응답에서 delete 작업 수행 요청 (또는 모든 편집 작업을 수행 하는 문제에 대 한 작업 또는 데이터를 변경 하는 기타 작업이 만들기) 보안 위험이 생깁니다. 자세한 내용은 참조 [ASP.NET MVC 팁 #46-보안 허점을 만들기 때문에 삭제 링크를 사용 하지 않는](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx) Stephen Walther 블로그.
- *Views\Student\Delete.cshtml*, 사이의 오류 메시지가 추가 `h2` 제목 및 `h3` 다음 예제와 같이 제목:

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample12.cshtml?highlight=2)]

    페이지를 선택 하 여 실행 된 **학생** 탭을 클릭 하 고는 **삭제** 하이퍼링크:

    ![Student_Delete_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image12.png)
- 클릭 **삭제**합니다. 인덱스 페이지 삭제 된 학생 없이 표시 됩니다. (오류 처리 코드에서 실제 동작에서의 예를 볼 수는 [동시성 처리](../../getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md) 이 시리즈의 뒷부분에 나오는 자습서입니다.)

## <a name="ensuring-that-database-connections-are-not-left-open"></a>데이터베이스 연결 열기 남아 있지 않습니다 보장

데이터베이스 연결이 제대로 종료 하는 한 리소스를 해제 된, 나타납니다에 컨텍스트 인스턴스가 삭제 될 있는지 확인 하십시오. 즉 이유는 스 캐 폴드 코드를 제공 합니다는 [Dispose](https://msdn.microsoft.com/library/system.idisposable.dispose(v=vs.110).aspx) 메서드 끝에 `StudentController` 클래스 *StudentController.cs*다음 예제에 나온 것 처럼:

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample13.cs)]

기본 `Controller` 클래스 이미 구현은 `IDisposable` 이 코드는 재정의를 추가 하기만 하면 되므로 인터페이스는 `Dispose(bool)` 메서드를 명시적으로 컨텍스트 인스턴스를 삭제 합니다.

## <a name="summary"></a>요약

에 대 한 간단한 CRUD 작업을 수행 하는 페이지의 전체 집합 해야 `Student` 엔터티. 데이터 필드에 대 한 UI 요소를 생성 하 MVC 도우미를 사용 합니다. MVC 도우미에 대 한 자세한 내용은 참조 [양식을 사용 하 여 HTML 도우미 렌더링](https://msdn.microsoft.com/library/dd410596(v=VS.98).aspx) (페이지는 MVC 3 하지만 MVC 4와 여전히 관련이).

다음 자습서에서는 정렬 및 페이징을 추가 하 여 인덱스 페이지의 기능을 확장 합니다.

다른 Entity Framework 리소스에 대 한 링크에서 확인할 수 있습니다는 [ASP.NET 데이터 액세스 콘텐츠 맵](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.

>[!div class="step-by-step"]
[이전](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)
[다음](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)
