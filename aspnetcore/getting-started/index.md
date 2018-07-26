---
title: ASP.NET Core 시작
author: rick-anderson
description: ASP.NET Core를 사용하여 간단한 Hello World 앱을 만들고 실행하는 빠른 자습서입니다.
ms.author: riande
ms.custom: mvc
ms.date: 05/31/2018
uid: getting-started
ms.openlocfilehash: 7ab9f303d74786c4ac76f002d0f2c66371e78cb8
ms.sourcegitcommit: b4c7b1a4c48dec0865f27874275c73da1f75e918
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2018
ms.locfileid: "39228584"
---
# <a name="get-started-with-aspnet-core"></a><span data-ttu-id="46337-103">ASP.NET Core 시작</span><span class="sxs-lookup"><span data-stu-id="46337-103">Get started with ASP.NET Core</span></span>

::: moniker range=">= aspnetcore-2.1"

1. <span data-ttu-id="46337-104">[!INCLUDE [](~/includes/2.1-SDK.md)]를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="46337-104">Install the [!INCLUDE [](~/includes/2.1-SDK.md)].</span></span>

2. <span data-ttu-id="46337-105">ASP.NET Core 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="46337-105">Create an ASP.NET Core project.</span></span> <span data-ttu-id="46337-106">명령 셸을 열고 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="46337-106">Open a command shell and enter the following command:</span></span>

    ```console
    dotnet new webapp -o aspnetcoreapp
    ```

    [!INCLUDE [](~/includes/webapp-alias-notice.md)]

3. <span data-ttu-id="46337-107">HTTPS 개발 인증서 신뢰:</span><span class="sxs-lookup"><span data-stu-id="46337-107">Trust the HTTPS development certificate:</span></span>

# <a name="windowstabwindows"></a>[<span data-ttu-id="46337-108">Windows</span><span class="sxs-lookup"><span data-stu-id="46337-108">Windows</span></span>](#tab/windows)

    ```console
    dotnet dev-certs https --trust
    ```

   <span data-ttu-id="46337-109">이전 명령으로 인해 다음 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="46337-109">The preceding command displays the following dialog:</span></span>

   ![보안 경고 대화 상자](_static/cert.png)

   <span data-ttu-id="46337-111">개발 인증서를 신뢰하는 데 동의하는 경우 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="46337-111">Select **Yes** if you agree to trust the development certificate.</span></span>

# <a name="macostabmacos"></a>[<span data-ttu-id="46337-112">macOS</span><span class="sxs-lookup"><span data-stu-id="46337-112">macOS</span></span>](#tab/macos)

    ```console
    dotnet dev-certs https --trust
    ```

   <span data-ttu-id="46337-113">이전 명령으로 인해 다음 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="46337-113">The preceding command displays the following message:</span></span>

   <span data-ttu-id="46337-114">*HTTPS 개발 인증서를 신뢰해야 합니다. 인증서를 신뢰할 수 없는 경우 다음 명령을 실행합니다.*`'sudo security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.keychain <<certificate>>'`*이 명령은 시스템 키 집합에 인증서를 설치하기 위해 암호를 묻는 메시지를 표시할 수 있습니다.    암호:*</span><span class="sxs-lookup"><span data-stu-id="46337-114">*Trusting the HTTPS development certificate was requested. If the certificate is not already trusted we will run the following command:* `'sudo security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.keychain <<certificate>>'` *This command might prompt you for your password to install the certificate on the system keychain.    Password:*</span></span>

   <span data-ttu-id="46337-115">개발 인증서를 신뢰하는 데 동의하는 경우 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="46337-115">Enter your password if you agree to trust the development certificate.</span></span>

# <a name="linuxtablinux"></a>[<span data-ttu-id="46337-116">Linux</span><span class="sxs-lookup"><span data-stu-id="46337-116">Linux</span></span>](#tab/linux)

   <a name="see-the-documentation-for-your-linux-distribution-on-how-to-trust-the-https-development-certificate"></a><span data-ttu-id="46337-117">HTTPS 개발 인증서를 신뢰하는 방법은 Linux 배포에 대한 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="46337-117">See the documentation for your Linux distribution on how to trust the HTTPS development certificate</span></span>
---

4. <span data-ttu-id="46337-118">앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="46337-118">Run the app:</span></span>

    ```console
    cd aspnetcoreapp
    dotnet run
    ```

5. <span data-ttu-id="46337-119">[http://localhost:5001](http://localhost:5001)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="46337-119">Browse to [http://localhost:5001](http://localhost:5001).</span></span>  <span data-ttu-id="46337-120">**동의**를 클릭하여 개인 정보 및 쿠키 정책에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="46337-120">Click **Accept** to accept the privacy and cookie policy.</span></span> <span data-ttu-id="46337-121">이 앱은 개인 정보를 보관하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="46337-121">This app doesn't keep personal information.</span></span>

6. <span data-ttu-id="46337-122">*Pages/About.cshtml*을 열고 다음과 같은 강조 표시된 태그로 페이지를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="46337-122">Open *Pages/About.cshtml* and modify the page with the following highlighted markup:</span></span>

    [!code-cshtml[](sample/getting-started/about.cshtml?highlight=9)]

7. <span data-ttu-id="46337-123">[http://localhost:5001/About](http://localhost:5001/About)으로 이동하여 변경 내용이 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="46337-123">Browse to [http://localhost:5001/About](http://localhost:5001/About) and verify the changes are displayed.</span></span>

[!INCLUDE [next steps](~/includes/getting-started/next-steps.md)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

1. <span data-ttu-id="46337-124">[!INCLUDE [](~/includes/net-core-sdk-download-link.md)]를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="46337-124">Install the [!INCLUDE [](~/includes/net-core-sdk-download-link.md)].</span></span>

2. <span data-ttu-id="46337-125">새 ASP.NET Core 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="46337-125">Create a new ASP.NET Core project.</span></span>

   <span data-ttu-id="46337-126">명령 셸을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="46337-126">Open a command shell.</span></span> <span data-ttu-id="46337-127">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="46337-127">Enter the following command:</span></span>

    ```console
    dotnet new razor -o aspnetcoreapp
    ```

3. <span data-ttu-id="46337-128">다음 명령을 사용하여 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="46337-128">Run the app with the following commands:</span></span>

    ```console
    cd aspnetcoreapp
    dotnet run
    ```

4. <span data-ttu-id="46337-129">[http://localhost:5000](http://localhost:5000)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="46337-129">Browse to [http://localhost:5000](http://localhost:5000).</span></span>

5. <span data-ttu-id="46337-130">*Pages/About.cshtml* 을 열고 페이지를 수정하여 “Hello, world!</span><span class="sxs-lookup"><span data-stu-id="46337-130">Open *Pages/About.cshtml* and modify the page to display the message "Hello, world!</span></span> <span data-ttu-id="46337-131">서버 시간은 @DateTime.Now입니다.” 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="46337-131">The time on the server is @DateTime.Now":</span></span>

    [!code-cshtml[](sample/getting-started/about.cshtml?highlight=9&range=1-9)]

6. <span data-ttu-id="46337-132">[http://localhost:5000/About](http://localhost:5000/About)으로 이동하여 변경 내용을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="46337-132">Browse to [http://localhost:5000/About](http://localhost:5000/About) and verify the changes.</span></span>

[!INCLUDE [next steps](~/includes/getting-started/next-steps.md)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

1. <span data-ttu-id="46337-133">[.NET Core 모든 다운로드 페이지](https://www.microsoft.com/net/download/all)에서 SDK 1.0.4용 .NET Core **SDK 설치 관리자**를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="46337-133">Install the .NET Core **SDK Installer** for SDK 1.0.4 from the [.NET Core All Downloads page](https://www.microsoft.com/net/download/all).</span></span>

2. <span data-ttu-id="46337-134">새 ASP.NET Core 프로젝트에 대한 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="46337-134">Create a folder for a new ASP.NET Core project.</span></span>

   <span data-ttu-id="46337-135">명령 셸을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="46337-135">Open a command shell.</span></span> <span data-ttu-id="46337-136">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="46337-136">Enter the following commands:</span></span>

   ```console
   mkdir aspnetcoreapp
   cd aspnetcoreapp
   ```

3. <span data-ttu-id="46337-137">컴퓨터에 최신 SDK 버전을 설치한 경우 *global.json* 파일을 만들어 1.0.4 SDK를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="46337-137">If you have installed a later SDK version on your machine, create a *global.json* file to select the 1.0.4 SDK.</span></span>

   ```json
   {
     "sdk": { "version": "1.0.4" }
   }
   ```

4. <span data-ttu-id="46337-138">새 ASP.NET Core 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="46337-138">Create a new ASP.NET Core project.</span></span>

   ```console
   dotnet new web
   ```

5. <span data-ttu-id="46337-139">패키지를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="46337-139">Restore the packages.</span></span>

    ```console
    dotnet restore
    ```

6. <span data-ttu-id="46337-140">앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="46337-140">Run the app.</span></span>

   ```console
   dotnet run
   ```

   <span data-ttu-id="46337-141">[dotnet run](/dotnet/core/tools/dotnet-run) 명령은 필요한 경우 앱을 먼저 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="46337-141">The [dotnet run](/dotnet/core/tools/dotnet-run) command builds the app first, if needed.</span></span>

7. <span data-ttu-id="46337-142">`http://localhost:5000`으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="46337-142">Browse to `http://localhost:5000`.</span></span>

[!INCLUDE [next steps](~/includes/getting-started/next-steps.md)]
::: moniker-end
