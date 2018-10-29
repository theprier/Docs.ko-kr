---
title: ASP.NET Core에서 Razor 페이지 시작
author: rick-anderson
description: 이 자습서 시리즈는 ASP.NET Core에서 Razor Pages를 사용하는 방법을 보여 줍니다. 모델을 만들고, Razor Pages에 대한 코드를 생성하고, Entity Framework Core 및 SQL Server를 데이터 액세스에 사용하고, 검색 기능을 추가하고, 입력 유효성 검사를 추가하고, 마이그레이션을 사용하여 모델을 업데이트하는 방법을 알아봅니다.
ms.author: riande
ms.date: 05/30/2018
uid: tutorials/razor-pages/razor-pages-start
ms.openlocfilehash: 4ee9a014114e2536f7584b2a1ff9d699fb971aa8
ms.sourcegitcommit: 375e9a67f5e1f7b0faaa056b4b46294cc70f55b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50206980"
---
# <a name="tutorial-get-started-with-razor-pages-in-aspnet-core"></a>자습서: ASP.NET Core에서 Razor Pages 시작

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)

::: moniker range="= aspnetcore-2.0"

이 자습서의 ASP.NET Core 2.1 버전을 따르는 것이 좋습니다. 더 많은 기능을 수행하고 다루기가 **훨씬** 쉽습니다. 버전 선택기에서 **ASP.NET Core 2.1**을 선택합니다.

![TOC의 버전 선택기](razor-pages-start/_static/v21.png)

::: moniker-end

이 자습서에서는 ASP.NET Core Razor 페이지 웹앱을 빌드하는 작업의 기본 사항을 설명합니다. Razor 페이지는 ASP.NET Core에서 웹앱 UI를 빌드하는 좋은 방법입니다.

이 자습서는 다음 세 가지 버전으로 제공됩니다.

* Windows: 이 자습서
* MacOS: [Mac용 Visual Studio로 Razor 페이지 시작](xref:tutorials/razor-pages-mac/razor-pages-start)
* macOS, Linux 및 Windows: [Visual Studio Code에서 ASP.NET Core Razor 페이지 시작](xref:tutorials/razor-pages-vsc/razor-pages-start)

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample)([다운로드 방법](xref:index#how-to-download-a-sample))

::: moniker range=">= aspnetcore-2.1"

## <a name="prerequisites"></a>전제 조건

[!INCLUDE [Prerequisites](~/includes/net-core-prereqs-windows.md)]

## <a name="create-a-razor-web-app"></a>Razor 웹앱 만들기

* Visual Studio **파일** 메뉴에서 **새로 만들기** > **프로젝트**를 선택합니다.
* 새 ASP.NET Core 웹 응용 프로그램을 만듭니다. 프로젝트 이름을 **RazorPagesMovie**로 지정합니다. 코드를 복사 후 붙여넣을 때 네임스페이스가 일치하도록 프로젝트 이름을 *RazorPagesMovie*로 지정해야 합니다.
 ![새 ASP.NET Core 웹 응용 프로그램](razor-pages-start/_static/np_2.1.png)
* 드롭다운에서 **ASP.NET Core 2.1**을 선택한 다음, **웹 응용 프로그램**을 선택합니다.

 ![새 ASP.NET Core 웹 응용 프로그램](razor-pages-start/_static/np_2_2.1.png)

Visual Studio 템플릿은 시작 프로젝트를 만듭니다.

![솔루션 탐색기](razor-pages-start/_static/se2.1.png)

**F5** 키를 눌러 디버그 모드에서 앱을 실행하거나 **Ctrl-F5** 키를 눌러 디버거를 연결하지 않고 실행합니다. **승인**을 선택하여 추적에 동의합니다. 이 앱은 개인 정보를 추적하지 않습니다. 템플릿 생성 코드는 [GDPR(일반 데이터 보호 규정)](xref:security/gdpr)을 충족할 수 있도록 자산을 포함합니다.

![홈 또는 인덱스 페이지](razor-pages-start/_static/homeGDPR.png)

다음 이미지에서는 추적을 승인한 후에 앱을 보여줍니다.

![홈 또는 인덱스 페이지](razor-pages-start/_static/home2.1.png)

* Visual Studio가 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)를 시작하고 앱을 실행합니다. 주소 표시줄에 `localhost:port#`이 표시되고 `example.com` 등은 표시되지 않습니다. 그 이유는 `localhost`가 로컬 컴퓨터의 표준 이름이기 때문입니다. Localhost는 로컬 컴퓨터의 웹 요청만 지원합니다. Visual Studio에서 웹 프로젝트를 만들 경우 웹 서버에는 임의 포트가 사용됩니다. 이전 이미지에서 포트 번호는 5001입니다. 앱을 실행할 경우 다른 포트 번호가 표시됩니다.
* **Ctrl+F5**(디버그 이외 모드)를 사용하여 앱을 시작하면 코드를 변경하고, 파일을 저장하고, 브라우저를 새로 고치고, 코드 변경 내용을 확인할 수 있습니다. 대부분의 개발자는 앱을 빠르게 시작하고 변경 내용을 확인하기 위해 디버그 이외 모드를 사용하려고 합니다.

[!INCLUDE [razor-pages-start](~/includes/RP/2.1/razor-pages-start.md)]

[!INCLUDE [F7](~/includes/RP/F7.md)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

## <a name="prerequisites"></a>전제 조건

[!INCLUDE [Prerequisites](~/includes/net-core-prereqs-windows.md)]

## <a name="create-a-razor-web-app"></a>Razor 웹앱 만들기

* Visual Studio **파일** 메뉴에서 **새로 만들기** > **프로젝트**를 선택합니다.
* 새 ASP.NET Core 웹 응용 프로그램을 만듭니다. 프로젝트 이름을 **RazorPagesMovie**로 지정합니다. 코드를 복사 후 붙여넣을 때 네임스페이스가 일치하도록 프로젝트 이름을 *RazorPagesMovie*로 지정해야 합니다.
  ![새 ASP.NET Core 웹 응용 프로그램](../../razor-pages/index/_static/np.png)
* 드롭다운에서 **ASP.NET Core 2.0**을 선택하고 **웹 응용 프로그램**을 선택합니다.

  [!INCLUDE [install 2.0](~/includes/dotnetcore-on-dotnetfx-vs.md)]

Visual Studio 템플릿은 시작 프로젝트를 만듭니다.

![솔루션 탐색기](razor-pages-start/_static/se.png)

**F5** 키를 눌러 디버그 모드에서 앱을 실행하거나 **Ctrl-F5**를 눌러 디버거를 연결하지 않고 실행합니다.

![홈 또는 인덱스 페이지](razor-pages-start/_static/home.png)

* Visual Studio가 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)를 시작하고 앱을 실행합니다. 주소 표시줄에 `localhost:port#`이 표시되고 `example.com` 등은 표시되지 않습니다. 그 이유는 `localhost`가 로컬 컴퓨터의 표준 이름이기 때문입니다. Localhost는 로컬 컴퓨터의 웹 요청만 지원합니다. Visual Studio에서 웹 프로젝트를 만들 경우 웹 서버에는 임의 포트가 사용됩니다. 이전 이미지에서 포트 번호는 5000입니다. 앱을 실행할 경우 다른 포트 번호가 표시됩니다.
* **Ctrl+F5**(디버그 이외 모드)를 사용하여 앱을 시작하면 코드를 변경하고, 파일을 저장하고, 브라우저를 새로 고치고, 코드 변경 내용을 확인할 수 있습니다. 대부분의 개발자는 앱을 빠르게 시작하고 변경 내용을 확인하기 위해 디버그 이외 모드를 사용하려고 합니다.

[!INCLUDE [razor-pages-start](~/includes/RP/razor-pages-start.md)]

::: moniker-end

> [!div class="step-by-step"]
> [다음: 모델 추가](xref:tutorials/razor-pages/model)
