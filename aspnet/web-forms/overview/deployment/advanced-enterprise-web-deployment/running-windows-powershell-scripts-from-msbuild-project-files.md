---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/running-windows-powershell-scripts-from-msbuild-project-files
title: MSBuild 프로젝트 파일에서 Windows PowerShell 스크립트 실행 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 빌드 및 배포 프로세스의 일환으로 Windows PowerShell 스크립트를 실행 하는 방법에 설명 합니다. 스크립트를 로컬로 실행할 수 있습니다 (즉,는 b에....
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 55f1ae45-fcb5-43a9-8415-fa5b935fc9c9
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/running-windows-powershell-scripts-from-msbuild-project-files
msc.type: authoredcontent
ms.openlocfilehash: c8ef22cfbba7b3b85944ea4c49f3183e5a6aafbb
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="running-windows-powershell-scripts-from-msbuild-project-files"></a>MSBuild 프로젝트 파일에서 Windows PowerShell 스크립트를 실행합니다.
====================
으로 [Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 빌드 및 배포 프로세스의 일환으로 Windows PowerShell 스크립트를 실행 하는 방법에 설명 합니다. (즉, 빌드 서버)에서 로컬 스크립트를 실행 하거나 원격으로 대상 웹 서버 또는 데이터베이스 서버에 같은 수 있습니다.
> 
> 배포 후 Windows PowerShell 스크립트를 실행 하는 이유는 이유 많습니다. 예를 들어, 다음을 수행합니다.
> 
> - 사용자 지정 이벤트 소스를 레지스트리에 추가 합니다.
> - 업로드에 대해 파일 시스템 디렉터리를 생성 합니다.
> - 빌드 디렉터리를 정리 합니다.
> - 사용자 지정 로그 파일에 항목을 기록 합니다.
> - 새로 프로 비전 된 웹 응용 프로그램에 사용자를 초대 메일을 보냅니다.
> - 적절 한 권한을 가진 사용자 계정을 만듭니다.
> - SQL Server 인스턴스 간 복제를 구성 합니다.
> 
> 이 항목에서는 Microsoft Build Engine (MSBuild) 프로젝트 파일에서 사용자 지정 대상에서 로컬 및 원격으로 Windows PowerShell 스크립트를 실행 하는 방법을 보여줍니다.


이 항목의 Fabrikam, inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 바탕으로 하는 자습서 시리즈의 일부를 형성 합니다. 샘플 솔루션을 사용 하는 자습서 시리즈가&#x2014;는 [Contact Manager 솔루션](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;현실적인 수준의 복잡성, Windows Communication ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내기 위해 WCF (foundation) 서비스 및 데이터베이스 프로젝트.

이 자습서의 핵심에는 배포 방법에 설명 된 분할 프로젝트 파일 접근 방식에 따라 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md), 두 개의 프로젝트 파일에 빌드 프로세스에 의해 제어 되는&#x2014;포함 환경 관련 빌드 및 배포 설정을 포함 하는 하나 및 모든 대상 환경에 적용 되는 지침을 빌드하십시오. 빌드 시 환경 관련 프로젝트 파일은 빌드 지침의 전체 집합을 구성 하기 위해 환경을 알 수 없는 프로젝트 파일에 병합 됩니다.

## <a name="task-overview"></a>작업 개요

단일 단계 또는 자동화 된 배포 프로세스의 일환으로 Windows PowerShell 스크립트를 실행 하려면 이러한 높은 수준의 작업을 완료 해야 합니다.

- 소스 제어 및 솔루션에 Windows PowerShell 스크립트를 추가 합니다.
- Windows PowerShell 스크립트를 호출 하는 명령을 만듭니다.
- 명령에 예약된 된 XML 문자를 이스케이프 합니다.
- 사용자 지정 MSBuild 프로젝트 파일의 대상 만들기 및 사용 된 **Exec** 명령을 실행 하는 작업입니다.

이 항목에서는 이러한 절차를 수행 하는 방법을 보여줍니다. 작업 및이 항목의 연습 MSBuild 대상 및 속성에 잘 알고 이미 하 고 사용자 지정 MSBuild 프로젝트 파일을 빌드 및 배포 프로세스를 진행 하는 데 사용 하는 방법을 이해 해야를 가정 합니다. 자세한 내용은 참조 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md) 및 [빌드 프로세스를 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md)합니다.

## <a name="creating-and-adding-windows-powershell-scripts"></a>만들기 및 Windows PowerShell 스크립트를 추가 합니다.

이 항목의에서 태스크에서는 명명 된 샘플 Windows PowerShell 스크립트를 사용 하 여 **LogDeploy.ps1** MSBuild에서 스크립트를 실행 하는 방법을 보여 주는 것입니다. **LogDeploy.ps1** 스크립트 로그 파일을 한 줄 항목을 기록 하는 간단한 함수가 포함:


[!code-javascript[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample1.js)]


**LogDeploy.ps1** 스크립트에서는 두 개의 매개 변수입니다. 첫 번째 매개 변수는 한 항목을 추가 하려면 로그 파일에 전체 경로 나타내는 및 두 번째 매개 변수는 로그 파일에 기록 하려면 배포 대상을 나타냅니다. 스크립트를 실행 하는 경우 로그 파일에이 형식에 선을 추가 합니다.


[!code-html[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample2.html)]


확인 하는 **LogDeploy.ps1** MSBuild를 사용할 수 있는 스크립트를 사용 해야 합니다.

- 소스 제어에 스크립트를 추가 합니다.
- Visual Studio 2010에서 솔루션에 스크립트를 추가 합니다.

빌드 서버에서 또는 원격 컴퓨터에서 스크립트를 실행 하려면 계획 인지 여부에 관계 없이 솔루션 콘텐츠를 포함 하는 스크립트를 배포할 필요가 없습니다. 한 가지 방법은 솔루션 폴더에 스크립트를 추가할 수 있습니다. 연락처 관리자 예제에서는 배포 프로세스의 일환으로 Windows PowerShell 스크립트를 사용 하려고 하기 때문에 이렇게 하면 게시 솔루션 폴더에 스크립트를 추가할 수 있습니다.

![](running-windows-powershell-scripts-from-msbuild-project-files/_static/image1.png)

솔루션 폴더의 내용은 소스 자료로 빌드 서버에 복사 됩니다. 그러나 프로젝트 출력의 어떠한 부분도 형성합니다.

## <a name="executing-a-windows-powershell-script-on-the-build-server"></a>빌드 서버에서 Windows PowerShell 스크립트를 실행합니다.

일부 시나리오에서는 프로젝트를 작성 하는 컴퓨터에서 Windows PowerShell 스크립트를 실행 하는 것이 좋습니다. 예를 들어 사용자 지정 로그 파일에 항목을 기록 또는 빌드 폴더를 정리 하는 Windows PowerShell 스크립트를 사용할 수 있습니다.

구문의 측면에서 MSBuild 프로젝트 파일에서 Windows PowerShell 스크립트를 실행 같습니다 일반 명령 프롬프트에서 Windows PowerShell 스크립트를 실행 합니다. 호출 실행 powershell.exe를 사용 하려면는 **– 명령** 스위치를 실행 하도록 Windows PowerShell 명령을 제공 합니다. (Windows PowerShell v 2에서 사용할 수도 있습니다는 **– 파일** 전환). 이 명령은이 형식을 취해야 합니다.


[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample3.cmd)]


예를 들어:


[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample4.cmd)]


스크립트에 대 한 경로 공백이 있으면 작은따옴표 앞에 앰퍼샌드 파일 경로 포함 하려면 필요 합니다. 명령을를 이미 사용 했습니다 때문에 큰따옴표를 사용할 수 없습니다.


[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample5.cmd)]


MSBuild에서이 명령을 호출할 때 몇 가지 추가 고려 사항이 있습니다. 첫째, 포함 해야는 **– NonInteractive** 여 스크립트가 자동으로 실행 되는지 확인 하는 플래그입니다. 다음으로 포함 해야는 **– ExecutionPolicy** 플래그는 적절 한 인수 값을 사용 합니다. Windows PowerShell 스크립트에 적용 됩니다 및 스크립트의 실행을 사용할 수 없는 기본 실행 정책을 재정의 하 여 실행 정책을 지정 합니다. 다음 인수 값 중에서 선택할 수 있습니다.

- 값이 **Unrestricted** Windows PowerShell 스크립트에 서명이 있는지 여부에 관계 없이 스크립트를 실행 하면 됩니다.
- 값이 **RemoteSigned** 로컬 컴퓨터에서 생성 된 서명 되지 않은 스크립트를 실행 하려면 Windows PowerShell을 사용 하면 됩니다. 그러나 다른 곳에서 만든 스크립트를 서명 되어야 합니다. (실제로 모르겠으면 빌드 서버에서 로컬로 Windows PowerShell 스크립트를 작성 한 가능성이 매우).
- 값이 **AllSigned** 서명 된 스크립트만 실행 하도록 Windows PowerShell을 사용 하면 됩니다.

기본 실행 정책은 **Restricted**, Windows PowerShell 스크립트 파일 실행을 방지 하는 합니다.

마지막으로, Windows PowerShell 명령에서 발생 하는 예약된 된 XML 문자를 이스케이프 해야 할 수도 있습니다.

- 작은따옴표와 대체  **&amp;a p o s;**
- 큰따옴표와 대체  **&amp;q u o t;**
- 앰퍼샌드와 대체  **&amp;amp;**

- 이러한 변경을 수행한 경우이 명령을 유사 합니다.


[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample6.cmd)]


사용자 지정 MSBuild 프로젝트 파일 내에서 있습니다 수 새 대상을 만들고 사용는 **Exec** 이 명령을 실행 하려면 작업:


[!code-xml[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample7.xml)]


이 예제는 note:

- MSBuild 속성으로 매개 변수 값은 Windows PowerShell 실행 파일의 위치와 같은 변수를 선언 합니다.
- 사용자가 명령줄에서이 값을 재정의할 수 있도록 조건이 포함 됩니다.
- **MSDeployComputerName** 속성이 프로젝트 파일에서 다른 곳에서 선언 됩니다.

이 대상 빌드 프로세스의 일부로 실행 하면 Windows PowerShell 명령을 실행 하 고 지정한 파일에 로그 항목을 쓸 됩니다.

## <a name="executing-a-windows-powershell-script-on-a-remote-computer"></a>원격 컴퓨터에서 Windows PowerShell 스크립트를 실행합니다.

Windows PowerShell은 스크립트를 통해 원격 컴퓨터에서 실행할 수 있는 [Windows 원격 관리](https://msdn.microsoft.com/library/windows/desktop/aa384426.aspx) (WinRM). 이 작업을 수행 하려면 사용 하는 [Invoke-command](https://technet.microsoft.com/library/dd347578.aspx) cmdlet. 이렇게 하면 원격 컴퓨터에 스크립트를 복사 하지 않고 하나 이상의 원격 컴퓨터에 대 한 스크립트를 실행할 수 있습니다. 스크립트를 실행 하 여 로컬 컴퓨터에 모든 결과가 반환 됩니다.

> [!NOTE]
> 사용 하기 전에 **Invoke-command** 원격 컴퓨터에서 스크립트를 실행할 Windows PowerShell cmdlet, 원격 메시지를 수신 하도록 WinRM 수신기를 구성 해야 합니다. 명령을 실행 하 여 이렇게 하려면 **winrm quickconfig** 원격 컴퓨터에 있습니다. 자세한 내용은 참조 [설치 및 구성에 대 한 Windows 원격 관리](https://msdn.microsoft.com/library/windows/desktop/aa384372(v=vs.85).aspx)합니다.


Windows PowerShell 창에서이 구문을 사용 실행 하는 **LogDeploy.ps1** 원격 컴퓨터에서 스크립트:


[!code-powershell[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample8.ps1)]


> [!NOTE]
> 다른 다양 한 방법을 사용 하 여 없는 **Invoke-command** 스크립트를 실행 하려면 파일에 있지만이 방법은 가장 간단한 매개 변수 값을 제공 하 고 공백 사용 하 여 경로 관리 해야 하는 경우.


이 명령 프롬프트에서를 실행 하면 실행 되는 Windows PowerShell을 호출 하 여 사용 해야는 **– 명령** 사용자 지침을 제공 하는 매개 변수:


[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample9.cmd)]


이전에 몇 가지 추가 스위치를 제공 하 고 MSBuild에서 명령을 실행할 때 예약된 된 XML 문자를 이스케이프 해야:


[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample10.cmd)]


마지막으로, 이전 처럼 사용할 수 있습니다는 **Exec** 명령을 실행 하기 위한 사용자 지정 MSBuild 대상 내에서 작업 합니다.


[!code-xml[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample11.xml)]


Windows PowerShell 스크립트에 지정 된 컴퓨터에서 실행 됩니다이 대상 빌드 프로세스의 일환으로를 실행 해도 **– computername** 인수입니다.

## <a name="conclusion"></a>결론

이 항목에는 MSBuild 프로젝트 파일에서 Windows PowerShell 스크립트를 실행 하는 방법을 설명 합니다. 단일 단계 또는 자동화 된 빌드 및 배포 프로세스의 일부로 로컬 또는 원격 컴퓨터에서 Windows PowerShell 스크립트를 실행 하려면이 방법을 사용할 수 있습니다.

## <a name="further-reading"></a>추가 정보

Windows PowerShell 스크립트에 서명을 하 고 실행 정책을 관리에 대 한 지침을 참조 하십시오. [Windows PowerShell 스크립트 실행](https://technet.microsoft.com/library/ee176949.aspx)합니다. 원격 컴퓨터에서 Windows PowerShell 명령 실행에 대 한 지침을 참조 하십시오. [원격 명령 실행](https://technet.microsoft.com/library/dd819505.aspx)합니다.

배포 프로세스 제어 기능을 사용자 지정 MSBuild 프로젝트 파일 사용에 대 한 자세한 내용은 참조 하십시오. [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md) 및 [빌드 프로세스를 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md)합니다.

> [!div class="step-by-step"]
> [이전](taking-web-applications-offline-with-web-deploy.md)
> [다음](troubleshooting-the-packaging-process.md)
