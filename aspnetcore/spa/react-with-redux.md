---
title: "React와 Redux 프로젝트 템플릿을 사용 하 여"
author: SteveSandersonMS
description: "React Redux 및 반응 만들기-앱에 대 한 ASP.NET Core 단일 페이지 응용 프로그램 (SPA) 프로젝트 템플릿으로 시작 하는 방법에 알아봅니다."
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 02/21/2018
ms.devlang: csharp
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: spa/react-with-redux
ms.openlocfilehash: f52f4a866b8bb2adeee19548df32f3e7a91761d1
ms.sourcegitcommit: 49fb3b7669b504d35edad34db8285e56b958a9fc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/23/2018
---
# <a name="use-the-react-with-redux-project-template"></a><span data-ttu-id="43db0-103">React와 Redux 프로젝트 템플릿을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="43db0-103">Use the React-with-Redux project template</span></span>

> [!NOTE]
> <span data-ttu-id="43db0-104">이 설명서 포함 되지 않습니다 반응으로 Redux 프로젝트 템플릿에 대 한 ASP.NET 코어 2.0.</span><span class="sxs-lookup"><span data-stu-id="43db0-104">This documentation isn't about the React-with-Redux project template included in ASP.NET Core 2.0.</span></span> <span data-ttu-id="43db0-105">최신 반응으로 Redux 서식 파일을 수동으로 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43db0-105">It's about the newer React-with-Redux template to which you can update manually.</span></span> <span data-ttu-id="43db0-106">서식 파일은 기본적으로 ASP.NET Core 2.1에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="43db0-106">The template is included in ASP.NET Core 2.1 by default.</span></span>

<span data-ttu-id="43db0-107">업데이트 된 Redux와 대응 프로젝트 템플릿은 ASP.NET Core 응용 프로그램을 사용 하 여 반응 Redux에 대 한 편리한 시작점을 제공 하 고 [react 만들기-app](https://github.com/facebookincubator/create-react-app) (CRA)는 다양 하 고 클라이언트 쪽 UI (사용자 인터페이스)를 구현 하는 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="43db0-107">The updated React-with-Redux project template provides a convenient starting point for ASP.NET Core apps using React, Redux, and [create-react-app](https://github.com/facebookincubator/create-react-app) (CRA) conventions to implement a rich, client-side user interface (UI).</span></span>

<span data-ttu-id="43db0-108">프로젝트 만들기 명령을 제외 하 고 반응으로 Redux 서식 파일에 대 한 모든 정보 React 템플릿으로 같습니다.</span><span class="sxs-lookup"><span data-stu-id="43db0-108">With the exception of the project creation command, all information about the React-with-Redux template is the same as the React template.</span></span> <span data-ttu-id="43db0-109">이 프로젝트를 만들려면 실행 `dotnet new reactredux` 대신 `dotnet new react`합니다.</span><span class="sxs-lookup"><span data-stu-id="43db0-109">To create this project type, run `dotnet new reactredux` instead of `dotnet new react`.</span></span> <span data-ttu-id="43db0-110">React 기반 템플릿 모두에 공통 된 기능에 대 한 자세한 내용은 참조 [템플릿 문서 반응](xref:spa/react)합니다.</span><span class="sxs-lookup"><span data-stu-id="43db0-110">For more information about the functionality common to both React-based templates, see [React template documentation](xref:spa/react).</span></span>
