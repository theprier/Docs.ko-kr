---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-8
title: 먼저 Entity Framework 4.0 Database를 사용 하 여 시작 및 ASP.NET 4 Web Forms-8 부 | Microsoft Docs
author: tdykstra
description: Contoso University 샘플 웹 응용 프로그램에는 Entity Framework를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 샘플 응용 프로그램은...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: aaadd9bb-5508-448c-ad57-5497dff90e13
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-8
msc.type: authoredcontent
ms.openlocfilehash: 249677c9e0eca248710bf730e57a7aeca5a9b5ce
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41835489"
---
<a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-8"></a>먼저 Entity Framework 4.0 Database를 사용 하 여 시작 및 ASP.NET 4 Web Forms-8 부
====================
[Tom Dykstra](https://github.com/tdykstra)

> Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 4.0 및 Visual Studio 2010을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대 한 정보를 참조 하세요. [시리즈의 첫 번째 자습서](the-entity-framework-and-aspnet-getting-started-part-1.md)


## <a name="using-dynamic-data-functionality-to-format-and-validate-data"></a>Dynamic Data 기능을 사용 하 여 서식을 지정 하 고 데이터 유효성 검사

이전 자습서에서 저장된 프로시저를 구현 합니다. 이 자습서에서는 보여줍니다 Dynamic Data 기능 다음과 같은 이점을 제공할 수 있습니다 하는 방법:

- 필드는 자동으로 해당 데이터 형식을 기반으로 하는 디스플레이에 서식이 지정 됩니다.
- 필드는 해당 데이터 형식을 기반으로 자동으로 유효성이 검사 합니다.
- 서식 지정 및 유효성 검사 동작을 사용자 지정 데이터 모델에 메타 데이터를 추가할 수 있습니다. 이렇게 하면 하나의 위치에서 서식 지정 및 유효성 검사 규칙을 추가할 수 있습니다 하 고 어디에서 나 자동으로 적용 되는 동적 데이터 컨트롤을 사용 하 여 필드에 액세스 하 합니다.

사용할 컨트롤을 표시 하 고 기존 필드를 편집 합니다.이 과정을 보려면 변경 *Students.aspx* 페이지에서 추가 서식 지정 및 유효성 검사 메타 데이터 이름 및 날짜 필드에는 `Student` 엔터티 형식입니다.

[![Image01](the-entity-framework-and-aspnet-getting-started-part-8/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image1.png)

## <a name="using-dynamicfield-and-dynamiccontrol-controls"></a>DynamicField 및 DynamicControl 컨트롤을 사용 하 여

열기는 *Students.aspx* 페이지 및 합니다 `StudentsGridView` 제어 바꾸기는 **이름** 및 **등록 날짜** `TemplateField` 다음 태그를 사용 하 여 요소:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample1.aspx)]

이 태그를 사용 하 여 `DynamicControl` 대신 제어 `TextBox` 하 고 `Label` 학생에서 컨트롤 템플릿 필드 이름을 지정 하 고 사용 하 여는 `DynamicField` 등록 날짜에 대 한 제어 합니다. 없는 형식 문자열을 지정 합니다.

추가 `ValidationSummary` 후에 컨트롤을 `StudentsGridView` 제어 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample2.aspx)]

에 `SearchGridView` 컨트롤에 대 한 태그를 바꿉니다는 **이름** 및 **등록 날짜** 에서 수행한 대로 열을 `StudentsGridView` 컨트롤을 생략 하는 제외는 `EditItemTemplate` 요소. `Columns` 의 요소는 `SearchGridView` 컨트롤은 이제 다음 태그를 포함 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample3.aspx)]

오픈 *Students.aspx.cs* 추가한 다음 `using` 문:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample4.cs)]

페이지에 대 한 처리기를 추가 `Init` 이벤트:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample5.cs)]

이 코드는 동적 데이터 서식 지정 및 유효성 검사의 필드에 대 한 이러한 데이터 바인딩된 컨트롤에서 제공 됩니다는 지정 된 `Student` 엔터티. 페이지를 실행 하는 경우 다음 예제와 같이 오류 메시지를 받게 되 면 일반적으로 의미를 호출 하지 않았습니다 합니다 `EnableDynamicData` 의 메서드 `Page_Init`:

`Could not determine a MetaTable. A MetaTable could not be determined for the data source 'StudentsEntityDataSource' and one could not be inferred from the request URL.`

페이지를 실행 합니다.

[![Image03](the-entity-framework-and-aspnet-getting-started-part-8/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image3.png)

에 **Enrollment Date** 열에서 속성 형식이 이기 때문에 날짜와 함께 표시 됩니다 `DateTime`. 나중에 수정 됩니다.

이제 동적 데이터가 기본 데이터 유효성 검사를 자동으로 제공 하는 알 수 있습니다. 예를 들어, 클릭 **편집**날짜 필드를 지우고, 클릭 **업데이트**는 동적 데이터 자동으로 수행이 필요한 필드 값이 데이터 모델에서 null을 허용 하기 때문에 표시 합니다. 필드에 오류 메시지가 후 별표를 표시 하는 페이지는 `ValidationSummary` 제어 합니다.

[![Image05](the-entity-framework-and-aspnet-getting-started-part-8/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image5.png)

생략할 수 있습니다는 `ValidationSummary` 컨트롤, 오류 메시지를 보려면 별표 위에 마우스 포인터를 포함할 수 있습니다.

[![Image06](the-entity-framework-and-aspnet-getting-started-part-8/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image7.png)

동적 데이터는 입력 데이터 유효성 검사도 합니다 **Enrollment Date** 필드는 유효한 날짜:

[![Image04](the-entity-framework-and-aspnet-getting-started-part-8/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image9.png)

알 수 있듯이 일반 오류 메시지입니다. 다음 섹션에서는 메시지와 유효성 검사 및 서식 지정 규칙을 사용자 지정 하는 방법을 배웁니다.

## <a name="adding-metadata-to-the-data-model"></a>데이터 모델에 대 한 메타 데이터 추가

일반적으로 동적 데이터에서 제공한 기능을 사용자 지정 해야 합니다. 예를 들어 데이터는 표시 하는 방법 및 오류 메시지의 콘텐츠를 변경할 수 있습니다. 하면 일반적으로 데이터 유효성 검사 규칙을 사용자 지정 동적 데이터에서 제공 하는 것 보다 더 많은 기능을 제공 데이터 형식에 따라 자동으로 합니다. 이 작업을 수행 하려면 엔터티 형식에 해당 하는 partial 클래스를 만들어야 합니다.

**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **ContosoUniversity** 프로젝트를 선택 **참조 추가**에 대 한 참조를 추가 하 고 `System.ComponentModel.DataAnnotations`입니다.

[![Image11](the-entity-framework-and-aspnet-getting-started-part-8/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image11.png)

에 *DAL* 폴더에 새 클래스 파일을 만들고, 이름을 *Student.cs*에서 템플릿 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample6.cs)]

이 코드에서는 partial 클래스는 `Student` 엔터티. `MetadataType` 이 partial 클래스에 적용 된 특성 메타 데이터를 지정 하는 데 사용 하는 클래스를 식별 합니다. 메타 데이터 클래스 이름을 지정할 수 있지만 엔터티 이름과 "메타 데이터"를 사용 하는 경우가 잦다 합니다.

속성 메타 데이터 클래스에 적용 되는 특성 서식 지정, 유효성 검사, 규칙 및 오류 메시지를 지정 합니다. 여기에 표시 된 특성에는 다음과 같은 결과가 제공 됩니다.

- `EnrollmentDate` (시간)을 제외한 날짜가 표시 됩니다.
- 두 이름 필드에 25 자 여야 합니다. 또는 적게 길이 및 사용자 지정 오류 메시지를 제공 합니다.
- 두 이름 필드는 필요 하 고 사용자 지정 오류 메시지를 제공 됩니다.

실행 합니다 *Students.aspx* 다시 페이지를 표시, 날짜 시간 없이 표시 됩니다.

[![Image08](the-entity-framework-and-aspnet-getting-started-part-8/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image13.png)

행을 편집 하 고 이름 필드의 값을 선택 취소 해 보세요. 필드 오류를 나타내는 별표 표시를 클릭 하기 전에 필드를 두면 즉시 **업데이트**합니다. 클릭 하면 **업데이트**, 지정한 오류 메시지 텍스트를 페이지에 표시 됩니다.

[![Image10](the-entity-framework-and-aspnet-getting-started-part-8/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image15.png)

25 자 보다 긴 이름을 입력, 클릭 **업데이트**, 페이지 지정한 오류 메시지 텍스트를 표시 합니다.

[![Image09](the-entity-framework-and-aspnet-getting-started-part-8/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image17.png)

이제 데이터 모델 메타 데이터에서 이러한 서식 지정 및 유효성 검사 규칙을 설정한 규칙 적용 됨을 자동으로 표시 하거나 이러한 필드에 대 한 변경을 허용 하는 모든 페이지에서 사용 된다면 `DynamicControl` 또는 `DynamicField` 컨트롤입니다. 프로그래밍 및 테스트를 보다 쉽게 그러면를 작성 해야 하는 중복 코드의 양을 줄이고 데이터 서식 지정 및 유효성 검사는 응용 프로그램을 통해 일치 하는 것이 되도록 합니다.

## <a name="more-information"></a>추가 정보

이 자습서 시리즈의 Entity Framework를 사용 하 여 시작을 완료 했습니다. Entity Framework를 사용 하는 방법을 배울 수 있도록 더 많은 리소스를 계속 진행 [다음 Entity Framework 자습서 시리즈의 첫 번째 자습서](../continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md) 또는 다음 사이트를 방문 하십시오.

- [Entity Framework FAQ](http://www.ef-faq.org/introduction.html)
- [Entity Framework 팀 블로그](https://blogs.msdn.com/b/adonet/)
- [MSDN Library에서 entity Framework 사용](https://msdn.microsoft.com/library/bb399572.aspx)
- [MSDN 데이터 개발자 센터에서 entity Framework 사용](https://msdn.microsoft.com/data/ef.aspx)
- [MSDN 라이브러리의 EntityDataSource 웹 서버 컨트롤 개요](https://msdn.microsoft.com/library/cc488502.aspx)
- [EntityDataSource 컨트롤 MSDN 라이브러리의 API 참조](https://msdn.microsoft.com/library/system.web.ui.webcontrols.entitydatasource.aspx)
- [MSDN의 entity Framework 포럼](https://social.msdn.microsoft.com/forums/adodotnetentityframework/)
- [Julie Lerman의 블로그](http://thedatafarm.com/blog/)

> [!div class="step-by-step"]
> [이전](the-entity-framework-and-aspnet-getting-started-part-7.md)
