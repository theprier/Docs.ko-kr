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
# <a name="environment-tag-helper-in-aspnet-core"></a>ASP.NET Core의 환경 태그 도우미

작성자: [Peter Kellner](http://peterkellner.net) 및 [Hisham Bin Ateya](https://twitter.com/hishambinateya)

환경 태그 도우미는 조건부로 현재 호스팅 환경에 따라 포함된 콘텐츠를 렌더링합니다. 단일 특성 `names`는 쉼표로 구분된 환경 이름 목록이며 현재 환경과 일치하는 경우 포함된 콘텐츠가 렌더링되도록 트리거합니다.

## <a name="environment-tag-helper-attributes"></a>환경 태그 도우미 특성

### <a name="names"></a>이름

포함된 콘텐츠를 렌더링하도록 트리거하는 단일 호스팅 환경 이름 또는 쉼표로 구분된 호스팅 환경 이름 목록을 허용합니다.

이러한 값은 ASP.NET Core 고정 속성 `HostingEnvironment.EnvironmentName`에서 반환된 현재 값과 비교됩니다.  이 값은 **준비**, **개발** 또는 **프로덕션** 중 하나입니다. 비교는 대/소문자를 무시합니다.

유효한 `environment` 태그 도우미의 예는 다음과 같습니다.

```cshtml
<environment names="Staging,Production">
  <strong>HostingEnvironment.EnvironmentName is Staging or Production</strong>
</environment>
```

## <a name="include-and-exclude-attributes"></a>특성 포함 및 제외

ASP.NET Core 2.x는 `include` & `exclude` 특성을 추가합니다. 이러한 특성은 포함 또는 제외 호스팅 환경 이름을 기반으로 포함된 콘텐츠를 렌더링하는 작업을 제어합니다.

### <a name="include-aspnet-core-20-and-later"></a>ASP.NET Core 2.0 이상 포함

`include` 속성에는 ASP.NET Core 1.0의 `names` 특성과 비슷한 동작이 포함됩니다.

```cshtml
<environment include="Staging,Production">
  <strong>HostingEnvironment.EnvironmentName is Staging or Production</strong>
</environment>
```

### <a name="exclude-aspnet-core-20-and-later"></a>ASP.NET Core 2.0 이상 제외

반면 `exclude` 속성을 통해 `EnvironmentTagHelper`가 지정된 콘텐츠를 제외한 모든 호스팅 환경 이름에 대해 포함된 콘텐츠를 렌더링할 수 있습니다.

```cshtml
<environment exclude="Development">
  <strong>HostingEnvironment.EnvironmentName is Staging or Production</strong>
</environment>
```

## <a name="additional-resources"></a>추가 리소스

* <xref:fundamentals/environments>
* <xref:fundamentals/dependency-injection#service-lifetimes-and-registration-options>
