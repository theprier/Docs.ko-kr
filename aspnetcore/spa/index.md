---
title: ASP.NET Core에서 단일 페이지 응용 프로그램 템플릿 사용
author: SteveSandersonMS
description: ASP.NET Core SPA(단일 페이지 응용 프로그램) 프로젝트 템플릿을 설치하고 시작하는 방법에 대해 알아봅니다.
manager: wpickett
monikerRange: '>= aspnetcore-2.0'
ms.author: scaddie
ms.custom: mvc
ms.date: 02/21/2018
ms.devlang: csharp
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: spa/index
ms.openlocfilehash: f7bb23e9001c7606c3e622bf4575a4debec56ccd
ms.sourcegitcommit: 466300d32f8c33e64ee1b419a2cbffe702863cdf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/27/2018
---
# <a name="use-the-single-page-application-templates-with-aspnet-core"></a>ASP.NET Core에서 단일 페이지 응용 프로그램 템플릿 사용

::: moniker range="= aspnetcore-2.0"

> [!NOTE]
> 릴리스된 .NET Core 2.0.x SDK에는 Angular, React 및 React with Redux에 대한 이전 프로젝트 템플릿이 포함됩니다. 이 문서는 그러한 이전 프로젝트 템플릿에 대한 내용이 아닙니다. 이 설명서는 ASP.NET 코어 2.0에 수동으로 설치할 수 있는 최신 Angular, React 및 React with Redux 템플릿용 입니다. 템플릿은 기본적으로 ASP.NET Core 2.1에 포함되어 있습니다.

::: moniker-end

## <a name="prerequisites"></a>전제 조건

* [!INCLUDE [](~/includes/net-core-sdk-download-link.md)]
* [Node.js](https://nodejs.org), 버전 6 이상

## <a name="installation"></a>설치

::: moniker range=">= aspnetcore-2.1"

템플릿은 ASP.NET Core 2.1과 함께 설치되어 있습니다.

::: moniker-end

::: moniker range="= aspnetcore-2.0"

ASP.NET Core 2.0이 있는 경우 다음 명령을 실행하여 Angular, React 및 React with Redux에 대해 업데이트된 ASP.NET Core 템플릿을 설치합니다.

```console
dotnet new --install Microsoft.DotNet.Web.Spa.ProjectTemplates::2.0.0
```

::: moniker-end

## <a name="use-the-templates"></a>템플릿 사용

* [Angular 프로젝트 템플릿 사용](xref:spa/angular)
* [React 프로젝트 템플릿 사용](xref:spa/react)
* [React with Redux 프로젝트 템플릿 사용](xref:spa/react-with-redux)
