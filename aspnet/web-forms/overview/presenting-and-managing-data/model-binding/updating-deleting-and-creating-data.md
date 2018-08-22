---
uid: web-forms/overview/presenting-and-managing-data/model-binding/updating-deleting-and-creating-data
title: 업데이트, 삭제 및 데이터 모델 바인딩 및 web forms를 사용 하 여 만들기 | Microsoft Docs
author: tfitzmac
description: 이 자습서 시리즈에서는 모델 바인딩을 사용 하 여 ASP.NET Web Forms 프로젝트의 기본 사항을 보여 줍니다. 모델 바인딩을 통해 데이터 상호 작용 자세한 직선-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 602baa94-5a4f-46eb-a717-7a9e539c1db4
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/updating-deleting-and-creating-data
msc.type: authoredcontent
ms.openlocfilehash: a3e098d7b10ba6218ffa1818ccf8fc8df6912a9e
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41831537"
---
<a name="updating-deleting-and-creating-data-with-model-binding-and-web-forms"></a>업데이트, 삭제 및 데이터 모델 바인딩 및 web forms를 사용 하 여 만들기
====================
[Tom FitzMacken](https://github.com/tfitzmac)

> 이 자습서 시리즈에서는 모델 바인딩을 사용 하 여 ASP.NET Web Forms 프로젝트의 기본 사항을 보여 줍니다. 모델 바인딩 보다 직관적인 데이터 원본 개체 (예: ObjectDataSource 또는 SqlDataSource) 처리 하는 보다 데이터 상호 작용 하 게 합니다. 이 시리즈 소개 자료를 사용 하 여 시작 하 고 나중에 자습서에서 고급 개념을 이동 합니다.
> 
> 이 자습서에는 만들기, 업데이트 및 모델 바인딩을 사용 하 여 데이터를 삭제 하는 방법을 보여 줍니다. 다음 속성을 설정 합니다.
> 
> - DeleteMethod
> - InsertMethod
> - UpdateMethod
> 
> 이러한 속성에서 해당 작업을 처리 하는 메서드의 이름을 수신 합니다. 이 메서드 내에서 데이터 상호 작용 하기 위한 논리를 제공 합니다.
> 
> 첫 번째 범위에서 만든 프로젝트를 기반으로 한이 자습서 [파트](retrieving-data.md) 계열의 합니다.
> 
> 할 수 있습니다 [다운로드](https://go.microsoft.com/fwlink/?LinkId=286116) C# 또는 VB. 전체 프로젝트 다운로드 가능한 코드를 Visual Studio 2012 또는 Visual Studio 2013을 사용 하 여 작동합니다. 이 자습서에 표시 된 Visual Studio 2013 서식 파일 보다 약간 다른 Visual Studio 2012 템플릿을 사용 합니다.


## <a name="what-youll-build"></a>만들 내용

이 자습서에서는 다음을 수행 해야합니다.

1. 동적 데이터 템플릿을 추가합니다
2. 모델 바인딩 메서드를 통해 데이터 업데이트 및 삭제를 사용 하도록 설정
3. 데이터 유효성 검사 규칙을 적용-데이터베이스에 새 레코드를 만드는 사용

## <a name="add-dynamic-data-templates"></a>동적 데이터 템플릿을 추가합니다

최상의 사용자 환경을 제공 하 고 코드 반복을 최소화 하려면 동적 데이터 템플릿을 사용 합니다. NuGet 패키지를 설치 하 여 기존 사이트를 미리 작성된 된 동적 데이터 템플릿을 쉽게 통합할 수 있습니다.

**NuGet 패키지 관리**를 설치 합니다 **DynamicDataTemplatesCS**합니다.

![동적 데이터 템플릿](updating-deleting-and-creating-data/_static/image1.png)

프로젝트에 이제 라는 폴더에 통지 **DynamicData**합니다. 해당 폴더에 있는 웹 폼에서 동적 컨트롤에 자동으로 적용 되는 템플릿을 찾을 수 있습니다.

![동적 데이터 폴더](updating-deleting-and-creating-data/_static/image2.png)

## <a name="enable-updating-and-deleting"></a>설정 업데이트 및 삭제

사용자 데이터베이스에서 레코드를 업데이트 및 삭제를 사용 하는 것은 데이터를 검색 하기 위한 프로세스와 매우 유사 합니다. 에 **UpdateMethod** 하 고 **DeleteMethod** 속성을 해당 작업을 수행 하는 메서드의 이름을 지정 합니다. GridView 컨트롤을 사용 하 여 편집의 자동 생성을 지정 하 고 단추를 삭제 합니다. 다음 강조 표시 된 코드를 GridView 코드의 추가 기능을 보여 줍니다.

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample1.aspx?highlight=4-5)]

코드 숨김 파일에 추가 하 여 문을 **System.Data.Entity.Infrastructure**합니다.

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample2.cs)]

그런 다음 다음 업데이트를 추가 하 고 메서드를 삭제 합니다.

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample3.cs)]

합니다 **tryupdatemodel에 전달** 메서드 웹 폼에서 데이터 항목에 일치 하는 데이터 바인딩된 값을 적용 합니다. 데이터 항목의 id 매개 변수 값에 따라 검색 됩니다.

## <a name="enforce-validation-requirements"></a>유효성 검사 요구 사항을 적용 합니다.

FirstName, LastName 및 Year 속성 Student 클래스에 적용 하는 유효성 검사 특성은 데이터를 업데이트할 때 자동으로 적용 됩니다. DynamicField 컨트롤 유효성 검사 특성을 기반으로 하는 클라이언트 및 서버 유효성 검사기를 추가 합니다. FirstName 및 LastName 속성은 모두 필요 합니다. FirstName 길이가 20 자를 초과할 수 없습니다 및 LastName 40 자를 초과할 수 없습니다. 연도는 AcademicYear 열거형에 대 한 유효한 값 이어야 합니다.

사용자 유효성 검사 요구 사항의 위반 하면 업데이트가 진행 되지 않습니다. 오류 메시지를 보려면 위에서 GridView ValidationSummary 컨트롤을 추가 합니다. 모델 바인딩에서 유효성 검사 오류를 표시 하려면 설정 합니다 **ShowModelStateErrors** 속성으로 설정 **true**합니다. 

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample4.aspx)]

웹 응용 프로그램을 실행 하 고 업데이트 하 고 레코드를 삭제 합니다.

![업데이트 데이터](updating-deleting-and-creating-data/_static/image3.png)

편집 모드에서 Year 속성에 대 한 값을 자동으로 렌더링할 때 드롭다운 목록으로 표시 합니다. Year 속성은 열거 값을 하 고 열거형 값에 대 한 동적 데이터 템플릿을 편집할 수 있도록 목록 드롭다운을 지정 합니다. 열어 해당 템플릿을 찾을 수 있습니다는 **열거형\_Edit.ascx** 파일을 **DynamicData**/**FieldTemplates** 폴더입니다.

유효한 값을 제공 하는 경우 업데이트를 성공적으로 완료 합니다. 유효성 검사 요구 사항 중 하나를 위반 하면 업데이트가 진행 되지 않습니다 하 고 오류 메시지를 표 형태 위에 표시 됩니다.

![오류 메시지](updating-deleting-and-creating-data/_static/image4.png)

## <a name="add-new-records"></a>새 레코드를 추가 합니다.

GridView 컨트롤을 다루지 않습니다 합니다 **InsertMethod** 속성 모델 바인딩을 사용 하 여 새 레코드를 추가 하는 것에 대 한 사용할 수 없습니다. InsertMethod 속성을 찾을 수 있습니다 합니다 **FormView**를 **DetailsView**, 또는 **ListView** 컨트롤입니다. 이 자습서에서는 새 레코드를 추가 하려면 FormView 컨트롤을 사용 합니다.

첫째, 만든 새 레코드를 추가 하는 것에 대 한 새 페이지에 링크를 추가 합니다. ValidationSummary, 위에 추가 합니다.

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample5.aspx)]

학생 페이지에 대 한 콘텐츠의 맨 위에 있는 새 링크 표시 됩니다.

![새 링크](updating-deleting-and-creating-data/_static/image5.png)

그런 다음 마스터 페이지를 사용 하 여 새 web form을 추가 하 고 이름을 **AddStudent**합니다. 마스터 페이지와 Site.Master를 선택 합니다.

사용 하 여 새 학생을 추가 하기 위한 필드를 렌더링 합니다는 **DynamicEntity** 제어 합니다. DynamicEntity 컨트롤 ItemType 속성에 지정 된 클래스에는 편집 가능한 속성을 렌더링 합니다. StudentID 속성으로 표시 되어 있으므로 합니다 **[ScaffoldColumn(false)]** 특성 사용 하므로 렌더링 되지 않습니다. AddStudent 페이지의 MainContent 자리 표시자를 다음 코드를 추가 합니다.

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample6.aspx)]

코드 숨김 파일 (AddStudent.aspx.cs)에서 추가 **를 사용 하 여** 문을 합니다 **ContosoUniversityModelBinding.Models** 네임 스페이스입니다.

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample7.cs)]

새 레코드 및 취소 단추에 대 한 이벤트 처리기를 삽입 하는 방법을 지정 하려면 다음 메서드를 추가 합니다.

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample8.cs)]

모든 변경 내용을 저장 합니다.

웹 응용 프로그램을 실행 하 고 새 학생을 만듭니다.

![새 학생을 추가 합니다.](updating-deleting-and-creating-data/_static/image6.png)

클릭 **삽입** 새 학생을 만들었는지 확인 합니다.

![새 학생을 표시 합니다.](updating-deleting-and-creating-data/_static/image7.png)

## <a name="conclusion"></a>결론

이 자습서에서는 업데이트, 삭제 및 만드는 데이터를 사용 합니다. 하면 확인 데이터와 상호 작용할 때 유효성 검사 규칙이 적용 됩니다.

다음에 [자습서](sorting-paging-and-filtering-data.md) 이 시리즈에서는 정렬, 페이징 및 필터링 데이터를 사용 합니다.

> [!div class="step-by-step"]
> [이전](retrieving-data.md)
> [다음](sorting-paging-and-filtering-data.md)
