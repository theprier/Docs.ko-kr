---
uid: web-forms/overview/deployment/visual-studio-web-deployment/introduction
title: "Visual Studio를 사용 하 여 ASP.NET 웹 배포: 소개 | Microsoft Docs"
author: tdykstra
description: "이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. 웹 응용 프로그램을 Azure 앱 서비스 웹 앱 또는 타사 호스팅 공급자에서 ASP.NET (게시) V를 사용 하 여..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/15/2013
ms.topic: article
ms.assetid: 24ad086d-865e-433c-9ac9-05f1a553da16
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/introduction
msc.type: authoredcontent
ms.openlocfilehash: e14f3bed001592c85bdbba868f51141bc52a9470
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="aspnet-web-deployment-using-visual-studio-introduction"></a>Visual Studio를 사용 하 여 ASP.NET 웹 배포: 소개
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> 이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. 웹 응용 프로그램을 Azure 앱 서비스 웹 앱 또는 타사 호스팅 공급자에서 ASP.NET (게시).NET 용 Azure SDK와 Visual Studio 2012를 사용 합니다. 대부분의 절차는 Visual Studio 2013 용 비슷합니다.
> 
> 인터넷을 통해 사용자를 사용할 수 있도록 하기 위해 웹 응용 프로그램을 개발 합니다. 하지만 개발 컴퓨터에서 작업 결과 얻게 하는 방법을 설명 했습니다은 직후에 일반적으로 웹 프로그래밍 자습서 중지 합니다. 이 일련의 자습서 시작 해제할 다른 위치: 웹 응용 프로그램을 작성, 테스트, 한 준비가 되 고 있습니다. 새로운 기능 이 자습서의 iis에 테스트를 위해 로컬 개발 컴퓨터 및 다음 스테이징 및 프로덕션에 대 한 제 3 자 호스팅 공급자 또는 Azure에 먼저 배포 하는 방법을 보여 줍니다. 배포 하는 예제 응용 프로그램은 Entity Framework, SQL Server 및 ASP.NET 멤버 자격 시스템을 사용 하는 웹 응용 프로그램 프로젝트입니다. ASP.NET Web Forms을 사용 하 여 샘플 응용 프로그램에 표시 된 절차는 ASP.NET MVC 및 Web API에도 적용 되지만 합니다.
> 
> 이 자습서는 Visual Studio에서 ASP.NET을 사용 하는 방법을 알고 있다고 가정 합니다. 시작 하려면 먼저는 이렇게 하지 않으면는 [기본 ASP.NET Web Forms 자습서](../../older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-1.md) 또는 [기본 ASP.NET MVC 자습서](../../../../mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md)합니다.
> 
> 자습서를 직접 관련 되지 않는 질문 해야 하도록를 게시할 수 있습니다는 [ASP.NET 배포 포럼](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment) 또는 [StackOverflow](http://stackoverflow.com)합니다.
> 
> 이 콘텐츠는 무료 전자책 (영문)에서 사용할 수는 또한 [TechNet 전자책 갤러리](https://social.technet.microsoft.com/wiki/contents/articles/11608.e-book-gallery-for-microsoft-technologies.aspx#ASPNETWebDeploymentusingVisualStudio)합니다.


## <a name="overview"></a>개요

이러한 자습서 SQL Server 데이터베이스가 포함 된 ASP.NET 웹 응용 프로그램을 배포 하는 과정을 안내 합니다. 테스트를 위해 로컬 개발 컴퓨터에 IIS를 이동한 다음에서 스테이징 및 프로덕션에 대 한 Azure SQL 데이터베이스 및 Azure 앱 서비스 웹 앱을 먼저 배포 합니다. One-click 게시 하는 Visual Studio를 사용 하 여 배포 하는 방법을 확인 하 고 명령줄을 사용 하 여 배포 하는 방법을 배웁니다.

자습서의 수 적일 배포 프로세스를 만들 수 있습니다. 사실, 기본 절차는 간단 합니다. 그러나 실제 상황에서 종종 해야 추가 배포 작업을 수행 하는 예를 들어 대상 서버에 폴더 사용 권한을 설정 합니다. म 바라면 서 실제 응용 프로그램을 성공적으로 배포에서 방해할 수 있는 정보 둬서는 안이 자습서는 이러한 추가 작업 중 일부에 대해 설명 했습니다.

이 자습서는 순서 대로 실행 되도록 설계 하 고 이전 부분을 기반으로 하는 각 부분입니다. 상황에 관련이 없는 일부를 건너뛸 수 있지만 다음 이후의 자습서 절차를 조정 해야 할 수 있습니다.

## <a name="intended-audience"></a>적용 대상

이 자습서는 환경에서 작업 하는 ASP.NET 개발자를 대상으로 위치:

- 프로덕션 환경은 Azure 앱 서비스 웹 앱 또는 타사 호스팅 공급자입니다.
- 배포 연속 통합 프로세스로 제한 되지만 Visual Studio에서 직접 수행할 수 있습니다.

배포 [소스 제어](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md) 를 사용 하는 [지속적인 업데이트](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) 프로세스 명령줄에서 배포 하는 방법을 보여 주는 자습서 하나를 제외 하 고이 자습서에서 다루지 않습니다. 지속적인 업데이트에 대 한 내용은 다음 리소스를 참조 합니다.

- [연속 통합 및 지속적인 업데이트 (Windows Azure로 응용 프로그램 빌딩 실제 클라우드)](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md)
- [Azure 앱 서비스의 웹 응용 프로그램 배포](https://azure.microsoft.com/en-us/documentation/articles/web-sites-deploy/)
- [엔터프라이즈 시나리오에서 웹 응용 프로그램 배포](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md) (의 엔터프라이즈 환경에 대 한 유용한 정보를 아직 Visual Studio 2010 용으로 작성 하는 자습서는 이전 집합입니다.)

## <a name="using-a-third-party-hosting-provider"></a>제 3 자 호스팅 공급자를 사용 하 여

이 자습서에서는 Azure 계정을 설정 하 고 스테이징 및 프로덕션에 대 한 응용 프로그램을 Azure 앱 서비스의 웹 응용 프로그램 배포 과정을 안내 합니다. 그러나 사용자가 선택한 타사 호스팅 공급자에 게 배포 하기 위한 동일한 기본 절차를 사용할 수 있습니다. 자습서에서는 Azure에 고유 프로세스를 통해 이동, 여기서은 바꾼 제 3 자 호스팅 공급자에서 예상할 수 있는 어떤 차이점이 합니다.

## <a name="deploying-web-app-projects"></a>웹 응용 프로그램 프로젝트 배포

샘플 응용 프로그램을 다운로드 하 고이 자습서에 대 한 배포는 Visual Studio 웹 응용 프로그램 프로젝트입니다. 그러나 최신 설치 하는 경우 [Visual Studio 웹 게시 업데이트](https://msdn.microsoft.com/tr-tr/library/jj161045.aspx), 웹 응용 프로그램 프로젝트에 대 한 동일한 배포 방법 및 도구를 사용할 수 있습니다.

## <a name="deploying-aspnet-mvc-projects"></a>ASP.NET MVC 프로젝트 배포

샘플 응용 프로그램은 ASP.NET Web Forms 프로젝트에서 이지만 작업을 수행 하는 방법을 배웁니다 모든 항목 에서도 ASP.NET MVC에 적용 됩니다. Visual Studio MVC 프로젝트는 또 다른 형태 웹 응용 프로그램 프로젝트입니다. 유일한 차이점은 ASP.NET MVC 또는의 대상 버전을 지원 하지 않는 호스팅 공급자를 배포 하는 경우 해야 하는 적절 한 설치 되어 있는지 ([MVC 3](http://nuget.org/packages/AspNetMvc/3.0.20105.0), [MVC 4](http://www.nuget.org/packages/Microsoft.AspNet.Mvc/4.0.30506.0) 또는 [MVC 5](http://www.nuget.org/packages/Microsoft.AspNet.Mvc)) 프로젝트에서 NuGet 패키지 합니다.

## <a name="programming-language"></a>프로그래밍 언어

샘플 응용 프로그램을 사용 하 여 C# 자습서에서는 C#에 대 한 지식이 필요 하지 않습니다 있고 자습서에 설명 된 배포 방법 언어 관련 없는 합니다.

## <a name="database-deployment-methods"></a>데이터베이스 배포 방법

세 가지 방법으로 Visual Studio에서 웹 배포와 함께 SQL Server 데이터베이스를 배포할 수 있습니다.

- Entity Framework Code First 마이그레이션
- DbDacFx Web Deploy 공급자
- DbFullSql 웹 배포 공급자

이 자습서에서는 이러한 메서드의 처음 두를 사용 합니다. DbFullSql Web Deploy 공급자는 더 이상 SQL Server Compact에서 SQL Server로 마이그레이션 등 몇 가지 특정 시나리오를 제외 하 고 권장 된 레거시 메서드입니다.

이 자습서에 나와 있는 메서드는 하지 SQL Server Compact, SQL Server 데이터베이스에 대 한 합니다. SQL Server Compact 데이터베이스를 배포 하는 방법에 대 한 정보를 참조 하십시오. [Visual Studio 웹 배포와 SQL Server Compact](../../older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12.md)합니다.

이 자습서에 나와 있는 메서드 사용 해야 하는 웹 배포 게시 방법입니다. 다른 게시 FPSE, FTP, 파일 시스템 등의 방법을 선호 하는 경우 참조 [웹 응용 프로그램 배포와 별도로 데이터베이스 배포](https://go.microsoft.com/fwlink/p/?LinkId=282413#databaseseparate) Visual Studio 및 ASP.NET에 대해 웹 배포 콘텐츠 맵에 있습니다.

### <a name="entity-framework-code-first-migrations"></a>Entity Framework Code First 마이그레이션

Entity Framework 버전 4.3, Microsoft Code First 마이그레이션을 도입 했습니다. Code First 마이그레이션을 데이터 모델에 대 한 증분 변경 하 고 데이터베이스에 변경 내용을 전파 하는 과정을 자동화 합니다. 첫 번째 코드의 이전 버전의 Entity Framework를 삭제 하 고 데이터 모델을 변경할 때마다 데이터베이스를 다시 만드는 일반적 사용 있습니다. 테스트 데이터를 쉽게 다시 만들 하지만 프로덕션 환경에서 일반적으로 데이터베이스를 삭제 하지 않고 데이터베이스 스키마를 업데이트 하기 때문에 개발에서 문제가 되지 않습니다. 마이그레이션 기능 코드 첫 번째 데이터베이스를 삭제 하 고 다시 만들기를 업데이트할 수 있습니다. Code First 필요한 스키마 변경을 수행 하는 방법을 자동으로 결정 하도록 하거나 변경 내용을 사용자 지정 하는 코드를 작성할 수 있습니다. Code First 마이그레이션에 대 한 소개를 참조 하십시오. [Code First 마이그레이션을](https://msdn.microsoft.com/library/hh770484.aspx)합니다.

웹 프로젝트를 배포 하는 Visual Studio에서 Code First 마이그레이션을 관리 하는 데이터베이스 배포 프로세스를 자동화할 수 있습니다. 게시 프로필을 만들 때 실행 Code First 마이그레이션을 (응용 프로그램 시작 시 실행) 이라는 레이블이 있는 확인란을 선택 합니다. 이 설정을 사용 하면 배포 프로세스에 Code First 사용 하도록 자동으로 대상 서버에서 응용 프로그램 Web.config 파일을 구성 하는 `MigrateDatabaseToLatestVersion` 이니셜라이저 클래스입니다.

Visual Studio 배포 과정에서 데이터베이스를 사용 하 여 작업을 수행 하지 않습니다. 배포 응용 프로그램 배포 후 처음으로 데이터베이스에 액세스 하면 Code First 자동으로 데이터베이스를 만들거나 데이터베이스 스키마를 최신 버전으로 업데이트 합니다. 응용 프로그램 마이그레이션 Seed 메서드를 구현 하는 데이터베이스를 만들거나 스키마 업데이트 후 메서드 실행 됩니다.

이 자습서에서는 응용 프로그램 데이터베이스를 배포 하려면 Code First 마이그레이션을 사용 합니다.

### <a name="the-dbdacfx-web-deploy-provider"></a>DbDacFx Web Deploy 공급자

Entity Framework Code First에 의해 관리 되지 SQL Server 데이터베이스에 대 한 게시 프로필을 구성 하는 경우 데이터베이스 업데이트 레이블이 있는 확인란을 선택할 수 있습니다. 초기 배포 하는 동안 dbDacFx 공급자가 원본 데이터베이스와 일치 하도록 대상 데이터베이스의 테이블 및 기타 데이터베이스 개체를 만듭니다. 후속 배포 공급자 원본 및 대상 데이터베이스의 차이점을 결정 하 고 원본 데이터베이스와 일치 하도록 대상 데이터베이스의 스키마를 업데이트 합니다. 기본적으로 공급자 않습니다 내용을 변경 테이블이 나 열 삭제 된 경우 등의 데이터 손실을 발생 합니다.

이 메서드는 데이터베이스 테이블에서 데이터의 배포를 자동화 되지 않습니다 있지만 그렇게 하 고 배포 하는 동안 실행 하도록 Visual Studio 구성 스크립트를 만들 수 있습니다. 배포 하는 동안 스크립트를 실행 하는 또 다른 이유는 스키마를 변경 데이터 손실 있으므로 자동으로 수행할 수 없는 것입니다.

이 자습서에서는 ASP.NET 멤버 자격 데이터베이스를 배포 하는 dbDacFx 공급자를 사용 합니다.

## <a name="troubleshooting-during-this-tutorial"></a>이 자습서에서 문제 해결

배포 하는 동안 오류가 발생 하거나 배포 된 사이트 올바르게 실행 되지 않은 경우 오류 메시지가 확실 한 해결책 항상 제공 하지 않습니다. 몇 가지 일반적인 문제 시나리오에 대 한 도움는 [참조 페이지의 문제 해결](troubleshooting.md) 를 사용할 수 있습니다. 오류 메시지가 자습서를 진행할 때 작동 하지 않는 경우 문제 해결 페이지를 확인 해야 합니다.

## <a name="comments-welcome"></a>시작 설명

이 자습서에 대 한 의견을 기다리겠습니다, 하 고 자습서 업데이트 될 때 모든 노력 됩니다 계정 수정 또는 제안이 자습서 주석에서 제공 되는 향상 된 기능에 대 한 고려 되도록 합니다.

<a id="prerequisites"></a>

## <a name="prerequisites"></a>필수 구성 요소

이 자습서는 다음 제품에 대 한 작성 했습니다.

- Windows 8 또는 Windows 7입니다.
- Visual Studio 2012 또는 Visual Studio 2012 Express for Web와 [최신 업데이트](https://go.microsoft.com/fwlink/?LinkId=272486)합니다.
- [Visual Studio 2012 용 azure SDK](https://go.microsoft.com/fwlink/?LinkId=254364)

Visual Studio 2010 SP1 또는 Visual Studio 2013을 사용 하 여 자습서를 따라 수 있지만 일부 스크린 샷을 다른 되며 일부 기능이 다르게 됩니다.

Visual Studio 2013을 사용 하는 경우 설치 [Visual Studio 2013 용 Azure SDK](https://go.microsoft.com/fwlink/?LinkID=324322)합니다.

Visual Studio 2010 s p 1을 사용 하는 경우에 다음 소프트웨어를 설치 합니다.

- [Visual Studio 2010 용 azure SDK](https://go.microsoft.com/fwlink/?LinkID=254269)
- [SQL Server Express LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=SQLLocalDBOnly_11_0)
- [SQL Server Data Tools](https://msdn.microsoft.com/en-us/library/hh500335.aspx)합니다.

SDK 종속성의 개수를 이미 있는 컴퓨터에 따라 Azure SDK를 설치 하면 몇 분에서 30 분 이상까지 시간이 오래 걸릴 수 있습니다. Azure에 대신 제 3 자 호스팅 공급자에 게시할 SDK는 Visual Studio 웹의 최신 업데이트를 포함 하기 때문에 기능을 게시 하려는 경우에는 Azure SDK가 필요 합니다.

> [!NOTE]
> 이 자습서는 Azure SDK의 버전 1.8.1 두고 작성 되었습니다. 그 후 새 버전 추가 기능으로 릴리스 되었습니다. 이러한 기능 및 링크에 대 한 자세한 정보를 포함 하는 리소스를 언급 하기 위해이 자습서에서는 업데이트 되었습니다.


지침과 스크린 샷 Windows 8 기반으로 하지만 자습서는 Windows 7에 대 한 차이점을 설명 합니다.

자습서를 완료 하는 데 필요한 다른 소프트웨어 있지만 아직 설치 되어 있이 필요가 없습니다. 자습서는 필요할 때 설치 단계를 안내 합니다.

## <a name="download-the-sample-application"></a>샘플 응용 프로그램 다운로드

배포 하는 응용 프로그램은 Contoso 대학,를 이미 만들었습니다. 에 설명 된 Contoso 대학 응용 프로그램을 느슨하게 기반 대학 웹 사이트의 단순화 된 버전의 [ASP.NET 사이트의 Entity Framework 자습서](https://asp.net/entity-framework/tutorials)합니다.

필수 구성 요소가 설치 되어 있는 경우 다운로드는 [Contoso 대학 웹 응용 프로그램](https://go.microsoft.com/fwlink/p/?LinkId=282627)합니다. *.zip* 프로젝트의 여러 버전이 포함 되어 있습니다. 자습서의 단계를 진행 하도록 C# 폴더에 있는 프로젝트를 시작 합니다. 이 자습서의 끝에 프로젝트 모양을 보려면 ContosoUniversity 엔드 폴더에 프로젝트를 엽니다.

자습서의 단계를 통해 작업에 대 한 프로젝트를 준비 하려면 다음 단계를 수행 합니다.

1. Visual Studio 프로젝트를 사용 하기 위한 사용 하 여 모든 폴더에 ContosoUniversity 라는 폴더의 C# 폴더에서 ContosoUniversity 솔루션 파일을 저장 합니다.

    기본적으로이 Visual Studio 2012에 대 한 다음 폴더입니다.

    `C:\Users\<username>\Documents\Visual Studio 2012\Projects`

    (이 자습서의 스크린 샷을 프로젝트 폴더는 루트 디렉터리에서에 있습니다는 `C`: 드라이브입니다.)
2. Visual Studio를 시작 하 고 프로젝트를 엽니다.
3. **솔루션 탐색기**솔루션을 마우스 오른쪽 단추로 클릭 하 고 클릭 **EnableNuGet 패키지 복원**합니다.
4. 솔루션을 빌드합니다.
5. 컴파일 오류가 발생 하는 경우 수동으로 NuGet 패키지를 복원 합니다.

    1. **솔루션 탐색기**솔루션을 마우스 오른쪽 단추로 클릭 한 다음 클릭 **솔루션에 대 한 NuGet 패키지 관리**합니다.
    2. 맨 위에 있는 **NuGet 패키지 관리** 대화 상자 표시 **일부 NuGet 패키지는이 솔루션에 없습니다. 복원 하려면 클릭 합니다.** 클릭는 **복원** 단추입니다.
    3. 솔루션을 다시 빌드합니다.
6. 응용 프로그램을 실행 하려면 CTRL + f 5를 누릅니다.

    응용 프로그램이 Contoso 대학 홈 페이지에 열립니다.

    ![홈 페이지 개발](introduction/_static/image1.png)

    (Visual Studio는 SQL Server Express LocalDB 인스턴스를 시작 하는 동안 대기 시간 수 있으며 얻을 수도 시간 초과 오류는 처리 시간이 너무 오래 걸립니다. 그러면 정당한 프로젝트 다시 시작합니다.)

웹 사이트 페이지의 메뉴 모음에서 액세스할 수 있으며 다음 기능을 수행할 수 있도록 합니다.

- 학생 통계 (정보 페이지)를 표시 합니다.
- 표시, 편집, 삭제 및 학생 들을 추가 합니다.
- 표시 및 편집 과정입니다.
- 표시 하 고 강사를 편집 합니다.
- 표시 하 고 부서를 편집 합니다.

다음은 몇 가지 대표 페이지의 스크린 샷을 합니다.

![학생 페이지 개발](introduction/_static/image2.png)

![학생 페이지 Dev 추가](introduction/_static/image3.png)

## <a name="review-application-features-that-affect-deployment"></a>배포에 영향을 주는 응용 프로그램 기능을 검토 합니다.

응용 프로그램의 다음 기능에 배포 하는 방법 또는 배포를 수행 해야 하면 영향을 줍니다. 이러한 각 계열에는 다음 자습서에서 자세히 설명 합니다.

- Contoso 대학 학생과 강사 이름과 같은 응용 프로그램 데이터를 저장할 SQL Server 데이터베이스를 사용 합니다. 데이터베이스에 테스트 데이터 및 프로덕션 데이터의 혼합 하 고 프로덕션 환경에 배포 하는 경우 테스트 데이터를 제외 하도록 해야 합니다.
- 응용 프로그램이 SQL Server 데이터베이스의 사용자 계정 정보를 저장 하는 ASP.NET 멤버 자격 시스템을 사용 합니다. 응용 프로그램에는 몇 가지 제한 된 정보에 대 한 액세스 권한이 있는 관리자가 사용자를 정의 합니다. 멤버 자격 데이터베이스 테스트 계정 없이 하지만 관리자 계정으로 배포 해야 합니다.
- 응용 프로그램 공급 업체 오류 로깅 및 보고 유틸리티를 사용 합니다. 이 유틸리티는 응용 프로그램과 함께 배포 되어야 하는 어셈블리에 제공 됩니다.
- 오류 로깅 유틸리티 파일 폴더에 XML 파일에 오류 정보를 기록 합니다. ASP.NET에 배포 된 사이트에서 실행 되는 계정에이 폴더에 대 한 쓰기 권한이 있고 배포에서이 폴더를 제외 해야 있는지 확인 해야 합니다. (그렇지 않은 경우 오류 로그 데이터는 테스트 환경에서 프로덕션에 배포할 수 있으며 및/또는 프로덕션 오류 로그 파일을 삭제 될 수 있습니다.)
- 응용 프로그램에 배포 된에서 변경 되어야 하는 일부 설정을 포함 *Web.config* 대상 환경 (테스트, 준비 또는 프로덕션) 및 빌드에 따라 변경 해야 하는 기타 설정에 따라 파일 구성 (디버그 또는 릴리스)입니다.
- Visual Studio 솔루션에는 클래스 라이브러리 프로젝트에 포함 됩니다. 이 프로젝트에서 생성 하는 어셈블리에만 배포할지 프로젝트 자체입니다.

## <a name="summary"></a>요약

이 시리즈의 첫 번째 자습서에서는 샘플 Visual Studio 프로젝트를 다운로드 한 있고 응용 프로그램을 배포 하는 방법에 영향을 주는 사이트 기능을 검토 합니다. 다음 자습서에서 자동으로 처리 되도록 이러한 기능 중 일부를 설정 하 여 배포를 위해 준비할 수 있습니다. 다른 수동으로 처리할 수 있습니다.

>[!div class="step-by-step"]
[다음](preparing-databases.md)
