---
title: ASP.NET Core 시작
author: rick-anderson
description: ASP.NET Core를 사용하여 간단한 Hello World 앱을 만들고 실행하는 빠른 자습서입니다.
manager: wpickett
ms.author: riande
ms.date: 10/18/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: getting-started
ms.openlocfilehash: c2f18c69901a5a6503314d508a776e6985872681
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="get-started-with-aspnet-core"></a>ASP.NET Core 시작

> [!NOTE]
> 이러한 지침은 최신 버전의 ASP.NET Core에 대한 것입니다. 이 문서의 1.1 버전은 [ASP.NET Core 1.1 시작](xref:getting-started-1.1)을 참조하세요.

1. [!INCLUDE [](~/includes/net-core-sdk-download-link.md)]를 설치합니다.

2. 새 .NET Core 프로젝트를 만듭니다.

   macOS 및 Linux에서 터미널 창을 엽니다. Windows에서 명령 프롬프트를 엽니다. 다음 명령을 입력합니다.

    ```terminal
    dotnet new razor -o aspnetcoreapp
    ```
    
3. 앱을 실행합니다.

    다음 명령을 사용하여 앱을 실행합니다.

    ```terminal
    cd aspnetcoreapp
    dotnet run
    ```

4. [http://localhost:5000](http://localhost:5000)으로 이동합니다.

5. <em>Pages/About.cshtml</em> 을 열고 페이지를 수정하여 “Hello, world! The time on the server is @DateTime.Now.” 메시지를 표시합니다.

    [!code-html[](getting-started/sample/getting-started/about.cshtml?highlight=9&range=1-9)]

6. [http://localhost:5000/About](http://localhost:5000/About)으로 이동하여 변경 내용을 확인합니다.

### <a name="next-steps"></a>다음 단계

시작 자습서는 [ASP.NET Core 자습서](tutorials/index.md)를 참조하세요.

ASP.NET Core 개념 및 아키텍처에 대한 소개는 [ASP.NET Core 소개](index.md) 및 [ASP.NET Core 기본 사항](fundamentals/index.md)을 참조하세요.

ASP.NET Core 앱은 .NET Core 또는 .NET Framework 기본 클래스 라이브러리 및 런타임을 사용할 수 있습니다. 자세한 내용은 [.NET Core와 .NET Framework 중에 선택](https://docs.microsoft.com/dotnet/articles/standard/choosing-core-framework-server)을 참조하세요.
