---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6
title: '6 단계: 데이터 주석 모델 유효성 검사에 사용 하 여 | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다. 6 부 V 모델에 대 한 데이터 주석을 사용 하 여 설명...
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/21/2011
ms.topic: article
ms.assetid: b3193d33-2d0b-4d98-9712-58bd897c62ec
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6
msc.type: authoredcontent
ms.openlocfilehash: 328eccb4324bb10a7e8dec819a70129fc14c42c4
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="part-6-using-data-annotations-for-model-validation"></a><span data-ttu-id="b4351-104">6 부: 모델 유효성 검사에 대 한 데이터 주석을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="b4351-104">Part 6: Using Data Annotations for Model Validation</span></span>
====================
<span data-ttu-id="b4351-105">으로 [Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="b4351-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="b4351-106">MVC Music Store는 소개 하 고 웹 개발에 대 한 ASP.NET MVC와 Visual Studio를 사용 하는 방법을 단계별로 설명 하는 자습서 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="b4351-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="b4351-107">MVC Music Store는 온라인 음악 앨범 판매 및 기본 사이트 관리, 사용자 로그인 및 장바구니 기능을 구현 하는 간단한 샘플 저장소 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="b4351-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="b4351-108">이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4351-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="b4351-109">6 부 데이터 주석을 사용 하 여 모델 유효성 검사에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4351-109">Part 6 covers Using Data Annotations for Model Validation.</span></span>


<span data-ttu-id="b4351-110">중요 한 문제는 폼 만들기 및 편집 해야: 유효성 검사 작동 하지 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="b4351-110">We have a major issue with our Create and Edit forms: they're not doing any validation.</span></span> <span data-ttu-id="b4351-111">수행할 수 있고, Price 필드는 필수 필드를 비워 또는 형식 문자 둡니다와 같은 and 볼 수 있겠지만, 첫 번째 오류는 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="b4351-111">We can do things like leave required fields blank or type letters in the Price field, and the first error we'll see is from the database.</span></span>

<span data-ttu-id="b4351-112">데이터 주석 모델 클래스를 추가 하 여 응용 프로그램에 유효성 검사를 쉽게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4351-112">We can easily add validation to our application by adding Data Annotations to our model classes.</span></span> <span data-ttu-id="b4351-113">ASP.NET MVC의 내용을 적용 하 고이 사용자에 게 적절 한 메시지를 표시 하므로 및 데이터 주석 허용 우리의 모델 속성에 적용 된 원하는 규칙을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4351-113">Data Annotations allow us to describe the rules we want applied to our model properties, and ASP.NET MVC will take care of enforcing them and displaying appropriate messages to our users.</span></span>

## <a name="adding-validation-to-our-album-forms"></a><span data-ttu-id="b4351-114">유효성 검사 앨범은 폼에 추가</span><span class="sxs-lookup"><span data-stu-id="b4351-114">Adding Validation to our Album Forms</span></span>

<span data-ttu-id="b4351-115">다음 데이터 주석을 특성 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4351-115">We'll use the following Data Annotation attributes:</span></span>

- <span data-ttu-id="b4351-116">**필수** – 속성이 필수 필드 임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b4351-116">**Required** – Indicates that the property is a required field</span></span>
- <span data-ttu-id="b4351-117">**DisplayName** – 양식 필드 및 유효성 검사 메시지에 사용 되는 원하는 텍스트 정의</span><span class="sxs-lookup"><span data-stu-id="b4351-117">**DisplayName** – Defines the text we want used on form fields and validation messages</span></span>
- <span data-ttu-id="b4351-118">**StringLength** – 문자열 필드에 대 한 최대 길이 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4351-118">**StringLength** – Defines a maximum length for a string field</span></span>
- <span data-ttu-id="b4351-119">**범위** – 숫자 필드에 대 한 최대 및 최소 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4351-119">**Range** – Gives a maximum and minimum value for a numeric field</span></span>
- <span data-ttu-id="b4351-120">**바인딩할** – 모델 속성을 매개 변수 또는 폼 값에 바인딩할 때 포함 하거나 제외 하도록 필드 나열</span><span class="sxs-lookup"><span data-stu-id="b4351-120">**Bind** – Lists fields to exclude or include when binding parameter or form values to model properties</span></span>
- <span data-ttu-id="b4351-121">**ScaffoldColumn** – 편집기 양식에서 필드를 숨기면 허용</span><span class="sxs-lookup"><span data-stu-id="b4351-121">**ScaffoldColumn** – Allows hiding fields from editor forms</span></span>

<span data-ttu-id="b4351-122">*참고: 데이터 주석 특성을 사용 하 여 모델 유효성 검사에 대 한 자세한 내용은 MSDN 설명서를 참조*[`https://go.microsoft.com/fwlink/?LinkId=159063`](https://go.microsoft.com/fwlink/?LinkId=159063)</span><span class="sxs-lookup"><span data-stu-id="b4351-122">*Note: For more information on Model Validation using Data Annotation attributes, see the MSDN documentation at*[`https://go.microsoft.com/fwlink/?LinkId=159063`](https://go.microsoft.com/fwlink/?LinkId=159063)</span></span>

<span data-ttu-id="b4351-123">앨범 클래스를 열고 다음 코드를 추가 *를 사용 하 여* 문을 맨 위에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4351-123">Open the Album class and add the following *using* statements to the top.</span></span>

[!code-csharp[Main](mvc-music-store-part-6/samples/sample1.cs)]

<span data-ttu-id="b4351-124">다음으로 아래와 같이 표시 및 유효성 검사 특성을 추가 하는 속성을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4351-124">Next, update the properties to add display and validation attributes as shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-6/samples/sample2.cs)]

<span data-ttu-id="b4351-125">We're 발생 하는 동안 변경 했습니다 Genre 및 음악가 가상 속성에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4351-125">While we're there, we've also changed the Genre and Artist to virtual properties.</span></span> <span data-ttu-id="b4351-126">따라서 지연 로드에 필요에 따라를 Entity Framework 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4351-126">This allows Entity Framework to lazy-load them as necessary.</span></span>

[!code-csharp[Main](mvc-music-store-part-6/samples/sample3.cs)]

<span data-ttu-id="b4351-127">예제의 앨범 모델에 이러한 특성 추가, 후 우리의 만들기 및 편집 화면 필드 유효성 검사 즉시 시작 하 고 표시 이름을 사용 하 여 우리 선택한 (예: 앨범 아트 Url AlbumArtUrl 대신).</span><span class="sxs-lookup"><span data-stu-id="b4351-127">After having added these attributes to our Album model, our Create and Edit screen immediately begin validating fields and using the Display Names we've chosen (e.g. Album Art Url instead of AlbumArtUrl).</span></span> <span data-ttu-id="b4351-128">응용 프로그램을 실행 하 고 /StoreManager/Create 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b4351-128">Run the application and browse to /StoreManager/Create.</span></span>

![](mvc-music-store-part-6/_static/image1.png)

<span data-ttu-id="b4351-129">다음으로, 일부 유효성 검사 규칙을 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4351-129">Next, we'll break some validation rules.</span></span> <span data-ttu-id="b4351-130">0의 가격을 입력 하 고 제목을 비워 둡니다.</span><span class="sxs-lookup"><span data-stu-id="b4351-130">Enter a price of 0 and leave the Title blank.</span></span> <span data-ttu-id="b4351-131">만들기 단추를 클릭할 때 유효성 검사 오류 메시지와 함께 어떤 필드 유효성 검사 규칙을 충족 하지 않는 보여 주는 정의한 표시 된 폼을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="b4351-131">When we click on the Create button, we will see the form displayed with validation error messages showing which fields did not meet the validation rules we have defined.</span></span>

![](mvc-music-store-part-6/_static/image2.png)

## <a name="testing-the-client-side-validation"></a><span data-ttu-id="b4351-132">클라이언트 쪽 유효성 검사 테스트</span><span class="sxs-lookup"><span data-stu-id="b4351-132">Testing the Client-Side Validation</span></span>

<span data-ttu-id="b4351-133">서버 쪽 유효성 검사는 사용자가 클라이언트 쪽 유효성 검사를 피할 수 때문에 응용 프로그램 관점에서 매우 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4351-133">Server-side validation is very important from an application perspective, because users can circumvent client-side validation.</span></span> <span data-ttu-id="b4351-134">그러나만 서버 쪽 유효성 검사를 구현 하는 웹 페이지 forms 세 가지 중요 한 문제를 일으킵니다.</span><span class="sxs-lookup"><span data-stu-id="b4351-134">However, webpage forms which only implement server-side validation exhibit three significant problems.</span></span>

1. <span data-ttu-id="b4351-135">사용자는 브라우저를 보낼 수에 대 한 응답으로 사용 하려면 게시를 서버에서 유효성을 검사할 폼에 대 한 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="b4351-135">The user has to wait for the form to be posted, validated on the server, and for the response to be sent to their browser.</span></span>
2. <span data-ttu-id="b4351-136">사용자는 이제 유효성 검사 규칙을 통과할 수 있도록 필드를 수정 하는 경우 대 한 즉각적인 피드백을 받게 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4351-136">The user doesn't get immediate feedback when they correct a field so that it now passes the validation rules.</span></span>
3. <span data-ttu-id="b4351-137">사용자의 브라우저를 활용 하는 대신 유효성 검사 논리를 수행 하려면 서버 리소스를 낭비는 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b4351-137">We are wasting server resources to perform validation logic instead of leveraging the user's browser.</span></span>

<span data-ttu-id="b4351-138">에서는 ASP.NET MVC 3 스 캐 폴드 템플릿이 있는 클라이언트 쪽 유효성 검사 기본 제공 되 고 어떠한 추가 작업이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4351-138">Fortunately, the ASP.NET MVC 3 scaffold templates have client-side validation built in, requiring no additional work whatsoever.</span></span>

<span data-ttu-id="b4351-139">유효성 검사 메시지가 즉시 제거 하므로 유효성 검사 요구 사항을 충족 Title 필드의 문자 하나를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4351-139">Typing a single letter in the Title field satisfies the validation requirements, so the validation message is immediately removed.</span></span>

![](mvc-music-store-part-6/_static/image3.png)


> [!div class="step-by-step"]
> <span data-ttu-id="b4351-140">[이전](mvc-music-store-part-5.md)
> [다음](mvc-music-store-part-7.md)</span><span class="sxs-lookup"><span data-stu-id="b4351-140">[Previous](mvc-music-store-part-5.md)
[Next](mvc-music-store-part-7.md)</span></span>
