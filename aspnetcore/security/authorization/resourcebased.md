---
title: ASP.NET Core에서 리소스 기반의 권한 부여
author: scottaddie
description: 권한 부여 속성 않습니다 요구 사항을 충족 하는 경우 ASP.NET Core 응용 프로그램의 리소스 기반 권한 부여를 구현 하는 방법을 알아봅니다.
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 11/07/2017
ms.devlang: csharp
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/authorization/resourcebased
ms.openlocfilehash: 3be2d9b9aef18763fbdba78e044dd6b68ddcef0c
ms.sourcegitcommit: 9bc34b8269d2a150b844c3b8646dcb30278a95ea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/12/2018
ms.locfileid: "34094284"
---
# <a name="resource-based-authorization-in-aspnet-core"></a>ASP.NET Core에서 리소스 기반의 권한 부여

권한 부여 전략 액세스 되는 리소스에 따라 달라 집니다. Author 속성에 문서를 가정 합니다. 작성자만 문서를 업데이트할 수 있습니다. 따라서 문서 권한 부여 평가 하기 전에 데이터 저장소에서 검색 해야 합니다.

특성 평가 데이터 바인딩 전에 페이지 처리기 또는 문서를 로드 하는 작업의 실행 하기 전에 발생 합니다. 이러한 이유로, 사용한 선언적 권한 부여는 `[Authorize]` 특성으로 충분 하지 않습니다. 대신, 사용자 지정 권한 부여 메서드를 호출할 수 있습니다&mdash;스타일 명령적 권한 부여 라고 합니다.

사용 하 여는 [앱 샘플](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/resourcebased/samples) ([다운로드 하는 방법](xref:tutorials/index#how-to-download-a-sample))이이 항목에서 설명 하는 기능을 탐색할 수 있습니다.

[권한 부여에 의해 보호 되는 사용자 데이터와 ASP.NET Core 응용 프로그램 만들기](xref:security/authorization/secure-data) 리소스 기반 권한 부여를 사용 하는 샘플 앱을 포함 합니다.

## <a name="use-imperative-authorization"></a>필수 권한 부여를 사용 하 여

권한 부여로 구현 됩니다는 [IAuthorizationService](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationservice) 내에서 서비스 컬렉션에 등록 하 고 서비스는 `Startup` 클래스입니다. 서비스를 통해 제공할 [종속성 주입](xref:fundamentals/dependency-injection#fundamentals-dependency-injection) 페이지 처리기 또는 작업에 있습니다.

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Controllers/DocumentController.cs?name=snippet_IAuthServiceDI&highlight=6)]

`IAuthorizationService` 에 두 개의 `AuthorizeAsync` 메서드 오버 로드: 리소스와 정책 이름 및 다른 리소스와 평가 하기 위한 요구 사항 목록이 수락 하나 수락 합니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

```csharp
Task<AuthorizationResult> AuthorizeAsync(ClaimsPrincipal user,
                          object resource,
                          IEnumerable<IAuthorizationRequirement> requirements);
Task<AuthorizationResult> AuthorizeAsync(ClaimsPrincipal user,
                          object resource,
                          string policyName);
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

```csharp
Task<bool> AuthorizeAsync(ClaimsPrincipal user,
                          object resource,
                          IEnumerable<IAuthorizationRequirement> requirements);
Task<bool> AuthorizeAsync(ClaimsPrincipal user,
                          object resource,
                          string policyName);
```

---

<a name="security-authorization-resource-based-imperative"></a>

다음 예제에서는 보안을 유지 하도록 리소스는 사용자 지정에 로드 됩니다 `Document` 개체입니다. `AuthorizeAsync` 오버 로드는 현재 사용자가 제공 된 문서를 편집할 수 있는지 여부를 확인 하기 위해 호출 된 합니다. 사용자 지정 "EditPolicy" 권한 부여 정책에 대 한 결정으로 구분 됩니다. 참조 [사용자 지정 정책 기반 권한 부여](xref:security/authorization/policies) 권한 부여 정책 만들기에 대 한 자세한 합니다.

> [!NOTE]
> 다음 코드 샘플 인증을 실행 하는 것으로 가정 하 고 집합의 `User` 속성입니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Pages/Document/Edit.cshtml.cs?name=snippet_DocumentEditHandler)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp1/Controllers/DocumentController.cs?name=snippet_DocumentEditAction)]

---

## <a name="write-a-resource-based-handler"></a>리소스 기반 처리기 작성

리소스 기반 권한 부여 보다 큰 차이가 없습니다.에 대 한 처리기를 작성 [일반 요구 사항 처리기 작성](xref:security/authorization/policies#security-authorization-policies-based-authorization-handler)합니다. 사용자 지정 요구 사항 클래스를 만들고 요구 사항 처리기 클래스를 구현 합니다. 처리기 클래스 요구 사항 및 리소스 종류를 지정합니다. 예를 들어 한 처리기를 활용 하는 `SameAuthorRequirement` 요구 사항 및 `Document` 리소스 모양은 다음과 같습니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Services/DocumentAuthorizationHandler.cs?name=snippet_HandlerAndRequirement)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp1/Services/DocumentAuthorizationHandler.cs?name=snippet_HandlerAndRequirement)]

---

요구 사항 및 처리기에 등록 된 `Startup.ConfigureServices` 메서드:

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Startup.cs?name=snippet_ConfigureServicesSample&highlight=3-7,9)]

### <a name="operational-requirements"></a>운영 요구 사항

CRUD (만들기, 읽기, 업데이트, 삭제) 작업의 결과에 따라 결정을 수행 하면 사용 하 여는 [OperationAuthorizationRequirement](/dotnet/api/microsoft.aspnetcore.authorization.infrastructure.operationauthorizationrequirement) 도우미 클래스입니다. 이 클래스를 사용 하면 각 작업 유형에 대해 개별 클래스 대신 단일 처리기를 작성할 수 있습니다. 이 기능을 사용 하려면 일부 작업 이름을 제공 합니다.

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Services/DocumentAuthorizationCrudHandler.cs?name=snippet_OperationsClass)]

처리기는 다음과 같이 사용 하 여 구현 된 `OperationAuthorizationRequirement` 요구 사항 및 `Document` 리소스:

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Services/DocumentAuthorizationCrudHandler.cs?name=snippet_Handler)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp1/Services/DocumentAuthorizationCrudHandler.cs?name=snippet_Handler)]

---

이전 처리기 리소스, 사용자의 id 및 요구 사항의를 사용 하 여 작업의 유효성을 검사 `Name` 속성입니다.

작업 리소스 처리기를 호출 하려면 작업을 호출할 때 지정 `AuthorizeAsync` 페이지 처리기의 동작입니다. 다음 예제에서는 인증 된 사용자가 제공 된 문서를 볼 수 있는지 여부를 결정 합니다.

> [!NOTE]
> 다음 코드 샘플 인증을 실행 하는 것으로 가정 하 고 집합의 `User` 속성입니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Pages/Document/View.cshtml.cs?name=snippet_DocumentViewHandler&highlight=10-11)]

권한 부여에 성공 하면 문서를 보기 위한 페이지가 반환 됩니다. 경우 권한 부여 실패 하지만 사용자가 인증 되 면 반환 `ForbidResult` 권한 부여에 실패 한 모든 인증 미들웨어에 알립니다. A `ChallengeResult` 인증을 수행 해야 하는 경우 반환 됩니다. 대화형 브라우저 클라이언트에는 사용자를 로그인 페이지로 리디렉션합니다 적절 한 수 있습니다.

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp1/Controllers/DocumentController.cs?name=snippet_DocumentViewAction&highlight=11-12)]

권한 부여에 성공 하면 문서에 대 한 보기 반환 됩니다. 권한 부여에 실패 하면 반환 `ChallengeResult` 모든 인증 미들웨어에 알리고 권한 부여 실패, 미들웨어 적절 한 응답을 걸릴 수 있습니다. 적절 한 응답 401 또는 403 상태 코드를 반환 될 수 없습니다. 대화형 브라우저 클라이언트에 대 한 사용자를 로그인 페이지로 리디렉션하여 관리할 수 있습니다.

---
