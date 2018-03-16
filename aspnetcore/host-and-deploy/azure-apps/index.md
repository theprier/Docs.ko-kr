---
title: "Azure App Service에서 ASP.NET Core 호스트"
author: guardrex
description: "유용한 리소스에 대한 링크를 통해 Azure App Service에서 ASP.NET Core 앱을 호스트하는 방법을 알아봅니다."
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 01/29/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/azure-apps/index
ms.openlocfilehash: cefbc27c8091a2ed1441663e3779d67aae2c64dd
ms.sourcegitcommit: 493a215355576cfa481773365de021bcf04bb9c7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
# <a name="host-aspnet-core-on-azure-app-service"></a>Azure App Service에서 ASP.NET Core 호스트

[Azure App Service](https://azure.microsoft.com/services/app-service/)는 ASP.NET Core를 비롯한 웹앱을 호스트하기 위한 [Microsoft 클라우드 컴퓨팅 플랫폼 서비스](https://azure.microsoft.com/)입니다.

[!INCLUDE[Azure App Service Preview Notice](../../includes/azure-apps-preview-notice.md)]

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

[Continuous deployment to Azure with VSTS](https://www.visualstudio.com/docs/build/aspnet/core/quick-to-azure)(VSTS를 사용하여 Azure에 연속 배포)  
ASP.NET Core 앱에 대한 CI 빌드를 설정하고 Azure App Service에 대한 연속 배포 릴리스를 만듭니다.

[Azure Web App 샌드박스](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox)  
Azure 앱 플랫폼에서 적용하는 Azure App Service 런타임 실행 제한 사항을 알아봅니다.

## <a name="application-configuration"></a>응용 프로그램 구성

ASP.NET Core 2.0 이상에서 [Microsoft.AspNetCore.All 메타패키지](xref:fundamentals/metapackage)의 세 패키지는 Azure App Service에 배포된 앱을 위한 자동 로깅 기능을 제공합니다.

* [Microsoft.AspNetCore.AzureAppServices.HostingStartup](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServices.HostingStartup/)은 [IHostingStartup](xref:host-and-deploy/platform-specific-configuration)을 사용하여 Azure App Service와 ASP.NET Core의 라이트업 통합을 제공합니다. 추가된 로깅 기능은 `Microsoft.AspNetCore.AzureAppServicesIntegration` 패키지에서 제공합니다.
* [Microsoft.AspNetCore.AzureAppServicesIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServicesIntegration/)은 [AddAzureWebAppDiagnostics](/dotnet/api/microsoft.extensions.logging.azureappservicesloggerfactoryextensions.addazurewebappdiagnostics)를 실행하여 `Microsoft.Extensions.Logging.AzureAppServices` 패키지의 Azure App Service 진단 로깅 공급자를 추가합니다.
* [Microsoft.Extensions.Logging.AzureAppServices](https://www.nuget.org/packages/Microsoft.Extensions.Logging.AzureAppServices/)는 Azure App Service 진단 로그 및 로그 스트리밍 기능을 지원하는 로거 구현을 제공합니다.

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

## <a name="additional-resources"></a>추가 자료

* [Web Apps 개요(5분 개요 비디오)](/azure/app-service/app-service-web-overview)
* [Azure App Service: .NET 앱을 호스트하기에 가장 좋은 서비스(55분 개요 비디오)](https://channel9.msdn.com/events/dotnetConf/2017/T222)
* [Azure Friday: Azure App Service 진단 및 문제 해결 환경(12분 비디오)](https://channel9.msdn.com/Shows/Azure-Friday/Azure-App-Service-Diagnostic-and-Troubleshooting-Experience)
* [Azure App Service 진단 개요](/azure/app-service/app-service-diagnostics)

Windows Server의 Azure App Service는 [IIS(인터넷 정보 서비스)](https://www.iis.net/)를 사용합니다. 다음 항목은 기본 IIS 기술과 관련이 있습니다.

* [IIS가 있는 Windows에서 ASP.NET Core 호스팅](xref:host-and-deploy/iis/index)
* [ASP.NET Core 모듈 소개](xref:fundamentals/servers/aspnet-core-module)
* [ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module)
* [ASP.NET Core와 함께 IIS 모듈 사용](xref:host-and-deploy/iis/modules)
* [Microsoft TechNet 라이브러리: Windows Server](/windows-server/windows-server-versions)
