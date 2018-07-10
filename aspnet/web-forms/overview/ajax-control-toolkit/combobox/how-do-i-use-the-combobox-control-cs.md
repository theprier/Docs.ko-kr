---
uid: web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-cs
title: ComboBox 컨트롤을 사용 하는 방법 (C#) | Microsoft Docs
author: microsoft
description: 콤보 상자에 사용자가 선택할 수 있는 옵션의 목록을 사용 하 여 텍스트의 유연성을 결합 하는 ASP.NET AJAX 컨트롤입니다.
ms.author: aspnetcontent
ms.date: 05/12/2009
ms.assetid: 0bbf4134-04df-4226-8930-d5bb99e27128
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 07da594647c9b43bd31644aa8c7fedb256a12916
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37839283"
---
<a name="how-do-i-use-the-combobox-control-c"></a>ComboBox 컨트롤을 사용 하는 방법 (C#)
====================
[Microsoft](https://github.com/microsoft)

> 콤보 상자에 사용자가 선택할 수 있는 옵션의 목록을 사용 하 여 텍스트의 유연성을 결합 하는 ASP.NET AJAX 컨트롤입니다.


이 자습서의 목표는 AJAX Control Toolkit ComboBox 컨트롤을 설명 합니다. ComboBox는 표준 ASP.NET DropDownList 컨트롤과 TextBox 컨트롤 간의 조합 처럼 작동합니다. 기존 항목 목록에서 선택 하거나 새 항목을 입력 합니다.

콤보 상자 자동 완성 컨트롤 extender 유사 하지만 컨트롤은 다양 한 시나리오에서 사용 됩니다. AutoComplete extender를 가져오도록 웹 서비스에 일치 하는 항목을 쿼리 합니다. 반면, 콤보 상자 컨트롤을 항목 집합을 사용 하 여 초기화 됩니다. AutoComplete extender는 사용 하 여 콤보 상자 컨트롤을 사용 하는 동안 다양 한 데이터 (자동차 부품의 수백만 개)를 사용 하 여 작업할 경우 적합 한 데이터의 작은 집합으로 작업 (자동차 부품의 수십 개).

## <a name="selecting-from-a-static-list-of-items"></a>항목의 정적 목록에서 선택

ComboBox 컨트롤을 사용 하는 간단한 예제 시작 s 수 있습니다. 드롭다운 목록에서 항목 목록을 정적 표시 한다고 가정해 보겠습니다. 그러나 목록이 완성 되는 가능성 열어 하려고 합니다. 사용자 목록에 사용자 지정 값 입력을 허용 하려면.

에서는 ll 새 ASP.NET Web Forms 페이지를 만들고 페이지에서 ComboBox 컨트롤을 사용 합니다. 프로젝트에 새 ASP.NET 페이지를 추가 하 고 디자인 뷰로 전환 합니다.

페이지의 콤보 상자 컨트롤을 사용 하려는 경우 페이지에 ScriptManager 컨트롤을 추가 해야 합니다. AJAX 확장명 탭 아래 ScriptManager 컨트롤을 디자이너 화면으로 끕니다. 페이지의 맨 위에 있는 ScriptManager 컨트롤을 추가 해야 즉시 열기 서버 쪽 아래에 추가할 수 있습니다 &lt;폼&gt; 태그입니다.

그런 다음 ComboBox 컨트롤을 페이지로 끌어옵니다. 다른 AJAX Control Toolkit 컨트롤 및 컨트롤 extenders 사용 (그림 1 참조)를 사용 하 여 도구 상자에서 콤보 상자 컨트롤을 찾을 수 있습니다.


[![명함을 만들기 위한 간단한 폼](how-do-i-use-the-combobox-control-cs/_static/image1.jpg)](how-do-i-use-the-combobox-control-cs/_static/image1.png)

**그림 01**: 도구 상자에서 콤보 상자 컨트롤을 선택 하면 ([큰 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-cs/_static/image2.png))


에서는 ll ComboBox 컨트롤을 사용 하 여 선택 항목의 정적 목록을 표시 합니다. 사용자는 세 가지 선택 목록에서 특정 수준의 해당 음식에 대 한 spiciness 선택할 수 있습니다:가, 미디어 및 핫 (그림 2 참조).


[![항목의 정적 목록에서 선택](how-do-i-use-the-combobox-control-cs/_static/image2.jpg)](how-do-i-use-the-combobox-control-cs/_static/image3.png)

**그림 02**: 항목의 정적 목록에서 선택 ([큰 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-cs/_static/image4.png))


두 가지 방법으로 이러한 선택 콤보 상자 컨트롤에 추가할 수 있습니다. 디자인 뷰에서 컨트롤을 마우스로 가리키면 옵션 편집 작업 옵션을 선택 및 항목 편집기를 열려면 먼저 (그림 3 참조).


[![ComboBox 항목 편집](how-do-i-use-the-combobox-control-cs/_static/image3.jpg)](how-do-i-use-the-combobox-control-cs/_static/image5.png)

**그림 03**: 콤보 상자 편집 항목 ([큰 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-cs/_static/image6.png))


두 번째 옵션은 열기 및 닫기 사이 항목 목록에 추가할 &lt;asp: 콤보 상자&gt; 소스 뷰에서 태그입니다. 목록 1에서 페이지 항목 목록이 있는 업데이트 된 콤보 상자를 포함 합니다.

**1-Static.aspx 나열**

[!code-aspx[Main](how-do-i-use-the-combobox-control-cs/samples/sample1.aspx)]

목록 1에서 페이지를 열면 콤보 상자에서 기존 옵션 중 하나를 선택할 수 있습니다. 즉, ComboBox DropDownList 컨트롤과 마찬가지로 작동합니다.

그러나 해야 하는 새 선택 (예를 들어, 슈퍼 매운) 기존 목록에 입력 하는 옵션. 따라서 콤보 상자는 또한 TextBox 컨트롤 처럼 작동합니다.

기존 선택 여부에 관계 없이 항목 또는 사용자 입력 항목을 사용자 지정 폼을 제출 하면 선택한 레이블 컨트롤에 표시 됩니다. btnSubmit 폼을 제출할 때\_클릭 처리기를 실행 하 고 레이블을 업데이트 합니다 (그림 4 참조).


[![선택한 항목 표시](how-do-i-use-the-combobox-control-cs/_static/image4.jpg)](how-do-i-use-the-combobox-control-cs/_static/image7.png)

**그림 04**: 선택한 항목 표시 ([큰 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-cs/_static/image8.png))


콤보 상자 폼 제출 되 면 선택한 항목을 검색 하기 위한 DropDownList 컨트롤과 같은 속성을 지원 합니다.

- SelectedItem.Text-선택한 항목의 Text 속성의 값을 표시 합니다.
- SelectedItem.Value-선택한 항목의 Value 속성의 값 또는 콤보 상자에 입력 한 텍스트를 표시 합니다.
- SelectedValue-동일 하지만 SelectedItem.Value이이 속성을 사용 하면 기본 (초기) 선택된 항목을 지정할 수 있습니다.

입력 한 다음 사용자 지정 선택 콤보 상자에 사용자 지정 선택 SelectedItem.Text와 SelectedItem.Value 속성에 할당 됩니다.

## <a name="selecting-the-list-of-items-from-the-database"></a>데이터베이스에서 항목 목록을 선택합니다.

데이터베이스에서 콤보 상자를 표시 하는 항목 목록을 검색할 수 있습니다. 예를 들어, SqlDataSource 컨트롤, ObjectDataSource 컨트롤, LinqDataSource, 또는 EntityDataSource ComboBox를 바인딩할 수 있습니다.

ComboBox에 동영상 목록을 표시할 한다고 가정해 보겠습니다. 영화 목록에 영화 데이터베이스 테이블에서 검색 하려고 합니다. 아래 단계를 수행합니다.

1. Movies.aspx 라는 페이지 만들기
2. AJAX 확장명 탭에서 ScriptManager 페이지 도구 상자에서 끌어 페이지에 ScriptManager 컨트롤을 추가 합니다.
3. 콤보 상자를 페이지로 끌어 페이지에는 ComboBox 컨트롤을 추가 합니다.
4. 선택한 디자인 뷰에서 ComboBox 컨트롤 위로 마우스를 가져가서 합니다 **데이터 소스 선택** 작업 옵션 (그림 5 참조). 데이터 소스 구성 마법사가 시작 됩니다.
5. 에 **데이터 원본을 선택** 단계를 선택 합니다 &lt;새 데이터 원본을&gt; 옵션.
6. 에 **데이터 소스 형식 선택** 단계에서 데이터베이스를 선택 합니다.
7. 에 **데이터 연결 선택** 단계 (예를 들어 MoviesDB.mdf) 데이터베이스를 선택 합니다.
8. 에 **응용 프로그램 구성 파일에 연결 문자열 저장** 단계, 연결 문자열을 저장 하는 옵션을 선택 합니다.
9. 에 **Select 문 구성** 단계 영화 데이터베이스 테이블을 선택 하 고 모든 열을 선택 합니다.
10. 에 **테스트 쿼리** 단계, "마침" 단추를 클릭 합니다.
11. 에 **데이터 소스 선택** 단계 선택 표시할 필드에 대 한 제목 열 및 데이터에 대 한 Id 열 필드 (그림 참조).
12. 마법사를 닫으려면 확인 단추를 클릭 합니다.


[![데이터 원본 선택](how-do-i-use-the-combobox-control-cs/_static/image5.jpg)](how-do-i-use-the-combobox-control-cs/_static/image9.png)

**그림 05**: 데이터 원본 선택 ([큰 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-cs/_static/image10.png))


[![데이터 값 및 텍스트 필드를 선택합니다.](how-do-i-use-the-combobox-control-cs/_static/image6.jpg)](how-do-i-use-the-combobox-control-cs/_static/image11.png)

**그림 06**: 데이터 값 및 텍스트 필드를 선택 ([큰 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-cs/_static/image12.png))


위의 단계를 완료 한 후에 콤보 상자 영화 데이터베이스 테이블에서 영화를 나타내는 SqlDataSource 컨트롤에 바인딩되어 있습니다. 페이지에 대 한 원본 (I 정리 서식을 약간) 목록 2와 같습니다.

**2-Movies.aspx 나열**

[!code-aspx[Main](how-do-i-use-the-combobox-control-cs/samples/sample2.aspx)]

ComboBox 컨트롤에 SqlDataSource 컨트롤을 가리키는 DataSourceID 속성이 있음을 알 수 있습니다. 브라우저에서 페이지를 열 때 데이터베이스에서 영화 목록에 표시 됩니다 (그림 7 참조). 선택 목록에서 동영상을 수 있습니다 또는 동영상 콤보 상자에 입력 하 여 새 동영상을 입력 합니다.


[![동영상 목록을 표시합니다.](how-do-i-use-the-combobox-control-cs/_static/image7.jpg)](how-do-i-use-the-combobox-control-cs/_static/image13.png)

**그림 07**: 영화 목록 표시 ([큰 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-cs/_static/image14.png))


## <a name="setting-the-dropdownstyle"></a>dropdownstyle은 설정

ComboBox의 동작을 변경 하려면 ComboBox dropdownstyle은 속성을 사용할 수 있습니다. 이 속성은 있는 허용 가능한 값:

- 드롭다운-드롭다운 화살표를 클릭할 때 목록 (기본값)은 ComboBox 표시 사용자 지정 값을 입력할 수 있습니다.
- 단순-콤보 상자 드롭다운 목록을 자동으로 표시 되 고 사용자 지정 값을 입력할 수 있습니다.
- DropDownList-ComboBox DropDownList 컨트롤과 마찬가지로 작동합니다.

다른 드롭다운 사이 고 간단한 경우 항목의 목록이 표시 됩니다. 간단한 경우 ComboBox에 포커스를 이동 하는 즉시 목록이 표시 됩니다. 드롭다운의 경우 항목의 목록을 보려면 화살표를 클릭 해야 합니다.

DropDownList 값 콤보 상자 컨트롤을 표준 DropDownList 컨트롤 처럼 사용 하면 됩니다. 그러나 여기서 중요 한 차이점이 있습니다. 이전 버전의 Internet Explorer 컨트롤 앞에 배치 되는 모든 컨트롤 앞에 나타납니다. 무한 z-인덱스를 사용 하 여 DropDownList 컨트롤을 표시 합니다. 콤보 상자의 HTML을 렌더링 하기 때문에 &lt;div&gt; HTML 대신 태그 &lt;선택&gt; 태그 ComboBox 올바르게는 z 순서입니다.

## <a name="setting-the-autocompletemode"></a>AutoCompleteMode 설정

콤보 상자 AutoCompleteMode 속성을 사용 하 여 콤보 상자에 텍스트를 입력할 때 적용할 결과 지정 합니다. 이 속성은 다음의 가능한 값을 허용 합니다.

- None-(기본값) 콤보 상자는 자동 완성 동작을 제공 하지 않습니다.
- 제안-콤보 상자 목록을 표시 하 고 목록에서 일치 하는 항목 강조 표시 (그림 8 참조).
- 추가-콤보 상자 목록 표시 되지 않습니다 하 고 목록에서 입력 한 (그림 9 참조)으로 일치 하는 항목을 추가 합니다.
- SuggestAppend-콤보 상자 목록 표시 및 입력 한 (그림 10 참조) 목록에서 일치 하는 항목을 추가 합니다.


[![콤보 상자는 제안](how-do-i-use-the-combobox-control-cs/_static/image8.jpg)](how-do-i-use-the-combobox-control-cs/_static/image15.png)

**그림 08**: The 콤보 상자는 제안 ([큰 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-cs/_static/image16.png))


[![일치 하는 텍스트를 추가 하는 콤보 상자](how-do-i-use-the-combobox-control-cs/_static/image9.jpg)](how-do-i-use-the-combobox-control-cs/_static/image17.png)

**그림 09**: 일치 하는 텍스트를 추가 하는 콤보 상자 ([큰 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-cs/_static/image18.png))


[![콤보 상자에서 제안 하 고 추가](how-do-i-use-the-combobox-control-cs/_static/image10.jpg)](how-do-i-use-the-combobox-control-cs/_static/image19.png)

**그림 10**: The 콤보 상자에서 제안 하 고 추가 ([큰 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-cs/_static/image20.png))


## <a name="summary"></a>요약

이 자습서에서는 ComboBox 컨트롤을 사용 하 여 고정된 된 항목 집합을 표시 하는 방법을 알아보았습니다. 에서는 ComboBox 컨트롤을 정적 항목 집합을 데이터베이스 테이블에 모두 바인딩됩니다. 마지막으로, 해당 dropdownstyle 및 AutoCompleteMode 속성을 설정 하 여 ComboBox의 동작을 수정 하는 방법을 알아보았습니다.

> [!div class="step-by-step"]
> [다음](how-do-i-use-the-combobox-control-vb.md)
