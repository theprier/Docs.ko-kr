---
title: Visual Studio Code에서 ASP.NET Core Razor 페이지 시작
author: rick-anderson
description: Visual Studio Code를 사용하여 ASP.NET Core Razor 페이지 웹앱을 빌드하는 방법에 대한 기본 사항을 배웁니다.
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.custom: mvc
ms.date: 10/24/2018
uid: tutorials/razor-pages-vsc/razor-pages-start
ms.openlocfilehash: 9ea66134c524a6a1a670d55bae4e66cf38a45274
ms.sourcegitcommit: 4d74644f11e0dac52b4510048490ae731c691496
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50089854"
---
# <a name="get-started-with-aspnet-core-razor-pages-in-visual-studio-code"></a>Visual Studio Code에서 ASP.NET Core Razor 페이지 시작

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)

이 자습서에서는 ASP.NET Core Razor 페이지 웹앱을 빌드하는 작업의 기본 사항을 설명합니다. 이 자습서를 시작하기 전에 [Razor 페이지 소개](xref:razor-pages/index)를 완료하는 것이 좋습니다. Razor 페이지는 ASP.NET Core에서 웹 응용 프로그램 UI를 빌드하는 좋은 방법입니다.

## <a name="prerequisites"></a>전제 조건

[!INCLUDE [](~/includes/net-core-prereqs-vscode.md)]

## <a name="create-a-razor-web-app"></a>Razor 웹앱 만들기

터미널에서 다음 명령을 실행합니다.

::: moniker range=">= aspnetcore-2.1"

```console
dotnet new webapp -o RazorPagesMovie
cd RazorPagesMovie
dotnet run
```

::: moniker-end

::: moniker range="= aspnetcore-2.0"

```console
dotnet new razor -o RazorPagesMovie
cd RazorPagesMovie
dotnet run
```

::: moniker-end

이전 명령은 [.NET Core CLI](/dotnet/core/tools/dotnet)를 사용하여 Razor 페이지 프로젝트를 만들고 실행합니다. 브라우저를 열고 http://localhost:5000으로 이동하여 응용 프로그램을 봅니다.

![홈 또는 인덱스 페이지](../razor-pages/razor-pages-start/_static/home.png)

[!INCLUDE [razor-pages-start](../../includes/RP/razor-pages-start.md)]

## <a name="open-the-project"></a>프로젝트 열기

Ctrl+C를 눌러 응용 프로그램을 종료합니다.

VS Code(Visual Studio Code)에서 **파일 > 폴더 열기**를 선택하고 *RazorPagesMovie* 폴더를 선택합니다.

- 다음 **경고** 메시지에 대해 **예**를 선택합니다. “빌드 및 디버그에 필요한 자산이 ‘RazorPagesMovie’에서 누락되었습니다. 추가할까요?”
- 다음 **정보** 메시지에 대해 **복원**을 선택합니다. “확인되지 않은 종속성이 있습니다.”

### <a name="launch-the-app"></a>앱 시작

Ctrl+F5를 눌러 디버깅 없이 앱을 시작합니다. 또는 **디버그** 메뉴에서 **디버깅하지 않고 시작**을 선택합니다.

다음 자습서에서는 프로젝트에 모델을 추가합니다. 

> [!div class="step-by-step"]
> [다음: 모델 추가](xref:tutorials/razor-pages-vsc/model)  
