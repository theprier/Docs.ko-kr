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
ms.openlocfilehash: fbb76f41f3178ddc4e51faa14edece1869a30cd0
ms.sourcegitcommit: 43bd79667bbdc8a07bd39fb4cd6f7ad3e70212fb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34729079"
---
# <a name="microsoftaspnetcoreall-metapackage-for-aspnet-core-20"></a><span data-ttu-id="5f367-103">ASP.NET Core 2.0용 Microsoft.AspNetCore.All 메타패키지</span><span class="sxs-lookup"><span data-stu-id="5f367-103">Microsoft.AspNetCore.All metapackage for ASP.NET Core 2.0</span></span>

> [!NOTE]
> <span data-ttu-id="5f367-104">ASP.NET Core 2.1 이상을 대상으로 하는 응용 프로그램은 이 패키지가 아닌 [Microsoft.AspNetCore.App](xref:fundamentals/metapackage-app)을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5f367-104">We recommend applications targeting ASP.NET Core 2.1 and later use the [Microsoft.AspNetCore.App](xref:fundamentals/metapackage-app) rather than this package.</span></span> <span data-ttu-id="5f367-105">이 문서의 [Microsoft.AspNetCore.All에서 Microsoft.AspNetCore.App으로 마이그레이션](#migrate)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5f367-105">See [Migrating from Microsoft.AspNetCore.All to Microsoft.AspNetCore.App](#migrate) in this article.</span></span>

<span data-ttu-id="5f367-106">이 기능을 사용하려면 .NET Core 2.x를 대상으로 하는 ASP.NET Core 2.x가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5f367-106">This feature requires ASP.NET Core 2.x targeting .NET Core 2.x.</span></span>

<span data-ttu-id="5f367-107">ASP.NET Core에 대한 [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) 메타패키지에는 다음 패키지들이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f367-107">The [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) metapackage for ASP.NET Core includes:</span></span>

* <span data-ttu-id="5f367-108">ASP.NET Core 팀에서 지원되는 모든 패키지</span><span class="sxs-lookup"><span data-stu-id="5f367-108">All supported packages by the ASP.NET Core team.</span></span>
* <span data-ttu-id="5f367-109">Entity Framework Core에서 지원되는 모든 패키지</span><span class="sxs-lookup"><span data-stu-id="5f367-109">All supported packages by the Entity Framework Core.</span></span> 
* <span data-ttu-id="5f367-110">ASP.NET Core 및 Entity Framework Core에서 사용되는 내부 및 타사 종속성</span><span class="sxs-lookup"><span data-stu-id="5f367-110">Internal and 3rd-party dependencies used by ASP.NET Core and Entity Framework Core.</span></span> 

<span data-ttu-id="5f367-111">ASP.NET Core 2.x 및 Entity Framework Core 2.x의 모든 기능은 `Microsoft.AspNetCore.All` 패키지에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f367-111">All the features of ASP.NET Core 2.x and Entity Framework Core 2.x are included in the `Microsoft.AspNetCore.All` package.</span></span> <span data-ttu-id="5f367-112">ASP.NET Core 2.0을 대상으로 하는 기본 프로젝트 템플릿에는 이 패키지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5f367-112">The default project templates targeting ASP.NET Core 2.0 use this package.</span></span>

<span data-ttu-id="5f367-113">`Microsoft.AspNetCore.All` 메타패키지의 버전 번호는 ASP.NET Core 버전 및 Entity Framework Core 버전을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5f367-113">The version number of the `Microsoft.AspNetCore.All` metapackage represents the ASP.NET Core version and Entity Framework Core version.</span></span>

<span data-ttu-id="5f367-114">`Microsoft.AspNetCore.All` 메타패키지를 사용하는 응용 프로그램은 [.NET Core 런타임 저장소](https://docs.microsoft.com/dotnet/core/deploying/runtime-store)를 자동으로 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="5f367-114">Applications that use the `Microsoft.AspNetCore.All` metapackage automatically take advantage of the [.NET Core Runtime Store](https://docs.microsoft.com/dotnet/core/deploying/runtime-store).</span></span> <span data-ttu-id="5f367-115">런타임 저장소에는 ASP.NET Core 2.x 응용 프로그램을 실행하는 데 필요한 모든 런타임 자산이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f367-115">The Runtime Store contains all the runtime assets needed to run ASP.NET Core 2.x applications.</span></span> <span data-ttu-id="5f367-116">`Microsoft.AspNetCore.All` 메타패키지를 사용할 경우, 참조되는 ASP.NET Core NuGet 패키지의 자산이 응용 프로그램을 사용하여 배포되지 **않습니다**. 이러한 자산은 &mdash; .NET Core 런타임 저장소에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f367-116">When you use the `Microsoft.AspNetCore.All` metapackage, **no** assets from the referenced ASP.NET Core NuGet packages are deployed with the application &mdash; the .NET Core Runtime Store contains these assets.</span></span> <span data-ttu-id="5f367-117">런타임 저장소의 자산은 응용 프로그램 시작 시간 단축을 위해 미리 컴파일됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f367-117">The assets in the Runtime Store are precompiled to improve application startup time.</span></span>

<span data-ttu-id="5f367-118">패키지 트리밍 프로세스를 이용하여 사용하지 않는 패키지를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f367-118">You can use the package trimming process to remove packages that you don't use.</span></span> <span data-ttu-id="5f367-119">트리밍된 패키지는 게시된 응용 프로그램 출력에서 제외됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f367-119">Trimmed packages are excluded in published application output.</span></span>

<span data-ttu-id="5f367-120">다음 *.csproj* 파일은 ASP.NET Core용 `Microsoft.AspNetCore.All` 메타패키지를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="5f367-120">The following *.csproj* file references the `Microsoft.AspNetCore.All` metapackage for ASP.NET Core:</span></span>

[!code-xml[](metapackage/samples/Metapackage.All.Example.csproj?highlight=6)]

<a name="migrate"></a>
## <a name="migrating-from-microsoftaspnetcoreall-to-microsoftaspnetcoreapp"></a><span data-ttu-id="5f367-121">Microsoft.AspNetCore.All에서 Microsoft.AspNetCore.App으로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="5f367-121">Migrating from Microsoft.AspNetCore.All to Microsoft.AspNetCore.App</span></span>

<span data-ttu-id="5f367-122">`Microsoft.AspNetCore.All`에는 다음 패키지가 포함되어 있지만 `Microsoft.AspNetCore.App` 패키지는 포함되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5f367-122">The following packages are included in `Microsoft.AspNetCore.All` but not the `Microsoft.AspNetCore.App` package.</span></span> 

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

<span data-ttu-id="5f367-123">앱이 이전 패키지 또는 이러한 패키지에서 가져온 패키지의 API를 사용하는 경우 `Microsoft.AspNetCore.All`에서 `Microsoft.AspNetCore.App`으로 전환하려면 프로젝트에 이러한 패키지에 대한 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5f367-123">To move from `Microsoft.AspNetCore.All` to `Microsoft.AspNetCore.App`, if your app uses any APIs from the above packages, or packages brought in by those packages, add references to those packages in your project.</span></span>

<span data-ttu-id="5f367-124">`Microsoft.AspNetCore.App`의 종속성이 아닌 이전 패키지의 종속성은 암시적으로 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5f367-124">Any dependencies of the preceding packages that otherwise aren't dependencies of `Microsoft.AspNetCore.App` are not included implicitly.</span></span> <span data-ttu-id="5f367-125">예:</span><span class="sxs-lookup"><span data-stu-id="5f367-125">For example:</span></span>

* <span data-ttu-id="5f367-126">`Microsoft.Extensions.Caching.Redis`의 종속성 `StackExchange.Redis`</span><span class="sxs-lookup"><span data-stu-id="5f367-126">`StackExchange.Redis` as a dependency of `Microsoft.Extensions.Caching.Redis`</span></span>
* <span data-ttu-id="5f367-127">`Microsoft.AspNetCore.ApplicationInsights.HostingStartup`의 종속성 `Microsoft.ApplicationInsights`</span><span class="sxs-lookup"><span data-stu-id="5f367-127">`Microsoft.ApplicationInsights` as a dependency of `Microsoft.AspNetCore.ApplicationInsights.HostingStartup`</span></span>
