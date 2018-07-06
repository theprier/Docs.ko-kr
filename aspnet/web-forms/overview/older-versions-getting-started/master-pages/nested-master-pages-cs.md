---
uid: web-forms/overview/older-versions-getting-started/master-pages/nested-master-pages-cs
title: 중첩 마스터 페이지 (C#) | Microsoft Docs
author: rick-anderson
description: 다른 내에서 하나의 마스터 페이지를 중첩 하는 방법을 보여 줍니다.
ms.author: aspnetcontent
ms.date: 07/28/2008
ms.assetid: 32b7fb6e-d74b-4048-91f8-70631b2523ee
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/nested-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: 71cefa603d1b54e8dbbeb0f6e7e3ef8e0c0a93f8
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37840647"
---
<a name="nested-master-pages-c"></a>중첩된 마스터 페이지 (C#)
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/d/6/6/d66ad554-afdd-409e-a5c3-201b774fbb31/ASPNET_MasterPages_Tutorial_10_CS.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/d/6/6/d66ad554-afdd-409e-a5c3-201b774fbb31/ASPNET_MasterPages_Tutorial_10_CS.pdf)

> 다른 내에서 하나의 마스터 페이지를 중첩 하는 방법을 보여 줍니다.


## <a name="introduction"></a>소개

지난 9 자습서에 걸쳐 마스터 페이지를 사용 하 여 사이트 전체 레이아웃을 구현 하는 방법을 살펴보았습니다. 간단히 말해 마스터 페이지를 사용, 우리 페이지 개발자는 마스터 페이지 콘텐츠 페이지에서 콘텐츠 페이지 별로 사용자 지정할 수 있는 특정 지역에서에서 일반적인 태그를 정의 합니다. 마스터 페이지에 ContentPlaceHolder 컨트롤 표시를 사용자 지정할 수 있는 지역을 선택 합니다. ContentPlaceHolder 컨트롤에 대 한 사용자 지정 된 태그는 콘텐츠 컨트롤을 통해 콘텐츠 페이지에 정의 됩니다.

사이트 전체에서 사용 되는 단일 레이아웃이 있을 경우 지금 살펴보았습니다 마스터 페이지 기술을 탁월 합니다. 그러나 많은 대규모 웹 사이트 사용자 지정 된 사이트 레이아웃을 다양 한 섹션이 있습니다. 예를 들어 병원 직원이 환자 정보, 활동 및 청구를 관리 하는 데 사용 하는 의료 응용 프로그램을 고려 합니다. 이 응용 프로그램에서 웹 페이지의 세 가지 유형의 있을 수 있습니다.

- 직원 멤버 관련 페이지 직원 가용성을 업데이트할 수 있는 일정을 보거나 휴가 요청 합니다.
- 직원 보거나 특정 환자에 대 한 정보를 편집 합니다. 여기서는 환자가 특정 페이지입니다.
- Accountants 검토할 현재 있는 청구 관련 페이지에는 상태 및 재무 보고서 클레임입니다.

모든 페이지에 위쪽 및 아래쪽 자주 사용 되는 링크의 시리즈 메뉴와 같은 일반적인 레이아웃을 공유할 수 있습니다. 하지만 직원, 환자 및 대금 청구 관련 페이지를이 일반적인 레이아웃을 사용자 지정 해야 합니다. 예를 들어, 아마도 모든 직원이 관련 페이지에는 현재 로그온된 한 사용자의 가용성 및 일별 일정을 표시 하는 일정 및 작업의 목록을 포함 해야 합니다. 아마도 모든 환자 특정 페이지 이름, 주소 및 해당 정보를 편집 하 고는 환자에 대 한 보험 정보를 표시 해야 합니다.

사용 하 여 이러한 사용자 지정된 레이아웃을 만들 수 있기 *중첩 된 마스터 페이지*합니다. 위의 시나리오를 구현 하려면 ContentPlaceHolders 사용자 지정할 수 있는 지역 정의 사용 하 여 사이트 전체 레이아웃, 메뉴 및 바닥글 콘텐츠를 정의 하는 마스터 페이지를 만들어 시작 했습니다. 에서는 다음 세 개의 중첩 된 마스터 페이지, 웹 페이지의 각 형식에 대 한 하나 만듭니다. 각 중첩 된 마스터 페이지는 마스터 페이지를 사용 하는 콘텐츠 페이지의 형식 간에 콘텐츠를 정의 합니다. 즉, 태그 및 편집 하 고 환자에 대 한 정보를 표시 하기 위한 논리를 프로그래밍 방식으로 환자의 특정 콘텐츠 페이지에 대 한 중첩 된 마스터 페이지 포함 됩니다. 새 환자 관련 페이지를 만들 때에이 중첩 된 마스터 페이지에 바인딩하는 것 했습니다.

이 자습서는 중첩 된 마스터 페이지의 이점을 강조 표시 하 여 시작 합니다. 그런 다음 만들고 중첩된 마스터 페이지를 사용 하는 방법을 보여 줍니다.

> [!NOTE]
> 중첩된 마스터 페이지의.NET Framework 버전 2.0부터 불가능 했입니다. 그러나 Visual Studio 2005는 중첩 된 마스터 페이지에 대 한 디자인 타임 지원은 포함 되지 않았습니다. 좋은 소식은 Visual Studio 2008 중첩된 마스터 페이지는 다양 한 디자인 타임 환경을 제공 하는 것입니다. 중첩된 마스터 페이지를 사용 하 여 관심 있는 해도 Visual Studio 2005를 여전히 사용 하는 경우 체크 아웃 [Scott Guthrie](https://weblogs.asp.net/scottgu/)의 블로그 항목 [VS 2005 디자인 타임에 중첩 된 마스터 페이지에 대 한 팁](https://weblogs.asp.net/scottgu/archive/2005/11/11/430382.aspx)합니다.


## <a name="the-benefits-of-nested-master-pages"></a>중첩된 마스터 페이지의 이점

많은 웹 사이트 페이지의 특정 형식에 특정 사용자 지정된 디자인 더 뿐만 아니라 사이트 디자인을 가장 중요 한 경우 예를 들어 데모 웹 응용 프로그램에서 만들었습니다 기본적인 관리 섹션 (페이지는 `~/Admin` 폴더). 현재 웹 페이지에는 `~/Admin` 관리 섹션에 없는 해당 페이지와 같은 마스터 페이지를 사용 하는 폴더 (즉, `Site.master` 또는 `Alternate.master`사용자의 선택에 따라).

> [!NOTE]
> 이제 사이트 하나만 마스터 페이지에 잠깐 동안 `Site.master`합니다. "를 사용 하는 중첩 마스터 페이지에 대 한의 관리 섹션"을 사용 하 여 시작 하는 두 개 (이상) 마스터 페이지를 사용 하 여 중첩 된 마스터 페이지를 사용 하 여이 자습서의 뒷부분에서 다루겠습니다.


추가 정보 또는 그렇지 않은 경우 수 없는 사이트에서 다른 페이지에 있는 링크를 포함 하도록 관리 페이지의 레이아웃을 사용자 지정 요청을 받았습니다를 가정해 보겠습니다. 이 요구 사항을 구현 하는 다음과 같은 네 가지 기술이 있습니다.

1. 모든 콘텐츠 페이지에 관리 관련 정보 및 링크를 수동으로 추가 된 `~/Admin` 폴더입니다.
2. 업데이트 된 `Site.master` 관리 섹션에서는 관련 정보 및 링크를 포함 하 여 코드를 표시 하거나 숨기려면이 섹션에서는 마스터 페이지를 추가 하는 마스터 페이지 중 관리 페이지를 방문 하는 여부에 따라 합니다.
3. 마스터 페이지를 새로 만들려면 관리 섹션을 위해 특별히에서 태그를 복사 `Site.master`관리 섹션에서는 관련 정보 및 링크를 추가 하 고 콘텐츠 페이지에 업데이트를 `~/Admin` 이 새 마스터를 사용 하는 폴더 페이지입니다.
4. 바인딩되는 중첩된 마스터 페이지를 만듭니다 `Site.master` 콘텐츠 페이지에 및를 `~/Admin` 마스터 페이지를 중첩 하는 새 폴더 사용 합니다. 이 중첩된 마스터 페이지 추가 정보 및 특정 관리 페이지에 대 한 링크는 및에 이미 정의 된 태그를 반복 해야 `Site.master`합니다.

첫 번째 옵션은 최소 마음에 들지 않는 경우 마스터 페이지를 사용 하 여 전체 점은을 수동으로 복사 하 고 일반적인 태그 새 ASP.NET 페이지에 붙여 넣습니다. 두 번째 옵션은 사용할 수 있지만 응용 프로그램을 줄이려면 대로 해당 관계식을 추가 하려면 개발자는 마스터 페이지를 편집이 태그를 해결 하려면 한 시기에 기억해 야 하며 가끔씩만 표시 되는 태그를 사용 하 여 마스터 페이지를 사용 하면 정확 하 게 숨긴 경우 특정 태그 및 표시 됩니다. 이 방법은 점점 더 많은 유형의이 단일 마스터 페이지를 수용할 수 하는 데 필요한 웹 페이지에서 사용자 지정으로 작은 해 것입니다.

세 번째 옵션은 혼잡 함을 제거 및 두 번째 옵션을 사용 하 여 복잡성 문제를 표시 합니다. 그러나 옵션 3의 주요 단점은 복사 및 붙여넣기에서 일반적인 레이아웃을 필요 하다는 점 `Site.master` 새 관리 섹션 별 마스터 페이지입니다. 에서는 나중에 사이트 전체 레이아웃을 변경 하려면 두 위치에서 변경 해야 했습니다.

네 번째 옵션을 중첩 마스터 페이지의 두 번째 및 세 번째 옵션을 제공 합니다. 사이트 전체 레이아웃 정보를 특정 지역에 특정 콘텐츠를 다른 파일에 분산 되어 있지만 하나의 최상위 마스터 페이지 파일에 유지 됩니다.

이 자습서를 살펴보고 만들고 간단한 중첩된 마스터 페이지를 사용 하 여 시작 합니다. 에서는 새로운 최상위 마스터 페이지, 두 개의 중첩 된 마스터 페이지 및 두 개의 콘텐츠 페이지를 만듭니다. 중첩된 마스터 페이지의 사용을 포함 하도록 기존 마스터 페이지 아키텍처에 업데이트를 "를 사용 하는 중첩 마스터 페이지에 대 한의 관리 섹션"부터 살펴보겠습니다. 특히, 중첩된 된 마스터 페이지를 생성 하 고 콘텐츠 페이지의 추가 사용자 지정 콘텐츠를 포함 하는 데 사용할는 `~/Admin` 폴더입니다.

## <a name="step-1-creating-a-simple-top-level-master-page"></a>1 단계: 간단한 최상위 마스터 페이지 만들기

중첩 된 마스터 만들기 하나를 기반으로 기존 마스터 페이지 및 기존 콘텐츠 페이지에 특정 항목을 이미 예상 하기 때문에 일부 복잡성을 수반를 업데이트 하는 최상위 마스터 페이지 대신이 새로운 중첩된 마스터 페이지를 사용 하도록 기존 콘텐츠 페이지 Contentplaceholder 최상위 마스터에서 페이지를 정의 합니다. 따라서 중첩된 마스터 페이지는 같은 이름의 동일한 ContentPlaceHolder 컨트롤 포함도 해야 합니다. 또한 특정 데모 응용 프로그램에 두 마스터 페이지 (`Site.master` 고 `Alternate.master`)이이 복잡성을 더 추가 하는 사용자의 기본 설정에 따라 콘텐츠 페이지에 동적으로 할당 되는 합니다. 이 자습서의 뒷부분에서 중첩 된 마스터 페이지를 사용 하 여 기존 응용 프로그램 업데이트 살펴보겠습니다 있지만 보겠습니다 간단한 첫 번째 포커스 중첩 마스터 페이지 예제.

라는 새 폴더를 만듭니다 `NestedMasterPages` 라는 해당 폴더에 새 마스터 페이지 파일을 추가한 `Simple.master`합니다. (그림 1 참조 솔루션 탐색기의 스크린 샷을 대 한이 폴더 및 파일 추가 된 후). 끌어서는 `AlternateStyles.css` 디자이너 솔루션 탐색기에서 스타일 시트 파일입니다. 이 추가 `<link>` 스타일 시트 파일에 요소를 `<head>` 요소 뒤 마스터 페이지의 `<head>` 요소의 태그와 같습니다:


[!code-aspx[Main](nested-master-pages-cs/samples/sample1.aspx)]

그런 다음의 웹 폼 내에서 다음 태그를 추가 `Simple.master`:


[!code-aspx[Main](nested-master-pages-cs/samples/sample2.aspx)]

이 태그는 남색 배경 기반 흰색 큰 글꼴로 페이지의 맨 위에 있는 "중첩 마스터 페이지 (단순)" 라는 링크를 표시 합니다. 아래에 `MainContent` ContentPlaceHolder 합니다. 그림 1은 `Simple.master` Visual Studio 디자이너에 로드 된 경우 마스터 페이지입니다.


[![중첩 된 마스터 페이지의 관리 섹션의 페이지에 콘텐츠 관련 정의](nested-master-pages-cs/_static/image2.png)](nested-master-pages-cs/_static/image1.png)

**그림 01**: The 중첩 마스터 페이지 정의 콘텐츠 관련 관리 섹션의 페이지 ([큰 이미지를 보려면 클릭](nested-master-pages-cs/_static/image3.png))


## <a name="step-2-creating-a-simple-nested-master-page"></a>2 단계: 간단한 중첩된 마스터 페이지 만들기

`Simple.master` 두 ContentPlaceHolder 컨트롤이 포함 되어 있습니다:는 `MainContent` 와 함께 Web Form 내에서 추가한 ContentPlaceHolder를 `head` 에 ContentPlaceHolder를 `<head>` 요소. 콘텐츠 페이지를 만들고에 바인딩할 경우 `Simple.master` 콘텐츠 페이지에는 두 콘텐츠 컨트롤을 두 ContentPlaceHolders 참조 해야 합니다. 마찬가지로, 경우 중첩 된 마스터 페이지를 만들고에 바인딩할 `Simple.master` 중첩된 마스터 페이지는 두 콘텐츠 컨트롤을 합니다.

새 중첩된 마스터 페이지를 추가 해 보겠습니다 합니다 `NestedMasterPages` 라는 폴더 `SimpleNested.master`합니다. 마우스 오른쪽 단추로 클릭는 `NestedMasterPages` 폴더 새 항목 추가 선택 합니다. 그러면 그림 2에 표시 된 새 항목 추가 대화 상자. 마스터 페이지 템플릿 유형 및 새 마스터 페이지 이름을 입력을 선택 합니다. 새 마스터 페이지가 중첩된 된 마스터 페이지를 함을 나타내려면 "마스터 페이지 선택" 확인란을 선택 합니다.

추가 단추를 클릭 합니다. 동일한 Select 마스터 페이지 콘텐츠 페이지를 바인딩할 때 마스터 페이지 대화 상자를 표시 됩니다 (그림 3 참조). 선택는 `Simple.master` 에서 마스터 페이지는 `NestedMasterPages` 폴더 확인을 클릭 합니다.

> [!NOTE]
> 웹 응용 프로그램 프로젝트 모델을 사용 하 여 웹 사이트 프로젝트 모델 대신 ASP.NET 웹 사이트를 만든 경우에 그림 2에 표시 된 새 항목 추가 대화 상자에서 확인란을 "마스터 페이지 선택"이 표시 되지 않습니다. 웹 응용 프로그램 프로젝트 모델을 사용 하는 경우 중첩된 된 마스터 페이지를 만들려면 (마스터 페이지 템플릿) 대신 중첩 마스터 페이지 템플릿을 선택 해야 합니다. 중첩 된 마스터 페이지 템플릿을 선택한 후 추가 클릭 하 그림 3 에서처럼 대화 상자가 나타납니다. 마스터 페이지 선택 동일 합니다.


[![확인 합니다 &quot;마스터 페이지 선택&quot; 중첩 마스터 페이지를 추가 하려면이 확인란을](nested-master-pages-cs/_static/image5.png)](nested-master-pages-cs/_static/image4.png)

**그림 02**: 중첩 마스터 페이지를 추가 하려면 "마스터 페이지 선택"을 확인란 ([큰 이미지를 보려면 클릭](nested-master-pages-cs/_static/image6.png))


[![중첩 된 마스터 페이지 Simple.master 마스터 페이지에 바인딩](nested-master-pages-cs/_static/image8.png)](nested-master-pages-cs/_static/image7.png)

**그림 03**: 중첩 마스터 페이지를 바인딩하는 `Simple.master` 마스터 페이지 ([클릭 하 여 큰 이미지 보기](nested-master-pages-cs/_static/image9.png))


중첩된 마스터 페이지의 선언적 태그를 아래에 나와 있는 두 콘텐츠 컨트롤을 최상위 마스터 페이지의 두 ContentPlaceHolder 컨트롤 참조를 포함 합니다.


[!code-aspx[Main](nested-master-pages-cs/samples/sample3.aspx)]

제외 하 고는 `<%@ Master %>` 지시문에 중첩 된 마스터 페이지의 초기 선언적 태그는 동일한 최상위 마스터 페이지 콘텐츠 페이지에 바인딩할 때 처음에 생성 되는 태그와 동일 합니다. 콘텐츠 페이지와 같은 `<%@ Page %>` 지시문을는 `<%@ Master %>` 지시문을 여기에 포함 됩니다는 `MasterPageFile` 중첩된 마스터 페이지의 부모 마스터 페이지를 지정 하는 특성입니다. 중첩된 마스터 페이지와 같은 최상위 마스터 페이지에 바인딩된 콘텐츠 페이지 간의 주요 차이점은 중첩 된 마스터 페이지 contentplaceholder를 포함할 수 있습니다. 중첩된 마스터 페이지의 ContentPlaceHolder 컨트롤 콘텐츠 페이지 태그를 사용자 지정할 수 있는 영역을 정의 합니다.

"Hello, from SimpleNested!" 텍스트가 표시 되도록이 중첩 된 마스터 페이지 업데이트 에 해당 하는 콘텐츠 컨트롤에는 `MainContent` 각각의 ContentPlaceHolder 컨트롤로 합니다.


[!code-aspx[Main](nested-master-pages-cs/samples/sample4.aspx)]

이 추가 마치면 중첩된 마스터 페이지를 저장 하 고 새 콘텐츠 페이지를 추가 합니다 `NestedMasterPages` 라는 폴더 `Default.aspx`에 바인딩할는 `SimpleNested.master` 마스터 페이지입니다. 이 페이지를 추가 하면 (그림 4 참조) 콘텐츠 컨트롤이 포함 되어 있는지 확인할 수 있습니다. 콘텐츠 페이지에만 액세스할 수 해당 *부모* 페이지의 ContentPlaceHolders를 마스터 합니다. `SimpleNested.master` ContentPlaceHolder 컨트롤이; 들어 있지 않습니다. 따라서이 마스터 페이지에 바인딩된 모든 콘텐츠 페이지는 모든 콘텐츠 컨트롤을 포함할 수 없습니다.


[![새 콘텐츠 페이지에 콘텐츠 컨트롤이 없는](nested-master-pages-cs/_static/image11.png)](nested-master-pages-cs/_static/image10.png)

**그림 04**:의 새 콘텐츠 페이지 포함 아니요 콘텐츠 컨트롤 ([큰 이미지를 보려면 클릭](nested-master-pages-cs/_static/image12.png))


중첩된 마스터 페이지를 업데이트 하는 위해 필요한 것은 (`SimpleNested.master`) contentplaceholder를 포함 합니다. 일반적으로 필요 하다는 ContentPlaceHolder 해당 부모 마스터 페이지에서 정의한 각 ContentPlaceHolder 있기 때문에 해당 자식 마스터 페이지나 콘텐츠 페이지에는 최상위 마스터 페이지의 ContentPlaceHolder를 사용 하 여 작업을 포함 하려면 중첩 된 마스터 페이지 컨트롤입니다.

업데이트 된 `SimpleNested.master` 해당 두 콘텐츠 컨트롤에 ContentPlaceHolder를 포함할 마스터 페이지입니다. ContentPlaceHolder 컨트롤을 해당 콘텐츠 컨트롤을 가리킵니다 ContentPlaceHolder 컨트롤로 같은 이름을 지정 합니다. 이라는 ContentPlaceHolder 컨트롤을 추가 `MainContent` 에서 콘텐츠를 제어할 `SimpleNested.master` 를 참조 하는 합니다 `MainContent` 에 ContentPlaceHolder `Simple.master`합니다. 참조 하는 콘텐츠 컨트롤에 동일한 작업을 수행 합니다 `head` ContentPlaceHolder 합니다.

> [!NOTE]
> 중첩된 마스터 페이지의 ContentPlaceHolder 컨트롤을 최상위 마스터 페이지에서 ContentPlaceHolders 동일 명명을 권장 하는 동안에이 명명 대칭 필요 하지 않습니다. 지정할 수 있습니다 ContentPlaceHolder 컨트롤 중첩된 마스터 페이지에서 원하는 어떤 이름도. 그러나 찾습니까 ContentPlaceHolders 협력 기억 하기 쉬운 내 최상위 마스터 페이지 및 중첩 된 마스터 페이지에 동일한 이름을 사용 하는 경우 페이지의 어떤 지역입니다.


이러한 추가 기능을 적용 한 후에 `SimpleNested.master` 마스터 페이지의 선언적 태그는 다음과 유사 합니다.


[!code-aspx[Main](nested-master-pages-cs/samples/sample5.aspx)]

삭제 합니다 `Default.aspx` 방금 만든 페이지 콘텐츠 및 다시 추가한 후에 바인딩하지는 `SimpleNested.master` 마스터 페이지입니다. 이 이번 Visual Studio 추가 두 콘텐츠 컨트롤을 `Default.aspx`에 정의 된 이제는 ContentPlaceHolders 참조 `SimpleNested.master` (그림 6 참조). "Default.aspx에서: Hello!" 텍스트를 추가 합니다. 참조 되는 콘텐츠 제어 `MainContent`입니다.

그림 5에서 관련 된 세 가지 엔터티를 보여 줍니다 `Simple.master`, `SimpleNested.master`, 및 `Default.aspx` -와 서로 관계입니다. 다이어그램에서 알 수 있듯이, 중첩된 마스터 페이지는 해당 부모의 ContentPlaceHolder를 콘텐츠 컨트롤을 구현 합니다. 콘텐츠 페이지에 액세스할 수 있도록 이러한 지역의 경우 중첩 된 마스터 페이지를 사용 하 여 자체 ContentPlaceHolders 콘텐츠 컨트롤에 추가 해야 합니다.


[![최상위 및 중첩 된 마스터 페이지 콘텐츠 페이지의 레이아웃 지정](nested-master-pages-cs/_static/image14.png)](nested-master-pages-cs/_static/image13.png)

**그림 05**: 최상위 및 중첩 된 마스터 페이지 콘텐츠 페이지의 레이아웃을 결정 ([큰 이미지를 보려면 클릭](nested-master-pages-cs/_static/image15.png))


이 동작은 콘텐츠 페이지 또는 마스터 페이지는 해당 부모 마스터 페이지에 인식 에서만 하는 방법을 보여 줍니다. 이 동작은 Visual Studio 디자이너에도 표시 됩니다. 그림 6에 대 한 디자이너를 보여 줍니다. `Default.aspx`합니다. 디자이너를 명확 하 게를 표시 하지만 일부 되지 않습니다 및 콘텐츠 페이지에서 편집할 수 있는 지역은 어디 인가요 명령이 중첩된 마스터 페이지에서 편집할 수 없는 지역 이란 무엇 이며 최상위 마스터 페이지의 영역을 명확히 구분 하지 않습니다.


[![콘텐츠 페이지 이제 ContentPlaceHolders 중첩 된 마스터 페이지에 대 한 콘텐츠 컨트롤을 포함](nested-master-pages-cs/_static/image17.png)](nested-master-pages-cs/_static/image16.png)

**그림 06**: The 콘텐츠 페이지 이제 포함 콘텐츠 컨트롤에 중첩 된 마스터 페이지의 ContentPlaceHolders ([큰 이미지를 보려면 클릭](nested-master-pages-cs/_static/image18.png))


## <a name="step-3-adding-a-second-simple-nested-master-page"></a>3 단계: 두 번째 간단한 중첩된 마스터 페이지 추가

여러 마스터 페이지를 중첩 하는 경우 중첩 된 마스터 페이지의 장점은 더 분명 하 게 합니다. 이 혜택을 설명 하기 위해 만들려면 또 다른 중첩 된 마스터 페이지에는 `NestedMasterPages` 폴더; 이름 새로 추가 된이 중첩 마스터 페이지 `SimpleNestedAlternate.master` 에 바인딩할는 `Simple.master` 마스터 페이지입니다. 2 단계에서에서 수행한 것 처럼 중첩 된 마스터 페이지의 두 콘텐츠 컨트롤에 contentplaceholder를 추가 합니다. "Hello, from SimpleNestedAlternate!" 라는 텍스트를 추가 최상위 마스터 페이지에 해당 하는 콘텐츠 컨트롤의 `MainContent` ContentPlaceHolder 합니다. 이러한 변경을 수행한 후 새 중첩된 마스터 페이지의 선언적 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](nested-master-pages-cs/samples/sample6.aspx)]

명명 된 콘텐츠 페이지를 만들 `Alternate.aspx` 에 `NestedMasterPages` 폴더에 바인딩할는 `SimpleNestedAlternate.master` 중첩된 마스터 페이지. "대체에서: Hello!" 텍스트를 추가 합니다. 에 해당 하는 콘텐츠 컨트롤의 `MainContent`합니다. 그림 7은 `Alternate.aspx` Visual Studio 디자이너를 통해 볼 때.


[![Alternate.aspx는 SimpleNestedAlternate.master 마스터 페이지에 바인딩되어](nested-master-pages-cs/_static/image20.png)](nested-master-pages-cs/_static/image19.png)

**그림 07**: `Alternate.aspx` 바인딩되는 `SimpleNestedAlternate.master` 마스터 페이지 ([클릭 하 여 큰 이미지 보기](nested-master-pages-cs/_static/image21.png))


그림 7 그림 6의 디자이너에서에서 디자이너를 비교 합니다. 최상위 마스터 페이지에 정의 된 동일한 레이아웃을 공유 하는 두 콘텐츠 페이지 (`Simple.master`), 즉 "중첩 마스터 페이지 자습서 (단순)" 제목입니다. 고유한 콘텐츠 부모 마스터 페이지-에 정의 된 "Hello, from SimpleNested!" 텍스트 둘 다 아직 그림 6에 "Hello, from SimpleNestedAlternate!" 그림 7. 사실 여기 이러한 차이 사소한 있지만이 예제에서는 좀 더 의미 있는 차이점을 포함 하도록 확장할 수 있습니다. 예를 들어 합니다 `SimpleNested.master` 반면 페이지에서 해당 콘텐츠 페이지에 관련 된 옵션을 사용 하 여 메뉴를 포함 될 수 있습니다 `SimpleNestedAlternate.master` 정보에 바인딩되는 콘텐츠 페이지와 관련이 있을 수 있습니다.

이제 가장 중요 한 사이트 레이아웃을 변경 해야 한다고 가정 합니다. 예를 들어, 모든 콘텐츠 페이지에 일반 연결의 목록을 추가 하 려 한다고 가정 합니다. 최상위 마스터 페이지를 업데이트 하는 것이 위해 `Simple.master`합니다. 중첩된 마스터 페이지에서 더 나아가 해당 콘텐츠 페이지에 바로 모든 변경 사항이 반영 됩니다.

에서는 가장 중요 한 사이트 레이아웃을 변경할 수 있는 간편 하 게를 보여 주기 위해 엽니다는 `Simple.master` 마스터 페이지 및 사이 다음 태그를 추가 합니다 `topContent` 및 `mainContent` `<div>` 요소:


[!code-aspx[Main](nested-master-pages-cs/samples/sample7.aspx)]

바인딩되는 모든 페이지의 맨 위에 두 개의 링크 추가 `Simple.master`, `SimpleNested.master`, 또는 `SimpleNestedAlternate.master`; 모든 중첩 된 마스터 페이지 및 해당 콘텐츠 페이지에 이러한 변경 내용은 즉시 적용 됩니다. 그림 8 나와 `Alternate.aspx` 브라우저를 통해 볼 때. Note (그림 7에 비해) 페이지의 맨 위에 있는 링크를 추가 합니다.


[![해당 중첩 마스터 페이지 및 해당 콘텐츠 페이지에 즉시 반영 됩니다 최상위 마스터 페이지를 변경 합니다.](nested-master-pages-cs/_static/image23.png)](nested-master-pages-cs/_static/image22.png)

**그림 08**: 해당 중첩 마스터 페이지 및 해당 콘텐츠 페이지에 즉시 반영 됩니다 최상위 마스터 페이지를 변경 ([큰 이미지를 보려면 클릭](nested-master-pages-cs/_static/image24.png))


## <a name="using-a-nested-master-page-for-the-administration-section"></a>중첩된 마스터 페이지를 사용 하 여 관리 섹션

이 시점에 살펴본 중첩 된 마스터의 장점을 페이지 하 고 만들고 ASP.NET 응용 프로그램에서 사용 하는 방법을 살펴보았습니다. 그러나 1, 2 및 3 단계에서 예제는 새 최상위 마스터 페이지, 새 중첩된 마스터 페이지 및 새 콘텐츠 페이지를 만드는 관여 합니다. 새 중첩된 마스터 페이지를 웹 사이트를 기존 최상위 마스터 페이지를 사용 하 여 및 콘텐츠 페이지 추가 어떨까요?

기존 웹 사이트에 중첩된 된 마스터 페이지를 통합 하 고 기존 콘텐츠 페이지를 사용 하 여 연결부터 시작 하는 보다 약간 더 많은 노력이 필요 합니다. 4, 5, 6 및 7 단계 라는 새 중첩된 마스터 페이지를 포함 하도록 데모 응용 프로그램을 살펴보면서으로 이러한 문제를 탐색 `AdminNested.master` 관리자에 대 한 지침을 포함 하 고 ASP.NET 페이지에서 사용 되는 `~/Admin` 폴더입니다.

데모 응용 프로그램에 중첩된 된 마스터 페이지를 통합 다음 단점을 제공 합니다.

- 기존 콘텐츠 페이지에 `~/Admin` 폴더는 해당 마스터 페이지에서 특정 기대 합니다. 먼저 있어야 특정 ContentPlaceHolder 컨트롤 기대 합니다. 또한 합니다 `~/Admin/AddProduct.aspx` 및 `~/Admin/Products.aspx` 페이지 호출 마스터 페이지의 공용 `RefreshRecentProductsGrid` 메서드를 설정 해당 `GridMessageText` 속성에 대 한 이벤트 처리기 또는 해당 `PricesDoubled` 이벤트입니다. 따라서 중첩된 마스터 페이지는 동일한 ContentPlaceHolders 및 공용 멤버를 제공 해야 합니다.
- 이전 자습서에서 개선 되었습니다 합니다 `BasePage` 동적으로 설정 하는 클래스를 `Page` 개체의 `MasterPageFile` 세션 변수를 기반으로 속성입니다. 에 지원 방식 동적 마스터 페이지 중첩된 마스터 페이지를 사용 하는 경우?

이러한 두 가지 문제를 중첩된 마스터 페이지를 작성 하 고 기존 콘텐츠 페이지에서 사용 하는 대로 노출 됩니다. 조사 하 고 발생 하면 이러한 문제를 작업도 비교적 쉽습니다 됩니다.

## <a name="step-4-creating-the-nested-master-page"></a>4 단계: 중첩 된 마스터 페이지 만들기

우리의 첫 번째 작업의 관리 섹션의 페이지에서 사용할 중첩된 마스터 페이지를 만드는 것입니다. 중첩 된 마스터 페이지를 새로 추가 하는 경우 2 단계에서에서 설명한 것 처럼 중첩 된 마스터 페이지의 부모 마스터 페이지를 지정 해야 합니다. 두 개의 최상위 마스터 페이지를 했습니다: `Site.master` 및 `Alternate.master`합니다. 만든 회수 `Alternate.master` 이전 자습서에서에서 코드를 작성 하 고는 `BasePage` Page 개체를 설정 하는 클래스 `MasterPageFile` 속성을 런타임에 `Site.master` 또는 `Alternate.master` 값에 따라는 `MyMasterPage` 세션 변수입니다.

구성 하려면 어떻게에서는 중첩 된 마스터 페이지를 해당 최상위 마스터 페이지를 사용 하도록? 두 가지 옵션이 있습니다.

- 두 개의 중첩 된 마스터 페이지를 만들고 `AdminNestedSite.master` 하 고 `AdminNestedAlternate.master`를 최상위 마스터 페이지를 바인딩합니다 `Site.master` 및 `Alternate.master`각각. `BasePage`, 차례로 설정할 것을 `Page` 개체의 `MasterPageFile` 적절 한 중첩 마스터 페이지.
- 중첩된 된 단일 마스터 페이지를 만들고이 마스터 페이지를 사용 하 여 콘텐츠 페이지를 가진 합니다. 그런 다음 런타임에 설정 해야 중첩된 마스터 페이지의 `MasterPageFile` 런타임에 적절 한 최상위 마스터 페이지에는 속성입니다. (마스터 페이지 수도 이제 알게 될 수 있습니다, 대로 `MasterPageFile` 속성입니다.)

두 번째 옵션을 사용해 보겠습니다. 하나의 파일을 만들 중첩 마스터 페이지에는 `~/Admin` 라는 폴더 `AdminNested.master`합니다. 때문에 둘 다 `Site.master` 하 고 `Alternate.master` contentplaceholder의 동일한 집합이 되도록 바인딩할 바랍니다 하지만 마스터 페이지에 바인딩합니다, 중요 하지 않습니다 `Site.master` 일관성의 위해서입니다.


[![~/Admin 폴더에는 중첩 된 마스터 페이지를 추가 합니다.](nested-master-pages-cs/_static/image26.png)](nested-master-pages-cs/_static/image25.png)

**그림 09**: 중첩 된 마스터 페이지를 추가 합니다 `~/Admin` 폴더입니다. ([클릭 하 여 큰 이미지 보기](nested-master-pages-cs/_static/image27.png))


Visual Studio 추가 4 중첩된 마스터 페이지에 4 개의 ContentPlaceHolder 컨트롤과 마스터 페이지에 바인딩되기 때문에 콘텐츠 컨트롤을 새 중첩된 마스터 페이지 파일 초기 태그입니다. 2 단계와 3 단계에서 각 콘텐츠 컨트롤에는 각각의 ContentPlaceHolder 컨트롤로 추가 최상위 마스터 페이지의 ContentPlaceHolder 컨트롤로 동일한 이름을 지정에서 수행한 것과 같이 또한 해당 하는 콘텐츠 컨트롤에 다음 태그를 추가 합니다 `MainContent` ContentPlaceHolder:


[!code-html[Main](nested-master-pages-cs/samples/sample8.html)]

다음으로 정의 된 `instructions` CSS 클래스를 `Styles.css` 및 `AlternateStyles.css` CSS 파일. 다음 CSS 규칙으로 인해 스타일이 적용 되는 HTML 요소는 `instructions` 연한 노랑 배경색을 검은색 실선 테두리와 표시 되는 클래스:


[!code-css[Main](nested-master-pages-cs/samples/sample9.css)]

이 태그 중첩된 마스터 페이지에 추가 되었으므로,이 중첩 된 마스터 페이지 (즉, 관리 섹션에서 페이지)를 사용 하는 해당 페이지에만 표시 됩니다.

중첩된 마스터 페이지에 대 한 이러한 추가 마치면 선언적 태그는 다음과 같아야 합니다.


[!code-aspx[Main](nested-master-pages-cs/samples/sample10.aspx)]

각 콘텐츠 컨트롤에 각각의 ContentPlaceHolder 컨트롤로 올바르고 ContentPlaceHolder 컨트롤의 `ID` 속성 최상위 마스터 페이지에서 해당 ContentPlaceHolder 컨트롤로 동일한 값이 할당 됩니다. 관리 섹션에서는 특정 태그에 표시 되는 또한는 `MainContent` ContentPlaceHolder 합니다.

그림 10은는 `AdminNested.master` Visual Studio의 디자이너를 통해 볼 때 중첩 된 마스터 페이지입니다. 맨 위에 있는 노란색 상자의 지침을 볼 수는 `MainContent` 콘텐츠 컨트롤입니다.


[![중첩 된 마스터 페이지는 관리자에 대 한 지침을 포함 하도록 최상위 마스터 페이지를 확장 합니다.](nested-master-pages-cs/_static/image29.png)](nested-master-pages-cs/_static/image28.png)

**그림 10**: 중첩 된 마스터 페이지는 관리자에 대 한 지침을 포함 하도록 최상위 마스터 페이지를 확장 합니다. ([클릭 하 여 큰 이미지 보기](nested-master-pages-cs/_static/image30.png))


## <a name="step-5-updating-the-existing-content-pages-to-use-the-new-nested-master-page"></a>5 단계: 새 중첩된 마스터 페이지를 사용 하려면 기존 콘텐츠 페이지 업데이트

새 콘텐츠 페이지에 연결 하려면 먼저 관리 섹션을 추가 하 고 언제 든 지는 `AdminNested.master` 방금 만든 마스터 페이지입니다. 하지만 페이지 콘텐츠 기존 어떨까요? 사이트의 모든 콘텐츠 페이지에서 파생 되는 현재는 `BasePage` 프로그래밍 방식으로 런타임에 콘텐츠 페이지의 마스터 페이지를 설정 하는 클래스입니다. 관리 섹션에서 콘텐츠 페이지에 사용 하려는 동작이 아닙니다. 이러한 콘텐츠 페이지를 사용 하 여 항상 원하는 대신는 `AdminNested.master` 페이지입니다. 런타임 시 오른쪽 최상위 콘텐츠 페이지를 선택 합니다. 중첩된 마스터 페이지에서 수행 됩니다.

달성 하는 가장 좋은 방법은 원하는 것이 동작은 라는 새 기본 페이지를 사용자 지정 클래스를 만드는 것 `AdminBasePage` 확장 하는 `BasePage` 클래스입니다. `AdminBasePage` 다음 재정의할 수는 `SetMasterPageFile` 설정 합니다 `Page` 개체의 `MasterPageFile` 하드 코드 된 값으로 "~ / Admin/AdminNested.master". 이러한 방식으로 모든 페이지에서 파생 된 `AdminBasePage` 사용할지 `AdminNested.master`반면에서 파생 되는 모든 페이지 `BasePage` 해야 해당 `MasterPageFile` 속성 설정에 동적으로 "~ / Site.master" 또는 "~ / Alternate.master"의 값을 기반으로 `MyMasterPage` 세션 변수입니다.

새 클래스 파일을 추가 하 여 시작 합니다 `App_Code` 라는 폴더 `AdminBasePage.cs`합니다. 있을 `AdminBasePage` 확장할 `BasePage` 한 후 재정의 `SetMasterPageFile` 메서드. 할당 메서드에 `MasterPageFile` 값 "~ / Admin/AdminNested.master"입니다. 클래스에 이러한 변경을 수행한 후 파일에는 다음과 같아야 합니다.


[!code-csharp[Main](nested-master-pages-cs/samples/sample11.cs)]

관리 섹션에서 파생 된 기존 콘텐츠 페이지에 이제 해야 `AdminBasePage` 대신 `BasePage`합니다. 각 콘텐츠 페이지에 대 한 코드 숨김 클래스 파일을 이동 합니다 `~/Admin` 폴더가 변경 합니다. 예를 들어 `~/Admin/Default.aspx` 코드 숨김 클래스 선언에서 변경할 수 있습니다.


[!code-csharp[Main](nested-master-pages-cs/samples/sample12.cs)]

대상:


[!code-csharp[Main](nested-master-pages-cs/samples/sample13.cs)]

그림 11을 보여 줍니다 어떻게 최상위 마스터 페이지 (`Site.master` 또는 `Alternate.master`), 중첩된 마스터 페이지 (`AdminNested.master`), 하 고 관리 섹션 콘텐츠 페이지는 서로 관련이 있습니다.


[![중첩 된 마스터 페이지의 관리 섹션의 페이지에 콘텐츠 관련 정의](nested-master-pages-cs/_static/image32.png)](nested-master-pages-cs/_static/image31.png)

**그림 11**: The 중첩 마스터 페이지 정의 콘텐츠 관련 관리 섹션의 페이지 ([큰 이미지를 보려면 클릭](nested-master-pages-cs/_static/image33.png))


## <a name="step-6-mirroring-the-master-pages-public-methods-and-properties"></a>6 단계: 마스터 페이지의 공용 메서드 및 속성 미러링

이전에 설명한 대로 합니다 `~/Admin/AddProduct.aspx` 하 고 `~/Admin/Products.aspx` 페이지 마스터 페이지를 사용 하 여 프로그래밍 방식으로 상호 작용: `~/Admin/AddProduct.aspx` 호출 마스터 페이지의 공용 `RefreshRecentProductsGrid` 메서드 집합과 해당 `GridMessageText` 속성 `~/Admin/Products.aspx` 에 대 한 이벤트 처리기는 `PricesDoubled` 이벤트입니다. 이전 자습서에서 만든 추상 `BaseMasterPage` 이러한 공용 멤버를 정의 하는 클래스입니다.

합니다 `~/Admin/AddProduct.aspx` 및 `~/Admin/Products.aspx` 페이지의 마스터 페이지에서 파생 되는 것으로 가정 합니다 `BaseMasterPage` 클래스입니다. `AdminNested.master` 페이지에서 단, 현재 확장을 `System.Web.UI.MasterPage` 클래스. 결과적으로 방문할 때 `~/Admin/Products.aspx` 는 `InvalidCastException` 메시지와 함께 throw 됩니다: "종류의 개체를 캐스팅할 수 없습니다. ' ASP.admin\_adminnested\_마스터 ' 'BaseMasterPage'를 입력 합니다."

있어야이 문제를 해결 합니다 `AdminNested.master` 코드 숨김 클래스 확장 `BaseMasterPage`합니다. 중첩된 마스터 페이지의 코드 숨김 클래스 선언에서 업데이트:


[!code-csharp[Main](nested-master-pages-cs/samples/sample14.cs)]

대상:


[!code-csharp[Main](nested-master-pages-cs/samples/sample15.cs)]

에서는 아직 완료 되지 합니다. 때문에 합니다 `BaseMasterPage` 클래스는 추상 클래스에서 재정의 해야 합니다 `abstract` 멤버 `RefreshRecentProductsGrid` 및 `GridMessageText`합니다. 이러한 멤버는 해당 사용자 인터페이스를 업데이트 하려면 최상위 마스터 페이지에서 사용 됩니다. (사실에 합니다 `Site.master` 마스터 페이지는 모두 최상위 마스터 페이지 모두 확장 되므로 이러한 메서드를 구현 하지만 이러한 메서드를 사용 하 여 `BaseMasterPage`.)

이러한 멤버를 구현 해야 하는 동안 `AdminNested.master`, 중첩된 마스터 페이지에서 사용 하는 최상위 마스터 페이지에 동일한 멤버를 호출 하는 단순히는 이러한 구현을 수행 해야 합니다. 관리 섹션에서 콘텐츠 페이지를 중첩 된 마스터 페이지를 호출 하는 경우에 예를 들어 `RefreshRecentProductsGrid` 메서드를 중첩된 마스터 페이지 작업을 수행 해야 모든는, 호출 `Site.master` 하거나 `Alternate.master`의 `RefreshRecentProductsGrid` 메서드.

이렇게 하려면 다음을 추가 하 여 시작 `@MasterType` 의 맨 위에 지시문 `AdminNested.master`:


[!code-aspx[Main](nested-master-pages-cs/samples/sample16.aspx)]

이전에 설명한 대로 합니다 `@MasterType` 라는 코드 숨김 클래스에 있는 강력한 형식의 속성을 추가 하는 지시문 `Master`합니다. 재정의 `RefreshRecentProductsGrid` 하 고 `GridMessageText` 멤버에 대 한 호출을 위임 하 고는 `Master`의 해당 메서드:


[!code-csharp[Main](nested-master-pages-cs/samples/sample17.cs)]

이 코드를 사용 하 여를 방문 하 여 관리 섹션의 콘텐츠 페이지를 사용할 수 있어야 합니다. 그림 12는 `~/Admin/Products.aspx` 브라우저를 통해 볼 때 페이지입니다. 알 수 있듯이 중첩된 마스터 페이지에 정의 되어 있는 관리 지침 상자를, 페이지에 포함 됩니다.


[![각 페이지의 맨 위에 있는 지침을 포함 하는 관리 섹션에서 콘텐츠 페이지](nested-master-pages-cs/_static/image35.png)](nested-master-pages-cs/_static/image34.png)

**그림 12**: 각 페이지 위쪽의 관리 섹션 포함 지침에는 콘텐츠 페이지 ([큰 이미지를 보려면 클릭](nested-master-pages-cs/_static/image36.png))


## <a name="step-7-using-the-appropriate-top-level-master-page-at-runtime"></a>7 단계: 적절 한 최상위 마스터 페이지를 사용 하 여 런타임 시

관리 섹션에서 모든 콘텐츠 페이지는 모든 기능을 갖춘, 모두 동일한 최상위 마스터 페이지를 사용 하 고 마스터 페이지에서 사용자가 선택한 무시 `ChooseMasterPage.aspx`합니다. 이 동작은 때문에 중첩 된 마스터 페이지에 해당 `MasterPageFile` 속성 정적으로 설정 `Site.master` 에서 해당 `<%@ Master %>` 지시문입니다.

로 설정 해야 하는 최종 사용자가 선택한 최상위 마스터 페이지를 사용 하는 `AdminNested.master`의 `MasterPageFile` 속성의 값을는 `MyMasterPage` 세션 변수입니다. 콘텐츠 페이지의 설정 했기 때문 `MasterPageFile` 속성에서 `BasePage`, 중첩된 마스터 페이지의 설정할 것을 생각할 수 있습니다 `MasterPageFile` 속성에서 `BaseMasterPage` 또는 `AdminNested.master`의 코드 숨김 클래스입니다. 하지만이 작동 하지 않습니다,를 설정 해야 하므로 `MasterPageFile` PreInit 단계의 끝 속성입니다. 에서는 프로그래밍 방식으로 마스터 페이지의 페이지 수명 주기를 탭 할 수 있는 가장 이른 시간 (발생 하는 PreInit 단계 후) Init 단계 이며

중첩된 마스터 페이지의 설정 해야 하므로 `MasterPageFile` 콘텐츠 페이지의 속성입니다. 유일한 콘텐츠는 사용 하는 페이지의 `AdminNested.master` 에서 파생 되는 마스터 페이지 `AdminBasePage`합니다. 따라서 있습니다이 논리를 넣을 수 했습니다. 되며에서는 5 단계에서에서의 `SetMasterPageFile` 메서드를 설정 합니다 `Page` 개체의 `MasterPageFile` 속성을 "~ / Admin/AdminNested.master"입니다. 업데이트 `SetMasterPageFile` 마스터 페이지의 설정 `MasterPageFile` 세션에 저장 된 결과에 대 한 속성:


[!code-csharp[Main](nested-master-pages-cs/samples/sample18.cs)]

합니다 `GetMasterPageFileFromSession` 메서드를 추가 했습니다는 `BasePage` 클래스는 이전 자습서에서는 세션 변수 값을 기준으로 해당 마스터 페이지 파일 경로 반환 합니다.

진행에서이 변경으로 사용자의 마스터 페이지 선택 관리 섹션으로 습득 합니다. 그림 13 그림 12 하지만 변경 된 후 사용자에 해당 마스터 페이지 선택 영역을 같은 페이지를 보여 줍니다. `Alternate.master`합니다.


[![사용자가 선택한 최상위 마스터 페이지를 사용 하 여 중첩 된 관리 페이지](nested-master-pages-cs/_static/image38.png)](nested-master-pages-cs/_static/image37.png)

**그림 13**: 중첩 관리 페이지를 사용 하 여 사용자가 최상위 마스터 페이지 선택 ([큰 이미지를 보려면 클릭](nested-master-pages-cs/_static/image39.png))


## <a name="summary"></a>요약

많은 like 콘텐츠 페이지 마스터 페이지에 바인딩할 수 있기 중첩 만들려면 자식 마스터 페이지에서 마스터 페이지 부모 마스터 페이지에 바인딩합니다. 자식 마스터 페이지는 해당 부모의 ContentPlaceHolders;의 각 콘텐츠 컨트롤을 정의할 수 있습니다. 이러한 콘텐츠 컨트롤에는 자체 ContentPlaceHolder 컨트롤 (뿐만 아니라 다른 태그)를 추가할 수 것. 중첩된 마스터 페이지는 모든 페이지는 가장 중요 한 디자인을 공유 하면서 사이트의 특정 섹션 고유한 사용자 지정이 필요한 대규모 웹 응용 프로그램에 매우 유용 합니다.

즐거운 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [중첩 된 ASP.NET 마스터 페이지](https://msdn.microsoft.com/library/x2b3ktt7.aspx)
- [중첩된 마스터 페이지 및 VS 2005 디자인 타임에 대 한 팁](https://weblogs.asp.net/scottgu/archive/2005/11/11/430382.aspx)
- [VS 2008 중첩 마스터 페이지 지원](https://weblogs.asp.net/scottgu/archive/2007/07/09/vs-2008-nested-master-page-support.aspx)

### <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 작성자의 여러 ASP/ASP.NET 서적과 4GuysFromRolla.com의 설립자 이며, 왔습니다 Microsoft 웹 기술을 1998 합니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 3.5 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)합니다. Scott에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com) 통하거나 저자의 블로그 [ http://ScottOnWriting.NET ](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](specifying-the-master-page-programmatically-cs.md)
> [다음](creating-a-site-wide-layout-using-master-pages-vb.md)
