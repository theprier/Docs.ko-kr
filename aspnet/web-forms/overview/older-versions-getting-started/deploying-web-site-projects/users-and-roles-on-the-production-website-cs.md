---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/users-and-roles-on-the-production-website-cs
title: 사용자 및 역할 프로덕션 웹 사이트 (C#) | Microsoft Docs
author: rick-anderson
description: ASP.NET 웹 사이트 관리 도구 (WSAT) 멤버 자격 및 역할 설정을 구성 하 고 만들기를 위한 웹 기반 사용자 인터페이스를 제공 편집을 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/09/2009
ms.topic: article
ms.assetid: dbc54313-5d05-4285-98b3-726edea6d0c9
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/users-and-roles-on-the-production-website-cs
msc.type: authoredcontent
ms.openlocfilehash: a97241cc41d2e2ffd923eafa5e09d5ea82a640f7
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37389960"
---
<a name="users-and-roles-on-the-production-website-c"></a>프로덕션 웹 사이트 (C#)의 사용자 및 역할
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[PDF 다운로드](http://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial16_CustomAWAT_cs.pdf)

> ASP.NET 웹 사이트 관리 도구 (WSAT) 및 만들기, 편집 및 삭제 사용자 및 역할 멤버 자격 및 역할 설정을 구성 하기 위한 웹 기반 사용자 인터페이스를 제공 합니다. 아쉽게도 WSAT 에서만 작동 localhost에서 방문할 때 브라우저를 통해 프로덕션 웹 사이트의 관리 도구에 연결할 수 없는 의미 합니다. 좋은 소식은 프로덕션의 사용자 및 역할을 관리할 수 있도록 하는 해결 방법이 있는지 보여 줍니다. 이 자습서는 등과 같은 해결이 방법을 살펴봅니다.


## <a name="introduction"></a>소개

다양 한 ASP.NET 2.0에 도입 되었습니다 *응용 프로그램 서비스*에 웹 응용 프로그램에 추가할 수 있는 구성 요소 서비스 제품군입니다. 도 서 리뷰 웹 사이트에 멤버 자격 및 역할 서비스를 다시 추가한 합니다 [ *서비스를 구성 하는 웹 사이트를 사용 하 여 응용 프로그램* 자습서](configuring-a-website-that-uses-application-services-cs.md)합니다. 멤버 자격 서비스 사용자 계정 만들기 및 관리를 용이 하 게 역할 서비스는 사용자 그룹으로 분류에 대 한 API를 제공 합니다. 도 서 리뷰 사이트에 세 개의 사용자 계정이-Scott, Jisun, 고 Alice-Scott과 Jisun 관리자 역할의 관리자가 단일 역할을 합니다.

ASP 합니다. NET의 응용 프로그램 서비스는 특정 구현에 연결 되지 않습니다. 특정 사용 하도록 응용 프로그램 서비스를 지시 하는 대신 *공급자*, 및 해당 공급자는 특정 기술을 사용 하 여 서비스를 구현 합니다. 사용 하 여도 서 리뷰 웹 응용 프로그램을 구성 했습니다 합니다 `SqlMembershipProvider` 및 `SqlRoleProvider` 멤버 자격 및 역할 서비스에 대 한 공급자입니다. 이러한 두 공급자는 SQL Server 데이터베이스에서 사용자 계정 및 역할 정보를 저장 하 고 웹 호스팅 회사에 호스팅된 인터넷 기반 웹 응용 프로그램에 대 한 가장 자주 사용 되는 공급자.

사용자 및 프로덕션 환경에서 역할 멤버 자격 및 역할 서비스를 사용 하 여 개발자를 위한 일반적인 문제를 관리 하는 합니다. 프로덕션 웹 사이트에서 사용자 계정 삭제, 새 역할을 추가 하거나 어떻게 기존 역할에 기존 사용자를 추가? 이 자습서에서는 프로덕션 웹 사이트의 사용자 및 역할을 관리 하기 위한 다양 한 기법을 살펴봅니다.

## <a name="using-the-aspnet-web-site-administration-tool"></a>ASP.NET 웹 사이트 관리 도구를 사용 하 여

ASP.NET에 포함 되어는 [웹 사이트 관리 도구](https://msdn.microsoft.com/library/yy40ytx0.aspx) (WSAT)는 손쉽게 사용자 계정 및 역할 만들기 및 관리 하 고 사용자 및 역할 기반 권한 부여 규칙을 지정할 수 있습니다. WSAT는를 사용 하려면 솔루션 탐색기에서 ASP.NET 구성 아이콘 또는 메뉴로 이동 하 여 웹 사이트 또는 프로젝트 및 ASP.NET 구성 옵션을 선택 합니다. 어느 방법이 든 웹 브라우저를 시작 하 고과 같은 주소에서 WSAT 가리키도록: `http://localhost:portNumber/asp.netwebadminfiles/default.aspx?applicationPhysicalPath=pathToApplication`

WSAT는 세 가지 섹션으로 구분 됩니다.

- **보안** -사용자, 역할 및 권한 부여 규칙을 관리 합니다.
- **ApplicationConfiguration** -관리 합니다 &lt;appSettings&gt; 및 여기에서 SMTP 설정 합니다. 있습니다 수도 오프 라인으로 응용 프로그램 및 디버깅 및 추적 여기에서 설정 관리 뿐만 기본 사용자 지정 오류 페이지를 지정 합니다.
- **ProviderConfiguration** -응용 프로그램 서비스에서 사용 하는 공급자를 구성 합니다.

보안 섹션 (에서처럼 **그림 1**) 새 사용자를 만들기, 사용자 관리, 만들기 및 역할을 관리 하 고 만들기 및 관리에 대 한 액세스 규칙에 대 한 링크가 포함 되어 있습니다. 여기에서 수 시스템에 새 역할을 추가, 기존 사용자를 삭제 또는 추가 또는 특정 사용자 계정에서 역할을 제거 합니다.

[![](users-and-roles-on-the-production-website-cs/_static/image2.png)](users-and-roles-on-the-production-website-cs/_static/image1.png)

**그림 1**: 사용자 및 역할 관리에 대 한 옵션을 포함 하는 WSAT 보안 섹션  
([클릭 하 여 큰 이미지 보기](users-and-roles-on-the-production-website-cs/_static/image3.png))

아쉽게도 WSAT는만 액세스할 수 있는 로컬. 원격 프로덕션 웹 사이트;에 WSAT를 방문할 수 없습니다. 방문 하는 경우 `www.yoursite.com/asp.netwebadminfiles/default.aspx` 404 찾을 수 없음 응답을 표시 합니다. WSAT 사용을 구동 하는 코드를 `Membership` 고 `Roles` 를 만들려면.NET Framework의 클래스를 편집 하 고 사용자 및 역할을 삭제 합니다. 이러한 클래스 사용에 어떤 공급자를 확인 하려면 웹 응용 프로그램의 구성 정보를 참조 하세요. 다시 합니다 [ *서비스를 구성 하는 웹 사이트를 사용 하 여 응용 프로그램* 자습서](configuring-a-website-that-uses-application-services-cs.md) 도 서 리뷰 웹 사이트를 사용 하 여 설정 합니다 `SqlMembershipProvider` 및 `SqlRoleProvider` 공급자. 추가이 뛰어나며 `<membership>` 하 고 `<roleManager>` 섹션을 `Web.config`입니다.

[!code-xml[Main](users-and-roles-on-the-production-website-cs/samples/sample1.xml)]

`<membership>` 및 `<roleManager>` 참조 섹션의 `SqlMembershipProvider` 및 `SqlRoleProvider` 의 공급자가 `type` 특성을 각각. 이러한 공급자는 지정된 된 SQL Server 데이터베이스에서 사용자 및 역할 정보를 저장합니다. 이러한 공급자에서 데이터베이스를 사용 하 여 지정 합니다 `connectionStringName` 특성인 `ReviewsConnectionString`에 정의 되어 있는 `~/ConfigSections/databaseConnectionStrings.config` 파일. 이전에 설명한 대로 합니다 `databaseConnectionStrings.config` 반면 파일 개발 환경에서 개발 데이터베이스에 연결 문자열을 포함 합니다 `databaseConnectionStrings.config` 프로덕션 데이터베이스에 연결 문자열을 포함 하는 프로덕션에서 파일입니다.

간단히 말해 WSAT는 개발 환경을 통해 로컬로 액세스할 수 있어야 합니다 및 지정 된 데이터베이스의 사용자 및 역할 정보를 사용 하 여 작동 합니다 `databaseConnectionStrings.config` 파일입니다. 따라서 연결 문자열 정보를 변경 하는 경우는 `databaseConnectionStrings.config` 파일 개발 환경에서 사용할 수 있습니다는 WSAT 로컬 사용자 및 프로덕션 환경에서 역할 관리 합니다.

이 기능을 설명 하기 위해 엽니다는 `databaseConnectionStrings.config` 개발 환경에서 Visual Studio에서 파일 및 프로덕션 데이터베이스 연결 문자열을 사용 하 여 개발 하는 데이터베이스 연결 문자열을 대체 합니다. WSAT는 시작, 보안 탭 이동 및 Sam 암호 "password!" 라는 새 사용자 추가 (작은 따옴표는 표시) 합니다. **그림 2** 이 계정을 만들 때 WSAT 화면을 보여 줍니다.

[![](users-and-roles-on-the-production-website-cs/_static/image5.png)](users-and-roles-on-the-production-website-cs/_static/image4.png)

**그림 2**: 프로덕션 환경에서 Sam 라는 새 사용자 만들기  
([클릭 하 여 큰 이미지 보기](users-and-roles-on-the-production-website-cs/_static/image6.png))

연결 문자열을 변경 했습니다 때문에 `databaseConnectionStrings.config` 프로덕션 데이터베이스 서버를 가리키도록 Sam은 프로덕션 환경에서 사용자로 추가 되었습니다. 이 확인 하려면에서 연결 문자열을 변경 합니다 `databaseConnectionStrings.config` 개발 데이터베이스에 파일을 살펴본는 `Login.aspx` 개발 환경에서 페이지. Sam로 로그인 하려고 (참조 **그림 3**).

[![](users-and-roles-on-the-production-website-cs/_static/image8.png)](users-and-roles-on-the-production-website-cs/_static/image7.png)

**그림 3**: 개발 환경에서 Sam으로 로그인 할 수 없습니다  
([클릭 하 여 큰 이미지 보기](users-and-roles-on-the-production-website-cs/_static/image9.png))

로그인 할 수 없습니다 Sam으로 개발 환경에서 사용자 계정 정보를 로컬 데이터베이스에 없기 때문에 있습니다. 보다는 프로덕션 데이터베이스에 추가 되었습니다. 이 확인 하려면의 내용 보기는 `aspnet_Users` 개발 및 프로덕션 데이터베이스의 테이블입니다. 개발 환경에서에 사용자 Scott, Jisun, Alice에 대 한 세 개의 레코드 없어야 합니다. 그러나는 `aspnet_Users` 프로덕션 데이터베이스의 테이블에 4 개의 레코드가: Scott, Jisun, Alice 및 Sam입니다. 따라서 개발 환경 통해서가 아니라 프로덕션 환경에서 웹 사이트를 통해 Sam 서명할 수 있습니다.

[![](users-and-roles-on-the-production-website-cs/_static/image11.png)](users-and-roles-on-the-production-website-cs/_static/image10.png)

**그림 4**: Sam 프로덕션 웹 사이트에 로그인 할 수 있습니다  
([클릭 하 여 큰 이미지 보기](users-and-roles-on-the-production-website-cs/_static/image12.png))

> [!NOTE]
> 연결 문자열을 변경 해야 합니다 `databaseConnectionStrings.config` 완료 되 면 다시 개발 데이터베이스에 파일의 연결 문자열 작업할 프로덕션 데이터를 사용 하 여 개발을 통해 사이트를 테스트할 때이 고 그렇지 WSAT 사용 환경입니다. 또한 염두에 앞에서 설명한 기법을 사용 하면 WSAT는 사용자 및 역할을 원격으로 관리 하는 데, 하는 동안 다른 WSAT 구성 옵션 (액세스 규칙, SMTP 설정, 디버깅 및 추적 설정 및 등) 중 하나에 대 한 변경 내용을 수정 합니다 `Web.config` 파일입니다. 따라서 설정을 변경에는 프로덕션 환경이 아닌 개발 환경에 적용 됩니다.


## <a name="creating-custom-user-and-role-management-web-pages"></a>사용자 및 역할 관리 웹 페이지 만들기

WSAT는 사용자 및 역할을 관리 하기 위한 상자 시스템의 부족을 제공 하지만 로컬로 실행할 수 있습니다 하며 프로덕션에서 역할과 사용자를 관리 하기 위해 연결 문자열 정보를 변경 합니다. 사용자 계정을 지 원하는 대부분의 웹 사이트에는 다양 한 사용자 및 역할 관리 웹 페이지를 통해 사이트 내의 페이지에서 사용자 및 역할을 관리 하려면 관리자가 포함 됩니다. 이러한 웹 기반 관리 페이지 훨씬 쉽게 사용자 및 역할을 관리 하 고 사이트에 필수적인 경우 많은 관리자 또는 관리자에 대 한 액세스 또는 Visual Studio는 WSAT를 시작 하는 데 기술적 배경 없는 있을 수 있습니다.

ASP.NET의 다양 한 끌어서 놓기 에서처럼 쉽지 이러한 관리 웹 페이지를 구현 하는 기본 제공 웹 로그인 관련 컨트롤 번호를 포함 합니다. 예를 들어, CreateUserWizard 컨트롤을 페이지로 끌어서 일부 속성을 설정 하 여 새 사용자 계정을 만들려면 관리자에 대 한 페이지를 만들 수 있습니다. 사실 에서처럼 WSAT에서 사용자를 만들기 위한 페이지 **그림 2** 페이지에 추가할 수 있는 동일한 CreateUserWizard 컨트롤을 사용 합니다. 또한 멤버 자격 및 역할 서비스의 기능을 통해 프로그래밍 방식으로 사용할 수는 `Membership` 및 `Roles` .NET Framework의 클래스입니다. 이러한 클래스를 사용 하 여 만들기, 편집 및 삭제 사용자 및 역할에도 역할에 사용자 추가 또는 제거에 대 한 어떤 역할에 사용자를 확인 하 고 다른 사용자 및 역할에 관련 된 작업을 수행 하는 코드를 작성할 수 있습니다.

에 [ *서비스를 구성 하는 웹 사이트를 사용 하 여 응용 프로그램* 자습서](configuring-a-website-that-uses-application-services-cs.md) 페이지를 추가 합니다 `Admin` 라는 폴더 `CreateAccount.aspx`합니다. 이 페이지에는 관리자가 사이트에 새 사용자 계정을 추가 하 고 새로 만든된 사용자가 관리자 역할에 있는지 여부를 지정할 수 있습니다 (참조 **그림 5**).

[![](users-and-roles-on-the-production-website-cs/_static/image14.png)](users-and-roles-on-the-production-website-cs/_static/image13.png)

**그림 5**: 관리자는 새 사용자 계정을 만들 수 있습니다  
([클릭 하 여 큰 이미지 보기](users-and-roles-on-the-production-website-cs/_static/image15.png))

에 대 한 자세한 사용에 대 한 단계별 지침과 함께 사용자 및 역할 관리 페이지를 구축 합니다 `Membership` 및 `Roles` 클래스 및 ASP.NET 웹 로그인 관련 컨트롤을 참조 해야 내 [웹 사이트 보안 자습서](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)합니다. 찾을 수 있습니다 지침 새 계정 만들기, 역할 만들기 및 관리를 위한 웹 페이지를 구축 하는 방법에 역할 및 다른 일반적인 관리 작업에 사용자를 할당 합니다.

프로덕션 웹 사이트의 WSAT 유사한 기능을 구현 하에 항상 고유한 일련의 WSAT의 기능을 구현 하는 웹 페이지를 빌드할 수 있습니다. 시작, 폴더에 위치한 WSAT 소스 코드를 체크 아웃 하는 데 `%WINDIR%\Microsoft.NET\Framework\v2.0.50727\ASP.NETWebAdminFiles`합니다. Dan Clem WSAT 대신이 문서의 공유 그는 사용 하는 다른 옵션도 [롤링 사용자 고유의 웹 사이트 관리 도구](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)합니다. Dan은 판독기 사용자 지정 WSAT 같은 도구를 빌드하는 과정을 안내 다운로드 (C#), 응용 프로그램의 소스 코드를 포함 하며 자신의 사용자 지정 WSAT 호스팅되는 웹 사이트를 추가 하기 위한 단계별 지침을 제공 합니다.

## <a name="summary"></a>요약

ASP.NET 웹 사이트 관리 도구 (WSAT) 웹 사이트에 대 한 사용자 및 역할 정보를 관리 하는 멤버 자격 및 역할 응용 프로그램 서비스를 사용 하 여 동시에 사용할 수 있습니다. 아쉽게도 WSAT만 액세스할 수 있는 로컬 이며 프로덕션 웹 사이트를 방문할 수 없습니다. 그러나 개발에서 연결 문자열을 변경 하 여 프로덕션 데이터베이스를 지점 환경 사용할 수는 WSAT 프로덕션 웹 사이트의 역할과 사용자를 관리할 수 합니다.

WSAT 접근 방식은 사용자 및 역할을 관리 하는 쉽고 빠르게 제공, 하는 동안 연결 문자열 정보를 임시 변경 뿐만 아니라 Visual Studio에서 WSAT 시작 해야 합니다. WSAT는 작업은 번거롭습니다 있고 없거나 Visual Studio와는 WSAT에 익숙하지 않은 관리자 또는 여러 관리자를 사용 하 여 웹 사이트에 대해 제대로 작동 하지 않습니다 프로덕션의 사용자 및 역할을 관리 하는 빠른 방법을 제공 합니다. 이러한 이유로, 사용자 계정을 지 원하는 대부분의 웹 사이트 관리 웹 페이지의 집합을 포함 합니다. WSAT는 필요 하지 않습니다 하 고 모든 컴퓨터에서 다양 한 관리자가 사용 하는 웹 페이지의 이러한 집합.

즐거운 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP를 검사 합니다. NET의 멤버 자격, 역할 및 프로필](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [고유한 웹 사이트 관리 도구를 롤링합니다.](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)
- [웹 사이트 관리 도구 개요](https://msdn.microsoft.com/library/yy40ytx0.aspx)
- [웹 사이트 보안 자습서](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)

> [!div class="step-by-step"]
> [이전](precompiling-your-website-cs.md)
> [다음](asp-net-hosting-options-vb.md)
