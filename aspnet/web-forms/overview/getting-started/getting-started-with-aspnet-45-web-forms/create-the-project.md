---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create-the-project
title: "프로젝트 만들기 | Microsoft Docs"
author: Erikre
description: "이 자습서 시리즈 것에 대 한 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 구축 하는 기초 알려 드리겠습니다 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/08/2014
ms.topic: article
ms.assetid: 2ce36f78-8ecb-4ab1-b748-6d0ab633ea3f
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create-the-project
msc.type: authoredcontent
ms.openlocfilehash: 094733dcbe31486385dda2f8b44ba77a17486c82
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="create-the-project"></a>프로젝트 만들기
====================
으로 [Erik Reitan](https://github.com/Erikre)

[Wingtip Toys 샘플 프로젝트 (C#)를 다운로드](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자책 (PDF)를 다운로드 합니다.](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 이 자습서 시리즈 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 웹에 대 한 ASP.NET Web Forms 응용 프로그램을 구축 하는 기초 알려 드리겠습니다. Visual Studio 2013 [C# 소스 코드를 사용 하 여 프로젝트](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 이 자습서 시리즈를 함께 사용할 수 있습니다.


이 자습서에서는, 검토, 만들고 ASP.NET의 기능에 익숙해질 수 있는 Visual Studio에서 기본 프로젝트를 실행 합니다. 또한 Visual Studio 환경을 검토 합니다.

## <a name="what-youll-learn"></a>학습 내용:

- 새 Web Forms 프로젝트를 만드는 방법.
- Web Forms 프로젝트의 파일 구조입니다.
- Visual Studio에서 프로젝트를 실행 하는 방법.
- 기본 Web forms 응용 프로그램의 다양 한 기능입니다.
- Visual Studio 환경을 사용 하는 방법에 대 한 몇 가지 기본 사항입니다.

## <a name="creating-the-project"></a>프로젝트 만들기

1. Visual Studio를 엽니다.
2. 선택 **새 프로젝트** 에서 **파일** Visual Studio에서 메뉴. 

    ![프로젝트-새 프로젝트 메뉴 항목 만들기](create-the-project/_static/image1.png)
3. 선택 된 **템플릿**  - &gt; **Visual C#**  - &gt; **웹** 왼쪽의 템플릿 그룹.
4. 선택 된 **ASP.NET 웹 응용 프로그램** 가운데 열에서 서식 파일입니다.  
 이 자습서 시리즈는.NET Framework 4.5.2를 사용 합니다.
5. 프로젝트 이름을 *WingtipToys* 선택 하 고는 **확인** 단추입니다. 

    ![새 프로젝트 대화 상자-프로젝트 만들기](create-the-project/_static/image2.png)

    > [!NOTE]
    > 이 자습서 시리즈의 프로젝트 이름이 **WingtipToys**합니다. 이 사용 하는 것이 좋습니다. *정확한* 예상 대로 작동 자습서 시리즈에서 제공 되는 코드를 프로젝트 이름입니다.
6. 다음으로, 선택는 **Web Forms** 템플릿을 선택 하 고는 **프로젝트 만들기** 단추입니다.  

    ![프로젝트-새 프로젝트 템플릿 만들기](create-the-project/_static/image3.png)

프로젝트를 만드는 데 약간 시간이 걸립니다. 준비 되 면 열고는 **Default.aspx** 페이지.

![프로젝트-새 프로젝트 템플릿 만들기](create-the-project/_static/image4.png)

간을 전환할 수 있습니다 **디자인** 보기 및 **소스** 아래쪽 가운데 창에 옵션을 선택 하 여 보기. **디자인** HTML 페이지, 콘텐츠 페이지, 마스터 페이지, ASP.NET 웹 페이지 보기를 표시 하 고 사용자 WYSIWYG 보기를 사용 하 여 제어 합니다. **소스** 편집할 수 있는 웹 페이지에 대 한 HTML 태그를 표시 합니다.

> [!TIP] 
> 
> **ASP.NET 프레임 워크 이해**
> 
> ASP.NET Web Forms 친숙 한 끌어서 놓기, 이벤트 기반 모델을 사용 하 여 빌드 동적 웹 사이트 수 있습니다. 디자인 화면과 수백 개의 컨트롤 및 구성 요소를 통해 빠르게 정교 하 고 강력한 UI 기반의 사이트 데이터 액세스를 작성할 수 있습니다. Wingtip 장난감 저장소가 ASP.NET Web Forms 기반 하지만이 자습서 시리즈에서 배우는 개념 중 대부분은 모든 ASP.NET에 적용할 수 있습니다.
> 
> ASP.NET 4 개의 기본 개발 프레임 워크를 제공합니다.
> 
> - [ASP.NET Web Forms](../../../index.md)  
>  Web Forms 프레임 워크 Microsoft Windows Forms (WinForms) 및 WPF/XAML/Silverlight와 같은 선언적 코딩 스타일과 제어 기반 프로그래밍을 선호 하는 개발자를 대상으로 합니다. 웹 개발에 대 한 신속한 응용 프로그램 (RAD) 개발 환경을 원하는 개발자와 많이 사용 되기 때문에 WYSIWYG 디자이너 기반 개발 모델을 제공 합니다. 웹 프로그래밍을 처음 접하는 기존 Microsoft RAD 클라이언트 개발 도구 (예: Visual Basic 및 Visual C#)에 익숙한 경우에 HTML 및 JavaScript 경험 필요 없이 웹 응용 프로그램을 신속 하 게 작성할 수 있습니다.
> - [ASP.NET MVC](../../../../mvc/index.md)  
>  ASP.NET MVC 패턴 및 테스트 기반 개발, 문제의 분리, 반전 IoC (), 제어 및 종속성 주입 (DI)와 같은 원칙에 관심이 개발자를 대상으로 합니다. 이 프레임 워크는 프레젠테이션 계층에서 웹 응용 프로그램의 비즈니스 논리 계층을 구분 하는 권장 합니다.
> - [ASP.NET 웹 페이지 2](../../../../web-pages/index.md)  
>  ASP.NET 웹 페이지에 따라 PHP는 간단한 웹 개발 스토리를 알아보려는 개발자를 대상으로 합니다. 웹 페이지 모델에서 HTML 페이지 만들고 동적으로 해당 태그를 렌더링 하는 방식을 제어 하기 위해 서버 기반 코드 페이지에 추가 합니다. 웹 페이지 수는 경량 프레임 워크 하도록 설계 된 아니며 쉬운 진입점 asp.net 사용자에 게 HTML 알지만 없을 만큼 광범위 한 프로그래밍 환경을-예를 들어, 학생 또는 취미 합니다. ASP.NET을 사용 하려면 PHP 또는 유사한 프레임 워크를 알고 있는 웹 개발자를 위한 좋은 방법 이기도 합니다.
> - [ASP.NET 단일 페이지 응용 프로그램](../../../../single-page-application/index.md)  
>  ASP.NET 단일 페이지 응용 프로그램 (SPA)를 사용 하면 HTML 5, CSS 3 및 JavaScript를 사용 하 여 중요 한 클라이언트 쪽 상호 작용을 포함 하는 응용 프로그램을 빌드할 수 있습니다. ASP.NET 및 Web Tools 2012.2 업데이트 knockout.js 및 ASP.NET Web API를 사용 하 여 단일 페이지 응용 프로그램을 구축 하기 위한 새 템플릿이 함께 제공 됩니다. 새 SPA 서식 파일 뿐 아니라 새 커뮤니티에서 만든 SPA 템플릿은 다운로드할 수 있습니다.
> 
> 4 개의 주 개발 프레임 워크 외에도 ASP.NET를 인식 하 고 친숙 한 되도록 중요 하지만이 자습서 시리즈에 포함 되지 않는 있는 추가 기술도 제공 합니다.
> 
> - [ASP.NET Web API](../../../../web-api/index.md) -다양 한 브라우저 및 모바일 장치를 포함 한 클라이언트를 연결할 HTTP 서비스를 빌드하기 위한 프레임 워크입니다.
> - [ASP.NET SignalR](../../../../signalr/index.md) -개발 실시간 웹 기능을 더 쉽게 하는 라이브러리입니다.


### <a name="reviewing-the-project"></a>프로젝트 검토

Visual Studio에서의 **솔루션 탐색기** 창에서 프로젝트 파일을 관리할 수 있습니다. 응용 프로그램에 추가 된 폴더에 살펴보겠습니다 **솔루션 탐색기**합니다. 웹 응용 프로그램 템플릿은 기본 폴더 구조를 추가합니다.

![솔루션 탐색기-프로젝트 만들기](create-the-project/_static/image5.png)

Visual Studio 프로젝트에 대 한 일부 파일과 초기 폴더를 만듭니다. 이 자습서의 뒷부분에서 사용 됩니다 하는 첫 번째 파일에는 다음과 같습니다.

| **파일** | **용도** |
| --- | --- |
| *Default.aspx* | 일반적으로 첫 번째 페이지는 응용 프로그램이 브라우저에서 실행 될 때 표시 됩니다. |
| *Site.Master* | 응용 프로그램에서 페이지에 대 한 일관 된 레이아웃 및 사용 하 여 표준 동작을 만들 수 있도록 하는 페이지입니다. |
| *Global.asax* | ASP.NET 또는 HTTP 모듈에서 발생 시킨 응용 프로그램 수준 및 세션 수준 이벤트에 응답 하기 위한 코드를 포함 하는 선택적 파일입니다. |
| *Web.config* | 응용 프로그램에 대 한 구성 데이터입니다. |

### <a name="running-the-default-web-application"></a>기본 웹 응용 프로그램 실행

기본 웹 응용 프로그램에 기본 제공 기능 및 지원에 따라 풍부한 환경을 제공 합니다. 기본 웹 forms 프로젝트를 변경 하지 않고도 응용 프로그램은 로컬 웹 브라우저에서 실행할 준비가 됩니다.

1. 키를 눌러는 ***F5*** Visual Studio에서 하는 동안 키입니다.   
 응용 프로그램 작성 되 고 웹 브라우저에 표시 됩니다.  

    ![프로젝트 만들기-기본 페이지](create-the-project/_static/image6.png)
2. 실행 중인 응용 프로그램 완료 검토 있으면 브라우저 창을 닫습니다.

이 기본 웹 응용 프로그램의 세 가지 주요 페이지는: *Default.aspx* (홈) *About.aspx*, 및 *Contact.aspx*합니다. 이러한 각 페이지의 위쪽 탐색 모음에서 연결할 수 있습니다. 계정 폴더에 포함 된 두 개의 추가 페이지인, Register.aspx 페이지 한 Login.aspx 페이지 있습니다. 이러한 두 페이지를 만들고, 저장 및 사용자 자격 증명의 유효성을 검사 하려면 ASP.NET의 멤버 자격 기능을 사용할 수 있도록 합니다.

## <a name="aspnet-web-forms-background"></a>ASP.NET Web Forms 배경

ASP.NET Web Forms는 동적으로 서버에서 실행 되는 코드를 있는 브라우저 또는 클라이언트 장치에 웹 페이지 출력을 생성 하는 Microsoft ASP.NET 기술을 기반으로 하는 페이지입니다. ASP.NET Web Forms 페이지에는 자동으로 스타일, 레이아웃 등의 기능에 대 한 올바른 브라우저 호환 HTML을 렌더링합니다. Web Forms.NET 공용 언어 런타임, 예: Microsoft Visual Basic 및 Microsoft Visual C#에서 지 원하는 모든 언어와 호환 됩니다. Web Forms 기반 또한는 [Microsoft.NET Framework](https://msdn.microsoft.com/vstudio/aa496123), 관리 되는 환경, 형식 안전성 및 상속 같은 같은 이점을 제공 합니다.

ASP.NET Web Forms 페이지를 실행 하는 경우 페이지가 일련의 처리 단계를 수행 하는 수명 주기를 통과 합니다. 이러한 단계에는 컨트롤 인스턴스화, 복원 및 상태를 유지 관리 이벤트 처리기 코드 실행, 렌더링 초기화 포함 됩니다. ASP.NET Web Forms의, 더 익숙해지면 것이 중요 이해 하는 [ASP.NET 페이지 수명 주기](https://msdn.microsoft.com/library/ms178472(v=vs.100).aspx) 결과 얻기에 대 한 적절 한 수명 주기 단계에서 코드를 작성할 수 있도록 합니다.

웹 서버 페이지에 대 한 요청을 받으면 페이지, 처리, 브라우저에 보내는 찾아 다음 모든 페이지 정보를 삭제 합니다. 사용자가 동일한 페이지를 다시 요청 하는 경우 서버 페이지를 처음부터 다시 처리 하는 전체 시퀀스를 반복 합니다. 즉, 서버에 처리 된 페이지는 페이지의 메모리가 없습니다. 상태 비저장 합니다. ASP.NET 페이지 프레임 워크의 페이지와 해당 컨트롤의 상태를 유지 관리 작업을 자동으로 처리 하 고 응용 프로그램 정보의 상태를 유지 하는 명시적 방법을 제공 합니다.

> [!TIP] 
> 
> **Web Forms 응용 프로그램 템플릿에서 웹 응용 프로그램 기능**
> 
> ASP.NET Web Forms 응용 프로그램 템플릿은 다양 한 기본 제공 기능을 제공합니다. 뿐만 아니라 제공 하는 *Home.aspx* 페이지는 *About.aspx* 페이지는 *Contact.aspx* 페이지 하지만 사용자가 등록 하 고 저장 하는 멤버 자격 기능을 포함 자격 증명 웹 사이트에 로그인 할 수 있도록 합니다. 이 개요는 ASP.NET Web Forms 응용 프로그램 템플릿과 Wingtip Toys 응용 프로그램에서 사용 하는 방법에 포함 된 기능 중 일부에 대 한 자세한 정보를 제공 합니다.
> 
> **멤버 자격**
> 
> [ASP.NET](https://msdn.microsoft.com/library/yh26yfzy.aspx) Identity 응용 프로그램에서 만든 데이터베이스에 사용자의 자격 증명을 저장 합니다. 사용자가 로그인 하는 경우 응용 프로그램 데이터베이스를 참조 하 여 자격 증명을 확인 합니다. 프로젝트의 *계정* 멤버 자격의 다양 한 부분을 구현 하는 파일을 포함 하는 폴더: 등록 로그인 암호를 변경 하 고 액세스 권한을 부여 합니다. 또한, ASP.NET Web Forms OAuth 및 OpenID 지원 됩니다. 이러한 인증 된 사용자가 Facebook, Twitter, Windows Live, Google로 이러한 계정에서 기존 자격 증명을 사용 하 여 사이트에 로그인을 허용 합니다.
> 
> ![솔루션 탐색기 (ASP.NET Identity)-프로젝트 만들기](create-the-project/_static/image7.png)
> 
> 기본적으로 템플릿은 SQL Server Express LocalDB에서 Visual Studio Express 2013 for Web와 함께 제공 되는 개발 데이터베이스 서버 인스턴스의 기본 데이터베이스 이름을 사용 하 여 멤버 자격 데이터베이스를 만듭니다.
> 
> **SQL Server Express LocalDB**
> 
> [SQL Server Express LocalDB](https://technet.microsoft.com/library/hh510202.aspx) 는 SQL Server 데이터베이스의 많은 프로그래밍 기능에 SQL Server의 경량 버전입니다. SQL Server Express LocalDB 사용자 모드에서 실행 있으며 짧은 목록이 설치 필수 구성 요소에 구성이 필요 없는 빠른 설치가입니다. Microsoft SQL Server, 데이터베이스 또는 Transact SQL 코드 수에서 이동 될 SQL Server Express LocalDB에서 SQL Server 및 SQL Azure 업그레이드 단계 없이 합니다. 따라서 SQL Server Express LocalDB 용도 개발자 환경으로 응용 프로그램의 모든 버전의 SQL Server를 대상으로 지정 합니다. SQL Server Express LocalDB는 SQL Server Compact에서 사용할 수 없는 저장된 프로시저, 사용자 정의 함수 및 집계,.NET Framework 통합, 공간 형식 등과 같은 기능을 사용할 수 있습니다.
> 
> **마스터 페이지**
> 
> [ASP.NET 마스터 페이지](https://msdn.microsoft.com/library/wtxbf3hh.aspx) 응용 프로그램에서 일관성 있는 모양과의 모든 페이지에 대 한 동작을 정의 합니다. 사용자에 게 표시 하는 마지막 페이지를 생성 하기 위해 개별 콘텐츠 페이지의 내용으로 병합 하는 마스터 페이지의 레이아웃입니다. Wingtip Toys 응용 프로그램에서 수정 된 *Site.master* 는 Wingtip Toys 웹 사이트의 모든 페이지 공유할 같은 고유한 로고 및 탐색 모음의 마스터 페이지입니다.
> 
> **HTML5**
> 
> ASP.NET Web Forms 응용 프로그램 템플릿에서 [HTML5](http://www.w3schools.com/html/html5_intro.asp), HTML 태그 언어의 최신 버전입니다. HTML5 새 요소와 웹 사이트를 만드는 쉽게 해 주는 기능을 지원 합니다.
> 
> **Modernizr**
> 
> HTML5 지원 하지 않는 브라우저를 사용할 수 있습니다 [Modernizr](http://www.modernizr.com/)합니다. Modernizr은 브라우저에서는 HTML5 기능을 지원 하 고 그렇지 않은 경우 사용할 수 있도록 있는지 여부를 검색할 수 있는 오픈 소스 JavaScript 라이브러리. ASP.NET Web Forms 응용 프로그램 템플릿에 Modernizr NuGet 패키지 설치 됩니다.
> 
> **Bootstrap**
> 
> Visual Studio 2013 프로젝트 템플릿을 사용 하 여 [부트스트랩](http://getbootstrap.com/), Twitter에서 만든 프레임 워크 레이아웃 및 테마 설정입니다. 다른 브라우저 창 크기에 맞게 레이아웃 동적으로 적용할 수는 반응 형 디자인을 제공 하기 위해 CSS3를 사용 하는 부트스트랩 합니다. 또한 쉽게 응용 프로그램의 모양과 느낌에 변경 내용을 적용 하려면 부트스트랩의 테마 설정 기능을 사용할 수 있습니다. 기본적으로 Visual Studio 2013에서 ASP.NET 웹 응용 프로그램 템플릿을 부트스트랩 NuGet 패키지로 포함 됩니다.
> 
> **NuGet 패키지**
> 
> ASP.NET Web Forms 응용 프로그램 템플릿 집합이 포함 되어 [NuGet](http://www.nuget.org/) 패키지 합니다. 이러한 패키지는 오픈 소스 라이브러리 및 도구의 형태로 구성 요소화 된 기능을 제공합니다. 응용 프로그램을 테스트 하 고 만들 수 있도록 패키지의 다양 한 방법이 있습니다. Visual Studio에서는 쉽게 추가, 제거, NuGet 패키지를 업데이트 합니다. 개발자가 만들고도 NuGet에 패키지를 추가할 수 있습니다.
> 
> ![만들기 프로젝트-NuGet 대화 상자](create-the-project/_static/image8.png)
> 
> 패키지를 설치 하면 NuGet 솔루션에 파일을 복사 하 고 변경 내용이 필요한 참조를 추가 하 고 웹 응용 프로그램과 연결 된 구성 변경 등을 자동으로 합니다. 라이브러리를 제거 하려는 경우 NuGet 파일을 제거 하 고 없는 좀 더 남아 있도록 프로젝트에서 만든 모든 변경 내용을 취소 합니다. NuGet은에서 사용할 수는 **도구** Visual Studio에서 메뉴.
> 
> **jQuery**
> 
> [jQuery](http://jquery.com/) 는 HTML 문서를 통과, 이벤트 처리, 애니메이션, 및 신속한 웹 개발에 Ajax 상호 작용을 간소화 하는 신속 하 고 간결한 JavaScript 라이브러리. JQuery JavaScript 라이브러리는 ASP.NET Web Forms 응용 프로그램 템플릿을에 NuGet 패키지로 포함 됩니다.
> 
> **비 가시적인 유효성 검사**
> 
> 클라이언트 쪽 유효성 검사 논리에 대 한 비 가시적인 JavaScript를 사용 하도록 구성 된 기본 제공 유효성 검사 컨트롤. 이 크게 JavaScript 페이지 태그에 인라인으로 렌더링할지 줄일 수 및 전체 페이지 크기를 줄입니다. 비 가시적인 유효성 검사의 설정을 기반으로 ASP.NET Web Forms 응용 프로그램 템플릿에 전역적으로 추가 됩니다는 &lt;appSettings&gt; 의 요소는 *Web.config* 응용 프로그램의 루트에 파일입니다.
> 
> **Entity Framework Code First**
> 
> Wingtip Toys 응용 프로그램 외에도 ASP.NET Web Forms 응용 프로그램 템플릿에 대 한 기능을 사용 하 여 [Entity Framework Code First](https://weblogs.asp.net/scottgu/archive/2010/12/08/announcing-entity-framework-code-first-ctp5-release.aspx)는 데이터로 작업할 때 코드 중심 개발을 수행할 수 있는 NuGet 라이브러리입니다. 간단히 말해서, 데이터베이스 부분을 작성 하는 코드에 따라 응용 프로그램을 만듭니다. Entity Framework를 사용 하 여 검색 하 고 강력한 형식의 개체로 데이터를 조작 합니다. 이렇게 하면 데이터를 액세스 하는 방법을 대 한 세부 정보를 사용 하지 않고 응용 프로그램의 비즈니스 논리에 집중할 수 있습니다.
> 
> 설치 된 라이브러리 및 ASP.NET Web Forms 서식 파일에 포함 된 패키지에 대 한 자세한 내용은 설치 된 NuGet 패키지 목록은 참조 하십시오. 이렇게 하려면 Visual Studio에는 새 Web Forms 프로젝트를 만들고 **도구**  - &gt; **라이브러리 패키지 관리자**  - &gt; **관리 솔루션에 대 한 NuGet 패키지**를 선택 하 고 **설치 된 패키지** 에 **NuGet 패키지 관리** 대화 상자.


### <a name="touring-visual-studio"></a>Visual Studio touring

Visual Studio에서 주 창에 포함 된 **솔루션 탐색기**, **서버 탐색기** (**데이터베이스 탐색기** Express에서), **속성 창**, **도구 상자**, **도구 모음**, 및 **문서 창**합니다.

![만들기 프로젝트-NuGet 대화 상자](create-the-project/_static/image9.png)

Visual Studio에 대 한 자세한 내용은 참조 [Visual Web Developer에 시각적 기준](https://msdn.microsoft.com/library/ee410104.aspx)합니다.

## <a name="summary"></a>요약

이 자습서에서 생성, 검토 하 고 하면 기본 Web Forms 응용 프로그램을 실행 합니다. 기본 Web forms 응용 프로그램의 다양 한 기능을 검토 하 고 Visual Studio 환경을 사용 하는 방법에 대 한 몇 가지 기본 사항을 배웠습니다. 다음 자습서에서는 데이터 액세스 계층을 만듭니다.

## <a name="additional-resources"></a>추가 리소스

[오른쪽 프로그래밍 모델을 선택 합니다.](../../../videos/how-do-i/choosing-the-right-programming-model.md)   
[웹 응용 프로그램 프로젝트와 웹 사이트 프로젝트 비교](https://msdn.microsoft.com/library/dd547590.aspx)   
[ASP.NET Web Forms 페이지 개요](https://msdn.microsoft.com/library/428509ah.aspx)

>[!div class="step-by-step"]
[이전](introduction-and-overview.md)
[다음](create_the_data_access_layer.md)
