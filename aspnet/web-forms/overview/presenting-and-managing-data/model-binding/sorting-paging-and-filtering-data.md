---
uid: web-forms/overview/presenting-and-managing-data/model-binding/sorting-paging-and-filtering-data
title: 정렬, 페이징 및 모델 바인딩 및 web forms를 사용 하 여 데이터 필터링 | Microsoft Docs
author: tfitzmac
description: 이 자습서 시리즈에서는 모델 바인딩을 사용 하 여 ASP.NET Web Forms 프로젝트의 기본 사항을 보여 줍니다. 모델 바인딩을 통해 데이터 상호 작용 자세한 직선-...
ms.author: aspnetcontent
ms.date: 02/27/2014
ms.assetid: 266e7866-e327-4687-b29d-627a0925e87d
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/sorting-paging-and-filtering-data
msc.type: authoredcontent
ms.openlocfilehash: ded398bcbbb8d7d9e5c882a598bf9d6faa6ea81e
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37833878"
---
<a name="sorting-paging-and-filtering-data-with-model-binding-and-web-forms"></a>정렬, 페이징 및 모델 바인딩 및 web forms를 사용 하 여 데이터를 필터링 합니다.
====================
[Tom FitzMacken](https://github.com/tfitzmac)

> 이 자습서 시리즈에서는 모델 바인딩을 사용 하 여 ASP.NET Web Forms 프로젝트의 기본 사항을 보여 줍니다. 모델 바인딩 보다 직관적인 데이터 원본 개체 (예: ObjectDataSource 또는 SqlDataSource) 처리 하는 보다 데이터 상호 작용 하 게 합니다. 이 시리즈 소개 자료를 사용 하 여 시작 하 고 나중에 자습서에서 고급 개념을 이동 합니다.
> 
> 이 자습서에서는 정렬, 페이징 및 모델 바인딩을 통해 데이터를 필터링을 추가 하는 방법을 보여줍니다.
> 
> 첫 번째 범위에서 만든 프로젝트를 기반으로 한이 자습서 [파트](retrieving-data.md) 계열의 합니다.
> 
> 할 수 있습니다 [다운로드](https://go.microsoft.com/fwlink/?LinkId=286116) C# 또는 VB. 전체 프로젝트 다운로드 가능한 코드를 Visual Studio 2012 또는 Visual Studio 2013을 사용 하 여 작동합니다. 이 자습서에 표시 된 Visual Studio 2013 서식 파일 보다 약간 다른 Visual Studio 2012 템플릿을 사용 합니다.


## <a name="what-youll-build"></a>만들 내용

이 자습서에서는 다음을 수행 해야합니다.

1. 정렬 및 데이터의 페이징 사용
2. 사용자가 선택에 따라 데이터 필터링을 사용 하도록 설정

## <a name="add-sorting"></a>정렬 추가

GridView에서 정렬 사용 하지 않는 것이 쉽습니다. Student.aspx 파일에서 설정 하기만 하면 됩니다 **AllowSorting** 하 **true** gridview에서입니다. 설정할 필요가 없습니다를 **SortExpression** DataField를 자동으로 사용 되는 각 열에 대 한 값입니다. GridView에는 선택한 값에서 데이터를 지정 하는 순서를 포함 하도록 쿼리를 수정 합니다. 아래 강조 표시 된 코드를 정렬 하기 위해 해야 할 추가 보여줍니다.

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample1.aspx?highlight=5)]

웹 응용 프로그램을 실행 하 고 다른 열 값을 기준으로 정렬 학생 레코드를 테스트 합니다.

![정렬 학생](sorting-paging-and-filtering-data/_static/image2.png)

## <a name="add-paging"></a>페이징 추가

페이징을 사용 하도록 설정도 매우 쉽습니다. GridView 설정 합니다 **AllowPaging** 속성을 **true** 설정 및를 **PageSize** 속성을 각 페이지에 표시 하려는 레코드의 수입니다. 이 자습서에서는 4로 설정할 수 있습니다.

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample2.aspx?highlight=5)]

웹 응용 프로그램을 실행 하 고 레코드를 단일 페이지에 표시 된 4 개 이하의 레코드를 사용 하 여 여러 페이지에 걸쳐 나뉩니다 이제 알 수 있습니다.

![페이징 추가](sorting-paging-and-filtering-data/_static/image4.png)

지연 된 쿼리 실행에는 응용 프로그램 효율성이 향상 됩니다. 전체 데이터 집합을 검색 하는 대신 GridView에는 현재 페이지에 대 한 레코드만 검색 하도록 쿼리를 수정 합니다.

## <a name="filter-records-by-user-selection"></a>사용자 선택 하 여 레코드 필터링

모델 바인딩을 사용 하면 모델 바인딩 메서드에서 매개 변수의 값을 설정 하는 방법을 지정 하는 몇 가지 특성을 추가 합니다. 이러한 특성은는 **System.Web.ModelBinding** 네임 스페이스입니다. 다음과 같은 변경 내용이 해당됩니다.

- Control
- 쿠키
- Form
- 프로필
- QueryString
- RouteData
- 세션
- UserProfile
- ViewState

이 자습서에서는 GridView에 표시 되는 레코드를 필터링 할 컨트롤의 값을 사용 합니다. 추가 된 **컨트롤** 특성을 이전에 만든 쿼리 메서드에 합니다. 에 [나중](using-query-string-values-to-retrieve-data.md) 자습서에서는 적용할를 **QueryString** 특성을 매개 변수 값은 쿼리 문자열 값에서 제공 됨을 지정 하는 매개 합니다.

먼저 ValidationSummary, 위에 학생에 게 표시 되는 필터링에 대 한 목록 드롭다운을 추가 합니다.

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample3.aspx?highlight=3-11)]

코드 숨김 파일에서 값을 받도록 컨트롤에서 선택 메서드를 수정 하 고 매개 변수의 이름 값을 제공 하는 컨트롤의 이름으로 설정 합니다.

추가 해야 합니다는 **를 사용 하 여** 문을 합니다 **System.Web.ModelBinding** 컨트롤 특성을 확인할 네임 스페이스입니다.

[!code-csharp[Main](sorting-paging-and-filtering-data/samples/sample4.cs)]

다음 코드는 드롭다운 목록 값에 따라 반환 된 데이터를 필터링 하기 위해 노력 다시 select 메서드를 보여줍니다. 매개 변수 이름이 같은 컨트롤에서이 매개 변수에 대 한 값을 가져오도록 지정 하기 전에 컨트롤 특성을 추가 합니다.

[!code-csharp[Main](sorting-paging-and-filtering-data/samples/sample5.cs)]

웹 응용 프로그램을 실행 하 고 드롭다운 학생의 목록을 필터링 하려면 목록에서에서 다른 값을 선택 합니다.

![필터 학생](sorting-paging-and-filtering-data/_static/image6.png)

## <a name="conclusion"></a>결론

이 자습서에서는 정렬 및 데이터의 페이징을 사용 합니다. 설정한 컨트롤의 값으로 데이터를 필터링 합니다.

다음에 [자습서](integrating-jquery-ui.md) 동적 데이터 템플릿에 JQuery UI 위젯을 통합 하 여 UI를 향상 됩니다.

> [!div class="step-by-step"]
> [이전](updating-deleting-and-creating-data.md)
> [다음](integrating-jquery-ui.md)
