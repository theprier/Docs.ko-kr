---
uid: web-forms/overview/getting-started/creating-a-basic-web-forms-page
title: "기본 ASP.NET 4.5 Web Forms 만들기 페이지 Visual Studio 2013에서 | Microsoft Docs"
author: Erikre
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/03/2014
ms.topic: article
ms.assetid: a2f1c635-0817-4a9a-8c13-d5b5d29727c0
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/getting-started/creating-a-basic-web-forms-page
msc.type: authoredcontent
ms.openlocfilehash: 20e920ff63444c0d69cecb972619b07fe6d23097
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="creating-a-basic-aspnet-45-web-forms-page-in-visual-studio-2013"></a>기본 ASP.NET 4.5 Web Forms 만들기 페이지에서 Visual Studio 2013
====================
으로 [Erik Reitan](https://github.com/Erikre)

이 연습에서 웹 개발 환경에 대 한 소개를 제공 [Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/en-us/downloads#vs) 및 [Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/en-us/downloads#express-web)합니다. 이 연습에서는 간단한 ASP.NET Web Forms 페이지를 만드는 과정을 안내 하 고 새 페이지를 만드는 컨트롤을 추가 하 고 코드를 작성 하는 기본적인 기술을 보여 줍니다.

이 연습에서 설명하는 작업은 다음과 같습니다.

- 파일 시스템 Web Forms 응용 프로그램 프로젝트를 만드는 중입니다.
- Visual Studio와 함께 파악 합니다.
- ASP.NET 페이지를 만듭니다.
- 컨트롤을 추가 합니다.
- 이벤트 처리기를 추가 합니다.
- 실행 하 고 Visual Studio에서 페이지를 테스트 합니다.

## <a name="prerequisites"></a>필수 구성 요소


이 연습을 완료하려면 다음 사항이 필요합니다.

- [Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/en-us/downloads#vs) 또는 [Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/en-us/downloads#express-web)합니다. .NET Framework는 자동으로 설치 됩니다. 

    > [!NOTE] 
    > 
    > Microsoft Visual Studio 2013 및 Microsoft Visual Studio Express 2013 for Web은 종종로 간주 Visual Studio이 자습서 시리즈 합니다.  
    >   
    > 이 연습에서는 선택 했다고 가정 Visual Studio를 사용 하는 경우는 **웹 개발** 설정의 컬렉션 처음으로 Visual Studio를 시작 합니다. 자세한 내용은 참조 [하는 방법: 웹 개발 환경 설정 선택](https://msdn.microsoft.com/library/ff521558.aspx)합니다.


## <a name="creating-a-web-application-project-and-a-page"></a>웹 응용 프로그램 프로젝트 및 페이지 만들기

<a id="sectionToggle0"></a>

이 연습 부분에서는 웹 응용 프로그램 프로젝트를 만들고 새 페이지를 추가 합니다. HTML 텍스트를 추가 및 브라우저에서 페이지를 실행도 있습니다.

### <a name="to-create-a-web-application-project"></a>웹 응용 프로그램 프로젝트를 만들려면

1. Microsoft Visual Studio를 엽니다.
2. **파일** 메뉴에서 **새 프로젝트**를 선택합니다.  
    ![파일 메뉴](creating-a-basic-web-forms-page/_static/image1.png)

    **새 프로젝트** 대화 상자가 나타납니다.
3. 선택 된 **템플릿**  - &gt; **Visual C#**  - &gt; **웹** 왼쪽의 템플릿 그룹.
4. 선택 된 **ASP.NET 웹 응용 프로그램** 가운데 열에서 서식 파일입니다.
5. 프로젝트 이름을 ***BasicWebApp*** 클릭는 **확인** 단추입니다.   
![새 프로젝트 대화 상자](creating-a-basic-web-forms-page/_static/image2.png)
6. 다음으로, 선택는 **Web Forms** 템플릿과 클릭은 **확인** 단추 프로젝트를 만듭니다.  
![새 ASP.NET 프로젝트 대화 상자](creating-a-basic-web-forms-page/_static/image3.png)  

    Visual Studio Web Forms 템플릿을 기반으로 하는 미리 작성 된 기능을 포함 하는 새 프로젝트를 만듭니다. 뿐만 아니라 제공 하는 *Home.aspx* 페이지는 *About.aspx* 페이지는 *Contact.aspx* 페이지 하지만 사용자가 등록 하 고 저장 하는 멤버 자격 기능을 포함 자격 증명 웹 사이트에 로그인 할 수 있도록 합니다. 새 페이지를 만들면 기본적으로 Visual Studio 표시에 있는 페이지 **소스** 페이지의 HTML 요소를 볼 수 있습니다. 다음 그림에 표시 되는 것에 나와 **소스** 라는 새 웹 페이지를 만들면 볼 *BasicWebApp.aspx*합니다.  
    ![소스 뷰](creating-a-basic-web-forms-page/_static/image4.png)


### <a name="a-tour-of-the-visual-studio-web-development-environment"></a>Visual Studio 웹 개발 환경의 둘러보기


페이지를 수정 하 여 계속 진행 하기 전에 Visual Studio 개발 환경에 익숙해질 수는 것이 유용 합니다. 다음 그림에는 windows 및 Visual Studio 및 Visual Studio Express for Web에서 사용할 수 있는 도구를 보여줍니다.

> [!NOTE] 
> 
> 이 다이어그램에서는 기본 창 및 창 위치를 보여 줍니다. **보기** 메뉴 추가 창을 표시할 다시 정렬 하 고 windows 사용자 기본 설정에 맞게 크기를 조정할 수 있습니다. 변경 내용이 이미 창 정렬에 적용 된 경우 나타나는 일치 하지 않습니다는 그림입니다.


 Visual Studio 환경

![Visual Studio 환경](creating-a-basic-web-forms-page/_static/image5.png)

### <a name="familiarize-yourself-with-the-web-designer"></a>웹 디자이너를 파악

위의 그림을 검토 하 고 다음 목록을 텍스트와 일치 한 창과 도구에 사용 되는 가장 일반적으로 설명 하는 합니다. (모든 창과 도구는 다음과 같은 볼 수 있는 표시 된 것만 앞의 그림에서입니다.)

- 도구 모음입니다. 텍스트, 텍스트 찾기 및에 서식을 지정 하기 위한 명령을 제공 합니다. 일부 도구 모음은에서 작업 하는 경우에 사용할 수 있는 **디자인** 보기.
- **솔루션 탐색기** 창. 웹 응용 프로그램에서 파일 및 폴더를 표시합니다.
- 문서 창입니다. 탭된 창에서 작업 하는 문서가 표시 됩니다. 탭을 클릭 하 여 문서 간에 전환할 수 있습니다.
- **속성** 창. 페이지, HTML 요소, 컨트롤 및 기타 개체에 대 한 설정을 변경할 수 있습니다.
- 보기 탭 합니다. 같은 문서에 대해 서로 다른 뷰를 표시 합니다. **디자인** 뷰는 WYSIWYG 편집 화면입니다. **소스** 보기는 HTML 편집기의 페이지입니다. **분할** 모두 뷰의 표시는 **디자인** 보기 및 **소스** 문서에 대 한 보기입니다. 작업을 수행는 **디자인** 및 **소스** 이 연습의 뒷부분에서 뷰. 웹 페이지를 열려면 선호 하는 경우 **디자인** 를 보려면는 **도구** 메뉴를 클릭 하 여 **옵션**을 선택는 **HTML 디자이너** 노드와 변경은 **에 페이지 시작** 옵션입니다.
- **도구 상자**합니다. 컨트롤 및 페이지로 끌어올 수 있는 HTML 요소를 제공 합니다. **도구 상자** 요소 공통 기능에 따라 그룹화 됩니다.
- S **erver 탐색기**합니다. 데이터베이스 연결을 표시 합니다. 서버 탐색기가 표시 되지 않는 경우 보기 메뉴에서 서버 탐색기를 클릭 합니다.


### <a name="creating-a-new-aspnet-web-forms-page"></a>새 ASP.NET Web Forms 페이지 만들기


사용 하 여 새 Web Forms 응용 프로그램을 만들 때는 **ASP.NET 웹 응용 프로그램** 프로젝트 템플릿을 Visual Studio 추가 라는 ASP.NET 페이지 (Web Forms 페이지) *Default.aspx*다른 여러 파일 외에, 및 폴더입니다. 사용할 수는 *Default.aspx* 웹 응용 프로그램에 대 한 홈 페이지와 페이지입니다. 그러나이 연습에서는 만들고 새 페이지를 사용 합니다.

### <a name="to-add-a-page-to-the-web-application"></a>웹 응용 프로그램 페이지를 추가 하려면


1. 닫기는 *Default.aspx* 페이지. 이렇게 하려면 파일 이름을 표시 하는 탭을 클릭 하 고 닫기 옵션을 클릭 합니다.
2. **솔루션 탐색기**, 웹 응용 프로그램 이름을 마우스 오른쪽 단추로 클릭 (응용 프로그램 이름이이 자습서에서는 **BasicWebSite**)를 클릭 하 고 **추가**  - &gt; **새 항목**합니다.   
**새 항목 추가** 대화 상자가 표시됩니다.
3. 선택 된 **Visual C#**  - &gt; **웹** 왼쪽의 템플릿 그룹입니다. 그런 다음 선택 **Web Form** 중간에서 나열 하 고 이름을 *FirstWebPage.aspx*합니다.   
    ![새 항목 추가 대화 상자](creating-a-basic-web-forms-page/_static/image6.png)
4. 클릭 **추가** 를 웹 페이지 프로젝트를 추가 합니다.  
Visual Studio에 새 페이지에 만들어지고 열립니다.


### <a name="adding-html-to-the-page"></a>페이지에 HTML 추가


이 연습 부분에서는 페이지에 몇 가지 정적 텍스트를 추가 합니다.

### <a name="to-add-text-to-the-page"></a>페이지에 텍스트를 추가 하려면


1. 문서 창의 아래쪽을 클릭는 **디자인** 진행 **디자인** 보기.

    디자인 뷰는 WYSIWYG와 유사한 방식으로 현재 페이지를 표시합니다. 이 시점에서 텍스트 또는 페이지의 컨트롤에 없으므로 파선 사각형의 윤곽선을 제외 하 고 페이지가 비어 있습니다. 이 사각형이 나타내는 **div** 페이지에서 요소입니다.
2. 점선으로 둘러싸여 사각형 내부를 클릭 합니다.
3. 형식 **Visual Web Developer 시작** 누릅니다 **ENTER** 두 번입니다.

    다음 그림에 입력 한 텍스트를 보여 줍니다. **디자인** 보기.

    ![디자인 뷰의 환영 텍스트](creating-a-basic-web-forms-page/_static/image7.png "디자인 뷰의 환영 텍스트")
4. 로 전환 **소스** 보기.

    HTML을 볼 수 **소스** 에 입력할 때 만든 보기 **디자인** 보기.  
    ![정적 텍스트와 웹 페이지](creating-a-basic-web-forms-page/_static/image8.png)


### <a name="running-the-page"></a>페이지를 실행 하면


페이지에 컨트롤을 추가 하 여 계속 진행 하기 전에 먼저 실행할 수 있습니다.

### <a name="to-run-the-page"></a>페이지를 실행 하려면


1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 *FirstWebPage.aspx* 선택 **시작 페이지로 설정**합니다.
2. 키를 눌러 **CTRL + f 5** 페이지를 실행 합니다.

    페이지는 브라우저에 표시 됩니다. 만든 페이지의 파일 이름 확장자가 있지만 *.aspx*, HTML 페이지 처럼 현재 실행 합니다.

    브라우저에서 페이지를 표시 하려면 스키마에 있는 페이지 **솔루션 탐색기** 선택 **브라우저에서 보기**합니다.
3. 웹 응용 프로그램을 중지 하려면 브라우저를 닫습니다.


## <a name="adding-and-programming-controls"></a>컨트롤 추가 및 프로그래밍


<a id="sectionToggle1"></a>

이제 페이지에 서버 컨트롤을 추가 합니다. 서버 컨트롤 단추, 레이블, 입력란 및 기타 친숙 한 컨트롤 같은 Web Forms 페이지에 대 한 일반적인 양식 처리 기능을 제공합니다. 그러나 클라이언트가 아닌 서버에서 실행 되는 코드를 사용 하 여 컨트롤을 프로그래밍할 수 있습니다.

추가 합니다는 [단추](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) 컨트롤은 [텍스트 상자에 붙여넣습니다](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) 컨트롤 및 [레이블](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) 처리할 코드를 작성 하 고 컨트롤을 페이지는 [클릭](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) 에 대 한 이벤트 [단추](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) 제어 합니다.

### <a name="to-add-controls-to-the-page"></a>페이지에 컨트롤을 추가 하려면


1. 클릭는 **디자인** 진행 **디자인** 보기.
2. 끝에 삽입 포인터를 놓습니다는 **Visual Web Developer 시작** 텍스트와 키를 눌러 **ENTER** 공간을 확보의 5 배는 **div** 요소 상자입니다.
3. 에 **도구 상자**를 확장 하 고는 **표준** 확장 되어 있지 않은 경우 그룹화 합니다.  
확장 해야 할 수는 **도구 상자** 볼 왼쪽 창.
4. 끌어서는 [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) 컨트롤을 페이지로 끌어서 가운데는 **div** 가 있는 요소 상자 **Visual Web Developer를 시작** 첫 번째 줄에서.
5. 끌어서는 [단추](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) 컨트롤을 페이지로 오른쪽에 놓습니다는 [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) 제어 합니다.
6. 끌어서는 [레이블](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) 컨트롤을 페이지로 별도 줄 아래에 놓습니다는 [단추](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) 제어 합니다.
7. 위의 삽입 지점을 [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) 컨트롤을 선택한 다음 입력 **이름 입력:** 합니다.

    이 정적 HTML 텍스트에 대 한 기본값은는 [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) 제어 합니다. 정적 HTML과 같은 페이지에 서버 컨트롤을 혼합할 수 있습니다. 다음 그림에 세 개의 컨트롤이 표시 하는 방법을 보여 줍니다. **디자인** 보기.

    ![디자인 뷰에서 세 가지 컨트롤](creating-a-basic-web-forms-page/_static/image9.png "디자인 보기에서 세 가지 컨트롤")


### <a name="setting-control-properties"></a>컨트롤 속성 설정


Visual Studio는 페이지에 있는 컨트롤의 속성을 설정 하는 다양 한 방법을 제공 합니다. 이 연습 부분에서는 모두에서 속성을 설정 합니다 **디자인** 보기 및 **소스** 보기.

### <a name="to-set-control-properties"></a>컨트롤 속성을 설정 하려면


1. 먼저, 표시 된 **속성** 에서 선택 하 여 windows는 **보기** 메뉴-&gt; **다른 창**  - &gt; **속성 창**합니다. 또는 선택할 수 있습니다 **F4** 표시 하는 **속성** 창.
2. 선택의 [단추](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) 컨트롤을 선택한 다음는 **속성** 창의 설정의 값 **텍스트** 를 **표시 이름**합니다. 다음 그림에 나와 있는 것 처럼 입력 한 텍스트는 디자이너의 단추에 표시 됩니다.

    ![단추 텍스트 설정](creating-a-basic-web-forms-page/_static/image10.png "설정 단추 텍스트")
3. 로 전환 **소스** 보기.

    **소스** 보기에는 HTML 서버 컨트롤에 대 한 Visual Studio가 생성 하는 요소를 포함 하 여 페이지에 표시 됩니다. 컨트롤이 선언 된 HTML과 유사한 구문을 사용 하 여 태그 접두사를 사용 하는 점을 제외 하 고 **asp:** 특성을 포함 하 고 **runat =&quot;서버&quot;**합니다.

    컨트롤 속성은 특성으로 선언 됩니다. 설정한 경우에 예를 들어는 [텍스트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.text.aspx) 속성에 대 한는 [단추](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) 제어 하 고, 1 단계에서 실제로 설정할는 **텍스트** 컨트롤의 태그에 특성입니다.

    > [!NOTE] 
    > 
    > 내 모든 컨트롤은 한 **양식** 특성도 포함 하는 요소를 **runat =&quot;서버&quot;**합니다. **runat =&quot;서버&quot;**  특성 및 **asp:** 접두사 컨트롤 태그 페이지를 실행할 때 서버에서 ASP.NET에서 처리 되기 있도록 컨트롤을 표시 합니다. 외부 코드  **&lt;runat =&quot;서버&quot; &gt;**  및  **&lt;스크립트 runat =&quot;서버&quot; &gt;**  요소를 브라우저에도 때문에 ASP.NET 코드는 여는 태그를 포함 하는 요소 내부에 있어야 합니다. 변경 되지 않은 전송 되는 **runat =&quot;서버&quot;**  특성입니다.
4. 다음을 추가 속성을 추가 합니다는 [레이블](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) 제어 합니다. 후 직접 삽입 지점을 **p: Label** 에  **&lt;p: Label&gt;**  태그, 및 키를 누릅니다 **스페이스바**합니다.

    설정할 수 있는 사용 가능한 속성의 목록을 표시 하는 드롭다운 목록이 나타납니다는 [레이블](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) 제어 합니다. 이 기능으로 이라고 **IntelliSense**에서 사용 하면 **소스** 페이지에 서버 컨트롤, HTML 요소 및 기타 항목의 구문 보기. 다음 그림에서는 **IntelliSense** 에 대 한 드롭다운 목록에서 [레이블](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) 제어 합니다.

    ![IntelliSense 특성](creating-a-basic-web-forms-page/_static/image11.png "IntelliSense 특성")
5. 선택 **ForeColor** 등호를 입력 합니다.

    IntelliSense의 색상 목록을 표시합니다.

    > [!NOTE] 
    > 
    > 표시할 수 있습니다는 **IntelliSense** 드롭다운 목록에서 키를 눌러 언제 든 **CTRL + J** 코드를 볼 때.
6. 색을 선택 된  **[레이블](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)**  컨트롤의 텍스트입니다. 흰색 배경에서 읽을 수 있도록 어두운 색을 선택 해야 합니다.

    **ForeColor** 특성 닫는 따옴표를 포함 하 여, 선택 된 색으로 완료 됩니다.


### <a name="programming-the-button-control"></a>Button 컨트롤 프로그래밍


이 연습에서는 사용자가 텍스트 상자에 입력 하 고 다음의 이름을 표시 이름을 읽는 코드를 작성 합니다는 [레이블](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) 제어 합니다.

### <a name="add-a-default-button-event-handler"></a>기본 단추 이벤트 처리기를 추가 합니다.


1. 로 전환 **디자인** 보기.
2. 두 번 클릭 하 여 [단추](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) 제어 합니다.

    기본적으로 Visual Studio 코드 숨김 파일을 전환 하 고에 대 한 기본 이벤트 처리기를 만듭니다는 [단추](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) 컨트롤의 기본 이벤트는 [클릭](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) 이벤트입니다. 코드 숨김 파일 (예: C#) 서버 코드에서 UI 태그 (예: HTML)를 구분합니다.   
이 이벤트 처리기에 대 한 코드를 추가 하는 커서에 배치 됩니다.

    > [!NOTE] 
    > 
    > 에 컨트롤을 두 번 클릭 하면 **디자인** 보기는 이벤트 처리기를 만들 수는 몇 가지 방법 중 하나일 뿐입니다.
3. 내에서 **Button1\_클릭** 이벤트 처리기, 형식 **Label1** 뒤에 마침표 (**.**).

    뒤에 마침표를 입력할 경우는 **ID** 레이블 (**Label1**), Visual Studio에 대 한 사용 가능한 구성원 목록이 표시 됩니다는 [레이블](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) 다음에 표시 된 대로 제어 그림입니다. 멤버 속성에 일반적으로, 메서드 또는 이벤트입니다.

    ![코드 보기의 IntelliSense](creating-a-basic-web-forms-page/_static/image12.png "코드 보기의 IntelliSense")
4. 완료 된 **클릭** 다음 코드 예제와 같이 표시 되도록 단추에 대 한 이벤트 처리기입니다.

    [!code-csharp[Main](creating-a-basic-web-forms-page/samples/sample1.cs?highlight=3)]

    [!code-vb[Main](creating-a-basic-web-forms-page/samples/sample2.vb?highlight=2)]
5. 보기로 다시 전환는 **소스** 마우스 오른쪽 단추로 클릭 하 여 HTML 태그의 보기 *FirstWebPage.aspx* 에 **솔루션 탐색기** 선택 하 고 **보기 태그**합니다.
6. 스크롤하여는  **&lt;p: Button&gt;**  요소입니다.  **&lt;p: Button&gt;**  이제 특성이 요소 **onclick =&quot;Button1\_클릭&quot;**합니다.

    이 특성 단추의 바인딩합니다 [클릭](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) 이전 단계에서 코딩 된 처리기 메서드를 이벤트입니다.

    이벤트 처리기 메서드 이름에는 제한이 있습니다. 표시 되는 이름에는 Visual Studio에서 만든 기본 이름이입니다. 중요 한 점은 이름을 사용 하는 **OnClick** html에서 특성 코드 숨김에 정의 된 메서드의 이름과 일치 해야 합니다.


### <a name="running-the-page"></a>페이지를 실행 하면


이제 페이지에서 서버 컨트롤을 테스트할 수 있습니다.

### <a name="to-run-the-page"></a>페이지를 실행 하려면


1. 키를 눌러 **CTRL + f 5** 브라우저에서 페이지를 실행 합니다. 오류가 발생 하는 경우 위의 단계를 다시 확인 합니다.
2. 텍스트 상자에 이름을 입력 하 고 클릭 하 고 **표시 이름** 단추입니다.

    입력 한 이름이 표시 됩니다는 [레이블](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) 제어 합니다. 참고 단추를 클릭할 때 페이지는 웹 서버에 게시 됩니다. 그런 다음 ASP.NET 페이지를 다시 만듭니다, 코드를 실행 (이 경우는 [단추](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) 컨트롤의 [클릭](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) 이벤트 처리기가 실행), 한 다음 새 페이지를 브라우저에 보냅니다. 브라우저에서 상태 표시줄을 시청 하는 경우에 페이지는 라운드트립이 수행 웹 서버에 단추를 클릭할 때마다 볼 수 있습니다.
3. 브라우저에서 페이지를 마우스 오른쪽 단추로 클릭 하 고 선택 하 여 실행 중인 페이지의 소스를 보려면 **소스 보기**합니다.

    페이지 소스 코드에 서버 코드 없이 HTML을 표시 합니다. 특히, 표시 되지 않으면는  **&lt;asp:&gt;**  에서 작업 하는 요소 **소스** 보기. 페이지를 실행 하는 경우 ASP.NET 서버 컨트롤을 처리 하 고 컨트롤을 나타내는 기능을 수행 하는 페이지에 HTML 요소를 렌더링 합니다. 예를 들어는  **&lt;p: Button&gt;**  컨트롤이 HTML로 렌더링 되는지  **&lt;입력 형식 =&quot;제출&quot; &gt;**  요소입니다.
4. 브라우저를 닫습니다.


## <a name="working-with-additional-controls"></a>추가 컨트롤 작업

<a id="sectionToggle2"></a>

이 연습 부분에서는을 사용 합니다는 [달력](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) 컨트롤을 한 번에 한 달의 날짜를 표시 합니다. [달력](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) 컨트롤은 작업 중인 단추, 텍스트 상자 및 레이블을 보다 더 복잡 한 컨트롤 하 고 서버 컨트롤의 몇 가지 추가 기능을 보여 줍니다.

이 섹션에서는 추가 됩니다 한 [System.Web.UI.WebControls.Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) 페이지를 제어 하 고 서식을 지정 합니다.

### <a name="to-add-a-calendar-control"></a>달력 컨트롤을 추가 하려면


1. Visual Studio로 전환 **디자인** 보기.
2. **표준** 의 섹션은 **도구 상자**를 끌어는 [달력](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) 컨트롤을 페이지로 아래로 끌어다 놓습니다는 **div** 요소는 다른 컨트롤을 포함 합니다.

    달력의 스마트 태그 패널이 표시 됩니다. 패널에는 쉽게 선택된 된 컨트롤에 대 한 가장 일반적인 작업을 수행할 수 있는 명령이 표시 됩니다. 다음 그림에서는 [달력](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) 에서 렌더링 된 제어 **디자인** 보기.

    ![디자인 뷰에서 컨트롤 달력](creating-a-basic-web-forms-page/_static/image13.png "디자인 뷰에서 컨트롤 달력")
3. 스마트 태그 패널에서 선택 **자동 서식**합니다.

    **자동 서식** 달력에 대 한 서식 구성표를 선택할 수 있는 대화 상자가 표시 됩니다. 다음 그림에서는 **자동 서식** 에 대 한 대화 상자는 [달력](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) 제어 합니다.

    ![자동 서식 대화 상자 (Calendar 컨트롤)](creating-a-basic-web-forms-page/_static/image14.png "자동 서식 대화 상자 (Calendar 컨트롤)")
4. **구성표 선택** 목록에서 선택 **간단한** 클릭 하 고 **확인**합니다.
5. 로 전환 **소스** 보기.

    볼 수는  **&lt;asp: 달력&gt;**  요소입니다. 이 요소는 요소 앞에서 만든 단순 컨트롤에 대 한 보다 훨씬 깁니다. 도 하위 요소와 같은  **&lt;WeekEndDayStyle&gt;**, 있으며 다양 한 서식 설정을 나타냅니다. 다음 그림에서는 [달력](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) 제어 **소스** 보기. (에 표시 되는 실제 태그 **소스** 뷰 그림에서 약간 달라질 수 있습니다.)

    ![소스 뷰에서 컨트롤 달력](creating-a-basic-web-forms-page/_static/image15.png "소스 뷰에서 컨트롤 달력")


### <a name="programming-the-calendar-control"></a>Calendar 컨트롤 프로그래밍


이 섹션에서는 프로그래밍 합니다는 [달력](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) 컨트롤에 현재 선택 된 날짜를 표시 합니다.

### <a name="to-program-the-calendar-control"></a>달력 컨트롤을 프로그래밍 하려면


1. **디자인** 보기에서 두 번 클릭은 [달력](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) 제어 합니다.

    새 이벤트 처리기를 생성 하 라는 코드 숨김 파일에 표시 *FirstWebPage.aspx.cs*합니다.
2. 완료 된 [SelectionChanged](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.selectionchanged.aspx) 이벤트 처리기를 다음 코드로 합니다.


    [!code-csharp[Main](creating-a-basic-web-forms-page/samples/sample3.cs?highlight=3)]


    [!code-vb[Main](creating-a-basic-web-forms-page/samples/sample4.vb?highlight=2)]

 위의 코드는 달력 컨트롤에서 선택한 날짜에 레이블 컨트롤의 텍스트를 설정합니다.


### <a name="running-the-page"></a>페이지를 실행 하면


이제 달력을 테스트할 수 있습니다.

### <a name="to-run-the-page"></a>페이지를 실행 하려면


1. 키를 눌러 **CTRL + f 5** 브라우저에서 페이지를 실행 합니다.
2. 달력에서 날짜를 클릭 합니다.

    에 클릭 한 날짜가 표시 됩니다는 [레이블](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) 제어 합니다.
3. 브라우저에서 페이지에 대 한 소스 코드를 봅니다.

    [달력](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) 컨트롤이 페이지에 렌더링 된는 **테이블**, 각 날짜는 **td** 요소입니다.
4. 브라우저를 닫습니다.


## <a name="next-steps"></a>다음 단계


<a id="nextStepsToggle"></a>

이 연습에서는 Visual Studio 페이지 디자이너의 기본 기능에 설명 했습니다. 만들기 및 Visual Studio에서 Web Forms 페이지를 편집 하는 방법을 이해 했으므로 다른 기능을 탐색 하는 것이 좋습니다. 예를 들어 다음을 수행 수 있습니다.

- ASP.NET Web Forms에 대 한 자세한 단계별 자습서 시리즈를 수행 하 여 자세한 [ASP.NET 4.5 Web Forms 및 Visual Studio 2013 시작](getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)합니다.
- Cascading 스타일 시트 (CSS)에 대해 자세히 알아보기 자세한 내용은 참조 [작업 CSS 개요](https://msdn.microsoft.com/library/bb398931.aspx)합니다.
