---
title: 기본 제공 ASP.NET Core 태그 도우미
author: pkellner
description: 기본 제공 ASP.NET Core 태그 도우미에서 생산성을 향상시키는 방법을 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 10/10/2018
uid: mvc/views/tag-helpers/builtin-th/Index
ms.openlocfilehash: 9cca912f43159e778a4c9419e6171f06b4037b8b
ms.sourcegitcommit: 036d4b03fd86ca5bb378198e29ecf2704257f7b2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/05/2019
ms.locfileid: "57346017"
---
# <a name="aspnet-core-built-in-tag-helpers"></a><span data-ttu-id="4c361-103">기본 제공 ASP.NET Core 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="4c361-103">ASP.NET Core built-in Tag Helpers</span></span>

<span data-ttu-id="4c361-104">작성자: [Peter Kellner](http://peterkellner.net)</span><span class="sxs-lookup"><span data-stu-id="4c361-104">By [Peter Kellner](http://peterkellner.net)</span></span>

<span data-ttu-id="4c361-105">태그 도우미에 대한 개요는 <xref:mvc/views/tag-helpers/intro>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4c361-105">For an overview of Tag Helpers, see <xref:mvc/views/tag-helpers/intro>.</span></span>

> [!NOTE]
> <span data-ttu-id="4c361-106">문서에서 설명하지 않는 기본 제공된 태그 도우미가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c361-106">There are built-in Tag Helpers which aren't described in the documentation.</span></span> <span data-ttu-id="4c361-107">이러한 태그 도우미는 [Razor](xref:mvc/views/razor) 뷰 엔진에서 내부적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c361-107">These Tag Helpers are used internally by the [Razor](xref:mvc/views/razor) view engine.</span></span> <span data-ttu-id="4c361-108">여기에는 웹 사이트의 루트 경로로 확장되는 `~`(물결표) 문자의 태그 도우미가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c361-108">This includes a Tag Helper for the `~` (tilde) character, which expands to the root path of the website.</span></span>

## <a name="built-in-aspnet-core-tag-helpers"></a><span data-ttu-id="4c361-109">기본 제공 ASP.NET Core 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="4c361-109">Built-in ASP.NET Core Tag Helpers</span></span>

<span data-ttu-id="4c361-110">**[앵커 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="4c361-110">**[Anchor Tag Helper](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper)**</span></span>

<span data-ttu-id="4c361-111">**[캐시 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="4c361-111">**[Cache Tag Helper](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper)**</span></span>

<span data-ttu-id="4c361-112">**[분산 캐시 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="4c361-112">**[Distributed Cache Tag Helper](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper)**</span></span>

<span data-ttu-id="4c361-113">**[환경 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="4c361-113">**[Environment Tag Helper](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper)**</span></span>

[comment]: **[FormActionTagHelper](xref:mvc/views/tag-helpers/builtin-th/form-action-tag-helper)**

<span data-ttu-id="4c361-114">**[폼 태그 도우미](xref:mvc/views/working-with-forms#the-form-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="4c361-114">**[Form Tag Helper](xref:mvc/views/working-with-forms#the-form-tag-helper)**</span></span>

<span data-ttu-id="4c361-115">**[양식 작업 태그 도우미](xref:mvc/views/working-with-forms#the-form-action-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="4c361-115">**[Form Action Tag Helper](xref:mvc/views/working-with-forms#the-form-action-tag-helper)**</span></span>

<span data-ttu-id="4c361-116">**[이미지 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/image-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="4c361-116">**[Image Tag Helper](xref:mvc/views/tag-helpers/builtin-th/image-tag-helper)**</span></span>

<span data-ttu-id="4c361-117">**[입력 태그 도우미](xref:mvc/views/working-with-forms#the-input-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="4c361-117">**[Input Tag Helper](xref:mvc/views/working-with-forms#the-input-tag-helper)**</span></span>

<span data-ttu-id="4c361-118">**[레이블 태그 도우미](xref:mvc/views/working-with-forms#the-label-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="4c361-118">**[Label Tag Helper](xref:mvc/views/working-with-forms#the-label-tag-helper)**</span></span>

[comment]: **[LinkTagHelper](xref:mvc/views/tag-helpers/builtin-th/link-tag-helper)**

[comment]: **[OptionTagHelper](xref:mvc/views/tag-helpers/builtin-th/option-tag-helper)**

[comment]: **[ScriptTagHelper](xref:mvc/views/tag-helpers/builtin-th/script-tag-helper)**

<span data-ttu-id="4c361-119">**[부분 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="4c361-119">**[Partial Tag Helper](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper)**</span></span>

<span data-ttu-id="4c361-120">**[선택 태그 도우미](xref:mvc/views/working-with-forms#the-select-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="4c361-120">**[Select Tag Helper](xref:mvc/views/working-with-forms#the-select-tag-helper)**</span></span>

<span data-ttu-id="4c361-121">**[텍스트 영역 태그 도우미](xref:mvc/views/working-with-forms#the-textarea-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="4c361-121">**[Textarea Tag Helper](xref:mvc/views/working-with-forms#the-textarea-tag-helper)**</span></span>

<span data-ttu-id="4c361-122">**[유효성 검사 메시지 태그 도우미](xref:mvc/views/working-with-forms#the-validation-message-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="4c361-122">**[Validation Message Tag Helper](xref:mvc/views/working-with-forms#the-validation-message-tag-helper)**</span></span>

<span data-ttu-id="4c361-123">**[유효성 검사 요약 태그 도우미](xref:mvc/views/working-with-forms#the-validation-summary-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="4c361-123">**[Validation Summary Tag Helper](xref:mvc/views/working-with-forms#the-validation-summary-tag-helper)**</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4c361-124">추가 자료</span><span class="sxs-lookup"><span data-stu-id="4c361-124">Additional resources</span></span>

* <xref:mvc/views/tag-helpers/intro>
* <xref:mvc/views/tag-helpers/th-components>
