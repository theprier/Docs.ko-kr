---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application
title: ASP.NET MVC 응용 프로그램에서 Entity Framework 사용 하 여 기본 CRUD 기능 구현 | Microsoft Docs
author: tdykstra
description: Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 6 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 5 응용 프로그램을 만드는 방법을 보여 줍니다...
ms.author: aspnetcontent
ms.date: 03/09/2015
ms.assetid: a2f70ba4-83d1-4002-9255-24732726c4f2
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 20c4ec6835f65c267245c5b37cdd5648e9787c71
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37837703"
---
<a name="implementing-basic-crud-functionality-with-the-entity-framework-in-aspnet-mvc-application"></a>ASP.NET MVC 응용 프로그램에서 Entity Framework 사용 하 여 기본 CRUD 기능 구현
====================
[Tom Dykstra](https://github.com/tdykstra)

[완료 된 프로젝트를 다운로드](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8) 또는 [PDF 다운로드](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20Entity%20Framework%206%20Code%20First%20using%20MVC%205.pdf)

> Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 6 Code First 및 Visual Studio 2013을 사용 하 여 ASP.NET MVC 5 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대한 정보는 [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조하세요.


이전 자습서에서 저장 하 고 Entity Framework 및 SQL Server LocalDB를 사용 하 여 데이터를 표시 하는 MVC 응용 프로그램을 만들었습니다. 이 자습서를 검토 및 CRUD 사용자 지정 됩니다 (만들기, 읽기, 업데이트, 삭제) MVC 스 캐 폴딩 자동으로 만드는 코드를 컨트롤러 및 보기에서 합니다.

> [!NOTE]
> 컨트롤러와 데이터 액세스 계층 간에 추상화 계층을 만들기 위해 리포지토리 패턴을 구현하는 일반적인 사례입니다. 이러한 자습서를 간단하고 Entity Framework 자체를 사용하는 방법을 가르치는 데 초점을 두도록 유지하기 위해 리포지토리를 사용하지 않습니다. 리포지토리를 구현 하는 방법에 대 한 내용은 참조는 [ASP.NET 데이터 액세스 콘텐츠 맵](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.


이 자습서에서는 다음 웹 페이지를 만듭니다.

![Student_Details_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image1.png)

![Student_Edit_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image2.png)

![Student_delete_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image3.png)

## <a name="create-a-details-page"></a>세부 정보 페이지 만들기

학생을 위한 스 캐 폴드 된 코드 `Index` 생략 된 페이지는 `Enrollments` 속성을 속성 컬렉션을 보유 하기 때문에 합니다. 에 `Details` 페이지 HTML 테이블에 컬렉션의 콘텐츠를 표시 합니다.

 *Controllers\StudentController.cs*에 대 한 작업 메서드는 `Details` 사용 하 여 볼를 [찾을](https://msdn.microsoft.com/library/gg696418(v=VS.103).aspx) 단일 검색 방법 `Student` 엔터티. 

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample1.cs)]

키 값으로 메서드에 전달 됩니다는 `id` 매개 변수에서 제공 됩니다 *데이터 라우팅* 에 **세부 정보** 인덱스 페이지의 하이퍼링크입니다.

### <a name="tip-route-data"></a>팁: **데이터 라우팅**

경로 데이터는 모델 바인더는 라우팅 테이블에 지정 된 URL 세그먼트에 있는 데이터입니다. 기본 경로 지정 하는 예를 들어 `controller`하십시오 `action`, 및 `id` 세그먼트:

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample2.cs?highlight=3)]

다음 URL에서 기본 경로 매핑합니다 `Instructor` 으로 `controller`를 `Index` 으로 `action` 1을 `id`; 이들은 경로 데이터 값입니다.

`http://localhost:1230/Instructor/Index/1?courseID=2021`

"? courseID 2021 =" 쿼리 문자열 값입니다. 전달 하는 경우에 모델 바인더가 작동을 `id` 쿼리 문자열 값으로:

`http://localhost:1230/Instructor/Index?id=1&CourseID=2021`

Url에 의해 만들어집니다 `ActionLink` Razor 보기의 문입니다. 다음 코드에서를 `id` 하므로 일치 하는 기본 경로 매개 변수 `id` 경로 데이터에 추가 됩니다.

[!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample3.cshtml)]

다음 코드에서 `courseID` 쿼리 문자열로 추가 기본 경로 매개 변수와 일치 하지 않습니다.

[!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample4.cshtml)]


1. 오픈 *Views\Student\Details.cshtml*합니다. 사용 하 여 각 필드가 표시 되는 `DisplayFor` 다음 예와에서 같이 도우미:

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample5.cshtml)]
2. 후 합니다 `EnrollmentDate` 필드 및 닫기 직전 `</dl>` 태그를 다음 예제에서와 같이 등록의 경우 목록을 표시 하는 강조 표시 된 코드를 추가 합니다.

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample6.cshtml?highlight=8-29)]

    코드를 붙여넣은 후 코드 들여쓰기가 잘못된 경우 CTRL-K-D를 눌러 수정합니다.

    이 코드는 `Enrollments` 탐색 속성의 엔터티를 통해 반복됩니다. 각 `Enrollment` 엔터티 속성의이 강좌 제목과 등급을 표시 합니다. 강좌 제목은에서 검색 되는 `Course` 에 저장 된 엔터티는 `Course` 의 탐색 속성은 `Enrollments` 엔터티. 이 데이터를 모두 검색 됩니다 데이터베이스에서 자동으로 필요할 때. (즉, 사용 하는 지연 로드 여기 있습니다. 지정 하지 않았습니다 *로딩과* 에 대 한는 `Courses` 탐색 속성에 등록 된 학생 들에 게는 같은 쿼리에서 검색할 수 없습니다. 대신 처음으로 액세스 하려고 하면는 `Enrollments` 탐색 속성을 새 쿼리는 데이터베이스로 전송 데이터를 검색 합니다. 알아볼 수 있습니다 지연 로드 및 즉시 로드 하는 방법에 대 한 합니다 [관련 데이터를 읽는](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) 이 시리즈의 뒷부분에 나오는 자습서입니다.)
3. 선택 하 여 페이지를 실행 합니다 **학생** 탭을 클릭 하는 **세부 정보** Alexander Carson에 대 한 링크입니다. (경우 Details.cshtml 파일이 열려 있을 때 CTRL + F5 키를 누르면 있습니다 얻습니다 HTTP 400 오류가 Visual Studio에서 세부 정보 페이지를 실행 하려고 하지만 표시할 학생을 지정 하는 링크에서에 도달 하지 못한. 이전과 URL에서 "학생/세부 정보"를 제거 하 고 다시 시도 또는 브라우저를 닫습니다, 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **뷰**를 클릭 하 고 **브라우저에서 보기**.)

    선택한 학생에 대한 강좌 및 등급의 목록이 표시됩니다.

    ![Student_Details_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image4.png)

## <a name="update-the-create-page"></a>만들기 페이지 업데이트

1. *Controllers\StudentController.cs*, 대체를 `HttpPost``Create` 추가 하는 다음 코드를 사용 하 여 동작 메서드를 `try-catch` 차단 하 고 제거 `ID` 에서 [바인딩 특성](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx) 에 대 한 스 캐 폴드를 만듭니다.

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample7.cs?highlight=3,5-6,13-18)]

    이 코드를 추가 합니다 `Student` ASP.NET MVC 모델 바인더에서 만든 엔터티를 `Students` 엔터티 집합 및 데이터베이스에 변경 내용을 저장 합니다. (*바인더 모델* 양식에서 전송한 데이터로 작업 하기 쉽도록; 모델 바인더는 게시 하는 변환 양식 값을 CLR 형식 및 매개 변수의 동작 메서드에 전달 하는 ASP.NET MVC 기능을 가리킵니다. 이 경우, 모델 바인더를 인스턴스화하는 `Student` 에서 엔터티 속성을 사용 하 여 값을 `Form` 컬렉션.)

    제거 `ID` 때문에 특성 바인딩에서 `ID` 행이 삽입 될 때 SQL 서버가 자동으로 설정 하는 기본 키 값입니다. 사용자 입력을에서 설정 하지 않습니다는 `ID` 값입니다.

    <a id="overpost"></a>

    ### <a name="security-warning---the-validateantiforgerytoken-attribute-helps-prevent-cross-site-request-forgerysecurityxsrfcsrf-prevention-in-aspnet-mvc-and-web-pagesmd-attacks-it-requires-a-corresponding-htmlantiforgerytoken-statement-in-the-view-which-youll-see-later"></a>보안 경고-합니다 `ValidateAntiForgeryToken` 특성을 방지할 수 있습니다 [교차 사이트 요청 위조](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) 공격입니다. 해당 하는 것이 필요할 `Html.AntiForgeryToken()` 보기에서는 나중에 볼 수 있는 문.

    `Bind` 특성이 으로부터 보호 하기 위해 한 가지 방법은 *과도 한 게시* 에서 시나리오를 만듭니다. 예를 들어 합니다 `Student` 엔터티를 포함를 `Secret` 설정 하려면이 웹 페이지를 원하지 않는 속성입니다.

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample8.cs?highlight=7)]

    없는 경우에을 `Secret` 해커가 웹 페이지의 필드는와 같은 도구를 사용할 수 [fiddler](http://fiddler2.com/home), 게시할 일부 JavaScript를 작성 또는 `Secret` 양식 값입니다. 없이 [바인딩할](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx) 모델 바인더를 만들 때 사용 되는 필드를 제한 하는 특성을 `Student` 인스턴스<em>를</em> 모델 바인더를 선택 하는 `Secret` 양식 값을 사용 하 여 만들기는 `Student` 엔터티 인스턴스입니다. 그런 다음, 해커가 `Secret` 양식 필드에 대해 지정한 모든 값은 데이터베이스에서 업데이트됩니다. 다음 이미지는 표시 된 fiddler 도구 추가 `Secret` 필드 (값 "OverPost")에 게시 된 양식 값.

    ![](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image5.png)  

    값 "OverPost"는 웹 페이지가 속성을 설정할 수 있도록 의도하지 않았지만 삽입된 행의 `Secret` 속성에 성공적으로 추가됩니다.

    보안 모범 사례를 사용 하는 것을 `Include` 매개 변수를 `Bind` 특성을 *화이트 리스트* 필드. 사용 하 여도 가능 합니다 `Exclude` 매개 변수를 *블랙 리스트* 제외 하려는 필드입니다. 이유 `Include` 것이 더 안전는 새 속성을 엔터티에 추가 하면 새 필드가 자동으로 보호 되지 됩니다는 `Exclude` 목록입니다.

    방지할 수 있습니다 먼저 데이터베이스에서 엔터티를 읽고 다음 호출 하는 편집 시나리오에서 초과 게시 `TryUpdateModel`허용 되는 명시적 속성 목록에 전달 합니다. 이 자습서에서 사용 되는 방법입니다.

    여러 개발자가는 것이 좋습니다는 초과 게시를 방지 하는 다른 방법은 모델 바인딩을 사용 하 여 엔터티 클래스를 사용 하지 않고 보기 모델을 사용 하는 것입니다. 보기 모델에서 업데이트하려는 속성만 포함합니다. MVC 모델 바인더가 완료 되 면 필요에 따라 같은 도구를 사용 하는 엔터티 인스턴스에 보기 모델 속성 복사 [AutoMapper](http://automapper.org/)합니다. Db를 사용 합니다. 엔터티의 항목 인스턴스를 해당 상태를 Unchanged로 설정 하 고 Property("PropertyName")를 설정 합니다. 보기 모델에 포함 된 각 엔터티 속성에서 true로 IsModified 합니다. 이 방법은 편집 및 만들기 시나리오에서 모두 작동합니다.

    이외의 합니다 `Bind` 특성을 `try-catch` 블록은 스 캐 폴드 된 코드에 대 한 유일한 변경 내용. 파생 되는 예외가 [DataException](https://msdn.microsoft.com/library/system.data.dataexception.aspx) 는 변경 내용을 저장 하는 동안 발견, 일반 오류 메시지가 표시 됩니다. [DataException](https://msdn.microsoft.com/library/system.data.dataexception.aspx) 예외는 때때로 인해 하면 프로그래밍 오류가 아니라 응용 프로그램에 의해 다시 시도 하려면 사용자는 것이 좋습니다. 이 샘플에서 구현되지 않지만 프로덕션 품질 응용 프로그램은 예외를 기록합니다. 자세한 내용은 [모니터링 및 원격 분석(Azure로 실제 클라우드 앱 빌드)](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry.md#log)에서 **정보에 대한 로그** 섹션을 참조하세요.

    코드 *Views\Student\Create.cshtml* 에서 살펴본 내용과 비슷합니다 *Details.cshtml*점을 제외 하 고 `EditorFor` 고 `ValidationMessageFor` 도우미 대신각필드에사용됩니다`DisplayFor`. 관련 코드는 다음과 같습니다.

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample9.cshtml)]

    *Create.chstml* 도 포함 되어 있습니다 `@Html.AntiForgeryToken()`에서 작동 하는 합니다 `ValidateAntiForgeryToken` 방지 하는 컨트롤러 특성 [교차 사이트 요청 위조](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) 공격입니다.

    변경할 필요가 *Create.cshtml*합니다.
2. 선택 하 여 페이지를 실행 합니다 **학생** 탭을 클릭 하 고 **새로 만들기**합니다.
3. 이름 및 잘못 된 날짜를 입력 하 고 클릭 **만들기** 오류 메시지를 확인 합니다.

    ![Students_Create_page_error_message](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image6.png)

    이는 기본적으로 얻는 서버 쪽 유효성 검사입니다. 이후의 자습서에서 클라이언트 쪽 유효성 검사에 대한 코드를 생성하는 특성을 추가하는 방법도 알아봅니다. 다음 강조 표시 된 코드에서 모델 유효성 검사를 표시 합니다 **만들기** 메서드.

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample10.cs?highlight=1)]
4. 유효한 값으로 날짜를 변경하고 **만들기**를 클릭하여 **인덱스** 페이지에 표시되는 새 학생을 봅니다.

    ![Students_Index_page_with_new_student](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image7.png)

## <a name="update-the-edit-httppost-method"></a>업데이트 편집 HttpPost 메서드

*Controllers\StudentController.cs*, `HttpGet` `Edit` 메서드 (없는 것을 `HttpPost` 특성) 사용 하 여를 `Find` 선택한 검색 하는 방법 `Student` 본 때 엔터티를 에 `Details` 메서드. 이 메서드를 변경할 필요가 없습니다.

그러나 대체 합니다 `HttpPost` `Edit` 작업 메서드를 다음 코드로:

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample11.cs)]

이러한 변경 내용을 방지 하기 위해 보안 모범 사례 구현 [초과 게시](#overpost)를 생성 하는 스 캐 폴더는 `Bind` 특성 및 엔터티는 수정 된 플래그를 사용 하 여 집합에 모델 바인더에서 만든 엔터티를 추가 합니다. 때문에 코드가 더 이상 권장 합니다 `Bind` 특성에 나열 되지 않은 필드에서 기존의 모든 데이터를 지웁니다는 `Include` 매개 변수입니다. 나중에 MVC 컨트롤러 스 캐 폴더 업데이트할 생성 하지 않도록 `Bind` 편집 방법에 대 한 특성입니다.

새 코드는 기존 엔터티를 호출 읽습니다 [tryupdatemodel에 전달](https://msdn.microsoft.com/library/system.web.mvc.controller.tryupdatemodel(v=vs.118).aspx) 게시 된 양식 데이터의 사용자 입력에서 필드를 업데이트 합니다. Entity Framework의 자동 변경 집합을 추적 합니다 [Modified](https://msdn.microsoft.com/library/system.data.entitystate.aspx) 엔터티에서 플래그입니다. 경우는 [SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx) 메서드가 호출 되는 `Modified` 플래그를 사용 하면 데이터베이스 행을 업데이트 하는 SQL 문을 만들려면 Entity Framework. [동시성 충돌](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md) 무시 되 고 변경 하지 않은 사용자를 포함 하 여 데이터베이스 행의 모든 열 업데이트 됩니다. (자습서의 뒷부분에서는 동시성 충돌을 처리 하는 방법을 보여 줍니다. 및 엔터티가 Unchanged로 설정 하 고 개별 설정할 수만 데이터베이스에서 업데이트할 개별 필드를 원하는 경우 필드를 수정 합니다.)

초과 게시를 방지 하기 위해 모범 사례로, 편집 페이지에서 업데이트 가능 하려는 필드는의 허용 목록에는 `TryUpdateModel` 매개 변수입니다. 현재 보호하는 추가 필드가 없지만 모델 바인더에서 바인딩하길 원하는 필드를 나열하는 것은 향후에 데이터 모델에 필드를 추가하는지 확인하며, 여기에서 명시적으로 추가할 때까지 자동으로 보호됩니다.

이러한 변경 내용의 결과로 HttpPost 편집 메서드의 메서드 서명은 같습니다 HttpGet 편집 메서드를 따라서 EditPost 메서드 이름을 변경 했습니다.

> [!TIP] 
> 
> **엔터티 상태 연결 및 SaveChanges 메서드**
> 
> 데이터베이스 컨텍스트는 메모리의 엔터티가 데이터베이스의 해당 열과 동기화 상태인지 여부의 추적을 유지하고 이 정보는 `SaveChanges` 메서드를 호출할 때 발생하는 작업을 결정합니다. 예를 들어 새 엔터티를 전달할 때 합니다 [추가](https://msdn.microsoft.com/library/system.data.entity.dbset.add(v=vs.103).aspx) 엔터티의 상태를로 설정 하는 메서드를 `Added`입니다. 호출 하는 [SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx) 메서드를 데이터베이스 컨텍스트 문제는 SQL `INSERT` 명령입니다.
> 
> 엔터티 중 하나가 될 수 있습니다 합니다[상태를 다음](https://msdn.microsoft.com/library/system.data.entitystate.aspx):
> 
> - `Added`. 엔터티가는 데이터베이스에 아직 존재 하지 않습니다. 합니다 `SaveChanges` 메서드를 실행 해야 합니다는 `INSERT` 문입니다.
> - `Unchanged`. `SaveChanges` 메서드에서 이 엔터티로 아무 작업도 수행할 필요가 없습니다. 데이터베이스에서 엔터티를 읽을 때 엔터티는 이 상태로 시작합니다.
> - `Modified`. 일부 또는 모든 엔터티의 속성 값이 수정되었습니다. 합니다 `SaveChanges` 메서드를 실행 해야 합니다는 `UPDATE` 문입니다.
> - `Deleted`. 엔터티가 삭제되도록 표시되었습니다. 합니다 `SaveChanges` 메서드를 실행 해야 합니다는 `DELETE` 문입니다.
> - `Detached`. 엔터티가 데이터베이스 컨텍스트에 의해 추적되지 않습니다.
> 
> 데스크톱 응용 프로그램에서는 일반적으로 상태 변경 내용이 자동으로 설정됩니다. 데스크톱 응용 프로그램 유형, 엔터티를 읽을 하 고 해당 속성 값의 일부를 변경 합니다. 이렇게 하면 해당 엔터티 상태가 자동으로 `Modified`로 변경됩니다. 호출 하면 `SaveChanges`, Entity Framework는 SQL 생성 `UPDATE` 변경한 실제 속성만 업데이트 하는 문이 있습니다.
> 
> 이 연속 시퀀스에 대 한 웹 앱의 연결이 끊긴된 특성을 허용 하지 않습니다. 합니다 [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx) 읽는 엔터티 페이지를 렌더링 한 후 삭제 됩니다. 경우는 `HttpPost` `Edit` 동작 메서드는, 새 요청은 및의 새 인스턴스를 갖습니다 합니다 [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx)이므로 엔터티 상태를 수동으로 설정 해야 `Modified.` 호출 하는 경우 다음 `SaveChanges`, Entity Framework는 컨텍스트에서 변경한 속성을 알 수 있는 방법이 있으므로 데이터베이스 행의 모든 열을 업데이트 합니다.
> 
> SQL을 사용 하려는 경우 `Update` 사용자가 실제로 변경한 필드만 업데이트 문을 수 있도록 사용 가능한 경우 (예: 숨겨진된 필드) 어떤 방식으로든에서 원래 값을 저장할 수 있습니다 합니다 `HttpPost` `Edit` 메서드가 호출 됩니다. 만들 수 있습니다는 `Student` 원래 값이 호출을 사용 하 여 엔터티를 `Attach` 메서드는 엔터티의 해당 원래 버전을 사용 하 여 새 값을 엔터티의 값으로 업데이트 한 다음 호출 `SaveChanges.` 자세한 내용은 참조 하세요. [ 엔터티 상태 및 SaveChanges](https://msdn.microsoft.com/data/jj592676) 하 고 [로컬 데이터](https://msdn.microsoft.com/data/jj592872) MSDN 데이터 개발자 센터에서.


HTML 및 Razor 코드 *Views\Student\Edit.cshtml* 에서 살펴본 내용과 비슷합니다 *Create.cshtml*, 및 변경이 필요 하지 않습니다.

선택 하 여 페이지를 실행 합니다 **학생** 탭을 클릭 한 다음는 **편집** 하이퍼링크입니다.

![Student_Edit_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image8.png)

데이터의 일부를 변경하고 **저장**을 클릭합니다. 인덱스 페이지의 변경 된 데이터가 표시 됩니다.

![Students_Index_page_after_edit](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image9.png)

## <a name="updating-the-delete-page"></a>삭제 페이지 업데이트

*Controllers\StudentController.cs*에 대 한 템플릿 코드를 `HttpGet` `Delete` 메서드를 `Find` 메서드를 선택한 `Student` 엔터티에 것에서 본는 `Details` 및 `Edit` 메서드. 그러나 `SaveChanges`에 대한 호출이 실패하는 경우 사용자 지정 오류 메시지를 구현하려면 이 메서드 및 해당 보기에 일부 기능을 추가합니다.

업데이트 및 만들기 작업에 대해 본 것과 같이 삭제 작업에는 두 개의 작업 메서드가 필요합니다. GET 요청에 대 한 응답에서 호출 되는 메서드는 사용자 승인 또는 삭제 작업을 취소할 수 있는 기회를 제공 하는 보기를 표시 합니다. 사용자가 승인하는 경우 POST 요청이 생성됩니다. 이 경우는 `HttpPost` `Delete` 메서드가 호출 되 고 해당 메서드 삭제 작업을 실제로 수행 되는 다음입니다.

추가 `try-catch` 차단 합니다 `HttpPost` `Delete` 데이터베이스 업데이트 될 때 발생할 수 있는 오류를 처리 하는 방법. 오류가 발생 하는 경우는 `HttpPost` `Delete` 메서드 호출을 `HttpGet` `Delete` 메서드, 오류가 발생 했음을 나타내는 매개 변수를 전달 합니다. `HttpGet Delete` 메서드는 다음 사용자에 게 취소 또는 다시 시도 하는 기회를 제공 하는 오류 메시지와 함께 확인 페이지를 다시 표시 합니다.

1. 대체는 `HttpGet` `Delete` 오류 보고를 관리 하는 다음 코드를 사용 하 여 동작 메서드: 

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample12.cs?highlight=1,7-10)]

    이 코드는 허용 된 [선택적 매개 변수](https://msdn.microsoft.com/library/dd264739.aspx) 변경 내용을 저장 하는 오류가 발생 한 후 메서드가 호출 되었는지 여부를 나타내는입니다. 이 매개 변수가 `false` 때 합니다 `HttpGet` `Delete` 이전 실패 없이 호출 됩니다. 호출 되는 경우는 `HttpPost` `Delete` 는 데이터베이스 업데이트 오류에 대 한 응답에서 메서드를 매개 변수는 `true` 오류 메시지가 보기에 전달 됩니다.
2. 대체는 `HttpPost` `Delete` 동작 메서드 (라는 `DeleteConfirmed`) 다음 코드를 사용 하 여 실제 삭제 작업을 수행 하며 모든 데이터베이스 업데이트 오류를 catch 합니다.

     [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample13.cs)]

     이 코드는 선택한 엔터티를 검색 한 다음 호출을 [제거](https://msdn.microsoft.com/library/system.data.entity.dbset.remove(v=vs.103).aspx) 엔터티의 상태를 설정 하는 방법 `Deleted`. 때 `SaveChanges` 호출 되는 SQL `DELETE` 명령이 생성 됩니다. 또한 `DeleteConfirmed`에서 `Delete`로 작업 메서드 이름을 변경했습니다. 명명 된 스 캐 폴드 된 코드를 `HttpPost` `Delete` 메서드 `DeleteConfirmed` 제공 하는 `HttpPost` 메서드에 고유한 서명 합니다. (CLR에는 오버 로드 된 메서드가 다른 메서드 매개 변수를 가질 수 필요 합니다.) 이제 서명 되는 고유 수 MVC 규칙을 사용 하 여 계속 사용 하는 동일한 이름을 합니다 `HttpPost` 및 `HttpGet` 메서드를 삭제 합니다.

     호출 하는 코드 줄을 대체 하 여 행을 검색 하는 불필요 한 SQL 쿼리를 피할 수 경우 대규모 응용 프로그램에서 성능 향상을 우선 순위를 `Find` 및 `Remove` 메서드를 다음 코드로:

     [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample14.cs)]

     이 코드를 인스턴스화하는 `Student` 기본 키 값을 사용 하 여 엔터티 다음 엔터티 상태를 설정 하 고 `Deleted`입니다. Entity Framework에서 엔터티를 삭제하기 위해 필요한 모든 것입니다.

     언급 했 듯이 합니다 `HttpGet` `Delete` 메서드 데이터를 삭제 하지 않습니다. GET에 대 한 응답에서 delete 작업 수행 요청 (또는 편집 작업을 수행 하는 문제에 대 한 만들기 작업이 나 데이터를 변경 하는 다른 모든 작업) 보안 위험이 생깁니다. 자세한 내용은 [ASP.NET MVC 팁 #46-보안 허점을 만들기 때문에 삭제 링크를 사용 하지 않는](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx) Stephen Walther의 블로그입니다.
3. *Views\Student\Delete.cshtml*, 사이는 오류 메시지를 추가 합니다 `h2` 제목 및 `h3` 다음 예제에서와 같이 제목:

     [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample15.cshtml?highlight=2)]

     선택 하 여 페이지를 실행 합니다 **학생** 탭을 클릭 하는 **삭제** 하이퍼링크:

     ![Student_Delete_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image10.png)
4. **삭제**를 클릭합니다. 삭제된 학생 없이 인덱스 페이지가 표시됩니다. (오류 처리에서 실행 중인 코드의 예를 볼 수는 [동시성 자습서](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md).)

## <a name="closing-database-connections"></a>닫는 데이터베이스 연결

데이터베이스 연결 닫기 및 가능한 한 빨리 보유 하는 리소스를 확보,이 사용 하 여 완료 되 면 컨텍스트 인스턴스를 삭제 합니다. 스 캐 폴드 된 코드는 제공 이유 즉를 [Dispose](https://msdn.microsoft.com/library/system.idisposable.dispose(v=vs.110).aspx) 메서드 끝에 `StudentController` 클래스 *StudentController.cs*다음 예제에서와 같이:

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample16.cs)]

기본 `Controller` 클래스가 이미 구현 하는 `IDisposable` 인터페이스를이 코드는 재정의 추가 하기만 하면 되므로 `Dispose(bool)` 컨텍스트 인스턴스를 명시적으로 삭제 하는 방법입니다.

<a id="transactions"></a>
## <a name="handling-transactions"></a>트랜잭션 처리

기본적으로 Entity Framework는 트랜잭션을 암시적으로 구현합니다. 여러 행 또는 테이블을 변경 하 고 호출 하는 시나리오에서 `SaveChanges`, Entity Framework 했는지를 자동으로 변경 내용을 모두 성공 하거나 모두 실패 합니다. 일부 변경 내용이 먼저 완료된 다음, 오류가 발생하는 경우 해당 변경 내용이 자동으로 롤백됩니다. 여기서 더 본격적인 제어가 필요한-예를 들어 트랜잭션의 Entity Framework 밖에 서 수행한 작업을 포함 하려는 경우 시나리오를 참조 하세요 [트랜잭션과 작업](https://msdn.microsoft.com/data/dn456843) MSDN에 있습니다.

## <a name="summary"></a>요약

이제 대 한 간단한 CRUD 작업을 수행 하는 페이지의 전체 집합 `Student` 엔터티. 데이터 필드에 대 한 UI 요소를 생성 하려면 MVC 도우미를 사용 합니다. MVC 도우미에 대 한 자세한 내용은 참조 하세요. [양식을 사용 하 여 HTML 도우미 렌더링](https://msdn.microsoft.com/library/dd410596(v=VS.98).aspx) (페이지는 MVC 3 하지만 MVC 5에도 적용이 대 한).

다음 자습서에서 정렬 및 페이징을 추가 하 여 인덱스 페이지의 기능을 확장할 수 있습니다.

이 자습서를 연결 하는 방법을 개선할 수 것에 의견을 남겨 주세요. 새 항목을 요청할 수도 있습니다 [표시 코드 사용 방법 보기](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code)합니다.

다른 Entity Framework 리소스에 대 한 링크에서 찾을 수 있습니다 [ASP.NET 데이터 액세스-권장 리소스](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.

> [!div class="step-by-step"]
> [이전](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)
> [다음](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)
