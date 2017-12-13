---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
title: "8 단계: 최종 페이지, 예외 처리 및 결론 | Microsoft Docs"
author: JoeStagner
description: "이 자습서 시리즈 모든 Tailspin Spyworks 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다. 8 부 페이지 및 예외에 대 한 연락처 페이지에 추가..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/21/2010
ms.topic: article
ms.assetid: 5aeadf8f-39f3-4f07-a78f-1c310c64fb23
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
msc.type: authoredcontent
ms.openlocfilehash: 0dd1717ff1051f18a78fe77402c7603008b9b486
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="part-8-final-pages-exception-handling-and-conclusion"></a><span data-ttu-id="1db4b-104">8 단계: 최종 페이지, 예외 처리 및 결론</span><span class="sxs-lookup"><span data-stu-id="1db4b-104">Part 8: Final Pages, Exception Handling, and Conclusion</span></span>
====================
<span data-ttu-id="1db4b-105">으로 [Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="1db4b-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="1db4b-106">Tailspin Spyworks.NET 플랫폼에 대해 강력 하 고 확장 가능한 응용 프로그램을 만드는 방법을 매우 간단한는 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1db4b-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="1db4b-107">Off 쇼핑, 체크 아웃, 및 관리를 포함 하 여 온라인 상점에서는 만들려는 ASP.NET 4에서 멋진 새로운 기능을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1db4b-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="1db4b-108">이 자습서 시리즈 모든 Tailspin Spyworks 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1db4b-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="1db4b-109">8 부 페이지 및 예외 처리에 대 한 연락처 페이지에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1db4b-109">Part 8 adds a contact page, about page, and exception handling.</span></span> <span data-ttu-id="1db4b-110">계열의 결론입니다.</span><span class="sxs-lookup"><span data-stu-id="1db4b-110">This is the conclusion of the series.</span></span>


## <a id="_Toc260221680"></a><span data-ttu-id="1db4b-111">페이지를 (ASP.NET에서 보내는 전자 메일)에 게 문의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="1db4b-111">Contact Page (Sending email from ASP.NET)</span></span>

<span data-ttu-id="1db4b-112">ContactUs.aspx 라는 새 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="1db4b-112">Create a new page named ContactUs.aspx</span></span>

<span data-ttu-id="1db4b-113">디자이너를 사용 하면 다음과 같은 형식은 ToolkitScriptManager 및는 AjaxdControlToolkit에서 편집기 컨트롤을 포함 하도록 특별 한 접근을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1db4b-113">Using the designer, create the following form taking special note to include the ToolkitScriptManager and the Editor control from the AjaxdControlToolkit.</span></span> <span data-ttu-id="1db4b-114">입니다.</span><span class="sxs-lookup"><span data-stu-id="1db4b-114">.</span></span>

![](tailspin-spyworks-part-8/_static/image1.jpg)

<span data-ttu-id="1db4b-115">코드 숨김 파일에에서는 click 이벤트 처리기를 생성 하 고 연락처 정보를 전자 메일로 보내도록 메서드를 구현 하려면 "제출" 단추를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1db4b-115">Double click on the "Submit" button to generate a click event handler in the code behind file and implement a method to send the contact information as an email.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample1.cs)]

<span data-ttu-id="1db4b-116">이 코드 하려면 메일을 보내는 데 사용할 SMTP 서버를 지정 하는 구성 섹션의 항목 web.config 파일에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1db4b-116">This code requires that your web.config file contain an entry in the configuration section that specifies the SMTP server to use for sending mail.</span></span>

[!code-xml[Main](tailspin-spyworks-part-8/samples/sample2.xml)]

## <a id="_Toc260221681"></a><span data-ttu-id="1db4b-117">페이지 정보</span><span class="sxs-lookup"><span data-stu-id="1db4b-117">About Page</span></span>

<span data-ttu-id="1db4b-118">AboutUs.aspx 라는 페이지를 만들고 원하는 모든 콘텐츠를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1db4b-118">Create a page named AboutUs.aspx and add whatever content you like.</span></span>

## <a id="_Toc260221682"></a><span data-ttu-id="1db4b-119">전역 예외 처리기</span><span class="sxs-lookup"><span data-stu-id="1db4b-119">Global Exception Handler</span></span>

<span data-ttu-id="1db4b-120">마지막으로, 응용 프로그램에 걸쳐 우리는 throw 된 예외 한 경우가 콜드는 예측할 수 없는 상황이 웹 응용 프로그램에서 처리 되지 않은 원인 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="1db4b-120">Lastly, throughout the application we have thrown exceptions and there are unforeseen circumstances that cold also cause unhandled exceptions in our web application.</span></span>

<span data-ttu-id="1db4b-121">처리 되지 않은 예외를 웹 사이트 방문자에 게 표시 되지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1db4b-121">We never want an unhandled exception to be displayed to a web site visitor.</span></span>

![](tailspin-spyworks-part-8/_static/image2.jpg)

<span data-ttu-id="1db4b-122">부문과 테러 사용자 경험은 별도로 처리 되지 않은 예외는 보안 문제가 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1db4b-122">Apart from being a terrible user experience unhandled exceptions can also be a security problem.</span></span>

<span data-ttu-id="1db4b-123">이 문제를 해결 하기 위해 전역 예외 처리기를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="1db4b-123">To solve this problem we will implement a global exception handler.</span></span>

<span data-ttu-id="1db4b-124">이 위해 Global.asax 파일을 열고 다음 미리 생성 된 이벤트 처리기를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1db4b-124">To do this, open the Global.asax file and note the following pre-generated event handler.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample3.cs)]

<span data-ttu-id="1db4b-125">응용 프로그램을 구현 하는 코드를 추가\_다음과 같은 오류 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="1db4b-125">Add code to implement the Application\_Error handler as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample4.cs)]

<span data-ttu-id="1db4b-126">그런 다음 솔루션에 Error.aspx 라는 페이지를 추가 하 고이 마크업 코드 조각 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1db4b-126">Then add a page named Error.aspx to the solution and add this markup snippet.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-8/samples/sample5.aspx)]

<span data-ttu-id="1db4b-127">페이지에 이제\_Request 개체에서 이벤트 처리기는 오류 메시지를 압축 해제를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="1db4b-127">Now in the Page\_Load event handler extract the error messages from the Request Object.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample6.cs)]

## <a id="_Toc260221683"></a><span data-ttu-id="1db4b-128">결론</span><span class="sxs-lookup"><span data-stu-id="1db4b-128">Conclusion</span></span>

<span data-ttu-id="1db4b-129">해당 ASP.NET WebForms 쉽게 버퍼 오버런 등의 데이터베이스 액세스 권한이 있으면 멤버 자격, AJAX 정교한 웹 사이트를 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1db4b-129">We've seen that that ASP.NET WebForms makes it easy to create a sophisticated website with database access, membership, AJAX, etc.</span></span> <span data-ttu-id="1db4b-130">매우 신속 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="1db4b-130">pretty quickly.</span></span>

<span data-ttu-id="1db4b-131">다행히이 자습서가 제공한 사용자 고유의 ASP.NET WebForms 응용 프로그램을 구축 하는 데 필요한 도구!</span><span class="sxs-lookup"><span data-stu-id="1db4b-131">Hopefully this tutorial has given you the tools you need to get started building your own ASP.NET WebForms applications!</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="1db4b-132">이전</span><span class="sxs-lookup"><span data-stu-id="1db4b-132">Previous</span></span>](tailspin-spyworks-part-7.md)
