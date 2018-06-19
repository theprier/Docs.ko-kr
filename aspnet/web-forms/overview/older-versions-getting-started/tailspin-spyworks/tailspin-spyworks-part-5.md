---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-5
title: '5 단계: 비즈니스 논리 | Microsoft Docs'
author: JoeStagner
description: 이 자습서 시리즈 모든 Tailspin Spyworks 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다. 5 단계는 비즈니스 논리를 추가합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/21/2010
ms.topic: article
ms.assetid: eaef475a-ca91-47ea-a4a7-d074005ed80c
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-5
msc.type: authoredcontent
ms.openlocfilehash: e4342e634ef8c4bcf4e0085650a28f414ab23736
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30885083"
---
<a name="part-5-business-logic"></a><span data-ttu-id="33033-104">5 단계: 비즈니스 논리</span><span class="sxs-lookup"><span data-stu-id="33033-104">Part 5: Business Logic</span></span>
====================
<span data-ttu-id="33033-105">으로 [Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="33033-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="33033-106">Tailspin Spyworks.NET 플랫폼에 대해 강력 하 고 확장 가능한 응용 프로그램을 만드는 방법을 매우 간단한는 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="33033-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="33033-107">Off 쇼핑, 체크 아웃, 및 관리를 포함 하 여 온라인 상점에서는 만들려는 ASP.NET 4에서 멋진 새로운 기능을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="33033-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="33033-108">이 자습서 시리즈 모든 Tailspin Spyworks 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="33033-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="33033-109">5 단계는 비즈니스 논리를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="33033-109">Part 5 adds some business logic.</span></span>


## <a id="_Toc260221671"></a>  <span data-ttu-id="33033-110">일부 비즈니스 논리 추가</span><span class="sxs-lookup"><span data-stu-id="33033-110">Adding Some Business Logic</span></span>

<span data-ttu-id="33033-111">웹 사이트를 방문 하는 사람이 때마다 사용할 수 있도록 쇼핑 경험상 주시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="33033-111">We want our shopping experience to be available whenever someone visits our web site.</span></span> <span data-ttu-id="33033-112">방문자를 찾아보고 등록 되거나에 기록 되지 않을 경우에 장바구니에 항목을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33033-112">Visitors will be able to browse and add items to the shopping cart even if they are not registered or logged in.</span></span> <span data-ttu-id="33033-113">체크 아웃 준비가 될 때 부여 됩니다 인증 하기 위한 옵션 되며 그렇지 않은 경우 아직 멤버 수 없게 됩니다 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33033-113">When they are ready to check out they will be given the option to authenticate and if they are not yet members they will be able to create an account.</span></span>

<span data-ttu-id="33033-114">즉, "사용자 등록 된" 상태로 쇼핑 카트 익명 상태에서 변환할 논리를 구현 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33033-114">This means that we will need to implement the logic to convert the shopping cart from an anonymous state to a "Registered User" state.</span></span>

<span data-ttu-id="33033-115">보겠습니다 "클래스" 라는 디렉터리를 만들고 마우스 오른쪽 단추로 클릭 폴더 MyShoppingCart.cs 라는 새 "Class" 파일을 만듭니다</span><span class="sxs-lookup"><span data-stu-id="33033-115">Let's create a directory named "Classes" then Right-Click on the folder and create a new "Class" file named MyShoppingCart.cs</span></span>

![](tailspin-spyworks-part-5/_static/image1.jpg)

![](tailspin-spyworks-part-5/_static/image1.png)

<span data-ttu-id="33033-116">앞서 설명한 것 처럼 작업이 수행 됩니다이 사용 하 고 MyShoppingCart.aspx 페이지를 구현 하는 클래스 확장 해 보겠습니다. NET의 강력한 "Partial 클래스" 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="33033-116">As previously mentioned we will be extending the class that implements the MyShoppingCart.aspx page and we will do this using .NET's powerful "Partial Class" construct.</span></span>

<span data-ttu-id="33033-117">쿼리하여 MyShoppingCart.aspx.cf 파일에 대 한 생성 된 호출은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="33033-117">The generated call for our MyShoppingCart.aspx.cf file looks like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample1.cs)]

<span data-ttu-id="33033-118">Note "부분" 키워드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="33033-118">Note the use of the "partial" keyword.</span></span>

<span data-ttu-id="33033-119">방금 생성 된 클래스 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="33033-119">The class file that we just generated looks like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample2.cs)]

<span data-ttu-id="33033-120">Partial 키워드도이 파일에 추가 하 여 우리의 구현 병합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33033-120">We will merge our implementations by adding the partial keyword to this file as well.</span></span>

<span data-ttu-id="33033-121">이제 당사의 새 클래스 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="33033-121">Our new class file now looks like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample3.cs)]

<span data-ttu-id="33033-122">클래스를 추가 하는 첫 번째 메서드는 "AddItem" 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="33033-122">The first method that we will add to our class is the "AddItem" method.</span></span> <span data-ttu-id="33033-123">이 방법은 사용자가 제품 목록 및 제품 세부 정보 페이지에 "아트를 추가" 링크를 클릭할 때 궁극적으로 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33033-123">This is the method that will ultimately be called when the user clicks on the "Add to Art" links on the Product List and Product Details pages.</span></span>

<span data-ttu-id="33033-124">다음을 사용 하는 추가 페이지 맨 위에 있는 문.</span><span class="sxs-lookup"><span data-stu-id="33033-124">Append the following to the using statements at the top of the page.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample4.cs)]

<span data-ttu-id="33033-125">이 메서드는 MyShoppingCart 클래스에 추가 하십시오.</span><span class="sxs-lookup"><span data-stu-id="33033-125">And add this method to the MyShoppingCart class.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample5.cs)]

<span data-ttu-id="33033-126">LINQ to Entities에 항목이 바구니에 이미 있는지 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="33033-126">We are using LINQ to Entities to see if the item is already in the cart.</span></span> <span data-ttu-id="33033-127">따라서 항목의 주문 수량을 업데이트, 그렇지 않으면 만듭니다 선택한 항목에 대 한 새 항목</span><span class="sxs-lookup"><span data-stu-id="33033-127">If so, we update the order quantity of the item, otherwise we create a new entry for the selected item</span></span>

<span data-ttu-id="33033-128">이 메서드를 호출 하기 위해이 메서드를 클래스 뿐 아니라 다음 항목이 추가 된 후 = 장바구니 현재를 표시 하는 AddToCart.aspx 페이지를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="33033-128">In order to call this method we will implement an AddToCart.aspx page that not only class this method but then displayed the current shopping a=cart after the item has been added.</span></span>

<span data-ttu-id="33033-129">솔루션 탐색기에서 솔루션 이름을 마우스 오른쪽 단추로 클릭 하 고 추가 하 고 이전에 수행한 대로 AddToCart.aspx 라는 새 페이지.</span><span class="sxs-lookup"><span data-stu-id="33033-129">Right-Click on the solution name in the solution explorer and add and new page named AddToCart.aspx as we have done previously.</span></span>

<span data-ttu-id="33033-130">구현을 낮은 스톡 문제 등과 같은 중간 결과 표시 하려면이 페이지를 사용할 수 있는 동안 페이지는 실제로 렌더링 되는 대신 "추가" 논리 호출 있고 리디렉션 합니다.</span><span class="sxs-lookup"><span data-stu-id="33033-130">While we could use this page to display interim results like low stock issues, etc, in our implementation, the page will not actually render, but rather call the "Add" logic and redirect.</span></span>

<span data-ttu-id="33033-131">이렇게 하려면 페이지에 다음 코드 추가 하겠습니다\_Load 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="33033-131">To accomplish this we'll add the following code to the Page\_Load event.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample6.cs)]

<span data-ttu-id="33033-132">클래스의 AddItem 메서드를 호출 하는 쿼리 문자열 매개 변수에서 장바구니에 추가 하려면 제품 검색 되는 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="33033-132">Note that we are retrieving the product to add to the shopping cart from a QueryString parameter and calling the AddItem method of our class.</span></span>

<span data-ttu-id="33033-133">발생 한 오류가 없으면 가정할 때 다음 구현 완벽 하 게 해 주는 SHoppingCart.aspx 페이지에 제어가 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33033-133">Assuming no errors are encountered control is passed to the SHoppingCart.aspx page which we will fully implement next.</span></span> <span data-ttu-id="33033-134">오류가 없어야 하는 경우 예외를 throw 했습니다.</span><span class="sxs-lookup"><span data-stu-id="33033-134">If there should be an error we throw an exception.</span></span>

<span data-ttu-id="33033-135">현재 구현 하지 않았습니다 아직 전역 오류 처리기를이 예외는 응용 프로그램에서 처리 되지 않은 거쳐야 하지만 여기서는이 문제를 해결할 곧 합니다.</span><span class="sxs-lookup"><span data-stu-id="33033-135">Currently we have not yet implemented a global error handler so this exception would go unhandled by our application but we will remedy this shortly.</span></span>

<span data-ttu-id="33033-136">참고 (을 통해 사용 가능 Debug.Fail() 문 사용도 `using System.Diagnostics;)`</span><span class="sxs-lookup"><span data-stu-id="33033-136">Note also the use of the statement Debug.Fail() (available via `using System.Diagnostics;)`</span></span>

<span data-ttu-id="33033-137">응용 프로그램이 디버거 내에서 실행 중인이 메서드를 지정 하는 오류 메시지와 함께 응용 프로그램 상태에 대 한 정보로 세부 대화 상자를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="33033-137">Is the application is running inside the debugger, this method will display a detailed dialog with information about the applications state along with the error message that we specify.</span></span>

<span data-ttu-id="33033-138">에서 실행 중일 때 프로덕션은 Debug.Fail() 문이 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33033-138">When running in production the Debug.Fail() statement is ignored.</span></span>

<span data-ttu-id="33033-139">위의 당사의 쇼핑 카트 클래스 이름 "GetShoppingCartId"에 메서드가에 대 한 호출 코드에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33033-139">You will note in the code above a call to a method in our shopping cart class names "GetShoppingCartId".</span></span>

<span data-ttu-id="33033-140">메서드를 구현 하는 다음과 같은 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="33033-140">Add the code to implement the method as follows.</span></span>

<span data-ttu-id="33033-141">Note도 업데이트 및 체크 아웃 단추와 카트 "전체"를 표시할 수 있습니다는 레이블을 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="33033-141">Note that we've also added update and checkout buttons and a label where we can display the cart "total".</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample7.cs)]

<span data-ttu-id="33033-142">이제 항목 당사의 쇼핑 카트를 추가할 수 있습니다 하지만 제품을 추가한 후 카트를 표시 하는 논리를 구현 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="33033-142">We can now add items to our shopping cart but we have not implemented the logic to display the cart after a product has been added.</span></span>

<span data-ttu-id="33033-143">따라서 MyShoppingCart.aspx 페이지에 추가 합니다 EntityDataSource 컨트롤 및 GridVire 컨트롤 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="33033-143">So, in the MyShoppingCart.aspx page we'll add an EntityDataSource control and a GridVire control as follows.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample8.aspx)]

<span data-ttu-id="33033-144">Updatecart 단추 두 번 클릭 하 고 태그에 선언에 지정 하는 click 이벤트 처리기를 생성할 수 있도록 디자이너에서 폼을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="33033-144">Call up the form in the designer so that you can double click on the Update Cart button and generate the click event handler that is specified in the declaration in the markup.</span></span>

<span data-ttu-id="33033-145">세부 정보는 나중에 구현 하지만이 작업을 수행 하겠습니다 빌드하고 오류 없이 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="33033-145">We'll implement the details later but doing this will let us build and run our application without errors.</span></span>

<span data-ttu-id="33033-146">응용 프로그램을 실행 하 고 장바구니에 항목을 추가 하는 경우이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33033-146">When you run the application and add an item to the shopping cart you will see this.</span></span>

![](tailspin-spyworks-part-5/_static/image2.jpg)

<span data-ttu-id="33033-147">우리는 약간 "default" 그리드 화면에서 세 개의 사용자 지정 열을 구현 하 여 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="33033-147">Note that we have deviated from the "default" grid display by implementing three custom columns.</span></span>

<span data-ttu-id="33033-148">첫 번째 편집, 수량에 대 한 "바인딩된" 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="33033-148">The first is an Editable, "Bound" field for the Quantity:</span></span>

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample9.aspx)]

<span data-ttu-id="33033-149">다음은 품목 합계가 (항목 시간을 정렬할 수량으로 비용)를 표시 하는 "계산된" 열:</span><span class="sxs-lookup"><span data-stu-id="33033-149">The next is a "calculated" column that displays the line item total (the item cost times the quantity to be ordered):</span></span>

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample10.aspx)]

<span data-ttu-id="33033-150">마지막으로 사용자가 항목을 쇼핑 차트에서 제거할 수 있는지를 나타내는 데 사용할 CheckBox 컨트롤을 포함 하는 사용자 지정 열을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="33033-150">Lastly we have a custom column that contains a CheckBox control that the user will use to indicate that the item should be removed from the shopping chart.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample11.aspx)]

![](tailspin-spyworks-part-5/_static/image3.jpg)

<span data-ttu-id="33033-151">볼 수 있듯이 총 줄이 비어 있으므로 순서 주문 총액을 계산 하는 일부 논리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="33033-151">As you can see, the Order Total line is empty so let's add some logic to calculate the Order Total.</span></span>

<span data-ttu-id="33033-152">먼저 MyShoppingCart 클래스 "GetTotal" 메서드를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="33033-152">We'll first implement a "GetTotal" method to our MyShoppingCart Class.</span></span>

<span data-ttu-id="33033-153">MyShoppingCart.cs 파일에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="33033-153">In the MyShoppingCart.cs file add the following code.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample12.cs)]

<span data-ttu-id="33033-154">페이지에서 다음\_Load 이벤트 처리기 합니다 우리의 GetTotal 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33033-154">Then in the Page\_Load event handler we'll can call our GetTotal method.</span></span> <span data-ttu-id="33033-155">동시에 테스트 경우 그에 따라 표시를 조정 하 고 쇼핑 카트가 비어 있는지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="33033-155">At the same time we'll add a test to see if the shopping cart is empty and adjust the display accordingly if it is.</span></span>

<span data-ttu-id="33033-156">이제 쇼핑 카트 비어 있으면이 가져올 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33033-156">Now if the shopping cart is empty we get this:</span></span>

![](tailspin-spyworks-part-5/_static/image4.jpg)

<span data-ttu-id="33033-157">고 그렇지 않은 경우이 합계 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="33033-157">And if not, we see our total.</span></span>

![](tailspin-spyworks-part-5/_static/image5.jpg)

<span data-ttu-id="33033-158">그러나이 페이지 아직 완료 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="33033-158">However, this page is not yet complete.</span></span>

<span data-ttu-id="33033-159">제거를 위해 표시 된 항목을 제거 하 고 일부 변경 눈금에서 사용자가 대로 새 수량 값을 확인 하 여 쇼핑 카트를 다시 계산 하는 추가 논리가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="33033-159">We will need additional logic to recalculate the shopping cart by removing items marked for removal and by determining new quantity values as some may have been changed in the grid by the user.</span></span>

<span data-ttu-id="33033-160">"RemoveItem" 메서드 MyShoppingCart.cs 사용자 제거에 대 한 항목을 표시 하는 경우에 경우를 처리 하도록에서 당사의 쇼핑 카트 클래스를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33033-160">Lets add a "RemoveItem" method to our shopping cart class in MyShoppingCart.cs to handle the case when a user marks an item for removal.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample13.cs)]

<span data-ttu-id="33033-161">이제 보겠습니다 ad 사용자가을 GridView에서 정렬할 품질 간단히 변경할 때 상황을 처리 하는 메서드.</span><span class="sxs-lookup"><span data-stu-id="33033-161">Now let's ad a method to handle the circumstance when a user simply changes the quality to be ordered in the GridView.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample14.cs)]

<span data-ttu-id="33033-162">위치에 기본 제거 및 업데이트 기능을 갖춘 실제로 데이터베이스의 쇼핑 카트를 업데이트 하는 논리를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33033-162">With the basic Remove and Update features in place we can implement the logic that actually updates the shopping cart in the database.</span></span> <span data-ttu-id="33033-163">(에 MyShoppingCart.cs)</span><span class="sxs-lookup"><span data-stu-id="33033-163">(In MyShoppingCart.cs)</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample15.cs)]

<span data-ttu-id="33033-164">이 메서드는 두 개의 매개 변수가 필요는 사실을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33033-164">You'll note that this method expects two parameters.</span></span> <span data-ttu-id="33033-165">하나는 쇼핑 카트 Id이 고 다른 사용자 정의 형식 개체의 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="33033-165">One is the shopping cart Id and the other is an array of objects of user defined type.</span></span>

<span data-ttu-id="33033-166">사용자 인터페이스 사항에이 논리의 종속성을 최소화할 수 있도록 म म 메서드에 직접 GridView 컨트롤에 액세스할 필요 없이 코드에 쇼핑 카트에 항목을 전달 하는 데 사용할 수 있는 데이터 구조를 정의 했습니다.</span><span class="sxs-lookup"><span data-stu-id="33033-166">So as to minimize the dependency of our logic on user interface specifics, we've defined a data structure that we can use to pass the shopping cart items to our code without our method needing to directly access the GridView control.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample16.cs)]

<span data-ttu-id="33033-167">MyShoppingCart.aspx.cs 파일에서 사용할 수 있습니다이 구조에서 업데이트 단추 클릭 이벤트 처리기 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="33033-167">In our MyShoppingCart.aspx.cs file we can use this structure in our Update Button Click Event handler as follows.</span></span> <span data-ttu-id="33033-168">Note 카트 업데이트할 뿐만 아니라 म 카트 합계도 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33033-168">Note that in addition to updating the cart we will update the cart total as well.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample17.cs)]

<span data-ttu-id="33033-169">이 줄의 코드를 있는 관심 있는 특정 note:</span><span class="sxs-lookup"><span data-stu-id="33033-169">Note with particular interest this line of code:</span></span>

[!code-javascript[Main](tailspin-spyworks-part-5/samples/sample18.js)]

<span data-ttu-id="33033-170">GetValues()는 특수 한 도우미 함수 MyShoppingCart.aspx.cs에서 다음과 같이 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33033-170">GetValues() is a special helper function that we will implement in MyShoppingCart.aspx.cs as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample19.cs)]

<span data-ttu-id="33033-171">이 GridView 컨트롤에 바인딩된 요소 값에 액세스 하는 방법은 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="33033-171">This provides a clean way to access the values of the bound elements in our GridView control.</span></span> <span data-ttu-id="33033-172">"제거 Item" CheckBox 컨트롤의 바인딩되지 않은 이후 FindControl() 메서드를 통해 액세스할 합니다.</span><span class="sxs-lookup"><span data-stu-id="33033-172">Since our "Remove Item" CheckBox Control is not bound we'll access it via the FindControl() method.</span></span>

<span data-ttu-id="33033-173">프로젝트의 개발에이 단계에서 체크 아웃 프로세스를 구현 준비 중 했습니다.</span><span class="sxs-lookup"><span data-stu-id="33033-173">At this stage in your project's development we are getting ready to implement the checkout process.</span></span>

<span data-ttu-id="33033-174">보겠습니다 이렇게 하기 전에 멤버 자격 데이터베이스를 생성 하 고 사용자 멤버 자격 리포지토리를 추가 하려면 Visual Studio를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="33033-174">Before doing so let's use Visual Studio to generate the membership database and add a user to the membership repository.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="33033-175">[이전](tailspin-spyworks-part-4.md)
> [다음](tailspin-spyworks-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="33033-175">[Previous](tailspin-spyworks-part-4.md)
[Next](tailspin-spyworks-part-6.md)</span></span>
