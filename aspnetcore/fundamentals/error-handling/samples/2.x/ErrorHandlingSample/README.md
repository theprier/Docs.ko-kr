---
ms.openlocfilehash: b1f7c306533e70f84e73a020c74756b91cae7ea7
ms.sourcegitcommit: 191d21c1e37b56f0df0187e795d9a56388bbf4c7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2019
ms.locfileid: "57665757"
---
# <a name="error-handling-sample-application"></a><span data-ttu-id="f105b-101">오류 처리 샘플 애플리케이션</span><span class="sxs-lookup"><span data-stu-id="f105b-101">Error Handling Sample Application</span></span>

<span data-ttu-id="f105b-102">이 샘플 앱에서는 [ASP.NET Core에서 오류 처리](https://docs.microsoft.com/aspnet/core/fundamentals/error-handling) 항목에 설명된 시나리오를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f105b-102">This sample app demonstrates the scenarios described in the [Handle errors in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/error-handling) topic.</span></span>

## <a name="configure-a-custom-exception-handling-page"></a><span data-ttu-id="f105b-103">사용자 지정 예외 처리 페이지 구성</span><span class="sxs-lookup"><span data-stu-id="f105b-103">Configure a custom exception handling page</span></span>

<span data-ttu-id="f105b-104">개발 환경에서 앱이 실행되지 않는 경우 예외 처리 미들웨어:</span><span class="sxs-lookup"><span data-stu-id="f105b-104">When the app isn't running in the Development environment, Exception Handling Middleware:</span></span>

* <span data-ttu-id="f105b-105">예외를 catch합니다.</span><span class="sxs-lookup"><span data-stu-id="f105b-105">Catches exceptions.</span></span>
* <span data-ttu-id="f105b-106">예외를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="f105b-106">Logs exceptions.</span></span>
* <span data-ttu-id="f105b-107">제공된 경로에 있는 대체 파이프라인에서 요청을 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f105b-107">Re-executes the request in an alternate pipeline at the path provided.</span></span>

## <a name="configure-custom-exception-handling-code"></a><span data-ttu-id="f105b-108">사용자 지정 예외 처리 코드 구성</span><span class="sxs-lookup"><span data-stu-id="f105b-108">Configure custom exception handling code</span></span>

<span data-ttu-id="f105b-109">사용자 지정 예외 처리 페이지의 오류에 대해 엔드포인트를 제공하는 대신 `UseExceptionHandler`에 람다를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f105b-109">An alternative to serving an endpoint for errors with a custom exception handling page is to provide a lambda to `UseExceptionHandler`.</span></span> <span data-ttu-id="f105b-110">`UseExceptionHandler`에 람다를 사용하면 응답을 반환하기 전에 오류에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f105b-110">Using a lambda with `UseExceptionHandler` allows access to the error before returning the response.</span></span>

<span data-ttu-id="f105b-111">샘플 앱에서는 `Startup.Configure`에서 사용자 지정 예외 처리 코드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f105b-111">The sample app demonstrates custom exception handling code in `Startup.Configure`.</span></span> <span data-ttu-id="f105b-112">*Startup.cs* 파일(`LambdaErrorHandler`)의 맨 위에 있는 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="f105b-112">Follow the instructions at the top of the *Startup.cs* file (`LambdaErrorHandler`).</span></span> <span data-ttu-id="f105b-113">앱이 시작된 후 인덱스 페이지의 **예외 Throw** 링크를 사용하여 예외를 트리거하세요.</span><span class="sxs-lookup"><span data-stu-id="f105b-113">After the app starts, trigger an exception with the **Throw Exception** link on the Index page.</span></span>
