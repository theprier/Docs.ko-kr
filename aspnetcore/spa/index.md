---
title: ASP.NET Core에서 단일 페이지 응용 프로그램 템플릿 사용
author: SteveSandersonMS
description: ASP.NET Core SPA(단일 페이지 응용 프로그램) 프로젝트 템플릿을 설치하고 시작하는 방법에 대해 알아봅니다.
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 02/21/2018
ms.devlang: csharp
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: spa/index
ms.openlocfilehash: eda4817de007f3c3184b2ba6ed6c97989ff17da5
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="use-the-single-page-application-templates-with-aspnet-core"></a><span data-ttu-id="0be1e-103">ASP.NET Core에서 단일 페이지 응용 프로그램 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="0be1e-103">Use the Single Page Application templates with ASP.NET Core</span></span>

> [!NOTE]
> <span data-ttu-id="0be1e-104">릴리스된 .NET Core 2.0.x SDK에는 Angular, React 및 React with Redux에 대한 이전 프로젝트 템플릿이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0be1e-104">The released .NET Core 2.0.x SDK includes older project templates for Angular, React, and React with Redux.</span></span> <span data-ttu-id="0be1e-105">이 문서는 그러한 이전 프로젝트 템플릿에 대한 내용이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="0be1e-105">This documentation isn't about those older project templates.</span></span> <span data-ttu-id="0be1e-106">이 설명서는 ASP.NET 코어 2.0에 수동으로 설치할 수 있는 최신 Angular, React 및 React with Redux 템플릿용 입니다.</span><span class="sxs-lookup"><span data-stu-id="0be1e-106">This documentation is for the latest Angular, React, and React with Redux templates, which can be installed manually into ASP.NET Core 2.0.</span></span> <span data-ttu-id="0be1e-107">템플릿은 기본적으로 ASP.NET Core 2.1에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0be1e-107">The templates are included by default with ASP.NET Core 2.1.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0be1e-108">전제 조건</span><span class="sxs-lookup"><span data-stu-id="0be1e-108">Prerequisites</span></span>

* [!INCLUDE [](~/includes/net-core-sdk-download-link.md)]
* <span data-ttu-id="0be1e-109">[Node.js](https://nodejs.org), 버전 6 이상</span><span class="sxs-lookup"><span data-stu-id="0be1e-109">[Node.js](https://nodejs.org), version 6 or later</span></span>

## <a name="installation"></a><span data-ttu-id="0be1e-110">설치</span><span class="sxs-lookup"><span data-stu-id="0be1e-110">Installation</span></span>

<span data-ttu-id="0be1e-111">ASP.NET Core 2.0이 있는 경우 다음 명령을 실행하여 Angular, React 및 React with Redux에 대해 업데이트된 ASP.NET Core 템플릿을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0be1e-111">If you have ASP.NET Core 2.0, run the following command to install the updated ASP.NET Core templates for Angular, React, and React with Redux:</span></span>

```console
dotnet new --install Microsoft.DotNet.Web.Spa.ProjectTemplates::2.0.0
```

## <a name="use-the-templates"></a><span data-ttu-id="0be1e-112">템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="0be1e-112">Use the templates</span></span>

- [<span data-ttu-id="0be1e-113">Angular 프로젝트 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="0be1e-113">Use the Angular project template</span></span>](xref:spa/angular)
- [<span data-ttu-id="0be1e-114">React 프로젝트 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="0be1e-114">Use the React project template</span></span>](xref:spa/react)
- [<span data-ttu-id="0be1e-115">React with Redux 프로젝트 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="0be1e-115">Use the React with Redux project template</span></span>](xref:spa/react-with-redux)
