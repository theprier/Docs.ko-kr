---
uid: webhooks/diagnostics/debugging
title: 디버깅 하는 ASP.NET 웹 후크 | Microsoft Docs
author: rick-anderson
description: ASP.NET 웹 후크를 디버깅 하는 방법입니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/17/2012
ms.topic: article
ms.assetid: 467da78b-3c35-4c51-8b08-77a32379e4a8
ms.technology: ''
ms.openlocfilehash: 5c567fb51db008526f59e09fce5bb60b66f6e479
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37389061"
---
# <a name="aspnet-webhooks-debugging"></a>디버깅 하는 ASP.NET 웹 후크  

## <a name="debugging-in-azure"></a>Azure에서 디버깅

Azure에서 실행 하는 동안 웹 응용 프로그램을 디버깅 하려면이 자습서를 참조 하세요 [Visual Studio를 사용 하 여 Azure App Service에서 웹 앱 문제 해결](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)합니다.

## <a name="debugging-with-source-and-symbols"></a>소스 및 기호를 사용 하 여 디버깅

사용자 고유의 코드를 디버깅 하는 것 외에도 Microsoft ASP.NET 웹 후크를로 직접 이동 하 고 실제로 디버그할 수는 모든.NET. 로컬 또는 원격으로 디버그 하는지 여부에 관계 없이 작동 합니다. 먼저,로 이동 하 여 소스 및 기호를 찾으려면 Visual Studio를 구성 **디버그** 차례로 **옵션 및 설정**합니다. 다음과 같은 옵션을 설정 합니다.

![옵션 및 설정](_static/SourceSymbols.png)

다음에 대 한 링크를 추가 [symbolsource.org](http://symbolsource.org) 소스 및 기호를 다운로드 합니다. 로 이동 합니다 **기호** 위 메뉴의 탭 및 기호 위치와 다음을 추가:

```
http://srv.symbolsource.org/pdb/Public
```

또한 캐시 디렉터리의 약식 이름을;에 있는지를 확인합니다 그렇지 않으면 파일 이름을 가져올 수 있습니다 너무 깁니다 기호를 로드 하지 그러면 합니다. 샘플 경로 다음과 같습니다.

```
C:\SymCache
```

설정은 다음과 유사 하 게 같아야 합니다.

![옵션 기호 파일 위치 예제](_static/SymSource.png)
