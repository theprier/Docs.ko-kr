---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/users-and-roles-on-the-production-website-cs
title: 사용자 및 역할 프로덕션 웹 사이트 (C#) | Microsoft Docs
author: rick-anderson
description: 멤버 자격 및 역할 설정을 구성 하기 위한 및 만들기, 웹 기반 사용자 인터페이스를 제공 하는 ASP.NET 웹 사이트 관리 도구 (WSAT) 편집는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/09/2009
ms.topic: article
ms.assetid: dbc54313-5d05-4285-98b3-726edea6d0c9
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/users-and-roles-on-the-production-website-cs
msc.type: authoredcontent
ms.openlocfilehash: e3e1165959ae47715e0037db7a3bc6ac58807653
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30888294"
---
<a name="users-and-roles-on-the-production-website-c"></a>사용자 및 역할 프로덕션 웹 사이트 (C#)
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[PDF 다운로드](http://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial16_CustomAWAT_cs.pdf)

> ASP.NET 웹 사이트 관리 도구 (WSAT) 및 만들기, 편집 및 삭제 사용자 및 역할 멤버 자격 및 역할 설정을 구성 하기 위한 웹 기반 사용자 인터페이스를 제공 합니다. 그러나는 WSAT 에서만 작동 localhost에서 열어 볼 때 프로덕션 웹 사이트 관리 도구 브라우저를 통해 도달할 수 있음을 의미 합니다. 다행히도 사용자 및 프로덕션에 대 한 역할을 관리할 수 있도록 해결 방법을 않는다는 것입니다. 이 자습서에서는 이러한 해결 방법 및 기타 보고서를 살펴봅니다.


## <a name="introduction"></a>소개

ASP.NET 2.0에는 다양 한 도입 *응용 프로그램 서비스*는 웹 응용 프로그램에 추가할 수 있는 구성 요소 서비스의 모음입니다. 책 검토 웹 사이트에 멤버 자격 및 역할 서비스를 다시 추가 [ *서비스를 구성 하는 웹 사이트를 사용 하 여 응용 프로그램* 자습서](configuring-a-website-that-uses-application-services-cs.md)합니다. 사용자 계정 만들기 및 관리,을 용이 하 게 멤버 자격 서비스 역할 서비스는 사용자를 그룹으로 분류 하기 위한 API를 제공 합니다. 책 검토 사이트에 있는 3 개의 사용자 계정을-Scott, Jisun, 및 Alice-및 Scott 및 관리자 역할의 Jisun Admin, 단일 역할을 합니다.

ASP입니다. NET의 응용 프로그램 서비스는 특정 구현에 연결 되지 않습니다. 특정을 사용 하는 응용 프로그램 서비스를 지시 하는 대신, *공급자*, 해당 공급자 특정 기술을 사용 하 여 서비스를 구현 하 고 있습니다. 책 검토 웹 응용 프로그램 사용 하도록 구성한는 `SqlMembershipProvider` 및 `SqlRoleProvider` 멤버 자격 및 역할 서비스에 대 한 공급자입니다. 이러한 두 공급자는 SQL Server 데이터베이스의 사용자 계정과 역할 정보를 저장 하 고는 웹 호스팅 회사에 호스팅된 인터넷 기반 웹 응용 프로그램에 대 한 가장 자주 사용 되는 공급자.

사용자 및 프로덕션 환경에 대 한 역할 멤버 자격 및 역할 서비스를 사용 하는 개발자를 위한 일반적인 과제는 관리입니다. 어떻게 않는 프로덕션 웹 사이트에서 사용자 계정을 삭제, 새 역할을 추가 하거나 기존 사용자 기존 역할에? 이 자습서에는 사용자 및 프로덕션 웹 사이트에 대 한 역할을 관리 하기 위한 다양 한 기술을 탐색 합니다.

## <a name="using-the-aspnet-web-site-administration-tool"></a>ASP.NET 웹 사이트 관리 도구를 사용 하 여

ASP.NET에 포함 되어는 [웹 사이트 관리 도구](https://msdn.microsoft.com/library/yy40ytx0.aspx) (WSAT)을 쉽게 만들고 사용자 계정과 역할을 관리 하 고 사용자 및 역할 기반 권한 부여 규칙을 지정할 수 있습니다. WSAT를 사용 하려면 솔루션 탐색기에서 ASP.NET 구성 아이콘을 클릭 하 고 또는 웹 사이트 또는 프로젝트 메뉴에서 ASP.NET 구성 옵션을 선택 합니다. 어느 방법이 든 웹 브라우저를 시작 하 고 같은 주소에서 WSAT 가리키는: `http://localhost:portNumber/asp.netwebadminfiles/default.aspx?applicationPhysicalPath=pathToApplication`

WSAT는 세 개의 섹션으로 구분 됩니다.

- **보안** -사용자, 역할 및 권한 부여 규칙을 관리 합니다.
- **ApplicationConfiguration** -관리는 &lt;appSettings&gt; 및 여기에서 SMTP 설정 합니다. 있습니다 수 또한 오프 라인 상태로 응용 프로그램 및 디버깅 및 추적 여기에서 설정 관리으로 기본 사용자 지정 오류 페이지를 지정 합니다.
- **ProviderConfiguration** -응용 프로그램 서비스에서 사용 하는 공급자를 구성 합니다.

보안 섹션 (에서처럼 **그림 1**) 새 사용자 만들기, 사용자 관리, 만들기 및 역할을 관리 하 고 만들기 및 관리에 대 한 액세스 규칙에 대 한 링크도 제공 합니다. 여기에서 수 시스템에 새 역할을 추가, 기존 사용자를 삭제 또는 추가 또는 특정 사용자 계정에서 역할을 제거 합니다.

[![](users-and-roles-on-the-production-website-cs/_static/image2.png)](users-and-roles-on-the-production-website-cs/_static/image1.png)

**그림 1**: WSAT 보안 섹션에는 사용자 및 역할을 관리 하기 위한 옵션을 포함  
([전체 크기 이미지를 보려면 클릭](users-and-roles-on-the-production-website-cs/_static/image3.png))

그러나이 WSAT는만 액세스할 수 있는 로컬. 원격 프로덕션 웹 사이트;에 WSAT 방문 수 없습니다. 방문 하는 경우 `www.yoursite.com/asp.netwebadminfiles/default.aspx` 404 찾을 수 없음 응답을 받을입니다. WSAT 사용 하 여를 구동 하는 코드는 `Membership` 및 `Roles` 를 만들려면.NET Framework의 클래스를 편집 하 고 사용자 및 역할을 삭제 합니다. 이러한 클래스를 지정 해야 합니다. 어떤 공급자를 확인 하려면 웹 응용 프로그램의 구성 정보를 참조 하십시오. 에 [ *서비스를 구성 하는 웹 사이트를 사용 하 여 응용 프로그램* 자습서](configuring-a-website-that-uses-application-services-cs.md) 책 검토 웹 사이트에서 사용 하도록 설정 하는 `SqlMembershipProvider` 및 `SqlRoleProvider` 공급자입니다. 추가 포함이 `<membership>` 및 `<roleManager>` 를 섹션 `Web.config`합니다.

[!code-xml[Main](users-and-roles-on-the-production-website-cs/samples/sample1.xml)]

`<membership>` 및 `<roleManager>` 참조 섹션는 `SqlMembershipProvider` 및 `SqlRoleProvider` 의 공급자가 `type` 특성도 각각. 이러한 공급자 지정된 된 SQL Server 데이터베이스의 사용자 및 역할 정보를 저장합니다. 이러한 공급자에서 데이터베이스를 사용 하 여 지정 된 `connectionStringName` 특성 `ReviewsConnectionString`에 정의 된는 `~/ConfigSections/databaseConnectionStrings.config` 파일입니다. 이전에 설명한 대로 `databaseConnectionStrings.config` 반면 개발 데이터베이스를 연결 문자열을 포함 하는 개발 환경에서 파일의 `databaseConnectionStrings.config` 파일 프로덕션에서 프로덕션 데이터베이스에 연결 문자열을 포함 합니다.

간단히 말해서는 WSAT 개발 환경을 통해 로컬로 액세스 해야 하 고에 지정 된 데이터베이스의 사용자 및 역할 정보 사용 방식과 `databaseConnectionStrings.config` 파일입니다. 따라서 연결 문자열 정보를 변경 하면는 `databaseConnectionStrings.config` 파일 개발 환경에서 사용 하 여는 WSAT 로컬로 프로덕션 환경에서 사용자 및 역할을 관리 합니다.

이 기능을 설명 하기 위해 엽니다는 `databaseConnectionStrings.config` 개발 환경에서 Visual Studio에서 파일을 프로덕션 데이터베이스 연결 문자열과 함께 개발 데이터베이스 연결 문자열을 대체 합니다. WSAT 실행 보안 탭으로 이동 하 고 Sam 암호 "password!" 라는 새 사용자 추가 (작은 따옴표가). **그림 2** 이 계정을 만들 때 WSAT 화면을 보여 줍니다.

[![](users-and-roles-on-the-production-website-cs/_static/image5.png)](users-and-roles-on-the-production-website-cs/_static/image4.png)

**그림 2**: 프로덕션 환경에 Sam 라는 새 사용자 만들기  
([전체 크기 이미지를 보려면 클릭](users-and-roles-on-the-production-website-cs/_static/image6.png))

연결 문자열을 변경 했습니다 때문에 `databaseConnectionStrings.config` 프로덕션 데이터베이스 서버를 가리키도록 Sam은 프로덕션 환경에 사용자로 추가 되었습니다. 이 확인 하려면 변경에서 연결 문자열은 `databaseConnectionStrings.config` 개발 데이터베이스에 다시 파일을 방문는 `Login.aspx` 개발 환경에서 페이지. Sam로에 로그인 하려고 (참조 **그림 3**).

[![](users-and-roles-on-the-production-website-cs/_static/image8.png)](users-and-roles-on-the-production-website-cs/_static/image7.png)

**그림 3**: 개발 환경에서 Sam으로 로그인 할 수 없습니다  
([전체 크기 이미지를 보려면 클릭](users-and-roles-on-the-production-website-cs/_static/image9.png))

로그인 할 수 없습니다 Sam로 개발 환경에서 사용자 계정 정보 로컬 데이터베이스에 존재 하지 않습니다. 보다는 프로덕션 데이터베이스에 추가 되었습니다. 이 확인 하려면의 내용 보기는 `aspnet_Users` 개발 및 프로덕션 데이터베이스의 테이블입니다. 개발 환경에서 사용자가 Scott, Jisun, Alice에 대 한 레코드를 3 개만 있을 것입니다. 그러나는 `aspnet_Users` 프로덕션 데이터베이스의 테이블에 4 개의 레코드가: Scott, Jisun, Alice 및 Sam 합니다. 따라서 프로덕션 환경에서 웹 사이트를 통해 있지만 개발 환경 통해서가 아니라 Sam에 로그인 수 있습니다.

[![](users-and-roles-on-the-production-website-cs/_static/image11.png)](users-and-roles-on-the-production-website-cs/_static/image10.png)

**그림 4**: Sam 프로덕션 웹 사이트에 로그인 할 수  
([전체 크기 이미지를 보려면 클릭](users-and-roles-on-the-production-website-cs/_static/image12.png))

> [!NOTE]
> 연결 문자열을 변경 하려면 반드시는 `databaseConnectionStrings.config` 완료 되 면 다시 개발 데이터베이스에 파일의 연결 문자열에서 개발 사이트를 테스트할 때 프로덕션 데이터와 함께 작업 합니다 WSAT 그렇지 않으면 작업 환경입니다. 또한 유념 지금까지 설명한 기술을 사용자 및 역할을 원격으로 관리 하는 WSAT를 사용할 수 있습니다, 하는 동안 다른 WSAT 구성 옵션 (액세스 규칙, SMTP 설정, 디버깅 및 추적 설정 및 등)에 대 한 변경의 를수정하는`Web.config` 파일입니다. 따라서 설정에 대 한 변경 내용을 프로덕션 환경이 아닌 개발 환경에 적용 됩니다.


## <a name="creating-custom-user-and-role-management-web-pages"></a>사용자 지정 사용자 및 역할 관리 웹 페이지 만들기

WSAT 사용자 및 역할을 관리 하기 위한 상자 시스템의 부족을 제공 하지만 로컬로 실행할 수 있습니다으로 이루어지며 사용자 및 프로덕션에 대 한 역할을 관리 하기 위해 연결 문자열 정보를 변경 하기. 사용자 계정을 지 원하는 대부분의 웹 사이트에는 다양 한 사용자 및 관리자는 사이트의 페이지에서 사용자 및 역할을 관리할 수 있도록 역할 관리 웹 페이지 포함 되어 있습니다. 이러한 웹 기반 관리 페이지 훨씬 쉬워집니다 사용자 및 역할을 관리 하 고 사이트에 필수적인 많은 관리자 또는 관리자가 없는 WSAT를 시작 하기 위해 Visual Studio를 사용 하 여 기술 배경 또는에 액세스할 수 있게 될 수 있습니다.

끌어서 놓기 만큼 쉬운 이렇게 관리 웹 페이지의 많은 구현 하는 기본 웹 로그인 관련 컨트롤의 ASP.NET에 있습니다. 예를 들어 관리자가 페이지로 CreateUserWizard 컨트롤을 끌어서 일부 속성을 설정 하 여 새 사용자 계정을 만들 수에 대 한 페이지를 만들 수 있습니다. 사실, 페이지에 표시 된 WSAT 사용자가 만들기 위한 **그림 2** 페이지에 추가할 수 있는 동일한 CreateUserWizard 컨트롤을 사용 합니다. 또한 구성원 자격 및 역할 서비스 기능을 통해 프로그래밍 방식으로 사용할 수는 `Membership` 및 `Roles` .NET Framework의 클래스. 이러한 클래스와 함께 만들기, 편집 및 삭제 사용자 및 역할을도 사용자 역할에 추가 또는 제거에 대 한 어떤 역할에 사용자가을 확인 하 고 다른 사용자 및 역할 관련 작업을 수행 하는 코드를 작성할 수 있습니다.

에 [ *서비스를 구성 하는 웹 사이트를 사용 하 여 응용 프로그램* 자습서](configuring-a-website-that-uses-application-services-cs.md) 페이지를 추가 했지만 `Admin` 라는 폴더 `CreateAccount.aspx`합니다. 이 페이지에서는 관리자가 사이트에 새 사용자 계정을 추가 하 고 새로 만든된 사용자가 관리자 역할에 있는지 여부를 지정할 수 (참조 **그림 5**).

[![](users-and-roles-on-the-production-website-cs/_static/image14.png)](users-and-roles-on-the-production-website-cs/_static/image13.png)

**그림 5**: 관리자는 새 사용자 계정을 만들 수 있습니다  
([전체 크기 이미지를 보려면 클릭](users-and-roles-on-the-production-website-cs/_static/image15.png))

사용자 및 역할 관리 페이지를 사용 하 여 대 한 단계별 지침과 빌드에 대해 보다 자세한에 대 한는 `Membership` 및 `Roles` 클래스와 ASP.NET 웹 로그인 관련 컨트롤 내용을 반드시 내 [웹 사이트 보안 자습서](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)합니다. 찾을 수 있습니다 지침 새 계정 만들기, 만들고 역할을 관리 하기 위한 웹 페이지를 작성 하는 방법에 역할 및 기타 일반 관리 작업에 사용자를 지정 합니다.

프로덕션 웹 사이트에서 WSAT 유사한 기능을 구현 하려면 사용자 고유의 일련 WSAT의 기능을 구현 하는 웹 페이지의 항상 작성할 수 있습니다. 시작 하십시오. % 폴더에 있는 WSAT 소스 코드를 체크 아웃 `%WINDIR%\Microsoft.NET\Framework\v2.0.50727\ASP.NETWebAdminFiles`합니다. 가 작성 한 문서를 공유 그 Dan Clem WSAT 대체를 사용 하 여 또 다른 옵션은 [롤링 Your 직접 웹 사이트 관리 도구](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)합니다. Dan은 판독기는 사용자 지정 WSAT와 유사한 도구를 만드는 과정을 단계별로 안내 합니다., (C#에서) 다운로드에 대 한 자신의 응용 프로그램의 소스 코드를 포함 및 그의 사용자 지정 WSAT 호스팅되는 웹 사이트를 추가 하기 위한 단계별 지침을 제공 합니다.

## <a name="summary"></a>요약

ASP.NET 웹 사이트 관리 도구 (WSAT) 웹 사이트에 대 한 사용자 및 역할 정보를 관리 하는 멤버 자격 및 역할 응용 프로그램 서비스와 함께에서 사용할 수 있습니다. 안타깝게도,는 WSAT만 액세스할 수 있는 로컬 있으며 프로덕션 웹 사이트를 방문할 수 없습니다. 그러나 개발에서 연결 문자열을 변경 하 여 프로덕션 데이터베이스를 가리킬 환경을 사용할 수는 WSAT 사용자 및 프로덕션 웹 사이트에 대 한 역할을 관리 하 합니다.

사용자 및 역할을 관리 하는 빠르고 쉬운 방법을 제공 하는 WSAT 접근을 하는 동안 연결 문자열 정보를 임시 변경을 Visual Studio에서 WSAT 시작 해야 합니다. WSAT 사용자 및 프로덕션 환경에 대 한 역할을 관리 하는 빠른 방법을 제공 하지만 것이 복잡 하 고 여러 관리자 또는 관리자에 게 없거나 Visual Studio와는 WSAT 익숙하지 않은 웹 사이트에 대해 제대로 작동 하지 않습니다. 이러한 이유로, 사용자 계정을 지 원하는 대부분의 웹 사이트 관리 웹 페이지의 집합을 포함 합니다. 이러한 웹 페이지는 WSAT 하지 않아도 집합과 모든 컴퓨터에서 다양 한 관리 사용자가 사용 합니다.

만족도 매우 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP를 검사 합니다. NET의 멤버 자격, 역할 및 프로필](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [자신의 웹 사이트 관리 도구를 롤링합니다.](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)
- [웹 사이트 관리 도구 개요](https://msdn.microsoft.com/library/yy40ytx0.aspx)
- [웹 사이트 보안 자습서](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)

> [!div class="step-by-step"]
> [이전](precompiling-your-website-cs.md)
> [다음](asp-net-hosting-options-vb.md)
