---
title: "요구 사항 처리기의 종속성 주입"
author: rick-anderson
description: "이 문서에서는 종속성 주입을 사용하여 ASP.NET Core 응용 프로그램에 권한 부여 요구 사항 처리기를 주입하는 방법을 설명합니다."
manager: wpickett
ms.author: riande
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/authorization/dependencyinjection
ms.openlocfilehash: 1b7506b49109264a8c628ea2e39ded9f5ace95d3
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="dependency-injection-in-requirement-handlers"></a>요구 사항 처리기의 종속성 주입

<a name="security-authorization-di"></a>

권한 부여 처리기는 구성 중 서비스 컬렉션에 [등록](policies.md#handler-registration)되어야 합니다([종속성 주입](../../fundamentals/dependency-injection.md#fundamentals-dependency-injection) 사용).

권한 부여 처리기 내부에서 평가해야 하는 규칙의 리포지토리가 존재하며, 해당 리포지토리가 서비스 컬렉션에 등록되어 있다고 가정해보겠습니다. 그러면 권한 부여가 이 종속성을 해결해서 생성자에 주입하게 됩니다.

예를 들어, 처리기에서 ASP.NET의 로깅 인프라를 사용하려면 처리기에 ILoggerFactory를 주입해야 합니다. 이 경우, 처리기의 코드는 다음과 같을 수 있습니다.

```csharp
public class LoggingAuthorizationHandler : AuthorizationHandler<MyRequirement>
{
    ILogger _logger;

    public LoggingAuthorizationHandler(ILoggerFactory loggerFactory)
    {
        _logger = loggerFactory.CreateLogger(this.GetType().FullName);
    }

    protected override Task HandleRequirementAsync(AuthorizationHandlerContext context, MyRequirement requirement)
    {
        _logger.LogInformation("Inside my handler");
        // Check if the requirement is fulfilled.
        return Task.CompletedTask;
    }
}
```

그리고 `services.AddSingleton()`를 이용해서 처리기를 등록합니다.

```csharp
services.AddSingleton<IAuthorizationHandler, LoggingAuthorizationHandler>();
```

그러면 응용 프로그램이 시작될 때 처리기의 인스턴스가 생성되고, DI가 등록된 `ILoggerFactory`를 생성자에 주입합니다.

> [!NOTE]
> Entity Framework를 사용하는 처리기는 싱글톤(singleton)으로 등록하면 안됩니다.
