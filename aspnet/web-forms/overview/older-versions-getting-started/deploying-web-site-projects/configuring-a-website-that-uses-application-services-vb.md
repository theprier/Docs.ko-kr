---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-a-website-that-uses-application-services-vb
title: 응용 프로그램 서비스 (VB)를 사용 하는 웹 사이트를 구성 | Microsoft Docs
author: rick-anderson
description: ASP.NET 버전 2.0에는 일련의.NET Framework의 일부 이며 문서 블록의 도구 모음 서비스를 yo으로 사용 하는 응용 프로그램 서비스를 도입 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/23/2009
ms.topic: article
ms.assetid: 9c31a42f-d8bb-4c0f-9ccc-597d4f70ac42
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-a-website-that-uses-application-services-vb
msc.type: authoredcontent
ms.openlocfilehash: 416cc5b3b6ac3c8e7a6c1a99a8b4f8d94b5b3428
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="configuring-a-website-that-uses-application-services-vb"></a>응용 프로그램 서비스 (VB)를 사용 하는 웹 사이트를 구성 합니다.
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/E/6/F/E6FE3A1F-EE3A-4119-989A-33D1A9F6F6DD/ASPNET_Hosting_Tutorial_09_VB.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/C/3/9/C391A649-B357-4A7B-BAA4-48C96871FEA6/aspnet_tutorial09_AppServicesConfig_vb.pdf)

> ASP.NET 버전 2.0에는 일련을의.NET Framework의 일부를 하 고 웹 응용 프로그램에 다양 한 기능을 추가 하는 데 사용할 수 있는 구성 요소 서비스의 모음으로 사용 하는 응용 프로그램 서비스를 도입 되었습니다. 이 자습서에서는 응용 프로그램 서비스를 사용 하려면 프로덕션 환경에서 웹 사이트를 구성 하는 방법을 살펴봅니다 및 일반적인 문제를 사용자 계정 및 프로덕션 환경에 대 한 역할을 관리 합니다.


## <a name="introduction"></a>소개

ASP.NET 버전 2.0에는 일련의 도입 *응용 프로그램 서비스*,.NET Framework의 일부인 하 고 문서 블록 집합이 서비스 역할은 웹 응용 프로그램에 다양 한 기능을 추가 하려면 사용할 수 있습니다. 응용 프로그램 서비스는 다음과 같습니다.

- **멤버 자격** -사용자 계정을 만들고 관리 하기 위한 API입니다.
- **역할** -사용자가 그룹으로 분류 하기 위한 API입니다.
- **프로필** -사용자 지정, 사용자 고유의 콘텐츠를 저장 하기 위한 API입니다.
- **사이트 맵** -예: 메뉴 및 이동 경로 탐색 컨트롤을 통해 표시 될 수 있는 계층의 형태로 사이트 s 논리 구조를 정의 하기 위한 API입니다.
- **개인 설정** -가장 흔히 사용 되는 사용자 지정 기본 설정을 유지 관리 하기 위한 API [ *WebParts*](https://msdn.microsoft.com/library/e0s9t4ck.aspx)합니다.
- **상태 모니터링** -성능, 보안, 오류 및 기타 시스템 상태 메트릭을 실행 중인 웹 응용 프로그램에 대 한 모니터링을 위한 API입니다.
  

응용 프로그램 서비스 Api는 특정 구현에 연결 되지 않습니다. 특정을 사용 하는 응용 프로그램 서비스를 지시 하는 대신, *공급자*, 해당 공급자 특정 기술을 사용 하 여 서비스를 구현 하 고 있습니다. 웹 호스팅 회사에 호스팅된 인터넷 기반 웹 응용 프로그램에 대 한 가장 자주 사용 되는 공급자에는 SQL Server 데이터베이스 구현을 사용 하는 해당 공급자가 있습니다. 예를 들어는 `SqlMembershipProvider` Microsoft SQL Server 데이터베이스의 사용자 계정 정보를 저장 하는 멤버 API에 대 한 공급자입니다.

응용 프로그램 서비스 및 SQL Server 공급자를 사용 하 여 응용 프로그램을 배포 하는 경우 몇 가지 과제를 추가 합니다. 먼저 응용 프로그램 서비스 데이터베이스 개체 개발 및 프로덕션 데이터베이스에 대해 올바르게 작성 고 적절 하 게 초기화 해야 합니다. 수행 되어야 하는 중요 한 구성 설정도 있습니다.

> [!NOTE]
> Api를 사용 하 여 설계 된 응용 프로그램 서비스는 [ *공급자 모델*](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx), s API에 대 한 구현 세부 정보를 런타임 시 제공 될 수 있는 디자인 패턴. .NET Framework와 같은 사용할 수 있는 응용 프로그램 서비스 공급자와 함께 제공 되는 `SqlMembershipProvider` 및 `SqlRoleProvider`, 멤버 자격에 대 한 공급자는 및 SQL Server를 사용 하는 역할 Api 데이터베이스 구현입니다. 만들 수 있습니다 및 플러그 인 사용자 지정 공급자입니다. 책 검토 웹 응용 프로그램이 이미 사이트 맵 API에 대 한 사용자 지정 공급자를 포함 하는 실제로 (`ReviewSiteMapProvider`)를 생성 하는 데이터에서 사이트 맵은 `Genres` 및 `Books` 데이터베이스의 테이블입니다.


이 자습서의 멤버 자격과 역할 Api를 사용 하도록 책 검토 웹 응용 프로그램을 확장 방법을 보는 것으로 시작 합니다. 다음 SQL Server 데이터베이스 구현으로 응용 프로그램 서비스를 사용 하 고 사용자 계정 및 프로덕션 환경에 대 한 역할을 관리 하는 일반적인 문제를 해결 하 여 완료 하는 웹 응용 프로그램 배포 안내 합니다.

## <a name="updates-to-the-book-reviews-application"></a>책 검토 응용 프로그램에 대 한 업데이트

지난 며칠 책 검토 웹 응용 프로그램이 동적, 데이터 기반 웹 응용 프로그램에 정적 웹 사이트에서 업데이트 된 자습서 장르 및 의견을 관리 하기 위한 관리 페이지의 집합으로 완료 합니다. 그러나이 관리 섹션에는 현재 보호 되지 않습니다-모든 사용자에 게 관리 페이지 URL을 알고 (또는 추측) 수에가지고 안심할 및 만들기, 편집 또는 삭제할 사이트에서 검토 합니다. 웹 사이트의 특정 부분을 보호 하는 일반적인 방법은 사용자 계정을 구현 하 고 다음 URL 권한 부여 규칙을 사용 하 여 특정 사용자 또는 역할에 대 한 액세스를 제한 하는 합니다. 이 자습서와 함께 다운로드할 수 있는 책 검토 웹 응용 프로그램 사용자 계정 및 역할을 지원합니다. 여러 개 정의 된 역할의 이름이 Admin 및이 역할의 사용자만의 관리 페이지에 액세스할 수 있습니다.

> [!NOTE]
> I 했습니다 책 검토 웹 응용 프로그램에서 3 개의 사용자 계정을 만든: Scott, Jisun, 및 Alice입니다. 모든 세 사용자가 동일한 암호: **암호!** Scott 및 Jisun 관리자 역할에는, Alice가 없습니다. 사이트 s-관리 페이지는 익명 사용자에 게 여전히 액세스할 수 있습니다. 에 로그인 하는 사이트를 방문를 관리 하려는 경우가 아니면 필요가 없습니다 즉, 관리자 역할의 사용자로 로그인 해야 합니다.는 경우.


책 검토 응용 프로그램 s 마스터 페이지 인증 되 고 익명 사용자에 대 한 다른 사용자 인터페이스를 포함 하도록 업데이트 되었습니다. 익명 사용자가 사이트를 방문할 경우 오른쪽 위 모서리의 로그인 링크를 발견 합니다. 인증된 된 사용자에 게, "ळ े, *username*!" 및를 로그 아웃 링크입니다. 여기서 s는 로그인 페이지에도 (`~/Login.aspx`), 방문자를 인증 하기 위한 사용자 인터페이스 및 논리를 제공 하는 로그인 웹 컨트롤을 포함 하 합니다. 관리자만 새 계정을 만들 수 있습니다. (페이지가 생성 및 관리 사용자 계정에는 `~/Admin` 폴더입니다.)

### <a name="configuring-the-membership-and-roles-apis"></a>멤버 자격 및 역할 Api 구성

책 검토 웹 응용 프로그램 사용자 계정을 지원 하 고 해당 사용자 역할 (즉, 관리자 역할)를 그룹화 할 멤버 자격 및 역할 Api를 사용 합니다. `SqlMembershipProvider` 및 `SqlRoleProvider` 공급자 클래스에 사용 하기 위해 SQL Server 데이터베이스에 역할 및 계정 정보를 저장 하는 데 사용 합니다.

> [!NOTE]
> 이 자습서에서의 멤버 자격과 역할 Api를 지원 하도록 웹 응용 프로그램을 구성을 상세히 되도록 적합 하지 않습니다. 이러한 Api 및 사용 하 여 웹 사이트를 구성 하는 데 필요한 단계를 철저 한 확인을 읽으세요 내 [ *웹 사이트 보안 자습서*](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)합니다.


SQL Server 데이터베이스와 응용 프로그램 서비스를 사용 하려면 먼저 사용자 계정을 저장할 데이터베이스에 이러한 공급자에서 사용 하는 데이터베이스 개체 및 저장 된 역할 정보를 추가 해야 합니다. 다양 한 테이블, 뷰 및 저장된 프로시저를 포함 하는 이러한 데이터베이스 필수 개체입니다. 그렇지 않으면 지정 되지 않은 경우는 `SqlMembershipProvider` 및 `SqlRoleProvider` 라는 SQL Server Express Edition 데이터베이스를 사용 하는 공급자 클래스 `ASPNETDB` 응용 프로그램 s에 있는 `App_Data` 폴더; 자동으로 만들어집니다 이러한 데이터베이스가 없는 경우 런타임 시 이러한 공급자가 필요한 데이터베이스 개체입니다.

가능 하면 및를 만들려면 일반적으로 이상적인 응용 프로그램 서비스 웹 사이트의 응용 프로그램별 데이터가 저장 되는 동일한 데이터베이스에 데이터베이스 개체. 라는 도구와 함께 제공 되는.NET Framework `aspnet_regsql.exe` 지정된 된 데이터베이스에 데이터베이스 개체를 설치 하는 합니다. 미리 gone를 있으며 이러한 개체를 추가 하려면이 도구를 사용 하 여 `Reviews.mdf` 여기에 데이터베이스는 `App_Data` 폴더 (개발 데이터베이스). 이러한 개체는 프로덕션 데이터베이스를 추가 하는 경우이 자습서의 뒷부분에서이 도구를 사용 하는 방법을 살펴보겠습니다.

응용 프로그램 데이터베이스에 데이터베이스 개체를 이외의 다른 서비스를 추가 하는 경우 `ASPNETDB` 사용자 지정 해야 합니다는 `SqlMembershipProvider` 및 `SqlRoleProvider` 공급자 클래스 구성을 적절 한 데이터베이스를 사용할 수 있도록 합니다. 사용자 지정 하려면 멤버 자격 공급자 추가 [  *&lt;구성원&gt; 요소* ](https://msdn.microsoft.com/library/1b9hw62f.aspx) 내에서 `<system.web>` 섹션 `Web.config`; 사용 하 여는 [  *&lt;roleManager&gt; 요소* ](https://msdn.microsoft.com/library/ms164660.aspx) 역할 공급자를 구성할 수 있습니다. 다음 코드 조각은 책 검토 응용 프로그램 s에서 가져온 것 `Web.config` 멤버 자격 및 역할 Api에 대 한 구성 설정을 보여 줍니다. 참고-새 공급자를 등록 모두 `ReviewMembership` 및 `ReviewRole` -사용 하는 `SqlMembershipProvider` 및 `SqlRoleProvider` 공급자, 각각.

[!code-xml[Main](configuring-a-website-that-uses-application-services-vb/samples/sample1.xml)]

`Web.config` 파일의 `<authentication>` 요소도 폼 기반 인증을 지원 하도록 구성 되어 있습니다.
  

[!code-xml[Main](configuring-a-website-that-uses-application-services-vb/samples/sample2.xml)]

### <a name="limiting-access-to-the-administration-pages"></a>관리 페이지에 대 한 액세스를 제한합니다.

ASP.NET을 사용 하면 쉽게 부여 하거나 특정 파일이 나 사용자 또는 역할을 통해 폴더에 대 한 액세스를 거부 하려면 해당 *URL 권한 부여* 기능입니다. (의 URL 권한 부여에서 간략하게 설명한는 *IIS 간의 차이점 Core 및 ASP.NET 개발 서버* 자습서 IIS 및 ASP.NET 개발 서버 정적 다르게에 대 한 URL 권한 부여 규칙을 적용 방법을 표시 합니다. 동적 콘텐츠입니다.) 및 에 대 한 액세스를 금지 하 려 하므로 `~/Admin` 관리자 역할의 사용자를 제외 하 고 폴더를이 폴더에 URL 권한 부여 규칙을 추가 해야 합니다. 특히, URL 권한 부여 규칙 관리자 역할의 사용자가 허용 하 고 다른 모든 사용자가 거부 해야 합니다. 추가 하 여 이렇게는 `Web.config` 파일을 여 `~/Admin` 다음과 같은 내용이 포함 된 폴더:

[!code-xml[Main](configuring-a-website-that-uses-application-services-vb/samples/sample3.xml)]

ASP.NET의 URL 권한 부여 기능 및 사용자와 역할에 대 한 권한 부여 규칙을 사용 하는 방법에 대 한 자세한 내용은 참조 해야에 대 한는 [ *사용자 기반 권한 부여* ](../../older-versions-security/membership/user-based-authorization-vb.md) 및 [ *역할 기반 권한 부여* ](../../older-versions-security/roles/role-based-authorization-vb.md) 자습서에서 내 [ *웹 사이트 보안 자습서*](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)합니다.

## <a name="deploying-a-web-application-that-uses-application-services"></a>응용 프로그램 서비스를 사용 하는 웹 응용 프로그램 배포

데이터베이스에 응용 프로그램 서비스 정보를 저장 하는 공급자 및 응용 프로그램 서비스를 사용 하는 웹 사이트를 배포할 때는 반드시 응용 프로그램 서비스에 필요한 데이터베이스 개체를 프로덕션 데이터베이스에서 만들 수 있습니다. 처음에 프로덕션 데이터베이스는 이러한 개체를 하므로 응용 프로그램을 처음 배포할 때 (또는 응용 프로그램 서비스를 추가한 후에 처음으로 배포 될 때), 이러한 필수 데이터베이스 개체 가져올 추가 단계를 수행 해야 합니다는 프로덕션 데이터베이스입니다.

또 다른 문제는 프로덕션 환경으로 개발 환경에서 만든 사용자 계정을 복제 하려는 경우 응용 프로그램 서비스를 사용 하는 웹 사이트를 배포할 때 발생할 수 있습니다. 멤버 자격 및 역할 구성에 따라 있기 프로덕션 데이터베이스를 개발 환경에서 생성 된 사용자 계정, 성공적으로 복사 하는 경우에 프로덕션 환경에서 웹 응용 프로그램에 이러한 사용자가 로그인 수 없습니다. 이 문제의 원인을 살펴봅니다 알아보고를 방지 하는 방법에 설명 하겠습니다.

좋은와 함께 제공 ASP.NET [ *웹 사이트 관리 도구 (WSAT)* ](https://msdn.microsoft.com/library/yy40ytx0.aspx) Visual Studio에서 시작할 수 있는 및 사용자 계정, 역할 및 권한 부여 규칙을 통해 웹 기반 관리 하도록 허용 인터페이스입니다. 안타깝게도,는 WSAT 에서만 작동 로컬 웹 사이트에 대 한 사용자 계정, 역할 및 프로덕션 환경에서 웹 응용 프로그램에 대 한 권한 부여 규칙을 원격으로 관리 하는 데 사용할 수 없습니다. 프로덕션 웹 사이트에서 WSAT 비슷한 동작을 구현 하 여 여러 가지 방법을 살펴보겠습니다.

### <a name="adding-the-database-objects-using-aspnetregsqlexe"></a>데이터베이스 개체를 사용 하 여 aspnet 추가\_regsql.exe

*데이터베이스 배포* 자습서에는 프로덕션 데이터베이스를 개발 데이터베이스에서 테이블 및 데이터를 복사 하는 방법을 배웠습니다 및 응용 프로그램 서비스 데이터베이스 개체를 복사 하려면 이러한 기술은 확실히 사용할 수는 프로덕션 데이터베이스입니다. 두 번째 방법은 `aspnet_regsql.exe` 도구를 추가 하거나 데이터베이스에서 응용 프로그램 서비스 데이터베이스 개체를 제거 합니다.

> [!NOTE]
> `aspnet_regsql.exe` 도구는 지정된 된 데이터베이스에서 데이터베이스 개체를 만듭니다. 것 마이그레이션하지 않습니다 이러한 데이터베이스 개체에 대 한 데이터 개발 데이터베이스에서 프로덕션 데이터베이스에 있습니다. 설명 하는 기술은 사용 하 여 프로덕션 데이터베이스를 개발 데이터베이스의 사용자 계정과 역할 정보를 복사 하는 것을 의미 하는 경우는 *데이터베이스 배포* 자습서입니다.


데이터베이스 개체를 사용 하 여 프로덕션 데이터베이스를 추가 하는 방법에 대해 s는 `aspnet_regsql.exe` 도구입니다. Windows 탐색기를 열고 %WINDIR%\ 컴퓨터에.NET Framework 버전 2.0 디렉터리로 이동 하 여 시작 Microsoft.NET\Framework\v2.0.50727 합니다. 있습니다 있습니다는 `aspnet_regsql.exe` 도구입니다. 이 도구를 사용 하는 명령줄에서 이지만 그래픽 사용자 인터페이스; 포함 두 번 클릭은 `aspnet_regsql.exe` 파일을 해당 그래픽 구성 요소를 시작 합니다.

도구가 용도 설명 하는 시작 화면을 표시 하 여 시작 합니다. 클릭는 그림 1에 나와 있는 "설치 옵션 선택" 화면으로 이동 합니다. 여기에서 응용 프로그램 서비스 데이터베이스 개체 또는 데이터베이스에서 제거를 추가할 수 있습니다. 이러한 개체는 프로덕션 데이터베이스를 추가 하려는 것 이므로 "응용 프로그램 서비스에 대 한 SQL Server 구성" 옵션을 선택 하 고 클릭 합니다.


[![응용 프로그램 서비스에 대 한 SQL Server를 구성 하도록 선택](configuring-a-website-that-uses-application-services-vb/_static/image2.jpg)](configuring-a-website-that-uses-application-services-vb/_static/image1.jpg)

**그림 1**: 응용 프로그램 서비스에 대 한 SQL Server 구성 하도록 선택 ([전체 크기 이미지를 보려면 클릭](configuring-a-website-that-uses-application-services-vb/_static/image3.jpg))


화면 "the 서버 및 데이터베이스 선택"에서 데이터베이스에 연결 하기 위한 정보 메시지가 표시 됩니다. 데이터베이스 서버, 보안 자격 증명 및 웹 호스팅 회사에 게 제공 하는 데이터베이스 이름을 입력 하 고 클릭 합니다.

> [!NOTE]
> 데이터베이스 서버 및 자격 증명을 입력 한 후 데이터베이스 드롭 다운 목록을 확장 하는 경우 오류가 발생할 수 있습니다. `aspnet_regsql.exe` 쿼리 도구는 `sysdatabases` 시스템 테이블에 서버에 있지만이 정보를 공개적으로 사용할 수 있도록 회사 잠금 데이터베이스 서버를 호스팅하는 일부 웹에 있는 데이터베이스 목록을 검색 합니다. 이 오류가 발생할 경우 데이터베이스 이름을 드롭 다운 목록에 직접 입력할 수 있습니다.


[![데이터베이스의 연결 정보를 사용 하 여 도구를 제공 합니다.](configuring-a-website-that-uses-application-services-vb/_static/image5.jpg)](configuring-a-website-that-uses-application-services-vb/_static/image4.jpg)

**그림 2**: 도구와 데이터베이스의 연결 정보를 제공 합니다. ([전체 크기 이미지를 보려면 클릭](configuring-a-website-that-uses-application-services-vb/_static/image6.jpg))


후속 화면이 응용 프로그램 서비스 데이터베이스 개체는 지정된 된 데이터베이스에 추가할 작업 수행, 즉 하려고을 요약 합니다. 이 작업을 완료 클릭 합니다. 몇 분 후 (그림 3 참조) 데이터베이스 개체를 추가한를 나타내어 최종 화면이 표시 됩니다.


[![성공 했습니다! 프로덕션 데이터베이스에 추가 된 응용 프로그램 서비스 데이터베이스 개체](configuring-a-website-that-uses-application-services-vb/_static/image8.jpg)](configuring-a-website-that-uses-application-services-vb/_static/image7.jpg)

**그림 3**: 성공! 응용 프로그램 서비스 데이터베이스 개체에 추가 된 프로덕션 데이터베이스 ([전체 크기 이미지를 보려면 클릭](configuring-a-website-that-uses-application-services-vb/_static/image9.jpg))


응용 프로그램 서비스 데이터베이스 개체는 프로덕션 데이터베이스에 성공적으로 추가 된 것을 확인 하려면 SQL Server Management Studio를 열고 프로덕션 데이터베이스에 연결 합니다. 데이터베이스에 응용 프로그램 서비스 데이터베이스 테이블 이제 표시 그림 4에서 볼 수 있듯이 `aspnet_Applications`, `aspnet_Membership`, `aspnet_Users`, 등입니다.


[![데이터베이스 개체는 프로덕션 데이터베이스에 추가 되었는지 확인 합니다.](configuring-a-website-that-uses-application-services-vb/_static/image11.jpg)](configuring-a-website-that-uses-application-services-vb/_static/image10.jpg)

**그림 4**: 데이터베이스 개체는 프로덕션 데이터베이스에 추가 되었는지 확인 ([전체 크기 이미지를 보려면 클릭](configuring-a-website-that-uses-application-services-vb/_static/image12.jpg))


사용 하기만 됩니다는 `aspnet_regsql.exe` 처음으로 또는 응용 프로그램 서비스를 사용 하 여 시작 된 후 처음으로 웹 응용 프로그램을 배포 하는 경우 도구입니다. 프로덕션 데이터베이스에서 이러한 데이터베이스 개체에 한 번은 t 필요가 다시 추가 하거나 수정 했습니다.

### <a name="copying-user-accounts-from-development-to-production"></a>개발에서 프로덕션 사용자 계정 복사

사용 하는 경우는 `SqlMembershipProvider` 및 `SqlRoleProvider` 공급자 클래스는 SQL Server 데이터베이스에 응용 프로그램 서비스 정보를 저장 하는 사용자 계정과 역할 정보 다양 한 포함 하 여 데이터베이스 테이블에에서 저장 됩니다 `aspnet_Users`, `aspnet_Membership`, `aspnet_Roles`, 및 `aspnet_UsersInRoles`, 등입니다. 개발 중 개발 환경에서 사용자 계정을 만든 경우 해당 데이터베이스 테이블에서 해당 레코드를 복사 하 여 프로덕션 환경에서 해당 사용자 계정을 복제할 수 있습니다. 데이터베이스 게시 마법사를 사용 하는 응용 프로그램 서비스 데이터베이스 개체를 배포할 경우 수 또한 하기로 선택 프로덕션에 대해서도를 개발에서 만들어진 사용자 계정은 발생 시키는 레코드 복사 합니다. 하지만 구성 설정에 따라 알게 될 수 있습니다 이러한 사용자 계정을 가진 개발에서 만들고 된 프로덕션 환경에 복사 합니다. 프로덕션 웹 사이트에서 로그인 할 수 없는 합니다. 제공?

`SqlMembershipProvider` 및 `SqlRoleProvider` 공급자 클래스는 이론적으로 각 응용 프로그램 수 있는 여러 응용 프로그램 겹치는 사용자 이름으로 사용자와 동일한 이름 가진 역할에 대 한 단일 데이터베이스 사용자 저장소로 사용 될 수 있도록 설계 되었습니다. 이러한 유연성을 허용 하려면 데이터베이스에서 응용 프로그램 목록을 유지 관리는 `aspnet_Applications` 테이블 및 각 사용자가 이러한 응용 프로그램 중 하나에 연결 합니다. 특히,는 `aspnet_Users` 테이블에는 `ApplicationId` 열에서 레코드를 각 사용자에 연결 하는 `aspnet_Applications` 테이블입니다.

이외에 `ApplicationId` 열은 `aspnet_Applications` 테이블도 포함 되어는 `ApplicationName` 응용 프로그램에 대 한 사람이 더 친숙 한 이름을 제공 하는 열입니다. 웹 사이트 지시 해야 로그인 페이지에서 사용자 s 자격 증명을 사용 하는 유효성 검사와 같은 사용자 계정을 사용 하려고 할 때의 `SqlMembershipProvider` 클래스 할 응용 프로그램을 사용 합니다. 응용 프로그램 이름을 제공 하 여이 및이 수행 하는 일반적으로에서 s 공급자 구성에서 값을 가져옵니다 `Web.config` -통해 구체적으로 `applicationName` 특성입니다.

그러나는 `applicationName` 특성에 지정 되지 않은 `Web.config`? 이 경우 멤버 자격 시스템으로 응용 프로그램 루트 경로 사용는 `applicationName` 값입니다. 경우는 `applicationName` 특성에서 명시적으로 설정 되지 않으면 `Web.config`, 그런 다음 다른 응용 프로그램 루트를 사용 하 여 개발 환경 및 프로덕션 환경 및 따라서 서로 다른 응용 프로그램에 연관 될 가능성은 응용 프로그램 서비스의 이름입니다. 이러한 불일치가 발생 하는 개발 환경에서 만든 해당 사용자 들 다음 경우는 `ApplicationId` 와 일치 하지 않는 값은 `ApplicationId` 프로덕션 환경에 대 한 값입니다. Net 결과 t-이득 해당 사용자가 로그인 할 수 있습니다.

> [!NOTE]
> 한다면이 경우-와 일치 하지 않는 프로덕션 환경에 복사 하는 사용자 계정으로 `ApplicationId` 이러한 잘못 된 업데이트 하는 쿼리를 작성할 수 값- `ApplicationId` 값을 `ApplicationId` 프로덕션에 사용 합니다. 업데이트 되 면 개발 환경에서 생성 된 계정을 가진 사용자가 이제 프로덕션에서 웹 응용 프로그램에 로그인 할 수 것입니다.


다행 스럽게도 동일한 두 가지 환경 사용 하는지 확인 하기 위해 취할 수 간단한 단계 임을 `ApplicationId` 명시적으로 설정 된-는 `applicationName` 특성 `Web.config` 모든 응용 프로그램 서비스 공급자에 대 한 합니다. 명시적으로 설정 된 `applicationName` 에서 특성 "BookReviews"을는 `<membership>` 및 `<roleManager>` 요소에서 다음이 코드는 `Web.config` 보여 줍니다.

[!code-xml[Main](configuring-a-website-that-uses-application-services-vb/samples/sample4.xml)]

에 대 한 설정에 대 한 자세한 내용은 `applicationName` 특성과 근거 참조 [ *Scott Guthrie* ](https://weblogs.asp.net/scottgu/) s 블로그 게시물 [ *항상 응용 프로그램 이름 설정 ASP.NET 멤버 자격 및 기타 공급자를 구성할 때 속성*](https://weblogs.asp.net/scottgu/443634)합니다.

### <a name="managing-user-accounts-in-the-production-environment"></a>프로덕션 환경에서 사용자 계정 관리

ASP.NET 웹 사이트 관리 도구 (WSAT)을 사용 하면 쉽게 만들고 및 사용자 계정 관리, 정의 및 역할을 적용 하 고 사용자 및 역할 기반 권한 부여 규칙 쓰십시오 수 있습니다. 웹 사이트 또는 프로젝트 메뉴 하 고 ASP.NET 구성 메뉴 항목을 선택 하거나 솔루션 탐색기로 이동 하 고 ASP.NET 구성 아이콘을 클릭 하 여 Visual Studio에서 WSAT를 시작할 수 있습니다. 그러나는 WSAT 로컬 웹 사이트와 작동할 수 있습니다. 따라서 프로덕션 환경에서 웹 사이트를 관리 하는 WSAT 워크스테이션에서 사용할 수 없습니다.

다행 스럽게도는 WSAT 제공한 모두 노출 하는 기능 인지 멤버 자격 및 역할 Api를 통해 프로그래밍 방식으로 사용할 수 또한 WSAT 화면 중 많은 표준 ASP.NET 로그인 관련 컨트롤을 사용 합니다. 즉, 필요한 관리 기능을 제공 하는 웹 사이트에 ASP.NET 페이지를 추가할 수 있습니다.

이전 자습서를 포함 하도록 책 검토 웹 응용 프로그램 업데이트 회수는 `~/Admin` 폴더 및이 폴더를 구성한만 관리자 역할의 사용자가 허용 하도록 합니다. 페이지 라는 해당 폴더에 추가한 `CreateAccount.aspx` 에서 있는 관리자는 새 사용자 계정을 만들 수 있습니다. 이 페이지는 CreateUserWizard 컨트롤을 사용 하 여 새 사용자 계정을 만들기 위한 사용자 인터페이스 및 백 엔드 논리를 표시 합니다. 어떤 s, 더 많은 사용자 지정한 적이 새 사용자는 관리자 역할에도 추가 해야 하는지 여부를 묻는 메시지를 표시 하는 확인란을 포함 하도록 컨트롤 (그림 5 참조). 약간의 작업은 사용자 및 역할 관리 관련 작업은 WSAT에서 제공 되는 구현 하는 페이지의 사용자 지정 집합을 작성할 수 있습니다.

> [!NOTE]
> 멤버 자격 및 역할 Api를 사용 하 여 ASP.NET 웹 로그인 관련 컨트롤과 함께 대 한 자세한 내용은 참조 해야에 대 한 내 [ *웹 사이트 보안 자습서*](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)합니다. CreateUserWizard 컨트롤 사용자 지정에 대 한 자세한 참조는 [ *사용자 계정 만들기* ](../../older-versions-security/membership/creating-user-accounts-vb.md) 및 [ *추가 사용자 정보를 저장* ](../../older-versions-security/membership/storing-additional-user-information-vb.md) 자습서, 또는 체크 아웃 [ *Erich Peterson* ](http://www.erichpeterson.com/) s 문서 [ *CreateUserWizard 컨트롤 사용자 지정* ](http://aspnet.4guysfromrolla.com/articles/070506-1.aspx).


[![관리자는 새 사용자 계정을 만들 수 있습니다.](configuring-a-website-that-uses-application-services-vb/_static/image14.jpg)](configuring-a-website-that-uses-application-services-vb/_static/image13.jpg)

**그림 5**: 관리자 수 새 사용자 계정 만들기 ([전체 크기 이미지를 보려면 클릭](configuring-a-website-that-uses-application-services-vb/_static/image15.jpg))


WSAT 체크 아웃의 모든 기능이 필요한 경우 [ *롤링 Your 직접 웹 사이트 관리 도구*](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx), 어떤 작성자에 Dan Clem 과정을 안내의 사용자 지정 WSAT 같은 도구를 작성 합니다. Dan (C#으로) 자신의 응용 프로그램의 소스 코드를 공유 하 고 호스팅된 웹 사이트에 추가 하기 위한 단계별 지침을 제공 합니다.

## <a name="summary"></a>요약

응용 프로그램 서비스 데이터베이스 구현을 사용 하는 웹 응용 프로그램을 배포 하는 경우 프로덕션 데이터베이스에 필요한 데이터베이스 개체를 먼저 확인 해야 합니다. 에 설명 된 기술을 사용 하 여 이러한 개체를 추가할 수는 *데이터베이스 배포* 자습서; 사용할 수 있습니다는 `aspnet_regsql.exe` 이 자습서에서 살펴본 것 처럼 도구입니다. 동기화에 대 한 기술 고 (이 사용자와 개발 환경에서 만든 역할 프로덕션에서 유효 해야 하는 경우에 중요) 개발 및 프로덕션 환경에서 사용 되는 응용 프로그램 이름 주위 센터 touched 우리는 밖의 문제 사용자 및 프로덕션 환경에서 역할을 관리 합니다.

만족도 매우 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [*ASP.NET SQL Server 등록 도구 (aspnet_regsql.exe)*](https://msdn.microsoft.com/library/ms229862.aspx)
- [*SQL Server에 대 한 응용 프로그램 서비스 데이터베이스 만들기*](https://msdn.microsoft.com/library/x28wfk74.aspx)
- [*SQL Server에서 멤버 자격 스키마 만들기*](../../older-versions-security/membership/creating-the-membership-schema-in-sql-server-vb.md)
- [*검사 하는 중 ASP.NET s 멤버 자격, 역할 및 프로필*](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [*자신의 웹 사이트 관리 도구를 롤링합니다.*](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)
- [*웹 사이트 보안 자습서*](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)
- [*웹 사이트 관리 도구 개요*](https://msdn.microsoft.com/library/yy40ytx0.aspx)

> [!div class="step-by-step"]
> [이전](configuring-the-production-web-application-to-use-the-production-database-vb.md)
> [다음](strategies-for-database-development-and-deployment-vb.md)
