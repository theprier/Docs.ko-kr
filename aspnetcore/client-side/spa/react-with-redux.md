---
title: ASP.NET Core와 함께 React-with-Redux 프로젝트 템플릿 사용
author: SteveSandersonMS
description: React with Redux 및 create-react-app에 대한 ASP.NET Core SPA(단일 페이지 응용 프로그램) 프로젝트 템플릿을 시작하는 방법을 알아봅니다.
monikerRange: '>= aspnetcore-2.0'
ms.author: scaddie
ms.custom: mvc
ms.date: 02/21/2018
uid: spa/react-with-redux
ms.openlocfilehash: dab3d20865250aae548bff4614e631dd7c73b46f
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36291486"
---
# <a name="use-the-react-with-redux-project-template-with-aspnet-core"></a>ASP.NET Core와 함께 React-with-Redux 프로젝트 템플릿 사용

::: moniker range="= aspnetcore-2.0"

> [!NOTE]
> 이 문서는 ASP.NET Core 2.0에 포함된 React-with-Redux 프로젝트 템플릿에 대한 내용이 아닙니다. 수동으로 업데이트할 수 있는 최신 React-with-Redux 템플릿에 대한 내용입니다. 템플릿은 ASP.NET Core 2.1에 기본적으로 포함됩니다.

::: moniker-end

업데이트된 React-with-Redux 프로젝트 템플릿은 React, Redux 및 CRA([create-react-app](https://github.com/facebookincubator/create-react-app)) 규칙을 사용하여 풍부한 클라이언트 쪽 UI(사용자 인터페이스)를 구현하는 ASP.NET Core 앱에 대한 편리한 시작점을 제공합니다.

프로젝트 만들기 명령을 제외하고 React-with-Redux 템플릿에 대한 모든 정보는 React 템플릿과 동일합니다. 이 프로젝트 형식을 만들려면 `dotnet new react` 대신 `dotnet new reactredux`를 실행합니다. React 기반 템플릿에 공통적인 기능에 대한 자세한 내용은 [React 템플릿 설명서](xref:spa/react)를 참조하세요.
