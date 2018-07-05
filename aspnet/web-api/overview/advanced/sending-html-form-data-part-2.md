---
uid: web-api/overview/advanced/sending-html-form-data-part-2
title: 'ASP.NET Web API에서에서 HTML 양식 데이터 보내기: 파일 업로드 및 다중 파트 MIME | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/21/2012
ms.topic: article
ms.assetid: a7f3c1b5-69d9-4261-b082-19ffafa5f16a
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-2
msc.type: authoredcontent
ms.openlocfilehash: 7c1c85f462141daf747e23aa4215d47f2d263140
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37386710"
---
<a name="sending-html-form-data-in-aspnet-web-api-file-upload-and-multipart-mime"></a><span data-ttu-id="9c316-102">ASP.NET Web API에서에서 HTML 양식 데이터 보내기: 파일 업로드 및 다중 파트 MIME</span><span class="sxs-lookup"><span data-stu-id="9c316-102">Sending HTML Form Data in ASP.NET Web API: File Upload and Multipart MIME</span></span>
====================
<span data-ttu-id="9c316-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="9c316-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

## <a name="part-2-file-upload-and-multipart-mime"></a><span data-ttu-id="9c316-104">2 부: 파일 업로드 및 다중 파트 MIME</span><span class="sxs-lookup"><span data-stu-id="9c316-104">Part 2: File Upload and Multipart MIME</span></span>

<span data-ttu-id="9c316-105">이 자습서에는 웹 API에 파일을 업로드 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9c316-105">This tutorial shows how to upload files to a web API.</span></span> <span data-ttu-id="9c316-106">다중 파트 MIME 데이터를 처리 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c316-106">It also describes how to process multipart MIME data.</span></span>

> [!NOTE]
> <span data-ttu-id="9c316-107">[완료 된 프로젝트 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-API-File-Upload-a8c0fb0d)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c316-107">[Download the completed project](https://code.msdn.microsoft.com/ASPNET-Web-API-File-Upload-a8c0fb0d).</span></span>


<span data-ttu-id="9c316-108">파일을 업로드 하는 것에 대 한 HTML 폼의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9c316-108">Here is an example of an HTML form for uploading a file:</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample1.html)]

![](sending-html-form-data-part-2/_static/image1.png)

<span data-ttu-id="9c316-109">이 양식에 텍스트 입력된 컨트롤 및 파일 입력된 컨트롤을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9c316-109">This form contains a text input control and a file input control.</span></span> <span data-ttu-id="9c316-110">폼 파일 입력된 컨트롤을 포함 하는 경우는 **enctype** 특성은 항상 &quot;다중 파트/폼 데이터&quot;, 다중 파트 MIME 메시지를 폼은 보내도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c316-110">When a form contains a file input control, the **enctype** attribute should always be &quot;multipart/form-data&quot;, which specifies that the form will be sent as a multipart MIME message.</span></span>

<span data-ttu-id="9c316-111">예제 요청을 확인 하 여 이해 하기 쉬운 다중 파트 MIME 메시지의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9c316-111">The format of a multipart MIME message is easiest to understand by looking at an example request:</span></span>

[!code-console[Main](sending-html-form-data-part-2/samples/sample2.cmd)]

<span data-ttu-id="9c316-112">이 메시지 두 나뉩니다 *파트*, 각각의 양식 컨트롤에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c316-112">This message is divided into two *parts*, one for each form control.</span></span> <span data-ttu-id="9c316-113">부분 경계는 대시로 시작 하는 선으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c316-113">Part boundaries are indicated by the lines that start with dashes.</span></span>

> [!NOTE]
> <span data-ttu-id="9c316-114">임의 구성 요소를 포함 하는 부분 경계 (&quot;41184676334&quot;) 경계 문자열 메시지 파트 내에서 실수로 표시 되지 않습니다 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c316-114">The part boundary includes a random component (&quot;41184676334&quot;) to ensure that the boundary string does not accidentally appear inside a message part.</span></span>


<span data-ttu-id="9c316-115">각 메시지 파트 파트 콘텐츠에 뒤에 하나 이상의 헤더를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c316-115">Each message part contains one or more headers, followed by the part contents.</span></span>

- <span data-ttu-id="9c316-116">Content-disposition 헤더 컨트롤의 이름을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9c316-116">The Content-Disposition header includes the name of the control.</span></span> <span data-ttu-id="9c316-117">또한 파일에 대 한 파일 이름을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c316-117">For files, it also contains the file name.</span></span>
- <span data-ttu-id="9c316-118">Content-type 헤더에에서 데이터를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9c316-118">The Content-Type header describes the data in the part.</span></span> <span data-ttu-id="9c316-119">이 헤더를 생략 하면 기본값은 텍스트/일반입니다.</span><span class="sxs-lookup"><span data-stu-id="9c316-119">If this header is omitted, the default is text/plain.</span></span>

<span data-ttu-id="9c316-120">이전 예제에서는 사용자 GrandCanyon.jpg, 콘텐츠 형식이 image/jpeg; 이라는 파일을 업로드 입력 텍스트의 값이 고 &quot;여름 휴가&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="9c316-120">In the previous example, the user uploaded a file named GrandCanyon.jpg, with content type image/jpeg; and the value of the text input was &quot;Summer Vacation&quot;.</span></span>

## <a name="file-upload"></a><span data-ttu-id="9c316-121">파일 업로드</span><span class="sxs-lookup"><span data-stu-id="9c316-121">File Upload</span></span>

<span data-ttu-id="9c316-122">이제는 다중 파트 MIME 메시지에서 파일을 읽는 Web API 컨트롤러에 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9c316-122">Now let's look at a Web API controller that reads files from a multipart MIME message.</span></span> <span data-ttu-id="9c316-123">컨트롤러는 비동기적으로 파일을 읽이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c316-123">The controller will read the files asynchronously.</span></span> <span data-ttu-id="9c316-124">Web API를 사용 하 여 비동기 작업을 지원 합니다 [작업 기반 프로그래밍 모델](https://msdn.microsoft.com/library/dd460693.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c316-124">Web API supports asynchronous actions using the [task-based programming model](https://msdn.microsoft.com/library/dd460693.aspx).</span></span> <span data-ttu-id="9c316-125">먼저, 다음은 코드를 지 원하는.NET Framework 4.5를 대상으로 하는 경우는 **비동기** 하 고 **await** 키워드입니다.</span><span class="sxs-lookup"><span data-stu-id="9c316-125">First, here is the code if you are targeting .NET Framework 4.5, which supports the **async** and **await** keywords.</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample3.cs)]

<span data-ttu-id="9c316-126">알림 컨트롤러 작업 매개 변수를 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9c316-126">Notice that the controller action does not take any parameters.</span></span> <span data-ttu-id="9c316-127">미디어 유형 포맷터를 호출 하지 않고 작업 내에서 요청 본문을 처리 했습니다 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="9c316-127">That's because we process the request body inside the action, without invoking a media-type formatter.</span></span>

<span data-ttu-id="9c316-128">합니다 **IsMultipartContent** 메서드는 다중 파트 MIME 메시지를 요청에 포함 되는지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c316-128">The **IsMultipartContent** method checks whether the request contains a multipart MIME message.</span></span> <span data-ttu-id="9c316-129">그렇지 않은 경우 컨트롤러 HTTP 상태 코드 415 (지원 되지 않는 미디어 형식)를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c316-129">If not, the controller returns HTTP status code 415 (Unsupported Media Type).</span></span>

<span data-ttu-id="9c316-130">합니다 **MultipartFormDataStreamProvider** 클래스는 파일 스트림을 업로드 된 파일에 대 한 할당 하는 도우미 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="9c316-130">The **MultipartFormDataStreamProvider** class is a helper object that allocates file streams for uploaded files.</span></span> <span data-ttu-id="9c316-131">다중 파트 MIME 메시지를 읽으려면 호출을 **ReadAsMultipartAsync** 메서드.</span><span class="sxs-lookup"><span data-stu-id="9c316-131">To read the multipart MIME message, call the **ReadAsMultipartAsync** method.</span></span> <span data-ttu-id="9c316-132">이 메서드는 모든 메시지 파트를 추출 하 고 제공한 스트림으로 씁니다 합니다 **MultipartFormDataStreamProvider**합니다.</span><span class="sxs-lookup"><span data-stu-id="9c316-132">This method extracts all of the message parts and writes them into the streams provided by the **MultipartFormDataStreamProvider**.</span></span>

<span data-ttu-id="9c316-133">메서드가 완료 되 면 파일에 대 한 정보를 가져올 수 있습니다 합니다 **데이터** 컬렉션인 속성의 **MultipartFileData** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="9c316-133">When the method completes, you can get information about the files from the **FileData** property, which is a collection of **MultipartFileData** objects.</span></span>

- <span data-ttu-id="9c316-134">**MultipartFileData.FileName** 저장 된 파일 서버의 로컬 파일 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9c316-134">**MultipartFileData.FileName** is the local file name on the server, where the file was saved.</span></span>
- <span data-ttu-id="9c316-135">**MultipartFileData.Headers** 파트 헤더가 포함 되어 있습니다 (*하지* 요청 헤더).</span><span class="sxs-lookup"><span data-stu-id="9c316-135">**MultipartFileData.Headers** contains the part header (*not* the request header).</span></span> <span data-ttu-id="9c316-136">콘텐츠에 액세스 하는 데 사용할 수 있습니다\_기질 및 Content-type 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="9c316-136">You can use this to access the Content\_Disposition and Content-Type headers.</span></span>

<span data-ttu-id="9c316-137">이름에서 알 수 있듯이 **ReadAsMultipartAsync** 비동기 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="9c316-137">As the name suggests, **ReadAsMultipartAsync** is an asynchronous method.</span></span> <span data-ttu-id="9c316-138">메서드가 완료 된 후 작업을 수행 하려면 사용 된 [연속 작업이](https://msdn.microsoft.com/library/ee372288.aspx) (.NET 4.0) 또는 **await** 키워드 (.NET 4.5).</span><span class="sxs-lookup"><span data-stu-id="9c316-138">To perform work after the method completes, use a [continuation task](https://msdn.microsoft.com/library/ee372288.aspx) (.NET 4.0) or the **await** keyword (.NET 4.5).</span></span>

<span data-ttu-id="9c316-139">.NET Framework 4.0 버전 이전 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9c316-139">Here is the .NET Framework 4.0 version of the previous code:</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample4.cs)]

## <a name="reading-form-control-data"></a><span data-ttu-id="9c316-140">양식 컨트롤 데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="9c316-140">Reading Form Control Data</span></span>

<span data-ttu-id="9c316-141">앞서 있는 HTML 폼에 텍스트 입력된 컨트롤을 했습니다.</span><span class="sxs-lookup"><span data-stu-id="9c316-141">The HTML form that I showed earlier had a text input control.</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample5.html)]

<span data-ttu-id="9c316-142">컨트롤의 값을 가져올 수는 **FormData** 의 속성을 **MultipartFormDataStreamProvider**합니다.</span><span class="sxs-lookup"><span data-stu-id="9c316-142">You can get the value of the control from the **FormData** property of the **MultipartFormDataStreamProvider**.</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample6.cs?highlight=15)]

<span data-ttu-id="9c316-143">**FormData** 되는 **NameValueCollection** 폼 컨트롤에 대 한 이름/값 쌍이 포함 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c316-143">**FormData** is a **NameValueCollection** that contains name/value pairs for the form controls.</span></span> <span data-ttu-id="9c316-144">컬렉션 중복 키를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c316-144">The collection can contain duplicate keys.</span></span> <span data-ttu-id="9c316-145">이 양식을 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="9c316-145">Consider this form:</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample7.html)]

![](sending-html-form-data-part-2/_static/image2.png)

<span data-ttu-id="9c316-146">요청 본문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9c316-146">The request body might look like this:</span></span>

[!code-console[Main](sending-html-form-data-part-2/samples/sample8.cmd)]

<span data-ttu-id="9c316-147">이런 경우는 **FormData** 컬렉션에는 다음 키/값 쌍을 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c316-147">In that case, the **FormData** collection would contain the following key/value pairs:</span></span>

- <span data-ttu-id="9c316-148">여정: 라운드트립</span><span class="sxs-lookup"><span data-stu-id="9c316-148">trip: round-trip</span></span>
- <span data-ttu-id="9c316-149">옵션: nonstop</span><span class="sxs-lookup"><span data-stu-id="9c316-149">options: nonstop</span></span>
- <span data-ttu-id="9c316-150">옵션: 날짜</span><span class="sxs-lookup"><span data-stu-id="9c316-150">options: dates</span></span>
- <span data-ttu-id="9c316-151">사용자: 창</span><span class="sxs-lookup"><span data-stu-id="9c316-151">seat: window</span></span>
