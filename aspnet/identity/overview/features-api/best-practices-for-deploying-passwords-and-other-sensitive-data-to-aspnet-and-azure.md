---
uid: identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure
title: ASP.NET 및 Azure App Service에 암호 및 기타 중요 한 데이터 배포에 대 한 유용한 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서는 어떻게 코드가 안전 하 게 저장 및 액세스할 수 보안 정보를 보여줍니다. 가장 중요 한 점은 암호나 다른 발신자 저장 하지 말아야 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/21/2015
ms.topic: article
ms.assetid: 97902c66-cb61-4d11-be52-73f962f2db0a
ms.technology: ''
msc.legacyurl: /identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure
msc.type: authoredcontent
ms.openlocfilehash: 8434c439cef7e30ddd45b78bb0bca5e4daeceaff
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37371011"
---
<a name="best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure-app-service"></a>ASP.NET 및 Azure App Service에 암호 및 기타 중요 한 데이터를 배포 하기 위한 모범 사례
====================
[Rick Anderson](https://github.com/Rick-Anderson)

> 이 자습서는 어떻게 코드가 안전 하 게 저장 및 액세스할 수 보안 정보를 보여줍니다. 무엇보다 중요한 점은 절대로 소스 코드에 암호나 기타 중요한 데이터를 저장하면 안 될 뿐만 아니라, 프로덕션 환경의 보안 정보를 개발 및 테스트 모드에서 사용해서는 안 된다는 것입니다
> 
> 샘플 코드 중 이며 간단한 WebJob 콘솔 앱을 데이터베이스 연결 문자열 암호, Twilio, SendGrid 및 Google을 보안 키에 액세스 해야 하는 ASP.NET MVC 앱
> 
> 온-프레미스 설정 및 PHP도 언급 됩니다.


- [개발 환경에서 암호를 사용 하 여 작업](#pwd)
- [개발 환경에서 연결 문자열 사용](#con)
- [WebJobs 콘솔 앱](#wj)
- [비밀을 Azure에 배포](#da)
- [온-프레미스 및 PHP에 대 한 정보](#not)
- [추가 리소스](#addRes)

<a id="pwd"></a>
## <a name="working-with-passwords-in-the-development-environment"></a>개발 환경에서 암호를 사용 하 여 작업

자습서는 자주 바랍니다 소스 코드에서 중요 한 데이터를 저장 하지 마십시오는 주의 해야를 사용 하 여 소스 코드에서 중요 한 데이터를 표시 합니다. 예를 들어, 내 [SMS 및 전자 메일 2FA 사용 하 여 ASP.NET MVC 5 앱](../../../mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md) 자습서에서 다음을 보여 합니다 *web.config* 파일:

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample1.xml)]

합니다 *web.config* 파일 이므로 소스 코드 파일에서 이러한 암호 저장 해서는 안 됩니다. 다행 스럽게도 합니다 `<appSettings>` 요소에는 `file` 중요 한 앱 구성 설정이 포함 된 외부 파일을 지정할 수 있는 특성입니다. 외부 파일에 소스 트리를 확인 하지는으로 외부 파일에 모든 비밀을 이동할 수 있습니다. 예를 들어, 다음 태그 파일에서에서 *AppSettingsSecrets.config* 모든 앱 암호를 포함 합니다.

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample2.xml)]

외부 파일에 태그 (*AppSettingsSecrets.config* 이 예제의)를에서 동일한 태그를 발견 되는 *web.config* 파일:

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample3.xml)]

태그를 사용 하 여 외부 파일의 내용을 병합 하는 ASP.NET 런타임이 &lt;appSettings&gt; 요소입니다. 지정된 된 파일을 찾을 수 없는 경우 런타임에서 파일 특성을 무시 합니다.

> [!WARNING]
> 보안-추가 하지 마십시오 하 *비밀.config* 프로젝트 파일 또는 소스 제어에 체크 인 합니다. 기본적으로 Visual Studio는 다음과 같이 설정 됩니다.는 `Build Action` 를 `Content`, 즉, 파일을 배포 합니다. 자세한 내용은 참조 하세요. [왜 없는 프로젝트 폴더 내에 있는 파일의 모든 배포?](https://msdn.microsoft.com/library/ee942158(v=vs.110).aspx#can_i_exclude_specific_files_or_folders_from_deployment) 에 대 한 모든 확장을 사용할 수 있지만 합니다 *비밀.config* 파일인 것이 가장 좋습니다 유지 *.config*처럼 IIS에서 구성 파일을 제공 하지 않습니다. 또한 합니다 *AppSettingsSecrets.config* 파일이 두 디렉터리 수준에서는 *web.config* 파일 이기 때문에 솔루션 디렉터리를 완전히 벗어납니다. 솔루션 디렉터리에서 파일을 이동 하 여 &quot;git 추가 \* &quot; 리포지토리에 추가 하지 않습니다.


<a id="con"></a>
## <a name="working-with-connection-strings-in-the-development-environment"></a>개발 환경에서 연결 문자열 사용

Visual Studio를 사용 하는 새 ASP.NET 프로젝트를 만듭니다 [LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx)합니다. LocalDB는 개발 환경에 맞게 만들어졌습니다. 암호를 필요 하지 않습니다, 그리고 따라서 소스 코드에 검사에서 비밀을 방지 하기 위해 아무것도 할 필요가 없습니다. 일부 개발 팀은 암호를 요구 하는 SQL Server (또는 다른 DBMS)의 전체 버전을 사용 합니다.

사용할 수는 `configSource` 전체를 바꾸려면 특성 `<connectionStrings>` 태그입니다. 달리는 `<appSettings>` `file` 태그를 병합 하는 특성을 `configSource` 특성은 태그를 대체 합니다. 에서는 다음 태그를 `configSource` 특성을 *web.config* 파일:

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample4.xml?highlight=1)]

> [!NOTE]
> 사용 하는 경우는 `configSource` 외부 파일에 연결 문자열을 이동 하려면 위에 표시 된 대로 특성 및 Visual studio 새 웹 사이트 만들기, 데이터베이스를 사용 하는 데이터베이스를 구성 하는 옵션이 제공 되지 않습니다 및 검색할 수 없습니다 경우 있습니다 pu Visual Studio에서 Azure로 blish 합니다. 사용 중인 경우는 `configSource` 특성인 PowerShell를 사용 하 여 만들고 웹 사이트 및 데이터베이스를 배포 하거나 만들 수 있습니다 웹 사이트 및 데이터베이스는 포털에서 게시 하기 전에 합니다. 합니다 [새로 만들기-AzureWebsitewithDB.ps1](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3) 스크립트에서 새 웹 사이트와 데이터베이스를 만듭니다.


> [!WARNING]
> 보안-달리 합니다 *AppSettingsSecrets.config* 파일을 외부 연결 문자열 파일 같은 루트 디렉터리에 있어야 *web.config* 않도록 예방 조치를 수행 해야 하므로 파일 원본 리포지토리로 확인 하지 마십시오.


> [!NOTE]
> **비밀 파일에서 보안 경고:** 테스트 및 개발에서 프로덕션 비밀을 사용 하지 않는 것이 좋습니다. 테스트 또는 개발에서 프로덕션 암호를 사용 하 여 이러한 비밀 누수가 발생 합니다.


<a id="wj"></a>
## <a name="webjobs-console-apps"></a>WebJobs 콘솔 앱

합니다 *app.config* 콘솔 앱에서 사용 되는 파일 상대 경로 지원 하지 않지만 절대 경로 지원 하지 않습니다. 프로젝트 디렉터리에서 암호를 이동할 절대 경로 사용할 수 있습니다. 다음 태그의 암호를 보여 줍니다.는 *C:\secrets\AppSettingsSecrets.config* 파일 및 비 중요 한 데이터에는 *app.config* 파일입니다.

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample5.xml?highlight=2)]

<a id="da"></a>
## <a name="deploying-secrets-to-azure"></a>비밀을 Azure에 배포

Azure에 웹 앱을 배포할 때 합니다 *AppSettingsSecrets.config* (즉, 원하는) 파일을 배포할 수 없습니다. 이동할 수 있습니다 합니다 [Azure 관리 포털](https://azure.microsoft.com/services/management-portal/) 이렇게 하려면 수동으로 설정 합니다.

1. 로 이동 [ https://portal.azure.com ](https://portal.azure.com), Azure 자격 증명으로 로그인 합니다.
2. 클릭 **찾아보기 &gt; Web Apps**, 웹 앱의 이름을 클릭 합니다.
3. 클릭 **모든 설정 &gt; 응용 프로그램 설정**합니다.

**앱 설정** 하 고 **연결 문자열** 값의 동일한 설정을 재정의 합니다 *web.config* 파일. 예에서에서는 배포 되지 않은 이러한 설정을 azure에 이러한 키에 있던 경우 하지만 합니다 *web.config* 파일을 포털에 표시 된 설정 보다 우선적으로 적용 됩니다.

수행 하는 것이 좋습니다는 [DevOps 워크플로](../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything.md) 사용 하 여 [Azure PowerShell](https://azure.microsoft.com/documentation/articles/install-configure-powershell/) (또는와 같은 다른 프레임 워크 [Chef](http://www.opscode.com/chef/) 하거나 [Puppet](http://puppetlabs.com/puppet/what-is-puppet))를 Azure에서 이러한 값을 설정 합니다. 자동화 합니다. 다음 PowerShell 스크립트를 사용 하 여 [Export-clixml](http://www.powershellcookbook.com/recipe/PukO/securely-store-credentials-on-disk) 디스크를 암호화 된 암호를 내보내려면:

[!code-powershell[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample6.ps1)]

'Name' 위의 스크립트에서 비밀 키의 이름 예는 '&quot;FB\_AppSecret&quot; 또는 "TwitterSecret"입니다. 브라우저에서 스크립트에서 만든 ".credential" 파일을 볼 수 있습니다. 아래 코드 조각은 각 자격 증명 파일을 테스트 하 고 명명 된 웹 앱에 대 한 암호를 설정 합니다.

[!code-powershell[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample7.ps1)]

> [!WARNING]
> 보안-중요 한 데이터를 배포 하려면 PowerShell 스크립트를 사용 하는 목적은 따라서 비교를 수행 하는 PowerShell 스크립트에 암호나 다른 비밀을 포함 하지 마세요. 합니다 [Get-credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet은 암호를 가져옵니다 하는 보안 메커니즘을 제공 합니다. UI 프롬프트를 사용 하 여 암호를 누수 방지할 수 있습니다.


### <a name="deploying-db-connection-strings"></a>배포 DB 연결 문자열

DB 연결 문자열은 앱 설정에 마찬가지로 처리 됩니다. Visual Studio에서 웹 앱을 배포 하는 경우 사용자에 대 한 연결 문자열 구성 됩니다. 포털에서이 확인할 수 있습니다. PowerShell을 사용 하 여 연결 문자열을 설정 하는 방법이 권장된 됩니다. PowerShell 스크립트의 예는 웹 사이트 및 데이터베이스를 만들고 연결 문자열을 설정 합니다. 웹 사이트에서 다운로드 [새로 만들기-AzureWebsitewithDB.ps1](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3) 에서 [Azure 스크립트 라이브러리](https://gallery.technet.microsoft.com/scriptcenter/site/search?f%5B0%5D.Type=RootCategory&amp;f%5B0%5D.Value=WindowsAzure).

<a id="not"></a>
## <a name="notes-for-php"></a>PHP에 대 한 정보

키-값 쌍을 둘 다에 대 한 이후 **앱 설정** 하 고 **연결 문자열** 모든 웹 앱 프레임 워크 (예: PHP) 수를 쉽게 사용 하는 개발자가 Azure App Service에서 환경 변수에 저장 되어 이러한 값을 검색 합니다. Stefan Schackow의를 참조 하세요 [Windows Azure 웹 사이트: 응용 프로그램 문자열 및 연결 문자열 작동 방식](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/) 앱 설정 및 연결 문자열을 읽을 PHP 코드 조각을 보여 주는 블로그 게시물.

## <a name="notes-for-on-premises-servers"></a>온-프레미스 서버에 대 한 정보

보안 암호에서 온-프레미스 웹 서버에 배포 하는 경우 도움이 [구성 파일의 구성 섹션 암호화](https://msdn.microsoft.com/library/ff647398.aspx)합니다. 안으로, Azure Websites에 대 한 권장 되는 동일한 접근 방식을 사용할 수 있습니다: 구성 파일에서 개발 설정을 유지 하 고 프로덕션 설정에 대 한 환경 변수 값을 사용 합니다. 하지만 Azure Websites에서 자동는 기능에 대 한 응용 프로그램 코드를 작성 해야,이 경우: 환경 변수에서 설정을 검색 하 고 구성 파일 설정 대신 이러한 값을 사용 또는 구성 파일 설정을 사용 하면 환경 변수를 제공 하지 않습니다.

<a id="addRes"></a>
## <a name="additional-resources"></a>추가 리소스

PowerShell의 예는 웹 앱 및 데이터베이스를 만드는 스크립트를 설정 연결 문자열 + 앱 설정, 다운로드 [새로 만들기-AzureWebsitewithDB.ps1](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3) 에서 합니다 [Azure 스크립트 라이브러리](https://gallery.technet.microsoft.com/scriptcenter/site/search?f%5B0%5D.Type=RootCategory&amp;f%5B0%5D.Value=WindowsAzure)합니다. 

Stefan Schackow 참조 [Windows Azure 웹 사이트: 응용 프로그램 문자열 및 연결 문자열 작업을 하는 방법](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)


Barry Dorrans 주신 ( [ @blowdart ](https://twitter.com/blowdart) ) 및 Carlos Farre 검토 합니다.
