---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4
title: ASP.NET MVC 4 소개 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서는 여기 Visual Studio 2013을 사용 하 여 사용할 경우 업데이트 된 버전입니다. 새 자습서 t를 통해 많은 향상 된 기능을 제공 하는 ASP.NET MVC 5를 사용 하는 중...
ms.author: riande
ms.date: 08/15/2012
ms.assetid: ed66530a-04d5-49eb-b76a-85be1f57c437
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 6442477c22c124f782642b770f9394873a988e85
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41829353"
---
<a name="intro-to-aspnet-mvc-4"></a>ASP.NET MVC 4 소개
====================
[Rick Anderson](https://github.com/Rick-Anderson)

> 이 자습서는 사용할 수 있는 경우 업데이트 된 버전 [같습니다](../../getting-started/introduction/getting-started.md) 사용 하 여 [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)합니다. 새 자습서에는이 자습서를 통해 많은 향상 된 기능을 제공 하는 ASP.NET MVC 5를 사용 합니다.
> 
> 이 자습서는 Microsoft를 사용 하 여 ASP.NET MVC 4 웹 응용 프로그램을 빌드하는 기본 사항 설명 [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) 또는 Visual Web Developer 2010 Express 서비스 팩 1입니다. 자습서를 완료 하려면 어떤 항목도 설치 하지 않아도 됩니다. visual Studio 2012 좋습니다. Visual Studio 2010을 사용 하는 경우 아래 구성 요소를 설치 해야 합니다. 다음 링크를 클릭 하 여 이들 모두를 설치할 수 있습니다.
> 
> - [Visual Studio Web Developer Express SP1 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 4 용 WPI 설치 관리자](https://go.microsoft.com/fwlink/?LinkId=243392)
> - [LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLLocalDBOnly_11_0)
> - [SSDT](https://blogs.msdn.com/b/rickandy/archive/2012/08/02/installing-and-using-sql-server-data-tools-ssdt-on-visual-studio-2010-and-vwd.aspx)
> 
> Visual Web Developer 2010 대신 Visual Studio 2010을 사용 하는 경우 설치 합니다 [ASP.NET MVC 4에 대 한 설치 관리자 WPI](https://go.microsoft.com/fwlink/?LinkId=243392) 및: [Visual Studio 2010 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)
> 
> C# 소스 코드를 사용 하 여 Visual Web Developer 프로젝트는 다음이 항목과 함께 사용할 수 있습니다. [C# 버전 다운로드](https://code.msdn.microsoft.com/Intro-to-ASPNET-MVC-4-61d0219d/file/114480/1/MvcMovie.zip)합니다.
> 
> 이 자습서에서 Visual Studio에서 응용 프로그램을 실행 합니다. 또한 가능 응용 프로그램 사용 가능한 인터넷을 통해 호스팅 공급자에 배포 하 여 합니다. Microsoft에서 제공 하는 무료 웹 호스팅에 최대 10 개의 웹 사이트를 [Windows Azure 평가판 계정](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604)합니다. Visual Studio 웹 프로젝트를 Windows Azure 웹 사이트를 배포 하는 방법에 대 한 정보를 참조 하세요 [만들기 및 ASP.NET 웹 사이트 및 Visual Studio를 사용 하 여 SQL Database를 배포](https://docs.microsoft.com/dotnet/azure/)합니다. 이 자습서에는 Windows Azure SQL Database (이전의 SQL Azure)에 SQL Server 데이터베이스를 배포 하려면 Entity Framework Code First 마이그레이션을 사용 하는 방법을 보여 줍니다.
> 
> Rick anderson이 자습서가 작성 ( [ @RickAndMSFT ](https://twitter.com/#!/RickAndMSFT) ).


## <a name="what-youll-build"></a>만들 내용

> [!NOTE]
> 이 자습서는 사용할 수 있는 경우 업데이트 된 버전 [같습니다](../../getting-started/introduction/getting-started.md) 사용 하 여 [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)합니다. 새 자습서에는이 자습서를 통해 많은 향상 된 기능을 제공 하는 ASP.NET MVC 5를 사용 합니다.


만들기, 편집, 검색 및 나열 하는 데이터베이스에서 동영상을 지 원하는 간단한 영화 목록 응용 프로그램을 구현할 수 있습니다. 다음은 빌드할 응용 프로그램의 두 가지 스크린샷입니다. 데이터베이스에서 동영상 목록을 표시 하는 페이지가 포함 됩니다.

![](intro-to-aspnet-mvc-4/_static/image1.png)

또한 응용 프로그램 추가, 편집 및 개별 문제에 대 한 참조 정보 뿐만 아니라 영화를 삭제할 수 있습니다. 데이터베이스에 저장 된 데이터가 올바른지 확인 하려면 유효성 검사를 포함 하는 모든 데이터 입력 시나리오입니다.

![](intro-to-aspnet-mvc-4/_static/image2.png)

## <a name="getting-started"></a>시작

Visual Studio Express 2012 또는 Visual Web Developer 2010 Express를 실행 하 여 시작 합니다. 이 시리즈에서는 Visual Studio Express 2012, 에서만 스크린 샷 대부분 Visual Studio 2010 SP1, Visual Studio 2012, Visual Studio Express 2012 또는 Visual Web Developer 2010 Express를 사용 하 여이 자습서를 완료할 수 있습니다. 선택 **새 프로젝트** 에서 합니다 **시작** 페이지입니다.

Visual Studio IDE 또는 통합된 개발 환경입니다. Microsoft Word를 사용 하 여 문서를 작성 하는 것 처럼 응용 프로그램을 만드는 IDE를 사용 합니다. Visual Studio에서 사용할 수 있는 다양 한 옵션을 보여 주는 맨 위에 있는 도구 모음이 있습니다. IDE에서 작업을 수행 하는 또 다른 방법은 제공 하는 메뉴가 있습니다. (예를 들어, 선택 하는 대신 **새 프로젝트** 에서 합니다 **시작** 페이지에서 메뉴를 사용 하 고 선택할 수 **파일** &gt; **새프로젝트**.)

![](intro-to-aspnet-mvc-4/_static/image3.png)

## <a name="creating-your-first-application"></a>응용 프로그램 처음 만들기

Visual Basic 또는 Visual C# 프로그래밍 언어로 사용 하 여 응용 프로그램을 만들 수 있습니다. 왼쪽의 Visual C#을 선택 하 고 선택한 **ASP.NET MVC 4 웹 응용 프로그램**합니다. 프로젝트 이름을 &quot;MvcMovie&quot; 을 클릭 한 다음 **확인**합니다.

![](intro-to-aspnet-mvc-4/_static/image4.png)

에 **새 ASP.NET MVC 4 프로젝트** 대화 상자에서 **인터넷 응용 프로그램**합니다. 둡니다 **Razor** 기본 뷰 엔진으로 합니다.

![](intro-to-aspnet-mvc-4/_static/image5.png)

**확인**을 클릭합니다. 있다면 응용 프로그램을 사용 지금은 아무 작업도 수행 하지 않고 방금 만든 ASP.NET MVC 프로젝트에 대 한 기본 템플릿을 사용 하는 visual Studio! 이 간단한 &quot;Hello World!&quot; 프로젝트의 응용 프로그램을 시작 하는 것이 좋습니다.

![](intro-to-aspnet-mvc-4/_static/image6.png)

**디버그** 메뉴에서 **디버깅 시작**을 선택합니다.

![](intro-to-aspnet-mvc-4/_static/image7.png)

디버깅을 시작 하려면 바로 가기 키 F5 인지 확인 합니다.

F5 Visual Studio IIS Express를 시작 하 고 웹 응용 프로그램을 실행 하면 됩니다. 그런 다음 visual Studio가 브라우저를 시작 하 고 응용 프로그램의 홈 페이지를 엽니다. 브라우저의 주소 표시줄에 다음과 같은 알림이 `localhost` 등은 표시 되지 않습니다 및 `example.com`합니다. 있기 때문입니다 `localhost` 는 방금 빌드한 응용 프로그램을 실행 하는 경우에 자신의 로컬 컴퓨터는 항상 가리킵니다. Visual Studio 웹 프로젝트를 실행할 때 임의 포트를 웹 서버에 사용 됩니다. 아래 이미지에서 포트 번호가 41788입니다. 응용 프로그램을 실행 하는 경우 아마도 다른 포트 번호를 표시 됩니다.

![](intro-to-aspnet-mvc-4/_static/image8.png)

즉시이 기본 템플릿을 사용 하면 집, 연락처 및에 대 한 페이지입니다. 또한 등록 및 로그인에 대 한 지원을 제공 하 고 Facebook 및 Twitter에 연결 합니다. 다음 단계는이 응용 프로그램의 작동 방식을 변경할 좀 더 자세히 알아보고 ASP.NET MVC 하는 것입니다. 브라우저를 닫고 몇 가지 코드를 변경해 보겠습니다.

> [!div class="step-by-step"]
> [다음](adding-a-controller.md)
