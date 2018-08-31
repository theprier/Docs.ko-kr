---
uid: visual-studio/overview/2017/optimize-build-perf
title: 솔루션에 대 한 빌드 성능 최적화
author: AngelosP
description: 솔루션에 대 한 빌드 성능 최적화
ms.author: riande
ms.date: 08/29/2018
msc.type: authoredcontent
ms.openlocfilehash: c1a5cf5e59374b4c0dd7150c5dd62fbde42af555
ms.sourcegitcommit: ecf2cd4e0613569025b28e12de3baa21d86d4258
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43312143"
---
# <a name="optimize-build-performance-for-solution"></a><span data-ttu-id="66620-103">솔루션에 대 한 빌드 성능 최적화</span><span class="sxs-lookup"><span data-stu-id="66620-103">Optimize build performance for solution</span></span>

<span data-ttu-id="66620-104">Visual Studio 2017 15.8 또는 나중에 메뉴 항목을 포함 합니다. **빌드** > **ASP.NET 컴파일** > **솔루션에 대 한 빌드 성능 최적화**합니다.</span><span class="sxs-lookup"><span data-stu-id="66620-104">Visual Studio 2017 15.8 or later include a menu item: **Build** > **ASP.NET Compilation** > **Optimize Build Performance for Solution**.</span></span>

![새 메뉴 항목의 스크린샷](optimize-build-perf/_static/optimize-build-performance-for-solution.png)

<span data-ttu-id="66620-106">ASP.NET에서는 ASP.NET 프로젝트는 컴파일러의 복사본에 저마다 독특한 즉 런타임에 해당 뷰를 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="66620-106">ASP.NET compiles its views at runtime, which means that an ASP.NET project carries with it a copy of the compiler.</span></span> <span data-ttu-id="66620-107">그러나 개발자 컴퓨터에서 컴파일러의 복사본에는 Visual Studio의 복사본과 일치 하지 않습니다 하는 경우 빌드 성능이 저하 됩니다 증분 빌드 1 ~ 3 초 순서.</span><span class="sxs-lookup"><span data-stu-id="66620-107">However on a developer machine when the copy of the compiler doesn't match Visual Studio's copy, build performance is impacted on the order of 1-3 seconds per incremental build.</span></span> <span data-ttu-id="66620-108">이 기능은 일반적으로 증분 빌드 속도의 Visual Studio와 일치 하도록 컴파일러에 프로젝트의 복사본을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="66620-108">This feature updates your project's copy of the compiler to match Visual Studio's, which usually speeds up incremental builds.</span></span>

<span data-ttu-id="66620-109">**이 Asp.net 4.7.1 적용할 또는 나중에 프로젝트에 해당, ASP.NET Core에 적용 되지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="66620-109">**This is applicable to ASP.NET Framework 4.7.1 or later projects only, it does not apply to ASP.NET Core.**</span></span>
