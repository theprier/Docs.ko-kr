---
uid: mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-vb
title: 보기 마스터 페이지 (VB)를 사용 하 여 페이지 레이아웃 만들기 | Microsoft Docs
author: microsoft
description: 이 자습서에서는 보기 마스터 페이지를 활용 하 여 응용 프로그램에서 여러 페이지에 대 한 일반적인 페이지 레이아웃을 만드는 방법을 알아봅니다. 사용할 수는 중...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: d34f90a1-6de3-482a-a326-f87fdcbaaaff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 4ff74b1dc1d83b7ec1c8ecf6eca341a5cd14403f
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41838176"
---
<a name="creating-page-layouts-with-view-master-pages-vb"></a>보기 마스터 페이지 (VB)를 사용 하 여 페이지 레이아웃 만들기
====================
[Microsoft](https://github.com/microsoft)

[PDF 다운로드](http://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_12_VB.pdf)

> 이 자습서에서는 보기 마스터 페이지를 활용 하 여 응용 프로그램에서 여러 페이지에 대 한 일반적인 페이지 레이아웃을 만드는 방법을 알아봅니다. 열이 두 페이지 레이아웃을 정의 하 고 모든 웹 응용 프로그램의 페이지에 대 한 2 열 레이아웃을 사용 예를 들어, 마스터 페이지 보기를 사용할 수 있습니다.


## <a name="creating-page-layouts-with-view-master-pages"></a>보기 마스터 페이지를 사용 하 여 페이지 레이아웃 만들기

이 자습서에서는 보기 마스터 페이지를 활용 하 여 응용 프로그램에서 여러 페이지에 대 한 일반적인 페이지 레이아웃을 만드는 방법을 알아봅니다. 열이 두 페이지 레이아웃을 정의 하 고 모든 웹 응용 프로그램의 페이지에 대 한 2 열 레이아웃을 사용 예를 들어, 마스터 페이지 보기를 사용할 수 있습니다.

있습니다 수 활용할 보기의 콘텐츠를 공유 하려면 일반적인 응용 프로그램에서 여러 페이지에 걸쳐 마스터 페이지. 예를 들어, 웹 사이트 로고, 탐색 링크와 배너 광고 보기 마스터 페이지에 배치할 수 있습니다. 이런 방식으로 모든 페이지에서 응용 프로그램은 자동으로이 콘텐츠를 표시 됩니다.

이 자습서에서는 마스터 페이지에 따라 새 뷰 콘텐츠 페이지를 만들고 새 보기 마스터 페이지를 만드는 방법을 알아봅니다.

### <a name="creating-a-view-master-page"></a>보기 마스터 페이지 만들기

2 열 레이아웃을 정의 하는 보기 마스터 페이지를 만들어 시작 해 보겠습니다. 추가한 새 보기 마스터 페이지를 MVC 프로젝트 Views\Shared 폴더를 마우스 오른쪽 단추로 클릭 하 여 메뉴 옵션을 선택 하면 **추가, 새 항목**, MVC 보기 마스터 페이지 템플릿을 선택 하 고 (그림 1 참조).


[![보기 마스터 페이지 추가](creating-page-layouts-with-view-master-pages-vb/_static/image2.png)](creating-page-layouts-with-view-master-pages-vb/_static/image1.png)

**그림 01**: 뷰 마스터 페이지 추가 ([큰 이미지를 보려면 클릭](creating-page-layouts-with-view-master-pages-vb/_static/image3.png))


응용 프로그램에서 둘 이상의 뷰 마스터 페이지를 만들 수 있습니다. 각 보기 마스터 페이지에는 다양 한 페이지 레이아웃을 정의할 수 있습니다. 예를 들어 좋습니다 2 열 레이아웃을 특정 페이지 및 기타 페이지 3 열 레이아웃 있어야 합니다.

보기 마스터 페이지와 매우 비슷하며 표준 ASP.NET MVC 보기. 그러나 기본 보기와 달리 뷰 마스터 페이지를 하나 이상 포함 `<asp:ContentPlaceHolder>` 태그입니다. `<contentplaceholder>` 태그는 개별 콘텐츠 페이지에서 재정의 될 수 있는 마스터 페이지의 영역을 표시 하는 데 사용 됩니다.

예를 들어, 보기 마스터 페이지 목록 1에서 2 열 레이아웃을 정의합니다. 포함 된 두 `<contentplaceholder>` 태그입니다. 하나의 `<ContentPlaceHolder>` 각 열에 대 한 합니다.

**목록 1 – `Views\Shared\Site.master`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample1.aspx)]

목록 1에서 마스터 페이지에는 두 개의 뷰의 본문 `<div>` 두 열에 해당 하는 태그입니다. Cascading Style Sheet 열 클래스가 둘 다에 적용 된 `<div>` 태그입니다. 이 클래스는 마스터 페이지의 맨 위에 선언 스타일 시트에 정의 됩니다. 디자인 뷰로 전환 하 여 보기 마스터 페이지를 렌더링할 방식을 미리 볼 수 있습니다. 소스 코드 편집기의 왼쪽 아래에 있는 디자인 탭을 클릭 (그림 2 참조).


[![마스터 페이지 디자이너의 미리 보기](creating-page-layouts-with-view-master-pages-vb/_static/image5.png)](creating-page-layouts-with-view-master-pages-vb/_static/image4.png)

**그림 02**: 마스터 페이지 디자이너의 미리 보기 ([큰 이미지를 보려면 클릭](creating-page-layouts-with-view-master-pages-vb/_static/image6.png))


### <a name="creating-a-view-content-page"></a>뷰 콘텐츠 페이지 만들기

보기 마스터 페이지를 만든 후에 하나 이상의 뷰 콘텐츠 페이지 보기 마스터 페이지를 기반으로 만들 수 있습니다. 예를 들어 Views\Home 폴더를 마우스 오른쪽 단추로 클릭 하 여 홈 컨트롤러에 대 한 인덱스 뷰 콘텐츠 페이지를 만들 수 있습니다 선택 **추가, 새 항목**선택 하는 **MVC 뷰 콘텐츠 페이지** 입력 템플릿 Index.aspx, 이름 및 추가 단추 (그림 3 참조).


[![뷰 콘텐츠 페이지 추가](creating-page-layouts-with-view-master-pages-vb/_static/image8.png)](creating-page-layouts-with-view-master-pages-vb/_static/image7.png)

**그림 03**: 뷰 콘텐츠 페이지 추가 ([큰 이미지를 보려면 클릭](creating-page-layouts-with-view-master-pages-vb/_static/image9.png))


추가 단추를 클릭 하면 새 대화 상자가 나타나는 뷰 콘텐츠 페이지와 연결할 보기 마스터 페이지를 선택할 수 있습니다 (그림 4 참조). 이전 섹션에서 만든 Site.master 뷰 마스터 페이지를 이동할 수 있습니다.


[![마스터 페이지를 선택합니다.](creating-page-layouts-with-view-master-pages-vb/_static/image11.png)](creating-page-layouts-with-view-master-pages-vb/_static/image10.png)

**그림 04**: 마스터 페이지 선택 ([큰 이미지를 보려면 클릭](creating-page-layouts-with-view-master-pages-vb/_static/image12.png))


Site.master 마스터 페이지에 따라 새 뷰 콘텐츠 페이지를 만든 후 2 목록에서 파일을 가져옵니다.

**2 – 나열 `Views\Home\Index.aspx`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample2.aspx)]

이 뷰를 포함 하는 `<asp:Content>` 각각에 해당 하는 태그를 `<asp:ContentPlaceHolder>` 보기 마스터 페이지의 태그에에서. 각 `<asp:Content>` 태그를 포함 하는 특정 가리키는 ContentPlaceHolderID 특성을 `<asp:ContentPlaceHolder>` 를 재정의 합니다.

또한 콘텐츠 목록 2에서 페이지 보기는 통지 일반와 HTML 닫는 태그의 없습니다. 예를 들어 없습니다을 열고 닫는 `<html>` 또는 `<head>` 태그입니다. 모든 표준 태그와 닫는 태그 보기 마스터 페이지에 포함 됩니다.

뷰 콘텐츠 페이지에 표시 하려는 내용을 안에 있어야를 `<asp:Content>` 태그입니다. HTML 또는 기타 콘텐츠 이러한 태그 외부에 배치 하면 다음 오류가 표시 됩니다는 페이지를 표시 하려고 합니다.

재정의할 필요가 모든 `<asp:ContentPlaceHolder>` 뷰 콘텐츠 페이지의 마스터 페이지의 태그입니다. 재정의 해야 하는 `<asp:ContentPlaceHolder>` 특정 콘텐츠를 사용 하 여 태그를 바꿀 때 태그를 지정 합니다.

예를 들어 목록 3에서 수정 된 인덱스 보기에는 두 개의 `<asp:Content>` 태그입니다. 각는 `<asp:Content>` 태그 일부 텍스트를 포함 합니다.

**3 – 나열 `Views\Home\Index.aspx (modified)`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample3.aspx)]

보기 3의 보기를 요청 하면 그림 5에서 페이지를 렌더링 합니다. 뷰를 두 개의 열을 사용 하 여 페이지를 렌더링 하는 알 수 있습니다. 확인, 또한 뷰 콘텐츠 페이지에서 콘텐츠 보기 마스터 페이지의 콘텐츠와 병합 되는 합니다.


[![인덱스 뷰 콘텐츠 페이지](creating-page-layouts-with-view-master-pages-vb/_static/image14.png)](creating-page-layouts-with-view-master-pages-vb/_static/image13.png)

**그림 05**: The 인덱스 뷰 콘텐츠 페이지 ([큰 이미지를 보려면 클릭](creating-page-layouts-with-view-master-pages-vb/_static/image15.png))


### <a name="modifying-view-master-page-content"></a>보기 마스터 페이지 콘텐츠를 수정합니다.

보기 마스터 페이지를 사용 하는 경우에 즉시 거의 발생할 수 있는 한 가지 문제는 서로 다른 뷰 콘텐츠 페이지를 요청 하면 마스터 페이지 콘텐츠 보기를 수정 하는 문제입니다. 예를 들어, 고유한 제목이 할 웹 응용 프로그램에서 각 페이지를 원하는 합니다. 그러나 제목 뷰 콘텐츠 페이지 아니라 보기 마스터 페이지에 선언 됩니다. 따라서 수행할 사용자 지정 방법 각 뷰 콘텐츠 페이지에 대 한 페이지 제목을?

뷰 콘텐츠 페이지에 의해 표시 되는 제목 수정할 수 있는 두 가지 있습니다. 먼저 title 특성에 페이지 제목을 지정할 수 있습니다는 `<%@ page %>` 지시문 뷰 콘텐츠 페이지의 맨 위에 선언 합니다. 예를 들어 인덱스 뷰에 페이지 제목을 "슈퍼 뛰어난 웹 사이트"를 할당 하려는 경우 인덱스 뷰의 맨 위에 있는 다음 지시문을 포함할 수 있습니다.

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample4.aspx)]

인덱스 보기 브라우저에 렌더링 되 면 원하는 제목 브라우저 제목 표시줄에 나타납니다.


[![브라우저 제목 표시줄](creating-page-layouts-with-view-master-pages-vb/_static/image17.png)](creating-page-layouts-with-view-master-pages-vb/_static/image16.png)


마스터 뷰 페이지를 작동 하려면 title 특성에 대 한 순서로 충족 해야 하는 중요 한 요구 사항 중 하나 있습니다. 보기 마스터 페이지를 포함 해야 합니다는 `<head runat="server">` 태그는 보통 대신 `<head>` 헤더에 대 한 태그입니다. 경우는 `<head>` 태그에는 runat = "server" 특성이 제목이 표시 되지 않습니다. 마스터 페이지에 필요한 기본 보기 `<head runat="server">` 태그입니다.

개별 뷰 콘텐츠 페이지에서 마스터 페이지 콘텐츠를 수정 하는 다른 방법은을 수정 하려는 영역을 래핑하는 것을 `<asp:ContentPlaceHolder>` 태그입니다. 예를 들어, 제목, 뿐만 아니라 마스터 뷰 페이지에서 렌더링 메타 태그를 변경 한다고 가정해 보겠습니다. 마스터 뷰 페이지 목록 4에는 `<asp:ContentPlaceHolder>` 태그 내에서 해당 `<head>` 태그입니다.

**4-목록 `Views\Shared\Site2.master`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample5.aspx)]

에 `<asp:ContentPlaceHolder>` 태그 목록 4에서 기본 콘텐츠를 포함: 기본 제목과 기본 메타 태그입니다. 이 재정의 하지 않으면 `<asp:ContentPlaceHolder>` 태그 개별 뷰 콘텐츠 페이지를 기본 콘텐츠가 표시 됩니다.

콘텐츠 보기 페이지 목록 5에서 재정의 된 `<asp:ContentPlaceHolder>` 사용자 지정 제목 및 사용자 지정 메타 태그를 표시 하기 위해 태그입니다.

**5-목록 `Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample6.aspx)]

### <a name="summary"></a>요약

이 자습서는 마스터 페이지 및 콘텐츠 페이지를 볼 기본적인 소개를 사용 하 여 제공 합니다. 새 보기 마스터 페이지를 만들고 그에 따라 뷰 콘텐츠 페이지를 만들 하는 방법을 알아보았습니다. 또한 특정 뷰 콘텐츠 페이지 로부터 마스터 뷰 페이지의 콘텐츠를 수정 하는 방법을 살펴보았습니다.

> [!div class="step-by-step"]
> [이전](using-the-tagbuilder-class-to-build-html-helpers-vb.md)
> [다음](passing-data-to-view-master-pages-vb.md)
