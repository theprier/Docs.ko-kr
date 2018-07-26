---
title: Azure App Service에서 ASP.NET Core 호스트
author: guardrex
description: 유용한 리소스에 대한 링크를 통해 Azure App Service에서 ASP.NET Core 앱을 호스트하는 방법을 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 07/24/2018
uid: host-and-deploy/azure-apps/index
ms.openlocfilehash: ece61a3e362ec5e2ff8f415351a0f9257fc72098
ms.sourcegitcommit: b4c7b1a4c48dec0865f27874275c73da1f75e918
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2018
ms.locfileid: "39228613"
---
# <a name="host-aspnet-core-on-azure-app-service"></a>Azure App Service에서 ASP.NET Core 호스트

[Azure App Service](https://azure.microsoft.com/services/app-service/)는 ASP.NET Core를 비롯한 웹앱을 호스트하기 위한 [Microsoft 클라우드 컴퓨팅 플랫폼 서비스](https://azure.microsoft.com/)입니다.

## <a name="useful-resources"></a>유용한 리소스

Azure [Web Apps 설명서](/azure/app-service/)는 Azure 앱 설명서, 샘플, 방법 가이드 및 기타 리소스를 제공합니다. ASP.NET Core 앱 호스트와 관련하여 두 가지 주목할 만한 자습서는 다음과 같습니다.

[빠른 시작: Azure에서 ASP.NET Core 웹앱 만들기](/azure/app-service/app-service-web-get-started-dotnet)  
Visual Studio를 사용하여 ASP.NET Core 웹앱을 만들고 Windows의 Azure App Service에 배포합니다.

[빠른 시작: Linux의 App Service에서 .NET Core 웹앱 만들기](/azure/app-service/containers/quickstart-dotnetcore)  
명령줄을 사용하여 ASP.NET Core 웹앱을 만들고 Linux의 Azure App Service에 배포합니다.

다음 문서는 ASP.NET Core 설명서에 제공됩니다.

[Visual Studio를 사용하여 Azure에 게시](xref:tutorials/publish-to-azure-webapp-using-vs)  
Visual Studio를 사용하여 Azure App Service에 ASP.NET Core 앱을 게시하는 방법을 알아봅니다.

[CLI 도구를 사용하여 Azure에 게시](xref:tutorials/publish-to-azure-webapp-using-cli)  
Git 명령줄 클라이언트를 사용하여 Azure App Service에 ASP.NET Core 앱을 게시하는 방법을 알아봅니다.

[Visual Studio 및 Git을 사용하여 Azure에 연속 배포](xref:host-and-deploy/azure-apps/azure-continuous-deployment)  
Visual Studio를 사용하여 ASP.NET Core 웹앱을 만들고 연속 배포를 위한 Git을 사용하여 Azure App Service에 배포하는 방법을 알아봅니다.

[VSTS를 사용하여 Azure에 연속 배포](https://www.visualstudio.com/docs/build/aspnet/core/quick-to-azure)  
ASP.NET Core 앱에 대한 CI 빌드를 설정하고 Azure App Service에 대한 연속 배포 릴리스를 만듭니다.

[Azure Web App 샌드박스](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox)  
Azure 앱 플랫폼에서 적용하는 Azure App Service 런타임 실행 제한 사항을 알아봅니다.

::: moniker range=">= aspnetcore-2.0"

## <a name="application-configuration"></a>응용 프로그램 구성

ASP.NET Core 2.0 이상에서 다음 NuGet 패키지는 Azure App Service에 배포된 앱에 대한 자동 로깅 기능을 제공합니다.

* [Microsoft.AspNetCore.AzureAppServices.HostingStartup](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServices.HostingStartup/)은 [IHostingStartup](xref:fundamentals/configuration/platform-specific-configuration)을 사용하여 Azure App Service와 ASP.NET Core의 강화 통합을 제공합니다. 추가된 로깅 기능은 `Microsoft.AspNetCore.AzureAppServicesIntegration` 패키지에서 제공합니다.
* [Microsoft.AspNetCore.AzureAppServicesIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServicesIntegration/)은 [AddAzureWebAppDiagnostics](/dotnet/api/microsoft.extensions.logging.azureappservicesloggerfactoryextensions.addazurewebappdiagnostics)를 실행하여 `Microsoft.Extensions.Logging.AzureAppServices` 패키지의 Azure App Service 진단 로깅 공급자를 추가합니다.
* [Microsoft.Extensions.Logging.AzureAppServices](https://www.nuget.org/packages/Microsoft.Extensions.Logging.AzureAppServices/)는 Azure App Service 진단 로그 및 로그 스트리밍 기능을 지원하는 로거 구현을 제공합니다.

.NET Core를 대상으로 지정하고 [Microsoft.AspNetCore.All 메타패키지](xref:fundamentals/metapackage)를 참조하는 경우 패키지가 이미 포함되어 있습니다. 패키지는 최신 [Microsoft.AspNetCore.App 메타패키지](xref:fundamentals/metapackage-app)에 포함되어 있지 않습니다. .NET Framework를 대상으로 지정하거나 `Microsoft.AspNetCore.App` 메타패키지를 참조하는 경우 개별 로깅 패키지를 참조합니다.

::: moniker-end

## <a name="proxy-server-and-load-balancer-scenarios"></a>프록시 서버 및 부하 분산 장치 시나리오

체계(HTTP/HTTPS) 및 요청이 시작된 원격 IP 주소를 전달하도록 전달된 헤더 미들웨어를 구성하는 IIS 통합 미들웨어 및 ASP.NET Core 모듈을 구성합니다. 추가 프록시 서버 및 부하 분산 장치 외에도 호스팅되는 앱에 추가 구성이 필요할 수 있습니다. 자세한 내용은 [프록시 서버 및 부하 분산 장치를 사용하도록 ASP.NET Core 구성](xref:host-and-deploy/proxy-load-balancer)을 참조하세요.

## <a name="monitoring-and-logging"></a>모니터링 및 로깅

모니터링, 로깅 및 문제 해결에 대한 자세한 내용은 다음 문서를 참조하세요.

[방법: Azure App Service에서 앱 모니터링](/azure/app-service/web-sites-monitor)  
앱 및 App Service 계획의 할당량 및 메트릭을 검토하는 방법을 알아봅니다.

[Azure App Service에서 웹앱에 대한 진단 로깅 사용](/azure/app-service/web-sites-enable-diagnostic-log)  
HTTP 상태 코드, 실패한 요청 및 웹 서버 활동에 대한 진단 로깅을 활성화하고 액세스하는 방법을 알아봅니다.

[ASP.NET Core의 오류 처리 소개](xref:fundamentals/error-handling)  
ASP.NET Core 앱에서 오류를 처리하기 위한 일반적인 접근법을 이해합니다.

[Azure App Service에서 ASP.NET Core 문제 해결](xref:host-and-deploy/azure-apps/troubleshoot)  
ASP.NET Core 앱을 사용하는 Azure App Service 배포에 대한 문제 진단 방법을 알아봅니다.

[ASP.NET Core를 사용하는 Azure App Service 및 IIS에 대한 일반적인 오류 참조](xref:host-and-deploy/azure-iis-errors-reference)  
Azure App Service/IIS에서 호스트하는 앱의 일반적인 배포 구성 오류와 문제 해결에 대한 조언을 참조하세요.

## <a name="data-protection-key-ring-and-deployment-slots"></a>데이터 보호 키 링 및 배포 슬롯

[데이터 보호 키](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management)는 *%HOME%\ASP.NET\DataProtection-Keys* 폴더에 저장됩니다. 이 폴더는 네트워크 저장소에서 지원하고, 앱을 호스트하는 모든 컴퓨터에서 동기화됩니다. 저장된 키는 보호되지 않습니다. 이 폴더는 단일 배포 슬롯에 앱의 모든 인스턴스에 대한 키 링을 제공합니다. 준비 및 프로덕션과 같은 별도의 배포 슬롯은 키 링을 공유하지 않습니다.

배포 슬롯을 바꿀 경우 데이터 보호를 사용하는 모든 시스템은 이전 슬롯 내에 있는 키 링을 사용하여 저장된 데이터의 암호를 해독할 수 없습니다. ASP.NET 쿠키 미들웨어는 데이터 보호를 사용하여 쿠키를 보호합니다. 이로 인해 표준 ASP.NET 쿠키 미들웨어를 사용하는 앱에서 사용자가 로그아웃됩니다. 슬롯에 관계없는 키 링 솔루션의 경우 다음과 같은 외부 키 링 공급자를 사용하세요.

* Azure Blob Storage
* Azure Key Vault
* SQL 저장소
* Redis Cache

자세한 내용은 [키 저장소 공급자](xref:security/data-protection/implementation/key-storage-providers)를 참조하세요.

## <a name="deploy-aspnet-core-preview-release-to-azure-app-service"></a>Azure App Service에 ASP.NET Core 미리 보기 릴리스 배포

다음과 같은 방법으로 Azure App Service에 ASP.NET Core 미리 보기 앱을 배포할 수 있습니다.

* [미리 보기 사이트 확장 설치](#install-the-preview-site-extension)
* [자체 포함된 앱 배포](#deploy-the-app-self-contained)
* [Web Apps for Containers에서 Docker 사용](#use-docker-with-web-apps-for-containers)

미리 보기 사이트 확장을 사용하는 데 문제가 발생하는 경우 [GitHub](https://github.com/aspnet/azureintegration/issues/new)에서 문제를 엽니다.

### <a name="install-the-preview-site-extension"></a>미리 보기 사이트 확장 설치

1. Azure Portal에서 App Service 블레이드로 이동합니다.
1. 웹앱을 선택합니다.
1. 검색 상자에 "ex"를 입력하거나 관리 창 목록을 **개발 도구** 아래로 스크롤합니다.
1. **개발 도구** > **확장**을 선택합니다.
1. **추가**를 선택합니다.

   ![이전 단계에서 Azure 앱 블레이드](index/_static/x1.png)

1. **ASP.NET Core 확장**을 선택합니다.
1. **확인**을 선택하여 적합한 조건을 적용합니다.
1. 확장을 설치하려면 **확인**을 선택합니다.

추가 작업이 완료되면 최신.NET Core 미리 보기가 설치됩니다. 콘솔에서 `dotnet --info`를 실행하여 설치를 확인할 수 있습니다. **App Service** 블레이드에서:

1. 검색 상자에 "con"을 입력하거나 관리 창 목록을 **개발 도구** 아래로 스크롤합니다.
1. **개발 도구** > **콘솔**을 선택합니다.
1. 콘솔에 `dotnet --info`를 입력합니다.

`2.1.300-preview1-008174` 버전이 최신 미리 보기 릴리스인 경우 명령 프롬프트에서 `dotnet --info`를 실행하여 다음과 같은 출력을 가져옵니다.

![이전 단계에서 Azure 앱 블레이드](index/_static/cons.png)

위 이미지(`2.1.300-preview1-008174`)에 표시된 ASP.NET Core 버전은 예제입니다. `dotnet --info`를 실행하면 사이트 확장을 구성할 때 최신 미리 보기 버전의 ASP.NET Core가 표시됩니다.

`dotnet --info`는 미리 보기가 설치되어 있는 사이트 확장에 대한 경로를 표시합니다. 기본 *ProgramFiles* 위치 대신 사이트 확장에서 앱이 실행된다고 표시합니다. *ProgramFiles*가 표시되면 사이트를 다시 시작하고 `dotnet --info`를 실행합니다.

**ARM 템플릿에서 미리 보기 사이트 확장 사용**

ARM 템플릿을 사용하여 앱을 만들고 배포하는 경우 `siteextensions` 리소스 형식을 사용하여 웹앱에 사이트 확장을 추가할 수 있습니다. 예:

[!code-json[Main](index/sample/arm.json?highlight=2)]

### <a name="deploy-the-app-self-contained"></a>자체 포함된 앱 배포

배포에 미리 보기 런타임을 전달하는 [자체 포함된 앱](/dotnet/core/deploying/#self-contained-deployments-scd)을 배포할 수 있습니다. 자체 포함된 앱을 배포하는 경우:

* 사이트는 준비할 필요가 없습니다.
* 공유 런타임 및 서버의 호스트를 사용하여 프레임워크 종속 배포를 위해 게시할 때와 다르게 앱을 게시해야 합니다.

자체 포함된 앱은 모든 ASP.NET Core 앱에 대한 옵션입니다.

### <a name="use-docker-with-web-apps-for-containers"></a>Web Apps for Containers에서 Docker 사용

[Docker 허브](https://hub.docker.com/r/microsoft/aspnetcore/)에는 최신 미리 보기 Docker 이미지가 포함됩니다. 이미지는 기본 이미지로 사용할 수 있습니다. 이미지를 사용하고 일반적으로 Web App for Containers에 배포합니다.

## <a name="additional-resources"></a>추가 자료

* [Web Apps 개요(5분 개요 비디오)](/azure/app-service/app-service-web-overview)
* [Azure App Service: .NET 앱을 호스트하기에 가장 좋은 서비스(55분 개요 비디오)](https://channel9.msdn.com/events/dotnetConf/2017/T222)
* [Azure Friday: Azure App Service 진단 및 문제 해결 환경(12분 비디오)](https://channel9.msdn.com/Shows/Azure-Friday/Azure-App-Service-Diagnostic-and-Troubleshooting-Experience)
* [Azure App Service 진단 개요](/azure/app-service/app-service-diagnostics)
* <xref:host-and-deploy/web-farm>

Windows Server의 Azure App Service는 [IIS(인터넷 정보 서비스)](https://www.iis.net/)를 사용합니다. 다음 항목은 기본 IIS 기술과 관련이 있습니다.

* <xref:host-and-deploy/iis/index>
* <xref:fundamentals/servers/aspnet-core-module>
* <xref:host-and-deploy/aspnet-core-module>
* <xref:host-and-deploy/iis/modules>
* [Microsoft TechNet 라이브러리: Windows Server](/windows-server/windows-server-versions)
