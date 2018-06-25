---
title: ASP.NET Core의 Environment 태그 도우미
author: pkellner
description: 모든 속성을 포함하여 정의된 ASP.NET Core Environment 태그 도우미
ms.author: riande
ms.date: 07/14/2017
uid: mvc/views/tag-helpers/builtin-th/environment-tag-helper
ms.openlocfilehash: 05c07b06a4fedac0b0ff39d168807f5e2e6996cf
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36276918"
---
# <a name="environment-tag-helper-in-aspnet-core"></a><span data-ttu-id="44e28-103">ASP.NET Core의 Environment 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="44e28-103">Environment Tag Helper in ASP.NET Core</span></span>

<span data-ttu-id="44e28-104">작성자: [Peter Kellner](http://peterkellner.net) 및 [Hisham Bin Ateya](https://twitter.com/hishambinateya)</span><span class="sxs-lookup"><span data-stu-id="44e28-104">By [Peter Kellner](http://peterkellner.net) and [Hisham Bin Ateya](https://twitter.com/hishambinateya)</span></span>

<span data-ttu-id="44e28-105">Environment 태그 도우미는 현재 호스팅 환경에 기반하여 포함된 콘텐츠를 조건부로 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="44e28-105">The Environment Tag Helper conditionally renders its enclosed content based on the current hosting environment.</span></span> <span data-ttu-id="44e28-106">유일한 특성인 `names`는 쉼표로 구분된 환경 이름의 목록으로 현재 환경과 일치하는 항목이 존재할 경우 포함된 콘텐츠가 렌더링되도록 트리거합니다.
</span><span class="sxs-lookup"><span data-stu-id="44e28-106">Its single attribute `names` is a comma separated list of environment names, that if any match to the current environment, will trigger the enclosed content to be rendered.</span></span>

## <a name="environment-tag-helper-attributes"></a><span data-ttu-id="44e28-107">Environment 태그 도우미의 특성</span><span class="sxs-lookup"><span data-stu-id="44e28-107">Environment Tag Helper Attributes</span></span>

### <a name="names"></a><span data-ttu-id="44e28-108">names</span><span class="sxs-lookup"><span data-stu-id="44e28-108">names</span></span>

<span data-ttu-id="44e28-109">포함된 콘텐츠를 렌더링하도록 트리거하는 단일 호스팅 환경 이름 또는 쉼표로 구분된 호스팅 환경 이름의 목록을 지정할 수 있습니다.
</span><span class="sxs-lookup"><span data-stu-id="44e28-109">Accepts a single hosting environment name or a comma-separated list of hosting environment names that trigger the rendering of the enclosed content.</span></span>

<span data-ttu-id="44e28-110">이러한 값은 ASP.NET Core의 정적 속성인 `HostingEnvironment.EnvironmentName`에서 반환된 현재 값과 비교됩니다.</span><span class="sxs-lookup"><span data-stu-id="44e28-110">These value(s) are compared to the current value returned from the ASP.NET Core static property `HostingEnvironment.EnvironmentName`.</span></span>  <span data-ttu-id="44e28-111">이 값은 **Staging**, **Development** 또는 **Production** 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="44e28-111">This value is one of the following: **Staging**; **Development** or **Production**.</span></span> <span data-ttu-id="44e28-112">이 비교에서 대/소문자는 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="44e28-112">The comparison ignores case.</span></span>

<span data-ttu-id="44e28-113">유효한 `environment` 태그 도우미의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="44e28-113">An example of a valid `environment` tag helper is:</span></span>

```cshtml
<environment names="Staging,Production">
  <strong>HostingEnvironment.EnvironmentName is Staging or Production</strong>
</environment>
```

## <a name="include-and-exclude-attributes"></a><span data-ttu-id="44e28-114">include 및 exclude 특성</span><span class="sxs-lookup"><span data-stu-id="44e28-114">include and exclude attributes</span></span>

<span data-ttu-id="44e28-115">ASP.NET Core 2.x에는 `include` & `exclude` 특성이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="44e28-115">ASP.NET Core 2.x adds the `include` & `exclude` attributes.</span></span> <span data-ttu-id="44e28-116">이러한 특성은 포함되거나 제외된 호스팅 환경 이름을 기반으로 포함된 콘텐츠의 렌더링 작업을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="44e28-116">These attributes control rendering the enclosed content based on the included or excluded hosting environment names.</span></span>

### <a name="include-aspnet-core-20-and-later"></a><span data-ttu-id="44e28-117">include (ASP.NET Core 2.0 이상)</span><span class="sxs-lookup"><span data-stu-id="44e28-117">include ASP.NET Core 2.0 and later</span></span>

<span data-ttu-id="44e28-118">`include` 속성은 ASP.NET Core 1.0의 `names` 특성과 비슷하게 동작합니다.</span><span class="sxs-lookup"><span data-stu-id="44e28-118">The `include` property has a similar behavior of the `names` attribute in ASP.NET Core 1.0.</span></span>

```cshtml
<environment include="Staging,Production">
  <strong>HostingEnvironment.EnvironmentName is Staging or Production</strong>
</environment>
```

### <a name="exclude-aspnet-core-20-and-later"></a><span data-ttu-id="44e28-119">exclude (ASP.NET Core 2.0 이상)</span><span class="sxs-lookup"><span data-stu-id="44e28-119">exclude ASP.NET Core 2.0 and later</span></span>

<span data-ttu-id="44e28-120">반면 `exclude` 속성을 사용하면 지정한 호스팅 환경 이름을 제외한 모든 호스팅 환경 이름에 대해 `EnvironmentTagHelper`가 포함된 콘텐츠를 렌더링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44e28-120">In contrast, the `exclude` property lets the `EnvironmentTagHelper` render the enclosed content for all hosting environment names except the one(s) that you specified.</span></span>

```cshtml
<environment exclude="Development">
  <strong>HostingEnvironment.EnvironmentName is Staging or Production</strong>
</environment>
```

## <a name="additional-resources"></a><span data-ttu-id="44e28-121">추가 자료</span><span class="sxs-lookup"><span data-stu-id="44e28-121">Additional resources</span></span>

* <xref:fundamentals/environments>
* <xref:fundamentals/dependency-injection#service-lifetimes-and-registration-options>
