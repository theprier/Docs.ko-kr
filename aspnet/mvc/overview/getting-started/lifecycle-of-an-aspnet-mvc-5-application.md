---
uid: mvc/overview/getting-started/lifecycle-of-an-aspnet-mvc-5-application
title: "ASP.NET MVC 5 응용 프로그램의 수명 주기 | Microsoft Docs"
author: cephalin
description: "ASP.NET MVC 5 응용 프로그램의 수명 주기를 차트를 PDF 문서를 다운로드 합니다. 이 주기 문서에서는 MVC 수명 주기를 간략하게 제공는 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/28/2014
ms.topic: article
ms.assetid: 9c1e3a75-b644-4480-8326-11300b1ec4b3
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/lifecycle-of-an-aspnet-mvc-5-application
msc.type: authoredcontent
ms.openlocfilehash: 5692c43168eb261c91f40e2046897a1e5d31a028
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="lifecycle-of-an-aspnet-mvc-5-application"></a><span data-ttu-id="5c253-104">ASP.NET MVC 5 응용 프로그램의 수명 주기</span><span class="sxs-lookup"><span data-stu-id="5c253-104">Lifecycle of an ASP.NET MVC 5 Application</span></span>
====================
<span data-ttu-id="5c253-105">으로 [Cephas 링크](https://github.com/cephalin)</span><span class="sxs-lookup"><span data-stu-id="5c253-105">by [Cephas Lin](https://github.com/cephalin)</span></span>

[<span data-ttu-id="5c253-106">PDF 문서를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c253-106">Download PDF Document</span></span>](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf)

<span data-ttu-id="5c253-107">여기에서 HTTP 수신 모든 ASP.NET MVC 5 응용 프로그램의 수명 주기는 HTTP 응답을 보내는 것에 요청 하는 차트를 다시 클라이언트에 PDF 문서를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c253-107">Here you can download a PDF document that charts the lifecycle of every ASP.NET MVC 5 application, from receiving the HTTP request to sending the HTTP response back to the client.</span></span> <span data-ttu-id="5c253-108">ASP.NET MVC와 접하는 사용자에 게 교육 도구로도 응용 프로그램의 특정 측면을 드릴 필요로 하는 사람들에 대 한 참조로 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5c253-108">It is designed both as an educational tool for those who are new to ASP.NET MVC and also as a reference for those who need to drill into specific aspects of the application.</span></span> <span data-ttu-id="5c253-109">PDF 문서에는 다음 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c253-109">The PDF document has the following features:</span></span>

- <span data-ttu-id="5c253-110">관련 [HttpApplication](https://msdn.microsoft.com/en-us/library/system.web.httpapplication.aspx) MVC에 통합 하는 위치를 쉽게 이해할 수 있도록 하는 단계는 [ASP.NET 응용 프로그램 수명 주기](https://msdn.microsoft.com/en-us/library/bb470252.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="5c253-110">Relevant [HttpApplication](https://msdn.microsoft.com/en-us/library/system.web.httpapplication.aspx) stages to help you understand where MVC integrates into the [ASP.NET application lifecycle](https://msdn.microsoft.com/en-us/library/bb470252.aspx).</span></span>
- <span data-ttu-id="5c253-111">높은 수준의 MVC 응용 프로그램 수명 주기 모든 MVC 응용 프로그램 요청 처리 파이프라인의를 통해 전달 되는 주요 단계를 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c253-111">A high-level view of the MVC application lifecycle, where you can understand the major stages that every MVC application passes through in the request processing pipeline.</span></span>  
    ![](lifecycle-of-an-aspnet-mvc-5-application/_static/image1.jpg)
- <span data-ttu-id="5c253-112">요청 처리 파이프라인의 세부 정보를 드릴 다운 표시 하는 세부 정보 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="5c253-112">A detail view that shows drills down into the details of the request processing pipeline.</span></span> <span data-ttu-id="5c253-113">상위 수준 뷰와 여러 단계로 주기 정보가 수집 되는 방법을 보려면 세부 정보 보기를 비교할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c253-113">You can compare the high-level view and the detail view to see how the lifecycles details are collected into the various stages.</span></span> <span data-ttu-id="5c253-114">[PDF 다운로드](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf) 더 크게 보려면 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c253-114">[Download PDF](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf) to see a larger view.</span></span>
    ![](lifecycle-of-an-aspnet-mvc-5-application/_static/image2.jpg)
- <span data-ttu-id="5c253-115">에 있는 모든 재정의 가능한 메서드가의 목적 및 배치는 [컨트롤러](https://msdn.microsoft.com/en-us/library/system.web.mvc.controller.aspx) 요청 처리 파이프라인에서 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="5c253-115">Placement and purpose of all overridable methods on the [Controller](https://msdn.microsoft.com/en-us/library/system.web.mvc.controller.aspx) object in the request processing pipeline.</span></span> <span data-ttu-id="5c253-116">수도 한 모든 메서드를 재정의 필요가 없을 수 있습니다 하지만 결과 얻기에 대 한 적절 한 수명 주기 단계에서 코드를 작성할 수 있도록 응용 프로그램 수명 주기에서 자신의 역할을 이해 하는 것이 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c253-116">You may or may not have the need to override any one method, but it is important for you to understand their role in the application lifecycle so that you can write code at the appropriate life cycle stage for the effect you intend.</span></span>
- <span data-ttu-id="5c253-117">각 필터 형식 (예: 인증, 권한 부여, 동작 및 결과)이 호출 하는 방법을 보여 주는 나간 접속 다이어그램.</span><span class="sxs-lookup"><span data-stu-id="5c253-117">Blown-up diagrams showing how each of the filter types (authentication, authorization, action, and result) is invoked.</span></span>
- <span data-ttu-id="5c253-118">세부 정보 보기에 대 한 관심의 각 지점에서 유용한 문서 또는 블로그를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c253-118">Link to a useful article or blog from each point of interest in the detail view.</span></span>


## <a name="next-steps"></a><span data-ttu-id="5c253-119">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5c253-119">Next Steps</span></span>

<span data-ttu-id="5c253-120">이 문서에 요구 사항에 충족 됩니까?</span><span class="sxs-lookup"><span data-stu-id="5c253-120">Does this document meet your need?</span></span> <span data-ttu-id="5c253-121">여러분의 의견 보내 주셔서 감사 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c253-121">We'd appreciate your feedback.</span></span> <span data-ttu-id="5c253-122">응용 프로그램에서 ASP.NET MVC 수명 주기 궁금한 사항이 있는 경우 [Stackoverflow](http://stackoverflow.com/help) 및 [ASP.NET MVC 포럼](https://forums.asp.net/1146.aspx) 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c253-122">If you have any question on the ASP.NET MVC lifecycle in your application, [Stackoverflow](http://stackoverflow.com/help) and the [ASP.NET MVC forums](https://forums.asp.net/1146.aspx) are great places to ask.</span></span> <span data-ttu-id="5c253-123">에 따라 [me](https://twitter.com/Cephas_MSFT) 에서 twitter 때문 내 최신 자습서에 대 한 업데이트를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c253-123">Follow [me](https://twitter.com/Cephas_MSFT) on twitter so you can get updates on my latest tutorials.</span></span>
