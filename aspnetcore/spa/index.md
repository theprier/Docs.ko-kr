---
title: "단일 페이지 응용 프로그램 템플릿 사용"
author: SteveSandersonMS
description: "ASP.NET Core SPA(단일 페이지 응용 프로그램) 미리 보기 프로젝트 템플릿을 설치하고 시작하는 방법에 대해 알아봅니다."
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 12/06/2017
ms.devlang: csharp
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: spa/index
ms.openlocfilehash: 59031d79a9558bb8fc94e55ac04e70876618dc02
ms.sourcegitcommit: 198fb0488e961048bfa376cf58cb853ef1d1cb91
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="use-the-single-page-application-templates-preview"></a><span data-ttu-id="a3c42-103">단일 페이지 응용 프로그램 템플릿(미리 보기) 사용</span><span class="sxs-lookup"><span data-stu-id="a3c42-103">Use the Single-Page Application templates (preview)</span></span>

> [!NOTE]
> <span data-ttu-id="a3c42-104">릴리스된 .NET Core 2.0.x SDK에는 Angular, React, React with Redux에 대한 프로젝트 템플릿이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3c42-104">The released .NET Core 2.0.x SDK includes project templates for Angular, React, and React with Redux.</span></span> <span data-ttu-id="a3c42-105">**이 문서는 그러한 릴리스된 프로젝트 템플릿에 대한 내용이 아닙니다.**</span><span class="sxs-lookup"><span data-stu-id="a3c42-105">**This documentation is not about those released project templates.**</span></span> <span data-ttu-id="a3c42-106">이 문서는 2018년 초에 출시 예정인 다음 버전의 Angular, React, React with Redux 템플릿용입니다.</span><span class="sxs-lookup"><span data-stu-id="a3c42-106">This documentation is for the next version of the Angular, React, and React with Redux templates, which we hope to ship in early 2018.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3c42-107">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="a3c42-107">Prerequisites</span></span>

* <span data-ttu-id="a3c42-108">[.NET Core SDK](https://www.microsoft.com/net/download), 버전 2.0.0 이상</span><span class="sxs-lookup"><span data-stu-id="a3c42-108">[.NET Core SDK](https://www.microsoft.com/net/download), version 2.0.0 or later</span></span>
* <span data-ttu-id="a3c42-109">[Node.js](https://nodejs.org), 버전 6 이상</span><span class="sxs-lookup"><span data-stu-id="a3c42-109">[Node.js](https://nodejs.org), version 6 or later</span></span>

## <a name="installation"></a><span data-ttu-id="a3c42-110">설치</span><span class="sxs-lookup"><span data-stu-id="a3c42-110">Installation</span></span>

<span data-ttu-id="a3c42-111">다음 명령을 실행하여 Angular, React, React with Redux에 대한 ASP.NET Core 템플릿의 **미리 보기**를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a3c42-111">Run the following command to install the **preview** release of the ASP.NET Core templates for Angular, React, and React with Redux:</span></span>

```console
dotnet new --install Microsoft.DotNet.Web.Spa.ProjectTemplates::2.0.0-preview1-final
```

## <a name="use-the-templates"></a><span data-ttu-id="a3c42-112">템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="a3c42-112">Use the templates</span></span>

- [<span data-ttu-id="a3c42-113">Angular 프로젝트 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="a3c42-113">Use the Angular project template</span></span>](xref:spa/angular)
- [<span data-ttu-id="a3c42-114">React 프로젝트 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="a3c42-114">Use the React project template</span></span>](xref:spa/react)
- [<span data-ttu-id="a3c42-115">React with Redux 프로젝트 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="a3c42-115">Use the React with Redux project template</span></span>](xref:spa/react-with-redux)
