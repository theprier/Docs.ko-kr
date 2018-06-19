---
uid: web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-vb
title: HTML 편집기 컨트롤을 사용 하려면 어떻게 해야 합니까? (VB) | Microsoft Docs
author: microsoft
description: HTMLEditor는 쉽게 작성 하 고 도구 모음 단추를 통해 HTML 콘텐츠를 편집할 수 있도록 ASP.NET AJAX 컨트롤입니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/12/2009
ms.topic: article
ms.assetid: 32ec9321-7c8c-4b0f-8234-99acb56df6b5
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 4833949a54fa9ae12eaf7b596a5fe1ddfd1f7b7a
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30873302"
---
<a name="how-do-i-use-the-html-editor-control-vb"></a>HTML 편집기 컨트롤을 사용 하려면 어떻게 해야 합니까? (VB)
====================
by [Microsoft](https://github.com/microsoft)

> HTMLEditor는 쉽게 작성 하 고 도구 모음 단추를 통해 HTML 콘텐츠를 편집할 수 있도록 ASP.NET AJAX 컨트롤입니다.


이 자습서의 목표 AJAX 컨트롤 도구 키트에 포함 된 HTML 편집기 컨트롤의 개요를 제공 하는 것입니다. HTML 편집기에 대 한 옵션이 글꼴 크기를 변경, 글꼴, 배경색을 변경, 전경색을 수정 텍스트 맞춤, 이미지, 추가 링크를 추가 하 고 수행 잘라내기, 복사 및 붙여넣기 작업 (그림 1 참조).


[![HTML 편집기](how-do-i-use-the-html-editor-control-vb/_static/image1.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image1.png)

**그림 01**: The HTML 편집기 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-html-editor-control-vb/_static/image2.png))


HTML 편집기를 사용 하면 디자인 모드를 사용 하 여 콘텐츠를 입력 하거나 HTML을 직접 입력할 수 있습니다. 또한 HTML 콘텐츠를 미리 보려면 옵션으로 제공 됩니다 (그림 2 참조).


[![디자인, HTML 및 미리 보기 단추](how-do-i-use-the-html-editor-control-vb/_static/image2.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image3.png)

**그림 02**: HTML, 디자인과 미리 보기 단추 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-html-editor-control-vb/_static/image4.png))


이 자습서에서는 HTML 편집기를 표시 하는 방법, HTML 편집기에서 표시 되는 도구 모음 단추를 사용자 지정 하는 방법 및 사이트 간 스크립팅 공격을 방지 하는 방법을 설명 합니다.

## <a name="displaying-the-html-editor"></a>HTML 편집기를 표시합니다.

HTML 편집기에서 ASP.NET 페이지를 사용 하려면 먼저 페이지에 ScriptManager 컨트롤을 먼저 추가 해야 합니다. ScriptManager 컨트롤은 Visual Studio/Visual Web Developer Express 도구 상자에서 AJAX 확장 탭 아래에 있습니다.

페이지에서 다른 컨트롤 앞에 페이지의 맨 ScriptManager 컨트롤을 배치 해야 합니다. 예를 들어 배치할 수 있습니다 즉시 열기 서버 쪽 아래 &lt;양식&gt; 태그입니다.

HTML 편집기 컨트롤은 들어 컨트롤의 다른 구성원과 도구 상자에 있습니다. 편집기 컨트롤 이름이 지정 됩니다 (그림 3 참조).


[![HTML 편집기 컨트롤](how-do-i-use-the-html-editor-control-vb/_static/image3.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image5.png)

**그림 03**: The HTML 편집기 컨트롤 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-html-editor-control-vb/_static/image6.png))


HTML 편집기 페이지를 끌어온 후 속성 시트에서 해당 속성을 설정할 수 있습니다. 예를 들어 일반적으로 원하는 너비와 높이 속성을 설정 합니다. 목록 1의 소스는 HTML 편집기를 포함 하는 ASP.NET 페이지를 포함 합니다.

**1-SimpleEditor.aspx 나열**

[!code-aspx[Main](how-do-i-use-the-html-editor-control-vb/samples/sample1.aspx)]

HTML 편집기 컨트롤, 단추 컨트롤 및 리터럴 컨트롤 목록 1의 페이지에 포함 되어 있습니다. HTML 편집기의 내용이 리터럴 제어에 표시 단추를 클릭할 때 (그림 4 참조).


[![HTML 편집기와 양식을 전송](how-do-i-use-the-html-editor-control-vb/_static/image4.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image7.png)

**그림 04**: 양식을 HTML 편집기와 전송 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-html-editor-control-vb/_static/image8.png))


HTML 편집기 Content 속성은 HTML 콘텐츠를 HTML 편집기에 입력 한 검색을 사용 합니다. 주의이 HTML 콘텐츠 JavaScript 포함 될 수 있습니다. 다음 섹션에서 JavaScript 주입 공격을 방지 하는 방법을 설명 합니다.

## <a name="customizing-the-html-editor-toolbar"></a>HTML 편집기 도구 모음 사용자 지정

정확 하 게 단추를 사용자 지정할 수는 편집기에 나타납니다. 예를 들어 다음 HTML 편집기 HTML 모드로 전환 하지 못하게 하려면 HTML 탭을 제거 하는 것이 좋습니다. 글꼴 크기 드롭다운 목록을 포럼에 과도 하 게 큰 텍스트 만들기 하지 못하게 하려면 제거 하려는 경우도 또는 메시지 post (그림 5 참조).


[![사용자 지정된 된 HTML 편집기](how-do-i-use-the-html-editor-control-vb/_static/image5.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image9.png)

**그림 05**: A HTML 편집기 사용자 지정 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-html-editor-control-vb/_static/image10.png))


새 HTML 편집기의 기본 편집기 클래스에서 파생 하 여 도구 모음 단추를 사용자 지정 합니다. 예를 들어 목록 2에서 사용자 지정 편집기 도구 모음 단추 굵게 및 기울임꼴만 포함합니다. 다른 모든 도구 모음 단추 제거 되었습니다. 또한, HTML 탭이 편집기의 맨 아래에서 제거 되었습니다 (않음 디자인 및 미리 보기 탭 아직 중지 되지 않은).

**2-응용 프로그램을 나열\_Code\CustomEditor.vb**

[!code-vb[Main](how-do-i-use-the-html-editor-control-vb/samples/sample2.vb)]

응용 프로그램에 목록 2의 클래스를 추가 해야\_클래스를 자동으로 컴파일되는 있도록 폴더를 코딩 합니다. 하는 경우 앱\_폴더를 추가 하기만 하면 다음 웹 사이트의 코드 폴더가 존재 하지 않습니다.

사용자 지정 편집기를 만든 후 있습니다 추가할 수를 ASP.NET 페이지에 같은 방식으로 일반 HTML 편집기 (참조 코드 3) 추가.

**3-ShowCustomEditor.aspx 나열**

[!code-aspx[Main](how-do-i-use-the-html-editor-control-vb/samples/sample3.aspx)]

## <a name="avoiding-cross-site-scripting-xss-attacks"></a>사이트 간 스크립팅 (XSS) 공격을 피하고

사용자 로부터 입력을 허용 하 고 웹 사이트에 해당 입력을 다시 표시 될 때마다 잠재적으로 교차 사이트 스크립팅 (XSS) 공격에 웹 사이트를 엽니다. 이론적으로, 악의적인 해커가 입력 다시 표시 되 면 실행 되는 JavaScript 코드를 제출할 수 없습니다. 사용자 암호 또는 기타 중요 한 정보를 도용 하는 JavaScript은 사용할 수 있습니다.

일반적으로 HTML 웹 페이지에 표시 하기 전에 사용자 로부터 검색할 어떤 입력 인코딩 XSS 공격 실패할 수 있습니다. 그러나 HTML HTML 편집기의 출력 인코딩 것만 인코딩하지 &lt;스크립트&gt; 태그를 모든 HTML 태그 인코딩해야 합니다. 즉, 글꼴 종류, 글꼴 크기, 배경색 등 서식을 모두는 손실 됩니다.

주민 등록 번호-암호, 신용 카드 번호 등 사용자가-중요 한 정보를 수집 하는 경우 사용자는 HTML 편집기에서 검색 하는 인코딩되지 않은 콘텐츠가 표시 되지 해야 것입니다. 신뢰할 수 있는 당사자가 웹 사이트에 HTML 콘텐츠를 다시 표시 하지는 또는 HTML 콘텐츠를 전송 하는 경우에만 HTML 편집기를 사용 해야 합니다.

예를 들어 블로그 응용 프로그램을 만들 경우 한다고 가정 합니다. 이 경우에는 블로그 게시물을 작성할 때 HTML 편집기를 사용 하려면 것이 좋습니다. 블로그 게시물을 전송 하는 유일한 한와, 아마도 악의적인 JavaScript 제출 자신 신뢰할 수 있습니다. 그러나 익명 사용자가 의견을 게시 하도록 허용 하는 경우에 HTML 편집기를 사용 하를 만들지 않습니다. 사용자는 암호 같은 중요 한 정보를 전송 하는 경우에 특히 주의 해야 합니다. 잠재적으로, 악의적인 사용자는 암호를 도용 하는 것에 대 한 올바른 JavaScript를 포함 하는 comment을 게시 합니다.

## <a name="summary"></a>요약

이 자습서에서는 들어에 포함 된 HTML 편집기 컨트롤에 간략하게 설명 함께 제공 된 있습니다. HTML 편집기를 사용 하 여 사용자 로부터 풍부한 콘텐츠를 허용 하도록 서버에 콘텐츠를 전송 하는 방법을 배웠습니다. 도 HTML 편집기에서 표시 되는 도구 모음 단추를 사용자 지정할 수는 방법을 설명 했습니다. 마지막으로, 잠재적으로 악의적인 입력을 허용 하도록 HTML 편집기를 사용할 때 교차 사이트 스크립팅 공격을 방지 하는 방법을 배웠습니다.

> [!div class="step-by-step"]
> [이전](how-do-i-use-the-html-editor-control-cs.md)
