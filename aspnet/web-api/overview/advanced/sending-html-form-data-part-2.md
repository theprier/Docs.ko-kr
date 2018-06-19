---
uid: web-api/overview/advanced/sending-html-form-data-part-2
title: 'ASP.NET Web API의에서 HTML 폼 데이터 보내기: 파일 업로드 및 다중 파트 MIME | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/21/2012
ms.topic: article
ms.assetid: a7f3c1b5-69d9-4261-b082-19ffafa5f16a
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-2
msc.type: authoredcontent
ms.openlocfilehash: 331d0e520a1fd8ec84aecd09a9c9e6d286c5893b
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
ms.locfileid: "28040144"
---
<a name="sending-html-form-data-in-aspnet-web-api-file-upload-and-multipart-mime"></a><span data-ttu-id="6e8e5-102">ASP.NET Web API의에서 HTML 폼 데이터 보내기: 파일 업로드 및 다중 파트 MIME</span><span class="sxs-lookup"><span data-stu-id="6e8e5-102">Sending HTML Form Data in ASP.NET Web API: File Upload and Multipart MIME</span></span>
====================
<span data-ttu-id="6e8e5-103">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="6e8e5-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

## <a name="part-2-file-upload-and-multipart-mime"></a><span data-ttu-id="6e8e5-104">2 단계: 파일 업로드 및 다중 파트 MIME</span><span class="sxs-lookup"><span data-stu-id="6e8e5-104">Part 2: File Upload and Multipart MIME</span></span>

<span data-ttu-id="6e8e5-105">이 자습서에서는 웹 API에 파일을 업로드 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6e8e5-105">This tutorial shows how to upload files to a web API.</span></span> <span data-ttu-id="6e8e5-106">또한 다중 파트 MIME 데이터를 처리 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8e5-106">It also describes how to process multipart MIME data.</span></span>

> [!NOTE]
> <span data-ttu-id="6e8e5-107">[완료 된 프로젝트를 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-API-File-Upload-a8c0fb0d)합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8e5-107">[Download the completed project](https://code.msdn.microsoft.com/ASPNET-Web-API-File-Upload-a8c0fb0d).</span></span>


<span data-ttu-id="6e8e5-108">파일을 업로드 하는 것에 대 한 HTML 폼의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6e8e5-108">Here is an example of an HTML form for uploading a file:</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample1.html)]

![](sending-html-form-data-part-2/_static/image1.png)

<span data-ttu-id="6e8e5-109">이 양식에 텍스트 입력된 컨트롤 및 파일 입력된 컨트롤을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8e5-109">This form contains a text input control and a file input control.</span></span> <span data-ttu-id="6e8e5-110">양식에 파일 입력된 컨트롤을 포함 하는 경우는 **enctype** 특성은 항상 &quot;multipart/폼 데이터&quot;, 폼으로 다중 파트 MIME 메시지를 보냈음을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8e5-110">When a form contains a file input control, the **enctype** attribute should always be &quot;multipart/form-data&quot;, which specifies that the form will be sent as a multipart MIME message.</span></span>

<span data-ttu-id="6e8e5-111">예제 요청 확인 하 여 이해 하기 가장 쉽고 다중 파트 MIME 메시지의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6e8e5-111">The format of a multipart MIME message is easiest to understand by looking at an example request:</span></span>

[!code-console[Main](sending-html-form-data-part-2/samples/sample2.cmd)]

<span data-ttu-id="6e8e5-112">이 메시지는 두 개의 나뉩니다 *부분*, 각 폼 컨트롤에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8e5-112">This message is divided into two *parts*, one for each form control.</span></span> <span data-ttu-id="6e8e5-113">일부가 경계는 대시로 시작 하는 선으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e8e5-113">Part boundaries are indicated by the lines that start with dashes.</span></span>

> [!NOTE]
> <span data-ttu-id="6e8e5-114">임의의 구성 요소를 포함 하는 파트 경계 (&quot;41184676334&quot;)를 경계 문자열 메시지 파트 내 실수로 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6e8e5-114">The part boundary includes a random component (&quot;41184676334&quot;) to ensure that the boundary string does not accidentally appear inside a message part.</span></span>


<span data-ttu-id="6e8e5-115">각 메시지 부분 파트 콘텐츠 앞에 오는 하나 이상의 머리글을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8e5-115">Each message part contains one or more headers, followed by the part contents.</span></span>

- <span data-ttu-id="6e8e5-116">Content-disposition 헤더 컨트롤의 이름을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8e5-116">The Content-Disposition header includes the name of the control.</span></span> <span data-ttu-id="6e8e5-117">파일에 대 한 파일 이름을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8e5-117">For files, it also contains the file name.</span></span>
- <span data-ttu-id="6e8e5-118">콘텐츠 형식 헤더 데이터 부분에 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8e5-118">The Content-Type header describes the data in the part.</span></span> <span data-ttu-id="6e8e5-119">이 헤더를 생략 하면 기본값이 텍스트/일반입니다.</span><span class="sxs-lookup"><span data-stu-id="6e8e5-119">If this header is omitted, the default is text/plain.</span></span>

<span data-ttu-id="6e8e5-120">이전 예에서 사용자 콘텐츠 형식이 image/jpeg; GrandCanyon.jpg, 라는 파일을 업로드 입력 텍스트의 값은 &quot;여름 휴가&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8e5-120">In the previous example, the user uploaded a file named GrandCanyon.jpg, with content type image/jpeg; and the value of the text input was &quot;Summer Vacation&quot;.</span></span>

## <a name="file-upload"></a><span data-ttu-id="6e8e5-121">파일 업로드</span><span class="sxs-lookup"><span data-stu-id="6e8e5-121">File Upload</span></span>

<span data-ttu-id="6e8e5-122">이제는 다중 파트 MIME 메시지에서 파일을 읽어 하는 Web API 컨트롤러에 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6e8e5-122">Now let's look at a Web API controller that reads files from a multipart MIME message.</span></span> <span data-ttu-id="6e8e5-123">컨트롤러는 비동기적으로 파일을 읽이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e8e5-123">The controller will read the files asynchronously.</span></span> <span data-ttu-id="6e8e5-124">Web API를 사용 하 여 비동기 작업을 지 원하는 [작업 기반 프로그래밍 모델](https://msdn.microsoft.com/library/dd460693.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8e5-124">Web API supports asynchronous actions using the [task-based programming model](https://msdn.microsoft.com/library/dd460693.aspx).</span></span> <span data-ttu-id="6e8e5-125">먼저, 다음은 코드를 지 원하는.NET Framework 4.5를 대상으로 하는 경우는 **비동기** 및 **await** 키워드입니다.</span><span class="sxs-lookup"><span data-stu-id="6e8e5-125">First, here is the code if you are targeting .NET Framework 4.5, which supports the **async** and **await** keywords.</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample3.cs)]

<span data-ttu-id="6e8e5-126">컨트롤러 동작 매개 변수를 사용 하지 않는 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8e5-126">Notice that the controller action does not take any parameters.</span></span> <span data-ttu-id="6e8e5-127">미디어 유형 포맷터를 호출 하지 않고 작업을 내부 요청 본문 처리 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="6e8e5-127">That's because we process the request body inside the action, without invoking a media-type formatter.</span></span>

<span data-ttu-id="6e8e5-128">**IsMultipartContent** 메서드를 요청 하는 다중 파트 MIME 메시지에 포함 되어 있는지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8e5-128">The **IsMultipartContent** method checks whether the request contains a multipart MIME message.</span></span> <span data-ttu-id="6e8e5-129">그렇지 않으면 컨트롤러 HTTP 상태 코드 415 (지원 되지 않는 미디어 유형)을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8e5-129">If not, the controller returns HTTP status code 415 (Unsupported Media Type).</span></span>

<span data-ttu-id="6e8e5-130">**MultipartFormDataStreamProvider** 클래스는 파일 스트림을 업로드 된 파일에 할당 하는 도우미 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6e8e5-130">The **MultipartFormDataStreamProvider** class is a helper object that allocates file streams for uploaded files.</span></span> <span data-ttu-id="6e8e5-131">다중 파트 MIME 메시지를 읽으려면 호출는 **ReadAsMultipartAsync** 메서드.</span><span class="sxs-lookup"><span data-stu-id="6e8e5-131">To read the multipart MIME message, call the **ReadAsMultipartAsync** method.</span></span> <span data-ttu-id="6e8e5-132">이 메서드는 모든 메시지 파트를 추출 하 고에서 제공 하는 스트림을에 기록 된 **MultipartFormDataStreamProvider**합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8e5-132">This method extracts all of the message parts and writes them into the streams provided by the **MultipartFormDataStreamProvider**.</span></span>

<span data-ttu-id="6e8e5-133">메서드가 완료 되 면에서 파일에 대 한 정보를 얻을 수 있습니다는 **데이터** 컬렉션인 속성의 **MultipartFileData** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6e8e5-133">When the method completes, you can get information about the files from the **FileData** property, which is a collection of **MultipartFileData** objects.</span></span>

- <span data-ttu-id="6e8e5-134">**MultipartFileData.FileName** 저장 된 파일 서버에서 로컬 파일 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6e8e5-134">**MultipartFileData.FileName** is the local file name on the server, where the file was saved.</span></span>
- <span data-ttu-id="6e8e5-135">**MultipartFileData.Headers** 파트 헤더가 포함 되어 (*하지* 요청 헤더).</span><span class="sxs-lookup"><span data-stu-id="6e8e5-135">**MultipartFileData.Headers** contains the part header (*not* the request header).</span></span> <span data-ttu-id="6e8e5-136">콘텐츠에 액세스 하는 데 사용할 수 있습니다\_Disposition 및 콘텐츠 형식 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="6e8e5-136">You can use this to access the Content\_Disposition and Content-Type headers.</span></span>

<span data-ttu-id="6e8e5-137">이름에서 알 수 있듯이 **ReadAsMultipartAsync** 비동기 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="6e8e5-137">As the name suggests, **ReadAsMultipartAsync** is an asynchronous method.</span></span> <span data-ttu-id="6e8e5-138">사용 하 여 파일을 메서드가 완료 된 후 작업을 수행 하는 [연속 작업](https://msdn.microsoft.com/library/ee372288.aspx) (.NET 4.0) 또는 **await** 키워드 (.NET 4.5).</span><span class="sxs-lookup"><span data-stu-id="6e8e5-138">To perform work after the method completes, use a [continuation task](https://msdn.microsoft.com/library/ee372288.aspx) (.NET 4.0) or the **await** keyword (.NET 4.5).</span></span>

<span data-ttu-id="6e8e5-139">.NET Framework 4.0 버전의 이전 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6e8e5-139">Here is the .NET Framework 4.0 version of the previous code:</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample4.cs)]

## <a name="reading-form-control-data"></a><span data-ttu-id="6e8e5-140">양식 컨트롤 데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="6e8e5-140">Reading Form Control Data</span></span>

<span data-ttu-id="6e8e5-141">HTML 폼을 이전 보여 주었습니다 텍스트 입력된 컨트롤을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e8e5-141">The HTML form that I showed earlier had a text input control.</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample5.html)]

<span data-ttu-id="6e8e5-142">컨트롤의 값을 얻을 수는 **FormData** 의 속성은 **MultipartFormDataStreamProvider**합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8e5-142">You can get the value of the control from the **FormData** property of the **MultipartFormDataStreamProvider**.</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample6.cs?highlight=15)]

<span data-ttu-id="6e8e5-143">**FormData** 는 **NameValueCollection** 폼 컨트롤에 대 한 이름/값 쌍을 포함 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8e5-143">**FormData** is a **NameValueCollection** that contains name/value pairs for the form controls.</span></span> <span data-ttu-id="6e8e5-144">컬렉션에 중복 키가 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e8e5-144">The collection can contain duplicate keys.</span></span> <span data-ttu-id="6e8e5-145">이 폼을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8e5-145">Consider this form:</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample7.html)]

![](sending-html-form-data-part-2/_static/image2.png)

<span data-ttu-id="6e8e5-146">요청 본문은 다음과 같이 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e8e5-146">The request body might look like this:</span></span>

[!code-console[Main](sending-html-form-data-part-2/samples/sample8.cmd)]

<span data-ttu-id="6e8e5-147">이 경우에 **FormData** 컬렉션 다음 키/값 쌍을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8e5-147">In that case, the **FormData** collection would contain the following key/value pairs:</span></span>

- <span data-ttu-id="6e8e5-148">여행: 라운드트립</span><span class="sxs-lookup"><span data-stu-id="6e8e5-148">trip: round-trip</span></span>
- <span data-ttu-id="6e8e5-149">옵션: nonstop</span><span class="sxs-lookup"><span data-stu-id="6e8e5-149">options: nonstop</span></span>
- <span data-ttu-id="6e8e5-150">옵션: 날짜</span><span class="sxs-lookup"><span data-stu-id="6e8e5-150">options: dates</span></span>
- <span data-ttu-id="6e8e5-151">사용자 단위: 창</span><span class="sxs-lookup"><span data-stu-id="6e8e5-151">seat: window</span></span>
