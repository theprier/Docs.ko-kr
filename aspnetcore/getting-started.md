---
title: ASP.NET Core 시작
author: rick-anderson
description: ASP.NET Core를 사용하여 간단한 Hello World 앱을 만들고 실행하는 빠른 자습서입니다.
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 05/10/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: getting-started
ms.openlocfilehash: e814277663ff5a964171a71ebb6e0f094e0ddc60
ms.sourcegitcommit: 3d071fabaf90e32906df97b08a8d00e602db25c0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="get-started-with-aspnet-core"></a><span data-ttu-id="cee85-103">ASP.NET Core 시작</span><span class="sxs-lookup"><span data-stu-id="cee85-103">Get started with ASP.NET Core</span></span>

::: moniker range=">= aspnetcore-2.0"

1. <span data-ttu-id="cee85-104">[!INCLUDE[](~/includes/net-core-sdk-download-link.md)]를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="cee85-104">Install the [!INCLUDE[](~/includes/net-core-sdk-download-link.md)].</span></span>

2. <span data-ttu-id="cee85-105">새 .NET Core 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cee85-105">Create a new .NET Core project.</span></span>

   <span data-ttu-id="cee85-106">macOS 및 Linux에서 터미널 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cee85-106">On macOS and Linux, open a terminal window.</span></span> <span data-ttu-id="cee85-107">Windows에서 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cee85-107">On Windows, open a command prompt.</span></span> <span data-ttu-id="cee85-108">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cee85-108">Enter the following command:</span></span>

    ```terminal
    dotnet new razor -o aspnetcoreapp
    ```

3. <span data-ttu-id="cee85-109">다음 명령을 사용하여 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cee85-109">Run the app with the following commands:</span></span>

    ```terminal
    cd aspnetcoreapp
    dotnet run
    ```

4. <span data-ttu-id="cee85-110">[http://localhost:5000](http://localhost:5000)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="cee85-110">Browse to [http://localhost:5000](http://localhost:5000).</span></span>

5. <span data-ttu-id="cee85-111">*Pages/About.cshtml* 을 열고 페이지를 수정하여 “Hello, world!</span><span class="sxs-lookup"><span data-stu-id="cee85-111">Open *Pages/About.cshtml* and modify the page to display the message "Hello, world!</span></span> <span data-ttu-id="cee85-112">서버 시간은 @DateTime.Now입니다.” 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="cee85-112">The time on the server is @DateTime.Now":</span></span>

    <span data-ttu-id="cee85-113">[!code-cshtml[](getting-started/sample/getting-started/about.cshtml?highlight=9&range=1-9)]</span><span class="sxs-lookup"><span data-stu-id="cee85-113">[!code-cshtml[](getting-started/sample/getting-started/about.cshtml?highlight=9&range=1-9)]</span></span>

6. <span data-ttu-id="cee85-114">[http://localhost:5000/About](http://localhost:5000/About)으로 이동하여 변경 내용을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cee85-114">Browse to [http://localhost:5000/About](http://localhost:5000/About) and verify the changes.</span></span>

[!INCLUDE[next steps](~/includes/getting-started/next-steps.md)]
::: moniker-end

::: moniker range="<= aspnetcore-1.1"

1. <span data-ttu-id="cee85-115">[.NET Core 모든 다운로드 페이지](https://www.microsoft.com/net/download/all)에서 SDK 1.0.4용 .NET Core **SDK 설치 관리자**를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="cee85-115">Install the .NET Core **SDK Installer** for SDK 1.0.4 from the [.NET Core All Downloads page](https://www.microsoft.com/net/download/all).</span></span>

2. <span data-ttu-id="cee85-116">새 .NET Core 프로젝트에 대한 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cee85-116">Create a folder for a new .NET Core project.</span></span>

   <span data-ttu-id="cee85-117">macOS 및 Linux에서 터미널 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cee85-117">On macOS and Linux, open a terminal window.</span></span> <span data-ttu-id="cee85-118">Windows에서 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cee85-118">On Windows, open a command prompt.</span></span>

   ```terminal
   mkdir aspnetcoreapp
   cd aspnetcoreapp
   ```

3. <span data-ttu-id="cee85-119">컴퓨터에 최신 SDK 버전을 설치한 경우 *global.json* 파일을 만들어 1.0.4 SDK를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cee85-119">If you have installed a later SDK version on your machine, create a *global.json* file to select the 1.0.4 SDK.</span></span>

   ```json
   {
     "sdk": { "version": "1.0.4" }
   }
   ```

4. <span data-ttu-id="cee85-120">새 .NET Core 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cee85-120">Create a new .NET Core project.</span></span>

   ```terminal
   dotnet new web
   ```

5. <span data-ttu-id="cee85-121">패키지를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="cee85-121">Restore the packages.</span></span>

    ```terminal
    dotnet restore
    ```

6. <span data-ttu-id="cee85-122">앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cee85-122">Run the app.</span></span>

   ```terminal
   dotnet run
   ```

   <span data-ttu-id="cee85-123">[dotnet run](/dotnet/core/tools/dotnet-run) 명령은 필요한 경우 앱을 먼저 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="cee85-123">The [dotnet run](/dotnet/core/tools/dotnet-run) command builds the app first, if needed.</span></span>

7. <span data-ttu-id="cee85-124">`http://localhost:5000`으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="cee85-124">Browse to `http://localhost:5000`.</span></span>

[!INCLUDE[next steps](~/includes/getting-started/next-steps.md)]
::: moniker-end