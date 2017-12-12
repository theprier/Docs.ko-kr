---
uid: mvc/overview/getting-started/introduction/examining-the-details-and-delete-methods
title: "세부 정보 및 삭제 메서드 검사 | Microsoft Docs"
author: Rick-Anderson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/26/2015
ms.topic: article
ms.assetid: f1d2a916-626c-4a54-8df4-77e6b9fff355
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/introduction/examining-the-details-and-delete-methods
msc.type: authoredcontent
ms.openlocfilehash: 6d7d0fe5bd2f6a6bd7f9c7ca04a8f142223ccf8e
ms.sourcegitcommit: d1d8071d4093bf2444b5ae19d6e45c3d187e338b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/19/2017
---
<a name="examining-the-details-and-delete-methods"></a><span data-ttu-id="1a4ab-102">세부 정보 및 삭제 메서드를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="1a4ab-102">Examining the Details and Delete Methods</span></span>
====================
<span data-ttu-id="1a4ab-103">으로 [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="1a4ab-103">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

[!INCLUDE[Tutorial Note](sample/code-location.md)]

<span data-ttu-id="1a4ab-104">자습서의이 부분에서는 검토해 자동으로 생성 된 `Details` 및 `Delete` 메서드.</span><span class="sxs-lookup"><span data-stu-id="1a4ab-104">In this part of the tutorial, you'll examine the automatically generated `Details` and `Delete` methods.</span></span>

## <a name="examining-the-details-and-delete-methods"></a><span data-ttu-id="1a4ab-105">세부 정보 및 삭제 메서드를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="1a4ab-105">Examining the Details and Delete Methods</span></span>

<span data-ttu-id="1a4ab-106">열기는 `Movie` 컨트롤러 검사는 `Details` 메서드.</span><span class="sxs-lookup"><span data-stu-id="1a4ab-106">Open the `Movie` controller and examine the `Details` method.</span></span>

![](examining-the-details-and-delete-methods/_static/image1.png)

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample1.cs)]

<span data-ttu-id="1a4ab-107">이 작업 메서드를 만든 MVC 스 캐 폴딩 엔진 메서드를 호출 하는 HTTP 요청을 보여 주는 메모를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a4ab-107">The MVC scaffolding engine that created this action method adds a comment showing a HTTP request that invokes the method.</span></span> <span data-ttu-id="1a4ab-108">이 경우에 `GET` URL 세그먼트를 사용 하 여 요청은 `Movies` 컨트롤러는 `Details` 메서드 및 `ID` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1a4ab-108">In this case it's a `GET` request with three URL segments, the `Movies` controller, the `Details` method and a `ID` value.</span></span>

<span data-ttu-id="1a4ab-109">코드 먼저 쉽게 사용 하 여 데이터를 검색 하는 `Find` 메서드.</span><span class="sxs-lookup"><span data-stu-id="1a4ab-109">Code First makes it easy to search for data using the `Find` method.</span></span> <span data-ttu-id="1a4ab-110">메서드에 구성 하는 중요 한 보안 기능 코드 확인 되는 `Find` 메서드 코드와 어떤 작업을 시도 하기 전에 동영상을 발견 했습니다.</span><span class="sxs-lookup"><span data-stu-id="1a4ab-110">An important security feature built into the method is that the code verifies that the `Find` method has found a movie before the code tries to do anything with it.</span></span> <span data-ttu-id="1a4ab-111">예를 들어 해커가 오류가 발생할 수를 사이트에 링크를에서 만든 URL을 변경 하 여 `http://localhost:xxxx/Movies/Details/1` 같이 `http://localhost:xxxx/Movies/Details/12345` (또는 실제 영화 표시 되지 않은 다른 값).</span><span class="sxs-lookup"><span data-stu-id="1a4ab-111">For example, a hacker could introduce errors into the site by changing the URL created by the links from `http://localhost:xxxx/Movies/Details/1` to something like `http://localhost:xxxx/Movies/Details/12345` (or some other value that doesn't represent an actual movie).</span></span> <span data-ttu-id="1a4ab-112">Null 동영상에 대 한 선택 하지 않은 경우 null 영화, 데이터베이스 오류가 생깁니다.</span><span class="sxs-lookup"><span data-stu-id="1a4ab-112">If you did not check for a null movie, a null movie would result in a database error.</span></span>

<span data-ttu-id="1a4ab-113">`Delete` 및 `DeleteConfirmed` 메서드를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="1a4ab-113">Examine the `Delete` and `DeleteConfirmed` methods.</span></span>

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample2.cs?highlight=17)]

<span data-ttu-id="1a4ab-114">`HTTP Get``Delete` 메서드는 지정 된 영화를 삭제 하지 않습니다, 동영상의 보기 반환 제출할 수 있습니다 (`HttpPost`) 삭제...</span><span class="sxs-lookup"><span data-stu-id="1a4ab-114">Note that the `HTTP Get``Delete` method doesn't delete the specified movie, it returns a view of the movie where you can submit (`HttpPost`) the deletion..</span></span> <span data-ttu-id="1a4ab-115">GET 요청에 대한 응답에서 삭제 작업 수행(또는 해당 문제를 위해 편집 작업 수행, 작업 만들기 또는 데이터를 변경하는 기타 작업)은 보안 허점을 야기합니다.</span><span class="sxs-lookup"><span data-stu-id="1a4ab-115">Performing a delete operation in response to a GET request (or for that matter, performing an edit operation, create operation, or any other operation that changes data) opens up a security hole.</span></span> <span data-ttu-id="1a4ab-116">이 대 한 자세한 내용은 Stephen Walther 블로그 항목을 참조 하십시오. [ASP.NET MVC 팁 #46-보안 허점을 만들기 때문에 삭제 링크를 사용 하지 않는](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="1a4ab-116">For more information about this, see Stephen Walther's blog entry [ASP.NET MVC Tip #46 — Don't use Delete Links because they create Security Holes](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx).</span></span>

<span data-ttu-id="1a4ab-117">데이터를 삭제하는 `HttpPost` 메서드는 HTTP POST 메서드에 고유한 서명 또는 이름을 제공하기 위해 `DeleteConfirmed`로 이름이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a4ab-117">The `HttpPost` method that deletes the data is named `DeleteConfirmed` to give the HTTP POST method a unique signature or name.</span></span> <span data-ttu-id="1a4ab-118">두 개의 메서드 서명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1a4ab-118">The two method signatures are shown below:</span></span>

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample3.cs)]

<span data-ttu-id="1a4ab-119">CLR(공용 언어 런타임)은 고유한 매개 변수 서명을 갖기 위해 오버로드된 메서드가 필요합니다(동일한 메서드 이름이지만 다른 매개 변수의 목록).</span><span class="sxs-lookup"><span data-stu-id="1a4ab-119">The common language runtime (CLR) requires overloaded methods to have a unique parameter signature (same method name but different list of parameters).</span></span> <span data-ttu-id="1a4ab-120">그러나 여기 해야 두 삭제 메서드-각각에 대 한 GET-와 게시에 매개 변수 시그니처를 포함 하는 두 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a4ab-120">However, here you need two Delete methods -- one for GET and one for POST -- that both have the same parameter signature.</span></span> <span data-ttu-id="1a4ab-121">(모두 매개 변수로 단일 정수를 허용해야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="1a4ab-121">(They both need to accept a single integer as a parameter.)</span></span>

<span data-ttu-id="1a4ab-122">이 출력을 정렬 하려면 몇 가지 기능을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a4ab-122">To sort this out, you can do a couple of things.</span></span> <span data-ttu-id="1a4ab-123">하나는 메서드를 서로 다른 이름을 지정입니다.</span><span class="sxs-lookup"><span data-stu-id="1a4ab-123">One is to give the methods different names.</span></span> <span data-ttu-id="1a4ab-124">앞의 예에서 스캐폴딩 메커니즘이 수행한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1a4ab-124">That's what the scaffolding mechanism did in the preceding example.</span></span> <span data-ttu-id="1a4ab-125">그러나 이는 작은 문제를 가져옵니다. ASP.NET은 URL의 세그먼트를 이름으로 작업 메서드에 매핑하고 메서드의 이름을 바꾸면 정상적으로 라우팅하여 해당 메서드를 찾을 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a4ab-125">However, this introduces a small problem: ASP.NET maps segments of a URL to action methods by name, and if you rename a method, routing normally wouldn't be able to find that method.</span></span> <span data-ttu-id="1a4ab-126">솔루션은 예제에서 확인한 것으로, `ActionName("Delete")` 특성을 `DeleteConfirmed` 메서드에 추가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1a4ab-126">The solution is what you see in the example, which is to add the `ActionName("Delete")` attribute to the `DeleteConfirmed` method.</span></span> <span data-ttu-id="1a4ab-127">포함 하는 URL 라우팅 시스템에 대 한 매핑을 효과적으로 수행 */Delete/* 게시물에 대 한 요청 찾을 수는 `DeleteConfirmed` 메서드.</span><span class="sxs-lookup"><span data-stu-id="1a4ab-127">This effectively performs mapping for the routing system so that a URL that includes */Delete/* for a POST request will find the `DeleteConfirmed` method.</span></span>

<span data-ttu-id="1a4ab-128">동일한 이름 및 시그니처가 있는 메서드에서 문제를 방지 하는 다른 일반적인 방법은 인위적으로 사용 되지 않는 매개 변수를 포함 하도록 POST 메서드의 시그니처를 변경 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1a4ab-128">Another common way to avoid a problem with methods that have identical names and signatures is to artificially change the signature of the POST method to include an unused parameter.</span></span> <span data-ttu-id="1a4ab-129">예를 들어, 일부 개발자가 추가 매개 변수 형식 `FormCollection` POST 메서드에 전달 되는 다음 단순히 하지 않는 매개 변수를 사용 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a4ab-129">For example, some developers add a parameter type `FormCollection` that is passed to the POST method, and then simply don't use the parameter:</span></span>

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample4.cs)]

## <a name="summary"></a><span data-ttu-id="1a4ab-130">요약</span><span class="sxs-lookup"><span data-stu-id="1a4ab-130">Summary</span></span>

<span data-ttu-id="1a4ab-131">이제 로컬 DB 데이터베이스에 데이터를 저장 하는 전체 ASP.NET MVC 응용 프로그램을 준비 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1a4ab-131">You now have a complete ASP.NET MVC application that stores data in a local DB database.</span></span> <span data-ttu-id="1a4ab-132">있습니다 수 만들기, 읽기, 업데이트, 삭제 및 영화를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a4ab-132">You can create, read, update, delete, and search for movies.</span></span>

![](examining-the-details-and-delete-methods/_static/image2.png)

## <a name="next-steps"></a><span data-ttu-id="1a4ab-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1a4ab-133">Next Steps</span></span>

<span data-ttu-id="1a4ab-134">작성 하 고 웹 응용 프로그램을 테스트 후 다른 사람이 인터넷을 통해 사용 하도록 사용할 수 있도록 하려면 다음 단계가입니다.</span><span class="sxs-lookup"><span data-stu-id="1a4ab-134">After you have built and tested a web application, the next step is to make it available to other people to use over the Internet.</span></span> <span data-ttu-id="1a4ab-135">이렇게 하려면 웹 호스팅 공급자를 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a4ab-135">To do that, you have to deploy it to a web hosting provider.</span></span> <span data-ttu-id="1a4ab-136">Microsoft에서 제공 하는 최대 10 개의 웹 사이트의 무료 웹 호스팅는 [무료 Azure 평가판 계정](https://www.windowsazure.com/en-us/pricing/free-trial/?WT.mc_id=A443DD604)합니다.</span><span class="sxs-lookup"><span data-stu-id="1a4ab-136">Microsoft offers free web hosting for up to 10 web sites in a [free Azure trial account](https://www.windowsazure.com/en-us/pricing/free-trial/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="1a4ab-137">다음 내 자습서를 따라 보시기 [멤버 자격, OAuth, SQL 데이터베이스와 Secure ASP.NET MVC 응용 프로그램을 Azure에 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)합니다.</span><span class="sxs-lookup"><span data-stu-id="1a4ab-137">I suggest you next follow my tutorial [Deploy a Secure ASP.NET MVC app with Membership, OAuth, and SQL Database to Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="1a4ab-138">뛰어난 자습서가 Tom Dykstra 중간 수준 [ASP.NET MVC 응용 프로그램에 대 한 Entity Framework 데이터 모델을 만드는](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1a4ab-138">An excellent tutorial is Tom Dykstra's intermediate-level [Creating an Entity Framework Data Model for an ASP.NET MVC Application](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="1a4ab-139">[Stackoverflow](http://stackoverflow.com/help) 및 [ASP.NET MVC 포럼](https://forums.asp.net/1146.aspx) 질문을 하는 좋은 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a4ab-139">[Stackoverflow](http://stackoverflow.com/help) and the [ASP.NET MVC forums](https://forums.asp.net/1146.aspx) are a great places to ask questions.</span></span> <span data-ttu-id="1a4ab-140">에 따라 [me](https://twitter.com/RickAndMSFT) 에서 twitter 때문 내 최신 자습서에 대 한 업데이트를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a4ab-140">Follow [me](https://twitter.com/RickAndMSFT) on twitter so you can get updates on my latest tutorials.</span></span>

<span data-ttu-id="1a4ab-141">피드백을 보내 주십시오.</span><span class="sxs-lookup"><span data-stu-id="1a4ab-141">Feedback is welcome.</span></span>

<span data-ttu-id="1a4ab-142">- [Rick Anderson](https://blogs.msdn.com/rickAndy) twitter:[@RickAndMSFT](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="1a4ab-142">— [Rick Anderson](https://blogs.msdn.com/rickAndy) twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT)</span></span>  
<span data-ttu-id="1a4ab-143">- [Scott Hanselman](http://www.hanselman.com/blog/) twitter:[@shanselman](https://twitter.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="1a4ab-143">— [Scott Hanselman](http://www.hanselman.com/blog/) twitter: [@shanselman](https://twitter.com/shanselman)</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="1a4ab-144">이전</span><span class="sxs-lookup"><span data-stu-id="1a4ab-144">Previous</span></span>](adding-validation.md)
