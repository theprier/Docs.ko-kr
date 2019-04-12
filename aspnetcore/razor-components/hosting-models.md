---
title: Razor 구성 요소 호스팅 모델
author: guardrex
description: 클라이언트 쪽 Blazor 및 서버 쪽 ASP.NET Core Razor 구성 요소 호스팅 모델을 이해 합니다.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 03/28/2019
uid: razor-components/hosting-models
ms.openlocfilehash: 8ed70117c94bf1a3e4c208f70310bbf0473bae44
ms.sourcegitcommit: 6bde1fdf686326c080a7518a6725e56e56d8886e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2019
ms.locfileid: "59515647"
---
# <a name="razor-components-hosting-models"></a>Razor 구성 요소 호스팅 모델

[Daniel Roth](https://github.com/danroth27)

Razor 구성 요소는 클라이언트 쪽에서 실행 하도록 설계 하는 웹 프레임 워크의 브라우저에는 [WebAssembly](http://webassembly.org/)-.NET 런타임 기반 (*Blazor*) 또는 ASP.NET Core에서 서버 쪽 (*ASP.NET Core Razor 구성 요소*). 호스팅 모델, 앱 및 구성 요소 모델에 관계 없이 *동일 하 게 유지*합니다. 이 문서에서는 사용 가능한 호스팅 모델을 설명 합니다.

* [클라이언트 쪽 Blazor](#client-side-hosting-model)
* [서버 쪽 ASP.NET Core Razor 구성 요소](#server-side-hosting-model)

## <a name="client-side-hosting-model"></a>클라이언트 쪽 호스팅 모델

[!INCLUDE[](~/includes/razor-components-preview-notice.md)]

Blazor의 주 호스팅 모델은 WebAssembly 브라우저에서 실행 중인 클라이언트 쪽입니다. Blazor 앱, 해당 앱의 종속성 및 .NET 런타임이 브라우저에 다운로드됩니다. 해당 앱은 브라우저 UI 스레드에서 직접 실행됩니다. 이벤트 처리의 UI 업데이트와 동일한 프로세스 내에서 발생합니다. 앱의 자산을 처리할 수 있는 정적 콘텐츠를 클라이언트에 서비스 웹 서버에 정적 파일로 배포 됩니다.

![Blazor 클라이언트 측: Blazor 앱 브라우저 내에서 UI 스레드에서 실행 됩니다.](hosting-models/_static/client-side.png)

클라이언트 쪽 호스팅 모델을 사용 하는 Blazor 앱을 만들려면 다음 템플릿 중 하나를 사용 합니다.

* **Blazor** ([dotnet 새 blazor](/dotnet/core/tools/dotnet-new)) &ndash; 정적 파일의 집합으로 배포 됩니다.
* **(ASP.NET Core 호스팅) Blazor** ([dotnet 새 blazorhosted](/dotnet/core/tools/dotnet-new)) &ndash; ASP.NET Core 서버에서 호스트 합니다. ASP.NET Core 앱 Blazor 앱 클라이언트를 제공 합니다. 웹 API 호출을 사용 하 여 네트워크를 통해 클라이언트 쪽 Blazor 앱 서버와 상호 작용할 수 또는 [SignalR](xref:signalr/introduction)합니다.

템플릿을 포함 합니다 *components.webassembly.js* 처리 하는 스크립트:

* .NET 런타임, 앱 및 앱의 종속성을 다운로드 합니다.
* 앱을 실행 하려면 런타임 초기화 합니다.

클라이언트 쪽 호스팅 모델에는 몇 가지 이점을 제공합니다. 클라이언트 쪽 Blazor:

* .NET 서버 쪽 종속성을 있습니다.
* 클라이언트 리소스 및 기능을 최대한 활용합니다.
* 오프 로드 서버에서 클라이언트로 작동 합니다.
* 오프 라인 시나리오를 지원합니다.

클라이언트 쪽 호스팅에 단점이 있습니다. 클라이언트 쪽 Blazor:

* 브라우저의 기능으로 앱을 제한합니다.
* 지원 되는 클라이언트 하드웨어 및 소프트웨어 (예를 들어, WebAssembly 지원)에 필요합니다.
* 로드 시간 더 오래 앱을 더 큰 다운로드 크기에 있습니다.
* .NET 런타임 및 도구 지원 성숙 적습니다 (예를 들어, 제한 사항 [.NET Standard](/dotnet/standard/net-standard) 지원 및 디버깅) 합니다.

## <a name="server-side-hosting-model"></a>서버 쪽 호스팅 모델

ASP.NET Core Razor 구성 요소 서버 쪽 호스팅 모델을 사용 하 여 응용 프로그램 서버에서 ASP.NET Core 앱 내에서 실행 됩니다. UI 업데이트, 이벤트 처리 및 JavaScript 호출을 통해 처리 되는 [SignalR](xref:signalr/introduction) 연결 합니다.

![ASP.NET Core Razor 구성 요소 서버 측: 브라우저와 상호 작용 (ASP.NET Core 앱 내에서 호스팅) 앱 서버에서 SignalR 연결을 통해.](hosting-models/_static/server-side.png)

ASP.NET Core를 사용 하 여 서버 쪽 호스팅 모델을 사용 하는 구성 요소 Razor 앱을 만들려면 **구성 요소 Razor** 템플릿 ([dotnet 새 razorcomponents](/dotnet/core/tools/dotnet-new)). ASP.NET Core 앱 Razor 구성 요소 서버 쪽 앱을 호스트 하 고 클라이언트가 연결 된 SignalR 끝점을 설정 합니다. 앱의를 참조 하는 ASP.NET Core 앱 `Startup` 추가할 클래스:

* 서버 쪽 구성 요소 Razor 서비스입니다.
* 요청 처리 파이프라인에 대 한 앱입니다.

[!code-csharp[](hosting-models/samples_snapshot/Startup.cs?highlight=5,27)]

합니다 *components.server.js* 스크립트&dagger; 클라이언트 연결을 설정 합니다. 것은 앱의 책임 (예를 들어 네트워크 연결이) 발생할 경우 필요에 따라 앱 상태를 유지 및 복원입니다.

서버 쪽 호스팅 모델에는 몇 가지 이점을 제공합니다. 서버 쪽 Razor 구성 요소:

* 클라이언트 쪽 Blazor 앱을 보다 훨씬 작은 앱 크기가 있고 훨씬 빠르게 로드 됩니다.
* 모든.NET Core 호환 되는 Api를 사용 하는 등 서버 기능의 활용을 걸릴 수 있습니다.
* 도구, 디버깅와 같은 기존.NET 예상 대로 작동 하므로.NET Core에 서버에서 실행 합니다.
* 씬 클라이언트와 함께 (예: 브라우저 WebAssembly 및 리소스를 지원 하지 않는 제한 된 장치).
* .NET /C# 앱의 구성 요소 코드를 포함 하 여 코드 베이스를 클라이언트에 제공 되지 않습니다.

서버 쪽 호스팅에 단점이 있습니다. 서버 쪽 Razor 구성 요소:

* 대기를 시간이 길어집니다. 모든 사용자 상호 작용을 네트워크 홉이 됩니다.
* 없는 오프 라인 지원을 제공 합니다. 클라이언트 연결에 실패 하면 앱 작동이 중지 됩니다.
* 확장성이 저하. 서버는 여러 클라이언트 연결을 관리 하 고 클라이언트 상태를 처리 해야 합니다.
* 앱을 제공 하는 ASP.NET Core 서버가 필요 합니다. (예: CDN)에서 서버 없이 배포 할 수 없습니다.

&dagger;합니다 *components.server.js* 스크립트는 다음 경로에 게시 됩니다. *bin / {디버그 | 릴리스} / {대상 프레임 워크} /publish/ {응용 프로그램 이름}. 앱/배포/_framework*합니다.
