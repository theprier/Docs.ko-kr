---
uid: identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure
title: ASP.NET 및 Azure 앱 서비스에 암호 및 기타 중요 한 데이터 배포에 대 한 유용한 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 어떻게 코드 안전 하 게 저장 하 고 수 보안 정보에 액세스 합니다. 가장 중요 한 점은 암호 또는 다른 보낼 저장 해서는 안 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/21/2015
ms.topic: article
ms.assetid: 97902c66-cb61-4d11-be52-73f962f2db0a
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure
msc.type: authoredcontent
ms.openlocfilehash: 995d9a088e3095f36a01d2adb19ec08e6a6d1b3e
ms.sourcegitcommit: 6784510cfb589308c3875ccb5113eb31031766b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2018
ms.locfileid: "28033023"
---
<a name="best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure-app-service"></a>ASP.NET 및 Azure 앱 서비스 암호 및 기타 중요 한 데이터를 배포 하기 위한 모범 사례
====================
으로 [Rick Anderson](https://github.com/Rick-Anderson)

> 이 자습서에서는 어떻게 코드 안전 하 게 저장 하 고 수 보안 정보에 액세스 합니다. 무엇보다 중요한 점은 절대로 소스 코드에 암호나 기타 중요한 데이터를 저장하면 안 될 뿐만 아니라, 프로덕션 환경의 보안 정보를 개발 및 테스트 모드에서 사용해서는 안 된다는 것입니다
> 
> 샘플 코드는 간단한 WebJob 콘솔 응용 프로그램 및 한 데이터베이스 연결 문자열 암호, Twilio, Google 및 SendGrid 보안 키에 액세스 해야 하는 ASP.NET MVC 응용 프로그램입니다.
> 
> 온-프레미스 설정 및 PHP는도 다룹니다.


- [개발 환경에서 암호 작업](#pwd)
- [개발 환경에서 연결 문자열 작업](#con)
- [WebJobs 콘솔 응용 프로그램](#wj)
- [Azure에 배포 하는 암호](#da)
- [온-프레미스 및 PHP에 대 한 정보](#not)
- [추가 리소스](#addRes)

<a id="pwd"></a>
## <a name="working-with-passwords-in-the-development-environment"></a>개발 환경에서 암호 작업

자습서는 자주 소스 코드에는 중요 한 데이터를 저장 하지 마십시오 해야 하는 주의할 다행 스럽게도 함께 소스 코드에서 중요 한 데이터를 표시 합니다. 예를 들어, 내 [SMS 및 전자 메일 2FA로 ASP.NET MVC 5 앱](../../../mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md) 에서 다음을 보여 주는 자습서는 *web.config* 파일:

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample1.xml)]

*web.config* 파일 이므로 소스 코드를 해당 파일에 이러한 암호 저장 해서는 안 됩니다. 다행히는 `<appSettings>` 요소에는 `file` 특성을 중요 한 응용 프로그램 구성 설정을 포함 하는 외부 파일을 지정할 수 있습니다. 외부 파일은 소스 트리에 체크 인 되지으로 외부 파일에 모든 암호를 이동할 수 있습니다. 다음 태그 파일의 예를 들어 *AppSettingsSecrets.config* 모든 앱 암호를 포함 합니다.

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample2.xml)]

외부 파일에 태그 (*AppSettingsSecrets.config* 이 샘플에서)를 동일한 태그에서 찾을 수는 *web.config* 파일:

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample3.xml)]

ASP.NET 런타임 병합의 태그를 사용 하 여 외부 파일의 내용을 &lt;appSettings&gt; 요소입니다. 런타임에서 지정된 된 파일을 찾을 수 없는 경우 파일 특성을 무시 합니다.

> [!WARNING]
> 보안-추가 하지 않으면 프로그램 *비밀.config* 프로젝트에 파일 또는 소스 제어에 체크 인 합니다. 기본적으로 Visual Studio 설정에서 `Build Action` 를 `Content`, 배포 된 파일을 의미 하는 합니다. 자세한 내용은 참조 [이유 하지 않는 프로젝트 폴더 내에 있는 파일의 모든 배포?](https://msdn.microsoft.com/library/ee942158(v=vs.110).aspx#can_i_exclude_specific_files_or_folders_from_deployment) 에 대 한 모든 확장을 사용할 수 있지만 *비밀.config* 파일인 것이 가장 좋습니다 유지 *.config*마찬가지로 IIS에서 구성 파일을 제공 하지 않습니다. 또한는 *AppSettingsSecrets.config* 파일은 최대 두 디렉터리 수준에서의 *web.config* 파일 이기 때문에 솔루션 디렉터리를 완전히 벗어났습니다. 솔루션 디렉터리에서 파일을 이동 하 여 &quot;git 추가 \* &quot; 리포지토리에 추가 되지는 않습니다.


<a id="con"></a>
## <a name="working-with-connection-strings-in-the-development-environment"></a>개발 환경에서 연결 문자열 작업

Visual Studio를 사용 하는 새 ASP.NET 프로젝트를 만듭니다 [LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx)합니다. LocalDB 개발 환경에 맞게 만들어졌습니다. 암호를 필요 하지 않습니다, 그리고 따라서 소스 코드에 검사에서 비밀 정보를 방지 하기 위해 어떤 작업도 수행할 필요가 없습니다. 일부 개발 팀 암호를 요구 하는 전체 버전의 SQL Server (또는 다른 DBMS)를 사용 합니다.

사용할 수는 `configSource` 전체를 바꿀 특성 `<connectionStrings>` 태그입니다. 와 달리는 `<appSettings>` `file` 특성의 태그를 병합 하는 `configSource` 특성은 태그를 대체 합니다. 에서는 다음 태그는 `configSource` 특성에 *web.config* 파일:

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample4.xml?highlight=1)]

> [!NOTE]
> 사용 하는 경우는 `configSource` 외부 파일로 연결 문자열을 이동 하려면 위와 같이 특성 및 새 웹 사이트를 만들려면 Visual studio, 데이터베이스를 사용 하 고 데이터베이스 구성의 옵션은 가져올 수를 검색 하지 못할 때 있습니다 pu Visual Studio에서 Azure에 게시 합니다. 사용 하는 경우는 `configSource` 특성을 PowerShell을 사용 하 여 웹 사이트 및 데이터베이스를 만들고 배포 하려면 하거나 만들 수 있습니다 웹 사이트와 데이터베이스 포털에 게시 하기 전에. [새로 AzureWebsitewithDB.ps1](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3) 스크립트는 새 웹 사이트 및 데이터베이스를 만듭니다.


> [!WARNING]
> 보안-달리는 *AppSettingsSecrets.config* 파일을 외부 연결 문자열 파일의 루트와 같은 디렉터리에 있어야 *web.config* 파일 이기 때문에 위해 예방 조치를 수행 해야 합니다. 소스 저장소로 확인 하지 마십시오.


> [!NOTE]
> **파일에 대 한 보안 경고:** 가장 좋은 방법은 프로덕션 테스트 및 개발에는 암호를 사용 하지 않도록 합니다. 테스트 또는 개발에서 생산 암호를 사용 하 여 이러한 암호 누수가 발생 합니다.


<a id="wj"></a>
## <a name="webjobs-console-apps"></a>WebJobs 콘솔 응용 프로그램

*app.config* 콘솔 응용 프로그램에서 사용 하는 파일 상대 경로 지원 하지 않지만 절대 경로 지원 합니다. 프로젝트 디렉터리에 암호를 벗어나게 하는 절대 경로 사용할 수 있습니다. 다음 태그에 비밀 정보를 보여 줍니다.는 *C:\secrets\AppSettingsSecrets.config* 파일 및 비 중요 한 데이터에는 *app.config* 파일입니다.

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample5.xml?highlight=2)]

<a id="da"></a>
## <a name="deploying-secrets-to-azure"></a>Azure에 배포 하는 암호

Azure에 웹 앱을 배포할 때의 *AppSettingsSecrets.config* (즉, 대상) 파일을 배포 되지 않습니다. 이동 해야 할 수는 [Azure 관리 포털](https://azure.microsoft.com/services/management-portal/) 그렇게 하려면 수동으로 설정 하 고 있습니다.

1. 로 이동 [ https://portal.azure.com ](https://portal.azure.com), Azure 자격 증명으로 로그인 합니다.
2. 클릭 **찾아보기 &gt; 웹 앱**, 웹 응용 프로그램의 이름을 클릭 합니다.
3. 클릭 **모든 설정을 &gt; 응용 프로그램 설정**합니다.

**앱 설정** 및 **연결 문자열** 값의 동일한 설정을 재정의 *web.config* 파일입니다. 예에서 우리 배포 되지 않은 이러한 설정을 Azure에 이러한 키 모두에 있지만 *web.config* 파일을 포털에 표시 된 설정을 우선 합니다.

수행 하는 것이 좋습니다는 [DevOps 워크플로](../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything.md) 사용 하 여 [Azure PowerShell](https://azure.microsoft.com/documentation/articles/install-configure-powershell/) (또는와 같은 다른 프레임 워크 [Chef](http://www.opscode.com/chef/) 또는 [Puppet](http://puppetlabs.com/puppet/what-is-puppet))를 자동화 Azure에서 이러한 값을 설정 합니다. 다음 PowerShell 스크립트를 사용 하 여 [Export-clixml](http://www.powershellcookbook.com/recipe/PukO/securely-store-credentials-on-disk) 디스크에 암호화 된 암호를 내보내려면:

[!code-powershell[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample6.ps1)]

위의 스크립트에 'Name'의 이름인 비밀 키와 같은 '&quot;FB\_AppSecret&quot; 또는 "TwitterSecret"입니다. 브라우저에서 스크립트에 의해 생성 되는 ".credential" 파일을 볼 수 있습니다. 아래 코드 조각 각 자격 증명 파일을 테스트 하 고 명명 된 웹 응용 프로그램에 대 한 암호를 설정 합니다.

[!code-powershell[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample7.ps1)]

> [!WARNING]
> 보안-암호 또는 기타 암호 중요 한 데이터를 배포 하는 PowerShell 스크립트를 사용 하는 목적은 너무 비교를 수행 하는 PowerShell 스크립트에 포함 하지 않습니다. [Get-credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet은 암호를 가져옵니다 하는 보안 메커니즘을 제공 합니다. UI 프롬프트를 사용 하는 암호를 누수 방지할 수 있습니다.


### <a name="deploying-db-connection-strings"></a>배포 DB 연결 문자열

앱 설정 DB 연결 문자열 비슷하게 처리 됩니다. Visual Studio에서 웹 앱을 배포 하는 경우 사용자에 대 한 연결 문자열 구성 됩니다. 포털에서이 확인할 수 있습니다. 연결 문자열을 설정 하는 권장된 방법은 PowerShell과 함께 됩니다. PowerShell 스크립트의 예는 웹 사이트를 만들고 데이터베이스 및 연결 문자열 설정 웹 사이트에서 다운로드 [새로 AzureWebsitewithDB.ps1](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3) 에서 [Azure 스크립트 라이브러리](https://gallery.technet.microsoft.com/scriptcenter/site/search?f%5B0%5D.Type=RootCategory&amp;f%5B0%5D.Value=WindowsAzure)합니다.

<a id="not"></a>
## <a name="notes-for-php"></a>PHP에 대 한 참고 사항

키-값 쌍 모두에 대 한 이후 **앱 설정** 및 **연결 문자열** 모든 웹 응용 프로그램 (PHP) 등의 프레임 워크 수를 쉽게 사용 하는 개발자가 Azure 앱 서비스 환경 변수에 저장 되어 있는 이러한 값을 검색 합니다. Stefan Schackow 참조 [Windows Azure 웹 사이트: 방법: 응용 프로그램 문자열 및 연결 문자열 작업](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/) 앱 설정 및 연결 문자열을 읽는 PHP 코드 조각을 보여 주는 블로그 게시물입니다.

## <a name="notes-for-on-premises-servers"></a>온-프레미스 서버에 대 한 참고 사항

온-프레미스 웹 서버를 배포 하는 경우에 하 여 보안 비밀을 도울 수 있습니다 [구성 파일의 구성 섹션 암호화](https://msdn.microsoft.com/library/ff647398.aspx)합니다. 대신 Azure 웹 사이트에 대 한 권장 같은 방법을 사용할 수 있습니다: 구성 파일에서 개발 설정 유지 하 고 프로덕션 설정에 대 한 환경 변수 값을 사용 합니다. 하지만 Azure 웹 사이트에서 자동 기능에 대 한 응용 프로그램 코드를 작성 해야이 경우: 환경 변수에서 설정을 검색 하 여 구성 파일 설정 대신 해당 값을 사용 하거나 구성 파일 설정을 사용 하는 경우 환경 변수는 찾을 수 없습니다.

<a id="addRes"></a>
## <a name="additional-resources"></a>추가 리소스

PowerShell에 대 한 예제 웹 응용 프로그램 + 데이터베이스를 만드는 스크립트를 설정 하는 연결 문자열 + 응용 프로그램 설정, 다운로드 [새로 AzureWebsitewithDB.ps1](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3) 에서 [Azure 스크립트 라이브러리](https://gallery.technet.microsoft.com/scriptcenter/site/search?f%5B0%5D.Type=RootCategory&amp;f%5B0%5D.Value=WindowsAzure)합니다. 

Stefan Schackow 참조 [Windows Azure 웹 사이트: 방법을 응용 프로그램 문자열 및 연결 문자열의 작동](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)


Barry Dorrans 노고 ( [ @blowdart ](https://twitter.com/blowdart) ) 및 Carlos Farre 검토 합니다.
