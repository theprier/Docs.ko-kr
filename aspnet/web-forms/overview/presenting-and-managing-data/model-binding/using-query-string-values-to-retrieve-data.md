---
uid: web-forms/overview/presenting-and-managing-data/model-binding/using-query-string-values-to-retrieve-data
title: 쿼리 문자열 값을 사용 하 여 모델 바인딩을 사용 하 여 데이터를 필터링 하 여 web forms | Microsoft Docs
author: tfitzmac
description: 이 자습서 시리즈에서는 모델 바인딩을 사용 하 여 ASP.NET Web Forms 프로젝트의 기본 사항을 보여 줍니다. 모델 바인딩을 통해 데이터 상호 작용 자세한 직선-...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/27/2014
ms.topic: article
ms.assetid: b90978bd-795d-4871-9ade-1671caff5730
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/using-query-string-values-to-retrieve-data
msc.type: authoredcontent
ms.openlocfilehash: 495489479ef912afcb89c267b56fb11e07f959ec
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37374732"
---
<a name="using-query-string-values-to-filter-data-with-model-binding-and-web-forms"></a>모델 바인딩 및 web forms를 사용 하 여 데이터를 필터링 하는 쿼리 문자열 값을 사용 하 여
====================
[Tom FitzMacken](https://github.com/tfitzmac)

> 이 자습서 시리즈에서는 모델 바인딩을 사용 하 여 ASP.NET Web Forms 프로젝트의 기본 사항을 보여 줍니다. 모델 바인딩 보다 직관적인 데이터 원본 개체 (예: ObjectDataSource 또는 SqlDataSource) 처리 하는 보다 데이터 상호 작용 하 게 합니다. 이 시리즈 소개 자료를 사용 하 여 시작 하 고 나중에 자습서에서 고급 개념을 이동 합니다.
> 
> 이 자습서에서는 쿼리 문자열의 값을 전달 하 고 해당 값을 사용 하 여 모델 바인딩을 통해 데이터를 검색 하는 방법을 보여 줍니다.
> 
> 이 자습서에서 만든 프로젝트를 기반 합니다 [이전](retrieving-data.md) 시리즈의 파트입니다.
> 
> 할 수 있습니다 [다운로드](https://go.microsoft.com/fwlink/?LinkId=286116) C# 또는 VB. 전체 프로젝트 다운로드 가능한 코드를 Visual Studio 2012 또는 Visual Studio 2013을 사용 하 여 작동합니다. 이 자습서에 표시 된 Visual Studio 2013 서식 파일 보다 약간 다른 Visual Studio 2012 템플릿을 사용 합니다.


## <a name="what-youll-build"></a>만들 내용

이 자습서에서는 다음을 수행 해야합니다.

1. 학생에 대 한 등록된 과정을 표시할 새 페이지 추가
2. 쿼리 문자열의 값을 기준으로 선택한 학생에 대 한 등록된 과정 검색
3. 새 페이지를 그리드 보기에서 쿼리 문자열 값을 사용 하 여 하이퍼링크 추가

이 자습서의 단계를 수행한 매우 비슷합니다 이전 [자습서](sorting-paging-and-filtering-data.md) 드롭다운 목록에서에서 사용자 선택에 따라 표시 된 학생을 필터링 합니다. 해당 자습서를 사용 하는 **제어** 특성 선택 메서드에서 매개 변수 값을 컨트롤에서 제공 됨을 지정 합니다. 이 자습서에서는 사용 합니다 **QueryString** select 메서드 매개 변수 값은 쿼리 문자열에서 제공 됨을 지정 하려면 특성입니다.

## <a name="add-new-page-for-displaying-a-students-courses"></a>학생의 코스를 표시 하기 위한 새 페이지 추가

Site.master 마스터 페이지를 사용 하는 새 web form을 추가 하 고 페이지의 이름을 **코스**합니다.

에 **Courses.aspx** 파일, 선택한 학생에 대 한 강좌를 표시 하는 그리드 보기를 추가 합니다.

[!code-aspx[Main](using-query-string-values-to-retrieve-data/samples/sample1.aspx)]

## <a name="define-the-select-method"></a>Select 메서드를 정의 합니다.

**Courses.aspx.cs**, 그리드 보기에서 지정한 이름 가진 select 메서드를 추가 합니다 **SelectMethod** 속성입니다. 메서드는 학생의 코스를 검색 하는 것에 대 한 쿼리를 정의 하 고 매개 변수 이름이 같은 매개 변수를 사용 하 여 쿼리 문자열 값에서 제공 됨을 지정 합니다.

먼저 다음을 추가 해야 합니다 **를 사용 하 여** 문입니다.

[!code-csharp[Main](using-query-string-values-to-retrieve-data/samples/sample2.cs)]

그런 다음 Courses.aspx.cs에 다음 코드를 추가 합니다.

[!code-csharp[Main](using-query-string-values-to-retrieve-data/samples/sample3.cs)]

QueryString 특성 StudentID 라는 쿼리 문자열 값을이 메서드의 매개 변수를 자동으로 할당 됩니다 것을 의미 합니다.

## <a name="add-hyperlink-with-query-string-value"></a>쿼리 문자열 값을 사용 하 여 하이퍼링크를 추가 합니다.

Students.aspx에서 표 뷰에서 새 강좌 페이지에 링크 되는 하이퍼링크 필드를 추가 합니다. 하이퍼링크는 학생의 id 사용 하 여 쿼리 문자열 값을 포함 됩니다.

Students.aspx에서 다음 필드를 총 크레딧 눈금 보기 열 필드 바로 아래에 추가 합니다.

[!code-aspx[Main](using-query-string-values-to-retrieve-data/samples/sample4.aspx?highlight=7-8)]

응용 프로그램을 실행 및 그리드 보기에 이제 과정 링크를 포함 합니다.

![하이퍼링크 추가](using-query-string-values-to-retrieve-data/_static/image1.png)

링크 중 하나를 클릭 하면 등록 된 해당 학생의 코스 표시 됩니다.

![강좌를 표시 합니다.](using-query-string-values-to-retrieve-data/_static/image2.png)

## <a name="conclusion"></a>결론

이 자습서에서는 쿼리 문자열 값을 사용 하 여 링크를 추가 합니다. Select 메서드 매개 변수 값에 대 한 쿼리 문자열 값을 사용 했습니다.

다음에 [자습서](adding-business-logic-layer.md), 비즈니스 논리 계층 및 데이터 액세스 계층을 코드 숨김 파일에서 코드를 이동 합니다.

> [!div class="step-by-step"]
> [이전](integrating-jquery-ui.md)
> [다음](adding-business-logic-layer.md)
