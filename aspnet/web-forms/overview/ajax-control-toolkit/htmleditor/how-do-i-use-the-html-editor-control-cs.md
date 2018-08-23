---
uid: web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-cs
title: HTML 편집기 컨트롤을 사용 하는 방법 (C#) | Microsoft Docs
author: microsoft
description: HTMLEditor에 쉽게 작성 하 고 도구 모음 단추를 통해 HTML 콘텐츠를 편집할 수 있도록 ASP.NET AJAX 컨트롤입니다.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: f47e6224-c2e5-4472-b069-b6c7b6115200
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 7bd7c5a604c897ac6dce92123e9e7ae4157d3e0e
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41829126"
---
<a name="how-do-i-use-the-html-editor-control-c"></a>HTML 편집기 컨트롤을 사용 하는 방법 (C#)
====================
[Microsoft](https://github.com/microsoft)

> HTMLEditor에 쉽게 작성 하 고 도구 모음 단추를 통해 HTML 콘텐츠를 편집할 수 있도록 ASP.NET AJAX 컨트롤입니다.


이 자습서의 목표는 AJAX Control Toolkit에 포함 된 HTML 편집기 컨트롤의 개요를 사용 하 여 제공 하는 것입니다. HTML 편집기에서 글꼴 크기를 변경, 글꼴, 배경 색을 변경, 전경색을 수정 하는 것에 대 한 옵션을 추가 하는 링크를 추가 이미지, 텍스트 맞춤을 변경 하 고 수행 잘라내기, 복사 및 붙여넣기 작업 (그림 1 참조).


[![HTML 편집기](how-do-i-use-the-html-editor-control-cs/_static/image1.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image1.png)

**그림 01**:의 HTML 편집기 ([큰 이미지를 보려면 클릭](how-do-i-use-the-html-editor-control-cs/_static/image2.png))


HTML 편집기를 사용 하면 디자인 모드를 사용 하 여 콘텐츠를 입력할 수 있습니다 또는 HTML을 직접 입력할 수 있습니다. 또한 HTML 콘텐츠를 미리 보려면 옵션으로 제공 됩니다 (그림 2 참조).


[![디자인, HTML 및 미리 보기 단추](how-do-i-use-the-html-editor-control-cs/_static/image2.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image3.png)

**그림 02**: 디자인, HTML 및 미리 보기 단추 ([큰 이미지를 보려면 클릭](how-do-i-use-the-html-editor-control-cs/_static/image4.png))


이 자습서에서는 HTML 편집기를 표시 하는 방법, HTML 편집기에서 표시 되는 도구 모음 단추를 사용자 지정 하는 방법 및 사이트 간 스크립팅 공격을 방지 하는 방법을 알아봅니다.

## <a name="displaying-the-html-editor"></a>HTML 편집기를 표시합니다.

HTML 편집기를 사용 하 여 ASP.NET 페이지에서 먼저 페이지에 ScriptManager 컨트롤을 추가 해야 합니다. ScriptManager 컨트롤은 Visual Studio/Visual Web Developer Express 도구 상자에서 AJAX 확장명 탭 아래에 있습니다.

페이지의 다른 컨트롤 보다 먼저 페이지의 맨 위에 있는 ScriptManager 컨트롤을 배치 해야 합니다. 예를 들어, 있습니다 수 아래에 배치 즉시 열기 서버측 &lt;폼&gt; 태그입니다.

HTML 편집기 컨트롤은 AJAX Control Toolkit 컨트롤의 나머지 부분을 사용 하 여 도구 상자에 있습니다. 편집기 컨트롤 지정 됩니다 (그림 3 참조).


[![HTML 편집기 컨트롤](how-do-i-use-the-html-editor-control-cs/_static/image3.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image5.png)

**그림 03**:의 HTML 편집기 컨트롤 ([큰 이미지를 보려면 클릭](how-do-i-use-the-html-editor-control-cs/_static/image6.png))


HTML 편집기를 페이지로 끌어 후 속성 시트에서 해당 속성을 설정할 수 있습니다. 예를 들어, 일반적으로 하려는 Width와 Height 속성을 설정 합니다. 목록 1 HTML 편집기를 포함 하는 ASP.NET 페이지에 대 한 원본을 포함 합니다.

**1-SimpleEditor.aspx 나열**

[!code-aspx[Main](how-do-i-use-the-html-editor-control-cs/samples/sample1.aspx)]

목록 1에서 페이지에는 HTML 편집기 컨트롤 및 단추 컨트롤을 리터럴 컨트롤을 포함 합니다. 리터럴 컨트롤의 HTML 편집기의 내용을 표시 단추를 클릭 하면 (그림 4 참조).


[![HTML 편집기 사용 하 여 양식을 제출](how-do-i-use-the-html-editor-control-cs/_static/image4.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image7.png)

**그림 04**: HTML 편집기 사용 하 여 양식을 제출 ([큰 이미지를 보려면 클릭](how-do-i-use-the-html-editor-control-cs/_static/image8.png))


HTML 편집기 콘텐츠 속성은 HTML 편집기에 입력 된 HTML 콘텐츠를 검색에 사용 됩니다. 이 HTML 콘텐츠에 JavaScript를 포함할 수 있음을 알아야 합니다. 다음 섹션에서는 JavaScript 주입 공격을 방지 하는 방법을 설명 합니다.

## <a name="customizing-the-html-editor-toolbar"></a>HTML 편집기 도구 모음 사용자 지정

정확 하 게 단추를 사용자 지정할 수 있습니다 편집기에 표시 합니다. 예를 들어 다음 HTML 편집기를 HTML 모드로 전환 하지 못하게 하려면 HTML 탭을 제거 하는 것이 좋습니다. 글꼴 크기 드롭다운 목록을 포럼에서 과도 하 게 큰 텍스트를 작성 하지 못하게 하려면 제거 하려는 또는 후에 메시지 (그림 5 참조).


[![사용자 지정된 된 HTML 편집기](how-do-i-use-the-html-editor-control-cs/_static/image5.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image9.png)

**그림 05**:는 HTML 편집기 사용자 지정 ([큰 이미지를 보려면 클릭](how-do-i-use-the-html-editor-control-cs/_static/image10.png))


새 HTML 편집기의 기본 편집기 클래스에서 파생 하 여 도구 모음 단추를 사용자 지정 합니다. 예를 들어 목록 2에서 사용자 지정 편집기 도구 모음 단추 굵게 및 기울임꼴만 포함합니다. 다른 모든 도구 모음 단추 제거 되었습니다. 또한 HTML 탭이 편집기의 맨 아래에서 제거 되었습니다 (있지만 디자인 및 미리 보기 탭은 여전히 남아 있습니다.)

**2-앱을 나열\_Code\CustomEditor.cs**

[!code-csharp[Main](how-do-i-use-the-html-editor-control-cs/samples/sample2.cs)]

앱에 코드 2에서 클래스를 추가 해야\_클래스는 자동으로 컴파일할 수 있도록 폴더를 코딩 합니다. 하는 경우 앱\_코드 폴더에 웹 사이트에 없는 경우 다음 폴더를 간단히 추가할 수 있습니다.

사용자 지정 편집기를 만든 후 추가할 수 있습니다이 ASP.NET 페이지에 동일한 방식으로 일반 HTML 편집기 (참조 코드 3)을 추가.

**3-ShowCustomEditor.aspx 나열**

[!code-aspx[Main](how-do-i-use-the-html-editor-control-cs/samples/sample3.aspx)]

## <a name="avoiding-cross-site-scripting-xss-attacks"></a>사이트 간 스크립팅 (XSS) 공격 방지

사용자 로부터 입력을 허용 하 고 웹 사이트에 해당 입력을 다시 표시 될 때마다 잠재적으로 교차 사이트 스크립팅 (XSS) 공격에 웹 사이트를 엽니다. 이론적으로 악의적인 해커에 게 입력이 다시 표시 하는 경우 실행 되는 JavaScript 코드를 제출할 수 있습니다. 사용자 암호 또는 기타 중요 한 정보를 도용 하는 JavaScript은 사용할 수 있습니다.

일반적으로 HTML 웹 페이지에 표시 하기 전에 사용자 로부터 검색 입력 인코딩 XSS 공격에 무효화 될 수 있습니다. 그러나 HTML 인코딩 출력 HTML 편집기의 것만 인코딩하지 &lt;스크립트&gt; 태그 모든 HTML 태그를 인코딩할 수도 됩니다. 즉, 글꼴, 글꼴 크기, 배경 색 등 서식을 모두 잃게 됩니다.

다음으로 사용자-암호, 신용 카드 번호와 사회 보장 번호-등의 중요 한 정보를 수집 하는 경우 HTML 편집기를 사용 하 여 사용자를 검색 하는 인코딩되지 않은 내용으로 표시 됩니다. 신뢰할 수 있는 당사자가 웹 사이트에 있는 HTML 콘텐츠를 표시 하지는 또는 HTML 콘텐츠를 전송 하는 경우에만 HTML 편집기를 사용 해야 합니다.

예를 들어 블로그 응용 프로그램을 만든다고 가정해 보겠습니다. 이 이런 경우에 블로그 게시물을 작성할 때 HTML 편집기를 사용 하려면 것이 좋습니다. 블로그 게시물을 제출 하는 유일한와, 아마도 악성 JavaScript를 제출할 필요가 직접 신뢰할 수 있습니다. 그러나 익명 사용자가 의견을 게시 하도록 허용 하는 경우 HTML 편집기를 사용 하는 것이 확인 하지 않습니다. 사용자는 암호와 같은 중요 한 정보를 제출 하는 경우에 특히 주의 해야 합니다. 잠재적으로 악의적인 사용자 암호를 도용 하는 것에 대 한 올바른 JavaScript를 포함 하는 주석을 게시할 수 있습니다.

## <a name="summary"></a>요약

이 자습서에서는 AJAX Control Toolkit에 포함 된 HTML 편집기 컨트롤의 간략 한 개요를 제공 된 있습니다. HTML 편집기를 사용 하 여 사용자 로부터 풍부한 콘텐츠를 적용 하 고 서버에 콘텐츠를 제출 하는 방법을 알아보았습니다. 또한 HTML 편집기에서 표시 되는 도구 모음 단추를 사용자 지정할 수 있습니다 하는 방법을 설명 했습니다. 마지막으로, 잠재적으로 악의적인 입력을 허용 하도록 HTML 편집기를 사용 하는 경우 사이트 간 스크립팅 공격을 방지 하는 방법을 알아보았습니다.

> [!div class="step-by-step"]
> [다음](how-do-i-use-the-html-editor-control-vb.md)
