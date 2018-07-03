---
uid: mvc/overview/releases/mvc51-release-notes
title: ASP.NET MVC 5.1의에서 새로운 기능 | Microsoft Docs
author: microsoft
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/27/2014
ms.topic: article
ms.assetid: 9a83a058-9b01-48aa-acce-ec041e694567
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/releases/mvc51-release-notes
msc.type: authoredcontent
ms.openlocfilehash: 2b63ca8868bbf31be569e2eb2edb51141b9f4330
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37362764"
---
<a name="whats-new-in-aspnet-mvc-51"></a><span data-ttu-id="df114-102">ASP.NET MVC 5.1의에서 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="df114-102">What's New in ASP.NET MVC 5.1</span></span>
====================
<span data-ttu-id="df114-103">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="df114-103">by [Microsoft](https://github.com/microsoft)</span></span>

<span data-ttu-id="df114-104">이 항목에서는 ASP.NET 웹 MVC 5.1의 새로운 기능을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="df114-104">This topic describes what's new for ASP.NET Web MVC 5.1.</span></span>

- [<span data-ttu-id="df114-105">소프트웨어 요구 사항</span><span class="sxs-lookup"><span data-stu-id="df114-105">Software Requirements</span></span>](#SoftwareRequirements)
- [<span data-ttu-id="df114-106">다운로드</span><span class="sxs-lookup"><span data-stu-id="df114-106">Download</span></span>](#download)
- [<span data-ttu-id="df114-107">문서</span><span class="sxs-lookup"><span data-stu-id="df114-107">Documentation</span></span>](#documentation)
- [<span data-ttu-id="df114-108">ASP.NET MVC 5.1의에서 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="df114-108">New Features in ASP.NET MVC 5.1</span></span>](#new-features)

    - [<span data-ttu-id="df114-109">특성 라우팅 기능 향상</span><span class="sxs-lookup"><span data-stu-id="df114-109">Attribute routing improvements</span></span>](#AttributeRouting)
    - [<span data-ttu-id="df114-110">부트스트랩 편집기 템플릿 지원</span><span class="sxs-lookup"><span data-stu-id="df114-110">Bootstrap support for editor templates</span></span>](#Bootstrap)
    - [<span data-ttu-id="df114-111">보기에서 열거형 지원</span><span class="sxs-lookup"><span data-stu-id="df114-111">Enum support in views</span></span>](#Enum)
    - [<span data-ttu-id="df114-112">MinLength/MaxLength 특성에 대 한 비간섭 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="df114-112">Unobtrusive validation for MinLength/MaxLength Attributes</span></span>](#Unobtrusive)
    - [<span data-ttu-id="df114-113">'This'이 컨텍스트 눈에 띄지 않는 ajax 지원</span><span class="sxs-lookup"><span data-stu-id="df114-113">Supporting the ‘this' context in Unobtrusive Ajax</span></span>](#thisContext)
- <span data-ttu-id="df114-114">[알려진 문제 및 주요 변경 내용](#KnownBreakingChanges)- [버그 수정](#bug-fixes)</span><span class="sxs-lookup"><span data-stu-id="df114-114">[Known Issues and Breaking Changes](#KnownBreakingChanges)- [Bug Fixes](#bug-fixes)</span></span>

<a id="SoftwareRequirements"></a>
## <a name="software-requirements"></a><span data-ttu-id="df114-115">소프트웨어 요구 사항</span><span class="sxs-lookup"><span data-stu-id="df114-115">Software Requirements</span></span>

- <span data-ttu-id="df114-116">Visual Studio 2012: 다운로드 [ASP.NET 및 웹 도구 2013.1 Visual Studio 2012 용](https://go.microsoft.com/fwlink/?LinkId=390062)합니다.</span><span class="sxs-lookup"><span data-stu-id="df114-116">Visual Studio 2012: Download [ASP.NET and Web Tools 2013.1 for Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkId=390062).</span></span>
- <span data-ttu-id="df114-117">Visual Studio 2013: 다운로드 [Visual Studio 2013 업데이트 1](https://go.microsoft.com/fwlink/?LinkId=390064)합니다.</span><span class="sxs-lookup"><span data-stu-id="df114-117">Visual Studio 2013: Download [Visual Studio 2013 Update 1](https://go.microsoft.com/fwlink/?LinkId=390064).</span></span> <span data-ttu-id="df114-118">이 업데이트는 ASP.NET MVC 5.1 Razor 뷰를 편집 하기 위해 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="df114-118">This update is needed for editing ASP.NET MVC 5.1 Razor Views.</span></span>

<a id="download"></a>
## <a name="download"></a><span data-ttu-id="df114-119">다운로드</span><span class="sxs-lookup"><span data-stu-id="df114-119">Download</span></span>

<span data-ttu-id="df114-120">NuGet 갤러리에서 NuGet 패키지로 런타임 기능 해제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df114-120">The runtime features are released as NuGet packages on the NuGet gallery.</span></span> <span data-ttu-id="df114-121">모든 런타임 패키지를 수행 합니다 [유의 적 버전](http://semver.org/) 사양입니다.</span><span class="sxs-lookup"><span data-stu-id="df114-121">All the runtime packages follow the [Semantic Versioning](http://semver.org/) specification.</span></span> <span data-ttu-id="df114-122">다음 버전이 최신 ASP.NET MVC 5.1 RTM 패키지: "5.1.2"입니다.</span><span class="sxs-lookup"><span data-stu-id="df114-122">The latest ASP.NET MVC 5.1 RTM package has the following version: "5.1.2".</span></span> <span data-ttu-id="df114-123">설치 하거나 이러한 패키지를 통해 업데이트할 수 있습니다 [NuGet](http://www.nuget.org/packages/Microsoft.AspNet.Mvc/)합니다.</span><span class="sxs-lookup"><span data-stu-id="df114-123">You can install or update these packages through [NuGet](http://www.nuget.org/packages/Microsoft.AspNet.Mvc/).</span></span> <span data-ttu-id="df114-124">릴리스에 NuGet의 해당 지역화 된 패키지도 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df114-124">The release also includes corresponding localized packages on NuGet.</span></span>

<span data-ttu-id="df114-125">설치 하거나 NuGet 패키지 관리자 콘솔을 사용 하 여 릴리스된 NuGet 패키지를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df114-125">You can install or update to the released NuGet packages by using the NuGet Package Manager Console:</span></span>

[!code-console[Main](mvc51-release-notes/samples/sample1.cmd)]

<a id="documentation"></a>
## <a name="documentation"></a><span data-ttu-id="df114-126">설명서</span><span class="sxs-lookup"><span data-stu-id="df114-126">Documentation</span></span>

<span data-ttu-id="df114-127">자습서 및 ASP.NET MVC 5.1 RTM에 대 한 다른 정보는 ASP.NET 웹 사이트에서 사용할 수 있습니다 ( https://www.asp.net)합니다.</span><span class="sxs-lookup"><span data-stu-id="df114-127">Tutorials and other information about ASP.NET MVC 5.1 RTM are available from the ASP.NET web site ( https://www.asp.net).</span></span> 

<a id="new-features"></a>
## <a name="new-features-in-aspnet-mvc-51"></a><span data-ttu-id="df114-128">ASP.NET MVC 5.1의에서 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="df114-128">New Features in ASP.NET MVC 5.1</span></span>

<a id="AttributeRouting"></a>

### <a name="attribute-routing-improvements"></a><span data-ttu-id="df114-129">특성 라우팅 기능 향상</span><span class="sxs-lookup"><span data-stu-id="df114-129">Attribute routing improvements</span></span>

 <span data-ttu-id="df114-130">특성 라우팅을 지원 제약 조건, 버전 관리 및 헤더를 사용 하도록 설정 하면 이제 경로 선택 영역을 기준으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="df114-130">Attribute routing now supports constraints, enabling versioning and header based route selection.</span></span> <span data-ttu-id="df114-131">특성 경로의 다양 한 측면을 통해 사용자 지정 가능한 됩니다 합니다 `IDirectRouteFactory` 인터페이스 및 `RouteFactoryAttribute` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="df114-131">Many aspects of attribute routes are now customizable via the `IDirectRouteFactory` interface and `RouteFactoryAttribute` class.</span></span> <span data-ttu-id="df114-132">경로 접두사는 이제 통해 확장이 가능 합니다 `IRoutePrefix` 인터페이스 및 `RoutePrefixAttribute` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="df114-132">The route prefix is now extensible via the `IRoutePrefix` interface and `RoutePrefixAttribute` class.</span></span> 

<a id="Enum"></a>

### <a name="enum-support-in-views"></a><span data-ttu-id="df114-133">보기에서 열거형 지원</span><span class="sxs-lookup"><span data-stu-id="df114-133">Enum support in views</span></span>

1. <span data-ttu-id="df114-134">새 `@Html.EnumDropDownListFor()` 도우미 메서드.</span><span class="sxs-lookup"><span data-stu-id="df114-134">New `@Html.EnumDropDownListFor()` helper methods.</span></span> <span data-ttu-id="df114-135">이러한 대부분의 식은 해야 하는 caveat 사용 하 여 HTML 도우미와 같은 사용 해야는 [enum](https://msdn.microsoft.com/en-us/library/cc138362.aspx) 형식 또는 [Nullable&lt;T&gt; ](https://msdn.microsoft.com/en-us/library/2cf62fcy.aspx) 여기서 `T` 되는 [enum](https://msdn.microsoft.com/en-us/library/cc138362.aspx) 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="df114-135">These should be used like most of the HTML helpers with the caveat that the expression must evaluate to an [enum](https://msdn.microsoft.com/en-us/library/cc138362.aspx) type or a [Nullable&lt;T&gt;](https://msdn.microsoft.com/en-us/library/2cf62fcy.aspx) where `T` is an [enum](https://msdn.microsoft.com/en-us/library/cc138362.aspx) type.</span></span> <span data-ttu-id="df114-136">사용 하 여 `EnumHelper.IsValidForEnumHelper()` 이러한 요구 사항을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="df114-136">Use `EnumHelper.IsValidForEnumHelper()` to check these requirements.</span></span>
2. <span data-ttu-id="df114-137">새 `EnumHelper.GetSelectList()` 반환 하는 메서드에 `IList<SelectListItem>`합니다.</span><span class="sxs-lookup"><span data-stu-id="df114-137">New `EnumHelper.GetSelectList()` methods which return an `IList<SelectListItem>`.</span></span> <span data-ttu-id="df114-138">예를 들어을 호출 하기 전에 선택 목록 조작 해야 하는 경우에 유용 `@Html.DropDownListFor()`, 이름이 표시 하려는 경우 또는 `@Html.EnumDropDownListFor()` 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="df114-138">This is useful when you need to manipulate a select list prior to calling, for example, `@Html.DropDownListFor()`, or when you wish to display the names which `@Html.EnumDropDownListFor()` shows.</span></span>

<span data-ttu-id="df114-139">다음 코드는 이러한 Api를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="df114-139">The following code shows these APIs.</span></span>

[!code-cshtml[Main](mvc51-release-notes/samples/sample2.cshtml)]

<span data-ttu-id="df114-140">전체 예제를 볼 수 있습니다 [여기](https://aspnet.codeplex.com/SourceControl/latest#Samples/MVC/EnumSample/)합니다.</span><span class="sxs-lookup"><span data-stu-id="df114-140">You can see a complete example [here](https://aspnet.codeplex.com/SourceControl/latest#Samples/MVC/EnumSample/).</span></span>

<a id="Bootstrap"></a>

### <a name="bootstrap-support-for-editor-templates"></a><span data-ttu-id="df114-141">부트스트랩 편집기 템플릿 지원</span><span class="sxs-lookup"><span data-stu-id="df114-141">Bootstrap support for editor templates</span></span>

<span data-ttu-id="df114-142">HTML 특성에서 이제 전달 하도록 허용 했습니다 [EditorFor](https://msdn.microsoft.com/en-us/library/system.web.mvc.html.editorextensions.editorfor(v=vs.100).aspx) 으로 [익명 개체](https://msdn.microsoft.com/en-us/library/bb397696.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="df114-142">We now allow passing in HTML attributes in [EditorFor](https://msdn.microsoft.com/en-us/library/system.web.mvc.html.editorextensions.editorfor(v=vs.100).aspx) as an [anonymous object](https://msdn.microsoft.com/en-us/library/bb397696.aspx).</span></span>

<span data-ttu-id="df114-143">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="df114-143">For example:</span></span>

[!code-cshtml[Main](mvc51-release-notes/samples/sample3.cshtml)]

<a id="Unobtrusive"></a>

### <a name="unobtrusive-validation-for-minlengthattribute-and-maxlengthattribute"></a><span data-ttu-id="df114-144">MinLengthAttribute MaxLengthAttribute 한 눈에 띄지 않는 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="df114-144">Unobtrusive validation for MinLengthAttribute and MaxLengthAttribute</span></span>

<span data-ttu-id="df114-145">문자열 및 배열 형식에 대 한 클라이언트 쪽 유효성 검사로 데코 레이트 속성 이제 지원 됩니다 합니다 [MinLength](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.minlengthattribute(v=vs.110).aspx) 하 고 [MaxLength](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.maxlengthattribute(v=vs.110).aspx) 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="df114-145">Client-side validation for string and array types will now be supported for properties decorated with the [MinLength](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.minlengthattribute(v=vs.110).aspx) and [MaxLength](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.maxlengthattribute(v=vs.110).aspx) attributes.</span></span>

<a id="thisContext"></a>

### <a name="supporting-the-this-context-in-unobtrusive-ajax"></a><span data-ttu-id="df114-146">'This'이 컨텍스트 눈에 띄지 않는 ajax 지원</span><span class="sxs-lookup"><span data-stu-id="df114-146">Supporting the ‘this' context in Unobtrusive Ajax</span></span>

<span data-ttu-id="df114-147">콜백 함수 (`OnBegin, OnComplete, OnFailure, OnSuccess`)를 통해 호출 요소를 찾는 수 이제는 `this` 컨텍스트.</span><span class="sxs-lookup"><span data-stu-id="df114-147">The callback functions (`OnBegin, OnComplete, OnFailure, OnSuccess`) will now be able to locate the invoking element via the `this` context.</span></span> <span data-ttu-id="df114-148">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="df114-148">For example:</span></span>

[!code-html[Main](mvc51-release-notes/samples/sample4.html)]

<a id="KnownBreakingChanges"></a>

## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="df114-149">알려진된 문제 및 주요 변경 내용</span><span class="sxs-lookup"><span data-stu-id="df114-149">Known Issues and Breaking Changes</span></span>

### <a name="attribute-routing"></a><span data-ttu-id="df114-150">특성 라우팅</span><span class="sxs-lookup"><span data-stu-id="df114-150">Attribute Routing</span></span>

<span data-ttu-id="df114-151">특성 라우팅 일치 항목이 모호성 이제 첫 번째 일치 항목을 선택 하는 대신 오류로 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="df114-151">Ambiguities in attribute routing matches will now report an error rather than choosing the first match.</span></span>

<span data-ttu-id="df114-152">특성 경로를 사용할 수 없습니다는 `{controller}` 매개 변수를 사용 하는 `{action}` 경로에 매개 변수 작업에 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="df114-152">Attribute routes are prohibited from using the `{controller}` parameter, and from using the `{action}` parameter on routes placed on actions.</span></span> <span data-ttu-id="df114-153">이러한 매개 변수 사용 모호성을 초래할 가능성이 매우 합니다.</span><span class="sxs-lookup"><span data-stu-id="df114-153">Uses of these parameters would very likely lead to ambiguities.</span></span> 

### <a name="scaffolding-mvcweb-api-into-a-project-with-51-packages-results-in-50-packages-for-ones-that-dont-already-exist-in-the-project"></a><span data-ttu-id="df114-154">프로젝트에 이미 존재 하지 않는 것에 대 한 패키지를 5.0에서 5.1 패키지 결과 사용 하 여 프로젝트에 스 캐 폴딩 MVC/웹 API</span><span class="sxs-lookup"><span data-stu-id="df114-154">Scaffolding MVC/Web API into a project with 5.1 packages results in 5.0 packages for ones that don't already exist in the project</span></span>

<span data-ttu-id="df114-155">ASP.NET MVC 5.1 RTM에 대 한 NuGet 패키지를 업데이트 해도 ASP.NET 스 캐 폴딩와 같은 Visual Studio 도구 또는 ASP.NET 웹 응용 프로그램 프로젝트 템플릿을 업데이트 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="df114-155">Updating NuGet packages for ASP.NET MVC 5.1 RTM does not update the Visual Studio tools such as ASP.NET scaffolding or the ASP.NET Web Application project template.</span></span> <span data-ttu-id="df114-156">이전 버전의 ASP.NET 런타임 패키지 (5.0.0.0)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="df114-156">They use the previous version of the ASP.NET runtime packages (5.0.0.0).</span></span> <span data-ttu-id="df114-157">결과적으로, ASP.NET 스 캐 폴딩은 이미 프로젝트에서 사용할 수 없는 경우에 필요한 패키지의 이전 버전 (5.0.0.0)으로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df114-157">As a result, the ASP.NET scaffolding will install the previous version (5.0.0.0) of the required packages, if they are not already available in your projects.</span></span> <span data-ttu-id="df114-158">그러나 Visual Studio 2013 RTM 또는 업데이트 1에서 ASP.NET 스 캐 폴딩 프로젝트에서 최신 패키지를 덮어쓰지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="df114-158">However, the ASP.NET scaffolding in Visual Studio 2013 RTM or Update 1 does not overwrite the latest packages in your projects.</span></span> <span data-ttu-id="df114-159">ASP.NET Web API 2.1 또는 ASP.NET MVC 5.1에 프로젝트의 패키지를 업데이트 한 후에 스 캐 폴딩을 사용 하는 경우 Web API 및 ASP.NET MVC의 버전이 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="df114-159">If you use ASP.NET scaffolding after updating the packages of your projects to Web API 2.1 or ASP.NET MVC 5.1, make sure the versions of Web API and ASP.NET MVC are consistent.</span></span> 

### <a name="syntax-highlighting-for-razor-views-in-visual-studio-2013"></a><span data-ttu-id="df114-160">Visual Studio 2013의 Razor 보기에 대 한 구문 강조 표시</span><span class="sxs-lookup"><span data-stu-id="df114-160">Syntax Highlighting for Razor Views in Visual Studio 2013</span></span>

<span data-ttu-id="df114-161">Visual Studio 2013 업데이트 하지 않고 ASP.NET MVC 5.1 RTM을 업데이트 하는 경우 Razor 뷰를 편집 하는 동안 구문 강조 표시에 대 한 Visual Studio 편집기 지원이 제공 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="df114-161">If you update to ASP.NET MVC 5.1 RTM without updating Visual Studio 2013, you will not get Visual Studio editor support for syntax highlighting while editing the Razor views.</span></span> <span data-ttu-id="df114-162">이 지원을 받으려면 Visual Studio 2013 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="df114-162">You will need to update Visual Studio 2013 to get this support.</span></span> 

### <a name="type-renames"></a><span data-ttu-id="df114-163">형식 이름 바꾸기</span><span class="sxs-lookup"><span data-stu-id="df114-163">Type Renames</span></span>

<span data-ttu-id="df114-164">특성 라우팅 확장성에 사용 되는 형식 중 일부는 5.1 RTM에서 이름이 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df114-164">Some of the types used for attribute routing extensibility are renamed in 5.1 RTM.</span></span>

| <span data-ttu-id="df114-165">**이전 형식 이름 (5.1 RC)**</span><span class="sxs-lookup"><span data-stu-id="df114-165">**Old Type Name (5.1 RC)**</span></span> | <span data-ttu-id="df114-166">**새 형식 이름을 (5.1 RTM)**</span><span class="sxs-lookup"><span data-stu-id="df114-166">**New Type Name (5.1 RTM)**</span></span> |
| --- | --- |
| <span data-ttu-id="df114-167">IDirectRouteProvider</span><span class="sxs-lookup"><span data-stu-id="df114-167">IDirectRouteProvider</span></span> | <span data-ttu-id="df114-168">IDirectRouteFactory</span><span class="sxs-lookup"><span data-stu-id="df114-168">IDirectRouteFactory</span></span> |
| <span data-ttu-id="df114-169">RouteProviderAttribute</span><span class="sxs-lookup"><span data-stu-id="df114-169">RouteProviderAttribute</span></span> | <span data-ttu-id="df114-170">RouteFactoryAttribute</span><span class="sxs-lookup"><span data-stu-id="df114-170">RouteFactoryAttribute</span></span> |
| <span data-ttu-id="df114-171">DirectRouteProviderContext</span><span class="sxs-lookup"><span data-stu-id="df114-171">DirectRouteProviderContext</span></span> | <span data-ttu-id="df114-172">DirectRouteFactoryContext</span><span class="sxs-lookup"><span data-stu-id="df114-172">DirectRouteFactoryContext</span></span> |

<a id="bug-fixes"></a>
## <a name="bug-fixes"></a><span data-ttu-id="df114-173">버그 수정</span><span class="sxs-lookup"><span data-stu-id="df114-173">Bug Fixes</span></span>

<span data-ttu-id="df114-174">이 이번에는 여러 버그 수정도 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df114-174">This release also includes several bug fixes.</span></span> <span data-ttu-id="df114-175">여기서 전체 목록을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df114-175">You can find the complete list here:</span></span>

- [<span data-ttu-id="df114-176">5.1.0 패키지</span><span class="sxs-lookup"><span data-stu-id="df114-176">5.1.0 package</span></span>](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=Closed&amp;type=All&amp;priority=All&amp;release=v5.1%20Preview|v5.1%20RTM&amp;assignedTo=All&amp;component=MVC&amp;sortField=AssignedTo&amp;sortDirection=Ascending&amp;page=0&amp;reasonClosed=Fixed)
- [<span data-ttu-id="df114-177">5.1.1 패키지</span><span class="sxs-lookup"><span data-stu-id="df114-177">5.1.1 package</span></span>](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=v5.1.1%20RTM&amp;assignedTo=All&amp;component=MVC&amp;sortField=AssignedTo&amp;sortDirection=Ascending&amp;page=0&amp;reasonClosed=Fixed)

<span data-ttu-id="df114-178">5.1.2 없습니다 버그 수정 하지만 IntelliSense 업데이트 패키지에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df114-178">The 5.1.2 package contains IntelliSense updates but no bug fixes.</span></span>
