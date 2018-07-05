---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/determining-what-files-need-to-be-deployed-cs
title: 이 배포 되도록 파일 확인 (C#) | Microsoft Docs
author: rick-anderson
description: 개발 환경에서 프로덕션 환경에 배포 해야 하는 파일에 일부 의존 하는지 여부를 ASP.NET 응용 프로그램이 빌드된 주세요...
ms.author: aspnetcontent
ms.date: 04/01/2009
ms.assetid: f8d78a88-cc91-40d8-bce3-3d7954f6033b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/determining-what-files-need-to-be-deployed-cs
msc.type: authoredcontent
ms.openlocfilehash: 3fb54feb32c3c4a4903c65751bf1a4ae4f016a22
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37831037"
---
<a name="determining-what-files-need-to-be-deployed-c"></a>이 배포 되도록 파일 확인 (C#)
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/4/5/F/45F815EC-8B0E-46D3-9FB8-2DC015CCA306/ASPNET_Hosting_Tutorial_02_CS.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial02_FilesToDeploy_cs.pdf)

> 개발 환경에서 프로덕션 환경에 배포 해야 하는 파일에 일부 의존 여부 ASP.NET 응용 프로그램 웹 사이트 모델 또는 웹 응용 프로그램 모델을 사용 하 여 작성 되었습니다. 이러한 두 프로젝트 모델과 프로젝트 모델 배포에 미치는 영향에 대해 알아보기


## <a name="introduction"></a>소개

ASP.NET 웹 응용 프로그램 개발 환경에서 프로덕션 환경에 ASP.NET 관련 파일을 복사 하는 작업을 수반 합니다. ASP.NET 웹 페이지 태그를 포함 하는 ASP.NET 관련 파일 및 코드와 클라이언트 쪽 및 서버 쪽 파일을 지원 합니다. 클라이언트 쪽 지원 파일이 해당 파일을 웹 페이지에서 참조 하 고 예를 들어 이미지, CSS 파일 및 JavaScript 파일을 브라우저에 직접 전송 합니다. 서버 쪽에서 요청을 처리 하는 데 사용 되는 서버 쪽 지원 파일이 포함 됩니다. 특히 SQL 파일에 구성 파일, 웹 서비스, 클래스 파일, 형식화 된 데이터 집합 및 LINQ를 포함 합니다.

일반적으로 모든 클라이언트 쪽 지원 파일을 복사할 개발 환경에서 프로덕션 환경에 있지만를 어셈블리로 (을 서버쪽코드를명시적으로컴파일하는여부에따라달라집니다서버쪽지원파일복사`.dll` 파일) 아니면 이러한 어셈블리를 자동으로 생성 된 것입니다. 이 자습서는 명시적으로 코드를 자동으로 수행이 컴파일 단계와 어셈블리로 컴파일할 때 배포 해야 하는 파일 강조 표시 합니다.

## <a name="explicit-compilation-versus-automatic-compilation"></a>자동 컴파일 및 명시적 컴파일

ASP.NET 웹 페이지 태그 및 소스 코드를 선언적으로 나뉩니다. 선언적 태그 부분 포함 HTML 웹 컨트롤 및 데이터 바인딩 구문을 사용 합니다. Visual Basic 또는 C# 코드로 작성 된 이벤트 처리기를 포함 하는 코드 부분입니다. 태그 및 코드 일부를 다른 파일에 일반적으로 구분 됩니다. `WebPage.aspx` 하는 동안 선언적 태그를 포함 `WebPage.aspx.cs` 코드를 포함 합니다.

현재 날짜 및 시간 페이지를 로드할 때 텍스트 속성을 설정할 레이블 컨트롤을 포함 하는 Clock.aspx 라는 ASP.NET 페이지를 것이 좋습니다. 선언적 태그 부분 (에 `Clock.aspx`)-Label 웹 컨트롤에 대 한 태그를 포함 하는`<asp:Label runat="server" id="TimeLabel" />` -코드 부분 (에 `Clock.aspx.cs`)는 것이 `Page_Load` 다음 코드를 사용 하 여 이벤트 처리기:

[!code-csharp[Main](determining-what-files-need-to-be-deployed-cs/samples/sample1.cs)]

이 페이지에서 페이지의 코드 부분에 대 한 요청을 처리 하는 ASP.NET 엔진에 대 한 순서 대로 (의 `WebPage.aspx.cs` 파일) 먼저 컴파일해야 합니다. 이 컴파일에 명시적으로 또는 자동으로 발생할 수 있습니다.

컴파일은 명시적으로 경우 전체 응용 프로그램의 소스 코드는 하나 이상의 어셈블리로 컴파일됩니다 (`.dll` 파일)에 응용 프로그램의 `Bin` 디렉터리입니다. 컴파일 문제가 발생 하면 자동으로 생성 된 자동 생성 어셈블리는 기본적으로에 배치 합니다 `Temporary ASP.NET` Files 폴더에서 찾을 수 있습니다 `%WINDOWS%\Microsoft.NET\Framework\`  *&lt;버전&gt;*, 이 위치를 통해 구성할 수는 있지만 합니다 [ `<compilation>` 요소](https://msdn.microsoft.com/library/s10awwz0.aspx) 에서 `Web.config`합니다. 명시적 컴파일을 사용 하 여 ASP.NET 응용 프로그램의 코드를 어셈블리로 컴파일하는 데 몇 가지 작업을 수행 해야 하 고 배포 하기 전에이 단계를 수행 합니다. 자동 컴파일을 사용 하 여 컴파일 프로세스 리소스에 처음 액세스할 때 웹 서버에서 발생 합니다.

사용 하면 어떤 컴파일 모델에 관계 없이, 모든 ASP.NET 페이지의 태그 부분 (의 `WebPage.aspx` 파일) 프로덕션 환경에 복사 해야 합니다. 명시적 컴파일을 사용 하 여 어셈블리를 복사 해야 합니다 `Bin` 폴더에 있지만 않아도 ASP.NET 페이지의 코드 부분을 복사 (의 `WebPage.aspx.cs` 파일). 자동 컴파일을 사용 하 여 코드 있는지, 그리고 해당 페이지를 방문 하는 경우 자동으로 컴파일할 수 있도록 코드 부분 파일을 복사 해야 합니다. 각 ASP.NET 웹 페이지의 태그 부분에 포함을 `@Page` 지시문에 명시적으로 이미 연결 된 코드 페이지의 컴파일된 여부 또는 자동으로 컴파일할 필요가 있는지 여부를 나타내는 특성입니다. 결과적으로, 프로덕션 환경 컴파일 모델 중 하나를 사용 하 여 원활 하 게 작업할 수 있으며 명시적 또는 자동 컴파일 사용 해야 함을 나타내기 위해 특수 한 구성 설정을 적용할 필요가 없습니다.

표 1에는 다른 파일을 자동 컴파일 및 명시적 컴파일을 사용 하는 경우 배포 요약 되어 있습니다. 컴파일에 관계 없이 모델 사용 하면 항상의 어셈블리를 배포 해야 합니다 `Bin` 폴더를 해당 폴더에 있는 경우. `Bin` 폴더 명시적 컴파일 모델을 사용 하는 경우 컴파일된 소스 코드를 포함 하는 웹 응용 프로그램에 특정 어셈블리를 포함 합니다. `Bin` 디렉터리도 다른 프로젝트에서 어셈블리 및 사용할 수 있습니다, 오픈 소스 또는 타사 어셈블리를 포함 하 고 이러한 프로덕션 서버에 배치 해야 해야 합니다. 따라서 일반으로 복사 합니다 `Bin` 배포 하는 경우 프로덕션 까지의 폴더입니다. (하지 않아도 자동 컴파일 모델을 사용 하 고 외부 어셈블리를 사용 하지 않는 경우는 `Bin` 확인 되는 디렉터리-!)

| **컴파일 모델** | **태그 부분 파일 배포** | **소스 코드 파일 배포** | **어셈블리를 배포 `Bin` 디렉터리?** |
| --- | --- | --- | --- |
| 명시적 컴파일 | 예 | 아니요 | 예 |
| 자동 컴파일 | 예 | 예 | 예 (있는 경우) |

**표 1:** 배포한 파일 사용 되는 컴파일 모델에 따라 달라 집니다.

## <a name="taking-a-trip-down-memory-lane"></a>여정 메모리 레인 축소를 수행합니다.

사용 되는 어떤 컴파일 방법에 따라 달라 집니다, 부분적으로 Visual Studio에서 ASP.NET 응용 프로그램 관리 하는 방법입니다. 이후 2000 년 있습니다의 NET의 처음 네 개의 서로 다른 버전의 Visual Studio-Visual Studio.NET 2002, Visual Studio.NET 2003, Visual Studio 2005 및 Visual Studio 2008 되었습니다. Visual Studio.NET 2002 및 2003 관리를 사용 하 여 ASP.NET 응용 프로그램을 *웹 응용 프로그램 프로젝트 모델*합니다. 웹 응용 프로그램 프로젝트 모델의 주요 기능은 다음과 같습니다.

- 프로젝트 구성을 단일 프로젝트 파일에 정의 되어 있는지 파일입니다. 프로젝트 파일에서 정의 되지 않은 모든 파일에는 Visual Studio에서 웹 응용 프로그램의 일부를 간주 되지 않습니다.
- 명시적 컴파일을 사용합니다. 에 배치 된 단일 어셈블리에 프로젝트 내에서 코드 파일을 컴파일하는 프로젝트를 빌드하는 `Bin` 폴더입니다.

Microsoft Visual Studio 2005 출시 하는 경우 웹 응용 프로그램 프로젝트 모델에 대 한 지원을 삭제 하며 웹 사이트 프로젝트 모델로 대체 되었습니다. 웹 사이트 프로젝트 모델로 구분 자체 웹 응용 프로그램 프로젝트 모델에서 다음과 같은 방법으로:

- 프로젝트의 파일을 제시 하는 단일 프로젝트 파일 대신 파일 시스템 대신 사용 됩니다. 즉, 웹 응용 프로그램 폴더 (또는 하위 폴더) 내의 모든 파일에는 프로젝트의 일부로 간주 됩니다.
- Visual Studio에서 프로젝트를 빌드할에서 어셈블리를 만들지 않습니다는 `Bin` 디렉터리입니다. 대신, 웹 사이트 프로젝트를 빌드할 컴파일 타임 오류를 보고 합니다.
- 자동 컴파일 지원 합니다. 코드 미리 컴파일된 (명시적 컴파일)을 사용할 수 있지만 웹 사이트 프로젝트는 일반적으로 프로덕션 환경에 태그 및 소스 코드를 복사 하 여 배포 됩니다.

Microsoft Visual Studio 2005 서비스 팩 1 릴리스되면 웹 응용 프로그램 프로젝트 모델을 다시 합니다. 그러나 Visual Web Developer만 웹 사이트 프로젝트 모델을 지원 하도록 계속 합니다. 좋은 소식은 Visual Web Developer 2008 서비스 팩 1을 사용 하 여이 제한 된 삭제 했음을 보여 줍니다. 현재 웹 응용 프로그램 프로젝트 모델 또는 웹 사이트 프로젝트 모델을 사용 하 여 Visual Studio (및 Visual Web Developer) ASP.NET 응용 프로그램을 만들 수 있습니다. 두 모델 경우 해당 장점 및 단점 가리킵니다 [웹 응용 프로그램 프로젝트 소개: 웹 사이트 프로젝트 비교 및 웹 응용 프로그램 프로젝트](https://msdn.microsoft.com/library/aa730880.aspx#wapp_topic5) 상황에 가장 적합 한 어떤 프로젝트 모델을 결정 하 고 두 모델의 비교 합니다.

## <a name="exploring-the-sample-web-application"></a>샘플 웹 응용 프로그램 탐색

이 자습서에 대 한 다운로드도 서 리뷰 라는 ASP.NET 응용 프로그램을 포함 합니다. 웹 사이트를 생성할 수 있습니다 취미 웹 사이트를 모방 책을 공유 하는 온라인 커뮤니티를 사용 하 여 검토 합니다. 이 ASP.NET 웹 응용 프로그램은 매우 간단 하며 다음 리소스를 구성 합니다.

- `Web.config`를 응용 프로그램의 구성 파일입니다.
- 마스터 페이지 (`Site.master`).
- 7 가지 다른 ASP.NET 페이지: 

    - ~`/Default.aspx`-사이트의 홈 페이지입니다.
    - ~`/About.aspx` -"의 사이트에 대 한" 페이지를 합니다.
    - ~`/Fiction/Default.aspx` -검토 했으므로 fiction 책 나열 된 페이지가 있습니다. 

        - ~`/Fiction/Blaze.aspx` -Richard Bachman novel 검토 *Blaze*합니다.
    - ~/`Tech/Default.aspx` -페이지를 검토 했으므로 관련 기술 서적을 나열 합니다. 

        - ~/`Tech/CYOW.aspx`-검토 *고유한 웹 사이트 만들기*합니다.
        - ~/`Tech/TYASP35.aspx` -검토 *가르치는 직접 ASP.NET 3.5 24 시간 동안에서*합니다.
- Styles 폴더에 3 개의 다른 CSS 파일을 선택 합니다.
- -ASP.NET 로고와 이미지의 세 가지 검토 책의 백그라운드에서 전원-모든 파일에 있는 이미지 4 개는 `Images` 폴더입니다.
- `Web.sitemap` 사이트 맵에서 정의 및 메뉴에 표시 되는 파일을 `Default.aspx` 루트 디렉터리에는 페이지 및 `Fiction` 및 `Tech` 폴더입니다.
- 라는 클래스 파일을 `BasePage.cs` 자료를 정의 하는 `Page` 클래스입니다. 이 클래스의 기능을 확장 합니다 `Page` 자동으로 설정 하 여 클래스를 `Title` 사이트 맵에 있는 페이지의 위치를 기준으로 속성입니다. 간단히 말해 모든 ASP.NET 코드 숨김 클래스를 확장 하는 `BasePage` (대신 `System.Web.UI.Page`) 제목을 사이트 맵에 해당 위치에 따라 값으로 설정 해야 합니다. 예를 들어 볼 때를 ~ /`Tech/CYOW.aspx` 페이지 제목을 "홈:: 기술:: 만들 사용자 고유의 웹 사이트"로 설정 됩니다.

그림 1에서는 브라우저를 통해 볼 때도 서 리뷰 웹 사이트의 스크린 샷을 보여 줍니다. 페이지를 참조 하는 여기 ~ /`Tech/TYASP35.aspx`, 책을 검토 하는 *가르치는 직접 ASP.NET 3.5 24 시간 동안에서*합니다. 페이지 맨 왼쪽된 열에서 메뉴에 걸쳐 있는 이동 경로에 정의 된 사이트 맵 구조에 기반한 `Web.sitemap`합니다. 오른쪽 위 모서리에서 이미지는 이미지에 있는 책 표지를 `Images` 폴더입니다. 웹 사이트의 모양과 느낌은 가장 중요 한 페이지 레이아웃 마스터 페이지에서 정의 되는 동안 Styles 폴더의 CSS 파일에 의해 명시 하는 스타일 시트 규칙 연계를 통해 정의 된 `Site.master`합니다.


[![서평 웹 사이트의 다양 한 제목 제공](determining-what-files-need-to-be-deployed-cs/_static/image2.png)](determining-what-files-need-to-be-deployed-cs/_static/image1.png)

**그림 1:** 서평 웹 사이트는 다양 한 제목에서의 검토를 제공 ([큰 이미지를 보려면 클릭](determining-what-files-need-to-be-deployed-cs/_static/image3.png))


이 응용 프로그램을 데이터베이스를 사용 하지 않습니다. 각 검토는 별도 웹 페이지 응용 프로그램에서으로 구현 됩니다. 이 자습서와 다음 몇 가지 자습서 데이터베이스 없는 웹 응용 프로그램 배포 안내 합니다. 그러나 이후 자습서에서이 응용 프로그램을 검토, 판독기 설명 및 기타 정보를 데이터베이스 내의 저장 향상 됩니다 하 고 데이터 기반 웹 응용 프로그램을 올바르게 배포 하기 위해 수행 해야 하는 단계를 살펴봅니다.

> [!NOTE]
> 이 자습서는 웹 호스트 공급자를 사용 하 여 ASP.NET 응용 프로그램 호스팅에 집중 하 고 ASP 같은 보조 항목을 탐색 하지는 않습니다. NET의 사이트 맵 시스템 또는 자료를 사용 하 여 `Page` 클래스입니다. 이러한 기술에 대 한 자세한 내용은 및 자습서 전체에서 포함 된 기타 항목에 대 한 자세한 배경은 각 자습서의 끝에 추가 정보 섹션을 참조 합니다.


이 자습서의이 다운로드는 웹 응용 프로그램의 두 복사본이, 다른 Visual Studio 프로젝트 형식으로 구현 하는 각: BookReviewsWAP, 웹 응용 프로그램 프로젝트 및 BookReviewsWSP, 웹 사이트 프로젝트입니다. 두 프로젝트는 Visual Web Developer 2008 SP1을 사용 하 여 만든 및 ASP.NET 3.5 SP1을 사용 합니다. 사용 하려면 이러한 프로젝트의 압축을 풀어 내용을 바탕으로 시작 합니다. 웹 응용 프로그램 프로젝트 (BookReviewsWAP)을 열고, BookReviewsWAP 폴더로 이동한 후 솔루션 파일을 두 번 `BookReviewsWAP.sln`합니다. (BookReviewsWSP) 웹 사이트 프로젝트를 열려면 Visual Studio를 시작 하 고 그런 다음 파일 메뉴에서 웹 사이트 열기 옵션을 선택, 이동 하는 `BookReviewsWSP` 바탕 화면에서 폴더 확인을 클릭 합니다.


파일 확인이 자습서의 나머지 두 섹션에서는 응용 프로그램을 배포 하는 경우 프로덕션 환경에 복사 해야 합니다. 다음 두 자습서- *[Your 사이트를 사용 하 여 FTP 배포](deploying-your-site-using-an-ftp-client-cs.md)* 하 고 *[배포 사이트를 사용 하 여 Visual Studio](deploying-your-site-using-visual-studio-cs.md)* -다양 한 방법 표시 웹 호스트 공급자에 이러한 파일을 복사 합니다.

## <a name="determining-the-files-to-deploy-for-the-web-application-project"></a>웹 응용 프로그램 프로젝트 배포 파일 확인

웹 응용 프로그램 프로젝트 모델 명시적 컴파일을 사용-프로젝트의 소스 코드를 응용 프로그램을 빌드할 때마다 단일 어셈블리로 컴파일됩니다. ASP.NET 페이지의 코드 숨김 파일을 포함 하는이 컴파일 (~ /`Default.aspx.cs`, ~ /`About.aspx.cs`등), 뿐만 `BasePage.cs` 클래스입니다. 결과 어셈블리 BookReviewsWAP.dll 이름은 및 응용 프로그램에 위치한 `Bin` 디렉터리입니다.

그림 2에서는 책 검토 웹 응용 프로그램 프로젝트를 구성 하는 파일을 보여 줍니다.


[![솔루션 탐색기에서 웹 응용 프로그램 프로젝트를 구성 하는 파일 나열](determining-what-files-need-to-be-deployed-cs/_static/image5.png)](determining-what-files-need-to-be-deployed-cs/_static/image4.png)

**그림 2**: 솔루션 탐색기를 웹 응용 프로그램 프로젝트를 구성 하는 파일 나열


웹 응용 프로그램 프로젝트 모델 시작을 사용 하 여 명시적으로 가장 최근 원본 코드를 어셈블리로 컴파일할 응용 프로그램을 작성 하 여 개발 하는 ASP.NET 응용 프로그램을 배포 합니다. 다음으로, 프로덕션 환경에는 다음 파일을 복사 합니다.

- 모든 ASP.NET에 대 한 선언적 태그를 포함 하는 파일 페이지와 같은 ~ /`Default.aspx`, ~ /`About.aspx`등입니다. 또한 복사본 사용 하 여 모든 사용자 컨트롤과 마스터 페이지에 대 한 선언적 태그 구성입니다.
- 어셈블리 (`.dll` 파일)에 `Bin` 폴더입니다. 프로그램 데이터베이스 파일을 복사할 필요가 없습니다 (`.pdb`) 또는 XML 파일에서 찾을 수는 `Bin` 디렉터리입니다.

프로덕션 환경에 ASP.NET 페이지의 소스 코드 파일을 복사할 필요가 없습니다도 복사 해야 합니다 `BasePage.cs` 클래스 파일입니다.

> [!NOTE]
> 그림 2에서 볼 수 있듯이 합니다 `BasePage` 라는 폴더에 배치 하는 프로젝트에 클래스 파일로 클래스는 구현 `HelperClasses`합니다. 프로젝트를 컴파일할 때의 코드를 `BasePage.cs` 파일은 단일 어셈블리로 ASP.NET 페이지의 코드 숨김 클래스와 함께 컴파일됩니다 `BookReviewsWAP.dll.` ASP.NET에는 특수 폴더 `App_Code` 웹에 대 한 클래스 파일을 저장 하도록 디자인 된 사이트 프로젝트입니다. 코드는 `App_Code` 폴더는 자동으로 컴파일되고 따라서 해서는 안 웹 응용 프로그램 프로젝트를 사용 하 여 합니다. 일반 폴더에 응용 프로그램의 클래스 파일을 배치 해야 대신 `HelperClasses`, 또는 `Classes`, 또는 이와 유사한 합니다. 또는 별도 클래스 라이브러리 프로젝트에서 클래스 파일을 배치할 수 있습니다.


ASP.NET 관련 태그 파일 및 어셈블리를 복사 하는 것 외에도 합니다 `Bin` 폴더를 해야-이미지 및 CSS 파일-클라이언트 쪽 지원 파일 뿐만 아니라 다른 서버 쪽 지원 파일을 복사할 `Web.config` 및 `Web.sitemap`합니다. 이러한 클라이언트 및 서버 쪽 지원 파일을 명시적 또는 자동 컴파일을 사용 하는지 여부에 관계 없이 프로덕션 환경에 복사 해야 합니다.

## <a name="determining-the-files-to-deploy-for-the-web-site-project-files"></a>파일을 웹 사이트 프로젝트 파일에 대 한 배포를 확인 합니다.

웹 사이트 프로젝트 모델로 자동 컴파일, 웹 응용 프로그램 프로젝트 모델을 사용 하는 경우 사용할 수 없는 기능을 지원 합니다. 명시적 컴파일을 사용 하 여 프로젝트의 소스 코드를 어셈블리로 컴파일할 하며 프로덕션 환경에 해당 어셈블리를 복사 합니다. 반면, 자동 컴파일을 사용 하 여 단순히 복사할 소스 코드를 프로덕션 환경 및 필요에 따라 요청 시 런타임에 의해 컴파일됩니다.

Visual Studio에서 빌드 메뉴 옵션은 웹 응용 프로그램 프로젝트와 웹 사이트 프로젝트 모두에 있습니다. 프로젝트의 소스 코드에 있는 단일 어셈블리로 컴파일하고 웹 응용 프로그램 프로젝트를 빌드하는 `Bin` 디렉터리; 빌드 웹 사이트 프로젝트를 컴파일 타임 오류를 확인 하지만 모든 어셈블리를 만들지 않습니다. 해야 할 웹 사이트 프로젝트 모델로 모든를 사용 하 여 개발 하는 ASP.NET 응용 프로그램을 배포 하려면 복사본 프로덕션 환경에 적절 한 파일 이지만 확인해보시기 바랍니다 첫 번째 빌드에 프로젝트를 컴파일 시간 오류가 없는지 확인 합니다.

그림 3에서는 책 검토 웹 사이트 프로젝트를 구성 하는 파일을 보여 줍니다.


 [![웹 사이트 프로젝트를 구성 하는 파일을 나열 하는 솔루션 탐색기](determining-what-files-need-to-be-deployed-cs/_static/image7.png)](determining-what-files-need-to-be-deployed-cs/_static/image6.png) 

**그림 3**: 솔루션 탐색기를 웹 사이트 프로젝트를 구성 하는 파일 나열


웹 사이트 프로젝트를 배포 된 코드 파일과 함께 ASP.NET 페이지, 마스터 페이지 및 사용자 정의 컨트롤에 대 한 태그 페이지를 포함 하는 프로덕션 환경-복사할 ASP.NET 관련 파일을 모두 포함 됩니다. BasePage.cs 등의 모든 클래스 파일을 복사 해야 합니다. `BasePage.cs` 파일에는 `App_Code` 폴더인 특수 ASP.NET 웹 사이트 프로젝트에서 클래스 파일에 대해 사용 되는 폴더입니다. 특수 폴더에 있는 클래스 파일을 프로덕션에도 만들 수 해야 합니다 `App_Code` 개발 환경에서 폴더에 복사 해야는 `App_Code` 프로덕션 폴더입니다.

ASP.NET 태그와 소스 코드 파일에 복사 하는 것 외에도 해야-이미지 및 CSS 파일-클라이언트 쪽 지원 파일 뿐만 아니라 다른 서버 쪽 지원 파일을 복사할 `Web.config` 고 `Web.sitemap`입니다.

> [!NOTE]
> 웹 사이트 프로젝트에는 명시적 컴파일을 사용할 수도 있습니다. 이후 자습서에서는 명시적으로 웹 사이트 프로젝트를 컴파일하는 방법을 검사 합니다.


## <a name="summary"></a>요약

ASP.NET 응용 프로그램 개발 환경에서 프로덕션 환경에 필요한 파일을 복사 하는 작업을 수반 합니다. 정확한 파일 집합에는 동기화 해야 하는 여부를 ASP.NET 응용 프로그램의 코드를 명시적으로 또는 자동으로 컴파일할에 따라 달라 집니다. 채택 컴파일 전략은 영향을 Visual Studio 구성 되어 있는지 여부는 웹 응용 프로그램 프로젝트 모델 또는 웹 사이트 프로젝트 모델을 사용 하 여 ASP.NET 응용 프로그램 관리.

웹 응용 프로그램 프로젝트 모델 명시적 컴파일을 사용 하 여 및에서 단일 어셈블리를 프로젝트의 코드를 컴파일하는 `Bin` 폴더입니다. 응용 프로그램, ASP.NET 페이지의 태그 부분과의 콘텐츠를 배포 하는 경우는 `Bin` 폴더 프로덕션 환경으로 푸시됩니다 해야;-코드 파일 및 코드 숨김 클래스, 예를 들어-응용 프로그램의 소스 코드 필요는 없습니다 프로덕션 환경에 복사 합니다.

웹 사이트 프로젝트 모델로 자습서 나중에 확인할 수 있듯이 명시적으로 웹 사이트 프로젝트를 컴파일할 수 있지만 기본적으로 자동 컴파일을 사용 합니다. 자동 컴파일을 사용 하는 ASP.NET 응용 프로그램을 배포 하려면 태그 부분 *고* 소스 코드를 프로덕션 환경에 복사 해야 합니다. 처음으로 요청 될 때 프로덕션 환경에서 코드를 자동으로 컴파일됩니다.

이제 개발 및 프로덕션 환경 간의 동기화 해야 하는 파일을 살펴보았습니다 한다고 웹 호스트 공급자도 서 리뷰 응용 프로그램 배포를 준비 합니다.

즐거운 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET 컴파일 개요](https://msdn.microsoft.com/library/ms178466.aspx)
- [ASP.NET 사용자 컨트롤](https://msdn.microsoft.com/library/y6wb1a0e.aspx)
- [ASP를 검사 합니다. NET의 사이트 탐색](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)
- [웹 응용 프로그램 프로젝트 소개](https://msdn.microsoft.com/library/aa730880.aspx)
- [마스터 페이지 자습서](../master-pages/creating-a-site-wide-layout-using-master-pages-cs.md)
- [페이지 간 코드 공유](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/pages/code.aspx)
- [ASP.NET 페이지의 코드 숨김 클래스에 대 한 사용자 지정 기본 클래스를 사용 하 여](http://aspnet.4guysfromrolla.com/articles/041305-1.aspx)
- [Visual Studio 2005의 웹 사이트 프로젝트 시스템: 것 이란 무엇 이며 왜 않았습니다 것?](https://weblogs.asp.net/scottgu/archive/2005/08/21/423201.aspx)
- [연습: Visual Studio에서 웹 응용 프로그램 프로젝트에 웹 사이트 프로젝트를 변환](https://msdn.microsoft.com/library/aa983476.aspx)

> [!div class="step-by-step"]
> [이전](asp-net-hosting-options-cs.md)
> [다음](deploying-your-site-using-an-ftp-client-cs.md)
