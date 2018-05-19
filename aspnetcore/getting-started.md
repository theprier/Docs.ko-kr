---
title: ASP.NET Core 시작
author: rick-anderson
description: ASP.NET Core를 사용하여 간단한 Hello World 앱을 만들고 실행하는 빠른 자습서입니다.
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 05/10/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: getting-started
ms.openlocfilehash: e814277663ff5a964171a71ebb6e0f094e0ddc60
ms.sourcegitcommit: 3d071fabaf90e32906df97b08a8d00e602db25c0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="get-started-with-aspnet-core"></a>ASP.NET Core 시작

::: moniker range=">= aspnetcore-2.0"

1. [!INCLUDE[](~/includes/net-core-sdk-download-link.md)]를 설치합니다.

2. 새 .NET Core 프로젝트를 만듭니다.

   macOS 및 Linux에서 터미널 창을 엽니다. Windows에서 명령 프롬프트를 엽니다. 다음 명령을 입력합니다.

    ```terminal
    dotnet new razor -o aspnetcoreapp
    ```

3. 다음 명령을 사용하여 앱을 실행합니다.

    ```terminal
    cd aspnetcoreapp
    dotnet run
    ```

4. [http://localhost:5000](http://localhost:5000)으로 이동합니다.

5. *Pages/About.cshtml* 을 열고 페이지를 수정하여 “Hello, world! 서버 시간은 @DateTime.Now입니다.” 메시지를 표시합니다.

    [!code-cshtml[](getting-started/sample/getting-started/about.cshtml?highlight=9&range=1-9)]

6. [http://localhost:5000/About](http://localhost:5000/About)으로 이동하여 변경 내용을 확인합니다.

[!INCLUDE[next steps](~/includes/getting-started/next-steps.md)]
::: moniker-end

::: moniker range="<= aspnetcore-1.1"

1. [.NET Core 모든 다운로드 페이지](https://www.microsoft.com/net/download/all)에서 SDK 1.0.4용 .NET Core **SDK 설치 관리자**를 설치합니다.

2. 새 .NET Core 프로젝트에 대한 폴더를 만듭니다.

   macOS 및 Linux에서 터미널 창을 엽니다. Windows에서 명령 프롬프트를 엽니다.

   ```terminal
   mkdir aspnetcoreapp
   cd aspnetcoreapp
   ```

3. 컴퓨터에 최신 SDK 버전을 설치한 경우 *global.json* 파일을 만들어 1.0.4 SDK를 선택합니다.

   ```json
   {
     "sdk": { "version": "1.0.4" }
   }
   ```

4. 새 .NET Core 프로젝트를 만듭니다.

   ```terminal
   dotnet new web
   ```

5. 패키지를 복원합니다.

    ```terminal
    dotnet restore
    ```

6. 앱을 실행합니다.

   ```terminal
   dotnet run
   ```

   [dotnet run](/dotnet/core/tools/dotnet-run) 명령은 필요한 경우 앱을 먼저 빌드합니다.

7. `http://localhost:5000`으로 이동합니다.

[!INCLUDE[next steps](~/includes/getting-started/next-steps.md)]
::: moniker-end