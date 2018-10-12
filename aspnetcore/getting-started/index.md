---
title: ASP.NET Core 시작
author: rick-anderson
description: ASP.NET Core를 사용하여 간단한 Hello World 앱을 만들고 실행하는 빠른 자습서입니다.
ms.author: riande
ms.custom: mvc
ms.date: 05/31/2018
uid: getting-started
ms.openlocfilehash: a6a5023594aec01370143e7d1f35fb45c109122a
ms.sourcegitcommit: 13940eb53c68664b11a2d685ee17c78faab1945d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47860942"
---
# <a name="get-started-with-aspnet-core"></a>ASP.NET Core 시작

이 문서에서는 ASP.NET Core 앱을 만들고 실행하는 단계를 제공합니다.

::: moniker range=">= aspnetcore-2.1"

1. [!INCLUDE [](~/includes/2.1-SDK.md)]를 설치합니다.

2. ASP.NET Core 프로젝트를 만듭니다. 명령 셸을 열고 다음 명령을 입력합니다.

   ```console
   dotnet new webapp -o aspnetcoreapp
   ```

3. HTTPS 개발 인증서 신뢰:

# <a name="windowstabwindows"></a>[Windows](#tab/windows)

  ```console
  dotnet dev-certs https --trust
  ```

  이전 명령으로 인해 다음 대화 상자가 표시됩니다.

  ![보안 경고 대화 상자](_static/cert.png)

  개발 인증서를 신뢰하는 데 동의하는 경우 **예**를 선택합니다.

# <a name="macostabmacos"></a>[macOS](#tab/macos)

  ```console
  dotnet dev-certs https --trust
  ```

  이전 명령으로 인해 다음 메시지가 표시됩니다.

  *HTTPS 개발 인증서를 신뢰해야 합니다. 인증서를 신뢰할 수 없는 경우*  `'sudo security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.keychain <<certificate>>'` 명령을 실행합니다.  
  *이 명령은 시스템 키 집합에 인증서를 설치하기 위해 암호를 묻는 메시지를 표시할 수 있습니다.
  
  암호:*

  개발 인증서를 신뢰하는 데 동의하는 경우 암호를 입력합니다.

# <a name="linuxtablinux"></a>[Linux](#tab/linux)

  HTTPS 개발 인증서를 신뢰하는 방법은 Linux 배포에 대한 설명서를 참조하세요.
   
---

4. 앱을 실행합니다.

   ```console
   cd aspnetcoreapp
   dotnet run
   ```

5. [http://localhost:5001](http://localhost:5001)으로 이동합니다.  **동의**를 클릭하여 개인 정보 및 쿠키 정책에 동의합니다. 이 앱은 개인 정보를 보관하지 않습니다.

6. *Pages/About.cshtml*을 열고 다음과 같은 강조 표시된 태그로 페이지를 수정합니다.

   [!code-cshtml[](sample/getting-started/about.cshtml?highlight=9)]

7. [http://localhost:5001/About](http://localhost:5001/About)으로 이동하여 변경 내용이 표시되는지 확인합니다.

[!INCLUDE [next steps](~/includes/getting-started/next-steps.md)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

1. [!INCLUDE [](~/includes/net-core-sdk-download-link.md)]를 설치합니다.

2. 새 ASP.NET Core 프로젝트를 만듭니다.

   명령 셸을 엽니다. 다음 명령을 입력합니다.

   ```console
   dotnet new razor -o aspnetcoreapp
   ```

3. 다음 명령을 사용하여 앱을 실행합니다.

   ```console
   cd aspnetcoreapp
   dotnet run
   ```

4. [http://localhost:5000](http://localhost:5000)으로 이동합니다.

5. *Pages/About.cshtml* 을 열고 페이지를 수정하여 “Hello, world! 서버 시간은 @DateTime.Now입니다.” 메시지를 표시합니다.

   [!code-cshtml[](sample/getting-started/about.cshtml?highlight=9&range=1-9)]

6. [http://localhost:5000/About](http://localhost:5000/About)으로 이동하여 변경 내용을 확인합니다.

[!INCLUDE [next steps](~/includes/getting-started/next-steps.md)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

1. [.NET Core 모든 다운로드 페이지](https://www.microsoft.com/net/download/all)에서 SDK 1.0.4용 .NET Core **SDK 설치 관리자**를 설치합니다.

2. 새 ASP.NET Core 프로젝트에 대한 폴더를 만듭니다.

   명령 셸을 엽니다. 다음 명령을 입력합니다.

   ```console
   mkdir aspnetcoreapp
   cd aspnetcoreapp
   ```

3. 컴퓨터에 최신 SDK 버전을 설치한 경우 *global.json* 파일을 만들어 1.0.4 SDK를 선택합니다.

   ```json
   {
     "sdk": { "version": "1.0.4" }
   }
   ```

4. 새 ASP.NET Core 프로젝트를 만듭니다.

   ```console
   dotnet new web
   ```

5. 패키지를 복원합니다.

   ```console
   dotnet restore
   ```

6. 앱을 실행합니다.

   ```console
   dotnet run
   ```

   [dotnet run](/dotnet/core/tools/dotnet-run) 명령은 필요한 경우 앱을 먼저 빌드합니다.

7. `http://localhost:5000`으로 이동합니다.

[!INCLUDE [next steps](~/includes/getting-started/next-steps.md)]

::: moniker-end
