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
# <a name="aspnet-webhooks-logging"></a>ASP.NET 웹 후크 로깅

Microsoft ASP.NET 웹 후크 문제 및 문제를 보고 하는 방법으로 로깅을 사용 합니다. 기본적으로 로그를 사용 하 여 기록 됩니다 [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) 수 있는 관리를 사용 하 여 [추적 수신기](https://msdn.microsoft.com/library/system.diagnostics.tracelistener.aspx) 같은 다른 로그 스트림 합니다.

Azure Web App으로 웹 응용 프로그램을 배포할 때 자동으로 선택 되므로 및이 로그 다른와 함께 관리할 수 있습니다 [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) 로깅. 자세한 내용은 참조 하십시오 [Azure App Service에서 웹 앱에 대 한 진단 로깅을 사용 하도록 설정](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/)

또한에서 직접 로그를 가져올 수 있습니다에 설명 된 대로 Visual Studio 내 [Visual Studio를 사용 하 여 Azure App Service에서 웹 앱 문제 해결](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)합니다.

## <a name="redirecting-logs"></a>로그 리디렉션

로그를 작성 하는 대신 [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace)와 같은 로그 관리자에 게 직접 기록할 수 있는 대체 로깅 구현을 제공 하는 것이 불가능 [Log4Net](http://logging.apache.org/log4net/) 고 [NLog ](http://nlog-project.org/). 구현 만으로는 [ILogger](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Common/Diagnostics/ILogger.cs) 원하는 종속성 주입 엔진을 사용 하 여 등록 하 고 Microsoft ASP.NET 웹 후크에 의해 픽업 가져오기 됩니다. 참조 하세요 [ASP.NET Web API 2에서 종속성 주입](https://www.asp.net/web-api/overview/advanced/dependency-injection) 세부 정보에 대 한 합니다.
