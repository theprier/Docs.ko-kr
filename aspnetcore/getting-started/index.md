---
title: ASP.NET Core 시작
author: rick-anderson
description: ASP.NET Core를 사용하여 간단한 Hello World 앱을 만들고 실행하는 빠른 자습서입니다.
ms.author: riande
ms.custom: mvc
ms.date: 01/15/2019
uid: getting-started
ms.openlocfilehash: eee927f4306fa7757f3f361e6c6f367658512897
ms.sourcegitcommit: 42a8164b8aba21f322ffefacb92301bdfb4d3c2d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54341812"
---
# <a name="tutorial-get-started-with-aspnet-core"></a><span data-ttu-id="6d691-103">자습서: ASP.NET Core 시작</span><span class="sxs-lookup"><span data-stu-id="6d691-103">Tutorial: Get started with ASP.NET Core</span></span>

<span data-ttu-id="6d691-104">이 자습서에서는 .NET Core 명령줄 인터페이스를 사용하여 ASP.NET Core 웹앱을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6d691-104">This tutorial shows how to use the .NET Core command-line interface to create an ASP.NET Core web app.</span></span>

<span data-ttu-id="6d691-105">다음을 수행하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6d691-105">You'll learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6d691-106">웹앱 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6d691-106">Create a web app project.</span></span>
> * <span data-ttu-id="6d691-107">로컬 HTTPS를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6d691-107">Enable local HTTPS.</span></span>
> * <span data-ttu-id="6d691-108">앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6d691-108">Run the app.</span></span>
> * <span data-ttu-id="6d691-109">Razor 페이지를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="6d691-109">Edit a Razor page.</span></span>

<span data-ttu-id="6d691-110">마지막에는 로컬 머신에서 작업 웹앱이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d691-110">At the end, you'll have a working web app running on your local machine.</span></span>

![웹앱 홈페이지](_static/home-page.png)

## <a name="prerequisites"></a><span data-ttu-id="6d691-112">전제 조건</span><span class="sxs-lookup"><span data-stu-id="6d691-112">Prerequisites</span></span>

* [<span data-ttu-id="6d691-113">.NET Core 2.2 SDK</span><span class="sxs-lookup"><span data-stu-id="6d691-113">.NET Core 2.2 SDK</span></span>](https://www.microsoft.com/net/download/all)

## <a name="create-a-web-app-project"></a><span data-ttu-id="6d691-114">웹앱 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="6d691-114">Create a web app project</span></span>

<span data-ttu-id="6d691-115">명령 셸을 열고 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6d691-115">Open a command shell, and enter the following command:</span></span>

```console
dotnet new webapp -o aspnetcoreapp
```

## <a name="enable-local-https"></a><span data-ttu-id="6d691-116">로컬 HTTPS 사용</span><span class="sxs-lookup"><span data-stu-id="6d691-116">Enable local HTTPS</span></span>

<span data-ttu-id="6d691-117">HTTPS 개발 인증서 신뢰:</span><span class="sxs-lookup"><span data-stu-id="6d691-117">Trust the HTTPS development certificate:</span></span>

# <a name="windowstabwindows"></a>[<span data-ttu-id="6d691-118">Windows</span><span class="sxs-lookup"><span data-stu-id="6d691-118">Windows</span></span>](#tab/windows)

```console
dotnet dev-certs https --trust
```

<span data-ttu-id="6d691-119">이전 명령으로 인해 다음 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d691-119">The preceding command displays the following dialog:</span></span>

![보안 경고 대화 상자](_static/cert.png)

<span data-ttu-id="6d691-121">개발 인증서를 신뢰하는 데 동의하는 경우 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6d691-121">Select **Yes** if you agree to trust the development certificate.</span></span>

# <a name="macostabmacos"></a>[<span data-ttu-id="6d691-122">macOS</span><span class="sxs-lookup"><span data-stu-id="6d691-122">macOS</span></span>](#tab/macos)

```console
dotnet dev-certs https --trust
```

<span data-ttu-id="6d691-123">이전 명령으로 인해 다음 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d691-123">The preceding command displays the following message:</span></span>

<span data-ttu-id="6d691-124">*HTTPS 개발 인증서를 신뢰해야 합니다. 인증서를 신뢰할 수 없는 경우*  `'sudo security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.keychain <<certificate>>'` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6d691-124">*Trusting the HTTPS development certificate was requested. If the certificate is not already trusted we will run the following command:* `'sudo security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.keychain <<certificate>>'`.</span></span>  
<span data-ttu-id="6d691-125">\*이 명령은 시스템 키 집합에 인증서를 설치하기 위해 암호를 묻는 메시지를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d691-125">\*This command might prompt you for your password to install the certificate on the system keychain.</span></span>

<span data-ttu-id="6d691-126">암호:\*</span><span class="sxs-lookup"><span data-stu-id="6d691-126">Password:\*</span></span>

<span data-ttu-id="6d691-127">개발 인증서를 신뢰하는 데 동의하는 경우 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6d691-127">Enter your password if you agree to trust the development certificate.</span></span>

# <a name="linuxtablinux"></a>[<span data-ttu-id="6d691-128">Linux</span><span class="sxs-lookup"><span data-stu-id="6d691-128">Linux</span></span>](#tab/linux)

<span data-ttu-id="6d691-129">HTTPS 개발 인증서를 신뢰하는 방법은 Linux 배포에 대한 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d691-129">See the documentation for your Linux distribution on how to trust the HTTPS development certificate.</span></span>

---

## <a name="run-the-app"></a><span data-ttu-id="6d691-130">앱 실행</span><span class="sxs-lookup"><span data-stu-id="6d691-130">Run the app</span></span>

<span data-ttu-id="6d691-131">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6d691-131">Run the following commands:</span></span>

```console
cd aspnetcoreapp
dotnet run
```

<span data-ttu-id="6d691-132">명령 셸에서 앱이 시작되었음을 나타낸 후 [https://localhost:5001](https://localhost:5001)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6d691-132">After the command shell indicates that the app has started, browse to [https://localhost:5001](https://localhost:5001).</span></span> <span data-ttu-id="6d691-133">**동의**를 클릭하여 개인 정보 및 쿠키 정책에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="6d691-133">Click **Accept** to accept the privacy and cookie policy.</span></span> <span data-ttu-id="6d691-134">이 앱은 개인 정보를 보관하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6d691-134">This app doesn't keep personal information.</span></span>

## <a name="edit-a-razor-page"></a><span data-ttu-id="6d691-135">Razor 페이지 편집</span><span class="sxs-lookup"><span data-stu-id="6d691-135">Edit a Razor page</span></span>

<span data-ttu-id="6d691-136">*Pages/Index.cshtml*을 열고 다음에서 강조 표시된 영역처럼 페이지를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="6d691-136">Open *Pages/Index.cshtml* and modify the page with the following highlighted markup:</span></span>

[!code-cshtml[](sample/index.cshtml?highlight=9)]

<span data-ttu-id="6d691-137">[https://localhost:5001](https://localhost:5001)로 이동하여 변경 내용이 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6d691-137">Browse to [https://localhost:5001](https://localhost:5001), and verify the changes are displayed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d691-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6d691-138">Next steps</span></span>

<span data-ttu-id="6d691-139">본 자습서에서는 다음 작업에 관한 방법을 학습했습니다.</span><span class="sxs-lookup"><span data-stu-id="6d691-139">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6d691-140">웹앱 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6d691-140">Create a web app project.</span></span>
> * <span data-ttu-id="6d691-141">로컬 HTTPS를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6d691-141">Enable local HTTPS.</span></span>
> * <span data-ttu-id="6d691-142">프로젝트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6d691-142">Run the project.</span></span>
> * <span data-ttu-id="6d691-143">페이지를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="6d691-143">Make a change.</span></span>

<span data-ttu-id="6d691-144">ASP.NET Core에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d691-144">To learn more about ASP.NET Core, see the introduction:</span></span>

> [!div class="nextstepaction"]
> <xref:index>
