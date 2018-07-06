---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything
title: (Azure 사용 하 여 실제 클라우드 앱 빌드) 모든 것을 자동화 | Microsoft Docs
author: MikeWasson
description: 실제 세계 클라우드 앱 빌드 Azure 전자책을 사용 하 여 Scott Guthrie를 개발한 프레젠테이션을 기반으로 합니다. 13 패턴과 그을 수 있는 방법을 설명 하는 중...
ms.author: aspnetcontent
ms.date: 06/12/2014
ms.assetid: ba6e6baa-9b9f-471f-b39d-b007a3addadc
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything
msc.type: authoredcontent
ms.openlocfilehash: 87b697847845ab88943e7a659ccd9487b9408d5a
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37839637"
---
<a name="automate-everything-building-real-world-cloud-apps-with-azure"></a>(Azure 사용 하 여 실제 클라우드 앱 빌드) 모든 것을 자동화합니다
====================
하 여 [Mike Wasson](https://github.com/MikeWasson)하십시오 [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)

[다운로드 해결 프로젝트](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자책 다운로드](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> 합니다 **실제 세계 클라우드 앱 빌드 Azure** 전자책 Scott Guthrie를 개발한 프레젠테이션을 기반으로 합니다. 13 패턴 설명 하 고 도움이 될 수 있는 사례 성공적인 클라우드를 위한 웹 앱을 개발할 수 있습니다. 전자책 소개를 참조 하세요 [첫 번째 장에서](introduction.md)합니다.


살펴보겠습니다 처음 세 패턴은 모든 소프트웨어 개발 프로젝트에 있지만 클라우드 프로젝트에 특히에 실제로 적용 합니다. 이 패턴은 개발 작업을 자동화 하는 방법에 대 한 합니다. 중요 한 항목을 있기 수동 프로세스 속도가 느리고 오류가 발생 하기 쉽습니다. 가능 하면 빠르고 안정적으로 agile 워크플로 설정으로 많은 자동화 합니다. 되므로 고유 하 게 클라우드 개발에 대 한 온-프레미스 환경에서 자동화 하기가 어렵거나 되는 많은 작업을 쉽게 자동화할 수 있습니다. 예를 들어, 전체 테스트를 설정할 수 있습니다 새 웹 서버와 백 엔드 Vm을 포함 하 여 환경, 데이터베이스, blob storage (파일 저장소), 큐 등입니다.

## <a name="devops-workflow"></a>DevOps 워크플로

"DevOps." 라는 용어를 듣고 점점 더 용어는 소프트웨어를 효율적으로 개발 하기 위해 개발 및 운영 작업을 통합 해야 하는 인식에서 개발 했습니다. 사용 하도록 설정 하려는 워크플로 종류가 하나는 응용 프로그램을 개발, 배포의 프로덕션 사용에 대해 알아봅니다, 지금까지 배운에 대 한 응답에서이 변경 하 수 사이클 반복 하 여 빠르고 안정적으로.

일부 성공적인 클라우드 개발 팀은 하루에 여러 번 라이브 환경에 배포합니다. 주 버전을 배포 하는 데 Azure 팀 업데이트 하지만 이제 2 ~ 3 개월 마다 모든 2 ~ 3 일 및 주 릴리스 2 ~ 3 주마다 부분 업데이트를 릴리스 합니다. 해당 주기를 실제로 사용 하면 고객 피드백에 응답할 수 있습니다.

이 작업을 수행 하기 위해 반복 하 고 안정적 이며 예측 가능한 이며 낮은 주기 시간에는 개발 및 배포 주기를 사용 하도록 설정 해야 합니다.

![DevOps 워크플로](automate-everything/_static/image1.png)

즉, 기간 사이의 시간 기능에 대 한 아이디어가 있는 경우 고객은 사용 하 고 피드백을 제공 하는 경우 가능한 한 짧은 것 이어야 합니다. 처음 세 패턴이 모든 항목이 소스 제어를 자동화 하 고 해당 유형의 프로세스를 사용 하도록 설정 하기 위해 권장 되는 모범 사례에 대 한 모든는 지속적인 통합 및 업데이트-키를 누릅니다.

## <a name="azure-management-scripts"></a>Azure 관리 스크립트

에 [이 전자책은 소개](introduction.md), Azure 관리 포털-웹 기반 콘솔을 살펴보았습니다. 관리 포털을 사용 하면 모니터링 하 고 모든 Azure에서 배포한 리소스를 관리할 수 있습니다. 웹 앱 및 Vm과 같은 서비스를 삭제, 해당 서비스를 구성, 모니터링 서비스 작업을 만들고 등 쉬운 경우 뛰어난 도구 이지만 사용 하는 수동 프로세스입니다. 특히 팀 환경에서에서 권장 하는 모든 규모의 프로덕션 응용 프로그램을 개발 하려는 경우 포털 배우고 Azure를 탐색 하기 위해 UI 통해 이동 하 고 반복 해 서 수행 됩니다 하는 프로세스를 자동화 합니다.

관리 포털에서 또는 Visual Studio에서 수동으로 수행할 수 있는 거의 모든 REST 관리 API를 호출 하 여 수행할 수도 있습니다. 사용 하 여 스크립트를 작성할 수 있습니다 [Windows PowerShell](https://msdn.microsoft.com/library/windowsazure/jj156055.aspx), 또는 같은 오픈 소스 프레임 워크를 사용할 수 있습니다 [Chef](http://www.opscode.com/chef/) 하거나 [Puppet](http://puppetlabs.com/puppet/what-is-puppet)합니다. 또한 Mac 또는 Linux 환경에서 Bash 명령줄 도구를 사용할 수 있습니다. Azure는 다양 한 이러한 모든 환경에 대 한 스크립팅 Api 있고는 [.NET 관리 API](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx) 스크립트 대신 코드를 작성 하려는 경우.

Fix It 응용 프로그램에 대 한 테스트 환경을 만들고 해당 환경에 프로젝트를 배포 프로세스를 자동화 하는 몇 가지 Windows PowerShell 스크립트 만들었습니다 및 이러한 스크립트의 내용 중 일부를 살펴보겠습니다.

## <a name="environment-creation-script"></a>환경 생성 스크립트

살펴보겠습니다 첫 번째 스크립트 라고 *새로 만들기-AzureWebsiteEnv.ps1*합니다. Fix It 테스트용으로 앱을 배포할 수 있습니다 Azure 환경을 만듭니다. 이 스크립트가 수행 하는 주요 작업은 다음과 같습니다.

- 웹 앱을 만듭니다.
- 저장소 계정을 만듭니다. (필수 blob 및 큐에 대 한 뒷부분에서 살펴보겠지만.)
- SQL Database 서버 및 두 개의 데이터베이스를 만듭니다: 응용 프로그램 데이터베이스 및 멤버 자격 데이터베이스입니다.
- 저장소 계정 및 데이터베이스에 액세스 하는 앱은 사용 하는 Azure의 설정을 저장 합니다.
- 배포를 자동화 하는 데 사용할 설정 파일을 만듭니다.

### <a name="run-the-script"></a>스크립트를 실행 합니다.


> [!NOTE]
> 챕터의이 부분에는 스크립트 및 명령을 실행 하기 위해 입력 하는 예제를 보여 줍니다. 이 데모 스크립트를 실행 하기 위해 알아야 할 모든 것을 제공 하지 않습니다. 단계별 방법-을 수행-it 지침은 [부록: The이 샘플 응용 프로그램 수정](the-fix-it-sample-application.md#deploybase)합니다.


Azure 서비스를 관리 하는 PowerShell 스크립트를 실행 하려면 Azure PowerShell 콘솔을 설치 하 고 Azure 구독을 사용 하도록 구성 해야 합니다. 설정한 후에 다음과 같은 명령을 사용 하 여 Fix It 환경 만들기 스크립트를 실행할 수 있습니다.

`.\New-AzureWebsiteEnv.ps1 -Name <websitename> -SqlDatabasePassword <password>`

`Name` 매개 변수는 데이터베이스 및 저장소 계정을 만들 때 사용할 이름을 지정 하며 `SqlDatabasePassword` 매개 변수는 SQL Database에 대해 만들어질 관리자 계정에 대 한 암호를 지정 합니다. 다른 매개 변수를 살펴본 후 나중에 사용할 수 있습니다.

![PowerShell 창](automate-everything/_static/image2.png)

스크립트가 완료 되 면 나타나면 관리 포털에서 작성 합니다. 두 개의 데이터베이스를 찾을 수 있습니다.

![Databases](automate-everything/_static/image3.png)

저장소 계정:

![저장소 계정](automate-everything/_static/image4.png)

및 웹 앱을 추가 합니다.

![웹 사이트](automate-everything/_static/image5.png)

에 **구성** 탭 웹 앱에 대 한 저장소 계정 설정이 있습니다 및 SQL 데이터베이스 연결 문자열 설정 수정에 대 한이 앱을 볼 수 있습니다.

![connectionStrings 및 appSettings](automate-everything/_static/image6.png)

합니다 *Automation* 폴더가 포함 하 고 있습니다를  *&lt;websitename&gt;.pubxml* 파일. 이 파일에는 MSBuild가 방금 만든 Azure 환경에 응용 프로그램을 배포 하는 데 사용할 설정을 저장 합니다. 예를 들어:

[!code-xml[Main](automate-everything/samples/sample1.xml)]

알 수 있듯이 스크립트에 전체 테스트 환경에 만들어지고 전체 프로세스는 약 90 초 후에 수행 됩니다.

테스트 환경 만들기를 하려는 팀의 누군가가 하는 경우에 스크립트를 실행할 수 있습니다. 빠르지만 할 뿐만 아니라도 이러한 확신할 수 있습니다 사용 하 고 있다고 environment를 사용 하는 것과 동일 합니다. 으로 확신 하는 경우 모든 사용자가 작업을 수동으로 설정 관리 포털 UI를 사용 하 여 매우 수 없습니다.

### <a name="a-look-at-the-scripts"></a>스크립트 살펴보기

이 작업을 수행 하는 세 가지 스크립트 실제로 있습니다. 명령줄에서 하나를 호출 하 고 자동으로 사용 하 여 다른 두 작업 중 일부를 수행 합니다.

- *새 AzureWebSiteEnv.ps1* 은 주 스크립트입니다.

    - *새 AzureStorage.ps1* 저장소 계정을 만듭니다.
    - *새 AzureSql.ps1* 데이터베이스를 만듭니다.

### <a name="parameters-in-the-main-script"></a>기본 스크립트의 매개 변수

기본 스크립트를 *새로 만들기-AzureWebSiteEnv.ps1*, 여러 매개 변수를 정의 합니다.

[!code-powershell[Main](automate-everything/samples/sample2.ps1)]

두 개의 매개 변수가 필요 합니다.

- 스크립트로 생성 된 웹 앱의 이름입니다. (URL에도 사용 됩니다. `<name>.azurewebsites.net`.)
- 스크립트가 생성 하는 데이터베이스 서버의 새 관리자의 암호입니다.

선택적 매개 변수를 사용 하는 데이터 센터 위치 (기본값: "미국 서 부"), 데이터베이스 서버 관리자 이름 (기본값은 "dbuser"), 및 데이터베이스 서버용 방화벽 규칙을 지정할 수 있습니다.

### <a name="create-the-web-app"></a>웹 앱 만들기

이 스크립트는 먼저 호출 하 여 웹 앱을 만들 되는 `New-AzureWebsite` cmdlet으로 전달 되도록 웹 앱 이름 및 위치 매개 변수 값:

[!code-powershell[Main](automate-everything/samples/sample3.ps1?highlight=2)]

### <a name="create-the-storage-account"></a>저장소 계정 만들기

기본 스크립트를 실행 합니다는 <em>새로 만들기-AzureStorage.ps1</em> 스크립트를 지정 "<em>&lt;websitename&gt;</em>저장소" 저장소 계정 이름에 대 한 동일한 데이터 센터의 위치 및 웹 앱입니다.

[!code-powershell[Main](automate-everything/samples/sample4.ps1?highlight=3)]

*새 AzureStorage.ps1* 호출을 `New-AzureStorageAccount` 를 만들고 저장소 계정에이 cmdlet은 계정 이름과 액세스 키 값을 반환 합니다. 응용 프로그램 blob 및 큐 저장소 계정에 액세스 하려면 이러한 값이 필요 합니다.

[!code-powershell[Main](automate-everything/samples/sample5.ps1?highlight=2)]

새 저장소 계정을; 항상 원하는 수 없습니다. 필요에 따라 기존 저장소 계정을 사용 하도록 지시 하는 매개 변수를 추가 하 여 스크립트를 향상 시킬 수 있습니다.

### <a name="create-the-databases"></a>데이터베이스 만들기

기본 스크립트는 다음 데이터베이스 생성 스크립트를 실행 *새로 만들기-AzureSql.ps1*, 후 기본 데이터베이스 설정 및 방화벽 규칙 이름:

[!code-powershell[Main](automate-everything/samples/sample6.ps1)]

[!code-powershell[Main](automate-everything/samples/sample7.ps1?highlight=2)]

데이터베이스 생성 스크립트를 개발 컴퓨터의 IP 주소를 검색 하 고 개발 컴퓨터에 연결 하 고 서버를 관리할 수 있도록 방화벽 규칙을 설정 합니다. 그런 다음 데이터베이스 생성 스크립트를 데이터베이스를 설정 하려면 몇 가지 단계를 거칩니다.

- 사용 하 여 서버를 만드는 `New-AzureSqlDatabaseServer` cmdlet.

    [!code-powershell[Main](automate-everything/samples/sample8.ps1?highlight=1)]
- 서버를 관리 하 고 웹 앱에 연결할 수 있도록 개발 컴퓨터를 사용 하도록 설정 하는 방화벽 규칙을 만듭니다. 

    [!code-powershell[Main](automate-everything/samples/sample9.ps1?highlight=3,5)]
- 서버 이름 및 자격 증명을 사용 하 여 포함 된 데이터베이스 컨텍스트를 만듭니다.는 `New-AzureSqlDatabaseServerContext` cmdlet.

    [!code-powershell[Main](automate-everything/samples/sample10.ps1?highlight=4)]

    `New-PSCredentialFromPlainText` 함수를 호출 하는 스크립트에는 `ConvertTo-SecureString` 반환 고 암호를 암호화 하는 cmdlet을 `PSCredential` 개체는 동일한 형식를 `Get-Credential` cmdlet을 반환 합니다.
- 응용 프로그램 데이터베이스를 만들고 사용 하 여 멤버 자격 데이터베이스를 `New-AzureSqlDatabase` cmdlet.

    [!code-powershell[Main](automate-everything/samples/sample11.ps1?highlight=2,5)]
- 각 데이터베이스에 대해 로컬로 정의 된 함수 tocreates 연결 문자열을 호출합니다. 응용 프로그램 데이터베이스에 액세스 하려면 이러한 연결 문자열을 사용 합니다. 

    [!code-powershell[Main](automate-everything/samples/sample12.ps1?highlight=1-2)]

    Get-SQLAzureDatabaseConnectionString는 연결 문자열에 제공 된 매개 변수 값에서 만든 스크립트에 정의 된 함수입니다.

    [!code-powershell[Main](automate-everything/samples/sample13.ps1?highlight=1)]
- 데이터베이스 서버 이름 및 연결 문자열을 사용 하 여 해시 테이블을 반환합니다.

    [!code-powershell[Main](automate-everything/samples/sample14.ps1)]

Fix It 응용 프로그램에서는 별도 멤버 자격 및 응용 프로그램 데이터베이스를 사용합니다. 단일 데이터베이스에 멤버 자격 및 응용 프로그램 데이터를 삽입할 수 이기도 합니다.

### <a name="store-app-settings-and-connection-strings"></a>앱 설정 및 연결 문자열 저장

설정 및 자동으로 읽으려고 할 때 응용 프로그램에 반환 되는 내용를 재정의 하는 연결 문자열을 저장할 수 있는 기능이 azure 합니다 `appSettings` 또는 `connectionStrings` Web.config 파일의 컬렉션입니다. 적용 하는 대신 이것이 [Web.config 변환](../../../../web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations.md) 배포 하는 경우. 자세한 내용은 [Azure에서 중요 한 데이터를 저장](source-control.md#appsettings) 이 전자책의 뒷부분에 나오는.

환경 생성 스크립트는 모든 Azure에 저장 합니다 `appSettings` 및 `connectionStrings` 응용 프로그램을 Azure에서 실행 될 때 저장소 계정 및 데이터베이스에 액세스 해야 하는 값입니다.

[!code-powershell[Main](automate-everything/samples/sample15.ps1)]

[!code-powershell[Main](automate-everything/samples/sample16.ps1)]

[!code-powershell[Main](automate-everything/samples/sample17.ps1?highlight=2)]

[New Relic](http://newrelic.com/) 는 원격 분석 프레임 워크에서 보여준 합니다 [모니터링 및 원격 분석](monitoring-and-telemetry.md) 장입니다. 환경 생성 스크립트에는 New Relic 설정이 전으로 되도록 웹 앱 다시 시작 합니다.

[!code-powershell[Main](automate-everything/samples/sample18.ps1?highlight=2)]

### <a name="preparing-for-deployment"></a>배포 준비

프로세스의 끝 환경 만들기 스크립트 배포 스크립트에 의해 사용 될 파일을 만드는 두 가지 함수를 호출 합니다.

게시 프로필을 만들고 이러한 함수 중 하나 *(&lt;websitename&gt;.pubxml* 파일). 에 대 한 정보를 저장 및 게시 설정을 가져오려면 Azure REST API를 호출 하는 코드를 *.publishsettings* 파일입니다. 템플릿 파일을 함께 해당 파일에서 정보를 사용 하 여 (*pubxml.template*)를 만드는 합니다 *.pubxml* 게시 프로필을 포함 하는 파일입니다. 이 두 단계로 Visual Studio에서 수행할 작업을 시뮬레이션: 다운로드를 *.publishsettings* 파일과 게시 프로필을 만들려면 가져옵니다.

다른 함수가 다른 템플릿 파일 (웹 사이트-environment.template)를 사용 하 여 만듭니다는 *웹 사이트 environment.xml* 와 함께 배포 스크립트를 사용 하는 설정이 포함 된 파일을 *.pubxml*파일입니다.

### <a name="troubleshooting-and-error-handling"></a>문제 해결 및 오류 처리

프로그램 같은 스크립트는: 실패할 수 있습니다 및 오류와 원인이 무엇에 대 한 수 만큼를 알고 싶은 힘듭니다. 따라서 환경 생성 스크립트의 값을 변경 합니다 `VerbosePreference` 변수를 `SilentlyContinue` 에 `Continue` 모든 세부 정보 표시 메시지 표시 되도록 합니다. 값도 변경 합니다 `ErrorActionPreference` 변수를 `Continue` 에 `Stop`스크립트도 비종료 오류가 발생할 경우 실행이 중지 되도록:

[!code-powershell[Main](automate-everything/samples/sample19.ps1)]

모든 작업을 수행 하기 전에 스크립트가 완료 되 면 경과 된 시간을 계산할 수 있도록 시작 시간을 저장 합니다.

[!code-powershell[Main](automate-everything/samples/sample20.ps1)]

작업이 완료 되 면 스크립트 경과 시간이 표시 됩니다.

[!code-powershell[Main](automate-everything/samples/sample21.ps1)]

및 스크립트의 모든 키 작업에 대 한 자세한 정보 메시지를 예를 들어 쓰기:

[!code-powershell[Main](automate-everything/samples/sample22.ps1)]

## <a name="deployment-script"></a>배포 스크립트

무엇을 *새 AzureWebsiteEnv.ps1* 환경 만들기에 대 한 스크립트는는 *게시 AzureWebsite.ps1* 스크립트는 응용 프로그램 배포에 대 한 합니다.

배포 스크립트에서 웹 앱의 이름을 가져옵니다 합니다 *웹 사이트 environment.xml* 환경 생성 스크립트에서 만든 파일입니다.

[!code-powershell[Main](automate-everything/samples/sample23.ps1)]

배포 사용자 암호를 가져와서 합니다 *.publishsettings* 파일:

[!code-powershell[Main](automate-everything/samples/sample24.ps1)]

실행 합니다 [MSBuild](http://msbuildbook.com/) 빌드 및 프로젝트를 배포 하는 명령:

[!code-powershell[Main](automate-everything/samples/sample25.ps1)]

지정한 경우는 `Launch` 명령줄에서 매개 변수를 호출 합니다 `Show-AzureWebsite` 웹 사이트 URL에 기본 브라우저를 열고 cmdlet.

[!code-powershell[Main](automate-everything/samples/sample26.ps1?highlight=3)]

이 이와 같은 명령을 사용 하 여 배포 스크립트를 실행할 수 있습니다.

`.\Publish-AzureWebsite.ps1 ..\MyFixIt\MyFixIt.csproj -Launch`

열어서 완료 되 면 브라우저의 클라우드에서 실행 하는 사이트를 사용 하 여는 `<websitename>.azurewebsites.net` URL입니다.

![Windows Azure에 배포 된 앱 수정](automate-everything/_static/image7.png)

## <a name="summary"></a>요약

이러한 스크립트를 사용 하 여 동일한 단계를 항상 동일한 옵션을 사용 하 여 동일한 순서로 실행할 수 확신할 수 있습니다. 이렇게 하면는 팀의 각 개발자 하지 사항을 놓치 셨습니까 엉망 항목 또는 다른 팀 멤버의 환경에서 또는 프로덕션 환경에서 동일한 방식으로 작동 하지 않습니다는 자신의 컴퓨터에서 사용자 지정 배포.

유사한 방식으로 REST API, Windows PowerShell 스크립트, API,.NET 언어 또는 Linux 또는 Mac.에서 실행할 수 있는 Bash 유틸리티를 사용 하 여 관리 포털에서 수행할 수 있는 대부분의 Azure 관리 기능을 자동화할 수 있습니다.

에 [다음 장에서](source-control.md) 소스 코드를 확인 하 고 소스 코드 리포지토리에서 스크립트를 포함 하는 중요 한 이유는 설명 드리겠습니다.

## <a name="resources"></a>자료

- [PowerShell 설치 및 구성 Windows Azure에 대 한](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1)합니다. Azure PowerShell cmdlet을 설치 하는 방법 및 필요한 컴퓨터에 Azure를 관리 하기 위해 계정을 인증서를 설치 하는 방법을 설명 합니다. 이 자체 PowerShell 학습을 위한 리소스에 대 한 링크 수도 있기 때문에 시작 하는 것이 적합 합니다.
- [Azure 스크립트 센터](https://docs.microsoft.com/azure/automation/automation-runbook-gallery)합니다. WindowsAzure.com 포털 시작된 자습서, cmdlet 참조 설명서와 소스 코드 및 샘플 스크립트에 대 한 링크를 사용 하 여 Azure 서비스를 관리 하는 스크립트를 개발 하기 위한 리소스
- [주말 Scripter: Azure 및 PowerShell을 사용 하 여 시작](http://blogs.technet.com/b/heyscriptingguy/archive/2013/06/22/weekend-scripter-getting-started-with-windows-azure-and-powershell.aspx)합니다. Windows PowerShell에 전용된 블로그의이 게시물 PowerShell을 사용 하 여 Azure 관리 기능에 대 한 훌륭한 소개를 제공 합니다.
- [Azure 플랫폼 간 명령줄 인터페이스 설치 및 구성](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest)합니다. 시스템을 Windows 뿐만 아니라 Mac 및 Linux에서 작동 하는 Azure 스크립팅 프레임 워크에 대 한 시작 자습서입니다.
- [Azure Sdk 다운로드 및 도구 항목의 명령줄 도구 섹션](https://azure.microsoft.com/downloads/)합니다. 설명서 및 azure 명령줄 도구와 관련 된 다운로드 포털 페이지입니다.
- [Azure 관리 라이브러리 및.NET을 사용 하 여 모든 것 자동화](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx)합니다. Scott hanselman이 Azure에 대 한.NET 관리 API를 소개합니다.
- [Windows PowerShell 스크립트를 사용 하 여 개발 및 테스트 환경에 게시할](https://msdn.microsoft.com/library/azure/dn642480.aspx)합니다. Visual Studio 웹 프로젝트에 대 한 자동으로 생성 하는 스크립트를 게시 하는 MSDN 설명서를 사용 하는 방법을 설명 합니다.
- [Visual Studio 2013 용 PowerShell 도구](https://visualstudiogallery.msdn.microsoft.com/c9eb3ba8-0c59-4944-9a62-6eee37294597)합니다. Visual Studio에서 Windows PowerShell 언어 지원을 추가 하는 visual Studio 확장입니다.

> [!div class="step-by-step"]
> [이전](introduction.md)
> [다음](source-control.md)
