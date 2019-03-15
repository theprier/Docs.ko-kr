---
ms.openlocfilehash: b1f7c306533e70f84e73a020c74756b91cae7ea7
ms.sourcegitcommit: 191d21c1e37b56f0df0187e795d9a56388bbf4c7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2019
ms.locfileid: "57665757"
---
# <a name="error-handling-sample-application"></a>오류 처리 샘플 애플리케이션

이 샘플 앱에서는 [ASP.NET Core에서 오류 처리](https://docs.microsoft.com/aspnet/core/fundamentals/error-handling) 항목에 설명된 시나리오를 보여 줍니다.

## <a name="configure-a-custom-exception-handling-page"></a>사용자 지정 예외 처리 페이지 구성

개발 환경에서 앱이 실행되지 않는 경우 예외 처리 미들웨어:

* 예외를 catch합니다.
* 예외를 기록합니다.
* 제공된 경로에 있는 대체 파이프라인에서 요청을 다시 실행합니다.

## <a name="configure-custom-exception-handling-code"></a>사용자 지정 예외 처리 코드 구성

사용자 지정 예외 처리 페이지의 오류에 대해 엔드포인트를 제공하는 대신 `UseExceptionHandler`에 람다를 제공합니다. `UseExceptionHandler`에 람다를 사용하면 응답을 반환하기 전에 오류에 액세스할 수 있습니다.

샘플 앱에서는 `Startup.Configure`에서 사용자 지정 예외 처리 코드를 보여 줍니다. *Startup.cs* 파일(`LambdaErrorHandler`)의 맨 위에 있는 지침을 따르세요. 앱이 시작된 후 인덱스 페이지의 **예외 Throw** 링크를 사용하여 예외를 트리거하세요.
