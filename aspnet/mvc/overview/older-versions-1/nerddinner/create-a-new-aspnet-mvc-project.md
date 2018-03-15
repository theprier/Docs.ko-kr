---
uid: mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
title: "새 ASP.NET MVC 프로젝트 만들기 | Microsoft Docs"
author: microsoft
description: "1 단계 기본 업그레이드 되었으며 수정 응용 프로그램 구조 제 자리에 배치 하는 방법을 보여 줍니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: 7e0e9928-8fdc-4b74-9882-55fac0976628
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
msc.type: authoredcontent
ms.openlocfilehash: 4d30a6803b1478014a2afb814ac317df27394446
ms.sourcegitcommit: 493a215355576cfa481773365de021bcf04bb9c7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
<a name="create-a-new-aspnet-mvc-project"></a>새 ASP.NET MVC 프로젝트 만들기
====================
by [Microsoft](https://github.com/microsoft)

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 이 무료의 1 단계 ["업그레이드 되었으며 수정" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 하는 워크 쓰루는 작고 빌드만 ASP.NET MVC 1을 사용 하 여 웹 응용 프로그램을 완료 하는 방법입니다.
> 
> 1 단계 기본 업그레이드 되었으며 수정 응용 프로그램 구조 제 자리에 배치 하는 방법을 보여 줍니다.
> 
> ASP.NET MVC 3을 사용 하는 경우 수행한 것이 좋습니다는 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.


## <a name="nerddinner-step-1-file-gtnew-project"></a>업그레이드 되었으며 수정 1 단계: 파일-&gt;새 프로젝트

먼저 업그레이드 되었으며 수정 응용 프로그램을 선택 하 여는 **파일-&gt;새 프로젝트** Visual Studio 2008 또는 무료 Visual Web Developer 2008 Express 내에서 메뉴 항목입니다.

이 "새 프로젝트" 대화 상자를 표시 합니다. 새 ASP.NET MVC 응용 프로그램을 만들려면 대화 상자의 왼쪽에 "웹" 노드를 선택 하 고 한 다음 오른쪽에서 "ASP.NET MVC 웹 응용 프로그램" 프로젝트 템플릿을 선택 합니다.

![](create-a-new-aspnet-mvc-project/_static/image1.png)

*중요: 다운로드 하 고 ASP.NET MVC-그렇지 않으면 새 프로젝트 대화 상자에는 나타나지 않습니다 설치 되어 있는지 확인 합니다. V2를 사용할 수는 [Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx) 아직 설치 하지 않은 경우 (ASP.NET MVC는 내에서 사용할 수는 "웹 플랫폼-&gt;프레임 워크 및 런타임" 섹션).*

"업그레이드 되었으며 수정" 만들고을 만드는 "확인" 단추를 클릭 한 다음을 새 프로젝트의 이름을 합니다.

"확인"을 클릭 하는 경우 Visual Studio도 새 응용 프로그램에 대 한 단위 테스트 프로젝트를 만들고 필요에 따라 요청 하는 추가 대화 상자를 표시 합니다. 이 단위 테스트 프로젝트를 사용 하면 기능 및 응용 프로그램의 동작을 확인 하는 자동화 된 테스트를 만들 수 있습니다 (다룰 것 문제가 어떻게이 자습서의 뒷부분에 나오는 할 일)입니다.

![](create-a-new-aspnet-mvc-project/_static/image2.png)

위의 대화 상자에 있는 "테스트 프레임 워크" 드롭다운에서 모든 사용 가능한 ASP.NET MVC 단위 테스트 프로젝트 템플릿이 함께 제공 된 컴퓨터에 설치 되어 채워집니다. MBUnit, NUnit, XUnit 버전을 다운로드할 수 있습니다. 기본 제공 Visual Studio 단위 테스트 프레임 워크 에서도 지원 됩니다.

*참고: Visual Studio 단위 테스트 프레임 워크는 Visual Studio 2008 Professional 및 이상 버전을 사용할 수만 있습니다. VS 2008 Standard Edition 또는 Visual Web Developer 2008 Express를 사용 하는 경우 다운로드 하 고이 대화 상자 표시 되도록 하려면에서 ASP.NET MVC에 대 한 NUnit, MBUnit 또는 XUnit 확장을 설치 해야 합니다. 모든 테스트 프레임 워크를 설치 하지 않은 경우에 대화 상자 표시 되지 않습니다.*

"Visual Studio 단위 테스트" 프레임 워크 옵션을 사용 하 여 알아보고 만듭니다, 테스트 프로젝트에 대 한 기본 "NerdDinner.Tests" 이름을 사용 하겠습니다. 클릭 하면 Visual Studio "확인" 단추는을 수행해 줍니다 솔루션을에-웹 응용 프로그램 및 단위 테스트 프로젝트를 두 개를 만듭니다.

![](create-a-new-aspnet-mvc-project/_static/image3.png)

### <a name="examining-the-nerddinner-directory-structure"></a>업그레이드 되었으며 수정 디렉터리 구조 검사

Visual Studio와 함께 새 ASP.NET MVC 응용 프로그램을 만들면 프로젝트에 자동으로 다양 한 파일 및 디렉터리 추가:

![](create-a-new-aspnet-mvc-project/_static/image4.png)

기본적으로 ASP.NET MVC 프로젝트는 6 개의 최상위 디렉터리:

| **Directory** | **용도** |
| --- | --- |
| **/Controllers** | URL 요청을 처리 하는 컨트롤러 클래스를 배치 하는 위치 |
| **/Models** | 나타내고 데이터를 조작 하는 클래스를 배치 하는 위치 |
| **/Views** | 렌더링 출력과 담당 하는 UI 템플릿 파일을 저장할 위치 |
| **/Scripts** | JavaScript 라이브러리 파일 및 스크립트 (.js)을 저장할 위치 |
| **/Content** | CSS 및 이미지 파일 및 기타 비-동적/비-JavaScript 콘텐츠를 배치 하는 위치 |
| **/App\_Data** | 데이터 파일을 저장 하는 경우 읽기/쓰기 하려고 합니다. |

ASP.NET MVC는이 구조를 필요 하지 않습니다. 사실, 대규모 응용 프로그램에서 작업 하는 개발자는 일반적으로 분할 응용 프로그램을 보다 잘 관리할 수 있도록 여러 프로젝트 (예: 데이터 모델 클래스 것으로 서 별도 클래스 라이브러리 프로젝트에서 웹 응용 프로그램에서). 그러나 기본 프로젝트 구조 म 새로 우리의 응용 프로그램 문제를 유지 하는 데 사용할 수 있는 좋은 기본 디렉터리 규칙을 제공지 않습니다.

/Controllers 디렉터리 확장 하는 경우는 Visual Studio-HomeController 및 AccountController – 두 컨트롤러 클래스 기본적으로 프로젝트에 추가 소요 됩니다.

![](create-a-new-aspnet-mvc-project/_static/image5.png)

/Views 디렉터리 확장을 다음과 같은 세 가지 하위 디렉터리-/Home, /Account /Shared – 뿐 아니라 여러 템플릿 폴더 내의 파일 기본적으로 프로젝트에 추가 된도 찾을 수 했습니다.

![](create-a-new-aspnet-mvc-project/_static/image6.png)

/Content 및 /Scripts 디렉터리를 확장 하는 경우 응용 프로그램 내에서 지원 되는 사이트의 모든 HTML 스타일을 지정 하는 데 사용 하는 Site.css 파일 뿐만 아니라 ASP.NET AJAX 및 jQuery 사용 하도록 설정할 수 있는 JavaScript 라이브러리 소요 됩니다.

![](create-a-new-aspnet-mvc-project/_static/image7.png)

NerdDinner.Tests 프로젝트 확장 다음과 같은 컨트롤러 클래스에 대 한 단위 테스트를 포함 하는 두 개의 클래스 찾을 수 있습니다.

![](create-a-new-aspnet-mvc-project/_static/image8.png)

이러한 기본 파일을 Visual Studio에서 추가를 입력 하는 기본 구조 작업 응용 프로그램-완료 되었으나 페이지, 계정 등록/로그인/로그 아웃 페이지 및 (모든 유선 접속 이며 작동 하 고 즉시) 처리 되지 않은 오류 페이지에 대 한 홈 페이지에 대 한.

### <a name="running-the-nerddinner-application"></a>업그레이드 되었으며 수정 응용 프로그램 실행

선택 하 여 프로젝트를 실행할 수 있습니다는 **디버그-&gt;디버깅 시작** 또는 **디버그-&gt;디버깅 하지 않고 시작** 메뉴 항목:

![](create-a-new-aspnet-mvc-project/_static/image9.png)

기본 제공 ASP.NET 웹 서버 Visual Studio와 함께 제공 되는 실행 되 고 응용 프로그램을 실행:

![](create-a-new-aspnet-mvc-project/_static/image10.png)

다음은 새 프로젝트 진행에 대 한 홈 페이지 (URL: "/")를 실행할 때:

![](create-a-new-aspnet-mvc-project/_static/image11.png)

"정보" 탭을 클릭 하면 표시 됩니다는 페이지에 대 한 (URL: "홈/곧 /"):

![](create-a-new-aspnet-mvc-project/_static/image12.png)

로그인 페이지에는 오른쪽 위에 "Log On" 링크를 클릭 하면 (URL: "/ 계정/로그온")

![](create-a-new-aspnet-mvc-project/_static/image13.png)

등록 링크를 클릭 하는 로그인 계정을 아직 경우 (URL: "/ 계정/레지스터") 새로 만들려면:

![](create-a-new-aspnet-mvc-project/_static/image14.png)

에 대 한 위의 홈을 구현 하는 코드 및 로그 아웃 /register 우리의 새 프로젝트를 만들 때 기본적으로 기능이 추가 되었습니다. 응용 프로그램의 시작 지점으로 때 사용 해야 합니다.

### <a name="testing-the-nerddinner-application"></a>업그레이드 되었으며 수정 응용 프로그램 테스트

Professional Edition 또는 더 높은 버전의 Visual Studio 2008을 사용 하는 기본 제공 단위 IDE 지원 Visual Studio 내에서 테스트 프로젝트 테스트 하 여 사용 하 여:

![](create-a-new-aspnet-mvc-project/_static/image15.png)

위의 옵션 중 하나를 선택 IDE 내에서 "테스트 결과" 창을 열고를 기본 제공 기능을 포괄 하는 새 프로젝트에 포함 된 27 단위 테스트에 통과/실패 상태와 함께 제공 됩니다.

![](create-a-new-aspnet-mvc-project/_static/image16.png)

이 자습서의 뒷부분에 대해서는 자동화 된 테스트에 대 한 자세히 알아보고 구현 하는 응용 프로그램 기능을 포괄 하는 추가 단위 테스트를 추가 하겠습니다.

### <a name="next-step"></a>다음 단계

이제 접수 했습니다 기본 응용 프로그램 구조 위치에 있습니다. 이제 보겠습니다 [응용 프로그램 데이터를 저장 하도록 데이터베이스를 만들](create-a-database.md)합니다.

>[!div class="step-by-step"]
[이전](introducing-the-nerddinner-tutorial.md)
[다음](create-a-database.md)
