---
title: ASP.NET Core 2.0 이상용 Microsoft.AspNetCore.All 메타패키지
author: Rick-Anderson
description: Microsoft.AspNetCore.All 메타패키지에는 지원되는 모든 ASP.NET Core 및 Entity Framework Core 패키지와 해당 종속성이 포함됩니다.
manager: wpickett
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.date: 09/20/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/metapackage
ms.openlocfilehash: c0d7d7fb5f41a91f8d881dd7880d8adcaa478968
ms.sourcegitcommit: 24c32648ab0c6f0be15333d7c23c1bf680858c43
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/20/2018
---
# <a name="microsoftaspnetcoreall-metapackage-for-aspnet-core-20"></a>ASP.NET Core 2.0용 Microsoft.AspNetCore.All 메타패키지

> [!NOTE]
> ASP.NET Core 2.1 이상을 대상으로 하는 응용 프로그램은 이 패키지가 아닌 [Microsoft.AspNetCore.App](xref:fundamentals/metapackage)을 사용하는 것이 좋습니다. 이 문서의 [Microsoft.AspNetCore.All에서 Microsoft.AspNetCore.App으로 마이그레이션](#migrate)을 참조하세요.

이 기능을 사용하려면 .NET Core 2.x를 대상으로 하는 ASP.NET Core 2.x가 필요합니다.

ASP.NET Core에 대한 [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) 메타패키지에는 다음 패키지들이 포함되어 있습니다.

* ASP.NET Core 팀에서 지원되는 모든 패키지
* Entity Framework Core에서 지원되는 모든 패키지 
* ASP.NET Core 및 Entity Framework Core에서 사용되는 내부 및 타사 종속성 

ASP.NET Core 2.x 및 Entity Framework Core 2.x의 모든 기능은 `Microsoft.AspNetCore.All` 패키지에 포함됩니다. ASP.NET Core 2.0을 대상으로 하는 기본 프로젝트 템플릿에는 이 패키지를 사용합니다.

`Microsoft.AspNetCore.All` 메타패키지의 버전 번호는 ASP.NET Core 버전 및 Entity Framework Core 버전을 나타냅니다.

`Microsoft.AspNetCore.All` 메타패키지를 사용하는 응용 프로그램은 [.NET Core 런타임 저장소](https://docs.microsoft.com/dotnet/core/deploying/runtime-store)를 자동으로 활용합니다. 런타임 저장소에는 ASP.NET Core 2.x 응용 프로그램을 실행하는 데 필요한 모든 런타임 자산이 포함됩니다. `Microsoft.AspNetCore.All` 메타패키지를 사용할 경우, 참조되는 ASP.NET Core NuGet 패키지의 자산이 응용 프로그램을 사용하여 배포되지 **않습니다**. 이러한 자산은 &mdash; .NET Core 런타임 저장소에 포함됩니다. 런타임 저장소의 자산은 응용 프로그램 시작 시간 단축을 위해 미리 컴파일됩니다.

패키지 트리밍 프로세스를 이용하여 사용하지 않는 패키지를 제거할 수 있습니다. 트리밍된 패키지는 게시된 응용 프로그램 출력에서 제외됩니다.

다음 *.csproj* 파일은 ASP.NET Core용 `Microsoft.AspNetCore.All` 메타패키지를 참조합니다.

[!code-xml[](metapackage/samples/Metapackage.All.Example.csproj?highlight=6)]

<a name="migrate"></a>
## <a name="migrating-from-microsoftaspnetcoreall-to-microsoftaspnetcoreapp"></a>Microsoft.AspNetCore.All에서 Microsoft.AspNetCore.App으로 마이그레이션

`Microsoft.AspNetCore.All`에는 다음 패키지가 포함되어 있지만 `Microsoft.AspNetCore.App` 패키지는 포함되어 있지 않습니다. 

* `Microsoft.AspNetCore.ApplicationInsights.HostingStartup`
* `Microsoft.AspNetCore.AzureAppServices.HostingStartup`
* `Microsoft.AspNetCore.AzureAppServicesIntegration`
* `Microsoft.AspNetCore.DataProtection.AzureKeyVault`
* `Microsoft.AspNetCore.DataProtection.AzureStorage`
* `Microsoft.AspNetCore.Server.Kestrel.Transport.Libuv`
* `Microsoft.AspNetCore.SignalR.Redis`
* `Microsoft.Data.Sqlite`
* `Microsoft.Data.Sqlite.Core`
* `Microsoft.EntityFrameworkCore.Sqlite`
* `Microsoft.EntityFrameworkCore.Sqlite.Core`
* `Microsoft.Extensions.Caching.Redis`
* `Microsoft.Extensions.Configuration.AzureKeyVault`
* `Microsoft.Extensions.Logging.AzureAppServices`
* `Microsoft.VisualStudio.Web.BrowserLink`

앱이 이전 패키지 또는 이러한 패키지에서 가져온 패키지의 API를 사용하는 경우 `Microsoft.AspNetCore.All`에서 `Microsoft.AspNetCore.App`으로 전환하려면 프로젝트에 이러한 패키지에 대한 참조를 추가합니다.

`Microsoft.AspNetCore.App`의 종속성이 아닌 이전 패키지의 종속성은 암시적으로 포함되지 않습니다. 예:

* `Microsoft.Extensions.Caching.Redis`의 종속성 `StackExchange.Redis`
* `Microsoft.AspNetCore.ApplicationInsights.HostingStartup`의 종속성 `Microsoft.ApplicationInsights`