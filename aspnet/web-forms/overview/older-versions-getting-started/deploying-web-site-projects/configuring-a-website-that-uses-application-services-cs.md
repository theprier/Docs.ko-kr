---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-a-website-that-uses-application-services-cs
title: 응용 프로그램 서비스 (C#)를 사용 하는 웹 사이트 구성 | Microsoft Docs
author: rick-anderson
description: ASP.NET 버전 2.0 일련의.NET Framework의 일부인 구성 요소 모음인 서비스는 yo 때 역할을 하며 응용 프로그램 서비스를 도입 하는 중...
ms.author: aspnetcontent
ms.date: 04/23/2009
ms.assetid: 1e33d1c6-3f9f-4c26-81e2-2a8f8907bb05
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-a-website-that-uses-application-services-cs
msc.type: authoredcontent
ms.openlocfilehash: 9bbf6d84c3ca25a3476901ec3d7996d5ca197446
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37837654"
---
<a name="configuring-a-website-that-uses-application-services-c"></a>응용 프로그램 서비스 (C#)를 사용 하는 웹 사이트를 구성 합니다.
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/E/6/F/E6FE3A1F-EE3A-4119-989A-33D1A9F6F6DD/ASPNET_Hosting_Tutorial_09_CS.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/C/3/9/C391A649-B357-4A7B-BAA4-48C96871FEA6/aspnet_tutorial09_AppServicesConfig_cs.pdf)

> ASP.NET 버전 2.0에는 일련을의.NET Framework의 일부 이며 웹 응용 프로그램에 풍부한 기능을 추가 하는 데 사용할 수 있는 구성 요소 서비스의 모음으로 사용 하는 응용 프로그램 서비스를 도입 했습니다. 이 자습서는 응용 프로그램 서비스를 사용 하 여 프로덕션 환경에서 웹 사이트를 구성 하는 방법에 살펴봅니다 및 사용자 계정 및 프로덕션 환경에서 역할을 관리 하는 일반적인 문제를 해결 합니다.


## <a name="introduction"></a>소개

ASP.NET 버전 2.0에는 일련의 도입 *응용 프로그램 서비스*,.NET Framework의 일부인 및 문서 블록의 제품군을 서비스로 제공 하는 웹 응용 프로그램에 풍부한 기능을 추가 하는 데 사용할 수 있습니다. 응용 프로그램 서비스는 다음과 같습니다.

- **멤버 자격** -사용자 계정을 만들고 관리 하기 위한 API입니다.
- **역할** -API 사용자 그룹으로 분류 합니다.
- **프로필** -사용자 지정, 사용자 고유의 콘텐츠를 저장 하기 위한 API입니다.
- **사이트 맵** -메뉴 등 이동 경로 탐색 컨트롤을 통해 표시 될 수 있는 계층의 형태로 사이트 s 논리 구조를 정의 하기 위한 API입니다.
- **개인 설정** -사용자 지정 기본 설정에 자주 사용을 유지 관리 하기 위한 API [ *WebParts*](https://msdn.microsoft.com/library/e0s9t4ck.aspx)합니다.
- **상태 모니터링** -API 성능, 보안, 오류 및 실행 중인 웹 응용 프로그램에 대 한 다른 시스템 상태 메트릭을 모니터링 합니다.
  

응용 프로그램 서비스 Api는 특정 구현에 연결 되지 않습니다. 특정 사용 하도록 응용 프로그램 서비스를 지시 하는 대신 *공급자*, 및 해당 공급자는 특정 기술을 사용 하 여 서비스를 구현 합니다. 웹 호스팅 회사에 호스팅된 인터넷 기반 웹 응용 프로그램에 대 한 가장 자주 사용 되는 공급자는 SQL Server 데이터베이스 구현을 사용 하는 해당 공급자입니다. 예를 들어를 `SqlMembershipProvider` 는 Microsoft SQL Server 데이터베이스의 사용자 계정 정보를 저장 하는 멤버 자격 API에 대 한 공급자입니다.

응용 프로그램 서비스 및 SQL Server 공급자를 사용 하 여 응용 프로그램을 배포 하는 경우 몇 가지 과제를 추가 합니다. 먼저 응용 프로그램 서비스 데이터베이스 개체를 개발 및 프로덕션 데이터베이스에서 제대로 만들어지지 고 적절 하 게 초기화 해야 합니다. 되어야 하는 중요 한 구성 설정이 있습니다.

> [!NOTE]
> Api를 사용 하 여 설계 된 응용 프로그램 서비스를 [ *공급자 모델*](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx), 구현 세부 정보를 런타임에 제공 API가 허용 하는 디자인 패턴입니다. .NET Framework를 사용할 수 있는와 같은 응용 프로그램 서비스 공급자 수와 함께 제공 되는 `SqlMembershipProvider` 및 `SqlRoleProvider`, 멤버 자격 공급자는 및 SQL Server를 사용 하는 역할 Api 데이터베이스 구현입니다. 만들 수도 있습니다 및 플러그 인을 사용자 지정 공급자입니다. 도 서 리뷰 웹 응용 프로그램이 이미 사이트 맵 API에 대 한 사용자 지정 공급자를 포함 하는 사실 (`ReviewSiteMapProvider`), 사이트 맵 데이터에서 생성 되는 `Genres` 및 `Books` 데이터베이스의 테이블입니다.


이 자습서는 멤버 자격 및 역할 Api를 사용 하 여도 서 리뷰 웹 응용 프로그램을 확장 하는 방법을 보는 것으로 시작 합니다. 그런 다음 배포 응용 프로그램 서비스를 사용 하 여 SQL Server 데이터베이스 구현에서는 사용자 계정 및 프로덕션 환경에서 역할을 관리 하는 일반적인 문제를 해결 하 여 완료 하는 웹 응용 프로그램을 안내 합니다.

## <a name="updates-to-the-book-reviews-application"></a>책 검토 응용 프로그램에 대 한 업데이트

지난 서평 웹 응용 프로그램은 데이터 기반 동적 웹 응용 프로그램에 정적 웹 사이트에서 업데이트 된 자습서는 장르 및 검토를 관리 하기 위한 관리 페이지의 집합을 사용 하 여 완료 합니다. 그러나이 관리 섹션에서는 현재 보호 되지 않습니다-사용자 관리 페이지 URL을 알고 있습니다 (또는 추측)는 수에가지고 안심할 및 만들기, 편집 또는 사이트에서의 검토를 삭제 합니다. 웹 사이트의 특정 부분을 보호 하기 위해 사용자 계정을 구현 하 여 다음 URL 권한 부여 규칙을 사용 하 여 특정 사용자 또는 역할에 대 한 액세스를 제한 하는 일반적인 방법은입니다. 이 자습서를 사용 하 여 다운로드할 수 있는 서 리뷰 웹 응용 프로그램 사용자 계정 및 역할을 지원합니다. 여러 개 정의 된 역할 이름이 Admin 및이 역할의 사용자만 관리 페이지에 액세스할 수 있습니다.

> [!NOTE]
> I ve도 서 리뷰 웹 응용 프로그램에서 3 개의 사용자 계정을 만든: Scott 고 Jisun, Alice입니다. 모든 세 명의 동일한 암호: **암호!** Scott 및 Jisun 관리자 역할이 있는, alice가 아닙니다. 사이트가 아닌 관리 페이지는 익명 사용자에 게 여전히 액세스할 수 있습니다. 즉, 필요가 없습니다를 관리 하려는 경우가 아니면 사이트를 방문 하 여 로그인 관리자 역할의 사용자로 로그인 해야 합니다는 경우.


도 서 리뷰 응용 프로그램 s 마스터 페이지 인증 및 익명 사용자에 대 한 다른 사용자 인터페이스를 포함 하도록 업데이트 되었습니다. 익명 사용자가 사이트를 방문할 경우 오른쪽 위 모서리의 로그인 링크를 확인 합니다. 인증된 된 사용자 확인 메시지를 ", 환영 *username*!" 및 로그 아웃에 대 한 링크입니다. 여기서 s는 로그인 페이지에도 (`~/Login.aspx`), 방문자를 인증 하기 위한 사용자 인터페이스 및 논리를 제공 하는 로그인 웹 컨트롤을 포함 하는 합니다. 관리자만 새 계정을 만들 수 있습니다. (페이지에서 사용자 계정을 만들고 관리에 대 한 가지는 `~/Admin` 폴더입니다.)

### <a name="configuring-the-membership-and-roles-apis"></a>멤버 자격 및 역할 Api 구성

도 서 리뷰 웹 응용 프로그램 사용자 계정을 지원 하 고 해당 사용자 역할 (즉, 관리자 역할)에 그룹 멤버 자격 및 역할 Api를 사용 합니다. 합니다 `SqlMembershipProvider` 및 `SqlRoleProvider` 공급자 클래스는 SQL Server 데이터베이스에 계정 및 역할 정보를 저장 하려고 하므로 사용 됩니다.

> [!NOTE]
> 멤버 자격 및 역할 Api를 지원 하도록 웹 응용 프로그램을 구성 하는 자세한 검사 되도록이 자습서를 사용 하는 것이 없습니다. 에 대 한 철저 한 이러한 Api 및 사용 하 여 웹 사이트를 구성 하는 데 필요한 단계를 읽어보세요 내 [ *웹 사이트 보안 자습서*](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)합니다.


SQL Server 데이터베이스를 사용 하 여 응용 프로그램 서비스를 사용 하려면 먼저 사용자 계정을 만들려는 데이터베이스에 이러한 공급자에서 사용 하는 데이터베이스 개체 및 저장 된 역할 정보를 추가 해야 합니다. 이러한 필수 데이터베이스 개체는 다양 한 테이블, 뷰 및 저장된 프로시저를 포함합니다. 지정이 고, 그렇지 않은 경우는 `SqlMembershipProvider` 및 `SqlRoleProvider` 라는 SQL Server Express Edition 데이터베이스를 사용 하는 공급자 클래스 `ASPNETDB` 응용 프로그램에서 있는 `App_Data` 폴더에 자동으로 만들어집니다 이러한 데이터베이스 존재 하지 않는 경우 런타임 시 이러한 공급자가 필요한 데이터베이스 개체입니다.

가능 하다 고 만들려면 일반적으로 이상적인 응용 프로그램 서비스 웹 사이트의 응용 프로그램별 데이터가 저장 된 동일한 데이터베이스의 데이터베이스 개체. 라는 도구와 함께 제공 되는.NET Framework `aspnet_regsql.exe` 지정된 된 데이터베이스에서 데이터베이스 개체를 설치 하는 합니다. 미리 했 고 이러한 개체를 추가 하려면이 도구를 사용 합니다 `Reviews.mdf` 데이터베이스에 `App_Data` 폴더 (개발 데이터베이스). 이러한 개체는 프로덕션 데이터베이스를 추가 하는 경우이 자습서의 뒷부분에서이 도구를 사용 하는 방법을 살펴보겠습니다.

Services 데이터베이스에 데이터베이스 개체 이외의 응용 프로그램을 추가 하는 경우 `ASPNETDB` 사용자 지정 해야 합니다 `SqlMembershipProvider` 및 `SqlRoleProvider` 공급자는 적절 한 데이터베이스를 사용할 수 있도록 구성 클래스입니다. 멤버 자격 공급자 사용자 지정 하려면 추가 [  *&lt;멤버 자격&gt; 요소* ](https://msdn.microsoft.com/library/1b9hw62f.aspx) 내는 `<system.web>` 섹션 `Web.config`; 사용을 [  *&lt;roleManager&gt; 요소* ](https://msdn.microsoft.com/library/ms164660.aspx) 역할 공급자를 구성 합니다. 다음 코드 조각도 서 리뷰 응용 프로그램 s에서 만들어진 `Web.config` 멤버 자격 및 역할 Api에 대 한 구성 설정을 보여 줍니다. 참고-새 공급자를 등록 하는 둘 다 `ReviewMembership` 하 고 `ReviewRole` -사용 하는 합니다 `SqlMembershipProvider` 및 `SqlRoleProvider` 공급자 각각.

[!code-xml[Main](configuring-a-website-that-uses-application-services-cs/samples/sample1.xml)]

합니다 `Web.config` s 파일 `<authentication>` 요소도 폼 기반 인증을 지원 하도록 구성 되어 있습니다.
  

[!code-xml[Main](configuring-a-website-that-uses-application-services-cs/samples/sample2.xml)]

### <a name="limiting-access-to-the-administration-pages"></a>관리 페이지에 대 한 액세스를 제한합니다.

ASP.NET을 사용 하면 특정 파일 또는 폴더를 통해 역할 또는 사용자가 액세스 부여 하거나 거부 하는 작업을 쉽게 해당 *URL 권한 부여* 기능입니다. (의 URL 권한 부여를 간략하게 설명한 합니다 *IIS 간의 차이점 Core 및 ASP.NET Development Server* 자습서 및 IIS와 ASP.NET 개발 서버의 URL 권한 부여 규칙 정적을 다르게 적용 하는 방법을 보여 주었습니다. 동적 콘텐츠입니다.) 및 에 액세스 하지 못하도록 하려는 것 이므로 `~/Admin` 관리자 역할의 사용자를 제외 하 고 폴더를이 폴더에 URL 권한 부여 규칙을 추가할 필요 합니다. 특히, URL 권한 부여 규칙은 관리자 역할의 사용자를 허용 하 고 다른 모든 사용자를 거부 해야 합니다. 추가 하 여 이렇게를 `Web.config` 파일을 `~/Admin` 다음 콘텐츠로 폴더:

[!code-xml[Main](configuring-a-website-that-uses-application-services-cs/samples/sample3.xml)]

에 ASP.NET의 URL 권한 부여 기능 자체에 사용자 및 역할에 대 한 권한 부여 규칙을 사용 하는 방법에 대 한 자세한 내용은 참조 해야 합니다 [ *사용자 기반 권한 부여* ](../../older-versions-security/membership/user-based-authorization-cs.md) 고 [ *역할 기반 권한 부여* ](../../older-versions-security/roles/role-based-authorization-cs.md) 자습서에서 내 [ *웹 사이트 보안 자습서*](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)합니다.

## <a name="deploying-a-web-application-that-uses-application-services"></a>응용 프로그램 서비스를 사용 하는 웹 응용 프로그램 배포

응용 프로그램 서비스 및 응용 프로그램 서비스 정보를 데이터베이스에 저장 하는 공급자를 사용 하는 웹 사이트를 배포 하는 경우 반드시 프로덕션 데이터베이스에서 필요한 응용 프로그램 서비스는 데이터베이스 개체를 만들 수 있습니다. 처음에 프로덕션 데이터베이스는 이러한 개체를 응용 프로그램을 처음으로 배포할 때 (또는 응용 프로그램 서비스를 추가한 후 처음으로 배포 될 때), 이러한 필수 데이터베이스 개체 가져올 추가 단계를 수행 해야 합니다 프로덕션 데이터베이스입니다.

또 다른 문제는 프로덕션 환경으로 개발 환경에서 생성 된 사용자 계정을 복제 하려는 경우에 응용 프로그램 서비스를 사용 하는 웹 사이트를 배포 하는 경우에 발생할 수 있습니다. 멤버 자격 및 역할 구성에 따라 있기 프로덕션 데이터베이스를 개발 환경에서 생성 된 사용자 계정에 성공적으로 복사 하는 경우에 이러한 사용자는 프로덕션 환경에서 웹 응용 프로그램에 서명할 수 없습니다. 이 문제의 원인을 확인 하 고를 방지 하는 방법을 설명 하겠습니다.

ASP.NET은 훌륭한 [ *웹 사이트 관리 도구 (WSAT)* ](https://msdn.microsoft.com/library/yy40ytx0.aspx) Visual Studio에서 실행할 수 있습니다를 사용 하면 계정, 역할 및 권한 부여 규칙을 통해 웹 기반 관리 인터페이스입니다. 그러나는 WSAT 에서만 작동 로컬 웹 사이트에 대 한 사용자 계정, 역할 및 프로덕션 환경에서 웹 응용 프로그램에 대 한 권한 부여 규칙을 원격으로 관리를 사용할 수 없음을 의미 합니다. 프로덕션 웹 사이트에서 WSAT 비슷한 동작을 구현 하는 다른 방법을 살펴보겠습니다.

### <a name="adding-the-database-objects-using-aspnetregsqlexe"></a>데이터베이스 개체를 사용 하 여 aspnet 추가\_regsql.exe

합니다 *데이터베이스를 배포* 자습서에서는 프로덕션 데이터베이스에 대해 개발 데이터베이스에서 테이블 및 데이터를 복사 하는 방법을 보여 주었습니다. 및 이러한 기법을 사용 하 여 응용 프로그램 서비스 데이터베이스 개체를 복사할 확실히 수는 프로덕션 데이터베이스입니다. 또 다른 방법은 `aspnet_regsql.exe` 도구를 추가 하거나 데이터베이스에서 응용 프로그램 서비스 데이터베이스 개체를 제거 합니다.

> [!NOTE]
> `aspnet_regsql.exe` 도구는 지정된 된 데이터베이스에서 데이터베이스 개체를 만듭니다. 프로덕션 데이터베이스에 개발 데이터베이스에서 이러한 데이터베이스 개체의 데이터를 마이그레이션하지 않습니다 것. 프로덕션 데이터베이스 개발 데이터베이스의 사용자 계정 및 역할 정보를 복사 하는 것을 의미 하는 경우에 설명 된 기술을 사용 합니다 *데이터베이스를 배포* 자습서입니다.


S를 사용 하 여 프로덕션 데이터베이스에 데이터베이스 개체를 추가 하는 방법을 살펴볼 수 있도록 합니다 `aspnet_regsql.exe` 도구입니다. Windows 탐색기를 열고 %WINDIR%\ 컴퓨터에서.NET Framework 버전 2.0 디렉터리로 이동 하 여 시작 Microsoft.NET\Framework\v2.0.50727 합니다. 확인 하 게 된 `aspnet_regsql.exe` 도구입니다. 명령줄에서이 도구를 사용할 수 있지만 여기에 그래픽 사용자 인터페이스 두 번 클릭 합니다 `aspnet_regsql.exe` 그래픽 구성 요소를 시작 하는 파일입니다.

이 도구는 용도 설명 하는 시작 화면을 표시 하 여 시작 합니다. 그림 1에 나와 있는 "설치 옵션 선택" 화면에 고급을 클릭 합니다. 여기에서 응용 프로그램 서비스 데이터베이스 개체 또는 데이터베이스에서 제거할 추가를 선택할 수 있습니다. 프로덕션 데이터베이스에 이러한 개체를 추가 하려고 하기 때문에 "응용 프로그램 서비스에 대 한 SQL Server 구성" 옵션을 선택 하 고 클릭 합니다.


[![응용 프로그램 서비스에 대 한 SQL Server를 구성 하려면 선택 합니다.](configuring-a-website-that-uses-application-services-cs/_static/image2.jpg)](configuring-a-website-that-uses-application-services-cs/_static/image1.jpg)

**그림 1**: 응용 프로그램 서비스에 대 한 SQL server 구성 선택 ([큰 이미지를 보려면 클릭](configuring-a-website-that-uses-application-services-cs/_static/image3.jpg))


"The 서버 및 데이터베이스 선택"에서 데이터베이스에 연결 하는 정보 화면을 요구 합니다. 데이터베이스 서버, 보안 자격 증명을 및 웹 호스팅 회사에 게 제공 데이터베이스 이름을 입력 하 고 클릭 합니다.

> [!NOTE]
> 데이터베이스 서버 및 자격 증명을 입력 한 후 데이터베이스 드롭다운 목록을 확장 하는 경우 오류가 발생할 수 있습니다. 합니다 `aspnet_regsql.exe` 쿼리 도구를 `sysdatabases` 시스템 테이블에이 정보는 공개적으로 사용할 수 있도록 회사 잠금 해당 데이터베이스 서버를 호스트 하는 일부 웹 서버에서 데이터베이스 목록을 검색 합니다. 이 오류가 발생할 경우 데이터베이스 이름을 드롭다운 목록에 직접 입력할 수 있습니다.


[![데이터베이스의 연결 정보를 사용 하 여 도구를 제공 합니다.](configuring-a-website-that-uses-application-services-cs/_static/image5.jpg)](configuring-a-website-that-uses-application-services-cs/_static/image4.jpg)

**그림 2**: 도구와 데이터베이스의 연결 정보를 제공 합니다. ([큰 이미지를 보려면 클릭](configuring-a-website-that-uses-application-services-cs/_static/image6.jpg))


후속 스크린 응용 프로그램 서비스 데이터베이스 개체를 지정한 데이터베이스에 추가 될 예정인 수행 되는 정보, 즉 작업을 요약 합니다. 이 작업을 완료 옆에 있는 클릭 합니다. 몇 분 후 (그림 3 참조) 데이터베이스 개체를 추가한는 주목할 최종 화면이 표시 됩니다.


[![성공 했습니다. 프로덕션 데이터베이스에 추가 된 응용 프로그램 서비스 데이터베이스 개체](configuring-a-website-that-uses-application-services-cs/_static/image8.jpg)](configuring-a-website-that-uses-application-services-cs/_static/image7.jpg)

**그림 3**: 성공! 응용 프로그램 서비스 데이터베이스 개체에 추가 된 프로덕션 데이터베이스 ([클릭 하 여 큰 이미지 보기](configuring-a-website-that-uses-application-services-cs/_static/image9.jpg))


를 응용 프로그램 서비스 데이터베이스 개체를 프로덕션 데이터베이스에 성공적으로 추가 되었는지 확인 하려면 SQL Server Management Studio 열고 프로덕션 데이터베이스에 연결 합니다. 이제 데이터베이스에서 응용 프로그램 서비스 데이터베이스 테이블 그림 4에서 알 수 있듯이, 표시 `aspnet_Applications`하십시오 `aspnet_Membership`, `aspnet_Users`등.


[![데이터베이스 개체를 프로덕션 데이터베이스에 추가 되었는지 확인 합니다.](configuring-a-website-that-uses-application-services-cs/_static/image11.jpg)](configuring-a-website-that-uses-application-services-cs/_static/image10.jpg)

**그림 4**: 데이터베이스 개체를 프로덕션 데이터베이스에 추가 되었는지 확인 ([큰 이미지를 보려면 클릭](configuring-a-website-that-uses-application-services-cs/_static/image12.jpg))


사용 해야만 `aspnet_regsql.exe` 처음으로 또는 응용 프로그램 서비스를 사용 하 여 시작 된 후 처음으로 웹 응용 프로그램을 배포 하는 경우 도구입니다. 프로덕션 데이터베이스에서이 데이터베이스 개체 들이 되 면 이러한이 t 다시 추가 하거나 수정 해야를 했습니다.

### <a name="copying-user-accounts-from-development-to-production"></a>개발에서 프로덕션 사용자 계정 복사

사용 하는 경우는 `SqlMembershipProvider` 하 고 `SqlRoleProvider` 공급자 클래스는 SQL Server 데이터베이스에 응용 프로그램 서비스 정보를 저장할 사용자 계정 및 역할 정보를 포함 하 여 데이터베이스 테이블의 다양 한 저장 됩니다 `aspnet_Users`, `aspnet_Membership`, `aspnet_Roles`, 및 `aspnet_UsersInRoles`, 특히 합니다. 개발 하는 동안 개발 환경에서 사용자 계정을 만드는 경우 해당 데이터베이스 테이블에서 해당 레코드를 복사 하 여 프로덕션 환경에서 해당 사용자 계정을 복제할 수 있습니다. 데이터베이스 게시 마법사를 사용 하는 응용 프로그램 서비스 데이터베이스 개체를 배포할 경우 수 또한 하기로 레코드를 프로덕션에 대해서도 개발에서 만든 사용자 계정에 복사 합니다. 그러나 구성 설정에 따라 사용할 수 있습니다 이러한 사용자 계정을 가진 개발에서 생성 되었으며 프로덕션 복사할 프로덕션 웹 사이트에서 로그인 할 수는 있습니다. 무엇을 제공 하나요?

합니다 `SqlMembershipProvider` 고 `SqlRoleProvider` 공급자 클래스는 단일 데이터베이스는 이론상에서 각 응용 프로그램 수 있는 여러 응용 프로그램에 겹치는 사용자를 사용 하 여 사용자와 동일한 이름 가진 역할에 대 한 사용자 저장소로 사용 될 수 있도록 설계 되었습니다. 데이터베이스에서 응용 프로그램의 목록을 유지 관리 등이 유연성을 허용 하는 `aspnet_Applications` 테이블 및 각 사용자는 이러한 응용 프로그램 중 하나를 사용 하 여 연결 합니다. 특히 합니다 `aspnet_Users` 테이블에는 `ApplicationId` 각 사용자 레코드에 연결 하는 열을 `aspnet_Applications` 테이블입니다.

외에 합니다 `ApplicationId` 열을 `aspnet_Applications` 테이블도 포함 되어 있습니다를 `ApplicationName` 응용 프로그램에 대 한 더 친숙 한 이름을 제공 하는 열. 웹 사이트를 지시 해야 로그인 페이지에서 사용자가 자격 증명 유효성 검사와 같은 사용자 계정을 사용 하려고 하는 경우는 `SqlMembershipProvider` 클래스를 사용 하려면 응용 프로그램입니다. 응용 프로그램 이름을 제공 하 여이 및이 수행 하는 일반적으로 공급자가 구성에서 값을 가져옵니다 `Web.config` -를 통해 특히는 `applicationName` 특성입니다.

그러나 합니다 `applicationName` 특성에 지정 되지 않은 `Web.config`? 이러한 경우 멤버 자격 시스템으로 응용 프로그램 루트 경로 사용 합니다 `applicationName` 값입니다. 경우는 `applicationName` 특성 명시적으로 설정 하지 않으면 `Web.config`, 그런 다음 되 고 다른 응용 프로그램 루트를 사용 하 여 개발 환경과 프로덕션 환경 및 다른 응용 프로그램과 연결 수는 응용 프로그램 서비스의 이름입니다. 개발 환경에서 생성 된 해당 사용자가 없는 경우 이러한 불일치가 발생 하는 경우는 `ApplicationId` 와 일치 하지 않는 값을 `ApplicationId` 프로덕션 환경에 대 한 값입니다. 결과적 된다는 t-이득 해당 사용자가 로그인 할 수 있습니다.

> [!NOTE]
> 한다면이 경우-일치 하지 않습니다를 사용 하 여 프로덕션에 복사 하는 사용자 계정과 `ApplicationId` 값이 잘못 된 업데이트 쿼리를 작성할 수 있습니다 `ApplicationId` 값을 `ApplicationId` 프로덕션에서 사용 합니다. 업데이트 되 면 개발 환경에서 생성 된 계정을 가진 사용자가 이제 프로덕션 환경에서 웹 응용 프로그램에 로그인 할 것입니다.


좋은 소식은 두 가지 환경 동일한을 사용 하는지 확인 하기 위해 취할 수는 간단한 단계는 `ApplicationId` -명시적으로 설정 합니다 `applicationName` 특성 `Web.config` 모든 응용 프로그램 서비스 공급자에 대 한 합니다. 명시적으로 설정 합니다 `applicationName` 에서 특성을 "BookReviews"는 `<membership>` 및 `<roleManager>` 요소에서이 코드 조각으로 `Web.config` 보여 줍니다.

[!code-xml[Main](configuring-a-website-that-uses-application-services-cs/samples/sample4.xml)]

설정에 대 한 자세한 내용은 합니다 `applicationName` 특성과 근거를 가리킵니다 [ *Scott Guthrie* ](https://weblogs.asp.net/scottgu/) s 블로그 게시물 [ *항상 applicationName 설정 ASP.NET 멤버 자격 및 기타 공급자를 구성 하는 경우 속성*](https://weblogs.asp.net/scottgu/443634)합니다.

### <a name="managing-user-accounts-in-the-production-environment"></a>프로덕션 환경에서 사용자 계정 관리

ASP.NET 웹 사이트 관리 도구 (WSAT) 쉽게 만들고 및 사용자 계정 관리, 정의 및 적용 역할을 하 고 사용자 및 역할 기반 권한 부여 규칙을 꿈꾸고입니다. 솔루션 탐색기로 이동 하 고 ASP.NET 구성 아이콘을 클릭 하 여 또는 웹 사이트 또는 프로젝트 메뉴를 이동 하 고 ASP.NET 구성 메뉴 항목을 선택 하 여 Visual Studio에서 WSAT를 시작할 수 있습니다. 아쉽게도 WSAT는 로컬 웹 사이트를 사용 하 여 작동할 수 있습니다. 따라서 프로덕션 환경에서 웹 사이트를 관리 하는 WSAT 워크스테이션에서 사용할 수 없습니다.

좋은 소식은 멤버 자격 및 역할 Api를 통해 프로그래밍 방식으로 사용할 수는 WSAT 제공한 모든 노출 하는 기능 또한 WSAT 화면 많은 표준 ASP.NET 로그인 관련 컨트롤을 사용 합니다. 즉, 필요한 관리 기능을 제공 하는 웹 사이트에 ASP.NET 페이지를 추가할 수 있습니다.

이전 자습서도 서 리뷰 웹 응용 프로그램을 포함 하는 업데이트 회수는 `~/Admin` 폴더와이 폴더를 구성한 관리자 역할의 사용자 수만 있도록 합니다. 페이지 라는 폴더에 추가한 `CreateAccount.aspx` 에서 관리자로 만들 있는 새 사용자 계정입니다. 이 페이지는 새 사용자 계정을 만들기 위한 사용자 인터페이스 및 백 엔드 논리를 표시할 CreateUserWizard 컨트롤을 사용 합니다. 더 많은 새로운 컨트롤 포함 새 사용자는 관리자 역할에도 추가 해야 하는지 여부를 요구 하는 확인란을 사용자 지정한 (그림 5 참조). 약간의 작업을 사용 하 여 사용자 및 역할 관리 관련 작업을 WSAT에서 제공 되는 구현 하는 사용자 지정 페이지 집합을 빌드할 수 있습니다.

> [!NOTE]
> ASP.NET 웹 로그인 관련 컨트롤을 함께 멤버 자격 및 역할 Api를 사용 하는 방법은 읽을 수 있는지에 대 한 필자의 [ *웹 사이트 보안 자습서*](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)합니다. CreateUserWizard 컨트롤 사용자 지정에 대 한 자세한 내용은 참조는 [ *사용자 계정 만들기* ](../../older-versions-security/membership/creating-user-accounts-cs.md) 하 고 [ *추가 사용자 정보 저장* ](../../older-versions-security/membership/storing-additional-user-information-cs.md) 자습서 또는 체크 아웃 [ *Erich Peterson* ](http://www.erichpeterson.com/) 의 기사 [ *CreateUserWizard 컨트롤 사용자 지정* ](http://aspnet.4guysfromrolla.com/articles/070506-1.aspx).


[![관리자는 새 사용자 계정을 만들 수 있습니다.](configuring-a-website-that-uses-application-services-cs/_static/image14.jpg)](configuring-a-website-that-uses-application-services-cs/_static/image13.jpg)

**그림 5**: 관리자 수 있습니다 새 사용자 계정 만들기 ([큰 이미지를 보려면 클릭](configuring-a-website-that-uses-application-services-cs/_static/image15.jpg))


WSAT 체크 아웃의 전체 기능을 사용 해야 하는 경우 [ *롤링 사용자 고유의 웹 사이트 관리 도구*](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx), 저자에서 Dan Clem 안내를 사용자 지정 WSAT 같은 도구를 빌드하는 프로세스입니다. Dan 자신의 응용 프로그램의 소스 코드 (C#)를 공유 하 고 호스팅된 웹 사이트에 추가 하기 위한 단계별 지침을 제공 합니다.

## <a name="summary"></a>요약

응용 프로그램 서비스 데이터베이스 구현을 사용 하는 웹 응용 프로그램을 배포 하는 경우 프로덕션 데이터베이스에 필요한 데이터베이스 개체를 먼저 확인 해야 합니다. 설명한 기법을 사용 하 여 이러한 개체를 추가할 수는 *데이터베이스를 배포* 자습서 사용할 수 있습니다는 `aspnet_regsql.exe` 도구를이 자습서에서 살펴본 것 처럼 합니다. 개발 및 프로덕션 환경 (프로덕션에서 유효 사용자 및 개발 환경에서 만든 역할을 하려는 경우 반드시) 및 기술에 사용 되는 응용 프로그램 이름 동기화 하는 작업을 중심으로 맞물리면서 기타 문제 사용자 및 프로덕션 환경에서 역할을 관리 합니다.

즐거운 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [*ASP.NET SQL Server 등록 도구 (aspnet_regsql.exe)*](https://msdn.microsoft.com/library/ms229862.aspx)
- [*SQL Server에 대 한 응용 프로그램 서비스 데이터베이스 만들기*](https://msdn.microsoft.com/library/x28wfk74.aspx)
- [*SQL Server에서 멤버 자격 스키마 만들기*](../../older-versions-security/membership/creating-the-membership-schema-in-sql-server-cs.md)
- [*ASP.NET가 멤버 자격, 역할 및 프로필을 검사합니다.*](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [*고유한 웹 사이트 관리 도구를 롤링합니다.*](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)
- [*웹 사이트 보안 자습서*](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)
- [*웹 사이트 관리 도구 개요*](https://msdn.microsoft.com/library/yy40ytx0.aspx)

> [!div class="step-by-step"]
> [이전](configuring-the-production-web-application-to-use-the-production-database-cs.md)
> [다음](strategies-for-database-development-and-deployment-cs.md)
