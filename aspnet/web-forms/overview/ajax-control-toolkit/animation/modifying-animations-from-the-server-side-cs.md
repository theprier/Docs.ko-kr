---
uid: web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-cs
title: 서버 쪽 (C#)에서 애니메이션 수정 | Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. 애니메이션 있을 수 있습니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: b0abec39-a1c9-422d-ba9a-ef16f6185af8
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-cs
msc.type: authoredcontent
ms.openlocfilehash: 83ce54b1cd2c226db36be75f61321a0fb710e0ca
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37376664"
---
<a name="modifying-animations-from-the-server-side-c"></a>서버 쪽 (C#)에서 애니메이션 수정
====================
[Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9CS.pdf)

> ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. 서버 쪽에서 애니메이션 변경할 수도 있습니다.


## <a name="overview"></a>개요

ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. 서버 쪽에서 애니메이션 변경할 수도 있습니다.

## <a name="steps"></a>단계

첫째, 포함 된 `ScriptManager` 페이지 그런 다음 ASP.NET AJAX 라이브러리 로드 되 면 컨트롤 도구 키트를 사용 하 여:

[!code-aspx[Main](modifying-animations-from-the-server-side-cs/samples/sample1.aspx)]

그러면 다음과 같은 텍스트 패널에 애니메이션 적용 됩니다.

[!code-aspx[Main](modifying-animations-from-the-server-side-cs/samples/sample2.aspx)]

패널에 대 한 연결 된 CSS 클래스에 유용한 배경 색을 정의 하 고 패널 고정된 너비를 설정할 수도:

[!code-css[Main](modifying-animations-from-the-server-side-cs/samples/sample3.css)]

코드의 나머지 서버 쪽에서 실행 되 고 태그;를 사용 하지 않습니다. 대신 사용 하 여 코드 만들기는 `AnimationExtender` 제어 합니다.

[!code-aspx[Main](modifying-animations-from-the-server-side-cs/samples/sample4.aspx)]

그러나 Control Toolkit 현재 제공 하지 않습니다 개별 애니메이션 만들기에 대 한 API 액세스 합니다. 하지만 설정할 수는 `AnimationExtender`의 애니메이션 속성 문자열을 포함 하는 애니메이션을 선언적으로 할당할 때 사용 되는 XML 태그입니다. 없어야 하는 XML을 만들기 위해는 `<Animations>` .NET Framework의 XML을 사용할 수 있습니다 지원 요소나, 다음 코드와 같이 문자열을 제공 하면 됩니다.

[!code-css[Main](modifying-animations-from-the-server-side-cs/samples/sample5.css)]

마지막으로 추가 합니다 `AnimationExtender` 내 현재 페이지로 컨트롤을 `<form runat="server">` 요소에 애니메이션이 포함 되며 실행 되었는지:

[!code-html[Main](modifying-animations-from-the-server-side-cs/samples/sample6.html)]


[![서버 쪽 C# /VB 코드를 사용 하 여 애니메이션이 만들어집니다.](modifying-animations-from-the-server-side-cs/_static/image2.png)](modifying-animations-from-the-server-side-cs/_static/image1.png)

애니메이션은 서버 쪽 C# /VB 코드를 사용 하 여 생성 됩니다 ([클릭 하 여 큰 이미지 보기](modifying-animations-from-the-server-side-cs/_static/image3.png))

> [!div class="step-by-step"]
> [이전](triggering-an-animation-in-another-control-cs.md)
> [다음](executing-animations-using-client-side-code-cs.md)
