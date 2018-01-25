---
title: "ASP.NET Core에서 태그 도우미를 작성합니다."
author: rick-anderson
description: "ASP.NET Core에서 태그 도우미를 작성 하는 방법을 알아봅니다."
ms.author: riande
manager: wpickett
ms.date: 01/19/2018
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: mvc/views/tag-helpers/authoring
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a1f1b2c2e60a1337c15f019185c764d0a9ada1b5
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
# <a name="author-tag-helpers-in-aspnet-core-a-walkthrough-with-samples"></a><span data-ttu-id="21ff8-103">ASP.NET Core, 샘플을 연습에서에서 만든 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="21ff8-103">Author Tag Helpers in ASP.NET Core, a walkthrough with samples</span></span>

<span data-ttu-id="21ff8-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="21ff8-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="21ff8-105">[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/tag-helpers/authoring/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="21ff8-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/tag-helpers/authoring/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="get-started-with-tag-helpers"></a><span data-ttu-id="21ff8-106">시작 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="21ff8-106">Get started with Tag Helpers</span></span>

<span data-ttu-id="21ff8-107">이 자습서는 프로그래밍 태그 도우미에 대 한 소개를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-107">This tutorial provides an introduction to programming Tag Helpers.</span></span> <span data-ttu-id="21ff8-108">[태그 도우미 소개](intro.md) 태그 도우미를 제공 하는 이점에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-108">[Introduction to Tag Helpers](intro.md) describes the benefits that Tag Helpers provide.</span></span>

<span data-ttu-id="21ff8-109">태그 도우미 클래스를 구현 하는 모든 클래스는는 `ITagHelper` 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-109">A tag helper is any class that implements the `ITagHelper` interface.</span></span> <span data-ttu-id="21ff8-110">그러나 태그 도우미를 작성할 때 일반적으로에서 파생 시키고 `TagHelper`, 따라서 제공에 대 한 액세스를 수행 하는 `Process` 메서드.</span><span class="sxs-lookup"><span data-stu-id="21ff8-110">However, when you author a tag helper, you generally derive from `TagHelper`, doing so gives you access to the `Process` method.</span></span>

1. <span data-ttu-id="21ff8-111">라는 새 ASP.NET Core 프로젝트 만들기 **AuthoringTagHelpers**합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-111">Create a new ASP.NET Core project called **AuthoringTagHelpers**.</span></span> <span data-ttu-id="21ff8-112">이 프로젝트에 대 한 인증에 필요 하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-112">You won't need authentication for this project.</span></span>

2. <span data-ttu-id="21ff8-113">태그 도우미 호출을 보관할 폴더를 만들 *TagHelpers*합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-113">Create a folder to hold the Tag Helpers called *TagHelpers*.</span></span> <span data-ttu-id="21ff8-114">*TagHelpers* 폴더는 *하지* 필요한 합리적인 규칙 이지만 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-114">The *TagHelpers* folder is *not* required, but it's a reasonable convention.</span></span> <span data-ttu-id="21ff8-115">이제 시작 하겠습니다 몇 가지 간단한 태그 도우미를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-115">Now let's get started writing some simple tag helpers.</span></span>

## <a name="a-minimal-tag-helper"></a><span data-ttu-id="21ff8-116">최소한의 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="21ff8-116">A minimal Tag Helper</span></span>

<span data-ttu-id="21ff8-117">이 섹션에서는 전자 메일 태그를 업데이트 하는 태그 도우미를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-117">In this section, you write a tag helper that updates an email tag.</span></span> <span data-ttu-id="21ff8-118">예:</span><span class="sxs-lookup"><span data-stu-id="21ff8-118">For example:</span></span>

```html
<email>Support</email>
   ```

<span data-ttu-id="21ff8-119">서버 해당 태그를 다음으로 변환 하는 전자 메일 태그 도우미를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-119">The server will use our email tag helper to convert that markup into the following:</span></span>

```html
<a href="mailto:Support@contoso.com">Support@contoso.com</a>
```

<span data-ttu-id="21ff8-120">즉, 앵커 태그는 하면 전자 메일 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-120">That is, an anchor tag that makes this an email link.</span></span> <span data-ttu-id="21ff8-121">블로그 엔진을 작성 하는 경우 동일한 도메인에 모든 마케팅, 지원 및 다른 연락처에 대 한 전자 메일을 보낼 수 필요 사용자에 게 이렇게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-121">You might want to do this if you are writing a blog engine and need it to send email for marketing, support, and other contacts, all to the same domain.</span></span>

1.  <span data-ttu-id="21ff8-122">다음 추가 `EmailTagHelper` 클래스는 *TagHelpers* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-122">Add the following `EmailTagHelper` class to the *TagHelpers* folder.</span></span>

    [!code-csharp[Main](authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/TagHelpers/z1EmailTagHelperCopy.cs)]
    
    <span data-ttu-id="21ff8-123">**참고:**</span><span class="sxs-lookup"><span data-stu-id="21ff8-123">**Notes:**</span></span>
    
    * <span data-ttu-id="21ff8-124">루트 클래스 이름의 요소를 대상으로 하는 명명 규칙을 사용 하 여 태그 도우미 (빼기는 *TagHelper* 클래스 이름의 부분)입니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-124">Tag helpers use a naming convention that targets elements of the root class name (minus the *TagHelper* portion of the class name).</span></span> <span data-ttu-id="21ff8-125">이 예제에서는 루트 이름 **전자 메일**TagHelper은 *전자 메일*이므로 `<email>` 태그 대상이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-125">In this example, the root name of **Email**TagHelper is *email*, so the `<email>` tag will be targeted.</span></span> <span data-ttu-id="21ff8-126">이 명명 규칙은 대부분 태그 도우미에 대 한 작동 해야, 나중에 재정의 하는 방법을 보여 드리 려 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-126">This naming convention should work for most tag helpers, later on I'll show how to override it.</span></span>
    
    * <span data-ttu-id="21ff8-127">`EmailTagHelper` 클래스는 `TagHelper`에서 파생됩니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-127">The `EmailTagHelper` class derives from `TagHelper`.</span></span> <span data-ttu-id="21ff8-128">`TagHelper` 클래스 태그 도우미를 작성 하기 위한 메서드 및 속성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-128">The `TagHelper` class provides methods and properties for writing Tag Helpers.</span></span>
    
    * <span data-ttu-id="21ff8-129">재정의 된 `Process` 방법은 태그 도우미 수행 하는 작업 실행을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-129">The overridden `Process` method controls what the tag helper does when executed.</span></span> <span data-ttu-id="21ff8-130">`TagHelper` 클래스는 비동기 버전을 제공 (`ProcessAsync`) 동일한 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-130">The `TagHelper` class also provides an asynchronous version (`ProcessAsync`) with the same parameters.</span></span>
    
    * <span data-ttu-id="21ff8-131">컨텍스트 매개 변수를 `Process` (및 `ProcessAsync`) 현재 HTML 태그의 실행과 관련 된 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-131">The context parameter to `Process` (and `ProcessAsync`) contains information associated with the execution of the current HTML tag.</span></span>
    
    * <span data-ttu-id="21ff8-132">출력 매개 변수를 `Process` (및 `ProcessAsync`)는 HTML 태그 및 콘텐츠를 생성 하는 데 원본 소스를 반영 하는 상태 저장 HTML 요소를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-132">The output parameter to `Process` (and `ProcessAsync`) contains a stateful HTML element representative of the original source used to generate an HTML tag and content.</span></span>
    
    * <span data-ttu-id="21ff8-133">통해 클래스 이름 접미사가 **TagHelper**, 즉 *하지* 필수, 모범 사례 규칙 것으로 간주 되지만 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-133">Our class name has a suffix of **TagHelper**, which is *not* required, but it's considered a best practice convention.</span></span> <span data-ttu-id="21ff8-134">클래스를 선언할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-134">You could declare the class as:</span></span>
    
    ```csharp
    public class Email : TagHelper
    ```

2.  <span data-ttu-id="21ff8-135">확인 하는 `EmailTagHelper` 우리의 모든 Razor 뷰를 사용할 수 있는 클래스, 추가 `addTagHelper` 지시문을 *Views/_ViewImports.cshtml* 파일:[!code-html[Main](../../../mvc/views/tag-helpers/authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/Views/_ViewImportsCopyEmail.cshtml?highlight=2,3)]</span><span class="sxs-lookup"><span data-stu-id="21ff8-135">To make the `EmailTagHelper` class available to all our Razor views, add the `addTagHelper` directive to the *Views/_ViewImports.cshtml* file: [!code-html[Main](../../../mvc/views/tag-helpers/authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/Views/_ViewImportsCopyEmail.cshtml?highlight=2,3)]</span></span>
    
    <span data-ttu-id="21ff8-136">위의 코드에서는 와일드 카드 구문을 사용할 수 있는 모든 태그 도우미 어셈블리에서 지정 하 여</span><span class="sxs-lookup"><span data-stu-id="21ff8-136">The code above uses the wildcard syntax to specify all the tag helpers in our assembly will be available.</span></span> <span data-ttu-id="21ff8-137">뒤의 첫 번째 문자열 `@addTagHelper` 로드할 태그 도우미를 지정 합니다 (사용 하 여 "\*" 모든 태그 도우미에 대 한), 및 두 번째 문자열 "AuthoringTagHelpers" 태그 도우미에는 어셈블리를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-137">The first string after `@addTagHelper` specifies the tag helper to load (Use "\*" for all tag helpers), and the second string "AuthoringTagHelpers" specifies the assembly the tag helper is in.</span></span> <span data-ttu-id="21ff8-138">또한 와일드 카드 구문을 사용 하 여 ASP.NET Core MVC 태그 도우미의 두 번째 줄을 제공 하는 확인 (해당 도우미에 대해서는 설명 [태그 도우미 소개](intro.md).) `@addTagHelper` 지시문 태그 도우미 Razor 뷰를 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-138">Also, note that the second line brings in the ASP.NET Core MVC tag helpers using the wildcard syntax (those helpers are discussed in [Introduction to Tag Helpers](intro.md).) It's the `@addTagHelper` directive that makes the tag helper available to the Razor view.</span></span> <span data-ttu-id="21ff8-139">또는 다음과 같이 태그 도우미의 정규화 된 이름 (FQN)를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-139">Alternatively, you can provide the fully qualified name (FQN) of a tag helper as shown below:</span></span>
    
```csharp
@using AuthoringTagHelpers
@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers
@addTagHelper AuthoringTagHelpers.TagHelpers.EmailTagHelper, AuthoringTagHelpers
```
    
<!--
the following snippet uses TagHelpers3 and should use TagHelpers (not the 3)
    [!code-html[Main](../../../mvc/views/tag-helpers/authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/Views/_ViewImports.cshtml?highlight=3&range=1-3)]
-->
    
<span data-ttu-id="21ff8-140">태그 도우미는 FQN를 사용 하 여 뷰를 추가 하려면 먼저는 FQN가 추가 (`AuthoringTagHelpers.TagHelpers.EmailTagHelper`), 및 다음 어셈블리 이름 (*AuthoringTagHelpers*).</span><span class="sxs-lookup"><span data-stu-id="21ff8-140">To add a tag helper to a view using a FQN, you first add the FQN (`AuthoringTagHelpers.TagHelpers.EmailTagHelper`), and then the assembly name (*AuthoringTagHelpers*).</span></span> <span data-ttu-id="21ff8-141">와일드 카드 구문을 사용 하 여 대부분의 개발자를 선호 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-141">Most developers will prefer to use the wildcard syntax.</span></span> <span data-ttu-id="21ff8-142">[태그 도우미 소개](intro.md) 태그 도우미 추가, 제거, 계층 및 와일드 카드 구문을 세부적으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-142">[Introduction to Tag Helpers](intro.md) goes into detail on tag helper adding, removing, hierarchy, and wildcard syntax.</span></span>
    
3.  <span data-ttu-id="21ff8-143">태그가 업데이트는 *Views/Home/Contact.cshtml* 이러한 변경 내용으로 파일:</span><span class="sxs-lookup"><span data-stu-id="21ff8-143">Update the markup in the *Views/Home/Contact.cshtml* file with these changes:</span></span>

    [!code-html[Main](../../../mvc/views/tag-helpers/authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/Views/Home/Contact.cshtml?highlight=15,16&range=1-17)]

4.  <span data-ttu-id="21ff8-144">응용 프로그램을 실행 하 고 선호 하는 브라우저를 사용 하 여 전자 메일 태그 앵커 태그도 바뀌는 것을 확인할 수 있도록 HTML 소스를 봅니다 (예를 들어 `<a>Support</a>`).</span><span class="sxs-lookup"><span data-stu-id="21ff8-144">Run the app and use your favorite browser to view the HTML source so you can verify that the email tags are replaced with anchor markup (For example, `<a>Support</a>`).</span></span> <span data-ttu-id="21ff8-145">*지원* 및 *마케팅* 는 링크로 렌더링 됩니다 있지만 없습니다는 `href` 특성을 작동할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-145">*Support* and *Marketing* are rendered as a links, but they don't have an `href` attribute to make them functional.</span></span> <span data-ttu-id="21ff8-146">다음 섹션에서이 문제를 해결 합니다 했습니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-146">We'll fix that in the next section.</span></span>

<span data-ttu-id="21ff8-147">참고: HTML 태그 및 특성, 태그, 클래스 이름 및 Razor, 및 C#의 특성을 같은 않습니다 대/소문자 구분.</span><span class="sxs-lookup"><span data-stu-id="21ff8-147">Note: Like HTML tags and attributes, tags, class names and attributes in Razor, and C# are not case-sensitive.</span></span>

## <a name="setattribute-and-setcontent"></a><span data-ttu-id="21ff8-148">SetAttribute 및 SetContent</span><span class="sxs-lookup"><span data-stu-id="21ff8-148">SetAttribute and SetContent</span></span>

<span data-ttu-id="21ff8-149">이 섹션에서는 업데이트 하는 `EmailTagHelper` 하 여 전자 메일에 대 한 유효한 앵커 태그를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-149">In this section, we'll update the `EmailTagHelper` so that it will create a valid anchor tag for email.</span></span> <span data-ttu-id="21ff8-150">업데이트를 가져오도록 Razor 보기의 정보 (형식으로 `mail-to` 특성)에서 앵커를 생성 합니다.이 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-150">We'll update it to take information from a Razor view (in the form of a `mail-to` attribute) and use that in generating the anchor.</span></span>

<span data-ttu-id="21ff8-151">업데이트는 `EmailTagHelper` 다음을 사용 하 여 클래스:</span><span class="sxs-lookup"><span data-stu-id="21ff8-151">Update the `EmailTagHelper` class with the following:</span></span>

[!code-csharp[Main](authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/TagHelpers/EmailTagHelperMailTo.cs?range=6-22)]

<span data-ttu-id="21ff8-152">**참고:**</span><span class="sxs-lookup"><span data-stu-id="21ff8-152">**Notes:**</span></span>

* <span data-ttu-id="21ff8-153">파스칼식 대/소문자 클래스 및 속성 이름 태그 도우미에 대 한 변환 자신의 [kebab 대/소문자를 줄이려면](https://stackoverflow.com/questions/11273282/whats-the-name-for-dash-separated-case/12273101)합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-153">Pascal-cased class and property names for tag helpers are translated into their [lower kebab case](https://stackoverflow.com/questions/11273282/whats-the-name-for-dash-separated-case/12273101).</span></span> <span data-ttu-id="21ff8-154">따라서 사용 하는 `MailTo` 특성을 사용 하 여 `<email mail-to="value"/>` 와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-154">Therefore, to use the `MailTo` attribute, you'll use `<email mail-to="value"/>` equivalent.</span></span>

* <span data-ttu-id="21ff8-155">마지막 줄이 최소 기능 태그 도우미에 대 한 완료 된 콘텐츠를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-155">The last line sets the completed content for our minimally functional tag helper.</span></span>

* <span data-ttu-id="21ff8-156">강조 표시 된 줄에는 특성을 추가 하기 위한 구문을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-156">The highlighted line shows the syntax for adding attributes:</span></span>

[!code-csharp[Main](authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/TagHelpers/EmailTagHelperMailTo.cs?highlight=6&range=14-21)]

<span data-ttu-id="21ff8-157">이 방법으로 속성 컬렉션에 현재 존재 하지 않는 "href" 특성에 대 한 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-157">That approach works for the attribute "href" as long as it doesn't currently exist in the attributes collection.</span></span> <span data-ttu-id="21ff8-158">사용할 수도 있습니다는 `output.Attributes.Add` 메서드를 태그 도우미 특성의 태그 특성 컬렉션의 끝에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-158">You can also use the `output.Attributes.Add` method to add a tag helper attribute to the end of the collection of tag attributes.</span></span>

1.  <span data-ttu-id="21ff8-159">태그가 업데이트는 *Views/Home/Contact.cshtml* 이러한 변경 내용으로 파일:[!code-html[Main](../../../mvc/views/tag-helpers/authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/Views/Home/ContactCopy.cshtml?highlight=15,16)]</span><span class="sxs-lookup"><span data-stu-id="21ff8-159">Update the markup in the *Views/Home/Contact.cshtml* file with these changes: [!code-html[Main](../../../mvc/views/tag-helpers/authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/Views/Home/ContactCopy.cshtml?highlight=15,16)]</span></span>

2.  <span data-ttu-id="21ff8-160">응용 프로그램을 실행 하 고 올바른 링크를 생성 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-160">Run the app and verify that it generates the correct links.</span></span>
    
    > [!NOTE]
    ><span data-ttu-id="21ff8-161">전자 메일 태그 자체 닫는 작성 하는 경우 (`<email mail-to="Rick" />`), 최종 출력도 자체적으로 닫는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-161">If you were to write the email tag self-closing (`<email mail-to="Rick" />`), the final output would also be self-closing.</span></span> <span data-ttu-id="21ff8-162">시작 태그를 사용 하 여 태그를 작성 하는 기능을 사용 하도록 설정 하려면 (`<email mail-to="Rick">`) 다음을 사용 하 여 클래스를 데코레이팅 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-162">To enable the ability to write the tag with only a start tag (`<email mail-to="Rick">`) you must decorate the class with the following:</span></span>
    >
    > [!code-csharp[Main](../../../mvc/views/tag-helpers/authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/TagHelpers/EmailTagHelperMailVoid.cs?highlight=1&range=6-10)]
    
    <span data-ttu-id="21ff8-163">자체적으로 닫는 전자 메일 태그 도우미 출력 사용할 때 `<a href="mailto:Rick@contoso.com" />`합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-163">With a self-closing email tag helper, the output would be `<a href="mailto:Rick@contoso.com" />`.</span></span> <span data-ttu-id="21ff8-164">자체적으로 닫는 앵커 태그 되지 않으므로 유효한 HTML을 만들라는, 원하지 하지만 자체적으로 닫는 태그 도우미를 만들려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-164">Self-closing anchor tags are not valid HTML, so you wouldn't want to create one, but you might want to create a tag helper that's self-closing.</span></span> <span data-ttu-id="21ff8-165">태그 도우미의 유형을 설정는 `TagMode` 태그를 읽은 후 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-165">Tag helpers set the type of the `TagMode` property after reading a tag.</span></span>
    
### <a name="processasync"></a><span data-ttu-id="21ff8-166">ProcessAsync</span><span class="sxs-lookup"><span data-stu-id="21ff8-166">ProcessAsync</span></span>

<span data-ttu-id="21ff8-167">이 섹션에서는 비동기 전자 메일 도우미를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-167">In this section, we'll write an asynchronous email helper.</span></span>

1.  <span data-ttu-id="21ff8-168">대체는 `EmailTagHelper` 를 다음 코드로 클래스:</span><span class="sxs-lookup"><span data-stu-id="21ff8-168">Replace the `EmailTagHelper` class with the following code:</span></span>

    [!code-csharp[Main](authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/TagHelpers/EmailTagHelper.cs?range=6-17)]

    <span data-ttu-id="21ff8-169">**참고:**</span><span class="sxs-lookup"><span data-stu-id="21ff8-169">**Notes:**</span></span>

    * <span data-ttu-id="21ff8-170">이 버전은 비동기 사용 `ProcessAsync` 메서드.</span><span class="sxs-lookup"><span data-stu-id="21ff8-170">This version uses the asynchronous `ProcessAsync` method.</span></span> <span data-ttu-id="21ff8-171">비동기 `GetChildContentAsync` 반환는 `Task` 포함 하는 `TagHelperContent`합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-171">The asynchronous `GetChildContentAsync` returns a `Task` containing the `TagHelperContent`.</span></span>

    * <span data-ttu-id="21ff8-172">사용 하 여는 `output` HTML 요소의 콘텐츠를 가져오지 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-172">Use the `output` parameter to get contents of the HTML element.</span></span>

2.  <span data-ttu-id="21ff8-173">다음과 같이 변경 하는 *Views/Home/Contact.cshtml* 태그 도우미 대상 전자 메일을 받을 수 있도록 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-173">Make the following change to the *Views/Home/Contact.cshtml* file so the tag helper can get the target email.</span></span>

    [!code-html[Main](../../../mvc/views/tag-helpers/authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/Views/Home/Contact.cshtml?highlight=15,16&range=1-17)]

3.  <span data-ttu-id="21ff8-174">응용 프로그램을 실행 하 고 유효한 전자 메일 링크를 생성 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-174">Run the app and verify that it generates valid email links.</span></span>

### <a name="removeall-precontentsethtmlcontent-and-postcontentsethtmlcontent"></a><span data-ttu-id="21ff8-175">RemoveAll, PreContent.SetHtmlContent and PostContent.SetHtmlContent</span><span class="sxs-lookup"><span data-stu-id="21ff8-175">RemoveAll, PreContent.SetHtmlContent and PostContent.SetHtmlContent</span></span>

1.  <span data-ttu-id="21ff8-176">다음 추가 `BoldTagHelper` 클래스는 *TagHelpers* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-176">Add the following `BoldTagHelper` class to the *TagHelpers* folder.</span></span>

    [!code-csharp[Main](authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/TagHelpers/BoldTagHelper.cs)]

    <span data-ttu-id="21ff8-177">**참고:**</span><span class="sxs-lookup"><span data-stu-id="21ff8-177">**Notes:**</span></span>
    
    * <span data-ttu-id="21ff8-178">`[HtmlTargetElement]` "bold" 이름이 HTML 특성을 포함 하는 HTML 요소를 지정 하는 특성 매개 변수는 일치 하는 전달 특성 및 `Process` 재정의 메서드는 클래스에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-178">The `[HtmlTargetElement]` attribute passes an attribute parameter that specifies that any HTML element that contains an HTML attribute named "bold" will match, and the `Process` override method in the class will run.</span></span> <span data-ttu-id="21ff8-179">이 예제는 `Process` 메서드 "bold" 특성을 제거 하 고 사용 하 여 포함 된 태그를 둘러싸는 `<strong></strong>`합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-179">In our sample, the `Process` method removes the "bold" attribute and surrounds the containing markup with `<strong></strong>`.</span></span>
    
    * <span data-ttu-id="21ff8-180">열기를 작성 해야 콘텐츠 기존 태그를 대체 하지 않으려면 때문에 `<strong>` 사용 하 여 태그는 `PreContent.SetHtmlContent` 메서드와 닫는 `</strong>` 사용 하 여 태그는 `PostContent.SetHtmlContent` 메서드.</span><span class="sxs-lookup"><span data-stu-id="21ff8-180">Because you don't want to replace the existing tag content, you must write the opening `<strong>` tag with the `PreContent.SetHtmlContent` method and the closing `</strong>` tag with the `PostContent.SetHtmlContent` method.</span></span>
    
2.  <span data-ttu-id="21ff8-181">수정 된 *About.cshtml* 포함할 뷰를는 `bold` 특성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-181">Modify the *About.cshtml* view to contain a `bold` attribute value.</span></span> <span data-ttu-id="21ff8-182">완성 된 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-182">The completed code is shown below.</span></span>

    [!code-html[Main](../../../mvc/views/tag-helpers/authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/Views/Home/AboutBoldOnly.cshtml?highlight=7)]

3.  <span data-ttu-id="21ff8-183">앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-183">Run the app.</span></span> <span data-ttu-id="21ff8-184">소스를 검사 하는 태그를 확인 하십시오. 즐겨 찾는 브라우저를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-184">You can use your favorite browser to inspect the source and verify the markup.</span></span>

    <span data-ttu-id="21ff8-185">`[HtmlTargetElement]` 위의 특성에만 "bold"의 특성 이름을 제공 하는 HTML 태그를 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-185">The `[HtmlTargetElement]` attribute above only targets HTML markup that provides an attribute name of "bold".</span></span> <span data-ttu-id="21ff8-186">`<bold>` 요소가 태그 도우미에서 수정 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-186">The `<bold>` element wasn't modified by the tag helper.</span></span>

4. <span data-ttu-id="21ff8-187">주석으로 처리는 `[HtmlTargetElement]` 고 특성 줄을 대상으로 기본값은 `<bold>` 폼의 HTML 태그, 태그 `<bold>`합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-187">Comment out the `[HtmlTargetElement]` attribute line and it will default to targeting `<bold>` tags, that is, HTML markup of the form `<bold>`.</span></span> <span data-ttu-id="21ff8-188">기억, 기본 명명 규칙 클래스 이름과 일치 합니다 **b o l d**TagHelper를 `<bold>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-188">Remember, the default naming convention will match the class name **Bold**TagHelper to `<bold>` tags.</span></span>

5. <span data-ttu-id="21ff8-189">응용 프로그램을 실행 하 고 있는지 확인은 `<bold>` 태그 태그 도우미에 의해 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-189">Run the app and verify that the `<bold>` tag is processed by the tag helper.</span></span>

<span data-ttu-id="21ff8-190">여러 개의 클래스를 데코레이팅하 `[HtmlTargetElement]` 특성 대상의 논리 OR 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-190">Decorating a class with multiple `[HtmlTargetElement]` attributes results in a logical-OR of the targets.</span></span> <span data-ttu-id="21ff8-191">예를 들어 아래 코드를 사용 하 여 굵게 태그 또는 특성 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-191">For example, using the code below, a bold tag or a bold attribute will match.</span></span>

[!code-csharp[Main](../../../mvc/views/tag-helpers/authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/TagHelpers/zBoldTagHelperCopy.cs?highlight=1,2&range=5-15)]

<span data-ttu-id="21ff8-192">동일한 문에서 특성이 여러 개를 추가 하는 경우 런타임에으로 처리할 수 있으며 논리적 AND</span><span class="sxs-lookup"><span data-stu-id="21ff8-192">When multiple attributes are added to the same statement, the runtime treats them as a logical-AND.</span></span> <span data-ttu-id="21ff8-193">예를 들어 아래 코드에는 HTML 요소 이름을 지정 해야 "bold" 라는 특성을 가진 "bold" (`<bold bold />`)와 일치 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-193">For example, in the code below, an HTML element must be named "bold" with an attribute named "bold" (`<bold bold />`) to match.</span></span>

```csharp
[HtmlTargetElement("bold", Attributes = "bold")]
   ```

<span data-ttu-id="21ff8-194">사용할 수도 있습니다는 `[HtmlTargetElement]` 대상 요소의 이름을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-194">You can also use the `[HtmlTargetElement]` to change the name of the targeted element.</span></span> <span data-ttu-id="21ff8-195">예를 들어는 `BoldTagHelper` 대상 `<MyBold>` 태그를 다음 특성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-195">For example if you wanted the `BoldTagHelper` to target `<MyBold>` tags, you would use the following attribute:</span></span>

```csharp
[HtmlTargetElement("MyBold")]
   ```

## <a name="pass-a-model-to-a-tag-helper"></a><span data-ttu-id="21ff8-196">모델 태그 도우미에 전달합니다</span><span class="sxs-lookup"><span data-stu-id="21ff8-196">Pass a model to a Tag Helper</span></span>

1.  <span data-ttu-id="21ff8-197">추가 *모델* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-197">Add a *Models* folder.</span></span>

2.  <span data-ttu-id="21ff8-198">다음 `WebsiteContext` 클래스를 *Models* 폴더에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-198">Add the following `WebsiteContext` class to the *Models* folder:</span></span>

    [!code-csharp[Main](authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/Models/WebsiteContext.cs)]

3.  <span data-ttu-id="21ff8-199">다음 추가 `WebsiteInformationTagHelper` 클래스는 *TagHelpers* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-199">Add the following `WebsiteInformationTagHelper` class to the *TagHelpers* folder.</span></span>

    [!code-csharp[Main](authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/TagHelpers/WebsiteInformationTagHelper.cs)]
    
    <span data-ttu-id="21ff8-200">**참고:**</span><span class="sxs-lookup"><span data-stu-id="21ff8-200">**Notes:**</span></span>
    
    * <span data-ttu-id="21ff8-201">태그 도우미 파스칼식 대/소문자 C# 클래스 이름 및 속성에 대 한 태그 도우미에 대 한 변환에서 설명한 대로 [kebab 대/소문자를 줄이려면](http://wiki.c2.com/?KebabCase)합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-201">As mentioned previously, tag helpers translates Pascal-cased C# class names and properties for tag helpers into [lower kebab case](http://wiki.c2.com/?KebabCase).</span></span> <span data-ttu-id="21ff8-202">따라서 사용 하는 `WebsiteInformationTagHelper` Razor에서 작성 `<website-information />`합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-202">Therefore, to use the `WebsiteInformationTagHelper` in Razor, you'll write `<website-information />`.</span></span>
    
    * <span data-ttu-id="21ff8-203">사용 하 여 대상 요소를 명시적으로 식별 되지 됩니다는 `[HtmlTargetElement]` 특성의 기본값을 `website-information` 대상이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-203">You are not explicitly identifying the target element with the `[HtmlTargetElement]` attribute, so the default of `website-information` will be targeted.</span></span> <span data-ttu-id="21ff8-204">다음 특성 (참고 kebab 사례 되지만 클래스 이름과 일치) 적용 한 경우:</span><span class="sxs-lookup"><span data-stu-id="21ff8-204">If you applied the following attribute (note it's not kebab case but matches the class name):</span></span>
    
    ```csharp
    [HtmlTargetElement("WebsiteInformation")]
    ```
    
    <span data-ttu-id="21ff8-205">더 낮은 kebab 사례 태그 `<website-information />` 일치 하지 않아 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-205">The lower kebab case tag `<website-information />` wouldn't match.</span></span> <span data-ttu-id="21ff8-206">사용 하려는 경우는 `[HtmlTargetElement]` 특성을 아래와 같이 kebab 대/소문자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-206">If you want use the `[HtmlTargetElement]` attribute, you would use kebab case as shown below:</span></span>
    
    ```csharp
    [HtmlTargetElement("Website-Information")]
    ```
    
    * <span data-ttu-id="21ff8-207">자체 닫는 요소에는 내용이 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-207">Elements that are self-closing have no content.</span></span> <span data-ttu-id="21ff8-208">이 예제에 대 한 Razor 태그를 사용 하 여 자체적으로 닫는 태그 이지만 태그 도우미를 만들는 [섹션](http://www.w3.org/TR/html5/sections.html#the-section-element) 요소 (자체적으로 닫는 아닌 고 작성 하는 내 콘텐츠는 `section` 요소).</span><span class="sxs-lookup"><span data-stu-id="21ff8-208">For this example, the Razor markup will use a self-closing tag, but the tag helper will be creating a [section](http://www.w3.org/TR/html5/sections.html#the-section-element) element (which isn't self-closing and you are writing content inside the `section` element).</span></span> <span data-ttu-id="21ff8-209">따라서 설정 해야 `TagMode` 를 `StartTagAndEndTag` 출력을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-209">Therefore, you need to set `TagMode` to `StartTagAndEndTag` to write output.</span></span> <span data-ttu-id="21ff8-210">또는 주석으로 처리 설정 행 `TagMode` 닫는 태그를 사용 하 여 태그를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-210">Alternatively, you can comment out the line setting `TagMode` and write markup with a closing tag.</span></span> <span data-ttu-id="21ff8-211">(이 자습서의 뒷부분에 나오는 예제 태그 제공 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="21ff8-211">(Example markup is provided later in this tutorial.)</span></span>
    
    * <span data-ttu-id="21ff8-212">`$` (달러 기호) 사용 하 여 다음 줄에서 한 [문자열 보간](https://docs.microsoft.com/dotnet/csharp/language-reference/keywords/interpolated-strings):</span><span class="sxs-lookup"><span data-stu-id="21ff8-212">The `$` (dollar sign) in the following line uses an [interpolated string](https://docs.microsoft.com/dotnet/csharp/language-reference/keywords/interpolated-strings):</span></span>
    
    ```cshtml
    $@"<ul><li><strong>Version:</strong> {Info.Version}</li>
    ```

4.  <span data-ttu-id="21ff8-213">다음 태그를 추가 *About.cshtml* 보기.</span><span class="sxs-lookup"><span data-stu-id="21ff8-213">Add the following markup to the *About.cshtml* view.</span></span> <span data-ttu-id="21ff8-214">강조 표시 된 태그는 웹 사이트 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-214">The highlighted markup displays the web site information.</span></span>
    
    [!code-html[Main](authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/Views/Home/About.cshtml?highlight=1,12-)]
    
    >[!NOTE]
    > <span data-ttu-id="21ff8-215">아래에 표시 된 Razor 태그:</span><span class="sxs-lookup"><span data-stu-id="21ff8-215">In the Razor markup shown below:</span></span>
    >
    >[!code-html[Main](authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/Views/Home/About.cshtml?range=13-17)]
    > 
    ><span data-ttu-id="21ff8-216">Razor 알고는 `info` 특성은 문자열이 아닌 클래스 및 C# 코드를 작성 하려면.</span><span class="sxs-lookup"><span data-stu-id="21ff8-216">Razor knows the `info` attribute is a class, not a string, and you want to write C# code.</span></span> <span data-ttu-id="21ff8-217">모든 문자열이 아닌 태그 도우미 특성 없이 쓸지는 `@` 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-217">Any non-string tag helper attribute should be written without the `@` character.</span></span>
    
5.  <span data-ttu-id="21ff8-218">응용 프로그램을 실행 하 고 웹 사이트 정보를 보려면 정보 보기로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-218">Run the app, and navigate to the About view to see the web site information.</span></span>

    >[!NOTE]
    ><span data-ttu-id="21ff8-219">닫는 태그에 다음 태그를 사용 하 고 있는 줄을 제거할 수 있습니다 `TagMode.StartTagAndEndTag` 태그 도우미에서:</span><span class="sxs-lookup"><span data-stu-id="21ff8-219">You can use the following markup with a closing tag and remove the line with `TagMode.StartTagAndEndTag` in the tag helper:</span></span>
    >
    >[!code-html[Main](authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/Views/Home/AboutNotSelfClosing.cshtml?range=13-18)]

## <a name="condition-tag-helper"></a><span data-ttu-id="21ff8-220">조건 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="21ff8-220">Condition Tag Helper</span></span>

<span data-ttu-id="21ff8-221">조건 태그 도우미 true 값을 전달 하는 경우의 출력을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-221">The condition tag helper renders output when passed a true value.</span></span>

1.  <span data-ttu-id="21ff8-222">다음 추가 `ConditionTagHelper` 클래스는 *TagHelpers* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-222">Add the following `ConditionTagHelper` class to the *TagHelpers* folder.</span></span>

    [!code-csharp[Main](authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/TagHelpers/ConditionTagHelper.cs)]

2.  <span data-ttu-id="21ff8-223">내용을 대체는 *Views/Home/Index.cshtml* 다음 태그로 파일:</span><span class="sxs-lookup"><span data-stu-id="21ff8-223">Replace the contents of the *Views/Home/Index.cshtml* file with the following markup:</span></span>

    ```cshtml
    @using AuthoringTagHelpers.Models
    @model WebsiteContext
    
    @{
        ViewData["Title"] = "Home Page";
    }
    
    <div>
        <h3>Information about our website (outdated):</h3>
        <website-information info=@Model />
        <div condition="@Model.Approved">
            <p>
                This website has <strong surround="em"> @Model.Approved </strong> been approved yet.
                Visit www.contoso.com for more information.
            </p>
        </div>
    </div>
    ```
    
3.  <span data-ttu-id="21ff8-224">대체는 `Index` 에서 메서드는 `Home` 를 다음 코드로 컨트롤러:</span><span class="sxs-lookup"><span data-stu-id="21ff8-224">Replace the `Index` method in the `Home` controller with the following code:</span></span>

    [!code-csharp[Main](authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/Controllers/HomeController.cs?range=9-18)]

4.  <span data-ttu-id="21ff8-225">응용 프로그램을 실행 하 고 홈 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-225">Run the app and browse to the home page.</span></span> <span data-ttu-id="21ff8-226">조건부의 태그를 `div` 렌더링 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-226">The markup in the conditional `div` won't be rendered.</span></span> <span data-ttu-id="21ff8-227">쿼리 문자열 추가 `?approved=true` url (예를 들어 `http://localhost:1235/Home/Index?approved=true`).</span><span class="sxs-lookup"><span data-stu-id="21ff8-227">Append the query string `?approved=true` to the URL (for example, `http://localhost:1235/Home/Index?approved=true`).</span></span> <span data-ttu-id="21ff8-228">`approved`가 true로 설정 되었고 조건부 태그 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-228">`approved` is set to true and the conditional markup will be displayed.</span></span>

>[!NOTE]
><span data-ttu-id="21ff8-229">사용 하 여는 [nameof](https://docs.microsoft.com/dotnet/csharp/language-reference/keywords/nameof) 연산자를 굵게 표시 된 태그 도우미에서와 마찬가지로 문자열을 지정 하지 않고 대상에 특성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-229">Use the [nameof](https://docs.microsoft.com/dotnet/csharp/language-reference/keywords/nameof) operator to specify the attribute to target rather than specifying a string as you did with the bold tag helper:</span></span>
>
>[!code-csharp[Main](../../../mvc/views/tag-helpers/authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/TagHelpers/zConditionTagHelperCopy.cs?highlight=1,2,5&range=5-18)]
>
><span data-ttu-id="21ff8-230">[nameof](https://docs.microsoft.com/dotnet/csharp/language-reference/keywords/nameof) 연산자는 보호 코드 해야 것도 리팩터링할 (하도록 이름을 변경 하려는 `RedCondition`) 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-230">The [nameof](https://docs.microsoft.com/dotnet/csharp/language-reference/keywords/nameof) operator will protect the code should it ever be refactored (we might want to change the name to `RedCondition`).</span></span>

### <a name="avoid-tag-helper-conflicts"></a><span data-ttu-id="21ff8-231">태그 도우미 충돌 방지</span><span class="sxs-lookup"><span data-stu-id="21ff8-231">Avoid Tag Helper conflicts</span></span>

<span data-ttu-id="21ff8-232">이 섹션에서는 한 쌍 자동 링크 태그 도우미의 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-232">In this section, you write a pair of auto-linking tag helpers.</span></span> <span data-ttu-id="21ff8-233">첫 번째는 HTML 앵커 태그 동일한 URL이 포함 된 (및 따라서 URL에 대 한 링크를 생성)를 HTTP로 시작 하는 URL을 포함 하는 태그를 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-233">The first will replace markup containing a URL starting with HTTP to an HTML anchor tag containing the same URL (and thus yielding a link to the URL).</span></span> <span data-ttu-id="21ff8-234">두 번째는 동일한 작업을 수행 URL에 대 한 WWW로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-234">The second will do the same for a URL starting with WWW.</span></span>

<span data-ttu-id="21ff8-235">이러한 두 도우미 밀접 한 관련이 있으므로 나중에 리팩터링할 수 있습니다에 같은 파일에 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-235">Because these two helpers are closely related and you may refactor them in the future, we'll keep them in the same file.</span></span>

1.  <span data-ttu-id="21ff8-236">다음 추가 `AutoLinkerHttpTagHelper` 클래스는 *TagHelpers* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-236">Add the following `AutoLinkerHttpTagHelper` class to the *TagHelpers* folder.</span></span>

    [!code-csharp[Main](authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/TagHelpers/z1AutoLinker.cs?range=7-19)]

    >[!NOTE]
    ><span data-ttu-id="21ff8-237">`AutoLinkerHttpTagHelper` 대상 클래스 `p` 요소 및 사용 하 여 [Regex](https://docs.microsoft.com/dotnet/standard/base-types/regular-expression-language-quick-reference) 앵커를 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-237">The `AutoLinkerHttpTagHelper` class targets `p` elements and uses [Regex](https://docs.microsoft.com/dotnet/standard/base-types/regular-expression-language-quick-reference) to create the anchor.</span></span>

2.  <span data-ttu-id="21ff8-238">끝에 다음 태그를 추가 *Views/Home/Contact.cshtml* 파일:</span><span class="sxs-lookup"><span data-stu-id="21ff8-238">Add the following markup to the end of the *Views/Home/Contact.cshtml* file:</span></span>

    [!code-html[Main](../../../mvc/views/tag-helpers/authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/Views/Home/Contact.cshtml?highlight=19)]

3.  <span data-ttu-id="21ff8-239">응용 프로그램을 실행 하 고 태그 도우미가 앵커를 제대로 렌더링 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-239">Run the app and verify that the tag helper renders the anchor correctly.</span></span>

4.  <span data-ttu-id="21ff8-240">업데이트는 `AutoLinker` 포함 하도록 클래스는 `AutoLinkerWwwTagHelper` www 텍스트도 원래 www 텍스트를 포함 하는 앵커 태그를 변환 됩니다입니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-240">Update the `AutoLinker` class to include the `AutoLinkerWwwTagHelper` which will convert www text to an anchor tag that also contains the original www text.</span></span> <span data-ttu-id="21ff8-241">업데이트 된 코드는 아래 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-241">The updated code is highlighted below:</span></span>

    [!code-csharp[Main](authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/TagHelpers/z1AutoLinker.cs?highlight=15-34&range=7-34)]

5.  <span data-ttu-id="21ff8-242">앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-242">Run the app.</span></span> <span data-ttu-id="21ff8-243">필름 www 텍스트를 한 링크로 렌더링 되지만 HTTP 텍스트 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-243">Notice the www text is rendered as a link but the HTTP text isn't.</span></span> <span data-ttu-id="21ff8-244">두 클래스에 중단점을 배치 하면 HTTP 태그 도우미 클래스 첫 번째 실행 되는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-244">If you put a break point in both classes, you can see that the HTTP tag helper class runs first.</span></span> <span data-ttu-id="21ff8-245">문제는 태그 도우미 출력에 캐시 되며 HTTP 태그 도우미의 캐시 된 출력 덮어씁니다 WWW 태그 도우미를 실행 하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-245">The problem is that the tag helper output is cached, and when the WWW tag helper is run, it overwrites the cached output from the HTTP tag helper.</span></span> <span data-ttu-id="21ff8-246">이 자습서의 뒷부분에 나오는 태그 도우미에서 실행 되는 순서를 제어 하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-246">Later in the tutorial we'll see how to control the order that tag helpers run in.</span></span> <span data-ttu-id="21ff8-247">다음 코드를 수정 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-247">We'll fix the code with the following:</span></span>

    [!code-csharp[Main](../../../mvc/views/tag-helpers/authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/TagHelpers/z1AutoLinkerCopy.cs?highlight=5,6,10,21,22,26&range=8-37)]

    >[!NOTE]
    ><span data-ttu-id="21ff8-248">자동 링크 태그 도우미의 첫 번째 버전을 다음 코드로 대상의 내용을 가져온:</span><span class="sxs-lookup"><span data-stu-id="21ff8-248">In the first edition of the auto-linking tag helpers, you got the content of the target with the following code:</span></span>
    >
    >[!code-csharp[Main](authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/TagHelpers/z1AutoLinker.cs?range=12)]
    >
    ><span data-ttu-id="21ff8-249">즉, 호출 `GetChildContentAsync` 를 사용 하는 `TagHelperOutput` 에 전달 되는 `ProcessAsync` 메서드.</span><span class="sxs-lookup"><span data-stu-id="21ff8-249">That is, you call `GetChildContentAsync` using the `TagHelperOutput` passed into the `ProcessAsync` method.</span></span> <span data-ttu-id="21ff8-250">언급 한 것 처럼 이전에 출력 캐시 되므로 마지막 태그 wins를 실행 하는 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-250">As mentioned previously, because the output is cached, the last tag helper to run wins.</span></span> <span data-ttu-id="21ff8-251">다음 코드와 함께 해당 문제가 해결:</span><span class="sxs-lookup"><span data-stu-id="21ff8-251">You fixed that problem with the following code:</span></span>
    >
    >[!code-csharp[Main](authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/TagHelpers/z2AutoLinkerCopy.cs?range=34-35)]
    >
    ><span data-ttu-id="21ff8-252">위의 코드 콘텐츠가 수정 된 출력 버퍼에서 콘텐츠를 가져옵니다 적 하는 경우를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-252">The code above checks to see if the content has been modified, and if it has, it gets the content from the output buffer.</span></span>

6.  <span data-ttu-id="21ff8-253">응용 프로그램을 실행 하 고 두 개의 링크가 예상 대로 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-253">Run the app and verify that the two links work as expected.</span></span> <span data-ttu-id="21ff8-254">우리의 자동 링커 태그 도우미는 완벽 한 상태가 나타날 수 있습니다, 미묘한 문제가 이었지만 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-254">While it might appear our auto linker tag helper is correct and complete, it has a subtle problem.</span></span> <span data-ttu-id="21ff8-255">WWW 태그 도우미 실행 될 경우 첫 번째, www 링크 올바른 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-255">If the WWW tag helper runs first, the www links won't be correct.</span></span> <span data-ttu-id="21ff8-256">코드를 추가 하 여 업데이트 된 `Order` 태그에서 실행 되는 순서를 제어 하는 오버 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-256">Update the code by adding the `Order` overload to control the order that the tag runs in.</span></span> <span data-ttu-id="21ff8-257">`Order` 속성 같은 요소를 대상으로 하는 다른 태그 도우미를 기준으로 실행 순서를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-257">The `Order` property determines the execution order relative to other tag helpers targeting the same element.</span></span> <span data-ttu-id="21ff8-258">기본 순서 값은 0이 고 더 낮은 값이 있는 인스턴스를 먼저 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-258">The default order value is zero and instances with lower values are executed first.</span></span>

    [!code-csharp[Main](authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/TagHelpers/z2AutoLinkerCopy.cs?highlight=5,6,7,8&range=8-15)]
    
    <span data-ttu-id="21ff8-259">위의 코드는 HTTP 태그 도우미 WWW 태그 도우미 하기 전에 실행 되도록 보장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-259">The above code will guarantee that the HTTP tag helper runs before the WWW tag helper.</span></span> <span data-ttu-id="21ff8-260">변경 `Order` 를 `MaxValue` WWW 태그에 대 한 생성 된 태그 올바른지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-260">Change `Order` to `MaxValue` and verify that the markup generated for the WWW tag is incorrect.</span></span>

## <a name="inspect-and-retrieve-child-content"></a><span data-ttu-id="21ff8-261">검사 하 고 자식 콘텐츠를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-261">Inspect and retrieve child content</span></span>

<span data-ttu-id="21ff8-262">태그 도우미 콘텐츠를 검색 하도록 여러 가지 속성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-262">The tag helpers provide several properties to retrieve content.</span></span>

-  <span data-ttu-id="21ff8-263">결과 `GetChildContentAsync` 추가할 수 있는 `output.Content`합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-263">The result of `GetChildContentAsync` can be appended to `output.Content`.</span></span>
-  <span data-ttu-id="21ff8-264">결과 검사할 수 `GetChildContentAsync` 와 `GetContent`합니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-264">You can inspect the result of `GetChildContentAsync` with `GetContent`.</span></span>
-  <span data-ttu-id="21ff8-265">수정 하는 경우 `output.Content`, TagHelper 본문을 실행 되거나 호출 하지 않으면 렌더링 되지 않습니다 `GetChildContentAsync` 자동 링커 샘플에서와 같이:</span><span class="sxs-lookup"><span data-stu-id="21ff8-265">If you modify `output.Content`, the TagHelper body won't be executed or rendered unless you call `GetChildContentAsync` as in our auto-linker sample:</span></span>

[!code-csharp[Main](../../views/tag-helpers/authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/TagHelpers/z1AutoLinkerCopy.cs?highlight=5,6,10&range=8-21)]

-  <span data-ttu-id="21ff8-266">여러 번 호출 `GetChildContentAsync` 같은 값을 반환 하 고 다시 실행 하지 않습니다는 `TagHelper` 를 캐시 된 결과 사용 하지 않는 나타내는 false 매개 변수를 전달 하지 않으면 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="21ff8-266">Multiple calls to `GetChildContentAsync` returns the same value and doesn't re-execute the `TagHelper` body unless you pass in a false parameter indicating not to use the cached result.</span></span>
