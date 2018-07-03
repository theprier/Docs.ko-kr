---
uid: webhooks/diagnostics/logging
title: ASP.NET 웹 후크 로깅 | Microsoft Docs
author: rick-anderson
description: ASP.NET 웹 후크 로그인 작업을 수행 하는 방법입니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/17/2012
ms.topic: article
ms.assetid: f71bc442-5f80-481b-a32c-a0ec18dee9d6
ms.technology: ''
ms.openlocfilehash: 5501d250ea6dd86c0cfddec8d9941ec16b4f57ba
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37364108"
---
# <a name="aspnet-webhooks-logging"></a><span data-ttu-id="09243-103">ASP.NET 웹 후크 로깅</span><span class="sxs-lookup"><span data-stu-id="09243-103">ASP.NET WebHooks logging</span></span>

<span data-ttu-id="09243-104">Microsoft ASP.NET 웹 후크 문제 및 문제를 보고 하는 방법으로 로깅을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="09243-104">Microsoft ASP.NET WebHooks uses logging as a way of reporting issues and problems.</span></span> <span data-ttu-id="09243-105">기본적으로 로그를 사용 하 여 기록 됩니다 [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) 수 있는 관리를 사용 하 여 [추적 수신기](https://msdn.microsoft.com/library/system.diagnostics.tracelistener.aspx) 같은 다른 로그 스트림 합니다.</span><span class="sxs-lookup"><span data-stu-id="09243-105">By default logs are written using [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) where they can be manged using [Trace Listeners](https://msdn.microsoft.com/library/system.diagnostics.tracelistener.aspx) like any other log stream.</span></span>

<span data-ttu-id="09243-106">Azure Web App으로 웹 응용 프로그램을 배포할 때 자동으로 선택 되므로 및이 로그 다른와 함께 관리할 수 있습니다 [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) 로깅.</span><span class="sxs-lookup"><span data-stu-id="09243-106">When deploying your Web Application as an Azure Web App, the logs are automatically picked up and can be managed together with any other [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) logging.</span></span> <span data-ttu-id="09243-107">자세한 내용은 참조 하십시오 [Azure App Service에서 웹 앱에 대 한 진단 로깅을 사용 하도록 설정](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/)</span><span class="sxs-lookup"><span data-stu-id="09243-107">For details, please see [Enable diagnostics logging for web apps in Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/)</span></span>

<span data-ttu-id="09243-108">또한에서 직접 로그를 가져올 수 있습니다에 설명 된 대로 Visual Studio 내 [Visual Studio를 사용 하 여 Azure App Service에서 웹 앱 문제 해결](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)합니다.</span><span class="sxs-lookup"><span data-stu-id="09243-108">In addition, logs can be obtained straight from inside Visual Studio as described in [Troubleshoot a web app in Azure App Service using Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).</span></span>

## <a name="redirecting-logs"></a><span data-ttu-id="09243-109">로그 리디렉션</span><span class="sxs-lookup"><span data-stu-id="09243-109">Redirecting Logs</span></span>

<span data-ttu-id="09243-110">로그를 작성 하는 대신 [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace)와 같은 로그 관리자에 게 직접 기록할 수 있는 대체 로깅 구현을 제공 하는 것이 불가능 [Log4Net](http://logging.apache.org/log4net/) 고 [NLog ](http://nlog-project.org/).</span><span class="sxs-lookup"><span data-stu-id="09243-110">Instead of writing logs to [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace), it is possible to provide an alternate logging implementation that can log directly to a log manager such as [Log4Net](http://logging.apache.org/log4net/) and [NLog](http://nlog-project.org/).</span></span> <span data-ttu-id="09243-111">구현 만으로는 [ILogger](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Common/Diagnostics/ILogger.cs) 원하는 종속성 주입 엔진을 사용 하 여 등록 하 고 Microsoft ASP.NET 웹 후크에 의해 픽업 가져오기 됩니다.</span><span class="sxs-lookup"><span data-stu-id="09243-111">Simply provide an implementation of [ILogger](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Common/Diagnostics/ILogger.cs) and register it with a dependency injection engine of your choice and it will get picked up by Microsoft ASP.NET WebHooks.</span></span> <span data-ttu-id="09243-112">참조 하세요 [ASP.NET Web API 2에서 종속성 주입](https://www.asp.net/web-api/overview/advanced/dependency-injection) 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="09243-112">Please see [Dependency Injection in ASP.NET Web API 2](https://www.asp.net/web-api/overview/advanced/dependency-injection) for details.</span></span>
