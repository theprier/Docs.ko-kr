---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12
title: 'SQL Server Compact Visual Studio를 사용 하 여를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: 소개-12 1 | Microsoft Docs'
author: tdykstra
description: 이 시리즈의 자습서에서는 배포 하는 방법을 보여 줍니다 (게시) ASP.NET 웹 응용 프로그램 프로젝트 Visual Stu를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/17/2011
ms.topic: article
ms.assetid: a2d7f33b-8c4a-4b48-9fb1-9139cf9b9878
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12
msc.type: authoredcontent
ms.openlocfilehash: 4a790fa72568caafdb2fab5efd9f334919c23719
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37398273"
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-introduction---1-of-12"></a>SQL Server Compact Visual Studio를 사용 하 여를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: 소개-12 1
====================
[Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 이 시리즈의 자습서에서는 배포 하는 방법을 보여 줍니다 (게시) ASP.NET 웹용 Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 웹 응용 프로그램 프로젝트입니다. Visual Studio 2010 웹 게시 업데이트를 설치 하는 경우에 사용할 수 있습니다.
> 
> Visual Studio 2012 RC 출시 이후 도입 된 배포 기능을 보여 줍니다, 이외의 SQL Server Compact, SQL Server 버전을 배포 하는 방법을 보여 줍니다 및 Azure App Service Web Apps를 배포 하는 방법을 보여 줍니다 하는 자습서를 참조 하세요 [ASP.NET 웹 배포 Visual Studio를 사용 하 여](../../deployment/visual-studio-web-deployment/introduction.md)입니다.
> 
> 이 자습서는 테스트를 위해 로컬 개발 컴퓨터에 IIS 및 타사 호스팅 공급자를 먼저 배포를 안내 합니다. 응용 프로그램을 배포 하는 응용 프로그램 데이터베이스 및 ASP.NET 멤버 자격 데이터베이스를 사용 합니다. SQL Server Compact를 사용 하 여 및 SQL Server Compact로 배포를 시작 하 고 나중에 자습서 보여드리겠습니다 데이터베이스 변경 내용을 배포 하는 방법 및 SQL Server로 마이그레이션하는 방법.
> 
> 이 자습서는 Visual Studio에서 ASP.NET을 사용 하는 방법을 알고 있다고 가정 합니다. 시작 하는 것이 좋습니다는 이렇게 하지 않으면를 [기본 ASP.NET Web Forms 자습서](../tailspin-spyworks/tailspin-spyworks-part-1.md) 또는 [기본 ASP.NET MVC 자습서](../../../../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)합니다.
> 
> 에 자습서로 직접 관련 되지 않은 질문이 있을 경우 게시할 수 하는 [ASP.NET 배포 포럼](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment)합니다.


## <a name="overview"></a>개요

이 자습서는 테스트를 위해 로컬 개발 컴퓨터에 IIS 및 타사 호스팅 공급자를 먼저 배포를 안내 합니다. 응용 프로그램을 배포 하는 응용 프로그램 데이터베이스 및 ASP.NET 멤버 자격 데이터베이스를 사용 합니다. SQL Server Compact를 사용 하 여 및 SQL Server Compact로 배포를 시작 하 고 나중에 자습서 보여드리겠습니다 데이터베이스 변경 내용을 배포 하는 방법 및 SQL Server로 마이그레이션하는 방법.

숫자 자습서-모든 11 및 문제 해결 페이지-수 확인 하기가 어렵게 생각 하는 배포 프로세스입니다. 실제로 사이트 배포에 대 한 기본 절차 자습서 집합의 상대적으로 작은 부분을 구성 합니다. 그러나 실제 상황에서 경우가 배포의 일부 작지만 중요 한 추가 측면에 대 한 정보-예를 들어 대상 서버의 폴더 사용 권한을 설정 합니다. 자습서를 성공적으로 실제 응용 프로그램 배포를 방해할 수 있는 정보 둬서는 안 기대를 사용 하 여 자습서에서 이러한 추가 기술 대부분 포함 했습니다.

자습서는 순서 대로 실행 되도록 설계 하 고 이전 부분을 기반으로 하는 각 부분입니다. 그러나 상황에 따라 관련이 없는 파트를 건너뛸 수 있습니다. (부분을 건너뜁니다 필요할 수 있습니다 나중에 자습서에서 절차를 조정할 수 있습니다.)

## <a name="intended-audience"></a>대상

이 자습서는 개발자를 대상으로 ASP.NET 소규모 조직 또는 다른 환경에서 작업 하는 위치:

- 지속적인 통합 프로세스 (자동화 된 빌드 및 배포) 사용 되지 않습니다.
- 프로덕션 환경에서 타사 호스팅 공급자입니다.
- 일반적으로 한 사람이 여러 역할 (개발, 테스트 및 배포 같은 사람)을 채웁니다.

엔터프라이즈 환경에서는 지속적인 통합 프로세스를 구현 하는 보다 일반적인 이며 프로덕션 환경에 일반적으로 회사의 서버에서 호스팅됩니다. 다른 사용자는 일반적으로 다양 한 역할을 수행합니다. 엔터프라이즈 배포에 대 한 정보를 참조 하세요 [엔터프라이즈 시나리오에서 웹 응용 프로그램 배포](../../deployment/deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)합니다.

모든 규모의 조직이 azure에 웹 응용 프로그램을 배포할 수도 있습니다 및 대부분의 이러한 자습서에 표시 된 절차는 Azure 앱 서비스 웹 앱에도 적용 합니다. Azure 소개를 참조 하세요 [ https://azure.microsoft.com ](https://azure.microsoft.com)합니다.

## <a name="the-hosting-provider-shown-in-the-tutorials"></a>이 자습서에 표시 된 호스팅 공급자

이 자습서에서는 호스팅 회사를 사용 하 여 계정을 설정 하 고 해당 호스팅 공급자에 게 응용 프로그램 배포 과정을 안내 합니다. 특정 호스팅 업체는 자습서에는 라이브 웹 사이트를 배포 하는 완벽 한 환경을 보여 줍니다 수 있도록 선택 했습니다. 다양 한 기능을 제공 하는 각 호스팅 회사 및 해당 서버에 배포 하는 환경에 따라 다양; 그러나이 자습서에서 설명 하는 프로세스가 전체 프로세스에 대 한 일반적입니다.

이 자습서에서는 Cytanium.com 사용 하는 호스팅 공급자를 사용할 수 있는 많은 하나인 및를 보증 하거나 권장 사항에는이 자습서에서 사용 하는 구성 하지 않습니다.

## <a name="deploying-web-site-projects"></a>웹 사이트 프로젝트를 배포합니다.

Contoso University Visual Studio 웹 응용 프로그램 프로젝트입니다. 대부분의 배포 방법 및이 자습서에서 설명 하는 도구에 적용 되지 않습니다 [웹 사이트 프로젝트](https://msdn.microsoft.com/library/dd547590.aspx)합니다. 웹 사이트 프로젝트를 배포 하는 방법에 대 한 자세한 내용은 [ASP.NET 배포 콘텐츠 맵](https://msdn.microsoft.com/library/bb386521.aspx#deployment_for_web_site_projects)합니다.

## <a name="deploying-aspnet-mvc-projects"></a>ASP.NET MVC 프로젝트를 배포합니다.

이 자습서에 대 한 ASP.NET Web Forms 프로젝트를 배포한 이지만 수행 하는 방법에 알아봅니다 모든 ASP.NET MVC에 적용할 수도 있습니다. Visual Studio MVC 프로젝트는 다른 형태의 웹 응용 프로그램 프로젝트입니다. 유일한 차이점은는 ASP.NET MVC 또는의 대상 버전을 지원 하지 않는 호스팅 공급자에 배포 하는 경우 해야 적절 한 설치 ([MVC 3](http://nuget.org/packages/AspNetMvc/3.0.20105.0) 또는 [MVC 4](http://nuget.org/packages/aspnetmvc)) 프로젝트에 NuGet 패키지.

## <a name="programming-language"></a>프로그래밍 언어

샘플 응용 프로그램을 사용 하 여 C# 자습서는 C#에 대 한 지식이 필요 하지 않습니다 있고 자습서에 설명 된 배포 방법 언어별 없는 합니다.

## <a name="troubleshooting-during-this-tutorial"></a>이 자습서에서 문제 해결

배포 하는 동안 오류가 발생 하거나 배포 된 사이트 올바르게 실행 되지 않은 경우 오류 메시지는 솔루션을 항상 제공 하지 않습니다. 몇 가지 일반적인 문제 시나리오를 사용 하 여 도움이 [문제 해결 참조 페이지](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md) 를 사용할 수 있습니다. 오류 메시지를 가져오거나 자습서를 진행할 때 작동 하지 않는 경우 문제 해결 페이지를 확인 해야 합니다.

## <a name="comments-welcome"></a>주석 시작

자습서에 대 한 의견을 기다리겠습니다를 하 고 자습서가 업데이트 되 면 노력 됩니다 계정 수정 또는 제안 자습서 주석에서 제공 되는 향상 된 기능에 대 한 야 합니다.

## <a name="prerequisites"></a>전제 조건

시작 하기 전에 Windows 7 이상을 사용 하 고 다음 제품 중 하나는 컴퓨터에 설치 되어 있는지 확인 합니다.

- [Visual Studio 2010 SP1](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)
- [Visual Web Developer Express 2010 SP1](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VWD2010SP1Pack)
- [Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC for Web](https://go.microsoft.com/fwlink/?LinkId=240162)

Visual Studio 2010 SP1 또는 Visual Web Developer Express 2010 SP1에 있는 경우 다음 제품을 설치 합니다.

- [Azure SDK for.NET (VS 2010 SP1)](https://go.microsoft.com/fwlink/?LinkID=208120) (웹 게시 업데이트 포함)
- [SQL Server 용 Microsoft Visual Studio 2010 SP1 도구 Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCEVSTools)

자습서를 완료 하려면 몇 가지 다른 소프트웨어가 필요 하지만 아직 로드는 필요가 없습니다. 이 자습서는 필요할 때 설치에 대 한 단계를 안내 합니다.

## <a name="downloading-the-sample-application"></a>샘플 응용 프로그램 다운로드

배포 응용 프로그램은 Contoso University,를 이미 만들었습니다. 에 설명 된 Contoso University 응용 프로그램을 느슨하게 기반 대학 웹 사이트의 단순화 된 버전의 [ASP.NET 사이트의 Entity Framework 자습서](https://asp.net/entity-framework/tutorials)합니다.

설치 필수 구성 요소에 있는 경우 다운로드 합니다 [Contoso University 웹 응용 프로그램](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)합니다. 합니다 *.zip* 파일 여러 버전의 프로젝트 및 모든 12 자습서를 포함 하는 PDF 파일을 포함 합니다. 자습서의 단계를 진행 하려면 ContosoUniversity 시작 될 때까지 시작 합니다. 프로젝트의 모양은 자습서의 끝을 확인 하려면 ContosoUniversity 엔드를 엽니다. 10 자습서의 전체 SQL Server로 마이그레이션하기 전에 프로젝트 모습을 확인 하려면 ContosoUniversity AfterTutorial09를 엽니다.

자습서 단계를 진행 하려면 준비가 ContosoUniversity Begin Visual Studio 프로젝트를 사용 하 여 작업에 대 한 사용 하 여 모든 폴더에 저장 합니다. 기본적으로이 다음 폴더입니다.

`C:\Users\<username>\Documents\Visual Studio 2012\Projects`

(이 자습서에서 스크린샷, 프로젝트 폴더는 루트 디렉터리에서에 있습니다는 `C`: 드라이브입니다.)

Visual Studio를 시작 하 고 프로젝트를 열고 CTRL-F5 키를 눌러 실행 합니다.

[![Home_page](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image2.png)](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image1.png)

웹 사이트 페이지의 메뉴 모음에서 액세스할 수 있으며 다음 기능을 수행할 수 있습니다.

- 학생 통계 (About 페이지)를 표시 합니다.
- 표시, 편집, 삭제 및 학생을 추가 합니다.
- 표시 및 편집 과정입니다.
- 표시 및 편집 강사입니다.
- 표시 하 고 부서를 편집 합니다.

다음은 몇 가지 대표적인 페이지의 스크린샷.

[![Students_Page](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image4.png)](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image3.png)

[![Add_Students_Page](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image6.png)](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image5.png)

## <a name="reviewing-application-features-that-affect-deployment"></a>배포에 영향을 주는 응용 프로그램 기능 검토

응용 프로그램의 다음 기능 배포 하기 위해 수행 해야 하거나 배포 하는 방법에 영향을 줍니다. 이러한 각 시리즈의 다음 자습서에서 자세히 설명 되어 있습니다.

- Contoso University student 및 instructor 이름과 같은 응용 프로그램 데이터를 저장 하는 SQL Server Compact 데이터베이스를 사용 합니다. 데이터베이스 테스트 데이터와 프로덕션 데이터의 조합에 포함 하 고 테스트 데이터를 제외 해야 하는 프로덕션에 배포할 때. 자습서 시리즈의 뒷부분에 나오는 SQL Server로 SQL Server Compact에서 마이그레이션할 수 있습니다.
- SQL Server Compact 데이터베이스의 사용자 계정 정보를 저장 하는 ASP.NET 멤버 자격 시스템을 사용 하는 응용 프로그램입니다. 응용 프로그램 몇 가지 제한 된 정보에 대 한 액세스 권한이 있는 사용자는 관리자 사용자를 정의 합니다. 테스트 계정을 없지만 관리자 계정이 하나를 사용 하 여 멤버 자격 데이터베이스를 배포 해야 합니다.
- 응용 프로그램 데이터베이스 및 멤버 자격 데이터베이스를 사용 하므로 SQL Server Compact 데이터베이스 엔진으로 데이터베이스 엔진 데이터베이스 자체 뿐만 아니라 호스팅 공급자를 배포 해야 합니다.
- 응용 프로그램 멤버 자격 시스템에서 SQL Server Compact 데이터베이스를 해당 데이터를 저장할 수 있도록 ASP.NET 유니버설 멤버 자격 공급자를 사용 합니다. 유니버설 멤버 자격 공급자를 포함 하는 어셈블리는 응용 프로그램과 함께 배포 되어야 합니다.
- 응용 프로그램 데이터는 응용 프로그램 데이터베이스에 액세스 하려면 Entity Framework 5.0을 사용 합니다. Entity Framework 5.0을 포함 하는 어셈블리는 응용 프로그램과 함께 배포 되어야 합니다.
- 응용 프로그램을 타사 오류 로깅 및 보고 유틸리티를 사용 합니다. 이 유틸리티는 응용 프로그램과 함께 배포 해야 하는 어셈블리에서 제공 됩니다.
- 오류 로깅 유틸리티 파일 폴더에 XML 파일에서 오류 정보를 씁니다. 배포에서이 폴더를 제외 해야 하에 배포 된 사이트의 ASP.NET에서 실행 되는 계정이이 폴더에 대 한 쓰기 권한이 있는지 확인 해야 합니다. (그렇지 않으면 테스트 환경에서 오류 로그 데이터를 프로덕션에 배포할 수 있습니다 및/또는 프로덕션 오류 로그 파일을 삭제 될 수 있습니다.)
- 응용 프로그램에 일부 설정을 변경 해야 하는 배포에 *Web.config* 대상 환경 (테스트 또는 프로덕션) 및 빌드에 따라 변경 해야 하는 다른 설정에 따라 파일 (디버그 또는 릴리스)를 구성 합니다.
- Visual Studio 솔루션에 클래스 라이브러리 프로젝트를 포함합니다. 이 프로젝트를 생성 하는 어셈블리에만 배포 프로젝트 자체입니다.

이 시리즈의 첫 번째 자습서에서는 샘플 Visual Studio 프로젝트를 다운로드 하 고 응용 프로그램을 배포 하는 방법에 영향을 주는 사이트 기능을 검토 합니다. 다음 자습서에서는 자동으로 처리할 이들 중 일부를 설정 하 여 배포를 위해 준비할 수 있습니다. 다른 수동으로 처리 있습니다.

> [!div class="step-by-step"]
> [다음](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md)
