---
title: Razor 구성 요소 종속성 주입
author: guardrex
description: Blazor 및 Razor 구성 요소 앱 services을 사용 하 여 구성 요소를 삽입 하 여는 방법을 참조 하세요.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 03/27/2019
uid: razor-components/dependency-injection
ms.openlocfilehash: 40aec2e3a5032039c7d921f67d7d333b03c07fb1
ms.sourcegitcommit: 3e9e1f6d572947e15347e818f769e27dea56b648
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2019
ms.locfileid: "59515612"
---
# <a name="razor-components-dependency-injection"></a>Razor 구성 요소 종속성 주입

[Rainer Stropek](https://www.timecockpit.com)

Razor 구성 요소 지원 [종속성 주입 (DI)](xref:fundamentals/dependency-injection)합니다. 앱 구성 요소를 삽입 하 여 기본 제공 서비스를 사용할 수 있습니다. 앱 수 또한 정의 및 사용자 지정 서비스를 등록 하 고 앱 전체에서 DI 통해 사용할 수 있도록 합니다.

## <a name="dependency-injection"></a>종속성 주입

DI는 중앙 위치에 구성 된 서비스에 액세스 하기 위한 기술입니다. 이 Razor 구성 요소 앱에 유용할 수 있습니다.

* 라고 하는 여러 구성 요소 간에 서비스 클래스의 단일 인스턴스를 공유를 *singleton* 서비스입니다.
* 참조 추상화를 사용 하 여 구체적인 서비스 클래스에서 구성 요소를 분리 합니다. 예를 들어 인터페이스 `IDataAccess` 앱에서 데이터에 액세스 합니다. 인터페이스를 구현 하는 구체적으로 `DataAccess` 클래스 및 응용 프로그램의 서비스 컨테이너에서 서비스로 등록 합니다. 구성 요소를 수신 하는 데 DI를 사용 하는 경우는 `IDataAccess` 구현, 구성 요소는 구체적인 형식 결합 되지 않습니다. 아마도 단위 테스트에서 모의 구현을 구현을 교환할 수 있습니다.

자세한 내용은 <xref:fundamentals/dependency-injection>을 참조하세요.

## <a name="add-services-to-di"></a>DI에 서비스 추가

새 앱을 만든 후 검사를 `Startup.ConfigureServices` 메서드:

```csharp
public void ConfigureServices(IServiceCollection services)
{
    // Add custom services here
}
```

`ConfigureServices` 메서드에 전달 되는 <xref:Microsoft.Extensions.DependencyInjection.IServiceCollection>, 서비스 설명자 개체의 목록입니다 (<xref:Microsoft.Extensions.DependencyInjection.ServiceDescriptor>). 서비스는 서비스 컬렉션에 대 한 서비스 설명자를 제공 하 여 추가 됩니다. 다음 예제에서는 사용 하 여 개념은 `IDataAccess` 인터페이스 및 구체적인 구현 `DataAccess`:

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddSingleton<IDataAccess, DataAccess>();
}
```

다음 표에 나와 있는 수명을 사용 하 여 서비스를 구성할 수 있습니다.

| 수명 | 설명 |
| -------- | ----------- |
| <xref:Microsoft.Extensions.DependencyInjection.ServiceDescriptor.Singleton*> | DI 만듭니다는 *단일 인스턴스* 서비스입니다. 필요한 모든 구성 요소는 `Singleton` 서비스는 동일한 서비스의 인스턴스를 받습니다. |
| <xref:Microsoft.Extensions.DependencyInjection.ServiceDescriptor.Transient*> | 구성 요소를 때마다의 인스턴스를 가져옵니다을 `Transient` 서비스 수신한 서비스 컨테이너에서를 *새 인스턴스* 서비스입니다. |
| <xref:Microsoft.Extensions.DependencyInjection.ServiceDescriptor.Scoped*> | 현재 클라이언트 쪽 Blazor DI 범위 개념이 필요는 없습니다. `Scoped` 처럼 `Singleton`합니다. 그러나 ASP.NET Core Razor 구성 요소를 지원 합니다 `Scoped` 수명입니다. Razor 구성 요소를 연결으로 범위가 지정 된 서비스를 등록 하는 범위가 지정 됩니다. 이러한 이유로 범위가 지정 된 서비스를 사용 하는 현재 사용자에 게 범위가 지정 되어야 합니다는 서비스에 대 한 기본 현재는 클라이언트 쪽에서 실행 하는 경우에 브라우저에서 합니다. |

DI 시스템은 ASP.NET Core에서 DI 시스템을 기반으로 합니다. 자세한 내용은 <xref:fundamentals/dependency-injection>을 참조하세요.

## <a name="default-services"></a>기본 서비스

기본 서비스는 앱의 서비스 컬렉션에 자동으로 추가 됩니다.

| 서비스 | 설명 |
| ------- | ----------- |
| <xref:System.Net.Http.HttpClient> | HTTP 요청 송수신 (singleton) URI로 식별 되는 리소스에서 HTTP 응답에 대 한 메서드를 제공 합니다. 이 인스턴스의 `HttpClient` 브라우저를 사용 하 여 백그라운드에서 HTTP 트래픽을 처리 합니다. [HttpClient.BaseAddress](xref:System.Net.Http.HttpClient.BaseAddress) 앱의 기본 URI 접두사를 자동으로 설정 됩니다. `HttpClient` 클라이언트 쪽 Blazor 앱에만 제공 됩니다. |
| `IJSRuntime` | 호출 될 수 있습니다 디스패치해야 하는 JavaScript 런타임 인스턴스를 나타냅니다. 자세한 내용은 <xref:razor-components/javascript-interop>을 참조하세요. |
| `IUriHelper` | Uri 및 탐색 상태 (단일 항목)를 사용 하 여 작업에 대 한 도우미를 포함 합니다. `IUriHelper` Blazor 및 Razor 구성 요소를 모두 앱에 제공 됩니다. |

기본 템플릿을 통해 추가 하는 기본 서비스 공급자 대신 사용자 지정 서비스 공급자를 사용 하는 것이 가능 합니다. 사용자 지정 서비스 공급자 표에 나열 된 기본 서비스를 자동으로 제공 하지 않습니다. 사용자 지정 서비스 공급자를 사용 하는 표에 표시 된 서비스가 필요 하는 경우 새 서비스 공급자에 필요한 서비스를 추가 합니다.

## <a name="request-a-service-in-a-component"></a>구성 요소에서 서비스 요청

서비스 서비스 컬렉션에 추가 된 후 서비스를 사용 하 여 구성 요소 Razor 템플릿에 삽입 합니다 [ @inject ](xref:mvc/views/razor#section-4) Razor 지시문입니다. `@inject` 두 매개 변수가 있습니다.

* 유형 이름: 삽입할 서비스의 형식입니다.
* 속성 이름: 삽입 된 app service를 수신 하는 속성의 이름입니다. 참고 속성 수동으로 만들기를 필요 하지 않습니다. 컴파일러는 속성을 만듭니다.

자세한 내용은 <xref:mvc/views/dependency-injection>을 참조하세요.

사용 하 여 `@inject` 문을 서로 다른 서비스를 삽입 합니다.

다음 예제에서는 `@inject`을 사용하는 방법을 보여 줍니다. 서비스 구현 `Services.IDataAccess` 구성 요소의 속성에 주입 됩니다 `DataRepository`합니다. 만 코드를 사용 하는 방식을 참고 합니다 `IDataAccess` 추상화 합니다.

[!code-cshtml[](dependency-injection/samples_snapshot/3.x/CustomerList.cshtml?highlight=2-3,23)]

내부적으로 생성 된 속성 (`DataRepository`)으로 데코 레이트 된는 `InjectAttribute` 특성입니다. 일반적으로이 특성을 직접 사용 되지 않습니다. 기본 클래스는 구성 요소에 필요한 경우 삽입 된 속성은 또한 필수 기본 클래스에 대 한 `InjectAttribute` 수동으로 추가할 수 있습니다.

```csharp
public class ComponentBase : IComponent
{
    // Dependency injection works even if using the
    // InjectAttribute in a component's base class.
    [Inject]
    protected IDataAccess DataRepository { get; set; }
    ...
}
```

기본 클래스에서 파생 된 구성 요소에는 `@inject` 지시문은 필요 하지 않습니다. `InjectAttribute` 기본 클래스는 충분 합니다.

```cshtml
@page "/demo"
@inherits ComponentBase

<h1>Demo Component</h1>
```

## <a name="dependency-injection-in-services"></a>서비스에서 종속성 주입

복잡 한 서비스에는 추가 서비스 필요할 수 있습니다. 이전 예에서 `DataAccess` 필요할 수 있습니다는 `HttpClient` 기본 서비스입니다. `@inject` (또는 `InjectAttribute`) 서비스에서 사용 하기 위해 사용할 수 없습니다. *생성자 주입* 대신 사용 해야 합니다. 필요한 서비스는 서비스의 생성자에 매개 변수를 추가 하 여 추가 됩니다. 종속성 주입 된 서비스를 만들 때이 생성자에 필요 하며, 적절 하 게 제공 서비스 인식 합니다.

```csharp
public class DataAccess : IDataAccess
{
    // The constructor receives an HttpClient via dependency
    // injection. HttpClient is a default service.
    public DataAccess(HttpClient client)
    {
        ...
    }
}
```

생성자 주입을 위한 필수 조건:

* 인수 모두 수행할 수 있습니다 종속성 주입으로 생성자가 하나 있어야 합니다. DI에서 포함 하지 않는 추가 매개 변수는 기본값을 지정 하는 경우 허용 되는 참고 합니다.
* 해당 생성자 없어야 *공용*합니다.
* 해당 생성자가 하나 여야 합니다. 모호성을 발생 시 DI에 예외가 throw 됩니다.

## <a name="additional-resources"></a>추가 자료

* <xref:fundamentals/dependency-injection>
* <xref:mvc/views/dependency-injection>
