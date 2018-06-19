---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/index
title: 편집, 삽입 및 데이터를 삭제 합니다. | Microsoft Docs
author: rick-anderson
description: 이 자습서에 BLL 메서드에 ObjectDataSource 컨트롤의 메서드를 매핑하는 방법 및 GridView, DetailsView, 및 FormView co를 구성 하는 방법을 표시 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/05/2011
ms.topic: article
ms.assetid: 9fc60498-ced4-47c6-b2cf-8d464e6aeef8
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data
msc.type: chapter
ms.openlocfilehash: 424781d445443ff2df3b5fda359dadc5243e1ea9
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
ms.locfileid: "26513812"
---
<a name="editing-inserting-and-deleting-data"></a><span data-ttu-id="a7813-103">편집, 삽입 및 데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="a7813-103">Editing, Inserting, and Deleting Data</span></span>
====================
> <span data-ttu-id="a7813-104">이 자습서에 GridView DetailsView를 구성 하는 방법 및 BLL 메서드에 ObjectDataSource 컨트롤의 메서드를 매핑하는 방법을 나타나고 FormView 제어 사용자가 데이터를 수정할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7813-104">In these tutorials you see how to map methods of the ObjectDataSource control to BLL methods, and how to configure the GridView, DetailsView, and FormView controls to let users modify data.</span></span>


- [<span data-ttu-id="a7813-105">삽입, 업데이트 및 삭제 (C#)의 개요</span><span class="sxs-lookup"><span data-stu-id="a7813-105">Overview of Inserting, Updating, and Deleting Data (C#)</span></span>](an-overview-of-inserting-updating-and-deleting-data-cs.md)
- [<span data-ttu-id="a7813-106">삽입, 업데이트 및 삭제 (C#)와 연결 된 이벤트를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7813-106">Examining the Events Associated with Inserting, Updating, and Deleting (C#)</span></span>](examining-the-events-associated-with-inserting-updating-and-deleting-cs.md)
- [<span data-ttu-id="a7813-107">ASP.NET 페이지 (C#)의 BLL 및 DAL 수준의 예외 처리</span><span class="sxs-lookup"><span data-stu-id="a7813-107">Handling BLL- and DAL-Level Exceptions in an ASP.NET Page (C#)</span></span>](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md)
- [<span data-ttu-id="a7813-108">편집을 유효성 검사 컨트롤을 추가 하 고 삽입 인터페이스 (C#)</span><span class="sxs-lookup"><span data-stu-id="a7813-108">Adding Validation Controls to the Editing and Inserting Interfaces (C#)</span></span>](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs.md)
- [<span data-ttu-id="a7813-109">데이터 수정 인터페이스 (C#)를 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="a7813-109">Customizing the Data Modification Interface (C#)</span></span>](customizing-the-data-modification-interface-cs.md)
- [<span data-ttu-id="a7813-110">낙관적 동시성 (C#) 구현</span><span class="sxs-lookup"><span data-stu-id="a7813-110">Implementing Optimistic Concurrency (C#)</span></span>](implementing-optimistic-concurrency-cs.md)
- [<span data-ttu-id="a7813-111">클라이언트 쪽 확인 (C#)을 삭제할 때 추가</span><span class="sxs-lookup"><span data-stu-id="a7813-111">Adding Client-Side Confirmation When Deleting (C#)</span></span>](adding-client-side-confirmation-when-deleting-cs.md)
- [<span data-ttu-id="a7813-112">사용자 (C#)에 따라 데이터 수정 기능 제한</span><span class="sxs-lookup"><span data-stu-id="a7813-112">Limiting Data Modification Functionality Based on the User (C#)</span></span>](limiting-data-modification-functionality-based-on-the-user-cs.md)
- [<span data-ttu-id="a7813-113">삽입, 업데이트 및 삭제 (VB)의 개요</span><span class="sxs-lookup"><span data-stu-id="a7813-113">Overview of Inserting, Updating, and Deleting Data (VB)</span></span>](an-overview-of-inserting-updating-and-deleting-data-vb.md)
- [<span data-ttu-id="a7813-114">삽입, 업데이트 및 삭제 (VB)와 연결 된 이벤트를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7813-114">Examining the Events Associated with Inserting, Updating, and Deleting (VB)</span></span>](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md)
- [<span data-ttu-id="a7813-115">ASP.NET 페이지 (VB)에서 BLL 및 DAL 수준의 예외 처리</span><span class="sxs-lookup"><span data-stu-id="a7813-115">Handling BLL- and DAL-Level Exceptions in an ASP.NET Page (VB)</span></span>](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb.md)
- [<span data-ttu-id="a7813-116">편집을 유효성 검사 컨트롤을 추가 하 고 인터페이스 (VB)를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7813-116">Adding Validation Controls to the Editing and Inserting Interfaces (VB)</span></span>](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md)
- [<span data-ttu-id="a7813-117">데이터 수정 인터페이스 (VB) 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="a7813-117">Customizing the Data Modification Interface (VB)</span></span>](customizing-the-data-modification-interface-vb.md)
- [<span data-ttu-id="a7813-118">낙관적 동시성 (VB) 구현</span><span class="sxs-lookup"><span data-stu-id="a7813-118">Implementing Optimistic Concurrency (VB)</span></span>](implementing-optimistic-concurrency-vb.md)
- [<span data-ttu-id="a7813-119">클라이언트 쪽 확인 (VB)를 삭제할 때 추가</span><span class="sxs-lookup"><span data-stu-id="a7813-119">Adding Client-Side Confirmation When Deleting (VB)</span></span>](adding-client-side-confirmation-when-deleting-vb.md)
- [<span data-ttu-id="a7813-120">사용자 (VB)에 따라 데이터 수정 기능 제한</span><span class="sxs-lookup"><span data-stu-id="a7813-120">Limiting Data Modification Functionality Based on the User (VB)</span></span>](limiting-data-modification-functionality-based-on-the-user-vb.md)
