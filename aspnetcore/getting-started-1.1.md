---
title: ASP.NET Core 1.1 시작
author: rick-anderson
description: 이 빠른 자습서를 따라 ASP.NET Core 1.1을 사용하여 간단한 Hello World 앱을 만들고 실행합니다.
manager: wpickett
ms.author: riande
ms.date: 08/07/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: getting-started-1.1
ms.openlocfilehash: c61a9a918e51bbd6c1f1142a04473393c8fc54ca
ms.sourcegitcommit: 48beecfe749ddac52bc79aa3eb246a2dcdaa1862
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="get-started-with-aspnet-core-11"></a><span data-ttu-id="c56b6-103">ASP.NET Core 1.1 시작</span><span class="sxs-lookup"><span data-stu-id="c56b6-103">Get Started with ASP.NET Core 1.1</span></span>

> [!NOTE]
> <span data-ttu-id="c56b6-104">이러한 지침은 ASP.NET Core 1.1에 대한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c56b6-104">These instructions are for ASP.NET Core 1.1.</span></span> <span data-ttu-id="c56b6-105">최신 버전을 찾고 있나요?</span><span class="sxs-lookup"><span data-stu-id="c56b6-105">Looking for the latest version?</span></span> <span data-ttu-id="c56b6-106">[이 자습서의 현재 버전](xref:getting-started)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c56b6-106">See [the current version of this tutorial](xref:getting-started).</span></span>

1. <span data-ttu-id="c56b6-107">[.NET Core 모든 다운로드 페이지](https://www.microsoft.com/net/download/all)에서 SDK 1.0.4용 .NET Core **SDK 설치 관리자**를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="c56b6-107">Install the .NET Core **SDK Installer** for SDK 1.0.4 from the [.NET Core All Downloads page](https://www.microsoft.com/net/download/all).</span></span>

2. <span data-ttu-id="c56b6-108">새 .NET Core 프로젝트에 대한 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c56b6-108">Create a folder for a new .NET Core project.</span></span>

   <span data-ttu-id="c56b6-109">macOS 및 Linux에서 터미널 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c56b6-109">On macOS and Linux, open a terminal window.</span></span> <span data-ttu-id="c56b6-110">Windows에서 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c56b6-110">On Windows, open a command prompt.</span></span>

   ```terminal
   mkdir aspnetcoreapp
   cd aspnetcoreapp
   ```

2. <span data-ttu-id="c56b6-111">컴퓨터에 최신 SDK 버전을 설치한 경우 *global.json* 파일을 만들어 1.0.4 SDK를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c56b6-111">If you have installed a later SDK version on your machine, create a *global.json* file to select the 1.0.4 SDK.</span></span>

   ```json
   {
     "sdk": { "version": "1.0.4" }
   }
   ```

2. <span data-ttu-id="c56b6-112">새 .NET Core 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c56b6-112">Create a new .NET Core project.</span></span>

   ```terminal
   dotnet new web
   ```
   
3.  <span data-ttu-id="c56b6-113">패키지를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="c56b6-113">Restore the packages.</span></span>

    ```terminal
    dotnet restore
    ```

4. <span data-ttu-id="c56b6-114">앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c56b6-114">Run the app.</span></span>

   <span data-ttu-id="c56b6-115">[dotnet run](/dotnet/core/tools/dotnet-run) 명령은 필요한 경우 앱을 먼저 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="c56b6-115">The [dotnet run](/dotnet/core/tools/dotnet-run) command builds the app first if needed.</span></span>

   ```terminal
   dotnet run
   ```

5. <span data-ttu-id="c56b6-116">`http://localhost:5000`으로 이동</span><span class="sxs-lookup"><span data-stu-id="c56b6-116">Browse to `http://localhost:5000`</span></span>

<!-- H3 to avoid a single-entry internal TOC -->
### <a name="next-steps"></a><span data-ttu-id="c56b6-117">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c56b6-117">Next steps</span></span>

<span data-ttu-id="c56b6-118">시작 자습서는 [ASP.NET Core 자습서](tutorials/index.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c56b6-118">For getting-started tutorials, see [ASP.NET Core Tutorials](tutorials/index.md)</span></span>

<span data-ttu-id="c56b6-119">ASP.NET Core 개념 및 아키텍처에 대한 소개는 [ASP.NET Core 소개](index.md) 및 [ASP.NET Core 기본 사항](fundamentals/index.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c56b6-119">For an introduction to ASP.NET Core concepts and architecture, see [ASP.NET Core Introduction](index.md) and [ASP.NET Core Fundamentals](fundamentals/index.md).</span></span>

<span data-ttu-id="c56b6-120">ASP.NET Core 앱은 .NET Core 또는 .NET Framework 기본 클래스 라이브러리 및 런타임을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c56b6-120">An ASP.NET Core app can use the .NET Core or .NET Framework Base Class Library and runtime.</span></span> <span data-ttu-id="c56b6-121">자세한 내용은 [.NET Core와 .NET Framework 중에 선택](https://docs.microsoft.com/dotnet/articles/standard/choosing-core-framework-server)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c56b6-121">For more information, see [Choosing between .NET Core and .NET Framework](https://docs.microsoft.com/dotnet/articles/standard/choosing-core-framework-server).</span></span>
