---
title: ASP.NET Core 시작
author: rick-anderson
description: ASP.NET Core를 사용하여 간단한 Hello World 앱을 만들고 실행하는 빠른 자습서입니다.
ms.author: riande
ms.custom: mvc
ms.date: 05/31/2018
uid: getting-started
ms.openlocfilehash: 22e9c982921cc03d89506e18ff99bf481027dda6
ms.sourcegitcommit: 931b6a2d7eb28a0f1295e8a95690b8c4c5f58477
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37077662"
---
# <a name="get-started-with-aspnet-core"></a><span data-ttu-id="3b427-103">ASP.NET Core 시작</span><span class="sxs-lookup"><span data-stu-id="3b427-103">Get started with ASP.NET Core</span></span>

::: moniker range=">= aspnetcore-2.1"

1. <span data-ttu-id="3b427-104">[!INCLUDE [](~/includes/2.1-SDK.md)]를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3b427-104">Install the [!INCLUDE [](~/includes/2.1-SDK.md)].</span></span>

2. <span data-ttu-id="3b427-105">ASP.NET Core 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3b427-105">Create an ASP.NET Core project.</span></span> <span data-ttu-id="3b427-106">명령 셸을 열고 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3b427-106">Open a command shell and enter the following command:</span></span>

    ```console
    dotnet new webapp -o aspnetcoreapp
    ```

    <span data-ttu-id="3b427-107">[!INCLUDE [](~/includes/webapp-alias-notice.md) [](~/includes/webapp-alias-notice.md)]</span><span class="sxs-lookup"><span data-stu-id="3b427-107">[!INCLUDE [](~/includes/webapp-alias-notice.md) [](~/includes/webapp-alias-notice.md)]</span></span>

3. <span data-ttu-id="3b427-108">HTTPS 개발 인증서 신뢰:</span><span class="sxs-lookup"><span data-stu-id="3b427-108">Trust the HTTPS development certificate:</span></span>

# <a name="windowstabwindows"></a>[<span data-ttu-id="3b427-109">Windows</span><span class="sxs-lookup"><span data-stu-id="3b427-109">Windows</span></span>](#tab/windows)

    ```console
    dotnet dev-certs https --trust
    ```

    The preceding command displays the following dialog:

    ![Security warning dialog](_static/cert.png)

    Select **Yes** if you agree to trust the development certificate.

# <a name="macostabmacos"></a>[<span data-ttu-id="3b427-110">macOS</span><span class="sxs-lookup"><span data-stu-id="3b427-110">macOS</span></span>](#tab/macos)

    ```console
    dotnet dev-certs https --trust
    ```

    The preceding command displays the following message:

    *Trusting the HTTPS development certificate was requested. If the certificate is not already trusted we will run the following command:*
    `'sudo security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.keychain <<certificate>>'`
    *This command might prompt you for your password to install the certificate on the system keychain.
    Password:*

    Enter your password if you agree to trust the development certificate.

# <a name="linuxtablinux"></a>[<span data-ttu-id="3b427-111">Linux</span><span class="sxs-lookup"><span data-stu-id="3b427-111">Linux</span></span>](#tab/linux)

    See the documentation for your Linux distribution on how to trust the HTTPS development certificate
---

4. <span data-ttu-id="3b427-112">앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3b427-112">Run the app:</span></span>

    ```console
    cd aspnetcoreapp
    dotnet run
    ```

5. <span data-ttu-id="3b427-113">[http://localhost:5001](http://localhost:5001)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3b427-113">Browse to [http://localhost:5001](http://localhost:5001).</span></span>  <span data-ttu-id="3b427-114">**동의**를 클릭하여 개인 정보 및 쿠키 정책에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="3b427-114">Click **Accept** to accept the privacy and cookie policy.</span></span> <span data-ttu-id="3b427-115">이 앱은 개인 정보를 보관하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3b427-115">This app doesn't keep personal information.</span></span>

6. <span data-ttu-id="3b427-116">*Pages/About.cshtml*을 열고 다음과 같은 강조 표시된 태그로 페이지를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b427-116">Open *Pages/About.cshtml* and modify the page with the following highlighted markup:</span></span>

    [!code-cshtml[](sample/getting-started/about.cshtml?highlight=9)]

7. <span data-ttu-id="3b427-117">[http://localhost:5001/About](http://localhost:5001/About)으로 이동하여 변경 내용이 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3b427-117">Browse to [http://localhost:5001/About](http://localhost:5001/About) and verify the changes are displayed.</span></span>

[!INCLUDE [next steps](~/includes/getting-started/next-steps.md)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

1. <span data-ttu-id="3b427-118">[!INCLUDE [](~/includes/net-core-sdk-download-link.md)]를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3b427-118">Install the [!INCLUDE [](~/includes/net-core-sdk-download-link.md)].</span></span>

2. <span data-ttu-id="3b427-119">새 ASP.NET Core 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3b427-119">Create a new ASP.NET Core project.</span></span>

   <span data-ttu-id="3b427-120">명령 셸을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3b427-120">Open a command shell.</span></span> <span data-ttu-id="3b427-121">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3b427-121">Enter the following command:</span></span>

    ```console
    dotnet new razor -o aspnetcoreapp
    ```

3. <span data-ttu-id="3b427-122">다음 명령을 사용하여 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3b427-122">Run the app with the following commands:</span></span>

    ```console
    cd aspnetcoreapp
    dotnet run
    ```

4. <span data-ttu-id="3b427-123">[http://localhost:5000](http://localhost:5000)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3b427-123">Browse to [http://localhost:5000](http://localhost:5000).</span></span>

5. <span data-ttu-id="3b427-124">*Pages/About.cshtml* 을 열고 페이지를 수정하여 “Hello, world!</span><span class="sxs-lookup"><span data-stu-id="3b427-124">Open *Pages/About.cshtml* and modify the page to display the message "Hello, world!</span></span> <span data-ttu-id="3b427-125">서버 시간은 @DateTime.Now입니다.” 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="3b427-125">The time on the server is @DateTime.Now":</span></span>

    [!code-cshtml[](sample/getting-started/about.cshtml?highlight=9&range=1-9)]

6. <span data-ttu-id="3b427-126">[http://localhost:5000/About](http://localhost:5000/About)으로 이동하여 변경 내용을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3b427-126">Browse to [http://localhost:5000/About](http://localhost:5000/About) and verify the changes.</span></span>

[!INCLUDE [next steps](~/includes/getting-started/next-steps.md)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

1. <span data-ttu-id="3b427-127">[.NET Core 모든 다운로드 페이지](https://www.microsoft.com/net/download/all)에서 SDK 1.0.4용 .NET Core **SDK 설치 관리자**를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3b427-127">Install the .NET Core **SDK Installer** for SDK 1.0.4 from the [.NET Core All Downloads page](https://www.microsoft.com/net/download/all).</span></span>

2. <span data-ttu-id="3b427-128">새 ASP.NET Core 프로젝트에 대한 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3b427-128">Create a folder for a new ASP.NET Core project.</span></span>

   <span data-ttu-id="3b427-129">명령 셸을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3b427-129">Open a command shell.</span></span> <span data-ttu-id="3b427-130">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3b427-130">Enter the following commands:</span></span>

   ```console
   mkdir aspnetcoreapp
   cd aspnetcoreapp
   ```

3. <span data-ttu-id="3b427-131">컴퓨터에 최신 SDK 버전을 설치한 경우 *global.json* 파일을 만들어 1.0.4 SDK를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3b427-131">If you have installed a later SDK version on your machine, create a *global.json* file to select the 1.0.4 SDK.</span></span>

   ```json
   {
     "sdk": { "version": "1.0.4" }
   }
   ```

4. <span data-ttu-id="3b427-132">새 ASP.NET Core 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3b427-132">Create a new ASP.NET Core project.</span></span>

   ```console
   dotnet new web
   ```

5. <span data-ttu-id="3b427-133">패키지를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="3b427-133">Restore the packages.</span></span>

    ```console
    dotnet restore
    ```

6. <span data-ttu-id="3b427-134">앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3b427-134">Run the app.</span></span>

   ```console
   dotnet run
   ```

   <span data-ttu-id="3b427-135">[dotnet run](/dotnet/core/tools/dotnet-run) 명령은 필요한 경우 앱을 먼저 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="3b427-135">The [dotnet run](/dotnet/core/tools/dotnet-run) command builds the app first, if needed.</span></span>

7. <span data-ttu-id="3b427-136">`http://localhost:5000`으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3b427-136">Browse to `http://localhost:5000`.</span></span>

[!INCLUDE [next steps](~/includes/getting-started/next-steps.md)]
::: moniker-end
