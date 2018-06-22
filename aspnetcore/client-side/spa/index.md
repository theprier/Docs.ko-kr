---
title: ASP.NET Core에서 단일 페이지 응용 프로그램 템플릿 사용
author: SteveSandersonMS
description: ASP.NET Core SPA(단일 페이지 응용 프로그램) 프로젝트 템플릿을 설치하고 시작하는 방법에 대해 알아봅니다.
monikerRange: '>= aspnetcore-2.0'
ms.author: scaddie
ms.custom: mvc
ms.date: 02/21/2018
uid: spa/index
ms.openlocfilehash: ab164ae5d2df47739ec04b32cd21835ffdf9f87f
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36291446"
---
# <a name="use-the-single-page-application-templates-with-aspnet-core"></a><span data-ttu-id="f2da6-103">ASP.NET Core에서 단일 페이지 응용 프로그램 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="f2da6-103">Use the Single Page Application templates with ASP.NET Core</span></span>

::: moniker range="= aspnetcore-2.0"

> [!NOTE]
> <span data-ttu-id="f2da6-104">릴리스된 .NET Core 2.0.x SDK에는 Angular, React 및 React with Redux에 대한 이전 프로젝트 템플릿이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2da6-104">The released .NET Core 2.0.x SDK includes older project templates for Angular, React, and React with Redux.</span></span> <span data-ttu-id="f2da6-105">이 문서는 그러한 이전 프로젝트 템플릿에 대한 내용이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="f2da6-105">This documentation isn't about those older project templates.</span></span> <span data-ttu-id="f2da6-106">이 설명서는 ASP.NET 코어 2.0에 수동으로 설치할 수 있는 최신 Angular, React 및 React with Redux 템플릿용 입니다.</span><span class="sxs-lookup"><span data-stu-id="f2da6-106">This documentation is for the latest Angular, React, and React with Redux templates, which can be installed manually into ASP.NET Core 2.0.</span></span> <span data-ttu-id="f2da6-107">템플릿은 기본적으로 ASP.NET Core 2.1에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2da6-107">The templates are included by default with ASP.NET Core 2.1.</span></span>

::: moniker-end

## <a name="prerequisites"></a><span data-ttu-id="f2da6-108">전제 조건</span><span class="sxs-lookup"><span data-stu-id="f2da6-108">Prerequisites</span></span>

* [!INCLUDE [](~/includes/net-core-sdk-download-link.md)]
* <span data-ttu-id="f2da6-109">[Node.js](https://nodejs.org), 버전 6 이상</span><span class="sxs-lookup"><span data-stu-id="f2da6-109">[Node.js](https://nodejs.org), version 6 or later</span></span>

## <a name="installation"></a><span data-ttu-id="f2da6-110">설치</span><span class="sxs-lookup"><span data-stu-id="f2da6-110">Installation</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="f2da6-111">템플릿은 ASP.NET Core 2.1과 함께 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2da6-111">The templates are already installed with ASP.NET Core 2.1.</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="f2da6-112">ASP.NET Core 2.0이 있는 경우 다음 명령을 실행하여 Angular, React 및 React with Redux에 대해 업데이트된 ASP.NET Core 템플릿을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f2da6-112">If you have ASP.NET Core 2.0, run the following command to install the updated ASP.NET Core templates for Angular, React, and React with Redux:</span></span>

```console
dotnet new --install Microsoft.DotNet.Web.Spa.ProjectTemplates::2.0.0
```

::: moniker-end

## <a name="use-the-templates"></a><span data-ttu-id="f2da6-113">템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="f2da6-113">Use the templates</span></span>

* [<span data-ttu-id="f2da6-114">Angular 프로젝트 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="f2da6-114">Use the Angular project template</span></span>](xref:spa/angular)
* [<span data-ttu-id="f2da6-115">React 프로젝트 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="f2da6-115">Use the React project template</span></span>](xref:spa/react)
* [<span data-ttu-id="f2da6-116">React with Redux 프로젝트 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="f2da6-116">Use the React with Redux project template</span></span>](xref:spa/react-with-redux)