---
uid: web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
title: 들어 (C#) 시작 | Microsoft Docs
author: microsoft
description: AJAX 컨트롤 도구 키트를 사용 하 여 시작 하기 전에 알아야 할 하기만 하면에 대해 알아봅니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/12/2009
ms.topic: article
ms.assetid: 16dc5c11-65be-4eae-a818-9fad7f8259c6
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
msc.type: authoredcontent
ms.openlocfilehash: e6a7a8d45f32a33eaacf3c42b52a02d2ada1aab6
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30879181"
---
<a name="get-started-with-the-ajax-control-toolkit-c"></a>시작 들어 (C#)
====================
by [Microsoft](https://github.com/microsoft)

> AJAX 컨트롤 도구 키트를 사용 하 여 시작 하기 전에 알아야 할 하기만 하면에 대해 알아봅니다.


들어 ASP.NET 응용 프로그램에서 사용할 수 있는 무료 30 개 이상의 컨트롤을 포함 합니다. 이 자습서에서는 AJAX 컨트롤 도구 키트를 다운로드 하 여 Visual Studio/Visual Web Developer Express 도구 상자에 도구 키트 컨트롤을 추가 하는 방법에 설명 합니다.

## <a name="downloading-the-ajax-control-toolkit"></a>AJAX 컨트롤 Toolkit을 다운로드

[들어](http://devexpress.com/act) ASP.NET 커뮤니티와 ASP.NET 팀의 멤버에 의해 개발 된 오픈 소스 프로젝트입니다. 


[![AJAX 컨트롤 Toolkit을 다운로드](get-started-with-the-ajax-control-toolkit-cs/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image1.png)

**그림 01**: AJAX 컨트롤 Toolkit을 다운로드 ([전체 크기 이미지를 보려면 클릭](get-started-with-the-ajax-control-toolkit-cs/_static/image2.png))


파일을 다운로드 한 후 파일을 차단 해제 해야 합니다. 파일을 마우스 오른쪽 단추로 클릭 하 고 속성을 선택한 클릭는 **차단 해제** 단추 (그림 2 참조).


[![AJAX 컨트롤 Toolkit ZIP 파일을 차단 해제](get-started-with-the-ajax-control-toolkit-cs/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image3.png)

**그림 02**: AJAX 컨트롤 Toolkit ZIP 파일을 차단 해제 ([전체 크기 이미지를 보려면 클릭](get-started-with-the-ajax-control-toolkit-cs/_static/image4.png))


파일의 차단을 해제 한 후 압축을 풀 수 파일: 파일을 마우스 오른쪽 단추로 클릭 하 고 선택 된 **압축 풀기** 메뉴 옵션입니다. 이제 Visual Studio/Visual Web Developer 도구 상자에 도구 키트를 추가할 준비가 되었습니다.

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a>도구 상자에 들어 추가

AJAX 컨트롤 도구 키트를 사용 하는 가장 쉬운 방법은 Visual Studio/Visual Web Developer 도구 상자에 도구 키트를 추가 하는 것 (그림 3 참조). 이런 방식으로 끌 수 있습니다 단순히 toolkit 컨트롤 페이지를 사용 하려는 경우.


[![들어 도구 상자에 표시 됩니다.](get-started-with-the-ajax-control-toolkit-cs/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image5.png)

**그림 03**: 들어 도구 상자에 나타납니다 ([전체 크기 이미지를 보려면 클릭](get-started-with-the-ajax-control-toolkit-cs/_static/image6.png))


첫째, 도구 상자에 들어 탭을 추가 해야 합니다. 다음이 단계를 수행 합니다.

1. 메뉴 옵션 파일을 새 웹 사이트를 선택 하 여 새 ASP.NET 웹 사이트를 만듭니다. 편집기에서 파일을 열려면 솔루션 탐색기 창에서 Default.aspx를 두 번 클릭 합니다.
2. 일반 탭 아래에 있는 도구 상자를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **탭 추가** (그림 4 참조).
3. AJAX 컨트롤 Toolkit 이라는 새 탭을 입력 합니다.


[![새 탭 추가](get-started-with-the-ajax-control-toolkit-cs/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image7.png)

**그림 04**: 새 탭이 추가 ([전체 크기 이미지를 보려면 클릭](get-started-with-the-ajax-control-toolkit-cs/_static/image8.png))


다음을 새 탭에 들어 컨트롤을 추가 해야 합니다. 아래 단계를 수행합니다.

- 들어 탭 아래에 있는 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **항목 선택 (그림 5 참조)** 합니다.
- 들어에 압축 하 고 AjaxControlToolkit.dll 어셈블리 선택 있는 위치로 이동 합니다.


[![도구 상자에 추가할 항목을 선택 합니다.](get-started-with-the-ajax-control-toolkit-cs/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image9.png)

**그림 05**: 도구 상자에 추가할 항목 선택 ([전체 크기 이미지를 보려면 클릭](get-started-with-the-ajax-control-toolkit-cs/_static/image10.png))


다음이 단계를 완료 한 후 도구 상자에는 도구 키트 컨트롤의 모든이 나타납니다.

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a>도구 키트의 새 버전으로 업그레이드

이전 버전의 도구 키트를 사용 하 던 이동 해야 하는 경우 최신 버전 권장된 단계와 같습니다.

- 이진 파일-웹 사이트 Bin 폴더에서 AjaxControlToolkit.dll 어셈블리의 이전 버전을 삭제 합니다.
- 도구 상자 항목-들어 탭 삭제 및 다시 AjaxControlToolkit.dll 어셈블리의 새 버전을 사용 하 여 탭을 만드는 데 위의 단계를 수행 합니다.

> [!div class="step-by-step"]
> [다음](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)
