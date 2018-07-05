---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
title: '6 부: ASP.NET 멤버 자격 | Microsoft Docs'
author: JoeStagner
description: 이 자습서 시리즈 모든 Tailspin Spyworks 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 6 부 ASP.NET 멤버 자격을 추가합니다.
ms.author: aspnetcontent
ms.date: 07/21/2010
ms.assetid: f70a310c-9557-4743-82cb-655265676d39
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
msc.type: authoredcontent
ms.openlocfilehash: 303c1edf548db1da9ef61d94bdd8157d6afbb2e4
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37804422"
---
<a name="part-6-aspnet-membership"></a><span data-ttu-id="cfdc4-104">6 부: ASP.NET 멤버 자격</span><span class="sxs-lookup"><span data-stu-id="cfdc4-104">Part 6: ASP.NET Membership</span></span>
====================
<span data-ttu-id="cfdc4-105">[Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="cfdc4-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="cfdc4-106">Tailspin Spyworks.NET 플랫폼에 대 한 강력 하 고 확장 가능한 응용 프로그램을 생성 하는 방법을 매우 단순 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cfdc4-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="cfdc4-107">해제 쇼핑, 체크 아웃 및 관리를 포함 하는 온라인 상점을 만들려고 ASP.NET 4에서 강력한 새 기능을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cfdc4-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="cfdc4-108">이 자습서 시리즈 모든 Tailspin Spyworks 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdc4-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="cfdc4-109">6 부 ASP.NET 멤버 자격을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdc4-109">Part 6 adds ASP.NET Membership.</span></span>


## <a id="_Toc260221672"></a>  <span data-ttu-id="cfdc4-110">ASP.NET 멤버 자격 사용</span><span class="sxs-lookup"><span data-stu-id="cfdc4-110">Working with ASP.NET Membership</span></span>

![](tailspin-spyworks-part-6/_static/image1.png)

<span data-ttu-id="cfdc4-111">보안을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdc4-111">Click Security</span></span>

![](tailspin-spyworks-part-6/_static/image1.jpg)

<span data-ttu-id="cfdc4-112">폼 인증 사용 한다고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdc4-112">Make sure that we are using forms authentication.</span></span>

![](tailspin-spyworks-part-6/_static/image2.jpg)

<span data-ttu-id="cfdc4-113">"Create User" 링크를 사용 하 여 몇 명의 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cfdc4-113">Use the "Create User" link to create a couple of users.</span></span>

![](tailspin-spyworks-part-6/_static/image3.jpg)

<span data-ttu-id="cfdc4-114">을 완료 한 후 솔루션 탐색기 창을 참조 및 보기를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="cfdc4-114">When done, refer to the Solution Explorer window and refresh the view.</span></span>

![](tailspin-spyworks-part-6/_static/image2.png)

<span data-ttu-id="cfdc4-115">ASPNETDB를 합니다. MDF 세밀 하 게 작성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdc4-115">Note that the ASPNETDB.MDF fine has been created.</span></span> <span data-ttu-id="cfdc4-116">이 파일을 사용 하면 멤버 자격 등 ASP.NET 핵심 서비스를 지원 하기 위해 표가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdc4-116">This file contains the tables to support the core ASP.NET services like membership.</span></span>

<span data-ttu-id="cfdc4-117">이제 체크 아웃 프로세스의 구현을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdc4-117">Now we can begin implementing the checkout process.</span></span>

<span data-ttu-id="cfdc4-118">CheckOut.aspx 페이지를 만들어 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdc4-118">Begin by creating a CheckOut.aspx page.</span></span>

<span data-ttu-id="cfdc4-119">CheckOut.aspx 페이지는 로그인 된 사용자 및 로그인 페이지에 로그인 하지 않은 사용자 리디렉션에 대 한 액세스 제한 됩니다 있도록 로그인 사용자를 사용할 수만 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdc4-119">The CheckOut.aspx page should only be available to users who are logged in so we will restrict access to logged in users and redirect users who are not logged in to the LogIn page.</span></span>

<span data-ttu-id="cfdc4-120">이렇게 하려면 다음 web.config 파일의 구성 섹션을 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdc4-120">To do this we'll add the following to the configuration section of our web.config file.</span></span>

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample1.xml)]

<span data-ttu-id="cfdc4-121">ASP.NET Web Forms 응용 프로그램에 대 한 템플릿을 자동으로 인증 섹션을 web.config 파일에 추가 하 고 기본 로그인 페이지를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdc4-121">The template for ASP.NET Web Forms applications automatically added an authentication section to our web.config file and established the default login page.</span></span>

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample2.xml)]

<span data-ttu-id="cfdc4-122">에서는 Login.aspx 코드 숨김 사용자가 로그인 할 때 익명 장바구니 마이그레이션 파일을 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdc4-122">We must modify the Login.aspx code behind file to migrate an anonymous shopping cart when the user logs in.</span></span> <span data-ttu-id="cfdc4-123">페이지 변경\_다음과 같이 이벤트를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdc4-123">Change the Page\_Load event as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample3.cs)]

<span data-ttu-id="cfdc4-124">세션 이름을 새로 로그인된 한 사용자로 설정 하 고 MyShoppingCart 클래스에서 MigrateCart 메서드를 호출 하 여 사용자의 장바구니에 임시 세션 id를 변경 하기 위해 다음과 같은 "LoggedIn" 이벤트 처리기를 추가 하십시오.</span><span class="sxs-lookup"><span data-stu-id="cfdc4-124">Then add a "LoggedIn" event handler like this to set the session name to the newly logged in user and change the temporary session id in the shopping cart to that of the user by calling the MigrateCart method in our MyShoppingCart class.</span></span> <span data-ttu-id="cfdc4-125">(.Cs 파일에서 구현 됨)</span><span class="sxs-lookup"><span data-stu-id="cfdc4-125">(Implemented in the .cs file)</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample4.cs)]

<span data-ttu-id="cfdc4-126">MigrateCart() 메서드 구현에는 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdc4-126">Implement the MigrateCart() method like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample5.cs)]

<span data-ttu-id="cfdc4-127">Checkout.aspx에서는 사용 하 여 한 EntityDataSource 및 GridView는 확인 페이지에서 당사의 쇼핑 카트 페이지에서 수행한 것 만큼 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdc4-127">In checkout.aspx we'll use an EntityDataSource and a GridView in our check out page much as we did in our shopping cart page.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-6/samples/sample6.aspx)]

<span data-ttu-id="cfdc4-128">GridView 제어권 MyList 이라는 "ondatabound" 이벤트 처리기를 지정\_RowDataBound 다음과 같이 해당 이벤트 처리기를 구현 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdc4-128">Note that our GridView control specifies an "ondatabound" event handler named MyList\_RowDataBound so let's implement that event handler like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample7.cs)]

<span data-ttu-id="cfdc4-129">실행 중인 총 쇼핑 카트에 각 행은 바인딩되고 GridView의 맨 아래 행을 업데이트 하는 대로이 메서드가 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdc4-129">This method keeps a running total of the shopping cart as each row is bound and updates the bottom row of the GridView.</span></span>

<span data-ttu-id="cfdc4-130">이 단계에 배치 하려면 "review" 표시를 구현 했습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdc4-130">At this stage we have implemented a "review" presentation of the order to be placed.</span></span>

<span data-ttu-id="cfdc4-131">보겠습니다 페이지로 코드 몇 줄을 추가 하 여 빈 카트 시나리오를 처리할\_Load 이벤트:</span><span class="sxs-lookup"><span data-stu-id="cfdc4-131">Let's handle an empty cart scenario by adding a few lines of code to our Page\_Load event:</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample8.cs)]

<span data-ttu-id="cfdc4-132">사용자가 "제출" 단추를 클릭할 때 제출 단추 클릭 이벤트 처리기에서 다음 코드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdc4-132">When the user clicks on the "Submit" button we will execute the following code in the Submit Button Click Event handler.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample9.cs)]

<span data-ttu-id="cfdc4-133">주문 제출 프로세스의 "핵심" SubmitOrder() 메서드의 MyShoppingCart 클래스에서 구현 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cfdc4-133">The "meat" of the order submission process is to be implemented in the SubmitOrder() method of our MyShoppingCart class.</span></span>

<span data-ttu-id="cfdc4-134">SubmitOrder 작업이 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cfdc4-134">SubmitOrder will:</span></span>

- <span data-ttu-id="cfdc4-135">시장 바구니에 모든 품목을 가져와 새 주문 레코드를 만들고 연관된 된 OrderDetails 레코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdc4-135">Take all the line items in the shopping cart and use them to create a new Order Record and the associated OrderDetails records.</span></span>
- <span data-ttu-id="cfdc4-136">배송 날짜를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdc4-136">Calculate Shipping Date.</span></span>
- <span data-ttu-id="cfdc4-137">쇼핑 카트를 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="cfdc4-137">Clear the shopping cart.</span></span>


[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample10.cs)]

<span data-ttu-id="cfdc4-138">이 샘플 응용 프로그램의 목적에 대 한 현재 날짜에 2 일을 추가 하기만 하면 운송 날짜를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdc4-138">For the purposes of this sample application we'll calculate a ship date by simply adding two days to the current date.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample11.cs)]

<span data-ttu-id="cfdc4-139">이제 응용 프로그램을 실행 시작부터 끝까지 쇼핑 프로세스 테스트를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdc4-139">Running the application now will permit us to test the shopping process from start to finish.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="cfdc4-140">[이전](tailspin-spyworks-part-5.md)
> [다음](tailspin-spyworks-part-7.md)</span><span class="sxs-lookup"><span data-stu-id="cfdc4-140">[Previous](tailspin-spyworks-part-5.md)
[Next](tailspin-spyworks-part-7.md)</span></span>
