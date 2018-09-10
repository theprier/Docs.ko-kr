---
title: ASP.NET Core의 영역
author: rick-anderson
description: 관련 기능을 별도의 네임스페이스(라우팅용) 및 폴더 구조(보기용)로 그룹화하는 데 사용되는 ASP.NET MVC 기능인 영역에 대해 알아봅니다.
ms.author: riande
ms.date: 02/14/2017
uid: mvc/controllers/areas
ms.openlocfilehash: b78bb5146f1ab9039fa9ff015471654510718ed6
ms.sourcegitcommit: ecf2cd4e0613569025b28e12de3baa21d86d4258
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43312220"
---
# <a name="areas-in-aspnet-core"></a>ASP.NET Core의 영역

작성자: [Dhananjay Kumar](https://twitter.com/debug_mode) 및 [Rick Anderson](https://twitter.com/RickAndMSFT)

영역은 관련 기능을 별도의 네임스페이스(라우팅용) 및 폴더 구조(뷰용)로 그룹화하는 데 사용되는 ASP.NET MVC 기능입니다. 영역을 사용하면 다른 경로 매개 변수 `area`를 `controller` 및 `action`에 추가하여 라우팅을 위한 계층 구조가 생성됩니다.

영역은 대규모 ASP.NET Core MVC 웹앱을 더 작은 기능 그룹으로 분할하는 방법을 제공합니다. 영역은 응용 프로그램 내에서 유효한 MVC 구조입니다. MVC 프로젝트에서 모델, 컨트롤러, 뷰와 같은 논리적 구성 요소는 서로 다른 폴더에 보관되며 MVC는 명명 규칙을 사용하여 이러한 구성 요소 간의 관계를 만듭니다. 대형 앱의 경우 앱을 별도의 고급 기능 영역으로 나누는 것이 좋습니다. 결제, 청구 및 검색 등과 같은 여러 비즈니스 단위가 있는 전자상거래 앱을 예로 들 수 있습니다. 이러한 각 단위에는 자체적인 논리 구성 요소 뷰, 컨트롤러 및 모델이 있습니다 이 시나리오에서는 영역을 사용하여 동일한 프로젝트에 있는 비즈니스 구성 요소를 물리적으로 파티션할 수 있습니다.

영역은 컨트롤러, 뷰 및 모델의 고유한 집합이 있는 ASP.NET Core MVC 프로젝트의 작은 기능 단위로 정의할 수 있습니다.

다음과 같은 경우 MVC 프로젝트에서 영역을 사용하는 것이 좋습니다.

* 응용 프로그램은 논리적으로 분리되어야 하는 여러 개의 고급 기능 구성 요소로 이루어져 있습니다.

* 각 기능 영역을 독립적으로 작업할 수 있도록 MVC 프로젝트를 파티션하려고 합니다.

영역 기능:

* ASP.NET Core MVC 앱은 원하는 수의 영역을 포함할 수 있습니다.

* 각 영역에는 고유한 컨트롤러, 모델 및 뷰가 있습니다.

* 영역을 사용하면 대규모 MVC 프로젝트를 독립적으로 작업할 수 있는 여러 개의 고급 구성 요소로 구성할 수 있습니다.

* 영역은 컨트롤러에 서로 다른 *영역*이 있는 한, 동일한 이름의 여러 컨트롤러를 지원합니다.

영역을 만들고 사용하는 방법을 보여주는 예를 살펴 보겠습니다. 컨트롤러와 뷰의 두 가지 구분된 그룹인 제품 및 서비스가 있는 스토어 앱이 있다고 가정해 보겠습니다. MVC 영역을 사용하는 일반적인 폴더 구조는 다음과 같습니다.

* 프로젝트 이름

  * 영역

    * 제품

      * 컨트롤러

        * HomeController.cs

        * ManageController.cs

      * 보기

        * 홈

          * Index.cshtml

        * 관리

          * Index.cshtml

    * 서비스

      * 컨트롤러

        * HomeController.cs

      * 보기

        * 홈

          * Index.cshtml

MVC가 영역에서 뷰를 렌더링하려고 할 때 기본적으로 다음 위치를 찾습니다.

```text
/Areas/<Area-Name>/Views/<Controller-Name>/<Action-Name>.cshtml
   /Areas/<Area-Name>/Views/Shared/<Action-Name>.cshtml
   /Views/Shared/<Action-Name>.cshtml
   ```

이 위치는 `Microsoft.AspNetCore.Mvc.Razor.RazorViewEngineOptions`의 `AreaViewLocationFormats`를 통해 변경할 수 있는 기본 위치입니다.

예를 들어 아래 코드에서는 폴더 이름을 'Areas'로 지정하는 대신 'Categories'로 변경했습니다.

```csharp
services.Configure<RazorViewEngineOptions>(options =>
   {
       options.AreaViewLocationFormats.Clear();
       options.AreaViewLocationFormats.Add("/Categories/{2}/Views/{1}/{0}.cshtml");
       options.AreaViewLocationFormats.Add("/Categories/{2}/Views/Shared/{0}.cshtml");
       options.AreaViewLocationFormats.Add("/Views/Shared/{0}.cshtml");
   });
   ```

한 가지 주의할 점은 *Views* 폴더의 구조만 중요하며 *Controllers* 및 *Models*와 같은 나머지 폴더의 내용은 중요하지 **않습니다**. 예를 들어 *Controllers* 및 *Models* 폴더는 필요하지 않습니다. *Controllers* 및 *Models*의 내용은 .dll로 컴파일된 코드일 뿐이기 때문이며, *Views*의 내용은 해당 뷰에 대한 요청이 이루어질 때까지 컴파일되지 않습니다.

폴더 계층 구조를 정의한 후에는 각 컨트롤러가 영역과 연결됨을 MVC에 알려야 합니다. 컨트롤러 이름을 `[Area]` 특성으로 데코레이팅하여 이 작업을 수행합니다.

```csharp
...
   namespace MyStore.Areas.Products.Controllers
   {
       [Area("Products")]
       public class HomeController : Controller
       {
           // GET: /Products/Home/Index
           public IActionResult Index()
           {
               return View();
           }

           // GET: /Products/Home/Create
           public IActionResult Create()
           {
               return View();
           }
       }
   }
   ```

새로 생성된 영역에서 작동하는 경로 정의를 설정합니다. [컨트롤러 작업으로 라우팅](routing.md) 아티클에서는 기존 경로 및 특성 경로를 사용하는 방법을 포함하여 경로 정의를 만드는 방법에 대해 자세히 설명합니다. 이 예에서는 기존 경로를 사용합니다. 이렇게 하려면 *Startup.cs* 파일을 열고 아래에 `areaRoute` 경로 정의를 추가하여 수정합니다.

```csharp
...
   app.UseMvc(routes =>
   {
     routes.MapRoute(
         name: "areaRoute",
         template: "{area:exists}/{controller=Home}/{action=Index}/{id?}");

     routes.MapRoute(
         name: "default",
         template: "{controller=Home}/{action=Index}/{id?}");
   });
   ```

`http://<yourApp>/products`으로 이동하면 `Products` 영역의 `HomeController`에 대한 `Index` 작업 메서드가 호출됩니다.

## <a name="link-generation"></a>링크 생성

* 영역 기반 컨트롤러 내의 작업에서 동일한 컨트롤러 내의 다른 작업으로의 링크를 생성합니다.

  현재 요청의 경로가 `/Products/Home/Create`와 같다고 가정해 보겠습니다.

  HtmlHelper 구문: `@Html.ActionLink("Go to Product's Home Page", "Index")`

  TagHelper 구문: `<a asp-action="Index">Go to Product's Home Page</a>`

  'area' 및 'controller' 값은 현재 요청의 컨텍스트에서 이미 사용할 수 있으므로 여기에 값을 제공할 필요는 없습니다. 이러한 종류의 값을 `ambient` 값이라고 합니다.

* 영역 기반 컨트롤러 내의 작업에서 다른 컨트롤러의 다른 작업으로의 링크 생성

  현재 요청의 경로가 `/Products/Home/Create`와 같다고 가정해 보겠습니다.

  HtmlHelper 구문: `@Html.ActionLink("Go to Manage Products Home Page", "Index", "Manage")`

  TagHelper 구문: `<a asp-controller="Manage" asp-action="Index">Go to Manage Products Home Page</a>`

  여기서 'area'의 앱비언트 값이 사용되지만 'controller' 값은 위에 명시적으로 지정됩니다.

* 영역 기반 컨트롤러 내의 작업에서 다른 컨트롤러 및 다른 영역의 다른 작업으로의 링크를 생성합니다.

  현재 요청의 경로가 `/Products/Home/Create`와 같다고 가정해 보겠습니다.

  HtmlHelper 구문: `@Html.ActionLink("Go to Services Home Page", "Index", "Home", new { area = "Services" })`

  TagHelper 구문: `<a asp-area="Services" asp-controller="Home" asp-action="Index">Go to Services Home Page</a>`

  여기서 앱비언트 값은 사용되지 않습니다.

* 영역 기반 컨트롤러 내의 작업에서 다른 컨트롤러 및 영역에 **없는** 다른 작업으로의 링크를 생성합니다.

  HtmlHelper 구문: `@Html.ActionLink("Go to Manage Products  Home Page", "Index", "Home", new { area = "" })`

  TagHelper 구문: `<a asp-area="" asp-controller="Manage" asp-action="Index">Go to Manage Products Home Page</a>`

  비-영역 기반 컨트롤러 작업에 대한 링크를 생성하고자 하므로 여기서 'area'에 대한 앱비언트 값을 비웁니다.

## <a name="publishing-areas"></a>영역 게시

`<Project Sdk="Microsoft.NET.Sdk.Web">`이 *.csproj* 파일에 포함되면 모든 `*.cshtml` 및 `wwwroot/**` 파일이 출력으로 게시됩니다.
