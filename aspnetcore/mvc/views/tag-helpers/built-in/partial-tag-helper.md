---
title: ASP.NET Core의 부분 태그 도우미
author: scottaddie
description: ASP.NET Core 부분 태그 도우미와 부분 보기를 렌더링할 때 각 특성이 수행하는 역할을 알아봅니다.
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: scaddie
ms.custom: mvc
ms.date: 04/13/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: mvc/views/tag-helpers/builtin-th/partial-tag-helper
ms.openlocfilehash: 670663b963f4207da793afff44d55b85ba58b7f8
ms.sourcegitcommit: c79fd3592f444d58e17518914f8873d0a11219c0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="partial-tag-helper-in-aspnet-core"></a>ASP.NET Core의 부분 태그 도우미

작성자: [Scott Addie](https://github.com/scottaddie)

[!INCLUDE [2.1 preview notice](~/includes/2.1.md)]

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/tag-helpers/built-in/samples)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

## <a name="overview"></a>개요

부분 태그 도우미는 Razor 페이지 및 MVC 앱에서 [부분 보기](xref:mvc/views/partial)를 렌더링하는 데 사용됩니다. 고려 사항:

* ASP.NET Core 2.1 이상이 필요합니다.
* [HTML 도우미 구문](xref:mvc/views/partial#referencing-a-partial-view) 대신 사용할 수 있습니다.
* 부분 보기를 비동기적으로 렌더링합니다.

부분 보기 렌더링을 위한 HTML 도우미 옵션은 다음과 같습니다.

* [@await Html.PartialAsync](/dotnet/api/microsoft.aspnetcore.mvc.rendering.htmlhelperpartialextensions.partialasync)
* [@await Html.RenderPartialAsync](/dotnet/api/microsoft.aspnetcore.mvc.rendering.htmlhelperpartialextensions.renderpartialasync)
* [@Html.Partial](/dotnet/api/microsoft.aspnetcore.mvc.rendering.htmlhelperpartialextensions.partial)
* [@Html.RenderPartial](/dotnet/api/microsoft.aspnetcore.mvc.rendering.htmlhelperpartialextensions.renderpartial)

*제품* 모델은 이 문서 전반의 샘플에서 사용됩니다.

[!code-csharp[](samples/TagHelpersBuiltIn/Models/Product.cs)]

부분 태그 도우미 특성의 인벤토리는 다음과 같습니다.

## <a name="name"></a>name

`name` 특성이 필요합니다. 렌더링할 부분 보기의 이름 또는 경로를 나타냅니다. 부분 보기 이름이 제공되는 경우 [보기 검색](xref:mvc/views/overview#view-discovery) 프로세스가 시작됩니다. 해당 프로세스는 명시적 경로가 제공될 때 우회됩니다.

다음 표시에서는 명시적 경로를 사용하여 *_ProductPartial.cshtml*이 *공유* 폴더에서 로드됨을 나타냅니다. [for](#for) 특성을 사용하면 모델이 바인딩을 위해 부분 보기에 전달됩니다.

[!code-cshtml[](samples/TagHelpersBuiltIn/Pages/Product.cshtml?name=snippet_Name)]

## <a name="for"></a>for

`for` 특성은 현재 모델과 비교 평가할 [ModelExpression](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.modelexpression)을 할당합니다. `ModelExpression`은 `@Model.` 구문을 유추합니다. 예를 들어 `for="@Model.Product"` 대신 `for="Product"`를 사용할 수 있습니다. 이 기본 유추 동작은 인라인 식을 정의하는 `@` 기호를 사용하여 재정의됩니다. `for` 특성은 [모델](#model) 특성과 함께 사용할 수 없습니다.

다음 표시는 *_ProductPartial.cshtml*을 로드합니다.

[!code-cshtml[](samples/TagHelpersBuiltIn/Pages/Product.cshtml?name=snippet_For)]

부분 보기는 연결된 페이지 모델의 `Product` 속성에 바인딩됩니다.

[!code-csharp[](samples/TagHelpersBuiltIn/Pages/Product.cshtml.cs?highlight=8)]

## <a name="model"></a>모델

`model` 특성은 부분 보기에 전달할 모델 인스턴스를 할당합니다. `model` 특성은 [for](#for) 특성과 함께 사용할 수 없습니다.

다음 표시에서는 새 `Product` 개체가 인스턴스화되고 바인딩을 위해 `model` 특성에 전달됩니다.

[!code-cshtml[](samples/TagHelpersBuiltIn/Pages/Product.cshtml?name=snippet_Model)]

## <a name="view-data"></a>view-data

`view-data` 특성은 부분 보기에 전달할 [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary)를 할당합니다. 다음 표시를 사용하면 부분 보기에서 전체 ViewData 컬렉션에 액세스할 수 있습니다.

[!code-cshtml[](samples/TagHelpersBuiltIn/Pages/Product.cshtml?name=snippet_ViewData&highlight=5-)]

위의 코드에서 `IsNumberReadOnly` 키 값은 `true`로 설정되고 ViewData 컬렉션에 추가됩니다. 따라서 `ViewData["IsNumberReadOnly"]`는 다음 부분 보기 내에서 액세스할 수 있습니다.

[!code-cshtml[](samples/TagHelpersBuiltIn/Pages/Shared/_ProductViewDataPartial.cshtml?highlight=5)]

이 예제에서 `ViewData["IsNumberReadOnly"]` 값은 *번호* 필드가 읽기 전용으로 표시되는지를 결정합니다.

## <a name="additional-resources"></a>추가 자료

* [부분 뷰](xref:mvc/views/partial)
* [약한 형식의 데이터(ViewData 및 ViewBag)](xref:mvc/views/overview#weakly-typed-data-viewdata-and-viewbag)
