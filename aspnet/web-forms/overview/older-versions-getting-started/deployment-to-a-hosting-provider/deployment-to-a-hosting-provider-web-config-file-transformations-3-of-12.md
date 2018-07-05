---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12
title: 'SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여를 사용 하 여 ASP.NET 웹 응용 프로그램을 배포 합니다: Web.Config 파일 변환-3 / 12 | Microsoft Docs'
author: tdykstra
description: 이 시리즈의 자습서에서는 배포 하는 방법을 보여 줍니다 (게시) ASP.NET 웹 응용 프로그램 프로젝트 Visual Stu를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/17/2011
ms.topic: article
ms.assetid: 2b0df3d9-450b-4ea6-b315-4c9650722cad
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12
msc.type: authoredcontent
ms.openlocfilehash: b9f8213920e9e69885021666143612ce7c542b69
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37388078"
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-webconfig-file-transformations---3-of-12"></a>SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여를 사용 하 여 ASP.NET 웹 응용 프로그램을 배포 합니다: Web.Config 파일 변환-3 / 12
====================
[Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 이 시리즈의 자습서에서는 배포 하는 방법을 보여 줍니다 (게시) ASP.NET 웹용 Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 웹 응용 프로그램 프로젝트입니다. Visual Studio 2010 웹 게시 업데이트를 설치 하는 경우에 사용할 수 있습니다. 계열에 대 한 소개를 참조 하세요 [시리즈의 첫 번째 자습서](deployment-to-a-hosting-provider-introduction-1-of-12.md)합니다.
> 
> Visual Studio 2012 RC 출시 이후 도입 된 배포 기능을 보여 줍니다, 이외의 SQL Server Compact, SQL Server 버전을 배포 하는 방법을 보여 줍니다 및 Azure App Service Web Apps를 배포 하는 방법을 보여 줍니다 하는 자습서를 참조 하세요 [ASP.NET 웹 배포 Visual Studio를 사용 하 여](../../deployment/visual-studio-web-deployment/introduction.md)입니다.


## <a name="overview"></a>개요

이 자습서에서는 변경 프로세스를 자동화 하는 방법을 보여 줍니다 합니다 *Web.config* 다른 대상 환경에 배포할 때 파일입니다. 대부분의 응용 프로그램 설정에는 *Web.config* 응용 프로그램을 배포할 때 달라 야 하는 파일입니다. 이러한 변경을 수행한 프로세스를 자동화 하는 상당히 지루한 작업 및 오류가 발생 하기 쉽습니다 배포할 때마다 수동으로 수행 하지 않아도 유지 합니다.

미리 알림: 오류 메시지를 가져오거나 자습서를 진행할 때 작동 하지 않는 경우 확인 해야 합니다 [문제 해결 페이지](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)합니다.

## <a name="webconfig-transformations-versus-web-deploy-parameters"></a>Web.config 변환 또는 웹 배포 매개 변수

변경 하는 프로세스를 자동화 하는 방법은 두 가지가 *Web.config* 파일 설정: [Web.config 변환](https://msdn.microsoft.com/library/dd465326.aspx) 하 고 [웹 배포 매개 변수](https://msdn.microsoft.com/library/ff398068.aspx)합니다. A *Web.config* 변환 파일을 변경 하는 방법을 지정 하는 XML 태그를 포함 합니다 *Web.config* 배포 될 때 파일입니다. 특정 다른 변경 내용을 빌드 구성 및 특정 게시 프로필을 지정할 수 있습니다. 기본 빌드 구성이 디버그 및 릴리스, 되며 사용자 지정 빌드 구성을 만들 수 있습니다. 게시 프로필은 일반적으로 대상 환경에 해당합니다. (자세히 게시 프로필에 배웁니다 합니다 [IIS 테스트 환경으로 배포](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md) 자습서입니다.)

다양 한 종류의에서 발견 되는 설정을 비롯 하 여 배포 하는 동안 구성 해야 하는 설정 지정 하려면 웹 배포 매개 변수를 사용할 수 *Web.config* 파일입니다. 지정 하는 데 사용 하는 경우 *Web.config* 파일 변경 내용이 웹 배포 매개 변수는 설정 하기가 더 복잡 하지만 배포할 때까지 설정 값을 알 수 없는 경우에 유용 합니다. 예를 들어, 엔터프라이즈 환경에서 만들 수 있습니다는 *배포 패키지* 프로덕션 환경에서 설치 하려면 IT 부서에서 사용자에 게 제공 하 고 해당 사용자를 연결 문자열 또는 하지 암호를 입력할 수 해야 합니다. 알고 있어야 합니다.

이 자습서에서 다루는 시나리오의 경우 알고를 수행 하는 모든 항목을 *Web.config* 파일 이기 때문에 웹 배포 매개 변수를 사용할 필요가 없습니다. 를 사용 하는 빌드 구성에 따라 다른 및 사용 하는 게시 프로필에 따라 다른 일부는 몇 가지 변환을 구성 합니다.

## <a name="creating-transformation-files-for-publish-profiles"></a>게시 프로필에 대 한 변환 파일 만들기

**솔루션 탐색기**, 확장 *Web.config* 보려는 합니다 *Web.Debug.config* 하 고 *Web.Release.config* 변환 파일을 두 개의 기본 빌드 구성에 대해 기본적으로 생성 됩니다.

![Web.config_transform_files](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image1.png)

Web.config 파일을 마우스 오른쪽 단추로 클릭 하 고 선택 하 여 사용자 지정 빌드 구성에 대 한 변환 파일을 만들 수 있습니다 **Config 변환 추가** 상황에 맞는 메뉴에서 있지만이 자습서를 수행할 필요가 없습니다.

빌드 구성이 아닌 배포 대상에 관련 된 변경 내용을 구성 하기 위한 두 변환 파일을 필요가 있습니다. 이 유형의 설정의 일반적인 예는 테스트 또는 프로덕션에 대 한 다른 WCF 끝점. 게시 해야 테스트 및 프로덕션과 명명 된 프로필을 만든 이후 자습서에서 한 *Web.Test.config* 파일 및 *Web.Production.config* 파일입니다.

게시 프로필에 연결 된 변환 파일을 수동으로 생성 되어야 합니다. **솔루션 탐색기**ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **Windows 탐색기에서 폴더 열기**합니다.

![Open_folder_in_Windows_Explorer](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image2.png)

**Windows 탐색기**를 선택 합니다 *Web.Release.config* 파일, 파일을 복사한 다음 두 개의 복사본이 합니다. 이러한 복사본의 이름을 *Web.Production.config* 하 고 *Web.Test.config*한 다음 닫고 **Windows 탐색기**합니다.

**솔루션 탐색기**, 클릭 **새로 고침** 새 파일을 볼 수 있습니다.

선택 하 고 새 파일, 마우스 오른쪽 단추로 클릭 한 다음 클릭 **프로젝트에 포함** 상황에 맞는 메뉴입니다.

![프로젝트의 테스트 및 프로덕션 구성 파일을 포함 하 여](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image3.png)

선택에 이러한 파일 배포를 방지 하려면 **솔루션 탐색기**, 한 다음는 **속성** 창 변경 합니다 **빌드 작업** 속성**콘텐츠** 하 **None**합니다. (빌드 구성을 기반으로 하는 변환 파일 배포에서 자동으로 차단 됩니다.)

이제 입력 준비가 *Web.config* 변환에는 *Web.config* 변환 파일.

## <a name="limiting-error-log-access-to-administrators"></a>관리자에 게 오류 로그 액세스를 제한합니다.

응용 프로그램을 실행 하는 동안 오류가 발생 하는 응용 프로그램 오류 시스템에서 생성 된 페이지 대신 일반 오류 페이지를 표시 하 고 사용 하는 경우 [Elmah NuGet 패키지](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx) 오류 로깅 및 보고에 대 한 합니다. 합니다 `customErrors` 요소에는 *Web.config* 오류 페이지를 지정 하는 파일:

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample1.xml)]

오류 페이지를 보려면 일시적으로 변경 합니다 `mode` 특성은 `customErrors` "RemoteOnly"를 "On" 및 Visual Studio에서 응용 프로그램을 실행 하는 요소. 와 같은 잘못 된 URL을 요청 하 여 오류를 발생 시킬 *Studentsxxx.aspx*합니다. 표시는 IIS에서 생성 된 "찾을 수 없음" 오류 페이지를 대신 합니다 *GenericErrorPage.aspx* 페이지입니다.

[![Error_page](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image5.png)](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image4.png)

오류 로그를 보려면 대체 URL에 사용 하 여 포트 번호 뒤 *elmah.axd* (스크린 샷에 예 `http://localhost:51130/elmah.axd`) Enter 키를 누릅니다.

[![Elmah_log_page](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image7.png)](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image6.png)

로 설정 해야 합니다 `customErrors` "RemoteOnly" 모드로 완료 되 면 요소입니다.

개발 컴퓨터에 보안 위험이 있는 프로덕션 환경에서 오류 로그 페이지에 무료로 액세스할 수 있도록 유용 합니다. 프로덕션 사이트에 대 한 관리자를 방금에서 변환을 구성 하 여 오류 로그 액세스를 제한 하는 권한 부여 규칙을 추가할 수 있습니다 합니다 *Web.Production.config* 파일입니다.

오픈 *Web.Production.config* 새 추가한 `location` 요소 바로 뒤 `configuration` 태그를 다음과 같이 합니다. (만 추가 되었는지 확인 합니다 `location` 요소 및 일부 컨텍스트를 제공 하기 위해서만 여기 나와 있는 주변 태그 하지 않습니다.)

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample2.xml?highlight=2-9)]

`Transform` 특성 값이 "Insert" 이면이 `location` 기존에 형제로 추가할 요소 `location` 요소에는 *Web.config* 파일. (이미 하나 `location` 권한 부여를 지정 하는 요소에 대 한 규칙은 **업데이트 크레딧** 페이지입니다.) 배포 후 프로덕션 사이트를 테스트할 때이 권한 부여 규칙이 유효한 지 확인 하려면 테스트할 수 있습니다.

이 코드를 추가 하는 것이 없는 있도록 테스트 환경에서 오류 로그 액세스를 제한할 필요가 합니다 *Web.Test.config* 파일입니다.

> [!NOTE] 
> 
> **보안 정보** 프로덕션 응용 프로그램에서 public에 오류 세부 정보를 표시 하거나 공용 위치에 해당 정보를 저장 하지 않습니다. 공격자는 오류 정보를 사용 하 여 취약점으로 인 한 사이트를 검색할 수 있습니다. 사용자 고유의 응용 프로그램에서 ELMAH를 사용 하는 경우에 보안 위험을 최소화 하기 위해 ELMAH를 구성할 수 있는 방법을 조사 해야 합니다. 이 자습서에서 ELMAH 예제 간주 되지 않아야 권장된 구성. 예제 응용 프로그램에서 파일을 만들 수 있어야 하는 폴더를 처리 하는 방법을 보여 주기 위해 선택 된 경우


## <a name="setting-an-environment-indicator"></a>환경 표시기를 설정합니다.

일반적인 시나리오는 *Web.config* 파일에 배포 하는 각 환경에서 다 수 있어야 하는 설정입니다. 예를 들어, WCF 서비스를 호출 하는 응용 프로그램 테스트 및 프로덕션 환경에서 다른 끝점을 해야 합니다. Contoso University 응용 프로그램에 이러한 종류의 설정도 포함 됩니다. 이 설정은 사이트의 페이지에는 사용자의 환경, 개발, 테스트 또는 프로덕션 같은 알려 주는 표시기를 표시 합니다. 설정 값은 응용 프로그램 "(Dev)"를 추가 되 고 있는지 여부를 결정 하거나 "(테스트)"의 기본 제목을 합니다 *Site.Master* 마스터 페이지:

[![Environment_indicator](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image9.png)](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image8.png)

응용 프로그램이 프로덕션 환경에서 실행 중일 때 환경 표시기는 생략 됩니다.

Contoso University 웹 페이지에 설정 된 값을 읽을 `appSettings` 에 *Web.config* 어떤 환경에서 실행 중인 응용 프로그램을 확인 하기 위해 파일:

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample3.xml)]

값은 "Test" 테스트 환경에 "Prod" 프로덕션 환경에서 이어야 합니다.

열기 *Web.Production.config* 추가한는 `appSettings` 여는 태그 바로 앞에 요소를 `location` 요소 이전에 추가한:

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample4.xml)]

합니다 `xdt:Transform` 특성 값이이 변환의 용도에 기존 요소의 특성 값을 변경 하는 "SetAttributes" 나타냅니다는 *Web.config* 파일입니다. 합니다 `xdt:Locator` 특성 값 "Match(key)" 수정할 요소를 하나 임을 나타냅니다입니다 `key` 일치 특성을 `key` 여기에 지정 된 특성입니다. 만 다른 특성의는 `add` 요소는 `value`, 변경 될 사항 되며 배포에 *Web.config* 파일입니다. 이 코드를 사용 하면를 `value` 특성을 `Environment` `appSettings` "Prod"로 설정 되는 요소는 *Web.config* 프로덕션에 배포 되는 파일.

그런 다음 동일한 변경이 적용 *Web.Test.config* 집합을 제외 하 고 파일을 `value` "Prod" 대신 "test"입니다. 완료 되 면를 `appSettings` 단원의 *Web.Test.config* 다음과 같이 표시 됩니다.

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample5.xml)]

## <a name="disabling-debug-mode"></a>디버그 모드를 사용 하지 않도록 설정

릴리스 빌드의 경우 원하지 않는 디버깅을 사용할 수 있는 환경에 관계 없이 배포 하는 합니다. 기본적으로는 *Web.Release.config* 변환 파일을 제거 하는 코드를 사용 하 여 자동으로 만들어집니다 합니다 `debug` 에서 특성을 `compilation` 요소:

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample6.xml)]

합니다 `Transform` 원인 특성을 `debug` 특성이 생략에서 배포 된 *Web.config* 릴리스 빌드를 배포할 때마다 파일입니다.

이 동일한 변환 되므로 테스트 및 프로덕션의 변환 파일 릴리스 변환 파일을 복사 하 여 만든 합니다. 제거를 열고 각 파일 있습니다 중복 필요 없는 합니다 **컴파일** 요소를 저장 하 고 각 파일을 닫습니다.

## <a name="setting-connection-strings"></a>연결 문자열 설정

대부분의 경우에서 하지 필요가 설정 연결 문자열 변환 하기 위해 게시 프로필의 연결 문자열을 지정할 수 있으므로. 하지만 예외가 SQL Server Compact 데이터베이스를 배포 하는 경우 및 Entity Framework Code First 마이그레이션을 사용 하 여 대상 서버에서 데이터베이스를 업데이트 합니다. 이 시나리오에서는 데이터베이스 스키마 업데이트에 대 한 서버에서 사용할 수 있는 추가 연결 문자열을 지정 해야 합니다. 이 변환은 설정 하려면 추가 **&lt;connectionStrings&gt;** 요소 바로 뒤 **&lt;configuration&gt;** 둘 다에서 태그 합니다 *Web.Test.config* 하며 *Web.Production.config* 파일 변환 합니다.

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample7.xml)]

합니다 `Transform` 특성 지정이 연결 문자열에 추가할 것을 *connectionStrings* 배포에서 요소 *Web.config* 파일. (게시 프로세스가 만들지만이 추가 연결 문자열 자동으로 존재 하지 않는 경우에 대 한 기본적으로는 **providerName** 특성 설정 됩니다 `System.Data.SqlClient`, SQL Server Compact 용 하지 작동 하지 않습니다. 연결 문자열에 수동으로 추가 하 여 유지 배포 프로세스의 잘못 된 공급자 이름을 사용 하 여 연결 문자열 요소를 만들지 못하게 합니다.)

모든 지정 이제는 *Web.config* Contoso University 응용 프로그램 테스트 및 프로덕션 배포에 필요한 변환 합니다. 다음 자습서에서는 프로젝트 속성을 설정 해야 하는 배포 설정 작업의 처리 있습니다 됩니다.

## <a name="more-information"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 Web.config 변환 시나리오를 참조 하세요 [ASP.NET 배포 콘텐츠 맵](https://msdn.microsoft.com/library/bb386521.aspx)합니다.

> [!div class="step-by-step"]
> [이전](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md)
> [다음](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12.md)
