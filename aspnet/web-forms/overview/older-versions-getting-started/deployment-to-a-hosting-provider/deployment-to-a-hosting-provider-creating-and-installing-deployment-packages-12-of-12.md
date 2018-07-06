---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12
title: SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여를 사용 하 여 ASP.NET 웹 응용 프로그램을 배포 합니다. (12는 12) 문제 해결 | Microsoft Docs
author: tdykstra
description: 이 시리즈의 자습서에서는 배포 하는 방법을 보여 줍니다 (게시) ASP.NET 웹 응용 프로그램 프로젝트 Visual Stu를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 중...
ms.author: aspnetcontent
ms.date: 11/17/2011
ms.assetid: 3fc23eed-921d-4d46-a610-a2d156e4bd03
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12
msc.type: authoredcontent
ms.openlocfilehash: d6175d46c6df3c9a4d9bc98492a4458bec45221c
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37811599"
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-troubleshooting-12-of-12"></a>SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여를 사용 하 여 ASP.NET 웹 응용 프로그램을 배포 합니다. (12는 12) 문제 해결
====================
[Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 이 시리즈의 자습서에서는 배포 하는 방법을 보여 줍니다 (게시) ASP.NET 웹용 Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 웹 응용 프로그램 프로젝트입니다. Visual Studio 2010 웹 게시 업데이트를 설치 하는 경우에 사용할 수 있습니다. 계열에 대 한 소개를 참조 하세요 [시리즈의 첫 번째 자습서](deployment-to-a-hosting-provider-introduction-1-of-12.md)합니다.
> 
> Visual Studio 2012 RC 출시 이후 도입 된 배포 기능을 보여 줍니다, 이외의 SQL Server Compact, SQL Server 버전을 배포 하는 방법을 보여 줍니다. 및 Windows Azure 웹 사이트에 배포 하는 방법을 보여 줍니다 하는 자습서를 참조 하세요. [ASP.NET 웹 배포 Visual Studio를 사용 하 여](../../deployment/visual-studio-web-deployment/introduction.md)입니다.


이 페이지에서는 Visual Studio를 사용 하 여 ASP.NET 웹 응용 프로그램을 배포할 때 발생할 수 있는 몇 가지 일반적인 문제를 설명 합니다. 각각에 대 한 가능한 원인과 해당 솔루션은 하나 이상의 제공 됩니다.

## <a name="server-error-in--application---current-custom-error-settings-prevent-details-of-the-error-from-being-viewed-remotely"></a>서버 오류 현재 사용자 지정 오류 설정을 원격으로 볼 수 없도록 오류의 세부 정보를 방지 '/' 응용 프로그램-

### <a name="scenario"></a>시나리오

사이트를 원격 호스트에 배포한 후 Web.config 파일에는 customErrors 설정에 언급 하지만 던 오류의 실제 원인을 나타내지 않습니다 오류 메시지가 표시:

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample1.cmd)]

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

기본적으로 ASP.NET 웹 응용 프로그램이 로컬 컴퓨터에서 실행 되는 경우에 자세한 오류 정보를 표시 합니다. 일반적으로 웹 응용 프로그램 이므로 인터넷을 통해 공개적으로 사용할 수 있는 해커는 취약점을 찾기 위해 응용 프로그램에서이 정보를 사용 하는 일을 할 수 있습니다 하는 경우 자세한 오류 정보를 표시 하지 않으려면입니다. 그러나를 배포 하는 사이트 또는 업데이트 사이트에 따라 잘못 될 수 시간과 실제 오류 메시지를 준비 해야 합니다.

원격 호스트에서 실행 될 때 자세한 오류 메시지를 표시 하도록 응용 프로그램을 사용 하도록 설정 하려면 Web.config 파일을 편집 `customErrors` 모드 해제 응용 프로그램을 다시 배포 하 고 응용 프로그램을 다시 실행 합니다.

1. 응용 프로그램 Web.config 파일에는 `customErrors` 요소에는 `system.web` 요소를 변경 합니다 `mode` 특성을 "off"로 합니다. 그렇지 않으면 추가 `customErrors` 요소에는 `system.web` 요소는 `mode` 다음 예와에서 같이 특성이 "off"로 설정:

    [!code-xml[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample2.xml?highlight=3)]
2. 응용 프로그램을 배포 합니다.
3. 응용 프로그램을 실행 하 고 모든 이전 오류를 발생 시킨 반복 합니다. 이제 실제 오류 메시지의 내용 확인할 수 있습니다.
4. 오류를 해결 하는 경우 원래 복원 `customErrors` 설정 하 고 응용 프로그램을 재배포 합니다.

## <a name="access-is-denied-in-a-web-page-that-uses-sql-server-compact"></a>액세스가 거부 되었습니다. 웹 페이지에서 사용 하 여 SQL Server Compact는

### <a name="scenario"></a>시나리오

SQL Server Compact를 사용 하는 사이트를 배포 하 고 데이터베이스에 액세스 하는 배포 된 사이트의 페이지를 실행 하는 경우 다음 오류 메시지가 표시:

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample3.cmd)]

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

서버에 네트워크 서비스 계정에 있는 SQL 서비스 Compact 네이티브 이진 파일을 읽을 수 있어야 합니다 *bin\amd64* 또는 *bin\x86* 하지만 폴더는 읽기 권한이 해당 폴더에 대 한 합니다. 집합에서 네트워크 서비스에 대 한 권한이 읽기를 *bin* 폴더, 하위 폴더에 사용 권한을 확장할 수 있도록 합니다.

## <a name="cannot-read-configuration-file-due-to-insufficient-permissions"></a>권한이 부족 하 여 구성 파일을 읽을 수 없습니다.

### <a name="scenario"></a>시나리오

클릭 하면 Visual Studio 게시 단추 로컬 컴퓨터에 IIS에 응용 프로그램 배포 실패를 게시 및 **출력** 창 다음과 유사한 오류 메시지를 표시 합니다.

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample4.cmd)]

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

한 번의 클릭을 사용 하려면 로컬 컴퓨터에 IIS에 게시, 관리자 권한으로 Visual Studio 실행 수 있습니다. Visual Studio를 닫고 관리자 권한으로 다시 시작 합니다.

## <a name="could-not-connect-to-the-destination-computer--using-the-specified-process"></a>대상 컴퓨터에 연결 하지 못했습니다... 지정된 된 프로세스를 사용 하 여

### <a name="scenario"></a>시나리오

클릭 하면 Visual Studio 게시 응용 프로그램을 배포 하는 단추 실패를 게시 및 **출력** 창 다음과 유사한 오류 메시지를 표시 합니다.

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample5.cmd)]

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

프록시 서버는 대상 서버와의 통신을 중단 됩니다. Windows 제어판에서 또는 Internet Explorer에서 선택 **인터넷 옵션** 선택 합니다 **연결** 탭 합니다. 에 **인터넷 속성** 대화 상자, 클릭 **LAN 설정**합니다. 에 **Local Area Network (LAN) 설정** 대화 상자, 일반를 **자동으로 설정 검색** 확인란을 선택 합니다. 다시 게시 단추를 클릭 합니다.

문제가 지속 되 면 프록시 또는 방화벽 설정을 사용 하 여 수행할 수 있는 작업을 확인 하려면 시스템 관리자에 게 문의 합니다. 웹 관리 서비스 배포 (8172;)에 대 한 비표준 포트를 사용 하 여 웹 배포 문제 발생 다른 연결에 대 한 웹 배포 포트 80을 사용 합니다. 타사 호스팅 공급자에 배포 하는 경우 일반적으로 웹 관리 서비스를 사용 하는 것입니다.

## <a name="default-net-40-application-pool-does-not-exist"></a>기본.NET 4.0 응용 프로그램 풀이 없습니다.

### <a name="scenario"></a>시나리오

.NET Framework 4가 필요 하는 응용 프로그램을 배포할 때 다음 오류 메시지가 표시:

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample6.cmd)]

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

IIS에서 ASP.NET 4 설치 되지 않았습니다. 에 배포 하는 서버는 개발 컴퓨터에 Visual Studio 2010를 설치 하는 경우 ASP.NET 4 컴퓨터에 설치 되어 있지만 iis에서를 설치할 수 없습니다. 배포 하는 서버에서 관리자 권한 명령 프롬프트를 열고 다음 명령을 실행 하 여 IIS에서 ASP.NET 4를 설치:

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample7.cmd)]

기본 응용 프로그램 풀의.NET Framework 버전을 수동으로 설정 하려면 할 수도 있습니다. 자세한 내용은 참조는 [IIS 테스트 환경으로 배포](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md) 자습서입니다.

## <a name="format-of-the-initialization-string-does-not-conform-to-specification-starting-at-index-0"></a>초기화 문자열 형식의 인덱스 0부터 시작 하는 사양에 맞지 않습니다.

### <a name="scenario"></a>시나리오

한 번의 클릭을 사용 하 여 응용 프로그램을 배포한 후 게시를 받으면 데이터베이스에 액세스 하는 페이지를 실행 하면 다음 오류 메시지:

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample8.cmd)]

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

엽니다는 *Web.config* 배포 된 사이트에 연결 문자열 값으로 시작 하는지 여부를 확인 하는 파일 `$(ReplacableToken_`다음 예제와 같이:

[!code-xml[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample9.xml)]

연결 문자열이 예제와 같이, 프로젝트 파일을 편집 하 고 다음 속성을 추가 합니다 `PropertyGroup` 모든 빌드 구성에 있는 요소:

[!code-xml[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample10.xml)]

그런 다음 응용 프로그램을 재배포 합니다.

## <a name="http-500-internal-server-error"></a>HTTP 500 내부 서버 오류

### <a name="scenario"></a>시나리오

배포 된 사이트를 실행 하면 다음 오류 메시지가 표시 오류의 원인을 나타내는 구체적인 정보 없이:

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample11.cmd)]

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

500 오류는 여러 가지 원인이 있지만 XML 변환 파일 중 하나에 잘못 된 위치에 XML 요소를 추가 하는 오류가 발생 하는 경우 이러한 자습서. 예를 들어, 변환을 삽입 하는 경우이 오류가 발생할 것 있습니다를 `<location>` 요소 아래에 있는 `<system.web>` 대신 바로 아래 `<configuration>`합니다. XML 변환 파일을 수정 하 고 다시 배포 하는 방법은 경우입니다.

## <a name="http-50021-internal-server-error"></a>HTTP 500.21 내부 서버 오류

### <a name="scenario"></a>시나리오

배포 된 사이트를 실행 하면 다음 오류 메시지가 표시:

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample12.cmd)]

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

사이트 대상 ASP.NET 4, 하지만 ASP.NET 4에에서 등록 하지 않은 IIS 서버에 배포 했습니다. 서버에서 관리자 권한 명령 프롬프트를 열고 다음 명령을 실행 하 여 ASP.NET 4를 등록 합니다.

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample13.cmd)]

기본 응용 프로그램 풀의.NET Framework 버전을 수동으로 설정 하려면 할 수도 있습니다. 자세한 내용은 참조는 [IIS 테스트 환경으로 배포](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md) 자습서입니다.

## <a name="login-failed-opening-sql-server-express-database-in-appdata"></a>SQL Server Express 데이터베이스를 여는 앱에서 로그인이 실패 했습니다\_데이터

### <a name="scenario"></a>시나리오

업데이트를 *Web.config* SQL Server Express 데이터베이스를 가리키도록 연결 문자열을 파일을 *.mdf* 파일에 *앱\_데이터* 폴더 및 첫 번째 다음 오류 메시지가 표시 응용 프로그램을 실행 하는 시간:

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample14.cmd)]

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

이름을 합니다 *.mdf* 파일 삭제 한 경우에 컴퓨터에 이전에 있던 모든 SQL Server Express 데이터베이스의 이름을 일치할 수 없습니다. 합니다 *.mdf* 기존 데이터베이스의 파일. 이름을 변경 합니다 *.mdf* 변경 데이터베이스 이름으로 사용 되지 않은 이름으로 파일을 *Web.config* 새 이름을 사용 하는 파일입니다. 사용할 수 있습니다 [SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593) 기존 SQL Server Express를 삭제 하려면 데이터베이스입니다.

## <a name="model-compatibility-cannot-be-checked"></a>검사할 수 없습니다. 모델 호환성

### <a name="scenario"></a>시나리오

업데이트를 *Web.config* 파일을 새 SQL Server Express 데이터베이스를 가리키도록 연결 문자열 및 다음과 같은 오류 메시지가 표시 처음으로 응용 프로그램을 실행 합니다.

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample15.cmd)]

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

전에 컴퓨터에 데이터베이스를 이미 있을 수 있습니다 것에서 일부 테이블을 사용 하 여 Web.config 파일에 배치 하면 데이터베이스 이름을 사용한 적이 되었습니다. 변경 하기 전에 컴퓨터의 사용 되지 않은 새 이름을 선택 합니다 *Web.config* 이 새 데이터베이스 이름을 사용 하 여 가리키도록 파일입니다. 사용할 수 있습니다 [SQL Server Express 유틸리티](https://www.microsoft.com/download/details.aspx?DisplayLang=en&amp;id=3990) 하거나 [SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593) 기존 데이터베이스를 삭제 합니다.

## <a name="sql-error-when-a-script-attempts-to-create-users-or-roles"></a>스크립트를 사용자 또는 역할을 만들려고 시도 하는 동안 SQL 오류가 발생 했습니다

### <a name="scenario"></a>시나리오

에 구성 된 데이터베이스 배포를 사용 하는 합니다 **패키지 및 게시 SQL** 탭을 배포 하는 동안 실행 되는 SQL 스크립트 포함 Create User 또는 Create Role 명령 및 스크립트 실행 실패 하면 해당 명령이 실행 될 때. 자세한 내용을 보려면 다음과 같은 메시지가 표시 될 수 있습니다.

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample16.cmd)]

에 데이터베이스 배포를 구성한 경우이 오류가 발생 합니다 **웹 게시** 마법사 대신 **SQL 패키지 및 게시** 탭에 스레드는 [구성 및 배포](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment) 포럼 및 솔루션 문제 해결이 페이지에 추가 됩니다.

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

배포를 수행 하는 데 사용할 사용자 계정에 사용자 또는 역할을 만들 수 있는 권한이 없습니다. 예를 들어, 호스팅 회사 할당할 수는 `db_datareader`, `db_datawriter`, 및 `db_ddladmin` 를 설정 하는 사용자 계정에는 역할입니다. 이들은 충분 한 대부분의 데이터베이스 개체를 만들기 위한 하지만 사용자 또는 역할을 만들기 위한 없습니다. 오류를 방지 하는 하나의 방법은 데이터베이스 배포에서 사용자 및 역할을 제외 하 여 것입니다. 편집 하 여이 수행할 수 있습니다는 `PreSource` 요소가 데이터베이스의 다음 특성을 포함 하도록에 자동으로 스크립트를 생성 합니다.

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample17.cmd)]

편집 하는 방법에 대 한 자세한 합니다 `PreSource` 프로젝트 파일의 요소를 참조 하세요 [방법: 프로젝트 파일에서 배포 설정 편집](https://msdn.microsoft.com/library/ff398069(v=vs.100).aspx)합니다. 사용자 또는 역할을 개발 데이터베이스에서 대상 데이터베이스에 필요한 경우 지원에 대 한 호스팅 공급자에 게 문의 합니다.

## <a name="sql-server-timeout-error-when-running-custom-scripts-during-deployment"></a>배포 하는 동안 사용자 지정 스크립트를 실행 하는 경우 SQL Server 시간 초과 오류

### <a name="scenario"></a>시나리오

사용자 지정 SQL 스크립트를 배포 하는 동안 실행할 지정 하 고 실행 될 때 웹 배포 하는 시간을 초과 합니다.

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

다른 트랜잭션 모드에 있는 여러 스크립트를 실행 시간 초과 오류가 발생할 수 있습니다. 기본적으로 트랜잭션에서 자동으로 생성 된 스크립트를 실행 하지만 사용자 지정 스크립트에는 않습니다. 선택 하는 경우는 **데이터 및/또는 기존 데이터베이스에서 스키마 가져오기** 옵션을 합니다 **SQL 패키지 및 게시** 탭 사용자 지정 SQL 스크립트를 추가 하는 경우 일부 스크립트의 트랜잭션 설정을 변경 해야 합니다 있도록 모든 스크립트에는 동일한 트랜잭션 설정을 사용 합니다. 자세한 내용은 [방법:를 사용 하 여 웹 프로젝트를 데이터베이스 응용 프로그램을 배포](https://msdn.microsoft.com/library/dd465343.aspx)합니다.

모두 동일한 있도록 트랜잭션 설정을 구성 해도이 오류가 여전히 발생 하는 경우 가능한 해결 방법은 개별적으로 스크립트를 실행 하는 것입니다. 에 **데이터베이스 스크립트** 표에 **패키지/게시** SQL 탭을 선택 취소를 **포함** 확인란 스크립트 시간 제한 오류를 발생 시킨 다음 프로젝트를 게시 합니다. 로 다시 이동 합니다 **데이터베이스 스크립트** 표에서 해당 스크립트의 선택 **포함** 확인란을 선택한의 선택을 취소는 **포함** 다른 스크립트에 대 한 확인란 합니다. 그런 다음 프로젝트를 다시 게시 합니다. 이 이번에 게시 하는 경우, 선택한 사용자 지정 스크립트를 실행 합니다.

## <a name="stream-data-of-site-manifest-is-not-yet-available"></a>사이트 매니페스트의 Stream 데이터를 아직 사용할 수 없습니다.

### <a name="scenario"></a>시나리오

설치 하는 경우 사용 하 여 패키지를 *deploy.cmd* 사용 하 여 파일을 `t` (테스트) 옵션을 다음 오류 메시지가 표시:

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample18.cmd)]

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

오류 메시지 명령을 테스트 보고서를 생성할 수 없는 것을 의미 합니다. 그러나 명령을 사용 하는 경우 실행 될 수 있습니다는 `y` (실제 설치) 옵션입니다. 메시지는 테스트 모드에서 명령을 실행 하는 문제가 있는 것만 나타냅니다.

## <a name="this-application-requires-managedruntimeversion-v40"></a>이 응용 프로그램 필요 ManagedRuntimeVersion v4.0

### <a name="scenario"></a>시나리오

배포 하려는 경우 다음 오류 메시지가 표시:

 오류:의 스트림 데이터를 ' sitemanifest/dbFullSql [@path= 'C:\TEMP\AdventureWorksGrant.sql']/sqlScript'를 사용할 수 없습니다. 사용 하려는 응용 프로그램 풀 'managedRuntimeVersion' 속성이 ('v2.0'로 설정 되어 있습니다. 이 응용 프로그램 'v4.0' 필요합니다. 

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

IIS에서 ASP.NET 4 설치 되지 않았습니다. 에 배포 하는 서버는 개발 컴퓨터에 Visual Studio 2010를 설치 하는 경우 ASP.NET 4 컴퓨터에 설치 되어 있지만 iis에서를 설치할 수 없습니다. 배포 하는 서버에서 관리자 권한 명령 프롬프트를 열고 다음 명령을 실행 하 여 IIS에서 ASP.NET 4를 설치:

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample19.cmd)]

## <a name="unable-to-cast-microsoftwebdeploymentdeploymentprovideroptions"></a>Microsoft.Web.Deployment.DeploymentProviderOptions 캐스팅할 수 없습니다.

### <a name="scenario"></a>시나리오

패키지를 배포 하는 경우 다음 오류 메시지가 표시:

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample20.cmd)]

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

웹 배포 2.0이 설치 되어 있는 서버에 웹 배포 1.1 UI를 사용 하 여 IIS 관리자에서 배포 하려고 합니다. 가져오기 패키지를 확인 하 여 배포 하는 IIS 원격 관리 도구를 사용 하는 경우는 **기능은 사용할 수 있는 새** 연결을 설정 하는 경우 대화 상자. (이 대화 상자만 표시 될 수 있습니다 한 번 연결이 먼저 설정 됩니다. 연결의 선택을 취소 하 고 다시 시작, IIS 관리자를 닫습니다를 입력 하 여 다시 시작 `inetmgr /reset` 명령 프롬프트에서.) 나열 된 기능 중 하나 인지 **웹 배포 UI**을 8 보다 낮은 버전 번호가 있기를 배포 하는 서버 1.1 및 2.0 버전의 웹 배포 설치 되어 있을 수 있습니다. 2.0이 설치 되어 있는 클라이언트를 배포 하려면 서버에만 웹 배포 2.0이 설치 되어 있어야 합니다. 이 문제를 해결 하려면 호스팅 공급자에 게 문의 해야 합니다.

## <a name="unable-to-load-the-native-components-of-sql-server-compact"></a>SQL Server Compact의 네이티브 구성 요소를 로드할 수 없습니다.

### <a name="scenario"></a>시나리오

배포 된 사이트를 실행 하면 다음 오류 메시지가 표시:

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample21.cmd)]

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

배포 된 사이트에 없는 *amd64* 하 고 *x86* 하위 폴더는 응용 프로그램에 네이티브 어셈블리를 사용 하 여 *bin* 폴더입니다. SQL Server Compact 설치 된 컴퓨터에서 네이티브 어셈블리에 위치한 *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private*합니다. Visual Studio 프로젝트에 올바른 폴더에 올바른 파일을 얻을 수 있는 최상의 방법은 NuGet SqlServerCompact 패키지를 설치 하는 것입니다. 네이티브 어셈블리를 복사 하는 빌드 후 스크립트를 추가 하는 패키지 설치 *amd64* 하 고 *x86*합니다. 그러나 배포에 대 한 순서로 프로젝트에 수동으로 포함 해야 합니다. 자세한 내용은 참조는 [SQL Server Compact 배포](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md) 자습서입니다.

## <a name="path-is-not-valid-error-after-deploying-an-entity-framework-code-first-application"></a>Entity Framework Code First 응용 프로그램을 배포한 후 "경로가 잘못 되었습니다." 오류

### <a name="scenario"></a>시나리오

SQL Server Compact 데이터베이스를 앱의 파일에 저장 하는 같은 Entity Framework Code First 마이그레이션 및 DBMS를 사용 하는 응용 프로그램을 배포한\_데이터 폴더. Code First 마이그레이션 후 첫 번째 배포 데이터베이스를 만들도록 구성 해야 합니다. 응용 프로그램을 실행 하는 경우 다음 예제와 같이 오류 메시지를 가져옵니다.

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample22.cmd)]

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

먼저 코드 데이터베이스 하지만 앱을 만들려고 시도\_데이터 폴더가 존재 하지 않습니다. 에 모든 파일을 저장 하지 않은 하거나 합니다 *앱\_데이터* 를 배포 하면 또는 선택한 폴더 **제외 앱\_데이터** 에 **웹패키지및게시** 탭의 **프로젝트 속성** 창입니다. 서버에 복사할 폴더에 파일이 없을 경우 배포 프로세스 서버에서 폴더를 만듭니다 없습니다. 사이트에서 설정한 데이터베이스를 이미 설치한 경우 배포 프로세스는 파일을 삭제 하며 *앱\_데이터* 폴더를 선택한 경우 자체 **대상에서 추가 파일 제거** 에서 게시 프로필입니다. .txt 파일과 같은 문제를 해결 하기 위해 자리 표시자 파일을 저장 합니다 *앱\_데이터* 폴더 필요가 있는지 **제외 앱\_데이터** 선택 하 고 다시 배포 합니다. 

## <a name="com-object-that-has-been-separated-from-its-underlying-rcw-cannot-be-used"></a>"기본 RCW에서 분리 된 COM 개체를 사용할 수 없습니다."

### <a name="scenario"></a>시나리오

성공적으로 되었습니다 한 번의 클릭을 사용 하 여 응용 프로그램 배포를 게시 하 고이 오류를 가져오기 시작 합니다.

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample23.cmd)]

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

닫고 Visual Studio를 다시 시작은 일반적으로이 오류를 해결 하는 데 필요한 모든 합니다.

## <a name="deployment-fails-because-user-credentials-used-for-publishing-dont-have-setacl-authority"></a>배포 실패 하기 때문에 사용자 자격 증명에 사용할 게시 없는 setACL 기관

### <a name="scenario"></a>시나리오

게시 실패 수를 나타내는 오류가 있는 기관 (사용 중인 사용자 계정 없는 setACL 기관) 폴더 사용 권한을 설정할 필요가 없습니다.

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

기본적으로 Visual Studio 설정 사이트의 루트 폴더에 읽기 권한 및 앱에 대 한 쓰기 권한이\_데이터 폴더. 추가 하 여이 동작을 해제 하는 사이트 폴더에 대 한 기본 권한을 올바른지, 그리고 설정할 필요가 없습니다를 알면 **&lt;IncludeSetACLProviderOn 대상&gt;False&lt;/ IncludeSetACLProviderOnDestination&gt;** (모든 프로필 적용할).wpp.targets 파일 또는 게시 프로필 파일 (단일 프로필을 적용할). 이러한 파일을 편집 하는 방법에 대 한 정보를 참조 하세요 [방법: 프로필 (.pubxml) 파일에서 배포 설정을 편집](https://msdn.microsoft.com/library/ff398069.aspx)합니다. 

## <a name="access-denied-errors-when-the-application-tries-to-write-to-an-application-folder"></a>응용 프로그램을 응용 프로그램 폴더에 기록 하려고 할 때 액세스 거부 오류

### <a name="scenario"></a>시나리오

해당 폴더에 대 한 쓰기 기관에 없기 때문에 응용 프로그램 폴더 중 하나에 파일 만들기 또는 편집 하려고 할 때 응용 프로그램 오류입니다.

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

기본적으로 Visual Studio 설정 사이트의 루트 폴더에 읽기 권한 및 앱에 대 한 쓰기 권한이\_데이터 폴더. 응용 프로그램에 필요한 하위 폴더에 대 한 쓰기 액세스 하는 경우에 표시 된 대로 해당 폴더에 대 한 권한을 설정할 수 있습니다는 [폴더 사용 권한 설정](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12.md) 하 고 [프로덕션 환경에 배포](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) 자습서입니다. 응용 프로그램 사이트의 루트 폴더에 대 한 쓰기 액세스에 필요한 경우 추가 하 여 루트 폴더에 읽기 전용 액세스를 설정 하지 못하도록 **&lt;IncludeSetACLProviderOn 대상&gt;False&lt;/ IncludeSetACLProviderOnDestination&gt;** (모든 프로필 적용할).wpp.targets 파일 또는 게시 프로필 파일 (단일 프로필을 적용할). 이러한 파일을 편집 하는 방법에 대 한 정보를 참조 하세요 [방법: 프로필 (.pubxml) 파일에서 배포 설정을 편집](https://msdn.microsoft.com/library/ff398069.aspx)합니다. <a id="aspnet45error"></a>

## <a name="configuration-error---targetframework-attribute-references-a-version-that-is-later-than-the-installed-version-of-the-net-framework"></a>구성 오류-targetFramework 특성 참조의.NET Framework 설치 된 버전 보다 최신 버전

### <a name="scenario"></a>시나리오

ASP.NET 4.5를 대상으로 하는 웹 프로젝트를 성공적으로 게시 되지만 응용 프로그램을 실행 하는 경우 (사용 하 여는 `customErrors` 모드는 Web.config 파일에서 "off"로 설정) 다음 오류가 발생 하면:

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample24.cmd)]

오류 페이지의 소스 오류 상자 오류의 원인으로 Web.config에서 다음 줄을 강조 표시합니다.

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample25.cmd)]

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

서버에서 ASP.NET 4.5를 지원 하지 않습니다. 시기 및 ASP.NET 4.5에 대 한 지원을 추가할 수 있는지를 확인 하려면 호스팅 공급자에 게 문의 합니다. ASP.NET 4 또는 이전 버전을 대상으로 하는 웹 프로젝트를 배포 해야 하는 서버를 업그레이드 하는 옵션이 아닌 경우 대신 합니다. 동일한 대상에는 ASP.NET 4 또는 이전 웹 프로젝트를 배포 하는 경우 선택 합니다 **대상에서 추가 파일 제거** 확인란 합니다 **설정** 탭은 **웹 게시**마법사. 선택 하지 않으면 **대상에서 추가 파일 제거**에 구성 오류 페이지를 계속 합니다.

프로젝트 **속성** windows에는 대상 프레임 워크 드롭다운 목록에 포함 되어 있지만 변경 하 여이 문제를 해결할 수 없는 **.NET Framework 4.5** 에 **.NETFramework4**. 이전 프레임 워크 버전으로 대상 프레임 워크를 변경 하면 프로젝트는 최신 프레임 워크 버전의 어셈블리에 대 한 참조 및 여전히 실행 되지 않습니다. 해야 수동으로 해당 참조를 변경 하거나.NET Framework 4 또는 이전 버전을 대상으로 하는 새 프로젝트를 만듭니다. 자세한 내용은 [웹 사이트에 대 한.NET Framework 타기](https://msdn.microsoft.com/library/bb398791(v=vs.100).aspx)합니다.

> [!div class="step-by-step"]
> [이전](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12.md)
