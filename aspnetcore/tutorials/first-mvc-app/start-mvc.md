---
title: ASP.NET Core MVC 및 Visual Studio 시작
author: rick-anderson
description: ASP.NET Core MVC 및 Visual Studio를 시작하는 방법을 배웁니다.
ms.author: riande
ms.date: 10/07/2017
uid: tutorials/first-mvc-app/start-mvc
ms.openlocfilehash: 738c49272c2ae2b075866001f06ad09fe73969f9
ms.sourcegitcommit: 9bb58d7c8dad4bbd03419bcc183d027667fefa20
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/04/2018
ms.locfileid: "52862202"
---
# <a name="get-started-with-aspnet-core-mvc-and-visual-studio"></a>ASP.NET Core MVC 및 Visual Studio 시작

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

이 자습서는 세 가지 버전이 있습니다.

* macOS: [Mac용 Visual Studio를 사용하여 ASP.NET Core MVC 앱 만들기](xref:tutorials/first-mvc-app-mac/start-mvc)
* Windows: [Visual Studio를 사용하여 ASP.NET Core MVC 앱 만들기](xref:tutorials/first-mvc-app/start-mvc)
* macOS, Linux 및 Windows: [Visual Studio Code를 사용하여 ASP.NET Core MVC 앱 만들기](xref:tutorials/first-mvc-app-xplat/start-mvc)

> [!NOTE]
> ASP.NET Core 목차에 대해 제안된 새 구조의 유용성을 테스트합니다.  몇 분 동안 현재 또는 제안된 목차에서 다른 7개의 항목을 찾는 연습을 수행하는 경우 [여기를 클릭하여 연구에 참여하세요](https://dpk4xbh5.optimalworkshop.com/treejack/aa11wn82).

## <a name="install-visual-studio-and-net-core"></a>Visual Studio 및 .NET Core 설치

::: moniker range=">= aspnetcore-2.1"

[!INCLUDE [](~/includes/net-core-prereqs-windows.md)]

## <a name="create-a-web-app"></a>웹앱 만들기

Visual Studio에서 **파일 > 새로 만들기 > 프로젝트**를 선택합니다.

![파일 > 새로 만들기 > 프로젝트](start-mvc/_static/alt_new_project.png)

**새 프로젝트** 대화 상자를 완료합니다.

* 왼쪽 창에서 **.NET Core**를 탭합니다.
* 가운데 창에서 **ASP.NET Core 웹 응용 프로그램(.NET Core)** 을 탭합니다.
* 프로젝트 이름을 “MvcMovie”로 지정합니다(코드를 복사할 때 네임스페이스가 일치하도록 프로젝트 이름을 “MvcMovie”로 지정해야 함).
* **확인**을 탭합니다.

![새 프로젝트 대화 상자, 왼쪽 창의 .Net core, ASP.NET Core 웹 ](start-mvc/_static/new_project2-21.png)

**새 ASP.NET Core 웹 응용 프로그램(.NET Core) - MvcMovie** 대화 상자를 완료합니다.

* 버전 선택기 드롭다운 상자에서 **ASP.NET Core 2.1**을 선택합니다.
* **웹 응용 프로그램(모델-뷰-컨트롤러)** 을 선택합니다.
* **확인**을 탭합니다.

![새 프로젝트 대화 상자, 왼쪽 창의 .Net core, ASP.NET Core 웹 ](start-mvc/_static/new_project22-21.png)

Visual Studio에서는 방금 만든 MVC 프로젝트에 대한 기본 템플릿을 사용했습니다. 프로젝트 이름을 입력하고 몇 가지 옵션을 선택하면 바로 앱이 작동합니다. 다음은 기본 시작 프로젝트이며 여기서 시작하는 것이 좋습니다.

**F5** 키를 탭하여 앱을 디버그 모드에서 실행하거나 **Ctrl-F5**를 탭하여 디버그 이외 모드에서 실행합니다.
<!-- These images are also used by uid: tutorials/first-mvc-app-xplat/start-mvc -->
![앱 실행](start-mvc/_static/1.png)

* Visual Studio가 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)를 시작하고 앱을 실행합니다. 주소 표시줄에 `localhost:port#`이 표시되고 `example.com` 등은 표시되지 않음을 알 수 있습니다. 그 이유는 `localhost`가 로컬 컴퓨터의 표준 이름이기 때문입니다. Visual Studio에서 웹 프로젝트를 만들 경우 웹 서버에는 임의 포트가 사용됩니다. 위 이미지에서 포트 번호는 5000입니다. 브라우저의 URL에는 `localhost:5000`이 표시됩니다. 앱을 실행할 경우 다른 포트 번호가 표시됩니다.
* **Ctrl+F5**(디버그 이외 모드)를 사용하여 앱을 시작하면 코드를 변경하고, 파일을 저장하고, 브라우저를 새로 고치고, 코드 변경 내용을 확인할 수 있습니다. 대부분의 개발자는 앱을 빠르게 시작하고 변경 내용을 확인하기 위해 디버그 이외 모드를 사용하려고 합니다.
* **디버그** 메뉴 항목에서 앱을 디버그 또는 디버그 이외 모드로 시작할 수 있습니다.

![디버그 메뉴](start-mvc/_static/debug_menu.png)

* **IIS Express** 단추를 탭하여 앱을 디버그할 수 있습니다.

![IIS Express](start-mvc/_static/iis_express.png)

기본 템플릿은 작동하는 **홈, 정보** 및 **연락처** 링크를 제공합니다. 위의 브라우저 이미지에는 이러한 링크가 표시되지 않습니다. 브라우저 크기에 따라 탐색 아이콘을 클릭하여 링크를 표시해야 할 수 있습니다.

![오른쪽 위의 탐색 아이콘](start-mvc/_static/2.png)

디버그 모드에서 실행 중인 경우 **Shift-F5**를 탭하여 디버깅을 중지합니다.

이 자습서의 다음 부분에서는 MVC에 대해 알아보고 일부 코드 작성을 시작합니다.

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!INCLUDE [](~/includes/net-core-prereqs.md)]

## <a name="create-a-web-app"></a>웹앱 만들기

Visual Studio에서 **파일 > 새로 만들기 > 프로젝트**를 선택합니다.

![파일 > 새로 만들기 > 프로젝트](start-mvc/_static/alt_new_project.png)

**새 프로젝트** 대화 상자를 완료합니다.

* 왼쪽 창에서 **.NET Core**를 탭합니다.
* 가운데 창에서 **ASP.NET Core 웹 응용 프로그램(.NET Core)** 을 탭합니다.
* 프로젝트 이름을 “MvcMovie”로 지정합니다(코드를 복사할 때 네임스페이스가 일치하도록 프로젝트 이름을 “MvcMovie”로 지정해야 함).
* **확인**을 탭합니다.

![새 프로젝트 대화 상자, 왼쪽 창의 .Net core, ASP.NET Core 웹 ](start-mvc/_static/new_project2.png)

**새 ASP.NET Core 웹 응용 프로그램(.NET Core) - MvcMovie** 대화 상자를 완료합니다.

* 버전 선택기 드롭다운 상자에서 **ASP.NET Core 2.-** 를 선택합니다.
* **웹 응용 프로그램(모델-보기-컨트롤러)** 을 선택합니다.
* **확인**을 탭합니다.

![새 프로젝트 대화 상자, 왼쪽 창의 .Net core, ASP.NET Core 웹 ](start-mvc/_static/new_project22.png)

Visual Studio에서는 방금 만든 MVC 프로젝트에 대한 기본 템플릿을 사용했습니다. 프로젝트 이름을 입력하고 몇 가지 옵션을 선택하면 바로 앱이 작동합니다. 다음은 기본 시작 프로젝트이며 여기서 시작하는 것이 좋습니다.

**F5** 키를 탭하여 앱을 디버그 모드에서 실행하거나 **Ctrl-F5**를 탭하여 디버그 이외 모드에서 실행합니다.
<!-- These images are also used by uid: tutorials/first-mvc-app-xplat/start-mvc -->
![앱 실행](start-mvc/_static/1.png)

* Visual Studio가 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)를 시작하고 앱을 실행합니다. 주소 표시줄에 `localhost:port#`이 표시되고 `example.com` 등은 표시되지 않음을 알 수 있습니다. 그 이유는 `localhost`가 로컬 컴퓨터의 표준 이름이기 때문입니다. Visual Studio에서 웹 프로젝트를 만들 경우 웹 서버에는 임의 포트가 사용됩니다. 위 이미지에서 포트 번호는 5000입니다. 브라우저의 URL에는 `localhost:5000`이 표시됩니다. 앱을 실행할 경우 다른 포트 번호가 표시됩니다.
* **Ctrl+F5**(디버그 이외 모드)를 사용하여 앱을 시작하면 코드를 변경하고, 파일을 저장하고, 브라우저를 새로 고치고, 코드 변경 내용을 확인할 수 있습니다. 대부분의 개발자는 앱을 빠르게 시작하고 변경 내용을 확인하기 위해 디버그 이외 모드를 사용하려고 합니다.
* **디버그** 메뉴 항목에서 앱을 디버그 또는 디버그 이외 모드로 시작할 수 있습니다.

![디버그 메뉴](start-mvc/_static/debug_menu.png)

* **IIS Express** 단추를 탭하여 앱을 디버그할 수 있습니다.

![IIS Express](start-mvc/_static/iis_express.png)

기본 템플릿은 작동하는 **홈, 정보** 및 **연락처** 링크를 제공합니다. 위의 브라우저 이미지에는 이러한 링크가 표시되지 않습니다. 브라우저 크기에 따라 탐색 아이콘을 클릭하여 링크를 표시해야 할 수 있습니다.

![오른쪽 위의 탐색 아이콘](start-mvc/_static/2.png)

디버그 모드에서 실행 중인 경우 **Shift-F5**를 탭하여 디버깅을 중지합니다.

이 자습서의 다음 부분에서는 MVC에 대해 알아보고 일부 코드 작성을 시작합니다.

::: moniker-end

> [!div class="step-by-step"]
> [다음](adding-controller.md)  
