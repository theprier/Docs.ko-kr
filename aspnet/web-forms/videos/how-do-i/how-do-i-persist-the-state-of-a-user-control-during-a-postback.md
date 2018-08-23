---
uid: web-forms/videos/how-do-i/how-do-i-persist-the-state-of-a-user-control-during-a-postback
title: '[How Do I]: Persist the State of a User Control During a Postback | Microsoft Docs'
author: rick-anderson
description: 이 비디오 Chris Pels 사용자 컨트롤에 하나 이상의 개체의 상태를 유지 하는 방법을 보여 줍니다. 먼저는 abilit 나타내는 사용자 컨트롤을 만들...
ms.author: riande
ms.date: 04/02/2009
ms.assetid: d1bca4c6-838c-40f7-87ec-80bb67e483e5
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-persist-the-state-of-a-user-control-during-a-postback
msc.type: video
ms.openlocfilehash: b15eef0af3e88f8ca333d9661c5d42a1dbc90151
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41831885"
---
<a name="how-do-i-persist-the-state-of-a-user-control-during-a-postback"></a>[방법]: 포스트백 하는 동안 사용자 정의 컨트롤의 상태를 유지 합니다.
[How Do I]: Persist the State of a User Control During a Postback
====================
<span data-ttu-id="77bb2-104">[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="77bb2-104">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="77bb2-105">이 비디오 Chris Pels 사용자 컨트롤에 하나 이상의 개체의 상태를 유지 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="77bb2-105">In this video Chris Pels shows how to persist the state of one or more objects in a user control.</span></span> <span data-ttu-id="77bb2-106">첫째, 사용자 검색에 대 한 필터 조건을 지정 하는 기능을 나타내는 사용자 정의 컨트롤을 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="77bb2-106">First, a user control is created that represents the ability for a user to specify filter criteria for a search.</span></span> <span data-ttu-id="77bb2-107">또한 필터 클래스과 함께 필터 정보를 저장할 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="77bb2-107">In addition, a companion Filter class is created to store the filter information.</span></span> <span data-ttu-id="77bb2-108">여러 사용자 인터페이스 요소와 함께 일부 메서드 및 필터 클래스 인스턴스에서 현재 필터 정보를 저장 하는 속성 필터 컨트롤에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="77bb2-108">Several user interface elements are added to the filter control along with some methods and properties to store the current filter information in the Filter class instance.</span></span> <span data-ttu-id="77bb2-109">다음으로, 사용자 컨트롤 지 속성 RegisterRequiresControlState 메서드 및 연결 된 저장 또는 복원할 메서드를 사용 하 여 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="77bb2-109">Next, the user control persistence is implemented using the RegisterRequiresControlState method and associated Save/Restore methods.</span></span> <span data-ttu-id="77bb2-110">이러한 메서드는 페이지 포스트백 중 필터 클래스 및 해당 데이터의 인스턴스를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="77bb2-110">These methods store the instance of the filter class and its data during page postbacks.</span></span> <span data-ttu-id="77bb2-111">마지막으로 컨트롤 상태 구현에 여러 개체를 저장 하는 방법 설명 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="77bb2-111">Finally, there is a discussion of how to store multiple objects in control state implementation.</span></span>

[<span data-ttu-id="77bb2-112">&#9654;비디오 (23 분)</span><span class="sxs-lookup"><span data-stu-id="77bb2-112">&#9654; Watch video (23 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-persist-the-state-of-a-user-control-during-a-postback)
