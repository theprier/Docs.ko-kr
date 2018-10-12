---
title: ASP.NET Core 시작
author: rick-anderson
description: ASP.NET Core를 사용하여 간단한 Hello World 앱을 만들고 실행하는 빠른 자습서입니다.
ms.author: riande
ms.custom: mvc
ms.date: 05/31/2018
uid: getting-started
ms.openlocfilehash: a6a5023594aec01370143e7d1f35fb45c109122a
ms.sourcegitcommit: 13940eb53c68664b11a2d685ee17c78faab1945d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47860942"
---
# <a name="get-started-with-aspnet-core"></a><span data-ttu-id="33819-103">ASP.NET Core 시작</span><span class="sxs-lookup"><span data-stu-id="33819-103">Get started with ASP.NET Core</span></span>

<span data-ttu-id="33819-104">이 문서에서는 ASP.NET Core 앱을 만들고 실행하는 단계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="33819-104">This document provides steps for creating and running an ASP.NET Core app.</span></span>

::: moniker range=">= aspnetcore-2.1"

1. <span data-ttu-id="33819-105">[!INCLUDE [](~/includes/2.1-SDK.md)]를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="33819-105">Install the [!INCLUDE [](~/includes/2.1-SDK.md)].</span></span>

2. <span data-ttu-id="33819-106">ASP.NET Core 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33819-106">Create an ASP.NET Core project.</span></span> <span data-ttu-id="33819-107">명령 셸을 열고 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="33819-107">Open a command shell and enter the following command:</span></span>

   ```console
   dotnet new webapp -o aspnetcoreapp
   ```

3. <span data-ttu-id="33819-108">HTTPS 개발 인증서 신뢰:</span><span class="sxs-lookup"><span data-stu-id="33819-108">Trust the HTTPS development certificate:</span></span>

# <a name="windowstabwindows"></a>[<span data-ttu-id="33819-109">Windows</span><span class="sxs-lookup"><span data-stu-id="33819-109">Windows</span></span>](#tab/windows)

  ```console
  dotnet dev-certs https --trust
  ```

  <span data-ttu-id="33819-110">이전 명령으로 인해 다음 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="33819-110">The preceding command displays the following dialog:</span></span>

  ![보안 경고 대화 상자](_static/cert.png)

  <span data-ttu-id="33819-112">개발 인증서를 신뢰하는 데 동의하는 경우 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33819-112">Select **Yes** if you agree to trust the development certificate.</span></span>

# <a name="macostabmacos"></a>[<span data-ttu-id="33819-113">macOS</span><span class="sxs-lookup"><span data-stu-id="33819-113">macOS</span></span>](#tab/macos)

  ```console
  dotnet dev-certs https --trust
  ```

  <span data-ttu-id="33819-114">이전 명령으로 인해 다음 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="33819-114">The preceding command displays the following message:</span></span>

  <span data-ttu-id="33819-115">*HTTPS 개발 인증서를 신뢰해야 합니다. 인증서를 신뢰할 수 없는 경우*  `'sudo security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.keychain <<certificate>>'` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="33819-115">*Trusting the HTTPS development certificate was requested. If the certificate is not already trusted we will run the following command:* `'sudo security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.keychain <<certificate>>'`.</span></span>  
  <span data-ttu-id="33819-116">\*이 명령은 시스템 키 집합에 인증서를 설치하기 위해 암호를 묻는 메시지를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33819-116">\*This command might prompt you for your password to install the certificate on the system keychain.</span></span>
  
  <span data-ttu-id="33819-117">암호:\*</span><span class="sxs-lookup"><span data-stu-id="33819-117">Password:\*</span></span>

  <span data-ttu-id="33819-118">개발 인증서를 신뢰하는 데 동의하는 경우 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="33819-118">Enter your password if you agree to trust the development certificate.</span></span>

# <a name="linuxtablinux"></a>[<span data-ttu-id="33819-119">Linux</span><span class="sxs-lookup"><span data-stu-id="33819-119">Linux</span></span>](#tab/linux)

  <span data-ttu-id="33819-120">HTTPS 개발 인증서를 신뢰하는 방법은 Linux 배포에 대한 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="33819-120">See the documentation for your Linux distribution on how to trust the HTTPS development certificate.</span></span>
   
---

4. <span data-ttu-id="33819-121">앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="33819-121">Run the app:</span></span>

   ```console
   cd aspnetcoreapp
   dotnet run
   ```

5. <span data-ttu-id="33819-122">[http://localhost:5001](http://localhost:5001)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="33819-122">Browse to [http://localhost:5001](http://localhost:5001).</span></span>  <span data-ttu-id="33819-123">**동의**를 클릭하여 개인 정보 및 쿠키 정책에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="33819-123">Click **Accept** to accept the privacy and cookie policy.</span></span> <span data-ttu-id="33819-124">이 앱은 개인 정보를 보관하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="33819-124">This app doesn't keep personal information.</span></span>

6. <span data-ttu-id="33819-125">*Pages/About.cshtml*을 열고 다음과 같은 강조 표시된 태그로 페이지를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="33819-125">Open *Pages/About.cshtml* and modify the page with the following highlighted markup:</span></span>

   [!code-cshtml[](sample/getting-started/about.cshtml?highlight=9)]

7. <span data-ttu-id="33819-126">[http://localhost:5001/About](http://localhost:5001/About)으로 이동하여 변경 내용이 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="33819-126">Browse to [http://localhost:5001/About](http://localhost:5001/About) and verify the changes are displayed.</span></span>

[!INCLUDE [next steps](~/includes/getting-started/next-steps.md)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

1. <span data-ttu-id="33819-127">[!INCLUDE [](~/includes/net-core-sdk-download-link.md)]를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="33819-127">Install the [!INCLUDE [](~/includes/net-core-sdk-download-link.md)].</span></span>

2. <span data-ttu-id="33819-128">새 ASP.NET Core 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33819-128">Create a new ASP.NET Core project.</span></span>

   <span data-ttu-id="33819-129">명령 셸을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="33819-129">Open a command shell.</span></span> <span data-ttu-id="33819-130">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="33819-130">Enter the following command:</span></span>

   ```console
   dotnet new razor -o aspnetcoreapp
   ```

3. <span data-ttu-id="33819-131">다음 명령을 사용하여 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="33819-131">Run the app with the following commands:</span></span>

   ```console
   cd aspnetcoreapp
   dotnet run
   ```

4. <span data-ttu-id="33819-132">[http://localhost:5000](http://localhost:5000)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="33819-132">Browse to [http://localhost:5000](http://localhost:5000).</span></span>

5. <span data-ttu-id="33819-133">*Pages/About.cshtml* 을 열고 페이지를 수정하여 “Hello, world!</span><span class="sxs-lookup"><span data-stu-id="33819-133">Open *Pages/About.cshtml* and modify the page to display the message "Hello, world!</span></span> <span data-ttu-id="33819-134">서버 시간은 @DateTime.Now입니다.” 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="33819-134">The time on the server is @DateTime.Now":</span></span>

   [!code-cshtml[](sample/getting-started/about.cshtml?highlight=9&range=1-9)]

6. <span data-ttu-id="33819-135">[http://localhost:5000/About](http://localhost:5000/About)으로 이동하여 변경 내용을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="33819-135">Browse to [http://localhost:5000/About](http://localhost:5000/About) and verify the changes.</span></span>

[!INCLUDE [next steps](~/includes/getting-started/next-steps.md)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

1. <span data-ttu-id="33819-136">[.NET Core 모든 다운로드 페이지](https://www.microsoft.com/net/download/all)에서 SDK 1.0.4용 .NET Core **SDK 설치 관리자**를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="33819-136">Install the .NET Core **SDK Installer** for SDK 1.0.4 from the [.NET Core All Downloads page](https://www.microsoft.com/net/download/all).</span></span>

2. <span data-ttu-id="33819-137">새 ASP.NET Core 프로젝트에 대한 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33819-137">Create a folder for a new ASP.NET Core project.</span></span>

   <span data-ttu-id="33819-138">명령 셸을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="33819-138">Open a command shell.</span></span> <span data-ttu-id="33819-139">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="33819-139">Enter the following commands:</span></span>

   ```console
   mkdir aspnetcoreapp
   cd aspnetcoreapp
   ```

3. <span data-ttu-id="33819-140">컴퓨터에 최신 SDK 버전을 설치한 경우 *global.json* 파일을 만들어 1.0.4 SDK를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33819-140">If you have installed a later SDK version on your machine, create a *global.json* file to select the 1.0.4 SDK.</span></span>

   ```json
   {
     "sdk": { "version": "1.0.4" }
   }
   ```

4. <span data-ttu-id="33819-141">새 ASP.NET Core 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33819-141">Create a new ASP.NET Core project.</span></span>

   ```console
   dotnet new web
   ```

5. <span data-ttu-id="33819-142">패키지를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="33819-142">Restore the packages.</span></span>

   ```console
   dotnet restore
   ```

6. <span data-ttu-id="33819-143">앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="33819-143">Run the app.</span></span>

   ```console
   dotnet run
   ```

   <span data-ttu-id="33819-144">[dotnet run](/dotnet/core/tools/dotnet-run) 명령은 필요한 경우 앱을 먼저 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="33819-144">The [dotnet run](/dotnet/core/tools/dotnet-run) command builds the app first, if needed.</span></span>

7. <span data-ttu-id="33819-145">`http://localhost:5000`으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="33819-145">Browse to `http://localhost:5000`.</span></span>

[!INCLUDE [next steps](~/includes/getting-started/next-steps.md)]

::: moniker-end
