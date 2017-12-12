---
uid: mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-vb
title: Creating Page Layouts with View Master Pages (VB) | Microsoft Docs
author: microsoft
description: "이 자습서를 사용 하 여 보기의 마스터 페이지 응용 프로그램에서 여러 페이지에 대 한 일반 페이지 레이아웃을 만드는 방법에 알아봅니다. 사용할 수는 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/16/2008
ms.topic: article
ms.assetid: d34f90a1-6de3-482a-a326-f87fdcbaaaff
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 5466ea8a33bd2ccfe36c0f01b6b474bbb8d540a3
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="creating-page-layouts-with-view-master-pages-vb"></a>Creating Page Layouts with View Master Pages (VB)
====================
여 [Microsoft](https://github.com/microsoft)

[PDF 다운로드](http://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_12_VB.pdf)

> 이 자습서를 사용 하 여 보기의 마스터 페이지 응용 프로그램에서 여러 페이지에 대 한 일반 페이지 레이아웃을 만드는 방법에 알아봅니다. 페이지 2 열 레이아웃을 정의 하 고 모든 웹 응용 프로그램의 페이지에 대 한 2 열 레이아웃 사용 예를 들어 뷰 마스터 페이지를 사용할 수 있습니다.


## <a name="creating-page-layouts-with-view-master-pages"></a>Creating Page Layouts with View Master Pages

이 자습서를 사용 하 여 보기의 마스터 페이지 응용 프로그램에서 여러 페이지에 대 한 일반 페이지 레이아웃을 만드는 방법에 알아봅니다. 페이지 2 열 레이아웃을 정의 하 고 모든 웹 응용 프로그램의 페이지에 대 한 2 열 레이아웃 사용 예를 들어 뷰 마스터 페이지를 사용할 수 있습니다.

수 이용할 있습니다 보기의 마스터 페이지 콘텐츠를 공유 공통 응용 프로그램에서 여러 페이지에 걸쳐 있습니다. 예를 들어 뷰 마스터 페이지에서 웹 사이트 로고, 탐색 링크 및 배너 광고를 배치할 수 있습니다. 이런 방식으로 모든 페이지에 응용 프로그램은 자동으로이 콘텐츠를 표시 됩니다.

이 자습서에서는 새 뷰 마스터 페이지를 만들고 마스터 페이지에 따라 새 뷰 콘텐츠 페이지는 방법에 설명 합니다.

### <a name="creating-a-view-master-page"></a>뷰 마스터 페이지 만들기

2 열 레이아웃을 정의 하는 뷰 마스터 페이지를 만들어 보겠습니다. 추가한 새 뷰 마스터 페이지를 MVC 프로젝트 Views\Shared 폴더를 마우스 오른쪽 단추로 클릭 하 여 메뉴 옵션을 선택 하면 **추가, 새 항목**, MVC 뷰 마스터 페이지 서식 파일을 선택 하 고 (그림 1 참조).


[![뷰 마스터 페이지를 추가합니다.](creating-page-layouts-with-view-master-pages-vb/_static/image2.png)](creating-page-layouts-with-view-master-pages-vb/_static/image1.png)

**그림 01**: 뷰 마스터 페이지 추가 ([전체 크기 이미지를 보려면 클릭](creating-page-layouts-with-view-master-pages-vb/_static/image3.png))


응용 프로그램에서 둘 이상의 뷰 마스터 페이지를 만들 수 있습니다. 각 보기 마스터 페이지는 다른 페이지 레이아웃을 정의할 수 있습니다. 예를 들어 2 열 레이아웃을 특정 페이지와 다른 페이지 3 열 레이아웃을 원하는 수 있습니다.

뷰 마스터 페이지 표준 ASP.NET MVC 보기와 매우 비슷하며 찾습니다. 그러나 기본 보기와 달리 뷰 마스터 페이지를 하나 이상 포함 `<asp:ContentPlaceHolder>` 태그입니다. `<contentplaceholder>` 태그는 개별 콘텐츠 페이지에서 재정의 될 수 있는 마스터 페이지의 영역을 표시 하는 데 사용 됩니다.

예를 들어 보기 마스터 페이지 목록 1에서 2 열 레이아웃을 정의합니다. 포함 된 두 개의 `<contentplaceholder>` 태그입니다. 하나의 `<ContentPlaceHolder>` 각 열에 대 한 합니다.

**1 – 나열`Views\Shared\Site.master`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample1.aspx)]

목록 1의 마스터 페이지에는 두 개의 보기의 본문 `<div>` 두 개의 열에 해당 하는 태그입니다. 스타일 시트 연계 열 클래스가 둘 다에 적용 된 `<div>` 태그입니다. 이 클래스는 마스터 페이지 맨 위에 있는 선언한 스타일 시트에 정의 됩니다. 디자인 뷰로 전환 하 여 뷰 마스터 페이지를 렌더링할 방식을 미리 볼 수 있습니다. 소스 코드 편집기의 왼쪽 아래에 디자인 탭을 클릭 (그림 2 참조).


[![마스터 페이지 디자이너의 미리 보기](creating-page-layouts-with-view-master-pages-vb/_static/image5.png)](creating-page-layouts-with-view-master-pages-vb/_static/image4.png)

**그림 02**: 마스터 페이지 디자이너의 미리 보기 ([전체 크기 이미지를 보려면 클릭](creating-page-layouts-with-view-master-pages-vb/_static/image6.png))


### <a name="creating-a-view-content-page"></a>뷰 콘텐츠 페이지 만들기

마스터 페이지 보기를 만든 후 콘텐츠 페이지 보기 마스터 페이지에 따라 하나 이상의 보기를 만들 수 있습니다. Views\Home 폴더를 마우스 오른쪽 단추로 클릭 하 여 홈 컨트롤러에 대 한 인덱스 뷰 콘텐츠 페이지를 만들 수는 예를 들어 선택 하면 **추가, 새 항목**선택한는 **MVC 뷰 콘텐츠 페이지** 입력 서식 파일 Index.aspx, 이름 및 추가 클릭 하면 단추 (그림 3 참조).


[![뷰 콘텐츠 페이지를 추가합니다.](creating-page-layouts-with-view-master-pages-vb/_static/image8.png)](creating-page-layouts-with-view-master-pages-vb/_static/image7.png)

**그림 03**: 뷰 콘텐츠 페이지 추가 ([전체 크기 이미지를 보려면 클릭](creating-page-layouts-with-view-master-pages-vb/_static/image9.png))


추가 단추를 클릭 한 후 새 대화 상자가 나타나는 뷰 콘텐츠 페이지와 연결할 마스터 페이지 뷰를 선택할 수 있습니다 (그림 4 참조). 이전 섹션에서 만든 Site.master 뷰 마스터 페이지를 이동할 수 있습니다.


[![마스터 페이지를 선택합니다.](creating-page-layouts-with-view-master-pages-vb/_static/image11.png)](creating-page-layouts-with-view-master-pages-vb/_static/image10.png)

**그림 04**: 마스터 페이지 선택 ([전체 크기 이미지를 보려면 클릭](creating-page-layouts-with-view-master-pages-vb/_static/image12.png))


Site.master 마스터 페이지에 따라 새 뷰 콘텐츠 페이지를 만든 후 목록 2에서 파일 가져오기

**2 – 나열`Views\Home\Index.aspx`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample2.aspx)]

이 보기에는 `<asp:Content>` 각각에 해당 하는 태그는 `<asp:ContentPlaceHolder>` 뷰 마스터 페이지의 태그에에서 있습니다. 각 `<asp:Content>` 태그를 포함 하는 특정 가리키는 ContentPlaceHolderID 특성 `<asp:ContentPlaceHolder>` 를 재정의 합니다.

또한 콘텐츠 보기 페이지 목록 2에서 공지 일반 여는 태그와 닫는 HTML 태그의 없습니다. 예를 들어 없기 열기 및 닫기 `<html>` 또는 `<head>` 태그입니다. 일반 여는 태그와 닫는 태그의 모든 뷰 마스터 페이지에 포함 됩니다.

내 보기 콘텐츠 페이지에 표시 하려는 모든 콘텐츠를 배치 해야 합니다는 `<asp:Content>` 태그입니다. HTML 또는 이러한 태그 외부에서 다른 콘텐츠를 배치 하는 경우 페이지를 보려고 할 때 오류가 발생 합니다.

재정의 하지 않아도 모든 `<asp:ContentPlaceHolder>` 콘텐츠 보기 페이지에 마스터 페이지의 태그입니다. 재정의 해야는 `<asp:ContentPlaceHolder>` 태그 특정 콘텐츠로 대체 하려는 경우 태그를 지정 합니다.

예를 들어 목록 3에서 수정 된 인덱스 보기에는 두 개의 `<asp:Content>` 태그입니다. 각각의 `<asp:Content>` 태그 일부 텍스트를 포함 합니다.

**3 – 나열`Views\Home\Index.aspx (modified)`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample3.aspx)]

보기 목록 3에 요청 될 때 그림 5에 있는 페이지를 렌더링 합니다. 공지 보기 두 개의 열이 있는 페이지를 렌더링 합니다. 또한 뷰 콘텐츠 페이지에서 콘텐츠가 뷰 마스터 페이지의 내용으로 병합은 확인할 수 있습니다.


[![인덱스 뷰 콘텐츠 페이지](creating-page-layouts-with-view-master-pages-vb/_static/image14.png)](creating-page-layouts-with-view-master-pages-vb/_static/image13.png)

**그림 05**: The 인덱스 뷰 콘텐츠 페이지 ([전체 크기 이미지를 보려면 클릭](creating-page-layouts-with-view-master-pages-vb/_static/image15.png))


### <a name="modifying-view-master-page-content"></a>뷰 마스터 페이지 콘텐츠를 수정합니다.

마스터 페이지 보기와 작업 하는 경우에 즉시 거의 발생 하는 문제 중 하나는 서로 다른 뷰 콘텐츠 페이지 요청 되는 경우 마스터 페이지 콘텐츠 보기를 수정 하는 문제입니다. 예를 들어 웹 응용 프로그램을 고유한 타이틀이에서 각 페이지를 원하는 합니다. 그러나 뷰 콘텐츠 페이지 아니라 뷰 마스터 페이지에 제목 선언 됩니다. 따라서 하면 사용자 지정 하려면 어떻게 각 보기 콘텐츠 페이지에 대 한 페이지 제목을?

두 가지는 뷰 콘텐츠 페이지에서 표시 되는 제목을 수정할 수 있습니다. 첫째, 페이지 제목을의 title 특성에 할당할 수 있습니다는 `<%@ page %>` 뷰 콘텐츠 페이지 맨 위에 있는 선언한 지시문입니다. 예를 들어 인덱스 뷰를 페이지 제목이 "슈퍼 뛰어난 웹 사이트"를 할당 하려는 경우에 인덱스 보기의 맨 위에 다음 지시문을 포함할 수 있습니다.

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample4.aspx)]

인덱스 뷰를 렌더링할 때 브라우저에 원하는 제목이 브라우저 제목 표시줄에 표시 됩니다.


[![브라우저 제목 표시줄](creating-page-layouts-with-view-master-pages-vb/_static/image17.png)](creating-page-layouts-with-view-master-pages-vb/_static/image16.png)


마스터 뷰 페이지에서 실행 되도록 한 title 특성에 대 한 순서에 만족 해야 하는 중요 한 요구 사항 하나 있습니다. 마스터 페이지 보기를 포함 해야 합니다는 `<head runat="server">` 일반 대신 태그 `<head>` 헤더에 대 한 태그입니다. 경우는 `<head>` 태그의 runat는 = "server" 특성 제목이 표시 되지 않습니다. 마스터 페이지에 필요한 기본 보기 `<head runat="server">` 태그입니다.

또 다른 개별 뷰 콘텐츠 페이지에서 마스터 페이지 콘텐츠를 수정 하는 방법은에 수정 하려는 영역을 래핑하는 `<asp:ContentPlaceHolder>` 태그입니다. 예를 들어 제목, 뿐만 아니라 마스터 뷰 페이지에서 렌더링 메타 태그를 변경 하 고 가정 합니다. 마스터 뷰 페이지 목록 4에는 `<asp:ContentPlaceHolder>` 태그 내에서 해당 `<head>` 태그입니다.

**4 – 나열`Views\Shared\Site2.master`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample5.aspx)]

에 `<asp:ContentPlaceHolder>` 태그 목록 4에는 기본 콘텐츠: 기본 제목과 기본 메타 태그입니다. 이 재정의 하지 않는 경우 `<asp:ContentPlaceHolder>` 개별 보기 콘텐츠 페이지에 태그를 기본 콘텐츠 표시 됩니다.

콘텐츠 보기 페이지 목록 5에서 재정의 된 `<asp:ContentPlaceHolder>` 제목 사용자 지정 및 사용자 지정 메타 태그를 표시 하기 위해 태그입니다.

**5-나열`Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample6.aspx)]

### <a name="summary"></a>요약

이 자습서 마스터 페이지 및 콘텐츠 페이지를 볼 한 기본적인 소개를 제공 합니다. 새 뷰 마스터 페이지를 만들고 그에 따라 콘텐츠 페이지 보기를 만드는 방법을 배웠습니다. 또한 특정 뷰 콘텐츠 페이지에서 보기 마스터 페이지의 내용을 수정 하는 방법을 검사 했습니다.

>[!div class="step-by-step"]
[이전](using-the-tagbuilder-class-to-build-html-helpers-vb.md)
[다음](passing-data-to-view-master-pages-vb.md)
