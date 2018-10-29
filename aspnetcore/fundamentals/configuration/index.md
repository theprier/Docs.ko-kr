---
title: ASP.NET Core의 구성
author: guardrex
description: 구성 API를 사용하여 ASP.NET Core 앱을 구성하는 방법을 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 10/09/2018
uid: fundamentals/configuration/index
ms.openlocfilehash: cbc48222aeb4a1d23144bfb70aece5a83a700d09
ms.sourcegitcommit: 375e9a67f5e1f7b0faaa056b4b46294cc70f55b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50207903"
---
# <a name="configuration-in-aspnet-core"></a><span data-ttu-id="5260e-103">ASP.NET Core의 구성</span><span class="sxs-lookup"><span data-stu-id="5260e-103">Configuration in ASP.NET Core</span></span>

<span data-ttu-id="5260e-104">[Luke Latham](https://github.com/guardrex)으로</span><span class="sxs-lookup"><span data-stu-id="5260e-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="5260e-105">ASP.NET Core의 앱 구성은 ‘구성 공급자’가 설정한 키-값 쌍을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-105">App configuration in ASP.NET Core is based on key-value pairs established by *configuration providers*.</span></span> <span data-ttu-id="5260e-106">구성 공급자는 다양한 구성 소스에서 구성 데이터를 키-값 쌍으로 읽어 들입니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-106">Configuration providers read configuration data into key-value pairs from a variety of configuration sources:</span></span>

::: moniker range=">= aspnetcore-2.1"

* <span data-ttu-id="5260e-107">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="5260e-107">Azure Key Vault</span></span>
* <span data-ttu-id="5260e-108">명령줄 인수</span><span class="sxs-lookup"><span data-stu-id="5260e-108">Command-line arguments</span></span>
* <span data-ttu-id="5260e-109">사용자 지정 공급자(설치 또는 생성된)</span><span class="sxs-lookup"><span data-stu-id="5260e-109">Custom providers (installed or created)</span></span>
* <span data-ttu-id="5260e-110">디렉터리 파일</span><span class="sxs-lookup"><span data-stu-id="5260e-110">Directory files</span></span>
* <span data-ttu-id="5260e-111">환경 변수</span><span class="sxs-lookup"><span data-stu-id="5260e-111">Environment variables</span></span>
* <span data-ttu-id="5260e-112">메모리 내 .NET 개체</span><span class="sxs-lookup"><span data-stu-id="5260e-112">In-memory .NET objects</span></span>
* <span data-ttu-id="5260e-113">설정 파일</span><span class="sxs-lookup"><span data-stu-id="5260e-113">Settings files</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0 || aspnetcore-1.1"

* <span data-ttu-id="5260e-114">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="5260e-114">Azure Key Vault</span></span>
* <span data-ttu-id="5260e-115">명령줄 인수</span><span class="sxs-lookup"><span data-stu-id="5260e-115">Command-line arguments</span></span>
* <span data-ttu-id="5260e-116">사용자 지정 공급자(설치 또는 생성된)</span><span class="sxs-lookup"><span data-stu-id="5260e-116">Custom providers (installed or created)</span></span>
* <span data-ttu-id="5260e-117">환경 변수</span><span class="sxs-lookup"><span data-stu-id="5260e-117">Environment variables</span></span>
* <span data-ttu-id="5260e-118">메모리 내 .NET 개체</span><span class="sxs-lookup"><span data-stu-id="5260e-118">In-memory .NET objects</span></span>
* <span data-ttu-id="5260e-119">설정 파일</span><span class="sxs-lookup"><span data-stu-id="5260e-119">Settings files</span></span>

::: moniker-end

::: moniker range="= aspnetcore-1.0"

* <span data-ttu-id="5260e-120">명령줄 인수</span><span class="sxs-lookup"><span data-stu-id="5260e-120">Command-line arguments</span></span>
* <span data-ttu-id="5260e-121">사용자 지정 공급자(설치 또는 생성된)</span><span class="sxs-lookup"><span data-stu-id="5260e-121">Custom providers (installed or created)</span></span>
* <span data-ttu-id="5260e-122">환경 변수</span><span class="sxs-lookup"><span data-stu-id="5260e-122">Environment variables</span></span>
* <span data-ttu-id="5260e-123">메모리 내 .NET 개체</span><span class="sxs-lookup"><span data-stu-id="5260e-123">In-memory .NET objects</span></span>
* <span data-ttu-id="5260e-124">설정 파일</span><span class="sxs-lookup"><span data-stu-id="5260e-124">Settings files</span></span>

::: moniker-end

<span data-ttu-id="5260e-125">‘옵션 패턴’은 이 항목에 설명된 구성 개념의 확장입니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-125">The *options pattern* is an extension of the configuration concepts described in this topic.</span></span> <span data-ttu-id="5260e-126">옵션은 클래스를 사용하여 관련 설정 그룹을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-126">Options uses classes to represent groups of related settings.</span></span> <span data-ttu-id="5260e-127">옵션 패턴 사용에 대한 자세한 내용은 <xref:fundamentals/configuration/options>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5260e-127">For more information on using the options pattern, see <xref:fundamentals/configuration/options>.</span></span>

<span data-ttu-id="5260e-128">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/index/samples)([다운로드 방법](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="5260e-128">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/index/samples) ([how to download](xref:index#how-to-download-a-sample))</span></span>

<span data-ttu-id="5260e-129">이 항목에서 제공하는 예제는 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-129">The examples provided in this topic rely upon:</span></span>

* <span data-ttu-id="5260e-130"><xref:Microsoft.Extensions.Configuration.FileConfigurationExtensions.SetBasePath*>를 사용하여 앱의 기본 경로 설정.</span><span class="sxs-lookup"><span data-stu-id="5260e-130">Setting the base path of the app with <xref:Microsoft.Extensions.Configuration.FileConfigurationExtensions.SetBasePath*>.</span></span> <span data-ttu-id="5260e-131">`SetBasePath`는 [Microsoft.Extensions.Configuration.FileExtensions](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.FileExtensions/) 패키지를 참조하여 앱에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-131">`SetBasePath` is made available to an app by referencing the [Microsoft.Extensions.Configuration.FileExtensions](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.FileExtensions/) package.</span></span>
* <span data-ttu-id="5260e-132"><xref:Microsoft.Extensions.Configuration.ConfigurationSection.GetSection*>을 사용하여 구성 파일의 섹션 확인.</span><span class="sxs-lookup"><span data-stu-id="5260e-132">Resolving sections of configuration files with <xref:Microsoft.Extensions.Configuration.ConfigurationSection.GetSection*>.</span></span> <span data-ttu-id="5260e-133">`GetSection`은 [Microsoft.Extensions.Configuration](https://www.nuget.org/packages/Microsoft.Extensions.Configuration/) 패키지를 참조하여 앱에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-133">`GetSection` is made available to an app by referencing the [Microsoft.Extensions.Configuration](https://www.nuget.org/packages/Microsoft.Extensions.Configuration/) package.</span></span>
* <span data-ttu-id="5260e-134"><xref:Microsoft.Extensions.Configuration.ConfigurationBinder.Bind*> 및 [Get&lt;T&gt;](xref:Microsoft.Extensions.Configuration.ConfigurationBinder.Get*)을 사용하여 구성을 .NET 클래스에 바인딩.</span><span class="sxs-lookup"><span data-stu-id="5260e-134">Binding configuration to .NET classes with <xref:Microsoft.Extensions.Configuration.ConfigurationBinder.Bind*> and [Get&lt;T&gt;](xref:Microsoft.Extensions.Configuration.ConfigurationBinder.Get*).</span></span> <span data-ttu-id="5260e-135">`Bind` 및 `Get<T>`는 [Microsoft.Extensions.Configuration.Binder](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.Binder/) 패키지를 참조하여 앱에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-135">`Bind` and `Get<T>` are made available to an app by referencing the [Microsoft.Extensions.Configuration.Binder](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.Binder/) package.</span></span> <span data-ttu-id="5260e-136">`Get<T>`는 ASP.NET Core 1.1 이상에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-136">`Get<T>` is available in ASP.NET Core 1.1 or later.</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="5260e-137">이러한 세 패키지는 [Microsoft.AspNetCore.App 메타패키지](xref:fundamentals/metapackage-app)에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-137">These three packages are included in the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app).</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="5260e-138">이러한 세 패키지는 [Microsoft.AspNetCore.All 메타패키지](xref:fundamentals/metapackage)에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-138">These three packages are included in the [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage).</span></span>

::: moniker-end

## <a name="host-vs-app-configuration"></a><span data-ttu-id="5260e-139">호스트 및 앱 구성</span><span class="sxs-lookup"><span data-stu-id="5260e-139">Host vs. app configuration</span></span>

<span data-ttu-id="5260e-140">앱을 구성하고 시작하기 전에 *호스트*를 구성하고 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-140">Before the app is configured and started, a *host* is configured and launched.</span></span> <span data-ttu-id="5260e-141">호스트는 앱 시작 및 수명 관리를 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-141">The host is responsible for app startup and lifetime management.</span></span> <span data-ttu-id="5260e-142">앱과 호스트 모두 이 항목에서 설명하는 구성 관리자를 사용하여 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-142">Both the app and the host are configured using the configuration providers described in this topic.</span></span> <span data-ttu-id="5260e-143">호스트 구성 키-값 쌍은 앱의 전역 구성에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-143">Host configuration key-value pairs become part of the app's global configuration.</span></span> <span data-ttu-id="5260e-144">호스트를 빌드할 때 구성 공급자를 사용하는 방법과 구성 소스가 호스트 구성에 미치는 영향에 대한 자세한 내용은 <xref:fundamentals/host/index>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5260e-144">For more information on how the configuration providers are used when the host is built and how configuration sources affect host configuration, see <xref:fundamentals/host/index>.</span></span>

## <a name="security"></a><span data-ttu-id="5260e-145">보안</span><span class="sxs-lookup"><span data-stu-id="5260e-145">Security</span></span>

<span data-ttu-id="5260e-146">다음 모범 사례를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="5260e-146">Adopt the following best practices:</span></span>

* <span data-ttu-id="5260e-147">구성 공급자 코드 또는 일반 텍스트 구성 파일에 암호 또는 기타 중요한 데이터를 절대 저장하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="5260e-147">Never store passwords or other sensitive data in configuration provider code or in plain text configuration files.</span></span>
* <span data-ttu-id="5260e-148">개발 또는 테스트 환경에서 프로덕션 비밀을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="5260e-148">Don't use production secrets in development or test environments.</span></span>
* <span data-ttu-id="5260e-149">의도치 않게 소스 코드 리포지토리에 커밋되는 일이 없도록 프로젝트 외부에서 비밀을 지정하세요.</span><span class="sxs-lookup"><span data-stu-id="5260e-149">Specify secrets outside of the project so that they can't be accidentally committed to a source code repository.</span></span>

<span data-ttu-id="5260e-150">[여러 환경을 사용하는 방법](xref:fundamentals/environments)과 [개발 시 비밀 관리자를 사용해 앱 비밀을 안전하게 보관](xref:security/app-secrets)하여 관리하는 방법(환경 변수를 사용하여 중요한 데이터를 저장하는 방법에 대한 조언 포함)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="5260e-150">Learn more about [how to use multiple environments](xref:fundamentals/environments) and managing the [safe storage of app secrets in development with the Secret Manager](xref:security/app-secrets) (includes advice on using environment variables to store sensitive data).</span></span> <span data-ttu-id="5260e-151">비밀 관리자는 파일 구성 공급자를 사용하여 사용자 비밀을 로컬 시스템의 JSON 파일에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-151">The Secret Manager uses the File Configuration Provider to store user secrets in a JSON file on the local system.</span></span> <span data-ttu-id="5260e-152">파일 구성 공급자에 대해서는 이 항목의 뒷부분에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-152">The File Configuration Provider is described later in this topic.</span></span>

<span data-ttu-id="5260e-153">[Azure Key Vault](https://azure.microsoft.com/services/key-vault/)는 앱 비밀을 안전하게 보관하기 위한 한 가지 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-153">[Azure Key Vault](https://azure.microsoft.com/services/key-vault/) is one option for the safe storage of app secrets.</span></span> <span data-ttu-id="5260e-154">자세한 내용은 <xref:security/key-vault-configuration>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5260e-154">For more information, see <xref:security/key-vault-configuration>.</span></span>

## <a name="hierarchical-configuration-data"></a><span data-ttu-id="5260e-155">계층적 구성 데이터</span><span class="sxs-lookup"><span data-stu-id="5260e-155">Hierarchical configuration data</span></span>

<span data-ttu-id="5260e-156">구성 API에서는 구성 키에 구분 기호를 사용해 계층적 데이터를 평면화하여 계층적 구성 데이터를 유지 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-156">The Configuration API is capable of maintaining hierarchical configuration data by flattening the hierarchical data with the use of a delimiter in the configuration keys.</span></span>

<span data-ttu-id="5260e-157">다음 JSON 파일에서는 두 섹션으로 이루어진 구조적 계층에 네 개의 키가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-157">In the following JSON file, four keys exist in a structured hierarchy of two sections:</span></span>

```json
{
  "section0": {
    "key0": "value",
    "key1": "value"
  },
  "section1": {
    "key0": "value",
    "key1": "value"
  }
}
```

<span data-ttu-id="5260e-158">파일을 구성으로 읽어 들이면 구성 소스의 원래 계층적 데이터 구조를 유지하기 위해 고유 키가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-158">When the file is read into configuration, unique keys are created to maintain the original hierarchical data structure of the configuration source.</span></span> <span data-ttu-id="5260e-159">콜론(`:`)을 사용해 섹션과 키를 평면화하여 원래 구조를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-159">The sections and keys are flattened with the use of a colon (`:`) to maintain the original structure:</span></span>

* <span data-ttu-id="5260e-160">section0:key0</span><span class="sxs-lookup"><span data-stu-id="5260e-160">section0:key0</span></span>
* <span data-ttu-id="5260e-161">section0:key1</span><span class="sxs-lookup"><span data-stu-id="5260e-161">section0:key1</span></span>
* <span data-ttu-id="5260e-162">section1:key0</span><span class="sxs-lookup"><span data-stu-id="5260e-162">section1:key0</span></span>
* <span data-ttu-id="5260e-163">section1:key1</span><span class="sxs-lookup"><span data-stu-id="5260e-163">section1:key1</span></span>

<span data-ttu-id="5260e-164">구성 데이터에서는 <xref:Microsoft.Extensions.Configuration.ConfigurationSection.GetSection*> 및 <xref:Microsoft.Extensions.Configuration.IConfiguration.GetChildren*> 메서드를 사용하여 섹션과 섹션의 자식을 격리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-164"><xref:Microsoft.Extensions.Configuration.ConfigurationSection.GetSection*> and <xref:Microsoft.Extensions.Configuration.IConfiguration.GetChildren*> methods are available to isolate sections and children of a section in the configuration data.</span></span> <span data-ttu-id="5260e-165">이러한 메서드에 대해서는 나중에 [GetSection, GetChildren 및 Exists](#getsection-getchildren-and-exists)에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-165">These methods are described later in [GetSection, GetChildren, and Exists](#getsection-getchildren-and-exists).</span></span>

## <a name="conventions"></a><span data-ttu-id="5260e-166">규칙</span><span class="sxs-lookup"><span data-stu-id="5260e-166">Conventions</span></span>

<span data-ttu-id="5260e-167">앱 시작 시 구성 공급자에서 지정한 순서로 구성 소스를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-167">At app startup, configuration sources are read in the order that their configuration providers are specified.</span></span>

<span data-ttu-id="5260e-168">파일 구성 공급자는 앱 시작 후 기본 설정 파일이 변경되면 구성을 다시 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-168">File Configuration Providers have the ability to reload configuration when an underlying settings file is changed after app startup.</span></span> <span data-ttu-id="5260e-169">파일 구성 공급자에 대해서는 이 항목의 뒷부분에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-169">The File Configuration Provider is described later in this topic.</span></span>

<span data-ttu-id="5260e-170"><xref:Microsoft.Extensions.Configuration.IConfiguration>은 앱의 [DI(종속성 주입)](xref:fundamentals/dependency-injection) 컨테이너에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-170"><xref:Microsoft.Extensions.Configuration.IConfiguration> is available in the app's [Dependency Injection (DI)](xref:fundamentals/dependency-injection) container.</span></span> <span data-ttu-id="5260e-171">구성 공급자는 호스트에서 설정될 때 DI가 제공되지 않으므로 DI를 활용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-171">Configuration providers can't utilize DI, as it's not available when they're set up by the host.</span></span>

<span data-ttu-id="5260e-172">구성키는 다음 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-172">Configuration keys adopt the following conventions:</span></span>

* <span data-ttu-id="5260e-173">키는 대/소문자를 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-173">Keys are case-insensitive.</span></span> <span data-ttu-id="5260e-174">예를 들어 `ConnectionString`과 `connectionstring`은 동일한 키로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-174">For example, `ConnectionString` and `connectionstring` are treated as equivalent keys.</span></span>
* <span data-ttu-id="5260e-175">같은 키의 값을 같거나 다른 여러 구성 공급자에서 설정하는 경우 키에 설정된 마지막 값이 사용되는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-175">If a value for the same key is set by the same or different configuration providers, the last value set on the key is the value used.</span></span>
* <span data-ttu-id="5260e-176">계층적 키</span><span class="sxs-lookup"><span data-stu-id="5260e-176">Hierarchical keys</span></span>
  * <span data-ttu-id="5260e-177">구성 API 내에서는 콜론 구분 기호(`:`)가 모든 플랫폼에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-177">Within the Configuration API, a colon separator (`:`) works on all platforms.</span></span>
  * <span data-ttu-id="5260e-178">환경 변수에서는 콜론 구분 기호가 일부 플랫폼에 적용되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-178">In environment variables, a colon separator may not work on all platforms.</span></span> <span data-ttu-id="5260e-179">두 개의 밑줄(`__`)은 모든 플랫폼에서 지원되며 콜론으로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-179">A double underscore (`__`) is supported by all platforms and is converted to a colon.</span></span>
  * <span data-ttu-id="5260e-180">Azure Key Vault에서 계층적 키는 `--`(두 개의 대시)를 구분 기호로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-180">In Azure Key Vault, hierarchical keys use `--` (two dashes) as a separator.</span></span> <span data-ttu-id="5260e-181">비밀을 앱의 구성으로 로드할 때 대시를 콜론으로 바꾸는 코드를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-181">You must provide code to replace the dashes with a colon when the secrets are loaded into the app's configuration.</span></span>
* <span data-ttu-id="5260e-182"><xref:Microsoft.Extensions.Configuration.ConfigurationBinder>는 구성 키에 배열 인덱스를 사용하여 배열을 개체에 바인딩하는 것을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-182">The <xref:Microsoft.Extensions.Configuration.ConfigurationBinder> supports binding arrays to objects using array indices in configuration keys.</span></span> <span data-ttu-id="5260e-183">배열 바인딩에 대해서는 [클래스에 배열 바인딩](#bind-an-array-to-a-class) 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-183">Array binding is described in the [Bind an array to a class](#bind-an-array-to-a-class) section.</span></span>

<span data-ttu-id="5260e-184">구성 값은 다음 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-184">Configuration values adopt the following conventions:</span></span>

* <span data-ttu-id="5260e-185">값은 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-185">Values are strings.</span></span>
* <span data-ttu-id="5260e-186">Null 값은 구성에 저장하거나 개체에 바인딩할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-186">Null values can't be stored in configuration or bound to objects.</span></span>

## <a name="providers"></a><span data-ttu-id="5260e-187">공급자</span><span class="sxs-lookup"><span data-stu-id="5260e-187">Providers</span></span>

<span data-ttu-id="5260e-188">다음 표에서는 ASP.NET Core 앱에서 사용할 수 있는 구성 공급자를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-188">The following table shows the configuration providers available to ASP.NET Core apps.</span></span>

::: moniker range=">= aspnetcore-2.1"

| <span data-ttu-id="5260e-189">공급자</span><span class="sxs-lookup"><span data-stu-id="5260e-189">Provider</span></span> | <span data-ttu-id="5260e-190">다음에서 구성 제공&hellip;</span><span class="sxs-lookup"><span data-stu-id="5260e-190">Provides configuration from&hellip;</span></span> |
| -------- | ----------------------------------- |
| <span data-ttu-id="5260e-191">[Azure Key Vault 구성 공급자](xref:security/key-vault-configuration)(‘보안’ 항목)</span><span class="sxs-lookup"><span data-stu-id="5260e-191">[Azure Key Vault Configuration Provider](xref:security/key-vault-configuration) (*Security* topics)</span></span> | <span data-ttu-id="5260e-192">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="5260e-192">Azure Key Vault</span></span> |
| [<span data-ttu-id="5260e-193">명령줄 구성 공급자</span><span class="sxs-lookup"><span data-stu-id="5260e-193">Command-line Configuration Provider</span></span>](#command-line-configuration-provider) | <span data-ttu-id="5260e-194">명령줄 매개 변수</span><span class="sxs-lookup"><span data-stu-id="5260e-194">Command-line parameters</span></span> |
| [<span data-ttu-id="5260e-195">사용자 지정 구성 공급자</span><span class="sxs-lookup"><span data-stu-id="5260e-195">Custom configuration provider</span></span>](#custom-configuration-provider) | <span data-ttu-id="5260e-196">사용자 지정 소스</span><span class="sxs-lookup"><span data-stu-id="5260e-196">Custom source</span></span> |
| [<span data-ttu-id="5260e-197">환경 변수 구성 공급자</span><span class="sxs-lookup"><span data-stu-id="5260e-197">Environment variables Configuration Provider</span></span>](#environment-variables-configuration-provider) | <span data-ttu-id="5260e-198">환경 변수</span><span class="sxs-lookup"><span data-stu-id="5260e-198">Environment variables</span></span> |
| [<span data-ttu-id="5260e-199">파일 구성 공급자</span><span class="sxs-lookup"><span data-stu-id="5260e-199">File Configuration Provider</span></span>](#file-configuration-provider) | <span data-ttu-id="5260e-200">파일(INI, JSON, XML)</span><span class="sxs-lookup"><span data-stu-id="5260e-200">Files (INI, JSON, XML)</span></span> |
| [<span data-ttu-id="5260e-201">파일별 키 구성 공급자</span><span class="sxs-lookup"><span data-stu-id="5260e-201">Key-per-file Configuration Provider</span></span>](#key-per-file-configuration-provider) | <span data-ttu-id="5260e-202">디렉터리 파일</span><span class="sxs-lookup"><span data-stu-id="5260e-202">Directory files</span></span> |
| [<span data-ttu-id="5260e-203">메모리 구성 공급자</span><span class="sxs-lookup"><span data-stu-id="5260e-203">Memory Configuration Provider</span></span>](#memory-configuration-provider) | <span data-ttu-id="5260e-204">메모리 내 컬렉션</span><span class="sxs-lookup"><span data-stu-id="5260e-204">In-memory collections</span></span> |
| <span data-ttu-id="5260e-205">[사용자 비밀(비밀 관리자)](xref:security/app-secrets)(‘보안’ 항목)</span><span class="sxs-lookup"><span data-stu-id="5260e-205">[User secrets (Secret Manager)](xref:security/app-secrets) (*Security* topics)</span></span> | <span data-ttu-id="5260e-206">사용자 프로필 디렉터리의 파일</span><span class="sxs-lookup"><span data-stu-id="5260e-206">File in the user profile directory</span></span> |

::: moniker-end

::: moniker range="= aspnetcore-2.0 || aspnetcore-1.1"

| <span data-ttu-id="5260e-207">공급자</span><span class="sxs-lookup"><span data-stu-id="5260e-207">Provider</span></span> | <span data-ttu-id="5260e-208">다음에서 구성 제공&hellip;</span><span class="sxs-lookup"><span data-stu-id="5260e-208">Provides configuration from&hellip;</span></span> |
| -------- | ----------------------------------- |
| <span data-ttu-id="5260e-209">[Azure Key Vault 구성 공급자](xref:security/key-vault-configuration)(‘보안’ 항목)</span><span class="sxs-lookup"><span data-stu-id="5260e-209">[Azure Key Vault Configuration Provider](xref:security/key-vault-configuration) (*Security* topics)</span></span> | <span data-ttu-id="5260e-210">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="5260e-210">Azure Key Vault</span></span> |
| [<span data-ttu-id="5260e-211">명령줄 구성 공급자</span><span class="sxs-lookup"><span data-stu-id="5260e-211">Command-line Configuration Provider</span></span>](#command-line-configuration-provider) | <span data-ttu-id="5260e-212">명령줄 매개 변수</span><span class="sxs-lookup"><span data-stu-id="5260e-212">Command-line parameters</span></span> |
| [<span data-ttu-id="5260e-213">사용자 지정 구성 공급자</span><span class="sxs-lookup"><span data-stu-id="5260e-213">Custom configuration provider</span></span>](#custom-configuration-provider) | <span data-ttu-id="5260e-214">사용자 지정 소스</span><span class="sxs-lookup"><span data-stu-id="5260e-214">Custom source</span></span> |
| [<span data-ttu-id="5260e-215">환경 변수 구성 공급자</span><span class="sxs-lookup"><span data-stu-id="5260e-215">Environment variables Configuration Provider</span></span>](#environment-variables-configuration-provider) | <span data-ttu-id="5260e-216">환경 변수</span><span class="sxs-lookup"><span data-stu-id="5260e-216">Environment variables</span></span> |
| [<span data-ttu-id="5260e-217">파일 구성 공급자</span><span class="sxs-lookup"><span data-stu-id="5260e-217">File Configuration Provider</span></span>](#file-configuration-provider) | <span data-ttu-id="5260e-218">파일(INI, JSON, XML)</span><span class="sxs-lookup"><span data-stu-id="5260e-218">Files (INI, JSON, XML)</span></span> |
| [<span data-ttu-id="5260e-219">메모리 구성 공급자</span><span class="sxs-lookup"><span data-stu-id="5260e-219">Memory Configuration Provider</span></span>](#memory-configuration-provider) | <span data-ttu-id="5260e-220">메모리 내 컬렉션</span><span class="sxs-lookup"><span data-stu-id="5260e-220">In-memory collections</span></span> |
| <span data-ttu-id="5260e-221">[사용자 비밀(비밀 관리자)](xref:security/app-secrets)(‘보안’ 항목)</span><span class="sxs-lookup"><span data-stu-id="5260e-221">[User secrets (Secret Manager)](xref:security/app-secrets) (*Security* topics)</span></span> | <span data-ttu-id="5260e-222">사용자 프로필 디렉터리의 파일</span><span class="sxs-lookup"><span data-stu-id="5260e-222">File in the user profile directory</span></span> |

::: moniker-end

::: moniker range="= aspnetcore-1.0"

| <span data-ttu-id="5260e-223">공급자</span><span class="sxs-lookup"><span data-stu-id="5260e-223">Provider</span></span> | <span data-ttu-id="5260e-224">다음에서 구성 제공&hellip;</span><span class="sxs-lookup"><span data-stu-id="5260e-224">Provides configuration from&hellip;</span></span> |
| -------- | ----------------------------------- |
| [<span data-ttu-id="5260e-225">명령줄 구성 공급자</span><span class="sxs-lookup"><span data-stu-id="5260e-225">Command-line Configuration Provider</span></span>](#command-line-configuration-provider) | <span data-ttu-id="5260e-226">명령줄 매개 변수</span><span class="sxs-lookup"><span data-stu-id="5260e-226">Command-line parameters</span></span> |
| [<span data-ttu-id="5260e-227">사용자 지정 구성 공급자</span><span class="sxs-lookup"><span data-stu-id="5260e-227">Custom configuration provider</span></span>](#custom-configuration-provider) | <span data-ttu-id="5260e-228">사용자 지정 소스</span><span class="sxs-lookup"><span data-stu-id="5260e-228">Custom source</span></span> |
| [<span data-ttu-id="5260e-229">환경 변수 구성 공급자</span><span class="sxs-lookup"><span data-stu-id="5260e-229">Environment variables Configuration Provider</span></span>](#environment-variables-configuration-provider) | <span data-ttu-id="5260e-230">환경 변수</span><span class="sxs-lookup"><span data-stu-id="5260e-230">Environment variables</span></span> |
| [<span data-ttu-id="5260e-231">파일 구성 공급자</span><span class="sxs-lookup"><span data-stu-id="5260e-231">File Configuration Provider</span></span>](#file-configuration-provider) | <span data-ttu-id="5260e-232">파일(INI, JSON, XML)</span><span class="sxs-lookup"><span data-stu-id="5260e-232">Files (INI, JSON, XML)</span></span> |
| [<span data-ttu-id="5260e-233">메모리 구성 공급자</span><span class="sxs-lookup"><span data-stu-id="5260e-233">Memory Configuration Provider</span></span>](#memory-configuration-provider) | <span data-ttu-id="5260e-234">메모리 내 컬렉션</span><span class="sxs-lookup"><span data-stu-id="5260e-234">In-memory collections</span></span> |
| <span data-ttu-id="5260e-235">[사용자 비밀(비밀 관리자)](xref:security/app-secrets)(‘보안’ 항목)</span><span class="sxs-lookup"><span data-stu-id="5260e-235">[User secrets (Secret Manager)](xref:security/app-secrets) (*Security* topics)</span></span> | <span data-ttu-id="5260e-236">사용자 프로필 디렉터리의 파일</span><span class="sxs-lookup"><span data-stu-id="5260e-236">File in the user profile directory</span></span> |

::: moniker-end

<span data-ttu-id="5260e-237">시작 시 구성 공급자에서 지정한 순서로 구성 소스를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-237">Configuration sources are read in the order that their configuration providers are specified at startup.</span></span> <span data-ttu-id="5260e-238">이 항목의 구성 공급자는 코드에서 정렬할 수 있는 순서가 아니라 사전순으로 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-238">The configuration providers described in this topic are described in alphabetical order, not in the order that your code may arrange them.</span></span> <span data-ttu-id="5260e-239">코드에서는 기본 구성 소스에 대한 우선 순위에 맞게 구성 공급자를 정렬하세요.</span><span class="sxs-lookup"><span data-stu-id="5260e-239">Order configuration providers in your code to suit your priorities for the underlying configuration sources.</span></span>

<span data-ttu-id="5260e-240">구성 공급자의 일반적인 순서는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-240">A typical sequence of configuration providers is:</span></span>

1. <span data-ttu-id="5260e-241">파일(*appsettings.json*, *appsettings.{Environment}.json*, 여기서 `{Environment}`는 앱의 현재 호스팅 환경)</span><span class="sxs-lookup"><span data-stu-id="5260e-241">Files (*appsettings.json*, *appsettings.{Environment}.json*, where `{Environment}` is the app's current hosting environment)</span></span>
1. [<span data-ttu-id="5260e-242">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="5260e-242">Azure Key Vault</span></span>](xref:security/key-vault-configuration)
1. <span data-ttu-id="5260e-243">[사용자 비밀(비밀 관리자)](xref:security/app-secrets)(개발 환경에만 해당)</span><span class="sxs-lookup"><span data-stu-id="5260e-243">[User secrets (Secret Manager)](xref:security/app-secrets) (in the Development environment only)</span></span>
1. <span data-ttu-id="5260e-244">환경 변수</span><span class="sxs-lookup"><span data-stu-id="5260e-244">Environment variables</span></span>
1. <span data-ttu-id="5260e-245">명령줄 인수</span><span class="sxs-lookup"><span data-stu-id="5260e-245">Command-line arguments</span></span>

<span data-ttu-id="5260e-246">일반적으로 명령줄 구성 공급자를 일련의 공급자에서 마지막에 배치하며, 따라서 다른 공급자에서 설정한 구성을 명령줄 인수로 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-246">It's a common practice to position the Command-line Configuration Provider last in a series of providers to allow command-line arguments to override configuration set by the other providers.</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="5260e-247">이 공급자 순서는 <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*>를 사용하여 새 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>를 초기화할 때 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-247">This sequence of providers is put into place when you initialize a new <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> with <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*>.</span></span> <span data-ttu-id="5260e-248">자세한 내용은 [웹 호스트: 호스트 설정](xref:fundamentals/host/web-host#set-up-a-host)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5260e-248">For more information, see [Web Host: Set up a host](xref:fundamentals/host/web-host#set-up-a-host).</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="5260e-249"><xref:Microsoft.Extensions.Configuration.ConfigurationBuilder>를 사용하고 `Startup`의 <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder.Build*> 메서드를 호출하여 호스트가 아니라 앱에 대해 이 공급자 순서를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-249">This sequence of providers can be created for the app (not the host) with a <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder> and a call to its <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder.Build*> method in `Startup`:</span></span>

```csharp
public Startup(IHostingEnvironment env)
{
    var builder = new ConfigurationBuilder()
        .SetBasePath(Directory.GetCurrentDirectory())
        .AddJsonFile("appsettings.json", optional: true, reloadOnChange: true)
        .AddJsonFile($"appsettings.{env.EnvironmentName}.json", optional: true, 
            reloadOnChange: true);

    var appAssembly = Assembly.Load(new AssemblyName(env.ApplicationName));

    if (appAssembly != null)
    {
        builder.AddUserSecrets(appAssembly, optional: true);
    }

    builder.AddEnvironmentVariables();

    Configuration = builder.Build();
}

public IConfiguration Configuration { get; }

public void ConfigureServices(IServiceCollection services)
{
    services.AddSingleton<IConfiguration>(Configuration);
}
```

<span data-ttu-id="5260e-250">앞의 예제에서 환경 이름(`env.EnvironmentName`) 및 앱 어셈블리 이름(`env.ApplicationName`)은 <xref:Microsoft.Extensions.Hosting.IHostingEnvironment>에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-250">In the preceding example, the environment name (`env.EnvironmentName`) and app assembly name (`env.ApplicationName`) are provided by the <xref:Microsoft.Extensions.Hosting.IHostingEnvironment>.</span></span> <span data-ttu-id="5260e-251">자세한 내용은 <xref:fundamentals/environments>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5260e-251">For more information, see <xref:fundamentals/environments>.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

## <a name="configureappconfiguration"></a><span data-ttu-id="5260e-252">ConfigureAppConfiguration</span><span class="sxs-lookup"><span data-stu-id="5260e-252">ConfigureAppConfiguration</span></span>

<span data-ttu-id="5260e-253">웹 호스트를 빌드할 때 <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*>을 호출하여 앱의 구성 공급자와 <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*>에 의해 자동으로 추가된 구성 공급자를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-253">Call <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*> when building the Web Host to specify the app's configuration providers in addition to those added automatically by <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*>:</span></span>

[!code-csharp[](index/samples/2.x/ConfigurationSample/Program.cs?name=snippet_Program&highlight=19)]

::: moniker-end

## <a name="command-line-configuration-provider"></a><span data-ttu-id="5260e-254">명령줄 구성 공급자</span><span class="sxs-lookup"><span data-stu-id="5260e-254">Command-line Configuration Provider</span></span>

<span data-ttu-id="5260e-255"><xref:Microsoft.Extensions.Configuration.CommandLine.CommandLineConfigurationProvider>은 런타임 시 명령줄 인수 키-값 쌍에서 구성을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-255">The <xref:Microsoft.Extensions.Configuration.CommandLine.CommandLineConfigurationProvider> loads configuration from command-line argument key-value pairs at runtime.</span></span>

<span data-ttu-id="5260e-256">명령줄 구성을 활성화하기 위해 <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder> 인스턴스에서 <xref:Microsoft.Extensions.Configuration.CommandLineConfigurationExtensions.AddCommandLine*> 확장 메서드가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-256">To activate command-line configuration, the <xref:Microsoft.Extensions.Configuration.CommandLineConfigurationExtensions.AddCommandLine*> extension method is called on an instance of <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder>.</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="5260e-257">`AddCommandLine`는 <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*>를 사용하여 새 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>를 초기화할 때 자동으로 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-257">`AddCommandLine` is automatically called when you initialize a new <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> with <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*>.</span></span> <span data-ttu-id="5260e-258">자세한 내용은 [웹 호스트: 호스트 설정](xref:fundamentals/host/web-host#set-up-a-host)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5260e-258">For more information, see [Web Host: Set up a host](xref:fundamentals/host/web-host#set-up-a-host).</span></span>

<span data-ttu-id="5260e-259">`CreateDefaultBuilder`는 다음 항목도 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-259">`CreateDefaultBuilder` also loads:</span></span>

* <span data-ttu-id="5260e-260">*appsettings.json* 및 *appsettings.{Environment}.json*에서 선택적 구성</span><span class="sxs-lookup"><span data-stu-id="5260e-260">Optional configuration from *appsettings.json* and *appsettings.{Environment}.json*.</span></span>
* <span data-ttu-id="5260e-261">[사용자 비밀(비밀 관리자)](xref:security/app-secrets)(개발 환경에서)</span><span class="sxs-lookup"><span data-stu-id="5260e-261">[User secrets (Secret Manager)](xref:security/app-secrets) (in the Development environment).</span></span>
* <span data-ttu-id="5260e-262">환경 변수.</span><span class="sxs-lookup"><span data-stu-id="5260e-262">Environment variables.</span></span>

<span data-ttu-id="5260e-263">`CreateDefaultBuilder`는 명령줄 구성 공급자를 마지막에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-263">`CreateDefaultBuilder` adds the Command-line Configuration Provider last.</span></span> <span data-ttu-id="5260e-264">따라서 런타임에 전달된 명령줄 인수가 다른 공급자에서 설정한 구성을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-264">Command-line arguments passed at runtime override configuration set by the other providers.</span></span>

<span data-ttu-id="5260e-265">`CreateDefaultBuilder`는 호스트를 생성할 때 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-265">`CreateDefaultBuilder` acts when the host is constructed.</span></span> <span data-ttu-id="5260e-266">따라서 `CreateDefaultBuilder`에서 활성화한 명령줄 구성이 호스트 생성 방식에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-266">Therefore, command-line configuration activated by `CreateDefaultBuilder` can affect how the host is configured.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="5260e-267">호스트를 빌드할 때 <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*>을 호출하여 앱의 구성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-267">Call <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*> when building the host to specify the app's configuration.</span></span>

<span data-ttu-id="5260e-268">`CreateDefaultBuilder`가 이미 `AddCommandLine`을 호출했습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-268">`AddCommandLine` has already been called by `CreateDefaultBuilder`.</span></span> <span data-ttu-id="5260e-269">앱 구성을 제공해야 하며, 명령줄 인수로 해당 구성을 재정의할 수 있는 경우 <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*>에 제공된 앱의 추가 제공 업체에 문의하고 마지막에 `AddCommandLine`을 호출하세요.</span><span class="sxs-lookup"><span data-stu-id="5260e-269">If you need to provide app configuration and still be able to override that configuration with command-line arguments, call the app's additional providers in <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*> and call `AddCommandLine` last.</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateWebHostBuilder(args).Build().Run();
    }

    public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
        WebHost.CreateDefaultBuilder(args)
            .ConfigureAppConfiguration((hostingContext, config) =>
            {
                // Call other providers here and call AddCommandLine last.
                config.AddCommandLine(args);
            })
            .UseStartup<Startup>();
}
```

<span data-ttu-id="5260e-270"><xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>을 직접 만들 경우 다음 구성으로 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*>을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-270">When creating a <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> directly, call <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> with the configuration:</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="5260e-271"><xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> 메서드를 사용하여 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>에 구성을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-271">Apply the configuration to <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> with the <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> method.</span></span>

<span data-ttu-id="5260e-272">`UseConfiguration`을 호출할 때 `CreateDefaultBuilder`가 이미 `AddCommandLine`을 호출했습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-272">`AddCommandLine` has already been called by `CreateDefaultBuilder` when `UseConfiguration` is called.</span></span> <span data-ttu-id="5260e-273">앱 구성을 제공해야 하며, 명령줄 인수로 해당 구성을 재정의할 수 있는 경우 `ConfigurationBuilder`에 제공된 앱의 추가 제공 업체에 문의하고 마지막에 `AddCommandLine`을 호출하세요.</span><span class="sxs-lookup"><span data-stu-id="5260e-273">If you need to provide app configuration and still be able to override that configuration with command-line arguments, call the app's additional providers on a `ConfigurationBuilder` and call `AddCommandLine` last.</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateWebHostBuilder(args).Build().Run();
    }

    public static IWebHostBuilder CreateWebHostBuilder(string[] args)
    {
        var config = new ConfigurationBuilder()
            // Call other providers here and call AddCommandLine last.
            .AddCommandLine(args)
            .Build();

        return WebHost.CreateDefaultBuilder(args)
            .UseConfiguration(config)
            .UseStartup<Startup>();
    }
}
```

<span data-ttu-id="5260e-274"><xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>을 직접 만들 경우 다음 구성으로 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*>을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-274">When creating a <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> directly, call <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> with the configuration:</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="5260e-275">명령줄 구성을 활성화하려면 <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder> 인스턴스에서 <xref:Microsoft.Extensions.Configuration.CommandLineConfigurationExtensions.AddCommandLine*> 확장 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-275">To activate command-line configuration, call the <xref:Microsoft.Extensions.Configuration.CommandLineConfigurationExtensions.AddCommandLine*> extension method on an instance of <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder>.</span></span>

<span data-ttu-id="5260e-276">이 공급자를 마지막에 호출하므로 다른 구성 공급자가 설정한 구성을 런타임에 전달되는 명령줄 인수가 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-276">Call the provider last to allow the command-line arguments passed at runtime to override configuration set by other configuration providers.</span></span>

<span data-ttu-id="5260e-277"><xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> 메서드를 사용하여 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>에 구성을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-277">Apply the configuration to <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> with the <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> method:</span></span>

::: moniker-end

```csharp
var config = new ConfigurationBuilder()
    // Call additional providers here as needed.
    // Call AddCommandLine last to allow arguments to override other configuration.
    .AddCommandLine(args)
    .Build();

var host = new WebHostBuilder()
    .UseConfiguration(config)
    .UseKestrel()
    .UseStartup<Startup>();
```

<span data-ttu-id="5260e-278">**예제**</span><span class="sxs-lookup"><span data-stu-id="5260e-278">**Example**</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="5260e-279">2.x 샘플 앱은 정적 편의 메서드 `CreateDefaultBuilder`를 활용하여 호스트를 빌드하며, <xref:Microsoft.Extensions.Configuration.CommandLineConfigurationExtensions.AddCommandLine*> 호출도 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-279">The 2.x sample app takes advantage of the static convenience method `CreateDefaultBuilder` to build the host, which includes a call to <xref:Microsoft.Extensions.Configuration.CommandLineConfigurationExtensions.AddCommandLine*>.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="5260e-280">1.x 샘플 앱은 <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder>에서 <xref:Microsoft.Extensions.Configuration.CommandLineConfigurationExtensions.AddCommandLine*>을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-280">The 1.x sample app calls <xref:Microsoft.Extensions.Configuration.CommandLineConfigurationExtensions.AddCommandLine*> on a <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder>.</span></span>

::: moniker-end

1. <span data-ttu-id="5260e-281">프로젝트의 디렉터리에서 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-281">Open a command prompt in the project's directory.</span></span>
1. <span data-ttu-id="5260e-282">`dotnet run` 명령에 명령줄 인수를 제공합니다(`dotnet run CommandLineKey=CommandLineValue`).</span><span class="sxs-lookup"><span data-stu-id="5260e-282">Supply a command-line argument to the `dotnet run` command, `dotnet run CommandLineKey=CommandLineValue`.</span></span>
1. <span data-ttu-id="5260e-283">앱이 실행되면 브라우저를 열어 `http://localhost:5000`의 앱으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-283">After the app is running, open a browser to the app at `http://localhost:5000`.</span></span>
1. <span data-ttu-id="5260e-284">`dotnet run`에 제공한 구성 명령줄 인수에 대한 키-값 쌍이 출력에 포함되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-284">Observe that the output contains the key-value pair for the configuration command-line argument provided to `dotnet run`.</span></span>

### <a name="arguments"></a><span data-ttu-id="5260e-285">인수</span><span class="sxs-lookup"><span data-stu-id="5260e-285">Arguments</span></span>

<span data-ttu-id="5260e-286">값은 등호(`=`) 다음에 와야 합니다. 또는 값이 공백 다음에 오는 경우 키에 접두사(`--` 또는 `/`)가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-286">The value must follow an equals sign (`=`), or the key must have a prefix (`--` or `/`) when the value follows a space.</span></span> <span data-ttu-id="5260e-287">등호를 사용하는 경우 값이 null일 수 있습니다(예: `CommandLineKey=`).</span><span class="sxs-lookup"><span data-stu-id="5260e-287">The value can be null if an equals sign is used (for example, `CommandLineKey=`).</span></span>

| <span data-ttu-id="5260e-288">키 접두사</span><span class="sxs-lookup"><span data-stu-id="5260e-288">Key prefix</span></span>               | <span data-ttu-id="5260e-289">예</span><span class="sxs-lookup"><span data-stu-id="5260e-289">Example</span></span>                                                |
| ------------------------ | ------------------------------------------------------ |
| <span data-ttu-id="5260e-290">접두사 없음</span><span class="sxs-lookup"><span data-stu-id="5260e-290">No prefix</span></span>                | `CommandLineKey1=value1`                               |
| <span data-ttu-id="5260e-291">대시 2개(`--`)</span><span class="sxs-lookup"><span data-stu-id="5260e-291">Two dashes (`--`)</span></span>        | <span data-ttu-id="5260e-292">`--CommandLineKey2=value2`, `--CommandLineKey2 value2`</span><span class="sxs-lookup"><span data-stu-id="5260e-292">`--CommandLineKey2=value2`, `--CommandLineKey2 value2`</span></span> |
| <span data-ttu-id="5260e-293">슬래시(`/`)</span><span class="sxs-lookup"><span data-stu-id="5260e-293">Forward slash (`/`)</span></span>      | <span data-ttu-id="5260e-294">`/CommandLineKey3=value3`, `/CommandLineKey3 value3`</span><span class="sxs-lookup"><span data-stu-id="5260e-294">`/CommandLineKey3=value3`, `/CommandLineKey3 value3`</span></span>   |

<span data-ttu-id="5260e-295">같은 명령 내에서 등호를 사용하는 명령줄 인수 키-값 쌍을 공백을 사용하는 키-값 쌍과 함께 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="5260e-295">Within the same command, don't mix command-line argument key-value pairs that use an equals sign with key-value pairs that use a space.</span></span>

<span data-ttu-id="5260e-296">명령 예:</span><span class="sxs-lookup"><span data-stu-id="5260e-296">Example commands:</span></span>

```console
dotnet run CommandLineKey1=value --CommandLineKey2=value /CommandLineKey2=value
dotnet run --CommandLineKey1 value /CommandLineKey2 value
dotnet run CommandLineKey1= CommandLineKey2=value
```

### <a name="switch-mappings"></a><span data-ttu-id="5260e-297">스위치 매핑</span><span class="sxs-lookup"><span data-stu-id="5260e-297">Switch mappings</span></span>

<span data-ttu-id="5260e-298">스위치 매핑은 키 이름 교체 논리를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-298">Switch mappings allow key name replacement logic.</span></span> <span data-ttu-id="5260e-299"><xref:Microsoft.Extensions.Configuration.ConfigurationBuilder>를 사용하여 구성을 수동으로 빌드하는 경우에는 <xref:Microsoft.Extensions.Configuration.CommandLineConfigurationExtensions.AddCommandLine*> 메서드에 대체 스위치를 포함하는 사전을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-299">When you manually build configuration with a <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder>, you can provide a dictionary of switch replacements to the <xref:Microsoft.Extensions.Configuration.CommandLineConfigurationExtensions.AddCommandLine*> method.</span></span>

<span data-ttu-id="5260e-300">스위치 매핑 사전을 사용하면 명령줄 인수를 통해 제공된 키와 일치하는 키에 대해 사전을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-300">When the switch mappings dictionary is used, the dictionary is checked for a key that matches the key provided by a command-line argument.</span></span> <span data-ttu-id="5260e-301">사전에서 명령줄 키가 발견되면 사전 값(대체 키)이 다시 전달되어 앱 구성의 키-값 쌍이 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-301">If the command-line key is found in the dictionary, the dictionary value (the key replacement) is passed back to set the key-value pair into the app's configuration.</span></span> <span data-ttu-id="5260e-302">단일 대시(`-`) 접두사가 붙은 명령줄 키에는 스위치 매핑이 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-302">A switch mapping is required for any command-line key prefixed with a single dash (`-`).</span></span>

<span data-ttu-id="5260e-303">스위치 매핑 사전 키 규칙:</span><span class="sxs-lookup"><span data-stu-id="5260e-303">Switch mappings dictionary key rules:</span></span>

* <span data-ttu-id="5260e-304">스위치는 단일 대시(`-`) 또는 이중 대시(`--`)로 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-304">Switches must start with a dash (`-`) or double-dash (`--`).</span></span>
* <span data-ttu-id="5260e-305">스위치 매핑 사전이 중복 키를 포함하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-305">The switch mappings dictionary must not contain duplicate keys.</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="5260e-306">호스트를 빌드할 때 <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*>을 호출하여 앱의 구성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-306">Call <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*> when building the host to specify the app's configuration:</span></span>

```csharp
public class Program
{
    public static readonly Dictionary<string, string> _switchMappings = 
        new Dictionary<string, string>
        {
            { "-CLKey1", "CommandLineKey1" },
            { "-CLKey2", "CommandLineKey2" }
        };

    public static void Main(string[] args)
    {
        CreateWebHostBuilder(args).Build().Run();
    }

    // Do not pass the args to CreateDefaultBuilder
    public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
        WebHost.CreateDefaultBuilder()
            .ConfigureAppConfiguration((hostingContext, config) =>
            {
                config.AddCommandLine(args, _switchMappings);
            })
            .UseStartup<Startup>();
}
```

<span data-ttu-id="5260e-307">앞의 예제와 같이 스위치 매핑이 사용되는 경우 `CreateDefaultBuilder` 호출에서 인수를 전달하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-307">As shown in the preceding example, the call to `CreateDefaultBuilder` shouldn't pass arguments when switch mappings are used.</span></span> <span data-ttu-id="5260e-308">`CreateDefaultBuilder` 메서드의 `AddCommandLine` 호출에는 매핑된 스위치가 포함되지 않으며 `CreateDefaultBuilder`에 스위치 매핑 사전을 전달할 방법은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-308">`CreateDefaultBuilder` method's `AddCommandLine` call doesn't include mapped switches, and there's no way to pass the switch mapping dictionary to `CreateDefaultBuilder`.</span></span> <span data-ttu-id="5260e-309">인수가 매핑된 스위치를 포함하고 `CreateDefaultBuilder`에 전달되는 경우 해당 `AddCommandLine` 공급자는 <xref:System.FormatException>으로 초기화하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-309">If the arguments include a mapped switch and are passed to `CreateDefaultBuilder`, its `AddCommandLine` provider fails to initialize with a <xref:System.FormatException>.</span></span> <span data-ttu-id="5260e-310">해결 방법으로 `CreateDefaultBuilder`에 인수를 전달하지 않고 대신 `ConfigurationBuilder` 메서드의 `AddCommandLine` 메서드에서 인수와 스위치 매핑 사전을 모두 처리하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-310">The solution isn't to pass the arguments to `CreateDefaultBuilder` but instead to allow the `ConfigurationBuilder` method's `AddCommandLine` method to process both the arguments and the switch mapping dictionary.</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateWebHostBuilder(args).Build().Run();
    }

    public static IWebHostBuilder CreateWebHostBuilder(string[] args)
    {
        var switchMappings = new Dictionary<string, string>
            {
                { "-CLKey1", "CommandLineKey1" },
                { "-CLKey2", "CommandLineKey2" }
            };

        var config = new ConfigurationBuilder()
            .AddCommandLine(args, switchMappings)
            .Build();

        // Do not pass the args to CreateDefaultBuilder
        return WebHost.CreateDefaultBuilder()
            .UseConfiguration(config)
            .UseStartup<Startup>();
    }
}
```

<span data-ttu-id="5260e-311">앞의 예제와 같이 스위치 매핑이 사용되는 경우 `CreateDefaultBuilder` 호출에서 인수를 전달하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-311">As shown in the preceding example, the call to `CreateDefaultBuilder` shouldn't pass arguments when switch mappings are used.</span></span> <span data-ttu-id="5260e-312">`CreateDefaultBuilder` 메서드의 `AddCommandLine` 호출에는 매핑된 스위치가 포함되지 않으며 `CreateDefaultBuilder`에 스위치 매핑 사전을 전달할 방법은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-312">`CreateDefaultBuilder` method's `AddCommandLine` call doesn't include mapped switches, and there's no way to pass the switch mapping dictionary to `CreateDefaultBuilder`.</span></span> <span data-ttu-id="5260e-313">인수가 매핑된 스위치를 포함하고 `CreateDefaultBuilder`에 전달되는 경우 해당 `AddCommandLine` 공급자는 <xref:System.FormatException>으로 초기화하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-313">If the arguments include a mapped switch and are passed to `CreateDefaultBuilder`, its `AddCommandLine` provider fails to initialize with a <xref:System.FormatException>.</span></span> <span data-ttu-id="5260e-314">해결 방법으로 `CreateDefaultBuilder`에 인수를 전달하지 않고 대신 `ConfigurationBuilder` 메서드의 `AddCommandLine` 메서드에서 인수와 스위치 매핑 사전을 모두 처리하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-314">The solution isn't to pass the arguments to `CreateDefaultBuilder` but instead to allow the `ConfigurationBuilder` method's `AddCommandLine` method to process both the arguments and the switch mapping dictionary.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

```csharp
public static void Main(string[] args)
{
    var switchMappings = new Dictionary<string, string>
        {
            { "-CLKey1", "CommandLineKey1" },
            { "-CLKey2", "CommandLineKey2" }
        };

    var config = new ConfigurationBuilder()
        .AddCommandLine(args, switchMappings)
        .Build();

    var host = new WebHostBuilder()
        .UseConfiguration(config)
        .UseKestrel()
        .UseStartup<Startup>()
        .Start();

    using (host)
    {
        Console.ReadLine();
    }
}
```

::: moniker-end

<span data-ttu-id="5260e-315">생성된 스위치 매핑 사전은 다음 표의 데이터를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-315">After the switch mappings dictionary is created, it contains the data shown in the following table.</span></span>

| <span data-ttu-id="5260e-316">Key</span><span class="sxs-lookup"><span data-stu-id="5260e-316">Key</span></span>       | <span data-ttu-id="5260e-317">값</span><span class="sxs-lookup"><span data-stu-id="5260e-317">Value</span></span>             |
| --------- | ----------------- |
| `-CLKey1` | `CommandLineKey1` |
| `-CLKey2` | `CommandLineKey2` |

<span data-ttu-id="5260e-318">앱을 시작할 때 스위치 매핑된 키가 사용되는 경우 구성은 사전에서 제공하는 키의 구성 값을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-318">If the switch-mapped keys are used when starting the app, configuration receives the configuration value on the key supplied by the dictionary:</span></span>

```console
dotnet run -CLKey1=value1 -CLKey2=value2
```

<span data-ttu-id="5260e-319">앞의 명령을 실행한 후 구성에는 다음 표에 표시된 값이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-319">After running the preceding command, configuration contains the values shown in the following table.</span></span>

| <span data-ttu-id="5260e-320">Key</span><span class="sxs-lookup"><span data-stu-id="5260e-320">Key</span></span>               | <span data-ttu-id="5260e-321">값</span><span class="sxs-lookup"><span data-stu-id="5260e-321">Value</span></span>    |
| ----------------- | -------- |
| `CommandLineKey1` | `value1` |
| `CommandLineKey2` | `value2` |

## <a name="environment-variables-configuration-provider"></a><span data-ttu-id="5260e-322">환경 변수 구성 공급자</span><span class="sxs-lookup"><span data-stu-id="5260e-322">Environment Variables Configuration Provider</span></span>

<span data-ttu-id="5260e-323"><xref:Microsoft.Extensions.Configuration.EnvironmentVariables.EnvironmentVariablesConfigurationProvider>는 런타임에 환경 변수 키-값 쌍에서 구성을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-323">The <xref:Microsoft.Extensions.Configuration.EnvironmentVariables.EnvironmentVariablesConfigurationProvider> loads configuration from environment variable key-value pairs at runtime.</span></span>

<span data-ttu-id="5260e-324">환경 변수 구성을 활성화하려면 <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder> 인스턴스에서 <xref:Microsoft.Extensions.Configuration.EnvironmentVariablesExtensions.AddEnvironmentVariables*> 확장 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-324">To activate environment variables configuration, call the <xref:Microsoft.Extensions.Configuration.EnvironmentVariablesExtensions.AddEnvironmentVariables*> extension method on an instance of <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder>.</span></span>

<span data-ttu-id="5260e-325">환경 변수에서 계층적 키를 사용할 경우 일부 플랫폼에서 콜론 구분 기호(`:`)가 작동하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-325">When working with hierarchical keys in environment variables, a colon separator (`:`) may not work on all platforms.</span></span> <span data-ttu-id="5260e-326">두 개의 밑줄(`__`)은 모든 플랫폼에서 지원되며 콜론으로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-326">A double underscore (`__`) is supported by all platforms and is replaced by a colon.</span></span>

<span data-ttu-id="5260e-327">[Azure App Service](https://azure.microsoft.com/services/app-service/)를 사용하면 Azure Portal에서 환경 변수를 설정할 수 있으므로 환경 변수 구성 공급자를 사용한 앱 구성을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-327">[Azure App Service](https://azure.microsoft.com/services/app-service/) permits you to set environment variables in the Azure Portal that can override app configuration using the Environment Variables Configuration Provider.</span></span> <span data-ttu-id="5260e-328">자세한 내용은 [Azure 앱: Azure Portal을 사용하여 앱 구성 재정의](xref:host-and-deploy/azure-apps/index#override-app-configuration-using-the-azure-portal)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5260e-328">For more information, see [Azure Apps: Override app configuration using the Azure Portal](xref:host-and-deploy/azure-apps/index#override-app-configuration-using-the-azure-portal).</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="5260e-329">`AddEnvironmentVariables`는 <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*>를 사용하여 새 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>를 초기화할 때 자동으로 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-329">`AddEnvironmentVariables` is automatically called when you initialize a new <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> with <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*>.</span></span> <span data-ttu-id="5260e-330">자세한 내용은 [웹 호스트: 호스트 설정](xref:fundamentals/host/web-host#set-up-a-host)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5260e-330">For more information, see [Web Host: Set up a host](xref:fundamentals/host/web-host#set-up-a-host).</span></span>

<span data-ttu-id="5260e-331">`CreateDefaultBuilder`는 다음 항목도 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-331">`CreateDefaultBuilder` also loads:</span></span>

* <span data-ttu-id="5260e-332">*appsettings.json* 및 *appsettings.{Environment}.json*에서 선택적 구성</span><span class="sxs-lookup"><span data-stu-id="5260e-332">Optional configuration from *appsettings.json* and *appsettings.{Environment}.json*.</span></span>
* <span data-ttu-id="5260e-333">[사용자 비밀(비밀 관리자)](xref:security/app-secrets)(개발 환경에서)</span><span class="sxs-lookup"><span data-stu-id="5260e-333">[User secrets (Secret Manager)](xref:security/app-secrets) (in the Development environment).</span></span>
* <span data-ttu-id="5260e-334">명령줄 인수.</span><span class="sxs-lookup"><span data-stu-id="5260e-334">Command-line arguments.</span></span>

<span data-ttu-id="5260e-335">사용자 비밀 및 *appsettings* 파일을 통해 구성을 설정한 후 환경 변수 구성 공급자를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-335">The Environment Variable Configuration Provider is called after configuration is established from user secrets and *appsettings* files.</span></span> <span data-ttu-id="5260e-336">이 위치에서 공급자를 호출하면 런타임에 환경 변수를 읽어 들여 사용자 비밀 및 *appsettings* 파일로 설정한 구성을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-336">Calling the provider in this position allows the environment variables read at runtime to override configuration set by user secrets and *appsettings* files.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="5260e-337">호스트를 빌드할 때 <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*>을 호출하여 앱의 구성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-337">Call <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*> when building the host to specify the app's configuration.</span></span>

<span data-ttu-id="5260e-338">`ASPNETCORE_` 접두사가 있는 환경 변수의 `AddEnvironmentVariables`가 `CreateDefaultBuilder`에 의해 이미 호출되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-338">`AddEnvironmentVariables` for environment variables prefixed with `ASPNETCORE_` has already been called by `CreateDefaultBuilder`.</span></span> <span data-ttu-id="5260e-339">추가 환경 변수에서 앱 구성을 제공해야 하는 경우에는 <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*>에서 앱의 추가 공급자를 호출하고 접두사가 있는 `AddEnvironmentVariables`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-339">If you need to provide app configuration from additional environment variables, call the app's additional providers in <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*> and call `AddEnvironmentVariables` with the prefix.</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateWebHostBuilder(args).Build().Run();
    }

    public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
        WebHost.CreateDefaultBuilder(args)
            .ConfigureAppConfiguration((hostingContext, config) =>
            {
                // Call additional providers here as needed.
                // Call AddEnvironmentVariables last if you need to allow environment
                // variables to override values from other providers.
                config.AddEnvironmentVariables(prefix: "PREFIX_");
            })
            .UseStartup<Startup>();
}
```

<span data-ttu-id="5260e-340"><xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>을 직접 만들 경우 다음 구성으로 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*>을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-340">When creating a <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> directly, call <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> with the configuration:</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="5260e-341"><xref:Microsoft.Extensions.Configuration.ConfigurationBuilder> 인스턴스에서 `AddEnvironmentVariables` 확장 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-341">Call the `AddEnvironmentVariables` extension method on an instance of <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder>.</span></span> <span data-ttu-id="5260e-342"><xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> 메서드를 사용하여 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>에 구성을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-342">Apply the configuration to <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> with the <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> method.</span></span>

<span data-ttu-id="5260e-343">`ASPNETCORE_` 접두사가 있는 환경 변수의 `AddEnvironmentVariables`가 `CreateDefaultBuilder`에 의해 이미 호출되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-343">`AddEnvironmentVariables` for environment variables prefixed with `ASPNETCORE_` has already been called by `CreateDefaultBuilder`.</span></span> <span data-ttu-id="5260e-344">추가 환경 변수에서 앱 구성을 제공해야 하는 경우에는 <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*>에서 앱의 추가 공급자를 호출하고 접두사가 있는 `AddEnvironmentVariables`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-344">If you need to provide app configuration from additional environment variables, call the app's additional providers in <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*> and call `AddEnvironmentVariables` with the prefix.</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateWebHostBuilder(args).Build().Run();
    }

    public static IWebHostBuilder CreateWebHostBuilder(string[] args)
    {
        var config = new ConfigurationBuilder()
            // Call additional providers here as needed.
            // Call AddEnvironmentVariables last if you need to allow environment
            // variables to override values from other providers.
            .AddEnvironmentVariables(prefix: "PREFIX_")
            .Build();

        return WebHost.CreateDefaultBuilder(args)
            .UseConfiguration(config)
            .UseStartup<Startup>();
    }
}
```

<span data-ttu-id="5260e-345"><xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>을 직접 만들 경우 다음 구성으로 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*>을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-345">When creating a <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> directly, call <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> with the configuration:</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="5260e-346"><xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> 메서드를 사용하여 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>에 구성을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-346">Apply the configuration to <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> with the <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> method:</span></span>

::: moniker-end

```csharp
var config = new ConfigurationBuilder()
    .AddEnvironmentVariables()
    .Build();

var host = new WebHostBuilder()
    .UseConfiguration(config)
    .UseKestrel()
    .UseStartup<Startup>();
```

<span data-ttu-id="5260e-347">**예제**</span><span class="sxs-lookup"><span data-stu-id="5260e-347">**Example**</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="5260e-348">2.x 샘플 앱은 정적 편의 메서드 `CreateDefaultBuilder`를 활용하여 호스트를 빌드하며, `AddEnvironmentVariables` 호출도 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-348">The 2.x sample app takes advantage of the static convenience method `CreateDefaultBuilder` to build the host, which includes a call to `AddEnvironmentVariables`.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="5260e-349">1.x 샘플 앱은 `ConfigurationBuilder`에서 `AddEnvironmentVariables`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-349">The 1.x sample app calls `AddEnvironmentVariables` on a `ConfigurationBuilder`.</span></span>

::: moniker-end

1. <span data-ttu-id="5260e-350">샘플 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-350">Run the sample app.</span></span> <span data-ttu-id="5260e-351">브라우저를 열어 `http://localhost:5000`의 앱으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-351">Open a browser to the app at `http://localhost:5000`.</span></span>
1. <span data-ttu-id="5260e-352">환경 변수 `ENVIRONMENT`에 대한 키-값 쌍이 출력에 포함되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-352">Observe that the output contains the key-value pair for the environment variable `ENVIRONMENT`.</span></span> <span data-ttu-id="5260e-353">이 값은 앱이 실행 중인 환경을 나타내며, 로컬에서 실행 중이면 일반적으로 `Development` 입니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-353">The value reflects the environment in which the app is running, typically `Development` when running locally.</span></span>

<span data-ttu-id="5260e-354">앱에서 렌더링하는 환경 변수 목록을 짧게 유지하기 위해 앱에서는 다음으로 시작하는 변수로 환경 변수를 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-354">To keep the list of environment variables rendered by the app short, the app filters environment variables to those that start with the following:</span></span>

* <span data-ttu-id="5260e-355">ASPNETCORE_</span><span class="sxs-lookup"><span data-stu-id="5260e-355">ASPNETCORE_</span></span>
* <span data-ttu-id="5260e-356">urls</span><span class="sxs-lookup"><span data-stu-id="5260e-356">urls</span></span>
* <span data-ttu-id="5260e-357">로깅</span><span class="sxs-lookup"><span data-stu-id="5260e-357">Logging</span></span>
* <span data-ttu-id="5260e-358">ENVIRONMENT</span><span class="sxs-lookup"><span data-stu-id="5260e-358">ENVIRONMENT</span></span>
* <span data-ttu-id="5260e-359">contentRoot</span><span class="sxs-lookup"><span data-stu-id="5260e-359">contentRoot</span></span>
* <span data-ttu-id="5260e-360">AllowedHosts</span><span class="sxs-lookup"><span data-stu-id="5260e-360">AllowedHosts</span></span>
* <span data-ttu-id="5260e-361">applicationName</span><span class="sxs-lookup"><span data-stu-id="5260e-361">applicationName</span></span>
* <span data-ttu-id="5260e-362">CommandLine</span><span class="sxs-lookup"><span data-stu-id="5260e-362">CommandLine</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="5260e-363">앱에서 사용할 수 있는 모든 환경 변수를 표시하려면 *Pages/Index.cshtml.cs*에서 `FilteredConfiguration`을 다음으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-363">If you wish to expose all of the environment variables available to the app, change the `FilteredConfiguration` in *Pages/Index.cshtml.cs* to the following:</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="5260e-364">앱에서 사용할 수 있는 모든 환경 변수를 표시하려면 *Controllers/HomeController.cs*에서 `FilteredConfiguration`을 다음으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-364">If you wish to expose all of the environment variables available to the app, change the `FilteredConfiguration` in *Controllers/HomeController.cs* to the following:</span></span>

::: moniker-end

```csharp
FilteredConfiguration = _config.AsEnumerable();
```

### <a name="prefixes"></a><span data-ttu-id="5260e-365">접두사</span><span class="sxs-lookup"><span data-stu-id="5260e-365">Prefixes</span></span>

<span data-ttu-id="5260e-366">`AddEnvironmentVariables` 메서드에 접두사를 제공하면 앱의 구성에 로드된 환경 변수가 필터링됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-366">Environment variables loaded into the app's configuration are filtered when you supply a prefix to the `AddEnvironmentVariables` method.</span></span> <span data-ttu-id="5260e-367">예를 들어 환경 변수를 `CUSTOM_` 접두사로 필터링하려면 구성 공급자에 이 접두사를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-367">For example, to filter environment variables on the prefix `CUSTOM_`, supply the prefix to the configuration provider:</span></span>

```csharp
var config = new ConfigurationBuilder()
    .AddEnvironmentVariables("CUSTOM_")
    .Build();
```

<span data-ttu-id="5260e-368">구성 키-값 쌍이 생성되면 접두사는 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-368">The prefix is stripped off when the configuration key-value pairs are created.</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="5260e-369">정적 편의 메서드 `CreateDefaultBuilder`는 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>를 생성하여 앱의 호스트를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-369">The static convenience method `CreateDefaultBuilder` creates a <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> to establish the app's host.</span></span> <span data-ttu-id="5260e-370">생성된 `WebHostBuilder`는 앞에 `ASPNETCORE_`가 붙은 환경 변수에서 호스트 구성을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-370">When `WebHostBuilder` is created, it finds its host configuration in environment variables prefixed with `ASPNETCORE_`.</span></span>

::: moniker-end

<span data-ttu-id="5260e-371">**연결 문자열 접두사**</span><span class="sxs-lookup"><span data-stu-id="5260e-371">**Connection string prefixes**</span></span>

<span data-ttu-id="5260e-372">구성 API에는 앱 환경에 대한 Azure 연결 문자열 구성과 관련된 네 개의 연결 문자열 환경 변수에 대한 특별한 처리 규칙이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-372">The Configuration API has special processing rules for four connection string environment variables involved in configuring Azure connection strings for the app environment.</span></span> <span data-ttu-id="5260e-373">즉, `AddEnvironmentVariables`에 접두사를 제공하지 않으면 표에 표시된 접두사가 붙은 환경 변수가 앱으로 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-373">Environment variables with the prefixes shown in the table are loaded into the app if no prefix is supplied to `AddEnvironmentVariables`.</span></span>

| <span data-ttu-id="5260e-374">연결 문자열 접두사</span><span class="sxs-lookup"><span data-stu-id="5260e-374">Connection string prefix</span></span> | <span data-ttu-id="5260e-375">공급자</span><span class="sxs-lookup"><span data-stu-id="5260e-375">Provider</span></span> |
| ------------------------ | -------- |
| `CUSTOMCONNSTR_` | <span data-ttu-id="5260e-376">사용자 지정 공급자</span><span class="sxs-lookup"><span data-stu-id="5260e-376">Custom provider</span></span> |
| `MYSQLCONNSTR_` | [<span data-ttu-id="5260e-377">MySQL</span><span class="sxs-lookup"><span data-stu-id="5260e-377">MySQL</span></span>](https://www.mysql.com/) |
| `SQLAZURECONNSTR_` | [<span data-ttu-id="5260e-378">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="5260e-378">Azure SQL Database</span></span>](https://azure.microsoft.com/services/sql-database/) |
| `SQLCONNSTR_` | [<span data-ttu-id="5260e-379">SQL Server</span><span class="sxs-lookup"><span data-stu-id="5260e-379">SQL Server</span></span>](https://www.microsoft.com/sql-server/) |

<span data-ttu-id="5260e-380">표에 표시된 네 개 접두사 중 하나가 붙은 환경 변수가 검색되어 구성으로 로드되면 다음과 같이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-380">When an environment variable is discovered and loaded into configuration with any of the four prefixes shown in the table:</span></span>

* <span data-ttu-id="5260e-381">환경 변수 접두사를 제거하고 구성 키 섹션(`ConnectionStrings`)을 추가하여 구성 키가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-381">The configuration key is created by removing the environment variable prefix and adding a configuration key section (`ConnectionStrings`).</span></span>
* <span data-ttu-id="5260e-382">데이터베이스 연결 제공자(지정된 공급자가 없는 `CUSTOMCONNSTR_` 제외)를 나타내는 새 구성 키-값 쌍이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-382">A new configuration key-value pair is created that represents the database connection provider (except for `CUSTOMCONNSTR_`, which has no stated provider).</span></span>

| <span data-ttu-id="5260e-383">환경 변수 키</span><span class="sxs-lookup"><span data-stu-id="5260e-383">Environment variable key</span></span> | <span data-ttu-id="5260e-384">변환된 구성 키</span><span class="sxs-lookup"><span data-stu-id="5260e-384">Converted configuration key</span></span> | <span data-ttu-id="5260e-385">공급자 구성 항목</span><span class="sxs-lookup"><span data-stu-id="5260e-385">Provider configuration entry</span></span>                                                    |
| ------------------------ | --------------------------- | ------------------------------------------------------------------------------- |
| `CUSTOMCONNSTR_<KEY>`    | `ConnectionStrings:<KEY>`   | <span data-ttu-id="5260e-386">구성 항목이 생성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-386">Configuration entry not created.</span></span>                                                |
| `MYSQLCONNSTR_<KEY>`     | `ConnectionStrings:<KEY>`   | <span data-ttu-id="5260e-387">키: `ConnectionStrings:<KEY>_ProviderName`:</span><span class="sxs-lookup"><span data-stu-id="5260e-387">Key: `ConnectionStrings:<KEY>_ProviderName`:</span></span><br><span data-ttu-id="5260e-388">값: `MySql.Data.MySqlClient`</span><span class="sxs-lookup"><span data-stu-id="5260e-388">Value: `MySql.Data.MySqlClient`</span></span> |
| `SQLAZURECONNSTR_<KEY>`  | `ConnectionStrings:<KEY>`   | <span data-ttu-id="5260e-389">키: `ConnectionStrings:<KEY>_ProviderName`:</span><span class="sxs-lookup"><span data-stu-id="5260e-389">Key: `ConnectionStrings:<KEY>_ProviderName`:</span></span><br><span data-ttu-id="5260e-390">값: `System.Data.SqlClient`</span><span class="sxs-lookup"><span data-stu-id="5260e-390">Value: `System.Data.SqlClient`</span></span>  |
| `SQLCONNSTR_<KEY>`       | `ConnectionStrings:<KEY>`   | <span data-ttu-id="5260e-391">키: `ConnectionStrings:<KEY>_ProviderName`:</span><span class="sxs-lookup"><span data-stu-id="5260e-391">Key: `ConnectionStrings:<KEY>_ProviderName`:</span></span><br><span data-ttu-id="5260e-392">값: `System.Data.SqlClient`</span><span class="sxs-lookup"><span data-stu-id="5260e-392">Value: `System.Data.SqlClient`</span></span>  |

## <a name="file-configuration-provider"></a><span data-ttu-id="5260e-393">파일 구성 공급자</span><span class="sxs-lookup"><span data-stu-id="5260e-393">File Configuration Provider</span></span>

<span data-ttu-id="5260e-394"><xref:Microsoft.Extensions.Configuration.FileConfigurationProvider>는 파일 시스템에서 구성을 로드하기 위한 기본 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-394"><xref:Microsoft.Extensions.Configuration.FileConfigurationProvider> is the base class for loading configuration from the file system.</span></span> <span data-ttu-id="5260e-395">다음 구성 공급자는 특정 파일 형식 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-395">The following configuration providers are dedicated to specific file types:</span></span>

* [<span data-ttu-id="5260e-396">INI 구성 공급자</span><span class="sxs-lookup"><span data-stu-id="5260e-396">INI Configuration Provider</span></span>](#ini-configuration-provider)
* [<span data-ttu-id="5260e-397">JSON 구성 공급자</span><span class="sxs-lookup"><span data-stu-id="5260e-397">JSON Configuration Provider</span></span>](#json-configuration-provider)
* [<span data-ttu-id="5260e-398">XML 구성 공급자</span><span class="sxs-lookup"><span data-stu-id="5260e-398">XML Configuration Provider</span></span>](#xml-configuration-provider)

### <a name="ini-configuration-provider"></a><span data-ttu-id="5260e-399">INI 구성 공급자</span><span class="sxs-lookup"><span data-stu-id="5260e-399">INI Configuration Provider</span></span>

<span data-ttu-id="5260e-400"><xref:Microsoft.Extensions.Configuration.Ini.IniConfigurationProvider>는 런타임에 INI 파일 키-값 쌍에서 구성을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-400">The <xref:Microsoft.Extensions.Configuration.Ini.IniConfigurationProvider> loads configuration from INI file key-value pairs at runtime.</span></span>

<span data-ttu-id="5260e-401">INI 파일 구성을 활성화하려면 <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder> 인스턴스에서 <xref:Microsoft.Extensions.Configuration.IniConfigurationExtensions.AddIniFile*> 확장 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-401">To activate INI file configuration, call the <xref:Microsoft.Extensions.Configuration.IniConfigurationExtensions.AddIniFile*> extension method on an instance of <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder>.</span></span>

<span data-ttu-id="5260e-402">콜론은 INI 파일 구성에서 콜론을 섹션 구분 기호로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-402">The colon can be used to as a section delimiter in INI file configuration.</span></span>

<span data-ttu-id="5260e-403">오버로드에서는 다음을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-403">Overloads permit specifying:</span></span>

* <span data-ttu-id="5260e-404">파일이 선택 사항인지 여부</span><span class="sxs-lookup"><span data-stu-id="5260e-404">Whether the file is optional.</span></span>
* <span data-ttu-id="5260e-405">파일이 변경되면 구성을 다시 로드하는지 여부</span><span class="sxs-lookup"><span data-stu-id="5260e-405">Whether the configuration is reloaded if the file changes.</span></span>
* <span data-ttu-id="5260e-406">파일에 액세스하는 데 사용되는 <xref:Microsoft.Extensions.FileProviders.IFileProvider></span><span class="sxs-lookup"><span data-stu-id="5260e-406">The <xref:Microsoft.Extensions.FileProviders.IFileProvider> used to access the file.</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="5260e-407">호스트를 빌드할 때 <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*>을 호출하여 앱의 구성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-407">Call <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*> when building the host to specify the app's configuration:</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateWebHostBuilder(args).Build().Run();
    }

    public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
        WebHost.CreateDefaultBuilder(args)
            .ConfigureAppConfiguration((hostingContext, config) =>
            {
                config.SetBasePath(Directory.GetCurrentDirectory());
                config.AddIniFile("config.ini", optional: true, reloadOnChange: true);
            })
            .UseStartup<Startup>();
}
```

<span data-ttu-id="5260e-408"><xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>을 직접 만들 경우 다음 구성으로 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*>을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-408">When creating a <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> directly, call <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> with the configuration:</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="5260e-409">`CreateDefaultBuilder`를 호출할 경우 다음 구성으로 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*>을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-409">When calling `CreateDefaultBuilder`, call <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> with the configuration:</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateWebHostBuilder(args).Build().Run();
    }

    public static IWebHostBuilder CreateWebHostBuilder(string[] args)
    {
        var config = new ConfigurationBuilder()
            .SetBasePath(Directory.GetCurrentDirectory())
            .AddIniFile("config.ini", optional: true, reloadOnChange: true)
            .Build();

        return WebHost.CreateDefaultBuilder(args)
            .UseConfiguration(config)
            .UseStartup<Startup>();
    }
}
```

<span data-ttu-id="5260e-410"><xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>을 직접 만들 경우 다음 구성으로 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*>을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-410">When creating a <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> directly, call <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> with the configuration:</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="5260e-411"><xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> 메서드를 사용하여 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>에 구성을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-411">Apply the configuration to <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> with the <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> method:</span></span>

::: moniker-end

```csharp
var config = new ConfigurationBuilder()
    .SetBasePath(Directory.GetCurrentDirectory())
    .AddIniFile("config.ini", optional: true, reloadOnChange: true)
    .Build();

var host = new WebHostBuilder()
    .UseConfiguration(config)
    .UseKestrel()
    .UseStartup<Startup>();
```

<span data-ttu-id="5260e-412">INI 구성 파일의 일반적인 예:</span><span class="sxs-lookup"><span data-stu-id="5260e-412">A generic example of an INI configuration file:</span></span>

```ini
[section0]
key0=value
key1=value

[section1]
subsection:key=value

[section2:subsection0]
key=value

[section2:subsection1]
key=value
```

<span data-ttu-id="5260e-413">이전 구성 파일은 `value`와 함께 다음 키를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-413">The previous configuration file loads the following keys with `value`:</span></span>

* <span data-ttu-id="5260e-414">section0:key0</span><span class="sxs-lookup"><span data-stu-id="5260e-414">section0:key0</span></span>
* <span data-ttu-id="5260e-415">section0:key1</span><span class="sxs-lookup"><span data-stu-id="5260e-415">section0:key1</span></span>
* <span data-ttu-id="5260e-416">section1:subsection:key</span><span class="sxs-lookup"><span data-stu-id="5260e-416">section1:subsection:key</span></span>
* <span data-ttu-id="5260e-417">section2:subsection0:key</span><span class="sxs-lookup"><span data-stu-id="5260e-417">section2:subsection0:key</span></span>
* <span data-ttu-id="5260e-418">section2:subsection1:key</span><span class="sxs-lookup"><span data-stu-id="5260e-418">section2:subsection1:key</span></span>

### <a name="json-configuration-provider"></a><span data-ttu-id="5260e-419">JSON 구성 공급자</span><span class="sxs-lookup"><span data-stu-id="5260e-419">JSON Configuration Provider</span></span>

<span data-ttu-id="5260e-420"><xref:Microsoft.Extensions.Configuration.Json.JsonConfigurationProvider>는 런타임에 JSON 파일 키-값 쌍에서 구성을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-420">The <xref:Microsoft.Extensions.Configuration.Json.JsonConfigurationProvider> loads configuration from JSON file key-value pairs during runtime.</span></span>

<span data-ttu-id="5260e-421">JSON 파일 구성을 활성화하려면 <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder> 인스턴스에서 <xref:Microsoft.Extensions.Configuration.JsonConfigurationExtensions.AddJsonFile*> 확장 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-421">To activate JSON file configuration, call the <xref:Microsoft.Extensions.Configuration.JsonConfigurationExtensions.AddJsonFile*> extension method on an instance of <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder>.</span></span>

<span data-ttu-id="5260e-422">오버로드에서는 다음을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-422">Overloads permit specifying:</span></span>

* <span data-ttu-id="5260e-423">파일이 선택 사항인지 여부</span><span class="sxs-lookup"><span data-stu-id="5260e-423">Whether the file is optional.</span></span>
* <span data-ttu-id="5260e-424">파일이 변경되면 구성을 다시 로드하는지 여부</span><span class="sxs-lookup"><span data-stu-id="5260e-424">Whether the configuration is reloaded if the file changes.</span></span>
* <span data-ttu-id="5260e-425">파일에 액세스하는 데 사용되는 <xref:Microsoft.Extensions.FileProviders.IFileProvider></span><span class="sxs-lookup"><span data-stu-id="5260e-425">The <xref:Microsoft.Extensions.FileProviders.IFileProvider> used to access the file.</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="5260e-426">`AddJsonFile`은 <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*>을 사용하여 새 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>를 초기화할 때 자동으로 두 번 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-426">`AddJsonFile` is automatically called twice when you initialize a new <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> with <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*>.</span></span> <span data-ttu-id="5260e-427">이 메서드는 호출되면 다음에서 구성을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-427">The method is called to load configuration from:</span></span>

* <span data-ttu-id="5260e-428">*appsettings.json* &ndash; 이 파일을 먼저 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-428">*appsettings.json* &ndash; This file is read first.</span></span> <span data-ttu-id="5260e-429">파일의 환경 버전이 *appsettings.json* 파일에서 제공한 값을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-429">The environment version of the file can override the values provided by the *appsettings.json* file.</span></span>
* <span data-ttu-id="5260e-430">*appsettings.{Environment}.json* &ndash; 파일의 환경 버전은 [IHostingEnvironment.EnvironmentName](xref:Microsoft.Extensions.Hosting.IHostingEnvironment.EnvironmentName*)을 기반으로 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-430">*appsettings.{Environment}.json* &ndash; The environment version of the file is loaded based on the [IHostingEnvironment.EnvironmentName](xref:Microsoft.Extensions.Hosting.IHostingEnvironment.EnvironmentName*).</span></span>

<span data-ttu-id="5260e-431">자세한 내용은 [웹 호스트: 호스트 설정](xref:fundamentals/host/web-host#set-up-a-host)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5260e-431">For more information, see [Web Host: Set up a host](xref:fundamentals/host/web-host#set-up-a-host).</span></span>

<span data-ttu-id="5260e-432">`CreateDefaultBuilder`는 다음 항목도 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-432">`CreateDefaultBuilder` also loads:</span></span>

* <span data-ttu-id="5260e-433">환경 변수.</span><span class="sxs-lookup"><span data-stu-id="5260e-433">Environment variables.</span></span>
* <span data-ttu-id="5260e-434">[사용자 비밀(비밀 관리자)](xref:security/app-secrets)(개발 환경에서)</span><span class="sxs-lookup"><span data-stu-id="5260e-434">[User secrets (Secret Manager)](xref:security/app-secrets) (in the Development environment).</span></span>
* <span data-ttu-id="5260e-435">명령줄 인수.</span><span class="sxs-lookup"><span data-stu-id="5260e-435">Command-line arguments.</span></span>

<span data-ttu-id="5260e-436">JSON 구성 공급자를 먼저 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-436">The JSON Configuration Provider is established first.</span></span> <span data-ttu-id="5260e-437">따라서 사용자 비밀, 환경 변수 및 명령줄 인수가 *appsettings* 파일에서 설정한 구성을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-437">Therefore, user secrets, environment variables, and command-line arguments override configuration set by the *appsettings* files.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="5260e-438">*appsettings.json* 및 *appsettings.{Environment}.json* 이외의 파일에 대한 앱 구성을 지정하도록 호스트를 빌드할 때 <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*>을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-438">Call <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*> when building the host to specify the app's configuration for files other than *appsettings.json* and *appsettings.{Environment}.json*:</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateWebHostBuilder(args).Build().Run();
    }

    public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
        WebHost.CreateDefaultBuilder(args)
            .ConfigureAppConfiguration((hostingContext, config) =>
            {
                config.SetBasePath(Directory.GetCurrentDirectory());
                config.AddJsonFile("config.json", optional: true, reloadOnChange: true);
            })
            .UseStartup<Startup>();
}
```

<span data-ttu-id="5260e-439"><xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>을 직접 만들 경우 다음 구성으로 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*>을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-439">When creating a <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> directly, call <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> with the configuration:</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="5260e-440"><xref:Microsoft.Extensions.Configuration.ConfigurationBuilder> 인스턴스에서 `AddJsonFile` 확장 메서드를 직접 호출할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-440">You can also directly call the `AddJsonFile` extension method on an instance of <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder>.</span></span>

<span data-ttu-id="5260e-441">`CreateDefaultBuilder`를 호출할 경우 다음 구성으로 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*>을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-441">When calling `CreateDefaultBuilder`, call <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> with the configuration:</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateWebHostBuilder(args).Build().Run();
    }

    public static IWebHostBuilder CreateWebHostBuilder(string[] args)
    {
        var config = new ConfigurationBuilder()
            .SetBasePath(Directory.GetCurrentDirectory())
            .AddJsonFile("config.json", optional: true, reloadOnChange: true)
            .Build();

        return WebHost.CreateDefaultBuilder(args)
            .UseConfiguration(config)
            .UseStartup<Startup>();
    }
}
```

<span data-ttu-id="5260e-442"><xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>을 직접 만들 경우 다음 구성으로 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*>을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-442">When creating a <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> directly, call <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> with the configuration:</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="5260e-443"><xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> 메서드를 사용하여 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>에 구성을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-443">Apply the configuration to <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> with the <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> method:</span></span>

::: moniker-end

```csharp
var config = new ConfigurationBuilder()
    .SetBasePath(Directory.GetCurrentDirectory())
    .AddJsonFile("config.json", optional: true, reloadOnChange: true)
    .Build();

var host = new WebHostBuilder()
    .UseConfiguration(config)
    .UseKestrel()
    .UseStartup<Startup>();
```

<span data-ttu-id="5260e-444">**예제**</span><span class="sxs-lookup"><span data-stu-id="5260e-444">**Example**</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="5260e-445">2.x 샘플 앱은 정적 편의 메서드 `CreateDefaultBuilder`를 활용하여 호스트를 빌드하며, `AddJsonFile` 두 번 호출도 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-445">The 2.x sample app takes advantage of the static convenience method `CreateDefaultBuilder` to build the host, which includes two calls to `AddJsonFile`.</span></span> <span data-ttu-id="5260e-446">구성은 *appsettings.json* 및 *appsettings.{Environment}.json*에서 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-446">Configuration is loaded from *appsettings.json* and *appsettings.{Environment}.json*.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="5260e-447">1.x 샘플 앱은 `ConfigurationBuilder`에서 `AddJsonFile`을 두 번 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-447">The 1.x sample app calls `AddJsonFile` twice on a `ConfigurationBuilder`.</span></span> <span data-ttu-id="5260e-448">구성은 *appsettings.json* 및 *appsettings.{Environment}.json*에서 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-448">Configuration is loaded from *appsettings.json* and *appsettings.{Environment}.json*.</span></span>

::: moniker-end

1. <span data-ttu-id="5260e-449">샘플 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-449">Run the sample app.</span></span> <span data-ttu-id="5260e-450">브라우저를 열어 `http://localhost:5000`의 앱으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-450">Open a browser to the app at `http://localhost:5000`.</span></span>
1. <span data-ttu-id="5260e-451">표에 표시된 대로 환경에 따라 다른 구성에 대한 키-값 쌍이 출력에 포함되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-451">Observe that the output contains key-value pairs for the configuration shown in the table depending on the environment.</span></span> <span data-ttu-id="5260e-452">로깅 구성 키는 콜론(`:`)을 계층 구분 기호로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-452">Logging configuration keys use the colon (`:`) as a hierarchical separator.</span></span>

| <span data-ttu-id="5260e-453">Key</span><span class="sxs-lookup"><span data-stu-id="5260e-453">Key</span></span>                        | <span data-ttu-id="5260e-454">개발 값</span><span class="sxs-lookup"><span data-stu-id="5260e-454">Development Value</span></span> | <span data-ttu-id="5260e-455">프로덕션 값</span><span class="sxs-lookup"><span data-stu-id="5260e-455">Production Value</span></span> |
| -------------------------- | :---------------: | :--------------: |
| <span data-ttu-id="5260e-456">Logging:LogLevel:System</span><span class="sxs-lookup"><span data-stu-id="5260e-456">Logging:LogLevel:System</span></span>    | <span data-ttu-id="5260e-457">정보</span><span class="sxs-lookup"><span data-stu-id="5260e-457">Information</span></span>       | <span data-ttu-id="5260e-458">정보</span><span class="sxs-lookup"><span data-stu-id="5260e-458">Information</span></span>      |
| <span data-ttu-id="5260e-459">Logging:LogLevel:Microsoft</span><span class="sxs-lookup"><span data-stu-id="5260e-459">Logging:LogLevel:Microsoft</span></span> | <span data-ttu-id="5260e-460">정보</span><span class="sxs-lookup"><span data-stu-id="5260e-460">Information</span></span>       | <span data-ttu-id="5260e-461">정보</span><span class="sxs-lookup"><span data-stu-id="5260e-461">Information</span></span>      |
| <span data-ttu-id="5260e-462">Logging:LogLevel:Default</span><span class="sxs-lookup"><span data-stu-id="5260e-462">Logging:LogLevel:Default</span></span>   | <span data-ttu-id="5260e-463">디버그</span><span class="sxs-lookup"><span data-stu-id="5260e-463">Debug</span></span>             | <span data-ttu-id="5260e-464">Error</span><span class="sxs-lookup"><span data-stu-id="5260e-464">Error</span></span>            |
| <span data-ttu-id="5260e-465">AllowedHosts</span><span class="sxs-lookup"><span data-stu-id="5260e-465">AllowedHosts</span></span>               | *                 | *                |

### <a name="xml-configuration-provider"></a><span data-ttu-id="5260e-466">XML 구성 공급자</span><span class="sxs-lookup"><span data-stu-id="5260e-466">XML Configuration Provider</span></span>

<span data-ttu-id="5260e-467"><xref:Microsoft.Extensions.Configuration.Xml.XmlConfigurationProvider>는 런타임에 XML 파일 키-값 쌍에서 구성을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-467">The <xref:Microsoft.Extensions.Configuration.Xml.XmlConfigurationProvider> loads configuration from XML file key-value pairs at runtime.</span></span>

<span data-ttu-id="5260e-468">XML 파일 구성을 활성화하려면 <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder> 인스턴스에서 <xref:Microsoft.Extensions.Configuration.XmlConfigurationExtensions.AddXmlFile*> 확장 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-468">To activate XML file configuration, call the <xref:Microsoft.Extensions.Configuration.XmlConfigurationExtensions.AddXmlFile*> extension method on an instance of <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder>.</span></span>

<span data-ttu-id="5260e-469">오버로드에서는 다음을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-469">Overloads permit specifying:</span></span>

* <span data-ttu-id="5260e-470">파일이 선택 사항인지 여부</span><span class="sxs-lookup"><span data-stu-id="5260e-470">Whether the file is optional.</span></span>
* <span data-ttu-id="5260e-471">파일이 변경되면 구성을 다시 로드하는지 여부</span><span class="sxs-lookup"><span data-stu-id="5260e-471">Whether the configuration is reloaded if the file changes.</span></span>
* <span data-ttu-id="5260e-472">파일에 액세스하는 데 사용되는 <xref:Microsoft.Extensions.FileProviders.IFileProvider></span><span class="sxs-lookup"><span data-stu-id="5260e-472">The <xref:Microsoft.Extensions.FileProviders.IFileProvider> used to access the file.</span></span>

<span data-ttu-id="5260e-473">구성 키-값 쌍이 생성되면 구성 파일의 루트 노드는 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-473">The root node of the configuration file is ignored when the configuration key-value pairs are created.</span></span> <span data-ttu-id="5260e-474">파일에 DTD(문서 종류 정의)나 네임스페이스는 지정하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="5260e-474">Don't specify a Document Type Definition (DTD) or namespace in the file.</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="5260e-475">호스트를 빌드할 때 <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*>을 호출하여 앱의 구성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-475">Call <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*> when building the host to specify the app's configuration:</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateWebHostBuilder(args).Build().Run();
    }

    public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
        WebHost.CreateDefaultBuilder(args)
            .ConfigureAppConfiguration((hostingContext, config) =>
            {
                config.SetBasePath(Directory.GetCurrentDirectory());
                config.AddXmlFile("config.xml", optional: true, reloadOnChange: true);
            })
            .UseStartup<Startup>();
}
```

<span data-ttu-id="5260e-476"><xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>을 직접 만들 경우 다음 구성으로 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*>을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-476">When creating a <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> directly, call <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> with the configuration:</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="5260e-477">`CreateDefaultBuilder`를 호출할 경우 다음 구성으로 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*>을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-477">When calling `CreateDefaultBuilder`, call <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> with the configuration:</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateWebHostBuilder(args).Build().Run();
    }

    public static IWebHostBuilder CreateWebHostBuilder(string[] args)
    {
        var config = new ConfigurationBuilder()
            .SetBasePath(Directory.GetCurrentDirectory())
            .AddXmlFile("config.xml", optional: true, reloadOnChange: true)
            .Build();

        return WebHost.CreateDefaultBuilder(args)
            .UseConfiguration(config)
            .UseStartup<Startup>();
    }
}
```

<span data-ttu-id="5260e-478"><xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>을 직접 만들 경우 다음 구성으로 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*>을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-478">When creating a <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> directly, call <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> with the configuration:</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="5260e-479"><xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> 메서드를 사용하여 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>에 구성을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-479">Apply the configuration to <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> with the <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> method:</span></span>

::: moniker-end

```csharp
var config = new ConfigurationBuilder()
    .SetBasePath(Directory.GetCurrentDirectory())
    .AddXmlFile("config.xml", optional: true, reloadOnChange: true)
    .Build();

var host = new WebHostBuilder()
    .UseConfiguration(config)
    .UseKestrel()
    .UseStartup<Startup>();
```

<span data-ttu-id="5260e-480">XML 구성 파일에서는 반복 섹션에 고유 요소 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-480">XML configuration files can use distinct element names for repeating sections:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <section0>
    <key0>value</key0>
    <key1>value</key1>
  </section0>
  <section1>
    <key0>value</key0>
    <key1>value</key1>
  </section1>
</configuration>
```

<span data-ttu-id="5260e-481">이전 구성 파일은 `value`와 함께 다음 키를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-481">The previous configuration file loads the following keys with `value`:</span></span>

* <span data-ttu-id="5260e-482">section0:key0</span><span class="sxs-lookup"><span data-stu-id="5260e-482">section0:key0</span></span>
* <span data-ttu-id="5260e-483">section0:key1</span><span class="sxs-lookup"><span data-stu-id="5260e-483">section0:key1</span></span>
* <span data-ttu-id="5260e-484">section1:key0</span><span class="sxs-lookup"><span data-stu-id="5260e-484">section1:key0</span></span>
* <span data-ttu-id="5260e-485">section1:key1</span><span class="sxs-lookup"><span data-stu-id="5260e-485">section1:key1</span></span>

<span data-ttu-id="5260e-486">같은 요소 이름을 사용하는 반복 요소는 다음과 같이 `name` 특성을 사용하여 요소를 구분하면 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-486">Repeating elements that use the same element name work if the `name` attribute is used to distinguish the elements:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <section name="section0">
    <key name="key0">value</key>
    <key name="key1">value</key>
  </section>
  <section name="section1">
    <key name="key0">value</key>
    <key name="key1">value</key>
  </section>
</configuration>
```

<span data-ttu-id="5260e-487">이전 구성 파일은 `value`와 함께 다음 키를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-487">The previous configuration file loads the following keys with `value`:</span></span>

* <span data-ttu-id="5260e-488">section:section0:key:key0</span><span class="sxs-lookup"><span data-stu-id="5260e-488">section:section0:key:key0</span></span>
* <span data-ttu-id="5260e-489">section:section0:key:key1</span><span class="sxs-lookup"><span data-stu-id="5260e-489">section:section0:key:key1</span></span>
* <span data-ttu-id="5260e-490">section:section1:key:key0</span><span class="sxs-lookup"><span data-stu-id="5260e-490">section:section1:key:key0</span></span>
* <span data-ttu-id="5260e-491">section:section1:key:key1</span><span class="sxs-lookup"><span data-stu-id="5260e-491">section:section1:key:key1</span></span>

<span data-ttu-id="5260e-492">특성을 사용하여 값을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-492">Attributes can be used to supply values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <key attribute="value" />
  <section>
    <key attribute="value" />
  </section>
</configuration>
```

<span data-ttu-id="5260e-493">이전 구성 파일은 `value`와 함께 다음 키를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-493">The previous configuration file loads the following keys with `value`:</span></span>

* <span data-ttu-id="5260e-494">key:attribute</span><span class="sxs-lookup"><span data-stu-id="5260e-494">key:attribute</span></span>
* <span data-ttu-id="5260e-495">section:key:attribute</span><span class="sxs-lookup"><span data-stu-id="5260e-495">section:key:attribute</span></span>

::: moniker range=">= aspnetcore-2.1"

## <a name="key-per-file-configuration-provider"></a><span data-ttu-id="5260e-496">파일별 키 구성 공급자</span><span class="sxs-lookup"><span data-stu-id="5260e-496">Key-per-file Configuration Provider</span></span>

<span data-ttu-id="5260e-497"><xref:Microsoft.Extensions.Configuration.KeyPerFile.KeyPerFileConfigurationProvider>는 디렉터리의 파일을 구성 키-값 쌍으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-497">The <xref:Microsoft.Extensions.Configuration.KeyPerFile.KeyPerFileConfigurationProvider> uses a directory's files as configuration key-value pairs.</span></span> <span data-ttu-id="5260e-498">키는 파일 이름이고,</span><span class="sxs-lookup"><span data-stu-id="5260e-498">The key is the file name.</span></span> <span data-ttu-id="5260e-499">값은 파일의 콘텐츠를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-499">The value contains the file's contents.</span></span> <span data-ttu-id="5260e-500">파일별 키 구성 공급자는 Docker 호스팅 시나리오에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-500">The Key-per-file Configuration Provider is used in Docker hosting scenarios.</span></span>

<span data-ttu-id="5260e-501">파일별 키 구성을 활성화하려면 <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder> 인스턴스에서 <xref:Microsoft.Extensions.Configuration.KeyPerFileConfigurationBuilderExtensions.AddKeyPerFile*> 확장 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-501">To activate key-per-file configuration, call the <xref:Microsoft.Extensions.Configuration.KeyPerFileConfigurationBuilderExtensions.AddKeyPerFile*> extension method on an instance of <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder>.</span></span> <span data-ttu-id="5260e-502">파일의 `directoryPath`는 절대 경로여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-502">The `directoryPath` to the files must be an absolute path.</span></span>

<span data-ttu-id="5260e-503">오버로드에서는 다음을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-503">Overloads permit specifying:</span></span>

* <span data-ttu-id="5260e-504">소스를 구성하는 `Action<KeyPerFileConfigurationSource>` 대리자</span><span class="sxs-lookup"><span data-stu-id="5260e-504">An `Action<KeyPerFileConfigurationSource>` delegate that configures the source.</span></span>
* <span data-ttu-id="5260e-505">디렉터리가 선택 사항인지 여부와 디렉터리의 경로</span><span class="sxs-lookup"><span data-stu-id="5260e-505">Whether the directory is optional and the path to the directory.</span></span>

<span data-ttu-id="5260e-506">호스트를 빌드할 때 <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*>을 호출하여 앱의 구성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-506">Call <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*> when building the host to specify the app's configuration:</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateWebHostBuilder(args).Build().Run();
    }

    public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
        WebHost.CreateDefaultBuilder(args)
            .ConfigureAppConfiguration((hostingContext, config) =>
            {
                config.SetBasePath(Directory.GetCurrentDirectory());
                config.AddKeyPerFile(directoryPath: path, optional: true);
            })
            .UseStartup<Startup>();
}
```

<span data-ttu-id="5260e-507"><xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>을 직접 만들 경우 다음 구성으로 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*>을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-507">When creating a <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> directly, call <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> with the configuration:</span></span>

```csharp
var path = Path.Combine(Directory.GetCurrentDirectory(), "path/to/files");
var config = new ConfigurationBuilder()
    .AddKeyPerFile(directoryPath: path, optional: true)
    .Build();

var host = new WebHostBuilder()
    .UseConfiguration(config)
    .UseKestrel()
    .UseStartup<Startup>();
```

::: moniker-end

## <a name="memory-configuration-provider"></a><span data-ttu-id="5260e-508">메모리 구성 공급자</span><span class="sxs-lookup"><span data-stu-id="5260e-508">Memory Configuration Provider</span></span>

<span data-ttu-id="5260e-509"><xref:Microsoft.Extensions.Configuration.Memory.MemoryConfigurationProvider>는 메모리 내 컬렉션을 구성 키-값 쌍으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-509">The <xref:Microsoft.Extensions.Configuration.Memory.MemoryConfigurationProvider> uses an in-memory collection as configuration key-value pairs.</span></span>

<span data-ttu-id="5260e-510">메모리 내 컬렉션 구성을 활성화하려면 <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder> 인스턴스에서 <xref:Microsoft.Extensions.Configuration.MemoryConfigurationBuilderExtensions.AddInMemoryCollection*> 확장 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-510">To activate in-memory collection configuration, call the <xref:Microsoft.Extensions.Configuration.MemoryConfigurationBuilderExtensions.AddInMemoryCollection*> extension method on an instance of <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder>.</span></span>

<span data-ttu-id="5260e-511">`IEnumerable<KeyValuePair<String,String>>`을 사용하여 구성 공급자를 초기화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-511">The configuration provider can be initialized with an `IEnumerable<KeyValuePair<String,String>>`.</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="5260e-512">호스트를 빌드할 때 <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*>을 호출하여 앱의 구성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-512">Call <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*> when building the host to specify the app's configuration:</span></span>

```csharp
public class Program
{
    public static readonly Dictionary<string, string> _dict = 
        new Dictionary<string, string>
        {
            {"MemoryCollectionKey1", "value1"},
            {"MemoryCollectionKey2", "value2"}
        };

    public static void Main(string[] args)
    {
        CreateWebHostBuilder(args).Build().Run();
    }

    public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
        WebHost.CreateDefaultBuilder(args)
            .ConfigureAppConfiguration((hostingContext, config) =>
            {
                config.AddInMemoryCollection(_dict);
            })
            .UseStartup<Startup>();
}
```

<span data-ttu-id="5260e-513"><xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>을 직접 만들 경우 다음 구성으로 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*>을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-513">When creating a <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> directly, call <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> with the configuration:</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="5260e-514">`CreateDefaultBuilder`를 호출할 경우 다음 구성으로 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*>을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-514">When calling `CreateDefaultBuilder`, call <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> with the configuration:</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateWebHostBuilder(args).Build().Run();
    }

    public static IWebHostBuilder CreateWebHostBuilder(string[] args)
    {
        var dict = new Dictionary<string, string>
            {
                {"MemoryCollectionKey1", "value1"},
                {"MemoryCollectionKey2", "value2"}
            };

        var config = new ConfigurationBuilder()
            .AddInMemoryCollection(dict)
            .Build();

        return WebHost.CreateDefaultBuilder(args)
            .UseConfiguration(config)
            .UseStartup<Startup>();
    }
}
```

<span data-ttu-id="5260e-515"><xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>을 직접 만들 경우 다음 구성으로 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*>을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-515">When creating a <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> directly, call <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> with the configuration:</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="5260e-516"><xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> 메서드를 사용하여 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>에 구성을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-516">Apply the configuration to <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> with the <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> method:</span></span>

::: moniker-end

```csharp
var dict = new Dictionary<string, string>
    {
        {"MemoryCollectionKey1", "value1"},
        {"MemoryCollectionKey2", "value2"}
    };

var config = new ConfigurationBuilder()
    .AddInMemoryCollection(dict)
    .Build();

var host = new WebHostBuilder()
    .UseConfiguration(config)
    .UseKestrel()
    .UseStartup<Startup>();
```

## <a name="getvalue"></a><span data-ttu-id="5260e-517">GetValue</span><span class="sxs-lookup"><span data-stu-id="5260e-517">GetValue</span></span>

<span data-ttu-id="5260e-518">[ConfigurationBinder.GetValue&lt;T&gt;](xref:Microsoft.Extensions.Configuration.ConfigurationBinder.GetValue*)는 지정된 키를 사용하여 구성에서 값을 추출하고 이 값을 지정된 형식으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-518">[ConfigurationBinder.GetValue&lt;T&gt;](xref:Microsoft.Extensions.Configuration.ConfigurationBinder.GetValue*) extracts a value from configuration with a specified key and converts it to the specified type.</span></span> <span data-ttu-id="5260e-519">오버로드를 사용하면 키를 찾을 수 없는 경우 기본값을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-519">An overload permits you to provide a default value if the key isn't found.</span></span>

<span data-ttu-id="5260e-520">다음 예제에서는 `NumberKey` 키를 사용하여 구성에서 문자열 값을 추출하고, 값을 `int`로 입력하고, 값을 `intValue` 변수에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-520">The following example extracts the string value from configuration with the key `NumberKey`, types the value as an `int`, and stores the value in the variable `intValue`.</span></span> <span data-ttu-id="5260e-521">구성 키에서 `NumberKey`을 찾을 수 없으면 `intValue`는 기본값 `99`를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-521">If `NumberKey` isn't found in the configuration keys, `intValue` receives the default value of `99`:</span></span>

```csharp
var intValue = config.GetValue<int>("NumberKey", 99);
```

## <a name="getsection-getchildren-and-exists"></a><span data-ttu-id="5260e-522">GetSection, GetChildren 및 Exists</span><span class="sxs-lookup"><span data-stu-id="5260e-522">GetSection, GetChildren, and Exists</span></span>

<span data-ttu-id="5260e-523">이어지는 예제에서는 다음 JSON 파일을 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="5260e-523">For the examples that follow, consider the following JSON file.</span></span> <span data-ttu-id="5260e-524">네 개의 키가 두 개 섹션에 있고, 두 섹션 중 하나에는 하위 섹션 쌍이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-524">Four keys are found across two sections, one of which includes a pair of subsections:</span></span>

```json
{
  "section0": {
    "key0": "value",
    "key1": "value"
  },
  "section1": {
    "key0": "value",
    "key1": "value"
  },
  "section2": {
    "subsection0" : {
      "key0": "value",
      "key1": "value"
    },
    "subsection1" : {
      "key0": "value",
      "key1": "value"
    }
  }
}
```

<span data-ttu-id="5260e-525">파일을 구성으로 읽어 들이면 구성 값을 저장하기 위해 다음과 같은 고유한 계층 키가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-525">When the file is read into configuration, the following unique hierarchical keys are created to hold the configuration values:</span></span>

* <span data-ttu-id="5260e-526">section0:key0</span><span class="sxs-lookup"><span data-stu-id="5260e-526">section0:key0</span></span>
* <span data-ttu-id="5260e-527">section0:key1</span><span class="sxs-lookup"><span data-stu-id="5260e-527">section0:key1</span></span>
* <span data-ttu-id="5260e-528">section1:key0</span><span class="sxs-lookup"><span data-stu-id="5260e-528">section1:key0</span></span>
* <span data-ttu-id="5260e-529">section1:key1</span><span class="sxs-lookup"><span data-stu-id="5260e-529">section1:key1</span></span>
* <span data-ttu-id="5260e-530">section2:subsection0:key0</span><span class="sxs-lookup"><span data-stu-id="5260e-530">section2:subsection0:key0</span></span>
* <span data-ttu-id="5260e-531">section2:subsection0:key1</span><span class="sxs-lookup"><span data-stu-id="5260e-531">section2:subsection0:key1</span></span>
* <span data-ttu-id="5260e-532">section2:subsection1:key0</span><span class="sxs-lookup"><span data-stu-id="5260e-532">section2:subsection1:key0</span></span>
* <span data-ttu-id="5260e-533">section2:subsection1:key1</span><span class="sxs-lookup"><span data-stu-id="5260e-533">section2:subsection1:key1</span></span>

### <a name="getsection"></a><span data-ttu-id="5260e-534">GetSection</span><span class="sxs-lookup"><span data-stu-id="5260e-534">GetSection</span></span>

<span data-ttu-id="5260e-535">[IConfiguration.GetSection](xref:Microsoft.Extensions.Configuration.IConfiguration.GetSection*)은 지정된 하위 섹션 키를 사용하여 구성 하위 섹션을 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-535">[IConfiguration.GetSection](xref:Microsoft.Extensions.Configuration.IConfiguration.GetSection*) extracts a configuration subsection with the specified subsection key.</span></span>

<span data-ttu-id="5260e-536">`section1`의 키-값 쌍만 포함하는 <xref:Microsoft.Extensions.Configuration.IConfigurationSection>을 반환하려면 `GetSection`을 호출하고 섹션 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-536">To return an <xref:Microsoft.Extensions.Configuration.IConfigurationSection> containing only the key-value pairs in `section1`, call `GetSection` and supply the section name:</span></span>

```csharp
var configSection = _config.GetSection("section1");
```

<span data-ttu-id="5260e-537">마찬가지로 `section2:subsection0`의 키 값을 가져오려면 `GetSection`을 호출하고 섹션 경로를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-537">Similarly, to obtain the values for keys in `section2:subsection0`, call `GetSection` and supply the section path:</span></span>

```csharp
var configSection = _config.GetSection("section2:subsection0");
```

<span data-ttu-id="5260e-538">`GetSection`은 `null`을 반환하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-538">`GetSection` never returns `null`.</span></span> <span data-ttu-id="5260e-539">일치하는 섹션을 찾을 수 없으면 빈 `IConfigurationSection`이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-539">If a matching section isn't found, an empty `IConfigurationSection` is returned.</span></span>

### <a name="getchildren"></a><span data-ttu-id="5260e-540">GetChildren</span><span class="sxs-lookup"><span data-stu-id="5260e-540">GetChildren</span></span>

<span data-ttu-id="5260e-541">`section2`에서 [IConfiguration.GetChildren](xref:Microsoft.Extensions.Configuration.IConfiguration.GetChildren*)을 호출하면 다음을 포함하는 `IEnumerable<IConfigurationSection>`이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-541">A call to [IConfiguration.GetChildren](xref:Microsoft.Extensions.Configuration.IConfiguration.GetChildren*) on `section2` obtains an `IEnumerable<IConfigurationSection>` that includes:</span></span>

* `subsection0`
* `subsection1`

```csharp
var configSection = _config.GetSection("section2");

var children = configSection.GetChildren();
```

::: moniker range=">= aspnetcore-2.0"

### <a name="exists"></a><span data-ttu-id="5260e-542">있음</span><span class="sxs-lookup"><span data-stu-id="5260e-542">Exists</span></span>

<span data-ttu-id="5260e-543">[ConfigurationExtensions.Exists](xref:Microsoft.Extensions.Configuration.ConfigurationExtensions.Exists*)를 사용하면 구성 섹션이 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-543">Use [ConfigurationExtensions.Exists](xref:Microsoft.Extensions.Configuration.ConfigurationExtensions.Exists*) to determine if a configuration section exists:</span></span>

```csharp
var sectionExists = _config.GetSection("section2:subsection2").Exists();
```

<span data-ttu-id="5260e-544">예제 데이터의 경우 구성 데이터에 `section2:subsection2` 섹션이 없으므로 `sectionExists`는 `false`입니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-544">Given the example data, `sectionExists` is `false` because there isn't a `section2:subsection2` section in the configuration data.</span></span>

::: moniker-end

## <a name="bind-to-a-class"></a><span data-ttu-id="5260e-545">클래스에 바인딩</span><span class="sxs-lookup"><span data-stu-id="5260e-545">Bind to a class</span></span>

<span data-ttu-id="5260e-546">‘옵션 패턴’을 사용하여 관련 설정 그룹을 나타내는 클래스에 구성을 바인딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-546">Configuration can be bound to classes that represent groups of related settings using the *options pattern*.</span></span> <span data-ttu-id="5260e-547">자세한 내용은 <xref:fundamentals/configuration/options>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5260e-547">For more information, see <xref:fundamentals/configuration/options>.</span></span>

<span data-ttu-id="5260e-548">구성 값이 문자열로 반환되지만, <xref:Microsoft.Extensions.Configuration.ConfigurationBinder.Bind*>를 호출하면 [POCO](https://wikipedia.org/wiki/Plain_Old_CLR_Object) 개체를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-548">Configuration values are returned as strings, but calling <xref:Microsoft.Extensions.Configuration.ConfigurationBinder.Bind*> enables the construction of [POCO](https://wikipedia.org/wiki/Plain_Old_CLR_Object) objects.</span></span>

<span data-ttu-id="5260e-549">샘플 앱은 `Starship` 모델(*Models/Starship.cs*)을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-549">The sample app contains a `Starship` model (*Models/Starship.cs*):</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/samples/2.x/ConfigurationSample/Models/Starship.cs?name=snippet1)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/samples/1.x/ConfigurationSample/Models/Starship.cs?name=snippet1)]

::: moniker-end

<span data-ttu-id="5260e-550">샘플 앱이 JSON 구성 공급자를 사용하여 구성을 로드하는 경우 *starship.json* 파일의 `starship` 섹션에서 구성을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-550">The `starship` section of the *starship.json* file creates the configuration when the sample app uses the JSON Configuration Provider to load the configuration:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-json[](index/samples/2.x/ConfigurationSample/starship.json)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-json[](index/samples/1.x/ConfigurationSample/starship.json)]

::: moniker-end

<span data-ttu-id="5260e-551">다음 구성 키-값 쌍이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-551">The following configuration key-value pairs are created:</span></span>

| <span data-ttu-id="5260e-552">Key</span><span class="sxs-lookup"><span data-stu-id="5260e-552">Key</span></span>                   | <span data-ttu-id="5260e-553">값</span><span class="sxs-lookup"><span data-stu-id="5260e-553">Value</span></span>                                             |
| --------------------- | ------------------------------------------------- |
| <span data-ttu-id="5260e-554">starship:name</span><span class="sxs-lookup"><span data-stu-id="5260e-554">starship:name</span></span>         | <span data-ttu-id="5260e-555">USS Enterprise</span><span class="sxs-lookup"><span data-stu-id="5260e-555">USS Enterprise</span></span>                                    |
| <span data-ttu-id="5260e-556">starship:registry</span><span class="sxs-lookup"><span data-stu-id="5260e-556">starship:registry</span></span>     | <span data-ttu-id="5260e-557">NCC-1701</span><span class="sxs-lookup"><span data-stu-id="5260e-557">NCC-1701</span></span>                                          |
| <span data-ttu-id="5260e-558">starship:class</span><span class="sxs-lookup"><span data-stu-id="5260e-558">starship:class</span></span>        | <span data-ttu-id="5260e-559">Constitution</span><span class="sxs-lookup"><span data-stu-id="5260e-559">Constitution</span></span>                                      |
| <span data-ttu-id="5260e-560">starship:length</span><span class="sxs-lookup"><span data-stu-id="5260e-560">starship:length</span></span>       | <span data-ttu-id="5260e-561">304.8</span><span class="sxs-lookup"><span data-stu-id="5260e-561">304.8</span></span>                                             |
| <span data-ttu-id="5260e-562">starship:commissioned</span><span class="sxs-lookup"><span data-stu-id="5260e-562">starship:commissioned</span></span> | <span data-ttu-id="5260e-563">False</span><span class="sxs-lookup"><span data-stu-id="5260e-563">False</span></span>                                             |
| <span data-ttu-id="5260e-564">trademark</span><span class="sxs-lookup"><span data-stu-id="5260e-564">trademark</span></span>             | <span data-ttu-id="5260e-565">Paramount Pictures Corp. http://www.paramount.com</span><span class="sxs-lookup"><span data-stu-id="5260e-565">Paramount Pictures Corp. http://www.paramount.com</span></span> |

<span data-ttu-id="5260e-566">샘플 앱은 `starship` 키를 사용하여 `GetSection`을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-566">The sample app calls `GetSection` with the `starship` key.</span></span> <span data-ttu-id="5260e-567">`starship` 키-값 쌍은 격리됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-567">The `starship` key-value pairs are isolated.</span></span> <span data-ttu-id="5260e-568">`Bind` 메서드는 `Starship` 클래스의 인스턴스를 전달하는 하위 섹션에서 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-568">The `Bind` method is called on the subsection passing in an instance of the `Starship` class.</span></span> <span data-ttu-id="5260e-569">인스턴스 값을 바인딩한 후 인스턴스는 렌더링할 속성에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-569">After binding the instance values, the instance is assigned to a property for rendering:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/samples/2.x/ConfigurationSample/Pages/Index.cshtml.cs?name=snippet_starship)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/samples/1.x/ConfigurationSample/Controllers/HomeController.cs?name=snippet_starship)]

::: moniker-end

## <a name="bind-to-an-object-graph"></a><span data-ttu-id="5260e-570">개체 그래프에 바인딩</span><span class="sxs-lookup"><span data-stu-id="5260e-570">Bind to an object graph</span></span>

<span data-ttu-id="5260e-571"><xref:Microsoft.Extensions.Configuration.ConfigurationBinder.Bind*>는 전체 POCO 개체 그래프를 바인딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-571"><xref:Microsoft.Extensions.Configuration.ConfigurationBinder.Bind*> is capable of binding an entire POCO object graph.</span></span>

<span data-ttu-id="5260e-572">다음 샘플은 개체 그래프에`Metadata` 및 `Actors` 클래스가 포함된 `TvShow` 모델(*Models/TvShow.cs*)을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-572">The sample contains a `TvShow` model whose object graph includes `Metadata` and `Actors` classes (*Models/TvShow.cs*):</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/samples/2.x/ConfigurationSample/Models/TvShow.cs?name=snippet1)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/samples/1.x/ConfigurationSample/Models/TvShow.cs?name=snippet1)]

::: moniker-end

<span data-ttu-id="5260e-573">샘플 앱의 *tvshow.xml* 파일에는 다음 구성 데이터가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-573">The sample app has a *tvshow.xml* file containing the configuration data:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-xml[](index/samples/2.x/ConfigurationSample/tvshow.xml)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-xml[](index/samples/1.x/ConfigurationSample/tvshow.xml)]

::: moniker-end

<span data-ttu-id="5260e-574">`Bind` 메서드를 사용하여 전체 `TvShow` 개체 그래프에 구성을 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-574">Configuration is bound to the entire `TvShow` object graph with the `Bind` method.</span></span> <span data-ttu-id="5260e-575">바인딩된 인스턴스는 렌더링할 속성에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-575">The bound instance is assigned to a property for rendering:</span></span>

::: moniker range=">= aspnetcore-2.0"

```csharp
var tvShow = new TvShow();
_config.GetSection("tvshow").Bind(tvShow);
TvShow = tvShow;
```

::: moniker-end

::: moniker range="< aspnetcore-2.0"

```csharp
var tvShow = new TvShow();
_config.GetSection("tvshow").Bind(tvShow);
viewModel.TvShow = tvShow;
```

::: moniker-end

::: moniker range=">= aspnetcore-1.1"

<span data-ttu-id="5260e-576">[ConfigurationBinder.Get&lt;T&gt;](xref:Microsoft.Extensions.Configuration.ConfigurationBinder.Get*)는 지정된 형식을 바인딩하고 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-576">[ConfigurationBinder.Get&lt;T&gt;](xref:Microsoft.Extensions.Configuration.ConfigurationBinder.Get*) binds and returns the specified type.</span></span> <span data-ttu-id="5260e-577">`Get<T>`가 `Bind`보다 사용하기 더 간편합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-577">`Get<T>` is more convenient than using `Bind`.</span></span> <span data-ttu-id="5260e-578">다음 코드에서는 앞의 예제에 `Get<T>`를 사용하여 바인딩된 인스턴스가 렌더링에 사용되는 속성에 바로 할당될 수 있도록 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-578">The following code shows how to use `Get<T>` with the preceding example, which allows the bound instance to be directly assigned to the property used for rendering:</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/samples/2.x/ConfigurationSample/Pages/Index.cshtml.cs?name=snippet_tvshow)]

::: moniker-end

::: moniker range="= aspnetcore-1.1"

[!code-csharp[](index/samples/1.x/ConfigurationSample/Controllers/HomeController.cs?name=snippet_tvshow)]

::: moniker-end

## <a name="bind-an-array-to-a-class"></a><span data-ttu-id="5260e-579">클래스에 배열 바인딩</span><span class="sxs-lookup"><span data-stu-id="5260e-579">Bind an array to a class</span></span>

<span data-ttu-id="5260e-580">다음 샘플 앱은 이 섹션에서 설명하는 개념을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-580">*The sample app demonstrates the concepts explained in this section.*</span></span>

<span data-ttu-id="5260e-581"><xref:Microsoft.Extensions.Configuration.ConfigurationBinder.Bind*>는 구성 키에 배열 인덱스를 사용하여 배열을 개체에 바인딩하는 것을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-581">The <xref:Microsoft.Extensions.Configuration.ConfigurationBinder.Bind*> supports binding arrays to objects using array indices in configuration keys.</span></span> <span data-ttu-id="5260e-582">숫자 키 세그먼트(`:0:`, `:1:`, &hellip; `:{n}:`)를 노출하는 모든 배열 형식은 POCO 클래스 배열에 배열 바인딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-582">Any array format that exposes a numeric key segment (`:0:`, `:1:`, &hellip; `:{n}:`) is capable of array binding to a POCO class array.</span></span>

> [!NOTE]
> <span data-ttu-id="5260e-583">바인딩은 규칙에 따라 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-583">Binding is provided by convention.</span></span> <span data-ttu-id="5260e-584">배열 바인딩을 구현하기 위해 사용자 지정 구성 공급자가 필요하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-584">Custom configuration providers aren't required to implement array binding.</span></span>

<span data-ttu-id="5260e-585">**메모리 내 배열 처리**</span><span class="sxs-lookup"><span data-stu-id="5260e-585">**In-memory array processing**</span></span>

<span data-ttu-id="5260e-586">다음 표에 표시된 구성 키 및 값을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="5260e-586">Consider the configuration keys and values shown in the following table.</span></span>

| <span data-ttu-id="5260e-587">Key</span><span class="sxs-lookup"><span data-stu-id="5260e-587">Key</span></span>     | <span data-ttu-id="5260e-588">값</span><span class="sxs-lookup"><span data-stu-id="5260e-588">Value</span></span>  |
| :-----: | :----: |
| <span data-ttu-id="5260e-589">array:0</span><span class="sxs-lookup"><span data-stu-id="5260e-589">array:0</span></span> | <span data-ttu-id="5260e-590">value0</span><span class="sxs-lookup"><span data-stu-id="5260e-590">value0</span></span> |
| <span data-ttu-id="5260e-591">array:1</span><span class="sxs-lookup"><span data-stu-id="5260e-591">array:1</span></span> | <span data-ttu-id="5260e-592">value1</span><span class="sxs-lookup"><span data-stu-id="5260e-592">value1</span></span> |
| <span data-ttu-id="5260e-593">array:2</span><span class="sxs-lookup"><span data-stu-id="5260e-593">array:2</span></span> | <span data-ttu-id="5260e-594">value2</span><span class="sxs-lookup"><span data-stu-id="5260e-594">value2</span></span> |
| <span data-ttu-id="5260e-595">array:4</span><span class="sxs-lookup"><span data-stu-id="5260e-595">array:4</span></span> | <span data-ttu-id="5260e-596">value4</span><span class="sxs-lookup"><span data-stu-id="5260e-596">value4</span></span> |
| <span data-ttu-id="5260e-597">array:5</span><span class="sxs-lookup"><span data-stu-id="5260e-597">array:5</span></span> | <span data-ttu-id="5260e-598">value5</span><span class="sxs-lookup"><span data-stu-id="5260e-598">value5</span></span> |

<span data-ttu-id="5260e-599">메모리 구성 공급자를 사용하는 샘플 앱에서는 다음과 같은 키 및 값이 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-599">These keys and values are loaded in the sample app using the Memory Configuration Provider:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/samples/2.x/ConfigurationSample/Program.cs?name=snippet_Program&highlight=3-10,22)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/samples/1.x/ConfigurationSample/Startup.cs?name=snippet_Startup&highlight=5-12,16)]

::: moniker-end

<span data-ttu-id="5260e-600">배열은 인덱스 &num;3에 대한 값을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-600">The array skips a value for index &num;3.</span></span> <span data-ttu-id="5260e-601">구성 바인더는 null 값을 바인딩하거나 바인딩된 개체에 null 항목을 만들 수 없으며, 이 점은 이 배열을 개체에 바인딩한 결과를 설명할 때 명확해집니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-601">The configuration binder isn't capable of binding null values or creating null entries in bound objects, which becomes clear in a moment when the result of binding this array to an object is demonstrated.</span></span>

<span data-ttu-id="5260e-602">샘플 앱에서는 POCO 클래스를 사용하여 바인딩된 구성 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-602">In the sample app, a POCO class is available to hold the bound configuration data:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/samples/2.x/ConfigurationSample/Models/ArrayExample.cs?name=snippet1)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/samples/1.x/ConfigurationSample/Models/ArrayExample.cs?name=snippet1)]

::: moniker-end

<span data-ttu-id="5260e-603">구성 데이터는 개체에 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-603">The configuration data is bound to the object:</span></span>

```csharp
var arrayExample = new ArrayExample();
_config.GetSection("array").Bind(arrayExample);
```

::: moniker range=">= aspnetcore-1.1"

<span data-ttu-id="5260e-604">[ConfigurationBinder.Get&lt;T&gt;](xref:Microsoft.Extensions.Configuration.ConfigurationBinder.Get*) 구문도 사용할 수 있으며, 이 경우 코드가 더 간결해집니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-604">[ConfigurationBinder.Get&lt;T&gt;](xref:Microsoft.Extensions.Configuration.ConfigurationBinder.Get*) syntax can also be used, which results in more compact code:</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/samples/2.x/ConfigurationSample/Pages/Index.cshtml.cs?name=snippet_array)]

::: moniker-end

::: moniker range="= aspnetcore-1.1"

[!code-csharp[](index/samples/1.x/ConfigurationSample/Controllers/HomeController.cs?name=snippet_array)]

::: moniker-end

<span data-ttu-id="5260e-605">바인딩된 개체 즉, `ArrayExample`의 인스턴스는 구성에서 배열 데이터를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-605">The bound object, an instance of `ArrayExample`, receives the array data from configuration.</span></span>

| <span data-ttu-id="5260e-606">`ArrayExamples.Entries` 인덱스</span><span class="sxs-lookup"><span data-stu-id="5260e-606">`ArrayExamples.Entries` Index</span></span> | <span data-ttu-id="5260e-607">`ArrayExamples.Entries` 값</span><span class="sxs-lookup"><span data-stu-id="5260e-607">`ArrayExamples.Entries` Value</span></span> |
| :---------------------------: | :---------------------------: |
| <span data-ttu-id="5260e-608">0</span><span class="sxs-lookup"><span data-stu-id="5260e-608">0</span></span>                             | <span data-ttu-id="5260e-609">value0</span><span class="sxs-lookup"><span data-stu-id="5260e-609">value0</span></span>                        |
| <span data-ttu-id="5260e-610">1</span><span class="sxs-lookup"><span data-stu-id="5260e-610">1</span></span>                             | <span data-ttu-id="5260e-611">value1</span><span class="sxs-lookup"><span data-stu-id="5260e-611">value1</span></span>                        |
| <span data-ttu-id="5260e-612">2</span><span class="sxs-lookup"><span data-stu-id="5260e-612">2</span></span>                             | <span data-ttu-id="5260e-613">value2</span><span class="sxs-lookup"><span data-stu-id="5260e-613">value2</span></span>                        |
| <span data-ttu-id="5260e-614">3</span><span class="sxs-lookup"><span data-stu-id="5260e-614">3</span></span>                             | <span data-ttu-id="5260e-615">value4</span><span class="sxs-lookup"><span data-stu-id="5260e-615">value4</span></span>                        |
| <span data-ttu-id="5260e-616">4</span><span class="sxs-lookup"><span data-stu-id="5260e-616">4</span></span>                             | <span data-ttu-id="5260e-617">value5</span><span class="sxs-lookup"><span data-stu-id="5260e-617">value5</span></span>                        |

<span data-ttu-id="5260e-618">바인딩된 개체의 인덱스 &num;3은 `array:4` 구성 키에 대한 구성 데이터와 `value4`의 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-618">Index &num;3 in the bound object holds the configuration data for the `array:4` configuration key and its value of `value4`.</span></span> <span data-ttu-id="5260e-619">배열이 포함된 구성 데이터를 바인딩할 때 구성 키의 배열 인덱스는 개체를 만들 때 구성 데이터를 반복하는 데에만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-619">When configuration data containing an array is bound, the array indices in the configuration keys are merely used to iterate the configuration data when creating the object.</span></span> <span data-ttu-id="5260e-620">구성 데이터에 null 값을 유지할 수 없으며, 구성 키의 배열에서 하나 이상의 인덱스를 건너뛰더라도 바인딩된 개체에 null 값 항목이 생성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-620">A null value can't be retained in configuration data, and a null-valued entry isn't created in a bound object when an array in configuration keys skip one or more indices.</span></span>

<span data-ttu-id="5260e-621">인덱스 &num;3에 대한 누락된 구성 항목은 `ArrayExamples` 인스턴스에 바인딩하기 전에 구성에서 올바른 키-값 쌍을 생성하는 모든 구성 공급자에서 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-621">The missing configuration item for index &num;3 can be supplied before binding to the `ArrayExamples` instance by any configuration provider that produces the correct key-value pair in configuration.</span></span> <span data-ttu-id="5260e-622">샘플에 누락된 키-값 쌍이 있는 추가 JSON 구성 공급자가 포함된 경우 `ArrayExamples.Entries`는 전체 구성 배열과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-622">If the sample included an additional JSON Configuration Provider with the missing key-value pair, the `ArrayExamples.Entries` matches the complete configuration array:</span></span>

<span data-ttu-id="5260e-623">*missing_value.json*:</span><span class="sxs-lookup"><span data-stu-id="5260e-623">*missing_value.json*:</span></span>

```json
{
  "array:entries:3": "value3"
}
```

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="5260e-624"><xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*>의 경우</span><span class="sxs-lookup"><span data-stu-id="5260e-624">In <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*>:</span></span>

```csharp
config.AddJsonFile("missing_value.json", optional: false, reloadOnChange: false);
```

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="5260e-625">`Startup` 생성자의 경우:</span><span class="sxs-lookup"><span data-stu-id="5260e-625">In the `Startup` constructor:</span></span>

```csharp
.AddJsonFile("missing_value.json", optional: false, reloadOnChange: false);
```

::: moniker-end

<span data-ttu-id="5260e-626">표에 표시된 키-값 쌍이 구성으로 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-626">The key-value pair shown in the table is loaded into configuration.</span></span>

| <span data-ttu-id="5260e-627">Key</span><span class="sxs-lookup"><span data-stu-id="5260e-627">Key</span></span>             | <span data-ttu-id="5260e-628">값</span><span class="sxs-lookup"><span data-stu-id="5260e-628">Value</span></span>  |
| :-------------: | :----: |
| <span data-ttu-id="5260e-629">array:entries:3</span><span class="sxs-lookup"><span data-stu-id="5260e-629">array:entries:3</span></span> | <span data-ttu-id="5260e-630">value3</span><span class="sxs-lookup"><span data-stu-id="5260e-630">value3</span></span> |

<span data-ttu-id="5260e-631">JSON 구성 공급자에 인덱스 &num;3에 대한 항목이 포함된 후 `ArrayExamples` 클래스 인스턴스를 바인딩하는 경우 `ArrayExamples.Entries` 배열에 이 값이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-631">If the `ArrayExamples` class instance is bound after the JSON Configuration Provider includes the entry for index &num;3, the `ArrayExamples.Entries` array includes the value.</span></span>

| <span data-ttu-id="5260e-632">`ArrayExamples.Entries` 인덱스</span><span class="sxs-lookup"><span data-stu-id="5260e-632">`ArrayExamples.Entries` Index</span></span> | <span data-ttu-id="5260e-633">`ArrayExamples.Entries` 값</span><span class="sxs-lookup"><span data-stu-id="5260e-633">`ArrayExamples.Entries` Value</span></span> |
| :---------------------------: | :---------------------------: |
| <span data-ttu-id="5260e-634">0</span><span class="sxs-lookup"><span data-stu-id="5260e-634">0</span></span>                             | <span data-ttu-id="5260e-635">value0</span><span class="sxs-lookup"><span data-stu-id="5260e-635">value0</span></span>                        |
| <span data-ttu-id="5260e-636">1</span><span class="sxs-lookup"><span data-stu-id="5260e-636">1</span></span>                             | <span data-ttu-id="5260e-637">value1</span><span class="sxs-lookup"><span data-stu-id="5260e-637">value1</span></span>                        |
| <span data-ttu-id="5260e-638">2</span><span class="sxs-lookup"><span data-stu-id="5260e-638">2</span></span>                             | <span data-ttu-id="5260e-639">value2</span><span class="sxs-lookup"><span data-stu-id="5260e-639">value2</span></span>                        |
| <span data-ttu-id="5260e-640">3</span><span class="sxs-lookup"><span data-stu-id="5260e-640">3</span></span>                             | <span data-ttu-id="5260e-641">value3</span><span class="sxs-lookup"><span data-stu-id="5260e-641">value3</span></span>                        |
| <span data-ttu-id="5260e-642">4</span><span class="sxs-lookup"><span data-stu-id="5260e-642">4</span></span>                             | <span data-ttu-id="5260e-643">value4</span><span class="sxs-lookup"><span data-stu-id="5260e-643">value4</span></span>                        |
| <span data-ttu-id="5260e-644">5</span><span class="sxs-lookup"><span data-stu-id="5260e-644">5</span></span>                             | <span data-ttu-id="5260e-645">value5</span><span class="sxs-lookup"><span data-stu-id="5260e-645">value5</span></span>                        |

<span data-ttu-id="5260e-646">**JSON 배열 처리**</span><span class="sxs-lookup"><span data-stu-id="5260e-646">**JSON array processing**</span></span>

<span data-ttu-id="5260e-647">JSON 파일에 배열이 포함된 경우 0부터 시작하는 섹션 인덱스를 사용하여 배열 요소에 대한 구성 키가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-647">If a JSON file contains an array, configuration keys are created for the array elements with a zero-based section index.</span></span> <span data-ttu-id="5260e-648">다음 구성 파일에서 `subsection`은 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-648">In the following configuration file, `subsection` is an array:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-json[](index/samples/2.x/ConfigurationSample/json_array.json)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-json[](index/samples/1.x/ConfigurationSample/json_array.json)]

::: moniker-end

<span data-ttu-id="5260e-649">JSON 구성 공급자는 구성 데이터를 다음 키-값 쌍으로 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-649">The JSON Configuration Provider reads the configuration data into the following key-value pairs:</span></span>

| <span data-ttu-id="5260e-650">Key</span><span class="sxs-lookup"><span data-stu-id="5260e-650">Key</span></span>                     | <span data-ttu-id="5260e-651">값</span><span class="sxs-lookup"><span data-stu-id="5260e-651">Value</span></span>  |
| ----------------------- | :----: |
| <span data-ttu-id="5260e-652">json_array:key</span><span class="sxs-lookup"><span data-stu-id="5260e-652">json_array:key</span></span>          | <span data-ttu-id="5260e-653">valueA</span><span class="sxs-lookup"><span data-stu-id="5260e-653">valueA</span></span> |
| <span data-ttu-id="5260e-654">json_array:subsection:0</span><span class="sxs-lookup"><span data-stu-id="5260e-654">json_array:subsection:0</span></span> | <span data-ttu-id="5260e-655">valueB</span><span class="sxs-lookup"><span data-stu-id="5260e-655">valueB</span></span> |
| <span data-ttu-id="5260e-656">json_array:subsection:1</span><span class="sxs-lookup"><span data-stu-id="5260e-656">json_array:subsection:1</span></span> | <span data-ttu-id="5260e-657">valueC</span><span class="sxs-lookup"><span data-stu-id="5260e-657">valueC</span></span> |
| <span data-ttu-id="5260e-658">json_array:subsection:2</span><span class="sxs-lookup"><span data-stu-id="5260e-658">json_array:subsection:2</span></span> | <span data-ttu-id="5260e-659">valueD</span><span class="sxs-lookup"><span data-stu-id="5260e-659">valueD</span></span> |

<span data-ttu-id="5260e-660">샘플 앱에서는 다음 POCO 클래스를 사용하여 구성 키-값 쌍을 바인딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-660">In the sample app, the following POCO class is available to bind the configuration key-value pairs:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/samples/2.x/ConfigurationSample/Models/JsonArrayExample.cs?name=snippet1)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/samples/1.x/ConfigurationSample/Models/JsonArrayExample.cs?name=snippet1)]

::: moniker-end

<span data-ttu-id="5260e-661">바인딩 후 `JsonArrayExample.Key`는 `valueA` 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-661">After binding, `JsonArrayExample.Key` holds the value `valueA`.</span></span> <span data-ttu-id="5260e-662">하위 섹션 값은 POCO 배열 속성 `Subsection`에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-662">The subsection values are stored in the POCO array property, `Subsection`.</span></span>

| <span data-ttu-id="5260e-663">`JsonArrayExample.Subsection` 인덱스</span><span class="sxs-lookup"><span data-stu-id="5260e-663">`JsonArrayExample.Subsection` Index</span></span> | <span data-ttu-id="5260e-664">`JsonArrayExample.Subsection` 값</span><span class="sxs-lookup"><span data-stu-id="5260e-664">`JsonArrayExample.Subsection` Value</span></span> |
| :---------------------------------: | :---------------------------------: |
| <span data-ttu-id="5260e-665">0</span><span class="sxs-lookup"><span data-stu-id="5260e-665">0</span></span>                                   | <span data-ttu-id="5260e-666">valueB</span><span class="sxs-lookup"><span data-stu-id="5260e-666">valueB</span></span>                              |
| <span data-ttu-id="5260e-667">1</span><span class="sxs-lookup"><span data-stu-id="5260e-667">1</span></span>                                   | <span data-ttu-id="5260e-668">valueC</span><span class="sxs-lookup"><span data-stu-id="5260e-668">valueC</span></span>                              |
| <span data-ttu-id="5260e-669">2</span><span class="sxs-lookup"><span data-stu-id="5260e-669">2</span></span>                                   | <span data-ttu-id="5260e-670">valueD</span><span class="sxs-lookup"><span data-stu-id="5260e-670">valueD</span></span>                              |

## <a name="custom-configuration-provider"></a><span data-ttu-id="5260e-671">사용자 지정 구성 공급자</span><span class="sxs-lookup"><span data-stu-id="5260e-671">Custom configuration provider</span></span>

<span data-ttu-id="5260e-672">샘플 앱에서는 [EF(Entity Framework)](/ef/core/)를 사용하여 데이터베이스에서 구성 키-값 쌍을 읽는 기본 구성 공급자를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-672">The sample app demonstrates how to create a basic configuration provider that reads configuration key-value pairs from a database using [Entity Framework (EF)](/ef/core/).</span></span>

<span data-ttu-id="5260e-673">이 공급자의 특징은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-673">The provider has the following characteristics:</span></span>

* <span data-ttu-id="5260e-674">데모용으로 EF 메모리 내 데이터베이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-674">The EF in-memory database is used for demonstration purposes.</span></span> <span data-ttu-id="5260e-675">연결 문자열이 필요한 데이터베이스를 사용하려면 보조 `ConfigurationBuilder`를 구현하여 다른 구성 공급자에서 연결 문자열을 제공하세요.</span><span class="sxs-lookup"><span data-stu-id="5260e-675">To use a database that requires a connection string, implement a secondary `ConfigurationBuilder` to supply the connection string from another configuration provider.</span></span>
* <span data-ttu-id="5260e-676">이 공급자는 시작 시 데이터베이스 테이블을 구성으로 읽어 들입니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-676">The provider reads a database table into configuration at startup.</span></span> <span data-ttu-id="5260e-677">이 공급자는 키별 기준으로 데이터베이스를 쿼리하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-677">The provider doesn't query the database on a per-key basis.</span></span>
* <span data-ttu-id="5260e-678">변경 시 다시 로드가 구현되지 않으므로 앱 시작 후 데이터베이스를 업데이트해도 앱 구성에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-678">Reload-on-change isn't implemented, so updating the database after the app starts has no effect on the app's configuration.</span></span>

<span data-ttu-id="5260e-679">데이터베이스에 구성 값을 저장하는 `EFConfigurationValue` 엔터티를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-679">Define an `EFConfigurationValue` entity for storing configuration values in the database.</span></span>

<span data-ttu-id="5260e-680">*Models/EFConfigurationValue.cs*:</span><span class="sxs-lookup"><span data-stu-id="5260e-680">*Models/EFConfigurationValue.cs*:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/samples/2.x/ConfigurationSample/Models/EFConfigurationValue.cs?name=snippet1)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/samples/1.x/ConfigurationSample/Models/EFConfigurationValue.cs?name=snippet1)]

::: moniker-end

<span data-ttu-id="5260e-681">구성된 값을 저장 및 액세스하는 `EFConfigurationContext`를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-681">Add an `EFConfigurationContext` to store and access the configured values.</span></span>

<span data-ttu-id="5260e-682">*EFConfigurationProvider/EFConfigurationContext.cs*:</span><span class="sxs-lookup"><span data-stu-id="5260e-682">*EFConfigurationProvider/EFConfigurationContext.cs*:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/samples/2.x/ConfigurationSample/EFConfigurationProvider/EFConfigurationContext.cs?name=snippet1)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/samples/1.x/ConfigurationSample/EFConfigurationProvider/EFConfigurationContext.cs?name=snippet1)]

::: moniker-end

<span data-ttu-id="5260e-683"><xref:Microsoft.Extensions.Configuration.IConfigurationSource>를 구현하는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-683">Create a class that implements <xref:Microsoft.Extensions.Configuration.IConfigurationSource>.</span></span>

<span data-ttu-id="5260e-684">*EFConfigurationProvider/EFConfigurationSource.cs*:</span><span class="sxs-lookup"><span data-stu-id="5260e-684">*EFConfigurationProvider/EFConfigurationSource.cs*:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/samples/2.x/ConfigurationSample/EFConfigurationProvider/EFConfigurationSource.cs?name=snippet1)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/samples/1.x/ConfigurationSample/EFConfigurationProvider/EFConfigurationSource.cs?name=snippet1)]

::: moniker-end

<span data-ttu-id="5260e-685"><xref:Microsoft.Extensions.Configuration.ConfigurationProvider>에서 상속하여 사용자 지정 구성 공급자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-685">Create the custom configuration provider by inheriting from <xref:Microsoft.Extensions.Configuration.ConfigurationProvider>.</span></span> <span data-ttu-id="5260e-686">구성 공급자는 비어 있는 데이터베이스를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-686">The configuration provider initializes the database when it's empty.</span></span>

<span data-ttu-id="5260e-687">*EFConfigurationProvider/EFConfigurationProvider.cs*:</span><span class="sxs-lookup"><span data-stu-id="5260e-687">*EFConfigurationProvider/EFConfigurationProvider.cs*:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/samples/2.x/ConfigurationSample/EFConfigurationProvider/EFConfigurationProvider.cs?name=snippet1)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/samples/1.x/ConfigurationSample/EFConfigurationProvider/EFConfigurationProvider.cs?name=snippet1)]

::: moniker-end

<span data-ttu-id="5260e-688">`AddEFConfiguration` 확장 메서드를 사용하여 구성 소스를 `ConfigurationBuilder`에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-688">An `AddEFConfiguration` extension method permits adding the configuration source to a `ConfigurationBuilder`.</span></span>

<span data-ttu-id="5260e-689">*Extensions/EntityFrameworkExtensions.cs*:</span><span class="sxs-lookup"><span data-stu-id="5260e-689">*Extensions/EntityFrameworkExtensions.cs*:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/samples/2.x/ConfigurationSample/Extensions/EntityFrameworkExtensions.cs?name=snippet1)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/samples/1.x/ConfigurationSample/Extensions/EntityFrameworkExtensions.cs?name=snippet1)]

::: moniker-end

<span data-ttu-id="5260e-690">다음 코드는 *Program.cs*에서 사용자 지정 `EFConfigurationProvider`를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-690">The following code shows how to use the custom `EFConfigurationProvider` in *Program.cs*:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/samples/2.x/ConfigurationSample/Program.cs?name=snippet_Program&highlight=26)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/samples/1.x/ConfigurationSample/Startup.cs?name=snippet_Startup&highlight=24)]

::: moniker-end

## <a name="access-configuration-during-startup"></a><span data-ttu-id="5260e-691">시작하는 동안 구성에 액세스</span><span class="sxs-lookup"><span data-stu-id="5260e-691">Access configuration during startup</span></span>

<span data-ttu-id="5260e-692">`Startup.ConfigureServices`의 구성 값에 액세스하려면 `IConfiguration`을 `Startup` 생성자에 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-692">Inject `IConfiguration` into the `Startup` constructor to access configuration values in `Startup.ConfigureServices`.</span></span> <span data-ttu-id="5260e-693">`Startup.Configure`의 구성에 액세스하려면 `IConfiguration`을 메서드에 직접 삽입하거나 생성자의 인스턴스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-693">To access configuration in `Startup.Configure`, either inject `IConfiguration` directly into the method or use the instance from the constructor:</span></span>

```csharp
public class Startup
{
    private readonly IConfiguration _config;

    public Startup(IConfiguration config)
    {
        _config = config;
    }

    public void ConfigureServices(IServiceCollection services)
    {
        var value = _config["key"];
    }

    public void Configure(IApplicationBuilder app, IConfiguration config)
    {
        var value = config["key"];
    }
}
```

<span data-ttu-id="5260e-694">시작 편의 메서드를 사용하여 구성에 액세스하는 방법의 예는 [앱 시작: 편의 메서드](xref:fundamentals/startup#convenience-methods)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5260e-694">For an example of accessing configuration using startup convenience methods, see [App startup: Convenience methods](xref:fundamentals/startup#convenience-methods).</span></span>

## <a name="access-configuration-in-a-razor-pages-page-or-mvc-view"></a><span data-ttu-id="5260e-695">Razor Pages 페이지 또는 MVC 뷰에서 구성에 액세스</span><span class="sxs-lookup"><span data-stu-id="5260e-695">Access configuration in a Razor Pages page or MVC view</span></span>

<span data-ttu-id="5260e-696">Razor Pages 페이지나 MVC 뷰에서 구성 설정에 액세스하려면 [Microsoft.Extensions.Configuration 네임스페이스](xref:Microsoft.Extensions.Configuration)에 [using 지시문](xref:mvc/views/razor#using)([C# 참조: using 지시문](/dotnet/csharp/language-reference/keywords/using-directive))을 추가하고 <xref:Microsoft.Extensions.Configuration.IConfiguration>을 페이지 또는 뷰로 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-696">To access configuration settings in a Razor Pages page or an MVC view, add a [using directive](xref:mvc/views/razor#using) ([C# reference: using directive](/dotnet/csharp/language-reference/keywords/using-directive)) for the [Microsoft.Extensions.Configuration namespace](xref:Microsoft.Extensions.Configuration) and inject <xref:Microsoft.Extensions.Configuration.IConfiguration> into the page or view.</span></span>

<span data-ttu-id="5260e-697">Razor 페이지에서:</span><span class="sxs-lookup"><span data-stu-id="5260e-697">In a Razor Pages page:</span></span>

```cshtml
@page
@model IndexModel
@using Microsoft.Extensions.Configuration
@inject IConfiguration Configuration

<!DOCTYPE html>
<html lang="en">
<head>
    <title>Index Page</title>
</head>
<body>
    <h1>Access configuration in a Razor Pages page</h1>
    <p>Configuration value for 'key': @Configuration["key"]</p>
</body>
</html>
```

<span data-ttu-id="5260e-698">MVC 뷰에서:</span><span class="sxs-lookup"><span data-stu-id="5260e-698">In an MVC view:</span></span>

```cshtml
@using Microsoft.Extensions.Configuration
@inject IConfiguration Configuration

<!DOCTYPE html>
<html lang="en">
<head>
    <title>Index View</title>
</head>
<body>
    <h1>Access configuration in an MVC view</h1>
    <p>Configuration value for 'key': @Configuration["key"]</p>
</body>
</html>
```

## <a name="add-configuration-from-an-external-assembly"></a><span data-ttu-id="5260e-699">외부 어셈블리의 구성 추가</span><span class="sxs-lookup"><span data-stu-id="5260e-699">Add configuration from an external assembly</span></span>

<span data-ttu-id="5260e-700"><xref:Microsoft.AspNetCore.Hosting.IHostingStartup>구현에서는 시작 시 앱의 `Startup` 클래스 외부에 있는 외부 어셈블리에서 앱에 향상된 기능을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5260e-700">An <xref:Microsoft.AspNetCore.Hosting.IHostingStartup> implementation allows adding enhancements to an app at startup from an external assembly outside of the app's `Startup` class.</span></span> <span data-ttu-id="5260e-701">자세한 내용은 <xref:fundamentals/configuration/platform-specific-configuration>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5260e-701">For more information, see <xref:fundamentals/configuration/platform-specific-configuration>.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5260e-702">추가 자료</span><span class="sxs-lookup"><span data-stu-id="5260e-702">Additional resources</span></span>

* <xref:fundamentals/configuration/options>
* <span data-ttu-id="5260e-703">[Deep Dive into Microsoft Configuration](https://www.paraesthesia.com/archive/2018/06/20/microsoft-extensions-configuration-deep-dive/)(Microsoft 구성 자세히 알아보기)</span><span class="sxs-lookup"><span data-stu-id="5260e-703">[Deep Dive into Microsoft Configuration](https://www.paraesthesia.com/archive/2018/06/20/microsoft-extensions-configuration-deep-dive/)</span></span>
