---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-3
title: "3 부: 레이아웃 및 범주 메뉴 | Microsoft Docs"
author: JoeStagner
description: "이 자습서 시리즈 모든 Tailspin Spyworks 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다. 3 부에서는 레이아웃 및 범주 메뉴를 추가 합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/21/2010
ms.topic: article
ms.assetid: 94ea1a70-a9bc-4241-8f36-08366d64bab9
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-3
msc.type: authoredcontent
ms.openlocfilehash: 57c0342efb67b94a0d8c8b06dc13a727e7184db8
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="part-3-layout-and-category-menu"></a><span data-ttu-id="219f5-104">3 부: 레이아웃 및 범주 메뉴</span><span class="sxs-lookup"><span data-stu-id="219f5-104">Part 3: Layout and Category Menu</span></span>
====================
<span data-ttu-id="219f5-105">으로 [Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="219f5-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="219f5-106">Tailspin Spyworks.NET 플랫폼에 대해 강력 하 고 확장 가능한 응용 프로그램을 만드는 방법을 매우 간단한는 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="219f5-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="219f5-107">Off 쇼핑, 체크 아웃, 및 관리를 포함 하 여 온라인 상점에서는 만들려는 ASP.NET 4에서 멋진 새로운 기능을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="219f5-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="219f5-108">이 자습서 시리즈 모든 Tailspin Spyworks 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="219f5-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="219f5-109">3 부에서는 레이아웃 및 범주 메뉴를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="219f5-109">Part 3 covers adding layout and a category menu.</span></span>


## <a id="_Toc260221669"></a><span data-ttu-id="219f5-110">일부 레이아웃 및 범주 메뉴 추가</span><span class="sxs-lookup"><span data-stu-id="219f5-110">Adding Some Layout and a Category Menu</span></span>

<span data-ttu-id="219f5-111">가격 사이트 마스터 페이지에서이 제품 범주 메뉴에 있는 왼쪽 열에 대 한 div를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="219f5-111">In our site master page we'll add a div for the left side column that will contain our product category menu.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-3/samples/sample1.aspx)]

<span data-ttu-id="219f5-112">Note는 원하는 정렬 및 기타 서식에서 제공 합니다 쿼리하여 Style.css 파일을 추가 하는 CSS 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="219f5-112">Note that the desired aligning and other formatting will be provided by the CSS class that we added to our Style.css file.</span></span>

[!code-css[Main](tailspin-spyworks-part-3/samples/sample2.css)]

<span data-ttu-id="219f5-113">기존 제품 범주 및 메뉴 항목을 만들 및 해당 연결에 대 한 상거래 데이터베이스를 쿼리하여 런타임 시 제품 범주 메뉴를 동적으로 만들 수 됩니다.</span><span class="sxs-lookup"><span data-stu-id="219f5-113">The product category menu will be dynamically created at runtime by querying the Commerce database for existing product categories and creating the menu items and corresponding links.</span></span>

<span data-ttu-id="219f5-114">이렇게 하려면 두 ASP를 사용 합니다. NET의 강력한 데이터를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="219f5-114">To accomplish this we will use two of ASP.NET's powerful data controls.</span></span> <span data-ttu-id="219f5-115">"데이터 원본 엔터티" 컨트롤과 "ListView" 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="219f5-115">The "Entity Data Source" control and the "ListView" control.</span></span>

![](tailspin-spyworks-part-3/_static/image1.jpg)

<span data-ttu-id="219f5-116">디자인 뷰로 전환 "" 하 고이 컨트롤을 구성 하는 도우미를 사용 하 여 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="219f5-116">Let's switch to "Design View" and use the helpers to configure our controls.</span></span>

![](tailspin-spyworks-part-3/_static/image2.jpg)

<span data-ttu-id="219f5-117">EDS로 EntityDataSource ID 속성을 설정 해 보겠습니다\_범주\_메뉴와 "데이터 소스 구성"를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="219f5-117">Let's set the EntityDataSource ID property to EDS\_Category\_Menu and click on "Configure Data Source".</span></span>

![](tailspin-spyworks-part-3/_static/image3.jpg)

<span data-ttu-id="219f5-118">Commerce 데이터베이스에 대 한 엔터티 데이터 원본 모델을 만들 때 us에 대해 만들어진 CommerceEntities 연결을 선택 하 고 "다음"을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="219f5-118">Select the CommerceEntities Connection that was created for us when we created the Entity Data Source Model for our Commerce Database and click "Next".</span></span>

![](tailspin-spyworks-part-3/_static/image4.jpg)

<span data-ttu-id="219f5-119">"또한 Categories" 엔터티 집합 이름을 선택 하 고 나머지 옵션은 기본값으로 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="219f5-119">Select the "Categories" Entity set name and leave the rest of the options as default.</span></span> <span data-ttu-id="219f5-120">"마침"을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="219f5-120">Click "Finish".</span></span>

<span data-ttu-id="219f5-121">이제 우리 ListView에 가격 페이지에 설정 된 ListView 컨트롤 인스턴스의 ID 속성을 설정 해 보겠습니다\_ProductsMenu 하 고 해당 도우미를 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="219f5-121">Now let's set the ID property of the ListView control instance that we placed on our page to ListView\_ProductsMenu and activate its helper.</span></span>

![](tailspin-spyworks-part-3/_static/image5.jpg)

<span data-ttu-id="219f5-122">그러나 제어 옵션을 사용 하 여 데이터 항목 표시 형식을 지정 수 있습니다 및 서식, 우리의 메뉴 만들기 놓기만 하면 간단한 표시 코드를 소스 뷰에서 입력할 됩니다 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="219f5-122">Though we could use control options to format the data item display and formatting, our menu creation will only require simple markup so we will enter the code in the source view.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-3/samples/sample3.aspx)]

<span data-ttu-id="219f5-123">"Eval" 문의 사항에 유의 하세요: &lt;% # Eval("CategoryName") %&gt;</span><span class="sxs-lookup"><span data-stu-id="219f5-123">Please note the "Eval" statement : &lt;%# Eval("CategoryName") %&gt;</span></span>

<span data-ttu-id="219f5-124">ASP.NET 구문 &lt;% # %&gt; 는 무엇이 든 내에 포함 된 결과 출력할 "의 줄"를 실행 하기 위해 런타임 지시 하는 줄임 표기 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="219f5-124">The ASP.NET syntax &lt;%# %&gt; is a shorthand convention that instructs the runtime to execute whatever is contained within and output the results "in Line".</span></span>

<span data-ttu-id="219f5-125">엔터티 모델 항목 이름의 값을 "CatagoryName" 인출 Eval("CategoryName") 문에 데이터 항목의 바인딩된 컬렉션에 현재 항목에 대 한 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="219f5-125">The statement Eval("CategoryName") instructs that, for the current entry in the bound collection of data items, fetch the value of the Entity Model item names "CatagoryName".</span></span> <span data-ttu-id="219f5-126">간결한 구문은 매우 강력한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="219f5-126">This is concise syntax for a very powerful feature.</span></span>

<span data-ttu-id="219f5-127">응용 프로그램을 지금 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="219f5-127">Lets run the application now.</span></span>

![](tailspin-spyworks-part-3/_static/image6.jpg)

<span data-ttu-id="219f5-128">에 불과하며 우리의 제품 범주 메뉴 표시 되 고 ProductsList.aspx 라는 메뉴 항목 링크가 가리키는 아직을 구현 해야 하는 페이지를 볼 수 있습니다 범주 메뉴 항목 중 하나 위에 가져간 म 포함 되어 있는지를 구축 했으므로 동적 쿼리 문자열 인수는는  범주 id입니다.</span><span class="sxs-lookup"><span data-stu-id="219f5-128">Note that our product category menu is now displayed and when we hover over one of the category menu items we can see the menu item link points to a page we have yet to implement named ProductsList.aspx and that we have built a dynamic query string argument that contains the category id.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="219f5-129">[이전](tailspin-spyworks-part-2.md)
[다음](tailspin-spyworks-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="219f5-129">[Previous](tailspin-spyworks-part-2.md)
[Next](tailspin-spyworks-part-4.md)</span></span>
