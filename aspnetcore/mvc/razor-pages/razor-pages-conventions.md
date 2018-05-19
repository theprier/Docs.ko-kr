---
title: ASP.NET Core에서 Razor 페이지 경로 및 앱 규칙
author: guardrex
description: 경로 및 앱 모델 공급자 규칙을 통해 페이지 라우팅, 검색 및 처리를 제어하는 방법을 검색합니다.
manager: wpickett
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.date: 04/12/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: mvc/razor-pages/razor-pages-conventions
ms.openlocfilehash: 15bb0687ffef777b82ea9374fdc3b92f3af7818b
ms.sourcegitcommit: 74be78285ea88772e7dad112f80146b6ed00e53e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="razor-pages-route-and-app-conventions-in-aspnet-core"></a>ASP.NET Core에서 Razor 페이지 경로 및 앱 규칙

[Luke Latham](https://github.com/guardrex)으로

페이지 [경로 및 앱 모델 공급자 규칙](xref:mvc/controllers/application-model#conventions)을 사용하여 Razor 페이지 앱에서 페이지 라우팅, 검색 및 처리를 제어하는 방법을 알아봅니다. 개별 페이지에 대한 사용자 지정 페이지 경로를 구성해야 하는 경우 이 항목의 뒷부분에서 설명할 [AddPageRoute 규칙](#configure-a-page-route)을 사용하여 페이지에 대한 라우팅을 구성합니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/razor-pages/razor-pages-conventions/sample/)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

::: moniker range="= aspnetcore-2.0"
| 시나리오 | 샘플에서는 다음 사항을 보여줍니다. |
| -------- | --------------------------- |
| [모델 규칙](#model-conventions)<br><br>Conventions.Add<ul><li>IPageRouteModelConvention</li><li>IPageApplicationModelConvention</li></ul> | 경로 템플릿 및 헤더를 앱의 페이지에 추가합니다. |
| [페이지 경로 작업 규칙](#page-route-action-conventions)<ul><li>AddFolderRouteModelConvention</li><li>AddPageRouteModelConvention</li><li>AddPageRoute</li></ul> | 폴더에 있는 페이지 및 단일 페이지에 경로 템플릿을 추가합니다. |
| [페이지 모델 작업 규칙](#page-model-action-conventions)<ul><li>AddFolderApplicationModelConvention</li><li>AddPageApplicationModelConvention</li><li>ConfigureFilter(필터 클래스, 람다 식 또는 필터 팩터리)</li></ul> | 폴더의 페이지에 헤더를 추가하고, 단일 페이지에 헤더를 추가하고, [필터 팩터리](xref:mvc/controllers/filters#ifilterfactory)를 구성하여 헤더를 앱의 페이지에 추가합니다. |
| [기본 페이지 앱 모델 공급자](#replace-the-default-page-app-model-provider) | 기본 페이지 모델 공급자를 대체하여 처리기 이름에 대한 규칙을 변경합니다. |
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
| 시나리오 | 샘플에서는 다음 사항을 보여줍니다. |
| -------- | --------------------------- |
| [모델 규칙](#model-conventions)<br><br>Conventions.Add<ul><li>IPageRouteModelConvention</li><li>IPageApplicationModelConvention</li><li>IPageHandlerModelConvention</li></ul> | 경로 템플릿 및 헤더를 앱의 페이지에 추가합니다. |
| [페이지 경로 작업 규칙](#page-route-action-conventions)<ul><li>AddFolderRouteModelConvention</li><li>AddPageRouteModelConvention</li><li>AddPageRoute</li></ul> | 폴더에 있는 페이지 및 단일 페이지에 경로 템플릿을 추가합니다. |
| [페이지 모델 작업 규칙](#page-model-action-conventions)<ul><li>AddFolderApplicationModelConvention</li><li>AddPageApplicationModelConvention</li><li>ConfigureFilter(필터 클래스, 람다 식 또는 필터 팩터리)</li></ul> | 폴더의 페이지에 헤더를 추가하고, 단일 페이지에 헤더를 추가하고, [필터 팩터리](xref:mvc/controllers/filters#ifilterfactory)를 구성하여 헤더를 앱의 페이지에 추가합니다. |
| [기본 페이지 앱 모델 공급자](#replace-the-default-page-app-model-provider) | 기본 페이지 모델 공급자를 대체하여 처리기 이름에 대한 규칙을 변경합니다. |
::: moniker-end

Razor 페이지 규칙은 `Startup` 클래스의 서비스 컬렉션에서 [AddMvc](/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addmvc)에 [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) 확장 메서드를 사용하여 추가되고 구성됩니다. 다음 규칙 예제는 이 토픽의 뒷부분에서 설명합니다.

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc()
        .AddRazorPagesOptions(options =>
            {
                options.Conventions.Add( ... );
                options.Conventions.AddFolderRouteModelConvention("/OtherPages", model => { ... });
                options.Conventions.AddPageRouteModelConvention("/About", model => { ... });
                options.Conventions.AddPageRoute("/Contact", "TheContactPage/{text?}");
                options.Conventions.AddFolderApplicationModelConvention("/OtherPages", model => { ... });
                options.Conventions.AddPageApplicationModelConvention("/About", model => { ... });
                options.Conventions.ConfigureFilter(model => { ... });
                options.Conventions.ConfigureFilter( ... );
            });
}
```

## <a name="model-conventions"></a>모델 규칙

[IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention)의 대리자를 추가하여 Razor 페이지에 적용되는 [모델 규칙](xref:mvc/controllers/application-model#conventions)을 추가합니다.

**모든 페이지에 경로 모델 규칙 추가**

[규칙](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions)을 사용하여 [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention)을 만들고, 페이지 경로 모델을 구축하는 동안 적용되는 [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) 인스턴스의 컬렉션에 추가합니다.

샘플 앱은 앱의 모든 페이지에 `{globalTemplate?}` 경로 템플릿을 추가합니다.

[!code-csharp[](razor-pages-conventions/sample/Conventions/GlobalTemplatePageRouteModelConvention.cs?name=snippet1)]

> [!NOTE]
> `AttributeRouteModel`에 대한 `Order` 속성을 `-1`로 설정합니다. 이렇게 하면 단일 경로 값이 제공될 때 이 템플릿에 첫 번째 경로 데이터 값 위치에 대한 우선 순위가 주어지며, 또한 자동으로 생성된 Razor 페이지 경로보다 우선하게 됩니다. 예를 들어 샘플은 항목의 뒷부분에서 `{aboutTemplate?}` 경로 템플릿을 추가합니다. `{aboutTemplate?}` 템플릿이 `1`의 `Order`로 제공됩니다. `/About/RouteDataValue`에서 정보 페이지를 요청하는 경우 "RouteDataValue"는 `Order` 속성 설정으로 인해 `RouteData.Values["aboutTemplate"]`(`Order = 1`)이 아닌 `RouteData.Values["globalTemplate"]`(`Order = -1`)으로 로드됩니다.

[규칙](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions) 추가와 같은 Razor 페이지 옵션은 MVC가 `Startup.ConfigureServices`의 서비스 컬렉션에 추가될 때 추가됩니다. 예제는 [샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/razor-pages/razor-pages-conventions/sample/)을 참조하세요.

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet1)]

`localhost:5000/About/GlobalRouteValue`에서 샘플의 정보 페이지를 요청하고 결과를 검사합니다.

![GlobalRouteValue의 경로 세그먼트를 사용하여 정보 페이지를 요청합니다. 렌더링된 페이지는 경로 데이터 값이 페이지의 OnGet 메서드에서 캡처되었음을 보여줍니다.](razor-pages-conventions/_static/about-page-global-template.png)

**모든 페이지에 앱 모델 규칙 추가**

[규칙](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions)을 사용하여 [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention)을 만들고, 페이지 앱 모델을 구축하는 동안 적용되는 [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) 인스턴스의 컬렉션에 추가합니다.

이 항목의 뒷부분에서 이 규칙 및 다른 규칙을 설명하기 위해 샘플 앱에는 `AddHeaderAttribute` 클래스가 포함됩니다. 클래스 생성자가 `name` 문자열 및 `values` 문자열 배열을 허용합니다. 이러한 값은 응답 헤더를 설정하는 `OnResultExecuting` 메서드에 사용됩니다. 전체 클래스는 항목의 뒷부분에 나오는 [페이지 모델 작업 규칙](#page-model-action-conventions) 섹션에서 보여줍니다.

샘플 앱에서는 앱의 모든 페이지에 `GlobalHeader` 헤더를 추가하는 `AddHeaderAttribute` 클래스를 사용합니다.

[!code-csharp[](razor-pages-conventions/sample/Conventions/GlobalHeaderPageApplicationModelConvention.cs?name=snippet1)]

*Startup.cs*:

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet2)]

`localhost:5000/About`에서 샘플의 정보 페이지를 요청하고 헤더를 검사하여 결과를 확인합니다.

![정보 페이지의 응답 헤더는 GlobalHeader가 추가되었음을 보여줍니다.](razor-pages-conventions/_static/about-page-global-header.png)

::: moniker range=">= aspnetcore-2.1"
**모든 페이지에 처리기 모델 규칙 추가**



[규칙](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions)을 사용하여 [IPageHandlerModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipagehandlermodelconvention)을 만들고, 페이지 처리기 모델을 구축하는 동안 적용되는 [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) 인스턴스의 컬렉션에 추가합니다.

```csharp
public class GlobalPageHandlerModelConvention 
    : IPageHandlerModelConvention
{
    public void Apply(PageHandlerModel model)
    {
        ...
    }
}
```

`Startup.ConfigureServices`:

```csharp
services.AddMvc()
    .AddRazorPagesOptions(options =>
        {
            options.Conventions.Add(new GlobalPageHandlerModelConvention());
        });
```
::: moniker-end

## <a name="page-route-action-conventions"></a>페이지 경로 작업 규칙

[IPageRouteModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelprovider)에서 파생되는 기본 경로 모델 공급자는 페이지 경로를 구성하기 위한 확장성 지점을 제공하도록 설계된 규칙을 호출합니다.

**폴더 경로 모델 규칙**

[AddFolderRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addfolderroutemodelconvention)을 사용하여 지정된 폴더 아래에 있는 모든 페이지에 [PageRouteModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageroutemodel)에 대한 작업을 호출하는 [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention)을 만들고 추가합니다.

샘플 앱에서는 `AddFolderRouteModelConvention`를 사용하여 `{otherPagesTemplate?}` 경로 템플릿을 *OtherPages* 폴더의 페이지에 추가합니다.

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet3)]

> [!NOTE]
> `AttributeRouteModel`에 대한 `Order` 속성을 `1`로 설정합니다. 그러면 단일 경로 값을 제공하는 경우 `{globalTemplate?}`에 대한 템플릿(항목의 앞에서 설정함)이 첫 번째 경로 데이터 값 위치에 지정된 우선 순위가 됩니다. `/OtherPages/Page1/RouteDataValue`에서 Page1 페이지를 요청하는 경우 "RouteDataValue"는 `Order` 속성 설정으로 인해 `RouteData.Values["otherPagesTemplate"]`(`Order = 1`)이 아닌 `RouteData.Values["globalTemplate"]`(`Order = -1`)으로 로드됩니다.

`localhost:5000/OtherPages/Page1/GlobalRouteValue/OtherPagesRouteValue`에서 샘플의 Page1 페이지를 요청하고 결과를 검사합니다.

![OtherPages 폴더의 Page1은 GlobalRouteValue 및 OtherPagesRouteValue라는 경로 세그먼트를 사용하여 요청됩니다. 렌더링된 페이지는 경로 데이터 값이 페이지의 OnGet 메서드에서 캡처되었음을 보여줍니다.](razor-pages-conventions/_static/otherpages-page1-global-and-otherpages-templates.png)

**페이지 경로 모델 규칙**

[AddPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addpageroutemodelconvention)을 사용하여 지정된 이름을 가진 페이지에 [PageRouteModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageroutemodel)에 대한 작업을 호출하는 [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention)을 만들고 추가합니다.

샘플 앱에서는 `AddPageRouteModelConvention`를 사용하여 `{aboutTemplate?}` 경로 템플릿을 정보 페이지에 추가합니다.

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet4)]

> [!NOTE]
> `AttributeRouteModel`에 대한 `Order` 속성을 `1`로 설정합니다. 그러면 단일 경로 값을 제공하는 경우 `{globalTemplate?}`에 대한 템플릿(항목의 앞에서 설정함)이 첫 번째 경로 데이터 값 위치에 지정된 우선 순위가 됩니다. `/About/RouteDataValue`에서 정보 페이지를 요청하는 경우 "RouteDataValue"는 `Order` 속성 설정으로 인해 `RouteData.Values["aboutTemplate"]`(`Order = 1`)이 아닌 `RouteData.Values["globalTemplate"]`(`Order = -1`)으로 로드됩니다.

`localhost:5000/About/GlobalRouteValue/AboutRouteValue`에서 샘플의 정보 페이지를 요청하고 결과를 검사합니다.

![정보 페이지는 GlobalRouteValue 및 AboutRouteValue에 대한 경로 세그먼트를 사용하여 요청됩니다. 렌더링된 페이지는 경로 데이터 값이 페이지의 OnGet 메서드에서 캡처되었음을 보여줍니다.](razor-pages-conventions/_static/about-page-global-and-about-templates.png)

## <a name="configure-a-page-route"></a>페이지 경로 구성

[AddPageRoute](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.addpageroute)를 사용하여 지정된 페이지 경로에 페이지에 대한 경로를 구성합니다. 페이지에 생성된 링크는 지정된 경로를 사용합니다. `AddPageRoute`는 `AddPageRouteModelConvention`을 사용하여 경로를 설정합니다.

샘플 앱은 *Contact.cshtml*의 `/TheContactPage`에 대한 경로를 만듭니다.

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet5)]

연락처 페이지도 기본 경로를 통해 `/Contact`에 도달할 수 있습니다.

연락처 페이지에 대한 샘플 앱의 사용자 지정 경로는 선택적 `text` 경로 세그먼트(`{text?}`)에 허용됩니다. 방문자가 해당 `/Contact` 경로에 있는 페이지에 액세스하는 경우 페이지에는 해당 `@page` 지시문에 있는 이 선택적 세그먼트가 포함됩니다.

[!code-cshtml[](razor-pages-conventions/sample/Pages/Contact.cshtml?highlight=1)]

렌더링된 페이지의 **연락처** 링크에 생성된 URL이 업데이트된 경로를 반영합니다.

![탐색 모음의 샘플 앱 연락처 링크](razor-pages-conventions/_static/contact-link.png)

![렌더링된 HTML에서 연락처 링크를 검사하면 href가 '/TheContactPage'로 설정되어 있음을 나타냅니다.](razor-pages-conventions/_static/contact-link-source.png)

일반적인 경로 `/Contact` 또는 사용자 지정 경로 `/TheContactPage`에서 연락처 페이지를 방문하세요. 추가 `text` 경로 세그먼트를 제공하는 경우 페이지는 제공한 HTML 인코딩 세그먼트를 보여줍니다.

![URL에서 'TextValue'라는 선택적 'text' 경로 세그먼트를 제공하는 에지 브라우저 예제입니다. 렌더링된 페이지에서는 'text' 세그먼트 값을 보여줍니다.](razor-pages-conventions/_static/route-segment-with-custom-route.png)

## <a name="page-model-action-conventions"></a>페이지 모델 작업 규칙

[IPageApplicationModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelprovider)에서 파생되는 기본 페이지 모델 공급자는 페이지 모델을 구성하기 위한 확장성 지점을 제공하도록 설계된 규칙을 호출합니다. 이러한 규칙은 페이지 검색 및 처리 시나리오를 빌드하고 수정하는 경우에 유용합니다.

샘플 앱은 이 섹션의 예제에서 응답 헤더를 적용하는 [ResultFilterAttribute](/dotnet/api/microsoft.aspnetcore.mvc.filters.resultfilterattribute)라는 `AddHeaderAttribute` 클래스를 사용합니다.

[!code-csharp[](razor-pages-conventions/sample/Filters/AddHeader.cs?name=snippet1)]

샘플을 규칙을 사용하여 폴더에 있는 모든 페이지 및 단일 페이지에 특성을 적용하는 방법을 보여줍니다.

**폴더 앱 모델 규칙**

[AddFolderApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addfolderapplicationmodelconvention)을 사용하여 지정된 폴더 아래에 있는 모든 페이지에 [PageApplicationModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageapplicationmodel) 인스턴스에 대한 작업을 호출하는 [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention)을 만들고 추가합니다.

이 샘플은 *OtherPages* 폴더 내의 페이지에 `OtherPagesHeader` 헤더를 추가하여 앱의 `AddFolderApplicationModelConvention`을 사용하는 방법을 보여줍니다.

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet6)]

`localhost:5000/OtherPages/Page1`에서 샘플의 Page1 페이지를 요청하고 헤더를 검사하여 결과를 확인합니다.

![OtherPages/Page1 페이지의 응답 헤더는 OtherPagesHeader가 추가되었음을 보여줍니다.](razor-pages-conventions/_static/page1-otherpages-header.png)

**페이지 앱 모델 규칙**

[AddPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addpageapplicationmodelconvention)을 사용하여 지정된 이름을 가진 페이지에 [PageApplicationModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageapplicationmodel)에 대한 작업을 호출하는 [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention)을 만들고 추가합니다.

샘플은 정보 페이지에 `AboutHeader` 헤더를 추가하여 `AddPageApplicationModelConvention`를 사용하는 방법을 보여줍니다.

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet7)]

`localhost:5000/About`에서 샘플의 정보 페이지를 요청하고 헤더를 검사하여 결과를 확인합니다.

![정보 페이지의 응답 헤더는 AboutHeader가 추가되었음을 보여줍니다.](razor-pages-conventions/_static/about-page-about-header.png)

**필터 구성**

[ConfigureFilter](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.configurefilter)는 지정된 필터를 적용하도록 구성합니다. 필터 클래스를 구현할 수 있지만 샘플 앱은 람다 식으로 필터를 구현하는 방법을 보여줍니다. 그러면 백그라운드에서 필터를 반환하는 팩터리로 구현됩니다.

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet8)]

페이지 앱 모델은 *OtherPages* 폴더에 있는 Page2 페이지로 이동하는 세그먼트에 대한 상대 경로를 확인하는 데 사용됩니다. 조건이 통과하는 경우 헤더가 추가됩니다. 그렇지 않으면 `EmptyFilter`이 적용됩니다.

`EmptyFilter`은 [작업 필터](xref:mvc/controllers/filters#action-filters)입니다. Razor 페이지에서 작업 필터를 무시하므로 경로에 `OtherPages/Page2`가 포함되지 않는 경우 의도한 대로 `EmptyFilter`이 작동되지 않습니다.

`localhost:5000/OtherPages/Page2`에서 샘플의 Page2 페이지를 요청하고 헤더를 검사하여 결과를 확인합니다.

![OtherPagesPage2Header는 Page2에 대한 응답에 추가됩니다.](razor-pages-conventions/_static/page2-filter-header.png)

**필터 팩터리 구성**

[ConfigureFilter](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.configurefilter?view=aspnetcore-2.0#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_ConfigureFilter_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_Func_Microsoft_AspNetCore_Mvc_ApplicationModels_PageApplicationModel_Microsoft_AspNetCore_Mvc_Filters_IFilterMetadata__)는 모든 Razor 페이지에 [필터](xref:mvc/controllers/filters)를 적용하도록 지정된 팩터리를 구성합니다.

샘플 앱은 앱의 페이지에 두 개의 값이 포함된 `FilterFactoryHeader` 헤더를 추가하여 [필터 팩터리](xref:mvc/controllers/filters#ifilterfactory)를 사용하는 예제를 제공합니다.

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet9)]

*AddHeaderWithFactory.cs*:

[!code-csharp[](razor-pages-conventions/sample/Factories/AddHeaderWithFactory.cs?name=snippet1)]

`localhost:5000/About`에서 샘플의 정보 페이지를 요청하고 헤더를 검사하여 결과를 확인합니다.

![정보 페이지의 응답 헤더에서는 두 개의 FilterFactoryHeader 헤더가 추가되었음을 보여줍니다.](razor-pages-conventions/_static/about-page-filter-factory-header.png)

## <a name="replace-the-default-page-app-model-provider"></a>기본 페이지 앱 모델 공급자 바꾸기

Razor 페이지는 `IPageApplicationModelProvider` 인터페이스를 사용하여 [DefaultPageApplicationModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.internal.defaultpageapplicationmodelprovider)를 만듭니다. 처리기 검색 및 처리에 대해 고유한 구현 논리를 제공하기 위해 기본 모델 공급자에서 상속할 수 있습니다. 기본 구현([참조 원본](https://github.com/aspnet/Mvc/blob/rel/2.0.1/src/Microsoft.AspNetCore.Mvc.RazorPages/Internal/DefaultPageApplicationModelProvider.cs))은 아래에서 설명할 *명명되지 않은* 및 *명명된* 처리기 명명에 대한 규칙을 설정합니다.

**기본 명명되지 않은 처리기 메서드**

HTTP 동사에 대한 처리기 메서드("명명되지 않은" 처리기 메서드)는 다음 규칙을 따릅니다. `On<HTTP verb>[Async]`(`Async`를 추가하는 것은 선택적이지만 비동기 메서드에서 사용하는 것이 좋습니다.)

| 명명되지 않은 처리기 메서드     | 작업                      |
| -------------------------- | ------------------------------ |
| `OnGet`/`OnGetAsync`       | 페이지 상태를 초기화합니다.     |
| `OnPost`/`OnPostAsync`     | POST 요청을 처리합니다.          |
| `OnDelete`/`OnDeleteAsync` | DELETE 요청을 처리합니다. |
| `OnPut`/`OnPutAsync`       | PUT 요청을 처리합니다.    |
| `OnPatch`/`OnPatchAsync`   | PATCH 요청을 처리합니다.  |

페이지에 대한 API를 호출하는 데 사용됩니다.

**기본 명명된 처리기 메서드**

개발자가 제공하는 처리기 메서드("명명된" 처리기 메서드)는 비슷한 규칙을 따릅니다. 처리기 이름은 HTTP 동사 뒤에 또는 HTTP 동사와 `Async` 사이에 표시됩니다. `On<HTTP verb><handler name>[Async]`(`Async`을 추가하는 것은 선택적이지만 비동기 메서드에서 사용하는 것이 좋습니다.) 예를 들어 메시지를 처리하는 메서드는 아래 표에 표시된 명명된 메시지일 수 있습니다.

| 예제 명명된 처리기 메서드             | 예제 작업        |
| ---------------------------------------- | ------------------------ |
| `OnGetMessage`/`OnGetMessageAsync`       | 메시지를 가져옵니다.        |
| `OnPostMessage`/`OnPostMessageAsync`     | 메시지를 게시합니다.          |
| `OnDeleteMessage`/`OnDeleteMessageAsync` | 메시지를 삭제합니다. |
| `OnPutMessage`/`OnPutMessageAsync`       | 메시지를 배치합니다.    |
| `OnPatchMessage`/`OnPatchMessageAsync`   | 메시지를 패치합니다.  |

페이지에 대한 API를 호출하는 데 사용됩니다.

**처리기 메서드 이름 사용자 지정**

명명되지 않은 및 명명된 처리기 메서드의 이름을 지정하는 방식을 변경하려는 경우를 가정합니다. 대체 이름 지정 체계는 메서드 이름을 "On"으로 시작되지 않도록 방지하고 첫 번째 단어 세그먼트를 사용하여 HTTP 동사를 결정합니다. 다른 변경을 수행할 수 있습니다(예: DELETE, PUT 및 PATCH에 대한 동사를 POST로 변환). 이러한 체계는 다음 표에 표시된 메서드 이름을 제공합니다.

| 처리기 메서드                       | 작업                      |
| ------------------------------------ | ------------------------------ |
| `Get`                                | 페이지 상태를 초기화합니다.     |
| `Post`/`PostAsync`                   | POST 요청을 처리합니다.          |
| `Delete`/`DeleteAsync`               | DELETE 요청을 처리합니다. |
| `Put`/`PutAsync`                     | PUT 요청을 처리합니다.    |
| `Patch`/`PatchAsync`                 | PATCH 요청을 처리합니다.  |
| `GetMessage`                         | 메시지를 가져옵니다.              |
| `PostMessage`/`PostMessageAsync`     | 메시지를 게시합니다.                |
| `DeleteMessage`/`DeleteMessageAsync` | 삭제할 메시지를 게시합니다.      |
| `PutMessage`/`PutMessageAsync`       | 배치할 메시지를 게시합니다.         |
| `PatchMessage`/`PatchMessageAsync`   | 패치할 메시지를 게시합니다.       |

페이지에 대한 API를 호출하는 데 사용됩니다.

이 체계를 설정하려면 `DefaultPageApplicationModelProvider` 클래스에서 상속하고, [CreateHandlerModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.internal.defaultpageapplicationmodelprovider.createhandlermodel) 메서드를 재정의하여 [PageModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel) 처리기 이름을 확인하는 사용자 지정 논리를 제공합니다. 샘플 앱에서는 `CustomPageApplicationModelProvider` 클래스에서 이 작업을 수행하는 방법을 보여줍니다.

[!code-csharp[](razor-pages-conventions/sample/CustomPageApplicationModelProvider.cs?name=snippet1&highlight=1-2,45-46,64-68,78-85,87,92,106)]

클래스의 장점은 다음과 같습니다.

* 클래스는 `DefaultPageApplicationModelProvider`에서 상속합니다.
* `TryParseHandlerMethod`는 `PageHandlerModel`를 만들 때 HTTP 동사(`httpMethod`) 및 명명된 처리기 이름(`handlerName`)을 결정하는 처리기를 처리합니다.
  * `Async` 후위가 있다면 무시합니다.
  * 대/소문자 구분을 사용하여 메서드 이름에서 HTTP 동사를 구문 분석합니다.
  * 메서드 이름(`Async` 제외)이 HTTP 동사 이름과 같은 경우 명명된 처리기가 없습니다. `handlerName`가 `null` 로 설정되고, 메서드 이름이 `Get`, `Post`, `Delete`, `Put` 또는 `Patch`입니다.
  * 메서드 이름(`Async` 제외)이 HTTP 동사 이름보다 긴 경우 명명된 처리기가 있습니다. `handlerName`는 `<method name (less 'Async', if present)>`로 설정됩니다. 예를 들어 "GetMessage" 및 "GetMessageAsync"는 모두 "GetMessage"라는 처리기 이름을 생성합니다.
  * DELETE, PUT 및 PATCH HTTP 동사는 POST로 변환됩니다.

`Startup` 클래스에 `CustomPageApplicationModelProvider`을 등록합니다.

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet10)]

*Index.cshtml.cs*의 페이지 모델은 앱에서 페이지에 대한 일반 처리기 메서드 명명 규칙을 변경하는 방법을 보여줍니다. Razor 페이지에서 사용되는 일반적인 "On" 접두사 이름 지정이 제거됩니다. 페이지 상태를 초기화하는 메서드의 이름은 이제 `Get`입니다. 페이지에 대한 페이지 모델을 여는 경우 앱 전체에서 사용하는 이 규칙을 볼 수 있습니다.

다른 메서드는 각각 해당 프로세스를 설명하는 HTTP 동사로 시작합니다. `Delete`로 시작하는 두 가지 메서드는 DELETE HTTP 동사로 정상적으로 처리되지만 `TryParseHandlerMethod`의 논리는 명시적으로 처리기 모두의 POST에 대해 동사로 설정합니다.

`Async`는 `DeleteAllMessages`와 `DeleteMessageAsync` 간에 선택 사항입니다. 모두 비동기 메서드이지만 `Async` 후위를 사용할지 선택할 수 있다면 사용하는 것이 좋습니다. `DeleteAllMessages`는 설명을 위해 사용되지만 이러한 `DeleteAllMessagesAsync` 메서드의 이름을 지정하는 것이 좋습니다. 샘플의 구현이라는 프로세스에 영향을 주지 않지만 `Async` 후위를 사용하면 비동기 메서드라는 점을 부각시킵니다.

[!code-csharp[](razor-pages-conventions/sample/Pages/Index.cshtml.cs?name=snippet1&highlight=1,6,16,29)]

*Index.cshtml*에서 제공된 처리기 이름은 `DeleteAllMessages` 및 `DeleteMessageAsync` 처리기 메서드와 일치합니다.

[!code-cshtml[](razor-pages-conventions/sample/Pages/Index.cshtml?range=29-60&highlight=7-8,24-25)]

처리기 메서드 이름 `DeleteMessageAsync`의 `Async`는 메서드에 대한 POST 요청과 일치하는 처리기에 대해 `TryParseHandlerMethod`을 기준으로 분류됩니다. `DeleteMessage`라는 `asp-page-handler` 이름은 처리기 메서드 `DeleteMessageAsync`와 일치합니다.

## <a name="mvc-filters-and-the-page-filter-ipagefilter"></a>MVC 필터 및 페이지 필터(IPageFilter)

Razor 페이지가 처리기 메서드를 사용하므로 MVC [작업 필터](xref:mvc/controllers/filters#action-filters)는 Razor 페이지에서 무시됩니다. [권한 부여](xref:mvc/controllers/filters#authorization-filters), [예외](xref:mvc/controllers/filters#exception-filters), [리소스](xref:mvc/controllers/filters#resource-filters) 및 [결과](xref:mvc/controllers/filters#result-filters)에 다른 유형의 MVC 필터를 사용할 수 있습니다. 자세한 내용은 [필터](xref:mvc/controllers/filters) 항목을 참조하세요.

페이지 필터([IPageFilter](/dotnet/api/microsoft.aspnetcore.mvc.filters.ipagefilter))는 Razor 페이지에 적용되는 필터입니다. 자세한 내용은 [Razor 페이지에 대한 필터 메서드](xref:mvc/razor-pages/filter)를 참조하세요.

## <a name="see-also"></a>참고 항목

* [Razor 페이지 권한 부여 규칙](xref:security/authorization/razor-pages-authorization)
