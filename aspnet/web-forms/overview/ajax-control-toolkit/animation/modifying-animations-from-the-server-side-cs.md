---
uid: web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-cs
title: 서버 쪽 (C#)에서 애니메이션 수정 | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크. 애니메이션 있을 수 있습니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: b0abec39-a1c9-422d-ba9a-ef16f6185af8
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-cs
msc.type: authoredcontent
ms.openlocfilehash: 6946875552c885ffb1f2a2eb7e728b85d7dd3973
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="modifying-animations-from-the-server-side-c"></a>서버 쪽 (C#)에서 애니메이션 수정
====================
으로 [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9CS.pdf)

> ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크. 애니메이션 서버 쪽에도 변경 될 수 있습니다.


## <a name="overview"></a>개요

ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크. 애니메이션 서버 쪽에도 변경 될 수 있습니다.

## <a name="steps"></a>단계

우선, 포함 된 `ScriptManager` 페이지; 그런 다음 ASP.NET AJAX 라이브러리 로드 되는 제어 도구 키트를 사용 하 여:

[!code-aspx[Main](modifying-animations-from-the-server-side-cs/samples/sample1.aspx)]

그러면 다음과 같은 텍스트의 패널에 애니메이션 적용 됩니다.

[!code-aspx[Main](modifying-animations-from-the-server-side-cs/samples/sample2.aspx)]

패널에 대 한 연결 된 CSS 클래스 좋은 배경색을 정의 하 고도 패널 고정된 폭을 설정 합니다.

[!code-css[Main](modifying-animations-from-the-server-side-cs/samples/sample3.css)]

코드의 나머지 서버 쪽에서 실행 되 고 태그; 사용 하지 않습니다. 대신, 사용 하 여 코드를 만드는 `AnimationExtender` 제어:

[!code-aspx[Main](modifying-animations-from-the-server-side-cs/samples/sample4.aspx)]

그러나 컨트롤 Toolkit 현재 제공 하지 않습니다 개별 애니메이션 만들기에 대 한 API 액세스 합니다. 그러나 설정 하 고는 `AnimationExtender`의 애니메이션 속성을 문자열로 애니메이션을 선언적으로 지정할 때 사용 되는 XML 태그를 포함 합니다. 포함 되지 않아야 하는 XML을 만들기 위해는 `<Animations>` 요소는.NET Framework의 XML을 사용할 수 있습니다 지원 하거나, 다음 코드 에서처럼 방금 제공 된 문자열:

[!code-css[Main](modifying-animations-from-the-server-side-cs/samples/sample5.css)]

마지막으로 추가 된 `AnimationExtender` 내 컨트롤을 현재 페이지는 `<form runat="server">` 애니메이션 포함 되어 있고 실행 요소:

[!code-html[Main](modifying-animations-from-the-server-side-cs/samples/sample6.html)]


[![C# /VB 서버 쪽 코드를 사용 하 여 애니메이션이 만들어집니다.](modifying-animations-from-the-server-side-cs/_static/image2.png)](modifying-animations-from-the-server-side-cs/_static/image1.png)

C# /VB 서버 쪽 코드를 사용 하 여 애니메이션 만들어집니다 ([전체 크기 이미지를 보려면 클릭](modifying-animations-from-the-server-side-cs/_static/image3.png))

> [!div class="step-by-step"]
> [이전](triggering-an-animation-in-another-control-cs.md)
> [다음](executing-animations-using-client-side-code-cs.md)
