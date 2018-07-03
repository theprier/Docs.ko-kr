---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-7
title: '7 부: 추가 기능 | Microsoft Docs'
author: JoeStagner
description: 이 자습서 시리즈 모든 Tailspin Spyworks 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 7 부 계정 revie 등의 추가 기능을 추가 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/21/2010
ms.topic: article
ms.assetid: 50223ee9-11b9-4cf3-bca2-e2f10bf471f3
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-7
msc.type: authoredcontent
ms.openlocfilehash: 8cdde10981835877e5ac2f65860010920a68d0a2
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37389178"
---
<a name="part-7-adding-features"></a><span data-ttu-id="69016-104">7 부: 추가 기능</span><span class="sxs-lookup"><span data-stu-id="69016-104">Part 7: Adding Features</span></span>
====================
<span data-ttu-id="69016-105">[Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="69016-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="69016-106">Tailspin Spyworks.NET 플랫폼에 대 한 강력 하 고 확장 가능한 응용 프로그램을 생성 하는 방법을 매우 단순 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="69016-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="69016-107">해제 쇼핑, 체크 아웃 및 관리를 포함 하는 온라인 상점을 만들려고 ASP.NET 4에서 강력한 새 기능을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="69016-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="69016-108">이 자습서 시리즈 모든 Tailspin Spyworks 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="69016-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="69016-109">7 부 계정 검토, 제품 사용 후기, 및 "인기 있는 항목" 및 "도 구매한" 사용자 정의 컨트롤 등의 추가 기능을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="69016-109">Part 7 adds additional features, such as account review, product reviews, and "popular items" and "also purchased" user controls.</span></span>


## <a id="_Toc260221673"></a>  <span data-ttu-id="69016-110">추가 기능</span><span class="sxs-lookup"><span data-stu-id="69016-110">Adding Features</span></span>

<span data-ttu-id="69016-111">사용자 카탈로그 찾아보기, 장바구니의 항목을 배치할 및 체크 아웃 프로세스를 완료 하지만 가지 다양 한 지원 기능 사이트를 개선 하기 위해 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69016-111">Though users can browse our catalog, place items in their shopping cart, and complete the checkout process, there are a number of supporting features that we will include to improve our site.</span></span>

1. <span data-ttu-id="69016-112">계정 검토 (목록 주문 배치 및 세부 정보를 확인 합니다.)</span><span class="sxs-lookup"><span data-stu-id="69016-112">Account Review (List orders placed and view details.)</span></span>
2. <span data-ttu-id="69016-113">프런트 페이지에 몇 가지 상황에 맞는 특정 콘텐츠를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="69016-113">Add some context specific content to the front page.</span></span>
3. <span data-ttu-id="69016-114">카탈로그에는 기능을 사용자가 검토 제품을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="69016-114">Add a feature to let users Review the products in the catalog.</span></span>
4. <span data-ttu-id="69016-115">프런트 페이지에서 제어 하는 인기 있는 항목 및 위치를 표시 하려면 사용자 컨트롤을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69016-115">Create a User Control to display Popular Items and Place that control on the front page.</span></span>
5. <span data-ttu-id="69016-116">"구입" 사용자 정의 컨트롤을 만들고 제품 정보 페이지에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="69016-116">Create an "Also Purchased" user control and add it to the product details page.</span></span>
6. <span data-ttu-id="69016-117">연락처 추가 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="69016-117">Add a Contact Page.</span></span>
7. <span data-ttu-id="69016-118">추가 페이지에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="69016-118">Add an About Page.</span></span>
8. <span data-ttu-id="69016-119">전역 오류</span><span class="sxs-lookup"><span data-stu-id="69016-119">Global Error</span></span>

## <a id="_Toc260221674"></a>  <span data-ttu-id="69016-120">계정 검토</span><span class="sxs-lookup"><span data-stu-id="69016-120">Account Review</span></span>

<span data-ttu-id="69016-121">"Account" 폴더에 하나의 명명 된 OrderList.aspx와는 다른 명명 된 OrderDetails.aspx 두.aspx 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="69016-121">In the "Account" folder create two .aspx pages one named OrderList.aspx and the other named OrderDetails.aspx</span></span>

<span data-ttu-id="69016-122">이전에 것 만큼 OrderList.aspx는 GridView 및 EntityDataSoure 컨트롤을 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="69016-122">OrderList.aspx will leverage the GridView and EntityDataSoure controls much as we have previously.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample1.aspx)]

<span data-ttu-id="69016-123">EntityDataSoure 사용자 이름을 필터링 하는 Orders 테이블에서 레코드를 선택 합니다 (참조는 WhereParameter) 사용자 로그의 경우 세션 변수에 설정 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="69016-123">The EntityDataSoure selects records from the Orders table filtered on the UserName (see the WhereParameter) which we set in a session variable when the user log's in.</span></span>

<span data-ttu-id="69016-124">GridView의 HyperlinkField에서 이러한 매개 변수를 또한 note:</span><span class="sxs-lookup"><span data-stu-id="69016-124">Note also these parameters in the HyperlinkField of the GridView:</span></span>

[!code-xml[Main](tailspin-spyworks-part-7/samples/sample2.xml)]

<span data-ttu-id="69016-125">이러한 OrderDetails.aspx 페이지에 쿼리 문자열 매개 변수로 OrderID 필드를 지정 하는 각 제품에 대 한 주문 세부 정보 보기에 대 한 링크를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="69016-125">These specify the link to the Order details view for each product specifying the OrderID field as a QueryString parameter to the OrderDetails.aspx page.</span></span>

## <a id="_Toc260221675"></a>  <span data-ttu-id="69016-126">OrderDetails.aspx</span><span class="sxs-lookup"><span data-stu-id="69016-126">OrderDetails.aspx</span></span>

<span data-ttu-id="69016-127">주문을 표시 하는 FormView 주문 데이터 및 GridView 사용 하 여 다른 EntityDataSource 주문의 모든 품목을 표시 하려면 액세스를 EntityDataSource 컨트롤을 사용 하 여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69016-127">We will use an EntityDataSource control to access the Orders and a FormView to display the Order data and another EntityDataSource with a GridView to display all the Order's line items.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample3.aspx)]

<span data-ttu-id="69016-128">코드 숨김 파일 (OrderDetails.aspx.cs)의 두 가지 작은 비트 했습니다.</span><span class="sxs-lookup"><span data-stu-id="69016-128">In the Code Behind file (OrderDetails.aspx.cs) we have two little bits of housekeeping.</span></span>

<span data-ttu-id="69016-129">먼저 OrderDetails에 항상 OrderId 가져옵니다 있는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69016-129">First we need to make sure that OrderDetails always gets an OrderId.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample4.cs)]

<span data-ttu-id="69016-130">또한 계산 되어 총 품목에서 순서를 표시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69016-130">We also need to calculate and display the order total from the line items.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample5.cs)]

## <a id="_Toc260221676"></a>  <span data-ttu-id="69016-131">홈 페이지</span><span class="sxs-lookup"><span data-stu-id="69016-131">The Home Page</span></span>

<span data-ttu-id="69016-132">Default.aspx 페이지에 몇 가지 정적 콘텐츠를 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="69016-132">Let's add some static content to the Default.aspx page.</span></span>

<span data-ttu-id="69016-133">먼저 "콘텐츠" 폴더를 만들겠습니다 및 그 안에 이미지 폴더 (및 홈 페이지에서 사용 될 이미지가 포함 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="69016-133">First I'll create a "Content" folder and within it an Images folder (and I'll include an image to be used on the home page.)</span></span>

<span data-ttu-id="69016-134">Default.aspx 페이지의 아래쪽 자리 표시자에 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="69016-134">Into the bottom placeholder of the Default.aspx page, add the following markup.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample6.aspx)]

## <a id="_Toc260221677"></a>  <span data-ttu-id="69016-135">제품 검토</span><span class="sxs-lookup"><span data-stu-id="69016-135">Product Reviews</span></span>

<span data-ttu-id="69016-136">먼저 링크를 사용 하 여 단추에서는 제품 검토를 입력 하는 데 사용할 수 있는 폼에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="69016-136">First we'll add a button with a link to a form that we can use to enter a product review.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample7.aspx)]

![](tailspin-spyworks-part-7/_static/image1.jpg)

<span data-ttu-id="69016-137">쿼리 문자열에는 ProductID 전달 하는 참고</span><span class="sxs-lookup"><span data-stu-id="69016-137">Note that we are passing the ProductID in the query string</span></span>

<span data-ttu-id="69016-138">다음 ReviewAdd.aspx 라는 페이지를 추가 해 보겠습니다</span><span class="sxs-lookup"><span data-stu-id="69016-138">Next let's add page named ReviewAdd.aspx</span></span>

<span data-ttu-id="69016-139">이 페이지는 ASP.NET AJAX Control Toolkit을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="69016-139">This page will use the ASP.NET AJAX Control Toolkit.</span></span> <span data-ttu-id="69016-140">경우 이미 않았다면에서 다운로드할 수 있도록 [DevExpress](http://devexpress.com/act) 사용 하 여 Visual Studio를 사용 하 여 여기에 대 한 도구 키트 설정 지침 이며 [ https://www.asp.net/learn/ajax-videos/video-76.aspx ](../../../videos/ajax-control-toolkit/how-do-i-get-started-with-the-aspnet-ajax-control-toolkit.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="69016-140">If you have not already done so you can download it from [DevExpress](http://devexpress.com/act) and there is guidance on setting up the toolkit for use with Visual Studio here [https://www.asp.net/learn/ajax-videos/video-76.aspx](../../../videos/ajax-control-toolkit/how-do-i-get-started-with-the-aspnet-ajax-control-toolkit.md).</span></span>

<span data-ttu-id="69016-141">디자인 모드에서 컨트롤 및 유효성 검사기 도구 상자에서 끌어서 아래와 같은 양식을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="69016-141">In design mode, drag controls and validators from the toolbox and build a form like the one below.</span></span>

![](tailspin-spyworks-part-7/_static/image2.jpg)

<span data-ttu-id="69016-142">태그는 다음과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="69016-142">The markup will look something like this.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample8.aspx)]

<span data-ttu-id="69016-143">검토를 입력할 수 있습니다 했으므로 제품 페이지에서 해당 검토를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69016-143">Now that we can enter reviews, lets display those reviews on the product page.</span></span>

<span data-ttu-id="69016-144">ProductDetails.aspx 페이지로이 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="69016-144">Add this markup to the ProductDetails.aspx page.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample9.aspx)]

<span data-ttu-id="69016-145">이제 응용 프로그램을 실행 하 고 제품 탐색 고객 검토를 비롯 한 제품 정보를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="69016-145">Running our application now and navigating to a product shows the product information including customer reviews.</span></span>

![](tailspin-spyworks-part-7/_static/image3.jpg)

## <a id="_Toc260221678"></a>  <span data-ttu-id="69016-146">인기 있는 항목 컨트롤 (사용자 정의 컨트롤 만들기)</span><span class="sxs-lookup"><span data-stu-id="69016-146">Popular Items Control (Creating User Controls)</span></span>

<span data-ttu-id="69016-147">웹 사이트의 판매를 늘리기 위해 몇 가지 기능이 "추천 판매" 많이 사용 되거나 관련 제품에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="69016-147">In order to increase sales on your web site we will add a couple of features to "suggestive sell" popular or related products.</span></span>

<span data-ttu-id="69016-148">이러한 기능 중 첫 번째 제품 카탈로그에 더 인기 있는 제품의 목록이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69016-148">The first of these features will be a list of the more popular product in our product catalog.</span></span>

<span data-ttu-id="69016-149">응용 프로그램의 홈 페이지에서 항목을 판매 맨 위에 표시 하려면 "사용자 컨트롤"을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="69016-149">We will create a "User Control" to display the top selling items on the home page of our application.</span></span> <span data-ttu-id="69016-150">되므로이 컨트롤을 간단히 끌어서 우리는 모든 페이지에 Visual Studio의 디자이너에서 컨트롤을 삭제 하 여 모든 페이지에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69016-150">Since this will be a control, we can use it on any page by simply dragging and dropping the control in Visual Studio's designer onto any page that we like.</span></span>

<span data-ttu-id="69016-151">Visual Studio의 솔루션 탐색기에서 솔루션 이름을 마우스 오른쪽 단추로 클릭 하 고 "컨트롤" 라는 새 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69016-151">In Visual Studio's solutions explorer, right-click on the solution name and create a new directory named "Controls".</span></span> <span data-ttu-id="69016-152">이렇게 하는 데 필요한 상태인 동안 "컨트롤" 디렉터리에는 모든 사용자 정의 컨트롤을 만들어서 구성 하는 프로젝트를 유지할 수 것입니다.</span><span class="sxs-lookup"><span data-stu-id="69016-152">While it is not necessary to do so, we will help keep our project organized by creating all our user controls in the "Controls" directory.</span></span>

<span data-ttu-id="69016-153">Controls 폴더 단추로 클릭 하 고 "새 항목"을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="69016-153">Right-click on the controls folder and choose "New Item" :</span></span>

![](tailspin-spyworks-part-7/_static/image4.jpg)

<span data-ttu-id="69016-154">"PopularItems"의 컨트롤에 대 한 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="69016-154">Specify a name for our control of "PopularItems".</span></span> <span data-ttu-id="69016-155">사용자 컨트롤에 대 한 파일 확장명은.ascx.aspx 하지는 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="69016-155">Note that the file extension for user controls is .ascx not .aspx.</span></span>

<span data-ttu-id="69016-156">인기 항목 사용자 제어권을 다음과 같이 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69016-156">Our Popular Items User control will be defined as follows.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample10.aspx)]

<span data-ttu-id="69016-157">여기에서는 아직이 응용 프로그램에 사용 하지 않은 메서드를 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="69016-157">Here we're using a method we have not used yet in this application.</span></span> <span data-ttu-id="69016-158">Repeater 컨트롤을 사용 하는 것을 데이터 소스 컨트롤을 사용 하는 대신는 linq to Entities 쿼리 결과에 Repeater 컨트롤을 바인딩하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="69016-158">We're using the repeater control and instead of using a data source control we're binding the Repeater Control to the results of a LINQ to Entities query.</span></span>

<span data-ttu-id="69016-159">이 컨트롤의 코드 숨김에 수행 하는 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="69016-159">In the code behind of our control we do that as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample11.cs)]

<span data-ttu-id="69016-160">Note는 컨트롤의 태그의 맨 위에 있는 중요 한 줄도 합니다.</span><span class="sxs-lookup"><span data-stu-id="69016-160">Note also this important line at the top of our control's markup.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample12.aspx)]

<span data-ttu-id="69016-161">분당 기준 가장 인기 있는 항목을 변경 하지 않으므로 하므로 응용 프로그램의 성능을 향상 시키기 위해 고통의 지시문을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69016-161">Since the most popular items won't be changing on a minute to minute basis we can add a aching directive to improve the performance of our application.</span></span> <span data-ttu-id="69016-162">이 지시어를 사용 하면 컨트롤의 출력 캐시를 만료 될 때만 실행 될 컨트롤 코드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69016-162">This directive will cause the controls code to only be executed when the cached output of the control expires.</span></span> <span data-ttu-id="69016-163">그렇지 않은 경우 컨트롤의 출력 캐시 된 버전이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69016-163">Otherwise, the cached version of the control's output will be used.</span></span>

<span data-ttu-id="69016-164">작업을 수행 해야 모든는 이제 Default.aspc 페이지에는 새 컨트롤을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="69016-164">Now all we have to do is include our new control in our Default.aspc page.</span></span>

<span data-ttu-id="69016-165">사용 하 여 끌어서 열기 열의 기본 폼에 컨트롤의 인스턴스를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="69016-165">Use drag and drop to place an instance of the control in the open column of our Default form.</span></span>

![](tailspin-spyworks-part-7/_static/image5.jpg)

<span data-ttu-id="69016-166">이제 응용 프로그램을 실행할 때 홈 페이지에 가장 인기 있는 항목이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69016-166">Now when we run our application the home page displays the most popular items.</span></span>

![](tailspin-spyworks-part-7/_static/image6.jpg)

## <a id="_Toc260221679"></a>  <span data-ttu-id="69016-167">(매개 변수를 사용 하 여 사용자 정의 컨트롤) 제어 "구입"</span><span class="sxs-lookup"><span data-stu-id="69016-167">"Also Purchased" Control (User Controls with Parameters)</span></span>

<span data-ttu-id="69016-168">두 번째 사용자 컨트롤을 만들어 다음 수준에 판매 하는 상황에 맞는 구체적인 정도 추가 하 여 추천 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="69016-168">The second User Control that we'll create will take suggestive selling to the next level by adding context specificity.</span></span>

<span data-ttu-id="69016-169">상위 "구입" 항목을 계산 하는 논리는 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="69016-169">The logic to calculate the top "Also Purchased" items is non-trivial.</span></span>

<span data-ttu-id="69016-170">"구입" 제어권 현재 선택 된 ProductID에 대 한 (이전에 구매한 경우) OrderDetails 레코드를 선택한 있는 고유한 각 주문의 Orderid를 잡고 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69016-170">Our "Also Purchased" control will select the OrderDetails records (previously purchased) for the currently selected ProductID and grab the OrderIDs for each unique order that is found.</span></span>

<span data-ttu-id="69016-171">그런 다음 선택 al 제품에서 이러한 모든 Orders와 구매 수량 합계입니다.</span><span class="sxs-lookup"><span data-stu-id="69016-171">Then we will select al the products from all those Orders and sum the quantities purchased.</span></span> <span data-ttu-id="69016-172">제품 수량 합계 하 여 정렬 하 고 상위 5 개 항목 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69016-172">We'll sort the products by that quantity sum and display the top five items.</span></span>

<span data-ttu-id="69016-173">이 논리의 복잡성을 지정 했습니다 저장 프로시저로이 알고리즘을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="69016-173">Given the complexity of this logic, we will implement this algorithm as a stored procedure.</span></span>

<span data-ttu-id="69016-174">저장된 프로시저에 대 한 T-SQL은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="69016-174">The T-SQL for the stored procedure is as follows.</span></span>

[!code-sql[Main](tailspin-spyworks-part-7/samples/sample13.sql)]

<span data-ttu-id="69016-175">테이블 및 엔터티 데이터 모델에서는 필요한 뷰 외에 지정한 엔터티 데이터 모델을 생성할 때 및 응용 프로그램에에서는 포함 하는 경우이 저장된 프로시저 (SelectPurchasedWithProducts) 데이터베이스에 있었음을 note합니다 이 저장된 프로시저를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69016-175">Note that this stored procedure (SelectPurchasedWithProducts) existed in the database when we included it in our application and when we generated the Entity Data Model we specified that, in addition to the Tables and Views that we needed, the Entity Data Model should include this stored procedure.</span></span>

<span data-ttu-id="69016-176">엔터티 데이터 모델에서 저장된 프로시저에 액세스 하는 함수 가져오기 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69016-176">To access the stored procedure from the Entity Data Model we need to import the function.</span></span>

<span data-ttu-id="69016-177">엔터티 데이터 모델 디자이너에서 열고 Model 브라우저를 열고 솔루션 탐색기에서 두 번 클릭 한 다음 디자이너에서 마우스 오른쪽 단추로 클릭 하 고 "Function Import 추가"를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="69016-177">Double Click on the Entity Data Model in the Solutions Explorer to open it in the designer and open the Model Browser, then right-click in the designer and select "Add Function Import".</span></span>

![](tailspin-spyworks-part-7/_static/image1.png)

<span data-ttu-id="69016-178">그러면이 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="69016-178">Doing so will open this dialog.</span></span>

![](tailspin-spyworks-part-7/_static/image2.png)

<span data-ttu-id="69016-179">"SelectPurchasedWithProducts"를 선택 하면 위에 표시 된 대로 필드 입력 하 고이 가져온 함수의 이름에 대 한 프로시저 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="69016-179">Fill out the fields as you see above, selecting the "SelectPurchasedWithProducts" and use the procedure name for the name of our imported function.</span></span>

<span data-ttu-id="69016-180">"확인"을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="69016-180">Click "Ok".</span></span>

<span data-ttu-id="69016-181">에서는 모델의 다른 항목 수 것으로 간단히 저장된 프로시저에 대해 프로그래밍할 수이 위해서입니다.</span><span class="sxs-lookup"><span data-stu-id="69016-181">Having done this we can simply program against the stored procedure as we might any other item in the model.</span></span>

<span data-ttu-id="69016-182">따라서이 "컨트롤" 폴더에 AlsoPurchased.ascx 라는 새 사용자 컨트롤을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69016-182">So, in our "Controls" folder create a new user control named AlsoPurchased.ascx.</span></span>

<span data-ttu-id="69016-183">이 컨트롤에 대 한 태그 PopularItems 컨트롤에 매우 익숙할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="69016-183">The markup for this control will look very familiar to the PopularItems control.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample14.aspx)]

<span data-ttu-id="69016-184">주목할 만한 차이점은 캐싱하지 않으면 출력 항목의 렌더링 되어야 하는 제품에서 달라 집니다 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="69016-184">The notable difference is that are not caching the output since the item's to be rendered will differ by product.</span></span>

<span data-ttu-id="69016-185">ProductId는 컨트롤에 "property" 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69016-185">The ProductId will be a "property" to the control.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample15.cs)]

<span data-ttu-id="69016-186">컨트롤의 PreRender 이벤트 처리기에서에서는 eed 다음 세 가지 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="69016-186">In the control's PreRender event handler we eed to do three things.</span></span>

1. <span data-ttu-id="69016-187">ProductID 설정 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="69016-187">Make sure the ProductID is set.</span></span>
2. <span data-ttu-id="69016-188">현재는 구매한 모든 제품 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="69016-188">See if there are any products that have been purchased with the current one.</span></span>
3. <span data-ttu-id="69016-189">2 단계에서에서 결정 된 대로 일부 항목을 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="69016-189">Output some items as determined in #2.</span></span>

<span data-ttu-id="69016-190">모델을 통해 저장된 프로시저를 호출 하려면 얼마나 쉬운지 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="69016-190">Note how easy it is to call the stored procedure through the model.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample16.cs)]

<span data-ttu-id="69016-191">없습니다 "도 구매"를 확인 한 후 쿼리에서 반환 된 결과에 반복기를 바인딩할 단순히 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69016-191">After determining that there ARE "also purchased" we can simply bind the repeater to the results returned by the query.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample17.cs)]

<span data-ttu-id="69016-192">"구입" 항목이 없는 경우 카탈로그에서 다른 인기 있는 항목만 단순히 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69016-192">If there were not any "also purchased" items we'll simply display other popular items from our catalog.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample18.cs)]

<span data-ttu-id="69016-193">"구입" 항목을 보려면 ProductDetails.aspx 페이지를 열려면 끌어서 AlsoPurchased 컨트롤 솔루션 탐색기에서 태그의이 위치에 표시 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="69016-193">To view the "Also Purchased" items, open the ProductDetails.aspx page and drag the AlsoPurchased control from the Solutions Explorer so that it appears in this position in the markup.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample19.aspx)]

<span data-ttu-id="69016-194">이렇게 세부 내용 페이지의 맨 위에 있는 컨트롤에 대 한 참조가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="69016-194">Doing so will create a reference to the control at the top of the ProductDetails page.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample20.aspx)]

<span data-ttu-id="69016-195">AlsoPurchased 사용자 정의 컨트롤에는 ProductId 숫자로 필요 하므로 페이지의 현재 데이터 모델 항목에 대해 Eval 문과 사용 하 여이 컨트롤의 ProductID 속성을 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69016-195">Since the AlsoPurchased user control requires a ProductId number we will set the ProductID property of our control by using an Eval statement against the current data model item of the page.</span></span>

![](tailspin-spyworks-part-7/_static/image3.png)

<span data-ttu-id="69016-196">빌드 및 지금 실행 하 고 제품으로 이동 "구입" 항목을 볼 했습니다.</span><span class="sxs-lookup"><span data-stu-id="69016-196">When we build and run now and browse to a product we see the "Also Purchased" items.</span></span>

![](tailspin-spyworks-part-7/_static/image7.jpg)

> [!div class="step-by-step"]
> <span data-ttu-id="69016-197">[이전](tailspin-spyworks-part-6.md)
> [다음](tailspin-spyworks-part-8.md)</span><span class="sxs-lookup"><span data-stu-id="69016-197">[Previous](tailspin-spyworks-part-6.md)
[Next](tailspin-spyworks-part-8.md)</span></span>
