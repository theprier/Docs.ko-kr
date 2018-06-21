---
title: ASP.NET Core의 호스트
author: guardrex
description: 앱 시작 및 수명 관리를 담당하는 ASP.NET Core 웹 호스트 및 .NET 일반 호스트에 대해 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 05/16/2018
uid: fundamentals/host/index
ms.openlocfilehash: 365c679e789c07818c6eb007f40f6aef43b82c44
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36276619"
---
# <a name="host-in-aspnet-core"></a>ASP.NET Core의 호스트

.NET 앱은 *호스트*를 구성 및 실행합니다. 호스트는 앱 시작 및 수명 관리를 담당합니다. 두 개의 호스트 API를 사용할 수 있습니다.

* [웹 호스트](xref:fundamentals/host/web-host) &ndash; 웹 응용 프로그램을 호스팅하는 데 적합합니다.
* [일반 호스트](xref:fundamentals/host/generic-host)(ASP.NET Core 2.1 이상) &ndash; 웹이 아닌 앱(예: 백그라운드 작업을 실행하는 앱)을 호스팅하는 데 적합합니다. 이후 릴리스에서는 일반 호스트가 웹앱을 포함한 모든 종류의 앱을 호스팅하는 데 적합해질 것입니다. 일반 호스트는 결국 웹 호스트를 대체하게 됩니다.

ASP.NET Core *웹앱*을 호스팅할 때 개발자는 [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder)에 기반한 웹 호스트를 사용해야 합니다. *비 웹앱*을 호스팅할 때 개발자는 [HostBuilder](/dotnet/api/microsoft.extensions.hosting.hostbuilder)에 기반한 제네릭 호스트를 사용해야 합니다.
