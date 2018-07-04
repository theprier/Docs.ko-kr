---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
title: '8 부: 최종 페이지, 예외 처리 및 결론 | Microsoft Docs'
author: JoeStagner
description: 이 자습서 시리즈 모든 Tailspin Spyworks 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 8 부 페이지 및 예외에 대 한 연락처 페이지를 추가 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/21/2010
ms.topic: article
ms.assetid: 5aeadf8f-39f3-4f07-a78f-1c310c64fb23
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
msc.type: authoredcontent
ms.openlocfilehash: 3f1d855e157f6a58995d301a793e660925767fb4
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37380255"
---
<a name="part-8-final-pages-exception-handling-and-conclusion"></a><span data-ttu-id="04841-104">8 부: 최종 페이지, 예외 처리 및 결론</span><span class="sxs-lookup"><span data-stu-id="04841-104">Part 8: Final Pages, Exception Handling, and Conclusion</span></span>
====================
<span data-ttu-id="04841-105">[Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="04841-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="04841-106">Tailspin Spyworks.NET 플랫폼에 대 한 강력 하 고 확장 가능한 응용 프로그램을 생성 하는 방법을 매우 단순 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="04841-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="04841-107">해제 쇼핑, 체크 아웃 및 관리를 포함 하는 온라인 상점을 만들려고 ASP.NET 4에서 강력한 새 기능을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="04841-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="04841-108">이 자습서 시리즈 모든 Tailspin Spyworks 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="04841-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="04841-109">8 부 페이지 및 예외 처리에 대 한 연락처 페이지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="04841-109">Part 8 adds a contact page, about page, and exception handling.</span></span> <span data-ttu-id="04841-110">시리즈의 결론입니다.</span><span class="sxs-lookup"><span data-stu-id="04841-110">This is the conclusion of the series.</span></span>


## <a id="_Toc260221680"></a>  <span data-ttu-id="04841-111">페이지 (ASP.NET에서 이메일 보내기)에 문의</span><span class="sxs-lookup"><span data-stu-id="04841-111">Contact Page (Sending email from ASP.NET)</span></span>

<span data-ttu-id="04841-112">ContactUs.aspx 라는 새 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="04841-112">Create a new page named ContactUs.aspx</span></span>

<span data-ttu-id="04841-113">디자이너를 사용 하는 ToolkitScriptManager 등의 AjaxdControlToolkit 편집기 컨트롤을 특수 기록 형식을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="04841-113">Using the designer, create the following form taking special note to include the ToolkitScriptManager and the Editor control from the AjaxdControlToolkit.</span></span> <span data-ttu-id="04841-114">.</span><span class="sxs-lookup"><span data-stu-id="04841-114">.</span></span>

![](tailspin-spyworks-part-8/_static/image1.jpg)

<span data-ttu-id="04841-115">코드 숨김 파일에서에서 클릭 이벤트 처리기를 생성 하 고 연락처 정보를 전자 메일로 보내기 위한 메서드를 구현 하 여 "제출" 단추를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="04841-115">Double click on the "Submit" button to generate a click event handler in the code behind file and implement a method to send the contact information as an email.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample1.cs)]

<span data-ttu-id="04841-116">이 코드는 web.config 파일을 메일을 보내는 데 사용할 SMTP 서버를 지정 하는 구성 섹션의 항목 포함 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="04841-116">This code requires that your web.config file contain an entry in the configuration section that specifies the SMTP server to use for sending mail.</span></span>

[!code-xml[Main](tailspin-spyworks-part-8/samples/sample2.xml)]

## <a id="_Toc260221681"></a>  <span data-ttu-id="04841-117">페이지에 대 한</span><span class="sxs-lookup"><span data-stu-id="04841-117">About Page</span></span>

<span data-ttu-id="04841-118">AboutUs.aspx 라는 페이지를 만들고 원하는 모든 콘텐츠를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="04841-118">Create a page named AboutUs.aspx and add whatever content you like.</span></span>

## <a id="_Toc260221682"></a>  <span data-ttu-id="04841-119">전역 예외 처리기</span><span class="sxs-lookup"><span data-stu-id="04841-119">Global Exception Handler</span></span>

<span data-ttu-id="04841-120">마지막으로, 응용 프로그램에 걸쳐 우리는 throw 된 예외 되며 예측할 수 없는 경우에는 콜드 또한 웹 응용 프로그램에서 처리 되지 않은 원인 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="04841-120">Lastly, throughout the application we have thrown exceptions and there are unforeseen circumstances that cold also cause unhandled exceptions in our web application.</span></span>

<span data-ttu-id="04841-121">웹 사이트 방문자에 게 표시할 처리 되지 않은 예외가 없습니다 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="04841-121">We never want an unhandled exception to be displayed to a web site visitor.</span></span>

![](tailspin-spyworks-part-8/_static/image2.jpg)

<span data-ttu-id="04841-122">처리 되지 않은 예외는 끔찍한 사용자 경험 중 외에도 보안 문제가 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04841-122">Apart from being a terrible user experience unhandled exceptions can also be a security problem.</span></span>

<span data-ttu-id="04841-123">이 문제를 해결 하려면 전역 예외 처리기를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="04841-123">To solve this problem we will implement a global exception handler.</span></span>

<span data-ttu-id="04841-124">이렇게 하려면 Global.asax 파일을 열고 다음 미리 생성 된 이벤트 처리기를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="04841-124">To do this, open the Global.asax file and note the following pre-generated event handler.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample3.cs)]

<span data-ttu-id="04841-125">응용 프로그램을 구현 하는 코드를 추가\_다음과 같은 오류 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="04841-125">Add code to implement the Application\_Error handler as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample4.cs)]

<span data-ttu-id="04841-126">그런 다음 솔루션에 Error.aspx 라는 페이지를 추가 하 고이 마크업 코드 조각 추가.</span><span class="sxs-lookup"><span data-stu-id="04841-126">Then add a page named Error.aspx to the solution and add this markup snippet.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-8/samples/sample5.aspx)]

<span data-ttu-id="04841-127">페이지에서 이제\_Request 개체에서 이벤트 처리기 추출 오류 메시지를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="04841-127">Now in the Page\_Load event handler extract the error messages from the Request Object.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample6.cs)]

## <a id="_Toc260221683"></a>  <span data-ttu-id="04841-128">결론</span><span class="sxs-lookup"><span data-stu-id="04841-128">Conclusion</span></span>

<span data-ttu-id="04841-129">ASP.NET WebForms 쉽게 살펴본 등 데이터베이스 액세스, 멤버 자격, AJAX 사용 하 여 정교한 웹 사이트를 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="04841-129">We've seen that ASP.NET WebForms makes it easy to create a sophisticated website with database access, membership, AJAX, etc.</span></span> <span data-ttu-id="04841-130">매우 신속 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="04841-130">pretty quickly.</span></span>

<span data-ttu-id="04841-131">다행히이 자습서가 제공한 고유한 ASP.NET WebForms 응용 프로그램 구축을 시작 하는 데 필요한 도구!</span><span class="sxs-lookup"><span data-stu-id="04841-131">Hopefully this tutorial has given you the tools you need to get started building your own ASP.NET WebForms applications!</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="04841-132">이전</span><span class="sxs-lookup"><span data-stu-id="04841-132">Previous</span></span>](tailspin-spyworks-part-7.md)
