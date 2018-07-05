---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
title: AJAX를 사용 하 여 매핑 시나리오 구현 | Microsoft Docs
author: microsoft
description: 11 단계 NerdDinner 응용 프로그램을 작성, 편집 또는 l을 보려는 dinners 보기는 사용자를 사용 하도록 설정 하면 AJAX 매핑 지원을 통합 하는 방법을 표시 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: f731990a-0a81-4d62-81df-87d676cdedd6
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
msc.type: authoredcontent
ms.openlocfilehash: 173ba551ca453ad46dbfd83ce1a2eb4a9b8eba3f
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37374294"
---
<a name="use-ajax-to-implement-mapping-scenarios"></a><span data-ttu-id="c9559-103">AJAX를 사용 하 여 매핑 시나리오 구현</span><span class="sxs-lookup"><span data-stu-id="c9559-103">Use AJAX to Implement Mapping Scenarios</span></span>
====================
<span data-ttu-id="c9559-104">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="c9559-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="c9559-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="c9559-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="c9559-106">이 무료의 11 단계 ["NerdDinner" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 는 안내를 통한 작은 빌드 하지만 ASP.NET MVC 1을 사용 하 여 웹 응용 프로그램을 완료 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-106">This is step 11 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="c9559-107">11 단계 NerdDinner 응용 프로그램을 작성, 편집 또는 dinner의 위치를 그래픽으로 보려면 dinners 보기는 사용자를 사용 하도록 설정 하면 AJAX 매핑 지원을 통합 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-107">Step 11 shows how to integrate AJAX mapping support into our NerdDinner application, enabling users who are creating, editing or viewing dinners to see the location of the dinner graphically.</span></span>
> 
> <span data-ttu-id="c9559-108">ASP.NET MVC 3을 사용 하는 경우 수행 하는 것이 좋습니다 합니다 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 하거나 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-step-11-integrating-an-ajax-map"></a><span data-ttu-id="c9559-109">NerdDinner 11 단계: AJAX 지도 통합</span><span class="sxs-lookup"><span data-stu-id="c9559-109">NerdDinner Step 11: Integrating an AJAX Map</span></span>

<span data-ttu-id="c9559-110">이제 약간 시각적으로 흥미로운 AJAX 매핑 지원을 통합 하 여 응용 프로그램을 만들 것 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-110">We'll now make our application a little more visually exciting by integrating AJAX mapping support.</span></span> <span data-ttu-id="c9559-111">이렇게 하면 만들기, 편집 또는 보기의 저녁 식사 위치를 그래픽으로 보려면 dinners 사용자 활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-111">This will enable users who are creating, editing or viewing dinners to see the location of the dinner graphically.</span></span>

### <a name="creating-a-map-partial-view"></a><span data-ttu-id="c9559-112">지도 부분 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="c9559-112">Creating a Map Partial View</span></span>

<span data-ttu-id="c9559-113">응용 프로그램 내의 여러 위치에서 매핑 기능을 사용 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-113">We are going to use mapping functionality in several places within our application.</span></span> <span data-ttu-id="c9559-114">시험 코드를 유지 하려면 여러 컨트롤러 작업 및 보기에서 다시 사용할 수 있는 단일 부분 템플릿 내에서 공통 맵 기능을 캡슐화 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-114">To keep our code DRY we'll encapsulate the common map functionality within a single partial template that we can re-use across multiple controller actions and views.</span></span> <span data-ttu-id="c9559-115">"Map.ascx"이 부분 뷰의 이름을 하 고 \Views\Dinners 디렉터리 내에 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-115">We'll name this partial view "map.ascx" and create it within the \Views\Dinners directory.</span></span>

<span data-ttu-id="c9559-116">만들 수 있습니다는 map.ascx 부분 \Views\Dinners 디렉터리를 마우스 오른쪽 단추로 클릭 하 고 추가-선택 하 여&gt;메뉴 명령을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-116">We can create the map.ascx partial by right-clicking on the \Views\Dinners directory and choosing the Add-&gt;View menu command.</span></span> <span data-ttu-id="c9559-117">에서는 "Map.ascx" 뷰의 이름을, 부분 뷰를 확인 하 고 나타내는 강력한 형식의 "Dinner" 모델 클래스를 전달 하려고 하:</span><span class="sxs-lookup"><span data-stu-id="c9559-117">We'll name the view "Map.ascx", check it as a partial view, and indicate that we are going to pass it a strongly-typed "Dinner" model class:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image1.png)

<span data-ttu-id="c9559-118">"추가" 단추를 클릭할 때 부분 템플릿은 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-118">When we click the "Add" button our partial template will be created.</span></span> <span data-ttu-id="c9559-119">다음 내용이 다음 Map.ascx 파일을 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-119">We'll then update the Map.ascx file to have the following content:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample1.aspx)]

<span data-ttu-id="c9559-120">첫 번째 &lt;스크립트&gt; 가리키는 Microsoft Virtual Earth 6.2 매핑 라이브러리를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-120">The first &lt;script&gt; reference points to the Microsoft Virtual Earth 6.2 mapping library.</span></span> <span data-ttu-id="c9559-121">두 번째 &lt;스크립트&gt; 이 일반적인 Javascript 매핑 논리를 캡슐화 할는 곧 만들 map.js 파일을 가리키는 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-121">The second &lt;script&gt; reference points to a map.js file that we will shortly create which will encapsulate our common Javascript mapping logic.</span></span> <span data-ttu-id="c9559-122">합니다 &lt;div id = "theMap"&gt; 요소 Virtual Earth가 지도 호스트 하는 데 사용할 HTML 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-122">The &lt;div id="theMap"&gt; element is the HTML container that Virtual Earth will use to host the map.</span></span>

<span data-ttu-id="c9559-123">그런 다음 포함 된 있습니다 &lt;스크립트&gt; 이 보기에 특정 두 JavaScript 함수를 포함 하는 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-123">We then have an embedded &lt;script&gt; block that contains two JavaScript functions specific to this view.</span></span> <span data-ttu-id="c9559-124">첫 번째 함수는 jQuery 유선 전화 접속 페이지가 클라이언트 쪽 스크립트를 실행할 준비가 되 면 실행 되는 함수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-124">The first function uses jQuery to wire-up a function that executes when the page is ready to run client-side script.</span></span> <span data-ttu-id="c9559-125">LoadMap() 도우미 함수를 호출 하기 virtual earth 맵 컨트롤을 로드 하려면 Map.js 스크립트 파일 내에서 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-125">It calls a LoadMap() helper function that we'll define within our Map.js script file to load the virtual earth map control.</span></span> <span data-ttu-id="c9559-126">두 번째 함수는 위치를 식별 하는 지도에 핀을 추가 하는 콜백 이벤트 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-126">The second function is a callback event handler that adds a pin to the map that identifies a location.</span></span>

<span data-ttu-id="c9559-127">서버 쪽에서는 사용 하는 방법을 확인할 수 있습니다 &lt;% = %&gt; 위도 및 경도 JavaScript에 매핑할 것임 저녁 식사를 포함 하는 클라이언트 쪽 스크립트 블록 내에서 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-127">Notice how we are using a server-side &lt;%= %&gt; block within the client-side script block to embed the latitude and longitude of the Dinner we want to map into the JavaScript.</span></span> <span data-ttu-id="c9559-128">이것이 (호출 하지 않아도 별도 AJAX 서버에 다시 – 값을 검색할 수 있도록 빠르게) 클라이언트 쪽 스크립트에서 사용할 수 있는 동적 값을 출력 하는 데 유용한 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-128">This is a useful technique to output dynamic values that can be used by client-side script (without requiring a separate AJAX call back to the server to retrieve the values – which makes it faster).</span></span> <span data-ttu-id="c9559-129">&lt;% = %&gt; – 서버의 뷰를 렌더링 하는 경우 블록 실행 되 고 따라서 html 출력 방금 결국 포함 된 JavaScript 값을 사용 하 여 (예: var 위도 47.64312; =) 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-129">The &lt;%= %&gt; blocks will execute when the view is rendering on the server – and so the output of the HTML will just end up with embedded JavaScript values (for example: var latitude = 47.64312;).</span></span>

### <a name="creating-a-mapjs-utility-library"></a><span data-ttu-id="c9559-130">Map.js 유틸리티 라이브러리 만들기</span><span class="sxs-lookup"><span data-stu-id="c9559-130">Creating a Map.js utility library</span></span>

<span data-ttu-id="c9559-131">이 맵에 대 한 JavaScript 기능을 캡슐화 (및 위의 LoadMap 및 LoadPin 메서드 구현)를 사용할 수 있는 Map.js 파일을 이제 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-131">Let's now create the Map.js file that we can use to encapsulate the JavaScript functionality for our map (and implement the LoadMap and LoadPin methods above).</span></span> <span data-ttu-id="c9559-132">수는 프로젝트 내에서 \Scripts 디렉터리를 마우스 오른쪽 단추로 클릭 하 여이 작업을 수행 하 고 선택한를 "추가-&gt;새 항목" 메뉴 명령, JScript 항목을 선택 하 고 "Map.js" 라는 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-132">We can do this by right-clicking on the \Scripts directory within our project, and then choose the "Add-&gt;New Item" menu command, select the JScript item, and name it "Map.js".</span></span>

<span data-ttu-id="c9559-133">다음 JavaScript 코드를 추가할 것은 지도가 표시는 dinners에 대 한 위치 핀을 추가 하는 Virtual Earth와 상호 작용할 Map.js 파일:</span><span class="sxs-lookup"><span data-stu-id="c9559-133">Below is the JavaScript code we'll add to the Map.js file that will interact with Virtual Earth to display our map and add locations pins to it for our dinners:</span></span>

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample2.js)]

### <a name="integrating-the-map-with-create-and-edit-forms"></a><span data-ttu-id="c9559-134">만들기 및 편집 양식와 지도 통합</span><span class="sxs-lookup"><span data-stu-id="c9559-134">Integrating the Map with Create and Edit Forms</span></span>

<span data-ttu-id="c9559-135">이제 기존 만들기 및 편집 시나리오를 사용 하 여 지도 지원을 통합 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-135">We'll now integrate the Map support with our existing Create and Edit scenarios.</span></span> <span data-ttu-id="c9559-136">좋은 소식은 손쉽게 할 일은이 및 변경의 컨트롤러 코드를 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-136">The good news is that this is pretty easy to-do, and doesn't require us to change any of our Controller code.</span></span> <span data-ttu-id="c9559-137">만들기 및 편집 보기를 사용 하 여 dinner 폼 UI를 구현 하는 일반적인 "DinnerForm" 부분 뷰를 공유 하므로 수 한곳에서 지도 추가 하 고 모두는 만들기 및 편집 시나리오를 사용 하 여.</span><span class="sxs-lookup"><span data-stu-id="c9559-137">Because our Create and Edit views share a common "DinnerForm" partial view to implement the dinner form UI, we can add the map in one place and have both our Create and Edit scenarios use it.</span></span>

<span data-ttu-id="c9559-138">할 일을 먼저 모든 \Views\Dinners\DinnerForm.ascx 부분 뷰를 열고 새 지도가 부분을 포함 하도록 업데이트 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-138">All we need to-do is to open the \Views\Dinners\DinnerForm.ascx partial view and update it to include our new map partial.</span></span> <span data-ttu-id="c9559-139">업데이트 된 DinnerForm 모양을 맵에 추가 되 면 다음과 같습니다 (참고: HTML 폼 요소 간략하게 표현 하기 위해 아래 코드 조각에서 생략 됩니다).</span><span class="sxs-lookup"><span data-stu-id="c9559-139">Below is what the updated DinnerForm will look like once the map is added (note: the HTML form elements are omitted from the code snippet below for brevity):</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample3.aspx)]

<span data-ttu-id="c9559-140">위의 부분 DinnerForm (Dinner 개체 뿐만 아니라 국가 dropdownlist를 채우는 데 SelectList 하므로) 모델 형식으로 "DinnerFormViewModel" 형식의 개체를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-140">The DinnerForm partial above takes an object of type "DinnerFormViewModel" as its model type (because it needs both a Dinner object, as well as a SelectList to populate the dropdownlist of countries).</span></span> <span data-ttu-id="c9559-141">부분 지도가 하기만 "Dinner" 형식의 개체 모델 형식은, 및 하므로 지도 부분 렌더링 하는 경우 전달 Dinner 하위 속성만 DinnerFormViewModel의에:</span><span class="sxs-lookup"><span data-stu-id="c9559-141">Our Map partial just needs an object of type "Dinner" as its model type, and so when we render the map partial we are passing just the Dinner sub-property of DinnerFormViewModel to it:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample4.aspx)]

<span data-ttu-id="c9559-142">JavaScript 함수를 "Address" HTML 텍스트 상자에 "흐리게" 이벤트를 연결할 부분에서는 jQuery 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-142">The JavaScript function we've added to the partial uses jQuery to attach a "blur" event to the "Address" HTML textbox.</span></span> <span data-ttu-id="c9559-143">텍스트 상자에 이야기를 클릭할 때 발생 하는 "포커스" 이벤트 또는 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-143">You've probably heard of "focus" events that fire when a user clicks or tabs into a textbox.</span></span> <span data-ttu-id="c9559-144">반대는 사용자는 텍스트 상자를 종료 될 때 발생 하는 "흐리게" 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-144">The opposite is a "blur" event that fires when a user exits a textbox.</span></span> <span data-ttu-id="c9559-145">위의 이벤트 처리기 문제가 발생 하면이 고 다음이 맵에 새 주소 위치를 그리는 경우 위도 및 경도 텍스트 상자 값을 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-145">The above event handler clears the latitude and longitude textbox values when this happens, and then plots the new address location on our map.</span></span> <span data-ttu-id="c9559-146">Map.js 파일 내에 정의한 콜백 이벤트 처리기는 virtual earth 것에 지정 했던 주소를 기반으로 하 여 반환 되는 값을 사용 하 여 폼에 경도 및 위도 텍스트 상자를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-146">A callback event handler that we defined within the map.js file will then update the longitude and latitude textboxes on our form using values returned by virtual earth based on the address we gave it.</span></span>

<span data-ttu-id="c9559-147">및 이제 다시 응용 프로그램을 실행 하 고는 표준 Dinner 폼 요소와 함께 표시 매핑할 기본값 살펴보겠습니다 "호스트 Dinner" 탭을 클릭 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-147">And now when we run our application again and click the "Host Dinner" tab we'll see a default map displayed along with our standard Dinner form elements:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image2.png)

<span data-ttu-id="c9559-148">주소를 입력 하 고 제거를 탭 한 다음, 지도 위치를 표시 하려면 동적으로 업데이트 됩니다 하 고 이벤트 처리기는 위치 값을 사용 하 여 위도/경도 텍스트 상자를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-148">When we type in an address, and then tab away, the map will dynamically update to display the location, and our event handler will populate the latitude/longitude textboxes with the location values:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image3.png)

<span data-ttu-id="c9559-149">새 저녁 식사를 저장 하 고 편집을 위해 다시 여십시오, 페이지를 로드할 때 지도 위치 표시 되도록 소요 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-149">If we save the new dinner and then open it again for editing, we'll find that the map location is displayed when the page loads:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image4.png)

<span data-ttu-id="c9559-150">주소 필드 변경 될 때마다 맵과 위도/경도 좌표를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-150">Every time the address field is changed, the map and the latitude/longitude coordinates will update.</span></span>

<span data-ttu-id="c9559-151">저녁 식사 위치를 표시 하는 지도, 했으므로 대신 숨겨진된 요소가 되도록 (지도 자동으로 업데이트 하는 주소를 입력 하는 각 시간) 이후 표시 텍스트 상자에서 위도 및 경도 양식 필드를 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-151">Now that the map displays the Dinner location, we can also change the Latitude and Longitude form fields from being visible textboxes to instead be hidden elements (since the map is automatically updating them each time an address is entered).</span></span> <span data-ttu-id="c9559-152">할 일이 Html.Hidden() 도우미 메서드를 사용 하 여 Html.TextBox() HTML 도우미를 사용 하 여 전환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-152">To-do this we'll switch from using the Html.TextBox() HTML helper to using the Html.Hidden() helper method:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample5.aspx)]

<span data-ttu-id="c9559-153">및 이제는 폼은 좀 더 친숙 하 고 원시 위도/경도 (여전히 데이터베이스에서 각 저녁 식사를 사용 하 여 저장) 동안 표시 되지 않도록:</span><span class="sxs-lookup"><span data-stu-id="c9559-153">And now our forms are a little more user-friendly and avoid displaying the raw latitude/longitude (while still storing them with each Dinner in the database):</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image5.png)

### <a name="integrating-the-map-with-the-details-view"></a><span data-ttu-id="c9559-154">세부 정보 보기와 지도 통합</span><span class="sxs-lookup"><span data-stu-id="c9559-154">Integrating the Map with the Details View</span></span>

<span data-ttu-id="c9559-155">이제는 보겠습니다 만들기 및 편집 시나리오를 사용 하 여 통합 하는 지도 세부 정보 시나리오를 사용 하 여 통합할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-155">Now that we have the map integrated with our Create and Edit scenarios, let's also integrate it with our Details scenario.</span></span> <span data-ttu-id="c9559-156">모든 할 일을 먼저 호출 하는 것 &lt;Html.RenderPartial("map") %; %&gt; 세부 정보 보기 내에서.</span><span class="sxs-lookup"><span data-stu-id="c9559-156">All we need to-do is to call &lt;% Html.RenderPartial("map"); %&gt; within the Details view.</span></span>

<span data-ttu-id="c9559-157">전체 세부 정보 보기 (맵 통합)을 소스 코드의 모양을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-157">Below is what the source code to the complete Details view (with map integration) looks like:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample6.aspx)]

<span data-ttu-id="c9559-158">이제 사용자가 /Dinners/세부 정보 / [id] URL로 이동할 때 보게 저녁을 지도에 dinner의 위치에 대 한 세부 정보 및 (압정-를 사용 하 여 전체 때 마우스를 가져갈 표시 dinner 제목과의 주소), RSVP fo에 대 한 AJAX 링크가 있고 r 것:</span><span class="sxs-lookup"><span data-stu-id="c9559-158">And now when a user navigates to a /Dinners/Details/[id] URL they'll see details about the dinner, the location of the dinner on the map (complete with a push-pin that when hovered over displays the title of the dinner and the address of it), and have an AJAX link to RSVP for it:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image6.png)

### <a name="implementing-location-search-in-our-database-and-repository"></a><span data-ttu-id="c9559-159">데이터베이스 및 저장소 위치 검색을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-159">Implementing Location Search in our Database and Repository</span></span>

<span data-ttu-id="c9559-160">AJAX 구현은 해제를 완료 하려면 사용자 가까이 dinners 그래픽 방식으로 검색할 수 있도록 응용 프로그램의 홈 페이지에 지도 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-160">To finish off our AJAX implementation, let's add a Map to the home page of the application that allows users to graphically search for dinners near them.</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image7.png)

<span data-ttu-id="c9559-161">효율적으로 Dinners radius 위치 기반 검색을 수행 하는 데이터베이스 및 데이터 저장소 계층 내에서 지원 구현부터 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-161">We'll begin by implementing support within our database and data repository layer to efficiently perform a location-based radius search for Dinners.</span></span> <span data-ttu-id="c9559-162">사용 하 여 새 [SQL 2008의 지리 공간 기능](https://www.microsoft.com/sqlserver/2008/en/us/spatial-data.aspx) 이 구현 하려면 Gary 드 라이덴 문서에서 설명 하는 SQL 함수 방법을 사용할 수 있습니다 또는 또는: [ http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx ](http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx) 한 Rob Conery LINQ to SQL 사용 하 여 여기서 사용 하는 방법에 대 한 블로그 게시물을 올렸습니다. [http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/](http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/)</span><span class="sxs-lookup"><span data-stu-id="c9559-162">We could use the new [geospatial features of SQL 2008](https://www.microsoft.com/sqlserver/2008/en/us/spatial-data.aspx) to implement this, or alternatively we can use a SQL function approach that Gary Dryden discussed in article here: [http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx](http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx) and Rob Conery blogged about using with LINQ to SQL here: [http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/](http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/)</span></span>

<span data-ttu-id="c9559-163">이 기법을 구현 하려면에서는 Visual Studio 내에서 "서버 탐색기", NerdDinner 데이터베이스를 선택 하 고 그 아래에서 "함수" 하위 노드를 마우스 오른쪽 단추로 클릭 열리고 새 "스칼라 반환 함수 만들기"를 선택:</span><span class="sxs-lookup"><span data-stu-id="c9559-163">To implement this technique, we will open the "Server Explorer" within Visual Studio, select the NerdDinner database, and then right-click on the "functions" sub-node under it and choose to create a new "Scalar-valued function":</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image8.png)

<span data-ttu-id="c9559-164">그런 다음 다음 DistanceBetween 함수에 붙여 넣고:</span><span class="sxs-lookup"><span data-stu-id="c9559-164">We'll then paste in the following DistanceBetween function:</span></span>

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample7.sql)]

<span data-ttu-id="c9559-165">그런 다음 새 테이블 반환 함수 "NearestDinners" 이라고 하는 SQL Server에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-165">We'll then create a new table-valued function in SQL Server that we'll call "NearestDinners":</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image9.png)

<span data-ttu-id="c9559-166">이 "NearestDinners" 테이블 함수 DistanceBetween 도우미 함수를 사용 하 여 위도의 100 마일 내 모든 Dinners를 반환 하 고 제공 했습니다 경도:</span><span class="sxs-lookup"><span data-stu-id="c9559-166">This "NearestDinners" table function uses the DistanceBetween helper function to return all Dinners within 100 miles of the latitude and longitude we supply it:</span></span>

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample8.sql)]

<span data-ttu-id="c9559-167">이 함수를 호출 하려면에서는 먼저 엽니다 LINQ to SQL 디자이너 우리의 \Models 디렉터리 내 NerdDinner.dbml 파일을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-167">To call this function, we'll first open up the LINQ to SQL designer by double-clicking on the NerdDinner.dbml file within our \Models directory:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image10.png)

<span data-ttu-id="c9559-168">에서는에서는 그런 다음 끕니다. NearestDinners 및 DistanceBetween 함수를 LINQ to SQL 디자이너 SQL NerdDinnerDataContext 클래스에는 LINQ의 메서드로 추가 하는:</span><span class="sxs-lookup"><span data-stu-id="c9559-168">We'll then drag the NearestDinners and DistanceBetween functions onto the LINQ to SQL designer, which will cause them to be added as methods on our LINQ to SQL NerdDinnerDataContext class:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image11.png)

<span data-ttu-id="c9559-169">예정 된 반환할 NearestDinner 함수를 사용 하는 DinnerRepository 클래스 "FindByLocation" 쿼리 메서드를 노출 합니다에서는 지정 된 위치의 100 마일 내에 있는 Dinners:</span><span class="sxs-lookup"><span data-stu-id="c9559-169">We can then expose a "FindByLocation" query method on our DinnerRepository class that uses the NearestDinner function to return upcoming Dinners that are within 100 miles of the specified location:</span></span>

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample9.cs)]

### <a name="implementing-a-json-based-ajax-search-action-method"></a><span data-ttu-id="c9559-170">JSON 기반 AJAX 검색 동작 메서드를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-170">Implementing a JSON-based AJAX Search Action Method</span></span>

<span data-ttu-id="c9559-171">이제 맵을 채우는 데 사용할 수 있는 Dinner 데이터 목록을 다시 반환할 새 FindByLocation() 리포지토리 메서드를 활용 하는 컨트롤러 동작 메서드에 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-171">We'll now implement a controller action method that takes advantage of the new FindByLocation() repository method to return back a list of Dinner data that can be used to populate a map.</span></span> <span data-ttu-id="c9559-172">이 동작 메서드에 다시 데이터를 반환할 Dinner JSON (JavaScript Object Notation) 형식으로 쉽게 조작할 수 JavaScript를 사용 하 여 클라이언트에 있도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-172">We'll have this action method return back the Dinner data in a JSON (JavaScript Object Notation) format so that it can be easily manipulated using JavaScript on the client.</span></span>

<span data-ttu-id="c9559-173">이 구현 하려면 만들겠습니다 새 "SearchController" 클래스 \Controllers 디렉터리를 마우스 오른쪽 단추로 클릭 하 고 추가-선택 하 여&gt;컨트롤러 메뉴 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-173">To implement this, we'll create a new "SearchController" class by right-clicking on the \Controllers directory and choosing the Add-&gt;Controller menu command.</span></span> <span data-ttu-id="c9559-174">그런 다음 아래와 같이 새 SearchController 클래스 내에서 "SearchByLocation" 동작 메서드를 구현 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-174">We'll then implement a "SearchByLocation" action method within the new SearchController class like below:</span></span>

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample10.cs)]

<span data-ttu-id="c9559-175">내부적으로 SearchController의 SearchByLocation 작업 메서드는 주변 dinners의 목록을 가져오려면 DinnerRespository에 FindByLocation 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-175">The SearchController's SearchByLocation action method internally calls the FindByLocation method on DinnerRespository to get a list of nearby dinners.</span></span> <span data-ttu-id="c9559-176">클라이언트에 직접 Dinner 개체를 반환, 보다는 하지만 그 대신 JsonDinner 개체 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-176">Rather than return the Dinner objects directly to the client, though, it instead returns JsonDinner objects.</span></span> <span data-ttu-id="c9559-177">저녁 식사 속성 하위 집합을 노출 하는 JsonDinner 클래스 (예: 보안상의 이유로 저녁 주최 있는 사람의 이름을 공개 하지 않습니다).</span><span class="sxs-lookup"><span data-stu-id="c9559-177">The JsonDinner class exposes a subset of Dinner properties (for example: for security reasons it doesn't disclose the names of the people who have RSVP'd for a dinner).</span></span> <span data-ttu-id="c9559-178">또한 Dinner – 존재 하지 않는 한 특정 dinner 연관 RSVP 개체의 수를 계산 하 여 동적으로 계산 되는 RSVPCount 속성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-178">It also includes an RSVPCount property that doesn't exist on Dinner– and which is dynamically calculated by counting the number of RSVP objects associated with a particular dinner.</span></span>

<span data-ttu-id="c9559-179">다음 컨트롤러 기본 클래스에서 Json() 도우미 메서드를 사용 하 여 dinners JSON 기반 통신 형식을 사용 하 여 시퀀스를 반환 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-179">We are then using the Json() helper method on the Controller base class to return the sequence of dinners using a JSON-based wire format.</span></span> <span data-ttu-id="c9559-180">JSON은 간단한 데이터 구조를 나타내기 위한 표준 텍스트 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-180">JSON is a standard text format for representing simple data-structures.</span></span> <span data-ttu-id="c9559-181">다음은 두 JsonDinner 개체의 JSON 형식 목록을 모양은 우리의 동작 메서드에서 반환 되는 경우의 예:</span><span class="sxs-lookup"><span data-stu-id="c9559-181">Below is an example of what a JSON-formatted list of two JsonDinner objects looks like when returned from our action method:</span></span>

[!code-json[Main](use-ajax-to-implement-mapping-scenarios/samples/sample11.json)]

### <a name="calling-the-json-based-ajax-method-using-jquery"></a><span data-ttu-id="c9559-182">JQuery를 사용 하는 JSON 기반 AJAX 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-182">Calling the JSON-based AJAX method using jQuery</span></span>

<span data-ttu-id="c9559-183">이제 SearchController의 SearchByLocation 동작 메서드를 사용 하 여 NerdDinner 응용 프로그램의 홈 페이지를 업데이트할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-183">We are now ready to update the home page of the NerdDinner application to use the SearchController's SearchByLocation action method.</span></span> <span data-ttu-id="c9559-184">할 일이 /Views/Home/Index.aspx 보기 템플릿을 열려면에서는 고 textbox, 검색 단추, 우리의 맵 업데이트와 &lt;div&gt; dinnerList 이라는 요소:</span><span class="sxs-lookup"><span data-stu-id="c9559-184">To-do this, we'll open the /Views/Home/Index.aspx view template and update it to have a textbox, search button, our map, and a &lt;div&gt; element named dinnerList:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample12.aspx)]

<span data-ttu-id="c9559-185">다음 페이지에 두 개의 JavaScript 함수를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-185">We can then add two JavaScript functions to the page:</span></span>

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample13.html)]

<span data-ttu-id="c9559-186">페이지가 처음 로드 하는 경우 지도 로드 하는 첫 번째 JavaScript 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-186">The first JavaScript function loads the map when the page first loads.</span></span> <span data-ttu-id="c9559-187">JavaScript 두 번째 JavaScript 함수 와이어 이벤트 처리기 [검색] 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-187">The second JavaScript function wires up a JavaScript click event handler on the search button.</span></span> <span data-ttu-id="c9559-188">단추를 누르면 Map.js 파일을 추가 하는 FindDinnersGivenLocation() JavaScript 함수를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-188">When the button is pressed it calls the FindDinnersGivenLocation() JavaScript function which we'll add to our Map.js file:</span></span>

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample14.js)]

<span data-ttu-id="c9559-189">이 FindDinnersGivenLocation() 함수 지도 호출합니다. 입력 한 위치에 가운데 Virtual Earth 컨트롤에서 find ().</span><span class="sxs-lookup"><span data-stu-id="c9559-189">This FindDinnersGivenLocation() function calls map.Find() on the Virtual Earth Control to center it on the entered location.</span></span> <span data-ttu-id="c9559-190">Virtual earth 맵 서비스 반환 될 때 지도입니다. Find () 메서드를 마지막 인수로 전달 callbackUpdateMapDinners 콜백 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-190">When the virtual earth map service returns, the map.Find() method invokes the callbackUpdateMapDinners callback method we passed it as the final argument.</span></span>

<span data-ttu-id="c9559-191">CallbackUpdateMapDinners() 방법은 실제 작업은 수행 하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-191">The callbackUpdateMapDinners() method is where the real work is done.</span></span> <span data-ttu-id="c9559-192">JQuery의 $.post() 도우미 메서드를 사용 하 여 위 도와 경도 새로 가운데 맵의 전달이 SearchController SearchByLocation() 동작 메서드에 – AJAX 호출을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-192">It uses jQuery's $.post() helper method to perform an AJAX call to our SearchController's SearchByLocation() action method – passing it the latitude and longitude of the newly centered map.</span></span> <span data-ttu-id="c9559-193">$.Post() 도우미 메서드가 완료 되 면 호출 되는 인라인 함수 정의 및 작업 메서드에 전달 될 "dinners" 라는 변수를 사용 하 여 SearchByLocation()에서 dinner JSON 형식의 결과가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-193">It defines an inline function that will be called when the $.post() helper method completes, and the JSON-formatted dinner results returned from the SearchByLocation() action method will be passed it using a variable called "dinners".</span></span> <span data-ttu-id="c9559-194">반환 된 각 저녁을 통해 foreach를 수행 하 고 dinner의 위도 및 경도 및 기타 속성을 사용 하 여 지도에 새 pin을를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-194">It then does a foreach over each returned dinner, and uses the dinner's latitude and longitude and other properties to add a new pin on the map.</span></span> <span data-ttu-id="c9559-195">또한 맵의 오른쪽 dinners HTML 목록을 dinner 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-195">It also adds a dinner entry to the HTML list of dinners to the right of the map.</span></span> <span data-ttu-id="c9559-196">이 다음 와이어 접속 가리키기 이벤트가 압정와 HTML 목록에 대 한 사용자 위로 가져갈 때 dinner에 대 한 세부 정보 표시 되도록:</span><span class="sxs-lookup"><span data-stu-id="c9559-196">It then wires-up a hover event for both the pushpins and the HTML list so that details about the dinner are displayed when a user hovers over them:</span></span>

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample15.html)]

<span data-ttu-id="c9559-197">및 이제 응용 프로그램을 실행 하 고 맵을 사용 하 여 표시 됩니다 것 홈 페이지 방문 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-197">And now when we run the application and visit the home-page we'll be presented with a map.</span></span> <span data-ttu-id="c9559-198">도시 이름을 입력할 때 근처 향후 dinners 지도 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-198">When we enter the name of a city the map will display the upcoming dinners near it:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image12.png)

<span data-ttu-id="c9559-199">저녁 식사를 마우스로 가리키면 세부 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-199">Hovering over a dinner will display details about it.</span></span>

<span data-ttu-id="c9559-200">Dinner 제목을 클릭 거품 또는 오른쪽에 있는 HTML 목록에는 이동할 우리 dinner –에서는 수 다음 필요에 따라 참석 여부 알림 요청:</span><span class="sxs-lookup"><span data-stu-id="c9559-200">Clicking the Dinner title either in the bubble or on the right-hand side in the HTML list will navigate us to the dinner – which we can then optionally RSVP for:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image13.png)

### <a name="next-step"></a><span data-ttu-id="c9559-201">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c9559-201">Next Step</span></span>

<span data-ttu-id="c9559-202">이제 NerdDinner 응용 프로그램의 모든 응용 프로그램 기능을 구현 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-202">We've now implemented all the application functionality of our NerdDinner application.</span></span> <span data-ttu-id="c9559-203">보겠습니다 이제 자동화 단위 수는 방법을 살펴보겠습니다도 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9559-203">Let's now look at how we can enable automated unit testing of it.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c9559-204">[이전](use-ajax-to-deliver-dynamic-updates.md)
> [다음](enable-automated-unit-testing.md)</span><span class="sxs-lookup"><span data-stu-id="c9559-204">[Previous](use-ajax-to-deliver-dynamic-updates.md)
[Next](enable-automated-unit-testing.md)</span></span>
