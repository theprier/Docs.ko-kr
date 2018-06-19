---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-vb
title: IIS와 ASP.NET 개발 서버 (VB) 간의 차이 핵심 | Microsoft Docs
author: rick-anderson
description: 로컬 ASP.NET 응용 프로그램을 테스트할 때 ASP.NET 개발 웹 서버를 사용 하는 가능성 됩니다. 그러나 프로덕션 웹 사이트는 가능성이 가장 높은 pow 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/01/2009
ms.topic: article
ms.assetid: 090e9205-52f3-4d72-ae31-44775b8b8421
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-vb
msc.type: authoredcontent
ms.openlocfilehash: 47b1959f9b92d161da0476b274c8154333ad80dc
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30887550"
---
<a name="core-differences-between-iis-and-the-aspnet-development-server-vb"></a>코어 IIS와 ASP.NET 개발 서버 (VB)의 차이점
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/4/5/F/45F815EC-8B0E-46D3-9FB8-2DC015CCA306/ASPNET_Hosting_Tutorial_06_VB.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial06_WebServerDiff_vb.pdf)

> 로컬 ASP.NET 응용 프로그램을 테스트할 때 ASP.NET 개발 웹 서버를 사용 하는 가능성 됩니다. 그러나 프로덕션 웹 사이트는 가능성이 가장 높은 전원이 IIS. 이러한 웹 서버 요청을 처리 하는 방법을 간의 차이 일부 있으며 이러한 차이는 중요 한 문제가 있을 수 있습니다. 이 자습서에서는 몇 가지 더 콘텐츠와 차이 탐색합니다.


## <a name="introduction"></a>소개

사용자가 ASP.NET 응용 프로그램을 방문할 때마다 브라우저가 웹 사이트에 요청을 보냅니다. 협력 합니다. ASP.NET 런타임이 생성 하 고 요청된 된 리소스에 대 한 콘텐츠를 반환 하는 웹 서버 소프트웨어를 해당 요청 선택 합니다. [**I** 인터넷 **I** 내용은 **S** ervices (IIS)](http://en.wikipedia.org/wiki/Internet_Information_Services) 됩니다에 대 한 공통 인터넷 기반 기능을 제공 하는 서비스의 도구 모음 Windows 서버입니다. IIS는; 프로덕션 환경에서 ASP.NET 응용 프로그램에 대 한 가장 일반적으로 사용 되는 웹 서버 것은 대부분 웹 호스트 공급자가 사용 되 고 ASP.NET 응용 프로그램 역할을 웹 서버 소프트웨어입니다. IIS도으로 사용할 수 개발 환경에서 웹 서버 소프트웨어 있지만 이렇게 하려면 IIS를 설치 하 고 올바르게 구성 합니다.


ASP.NET 개발 서버는 개발 환경;에 대 한 다른 웹 서버 옵션 와 함께 제공 하 고 Visual Studio에 통합 합니다. 웹 응용 프로그램을 IIS를 사용 하도록 구성 않은 ASP.NET 개발 서버는 자동으로 시작 하 고 처음으로 Visual Studio 내에서 웹 페이지 방문의 웹 서버로 사용 되는 합니다. 데모 웹 응용 프로그램에서 다시 만든는 [ *결정 어떤 파일 배포 해야 할* ](determining-what-files-need-to-be-deployed-vb.md) 자습서에는 IIS를 사용 하도록 구성 되지 않은 파일 시스템 기반 웹 응용 프로그램 모두 되었습니다. 따라서 Visual Studio 내에서 이러한 웹 사이트 중 하나를 방문할 때 ASP.NET 개발 서버 사용 됩니다.

완벽 한 상황에서는 개발 및 프로덕션 환경 동일한 것입니다. 그러나 이전 자습서에서 설명한 것 처럼는 경우도 많습니다 서로 다른 구성 설정을 유지 하려면 환경에 대 한 합니다. 환경에서 다른 웹 서버 소프트웨어를 사용 하 여 응용 프로그램을 배포할 때 고려해 야 하는 다른 변수를 추가 합니다. 이 자습서에서는 IIS 및 ASP.NET 개발 서버 간의 주요 차이점에 설명 합니다. 이러한 차이로 인해 온전 하 게 개발 환경에서 실행 되는 코드의 예외를 throw 하거나 프로덕션 환경에서 실행 될 때와 다르게 동작 위치 시나리오가 있습니다.

## <a name="security-context-differences"></a>보안 컨텍스트 차이점

들어오는 요청을 처리 하는 웹 서버 소프트웨어 때마다 해당 요청 특정 보안 컨텍스트와 연결 합니다. 이 보안 컨텍스트 정보는 요청에서 허용 하는 동작을 결정 하는 운영 체제에서 사용 됩니다. 예를 들어, ASP.NET 페이지 파일 디스크에 일부 메시지를 기록 하는 코드를 포함할 수 있습니다. 오류 없이 실행 되도록이 ASP.NET 페이지에 대 한 순서로 보안 컨텍스트 적절 한 파일 시스템 수준 사용 권한, 즉 쓰기 해당 파일에 대해 권한이 있어야 합니다.

ASP.NET 개발 서버는 현재 로그온된 한 사용자의 보안 컨텍스트를 들어오는 요청을 연결합니다. 관리자 권한으로 바탕 화면에 로그온 한 경우 ASP.NET 개발 서버에서 제공 하는 ASP.NET 페이지에서 관리자 권한으로 동일한 액세스 권한이 있어야 합니다. 그러나 IIS에서 처리 하는 ASP.NET 요청 특정 컴퓨터 계정과 연결 됩니다. 기본적으로 네트워크 서비스 컴퓨터 계정은 웹 호스트 공급자 수 있는 구성 되어 있지만 고유한 계정을 각 고객에 대 한 IIS 6 및 7. 버전에서 사용 됩니다. 게다가 웹 호스트 공급자 컴퓨터 계정에이에 제한 된 권한을 제공 합니다. 그 결과 개발 환경에서 오류 없이 실행 하지만 프로덕션 환경에서 호스팅되는 경우 권한 부여 관련 예외를 생성 하는 웹 페이지를 할 수도 있습니다.

다른 사람이 가장 최근 날짜와 시간을 저장 하는 디스크에 파일을 만들고 책 검토 웹 사이트의 페이지를 만든 작업에 이러한 종류의 오류를 표시 하려면 볼는 *업무량이 직접 ASP.NET 3.5 24 시간 동안에서* 검토 합니다. 단계를 따르려면 열고는 `~/Tech/TYASP35.aspx` 페이지 및 다음 코드를 추가 하는 `Page_Load` 이벤트 처리기:

[!code-vb[Main](core-differences-between-iis-and-the-asp-net-development-server-vb/samples/sample1.vb)]

> [!NOTE]
> [ `File.WriteAllText` 메서드](https://msdn.microsoft.com/library/system.io.file.writealltext.aspx) 존재 하지 않는 경우 다음 지정된 된 콘텐츠를 씁니다 새 파일을 만듭니다. 파일이 이미 있는 경우 기존 내용을 덮어씁니다.


다음으로 방문는 *업무량이 직접 ASP.NET 3.5 24 시간 동안에서* ASP.NET 개발 서버를 사용 하 여 개발 환경에서 책 검토 페이지. 로그인 되어 있다고 가정할 경우 만들고는 웹에서 텍스트 파일을 수정 하려면 적절 한 권한이 있는 계정 사용 하 여 컴퓨터에 로그온 할 응용 프로그램의 루트 디렉터리는 우수, 이전과 동일 나타나지만 날짜 및 시간과 사용자의 페이지는 때마다 방문  IP 주소에 저장 됩니다는 `LastTYASP35Access.txt` 파일입니다. 이 파일을; 브라우저를 가리키도록 그림 1에 나와 있는 것과 유사한 메시지가 나타납니다.


[![텍스트 파일에 마지막 날짜와 시간에서 우수 개체를 방문한&lt;](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image2.png)](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image1.png)

**그림 1**: 텍스트 파일에 마지막 날짜와 시간에서 우수 개체를 방문한 ([전체 크기 이미지를 보려면 클릭](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image3.png))


프로덕션 환경에 웹 응용 프로그램을 배포 하 고 호스팅된을 방문 *업무량이 직접 ASP.NET 3.5 24 시간 동안에서* 책 검토 페이지. 이 시점에서 하거나 나타납니다 책 검토 페이지 normal 또는 그림 2에 표시 되는 오류 메시지. 일부 웹 호스트 공급자는 경우 페이지는 오류 없이 작동 익명 ASP.NET 컴퓨터 계정에 대 한 쓰기 권한을 부여 합니다. 웹 호스트 공급자가 익명 계정에 대 한 쓰기 액세스를 금지 하는 반면 경우 아니라면 [ `UnauthorizedAccessException` 예외](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx) 발생할 때의 `TYASP35.aspx` 페이지 현재 날짜 및 시간에 쓰려고 시도 `LastTYASP35Access.txt` 파일입니다.


[![IIS에서 사용 되는 기본 컴퓨터 계정에 파일 시스템에 쓸 수 있는 권한이 없는](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image5.png)](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image4.png)

**그림 2**: The 기본 컴퓨터 계정을 사용 하 여 IIS가 있는 권한이 아닌 파일 시스템에 대 한 쓰기를 ([전체 크기 이미지를 보려면 클릭](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image6.png))


다행히도 대부분 웹 호스트 공급자 어떤 종류의 웹 사이트의 파일 시스템 사용 권한을 지정할 수 있는 사용 권한 도구는입니다. 루트 디렉터리에 익명 ASP.NET 계정 쓰기 권한을 부여 하 고 책 검토 페이지를 다시 검토 합니다. (필요한 경우 웹 호스트 공급자에 문의 기본 ASP.NET 계정에 쓰기 권한을 부여 하는 방법에.) 페이지가 오류 없이 로드 해야 하는이 시간 및 `LastTYASP35Access.txt` 파일을 성공적으로 만들 합니다.

가져가기 자리를 비울 다음은 IIS 보다 다른 보안 컨텍스트에서 ASP.NET 개발 서버 작동을 하기 때문에 수 있다는 것을 읽기 또는 쓰기 파일 시스템에는 ASP.NET 페이지가에서 읽기 또는 Windows 이벤트 로그에 쓰기 또는 읽기 또는 쓰기 windows  레지스트리를 개발에서 예상한 대로 작동 하지만 프로덕션에 대 한 예외를 생성 합니다. 웹 응용 프로그램을 빌드하는 공유 웹 호스팅 환경에 배포 됩니다 때 읽을 하지 않거나 이벤트 로그 또는 Windows 레지스트리에 작성 합니다. 또한 주의 읽기 또는 읽기 권한을 부여 하 고 프로덕션 환경에서 해당 폴더에 대 한 권한이 작성 해야 할 수 있습니다 하지만 파일 시스템에 쓰는 경우는 모든 ASP.NET 페이지 합니다.

## <a name="differences-on-serving-static-content"></a>정적 콘텐츠를 서비스에 차이점

IIS 및 ASP.NET 개발 서버 간의 또 다른 주요 차이점은 정적 콘텐츠에 대 한 요청을 처리 하는 방식입니다. ASP.NET 페이지, 이미지 또는 JavaScript 파일에 ASP.NET 개발 서버에 저장 되는 모든 요청은 ASP.NET 런타임에 의해 처리 됩니다. 기본적으로 IIS만 ASP.NET 런타임이 때 호출, ASP.NET 웹 페이지, 웹 서비스 등과 같은 ASP.NET 리소스에 대 한 요청을 제공 합니다. -이미지, CSS 파일, JavaScript 파일, PDF 파일, ZIP 파일 및 like-정적 콘텐츠에 대 한 요청은 ASP.NET 런타임이의 개입 없이도 IIS에 의해 검색 됩니다. (것 IIS 정적 콘텐츠를 처리할 때 ASP.NET 런타임과 함께 작동 하도록 지시할 수 있습니다; 자세한 내용은이 자습서에서는 "공연 폼 기반 인증 및 IIS 7 사용 하 여 정적 파일에서 URL 인증" 섹션을 참조 하십시오.)

ASP.NET 런타임 여러 (요청자 식별) 하는 인증 및 권한 부여 (요청자에 게 요청된 된 콘텐츠를 볼 수 있는 권한을 여부를 확인)를 포함 하 여 요청 된 콘텐츠를 생성 하는 단계를 수행 합니다. 인기 있는 인증 형식은 *폼 기반 인증*에 사용자로 식별 되는 웹 페이지에 텍스트 상자에-일반적으로 사용자 이름 및 암호-자격 증명을 입력 합니다. 자격 증명 유효성 검사 시 웹 사이트를 저장 한 *인증 티켓* 모든 후속 요청에 웹 사이트에 전송 되 고 사용 하는 것은 사용자를 인증 하는 사용자의 브라우저에서 쿠키입니다. 지정할 수는 또한 *URL 권한 부여* 사용자가 지정 하는 규칙 수 또는 특정 폴더에 액세스할 수 없습니다. 대부분의 ASP.NET 웹 사이트 사용자 계정을 지원 하 고 사이트의 특정 역할에 속하는 사용자 또는 인증 된 사용자에 액세스할 수 있는 부분을 정의 하 폼 기반 인증 및 권한 부여 URL 사용 합니다.

> [!NOTE]
> ASP의 철저 한 검사 합니다. NET의 폼 기반 인증, URL 권한 부여 및 기타 사용자 계정 관련 기능을 확인 수 내 [웹 사이트 보안 자습서](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)합니다.


웹 사이트를 폴더, URL 권한 부여를 사용 하 여 인증 된 사용자만 사용할 수 있도록 구성 되어 있고 폼 기반 인증을 사용 하 여 사용자 계정을 지 원하는 것이 좋습니다. 이 폴더에 ASP.NET 페이지 및 PDF 파일 및 의도 임을 하는 인증 된 사용자만 이러한 PDF 파일을 볼 수 한다고 가정 합니다.

방문자가 직접 자신의 브라우저의 주소 표시줄에에서 URL을 입력 하 여 이러한 PDF 파일 중 하나를 보려고 할 경우 어떻게 됩니까? 를 확인 하려면 보겠습니다 책 검토 사이트에서 새 폴더 만들기, 일부 PDF 파일을 추가 및 익명 사용자가이 폴더 방문 하지 못하게 하려면 URL 권한 부여를 사용 하도록 사이트를 구성 합니다. 데모 응용 프로그램을 다운로드 하는 경우 표시 폴더가 만들어졌는지 `PrivateDocs` 에서 PDF 추가 내 [웹 사이트 보안 자습서](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md) (어떻게 적합!). `PrivateDocs` 폴더에 포함 되어는 `Web.config` 익명 사용자의 거부 하려면 URL 권한 부여 규칙을 지정 하는 파일:

[!code-xml[Main](core-differences-between-iis-and-the-asp-net-development-server-vb/samples/sample2.xml)]

루트 디렉터리에 Web.config 파일을 업데이트 하 여 폼 기반 인증을 사용 하도록 웹 응용 프로그램을 구성 했지만 마지막으로, 대체:

[!code-xml[Main](core-differences-between-iis-and-the-asp-net-development-server-vb/samples/sample3.xml)]

바꿀 대상:

[!code-xml[Main](core-differences-between-iis-and-the-asp-net-development-server-vb/samples/sample4.xml)]

ASP.NET 개발 서버를 사용 하 여 사이트를 방문 하 고 브라우저의 주소 표시줄에서 PDF 파일 중 하나를 직접 URL을 입력 합니다. 이 자습서의 URL은 같이 표시와 연결 된 웹 사이트 다운로드 한 경우: `http://localhost:portNumber/PrivateDocs/aspnet_tutorial01_Basics_vb.pdf`

주소 표시줄에이 URL을 입력 하면 해당 브라우저 파일에 대 한 ASP.NET 개발 서버는 요청을 보냅니다. ASP.NET 개발 서버는 요청을 처리를 위해 ASP.NET 런타임 넘깁니다. 에서는 아직 로그인 하지 않은 것 때문에 `Web.config` 에 `PrivateDocs` 폴더 익명 액세스를 거부 하도록 구성 되어, ASP.NET 런타임이 자동으로 리디렉션하여 우리 로그인 페이지로 `Login.aspx` (그림 3 참조). ASP.NET에 포함 되어 사용자 페이지에 있는 로그를 리디렉션하는 경우는 `ReturnUrl` querystring 매개 변수 페이지를 나타내는 사용자를 보려면 시도 했습니다. 이 페이지에는 사용자를 성공적으로 로그인 한 후를 반환할 수 있습니다.


[![권한이 없는 사용자가 자동으로 로그인 페이지로 리디렉션됩니다.](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image8.png)](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image7.png)

**그림 3**: 권한이 없는 사용자가 자동으로 로그인 페이지로 리디렉션됩니다. ([전체 크기 이미지를 보려면 클릭](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image9.png))


이제이 프로덕션에서의 동작 방법을 살펴보겠습니다. 응용 프로그램을 배포 하 고의 Pdf 중 하나를 직접 URL을 입력에서 `PrivateDocs` 프로덕션 환경에는 폴더입니다. 이 메시지는 파일에 대 한 IIS 요청을 보낼 브라우저를 표시 합니다. 정적 파일은 요청 때문에 IIS를 검색 하 고 ASP.NET 런타임이 호출 하지 않고 파일을 반환 합니다. 결과적으로 수행 되어야 합니다; URL 권한 부여 검사 없이 있었습니다. 코드가 개인 PDF의 내용이 파일에 직접 URL을 알고 있는 모든 사람이 액세스할 수 있습니다.


[![익명 사용자가 파일을 직접 URL을 입력 하 여 개인 PDF 파일을 다운로드할 수 있습니다.](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image11.png)](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image10.png)

**그림 4**: 익명 사용자가 다운로드할 수는 개인 PDF 파일에서 입력 직접 URL 파일 ([전체 크기 이미지를 보려면 클릭](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image12.png))


### <a name="performing-forms-based-authentication-and-url-authentication-on-static-files-with-iis-7"></a>IIS 7과 함께 정적 파일에 대해 폼 기반 인증 및 URL 인증 수행

몇 가지 방법 권한 없는 사용자 로부터 정적 콘텐츠를 보호 하는 데 사용할 수 있습니다. IIS 7 도입는 *통합된 파이프라인*, ASP.NET 런타임 워크플로 사용 하 여 IIS의 워크플로 결혼입니다. 간단히 말해, 들어오는 모든 요청 (예: PDF 파일 정적 콘텐츠 포함) ASP.NET 런타임 인증 및 권한 부여 모듈을 호출 하는 IIS를 지시할 수 있습니다. 통합된 파이프라인을 사용 하 여 웹 사이트를 구성 하는 방법을 알아보려면 웹 호스트 공급자에 게 문의 합니다.

IIS가 사용 하도록 구성 되 면 통합된 파이프라인에 다음 태그를 추가 하는 고 `Web.config` 루트 디렉터리에에서 파일:

[!code-xml[Main](core-differences-between-iis-and-the-asp-net-development-server-vb/samples/sample5.xml)]

이 태그는 ASP.NET 기반 인증 및 권한 부여 모듈을 사용 하는 IIS 7을 지시 합니다. 응용 프로그램을 다시 배포 하 고 PDF 파일을 다시 방문. IIS에서 요청을 처리 하는 경우이 시간 제공 ASP.NET 런타임 인증 및 권한 부여 논리 기회를 요청을 검사 합니다. 인증 된 사용자만의 내용을 볼 수 있으므로 `PrivateDocs` 익명 방문자 폴더를 자동으로 로그인 페이지로 리디렉션됩니다. (그림 3을 다시 참조).

> [!NOTE]
> 웹 호스트 공급자는 계속 IIS 6을 사용 하는 경우 통합된 파이프라인 기능을 사용할 수 없습니다. 한 가지 해결 방법은 HTTP 액세스를 금지 하는 폴더에 개인 문서를 저장 하는 (예: `App_Data`) 한 다음 이러한 문서를 처리 하는 페이지를 만듭니다. 이 페이지를 호출할 수 있습니다 `GetPDF.aspx`, 쿼리 문자열 매개 변수를 통해 PDF의 이름을 전달 됩니다. `GetPDF.aspx` 페이지는 사용자가 파일을 볼 수 있으며,이 경우 사용 먼저 확인 됩니다는 [ `Response.WriteFile(filePath)` ](https://msdn.microsoft.com/library/system.web.httpresponse.writefile.aspx) 메서드는 요청 된 PDF 파일의 내용을 요청 클라이언트로 다시 보낼 수 있습니다. 이 기술이 통합된 파이프라인 수 있도록 하지 않은 경우에 IIS 7에 대 한 작동할 것입니다.


## <a name="summary"></a>요약

프로덕션 환경에서 웹 응용 프로그램을 Microsoft의 IIS 웹 서버 소프트웨어를 사용 하 여 호스팅됩니다. 하지만 개발 환경에서 응용 프로그램 호스트할 수는 IIS 또는 ASP.NET 개발 서버를 사용 하 여 합니다. 이상적으로 동일한 웹 서버 소프트웨어를 서로 다른 소프트웨어를 사용 하 여 조합에 또 다른 변수를 추가 하기 때문에 두 환경에서 사용 해야 합니다. 그러나 ASP.NET 개발 서버 사용 편의성 하면 매력적인 선택 개발 환경에서 있습니다. 다행 스럽게도 가지만 몇 가지 근본적인 차이가 IIS와 ASP.NET 개발 서버 간 및 이러한 차이점을 알고 있다면 있습니다 단계를 수행할 수는 응용 프로그램이 작동 하 고 동일한 기능을 수행 하지 확인 하려면 관계 없이 방식으로 환경입니다.

만족도 매우 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [IIS 7.0에서 ASP.NET과 통합](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)
- [ASP.NET 포럼 인증을 사용 하 여 모든 종류의 IIS 7에서 콘텐츠](https://blogs.iis.net/bills/archive/2007/05/19/using-asp-net-forms-authentication-with-all-types-of-content-with-iis7-video.aspx) (비디오)
- [Visual Web Developer에서 웹 서버](https://msdn.microsoft.com/library/58wxa9w5.aspx)

> [!div class="step-by-step"]
> [이전](common-configuration-differences-between-development-and-production-vb.md)
> [다음](deploying-a-database-vb.md)
