---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/determining-what-files-need-to-be-deployed-cs
title: 배포 파일에 필요한 확인 (C#) | Microsoft Docs
author: rick-anderson
description: 개발 환경에서 프로덕션 환경에 배포 해야 하는 파일 정도 따라 결정 여부는 ASP.NET 응용 프로그램이 빌드된 주세요...
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/01/2009
ms.topic: article
ms.assetid: f8d78a88-cc91-40d8-bce3-3d7954f6033b
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/determining-what-files-need-to-be-deployed-cs
msc.type: authoredcontent
ms.openlocfilehash: ff5f1d7d156efa12d97382db56211a07c43178fd
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30888671"
---
<a name="determining-what-files-need-to-be-deployed-c"></a>배포 파일에 필요한 확인 (C#)
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/4/5/F/45F815EC-8B0E-46D3-9FB8-2DC015CCA306/ASPNET_Hosting_Tutorial_02_CS.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial02_FilesToDeploy_cs.pdf)

> 개발 환경에서 프로덕션 환경에 배포 해야 하는 파일 정도 따라 결정 여부 ASP.NET 응용 프로그램 모델 웹 사이트 또는 웹 응용 프로그램 모델을 사용 하 여 작성 되었습니다. 이러한 두 가지 프로젝트 모델 및 프로젝트 모델 배포에 미치는 영향에 대해 자세히 알아보기


## <a name="introduction"></a>소개

ASP.NET 웹 응용 프로그램을 배포 하려면 프로덕션 환경에는 개발 환경에서 ASP.NET 관련 파일을 복사 해야 합니다. ASP.NET 관련 파일에 ASP.NET 웹 페이지 태그 및 코드와 클라이언트 및 서버 쪽 파일을 지원 합니다. 클라이언트 쪽 지원 파일은 해당 웹 페이지에서 참조 하 고 예를 들어 브라우저-CSS 파일, 이미지, JavaScript 파일에 직접 전송입니다. 서버 쪽에서 요청을 처리 하는 데 사용 되는 서버 쪽 지원 파일이 포함 됩니다. 이 구성 파일, 웹 서비스, 클래스 파일, 형식화 된 데이터 집합 및 LINQ 다른 규칙 으로부터 SQL 파일을 포함 합니다.

일반적으로 모든 클라이언트 쪽 지원 파일 개발 환경에서 프로덕션 환경에 복사 해야 하지만 (한 어셈블리로서버쪽코드명시적으로컴파일하는여부에따라달라집니다서버쪽지원파일복사`.dll` 파일) 또는 이러한 어셈블리를 자동으로 생성 된 발생 하는 경우. 이 자습서에서는 명시적으로이 컴파일 단계를 자동으로 발생할 때와 비교를 어셈블리에 코드를 컴파일할 때 배포 해야 하는 파일 강조 표시 합니다.

## <a name="explicit-compilation-versus-automatic-compilation"></a>명시적 컴파일을 자동 컴파일 비교

ASP.NET 웹 페이지 태그 및 소스 코드를 선언적으로 나뉩니다. 선언적 태그 부분 포함 HTML, 웹 컨트롤 및 데이터 바인딩 구문을 사용 합니다. Visual Basic 또는 C# 코드로 작성 된 이벤트 처리기를 포함 하는 코드 부분입니다. 태그와 코드 일부를 다른 파일에 일반적으로 구분 됩니다: `WebPage.aspx` 포함 하는 동안 선언 태그 `WebPage.aspx.cs` 코드를 저장 합니다.

ASP.NET 페이지를 라는 Clock.aspx 텍스트 속성이 현재 날짜 및 페이지가 로드 될 때 시간으로 설정 된 레이블 컨트롤을 포함 하는 것이 좋습니다. 선언적 태그 부분 (에 `Clock.aspx`)-Label 웹 컨트롤에 대 한 태그는 포함`<asp:Label runat="server" id="TimeLabel" />` -코드 부분 하는 동안 (에서 `Clock.aspx.cs`) 갖기는 `Page_Load` 이벤트 처리기를 다음 코드로:

[!code-csharp[Main](determining-what-files-need-to-be-deployed-cs/samples/sample1.cs)]

이 페이지에서는 페이지의 코드 부분에 대 한 요청을 처리 하는 ASP.NET 엔진에 대 한 순서 대로 (의 `WebPage.aspx.cs` 파일) 먼저 컴파일해야 합니다. 이 컴파일 명시적으로 또는 자동으로 발생할 수 있습니다.

컴파일할 때 발생 하는 명시적으로 경우 전체 응용 프로그램의 소스 코드는 하나 이상의 어셈블리로 컴파일됩니다 (`.dll` 파일)에 응용 프로그램의 `Bin` 디렉터리입니다. 컴파일 문제가 발생 하면 자동으로 생성 된 자동 생성 기본적으로 어셈블리는에 배치 된 `Temporary ASP.NET` 파일 폴더에서 찾을 수 있는 `%WINDOWS%\Microsoft.NET\Framework\`  *&lt;버전&gt;*, 이 위치를 통해 구성할 수는 있지만 [ `<compilation>` 요소](https://msdn.microsoft.com/library/s10awwz0.aspx) 에서 `Web.config`합니다. 명시적 컴파일을 사용한 ASP.NET 응용 프로그램의 코드를 어셈블리로 컴파일할 작업을 수행 해야 하 고이 단계를 배포 하기 전에 발생 합니다. 자동 컴파일을 컴파일 프로세스 리소스에 처음 액세스할 때 웹 서버에서 발생 합니다.

사용 하면 어떤 컴파일 모델에 관계 없이, 모든 ASP.NET 페이지의 태그 부분 (의 `WebPage.aspx` 파일) 프로덕션 환경에 복사 해야 합니다. 어셈블리를 복사 해야 명시적 컴파일을 사용한는 `Bin` 폴더, ASP.NET 페이지의 코드 부분을 복사 하지 않아도 (의 `WebPage.aspx.cs` 파일). 자동 컴파일 코드 표시 되며 해당 페이지를 방문 하는 경우 자동으로 컴파일할 수 있도록 코드 부분 파일을 복사 해야 합니다. 각 ASP.NET 웹 페이지의 태그 부분에 포함 되어는 `@Page` 지시문을 명시적으로 이미 연결 된 코드 페이지의 컴파일된 여부 또는 자동으로 컴파일할 필요가 있는지 여부를 나타내는 특성입니다. 결과적으로, 프로덕션 환경 중 하나 컴파일 모델을 원활 하 게 사용할 수 있으며 명시적 또는 자동 컴파일을 사용 해야 함을 나타내기 위해 특별 한 구성 설정을 적용할 필요가 없습니다.

표 1에는 배포와 자동 컴파일 명시적 컴파일을 사용 하는 경우 서로 다른 파일 요약 되어 있습니다. 컴파일에 관계 없이 모델에 사용 하면 항상의 어셈블리를 배포 해야는 `Bin` 해당 폴더가 있으면 폴더에 있습니다. `Bin` 폴더 명시적 컴파일 모델을 사용 하는 경우 컴파일된 소스 코드를 포함 하는 웹 응용 프로그램에 특정 어셈블리에 포함 되어 있습니다. `Bin` 디렉터리도 다른 프로젝트에서 어셈블리 및 사용 중일 수 있습니다, 타사 또는 오픈 소스 어셈블리를 포함 하 고는 프로덕션 서버에 저장 하는 데 필요 합니다. 따라서 일반으로 복사 된 `Bin` 프로덕션을 배포할 때까지 폴더입니다. (자동 컴파일 모델을 사용 하 고 모든 외부 어셈블리를 사용 하지 않는 경우 없을 수는 `Bin` 확인 되는 디렉터리-!)

| **컴파일 모델** | **태그 부분 파일 배포 합니까?** | **소스 코드 파일을 배포 합니까?** | **어셈블리를 배포 `Bin` 디렉터리?** |
| --- | --- | --- | --- |
| 명시적 컴파일 | 예 | 아니요 | 예 |
| 자동 컴파일 | 예 | 예 | 예 (있는 경우) |

**표 1:** 배포한 어떤 파일이 사용 되는 컴파일 모델에 따라 달라 집니다.

## <a name="taking-a-trip-down-memory-lane"></a>메모리 레인 아래로 여행 라인으로 전환

사용 되는 어떤 컴파일 방법에 따라 다름, 부분적으로 Visual Studio에서 ASP.NET 응용 프로그램을 관리 하는 방법 패키지와 마찬가지로 네 개의 서로 다른 버전의 Visual Studio-Visual Studio.NET 2002, Visual Studio.NET 2003, Visual Studio 2005 및 Visual Studio 2008 내용이 2000 년에 NET의 초기 합니다. Visual Studio.NET 2002 및 2003 관리를 사용 하 여 ASP.NET 응용 프로그램에서 *웹 응용 프로그램 프로젝트 모델*합니다. 웹 응용 프로그램 프로젝트 모델의 주요 기능은 다음과 같습니다.

- 프로젝트 구성을 단일 프로젝트 파일에 정의 된 파일입니다. 모든 파일은 프로젝트 파일에 정의 되어 있지는 Visual Studio에서 웹 응용 프로그램의 일부로 간주 되지 않습니다.
- 명시적 컴파일을 사용합니다. 프로젝트 내에서 코드 파일에 배치 된 단일 어셈블리로 컴파일합니다 프로젝트를 빌드하면는 `Bin` 폴더입니다.

Microsoft Visual Studio 2005를 릴리스 했습니다. 이러한 제거 웹 응용 프로그램 프로젝트 모델에 대 한 지원 하 고 웹 사이트 프로젝트 모델을 대체 합니다. 웹 사이트 프로젝트 모델 differentiated 자체 웹 응용 프로그램 프로젝트 모델에서 다음과 같은 방법으로:

- 프로젝트 파일을 확인 하는 단일 프로젝트 파일을 설치 하는 대신 파일 시스템 대신 사용 됩니다. 즉, 웹 응용 프로그램 폴더 (또는 하위 폴더) 안에 있는 모든 파일에는 프로젝트의 일부로 간주 됩니다.
- Visual Studio에서 프로젝트를 빌드하면에서는 변수에서 어셈블리는 `Bin` 디렉터리입니다. 대신, 웹 사이트 프로젝트를 빌드하는 컴파일 타임 오류를 보고 합니다.
- 자동 컴파일 지원 합니다. 코드 미리 컴파일된 (명시적 컴파일)을 사용할 수 있지만 웹 사이트 프로젝트를 프로덕션 환경에 태그 및 소스 코드를 복사 하 여 일반적으로 배포 됩니다.

Microsoft Visual Studio 2005 서비스 팩 1을 릴리스 하는 경우 웹 응용 프로그램 프로젝트 모델을 다시 합니다. 그러나 Visual Web Developer만 웹 사이트 프로젝트 모델을 지원 하도록 계속 합니다. 다행 스럽게도이 제한은 Visual Web Developer 2008 서비스 팩 1 인해 삭제 되었습니다. 오늘 Visual Studio에 (Visual Web Developer) 웹 응용 프로그램 프로젝트 모델이 나 웹 사이트 프로젝트 모델을 사용 하 여 ASP.NET 응용 프로그램을 만들 수 있습니다. 두 모델의 장단점은 있습니다. 참조 [웹 응용 프로그램 프로젝트 소개: 웹 사이트 프로젝트 비교와 웹 응용 프로그램 프로젝트](https://msdn.microsoft.com/library/aa730880.aspx#wapp_topic5) 은 두 모델의 및 어떤 프로젝트 모델이 상황에 가장 적합 한 결정에 도움이 되는 비교에 대 한 합니다.

## <a name="exploring-the-sample-web-application"></a>샘플 웹 응용 프로그램 탐색

이 자습서에 대 한 다운로드 라는 책 검토 ASP.NET 응용 프로그램을 포함 합니다. 웹 사이트 사용자를 만들 수는 취미 웹 사이트를 모방 해당 책을 공유 하는 온라인 커뮤니티와 검토 합니다. 이 ASP.NET 웹 응용 프로그램은 매우 간단 하 고 다음 리소스 구성:

- `Web.config`를 응용 프로그램의 구성 파일입니다.
- 마스터 페이지 (`Site.master`).
- 7 개의 서로 다른 ASP.NET 페이지: 

    - ~`/Default.aspx`-사이트의 홈 페이지입니다.
    - ~`/About.aspx` -"에 대 한 사이트의" 페이지.
    - ~`/Fiction/Default.aspx` -소설 책 검토 된에 나열 된 페이지가 있습니다. 

        - ~`/Fiction/Blaze.aspx` -Richard Bachman novel 검토 *Blaze*합니다.
    - ~/`Tech/Default.aspx` -검토 된 기술 책 나열 된 페이지가 있습니다. 

        - ~/`Tech/CYOW.aspx`-검토 *직접 웹 사이트 만들기*합니다.
        - ~/`Tech/TYASP35.aspx` -검토 *업무량이 직접 ASP.NET 3.5 24 시간 동안에서*합니다.
- Styles 폴더에 3 개의 다른 CSS 파일을 선택 합니다.
- -ASP.NET 로고와 이미지의 세 가지 검토 한 책의 내부적으로 Powered-모든 파일에 있는 이미지 4 개는 `Images` 폴더입니다.
- A `Web.sitemap` 사이트 맵을 정의 하 고 메뉴에 표시 하는 데 사용 되는 파일의 `Default.aspx` 루트 디렉터리의 페이지 및 `Fiction` 및 `Tech` 폴더입니다.
- 라는 클래스 파일을 `BasePage.cs` 기본을 정의 하는 `Page` 클래스입니다. 기능을 확장 하는이 클래스는 `Page` 자동으로 설정 하 여 클래스는 `Title` 속성 사이트 맵에서 페이지의 위치에 기반 합니다. 간단히 말해, 모든 ASP.NET 코드 숨김 클래스를 확장 하는 `BasePage` (대신 `System.Web.UI.Page`) 제목 사이트 맵에서 해당 위치에 따라 값으로 설정 해야 합니다. 예를 들어, 볼 때는 ~ /`Tech/CYOW.aspx` 페이지 제목이 "홈:: 기술:: 만들 직접 웹 사이트"로 설정 되어 있습니다.

그림 1에는 브라우저를 통해 볼 때 책 검토 웹 사이트의 스크린 샷을 나와 있습니다. 페이지를 참조 하는 여기 ~ /`Tech/TYASP35.aspx`, 책을 검토 하는 *업무량이 직접 ASP.NET 3.5 24 시간 동안에서*합니다. 에 정의 된 사이트 맵 구조를 기반으로 하는 페이지 및 왼쪽된 열에서 메뉴의 맨 위쪽에 걸쳐 있는 이동 경로 탐색 `Web.sitemap`합니다. 오른쪽 위 모퉁이에 이미지의 크기는 이미지에 있는 책 표지 중 하나는 `Images` 폴더입니다. 가장 중요 한 페이지 레이아웃 마스터 페이지에 정의 되어 있는 동안 Styles 폴더의 CSS 파일에 의해 명시 하는 스타일 시트 규칙 연계를 통해 웹 사이트의 모양과 느낌 정의한 `Site.master`합니다.


[![검토 하는 책 웹 사이트가 타이틀 목록에 리뷰를 제공합니다.](determining-what-files-need-to-be-deployed-cs/_static/image2.png)](determining-what-files-need-to-be-deployed-cs/_static/image1.png)

**그림 1:** 책 검토 웹 사이트가 제공 다양 한 제목에서 검토 ([전체 크기 이미지를 보려면 클릭](determining-what-files-need-to-be-deployed-cs/_static/image3.png))


이 응용 프로그램 데이터베이스입니다; 사용 하지 않습니다. 각 검토 별도 웹 페이지 응용 프로그램에서으로 구현 됩니다. 이 자습서 (및 다음 몇 가지 자습서) 데이터베이스를 하지 않은 웹 응용 프로그램을 배포 하는 과정을 안내 합니다. 그러나 이후 자습서에서는이 응용 프로그램을 검토, 독자의 의견 및 기타 정보는 데이터베이스 내의 저장 돋보이게 할 하 고 데이터 기반 웹 응용 프로그램을 올바르게 배포 하기 위해 수행 해야 하는 단계를 설명 합니다.

> [!NOTE]
> 이러한 자습서 웹 호스트 공급자는 ASP.NET 응용 프로그램 호스팅에 집중 하 고 ASP 같은 보조 항목을 탐색 하지는 않습니다. NET의 사이트 맵 시스템 또는 한 자료를 사용 하 여 `Page` 클래스입니다. 이러한 기술에 대 한 자세한 내용은 및 자습서 전체에서 포함 된 기타 항목에 대해 각 자습서의 끝에 추가 정보 섹션을 참조 합니다.


이 자습서 다운로드에는 웹 응용 프로그램의 두 복사본이, 다른 Visual Studio 프로젝트 형식으로 구현 하는 각: BookReviewsWAP, 웹 응용 프로그램 프로젝트 및 BookReviewsWSP, 웹 사이트 프로젝트입니다. 두 프로젝트가 모두 Visual Web Developer 2008 SP1를 사용 하 여 만든 및 ASP.NET 3.5 s p 1을 사용 합니다. 사용 하려면 이러한 프로젝트 내용을 바탕으로 압축을 푸는 시작 합니다. 웹 응용 프로그램 프로젝트 (BookReviewsWAP)을 열고 BookReviewsWAP 폴더를 탐색, 솔루션 파일을 두 번 `BookReviewsWAP.sln`합니다. (BookReviewsWSP) 웹 사이트 프로젝트를 열려면 Visual Studio를 시작 하 고 그런 다음 웹 사이트 열기 옵션을 선택 하 고 파일 메뉴에서를 찾은 `BookReviewsWSP` 폴더 바탕 화면에서 확인을 클릭 합니다.


파일 확인이 자습서의 나머지 두 개의 섹션에 응용 프로그램을 배포 하는 경우 프로덕션 환경에 복사 해야 합니다. 다음 두 자습서- *[Your 사이트를 사용 하 여 FTP 배포](deploying-your-site-using-an-ftp-client-cs.md)* 및 *[배포 Your 사이트를 사용 하 여 Visual Studio](deploying-your-site-using-visual-studio-cs.md)* -여러 가지 방법을 보여 줍니다 웹 호스트 공급자에이 파일을 복사 합니다.

## <a name="determining-the-files-to-deploy-for-the-web-application-project"></a>배포할 웹 응용 프로그램 프로젝트에 대 한 파일을 확인 합니다.

웹 응용 프로그램 프로젝트 모델에서 명시적 컴파일을 사용-프로젝트의 소스 코드는 응용 프로그램을 빌드할 때마다 단일 어셈블리로 컴파일됩니다. ASP.NET 페이지의 코드 숨김 파일을 포함 하는이 컴파일 (~ /`Default.aspx.cs`, ~ /`About.aspx.cs`등),으로 `BasePage.cs` 클래스입니다. 결과 어셈블리 BookReviewsWAP.dll 이름이 고 응용 프로그램의에 위치한 `Bin` 디렉터리입니다.

그림 2에서는 책 검토 웹 응용 프로그램 프로젝트를 구성 하는 파일을 보여 줍니다.


[![웹 응용 프로그램 프로젝트를 구성 하는 파일을 나열 하는 솔루션 탐색기](determining-what-files-need-to-be-deployed-cs/_static/image5.png)](determining-what-files-need-to-be-deployed-cs/_static/image4.png)

**그림 2**: 웹 응용 프로그램 프로젝트를 구성 하는 파일을 나열 하는 솔루션 탐색기


웹 응용 프로그램 프로젝트 모델 시작을 사용 하 여 명시적으로 가장 최근의 소스 코드를 어셈블리로 컴파일할 수 있도록 응용 프로그램을 작성 하 여 개발 하는 ASP.NET 응용 프로그램을 배포 합니다. 다음으로 프로덕션 환경에 다음 파일을 복사 합니다.

- 와 같은 모든 ASP.NET에 대 한 선언적 태그를 포함 하는 파일 페이지 ~ /`Default.aspx`, ~ /`About.aspx`등입니다. 모든 마스터 페이지 및 사용자 정의 컨트롤에 대 한 선언적 태그를 또한 복사본입니다.
- 어셈블리 (`.dll` 파일)에 `Bin` 폴더입니다. 프로그램 데이터베이스 파일을 복사할 필요가 없습니다 (`.pdb`) 또는 XML 파일을 찾을 수 있습니다는 `Bin` 디렉터리입니다.

프로덕션 환경에 ASP.NET 페이지의 소스 코드 파일을 복사할 필요가 없습니다 또는 복사 해야 하는 `BasePage.cs` 클래스 파일입니다.

> [!NOTE]
> 그림 2에서 볼 수 있듯이 `BasePage` 이라는 폴더에 배치 하는 프로젝트에 클래스 파일로 클래스가 구현 되는 `HelperClasses`합니다. 프로젝트를 컴파일할 때의 코드는 `BasePage.cs` ASP.NET 페이지의 코드 숨김 클래스와 함께 단일 어셈블리로 파일은 컴파일됩니다 `BookReviewsWAP.dll.` ASP.NET 라는 특수 폴더에는 `App_Code` 웹에 대 한 클래스 파일을 저장 하도록 디자인 된 사이트 프로젝트입니다. 코드는 `App_Code` 폴더 자동으로 컴파일되고 따라서 사용할 수 없습니다 웹 응용 프로그램 프로젝트입니다. 기본 폴더에 응용 프로그램의 클래스 파일을 배치 해야 대신 `HelperClasses`, 또는 `Classes`, 또는 이와 비슷한 합니다. 또는 별도 클래스 라이브러리 프로젝트에 클래스 파일을 배치할 수 있습니다.


ASP.NET 관련 태그 파일과에 있는 어셈블리를 복사 하는 것 외에도 `Bin` 폴더도 해야-이미지 및 CSS 파일-클라이언트 쪽 지원 파일 뿐만 아니라 다른 서버 쪽 지원 파일을 복사 `Web.config` 및 `Web.sitemap`합니다. 이러한 클라이언트 및 서버 쪽 지원 파일을 자동 또는 명시적 컴파일을 사용 하는지 여부에 관계 없이 프로덕션 환경에 복사 해야 합니다.

## <a name="determining-the-files-to-deploy-for-the-web-site-project-files"></a>배포할 웹 사이트 프로젝트 파일에 대 한 파일을 확인 합니다.

웹 사이트 프로젝트 모델 자동 컴파일을, 웹 응용 프로그램 프로젝트 모델을 사용 하는 경우 사용할 수 없는 기능을 지원 합니다. 명시적 컴파일을 사용 하면 프로젝트의 소스 코드를 어셈블리로 컴파일할 하 고 해당 어셈블리를 프로덕션 환경에 복사 해야 합니다. 반면에 자동 컴파일을 사용 하면 단순히 소스 코드 프로덕션 환경에 복사한 필요에 따라 필요에 따라 런타임에 의해 컴파일됩니다.

Visual Studio에서 빌드 메뉴 옵션은 웹 응용 프로그램 프로젝트와 웹 사이트 프로젝트에 있습니다. 프로젝트의 소스 코드에 있는 단일 어셈블리로 컴파일합니다 웹 응용 프로그램 프로젝트를 빌드하는 `Bin` 디렉터리; 건물 웹 사이트 프로젝트를 컴파일 타임 오류를 확인 하지만 모든 어셈블리를 만들지 않습니다. 해야 할 웹 사이트 프로젝트 모델 모두 사용 하 여 개발 하는 ASP.NET 응용 프로그램을 배포 하는 복사 프로덕션 환경에 적절 한 파일 이지만 바랍니다 첫 번째 빌드할 프로젝트를 컴파일 타임 오류가 없는지 확인 하십시오.

그림 3에서는 책 검토 웹 사이트 프로젝트를 구성 하는 파일을 보여 줍니다.


 [![웹 사이트 프로젝트를 구성 하는 파일을 나열 하는 솔루션 탐색기](determining-what-files-need-to-be-deployed-cs/_static/image7.png)](determining-what-files-need-to-be-deployed-cs/_static/image6.png) 

**그림 3**: 웹 사이트 프로젝트를 구성 하는 파일을 나열 하는 솔루션 탐색기


웹 사이트 프로젝트를 배포 된 코드 파일과 함께 ASP.NET 페이지, 마스터 페이지 및 사용자 정의 컨트롤에 대 한 태그 페이지가 포함 된 프로덕션 환경-모든 ASP.NET 관련 파일을 복사 해야 합니다. BasePage.cs 같은 모든 클래스 파일을 복사 해야 할 수도 있습니다. `BasePage.cs` 파일은 `App_Code` 클래스 파일에 대 한 웹 사이트 프로젝트에서 사용 되는 특별 한 ASP.NET 폴더에 있는 폴더입니다. 특수 폴더의 클래스 파일에 프로덕션 만들 필요는 `App_Code` 개발 환경에 폴더에 복사 해야는 `App_Code` 프로덕션 폴더입니다.

ASP.NET 태그 및 소스 코드 파일을 복사 하는 것 외에도 또한 해야-이미지 및 CSS 파일-클라이언트 쪽 지원 파일 뿐만 아니라 다른 서버 쪽 지원 파일을 복사할 `Web.config` 및 `Web.sitemap`합니다.

> [!NOTE]
> 웹 사이트 프로젝트 명시적 컴파일을 사용할 수도 있습니다. 명시적으로 웹 사이트 프로젝트를 컴파일하는 방법에 대 한 이후 자습서를 검사 합니다.


## <a name="summary"></a>요약

ASP.NET 응용 프로그램을 배포 하려면 개발 환경에서 프로덕션 환경에 필요한 파일을 복사 해야 합니다. 동기화 하는 파일의 정확한 집합 여부 ASP.NET 응용 프로그램의 코드가 명시적으로 또는 자동으로 컴파일됩니다에 따라 달라 집니다. 사용 되는 컴파일 전략은의 영향을 Visual Studio 구성 되어 있는지 여부 웹 응용 프로그램 프로젝트 모델이 나 웹 사이트 프로젝트 모델을 사용 하 여 ASP.NET 응용 프로그램을 관리 합니다.

웹 응용 프로그램 프로젝트 모델 명시적 컴파일을 사용 하 여 및에서 단일 어셈블리에 프로젝트의 코드를 컴파일하는 `Bin` 폴더입니다. 응용 프로그램, ASP.NET 페이지의 태그 부분과의 콘텐츠를 배포 하는 경우는 `Bin` 폴더 프로덕션 환경에 푸시 해야;-코드 파일 및 코드 숨김 클래스, 예를 들어-응용 프로그램의 소스 코드 필요는 없습니다 프로덕션 환경에 복사 되도록 합니다.

웹 사이트 프로젝트 모델 자습서 나중에 알 수 있듯이 명시적으로 웹 사이트 프로젝트를 컴파일할 수 있지만 기본적으로 자동 컴파일을 사용 합니다. 자동 컴파일을 사용 하는 ASP.NET 응용 프로그램을 배포 하려면 태그 부분 *및* 소스 코드를 프로덕션 환경에 복사 해야 합니다. 코드가 처음으로 요청 될 때 자동으로 프로덕션 환경에 컴파일됩니다.

개발 및 프로덕션 환경 간에 동기화 하는 데 필요한 파일을 살펴보았습니다 했으므로 책 검토 응용 프로그램 웹 호스트 공급자에 배포할 준비가 됩니다.

만족도 매우 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET 컴파일 개요](https://msdn.microsoft.com/library/ms178466.aspx)
- [ASP.NET 사용자 정의 컨트롤](https://msdn.microsoft.com/library/y6wb1a0e.aspx)
- [ASP를 검사 합니다. NET의 사이트 탐색](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)
- [웹 응용 프로그램 프로젝트 소개](https://msdn.microsoft.com/library/aa730880.aspx)
- [마스터 페이지 자습서](../master-pages/creating-a-site-wide-layout-using-master-pages-cs.md)
- [페이지 간 코드 공유](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/pages/code.aspx)
- [ASP.NET 페이지의 코드 숨김 클래스에 대 한 사용자 지정 기본 클래스를 사용 하 여](http://aspnet.4guysfromrolla.com/articles/041305-1.aspx)
- [Visual Studio 2005의 웹 사이트 프로젝트 시스템: 것 란 무엇이 고 왜 수행할가?](https://weblogs.asp.net/scottgu/archive/2005/08/21/423201.aspx)
- [연습: Visual Studio에서 웹 응용 프로그램 프로젝트를 웹 사이트 프로젝트를 변환](https://msdn.microsoft.com/library/aa983476.aspx)

> [!div class="step-by-step"]
> [이전](asp-net-hosting-options-cs.md)
> [다음](deploying-your-site-using-an-ftp-client-cs.md)
