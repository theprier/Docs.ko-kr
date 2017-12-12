---
uid: whitepapers/what-is-new-in-aspnet-mvc
title: "ASP.NET MVC 2의에서 새로운 기능 | Microsoft Docs"
author: rick-anderson
description: "이 문서에서는 새로운 기능과 향상 된 ASP.NET MVC 2에서 도입 된에 대해 설명 합니다. 이 문서를 다운로드할 수 이기도합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/20/2010
ms.topic: article
ms.assetid: 69a8d6f8-4b10-4602-8822-2d6c05fc432b
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /whitepapers/what-is-new-in-aspnet-mvc
msc.type: content
ms.openlocfilehash: e7f92dd7a09d1986ad775203effcbce76fb0e6f4
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="whats-new-in-aspnet-mvc-2"></a>ASP.NET MVC 2의에서 새로운 기능
====================
> 이 문서에서는 새로운 기능과 향상 된 ASP.NET MVC 2에서 도입 된에 대해 설명 합니다. 이 문서는 가능 [다운로드](https://download.microsoft.com/download/F/1/6/F16F9AF9-8EF4-4845-BC97-639791D5699C/WhatIsNewInMVC_2.pdf)


[소개](#_TOC1)   
[1.0 ASP.NET MVC 프로젝트를 ASP.NET MVC 2로 업그레이드](#_TOC2)   
[새로운 기능](#_TOC3)   
[템플릿 기반 도우미](#_TOC3_1)   
[영역](#_TOC3_2)   
[비동기 컨트롤러에 대 한 지원](#_TOC3_3)   
[동작 메서드 매개 변수에서 DefaultValueAttribute에 대 한 지원](#_TOC3_4)   
[모델 바인더를 사용 하 여 이진 데이터 바인딩에 대 한 지원](#_TOC3_5)   
[ModelMetadata 및 ModelMetadataProvider 클래스](#_TOC3_6)   
[DataAnnotations 특성에 대 한 지원](#_TOC3_7)   
[모델 유효성 검사기 공급자](#_TOC3_8)   
[클라이언트 쪽 유효성 검사](#_TOC3_9)   
[Visual Studio 2010에 대 한 새 코드 조각](#_TOC3_10)   
[새 RequireHttpsAttribute 작업 필터](#_TOC3_11)   
[HTTP 메서드 동사를 재정의합니다.](#_TOC3_12)   
[템플릿 기반 도우미에 대 한 새 HiddenInputAttribute 클래스](#_TOC3_13)   
[Html.ValidationSummary 도우미 메서드는 모델 수준 오류를 표시할 수 있습니다.](#_TOC3_14)   
[T4 템플릿을 Visual Studio 생성 된 코드에서 특정.NET Framework의 대상 버전으로](#_TOC3_15)[API 개선 사항](#_TOC4)  
[주요 변경 내용](#_TOC5)  
[고 지 사항](#_TOC6)  

## <a id="_TOC1"></a>소개

ASP.NET MVC 2 ASP.NET MVC 1.0을 바탕으로 하며 다양 한 생산성 증가에 포커스를 설정 하는 기능과 향상 된 기능을 소개 합니다. 적용할 계속 해 서 모든 기술 자료, 기술, 코드 및 ASP.NET MVC 1.0에 대 한 확장이이 릴리스는 ASP.NET MVC 1.0과 호환 됩니다.

ASP.NET MVC에 대 한 자세한 내용은 다음 리소스를 참조 합니다.

- [MSDN에서 ASP.NET MVC 설명서](https://go.microsoft.com/fwlink/?LinkId=159758)
- [ASP.NET MVC 웹 사이트](https://asp.net/mvc/)
- [ASP.NET MVC 포럼](https://forums.asp.net/1146.aspx)

## <a id="_TOC2"></a>1.0 ASP.NET MVC 프로젝트를 ASP.NET MVC 2로 업그레이드

ASP.NET MVC 2 ASP.NET MVC 1.0 응용 프로그램을 ASP.NET MVC 2로 업그레이드 하는 시기 선택에 응용 프로그램 개발자가 유연성을 제공 하는 동일한 서버에 ASP.NET MVC 1.0 나란히 설치할 수 있습니다. 업그레이드 하는 방법에 대 한 내용은 문서를 참조 하십시오. [ASP.NET 1.0 응용 프로그램을 ASP.NET MVC 2로 업그레이드](https://go.microsoft.com/fwlink/?LinkID=185459)합니다.

## <a id="_TOC3"></a>새로운 기능

이 섹션에 도입 된 기능에 설명 MVC 2 릴리스에서 합니다.

### <a id="_TOC3_1"></a>템플릿 기반 도우미

템플릿 기반 도우미 사용 하 여 편집에 대 한 HTML 요소를 자동으로 연결 및 데이터 형식으로 표시 합니다. 예를 들어 System.DateTime 형식의 데이터 보기에 표시 되 면 날짜 선택 UI 요소를 자동으로 렌더링할 수 있습니다. 필드 템플릿을 ASP.NET Dynamic Data에서 어떻게 작동 하는 것과 비슷합니다. 자세한 내용은 참조 [데이터 표시를 사용 하 여 템플릿 기반 도우미](https://go.microsoft.com/fwlink/?LinkId=159062) MSDN 웹 사이트에 있습니다.

### <a id="_TOC3_2"></a>영역

영역 사용 하면 대형 웹 응용 프로그램의 복잡성을 관리 하기 위해 여러 개의 작은 섹션으로 큰 프로젝트를 구성할 수 있습니다. 각 섹션 ("영역")는 일반적으로 큰 웹 사이트의 개별 섹션을 나타냅니다 및 컨트롤러와 뷰의 관련된 집합을 그룹화 하는 데 사용 됩니다. 자세한 내용은 참조 [연습: 영역에서 ASP.NET MVC 응용 프로그램 구성](https://go.microsoft.com/fwlink/?LinkId=158978) MSDN 웹 사이트에 있습니다.

솔루션 탐색기에서 새 영역을 만들려면 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 추가 클릭 한 다음 영역을 클릭 합니다. 영역 이름에 대 한 묻는 대화 상자가 나타납니다. 영역 이름을 입력 한 후 Visual Studio 프로젝트에 새 영역을 추가 합니다.

다음 그림은 두 개의 영역, 관리 및 블로그를 사용 하 여 프로젝트에 대 한 레이아웃 예입니다.

![](what-is-new-in-aspnet-mvc/_static/image1.png)

영역을 만들 때 Visual Studio는 각 영역에 AreaRegistration에서 파생 되는 클래스를 추가 합니다. 다음 예제와 같이이 클래스 및 해당 경로 영역을 등록 하기 위해 필요 합니다.

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample1.cs)]

ASP.NET MVC 2에 대 한 기본 프로젝트 템플릿은 Global.asax 파일에 대 한 코드에서는 RegisterAllAreas 메서드 호출을 포함합니다. 이 메서드는 AreaRegistration 클래스에서 파생 되는 모든 형식에 대 한 조회를 형식의 인스턴스를 인스턴스화하고 다음 인스턴스에서 RegisterArea 메서드를 호출 하 여 프로젝트의 각 영역을 등록 합니다. 다음 예제에서는 이것은 수행 하는 방법을 보여 줍니다.

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample2.cs)]

지정 하지 않으면 네임 스페이스 RegisterArea 메서드에서 컨텍스트 호출 하 여 하는 경우. Namespaces.Add 메서드, 등록 클래스의 네임 스페이스는 기본적으로 사용 됩니다.

### <a id="_TOC3_3"></a>비동기 컨트롤러에 대 한 지원

이제 ASP.NET MVC 2에는 요청을 비동기적으로 처리 하는 컨트롤러 수 있습니다. 이 자주 함수와 비 블록 킹를 대신 호출을 차단 작업 (예: 네트워크 요청 수)를 호출 하는 서버를 허용 하 여 성능이 향상 될 수 있습니다. 자세한 내용은 참조는 [ASP.NET MVC에서 비동기 컨트롤러를 사용 하 여](https://msdn.microsoft.com/en-us/library/ee728598(v=VS.100).aspx) MSDN 항목.

### <a id="_TOC3_4"></a>동작 메서드 매개 변수에서 DefaultValueAttribute에 대 한 지원

System.ComponentModel.DefaultValueAttribute 클래스에서 인수 매개 변수에 동작 메서드에 대해 제공 해야 하는 기본값을 수 있습니다. 예를 들어 다음과 같은 기본 경로가 정의 되어 있다고 가정 합니다.

[!code-json[Main](what-is-new-in-aspnet-mvc/samples/sample3.json)]

또한 다음 컨트롤러 및 작업 메서드가 정의 되어 있다고 가정 합니다.

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample4.cs)]

다음 요청 중 Url는 호출 앞의 예제에 정의 된 보기 동작 메서드가 합니다.

- / 문서/뷰/123
- / 문서/뷰/123? 페이지 = 1 (효과적으로 동일 이전 요청)
- / 문서/뷰/123? 페이지 = 2

DefaultValueAttribute 특성이 없으면 위의 목록에서 첫 번째 URL 작동 하지 않습니다, 페이지 인수는 null이 아닌 값 형식 값을 지정 하지 않았습니다.

선택적 매개 변수는 다음 예제와 같이 코드를 Visual Basic 2010 또는 Visual C# 2010에서 작성 한 경우 DefaultValueAttribute 특성 대신 사용할 수 있습니다.

[!code-vb[Main](what-is-new-in-aspnet-mvc/samples/sample5.vb)]

### <a id="_TOC3_5"></a>모델 바인더를 사용 하 여 이진 데이터 바인딩에 대 한 지원

두 개의 새 오버 로드 Html.Hidden 도우미의 이진 값을 base 64 인코딩 문자열로 인코딩할 가지가 있습니다.

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample6.cs)]

일반적인 사용 뷰에서 개체에 대 한 타임 스탬프를 포함 하는 것입니다. 예를 들어 응용 프로그램에 다음과 같은 제품 개체를 포함 될 수 있습니다.

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample7.cs)]

편집 폼 예제에 나와 있는 것 처럼 폼의 타임 스탬프 속성을 렌더링할 수 있습니다.

[!code-aspx[Main](what-is-new-in-aspnet-mvc/samples/sample8.aspx)]

이 태그는 다음 예제와 유사 하는 base 64 인코딩 문자열로 타임 스탬프 값으로는 숨겨진된 input 요소를 렌더링 합니다.

[!code-html[Main](what-is-new-in-aspnet-mvc/samples/sample9.html)]

다음 예제와 같이이 양식은 제품 형식의 인수에는 동작 메서드에 게시 될 수 있습니다.

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample10.cs)]

작업 메서드에서 타임 스탬프 속성이 게시 된 base 64 인코딩 문자열을 바이트 배열로 변환 되기 때문에 올바르게 채워집니다.

### <a id="_TOC3_6"></a>ModelMetadata 및 ModelMetadataProvider 클래스

ModelMetadataProvider 클래스 뷰 내에서 모델에 대 한 메타 데이터를 가져오기 위한 추상화를 제공 합니다. MVC 2 System.ComponentModel.DataAnnotations 네임 스페이스의 특성에 의해 노출 되는 메타 데이터를 사용할 수 있도록 하는 기본 공급자가 포함 되어 있습니다. 데이터베이스 또는 XML 파일 등의 다른 데이터 저장소에서 메타 데이터를 제공 하는 메타 데이터 공급자를 만드는 것 같습니다.

ViewDataDictionary 클래스 ModelMetadataProvider 클래스에 의해 모델에서 추출 된 메타 데이터를 포함 한 ModelMetadata 개체를 노출 합니다. 따라서이 메타 데이터를 사용 하 고 해당 출력을 적절 하 게 조정 하는 템플릿 기반 도우미 수 있습니다.

자세한 내용은 참조에 대 한 설명서는 [ModelMetadata](https://msdn.microsoft.com/en-us/library/system.web.mvc.modelmetadataprovider(VS.100).aspx) 및 [ModelMetadataProvider](https://msdn.microsoft.com/en-us/library/system.web.mvc.modelmetadataprovider(VS.100).aspx) 클래스입니다.

### <a id="_TOC3_7"></a>DataAnnotations 특성에 대 한 지원

ASP.NET MVC 2 지원 (System.ComponentModel.DataAnnotations 네임 스페이스에 정의 됨) RangeAttribute, RequiredAttribute, StringLengthAttribute, 및 RegexAttribute 유효성 검사 특성을 사용 하 여 모델에 입력을 제공 하기 위해 바인딩할 때 유효성 검사 합니다.

자세한 내용은 참조 [하는 방법: 모델 데이터 DataAnnotations를 사용 하 여 특성의 유효성을 검사](https://go.microsoft.com/fwlink/?LinkId=159063) MSDN 웹 사이트에 있습니다. 이러한 특성의 사용을 보여 주는 샘플 프로젝트에서 다운로드할 수는 [https://go.microsoft.com/fwlink/?LinkId=157753](https://go.microsoft.com/fwlink/?LinkId=157753)합니다.

### <a id="_TOC3_8"></a>모델 유효성 검사기 공급자

모델 유효성 검사 공급자 클래스는 모델에 대 한 유효성 검사 논리를 제공 하는 추상화를 나타냅니다. ASP.NET MVC System.ComponentModel.DataAnnotations 네임 스페이스에 포함 된 유효성 검사 특성을 기반으로 기본 공급자가 포함 되어 있습니다. 모델에 사용자 지정 유효성 검사 규칙 및 유효성 검사 규칙의 사용자 지정 매핑을 정의 하는 고유한 유효성 검사 공급자를 만들 수 있습니다. 자세한 내용은 참조에 대 한 설명서는 [ModelValidatorProvider](https://msdn.microsoft.com/en-us/library/system.web.mvc.ModelValidatorProvider(VS.100).aspx) 클래스입니다.

### <a id="_TOC3_9"></a>클라이언트 쪽 유효성 검사

모델 유효성 검사기 공급자 클래스는 클라이언트 쪽 유효성 검사 라이브러리에서 사용할 수 있는 JSON 직렬화 된 데이터의 형태로 브라우저에 유효성 검사 메타 데이터를 노출 합니다. ASP.NET MVC 2 클라이언트 유효성 검사 라이브러리와 앞에서 기록한 DataAnnotations 네임 스페이스 유효성 검사 특성을 지 원하는 어댑터를 포함 합니다. 공급자 클래스를 사용 하면 대체 라이브러리에 대 한 호출이 고 JSON 데이터를 처리 하는 어댑터를 작성 하 여 다른 클라이언트 유효성 검사 라이브러리를 사용할 수 있습니다.

### <a id="_TOC3_10"></a>Visual Studio 2010에 대 한 새 코드 조각

ASP.NET MVC 2에 대 한 HTML 코드 조각 집합이 Visual Studio 2010과 함께 설치 됩니다. 이러한 조각 도구 메뉴에서 보려는 코드 조각 관리자를 선택 합니다. 언어에 대 한 HTML을 선택한 위치에 대 한 ASP.NET MVC 2를 선택 합니다. 코드 조각을 사용 하는 방법에 대 한 자세한 내용은 Visual Studio 설명서를 참조 하십시오.

### <a id="_TOC3_11"></a>새 RequireHttpsAttribute 작업 필터

ASP.NET MVC 2 작업 메서드 및 컨트롤러에 적용할 수 있는 새 RequireHttpsAttribute 클래스를 포함 합니다. 기본적으로 필터를 ssl (HTTPS)에 해당 하는 비 SSL HTTP 요청을 리디렉션합니다.

### <a id="_TOC3_12"></a>HTTP 메서드 동사를 재정의합니다.

REST 아키텍처 스타일을 사용 하 여 웹 사이트를 빌드할 때 HTTP 동사도 리소스에 대해 수행할 작업을 결정 하는 데 사용 됩니다. REST를 사용 하려면 GET, PUT, POST 및 삭제 된 모든 범위의 일반 HTTP 동사를 포함 하 여 해당 응용 프로그램 지원을 해야 합니다.

ASP.NET MVC 2 작업 메서드 및 해당 기능 compact 구문에 적용할 수 있는 새 특성을 포함 합니다. 이러한 특성을 ASP.NET MVC HTTP 동사에 따라 동작 메서드의 선택 하려면 사용 합니다. 다음 예제에서는 POST 요청에서는 첫 번째 작업 메서드를 호출 하는 및 PUT 요청에서 두 번째 동작 메서드를 호출 합니다.

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample11.cs)]

이전 버전의 ASP.NET MVC에서는 이러한 작업 메서드는 다음 예제와 같이 더 자세한 구문이 필요 합니다.

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample12.cs)]

브라우저 GET 및 HTTP POST 동사를 지원 하므로 다른 동사 필요한 작업을 게시 하는 것이 불가능 합니다. 따라서 기본적으로 모든 RESTful 요청을 지원 하도록 수 없으면입니다.

그러나 ASP.NET MVC 2 POST 작업 하는 동안 요청 RESTful를 지원 하기 위해 새 HttpMethodOverride HTML 도우미 메서드를 소개 합니다. 이 메서드는 해당 폼을 효과적으로 모든 HTTP 메서드를 에뮬레이트하는 숨겨진된 input 요소를 렌더링 합니다. 예를 들어 HttpMethodOverride HTML 도우미 메서드를 사용 하 여 사용할 수 있습니다 표시 양식을 제출 하 여 PUT 또는 DELETE 요청을 수 있습니다. HttpMethodOverride의 동작에는 다음과 같은 특성이 달라 집니다.

- HttpPostAttribute
- HttpPutAttribute
- HttpGetAttribute
- HttpDeleteAttribute
- AcceptVerbsAttribute

숨겨진된 input 요소는 HTTP 메서드 재정의 X 이름 및 값이 HTTP 동사를 에뮬레이션 하기 위해 설정에 있습니다. 재정의 값도 지정할 수 있습니다 HTTP 헤더 또는 쿼리 문자열 값을 이름/값 쌍으로.

재정의 실제 요청은 POST 요청 하는 경우에 사용할 수 있습니다. 다른 HTTP 동사를 사용 하는 요청에 대 한 재정의 값이 무시 됩니다.

### <a id="_TOC3_13"></a>템플릿 기반 도우미에 대 한 새 HiddenInputAttribute 클래스

새 HiddenInputAttribute 특성 편집기 서식 파일에서 모델을 표시할 때는 숨겨진된 input 요소를 렌더링 해야 하는지 여부를 나타내기 위해 모델 속성에 적용할 수 있습니다. (특성 설정 HiddenInput 암시적 UIHint 값). 특성의 DisplayValue 속성을 사용 하면 값 편집기에 표시 되는지 여부를 지정 하 고 디스플레이 모드를 수행할 수 있습니다. DisplayValue false로 설정 되 면 아무 것도 표시, 일반적으로 필드를 둘러싸고 있는 HTML 태그에도 없습니다. DisplayValue에 대 한 기본값은 true입니다.

다음과 같은 시나리오에서 HiddenInputAttribute 특성을 사용할 수 있습니다.

- 뷰 개체의 ID를 편집 하는 사용자가 수 있습니다. 컨트롤러에 다시 전달 될 수 있도록 이전 ID를 포함 하는 숨겨진된 input 요소를 제공 하는 것도 값을 표시 해야 하는 시점과 합니다.
- 뷰일 수 있습니다 때 사용자가 이진 속성 되지 표시할지, 예: 타임 스탬프 속성을 편집 합니다. 이 경우 값과 주변 HTML 태그입니다 (예: 레이블 및 값) 표시 되지 않습니다.

다음 예제에서는 HiddenInputAttribute 클래스를 사용 하는 방법을 보여 줍니다.

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample13.cs)]

특성이 설정 되 면 true로 (또는 지정 된 매개) 다음이 수행 됩니다.

- 디스플레이 템플릿이에서 레이블을 렌더링 되 고 값은 사용자에 게 표시 됩니다.
- 편집기 템플릿에서 레이블을 렌더링 되 고 숨겨진된 input 요소에는 값은 렌더링 됩니다.

특성을 false로 설정 하는 경우 결과 다음과 같습니다.

- 디스플레이 템플릿이 아무 것도 해당 필드에 대 한 렌더링 됩니다.
- 편집기 서식 파일에서 레이블이 렌더링 되 고 숨겨진된 input 요소에는 값은 렌더링 됩니다.

### <a id="_TOC3_14"></a>Html.ValidationSummary 도우미 메서드는 모델 수준 오류를 표시할 수 있습니다.

모든 유효성 검사 오류에 항상 표시 하는 경우 대신 Html.ValidationSummary 도우미 메서드는 모델 수준의 오류만 표시 하는 새 옵션을 있습니다. 이렇게 하면 유효성 검사 요약에 표시할 모델 수준의 오류 및 필드별 오류 각 필드 옆에 표시 됩니다.

### <a id="_TOC3_15"></a>T4 템플릿을 Visual Studio 생성 된 코드에서 특정.NET Framework의 대상 버전으로

새 속성을 사용할 되는 T4 파일을 응용 프로그램에서 사용 되는.NET Framework의 버전을 지정 하는 ASP.NET MVC T4 호스트에서 합니다. 따라서 T4 템플릿을 코드와.NET Framework의 버전에만 적용 되는 태그를 생성할 수 있습니다. Visual Studio 2008에서이 값은 항상.NET 3.5. Visual Studio 2010에서의 값은.NET 3.5 또는.NET 4입니다.

## <a id="_TOC4"></a>향상 된 API

이 섹션에는 기존 ASP.NET MVC 형식 및 멤버에 대 한 변경 내용을 설명합니다.

- 컨트롤러 클래스에서 보호 된 가상 CreateActionInvoker 메서드를 추가 합니다. 이 메서드가 컨트롤러의 ActionInvoker 속성에 의해 호출 되 고 없는 호출자가 이미 설정 하는 경우 호출자의 지연 인스턴스화 허용 합니다.
- AuthorizeAttribute 클래스에서 보호 된 가상 HandleUnauthorizedRequest 메서드를 추가 합니다. 이 권한 부여에 실패 하는 경우 동작을 제어 하는 AuthorizeAttribute에서 파생 되는 필터를 사용 하도록 설정 합니다.
- ValueProviderDictionary 클래스에는 Add (키, 개체 값 문자열) 메서드를 추가 했습니다. 이 옵션을 사용 하면 다음 예제와 같이 ValueProviderDictionary에 대 한 사전 이니셜라이저 구문을 사용할 수 있습니다.

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample14.cs)]

- 추가 get\_Sys.Mvc.AjaxContext 클래스의 메서드에 개체입니다. 이것이 get 유사한 JavaScript 방법\_가져오기 응답의 경우 콘텐츠 형식은 application/json이 있지만 데이터 방법\_개체 JSON 개체를 반환 합니다.
- AuthorizationContext 클래스에는 ActionDescriptor 속성이 추가 되었습니다.
- 속성이 없는 경우에 ID 속성이 포함 하는 모델에 바인딩할 때 문제를 해결 하려면 사용할 수 있는 UrlParameter.Optional 토큰을 추가 합니다. 폼 게시에서. 자세한 내용을 보려면 항목을 참조 [ASP.NET MVC 2 선택적 URL 매개 변수](http://haacked.com/archive/2010/02/12/asp-net-mvc-2-optional-url-parameters.aspx) Phil Haack의 블로그에서 합니다.

## <a id="_TOC5"></a>주요 변경 내용

다음과 같이 변경에는 기존 ASP.NET MVC 1.0 응용 프로그램에서 오류가 발생할 수 있습니다.

#### <a name="change-in-property-validation-behavior-for-classes-that-implement-idataerrorinfo"></a>IDataErrorInfo를 구현 하는 클래스에 대 한 속성 유효성 검사 동작에서 변경

IDataErrorInfo를 사용 하 여 유효성 검사를 수행 하는 모델 개체에 대 한 모든 속성의 유효성이 확인 되는 새 값을 설정 했는지에 관계 없이 합니다. ASP.NET MVC 1.0에서 속성을 설정 하는 새 값을 검사 합니다. ASP.NET MVC 2 IDataErrorInfo의 오류 속성이 모든 속성 유효성 검사기는 정상적으로 수행 하는 경우에 호출 됩니다.

#### <a name="iis-script-mapping-script-is-no-longer-available-in-the-installer"></a>IIS 스크립트 매핑 스크립트 설치 관리자는 더 이상

IIS 스크립트 매핑 스크립트는 클래식 모드에서 IIS 7 및 IIS 6에 대 한 스크립트 맵을 구성 하는 데 사용 되는 명령줄 스크립트입니다. 스크립트 매핑 스크립트 통합된 모드에서 IIS 7을 사용 하는 경우 또는 Visual Studio 개발 서버를 사용 하는 경우 필요 하지 않습니다. 스크립트에 지원 되지 않는 별도 다운로드로 제공 되는 [ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack)합니다.

#### <a name="the-htmlsubstitute-helper-method-in-mvc-futures-is-no-longer-available"></a>MVC 미래에 Html.Substitute 도우미 메서드를 사용할 수 없습니다.

MVC 뷰 엔진의 렌더링 동작 변경 내용으로 인해 Html.Substitute 도우미 메서드는 작동 하지 않으며 제거 되었습니다.

#### <a name="the-ivalueprovider-interface-replaces-all-uses-of-idictionary"></a>IValueProvider 인터페이스의 IDictionary 모든 사용을 대체

이제 MVC 1.0의 IDictionary를 허용 하는 모든 속성 또는 메서드의 인수 IValueProvider 허용 합니다. 이 변경 내용은 사용자 지정 값 공급자 또는 사용자 지정 모델 바인더를 포함 하는 응용 프로그램만 결정 합니다. 이 변경의 영향을 받는 메서드 및 속성의 예는 다음과 같습니다.

- ValueProvider 속성 ControllerBase 및 ModelBindingContext 클래스입니다.
- 컨트롤러 클래스의 TryUpdateModel 메서드를 지정 합니다.

#### <a name="new-css-classes-were-added-in-the-sitecss-file"></a>Site.css 파일에서 추가 된 새 CSS 클래스

ASP.NET MVC 프로젝트 템플릿에서 Site.css 파일 템플릿 기반 도우미 및 유효성 검사 기능으로 사용 하는 새 스타일을 포함 하도록 업데이트 되었습니다.

#### <a name="helpers-now-return-an-mvchtmlstring-object"></a>도우미는 이제 MvcHtmlString 개체 반환

ASP.NET 4에서 이러한 지원을 새 HTML 인코딩 식 구문을 사용 하려면 HTML 도우미에 대 한 반환 형식을 이제 MvcHtmlString 대신 문자열입니다. ASP.NET 3.5에서 ASP.NET MVC 2 및 새로운 도우미를 사용 하는 경우 됩니다는 HTML 인코딩 구문을; 이용할 수 새 구문은 ASP.NET 4에서 ASP.NET MVC 2를 실행 하는 경우에 사용할 수 있습니다.

#### <a name="jsonresult-now-responds-only-to-http-post-requests"></a>이제 JsonResult에 HTTP POST 요청에만 응답

JSON 하이재킹 기본적으로 정보 노출 될 가능성이 있는 공격을 완화 하기 위해 JsonResult 클래스는 이제 HTTP POST 요청에만 응답 합니다. 대신 POST를 사용 하는 JsonResult 개체를 반환 하는 작업 메서드를 호출 Ajax 가져오기 변경 되어야 합니다. 필요한 경우에 JsonResult의 새 JsonRequestBehavior 속성을 설정 하 여이 동작을 재정의할 수 있습니다. 악용 가능성에 대 한 자세한 내용은 블로그 게시물을 참조 하십시오. [JSON 하이재킹](http://haacked.com/archive/2009/06/25/json-hijacking.aspx) Phil Haack의 블로그에서 합니다.

#### <a name="model-and-modeltype-property-setters-on-modelbindingcontext-are-obsolete"></a>모델 및 ModelType 속성 setter ModelBindingContext에 사용 되지 않습니다.

새 설정 가능한 ModelMetadata 속성 ModelBindingContext 클래스에 추가 되었습니다. 새 속성에는 모델과 ModelType 속성 모두 캡슐화합니다. 모델 및 ModelType 속성 사용 되지 않지만, 이전 버전과 호환성에 대 한 속성 getter 계속 작동 합니다. 이러한 값을 검색할 ModelMetadata 속성에 위임 합니다.

#### <a name="changes-to-the-defaultcontrollerfactory-class-break-custom-controller-factories-that-derive-from-it"></a>여기에서 파생 되는 사용자 지정 컨트롤러 팩터리를 중단 DefaultControllerFactory 클래스에 대 한 변경

DefaultControllerFactory 클래스 RequestContext 속성을 제거 하 여 수정 되었습니다. 이 속성을 대신 요청 컨텍스트 인스턴스가 보호 된 가상 GetControllerInstance 및 GetControllerType 메서드에 전달 됩니다. 이 변경 내용은 DefaultControllerFactory에서 파생 되는 사용자 지정 컨트롤러 팩터리를 결정 합니다.

사용자 지정 컨트롤러 팩터리는 ASP.NET MVC에 대 한 종속성 주입 응용 프로그램을 제공 하 여 자주 사용 됩니다. ASP.NET MVC 2를 지원 하기 위해 사용자 지정 컨트롤러 팩터리를 업데이트 하려면 메서드 서명 또는 서명 새 서명을 일치 하도록 변경 하 고 속성 대신 요청 컨텍스트 매개 변수를 사용 합니다.

#### <a name="area-is-a-now-a-reserved-route-value-key"></a>"영역"이 이제 예약 된 경로 값 키

이제 "컨트롤러" 및 "작업"을 수행 하는 동일한 방식으로에서 경로 값에서 문자열 "영역" ASP.NET MVC의이 특별 한 의미를 갖습니다. 한 의미는 HTML 도우미 "영역"을 포함 하는 경로 값 사전으로 제공 하는 경우 도우미 추가 되 고 더 이상 "영역" 쿼리 문자열에서입니다.

영역 기능을 사용 하는 경우에 경로 URL의 일부로 {영역}를 사용 하지 않도록 해야 합니다.


## <a id="_TOC6"></a>고 지 사항

본 문서는 예비 문서이며, 여기에 설명한 소프트웨어의 최종 상업적 출시 전에 크게 변경될 수 있습니다.

이 문서에 포함된 정보는 게시 날짜 현재 논의된 문제에 대한 Microsoft Corporation의 당시 관점을 나타냅니다. Microsoft는 변화하는 시장 상황에 부응해야 하므로, Microsoft의 일부에 대한 책임으로 해석되어서는 안되며, 게시 날짜 이후 소개된 정보의 정확성을 Microsoft가 보증할 수 없습니다.

이 백서는 정보 제공만을 목적으로 합니다. Microsoft는 이 문서에 있는 정보에 대한 명시적 또는 묵시적, 법적인 보증을 하지 않습니다.

해당 저작권법을 준수하는 것은 사용자의 책임입니다. 저작권에서의 권리와는 별도로, 이 설명서의 어떠한 부분도 Microsoft의 명시적인 서면 승인 없이는 어떠한 형식이나 수단(전기적, 기계적, 복사기에 의한 복사, 디스크 복사 또는 다른 방법) 또는 목적으로도 복제되거나, 검색 시스템에 저장 또는 도입되거나, 전송될 수 없습니다.

Microsoft가 이 설명서 본안에 관련된 특허권, 상표권, 저작권 또는 기타 지적 재산권 등을 보유할 수도 있습니다. 서면 사용권 계약에 따라 Microsoft로부터 귀하에게 명시적으로 제공된 권리 이외에, 이 문서의 제공은 귀하에게 이러한 특허권, 상표권, 저작권, 또는 기타 지적 소유권 등에 대한 어떠한 사용권도 허여하지 않습니다.

다른 설명이 없는 한, 용례에 사용된 회사, 기관, 제품, 도메인 이름, 전자 메일 주소, 로고, 사람, 장소 및 이벤트 등은 실제 데이터가 아닙니다. 어떠한 실제 회사, 기관, 제품, 도메인 이름, 전자 메일 주소, 로고, 사람, 장소 또는 이벤트와도 연관시킬 의도가 없으며 그렇게 유추해서도 안 됩니다.

© 2010 Microsoft Corporation입니다. All rights reserved.

Microsoft 및 Windows는 미국 및/또는 기타 국가에서 Microsoft Corporation의 상표이거나 등록된 상표입니다.

여기에 언급된 실제 회사와 제품의 이름은 각각 해당 소유자의 상표일 수 있습니다.
