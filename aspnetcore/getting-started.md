---
title: "ASP.NET Core 2.0 시작"
author: rick-anderson
description: "ASP.NET Core를 사용하여 간단한 Hello World 앱을 만들고 실행하는 빠른 자습서입니다."
manager: wpickett
ms.author: riande
ms.date: 10/18/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: getting-started
ms.openlocfilehash: eb1fd748029743ca6991927cc95b612ed1975338
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="get-started-with-aspnet-core"></a><span data-ttu-id="f19ff-103">ASP.NET Core 시작</span><span class="sxs-lookup"><span data-stu-id="f19ff-103">Get Started with ASP.NET Core</span></span>

> [!NOTE]
> <span data-ttu-id="f19ff-104">이러한 지침은 최신 버전의 ASP.NET Core에 대한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f19ff-104">These instructions are for the latest version of ASP.NET Core.</span></span> <span data-ttu-id="f19ff-105">이전 버전을 시작하려고 하나요?</span><span class="sxs-lookup"><span data-stu-id="f19ff-105">Looking to get started with an earlier version?</span></span> <span data-ttu-id="f19ff-106">[이 자습서의 1.1 버전](xref:getting-started-1.1)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f19ff-106">See [the 1.1 version of this tutorial](xref:getting-started-1.1).</span></span>

1. <span data-ttu-id="f19ff-107">[.NET Core](https://www.microsoft.com/net/core/)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f19ff-107">Install [.NET Core](https://www.microsoft.com/net/core/).</span></span>

2. <span data-ttu-id="f19ff-108">새 .NET Core 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f19ff-108">Create a new .NET Core project.</span></span>

   <span data-ttu-id="f19ff-109">macOS 및 Linux에서 터미널 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f19ff-109">On macOS and Linux, open a terminal window.</span></span> <span data-ttu-id="f19ff-110">Windows에서 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f19ff-110">On Windows, open a command prompt.</span></span> <span data-ttu-id="f19ff-111">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f19ff-111">Enter the following command:</span></span>

    ```terminal
    dotnet new razor -o aspnetcoreapp
    ```
    
4. <span data-ttu-id="f19ff-112">앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f19ff-112">Run the app.</span></span>

    <span data-ttu-id="f19ff-113">다음 명령을 사용하여 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f19ff-113">Use the following commands to run the app:</span></span>

    ```terminal
    cd aspnetcoreapp
    dotnet run
    ```

5. <span data-ttu-id="f19ff-114">[http://localhost:5000](http://localhost:5000)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f19ff-114">Browse to [http://localhost:5000](http://localhost:5000)</span></span>

6. <span data-ttu-id="f19ff-115">*Pages/About.cshtml* 을 열고 페이지를 수정하여 “Hello, world!</span><span class="sxs-lookup"><span data-stu-id="f19ff-115">Open *Pages/About.cshtml* and modify the page to display the message "Hello, world!</span></span> <span data-ttu-id="f19ff-116">The time on the server is @DateTime.Now.” 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f19ff-116">The time on the server is @DateTime.Now ":</span></span>

    [!code-html[Main](getting-started/sample/getting-started/about.cshtml?highlight=9&range=1-9)]

7. <span data-ttu-id="f19ff-117">[http://localhost:5000/About](http://localhost:5000/About)으로 이동하여 변경 내용을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f19ff-117">Browse to [http://localhost:5000/About](http://localhost:5000/About) and verify the changes.</span></span>

### <a name="next-steps"></a><span data-ttu-id="f19ff-118">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f19ff-118">Next steps</span></span>

<span data-ttu-id="f19ff-119">시작 자습서는 [ASP.NET Core 자습서](tutorials/index.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f19ff-119">For getting-started tutorials, see [ASP.NET Core Tutorials](tutorials/index.md)</span></span>

<span data-ttu-id="f19ff-120">ASP.NET Core 개념 및 아키텍처에 대한 소개는 [ASP.NET Core 소개](index.md) 및 [ASP.NET Core 기본 사항](fundamentals/index.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f19ff-120">For an introduction to ASP.NET Core concepts and architecture, see [ASP.NET Core Introduction](index.md) and [ASP.NET Core Fundamentals](fundamentals/index.md).</span></span>

<span data-ttu-id="f19ff-121">ASP.NET Core 앱은 .NET Core 또는 .NET Framework 기본 클래스 라이브러리 및 런타임을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f19ff-121">An ASP.NET Core app can use the .NET Core or .NET Framework Base Class Library and runtime.</span></span> <span data-ttu-id="f19ff-122">자세한 내용은 [.NET Core와 .NET Framework 중에 선택](https://docs.microsoft.com/dotnet/articles/standard/choosing-core-framework-server)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f19ff-122">For more information, see [Choosing between .NET Core and .NET Framework](https://docs.microsoft.com/dotnet/articles/standard/choosing-core-framework-server).</span></span>
