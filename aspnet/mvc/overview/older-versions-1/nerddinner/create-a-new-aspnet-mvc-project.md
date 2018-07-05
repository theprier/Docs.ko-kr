---
uid: mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
title: 새 ASP.NET MVC 프로젝트 만들기 | Microsoft Docs
author: microsoft
description: 1 단계를에서 기본 NerdDinner 응용 프로그램 구조를 배치 하는 방법을 보여 줍니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: 7e0e9928-8fdc-4b74-9882-55fac0976628
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
msc.type: authoredcontent
ms.openlocfilehash: 9f5e0b3f82d113fc72ab4002ec8d06ad8444dceb
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37374278"
---
<a name="create-a-new-aspnet-mvc-project"></a>새 ASP.NET MVC 프로젝트 만들기
====================
[Microsoft](https://github.com/microsoft)

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 이 무료의 1 단계 ["NerdDinner" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 는 안내를 통한 작은 빌드 하지만 ASP.NET MVC 1을 사용 하 여 웹 응용 프로그램을 완료 하는 방법입니다.
> 
> 1 단계를에서 기본 NerdDinner 응용 프로그램 구조를 배치 하는 방법을 보여 줍니다.
> 
> ASP.NET MVC 3을 사용 하는 경우 수행 하는 것이 좋습니다 합니다 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 하거나 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.


## <a name="nerddinner-step-1-file-gtnew-project"></a>NerdDinner 1 단계: 파일-&gt;새 프로젝트

NerdDinner 응용 프로그램을 선택 하 여 먼저 합니다 **파일-&gt;새 프로젝트** Visual Studio 2008 또는 무료 Visual Web Developer 2008 Express에서 메뉴 항목입니다.

"새 프로젝트" 대화 상자가 표시 됩니다. 새 ASP.NET MVC 응용 프로그램을 만들려면 대화 상자의 왼쪽에서 "웹" 노드를 선택 하 고 선택한 다음 오른쪽의 "ASP.NET MVC 웹 응용 프로그램" 프로젝트 템플릿의 됩니다.

![](create-a-new-aspnet-mvc-project/_static/image1.png)

*중요: 다운로드 하 고 ASP.NET MVC-그렇지 않은 경우 새 프로젝트 대화 상자에 나타나지 설치 되어 있는지 확인 합니다. V2의 사용할 수는 [Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx) 아직 설치 하지 않은 경우 (ASP.NET MVC는 내에서 사용할 수는 "웹 플랫폼-&gt;프레임 워크 및 런타임" 섹션).*

에서는 하겠습니다 "NerdDinner"를 만들고 만들 "확인" 단추를 클릭 한 다음 새 프로젝트의 이름을 지정 합니다.

"확인"를 클릭 하는 경우 Visual Studio는 필요에 따라도 새 응용 프로그램에 대 한 단위 테스트 프로젝트를 만들 요청 추가 대화 상자를 표시 합니다. 이 단위 테스트 프로젝트 기능 및 응용 프로그램의 동작을 확인 하는 자동화 된 테스트를 만들 수 있습니다 (다루게 무언가 어떻게 할 일이이 자습서의 뒷부분에서).

![](create-a-new-aspnet-mvc-project/_static/image2.png)

위 대화 상자에서 "테스트 프레임 워크" 드롭다운에서 모든 사용 가능한 ASP.NET MVC 단위 테스트 프로젝트 템플릿 컴퓨터에 설치를 사용 하 여 채워집니다. XUnit, NUnit 및 MBUnit에 버전을 다운로드할 수 있습니다. 기본 제공 Visual Studio 단위 테스트 프레임 워크 에서도 지원 됩니다.

*참고: Visual Studio 단위 테스트 프레임 워크는만 Visual Studio 2008 Professional 및 이상 버전을 사용 하 여 사용할 수 있습니다. VS 2008 Standard Edition 또는 Visual Web Developer 2008 Express를 사용 하는 경우 다운로드 하 고이 대화 상자 표시를 위해에서 ASP.NET MVC에 대 한 NUnit 이나 MBUnit XUnit 확장을 설치 해야 합니다. 모든 테스트 프레임 워크 설치 되지 않은 경우에 대화 상자가 표시 되지 않습니다.*

을 만들어 테스트 프로젝트에 대 한 기본 "NerdDinner.Tests" 이름을 사용 하 고 "Visual Studio 단위 테스트" 프레임 워크 옵션을 사용 하겠습니다. 클릭 하면 "확인" 단추 Visual Studio 솔루션이 만들어집니다 한 것은 단위 테스트에 대 한 웹 응용 프로그램에 대 한 개와 두 프로젝트를 사용 하 여:

![](create-a-new-aspnet-mvc-project/_static/image3.png)

### <a name="examining-the-nerddinner-directory-structure"></a>NerdDinner 디렉터리 구조를 검사합니다.

Visual Studio를 사용 하 여 새 ASP.NET MVC 응용 프로그램을 만들 때 프로젝트에 파일 및 디렉터리의 숫자로 자동으로 추가 합니다.

![](create-a-new-aspnet-mvc-project/_static/image4.png)

기본적으로 ASP.NET MVC 프로젝트에 6 개의 최상위 디렉터리

| **디렉터리** | **용도** |
| --- | --- |
| **/Controllers** | URL 요청을 처리 하는 컨트롤러 클래스를 배치 하는 위치 |
| **/Models** | 나타내는 데이터를 조작 하는 클래스를 배치 하는 위치 |
| **/ 뷰** | 렌더링 출력과 관련 된 UI 템플릿 파일을 배치 하는 위치 |
| **/Scripts** | JavaScript 라이브러리 파일 및 스크립트 (.js)을 배치 하는 위치 |
| **/Content** | CSS 및 이미지 파일을 다른 비-동적/비-JavaScript 콘텐츠를 배치 하는 위치 |
| **/ 앱\_데이터** | 데이터 파일을 저장 하는 경우 읽기/쓰기 하려고 합니다. |

ASP.NET MVC는이 구조를 필요 하지 않습니다. 사실, 대규모 응용 프로그램에서 작업 하는 개발자는 일반적으로 분할 응용 프로그램을 보다 잘 관리할 수 있도록 여러 프로젝트에서 (예: 데이터 모델 클래스도 별도 클래스 라이브러리 프로젝트를 웹 응용 프로그램에서). 그러나 기본 프로젝트 구조는 응용 프로그램 문제를 정리 되도록 사용할 수 있는 유용한 기본 디렉터리 규칙을 제공지 않습니다.

/Controllers 디렉터리 확장에서는 알는 Visual Studio – HomeController과 AccountController – 두 컨트롤러 클래스 기본적으로 프로젝트에 추가 합니다.

![](create-a-new-aspnet-mvc-project/_static/image5.png)

/Views 디렉터리를 확장 하는 경우 세 개의 하위 디렉터리가 – /Home, /Account /Shared – 뿐만 아니라 여러 템플릿 파일 내에 기본적으로 프로젝트에 추가 된도 알게 됩니다.

![](create-a-new-aspnet-mvc-project/_static/image6.png)

/Content 및 /Scripts 디렉터리를 확장 하는 경우 응용 프로그램 내에서 지 원하는 사이트의 모든 HTML 스타일을 지정 하는 데 사용 되는 Site.css 파일 뿐만 아니라 ASP.NET AJAX 및 jQuery 사용 하도록 설정할 수 있는 JavaScript 라이브러리를 찾을 수 것:

![](create-a-new-aspnet-mvc-project/_static/image7.png)

NerdDinner.Tests 프로젝트를 확장 하는 경우 컨트롤러 클래스에 대 한 단위 테스트를 포함 하는 두 개의 클래스를 찾을 수 했습니다.

![](create-a-new-aspnet-mvc-project/_static/image8.png)

Visual Studio에서 추가 된 이러한 기본 파일 우리 기본 구조를 사용 하 여 작업 응용 프로그램을 제공-페이지, 계정 등록/로그인/로그 아웃 페이지와 처리 되지 않은 오류 페이지 (모든: 했으니 및 즉시 작업)에 대 한 홈 페이지를 사용 하 여 완료 합니다.

### <a name="running-the-nerddinner-application"></a>NerdDinner 응용 프로그램 실행

프로젝트 중 하나를 선택 하 여 실행할 수 있습니다 합니다 **디버그-&gt;디버깅 시작** 하거나 **디버그-&gt;디버깅 하지 않고 시작** 메뉴 항목:

![](create-a-new-aspnet-mvc-project/_static/image9.png)

이 기본 제공 ASP.NET 웹 서버에서 시작-Visual Studio와 함께 제공 되는 되며 응용 프로그램을 실행 합니다.

![](create-a-new-aspnet-mvc-project/_static/image10.png)

다음은 새 프로젝트의 홈 페이지 (URL: "/") 실행 시:

![](create-a-new-aspnet-mvc-project/_static/image11.png)

"About" 탭을 클릭 하면 표시 됩니다는 페이지에 대 한 (URL: "/ Home/에 대 한"):

![](create-a-new-aspnet-mvc-project/_static/image12.png)

로그인 페이지에는 오른쪽 상단에서 "Log On" 링크 (URL: "/ 계정/로그온")

![](create-a-new-aspnet-mvc-project/_static/image13.png)

에서는 등록 링크를 클릭할 수 있습니다 로그인 계정이 없는 경우 (URL: "/ 계정/등록") 새로 만들려면:

![](create-a-new-aspnet-mvc-project/_static/image14.png)

에 대 한 위의 가정용을 구현 하는 코드 및 로그 아웃 등록 / 기능, 새 프로젝트를 만들 때 기본적으로 추가 되었습니다. 이 응용 프로그램의 시작 점으로 사용 하겠습니다.

### <a name="testing-the-nerddinner-application"></a>NerdDinner 응용 프로그램 테스트

Professional Edition 또는 더 높은 버전의 Visual Studio 2008을 사용 하는 것 테스트 IDE 지원을 Visual Studio 내에서 기본 제공 단위 테스트 프로젝트를 사용할 수 있습니다.

![](create-a-new-aspnet-mvc-project/_static/image15.png)

위의 옵션 중 하나를 선택 하면 IDE 내에서 "테스트 결과" 창을 엽니다 되며 기본 제공 기능을 포함 하는 새 프로젝트에 포함 된 27 단위 테스트에 통과/실패 상태를 사용 하 여 제공:

![](create-a-new-aspnet-mvc-project/_static/image16.png)

이 자습서의 뒷부분에 나오는에서는 자동화 된 테스트를 자세히 설명 하 고 구현 하는 응용 프로그램 기능을 포함 하는 추가 단위 테스트를 추가 합니다.

### <a name="next-step"></a>다음 단계

현재 위치에서 이제 기본 응용 프로그램 구조에 답변이 있습니다. 이제 보겠습니다 [응용 프로그램 데이터를 저장 하도록 데이터베이스를 만드는](create-a-database.md)합니다.

> [!div class="step-by-step"]
> [이전](introducing-the-nerddinner-tutorial.md)
> [다음](create-a-database.md)
