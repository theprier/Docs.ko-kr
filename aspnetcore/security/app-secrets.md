---
title: ASP.NET Core에서 개발의 앱 암호의 안전한 저장소
author: rick-anderson
description: 저장 하 고 ASP.NET Core 응용 프로그램을 개발 하는 동안 앱 암호로 중요 한 정보를 검색 하는 방법을 알아봅니다.
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 05/16/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/app-secrets
ms.openlocfilehash: 88b4ee9a963543f8cc97cb66271628a14fe657de
ms.sourcegitcommit: 3a893ae05f010656d99d6ddf55e82f1b5b6933bc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/18/2018
---
# <a name="safe-storage-of-app-secrets-in-development-in-aspnet-core"></a><span data-ttu-id="40d2b-103">ASP.NET Core에서 개발의 앱 암호의 안전한 저장소</span><span class="sxs-lookup"><span data-stu-id="40d2b-103">Safe storage of app secrets in development in ASP.NET Core</span></span>

<span data-ttu-id="40d2b-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT), [김 Roth](https://github.com/danroth27), 및 [Scott Addie](https://github.com/scottaddie)</span><span class="sxs-lookup"><span data-stu-id="40d2b-104">By [Rick Anderson](https://twitter.com/RickAndMSFT), [Daniel Roth](https://github.com/danroth27), and [Scott Addie](https://github.com/scottaddie)</span></span>

::: moniker range="<= aspnetcore-1.1"
<span data-ttu-id="40d2b-105">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/app-secrets/samples/1.1)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="40d2b-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/app-secrets/samples/1.1) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>
::: moniker-end
::: moniker range=">= aspnetcore-2.0"
<span data-ttu-id="40d2b-106">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/app-secrets/samples/2.1)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="40d2b-106">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/app-secrets/samples/2.1) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>
::: moniker-end

<span data-ttu-id="40d2b-107">이 문서에 저장 하 고 ASP.NET Core 응용 프로그램을 개발 하는 동안 중요 한 데이터를 검색 하는 기술을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-107">This document explains techniques for storing and retrieving sensitive data during the development of an ASP.NET Core app.</span></span> <span data-ttu-id="40d2b-108">소스 코드에서 암호 또는 기타 중요 한 데이터를 저장 해서는 안 하 고 개발에서 생산 암호를 사용 하거나 모드를 테스트 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-108">You should never store passwords or other sensitive data in source code, and you shouldn't use production secrets in development or test mode.</span></span> <span data-ttu-id="40d2b-109">저장 하 고 Azure 테스트 및 프로덕션 비밀 정보를 보호할 수는 [Azure 키 자격 증명 모음 구성 공급자](xref:security/key-vault-configuration)합니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-109">You can store and protect Azure test and production secrets with the [Azure Key Vault configuration provider](xref:security/key-vault-configuration).</span></span>

## <a name="environment-variables"></a><span data-ttu-id="40d2b-110">환경 변수</span><span class="sxs-lookup"><span data-stu-id="40d2b-110">Environment variables</span></span>

<span data-ttu-id="40d2b-111">응용 프로그램 보안 코드 또는 로컬 구성 파일의 저장소를 방지 하기 위해 환경 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-111">Environment variables are used to avoid storage of app secrets in code or in local configuration files.</span></span> <span data-ttu-id="40d2b-112">환경 변수는 모든 이전에 지정 된 구성 소스에 대 한 구성 값을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-112">Environment variables override configuration values for all previously specified configuration sources.</span></span>

::: moniker range="<= aspnetcore-1.1"
<span data-ttu-id="40d2b-113">호출 하 여 환경 변수 값을 읽는 구성 [AddEnvironmentVariables](/dotnet/api/microsoft.extensions.configuration.environmentvariablesextensions.addenvironmentvariables) 에 `Startup` 생성자:</span><span class="sxs-lookup"><span data-stu-id="40d2b-113">Configure the reading of environment variable values by calling [AddEnvironmentVariables](/dotnet/api/microsoft.extensions.configuration.environmentvariablesextensions.addenvironmentvariables) in the `Startup` constructor:</span></span>

<span data-ttu-id="40d2b-114">[!code-csharp[](app-secrets/samples/1.1/UserSecrets/Startup.cs?name=snippet_StartupConstructor&highlight=10)]</span><span class="sxs-lookup"><span data-stu-id="40d2b-114">[!code-csharp[](app-secrets/samples/1.1/UserSecrets/Startup.cs?name=snippet_StartupConstructor&highlight=10)]</span></span>
::: moniker-end

<span data-ttu-id="40d2b-115">ASP.NET Core 웹 응용 프로그램 고려 **개별 사용자 계정** 보안을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-115">Consider an ASP.NET Core web app in which **Individual User Accounts** security is enabled.</span></span> <span data-ttu-id="40d2b-116">프로젝트의 기본 데이터베이스 연결 문자열을 포함 되어 *appsettings.json* 키와 파일 `DefaultConnection`합니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-116">A default database connection string is included in the project's *appsettings.json* file with the key `DefaultConnection`.</span></span> <span data-ttu-id="40d2b-117">기본 연결 문자열은 localdb 사용자 모드에서 실행 되 고 암호가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-117">The default connection string is for LocalDB, which runs in user mode and doesn't require a password.</span></span> <span data-ttu-id="40d2b-118">응용 프로그램 배포 시는 `DefaultConnection` 환경 변수 값과 키 값을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-118">During app deployment, the `DefaultConnection` key value can be overridden with an environment variable's value.</span></span> <span data-ttu-id="40d2b-119">환경 변수는 중요 한 자격 증명으로 완전 한 연결 문자열을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-119">The environment variable may store the complete connection string with sensitive credentials.</span></span>

> [!WARNING]
> <span data-ttu-id="40d2b-120">환경 변수는 일반적으로 암호화 되지 않은 일반 텍스트에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-120">Environment variables are generally stored in plain, unencrypted text.</span></span> <span data-ttu-id="40d2b-121">컴퓨터 또는 프로세스가 손상 되 면 환경 변수는 신뢰할 수 없는 당사자가 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-121">If the machine or process is compromised, environment variables can be accessed by untrusted parties.</span></span> <span data-ttu-id="40d2b-122">사용자의 비밀으로 공개 되지 않도록 추가 조치가 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-122">Additional measures to prevent disclosure of user secrets may be required.</span></span>

## <a name="secret-manager"></a><span data-ttu-id="40d2b-123">Secret Manager</span><span class="sxs-lookup"><span data-stu-id="40d2b-123">Secret Manager</span></span>

<span data-ttu-id="40d2b-124">암호 관리자 도구는 ASP.NET Core 프로젝트를 개발 하는 동안 중요 한 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-124">The Secret Manager tool stores sensitive data during the development of an ASP.NET Core project.</span></span> <span data-ttu-id="40d2b-125">이 컨텍스트에서 중요 한 데이터 조각이 응용 프로그램 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-125">In this context, a piece of sensitive data is an app secret.</span></span> <span data-ttu-id="40d2b-126">앱 암호는 프로젝트 트리에서 별도 위치에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-126">App secrets are stored in a separate location from the project tree.</span></span> <span data-ttu-id="40d2b-127">앱 암호는 특정 프로젝트와 관련 된 또는 여러 프로젝트 간에 공유 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-127">The app secrets are associated with a specific project or shared across several projects.</span></span> <span data-ttu-id="40d2b-128">앱 암호는 소스 제어에 체크 인 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-128">The app secrets aren't checked into source control.</span></span>

> [!WARNING]
> <span data-ttu-id="40d2b-129">암호 관리자 도구 저장 된 암호를 암호화 하지 않습니다 하 고 신뢰할 수 있는 저장소로 처리 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-129">The Secret Manager tool doesn't encrypt the stored secrets and shouldn't be treated as a trusted store.</span></span> <span data-ttu-id="40d2b-130">개발 용도로입니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-130">It's for development purposes only.</span></span> <span data-ttu-id="40d2b-131">키와 값은 사용자 프로필 디렉터리에 위치한 JSON 구성 파일에 저장됩니다. </span><span class="sxs-lookup"><span data-stu-id="40d2b-131">The keys and values are stored in a JSON configuration file in the user profile directory.</span></span>

## <a name="how-the-secret-manager-tool-works"></a><span data-ttu-id="40d2b-132">Secret Manager 도구의 동작 방식</span><span class="sxs-lookup"><span data-stu-id="40d2b-132">How the Secret Manager tool works</span></span>

<span data-ttu-id="40d2b-133">Secret Manager 도구는 값이 저장되는 위치 및 방법 같은 구현에 관한 세부적인 내용을 추상화합니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-133">The Secret Manager tool abstracts away the implementation details, such as where and how the values are stored.</span></span> <span data-ttu-id="40d2b-134">이런 세부적인 내용을 모르더라도 Secret Manager 도구를 사용하는 데는 아무런 지장이 없습니다. </span><span class="sxs-lookup"><span data-stu-id="40d2b-134">You can use the tool without knowing these implementation details.</span></span> <span data-ttu-id="40d2b-135">값에 저장 되는 [JSON](https://json.org/) 로컬 컴퓨터에서 시스템으로 보호 된 사용자 프로필 폴더에 구성 파일:</span><span class="sxs-lookup"><span data-stu-id="40d2b-135">The values are stored in a [JSON](https://json.org/) configuration file in a system-protected user profile folder on the local machine:</span></span>

# <a name="windowstabwindows"></a>[<span data-ttu-id="40d2b-136">Windows</span><span class="sxs-lookup"><span data-stu-id="40d2b-136">Windows</span></span>](#tab/windows)

<span data-ttu-id="40d2b-137">파일 시스템 경로:</span><span class="sxs-lookup"><span data-stu-id="40d2b-137">File system path:</span></span>

`%APPDATA%\Microsoft\UserSecrets\<user_secrets_id>\secrets.json`

# <a name="macostabmacos"></a>[<span data-ttu-id="40d2b-138">macOS</span><span class="sxs-lookup"><span data-stu-id="40d2b-138">macOS</span></span>](#tab/macos)

<span data-ttu-id="40d2b-139">파일 시스템 경로:</span><span class="sxs-lookup"><span data-stu-id="40d2b-139">File system path:</span></span>

`~/.microsoft/usersecrets/<user_secrets_id>/secrets.json`

# <a name="linuxtablinux"></a>[<span data-ttu-id="40d2b-140">Linux</span><span class="sxs-lookup"><span data-stu-id="40d2b-140">Linux</span></span>](#tab/linux)

<span data-ttu-id="40d2b-141">파일 시스템 경로:</span><span class="sxs-lookup"><span data-stu-id="40d2b-141">File system path:</span></span>

`~/.microsoft/usersecrets/<user_secrets_id>/secrets.json`

---

<span data-ttu-id="40d2b-142">앞의 파일 경로, 대체 `<user_secrets_id>` 와 `UserSecretsId` 에 지정 된 값의 *.csproj* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-142">In the preceding file paths, replace `<user_secrets_id>` with the `UserSecretsId` value specified in the *.csproj* file.</span></span>

<span data-ttu-id="40d2b-143">위치 또는 보안 관리자 도구와 함께 저장 되는 데이터의 형식에 의존 하는 코드를 작성 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="40d2b-143">Don't write code that depends on the location or format of data saved with the Secret Manager tool.</span></span> <span data-ttu-id="40d2b-144">이러한 구현 정보를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-144">These implementation details may change.</span></span> <span data-ttu-id="40d2b-145">예를 들어 비밀 값 암호화 되지 않습니다 되지만 나중에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-145">For example, the secret values aren't encrypted, but could be in the future.</span></span>

::: moniker range="<= aspnetcore-2.0"
## <a name="install-the-secret-manager-tool"></a><span data-ttu-id="40d2b-146">암호 관리자 도구를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-146">Install the Secret Manager tool</span></span>

<span data-ttu-id="40d2b-147">암호 관리자 도구는.NET Core SDK 2.1에서.NET Core CLI 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-147">The Secret Manager tool is bundled with the .NET Core CLI in .NET Core SDK 2.1.</span></span> <span data-ttu-id="40d2b-148">.NET Core SDK 2.0 및 이전 버전에서 도구를 설치 해야만 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-148">For .NET Core SDK 2.0 and earlier, tool installation is necessary.</span></span>

<span data-ttu-id="40d2b-149">설치는 [Microsoft.Extensions.SecretManager.Tools](https://www.nuget.org/packages/Microsoft.Extensions.SecretManager.Tools/) ASP.NET Core 프로젝트에 NuGet 패키지:</span><span class="sxs-lookup"><span data-stu-id="40d2b-149">Install the [Microsoft.Extensions.SecretManager.Tools](https://www.nuget.org/packages/Microsoft.Extensions.SecretManager.Tools/) NuGet package in your ASP.NET Core project:</span></span>

<span data-ttu-id="40d2b-150">[!code-xml[](app-secrets/samples/1.1/UserSecrets/UserSecrets.csproj?name=snippet_CsprojFile&highlight=13-14)]</span><span class="sxs-lookup"><span data-stu-id="40d2b-150">[!code-xml[](app-secrets/samples/1.1/UserSecrets/UserSecrets.csproj?name=snippet_CsprojFile&highlight=13-14)]</span></span>

<span data-ttu-id="40d2b-151">도구 설치를 확인 하는 명령 셸에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-151">Execute the following command in a command shell to validate the tool installation:</span></span>

```console
dotnet user-secrets -h
```

<span data-ttu-id="40d2b-152">암호 관리자 도구 사용법 예제, 옵션 및 명령 도움말을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-152">The Secret Manager tool displays sample usage, options, and command help:</span></span>

```console
Usage: dotnet user-secrets [options] [command]

Options:
  -?|-h|--help                        Show help information
  --version                           Show version information
  -v|--verbose                        Show verbose output
  -p|--project <PROJECT>              Path to project. Defaults to searching the current directory.
  -c|--configuration <CONFIGURATION>  The project configuration to use. Defaults to 'Debug'.
  --id                                The user secret ID to use.

Commands:
  clear   Deletes all the application secrets
  list    Lists all the application secrets
  remove  Removes the specified user secret
  set     Sets the user secret to the specified value

Use "dotnet user-secrets [command] --help" for more information about a command.
```

> [!NOTE]
> <span data-ttu-id="40d2b-153">와 같은 디렉터리에 있어야는 *.csproj* 파일에 정의 된 도구를 실행 하는 *.csproj* 파일의 `DotNetCliToolReference` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-153">You must be in the same directory as the *.csproj* file to run tools defined in the *.csproj* file's `DotNetCliToolReference` elements.</span></span>
::: moniker-end

## <a name="set-a-secret"></a><span data-ttu-id="40d2b-154">암호를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-154">Set a secret</span></span>

<span data-ttu-id="40d2b-155">암호 관리자 도구는 사용자 프로필에 저장 된 프로젝트 관련 구성 설정에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-155">The Secret Manager tool operates on project-specific configuration settings stored in your user profile.</span></span> <span data-ttu-id="40d2b-156">사용자 암호를 사용 하려면 정의 `UserSecretsId` 요소 내에서 한 `PropertyGroup` 의 *.csproj* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-156">To use user secrets, define a `UserSecretsId` element within a `PropertyGroup` of the *.csproj* file.</span></span> <span data-ttu-id="40d2b-157">값 `UserSecretsId` 은 선택적 요소 이지만 프로젝트에 고유 합니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-157">The value of `UserSecretsId` is arbitrary, but is unique to the project.</span></span> <span data-ttu-id="40d2b-158">개발자는 대부분 `UserSecretsId` 값에 GUID를 생성해서 지정합니다. </span><span class="sxs-lookup"><span data-stu-id="40d2b-158">Developers typically generate a GUID for the `UserSecretsId`.</span></span>

::: moniker range="<= aspnetcore-1.1"
<span data-ttu-id="40d2b-159">[!code-xml[](app-secrets/samples/1.1/UserSecrets/UserSecrets.csproj?name=snippet_PropertyGroup&highlight=3)]</span><span class="sxs-lookup"><span data-stu-id="40d2b-159">[!code-xml[](app-secrets/samples/1.1/UserSecrets/UserSecrets.csproj?name=snippet_PropertyGroup&highlight=3)]</span></span>
::: moniker-end
::: moniker range=">= aspnetcore-2.0"
<span data-ttu-id="40d2b-160">[!code-xml[](app-secrets/samples/2.1/UserSecrets/UserSecrets.csproj?name=snippet_PropertyGroup&highlight=3)]</span><span class="sxs-lookup"><span data-stu-id="40d2b-160">[!code-xml[](app-secrets/samples/2.1/UserSecrets/UserSecrets.csproj?name=snippet_PropertyGroup&highlight=3)]</span></span>
::: moniker-end

> [!TIP]
> <span data-ttu-id="40d2b-161">Visual Studio에서 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **관리 사용자의 비밀** 상황에 맞는 메뉴입니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-161">In Visual Studio, right-click the project in Solution Explorer, and select **Manage User Secrets** from the context menu.</span></span> <span data-ttu-id="40d2b-162">이 제스처 추가 `UserSecretsId` 에 GUID로 채워진 요소는 *.csproj* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-162">This gesture adds a `UserSecretsId` element, populated with a GUID, to the *.csproj* file.</span></span> <span data-ttu-id="40d2b-163">Visual Studio가 열릴는 *secrets.json* 파일 텍스트 편집기에서.</span><span class="sxs-lookup"><span data-stu-id="40d2b-163">Visual Studio opens a *secrets.json* file in the text editor.</span></span> <span data-ttu-id="40d2b-164">내용을 대체 *secrets.json* 저장할 키-값 쌍을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-164">Replace the contents of *secrets.json* with the key-value pairs to be stored.</span></span> <span data-ttu-id="40d2b-165">예를 들면 [!INCLUDE[secrets.json file](~/includes/app-secrets/secrets-json-file.md)] 같은 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-165">For example: [!INCLUDE[secrets.json file](~/includes/app-secrets/secrets-json-file.md)]</span></span>

<span data-ttu-id="40d2b-166">키와 해당 값으로 구성 된 앱 암호를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-166">Define an app secret consisting of a key and its value.</span></span> <span data-ttu-id="40d2b-167">암호는 해당 프로젝트와 관련 `UserSecretsId` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-167">The secret is associated with the project's `UserSecretsId` value.</span></span> <span data-ttu-id="40d2b-168">예를 들어 있는 디렉터리에서 다음 명령을 실행는 *.csproj* 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-168">For example, run the following command from the directory in which the *.csproj* file exists:</span></span>

```console
dotnet user-secrets set "Movies:ServiceApiKey" "12345"
```

<span data-ttu-id="40d2b-169">앞의 예제에서 콜론 나타냅니다 `Movies` 은 개체 리터럴을 `ServiceApiKey` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-169">In the preceding example, the colon denotes that `Movies` is an object literal with a `ServiceApiKey` property.</span></span>

<span data-ttu-id="40d2b-170">암호 관리자 도구는 너무 다른 디렉터리에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-170">The Secret Manager tool can be used from other directories too.</span></span> <span data-ttu-id="40d2b-171">사용 하 여는 `--project` 옵션을 파일 시스템 경로 제공 하는 *.csproj* 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-171">Use the `--project` option to supply the file system path at which the *.csproj* file exists.</span></span> <span data-ttu-id="40d2b-172">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="40d2b-172">For example:</span></span>

```console
dotnet user-secrets set "Movies:ServiceApiKey" "12345" --project "C:\apps\WebApp1\src\WebApp1"
```

## <a name="set-multiple-secrets"></a><span data-ttu-id="40d2b-173">여러 암호를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-173">Set multiple secrets</span></span>

<span data-ttu-id="40d2b-174">JSON에 파이프 하 여 보안의 일괄 처리를 설정할 수 있습니다는 `set` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-174">A batch of secrets can be set by piping JSON to the `set` command.</span></span> <span data-ttu-id="40d2b-175">다음 예제에서는 *input.json* 파일의 내용으로 파이프 되는 `set` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-175">In the following example, the *input.json* file's contents are piped to the `set` command.</span></span>

# <a name="windowstabwindows"></a>[<span data-ttu-id="40d2b-176">Windows</span><span class="sxs-lookup"><span data-stu-id="40d2b-176">Windows</span></span>](#tab/windows)

<span data-ttu-id="40d2b-177">명령 셸을 열고 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-177">Open a command shell, and execute the following command:</span></span>

  ```console
  type .\input.json | dotnet user-secrets set
  ```

# <a name="macostabmacos"></a>[<span data-ttu-id="40d2b-178">macOS</span><span class="sxs-lookup"><span data-stu-id="40d2b-178">macOS</span></span>](#tab/macos)

<span data-ttu-id="40d2b-179">명령 셸을 열고 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-179">Open a command shell, and execute the following command:</span></span>

  ```console
  cat ./input.json | dotnet user-secrets set
  ```

# <a name="linuxtablinux"></a>[<span data-ttu-id="40d2b-180">Linux</span><span class="sxs-lookup"><span data-stu-id="40d2b-180">Linux</span></span>](#tab/linux)

<span data-ttu-id="40d2b-181">명령 셸을 열고 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-181">Open a command shell, and execute the following command:</span></span>

  ```console
  cat ./input.json | dotnet user-secrets set
  ```

---

## <a name="access-a-secret"></a><span data-ttu-id="40d2b-182">암호에 액세스</span><span class="sxs-lookup"><span data-stu-id="40d2b-182">Access a secret</span></span>

<span data-ttu-id="40d2b-183">[ASP.NET Core 구성 API](xref:fundamentals/configuration/index) 보안 관리자 암호에 대 한 액세스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-183">The [ASP.NET Core Configuration API](xref:fundamentals/configuration/index) provides access to Secret Manager secrets.</span></span> <span data-ttu-id="40d2b-184">.NET Core를 대상으로 1.x 또는.NET Framework 설치는 [Microsoft.Extensions.Configuration.UserSecrets](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.UserSecrets) NuGet 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-184">If targeting .NET Core 1.x or .NET Framework, install the [Microsoft.Extensions.Configuration.UserSecrets](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.UserSecrets) NuGet package.</span></span>

::: moniker range="<= aspnetcore-1.1"
<span data-ttu-id="40d2b-185">사용자 암호 구성 소스를 추가 `Startup` 생성자:</span><span class="sxs-lookup"><span data-stu-id="40d2b-185">Add the user secrets configuration source to the `Startup` constructor:</span></span>

<span data-ttu-id="40d2b-186">[!code-csharp[](app-secrets/samples/1.1/UserSecrets/Startup.cs?name=snippet_StartupConstructor&highlight=5-8)]</span><span class="sxs-lookup"><span data-stu-id="40d2b-186">[!code-csharp[](app-secrets/samples/1.1/UserSecrets/Startup.cs?name=snippet_StartupConstructor&highlight=5-8)]</span></span>
::: moniker-end

<span data-ttu-id="40d2b-187">사용자 암호를 통해 검색할 수 있습니다는 `Configuration` API:</span><span class="sxs-lookup"><span data-stu-id="40d2b-187">User secrets can be retrieved via the `Configuration` API:</span></span>

::: moniker range="<= aspnetcore-1.1"
<span data-ttu-id="40d2b-188">[!code-csharp[](app-secrets/samples/1.1/UserSecrets/Startup.cs?name=snippet_StartupClass&highlight=23)]</span><span class="sxs-lookup"><span data-stu-id="40d2b-188">[!code-csharp[](app-secrets/samples/1.1/UserSecrets/Startup.cs?name=snippet_StartupClass&highlight=23)]</span></span>
::: moniker-end
::: moniker range=">= aspnetcore-2.0"
<span data-ttu-id="40d2b-189">[!code-csharp[](app-secrets/samples/2.1/UserSecrets/Startup.cs?name=snippet_StartupClass&highlight=14)]</span><span class="sxs-lookup"><span data-stu-id="40d2b-189">[!code-csharp[](app-secrets/samples/2.1/UserSecrets/Startup.cs?name=snippet_StartupClass&highlight=14)]</span></span>
::: moniker-end

## <a name="string-replacement-with-secrets"></a><span data-ttu-id="40d2b-190">암호와 문자열 대체</span><span class="sxs-lookup"><span data-stu-id="40d2b-190">String replacement with secrets</span></span>

<span data-ttu-id="40d2b-191">일반 텍스트에 암호를 저장 하는 것은 위험 합니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-191">Storing passwords in plain text is risky.</span></span> <span data-ttu-id="40d2b-192">데이터베이스 연결 문자열에 저장 하는 예를 들어 *appsettings.json* 지정된 된 사용자에 대 한 암호를 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-192">For example, a database connection string stored in *appsettings.json* may include a password for the specified user:</span></span>

[!code-json[](app-secrets/samples/2.1/UserSecrets/appsettings-unsecure.json?highlight=3)]

<span data-ttu-id="40d2b-193">암호로 암호를 저장 하는 보다 안전한 방법이입니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-193">A more secure approach is to store the password as a secret.</span></span> <span data-ttu-id="40d2b-194">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="40d2b-194">For example:</span></span>

```console
dotnet user-secrets set "DbPassword" "pass123"
```

<span data-ttu-id="40d2b-195">암호를 대체할 *appsettings.json* 을 자리 표시자입니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-195">Replace the password in *appsettings.json* with a placeholder.</span></span> <span data-ttu-id="40d2b-196">다음 예에서 `{0}` 폼에 자리 표시자로 사용 되는 [복합 형식 문자열](/dotnet/standard/base-types/composite-formatting#composite-format-string)합니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-196">In the following example, `{0}` is used as the placeholder to form a [Composite Format String](/dotnet/standard/base-types/composite-formatting#composite-format-string).</span></span>

[!code-json[](app-secrets/samples/2.1/UserSecrets/appsettings.json?highlight=3)]

<span data-ttu-id="40d2b-197">연결 문자열을 완료 하려면 자리 표시자에 암호의 값을 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-197">The secret's value can be injected into the placeholder to complete the connection string:</span></span>

::: moniker range="<= aspnetcore-1.1"
<span data-ttu-id="40d2b-198">[!code-csharp[](app-secrets/samples/1.1/UserSecrets/Startup2.cs?name=snippet_StartupClass&highlight=23-25)]</span><span class="sxs-lookup"><span data-stu-id="40d2b-198">[!code-csharp[](app-secrets/samples/1.1/UserSecrets/Startup2.cs?name=snippet_StartupClass&highlight=23-25)]</span></span>
::: moniker-end
::: moniker range=">= aspnetcore-2.0"
<span data-ttu-id="40d2b-199">[!code-csharp[](app-secrets/samples/2.1/UserSecrets/Startup2.cs?name=snippet_StartupClass&highlight=14-16)]</span><span class="sxs-lookup"><span data-stu-id="40d2b-199">[!code-csharp[](app-secrets/samples/2.1/UserSecrets/Startup2.cs?name=snippet_StartupClass&highlight=14-16)]</span></span>
::: moniker-end

## <a name="list-the-secrets"></a><span data-ttu-id="40d2b-200">암호 나열</span><span class="sxs-lookup"><span data-stu-id="40d2b-200">List the secrets</span></span>

[!INCLUDE[secrets.json file](~/includes/app-secrets/secrets-json-file-and-text.md)]

<span data-ttu-id="40d2b-201">디렉터리에서 다음 명령을 실행는 *.csproj* 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-201">Run the following command from the directory in which the *.csproj* file exists:</span></span>

```console
dotnet user-secrets list
```

<span data-ttu-id="40d2b-202">다음과 같은 출력이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-202">The following output appears:</span></span>

```console
Movies:ServiceApiKey = 12345
Movies:ConnectionString = Server=(localdb)\mssqllocaldb;Database=Movie-1;Trusted_Connection=True;MultipleActiveResultSets=true
```

<span data-ttu-id="40d2b-203">키 이름에 콜론 앞의 예제에서 내에서 개체 계층 구조를 나타냅니다 *secrets.json*합니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-203">In the preceding example, a colon in the key names denotes the object hierarchy within *secrets.json*.</span></span>

## <a name="remove-a-single-secret"></a><span data-ttu-id="40d2b-204">단일 암호를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-204">Remove a single secret</span></span>

[!INCLUDE[secrets.json file](~/includes/app-secrets/secrets-json-file-and-text.md)]

<span data-ttu-id="40d2b-205">디렉터리에서 다음 명령을 실행는 *.csproj* 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-205">Run the following command from the directory in which the *.csproj* file exists:</span></span>

```console
dotnet user-secrets remove "Movies:ConnectionString"
```

<span data-ttu-id="40d2b-206">응용 프로그램의 *secrets.json* 와 연결 된 키-값 쌍을 제거 하려면 파일을 수정한는 `MoviesConnectionString` 키:</span><span class="sxs-lookup"><span data-stu-id="40d2b-206">The app's *secrets.json* file was modified to remove the key-value pair associated with the `MoviesConnectionString` key:</span></span>

```json
{
  "Movies": {
    "ServiceApiKey": "12345"
  }
}
```

<span data-ttu-id="40d2b-207">실행 `dotnet user-secrets list` 다음 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-207">Running `dotnet user-secrets list` displays the following message:</span></span>

```console
Movies:ServiceApiKey = 12345
```

## <a name="remove-all-secrets"></a><span data-ttu-id="40d2b-208">모든 암호를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-208">Remove all secrets</span></span>

[!INCLUDE[secrets.json file](~/includes/app-secrets/secrets-json-file-and-text.md)]

<span data-ttu-id="40d2b-209">디렉터리에서 다음 명령을 실행는 *.csproj* 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-209">Run the following command from the directory in which the *.csproj* file exists:</span></span>

```console
dotnet user-secrets clear
```

<span data-ttu-id="40d2b-210">삭제 된 응용 프로그램에 대 한 모든 사용자 암호는 *secrets.json* 파일:</span><span class="sxs-lookup"><span data-stu-id="40d2b-210">All user secrets for the app have been deleted from the *secrets.json* file:</span></span>

```json
{}
```

<span data-ttu-id="40d2b-211">실행 `dotnet user-secrets list` 다음 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40d2b-211">Running `dotnet user-secrets list` displays the following message:</span></span>

```console
No secrets configured for this application.
```

## <a name="additional-resources"></a><span data-ttu-id="40d2b-212">추가 자료</span><span class="sxs-lookup"><span data-stu-id="40d2b-212">Additional resources</span></span>

* <xref:fundamentals/configuration/index>
* <xref:security/key-vault-configuration>