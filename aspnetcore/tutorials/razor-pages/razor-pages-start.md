---
title: ASP.NET Core에서 Razor 페이지 시작
author: rick-anderson
monikerRange: '>= aspnetcore-2.2'
description: 이 자습서 시리즈는 ASP.NET Core에서 Razor Pages를 사용하는 방법을 보여 줍니다. 모델을 만들고, Razor Pages에 대한 코드를 생성하고, Entity Framework Core 및 SQL Server를 데이터 액세스에 사용하고, 검색 기능을 추가하고, 입력 유효성 검사를 추가하고, 마이그레이션을 사용하여 모델을 업데이트하는 방법을 알아봅니다.
ms.author: riande
ms.date: 12/5/2018
uid: tutorials/razor-pages/razor-pages-start
ms.openlocfilehash: 1152ebfcee48a46ecd28c941fce32d3fc1e05c41
ms.sourcegitcommit: 9bb58d7c8dad4bbd03419bcc183d027667fefa20
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/04/2018
ms.locfileid: "52861630"
---
# <a name="tutorial-get-started-with-razor-pages-in-aspnet-core"></a>자습서: ASP.NET Core에서 Razor Pages 시작

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)

이 자습서에서는 ASP.NET Core Razor 페이지 웹앱을 빌드하는 작업의 기본 사항을 설명합니다.

앱은 동영상 제목의 데이터베이스를 관리합니다. 다음과 같은 작업을 수행하는 방법을 살펴봅니다.

> [!div class="checklist"]
> * Razor Pages 웹앱 만들기
> * 모델 추가 및 스캐폴드
> * 데이터베이스 작업
> * 검색 및 유효성 검사 추가

작업을 완료하면 앱에서 동영상 제목 항목을 관리하고 표시할 수 있게 됩니다.

[!INCLUDE[](~/includes/rp/download.md)]

## <a name="prerequisites"></a>전제 조건

[!INCLUDE[](~/includes/net-core-prereqs-all-2.2.md)]

## <a name="create-a-razor-web-app"></a>Razor 웹앱 만들기

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

* Visual Studio **파일** 메뉴에서 **새로 만들기** > **프로젝트**를 선택합니다.
* 새 ASP.NET Core 웹 응용 프로그램을 만듭니다. 프로젝트 이름을 **RazorPagesMovie**로 지정합니다. 코드를 복사 후 붙여넣을 때 네임스페이스가 일치하도록 프로젝트 이름을 *RazorPagesMovie*로 지정해야 합니다.
 ![새 ASP.NET Core 웹 응용 프로그램](razor-pages-start/_static/np_2.1.png)

* 드롭다운에서 **ASP.NET Core 2.2**를 선택한 다음, **웹 애플리케이션**을 선택합니다.

  ![새 ASP.NET Core 웹 응용 프로그램](razor-pages-start/_static/np_2_2.2.png)

  다음 시작 프로젝트를 만듭니다.

  ![솔루션 탐색기](razor-pages-start/_static/se2.2.png)

* **Ctrl-F5** 키를 눌러서 디버거 없이 실행합니다.

  Visual Studio가 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)를 시작하고 앱을 실행합니다. 주소 표시줄에 `localhost:port#`이 표시되고 `example.com` 등은 표시되지 않습니다. `localhost`가 로컬 컴퓨터의 표준 호스트 이름이기 때문입니다. Localhost는 로컬 컴퓨터의 웹 요청만 지원합니다. Visual Studio에서 웹 프로젝트를 만들 경우 웹 서버에는 임의 포트가 사용됩니다. 이전 이미지에서 포트 번호는 5001입니다. 앱을 실행할 경우 다른 포트 번호가 표시됩니다.

  **Ctrl+F5**(디버그 이외 모드)를 사용하여 앱을 시작하면 코드를 변경하고, 파일을 저장하고, 브라우저를 새로 고치고, 코드 변경 내용을 확인할 수 있습니다. 대부분의 개발자는 페이지 및 보기 변경 내용을 새로 고치기 위해 디버그 이외 모드를 사용하려고 합니다.

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code)

* [통합 터미널](https://code.visualstudio.com/docs/editor/integrated-terminal)을 엽니다.
* 디렉터리(`cd`)를 프로젝트를 포함하는 폴더로 변경합니다.
* 다음 명령을 실행합니다.

   ```console
   dotnet new webapp -o RazorPagesMovie
   code -r RazorPagesMovie
   ```

  * 다음과 같은 대화 상자가 표시됩니다. **빌드 및 디버그에 필요한 자산이 'RazorPagesMovie'에서 누락되었습니다. 추가할까요?**  **예**를 선택합니다.

  * `dotnet new webapp -o RazorPagesMovie`: *RazorPagesMovie* 폴더에서 새 Razor Pages 프로젝트를 만듭니다.
  * `code -r RazorPagesMovie`: Visual Studio Code에서 *RazorPagesMovie.csproj* 프로젝트 파일을 로드합니다.

### <a name="launch-the-app"></a>앱 시작

* **Ctrl-F5** 키를 눌러서 디버거 없이 실행합니다.

  Visual Studio Code가 [Kestrel](xref:fundamentals/servers/kestrel)을 시작하고, 브라우저를 시작하고, `http://localhost:5001`로 이동합니다. 주소 표시줄에 `localhost:port:5001`이 표시되고 `example.com` 등은 표시되지 않습니다. 그 이유는 `localhost`가 로컬 컴퓨터의 표준 이름이기 때문입니다. Localhost는 로컬 컴퓨터의 웹 요청만 지원합니다.

  **Ctrl+F5**(디버그 이외 모드)를 사용하여 앱을 시작하면 코드를 변경하고, 파일을 저장하고, 브라우저를 새로 고치고, 코드 변경 내용을 확인할 수 있습니다. 대부분의 개발자는 페이지 및 보기 변경 내용을 새로 고치기 위해 디버그 이외 모드를 사용하려고 합니다.

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[Visual Studio for Mac](#tab/visual-studio-mac)

터미널에서 다음 명령을 실행합니다.

<!-- TODO: update these instruction once mac support 2.2 projects -->

```console
dotnet new webapp -o RazorPagesMovie
cd RazorPagesMovie
dotnet run
```

이전 명령은 [.NET Core CLI](/dotnet/core/tools/dotnet)를 사용하여 Razor 페이지 프로젝트를 만들고 실행합니다. 브라우저를 열고 http://localhost:5000으로 이동하여 응용 프로그램을 봅니다.

## <a name="open-the-project"></a>프로젝트 열기

Ctrl+C를 눌러 응용 프로그램을 종료합니다.

Visual Studio에서 **파일 > 열기**를 선택하고 *RazorPagesMovie.csproj* 파일을 선택합니다.

### <a name="launch-the-app"></a>앱 시작

**실행 > 디버깅하지 않고 시작**을 선택하여 앱을 시작합니다. Visual Studio가 [Kestrel](xref:fundamentals/servers/kestrel)을 시작하고, 브라우저를 시작하고, `http://localhost:5001`으로 이동합니다.

<!-- End of VS tabs -->

---

* **승인**을 선택하여 추적에 동의합니다. 이 앱은 개인 정보를 추적하지 않습니다. 템플릿 생성 코드는 [GDPR(일반 데이터 보호 규정)](xref:security/gdpr)을 충족할 수 있도록 자산을 포함합니다.

  ![홈 또는 인덱스 페이지](razor-pages-start/_static/homeGDPR2.2.png)

  다음 이미지에서는 추적을 승인한 후에 앱을 보여줍니다.

  ![홈 또는 인덱스 페이지](razor-pages-start/_static/home2.2.png)

## <a name="project-files-and-folders"></a>프로젝트 파일 및 폴더

다음 표에는 프로젝트의 파일 및 폴더가 나와 있습니다. 자습서의 이 시점에서 *Startup.cs* 파일을 이해하는 것이 가장 중요합니다. 아래 제공된 각 링크를 검토할 필요는 없습니다. 프로젝트의 파일이나 폴더에 대한 자세한 정보가 필요할 경우 링크가 참조로 제공됩니다.

| 파일 또는 폴더              | 용도 |
| ----------------- | ------------ |
| *wwwroot* | 정적 파일을 포함합니다. [고정 파일](xref:fundamentals/static-files)을 참조하세요. |
| *페이지* | [Razor 페이지](xref:razor-pages/index)에 대한 폴더입니다. |
| *appsettings.json* | [구성](xref:fundamentals/configuration/index) |
| *Program.cs* | ASP.NET Core 앱을 [호스트](xref:fundamentals/host/index)합니다.|
| *Startup.cs* | 서비스 및 요청 파이프라인을 구성합니다. [시작](xref:fundamentals/startup)을 참조하세요.|

### <a name="the-pages-folder"></a>Pages 폴더

*_Layout.cshtml* 파일은 공통적인 HTML 요소(스크립트 및 스타일시트)를 포함하고 응용 프로그램 레이아웃을 설정합니다. 예를 들어 **RazorPagesMovie**, **홈** 또는 **개인 정보**를 클릭하면 동일한 요소가 표시됩니다. 공통적인 요소에는 창 위쪽의 탐색 메뉴 및 아래쪽의 헤더가 포함됩니다. 자세한 내용은 [레이아웃](xref:mvc/views/layout)을 참조하세요.

*_ViewImports.cshtml* 파일에는 각 Razor 페이지로 가져온 Razor 지시문이 포함됩니다. 자세한 내용은 [공유된 지시문 가져오기](xref:mvc/views/layout#importing-shared-directives)를 참조하세요.

*_ViewStart.cshtml*은 Razor 페이지 `Layout` 속성을 설정하여 *_Layout.cshtml* 파일을 사용합니다. 자세한 내용은 [레이아웃](xref:mvc/views/layout)을 참조하세요.

*_ValidationScriptsPartial.cshtml* 파일은 [jQuery](https://jquery.com/) 유효성 검사 스크립트에 대한 참조를 제공합니다. 자습서의 뒷부분에서 `Create` 및 `Edit` 페이지를 추가하면 *_ValidationScriptsPartial.cshtml* 파일이 사용됩니다.

다음 작업에 `Index`, `Error` 및 `Privacy` 페이지가 제공됩니다.

* `Index`: 앱 시작
* `Error`: 오류 정보 표시
* `Privacy`: 사이트의 개인 정보 취급 방침에 대한 세부 정보 지정

이 자습서에서는 이전 페이지를 사용하지 않습니다.

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

<a name="f7"></a>
### <a name="use-f7-to-toggle-between-a-razor-page-and-the-pagemodel"></a>F7 키를 사용하여 Razor 페이지와 PageModel 간에 토글

F7 키를 사용하면 Razor Page(*\*.cshtml* 파일)와 C# 파일(*\*.cshtml.cs*)을 토글할 수 있습니다.

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code)

<!-- TODO review  Need something in these tabs -->

규칙에 따라 Razor Page(*\*.cshtml* 파일)와 연결된 `PageModel`에는 동일한 루트 파일 이름이 있습니다.

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[Visual Studio for Mac](#tab/visual-studio-mac)

규칙에 따라 Razor Page(*\*.cshtml* 파일)와 연결된 `PageModel`에는 동일한 루트 파일 이름이 있습니다.

---

> [!div class="step-by-step"]
> [다음: 모델 추가](xref:tutorials/razor-pages/model)