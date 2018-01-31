---
uid: whitepapers/aspnet-web-deployment-content-map
title: "ASP.NET 웹 배포-권장 리소스 | Microsoft Docs"
author: rick-anderson
description: "이 항목에서는 설명서의 링크를 배포 하는 방법에 대 한 리소스 (게시) ASP.NET 웹 비주얼 웹 De Visual Studio 2010을 사용 하 여 IIS에 응용 프로그램..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/14/2014
ms.topic: article
ms.assetid: 58b583cd-c4ab-47a3-8527-8c92c298c91f
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /whitepapers/aspnet-web-deployment-content-map
msc.type: content
ms.openlocfilehash: 78ff183394b5ff92f789b50551d01d28f9bff93b
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="aspnet-web-deployment---recommended-resources"></a>ASP.NET 웹 배포-권장 리소스
====================
> 이 항목에서는 설명서의 링크를 배포 하는 방법에 대 한 리소스 (게시) ASP.NET 웹 응용 프로그램을 Visual Studio 2010, Visual Web Developer 2010 이상 버전을 사용 하 여 IIS 합니다.
> 
> 훌륭한 블로그 게시물을 알고 있는 경우 [stackoverflow](http://stackoverflow.com) 스레드나 다른 링크는 것이 유용한 [전자 메일을 보내](mailto:aspnetue@microsoft.com?subject=Deployment Content Map) 링크와 합니다.
> 
> > [!NOTE] 
> > 
> > 최신 릴리스를 설치 하는 경우에 사용할 수 있는 배포 기능에 대해 많은이 리소스는 [Visual Studio 웹 게시 업데이트](https://go.microsoft.com/fwlink/?LinkID=208120)합니다. 기능 중 일부는 Visual Studio 2012 또는 Visual Studio 2013 에서만 사용할 수 있습니다.


이 항목에는 다음과 같은 단원이 포함되어 있습니다.

- [웹 프로젝트에 대 한 배포 옵션 이해](#understanding)
- [호스팅 공급자는 ASP.NET 응용 프로그램에 대 한 찾기](#findinghosting)
- [Visual Studio에서 웹 응용 프로그램 배포](#fromvs)
- [만들고 웹 배포 패키지를 설치 하 여 웹 응용 프로그램 배포](#package)
- [CI (연속 통합) 프로세스를 사용 하 여 웹 응용 프로그램 배포](#ci)
- [배포 중 대상 Web.config 파일 또는 app.config 파일에서 설정을 변경 하려면 Web.config 변환 사용](#transforms)
- [웹 배포 매개 변수를 사용 하 여 배포 하는 동안 대상 웹 응용 프로그램의 설정을 변경 하려면](#webdeployparms)
- [지 원하는 응용 프로그램 오프 라인 배포 중](#appoffline)
- [데이터베이스 또는 변경 내용을 배포 웹 응용 프로그램 배포의 일부로 데이터베이스에](#databasewithweb)
- [웹 응용 프로그램 배포와 별도로 데이터베이스 배포](#databaseseparate)
- [멤버 자격 및 프로 파일링 같은 서비스 ASP.NET 응용 프로그램을 사용 하는 웹 응용 프로그램 배포](#aspnetmembership)
- [배포를 위한 미리 컴파일](#precompiling)
- [인트라넷 웹 응용 프로그램 배포](#intranet)
- [기본 자동화 되지 않음은 일반적인 배포 작업 자동화](#automating)
- [개발자가 웹 배포를 사용 하 여 웹 응용 프로그램을 배포할 수 있도록 웹 서버를 구성 합니다.](#configuringservers)
- [호스팅 공급자에 대 한 서버 구성](#hostingprovider)
- [배포 문제 해결](#troubleshooting)
- [특정 배포 질문 도움말 보기](#gettinghelp)
- [추가 리소스](#additional)


<a id="understanding"></a>


## <a name="understanding-deployment-options-for-web-projects"></a>웹 프로젝트에 대 한 배포 옵션 이해

- [Visual Studio 및 ASP.NET에 대 한 웹 배포 개요](https://msdn.microsoft.com/library/dd394698.aspx) (MSDN).
- [Windows Azure 웹 사이트를 배포 하는 방법](https://docs.microsoft.com/azure/app-service-web/web-sites-deploy)합니다. 웹 프로젝트를 Windows Azure 웹 사이트를 포함 하 여 배포에 대 한 리소스에 옵션 및 링크에 설명 [지속적인 업데이트](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) (에서 자동화 된 [소스 제어](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md)) Visual Studio를 사용 하 여 뿐만 아니라 합니다.
- [Visual Studio 2012 웹 게시 개선](../visual-studio/overview/2012/visual-studio-2012-web-publishing-improvements.md) (Scott hanselman의 비디오).
- [VS 2010에서 웹 배포에 대 한 개요 게시](http://vishaljoshi.blogspot.com/2009/09/overview-post-for-web-deployment-in-vs.html) (Vishal Joshi 블로그). 이전 블로그 게시물 하지만 Visual Studio 2010 리소스 중 일부는 Visual Studio 2012에도 적용 하는 정보를 연결 합니다.


<a id="findinghosting"></a>


## <a name="finding-hosting-providers-for-an-aspnet-application"></a>호스팅 공급자는 ASP.NET 응용 프로그램에 대 한 찾기

- [ASP.NET 호스팅](https://asp.net/hosting)


<a id="fromvs"></a>


## <a name="deploying-a-web-application-from-visual-studio"></a>Visual Studio에서 웹 응용 프로그램 배포

- [Windows Azure 웹 사이트를 배포 하는 방법](https://docs.microsoft.com/azure/app-service-web/web-sites-deploy)합니다. 옵션에 설명 하 고 Windows Azure 웹 사이트를 웹 프로젝트를 배포 하는 리소스에 대 한 링크를 제공 합니다. Visual Studio에서 배포에 대 한 섹션을 포함 합니다.
- [Visual Studio를 사용 하 여 ASP.NET 웹 배포](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md)합니다. 12 부분으로 이루어진 자습서 시리즈에서는 SQL Server 데이터베이스와 웹 응용 프로그램을 배포 하는 방법을 보여 줍니다. 데이터베이스에 대 한 배포 dbDacFx 공급자와 Entity Framework Code First 마이그레이션을 사용 됩니다. 에 대 한 정보도 포함 [Web.config 파일 변환](../web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations.md), [개별 파일을 배포](../web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update.md#specificfiles), [명령줄 배포](../web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment.md), 및 [하는 방법 Visual Studio 웹 사용자 지정 파이프라인.pubxml 파일을 편집 하 여 게시](../web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files.md)합니다. Web Forms, MVC, Web API 등의 모든 ASP.NET 웹 프로젝트에 적용 됨)
- [방법: 배포 된 웹 프로젝트를 사용 하 여 한 번의 클릭 게시 Visual Studio에서](https://msdn.microsoft.com/library/dd465337.aspx) (Visual Studio 웹 게시 마법사에 대 한 정보를 참조 합니다.)
- [SQL Server Compact Visual Studio를 사용 하 여 ASP.NET 웹 응용 프로그램 배포](../web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12.md)합니다. 이 이전 버전의 **Visual Studio를 사용 하 여 ASP.NET 웹 배포** 이 섹션의 맨 위에 나열 합니다. SQL Server Compact 데이터베이스를 배포 하는 방법 및 전체 버전의 SQL Server를 SQL Server Compact에서 마이그레이션하는 방법에 대 한 내용은 지금은 주로 유용 합니다.
- [.NET 다중 계층 응용 프로그램 사용 하 여 저장소 테이블, 큐 및 Blob](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36) (Microsoft Azure 사이트). 5 부분으로 이루어진 자습서 시리즈 MVC 프로젝트를 만들어 Windows Azure 클라우드 서비스에 배포 하는 방법을 보여 줍니다.


<a id="package"></a>
## <a name="deploying-a-web-application-by-creating-and-installing-a-web-deployment-package"></a>만들고 웹 배포 패키지를 설치 하 여 웹 응용 프로그램 배포

- [방법: Visual Studio에서 웹 배포 패키지 만들기](https://msdn.microsoft.com/library/dd465323.aspx) (MSDN).
- [방법: Visual Studio가 설치.deploy.cmd 파일을 사용 하 여 배포 패키지를 만든](https://msdn.microsoft.com/library/ff356104.aspx) (MSDN).
- [웹 배포 패키지를 사용 하 여 개발 상자에 IIS를 제 3 자 호스트를 배포 하려면](http://sedodream.com/2011/11/08/UsingAWebDeployPackageToDeployToIISOnTheDevBoxAndToAThirdPartyHost.aspx) (Sayed Hashimi 블로그). IIS에서 로컬 컴퓨터에 배포 패키지를 설치 및 호스팅에 회사 하 여 IIS 관리자를 사용 하는 방법을 원격 관리용 IIS 관리자를 지원 합니다.
- [웹 배포 패키지에서 Visual Studio 2010 빌드](https://www.iis.net/learn/publish/using-web-deploy/building-a-web-deploy-package-from-visual-studio-2010) (IIS.NET 웹 사이트). 명령줄 패키지 만들기 및 설치에 대 한 지침을 포함합니다.
- [패키지 게시 아무 곳](http://sedodream.com/2012/03/14/PackageWebUpdatedAndVideoBelow.aspx) (Sayed Hashimi 블로그). 여러 서버에 하나의 패키지를 배포할 수 있도록 여러 대상 환경에 대 한 Web.config 파일을 변형 하는 프로세스를 자동화 하는 NuGet 패키지를 소개 합니다. 참고 항목에서 [PackageWeb 비디오](https://www.youtube.com/watch?v=-LvUJFI8CzM) Sayed Hashimi 여 합니다.

다음 섹션을 참조 하십시오.


<a id="ci"></a>


## <a name="deploying-a-web-application-using-a-continuous-integration-ci-process"></a>CI (연속 통합) 프로세스를 사용 하 여 웹 응용 프로그램 배포

- [연속 통합 및 지속적인 업데이트 (Windows Azure로 응용 프로그램 빌딩 실제 클라우드).](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) 연속 통합 및 지속적인 업데이트를 소개 하는 전자 문서 장 합니다.
- [Windows Azure 웹 사이트를 배포 하는 방법](https://docs.microsoft.com/azure/app-service-web/web-sites-deploy)합니다. Windows Azure 웹 사이트를 웹 프로젝트를 배포 하기 위한 리소스 옵션 및 링크를 설명 합니다. 소스 제어에서 배포를 자동화 하는 방법에 대 한 섹션을 포함 합니다.
- [엔터프라이즈 시나리오에서 웹 응용 프로그램 배포](../web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)합니다. 40 부분으로 이루어진 자습서 시리즈에는 Visual Studio 2010 및 Team Foundation Server 2010을 사용 하 여 CI 프로세스에서 배포를 자동화 하는 방법을 보여 줍니다.
- [Microsoft Build Engine 내: MSBuild 및 Sayed Hashimi 및 William Bartholomew Team Foundation Build를 사용 하 여](http://msbuildbook.com)합니다. 웹 리소스 책 않으며 연속 통합 시나리오에 대 한 MSBuild를 구성 하는 방법을 학습 하기 위한 필수 지침 이기입니다.
- [MSBuild 확장 팩](https://github.com/mikefourie/MSBuildExtensionPack)합니다. 배포 작업을 포함합니다.
- [Team Foundation 빌드 사용자 지정 가이드](https://aka.ms/vsarsolutions)합니다. Team Foundation Server 설정의 ALM rangers 설명서 웹 배포에 설명 하 고 자습서 및 동영상을 포함 합니다.
- [CI 서버에서 SlowCheetah XML 변환](http://sedodream.com/2011/12/12/SlowCheetahXMLTransformsFromACIServer.aspx) (Sayed Hashimi 블로그). Visual Studio 추가 기능을 app.config 및 다른 XML 파일을 변환 하기 위한 SlowCheetah를 사용 하는 방법에 설명 합니다.

참고 항목 [는 지 원하는 응용 프로그램 오프 라인 배포 하는 동안](aspnet-web-deployment-content-map.md#appoffline) 이 페이지의 뒷부분에 나오는 합니다.


<a id="transforms"></a>


## <a name="using-webconfig-transformations-to-change-settings-in-the-destination-webconfig-file-or-appconfig-file-during-deployment"></a>배포 중 대상 Web.config 파일 또는 app.config 파일에서 설정을 변경 하려면 Web.config 변환 사용

- [Web.config 파일 변환](../web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations.md)합니다.
- [Visual Studio를 사용 하 여 웹 프로젝트 배포에 대 한 Web.config 변환 구문은](https://msdn.microsoft.com/library/dd465326.aspx) (MSDN).
- [Web.config 변환 도구 2012.2-웹](https://www.youtube.com/watch?v=HdPK8mxpKEI) (Sayed Hashimi YouTube 비디오). Web.config 변환 미리 보기를 설정 하는 방법을 보여 줍니다.
- [Web.config 변환을 비활성화 하려면 어떻게 합니까?](https://msdn.microsoft.com/library/ee942158.aspx#disable_web_config_transformation) (MSDN)입니다.
- [Web.config 변환 하는 대신 웹 배포 매개 변수는 경우 사용 해야 합니까?](https://msdn.microsoft.com/library/ee942158.aspx#web_deploy_parameters) (MSDN)입니다.
- [Codeplex.com에 발표 (XML 문서 변형) XDT](https://blogs.msdn.com/b/webdev/archive/2013/04/23/xdt-xml-document-transform-released-on-codeplex-com.aspx) (.NET 웹 개발 및 도구 블로그). Web.config 파일 변환 엔진에 대 한 소스 코드의 가용성을 알리는 하 고 사용 하는 몇 가지 도구를 나열 합니다.
- [Windows Azure 웹 사이트: 응용 프로그램의 문자열 방법 및 연결 문자열 작업](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx) (Microsoft Azure 블로그). 대상 환경은 Windows Azure 웹 사이트를 변형 하려면 Web.config에 대 한 대안 변환 `appSettings` 또는 `connectionStrings`합니다.


<a id="webdeployparms"></a>


## <a name="using-web-deploy-parameters-to-change-settings-in-the-destination-web-application-during-deployment"></a>웹 배포 매개 변수를 사용 하 여 배포 하는 동안 대상 웹 응용 프로그램의 설정을 변경 하려면

- [방법: 사용 하 여 웹 배포 매개 변수는 웹 배포 패키지에](https://msdn.microsoft.com/library/ff398068.aspx) (MSDN).
- [MSDeploy: 게시 프로필에 따라 게시에 대 한 앱 설정을 업데이트 하는 방법](http://sedodream.com/2013/03/02/MSDeployHowToUpdateAppSettingsOnPublishBasedOnThePublishProfile.aspx) (Sayed Hashimi 블로그). Visual Studio에 웹 배포 매개 변수를 통합 하는 방법을 보여 줍니다 게시 프로필 합니다.
- [웹 배포 매개 변수화](https://www.iis.net/learn/publish/using-web-deploy/web-deploy-parameterization) (IIS.NET 웹 사이트).
- [웹 배포 매개 변수화 동작에서](http://vishaljoshi.blogspot.com/2010/07/web-deploy-parameterization-in-action.html) (Vishal Joshi 블로그).
- [웹 배포 매개 변수화 vs입니다. Web.config 변환](http://vishaljoshi.blogspot.com/2010/06/parameterization-vs-webconfig.html) (Vishal Joshi 블로그).
- [Windows Azure 웹 사이트: 응용 프로그램의 문자열 방법 및 연결 문자열 작업](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx) (Microsoft Azure 블로그). 대상 환경은 Windows Azure 웹 사이트를 매개 변수화 하려는 경우 대신 웹 배포 매개 변수 `appSettings` 또는 `connectionStrings`합니다.


<a id="appoffline"></a>


## <a name="making-sure-an-application-is-off-line-during-deployment"></a>지 원하는 응용 프로그램 오프 라인 배포 중

- [Visual Studio를 사용 하 여 ASP.NET 웹 배포: 코드 업데이트 배포](../web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update.md)합니다. 섹션을 참조 **배포 하는 동안 있는 오프 라인 응용 프로그램입니다.**
- [응용 프로그램을 오프 라인 게시 하기 전에](https://www.iis.net/learn/publish/deploying-application-packages/taking-an-application-offline-before-publishing) (IIS.net 사이트). 응용 프로그램의 처리를 자동화 하는 웹 배포 3.0에 기본 제공 기능을 설명\_offline.htm 파일입니다. 이 기능은 사용자 지정 앱과 함께 작동 하지 않습니다\_offline.htm 파일입니다.
- [게시 하는 동안 웹 응용 프로그램 오프 라인으로 수행 하는 방법](http://sedodream.com/2012/01/08/HowToTakeYourWebAppOfflineDuringPublishing.aspx) (Sayed Hashimi 블로그). 사용자 지정 앱을 사용 하는 프로세스를 자동화 하는 방법\_offline.htm 파일입니다.
- [웹 응용 프로그램을 오프 라인 및 usechecksum에 대 한 업데이트를 게시](https://blogs.msdn.com/b/webdev/archive/2013/10/30/web-publishing-updates-for-app-offline-and-usechecksum.aspx) (Microsoft 웹 개발 블로그). 응용 프로그램의 사용을 자동화 하기 위한 또 다른 옵션\_offline.htm 파일입니다.
- [웹 배포 3.5 RTW](https://blogs.iis.net/msdeploy/archive/2013/07/09/webdeploy-3-5-rtw.aspx) (IIS.net 사이트). 사용자 지정 앱에 대 한 웹 배포 3.5의 새로운 기능\_offline.htm 파일입니다.


<a id="databasewithweb"></a>


## <a name="deploying-a-database-or-changes-to-a-database-as-part-of-web-application-deployment"></a>데이터베이스 또는 변경 내용을 배포 웹 응용 프로그램 배포의 일부로 데이터베이스에

- [Visual Studio에서 데이터베이스 배포를 구성할](https://msdn.microsoft.com/library/dd394698.aspx#dbdeployment) (MSDN). 웹 프로젝트를 사용 하 여 데이터베이스를 배포 하기 위한 옵션의 개요입니다.
- [Visual Studio를 사용 하 여 ASP.NET 웹 배포](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md)합니다. 12 부분으로 이루어진 자습서 시리즈 dbDacFx 공급자 및 Entity Framework Code First 마이그레이션을 사용 하 여 데이터베이스 배포를 보여 줍니다.
- [방법: 웹 배포 한 번의 클릭을 사용 하 여 프로젝트를 Visual Studio에서 게시](https://msdn.microsoft.com/library/dd465337.aspx) (MSDN).
- [Windows Azure 웹 사이트에 멤버 자격, OAuth, SQL 데이터베이스와 보안 ASP.NET MVC 5 앱을 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)합니다. 빌드 및 단일 SQL Server를 사용 하는 응용 프로그램을 배포 하는 긴 자습서는 데이터베이스 멤버 자격 및 응용 프로그램 데이터에 대 한 합니다.
- [SQL Server Compact Visual Studio를 사용 하 여 ASP.NET 웹 응용 프로그램 배포](../web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12.md)합니다. 12 부분으로 이루어진 자습서 시리즈를 정식 버전의 SQL Server SQL Server Compact에서 마이그레이션하는 방법 및 SQL Server Compact 데이터베이스를 배포 하는 방법을 보여 줍니다.

만들기, 웹 배포 패키지를 설치 및이 페이지의 앞부분에 나오는 CI (연속 통합) 프로세스를 사용 하 여 웹 응용 프로그램을 배포 하 여 웹 응용 프로그램 배포를 참조 합니다.


<a id="databaseseparate"></a>


## <a name="deploying-a-database-separately-from-web-application-deployment"></a>웹 응용 프로그램 배포와 별도로 데이터베이스 배포

- [SQL Server Data Tools](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx) (MSDN).
- [SQL Server 데이터베이스 프로젝트에서 데이터를 포함 하 여](https://blogs.msdn.com/b/ssdt/archive/2012/02/02/including-data-in-an-sql-server-database-project.aspx) (SQL Server Data Tools 팀 블로그). 데이터베이스를 배포 하는 경우 스키마와 데이터 모두를 배포 하는 방법입니다.
- [Windows Azure로 데이터베이스를 배포 하는 방법](https://docs.microsoft.com/azure/sql-database/sql-database-cloud-migrate) (Microsoft Azure 사이트)
- [Windows Azure SQL 데이터베이스 (이전의 SQL Azure)로 데이터베이스 마이그레이션](https://msdn.microsoft.com/library/windowsazure/ee730904.aspx) (MSDN).
- [SSDT를 사용 하 여 SQL Azure로 데이터베이스 마이그레이션](https://blogs.msdn.com/b/ssdt/archive/2012/04/19/migrating-a-database-to-sql-azure-using-ssdt.aspx) (SQL Server Data Tools 팀 블로그).
- [Windows Azure로 데이터 중심 응용 프로그램 마이그레이션](https://msdn.microsoft.com/library/jj156154.aspx) (MSDN).
- [Windows Azure SQL 데이터베이스로 SQL Server 데이터베이스 마이그레이션](https://msdn.microsoft.com/library/windowsazure/jj156160.aspx) (MSDN).


<a id="aspnetmembership"></a>


## <a name="deploying-a-web-application-that-uses-aspnet-application-services-such-as-membership-and-profiling"></a>멤버 자격 및 프로 파일링 같은 서비스 ASP.NET 응용 프로그램을 사용 하는 웹 응용 프로그램 배포

- [Windows Azure 웹 사이트에 멤버 자격, OAuth, SQL 데이터베이스와 보안 ASP.NET MVC 5 앱을 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)합니다. 빌드 및 단일 SQL Server를 사용 하는 응용 프로그램을 배포 하는 긴 자습서는 데이터베이스 멤버 자격 및 응용 프로그램 데이터에 대 한 합니다.
- [ASP.NET Identity](https://asp.net/identity/)합니다. ASP.NET Id에 대 한 리소스입니다.
- [Visual Studio를 사용 하 여 ASP.NET 웹 배포](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md)합니다. 12 부분으로 이루어진 자습서 시리즈에는 ASP.NET 멤버 자격 데이터베이스를 배포 하는 방법을 보여 줍니다.
- [응용 프로그램 서비스를 사용 하는 웹 사이트를 구성](../web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-a-website-that-uses-application-services-cs.md)합니다. 웹 사이트에 대 한 프로젝트 하지만 이기도 웹 응용 프로그램 프로젝트와 관련이 있습니다.
- [사용자 및 프로덕션 웹 사이트에 대 한 역할](../web-forms/overview/older-versions-getting-started/deploying-web-site-projects/users-and-roles-on-the-production-website-cs.md)합니다. 웹 사이트에 대 한 프로젝트 하지만 이기도 웹 응용 프로그램 프로젝트와 관련이 있습니다.


<a id="precompiling"></a>


## <a name="precompiling-for-deployment"></a>배포를 위한 미리 컴파일

- [ASP.NET 웹 응용 프로그램 프로젝트에 대 한 미리 컴파일 개요](https://msdn.microsoft.com/library/aa983464.aspx) (MSDN).
- [패키지/게시 웹 탭, 프로젝트 속성](https://msdn.microsoft.com/library/dd410108.aspx) (MSDN).
- [고급 설정 대화 상자를 미리 컴파일하](https://msdn.microsoft.com/library/hh475319.aspx) (MSDN).


<a id="intranet"></a>


## <a name="deploying-an-intranet-web-application"></a>인트라넷 웹 응용 프로그램 배포

- [온-프레미스 조직 인증 옵션 (ADFS)를 사용 하 여 Visual Studio 2013에서 ASP.NET과](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/) (Vittorio Bertocci 하 여 블로그).
- [ASP.NET MVC를 사용 하 여 인트라넷 사이트 만드는 방법](https://msdn.microsoft.com/library/gg703322(VS.98).aspx) (MSDN). Visual Studio 2010에 대 한 이전 연습 기록 된 인트라넷 프로젝트 템플릿에서 Visual Studio 2013에 도입 된 주요 변경 사항이 반영 되지 않습니다.


<a id="automating"></a>


## <a name="automating-common-deployment-tasks-that-are-not-automated-out-of-the-box"></a>기본 자동화 되지 않음은 일반적인 배포 작업 자동화

- [Visual Studio를 사용 하 여 ASP.NET 웹 배포: 불필요 한 파일이 배포](../web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files.md)합니다.
- [웹 게시에 폴더 사용 권한을 설정](http://sedodream.com/2011/11/08/SettingFolderPermissionsOnWebPublish.aspx) (Sayed Hashimi 블로그).
- [웹 프로젝트 패키지에 대 한 레지스트리 설정을 포함 하도록 대상 파일을 확장 하는 방법](https://blogs.msdn.com/webdevtools/archive/2010/02/09/how-to-extend-target-file-to-include-registry-settings-for-web-project-package.aspx) (웹 개발 도구와 블로그).
- [확장 XML (Web.config) 변환을](http://sedodream.com/2010/09/09/ExtendingXMLWebconfigConfigTransformation.aspx) (Sayed Hashimi 블로그). 사용자 지정 XDT 변환을 만드는 방법을 보여 줍니다.
- [웹 배포 도구 (MSDeploy) 사용자 지정 공급자 Take 1](http://sedodream.com/2010/03/11/WebDeploymentToolMSDeployCustomProviderTake1.aspx) (Sayed Hashimi 블로그). 웹 배포 사용자 지정 공급자를 만드는 방법을 보여 줍니다.
- [패키지 및 COM 구성 요소를 배포 하는 방법](https://blogs.msdn.com/webdevtools/archive/2010/03/03/how-to-package-and-deploy-com-component.aspx) (웹 개발 도구와 블로그).
- [.NET 어셈블리를 패키지 하는 방법](https://blogs.msdn.com/webdevtools/archive/2010/02/19/how-to-package-com-component.aspx) (웹 개발 도구와 블로그). GAC에 어셈블리를 배포 하는 방법.
- [모든 IIS, 웹 배포 및 기타 정보를 사용 하 여 웹 서버에 대 한 Initialize Your Windows Azure VM으로 스크립팅](http://www.tugberkugurlu.com/archive/script-out-everything-initialize-your-windows-azure-vm-for-your-web-server-with-iis-web-deploy-and-other-stuff) (Tugberk Ugurlu 블로그).


<a id="configuringservers"></a>


## <a name="configuring-web-servers-so-that-developers-can-deploy-web-applications-to-them-using-web-deploy"></a>개발자가 웹 배포를 사용 하 여 웹 응용 프로그램을 배포할 수 있도록 웹 서버를 구성 합니다.

- [관리자 및 관리자가 아닌 배포에 대 한 웹 배포 설치 및 구성](https://www.iis.net/learn/install/installing-publishing-technologies/installing-and-configuring-web-deploy) (IIS.net 사이트).


<a id="hostingprovider"></a>


## <a name="configuring-servers-for-a-hosting-provider"></a>호스팅 공급자에 대 한 서버 구성

- [Microsoft ASP.NET 4 호스팅 배포 가이드](https://go.microsoft.com/fwlink/?LinkId=191365) (Microsoft 다운로드 센터).
- [프로필 XML 파일을 생성](https://www.iis.net/learn/web-hosting/joining-the-web-hosting-gallery/generate-a-profile-xml-file) (IIS.net 사이트).


<a id="troubleshooting"></a>


## <a name="troubleshooting-deployment-problems"></a>배포 문제 해결

- [Visual Studio에서 Windows Azure 웹 사이트 문제 해결](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio) (Microsoft Azure 사이트).
- [Visual Studio를 사용 하 여 ASP.NET 웹 배포: 문제 해결](../web-forms/overview/deployment/visual-studio-web-deployment/troubleshooting.md)합니다.
- [일반적인 문제 해결 웹 문제 배포](https://www.iis.net/learn/publish/troubleshooting-web-deploy/troubleshooting-common-problems-with-web-deploy)합니다.
- [배포 오류 코드를 웹](https://www.iis.net/learn/publish/troubleshooting-web-deploy/web-deploy-error-codes) (IIS.net 사이트).
- [Visual Studio 및 ASP.NET에 대 한 배포 FAQ 웹](https://msdn.microsoft.com/library/ee942158.aspx) (MSDN).
- [IIS와 ASP.NET 개발 서버 간의 차이 핵심](../web-forms/overview/older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md)합니다.
- [개발 및 프로덕션 간의 일반적인 구성 차이](../web-forms/overview/older-versions-getting-started/deploying-web-site-projects/common-configuration-differences-between-development-and-production-cs.md)합니다.
- [보통 신뢰 ASP.NET 응용 프로그램 호스팅](http://www.4guysfromrolla.com/articles/100307-1.aspx) (4 Guy Rolla 사이트에서).


<a id="gettinghelp"></a>


## <a name="getting-help-with-a-specific-deployment-question"></a>특정 배포 질문 도움말 보기

- [ASP.NET 구성 및 배포 포럼](https://forums.asp.net/26.aspx/1?Configuration and Deployment)합니다.
- [StackOverflow.com](http://www.StackOverflow.com).


<a id="additional"></a>


## <a name="additional-resources"></a>추가 리소스

이 섹션에서는 Visual Studio 및 IIS 배포 도구를 사용 하는 방법에 대 한 자세한 학습에 유용한 추가 리소스 링크를 제공 합니다.

다음 블로그 자주 Visual Studio 웹 배포에 대 한 정보를 포함 합니다.

- [웹 개발 도구를 Microsoft 블로그 언제](https://blogs.msdn.com/b/webdevtools/)합니다.
- [Sayed Hashimi 블로그](http://www.sedodream.com/)합니다.

다음 리소스는 웹 배포, Visual Studio를 사용 하 여 웹 응용 프로그램 프로젝트 배포 작업을 수행 하는 IIS 프레임 워크에 대 한 설명서를 제공 합니다. 웹에서 배포에 대해 질문할 수는 [웹 배포 도구 포럼](https://go.microsoft.com/fwlink/?LinkId=149411) IIS.net 웹 사이트에 있습니다.

- [웹 소개 배포](https://www.iis.net/learn/publish/using-web-deploy/introduction-to-web-deploy)합니다.
- [설치 및 구성 웹 배포](https://www.iis.net/learn/install/installing-publishing-technologies/installing-and-configuring-web-deploy)합니다.
- [설치 프로그램을 배포 하는 웹을 자동화 하기 위한 PowerShell 스크립트](https://www.iis.net/learn/publish/using-web-deploy/powershell-scripts-for-automating-web-deploy-setup)합니다.
- [웹 배포 도구](https://go.microsoft.com/fwlink/?LinkId=151481)합니다. TechNet 사이트에서 웹 배포 설명서에 대 한 목차 노드의 최상위 테이블입니다. 유용한 참조 정보 대부분 년에 대 한 페이지를 업데이트 하지 않은 TechNet의도 포함 됩니다.
- [Microsoft.Web.Deployment Namespace](https://go.microsoft.com/fwlink/?LinkId=148630)합니다. API 설명서 버전 1.0부터 바뀌지 않았습니다.
- [Microsoft 웹 배포 팀 블로그](https://blogs.iis.net/msdeploy/default.aspx)합니다.
- [IIS.net 웹 사이트의 게시 탭](https://www.iis.net/learn/publish)합니다.
