---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create-the-project
title: 프로젝트 만들기 | Microsoft Docs
author: Erikre
description: 이 자습서 시리즈는 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 것에 대 한 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항 설명 하는 중...
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 2ce36f78-8ecb-4ab1-b748-6d0ab633ea3f
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create-the-project
msc.type: authoredcontent
ms.openlocfilehash: de0f8092342a8ba8979a31e9a97b603e44e6a85d
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41828751"
---
<a name="create-the-project"></a>프로젝트 만들기
====================
[Erik Reitan](https://github.com/Erikre)

[Wingtip Toys 샘플 프로젝트 (C#)를 다운로드](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자책 (PDF) 다운로드](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 이 자습서 시리즈는 ASP.NET 4.5와 Microsoft Visual Studio Express 2013 for Web 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 합니다. Visual Studio 2013 [C# 소스 코드를 사용 하 여 프로젝트](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 이 자습서 시리즈를 함께 사용할 수 있습니다.


이 자습서에서는, 검토를 만들고 ASP.NET의 기능에 익숙해질 수 있는 Visual Studio에서 기본 프로젝트를 실행 합니다. 또한 Visual Studio 환경을 검토 합니다.

## <a name="what-youll-learn"></a>학습할 내용:

- 새 Web Forms 프로젝트를 만드는 방법입니다.
- Web Forms 프로젝트의 파일 구조입니다.
- Visual Studio에서 프로젝트를 실행 하는 방법.
- 기본 Web forms 응용 프로그램의 다양 한 기능입니다.
- Visual Studio 환경을 사용 하는 방법에 대 한 몇 가지 기본 사항입니다.

## <a name="creating-the-project"></a>프로젝트 만들기

1. Visual Studio를 엽니다.
2. 선택 **새 프로젝트** 에서 합니다 **파일** Visual Studio의 메뉴. 

    ![프로젝트-새 프로젝트 메뉴 항목 만들기](create-the-project/_static/image1.png)
3. 선택 된 **템플릿을**  - &gt; **Visual C#**  - &gt; **웹** 왼쪽의 템플릿 그룹입니다.
4. 선택 된 **ASP.NET 웹 응용 프로그램** 가운데 열에서 템플릿.  
 이 자습서 시리즈는.NET Framework 4.5.2를 사용 합니다.
5. 프로젝트 이름을 *WingtipToys* 선택 합니다 **확인** 단추입니다. 

    ![프로젝트-새 프로젝트 대화 상자 만들기](create-the-project/_static/image2.png)

    > [!NOTE]
    > 이 자습서 시리즈에서 프로젝트의 이름은 **WingtipToys**합니다. 이 사용 하는 것이 좋습니다 *정확한* 이름을 프로젝트에 기능이 정상적으로 작동 자습서 시리즈 전체에서 코드를 제공 합니다.

6. 클릭 합니다 **인증 변경** 단추입니다. 선택 **개별 사용자 계정** 을 클릭 합니다 **확인** 단추입니다.

7. 선택 된 **Web Forms** 템플릿과 클릭 합니다 **확인** 단추.

    ![프로젝트-새 프로젝트 템플릿 만들기](create-the-project/_static/image3.png)

프로젝트를 만드는 데 잠시 시간이 걸립니다. 준비 되 면 엽니다는 **Default.aspx** 페이지입니다.

![프로젝트-새 프로젝트 템플릿 만들기](create-the-project/_static/image4.png)

전환할 수 있습니다 **디자인** 보기 및 **원본** 가운데 창의 맨 아래에서 옵션을 선택 하 여 보기. **디자인** WYSIWYG 뷰를 사용 하 여 사용자 정의 컨트롤 및 HTML 페이지, 콘텐츠 페이지, 마스터 페이지, ASP.NET 웹 페이지 보기에 표시 됩니다. **원본** 편집할 수 있는 웹 페이지에 대 한 HTML 태그를 표시 합니다.

> [!TIP] 
> 
> **ASP.NET 프레임 워크 이해**
> 
> ASP.NET Web Forms 익숙한 끌어서 놓기, 이벤트 기반 모델을 사용 하 여 빌드 동적 웹 사이트 수 있습니다. 디자인 화면과 수백 개의 컨트롤 및 구성 요소를 통해 데이터 액세스를 지원하는 정교하고 강력한 UI 중심 사이트를 신속하게 빌드할 수 있습니다. Wingtip 장난감 ASP.NET Web Forms를 기반으로 하지만 모든 ASP.NET에 적용할 수 있는 많은 개념이 자습서 시리즈에서에 대해 알아봅니다.
> 
> ASP.NET 4 주요 개발 프레임 워크를 제공합니다.
> 
> - [ASP.NET Web Forms](../../../index.md)  
>  Web Forms 프레임 워크 (WinForms) Microsoft Windows Forms 및 WPF/XAML/Silverlight와 같은 선언적 및 컨트롤 기반 프로그래밍을 선호 하는 개발자를 대상으로 합니다. 웹 개발을 위한 신속한 응용 프로그램 RAD (개발) 환경에 대 한 개발자를 사용 하 여 인기 있는 이므로 WYSIWYG 디자이너 기반 개발 모델을 제공 합니다. 웹 프로그래밍 하 고 (예: Visual Basic 및 Visual C#) 기존 Microsoft RAD 클라이언트 개발 도구에 익숙한 경우에 HTML 및 JavaScript 경험 하지 않고도 웹 응용 프로그램을 신속 하 게 빌드할 수 있습니다.
> - [ASP.NET MVC](../../../../mvc/index.md)  
>  ASP.NET MVC 패턴 및 테스트 기반 개발, 중요 한 부분의 분리, 제어 반전 (IoC) 이나 종속성 주입 (DI) 같은 원칙에 관심이 있는 개발자를 대상으로 합니다. 이 프레임 워크는 프레젠테이션 계층에서 웹 응용 프로그램의 비즈니스 논리 레이어를 구분 하는 권장 합니다.
> - [ASP.NET 웹 페이지 2](../../../../web-pages/index.md)  
>  ASP.NET 웹 페이지는 간단한 웹 개발 스토리를 PHP 행을 따라 하려는 개발자를 대상으로 합니다. 웹 페이지 모델에서 HTML 페이지 만들고 동적으로 태그 렌더링 되는 방식을 제어 하기 위해 서버 기반 코드 페이지를 추가 합니다. 웹 페이지 경량 프레임 워크가 되도록 설계 된 이며 쉬운 진입점 ASP.NET HTML 알지만 없을 광범위 한 프로그래밍 환경-예를 들어 사용자, 학생 또는 취미입니다. ASP.NET을 사용 하려면 PHP 나 비슷한 프레임 워크를 알고 있는 웹 개발자를 위한 좋은 방법 이기도 합니다.
> - [ASP.NET 단일 페이지 응용 프로그램](../../../../single-page-application/index.md)  
>  ASP.NET SPA(단일 페이지 응용 프로그램)는 HTML 5, CSS 3 및 JavaScript를 사용하여 중요한 클라이언트 쪽 상호 작용을 포함하는 응용 프로그램을 빌드할 수 있도록 도와줍니다. ASP.NET 및 Web Tools 2012.2 업데이트에는 knockout.js 및 ASP.NET Web API를 사용 하 여 단일 페이지 응용 프로그램을 구축 하기 위한 새 템플릿으로 제공 됩니다. 새 SPA 템플릿 외에도 새 커뮤니티에서 만든 SPA 템플릿을 다운로드할 사용할 수도 있습니다.
> 
> 4 개의 주요 개발 프레임 워크 외에도 ASP.NET은 또한 인식 하 고 익숙한 되도록 중요 하지만이 자습서 시리즈에서 해결 되지 않은 추가 기술을 제공 합니다.
> 
> - [ASP.NET Web API](../../../../web-api/index.md) -광범위 한 브라우저 및 모바일 장치를 비롯 하 여 클라이언트를 연결 하는 HTTP 서비스를 빌드하기 위한 프레임 워크입니다.
> - [ASP.NET SignalR](../../../../signalr/index.md) -개발 실시간 웹 기능을 더 쉽게 하는 라이브러리입니다.


### <a name="reviewing-the-project"></a>프로젝트 검토

Visual Studio에는 **솔루션 탐색기** 창에서는 프로젝트 파일을 관리할 수 있습니다. 응용 프로그램에 추가 된 폴더에 살펴보겠습니다 **솔루션 탐색기**합니다. 웹 응용 프로그램 템플릿은 기본 폴더 구조를 추가합니다.

![솔루션 탐색기 프로젝트-만들기](create-the-project/_static/image5.png)

Visual Studio 프로젝트에 대 한 일부 파일과 초기 폴더를 만듭니다. 이 자습서의 뒷부분에서 사용 됩니다는 첫 번째 파일 다음과 같습니다.

| **파일** | **용도** |
| --- | --- |
| *Default.aspx* | 일반적으로 첫 번째 페이지를 브라우저에서 응용 프로그램을 실행할 때는 표시 합니다. |
| *Site.Master* | 응용 프로그램에서 페이지에 대 한 일관 된 레이아웃 및 사용 하 여 표준 동작을 만들 수 있도록 하는 페이지입니다. |
| *Global.asax* | ASP.NET에서 또는 HTTP 모듈에서 발생 하는 응용 프로그램 수준 및 세션 수준 이벤트에 응답 하는 것에 대 한 코드를 포함 하는 선택적 파일입니다. |
| *Web.config* | 응용 프로그램에 대 한 구성 데이터입니다. |

### <a name="running-the-default-web-application"></a>기본 웹 응용 프로그램 실행

기본 웹 응용 프로그램 기본 제공 기능 및 지원에 따라 다양 한 환경을 제공 합니다. 기본 웹 폼 프로젝트를 변경 하지 않고 응용 프로그램을 로컬 웹 브라우저에서 실행할 준비가 되었습니다.

1. 키를 눌러 합니다 ***F5*** Visual Studio에서 하는 동안 키입니다.   
 응용 프로그램이 빌드되고 웹 브라우저에 표시 됩니다.  

    ![프로젝트 만들기-기본 페이지](create-the-project/_static/image6.png)
2. 실행 중인 응용 프로그램이 완료 된 검토를 만든 후에 브라우저 창을 닫습니다.

이 기본 웹 응용 프로그램에 세 가지 주요 페이지: *Default.aspx* (홈) *About.aspx*, 및 *Contact.aspx*합니다. 이러한 각 페이지의 위쪽 탐색 모음에서 도달할 수 있습니다. Account 폴더에 포함 된 두 개의 추가 페이지인, Register.aspx 페이지 및 Login.aspx 페이지 있습니다. 이러한 두 페이지를 만들고, 저장 및 사용자 자격 증명의 유효성을 검사 하려면 ASP.NET 멤버 자격 기능을 사용할 수 있습니다.

## <a name="aspnet-web-forms-background"></a>ASP.NET Web Forms 배경

ASP.NET Web Forms는 동적으로 서버에서 실행 되는 코드 브라우저 또는 클라이언트 장치에 웹 페이지 출력을 생성 하는 Microsoft ASP.NET 기술을 기반으로 하는 페이지입니다. 자동으로 ASP.NET Web Forms 페이지를 스타일, 레이아웃 등의 기능에 대 한 올바른 브라우저 규격 HTML을 렌더링합니다. Web Forms는.NET 공용 언어 런타임, Microsoft Visual Basic 및 Microsoft Visual C# 등을 지 원하는 모든 언어와 호환 됩니다. 또한 Web Forms 기반으로 합니다 [Microsoft.NET Framework](https://msdn.microsoft.com/vstudio/aa496123), 상속, 형식 안전성 및 관리 되는 환경 등의 이점을 제공 합니다.

ASP.NET Web Forms 페이지를 실행 하는 경우 페이지를 일련의 처리 단계를 수행 하는 수명 주기를 거칩니다. 이러한 단계 초기화 컨트롤 인스턴스화 및 복원 상태 유지 관리 이벤트 처리기 코드를 실행 및 렌더링을 포함 합니다. ASP.NET Web Forms의 기능을 더 익숙해지면 때 이해 해야 합니다 [ASP.NET 페이지 수명 주기의](https://msdn.microsoft.com/library/ms178472(v=vs.100).aspx) 결과 얻기 위해 적절 한 수명 주기 단계에서 코드를 작성할 수 있도록 합니다.

웹 서버 페이지에 대 한 요청을 받으면 페이지, 처리, 브라우저로 보내는 찾아 다음 모든 페이지 정보를 삭제 합니다. 사용자가 같은 페이지를 다시 요청 하는 경우 서버 페이지를 처음부터 다시 처리 하는 전체 시퀀스를 반복 합니다. 다른 말로 하면 서버 메모리가 없고 페이지 처리 페이지에는 상태 비저장입니다. ASP.NET 페이지 프레임 워크 페이지와 해당 컨트롤의 상태를 유지 관리 작업을 자동으로 처리 하 고 응용 프로그램별 정보의 상태를 유지 하는 명시적 방법을 제공 합니다.

> [!TIP] 
> 
> **Web Forms 응용 프로그램 템플릿에서 웹 응용 프로그램 기능**
> 
> ASP.NET Web Forms 응용 프로그램 템플릿을 다양 한 기본 제공 기능을 제공합니다. 뿐만 아니라 제공 된를 *Home.aspx* 페이지를 *About.aspx* 페이지를 *Contact.aspx* 사용자를 등록 하 고 저장 하는 멤버 자격 기능을 포함 하지만 페이지 자격 증명을 웹 사이트 로그온 할 수 있도록 합니다. 이 개요는 ASP.NET Web Forms 응용 프로그램 템플릿 및 사용 방법에 Wingtip Toys 응용 프로그램에 포함 된 기능 중 일부에 대 한 자세한 정보를 제공 합니다.
> 
> **멤버 자격**
> 
> [ASP.NET](https://msdn.microsoft.com/library/yh26yfzy.aspx) Identity 응용 프로그램에서 생성 된 데이터베이스에 사용자의 자격 증명을 저장 합니다. 사용자가 로그인 하는 경우 응용 프로그램 데이터베이스를 참조 하 여 자격 증명을 확인 합니다. 프로젝트의 *계정* 폴더 멤버 자격의 여러 부분을 구현 하는 파일 포함: 등록, 로그인, 암호를 변경 하 고 액세스 권한을 부여 합니다. 또한 ASP.NET Web Forms는 OAuth 및 OpenID를 지원합니다. 이러한 향상 된 인증 사용자가 Facebook, Twitter, Windows Live 및 Google로 이러한 계정에서 기존 자격 증명을 사용 하 여 사이트에 로그인을 허용 합니다.
> 
> ![솔루션 탐색기 (ASP.NET Id)-프로젝트 만들기](create-the-project/_static/image7.png)
> 
> 기본적으로 템플릿은 SQL Server Express LocalDB를 Visual Studio Express 2013 for Web 사용 하 여 제공 되는 개발 데이터베이스 서버 인스턴스의 기본 데이터베이스 이름을 사용 하 여 멤버 자격 데이터베이스를 만듭니다.
> 
> **SQL Server Express LocalDB**
> 
> [SQL Server Express LocalDB](https://technet.microsoft.com/library/hh510202.aspx) SQL Server 데이터베이스의 많은 프로그래밍 기능에는 SQL Server의 경량 버전입니다. SQL Server Express LocalDB 사용자 모드에서 실행 되며에 짧은 목록이 설치 필수 구성 요소는 신속 하 고 구성 없이 설치 합니다. Microsoft SQL Server, 데이터베이스 또는 TRANSACT-SQL 코드에서 이동할 수 있습니다 SQL Server Express LocalDB에서 SQL Server 및 SQL Azure 업그레이드 단계 없이 합니다. 따라서 SQL Server Express LocalDB 모든 버전의 SQL Server를 대상으로 하는 응용 프로그램에 대 한 개발자 환경으로 사용 수 있습니다. SQL Server Express LocalDB는 SQL Server Compact에서 사용할 수 없는 저장된 프로시저, 사용자 정의 함수 및 집계,.NET Framework 통합, 공간 형식 등과 같은 기능을 사용 합니다.
> 
> **마스터 페이지**
> 
> [ASP.NET 마스터 페이지](https://msdn.microsoft.com/library/wtxbf3hh.aspx) 응용 프로그램에서 일관성 있는 모양과의 모든 페이지에 대 한 동작을 정의 합니다. 마스터 페이지의 레이아웃은 사용자에 게 표시 되는 마지막 페이지를 생성 하기 위해 개별 콘텐츠 페이지의 콘텐츠와 병합 합니다. Wingtip Toys 응용 프로그램을 수정 합니다 *Site.master* 마스터 페이지는 Wingtip Toys 웹 사이트의 모든 페이지 공유할 같은 눈에 띄는 로고 및 탐색 모음입니다.
> 
> **HTML5**
> 
> ASP.NET Web Forms 응용 프로그램 템플릿은 지원 [HTML5](http://www.w3schools.com/html/html5_intro.asp)는 최신 버전의 HTML 태그 언어입니다. HTML5는 새 요소와 쉽게 웹 사이트를 만들 수 있는 기능을 지원 합니다.
> 
> **Modernizr**
> 
> 브라우저의 HTML5를 지원 하지 않는 경우 사용할 수 있습니다 [Modernizr](http://www.modernizr.com/)합니다. Modernizr는 브라우저는 HTML5 기능을 지원 하 고 그렇지 않은 경우 사용 하도록 설정 여부를 검색할 수 있는 오픈 소스 JavaScript 라이브러리. ASP.NET Web Forms 응용 프로그램 템플릿에 Modernizr NuGet 패키지로 설치 됩니다.
> 
> **부트스트랩**
> 
> Visual Studio 2013 프로젝트 템플릿을 사용 하 여 [부트스트랩](http://getbootstrap.com/), Twitter에서 만든 레이아웃 및 테마 프레임 워크입니다. 부트스트랩 CSS3를 사용 하 여 레이아웃 다른 브라우저 창 크기를 동적으로 조정할 수는 반응 형 디자인을 제공 합니다. 또한 쉽게 응용 프로그램의 모양 및 느낌이 변경 내용을 적용 하려면 부트스트랩 테마 기능을 사용할 수 있습니다. 기본적으로 Visual Studio 2013에서 ASP.NET 웹 응용 프로그램 템플릿을 NuGet 패키지로 부트스트랩을 포함합니다.
> 
> **NuGet 패키지**
> 
> ASP.NET Web Forms 응용 프로그램 템플릿 집합을 포함 [NuGet](http://www.nuget.org/) 패키지 있습니다. 이러한 패키지는 오픈 소스 라이브러리 및 도구 구성 요소화 된 기능을 제공합니다. 다양 한 패키지를 만들고 응용 프로그램을 테스트 하는 데 있습니다. Visual Studio 쉽게 추가, 제거 및 NuGet 패키지를 업데이트 합니다. 개발자가 만들 수 있으며 NuGet 패키지에도 추가 됩니다.
> 
> ![프로젝트-NuGet 대화 상자 만들기](create-the-project/_static/image8.png)
> 
> 패키지를 설치할 때 NuGet 솔루션 파일을 복사 하 고 어떤 변경이 필요한 참조를 추가 하 여 웹 응용 프로그램과 연결 된 구성 변경 등을 자동으로. 라이브러리를 제거 하려는 경우 NuGet 파일을 제거 하 고 없습니다 혼란 남아 있도록 프로젝트에 대 한 모든 변경 내용을 취소 합니다. NuGet에서 사용할 수는 **도구** Visual Studio의 메뉴.
> 
> **jQuery**
> 
> [jQuery](http://jquery.com/) HTML 문서 통과, 이벤트 처리, 애니메이션 효과 적용, 및 빠른 웹 개발을 위한 Ajax 상호 작용을 단순화 하는 빠르고 간결한 JavaScript 라이브러리입니다. JQuery JavaScript 라이브러리를 NuGet 패키지로 ASP.NET Web Forms 응용 프로그램 템플릿에 포함 됩니다.
> 
> **비간섭 유효성 검사**
> 
> 기본 제공 유효성 검사기 컨트롤 클라이언트 쪽 유효성 검사 논리에 대 한 비간섭 JavaScript를 사용 하도록 구성 된 합니다. 이 크게 줄어듭니다 페이지 태그에 인라인으로 렌더링 하는 JavaScript 및 전체 페이지 크기를 줄입니다. 비간섭 유효성 검사의 설정을 기반으로 ASP.NET Web Forms 응용 프로그램 템플릿의에 전체적으로 추가 됩니다는 &lt;appSettings&gt; 의 요소를 *Web.config* 응용 프로그램의 루트에 있는 파일입니다.
> 
> **Entity Framework Code First**
> 
> Wingtip Toys 응용 프로그램에서 ASP.NET Web Forms 응용 프로그램 템플릿에서 기능 외에도 다음을 사용 합니다. [Entity Framework Code First](https://weblogs.asp.net/scottgu/archive/2010/12/08/announcing-entity-framework-code-first-ctp5-release.aspx), 데이터로 작업할 때 코드 중심의 개발을 수 있는 NuGet 라이브러리는 합니다. 간단히 말해서, 작성 하는 코드에 따라 응용 프로그램의 데이터베이스 부분을 만듭니다. Entity Framework를 사용 하 여 검색 하 고 강력한 형식의 개체로 데이터를 조작 합니다. 데이터에 액세스 하는 방법의 세부 정보를 사용 하지 않고 응용 프로그램에 비즈니스 논리에 집중이 있습니다.
> 
> 설치 된 라이브러리 및 ASP.NET Web Forms 템플릿을 사용 하 여 포함 된 패키지에 대 한 자세한 내용은 설치 된 NuGet 패키지 목록을 참조 하세요. 이렇게 하려면 Visual Studio에서 만드는 새 Web Forms 프로젝트를 선택 **도구가**  - &gt; **라이브러리 패키지 관리자**  - &gt; **관리 솔루션용 NuGet 패키지**를 선택 하 고 **패키지를 설치** 에 **NuGet 패키지 관리** 대화 상자.


### <a name="touring-visual-studio"></a>Visual Studio touring

Visual Studio에서 기본 windows 포함 된 **솔루션 탐색기**의 **서버 탐색기** (**데이터베이스 탐색기** Express에서), **속성 창**, **도구 상자**서 **도구 모음**, 및 **문서 창**합니다.

![프로젝트-NuGet 대화 상자 만들기](create-the-project/_static/image9.png)

Visual Studio에 대 한 자세한 내용은 참조 하세요. [Visual Web Developer에 대 한 시각적 가이드](https://msdn.microsoft.com/library/ee410104.aspx)합니다.

## <a name="summary"></a>요약

이 자습서에서는, 검토를 만들고 기본 Web Forms 응용 프로그램을 실행 합니다. 기본 Web forms 응용 프로그램의 다양 한 기능을 검토 하 고 Visual Studio 환경을 사용 하는 방법에 대 한 몇 가지 기본 사항을 학습 합니다. 다음 자습서에서는 데이터 액세스 계층을 만듭니다.

## <a name="additional-resources"></a>추가 리소스

[적절 한 프로그래밍 모델 선택](../../../videos/how-do-i/choosing-the-right-programming-model.md)   
[웹 응용 프로그램 프로젝트와 웹 사이트 프로젝트 비교](https://msdn.microsoft.com/library/dd547590.aspx)   
[ASP.NET Web Forms 페이지 개요](https://msdn.microsoft.com/library/428509ah.aspx)

> [!div class="step-by-step"]
> [이전](introduction-and-overview.md)
> [다음](create_the_data_access_layer.md)
