---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6
title: '6 부: 모델 유효성 검사에 대 한 데이터 주석 사용 | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 6 부에서는 V 모델에 대 한 데이터 주석 사용을 설명 하는 중...
ms.author: aspnetcontent
ms.date: 04/21/2011
ms.assetid: b3193d33-2d0b-4d98-9712-58bd897c62ec
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6
msc.type: authoredcontent
ms.openlocfilehash: 10884f569f0f5d95517b73daab31fbd269a4726a
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37825955"
---
<a name="part-6-using-data-annotations-for-model-validation"></a><span data-ttu-id="0f6d2-104">6 부: 모델 유효성 검사에 대 한 데이터 주석 사용</span><span class="sxs-lookup"><span data-stu-id="0f6d2-104">Part 6: Using Data Annotations for Model Validation</span></span>
====================
<span data-ttu-id="0f6d2-105">[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="0f6d2-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="0f6d2-106">MVC Music Store 자습서 응용 프로그램을 소개 하 고 웹 개발을 위한 ASP.NET MVC 및 Visual Studio를 사용 하는 방법을 단계별로 설명 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f6d2-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="0f6d2-107">MVC Music Store는 온라인 음악 앨범을 판매 하 고 기본 사이트 관리, 사용자 로그인 및 장바구니 기능을 구현 하는 간단한 샘플 저장소 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="0f6d2-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="0f6d2-108">이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f6d2-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="0f6d2-109">6 부 모델 유효성 검사에 대 한 데이터 주석을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f6d2-109">Part 6 covers Using Data Annotations for Model Validation.</span></span>


<span data-ttu-id="0f6d2-110">만들기 및 편집 폼을 사용 하 여 중요 한 문제가 있다고: 유효성 검사를 수행 중인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f6d2-110">We have a major issue with our Create and Edit forms: they're not doing any validation.</span></span> <span data-ttu-id="0f6d2-111">가격 필드에 필수 필드를 빈 또는 형식 문자를 유지 하는 등 수행할 수 있습니다이 고 데이터베이스에서 살펴보겠습니다 첫 번째 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f6d2-111">We can do things like leave required fields blank or type letters in the Price field, and the first error we'll see is from the database.</span></span>

<span data-ttu-id="0f6d2-112">데이터 주석 모델 클래스를 추가 하 여 응용 프로그램에 유효성 검사를 쉽게 추가할 수 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0f6d2-112">We can easily add validation to our application by adding Data Annotations to our model classes.</span></span> <span data-ttu-id="0f6d2-113">데이터 주석 허락 하는 모델 속성에 적용 되는 원하는 규칙에 설명 하 고 ASP.NET MVC 해 줄 것으로 강제 적용 하 고 사용자에 게 적절 한 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f6d2-113">Data Annotations allow us to describe the rules we want applied to our model properties, and ASP.NET MVC will take care of enforcing them and displaying appropriate messages to our users.</span></span>

## <a name="adding-validation-to-our-album-forms"></a><span data-ttu-id="0f6d2-114">앨범은 폼에 유효성 검사 추가</span><span class="sxs-lookup"><span data-stu-id="0f6d2-114">Adding Validation to our Album Forms</span></span>

<span data-ttu-id="0f6d2-115">다음 데이터 주석 특성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f6d2-115">We'll use the following Data Annotation attributes:</span></span>

- <span data-ttu-id="0f6d2-116">**필요한** – 속성이 필수 필드 임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0f6d2-116">**Required** – Indicates that the property is a required field</span></span>
- <span data-ttu-id="0f6d2-117">**DisplayName** – 양식 필드 유효성 검사 메시지에 사용 되는 대상 텍스트를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f6d2-117">**DisplayName** – Defines the text we want used on form fields and validation messages</span></span>
- <span data-ttu-id="0f6d2-118">**StringLength** – 문자열 필드에 대 한 최대 길이 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f6d2-118">**StringLength** – Defines a maximum length for a string field</span></span>
- <span data-ttu-id="0f6d2-119">**범위** – 숫자 필드에 대 한 최대 및 최소 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f6d2-119">**Range** – Gives a maximum and minimum value for a numeric field</span></span>
- <span data-ttu-id="0f6d2-120">**바인딩** – 모델 속성을 매개 변수 또는 형식 값을 바인딩하는 경우를 포함 하거나 제외 하도록 필드를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f6d2-120">**Bind** – Lists fields to exclude or include when binding parameter or form values to model properties</span></span>
- <span data-ttu-id="0f6d2-121">**ScaffoldColumn** – 편집기 폼에서 필드를 숨기면 허용</span><span class="sxs-lookup"><span data-stu-id="0f6d2-121">**ScaffoldColumn** – Allows hiding fields from editor forms</span></span>

<span data-ttu-id="0f6d2-122">*참고: 데이터 주석 특성을 사용 하 여 모델 유효성 검사에 대 한 자세한 내용은 참조는 MSDN 설명서*[`https://go.microsoft.com/fwlink/?LinkId=159063`](https://go.microsoft.com/fwlink/?LinkId=159063)</span><span class="sxs-lookup"><span data-stu-id="0f6d2-122">*Note: For more information on Model Validation using Data Annotation attributes, see the MSDN documentation at*[`https://go.microsoft.com/fwlink/?LinkId=159063`](https://go.microsoft.com/fwlink/?LinkId=159063)</span></span>

<span data-ttu-id="0f6d2-123">앨범 클래스를 열고 다음을 추가 합니다 *를 사용 하 여* 문을 맨 위에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f6d2-123">Open the Album class and add the following *using* statements to the top.</span></span>

[!code-csharp[Main](mvc-music-store-part-6/samples/sample1.cs)]

<span data-ttu-id="0f6d2-124">그런 다음 아래와 같이 표시 및 유효성 검사 특성을 추가 하는 속성을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f6d2-124">Next, update the properties to add display and validation attributes as shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-6/samples/sample2.cs)]

<span data-ttu-id="0f6d2-125">그곳에서 있는 동안 변경 했습니다 장르 및 음악가 가상 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="0f6d2-125">While we're there, we've also changed the Genre and Artist to virtual properties.</span></span> <span data-ttu-id="0f6d2-126">이렇게 하면 지연 로드 고 필요에 따라 Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="0f6d2-126">This allows Entity Framework to lazy-load them as necessary.</span></span>

[!code-csharp[Main](mvc-music-store-part-6/samples/sample3.cs)]

<span data-ttu-id="0f6d2-127">앨범 모델에 이러한 특성을 추가 하지, 후 우리의 만들기 및 편집 화면에 즉시 보내기 시작 필드 유효성 검사 및 표시 이름을 사용 하 여 (예: 앨범 아트 Url AlbumArtUrl 대신)를 선택 했습니다.</span><span class="sxs-lookup"><span data-stu-id="0f6d2-127">After having added these attributes to our Album model, our Create and Edit screen immediately begin validating fields and using the Display Names we've chosen (e.g. Album Art Url instead of AlbumArtUrl).</span></span> <span data-ttu-id="0f6d2-128">응용 프로그램을 실행 하 고 /StoreManager/Create 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="0f6d2-128">Run the application and browse to /StoreManager/Create.</span></span>

![](mvc-music-store-part-6/_static/image1.png)

<span data-ttu-id="0f6d2-129">다음으로, 일부 유효성 검사 규칙 중단 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f6d2-129">Next, we'll break some validation rules.</span></span> <span data-ttu-id="0f6d2-130">0의 가격을 입력 하 고 제목을 비워 둡니다.</span><span class="sxs-lookup"><span data-stu-id="0f6d2-130">Enter a price of 0 and leave the Title blank.</span></span> <span data-ttu-id="0f6d2-131">만들기 단추를 클릭 하는 경우에 유효성 검사 오류 메시지와 함께 필드 유효성 검사 규칙을 충족 하지 않은 표시를 정의 했으며 표시 된 양식을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0f6d2-131">When we click on the Create button, we will see the form displayed with validation error messages showing which fields did not meet the validation rules we have defined.</span></span>

![](mvc-music-store-part-6/_static/image2.png)

## <a name="testing-the-client-side-validation"></a><span data-ttu-id="0f6d2-132">클라이언트 쪽 유효성 검사 테스트</span><span class="sxs-lookup"><span data-stu-id="0f6d2-132">Testing the Client-Side Validation</span></span>

<span data-ttu-id="0f6d2-133">서버 쪽 유효성 검사 응용 프로그램 관점에서 매우 중요 한 이므로 사용자가 클라이언트 쪽 유효성 검사를 피할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f6d2-133">Server-side validation is very important from an application perspective, because users can circumvent client-side validation.</span></span> <span data-ttu-id="0f6d2-134">그러나 웹 페이지 forms만 서버 쪽 유효성 검사를 구현 하는 세 가지 중요 한 문제를 일으킵니다.</span><span class="sxs-lookup"><span data-stu-id="0f6d2-134">However, webpage forms which only implement server-side validation exhibit three significant problems.</span></span>

1. <span data-ttu-id="0f6d2-135">사용자가 브라우저에 전송할 응답에 대 한 폼 게시, 서버의 유효성을 검사할 수에서 기다린 후 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f6d2-135">The user has to wait for the form to be posted, validated on the server, and for the response to be sent to their browser.</span></span>
2. <span data-ttu-id="0f6d2-136">사용자는 이제 유효성 검사 규칙을 통과할 수 있도록 필드를 수정 하는 경우 즉각적인 피드백을 받게 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0f6d2-136">The user doesn't get immediate feedback when they correct a field so that it now passes the validation rules.</span></span>
3. <span data-ttu-id="0f6d2-137">사용자의 브라우저를 활용 하는 대신 유효성 검사 논리를 수행 하는 서버 리소스를 낭비 하 했습니다.</span><span class="sxs-lookup"><span data-stu-id="0f6d2-137">We are wasting server resources to perform validation logic instead of leveraging the user's browser.</span></span>

<span data-ttu-id="0f6d2-138">다행 스럽게도 ASP.NET MVC 3 스 캐 폴드 템플릿 모두 클라이언트 쪽 유효성 검사에는 기본적으로 추가 작업이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f6d2-138">Fortunately, the ASP.NET MVC 3 scaffold templates have client-side validation built in, requiring no additional work whatsoever.</span></span>

<span data-ttu-id="0f6d2-139">유효성 검사 메시지를 즉시 제거 됩니다 있도록 유효성 검사 요구 사항을 충족 제목 필드에서 문자 하나를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f6d2-139">Typing a single letter in the Title field satisfies the validation requirements, so the validation message is immediately removed.</span></span>

![](mvc-music-store-part-6/_static/image3.png)


> [!div class="step-by-step"]
> <span data-ttu-id="0f6d2-140">[이전](mvc-music-store-part-5.md)
> [다음](mvc-music-store-part-7.md)</span><span class="sxs-lookup"><span data-stu-id="0f6d2-140">[Previous](mvc-music-store-part-5.md)
[Next](mvc-music-store-part-7.md)</span></span>
