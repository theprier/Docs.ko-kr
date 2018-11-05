---
uid: web-forms/overview/presenting-and-managing-data/model-binding/integrating-jquery-ui
title: 모델 바인딩 및 web forms를 사용 하 여 JQuery UI Datepicker 통합 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서 시리즈에서는 모델 바인딩을 사용 하 여 ASP.NET Web Forms 프로젝트의 기본 사항을 보여 줍니다. 모델 바인딩을 통해 데이터 상호 작용 자세한 직선-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 3cbab37b-fb0f-4751-9ec4-74e068c3f380
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/integrating-jquery-ui
msc.type: authoredcontent
ms.openlocfilehash: ff1b17295c58d40d55bdcd4346b83121b579bb4c
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51020561"
---
<a name="integrating-jquery-ui-datepicker-with-model-binding-and-web-forms"></a>모델 바인딩 및 web forms를 사용 하 여 JQuery UI Datepicker 통합
====================
[Tom FitzMacken](https://github.com/tfitzmac)

> 이 자습서 시리즈에서는 모델 바인딩을 사용 하 여 ASP.NET Web Forms 프로젝트의 기본 사항을 보여 줍니다. 모델 바인딩 보다 직관적인 데이터 원본 개체 (예: ObjectDataSource 또는 SqlDataSource) 처리 하는 보다 데이터 상호 작용 하 게 합니다. 이 시리즈 소개 자료를 사용 하 여 시작 하 고 나중에 자습서에서 고급 개념을 이동 합니다.
> 
> 이 자습서에서는 JQuery UI를 추가 하는 방법을 보여 줍니다 [Datepicker 위젯](http://jqueryui.com/datepicker/) Web Form을 사용 하 여 모델을 선택한 값을 사용 하 여 데이터베이스를 업데이트 합니다.
> 
> 이 자습서에서 만든 프로젝트를 기반 합니다 [첫 번째](retrieving-data.md) 하 고 [두 번째](updating-deleting-and-creating-data.md) 시리즈의 파트입니다.
> 
> 할 수 있습니다 [다운로드](https://go.microsoft.com/fwlink/?LinkId=286116) C# 또는 VB. 전체 프로젝트 다운로드 가능한 코드를 Visual Studio 2012 또는 Visual Studio 2013을 사용 하 여 작동합니다. 이 자습서에 표시 된 Visual Studio 2013 서식 파일 보다 약간 다른 Visual Studio 2012 템플릿을 사용 합니다.


## <a name="what-youll-build"></a>만들 내용

이 자습서에서는 다음을 수행 해야합니다.

1. 학생 등록 날짜를 기록 하기 위해 모델에 속성 추가
2. JQuery UI Datepicker 위젯을 사용 하 여 등록 날짜를 선택 하려면 사용자를 사용 하도록 설정
3. 등록 날짜에 대 한 유효성 검사 규칙을 적용 합니다.

JQuery UI Datepicker 위젯을 사용 하면 쉽게 필드와 상호 작용할 때 표시 되는 달력에서 날짜를 선택할 수 있습니다. 이 위젯을 사용 하 여 수동으로 날짜를 입력 하는 보다 사용자에 대 한 더 편리할 수 있습니다. 데이터 작업에 대 한 모델 바인딩을 사용 하는 페이지 Datepicker 위젯 통합 적은 양의 추가 작업이 필요 합니다.

## <a name="add-a-new-property-to-the-model"></a>모델에 새 속성 추가

먼저 추가 합니다는 **날짜/시간** 속성에 학생을 모델링 하 고 해당 변경 내용을 데이터베이스에 마이그레이션. 오픈 **UniversityModels.cs**, 학생 모델을 강조 표시 된 코드를 추가 합니다.

[!code-csharp[Main](integrating-jquery-ui/samples/sample1.cs?highlight=16-18)]

합니다 **RangeAttribute** 속성에 대 한 유효성 검사 규칙을 적용 하기 위해 포함 되었습니다. 이 자습서에서는 Contoso University는 2013 년 1 월 1 일 년에 설립 된 이전 등록 날짜가 유효 하지 않습니다 고 가정 됩니다.

패키지 관리 창에서 명령을 실행 하 여 마이그레이션을 추가 **추가 마이그레이션 AddEnrollmentDate**합니다. 마이그레이션 코드 Student 테이블에 새 날짜/시간 열을 추가 하는 것을 확인 합니다. RangeAttribute에서 지정 된 값에 맞게, 아래 강조 표시 된 코드에 표시 된 대로 새 열에 대 한 기본값을 추가 합니다.

[!code-csharp[Main](integrating-jquery-ui/samples/sample2.cs?highlight=11)]

마이그레이션 파일에 변경 내용을 저장 합니다.

데이터를 다시 시드할 필요가 없습니다. 따라서 엽니다 **Configuration.cs** 마이그레이션 폴더에 제거 하거나에서 코드를 주석 처리 합니다 **초기값** 메서드. 파일을 저장한 후 닫습니다.

이제 명령을 **데이터베이스 업데이트**합니다. 이제 데이터베이스 열에 있는 EnrollmentDate에 대 한 기본값을 갖는 모든 기존 레코드에 유의 하십시오.

## <a name="add-dynamic-controls-for-enrollment-date"></a>등록 날짜에 대 한 동적 컨트롤을 추가 합니다.

이제 표시 하 고 등록 날짜 편집에 대 한 컨트롤을 추가 합니다. 이 시점에서 텍스트 상자를 통해 값을 편집 합니다. 자습서의 뒷부분에 나오는 JQuery Datepicker 위젯에 입력란을 바뀝니다.

먼저 것이를 변경할 필요가 없습니다 명심 해야 합니다 **AddStudent.aspx** 파일. DynamicEntity 컨트롤 새 속성을 자동으로 렌더링 됩니다.

오픈 **Students.aspx**를 다음 강조 표시 된 코드를 추가 합니다.

[!code-aspx[Main](integrating-jquery-ui/samples/sample3.aspx?highlight=13)]

응용 프로그램을 실행 하 고 날짜를 입력 하 여 등록 날짜의 값을 설정할 수 있는지 확인 합니다. 새 학생을 추가 하는 경우:

![설정된 된 날짜](integrating-jquery-ui/_static/image1.png)

또는 기존 값을 편집 합니다.

![날짜 편집](integrating-jquery-ui/_static/image2.png)

입력 날짜 작동 하지만 고객 환경을 제공 하려는 되지 않을 수 있습니다. 다음 섹션에서는 달력을 통해 날짜를 선택 하면 합니다.

## <a name="install-nuget-package-to-work-with-jquery-ui"></a>JQuery UI를 사용 하려면 NuGet 패키지 설치

합니다 **쥬 스 잔 UI** NuGet 패키지에는 웹 응용 프로그램에 JQuery UI 위젯 쉽게 통합할 수 있습니다. 이 패키지를 사용 하려면 NuGet을 통해 설치 합니다.

![쥬 스 잔 UI 추가](integrating-jquery-ui/_static/image3.png)

버전을 설치 하는 쥬 스 잔 UI 응용 프로그램에서 JQuery 버전이 충돌할 수 있습니다. 이 자습서를 진행 하기 전에 응용 프로그램을 실행 해 보십시오. JavaScript 오류가 발생 하는 경우에 JQuery 버전을 조정 해야 합니다. JQuery의 예상된 버전 (버전 1.8.2이이 자습서를 작성 시), 스크립트 폴더에 추가 하거나 Site.master에서 JQuery 파일의 경로를 지정할 수 있습니다.

[!code-aspx[Main](integrating-jquery-ui/samples/sample4.aspx)]

## <a name="customize-datetime-template-to-include-datepicker-widget"></a>Datepicker 위젯을 포함할 DateTime 템플릿을 사용자 지정

날짜/시간 값을 편집 하는 것에 대 한 동적 데이터 템플릿과 Datepicker 위젯을 추가 합니다. 위젯 템플릿에 추가 하 여 두 폼에 새 학생을 추가 및 편집 학생용 그리드 보기에서 자동으로 렌더링 됩니다. 오픈 **날짜/시간\_Edit.ascx**를 다음 강조 표시 된 코드를 추가 합니다.

[!code-aspx[Main](integrating-jquery-ui/samples/sample5.aspx?highlight=3)]

코드 숨김 파일에서 DatePicker에 대 한 최소 및 최대 날짜를 설정 합니다. 이러한 값을 설정 하 여 잘못 된 날짜를 이동할 수 없도록 사용자를 못합니다. 최소 및 최대 값을 검색 합니다는 **RangeAttribute** 제공 되는 경우 날짜/시간 속성에 있습니다. 오픈 **날짜/시간\_Edit.ascx.cs**, 다음 강조 표시 된 코드 페이지를 추가 하 고\_메서드를 로드 합니다.

[!code-csharp[Main](integrating-jquery-ui/samples/sample6.cs?highlight=9-14)]

웹 응용 프로그램을 실행 하 고 AddStudent 페이지로 이동 합니다. 필드에 대 한 값을 제공 하 고 등록 날짜에 대 한 텍스트 상자에서 클릭 하면 달력이 표시 됩니다.

![날짜 선택](integrating-jquery-ui/_static/image4.png)

날짜를 선택 하 고 클릭 **삽입**합니다. RangeAttribute 서버의 유효성 검사를 실행 합니다. Datepicker에 minDate 속성을 설정 하 여도 클라이언트에서 유효성 검사를 적용 합니다. 달력 사용자 minDate 변수의 이전 날짜를 이동할 수 없습니다.

그리드 보기에서 레코드를 편집할 때 달력도 표시 됩니다.

![GridView의 Datepicker](integrating-jquery-ui/_static/image5.png)

## <a name="conclusion"></a>결론

이 자습서에서는 JQuery 위젯 모델 바인딩을 사용 하는 web form을 통합 하는 방법을 알아보았습니다.

다음에 [자습서](using-query-string-values-to-retrieve-data.md), 데이터를 선택할 때 쿼리 문자열 값을 사용 합니다.

> [!div class="step-by-step"]
> [이전](sorting-paging-and-filtering-data.md)
> [다음](using-query-string-values-to-retrieve-data.md)
