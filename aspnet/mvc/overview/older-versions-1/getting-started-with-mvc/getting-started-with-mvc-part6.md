---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part6
title: 추가 된 메서드를 만들고 보기 만들기 | Microsoft Docs
author: shanselman
description: ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 읽기 및 쓰기는 데이터베이스에서 단순 웹 응용 프로그램을 만듭니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/14/2010
ms.topic: article
ms.assetid: a3a90963-0286-4fa0-9b3d-c230cc18b0a3
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part6
msc.type: authoredcontent
ms.openlocfilehash: 48e656a0c394b9db5baaec9c557ec38c4020d41b
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="adding-a-create-method-and-create-view"></a><span data-ttu-id="65006-104">추가 된 메서드를 만들고 보기 만들기</span><span class="sxs-lookup"><span data-stu-id="65006-104">Adding a Create Method and Create View</span></span>
====================
<span data-ttu-id="65006-105">으로 [Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="65006-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="65006-106">ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="65006-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="65006-107">읽기 및 쓰기는 데이터베이스에서 단순 웹 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65006-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="65006-108">방문는 [ASP.NET MVC 학습 센터](../../../index.md) 자습서 및 예제에는 다른 ASP.NET MVC를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65006-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>


<span data-ttu-id="65006-109">이 섹션에서는 사용자가 데이터베이스에 새 동영상을 만들 수 있도록 하는 데 필요한 지원을 구현 것 이며 합니다.</span><span class="sxs-lookup"><span data-stu-id="65006-109">In this section we are going to implement the support necessary to enable users to create new movies in our database.</span></span> <span data-ttu-id="65006-110">영화/만들기 URL 동작을 구현 하 여 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="65006-110">We'll do this by implementing the /Movies/Create URL action.</span></span>

<span data-ttu-id="65006-111">영화/만들기 URL 구현 두 단계로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="65006-111">Implementing the /Movies/Create URL is a two step process.</span></span> <span data-ttu-id="65006-112">사용자가 동영상/만들기 URL를 처음 방문할 때 새 동영상을 입력 하 여 채울 수 있는 HTML 폼을 표시 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="65006-112">When a user first visits the /Movies/Create URL we want to show them an HTML form that they can fill out to enter a new movie.</span></span> <span data-ttu-id="65006-113">그런 다음 사용자가 폼과 데이터는 서버에 다시 게시를 전송 하려고 게시 된 콘텐츠를 검색 하 고 데이터베이스에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="65006-113">Then, when the user submits the form and posts the data back to the server, we want to retrieve the posted contents and save it into our database.</span></span>

<span data-ttu-id="65006-114">MoviesController 클래스 내에서 두 개의 create () 메서드 내에서 이러한 두 단계를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="65006-114">We'll implement these two steps within two Create() methods within our MoviesController class.</span></span> <span data-ttu-id="65006-115">한 가지 방법은 표시 됩니다는 &lt;양식&gt; 사용자를 만들려면 새 동영상을 채울 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65006-115">One method will show the &lt;form&gt; that the user should fill out to create a new movie.</span></span> <span data-ttu-id="65006-116">두 번째 방법은 사용자가을 전송할 때 게시 된 데이터 처리를 처리할는 &lt;양식&gt; 를 서버에 백업 하 고 데이터베이스 내에서 새 동영상을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="65006-116">The second method will handle processing the posted data when the user submits the &lt;form&gt; back to the server, and save a new Movie within our database.</span></span>

<span data-ttu-id="65006-117">다음은 코드가를 구현 하려면 MoviesController 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="65006-117">Below is the code we'll add to our MoviesController class to implement this:</span></span>

[!code-csharp[Main](getting-started-with-mvc-part6/samples/sample1.cs)]

<span data-ttu-id="65006-118">위의 코드는 모든 컨트롤러 내에서 사용 해야 하는 코드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="65006-118">The above code contains all of the code that we'll need within our Controller.</span></span>

<span data-ttu-id="65006-119">이제 사용자에 게을 둔 양식을 표시 하는을 사용 해야 하는 Create View 템플릿을 구현 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="65006-119">Let's now implement the Create View template that we'll use to display a form to the user.</span></span> <span data-ttu-id="65006-120">첫 번째 Create 메서드를 마우스 오른쪽 단추로 클릭 알아보고 영화 폼에 대 한 보기 템플릿을 만들려면 "뷰 추가"를 선택 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="65006-120">We'll right click in the first Create method and select "Add View" to create the view template for our Movie form.</span></span>

<span data-ttu-id="65006-121">해당 보기 데이터 클래스 보기 템플릿 "영화"를 전달 하려고 하 고 "만들기" 템플릿 "스 캐" 한다고 지정 하는 선택 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="65006-121">We'll select that we are going to pass the view template a "Movie" as its view data class, and indicate that we want to "scaffold" a "Create" template.</span></span>

<span data-ttu-id="65006-122">[![뷰 추가](getting-started-with-mvc-part6/_static/image2.png)](getting-started-with-mvc-part6/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="65006-122">[![Add View](getting-started-with-mvc-part6/_static/image2.png)](getting-started-with-mvc-part6/_static/image1.png)</span></span>

<span data-ttu-id="65006-123">추가 단추를 클릭 한 후 드립니다 \Movies\Create.aspx 보기 템플릿 만들어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65006-123">After you click the Add button, \Movies\Create.aspx View template will be created for you.</span></span> <span data-ttu-id="65006-124">"만들기"를 "콘텐츠 보기" 드롭다운 목록에서 선택 것 때문에 뷰 추가 대화 상자 자동으로 "스 캐 폴드 된" 일부 기본 콘텐츠를 수행해 줍니다.</span><span class="sxs-lookup"><span data-stu-id="65006-124">Because we selected "Create" from the "view content" dropdown, the Add View dialog automatically "scaffolded" some default content for us.</span></span> <span data-ttu-id="65006-125">스 캐 폴딩을 HTML 만든 &lt;양식&gt;, 이동, 메시지 유효성 검사 오류에 대 한 전체 및 클래스의 각 속성에 대 한 레이블 및 필드 만든 동영상에 대 한 스 캐 폴딩 알고, 있으므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="65006-125">The scaffolding created an HTML &lt;form&gt;, a place for validation error messages to go, and since scaffolding knows about Movies, it created Label and Fields for each property of our class.</span></span>

[!code-aspx[Main](getting-started-with-mvc-part6/samples/sample2.aspx)]

<span data-ttu-id="65006-126">데이터베이스의 ID가 영화를 자동으로 제공 하며, 이므로 해당 참조 모델을 제거 해당 필드 보겠습니다. Id 만들기 시각입니다.</span><span class="sxs-lookup"><span data-stu-id="65006-126">Since our database automatically gives a Movie an ID, let's remove those fields that reference model.Id from our Create View.</span></span> <span data-ttu-id="65006-127">후 7 선을 제거 &lt;범례&gt;필드&lt;/legend&gt; 대로 않도록 하는 ID 필드 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="65006-127">Remove the 7 lines after &lt;legend&gt;Fields&lt;/legend&gt; as they show the ID field that we don't want.</span></span>

<span data-ttu-id="65006-128">보겠습니다 이제 새 동영상을 만들고 데이터베이스에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="65006-128">Let's now create a new movie and add it to the database.</span></span> <span data-ttu-id="65006-129">응용 프로그램을 다시 실행 하 여 알아보고 방문 하겠습니다는 "/ 영화" 새 동영상을 추가 하려면 "만들기" 연결 URL을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="65006-129">We'll do this by running the application again and visit the "/Movies" URL and click the "Create" link to add a new Movie.</span></span>

<span data-ttu-id="65006-130">[![만들기-Windows Internet Explorer](getting-started-with-mvc-part6/_static/image4.png)](getting-started-with-mvc-part6/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="65006-130">[![Create - Windows Internet Explorer](getting-started-with-mvc-part6/_static/image4.png)](getting-started-with-mvc-part6/_static/image3.png)</span></span>

<span data-ttu-id="65006-131">만들기 단추를 클릭가 게시 다시 (통해 HTTP POST) 방금 만든 /Movies/Create 메서드에이 폼에 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="65006-131">When we click the Create button, we'll be posting back (via HTTP POST) the data on this form to the /Movies/Create method that we just created.</span></span> <span data-ttu-id="65006-132">때 시스템이 자동으로 url "numTimes" 및 "name" 매개 변수는 데 걸린 하 고 해당 메서드를 앞에 있는 매개 변수에 매핑된 마찬가지로 시스템은 자동으로 양식 필드에서 게시물을 가져오고 개체에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="65006-132">Just like when the system automatically took the "numTimes" and "name " parameter out of the URL and mapped them to parameters on a method earlier, the system will automatically take the Form Fields from a POST and map them to an object.</span></span> <span data-ttu-id="65006-133">이 경우 "ReleaseDate" 및 "제목"와 같은 html 필드의 값을 자동으로 동영상의 새 인스턴스를 올바른 속성에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="65006-133">In this case, values from fields in HTML like "ReleaseDate" and "Title" will automatically be put into the correct properties of a new instance of a Movie.</span></span>

<span data-ttu-id="65006-134">이제 두 번째 Create 메서드 우리의 MoviesController에서 다시 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="65006-134">Let's look at the second Create method from our MoviesController again.</span></span> <span data-ttu-id="65006-135">걸리는 "영화" 개체를 인수로 사항을 참고 하십시오.</span><span class="sxs-lookup"><span data-stu-id="65006-135">Notice how it takes a "Movie" object as an argument:</span></span>

[!code-csharp[Main](getting-started-with-mvc-part6/samples/sample3.cs)]

<span data-ttu-id="65006-136">이 영화 개체가 만들기 작업 메서드의 [HttpPost] 버전에 전달 된 다음 및 데이터베이스에 저장 하 고 사용자 영화 목록에 저장 된 결과 보여 주는 index () 동작 메서드를 다시 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="65006-136">This Movie object was then passed to the [HttpPost] version of our Create action method, and we saved it in the database and then redirected the user back to the Index() action method which will show the saved result in the movie list:</span></span>

<span data-ttu-id="65006-137">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part6/_static/image6.png)](getting-started-with-mvc-part6/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="65006-137">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part6/_static/image6.png)](getting-started-with-mvc-part6/_static/image5.png)</span></span>

<span data-ttu-id="65006-138">म 우리의 영화은 하지만 및 제목 없음 함께 동영상을 저장 하는 데이터베이스 허용 하지 않는 확인 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="65006-138">We aren't checking if our movies are correct, though, and the database won't allow us to save a movie with no Title.</span></span> <span data-ttu-id="65006-139">이 좋을 수 알립니다를 이전 데이터베이스에서 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="65006-139">It'd be nice if we could tell the user that before the database threw an error.</span></span> <span data-ttu-id="65006-140">응용 프로그램에 유효성 검사 지원을 추가 하 여 다음이 단계를 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="65006-140">We'll do this next by adding validation support to our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="65006-141">[이전](getting-started-with-mvc-part5.md)
> [다음](getting-started-with-mvc-part7.md)</span><span class="sxs-lookup"><span data-stu-id="65006-141">[Previous](getting-started-with-mvc-part5.md)
[Next](getting-started-with-mvc-part7.md)</span></span>
