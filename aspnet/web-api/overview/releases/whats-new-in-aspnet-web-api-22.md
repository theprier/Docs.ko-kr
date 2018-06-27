---
uid: web-api/overview/releases/whats-new-in-aspnet-web-api-22
title: ASP.NET Web API 2.2의에서 새로운 기능 | Microsoft Docs
author: microsoft
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/25/2014
ms.topic: article
ms.assetid: 99c59ae4-167e-4f66-a6cd-d3f1098c4e4a
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/releases/whats-new-in-aspnet-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: 89b065fccd0e4864f4a24c37b4caa29a1e127840
ms.sourcegitcommit: 356c8d394aaf384c834e9c90cabab43bfe36e063
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2018
ms.locfileid: "36961301"
---
<a name="whats-new-in-aspnet-web-api-22"></a><span data-ttu-id="bc1ec-102">ASP.NET Web API 2.2의에서 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="bc1ec-102">What's New in ASP.NET Web API 2.2</span></span>
====================
<span data-ttu-id="bc1ec-103">여 [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="bc1ec-103">by [Microsoft](https://github.com/microsoft)</span></span>

<span data-ttu-id="bc1ec-104">이 항목에서는 ASP.NET 웹 API 2.2에 대 한 새로운 기능을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-104">This topic describes what's new for ASP.NET Web API 2.2.</span></span>

- [<span data-ttu-id="bc1ec-105">다운로드</span><span class="sxs-lookup"><span data-stu-id="bc1ec-105">Download</span></span>](#download)
- [<span data-ttu-id="bc1ec-106">문서</span><span class="sxs-lookup"><span data-stu-id="bc1ec-106">Documentation</span></span>](#documentation)
- [<span data-ttu-id="bc1ec-107">ASP.NET Web API 2.2의에서 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="bc1ec-107">New Features in ASP.NET Web API 2.2</span></span>](#newf)

    - [<span data-ttu-id="bc1ec-108">OData v4</span><span class="sxs-lookup"><span data-stu-id="bc1ec-108">OData v4</span></span>](#OData)
    - [<span data-ttu-id="bc1ec-109">라우팅 향상 된 기능 특성</span><span class="sxs-lookup"><span data-stu-id="bc1ec-109">Attribute Routing Improvements</span></span>](#ARI)
    - [<span data-ttu-id="bc1ec-110">Windows Phone 8.1에 대 한 웹 API 클라이언트 지원</span><span class="sxs-lookup"><span data-stu-id="bc1ec-110">Web API Client support for Windows Phone 8.1</span></span>](#phone)
- [<span data-ttu-id="bc1ec-111">알려진된 문제 및 주요 변경 내용</span><span class="sxs-lookup"><span data-stu-id="bc1ec-111">Known Issues and Breaking Changes</span></span>](#known-issues)
- [<span data-ttu-id="bc1ec-112">버그 수정</span><span class="sxs-lookup"><span data-stu-id="bc1ec-112">Bug Fixes</span></span>](#bug-fixes)
- [<span data-ttu-id="bc1ec-113">Microsoft.AspNet.OData 5.2.1</span><span class="sxs-lookup"><span data-stu-id="bc1ec-113">Microsoft.AspNet.OData 5.2.1</span></span>](#odata521)
- [<span data-ttu-id="bc1ec-114">5.2.2 Microsoft.AspNet.WebAPI</span><span class="sxs-lookup"><span data-stu-id="bc1ec-114">Microsoft.AspNet.WebAPI 5.2.2</span></span>](#522RC)
- [<span data-ttu-id="bc1ec-115">5.2.3 Microsoft.AspNet.WebAPI 베타</span><span class="sxs-lookup"><span data-stu-id="bc1ec-115">Microsoft.AspNet.WebAPI 5.2.3 Beta</span></span>](#523)

<a id="download"></a>
## <a name="download"></a><span data-ttu-id="bc1ec-116">다운로드</span><span class="sxs-lookup"><span data-stu-id="bc1ec-116">Download</span></span>

<span data-ttu-id="bc1ec-117">런타임 기능은 NuGet 갤러리에서 NuGet 패키지로 해제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-117">The runtime features are released as NuGet packages on the NuGet gallery.</span></span> <span data-ttu-id="bc1ec-118">모든 런타임 패키지에 따라는 [의미 체계 버전 관리](http://semver.org/) 사양입니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-118">All the runtime packages follow the [Semantic Versioning](http://semver.org/) specification.</span></span> <span data-ttu-id="bc1ec-119">최신 ASP.NET 웹 API 2.2 패키지에는 다음 버전: "5.2.0"입니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-119">The latest ASP.NET Web API 2.2 package has the following version: "5.2.0".</span></span> <span data-ttu-id="bc1ec-120">설치 또는 업데이트를 통해 이러한 패키지 [NuGet](http://www.nuget.org/packages/Microsoft.AspNet.WebApi/)합니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-120">You can install or update these packages through [NuGet](http://www.nuget.org/packages/Microsoft.AspNet.WebApi/).</span></span> <span data-ttu-id="bc1ec-121">릴리스에 NuGet에 해당 지역화 된 패키지도 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-121">The release also includes corresponding localized packages on NuGet.</span></span>

<span data-ttu-id="bc1ec-122">설치 하거나 NuGet 패키지 관리자 콘솔을 사용 하 여 출시 된 NuGet 패키지를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-122">You can install or update to the released NuGet packages by using the NuGet Package Manager Console:</span></span>

[!code-console[Main](whats-new-in-aspnet-web-api-22/samples/sample1.cmd)]

<a id="documentation"></a>
## <a name="documentation"></a><span data-ttu-id="bc1ec-123">설명서</span><span class="sxs-lookup"><span data-stu-id="bc1ec-123">Documentation</span></span>

<span data-ttu-id="bc1ec-124">ASP.NET 웹 사이트에서 사용할 수 있는 자습서 및 ASP.NET 웹 API 2.2에 대 한 기타 정보 ([https://www.asp.net/web-api](../../index.md)).</span><span class="sxs-lookup"><span data-stu-id="bc1ec-124">Tutorials and other information about ASP.NET Web API 2.2 are available from the ASP.NET web site ([https://www.asp.net/web-api](../../index.md)).</span></span>

<a id="newf"></a>
## <a name="new-features-in-aspnet-web-api-22"></a><span data-ttu-id="bc1ec-125">ASP.NET Web API 2.2의에서 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="bc1ec-125">New Features in ASP.NET Web API 2.2</span></span>

<a id="OData"></a>
### <a name="odata-v4"></a><span data-ttu-id="bc1ec-126">OData v4</span><span class="sxs-lookup"><span data-stu-id="bc1ec-126">OData v4</span></span>

<span data-ttu-id="bc1ec-127">이 릴리스에서 OData v4 프로토콜에 대 한 지원을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-127">This release adds support for the OData v4 protocol.</span></span> <span data-ttu-id="bc1ec-128">자세한 내용은 참조는 [Web API OData v4 설명서입니다.](../odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint.md)</span><span class="sxs-lookup"><span data-stu-id="bc1ec-128">For more information, see the [Web API OData v4 documentation.](../odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint.md)</span></span>

<span data-ttu-id="bc1ec-129">다음은 몇 가지 주요 기능 및 OData v 4에 대 한 변경입니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-129">Here are some of the key features and changes for OData v4:</span></span>

- [<span data-ttu-id="bc1ec-130">OData 모델의 별칭 속성에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="bc1ec-130">Support for aliasing properties in OData model</span></span>](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataModelAliasingSample/)
- [<span data-ttu-id="bc1ec-131">ComplexTypeAttribute, AssociationAttribute, TimesTampAttribute 및 ConcurrencyCheckAttribute ODataConventionModelBuilder에에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="bc1ec-131">Support for ComplexTypeAttribute, AssociationAttribute, TimesTampAttribute and ConcurrencyCheckAttribute in ODataConventionModelBuilder</span></span>](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataEtagSample/)
- [<span data-ttu-id="bc1ec-132">작업에 대 한 친숙 한 Title을 제공 하는 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-132">Provide ability to supply friendly Title for actions</span></span>](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataActionsSample/)
- <span data-ttu-id="bc1ec-133">ODL UriParser와 통합</span><span class="sxs-lookup"><span data-stu-id="bc1ec-133">Integrate with ODL UriParser</span></span>
- <span data-ttu-id="bc1ec-134">에 대 한 지원 [enum](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataEnumTypeSample/ODataEnumTypeSample/), [제약](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataContainmentSample/) 및 [singleton](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataSingletonSample/)</span><span class="sxs-lookup"><span data-stu-id="bc1ec-134">Support for [enum](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataEnumTypeSample/ODataEnumTypeSample/), [containment](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataContainmentSample/) and [singleton](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataSingletonSample/)</span></span>
- <span data-ttu-id="bc1ec-135">기본 형식에 캐스팅 지원</span><span class="sxs-lookup"><span data-stu-id="bc1ec-135">Support cast for primitive types</span></span>
- [<span data-ttu-id="bc1ec-136">OData 함수 지원 추가</span><span class="sxs-lookup"><span data-stu-id="bc1ec-136">Added OData function support</span></span>](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataFunctionSample/)
- [<span data-ttu-id="bc1ec-137">함수 호출에 대 한 매개 변수 별칭을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-137">Support parameter aliases for function calls</span></span>](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataFunctionSample/)
- [<span data-ttu-id="bc1ec-138">모델에 카멜 케이스 명명 규칙을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-138">Support camel case naming convention in model</span></span>](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataCamelCaseSample/)
- <span data-ttu-id="bc1ec-139">캐스팅할 $filter에에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="bc1ec-139">Support for cast() in $filter</span></span>
- <span data-ttu-id="bc1ec-140">개방형 복합 형식에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="bc1ec-140">Support for open complex type</span></span>
- <span data-ttu-id="bc1ec-141">제거 EntitySetController 및 AsyncEntitySetController</span><span class="sxs-lookup"><span data-stu-id="bc1ec-141">Removed EntitySetController and AsyncEntitySetController</span></span>
- [<span data-ttu-id="bc1ec-142">변경 된 $link $ref</span><span class="sxs-lookup"><span data-stu-id="bc1ec-142">Changed $link to $ref</span></span>](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataServiceSample/)
- [<span data-ttu-id="bc1ec-143">특성 라우팅 지원 추가</span><span class="sxs-lookup"><span data-stu-id="bc1ec-143">Added Attribute routing support</span></span>](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataAttributeRoutingSample/)
- <span data-ttu-id="bc1ec-144">6.4.0 OData 핵심 라이브러리를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="bc1ec-144">Uses OData Core Libraries 6.4.0</span></span>

<a id="ARI"></a>
### <a name="attribute-routing-improvements"></a><span data-ttu-id="bc1ec-145">라우팅 향상 된 기능 특성</span><span class="sxs-lookup"><span data-stu-id="bc1ec-145">Attribute Routing Improvements</span></span>

<span data-ttu-id="bc1ec-146">특성 라우팅을 이제 호출 IDirectRouteProvider 특성 경로 검색 하 고 구성 하는 방식을 완전히 제어할 수 있는 확장성 지점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-146">Attribute Routing now provides an extensibility point called IDirectRouteProvider, which allows full control over how attribute routes are discovered and configured.</span></span> <span data-ttu-id="bc1ec-147">IDirectRouteProvider는 이러한 작업에 대 한 어떤 라우팅 구성이 가능 정확 하 게 지정 하려면 연결 된 경로 정보 함께 컨트롤러 및 작업의 목록을 제공 하는 일을 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-147">An IDirectRouteProvider is responsible for providing a list of actions and controllers along with associated route information to specify exactly what routing configuration is desired for those actions.</span></span> <span data-ttu-id="bc1ec-148">IDirectRouteProvider 구현은 MapAttributes/MapHttpAttributeRoutes를 호출할 때 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-148">An IDirectRouteProvider implementation may be specified when calling MapAttributes/MapHttpAttributeRoutes.</span></span>

<span data-ttu-id="bc1ec-149">IDirectRouteProvider 사용자 지정의 기본 구현에서는 DefaultDirectRouteProvider를 확장 하 여 가장 쉬운 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-149">Customizing IDirectRouteProvider will be easiest by extending our default implementation, DefaultDirectRouteProvider.</span></span> <span data-ttu-id="bc1ec-150">이 클래스는 특성 검색 경로 항목을 만들고 경로 접두사와 영역 접두사를 검색 하기 위한 논리를 변경 하는 별도 재정의 가능한 가상 메서드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-150">This class provides separate overridable virtual methods to change the logic for discovering attributes, creating route entries, and discovering route prefix and area prefix.</span></span>

<span data-ttu-id="bc1ec-151">다음은이 새로운 확장 지점으로 수행할 수는 몇 가지 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-151">Following are some examples on what you could do with this new extensibility point:</span></span>

1. <span data-ttu-id="bc1ec-152">경로 특성 상속을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-152">Support inheritance of Route attributes</span></span>

    <span data-ttu-id="bc1ec-153">예제:</span><span class="sxs-lookup"><span data-stu-id="bc1ec-153">Example:</span></span>

    <span data-ttu-id="bc1ec-154">Like "/ 10/api/값" 요청은 "성공: 10"을 성공적으로 여기 반환</span><span class="sxs-lookup"><span data-stu-id="bc1ec-154">Here a request like "/api/values/10" would successfully return "Success:10"</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-web-api-22/samples/sample2.cs)]
2. <span data-ttu-id="bc1ec-155">원하는 몇 가지 규칙에 따라 특성 경로 대 한 기본 경로 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-155">Provide a default route name for your attribute routes by following some convention you like.</span></span> <span data-ttu-id="bc1ec-156">기본적으로 특성 라우팅을 특성 경로 대 한 이름을 만들 자동으로 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-156">By default, attribute routing doesn't automatically create names for attribute routes.</span></span>
3. <span data-ttu-id="bc1ec-157">경로 테이블에 결국 전에 하나의 중앙 위치에 경로 템플릿을 특성 경로 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-157">Modify attribute routes' route template at one central place before they end up in the route table.</span></span>

<a id="phone"></a>
### <a name="web-api-client-support-for-windows-phone-81"></a><span data-ttu-id="bc1ec-158">Windows Phone 8.1에 대 한 웹 API 클라이언트 지원</span><span class="sxs-lookup"><span data-stu-id="bc1ec-158">Web API Client Support for Windows Phone 8.1</span></span>

<span data-ttu-id="bc1ec-159">이제 Windows Phone 8.1을 대상으로 할 때 또는 웹 API 클라이언트 논리를 구현 하는 웹 API 클라이언트 NuGet 패키지를 사용할 수 있습니다는 유니버설 앱 내에서.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-159">You can now use the Web API Client NuGet package to implement your Web API client logic when targeting Windows Phone 8.1 or from within a Universal App.</span></span>

<a id="known-issues"></a>
## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="bc1ec-160">알려진된 문제 및 주요 변경 내용</span><span class="sxs-lookup"><span data-stu-id="bc1ec-160">Known Issues and Breaking Changes</span></span>

<span data-ttu-id="bc1ec-161">이 섹션에서는 알려진된 문제 및 ASP.NET 웹 API 2.2의 주요 변경 내용에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-161">This section describes known issues and breaking changes in the ASP.NET Web API 2.2.</span></span>

### <a name="odata-v4"></a><span data-ttu-id="bc1ec-162">OData v4</span><span class="sxs-lookup"><span data-stu-id="bc1ec-162">OData v4</span></span>

#### <a name="model-builder"></a><span data-ttu-id="bc1ec-163">모델 작성기</span><span class="sxs-lookup"><span data-stu-id="bc1ec-163">Model builder</span></span>

<span data-ttu-id="bc1ec-164">문제: 오버 로드 된 함수의 표시 되지 않았습니다 FunctionImport로</span><span class="sxs-lookup"><span data-stu-id="bc1ec-164">Issue: Overloaded Functions could not be exposed as FunctionImport</span></span>

<span data-ttu-id="bc1ec-165">있는 경우 오버 로드 된 함수 2 고 FunctionImport System.InvalidOperationException ~/GetAllConventionCustomers(CustomerName={customerName}) 결과 요청 하는 다음 아래와 같이 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-165">If there are 2 overloaded functions and they are also FunctionImport as shown below then requesting ~/GetAllConventionCustomers(CustomerName={customerName}) results in System.InvalidOperationException.</span></span>

[!code-xml[Main](whats-new-in-aspnet-web-api-22/samples/sample3.xml)]

<span data-ttu-id="bc1ec-166">해결 방법:이 문제에 대 한 해결 FunctionImports로 모두 함수 오버 로드를 추가 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-166">Workaround: The workaround for this issue is to add both the function overloads as FunctionImports.</span></span>

#### <a name="odata-routing"></a><span data-ttu-id="bc1ec-167">OData 라우팅</span><span class="sxs-lookup"><span data-stu-id="bc1ec-167">OData Routing</span></span>

<span data-ttu-id="bc1ec-168">URL을 포함 하는 문자열 리터럴을 슬래시 (%2F) 인코딩되고 backslash(%5C) OData 리소스 경로에 사용 될 때 404 오류를 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-168">String literals that include the URL encoded slash (%2F), and backslash(%5C) cause a 404 error when they are used in the OData resource paths.</span></span>

<span data-ttu-id="bc1ec-169">예를 들어 함수의 매개 변수 또는 엔터티 집합의 키 값으로 OData 리소스 경로에 문자열 리터럴은 사용할 수 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-169">For example, string literals can be used in the OData resource paths as parameters of functions or key values of entity sets.</span></span>

<span data-ttu-id="bc1ec-170">/Employees/Total.GetCount(Name='Name%2F')</span><span class="sxs-lookup"><span data-stu-id="bc1ec-170">/Employees/Total.GetCount(Name='Name%2F')</span></span>

<span data-ttu-id="bc1ec-171">/Employees('Name%5C')</span><span class="sxs-lookup"><span data-stu-id="bc1ec-171">/Employees('Name%5C')</span></span>

<span data-ttu-id="bc1ec-172">서비스는 호스트는 이스케이프 해제 이러한 요청을 수신 하는 것에 웹 API 런타임에 전달 하기 전에 시퀀스 이스케이프 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-172">When services receive such requests the hosts will un-escape those escape sequences before passing them to the Web API runtime.</span></span> <span data-ttu-id="bc1ec-173">이 다음과 같은 공격 으로부터 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-173">This protects against attacks like the following:</span></span>  
  
`http://www.contoso.com/..%2F..%2F/Windows/System32/cmd.exe?/c+dir+c:`

<span data-ttu-id="bc1ec-174">그러면 Web API OData 스택이 404 (찾을 수 없음) 오류를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-174">This causes the Web API OData stack to return a 404 error (Not Found).</span></span> <span data-ttu-id="bc1ec-175">이 오류를 방지 하려면 클라이언트에는 슬래시 (%252F)에 대 한 이중 이스케이프 시퀀스와 백슬래시 (%255 C)를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-175">To prevent this error, your client should use the double escape sequences for slash (%252F) and backslash (%255C).</span></span> <span data-ttu-id="bc1ec-176">/Employees 같은 쿼리 문자열에 대 한이 문제가 발생 하지? $filter Name eq '이름 %2F' =</span><span class="sxs-lookup"><span data-stu-id="bc1ec-176">This does not happen for query strings such as /Employees?$filter=Name eq 'Name%2F'</span></span>

<span data-ttu-id="bc1ec-177">**언 이스케이프 된 슬래시 ('/')에 유의 하 고 백슬래시 (")는 OData 리소스 경로 문자열 리터럴에 사용할 수 없습니다. 슬래시 경로 구분 기호에만 표시 되어야 백슬래시 OData 리소스 경로에 전혀 표시 되지 않으며 (모두는 OData 쿼리 문자열의 특정 부분에서 사용할 수 있습니다.)**</span><span class="sxs-lookup"><span data-stu-id="bc1ec-177">**Note un-escaped slashes ('/') and backslashes ('') are not legal in OData resource path string literals. Slashes should appear only as path separators and backslashes should not appear in the OData resource path at all. (Both are usable in some portions of an OData query string.)**</span></span>

<span data-ttu-id="bc1ec-178">해결 방법: DefaultODataPathHandler 실제로 구문 분석 하기 전에 슬래시 및 문자열 리터럴에 백슬래시를 이스케이프 하의 Parse 메서드를 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-178">Workaround: You could override the Parse method of DefaultODataPathHandler to escape the slash and backslash in string literals before actually parsing them.</span></span> <span data-ttu-id="bc1ec-179">이 접근 방법의 예제를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-179">You can find a sample of this approach here.</span></span>

### <a name="odata-v3"></a><span data-ttu-id="bc1ec-180">OData v 3</span><span class="sxs-lookup"><span data-stu-id="bc1ec-180">OData v3</span></span>

#### <a name="queryable"></a><span data-ttu-id="bc1ec-181">[쿼리 가능]</span><span class="sxs-lookup"><span data-stu-id="bc1ec-181">[Queryable]</span></span>

<span data-ttu-id="bc1ec-182">[Queryable] 특성을 사용 하는 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-182">The [Queryable] attribute is deprecated.</span></span> <span data-ttu-id="bc1ec-183">새 OData v3 응용 프로그램 사용 해야 **System.Web.Http.OData.EnableQueryAttribute**합니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-183">New OData v3 applications should use **System.Web.Http.OData.EnableQueryAttribute**.</span></span>

<span data-ttu-id="bc1ec-184">**ODataHttpConfigurationExtensions.EnableQuerySupport** 확장 메서드는 이제 추가 **EnableQueryAttribute** 를 전역 필터 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-184">The **ODataHttpConfigurationExtensions.EnableQuerySupport** extension method now adds an **EnableQueryAttribute** to the global filter collection.</span></span> <span data-ttu-id="bc1ec-185">모든 컨트롤러에 포함 하는 경우는 **[Queryable]** 특성, 호출 `config.EnableQuerySupport()` 하면는 **[Queryable]** 실패 하는 특성</span><span class="sxs-lookup"><span data-stu-id="bc1ec-185">If any controllers have the **[Queryable]** attribute, calling `config.EnableQuerySupport()` will cause the **[Queryable]** attribute to fail</span></span>

<span data-ttu-id="bc1ec-186">이 문제를 해결 하는 권장된 방법의 모든 인스턴스는 **QueryableAttribute** 와 **System.Web.Http.OData.EnableQueryAttribute**합니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-186">The recommended way to resolve this issue is to replace all instances of **QueryableAttribute** with **System.Web.Http.OData.EnableQueryAttribute**.</span></span>

<span data-ttu-id="bc1ec-187">다른 해결 Web API 구성에서 다음 코드를 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-187">An alternative workaround is to use the following code in your Web API configuration:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-web-api-22/samples/sample4.cs)]

### <a name="attribute-routing"></a><span data-ttu-id="bc1ec-188">특성 라우팅</span><span class="sxs-lookup"><span data-stu-id="bc1ec-188">Attribute Routing</span></span>

<span data-ttu-id="bc1ec-189">문제: FromUri 특성으로 데코레이팅되 어는 복합 형식의 모델 바인딩 다르게 동작 특성 라우팅을 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-189">Issue: Model binding of complex type which is decorated with FromUri attribute behaves differently when using Attribute Routing.</span></span>

<span data-ttu-id="bc1ec-190">다음 링크 문제를 추적 하 고도 문제를 해결 하는 방법에 대 한 세부 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-190">Following link is tracking the issue and also has details about a workaround.</span></span>  
[http://aspnetwebstack.codeplex.com/workitem/1944](http://aspnetwebstack.codeplex.com/workitem/1944)

<span data-ttu-id="bc1ec-191">문제: 스 캐 폴딩 MVC/웹 API 5.2.0 사용 하 여 프로젝트에 패키지 결과 5.1.2에서 프로젝트에 이미 존재 하지 않는 것에 대 한 패키지</span><span class="sxs-lookup"><span data-stu-id="bc1ec-191">Issue: Scaffolding MVC/Web API into a project with 5.2.0 packages results in 5.1.2 packages for ones that don't already exist in the project</span></span>

<span data-ttu-id="bc1ec-192">ASP.NET MVC 5.2에 대 한 NuGet 패키지를 업데이트 해도 ASP.NET 스 캐 폴딩 같은 Visual Studio 도구 또는 ASP.NET 웹 응용 프로그램 프로젝트 템플릿을 업데이트 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-192">Updating NuGet packages for ASP.NET MVC 5.2 does not update the Visual Studio tools such as ASP.NET scaffolding or the ASP.NET Web Application project template.</span></span> <span data-ttu-id="bc1ec-193">이전 버전의 ASP.NET 런타임 패키지 (예:: Update 2에서 5.1.2) 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-193">They use the previous version of the ASP.NET runtime packages (e.g. 5.1.2 in Update 2).</span></span> <span data-ttu-id="bc1ec-194">결과적으로, ASP.NET 스 캐 폴딩은 이미 프로젝트에서 사용할 수 없는 경우에 필요한 패키지의 이전 버전 (예:: Update 2에서 5.1.2)으로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-194">As a result, the ASP.NET scaffolding will install the previous version (e.g. 5.1.2 in Update 2) of the required packages, if they are not already available in your projects.</span></span> <span data-ttu-id="bc1ec-195">그러나 Visual Studio 2013 RTM 또는 업데이트 1에서 ASP.NET 스 캐 폴딩을 프로젝트에서 최신 패키지를 덮어쓰지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-195">However, the ASP.NET scaffolding in Visual Studio 2013 RTM or Update 1 does not overwrite the latest packages in your projects.</span></span> <span data-ttu-id="bc1ec-196">ASP.NET 웹 API 2.2 또는 ASP.NET MVC 5.2로 프로젝트의 패키지를 업데이트 한 후에 스 캐 폴딩을 사용 하는 경우에 버전의 웹 API 및 ASP.NET MVC 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-196">If you use ASP.NET scaffolding after updating the packages of your projects to Web API 2.2 or ASP.NET MVC 5.2, make sure the versions of Web API and ASP.NET MVC are consistent.</span></span>

<a id="bug-fixes"></a>
## <a name="bug-fixes-and-minor-feature-updates"></a><span data-ttu-id="bc1ec-197">버그 수정 및 사소한 기능 업데이트</span><span class="sxs-lookup"><span data-stu-id="bc1ec-197">Bug Fixes and Minor Feature Updates</span></span>

<span data-ttu-id="bc1ec-198">이 릴리스에 여러 가지 버그 수정 및 사소한 기능에도 기능이 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-198">This release also includes several bug fixes and minor feature updates.</span></span> <span data-ttu-id="bc1ec-199">전체 목록은 여기를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-199">You can find the complete list here:</span></span>

- [<span data-ttu-id="bc1ec-200">5.2 패키지</span><span class="sxs-lookup"><span data-stu-id="bc1ec-200">5.2 package</span></span>](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=v5.2%20RC|v5.2%20RTM&assignedTo=All&component=Web%20API|Web%20API%20OData&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="odata521"></a>
## <a name="microsoftaspnetodata-521"></a><span data-ttu-id="bc1ec-201">Microsoft.AspNet.OData 5.2.1</span><span class="sxs-lookup"><span data-stu-id="bc1ec-201">Microsoft.AspNet.OData 5.2.1</span></span>

<span data-ttu-id="bc1ec-202">Microsoft.AspNet.OData 5.2.1 패키지 없는 버그 수정 하지만 NuGet 종속성 업데이트를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-202">The Microsoft.AspNet.OData 5.2.1 package contains NuGet dependency updates but no bug fixes.</span></span> <span data-ttu-id="bc1ec-203">이 업데이트를 더 이상 엄격한 종속성에 Microsoft.OData.Core 6.4.0, 있지만 하나 6.4.0 사이의 7.0.0까지 차단 버전으로 업그레이드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-203">With this update, there is no longer a strict dependency on Microsoft.OData.Core 6.4.0, but one can upgrade to any version between 6.4.0 and 7.0.0.</span></span>

<a id="522RC"></a>
## <a name="microsoftaspnetwebapi-522"></a><span data-ttu-id="bc1ec-204">5.2.2 Microsoft.AspNet.WebAPI</span><span class="sxs-lookup"><span data-stu-id="bc1ec-204">Microsoft.AspNet.WebAPI 5.2.2</span></span>

<span data-ttu-id="bc1ec-205">이 릴리스에서 종속성에 대 한 변경 기능이 되었습니다 `Json.Net 6.0.4`합니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-205">In this release we have made a dependency change for `Json.Net 6.0.4`.</span></span> <span data-ttu-id="bc1ec-206">이 버전의 새로운 기능에 대 한 자세한 내용은 `Json.NET`, 참조 [Json.NET 6.0 릴리스 4-JSON 병합 종속성 주입](http://james.newtonking.com/archive/2014/08/04/json-net-6-0-release-4-json-merge-dependency-injection)합니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-206">For more information on what is new in this release of `Json.NET`, see [Json.NET 6.0 Release 4 - JSON Merge, Dependency Injection](http://james.newtonking.com/archive/2014/08/04/json-net-6-0-release-4-json-merge-dependency-injection).</span></span> <span data-ttu-id="bc1ec-207">이 릴리스에서 웹 API의 새로운 기능 또는 버그 수정 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-207">This release doesn't have any other new features or bug fixes in Web API.</span></span> <span data-ttu-id="bc1ec-208">이후에이 새 버전의 웹 API에 따라 달라 지도록 소유 म 다른 모든 종속 패키지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-208">We have subsequently updated all other dependent packages we own to depend on this new version of Web API.</span></span>

<a id="523"></a>
## <a name="microsoftaspnetwebapi-523-beta"></a><span data-ttu-id="bc1ec-209">5.2.3 Microsoft.AspNet.WebAPI 베타</span><span class="sxs-lookup"><span data-stu-id="bc1ec-209">Microsoft.AspNet.WebAPI 5.2.3 Beta</span></span>

<span data-ttu-id="bc1ec-210">릴리스에 대 한 읽을 수 [여기](https://blogs.msdn.com/b/webdev/archive/2014/12/17/asp-net-mvc-5-2-3-web-pages-5-2-3-and-web-api-5-2-3-beta-releases.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-210">You can read about the release [here](https://blogs.msdn.com/b/webdev/archive/2014/12/17/asp-net-mvc-5-2-3-web-pages-5-2-3-and-web-api-5-2-3-beta-releases.aspx).</span></span> <span data-ttu-id="bc1ec-211">이 릴리스에 버그 수정만 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-211">This release contains only bug fixes.</span></span> <span data-ttu-id="bc1ec-212">사용할 수 있습니다 [이 쿼리](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=Closed&amp;type=All&amp;priority=All&amp;release=v5.2.3%20Beta&amp;assignedTo=All&amp;component=Web%20API&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0&amp;reasonClosed=Fixed) 이 릴리스에서 수정 된 문제 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc1ec-212">You can use [this query](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=Closed&amp;type=All&amp;priority=All&amp;release=v5.2.3%20Beta&amp;assignedTo=All&amp;component=Web%20API&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0&amp;reasonClosed=Fixed) to see the list of issues fixed in this release.</span></span>
