---
title: ASP.NET 및 ASP.NET Core 중에서 선택
author: rick-anderson
description: ASP.NET 및 ASP.NET Core 중에서 선택하는 방법을 알아보세요.
ms.author: riande
ms.date: 05/11/2018
uid: fundamentals/choose-between-aspnet-and-aspnetcore
ms.openlocfilehash: 6d759c0bc5e5c7d32d6c14786db6ba9fe7a2f1e8
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36297232"
---
# <a name="choose-between-aspnet-and-aspnet-core"></a>ASP.NET 및 ASP.NET Core 중에서 선택

만들려는 웹앱과 관계없이 ASP.NET에는 Windows Server를 대상으로 하는 엔터프라이즈 웹앱에서 Linux 컨테이너를 대상으로 하는 작은 마이크로 서비스 및 그 사이의 모든 항목에 대한 솔루션이 있습니다.

## <a name="aspnet-core"></a>ASP.NET Core

ASP.NET Core는 Windows, macOS 또는 Linux에서 클라우드 기반 최신 웹앱을 빌드하기 위한 오픈 소스 플랫폼 간 프레임워크입니다.

## <a name="aspnet"></a>ASP.NET

ASP.NET은 Windows에서 엔터프라이즈급 서버 기반 웹앱을 만들 때 필요한 모든 서비스를 제공하는 완성도 있는 프레임워크입니다.

## <a name="framework-selection"></a>프레임워크 선택 영역

사용자의 요구에 가장 적합한 프레임워크를 확인하려면 아래 표를 검토합니다.

| ASP.NET Core | ASP.NET |
|---|---|
|Windows, macOS 또는 Linux용 빌드|Windows용 빌드|
|[Razor 페이지](xref:razor-pages/index)는 ASP.NET Core 2.x에서 웹 UI를 만드는 좋은 방법입니다. [MVC](xref:mvc/overview), [Web API](xref:tutorials/first-web-api) 및 [SignalR](xref:signalr/introduction)도 참조하세요.|[Web Forms](/aspnet/web-forms), [SignalR](/aspnet/signalr), [MVC](/aspnet/mvc), [Web API](/aspnet/web-api/), [WebHooks](/aspnet/webhooks/) 또는 [웹 페이지](/aspnet/web-pages)를 사용합니다.|
|컴퓨터당 여러 버전|컴퓨터당 하나의 버전|
|C# 또는 F#을 사용하여 Visual Studio, [Mac용 Visual Studio](https://www.visualstudio.com/vs/visual-studio-mac/) 또는 [Visual Studio Code](https://code.visualstudio.com/)에서 개발|C#, VB 또는 F#을 사용하여 Visual Studio에서 개발|
|ASP.NET보다 고성능|성능 양호|
|[.NET Framework 또는 .NET Core 런타임 선택](/dotnet/articles/standard/choosing-core-framework-server)|.NET Framework 런타임 사용|

## <a name="aspnet-core-scenarios"></a>ASP.NET Core 시나리오

* [Razor 페이지](xref:razor-pages/index)는 ASP.NET Core 2.x에서 웹 UI를 만드는 좋은 방법입니다.
* [웹 사이트](xref:tutorials/first-mvc-app/index)
* [API](xref:tutorials/first-web-api)
* [실시간](xref:signalr/index)

## <a name="aspnet-scenarios"></a>ASP.NET 시나리오

* [웹 사이트](/aspnet/mvc)
* [API](/aspnet/web-api)
* [실시간](/aspnet/signalr)

## <a name="resources"></a>자료

* [ASP.NET 소개](/aspnet/overview)
* [ASP.NET Core 소개](xref:index)
