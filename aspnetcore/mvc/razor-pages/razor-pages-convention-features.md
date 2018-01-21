---
title: "ASP.NET Core에서 razor 페이지 경로 및 응용 프로그램 규칙 기능"
author: guardrex
description: "경로 및 응용 프로그램 모델 공급자 규칙 기능 하는 방법을 제어 페이지 라우팅, 검색 및 처리를 검색 합니다."
ms.author: riande
manager: wpickett
ms.date: 10/23/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: mvc/razor-pages/razor-pages-convention-features
ms.openlocfilehash: 69475ca9abd4e732dc704ad6a8a2fffe219984f7
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="razor-pages-route-and-app-convention-features-in-aspnet-core"></a>ASP.NET Core에서 razor 페이지 경로 및 응용 프로그램 규칙 기능

[Luke Latham](https://github.com/guardrex)으로

라우팅 페이지, 검색 및 Razor 페이지 응용 프로그램에서 처리를 제어 하려면 페이지 경로 및 응용 프로그램 모델 공급자 규칙 기능을 사용 하는 방법에 알아봅니다. 개별 페이지에 대 한 사용자 지정 페이지 경로 구성 해야 할 때 사용 하 여 페이지에 대 한 라우팅을 구성는 [AddPageRoute 규칙](#configure-a-page-route) 이 항목의 뒷부분에서 설명 합니다.

사용 하 여는 [샘플 응용 프로그램](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/razor-pages/razor-pages-convention-features/sample) ([다운로드 하는 방법을](xref:tutorials/index#how-to-download-a-sample))이이 항목에서 설명 하는 기능을 탐색할 수 있습니다.

| 기능 | 샘플을 보여 줍니다. |
| -------- | --------------------------- |
| [경로 및 응용 프로그램에 해당 하는 모델의 규칙](#add-route-and-app-model-conventions)<br><br>Conventions.Add<ul><li>IPageRouteModelConvention</li><li>IPageApplicationModelConvention</li></ul> | 경로 템플릿 및 헤더는 응용 프로그램의 페이지에 추가 합니다. |
| [경로 동작 규칙 페이지](#page-route-action-conventions)<ul><li>AddFolderRouteModelConvention</li><li>AddPageRouteModelConvention</li><li>AddPageRoute</li></ul> | 폴더에 있는 페이지를 한 페이지를 경로 템플릿을 추가 합니다. |
| [페이지 모델 작업 규칙](#page-model-action-conventions)<ul><li>AddFolderApplicationModelConvention</li><li>AddPageApplicationModelConvention</li><li>ConfigureFilter (필터 클래스, 람다 식 또는 필터 팩터리)</li></ul> | 단일 페이지에 헤더를 추가 및 구성 폴더의 페이지에 헤더를 추가는 [필터 공장](xref:mvc/controllers/filters#ifilterfactory) 는 응용 프로그램의 페이지에 헤더를 추가 하려면. |
| [기본 페이지 응용 프로그램 모델 공급자](#replace-the-default-page-app-model-provider) | 처리기 이름 지정에 대 한 규칙을 변경 하려면 기본 페이지 모델 공급자를 대체 합니다. |

## <a name="add-route-and-app-model-conventions"></a>경로 및 응용 프로그램 모델 규칙 추가

에 대 한 대리자를 추가 [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) Razor 페이지에 적용 되는 경로 및 응용 프로그램 모델 규칙을 추가 합니다.

**모든 페이지에 경로 모델 규칙 추가**

사용 하 여 [규칙](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions) 만들고 추가 하는 [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention) 의 컬렉션에 [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) 경로 및 페이지 모델 동안 적용 되는 인스턴스 구문을 사용 합니다.

샘플 응용 프로그램 추가 `{globalTemplate?}` 의 모든 앱에서 페이지 경로 템플릿입니다.

[!code-csharp[Main](razor-pages-convention-features/sample/Conventions/GlobalTemplatePageRouteModelConvention.cs?name=snippet1)]

> [!NOTE]
> `Order` 속성에 대 한는 `AttributeRouteModel` 로 설정 된 `0` (영)입니다. 이렇게 하면이 서식 파일은 단일 경로 값을 제공 하는 경우 첫 번째 경로 데이터 값 위치에 대 한 우선 순위를 지정 합니다. 이 샘플의 추가 예를 들어는 `{aboutTemplate?}` 항목의 뒷부분에 나오는 경로 템플릿입니다. `{aboutTemplate?}` 템플릿이 제공 됩니다는 `Order` 의 `1`합니다. 정보 페이지에서 요청 될 경우 `/About/RouteDataValue`, "RouteDataValue"에 로드 된 `RouteData.Values["globalTemplate"]` (`Order = 0`) 및 not `RouteData.Values["aboutTemplate"]` (`Order = 1`) 설정으로 인해는 `Order` 속성입니다.

*Startup.cs*:

[!code-csharp[Main](razor-pages-convention-features/sample/Startup.cs?name=snippet1)]

요청에 대 한 페이지 샘플의 `localhost:5000/About/GlobalRouteValue` 하 고 결과 검사 합니다.

![정보 페이지 GlobalRouteValue의 경로 세그먼트와 요청 됩니다. 렌더링된 된 페이지는 페이지의 OnGet 메서드에서 경로 데이터 값은 캡처 함을 보여 줍니다.](razor-pages-convention-features/_static/about-page-global-template.png)

**모든 페이지에 응용 프로그램 모델 규칙 추가**

사용 하 여 [규칙](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions) 만들고 추가 하는 [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention) 의 컬렉션에 [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) 경로 및 페이지 동안 적용 되는 인스턴스 모델 생성 합니다.

샘플 응용 프로그램에 포함 되어이 및 다른 규칙 항목의 뒷부분에 나오는 보여 주기 위해는 `AddHeaderAttribute` 클래스입니다. 클래스 생성자가 허용 된 `name` 문자열 및 `values` 문자열 배열을 반환 합니다. 이러한 값에 사용 되는 `OnResultExecuting` 응답 헤더를 설정 하는 메서드. 전체 클래스에 표시 되는 [모델 작업 규칙 페이지](#page-model-action-conventions) 항목의 뒷부분에 나오는 섹션.

샘플 앱에서는 `AddHeaderAttribute` 머리글을 추가 하려면 클래스 `GlobalHeader`, 모든 앱에서 페이지에:

[!code-csharp[Main](razor-pages-convention-features/sample/Conventions/GlobalHeaderPageApplicationModelConvention.cs?name=snippet1)]

*Startup.cs*:

[!code-csharp[Main](razor-pages-convention-features/sample/Startup.cs?name=snippet2)]

요청에 대 한 페이지 샘플의 `localhost:5000/About` 결과를 보려면 헤더를 검사 하 고 있습니다.

![정보 페이지의 응답 헤더는 GlobalHeader 추가 된 것을 표시 합니다.](razor-pages-convention-features/_static/about-page-global-header.png)

## <a name="page-route-action-conventions"></a>경로 동작 규칙 페이지

파생 되는 기본 경로 모델 공급자 [IPageRouteModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelprovider) 페이지 경로 구성 하기 위한 확장 지점을 제공 하도록 설계 된 규칙을 호출 합니다.

**폴더 경로 모델 규칙**

사용 하 여 [AddFolderRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addfolderroutemodelconvention) 만들고 추가 하는 [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention) 에 작업을 호출 하는 [PageRouteModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageroutemodel) 아래 페이지의 모든는 지정 된 폴더입니다.

샘플 앱에서는 `AddFolderRouteModelConvention` 추가 하는 `{otherPagesTemplate?}` 경로 템플릿을의 페이지에는 *OtherPages* 폴더:

[!code-csharp[Main](razor-pages-convention-features/sample/Startup.cs?name=snippet3)]

> [!NOTE]
> `Order` 속성에 대 한는 `AttributeRouteModel` 로 설정 된 `1`합니다. 이렇게 하면에 대 한 템플릿 `{globalTemplate?}` (이 항목의 앞부분에 나오는 설정) 하면 단일 경로 값을 제공 하는 경우 첫 번째 경로 데이터 값 위치에 대 한 우선 순위가 지정 됩니다. 페이지 1 페이지를 요청 하는 경우 `/OtherPages/Page1/RouteDataValue`, "RouteDataValue"에 로드 된 `RouteData.Values["globalTemplate"]` (`Order = 0`) 및 not `RouteData.Values["otherPagesTemplate"]` (`Order = 1`) 설정으로 인해는 `Order` 속성입니다.

요청에서 샘플의 1 페이지 페이지 `localhost:5000/OtherPages/Page1/GlobalRouteValue/OtherPagesRouteValue` 하 고 결과 검사 합니다.

![OtherPages 폴더에 대 한 1 페이지 GlobalRouteValue 및 OtherPagesRouteValue 경로 세그먼트와 요청 됩니다. 렌더링된 된 페이지는 페이지의 OnGet 메서드에 경로 데이터 값은 캡처 함을 보여 줍니다.](razor-pages-convention-features/_static/otherpages-page1-global-and-otherpages-templates.png)

**페이지 경로 모델 규칙**

사용 하 여 [AddPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addpageroutemodelconvention) 만들고 추가 하는 [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention) 에 작업을 호출 하는 [PageRouteModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageroutemodel) 지정 된 페이지에 대 한 이름입니다.

샘플 앱에서는 `AddPageRouteModelConvention` 추가 하는 `{aboutTemplate?}` 경로 템플릿을 정보 페이지에:

[!code-csharp[Main](razor-pages-convention-features/sample/Startup.cs?name=snippet4)]

> [!NOTE]
> `Order` 속성에 대 한는 `AttributeRouteModel` 로 설정 된 `1`합니다. 이렇게 하면에 대 한 템플릿 `{globalTemplate?}` (이 항목의 앞부분에 나오는 설정) 하면 단일 경로 값을 제공 하는 경우 첫 번째 경로 데이터 값 위치에 대 한 우선 순위가 지정 됩니다. 정보 페이지에서 요청 된 경우 `/About/RouteDataValue`, "RouteDataValue"에 로드 된 `RouteData.Values["globalTemplate"]` (`Order = 0`) 및 not `RouteData.Values["aboutTemplate"]` (`Order = 1`) 설정으로 인해는 `Order` 속성입니다.

요청에 대 한 페이지 샘플의 `localhost:5000/About/GlobalRouteValue/AboutRouteValue` 하 고 결과 검사 합니다.

![페이지에 대 한 요청 된 경로 세그먼트와 GlobalRouteValue 및 AboutRouteValue 합니다. 렌더링된 된 페이지는 페이지의 OnGet 메서드에 경로 데이터 값은 캡처 함을 보여 줍니다.](razor-pages-convention-features/_static/about-page-global-and-about-templates.png)

## <a name="configure-a-page-route"></a>페이지 경로 구성

사용 하 여 [AddPageRoute](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.addpageroute) 지정된 페이지 경로에 페이지에 대 한 경로 구성 합니다. 페이지에 생성 된 링크에 지정 된 경로 사용합니다. `AddPageRoute`사용 하 여 `AddPageRouteModelConvention` 경로 설정 합니다.

샘플 응용 프로그램에 대 한 경로 만듭니다. `/TheContactPage` 에 대 한 *Contact.cshtml*:

[!code-csharp[Main](razor-pages-convention-features/sample/Startup.cs?name=snippet5)]

연락처 페이지에도 액세스할 수 `/Contact` 의 기본 경로 통해.

연락처 페이지에 샘플 응용 프로그램의 사용자 지정 경로 선택 사항에 대 한 허용 `text` 경로 세그먼트 (`{text?}`). 이 선택적 세그먼트에는 페이지에도 포함 되어 해당 `@page` 방문자에 있는 페이지에 액세스 하는 경우 지시문의 `/Contact` 경로:

[!code-cshtml[Main](razor-pages-convention-features/sample/Pages/Contact.cshtml?highlight=1)]

URL에 대해 생성 하는 **연락처** 업데이트 된 경로 반영 하는 렌더링 된 페이지의 링크:

![탐색 모음에서 샘플 응용 프로그램에 게 문의 링크](razor-pages-convention-features/_static/contact-link.png)

![Href로 설정 되어 있는지 나타냅니다 렌더링 된 html에서 연락처 링크 검사 ' / TheContactPage'](razor-pages-convention-features/_static/contact-link-source.png)

페이지를 방문 하면 연락처 하나에 해당 일반 경로 `/Contact`, 또는 사용자 지정 경로 `/TheContactPage`합니다. 추가로 제공 하는 경우 `text` 경로 세그먼트의 페이지에 표시는 HTML로 인코딩된 세그먼트를 제공 해야 합니다.

![제공 된 옵션 'text' 경로 세그먼트 'TextValue' url에서의 edge 브라우저 예제입니다. 렌더링 된 페이지에는 'text' 세그먼트 값을 표시 됩니다.](razor-pages-convention-features/_static/route-segment-with-custom-route.png)

## <a name="page-model-action-conventions"></a>페이지 모델 작업 규칙

구현 하는 기본 페이지 모델 공급자 [IPageApplicationModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelprovider) 페이지 모델을 구성 하기 위한 확장 지점을 제공 하도록 설계 된 규칙을 호출 합니다. 이러한 규칙은 빌드 및 페이지 검색 및 처리 기능을 수정 하는 경우에 유용 합니다.

샘플 응용 프로그램에 대 한이 섹션의 예제를 사용 하 여는 `AddHeaderAttribute` 클래스 즉는 [ResultFilterAttribute](/dotnet/api/microsoft.aspnetcore.mvc.filters.resultfilterattribute), 응답 헤더를 적용 하 합니다.

[!code-csharp[Main](razor-pages-convention-features/sample/Filters/AddHeader.cs?name=snippet1)]

규칙을 사용 하는 샘플 및 단일 페이지 폴더에 있는 페이지의 모든 특성을 적용 하는 방법을 보여 줍니다.

**응용 프로그램 모델 규칙 폴더**

사용 하 여 [AddFolderApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addfolderapplicationmodelconvention) 만들고 추가 하는 [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention) 에 작업을 호출 하는 [PageApplicationModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageapplicationmodel) 에 대 한 인스턴스 지정된 된 폴더 아래에 있는 모든 페이지입니다.

이 샘플의 사용법을 보여줍니다 `AddFolderApplicationModelConvention` 헤더를 추가 하 여 `OtherPagesHeader`, 내부 페이지에는 *OtherPages* 응용 프로그램의 폴더:

[!code-csharp[Main](razor-pages-convention-features/sample/Startup.cs?name=snippet6)]

요청에서 샘플의 1 페이지 페이지 `localhost:5000/OtherPages/Page1` 결과를 보려면 헤더를 검사 하 고 있습니다.

![페이지 OtherPages/1 페이지의 응답 헤더는 OtherPagesHeader 추가 된 것을 표시 합니다.](razor-pages-convention-features/_static/page1-otherpages-header.png)

**응용 프로그램 모델 규칙 페이지**

사용 하 여 [AddPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addpageapplicationmodelconvention) 만들고 추가 하는 [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention) 에 작업을 호출 하는 [PageApplicationModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageapplicationmodel) 페이지 speciifed 이름입니다.

이 샘플의 사용법을 보여줍니다 `AddPageApplicationModelConvention` 헤더를 추가 하 여 `AboutHeader`, 정보 페이지에:

[!code-csharp[Main](razor-pages-convention-features/sample/Startup.cs?name=snippet7)]

요청에 대 한 페이지 샘플의 `localhost:5000/About` 결과를 보려면 헤더를 검사 하 고 있습니다.

![정보 페이지의 응답 헤더는 AboutHeader 추가 된 것을 표시 합니다.](razor-pages-convention-features/_static/about-page-about-header.png)

**필터 구성**

[ConfigureFilter](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.configurefilter) 적용할 지정된 된 필터를 구성 합니다. 필터 클래스를 구현할 수 있지만 샘플 응용 프로그램에 백그라운드는 필터를 반환 하는 팩터리로 구현 되는 람다 식에 필터를 구현 하는 방법을 보여 줍니다.

[!code-csharp[Main](razor-pages-convention-features/sample/Startup.cs?name=snippet8)]

페이지 응용 프로그램 모델에서 페이지 2 페이지를 가리키는 세그먼트에 대 한 상대 경로 확인을 위해 사용 된 *OtherPages* 폴더입니다. 조건을 통과 하는 경우에 헤더가 추가 됩니다. 그렇지 않은 경우, `EmptyFilter` 적용 됩니다.

`EmptyFilter`이 [작업 필터](xref:mvc/controllers/filters#action-filters)합니다. Razor 페이지에서 작업 필터를 무시 하므로 `EmptyFilter` 아니요 ops 경로 포함 하지 않는 경우 의도 한 대로 `OtherPages/Page2`합니다.

요청에서 샘플의 2 페이지 페이지 `localhost:5000/OtherPages/Page2` 결과를 보려면 헤더를 검사 하 고 있습니다.

![OtherPagesPage2Header 2 페이지에 대 한 응답에 추가 됩니다.](razor-pages-convention-features/_static/page2-filter-header.png)

**필터 팩터리 구성**

[ConfigureFilter](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.configurefilter?view=aspnetcore-2.0#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_ConfigureFilter_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_Func_Microsoft_AspNetCore_Mvc_ApplicationModels_PageApplicationModel_Microsoft_AspNetCore_Mvc_Filters_IFilterMetadata__) 적용 하려면 지정 된 팩터리 구성 [필터](xref:mvc/controllers/filters) 모든 Razor 페이지에 있습니다.

사용 하는 예제를 제공 하는 샘플 응용 프로그램을 [필터 공장](xref:mvc/controllers/filters#ifilterfactory) 헤더를 추가 하 여 `FilterFactoryHeader`, 응용 프로그램의 페이지에 두 값이 포함:

[!code-csharp[Main](razor-pages-convention-features/sample/Startup.cs?name=snippet9)]

*AddHeaderWithFactory.cs*:

[!code-csharp[Main](razor-pages-convention-features/sample/Factories/AddHeaderWithFactory.cs?name=snippet1)]

요청에 대 한 페이지 샘플의 `localhost:5000/About` 결과를 보려면 헤더를 검사 하 고 있습니다.

![응답 헤더 정보 페이지의 두 개의 FilterFactoryHeader 헤더 추가 된 것을 표시 합니다.](razor-pages-convention-features/_static/about-page-filter-factory-header.png)

## <a name="replace-the-default-page-app-model-provider"></a>기본 페이지 응용 프로그램 모델 공급자를 대체 합니다.

Razor 페이지를 사용 하 여는 `IPageApplicationModelProvider` 를 만들려면 인터페이스는 [DefaultPageApplicationModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.internal.defaultpageapplicationmodelprovider)합니다. 처리기 검색 및 처리에 대 한 직접 구현 논리를 제공 하는 기본 모델 공급자에서 상속할 수 있습니다. 기본 구현 ([참조 소스](https://github.com/aspnet/Mvc/blob/rel/2.0.1/src/Microsoft.AspNetCore.Mvc.RazorPages/Internal/DefaultPageApplicationModelProvider.cs))에 대 한 규칙을 설정 *명명 되지 않은* 및 *라는* 아래 설명 하는 처리기 이름을 지정 합니다.

**기본 명명 되지 않은 처리기 메서드**

HTTP 동사 ("명명 되지 않은" 처리기 메서드)에 대 한 처리기 메서드는 규칙을 따릅니다: `On<HTTP verb>[Async]` (추가 `Async` 은 선택적 이지만 비동기 메서드에 대 한 권장).

| 명명 되지 않은 처리기 메서드     | 작업                      |
| -------------------------- | ------------------------------ |
| `OnGet`/`OnGetAsync`       | 페이지 상태를 초기화 합니다.     |
| `OnPost`/`OnPostAsync`     | POST 요청을 처리 합니다.          |
| `OnDelete`/`OnDeleteAsync` | 삭제 요청 수 &#8224; 처리 합니다. |
| `OnPut`/`OnPutAsync`       | PUT 요청을 &#8224; 처리 합니다.    |
| `OnPatch`/`OnPatchAsync`   | PATCH 요청 &#8224; 처리 합니다.  |

&#8224; 페이지에 대 한 API 호출에 사용 합니다.

**기본 명명 된 처리기 메서드**

("이름" 처리기 메서드)는 개발자가 제공 하는 처리기 메서드는 비슷한 규칙을 따릅니다. HTTP 동사 또는 HTTP 동사 뒤 처리기 이름은 표시 및 `Async`: `On<HTTP verb><handler name>[Async]` (추가 `Async` 은 선택적 이지만 비동기 메서드에 대 한 권장). 예를 들어 메시지를 처리 하는 메서드는 아래 표에 표시 된 명명 걸릴 수 있습니다.

| 라는 처리기 메서드 예제             | 예제 작업        |
| ---------------------------------------- | ------------------------ |
| `OnGetMessage`/`OnGetMessageAsync`       | 메시지를 가져옵니다.        |
| `OnPostMessage`/`OnPostMessageAsync`     | 메시지를 게시 합니다.          |
| `OnDeleteMessage`/`OnDeleteMessageAsync` | 메시지 #8224; 삭제 합니다. |
| `OnPutMessage`/`OnPutMessageAsync`       | 메시지 &#8224; 넣습니다.    |
| `OnPatchMessage`/`OnPatchMessageAsync`   | 메시지 &#8224; PATCH 합니다.  |

&#8224; 페이지에 대 한 API 호출에 사용 합니다.

**처리기 메서드 이름을 사용자 지정**

명명 되지 않은 및 명명 된 처리기 메서드가 이름을 지정 하는 방식을 변경 하려는 경우를 가정 합니다. 대체 이름 지정 체계 메서드 이름이 "On"으로 시작 되지 않는 HTTP 동사를 확인 하려면 첫 번째 단어 세그먼트를 사용 하는 것입니다. 다른 변경을 수행할 수 있습니다 삭제에 대 한 동사를 변환, 예: PUT, 및 POST를 패치 합니다. 구성표를 다음 표에 표시 된 메서드 이름을 제공 합니다.

| 처리기 메서드                       | 작업                      |
| ------------------------------------ | ------------------------------ |
| `Get`                                | 페이지 상태를 초기화 합니다.     |
| `Post`/`PostAsync`                   | POST 요청을 처리 합니다.          |
| `Delete`/`DeleteAsync`               | 삭제 요청 수 &#8224; 처리 합니다. |
| `Put`/`PutAsync`                     | PUT 요청을 &#8224; 처리 합니다.    |
| `Patch`/`PatchAsync`                 | PATCH 요청 &#8224; 처리 합니다.  |
| `GetMessage`                         | 메시지를 가져옵니다.              |
| `PostMessage`/`PostMessageAsync`     | 메시지를 게시 합니다.                |
| `DeleteMessage`/`DeleteMessageAsync` | 삭제할 메시지를 게시 합니다.      |
| `PutMessage`/`PutMessageAsync`       | 배치에 메시지를 게시 합니다.         |
| `PatchMessage`/`PatchMessageAsync`   | 패치에 메시지를 게시 합니다.       |

&#8224; 페이지에 대 한 API 호출에 사용 합니다.

이 체계를 설정 하려면에서 상속 하는 `DefaultPageApplicationModelProvider` 클래스 및 재정의 [CreateHandlerModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.internal.defaultpageapplicationmodelprovider.createhandlermodel) 확인 하기 위한 사용자 지정 논리를 제공 하는 메서드 [PageModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel) 처리기 이름은 합니다. 샘플 앱 표시이 작업을 수행 하는 방법의 `CustomPageApplicationModelProvider` 클래스:

[!code-csharp[Main](razor-pages-convention-features/sample/CustomPageApplicationModelProvider.cs?name=snippet1&highlight=1-2,45-46,64-68,78-85,87,92,106)]

클래스의 장점:

* 클래스에서 상속 `DefaultPageApplicationModelProvider`합니다.
* `TryParseHandlerMethod` 처리 하는 HTTP 동사를 결정 하는 처리기 (`httpMethod`) 및 명명 된 처리기 이름 (`handlerName`)를 만들 때는 `PageHandlerModel`합니다.
  * `Async` 있는 경우, 후 위 무시 됩니다.
  * 대/소문자 구분 메서드 이름에서 HTTP 동사를 구문 분석 하는 데 사용 됩니다.
  * 때 메서드 이름 (없이 `Async`)는 HTTP 동사 이름 같음, 처리기가 없는 명명 합니다. `handlerName` 로 설정 된 `null`, 그리고 메서드 이름이 `Get`, `Post`, `Delete`, `Put`, 또는 `Patch`합니다.
  * 때 메서드 이름 (없이 `Async`) HTTP 동사 이름 보다 긴 명명 된 처리기가 있습니다. `handlerName`는 `<method name (less 'Async', if present)>`로 설정됩니다. 예를 들어 "GetMessage" 및 "GetMessageAsync" 모두 "GetMessage"의 처리기 이름을 생성합니다.
  * DELETE, PUT, 및 PATCH HTTP 동사는 POST로 변환 됩니다.

등록 된 `CustomPageApplicationModelProvider` 에 `Startup` 클래스:

[!code-csharp[Main](razor-pages-convention-features/sample/Startup.cs?name=snippet10)]

코드 숨김 파일 *Index.cshtml.cs* 페이지 응용 프로그램에 대 한 일반 처리기 메서드 명명 규칙은 변경 하는 방법을 보여 줍니다. "에서" 접두사 명명 Razor 페이지를 사용 하는 일반적인 제거 됩니다. 페이지 상태를 초기화 하는 메서드는 이제 이름이 `Get`합니다. 여러 페이지에 대 한 코드 숨김 파일을 열 경우 응용 프로그램 전체에서 사용 하는이 규칙을 볼 수 있습니다.

다른 메서드는 각각 처리를 설명 하는 HTTP 동사와 시작 합니다. 로 시작 하는 두 가지 방법 `Delete` DELETE HTTP 동사 하지만의 논리로 정상적으로 처리 됩니다 `TryParseHandlerMethod` 명시적으로 모두 처리기에 대 한 동사 POST로 설정 합니다.

`Async` 는 선택 사항 간의 `DeleteAllMessages` 및 `DeleteMessageAsync`합니다. 비동기 메서드 모두 하지만 사용 하도록 선택할 수는 `Async` 여부를 후 위; 수행 하는 것이 좋습니다. `DeleteAllMessages`설명을 위해 여기에이 있지만 이러한 메서드의 이름을 지정 하는 것이 좋습니다 `DeleteAllMessagesAsync`합니다. 처리에 영향을 주지 샘플의 구현 하지만 사용 하는 `Async` 비동기 메서드로 된다는 사실에 입각 호출 후 위 합니다.

[!code-csharp[Main](razor-pages-convention-features/sample/Pages/Index.cshtml.cs?name=snippet1&highlight=1,6,16,29)]

에 제공 된 처리기 이름을 확인 *Index.cshtml* 일치는 `DeleteAllMessages` 및 `DeleteMessageAsync` 처리기 메서드:

[!code-cshtml[Main](razor-pages-convention-features/sample/Pages/Index.cshtml?range=29-60&highlight=7-8,24-25)]

`Async`처리기 메서드 이름에 `DeleteMessageAsync` 는 축소 하 여 포함 된 `TryParseHandlerMethod` 처리기 메서드를 POST 요청의 일치에 대 한 합니다. `asp-page-handler` 이름 `DeleteMessage` 처리기 메서드에 일치 `DeleteMessageAsync`합니다.

## <a name="mvc-filters-and-the-page-filter-ipagefilter"></a>MVC 필터 및 페이지 필터 (IPageFilter)

MVC [작업 필터](xref:mvc/controllers/filters#action-filters) Razor 페이지 처리기 메서드를 사용 하므로 Razor 페이지에서 무시 됩니다. 다른 유형의 MVC 필터는 사용할 수 있습니다 사용할 수 있는: [권한 부여](xref:mvc/controllers/filters#authorization-filters), [예외](xref:mvc/controllers/filters#exception-filters), [리소스](xref:mvc/controllers/filters#resource-filters), 및 [결과](xref:mvc/controllers/filters#result-filters)합니다. 자세한 내용은 참조는 [필터](xref:mvc/controllers/filters) 항목입니다.

페이지 필터 ([IPageFilter](/dotnet/api/microsoft.aspnetcore.mvc.filters.ipagefilter)) Razor 페이지에 적용 되는 필터입니다. 주변 페이지 처리기 메서드를 실행 합니다. 처리기 메서드 실행 페이지의 단계에서 사용자 지정 코드를 처리할 수 있습니다. 샘플 응용 프로그램의 한 예는 다음과 같습니다.

[!code-csharp[Main](razor-pages-convention-features/sample/Filters/ReplaceRouteValueFilterAttribute.cs?name=snippet1)]

이 필터에 대 한 검사는 `globalTemplate` "ReplacementValue"에서 "TriggerValue" 및 교체의 값을 라우팅합니다.

`ReplaceRouteValueFilter` 특성에 직접 적용할 수 있습니다는 `PageModel` 코드 숨김에서:

[!code-csharp[Main](razor-pages-convention-features/sample/Pages/OtherPages/Page3.cshtml.cs?range=10-12&highlight=1)]

에 있는 샘플 응용 프로그램에서 요청 Page3 페이지 `localhost:5000/OtherPages/Page3/TriggerValue`합니다. 필터는 경로 값을 대체 하는 방법을 확인 합니다.

![경로 값을 ReplacementValue 바꿀 필터에서 TriggerValue 경로 세그먼트 결과로 OtherPages/Page3를 요청 합니다.](razor-pages-convention-features/_static/otherpages-page3-filter-replacement-value.png)

## <a name="see-also"></a>참고 항목

* [Razor 페이지 권한 부여 규칙](xref:security/authorization/razor-pages-authorization)
