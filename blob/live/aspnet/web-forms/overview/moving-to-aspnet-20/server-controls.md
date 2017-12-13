---
uid: web-forms/overview/moving-to-aspnet-20/server-controls
title: "서버 컨트롤 | Microsoft Docs"
author: microsoft
description: "ASP.NET 2.0에는 여러 가지 방법으로 서버 컨트롤을 향상 시킵니다. 이 단원에서는 ASP.NET 2.0 방법 및 Visual Studio 200에 대 한 아키텍처 변경 사항 중 일부 설명 합니다..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2005
ms.topic: article
ms.assetid: 43f6ac47-76fc-4cf7-8e9f-c18ce673dfd8
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/server-controls
msc.type: authoredcontent
ms.openlocfilehash: 09f1a2e4de024e5778e69fdd691d9cb0040459f3
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="server-controls"></a><span data-ttu-id="15412-104">서버 컨트롤</span><span class="sxs-lookup"><span data-stu-id="15412-104">Server Controls</span></span>
====================
<span data-ttu-id="15412-105">여 [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="15412-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="15412-106">ASP.NET 2.0에는 여러 가지 방법으로 서버 컨트롤을 향상 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="15412-106">ASP.NET 2.0 enhances server controls in many ways.</span></span> <span data-ttu-id="15412-107">이 단원에서는 ASP.NET 2.0 하는 방법에 대 한 아키텍처 변경 사항 중 일부 다루게 될 것 및 Visual Studio 2005 서버 컨트롤을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-107">In this module, we'll cover some of the architectural changes to the way ASP.NET 2.0 and Visual Studio 2005 deals with server controls.</span></span>


<span data-ttu-id="15412-108">ASP.NET 2.0에는 여러 가지 방법으로 서버 컨트롤을 향상 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="15412-108">ASP.NET 2.0 enhances server controls in many ways.</span></span> <span data-ttu-id="15412-109">이 단원에서는 ASP.NET 2.0 하는 방법에 대 한 아키텍처 변경 사항 중 일부 다루게 될 것 및 Visual Studio 2005 서버 컨트롤을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-109">In this module, we'll cover some of the architectural changes to the way ASP.NET 2.0 and Visual Studio 2005 deals with server controls.</span></span>

## <a name="view-state"></a><span data-ttu-id="15412-110">상태 보기</span><span class="sxs-lookup"><span data-stu-id="15412-110">View state</span></span>

<span data-ttu-id="15412-111">뷰 상태에 ASP.NET 2.0의 주요 변경 작업은 크기가 크게 절감 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-111">The primary change in view state in ASP.NET 2.0 is a dramatic reduction in size.</span></span> <span data-ttu-id="15412-112">달력 컨트롤에 있는 페이지를 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-112">Consider a page with only a Calendar control on it.</span></span> <span data-ttu-id="15412-113">ASP.NET 1.1에서 뷰 상태 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-113">Here is the view state in ASP.NET 1.1.</span></span>

[!code-css[Main](server-controls/samples/sample1.css)]

<span data-ttu-id="15412-114">이제 여기는 보기 상태와 동일한 페이지에서 ASP.NET 2.0입니다.</span><span class="sxs-lookup"><span data-stu-id="15412-114">Now here's the view state on an identical page in ASP.NET 2.0.</span></span>

[!code-css[Main](server-controls/samples/sample2.css)]

<span data-ttu-id="15412-115">매우 중요 한 변경 된 주며 뷰 상태 연결을 통해 앞뒤로 수행을 고려이 변경 수 개발자 성능이 많이 향상 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-115">That's a pretty significant change, and considering that view state is carried back and forth over the wire, this change can give developers a significant performance increase.</span></span> <span data-ttu-id="15412-116">상태 보기의 크기를 줄이는 것 내부적으로 처리 하는 방식 때문 크게입니다.</span><span class="sxs-lookup"><span data-stu-id="15412-116">The reduction in size of view state is largely due to the way that we handle it internally.</span></span> <span data-ttu-id="15412-117">뷰 상태는 Base64 인코딩된 문자열을 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-117">Remember that view state is a Base64 encoded string.</span></span> <span data-ttu-id="15412-118">ASP.NET 2.0에서 뷰 상태 변경을 더 잘 이해 하려면 위 예제에서 디코딩된 값 살펴보겠습니다 죠.</span><span class="sxs-lookup"><span data-stu-id="15412-118">To better understand the change in view state in ASP.NET 2.0, let's have a look at the decoded values from the examples above.</span></span>

<span data-ttu-id="15412-119">디코딩된 1.1 뷰 상태는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-119">Here is the 1.1 view state decoded:</span></span>

[!code-css[Main](server-controls/samples/sample3.css)]

<span data-ttu-id="15412-120">이 값은 알 수 없는, 처럼 약간 보일 수 있지만 패턴을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-120">This may look a bit like gibberish, but there is a pattern here.</span></span> <span data-ttu-id="15412-121">ASP.NET에서 1.x에서는 사용 되지 않는 단일 문자 데이터 형식을 식별 하 고 사용 하 여 값을 구분는 &lt; &gt; 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="15412-121">In ASP.NET 1.x, we used single characters to identify data-types and delimited values using the &lt;&gt; characters.</span></span> <span data-ttu-id="15412-122">위의 보기 상태 예제에서 "t"는 세 개를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="15412-122">The "t" in the view state sample above represents a Triplet.</span></span> <span data-ttu-id="15412-123">세 개 포함 한 쌍의 ArrayLists ("l" ArrayList를 나타냅니다.) 이러한 ArrayLists 중 하나는 i n t 32에 포함 ("i") 값이 1과 다른 다른 세 개를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-123">The Triplet contains a pair of ArrayLists (the "l" represents an ArrayList.) One of those ArrayLists contains an Int32 ("i") with a value of 1 and the other contains another Triplet.</span></span> <span data-ttu-id="15412-124">세 개 ArrayLists 등 쌍을 포함 합니다. 쌍을 포함 하는 개가 형식이 사용, 우리에 문자를 통해 데이터 형식을 식별 하 고 사용 하 여 기억 하는 것이 중요은 &lt; 및 &gt; 문자 구분 기호로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-124">The Triplet contains a pair of ArrayLists, etc. The important thing to remember is that we use Triplets that contain pairs, we identify the data-types via a letter, and we use the &lt; and &gt; characters as delimiters.</span></span>

<span data-ttu-id="15412-125">ASP.NET 2.0에서 디코딩된 뷰 상태 약간 다르게 보입니다.</span><span class="sxs-lookup"><span data-stu-id="15412-125">In ASP.NET 2.0, the decoded view state looks a bit different.</span></span>

[!code-powershell[Main](server-controls/samples/sample4.ps1)]

<span data-ttu-id="15412-126">디코딩된 뷰 상태의 모양이 크게 변화를 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-126">You should notice a huge change in the appearance of the decoded view state.</span></span> <span data-ttu-id="15412-127">이러한 변경에 몇 가지 아키텍처 토대가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-127">This change has several architectural underpinnings.</span></span> <span data-ttu-id="15412-128">뷰 상태는 LosFormatter 데이터를 직렬화 하 1.x ASP.NET에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-128">View state in ASP.NET 1.x used the LosFormatter to serialize data.</span></span> <span data-ttu-id="15412-129">2.0에서는 새로운 ObjectStateFormatter 클래스를 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-129">In 2.0, we use the new ObjectStateFormatter class.</span></span> <span data-ttu-id="15412-130">이 클래스는 serialization 및 deserialization 상태 보기 상태와 컨트롤을 지원 하기 위해 특별히 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-130">This class was specifically designed to aid in the serialization and deserialization of view state and control state.</span></span> <span data-ttu-id="15412-131">(컨트롤 상태는 다음 섹션 살펴보겠습니다.) 기준인 serialization 및 deserialization을 수행 하는 방법을 변경 하 여 얻은 많은 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-131">(Control state will be covered in the next section.) There are many benefits gained by changing the method by which serialization and deserialization take place.</span></span> <span data-ttu-id="15412-132">가장 큰 중 하나는 TextWriter를 사용 하 여 LosFormatter 달리는 ObjectStateFormatter 사용 BinaryWriter 사실입니다.</span><span class="sxs-lookup"><span data-stu-id="15412-132">One of the most dramatic is the fact that unlike the LosFormatter which uses a TextWriter, the ObjectStateFormatter uses a BinaryWriter.</span></span> <span data-ttu-id="15412-133">따라서 ASP.NET 2.0 바이트 문자열 대신 일련 뷰 상태를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-133">This allows ASP.NET 2.0 to store view state a series of bytes instead of strings.</span></span> <span data-ttu-id="15412-134">예를 들어 정수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-134">Take, for example, an integer.</span></span> <span data-ttu-id="15412-135">ASP.NET 1.1 정수 4 바이트의 뷰 상태를 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-135">In ASP.NET 1.1, an integer required 4 bytes of view state.</span></span> <span data-ttu-id="15412-136">ASP.NET 2.0에서이 동일한 정수 1 바이트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-136">In ASP.NET 2.0, that same integer only requires 1 byte.</span></span> <span data-ttu-id="15412-137">저장 된 뷰 상태 불필요 한 다른 개선 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-137">Other enhancements were made to decrease the amount of view state that is stored.</span></span> <span data-ttu-id="15412-138">날짜/시간 값을 예를 들어 이제 저장 됩니다는 TickCount를 사용 하 여 문자열 대신.</span><span class="sxs-lookup"><span data-stu-id="15412-138">DateTime values, for example, are now stored using a TickCount instead of a string.</span></span>

<span data-ttu-id="15412-139">아직 충분 하지 그 하는 경우 특별히 주의 기울여야 DataGrid와 비슷한 컨트롤이 가장 큰 소비자 1.x에서 뷰 상태 중 하나에 팩트로 지불 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-139">As if all of that weren't enough, special attention was paid to the fact that one of the greatest consumers of view state in 1.x was the DataGrid and similar controls.</span></span> <span data-ttu-id="15412-140">같은 뷰 상태 관련 되어 DataGrid 컨트롤의 주요 단점은 대량의 반복 되는 정보가 종종 포함 한다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="15412-140">A major drawback of controls such as the DataGrid where view state is concerned is that it often contains large amounts of repeated information.</span></span> <span data-ttu-id="15412-141">ASP.NET에서 1.x 및에 비해 너무 커지면된 뷰 상태에 다시 결과 단순히 정보가 저장 된 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-141">In ASP.NET 1.x, that repeated information was simply stored over and over again resulting in a bloated view state.</span></span> <span data-ttu-id="15412-142">ASP.NET 2.0을 사용 하 여 새 IndexedString 클래스 이러한 데이터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-142">In ASP.NET 2.0, we use the new IndexedString class to store such data.</span></span> <span data-ttu-id="15412-143">문자열 반복 되는 경우는 IndexedString 및 IndexedString 개체의 실행 중인 테이블에서 인덱스에 대 한 토큰만 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-143">If a string repeats, we just store the token for the IndexedString and the index within a running table of IndexedString objects.</span></span>

## <a name="control-state"></a><span data-ttu-id="15412-144">컨트롤 상태</span><span class="sxs-lookup"><span data-stu-id="15412-144">Control State</span></span>

<span data-ttu-id="15412-145">뷰 상태와 함께 개발자 있던 주요 gripes 하나인 HTTP 페이로드를 추가 하는 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="15412-145">One of the major gripes that developers had with view state was the size that it added to the HTTP payload.</span></span> <span data-ttu-id="15412-146">에서 설명한 대로 DataGrid 컨트롤 뷰 상태의 가장 큰 소비자 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="15412-146">As previously mentioned, one of the greatest consumers of view state is the DataGrid control.</span></span> <span data-ttu-id="15412-147">많은 양의 DataGrid에 의해 생성 된 뷰 상태를 방지 하려면 많은 개발자에 게 해당 컨트롤에 대 한 뷰 상태를 단순히 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-147">To avoid the huge amounts of view state generated by a DataGrid, many developers simply disabled view state for that control.</span></span> <span data-ttu-id="15412-148">그러나 해당 솔루션에 적절 한 항상 없습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-148">Unfortunately, that solution wasn't always a good one.</span></span> <span data-ttu-id="15412-149">뷰 상태 1.x ASP.NET에서 컨트롤의 올바른 작동을 위해 필요한 데이터 뿐만 아니라를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-149">View state in ASP.NET 1.x contains not only data necessary for the correct functionality of the control.</span></span> <span data-ttu-id="15412-150">또한 컨트롤의 UI 상태에 대 한 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-150">It also contains information concerning the state of the control's UI.</span></span> <span data-ttu-id="15412-151">이 모든 UI 정보를 볼 필요가 없는 경우에 뷰 상태를 사용 하도록 설정 해야 DataGrid에 페이지 매김 허용 하려는 경우 상태 포함 되어 있음을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-151">This means that if you want to allow for pagination on a DataGrid, you must enable view state even if you don't need all of the UI information that view state contains.</span></span> <span data-ttu-id="15412-152">동작만 있는 시나리오는</span><span class="sxs-lookup"><span data-stu-id="15412-152">It's an all-or-nothing scenario.</span></span>

<span data-ttu-id="15412-153">ASP.NET 2.0 컨트롤 상태 컨트롤 상태의 도입을 통해 원활 하 게 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-153">In ASP.NET 2.0, control state solves that problem nicely via the introduction of control state.</span></span> <span data-ttu-id="15412-154">컨트롤 상태 컨트롤의 적절 한 기능에 반드시 필요한 데이터를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-154">Control state contains the data that is absolutely necessary for the proper functionality of a control.</span></span> <span data-ttu-id="15412-155">뷰 상태와는 달리 컨트롤 상태를 해제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-155">Unlike view state, control state cannot be disabled.</span></span> <span data-ttu-id="15412-156">따라서이 컨트롤 상태에 저장 되는 데이터 신중 하 게 제어는 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-156">Therefore, it is important that the data being stored in control state is carefully controlled.</span></span>

> [!NOTE]
> <span data-ttu-id="15412-157">제어 상태에서 뷰 상태와 함께 유지 되는 \_ \_VIEWSTATE 숨겨진된 양식 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="15412-157">Control state is persisted along with the view state in the \_\_VIEWSTATE hidden form field.</span></span>


<span data-ttu-id="15412-158">이 비디오는 상태 보기 상태와 컨트롤의 연습입니다.</span><span class="sxs-lookup"><span data-stu-id="15412-158">This video is a walkthrough of view state and control state.</span></span>


![](server-controls/_static/image1.png)


[<span data-ttu-id="15412-159">전체 화면 비디오 열기</span><span class="sxs-lookup"><span data-stu-id="15412-159">Open Full-Screen Video</span></span>](server-controls/_static/state1.wmv)


<span data-ttu-id="15412-160">읽기 / 쓰기 상태를 제어를 위해 서버 컨트롤에 대 한 순서로 세 단계를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-160">In order for a server control to read and write to control state, you must take three steps.</span></span>

## <a name="step-1-call-the-registerrequirescontrolstate-method"></a><span data-ttu-id="15412-161">1 단계: RegisterRequiresControlState 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-161">Step 1: Call the RegisterRequiresControlState Method</span></span>

<span data-ttu-id="15412-162">RegisterRequiresControlState 메서드 컨트롤 컨트롤 상태를 유지 해야 함을 ASP.NET에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="15412-162">The RegisterRequiresControlState method informs ASP.NET that a control needs to persist control state.</span></span> <span data-ttu-id="15412-163">컨트롤인 등록 되는 컨트롤 형식의 인수 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-163">It takes one argument of type Control which is the control that is being registered.</span></span>

<span data-ttu-id="15412-164">등록 요청 요청 지속 되지 않는 확인 하는 것이 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-164">It is important to note that registration does not persist from request to request.</span></span> <span data-ttu-id="15412-165">따라서이 메서드 컨트롤 상태를 유지 하는 컨트롤이 이면 모든 요청에 대해 호출 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-165">Therefore, this method must be called on every request if a control is to persist control state.</span></span> <span data-ttu-id="15412-166">OnInit에서 메서드를 호출 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-166">It is recommended that the method be called in OnInit.</span></span>

[!code-csharp[Main](server-controls/samples/sample5.cs)]

## <a name="step-2-override-savecontrolstate"></a><span data-ttu-id="15412-167">2 단계: SaveControlState 재정의</span><span class="sxs-lookup"><span data-stu-id="15412-167">Step 2: Override SaveControlState</span></span>

<span data-ttu-id="15412-168">SaveControlState 메서드 다시 마지막 게시 이후로 컨트롤 컨트롤에 대 한 상태 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-168">The SaveControlState method saves control state changes for a control since the last post back.</span></span> <span data-ttu-id="15412-169">컨트롤의 상태를 나타내는 개체를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-169">It returns an object representing the control's state.</span></span>

## <a name="step-3-override-loadcontrolstate"></a><span data-ttu-id="15412-170">3 단계: LoadControlState 재정의</span><span class="sxs-lookup"><span data-stu-id="15412-170">Step 3: Override LoadControlState</span></span>

<span data-ttu-id="15412-171">LoadControlState 메서드 컨트롤에 저장 된 상태를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-171">The LoadControlState method loads saved state into a control.</span></span> <span data-ttu-id="15412-172">메서드는 개체는 컨트롤에 대 한 저장된 된 상태를 보유 하는 형식의 인수 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-172">The method takes one argument of type Object which holds the saved state for the control.</span></span>

## <a name="full-xhtml-compliance"></a><span data-ttu-id="15412-173">전체 XHTML 규정 준수</span><span class="sxs-lookup"><span data-stu-id="15412-173">Full XHTML Compliance</span></span>

<span data-ttu-id="15412-174">모든 웹 개발자는 웹 응용 프로그램의 표준의 중요성을 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-174">Any Web developer knows the importance of standards in Web applications.</span></span> <span data-ttu-id="15412-175">표준 기반 개발 환경을 유지 하기 위해 ASP.NET 2.0은 XHTML 호환 완벽 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-175">In order to maintain a standards-based development environment, ASP.NET 2.0 is fully XHTML compliant.</span></span> <span data-ttu-id="15412-176">따라서 모든 태그는 HTML 4.0을 지 원하는 브라우저에서 XHTML 표준에 따라 렌더링 이상입니다.</span><span class="sxs-lookup"><span data-stu-id="15412-176">Therefore, all tags are rendered according to XHTML standards in browsers that support HTML 4.0 or greater.</span></span>

<span data-ttu-id="15412-177">ASP.NET 1.1에서 DOCTYPE 정의 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-177">The DOCTYPE definition in ASP.NET 1.1 was as follows:</span></span>

[!code-html[Main](server-controls/samples/sample6.html)]

<span data-ttu-id="15412-178">ASP.NET 2.0에서 기본 문서 종류 정의 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-178">In ASP.NET 2.0, the default DOCTYPE definition is as follows:</span></span>

[!code-html[Main](server-controls/samples/sample7.html)]

<span data-ttu-id="15412-179">를 선택한 경우에 구성 파일에서 xhtmlConformance 노드를 통해 기본 XHML 규정 준수를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-179">If you choose, you can alter the default XHML compliance via the xhtmlConformance node in the configuration file.</span></span> <span data-ttu-id="15412-180">예를 들어 web.config 파일에서 다음 노드 XHTML 1.0 Strict로 XHTML 규정 준수를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-180">For example, the following node in the web.config file will change XHTML compliance to XHTML 1.0 Strict:</span></span>

[!code-xml[Main](server-controls/samples/sample8.xml)]

<span data-ttu-id="15412-181">을 선택 하면 ASP.NET에서 사용 되는 레거시 구성을 사용 하려면 ASP.NET 구성할 수도 있습니다 다음과 같이 1.x:</span><span class="sxs-lookup"><span data-stu-id="15412-181">If you choose, you can also configure ASP.NET to use the legacy configuration used in ASP.NET 1.x as follows:</span></span>

[!code-xml[Main](server-controls/samples/sample9.xml)]

## <a name="adaptive-rendering-using-adapters"></a><span data-ttu-id="15412-182">어댑터를 사용 하 여 렌더링 적응</span><span class="sxs-lookup"><span data-stu-id="15412-182">Adaptive Rendering Using Adapters</span></span>

<span data-ttu-id="15412-183">ASP.NET에서 1.x, 포함 된 구성 파일을 &lt;browserCaps&gt; HttpBrowserCapabilities 개체를 채우는 섹션.</span><span class="sxs-lookup"><span data-stu-id="15412-183">In ASP.NET 1.x, the configuration file contained a &lt;browserCaps&gt; section that populated a HttpBrowserCapabilities object.</span></span> <span data-ttu-id="15412-184">이 개체는 개발자가 어떤 장치는 특정 요청을 수행할 결정 및 코드를 적절 하 게 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-184">This object allowed a developer to determine what device is making a particular request and render code appropriately.</span></span> <span data-ttu-id="15412-185">ASP.NET 2.0에서 모델이 개선 하 고 이제 새 ControlAdapter 클래스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-185">In ASP.NET 2.0, the model has improved and now uses the new ControlAdapter class.</span></span> <span data-ttu-id="15412-186">ControlAdapter 클래스는 컨트롤의 수명 주기에서 이벤트를 재정의 하 고 사용자 에이전트의 기능에 따라 컨트롤의 렌더링을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-186">The ControlAdapter class overrides events in the control's lifecycle and controls the rendering of controls based upon the user agent's capabilities.</span></span> <span data-ttu-id="15412-187">특정 사용자 에이전트의 기능에는 c:\windows\microsoft.net\framework\v2.0 저장 브라우저 정의 파일 (브라우저 파일 확장명으로 파일)에 정의 됩니다. \* \* \* \*\CONFIG\Browsers 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="15412-187">The capabilities of a specific user agent are defined by a browser definition file (a file with a .browser file extension) stored in the c:\windows\microsoft.net\framework\v2.0.\*\*\*\*\CONFIG\Browsers folder.</span></span>

> [!NOTE]
> <span data-ttu-id="15412-188">ControlAdapter 클래스는 추상 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="15412-188">The ControlAdapter class is an abstract class.</span></span>


<span data-ttu-id="15412-189">과 거의 동일한는 &lt;browserCaps&gt; 1.x 브라우저 정의 파일의에서 섹션을 요청 하는 브라우저를 식별 하기 위해 사용자 에이전트 문자열을 구문 분석 정규식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-189">Much like the &lt;browserCaps&gt; section in 1.x, the browser definition file uses a Regular Expression to parse the user agent string in order to identify the requesting browser.</span></span> <span data-ttu-id="15412-190">이 해당 사용자 에이전트에 대 한 특정 기능을 정의 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-190">It them defines particular capabilities for that user agent.</span></span> <span data-ttu-id="15412-191">ControlAdapter Render 메서드를 통해 컨트롤을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-191">The ControlAdapter renders the control via the Render method.</span></span> <span data-ttu-id="15412-192">따라서 Render 메서드를 재정의 하면에서 호출 하지 않아야 렌더링 기본 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="15412-192">Therefore, if you override the Render method, you should not call Render on the base class.</span></span> <span data-ttu-id="15412-193">이렇게 하면 어댑터에 대해 한 번씩 하 고 컨트롤 자체에 대 한 한 번, 두 번 발생 하도록 렌더링 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-193">Doing so may cause rendering to occur twice, once for the adapter and once for the control itself.</span></span>

## <a name="developing-a-custom-adapter"></a><span data-ttu-id="15412-194">사용자 지정 어댑터 개발</span><span class="sxs-lookup"><span data-stu-id="15412-194">Developing a Custom Adapter</span></span>

<span data-ttu-id="15412-195">ControlAdapter에서 상속 하 여 사용자 지정 어댑터를 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-195">You can develop your own custom adapter by inheriting from ControlAdapter.</span></span> <span data-ttu-id="15412-196">또한 어댑터는 페이지에 대 한 필요한 상황의 경우 PageAdapter 추상 클래스에서 상속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-196">Additionally, you can inherit from the abstract class PageAdapter in cases where an adapter is needed for a page.</span></span> <span data-ttu-id="15412-197">컨트롤을 사용자 지정 어댑터의 매핑을 통해 수행 됩니다는 &lt;controlAdapters&gt; 브라우저 정의 파일의 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="15412-197">Mapping of controls to your custom adapter is accomplished via the &lt;controlAdapters&gt; element in the browser definition file.</span></span> <span data-ttu-id="15412-198">예를 들어 브라우저 정의 파일에서 다음과 같은 XML 메뉴 어댑터 클래스에 메뉴 컨트롤을 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-198">For example, the following XML from a browser definition file maps the Menu control to the MenuAdapter class:</span></span>

[!code-html[Main](server-controls/samples/sample10.html)]

<span data-ttu-id="15412-199">컨트롤 개발자가 특정 장치 또는 브라우저를 대상에 대 한 매우 쉽게 됩니다이 모델을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-199">Using this model, it becomes quite easy for a control developer to target a particular device or browser.</span></span> <span data-ttu-id="15412-200">모든 장치에서 페이지가 렌더링 되는 방식을 완전히 제어 하는 개발자에 대 한 매우 간단 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-200">It's also quite simple for a developer to have complete control over how pages render on every device.</span></span>

## <a name="per-device-rendering"></a><span data-ttu-id="15412-201">장치 단위 렌더링</span><span class="sxs-lookup"><span data-stu-id="15412-201">Per-Device Rendering</span></span>

<span data-ttu-id="15412-202">ASP.NET 2.0에서 서버 컨트롤 속성에 지정 된 장치는 브라우저의 접두사를 사용 하 여 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-202">Server control properties in ASP.NET 2.0 can be specified per-device using a browser-specific prefix.</span></span> <span data-ttu-id="15412-203">예를 들어 아래 코드 페이지를 검색 하는 장치 사용량에 따라 레이블의 텍스트를 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15412-203">For example, the code below will change the Text of a label depending upon which device is being used to browse the page.</span></span>

[!code-aspx[Main](server-controls/samples/sample11.aspx)]

<span data-ttu-id="15412-204">레이블이 "탐색 하는 Internet Explorer에서." 라는 텍스트를 표시할 수 Internet Explorer에서이 레이블을 포함 하는 페이지를 찾아볼 때</span><span class="sxs-lookup"><span data-stu-id="15412-204">When the page containing this label is browsed from Internet Explorer, the label will display text saying "You are browsing from Internet Explorer."</span></span> <span data-ttu-id="15412-205">Firefox에서 페이지를 찾아볼 때는 표시 될 텍스트 "Firefox에서 이동 하는 있습니다."</span><span class="sxs-lookup"><span data-stu-id="15412-205">When the page is browsed from Firefox, the label will display the text "You are browsing from Firefox."</span></span> <span data-ttu-id="15412-206">다른 모든 장치에서 페이지를 찾아볼 때 표시될지 "알 수 없는 장치에서 이동 하는 있습니다."</span><span class="sxs-lookup"><span data-stu-id="15412-206">When the page is browsed from any other device, it will display "You are browsing from an unknown device."</span></span> <span data-ttu-id="15412-207">이 특수 구문을 사용 하 여 모든 속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-207">Any property can be specified using this special syntax.</span></span>

## <a name="setting-focus"></a><span data-ttu-id="15412-208">포커스 설정</span><span class="sxs-lookup"><span data-stu-id="15412-208">Setting Focus</span></span>

<span data-ttu-id="15412-209">ASP.NET 1.x 개발자가 특정 컨트롤에 초기 포커스를 설정 하는 방법에 대 한 질문과 대답입니다.</span><span class="sxs-lookup"><span data-stu-id="15412-209">ASP.NET 1.x developers frequently asked about how to set initial focus on a particular control.</span></span> <span data-ttu-id="15412-210">예를 들어 로그인 페이지에서 페이지 처음 로드 될 때 포커스를 가져올 사용자 ID 텍스트 상자에 있어야는 것이 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-210">For example, on a login page, it's useful to have the User ID textbox get the focus when the page first loads.</span></span> <span data-ttu-id="15412-211">ASP.NET이 1.x 일부 클라이언트 쪽 스크립트를 작성할 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-211">In ASP.NET 1.x, doing this required writing some client-side script.</span></span> <span data-ttu-id="15412-212">이러한 스크립트는 간단한 작업이, 이지만 SetFocus 메서드 덕분에 ASP.NET 2.0에서 필요는 더 이상입니다.</span><span class="sxs-lookup"><span data-stu-id="15412-212">Even though such a script is a trivial task, it's no longer necessary in ASP.NET 2.0 thanks to the SetFocus method.</span></span> <span data-ttu-id="15412-213">SetFocus 메서드 포커스 받아야 하는 제어를 표시 하는 하나의 인수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-213">The SetFocus method takes one argument indicating the control that should receive focus.</span></span> <span data-ttu-id="15412-214">이 인수를 문자열로 컨트롤의 클라이언트 ID 또는 제어 개체로 서버 컨트롤의 이름을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-214">This argument can either be the client ID of the control as a string or the name of the Server control as a Control object.</span></span> <span data-ttu-id="15412-215">예를 들어 초기 포커스 페이지가 처음 로드 될 때 txtUserID 호출 TextBox 컨트롤을 설정 하려면 페이지에 다음 코드 추가\_부하:</span><span class="sxs-lookup"><span data-stu-id="15412-215">For example, to set the initial focus to a TextBox control called txtUserID when the page first loads, add the following code to Page\_Load:</span></span>

[!code-csharp[Main](server-controls/samples/sample12.cs)]

<span data-ttu-id="15412-216">-또는</span><span class="sxs-lookup"><span data-stu-id="15412-216">-- or</span></span>

[!code-csharp[Main](server-controls/samples/sample13.cs)]

<span data-ttu-id="15412-217">ASP.NET 2.0 (이전에 설명) Webresource.axd 처리기를 사용 하 여 포커스를 설정 하는 클라이언트 쪽 함수 렌더링.</span><span class="sxs-lookup"><span data-stu-id="15412-217">ASP.NET 2.0 uses the Webresource.axd handler (discussed previously) to render a client-side function that sets the focus.</span></span> <span data-ttu-id="15412-218">클라이언트 쪽 함수 이름은 WebForm\_AutoFocus 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-218">The name of the client-side function is WebForm\_AutoFocus as shown here:</span></span>

[!code-html[Main](server-controls/samples/sample14.html)]

<span data-ttu-id="15412-219">또는 해당 컨트롤에 초기 포커스를 설정 하는 컨트롤에 대 한 포커스 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-219">Alternatively, you can use the Focus method for a control to set the initial focus to that control.</span></span> <span data-ttu-id="15412-220">포커스 메서드 Control 클래스에서 파생 되 고 모든 ASP.NET 2.0 컨트롤에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-220">The Focus method derives from the Control class and is available to all ASP.NET 2.0 controls.</span></span> <span data-ttu-id="15412-221">유효성 검사 오류가 발생 하는 경우 특정 컨트롤에 포커스를 설정 하는 것도 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-221">It is also possible to set focus to a particular control when a validation error occurs.</span></span> <span data-ttu-id="15412-222">이후 단원에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-222">That will be covered in a later module.</span></span>

## <a name="new-server-controls-in-aspnet-20"></a><span data-ttu-id="15412-223">ASP.NET 2.0의에서 새로운 서버 컨트롤</span><span class="sxs-lookup"><span data-stu-id="15412-223">New Server Controls in ASP.NET 2.0</span></span>

<span data-ttu-id="15412-224">ASP.NET 2.0의 새로운 서버 컨트롤은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-224">The following are new server controls in ASP.NET 2.0.</span></span> <span data-ttu-id="15412-225">이후 모듈에서 그 중 일부에 대해 좀 더 자세히 이동지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="15412-225">We will go into more detail on some of them in later modules.</span></span>

## <a name="imagemap-control"></a><span data-ttu-id="15412-226">ImageMap 컨트롤</span><span class="sxs-lookup"><span data-stu-id="15412-226">ImageMap Control</span></span>

<span data-ttu-id="15412-227">ImageMap 컨트롤을 사용 하면 핫스폿 다시 게시를 시작 하거나 URL을 탐색할 수 있는 이미지를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-227">The ImageMap control allows you to add hotspots to an image that can initiate a post back or navigate to a URL.</span></span> <span data-ttu-id="15412-228">세 가지가 핫스폿에의 사용할 수 있습니다. CircleHotSpot, RectangleHotSpot, 및 PolygonHotSpot 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-228">There are three types of hotspots available; CircleHotSpot, RectangleHotSpot, and PolygonHotSpot.</span></span> <span data-ttu-id="15412-229">핫스팟 Visual Studio 또는 프로그래밍 방식으로 코드에서 컬렉션 편집기를 통해 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15412-229">Hotspots are added via a collection editor in Visual Studio or programmatically in code.</span></span> <span data-ttu-id="15412-230">이미지에 핫스폿 그리기에 사용할 수 있는 사용자 인터페이스 없이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-230">There is no user-interface available for drawing hotspots on an image.</span></span> <span data-ttu-id="15412-231">좌표 및 크기 또는 핫 스폿의 반지름을 선언적으로 지정 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-231">The coordinates and size or radius of the hotspot must be specified declaratively.</span></span> <span data-ttu-id="15412-232">디자이너에서 핫스팟의 시각적 표시가 이기도합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-232">There is also no visual representation of a hotspot in the designer.</span></span> <span data-ttu-id="15412-233">핫스팟을 URL로 이동한 다음에 구성 된 경우 URL 핫 스폿의 NavigateUrl 속성을 통해 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15412-233">If a hotspot is configured to navigate to a URL, the URL is specified via the NavigateUrl property of the hotspot.</span></span> <span data-ttu-id="15412-234">게시의 경우 속성을 사용 하면 서버 쪽 코드에 다시 게시에서 검색할 수 있는 문자열을 전달할 수 있습니다 PostBackValue 핫스팟을 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-234">In the case of a post back hotspot, the PostBackValue property allows you to pass a string in the post back that can be retrieved in server-side code.</span></span>


![Visual Studio에서 hotSpot 컬렉션 편집기](server-controls/_static/image1.jpg)

<span data-ttu-id="15412-236">**그림 1**: Visual Studio에서 HotSpot 컬렉션 편집기</span><span class="sxs-lookup"><span data-stu-id="15412-236">**Figure 1**: HotSpot Collection Editor in Visual Studio</span></span>


## <a name="bulletedlist-control"></a><span data-ttu-id="15412-237">BulletedList 컨트롤</span><span class="sxs-lookup"><span data-stu-id="15412-237">BulletedList Control</span></span>

<span data-ttu-id="15412-238">BulletedList 컨트롤은 쉽게 수 있는 데이터 바인딩된 글머리 기호 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="15412-238">The BulletedList control is a bulleted list that can easily be data bound.</span></span> <span data-ttu-id="15412-239">목록 순서를 지정할 수 (숫자) 또는 BulletStyle 속성을 통해 순서가 지정 되지 않은 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-239">The list can be ordered (numbered) or unordered via the BulletStyle property.</span></span> <span data-ttu-id="15412-240">목록의 각 항목은 ListItem 개체에 의해 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15412-240">Each item in the list is represented by a ListItem object.</span></span>


![Visual Studio에서 BulletedList 컨트롤](server-controls/_static/image1.gif)

<span data-ttu-id="15412-242">**그림 2**: Visual Studio에서 BulletedList 컨트롤</span><span class="sxs-lookup"><span data-stu-id="15412-242">**Figure 2**: BulletedList Control in Visual Studio</span></span>


## <a name="hiddenfield-control"></a><span data-ttu-id="15412-243">HiddenField 컨트롤</span><span class="sxs-lookup"><span data-stu-id="15412-243">HiddenField Control</span></span>

<span data-ttu-id="15412-244">HiddenField 컨트롤을 해당 값은 서버 쪽 코드에서 사용할 수 있는 페이지에는 숨겨진된 폼 필드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-244">The HiddenField control adds a hidden form field to your page, the value of which is available in server-side code.</span></span> <span data-ttu-id="15412-245">숨겨진된 폼 필드의 값은 일반적으로 post 백업 간에 변경 되지 않고 유지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-245">The value of a hidden form field is generally expected to remain unchanged between post backs.</span></span> <span data-ttu-id="15412-246">그러나 악의적인 사용자가 다시 게시 값 전에 변경에 대 한 같습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-246">However, it is possible for a malicious user to change the value prior to post back.</span></span> <span data-ttu-id="15412-247">이 경우 HiddenField 컨트롤 경우 재정의 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-247">If this happens, the HiddenField control will raise the ValueChanged event.</span></span> <span data-ttu-id="15412-248">HiddenField 컨트롤에 중요 한 정보가 있는 경우 변경 되지 않은 상태로 유지 되는지 확인 하려는 경우 재정의 코드에서 처리 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-248">If you have sensitive information in the HiddenField control and you want to ensure that it remains unchanged, you should handle the ValueChanged event in your code.</span></span>

## <a name="fileupload-control"></a><span data-ttu-id="15412-249">파일 업로드 컨트롤</span><span class="sxs-lookup"><span data-stu-id="15412-249">FileUpload Control</span></span>

<span data-ttu-id="15412-250">ASP.NET 2.0에서 파일 업로드 컨트롤을 사용 하면 ASP.NET 페이지를 통해 웹 서버에 파일을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-250">The FileUpload control in ASP.NET 2.0 makes it possible to upload files to a Web server via an ASP.NET page.</span></span> <span data-ttu-id="15412-251">이 컨트롤은 몇 가지 예외를 사용 하 여 ASP.NET 1.x HtmlInputFile 클래스와 매우 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-251">This control is quite similar to the ASP.NET 1.x HtmlInputFile class with a few exceptions.</span></span> <span data-ttu-id="15412-252">ASP.NET에서 1.x 것을 권장 했습니다 좋은 파일을 갖는 경우를 확인 하기 위해 null에 대 한 PostedFile 속성을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-252">In ASP.NET 1.x, it was recommended that the PostedFile property be checked for null in order to determine if you had a good file.</span></span> <span data-ttu-id="15412-253">ASP.NET 2.0에서 파일 업로드 컨트롤 같은 목적을 위해 사용할 수 있으며이 좀 더 효율적 새 HasFile 속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-253">The FileUpload control in ASP.NET 2.0 adds a new HasFile property that you can use for the same purpose and it's a bit more efficient.</span></span>

<span data-ttu-id="15412-254">PostedFile 속성이 HttpPostedFile 개체에 대 한 액세스를 위해 계속 사용할 수 이지만 이제 파일 업로드 컨트롤 기본적으로 사용할 수는 HttpPostedFile 기능 중 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="15412-254">The PostedFile property is still available for access to an HttpPostedFile object, but some of the functionality of the HttpPostedFile is now available intrinsically with the FileUpload control.</span></span> <span data-ttu-id="15412-255">예를 들어, ASP.NET에 업로드 된 파일을 저장 하려면 HttpPostedFile 개체에서 SaveAs 메서드를 호출할 1.x 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-255">For example, to save an uploaded file in ASP.NET 1.x, you call the SaveAs method on the HttpPostedFile object.</span></span> <span data-ttu-id="15412-256">파일 업로드 컨트롤을 사용 하 여 ASP.NET 2.0에서, 파일 업로드 컨트롤 자체에서 SaveAs 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-256">Using the FileUpload control in ASP.NET 2.0, you would call the SaveAs method on the FileUpload control itself.</span></span>

<span data-ttu-id="15412-257">2.0 동작 (및 가능성이 가장 중요 한 변경)의 또 다른 큰 변화가 전체 업로드 된 파일을 저장 하기 전에 메모리에 로드 하는 데 필요한 더 이상 된다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="15412-257">Another significant change in the 2.0 behavior (and likely the most significant change) is that it is no longer necessary to load an entire uploaded file into memory before saving it.</span></span> <span data-ttu-id="15412-258">1.x 업로드 된 모든 파일이 기록 되기 전에 메모리에 완전히 저장 됩니다 디스크에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-258">In 1.x, any file that was uploaded is saved entirely into memory prior to being written to disk.</span></span> <span data-ttu-id="15412-259">이 아키텍처는 큰 파일 업로드를 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-259">This architecture prevents the upload of large files.</span></span>

<span data-ttu-id="15412-260">ASP.NET 2.0에서 requestLengthDiskThreshold 특성 httpRuntime 요소의 크기를 구성할 수 있습니다 기록 되기 전에 메모리에 버퍼에 저장 된 디스크에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-260">In ASP.NET 2.0, the requestLengthDiskThreshold attribute of the httpRuntime element allows you to configure how many Kilobytes are held in a buffer in memory prior to being written to disk.</span></span>

<span data-ttu-id="15412-261">**중요 한**:이 값 (킬로바이트) (바이트)에서 이며 기본값은 256 MSDN 설명서 (및 다른 곳에서 설명서) 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-261">**IMPORTANT**: MSDN documentation (and documentation elsewhere) specifies that this value is in bytes (not Kilobytes) and that the default is 256.</span></span> <span data-ttu-id="15412-262">킬로바이트 단위로 실제로 지정 된 값 및 기본값은 80입니다.</span><span class="sxs-lookup"><span data-stu-id="15412-262">The value is actually specified in Kilobytes and the default value is 80.</span></span> <span data-ttu-id="15412-263">기본값은 80 K 함으로써 대형 개체 힙에 버퍼 종료 하지 않습니다 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-263">By having a default value of 80K, we ensure that the buffer does not end up on the large object heap.</span></span>

## <a name="wizard-control"></a><span data-ttu-id="15412-264">마법사 컨트롤</span><span class="sxs-lookup"><span data-stu-id="15412-264">Wizard Control</span></span>

<span data-ttu-id="15412-265">것이 일반적 패널을 사용 하 여 "페이지" 또는 페이지를 전송 하 여 일련의 정보를 수집 하려는 ASP.NET 개발자 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-265">It is fairly common to encounter ASP.NET developers struggling with attempting to gather information in a series of "pages" using panels or by transferring from page to page.</span></span> <span data-ttu-id="15412-266">것, 노력은 하면 당황 스 러 하나 이며 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="15412-266">More often than not, the endeavor is a frustrating one and is time consuming.</span></span> <span data-ttu-id="15412-267">새 Wizard 컨트롤 사용자가 잘 알고 있는 마법사 인터페이스의 선형 및 비선형 단계에 대 한 허용 하 여 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-267">The new Wizard control solves the problems by allowing for linear and non-linear steps in a wizard interface that users are familiar with.</span></span> <span data-ttu-id="15412-268">마법사 컨트롤 입력된 양식 처럼 일련의 단계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-268">The Wizard control presents input forms in a series of steps.</span></span> <span data-ttu-id="15412-269">각 단계는 특정 유형의 컨트롤의 StepType 속성에 지정 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="15412-269">Each step is of a particular type specified by the StepType property of the control.</span></span> <span data-ttu-id="15412-270">사용 가능한 단계 종류는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-270">The available step types are as follows:</span></span>

| <span data-ttu-id="15412-271">**단계 유형**</span><span class="sxs-lookup"><span data-stu-id="15412-271">**Step Type**</span></span> | <span data-ttu-id="15412-272">**설명**</span><span class="sxs-lookup"><span data-stu-id="15412-272">**Explanation**</span></span> |
| --- | --- |
| <span data-ttu-id="15412-273">자동</span><span class="sxs-lookup"><span data-stu-id="15412-273">Auto</span></span> | <span data-ttu-id="15412-274">마법사는 단계의 단계 계층 구조 내에서 위치에 따라 유형을 자동으로 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-274">The wizard automatically determines the type of step based upon its position within the step hierarchy.</span></span> |
| <span data-ttu-id="15412-275">시작</span><span class="sxs-lookup"><span data-stu-id="15412-275">Start</span></span> | <span data-ttu-id="15412-276">소개 문에 제공 자주 사용 되는 첫 번째 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="15412-276">The first step, often used to present an introductory statement.</span></span> |
| <span data-ttu-id="15412-277">단계</span><span class="sxs-lookup"><span data-stu-id="15412-277">Step</span></span> | <span data-ttu-id="15412-278">일반적인 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="15412-278">A normal step.</span></span> |
| <span data-ttu-id="15412-279">마침</span><span class="sxs-lookup"><span data-stu-id="15412-279">Finish</span></span> | <span data-ttu-id="15412-280">마법사를 완료 하는 단추를 표시 하는 데 일반적으로 최종 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="15412-280">The final step, usually used to present a button to finish the wizard.</span></span> |
| <span data-ttu-id="15412-281">완료</span><span class="sxs-lookup"><span data-stu-id="15412-281">Complete</span></span> | <span data-ttu-id="15412-282">성공 또는 실패를 통신 하는 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-282">Presents a message communicating success or failure.</span></span> |

> [!NOTE]
> <span data-ttu-id="15412-283">마법사 컨트롤은 ASP.NET 컨트롤 상태를 사용 하 여 해당 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="15412-283">The Wizard control keeps track of its state using ASP.NET control state.</span></span> <span data-ttu-id="15412-284">따라서 EnableViewState 속성 모든 단점이 없이 false로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-284">Therefore, the EnableViewState property can be set to false without any detriment.</span></span>


<span data-ttu-id="15412-285">이 비디오는 Wizard 컨트롤의 연습 과정입니다.</span><span class="sxs-lookup"><span data-stu-id="15412-285">This video is a walkthrough of the Wizard control.</span></span>


![](server-controls/_static/image2.png)


[<span data-ttu-id="15412-286">전체 화면 비디오 열기</span><span class="sxs-lookup"><span data-stu-id="15412-286">Open Full-Screen Video</span></span>](server-controls/_static/wizard1.wmv)


## <a name="localize-control"></a><span data-ttu-id="15412-287">컨트롤 지역화</span><span class="sxs-lookup"><span data-stu-id="15412-287">Localize Control</span></span>

<span data-ttu-id="15412-288">Localize 컨트롤 리터럴 제어 하는 것과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-288">The Localize control is similar to a Literal control.</span></span> <span data-ttu-id="15412-289">그러나 Localize 컨트롤에는 **모드** 여기에 추가 되는 태그를 렌더링 하는 방식을 제어 하는 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-289">However, the Localize control has a **Mode** property that controls how markup that is added to it is rendered.</span></span> <span data-ttu-id="15412-290">모드 속성은 다음 값을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-290">The Mode property supports the following values:</span></span>

| <span data-ttu-id="15412-291">**모드**</span><span class="sxs-lookup"><span data-stu-id="15412-291">**Mode**</span></span> | <span data-ttu-id="15412-292">**설명**</span><span class="sxs-lookup"><span data-stu-id="15412-292">**Explanation**</span></span> |
| --- | --- |
| <span data-ttu-id="15412-293">변형</span><span class="sxs-lookup"><span data-stu-id="15412-293">Transform</span></span> | <span data-ttu-id="15412-294">태그는 요청 하는 브라우저의 프로토콜에 따라 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15412-294">Markup is transformed according to the protocol of the browser making the request.</span></span> |
| <span data-ttu-id="15412-295">통과 연결</span><span class="sxs-lookup"><span data-stu-id="15412-295">PassThrough</span></span> | <span data-ttu-id="15412-296">로 태그를 렌더링할-됩니다.</span><span class="sxs-lookup"><span data-stu-id="15412-296">Markup is rendered as-is.</span></span> |
| <span data-ttu-id="15412-297">인코딩</span><span class="sxs-lookup"><span data-stu-id="15412-297">Encode</span></span> | <span data-ttu-id="15412-298">컨트롤에 추가 되는 태그는 HtmlEncode를 사용 하 여 인코딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="15412-298">Markup that is added to the control is encoded using HtmlEncode.</span></span> |

## <a name="multiview-and-view-controls"></a><span data-ttu-id="15412-299">MultiView 및 뷰 컨트롤</span><span class="sxs-lookup"><span data-stu-id="15412-299">MultiView and View Controls</span></span>

<span data-ttu-id="15412-300">MultiView 컨트롤 뷰 컨트롤에 대 한 컨테이너로 사용 하 고 View 컨트롤 컨테이너 역할을 훨씬 (패널 컨트롤)를 같은 다른 컨트롤에 대 한 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="15412-300">The MultiView control acts as a container for View controls, and the View control acts as a container (much like a Panel control) for other controls.</span></span> <span data-ttu-id="15412-301">MultiView 컨트롤의 각 보기는 단일 뷰 컨트롤에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15412-301">Each view in a MultiView control is represented by a single View control.</span></span> <span data-ttu-id="15412-302">MultiView에서 뷰 컨트롤에서 첫 번째 뷰입니다 0, 두 번째는 1, 뷰 등입니다. MultiView 컨트롤 ActiveViewIndex를 지정 하 여 보기를 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-302">The first View control in the MultiView is view 0, the second is view 1, etc. You can switch views by specifying the ActiveViewIndex of the MultiView control.</span></span>

## <a name="substitution-control"></a><span data-ttu-id="15412-303">대체 컨트롤</span><span class="sxs-lookup"><span data-stu-id="15412-303">Substitution Control</span></span>

<span data-ttu-id="15412-304">대체 컨트롤은 ASP.NET 캐싱와 함께에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15412-304">The Substitution control is used in conjunction with ASP.NET caching.</span></span> <span data-ttu-id="15412-305">캐싱, 활용 하려는 하지만 (즉, 페이지의 부분 캐싱을에서 제외 되는) 각 요청에 대해 업데이트 해야 하는 페이지의 부분에 있는 경우, 대체 구성 요소 뛰어난 솔루션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-305">In cases where you want to take advantage of caching, but you have portions of a page that must be updated on each request (in other words, portions of a page that are exempt from caching), the Substitution component provides a great solution.</span></span> <span data-ttu-id="15412-306">컨트롤에서 어떠한 출력도 자체적으로 렌더링 실제로 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-306">The control doesn't actually render any output on its own.</span></span> <span data-ttu-id="15412-307">대신, 서버 쪽 코드의 메서드에 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="15412-307">Instead, it is bound to a method in server-side code.</span></span> <span data-ttu-id="15412-308">페이지 요청 되 면 메서드가 호출 되 고 대체 컨트롤 대신 반환 된 태그 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15412-308">When the page is requested, the method is called and the returned markup is rendered in place of the substitution control.</span></span>

<span data-ttu-id="15412-309">대체 컨트롤 연결 된 메서드를 통해 지정 됩니다는 **MethodName** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="15412-309">The method to which the Substitution control is bound is specified via the **MethodName** property.</span></span> <span data-ttu-id="15412-310">해당 메서드는 다음 조건을 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-310">That method must meet the following criteria:</span></span>

- <span data-ttu-id="15412-311">정적 (VB의 경우 공유) 메서드에 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-311">It must be a static (shared in VB) method.</span></span>
- <span data-ttu-id="15412-312">HttpContext 형식의 매개 변수 하나를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-312">It accepts one parameter of type HttpContext.</span></span>
- <span data-ttu-id="15412-313">페이지에 컨트롤을 대체 해야 하는 태그를 나타내는 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-313">It returns a string representing the markup that should replace the control on the page.</span></span>

<span data-ttu-id="15412-314">해당 매개 변수를 통해 현재 HttpContext에 대 한 액세스는 것은 하지만 대체 컨트롤에는 페이지에 있는 다른 컨트롤을 수정할 수 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-314">The Substitution control does not have the ability to modify any other control on the page, but it does have access to the current HttpContext via its parameter.</span></span>

## <a name="gridview-control"></a><span data-ttu-id="15412-315">GridView 컨트롤</span><span class="sxs-lookup"><span data-stu-id="15412-315">GridView Control</span></span>

<span data-ttu-id="15412-316">GridView 컨트롤은 DataGrid 컨트롤의 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-316">The GridView control is the replacement for the DataGrid control.</span></span> <span data-ttu-id="15412-317">이 컨트롤은 이후 단원에서 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-317">This control will be covered in more detail in a later module.</span></span>

## <a name="detailsview-control"></a><span data-ttu-id="15412-318">DetailsView 컨트롤</span><span class="sxs-lookup"><span data-stu-id="15412-318">DetailsView Control</span></span>

<span data-ttu-id="15412-319">DetailsView 컨트롤을 사용 하면 데이터 원본에서 단일 레코드를 표시 하 고 편집 하거나 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-319">The DetailsView control allows you to display a single record from a data source and to edit or delete it.</span></span> <span data-ttu-id="15412-320">이후 단원에서 자세히 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="15412-320">It is covered in more detail in a later module.</span></span>

## <a name="formview-control"></a><span data-ttu-id="15412-321">FormView 컨트롤</span><span class="sxs-lookup"><span data-stu-id="15412-321">FormView Control</span></span>

<span data-ttu-id="15412-322">FormView 컨트롤을 사용 하 여 구성 가능한 인터페이스에 데이터 원본에서 단일 레코드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-322">The FormView control is used to display a single record from a datasource in a configurable interface.</span></span> <span data-ttu-id="15412-323">이후 단원에서 자세히 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="15412-323">It is covered in more detail in a later module.</span></span>

## <a name="accessdatasource-control"></a><span data-ttu-id="15412-324">AccessDataSource 컨트롤</span><span class="sxs-lookup"><span data-stu-id="15412-324">AccessDataSource Control</span></span>

<span data-ttu-id="15412-325">AccessDataSource 컨트롤에 사용 되는 Access 데이터베이스를 바인딩할 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="15412-325">The AccessDataSource control is used to data bind an Access database.</span></span> <span data-ttu-id="15412-326">이후 단원에서 자세히 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="15412-326">It is covered in more detail in a later module.</span></span>

## <a name="objectdatasource-control"></a><span data-ttu-id="15412-327">ObjectDataSource 컨트롤</span><span class="sxs-lookup"><span data-stu-id="15412-327">ObjectDataSource Control</span></span>

<span data-ttu-id="15412-328">ObjectDataSource 컨트롤은 컨트롤 수 수에 데이터 바인딩된 2 계층 모델 대신 중간 계층 비즈니스 개체 데이터 소스에 직접 바인딩된은 컨트롤이 있도록 3 계층 아키텍처를 지 원하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15412-328">The ObjectDataSource control is used to support a three-tier architecture so that controls can be data-bound to a middle-tier business object as opposed to a two-tiered model where controls are bound directly to the data source.</span></span> <span data-ttu-id="15412-329">이후 단원에서 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-329">It will be discussed in more detail in a later module.</span></span>

## <a name="xmldatasource-control"></a><span data-ttu-id="15412-330">XmlDataSource 컨트롤</span><span class="sxs-lookup"><span data-stu-id="15412-330">XmlDataSource Control</span></span>

<span data-ttu-id="15412-331">XmlDataSource 컨트롤에 XML 데이터 소스에 데이터 바인딩을 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15412-331">The XmlDataSource control is used to data bind to an XML data source.</span></span> <span data-ttu-id="15412-332">이후 단원에서 자세히 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="15412-332">It is covered in more detail in a later module.</span></span>

## <a name="sitemapdatasource-control"></a><span data-ttu-id="15412-333">SiteMapDataSource 제어</span><span class="sxs-lookup"><span data-stu-id="15412-333">SiteMapDataSource Control</span></span>

<span data-ttu-id="15412-334">SiteMapDataSource 컨트롤 사이트 맵을 기반으로 하는 사이트 탐색 컨트롤에 대 한 데이터 바인딩을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-334">The SiteMapDataSource control provides data binding for site navigation controls based on a site map.</span></span> <span data-ttu-id="15412-335">이후 단원에서 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-335">It will be discussed in more detail in a later module.</span></span>

## <a name="sitemappath-control"></a><span data-ttu-id="15412-336">SiteMapPath 컨트롤</span><span class="sxs-lookup"><span data-stu-id="15412-336">SiteMapPath Control</span></span>

<span data-ttu-id="15412-337">SiteMapPath 컨트롤에는 일련의 breadcrumb 흔히 탐색 링크를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-337">The SiteMapPath control displays a series of navigation links commonly referred to as breadcrumbs.</span></span> <span data-ttu-id="15412-338">이후 단원에서 자세히 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="15412-338">It is covered in more detail in a later module.</span></span>

## <a name="menu-control"></a><span data-ttu-id="15412-339">Menu 컨트롤</span><span class="sxs-lookup"><span data-stu-id="15412-339">Menu Control</span></span>

<span data-ttu-id="15412-340">Menu 컨트롤 DHTML을 사용 하 여 동적 메뉴를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-340">The Menu control displays dynamic menus using DHTML.</span></span> <span data-ttu-id="15412-341">이후 단원에서 자세히 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="15412-341">It is covered in more detail in a later module.</span></span>

## <a name="treeview-control"></a><span data-ttu-id="15412-342">TreeView 컨트롤</span><span class="sxs-lookup"><span data-stu-id="15412-342">TreeView Control</span></span>

<span data-ttu-id="15412-343">TreeView 컨트롤을 사용 하 여 데이터의 계층적 트리 뷰를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-343">The TreeView control is used to display a hierarchical tree view of data.</span></span> <span data-ttu-id="15412-344">이후 단원에서 자세히 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="15412-344">It is covered in more detail in a later module.</span></span>

## <a name="login-control"></a><span data-ttu-id="15412-345">Login 컨트롤</span><span class="sxs-lookup"><span data-stu-id="15412-345">Login Control</span></span>

<span data-ttu-id="15412-346">웹 사이트에 로그인 하는 메커니즘에 대 한 로그인 제어를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-346">The Login control provides for a mechanism to log into a Web site.</span></span> <span data-ttu-id="15412-347">이후 단원에서 자세히 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="15412-347">It is covered in more detail in a later module.</span></span>

## <a name="loginview-control"></a><span data-ttu-id="15412-348">LoginView 컨트롤</span><span class="sxs-lookup"><span data-stu-id="15412-348">LoginView Control</span></span>

<span data-ttu-id="15412-349">LoginView 컨트롤 허용 사용자의 로그인 상태에 따라 서로 다른 템플릿 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-349">The LoginView control allows for the display of different templates based upon a user's login status.</span></span> <span data-ttu-id="15412-350">이후 단원에서 자세히 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="15412-350">It is covered in more detail in a later module.</span></span>

## <a name="passwordrecovery-control"></a><span data-ttu-id="15412-351">PasswordRecovery 제어</span><span class="sxs-lookup"><span data-stu-id="15412-351">PasswordRecovery Control</span></span>

<span data-ttu-id="15412-352">PasswordRecovery 컨트롤은 ASP.NET 응용 프로그램의 사용자가 잊어버린된 암호 검색에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15412-352">The PasswordRecovery control is used to retrieve forgotten passwords by users of an ASP.NET application.</span></span> <span data-ttu-id="15412-353">이후 단원에서 자세히 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="15412-353">It is covered in more detail in a later module.</span></span>

## <a name="loginstatus"></a><span data-ttu-id="15412-354">LoginStatus</span><span class="sxs-lookup"><span data-stu-id="15412-354">LoginStatus</span></span>

<span data-ttu-id="15412-355">LoginStatus 컨트롤은 사용자의 로그인 상태를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="15412-355">The LoginStatus control displays a user's login status.</span></span> <span data-ttu-id="15412-356">이후 단원에서 자세히 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="15412-356">It is covered in more detail in a later module.</span></span>

## <a name="loginname"></a><span data-ttu-id="15412-357">LoginName</span><span class="sxs-lookup"><span data-stu-id="15412-357">LoginName</span></span>

<span data-ttu-id="15412-358">LoginName 컨트롤 후 ASP.NET 응용 프로그램에 로그인 하는 사용자의 사용자 이름을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-358">The LoginName control displays a user's username after being logged into an ASP.NET application.</span></span> <span data-ttu-id="15412-359">이후 단원에서 자세히 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="15412-359">It is covered in more detail in a later module.</span></span>

## <a name="createuserwizard"></a><span data-ttu-id="15412-360">CreateUserWizard</span><span class="sxs-lookup"><span data-stu-id="15412-360">CreateUserWizard</span></span>

<span data-ttu-id="15412-361">CreateUserWizard는 사용자가 ASP.NET 응용 프로그램에서 사용 하기 위해 ASP.NET 멤버 자격 계정을 만들 수 있도록 구성할 수 있는 마법사입니다.</span><span class="sxs-lookup"><span data-stu-id="15412-361">The CreateUserWizard is a configurable wizard which gives users the ability to create an ASP.NET Membership account for use in an ASP.NET application.</span></span> <span data-ttu-id="15412-362">이후 단원에서 자세히 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="15412-362">It is covered in more detail in a later module.</span></span>

## <a name="changepassword"></a><span data-ttu-id="15412-363">암호 변경</span><span class="sxs-lookup"><span data-stu-id="15412-363">ChangePassword</span></span>

<span data-ttu-id="15412-364">ChangePassword 컨트롤을 사용 하면 ASP.NET 응용 프로그램에 대 한 암호를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15412-364">The ChangePassword control allows users to change their password for an ASP.NET application.</span></span> <span data-ttu-id="15412-365">이후 단원에서 자세히 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="15412-365">It is covered in more detail in a later module.</span></span>

## <a name="various-webparts"></a><span data-ttu-id="15412-366">다양 한 웹 파트</span><span class="sxs-lookup"><span data-stu-id="15412-366">Various WebParts</span></span>

<span data-ttu-id="15412-367">ASP.NET 2.0 웹 파트를 다양 한 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15412-367">ASP.NET 2.0 ships with various Web Parts.</span></span> <span data-ttu-id="15412-368">이후 단원에서 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="15412-368">These will be covered in detail in a later module.</span></span>
