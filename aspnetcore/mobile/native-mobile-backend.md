---
title: ASP.NET Core를 사용하여 네이티브 모바일 앱용 백 엔드 서비스 만들기
author: ardalis
description: ASP.NET Core MVC를 사용하여 네이티브 모바일 앱을 지원하는 백 엔드 서비스를 만드는 방법을 배웁니다.
manager: wpickett
ms.author: riande
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: mobile/native-mobile-backend
ms.openlocfilehash: 18aecea00eb9cda3462ede7e478616a99cf302f8
ms.sourcegitcommit: 48beecfe749ddac52bc79aa3eb246a2dcdaa1862
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
ms.locfileid: "30073180"
---
# <a name="create-backend-services-for-native-mobile-apps-with-aspnet-core"></a><span data-ttu-id="00c13-103">ASP.NET Core를 사용하여 네이티브 모바일 앱용 백 엔드 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="00c13-103">Create backend services for native mobile apps with ASP.NET Core</span></span>

<span data-ttu-id="00c13-104">작성자: [Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="00c13-104">By [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="00c13-105">모바일 앱은 ASP.NET Core 백 엔드 서비스와 쉽게 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-105">Mobile apps can easily communicate with ASP.NET Core backend services.</span></span>

[<span data-ttu-id="00c13-106">샘플 백 엔드 서비스 코드 보기 및 다운로드</span><span class="sxs-lookup"><span data-stu-id="00c13-106">View or download sample backend services code</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/mobile/native-mobile-backend/sample)

## <a name="the-sample-native-mobile-app"></a><span data-ttu-id="00c13-107">샘플 네이티브 모바일 앱</span><span class="sxs-lookup"><span data-stu-id="00c13-107">The Sample Native Mobile App</span></span>

<span data-ttu-id="00c13-108">이 자습서에서는 네이티브 모바일 앱을 지원하기 위해 ASP.NET Core MVC를 사용하여 백 엔드 서비스를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-108">This tutorial demonstrates how to create backend services using ASP.NET Core MVC to support native mobile apps.</span></span> <span data-ttu-id="00c13-109">Android, iOS, Windows 유니버설 및 Window Phone 장치에 대한 별도 네이티브 클라이언트를 포함하는 네이티브 클라이언트로 [Xamarin Forms ToDoRest 앱](/xamarin/xamarin-forms/data-cloud/consuming/rest)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-109">It uses the [Xamarin Forms ToDoRest app](/xamarin/xamarin-forms/data-cloud/consuming/rest) as its native client, which includes separate native clients for Android, iOS, Windows Universal, and Window Phone devices.</span></span> <span data-ttu-id="00c13-110">연결된 자습서를 따라 네이티브 앱을 만들고(필요한 무료 Xamarin 도구 설치) Xamarin 샘플 솔루션을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-110">You can follow the linked tutorial to create the native app (and install the necessary free Xamarin tools), as well as download the Xamarin sample solution.</span></span> <span data-ttu-id="00c13-111">Xamarin 샘플에는 이 문서의 ASP.NET Core 앱이 바꾸는 ASP.NET Web API 2 서비스 프로젝트가 포함되어 있습니다(클라이언트에서 필요한 변경 내용 없이).</span><span class="sxs-lookup"><span data-stu-id="00c13-111">The Xamarin sample includes an ASP.NET Web API 2 services project, which this article's ASP.NET Core app replaces (with no changes required by the client).</span></span>

![Android 스마트폰에서 실행되는 To Do Rest 응용 프로그램](native-mobile-backend/_static/todo-android.png)

### <a name="features"></a><span data-ttu-id="00c13-113">기능</span><span class="sxs-lookup"><span data-stu-id="00c13-113">Features</span></span>

<span data-ttu-id="00c13-114">ToDoRest 앱은 할 일 항목 나열, 추가, 삭제 및 업데이트를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-114">The ToDoRest app supports listing, adding, deleting, and updating To-Do items.</span></span> <span data-ttu-id="00c13-115">각 항목에는 ID, 이름, 메모 및 완료되었는지 여부를 나타내는 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-115">Each item has an ID, a Name, Notes, and a property indicating whether it's been Done yet.</span></span>

<span data-ttu-id="00c13-116">위에 표시된 것처럼 항목의 주 보기는 각 항목의 이름을 나열하고 확인 표시로 완료되었는지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-116">The main view of the items, as shown above, lists each item's name and indicates if it's done with a checkmark.</span></span>

<span data-ttu-id="00c13-117">`+` 아이콘을 누르면 항목 추가 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-117">Tapping the `+` icon opens an add item dialog:</span></span>

![항목 추가 대화 상자](native-mobile-backend/_static/todo-android-new-item.png)

<span data-ttu-id="00c13-119">기본 목록 화면에서 항목을 누르면 항목의 이름, 메모 및 완료 설정을 수정할 수 있거나 항목을 삭제할 수 있는 편집 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-119">Tapping an item on the main list screen opens up an edit dialog where the item's Name, Notes, and Done settings can be modified, or the item can be deleted:</span></span>

![항목 편집 대화 상자](native-mobile-backend/_static/todo-android-edit-item.png)

<span data-ttu-id="00c13-121">이 샘플은 기본적으로 읽기 전용 작업을 허용하는 developer.xamarin.com에서 호스팅되는 백 엔드 서비스를 사용하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-121">This sample is configured by default to use backend services hosted at developer.xamarin.com, which allow read-only operations.</span></span> <span data-ttu-id="00c13-122">컴퓨터에서 실행되는 다음 섹션에서 만든 ASP.NET Core 앱을 직접 테스트하려면 앱의 `RestUrl` 상수를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-122">To test it out yourself against the ASP.NET Core app created in the next section running on your computer, you'll need to update the app's `RestUrl` constant.</span></span> <span data-ttu-id="00c13-123">`ToDoREST` 프로젝트로 이동하고 *Constants.cs* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-123">Navigate to the `ToDoREST` project and open the *Constants.cs* file.</span></span> <span data-ttu-id="00c13-124">`RestUrl`을 컴퓨터의 IP 주소를 포함하는 URL로 바꿉니다(이 주소는 컴퓨터에서가 아니라 장치 에뮬레이터에서 사용되므로 localhost 또는 127.0.0.1이 아님).</span><span class="sxs-lookup"><span data-stu-id="00c13-124">Replace the `RestUrl` with a URL that includes your machine's IP address (not localhost or 127.0.0.1, since this address is used from the device emulator, not from your machine).</span></span> <span data-ttu-id="00c13-125">포트 번호도 포함합니다(5000).</span><span class="sxs-lookup"><span data-stu-id="00c13-125">Include the port number as well (5000).</span></span> <span data-ttu-id="00c13-126">서비스가 장치와 작동하는지 테스트하기 위해 이 포트에 대한 액세스를 차단하는 활성 방화벽이 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-126">In order to test that your services work with a device, ensure you don't have an active firewall blocking access to this port.</span></span>

```csharp
// URL of REST service (Xamarin ReadOnly Service)
//public static string RestUrl = "http://developer.xamarin.com:8081/api/todoitems{0}";

// use your machine's IP address
public static string RestUrl = "http://192.168.1.207:5000/api/todoitems/{0}";
```

## <a name="creating-the-aspnet-core-project"></a><span data-ttu-id="00c13-127">ASP.NET Core 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="00c13-127">Creating the ASP.NET Core Project</span></span>

<span data-ttu-id="00c13-128">Visual Studio에서 새 ASP.NET Core 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-128">Create a new ASP.NET Core Web Application in Visual Studio.</span></span> <span data-ttu-id="00c13-129">웹 API 템플릿과 인증 안 함을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-129">Choose the Web API template and No Authentication.</span></span> <span data-ttu-id="00c13-130">프로젝트 이름을 *ToDoApi*로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-130">Name the project *ToDoApi*.</span></span>

![Web API 프로젝트 템플릿이 선택된 새 ASP.NET 웹 응용 프로그램 대화 상자](native-mobile-backend/_static/web-api-template.png)

<span data-ttu-id="00c13-132">응용 프로그램은 포트 5000에 대한 모든 요청에 응답해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-132">The application should respond to all requests made to port 5000.</span></span> <span data-ttu-id="00c13-133">이를 수행하기 위해 `.UseUrls("http://*:5000")`를 포함하도록 *Program.cs*를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-133">Update *Program.cs* to include `.UseUrls("http://*:5000")` to achieve this:</span></span>

[!code-csharp[](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Program.cs?range=10-16&highlight=3)]

> [!NOTE]
> <span data-ttu-id="00c13-134">기본적으로 로컬이 아닌 요청을 무시하는 IIS Express 뒤에서보다 응용 프로그램을 직접 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-134">Make sure you run the application directly, rather than behind IIS Express, which ignores non-local requests by default.</span></span> <span data-ttu-id="00c13-135">명령 프롬프트에서 [dotnet run](/dotnet/core/tools/dotnet-run)을 실행하거나 Visual Studio 도구 모음의 디버그 대상 드롭다운에서 응용 프로그램 이름 프로필을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-135">Run [dotnet run](/dotnet/core/tools/dotnet-run) from a command prompt, or choose the application name profile from the Debug Target dropdown in the Visual Studio toolbar.</span></span>

<span data-ttu-id="00c13-136">할 일 항목을 나타내도록 모델 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-136">Add a model class to represent To-Do items.</span></span> <span data-ttu-id="00c13-137">`[Required]` 특성을 사용하여 필수 필드를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-137">Mark required fields using the `[Required]` attribute:</span></span>

[!code-csharp[](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Models/ToDoItem.cs)]

<span data-ttu-id="00c13-138">API 메서드에는 데이터를 사용하는 방법이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-138">The API methods require some way to work with data.</span></span> <span data-ttu-id="00c13-139">원래 Xamarin 샘플에서 사용하는 동일한 `IToDoRepository` 인터페이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-139">Use the same `IToDoRepository` interface the original Xamarin sample uses:</span></span>

[!code-csharp[](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Interfaces/IToDoRepository.cs)]

<span data-ttu-id="00c13-140">이 샘플의 경우 구현은 항목의 개별 컬렉션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-140">For this sample, the implementation just uses a private collection of items:</span></span>

[!code-csharp[](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Services/ToDoRepository.cs)]

<span data-ttu-id="00c13-141">*Startup.cs*에서 구현을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-141">Configure the implementation in *Startup.cs*:</span></span>

[!code-csharp[](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Startup.cs?highlight=6&range=29-35)]

<span data-ttu-id="00c13-142">이 시점에서 *ToDoItemsController*를 만들 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-142">At this point, you're ready to create the *ToDoItemsController*.</span></span>

> [!TIP]
> <span data-ttu-id="00c13-143">[ASP.NET Core MVC 및 Visual Studio를 사용하여 첫 번째 Web API 빌드](../tutorials/first-web-api.md)에서 Web API를 만드는 방법에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-143">Learn more about creating web APIs in [Build your first Web API with ASP.NET Core MVC and Visual Studio](../tutorials/first-web-api.md).</span></span>

## <a name="creating-the-controller"></a><span data-ttu-id="00c13-144">컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="00c13-144">Creating the Controller</span></span>

<span data-ttu-id="00c13-145">프로젝트에 새 컨트롤러, *ToDoItemsController*를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-145">Add a new controller to the project, *ToDoItemsController*.</span></span> <span data-ttu-id="00c13-146">Microsoft.AspNetCore.Mvc.Controller에서 상속해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-146">It should inherit from Microsoft.AspNetCore.Mvc.Controller.</span></span> <span data-ttu-id="00c13-147">`Route` 특성을 추가하여 컨트롤러에서 `api/todoitems`로 시작하는 경로에 대해 만든 요청을 처리하는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-147">Add a `Route` attribute to indicate that the controller will handle requests made to paths starting with `api/todoitems`.</span></span> <span data-ttu-id="00c13-148">경로의 `[controller]` 토큰은 컨트롤러의 이름으로 대체되며(`Controller` 접미사 생략) 글로벌 경로에 대해 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-148">The `[controller]` token in the route is replaced by the name of the controller (omitting the `Controller` suffix), and is especially helpful for global routes.</span></span> <span data-ttu-id="00c13-149">[라우팅](../fundamentals/routing.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-149">Learn more about [routing](../fundamentals/routing.md).</span></span>

<span data-ttu-id="00c13-150">컨트롤러는 작동하기 위해 `IToDoRepository`가 필요합니다. 컨트롤러의 생성자를 통해 이 유형의 인스턴스를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-150">The controller requires an `IToDoRepository` to function; request an instance of this type through the controller's constructor.</span></span> <span data-ttu-id="00c13-151">런타임 시 이 인스턴스는 [종속성 주입](../fundamentals/dependency-injection.md)에 대한 프레임워크의 지원을 사용하여 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-151">At runtime, this instance will be provided using the framework's support for [dependency injection](../fundamentals/dependency-injection.md).</span></span>

[!code-csharp[](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Controllers/ToDoItemsController.cs?range=1-17&highlight=9,14)]

<span data-ttu-id="00c13-152">이 API는 데이터 원본에서 CRUD(만들기, 읽기, 업데이트, 삭제) 작업을 수행하도록 4개의 다른 HTTP 동사를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-152">This API supports four different HTTP verbs to perform CRUD (Create, Read, Update, Delete) operations on the data source.</span></span> <span data-ttu-id="00c13-153">이 중 가장 간단한 것은 HTTP GET 요청에 해당하는 읽기 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-153">The simplest of these is the Read operation, which corresponds to an HTTP GET request.</span></span>

### <a name="reading-items"></a><span data-ttu-id="00c13-154">항목 읽기</span><span class="sxs-lookup"><span data-stu-id="00c13-154">Reading Items</span></span>

<span data-ttu-id="00c13-155">항목의 목록 요청은 `List` 메서드에 대한 GET 요청으로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-155">Requesting a list of items is done with a GET request to the `List` method.</span></span> <span data-ttu-id="00c13-156">`List` 메서드의 `[HttpGet]` 특성은 이 작업이 GET 요청만을 처리해야 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-156">The `[HttpGet]` attribute on the `List` method indicates that this action should only handle GET requests.</span></span> <span data-ttu-id="00c13-157">이 작업에 대한 경로는 컨트롤러에 지정된 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-157">The route for this action is the route specified on the controller.</span></span> <span data-ttu-id="00c13-158">경로의 일부로 작업 이름을 사용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-158">You don't necessarily need to use the action name as part of the route.</span></span> <span data-ttu-id="00c13-159">각 작업에 고유하고 명확한 경로가 있도록 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-159">You just need to ensure each action has a unique and unambiguous route.</span></span> <span data-ttu-id="00c13-160">라우팅 특성은 특정 경로를 작성하도록 컨트롤러와 메서드 수준 모두에 적용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-160">Routing attributes can be applied at both the controller and method levels to build up specific routes.</span></span>

[!code-csharp[](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Controllers/ToDoItemsController.cs?range=19-23)]

<span data-ttu-id="00c13-161">`List` 메서드는 200 정상 응답 코드와 JSON으로 직렬화된 모든 할 일 항목을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-161">The `List` method returns a 200 OK response code and all of the ToDo items, serialized as JSON.</span></span>

<span data-ttu-id="00c13-162">여기에 표시된 [Postman](https://www.getpostman.com/docs/)과 같은 다양한 도구를 사용하여 새 API 메서드를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-162">You can test your new API method using a variety of tools, such as [Postman](https://www.getpostman.com/docs/), shown here:</span></span>

![할 일 항목에 대한 GET 요청을 보여 주는 Postman 콘솔 및 반환되는 세 가지 항목에 대한 JSON을 보여 주는 응답의 본문](native-mobile-backend/_static/postman-get.png)

### <a name="creating-items"></a><span data-ttu-id="00c13-164">항목 만들기</span><span class="sxs-lookup"><span data-stu-id="00c13-164">Creating Items</span></span>

<span data-ttu-id="00c13-165">일반적으로 새 데이터 항목 만들기는 HTTP POST 동사로 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-165">By convention, creating new data items is mapped to the HTTP POST verb.</span></span> <span data-ttu-id="00c13-166">`Create` 메서드에는 적용된 `[HttpPost]` 특성이 있으며 `ToDoItem` 인스턴스를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-166">The `Create` method has an `[HttpPost]` attribute applied to it, and accepts a `ToDoItem` instance.</span></span> <span data-ttu-id="00c13-167">`item` 인수는 POST의 본문에 전달되므로 이 매개 변수는 `[FromBody]` 특성으로 데코레이팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-167">Since the `item` argument will be passed in the body of the POST, this parameter is decorated with the `[FromBody]` attribute.</span></span>

<span data-ttu-id="00c13-168">메서드 내부에서 유효성 및 데이터 저장소의 이전 존재에 대해 항목이 선택되며 문제가 발생하지 않는 경우 리포지토리를 사용하여 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-168">Inside the method, the item is checked for validity and prior existence in the data store, and if no issues occur, it's added using the repository.</span></span> <span data-ttu-id="00c13-169">`ModelState.IsValid`를 확인하면 [모델 유효성 검사](../mvc/models/validation.md)를 수행하고, 사용자 입력을 허용하는 모든 API 메서드에서 수행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-169">Checking `ModelState.IsValid` performs [model validation](../mvc/models/validation.md), and should be done in every API method that accepts user input.</span></span>

[!code-csharp[](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Controllers/ToDoItemsController.cs?range=25-46)]

<span data-ttu-id="00c13-170">샘플은 모바일 클라이언트에 전달되는 오류 코드를 포함하는 열거형을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-170">The sample uses an enum containing error codes that are passed to the mobile client:</span></span>

[!code-csharp[](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Controllers/ToDoItemsController.cs?range=91-99)]

<span data-ttu-id="00c13-171">요청의 본문에 JSON 형식의 새 개체를 제공하는 POST 동사를 선택하여 Postman을 사용하는 새 항목 추가를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-171">Test adding new items using Postman by choosing the POST verb providing the new object in JSON format in the Body of the request.</span></span> <span data-ttu-id="00c13-172">또한 `application/json`의 `Content-Type`을 지정하는 요청 헤더를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-172">You should also add a request header specifying a `Content-Type` of `application/json`.</span></span>

![POST 및 응답을 보여 주는 Postman 콘솔](native-mobile-backend/_static/postman-post.png)

<span data-ttu-id="00c13-174">메서드는 응답에서 새로 만든 항목을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-174">The method returns the newly created item in the response.</span></span>

### <a name="updating-items"></a><span data-ttu-id="00c13-175">항목 업데이트</span><span class="sxs-lookup"><span data-stu-id="00c13-175">Updating Items</span></span>

<span data-ttu-id="00c13-176">레코드 수정은 HTTP PUT 요청을 사용하여 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-176">Modifying records is done using HTTP PUT requests.</span></span> <span data-ttu-id="00c13-177">이 변경 외에 `Edit` 메서드는 `Create`와 거의 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-177">Other than this change, the `Edit` method is almost identical to `Create`.</span></span> <span data-ttu-id="00c13-178">레코드를 찾을 수 없는 경우 `Edit` 작업은 `NotFound`(404) 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-178">Note that if the record isn't found, the `Edit` action will return a `NotFound` (404) response.</span></span>

[!code-csharp[](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Controllers/ToDoItemsController.cs?range=48-69)]

<span data-ttu-id="00c13-179">Postman으로 테스트하려면 동사를 PUT으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-179">To test with Postman, change the verb to PUT.</span></span> <span data-ttu-id="00c13-180">요청의 본문에서 업데이트된 개체 데이터를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-180">Specify the updated object data in the Body of the request.</span></span>

![PUT 및 응답을 보여 주는 Postman 콘솔](native-mobile-backend/_static/postman-put.png)

<span data-ttu-id="00c13-182">이 메서드는 성공한 경우 기존 API와의 일관성을 위해 `NoContent`(204) 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-182">This method returns a `NoContent` (204) response when successful, for consistency with the pre-existing API.</span></span>

### <a name="deleting-items"></a><span data-ttu-id="00c13-183">항목 삭제</span><span class="sxs-lookup"><span data-stu-id="00c13-183">Deleting Items</span></span>

<span data-ttu-id="00c13-184">레코드 삭제는 서비스에 대해 DELETE 요청을 만들고, 삭제될 항목의 ID를 전달하여 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-184">Deleting records is accomplished by making DELETE requests to the service, and passing the ID of the item to be deleted.</span></span> <span data-ttu-id="00c13-185">업데이트를 사용하면 존재하지 않는 항목에 대한 요청은 `NotFound` 응답을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-185">As with updates, requests for items that don't exist will receive `NotFound` responses.</span></span> <span data-ttu-id="00c13-186">그렇지 않으면 성공한 요청은 `NoContent`(204) 응답을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-186">Otherwise, a successful request will get a `NoContent` (204) response.</span></span>

[!code-csharp[](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Controllers/ToDoItemsController.cs?range=71-88)]

<span data-ttu-id="00c13-187">삭제 기능을 테스트할 때 요청의 본문에 아무 것도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-187">Note that when testing the delete functionality, nothing is required in the Body of the request.</span></span>

![DELETE 및 응답을 보여 주는 Postman 콘솔](native-mobile-backend/_static/postman-delete.png)

## <a name="common-web-api-conventions"></a><span data-ttu-id="00c13-189">공통 Web API 규칙</span><span class="sxs-lookup"><span data-stu-id="00c13-189">Common Web API Conventions</span></span>

<span data-ttu-id="00c13-190">앱에 대해 백 엔드 서비스를 개발하는 경우 교차 편집 문제 처리를 위해 일관적인 규칙의 집합 또는 정책을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-190">As you develop the backend services for your app, you will want to come up with a consistent set of conventions or policies for handling cross-cutting concerns.</span></span> <span data-ttu-id="00c13-191">예를 들어 위에 표시된 서비스에서 발견되지 않았던 특정 레코드에 대한 요청은 `BadRequest` 응답 대신 `NotFound` 응답을 받았습니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-191">For example, in the service shown above, requests for specific records that weren't found received a `NotFound` response, rather than a `BadRequest` response.</span></span> <span data-ttu-id="00c13-192">마찬가지로, 모델 바인딩 형식을 전달한 이 서비스에 대해 만든 명령은 항상 `ModelState.IsValid`를 확인했고 잘못된 모델 유형에 대해 `BadRequest`를 반환했습니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-192">Similarly, commands made to this service that passed in model bound types always checked `ModelState.IsValid` and returned a `BadRequest` for invalid model types.</span></span>

<span data-ttu-id="00c13-193">API에 대한 일반적인 정책을 식별했으면 [필터](../mvc/controllers/filters.md)에서 캡슐화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-193">Once you've identified a common policy for your APIs, you can usually encapsulate it in a [filter](../mvc/controllers/filters.md).</span></span> <span data-ttu-id="00c13-194">[ASP.NET Core MVC 응용 프로그램에서 일반적인 API 정책을 캡슐화하는 방법](https://msdn.microsoft.com/magazine/mt767699.aspx)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="00c13-194">Learn more about [how to encapsulate common API policies in ASP.NET Core MVC applications](https://msdn.microsoft.com/magazine/mt767699.aspx).</span></span>
