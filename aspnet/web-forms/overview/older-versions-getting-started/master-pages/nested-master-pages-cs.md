---
uid: web-forms/overview/older-versions-getting-started/master-pages/nested-master-pages-cs
title: 마스터 페이지 (C#) 중첩 된 | Microsoft Docs
author: rick-anderson
description: 내에서 다른 한 마스터 페이지를 중첩 하는 방법을 보여 줍니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/28/2008
ms.topic: article
ms.assetid: 32b7fb6e-d74b-4048-91f8-70631b2523ee
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/nested-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: c9497659e0b8ff8164f122e6e3cb382ac0355a32
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30891466"
---
<a name="nested-master-pages-c"></a>중첩 된 마스터 페이지 (C#)
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/d/6/6/d66ad554-afdd-409e-a5c3-201b774fbb31/ASPNET_MasterPages_Tutorial_10_CS.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/d/6/6/d66ad554-afdd-409e-a5c3-201b774fbb31/ASPNET_MasterPages_Tutorial_10_CS.pdf)

> 내에서 다른 한 마스터 페이지를 중첩 하는 방법을 보여 줍니다.


## <a name="introduction"></a>소개

지난 9 개의 자습서의 과정 동안 마스터 페이지와 사이트 전체 레이아웃을 구현 하는 방법을 살펴보았습니다. 간단히 말해, 마스터 페이지 수, 페이지 개발자 콘텐츠 페이지 콘텐츠 페이지 단위로 지정할 수 있는 특정 영역 함께 마스터 페이지에서 일반적인 태그를 정의할 수 있습니다. 마스터 페이지에서 ContentPlaceHolder 컨트롤 나타내는 사용자 지정 가능한 지역을 선택 합니다. ContentPlaceHolder 컨트롤에 대 한 사용자 지정 된 태그는 콘텐츠 컨트롤을 통해 콘텐츠 페이지에 정의 됩니다.

지금까지 알아보았으므로 마스터 페이지 기술을 사이트 전체에서 사용 되는 단일 레이아웃이 있는 경우에 유용 합니다. 그러나 큰 웹 사이트의 대부분은 다양 한 섹션에서 사용자 지정 된 사이트 레이아웃이 있습니다. 예를 들어 병원 담당자가 환자 정보, 활동 및 대금 청구를 관리 하는 데 사용 되는 의료 응용 프로그램입니다. 이 응용 프로그램에서 웹 페이지의 하나일 수 있습니다.

- 직원 멤버 관련 페이지가 직원 가용성을 업데이트할 수 있는 일정을 보거나 휴가 요청 합니다.
- 환자 관련 페이지가 있는 직원 정보 보기 또는 편집 특정 환자에 대 한 합니다.
- 대금 청구 관련 페이지가 회계 담당자 검토 현재 상태 및 재무 보고서를 요청 하십시오.

모든 페이지 위쪽 및 아래쪽 자주 사용 되는 링크의 계열에서 메뉴와 같은 일반적인 레이아웃을 공유할 수 있습니다. 하지만이 일반적인 레이아웃을 사용자 지정 하는 직원, 환자 차원 및 대금 청구 관련 페이지가 할 수 있습니다. 예를 들어 아마도 모든 직원 관련 페이지에는 현재 로그온된 한 사용자의 가용성 및 일별 일정을 표시 하는 일정 및 작업 목록이 포함 되어야 합니다. 아마도 모든 환자 관련 페이지 이름, 주소 및 정보를 가져올 편집 하 고 환자에 대 한 보험 정보를 표시 해야 합니다.

사용 하 여 이러한 사용자 지정된 레이아웃을 만들 수는 *중첩 된 마스터 페이지*합니다. 위의 시나리오를 구현 하려면 contentplaceholders의 사용자 지정 가능한 영역을 정의 사용 하 여 사이트 전체 레이아웃, 메뉴 및 바닥글 콘텐츠를 정의 하는 마스터 페이지를 만드는 것 먼저. 다음 세 개의 중첩 된 마스터 페이지, 웹 페이지의 각 형식에 대 한 하나 만듭니다. 각 중첩 된 마스터 페이지의 마스터 페이지를 사용 하는 콘텐츠 페이지 형식 간에 콘텐츠를 정의 합니다. 즉, 태그 및 편집 하 고 환자에 대 한 정보를 표시 하기 위한 프로그래밍 논리를 환자 관련 콘텐츠 페이지에 대 한 중첩 된 마스터 페이지 포함 합니다. 새 환자 관련 페이지를 만들 때이 중첩 된 마스터 페이지에 바인딩하는 것 했습니다.

중첩 된 마스터 페이지의 이점을 강조 표시 하 여이 자습서를 시작 합니다. 그런 다음 만들고 중첩 된 마스터 페이지를 사용 하는 방법을 보여 줍니다.

> [!NOTE]
> 중첩 된 마스터 페이지의.NET Framework 버전 2.0부터 가능한 되었습니다. 그러나 Visual Studio 2005는 중첩 된 마스터 페이지에 대 한 디자인 타임 지원을 포함 되지 않았습니다. 다행히도 Visual Studio 2008 중첩 된 마스터 페이지에 대 한 풍부한 디자인 타임 환경을 제공 한다는입니다. 중첩 된 마스터 페이지를 사용 하 여 관심 있는 해도 Visual Studio 2005를 계속 사용 하는 경우 체크 아웃 [Scott Guthrie](https://weblogs.asp.net/scottgu/)의 블로그 항목- [VS 2005 디자인 타임에서 중첩 된 마스터 페이지에 대 한 팁](https://weblogs.asp.net/scottgu/archive/2005/11/11/430382.aspx)합니다.


## <a name="the-benefits-of-nested-master-pages"></a>중첩 된 마스터 페이지의 이점

대부분의 웹 사이트는 특정 유형의 페이지에만 사용자 지정된 디자인 더 뿐 아니라는 가장 중요 한 사이트 디자인 합니다. 예를 들어, 데모 웹 응용 프로그램에서 만들어져 기초적인 관리 섹션 (의 페이지는 `~/Admin` 폴더). 현재 웹 페이지에는 `~/Admin` 관리 섹션에는 해당 페이지와 같은 마스터 페이지를 사용 하는 폴더 (즉, `Site.master` 또는 `Alternate.master`사용자의 선택에 따라).

> [!NOTE]
> 이제는 사이트에 하나만 마스터 페이지를 가장 `Site.master`합니다. 두 개 이상의 마스터 페이지를 사용 하는 중첩 된 마스터 페이지에 대 한 the 관리 "섹션"로 시작 하는 중첩 된 마스터 페이지를 사용 하 여이 자습서의 뒷부분에서 설명 합니다.


추가 정보 또는 수 없는 사이트의 다른 페이지에 없는 링크를 포함 하도록 관리 페이지의 레이아웃을 사용자 지정 요청 받았습니다 म 한다고 가정 합니다. 이 요구 사항을 구현 하기 위한 4 개의 기술을 가지가 있습니다.

1. 모든 콘텐츠 페이지에 관리 관련 정보 및 링크를 수동으로 추가 `~/Admin` 폴더입니다.
2. 업데이트는 `Site.master` 마스터 페이지를 표시 하거나 숨기려면이 섹션에서는 마스터 페이지에 코드를 추가 및 관리 섹션 관련 정보 및 링크를 포함 하는지 여부는 관리 페이지 중 하나를 방문 하 기반 합니다.
3. 마스터 페이지를 새로 만들 관리 섹션에 대 한 구체적으로 태그를 통해 복사 `Site.master`관리 섹션 관련 정보 및 링크를 추가 하 고 다음에서 콘텐츠 페이지를 업데이트는 `~/Admin` 이 새 마스터를 사용 하는 폴더 페이지입니다.
4. 에 바인딩되는 중첩 된 마스터 페이지를 만들 `Site.master` , 콘텐츠 페이지에는 `~/Admin` 마스터 페이지를 중첩 하는 새 폴더 사용 합니다. 이 중첩 된 마스터 페이지는 추가 정보 및 링크 관리 페이지에만 포함 및 태그에 이미 정의 된 반복 않아도 `Site.master`합니다.

첫 번째 옵션은 가장 마음에 들지 않는입니다. 마스터 페이지를 사용 하 여 수동으로 복사 하 고 새 ASP.NET 페이지에 일반 태그를 붙여을 옮기는 것입니다. 두 번째 옵션은 사용할 수 있지만 응용 프로그램을 줄이려면 대로 것 관계식을 추가 하려면 가끔씩만 표시 되 고 개발자 마스터 페이지를 편집이 태그를 해결 하 고 시기를 기억할 필요가 있는 태그로 마스터 페이지를 사용 하면 정확 하 게 숨겨진 특정 태그와 표시 됩니다. 이 방법은 점점 더 많은 유형의이 단일 마스터 페이지에서 수용 하는 데 필요한 웹 페이지에서 사용자 지정으로 덜 해 것입니다.

코드에서 제거 하는 세 번째 옵션을 표시 복잡성 surfaced는 두 번째 옵션을 사용 합니다. 그러나 옵션 3의 주요 단점은 필요 하다는 것을 복사 하 고 일반적인 레이아웃을 붙여 `Site.master` 새 관리 섹션 별 마스터 페이지로 합니다. 경우 나중에 두 위치에서 변경 하 게 해야 사이트 전체 레이아웃을 변경 하려고 합니다.

네 번째 옵션을 중첩 된 마스터 페이지의 두 번째 및 세 번째 옵션을 제공 합니다. 사이트 전체 레이아웃 정보는 유지 관리 한 파일-최상위 마스터 페이지-특정 영역에만 콘텐츠를 다른 파일에 분리 됩니다.

이 자습서를 살펴보고 만들고 간단한 중첩 된 마스터 페이지를 사용 하 여 시작 합니다. 새로운 최상위 마스터 페이지, 두 개의 중첩 된 마스터 페이지 및 두 개의 콘텐츠 페이지 만듭니다. 중첩 된 마스터 페이지의 사용을 포함 하도록 기존 마스터 페이지 아키텍처 우리의 업데이트 살펴봅니다 "를 사용 하는 중첩 된 마스터 페이지에 대 한 the 관리 섹션"로 시작 합니다. 특히, 우리 만든 중첩 된 마스터 페이지를 사용 하 여 콘텐츠 페이지에 대 한 추가 사용자 지정 콘텐츠를 포함 하도록는 `~/Admin` 폴더입니다.

## <a name="step-1-creating-a-simple-top-level-master-page"></a>1 단계: 간단한 최상위 마스터 페이지 만들기

중첩 된 마스터 만들기 페이지를 기반으로 기존 마스터 중 하나에 하 고 기존 콘텐츠 페이지에 특정 항목을 이미 기대 하기 때문에 일부 복잡성을 수반 최상위 마스터 페이지 대신이 새로운 중첩 된 마스터 페이지를 사용 하도록 기존 콘텐츠 페이지를 업데이트 한 다음 ContentPlaceHolder 제어 최상위 마스터 페이지에 정의 합니다. 따라서 중첩 된 마스터 페이지와 같은 이름의 동일한 ContentPlaceHolder 컨트롤을도 포함 해야 합니다. 또한 특정 데모 응용 프로그램에 두 개의 마스터 페이지 (`Site.master` 및 `Alternate.master`) 이러한 복잡성을 더 추가 하는 사용자의 기본 설정에 따라 콘텐츠 페이지에 동적으로 할당 되어 있습니다. 이 자습서의 뒷부분에 나오는 중첩 된 마스터 페이지를 사용 하도록 기존 응용 프로그램 업데이트 하는 방법에 있지만 간단한 중점을 첫 번째 마스터 페이지 예제를 중첩 하는 보겠습니다.

라는 새 폴더 만들기 `NestedMasterPages` 다음 새 마스터 페이지 파일을 해당 폴더에 추가 `Simple.master`합니다. (그림 1 참조 솔루션 탐색기의 스크린 샷을 대 한이 폴더 및 파일이 추가 된 후). 끌어서는 `AlternateStyles.css` 디자이너 솔루션 탐색기에서 스타일 시트 파일입니다. 이렇게 하면 추가 `<link>` 요소에서 스타일 시트 파일에는 `<head>` 요소 뒤 마스터 페이지의 `<head>` 요소의 태그 같습니다:


[!code-aspx[Main](nested-master-pages-cs/samples/sample1.aspx)]

그런 다음 Web Form의 내에서 다음 태그를 추가 `Simple.master`:


[!code-aspx[Main](nested-master-pages-cs/samples/sample2.aspx)]

이 태그 남색 배경 기반 흰색를 큰 글꼴로 페이지 맨 위에 있는 "Nested 마스터 페이지 (단순)" 이라는 링크가 표시 됩니다. 아래에 `MainContent` ContentPlaceHolder 합니다. 그림 1에 나와 `Simple.master` Visual Studio 디자이너에 로드 될 때 마스터 페이지입니다.


[![중첩 된 마스터 페이지의 관리 섹션에 있는 페이지에 콘텐츠 관련 정의](nested-master-pages-cs/_static/image2.png)](nested-master-pages-cs/_static/image1.png)

**그림 01**: The 중첩 된 마스터 페이지를 정의 콘텐츠 관련 관리 섹션에 있는 페이지 ([전체 크기 이미지를 보려면 클릭](nested-master-pages-cs/_static/image3.png))


## <a name="step-2-creating-a-simple-nested-master-page"></a>2 단계: 간단한 중첩 된 마스터 페이지 만들기

`Simple.master` 두 개의 ContentPlaceHolder 컨트롤이 포함:는 `MainContent` 와 함께 웹 폼 내에서 추가 ContentPlaceHolder는 `head` 에서 ContentPlaceHolder는 `<head>` 요소. 콘텐츠 페이지를 만들고에 바인딩할 경우 `Simple.master` 콘텐츠 페이지 콘텐츠 컨트롤을 두 가지 두 contentplaceholders의 참조 하는 것입니다. 마찬가지로, 중첩된 된 마스터 페이지를 만든 경우 하에 바인딩할 `Simple.master` 중첩 된 마스터 페이지 콘텐츠 컨트롤을 두 가지 해야 합니다.

새 중첩 된 마스터 페이지를 추가 해 보겠습니다는 `NestedMasterPages` 라는 폴더 `SimpleNested.master`합니다. 마우스 오른쪽 단추로 클릭는 `NestedMasterPages` 폴더를 새 항목 추가 선택 합니다. 이 그림 2에 표시 된 새 항목 추가 대화 상자를 엽니다. 마스터 페이지 템플릿 유형을 선택 하는 새 마스터 페이지의 이름을 입력 합니다. 새 마스터 페이지에서 중첩된 된 마스터 페이지를 해야 함을 나타내려면 "마스터 페이지 선택" 확인란을 선택 합니다.

추가 단추를 클릭 합니다. 동일한 Select 마스터 페이지 콘텐츠 페이지에 바인딩할 때 참조 마스터 페이지 대화 상자가 표시 됩니다 (그림 3 참조). 선택 된 `Simple.master` 마스터 페이지에는 `NestedMasterPages` 폴더 확인을 클릭 합니다.

> [!NOTE]
> 웹 사이트 프로젝트 모델 대신 웹 응용 프로그램 프로젝트 모델을 사용 하 여 ASP.NET 웹 사이트를 만든 경우 그림 2에 표시 된 새 항목 추가 대화 상자에서 "마스터 페이지 선택" 확인란을 표시 되지 않습니다. 만들려는 웹 응용 프로그램 프로젝트 모델을 사용 하는 경우 중첩된 된 마스터 페이지 (마스터 페이지 템플릿) 하는 대신 중첩 된 마스터 페이지 파일을 선택 해야 합니다. 중첩 된 마스터 페이지 템플릿을 선택한 후 추가 클릭 하면, 그림 3과 같은 대화 상자가 나타납니다. 마스터 페이지를 선택 동일 합니다.


[![확인 된 &quot;마스터 페이지 선택&quot; 중첩 된 마스터 페이지를 추가 하려면이 확인란을](nested-master-pages-cs/_static/image5.png)](nested-master-pages-cs/_static/image4.png)

**그림 02**: 확인란을 선택 "마스터 페이지 선택" 중첩 된 마스터 페이지를 추가 하려면 ([전체 크기 이미지를 보려면 클릭](nested-master-pages-cs/_static/image6.png))


[![중첩 된 마스터 페이지 Simple.master 마스터 페이지에 바인딩](nested-master-pages-cs/_static/image8.png)](nested-master-pages-cs/_static/image7.png)

**그림 03**: 중첩 된 마스터 페이지를 바인딩하는 `Simple.master` 마스터 페이지 ([전체 크기 이미지를 보려면 클릭](nested-master-pages-cs/_static/image9.png))


중첩 된 마스터 페이지의 선언적 태그를 아래 표시 된 두 개의 콘텐츠 컨트롤을 최상위 마스터 페이지의 두 ContentPlaceHolder 컨트롤 참조를 포함 합니다.


[!code-aspx[Main](nested-master-pages-cs/samples/sample3.aspx)]

제외 하 고는 `<%@ Master %>` 지시문, 중첩 된 마스터 페이지의 초기 선언적 태그는 동일한 최상위 마스터 페이지 콘텐츠 페이지에 바인딩할 때 처음 생성 되는 태그와 동일 합니다. 콘텐츠 페이지의 같은 `<%@ Page %>` 지시문의 `<%@ Master %>` 지시문 여기에 포함 됩니다는 `MasterPageFile` 중첩 된 마스터 페이지의 부모에 대 한 마스터 페이지를 지정 하는 특성입니다. 중첩 된 마스터 페이지와 같은 최상위 마스터 페이지에 바인딩된 콘텐츠 페이지 간의 주요 차이점은 중첩 된 마스터 페이지 ContentPlaceHolder 컨트롤을 포함할 수 있습니다. 중첩 된 마스터 페이지의 ContentPlaceHolder 컨트롤 콘텐츠 페이지 태그를 사용자 지정할 수 있는 영역을 정의 합니다.

텍스트 "Hello, SimpleNested에서!"이 표시 되도록이 중첩 된 마스터 페이지를 업데이트 합니다. 에 해당 하는 콘텐츠 컨트롤에는 `MainContent` ContentPlaceHolder 제어 합니다.


[!code-aspx[Main](nested-master-pages-cs/samples/sample4.aspx)]

이 추가 마치면 중첩 된 마스터 페이지를 저장 한 후에 새 콘텐츠 페이지를 추가 `NestedMasterPages` 라는 폴더 `Default.aspx`에 바인딩할는 `SimpleNested.master` 마스터 페이지입니다. 이 페이지에 추가 되 면 콘텐츠 (그림 4 참조) 컨트롤이 포함 되어 있는 확인할 놀랄 수 있습니다! 콘텐츠 페이지에만 액세스할 수는 *부모* 마스터 페이지의 contentplaceholders의 합니다. `SimpleNested.master` ContentPlaceHolder 컨트롤이; 들어 있지 않습니다. 따라서이 마스터 페이지에 바인딩된 모든 콘텐츠 페이지 모든 콘텐츠 컨트롤을 포함할 수 없습니다.


[![새 콘텐츠 페이지 컨트롤이 포함 되지 않은 콘텐츠](nested-master-pages-cs/_static/image11.png)](nested-master-pages-cs/_static/image10.png)

**그림 04**:의 새 콘텐츠 페이지 포함 아니요 콘텐츠 컨트롤 ([전체 크기 이미지를 보려면 클릭](nested-master-pages-cs/_static/image12.png))


그러려면 필요한 것은 중첩 된 마스터 페이지를 업데이트 (`SimpleNested.master`) ContentPlaceHolder 컨트롤을 포함 합니다. 일반적으로 ContentPlaceHolder 부모 마스터 페이지에 정의 된 각 ContentPlaceHolder 되므로 해당 자식 마스터 페이지 또는 콘텐츠 페이지를 최상위 마스터 페이지의 ContentPlaceHolder를 사용 하 여 작업에 대 한 포함 하도록 하려면 중첩 된 마스터 페이지 합니다. 제어 합니다.

업데이트는 `SimpleNested.master` 마스터 페이지의 두 콘텐츠 컨트롤에는 ContentPlaceHolder 포함 하도록 합니다. ContentPlaceHolder 컨트롤의 콘텐츠 컨트롤을 가리키는 ContentPlaceHolder 컨트롤로 같은 이름을 지정 합니다. 즉, 라는 ContentPlaceHolder 컨트롤을 추가 `MainContent` 콘텐츠 컨트롤에 `SimpleNested.master` 참조 하는 `MainContent` 에서 ContentPlaceHolder `Simple.master`합니다. 참조 하는 콘텐츠 컨트롤에 같은 방식으로 `head` ContentPlaceHolder 합니다.

> [!NOTE]
> 중첩 된 마스터 페이지에서 ContentPlaceHolder 컨트롤을 최상위 마스터 페이지에 contentplaceholders의와 동일 하 게 명명이 좋지만, 명명 대칭이 필요 하지 않습니다. 제공할 수 있습니다 ContentPlaceHolder 컨트롤 중첩 된 마스터 페이지의 이름은 원하는 대로. 그러나 찾습니까 contentplaceholders의 협력 기억 하기 쉬운 내 최상위 마스터 페이지 및 중첩 된 마스터 페이지에 동일한 이름을 사용 하는 경우 페이지의 어떤 영역입니다.


추가 하는이 코드를 변경한 후 사용자 `SimpleNested.master` 선언 마스터 페이지의 태그는 다음과 비슷해야 합니다.


[!code-aspx[Main](nested-master-pages-cs/samples/sample5.aspx)]

삭제 된 `Default.aspx` 콘텐츠 페이지 방금 만든 한 다음 다시 추가,에 바인딩하기는 `SimpleNested.master` 마스터 페이지입니다. 두 개이 이번 Visual Studio 추가 콘텐츠 컨트롤을 `Default.aspx`에 정의 된 이제는 contentplaceholders의 참조 `SimpleNested.master` (그림 6 참조). "Default.aspx에서: Hello!" 텍스트를 추가 합니다. 참조 되는 콘텐츠 컨트롤 `MainContent`합니다.

그림 5-여기에 포함 하는 세 가지 엔터티는 `Simple.master`, `SimpleNested.master`, 및 `Default.aspx` -서로 간의 관계입니다. 다이어그램에서 보듯이 중첩 된 마스터 페이지는 해당 부모의 ContentPlaceHolder를 콘텐츠 컨트롤을 구현 합니다. 이러한 영역 콘텐츠 페이지에 액세스할 수 있어야, 중첩 된 마스터 페이지 콘텐츠 컨트롤에는 자체 contentplaceholders의 추가 해야 합니다.


[![최상위 및 중첩 된 마스터 페이지 콘텐츠 페이지의 레이아웃 지정](nested-master-pages-cs/_static/image14.png)](nested-master-pages-cs/_static/image13.png)

**그림 05**: 최상위 및 중첩 된 마스터 페이지 콘텐츠 페이지의 레이아웃을 지정 ([전체 크기 이미지를 보려면 클릭](nested-master-pages-cs/_static/image15.png))


이 동작은 방법을 콘텐츠 페이지 또는 마스터 페이지는 에서만 인식 하 고 해당 부모 마스터 페이지를 보여 줍니다. 이 문제는 Visual Studio 디자이너도도 표시 됩니다. 그림 6에 대 한 디자이너를 보여 줍니다. `Default.aspx`합니다. 어떤 영역 콘텐츠 페이지에서 편집할 수 있으며 일부 되지 않습니다을 명확 하 게 표시 하는 디자이너, 중첩 된 마스터 페이지에서 이란 불가능 하 고 최상위 마스터 페이지에서 영역은 명확히 구분 하지 않습니다.


[![콘텐츠 페이지 지금 contentplaceholders의 중첩 된 마스터 페이지에 대 한 콘텐츠 컨트롤을 포함](nested-master-pages-cs/_static/image17.png)](nested-master-pages-cs/_static/image16.png)

**그림 06**: The 콘텐츠 페이지 이제 포함 콘텐츠 컨트롤에 대 한 중첩 된 마스터 페이지의 contentplaceholders의 ([전체 크기 이미지를 보려면 클릭](nested-master-pages-cs/_static/image18.png))


## <a name="step-3-adding-a-second-simple-nested-master-page"></a>3 단계: 두 번째 단순 중첩 된 마스터 페이지를 추가합니다.

중첩 된 마스터 페이지의 이점은 여러 개의 중첩 된 마스터 페이지에 있는 경우 더 분명 하 게 점입니다. 을 설명 하기 위해이 혜택에 또 다른 중첩 된 마스터 페이지를 만듭니다는 `NestedMasterPages` 폴더; 중첩 이름이 새 마스터 페이지 `SimpleNestedAlternate.master` 에 바인딩할는 `Simple.master` 마스터 페이지입니다. 2 단계에서에서 수행한 것 처럼 중첩 된 마스터 페이지의 두 가지 콘텐츠 컨트롤에서 ContentPlaceHolder 컨트롤을 추가 합니다. "SimpleNestedAlternate에서: Hello!" 라는 텍스트를 추가 최상위 마스터 페이지에 해당 하는 콘텐츠 컨트롤에 `MainContent` ContentPlaceHolder 합니다. 이러한 변경을 수행한 후 새 중첩 된 마스터 페이지의 선언적 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](nested-master-pages-cs/samples/sample6.aspx)]

명명 된 콘텐츠 페이지를 만들 `Alternate.aspx` 에 `NestedMasterPages` 폴더에 바인딩합니다는 `SimpleNestedAlternate.master` 중첩 된 마스터 페이지입니다. "대체 용어에서: Hello!" 텍스트를 추가 합니다. 에 해당 하는 콘텐츠 컨트롤에 `MainContent`합니다. 그림 7은 `Alternate.aspx` Visual Studio 디자이너를 통해 표시 될 경우.


[![Alternate.aspx는 SimpleNestedAlternate.master 마스터 페이지에 바인딩된](nested-master-pages-cs/_static/image20.png)](nested-master-pages-cs/_static/image19.png)

**그림 07**: `Alternate.aspx` 바인딩되는 `SimpleNestedAlternate.master` 마스터 페이지 ([전체 크기 이미지를 보려면 클릭](nested-master-pages-cs/_static/image21.png))


그림 7을 그림 6에 디자이너의 디자이너를 비교 합니다. 최상위 마스터 페이지에 정의 된 동일한 레이아웃을 공유 하는 두 콘텐츠 페이지 (`Simple.master`), 즉 "Nested 마스터 페이지 자습서 (단순)" 제목입니다. 아직 둘 다 고유한 콘텐츠 부모 마스터 페이지-에 정의 된 텍스트 "Hello, SimpleNested에서!" 그림 6 및 "SimpleNestedAlternate에서: Hello!"에서 그림 7입니다. 부여, 여기에 이러한 차이점은 중요 하지 않습니다 되지만이 예제에서는 더 의미 있는 차이 포함 하도록 확장할 수 있습니다. 예를 들어,는 `SimpleNested.master` 반면 페이지 콘텐츠 페이지의 특정 옵션이 있는 메뉴가 포함 될 수 있습니다 `SimpleNestedAlternate.master` 에 바인딩되는 콘텐츠 페이지와 관련 된 정보가 있을 수 있습니다.

이제 가장 중요 한 사이트 레이아웃을 변경 해야 한다고 가정 합니다. 예를 들어, 모든 콘텐츠 페이지에 일반 연결의 목록을 추가 하 려 한다고 가정 합니다. 이 최상위 마스터 페이지 업데이트를 위해 `Simple.master`합니다. 변경 내용을에 중첩 된 마스터 페이지 및 확장을 통해, 해당 콘텐츠 페이지에 바로 반영 됩니다.

म 가장 중요 한 사이트 레이아웃을 변경할 수 있는 간편한을 보여 주기 위해 열고는 `Simple.master` 사이 다음 태그를 추가 하 고 마스터 페이지는 `topContent` 및 `mainContent` `<div>` 요소:


[!code-aspx[Main](nested-master-pages-cs/samples/sample7.aspx)]

그러면 두 개의 링크가에 바인딩되는 모든 페이지의 맨 위에 추가 `Simple.master`, `SimpleNested.master`, 또는 `SimpleNestedAlternate.master`; 모든 중첩 된 마스터 페이지와 해당 콘텐츠 페이지에 이러한 변경 내용은 즉시 적용 합니다. 그림 8 나와 `Alternate.aspx` 브라우저를 통해 볼 때. Note (그림 7 비교) 페이지의 위쪽에 표시 된 링크를 추가 합니다.


[![해당 중첩 된 마스터 페이지 및 해당 콘텐츠 페이지에 바로 반영 됩니다 최상위 마스터 페이지에 변경](nested-master-pages-cs/_static/image23.png)](nested-master-pages-cs/_static/image22.png)

**그림 08**: 최상위 마스터 페이지에 변경의 중첩 된 마스터 페이지 및 해당 콘텐츠 페이지에 바로 반영 됩니다 ([전체 크기 이미지를 보려면 클릭](nested-master-pages-cs/_static/image24.png))


## <a name="using-a-nested-master-page-for-the-administration-section"></a>중첩 된 마스터 페이지를 사용 하 여 관리 섹션에 대 한

이 시점에서 페이지 중첩 된 마스터의 장점에 보지 못했을 하 고 만들고 ASP.NET 응용 프로그램에서 사용 하는 방법에 알아보았습니다. 그러나 1, 2, 3, 단계의 예제에서는 새 최상위 마스터 페이지, 새 중첩 된 마스터 페이지 및 새 콘텐츠 페이지 만들기에 관련 되었습니다. 새 중첩 된 마스터 페이지를 웹 사이트에 있는 기존 최상위 마스터 페이지 및 콘텐츠 페이지 추가 작업은 어떤가요?

기존 웹 사이트에 중첩된 된 마스터 페이지를 통합 하 고 기존 콘텐츠 페이지와 연결 하 고 처음부터 시작 하는 보다 약간 더 많은 노력이 필요 합니다. 4, 5, 6 및 7 단계는 새 중첩 된 마스터 페이지를 포함 하도록 데모 응용 프로그램을 확장 하는 것 처럼 이러한 과제를 탐색 `AdminNested.master` 관리자에 대 한 지침을 포함 하 고에서 ASP.NET 페이지에서 사용 되는 `~/Admin` 폴더입니다.

데모 응용 프로그램에 중첩된 된 마스터 페이지 통합 다음 장애물을 도입 합니다.

- 기존 콘텐츠 페이지에 `~/Admin` 폴더의 마스터 페이지에서 특정 예측도 합니다. 먼저 존재 하도록 특정 ContentPlaceHolder 컨트롤 기대 합니다. 또한는 `~/Admin/AddProduct.aspx` 및 `~/Admin/Products.aspx` 페이지 호출할 마스터 페이지의 공용 `RefreshRecentProductsGrid` 메서드를 설정 해당 `GridMessageText` 속성에 대 한 이벤트 처리기 수도 있고 해당 `PricesDoubled` 이벤트입니다. 따라서 중첩 된 마스터 페이지 contentplaceholders의 동일한 및 public 멤버를 제공 해야 합니다.
- 확장에서는 이전 자습서에서는 `BasePage` 클래스를 동적으로 설정 된 `Page` 개체의 `MasterPageFile` 세션 변수를 기반으로 한 속성입니다. 어떻게 하 지원 동적 마스터 페이지 중첩 된 마스터 페이지를 사용 하는 경우?

이러한 두 가지 문제를 중첩 된 마스터 페이지를 작성 하 고는 기존 콘텐츠 페이지에서 라이브러리를 사용 하는 대로 노출할 합니다. 조사 알아보고 발생할 때 이러한 문제를 작업도 비교적 쉽습니다 하겠습니다.

## <a name="step-4-creating-the-nested-master-page"></a>4 단계: 중첩 된 마스터 페이지 만들기

이 첫 번째 작업의 관리 섹션에 있는 페이지에 사용할 중첩 된 마스터 페이지를 만드는 것입니다. 중첩 된 마스터 페이지를 추가 하는 경우 2 단계에서에서 설명한 것 처럼 중첩 된 마스터 페이지의 부모에 대 한 마스터 페이지를 지정 해야 합니다. 두 개의 최상위 마스터 페이지 했습니다: `Site.master` 및 `Alternate.master`합니다. 만든 회수 `Alternate.master` 이전 자습서에서의 코드를 작성 하 고는 `BasePage` Page 개체를 설정 하는 클래스 `MasterPageFile` 속성을 런타임에 `Site.master` 또는 `Alternate.master` 값에 따라는 `MyMasterPage` 세션 변수입니다.

구성 하려면 어떻게 우리는 중첩 된 마스터 페이지에 적절 한 최상위 마스터 페이지를 사용 하도록? 두 가지 옵션이 있습니다.

- 두 개의 중첩 된 마스터 페이지를 만들어 `AdminNestedSite.master` 및 `AdminNestedAlternate.master`, 최상위 마스터 페이지에 바인딩할 `Site.master` 및 `Alternate.master`각각. `BasePage`, 그런 다음 설정할 것는 `Page` 개체의 `MasterPageFile` 적절 한 중첩 된 마스터 페이지에 있습니다.
- 이 특정 마스터 페이지를 사용 하 여 콘텐츠 페이지를 있고 단일 중첩 된 마스터 페이지를 만듭니다. 그런 다음 런타임에 해야 한다는 의미는 중첩 된 마스터 페이지의 설정 `MasterPageFile` 런타임에 적절 한 최상위 마스터 페이지에는 속성입니다. (처럼 지금까지 알게 될 수 있습니다, 마스터 페이지도 가집니다는 `MasterPageFile` 속성입니다.)

두 번째 옵션을 사용 하겠습니다. 하나의 중첩 된 마스터 페이지 파일 만들기에 `~/Admin` 라는 폴더 `AdminNested.master`합니다. 때문에 둘 다 `Site.master` 및 `Alternate.master` 동일한 ContentPlaceHolder 컨트롤 집합을 확인해에 바인딩할 수 있지만 어떤 마스터 페이지에 바인딩합니다, 문제가 되지 않습니다 `Site.master` 일관성의 위해서입니다.


[![중첩 된 마스터 페이지 ~/Admin 폴더에 추가 합니다.](nested-master-pages-cs/_static/image26.png)](nested-master-pages-cs/_static/image25.png)

**그림 09**: 중첩 된 마스터 페이지를 추가 `~/Admin` 폴더입니다. ([전체 크기 이미지를 보려면 클릭](nested-master-pages-cs/_static/image27.png))


Visual Studio 4 개 추가 하는 중첩 된 마스터 페이지 4 개의 ContentPlaceHolder 컨트롤이 포함 된 마스터 페이지에 바인딩되므로 콘텐츠 컨트롤을 새 중첩 된 마스터 페이지 파일 초기 태그입니다. 2 단계와 3 단계를 ContentPlaceHolder 컨트롤 각 콘텐츠 컨트롤을 추가할 최상위 마스터 페이지의 ContentPlaceHolder 컨트롤로 동일한 이름을 지정 같이 합니다. 또한 다음 태그에 해당 하는 콘텐츠 컨트롤에 추가 된 `MainContent` ContentPlaceHolder:


[!code-html[Main](nested-master-pages-cs/samples/sample8.html)]

다음으로 정의 된 `instructions` CSS 클래스에 `Styles.css` 및 `AlternateStyles.css` CSS 파일입니다. 다음과 같은 CSS 규칙으로 인해으로 스타일이 지정 된 HTML 요소는 `instructions` 연한 노랑 배경색 및 검정, 단색 테두리와 함께 표시 되는 클래스:


[!code-css[Main](nested-master-pages-cs/samples/sample9.css)]

이 태그 중첩 된 마스터 페이지에 추가 되었으므로,이 중첩 된 마스터 페이지 (즉, 관리 섹션에서 페이지)를 사용 하는 해당 페이지에만 표시 됩니다.

중첩 된 마스터 페이지에 추가 하는이 코드를 변경한 후 해당 선언 태그 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](nested-master-pages-cs/samples/sample10.aspx)]

ContentPlaceHolder 컨트롤과 하는 각 콘텐츠 컨트롤에 ContentPlaceHolder 컨트롤의 `ID` 속성 같은 최상위 마스터 페이지에 있는 해당 ContentPlaceHolder 컨트롤 값이 할당 됩니다. 관리 섹션 관련 태그에 표시 되는 또한는 `MainContent` ContentPlaceHolder 합니다.

그림 10은는 `AdminNested.master` Visual Studio의 디자이너를 통해 볼 때 중첩 된 마스터 페이지입니다. 위쪽에 노란색 상자의 지침을 확인할 수 있습니다는 `MainContent` 콘텐츠 컨트롤을 합니다.


[![중첩 된 마스터 페이지를 최상위 마스터 페이지 관리자에 대 한 지침을 포함 하도록 확장 합니다.](nested-master-pages-cs/_static/image29.png)](nested-master-pages-cs/_static/image28.png)

**그림 10**: 중첩 된 마스터 페이지를 최상위 마스터 페이지 관리자에 대 한 지침을 포함 하도록 확장 합니다. ([전체 크기 이미지를 보려면 클릭](nested-master-pages-cs/_static/image30.png))


## <a name="step-5-updating-the-existing-content-pages-to-use-the-new-nested-master-page"></a>5 단계: 새 중첩 된 마스터 페이지를 사용 하도록 기존 콘텐츠 페이지를 업데이트 합니다.

새 콘텐츠 페이지를 바인딩해야 하 여 관리 섹션에 추가 하 고 언제 든 지는 `AdminNested.master` 방금 만든 마스터 페이지입니다. 하지만 콘텐츠 페이지는 기존 어떻습니까? 사이트의 모든 콘텐츠 페이지에서 파생 되는 현재는 `BasePage` 클래스를 프로그래밍 방식으로 런타임에 콘텐츠 페이지의 마스터 페이지를 설정 합니다. 콘텐츠 페이지의 관리 섹션에 대 한 결과가 아닙니다. 대신, 이러한 콘텐츠 페이지를 항상 사용 원하는 `AdminNested.master` 페이지. 런타임 시 오른쪽 최상위 콘텐츠 페이지를 선택 하려면 중첩 된 마스터 페이지에서 수행 됩니다.

얻을 수 있는 가장 좋은 방법은이 필요한 동작은 라는 새 기본 페이지를 사용자 지정 클래스를 만드는 것 `AdminBasePage` 확장 하 고 `BasePage` 클래스입니다. `AdminBasePage` 다음을 재정의할 수는 `SetMasterPageFile` 설정는 `Page` 개체의 `MasterPageFile` 하드 코드 된 값으로 "~ / Admin/AdminNested.master"입니다. 이러한 방식으로 모든 페이지에서 파생 된 `AdminBasePage` ´ ֲ `AdminNested.master`에서 파생 되는 모든 페이지에서는 `BasePage` 갖습니다 해당 `MasterPageFile` 속성 중 하나에 동적으로 설정 "~ / Site.master" 또는 "~ / Alternate.master"의 값에 따라는 `MyMasterPage` 세션 변수입니다.

새 클래스 파일을 추가 하 여 시작 된 `App_Code` 라는 폴더 `AdminBasePage.cs`합니다. 가 `AdminBasePage` 확장 `BasePage` 한 후 재정의 `SetMasterPageFile` 메서드. 해당 메서드의 할당은 `MasterPageFile` 값 "~ / Admin/AdminNested.master"입니다. 클래스에 이러한 변경을 수행한 후 파일에는 다음과 같아야 합니다.


[!code-csharp[Main](nested-master-pages-cs/samples/sample11.cs)]

이제 섹션에서 파생 되는 관리에서 기존 콘텐츠 페이지를 포함 하도록 해야 `AdminBasePage` 대신 `BasePage`합니다. 각 콘텐츠 페이지에 대 한 코드 숨김 클래스 파일로 이동 하는 `~/Admin` 폴더 이와 같이 변경 하 고 있습니다. 예를 들어 `~/Admin/Default.aspx` 에서 코드 숨김 클래스 선언을 변경 합니다.


[!code-csharp[Main](nested-master-pages-cs/samples/sample12.cs)]

대상:


[!code-csharp[Main](nested-master-pages-cs/samples/sample13.cs)]

그림 11 보여주고 어떻게 최상위 마스터 페이지 (`Site.master` 또는 `Alternate.master`), 중첩 된 마스터 페이지 (`AdminNested.master`), 관리 섹션 콘텐츠 페이지는 서로 관련이 및 합니다.


[![중첩 된 마스터 페이지의 관리 섹션에 있는 페이지에 콘텐츠 관련 정의](nested-master-pages-cs/_static/image32.png)](nested-master-pages-cs/_static/image31.png)

**그림 11**: The 중첩 된 마스터 페이지를 정의 콘텐츠 관련 관리 섹션에 있는 페이지 ([전체 크기 이미지를 보려면 클릭](nested-master-pages-cs/_static/image33.png))


## <a name="step-6-mirroring-the-master-pages-public-methods-and-properties"></a>6 단계: 미러링 마스터 페이지의 공용 메서드 및 속성

이전에 설명한 대로 `~/Admin/AddProduct.aspx` 및 `~/Admin/Products.aspx` 마스터 페이지와 페이지 프로그래밍 방식으로 상호 작용: `~/Admin/AddProduct.aspx` 호출 마스터 페이지의 공용 `RefreshRecentProductsGrid` 메서드 및 집합의 `GridMessageText` 속성 `~/Admin/Products.aspx` 에 대 한 이벤트 처리기가는 `PricesDoubled` 이벤트입니다. 추상 이전 자습서에서 만든 `BaseMasterPage` 이러한 공용 멤버를 정의 하는 클래스입니다.

`~/Admin/AddProduct.aspx` 및 `~/Admin/Products.aspx` 페이지의 마스터 페이지에서 파생 되었는지 가정은 `BaseMasterPage` 클래스입니다. 하지만 `AdminNested.master` 페이지, 현재 확장 된 `System.Web.UI.MasterPage` 클래스입니다. 결과적으로 방문할 때 `~/Admin/Products.aspx` 는 `InvalidCastException` 메시지와 함께 발생: "종류의 개체를 캐스팅할 수 없습니다. ' ASP.admin\_adminnested\_마스터 ' 'BaseMasterPage'를 입력 합니다."

있어야이 문제를 해결 하는 `AdminNested.master` 코드 숨김 클래스 확장 `BaseMasterPage`합니다. 중첩 된 마스터 페이지의 코드 숨김 클래스 선언에서 업데이트 합니다.


[!code-csharp[Main](nested-master-pages-cs/samples/sample14.cs)]

대상:


[!code-csharp[Main](nested-master-pages-cs/samples/sample15.cs)]

에서는 아직 완료 되지 않았습니다. 때문에 `BaseMasterPage` 클래스는 추상 클래스, 재정의 해야는 `abstract` 멤버 `RefreshRecentProductsGrid` 및 `GridMessageText`합니다. 이러한 멤버는 해당 사용자 인터페이스를 업데이트 하려면 최상위 마스터 페이지에서 사용 됩니다. (만 실제로 `Site.master` 마스터 페이지 최상위 마스터 페이지를 둘 다 모두 확장 하므로 이러한 메서드를 구현 하지만 이러한 방법을 사용 하 여 `BaseMasterPage`.)

이러한 멤버를 구현 해야 하는 동안 `AdminNested.master`, 이러한 구현 작업을 수행 하는 필요한 단순히 중첩 된 마스터 페이지에서 사용 하는 최상위 마스터 페이지에 동일한 멤버를 호출 합니다. 관리 섹션에서 해당 콘텐츠 페이지 중첩 된 마스터 페이지를 호출 하는 경우에 예를 들어, `RefreshRecentProductsGrid` 메서드, 중첩 된 마스터 페이지에서 작업을 수행 해야 하는 모든, 차례로, 호출 `Site.master` 또는 `Alternate.master`의 `RefreshRecentProductsGrid` 메서드.

이를 위해 다음을 추가 하 여 시작 `@MasterType` 지시문의 맨 위에 `AdminNested.master`:


[!code-aspx[Main](nested-master-pages-cs/samples/sample16.aspx)]

이전에 설명한 대로 `@MasterType` 라는 코드 숨김 클래스에는 강력한 형식의 속성을 추가 하는 지시문 `Master`합니다. 그런 다음 재정의 `RefreshRecentProductsGrid` 및 `GridMessageText` 멤버 단순히에 대 한 호출을 위임 하 고는 `Master`의 메서드를 해당:


[!code-csharp[Main](nested-master-pages-cs/samples/sample17.cs)]

이 코드가 방문 하 여 관리 섹션의 콘텐츠 페이지를 사용할 수 있습니다. 그림 12는 `~/Admin/Products.aspx` 브라우저를 통해 볼 때 페이지입니다. 볼 수 있듯이 페이지에는 중첩 된 마스터 페이지에 정의 된 관리 지침 상자를 포함 됩니다.


[![관리 섹션에서 콘텐츠 페이지에는 각 페이지 맨 위에 있는 지침 포함](nested-master-pages-cs/_static/image35.png)](nested-master-pages-cs/_static/image34.png)

**그림 12**: 각 페이지 위쪽에서 관리 섹션 포함 지침에 설명 된 The 콘텐츠 페이지 ([전체 크기 이미지를 보려면 클릭](nested-master-pages-cs/_static/image36.png))


## <a name="step-7-using-the-appropriate-top-level-master-page-at-runtime"></a>7 단계: 적절 한 최상위 마스터 페이지를 사용 하 여 런타임 시

관리 섹션에서 모든 콘텐츠 페이지는 완벽 하 게 작동 하지만, 모두 동일한 최상위 마스터 페이지를 사용 하며 마스터 페이지에서 사용자가 선택한 무시 `ChooseMasterPage.aspx`합니다. 이 동작은 때문를 중첩 된 마스터 페이지에 해당 `MasterPageFile` 속성이 정적으로로 설정 `Site.master` 에 해당 `<%@ Master %>` 지시문입니다.

공간을 최종 사용자가 선택한 최상위 마스터 페이지를 사용 하 여 `AdminNested.master`의 `MasterPageFile` 속성의 값을는 `MyMasterPage` 세션 변수입니다. 콘텐츠 페이지를 설정 하는 이유 때문에 `MasterPageFile` 속성에 `BasePage`, 중첩 된 마스터 페이지의 설정할 것 나타난다고 생각할 수 있습니다 `MasterPageFile` 속성 `BaseMasterPage` 또는 `AdminNested.master`의 코드 숨김 클래스입니다. 그러나이 작동 하지 않습니다,를 설정 하기 때문에 `MasterPageFile` PreInit 단계를 완료 하 여 속성입니다. 마스터 페이지의 페이지 수명 주기를 프로그래밍 방식으로 활용할 수 있습니다 하는 가장 빠른 시간은 (발생 하는 PreInit 단계 후) Init 단계로입니다.

따라서 중첩 된 마스터 페이지를 설정 해야 `MasterPageFile` 콘텐츠 페이지의 속성입니다. 전용 콘텐츠 사용 하는 페이지는 `AdminNested.master` 마스터 페이지에서 파생 `AdminBasePage`합니다. 따라서 있습니다이 논리를 넣을 수 있습니다. 가에서는 5 단계에서에서는 `SetMasterPageFile` 설정 메서드는 `Page` 개체의 `MasterPageFile` 속성을 "~ / Admin/AdminNested.master"입니다. 업데이트 `SetMasterPageFile` 마스터 페이지의 설정 `MasterPageFile` 세션에 저장 된 결과에 속성:


[!code-csharp[Main](nested-master-pages-cs/samples/sample18.cs)]

`GetMasterPageFileFromSession` 에 추가한 메서드는 `BasePage` 클래스 이전 자습서에서는 적절 한 마스터 페이지 파일 경로 기반 세션 변수 값으로 반환 합니다.

위치에이 변경으로 인해 사용자의 마스터 페이지 선택을 통해 관리 섹션에 전달합니다. 그림 13 그림 12 동일 하지만 사용자가 자신의 마스터 페이지 선택 영역을 변경한 후 같은 페이지를 보여 줍니다. `Alternate.master`합니다.


[![사용자가 선택한 최상위 마스터 페이지를 사용 하는 중첩 된 관리 페이지](nested-master-pages-cs/_static/image38.png)](nested-master-pages-cs/_static/image37.png)

**그림 13**: Nested 관리 페이지를 사용 하는 사용자가 최상위 마스터 페이지 선택 ([전체 크기 이미지를 보려면 클릭](nested-master-pages-cs/_static/image39.png))


## <a name="summary"></a>요약

많은 like 어떻게 콘텐츠 페이지는 마스터 페이지에 바인딩할 수, 중첩을 만들 수는 자식 마스터 페이지를 사용 함으로써 마스터 페이지 상위 마스터 페이지에 바인딩합니다. 자식 마스터 페이지는 각 해당 부모의 contentplaceholders의;에 대 한 콘텐츠 컨트롤을 정의할 수 있습니다. 콘텐츠를 콘텐츠 컨트롤을 다음 자체 ContentPlaceHolder 컨트롤이 (뿐만 아니라 다른 태그)를 추가할 수 있습니다. 중첩 된 마스터 페이지는 있는 모든 페이지는 가장 중요 한 디자인을 공유 아직 고유한 사용자 지정 항목을 요구 하는 사이트의 특정 섹션 대형 웹 응용 프로그램에서 매우 유용 합니다.

만족도 매우 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [중첩 된 ASP.NET 마스터 페이지](https://msdn.microsoft.com/library/x2b3ktt7.aspx)
- [중첩 된 마스터 페이지 및 VS 2005 디자인 타임에 대 한 팁](https://weblogs.asp.net/scottgu/archive/2005/11/11/430382.aspx)
- [VS 2008 중첩 마스터 페이지 지원](https://weblogs.asp.net/scottgu/archive/2007/07/09/vs-2008-nested-master-page-support.aspx)

### <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 작성자 여러 ASP/ASP.NET 설명서와 4GuysFromRolla.com의 창립자의 근무 기간이 Microsoft 웹 기술을 1998 이후입니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 3.5 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)합니다. Scott에 도달할 수 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com) 또는에서 그의 블로그 통해 [ http://ScottOnWriting.NET ](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](specifying-the-master-page-programmatically-cs.md)
> [다음](creating-a-site-wide-layout-using-master-pages-vb.md)
