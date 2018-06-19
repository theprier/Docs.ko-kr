---
uid: mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-vb
title: HTML 도우미 (VB)를 TagBuilder 클래스를 사용 하 여 | Microsoft Docs
author: StephenWalther
description: Stephen Walther TagBuilder 클래스의 이름을 ASP.NET MVC 프레임 워크에 유용한 유틸리티 클래스를 소개 합니다. TagBuilder 클래스를 쉽게 사용할 수 있습니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/02/2009
ms.topic: article
ms.assetid: ec26f264-d0ea-4031-9943-825505a3ac4b
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-vb
msc.type: authoredcontent
ms.openlocfilehash: 2b72e08dff646f66252f210543230186cab6e641
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30872233"
---
<a name="using-the-tagbuilder-class-to-build-html-helpers-vb"></a><span data-ttu-id="be4fd-104">HTML 도우미 (VB)를 TagBuilder 클래스를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="be4fd-104">Using the TagBuilder Class to Build HTML Helpers (VB)</span></span>
====================
<span data-ttu-id="be4fd-105">으로 [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="be4fd-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="be4fd-106">Stephen Walther TagBuilder 클래스의 이름을 ASP.NET MVC 프레임 워크에 유용한 유틸리티 클래스를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-106">Stephen Walther introduces you to a useful utility class in the ASP.NET MVC framework named the TagBuilder class.</span></span> <span data-ttu-id="be4fd-107">HTML 태그를 손쉽게 바인딩할 TagBuilder 클래스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-107">You can use the TagBuilder class to easily build HTML tags.</span></span>


<span data-ttu-id="be4fd-108">ASP.NET MVC 프레임 워크에는 HTML 도우미를 작성할 때 사용할 수 있는 TagBuilder 클래스 라는 유용한 유틸리티 클래스가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-108">The ASP.NET MVC framework includes a useful utility class named the TagBuilder class that you can use when building HTML helpers.</span></span> <span data-ttu-id="be4fd-109">TagBuilder 클래스 클래스의 이름에서 알 수 있듯이 사용 하면 HTML 태그를 쉽게 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-109">The TagBuilder class, as the name of the class suggests, enables you to easily build HTML tags.</span></span> <span data-ttu-id="be4fd-110">이 간략 한 자습서에서 제공 됩니다 TagBuilder 클래스의 개요 및 HTML을 렌더링 하는 간단한 HTML 도우미를 작성할 때이 클래스를 사용 하는 방법을 알아봅니다 &lt;img&gt; 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-110">In this brief tutorial, you are provided with an overview of the TagBuilder class and you learn how to use this class when building a simple HTML helper that renders HTML &lt;img&gt; tags.</span></span>

## <a name="overview-of-the-tagbuilder-class"></a><span data-ttu-id="be4fd-111">TagBuilder 클래스의 개요</span><span class="sxs-lookup"><span data-stu-id="be4fd-111">Overview of the TagBuilder Class</span></span>

<span data-ttu-id="be4fd-112">TagBuilder 클래스 System.Web.Mvc 네임 스페이스에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-112">The TagBuilder class is contained in the System.Web.Mvc namespace.</span></span> <span data-ttu-id="be4fd-113">다섯 가지 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-113">It has five methods:</span></span>

- <span data-ttu-id="be4fd-114">AddCssClass()-를 사용 하면 새 *클래스 = ""* 태그에 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-114">AddCssClass() – Enables you to add a new *class=""* attribute to a tag.</span></span>
- <span data-ttu-id="be4fd-115">GenerateId() – 태그에 id 특성을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-115">GenerateId() – Enables you to add an id attribute to a tag.</span></span> <span data-ttu-id="be4fd-116">이 메서드는 id에서 마침표를 대체 자동으로 (기본적으로 마침표 밑줄로 바뀝니다)</span><span class="sxs-lookup"><span data-stu-id="be4fd-116">This method automatically replaces periods in the id (by default, periods are replaced by underscores)</span></span>
- <span data-ttu-id="be4fd-117">MergeAttribute()-를 사용 하는 태그 특성을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-117">MergeAttribute() – Enables you to add attributes to a tag.</span></span> <span data-ttu-id="be4fd-118">이 메서드의 오버 로드를 여러 개 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-118">There are multiple overloads of this method.</span></span>
- <span data-ttu-id="be4fd-119">SetInnerText()-를 사용 하는 태그의 내부 텍스트를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-119">SetInnerText() – Enables you to set the inner text of the tag.</span></span> <span data-ttu-id="be4fd-120">내부 텍스트는 HTML로 자동으로 인코드 합니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-120">The inner text is HTML encode automatically.</span></span>
- <span data-ttu-id="be4fd-121">Tostring ()-를 사용 하면 태그를 렌더링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-121">ToString() – Enables you to render the tag.</span></span> <span data-ttu-id="be4fd-122">일반 태그, 시작 태그, 끝 태그 또는 자체적으로 닫는 태그를 만들 것인지 여부를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-122">You can specify whether you want to create a normal tag, a start tag, an end tag, or a self-closing tag.</span></span>
  

<span data-ttu-id="be4fd-123">TagBuilder 클래스에 4 개의 중요 한 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-123">The TagBuilder class has four important properties:</span></span>

- <span data-ttu-id="be4fd-124">특성-모든 태그의 특성을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-124">Attributes – Represents all of the attributes of the tag.</span></span>
- <span data-ttu-id="be4fd-125">IdAttributeDotReplacement – 마침표 (기본값은 밑줄)를 바꾸는 GenerateId() 메서드에서 사용 되는 문자를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-125">IdAttributeDotReplacement – Represents the character used by the GenerateId() method to replace periods (the default is an underscore).</span></span>
- <span data-ttu-id="be4fd-126">InnerHTML – 내부 태그의 내용을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-126">InnerHTML – Represents the inner contents of the tag.</span></span> <span data-ttu-id="be4fd-127">이 속성에 문자열을 할당 *없는* 문자열을 HTML로 인코드 합니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-127">Assigning a string to this property *does not* HTML encode the string.</span></span>
- <span data-ttu-id="be4fd-128">TagName – 태그의 이름을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-128">TagName – Represents the name of the tag.</span></span>

<span data-ttu-id="be4fd-129">이러한 메서드 및 속성 사용 하면 모든 기본 메서드 및 속성의 HTML 태그를 작성 해야 하는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-129">These methods and properties give you all of the basic methods and properties that you need to build up an HTML tag.</span></span> <span data-ttu-id="be4fd-130">실제로 TagBuilder 클래스를 사용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-130">You don't really need to use the TagBuilder class.</span></span> <span data-ttu-id="be4fd-131">StringBuilder 클래스를 대신 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-131">You could use a StringBuilder class instead.</span></span> <span data-ttu-id="be4fd-132">그러나 TagBuilder 클래스를 사용 하 여 수명의 좀 더 쉽게 합니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-132">However, the TagBuilder class makes your life a little easier.</span></span>

## <a name="creating-an-image-html-helper"></a><span data-ttu-id="be4fd-133">이미지 HTML 도우미 만들기</span><span class="sxs-lookup"><span data-stu-id="be4fd-133">Creating an Image HTML Helper</span></span>

<span data-ttu-id="be4fd-134">TagBuilder 클래스의 인스턴스를 만들 때 TagBuilder 생성자를 작성 하려면 하는 태그의 이름을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-134">When you create an instance of the TagBuilder class, you pass the name of the tag that you want to build to the TagBuilder constructor.</span></span> <span data-ttu-id="be4fd-135">다음으로 태그의 특성을 수정 하려면 AddCssClass 및 MergeAttribute() 메서드 등의 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-135">Next, you can call methods like the AddCssClass and MergeAttribute() methods to modify the attributes of the tag.</span></span> <span data-ttu-id="be4fd-136">마지막으로 태그를 렌더링 하 tostring () 메서드를 호출 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-136">Finally, you call the ToString() method to render the tag.</span></span>

<span data-ttu-id="be4fd-137">예를 들어 목록 1 이미지 HTML 도우미를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-137">For example, Listing 1 contains an Image HTML helper.</span></span> <span data-ttu-id="be4fd-138">이미지 도우미와 HTML을 나타내는 TagBuilder 내부적으로 구현 됩니다 &lt;img&gt; 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-138">The Image helper is implemented internally with a TagBuilder that represents an HTML &lt;img&gt; tag.</span></span>

<span data-ttu-id="be4fd-139">**Listing 1 – Helpers\ImageHelper.vb**</span><span class="sxs-lookup"><span data-stu-id="be4fd-139">**Listing 1 – Helpers\ImageHelper.vb**</span></span>

[!code-vb[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample1.vb)]

<span data-ttu-id="be4fd-140">모듈 목록 1에 Image() 라는 두 개의 오버 로드 된 메서드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-140">The module in Listing 1 contains two overloaded methods named Image().</span></span> <span data-ttu-id="be4fd-141">Image() 메서드를 호출할 때 또는 HTML 특성의 집합을 나타내는 개체를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-141">When you call the Image() method, you can pass an object which represents a set of HTML attributes or not.</span></span>

<span data-ttu-id="be4fd-142">TagBuilder.MergeAttribute() 메서드를 사용 하 여 TagBuilder에 src 특성 등의 개별 특성을 추가 하는 방법을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-142">Notice how the TagBuilder.MergeAttribute() method is used to add individual attributes such as the src attribute to the TagBuilder.</span></span> <span data-ttu-id="be4fd-143">또한 알 TagBuilder.MergeAttributes() 메서드를 사용 하 여 TagBuilder에 특성의 컬렉션을 추가 하는 방법을 합니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-143">Notice, furthermore, how the TagBuilder.MergeAttributes() method is used to add a collection of attributes to the TagBuilder.</span></span> <span data-ttu-id="be4fd-144">MergeAttributes() 메서드에 사전&lt;문자열, o b j&gt; 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-144">The MergeAttributes() method accepts a Dictionary&lt;string,object&gt; parameter.</span></span> <span data-ttu-id="be4fd-145">RouteValueDictionary 클래스는 리소스를 사전에 특성의 컬렉션을 나타내는 개체를 변환 하는 데 사용&lt;문자열, o b j&gt;합니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-145">The RouteValueDictionary class is used to convert the Object representing the collection of attributes into a Dictionary&lt;string,object&gt;.</span></span>

<span data-ttu-id="be4fd-146">이미지 도우미를 만든 후에 다른 표준 HTML 도우미 중 하나라도 마찬가지로 사용해 ASP.NET MVC 뷰에 도우미를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-146">After you create the Image helper, you can use the helper in your ASP.NET MVC views just like any of the other standard HTML helpers.</span></span> <span data-ttu-id="be4fd-147">보기 목록 2에 이미지 도우미를 사용 하 여 Xbox의 동일한 이미지를 두 번 표시 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="be4fd-147">The view in Listing 2 uses the Image helper to display the same image of an Xbox twice (see Figure 1).</span></span> <span data-ttu-id="be4fd-148">Image() 도우미를 사용 하거나 사용 된 HTML 특성 컬렉션이 없으면 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-148">The Image() helper is called both with and without an HTML attribute collection.</span></span>

<span data-ttu-id="be4fd-149">**Listing 2 – Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="be4fd-149">**Listing 2 – Home\Index.aspx**</span></span>

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample2.aspx)]


<span data-ttu-id="be4fd-150">[![새 프로젝트 대화 상자](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="be4fd-150">[![The New Project dialog box](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.png)</span></span>

<span data-ttu-id="be4fd-151">**그림 01**: 이미지 도우미를 사용 하 여 ([전체 크기 이미지를 보려면 클릭](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="be4fd-151">**Figure 01**: Using the Image helper([Click to view full-size image](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image2.png))</span></span>


<span data-ttu-id="be4fd-152">공지 Index.aspx 보기의 맨 위쪽에 이미지 도우미에 연결 된 네임 스페이스를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-152">Notice that you must import the namespace associated with the Image helper at the top of the Index.aspx view.</span></span> <span data-ttu-id="be4fd-153">도우미는 다음 지시문으로 가져오게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-153">The helper is imported with the following directive:</span></span>

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample3.aspx)]

<span data-ttu-id="be4fd-154">Visual Basic 응용 프로그램에서는 기본 네임 스페이스는 응용 프로그램의 이름으로 같습니다.</span><span class="sxs-lookup"><span data-stu-id="be4fd-154">In a Visual Basic application, the default namespace is the same as the name of the application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="be4fd-155">[이전](creating-custom-html-helpers-vb.md)
> [다음](creating-page-layouts-with-view-master-pages-vb.md)</span><span class="sxs-lookup"><span data-stu-id="be4fd-155">[Previous](creating-custom-html-helpers-vb.md)
[Next](creating-page-layouts-with-view-master-pages-vb.md)</span></span>
