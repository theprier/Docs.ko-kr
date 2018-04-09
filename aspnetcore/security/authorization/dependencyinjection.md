---
title: ASP.NET Core의 요구 사항 처리기의 종속성 주입
author: rick-anderson
description: 종속성 주입을 사용 하 여 ASP.NET Core 응용 프로그램에 권한 부여 요구 사항을 처리기를 삽입 하는 방법에 알아봅니다.
manager: wpickett
ms.author: riande
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/authorization/dependencyinjection
ms.openlocfilehash: 4de7f0e49ade459968f8c30fbad76ce96a65815f
ms.sourcegitcommit: 48beecfe749ddac52bc79aa3eb246a2dcdaa1862
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="dependency-injection-in-requirement-handlers-in-aspnet-core"></a><span data-ttu-id="57778-103">ASP.NET Core의 요구 사항 처리기의 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="57778-103">Dependency injection in requirement handlers in ASP.NET Core</span></span>

<a name="security-authorization-di"></a>

<span data-ttu-id="57778-104">권한 부여 처리기는 구성 중 서비스 컬렉션에 [등록](xref:security/authorization/policies#handler-registration)되어야 합니다([종속성 주입](xref:fundamentals/dependency-injection#fundamentals-dependency-injection) 사용).</span><span class="sxs-lookup"><span data-stu-id="57778-104">[Authorization handlers must be registered](xref:security/authorization/policies#handler-registration) in the service collection during configuration (using [dependency injection](xref:fundamentals/dependency-injection#fundamentals-dependency-injection)).</span></span>

<span data-ttu-id="57778-105">권한 부여 처리기 내부에서 평가해야 하는 규칙의 리포지토리가 존재하며, 해당 리포지토리가 서비스 컬렉션에 등록되어 있다고 가정해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="57778-105">Suppose you had a repository of rules you wanted to evaluate inside an authorization handler and that repository was registered in the service collection.</span></span> <span data-ttu-id="57778-106">그러면 권한 부여가 이 종속성을 해결해서 생성자에 주입하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57778-106">Authorization will resolve and inject that into your constructor.</span></span>

<span data-ttu-id="57778-107">예를 들어, 처리기에서 ASP.NET의 로깅 인프라를 사용하려면 처리기에 `ILoggerFactory`를 주입해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57778-107">For example, if you wanted to use ASP.NET's logging infrastructure you would want to inject `ILoggerFactory` into your handler.</span></span> <span data-ttu-id="57778-108">이 경우, 처리기의 코드는 다음과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57778-108">Such a handler might look like:</span></span>

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

<span data-ttu-id="57778-109">그리고 `services.AddSingleton()`를 이용해서 처리기를 등록합니다:</span><span class="sxs-lookup"><span data-stu-id="57778-109">You would register the handler with `services.AddSingleton()`:</span></span>

```csharp
services.AddSingleton<IAuthorizationHandler, LoggingAuthorizationHandler>();
```

<span data-ttu-id="57778-110">그러면 응용 프로그램이 시작될 때 처리기의 인스턴스가 생성되고, DI가 등록된 `ILoggerFactory`를 생성자에 주입합니다.</span><span class="sxs-lookup"><span data-stu-id="57778-110">An instance of the handler will be created when your application starts, and DI will inject the registered `ILoggerFactory` into your constructor.</span></span>

> [!NOTE]
> <span data-ttu-id="57778-111">Entity Framework를 사용하는 처리기는 싱글톤(singleton)으로 등록하면 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="57778-111">Handlers that use Entity Framework shouldn't be registered as singletons.</span></span>
