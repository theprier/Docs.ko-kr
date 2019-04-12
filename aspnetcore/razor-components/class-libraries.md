---
title: Razor 구성 요소 클래스 라이브러리
author: guardrex
description: 외부 구성 요소 라이브러리에서 구성 요소 Razor 앱에 구성 요소를 포함할 수 있습니다 하는 방법을 알아봅니다.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 03/14/2019
uid: razor-components/class-libraries
ms.openlocfilehash: 1064ad60d90af15af483ba9bca5ed85fb63c2924
ms.sourcegitcommit: 10e14b85490f064395e9b2f423d21e3c2d39ed8b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2019
ms.locfileid: "59515589"
---
# <a name="razor-components-class-libraries"></a>Razor 구성 요소 클래스 라이브러리

[Simon Timms](https://github.com/stimms)

구성 요소는 Razor 클래스 라이브러리의 프로젝트 간에 공유할 수 있습니다. 구성 요소를 포함할 수 있습니다.

* 솔루션의 다른 프로젝트입니다.
* NuGet 패키지입니다.
* 참조 된.NET 라이브러리입니다.

구성 요소는 일반.NET 형식 처럼 Razor 클래스 라이브러리에서 제공 하는 구성 요소는 일반.NET 어셈블리입니다.

사용 된 `razorclasslib` (Razor 클래스 라이브러리) 템플릿을 사용 하 여 합니다 [새 dotnet](/dotnet/core/tools/dotnet-new) 명령:

```console
dotnet new razorclasslib -o MyComponentLib1
```

추가 구성 요소 Razor 파일 (*.razor*)는 Razor 클래스 라이브러리입니다.

기존 프로젝트에 라이브러리를 추가 하려면 사용 합니다 [dotnet sln](/dotnet/core/tools/dotnet-sln) 명령:

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

```console
dotnet sln add .\MyComponentLib1
```

# <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli)

```console
dotnet add WebApplication1 reference MyComponentLib1
```

---

> [!NOTE]
> Razor 클래스 라이브러리는 ASP.NET Core 미리 보기 3에서 Blazor 앱과 호환 되지 않습니다.
>
> 만들어진 Blazor 클래스 라이브러리를 사용 하 여 Blazor 및 Razor 구성 요소 앱과 공유할 수 있는 라이브러리의 구성 요소를 만들려면는 `blazorlib` 템플릿.
>
> Razor 클래스 라이브러리는 ASP.NET Core 미리 보기 3의 정적 자산을 지원 하지 않습니다. 구성 요소 라이브러리를 사용 하 여 `blazorlib` 템플릿 이미지, JavaScript 및 스타일 시트 같은 정적 파일을 포함할 수 있습니다. 빌드 시 정적 파일은 빌드된 어셈블리 파일에 포함 됩니다 (*.dll*), 해당 리소스를 포함 하는 방법에 걱정할 필요 없이 구성 요소 사용을 허용 하는 합니다. 에 포함 된 모든 파일을 `content` 디렉터리 포함 리소스로 표시 됩니다.

## <a name="consume-a-library-component"></a>라이브러리 구성 요소를 사용 합니다.

다른 프로젝트에 라이브러리에 정의 된 구성 요소를 사용 하기 위해 합니다 [ @addTagHelper ](xref:mvc/views/tag-helpers/intro#add-helper-label) 지시문을 사용 해야 합니다. 개별 구성 요소 이름으로 추가할 수 있습니다.

지시문의 일반 형식은 다음과 같습니다.

```cshtml
@addTagHelper MyComponentLib1.Component1, MyComponentLib1

<h1>Hello, world!</h1>

Welcome to your new app.

<Component1 />
```

예를 들어 다음 지시문 추가 `Component1` 의 `MyComponentLib1`:

```cshtml
@addTagHelper MyComponentLib1.Component1, MyComponentLib1
```

그러나는 것이 일반적 모든 와일드 카드를 사용 하 여 어셈블리에서 구성 요소를 포함 하도록 (`*`):

```cshtml
@addTagHelper *, MyComponentLib1
```

합니다 `@addTagHelper` 지시문에 포함할 수 있습니다 *_ViewImport.cshtml* 단일 페이지 또는 폴더 내의 페이지 집합에 적용 된 또는 전체 프로젝트에 사용할 수 있는 구성 요소를 확인 합니다. 사용 하 여는 `@addTagHelper` 지시문 내부에 구성 요소 라이브러리의 구성 요소 사용 될 수 있습니다 앱과 동일한 어셈블리에 있는 것 처럼 합니다.

## <a name="build-pack-and-ship-to-nuget"></a>빌드, 팩 및 NuGet에 배송

구성 요소 라이브러리는 표준.NET 라이브러리 이기 때문에 패키징 및 NuGet에 패키징 및 nuget 라이브러리 전달 다르지 않습니다. 패키징을 사용 하 여 수행 되는 [dotnet 팩](/dotnet/core/tools/dotnet-pack) 명령:

```console
dotnet pack
```

사용 하는 NuGet 패키지를 업로드 합니다 [dotnet nuget](/dotnet/core/tools/dotnet-nuget-push) 명령:

```console
dotnet nuget publish
```

사용 하는 경우는 `blazorlib` 템플릿, 정적 리소스는 NuGet 패키지에 포함 됩니다. 라이브러리 소비자에 게 자동으로 수신 스크립트 및 스타일 시트 되므로 소비자가 리소스를 수동으로 설치할 필요가 없습니다.
