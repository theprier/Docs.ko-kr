---
uid: web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
title: 'Visual Studio를 사용 하 여 ASP.NET 웹 배포: Web.config 파일 변환 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시)에서 실행 중인 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/15/2013
ms.topic: article
ms.assetid: 5a2a927b-14cb-40bc-867a-f0680f9febd7
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
msc.type: authoredcontent
ms.openlocfilehash: 4d8a7d2a6faa0b03fff4416778101b47df2dd26e
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37371767"
---
<a name="aspnet-web-deployment-using-visual-studio-webconfig-file-transformations"></a>Visual Studio를 사용 하 여 ASP.NET 웹 배포: Web.config 파일 변환
====================
[Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> 이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시) Visual Studio 2012 또는 Visual Studio 2010을 사용 하 여 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자입니다. 시리즈에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](introduction.md)합니다.


## <a name="overview"></a>개요

이 자습서에서는 변경 프로세스를 자동화 하는 방법을 보여 줍니다 합니다 *Web.config* 다른 대상 환경에 배포할 때 파일입니다. 대부분의 응용 프로그램 설정에는 *Web.config* 응용 프로그램을 배포할 때 달라 야 하는 파일입니다. 이러한 변경을 수행한 프로세스를 자동화 하는 상당히 지루한 작업 및 오류가 발생 하기 쉽습니다 배포할 때마다 수동으로 수행 하지 않아도 유지 합니다.

미리 알림: 오류 메시지를 가져오거나 자습서를 진행할 때 작동 하지 않는 경우 확인 해야 합니다 [문제 해결 페이지](troubleshooting.md)합니다.

## <a name="webconfig-transformations-versus-web-deploy-parameters"></a>웹 배포 매개 변수 및 Web.config 변환

변경 하는 프로세스를 자동화 하는 방법은 두 가지가 *Web.config* 파일 설정: [Web.config 변환](https://msdn.microsoft.com/library/dd465326.aspx) 하 고 [웹 배포 매개 변수](https://msdn.microsoft.com/library/ff398068.aspx)합니다. A *Web.config* 변환 파일을 변경 하는 방법을 지정 하는 XML 태그를 포함 합니다 *Web.config* 배포 될 때 파일입니다. 특정 다른 변경 내용을 빌드 구성 및 특정 게시 프로필을 지정할 수 있습니다. 기본 빌드 구성이 디버그 및 릴리스, 되며 사용자 지정 빌드 구성을 만들 수 있습니다. 게시 프로필은 일반적으로 대상 환경에 해당합니다. (자세히 게시 프로필에 배웁니다 합니다 [IIS 테스트 환경으로 배포](deploying-to-iis.md) 자습서입니다.)

다양 한 종류의에서 발견 되는 설정을 비롯 하 여 배포 하는 동안 구성 해야 하는 설정 지정 하려면 웹 배포 매개 변수를 사용할 수 *Web.config* 파일입니다. 지정 하는 데 사용 하는 경우 *Web.config* 파일 변경 내용이 웹 배포 매개 변수는 설정 하기가 더 복잡 하지만 배포할 때까지 설정 값을 알 수 없는 경우에 유용 합니다. 예를 들어, 엔터프라이즈 환경에서 만들 수 있습니다는 *배포 패키지* 프로덕션 환경에서 설치 하려면 IT 부서에서 사용자에 게 제공 하 고 해당 사용자를 연결 문자열 또는 하지 암호를 입력할 수 해야 합니다. 알고 있어야 합니다.

이 자습서 시리즈에 설명 하는 시나리오의 경우 사전에 알고를 수행 하는 모든 항목을 *Web.config* 파일 이기 때문에 웹 배포 매개 변수를 사용할 필요가 없습니다. 를 사용 하는 빌드 구성에 따라 다른 및 사용 하는 게시 프로필에 따라 다른 일부는 몇 가지 변환을 구성 합니다.

<a id="watransforms"></a>

## <a name="specifying-webconfig-settings-in-azure"></a>Azure에서 Web.config 설정 지정

경우는 *Web.config* 변경 하려면 원하는 파일 설정에는 `<connectionStrings>` 또는 `<appSettings>` 요소를 자동화 하는 동안 변경 내용에 대 한 다른 옵션이 Azure App Service에서 Web Apps에 배포 하는 경우 및 배포 합니다. Azure에서 적용 하려는 설정을 입력할 수는 **구성** 웹 앱에 대 한 관리 포털 페이지의 탭 (아래로 스크롤하여는 **앱 설정** 및 **연결 문자열**  섹션). 프로젝트를 배포할 때 Azure는 자동으로 변경 내용을 적용 합니다. 자세한 내용은 [Windows Azure 웹 사이트: 응용 프로그램 문자열 및 연결 문자열 작동 방식](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx)합니다.

## <a name="default-transformation-files"></a>기본 변환 파일

**솔루션 탐색기**, 확장 *Web.config* 보려는 합니다 *Web.Debug.config* 하 고 *Web.Release.config* 변환 파일을 두 개의 기본 빌드 구성에 대해 기본적으로 생성 됩니다.

![Web.config_transform_files](web-config-transformations/_static/image1.png)

Web.config 파일을 마우스 오른쪽 단추로 클릭 하 고 선택 하 여 사용자 지정 빌드 구성에 대 한 변환 파일을 만들 수 있습니다 **Config 변환 추가** 상황에 맞는 메뉴입니다. 이 자습서를 수행할 필요가 없습니다 및 메뉴 옵션을 사용 하지 않으면 모든 사용자 지정 빌드 구성을 만들지 때문입니다.

나중을 만든 세 가지 자세한 변환 파일을 각각 테스트에 대 한 스테이징 및 프로덕션 게시 프로필. 대상 환경에 종속 되므로 게시 프로필 변환 파일에서 처리할 수 있습니다 하는 설정의 일반적인 예는 테스트 또는 프로덕션에 대 한 다른 WCF 끝점. 만든 게시 프로필 변환 파일 나중에 자습서에서 사용 하 여 이동 하는 게시 프로필을 만든 후 합니다.

## <a name="disable-debug-mode"></a>디버그 모드를 사용 하지 않도록 설정

대상 환경은 대신 빌드 구성에 따라 달라 지는 설정의 예로 `debug` 특성입니다. 릴리스 빌드의 경우 일반적으로 원하는 디버깅 사용 안 함에 배포 되는 환경에 관계 없이 합니다. 따라서 기본적으로 Visual Studio 프로젝트 템플릿 만들기 *Web.Release.config* 를 제거 하는 코드를 사용 하 여 파일을 변환 합니다 `debug` 에서 특성을 `compilation` 요소입니다. 기본 다음과 같습니다 *Web.Release.config*: 코드에서 주석으로 처리 되는 몇 가지 샘플 변환 코드 외에도 포함 합니다 `compilation` 요소를 제거 하는 `debug` 특성:

[!code-xml[Main](web-config-transformations/samples/sample1.xml?highlight=18)]

`xdt:Transform="RemoveAttributes(debug)"` 특성 것임을 지정 합니다 `debug` 에서 제거할 특성을 `system.web/compilation` 배포에서 요소 *Web.config* 파일. 이 릴리스 빌드를 배포할 때마다 수행 됩니다.

## <a name="limit-error-log-access-to-administrators"></a>관리자에 게 오류 로그 액세스를 제한 합니다.

응용 프로그램을 실행 하는 동안 오류가 발생 하는 응용 프로그램 오류 시스템에서 생성 된 페이지 대신 일반 오류 페이지를 표시 하 고 사용 하는 경우는 [Elmah NuGet 패키지](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx) 오류 로깅 및 보고에 대 한 합니다. 합니다 `customErrors` 응용 프로그램에서 요소 *Web.config* 오류 페이지를 지정 하는 파일:

[!code-xml[Main](web-config-transformations/samples/sample2.xml)]

오류 페이지를 보려면 일시적으로 변경 합니다 `mode` 특성은 `customErrors` "RemoteOnly"를 "On" 및 Visual Studio에서 응용 프로그램을 실행 하는 요소. 와 같은 잘못 된 URL을 요청 하 여 오류를 발생 시킬 *Studentsxxx.aspx*합니다. IIS에서 생성 된 "리소스를 찾을 수 없습니다" 오류 대신 페이지를 표시 합니다 *GenericErrorPage.aspx* 페이지입니다.

![오류 페이지](web-config-transformations/_static/image2.png)

오류 로그를 보려면 대체 URL에 사용 하 여 포트 번호 뒤 *elmah.axd* (예를 들어 `http://localhost:51130/elmah.axd`) Enter 키를 누릅니다.

![ELMAH 페이지](web-config-transformations/_static/image3.png)

로 설정 해야 합니다 `customErrors` "RemoteOnly" 모드로 완료 되 면 요소입니다.

개발 컴퓨터에 보안 위험이 있는 프로덕션 환경에서 오류 로그 페이지에 무료로 액세스할 수 있도록 유용 합니다. 관리자에 게 오류 로그 액세스를 제한 하는 권한 부여 규칙을 추가 하 고 제한 하면 작동 하는지 확인 하려는 프로덕션 사이트에 대 한 테스트 및 스테이징도에서 원하는 합니다. 따라서이 릴리스 빌드를 배포할 때마다 및에 속해 있으므로 구현 하려는 또 다른 변화가 합니다 *Web.Release.config* 파일입니다.

열기 *Web.Release.config* 새 추가한 `location` 닫기 직전 요소 `configuration` 태그를 다음과 같이 합니다.

[!code-xml[Main](web-config-transformations/samples/sample3.xml?highlight=27-34)]

`Transform` 특성 값이 "Insert" 이면이 `location` 기존에 형제로 추가할 요소 `location` 요소에는 *Web.config* 파일. (이미 하나 `location` 권한 부여를 지정 하는 요소에 대 한 규칙은 **업데이트 크레딧** 페이지입니다.)

이제는 하이 올바르게 코딩 되도록 변환을 미리 볼 수 있습니다.

**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 *Web.Release.config* 클릭 **Preview 변환**합니다.

![변환 메뉴 미리 보기](web-config-transformations/_static/image4.png)

개발 보여 주는 페이지가 열립니다 *Web.config* 파일 및를 왼쪽에 배포 된 *Web.config* 파일 보이는지 오른쪽의 변경 내용을 강조 표시 합니다.

![디버그 변환의 미리 보기](web-config-transformations/_static/image5.png)

![위치 변환의 미리 보기](web-config-transformations/_static/image6.png)

(미리 보기에서 알 수 있듯이 직접 작성 하지 않은 일부 추가 변경 사항에 대 한 변환: 일반적으로 관련 되어 이러한 기능에 영향을 주지는 공백을 제거 합니다.)

배포 후 사이트를 테스트 하는 경우 권한 부여 규칙을이 유효한 지 확인도 테스트할 수 있습니다.

> [!NOTE] 
> 
> **보안 정보** 프로덕션 응용 프로그램에서 public에 오류 세부 정보를 표시 하거나 공용 위치에 해당 정보를 저장 하지 않습니다. 공격자는 오류 정보를 사용 하 여 취약점으로 인 한 사이트를 검색할 수 있습니다. 사용자 고유의 응용 프로그램에서 ELMAH를 사용 하는 경우 보안 위험을 최소화 하기 위해 ELMAH를 구성 합니다. 이 자습서에서 ELMAH 예제 간주 되지 않아야 권장된 구성. 예제 응용 프로그램에서 파일을 만들 수 있어야 하는 폴더를 처리 하는 방법을 보여 주기 위해 선택 된 경우 자세한 내용은 [ELMAH 끝점을 보호](https://code.google.com/p/elmah/wiki/SecuringErrorLogPages)합니다.


## <a name="a-setting-that-youll-handle-in-publish-profile-transformation-files"></a>처리할 수 있는 설정을 게시 프로필 변환 파일

일반적인 시나리오는 *Web.config* 파일에 배포 하는 각 환경에서 다 수 있어야 하는 설정입니다. 예를 들어, WCF 서비스를 호출 하는 응용 프로그램 테스트 및 프로덕션 환경에서 다른 끝점을 해야 합니다. Contoso University 응용 프로그램에 이러한 종류의 설정도 포함 됩니다. 이 설정은 사이트의 페이지에는 사용자의 환경, 개발, 테스트 또는 프로덕션 같은 알려 주는 표시기를 표시 합니다. 설정 값은 응용 프로그램 "(Dev)"를 추가 되 고 있는지 여부를 결정 하거나 "(테스트)"의 기본 제목을 합니다 *Site.Master* 마스터 페이지:

![환경 표시기](web-config-transformations/_static/image7.png)

응용 프로그램 스테이징 또는 프로덕션에서 실행 중인 경우 환경 표시기는 생략 됩니다.

Contoso University 웹 페이지에 설정 된 값을 읽을 `appSettings` 에 *Web.config* 어떤 환경에서 실행 중인 응용 프로그램을 확인 하기 위해 파일:

[!code-xml[Main](web-config-transformations/samples/sample4.xml)]

값 "Test" 테스트 환경에 있고 "Prod" 스테이징 및 프로덕션에 대 한 합니다.

변환 파일에서 다음 코드는이 변환을 구현 합니다.

[!code-xml[Main](web-config-transformations/samples/sample5.xml)]

합니다 `xdt:Transform` 특성 값이이 변환의 용도에 기존 요소의 특성 값을 변경 하는 "SetAttributes" 나타냅니다는 *Web.config* 파일입니다. 합니다 `xdt:Locator` 특성 값 "Match(key)" 수정할 요소를 하나 임을 나타냅니다입니다 `key` 일치 특성을 `key` 여기에 지정 된 특성입니다. 만 다른 특성의는 `add` 요소는 `value`, 변경 될 사항 되며 배포에 *Web.config* 파일입니다. 하면 여기에 나온 코드는 `value` 특성을 `Environment` `appSettings` "Test"로 설정 되는 요소는 *Web.config* 배포 되는 파일.

이 변환을 게시 프로필 변환 파일을 아직 만들지 않은에 속해 있습니다. 만들고 테스트, 스테이징 및 프로덕션 환경에 대 한 게시 프로필을 만들 때이 변경 내용을 구현 하는 변환 파일을 업데이트 합니다. 로그인 할 수 있습니다는 [IIS에 배포](deploying-to-iis.md) 하 고 [프로덕션 환경에 배포](deploying-to-production.md) 자습서입니다.

> [!NOTE]
> 이 설정은 때문에 합니다 `<appSettings>` 요소인 해야 Azure App Service 참조에서 Web Apps에 배포 하는 경우 변환 지정 하기 위한 또 다른 방법은 [Azure에서 지정 하는 Web.config 설정을](#watransforms) 의 앞부분에 나오는 이 항목입니다.


## <a name="setting-connection-strings"></a>연결 문자열 설정

기본 변환 파일에서 연결 문자열을 업데이트 하는 방법을 보여 주는 예제를 포함 되어 있지만 대부분의 경우에서 하지 필요가 설정 연결 문자열 변환 하기 위해 게시 프로필의 연결 문자열을 지정할 수 있으므로. 로그인 할 수 있습니다는 [IIS에 배포](deploying-to-iis.md) 하 고 [프로덕션 환경에 배포](deploying-to-production.md) 자습서입니다.

## <a name="summary"></a>요약

수행할 수 있는 만큼 이제 *Web.config* 변환 전에 게시 프로필을 만들고 배포 된 Web.config 파일의 수는 미리 보기를 살펴보았습니다.

![위치 변환의 미리 보기](web-config-transformations/_static/image8.png)

다음 자습서에서는 프로젝트 속성을 설정 해야 하는 배포 설정 작업의 처리 있습니다 됩니다.

## <a name="more-information"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 참조 하세요. [배포 하는 동안 대상 web.config 또는 app.config 파일의 설정을 변경 하려면 Web.config를 사용 하 여 변환](https://go.microsoft.com/fwlink/p/?LinkId=282413#transforms) 에 대 한 웹 배포 콘텐츠 맵 Visual Studio 및 ASP.NET입니다.

> [!div class="step-by-step"]
> [이전](preparing-databases.md)
> [다음](project-properties.md)
