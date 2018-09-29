---
title: ASP.NET Core 호스트 및 배포
author: rick-anderson
description: 호스팅 환경을 설정하고 ASP.NET Core 앱을 배포하는 방법을 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 08/07/2017
uid: host-and-deploy/index
ms.openlocfilehash: 024275be3fc5db3f2ed2f7cea1582a1a5f12bda7
ms.sourcegitcommit: 32f5ee0690604d451f61e9a5c28881c9fcf85738
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/29/2018
ms.locfileid: "47454760"
---
# <a name="host-and-deploy-aspnet-core"></a>ASP.NET Core 호스트 및 배포

일반적으로 ASP.NET Core 앱을 호스팅 환경에 배포하기 위해서는 다음을 수행합니다.

* 호스팅 서버의 폴더에 앱을 게시합니다.
* 요청이 도착할 때 앱을 시작하고 작동이 중단되거나 서버가 다시 부팅된 후 앱을 다시 시작하는 프로세스 관리자를 설정합니다.
* 역방향 프록시 구성이 필요한 경우 요청을 앱에 전달하는 역방향 프록시를 설정합니다.

## <a name="publish-to-a-folder"></a>폴더에 게시

[dotnet publish](/dotnet/articles/core/tools/dotnet-publish) CLI 명령은 앱 코드를 컴파일하고 앱을 *publish* 폴더로 실행하는 데 필요한 파일을 복사합니다. Visual Studio에서 배포할 경우 파일이 배포 대상에 복사되기 전에 [dotnet publish](/dotnet/core/tools/dotnet-publish) 단계가 자동으로 수행됩니다.

### <a name="folder-contents"></a>폴더 콘텐츠

*publish* 폴더에는 앱, 해당 종속성 및 필요한 경우 .NET 런타임에 대한 *.exe* 및 *.dll* 파일이 있습니다.

.NET Core 앱은 *자체 포함* 또는 *프레임워크 종속* 앱으로 게시할 수 있습니다. 앱이 자체 포함인 경우 .NET 런타임이 포함된 *.dll* 파일은 *publish* 폴더에 포함됩니다. 앱이 프레임워크 종속인 경우 서버에 설치된 .NET 버전에 대한 참조가 앱에 포함되므로 .NET 런타임 파일이 포함되지 않습니다. 기본 배포 모델은 프레임워크 종속입니다. 자세한 내용은 [.NET Core 응용 프로그램 배포](/dotnet/articles/core/deploying/index)를 참조하세요.

*.exe* 및 *.dll* 파일 이외에 ASP.NET Core 앱에 대한 *publish* 폴더에는 일반적으로 구성 파일, 정적 자산 및 MVC 뷰가 포함됩니다. 자세한 내용은 [디렉터리 구조](xref:host-and-deploy/directory-structure)를 참조하세요.

## <a name="set-up-a-process-manager"></a>프로세스 관리자 설정

ASP.NET Core 앱은 서버가 부팅되고 작동 중단 후 다시 시작될 때 시작되어야 하는 콘솔 앱입니다. 시작 및 다시 시작을 자동화하려면 프로세스 관리자가 필요합니다. ASP.NET Core에 대한 가장 일반적인 프로세스 관리자는 다음과 같습니다.

* Linux
  * [Nginx](xref:host-and-deploy/linux-nginx)
  * [Apache](xref:host-and-deploy/linux-apache)
* Windows
  * [IIS](xref:host-and-deploy/iis/index)
  * [Windows 서비스](xref:host-and-deploy/windows-service)

## <a name="set-up-a-reverse-proxy"></a>역방향 프록시 설정

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

앱에서 [Kestrel](xref:fundamentals/servers/kestrel) 웹 서버를 사용할 경우 [Nginx](xref:host-and-deploy/linux-nginx), [Apache](xref:host-and-deploy/linux-apache) 또는 [IIS](xref:host-and-deploy/iis/index)를 역방향 프록시 서버로 사용할 수 있습니다. 역방향 프록시 서버는 인터넷에서 HTTP 요청을 수신하고 몇몇 사전 처리 후에 Kestrel에 전달합니다.

&mdash;역방향 프록시 서버의 유무에 상관없이&mdash; ASP.NET Core 2.0 이상 앱에 대해 지원되는 유효한 호스팅 구성입니다. 자세한 내용은 [Kestrel를 역방향 프록시와 함께 사용할 경우](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy)를 참조하세요.

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

앱에서 [Kestrel](xref:fundamentals/servers/kestrel) 웹 서버를 사용하고 인터넷에 노출될 경우 [Nginx](xref:host-and-deploy/linux-nginx), [Apache](xref:host-and-deploy/linux-apache) 또는 [IIS](xref:host-and-deploy/iis/index)를 역방향 프록시 서버로 사용합니다. 역방향 프록시 서버는 인터넷에서 HTTP 요청을 수신하고 몇몇 사전 처리 후에 Kestrel에 전달합니다. 역방향 프록시를 사용하는 주요 이유는 보안 때문입니다. 자세한 내용은 [Kestrel를 역방향 프록시와 함께 사용할 경우](xref:fundamentals/servers/kestrel?tabs=aspnetcore1x#when-to-use-kestrel-with-a-reverse-proxy)를 참조하세요.

---

## <a name="proxy-server-and-load-balancer-scenarios"></a>프록시 서버 및 부하 분산 장치 시나리오

프록시 서버 및 부하 분산 장치 외에도 호스팅되는 앱에 추가 구성이 필요할 수 있습니다. 추가 구성이 없는 앱에는 체계(HTTP/HTTPS) 및 요청이 시작된 원격 IP 주소에 대한 액세스 권한이 없을 수 있습니다. 자세한 내용은 [프록시 서버 및 부하 분산 장치를 사용하도록 ASP.NET Core 구성](xref:host-and-deploy/proxy-load-balancer)을 참조하세요.

## <a name="using-visual-studio-and-msbuild-to-automate-deployment"></a>Visual Studio 및 MSBuild를 사용하여 배포 자동화

일반적으로 배포에는 [dotnet publish](/dotnet/core/tools/dotnet-publish)에서 서버로 출력을 복사하는 것 외에 추가 작업이 필요합니다. 예를 들어 추가 파일이 필요하거나 *publish* 폴더에서 제외될 수 있습니다. Visual Studio에서는 웹 배포에 MSBuild를 사용하고 MSBuild를 사용자 지정하여 배포 중에 많은 다른 작업을 수행할 수 있습니다. 자세한 내용은 [Visual Studio에서 프로필 게시](xref:host-and-deploy/visual-studio-publish-profiles) 및 [MSBuild 및 Team Foundation Build 사용](http://msbuildbook.com/) 문서를 참조하세요.

[웹 게시 기능](xref:tutorials/publish-to-azure-webapp-using-vs)을 사용하거나 [기본 제공 Git 지원](xref:host-and-deploy/azure-apps/azure-continuous-deployment)을 사용하여 Visual Studio에서 Azure App Service로 앱을 직접 배포할 수 있습니다. Azure DevOps Services는 [Azure App Service에 지속적인 배포](/azure/devops/pipelines/targets/webapp)를 지원합니다.

## <a name="publishing-to-azure"></a>Azure에 게시

Visual Studio를 사용하여 Azure에 앱을 게시하는 방법에 관한 지침은 [Visual Studio를 사용하여 Azure App Service에 ASP.NET Core 웹앱 게시](xref:tutorials/publish-to-azure-webapp-using-vs)를 참조하세요. [명령줄](/azure/app-service/app-service-web-get-started-dotnet)에서도 앱을 Azure에 게시할 수 있습니다.

## <a name="host-in-a-web-farm"></a>웹 팜에서 호스트

웹 팜 환경에서 ASP.NET Core 앱을 호스팅하는 구성에 대한 자세한 내용(예: 확장성을 위해 앱의 여러 인스턴스 배포)은 <xref:host-and-deploy/web-farm>을 참조하세요.

## <a name="additional-resources"></a>추가 자료

Docker를 호스팅 환경으로 사용하는 방법에 대한 자세한 내용은 [Docker에서 ASP.NET Core 앱 호스트](xref:host-and-deploy/docker/index)를 참조하세요.
