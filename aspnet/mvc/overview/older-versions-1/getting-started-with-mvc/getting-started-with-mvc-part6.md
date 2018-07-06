---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part6
title: 추가 된 메서드를 만들고 보기 | Microsoft Docs
author: shanselman
description: ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 읽기 및 쓰기 데이터베이스에서 간단한 웹 응용 프로그램을 만듭니다.
ms.author: aspnetcontent
ms.date: 08/14/2010
ms.assetid: a3a90963-0286-4fa0-9b3d-c230cc18b0a3
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part6
msc.type: authoredcontent
ms.openlocfilehash: cf0d721b551c38e8c38e35f82b73ee1b14cd068f
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37840968"
---
<a name="adding-a-create-method-and-create-view"></a><span data-ttu-id="cfed7-104">추가 된 메서드를 만들고 보기</span><span class="sxs-lookup"><span data-stu-id="cfed7-104">Adding a Create Method and Create View</span></span>
====================
<span data-ttu-id="cfed7-105">[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="cfed7-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="cfed7-106">ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="cfed7-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="cfed7-107">읽기 및 쓰기 데이터베이스는 간단한 웹 응용 프로그램을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfed7-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="cfed7-108">방문 합니다 [ASP.NET MVC 학습 센터](../../../index.md) 자습서 및 샘플 다른 ASP.NET MVC를 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfed7-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>


<span data-ttu-id="cfed7-109">이 섹션에서 사용자가 데이터베이스에 새 영화를 만들 수 있게 하는 데 필요한 지원을 구현 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfed7-109">In this section we are going to implement the support necessary to enable users to create new movies in our database.</span></span> <span data-ttu-id="cfed7-110">동영상/만들기 URL 동작을 구현 하 여이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfed7-110">We'll do this by implementing the /Movies/Create URL action.</span></span>

<span data-ttu-id="cfed7-111">두 단계로 구성 됩니다 영화/만들기 URL을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfed7-111">Implementing the /Movies/Create URL is a two step process.</span></span> <span data-ttu-id="cfed7-112">사용자가 영화/만들기 URL를 처음 방문할 때 새 동영상 입력을 채울 수 있는 HTML 폼 표시 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfed7-112">When a user first visits the /Movies/Create URL we want to show them an HTML form that they can fill out to enter a new movie.</span></span> <span data-ttu-id="cfed7-113">그런 다음 사용자가 폼 및 데이터를 서버에 다시 게시를 전송 하려고 게시 된 콘텐츠를 검색 하 고 데이터베이스에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfed7-113">Then, when the user submits the form and posts the data back to the server, we want to retrieve the posted contents and save it into our database.</span></span>

<span data-ttu-id="cfed7-114">두 create () 메서드 내에서 이러한 두 단계 MoviesController 클래스 내에서 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cfed7-114">We'll implement these two steps within two Create() methods within our MoviesController class.</span></span> <span data-ttu-id="cfed7-115">한 가지 방법은 표시 됩니다는 &lt;폼&gt; 사용자를 만드는 새 동영상을 작성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfed7-115">One method will show the &lt;form&gt; that the user should fill out to create a new movie.</span></span> <span data-ttu-id="cfed7-116">두 번째 방법은 사용자가 제출 하는 경우 게시 된 데이터를 처리 처리할 합니다 &lt;폼&gt; 서버에 백업 하 고 데이터베이스 내에서 새 동영상을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfed7-116">The second method will handle processing the posted data when the user submits the &lt;form&gt; back to the server, and save a new Movie within our database.</span></span>

<span data-ttu-id="cfed7-117">다음 코드는이 구현 하려면 MoviesController 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfed7-117">Below is the code we'll add to our MoviesController class to implement this:</span></span>

[!code-csharp[Main](getting-started-with-mvc-part6/samples/sample1.cs)]

<span data-ttu-id="cfed7-118">위의 코드는 모든 컨트롤러 내 해야 하는 코드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfed7-118">The above code contains all of the code that we'll need within our Controller.</span></span>

<span data-ttu-id="cfed7-119">Create View 템플릿을 사용 하 여 사용자에 게 폼을 표시 하는 이제 구현 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="cfed7-119">Let's now implement the Create View template that we'll use to display a form to the user.</span></span> <span data-ttu-id="cfed7-120">첫 번째 Create 메서드를 마우스 오른쪽 단추로 클릭 하 고 영화 폼에 대 한 보기 템플릿을 만들려면 "뷰 추가"를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfed7-120">We'll right click in the first Create method and select "Add View" to create the view template for our Movie form.</span></span>

<span data-ttu-id="cfed7-121">해당 보기 데이터 클래스로 보기 템플릿에서 "영화"을 전달 하려고 하 고 "스 캐 폴드" "만들기" 템플릿으로 하려고 한다는 것을 나타내려면 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfed7-121">We'll select that we are going to pass the view template a "Movie" as its view data class, and indicate that we want to "scaffold" a "Create" template.</span></span>

<span data-ttu-id="cfed7-122">[![뷰 추가](getting-started-with-mvc-part6/_static/image2.png)](getting-started-with-mvc-part6/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="cfed7-122">[![Add View](getting-started-with-mvc-part6/_static/image2.png)](getting-started-with-mvc-part6/_static/image1.png)</span></span>

<span data-ttu-id="cfed7-123">추가 단추를 클릭 하면 \Movies\Create.aspx 템플릿 보기를 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cfed7-123">After you click the Add button, \Movies\Create.aspx View template will be created for you.</span></span> <span data-ttu-id="cfed7-124">"콘텐츠 보기" 드롭다운에서 "만들기"를 선택 했기 때문에 뷰 추가 대화 상자 자동으로 "스 캐 폴드 된" 일부 기본 콘텐츠 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfed7-124">Because we selected "Create" from the "view content" dropdown, the Add View dialog automatically "scaffolded" some default content for us.</span></span> <span data-ttu-id="cfed7-125">스 캐 폴딩을 만들 HTML &lt;폼&gt;, 유효성 검사 오류에 대 한 위치에서 메시지 및 스 캐 폴딩 영화를 알고, 이후 만들어질 레이블과 필드 클래스의 각 속성에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfed7-125">The scaffolding created an HTML &lt;form&gt;, a place for validation error messages to go, and since scaffolding knows about Movies, it created Label and Fields for each property of our class.</span></span>

[!code-aspx[Main](getting-started-with-mvc-part6/samples/sample2.aspx)]

<span data-ttu-id="cfed7-126">데이터베이스 자동으로 영화 ID를 제공 하므로 참조 모델을 제거 필드로 보겠습니다. 만들기 보기에서 id입니다.</span><span class="sxs-lookup"><span data-stu-id="cfed7-126">Since our database automatically gives a Movie an ID, let's remove those fields that reference model.Id from our Create View.</span></span> <span data-ttu-id="cfed7-127">제거 후 7 줄 &lt;범례&gt;필드&lt;/legend&gt; 아직 ID 필드는 표시 된 대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfed7-127">Remove the 7 lines after &lt;legend&gt;Fields&lt;/legend&gt; as they show the ID field that we don't want.</span></span>

<span data-ttu-id="cfed7-128">보겠습니다 이제 새 동영상을 만들고 데이터베이스에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfed7-128">Let's now create a new movie and add it to the database.</span></span> <span data-ttu-id="cfed7-129">응용 프로그램을 다시 실행 하 여이 작업을 수행 하 고 방문 드리겠습니다는 "/ 영화" 새 영화를 추가 하려면 "만들기" 링크 URL을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfed7-129">We'll do this by running the application again and visit the "/Movies" URL and click the "Create" link to add a new Movie.</span></span>

<span data-ttu-id="cfed7-130">[![만들기-Windows Internet Explorer](getting-started-with-mvc-part6/_static/image4.png)](getting-started-with-mvc-part6/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="cfed7-130">[![Create - Windows Internet Explorer](getting-started-with-mvc-part6/_static/image4.png)](getting-started-with-mvc-part6/_static/image3.png)</span></span>

<span data-ttu-id="cfed7-131">만들기 단추를 클릭 하면 되십시오 다시 (HTTP POST를 통해) 우리가 방금 만들었던 /Movies/Create 메서드에이 양식의 데이터를입니다.</span><span class="sxs-lookup"><span data-stu-id="cfed7-131">When we click the Create button, we'll be posting back (via HTTP POST) the data on this form to the /Movies/Create method that we just created.</span></span> <span data-ttu-id="cfed7-132">시스템 자동으로 URL에서 "numTimes" 및 "name" 매개 변수는 데 걸린 시간과 메서드 앞에 있는 매개 변수에 매핑된 해당, 마찬가지로 시스템은 및 자동으로 수행 양식 필드 게시물에서 개체에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="cfed7-132">Just like when the system automatically took the "numTimes" and "name " parameter out of the URL and mapped them to parameters on a method earlier, the system will automatically take the Form Fields from a POST and map them to an object.</span></span> <span data-ttu-id="cfed7-133">이 경우 "ReleaseDate" 및 "Title"와 같은 html 필드의 값은 동영상의 새 인스턴스를 올바른 속성에 자동으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cfed7-133">In this case, values from fields in HTML like "ReleaseDate" and "Title" will automatically be put into the correct properties of a new instance of a Movie.</span></span>

<span data-ttu-id="cfed7-134">보겠습니다 두 번째 Create 메서드는 MoviesController에서 다시 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfed7-134">Let's look at the second Create method from our MoviesController again.</span></span> <span data-ttu-id="cfed7-135">"영화" 개체를 인수로 사용 하는 방법을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfed7-135">Notice how it takes a "Movie" object as an argument:</span></span>

[!code-csharp[Main](getting-started-with-mvc-part6/samples/sample3.cs)]

<span data-ttu-id="cfed7-136">이 동영상 개체 만들기 작업 메서드를 사용 하 여 [HttpPost] 버전으로 전달한 다음 및 데이터베이스에 저장 하 고 영화 목록에 저장 된 결과 보여 주는 index () 작업 메서드를 다시 사용자 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="cfed7-136">This Movie object was then passed to the [HttpPost] version of our Create action method, and we saved it in the database and then redirected the user back to the Index() action method which will show the saved result in the movie list:</span></span>

<span data-ttu-id="cfed7-137">[![영화 목록-Windows Internet Explorer](getting-started-with-mvc-part6/_static/image6.png)](getting-started-with-mvc-part6/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="cfed7-137">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part6/_static/image6.png)](getting-started-with-mvc-part6/_static/image5.png)</span></span>

<span data-ttu-id="cfed7-138">이 동영상은 하지만 잘못 및 데이터베이스 제목 없음를 사용 하 여 영화를 저장할 수 없습니다 확인 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cfed7-138">We aren't checking if our movies are correct, though, and the database won't allow us to save a movie with no Title.</span></span> <span data-ttu-id="cfed7-139">사용자 데이터베이스 앞에 오류가 발생 했습니다 알려줍니다 수 하는 경우 유용한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cfed7-139">It'd be nice if we could tell the user that before the database threw an error.</span></span> <span data-ttu-id="cfed7-140">응용 프로그램에 유효성 검사 지원을 추가 하 여이 다음을 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="cfed7-140">We'll do this next by adding validation support to our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="cfed7-141">[이전](getting-started-with-mvc-part5.md)
> [다음](getting-started-with-mvc-part7.md)</span><span class="sxs-lookup"><span data-stu-id="cfed7-141">[Previous](getting-started-with-mvc-part5.md)
[Next](getting-started-with-mvc-part7.md)</span></span>
