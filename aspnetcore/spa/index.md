---
title: "단일 페이지 응용 프로그램 템플릿 사용"
author: SteveSandersonMS
description: "ASP.NET Core SPA(단일 페이지 응용 프로그램) 프로젝트 템플릿을 설치하고 시작하는 방법에 대해 알아봅니다."
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 02/21/2018
ms.devlang: csharp
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: spa/index
ms.openlocfilehash: 63b56de101199e9ea0d66d89d2dd7288e47902f6
ms.sourcegitcommit: 49fb3b7669b504d35edad34db8285e56b958a9fc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/23/2018
---
# <a name="use-the-single-page-application-templates"></a>단일 페이지 응용 프로그램 템플릿 사용

> [!NOTE]
> 릴리스된 .NET Core 2.0.x SDK에는 Angular, React 및 React with Redux에 대한 이전 프로젝트 템플릿이 포함됩니다. 이 문서는 그러한 이전 프로젝트 템플릿에 대한 내용이 아닙니다. 이 설명서는 ASP.NET 코어 2.0에 수동으로 설치할 수 있는 최신 Angular, React 및 React with Redux 템플릿용 입니다. 템플릿은 기본적으로 ASP.NET Core 2.1에 포함되어 있습니다.

## <a name="prerequisites"></a>필수 구성 요소

* [.NET Core SDK](https://www.microsoft.com/net/download), 버전 2.0.0 이상
* [Node.js](https://nodejs.org), 버전 6 이상

## <a name="installation"></a>설치

ASP.NET Core 2.0이 있는 경우 다음 명령을 실행하여 Angular, React 및 React with Redux에 대해 업데이트된 ASP.NET Core 템플릿을 설치합니다.

```console
dotnet new --install Microsoft.DotNet.Web.Spa.ProjectTemplates::2.0.0
```

## <a name="use-the-templates"></a>템플릿 사용

- [Angular 프로젝트 템플릿 사용](xref:spa/angular)
- [React 프로젝트 템플릿 사용](xref:spa/react)
- [React with Redux 프로젝트 템플릿 사용](xref:spa/react-with-redux)
