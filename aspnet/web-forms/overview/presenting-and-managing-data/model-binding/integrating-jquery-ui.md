---
uid: web-forms/overview/presenting-and-managing-data/model-binding/integrating-jquery-ui
title: "모델 바인딩 및 web forms JQuery UI Datepicker 통합 | Microsoft Docs"
author: tfitzmac
description: "이 자습서 시리즈 모델 바인딩을 사용 하 여 ASP.NET Web Forms 프로젝트의 기본 사항을 보여 줍니다. 모델 바인딩 데이터 상호 작용 하 게 더 많은 직선-중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/27/2014
ms.topic: article
ms.assetid: 3cbab37b-fb0f-4751-9ec4-74e068c3f380
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/integrating-jquery-ui
msc.type: authoredcontent
ms.openlocfilehash: da3c8f347a709a4c9a47fd0ecce5201d9b0cd1b1
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="integrating-jquery-ui-datepicker-with-model-binding-and-web-forms"></a>모델 바인딩 및 web forms JQuery UI Datepicker 통합
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 자습서 시리즈 모델 바인딩을 사용 하 여 ASP.NET Web Forms 프로젝트의 기본 사항을 보여 줍니다. 모델 바인딩 데이터 원본 개체 (예: ObjectDataSource 또는 SqlDataSource) 처리 하는 보다 간단한 것 보다 데이터 상호 작용 하 게 합니다. 이 시리즈 소개 자료로 시작 하 고 이후의 자습서의 보다 발전된 된 개념 이동 합니다.
> 
> JQuery UI를 추가 하는 방법을 보여 주는이 자습서 [Datepicker 위젯](http://jqueryui.com/datepicker/) Web Form 및 선택한 값으로 데이터베이스를 업데이트 하려면 바인딩 모델을 사용 합니다.
> 
> 이 자습서에서 만든 프로젝트에 빌드는 [첫 번째](retrieving-data.md) 및 [두 번째](updating-deleting-and-creating-data.md) 시리즈의 일부입니다.
> 
> 있습니다 수 [다운로드](https://go.microsoft.com/fwlink/?LinkId=286116) C# 또는 VB. 전체 프로젝트 다운로드 가능한 코드는 Visual Studio 2012 또는 Visual Studio 2013과 함께 작동합니다. 이 자습서에 표시 된 Visual Studio 2013 서식 파일 보다 약간 차이가 있는 Visual Studio 2012 템플릿을 사용 합니다.


## <a name="what-youll-build"></a>만들 것인지

이 자습서에서는 다음을 수행합니다.

1. 학생의 등록 날짜를 기록 하 여 모델에 속성 추가
2. 사용자는 JQuery UI Datepicker 위젯을 사용 하 여 등록 날짜를 선택할 수 있도록
3. 등록 날짜에 대 한 유효성 검사 규칙을 적용 합니다.

JQuery UI Datepicker 위젯을 사용 하면 쉽게 필드와 상호 작용할 때 팝업으로 나타나는 달력에서 날짜를 선택할 수 있습니다. 이 도구를 사용 하는 보다 편리 하 게 사용자에 대 한 날짜를 수동으로 입력 수 있습니다. 데이터 작업에 대 한 모델 바인딩을 사용 하는 페이지에 Datepicker 위젯 통합 적은 양의 추가 작업이 필요 합니다.

## <a name="add-a-new-property-to-the-model"></a>모델에 새 속성 추가

먼저, 추가 됩니다 한 **Datetime** 속성 프로그램 학생을 모델 및 해당 변경 내용을 데이터베이스에 마이그레이션할 합니다. 열기 **UniversityModels.cs**, 및 학생 모델에 강조 표시 된 코드를 추가 합니다.

[!code-csharp[Main](integrating-jquery-ui/samples/sample1.cs?highlight=16-18)]

**RangeAttribute** 속성에 대 한 유효성 검사 규칙을 적용 하기 위해 포함 되었습니다. 이 자습서에서는 Contoso 대학 2013 년 1 월 1 일에 설립 및 이전 등록 날짜 유효 하지 않습니다 가정 합니다.

패키지 관리 창에서 명령을 실행 하 여 마이그레이션을 추가 **추가 마이그레이션 AddEnrollmentDate**합니다. 마이그레이션 코드에 새 Datetime 열 학생 테이블에 추가 확인 합니다. RangeAttribute에 지정 된 값과 일치 하려면 아래의 강조 표시 된 코드에 표시 된 대로 새 열에 대 한 기본값을를 추가 합니다.

[!code-csharp[Main](integrating-jquery-ui/samples/sample2.cs?highlight=11)]

마이그레이션 파일에 변경 내용을 저장 합니다.

데이터 다시 초기값으로 사용할 필요가 없습니다. 따라서 열고 **Configuration.cs** Migrations 폴더에서 제거 하거나 코드에서 주석으로 처리는 **시드** 메서드. 파일을 저장한 후 닫습니다.

이제 명령 실행 **데이터베이스 업데이트**합니다. 열이 데이터베이스에 있으면 EnrollmentDate에 대 한 기본값을 가집니다 기존 레코드를 모두 확인 합니다.

## <a name="add-dynamic-controls-for-enrollment-date"></a>등록 날짜에 대 한 동적 컨트롤을 추가 합니다.

이제을 표시 하 고 등록 날짜 편집 컨트롤을 추가 합니다. 이 시점에서 텍스트 상자를 통해 값 편집 합니다. 자습서의 뒷부분에 나오는 텍스트 상자는 JQuery Datepicker 위젯에 변경 합니다.

변경할 필요가 없습니다 점에 주의 해야 하는 첫째, 고 **AddStudent.aspx** 파일입니다. DynamicEntity 컨트롤 새 속성을 자동으로 렌더링 됩니다.

열기 **Students.aspx**, 다음 강조 표시 된 코드를 추가 합니다.

[!code-aspx[Main](integrating-jquery-ui/samples/sample3.aspx?highlight=13)]

응용 프로그램을 실행 하 고 날짜를 입력 하 여 등록 날짜 값을 설정할 수 있습니다. 새 학생 추가 하는 경우:

![날짜 설정된](integrating-jquery-ui/_static/image1.png)

또는 기존 값을 편집 합니다.

![날짜 편집](integrating-jquery-ui/_static/image2.png)

입력 날짜 작동 하지만 사용자 환경을 제공 하려면 아닐 수 있습니다. 다음 섹션에서 일정을 통해 날짜를 선택 하면 있습니다.

## <a name="install-nuget-package-to-work-with-jquery-ui"></a>JQuery UI를 작성 하려면 NuGet 패키지 설치

**쥬 UI** NuGet 패키지에는 웹 응용 프로그램에 JQuery UI 도구가 쉽게 통합할 수 있습니다. 이 패키지를 사용 하려면 NuGet을 통해 설치 합니다.

![쥬 UI 추가](integrating-jquery-ui/_static/image3.png)

설치 하는 쥬 UI 버전 응용 프로그램에서 버전의 JQuery와 충돌할 수 있습니다. 이 자습서와 함께 계속 하기 전에 응용 프로그램을 실행 하십시오. JavaScript 오류가 발생 하는 경우에 JQuery 버전을 조정 해야 합니다. 필요한 버전의 JQuery 스크립트 폴더 (버전 1.8.2 작성이 자습서의 시)에 추가 하거나 Site.master에서 JQuery 파일의 경로를 지정할 수 있습니다.

[!code-aspx[Main](integrating-jquery-ui/samples/sample4.aspx)]

## <a name="customize-datetime-template-to-include-datepicker-widget"></a>Datepicker 위젯 포함 하도록 DateTime 템플릿을 사용자 지정

날짜/시간 값을 편집 하기 위한 동적 데이터 서식 파일에 Datepicker 위젯을 추가 합니다. 서식 파일에 위젯을 추가 하 여 새 학생을 추가 하기 위한 형식 및 편집 하는 학습자는 표 뷰에서 자동으로 렌더링지 않습니다. 열기 **DateTime\_Edit.ascx**, 다음 강조 표시 된 코드를 추가 합니다.

[!code-aspx[Main](integrating-jquery-ui/samples/sample5.aspx?highlight=3)]

코드 숨김 파일에는 DatePicker에 대 한 최소 및 최대 날짜를 설정 합니다. 이러한 값을 설정 하 여 잘못 된 날짜를 이동할 수 없도록 사용자를 못합니다. 최소 및 최대 값을 검색 합니다는 **RangeAttribute** 제공 된 경우에 날짜/시간 속성에 있습니다. 열기 **DateTime\_Edit.ascx.cs**, 다음 강조 표시 된 코드 페이지를 추가 하 고\_메서드를 로드 합니다.

[!code-csharp[Main](integrating-jquery-ui/samples/sample6.cs?highlight=9-14)]

웹 응용 프로그램을 실행 하 고 AddStudent 페이지로 이동 합니다. 필드에 대 한 값을 제공 하 고 등록 날짜에 대 한 텍스트 상자에서 클릭할 때 일정이 표시 됩니다.

![날짜 선택](integrating-jquery-ui/_static/image4.png)

날짜를 선택 하 고 클릭 **삽입**합니다. RangeAttribute 서버에서 유효성 검사를 적용합니다. 에 Datepicker minDate 속성을 설정 하 여도 클라이언트에서 유효성 검사를 적용 합니다. 달력은 minDate 값 이전 날짜로로 이동 하는 사용자를 수는 없습니다.

그리드 보기에서 레코드를 편집 하면 달력도 표시 됩니다.

![GridView에서 Datepicker](integrating-jquery-ui/_static/image5.png)

## <a name="conclusion"></a>결론

이 자습서에서는 JQuery 위젯 모델 바인딩을 사용 하는 웹 폼에 통합 하는 방법을 배웠습니다.

다음에서 [자습서](using-query-string-values-to-retrieve-data.md), 데이터를 선택할 때 쿼리 문자열 값을 사용 합니다.

>[!div class="step-by-step"]
[이전](sorting-paging-and-filtering-data.md)
[다음](using-query-string-values-to-retrieve-data.md)
