---
title: "ASP.NET Core 2.x 이상용 Microsoft.AspNetCore.All 메타패키지"
author: Rick-Anderson
description: "Microsoft.AspNetCore.All 메타패키지에는 지원되는 모든 ASP.NET Core 및 Entity Framework Core 패키지와 해당 종속성이 포함됩니다."
manager: wpickett
ms.author: riande
ms.date: 09/20/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/metapackage
ms.openlocfilehash: 07220fdae299723088fa85e452cedff5e5685bd7
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
#<a name="microsoftaspnetcoreall-metapackage-for-aspnet-core-2x"></a><span data-ttu-id="c7051-103">ASP.NET Core 2.x용 Microsoft.AspNetCore.All 메타패키지</span><span class="sxs-lookup"><span data-stu-id="c7051-103">Microsoft.AspNetCore.All metapackage for ASP.NET Core 2.x</span></span>

<span data-ttu-id="c7051-104">이 기능을 사용하려면 .NET Core 2.x를 대상으로 하는 ASP.NET Core 2.x가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c7051-104">This feature requires ASP.NET Core 2.x targeting .NET Core 2.x.</span></span>

<span data-ttu-id="c7051-105">ASP.NET Core에 대한 [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) 메타패키지는 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c7051-105">The [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) metapackage for ASP.NET Core includes:</span></span>

* <span data-ttu-id="c7051-106">ASP.NET Core 팀에서 지원되는 모든 패키지</span><span class="sxs-lookup"><span data-stu-id="c7051-106">All supported packages by the ASP.NET Core team.</span></span>
* <span data-ttu-id="c7051-107">Entity Framework Core에서 지원되는 모든 패키지</span><span class="sxs-lookup"><span data-stu-id="c7051-107">All supported packages by the Entity Framework Core.</span></span> 
* <span data-ttu-id="c7051-108">ASP.NET Core 및 Entity Framework Core에서 사용하는 내부 및 타사 종속성</span><span class="sxs-lookup"><span data-stu-id="c7051-108">Internal and 3rd-party dependencies used by ASP.NET Core and Entity Framework Core.</span></span> 

<span data-ttu-id="c7051-109">ASP.NET Core 2.x 및 Entity Framework Core 2.x의 모든 기능은 `Microsoft.AspNetCore.All` 패키지에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7051-109">All the features of ASP.NET Core 2.x and Entity Framework Core 2.x are included in the `Microsoft.AspNetCore.All` package.</span></span> <span data-ttu-id="c7051-110">기본 프로젝트 템플릿은 이 패키지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c7051-110">The default project templates use this package.</span></span>

<span data-ttu-id="c7051-111">`Microsoft.AspNetCore.All` 메타패키지의 버전 번호는 ASP.NET Core 버전 및 Entity Framework Core 버전(.NET Core 버전에 맞게 조정)을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c7051-111">The version number of the `Microsoft.AspNetCore.All` metapackage represents the ASP.NET Core version and Entity Framework Core version (aligned with the .NET Core version).</span></span>

<span data-ttu-id="c7051-112">`Microsoft.AspNetCore.All` 메타패키지를 사용하는 응용 프로그램은 [.NET Core 런타임 저장소](https://docs.microsoft.com/dotnet/core/deploying/runtime-store)를 자동으로 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="c7051-112">Applications that use the `Microsoft.AspNetCore.All` metapackage automatically take advantage of the [.NET Core Runtime Store](https://docs.microsoft.com/dotnet/core/deploying/runtime-store).</span></span> <span data-ttu-id="c7051-113">런타임 저장소에는 ASP.NET Core 2.x 응용 프로그램을 실행하는 데 필요한 모든 런타임 자산이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7051-113">The Runtime Store contains all the runtime assets needed to run ASP.NET Core 2.x applications.</span></span> <span data-ttu-id="c7051-114">`Microsoft.AspNetCore.All` 메타패키지를 사용할 경우, 참조되는 ASP.NET Core NuGet 패키지의 자산이 응용 프로그램을 사용하여 배포되지 **않습니다**. 이러한 자산은 &mdash; .NET Core 런타임 저장소에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7051-114">When you use the `Microsoft.AspNetCore.All` metapackage, **no** assets from the referenced ASP.NET Core NuGet packages are deployed with the application &mdash; the .NET Core Runtime Store contains these assets.</span></span> <span data-ttu-id="c7051-115">런타임 저장소의 자산은 응용 프로그램 시작 시간 단축을 위해 미리 컴파일됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7051-115">The assets in the Runtime Store are precompiled to improve application startup time.</span></span>

<span data-ttu-id="c7051-116">패키지 트리밍 프로세스를 이용하여 사용하지 않는 패키지를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7051-116">You can use the package trimming process to remove packages that you don't use.</span></span> <span data-ttu-id="c7051-117">트리밍된 패키지는 게시된 응용 프로그램 출력에서 제외됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7051-117">Trimmed packages are excluded in published application output.</span></span>

<span data-ttu-id="c7051-118">다음 *.csproj* 파일은 ASP.NET Core용 `Microsoft.AspNetCore.All` 메타패키지를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="c7051-118">The following *.csproj* file references the `Microsoft.AspNetCore.All` metapackage for ASP.NET Core:</span></span>

[!code-xml[Main](..\mvc\views\view-compilation\sample\MvcRazorCompileOnPublish2.csproj?highlight=9)]
