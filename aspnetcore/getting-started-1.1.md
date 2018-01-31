---
title: "ASP.NET Core 1.1 시작"
author: rick-anderson
description: "ASP.NET Core 1.1을 사용하여 간단한 Hello World 앱을 만들고 실행하는 빠른 자습서입니다."
manager: wpickett
ms.author: riande
ms.date: 08/07/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: getting-started-1.1
ms.openlocfilehash: 895e91efbba931923540e4cd182862cbc1851585
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="getting-started-with-aspnet-core-11"></a>ASP.NET Core 1.1 시작

> [!NOTE]
> 이러한 지침은 ASP.NET Core 1.1에 대한 것입니다. 최신 버전을 찾고 있나요? [이 자습서의 현재 버전](xref:getting-started)을 참조하세요.

1. [.NET Core 1.0.5 & 1.1.2 SDK 1.0.4 다운로드 페이지](https://github.com/dotnet/core/blob/master/release-notes/download-archives/1.0.5-download.md)에서 SDK 1.0.4에 대한 .NET Core **SDK 설치 관리자**를 설치합니다.

2. 새 .NET Core 프로젝트에 대한 폴더를 만듭니다.

   macOS 및 Linux에서 터미널 창을 엽니다. Windows에서 명령 프롬프트를 엽니다.

   ```terminal
   mkdir aspnetcoreapp
   cd aspnetcoreapp
   ```

2. 컴퓨터에 최신 SDK 버전을 설치한 경우 *global.json* 파일을 만들어 1.0.4 SDK를 선택합니다.

   ```json
   {
     "sdk": { "version": "1.0.4" }
   }
   ```

2. 새 .NET Core 프로젝트를 만듭니다.

   ```terminal
   dotnet new web
   ```
   
3.  패키지를 복원합니다.

    ```terminal
    dotnet restore
    ```

4. 앱을 실행합니다.

   `dotnet run` 명령은 필요한 경우 앱을 먼저 빌드합니다.

   ```terminal
   dotnet run
   ```

5. `http://localhost:5000`으로 이동

<!-- H3 to avoid a single-entry internal TOC -->
### <a name="next-steps"></a>다음 단계

시작 자습서는 [ASP.NET Core 자습서](tutorials/index.md)를 참조하세요.

ASP.NET Core 개념 및 아키텍처에 대한 소개는 [ASP.NET Core 소개](index.md) 및 [ASP.NET Core 기본 사항](fundamentals/index.md)을 참조하세요.

ASP.NET Core 앱은 .NET Core 또는 .NET Framework 기본 클래스 라이브러리 및 런타임을 사용할 수 있습니다. 자세한 내용은 [.NET Core와 .NET Framework 중에 선택](https://docs.microsoft.com/dotnet/articles/standard/choosing-core-framework-server)을 참조하세요.
