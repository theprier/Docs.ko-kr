---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs
title: IIS와 ASP.NET 개발 서버 (C#) 간의 차이점을 핵심 | Microsoft Docs
author: rick-anderson
description: ASP.NET 응용 프로그램을 로컬로 테스트 하는 경우에 ASP.NET 개발 웹 서버를 사용 하는 것이 경우가 있습니다. 그러나 프로덕션 웹 사이트는 가장 가능성이 높은 pow...
ms.author: riande
ms.date: 04/01/2009
ms.assetid: 13a5a423-9235-4dde-b408-2fd10f791d63
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs
msc.type: authoredcontent
ms.openlocfilehash: 19ca40374f97d59cac4f1677f886f3e48eab7b67
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41837848"
---
<a name="core-differences-between-iis-and-the-aspnet-development-server-c"></a>IIS와 ASP.NET 개발 서버 (C#) 간의 주요 차이점
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/4/5/F/45F815EC-8B0E-46D3-9FB8-2DC015CCA306/ASPNET_Hosting_Tutorial_06_CS.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial06_WebServerDiff_cs.pdf)

> ASP.NET 응용 프로그램을 로컬로 테스트 하는 경우에 ASP.NET 개발 웹 서버를 사용 하는 것이 경우가 있습니다. 그러나 프로덕션 웹 사이트는 가장 가능성이 높은 전원이 IIS입니다. 이러한 웹 서버 요청을 처리 하는 방법의 몇 가지 차이점 있으며 이러한 차이점에는 중요 한 문제가 있을 수 있습니다. 이 자습서에서는 몇 가지 더 밀접 차이점을 살펴봅니다.


## <a name="introduction"></a>소개

사용자가 ASP.NET 응용 프로그램을 방문할 때마다 자신의 브라우저는 웹 사이트에 요청을 보냅니다. 요청 생성 하 고 요청된 된 리소스에 대 한 콘텐츠를 반환 합니다. ASP.NET 런타임이 사용 하 여 조정 하는 웹 서버 소프트웨어에 의해 선택 됩니다. 합니다[**있습니까** 인터넷 **합니까** 내용은 **S** ervices (IIS)](http://en.wikipedia.org/wiki/Internet_Information_Services) 는 일반적인 인터넷 기반 기능을 제공 하는 서비스 제품군입니다 Windows 서버입니다. IIS는 프로덕션 환경;에서 ASP.NET 응용 프로그램에 대 한 가장 일반적으로 사용 되는 웹 서버 웹 호스트 공급자를 통해 ASP.NET 응용 프로그램을 제공 하는 데 사용 되는 웹 서버 소프트웨어 가능성이 높습니다. IIS 사용할 수도 있습니다 개발 환경에서 웹 서버 소프트웨어 있지만 이렇게 하려면 IIS를 설치 하 고 올바르게 구성 합니다.


ASP.NET Development Server는 개발 환경 위한 대체 웹 서버 옵션 와 함께 제공 되 고 Visual Studio에 통합 됩니다. IIS를 사용 하도록 웹 응용 프로그램에서 구성한 경우가 아니면 ASP.NET Development Server는 자동으로 시작 되 고 처음으로 Visual Studio 내에서 웹 페이지를 방문 하면 웹 서버로 사용 합니다. 데모 웹 응용 프로그램에서 다시 만든 합니다 [ *결정 파일 필요한 배포할* ](determining-what-files-need-to-be-deployed-cs.md) 자습서 된 IIS를 사용 하도록 구성 되지 않은 두 파일 시스템 기반 웹 응용 프로그램. 따라서 Visual Studio 내에서 이러한 웹 사이트 중 하나를 방문할 때 ASP.NET Development Server 사용 됩니다.

완벽 한 환경에서 개발 및 프로덕션 환경은 동일 합니다. 그러나 이전 자습서에서 설명한 대로 드물지 않습니다 서로 다른 구성 설정을 갖도록 환경에 대 한 합니다. 다른 웹 서버 소프트웨어를 사용 하 여 환경에서 응용 프로그램을 배포할 때 고려해 야 하는 다른 변수를 추가 합니다. 이 자습서에서는 IIS와 ASP.NET 개발 서버 간의 주요 차이점을 설명합니다. 이러한 차이로 인해 온전 하 게 개발 환경에서 실행 되는 코드의 예외를 throw 하거나 프로덕션 환경에서 실행할 때 다르게 동작 있는 경우도 있습니다.

## <a name="security-context-differences"></a>보안 컨텍스트 차이점

한 들어오는 요청을 처리 하는 웹 서버 소프트웨어 때마다 해당 요청을 특정 보안 컨텍스트를 사용 하 여 연결 합니다. 이 보안 컨텍스트 정보는 요청에서 허용 되는 작업을 확인 하려면 운영 체제에서 사용 됩니다. 예를 들어, ASP.NET 페이지 파일 디스크에 일부 메시지를 기록 하는 코드를 포함할 수 있습니다. 오류 없이 실행 되도록이 ASP.NET 페이지에 대 한 순서로 보안 컨텍스트가 적절 한 파일 시스템 수준 권한, 즉 해당 파일에 대 한 권한을 작성 있어야 합니다.

ASP.NET Development Server는 현재 로그온된 한 사용자의 보안 컨텍스트를 사용 하 여 들어오는 요청을 연결합니다. 관리자 권한으로 바탕 화면에 로그온 하는 경우 ASP.NET Development Server에서 제공 하는 ASP.NET 페이지 관리자로 동일한 액세스 권한을 해야 합니다. 그러나 IIS에서 처리 하는 ASP.NET 요청은 특정 컴퓨터 계정과 연결 됩니다. 웹 호스트 공급자 각 고객에 대 한 고유한 계정을 구성할 수 있을 수 있지만 기본적으로 네트워크 서비스 컴퓨터 계정은 IIS 6 및 7 버전에서 사용 됩니다. 게다가 웹 호스트 공급자에이 컴퓨터 계정에 제한 된 권한을 제공 합니다. 결과 개발 환경에서 오류 없이 실행 되지만 프로덕션 환경에서 호스트 되는 경우 권한 부여와 관련 된 예외를 생성 하는 웹 페이지가 있는 경우

사용자가 가장 최근 날짜와 시간을 저장 하는 디스크에 파일을 만드는 서 리뷰 웹 사이트의 페이지를 만든 경우 작업에서 이러한 종류의 오류를 표시할 볼를 *설명 직접 ASP.NET 3.5 24 시간 동안에서* 검토 합니다. 자습서에 따라 엽니다는 `~/Tech/TYASP35.aspx` 페이지는 다음 코드를 추가 하는 `Page_Load` 이벤트 처리기:

[!code-csharp[Main](core-differences-between-iis-and-the-asp-net-development-server-cs/samples/sample1.cs)]

> [!NOTE]
> 합니다 [ `File.WriteAllText` 메서드](https://msdn.microsoft.com/library/system.io.file.writealltext.aspx) 존재 하지 않는 경우 다음에 지정된 된 콘텐츠를 씁니다 새 파일을 만듭니다. 파일이 이미 있는 경우 기존 내용을 덮어씁니다.


다음을 방문 합니다 *가르치는 직접 ASP.NET 3.5 24 시간 동안에서* ASP.NET Development Server를 사용 하 여 개발 환경에서 책 검토 페이지. 로그인을 만든다고 가정 만들기 및 웹에서 텍스트 파일을 수정 하기 위한 권한이 있는 계정 사용 하 여 컴퓨터에 응용 프로그램의 루트 디렉터리는 서적 검토, 이전과 동일 하 게 보이지만 때마다 페이지를 방문한 사용자의 날짜와 시간  IP 주소에 저장 됩니다는 `LastTYASP35Access.txt` 파일입니다. 이 파일에 브라우저를 가리키면 그림 1에 나와 비슷한 오류 메시지가 표시 됩니다.


[![텍스트 파일에 마지막 날짜 및 시간 서적 검토 방문한 적이](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image2.png)](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image1.png)

**그림 1**: 텍스트 파일에 마지막 날짜 및 시간 서적 검토를 열어 보 았 ([큰 이미지를 보려면 클릭](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image3.png))


프로덕션 웹 응용 프로그램을 배포 하 고 다음 호스팅된를 방문 *가르치는 직접 ASP.NET 3.5 24 시간 동안에서* 책 검토 페이지입니다. 이 시점에서 하거나 책 검토 페이지 normal 또는 그림 2와 같은 오류 메시지가 표시 됩니다. 일부 웹 호스트 공급자에는 경우 페이지는 오류 없이 작동 하는 익명 ASP.NET 컴퓨터 계정에 쓰기 권한을 부여 합니다. 그러나 웹 호스트 공급자에 익명 계정에 대 한 쓰기 액세스를 금지 하는 경우는 [ `UnauthorizedAccessException` 예외](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx) 발생할 때를 `TYASP35.aspx` 페이지에서 현재 날짜 및 시간을 작성 하려고는 `LastTYASP35Access.txt` 파일입니다.


[![IIS에서 사용 하는 기본 컴퓨터 계정에는 파일 시스템에 쓸 수 있는 권한이 없는 합니다.](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image5.png)](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image4.png)

**그림 2**:의 기본 컴퓨터 계정에서 사용 하는 IIS에 있는 권한이 아닌 파일 시스템에 쓰기 ([큰 이미지를 보려면 클릭](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image6.png))


좋은 소식은 대부분의 웹 호스트 공급자 일종의 웹 사이트의 파일 시스템 사용 권한을 지정할 수 있는 권한 도구는입니다. 루트 디렉터리에 익명 ASP.NET 계정 쓰기 액세스 권한을 부여 하 고 책 검토 페이지를 다시 검토 합니다. (필요한 경우 웹 호스트 공급자에 문의 기본 ASP.NET 계정에 대 한 쓰기 권한을 부여 하는 방법에.) 오류 없이 페이지가 로드 해야 하는이 시간 및 `LastTYASP35Access.txt` 파일은 성공적으로 생성 되어야 합니다.

수행 떨어진 같습니다는 있기 때문에 IIS 이외의 다른 보안 컨텍스트에서 작동 ASP.NET Development Server는 읽기 또는 쓰기 파일 시스템에 ASP.NET 페이지에서 읽기 또는 Windows 이벤트 로그에 쓰기 또는 읽기 또는 쓰기를 Windows에  레지스트리는 개발에 대 한 예상 대로 작동 하지만 프로덕션에 예외를 생성 합니다. 웹 응용 프로그램을 빌드하는 공유 웹 호스팅 환경에 배포 됩니다, 경우 읽기 하지 않거나 이벤트 로그 또는 Windows 레지스트리에 작성 합니다. 참고에서 읽어오거나 파일 시스템에 프로덕션 환경에서 해당 폴더에 대 한 권한이 쓰고 읽기 권한을 부여 해야 할 수도 있는 모든 ASP.NET 페이지의 걸립니다.

## <a name="differences-on-serving-static-content"></a>정적 콘텐츠 지원의 차이점

IIS와 ASP.NET 개발 서버 간의 또 다른 주요 차이점은 정적 콘텐츠에 대 한 요청 처리 방법을 ASP.NET 페이지, 이미지 또는 JavaScript 파일을 ASP.NET Development Server에 저장 되는 모든 요청은 ASP.NET 런타임에 의해 처리 됩니다. 기본적으로 IIS만 호출 ASP.NET 런타임은 ASP.NET 리소스의 경우 ASP.NET 웹 페이지, 웹 서비스 등과 같은 요청이 들어올 때 합니다. -이미지, CSS, JavaScript 파일, PDF 파일, ZIP 파일 파일과 같은-정적 콘텐츠에 대 한 요청은 ASP.NET 런타임의 개입 없이도 IIS에서 검색 됩니다. (해당 정적 콘텐츠를 제공 하는 경우 ASP.NET 런타임은 작업 하려면 IIS 명령 할 수도 있습니다; 자세한 내용은이 자습서에서는 "수행 폼 기반 인증 및 IIS 7 사용 하 여 정적 파일에 대 한 URL 인증" 섹션을 참조 하세요.)

ASP.NET 런타임은 다양 한 (요청자를 식별) 하는 인증 및 권한 부여 (요청자에 게 요청 된 콘텐츠를 볼 수 있는 권한이 있으면 확인)를 비롯 하 여 요청 된 콘텐츠를 생성 하는 단계를 수행 합니다. 인증의 인기 있는 폼이 *폼 기반 인증*, 웹 페이지에서 텍스트 상자에 일반적으로 사용자 이름 및 암호-자격 증명을 입력 하 여 식별 되는 사용자의 합니다. 자격 증명 유효성 검사 시 웹 사이트는 다음과 같이 저장 됩니다.는 *인증 티켓* 웹 사이트에 모든 후속 요청을 사용 하 여 전송 되 고 사용자 인증을 위해 사용 되는 사용자의 브라우저에서 쿠키입니다. 지정할 수는 또한 *URL 권한 부여* 사용자 지정 하는 규칙 수 또는 특정 폴더에 액세스할 수 없습니다. 많은 ASP.NET 웹 사이트 사용자 계정을 지원 하 고 인증 된 사용자 또는 특정 역할에 속하는 사용자에 게 액세스할 수 있는 사이트의 부분을 정의 하 폼 기반 인증 및 권한 부여 URL 사용 합니다.

> [!NOTE]
> ASP의 철저 한 검사 합니다. NET의 폼 기반 인증, URL 권한 부여 및 기타 사용자 계정 관련 기능을 확인 수 내 [웹 사이트 보안 자습서](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)합니다.


폼 기반 인증을 사용 하 여 사용자 계정을 지 원하는 폴더, URL 권한 부여를 사용 하 여 인증 된 사용자만 사용할 수 있도록 구성 되어 있고 웹 사이트를 고려해 야 합니다. 이 폴더에 ASP.NET 페이지를 PDF 파일 및 의도 임을 인증 된 사용자만 이러한 PDF 파일을 볼 수 있습니다 가정해 보겠습니다.

방문자가 직접 자신의 브라우저의 주소 표시줄에서에서 URL을 입력 하 여이 PDF 파일 중 하나를 보려고 할 경우 어떻게 되나요? 를 찾으려면 보겠습니다도 서 리뷰 사이트에 새 폴더를 만들고, 일부 PDF 파일을 추가 및 익명 사용자가이 폴더 방문 하지 못하게 하려면 URL 권한 부여를 사용 하도록 사이트 구성 데모 응용 프로그램을 다운로드 하는 경우 표시 폴더가 만들어졌는지 `PrivateDocs` 에서 PDF를 추가 하 고 내 [웹 사이트 보안 자습서](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md) (어떻게 맞춤!). 합니다 `PrivateDocs` 폴더를 `Web.config` 익명 사용자를 거부 하려면 URL 권한 부여 규칙을 지정 하는 파일:

[!code-xml[Main](core-differences-between-iis-and-the-asp-net-development-server-cs/samples/sample2.xml)]

마지막으로 업데이트 하 여 폼 기반 인증을 사용 하도록 웹 응용 프로그램을 구성 합니다 `Web.config` 루트 디렉터리에 파일 대체:

[!code-xml[Main](core-differences-between-iis-and-the-asp-net-development-server-cs/samples/sample3.xml)]

바꿀 대상:

[!code-xml[Main](core-differences-between-iis-and-the-asp-net-development-server-cs/samples/sample4.xml)]

ASP.NET Development Server를 사용 하 여 사이트를 방문 하 고 브라우저의 주소 표시줄에서 PDF 파일 중 하나를 직접 URL을 입력 합니다. URL과 비슷할이 자습서를 사용 하 여 연결 된 웹 사이트 다운로드 한 경우: `http://localhost:portNumber/PrivateDocs/aspnet_tutorial01_Basics_vb.pdf`

주소 표시줄에이 URL을 입력 하면 해당 브라우저에서 파일에 대 한 ASP.NET 개발 서버는 요청을 보내야 합니다. ASP.NET Development Server는 처리를 위해 ASP.NET 런타임에서 요청 넘깁니다. 에서는 아직 로그인 하지 않은 것 때문에 합니다 `Web.config` 에 `PrivateDocs` 폴더는 익명 액세스를 거부 하도록 구성 된, ASP.NET 런타임이 자동으로 우리를 로그인 페이지로 리디렉션합니다, `Login.aspx` (그림 3 참조). 사용자를 로그인 페이지로 리디렉션, ASP.NET에 포함 됩니다는 `ReturnUrl` 보려는 사용자가 하려는 페이지를 나타내는 쿼리 문자열 매개 변수입니다. 사용자를 성공적으로 로그인 한 후이 페이지를 반환할 수 있습니다.


[![권한이 없는 사용자가 자동으로 로그인 페이지로 리디렉션됩니다.](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image8.png)](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image7.png)

**그림 3**: 권한이 없는 사용자가 자동으로 로그인 페이지로 리디렉션됩니다 ([큰 이미지를 보려면 클릭](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image9.png))


이제 프로덕션에서이 동작은 확인해 보겠습니다. 응용 프로그램을 배포 하 고 직접 URL에 Pdf 중 하나를 입력 합니다 `PrivateDocs` 프로덕션 환경에서 폴더입니다. 이 파일에 대 한 IIS 요청을 보낼 브라우저 라는 메시지가 표시 됩니다. IIS 정적 파일 요청 때문에 검색 하 고 ASP.NET 런타임에서 호출 하지 않고 파일을 반환 합니다. 결과적으로, 했습니다 없는 URL 권한 부여 확인 수행 화면이 개인 PDF의 내용을 파일에 직접 URL을 아는 사람에 게 액세스할 수 있습니다.


[![익명 사용자에 게 파일에 직접 URL을 입력 하 여 개인 PDF 파일을 다운로드할 수 있습니다.](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image11.png)](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image10.png)

**그림 4**: 익명 사용자가 다운로드할 수는 개인 PDF 파일에서 입력 직접 URL 파일 ([큰 이미지를 보려면 클릭](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image12.png))


### <a name="performing-forms-based-authentication-and-url-authentication-on-static-files-with-iis-7"></a>IIS 7 사용 하 여 정적 파일에서 폼 기반 인증 및 URL 인증을 수행합니다.

몇 가지 방법으로 권한 없는 사용자 로부터 정적 콘텐츠를 보호 하는 데 사용할 수 있습니다. IIS 7을 도입 합니다 *통합된 파이프라인*, ASP.NET 런타임의 워크플로 사용 하 여 IIS의 워크플로 결혼는. 간단히 말해 ASP.NET 런타임의 인증 및 권한 부여 모듈 (PDF 파일과 같은 정적 콘텐츠 포함) 들어오는 모든 요청을 호출 하는 IIS를 지시할 수 있습니다. 통합된 파이프라인을 사용 하도록 웹 사이트를 구성 하는 방법을 알아보려면 웹 호스트 공급자에 게 문의 합니다.

통합된 파이프라인 추가 다음 태그를 사용 하도록 IIS를 구성 했으면는 `Web.config` 루트 디렉터리에 파일:

[!code-xml[Main](core-differences-between-iis-and-the-asp-net-development-server-cs/samples/sample5.xml)]

이 태그는 ASP.NET 기반 인증 및 권한 부여 모듈을 사용 하도록 IIS 7을 지시 합니다. 다시 응용 프로그램을 배포 하 고 다시 방문 하 여 PDF 파일입니다. IIS에서 요청을 처리 하는 경우이 시간 제공 ASP.NET 런타임의 인증 및 권한 부여 논리 요청 검사 수입니다. 인증 된 사용자만의 내용을 볼 수 있으므로 `PrivateDocs` 익명 방문자 폴더는 자동으로 로그인 페이지로 리디렉션됩니다. (그림 3을 다시 참조).

> [!NOTE]
> 웹 호스트 공급자는 여전히 IIS 6를 사용 하는 경우 통합된 파이프라인 기능을 사용할 수 없습니다. HTTP 액세스를 금지 하는 폴더에 개인 문서를 배치 하는 한 가지 해결 방법은 (같은 `App_Data`) 한 다음 이러한 문서에 맞도록 페이지를 만듭니다. 이 페이지를 호출할 수 있습니다 `GetPDF.aspx`, 쿼리 문자열 매개 변수를 통해 PDF의 이름을 전달 됩니다. `GetPDF.aspx` 페이지는 먼저 확인 하는 사용자 파일을 볼 수 있는 권한이 고 그렇다면 사용 합니다 [ `Response.WriteFile(filePath)` ](https://msdn.microsoft.com/library/system.web.httpresponse.writefile.aspx) 요청된 된 PDF 파일의 내용을 요청 클라이언트로 다시 보내는 방법. 이 기술은 통합된 파이프라인을 사용 하도록 설정 하지 않은 경우 IIS 7에 대해서도 작동 됩니다.


## <a name="summary"></a>요약

프로덕션 환경에서 웹 응용 프로그램은 Microsoft의 IIS 웹 서버 소프트웨어를 사용 하 여 호스트 됩니다. 그러나 개발 환경에서 응용 프로그램이 호스팅될 수 IIS 또는 ASP.NET Development Server를 사용 하 여 합니다. 이상적으로 동일한 웹 서버 소프트웨어의 조합에 다른 변수를 추가 서로 다른 소프트웨어를 사용 하 여 하기 때문에 두 환경 모두에서 사용 해야 합니다. 그러나 ASP.NET Development Server 사용 편의성 매력적인 선택에서에서 있도록 개발 환경입니다. 좋은 소식은 몇 가지 기본적인 차이가 IIS와 ASP.NET 개발 서버 간의 이러한 차이점을 알고 있다면 있습니다 단계를 수행할 수는 응용 프로그램이 작동 하 고 동일한 기능을 확인 하는 데 방식에 관계 없이 환경입니다.

즐거운 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [Iis 7.0 ASP.NET 통합](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)
- [ASP.NET 포럼 인증을 사용 하 여 모든 유형의 IIS 7에서 콘텐츠를 사용 하 여](https://blogs.iis.net/bills/archive/2007/05/19/using-asp-net-forms-authentication-with-all-types-of-content-with-iis7-video.aspx) (비디오)
- [Visual Web Developer에서 웹 서버](https://msdn.microsoft.com/library/58wxa9w5.aspx)

> [!div class="step-by-step"]
> [이전](common-configuration-differences-between-development-and-production-cs.md)
> [다음](deploying-a-database-cs.md)
