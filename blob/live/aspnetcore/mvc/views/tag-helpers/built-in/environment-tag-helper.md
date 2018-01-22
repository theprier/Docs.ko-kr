---
title: "ASP.NET Core에서 환경 태그 도우미"
author: pkellner
description: "ASP.NET Core 환경 태그 도우미 정의 된 모든 속성을 포함 하 여"
ms.author: riande
manager: wpickett
ms.date: 07/14/2017
ms.topic: article
ms.technology: aspnet
ms.prod: aspnet-core
uid: mvc/views/tag-helpers/builtin-th/environment-tag-helper
ms.openlocfilehash: 32646f1fdaf840f796da1ec573459157a41a86d1
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="environment-tag-helper-in-aspnet-core"></a><span data-ttu-id="a8b36-103">ASP.NET Core에서 환경 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="a8b36-103">Environment Tag Helper in ASP.NET Core</span></span>

<span data-ttu-id="a8b36-104">여 [Peter Kellner](http://peterkellner.net) 및 [Hisham Bin Ateya](https://twitter.com/hishambinateya)</span><span class="sxs-lookup"><span data-stu-id="a8b36-104">By [Peter Kellner](http://peterkellner.net) and [Hisham Bin Ateya](https://twitter.com/hishambinateya)</span></span>

<span data-ttu-id="a8b36-105">환경 태그 도우미 조건에 따라 현재 호스팅 환경에 따라 포함된 된 콘텐츠에 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b36-105">The Environment Tag Helper conditionally renders its enclosed content based on the current hosting environment.</span></span> <span data-ttu-id="a8b36-106">단일 특성 `names` 쉼표로 구분 된 목록이 환경 이름, 하는 모든 포함 된 콘텐츠를 렌더링할 수를 트리거할 현재 환경에 일치 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="a8b36-106">Its single attribute `names` is a comma separated list of environment names, that if any match to the current environment, will trigger the enclosed content to be rendered.</span></span>

## <a name="environment-tag-helper-attributes"></a><span data-ttu-id="a8b36-107">환경 태그 도우미 특성</span><span class="sxs-lookup"><span data-stu-id="a8b36-107">Environment Tag Helper Attributes</span></span>

### <a name="names"></a><span data-ttu-id="a8b36-108">이름</span><span class="sxs-lookup"><span data-stu-id="a8b36-108">names</span></span>

<span data-ttu-id="a8b36-109">단일 호스팅 환경 이름 또는 호스팅 환경 이름의 포함 된 콘텐츠를 렌더링을 트리거하는 쉼표로 구분 된 목록을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b36-109">Accepts a single hosting environment name or a comma-separated list of hosting environment names that trigger the rendering of the enclosed content.</span></span>

<span data-ttu-id="a8b36-110">이러한 값은 ASP.NET Core 정적 속성에서 반환 된 현재 값과 비교할 `HostingEnvironment.EnvironmentName`합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b36-110">These value(s) are compared to the current value returned from the ASP.NET Core static property `HostingEnvironment.EnvironmentName`.</span></span>  <span data-ttu-id="a8b36-111">이 값은 다음 중 하나: **준비**; **개발** 또는 **프로덕션**합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b36-111">This value is one of the following: **Staging**; **Development** or **Production**.</span></span> <span data-ttu-id="a8b36-112">비교는 대/소문자를 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b36-112">The comparison ignores case.</span></span>

<span data-ttu-id="a8b36-113">유효한의 예로 `environment` 태그 도우미는:</span><span class="sxs-lookup"><span data-stu-id="a8b36-113">An example of a valid `environment` tag helper is:</span></span>

```cshtml
<environment names="Staging,Production">
  <strong>HostingEnvironment.EnvironmentName is Staging or Production</strong>
</environment>
```

## <a name="include-and-exclude-attributes"></a><span data-ttu-id="a8b36-114">include 및 exclude 특성</span><span class="sxs-lookup"><span data-stu-id="a8b36-114">include and exclude attributes</span></span>

<span data-ttu-id="a8b36-115">ASP.NET Core 2.x 추가 `include`  &  `exclude` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="a8b36-115">ASP.NET Core 2.x adds the `include` & `exclude` attributes.</span></span> <span data-ttu-id="a8b36-116">포함 또는 제외 호스팅 환경 이름을 기반으로 포함 된 콘텐츠를 렌더링 하 이러한 특성 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b36-116">These attributes control rendering the enclosed content based on the included or excluded hosting environment names.</span></span>

### <a name="include-aspnet-core-20-and-later"></a><span data-ttu-id="a8b36-117">2.0 이상 ASP.NET Core를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b36-117">include ASP.NET Core 2.0 and later</span></span>

<span data-ttu-id="a8b36-118">`include` 의 비슷한 동작을 포함 하는 속성은 `names` ASP.NET Core 1.0의 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="a8b36-118">The `include` property has a similar behavior of the `names` attribute in ASP.NET Core 1.0.</span></span>

```cshtml
<environment include="Staging,Production">
  <strong>HostingEnvironment.EnvironmentName is Staging or Production</strong>
</environment>
```

### <a name="exclude-aspnet-core-20-and-later"></a><span data-ttu-id="a8b36-119">ASP.NET Core 2.0 이상 제외</span><span class="sxs-lookup"><span data-stu-id="a8b36-119">exclude ASP.NET Core 2.0 and later</span></span>

<span data-ttu-id="a8b36-120">반면,는 `exclude` 속성을 사용은 `EnvironmentTagHelper` 지정한 유형 제외한 모든 호스팅 환경 이름에 대해 포함 된 콘텐츠를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b36-120">In contrast, the `exclude` property lets the `EnvironmentTagHelper` render the enclosed content for all hosting environment names except the one(s) that you specified.</span></span>

```cshtml
<environment exclude="Development">
  <strong>HostingEnvironment.EnvironmentName is Staging or Production</strong>
</environment>
```

## <a name="additional-resources"></a><span data-ttu-id="a8b36-121">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="a8b36-121">Additional resources</span></span>

* <xref:fundamentals/environments>
* <xref:fundamentals/dependency-injection#service-lifetimes-and-registration-options>
