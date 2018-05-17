---
title: ASP.NET Core에서 개발의 앱 암호의 안전한 저장소
author: rick-anderson
description: 개발 중 보안 정보를 안전하게 저장하는 방법을 보여줍니다.
manager: wpickett
ms.author: riande
ms.date: 09/15/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/app-secrets
ms.openlocfilehash: a268fd76a303dc1185b451e4f678fc2fe761e80a
ms.sourcegitcommit: 9bc34b8269d2a150b844c3b8646dcb30278a95ea
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/12/2018
---
# <a name="safe-storage-of-app-secrets-in-development-in-aspnet-core"></a><span data-ttu-id="09996-103">ASP.NET Core에서 개발의 앱 암호의 안전한 저장소</span><span class="sxs-lookup"><span data-stu-id="09996-103">Safe storage of app secrets in development in ASP.NET Core</span></span>

<span data-ttu-id="09996-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT), [김 Roth](https://github.com/danroth27), 및 [Scott Addie](https://scottaddie.com)</span><span class="sxs-lookup"><span data-stu-id="09996-104">By [Rick Anderson](https://twitter.com/RickAndMSFT), [Daniel Roth](https://github.com/danroth27), and [Scott Addie](https://scottaddie.com)</span></span> 

<span data-ttu-id="09996-105">이 문서에서는 개발 중 Secret Manager 도구를 이용해서 코드 외부에 보안 정보를 저장하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="09996-105">This document shows how you can use the Secret Manager tool in development to keep secrets out of your code.</span></span> <span data-ttu-id="09996-106">무엇보다 중요한 점은 절대로 소스 코드에 암호나 기타 중요한 데이터를 저장하면 안 될 뿐만 아니라, 프로덕션 환경의 보안 정보를 개발 및 테스트 모드에서 사용해서는 안 된다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="09996-106">The most important point is you should never store passwords or other sensitive data in source code, and you shouldn't use production secrets in development and test mode.</span></span> <span data-ttu-id="09996-107">대신, 이런 값들을 [구성](xref:fundamentals/configuration/index) 시스템을 이용해서 환경 변수로부터 읽거나, 또는 Secret Manager 도구를 이용해서 저장된 값으로부터 읽어올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09996-107">You can instead use the [configuration](xref:fundamentals/configuration/index) system to read these values from environment variables or from values stored using the Secret Manager tool.</span></span> <span data-ttu-id="09996-108">Secret Manager 도구는 민감한 보안 정보가 소스 제어에 체크인되지 않게 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="09996-108">The Secret Manager tool helps prevent sensitive data from being checked into source control.</span></span> <span data-ttu-id="09996-109">이 문서에서 설명하는 Secret Manager 도구를 이용해서 저장된 보안 정보는 [구성](xref:fundamentals/configuration/index) 시스템으로 읽을 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="09996-109">The [configuration](xref:fundamentals/configuration/index) system can read secrets stored with the Secret Manager tool described in this article.</span></span>

<span data-ttu-id="09996-110">Secret Manager 도구는 개발 시에만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="09996-110">The Secret Manager tool is used only in development.</span></span> <span data-ttu-id="09996-111">Azure의 테스트 및 프로덕션 보안 데이터는 [Microsoft Azure Key Vault](https://azure.microsoft.com/services/key-vault/) 구성 공급자를 이용해서 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09996-111">You can safeguard Azure test and production secrets with the [Microsoft Azure Key Vault](https://azure.microsoft.com/services/key-vault/) configuration provider.</span></span> <span data-ttu-id="09996-112">보다 자세한 정보는 [Azure 키 자격 증명 모음 구성 공급자](xref:security/key-vault-configuration)를 참고하시기 바랍니다. </span><span class="sxs-lookup"><span data-stu-id="09996-112">See [Azure Key Vault configuration provider](xref:security/key-vault-configuration) for more information.</span></span>

## <a name="environment-variables"></a><span data-ttu-id="09996-113">환경 변수</span><span class="sxs-lookup"><span data-stu-id="09996-113">Environment variables</span></span>

<span data-ttu-id="09996-114">코드나 로컬 구성 파일에 응용 프로그램의 보안 정보를 저장하지 않으려면 환경 변수에 보안 정보를 저장합니다. </span><span class="sxs-lookup"><span data-stu-id="09996-114">To avoid storing app secrets in code or in local configuration files, you store secrets in environment variables.</span></span> <span data-ttu-id="09996-115">`AddEnvironmentVariables` 를 호출하면 환경 변수에서 값을 읽도록 [구성](xref:fundamentals/configuration/index) 프레임워크를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="09996-115">You can setup the [configuration](xref:fundamentals/configuration/index) framework to read values from environment variables by calling `AddEnvironmentVariables`.</span></span> <span data-ttu-id="09996-116">그런 다음, 환경 변수를 사용해서 기존에 지정된 모든 구성 소스의 구성 값을 재지정 할 수 있습니다. </span><span class="sxs-lookup"><span data-stu-id="09996-116">You can then use environment variables to override configuration values for all previously specified configuration sources.</span></span>

<span data-ttu-id="09996-117">예를 들어, Visual Studio에서 개별 사용자 계정 옵션으로 새로운 ASP.NET Core 웹 응용 프로그램을 생성하면, 프로젝트의 *appsettings.json* 파일에 `DefaultConnection`이라는 키를 가진 기본 연결 문자열이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="09996-117">For example, if you create a new ASP.NET Core web app with individual user accounts, it will add a default connection string to the *appsettings.json* file in the project with the key `DefaultConnection`.</span></span> <span data-ttu-id="09996-118">이 기본 연결 문자열은 사용자 모드에서 실행되고 암호를 요구하지 않는 LocalDB를 사용하도록 구성됩니다. </span><span class="sxs-lookup"><span data-stu-id="09996-118">The default connection string is setup to use LocalDB, which runs in user mode and doesn't require a password.</span></span> <span data-ttu-id="09996-119">응용 프로그램을 테스트 서버나 프로덕션 서버에 배포할 때, `DefaultConnection` 키의 값을 테스트 또는 프로덕션 데이터베이스 서버의 연결 문자열이 지정된(민감한 자격 증명이 포함될 수 있는) 환경 변수 설정으로 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09996-119">When you deploy your application to a test or production server, you can override the `DefaultConnection` key value with an environment variable setting that contains the connection string (potentially with sensitive credentials) for a test or production database server.</span></span>

>[!WARNING]
> <span data-ttu-id="09996-120">일반적으로 환경 변수는 평문으로 저장되며 암호화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="09996-120">Environment variables are generally stored in plain text and are not encrypted.</span></span> <span data-ttu-id="09996-121">컴퓨터나 프로세스가 손상될 경우, 신뢰할 수 없는 사용자가 환경 변수에 접근할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09996-121">If the machine or process is compromised, then environment variables can be accessed by untrusted parties.</span></span> <span data-ttu-id="09996-122">따라서 여전히 사용자의 보안 정보 유출을 방지하기 위한 추가적인 방안이 필요할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09996-122">Additional measures to prevent disclosure of user secrets may still be required.</span></span>

## <a name="secret-manager"></a><span data-ttu-id="09996-123">Secret Manager</span><span class="sxs-lookup"><span data-stu-id="09996-123">Secret Manager</span></span>

<span data-ttu-id="09996-124">Secret Manager 도구는 개발 작업에 필요한 민감한 데이터를 프로젝트의 디렉터리 구조 외부에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="09996-124">The Secret Manager tool stores sensitive data for development work outside of your project tree.</span></span> <span data-ttu-id="09996-125">암호 관리자 도구는 개발 하는 동안.NET Core 프로젝트에 대 한 기밀 정보를 사용할 수 있는 프로젝트 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="09996-125">The Secret Manager tool is a project tool that can be used to store secrets for a .NET Core project during development.</span></span> <span data-ttu-id="09996-126">Secret Manager 도구를 사용하면 응용 프로그램의 보안 정보를 특정 프로젝트와 연결하고 이를 여러 프로젝트에서 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09996-126">With the Secret Manager tool, you can associate app secrets with a specific project and share them across multiple projects.</span></span>

>[!WARNING]
> <span data-ttu-id="09996-127">암호 관리자 도구 저장 된 암호를 암호화 하지 않습니다 하 고 신뢰할 수 있는 저장소로 처리 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09996-127">The Secret Manager tool doesn't encrypt the stored secrets and shouldn't be treated as a trusted store.</span></span> <span data-ttu-id="09996-128">개발 용도로입니다.</span><span class="sxs-lookup"><span data-stu-id="09996-128">It's for development purposes only.</span></span> <span data-ttu-id="09996-129">키와 값은 사용자 프로필 디렉터리에 위치한 JSON 구성 파일에 저장됩니다. </span><span class="sxs-lookup"><span data-stu-id="09996-129">The keys and values are stored in a JSON configuration file in the user profile directory.</span></span>

## <a name="installing-the-secret-manager-tool"></a><span data-ttu-id="09996-130">Secret Manager 도구 설치하기</span><span class="sxs-lookup"><span data-stu-id="09996-130">Installing the Secret Manager tool</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="09996-131">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="09996-131">Visual Studio</span></span>](#tab/visual-studio/)

<span data-ttu-id="09996-132">마우스 오른쪽 버튼으로 솔루션 탐색기에서 프로젝트를 클릭한 다음, 컨텍스트 메뉴에서 **\<project_name\>.csproj 편집 (Edit \<project_name\>.csproj)** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="09996-132">Right-click the project in Solution Explorer, and select **Edit \<project_name\>.csproj** from the context menu.</span></span> <span data-ttu-id="09996-133">다음에 강조 표시된 줄을 *.csproj* 파일에 추가하고 저장하면 관련된 NuGet 패키지가 복원됩니다.</span><span class="sxs-lookup"><span data-stu-id="09996-133">Add the highlighted line to the *.csproj* file, and save to restore the associated NuGet package:</span></span>

[!code-xml[](app-secrets/sample/UserSecrets/UserSecrets-before.csproj?highlight=10)]

<span data-ttu-id="09996-134">다시 마우스 오른쪽 버튼으로 솔루션 탐색기에서 프로젝트를 클릭한 다음, 컨텍스트 메뉴에서 **사용자 암호 관리 (Manage User Secrets)** 를 선택합니다. </span><span class="sxs-lookup"><span data-stu-id="09996-134">Right-click the project in Solution Explorer again, and select **Manage User Secrets** from the context menu.</span></span> <span data-ttu-id="09996-135">그러면 다음 예제에 강조 표시된 것처럼 *.csproj* 파일의 `PropertyGroup` 노드 하위에 새로운 `UserSecretsId` 노드가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="09996-135">This gesture adds a new `UserSecretsId` node within a `PropertyGroup` of the *.csproj* file, as highlighted in the following sample:</span></span>

[!code-xml[](app-secrets/sample/UserSecrets/UserSecrets-after.csproj?highlight=4)]

<span data-ttu-id="09996-136">수정된 *.csproj* 파일을 저장하면 텍스트 편집기에서 `secrets.json` 파일이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="09996-136">Saving the modified *.csproj* file also opens a `secrets.json` file in the text editor.</span></span> <span data-ttu-id="09996-137">`secrets.json` 파일의 내용을 다음 코드로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="09996-137">Replace the contents of the `secrets.json` file with the following code:</span></span>

```json
{
    "MySecret": "ValueOfMySecret"
}
```

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="09996-138">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="09996-138">Visual Studio Code</span></span>](#tab/visual-studio-code/)

<span data-ttu-id="09996-139">추가 `Microsoft.Extensions.SecretManager.Tools` 에 *.csproj* 파일을 실행 [dotnet 복원](/dotnet/core/tools/dotnet-restore)합니다.</span><span class="sxs-lookup"><span data-stu-id="09996-139">Add `Microsoft.Extensions.SecretManager.Tools` to the *.csproj* file and run [dotnet restore](/dotnet/core/tools/dotnet-restore).</span></span> <span data-ttu-id="09996-140">명령줄에서 동일한 단계를 사용해서 Secret Manager 도구를 설치할 수 있습니다. </span><span class="sxs-lookup"><span data-stu-id="09996-140">You can use the same steps to install the Secret Manager Tool using for the command line.</span></span>

[!code-xml[](app-secrets/sample/UserSecrets/UserSecrets-before.csproj?highlight=10)]

<span data-ttu-id="09996-141">다음 명령을 실행해서 Secret Manager 도구를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="09996-141">Test the Secret Manager tool by running the following command:</span></span>

```console
dotnet user-secrets -h
```

<span data-ttu-id="09996-142">그러면 Secret Manager 도구의 사용법, 옵션 및 명령 도움말이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="09996-142">The Secret Manager tool will display usage, options and command help.</span></span>

> [!NOTE]
> <span data-ttu-id="09996-143">이렇게 *.csproj* 파일의 `DotNetCliToolReference` 노드에 정의된 도구를 실행하려면 *.csproj* 파일과 동일한 디렉터리에 위치해 있어야 합니다. </span><span class="sxs-lookup"><span data-stu-id="09996-143">You must be in the same directory as the *.csproj* file to run tools defined in the *.csproj* file's `DotNetCliToolReference` nodes.</span></span>

<span data-ttu-id="09996-144">Secret Manager 도구는 사용자 프로필에 저장된 프로젝트별 구성 설정을 대상으로 동작합니다.</span><span class="sxs-lookup"><span data-stu-id="09996-144">The Secret Manager tool operates on project-specific configuration settings that are stored in your user profile.</span></span> <span data-ttu-id="09996-145">사용자 보안 정보를 사용하려면 프로젝트의 *.csproj* 파일에 `UserSecretsId` 값을 지정해야 합니다. </span><span class="sxs-lookup"><span data-stu-id="09996-145">To use user secrets, the project must specify a `UserSecretsId` value in its *.csproj* file.</span></span> <span data-ttu-id="09996-146">`UserSecretsId` 값은 선택적이긴 하지만 일반적으로 프로젝트에 고유합니다.</span><span class="sxs-lookup"><span data-stu-id="09996-146">The value of `UserSecretsId` is arbitrary, but is generally unique to the project.</span></span> <span data-ttu-id="09996-147">개발자는 대부분 `UserSecretsId` 값에 GUID를 생성해서 지정합니다. </span><span class="sxs-lookup"><span data-stu-id="09996-147">Developers typically generate a GUID for the `UserSecretsId`.</span></span>

<span data-ttu-id="09996-148">프로젝트의 *.csproj* 파일에 `UserSecretsId` 를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="09996-148">Add a `UserSecretsId` for your project in the *.csproj* file:</span></span>

[!code-xml[](app-secrets/sample/UserSecrets/UserSecrets-after.csproj?highlight=4)]

<span data-ttu-id="09996-149">Secret Manager 도구를 사용해서 보안 정보를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="09996-149">Use the Secret Manager tool to set a secret.</span></span> <span data-ttu-id="09996-150">예를 들어 프로젝트 디렉터리의 명령 창에 다음과 같이 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="09996-150">For example, in a command window from the project directory, enter the following:</span></span>

```console
dotnet user-secrets set MySecret ValueOfMySecret
```

<span data-ttu-id="09996-151">다른 디렉터리에서 Secret Manager 도구를 실행할 수도 있지만, `--project` 옵션을 사용해서 *.csproj* 파일의 경로를 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09996-151">You can run the Secret Manager tool from other directories, but you must use the `--project` option to pass in the path to the *.csproj* file:</span></span>

```console
dotnet user-secrets set MySecret ValueOfMySecret --project c:\work\WebApp1\src\webapp1
```

<span data-ttu-id="09996-152">Secret Manager 도구를 사용해서 응용 프로그램의 보안 정보의 목록을 나열하거나 제거하고 초기화시킬 수도 있습니다. </span><span class="sxs-lookup"><span data-stu-id="09996-152">You can also use the Secret Manager tool to list, remove and clear app secrets.</span></span>

---

## <a name="accessing-user-secrets-via-configuration"></a><span data-ttu-id="09996-153">구성을 통해서 사용자 보안 정보에 접근하기</span><span class="sxs-lookup"><span data-stu-id="09996-153">Accessing user secrets via configuration</span></span>

<span data-ttu-id="09996-154">구성 시스템을 통해서 Secret Manager 도구의 사용자 보안 정보에 접근할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09996-154">You access Secret Manager secrets through the configuration system.</span></span> <span data-ttu-id="09996-155">추가 `Microsoft.Extensions.Configuration.UserSecrets` 패키지 및 실행 [dotnet 복원](/dotnet/core/tools/dotnet-restore)합니다.</span><span class="sxs-lookup"><span data-stu-id="09996-155">Add the `Microsoft.Extensions.Configuration.UserSecrets` package and run [dotnet restore](/dotnet/core/tools/dotnet-restore).</span></span>

<span data-ttu-id="09996-156">그리고 `Startup`의 생성자에 사용자 보안 정보 구성 소스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="09996-156">Add the user secrets configuration source to the `Startup` method:</span></span>

[!code-csharp[](app-secrets/sample/UserSecrets/Startup.cs?highlight=16-19)]

<span data-ttu-id="09996-157">그러면 구성 API를 통해서 사용자 보안 정보에 접근할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09996-157">You can access user secrets via the configuration API:</span></span>

[!code-csharp[](app-secrets/sample/UserSecrets/Startup.cs?highlight=26-29)]

## <a name="how-the-secret-manager-tool-works"></a><span data-ttu-id="09996-158">Secret Manager 도구의 동작 방식</span><span class="sxs-lookup"><span data-stu-id="09996-158">How the Secret Manager tool works</span></span>

<span data-ttu-id="09996-159">Secret Manager 도구는 값이 저장되는 위치 및 방법 같은 구현에 관한 세부적인 내용을 추상화합니다.</span><span class="sxs-lookup"><span data-stu-id="09996-159">The Secret Manager tool abstracts away the implementation details, such as where and how the values are stored.</span></span> <span data-ttu-id="09996-160">이런 세부적인 내용을 모르더라도 Secret Manager 도구를 사용하는 데는 아무런 지장이 없습니다. </span><span class="sxs-lookup"><span data-stu-id="09996-160">You can use the tool without knowing these implementation details.</span></span> <span data-ttu-id="09996-161">현재 버전에서는 사용자 프로필 디렉터리의 [JSON](http://json.org/) 구성 파일에 값이 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="09996-161">In the current version, the values are stored in a [JSON](http://json.org/) configuration file in the user profile directory:</span></span>

* <span data-ttu-id="09996-162">Windows: `%APPDATA%\microsoft\UserSecrets\<userSecretsId>\secrets.json`</span><span class="sxs-lookup"><span data-stu-id="09996-162">Windows: `%APPDATA%\microsoft\UserSecrets\<userSecretsId>\secrets.json`</span></span>

* <span data-ttu-id="09996-163">Linux: `~/.microsoft/usersecrets/<userSecretsId>/secrets.json`</span><span class="sxs-lookup"><span data-stu-id="09996-163">Linux: `~/.microsoft/usersecrets/<userSecretsId>/secrets.json`</span></span>

* <span data-ttu-id="09996-164">macOS: `~/.microsoft/usersecrets/<userSecretsId>/secrets.json`</span><span class="sxs-lookup"><span data-stu-id="09996-164">macOS: `~/.microsoft/usersecrets/<userSecretsId>/secrets.json`</span></span>

<span data-ttu-id="09996-165">여기서 `userSecretsId` 의 값은 *.csproj* 파일에 지정된 값입니다. </span><span class="sxs-lookup"><span data-stu-id="09996-165">The value of `userSecretsId` comes from the value specified in *.csproj* file.</span></span>

<span data-ttu-id="09996-166">이러한 구현 정보 변경 될 수 있으므로 위치나 암호 관리자 도구와 함께 저장 된 데이터의 형식에 따라 달라 지 코드를 작성 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09996-166">You shouldn't write code that depends on the location or format of the data saved with the Secret Manager tool, as these implementation details might change.</span></span> <span data-ttu-id="09996-167">예를 들어, 지금은 보안 정보가 암호화되지 *않지만* 나중에는 암호화될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09996-167">For example, the secret values are currently *not* encrypted today, but could be someday.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="09996-168">추가 자료</span><span class="sxs-lookup"><span data-stu-id="09996-168">Additional resources</span></span>

* [<span data-ttu-id="09996-169">구성</span><span class="sxs-lookup"><span data-stu-id="09996-169">Configuration</span></span>](xref:fundamentals/configuration/index)
