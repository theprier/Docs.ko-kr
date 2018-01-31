---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12
title: "SQL Server Compact Visual Studio를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: 1 / 12-소개 | Microsoft Docs"
author: tdykstra
description: "이 일련의 자습서 배포 하는 방법을 보여 줍니다. (게시) ASP.NET Visual Stu를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 웹 응용 프로그램 프로젝트..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/17/2011
ms.topic: article
ms.assetid: a2d7f33b-8c4a-4b48-9fb1-9139cf9b9878
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12
msc.type: authoredcontent
ms.openlocfilehash: 9c0edb301de85d15b9a3527382b72211f6f3d3ec
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-introduction---1-of-12"></a>SQL Server Compact Visual Studio를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: 1 / 12-소개
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 이 일련의 자습서 배포 하는 방법을 보여 줍니다. (게시)는 ASP.NET 웹에 대 한 Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 웹 응용 프로그램 프로젝트입니다. 웹 게시 업데이트를 설치 하는 경우에 Visual Studio 2010을 사용할 수 있습니다.
> 
> Visual Studio 2012 RC 릴리스 이후 도입 된 배포 기능을 표시, 이외의 SQL Server Compact, SQL Server 버전을 배포 하는 방법을 보여 줍니다. 및 Azure 앱 서비스 웹 앱을 배포 하는 방법을 보여 줍니다. 하는 자습서를 참조 하십시오. [ASP.NET 웹 배포 Visual Studio를 사용 하 여](../../deployment/visual-studio-web-deployment/introduction.md)합니다.
> 
> 이 자습서의 iis에 테스트를 위해 로컬 개발 컴퓨터 및 다음 타사 호스팅 공급자에 먼저 배포 하는 과정을 안내 합니다. 응용 프로그램을 배포 하는 응용 프로그램 데이터베이스 및 ASP.NET 멤버 자격 데이터베이스를 사용 합니다. 높아져 SQL Server Compact를 사용 하 여 SQL Server Compact를 배포 및 시작 하 고 이후 보여 주는 자습서 데이터베이스 변경 내용을 배포 하는 방법과 SQL Server로 마이그레이션하는 방법에 키를 누릅니다.
> 
> 이 자습서는 Visual Studio에서 ASP.NET을 사용 하는 방법을 알고 있다고 가정 합니다. 시작 하려면 먼저는 이렇게 하지 않으면는 [기본 ASP.NET Web Forms 자습서](../tailspin-spyworks/tailspin-spyworks-part-1.md) 또는 [기본 ASP.NET MVC 자습서](../../../../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)합니다.
> 
> 자습서를 직접 관련 되지 않는 질문 해야 하도록를 게시할 수 있습니다는 [ASP.NET 배포 포럼](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment)합니다.


## <a name="overview"></a>개요

이 자습서의 iis에 테스트를 위해 로컬 개발 컴퓨터 및 다음 타사 호스팅 공급자에 먼저 배포 하는 과정을 안내 합니다. 응용 프로그램을 배포 하는 응용 프로그램 데이터베이스 및 ASP.NET 멤버 자격 데이터베이스를 사용 합니다. 높아져 SQL Server Compact를 사용 하 여 SQL Server Compact를 배포 및 시작 하 고 이후 보여 주는 자습서 데이터베이스 변경 내용을 배포 하는 방법과 SQL Server로 마이그레이션하는 방법에 키를 누릅니다.

수의 자습서 – 모든 11 및 문제 해결 페이지-못할 적일 배포 프로세스입니다. 사실, 기본 절차는 사이트를 배포 하기 위한 자습서 집합의 상대적으로 작은 부분을 확인 합니다. 그러나 실제 상황에서 주로 해야 배포의 일부 작지만 중요 한 추가 측면에 대 한 정보-예를 들어 대상 서버에 폴더 사용 권한을 설정 합니다. 이러한 추가 기술 대부분 자습서에서는 실제 응용 프로그램을 성공적으로 배포에서 방해할 수 있는 정보 둬서는 안 기대와 자습서에 포함 되어 있습니다.

이 자습서는 순서 대로 실행 되도록 설계 하 고 이전 부분을 기반으로 하는 각 부분입니다. 그러나 상황에 맞는 관련이 없는 파트를 건너뛸 수 있습니다. (부분을 건너뜁니다 해야 이후의 자습서 절차를 조정할 수 있습니다.)

## <a name="intended-audience"></a>적용 대상

이 자습서는 소규모 조직 또는 기타 환경에서 작업 하는 ASP.NET 개발자를 대상으로 위치:

- 연속 통합 프로세스 (자동화 된 빌드 및 배포) 사용 되지 않습니다.
- 프로덕션 환경에는 제 3 자 호스팅 공급자입니다.
- 일반적으로 한 사람이 여러 역할 (동일인일 개발, 테스트에 대해 수행 하 고 배포)를 채웁니다.

엔터프라이즈 환경에서 연속 통합 프로세스를 구현 하는 보다 일반적인 사용 되며 프로덕션 환경에 일반적으로 회사의 서버에서 호스팅됩니다. 일반적으로 각기 다른 사용자가 다른 역할을 수행 합니다. 엔터프라이즈 배포에 대 한 정보를 참조 하십시오. [엔터프라이즈 시나리오에서 웹 응용 프로그램 배포](../../deployment/deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)합니다.

모든 규모의 웹 응용 프로그램을 Azure에 배포할 수도 및 대부분의 이러한 자습서에 표시 된 절차는 Azure 앱 서비스 웹 앱에도 적용 합니다. Azure에 대 한 소개를 참조 하십시오. [https://azure.microsoft.com](https://azure.microsoft.com)합니다.

## <a name="the-hosting-provider-shown-in-the-tutorials"></a>이 자습서에 표시 된 호스팅 공급자

이 자습서에서는 호스팅 회사 계정을 설정 하 고 해당 호스팅 공급자에 게 응용 프로그램 배포 과정을 안내 합니다. 특정 호스팅 업체는 자습서는 라이브 웹 사이트에 배포 하는 전체 환경을 보여 수 있도록 선택 되었습니다. 다양 한 기능을 제공 하는 각 호스팅 회사 및 해당 서버에 배포의 경험에 따라 다양 합니다. 그러나이 자습서에 설명 된 프로세스는 전체 프로세스에 대 한 일반.

Cytanium.com,이 자습서에 사용 되는 호스팅 공급자 중 하나를 사용할 수 있는 많은 이며를 보증 하거나 권장으로 간주 되지 않으며이 자습서에 사용 합니다.

## <a name="deploying-web-site-projects"></a>웹 사이트 프로젝트 배포

Contoso 대학 Visual Studio 웹 응용 프로그램 프로젝트입니다. 대부분의 배포 방법 및이 자습서에서 설명 하는 도구에는 적용 되지 않습니다 [웹 사이트 프로젝트](https://msdn.microsoft.com/library/dd547590.aspx)합니다. 웹 사이트 프로젝트를 배포 하는 방법에 대 한 정보를 참조 하십시오. [ASP.NET 배포 콘텐츠 맵](https://msdn.microsoft.com/library/bb386521.aspx#deployment_for_web_site_projects)합니다.

## <a name="deploying-aspnet-mvc-projects"></a>ASP.NET MVC 프로젝트 배포

이 자습서에 대 한 ASP.NET Web Forms 프로젝트를 배포한 있지만 작업을 수행 하는 방법을 배웁니다 모든 항목 에서도 ASP.NET MVC에 적용 됩니다. Visual Studio MVC 프로젝트는 또 다른 형태 웹 응용 프로그램 프로젝트입니다. 유일한 차이점은 ASP.NET MVC 또는의 대상 버전을 지원 하지 않는 호스팅 공급자를 배포 하는 경우 해야 하는 적절 한 설치 되어 있는지 ([MVC 3](http://nuget.org/packages/AspNetMvc/3.0.20105.0) 또는 [MVC 4](http://nuget.org/packages/aspnetmvc)) 프로젝트에서 NuGet 패키지 합니다.

## <a name="programming-language"></a>프로그래밍 언어

샘플 응용 프로그램을 사용 하 여 C# 자습서에서는 C#에 대 한 지식이 필요 하지 않습니다 있고 자습서에 설명 된 배포 방법 언어 관련 없는 합니다.

## <a name="troubleshooting-during-this-tutorial"></a>이 자습서에서 문제 해결

배포 하는 동안 오류가 발생 하거나 배포 된 사이트 올바르게 실행 되지 않은 경우에 항상 오류 메시지 솔루션을 제공 하지 않습니다. 몇 가지 일반적인 문제 시나리오에 대 한 도움는 [참조 페이지의 문제 해결](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md) 를 사용할 수 있습니다. 오류 메시지가 자습서를 진행할 때 작동 하지 않는 경우 문제 해결 페이지를 확인 해야 합니다.

## <a name="comments-welcome"></a>주석 시작

이 자습서에 대 한 의견을 기다리겠습니다, 하 고 자습서 업데이트 될 때 모든 노력 됩니다 계정 수정 또는 제안이 자습서 주석에서 제공 되는 향상 된 기능에 대 한 고려 되도록 합니다.

## <a name="prerequisites"></a>필수 구성 요소

시작 하기 전에 Windows 7 이상 있고 컴퓨터에 설치 된 다음 제품 중 하나에 있는지 확인 합니다.

- [Visual Studio 2010 SP1](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)
- [Visual Web Developer Express 2010 SP1](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VWD2010SP1Pack)
- [Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC for Web](https://go.microsoft.com/fwlink/?LinkId=240162)

Visual Studio 2010 SP1 또는 Visual Web Developer Express 2010 SP1를 설정한 경우 다음 제품이 설치:

- [Azure SDK for.NET (VS 2010 SP1)](https://go.microsoft.com/fwlink/?LinkID=208120) (웹 게시 업데이트 포함)
- [Microsoft Visual Studio 2010 SP1 도구 for SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCEVSTools)

자습서를 완료 하는 데 필요한 다른 소프트웨어 있지만 아직 로드 있이 필요가 없습니다. 자습서는 필요할 때 설치 단계를 안내 합니다.

## <a name="downloading-the-sample-application"></a>샘플 응용 프로그램 다운로드

배포 하는 응용 프로그램은 Contoso 대학,를 이미 만들었습니다. 에 설명 된 Contoso 대학 응용 프로그램을 느슨하게 기반 대학 웹 사이트의 단순화 된 버전의 [ASP.NET 사이트의 Entity Framework 자습서](https://asp.net/entity-framework/tutorials)합니다.

필수 구성 요소가 설치 되어 있는 경우 다운로드는 [Contoso 대학 웹 응용 프로그램](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)합니다. *.zip* 프로젝트 및 모든 12 자습서를 포함 하는 PDF 파일의 여러 버전이 포함 되어 있습니다. 자습서의 단계를 진행 하려면 ContosoUniversity Begin 사용을 시작 합니다. 이 자습서의 끝에 프로젝트 모양을 보려면 ContosoUniversity 끝을 엽니다. 프로젝트의 모양을 10 자습서의 전체 SQL Server로 마이그레이션을 시작 하기 전에 보려면 ContosoUniversity AfterTutorial09를 엽니다.

자습서 단계를 진행 하도록 준비를 하려면 Visual Studio 프로젝트를 사용 하기 위한 사용 하 여 모든 폴더에 저장을 ContosoUniversity 시작 합니다. 기본적으로이 다음 폴더입니다.

`C:\Users\<username>\Documents\Visual Studio 2012\Projects`

(이 자습서의 스크린 샷을 프로젝트 폴더는 루트 디렉터리에서에 있습니다는 `C`: 드라이브입니다.)

Visual Studio를 시작 하 고 프로젝트를 열고 실행 하려면 CTRL + f 5를 누릅니다.

[![Home_page](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image2.png)](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image1.png)

웹 사이트 페이지의 메뉴 모음에서 액세스할 수 있으며 다음 기능을 수행할 수 있도록 합니다.

- 학생 통계 (정보 페이지)를 표시 합니다.
- 표시, 편집, 삭제 및 학생 들을 추가 합니다.
- 표시 및 편집 과정입니다.
- 표시 하 고 강사를 편집 합니다.
- 표시 하 고 부서를 편집 합니다.

다음은 몇 가지 대표 페이지의 스크린 샷을 합니다.

[![Students_Page](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image4.png)](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image3.png)

[![Add_Students_Page](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image6.png)](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image5.png)

## <a name="reviewing-application-features-that-affect-deployment"></a>배포에 영향을 주는 응용 프로그램 기능을 검토 합니다.

응용 프로그램의 다음 기능에 배포 하는 방법 또는 배포를 수행 해야 하면 영향을 줍니다. 이러한 각 계열에는 다음 자습서에서 자세히 설명 합니다.

- Contoso 대학 학생과 강사 이름과 같은 응용 프로그램 데이터를 저장할 SQL Server Compact 데이터베이스를 사용 합니다. 데이터베이스에 테스트 데이터 및 프로덕션 데이터의 혼합 하 고 프로덕션 환경에 배포 하는 경우 테스트 데이터를 제외 하도록 해야 합니다. 자습서 시리즈의 뒷부분에 나오는 SQL Server에 SQL Server Compact에서 마이그레이션할 수 있습니다.
- 응용 프로그램이 SQL Server Compact 데이터베이스의 사용자 계정 정보를 저장 하는 ASP.NET 멤버 자격 시스템을 사용 합니다. 응용 프로그램에는 몇 가지 제한 된 정보에 대 한 액세스 권한이 있는 관리자가 사용자를 정의 합니다. 관리자 계정 하나 있지만 해도 테스트 계정을 멤버 자격 데이터베이스를 배포 해야 합니다.
- 응용 프로그램 데이터베이스 및 멤버 자격 데이터베이스를 사용 하므로 SQL Server Compact는 데이터베이스 엔진으로 데이터베이스 자체 뿐만 아니라 호스팅 공급자에 데이터베이스 엔진을 배포 해야 합니다.
- 응용 프로그램 멤버 자격 시스템 SQL Server Compact 데이터베이스에 데이터를 저장할 수 있도록 ASP.NET 유니버설 멤버 자격 공급자를 사용 합니다. 범용 멤버 자격 공급자를 포함 하는 어셈블리는 응용 프로그램과 함께 배포 되어야 합니다.
- 응용 프로그램 데이터는 응용 프로그램 데이터베이스에 액세스 하는 Entity Framework 5.0을 사용 합니다. Entity Framework 5.0을 포함 하는 어셈블리는 응용 프로그램과 함께 배포 되어야 합니다.
- 응용 프로그램 공급 업체 오류 로깅 및 보고 유틸리티를 사용 합니다. 이 유틸리티는 응용 프로그램과 함께 배포 되어야 하는 어셈블리에 제공 됩니다.
- 오류 로깅 유틸리티 파일 폴더에 XML 파일에 오류 정보를 기록 합니다. ASP.NET에 배포 된 사이트에서 실행 되는 계정에이 폴더에 대 한 쓰기 권한이 있고 배포에서이 폴더를 제외 해야 있는지 확인 해야 합니다. (그렇지 않은 경우 오류 로그 데이터는 테스트 환경에서 프로덕션에 배포할 수 있으며 및/또는 프로덕션 오류 로그 파일을 삭제 될 수 있습니다.)
- 응용 프로그램에 배포 된에서 변경 되어야 하는 일부 설정을 포함 *Web.config* 대상 환경 (테스트 또는 프로덕션) 및 빌드에 따라 변경 해야 하는 기타 설정에 따라 파일 구성 (디버그 또는 릴리스)입니다.
- Visual Studio 솔루션에는 클래스 라이브러리 프로젝트에 포함 됩니다. 이 프로젝트에서 생성 하는 어셈블리에만 배포할지 프로젝트 자체입니다.

이 시리즈의 첫 번째 자습서에서는 샘플 Visual Studio 프로젝트를 다운로드 한 있고 응용 프로그램을 배포 하는 방법에 영향을 주는 사이트 기능을 검토 합니다. 다음 자습서에서 자동으로 처리 되도록 이러한 기능 중 일부를 설정 하 여 배포를 위해 준비할 수 있습니다. 다른 수동으로 처리할 수 있습니다.

>[!div class="step-by-step"]
[다음](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md)
