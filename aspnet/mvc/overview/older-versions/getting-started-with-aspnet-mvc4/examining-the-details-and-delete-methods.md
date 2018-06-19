---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-details-and-delete-methods
title: 세부 정보 및 삭제 메서드 검사 | Microsoft Docs
author: Rick-Anderson
description: 참고:이 자습서의 업데이트 된 버전은 ASP.NET MVC 5 및 Visual Studio 2013을 사용 하는 있습니다. 것이 더 안전 하 고 진행할 데모를 단순...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/28/2012
ms.topic: article
ms.assetid: 11425ff3-09fc-4efa-be9a-b53bce503460
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-details-and-delete-methods
msc.type: authoredcontent
ms.openlocfilehash: 00f7e5d6679f1bd8875931e601c8151049f785ac
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30868778"
---
<a name="examining-the-details-and-delete-methods"></a><span data-ttu-id="efbae-104">세부 정보 및 삭제 메서드를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="efbae-104">Examining the Details and Delete Methods</span></span>
====================
<span data-ttu-id="efbae-105">으로 [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="efbae-105">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> > [!NOTE]
> > <span data-ttu-id="efbae-106">이 자습서의 업데이트 된 버전은 사용할 수 있는 [여기](../../getting-started/introduction/getting-started.md) ASP.NET MVC 5 및 Visual Studio 2013을 사용 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="efbae-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="efbae-107">더 안전 하 고 따라 하기 쉽고 이며 더 많은 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="efbae-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>


<span data-ttu-id="efbae-108">자습서의이 부분에서는 검토해 자동으로 생성 된 `Details` 및 `Delete` 메서드.</span><span class="sxs-lookup"><span data-stu-id="efbae-108">In this part of the tutorial, you'll examine the automatically generated `Details` and `Delete` methods.</span></span>

## <a name="examining-the-details-and-delete-methods"></a><span data-ttu-id="efbae-109">세부 정보 및 삭제 메서드를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="efbae-109">Examining the Details and Delete Methods</span></span>

<span data-ttu-id="efbae-110">열기는 `Movie` 컨트롤러 검사는 `Details` 메서드.</span><span class="sxs-lookup"><span data-stu-id="efbae-110">Open the `Movie` controller and examine the `Details` method.</span></span>

![](examining-the-details-and-delete-methods/_static/image1.png)

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample1.cs)]

<span data-ttu-id="efbae-111">이 작업 메서드를 만든 MVC 스 캐 폴딩 엔진 메서드를 호출 하는 HTTP 요청을 보여 주는 메모를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="efbae-111">The MVC scaffolding engine that created this action method adds a comment showing a HTTP request that invokes the method.</span></span> <span data-ttu-id="efbae-112">이 경우에 `GET` URL 세그먼트를 사용 하 여 요청은 `Movies` 컨트롤러는 `Details` 메서드 및 `ID` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="efbae-112">In this case it's a `GET` request with three URL segments, the `Movies` controller, the `Details` method and a `ID` value.</span></span>

<span data-ttu-id="efbae-113">코드 먼저 쉽게 사용 하 여 데이터를 검색 하는 `Find` 메서드.</span><span class="sxs-lookup"><span data-stu-id="efbae-113">Code First makes it easy to search for data using the `Find` method.</span></span> <span data-ttu-id="efbae-114">메서드에 구성 하는 중요 한 보안 기능 코드 확인 되는 `Find` 메서드 코드와 어떤 작업을 시도 하기 전에 동영상을 발견 했습니다.</span><span class="sxs-lookup"><span data-stu-id="efbae-114">An important security feature built into the method is that the code verifies that the `Find` method has found a movie before the code tries to do anything with it.</span></span> <span data-ttu-id="efbae-115">예를 들어 해커가 오류가 발생할 수를 사이트에 링크를에서 만든 URL을 변경 하 여 `http://localhost:xxxx/Movies/Details/1` 같이 `http://localhost:xxxx/Movies/Details/12345` (또는 실제 영화 표시 되지 않은 다른 값).</span><span class="sxs-lookup"><span data-stu-id="efbae-115">For example, a hacker could introduce errors into the site by changing the URL created by the links from `http://localhost:xxxx/Movies/Details/1` to something like `http://localhost:xxxx/Movies/Details/12345` (or some other value that doesn't represent an actual movie).</span></span> <span data-ttu-id="efbae-116">Null 동영상에 대 한 선택 하지 않은 경우 null 영화, 데이터베이스 오류가 생깁니다.</span><span class="sxs-lookup"><span data-stu-id="efbae-116">If you did not check for a null movie, a null movie would result in a database error.</span></span>

<span data-ttu-id="efbae-117">`Delete` 및 `DeleteConfirmed` 메서드를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="efbae-117">Examine the `Delete` and `DeleteConfirmed` methods.</span></span>

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample2.cs?highlight=17)]

<span data-ttu-id="efbae-118">`HTTP Get``Delete` 메서드는 지정 된 영화를 삭제 하지 않습니다, 동영상의 보기 반환 제출할 수 있습니다 (`HttpPost`) 삭제...</span><span class="sxs-lookup"><span data-stu-id="efbae-118">Note that the `HTTP Get``Delete` method doesn't delete the specified movie, it returns a view of the movie where you can submit (`HttpPost`) the deletion..</span></span> <span data-ttu-id="efbae-119">GET 요청에 대한 응답에서 삭제 작업 수행(또는 해당 문제를 위해 편집 작업 수행, 작업 만들기 또는 데이터를 변경하는 기타 작업)은 보안 허점을 야기합니다.</span><span class="sxs-lookup"><span data-stu-id="efbae-119">Performing a delete operation in response to a GET request (or for that matter, performing an edit operation, create operation, or any other operation that changes data) opens up a security hole.</span></span> <span data-ttu-id="efbae-120">이 대 한 자세한 내용은 Stephen Walther 블로그 항목을 참조 하십시오. [ASP.NET MVC 팁 #46-보안 허점을 만들기 때문에 삭제 링크를 사용 하지 않는](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="efbae-120">For more information about this, see Stephen Walther's blog entry [ASP.NET MVC Tip #46 — Don't use Delete Links because they create Security Holes](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx).</span></span>

<span data-ttu-id="efbae-121">데이터를 삭제하는 `HttpPost` 메서드는 HTTP POST 메서드에 고유한 서명 또는 이름을 제공하기 위해 `DeleteConfirmed`로 이름이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="efbae-121">The `HttpPost` method that deletes the data is named `DeleteConfirmed` to give the HTTP POST method a unique signature or name.</span></span> <span data-ttu-id="efbae-122">두 개의 메서드 서명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="efbae-122">The two method signatures are shown below:</span></span>

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample3.cs)]

<span data-ttu-id="efbae-123">CLR(공용 언어 런타임)은 고유한 매개 변수 서명을 갖기 위해 오버로드된 메서드가 필요합니다(동일한 메서드 이름이지만 다른 매개 변수의 목록).</span><span class="sxs-lookup"><span data-stu-id="efbae-123">The common language runtime (CLR) requires overloaded methods to have a unique parameter signature (same method name but different list of parameters).</span></span> <span data-ttu-id="efbae-124">그러나 여기 해야 두 삭제 메서드-각각에 대 한 GET-와 게시에 매개 변수 시그니처를 포함 하는 두 합니다.</span><span class="sxs-lookup"><span data-stu-id="efbae-124">However, here you need two Delete methods -- one for GET and one for POST -- that both have the same parameter signature.</span></span> <span data-ttu-id="efbae-125">(모두 매개 변수로 단일 정수를 허용해야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="efbae-125">(They both need to accept a single integer as a parameter.)</span></span>

<span data-ttu-id="efbae-126">이 출력을 정렬 하려면 몇 가지 기능을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efbae-126">To sort this out, you can do a couple of things.</span></span> <span data-ttu-id="efbae-127">하나는 메서드를 서로 다른 이름을 지정입니다.</span><span class="sxs-lookup"><span data-stu-id="efbae-127">One is to give the methods different names.</span></span> <span data-ttu-id="efbae-128">앞의 예에서 스캐폴딩 메커니즘이 수행한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="efbae-128">That's what the scaffolding mechanism did in the preceding example.</span></span> <span data-ttu-id="efbae-129">그러나 이는 작은 문제를 가져옵니다. ASP.NET은 URL의 세그먼트를 이름으로 작업 메서드에 매핑하고 메서드의 이름을 바꾸면 정상적으로 라우팅하여 해당 메서드를 찾을 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="efbae-129">However, this introduces a small problem: ASP.NET maps segments of a URL to action methods by name, and if you rename a method, routing normally wouldn't be able to find that method.</span></span> <span data-ttu-id="efbae-130">솔루션은 예제에서 확인한 것으로, `ActionName("Delete")` 특성을 `DeleteConfirmed` 메서드에 추가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="efbae-130">The solution is what you see in the example, which is to add the `ActionName("Delete")` attribute to the `DeleteConfirmed` method.</span></span> <span data-ttu-id="efbae-131">포함 하는 URL 라우팅 시스템에 대 한 매핑을 효과적으로 수행 <em>/Delete/</em>게시물에 대 한 요청 찾을 수는 `DeleteConfirmed` 메서드.</span><span class="sxs-lookup"><span data-stu-id="efbae-131">This effectively performs mapping for the routing system so that a URL that includes <em>/Delete/</em>for a POST request will find the `DeleteConfirmed` method.</span></span>

<span data-ttu-id="efbae-132">동일한 이름 및 시그니처가 있는 메서드에서 문제를 방지 하는 다른 일반적인 방법은 인위적으로 사용 되지 않는 매개 변수를 포함 하도록 POST 메서드의 시그니처를 변경 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="efbae-132">Another common way to avoid a problem with methods that have identical names and signatures is to artificially change the signature of the POST method to include an unused parameter.</span></span> <span data-ttu-id="efbae-133">예를 들어, 일부 개발자가 추가 매개 변수 형식 `FormCollection` POST 메서드에 전달 되는 다음 단순히 하지 않는 매개 변수를 사용 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efbae-133">For example, some developers add a parameter type `FormCollection` that is passed to the POST method, and then simply don't use the parameter:</span></span>

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample4.cs)]

## <a name="summary"></a><span data-ttu-id="efbae-134">요약</span><span class="sxs-lookup"><span data-stu-id="efbae-134">Summary</span></span>

<span data-ttu-id="efbae-135">이제 로컬 DB 데이터베이스에 데이터를 저장 하는 전체 ASP.NET MVC 응용 프로그램을 준비 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="efbae-135">You now have a complete ASP.NET MVC application that stores data in a local DB database.</span></span> <span data-ttu-id="efbae-136">있습니다 수 만들기, 읽기, 업데이트, 삭제 및 영화를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="efbae-136">You can create, read, update, delete, and search for movies.</span></span>

![](examining-the-details-and-delete-methods/_static/image2.png)

## <a name="next-steps"></a><span data-ttu-id="efbae-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="efbae-137">Next Steps</span></span>

<span data-ttu-id="efbae-138">작성 하 고 웹 응용 프로그램을 테스트 후 다른 사람이 인터넷을 통해 사용 하도록 사용할 수 있도록 하려면 다음 단계가입니다.</span><span class="sxs-lookup"><span data-stu-id="efbae-138">After you have built and tested a web application, the next step is to make it available to other people to use over the Internet.</span></span> <span data-ttu-id="efbae-139">이렇게 하려면 웹 호스팅 공급자를 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="efbae-139">To do that, you have to deploy it to a web hosting provider.</span></span> <span data-ttu-id="efbae-140">Microsoft에서 제공 하는 최대 10 개의 웹 사이트의 무료 웹 호스팅는 [Windows Azure 평가판 계정 무료](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604)합니다.</span><span class="sxs-lookup"><span data-stu-id="efbae-140">Microsoft offers free web hosting for up to 10 web sites in a [free Windows Azure trial account](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="efbae-141">다음 내 자습서를 따라 보시기 [Windows Azure 웹 사이트 멤버 자격, OAuth, SQL 데이터베이스와 Secure ASP.NET MVC 응용 프로그램 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)합니다.</span><span class="sxs-lookup"><span data-stu-id="efbae-141">I suggest you next follow my tutorial [Deploy a Secure ASP.NET MVC app with Membership, OAuth, and SQL Database to a Windows Azure Web Site](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="efbae-142">뛰어난 자습서가 Tom Dykstra 중간 수준 [ASP.NET MVC 응용 프로그램에 대 한 Entity Framework 데이터 모델을 만드는](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="efbae-142">An excellent tutorial is Tom Dykstra's intermediate-level [Creating an Entity Framework Data Model for an ASP.NET MVC Application](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="efbae-143">[Stackoverflow](http://stackoverflow.com/help) 및 [ASP.NET MVC 포럼](https://forums.asp.net/1146.aspx) 질문을 하는 좋은 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="efbae-143">[Stackoverflow](http://stackoverflow.com/help) and the [ASP.NET MVC forums](https://forums.asp.net/1146.aspx) are a great places to ask questions.</span></span> <span data-ttu-id="efbae-144">에 따라 [me](https://twitter.com/RickAndMSFT) 에서 twitter 때문 내 최신 자습서에 대 한 업데이트를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efbae-144">Follow [me](https://twitter.com/RickAndMSFT) on twitter so you can get updates on my latest tutorials.</span></span>

<span data-ttu-id="efbae-145">피드백을 보내 주십시오.</span><span class="sxs-lookup"><span data-stu-id="efbae-145">Feedback is welcome.</span></span>

<span data-ttu-id="efbae-146">- [Rick Anderson](https://blogs.msdn.com/rickAndy) twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="efbae-146">— [Rick Anderson](https://blogs.msdn.com/rickAndy) twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT)</span></span>  
<span data-ttu-id="efbae-147">- [Scott Hanselman](http://www.hanselman.com/blog/) twitter: [@shanselman](https://twitter.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="efbae-147">— [Scott Hanselman](http://www.hanselman.com/blog/) twitter: [@shanselman](https://twitter.com/shanselman)</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="efbae-148">이전</span><span class="sxs-lookup"><span data-stu-id="efbae-148">Previous</span></span>](adding-validation-to-the-model.md)
