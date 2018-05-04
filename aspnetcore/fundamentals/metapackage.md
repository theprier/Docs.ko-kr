---
title: ASP.NET Core 2.x 이상용 Microsoft.AspNetCore.All 메타패키지
author: Rick-Anderson
description: Microsoft.AspNetCore.All 메타패키지에는 지원되는 모든 ASP.NET Core 및 Entity Framework Core 패키지와 해당 종속성이 포함됩니다.
manager: wpickett
monikerRange: = aspnetcore-2.0
ms.author: riande
ms.date: 09/20/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/metapackage
ms.openlocfilehash: 4c11f15e659565325bfe8b8d91188b62177b251d
ms.sourcegitcommit: c79fd3592f444d58e17518914f8873d0a11219c0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="microsoftaspnetcoreall-metapackage-for-aspnet-core-2x"></a>ASP.NET Core 2.x용 Microsoft.AspNetCore.All 메타패키지

이 기능을 사용하려면 .NET Core 2.x를 대상으로 하는 ASP.NET Core 2.x가 필요합니다.

ASP.NET Core에 대한 [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) 메타패키지에는 다음 패키지들이 포함되어 있습니다.

* ASP.NET Core 팀에서 지원되는 모든 패키지
* Entity Framework Core에서 지원되는 모든 패키지 
* ASP.NET Core 및 Entity Framework Core에서 사용되는 내부 및 타사 종속성 

ASP.NET Core 2.x 및 Entity Framework Core 2.x의 모든 기능은 `Microsoft.AspNetCore.All` 패키지에 포함됩니다. ASP.NET Core 2.0을 대상으로 하는 기본 프로젝트 템플릿에는 이 패키지를 사용합니다.

`Microsoft.AspNetCore.All` 메타패키지의 버전 번호는 ASP.NET Core 버전 및 Entity Framework Core 버전(.NET Core 버전에 맞게 조정)을 나타냅니다.

`Microsoft.AspNetCore.All` 메타패키지를 사용하는 응용 프로그램은 [.NET Core 런타임 저장소](https://docs.microsoft.com/dotnet/core/deploying/runtime-store)를 자동으로 활용합니다. 런타임 저장소에는 ASP.NET Core 2.x 응용 프로그램을 실행하는 데 필요한 모든 런타임 자산이 포함됩니다. `Microsoft.AspNetCore.All` 메타패키지를 사용할 경우, 참조되는 ASP.NET Core NuGet 패키지의 자산이 응용 프로그램을 사용하여 배포되지 **않습니다**. 이러한 자산은 &mdash; .NET Core 런타임 저장소에 포함됩니다. 런타임 저장소의 자산은 응용 프로그램 시작 시간 단축을 위해 미리 컴파일됩니다.

패키지 트리밍 프로세스를 이용하여 사용하지 않는 패키지를 제거할 수 있습니다. 트리밍된 패키지는 게시된 응용 프로그램 출력에서 제외됩니다.

다음 *.csproj* 파일은 ASP.NET Core용 `Microsoft.AspNetCore.All` 메타패키지를 참조합니다.

[!code-xml[](../mvc/views/view-compilation/sample/MvcRazorCompileOnPublish2.csproj?highlight=9)]
