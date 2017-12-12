---
uid: web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
title: "Visual Studio를 사용 하 여 ASP.NET 웹 배포: Web.config 파일 변환 | Microsoft Docs"
author: tdykstra
description: "이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시) 실행 하 여 웹 응용 프로그램을 Azure 앱 서비스 웹 앱 또는 타사 호스팅 공급자 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/15/2013
ms.topic: article
ms.assetid: 5a2a927b-14cb-40bc-867a-f0680f9febd7
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
msc.type: authoredcontent
ms.openlocfilehash: a88d8f35c770b362b74f787fee2c60a7577bccb2
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="aspnet-web-deployment-using-visual-studio-webconfig-file-transformations"></a>Visual Studio를 사용 하 여 ASP.NET 웹 배포: Web.config 파일 변환
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> 이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시) Visual Studio 2012 또는 Visual Studio 2010을 사용 하 여 웹 응용 프로그램을 Azure 앱 서비스 웹 앱 또는 타사 호스팅 공급자입니다. 계열에 대 한 정보를 참조 하십시오. [시리즈의 첫 번째 자습서](introduction.md)합니다.


## <a name="overview"></a>개요

이 자습서에서는 변경 프로세스를 자동화 하는 방법의 *Web.config* 파일을 다른 대상 환경에 배포 합니다. 대부분의 응용 프로그램 설정이 *Web.config* 파일을 응용 프로그램을 배포할 때 달라 야 합니다. 이러한 변경의 프로세스를 자동화 하 고 오류가 발생할 때 번거로울 것 배포 될 때마다 수동으로 수행 하지 않아도 유지 합니다.

미리 알림: 오류 메시지가 자습서를 진행할 때 작동 하지 않는 경우 반드시 확인는 [문제 해결 페이지](troubleshooting.md)합니다.

## <a name="webconfig-transformations-versus-web-deploy-parameters"></a>Web.config 변환 또는 웹 배포 매개 변수

변경 프로세스를 자동화 하는 방법은 두 가지가 *Web.config* 파일 설정: [Web.config 변환](https://msdn.microsoft.com/en-us/library/dd465326.aspx) 및 [웹 배포 매개 변수](https://msdn.microsoft.com/en-us/library/ff398068.aspx)합니다. A *Web.config* 변경 하는 방법을 지정 하는 XML 태그를 포함 하는 변환 파일은 *Web.config* 배포 될 때 파일입니다. 다른 특정 빌드 구성 변경과 관련에 대 한 게시 프로필을 지정할 수 있습니다. 기본 빌드 구성이 디버그 및 릴리스, 되며 사용자 지정 빌드 구성을 만들 수 있습니다. 게시 프로필은 일반적으로 대상 환경에 해당합니다. (의 프로필 게시에 대해 자세히 알아봅니다는 [iis 테스트 환경으로 배포](deploying-to-iis.md) 자습서입니다.)

웹 배포 매개 변수를 사용 하 여에서 발견 되는 설정을 포함 하 여 배포 하는 동안 구성 해야 하는 설정의 다양 한 종류를 지정할 수 있습니다 *Web.config* 파일입니다. 지정 하는 데 사용 하는 경우 *Web.config* 파일 변경, 웹 배포 매개 변수는 설정 하기가 더 복잡 하지만 값을 배포할 때까지 설정할 수 있는 알지 못할 경우에 유용 합니다. 예를 들어, 엔터프라이즈 환경에서 만들 수 있습니다는 *배포 패키지* 및 프로덕션 환경에서 설치 하려면 IT 부서에서 사용자에 게 지정 하 고 그 사람이 연결 문자열 또는 하지 않도록 암호를 입력할 수 알고 있습니다.

이 자습서 시리즈 검사 하는 시나리오를 위해 미리 알고 있는 하기 위해 수행 해야 하는 모든 항목은 *Web.config* 파일 이기 때문에 웹 배포 매개 변수를 사용할 필요가 없습니다. 을 사용 하는 빌드 구성에 따라 다른 및 일부 다른 사용 될 게시 프로필이 따라 일부 변환을 구성 합니다.

<a id="watransforms"></a>

## <a name="specifying-webconfig-settings-in-azure"></a>Azure에서 Web.config 설정 지정

경우는 *Web.config* 중인 파일 설정을 변경 하려면 원하는 `<connectionStrings>` 또는 `<appSettings>` 요소를 자동화 하는 동안 변경 내용에 대 한 또 다른 옵션 했으므로 Azure 앱 서비스에서 웹 앱을 배포 하는 경우 배포 합니다. 에 Azure에서 적용 하려는 설정을 입력할 수는 **구성** 웹 앱에 대 한 관리 포털 페이지의 탭 (으로 아래로 스크롤하여는 **앱 설정** 및 **연결 문자열**  섹션). 프로젝트를 배포할 때 Azure는 자동으로 변경 내용을 적용 합니다. 자세한 내용은 참조 [Windows Azure 웹 사이트: 방법: 응용 프로그램 문자열 및 연결 문자열 작업](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx)합니다.

## <a name="default-transformation-files"></a>기본 변환 파일

**솔루션 탐색기**를 확장 하 고 *Web.config* 볼 수는 *Web.Debug.config* 및 *Web.Release.config* 변환 파일은 두 개의 기본 빌드 구성에 대해 기본적으로 생성 됩니다.

![Web.config_transform_files](web-config-transformations/_static/image1.png)

Web.config 파일을 마우스 오른쪽 단추로 클릭 하 고 선택 하 여 사용자 지정 빌드 구성에 대 한 변환 파일을 만들 수 있습니다 **구성 변환 추가** 상황에 맞는 메뉴입니다. 이 자습서를 수행할 필요가 없습니다 및 모든 사용자 지정 빌드 구성을 생성 하지 않은 때문에 메뉴 옵션을 해제 합니다.

나중에 만들게 세 자세한 변환 당 하나의 파일을 각 테스트, 준비를 및 프로덕션 게시 프로필 합니다. 처리 하는 것에 게시 프로필 변환 파일을 대상 환경에 따라 달라 지므로 하는 설정의 일반적인 예는 프로덕션 및 테스트에 대 한 다른 WCF 끝점입니다. 게시 프로필 변환 파일에서에서 만듭니다 이후의 자습서에 사용 되는 게시 프로필을 만든 후 합니다.

## <a name="disable-debug-mode"></a>디버그 모드를 사용 하지 않도록 설정

하지 않고 대상 환경에는 빌드 구성에 종속 되는 설정의 예는 `debug` 특성입니다. 릴리스 빌드에 대 한 일반적으로 원하는 비활성화 디버깅 환경을 관계 없이 배포 합니다. 따라서 기본적으로 Visual Studio 프로젝트 템플릿 만들기 *Web.Release.config* 파일을 제거 하는 코드로 변환는 `debug` 에서 특성은 `compilation` 요소입니다. 다음은 기본 *Web.Release.config*: 코드에서 주석 처리 하는 일부 샘플 변환 코드 외에도 포함는 `compilation` 제거 하는 요소는 `debug` 특성:

[!code-xml[Main](web-config-transformations/samples/sample1.xml?highlight=18)]

`xdt:Transform="RemoveAttributes(debug)"` 특성 지정 되도록는 `debug` 특성에서 제거할는 `system.web/compilation` 요소에는 배포 된 *Web.config* 파일입니다. 이 릴리스 빌드를 배포할 때마다 수행 됩니다.

## <a name="limit-error-log-access-to-administrators"></a>관리자에 대 한 오류 로그 액세스를 제한 합니다.

응용 프로그램을 실행 하는 동안 오류가 발생 하는 응용 프로그램 시스템에서 생성 된 오류 페이지 대신 일반 오류 페이지를 표시 하 고 사용 하 여는 [Elmah NuGet 패키지](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx) 오류 로깅 및 보고에 대 한 합니다. `customErrors` 응용 프로그램의 요소 *Web.config* 오류 페이지를 지정 하는 파일:

[!code-xml[Main](web-config-transformations/samples/sample2.xml)]

오류 페이지를 보려면 일시적으로 변경는 `mode` 특성에는 `customErrors` 의 요소를 "On" "RemoteOnly"와 Visual Studio에서 응용 프로그램을 실행 합니다. 와 같은 잘못 된 URL을 요청 하 여 오류가 발생 *Studentsxxx.aspx*합니다. IIS에서 생성 된 "리소스 찾을 수 없습니다" 오류 대신 페이지를 참조 하는 *GenericErrorPage.aspx* 페이지.

![오류 페이지](web-config-transformations/_static/image2.png)

오류 로그를 보려면 대체 URL의 모든 개체와 포트 번호 뒤 *elmah.axd* (예를 들어 `http://localhost:51130/elmah.axd`) Enter 키를 누릅니다.

![ELMAH 페이지](web-config-transformations/_static/image3.png)

설정 해야는 `customErrors` "RemoteOnly" 모드로 완료 되 면 요소입니다.

이 개발 컴퓨터에서 오류 로그 페이지에 있지만 보안 위험이 프로덕션 환경에서 사용 가능한 액세스를 허용 하도록 편리 합니다. 관리자에 게 오류 로그 액세스를 제한 하는 권한 부여 규칙을 추가 하 고 제한 하면 작동 하는지 확인 하려는 프로덕션 사이트에 대 한 테스트와도 준비에서 원하는 합니다. 따라서이 다른 변경 내용에 속해 있으므로 및 릴리스 빌드를 배포할 때마다 구현 하려는 *Web.Release.config* 파일입니다.

열기 *Web.Release.config* 를 새로 추가 `location` 닫는 바로 앞 요소 `configuration` 태그를 다음과 같이 합니다.

[!code-xml[Main](web-config-transformations/samples/sample3.xml?highlight=27-34)]

`Transform` "삽입"의 특성 값으로 인해이 `location` 기존에 형제로 추가 `location` 의 요소는 *Web.config* 파일입니다. (하나도 이미 `location` 규칙에 대 한 권한 부여를 지정 하는 요소는 **업데이트 크레딧** 페이지입니다.)

이제는 코딩 것 올바르게 되도록 변환을 미리 볼 수 있습니다.

**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 *Web.Release.config* 클릭 **미리 보기 변환**합니다.

![미리 보기 변형 메뉴](web-config-transformations/_static/image4.png)

개발을 보여 주는 페이지가 열리면 *Web.config* 왼쪽 내용에 파일에서 배포 된 *Web.config* 파일 버리면 오른쪽에 강조 표시 하는 변경 내용으로 합니다.

![디버그 변환의 미리 보기](web-config-transformations/_static/image5.png)

![위치 변환의 미리 보기](web-config-transformations/_static/image6.png)

(미리 보기에서 눈에 띄지 직접 작성 하지 않은 일부 변경에 대 한 변환: 기능에 영향을 주지는 공백을 제거 하 고 일반적으로 다음이 포함 될.)

배포 후 사이트를 테스트 하는 경우 권한 부여 규칙이 유효한 지 확인 하려면 테스트할 것입니다.

> [!NOTE] 
> 
> **보안 정보** 프로덕션 응용 프로그램에서 public에 오류 세부 정보를 표시 하거나 공용 위치에 해당 정보를 저장 하지 않습니다. 공격자가 사이트에 대 한 취약점 오류 정보를 사용할 수 있습니다. 응용 프로그램에서 ELMAH를 사용 하는 경우 보안 위험을 최소화 하기 위해 ELMAH를 구성 합니다. 이 자습서에서 ELMAH 예제 간주 되지 않아야 권장된 구성. 응용 프로그램에서 파일을 만들 수 있어야 하는 폴더를 처리 하는 방법을 보여 주기 위해 선택 하는 예입니다. 자세한 내용은 참조 [ELMAH 끝점 보안](https://code.google.com/p/elmah/wiki/SecuringErrorLogPages)합니다.


## <a name="a-setting-that-youll-handle-in-publish-profile-transformation-files"></a>처리할 수 있는 설정을 게시 프로필 변환 파일

일반적인 시나리오는 한 *Web.config* 파일에 배포 하는 각 환경에 달라 야 하는 설정입니다. 예를 들어 WCF 서비스를 호출 하는 응용 프로그램 테스트 및 프로덕션 환경에서 다른 끝점을 할 수 있습니다. Contoso 대학교 응용 프로그램은 이러한 종류의 설정도 포함합니다. 이 설정은 사이트의 페이지에는 in, 개발, 테스트 또는 프로덕션 같은 환경을 알려 주는 표시기를 표시를 제어 합니다. 설정 값은 응용 프로그램 "(Dev)" 추가 되 고 있는지 여부를 결정 하거나 "(테스트)"에서 기본 머리글을는 *Site.Master* 마스터 페이지:

![환경 표시기](web-config-transformations/_static/image7.png)

환경 표시기는 스테이징 또는 프로덕션에서 응용 프로그램이 실행 중인 경우 무시 됩니다.

Contoso 대학 웹 페이지에서 설정 된 값을 읽기 `appSettings` 에 *Web.config* 응용 프로그램에서 실행 중인 환경을 확인 하기 위해 파일:

[!code-xml[Main](web-config-transformations/samples/sample4.xml)]

값 "Test" 테스트 환경에서와 스테이징 및 프로덕션에 대 한 "프로덕션" 합니다.

변환 파일에서 다음 코드는이 변환을 구현 합니다.

[!code-xml[Main](web-config-transformations/samples/sample5.xml)]

`xdt:Transform` 특성 값이이 변환의 목적에서 기존 요소 특성 값을 변경 된다는 "SetAttributes" 의미는 *Web.config* 파일입니다. `xdt:Locator` 특성 값 "Match(key)" 요소를 수정할 수는 하나 임을 나타냅니다. 해당 `key` 일치 특성는 `key` 여기에서 지정 된 특성입니다. 만 다른 특성의는 `add` 요소는 `value`, 변경 될 사항이 배포 된 *Web.config* 파일입니다. 원인을 여기 표시 된 코드는 `value` 특성의는 `Environment` `appSettings` 에서 "Test"로 설정 하는 요소는 *Web.config* 배포 되는 파일입니다.

이 변환은 아직 만들지 않은 있는 게시 프로필 변환 파일에 속합니다. 작성 하 고 테스트, 스테이징 및 프로덕션 환경에 대 한 게시 프로필을 만들 때이 변경 내용을 구현 하는 변환 파일을 업데이트 합니다. 작업입니다는 [IIS에 배포](deploying-to-iis.md) 및 [프로덕션 환경으로 배포](deploying-to-production.md) 자습서입니다.

> [!NOTE]
> 이 설정은 이므로 `<appSettings>` Azure 앱 서비스 참조의 웹 앱에 배포 하는 경우 변환 지정 하기 위한 또 다른 방법은 있는 요소를 [Azure에서 지정 하는 Web.config 설정을](#watransforms) 의 앞부분에 나오는 이 항목의 합니다.


## <a name="setting-connection-strings"></a>연결 문자열 설정

기본 변환 파일에서 연결 문자열을 업데이트 하는 방법을 보여 주는 예제를 포함 되어 있지만 대부분의 경우에서 필요가 없습니다 연결 문자열 변환을 설정 하려면 게시 프로필에 연결 문자열을 지정할 수 있으므로 합니다. 작업입니다는 [IIS에 배포](deploying-to-iis.md) 및 [프로덕션 환경으로 배포](deploying-to-production.md) 자습서입니다.

## <a name="summary"></a>요약

된 수 만큼 이제 *Web.config* 게시 프로필을 만들고 배포 된 Web.config 파일에는 것의 미리 보기를 살펴 보았으며 전에 변환 합니다.

![위치 변환의 미리 보기](web-config-transformations/_static/image8.png)

다음 자습서에서 있습니다 수 작업을 처리할 배포 설치 프로젝트 속성을 설정 해야 하는 합니다.

## <a name="more-information"></a>추가 정보

이 자습서에서 포함 하는 항목에 대 한 자세한 내용은 참조 [배포 중 대상 Web.config 파일 또는 app.config 파일에서 설정을 변경 하려면 Web.config를 사용 하 여 변환](https://go.microsoft.com/fwlink/p/?LinkId=282413#transforms) 에 대 한 웹 배포 콘텐츠 맵 Visual Studio 및 ASP.NET입니다.

>[!div class="step-by-step"]
[이전](preparing-databases.md)
[다음](project-properties.md)
