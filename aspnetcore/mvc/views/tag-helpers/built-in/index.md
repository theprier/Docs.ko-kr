---
title: 기본 제공 ASP.NET Core 태그 도우미
author: pkellner
description: 기본 제공 ASP.NET Core 태그 도우미에서 생산성을 향상시키는 방법을 알아봅니다.
manager: wpickett
ms.author: riande
ms.date: 09/13/2017
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: mvc/views/tag-helpers/builtin-th/Index
ms.openlocfilehash: f539f96a87b125c0f55855f780bbff005db8c0d9
ms.sourcegitcommit: 493a215355576cfa481773365de021bcf04bb9c7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
ms.locfileid: "29903210"
---
# <a name="aspnet-core-built-in-tag-helpers"></a><span data-ttu-id="32bfa-103">기본 제공 ASP.NET Core 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="32bfa-103">ASP.NET Core built-in Tag Helpers</span></span>

<span data-ttu-id="32bfa-104">작성자: [Peter Kellner](http://peterkellner.net)</span><span class="sxs-lookup"><span data-stu-id="32bfa-104">By [Peter Kellner](http://peterkellner.net)</span></span>

<span data-ttu-id="32bfa-105">ASP.NET Core에는 생산성을 향상하기 위해 다양한 기본 제공 태그 도우미가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32bfa-105">ASP.NET Core includes many built-in Tag Helpers to boost your productivity.</span></span> <span data-ttu-id="32bfa-106">이 섹션에서는 기본 제공 태그 도우미의 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="32bfa-106">This section provides an overview of the built-in Tag Helpers.</span></span>

> [!NOTE]
> <span data-ttu-id="32bfa-107">[Razor](xref:mvc/views/razor) 뷰 엔진에서 내부적으로 사용하기 때문에 다루지 않는 기본 제공 태그 도우미도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32bfa-107">There are built-in Tag Helpers which aren't discussed, since they're used internally by the [Razor](xref:mvc/views/razor) view engine.</span></span> <span data-ttu-id="32bfa-108">여기에는 웹 사이트의 루트 경로로 확장되는 ~ 문자의 태그 도우미가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="32bfa-108">This includes a Tag Helper for the ~ character, which expands to the root path of the website.</span></span>

## <a name="built-in-aspnet-core-tag-helpers"></a><span data-ttu-id="32bfa-109">기본 제공 ASP.NET Core 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="32bfa-109">Built-in ASP.NET Core Tag Helpers</span></span>

<span data-ttu-id="32bfa-110">**[앵커 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="32bfa-110">**[Anchor Tag Helper](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper)**</span></span>

<span data-ttu-id="32bfa-111">**[캐시 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="32bfa-111">**[Cache Tag Helper](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper)**</span></span>

<span data-ttu-id="32bfa-112">**[분산 캐시 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="32bfa-112">**[Distributed Cache Tag Helper](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper)**</span></span>

<span data-ttu-id="32bfa-113">**[환경 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="32bfa-113">**[Environment Tag Helper](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper)**</span></span>

[comment]: **[FormActionTagHelper](xref:mvc/views/tag-helpers/builtin-th/form-action-tag-helper)**

<span data-ttu-id="32bfa-114">**[폼 태그 도우미](xref:mvc/views/working-with-forms#the-form-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="32bfa-114">**[Form Tag Helper](xref:mvc/views/working-with-forms#the-form-tag-helper)**</span></span>

<span data-ttu-id="32bfa-115">**[이미지 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/image-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="32bfa-115">**[Image Tag Helper](xref:mvc/views/tag-helpers/builtin-th/image-tag-helper)**</span></span>

<span data-ttu-id="32bfa-116">**[입력 태그 도우미](xref:mvc/views/working-with-forms#the-input-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="32bfa-116">**[Input Tag Helper](xref:mvc/views/working-with-forms#the-input-tag-helper)**</span></span>

<span data-ttu-id="32bfa-117">**[레이블 태그 도우미](xref:mvc/views/working-with-forms#the-label-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="32bfa-117">**[Label Tag Helper](xref:mvc/views/working-with-forms#the-label-tag-helper)**</span></span>

[comment]: **[LinkTagHelper](xref:mvc/views/tag-helpers/builtin-th/link-tag-helper)**

[comment]: **[OptionTagHelper](xref:mvc/views/tag-helpers/builtin-th/option-tag-helper)**

[comment]: **[ScriptTagHelper](xref:mvc/views/tag-helpers/builtin-th/script-tag-helper)**

<span data-ttu-id="32bfa-118">**[부분 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="32bfa-118">**[Partial Tag Helper](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper)**</span></span>

<span data-ttu-id="32bfa-119">**[선택 태그 도우미](xref:mvc/views/working-with-forms#the-select-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="32bfa-119">**[Select Tag Helper](xref:mvc/views/working-with-forms#the-select-tag-helper)**</span></span>

<span data-ttu-id="32bfa-120">**[텍스트 영역 태그 도우미](xref:mvc/views/working-with-forms#the-textarea-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="32bfa-120">**[Textarea Tag Helper](xref:mvc/views/working-with-forms#the-textarea-tag-helper)**</span></span>

<span data-ttu-id="32bfa-121">**[유효성 검사 메시지 태그 도우미](xref:mvc/views/working-with-forms#the-validation-message-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="32bfa-121">**[Validation Message Tag Helper](xref:mvc/views/working-with-forms#the-validation-message-tag-helper)**</span></span>

<span data-ttu-id="32bfa-122">**[유효성 검사 요약 태그 도우미](xref:mvc/views/working-with-forms#the-validation-summary-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="32bfa-122">**[Validation Summary Tag Helper](xref:mvc/views/working-with-forms#the-validation-summary-tag-helper)**</span></span>

## <a name="additional-resources"></a><span data-ttu-id="32bfa-123">추가 자료</span><span class="sxs-lookup"><span data-stu-id="32bfa-123">Additional resources</span></span>

* [<span data-ttu-id="32bfa-124">클라이언트 쪽 개발</span><span class="sxs-lookup"><span data-stu-id="32bfa-124">Client-side development</span></span>](xref:client-side/index)
* [<span data-ttu-id="32bfa-125">태그 도우미</span><span class="sxs-lookup"><span data-stu-id="32bfa-125">Tag Helpers</span></span>](xref:mvc/views/tag-helpers/intro)
