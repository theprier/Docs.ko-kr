---
ms.openlocfilehash: 07abb12af390c0f2a50e98fc5e53545b6635f968
ms.sourcegitcommit: 191d21c1e37b56f0df0187e795d9a56388bbf4c7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2019
ms.locfileid: "57665511"
---
# <a name="aspnet-core-web-api-controller-sample"></a>ASP.NET Core Web API 컨트롤러 샘플

이 샘플 앱은 다음 프로젝트로 구성되어 있습니다.

- **WebApiSample.Api.22**: .NET Core 2.2를 대상으로 하는 ASP.NET Core 2.2 프로젝트입니다.
- **WebApiSample.Api.21**: .NET Core 2.1을 대상으로 하는 ASP.NET Core 2.1 프로젝트입니다.
- **WebApiSample.Api.Pre21**: .NET Core 2.0을 대상으로 하는 ASP.NET Core 2.0 프로젝트입니다.
- **WebApiSample.DataAccess**: 2개의 Web API 프로젝트에 대한 데이터 액세스 계층의 역할을 담당하는 .NET Standard 2.0 클래스 라이브러리입니다.

이 샘플에서는 다양한 Web API 컨트롤러를 만듭니다.

- [ControllerBase에서 클래스 파생](https://docs.microsoft.com/aspnet/core/web-api#derive-class-from-controllerbase)
- [ApiControllerAttribute로 클래스에 주석 달기](https://docs.microsoft.com/aspnet/core/web-api#annotate-class-with-apicontrollerattribute)
