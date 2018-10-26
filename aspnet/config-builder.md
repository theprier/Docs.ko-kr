---
uid: config-builder
title: ASP.NET에 대 한 구성 작성기
author: rick-anderson
description: 외부 소스의 web.config 값 이외의 원본에서 구성 데이터를 가져오는 방법에 알아봅니다.
ms.author: riande
ms.date: 10/29/2018
ms.technology: aspnet
msc.type: content
ms.openlocfilehash: d5a3916c3df9778d14be80342bafbc3456a69a03
ms.sourcegitcommit: f2d14a7518d6ee51aca9333818ac1276e7b5ecef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50134537"
---
# <a name="configuration-builders-for-aspnet"></a><span data-ttu-id="48755-103">ASP.NET에 대 한 구성 작성기</span><span class="sxs-lookup"><span data-stu-id="48755-103">Configuration builders for ASP.NET</span></span>

<span data-ttu-id="48755-104">하 여 [Stephen Molloy](https://github.com/StephenMolloy) 고 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="48755-104">By [Stephen Molloy](https://github.com/StephenMolloy) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="48755-105">구성 작성기 외부 원본에서 구성 값을 가져오려면 ASP.NET 앱에 대 한 현대적이 고 민첩 한 메커니즘을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-105">Configuration builders provide a modern and agile mechanism for ASP.NET apps to get configuration values from external sources.</span></span>

<span data-ttu-id="48755-106">구성 작성기:</span><span class="sxs-lookup"><span data-stu-id="48755-106">Configuration builders:</span></span>

* <span data-ttu-id="48755-107">이상 및.NET Framework 4.7.1에서에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="48755-107">Are available in .NET Framework 4.7.1 and later.</span></span>
* <span data-ttu-id="48755-108">구성 값을 읽기 위한 유연한 메커니즘을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-108">Provide a flexible mechanism for reading configuration values.</span></span>
* <span data-ttu-id="48755-109">컨테이너로 이동 하 고 클라우드 포커스가 있는 환경 일부 앱의 기본 요구를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-109">Address some of the basic needs of apps as they move into a container and cloud focused environment.</span></span>
* <span data-ttu-id="48755-110">사용할 수 있습니다 (예: Azure Key Vault 및 환경 변수) 이전에 사용할 수 없는 원본의 그리는 방식으로 구성 데이터에 대 한 보호를 개선 하기 위해.NET 구성 시스템에서.</span><span class="sxs-lookup"><span data-stu-id="48755-110">Can be used to improve protection of configuration data by drawing from sources previously unavailable (for example, Azure Key Vault and environment variables) in the .NET configuration system.</span></span>

## <a name="keyvalue-configuration-builders"></a><span data-ttu-id="48755-111">키/값 구성 작성기</span><span class="sxs-lookup"><span data-stu-id="48755-111">Key/value configuration builders</span></span>

<span data-ttu-id="48755-112">구성 작성기에 의해 처리 될 수 있는 일반적인 시나리오는 키/값 패턴을 따르는 구성 섹션에 대 한 기본 키/값 대체 메커니즘을 제공 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="48755-112">A common scenario that can be handled by configuration builders is to provide a basic key/value replacement mechanism for configuration sections that follow a key/value pattern.</span></span> <span data-ttu-id="48755-113">.NET Framework에 대 한 개념이 ConfigurationBuilders 특정 구성 섹션 또는 패턴으로 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="48755-113">The .NET Framework concept of ConfigurationBuilders is not limited to specific configuration sections or patterns.</span></span> <span data-ttu-id="48755-114">그러나 구성 작성기에 많은 `Microsoft.Configuration.ConfigurationBuilders` ([github](https://github.com/aspnet/MicrosoftConfigurationBuilders)), [NuGet](https://www.nuget.org/packages?q=Microsoft.Configuration.ConfigurationBuilders) 키/쌍 패턴 내에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-114">However, many of the configuration builders in `Microsoft.Configuration.ConfigurationBuilders` ([github](https://github.com/aspnet/MicrosoftConfigurationBuilders)), [NuGet](https://www.nuget.org/packages?q=Microsoft.Configuration.ConfigurationBuilders) work within the key/value pattern.</span></span>

## <a name="keyvalue-configuration-builders-settings"></a><span data-ttu-id="48755-115">키/값 구성 작성기 설정</span><span class="sxs-lookup"><span data-stu-id="48755-115">Key/value configuration builders settings</span></span>

<span data-ttu-id="48755-116">다음 설정의 모든 키/값 구성 작성기를 적용할 `Microsoft.Configuration.ConfigurationBuilders`합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-116">The following settings apply to all key/value configuration builders in `Microsoft.Configuration.ConfigurationBuilders`.</span></span>

### <a name="mode"></a><span data-ttu-id="48755-117">모드</span><span class="sxs-lookup"><span data-stu-id="48755-117">Mode</span></span>

<span data-ttu-id="48755-118">키/값 정보가 외부 원본 구성 시스템의 선택 된 키/값 요소를 채우는 데 사용 하는 구성 작성기입니다.</span><span class="sxs-lookup"><span data-stu-id="48755-118">The configuration builders use an external source of key/value information to populate selected key/value elements of the configuration system.</span></span> <span data-ttu-id="48755-119">특히 합니다 `<appSettings/>` 고 `<connectionStrings/>` 섹션 구성 작성기에서 특별 한 처리를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-119">Specifically, the `<appSettings/>` and `<connectionStrings/>` sections receive special treatment from the configuration builders.</span></span> <span data-ttu-id="48755-120">작성기는 세 가지 모드로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-120">The builders work in three modes:</span></span>

* <span data-ttu-id="48755-121">`Strict` -기본 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="48755-121">`Strict` - The default mode.</span></span> <span data-ttu-id="48755-122">이 모드에서는 구성 작성기를 잘 알려진 키/값 중심 구성 섹션에 대해서만 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-122">In this mode, the configuration builder only operates on well-known key/value-centric configuration sections.</span></span> <span data-ttu-id="48755-123">`Strict` 모드 섹션에서 각 키를 열거합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-123">`Strict` mode enumerates each key in the section.</span></span> <span data-ttu-id="48755-124">일치 하는 키가 없으면 외부 원본:</span><span class="sxs-lookup"><span data-stu-id="48755-124">If a matching key is found in the external source:</span></span>

   * <span data-ttu-id="48755-125">구성 작성기는 외부 원본에서 값을 사용 하 여 결과 구성 섹션에서 값을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-125">The configuration builders replace the value in the resulting configuration section with the value from the external source.</span></span>
* <span data-ttu-id="48755-126">`Greedy` -이 모드는 밀접 한 관련이 `Strict` 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="48755-126">`Greedy` - This mode is closely related to `Strict` mode.</span></span> <span data-ttu-id="48755-127">대신 원래 구성에 이미 존재 하는 키를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-127">Rather than being limited to keys that already exist in the original configuration:</span></span>

  * <span data-ttu-id="48755-128">구성 작성기 결과 구성 섹션에는 외부 원본에서 모든 키/값 쌍을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-128">The configuration builders adds all key/value pairs from the external source into the resulting configuration section.</span></span>

* <span data-ttu-id="48755-129">`Expand` -구성 섹션 개체를 구문 분석 전에 원시 XML에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-129">`Expand` - Operates on the raw XML before it's parsed into a configuration section object.</span></span> <span data-ttu-id="48755-130">이 문자열에서 토큰의 확장으로 간주 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48755-130">It can be thought of as an expansion of tokens in a string.</span></span> <span data-ttu-id="48755-131">패턴과 일치 하는 원시 XML 문자열의 일부가 `${token}` 토큰 확장에 대 한 후보입니다.</span><span class="sxs-lookup"><span data-stu-id="48755-131">Any part of the raw XML string that matches the pattern `${token}` is a candidate for token expansion.</span></span> <span data-ttu-id="48755-132">해당 값이 없는 외부 소스에 없으면 토큰 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="48755-132">If no corresponding value is found in the external source, then the token is not changed.</span></span> <span data-ttu-id="48755-133">이 모드는 작성기에 제한 되지 않습니다.는 `<appSettings/>` 및 `<connectionStrings/>` 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="48755-133">Builders in this mode are not limited to the `<appSettings/>` and `<connectionStrings/>` sections.</span></span>

<span data-ttu-id="48755-134">다음과 같은 태그가 *web.config* 사용 하도록 설정 된 [EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/) 에서 `Strict` 모드:</span><span class="sxs-lookup"><span data-stu-id="48755-134">The following markup from *web.config* enables the [EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/) in `Strict` mode:</span></span>

[!code-xml[Main](config-builder/MyConfigBuilders/WebDefault.config?name=snippet)]

<span data-ttu-id="48755-135">다음 코드는 읽기를 `<appSettings/>` 하 고 `<connectionStrings/>` 앞의 *web.config* 파일:</span><span class="sxs-lookup"><span data-stu-id="48755-135">The following code reads the `<appSettings/>` and `<connectionStrings/>` shown in the preceding *web.config* file:</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/About.aspx.cs)]

<span data-ttu-id="48755-136">위의 코드 속성 값을 설정 하 고:</span><span class="sxs-lookup"><span data-stu-id="48755-136">The preceding code will set the property values to:</span></span>

* <span data-ttu-id="48755-137">값을 *web.config* 키 환경 변수에 설정 되어 있지 않으면 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="48755-137">The values in the *web.config* file if the keys are not set in environment variables.</span></span>
* <span data-ttu-id="48755-138">환경 값 경우 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-138">The values of the environment variable, if set.</span></span>

<span data-ttu-id="48755-139">예를 들어 `ServiceID` 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="48755-139">For example, `ServiceID` will contain:</span></span>

* <span data-ttu-id="48755-140">"ServiceID" value web.config의 경우 환경 변수 `ServiceID` 설정 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="48755-140">"ServiceID value from web.config", if the environment variable `ServiceID` is not set.</span></span>
* <span data-ttu-id="48755-141">값을 `ServiceID` 환경 변수인 경우 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-141">The value of the `ServiceID` environment variable, if set.</span></span>

<span data-ttu-id="48755-142">다음 이미지는 `<appSettings/>` 앞의 키/값 *web.config* 환경 편집기에서 파일 설정:</span><span class="sxs-lookup"><span data-stu-id="48755-142">The following image shows the `<appSettings/>` keys/values from the preceding *web.config* file set in the environment editor:</span></span>

![환경 편집기](config-builder/static/env.png)

<span data-ttu-id="48755-144">참고: 종료 하 고 환경 변수에서 변경 내용을 확인 하려면 Visual Studio를 다시 시작 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48755-144">Note: You might need to exit and restart Visual Studio to see changes in environment variables.</span></span>

### <a name="prefix-handling"></a><span data-ttu-id="48755-145">접두사 처리</span><span class="sxs-lookup"><span data-stu-id="48755-145">Prefix handling</span></span>

<span data-ttu-id="48755-146">때문에 키 접두사 설정 키를 간소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48755-146">Key prefixes can simplify setting keys because:</span></span>

* <span data-ttu-id="48755-147">.NET Framework 구성이 복잡 하 고 중첩 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="48755-147">The .NET Framework configuration is complex and nested.</span></span>
* <span data-ttu-id="48755-148">외부 키/값 소스는 일반적으로 기본 및 특성상 평면입니다.</span><span class="sxs-lookup"><span data-stu-id="48755-148">External key/value sources are commonly basic and flat by nature.</span></span> <span data-ttu-id="48755-149">예를 들어, 환경 변수 중첩 되지 않은 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-149">For example, environment variables are not nested.</span></span>

<span data-ttu-id="48755-150">다음 방법 중 하나를 사용 하 여 둘 다를 삽입할 `<appSettings/>` 고 `<connectionStrings/>` 환경 변수를 통해 구성에:</span><span class="sxs-lookup"><span data-stu-id="48755-150">Use any of the following approaches to inject both `<appSettings/>` and `<connectionStrings/>` into the configuration via environment variables:</span></span>

* <span data-ttu-id="48755-151">사용 하 여 합니다 `EnvironmentConfigBuilder` 기본에서 `Strict` 모드 및 구성 파일에서 적절 한 키 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="48755-151">With the `EnvironmentConfigBuilder` in the default `Strict` mode and the appropriate key names in the configuration file.</span></span> <span data-ttu-id="48755-152">이전 코드와 태그에서는이 접근 방식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-152">The preceding code and markup takes this approach.</span></span> <span data-ttu-id="48755-153">이렇게 할 수 있습니다 **되지** 키 모두에 동일 하 게 명명 된 `<appSettings/>` 및 `<connectionStrings/>`합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-153">Using this approach you can **not** have identically named keys in both `<appSettings/>` and `<connectionStrings/>`.</span></span>
* <span data-ttu-id="48755-154">사용 하 여 두 `EnvironmentConfigBuilder`에서 s `Greedy` 고유한 접두사를 사용 하 여 모드 및 `stripPrefix`.</span><span class="sxs-lookup"><span data-stu-id="48755-154">Use two `EnvironmentConfigBuilder`s in `Greedy` mode with distinct prefixes and `stripPrefix`.</span></span> <span data-ttu-id="48755-155">이 방법을 사용 하 여 앱 읽어보세요 `<appSettings/>` 및 `<connectionStrings/>` 구성 파일을 업데이트 하지 않고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-155">With this approach, the app can read `<appSettings/>` and `<connectionStrings/>` without needing to update the configuration file.</span></span> <span data-ttu-id="48755-156">다음 섹션인 [stripPrefix](#stripprefix),이 작업을 수행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="48755-156">The next section,  [stripPrefix](#stripprefix),  shows how to do this.</span></span>
* <span data-ttu-id="48755-157">사용 하 여 두 `EnvironmentConfigBuilder`의 `Greedy` 고유한 접두사를 사용 하 여 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="48755-157">Use two `EnvironmentConfigBuilder`s in `Greedy` mode with distinct prefixes.</span></span> <span data-ttu-id="48755-158">이 방법을 사용 하 여 키 이름을 접두사로 달라 야 하는 대로 중복 키 이름 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="48755-158">With this approach you can't have duplicate key names as key names must differ by prefix.</span></span>  <span data-ttu-id="48755-159">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="48755-159">For example:</span></span>

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefix.config?name=snippet&highlight=11-99)]

<span data-ttu-id="48755-160">위의 태그를 사용 하 여 동일한 기본 키/값 소스를 채우는 두 개의 서로 다른 섹션에 대 한 구성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48755-160">With the preceding markup, the same flat key/value source can be used to populate configuration for two different sections.</span></span>

<span data-ttu-id="48755-161">다음 이미지는 `<appSettings/>` 하 고 `<connectionStrings/>` 앞에서 키/값 *web.config* 환경 편집기에서 파일 설정:</span><span class="sxs-lookup"><span data-stu-id="48755-161">The following image shows the `<appSettings/>` and `<connectionStrings/>` keys/values from the preceding *web.config* file set in the environment editor:</span></span>

![환경 편집기](config-builder/static/prefix.png)

<span data-ttu-id="48755-163">다음 코드는 읽기를 `<appSettings/>` 하 고 `<connectionStrings/>` 앞에 포함 된 키/값 *web.config* 파일:</span><span class="sxs-lookup"><span data-stu-id="48755-163">The following code reads the `<appSettings/>` and `<connectionStrings/>` keys/values contained in the preceding *web.config* file:</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/Contact.aspx.cs?name=snippet)]

<span data-ttu-id="48755-164">위의 코드 속성 값을 설정 하 고:</span><span class="sxs-lookup"><span data-stu-id="48755-164">The preceding code will set the property values to:</span></span>

* <span data-ttu-id="48755-165">값을 *web.config* 키 환경 변수에 설정 되어 있지 않으면 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="48755-165">The values in the *web.config* file if the keys are not set in environment variables.</span></span>
* <span data-ttu-id="48755-166">환경 값 경우 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-166">The values of the environment variable, if set.</span></span>

<span data-ttu-id="48755-167">예를 들어 이전 사용 하 여 *web.config* 파일인 이전 환경 편집기 이미지를 이전 코드를 다음 값의 키/값 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="48755-167">For example, using the previous *web.config* file, the keys/values in the previous  environment editor image, and the previous code, the following values are set:</span></span>

|  <span data-ttu-id="48755-168">Key</span><span class="sxs-lookup"><span data-stu-id="48755-168">Key</span></span>              | <span data-ttu-id="48755-169">값</span><span class="sxs-lookup"><span data-stu-id="48755-169">Value</span></span> |
| ----------------- | ------------ |
|     <span data-ttu-id="48755-170">AppSetting_ServiceID</span><span class="sxs-lookup"><span data-stu-id="48755-170">AppSetting_ServiceID</span></span>           | <span data-ttu-id="48755-171">환경 변수에서 AppSetting_ServiceID</span><span class="sxs-lookup"><span data-stu-id="48755-171">AppSetting_ServiceID from env variables</span></span>|
|    <span data-ttu-id="48755-172">AppSetting_default</span><span class="sxs-lookup"><span data-stu-id="48755-172">AppSetting_default</span></span>            | <span data-ttu-id="48755-173">Env AppSetting_default 값</span><span class="sxs-lookup"><span data-stu-id="48755-173">AppSetting_default value from env</span></span> |
|       <span data-ttu-id="48755-174">ConnStr_default</span><span class="sxs-lookup"><span data-stu-id="48755-174">ConnStr_default</span></span>         | <span data-ttu-id="48755-175">Env에서 ConnStr_default val</span><span class="sxs-lookup"><span data-stu-id="48755-175">ConnStr_default val from env</span></span>|

### <a name="stripprefix"></a><span data-ttu-id="48755-176">stripPrefix</span><span class="sxs-lookup"><span data-stu-id="48755-176">stripPrefix</span></span>

<span data-ttu-id="48755-177">`stripPrefix`: 부울, 기본값은 `false`합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-177">`stripPrefix`: boolean, defaults to `false`.</span></span> 

<span data-ttu-id="48755-178">이전 XML 태그를 사용 하는 앱 설정에서 연결 문자열을 구분 하지만에서 모든 키가 필요 합니다 *web.config* 지정된 된 접두사를 사용 하는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="48755-178">The preceding XML markup separates app settings from connection strings but requires all the keys in the *web.config* file to use the specified prefix.</span></span> <span data-ttu-id="48755-179">예를 들어 접두사 `AppSetting` 에 추가 해야 합니다 `ServiceID` 키 ("AppSetting_ServiceID").</span><span class="sxs-lookup"><span data-stu-id="48755-179">For example, the prefix `AppSetting` must be added to the `ServiceID` key ("AppSetting_ServiceID").</span></span> <span data-ttu-id="48755-180">사용 하 여 `stripPrefix`, 접두사에서 사용 되지 않습니다 합니다 *web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="48755-180">With `stripPrefix`, the prefix is not used in the *web.config* file.</span></span> <span data-ttu-id="48755-181">구성 작성기 소스 (예를 들어, 환경에서.)에 붙여야 합니다. 대부분의 개발자가 사용 하는 것으로 예상 `stripPrefix`합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-181">The prefix is required in the configuration builder source (for example, in the environment.) We anticipate most developers will use `stripPrefix`.</span></span>

<span data-ttu-id="48755-182">응용 프로그램은 일반적으로 접두사를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-182">Applications typically strip off the prefix.</span></span> <span data-ttu-id="48755-183">다음 *web.config* 접두사를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-183">The following *web.config* strips the prefix:</span></span>

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefixStrip.config?name=snippet&highlight=14,19)]

<span data-ttu-id="48755-184">앞의 *web.config* 파일을 `default` 키가 둘 다에 `<appSettings/>` 및 `<connectionStrings/>`합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-184">In the preceding *web.config* file, the `default` key is in both the `<appSettings/>` and `<connectionStrings/>`.</span></span>

<span data-ttu-id="48755-185">다음 이미지는 `<appSettings/>` 하 고 `<connectionStrings/>` 앞에서 키/값 *web.config* 환경 편집기에서 파일 설정:</span><span class="sxs-lookup"><span data-stu-id="48755-185">The following image shows the `<appSettings/>` and `<connectionStrings/>` keys/values from the preceding *web.config* file set in the environment editor:</span></span>

![환경 편집기](config-builder/static/prefix.png)

<span data-ttu-id="48755-187">다음 코드는 읽기를 `<appSettings/>` 하 고 `<connectionStrings/>` 앞에 포함 된 키/값 *web.config* 파일:</span><span class="sxs-lookup"><span data-stu-id="48755-187">The following code reads the `<appSettings/>` and `<connectionStrings/>` keys/values contained in the preceding *web.config* file:</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/About2.aspx.cs?name=snippet)]

<span data-ttu-id="48755-188">위의 코드 속성 값을 설정 하 고:</span><span class="sxs-lookup"><span data-stu-id="48755-188">The preceding code will set the property values to:</span></span>

* <span data-ttu-id="48755-189">값을 *web.config* 키 환경 변수에 설정 되어 있지 않으면 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="48755-189">The values in the *web.config* file if the keys are not set in environment variables.</span></span>
* <span data-ttu-id="48755-190">환경 값 경우 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-190">The values of the environment variable, if set.</span></span>

<span data-ttu-id="48755-191">예를 들어 이전 사용 하 여 *web.config* 파일인 이전 환경 편집기 이미지를 이전 코드를 다음 값의 키/값 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="48755-191">For example, using the previous *web.config* file, the keys/values in the previous  environment editor image, and the previous code, the following values are set:</span></span>

|  <span data-ttu-id="48755-192">Key</span><span class="sxs-lookup"><span data-stu-id="48755-192">Key</span></span>              | <span data-ttu-id="48755-193">값</span><span class="sxs-lookup"><span data-stu-id="48755-193">Value</span></span> |
| ----------------- | ------------ |
|     <span data-ttu-id="48755-194">ServiceID</span><span class="sxs-lookup"><span data-stu-id="48755-194">ServiceID</span></span>           | <span data-ttu-id="48755-195">환경 변수에서 AppSetting_ServiceID</span><span class="sxs-lookup"><span data-stu-id="48755-195">AppSetting_ServiceID from env variables</span></span>|
|    <span data-ttu-id="48755-196">default</span><span class="sxs-lookup"><span data-stu-id="48755-196">default</span></span>            | <span data-ttu-id="48755-197">Env AppSetting_default 값</span><span class="sxs-lookup"><span data-stu-id="48755-197">AppSetting_default value from env</span></span> |
|    <span data-ttu-id="48755-198">default</span><span class="sxs-lookup"><span data-stu-id="48755-198">default</span></span>         | <span data-ttu-id="48755-199">Env에서 ConnStr_default val</span><span class="sxs-lookup"><span data-stu-id="48755-199">ConnStr_default val from env</span></span>|

### <a name="tokenpattern"></a><span data-ttu-id="48755-200">tokenPattern</span><span class="sxs-lookup"><span data-stu-id="48755-200">tokenPattern</span></span>

<span data-ttu-id="48755-201">`tokenPattern`: String, 기본값은 `@"\$\{(\w+)\}"`</span><span class="sxs-lookup"><span data-stu-id="48755-201">`tokenPattern`: String, defaults to `@"\$\{(\w+)\}"`</span></span>

<span data-ttu-id="48755-202">합니다 `Expand` 처럼 보이는 토큰에 대 한 원시 XML을 검색 하는 동작 작성기 중 `${token}`합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-202">The `Expand` behavior of the builders searches the raw XML for tokens that look like `${token}`.</span></span> <span data-ttu-id="48755-203">기본 정규식을 사용 하 여 수행 됩니다 검색 `@"\$\{(\w+)\}"`합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-203">Searching is done with the default regular expression `@"\$\{(\w+)\}"`.</span></span> <span data-ttu-id="48755-204">일치 하는 문자 집합이 `\w` XML과 많은 구성 소스 허용 보다 더 엄격 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-204">The set of characters that matches `\w` is more strict than XML and many configuration sources allow.</span></span> <span data-ttu-id="48755-205">사용 하 여 `tokenPattern` 때 보다 이상의 문자 `@"\$\{(\w+)\}"` 토큰 이름에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-205">Use `tokenPattern` when more characters than `@"\$\{(\w+)\}"` are required in the token name.</span></span>

<span data-ttu-id="48755-206">`tokenPattern`: 문자열:</span><span class="sxs-lookup"><span data-stu-id="48755-206">`tokenPattern`: String:</span></span>

* <span data-ttu-id="48755-207">개발자를 토큰 일치에 사용 되는 정규식을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48755-207">Allows developers to change the regex that is used for token matching.</span></span>
* <span data-ttu-id="48755-208">잘 구성 된, 위험한 regex 인지 유효성을 검사 하지 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="48755-208">No validation is done to make sure it is a well-formed, non-dangerous regex.</span></span>
* <span data-ttu-id="48755-209">캡처 그룹을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-209">It must contain a capture group.</span></span> <span data-ttu-id="48755-210">전체 정규식에는 전체 토큰을 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-210">The entire regex must match the entire token.</span></span> <span data-ttu-id="48755-211">첫 번째 캡처 구성 소스에서 찾을 토큰 이름 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-211">The first capture must be the token name to look up in the configuration source.</span></span>

## <a name="configuration-builders-in-microsoftconfigurationconfigurationbuilders"></a><span data-ttu-id="48755-212">구성 작성기 Microsoft.Configuration.ConfigurationBuilders에서</span><span class="sxs-lookup"><span data-stu-id="48755-212">Configuration builders in Microsoft.Configuration.ConfigurationBuilders</span></span>

### <a name="environmentconfigbuilder"></a><span data-ttu-id="48755-213">EnvironmentConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="48755-213">EnvironmentConfigBuilder</span></span>

```xml
<add name="Environment"
    [mode|prefix|stripPrefix|tokenPattern] 
    type="Microsoft.Configuration.ConfigurationBuilders.EnvironmentConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Environment" />
```

<span data-ttu-id="48755-214">합니다 [EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/):</span><span class="sxs-lookup"><span data-stu-id="48755-214">The [EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/):</span></span>

* <span data-ttu-id="48755-215">가장 구성 작성기의 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-215">Is the simplest of the configuration builders.</span></span>
* <span data-ttu-id="48755-216">환경에서 값을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="48755-216">Reads values from the environment.</span></span>
* <span data-ttu-id="48755-217">추가 구성 옵션이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="48755-217">Does not have any additional configuration options.</span></span>
* <span data-ttu-id="48755-218">`name` 특성 값은 임의입니다.</span><span class="sxs-lookup"><span data-stu-id="48755-218">The `name` attribute value is arbitrary.</span></span>

<span data-ttu-id="48755-219">**참고:** Windows 컨테이너 환경에서 런타임 시 설정 된 변수 EntryPoint 프로세스 환경에 삽입만 됩니다.</span><span class="sxs-lookup"><span data-stu-id="48755-219">**Note:** In a Windows container environment, variables set at run time are only injected into the EntryPoint process environment.</span></span> <span data-ttu-id="48755-220">서비스로 실행 되는 앱 또는 컨테이너의 메커니즘을 통해 삽입 된이 고, 그렇지 않으면 이러한 변수를 진입점이 아닌 프로세스를 선택 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="48755-220">Apps that run as a service or a non-EntryPoint process do not pick up these variables unless they are otherwise injected through a mechanism in the container.</span></span> <span data-ttu-id="48755-221">에 대 한 [IIS](https://github.com/Microsoft/iis-docker/pull/41)/[ASP.NET](https://github.com/Microsoft/aspnet-docker)-현재 버전의 컨테이너 기반 [ServiceMonitor.exe](https://github.com/Microsoft/iis-docker/pull/41) 이 처리 합니다 *DefaultAppPool* 만 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-221">For [IIS](https://github.com/Microsoft/iis-docker/pull/41)/[ASP.NET](https://github.com/Microsoft/aspnet-docker)-based containers, the current version of [ServiceMonitor.exe](https://github.com/Microsoft/iis-docker/pull/41) handles this in the *DefaultAppPool* only.</span></span> <span data-ttu-id="48755-222">다른 Windows 기반 컨테이너 변형 진입점이 아닌 프로세스에 대 한 자신의 주입 메커니즘을 개발 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-222">Other Windows-based container variants may need to develop their own injection mechanism for non-EntryPoint processes.</span></span>

### <a name="usersecretsconfigbuilder"></a><span data-ttu-id="48755-223">UserSecretsConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="48755-223">UserSecretsConfigBuilder</span></span>

> [!WARNING]
> <span data-ttu-id="48755-224">암호 저장, 중요 한 연결 문자열 또는 기타 중요 한 데이터 소스 코드에서 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="48755-224">Never store passwords, sensitive connection strings, or other sensitive data in source code.</span></span> <span data-ttu-id="48755-225">프로덕션 비밀을 사용 하지 않아야 개발 또는 테스트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-225">Production secrets should not be used for development or test.</span></span>

```xml
<add name="UserSecrets"
    [mode|prefix|stripPrefix|tokenPattern]
    (userSecretsId="{secret string, typically a GUID}" | userSecretsFile="~\secrets.file")
    [optional="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.UserSecretsConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.UserSecrets" />
```

<span data-ttu-id="48755-226">이 구성 작성기는 유사한 기능을 제공 [ASP.NET Core 암호 관리자](/aspnet/core/security/app-secrets)합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-226">This configuration builder provides a feature similar to [ASP.NET Core Secret Manager](/aspnet/core/security/app-secrets).</span></span>

<span data-ttu-id="48755-227">합니다 [UserSecretsConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.UserSecrets/) .NET Framework 프로젝트에서 사용할 수 있지만 암호 파일을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-227">The [UserSecretsConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.UserSecrets/) can be used in .NET Framework projects, but a secrets file must be specified.</span></span> <span data-ttu-id="48755-228">정의할 수 있습니다는 `UserSecretsId` 프로젝트의 속성이 파일을 읽기 위한 올바른 위치에 원시 비밀 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="48755-228">Alternatively, you can define the `UserSecretsId` property in the project file and create the raw secrets file in the correct location for reading.</span></span> <span data-ttu-id="48755-229">외부 프로젝트 종속성을 유지 하려면 비밀 파일에는 서식이 지정 된 XML입니다.</span><span class="sxs-lookup"><span data-stu-id="48755-229">To keep external dependencies out of your project, the secret file is XML formatted.</span></span> <span data-ttu-id="48755-230">XML 서식 지정는 구현 세부 정보 이며 형식 방법에 의존 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-230">The XML formatting is an implementation detail, and the format should not be relied upon.</span></span> <span data-ttu-id="48755-231">공유 하는 경우는 *secrets.json* .NET Core 프로젝트를 사용 하 여 파일을 사용 하는 것이 좋습니다는 [SimpleJsonConfigBuilder](#simplejsonconfig)합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-231">If you need to share a *secrets.json* file with .NET Core projects, consider using the [SimpleJsonConfigBuilder](#simplejsonconfig).</span></span> <span data-ttu-id="48755-232">`SimpleJsonConfigBuilder` .NET Core도 고려해 야 변경 될 수 있습니다 구현 세부 정보에 대 한 서식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-232">The `SimpleJsonConfigBuilder` format for .NET Core should also be considered an implementation detail subject to change.</span></span>

<span data-ttu-id="48755-233">구성에 대 한 특성 `UserSecretsConfigBuilder`:</span><span class="sxs-lookup"><span data-stu-id="48755-233">Configuration attributes for `UserSecretsConfigBuilder`:</span></span>

* <span data-ttu-id="48755-234">`userSecretsId` -이것이 XML 비밀 파일을 식별 하기 위한 기본 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="48755-234">`userSecretsId` - This is the preferred method for identifying an XML secrets file.</span></span> <span data-ttu-id="48755-235">.NET Core를 사용 하 여 비슷하게 작동을 `UserSecretsId` 프로젝트 속성을이 식별자를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-235">It works similar to .NET Core, which uses a `UserSecretsId` project property to store this identifier.</span></span> <span data-ttu-id="48755-236">문자열은 고유 해야 합니다., GUID 여야 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="48755-236">The string must be unique, it doesn't need to be a GUID.</span></span> <span data-ttu-id="48755-237">이 특성을 사용 합니다 `UserSecretsConfigBuilder` 잘 알려진 로컬 위치에서 (`%APPDATA%\Microsoft\UserSecrets\<UserSecrets Id>\secrets.xml`)이이 식별자에 속하는 비밀 파일에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-237">With this attribute, the `UserSecretsConfigBuilder` look in a well-known local location (`%APPDATA%\Microsoft\UserSecrets\<UserSecrets Id>\secrets.xml`) for a secrets file belonging to this identifier.</span></span>
* <span data-ttu-id="48755-238">`userSecretsFile` 암호를 포함 하는 파일 지정-선택적 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="48755-238">`userSecretsFile` - An optional attribute specifying the file containing the secrets.</span></span> <span data-ttu-id="48755-239">`~` 응용 프로그램 루트를 참조 하는 시작 시 문자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48755-239">The `~` character can be used at the start to reference the application root.</span></span> <span data-ttu-id="48755-240">이 특성 중 하나 또는 `userSecretsId` 특성이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-240">Either this attribute or the `userSecretsId` attribute is required.</span></span> <span data-ttu-id="48755-241">둘 다 지정 `userSecretsFile` 우선적으로 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-241">If both are specified, `userSecretsFile` takes precedence.</span></span>
* <span data-ttu-id="48755-242">`optional`: 부울 기본값 `true` -비밀 파일을 찾을 수 없는 경우 예외를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-242">`optional`: boolean, default value `true` - Prevents an exception if the secrets file cannot be found.</span></span> 
* <span data-ttu-id="48755-243">`name` 특성 값은 임의입니다.</span><span class="sxs-lookup"><span data-stu-id="48755-243">The `name` attribute value is arbitrary.</span></span>

<span data-ttu-id="48755-244">비밀 파일을 다음 형식으로 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48755-244">The secrets file has the following format:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<root>
  <secrets ver="1.0">
    <secret name="secret key name" value="secret value" />
  </secrets>
</root>
```

### <a name="azurekeyvaultconfigbuilder"></a><span data-ttu-id="48755-245">AzureKeyVaultConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="48755-245">AzureKeyVaultConfigBuilder</span></span>

```xml
<add name="AzureKeyVault"
    [mode|prefix|stripPrefix|tokenPattern]
    (vaultName="MyVaultName" |
     uri="https:/MyVaultName.vault.azure.net")
    [connectionString="connection string"]
    [version="secrets version"]
    [preloadSecretNames="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.AzureKeyVaultConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Azure" />
```

<span data-ttu-id="48755-246">합니다 [AzureKeyVaultConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Azure/) 에 저장 된 값을 읽고 합니다 [Azure Key Vault](/azure/key-vault/key-vault-whatis)합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-246">The [AzureKeyVaultConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Azure/) reads values stored in the [Azure Key Vault](/azure/key-vault/key-vault-whatis).</span></span>

<span data-ttu-id="48755-247">`vaultName` (자격 증명 모음의 이름) 또는 자격 증명 모음 URI 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-247">`vaultName` is required (either the name of the vault or a URI to the vault).</span></span> <span data-ttu-id="48755-248">다른 특성에 연결할 자격 증명 모음에 대 한 제어를 허용 하지만 응용 프로그램을 사용 하는 환경에서 실행 하지 않는 경우에 필요는 `Microsoft.Azure.Services.AppAuthentication`합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-248">The other attributes allow control about which vault to connect to, but are only necessary if the application is not running in an environment that works with `Microsoft.Azure.Services.AppAuthentication`.</span></span> <span data-ttu-id="48755-249">Azure 서비스 인증 라이브러리가 자동으로 실행 환경에서 연결 정보를 가능 하면 선택 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="48755-249">The Azure Services Authentication library is used to automatically pick up connection information from the execution environment if possible.</span></span> <span data-ttu-id="48755-250">자동으로 재정의할 수 있습니다 연결 정보의 연결 문자열을 제공 하 여 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-250">You can override automatically pick up of connection information by providing a connection string.</span></span>

* <span data-ttu-id="48755-251">`vaultName` -필요한 경우 `uri` 에서 제공 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="48755-251">`vaultName` - Required if `uri` in not provided.</span></span> <span data-ttu-id="48755-252">키/값 쌍을 읽어 올 Azure 구독에서 자격 증명 모음의 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-252">Specifies the name of the vault in your Azure subscription from which to read key/value pairs.</span></span>
* <span data-ttu-id="48755-253">`connectionString` 사용할 연결 문자열- [AzureServiceTokenProvider](https://docs.microsoft.com/en-us/azure/key-vault/service-to-service-authentication#connection-string-support)</span><span class="sxs-lookup"><span data-stu-id="48755-253">`connectionString` - A connection string usable by [AzureServiceTokenProvider](https://docs.microsoft.com/en-us/azure/key-vault/service-to-service-authentication#connection-string-support)</span></span>
* <span data-ttu-id="48755-254">`uri` -지정 된 다른 Key Vault 공급자에 연결 합니다. `uri` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="48755-254">`uri` - Connects to other Key Vault providers with the specified `uri` value.</span></span> <span data-ttu-id="48755-255">지정 하지 않으면 Azure (`vaultName`) 자격 증명 모음 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="48755-255">If not specified, Azure (`vaultName`) is the vault provider.</span></span>
* <span data-ttu-id="48755-256">`version` -Azure Key Vault 비밀에 대 한 버전 관리 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-256">`version` - Azure Key Vault provides a versioning feature for secrets.</span></span> <span data-ttu-id="48755-257">경우 `version` 를 지정 하면 작성기만이 버전을 일치 하는 비밀을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-257">If `version` is specified, the builder only retrieves secrets matching this version.</span></span>
* <span data-ttu-id="48755-258">`preloadSecretNames` -기본적으로이 작성기 쿼리 **모든** 초기화 될 때 키를 key vault의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="48755-258">`preloadSecretNames` - By default, this builder querys **all** key names in the key vault when it is initialized.</span></span> <span data-ttu-id="48755-259">모든 키 값 읽기를 방지 하려면이 특성을 설정 `false`합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-259">To prevent reading all key values, set this attribute to `false`.</span></span> <span data-ttu-id="48755-260">이 값을 설정 `false` 한 번에 한 암호를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="48755-260">Setting this to `false` reads secrets one at a time.</span></span> <span data-ttu-id="48755-261">한 번에 하나씩 유용할 수 있습니다 자격 증명 모음 "Get" 액세스를 허용 하지만 하지 "목록"에 액세스 하는 경우 비밀을 읽는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="48755-261">Reading secrets one at a time can useful if the vault allows "Get" access but not "List" access.</span></span> <span data-ttu-id="48755-262">**참고:** 사용 하는 경우 `Greedy` 모드 `preloadSecretNames` 있어야 `true` (기본값입니다.)</span><span class="sxs-lookup"><span data-stu-id="48755-262">**Note:** When using `Greedy` mode, `preloadSecretNames` must be `true` (the default.)</span></span>

### <a name="keyperfileconfigbuilder"></a><span data-ttu-id="48755-263">KeyPerFileConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="48755-263">KeyPerFileConfigBuilder</span></span>

```xml
<add name="KeyPerFile"
    [mode|prefix|stripPrefix|tokenPattern]
    (directoryPath="PathToSourceDirectory")
    [ignorePrefix="ignore."]
    [keyDelimiter=":"]
    [optional="false"]
    type="Microsoft.Configuration.ConfigurationBuilders.KeyPerFileConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.KeyPerFile" />
```

<span data-ttu-id="48755-264">[KeyPerFileConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.KeyPerFile/) 값의 원본으로 디렉터리의 파일을 사용 하는 기본 구성 작성기를 됩니다.</span><span class="sxs-lookup"><span data-stu-id="48755-264">[KeyPerFileConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.KeyPerFile/) is a basic configuration builder that uses a directory's files as a source of values.</span></span> <span data-ttu-id="48755-265">파일의 이름을 키가 고 내용이 값입니다.</span><span class="sxs-lookup"><span data-stu-id="48755-265">A file's name is the key, and the contents are the value.</span></span> <span data-ttu-id="48755-266">이 구성 작성기 오케스트레이션된 컨테이너 환경에서 실행 하는 경우 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48755-266">This configuration builder can be useful when running in an orchestrated container environment.</span></span> <span data-ttu-id="48755-267">Docker Swarm 및 Kubernetes를 제공 하는 같은 시스템 `secrets` 해당 오케스트레이션된 windows 컨테이너로이 키 파일 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="48755-267">Systems like Docker Swarm and Kubernetes provide `secrets` to their orchestrated windows containers in this key-per-file manner.</span></span>

<span data-ttu-id="48755-268">특성 세부 정보:</span><span class="sxs-lookup"><span data-stu-id="48755-268">Attribute details:</span></span>

* <span data-ttu-id="48755-269">`directoryPath` - 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="48755-269">`directoryPath` - Required.</span></span> <span data-ttu-id="48755-270">값에 대 한 확인에 대 한 경로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-270">Specifies a path to look in for values.</span></span> <span data-ttu-id="48755-271">암호에 저장 되는 Windows 용 docker를 *C:\ProgramData\Docker\secrets* 기본적으로 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="48755-271">Docker for Windows secrets are stored in the *C:\ProgramData\Docker\secrets* directory by default.</span></span>
* <span data-ttu-id="48755-272">`ignorePrefix` -이 접두사로 시작 하는 파일 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="48755-272">`ignorePrefix` - Files that start with this prefix are excluded.</span></span> <span data-ttu-id="48755-273">기본값은 "무시 합니다."입니다.</span><span class="sxs-lookup"><span data-stu-id="48755-273">Defaults to "ignore.".</span></span>
* <span data-ttu-id="48755-274">`keyDelimiter` -기본값은 `null`합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-274">`keyDelimiter` - Default value is `null`.</span></span> <span data-ttu-id="48755-275">를 지정 하는 경우 구성 작성기를 트래버스 디렉터리의 여러 수준을 구분이 기호와 함께 키 이름을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-275">If specified, the configuration builder traverses multiple levels of the directory, building up key names with this delimiter.</span></span> <span data-ttu-id="48755-276">이 값이 `null`, 디렉터리의 최상위 수준에서 구성 작성기를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-276">If this value is `null`, the configuration builder only looks at the top level of the directory.</span></span>
* <span data-ttu-id="48755-277">`optional` -기본값은 `false`합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-277">`optional` -  Default value is `false`.</span></span> <span data-ttu-id="48755-278">소스 디렉터리가 없는 경우 구성 작성기에서 오류가 발생 해야 하는지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-278">Specifies whether the configuration builder should cause errors if the source directory doesn't exist.</span></span>

### <a name="simplejsonconfigbuilder"></a><span data-ttu-id="48755-279">SimpleJsonConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="48755-279">SimpleJsonConfigBuilder</span></span>

> [!WARNING]
> <span data-ttu-id="48755-280">암호 저장, 중요 한 연결 문자열 또는 기타 중요 한 데이터 소스 코드에서 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="48755-280">Never store passwords, sensitive connection strings, or other sensitive data in source code.</span></span> <span data-ttu-id="48755-281">프로덕션 비밀을 사용 하지 않아야 개발 또는 테스트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-281">Production secrets should not be used for development or test.</span></span>

```xml
<add name="SimpleJson"
    [mode|prefix|stripPrefix|tokenPattern]
    jsonFile="~\config.json"
    [optional="true"]
    [jsonMode="(Flat|Sectional)"]
    type="Microsoft.Configuration.ConfigurationBuilders.SimpleJsonConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Json" />
```

<span data-ttu-id="48755-282">.NET core 프로젝트는 자주 구성에 대 한 JSON 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-282">.NET Core projects frequently use JSON files for configuration.</span></span> <span data-ttu-id="48755-283">합니다 [SimpleJsonConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Json/) .NET Framework에서 사용할.NET Core JSON 파일을 허용 하는 작성기입니다.</span><span class="sxs-lookup"><span data-stu-id="48755-283">The [SimpleJsonConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Json/) builder allows .NET Core JSON files to be used in the .NET Framework.</span></span> <span data-ttu-id="48755-284">이 구성 작성기는.NET Framework 구성의 특정 키/값 영역에 기본 키/값 원본에서 기본 매핑을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-284">This configuration builder is provides a basic mapping from a flat key/value source into specific key/value areas of .NET Framework configuration.</span></span> <span data-ttu-id="48755-285">이 구성 작성기 않습니다 **되지** 계층적 구성에 대 한 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-285">This configuration builder does **not** provide for hierarchical configurations.</span></span> <span data-ttu-id="48755-286">JSON 지원 파일을 사전에 복잡 한 계층적 개체가 아니라는 것과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-286">The JSON backing file is similar to a dictionary, not a complex hierarchical object.</span></span> <span data-ttu-id="48755-287">여러 수준의 계층적 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48755-287">A multi-level hierarchical file can be used.</span></span> <span data-ttu-id="48755-288">이 공급자 `flatten`s 각 수준을 사용 하 여 속성 이름을 추가 하 여 깊이 `:` 를 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-288">This provider `flatten`s the depth by appending the property name at each level using `:` as a delimiter.</span></span>

<span data-ttu-id="48755-289">특성 세부 정보:</span><span class="sxs-lookup"><span data-stu-id="48755-289">Attribute details:</span></span>

* <span data-ttu-id="48755-290">`jsonFile` - 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="48755-290">`jsonFile` - Required.</span></span> <span data-ttu-id="48755-291">JSON 파일을 읽어올 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-291">Specifies the JSON file to read from.</span></span> <span data-ttu-id="48755-292">`~` 앱 루트를 참조 하는 시작 시 문자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48755-292">The `~` character can be used at the start to reference the app root.</span></span>
* <span data-ttu-id="48755-293">`optional` -부울, 기본값은 `true`합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-293">`optional` - Boolean,  default value is `true`.</span></span> <span data-ttu-id="48755-294">방지 JSON 파일을 찾을 수 없는 경우 예외를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-294">Prevents throwing exceptions if the JSON file cannot be found.</span></span>
* <span data-ttu-id="48755-295">`jsonMode` - `[Flat|Sectional]`.</span><span class="sxs-lookup"><span data-stu-id="48755-295">`jsonMode` - `[Flat|Sectional]`.</span></span> <span data-ttu-id="48755-296">기본값은 `Flat`입니다.</span><span class="sxs-lookup"><span data-stu-id="48755-296">`Flat` is the default.</span></span> <span data-ttu-id="48755-297">때 `jsonMode` 는 `Flat`, JSON 파일을 단일 플랫 키/값 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="48755-297">When `jsonMode` is `Flat`, the JSON file is a single flat key/value source.</span></span> <span data-ttu-id="48755-298">합니다 `EnvironmentConfigBuilder` 및 `AzureKeyVaultConfigBuilder` 단일 플랫 키/값 소스 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-298">The `EnvironmentConfigBuilder` and `AzureKeyVaultConfigBuilder` are also single flat key/value sources.</span></span> <span data-ttu-id="48755-299">경우는 `SimpleJsonConfigBuilder` 에 구성 된 `Sectional` 모드:</span><span class="sxs-lookup"><span data-stu-id="48755-299">When the `SimpleJsonConfigBuilder` is configured in `Sectional` mode:</span></span>

  * <span data-ttu-id="48755-300">JSON 파일을 여러 사전에 최상위 수준에 개념적으로 구분 됩니다.</span><span class="sxs-lookup"><span data-stu-id="48755-300">The JSON file is conceptually divided just at the top level into multiple dictionaries.</span></span>
  * <span data-ttu-id="48755-301">각 사전에 연결 된 최상위 속성 이름과 일치 하는 구성 섹션에만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="48755-301">Each of the dictionaries is only applied to the configuration section that matches the top-level property name attached to them.</span></span> <span data-ttu-id="48755-302">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="48755-302">For example:</span></span>

```json
    {
        "appSettings" : {
            "setting1" : "value1",
            "setting2" : "value2",
            "complex" : {
                "setting1" : "complex:value1",
                "setting2" : "complex:value2",
            }
        }
    }
```

## <a name="implementing-a-custom-keyvalue-configuration-builder"></a><span data-ttu-id="48755-303">사용자 지정 키/값 구성 작성기 구현</span><span class="sxs-lookup"><span data-stu-id="48755-303">Implementing a custom key/value configuration builder</span></span>

<span data-ttu-id="48755-304">구성 작성기에는 요구 사항을 충족 하지 않습니다, 경우에 사용자 지정을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48755-304">If the configuration builders don't meet your needs, you can write a custom one.</span></span> <span data-ttu-id="48755-305">`KeyValueConfigBuilder` 대체 모드 및 대부분의 접두사 문제를 처리 하는 기본 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="48755-305">The `KeyValueConfigBuilder` base class handles substitution modes and most prefix concerns.</span></span> <span data-ttu-id="48755-306">구현 하는 프로젝트만 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="48755-306">An implementing project need only:</span></span>

* <span data-ttu-id="48755-307">기본 클래스에서 상속 되며 통해 키/값 쌍의 기본 소스를 구현 합니다 `GetValue` 고 `GetAllValues`:</span><span class="sxs-lookup"><span data-stu-id="48755-307">Inherit from the base class and implement a basic source of key/value pairs through the `GetValue` and `GetAllValues`:</span></span>
* <span data-ttu-id="48755-308">추가 된 [Microsoft.Configuration.ConfigurationBuilders.Base](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Base/) 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="48755-308">Add the [Microsoft.Configuration.ConfigurationBuilders.Base](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Base/) to the project.</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/MyCustomConfigBuilder.cs)]

<span data-ttu-id="48755-309">`KeyValueConfigBuilder` 기본 클래스는 많이 제공 및 일관 된 동작 키/값에서 구성 작성기입니다.</span><span class="sxs-lookup"><span data-stu-id="48755-309">The `KeyValueConfigBuilder` base class provides much of the work and consistent behavior across key/value configuration builders.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="48755-310">추가 자료</span><span class="sxs-lookup"><span data-stu-id="48755-310">Additional resources</span></span>

* [<span data-ttu-id="48755-311">구성 작성기 GitHub 리포지토리</span><span class="sxs-lookup"><span data-stu-id="48755-311">Configuration Builders GitHub repository</span></span>](https://github.com/aspnet/MicrosoftConfigurationBuilders)
* [<span data-ttu-id="48755-312">.NET을 사용 하 여 Azure Key Vault에 서비스 간 인증</span><span class="sxs-lookup"><span data-stu-id="48755-312">Service-to-service authentication to Azure Key Vault using .NET</span></span>](/azure/key-vault/service-to-service-authentication#connection-string-support)
