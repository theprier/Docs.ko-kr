---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-9
title: "데이터베이스에 새 항목 추가 | Microsoft Docs"
author: MikeWasson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/16/2014
ms.topic: article
ms.assetid: 0967c29e-e124-4db0-a788-c45d0ff5aff2
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-9
msc.type: authoredcontent
ms.openlocfilehash: d33355b1bd286513958f71ce5521942a6cbb584f
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="add-a-new-item-to-the-database"></a><span data-ttu-id="30da5-102">데이터베이스에 새 항목 추가</span><span class="sxs-lookup"><span data-stu-id="30da5-102">Add a New Item to the Database</span></span>
====================
<span data-ttu-id="30da5-103">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="30da5-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="30da5-104">완료 된 프로젝트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="30da5-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="30da5-105">이 섹션에서는 새 책을 만들 수 있는 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="30da5-105">In this section, you will add the ability for users to create a new book.</span></span> <span data-ttu-id="30da5-106">App.js의 보기 모델에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="30da5-106">In app.js, add the following code to the view model:</span></span>

[!code-javascript[Main](part-9/samples/sample1.js)]

<span data-ttu-id="30da5-107">Index.cshtml에서 태그를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="30da5-107">In Index.cshtml, replace the following markup:</span></span>

[!code-html[Main](part-9/samples/sample2.html)]

<span data-ttu-id="30da5-108">코드로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="30da5-108">With:</span></span>

[!code-html[Main](part-9/samples/sample3.html)]

<span data-ttu-id="30da5-109">이 태그에는 새 author 전송에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30da5-109">This markup creates a form for submitting a new author.</span></span> <span data-ttu-id="30da5-110">작성자 드롭 다운 목록에 대 한 값은 데이터 바인딩된은 `authors` 보기 모델에 예측 가능한 합니다.</span><span class="sxs-lookup"><span data-stu-id="30da5-110">The values for the author drop-down list are data-bound to the `authors` observable in the view model.</span></span> <span data-ttu-id="30da5-111">다른 폼 입력에 대 한 값은 데이터 바인딩된은 `newBook` 보기 모델의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="30da5-111">For the other form inputs, the values are data-bound to the `newBook` property of the view model.</span></span>

<span data-ttu-id="30da5-112">폼에 전송 처리기에 바인딩된는 `addBook` 함수:</span><span class="sxs-lookup"><span data-stu-id="30da5-112">The submit handler on the form is bound to the `addBook` function:</span></span>

[!code-html[Main](part-9/samples/sample4.html)]

<span data-ttu-id="30da5-113">`addBook` 함수는 JSON 개체를 만드는 데 데이터 바인딩된 폼 입력의 현재 값을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="30da5-113">The `addBook` function reads the current values of the data-bound form inputs to create a JSON object.</span></span> <span data-ttu-id="30da5-114">JSON 개체를 게시 한 다음 `/api/books`합니다.</span><span class="sxs-lookup"><span data-stu-id="30da5-114">Then it POSTs the JSON object to `/api/books`.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="30da5-115">[이전](part-8.md)
[다음](part-10.md)</span><span class="sxs-lookup"><span data-stu-id="30da5-115">[Previous](part-8.md)
[Next](part-10.md)</span></span>
