---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-your-site-using-an-ftp-client-cs
title: FTP 클라이언트 (C#)를 사용 하 여 사이트를 배포 합니다. | Microsoft Docs
author: rick-anderson
description: ASP.NET 응용 프로그램을 배포 하는 가장 간단한 방법은 개발 환경에서 프로덕션 환경에 필요한 파일을 수동으로 복사 방법은입니다. 이번...
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/01/2009
ms.topic: article
ms.assetid: a3599cf7-8474-4006-954a-3bc693736b66
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-your-site-using-an-ftp-client-cs
msc.type: authoredcontent
ms.openlocfilehash: 1fa0c72beb18ceabefeae41bec64dda036372d79
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37385329"
---
<a name="deploying-your-site-using-an-ftp-client-c"></a>FTP 클라이언트 (C#)를 사용 하 여 사이트 배포
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/4/5/F/45F815EC-8B0E-46D3-9FB8-2DC015CCA306/ASPNET_Hosting_Tutorial_03_CS.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial03_DeployingViaFTP_cs.pdf)

> ASP.NET 응용 프로그램을 배포 하는 가장 간단한 방법은 개발 환경에서 프로덕션 환경에 필요한 파일을 수동으로 복사 방법은입니다. 이 자습서에서는 웹 호스트 공급자에 바탕 화면에서 파일을 가져올 FTP 클라이언트를 사용 하는 방법을 보여 줍니다.


## <a name="introduction"></a>소개

이전 자습서를 간단한 책 검토 ASP.NET 웹 응용 프로그램을 ASP.NET 페이지, 마스터 페이지, 사용자 지정 기본 소수의 이루어집니다 도입 `Page` 클래스, 이미지, 개수 및 세 가지 CSS 스타일 시트입니다. 이제이 시점에서 응용 프로그램은 액세스할 수 있게 하려면 인터넷에 연결 된 웹 호스트 공급자를이 응용 프로그램을 배포할 준비가 되었습니다!


토론에서 합니다 [ *결정 파일 필요한 배포할* ](determining-what-files-need-to-be-deployed-cs.md) 자습서, 알고 웹 호스트 공급자에 복사 해야 하는 파일입니다. (파일 복사는 회수에 따라 달라 집니다 여부 응용 프로그램이 명시적으로 또는 자동으로 컴파일됩니다.) 그러나에서는 어떻게 파일 (데스크톱) 개발 환경에서 프로덕션 환경 (웹 호스트 공급자에 의해 관리 되는 웹 서버)까지? 합니다 [ **F** ile **T** ransfer **P** rotocol (FTP)](http://en.wikipedia.org/wiki/File_Transfer_Protocol) 네트워크를 통해 다른 컴퓨터에서 파일을 복사 하는 데 자주 사용 되는 프로토콜입니다. 또 다른 방법은 FrontPage Server Extensions (FPSE)입니다. 이 자습서는 독립 실행형 FTP 클라이언트 소프트웨어를 사용 하 여 개발 환경에서 프로덕션 환경에 필요한 파일을 배포에 중점을 둡니다.

> [!NOTE]
> Visual Studio에는 FTP;를 통해 웹 사이트 게시 도구가 포함 되어 있습니다. 다음 자습서를 살펴보고 FPSE를 사용 하는 도구 뿐만 아니라 이러한 도구를 설명 합니다.


해야 하는 FTP를 사용 하 여 파일을 복사 하는 *FTP 클라이언트* 개발 환경에서. FTP 클라이언트를 실행 하는 컴퓨터에 설치 된 컴퓨터에서 파일을 복사 하도록 디자인 된 응용 프로그램을 *FTP 서버*합니다. (을 대부분 마찬가지로 FTP 통해 파일 전송을 웹 호스트 공급자에 지 원하는 경우 다음 FTP server가 해당 웹 서버에서 실행 합니다.) 사용할 수 있는 FTP 클라이언트 응용 프로그램의 여러 가지가 있습니다. 웹 브라우저를 FTP 클라이언트로 double 수 있습니다. 내 즐겨 찾는 FTP 클라이언트와이 자습서에서는 사용할 것은 [FileZilla](http://filezilla-project.org/), Windows, Linux 및 Mac에 사용할 수 있는 무료, 오픈 소스 FTP 클라이언트입니다. 모든 FTP 클라이언트 작동, 그러나 하므로 자유롭게 가장 편안한는 모든 클라이언트를 사용 합니다.

수에 따라 수행 하는 경우는 필요 하기 전에 웹 호스트 공급자를 사용 하 여 계정을 만들려면 완료할 수 있습니다이 자습서 또는 후속. 이전 자습서에서 설명한 대로, 다양 한 가격, 기능 및 서비스의 품질을 사용 하 여 웹 호스트 공급자 계열사 gaggle 가지가 있습니다. 이 자습서 시리즈를 사용 합니다. [할인 ASP.NET](http://discountasp.net) 내 웹 호스트 공급자 있지만 따르면 모든 웹 호스트 공급자와 함께 지 원하는 사이트에서 개발 된 ASP.NET 버전으로 합니다. (이러한 자습서 사용 하 여 만든 ASP.NET 3.5.) 또한 복사할 파일의 웹 호스트 공급자 수는 것 때문에 FTP를 사용 하 여이 자습서 및 나중에 적용될지 반드시 웹 호스트 공급자는 웹 서버에 대 한 FTP 액세스를 지원 합니다. 거의 모든 웹 호스트 공급자는이 기능을 제공 하지만 등록 하기 전에 다시 확인 해야 합니다.

## <a name="deploying-the-book-review-web-application-project"></a>책 검토 웹 응용 프로그램 프로젝트 배포

두 가지 버전 서적 검토 웹 응용 프로그램의 회수: 웹 응용 프로그램 프로젝트 모델 (BookReviewsWAP) 및 웹 사이트 프로젝트 모델로 (BookReviewsWSP)를 사용 하 여 사용 하 여 구현 합니다. 사이트를 자동으로 또는 명시적으로 컴파일되고 해당 컴파일 모델 배포 해야 하는 파일을 지정 하는지 여부를 프로젝트 형식에 영향을 줍니다. 따라서 살펴보겠습니다 BookReviewsWAP 및 BookReviewsWSP 프로젝트를 개별적으로 배포 된 BookReviewsWAP부터. 시간을 내어 하지 않았으면 지금 이미 있는 경우 이러한 두 ASP.NET 응용 프로그램을 다운로드 합니다.

로 이동 하 여 BookReviewsWAP 프로젝트를 시작 합니다 `BookReviewsWAP` 폴더를 두 번 클릭 하 고는 `BookReviewsWAP.sln` 파일입니다. 가 프로젝트를 배포 하기 전에 빌드 컴파일된 어셈블리에서 소스 코드에 변경 내용을 포함 하도록 해야 합니다. 프로젝트를 빌드하려면 빌드 메뉴로 이동 하 고 빌드 BookReviewsWAP 메뉴 옵션을 선택 합니다. 프로젝트의 소스 코드를 단일 어셈블리로 컴파일하고이 `BookReviewsWAP.dll`에 배치 되는 `Bin` 폴더입니다.

이제 필요한 파일을 배포할 준비가 되었습니다! FTP 클라이언트를 시작 하 고 웹 호스트 공급자에서 웹 서버에 연결 합니다. (웹 호스팅 회사를 사용 하 여 로그인 할 때 이러한는 전자 메일을 보내 FTP 서버에 연결 하는 방법에 대 한 정보는이 FTP 서버 뿐만 아니라 사용자 이름 및 암호에 대 한 주소를 포함 합니다.)

바탕 화면에서 다음 파일을 웹 호스트 공급자에서 루트 웹 사이트 폴더에 복사 합니다. 웹 서버에 FTP 웹에서 호스팅할 때 공급자 루트 웹 사이트 디렉터리에서 가능성이 높습니다. 그러나 일부 웹 호스트 공급자는 라는 하위 폴더 `www` 또는 `wwwroot` 웹 사이트 파일에 대 한 루트 폴더는 역할을 합니다. 마지막으로 파일 FTPing 때 해야-프로덕션 환경에서 해당 폴더 구조를 만듭니다는 `Bin` 폴더를 `Fiction` 폴더를 `Images` 폴더 등에입니다.

- `~/Default.aspx`
- `~/About.aspx`
- `~/Site.master`
- `~/Web.config`
- `~/Web.sitemap`
- 전체 콘텐츠를 `Styles` 폴더
- 전체 콘텐츠를 `Images` 폴더 (및 해당 하위 폴더 `BookCovers`)
- `~/Fiction/Default.aspx`
- `~/Fiction/Blaze.aspx`
- `~/Tech/Default.aspx`
- `~/Tech/CYOW.aspx`
- `~/Tech/TYASP35.aspx`
- `~/Bin/BookReviewsWAP.dll`

그림 1에서는 필요한 파일을 복사한 후 FileZilla를 보여 줍니다. FileZilla는 왼쪽 및 오른쪽에 원격 컴퓨터의 파일에 로컬 컴퓨터의 파일을 표시합니다. 그림 1에 나와 것 처럼 ASP.NET 소스 코드 파일을 같은 `About.aspx.cs`, 로컬 컴퓨터 (개발 환경)에 있지만 코드 파일을 사용 하는 경우 배포할 필요가 있으므로 웹 호스트 공급자 (프로덕션 환경)에 복사 되지 않았습니다 명시적 컴파일입니다.

> [!NOTE]
> 에 됩니다 프로덕션 서버에서 소스 코드 파일에 피해를 주지 무시 됩니다. ASP.NET 소스 코드 파일을 프로덕션 서버에 있는 경우에 없는 웹 사이트 방문자에 액세스할 수 있도록 기본적으로 소스 코드 파일에 HTTP 요청을 금지 합니다. (즉, 사용자가 방문 하려고 하는 경우 `http://www.yoursite.com/Default.aspx.cs` 설명 하는 오류 페이지가 이러한 종류의 파일-생깁니다 `.cs` 파일을 사용할 수 없습니다.)


[![FTP 클라이언트를 사용 하 여 웹 서버는 웹 호스트 공급자에 바탕 화면에서 필요한 파일을 복사 하려면](deploying-your-site-using-an-ftp-client-cs/_static/image2.png)](deploying-your-site-using-an-ftp-client-cs/_static/image1.png)

**그림 1**: 웹 서버는 웹 호스트 공급자에 바탕 화면에서 필요한 파일을 복사 하는 FTP 클라이언트를 사용 하 여 ([큰 이미지를 보려면 클릭](deploying-your-site-using-an-ftp-client-cs/_static/image3.png))


사이트를 배포한 후 잠시 사이트를 테스트 합니다. 도메인 이름 구입 및 DNS 설정을 구성 해야 하는 경우 제대로 도메인 이름을 입력 하 여 사용자 사이트를 방문할 수 있습니다. 또는 웹 호스트 공급자는 제공한 하면 사이트에 대 한 URL을 사용 하 여는 모양은 *accountname*. *webhostprovider*.com 또는 *webhostprovider*.com /*accountname*합니다. 예를 들어 ASP.NET 할인에 내 계정에 대 한 URL은: `http://httpruntime.web703.discountasp.net`합니다.

그림 2에서는 배포 된도 서 리뷰 사이트를 보여 줍니다. 보고 해당 할인 asp를 참고 합니다. NET의 서버에서 `http://httpruntime.web703.discountasp.net`합니다. 이 시점에서 내 웹 사이트를 볼 수는 인터넷에 연결 된 모든 사용자가! 를 의도 한 대로 사이트의 모양과 개발 환경에서 테스트할 때 수행한 것 처럼 동작 합니다.

> [!NOTE]
> 잠시가 되도록 응용 프로그램을 볼 때 오류가 발생 하는 경우 올바른 파일 집합이 배포 했습니다. 다음으로, 문제에 대 한 단서를 표시 하는 경우 오류 메시지를 확인 합니다. 다음 웹 호스트 회사의 헬프 데스크를 설정 하거나 적절 한 포럼에 질문을 게시 합니다 [ASP.NET 포럼](https://forums.asp.net/)합니다.


[![인터넷에 연결 된 모든 사용자에 게 책 검토 사이트를 이제 액세스할 수](deploying-your-site-using-an-ftp-client-cs/_static/image5.png)](deploying-your-site-using-an-ftp-client-cs/_static/image4.png)

**그림 2**: 인터넷에 연결 된 모든 사용자에 게는 책 검토 사이트는 이제 액세스할 수 있습니다 ([큰 이미지를 보려면 클릭](deploying-your-site-using-an-ftp-client-cs/_static/image6.png))


## <a name="deploying-the-book-review-web-site-project"></a>책 검토 웹 사이트 프로젝트를 배포합니다.

컴파일된 어셈블리 없음 방법이 BookReviewsWSP 웹 사이트 프로젝트와 같은 자동 컴파일을 사용 하는 ASP.NET 응용 프로그램을 배포 하는 경우는 `Bin` 폴더입니다. 결과적으로, 웹 응용 프로그램의 소스 코드 파일을 프로덕션 환경에 배포 되어야 합니다. 이 프로세스를 살펴보겠습니다.

와 마찬가지로 웹 응용 프로그램 프로젝트를 배포 하기 전에 응용 프로그램 빌드하는 것이 좋습니다. 웹 사이트 프로젝트를 빌드할 어셈블리 만들지 않습니다, 하지만 페이지의 컴파일 타임 오류 검사지 않습니다. 검색할 사이트 방문자가 필요 하지 않고이 오류를 찾기 위해 이러한 이제 더 나은!

프로젝트를 성공적으로 빌드하면 FTP 클라이언트를 사용 하 여 웹 호스트 공급자에서 루트 웹 사이트 폴더에 다음 파일을 복사 합니다. 프로덕션 환경에서 해당 폴더 구조를 생성 해야 합니다.

> [!NOTE]
> 프로젝트는 있지만 BookReviewsWSP 프로젝트 배포를 시도 하려는 BookReviewsWAP을 이미 배포한 경우 먼저 BookReviewsWAP를 배포 하는 경우 업로드 된 웹 서버에 있는 파일의 모든를 삭제 하 고 BookReviewsWSP에 대 한 파일을 배포 합니다.


- `~/Default.aspx`
- `~/Default.aspx.cs`
- `~/About.aspx`
- `~/About.aspx.cs`
- `~/Site.master`
- `~/Site.master.cs`
- `~/Web.config`
- `~/Web.sitemap`
- 전체 콘텐츠를 `Styles` 폴더
- 전체 콘텐츠를 `Images` 폴더 (및 해당 하위 폴더 `BookCovers`)
- `~/App_Code/BasePage.cs`
- `~/Fiction/Default.aspx`
- `~/Fiction/Default.aspx.cs`
- `~/Fiction/Blaze.aspx`
- `~/Fiction/Blaze.aspx.cs`
- `~/Tech/Default.aspx`
- `~/Tech/Default.aspx.cs`
- `~/Tech/CYOW.aspx`
- `~/Tech/CYOW.aspx.cs`
- `~/Tech/TYASP35.aspx`
- `~/Tech/TYASP35.aspx.cs`

그림 3에서는 필요한 파일을 복사한 후 FileZilla를 보여 줍니다. ASP.NET 소스와 같은 코드 파일을 볼 수 있듯이 `About.aspx.cs`, 코드 파일에서 자동을 사용 하는 경우 배포 해야 하기 때문에 로컬 컴퓨터 (개발 환경)와 웹 호스트 공급자 (프로덕션 환경)에 컴파일입니다.


[![FTP 클라이언트를 사용 하 여 웹 서버는 웹 호스트 공급자에 바탕 화면에서 필요한 파일을 복사 하려면](deploying-your-site-using-an-ftp-client-cs/_static/image8.png)](deploying-your-site-using-an-ftp-client-cs/_static/image7.png)

**그림 3**: 웹 서버는 웹 호스트 공급자에 바탕 화면에서 필요한 파일을 복사 하는 FTP 클라이언트를 사용 하 여 ([큰 이미지를 보려면 클릭](deploying-your-site-using-an-ftp-client-cs/_static/image9.png))


사용자 환경 응용 프로그램의 컴파일 모델에 의해 영향을 받지 않습니다. 동일한 ASP.NET 페이지에 액세스할 수 및 표시 하며 웹 사이트는 웹 응용 프로그램 프로젝트 모델 또는 웹 사이트 프로젝트 모델을 사용 하 여 만들었는지 여부를 동일 하 게 동작 합니다.

### <a name="updating-a-web-application-on-production"></a>프로덕션 웹 응용 프로그램 업데이트

웹 응용 프로그램 개발 및 배포 하는 일회성 프로세스 않습니다. 예를 들어 서적 검토 웹 사이트를 만들 때 다양 한 페이지를 작성 했으며 개인용 컴퓨터 (개발 환경) 내에 함께 제공 되는 코드를 작성 합니다. 특정 안정적인 상태에 도달한 후 합니까 내 응용 프로그램을 배포 사이트를 방문 내 리뷰를 읽을 수 있도록 합니다. 하지만 배포 내 개발이이 사이트에서의 끝을 표시 하지 않습니다. 수 추가 자세한도 서 리뷰 또는 속도 책 내 방문자를 허용 하는 등의 새로운 기능을 구현 하거나 자신의 의견을 남겨 합니다. 이러한 향상 된 개발 환경에서 개발할 수는 및 완료 되 면 배포 해야 합니다. 개발 및 배포, 따라서 순환 됩니다. 응용 프로그램을 개발 하 고 배포 합니다. 프로덕션 환경에서 및을 사이트가 라이브 인지 하는 동안 새 기능이 추가 되었습니다 하 고 다시 응용 프로그램을 배포 해야 하는 시간이 지남에 따라 버그를 수정 합니다. 등에 등입니다.

예상할 수 있듯이, 새로운 기능과 변경 된 파일을 복사 해야 하는 웹 응용 프로그램을 다시 배포 하는 경우. 변경 되지 않은 페이지를 다시 배포 하지 않아도 없거나 서버 또는 클라이언트 쪽 (하지만 이렇게 하더라도 피해는) 파일을 지원 합니다.

> [!NOTE]
> 염두에서에 두 경우 명시적 컴파일을 사용 하는 프로젝트에 새 ASP.NET 페이지를 추가 하거나 코드와 관련 된 내용을 변경, 언제 든 지 다시 작성 해야 프로젝트에서 어셈블리를 업데이트 하는 것은 `Bin` 폴더입니다. 따라서 프로덕션 (다른 새로운 기능과 업데이트 된 콘텐츠와 함께)에서 웹 응용 프로그램을 업데이트 하는 경우 프로덕션 환경에이 업데이트 된 어셈블리를 복사 해야 합니다.


이해를 변경 하는 `Web.config` 또는 파일을 `Bin` 디렉터리 중지 하 고 웹 사이트의 응용 프로그램 풀을 다시 시작 합니다. 사용 하 여 세션 상태 저장 되는 경우는 `InProc` 모드 (기본값) 다음 사이트의 방문자에 게 이러한 키 파일이 수정 될 때마다 해당 세션 상태를 잃게 됩니다. 이 문제를 방지 하는 것이 좋습니다 사용 하 여 세션을 저장 합니다 `StateServer` 또는 `SQLServer` 모드입니다. 이 항목에 대 한 자세한 내용은 읽을 [세션 상태 모드](https://msdn.microsoft.com/library/ms178586.aspx)합니다.

마지막으로, 프로덕션 환경에 복사 해야 하는 파일의 크기와 수에 따라 몇 분 정도 몇 초에서 어디서 나 사용할 수 응용 프로그램을 다시 배포 있는 염두에 둡니다. 이 시간 동안 해당 사이트를 방문 하는 사용자 오류 또는 부적절 한 동작 발생할 수 있습니다. 해제할 수 있습니다"" 전체 응용 프로그램 라는 페이지를 추가 하 여 `App_Offline.htm` 사용자에 게 설명 하는 응용 프로그램의 루트 디렉터리에는 사이트 유지 관리 (또는 모든) 중단 되 고이가 하는 수 백업 곧 합니다. 경우는 `App_Offline.htm` 파일이 있는지, ASP.NET 런타임이 해당 페이지로 들어오는 모든 요청을 리디렉션합니다.

## <a name="summary"></a>요약

웹 응용 프로그램을 배포 하려면 개발 환경에서 프로덕션 환경에 필요한 파일을 복사 해야 합니다. 네트워크를 통해 파일이 전송 되는 가장 일반적인 방법은 FTP 파일 전송 프로토콜 (), 이며 대부분의 웹 호스트 공급자는 웹 서버에 FTP 액세스를 지원 합니다. 이 자습서에서는 웹 서버에 필요한 파일을 배포 하는 FTP 클라이언트를 사용 하는 방법에 살펴보았습니다. 을 배포한 후 웹 사이트를 방문할 수 있습니다 누구나 연결으로 인터넷에!

즐거운 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [앱\_Offline.htm 및 "IE 친숙 한 오류" 기능을 해결 하기](https://weblogs.asp.net/scottgu/App_5F00_Offline.htm-and-working-around-the-_2200_IE-Friendly-Errors_2200_-feature)
- [세션 상태 모드](https://msdn.microsoft.com/library/ms178586.aspx)

> [!div class="step-by-step"]
> [이전](determining-what-files-need-to-be-deployed-cs.md)
> [다음](deploying-your-site-using-visual-studio-cs.md)
