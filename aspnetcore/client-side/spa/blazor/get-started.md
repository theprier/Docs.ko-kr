---
title: Blazor 시작
author: guardrex
description: 만들고 Blazor 프로젝트를 수정 하 여 Blazor를 사용 하 여 시작 하는 방법에 알아봅니다.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 02/12/2019
uid: spa/blazor/get-started
ms.openlocfilehash: 667c57d536450fa2f8ae1cabc7c5a76a16d38a55
ms.sourcegitcommit: 191d21c1e37b56f0df0187e795d9a56388bbf4c7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2019
ms.locfileid: "57665589"
---
# <a name="get-started-with-blazor"></a>Blazor 시작

작성자: [Daniel Roth](https://github.com/danroth27) 및 [Luke Latham](https://github.com/guardrex)

[!INCLUDE[](~/includes/razor-components-preview-notice.md)]

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

필수 구성 요소:

[!INCLUDE[](~/includes/net-core-prereqs-vs-3.0.md)]

Visual Studio에서 첫 번째 Blazor 프로젝트를 만들려면:

1. 최신 설치 [Blazor 언어 서비스 확장](https://go.microsoft.com/fwlink/?linkid=870389) Visual Studio Marketplace에서. 이 단계에 게 Blazor 템플릿을 사용할 수 있는 Visual Studio입니다.
1. 명령 셸에서 다음 명령을 실행 하 여.NET Core CLI와 함께 사용할 Blazor 템플릿을 확인:

   ```console
   dotnet new -i Microsoft.AspNetCore.Blazor.Templates::0.9.0-preview3-19154-02
   ```

1. 선택 **파일** > **새 프로젝트** > **Web** > **ASP.NET Core 웹 응용 프로그램**합니다.
1. 했는지 **.NET Core** 하 고 **ASP.NET Core 3.0** 맨 위에 있는 선택 됩니다.
1. **Blazor** 템플릿을 선택하고 **확인**을 선택합니다.
1. **F5** 키를 눌러 앱을 실행합니다.

지금까지 지금까지 첫 번째 Blazor 앱을 실행 했습니다!

<!--

# [Visual Studio Code](#tab/visual-studio-code)

Prerequisites:

[!INCLUDE[](~/includes/net-core-prereqs-vsc-3.0.md)]

To create your first Blazor project in Visual Studio Code:

1. Execute the following command in a command shell:

   ```console
   dotnet new blazor -o WebApplication1
   ```

1. Open the *WebApplication1* folder in Visual Studio Code.

1. Visual Studio code offers to create assets to build and debug the app, which includes the *tasks.json* and *launch.json* files. Select **Yes** to add the assets.

1. Execute the app using the Visual Studio Code debugger.

1. In a browser, navigate to `https://localhost:5001`.

Congratulations! You just ran your first Blazor app!

# [Visual Studio for Mac](#tab/visual-studio-mac)

.NET Core 3.0 will be supported with Visual Studio for Mac version 8.0 or later. Visual Studio for Mac version 8.0 Preview isn't available at this time.

Use the [.NET Core CLI version of this topic](xref:razor-components/get-started?tabs=netcore-cli) on macOS.

[!INCLUDE[](~/includes/net-core-prereqs-mac-3.0.md)]

To create your first project Blazor project in Visual Studio for Mac:

1. Select **File** > **New Solution** or **New Project**.
1. In the sidebar, select **.NET Core** > **App**.
1. Select **Blazor** and select **Next**.
1. The **Target Framework** defaults to **.NET Core 3.0**. Select **Next**.
1. In the **Project Name** field, enter `WebApplication1`. Select **Create**.
1. Select **Run** > **Run Without Debugging** to run the app *without the debugger*. Running with the debugger isn't supported at this time.

Congratulations! You just ran your first Blazor app!
-->

# <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli/)

필수 구성 요소:

* [.NET core SDK 3.0 미리 보기](https://dotnet.microsoft.com/download/dotnet-core/3.0)

1. 명령 셸에서 다음 명령을 실행 하 여 Blazor 템플릿을 추가 합니다.

   ```console
   dotnet new -i Microsoft.AspNetCore.Blazor.Templates::0.9.0-preview3-19154-02
   ```

1. 명령 셸에서 첫 번째 Blazor 프로젝트를 만듭니다.

   ```console
   dotnet new blazor -o WebApplication1
   cd WebApplication1
   dotnet run
   ```

1. 브라우저에서 `https://localhost:5001`로 이동합니다.

지금까지 지금까지 첫 번째 Blazor 앱을 실행 했습니다!

---

## <a name="blazor-project"></a>Blazor 프로젝트

앱을 실행 하는 경우 여러 페이지 세로 막대의 탭에서 사용할 수 있습니다.

* 홈
* 카운터
* 데이터 가져오기

카운터 페이지에서 **Click me** 단추를 선택하여 페이지 새로 고침 없이 카운터를 증분합니다. 일반적으로 웹 페이지에서 카운터를 증가 하려면 JavaScript를 작성 해야 하지만 Blazor 사용 하 여 더 나은 접근 방식을 제공 C#입니다.

*Pages/Counter.cshtml*:

[!code-cshtml[](get-started/samples_snapshot/3.x/Counter1.cshtml)]

에 대 한 요청 `/counter` 에 지정 된 대로 브라우저에서을 `@page` 맨 위에 있는 지시문 하면 카운터 구성 요소를 해당 콘텐츠를 렌더링 합니다. 구성 요소는 메모리 내 표현을 유연 하 고 효율적인 방식으로 UI를 업데이트 하는 데 사용할 수 있는 렌더링 트리를 렌더링 합니다.

각 시간 합니다 **Click me** 단추를 선택 합니다.

* `onclick` 이벤트가 발생 합니다.
* `IncrementCount` 메서드가 호출됩니다.
* `currentCount` 증분됩니다.
* 구성 요소를 다시 렌더링 됩니다.

런타임에 이전 내용으로 새 콘텐츠를 비교 하 여 변경 된 내용이만 문서 개체 모델 (DOM)에 적용 됩니다.

HTML과 유사한 구문을 사용 하는 다른 구성 요소는 구성 요소를 추가 합니다. 구성 요소 매개 변수는 특성 또는 자식 콘텐츠를 사용 하 여 지정 됩니다. 예를 들어, 카운터 구성 요소 수에 추가할 앱의 홈 페이지를 추가 하 여를 `<Counter />` 요소 인덱스 구성 요소입니다.

*pages/Index.cshtml*, 카운터 구성 요소를 사용 하 여 설문 조사 프롬프트 구성 요소를 교체 합니다.

[!code-cshtml[](get-started/samples_snapshot/3.x/Index1.cshtml?highlight=7)]

앱을 실행합니다. 홈 페이지에는 자체 카운터가 있습니다.

매개 변수를 카운터 구성 요소를 추가 하려면 구성 요소의 업데이트 `@functions` 블록:

* 에 대 한 속성을 추가 `IncrementAmount` 데코 레이트 된 `[Parameter]` 특성입니다.
* `currentCount` 값을 늘릴 때 `IncrementAmount`를 사용하도록 `IncrementCount` 메서드를 변경합니다.

*Pages/Counter.cshtml*:

[!code-cshtml[](get-started/samples_snapshot/3.x/Counter2.cshtml?highlight=4,8)]

특성을 사용하여 Home 구성 요소의 `<Counter>` 요소에 `IncrementAmount` 매개 변수를 지정합니다.

*Pages/Index.cshtml*:

[!code-cshtml[](get-started/samples_snapshot/3.x/Index2.cshtml)]

앱을 실행합니다. 홈 페이지에는 각 시간을 10 씩 증가 하는 자체 카운터가 합니다 **Click me** 단추를 선택 합니다.

## <a name="next-steps"></a>다음 단계

<xref:tutorials/first-razor-components-app>
