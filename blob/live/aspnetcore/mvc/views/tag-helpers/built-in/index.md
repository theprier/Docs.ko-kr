---
title: "기본 제공 ASP.NET Core 태그 도우미"
author: pkellner
description: "기본 제공 ASP.NET Core 태그 도우미"
keywords: "ASP.NET Core, 태그 도우미"
ms.author: riande
manager: wpickett
ms.date: 09/13/2017
ms.topic: article
ms.technology: aspnet
ms.prod: aspnet-core
uid: mvc/views/tag-helpers/builtin-th/Index
ms.openlocfilehash: dd732822a715df19c0ee4b6accad3455ad6537da
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
# <a name="aspnet-core-built-in-tag-helpers"></a><span data-ttu-id="caae6-104">기본 제공 ASP.NET Core 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="caae6-104">ASP.NET Core built-in Tag Helpers</span></span>

<span data-ttu-id="caae6-105">작성자: [Peter Kellner](http://peterkellner.net)</span><span class="sxs-lookup"><span data-stu-id="caae6-105">By [Peter Kellner](http://peterkellner.net)</span></span> 

<span data-ttu-id="caae6-106">ASP.NET Core에는 생산성을 향상하기 위해 다양한 기본 제공 태그 도우미가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="caae6-106">ASP.NET Core includes many built-in Tag Helpers to boost your productivity.</span></span> <span data-ttu-id="caae6-107">이 섹션에서는 기본 제공 태그 도우미의 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="caae6-107">This section provides an overview of the built-in Tag Helpers.</span></span>

> [!NOTE]
> <span data-ttu-id="caae6-108">[Razor](xref:mvc/views/razor) 뷰 엔진에서 내부적으로 사용하기 때문에 다루지 않는 기본 제공 태그 도우미도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="caae6-108">There are built-in Tag Helpers which aren't discussed, since they're used internally by the [Razor](xref:mvc/views/razor) view engine.</span></span> <span data-ttu-id="caae6-109">여기에는 웹 사이트의 루트 경로로 확장되는 ~ 문자의 태그 도우미가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="caae6-109">This includes a Tag Helper for the ~ character, which expands to the root path of the website.</span></span>

## <a name="built-in-aspnet-core-tag-helpers"></a><span data-ttu-id="caae6-110">기본 제공 ASP.NET Core 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="caae6-110">Built-in ASP.NET Core Tag Helpers</span></span>

<span data-ttu-id="caae6-111">**[앵커 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="caae6-111">**[Anchor Tag Helper](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper)**</span></span>

<span data-ttu-id="caae6-112">**[캐시 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="caae6-112">**[Cache Tag Helper](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper)**</span></span>

<span data-ttu-id="caae6-113">**[분산 캐시 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="caae6-113">**[Distributed Cache Tag Helper](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper)**</span></span>

<span data-ttu-id="caae6-114">**[환경 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="caae6-114">**[Environment Tag Helper](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper)**</span></span>

[comment]: **[FormActionTagHelper](xref:mvc/views/tag-helpers/builtin-th/form-action-tag-helper)**

<span data-ttu-id="caae6-115">**[폼 태그 도우미](xref:mvc/views/working-with-forms#the-form-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="caae6-115">**[Form Tag Helper](xref:mvc/views/working-with-forms#the-form-tag-helper)**</span></span>

<span data-ttu-id="caae6-116">**[이미지 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/image-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="caae6-116">**[Image Tag Helper](xref:mvc/views/tag-helpers/builtin-th/image-tag-helper)**</span></span>

<span data-ttu-id="caae6-117">**[입력 태그 도우미](xref:mvc/views/working-with-forms#the-input-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="caae6-117">**[Input Tag Helper](xref:mvc/views/working-with-forms#the-input-tag-helper)**</span></span>

<span data-ttu-id="caae6-118">**[레이블 태그 도우미](xref:mvc/views/working-with-forms#the-label-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="caae6-118">**[Label Tag Helper](xref:mvc/views/working-with-forms#the-label-tag-helper)**</span></span>

[comment]: **[LinkTagHelper](xref:mvc/views/tag-helpers/builtin-th/link-tag-helper)**

[comment]: **[OptionTagHelper](xref:mvc/views/tag-helpers/builtin-th/option-tag-helper)**

[comment]: **[ScriptTagHelper](xref:mvc/views/tag-helpers/builtin-th/script-tag-helper)**

<span data-ttu-id="caae6-119">**[선택 태그 도우미](xref:mvc/views/working-with-forms#the-select-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="caae6-119">**[Select Tag Helper](xref:mvc/views/working-with-forms#the-select-tag-helper)**</span></span>

<span data-ttu-id="caae6-120">**[텍스트 영역 태그 도우미](xref:mvc/views/working-with-forms#the-textarea-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="caae6-120">**[Textarea Tag Helper](xref:mvc/views/working-with-forms#the-textarea-tag-helper)**</span></span>

<span data-ttu-id="caae6-121">**[유효성 검사 메시지 태그 도우미](xref:mvc/views/working-with-forms#the-validation-message-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="caae6-121">**[Validation Message Tag Helper](xref:mvc/views/working-with-forms#the-validation-message-tag-helper)**</span></span>

<span data-ttu-id="caae6-122">**[유효성 검사 요약 태그 도우미](xref:mvc/views/working-with-forms#the-validation-summary-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="caae6-122">**[Validation Summary Tag Helper](xref:mvc/views/working-with-forms#the-validation-summary-tag-helper)**</span></span>

## <a name="additional-resources"></a><span data-ttu-id="caae6-123">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="caae6-123">Additional resources</span></span>

* [<span data-ttu-id="caae6-124">클라이언트 쪽 개발</span><span class="sxs-lookup"><span data-stu-id="caae6-124">Client-Side Development</span></span>](xref:client-side/index)
* [<span data-ttu-id="caae6-125">태그 도우미</span><span class="sxs-lookup"><span data-stu-id="caae6-125">Tag Helpers</span></span>](xref:mvc/views/tag-helpers/intro)
