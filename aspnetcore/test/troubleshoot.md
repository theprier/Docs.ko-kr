---
title: ASP.NET Core 프로젝트 문제 해결
author: Rick-Anderson
description: 이해 하 고 경고 및 ASP.NET Core 프로젝트를 사용 하 여 오류를 해결 합니다.
manager: wpickett
ms.author: riande
ms.date: 04/05/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: content
uid: test/troubleshoot
ms.openlocfilehash: 8ff8ddaf4a35a02db650ff429ffbbf4e76a53ecf
ms.sourcegitcommit: 4e3497bda0c3e5011ffba3717eb61a1d46c61c15
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/14/2018
ms.locfileid: "35613007"
---
# <a name="troubleshoot-aspnet-core-projects"></a>ASP.NET Core 프로젝트 문제 해결

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)

다음 링크는 문제 해결 지침을 제공 합니다.

* [Azure App Service에서 ASP.NET Core 문제 해결](xref:host-and-deploy/azure-apps/troubleshoot)
* [IIS에서 ASP.NET Core 문제 해결](xref:host-and-deploy/iis/troubleshoot)
* [ASP.NET Core를 사용하는 Azure App Service 및 IIS에 대한 일반적인 오류 참조](xref:host-and-deploy/azure-iis-errors-reference)
* [ASP.NET Core 응용 프로그램의 문제를 진단 하는 NDC 회의 (런던 2018):](https://www.youtube.com/watch?v=RYI0DHoIVaA)
* [ASP.NET Core 성능 문제를 해결 하는 ASP.NET 블로그:](https://blogs.msdn.microsoft.com/webdev/2018/05/23/asp-net-core-performance-improvements/)

## <a name="net-core-sdk-warnings"></a>.NET core SDK 경고

### <a name="both-the-32-bit-and-64-bit-versions-of-the-net-core-sdk-are-installed"></a>설치 되는 32 비트 및 64 비트 버전의.NET Core SDK

에 **새 프로젝트** 대화 ASP.NET Core에 대 한 다음과 같은 경고가 표시 될 수 있습니다.

> 32와 64 비트 버전의.NET Core SDK 설치 됩니다. 에 설치 된 64 비트 버전에서 템플릿만 ' c:\\Program Files\\dotnet\\sdk\\' 표시 됩니다.

![경고 메시지를 보여 주는 OneASP.NET 대화 상자의 스크린 샷](troubleshoot/_static/both32and64bit.png)

이 경고를 표시 하는 경우 (x86) 32 비트 및 64 비트 (x64) 버전의 모두는 [.NET Core SDK](https://www.microsoft.com/net/download/all) 설치 됩니다. 두 버전을 설치할 수 있습니다 하는 일반적인 이유는 다음과 같습니다.

* 원래 32 비트 컴퓨터를 사용 하 여.NET Core SDK 설치 관리자 다운로드 하지만 다음 복사 프로세스를 수행한 후 하는 64 비트 컴퓨터에 설치 합니다.
* 32 비트.NET Core SDK가 다른 응용 프로그램으로 설치 됩니다.
* 잘못 된 버전은 다운로드 되어 설치 되었습니다.

이 경고를 방지 하기 위해 32 비트.NET Core SDK를 제거 합니다. 제거 **제어판** > **프로그램 및 기능** > **제거 또는 변경 프로그램**합니다. 경고의 발생 이유 및 그 의미를 이해 하는 경우 경고를 무시할 수 있습니다.

### <a name="the-net-core-sdk-is-installed-in-multiple-locations"></a>.NET Core SDK가 여러 위치에 설치 되어 있습니다.

에 **새 프로젝트** 대화 ASP.NET Core에 대 한 다음과 같은 경고가 표시 될 수 있습니다.

> .NET Core SDK는 여러 위치에 설치 됩니다. 에 설치 된과에서 템플릿만 ' c:\\Program Files\\dotnet\\sdk\\' 표시 됩니다.

![경고 메시지를 보여 주는 OneASP.NET 대화 상자의 스크린 샷](troubleshoot/_static/multiplelocations.png)

.NET Core SDK의 하나 이상 설치 디렉터리의 외부에 있는 경우이 메시지가 나타나는 *c:\\Program Files\\dotnet\\sdk\\*합니다. 일반적으로.NET Core SDK MSI 설치 프로그램을 대신 복사/붙여넣기를 사용 하는 컴퓨터에 배포 된 경우 발생 합니다.

이 경고를 방지 하기 위해 32 비트.NET Core SDK를 제거 합니다. 제거 **제어판** > **프로그램 및 기능** > **제거 또는 변경 프로그램**합니다. 경고의 발생 이유 및 그 의미를 이해 하는 경우 경고를 무시할 수 있습니다.

### <a name="no-net-core-sdks-were-detected"></a>.NET Core Sdk은 찾았습니다.

에 **새 프로젝트** 대화 ASP.NET Core에 대 한 다음과 같은 경고가 표시 될 수 있습니다.

> .NET Core Sdk에서 검색 된 'PATH' 환경 변수에 포함 된를 확인 합니다.

![경고 메시지를 보여 주는 OneASP.NET 대화 상자의 스크린 샷](troubleshoot/_static/NoNetCore.png)

이 경고를 표시 하는 경우 환경 변수 `PATH` 컴퓨터에 모든.NET Core Sdk를 가리키지 않습니다. 이 문제를 해결 방법:

* 설치 또는.NET Core SDK 설치 되었는지 확인 합니다.
* 확인 된 `PATH` 환경 변수는 SDK가 설치 하는 위치를 가리킵니다. 설치 관리자는 일반적으로 설정 된 `PATH`합니다.

::: moniker range=">= aspnetcore-2.1"

### <a name="use-of-ihtmlhelperpartial-may-result-in-app-deadlocks"></a>응용 프로그램 교착 상태에서 IHtmlHelper.Partial 사용 될 수 있습니다.

ASP.NET Core 2.1 이상 버전에서는 호출 `Html.Partial` 교착 상태가 발생할 수 있으므로 분석기 경고를 발생 합니다. 가 경고 메시지:

> 응용 프로그램 교착 상태에서 IHtmlHelper.Partial 사용 될 수 있습니다. 사용 하는 것이 좋습니다 `<partial>` 태그 도우미 또는 `IHtmlHelper.PartialAsync`합니다.

에 대 한 호출이 `@Html.Partial` 으로 대체 해야 `@await Html.PartialAsync` 또는 부분 태그 도우미 `<partial name="_Partial" />`합니다.

::: moniker-end
