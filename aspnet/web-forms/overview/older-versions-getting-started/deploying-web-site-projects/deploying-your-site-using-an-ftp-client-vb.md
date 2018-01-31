---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-your-site-using-an-ftp-client-vb
title: "FTP 클라이언트 (VB)를 사용 하 여 사이트를 배포 합니다. | Microsoft Docs"
author: rick-anderson
description: "ASP.NET 응용 프로그램을 배포 하는 가장 간단한 방법은 개발 환경에서 프로덕션 환경에 필요한 파일을 수동으로 복사 하는 합니다. 여..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/01/2009
ms.topic: article
ms.assetid: 09279194-bcf9-4b59-a09d-c68e5926a758
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-your-site-using-an-ftp-client-vb
msc.type: authoredcontent
ms.openlocfilehash: 7792891aed6f0c5e952018dacb36a1d267cb6ae0
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
<a name="deploying-your-site-using-an-ftp-client-vb"></a>FTP 클라이언트 (VB)를 사용 하 여 사이트를 배포 합니다.
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/4/5/F/45F815EC-8B0E-46D3-9FB8-2DC015CCA306/ASPNET_Hosting_Tutorial_03_VB.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial03_DeployingViaFTP_vb.pdf)

> ASP.NET 응용 프로그램을 배포 하는 가장 간단한 방법은 개발 환경에서 프로덕션 환경에 필요한 파일을 수동으로 복사 하는 합니다. 이 자습서에는 웹 호스트 공급자에 데스크톱에서 파일을 가져올 수는 FTP 클라이언트를 사용 하는 방법을 보여 줍니다.


## <a name="introduction"></a>소개

이전 자습서는 간단한 책 검토 ASP.NET 웹 응용 프로그램, ASP.NET 페이지, 마스터 페이지, 사용자 지정 자료는 소수의으로 구성 되는 도입 `Page` 클래스, 이미지, 수 및 3 개의 CSS 스타일 시트입니다. 이제 이때 응용 프로그램을 인터넷에 연결 된 모든 사용자에 게 액세스할 수 있는 웹 호스트 공급자에이 응용 프로그램을 배포할 준비가 되었습니다!


우리의 논의는 [ *결정 어떤 파일 배포 해야 할* ](determining-what-files-need-to-be-deployed-vb.md) 자습서, 회원님의 웹 호스트 공급자에 복사 해야 하는 파일입니다. (회수 어떤 파일이 복사 되는 여부 응용 프로그램이 명시적으로 또는 자동으로 컴파일되고에 따라 다릅니다.) 하지만 수행 우리 파일에서에서 어떻게 개발 환경 (desktop)까지 프로덕션 환경 (웹 호스트 공급자에 의해 관리 되는 웹 서버)? [ **F** ile **T** ransfer **P** rotocol (FTP)](http://en.wikipedia.org/wiki/File_Transfer_Protocol) 를 한 컴퓨터에서 네트워크를 통해 다른 파일을 복사 하는 데 자주 사용 되는 프로토콜입니다. 두 번째 방법은 FrontPage Server Extensions (FPSE)입니다. 이 자습서는 독립 실행형 FTP 클라이언트 소프트웨어를 사용 하 여 개발 환경에서 프로덕션 환경에 필요한 파일을 배포 하려면에 중점을 둡니다.

> [!NOTE]
> Visual Studio; FTP 통해 웹 사이트 게시 도구를 포함합니다. 다음 자습서를 살펴보면 FPSE를 사용 하는 도구 뿐만 아니라 이러한 도구를 설명 합니다.


해야 하는 FTP를 사용 하 여 파일을 복사 하는 *FTP 클라이언트* 개발 환경에 있습니다. FTP 클라이언트는 실행 중인 컴퓨터에 설치 된 컴퓨터에서 파일을 복사 하도록 설계 된 응용 프로그램 프로그램 *FTP 서버*합니다. (웹 호스트 공급자에서 지원할 경우 FTP 통해 파일을 전송 대부분와 마찬가지로, 다음가 해당 웹 서버에서 실행 하는 FTP 서버입니다.) 사용할 수 있는 FTP 클라이언트 응용 프로그램의 여러 가지가 있습니다. 웹 브라우저는 FTP 클라이언트로 double 수 있습니다. 내 즐겨 찾는 FTP 클라이언트와이 자습서에 대 한 사용 하겠습니다 하나는 [FileZilla](http://filezilla-project.org/), Windows, Linux 및 Mac에 사용할 수 있는 무료, 오픈 소스 FTP 클라이언트입니다. 어떤 FTP 클라이언트 작동, 하지만 그럴 자유롭게 모든 클라이언트에 익숙한 가장을 사용 합니다.

따라 있습니다 하는 경우 됩니다 필요 하기 전에 웹 호스트 공급자를 사용 하 여 계정 키를 만들려면 완료할 수 있습니다이 자습서 또는 이후의 조건. 이전 자습서에서 설명한 대로, 가격, 기능 및 서비스 품질의 다양 한와 웹 호스트 공급자 회사의 gaggle가 있습니다. 이 자습서 시리즈에 대 한 사용 하겠습니다 [할인 ASP.NET](http://discountasp.net) 내 웹 호스트 공급자에 있지만 함께 수행할 수 모든 웹 호스트 공급자도에서 사이트를 개발 하는 ASP.NET 버전을 지원 합니다. (이러한 자습서 사용 하 여 만든 ASP.NET 3.5.) 또한 되기 때문에 우리는 수 파일을 복사할 웹 호스트 공급자 FTP를 사용 하 여이 자습서에서는 및에서 나중에 스토리 명령적 웹 호스트 공급자의 웹 서버에 대 한 FTP 액세스를 지원 합니다. 거의 모든 웹 호스트 공급자는이 기능을 제공 하지만 등록 하기 전에 여러 번 확인 해야 합니다.

## <a name="deploying-the-book-review-web-application-project"></a>책 검토 웹 응용 프로그램 프로젝트를 배포합니다.

우수 웹 응용 프로그램의 두 버전이 있습니다 회수: 웹 응용 프로그램 프로젝트 모델 (BookReviewsWAP) 오류 코드 및 기타 웹 사이트 프로젝트 모델 (BookReviewsWSP)를 사용 하 여 사용 하 여 구현 합니다. 프로젝트 형식 사이트가 자동으로 또는 명시적으로 컴파일되고 해당 컴파일 모델을 배포 해야 할 파일을 지정 여부에 영향을 줍니다. 따라서 살펴보겠습니다 BookReviewsWAP 및 BookReviewsWSP 프로젝트를 개별적으로 배포는 BookReviewsWAP로 시작 합니다. 잠시 하지 않았으면 지금 이미 하는 경우이 두 ASP.NET 응용 프로그램을 다운로드할 수 있습니다.

로 이동 하 여 BookReviewsWAP 프로젝트를 시작 합니다.는 `BookReviewsWAP` 폴더를 두 번 클릭 하 고 `BookReviewsWAP.sln` 파일입니다. 프로젝트를 배포 하기 전에 소스 코드를 변경 컴파일된 어셈블리에 포함 되어 있는지 확인 하도록 작성 해야 합니다. 프로젝트를 빌드하려면 빌드 메뉴로 이동한 BookReviewsWAP 빌드 메뉴 옵션을 선택 합니다. 단일 어셈블리에 프로젝트의 소스 코드를 컴파일하고이 `BookReviewsWAP.dll`에 추가 하는 `Bin` 폴더입니다.

이제 필요한 파일을 배포할 준비가 되었습니다! FTP 클라이언트를 시작 하 고 웹 호스트 공급자에서 웹 서버에 연결 합니다. (호스팅 업체는 웹 등록은 전자 메일로 전송 됩니다 하면 FTP 서버에 연결 하는 방법에 대 한 정보, 여기에 FTP 서버 뿐만 아니라 사용자 이름 및 암호에 대 한 주소)

바탕 화면에서 다음 파일을 웹 호스트 공급자에서 루트 웹 사이트 폴더에 복사 합니다. 웹 서버에 FTP는 웹에서 호스팅할 때 공급자 웹 사이트 루트 디렉터리에 가능성이 높습니다. 그러나 일부 웹 호스트 공급자는 라는 하위 폴더 `www` 또는 `wwwroot` 역할을 웹 사이트 파일에 대 한 루트 폴더입니다. 마지막으로, 파일 FTPing 때 해야 할 수 있습니다-프로덕션 환경에 해당 폴더 구조를 만드는 `Bin` 폴더는 `Fiction` 폴더는 `Images` 폴더 및 기타 등등.

- `~/Default.aspx`
- `~/About.aspx`
- `~/Site.master`
- `~/Web.config`
- `~/Web.sitemap`
- 전체 내용을 `Styles` 폴더
- 전체 내용을 `Images` 폴더 (및 그 하위 폴더 `BookCovers`)
- `~/Fiction/Default.aspx`
- `~/Fiction/Blaze.aspx`
- `~/Tech/Default.aspx`
- `~/Tech/CYOW.aspx`
- `~/Tech/TYASP35.aspx`
- `~/Bin/BookReviewsWAP.dll`

그림 1은 필요한 파일을 복사한 후 FileZilla를 보여줍니다. FileZilla 왼쪽 및 오른쪽에 원격 컴퓨터에 있는 파일에 로컬 컴퓨터에 있는 파일을 표시합니다. 그림 1와 같이 ASP.NET 소스 코드 파일 같은 `About.aspx.vb`, 로컬 컴퓨터 (개발 환경)에 있는 하지만 코드 파일을 사용 하는 경우 배포할 필요가 없습니다 때문에 웹 호스트 공급자 (프로덕션 환경)에 복사 되지 않았습니다 명시적 컴파일을 합니다.

> [!NOTE]
> 에 됩니다 프로덕션 서버에서 소스 코드 파일을 포함 하더라도 피해는 무시 됩니다. ASP.NET은 기본적으로 소스 코드 파일에 대 한 HTTP 요청을 금지 하는 소스 코드 파일 프로덕션 서버에 없는 경우에 방문자가 웹 사이트에 액세스할 수 없게 됩니다. (즉, 사용자가 방문 하려고 하는 경우 `http://www.yoursite.com/Default.aspx.vb` 이러한 종류의 파일-있음을 설명 하는 오류 페이지를 얻게 될 것 `.vb` -파일을 사용할 수 없습니다.)


[![FTP 클라이언트를 사용 하 여 웹 호스트 공급자에서 웹 서버에 바탕 화면에서 필요한 파일을 복사 합니다.](deploying-your-site-using-an-ftp-client-vb/_static/image2.png)](deploying-your-site-using-an-ftp-client-vb/_static/image1.png)

**그림 1**: FTP 클라이언트를 사용 하 여 데스크톱에서 웹 호스트 공급자에서 웹 서버에 필요한 파일을 복사 ([전체 크기 이미지를 보려면 클릭](deploying-your-site-using-an-ftp-client-vb/_static/image3.png))


사이트를 배포한 후 잠시 사이트 테스트 합니다. 도메인 이름 및에서 DNS 설정을 구성 해야 하는 경우 적절 하 게 도메인 이름을 입력 하 여 사이트를 방문할 수도 있습니다. 또는 웹 호스트 공급자 해야 제공한 하면 사이트에 url을 다음과 같이 표시 됩니다는 *accountname*. *webhostprovider*.com 또는 *webhostprovider*.com /*accountname*합니다. 예를 들어 ASP.NET 할인에 내 계정에 대 한 URL은: `http://httpruntime.web703.discountasp.net`합니다.

그림 2에 배포 된 책 검토 사이트를 보여 줍니다. 그 내용을 보고 asp 할인을 참고 합니다. NET의 서버에 `http://httpruntime.web703.discountasp.net`합니다. 이 시점에서 인터넷에 연결 된 모든 사용자 내 웹 사이트를 볼 수 있습니다! 우리는 예상 대로 사이트의 모양과 했을 때 개발 환경에서 테스트 동일 하 게 동작 합니다.

> [!NOTE]
> 잠시가 되도록 응용 프로그램을 볼 때 오류가 발생 하는 경우 올바른 집합 파일을 배포 했습니다. 그런 다음, 오류 메시지 문제에 대 한 한 단서를 표시 하는 경우를 확인 합니다. 그런 다음, 웹 호스트 회사의 기술 지원팀에 설정 하거나 적절 한 포럼에서 질문을 게시 수는 [ASP.NET 포럼](https://forums.asp.net/)합니다.


[![책 검토 사이트를 인터넷에 연결 된 모든 사용자에 게 이제 액세스할 수 있습니다.](deploying-your-site-using-an-ftp-client-vb/_static/image5.png)](deploying-your-site-using-an-ftp-client-vb/_static/image4.png)

**그림 2**: 인터넷에 연결 된 모든 사용자에 게 책 검토 사이트의는 이제 액세스할 수 있는 ([전체 크기 이미지를 보려면 클릭](deploying-your-site-using-an-ftp-client-vb/_static/image6.png))


## <a name="deploying-the-book-review-web-site-project"></a>책 검토 웹 사이트 프로젝트 배포

되에서 컴파일된 어셈블리가 BookReviewsWSP 웹 사이트 프로젝트와 같은 자동 컴파일을 사용 하는 ASP.NET 응용 프로그램을 배포 하는 경우는 `Bin` 폴더입니다. 결과적으로, 웹 응용 프로그램의 소스 코드 파일을 프로덕션 환경에 배포 되어야 합니다. 이 프로세스를 살펴보겠습니다.

대로 웹 응용 프로그램 프로젝트와 함께 첫 번째 빌드 배포 하기 전에 응용 프로그램에는 것이 좋습니다. 웹 사이트 프로젝트를 빌드하는 어셈블리를 만들지 않습니다, 하는 동안 페이지의 모든 컴파일 타임 오류에 대 한 확인지 않습니다. 이러한 오류를 지금 찾기의 상태를 대신를 검색할 사이트 방문자가 있는!

성공적으로 프로젝트를 빌드한 후 웹 호스트 공급자에서 루트 웹 사이트 폴더에 다음 파일을 복사 하 여 FTP 클라이언트를 사용 합니다. 프로덕션 환경에서 해당 폴더 구조를 생성 해야 합니다.

> [!NOTE]
> 프로젝트는 하지만 BookReviewsWSP 프로젝트 배포를 시도 하려는 BookReviewsWAP를 이미 배포한 경우 먼저 BookReviewsWAP를 배포 하는 경우 업로드 된 웹 서버에서 파일을 모두 삭제 하 고 BookReviewsWSP에 대 한 파일을 배포 합니다.


- `~/Default.aspx`
- `~/Default.aspx.vb`
- `~/About.aspx`
- `~/About.aspx.vb`
- `~/Site.master`
- `~/Site.master.vb`
- `~/Web.config`
- `~/Web.sitemap`
- 전체 내용을 `Styles` 폴더
- 전체 내용을 `Images` 폴더 (및 그 하위 폴더 `BookCovers`)
- `~/App_Code/BasePage.vb`
- `~/Fiction/Default.aspx`
- `~/Fiction/Default.aspx.vb`
- `~/Fiction/Blaze.aspx`
- `~/Fiction/Blaze.aspx.vb`
- `~/Tech/Default.aspx`
- `~/Tech/Default.aspx.vb`
- `~/Tech/CYOW.aspx`
- `~/Tech/CYOW.aspx.vb`
- `~/Tech/TYASP35.aspx`
- `~/Tech/TYASP35.aspx.vb`

그림 3은 필요한 파일을 복사한 후 FileZilla를 나타냅니다. ASP.NET 소스와 같은 코드 파일을 볼 수 있듯이 `About.aspx.vb`, 코드 파일에서 자동를 사용 하는 경우 배포 해야 하기 때문에 로컬 컴퓨터 (개발 환경)와 웹 호스트 공급자 (프로덕션 환경)에 컴파일입니다.


[![FTP 클라이언트를 사용 하 여 웹 호스트 공급자에서 웹 서버에 바탕 화면에서 필요한 파일을 복사](deploying-your-site-using-an-ftp-client-vb/_static/image8.png)](deploying-your-site-using-an-ftp-client-vb/_static/image7.png)

**그림 3**: FTP 클라이언트를 사용 하 여 데스크톱에서 웹 호스트 공급자에서 웹 서버에 필요한 파일을 복사 ([전체 크기 이미지를 보려면 클릭](deploying-your-site-using-an-ftp-client-vb/_static/image9.png))


사용자 환경이 응용 프로그램의 컴파일 모델의 영향을 받지 않습니다. 같은 ASP.NET 페이지 액세스할 수 있으며 모양 및 웹 사이트를 웹 응용 프로그램 프로젝트 모델이 나 웹 사이트 프로젝트 모델을 사용 하 여 만들었는지 여부를 동일 하 게 동작 합니다.

## <a name="updating-a-web-application-on-production"></a>프로덕션에 있는 웹 응용 프로그램 업데이트

웹 응용 프로그램 개발 및 배포 일회성 프로세스 하지 않습니다. 예를 들어 우수 웹 사이트를 만들 때 다양 한 페이지를 작성 했으며 개인용 컴퓨터 (개발 환경) 내에서 해당 코드를 작성 합니다. 특정 안정적인 상태에 도달한 후 I 배포 내 응용 프로그램과 다른 사이트를 방문 하 고 내 리뷰 수 있도록 합니다. 하지만 배포 내 개발이이 사이트에서의 끝을 표시 하지 않습니다. 더 많은 책 검토를 추가 또는 속도 설명서 내 방문자를 허용 하는 등의 새로운 기능을 구현 하거나 자신의 의견 남길 수 있습니다 I. 이러한 기능 향상은 개발 환경에서 개발할 수 및 완료 되 면 배포 해야 합니다. 개발 및 배포, 따라서 순환 됩니다. 응용 프로그램을 개발 하 고 배포 합니다. 사이트가 실행 되는 동안 프로덕션 환경에서 새 기능을 추가 및 버그 다시 응용 프로그램 배포 필요로 하는 시간에 따라 수정 됩니다. 등에 등입니다.

예상 대로, 새로운 기능과 변경 된 파일을 복사 해야 하는 웹 응용 프로그램을 다시 배포 하는 경우. 변경 되지 않은 페이지를 다시 배포 하지 않아도 없거나 서버 또는 클라이언트 쪽 지원 파일 (이 작업에 나쁜 영향을 미치지 있지만).

> [!NOTE]
> 프로젝트에 새 ASP.NET 페이지를 추가 또는 관련 된 코드를 변경할 때마다 할 경우에 어셈블리를 업데이트 하는 프로젝트를 다시 작성은 명시적 컴파일을 사용 하 여 때 염두에 한 가지는 `Bin` 폴더입니다. 따라서 다른 새로운 기능과 업데이트 된 콘텐츠) (함께 프로덕션에 있는 웹 응용 프로그램을 업데이트할 때 프로덕션 환경에이 업데이트 된 어셈블리를 복사 해야 합니다.


또한 이해 하 고를 변경 하는 `Web.config` 또는 파일에는 `Bin` 디렉터리 중지 하 고 웹 사이트의 응용 프로그램 풀을 다시 시작 합니다. 사용 하 여 세션 상태가 저장 되는 경우는 `InProc` 모드 (기본값) 다음 사이트의 방문자 이러한 키 파일은 수정 될 때마다 자신의 세션 상태를 잃게 됩니다. 이 문제를 방지 하려면 사용 하 여 세션을 저장할 것 고려해 보십시오.는 `StateServer` 또는 `SQLServer` 모드입니다. 에 대 한 자세한 내용은이 항목 [세션 상태 모드](https://msdn.microsoft.com/library/ms178586.aspx)합니다.

마지막으로, 응용 프로그램을 다시 배포할 수를 사용 하는 아무 곳 이나 몇 초에서 프로덕션 환경에 복사 해야 하는 파일의 크기와 수에 따라 몇 분 정도 염두에 둬야 합니다. 이 시간 동안 오류 또는 부적절 한 동작 해당 사이트를 방문 하는 사용자가 발생할 수 있습니다. "기능을 해제" 전체 응용 프로그램 페이지를 추가 하 여 `App_Offline.htm` 사용자에 게 설명 하는 응용 프로그램의 루트 디렉터리를 사이트 유지 관리 키나 다운 되 고 됩니다 백업 곧 수 있습니다. 경우는 `App_Offline.htm` 파일이 있는지, ASP.NET 런타임이 해당 페이지에 들어오는 모든 요청을 리디렉션합니다.

## <a name="summary"></a>요약

웹 응용 프로그램을 배포 하려면 개발 환경에서 프로덕션 환경에 필요한 파일을 복사 해야 합니다. 가장 일반적인 방법은 네트워크를 통해 파일이 전송 됩니다는 FTP 파일 전송 프로토콜 (), 이며 대부분의 웹 호스트 공급자는 웹 서버에 대 한 FTP 액세스를 지원 합니다. 이 자습서에서는 웹 서버에 필요한 파일을 배포 하는 FTP 클라이언트를 사용 하는 방법에 살펴보았습니다. 배포 된 후 웹 사이트 방문할 수 누구나 연결 인터넷에!

만족도 매우 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [응용 프로그램\_Offline.htm 및 해결 "IE 친숙 한" 오류"기능](https://weblogs.asp.net/scottgu/App_5F00_Offline.htm-and-working-around-the-_2200_IE-Friendly-Errors_2200_-feature)
- [세션 상태 모드](https://msdn.microsoft.com/library/ms178586.aspx)

>[!div class="step-by-step"]
[이전](determining-what-files-need-to-be-deployed-vb.md)
[다음](deploying-your-site-using-visual-studio-vb.md)
