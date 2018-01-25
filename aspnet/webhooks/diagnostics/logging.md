---
uid: webhooks/diagnostics/logging
title: "ASP.NET Webhook 로깅 | Microsoft Docs"
author: rick-anderson
description: "ASP.NET Webhook에서 로깅을 수행 하는 방법입니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/17/2012
ms.topic: article
ms.assetid: f71bc442-5f80-481b-a32c-a0ec18dee9d6
ms.technology: 
ms.prod: .net-framework
ms.openlocfilehash: 042d20e38a9bc4f1e9792f6e3ff5be11a1eaa882
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
# <a name="aspnet-webhooks-logging"></a><span data-ttu-id="70b76-103">ASP.NET Webhook 로깅</span><span class="sxs-lookup"><span data-stu-id="70b76-103">ASP.NET WebHooks logging</span></span>

<span data-ttu-id="70b76-104">Microsoft ASP.NET Webhook 문제 및 문제를 보고 하는 방법으로 로깅을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b76-104">Microsoft ASP.NET WebHooks uses logging as a way of reporting issues and problems.</span></span> <span data-ttu-id="70b76-105">기본적으로 로그를 사용 하 여 기록 된 [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) 사용 하 여이 사용할 수 있는 [추적 수신기](https://msdn.microsoft.com/library/system.diagnostics.tracelistener.aspx) 다른 로그 스트림과 같은 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b76-105">By default logs are written using [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) where they can be manged using [Trace Listeners](https://msdn.microsoft.com/library/system.diagnostics.tracelistener.aspx) like any other log stream.</span></span>

<span data-ttu-id="70b76-106">로그 자동으로 선택 되므로 및 다른 함께 관리할 수는 Azure 웹 앱으로 웹 응용 프로그램을 배포할 때는 [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) 로깅.</span><span class="sxs-lookup"><span data-stu-id="70b76-106">When deploying your Web Application as an Azure Web App, the logs are automatically picked up and can be managed together with any other [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) logging.</span></span> <span data-ttu-id="70b76-107">자세한 내용은 참조 하십시오 [Azure 앱 서비스의 웹 앱에 대 한 진단 로깅 사용](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/)</span><span class="sxs-lookup"><span data-stu-id="70b76-107">For details, please see [Enable diagnostics logging for web apps in Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/)</span></span>

<span data-ttu-id="70b76-108">또한 바로에서 로그를 얻을 수 있습니다에 설명 된 대로 Visual Studio 내 [Visual Studio를 사용 하 여 Azure 앱 서비스의 웹 앱의 문제를 해결](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)합니다.</span><span class="sxs-lookup"><span data-stu-id="70b76-108">In addition, logs can be obtained straight from inside Visual Studio as described in [Troubleshoot a web app in Azure App Service using Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).</span></span>

## <a name="redirecting-logs"></a><span data-ttu-id="70b76-109">로그 리디렉션</span><span class="sxs-lookup"><span data-stu-id="70b76-109">Redirecting Logs</span></span>

<span data-ttu-id="70b76-110">로그를 작성 하는 대신 [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace)와 같은 로그 관리자에 게 직접 로깅할 수 있는 대체 로깅 구현을 제공 하는 것이 불가능 [Log4Net](http://logging.apache.org/log4net/) 및 [NLog ](http://nlog-project.org/).</span><span class="sxs-lookup"><span data-stu-id="70b76-110">Instead of writing logs to [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace), it is possible to provide an alternate logging implementation that can log directly to a log manager such as [Log4Net](http://logging.apache.org/log4net/) and [NLog](http://nlog-project.org/).</span></span> <span data-ttu-id="70b76-111">구현을 제공 하기만 하면 [ILogger](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Common/Diagnostics/ILogger.cs) 및 선택한 종속성 주입 엔진에 등록 하며 Microsoft ASP.NET Webhook 하 여 선택 가져오기 됩니다.</span><span class="sxs-lookup"><span data-stu-id="70b76-111">Simply provide an implementation of [ILogger](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Common/Diagnostics/ILogger.cs) and register it with a dependency injection engine of your choice and it will get picked up by Microsoft ASP.NET WebHooks.</span></span> <span data-ttu-id="70b76-112">참조 하십시오 [ASP.NET Web API 2의 종속성 주입](https://www.asp.net/web-api/overview/advanced/dependency-injection) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b76-112">Please see [Dependency Injection in ASP.NET Web API 2](https://www.asp.net/web-api/overview/advanced/dependency-injection) for details.</span></span>
