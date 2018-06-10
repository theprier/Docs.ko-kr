---
title: "ASP.NET Core의 Environment 태그 도우미"
author: pkellner
description: "모든 속성을 비롯하여 정의된 ASP.NET Core Environment 태그 도우미"
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
# <a name="environment-tag-helper-in-aspnet-core"></a>ASP.NET Core의 Environment 태그 도우미

작성자: [Peter Kellner](http://peterkellner.net) 및 [Hisham Bin Ateya](https://twitter.com/hishambinateya)

Environment 태그 도우미는 현재 호스팅 환경에 기반하여 포함된 콘텐츠를 조건부로 렌더링합니다. 유일한 특성인 `names`는 쉼표로 구분된 환경 이름의 목록으로 현재 환경과 일치하는 항목이 존재할 경우 포함된 콘텐츠가 렌더링되도록 트리거합니다.

## <a name="environment-tag-helper-attributes"></a>Environment 태그 도우미의 특성

### <a name="names"></a>names

포함된 콘텐츠를 렌더링하도록 트리거하는 단일 호스팅 환경 이름 또는 쉼표로 구분된 호스팅 환경 이름의 목록을 지정할 수 있습니다.

이 값(들)은 ASP.NET Core의 정적 속성인 `HostingEnvironment.EnvironmentName`에서 반환된 현재 값과 비교됩니다. 이 값은 **Staging**, **Development** 또는 **Production** 중 하나입니다. 이 비교에서 대/소문자는 무시됩니다.

유효한 `environment` 태그 도우미의 사례는 다음과 같습니다.

```cshtml
<environment names="Staging,Production">
  <strong>HostingEnvironment.EnvironmentName is Staging or Production</strong>
</environment>
```

## <a name="include-and-exclude-attributes"></a>include 및 exclude 특성

ASP.NET Core 2.x에는 `include` 및 `exclude` 특성이 추가되었습니다. 이 특성들은 포함된 또는 제외된 호스팅 환경 이름을 기반으로 포함된 콘텐츠의 렌더링 작업을 제어합니다.

### <a name="include-aspnet-core-20-and-later"></a>include (ASP.NET Core 2.0 이상)

`include` 속성은 ASP.NET Core 1.0의 `names` 특성과 비슷하게 동작합니다.

```cshtml
<environment include="Staging,Production">
  <strong>HostingEnvironment.EnvironmentName is Staging or Production</strong>
</environment>
```

### <a name="exclude-aspnet-core-20-and-later"></a>exclude (ASP.NET Core 2.0 이상)

반면 `exclude` 속성을 사용하면 지정한 호스팅 환경 이름(들)을 제외한 모든 호스팅 환경 이름에 대해 `EnvironmentTagHelper`가 포함된 콘텐츠를 렌더링할 수 있습니다.

```cshtml
<environment exclude="Development">
  <strong>HostingEnvironment.EnvironmentName is Staging or Production</strong>
</environment>
```

## <a name="additional-resources"></a>추가 자료

* <xref:fundamentals/environments>
* <xref:fundamentals/dependency-injection#service-lifetimes-and-registration-options>
