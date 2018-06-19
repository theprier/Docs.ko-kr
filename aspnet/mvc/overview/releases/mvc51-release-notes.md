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
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/releases/mvc51-release-notes
msc.type: authoredcontent
ms.openlocfilehash: be10486c9fd39738f44cdda4fedb409058017601
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/10/2018
ms.locfileid: "26504052"
---
<a name="whats-new-in-aspnet-mvc-51"></a>ASP.NET MVC 5.1의에서 새로운 기능
====================
by [Microsoft](https://github.com/microsoft)

이 항목에서는 ASP.NET 웹 MVC 5.1에 대 한 새로운 기능을 설명 합니다.

- [소프트웨어 요구 사항](#SoftwareRequirements)
- [다운로드](#download)
- [문서](#documentation)
- [ASP.NET MVC 5.1의에서 새로운 기능](#new-features)

    - [라우팅 향상 된 기능 특성](#AttributeRouting)
    - [부트스트랩 편집기 템플릿 지원](#Bootstrap)
    - [뷰에서 열거형 지원](#Enum)
    - [MinLength/MaxLength 특성에 대 한 비 가시적인 유효성 검사](#Unobtrusive)
    - [비 가시적인 Ajax에서 'this'이 컨텍스트를 지 원하는](#thisContext)
- [알려진 문제 및 주요 변경 내용](#KnownBreakingChanges)- [버그 수정](#bug-fixes)

<a id="SoftwareRequirements"></a>
## <a name="software-requirements"></a>소프트웨어 요구 사항

- Visual Studio 2012: 다운로드 [ASP.NET 및 웹 도구 Visual Studio 2012 용 2013.1](https://go.microsoft.com/fwlink/?LinkId=390062)합니다.
- Visual Studio 2013의 경우: 다운로드 [Visual Studio 2013 업데이트 1](https://go.microsoft.com/fwlink/?LinkId=390064)합니다. ASP.NET MVC 5.1 Razor 뷰를 편집 하기 위해이 업데이트가 필요 합니다.

<a id="download"></a>
## <a name="download"></a>다운로드

런타임 기능은 NuGet 갤러리에서 NuGet 패키지로 해제 됩니다. 모든 런타임 패키지에 따라는 [의미 체계 버전 관리](http://semver.org/) 사양입니다. ASP.NET MVC 5.1 RTM 최신 패키지에는 다음 버전: "5.1.2"입니다. 설치 또는 업데이트를 통해 이러한 패키지 [NuGet](http://www.nuget.org/packages/Microsoft.AspNet.Mvc/)합니다. 릴리스에 NuGet에 해당 지역화 된 패키지도 포함 됩니다.

설치 하거나 NuGet 패키지 관리자 콘솔을 사용 하 여 출시 된 NuGet 패키지를 업데이트할 수 있습니다.

[!code-console[Main](mvc51-release-notes/samples/sample1.cmd)]

<a id="documentation"></a>
## <a name="documentation"></a>설명서

ASP.NET 웹 사이트에서 사용할 수 있는 자습서 및 ASP.NET MVC 5.1 RTM에 대 한 기타 정보 ( https://www.asp.net)합니다. 

<a id="new-features"></a>
## <a name="new-features-in-aspnet-mvc-51"></a>ASP.NET MVC 5.1의에서 새로운 기능

<a id="AttributeRouting"></a>

### <a name="attribute-routing-improvements"></a>라우팅 향상 된 기능 특성

 라우팅 지원 제약 조건, 버전 관리 및 헤더를 사용 하면 이제 특성 기반 경로 선택 합니다. 특성 경로 많은 측면을 통해 사용자 지정 가능한 이제는 `IDirectRouteFactory` 인터페이스 및 `RouteFactoryAttribute` 클래스입니다. 경로 접두사를 통해 확장 가능한는 이제는 `IRoutePrefix` 인터페이스 및 `RoutePrefixAttribute` 클래스입니다. 

<a id="Enum"></a>

### <a name="enum-support-in-views"></a>뷰에서 열거형 지원

1. 새 `@Html.EnumDropDownListFor()` 도우미 메서드. 대부분의 식을 계산 되어야 하는 다 경고와 함께 HTML 도우미와 같이 사용할 수 해야 이러한는 [enum](https://msdn.microsoft.com/en-us/library/cc138362.aspx) 형식 또는 [Nullable&lt;T&gt; ](https://msdn.microsoft.com/en-us/library/2cf62fcy.aspx) 여기서 `T` 는 는[enum](https://msdn.microsoft.com/en-us/library/cc138362.aspx) 유형입니다. 사용 하 여 `EnumHelper.IsValidForEnumHelper()` 이러한 요구 사항을 확인 하려면.
2. 새 `EnumHelper.GetSelectList()` 반환 하는 메서드는 `IList<SelectListItem>`합니다. 예를 들어을 호출 하기 전에 선택 목록 조작 해야 하는 경우에 유용 `@Html.DropDownListFor()`, 이름을 표시 하려면 또는 `@Html.EnumDropDownListFor()` 보여 줍니다.

다음 코드에서는 이러한 Api를 보여 줍니다.

[!code-cshtml[Main](mvc51-release-notes/samples/sample2.cshtml)]

전체 예제를 볼 수 있습니다 [여기](https://aspnet.codeplex.com/SourceControl/latest#Samples/MVC/EnumSample/)합니다.

<a id="Bootstrap"></a>

### <a name="bootstrap-support-for-editor-templates"></a>부트스트랩 편집기 템플릿 지원

HTML 특성에서 전달 이제 허용 [EditorFor](https://msdn.microsoft.com/en-us/library/system.web.mvc.html.editorextensions.editorfor(v=vs.100).aspx) 로 [익명 개체](https://msdn.microsoft.com/en-us/library/bb397696.aspx)합니다.

예를 들어:

[!code-cshtml[Main](mvc51-release-notes/samples/sample3.cshtml)]

<a id="Unobtrusive"></a>

### <a name="unobtrusive-validation-for-minlengthattribute-and-maxlengthattribute"></a>MinLengthAttribute 및 MaxLengthAttribute 비간섭 유효성 검사

로 데코레이팅 되었습니다 속성에 대 한 문자열 및 배열 형식에 대 한 클라이언트 쪽 유효성 검사는 지원 이제는 [MinLength](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.minlengthattribute(v=vs.110).aspx) 및 [MaxLength](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.maxlengthattribute(v=vs.110).aspx) 특성입니다.

<a id="thisContext"></a>

### <a name="supporting-the-this-context-in-unobtrusive-ajax"></a>비 가시적인 Ajax에서 'this'이 컨텍스트를 지 원하는

콜백 함수 (`OnBegin, OnComplete, OnFailure, OnSuccess`)를 통해 호출 요소를 찾을 수 이제 됩니다는 `this` 컨텍스트. 예를 들어:

[!code-html[Main](mvc51-release-notes/samples/sample4.html)]

<a id="KnownBreakingChanges"></a>

## <a name="known-issues-and-breaking-changes"></a>알려진된 문제 및 주요 변경 내용

### <a name="attribute-routing"></a>특성 라우팅

특성에서 일치 하는 라우팅 항목에 모호성이 첫 번째 일치 항목을 선택 하는 대신 오류가 보고 이제 합니다.

특성 경로 사용 하 여에서 금지 됩니다는 `{controller}` 매개 변수를 사용 하 여 간에 `{action}` 경로에 매개 변수가 작업에 배치 합니다. 이러한 매개 변수를 사용 하 여 모호성을 초래할 가능성이 매우 합니다. 

### <a name="scaffolding-mvcweb-api-into-a-project-with-51-packages-results-in-50-packages-for-ones-that-dont-already-exist-in-the-project"></a>5.1 패키지 결과 프로젝트에 이미 존재 하지 않는 것에 대 한 5.0 패키지를 사용 하는 프로젝트에 스 캐 폴딩 MVC/웹 API

ASP.NET MVC 5.1 RTM에 대 한 NuGet 패키지를 업데이트 해도 ASP.NET 스 캐 폴딩 같은 Visual Studio 도구 또는 ASP.NET 웹 응용 프로그램 프로젝트 템플릿을 업데이트 되지 않습니다. 이전 버전의 ASP.NET 런타임 패키지 (5.0.0.0) 사용합니다. 결과적으로, ASP.NET 스 캐 폴딩은 이미 프로젝트에서 사용할 수 없는 경우에 필요한 패키지의 이전 버전 (5.0.0.0)으로 설치 됩니다. 그러나 Visual Studio 2013 RTM 또는 업데이트 1에서 ASP.NET 스 캐 폴딩을 프로젝트에서 최신 패키지를 덮어쓰지 않습니다. ASP.NET 웹 API 2.1 또는 ASP.NET MVC 5.1에 프로젝트의 패키지를 업데이트 한 후에 스 캐 폴딩을 사용 하는 경우에 버전의 웹 API 및 ASP.NET MVC 일치 하는지 확인 합니다. 

### <a name="syntax-highlighting-for-razor-views-in-visual-studio-2013"></a>Visual Studio 2013에서 Razor 뷰의 구문 강조 표시

Visual Studio 2013 업데이트 하지 않고 ASP.NET MVC 5.1 RTM으로 업데이트 하는 경우에 하지 Razor 뷰를 편집 하는 동안 구문 강조 표시에 대 한 Visual Studio 편집기 지원을 받을 수 있습니다. 이 지원을 받기 위해 Visual Studio 2013 업데이트 해야 합니다. 

### <a name="type-renames"></a>형식 이름 바꾸기

라우팅 확장 특성에 사용 되는 형식 중 일부는 5.1 RTM의 이름이 변경 됩니다.

| **이전 형식 이름 (5.1 RC)** | **새 형식 이름을 (5.1 RTM)** |
| --- | --- |
| IDirectRouteProvider | IDirectRouteFactory |
| RouteProviderAttribute | RouteFactoryAttribute |
| DirectRouteProviderContext | DirectRouteFactoryContext |

<a id="bug-fixes"></a>
## <a name="bug-fixes"></a>버그 수정

이 버전에는 다양 한 버그 수정 사항이 포함 되어 있습니다. 전체 목록은 여기를 찾을 수 있습니다.

- [5.1.0 패키지](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=Closed&amp;type=All&amp;priority=All&amp;release=v5.1%20Preview|v5.1%20RTM&amp;assignedTo=All&amp;component=MVC&amp;sortField=AssignedTo&amp;sortDirection=Ascending&amp;page=0&amp;reasonClosed=Fixed)
- [5.1.1 패키지](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=v5.1.1%20RTM&amp;assignedTo=All&amp;component=MVC&amp;sortField=AssignedTo&amp;sortDirection=Ascending&amp;page=0&amp;reasonClosed=Fixed)

5.1.2 없는 버그 수정 하지만 IntelliSense 업데이트 패키지에 포함 되어 있습니다.
