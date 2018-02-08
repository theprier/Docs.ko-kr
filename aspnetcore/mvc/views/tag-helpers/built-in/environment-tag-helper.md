---
title: "ASP.NET Core의 환경 태그 도우미"
author: pkellner
description: "모든 속성을 비롯하여 정의된 ASP.NET Core 환경 태그 도우미"
manager: wpickett
ms.author: riande
ms.date: 07/14/2017
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: mvc/views/tag-helpers/builtin-th/environment-tag-helper
ms.openlocfilehash: 7a99ee0e59c7f49a3208d2c86c11cabce4294889
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="environment-tag-helper-in-aspnet-core"></a><span data-ttu-id="c125f-103">ASP.NET Core의 환경 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="c125f-103">Environment Tag Helper in ASP.NET Core</span></span>

<span data-ttu-id="c125f-104">작성자: [Peter Kellner](http://peterkellner.net) 및 [Hisham Bin Ateya](https://twitter.com/hishambinateya)</span><span class="sxs-lookup"><span data-stu-id="c125f-104">By [Peter Kellner](http://peterkellner.net) and [Hisham Bin Ateya](https://twitter.com/hishambinateya)</span></span>

<span data-ttu-id="c125f-105">환경 태그 도우미는 조건부로 현재 호스팅 환경에 따라 포함된 콘텐츠를 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="c125f-105">The Environment Tag Helper conditionally renders its enclosed content based on the current hosting environment.</span></span> <span data-ttu-id="c125f-106">단일 특성 `names`는 쉼표로 구분된 환경 이름 목록이며 현재 환경과 일치하는 경우 포함된 콘텐츠가 렌더링되도록 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="c125f-106">Its single attribute `names` is a comma separated list of environment names, that if any match to the current environment, will trigger the enclosed content to be rendered.</span></span>

## <a name="environment-tag-helper-attributes"></a><span data-ttu-id="c125f-107">환경 태그 도우미 특성</span><span class="sxs-lookup"><span data-stu-id="c125f-107">Environment Tag Helper Attributes</span></span>

### <a name="names"></a><span data-ttu-id="c125f-108">이름</span><span class="sxs-lookup"><span data-stu-id="c125f-108">names</span></span>

<span data-ttu-id="c125f-109">포함된 콘텐츠를 렌더링하도록 트리거하는 단일 호스팅 환경 이름 또는 쉼표로 구분된 호스팅 환경 이름 목록을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="c125f-109">Accepts a single hosting environment name or a comma-separated list of hosting environment names that trigger the rendering of the enclosed content.</span></span>

<span data-ttu-id="c125f-110">이러한 값은 ASP.NET Core 고정 속성 `HostingEnvironment.EnvironmentName`에서 반환된 현재 값과 비교됩니다.</span><span class="sxs-lookup"><span data-stu-id="c125f-110">These value(s) are compared to the current value returned from the ASP.NET Core static property `HostingEnvironment.EnvironmentName`.</span></span>  <span data-ttu-id="c125f-111">이 값은 **준비**, **개발** 또는 **프로덕션** 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="c125f-111">This value is one of the following: **Staging**; **Development** or **Production**.</span></span> <span data-ttu-id="c125f-112">비교는 대/소문자를 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="c125f-112">The comparison ignores case.</span></span>

<span data-ttu-id="c125f-113">유효한 `environment` 태그 도우미의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c125f-113">An example of a valid `environment` tag helper is:</span></span>

```cshtml
<environment names="Staging,Production">
  <strong>HostingEnvironment.EnvironmentName is Staging or Production</strong>
</environment>
```

## <a name="include-and-exclude-attributes"></a><span data-ttu-id="c125f-114">특성 포함 및 제외</span><span class="sxs-lookup"><span data-stu-id="c125f-114">include and exclude attributes</span></span>

<span data-ttu-id="c125f-115">ASP.NET Core 2.x는 `include` & `exclude` 특성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c125f-115">ASP.NET Core 2.x adds the `include` & `exclude` attributes.</span></span> <span data-ttu-id="c125f-116">이러한 특성은 포함 또는 제외 호스팅 환경 이름을 기반으로 포함된 콘텐츠를 렌더링하는 작업을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="c125f-116">These attributes control rendering the enclosed content based on the included or excluded hosting environment names.</span></span>

### <a name="include-aspnet-core-20-and-later"></a><span data-ttu-id="c125f-117">ASP.NET Core 2.0 이상 포함</span><span class="sxs-lookup"><span data-stu-id="c125f-117">include ASP.NET Core 2.0 and later</span></span>

<span data-ttu-id="c125f-118">`include` 속성에는 ASP.NET Core 1.0의 `names` 특성과 비슷한 동작이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c125f-118">The `include` property has a similar behavior of the `names` attribute in ASP.NET Core 1.0.</span></span>

```cshtml
<environment include="Staging,Production">
  <strong>HostingEnvironment.EnvironmentName is Staging or Production</strong>
</environment>
```

### <a name="exclude-aspnet-core-20-and-later"></a><span data-ttu-id="c125f-119">ASP.NET Core 2.0 이상 제외</span><span class="sxs-lookup"><span data-stu-id="c125f-119">exclude ASP.NET Core 2.0 and later</span></span>

<span data-ttu-id="c125f-120">반면 `exclude` 속성을 통해 `EnvironmentTagHelper`가 지정된 콘텐츠를 제외한 모든 호스팅 환경 이름에 대해 포함된 콘텐츠를 렌더링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c125f-120">In contrast, the `exclude` property lets the `EnvironmentTagHelper` render the enclosed content for all hosting environment names except the one(s) that you specified.</span></span>

```cshtml
<environment exclude="Development">
  <strong>HostingEnvironment.EnvironmentName is Staging or Production</strong>
</environment>
```

## <a name="additional-resources"></a><span data-ttu-id="c125f-121">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="c125f-121">Additional resources</span></span>

* <xref:fundamentals/environments>
* <xref:fundamentals/dependency-injection#service-lifetimes-and-registration-options>
