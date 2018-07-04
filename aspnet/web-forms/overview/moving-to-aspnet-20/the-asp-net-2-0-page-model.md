---
uid: web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
title: ASP.NET 2.0 페이지 모델 | Microsoft Docs
author: microsoft
description: Asp.net에서 1.x에서 개발자는 인라인 코드 모델 및 코드 숨김 코드 모델 중에서 선택 해야 했습니다. 코드 숨김의 Src attr 중 하나를 사용 하 여 구현할 수 있습니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2005
ms.topic: article
ms.assetid: af4575a3-0ae3-4638-ba4d-218fad7a1642
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
msc.type: authoredcontent
ms.openlocfilehash: 9d62aee5e0754b1910b923ad9ae501ebed91097e
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37379889"
---
<a name="the-aspnet-20-page-model"></a><span data-ttu-id="f2fa7-104">ASP.NET 2.0 페이지 모델</span><span class="sxs-lookup"><span data-stu-id="f2fa7-104">The ASP.NET 2.0 Page Model</span></span>
====================
<span data-ttu-id="f2fa7-105">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="f2fa7-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="f2fa7-106">Asp.net에서 1.x에서 개발자는 인라인 코드 모델 및 코드 숨김 코드 모델 중에서 선택 해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-106">In ASP.NET 1.x, developers had a choice between an inline code model and a code-behind code model.</span></span> <span data-ttu-id="f2fa7-107">코드 숨김 Src 특성 또는 코드 숨김 특성을 사용 하 여 구현할 수는 @Page 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-107">Code-behind could be implemented using either the Src attribute or the CodeBehind attribute of the @Page directive.</span></span> <span data-ttu-id="f2fa7-108">ASP.NET 2.0에서는 개발자에 게 아직 인라인 코드와 코드 숨김 하지만 코드 숨김 모델을 크게 향상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-108">In ASP.NET 2.0, developers still have a choice between inline code and code-behind, but there have been significant enhancements to the code-behind model.</span></span>


<span data-ttu-id="f2fa7-109">Asp.net에서 1.x에서 개발자는 인라인 코드 모델 및 코드 숨김 코드 모델 중에서 선택 해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-109">In ASP.NET 1.x, developers had a choice between an inline code model and a code-behind code model.</span></span> <span data-ttu-id="f2fa7-110">코드 숨김 Src 특성 또는 코드 숨김 특성을 사용 하 여 구현할 수는 @Page 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-110">Code-behind could be implemented using either the Src attribute or the CodeBehind attribute of the @Page directive.</span></span> <span data-ttu-id="f2fa7-111">ASP.NET 2.0에서는 개발자에 게 아직 인라인 코드와 코드 숨김 하지만 코드 숨김 모델을 크게 향상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-111">In ASP.NET 2.0, developers still have a choice between inline code and code-behind, but there have been significant enhancements to the code-behind model.</span></span>

## <a name="improvements-in-the-code-behind-model"></a><span data-ttu-id="f2fa7-112">코드 숨김 모델의 향상 된 기능</span><span class="sxs-lookup"><span data-stu-id="f2fa7-112">Improvements in the Code-Behind Model</span></span>

<span data-ttu-id="f2fa7-113">ASP.NET에 존재 하므로 모델을 신속 하 게 검토 것이 가장 좋습니다 ASP.NET 2.0의 코드 숨김 모델의 변경 내용의 완벽 하 게 이해 하려면 1.x 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-113">In order to fully understand the changes in the code-behind model in ASP.NET 2.0, its best to quickly review the model as it existed in ASP.NET 1.x.</span></span>

## <a name="the-code-behind-model-in-aspnet-1x"></a><span data-ttu-id="f2fa7-114">Asp.net에서 코드 숨김 모델 1.x</span><span class="sxs-lookup"><span data-stu-id="f2fa7-114">The Code-Behind Model in ASP.NET 1.x</span></span>

<span data-ttu-id="f2fa7-115">Asp.net에서 1.x에서 ASPX 파일 (Webform) 및 프로그래밍 코드를 포함 하는 코드 숨김 파일의 코드 숨김 모델 구성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-115">In ASP.NET 1.x, the code-behind model consisted of an ASPX file (the Webform) and a code-behind file containing programming code.</span></span> <span data-ttu-id="f2fa7-116">두 개의 파일을 사용 하 여 연결 된 된 @Page ASPX 파일에서 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-116">The two files were connected using the @Page directive in the ASPX file.</span></span> <span data-ttu-id="f2fa7-117">ASPX 페이지에 있는 각 컨트롤 인스턴스에 변수로 코드 숨김 파일에 해당 선언이 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-117">Each control on the ASPX page had a corresponding declaration in the code-behind file as an instance variable.</span></span> <span data-ttu-id="f2fa7-118">또한 코드 숨김 파일 이벤트 바인딩에 대 한 코드를 포함 하 고 Visual Studio 디자이너에 필요한 코드를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-118">The code-behind file also contained code for event binding and generated code necessary for the Visual Studio designer.</span></span> <span data-ttu-id="f2fa7-119">이 모델도 꽤 잘 작동 하지만 ASPX 페이지에서 모든 ASP.NET 요소 코드 숨김 파일에 해당 하는 코드를 필요 하기 때문에 코드 및 콘텐츠 true 분리할 수 없습니다. 없었습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-119">This model worked fairly well, but because every ASP.NET element in the ASPX page required corresponding code in the code-behind file, there was no true separation of code and content.</span></span> <span data-ttu-id="f2fa7-120">예를 들어, 디자이너가 Visual Studio IDE 외부에서 ASPX 파일에 새 서버 컨트롤을 추가 하는 경우 응용 프로그램 해당 컨트롤에 대 한 선언 없어서 코드 숨김 파일에 중단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-120">For example, if a designer added a new server control to an ASPX file outside of the Visual Studio IDE, the application would break due to the absence of a declaration for that control in the code-behind file.</span></span>

## <a name="the-code-behind-model-in-aspnet-20"></a><span data-ttu-id="f2fa7-121">ASP.NET 2.0의에서 코드 숨김 모델</span><span class="sxs-lookup"><span data-stu-id="f2fa7-121">The Code-Behind Model in ASP.NET 2.0</span></span>

<span data-ttu-id="f2fa7-122">ASP.NET 2.0이이 모델 크게 개선합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-122">ASP.NET 2.0 greatly improves upon this model.</span></span> <span data-ttu-id="f2fa7-123">ASP.NET 2.0의 코드 숨김 새를 사용 하 여 구현 됩니다 *partial 클래스* ASP.NET 2.0에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-123">In ASP.NET 2.0, code-behind is implemented using the new *partial classes* provided in ASP.NET 2.0.</span></span> <span data-ttu-id="f2fa7-124">ASP.NET 2.0의 코드 숨김 클래스를 클래스 정의의 일부로 있음을 의미 하는 partial 클래스로 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-124">The code-behind class in ASP.NET 2.0 is definied as a partial class meaning that it contains only part of the class definition.</span></span> <span data-ttu-id="f2fa7-125">클래스 정의의 남은 부분 런타임에 또는 웹 사이트 미리 컴파일 되었는지 ASPX 페이지를 사용 하 여 ASP.NET 2.0에 의해 동적으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-125">The remaining part of the class definition is dynamically generated by ASP.NET 2.0 using the ASPX page at runtime or when the Web site is precompiled.</span></span> <span data-ttu-id="f2fa7-126">코드 숨김 파일 및 ASPX 페이지 간의 링크는 여전히 @ Page 지시문을 사용 하 여 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-126">The link between the code-behind file and the ASPX page is still established using the @ Page directive.</span></span> <span data-ttu-id="f2fa7-127">그러나 코드 숨김 또는 Src 특성을 대신 ASP.NET 2.0 이제 CodeFile는 특성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-127">However, instead of a CodeBehind or Src attribute, ASP.NET 2.0 now uses the CodeFile attribute.</span></span> <span data-ttu-id="f2fa7-128">Inherits 특성 페이지에 대 한 클래스 이름을 지정 하도 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-128">The Inherits attribute is also used to specify the class name for the page.</span></span>

<span data-ttu-id="f2fa7-129">일반적인 @ Page 지시문이 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-129">A typical @ Page directive might look like this:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample1.aspx)]

<span data-ttu-id="f2fa7-130">ASP.NET 2.0 코드 숨김 파일에는 일반적인 클래스 정의 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-130">A typical class definition in an ASP.NET 2.0 code-behind file might look like this:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample2.cs)]

> [!NOTE]
> <span data-ttu-id="f2fa7-131">C# 및 Visual Basic은 현재 partial 클래스를 지원 합니다만 관리 되는 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-131">C# and Visual Basic are the only managed languages that currently support partial classes.</span></span> <span data-ttu-id="f2fa7-132">따라서 J#을 사용 하는 개발자가 ASP.NET 2.0의 코드 숨김 모델을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-132">Therefore, developers using J# will not be able to use the code-behind model in ASP.NET 2.0.</span></span>


<span data-ttu-id="f2fa7-133">개발자는 자신이 만든 코드를 포함 하는 코드 파일을 이제는 때문에 코드 숨김 모델을 향상 하는 새 모델.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-133">The new model enhances the code-behind model because developers will now have code files that contain only the code that they have created.</span></span> <span data-ttu-id="f2fa7-134">또한 제공 코드 및 콘텐츠 true 분리에 대 한 코드 숨김 파일에 인스턴스 변수 선언이 없으면 있기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-134">It also provides for a true separation of code and content because there are no instance variable declarations in the code-behind file.</span></span>

> [!NOTE]
> <span data-ttu-id="f2fa7-135">ASPX 페이지에 대 한 partial 클래스 이벤트 바인딩이 수행 이기 때문에 Visual Basic 개발자는 코드 숨김에서 이벤트에 바인딩할 Handles 키워드를 사용 하 여 성능이 약간 향상을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-135">Because the partial class for the ASPX page is where event binding takes place, Visual Basic developers can realize a slight performance increase by using the Handles keyword in code-behind to bind events.</span></span> <span data-ttu-id="f2fa7-136">C#에 해당 하는 키워드가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-136">C# has no equivalent keyword.</span></span>


## <a name="new--page-directive-attributes"></a><span data-ttu-id="f2fa7-137">새 @ Page 지시문 특성</span><span class="sxs-lookup"><span data-stu-id="f2fa7-137">New @ Page Directive Attributes</span></span>

<span data-ttu-id="f2fa7-138">ASP.NET 2.0의 @ Page 지시문에 많은 새 특성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-138">ASP.NET 2.0 adds many new attributes to the @ Page directive.</span></span> <span data-ttu-id="f2fa7-139">다음 특성은 ASP.NET 2.0의 새로운 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-139">The following attributes are new in ASP.NET 2.0.</span></span>

## <a name="async"></a><span data-ttu-id="f2fa7-140">Async</span><span class="sxs-lookup"><span data-stu-id="f2fa7-140">Async</span></span>

<span data-ttu-id="f2fa7-141">비동기 특성을 사용 하면 비동기적으로 실행 되는 페이지를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-141">The Async attribute allows you to configure page to be executed asynchronously.</span></span> <span data-ttu-id="f2fa7-142">나중에이 모듈의에서 비동기 페이지도 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-142">Well cover asynchronous pages later in this module.</span></span>

## <a name="asynctimeout"></a><span data-ttu-id="f2fa7-143">AsyncTimeout</span><span class="sxs-lookup"><span data-stu-id="f2fa7-143">AsyncTimeout</span></span>

<span data-ttu-id="f2fa7-144">비동기 페이지에 대 한 제한 시간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-144">Specified the timeout for asynchronous pages.</span></span> <span data-ttu-id="f2fa7-145">기본값은 45 초입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-145">The default is 45 seconds.</span></span>

## <a name="codefile"></a><span data-ttu-id="f2fa7-146">CodeFile</span><span class="sxs-lookup"><span data-stu-id="f2fa7-146">CodeFile</span></span>

<span data-ttu-id="f2fa7-147">CodeFile 특성은 코드 숨김 특성이 Visual Studio 2002/2003에 대 한 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-147">The CodeFile attribute is the replacement for the CodeBehind attribute in Visual Studio 2002/2003.</span></span>

### <a name="codefilebaseclass"></a><span data-ttu-id="f2fa7-148">CodeFileBaseClass</span><span class="sxs-lookup"><span data-stu-id="f2fa7-148">CodeFileBaseClass</span></span>

<span data-ttu-id="f2fa7-149">CodeFileBaseClass 특성은 단일 기본 클래스에서 파생 시키는 여러 페이지를 하려는 경우에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-149">The CodeFileBaseClass attribute is used in cases where you want multiple pages to derive from a single base class.</span></span> <span data-ttu-id="f2fa7-150">이 특성이 없으면 ASP.NET에서 partial 클래스의 구현으로 인해 공유 공통 필드를 사용 하 여 ASPX 페이지에 선언 된 컨트롤이 참조 하는 기본 클래스는 제대로 작동 하지 때문에 ASP 합니다. 네트워크 컴파일 엔진 페이지의 컨트롤을 기반으로 하는 새 멤버를 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-150">Because of the implementation of partial classes in ASP.NET, without this attribute, a base class that uses shared common fields to reference controls declared in an ASPX page would not work properly because ASP.NETs compilation engine will automatically create new members based on controls in the page.</span></span> <span data-ttu-id="f2fa7-151">따라서 ASP.NET의 두 개 이상의 페이지에 대 한 공통 기본 클래스를 하려는 경우를 정의 해야 CodeFileBaseClass 특성의 기본 클래스를 지정 하 고 해당 기본 클래스에서 각 페이지 클래스를 파생 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-151">Therefore, if you want a common base class for two or more pages in ASP.NET, you will need to define specify your base class in the CodeFileBaseClass attribute and then derive each pages class from that base class.</span></span> <span data-ttu-id="f2fa7-152">CodeFile 특성이이 특성을 사용 하는 경우에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-152">The CodeFile attribute is also required when this attribute is used.</span></span>

## <a name="compilationmode"></a><span data-ttu-id="f2fa7-153">CompilationMode</span><span class="sxs-lookup"><span data-stu-id="f2fa7-153">CompilationMode</span></span>

<span data-ttu-id="f2fa7-154">이 특성을 사용 하면 ASPX 페이지의 CompilationMode 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-154">This attribute allows you to set the CompilationMode property of the ASPX page.</span></span> <span data-ttu-id="f2fa7-155">CompilationMode 속성은 값을 포함 하는 열거형 **항상**를 **자동**, 및 **Never**합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-155">The CompilationMode property is an enumeration containing the values **Always**, **Auto**, and **Never**.</span></span> <span data-ttu-id="f2fa7-156">기본값은 **항상**합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-156">The default is **Always**.</span></span> <span data-ttu-id="f2fa7-157">합니다 **자동** 설정을 동적으로 가능한 경우 페이지를 컴파일되지 ASP.NET 못합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-157">The **Auto** setting will prevent ASP.NET from dynamically compiling the page if possible.</span></span> <span data-ttu-id="f2fa7-158">페이지를 제외 하 고 동적 컴파일에서 성능을 향상 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-158">Excluding pages from dynamic compilation increases performance.</span></span> <span data-ttu-id="f2fa7-159">그러나 제외 된 페이지를 컴파일해야 하는 코드를 있으면 페이지를 찾아볼 때 오류가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-159">However, if a page that is excluded contains that code that must be compiled, an error will be thrown when the page is browsed.</span></span>

## <a name="enableeventvalidation"></a><span data-ttu-id="f2fa7-160">EnableEventValidation</span><span class="sxs-lookup"><span data-stu-id="f2fa7-160">EnableEventValidation</span></span>

<span data-ttu-id="f2fa7-161">이 특성 포스트백 및 콜백 이벤트를 검사할지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-161">This attribute specifies whether or not postback and callback events are validated.</span></span> <span data-ttu-id="f2fa7-162">이 설정 된 경우에 다시 게시 인수 또는 콜백 이벤트 원래 렌더링 하는 서버 컨트롤에서 원래 출처는 되도록 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-162">When this is enabled, arguments to postback or callback events are checked to ensure that they originated from the server control that originally rendered them.</span></span>

## <a name="enabletheming"></a><span data-ttu-id="f2fa7-163">EnableTheming</span><span class="sxs-lookup"><span data-stu-id="f2fa7-163">EnableTheming</span></span>

<span data-ttu-id="f2fa7-164">이 특성 페이지에 ASP.NET 테마가 사용 되는지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-164">This attribute specifies whether or not ASP.NET themes are used on a page.</span></span> <span data-ttu-id="f2fa7-165">기본값은 **false**입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-165">The default is **false**.</span></span> <span data-ttu-id="f2fa7-166">ASP.NET 테마에서 다루어진 [모듈 10](profiles-themes-and-web-parts.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-166">ASP.NET themes are covered in [Module 10](profiles-themes-and-web-parts.md).</span></span>

## <a name="linepragmas"></a><span data-ttu-id="f2fa7-167">LinePragmas</span><span class="sxs-lookup"><span data-stu-id="f2fa7-167">LinePragmas</span></span>

<span data-ttu-id="f2fa7-168">이 특성 컴파일하는 동안 줄 pragma를 추가할지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-168">This attribute specifies whether line pragmas should be added during compilation.</span></span> <span data-ttu-id="f2fa7-169">줄 pragma은 코드의 특정 섹션을 표시 하기 위해 디버거에서 사용 하는 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-169">Line pragmas are options used by debuggers to mark specific sections of code.</span></span>

## <a name="maintainscrollpositiononpostback"></a><span data-ttu-id="f2fa7-170">MaintainScrollPositionOnPostback</span><span class="sxs-lookup"><span data-stu-id="f2fa7-170">MaintainScrollPositionOnPostback</span></span>

<span data-ttu-id="f2fa7-171">이 특성에 JavaScript는 포스트백 간에 스크롤 위치를 유지 하기 위해 페이지에 삽입 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-171">This attribute specifies whether or not JavaScript is injected into the page in order to maintain scroll position between postbacks.</span></span> <span data-ttu-id="f2fa7-172">이 특성은 **false** 기본적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-172">This attribute is **false** by default.</span></span>

<span data-ttu-id="f2fa7-173">이 특성이 **true**, ASP.NET 추가 된 &lt;스크립트&gt; 포스트백 될 때 다음과 같은 블록:</span><span class="sxs-lookup"><span data-stu-id="f2fa7-173">When this attribute is **true**, ASP.NET will add a &lt;script&gt; block on postback that looks like this:</span></span>

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample3.html)]

<span data-ttu-id="f2fa7-174">이 스크립트 블록에 대 한 src WebResource.axd는 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-174">Note that the src for this script block is WebResource.axd.</span></span> <span data-ttu-id="f2fa7-175">이 리소스는 실제 경로가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-175">This resource is not a physical path.</span></span> <span data-ttu-id="f2fa7-176">이 스크립트를 요청 하면 ASP.NET은 동적으로 스크립트를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-176">When this script is requested, ASP.NET dynamically builds the script.</span></span>

### <a name="masterpagefile"></a><span data-ttu-id="f2fa7-177">MasterPageFile</span><span class="sxs-lookup"><span data-stu-id="f2fa7-177">MasterPageFile</span></span>

<span data-ttu-id="f2fa7-178">이 특성은 현재 페이지의 마스터 페이지 파일을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-178">This attribute specifies the master page file for the current page.</span></span> <span data-ttu-id="f2fa7-179">상대 또는 절대 경로일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-179">The path can be relative or absolute.</span></span> <span data-ttu-id="f2fa7-180">마스터 페이지에 나와 [모듈 4](master-pages.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-180">Master pages are covered in [Module 4](master-pages.md).</span></span>

## <a name="stylesheettheme"></a><span data-ttu-id="f2fa7-181">StyleSheetTheme</span><span class="sxs-lookup"><span data-stu-id="f2fa7-181">StyleSheetTheme</span></span>

<span data-ttu-id="f2fa7-182">이 특성을 사용 하면 ASP.NET 2.0 테마를 통해 정의 된 사용자 인터페이스 모양 속성을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-182">This attribute allows you to override user-interface appearance properties defined by an ASP.NET 2.0 theme.</span></span> <span data-ttu-id="f2fa7-183">테마에 나와 [모듈 10](profiles-themes-and-web-parts.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-183">Themes are covered in [Module 10](profiles-themes-and-web-parts.md).</span></span>

## <a name="theme"></a><span data-ttu-id="f2fa7-184">테마</span><span class="sxs-lookup"><span data-stu-id="f2fa7-184">Theme</span></span>

<span data-ttu-id="f2fa7-185">페이지 테마를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-185">Specifies the theme for the page.</span></span> <span data-ttu-id="f2fa7-186">StyleSheetTheme 특성에 대 한 값을 지정 하지 않으면, 테마 특성 페이지의 컨트롤에 적용 되는 모든 스타일을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-186">If a value is not specified for the StyleSheetTheme attribute, the Theme attribute overrides all styles applied to controls on the page.</span></span>

## <a name="title"></a><span data-ttu-id="f2fa7-187">제목</span><span class="sxs-lookup"><span data-stu-id="f2fa7-187">Title</span></span>

<span data-ttu-id="f2fa7-188">페이지의 제목을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-188">Sets the title for the page.</span></span> <span data-ttu-id="f2fa7-189">여기에 지정 된 값이 표시 됩니다는 &lt;title&gt; 렌더링된 된 페이지의 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-189">The value specified here will appear in the &lt;title&gt; element of the rendered page.</span></span>

### <a name="viewstateencryptionmode"></a><span data-ttu-id="f2fa7-190">ViewStateEncryptionMode</span><span class="sxs-lookup"><span data-stu-id="f2fa7-190">ViewStateEncryptionMode</span></span>

<span data-ttu-id="f2fa7-191">ViewStateEncryptionMode 열거형의 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-191">Sets the value for the ViewStateEncryptionMode enumeration.</span></span> <span data-ttu-id="f2fa7-192">사용 가능한 값은 **Always**를 **자동**, 및 **Never**합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-192">The available values are **Always**, **Auto**, and **Never**.</span></span> <span data-ttu-id="f2fa7-193">기본값은 **자동**합니다. 이 특성의 값으로 설정 된 경우 **자동**, viewstate는 암호화 컨트롤을 호출 하 여 요청 되는 **RegisterRequiresViewStateEncryption** 메서드.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-193">The default value is **Auto**. When this attribute is set to a value of **Auto**, viewstate is encrypted is a control requests it by calling the **RegisterRequiresViewStateEncryption** method.</span></span>

## <a name="setting-public-property-values-via-the--page-directive"></a><span data-ttu-id="f2fa7-194">공용 속성 값을 통해 @ Page 지시문을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-194">Setting Public Property Values via the @ Page Directive</span></span>

<span data-ttu-id="f2fa7-195">다른 새로운 ASP.NET 2.0의 @ Page 지시문의 기능은 기본 클래스의 공용 속성의 초기 값을 설정 하는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-195">Another new capability of the @ Page directive in ASP.NET 2.0 is the ability to set the initial value of public properties of a base class.</span></span> <span data-ttu-id="f2fa7-196">예를 들어 이라는 공용 속성이 있다고 가정해 보겠습니다 **SomeText** 기본 클래스 및 해당 기입할 있습니다를 초기화할 **Hello** 페이지가 로드 될 때입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-196">Suppose, for example, that you have a public property called **SomeText** in your base class and you d like it to be initialized to **Hello** when a page is loaded.</span></span> <span data-ttu-id="f2fa7-197">단순히 @ Page 지시문에 값을 설정 하 여이 수행할 수 있습니다 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-197">You can accomplish this by simply setting the value in the @ Page directive like so:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample4.aspx)]

<span data-ttu-id="f2fa7-198">합니다 **SomeText** 기본 클래스에서 SomeText 속성의 초기 값을 설정 하는 @ Page 지시문의 특성 *Hello!* 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-198">The **SomeText** attribute of the @ Page directive sets the initial value of the SomeText property in the base class to *Hello!*.</span></span> <span data-ttu-id="f2fa7-199">아래 비디오에서는 @ Page 지시문을 사용 하 여 기본 클래스의 공용 속성의 초기 값을 설정 하는 연습입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-199">The video below is a walkthrough of setting the initial value of a public property in a base class using the @ Page directive.</span></span>


![](the-asp-net-2-0-page-model/_static/image1.png)


[<span data-ttu-id="f2fa7-200">전체 화면 비디오 열기</span><span class="sxs-lookup"><span data-stu-id="f2fa7-200">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/setprop1.wmv)


## <a name="new-public-properties-of-the-page-class"></a><span data-ttu-id="f2fa7-201">페이지 클래스의 새 공용 속성</span><span class="sxs-lookup"><span data-stu-id="f2fa7-201">New Public Properties of the Page Class</span></span>

<span data-ttu-id="f2fa7-202">다음 공용 속성은 ASP.NET 2.0의 새로운 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-202">The following public properties are new in ASP.NET 2.0.</span></span>

## <a name="apprelativetemplatesourcedirectory"></a><span data-ttu-id="f2fa7-203">AppRelativeTemplateSourceDirectory</span><span class="sxs-lookup"><span data-stu-id="f2fa7-203">AppRelativeTemplateSourceDirectory</span></span>

<span data-ttu-id="f2fa7-204">페이지나 컨트롤에 응용 프로그램에 상대적인 경로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-204">Returns the application-relative path to the page or control.</span></span> <span data-ttu-id="f2fa7-205">에 있는 페이지에 대 한 예를 들어 http://app/folder/page.aspx, 속성은 반환 ~ / 폴더/입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-205">For example, for a page located at http://app/folder/page.aspx, the property returns ~/folder/.</span></span>

## <a name="apprelativevirtualpath"></a><span data-ttu-id="f2fa7-206">AppRelativeVirtualPath</span><span class="sxs-lookup"><span data-stu-id="f2fa7-206">AppRelativeVirtualPath</span></span>

<span data-ttu-id="f2fa7-207">페이지나 컨트롤에 상대 가상 디렉터리 경로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-207">Returns the relative virtual directory path to the page or control.</span></span> <span data-ttu-id="f2fa7-208">에 있는 페이지에 대 한 예를 들어 http://app/folder/page.aspx, 속성은 반환 ~ / folder/page.aspx 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-208">For example for a page located at http://app/folder/page.aspx, the property returns ~/folder/page.aspx.</span></span>

## <a name="asynctimeout"></a><span data-ttu-id="f2fa7-209">AsyncTimeout</span><span class="sxs-lookup"><span data-stu-id="f2fa7-209">AsyncTimeout</span></span>

<span data-ttu-id="f2fa7-210">비동기 페이지 처리에 사용 되는 제한 시간을 가져오거나 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-210">Gets or sets the timeout used for asynchronous page handling.</span></span> <span data-ttu-id="f2fa7-211">(비동기 페이지는이 모듈의 뒷부분에 나오는 다룰 수 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="f2fa7-211">(Asynchronous pages will be covered later in this module.)</span></span>

## <a name="clientquerystring"></a><span data-ttu-id="f2fa7-212">ClientQueryString</span><span class="sxs-lookup"><span data-stu-id="f2fa7-212">ClientQueryString</span></span>

<span data-ttu-id="f2fa7-213">요청된 된 URL의 쿼리 문자열 부분을 반환 하는 읽기 전용 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-213">A read-only property that returns the query string portion of the requested URL.</span></span> <span data-ttu-id="f2fa7-214">이 값은 URL로 인코딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-214">This value is URL encoded.</span></span> <span data-ttu-id="f2fa7-215">디코드해야 HttpServerUtility 클래스의 UrlDecode 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-215">You can use the UrlDecode method of the HttpServerUtility class to decode it.</span></span>

## <a name="clientscript"></a><span data-ttu-id="f2fa7-216">ClientScript</span><span class="sxs-lookup"><span data-stu-id="f2fa7-216">ClientScript</span></span>

<span data-ttu-id="f2fa7-217">이 속성에는 ASP.NETs 내보내기 클라이언트 쪽 스크립트의 관리를 사용할 수 있는 ClientScriptManager 개체를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-217">This property returns a ClientScriptManager object that can be used to manage ASP.NETs emission of client-side script.</span></span> <span data-ttu-id="f2fa7-218">(ClientScriptManager 클래스는이 모듈의 뒷부분에 설명 됨).</span><span class="sxs-lookup"><span data-stu-id="f2fa7-218">(The ClientScriptManager class is covered later in this module.)</span></span>

## <a name="enableeventvalidation"></a><span data-ttu-id="f2fa7-219">EnableEventValidation</span><span class="sxs-lookup"><span data-stu-id="f2fa7-219">EnableEventValidation</span></span>

<span data-ttu-id="f2fa7-220">이 속성 포스트백 및 콜백 이벤트에 대 한 이벤트 유효성 검사를 설정할지 여부를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-220">This property controls whether or not event validation is enabled for postback and callback events.</span></span> <span data-ttu-id="f2fa7-221">사용 하도록 설정 하는 경우에 다시 게시 인수 또는 콜백 이벤트 원래 렌더링 하는 서버 컨트롤에서 원래 출처는 되도록 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-221">When enabled, arguments to postback or callback events are verified to ensure that they originated from the server control that originally rendered them.</span></span>

## <a name="enabletheming"></a><span data-ttu-id="f2fa7-222">EnableTheming</span><span class="sxs-lookup"><span data-stu-id="f2fa7-222">EnableTheming</span></span>

<span data-ttu-id="f2fa7-223">이 속성은 페이지에 ASP.NET 2.0 테마를 적용 여부를 지정 하는 부울을 가져오거나 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-223">This property gets or sets a Boolean that specifies whether or not an ASP.NET 2.0 theme applies to the page.</span></span>

## <a name="form"></a><span data-ttu-id="f2fa7-224">Form</span><span class="sxs-lookup"><span data-stu-id="f2fa7-224">Form</span></span>

<span data-ttu-id="f2fa7-225">이 속성 HtmlForm 개체로 ASPX 페이지에서 HTML 폼을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-225">This property returns the HTML form on the ASPX page as an HtmlForm object.</span></span>

## <a name="header"></a><span data-ttu-id="f2fa7-226">헤더</span><span class="sxs-lookup"><span data-stu-id="f2fa7-226">Header</span></span>

<span data-ttu-id="f2fa7-227">이 속성 페이지 머리글을 포함 하는 HtmlHead 개체에 대 한 참조를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-227">This property returns a reference to an HtmlHead object that contains the page header.</span></span> <span data-ttu-id="f2fa7-228">Get/set 스타일 시트, 메타 태그를 반환된 된 HtmlHead 개체를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-228">You can use the returned HtmlHead object to get/set style sheets, Meta tags, etc.</span></span>

## <a name="idseparator"></a><span data-ttu-id="f2fa7-229">IdSeparator</span><span class="sxs-lookup"><span data-stu-id="f2fa7-229">IdSeparator</span></span>

<span data-ttu-id="f2fa7-230">이 읽기 전용 속성은 ASP.NET 페이지의 컨트롤에 대 한 고유 ID를 구성 하는 경우 컨트롤 식별자를 구분 하는 데 사용 되는 문자를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-230">This read-only property gets the character that is used to separate control identifiers when ASP.NET is building a unique ID for controls on a page.</span></span> <span data-ttu-id="f2fa7-231">코드에서 직접 사용하기에 적합하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-231">It is not intended to be used directly from your code.</span></span>

## <a name="isasync"></a><span data-ttu-id="f2fa7-232">IsAsync</span><span class="sxs-lookup"><span data-stu-id="f2fa7-232">IsAsync</span></span>

<span data-ttu-id="f2fa7-233">이 속성은 비동기 페이지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-233">This property allows for asynchronous pages.</span></span> <span data-ttu-id="f2fa7-234">비동기 페이지는이 모듈의 뒷부분에서 설명 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-234">Asynchronous pages are discussed later in this module.</span></span>

## <a name="iscallback"></a><span data-ttu-id="f2fa7-235">IsCallback</span><span class="sxs-lookup"><span data-stu-id="f2fa7-235">IsCallback</span></span>

<span data-ttu-id="f2fa7-236">이 읽기 전용 속성은 반환 **true** 페이지 콜백의 결과인 경우.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-236">This read-only property returns **true** if the page is the result of a call back.</span></span> <span data-ttu-id="f2fa7-237">콜백이이 모듈의 뒷부분에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-237">Call backs are discussed later in this module.</span></span>

## <a name="iscrosspagepostback"></a><span data-ttu-id="f2fa7-238">IsCrossPagePostBack</span><span class="sxs-lookup"><span data-stu-id="f2fa7-238">IsCrossPagePostBack</span></span>

<span data-ttu-id="f2fa7-239">이 읽기 전용 속성은 반환 **true** 페이지는 페이지 간 다시 게시의 일부인 경우.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-239">This read-only property returns **true** if the page is part of a cross-page postback.</span></span> <span data-ttu-id="f2fa7-240">페이지 간 포스트백이이 모듈의 뒷부분에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-240">Cross-page postbacks are covered later in this module.</span></span>

## <a name="items"></a><span data-ttu-id="f2fa7-241">항목</span><span class="sxs-lookup"><span data-stu-id="f2fa7-241">Items</span></span>

<span data-ttu-id="f2fa7-242">페이지 컨텍스트에 저장 된 모든 개체가 포함 된 IDictionary 인스턴스에 대 한 참조를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-242">Returns a reference to an IDictionary instance that contains all objects stored in the pages context.</span></span> <span data-ttu-id="f2fa7-243">이 IDictionary 개체에 항목을 추가할 수 있습니다를 더 컨텍스트의 수명 동안 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-243">You can add items to this IDictionary object and they will be available to you throughout the lifetime of the context.</span></span>

## <a name="maintainscrollpositiononpostback"></a><span data-ttu-id="f2fa7-244">MaintainScrollPositionOnPostBack</span><span class="sxs-lookup"><span data-stu-id="f2fa7-244">MaintainScrollPositionOnPostBack</span></span>

<span data-ttu-id="f2fa7-245">이 속성 ASP.NET 포스트백을 발생 한 후 페이지 스크롤 브라우저의 위치에에서 유지 관리 하는 JavaScript를 내보내는 여부를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-245">This property controls whether or not ASP.NET emits JavaScript that maintains the pages scroll position in the browser after a postback occurs.</span></span> <span data-ttu-id="f2fa7-246">(이 속성의 세부 정보는이 모듈의 앞부분에서 설명 했습니다.)</span><span class="sxs-lookup"><span data-stu-id="f2fa7-246">(Details of this property were discussed earlier in this module.)</span></span>

## <a name="master"></a><span data-ttu-id="f2fa7-247">마스터</span><span class="sxs-lookup"><span data-stu-id="f2fa7-247">Master</span></span>

<span data-ttu-id="f2fa7-248">이 읽기 전용 속성에는 마스터 페이지에 적용 된 페이지에 대 한 MasterPage 인스턴스에 대 한 참조를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-248">This read-only property returns a reference to the MasterPage instance for a page to which a master page has been applied.</span></span>

## <a name="masterpagefile"></a><span data-ttu-id="f2fa7-249">MasterPageFile</span><span class="sxs-lookup"><span data-stu-id="f2fa7-249">MasterPageFile</span></span>

<span data-ttu-id="f2fa7-250">페이지의 마스터 페이지 파일 이름을 가져오거나 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-250">Gets or sets the master page filename for the page.</span></span> <span data-ttu-id="f2fa7-251">만 PreInit 메서드에서이 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-251">This property can only be set in the PreInit method.</span></span>

## <a name="maxpagestatefieldlength"></a><span data-ttu-id="f2fa7-252">MaxPageStateFieldLength</span><span class="sxs-lookup"><span data-stu-id="f2fa7-252">MaxPageStateFieldLength</span></span>

<span data-ttu-id="f2fa7-253">이 속성 페이지 상태에 대 한 최대 길이 바이트 단위로 설정 하거나 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-253">This property gets or sets the maximum length for the pages state in bytes.</span></span> <span data-ttu-id="f2fa7-254">속성을 양수로 설정 된, 경우 페이지 뷰 상태는 나눌 수 여러 숨겨진된 필드에 지정 된 바이트 수를 초과 하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-254">If the property is set to a positive number, the pages view state will be broken up into multiple hidden fields so that it doesnt exceed the number of bytes specified.</span></span> <span data-ttu-id="f2fa7-255">속성이 음수 이면 보기 상태 청크로 분할 되지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-255">If the property is a negative number, the view state will not be broken into chunks.</span></span>

## <a name="pageadapter"></a><span data-ttu-id="f2fa7-256">PageAdapter</span><span class="sxs-lookup"><span data-stu-id="f2fa7-256">PageAdapter</span></span>

<span data-ttu-id="f2fa7-257">요청한 브라우저에 대 한 페이지를 수정 하는 PageAdapter 개체에 대 한 참조를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-257">Returns a reference to the PageAdapter object that modifies the page for the requesting browser.</span></span>

## <a name="previouspage"></a><span data-ttu-id="f2fa7-258">PreviousPage</span><span class="sxs-lookup"><span data-stu-id="f2fa7-258">PreviousPage</span></span>

<span data-ttu-id="f2fa7-259">에의 Server.Transfer 또는 페이지 간 포스트백의 이전 페이지에 대 한 참조를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-259">Returns a reference to the previous page in cases of a Server.Transfer or a cross-page postback.</span></span>

## <a name="skinid"></a><span data-ttu-id="f2fa7-260">SkinID</span><span class="sxs-lookup"><span data-stu-id="f2fa7-260">SkinID</span></span>

<span data-ttu-id="f2fa7-261">ASP.NET 2.0 페이지에 적용할 스킨을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-261">Specifies the ASP.NET 2.0 skin to apply to the page.</span></span>

## <a name="stylesheettheme"></a><span data-ttu-id="f2fa7-262">StyleSheetTheme</span><span class="sxs-lookup"><span data-stu-id="f2fa7-262">StyleSheetTheme</span></span>

<span data-ttu-id="f2fa7-263">이 속성 페이지에 적용 되는 스타일 시트를 가져오거나 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-263">This property gets or sets the style sheet that is applied to a page.</span></span>

## <a name="templatecontrol"></a><span data-ttu-id="f2fa7-264">TemplateControl</span><span class="sxs-lookup"><span data-stu-id="f2fa7-264">TemplateControl</span></span>

<span data-ttu-id="f2fa7-265">페이지에 대 한 포함 하는 컨트롤에 대 한 참조를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-265">Returns a reference to the containing control for the page.</span></span>

## <a name="theme"></a><span data-ttu-id="f2fa7-266">테마</span><span class="sxs-lookup"><span data-stu-id="f2fa7-266">Theme</span></span>

<span data-ttu-id="f2fa7-267">페이지에 적용 하는 ASP.NET 2.0 테마의 이름을 가져오거나 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-267">Gets or sets the name of the ASP.NET 2.0 theme applied to the page.</span></span> <span data-ttu-id="f2fa7-268">이 값은 PreInit 메서드 전에 설정 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-268">This value must be set prior to the PreInit method.</span></span>

## <a name="title"></a><span data-ttu-id="f2fa7-269">제목</span><span class="sxs-lookup"><span data-stu-id="f2fa7-269">Title</span></span>

<span data-ttu-id="f2fa7-270">이 속성에는 페이지 헤더에서 가져온 대로 페이지의 제목을 설정 하거나 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-270">This property gets or sets the title for the page as obtained from the pages header.</span></span>

## <a name="viewstateencryptionmode"></a><span data-ttu-id="f2fa7-271">ViewStateEncryptionMode</span><span class="sxs-lookup"><span data-stu-id="f2fa7-271">ViewStateEncryptionMode</span></span>

<span data-ttu-id="f2fa7-272">페이지의 ViewStateEncryptionMode을 가져오거나 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-272">Gets or sets the ViewStateEncryptionMode of the page.</span></span> <span data-ttu-id="f2fa7-273">이 모듈의 앞부분에서이 속성의 자세한 내용은 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-273">See a detailed discussion of this property earlier in this module.</span></span>

## <a name="new-protected-properties-of-the-page-class"></a><span data-ttu-id="f2fa7-274">페이지 클래스의 새 보호 된 속성</span><span class="sxs-lookup"><span data-stu-id="f2fa7-274">New Protected Properties of the Page Class</span></span>

<span data-ttu-id="f2fa7-275">다음은 ASP.NET 2.0에서 페이지 클래스의 새 보호 된 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-275">The following are the new protected properties of the Page class in ASP.NET 2.0.</span></span>

## <a name="adapter"></a><span data-ttu-id="f2fa7-276">어댑터</span><span class="sxs-lookup"><span data-stu-id="f2fa7-276">Adapter</span></span>

<span data-ttu-id="f2fa7-277">요청 하는 장치에서 페이지를 렌더링 하는 ControlAdapter에 대 한 참조를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-277">Returns a reference to the ControlAdapter that renders the page on the device that requested it.</span></span>

## <a name="asyncmode"></a><span data-ttu-id="f2fa7-278">AsyncMode</span><span class="sxs-lookup"><span data-stu-id="f2fa7-278">AsyncMode</span></span>

<span data-ttu-id="f2fa7-279">이 속성 페이지를 비동기적으로 처리 하 고 있는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-279">This property indicates whether or not the page is processed asynchronously.</span></span> <span data-ttu-id="f2fa7-280">코드에 직접적 런타임에서 사용할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-280">It is intended for use by the runtime and not directly in code.</span></span>

## <a name="clientidseparator"></a><span data-ttu-id="f2fa7-281">ClientIDSeparator</span><span class="sxs-lookup"><span data-stu-id="f2fa7-281">ClientIDSeparator</span></span>

<span data-ttu-id="f2fa7-282">이 속성 컨트롤에 대 한 고유한 클라이언트 Id를 만들 때 구분 기호로 사용 되는 문자를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-282">This property returns the character used as a separator when creating unique client IDs for controls.</span></span> <span data-ttu-id="f2fa7-283">코드에 직접적 런타임에서 사용할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-283">It is intended for use by the runtime and not directly in code.</span></span>

## <a name="pagestatepersister"></a><span data-ttu-id="f2fa7-284">PageStatePersister</span><span class="sxs-lookup"><span data-stu-id="f2fa7-284">PageStatePersister</span></span>

<span data-ttu-id="f2fa7-285">이 속성 페이지에 대 한 PageStatePersister 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-285">This property returns the PageStatePersister object for the page.</span></span> <span data-ttu-id="f2fa7-286">이 속성은 ASP.NET 컨트롤 개발자가 주로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-286">This property is primarily used by ASP.NET control developers.</span></span>

## <a name="uniquefilepathsuffix"></a><span data-ttu-id="f2fa7-287">UniqueFilePathSuffix</span><span class="sxs-lookup"><span data-stu-id="f2fa7-287">UniqueFilePathSuffix</span></span>

<span data-ttu-id="f2fa7-288">이 속성에는 브라우저 캐싱을 위해 파일 경로에 추가 되는 고유한 suffic 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-288">This property returns a unique suffic that is appended to the file path for caching browsers.</span></span> <span data-ttu-id="f2fa7-289">기본값은 \_ \_ufps = 6 자리 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-289">The default value is \_\_ufps= and a 6-digit number.</span></span>

## <a name="new-public-methods-for-the-page-class"></a><span data-ttu-id="f2fa7-290">Page 클래스에 대 한 새 공용 메서드</span><span class="sxs-lookup"><span data-stu-id="f2fa7-290">New Public Methods for the Page Class</span></span>

<span data-ttu-id="f2fa7-291">다음 공용 메서드는 ASP.NET 2.0에서 페이지 클래스에 새 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-291">The following public methods are new to the Page class in ASP.NET 2.0.</span></span>

## <a name="addonprerendercompleteasync"></a><span data-ttu-id="f2fa7-292">AddOnPreRenderCompleteAsync</span><span class="sxs-lookup"><span data-stu-id="f2fa7-292">AddOnPreRenderCompleteAsync</span></span>

<span data-ttu-id="f2fa7-293">이 메서드는 비동기 페이지 실행에 대 한 이벤트 처리기 대리자를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-293">This method registers event handler delegates for asynchronous page execution.</span></span> <span data-ttu-id="f2fa7-294">비동기 페이지는이 모듈의 뒷부분에서 설명 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-294">Asynchronous pages are discussed later in this module.</span></span>

## <a name="applystylesheetskin"></a><span data-ttu-id="f2fa7-295">ApplyStyleSheetSkin</span><span class="sxs-lookup"><span data-stu-id="f2fa7-295">ApplyStyleSheetSkin</span></span>

<span data-ttu-id="f2fa7-296">페이지 스타일 시트의 속성 페이지에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-296">Applies the properties in a pages style sheet to the page.</span></span>

## <a name="executeregisteredasynctasks"></a><span data-ttu-id="f2fa7-297">ExecuteRegisteredAsyncTasks</span><span class="sxs-lookup"><span data-stu-id="f2fa7-297">ExecuteRegisteredAsyncTasks</span></span>

<span data-ttu-id="f2fa7-298">이 메서드 시작 하는 비동기 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-298">This method beings an asynchronous task.</span></span>

### <a name="getvalidators"></a><span data-ttu-id="f2fa7-299">GetValidators</span><span class="sxs-lookup"><span data-stu-id="f2fa7-299">GetValidators</span></span>

<span data-ttu-id="f2fa7-300">지정 되지 않은 경우 지정 된 유효성 검사 그룹 또는 기본 유효성 검사 그룹에 대 한 유효성 검사기의 컬렉션을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-300">Returns a collection of validators for the specified validation group or the default validation group if none is specified.</span></span>

## <a name="registerasynctask"></a><span data-ttu-id="f2fa7-301">RegisterAsyncTask</span><span class="sxs-lookup"><span data-stu-id="f2fa7-301">RegisterAsyncTask</span></span>

<span data-ttu-id="f2fa7-302">이 메서드는 새 비동기 작업을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-302">This method registers a new async task.</span></span> <span data-ttu-id="f2fa7-303">비동기 페이지는이 모듈의 뒷부분에서 설명 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-303">Asynchronous pages are covered later in this module.</span></span>

## <a name="registerrequirescontrolstate"></a><span data-ttu-id="f2fa7-304">RegisterRequiresControlState</span><span class="sxs-lookup"><span data-stu-id="f2fa7-304">RegisterRequiresControlState</span></span>

<span data-ttu-id="f2fa7-305">이 메서드는 페이지 컨트롤 상태를 유지 해야는 ASP.NET을 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-305">This method tells ASP.NET that the pages control state must be persisted.</span></span>

## <a name="registerrequiresviewstateencryption"></a><span data-ttu-id="f2fa7-306">RegisterRequiresViewStateEncryption</span><span class="sxs-lookup"><span data-stu-id="f2fa7-306">RegisterRequiresViewStateEncryption</span></span>

<span data-ttu-id="f2fa7-307">이 메서드는 페이지 viewstate 암호화를 요구 하는 ASP.NET을 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-307">This method tells ASP.NET that the pages viewstate requires encryption.</span></span>

## <a name="resolveclienturl"></a><span data-ttu-id="f2fa7-308">ResolveClientUrl</span><span class="sxs-lookup"><span data-stu-id="f2fa7-308">ResolveClientUrl</span></span>

<span data-ttu-id="f2fa7-309">이미지에 대 한 클라이언트 요청에 대해 사용할 수 있는 상대 URL을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-309">Returns a relative URL that can be used for client requests for images, etc.</span></span>

## <a name="setfocus"></a><span data-ttu-id="f2fa7-310">SetFocus</span><span class="sxs-lookup"><span data-stu-id="f2fa7-310">SetFocus</span></span>

<span data-ttu-id="f2fa7-311">이 메서드는 페이지가 처음 로드 될 때 지정 된 컨트롤에 포커스를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-311">This method will set the focus to the control that is specified when the page is initially loaded.</span></span>

## <a name="unregisterrequirescontrolstate"></a><span data-ttu-id="f2fa7-312">UnregisterRequiresControlState</span><span class="sxs-lookup"><span data-stu-id="f2fa7-312">UnregisterRequiresControlState</span></span>

<span data-ttu-id="f2fa7-313">이 메서드는 컨트롤 상태 지 속성을 더 이상 필요한 것으로 전달 되는 컨트롤의 등록을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-313">This method will unregister the control that is passed to it as no longer requiring control state persistence.</span></span>

## <a name="changes-to-the-page-lifecycle"></a><span data-ttu-id="f2fa7-314">페이지 수명 주기 변경</span><span class="sxs-lookup"><span data-stu-id="f2fa7-314">Changes to the Page Lifecycle</span></span>

<span data-ttu-id="f2fa7-315">ASP.NET 2.0의 페이지 수명 주기를 크게 변경 되지 않은 고려해 야 하는 몇 가지 새로운 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-315">The page lifecycle in ASP.NET 2.0 hasnt changed dramatically, but there are some new methods that you should be aware of.</span></span> <span data-ttu-id="f2fa7-316">ASP.NET 2.0 페이지 수명 주기 아래에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-316">The ASP.NET 2.0 page lifecycle is outlined below.</span></span>

## <a name="preinit-new-in-aspnet-20"></a><span data-ttu-id="f2fa7-317">PreInit (의 ASP.NET 2.0)</span><span class="sxs-lookup"><span data-stu-id="f2fa7-317">PreInit (New in ASP.NET 2.0)</span></span>

<span data-ttu-id="f2fa7-318">PreInit 이벤트에는 개발자가 액세스할 수 있는 수명 주기에서 가장 빠른 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-318">The PreInit event is the earliest stage in the lifecycle that a developer can access.</span></span> <span data-ttu-id="f2fa7-319">이 이벤트의 추가를 프로그래밍 방식으로 변경 ASP.NET 2.0 테마, 마스터 페이지는 ASP.NET 2.0 프로필에 대 한 속성에 액세스할 수 있습니다. 다시 게시 상태를 해당 사실을 알아야 수명 주기에서이 시점에서 컨트롤에 Viewstate 아직 적용 되지 않습니다 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-319">The addition of this event makes it possible to programmatically change ASP.NET 2.0 themes, master pages, access properties for an ASP.NET 2.0 profile, etc. If you are in a postback state, its important to realize that Viewstate has not yet been applied to controls at this point in the lifecycle.</span></span> <span data-ttu-id="f2fa7-320">따라서 개발자는 컨트롤의 속성을이 단계에서 변경 되 면 페이지 주기의 뒷부분에서 덮어 가능성이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-320">Therefore, if a developer changes a property of a control at this stage, it will likely be overwritten later in the pages lifecycle.</span></span>

## <a name="init"></a><span data-ttu-id="f2fa7-321">Init</span><span class="sxs-lookup"><span data-stu-id="f2fa7-321">Init</span></span>

<span data-ttu-id="f2fa7-322">ASP.NET의 Init 이벤트 변경 되지 않은 1.x 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-322">The Init event has not changed from ASP.NET 1.x.</span></span> <span data-ttu-id="f2fa7-323">이 여기서 하려는 읽거나 페이지에서 컨트롤의 속성을 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-323">This is where you would want to read or initialize properties of controls on your page.</span></span> <span data-ttu-id="f2fa7-324">이 단계, 마스터 페이지, 테마 등 페이지에 이미 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-324">At this stage, master pages, themes, etc. are already applied to the page.</span></span>

## <a name="initcomplete-new-in-20"></a><span data-ttu-id="f2fa7-325">InitComplete (2.0의 새로운 기능)</span><span class="sxs-lookup"><span data-stu-id="f2fa7-325">InitComplete (New in 2.0)</span></span>

<span data-ttu-id="f2fa7-326">InitComplete 이벤트는 페이지 초기화 단계가 끝날 때 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-326">The InitComplete event is called at the end of the pages initialization stage.</span></span> <span data-ttu-id="f2fa7-327">이 시점에서 수명 주기에서 액세스할 수 페이지의 컨트롤 있지만 상태로 아직 채워지지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-327">At this point in the lifecycle, you can access controls on the page, but their state has not yet been populated.</span></span>

## <a name="preload-new-in-20"></a><span data-ttu-id="f2fa7-328">(2.0의 새로운 기능)를 미리 로드</span><span class="sxs-lookup"><span data-stu-id="f2fa7-328">PreLoad (New in 2.0)</span></span>

<span data-ttu-id="f2fa7-329">이 이벤트는 모든 포스트백 데이터가 적용 된 후 페이지 하기 직전에 호출 됩니다\_로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-329">This event is called after all postback data has been applied and just prior to Page\_Load.</span></span>

## <a name="load"></a><span data-ttu-id="f2fa7-330">Load</span><span class="sxs-lookup"><span data-stu-id="f2fa7-330">Load</span></span>

<span data-ttu-id="f2fa7-331">ASP.NET의 Load 이벤트 변경 되지 않은 1.x 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-331">The Load event has not changed from ASP.NET 1.x.</span></span>

## <a name="loadcomplete-new-in-20"></a><span data-ttu-id="f2fa7-332">LoadComplete (2.0의 새로운 기능)</span><span class="sxs-lookup"><span data-stu-id="f2fa7-332">LoadComplete (New in 2.0)</span></span>

<span data-ttu-id="f2fa7-333">LoadComplete 이벤트 페이지 로드 단계가에서 마지막 이벤트가입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-333">The LoadComplete event is the last event in the pages load stage.</span></span> <span data-ttu-id="f2fa7-334">이 단계에서는 모든 포스트백 및 viewstate 데이터 페이지에 적용 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-334">At this stage, all postback and viewstate data has been applied to the page.</span></span>

## <a name="prerender"></a><span data-ttu-id="f2fa7-335">PreRender</span><span class="sxs-lookup"><span data-stu-id="f2fa7-335">PreRender</span></span>

<span data-ttu-id="f2fa7-336">Viewstate를 페이지에 동적으로 추가 되는 컨트롤에 대 한 제대로 유지 하려는 경우 PreRender 이벤트를 추가할 수 있는 마지막 기회입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-336">If you would like for viewstate to be properly maintained for controls that are added to the page dynamically, the PreRender event is the last opportunity to add them.</span></span>

## <a name="prerendercomplete-new-in-20"></a><span data-ttu-id="f2fa7-337">PreRenderComplete (2.0의 새로운 기능)</span><span class="sxs-lookup"><span data-stu-id="f2fa7-337">PreRenderComplete (New in 2.0)</span></span>

<span data-ttu-id="f2fa7-338">PreRenderComplete 단계에서 모든 컨트롤을 페이지에 추가한 하 고 페이지를 렌더링할 준비가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-338">At the PreRenderComplete stage, all controls have been added to the page and the page is ready to be rendered.</span></span> <span data-ttu-id="f2fa7-339">PreRenderComplete 이벤트 페이지 viewstate 저장 되기 전에 발생 하는 마지막 이벤트가입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-339">The PreRenderComplete event is the last event raised before the pages viewstate is saved.</span></span>

## <a name="savestatecomplete-new-in-20"></a><span data-ttu-id="f2fa7-340">SaveStateComplete (2.0의 새로운 기능)</span><span class="sxs-lookup"><span data-stu-id="f2fa7-340">SaveStateComplete (New in 2.0)</span></span>

<span data-ttu-id="f2fa7-341">모든 페이지 viewstate 및 컨트롤 상태 저장 한 후에 즉시 SaveStateComplete 이벤트 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-341">The SaveStateComplete event is called immediately after all page viewstate and control state has been saved.</span></span> <span data-ttu-id="f2fa7-342">이 페이지를 실제로 브라우저에 렌더링 하기 전에 마지막 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-342">This is the last event before the page is actually rendered to the browser.</span></span>

## <a name="render"></a><span data-ttu-id="f2fa7-343">렌더링</span><span class="sxs-lookup"><span data-stu-id="f2fa7-343">Render</span></span>

<span data-ttu-id="f2fa7-344">Render 메서드는 ASP.NET 이후 변경 되지 않은 1.x 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-344">The Render method has not changed since ASP.NET 1.x.</span></span> <span data-ttu-id="f2fa7-345">여기서는 HtmlTextWriter 초기화 되 고 페이지가 브라우저에 렌더링 될 경우</span><span class="sxs-lookup"><span data-stu-id="f2fa7-345">This is where the HtmlTextWriter is initialized and the page is rendered to the browser.</span></span>

## <a name="cross-page-postback-in-aspnet-20"></a><span data-ttu-id="f2fa7-346">ASP.NET 2.0의에서 페이지 간 포스트백</span><span class="sxs-lookup"><span data-stu-id="f2fa7-346">Cross-Page Postback in ASP.NET 2.0</span></span>

<span data-ttu-id="f2fa7-347">Asp.net에서 1.x에서 포스트백 된 동일한 페이지에 게시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-347">In ASP.NET 1.x, postbacks were required to post to the same page.</span></span> <span data-ttu-id="f2fa7-348">페이지 간 포스트백 된 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-348">Cross-page postbacks were not allowed.</span></span> <span data-ttu-id="f2fa7-349">ASP.NET 2.0 IButtonControl 인터페이스를 통해 다른 페이지를 다시 게시 하는 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-349">ASP.NET 2.0 adds the ability to post back to a different page via the IButtonControl interface.</span></span> <span data-ttu-id="f2fa7-350">새 IButtonControl 인터페이스 (단추를 LinkButton 및 ImageButton 타사 사용자 지정 컨트롤 외에도)를 구현 하는 모든 컨트롤 PostBackUrl 특성의 사용을 통해이 새 기능을 활용을 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-350">Any control that implements the new IButtonControl interface (Button, LinkButton, and ImageButton in addition to third-party custom controls) can take advantage of this new functionality via the use of the PostBackUrl attribute.</span></span> <span data-ttu-id="f2fa7-351">다음 코드에서는 두 번째 페이지를 다시 게시 하는 단추 컨트롤을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-351">The following code shows a Button control that posts back to a second page.</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample5.aspx)]

<span data-ttu-id="f2fa7-352">페이지 다시 게시 되 면 포스트백을 시작 하는 페이지는 두 번째 페이지의 PreviousPage 속성을 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-352">When the page is posted back, the Page that initiates the postback is accessible via the PreviousPage property on the second page.</span></span> <span data-ttu-id="f2fa7-353">이 기능은 새 WebForm를 통해 구현 됩니다\_다른 페이지에 컨트롤을 포스트백 때 ASP.NET 2.0 페이지를 렌더링 하는 DoPostBackWithOptions 클라이언트 쪽 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-353">This functionality is implemented via the new WebForm\_DoPostBackWithOptions client-side function that ASP.NET 2.0 renders to the page when a control posts back to a different page.</span></span> <span data-ttu-id="f2fa7-354">이 JavaScript 함수는 클라이언트에 스크립트를 만드는 새 WebResource.axd 처리기에 의해 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-354">This JavaScript function is provided by the new WebResource.axd handler which emits script to the client.</span></span>

<span data-ttu-id="f2fa7-355">아래 비디오에서는 연습 페이지 간 포스트백을 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-355">The video below is a walkthrough of a cross-page postback.</span></span>


![](the-asp-net-2-0-page-model/_static/image2.png)


[<span data-ttu-id="f2fa7-356">전체 화면 비디오 열기</span><span class="sxs-lookup"><span data-stu-id="f2fa7-356">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/xpage1.wmv)


## <a name="more-details-on-cross-page-postbacks"></a><span data-ttu-id="f2fa7-357">페이지 간 포스트백에 대 한 자세한 내용</span><span class="sxs-lookup"><span data-stu-id="f2fa7-357">More Details on Cross-Page Postbacks</span></span>

### <a name="viewstate"></a><span data-ttu-id="f2fa7-358">Viewstate</span><span class="sxs-lookup"><span data-stu-id="f2fa7-358">Viewstate</span></span>

<span data-ttu-id="f2fa7-359">수 요청한 직접 이미 페이지 간 포스트백 시나리오의 첫 번째 페이지에서 viewstate 어떻게 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-359">You may have asked yourself already about what happens to the viewstate from the first page in a cross-page postback scenario.</span></span> <span data-ttu-id="f2fa7-360">결국은 다음과 같이 IPostBackDataHandler 구현 하지 않는 모든 컨트롤에 유지 됩니다 viewstate 통해 해당 상태 이므로 페이지 간 포스트백의 두 번째 페이지에서 해당 컨트롤의 속성에 액세스할 수, 페이지에 대 한 viewstate에 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-360">After all, any control that does not implement IPostBackDataHandler will persist its state via viewstate, so to have access to the properties of that control on the second page of a cross-page postback, you must have access to the viewstate for the page.</span></span> <span data-ttu-id="f2fa7-361">ASP.NET 2.0 이라는 두 번째 페이지에서 새 숨겨진된 필드를 사용 하 여이 시나리오의 담당 \_ \_PREVIOUSPAGE 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-361">ASP.NET 2.0 takes care of this scenario using a new hidden field in the second page called \_\_PREVIOUSPAGE.</span></span> <span data-ttu-id="f2fa7-362">합니다 \_ \_PREVIOUSPAGE 양식 필드는 두 번째 페이지에서 모든 컨트롤의 속성에 액세스할 수 있습니다 있도록 첫 번째 페이지에 대 한 viewstate 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-362">The \_\_PREVIOUSPAGE form field contains the viewstate for the first page so that you can have access to the properties of all controls in the second page.</span></span>

### <a name="circumventing-findcontrol"></a><span data-ttu-id="f2fa7-363">FindControl 우회</span><span class="sxs-lookup"><span data-stu-id="f2fa7-363">Circumventing FindControl</span></span>

<span data-ttu-id="f2fa7-364">페이지 간 포스트백의 비디오 연습에서는 첫 번째 페이지의 TextBox 컨트롤에 대 한 참조를 가져오려면 FindControl 메서드를 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-364">In the video walkthrough of a cross-page postback, I used the FindControl method to get a reference to the TextBox control on the first page.</span></span> <span data-ttu-id="f2fa7-365">해당 메서드를 적합 하지만 FindControl 비용이 많이 드는 이며 추가 코드를 작성 해야 하므로.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-365">That method works well for that purpose, but FindControl is expensive and it requires writing additional code.</span></span> <span data-ttu-id="f2fa7-366">다행 스럽게도 ASP.NET 2.0 많은 시나리오에서 작동 하는이 목적을 위해 FindControl에 대안을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-366">Fortunately, ASP.NET 2.0 provides an alternative to FindControl for this purpose that will work in many scenarios.</span></span> <span data-ttu-id="f2fa7-367">PreviousPageType 지시문 TypeName 또는 VirtualPath 특성을 사용 하 여 이전 페이지에는 강력한 형식의 참조를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-367">The PreviousPageType directive allows you to have a strongly-typed reference to the previous page by using either the TypeName or the VirtualPath attribute.</span></span> <span data-ttu-id="f2fa7-368">TypeName 특성을 사용 하면 VirtualPath 특성을 사용 하면 가상 경로 사용 하 여 이전 페이지를 참조 하는 동안 이전 페이지의 유형을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-368">The TypeName attribute allows you to specify the type of the previous page while the VirtualPath attribute allows you to refer to the previous page using a virtual path.</span></span> <span data-ttu-id="f2fa7-369">PreviousPageType 지시문을 설정한 후 컨트롤, 공용 속성을 사용 하 여 액세스할 수 있도록 하려는 등 다음 노출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-369">After you've set the PreviousPageType directive, you must then expose the controls, etc. to which you want to allow access using public properties.</span></span>

## <a name="lab-1-cross-page-postback"></a><span data-ttu-id="f2fa7-370">랩 1 페이지 간 포스트백</span><span class="sxs-lookup"><span data-stu-id="f2fa7-370">Lab 1 Cross-Page Postback</span></span>

<span data-ttu-id="f2fa7-371">이 실습에서는 ASP.NET 2.0의 새 페이지 간 다시 게시 기능을 사용 하는 응용 프로그램에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-371">In this lab, you will create an application that uses the new cross-page postback functionality of ASP.NET 2.0.</span></span>

1. <span data-ttu-id="f2fa7-372">Visual Studio 2005를 열고 새 ASP.NET 웹 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-372">Open Visual Studio 2005 and create a new ASP.NET Web site.</span></span>
2. <span data-ttu-id="f2fa7-373">Page2.aspx를 호출 하는 새 Webform를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-373">Add a new Webform called page2.aspx.</span></span>
3. <span data-ttu-id="f2fa7-374">디자인 보기에서 Default.aspx를 열고 단추 컨트롤과 TextBox 컨트롤을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-374">Open the Default.aspx in Design view and add a Button control and a TextBox control.</span></span> 

    1. <span data-ttu-id="f2fa7-375">단추 컨트롤의 ID를 제공 **SubmitButton** 텍스트 상자 컨트롤의 ID 및 **UserName**합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-375">Give the Button control an ID of **SubmitButton** and the TextBox control an ID of **UserName**.</span></span>
    2. <span data-ttu-id="f2fa7-376">Page2.aspx로 단추의 PostBackUrl 속성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-376">Set the PostBackUrl property of the Button to page2.aspx.</span></span>
4. <span data-ttu-id="f2fa7-377">소스 뷰에서 page2.aspx를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-377">Open page2.aspx in Source view.</span></span>
5. <span data-ttu-id="f2fa7-378">아래 표시 된 것과 같이 @ PreviousPageType 지시문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-378">Add a @ PreviousPageType directive as shown below:</span></span>
6. <span data-ttu-id="f2fa7-379">페이지에 다음 코드를 추가\_page2.aspx의 코드 숨김의 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-379">Add the following code to the Page\_Load of page2.aspx's code-behind:</span></span> 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample6.cs)]
7. <span data-ttu-id="f2fa7-380">빌드 메뉴에서 빌드를 클릭 하 여 프로젝트를 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-380">Build the project by clicking on Build on the Build menu.</span></span>
8. <span data-ttu-id="f2fa7-381">Default.aspx에 대 한 코드 숨김에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-381">Add the following code to the code-behind for Default.aspx:</span></span> 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample7.cs)]
9. <span data-ttu-id="f2fa7-382">페이지 변경\_다음과 page2.aspx에서 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-382">Change the Page\_Load in page2.aspx to the following:</span></span> 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample8.cs)]
10. <span data-ttu-id="f2fa7-383">프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-383">Build the project.</span></span>
11. <span data-ttu-id="f2fa7-384">프로젝트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-384">Run the project.</span></span>
12. <span data-ttu-id="f2fa7-385">텍스트 상자에 이름을 입력 하 고 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-385">Enter your name in the TextBox and click the button.</span></span>
13. <span data-ttu-id="f2fa7-386">결과 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="f2fa7-386">What is the result?</span></span>

## <a name="asynchronous-pages-in-aspnet-20"></a><span data-ttu-id="f2fa7-387">ASP.NET 2.0의에서 비동기 페이지</span><span class="sxs-lookup"><span data-stu-id="f2fa7-387">Asynchronous Pages in ASP.NET 2.0</span></span>

<span data-ttu-id="f2fa7-388">ASP.NET에서 많은 경합 문제는 외부 호출 (예: 웹 서비스 또는 데이터베이스 호출), 파일 IO 대기 시간 등의 대기 시간이 발생 합니다. ASP.NET 응용 프로그램에 대해 요청 하는 ASP.NET 해당 요청을 서비스에 작업자 스레드 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-388">Many contention problems in ASP.NET are caused by latency of external calls (such as Web service or database calls), file IO latency, etc. When a request is made against an ASP.NET application, ASP.NET uses one of its worker threads to service that request.</span></span> <span data-ttu-id="f2fa7-389">요청이 완료 되 고 응답이 전송 된 때까지 해당 스레드를 소유 하는 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-389">That request owns that thread until the request is complete and the response has been sent.</span></span> <span data-ttu-id="f2fa7-390">ASP.NET 2.0 페이지를 비동기적으로 실행 하는 기능을 추가 하 여 이러한 유형의 문제를 사용 하 여 대기 시간 문제를 해결 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-390">ASP.NET 2.0 seeks to resolve latency issues with these types of issues by adding the capability to execute pages asynchronously.</span></span> <span data-ttu-id="f2fa7-391">즉, 작업자 스레드 수 요청을 시작 하 고 다음 신속 하 게 사용할 수 있는 스레드 풀으로 반환 되므로 다른 스레드로 추가 실행을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-391">That means that a worker thread can start the request and then hand off additional execution to another thread, thereby returning to the available thread pool quickly.</span></span> <span data-ttu-id="f2fa7-392">파일 IO, 데이터베이스 호출 등이 완료 되 면 새 스레드는 요청을 완료 하기 스레드 풀에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-392">When the file IO, database call, etc. has completed, a new thread is obtained from the thread pool to finish the request.</span></span>

<span data-ttu-id="f2fa7-393">첫 번째 단계는 비동기적으로 실행 하는 페이지를 설정 하는 것은 **비동기** 같이 page 지시문의 특성:</span><span class="sxs-lookup"><span data-stu-id="f2fa7-393">The first step in making a page execute asynchronously is to set the **Async** attribute of the page directive like so:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample9.aspx)]

<span data-ttu-id="f2fa7-394">이 특성은 페이지에 IHttpAsyncHandler를 구현 하는 ASP.NET에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-394">This attribute tells ASP.NET to implement the IHttpAsyncHandler for the page.</span></span>

<span data-ttu-id="f2fa7-395">다음 단계는 PreRender 전에 페이지의 수명 주기 내 현재 시점 AddOnPreRenderCompleteAsync 메서드를 호출 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-395">The next step is to call the AddOnPreRenderCompleteAsync method at a point in the lifecycle of the page prior to PreRender.</span></span> <span data-ttu-id="f2fa7-396">(이 일반적으로 메서드는 페이지에서\_로드 합니다.) AddOnPreRenderCompleteAsync 메서드는 두 매개 변수입니다. BeginEventHandler 및를 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-396">(This method is typically called in Page\_Load.) The AddOnPreRenderCompleteAsync method takes two parameters; a BeginEventHandler and an EndEventHandler.</span></span> <span data-ttu-id="f2fa7-397">BeginEventHandler를 하 여를 매개 변수로 전달 되는 IAsyncResult를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-397">The BeginEventHandler returns an IAsyncResult which is then passed as a parameter to the EndEventHandler.</span></span>

<span data-ttu-id="f2fa7-398">아래 동영상은 비동기 페이지 요청을 연습입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-398">The video below is a walkthrough of an asynchronous page request.</span></span>


![](the-asp-net-2-0-page-model/_static/image3.png)


[<span data-ttu-id="f2fa7-399">전체 화면 비디오 열기</span><span class="sxs-lookup"><span data-stu-id="f2fa7-399">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/async1.wmv)


> [!NOTE]
> <span data-ttu-id="f2fa7-400">하 여 완료 될 때까지 비동기 페이지를 브라우저에 렌더링 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-400">An async page does not render to the browser until the EndEventHandler has completed.</span></span> <span data-ttu-id="f2fa7-401">점에 의심의 여지가 있지만 일부 개발자는 비동기 요청을 비동기 콜백을 비슷한 것으로 간주 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-401">No doubt but that some developers will think of async requests as being similar to async callbacks.</span></span> <span data-ttu-id="f2fa7-402">자신이 실현 하는 것이 반드시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-402">It's important to realize that they are not.</span></span> <span data-ttu-id="f2fa7-403">비동기 요청에 장점은 첫 번째 작업자 스레드가 줄어듭니다 바인딩된 IO 되어 경합 등 새 서비스 요청을 스레드 풀만 반환 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-403">The benefit to asynchronous requests is that the first worker thread can be returned to the thread pool to service new requests, thereby reducing contention due to being IO bound, etc.</span></span>


## <a name="script-callbacks-in-aspnet-20"></a><span data-ttu-id="f2fa7-404">Script Callbacks in ASP.NET 2.0</span><span class="sxs-lookup"><span data-stu-id="f2fa7-404">Script Callbacks in ASP.NET 2.0</span></span>

<span data-ttu-id="f2fa7-405">콜백과 연관 깜박임을 방지 하는 방법에 대 한 웹 개발자가 항상 살펴본 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-405">Web developers have always looked for ways to prevent the flickering associated with a callback.</span></span> <span data-ttu-id="f2fa7-406">ASP.NET 1.x에서 SmartNavigation, 깜박임을 방지에 대 한 가장 일반적인 방법은 했지만 SmartNavigation 클라이언트에서 해당 구현의 복잡성으로 인해 일부 개발자에 대 한 문제를 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-406">In ASP.NET 1.x, SmartNavigation was the most common method for avoiding flickering, but SmartNavigation caused problems for some developers because of the complexity of its implementation on the client.</span></span> <span data-ttu-id="f2fa7-407">ASP.NET 2.0 스크립트 콜백을 사용 하 여이 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-407">ASP.NET 2.0 addresses this issue with script callbacks.</span></span> <span data-ttu-id="f2fa7-408">JavaScript 통해 웹 서버에 대 한 요청에 XMLHttp를 활용 하는 스크립트 콜백 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-408">Script callbacks utilize XMLHttp to make requests against the Web server via JavaScript.</span></span> <span data-ttu-id="f2fa7-409">XMLHttp 요청 브라우저의 DOM. 통해 다음 조작할 수 있는 XML 데이터를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-409">The XMLHttp request returns XML data that can then be manipulated via the browser's DOM.</span></span> <span data-ttu-id="f2fa7-410">XMLHttp 코드 새 WebResource.axd 처리기에서 사용자 로부터 숨겨집니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-410">XMLHttp code is hidden from the user by the new WebResource.axd handler.</span></span>

<span data-ttu-id="f2fa7-411">ASP.NET 2.0의 스크립트 콜백을 구성 하기 위해 필요한 여러 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-411">There are several steps that are necessary in order to configure a script callback in ASP.NET 2.0.</span></span>

## <a name="step-1--implement-the-icallbackeventhandler-interface"></a><span data-ttu-id="f2fa7-412">1 단계: ICallbackEventHandler 인터페이스를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-412">Step 1 : Implement the ICallbackEventHandler Interface</span></span>

<span data-ttu-id="f2fa7-413">ASP.NET 스크립트 콜백에 참여 하 여 페이지 인식에 대 한 순서로 ICallbackEventHandler 인터페이스를 구현 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-413">In order for ASP.NET to recognize your page as participating in a script callback, you must implement the ICallbackEventHandler interface.</span></span> <span data-ttu-id="f2fa7-414">이렇게 하려면 코드 숨김 파일에서 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-414">You can do this in your code-behind file like so:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample10.cs)]

<span data-ttu-id="f2fa7-415">또한 이렇게 하므로 @ Implements 지시문 like를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="f2fa7-415">You can also do this using the @ Implements directive like so:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample11.aspx)]

<span data-ttu-id="f2fa7-416">인라인 ASP.NET 코드를 사용 하는 경우에 일반적으로 @ Implements 지시문을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-416">You would typically use the @ Implements directive when using inline ASP.NET code.</span></span>

## <a name="step-2--call-getcallbackeventreference"></a><span data-ttu-id="f2fa7-417">2 단계: GetCallbackEventReference 호출</span><span class="sxs-lookup"><span data-stu-id="f2fa7-417">Step 2 : Call GetCallbackEventReference</span></span>

<span data-ttu-id="f2fa7-418">이전에 설명한 대로 XMLHttp 호출 WebResource.axd 처리기에 캡슐화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-418">As mentioned previously, the XMLHttp call is encapsulated in the WebResource.axd handler.</span></span> <span data-ttu-id="f2fa7-419">ASP.NET WebForm에 대 한 호출 추가 페이지를 렌더링할 때\_DoCallback, WebResource.axd에서 제공 하는 클라이언트 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-419">When your page is rendered, ASP.NET will add a call to WebForm\_DoCallback, a client script that is provided by WebResource.axd.</span></span> <span data-ttu-id="f2fa7-420">WebForm\_DoCallback 함수를 대체 합니다 \_ \_콜백의 doPostBack 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-420">The WebForm\_DoCallback function replaces the \_\_doPostBack function for a callback.</span></span> <span data-ttu-id="f2fa7-421">유의 해야 \_ \_doPostBack은 프로그래밍 방식으로 페이지의 폼을 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-421">Remember that \_\_doPostBack programmatically submits the form on the page.</span></span> <span data-ttu-id="f2fa7-422">따라서 포스트백을 방지 하려면 콜백 시나리오에서는 \_ \_doPostBack 적절 하지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-422">In a callback scenario, you want to prevent a postback, so \_\_doPostBack will not suffice.</span></span>

> [!NOTE]
> <span data-ttu-id="f2fa7-423">\_\_doPostBack은 클라이언트 스크립트 콜백 시나리오의 페이지로 계속 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-423">\_\_doPostBack is still rendered to the page in a client script callback scenario.</span></span> <span data-ttu-id="f2fa7-424">그러나 콜백에 대 한 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-424">However, it's not used for the callback.</span></span>


<span data-ttu-id="f2fa7-425">인수를 WebForm\_DoCallback 클라이언트 쪽 함수는 일반적으로 페이지에서 호출할 수 있는 GetCallbackEventReference 서버 측 함수를 통해 제공 됩니다\_로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-425">The arguments for the WebForm\_DoCallback client-side function are provided via the server-side function GetCallbackEventReference which would normally be called in Page\_Load.</span></span> <span data-ttu-id="f2fa7-426">GetCallbackEventReference 하는 일반적인 호출은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-426">A typical call to GetCallbackEventReference might look like this:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample12.cs)]

> [!NOTE]
> <span data-ttu-id="f2fa7-427">이 경우 cm는 ClientScriptManager의 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-427">In this case, cm is an instance of ClientScriptManager.</span></span> <span data-ttu-id="f2fa7-428">이 모듈의 뒷부분에 나오는 ClientScriptManager 클래스를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-428">The ClientScriptManager class will be covered later in this module.</span></span>


<span data-ttu-id="f2fa7-429">GetCallbackEventReference의 몇 가지 오버 로드 된 버전이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-429">There are several overloaded versions of GetCallbackEventReference.</span></span> <span data-ttu-id="f2fa7-430">이 경우 인수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-430">In this case, the arguments are as follows:</span></span>

`this`

<span data-ttu-id="f2fa7-431">GetCallbackEventReference 호출 되 고 있는 컨트롤에 대 한 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-431">A reference to the control where GetCallbackEventReference is being called.</span></span> <span data-ttu-id="f2fa7-432">이 경우 페이지 자체는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-432">In this case, it's the page itself.</span></span>

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample13.js)]

<span data-ttu-id="f2fa7-433">클라이언트 쪽 코드에서 서버 쪽 이벤트에 전달 되는 문자열 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-433">A string argument that will be passed from the client-side code to the server-side event.</span></span> <span data-ttu-id="f2fa7-434">이 경우 드롭다운의 값을 전달 하는 Im ddlCompany를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-434">In this case, Im passing the value of a dropdown called ddlCompany.</span></span>

`ShowCompanyName`

<span data-ttu-id="f2fa7-435">서버 쪽 콜백 이벤트에서 반환 값 (문자열)으로 허용 하는 클라이언트 쪽 함수의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-435">The name of the client-side function that will accept the return value (as string) from the server-side callback event.</span></span> <span data-ttu-id="f2fa7-436">이 함수는 서버 쪽 콜백에 성공할 경우에 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-436">This function will only be called when the server-side callback is successful.</span></span> <span data-ttu-id="f2fa7-437">따라서 견고성을 위해 것이 좋습니다 GetCallbackEventReference 오류 발생 시 실행 하는 클라이언트 쪽 함수 이름을 지정 하는 추가 문자열 인수를 받아들이는 오버 로드 된 버전을 사용 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-437">Therefore, for the sake of robustness, it is generally recommended to use the overloaded version of GetCallbackEventReference that takes an additional string argument specifying the name of a client-side function to execute in the event of an error.</span></span>

`null`

<span data-ttu-id="f2fa7-438">서버로 콜백 전에 시작 된 클라이언트 측 함수를 나타내는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-438">A string representing a client-side function that it initiated before the callback to the server.</span></span> <span data-ttu-id="f2fa7-439">이 예제의 경우 인수가 null 이므로 해당 스크립트가 없습니다. 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-439">In this case, there is no such script, so the argument is null.</span></span>

`true`

<span data-ttu-id="f2fa7-440">콜백을 비동기적으로 수행 하는지 여부를 지정 하는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-440">A Boolean specifying whether or not to conduct the callback asynchronously.</span></span>

<span data-ttu-id="f2fa7-441">WebForm 호출\_DoCallback 클라이언트에서 이러한 인수를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-441">The call to WebForm\_DoCallback on the client will pass these arguments.</span></span> <span data-ttu-id="f2fa7-442">따라서 클라이언트에서이 페이지를 렌더링할 때 해당 코드 보입니다 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-442">Therefore, when this page is rendered on the client, that code will look like so:</span></span>

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample14.js)]

<span data-ttu-id="f2fa7-443">클라이언트에서 함수의 서명은 약간 다른 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-443">Notice that the signature of the function on the client is a bit different.</span></span> <span data-ttu-id="f2fa7-444">클라이언트 쪽 함수에는 5 개 문자열 및 부울 값을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-444">The client-side function passes 5 strings and a Boolean.</span></span> <span data-ttu-id="f2fa7-445">추가 문자열 (null 인 위 예제의) 서버 쪽 콜백이 발생 하는 오류를 처리 하는 클라이언트 측 함수를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-445">The additional string (which is null in the above example) contains the client-side function that will handle any errors from the server-side callback.</span></span>

## <a name="step-3--hook-the-client-side-control-event"></a><span data-ttu-id="f2fa7-446">3 단계: 클라이언트 쪽 컨트롤 이벤트에 연결</span><span class="sxs-lookup"><span data-stu-id="f2fa7-446">Step 3 : Hook the Client-Side Control Event</span></span>

<span data-ttu-id="f2fa7-447">문자열 변수에 할당 된 위의 GetCallbackEventReference의 반환 값을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-447">Notice that the return value of GetCallbackEventReference above was assigned to a string variable.</span></span> <span data-ttu-id="f2fa7-448">콜백을 시작 하는 컨트롤에 대 한 클라이언트 쪽 이벤트를 연결 문자열이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-448">That string is used to hook a client-side event for the control that initiates the callback.</span></span> <span data-ttu-id="f2fa7-449">이 예제에서는 콜백 시작 페이지에서 드롭다운에 연결 하려고 하므로 합니다 *OnChange* 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-449">In this example, the callback is initiated by a dropdown on the page, so I want to hook the *OnChange* event.</span></span>

<span data-ttu-id="f2fa7-450">다음과 같이 클라이언트 쪽 태그에 처리기를 간단히 추가 클라이언트 쪽 이벤트를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-450">To hook the client-side event, simply add a handler to the client-side markup as follows:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample15.cs)]

<span data-ttu-id="f2fa7-451">이전에 설명한 대로 *cbRef* GetCallbackEventReference 호출의 반환 값입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-451">Recall that *cbRef* is the return value from the call to GetCallbackEventReference.</span></span> <span data-ttu-id="f2fa7-452">WebForm 호출 포함\_위에 나온 DoCallback 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-452">It contains the call to WebForm\_DoCallback that was shown above.</span></span>

## <a name="step-4--register-the-client-side-script"></a><span data-ttu-id="f2fa7-453">4 단계: 클라이언트 쪽 스크립트 등록</span><span class="sxs-lookup"><span data-stu-id="f2fa7-453">Step 4 : Register the Client-Side Script</span></span>

<span data-ttu-id="f2fa7-454">GetCallbackEventReference 호출 클라이언트 쪽 스크립트 호출 되도록 지정 하는 재현 율 **ShowCompanyName** 서버측 콜백 성공 시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-454">Recall that the call to GetCallbackEventReference specified that a client-side script called **ShowCompanyName** would be executed when the server-side callback succeeds.</span></span> <span data-ttu-id="f2fa7-455">스크립트가는 ClientScriptManager 인스턴스를 사용 하 여 페이지에 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-455">That script needs to be added to the page using a ClientScriptManager instance.</span></span> <span data-ttu-id="f2fa7-456">(ClientScriptManager 클래스가이 모듈의 뒷부분에 나오는 표에서 됩니다.) 따라서 해당 같은 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-456">(The ClientScriptManager class will be dicussed later in this module.) You do that like so:</span></span>

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample16.js)]

## <a name="step-5--call-the-methods-of-the-icallbackeventhandler-interface"></a><span data-ttu-id="f2fa7-457">5 단계: ICallbackEventHandler 인터페이스의 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-457">Step 5 : Call the Methods of the ICallbackEventHandler Interface</span></span>

<span data-ttu-id="f2fa7-458">결국 ICallbackEventHandler 코드에서 구현 해야 하는 두 메서드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-458">The ICallbackEventHandler contains two methods that you need to implement in your code.</span></span> <span data-ttu-id="f2fa7-459">이들은 **RaiseCallbackEvent** 하 고 **GetCallbackEvent**합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-459">They are **RaiseCallbackEvent** and **GetCallbackEvent**.</span></span>

<span data-ttu-id="f2fa7-460">**RaiseCallbackEvent** 인수로 문자열을 nothing을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-460">**RaiseCallbackEvent** takes a string as an argument and returns nothing.</span></span> <span data-ttu-id="f2fa7-461">WebForm 클라이언트측 호출에서 전달 되는 문자열 인수는\_DoCallback 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-461">The string argument is passed from the client-side call to WebForm\_DoCallback.</span></span> <span data-ttu-id="f2fa7-462">이 경우 해당 값은는 *값* ddlCompany 라는 드롭다운의 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-462">In this case, that value is the *value* attribute of the dropdown called ddlCompany.</span></span> <span data-ttu-id="f2fa7-463">서버 쪽 코드 RaiseCallbackEvent 메서드에 배치 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-463">Your server-side code should be placed in the RaiseCallbackEvent method.</span></span> <span data-ttu-id="f2fa7-464">예를 들어 콜백이 외부 리소스에 대해 WebRequest 중이면 해당 코드 RaiseCallbackEvent에 배치 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-464">For example, if your callback is making a WebRequest against an external resource, that code should be placed in RaiseCallbackEvent.</span></span>

<span data-ttu-id="f2fa7-465">**GetCallbackEvent** 는 클라이언트 콜백의 반환을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-465">**GetCallbackEvent** is responsible for processing the return of the callback to the client.</span></span> <span data-ttu-id="f2fa7-466">인수가 없는 하 고 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-466">It takes no arguments and returns a string.</span></span> <span data-ttu-id="f2fa7-467">반환 되는 문자열 전달할 인수로 서 클라이언트 쪽 함수를이 예제의 *ShowCompanyName*합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-467">The string that it returns will be passed as an argument to the client-side function, in this case *ShowCompanyName*.</span></span>

<span data-ttu-id="f2fa7-468">위의 단계를 마친 후 ASP.NET 2.0에 스크립트 콜백은 수행 준비가 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-468">Once you have completed the above steps, you are ready to perform a script callback in ASP.NET 2.0.</span></span>


![](the-asp-net-2-0-page-model/_static/image4.png)


[<span data-ttu-id="f2fa7-469">전체 화면 비디오 열기</span><span class="sxs-lookup"><span data-stu-id="f2fa7-469">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/callback1.wmv)


<span data-ttu-id="f2fa7-470">ASP.NET 스크립트 콜백은 함으로써 XMLHttp 호출을 지 원하는 모든 브라우저에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-470">Script callbacks in ASP.NET are supported in any browser that supports making XMLHttp calls.</span></span> <span data-ttu-id="f2fa7-471">에 포함 하는 모든 최신 브라우저를 사용 하 여 지금 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-471">That includes all of the modern browsers in use today.</span></span> <span data-ttu-id="f2fa7-472">Internet Explorer는 내장 XMLHttp 개체를 사용 하는 다른 최신 브라우저 (예정 된 IE 7 포함)는 XMLHttp ActiveX 개체를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-472">Internet Explorer uses the XMLHttp ActiveX object while other modern browsers (including the upcoming IE 7) use an intrinsic XMLHttp object.</span></span> <span data-ttu-id="f2fa7-473">프로그래밍 방식으로 사용할 수 있는 브라우저에서 콜백을 지 원하는 경우를 결정 하는 **Request.Browser.SupportCallback** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-473">To programmatically determine if a browser supports callbacks, you can use the **Request.Browser.SupportCallback** property.</span></span> <span data-ttu-id="f2fa7-474">이 속성은 반환 **true** 요청 하는 클라이언트에 스크립트 콜백은 지 원하는 경우.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-474">This property will return **true** if the requesting client supports script callbacks.</span></span>

## <a name="working-with-client-script-in-aspnet-20"></a><span data-ttu-id="f2fa7-475">ASP.NET 2.0에서에서 클라이언트 스크립트를 사용 하 여 작업</span><span class="sxs-lookup"><span data-stu-id="f2fa7-475">Working with Client Script in ASP.NET 2.0</span></span>

<span data-ttu-id="f2fa7-476">ASP.NET 2.0의 클라이언트 스크립트는 ClientScriptManager 클래스 사용을 통해 관리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-476">Client scripts in ASP.NET 2.0 are managed via the use of the ClientScriptManager class.</span></span> <span data-ttu-id="f2fa7-477">ClientScriptManager 클래스는 형식 및 이름을 사용 하 여 클라이언트 스크립트의 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-477">The ClientScriptManager class keeps track of client scripts using a type and a name.</span></span> <span data-ttu-id="f2fa7-478">이렇게 하면 동일한 스크립트를 두 번 이상 삽입 페이지에 프로그래밍 방식으로 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-478">This prevents the same script from being programmatically inserted on a page more than once.</span></span>

> [!NOTE]
> <span data-ttu-id="f2fa7-479">스크립트를 페이지에 성공적으로 등록 된 후 이후 모든 시도 동일한 스크립트를 등록 하려면를 두 번째로 등록 되지 않은 스크립트를 간단히 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-479">After a script has been successfully registered on a page, any subsequent attempt to register the same script will simply result in the script not being registered a second time.</span></span> <span data-ttu-id="f2fa7-480">중복 된 스크립트가 추가 됩니다 하 고 예외가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-480">No duplicate scripts are added and no exception occurs.</span></span> <span data-ttu-id="f2fa7-481">불필요 한 계산을 방지 하려면 두 번 이상 등록 하지 않도록 스크립트는 이미 등록 되어 있는지 확인 하는 데 사용할 수 있는 메서드를 가지입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-481">To avoid unnecessary computation, there are methods that you can use to determine if a script is already registered so that you do not attempt to register it more than once.</span></span>


<span data-ttu-id="f2fa7-482">ClientScriptManager 메서드의 모든 현재 ASP.NET 개발자에 게 익숙할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-482">The methods of the ClientScriptManager should be familiar to all current ASP.NET developers:</span></span>

## <a name="registerclientscriptblock"></a><span data-ttu-id="f2fa7-483">RegisterClientScriptBlock</span><span class="sxs-lookup"><span data-stu-id="f2fa7-483">RegisterClientScriptBlock</span></span>

<span data-ttu-id="f2fa7-484">이 메서드는 렌더링된 된 페이지의 위쪽에 스크립트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-484">This method adds a script to the top of the rendered page.</span></span> <span data-ttu-id="f2fa7-485">클라이언트에서 명시적으로 호출 되는 함수를 추가할 때 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-485">This is useful for adding functions that will be explicitly called on the client.</span></span>

<span data-ttu-id="f2fa7-486">이 메서드의 두 오버 로드 된 버전이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-486">There are two overloaded versions of this method.</span></span> <span data-ttu-id="f2fa7-487">네 개의 인수 중 3 개는 공통적으로 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-487">Three of four arguments are common among them.</span></span> <span data-ttu-id="f2fa7-488">다음 창이 여기에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-488">They are:</span></span>

`type (string)`

<span data-ttu-id="f2fa7-489">합니다 ***형식*** 인수를 스크립트에 대 한 형식을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-489">The ***type*** argument identifies a type for the script.</span></span> <span data-ttu-id="f2fa7-490">(이 페이지의 형식을 사용 하는 것이 좋습니다는 일반적으로. 형식에 대해 GetType()) 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-490">It is generally a good idea to use the page's type (this.GetType()) for the type.</span></span>

`key (string)`

<span data-ttu-id="f2fa7-491">합니다 ***키*** 인수는 스크립트에 대 한 사용자 정의 키입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-491">The ***key*** argument is a user-defined key for the script.</span></span> <span data-ttu-id="f2fa7-492">각 스크립트에 대해 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-492">This should be unique for each script.</span></span> <span data-ttu-id="f2fa7-493">동일한 키 및 형식은 이미 추가 된 스크립트를 사용 하 여 스크립트를 추가 하려는 경우 추가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-493">If you attempt to add a script with the same key and type of an already added script, it will not be added.</span></span>

`script (string)`

<span data-ttu-id="f2fa7-494">합니다 ***스크립트*** 인수가 추가 하기 위한 실제 스크립트를 포함 하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-494">The ***script*** argument is a string containing the actual script to add.</span></span> <span data-ttu-id="f2fa7-495">StringBuilder를 사용 하 여 스크립트를 만들고 다음 할당할 StringBuilder의 tostring () 메서드를 사용 하는 것이 좋습니다 합니다 ***스크립트*** 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-495">It's recommended that you use a StringBuilder to create the script and then use the ToString() method on the StringBuilder to assign the ***script*** argument.</span></span>

<span data-ttu-id="f2fa7-496">만 세 개의 인수를 사용 하는 오버 로드 된 RegisterClientScriptBlock를 사용 하면 스크립트 요소를 포함 해야 합니다 (&lt;스크립트&gt; 하 고 &lt;/script&gt;) 스크립트에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-496">If you use the overloaded RegisterClientScriptBlock that only takes three arguments, you must include script elements (&lt;script&gt; and &lt;/script&gt;) in your script.</span></span>

<span data-ttu-id="f2fa7-497">네 번째 인수를 받아들이는 RegisterClientScriptBlock의 오버 로드를 사용 하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-497">You may choose to use the overload of RegisterClientScriptBlock that takes a fourth argument.</span></span> <span data-ttu-id="f2fa7-498">네 번째 인수에는 ASP.NET를 스크립트 요소를 추가할지 여부를 지정 하는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-498">The fourth argument is a Boolean that specifies whether or not ASP.NET should add script elements for you.</span></span> <span data-ttu-id="f2fa7-499">이 인수가 **true**, 스크립트는 스크립트 요소가 명시적으로 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-499">If this argument is **true**, your script should not include the script elements explicitly.</span></span>

<span data-ttu-id="f2fa7-500">스크립트를 이미 등록 된 경우 확인 하려면 IsClientScriptBlockRegistered 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-500">Use the IsClientScriptBlockRegistered method to determine if a script has already been registered.</span></span> <span data-ttu-id="f2fa7-501">따라서 이미 등록 된 스크립트를 다시 등록 시도가 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-501">This allows you to avoid an attempt to re-register a script that has already been registered.</span></span>

### <a name="registerclientscriptinclude-new-in-20"></a><span data-ttu-id="f2fa7-502">RegisterClientScriptInclude (2.0의 새로운 기능)</span><span class="sxs-lookup"><span data-stu-id="f2fa7-502">RegisterClientScriptInclude (New in 2.0)</span></span>

<span data-ttu-id="f2fa7-503">RegisterClientScriptInclude 태그 외부 스크립트 파일에 연결 되는 스크립트 블록을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-503">The RegisterClientScriptInclude tag creates a script block that links to an external script file.</span></span> <span data-ttu-id="f2fa7-504">두 개의 오버 로드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-504">It has two overloads.</span></span> <span data-ttu-id="f2fa7-505">하나는 키와 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-505">One takes a key and a URL.</span></span> <span data-ttu-id="f2fa7-506">두 번째 유형을 지정 하는 세 번째 인수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-506">The second adds a third argument specifying the type.</span></span>

<span data-ttu-id="f2fa7-507">예를 들어, 다음 코드에서는 스크립트 블록을 jsfunctions.js 연결 되는 응용 프로그램의 스크립트 폴더의 루트에:</span><span class="sxs-lookup"><span data-stu-id="f2fa7-507">For example, the following code generates a script block that links to jsfunctions.js in the root of the scripts folder of the application:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample17.cs)]

<span data-ttu-id="f2fa7-508">이 코드는 렌더링된 된 페이지에서 다음 코드를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-508">This code produces the following code in the rendered page:</span></span>

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample18.html)]

> [!NOTE]
> <span data-ttu-id="f2fa7-509">스크립트 블록은 페이지의 맨 아래에 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-509">The script block is rendered at the bottom of the page.</span></span>


<span data-ttu-id="f2fa7-510">스크립트를 이미 등록 된 경우 확인 하려면 IsClientScriptIncludeRegistered 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-510">Use the IsClientScriptIncludeRegistered method to determine if a script has already been registered.</span></span> <span data-ttu-id="f2fa7-511">따라서 스크립트를 다시 등록 하는 시도 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-511">This allows you to avoid an attempt to re-register a script.</span></span>

## <a name="registerstartupscript"></a><span data-ttu-id="f2fa7-512">RegisterStartupScript</span><span class="sxs-lookup"><span data-stu-id="f2fa7-512">RegisterStartupScript</span></span>

<span data-ttu-id="f2fa7-513">RegisterClientScriptBlock 방법으로 동일한 인수 RegisterStartupScript 메서드.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-513">The RegisterStartupScript method takes the same arguments as the RegisterClientScriptBlock method.</span></span> <span data-ttu-id="f2fa7-514">RegisterStartupScript를 사용 하 여 등록 된 스크립트 페이지가 로드 된 후 하기 전에 실행 OnLoad 클라이언트 쪽 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-514">A script registered with RegisterStartupScript executes after the page loads but before the OnLoad client-side event.</span></span> <span data-ttu-id="f2fa7-515">1.x를 닫기 전에 RegisterStartupScript를 사용 하 여 등록 된 스크립트 주문한 &lt;/f&gt; RegisterClientScriptBlock를 사용 하 여 등록 된 스크립트를 연 후 즉시 주문한 하는 동안 태그 &lt;폼&gt; 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-515">In 1.X, scripts registered with RegisterStartupScript were placed just before the closing &lt;/form&gt; tag while scripts registered with RegisterClientScriptBlock were placed immediately after the opening &lt;form&gt; tag.</span></span> <span data-ttu-id="f2fa7-516">ASP.NET 2.0에서는 모두 사항이 닫기 직전 &lt;/f&gt; 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-516">In ASP.NET 2.0, both are placed immediately before the closing &lt;/form&gt; tag.</span></span>

> [!NOTE]
> <span data-ttu-id="f2fa7-517">RegisterStartupScript를 사용 하 여 함수를 등록 하는 경우 클라이언트 쪽 코드에서 명시적으로 호출 될 때까지 해당 함수가 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-517">If you register a function with RegisterStartupScript, that function will not execute until you explicitly call it in client-side code.</span></span>


<span data-ttu-id="f2fa7-518">스크립트를 이미 등록 된 경우를 확인 하 고 다시 스크립트를 등록 하려고 시도 방지 하려면 IsStartupScriptRegistered 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-518">Use the IsStartupScriptRegistered method to determine if a script has already been registered and avoid an attempt to re-register a script.</span></span>

## <a name="other-clientscriptmanager-methods"></a><span data-ttu-id="f2fa7-519">다른 ClientScriptManager 메서드</span><span class="sxs-lookup"><span data-stu-id="f2fa7-519">Other ClientScriptManager Methods</span></span>

<span data-ttu-id="f2fa7-520">다음은 ClientScriptManager 클래스의 다른 유용한 메서드 중 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-520">Here are some of the other useful methods of the ClientScriptManager class.</span></span>


|  <span data-ttu-id="f2fa7-521"><strong>GetCallbackEventReference</strong></span><span class="sxs-lookup"><span data-stu-id="f2fa7-521"><strong>GetCallbackEventReference</strong></span></span>   |                                                 <span data-ttu-id="f2fa7-522">이 모듈의 앞부분에서 콜백 스크립트를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-522">See script callbacks earlier in this module.</span></span>                                                 |
|-----------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
|  <span data-ttu-id="f2fa7-523"><strong>GetPostBackClientHyperlink</strong></span><span class="sxs-lookup"><span data-stu-id="f2fa7-523"><strong>GetPostBackClientHyperlink</strong></span></span>  |                <span data-ttu-id="f2fa7-524">JavaScript 참조를 가져옵니다 (javascript:&lt;호출&gt;)는 클라이언트 쪽 이벤트에서 다시 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-524">Gets a JavaScript reference (javascript:&lt;call&gt;) that can be used to post back from a client-side event.</span></span>                 |
|  <span data-ttu-id="f2fa7-525"><strong>GetPostBackEventReference</strong></span><span class="sxs-lookup"><span data-stu-id="f2fa7-525"><strong>GetPostBackEventReference</strong></span></span>   |                                   <span data-ttu-id="f2fa7-526">클라이언트에서 다시 게시를 시작 하는 문자열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-526">Gets a string that can be used to initiate a post back from the client.</span></span>                                    |
|      <span data-ttu-id="f2fa7-527"><strong>GetWebResourceUrl</strong></span><span class="sxs-lookup"><span data-stu-id="f2fa7-527"><strong>GetWebResourceUrl</strong></span></span>       | <span data-ttu-id="f2fa7-528">어셈블리에 포함 된 리소스에 URL을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-528">Returns a URL to a resource that is embedded in an assembly.</span></span> <span data-ttu-id="f2fa7-529">와 함께 사용 해야 합니다 <strong>RegisterClientScriptResource</strong>합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-529">Must be used in conjunction with <strong>RegisterClientScriptResource</strong>.</span></span> |
| <span data-ttu-id="f2fa7-530"><strong>RegisterClientScriptResource</strong></span><span class="sxs-lookup"><span data-stu-id="f2fa7-530"><strong>RegisterClientScriptResource</strong></span></span> |     <span data-ttu-id="f2fa7-531">페이지를 사용 하 여 웹 리소스를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-531">Registers a Web resource with the page.</span></span> <span data-ttu-id="f2fa7-532">이러한 리소스가 어셈블리에 포함 하 고 새 WebResource.axd 처리기에서 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-532">These are resources embedded in an assembly and handled by the new WebResource.axd handler.</span></span>      |
|     <span data-ttu-id="f2fa7-533"><strong>RegisterHiddenField</strong></span><span class="sxs-lookup"><span data-stu-id="f2fa7-533"><strong>RegisterHiddenField</strong></span></span>      |                                                 <span data-ttu-id="f2fa7-534">페이지를 사용 하 여 숨겨진된 양식 필드를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-534">Registers a hidden form field with the page.</span></span>                                                 |
|  <span data-ttu-id="f2fa7-535"><strong>RegisterOnSubmitStatement</strong></span><span class="sxs-lookup"><span data-stu-id="f2fa7-535"><strong>RegisterOnSubmitStatement</strong></span></span>   |                                  <span data-ttu-id="f2fa7-536">HTML 폼이 제출 될 때 실행 되는 클라이언트 쪽 코드를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fa7-536">Registers client-side code that executes when the HTML form is submitted.</span></span>                                   |

