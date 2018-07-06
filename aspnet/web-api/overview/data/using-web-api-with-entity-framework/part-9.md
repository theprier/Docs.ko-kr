---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-9
title: 데이터베이스에 새 항목 추가 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
ms.date: 06/16/2014
ms.assetid: 0967c29e-e124-4db0-a788-c45d0ff5aff2
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-9
msc.type: authoredcontent
ms.openlocfilehash: 36251ba907a6f580b63f0fded0591c26b6ff879e
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37818510"
---
<a name="add-a-new-item-to-the-database"></a><span data-ttu-id="85c2e-102">데이터베이스에 새 항목 추가</span><span class="sxs-lookup"><span data-stu-id="85c2e-102">Add a New Item to the Database</span></span>
====================
<span data-ttu-id="85c2e-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="85c2e-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="85c2e-104">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="85c2e-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="85c2e-105">이 섹션에서는 사용자가 새 책을 만들 수 있는 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c2e-105">In this section, you will add the ability for users to create a new book.</span></span> <span data-ttu-id="85c2e-106">App.js에서 다음 코드는 보기 모델에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c2e-106">In app.js, add the following code to the view model:</span></span>

[!code-javascript[Main](part-9/samples/sample1.js)]

<span data-ttu-id="85c2e-107">Index.cshtml에서 다음 태그를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="85c2e-107">In Index.cshtml, replace the following markup:</span></span>

[!code-html[Main](part-9/samples/sample2.html)]

<span data-ttu-id="85c2e-108">바꿀 대상:</span><span class="sxs-lookup"><span data-stu-id="85c2e-108">With:</span></span>

[!code-html[Main](part-9/samples/sample3.html)]

<span data-ttu-id="85c2e-109">이 태그에는 새 author 제출 하기 위한 양식을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="85c2e-109">This markup creates a form for submitting a new author.</span></span> <span data-ttu-id="85c2e-110">작성자 드롭 다운 목록에 대 한 값은 데이터 바인딩된은 `authors` 보기 모델의 observable입니다.</span><span class="sxs-lookup"><span data-stu-id="85c2e-110">The values for the author drop-down list are data-bound to the `authors` observable in the view model.</span></span> <span data-ttu-id="85c2e-111">다른 폼 입력에 대 한 값은 데이터 바인딩된은 `newBook` 보기 모델의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="85c2e-111">For the other form inputs, the values are data-bound to the `newBook` property of the view model.</span></span>

<span data-ttu-id="85c2e-112">폼의 제출 처리기 바인딩되는 `addBook` 함수:</span><span class="sxs-lookup"><span data-stu-id="85c2e-112">The submit handler on the form is bound to the `addBook` function:</span></span>

[!code-html[Main](part-9/samples/sample4.html)]

<span data-ttu-id="85c2e-113">`addBook` 함수는 JSON 개체를 만드는 데 데이터 바인딩된 폼 입력의 현재 값을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="85c2e-113">The `addBook` function reads the current values of the data-bound form inputs to create a JSON object.</span></span> <span data-ttu-id="85c2e-114">JSON 개체를 게시 한 다음 `/api/books`합니다.</span><span class="sxs-lookup"><span data-stu-id="85c2e-114">Then it POSTs the JSON object to `/api/books`.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="85c2e-115">[이전](part-8.md)
> [다음](part-10.md)</span><span class="sxs-lookup"><span data-stu-id="85c2e-115">[Previous](part-8.md)
[Next](part-10.md)</span></span>
