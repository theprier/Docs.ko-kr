---
uid: web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-vb
title: ComboBox 컨트롤을 사용 하려면 어떻게 해야 합니까? (VB) | Microsoft Docs
author: microsoft
description: 콤보 상자에는 사용자가 선택할 수 있는 옵션의 목록을 사용 하 여 입력란의 유연성을 결합 하는 ASP.NET AJAX 컨트롤입니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/12/2009
ms.topic: article
ms.assetid: e887e7b2-a6e7-4a28-a134-ba334494badb
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-vb
msc.type: authoredcontent
ms.openlocfilehash: e42844e326cb190502a51c5a85195b4752d7e827
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="how-do-i-use-the-combobox-control-vb"></a>ComboBox 컨트롤을 사용 하려면 어떻게 해야 합니까? (VB)
====================
by [Microsoft](https://github.com/microsoft)

> 콤보 상자에는 사용자가 선택할 수 있는 옵션의 목록을 사용 하 여 입력란의 유연성을 결합 하는 ASP.NET AJAX 컨트롤입니다.


이 자습서의 목표 AJAX 컨트롤 Toolkit ComboBox 컨트롤을 설명 하는 것입니다. ComboBox 표준 ASP.NET DropDownList 컨트롤 및 TextBox 컨트롤 간의 조합 처럼 작동합니다. 항목의 기존 목록에서 선택 하거나 새 항목을 입력 합니다.

ComboBox 자동 완성 컨트롤 extender를 유사 하지만 컨트롤은 다양 한 시나리오에서 사용 됩니다. 자동 완성 extender 일치 하는 항목을 검색 하는 웹 서비스를 쿼리 합니다. 반면, ComboBox 컨트롤 항목의 집합으로 초기화 됩니다. 자동 완성 extender는 사용 하 여 의미 ComboBox 컨트롤을 사용 하는 동안 다양 한 데이터 (자동차 부분의 수백만)를 사용 하 여 작업할 때 적합 한 작은 데이터 집합 작업 (자동차 부분의 수십).

## <a name="selecting-from-a-static-list-of-items"></a>항목의 정적 목록에서 선택

ComboBox 컨트롤을 사용 하는 간단한 예제로 시작 하는 s를 사용 합니다. 드롭다운 목록에서 항목의 정적 목록을 표시 하 고 가정 합니다. 그러나 목록이 완전 한지 가능성 남겨 하려고 합니다. 사용자가 목록에 사용자 지정 값을 입력 하도록 허용 하려고 합니다.

म ll 새 ASP.NET Web Forms 페이지를 만들고 페이지에서 ComboBox 컨트롤을 사용 합니다. ASP.NET 페이지에 새 프로젝트에 추가 하 고 디자인 뷰로 전환 합니다.

페이지에서 ComboBox 컨트롤을 사용 하려면 페이지에 ScriptManager 컨트롤을 추가 해야 합니다. ScriptManager 컨트롤을 AJAX 확장 탭 아래에서 디자이너 화면으로 끕니다. 페이지 맨 위에 있는 ScriptManager 컨트롤을 추가 해야 여는 서버 쪽 아래 바로 추가할 수 있습니다 &lt;양식&gt; 태그입니다.

다음으로 페이지로 ComboBox 컨트롤을 끕니다. 다른 들어 컨트롤 및 컨트롤 extender (그림 1 참조) 도구 상자에서 ComboBox 컨트롤을 찾을 수 있습니다.


[![명함을 만들기 위한 단순 양식](how-do-i-use-the-combobox-control-vb/_static/image1.jpg)](how-do-i-use-the-combobox-control-vb/_static/image1.png)

**그림 01**: 도구 상자에서 ComboBox 컨트롤을 선택 하면 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-vb/_static/image2.png))


म ll ComboBox 컨트롤을 사용 하 여 선택 항목의 정적 목록을 표시 합니다. 사용자의 세 개의 선택 목록에서 spiciness 자신의 음식에 대 한 특정 수준의 선택할 수: 가벼운 욕설, 보통 및 핫 (그림 2 참조).


[![항목의 정적 목록에서 선택](how-do-i-use-the-combobox-control-vb/_static/image2.jpg)](how-do-i-use-the-combobox-control-vb/_static/image3.png)

**그림 02**: 항목의 정적 목록에서 선택 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-vb/_static/image4.png))


두 가지 방법으로 이러한 선택을 ComboBox 컨트롤을 추가할 수 있습니다. 디자인 뷰에서 컨트롤을 마우스로 가리키면 때 옵션 편집 작업 옵션을 선택 하 고 항목 편집기를 열려면 먼저 (그림 3 참조).


[![콤보 상자 항목 편집](how-do-i-use-the-combobox-control-vb/_static/image3.jpg)](how-do-i-use-the-combobox-control-vb/_static/image5.png)

**그림 03**: 콤보 상자 편집 항목 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-vb/_static/image6.png))


두 번째 옵션은 여는 태그와 닫는 사이에서 항목의 목록을 추가할 &lt;asp: ComboBox&gt; 소스 뷰에서 태그입니다. 목록 1의 페이지 항목 목록이 있는 업데이트 된 콤보 상자를 포함 합니다.

**1-Static.aspx 나열**

[!code-aspx[Main](how-do-i-use-the-combobox-control-vb/samples/sample1.aspx)]

목록 1의 페이지를 열 때 콤보 상자에서 기존 옵션 중 하나를 선택할 수 있습니다. 즉, ComboBox DropDownList 컨트롤과 마찬가지로 작동합니다.

그러나 새로운 항목 (예를 들어 슈퍼 매운) 기존 목록에 없는 입력 하는 옵션도 제공 있습니다. 따라서 콤보 상자는 또한 TextBox 컨트롤 처럼 작동합니다.

기존 선택 여부에 관계 없이 항목 또는 사용자 입력 항목을 사용자 지정 폼을 제출 하면 사용자가 선택한 레이블 컨트롤에 표시 합니다. btnSubmit 폼을 제출할 때\_클릭 처리기를 실행 하 고 레이블을 업데이트 (그림 4 참조).


[![선택한 항목 표시](how-do-i-use-the-combobox-control-vb/_static/image4.jpg)](how-do-i-use-the-combobox-control-vb/_static/image7.png)

**그림 04**: 선택한 항목 표시 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-vb/_static/image8.png))


콤보 상자 폼을 제출 하는 선택한 항목을 검색 하기 위한 DropDownList 컨트롤과 같은 속성을 지원 합니다.

- SelectedItem.Text-선택한 항목의 Text 속성의 값을 표시 합니다.
- SelectedItem.Value-선택한 항목의 Value 속성의 값을 표시 하거나 콤보 상자에 입력 된 텍스트를 표시 합니다.
- SelectedValue-동일 하지만 SelectedItem.Value이이 속성을 사용 하면 기본값 (초기) 선택된 항목을 지정할 수 있습니다.

입력 한 다음 사용자 지정 선택 콤보 상자에 사용자 지정 선택은 SelectedItem.Text와 SelectedItem.Value 속성에 할당 됩니다.

## <a name="selecting-the-list-of-items-from-the-database"></a>데이터베이스에서 항목의 목록을 선택합니다.

데이터베이스에서 콤보 상자를 표시 하는 항목 목록을 검색할 수 있습니다. 예를 들어 SqlDataSource 컨트롤, ObjectDataSource 컨트롤는 LinqDataSource 또는 EntityDataSource ComboBox를 바인딩할 수 있습니다.

ComboBox에 동영상 목록을 표시 하 고 가정 합니다. 영화 데이터베이스 테이블에서 영화 목록을 검색 하려고 합니다. 아래 단계를 수행합니다.

1. Movies.aspx 라는 페이지 만들기
2. AJAX 확장 탭 아래쪽에서 ScriptManager 페이지 도구 상자에서 끌어 페이지에 ScriptManager 컨트롤을 추가 합니다.
3. ComboBox를 페이지로 끌어 페이지로 ComboBox 컨트롤을 추가 합니다.
4. 디자인 뷰에서 마우스 포인터로 ComboBox 컨트롤을 선택 하 고는 **데이터 소스 선택** 작업 옵션 (그림 5 참조). 데이터 소스 구성 마법사가 시작 됩니다.
5. 에 **데이터 원본을 선택** 단계에서는 &lt;새 데이터 원본을&gt; 옵션입니다.
6. 에 **데이터 소스 형식 선택** 단계, 데이터베이스를 선택 합니다.
7. 에 **데이터 연결 선택** 단계, (예를 들어 MoviesDB.mdf) 해당 데이터베이스를 선택 합니다.
8. 에 **응용 프로그램 구성 파일에 연결 문자열 저장** 단계, 연결 문자열을 저장 하도록 선택 합니다.
9. 에 **Select 문 구성** 단계 영화 데이터베이스 테이블을 선택 하 고 모든 열을 선택 합니다.
10. 에 **쿼리 테스트** 단계, "마침" 단추를 클릭 합니다.
11. 에 **데이터 소스 선택** 단계에서 선택 표시 하려면 필드에 대 한 Title 열 및 데이터에 대 한 Id 열 필드 (그림 참조).
12. 마법사를 닫으려면 확인 단추를 클릭 합니다.


[![데이터 원본 선택](how-do-i-use-the-combobox-control-vb/_static/image5.jpg)](how-do-i-use-the-combobox-control-vb/_static/image9.png)

**그림 05**: 데이터 원본 선택 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-vb/_static/image10.png))


[![데이터 텍스트 및 값 필드를 선택합니다.](how-do-i-use-the-combobox-control-vb/_static/image6.jpg)](how-do-i-use-the-combobox-control-vb/_static/image11.png)

**그림 06**: 데이터 텍스트 및 값 필드 선택 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-vb/_static/image12.png))


위의 단계를 완료 한 후 ComboBox 영화 데이터베이스 테이블에서의 영화를 나타내는 SqlDataSource 컨트롤에 바인딩됩니다. 페이지에 대 한 소스 (I 정리 서식을 약간) 목록 2와 유사 합니다.

**2-Movies.aspx 나열**

[!code-aspx[Main](how-do-i-use-the-combobox-control-vb/samples/sample2.aspx)]

ComboBox 컨트롤 SqlDataSource 컨트롤을 가리키는 DataSourceID 속성을 갖고 있음을 알게 됩니다. 브라우저에서 페이지를 열 때 데이터베이스에서 영화 목록이 표시 됩니다 (그림 7 참조). 선택 목록에서 영화 수 또는 동영상 콤보 상자에 입력 하 여 새 동영상을 입력 합니다.


[![동영상 목록을 표시합니다.](how-do-i-use-the-combobox-control-vb/_static/image7.jpg)](how-do-i-use-the-combobox-control-vb/_static/image13.png)

**그림 07**: 영화 목록이 표시 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-vb/_static/image14.png))


## <a name="setting-the-dropdownstyle"></a>DropDownStyle는 설정

ComboBox의 동작을 변경 하려면 ComboBox DropDownStyle 속성을 사용할 수 있습니다. 이 속성은 있는 허용 가능한 값:

- 드롭다운-(기본값)는 ComboBox 드롭다운 목록에서 화살표를 클릭할 때 표시 됩니다는 사용자 지정 값을 입력할 수 있습니다.
- 단순-ComboBox 드롭다운 목록을 자동으로 표시 하 고 사용자 지정 값을 입력할 수 있습니다.
- DropDownList-ComboBox DropDownList 컨트롤과 마찬가지로 작동합니다.

단순 및 드롭다운 간의 차이 항목 목록이 표시 될 때입니다. 단순의 경우는 콤보 상자에 포커스를 이동 하면 즉시 목록이 표시 됩니다. 드롭다운에서 경우 항목의 목록을 보려면 화살표를 클릭 해야 합니다.

DropDownList 값 검사가 ComboBox 컨트롤 표준 DropDownList 컨트롤 처럼 작동 하도록 합니다. 그러나 여기에 중요 한 차이점이 있습니다. 이전 버전의 Internet Explorer 컨트롤 앞에 배치 하는 모든 컨트롤 앞에 표시 됩니다 무한 z-인덱스 DropDownList 컨트롤을 표시 합니다. 콤보 상자는 HTML을 렌더링 하기 때문에 &lt;div&gt; 태그는 HTML 대신 &lt;선택&gt; 태그, ComboBox 올바르게는 존중 z 순서 지정 합니다.

## <a name="setting-the-autocompletemode"></a>AutoCompleteMode 설정

ComboBox AutoCompleteMode 속성을 사용 하 여 콤보 상자에 텍스트를 입력할 때 수행 되는 작업을 지정할 수 있습니다. 이 속성은 다음 값을 허용합니다.

- None-(기본값) 콤보 상자는 자동 완성 동작을 제공 하지 않습니다.
- 제안-ComboBox 목록을 표시 하 고 목록에서 일치 하는 항목 강조 표시 (그림 8 참조).
- 추가-콤보 상자 목록에 나타나지 않습니다 하 고 목록에서 입력 한 (그림 9 참조)으로 일치 하는 항목을 추가 합니다.
- SuggestAppend-ComboBox 모두 목록을 표시 하 고 목록에서 입력 한 (그림 10 참조)으로 일치 하는 항목을 추가 합니다.


[![ComboBox 만듭니다 제안을](how-do-i-use-the-combobox-control-vb/_static/image8.jpg)](how-do-i-use-the-combobox-control-vb/_static/image15.png)

**그림 08**: The ComboBox 만듭니다 제안 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-vb/_static/image16.png))


[![일치 하는 텍스트를 추가 하는 콤보 상자](how-do-i-use-the-combobox-control-vb/_static/image9.jpg)](how-do-i-use-the-combobox-control-vb/_static/image17.png)

**그림 09**: ComboBox 일치 하는 텍스트를 추가 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-vb/_static/image18.png))


[![ComboBox를 소개 하 고 추가](how-do-i-use-the-combobox-control-vb/_static/image10.jpg)](how-do-i-use-the-combobox-control-vb/_static/image19.png)

**그림 10**: The ComboBox를 소개 하 고 추가 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-vb/_static/image20.png))


## <a name="summary"></a>요약

이 자습서에서는 항목의 고정된 된 집합을 표시 하려면 ComboBox 컨트롤을 사용 하는 방법을 배웠습니다. 에서는 ComboBox 컨트롤을 항목을 설정 하는 정적 하 고 데이터베이스 테이블에 모두 바인딩됩니다. 마지막으로, 해당 DropDownStyle 고 AutoCompleteMode 속성을 설정 하 여 ComboBox의 동작을 수정 하는 방법을 배웠습니다.

> [!div class="step-by-step"]
> [이전](how-do-i-use-the-combobox-control-cs.md)
