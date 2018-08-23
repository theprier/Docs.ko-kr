---
uid: web-forms/overview/deployment/visual-studio-web-deployment/troubleshooting
title: 'Visual Studio를 사용 하 여 ASP.NET 웹 배포: 문제 해결 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시)에서 실행 중인 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자...
ms.author: riande
ms.date: 06/01/2015
ms.assetid: c0090595-ab3b-4b9b-9e16-7a1891e8cb2f
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: 65cd5cd9f7d1f9c5fdaea9b0d16bdfd84259efdd
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41838869"
---
<a name="aspnet-web-deployment-using-visual-studio-troubleshooting"></a>Visual Studio를 사용 하 여 ASP.NET 웹 배포: 문제 해결
====================
[Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> 이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시) Visual Studio 2012 또는 Visual Studio 2010을 사용 하 여 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자입니다. 시리즈에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](introduction.md)합니다.


이 페이지에서는 Visual Studio를 사용 하 여 ASP.NET 웹 응용 프로그램을 배포할 때 발생할 수 있는 몇 가지 일반적인 문제를 설명 합니다. 각각에 대 한 가능한 원인과 해당 솔루션은 하나 이상의 제공 됩니다.

표시 된 시나리오는 Azure와 타사 호스팅 공급자에 적용 됩니다. Azure App Service에서 웹 앱 문제를 해결 하는 방법에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [Visual Studio를 사용하여 Azure App Service의 웹앱 문제 해결](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)
- [Azure App Service에서 Web Apps 모니터링](https://azure.microsoft.com/documentation/articles/web-sites-monitor//)
- [.NET 용 Windows Azure SDK 2.0의 출시를 발표](http://https://weblogs.asp.net/scottgu/announcing-the-release-of-windows-azure-sdk-2-0-for-net) (ScottGu의 블로그는 Visual Studio에서 진단 로그를 가져오는 방법을 표시 하는 데 사용)

## <a name="server-error-in--application---current-custom-error-settings-prevent-details-of-the-error-from-being-viewed-remotely"></a>서버 오류 현재 사용자 지정 오류 설정을 원격으로 볼 수 없도록 오류의 세부 정보를 방지 '/' 응용 프로그램-

### <a name="scenario"></a>시나리오

사이트를 원격 호스트에 배포한 후 Web.config 파일에는 customErrors 설정에 언급 하지만 던 오류의 실제 원인을 나타내지 않습니다 오류 메시지가 표시:

[!code-xml[Main](troubleshooting/samples/sample1.xml)]

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

기본적으로 ASP.NET 웹 응용 프로그램이 로컬 컴퓨터에서 실행 되는 경우에 자세한 오류 정보를 표시 합니다. 일반적으로 웹 응용 프로그램 이므로 인터넷을 통해 공개적으로 사용할 수 있는 해커는 취약점을 찾기 위해 응용 프로그램에서이 정보를 사용 하는 일을 할 수 있습니다 하는 경우 자세한 오류 정보를 표시 하지 않으려면입니다. 그러나를 배포 하는 사이트 또는 업데이트 사이트에 따라 잘못 될 수 시간과 실제 오류 메시지를 준비 해야 합니다.

원격 호스트에서 실행 될 때 자세한 오류 메시지를 표시 하도록 응용 프로그램을 사용 하려면, customErrors 모드를 해제 하 고, 응용 프로그램을 다시 배포 하 고, 응용 프로그램을 다시 실행 하려면 Web.config 파일을 편집 합니다.

1. 응용 프로그램 Web.config 파일에 acustomErrors 요소 thesystem.web 요소의 경우 themode 특성을 "off"로 변경 합니다. 그렇지 않으면 요소를 추가 acustomErrors thesystem.web 요소 themode 특성을 "off"로 설정 하 여 다음 예와에서 같이: 

    [!code-xml[Main](troubleshooting/samples/sample2.xml)]
2. 응용 프로그램을 배포 합니다.
3. 응용 프로그램을 실행 하 고 모든 이전 오류를 발생 시킨 반복 합니다. 이제 실제 오류 메시지의 내용 확인할 수 있습니다.
4. 오류를 해결 하는 경우 원래 customErrors 설정을 복원 하 고 응용 프로그램을 재배포 합니다.

## <a name="cannot-createshadow-copy-contosouniversity-when-that-file-already-exists"></a>없습니다 만들어 섀도 복사본 'ContosoUniversity' 파일이 이미 있는 경우.

### <a name="scenario"></a>시나리오

Visual Studio에서 프로젝트를 실행 하려고 할 때 다음과 비슷한 메시지와 함께 오류 페이지를 가져옵니다.

'/' 응용 프로그램에 서버 오류가 발생 했습니다. 없습니다 만들어 섀도 복사본 'ContosoUniversity' 파일이 이미 있는 경우.

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

잠깐 브라우저 새로 고침 또는 사이트를 다시 컴파일할 및 다시 실행 해 보십시오.

## <a name="access-is-denied-in-a-web-page-that-uses-sql-server-compact"></a>액세스가 거부 되었습니다. 웹 페이지에서 사용 하 여 SQL Server Compact는

### <a name="scenario"></a>시나리오

SQL Server Compact를 사용 하는 사이트를 배포 하 고 데이터베이스에 액세스 하는 배포 된 사이트의 페이지를 실행 하는 경우 다음 오류 메시지가 표시:

액세스가 거부되었습니다. (HRESULT의 예외: 0x80070005 (E\_ACCESSDENIED))

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

서버에 네트워크 서비스 계정에 있는 SQL 서비스 Compact 네이티브 이진 파일을 읽을 수 있어야 합니다 *bin\amd64* 또는 *bin\x86* 하지만 폴더는 읽기 권한이 해당 폴더에 대 한 합니다. 집합에서 네트워크 서비스에 대 한 권한이 읽기를 *bin* 폴더, 하위 폴더에 사용 권한을 확장할 수 있도록 합니다.

## <a name="cannot-read-configuration-file-due-to-insufficient-permissions"></a>권한이 부족 하 여 구성 파일을 읽을 수 없습니다.

### <a name="scenario"></a>시나리오

클릭 하면 Visual Studio 게시 단추 로컬 컴퓨터에 IIS에 응용 프로그램 배포 실패를 게시 및 **출력** 창 다음과 유사한 오류 메시지를 표시 합니다.

' MACHINE/리디렉션 ' IIS 구성 파일을 읽는 오류가 발생 했습니다. 이 작업을 수행 하는 id가 하는 중... 오류: 권한이 부족 하 여 구성 파일을 읽을 수 없습니다.

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

한 번의 클릭을 사용 하려면 로컬 컴퓨터에 IIS에 게시, 관리자 권한으로 Visual Studio 실행 수 있습니다. Visual Studio를 닫고 관리자 권한으로 다시 시작 합니다.

## <a name="could-not-connect-to-the-destination-computer--using-the-specified-process"></a>대상 컴퓨터에 연결 하지 못했습니다... 지정된 된 프로세스를 사용 하 여

### <a name="scenario"></a>시나리오

클릭 하면 Visual Studio 게시 응용 프로그램을 배포 하는 단추 실패를 게시 및 **출력** 창 다음과 유사한 오류 메시지를 표시 합니다.

[!code-console[Main](troubleshooting/samples/sample3.cmd)]

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

프록시 서버는 대상 서버와의 통신을 중단 됩니다. Windows 제어판에서 또는 Internet Explorer에서 선택 **인터넷 옵션** 선택 합니다 **연결** 탭 합니다. 에 **인터넷 속성** 대화 상자, 클릭 **LAN 설정**합니다. 에 **Local Area Network (LAN) 설정** 대화 상자, 일반를 **자동으로 설정 검색** 확인란을 선택 합니다. 다시 게시 단추를 클릭 합니다.

문제가 지속 되 면 프록시 또는 방화벽 설정을 사용 하 여 수행할 수 있는 작업을 확인 하려면 시스템 관리자에 게 문의 합니다. 웹 관리 서비스 배포 (8172;)에 대 한 비표준 포트를 사용 하 여 웹 배포 문제 발생 다른 연결에 대 한 웹 배포 포트 80을 사용 합니다. 타사 호스팅 공급자에 배포 하는 경우 일반적으로 웹 관리 서비스를 사용 하는 것입니다.

## <a name="default-net-40-application-pool-does-not-exist"></a>기본.NET 4.0 응용 프로그램 풀이 없습니다.

### <a name="scenario"></a>시나리오

.NET Framework 4가 필요 하는 응용 프로그램을 배포할 때 다음 오류 메시지가 표시:

기본.NET 4.0 응용 프로그램 풀이 존재 하지 않거나 응용 프로그램을 추가할 수 없습니다. ASP.NET 4.0이이 컴퓨터에 설치 되어 있는지 확인 하십시오.

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

IIS에서 ASP.NET 4 설치 되지 않았습니다. 에 배포 하는 서버는 개발 컴퓨터에 Visual Studio 2010를 설치 하는 경우 ASP.NET 4 컴퓨터에 설치 되어 있지만 iis에서를 설치할 수 없습니다. 배포 하는 서버에서 관리자 권한 명령 프롬프트를 열고 다음 명령을 실행 하 여 IIS에서 ASP.NET 4를 설치:

[!code-console[Main](troubleshooting/samples/sample4.cmd)]

기본 응용 프로그램 풀의.NET Framework 버전을 수동으로 설정 하려면 할 수도 있습니다. 자세한 내용은이 시리즈의 자습서 테스트 환경으로 IIS에 배포를 참조 하세요.

## <a name="format-of-the-initialization-string-does-not-conform-to-specification-starting-at-index-0"></a>초기화 문자열 형식의 인덱스 0부터 시작 하는 사양에 맞지 않습니다.

### <a name="scenario"></a>시나리오

한 번의 클릭을 사용 하 여 응용 프로그램을 배포한 후 게시를 받으면 데이터베이스에 액세스 하는 페이지를 실행 하면 다음 오류 메시지:

초기화 문자열 형식의 인덱스 0부터 시작 하는 사양에 맞지 않습니다.

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

엽니다는 *Web.config* 배포 된 사이트에 연결 문자열 값을 $로 시작 하는지 여부를 확인 하는 파일 (ReplacableToken\_, 다음 예제 에서처럼에서:

[!code-xml[Main](troubleshooting/samples/sample5.xml)]

연결 문자열이 예제와 같이, 프로젝트 파일을 편집 하 고 모든 빌드 구성 되는 PropertyGroup 요소에 다음 속성을 추가 합니다.

[!code-xml[Main](troubleshooting/samples/sample6.xml)]

그런 다음 응용 프로그램을 재배포 합니다.

## <a name="http-500-internal-server-error"></a>HTTP 500 내부 서버 오류

### <a name="scenario"></a>시나리오

배포 된 사이트를 실행 하면 다음 오류 메시지가 표시 오류의 원인을 나타내는 구체적인 정보 없이:

HTTP 오류 500-내부 서버 오류입니다.

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

500 오류는 여러 가지 원인이 있지만 Web.config 변환 파일 중 하나에 잘못 된 위치에 XML 요소를 추가 하는 오류가 발생 하는 경우 이러한 자습서. 예를 들어, 변환을 삽입 하는 경우이 오류가 발생할 것 있습니다를 &lt;위치&gt; 요소 아래에 있는 &lt;system.web&gt; 대신 바로 아래 &lt;구성&gt;합니다. 변환이 의도 한 대로 작동 하는지 확인 하려면 Web.config 변환 미리 보기 기능을 사용할 수 있습니다. 올바르게 코딩 하는 변환의 찾을 경우 솔루션 변환 파일을 수정 하 고 다시 배포 하는 것입니다. 확실 한 오류가 없으면 변환 주석으로 처리 해 500 오류를 일으키는지 어느를 다시 배포 합니다.

## <a name="http-50021-internal-server-error"></a>HTTP 500.21 내부 서버 오류

### <a name="scenario"></a>시나리오

배포 된 사이트를 실행 하면 다음 오류 메시지가 표시:

HTTP 오류 500.21-내부 서버 오류입니다. "PageHandlerFactory 통합" 처리기에 해당 모듈 목록에 잘못 된 모듈 "ManagedPipelineHandler"입니다.

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

사이트 대상 ASP.NET 4, 하지만 ASP.NET 4에에서 등록 하지 않은 IIS 서버에 배포 했습니다. 서버에서 관리자 권한 명령 프롬프트를 열고 다음 명령을 실행 하 여 ASP.NET 4를 등록 합니다.

[!code-console[Main](troubleshooting/samples/sample7.cmd)]

기본 응용 프로그램 풀의.NET Framework 버전을 수동으로 설정 하려면 할 수도 있습니다. 자세한 내용은이 시리즈의 자습서 테스트 환경으로 IIS에 배포를 참조 하세요.

## <a name="login-failed-opening-sql-server-express-database-in-appdata"></a>SQL Server Express 데이터베이스를 여는 앱에서 로그인이 실패 했습니다\_데이터

### <a name="scenario"></a>시나리오

업데이트를 *Web.config* SQL Server Express 데이터베이스를 가리키도록 연결 문자열을 파일을 *.mdf* 파일에 *앱\_데이터* 폴더 및 첫 번째 다음 오류 메시지가 표시 응용 프로그램을 실행 하는 시간:

System.Data.SqlClient.SqlException: "DatabaseName" 로그인에서 요청한 데이터베이스를 열 수 없습니다. 로그인에 실패했습니다.

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

이름을 합니다 *.mdf* 파일 삭제 한 경우에 컴퓨터에 이전에 있던 모든 SQL Server Express 데이터베이스의 이름을 일치할 수 없습니다. 합니다 *.mdf* 기존 데이터베이스의 파일. 이름을 변경 합니다 *.mdf* 변경 데이터베이스 이름으로 사용 되지 않은 이름으로 파일을 *Web.config* 새 이름을 사용 하는 파일입니다. 사용할 수 있습니다 [SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593) 기존 SQL Server Express를 삭제 하려면 데이터베이스입니다.

## <a name="model-compatibility-cannot-be-checked"></a>검사할 수 없습니다. 모델 호환성

### <a name="scenario"></a>시나리오

업데이트를 *Web.config* 파일을 새 SQL Server Express 데이터베이스를 가리키도록 연결 문자열 및 다음과 같은 오류 메시지가 표시 처음으로 응용 프로그램을 실행 합니다.

데이터베이스는 모델 메타 데이터를 포함 하지 않으므로 모델 호환성을 확인할 수 없습니다. IncludeMetadataConvention DbModelBuilder 규칙에 추가 되어 있는지 확인 합니다.

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

전에 컴퓨터에 데이터베이스를 이미 있을 수 있습니다 것에서 일부 테이블을 사용 하 여 Web.config 파일에 배치 하면 데이터베이스 이름을 사용한 적이 되었습니다. 변경 하기 전에 컴퓨터의 사용 되지 않은 새 이름을 선택 합니다 *Web.config* 이 새 데이터베이스 이름을 사용 하 여 가리키도록 파일입니다. 사용할 수 있습니다 [SQL Server Express 유틸리티](https://www.microsoft.com/download/details.aspx?DisplayLang=en&amp;id=3990) 하거나 [SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593) 기존 데이터베이스를 삭제 합니다.

## <a name="sql-error-when-a-script-attempts-to-create-users-or-roles"></a>스크립트를 사용자 또는 역할을 만들려고 시도 하는 동안 SQL 오류가 발생 했습니다

### <a name="scenario"></a>시나리오

에 구성 된 데이터베이스 배포를 사용 하는 합니다 **패키지 및 게시 SQL** 탭을 배포 하는 동안 실행 되는 SQL 스크립트 포함 Create User 또는 Create Role 명령 및 스크립트 실행 실패 하면 해당 명령이 실행 될 때. 자세한 내용을 보려면 다음과 같은 메시지가 표시 될 수 있습니다.

[!code-console[Main](troubleshooting/samples/sample8.cmd)]

에 데이터베이스 배포를 구성한 경우이 오류가 발생 합니다 **웹 게시** 마법사 대신 **SQL 패키지 및 게시** 탭에 스레드는 [구성 및 배포](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment) 포럼 및 솔루션 문제 해결이 페이지에 추가 됩니다.

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

배포를 수행 하는 데 사용할 사용자 계정에 사용자 또는 역할을 만들 수 있는 권한이 없습니다. 호스팅 업체에서 db를 할당할 수는 예를 들어\_datareader를 db\_datawriter 여부, 및 db\_를 설정 하는 사용자 계정에 ddladmin 역할입니다. 이들은 충분 한 대부분의 데이터베이스 개체를 만들기 위한 하지만 사용자 또는 역할을 만들기 위한 없습니다. 오류를 방지 하는 하나의 방법은 데이터베이스 배포에서 사용자 및 역할을 제외 하 여 것입니다. 다음 특성을 포함 하도록 데이터베이스의 자동으로 생성 된 스크립트에 대 한 PreSource 요소를 편집 하 여이 수행할 수 있습니다.

[!code-console[Main](troubleshooting/samples/sample9.cmd)]

프로젝트 파일에서 PreSource 요소를 편집 하는 방법에 대 한 정보를 참조 하세요 [방법: 프로젝트 파일에서 배포 설정 편집](https://msdn.microsoft.com/library/ff398069(v=vs.100).aspx)합니다. 사용자 또는 역할을 개발 데이터베이스에서 대상 데이터베이스에 필요한 경우 지원에 대 한 호스팅 공급자에 게 문의 합니다.

## <a name="sql-server-timeout-error-when-running-custom-scripts-during-deployment"></a>배포 하는 동안 사용자 지정 스크립트를 실행 하는 경우 SQL Server 시간 초과 오류

### <a name="scenario"></a>시나리오

사용자 지정 SQL 스크립트를 배포 하는 동안 실행할 지정 하 고 실행 될 때 웹 배포 하는 시간을 초과 합니다.

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

다른 트랜잭션 모드에 있는 여러 스크립트를 실행 시간 초과 오류가 발생할 수 있습니다. 기본적으로 트랜잭션에서 자동으로 생성 된 스크립트를 실행 하지만 사용자 지정 스크립트에는 않습니다. 선택 하는 경우는 **데이터 및/또는 기존 데이터베이스에서 스키마 가져오기** 옵션을 합니다 **SQL 패키지 및 게시** 탭 사용자 지정 SQL 스크립트를 추가 하는 경우 일부 스크립트의 트랜잭션 설정을 변경 해야 합니다 있도록 모든 스크립트에는 동일한 트랜잭션 설정을 사용 합니다. 자세한 내용은 [방법:를 사용 하 여 웹 프로젝트를 데이터베이스 응용 프로그램을 배포](https://msdn.microsoft.com/library/dd465343.aspx)합니다.

모두 동일한 있도록 트랜잭션 설정을 구성 해도이 오류가 여전히 발생 하는 경우 가능한 해결 방법은 개별적으로 스크립트를 실행 하는 것입니다. 에 **데이터베이스 스크립트** 표에 **패키지/게시** SQL 탭을 선택 취소를 **포함** 확인란 스크립트 시간 제한 오류를 발생 시킨 다음 프로젝트를 게시 합니다. 로 다시 이동 합니다 **데이터베이스 스크립트** 표에서 해당 스크립트의 선택 **포함** 확인란을 선택한의 선택을 취소는 **포함** 다른 스크립트에 대 한 확인란 합니다. 그런 다음 프로젝트를 다시 게시 합니다. 이 이번에 게시 하는 경우, 선택한 사용자 지정 스크립트를 실행 합니다.

## <a name="stream-data-of-site-manifest-is-not-yet-available"></a>사이트 매니페스트의 Stream 데이터를 아직 사용할 수 없습니다.

### <a name="scenario"></a>시나리오

설치 하는 경우 사용 하 여 패키지를 *deploy.cmd* 파일 t (테스트) 옵션을 사용 하 여 다음과 같은 오류 메시지가 표시:

오류:의 스트림 데이터를 ' sitemanifest/dbFullSql [@path= 'C:\TEMP\AdventureWorksGrant.sql']/sqlScript'를 사용할 수 없습니다.

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

오류 메시지 명령을 테스트 보고서를 생성할 수 없는 것을 의미 합니다. 그러나 y (실제 설치) 옵션을 사용 하는 경우 명령이 실행 될 수 있습니다. 메시지는 테스트 모드에서 명령을 실행 하는 문제가 있는 것만 나타냅니다.

## <a name="this-application-requires-managedruntimeversion-v40"></a>이 응용 프로그램 필요 ManagedRuntimeVersion v4.0

### <a name="scenario"></a>시나리오

배포 하려는 경우 다음 오류 메시지가 표시:

사용 하려는 응용 프로그램 풀 'managedRuntimeVersion' 속성이 ('v2.0'로 설정 되어 있습니다. 이 응용 프로그램 'v4.0' 필요합니다.

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

IIS에서 ASP.NET 4 설치 되지 않았습니다. 에 배포 하는 서버는 개발 컴퓨터에 Visual Studio 2010를 설치 하는 경우 ASP.NET 4 컴퓨터에 설치 되어 있지만 iis에서를 설치할 수 없습니다. 배포 하는 서버에서 관리자 권한 명령 프롬프트를 열고 다음 명령을 실행 하 여 IIS에서 ASP.NET 4를 설치:

[!code-console[Main](troubleshooting/samples/sample10.cmd)]

## <a name="unable-to-cast-microsoftwebdeploymentdeploymentprovideroptions"></a>Microsoft.Web.Deployment.DeploymentProviderOptions 캐스팅할 수 없습니다.

### <a name="scenario"></a>시나리오

패키지를 배포 하는 경우 다음 오류 메시지가 표시:

'Microsoft.Web.Deployment.DeploymentProviderOptions'를 ' Microsoft.Web.Deployment.DeploymentProviderOptions' 형식의 개체를 캐스팅할 수 없습니다.

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

웹 배포 2.0이 설치 되어 있는 서버에 웹 배포 1.1 UI를 사용 하 여 IIS 관리자에서 배포 하려고 합니다. 가져오기 패키지를 확인 하 여 배포 하는 IIS 원격 관리 도구를 사용 하는 경우는 **기능은 사용할 수 있는 새** 연결을 설정 하는 경우 대화 상자. (이 대화 상자만 표시 될 수 있습니다 한 번 연결이 먼저 설정 됩니다. 연결의 선택을 취소 하 고 다시 시작, IIS 관리자를 닫습니다 및 inetmgr을 입력 하 여 다시 시작 간 명령 프롬프트에서 다시 설정 합니다.) 나열 된 기능 중 하나 인지 **웹 배포 UI**을 8 보다 낮은 버전 번호가 있기를 배포 하는 서버 1.1 및 2.0 버전의 웹 배포 설치 되어 있을 수 있습니다. 2.0이 설치 되어 있는 클라이언트를 배포 하려면 서버에만 웹 배포 2.0이 설치 되어 있어야 합니다. 이 문제를 해결 하려면 호스팅 공급자에 게 문의 해야 합니다.

## <a name="unable-to-load-the-native-components-of-sql-server-compact"></a>SQL Server Compact의 네이티브 구성 요소를 로드할 수 없습니다.

### <a name="scenario"></a>시나리오

배포 된 사이트를 실행 하면 다음 오류 메시지가 표시:

SQL Server compact 버전 8482 ADO.NET 공급자에 게 해당 네이티브 구성 요소를 로드할 수 없습니다. 올바른 버전의 SQL Server Compact를 설치 합니다. 자세한 내용은 기술 자료 문서 974247 참조 하십시오.

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

배포 된 사이트에 없는 *amd64* 하 고 *x86* 하위 폴더는 응용 프로그램에 네이티브 어셈블리를 사용 하 여 *bin* 폴더입니다. SQL Server Compact 설치 된 컴퓨터에서 네이티브 어셈블리에 위치한 *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private*합니다. Visual Studio 프로젝트에 올바른 폴더에 올바른 파일을 얻을 수 있는 최상의 방법은 NuGet SqlServerCompact 패키지를 설치 하는 것입니다. 네이티브 어셈블리를 복사 하는 빌드 후 스크립트를 추가 하는 패키지 설치 *amd64* 하 고 *x86*합니다. 그러나 배포에 대 한 순서로 프로젝트에 수동으로 포함 해야 합니다. 자세한 내용은 참조는 [SQL Server Compact 배포](../../older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md) 자습서입니다.

## <a name="path-is-not-valid-error-after-deploying-an-entity-framework-code-first-application"></a>Entity Framework Code First 응용 프로그램을 배포한 후 "경로가 잘못 되었습니다." 오류

### <a name="scenario"></a>시나리오

SQL Server Compact 데이터베이스를 앱의 파일에 저장 하는 같은 Entity Framework Code First 마이그레이션 및 DBMS를 사용 하는 응용 프로그램을 배포한\_데이터 폴더. Code First 마이그레이션 후 첫 번째 배포 데이터베이스를 만들도록 구성 해야 합니다. 응용 프로그램을 실행 하는 경우 다음 예제와 같이 오류 메시지를 가져옵니다.

경로가 잘못 되었습니다. 데이터베이스에 대 한 디렉터리를 확인 합니다. [Path = c:\inetpub\wwwroot\App\_Data\DatabaseName.sdf ]

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

먼저 코드 데이터베이스 하지만 앱을 만들려고 시도\_데이터 폴더가 존재 하지 않습니다. 에 모든 파일을 저장 하지 않은 하거나 합니다 *앱\_데이터* 를 배포 하면 또는 선택한 폴더 **제외 앱\_데이터** 에 **웹패키지및게시** 프로젝트 속성 창의 탭 합니다. 서버에 복사할 폴더에 파일이 없을 경우 배포 프로세스 서버에서 폴더를 만듭니다 없습니다. 사이트에서 설정한 데이터베이스를 이미 설치한 경우 배포 프로세스는 파일을 삭제 하며 *앱\_데이터* 폴더를 선택한 경우 자체 **대상에서 추가 파일 제거** 에서 게시 프로필입니다. .txt 파일과 같은 문제를 해결 하기 위해 자리 표시자 파일을 저장 합니다 *앱\_데이터* 폴더 필요가 있는지 **제외 앱\_데이터** 선택 하 고 다시 배포 합니다.

## <a name="com-object-that-has-been-separated-from-its-underlying-rcw-cannot-be-used"></a>"기본 RCW에서 분리 된 COM 개체를 사용할 수 없습니다."

### <a name="scenario"></a>시나리오

성공적으로 되었습니다 한 번의 클릭을 사용 하 여 응용 프로그램 배포를 게시 하 고이 오류를 가져오기 시작 합니다.

Web deployment 작업에 실패 했습니다. (원격 에이전트 URL로 요청을 완료할 수 없습니다 '<https://serverurl.com/msdeploy.axd?site=sitename>'.)  
 원격 에이전트 URL로 요청을 완료할 수 없습니다 '<https://url/msdeploy.axd?site=sitename>'.  
요청이 중단 되었습니다: 요청이 취소 되었습니다.  
기본 RCW에서 분리 된 COM 개체를 사용할 수 없습니다.

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

기본적으로 Visual Studio 설정 사이트의 루트 폴더에 읽기 권한 및 앱에 대 한 쓰기 권한이\_데이터 폴더. 응용 프로그램 하위 폴더에 대 한 쓰기 액세스에 필요한 경우이 시리즈의 자습서에서는 프로덕션 환경에 배포 폴더 사용 권한 설정에 표시 된 것 처럼 해당 폴더에 대 한 권한을 설정할 수 있습니다. 응용 프로그램 사이트의 루트 폴더에 대 한 쓰기 액세스에 필요한 경우 추가 하 여 루트 폴더에 읽기 전용 액세스를 설정 하지 못하도록 **&lt;IncludeSetACLProviderOn 대상&gt;False&lt;/ IncludeSetACLProviderOnDestination&gt;** (모든 프로필 적용할).wpp.targets 파일 또는 게시 프로필 파일 (단일 프로필을 적용할). 이러한 파일을 편집 하는 방법에 대 한 정보를 참조 하세요 [방법: 프로필 (.pubxml) 파일에서 배포 설정을 편집](https://msdn.microsoft.com/library/ff398069.aspx)합니다.

<a id="aspnet45error"></a>

## <a name="configuration-error---targetframework-attribute-references-a-version-that-is-later-than-the-installed-version-of-the-net-framework"></a>구성 오류-targetFramework 특성 참조의.NET Framework 설치 된 버전 보다 최신 버전

### <a name="scenario"></a>시나리오

ASP.NET 4.5를 대상으로 하는 웹 프로젝트를 성공적으로 게시 되지만 다음 오류가 발생 하면 ("꺼짐" 파일에 있는 web.config로 customErrors 모드)와 응용 프로그램을 실행 하는 경우:

'TargetFramework' 특성을 &lt;컴파일&gt; Web.config 파일의 요소 나중의.NET Framework 4.0 대상 버전에만 사용 됩니다 (예를 들어, '&lt;컴파일 targetFramework = "4.0"&gt;'). 'TargetFramework' 특성에는 현재 설치 된 버전의.NET Framework 보다 최신 버전을 참조 합니다. .NET Framework의 올바른 대상 버전을 지정 하거나.NET Framework의 필수 버전을 설치 합니다.

오류 페이지의 소스 오류 상자 오류의 원인으로 Web.config에서 다음 줄을 강조 표시합니다.

&lt;컴파일 targetFramework = "4.5" /&gt;

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

서버에서 ASP.NET 4.5를 지원 하지 않습니다. 시기 및 ASP.NET 4.5에 대 한 지원을 추가할 수 있는지를 확인 하려면 호스팅 공급자에 게 문의 합니다. ASP.NET 4 또는 이전 버전을 대상으로 하는 웹 프로젝트를 배포 해야 하는 서버를 업그레이드 하는 옵션이 아닌 경우 대신 합니다.

동일한 대상에는 ASP.NET 4 또는 이전 웹 프로젝트를 배포 하는 경우 선택 합니다 **대상에서 추가 파일 제거** 확인란 합니다 **설정** 탭은 **웹 게시**마법사. 선택 하지 않으면 **대상에서 추가 파일 제거**에 구성 오류 페이지를 계속 합니다.

프로젝트 **속성** windows에는 대상 프레임 워크 드롭다운 목록에 포함 되어 있지만 변경 하 여이 문제를 해결할 수 없는 **.NET Framework 4.5** 에 **.NETFramework4**. 이전 프레임 워크 버전으로 대상 프레임 워크를 변경 하면 프로젝트는 최신 프레임 워크 버전의 어셈블리에 대 한 참조 및 여전히 실행 되지 않습니다. 해야 수동으로 해당 참조를 변경 하거나.NET Framework 4 또는 이전 버전을 대상으로 하는 새 프로젝트를 만듭니다. 자세한 내용은 [웹 사이트에 대 한.NET Framework 타기](https://msdn.microsoft.com/library/bb398791(v=vs.100).aspx)합니다.

## <a name="medium-trust-errors"></a>보통 신뢰 오류

### <a name="scenario"></a>시나리오

프로덕션 환경에서 응용 프로그램을 실행 하는 경우에 보통 신뢰와 관련 된 오류가 가져옵니다.

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

많은 타사 호스팅 공급자는 몇 가지 작업을 수행할 수 없습니다는 보통 신뢰에서 웹 사이트를 실행 합니다. 예를 들어, 응용 프로그램 코드 없습니다 Windows 레지스트리에 액세스 및 없습니다 읽기 또는 쓰기 응용 프로그램의 폴더 계층 구조 외부에 있는 파일입니다. 기본적으로 응용 프로그램에서 실행 *완전 신뢰* 로컬 컴퓨터에서 의미 하는 응용 프로그램이 프로덕션에 배포할 때 오류가 발생 하는 작업을 수행 하는 일을 할 수 있습니다.

문제를 해결 하기 위해 로컬 IIS 환경에서 보통 신뢰에서 실행 되도록 응용 프로그램을 구성할 수 있습니다. 이렇게 하려면 응용 프로그램을 엽니다 *Web.config* 파일을 추가한를 **트러스트** 요소에는 **system.web** 요소를이 예와 같이 합니다.

[!code-xml[Main](troubleshooting/samples/sample11.xml)]

응용 프로그램이 이제 로컬 컴퓨터에도 IIS에서 보통 신뢰에서 실행 됩니다.

이 경우 작업을 수행 하지 Azure 보통 신뢰 필요 하지 않기 때문에 Azure App Service에 배포 됩니다. 2012 년 2 월에에서이 자습서를 쓰고 시이 메서드를 사용 하 여 응용 프로그램을 쉽게 보통 신뢰 수준에서 실행 하면 오류가 발생 Azure에서.

Entity Framework Code First 마이그레이션을 사용 하는 보통 신뢰 수준에서 응용 프로그램을 실행 하는 호스팅 공급자에 배포 하는 경우 버전 5.0 했는지 또는 나중에 설치를 확인 합니다. Entity framework 버전 4.3, 마이그레이션 데이터베이스 스키마를 업데이트 하려면 완전 신뢰가 필요 합니다.

## <a name="http-40417-not-found-error"></a>HTTP 404.17 찾을 수 없음 오류

### <a name="scenario"></a>시나리오

IIS에서 개발 컴퓨터에 배포 된 사이트를 실행 하면 서버 Default.aspx를 처리할 수 없습니다를 보고 다음 오류 메시지가 표시:

HTTP 오류 404.17-찾을 수 없음

요청 된 콘텐츠를 스크립트로 및 정적 파일 처리기에서 처리 되지 않습니다.

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결

컴퓨터에 ASP.NET 4.5를 설치할 수 있습니다. ASP.NET 4.5를 설치 하는 방법을 설명 하는이 시리즈의 자습서 테스트 환경으로 IIS에 배포의 단계를 참조 하세요.

> [!div class="step-by-step"]
> [이전](deploying-extra-files.md)
