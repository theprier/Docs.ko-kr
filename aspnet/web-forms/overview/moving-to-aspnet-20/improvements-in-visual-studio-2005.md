---
uid: web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
title: Visual Studio 2005의 개선 사항 | Microsoft Docs
author: microsoft
description: Visual Studio 2005 웹 응용 프로그램 개발자에 향상 된 기능 및 향상 된 웹 프로젝트에 긴 목록 제공합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2005
ms.topic: article
ms.assetid: 72d90cd0-b3d9-454c-b2eb-ed0d9812f32c
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
msc.type: authoredcontent
ms.openlocfilehash: aafc59980e807677d6023110d324365ce92bb5fc
ms.sourcegitcommit: d8aa1d314891e981460b5e5c912afb730adbb3ad
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/05/2018
ms.locfileid: "28987992"
---
<a name="improvements-in-visual-studio-2005"></a>Visual Studio 2005의 향상 된 기능
====================
by [Microsoft](https://github.com/microsoft)

> Visual Studio 2005 웹 응용 프로그램 개발자에 향상 된 기능 및 향상 된 웹 프로젝트에 긴 목록 제공합니다.


Visual Studio 2005 웹 응용 프로그램 개발자에 향상 된 기능 및 향상 된 웹 프로젝트에 긴 목록 제공합니다. 강력 하지만 Visual Studio.NET 2002 및 2003은, 많은 불만 사항에에서 있었습니다 웹 프로젝트 된 처리 하는 방식. Visual Studio 2005 이러한 불만 사항 해결 하는 데 많은 새 기능을 추가 합니다. Visual Studio.NET 2003 웹 응용 프로그램의 컴파일을 처리 하는 방식을 선호 하는, 참조 [웹 응용 프로그램 프로젝트](https://go.microsoft.com/fwlink/?LinkId=57870)합니다.

이 모듈에서는 잘 웹 프로젝트 생성, 관리 및 개발의 향상 된 기능을 다룹니다. 이후 단원에서 웹 프로젝트를 빌드하고 배포 하기의 개선 사항도 다룹니다.

## <a name="frontpage-server-extensions"></a>FrontPage Server Extensions

Visual Studio.NET 2002 및 2003 FrontPage Server Extensions 상자에서 만들거나 웹 프로젝트를 작성 하기 위해 필요 합니다. 개발자는 두 가지 서로 다른 액세스 모드 (FrontPage Server Extensions 또는 파일 액세스 모드) 사이 선택을, 모두 FrontPage Server Extensions IIS 등의 응용 프로그램 루트를 설정 하는 등 작업을 수행 하는 데 사용 합니다.

Visual Studio 2005 로컬 프로젝트에 대 한 범주에 대 한 의존도 제거합니다. Visual Studio 2005는 이제 IIS 메타 베이스 FrontPage Server Extensions를 사용 하는 대신 직접 액세스 합니다. Visual Studio 2005는 또한 FrontPage Server Extensions를 요구 하지 않고 원격 프로젝트 액세스를 허용 하는 FTP에 대 한 지원을 추가 합니다.

해당 프로젝트에서 FrontPage Server Extensions를 사용 하려는 개발자는 옵션은 계속 사용할 수입니다. 그러나 강력한 ASP.NET 개발자 커뮤니티 피드백에 따라는 없습니다.

> [!NOTE]
> FrontPage Server Extensions가 원격 프로젝트 만들기, 열기 등 여전히 필요 합니다.


## <a name="aspnet-development-server"></a>ASP.NET Development Server

Visual Studio 2005 ASP.NET 개발 서버를 호출 하는 새 웹 서버와 함께 제공 됩니다. (이 웹 서버를 이전에 Cassini.)

ASP.NET Development Server의 다양 한 이점이 있습니다.

- 관리자가 아닌 사용자도 개발 하 고 웹 서버 디버깅에 대 한 가능한 되었습니다.
- ASP.NET 개발 서버는 동적으로 유연한 프로젝트 위치에 대 한 허용 하는 파일 시스템의 모든 위치에 가상 디렉터리를 매핑합니다.
- Windows XP Professional에 IIS를 이미 사용 중인 사용자는 이제 IIS에서 기본 웹 사이트의 파일 또는 폴더 구조에 영향을 주지 않는 새 웹 응용 프로그램을 만들 수 있습니다.

ASP.NET 개발 서버를 활용 하기 위해 특별 한 구성이 필요 합니다. 파일 시스템에서 호스팅되는 웹 프로젝트를 디버깅 하거나 검색할 때 Visual Studio 2005는 임의의 포트에서 요청 서비스에서 ASP.NET 개발 서버 인스턴스의 자동 시작 됩니다.

이 모듈의 뒷부분에 나오는 ASP.NET 개발 서버에서 자세한 정보를 설명 합니다.

## <a name="improved-file-management"></a>향상 된 파일 관리

Visual Studio 2002 및 2003에서 프로젝트 파일 (VB.NET에 대 한.vbproj) 및 C#에 대 한.csproj 웹 응용 프로그램의 모든 파일에 정보를 저장 합니다. 솔루션 탐색기 표시 프로젝트 파일의 파일 정보를 기반으로 합니다. 이 인해 솔루션 탐색기 외부 편집기 사용 된 경우에 종종 잘못 된 정보가 표시 됩니다. Visual Studio 2002 및 2003은 종종 파일 변경 내용을 덮어쓰거나 파일의 최신 버전을 표시 하지.

Visual Studio 2005에서는 프로젝트 파일입니다. 대신, 파일 및 폴더 정보는 정확 하 게 프로젝트의 파일 표시에 디스크에서 읽습니다. Visual Studio 2002 및 2003의 참조 폴더는 웹 응용 프로그램에서 실제 폴더를 나타내지 않습니다 때문에 Visual Studio 2005 솔루션 탐색기에서 References 폴더를도 제거 합니다. Visual Studio 2005에서 프로젝트에 대 한 참조에 액세스 하려면 프로젝트에 대 한 속성 페이지를 사용 해야 합니다.

## <a name="creating-web-projects"></a>웹 프로젝트 만들기

웹 개발자가 Visual Studio 2005에서 프로젝트를 만드는 데 사용할 수 있는 여러 가지 새로운 옵션 있어야 합니다. 웹 사이트는 파일 시스템에서 아무 곳 이나 지금 만들 수 있습니다 및 다음 디버깅할 수 있습니다 또는 새 ASP.NET 개발 서버를 사용 하 여 찾아볼 합니다. 개발자는 FTP를 사용 하 여 새 웹 사이트를 만들 수도 수 있습니다.

Visual Studio 2005에서 웹 프로젝트를 만드는 연습 동영상을 보려면 여기를 클릭 합니다.


![](improvements-in-visual-studio-2005/_static/image1.png)


[전체 화면 비디오 열기](improvements-in-visual-studio-2005/_static/creating_projects1.wmv)


### <a name="file-system-projects"></a>파일 시스템 프로젝트

동영상 연습에서 살펴본 것 처럼 또는 로컬 컴퓨터에서 파일 공유를 통해 원격 위치에서 파일 시스템에 웹 사이트를 만들 수도 있습니다. 파일 시스템에서 생성 된 웹 사이트를 찾는 및 ASP.NET 개발 서버를 사용 하 여 디버깅 합니다.

> [!NOTE]
> ASP.NET 개발 서버는 고객에 대 한 일부 혼란이 발생할 수 있습니다. 웹 프로젝트를 IISs 디렉터리 구조 (예: c: / inetpub/wwwroot)에 파일 시스템에 생성 하는 경우 웹 사이트 여전히 Visual Studio 2005 내에서 시작 하는 경우 ASP.NET 개발 서버를 통해 검색할 수 있습니다. 따라서 모든 IIS 구성 (즉, 인증 방법) 적용 되지 않습니다.


기본 웹 프로젝트도 많이 제거 하 여 오버 헤드와 같이 Default.aspx 페이지, default.cs 파일 및 응용 프로그램/_Data 폴더 포함 됩니다. Web.config 및 특수 폴더 (예: 응용 프로그램/_code)는 필요에 따라 추가 됩니다. 웹 프로젝트 파일 및 필요한 폴더에만 포함 됩니다.

### <a name="http-projects"></a>HTTP 프로젝트

HTTP 프로젝트 원격 웹 사이트 또는 로컬 IIS 웹 사이트에서 만들어진 프로젝트에 수 있습니다. 기본 프로젝트 위치는 `http://localhost`합니다. 찾아보기 단추를 누르면 방법은 두 가지 HTTP: 로컬 IIS 및 원격 사이트입니다. 이러한 두 옵션의 주요 차이점은 웹 사이트 정보 파일이 웹 서버에 복사 되는 방법 및 위치 선택 대화 상자에서 표시 되는 메서드.

로컬 IIS 옵션 로컬 컴퓨터에서 메타 베이스에서 사이트 정보를 읽고 및 파일 시스템을 사용 하 여 파일이 복사 됩니다. 원격 사이트 옵션 FrontPage Server Extensions 이름과 사이트 정보를 사용 하 고 HTTP를 사용 하 여 파일은 복사 하 고 FrontPage Server Extensions RPC 호출 합니다.

> [!NOTE]
> Get/_aspx/_ver.aspx 있고 vs###/_tmp.htm 파일 버전 정보를 확인 하려면 더 이상 사용 됩니다.


기본 HTTP 방법은 로컬 IIS입니다. 이 옵션을 사용할 수 있는 사이트를 확인 하려면 IIS 메타 베이스 및 콘텐츠 생성 될 위치 읽습니다. 트리 뷰에서 선택 하 여 다른 폴더 또는 가상 디렉터리를 선택할 수 있습니다. 있습니다 수도 새 가상 디렉터리 만들기, 폴더, 응용 프로그램으로 표시으로이 대화 상자에서 기존 가상 디렉터리를 삭제 합니다.


![위치 대화 상자를 선택 합니다.](improvements-in-visual-studio-2005/_static/image1.gif)

**그림 1**:는 위치 대화 상자를 선택 합니다.


와 달리 이전 버전의 Visual Studio를 선택 하는 경우에 **Secure Sockets Layer** 경우 요청 하는 보안 경고 대화 상자가 표시 됩니다, 확인란을 선택 하 고 SSL 인증서를 찾는 URL을 일치 하지 않습니다 계속 하려고 합니다. Visual Studio.NET 2003을 사용 하 여 사용 된 인증서 나와 일치 하는 경우, 프로젝트 만들기 실패 합니다.


![보안 경고에 대 한 SSL 인증서](improvements-in-visual-studio-2005/_static/image2.gif)

**그림 2**: SSL 인증서에 대 한 보안 경고


### <a name="note-on-host-headers"></a>호스트 헤더에 대 한 참고

특정 IP에 바인딩된 사이트에서 웹 응용 프로그램을 만드는 경우에 호스트 헤더 구성 되어 있는지 확인 해야 합니다. 그렇지 않으면 Visual Studio에서 사이트 만듭니다 `http://localhost`, 하지만 사이트는를 탐색 하거나 IDE 내에서 디버깅 하는 경우 IP 주소가 올바르게 확인 되지 것입니다.

원격 사이트 옵션을 선택 하면 대화 상자를 새 웹 사이트에 대 한 대상 URL을 입력할 수로 변경 됩니다. 이 URL에 FrontPage Server Extensions 사용 하도록 설정 하는 서버에 있어야 합니다. FrontPage Server Extensions를 사용 하 여 로컬 웹 서버와 함께 작업 하려는 경우 원격 사이트 옵션을 사용할 수 있으며 로컬 URL을 지정.


![원격 서버에 웹 사이트 만들기](improvements-in-visual-studio-2005/_static/image1.jpg)

**그림 3**: 원격 서버에 웹 사이트 만들기


를 만들 때 응용 프로그램 SSL 통해 원격 사이트에 SSL 인증서와 일치 하지 않으면 확인 대화 상자에서 로컬 IIS 옵션을 사용 하는 경우 표시 대화 상자 보다 약간 차이가 있습니다.


![원격 사이트 보안 경고](improvements-in-visual-studio-2005/_static/image3.gif)

**그림 4**: 원격 사이트 보안 경고


<a id="_Toc116100243"></a>

#### <a name="ftp"></a>FTP

Visual Studio 2005에서는 FTP 통해 웹 사이트를 만드는 옵션을 제공 합니다. 이 옵션을 사용 하면 IDE는 사용자가 임시 폴더에 파일을 로컬로 만듭니다 하 고 FTP를 사용 하 여 FTP 위치에 파일을 이동 합니다.

> [!NOTE]
> 임시 폴더 위치가 c: / Documents and Settings /&lt;사용자&gt;로컬/설정/Temp/VWDWebCache/&lt;서버&gt;/_&lt;응용 프로그램 이름&gt;


FTP 옵션을 사용할 경우 위치 선택 대화 상자가 나타납니다. 아래와 같이이 대화 상자에 필요한 FTP 연결 정보를 입력 합니다.


![FTP에 대 한 위치 대화 상자를 선택 합니다.](improvements-in-visual-studio-2005/_static/image2.jpg)

**그림 5**:는 FTP에 대 한 위치 대화 상자를 선택 합니다.


## <a name="lab-setup-ftp-site-and-create-a-project"></a>랩: 설정 FTP 사이트 및 프로젝트 만들기

다음 단계는 사용자만은 FTP를 통해를 업로드할 수 있는 위치에 있도록 FTP 사이트를 구성 합니다.

### <a name="install-the-ftp-service"></a>FTP 서비스를 설치 합니다.

1. 프로그램 추가 / 제거를 열고, Windows 구성 요소 추가/제거를 선택 합니다.
2. 인터넷 정보 서비스 (Windows 2003에서 응용 프로그램 서버)를 선택 하 고 클릭 **세부 정보**합니다.
3. 확인 **파일 전송 프로토콜 (FTP) 서비스** 클릭 **확인**합니다.
4. 클릭 **다음** FTP 서비스를 설치 합니다.

### <a name="create-a-new-folder-for-content"></a>콘텐츠에 대 한 새 폴더 만들기

1. Windows 탐색기에서 라는 새 폴더를 만들 **User1** c: / inetpub/wwwroot 안에 있습니다.

#### <a name="configure-folders-and-permissions-on-folders"></a>폴더에서 폴더와 사용 권한을 구성 합니다.

1. 관리 도구에서 인터넷 정보 서비스 스냅인을 엽니다. 지금 컴퓨터 이름은 노드 아래에 FTP 사이트 폴더를 갖게 됩니다.
2. 확장 **FTP 사이트**합니다.
3. 마우스 오른쪽 단추로 클릭는 **기본 FTP 사이트**선택, **새로**, 다음 **가상 디렉터리**, 클릭 **다음**합니다.
4. 입력 **User1** 가상 디렉터리 이름과 클릭에 대 한 **다음**합니다.
5. 입력 **c: / inetpub/wwwroot/User1** 경로 클릭에 대 한 **다음**합니다.
6. 클릭 **다음** 차례로 **마침** 마법사를 완료 합니다.
7. 마우스 오른쪽 단추로 클릭는 **User1** 선택한 기본 FTP 사이트 가상 디렉터리 **속성**합니다.
8. 확인의 **쓰기** 확인란을 클릭 하 고 **확인** 는 대화 상자를 닫습니다.
9. 마우스 오른쪽 단추로 클릭 **기본 FTP 사이트** 선택 **속성**합니다.
10. 에 **보안 계정** 탭을 선택 취소 **익명 연결 허용**합니다.
11. 클릭 **예** 계속할 것인지 묻는 대화 상자.
12. 클릭 **확인** 는 대화 상자를 닫습니다.
13. 확장 된 **기본 웹 사이트** 아래는 **웹 사이트** 노드.
14. 마우스 오른쪽 단추로 클릭는 **User1** 디렉터리 및 선택 **속성**
15. 에 **응용 프로그램 설정** 섹션에서 클릭 **만들기** 응용 프로그램으로 폴더를 표시 합니다.
16. 클릭 **확인** 는 대화 상자를 닫습니다.
17. 인터넷 정보 서비스 스냅인을 닫습니다.

### <a name="create-web-project"></a>웹 프로젝트 만들기

1. Visual Studio 2005를 엽니다.
2. **파일** 메뉴 선택 **새 웹 사이트**합니다.
3. 에 **위치** 드롭다운 **FTP**합니다.
4. **찾아보기**를 클릭합니다.
5. 입력 **localhost** 에 **서버** 텍스트 상자에 붙여넣습니다.
6. 입력 **User1** 디렉터리 텍스트 상자에 있습니다.
7. 클릭 **열려**합니다. FTP 위치는 새 웹 사이트 대화 상자에 입력 됩니다.
8. **확인**을 클릭합니다.
9. 선택을 취소 **익명 로그온** FTP 로그온 대화 상자에서 자격 증명을 입력 하 고 클릭 **확인**합니다.
10. 프로젝트에 대 한 URL은 무엇입니까? (프로젝트에 대 한 URL은 솔루션 탐색기 나타납니다.)
11. **빌드** 메뉴 선택 **웹 사이트 빌드** 또는 **솔루션 빌드**합니다.
12. 솔루션 탐색기에서 Default.aspx를 마우스 오른쪽 단추로 클릭 하 고 선택 **브라우저에서 보기**합니다.
13. 웹 사이트 URL 필요 대화 상자에 입력 `http://localhost/user1` URL 및 클릭 **확인**합니다.

> [!NOTE]
> 형식 /_Default 로드할 수 없음을 나타내는 오류가 발생할 경우 ASP.NET 2.0를 웹 사이트와 이전 버전에서 실행 되 고 있는지 확인 합니다. 인터넷 정보 서비스에서 ASP.NET 탭에서 시작할 수 있습니다.


## <a name="opening-web-projects"></a>웹 프로젝트 열기

웹 프로젝트를 열면 프로젝트 만들기와 비슷합니다. 다음 섹션에서는 관심을 기울 아웃에 대 한 IDE 내에서 작업 하는 동안 영역을 호출 합니다. 또한 HTTP 및 FTP를 사용 하 여 웹 프로젝트를 사용한 작업에 대해서도 설명 합니다.

웹 프로젝트를 열려면 파일 메뉴에서 웹 사이트 열기를 선택 합니다. 이전에 대상 동일한 위치 선택 대화 상자와 라는 메시지가 되 고 같은 네 가지 옵션을 사용할 수 있는: 파일 시스템, 로컬 IIS, FTP 및 원격 사이트입니다.

<a id="_Toc116100245"></a>

## <a name="file-system"></a>파일 시스템

앞에서 설명한 대로이 단원에서는 Visual Studio는 더 이상 프로젝트 파일을 사용 합니다. 따라서 파일 시스템에서 웹 사이트를 열려고 하면 실제로 옵션이 있습니다 선택한 폴더는 웹 프로젝트를 Visual Studio에서 처음으로 만들어지지 않은 경우에 원하는 모든 폴더를 선택 합니다. 예를 들어 웹 사이트와 내 문서 폴더를 열지 선택할 수 있으며 Visual Studio는 기꺼이 열고 아래와 같이 파일을 표시 합니다.


![웹 사이트로 열린 내 문서](improvements-in-visual-studio-2005/_static/image3.jpg)

**그림 6**: *내 문서* 웹 사이트로 열


Visual Studio만을 만들기 때문에 필요한 경우 추가 파일 및 폴더에 추가 파일이 나 폴더가 없기 열 위치에 추가 됩니다. 이 아키텍처의 부작용을 파일 시스템에 웹 사이트를 중첩에서 하지 있습니다. 예를 들어 다음과 같은 디렉터리 구조를 것이 좋습니다.

에 c: / 입력 하면 MyWebSite 웹 프로젝트

C: / 입력 하면 MyWebSite/Nested에 다른 웹 프로젝트

c: / 입력 하면 MyWebSite 웹 사이트를 열 때 중첩 된 폴더는 해당 응용 프로그램의 하위 폴더로 표시 됩니다.

<a id="_Toc116100246"></a>

## <a name="http"></a>HTTP

IIS 메타 베이스 (로컬 IIS) 또는 FrontPage Server Extensions (원격 사이트)를 사용 하 여 설정은 읽어 HTTP 통해 웹 사이트를 열 때 중첩 된 웹 응용 프로그램에 있는 경우 응용 프로그램으로 식별 하는 아이콘으로도 표시 됩니다 이러한. Frontpage에서 웹 응용 프로그램으로 작업에 익숙한 Visual Studio 2005에서의 동작과가 비슷합니다.

Visual Studio IDE 내에서 현재 열려 있는 응용 프로그램 아래에 중첩 된 응용 프로그램에 대 한 아이콘이 표시 되는 경우에 것은 허용 되지 않습니다 확장할 자신의 콘텐츠를 볼 수 있습니다. 그러나 열에 두 번 클릭 수 있습니다. 이렇게 하면 웹 응용 프로그램을 엽니다 (또는 현재 열려 있는 솔루션을 바꾸기) 묻는 대화 상자가 나타납니다 또는 현재 솔루션에 웹 응용 프로그램을 추가 합니다.


![중첩 된 응용 프로그램 아이콘을 두 번 클릭 하면이 대화 상자 표시](improvements-in-visual-studio-2005/_static/image4.jpg)

**그림 7**: 중첩 된 응용 프로그램 아이콘을 두 번 클릭 하면이 대화 상자 표시


<a id="_Toc116100247"></a>

## <a name="ftp-site"></a>FTP 사이트

FTP 통해 사이트를 열 때 파일은 모두 로컬로 복사 임시 폴더에 있습니다. 로컬 저장소 위치에 대 한 전체 경로 프로젝트에 대 한 속성 창에 표시 되 고 다음 형식을 사용 하 여 만들어집니다.

C: / Documents and Settings /&lt;사용자&gt;로컬/설정/Temp/VWDWebCache/&lt;서버&gt;/_&lt;응용 프로그램 이름&gt;

FTP를 사용 하면 Visual Studio를 아래와 같이 찾아볼 수 있도록 프로젝트에 대 한 기본 URL을 지정 해야 합니다. 기본 URL을 지정 하지 않으면 Visual Studio 라는 나타납니다에 대 한 웹 사이트의 페이지를 탐색 하려고 처음으로 합니다.


![FTP 사이트에 대 한 기본 URL을 지정](improvements-in-visual-studio-2005/_static/image5.jpg)

**그림 8**: FTP 사이트에 대 한 기본 URL 지정


## <a name="improvements-in-compilation"></a>컴파일의 향상 된 기능

작업에서 Visual Studio 2005 웹 응용 프로그램을 이전 버전 보다 훨씬 빠릅니다. 이 수는 없는 일부만 컴파일 아키텍처의 변경 내용에 있습니다.

Visual Studio 2002 및 2003에서 웹 응용 프로그램으로 /bin 폴더에 있는 하나의 주 어셈블리로 컴파일 되었습니다. Visual Studio 2005에서 응용 프로그램/_Code 폴더 추가 되었습니다. 클래스 및 기타 UI가 아닌 코드는 응용 프로그램/_Code 폴더에 추가 됩니다. Visual Studio에서 프로젝트를 빌드할 때 응용 프로그램/_Code 폴더의 모든 파일은 단일 App/_Code.dll 파일로 컴파일됩니다. 이러한 변경의 결과 후속 빌드는 이전 버전 보다 훨씬 빠릅니다.

> [!NOTE]
> ASP.NET 웹 응용 프로그램을 빌드하 MSBuild 명령줄 유틸리티를 사용할 수도 있습니다. 모듈 9에에서 해당 도구를 설명 합니다.


다른 컴파일 향상 된 빌드 메뉴에서 새 빌드 페이지 옵션입니다. 이 기능을 사용 하면 개발자가 변경 내용을 보다 신속 하 게 컴파일될 수 있도록 현재 페이지만 (함께, 시의 종속성)를 다시 작성 합니다. C# IntelliSense 등을 업데이트 하기 위해에 대 한 백그라운드 컴파일을 제공 하지 않으므로, 유익한 지 보내주신이 기능에서 intellisense가 단순히 단일 페이지를 다시 작성 하 여 신속 하 게 업데이트할 수 있습니다.

프로젝트에 대 한 빌드 속성을 사용 하 여 빌드 시작 페이지가 실행 되기 전에 발생 하는 형식을 구성할 수 있습니다. 개발자는 Visual Studio 코드 변경 후 응용 프로그램을 보다 신속 하 게 디버깅을 시작할 수 있도록만 빌드 현재 페이지를 선택할 수 있습니다.


![빌드 페이지 시작 작업](improvements-in-visual-studio-2005/_static/image6.jpg)

**그림 9**: 빌드 페이지 시작 작업


Visual Studio 및 ASP.NET 아키텍처에 향상 된 또 다른 훌륭한 기능 편집 영역에 있으며 계속 됩니다. Visual Studio 2005에서 개발자가 프로젝트 디버깅을 시작 디버거를 분리 하지 않고 프로젝트에서 코드 변경 내용을 확인 합니다. 사실, 새 클래스를 추가 하는 프로젝트 디버깅을 시작할 문자 그대로 수, 해당 클래스에 코드를 추가, 해당 클래스의 새 인스턴스를 만드는 사용자 페이지에 코드를 추가 및 디버거를 분리 하지 않고 모든 클래스의 메서드를 실행 합니다. 새 코드를 실행 하는 것은 말 그대로 브라우저 새로 고침 하는 것 만큼 쉽게!

편집의 연습 동영상을 참조 하 고 Visual Studio 2005에서 기능을 계속 하려면 여기를 클릭 합니다.


![](improvements-in-visual-studio-2005/_static/image2.png)


[전체 화면 비디오 열기](improvements-in-visual-studio-2005/_static/editcontinue1.wmv)


강력한 편집 하며 계속 하기 기능 ASP.NET 2.0에서 및 ASP.NET 응용 프로그램에 대 한 아키텍처 변경으로 인해 Visual Studio 2005는 합니다. ASP.NET에서 Visual Studio 2002/2003에서 만든 응용 프로그램 1.x /bin 폴더에 저장 된 기본 어셈블리로 컴파일된 합니다. 모든 클래스, 페이지, 등 해당 하나의 DLL에 컴파일된 응용 프로그램에 대 한 합니다. 다음 런타임 시, ASP.NET 컨트롤, 태그 및 페이지 내의 ASP.NET 코드의 모든 컴파일 것 및 Dll에는 ASP.NET 임시 폴더에 복사 합니다.

두 개의 컴파일 모델 런타임에 (Visual Studio 용 하나) 및 ASP.NET에 대 한 위의 설명에 ASP.NET 2.0을 사용 하는 Visual Studio 2005에서 한 하나의 일반적인 컴파일 모델에 병합 되었습니다. 즉, 런타임에 모든 컴파일 문제가 대신 개발 단계에서 이제 발생 합니다. 디자이너와 사용자 정의 컨트롤 및 마스터 페이지 등의 기능에 대 한 IntelliSense 지원에 대 한 수도 있습니다.

사용자 정의 컨트롤에 대 한 디자이너 지원 연습 비디오를 보려면 여기를 클릭 합니다.


![](improvements-in-visual-studio-2005/_static/image3.png)


[전체 화면 비디오 열기](improvements-in-visual-studio-2005/_static/usercontrols1.wmv)


> [!NOTE]
> 사용자 정의 컨트롤은 페이지에서 제거 되 면는 @Register 지시문을 태그에 상태를 유지 하 고 웹 사이트에서 사용자 정의 컨트롤을 삭제 하는 파서 오류를 방지 하려면 수동으로 제거 해야 합니다.


다른 향상 된 Visual Studio 컴파일 모델은 웹 사이트 게시 기능입니다. 게시 기능 웹 사이트를 미리 컴파일하고, 때문에 개발자가 요청에 있는 모든 내용을 컴파일할 필요가 없으므로 때문에 성능이 향상된 누릴 수 있습니다. 것도 미리 컴파일한 앱/_Code 폴더의 모든 소스 코드를 DLL로 소스 코드가 없는를 배포할 수 있도록 합니다.


![게시 웹 사이트 대화 상자](improvements-in-visual-studio-2005/_static/image7.jpg)

**그림 10**: 게시 웹 사이트 대화 상자


> [!NOTE]
> ASP.NET 웹 응용 프로그램을 미리 컴파일 aspnet/_compile.exe 유틸리티를 사용할 수도 있습니다. 모듈 9에에서 해당 도구를 설명 합니다.


경우 아래와 같이 Temporary ASP.NET Files 폴더에 저장 됩니다 게시 웹 사이트를 미리 컴파일된 파일 있습니다. 사용 하 여 파일을 *.compiled* 파일 확장명은 특정 Dll에 대 한 종속성을 정의 하는 XML 파일입니다. 모든 Webform 또는 사용자 정의 컨트롤으로 시작 하는 임의의 Dll로 컴파일되는 *응용 프로그램 /_웹 /_* 합니다.

두면는 *미리 컴파일된이 사이트를 업데이트할 수 있도록 허용* checkbox가 선택 태그 Webforms 및 사용자 컨트롤 내에서 배포 후 변경할 수 있도록 하는 DLL로 미리 컴파일된 되지 것입니다. 배포 된 콘텐츠에 대 한 변경이 허용 되지 않습니다 수 있도록 태그 고정 하지 않으려면이 확인란의 선택을 취소 합니다.

*사용 하 여 고정 명명 고 페이지당 하나의 어셈블리만* 확인란을 사용 하 여 각 페이지는 고정 이름의 어셈블리에 컴파일됩니다 일괄 컴파일을 사용 하지 않도록 설정할 수 있습니다. 이 상자를 선택 되지 않은 상태로 일괄 컴파일을 활용할 수 있습니다.

*미리 컴파일된 어셈블리에서 강력한 이름 사용* 확인란을 선택 하면 강력한 이름을 지정 하 여 미리 컴파일된 어셈블리입니다.

> [!NOTE]
> ASP.NET에서 1.x 강력한 이름의 어셈블리를 전역 어셈블리 캐시 (GAC)에 설치 해야 합니다. ASP.NET 2.0에서는 강력한 이름의 어셈블리를 GAC에 설치 하는 데 필요 없는 경우


![ASP.NET 응용 프로그램 미리 컴파일된 파일](improvements-in-visual-studio-2005/_static/image8.jpg)

**그림 11**: ASP.NET 응용 프로그램 미리 컴파일된 파일


> [!NOTE]
> 위의 응용 프로그램에 web.config 파일이 있었습니다. 있었다면, 것은 호출 된 *PrecompiledApp.config* 웹 게시 한 후 사이트 프로세스입니다.


## <a name="improvements-in-deployment"></a>배포 향상 기능

으로 Visual Studio 2002 및 2003을 사용 하 여 Visual Studio 2005에서는 프로젝트 복사 기능을 제공 합니다. 그러나이 기능은 Visual Studio 2005에서 강화 되었습니다 않으며은 이제 이라는 웹 사이트 복사 합니다.

웹 사이트 복사 대화는 왼쪽된 프레임 및 오른쪽 프레임으로 분할 됩니다. 왼쪽된 프레임은 소스 웹 사이트, 오른쪽 프레임은 원격 웹 사이트 라고 합니다. 일부 개발자가 혼동을 줄 수 있는 한 가지 없다는 오른쪽 프레임에 표시 되는 사이트 반드시 원격 사이트입니다. IIS의 로컬 인스턴스 또는 로컬 파일 시스템에서 사이트 수 있습니다. 또한 왼쪽된 프레임에 표시 되는 사이트 아닐 소스 웹 사이트 대화 상자를 사용 하면 원격 웹 사이트에서 게시할 수 있으므로 *를* 소스 웹 사이트입니다.

원격 웹 사이트에는 프로젝트를 복사 하는 경우 해당 사이트에 설치 된 FrontPage Server Extensions 있어야 합니다. 그렇지 않은 경우 FTP를 사용 하 여 연결 해야 합니다. 반면에 로컬 IIS 인스턴스에 프로젝트를 복사 하는 경우 FrontPage Server Extensions 필요 하지 않습니다.

> [!NOTE]
> 로컬 IIS 인스턴스에서 새 웹 사이트를 만들려고 시도 하는 경우 FrontPage 2002 Server Extensions가 설치 된 SharePoint 서버에서 웹 사이트 만들기가 지원 되지 않습니다는 라는 오류 메시지가 얻게 됩니다. 이 경우 FrontPage 2000 Server Extensions를 설치 하거나 FrontPage Server Extensions 제거 옵션도 있습니다.


웹 사이트 복사 기능을 연습 동영상을 보려면 여기를 클릭 합니다.


![](improvements-in-visual-studio-2005/_static/image4.png)


[전체 화면 비디오 열기](improvements-in-visual-studio-2005/_static/copysite1.wmv)


## <a name="improvements-in-debugging"></a>디버깅의 향상 된 기능

Visual Studio 2005에서 디버깅 하는 네 가지 주요 향상 기능이 있습니다.

- 기본적으로 관리자가 아닌 로컬로 디버깅 불가능 합니다.
- 컴파일 요소에 대 한 디버그 특성은 기본적으로 false 이제입니다.
- 원격 디버깅 설치 및 구성 하는 이전 보다 훨씬 간단 합니다.
- 이제 FTP 위치를 통해 연 웹 사이트를 디버깅할 수 있습니다.

## <a name="debugging-as-a-non-administrator"></a>관리자가 아닌 방식으로 디버깅

ASP.NET 개발 서버를 추가 관리자 이외의 사용자가을 쉽게 즉시 ASP.NET 응용 프로그램을 디버깅할 수 있습니다. 로컬 파일 시스템에서 실행 중인 ASP.NET 응용 프로그램을 디버깅할 때 Visual Studio는 로그온 한 사용자의 컨텍스트 내에서 ASP.NET 개발 서버를 시작 합니다. 그러면 해당 사용자 추가 구성 없이 해당 응용 프로그램을 디버깅할 수 있습니다.

## <a name="debug-is-false-by-default"></a>디버그 False가 기본적으로

ASP.NET에서 1.x는 *디버그* 특성에 *컴파일* web.config 파일의 요소를 설정한 *true* 기본적으로 합니다. 그 항상 추천한 개발자가이 특성을 설정 *false* 프로덕션 환경에 응용 프로그램을 배포 하기 전에 있지만 대부분의 개발자로 설정 된 디버그 특성 종료 작업의 결과 완전히 이해 하지 때문에 true 이면 단순히 마지막로-됩니다.

가장 심각한 문제 디버그 특성이 true로 설정 된 ASP.NETs 컴파일 모델을 일괄 처리를 해제 함을 합니다. 따라서 각 페이지는 별도 DLL로 컴파일됩니다. 의미 있는 웹 응용 프로그램이 수천 페이지 (하지 드러나지의 어떤 방법으로)는 구성 하는 경우 해당 응용 프로그램에서 여러 개의 작은 Dll이 천 만들어질 수 있습니다. 이러한 Dll은 크기가 작으며, 메모리의 특정 위치에 로드 되지 않습니다. 따라서 이들은 시스템 메모리에서 조각화가 발생 하며 OutOfMemoryException 발생 될 수 있습니다.

ASP.NET 2.0에서 debug 특성은 기본적으로 false로 설정 됩니다. 이미 확인 한 것 처럼, 개발자는 Visual Studio 2005에서 ASP.NET 응용 프로그램을 디버깅 하는 경우 디버깅 하도록 설정한 web.config 파일을 추가 하려면 메시지가 표시 됩니다. ASP.NET에 있던 동일한 단점 그로 인해 이렇게 1.x 하지만 이제 개발자는 특성을 프로덕션 환경에 응용 프로그램을 이동 하기 전에 false로 다시 설정할지를 경고 명확 하 게 합니다.

## <a name="remote-debugging-setup-and-configuration"></a>원격 디버깅 설치 및 구성

Visual Studio 2002/2003에서 컴퓨터 디버그 관리자 (mdm.exe) 및 vs7jit.exe 프로세스에 사용한 원격 디버깅 합니다. 즉, 원격 디버깅 문제 해결 종종 고객에 대 한 검은색 상자 인시던트 였으며 PSS에 대 한 훨씬 더 자주 하지 못했습니다.

Visual Studio 2005 mdm.exe 및 vs7jit.exe 프로세스에 대 한 의존도 제거합니다. 대신 사용 한다는 점을 원격 디버그 모니터 (msvsmon.exe) 서비스

Visual Studio 2005의 원격 디버깅에 대 한 요구 사항은 매우 간단 합니다. 디버깅 하기 전에 원격 서버에서 msvsmon.exe를 실행 해야 합니다. Visual Studio CD에서 원격 디버그 모니터를 설치할 수 있습니다 또는 웹 서버에 전혀 아무것도 설치 하지 않고 공유에서 msvsmon.exe를 간단히 실행할 수 있습니다.

Msvsmon.exe를 실행 하면 원격 디버깅 차단 되 고 포트에 대 한 것에서 문제가 발생할 수도 가능성이 높습니다. 다행히 쉽게 차단 해제할 수 있습니다 포트 오른쪽 경고 대화 상자 내에서 다음과 같이 합니다.


![Windows 방화벽이 원격 디버깅 차단 인지 알림](improvements-in-visual-studio-2005/_static/image9.jpg)

**그림 12**: 알림 Windows 방화벽이 원격 디버깅 차단 됩니다.


디버깅에 필요한 포트를 차단이 해제 되 면 아래와 같이 원격 디버깅 모니터 나타납니다. 이 인터페이스에서 연결을 모니터링 하 고 디버깅 권한이 쉽게 변경할 수 있습니다.


![원격 디버깅 모니터](improvements-in-visual-studio-2005/_static/image10.jpg)

**그림 13**: 원격 디버깅 모니터


에 원격으로 FTP를 통해 열린 웹 응용 프로그램을 디버깅할 수 이기도 합니다. 단계 이전에 설명 된와 동일 합니다. 그러나이 모듈의 앞부분에 설명 된 대로 FTP 프로젝트 검색에 대 한 기본 URL을 지정 해야 합니다.

## <a name="lab-2"></a>Lab 2

## <a name="remote-debugging-with-visual-studio-2005"></a>Visual Studio 2005를 사용 하 여 원격 디버깅

이 실습에서는 Visual Studio 2005를 사용 하 여 원격 디버깅을 통해 안내 합니다.

이 랩의 연습 동영상을 보려면 여기를 클릭 합니다.


![](improvements-in-visual-studio-2005/_static/image5.png)


[전체 화면 비디오 열기](improvements-in-visual-studio-2005/_static/remdebug1.wmv)


이 랩에서 사용 하면 하나의 Visual Studio 2005를 실행 하 고 다른 실행 중인 IIS 5 이상 두 컴퓨터를 포함 하도록 해야 합니다.

1. Visual Studio 2005를 열고 원격 서버에서 새 웹 사이트를 만듭니다.

> [!NOTE]
> 원격 IIS 인스턴스 또는 FTP를 통해 웹 사이트를 만들 수 있습니다.


1. 원격 웹 서버에서 UNC 경로 사용 하 여 개발 컴퓨터에서 msvsmon.exe를 찾아 실행 합니다.  
 Msvsmon.exe의 기본 위치는 //server/c$/Program 파일/Microsoft Visual Studio 8/Common7/IDE/원격 디버거/x86 합니다.
2. 원격 디버깅을 위해 포트 차단을 해제 하 라는 메시지가 나타나면 그렇게 합니다.
3. 개발 컴퓨터에서 Default.aspx에 대 한 코드 숨김 열고 페이지 / (_l) 메서드에 중단점을 설정 합니다.
4. 개발 컴퓨터에서 디버깅을 시작 합니다.

예상 대로 중단점이 적중 되어야 합니다.

## <a name="aspnet-development-server"></a>ASP.NET Development Server

앞에서 설명한 마십시오,으로 Visual Studio 2005 ASP.NET 개발 서버를 호출 하는 웹 서버와 함께 제공 됩니다. (ASP.NET 개발 서버는 라고도 Cassini.) 이 웹 서버가을 찾아서 다음 파일 시스템에서 실행 되는 웹 응용 프로그램을 디버깅 하는 편리한 방법입니다.

ASP.NET 개발 서버는 제한 된 웹 서버. 원격 연결을 허용 하지 않습니다, 그리고 웹 서버를 시작한 사용자 이외의 모든 사용자의 모든 요청을 허용 하지 않습니다. ASP 페이지를 처리 하는 기능이 있는 되지 않습니다. ASP.NET 리소스 및 HTML 리소스 (이미지, CSS 파일 등 포함)만 제공 됩니다.

C:/Windows/Microsoft.NET/Framework/v2.0./에 있는 WebDev.WebServer.exe 파일을 실행 하 여 명령줄을 통해 ASP.NET 개발 서버를 시작할 수*/* /  */*/*. 다음과 같은 대화 상자가 사용할 수 있는 매개 변수를 표시 합니다.


![](improvements-in-visual-studio-2005/_static/image11.jpg)

**그림 14**


> [!NOTE]
> 명령줄을 통해 명시적으로 시작 될 때 ASP.NET 개발 서버 지원 되지 않습니다.
