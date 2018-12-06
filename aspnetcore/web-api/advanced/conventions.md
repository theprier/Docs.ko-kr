---
title: 웹 API 규칙 사용
author: pranavkm
description: ASP.NET Core에서 웹 API 규칙에 대해 알아봅니다.
monikerRange: '>= aspnetcore-2.2'
ms.author: pranavkm
ms.custom: mvc
ms.date: 11/13/2018
uid: web-api/advanced/conventions
ms.openlocfilehash: ede9a46c160cf6a49aa93da710af0bf0b8f59acc
ms.sourcegitcommit: c4572be5ebb301013a5698caf9b5572b76cb2e34
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/30/2018
ms.locfileid: "52710077"
---
# <a name="use-web-api-conventions"></a>웹 API 규칙 사용

ASP.NET Core 2.2에는 일반적인 [API 설명서](xref:tutorials/web-api-help-pages-using-swagger)를 추출하여 여러 작업, 컨트롤러 또는 어셈블리 내 모든 컨트롤러에 적용하는 방법이 도입되었습니다. 웹 API 규칙은 개별 작업을 [[ProducesResponseType]](xref:Microsoft.AspNetCore.Mvc.ProducesResponseTypeAttribute)으로 데코레이팅하는 대체자입니다. 이 옵션을 사용하면 작업에 적용되는 규칙 메서드를 선택하는 방법으로 작업에서 반환되는 가장 일반적인 "기존" 반환 형식 및 상태 코드를 정의할 수 있습니다.

기본적으로 ASP.NET Core MVC 2.2는 기본 규칙 조합인 `Microsoft.AspNetCore.Mvc.DefaultApiConventions`와 함께 제공됩니다. 규칙은 ASP.NET Core 스캐폴드 컨트롤러를 기반으로 합니다. 작업이 스캐폴딩 생성의 패턴을 따르는 경우, 기본 규칙을 성공적으로 사용해야 합니다.

런타임 시 <xref:Microsoft.AspNetCore.Mvc.ApiExplorer>가 규칙을 이해합니다. `ApiExplorer`는 Open API 문서 생성기와 통신하기 위한 MVC의 개요입니다. 적용된 규칙의 특성은 작업과 연결되며 작업의 Swagger 설명서에 포함됩니다. API 분석기도 규칙을 이해합니다. 작업이 색다른 경우(예를 들어 적용된 규칙에 의해 문서화되지 않은 상태 코드를 반환하는 경우) 경고가 생성되어 문서화하도록 권장합니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/advanced/conventions/sample) ([다운로드 방법](xref:index#how-to-download-a-sample))

## <a name="apply-web-api-conventions"></a>웹 API 규칙 적용

규칙을 적용하는 세 가지가 방법이 있습니다. 규칙이 구성되지 않습니다. 각 작업이 정확히 하나의 규칙과 연결될 수 있습니다. 보다 구체적인 규칙(아래에 자세히 설명됨)은 덜 구체적인 규칙보다 우선합니다. 동일한 우선순위의 둘 이상의 규칙이 작업에 적용되는 경우 선택은 명확하지 않습니다. 다음 옵션은 가장 구체적인 것에서 가장 덜 구체적인 것까지 작업에 규칙을 적용할 수 있습니다.

1. `Microsoft.AspNetCore.Mvc.ApiConventionMethodAttribute` &mdash; 개별 작업에 적용되며 규칙 형식 및 적용되는 규칙 방법을 지정합니다. 다음 샘플에서는 `Update` 작업에 규칙 메서드 `Microsoft.AspNetCore.Mvc.DefaultApiConventions.Put`이 적용됩니다.

    [!code-csharp[](conventions/sample/Controllers/ContactsConventionController.cs?name=apiconventionmethod&highlight=2-3)]

1. &mdash; 컨트롤러에 `Microsoft.AspNetCore.Mvc.ApiConventionTypeAttribute`를 적용하면 컨트롤러에서 모든 작업에 규칙 유형을 적용합니다. 규칙 메서드는 적용하는 작업(작성 규칙의 일부로써의 세부 사항)를 결정하는 힌트로 데코레이팅됩니다. 예:

    [!code-csharp[](conventions/sample/Controllers/ContactsConventionController.cs?name=apiconventiontypeattribute)]

1. &mdash; 어셈블리에 적용된 `Microsoft.AspNetCore.Mvc.ApiConventionTypeAttribute`는 현재 어셈블리의 모든 컨트롤러에 규칙 유형을 적용합니다. 예:

    [!code-csharp[](conventions/sample/Startup.cs?name=apiconventiontypeattribute)]

## <a name="create-web-api-conventions"></a>웹 API 규칙 만들기

규칙은 메서드가 있는 정적 형식입니다. 이러한 메서드에는 `[ProducesResponseType]` 또는 `[ProducesDefaultResponseType]` 특성으로 주석이 추가됩니다.

```csharp
public static class MyAppConventions
{
    [ProducesResponseType(200)]
    [ProducesResponseType(404)]
    public static void Find(int id)
    {
    }
}
```

이 규칙을 어셈블리에 적용하면 다른 특정 메타데이터 특성이 없는 한 이름이 `Find`이고 `id`로 명명된 정확히 하나의 매개 변수가 있는 모든 작업에 적용되는 규칙 메서드가 됩니다.

`[ProducesResponseType]` 및 `[ProducesDefaultResponseType]` 외에도 `[ApiConventionNameMatch]` 및 `[ApiConventionTypeMatch]`를 적용할 메서드를 결정하는 규칙 메서드에 적용될 수 있습니다. 예:

```csharp
[ProducesResponseType(200)]
[ProducesResponseType(404)]
[ApiConventionNameMatch(ApiConventionNameMatchBehavior.Prefix)]
public static void Find(
    [ApiConventionNameMatch(ApiConventionNameMatchBehavior.Suffix)]
    int id)
{ }
```

* 메서드에 적용된 `Microsoft.AspNetCore.Mvc.ApiExplorer.ApiConventionNameMatchBehavior.Prefix` 옵션은 "찾기"로 접두사가 지정된 모든 작업과 일치할 수 있음을 나타냅니다. 여기에는 `Find`, `FindPet` 또는 `FindById`와 같은 메서드가 포함됩니다.
* 매개 변수에 적용된 `Microsoft.AspNetCore.Mvc.ApiExplorer.ApiConventionNameMatchBehavior.Suffix`는 규칙이 접미사 식별자로 끝나는 정확히 하나의 매개 변수와 메서드를 일치시킬 수 있음을 나타냅니다. 여기에는 `id` 또는 `petId`와 같은 매개 변수가 포함됩니다. `ApiConventionTypeMatch`는 매개 변수 유형을 제한하는 형식에도 유사하게 적용할 수 있습니다. `params[]` 인수를 사용하여 명시적으로 일치할 필요가 없는 나머지 매개 변수를 나타낼 수 있습니다.
