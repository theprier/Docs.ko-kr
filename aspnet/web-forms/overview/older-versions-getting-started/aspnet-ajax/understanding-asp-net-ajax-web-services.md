---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-web-services
title: ASP.NET AJAX 웹 서비스를 이해 | Microsoft Docs
author: scottcate
description: 웹 서비스는 분산된 시스템 간에 데이터를 교환 하기 위한 플랫폼 간 솔루션을 제공 하는.NET framework의 필수적인 부분입니다. 하지만 웹...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/28/2008
ms.topic: article
ms.assetid: 3332d6e7-e2e1-4144-b805-e71d51e7e415
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-web-services
msc.type: authoredcontent
ms.openlocfilehash: 0b9f61f895fea1960ebd25780454b86d5c3ba1bb
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="understanding-aspnet-ajax-web-services"></a>ASP.NET AJAX 웹 서비스 이해
====================
으로 [Scott 인증서](https://github.com/scottcate)

[PDF 다운로드](http://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial05_Web_Services_with_MS_Ajax_cs.pdf)

> 웹 서비스는 분산된 시스템 간에 데이터를 교환 하기 위한 플랫폼 간 솔루션을 제공 하는.NET framework의 필수적인 부분입니다. 웹 서비스는 일반적으로 서로 다른 운영 체제, 개체 모델 및 프로그래밍 언어 데이터를 주고받을 수 있도록 사용 되지만 이러한 데도 사용할 수 있습니다 동적으로 ASP.NET AJAX 페이지에 데이터를 삽입 또는 백 엔드 시스템에는 페이지에서 데이터를 전송 합니다. 이 모든 작업에 다시 게시 하지 않고 수행할 수 있습니다.


## <a name="calling-web-services-with-aspnet-ajax"></a>ASP.NET AJAX와 함께 웹 서비스 호출

Dan Wahlin

웹 서비스는 분산된 시스템 간에 데이터를 교환 하기 위한 플랫폼 간 솔루션을 제공 하는.NET framework의 필수적인 부분입니다. 웹 서비스는 일반적으로 서로 다른 운영 체제, 개체 모델 및 프로그래밍 언어 데이터를 주고받을 수 있도록 사용 되지만 이러한 데도 사용할 수 있습니다 동적으로 ASP.NET AJAX 페이지에 데이터를 삽입 또는 백 엔드 시스템에는 페이지에서 데이터를 전송 합니다. 이 모든 작업에 다시 게시 하지 않고 수행할 수 있습니다.

ASP.NET AJAX UpdatePanel 컨트롤에 AJAX 하는 간단한 방법을 제공 하며 ASP.NET 페이지를 사용 하도록 설정, UpdatePanel을 사용 하지 않고 서버에서 데이터를 동적으로 액세스 하는 경우가 있을 수 있습니다. 이 문서에서 만들고 ASP.NET AJAX 페이지 내에서 웹 서비스를 사용 하 여이 수행 하는 방법을 볼 수 있습니다.

이 문서는 AutoCompleteExtender를 호출 하는 ASP.NET AJAX 도구 키트에서 사용 하도록 설정 하는 웹 서비스 제어를 비롯 하 여 핵심 ASP.NET AJAX 확장에 사용할 수 있는 기능에 집중 합니다. 다루고는 AJAX 사용 웹 서비스를 정의 클라이언트 프록시를 만들기 및 JavaScript 사용 하 여 웹 서비스 호출에 있습니다. ASP.NET 페이지 메서드를 직접 웹 서비스 호출 수 설정 하는 방법도 표시 됩니다.

## <a name="web-services-configuration"></a>웹 서비스 구성

Visual Studio 2008과 함께 새 웹 사이트 프로젝트를 만들면 web.config 파일에 이전 버전의 Visual Studio의 사용자에 게 익숙하지 않을 수 있는 새로운 기능이 추가 수가 있습니다. 이러한 수정 중 일부 매핑될 "asp" 접두사 ASP.NET AJAX 컨트롤 이므로 필수 HttpHandlers 및 Httpmodule을 정의 하는 동안 페이지에서 사용할 수 있습니다. 수정 내용이 표시 목록 1의 `<httpHandlers>` web.config 웹 서비스 호출에 영향을 주는 요소입니다. HttpHandler.asmx 호출을 처리 하는 데 사용 되는 기본 사라지고 System.Web.Extensions.dll 어셈블리에 있는 ScriptHandlerFactory 클래스 아래 템플릿으로 바뀝니다. System.Web.Extensions.dll 모든 ASP.NET AJAX에서 사용 하는 핵심 기능을 포함 합니다.

**목록 1입니다. ASP.NET AJAX 웹 서비스 핸들러 구성**

[!code-xml[Main](understanding-asp-net-ajax-web-services/samples/sample1.xml)]

JavaScript 웹 서비스 프록시를 사용 하 여.NET 웹 서비스에 ASP.NET AJAX 페이지에서 만들어지는 개체 JSON (JavaScript Notation) 호출을 허용 하기 위해이 HttpHandler 대체 구성 됩니다. ASP.NET AJAX 웹 서비스에 일반적으로 웹 서비스와 관련 된 표준 SOAP Simple Object Access Protocol () 호출 반대로 JSON 메시지를 보냅니다. 따라서 더 작은 요청 및 응답 메시지 전체 됩니다. 또한 있습니다 데이터의 보다 효율적인 클라이언트 쪽 처리에 대 한 ASP.NET AJAX JavaScript 라이브러리는 JSON 개체를 사용 하도록 최적화 되어 있으므로. 2 및 JSON 형식으로 serialize 되는 웹 서비스 요청 및 응답 메시지의 목록 3 표시 예를 나열 합니다. 목록 2에 표시 되는 요청 메시지 고객 개체의 배열 및 관련된 속성 목록 3의 응답 메시지를 전달 하는 동안 값이 "벨기에" 인 국가 매개 변수를 전달 합니다.

**2를 나열 합니다. 웹 서비스 요청 메시지를 JSON으로 직렬화 됨**

[!code-json[Main](understanding-asp-net-ajax-web-services/samples/sample2.json)]

> *> [!NOTE] 작업 이름이 웹 서비스 URL의 일부분으로 정의 된 또한 JSON을 통해 요청 메시지 항상 전송 되지 않습니다. 웹 서비스를 통해 전달 될 매개 변수를 true로 설정 UseHttpGet 매개 변수와 함께 ScriptMethod 특성을 사용할 수는 쿼리 문자열 매개 변수입니다.*


**3을 나열 합니다. 웹 서비스 응답 메시지를 JSON으로 직렬화 됨**

[!code-json[Main](understanding-asp-net-ajax-web-services/samples/sample3.json)]

다음 섹션에서 웹 서비스를 JSON 요청 메시지를 처리 하 고 단순 / 복합 형식에서 응답을 만드는 방법을 배웁니다.

## <a name="creating-ajax-enabled-web-services"></a>AJAX 사용 웹 서비스 만들기

ASP.NET AJAX 프레임 워크에는 웹 서비스를 호출 하는 여러 가지 방법으로 제공 합니다. (ASP.NET AJAX 도구 키트에서 사용 가능) AutoCompleteExtender 컨트롤 또는 JavaScript를 사용할 수 있습니다. 그러나 서비스를 호출 하기 전에 있는 AJAX 가능 하 게 것 클라이언트 스크립트 코드에서 호출 될 수 있도록 합니다.

ASP.NET 웹 서비스를 처음 접하는 여부를 만들려면 간단 하 고 AJAX 기능을 사용 하도록 서비스를 찾을 수 있습니다. .NET framework에 지원 되는 2002의 초기 릴리스 이후 ASP.NET 웹 서비스 만들기 및 ASP.NET AJAX Extensions.NET framework의 기본 기능 집합에 따른 추가 AJAX 기능을 제공 합니다. Visual Studio.NET 2008 베타 2.asmx 웹 서비스 파일을 만드는 데 기본적으로 지원 하 고 System.Web.Services.WebService 클래스에서 클래스 옆에 있는 연결 된 코드를 자동으로 파생 됩니다. 메서드를 클래스에 추가 하면 웹 서비스 소비자의 호출을 위해 WebMethod 특성을 적용 해야 합니다.

목록 4 GetCustomersByCountry() 라는 메서드를 WebMethod 특성을 적용 하는 예를 보여 줍니다.

**4를 나열 합니다. WebMethod 특성을 사용 하 여 웹 서비스**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample4.cs)]

GetCustomersByCountry() 메서드 국가 매개 변수를 받아들이고 고객 개체 배열을 반환 합니다. 메서드에 전달 된 국가 값은 호출, 데이터베이스에서 데이터를 검색 하는 데이터 계층 클래스 데이터로 고객 개체 속성을 채울 배열을 반환할는 비즈니스 레이어 클래스에 전달 됩니다.

## <a name="using-the-scriptservice-attribute"></a>ScriptService 특성을 사용 하 여

특성을 사용 하면 웹 서비스에 표준 SOAP 메시지를 보내는 클라이언트에 의해 호출 될 GetCustomersByCountry() 메서드 WebMethod를 추가 하는 동안 기본 ASP.NET AJAX 응용 프로그램에서 만들어지는 JSON 호출을 허용 하지 않습니다 것입니다. ASP.NET AJAX 확장을 적용 해야 할 수 있게 하려면 JSON 호출을 허용 하도록 `ScriptService` 특성을 웹 서비스 클래스. 이 사용 하면 JSON을 사용 하 여 포맷 하는 응답 메시지를 보내려면 웹 서비스 및 클라이언트 쪽 스크립트 JSON 메시지를 전송 하 여 서비스를 호출할 수 있습니다.

목록 5 ScriptService 특성 CustomersService 라는 웹 서비스 클래스를 적용 하는 예를 보여 줍니다.

**5를 나열 합니다. 웹 서비스를 AJAX 가능 하 게 ScriptService 특성을 사용 하 여**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample5.cs)]

AJAX 스크립트 코드에서 호출할 수 있습니다 나타내는 표식 ScriptService 특성 역할을 합니다. 실제로 백그라운드에서 발생 하는 JSON serialization 또는 deserialization 작업 중 하나를 처리 하지 않는 것입니다. (Web.config에서 구성) ScriptHandlerFactory와 기타 관련된 클래스 대량의 JSON 처리를 수행 합니다.

## <a name="using-the-scriptmethod-attribute"></a>ScriptMethod 특성을 사용 하 여

ScriptService 특성이 ASP.NET AJAX 페이지에서 사용할.NET 웹 서비스에 정의 해야 하는 유일한 ASP.NET AJAX 특성이입니다. 그러나 ScriptMethod 이라는 다른 특성에는 서비스의 웹 메서드에 직접도 적용할 수 있습니다. 포함 하 여 세 가지 속성을 정의 하는 ScriptMethod `UseHttpGet`, `ResponseFormat` 및 `XmlSerializeString`합니다. 이러한 속성의 값을 변경 요청 웹 메서드의 허용 유형을 웹 메서드를 원시 XML 데이터 형식으로 반환 해야 하는 경우 GET,으로 변경 해야 하는 경우에 유용할 수 있는 `XmlDocument` 또는 `XmlElement` 개체나 데이터에서 반환 하는 경우는  서비스는 JSON이 아닌 XML로 serialize 항상 해야 합니다.

웹 메서드를 사용 해야 하는 경우 속성을 사용할 수 있습니다 UseHttpGet POST 요청이 아닌 요청을 가져옵니다. 요청 쿼리 문자열 매개 변수를 변환할 웹 메서드에 입력된 매개 변수가 있는 URL을 사용 하 여 전송 됩니다. 속성의 기본값은 false 및만 해야 UseHttpGet로 설정할 수 `true` 성공 하 고 중요 한 데이터는 웹 서비스에 전달 되지 않은 경우 작업은 알려진 하는 경우. 목록 6 UseHttpGet 속성과 함께 ScriptMethod 특성을 사용 하는 예제를 보여 줍니다.

**6을 나열 합니다. UseHttpGet 속성으로 ScriptMethod 특성을 사용 합니다.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample6.cs)]

목록 6에 HttpGetEcho 웹 메서드를 호출할 때 전송 되는 헤더의 예는 다음 나와 있습니다.

`GET /CustomerViewer/DemoService.asmx/HttpGetEcho?input=%22Input Value%22 HTTP/1.1`

HTTP GET 요청을 수락 하도록 웹 메서드를 허용 하는 것 외에도 ScriptMethod 특성 데도 사용할 수 있습니다 때 XML 응답의 JSON 보다는 서비스에서 반환 해야 합니다. 예를 들어 웹 서비스는 원격 사이트에서 RSS 피드를 검색 하 고 XmlDocument 또는 XmlElement 개체로 반환할 수 있습니다. 처리 하는 XML의 데이터 발생할 수 있습니다 다음 클라이언트에서.

목록 7 ResponseFormat 속성을 사용 하 여 XML 데이터 웹 메서드에서 반환 되어야 함을 지정 하려면 예를 보여 줍니다.

**7을 나열 합니다. ResponseFormat 속성으로 ScriptMethod 특성을 사용 합니다.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample7.cs)]

ResponseFormat 속성 XmlSerializeString 속성과 함께 사용할 수도 있습니다. XmlSerializeString 속성이 기본값인 false 이므로 모든 제외한 웹 메서드에서 반환 하는 문자열 형식을 XML로 serialize 되는지 반환 때는 `ResponseFormat` 속성이 `ResponseFormat.Xml`합니다. 때 `XmlSerializeString` 로 설정 된 `true`, 웹 메서드에서 반환 하는 모든 형식은 문자열 형식을 포함 한 XML로 serialize 됩니다. ResponseFormat 속성의 값이 있으면 `ResponseFormat.Json` XmlSerializeString 속성은 무시 됩니다.

8 나열 하는 XML로 serialize 되는 문자열을 강제로 XmlSerializeString 속성을 사용 하는 예제를 보여 줍니다.

**8를 나열 합니다. XmlSerializeString 속성으로 ScriptMethod 특성 사용**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample8.cs)]

목록 8에 표시 된 GetXmlString 웹 메서드 호출에서 반환 되는 값 다음에 나타납니다.

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample9.cs)]

기본 JSON 형식의 요청 및 응답 메시지의 전체 크기를 최소화 하 고 브라우저 간 방식으로 더 쉽게 ASP.NET AJAX 클라이언트에서 사용 됩니다, 있지만 ResponseFormat 및 XmlSerializeString 속성 수 활용 하는 경우 클라이언트 Internet Explorer 5와 같은 또는 더 높은 응용 프로그램 웹 메서드에서 반환 되는 XML 데이터를 기대 합니다.

## <a name="working-with-complex-types"></a>복합 형식 사용

목록 5는 예제를 보여의 웹 서비스에서 Customer 라는 복합 형식을 반환 합니다. Customer 클래스는 여러 다른 간단한 종류 FirstName 및 LastName 등의 속성으로 내부적으로 정의합니다. 입력된 매개 변수로 사용 되는 복합 형식 또는 AJAX 사용 웹 메서드의 반환 형식을 자동으로 클라이언트 쪽에 보내지기 전에 JSON으로 serialize 됩니다. 그러나 중첩 된 복합 형식 (다른 형식 내에서 내부적으로 정의 된)은 사용할 수 없습니다 클라이언트에 독립 실행형 개체로 기본적으로.

여기서는 웹 서비스에서 사용 하는 중첩된 된 복합 형식을 사용 해야 클라이언트 페이지에서의 경우에서 ASP.NET AJAX GenerateScriptType 특성 웹 서비스에 추가할 수 있습니다. 목록 9에 표시 된 CustomerDetails 클래스 주소 및 성별 속성을 포함 하는 예를 들어 있는 ***중첩 된 복합 형식을 나타냅니다.***

**9를 나열 합니다. 여기에 표시 된 CustomerDetails 클래스에 두 개의 중첩 된 복합 형식을 포함 합니다.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample10.cs)]

목록 9에 표시 된 CustomerDetails 클래스 내에서 정의 된 주소 및 성별 개체 않습니다 자동으로 사용할 수 있게 사용 하기 위해 JavaScript 통해 클라이언트 쪽에서 중첩된 형식 이므로 (주소는 클래스 및 성별은 열거형)입니다. 웹 서비스 내에서 사용 되는 중첩된 형식은 클라이언트 쪽에서 사용할 수 있어야 하는 경우에서 앞에서 언급 한 GenerateScriptType 특성을 사용할 수 있습니다 (목록 10 참조). 이 특성은 중첩 된 복합 형식을 서로 다른 서비스에서 반환 되는 있는 경우에 여러 번 추가할 수 있습니다. 특정 웹 메서드 위에 또는 웹 서비스 클래스에 직접 적용할 수 있습니다.

**10을 나열 합니다. GenerateScriptService 특성을 사용 하 여 클라이언트에 사용할 수 있어야 하는 중첩된 형식을 정의 합니다.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample11.cs)]

적용 하 여는 `GenerateScriptType` 특성 웹 서비스, 주소 및 성별 형식에 자동으로 사용 가능 하 게 사용 하기 위해 클라이언트 측 ASP.NET AJAX JavaScript 코드입니다. 자동으로 생성 되 고 웹 서비스에 GenerateScriptType 특성을 추가 하 여 클라이언트에 전송 하는 JavaScript의 예로 목록 11에 표시 됩니다. 문서의 뒷부분에 중첩 된 복합 형식을 사용 하는 방법을 볼 수 있습니다.

**11을 나열 합니다. 중첩 된 복합 형식을 ASP.NET AJAX 페이지에서 사용할 수 있습니다.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample12.cs)]

웹 서비스를 만들고 ASP.NET AJAX 페이지에 액세스할 수 있도록 하는 방법, 살펴보았으므로 이제 만들고 데이터를 검색 하거나 웹 서비스에 보낼 수 있도록 JavaScript 프록시를 사용 하는 방법에 대해를 살펴보겠습니다.

## <a name="creating-javascript-proxies"></a>JavaScript 프록시 만들기

일반적으로 표준 웹 서비스 (.NET 또는 다른 플랫폼) 호출 하면 보내는 SOAP 요청 및 응답 메시지의 복잡성 으로부터 보호 하는 프록시 개체를 만드는 과정이 포함 됩니다. ASP.NET AJAX 웹 서비스 호출 에서도 JavaScript 프록시가 만들고 사용할 수 있는 쉽게 직렬화 및 JSON 메시지를 역직렬화 하는 방법에 대 한 걱정 없이 서비스를 호출 하는 데 사용 합니다. ASP.NET AJAX ScriptManager 컨트롤을 사용 하 여 JavaScript 프록시를 자동으로 생성할 수 있습니다.

웹 서비스를 호출할 수 있는 JavaScript 프록시를 만드는 ScriptManager의 서비스 속성을 사용 하 여 수행 됩니다. 이 속성을 사용 하는 ASP.NET AJAX 페이지 다시 게시 작업을 요구 하지 않고 데이터를 받으려면 비동기적으로 호출할 수 있는 하나 이상의 서비스를 정의할 수 있습니다. ASP.NET AJAX를 사용 하 여 서비스를 정의 `ServiceReference` 컨트롤 및 컨트롤의 웹 서비스 URL 할당 `Path` 속성입니다. 12 나열 CustomersService.asmx 라는 서비스 참조의 예를 보여 줍니다.

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample13.aspx)]

**12를 나열 합니다. ASP.NET AJAX 페이지에서 사용 하는 웹 서비스를 정의 합니다.**

ScriptManager 컨트롤을 통해 CustomersService.asmx에 대 한 참조를 추가 하면 동적으로 생성 하 고 페이지에서 참조 하는 JavaScript 프록시. 프록시를 사용 하 여 포함 된는 &lt;스크립트&gt; 태그 및 CustomersService.asmx 파일을 호출 하 고 /js의 끝에 추가 하 여 동적으로 로드 합니다. 다음 예제에서는 web.config에 디버깅 사용 하지 않도록 설정 하는 경우 JavaScript 프록시 페이지에 포함 하는 방법을 보여 줍니다.

[!code-html[Main](understanding-asp-net-ajax-web-services/samples/sample14.html)]

> *> [!NOTE] 생성 되는 실제 JavaScript 프록시 코드를 확인 하려는 경우 Internet Explorer의 주소 상자에 원하는.NET 웹 서비스 URL을 입력 하 고 /js의 끝에 추가할 수 있습니다.*


JavaScript 프록시의 디버그 버전으로 페이지에 포함 될 web.config에서 디버깅을 설정한 경우 다음에 나타납니다.

[!code-html[Main](understanding-asp-net-ajax-web-services/samples/sample15.html)]

ScriptManager에서 만든 JavaScript 프록시 페이지에 직접 포함 될 수 있지만 사용 하 여 참조 하지 않고는 &lt;스크립트&gt; 태그의 src 특성입니다. ServiceReference 컨트롤의 InlineScript 속성을 true (기본값은 false)로 설정 하 여이 작업을 수행할 수 있습니다. 여러 페이지에 걸쳐 및 서버에 대 한 네트워크 호출의 수를 줄이기 위해 원하는 프록시 공유 되지 않은 경우에 유용할 수 있습니다. ASP.NET AJAX 응용 프로그램에서 여러 페이지에서 프록시 사용 되는 경우의 기본값은 false이 좋습니다. 브라우저에서 InlineScript 프록시 스크립트를 true로 설정 되 면을 캐시할 수 없습니다. InlineScript 속성을 사용 하는 예제는 다음 표시 됩니다.

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample16.aspx)]

## <a name="using-javascript-proxies"></a>JavaScript 프록시를 사용 하 여

ScriptManager 컨트롤을 사용 하는 ASP.NET AJAX 페이지에서 참조 되는 웹 서비스 웹 서비스에 대 한 호출을 가능 하 고 콜백 함수를 사용 하 여 반환된 된 데이터를 처리할 수 있습니다. 웹 서비스 (있는 경우) 해당 네임 스페이스를 참조, 클래스 이름 및 웹 메서드 이름으로 호출 됩니다. 반환된 된 데이터를 처리 하는 콜백 함수를 함께 웹 서비스에 전달 된 매개 변수를 정의할 수 있습니다.

GetCustomersByCountry() 라는 웹 메서드를 호출 하는 JavaScript 프록시를 사용 하는 예제는 13 목록에 표시 됩니다. GetCustomersByCountry() 함수는 최종 사용자가 페이지에 있는 단추를 클릭할 때 호출 됩니다.

**13을 나열 합니다. JavaScript 프록시를 통해 웹 서비스를 호출 합니다.**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample17.js)]

이 호출은 InterfaceTraining 네임 스페이스를 참조, 서비스에 대 한 CustomersService 클래스와 GetCustomersByCountry 웹 메서드가 정의 합니다. 텍스트 상자에서 가져온 국가 값 뿐만 아니라 라는 OnWSRequestComplete 비동기 웹 서비스 호출이 반환 될 때 호출 해야 하는 콜백 함수를 전달 합니다. OnWSRequestComplete 처리 하는 서비스에서 반환 된 고객 개체의 배열을 페이지에 표시 되는 테이블에 변환 합니다. 호출에서 생성 된 출력을 그림 1에 표시 됩니다.


[![웹 서비스에 대 한 비동기 AJAX 호출 하 여 가져온 데이터를 바인딩입니다.](understanding-asp-net-ajax-web-services/_static/image2.png)](understanding-asp-net-ajax-web-services/_static/image1.png)

**그림 1**: 웹 서비스에 대 한 비동기 AJAX 호출 하 여 가져온 데이터 바인딩.  ([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-web-services/_static/image3.png))


또한 JavaScript 프록시 웹 메서드를 호출 해야 하지만 프록시 안 응답을 기다리는 경우에 웹 서비스에 단방향 호출을 만들 수 있습니다. 예를 들어 다음 작업 흐름 같은 프로세스 시작 하는 서비스에서의 반환 값을 기다리지 않고 웹 서비스를 호출 하는 것이 좋습니다. 단방향 호출 수는 서비스에 수행 해야 하는 경우에 간단 하 게 목록 13에 표시 되는 콜백 함수를 생략할 수 있습니다. 콜백 함수가 정의 되어 있으므로 데이터를 반환 하는 웹 서비스에 대 한 프록시 개체 대기 하지 않습니다.

## <a name="handling-errors"></a>오류 처리

웹 서비스에 대 한 비동기 콜백을 여러 유형의 아래, 반환 되는 예외 또는 웹 서비스를 사용할 수 없게 되 고 네트워크와 같은 오류가 발생할 수 있습니다. 다행히 JavaScript 프록시 개체는 ScriptManager에서 생성 된 오류 및 앞에 표시 된 성공 콜백에 외에도 오류를 처리 하도록 정의할 수에 대 한 콜백을 여러 개 허용 합니다. 14 목록에 표시 된 대로 웹 메서드에 대 한 호출의 표준 콜백 함수가 직후 오류 콜백 함수를 정의할 수 있습니다.

**14를 나열 합니다. Error 콜백 함수를 정의 하 고 오류를 표시 합니다.**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample18.js)]

웹 서비스를 호출할 때 발생 하는 모든 오류를 매개 변수로 오류를 나타내는 개체를 허용 하는 호출 될 OnWSRequestFailed() 콜백 함수를 트리거합니다. Error 개체 뿐만 아니라 여부 호출 시간이 초과 되었습니다 오류의 원인을 확인 하려면 다양 한 기능을 노출 합니다. 14 나열 하는 다른 오류 함수를 사용 하는 예제 보여주며 그림 2는 함수에 의해 생성 된 출력의 예를 보여 줍니다.


[![ASP.NET AJAX 오류 함수를 호출 하 여 생성 된 출력 합니다.](understanding-asp-net-ajax-web-services/_static/image5.png)](understanding-asp-net-ajax-web-services/_static/image4.png)

**그림 2**: ASP.NET AJAX 오류 함수를 호출 하 여 생성 된 출력 합니다.  ([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-web-services/_static/image6.png))


## <a name="handling-xml-data-returned-from-a-web-service"></a>웹 서비스에서 반환 된 XML 데이터를 처리 합니다.

이전 웹 메서드는 ResponseFormat 속성과 함께 ScriptMethod 특성을 사용 하 여 원시 XML 데이터를 반환할 수 어떻게 있을 것입니다. ResponseFormat ResponseFormat.Xml으로 설정 된 경우 웹 서비스에서 반환 된 데이터는 JSON이 아닌 XML로 serialize 됩니다. XML 데이터를 JavaScript 또는 XSLT를 사용 하 여 처리를 위해 클라이언트에 직접 전달 해야 하는 경우에 유용할 수 있습니다. 현재 시간에 Internet Explorer 5 이상이 구문 분석 하 고 MSXML에 대 한 기본 제공 지원으로 인해 XML 데이터를 필터링에 대 한 최상의 클라이언트 쪽 개체 모델을 제공 합니다.

웹 서비스에서 XML 데이터를 검색 하는 것은 다른 데이터 형식을 검색 하는 방법과 다르지 않습니다. 적절 한 함수를 호출 하는 콜백 함수를 정의 합니다. JavaScript 프록시를 호출 하 여 시작 합니다. 호출에서 반환 되 면 콜백 함수에서 데이터를 처리할 수 있습니다.

15 나열 하는 XmlElement 개체를 반환 하는 GetRssFeed() 라는 웹 메서드를 호출 합니다. 예를 보여 줍니다. GetRssFeed()는 RSS 피드를 검색에 대 한 URL을 나타내는 단일 매개 변수를 허용 합니다.

**15를 나열 합니다. 웹 서비스에서 반환 된 XML 데이터를 사용 합니다.**

[!code-html[Main](understanding-asp-net-ajax-web-services/samples/sample19.html)]

이 예제에서는 RSS 피드 URL을 전달 하 고 OnWSRequestComplete() 함수에서 반환 된 XML 데이터를 처리 합니다. OnWSRequestComplete() 경우 브라우저는 MSXML 파서를 사용할 수 있는지 여부를 확인 하려면 Internet Explorer를 먼저 확인 합니다. 그럴 경우 XPath 문을 사용 하는 모든 찾으려고 &lt;항목&gt; RSS 피드 내에 태그입니다. 그런 다음이 각 항목 반복 및 연결 된 &lt;제목&gt; 및 &lt;링크&gt; 태그 배치 되 고 각 항목의 데이터를 표시 하려면 처리 됩니다. 그림 3에는 ASP.NET AJAX GetRssFeed() 웹 메서드에 JavaScript 프록시를 통해 호출을 생성 하는 출력의 예가 나와 있습니다.

## <a name="handling-complex-types"></a>복합 형식 처리

복합 형식은 수락 또는 웹 서비스에서 반환 되는 JavaScript 프록시를 통해 자동으로 노출 됩니다. 그러나 중첩 된 복합 형식을 직접 액세스할 수 없는 클라이언트 쪽에서 앞서 설명한 것 처럼 GenerateScriptType 특성이 서비스에 적용 하지 않는 한 합니다. 클라이언트 쪽에서 중첩된 된 복합 형식을 사용 하는 이유는?

이 질문의 답 가정는 ASP.NET AJAX 페이지 고객 데이터를 표시 하면 최종 사용자가 고객의 주소를 업데이트 합니다. 웹 서비스 주소 유형 (CustomerDetails 클래스 내에 정의 된 복합 형식)을 클라이언트로 보낼 수 있는지를 지정 하는 경우 더 나은 코드 다시 사용에 대 한 별도 기능으로 업데이트 프로세스를 나눌 수 있습니다.


[![RSS 데이터를 반환 하는 웹 서비스 호출에서 만들기를 출력 합니다.](understanding-asp-net-ajax-web-services/_static/image8.png)](understanding-asp-net-ajax-web-services/_static/image7.png)

**그림 3**: RSS 데이터를 반환 하는 웹 서비스 호출에서 만들기를 출력 합니다.  ([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-web-services/_static/image9.png))


16 나열 하는 모델 네임 스페이스에 정의 되는 주소 개체를 호출 하는 클라이언트 쪽 코드의 예를 업데이트 된 데이터로 채우는 CustomerDetails 개체의 주소 속성에 할당을 보여 줍니다. 그러면 CustomerDetails 개체 처리를 위해 웹 서비스에 전달 됩니다.

**16을 나열 합니다. 중첩 된 복합 형식을 사용 하 여**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample20.js)]

## <a name="creating-and-using-page-methods"></a>만들기 및 페이지 메서드를 사용 합니다.

웹 서비스 재사용이 서비스의 여러 ASP.NET AJAX 페이지를 포함 하 여 클라이언트를 표시 하는 뛰어난 방법을 제공 합니다. 그러나 페이지 않습니다 계속 사용 하거나 다른 페이지에서 공유 하는 데이터를 검색 해야 하는 경우가 있을 수 있습니다. 이 경우 페이지 데이터에 액세스할 수 있도록.asmx 파일을 만드는 처럼 보이지만 개념을 세우는 서비스는 단일 페이지에만 사용 하므로 합니다.

ASP.NET AJAX는 독립 실행형.asmx 파일을 만들지 않고 웹 서비스와 유사한 호출을 만들기 위한 다른 메커니즘을 제공 합니다. 이 "페이지 메서드" 라고 하는 기술을 사용 하 여 수행 됩니다. 페이지 메서드는에 적용 된 WebMethod 특성이 있는 페이지나 코드 병행 파일에서 직접 포함 되는 정적 (VB.NET의 경우 공유) 메서드입니다. WebMethod 특성을 적용 하 여 호출할 수 있습니다 라는 PageMethods 런타임에 동적으로 생성 되는 특별 한 JavaScript 개체를 사용 하 여 합니다. PageMethods 개체 JSON serialization/deserialization 프로세스에서 사용자를 보호 하는 프록시 역할을 합니다. Note를 PageMethods 개체를 사용 하려면 설정 해야 ScriptManager의 EnablePageMethods 속성을 true로 합니다.

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample21.aspx)]

17 나열 하는 ASP.NET 코드 병행 클래스에서 두 개의 페이지 메서드를 정의 합니다. 예를 보여 줍니다. 이러한 메서드는 앱에 있는 비즈니스 레이어 클래스에서 데이터를 검색\_웹 사이트의 코드 폴더입니다.

**17을 나열 합니다. 페이지 메서드를 정의 합니다.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample22.cs)]

ScriptManager 페이지에 웹 메서드가 있는지 여부를 감지할 때 앞에서 언급 한 PageMethods 개체에 대 한 동적 참조를 생성 합니다. 웹 메서드를 호출 하는 메서드와 전달 되어야 하는 모든 필수 매개 변수 데이터의 이름이 차례로 나옵니다 PageMethods 클래스를 참조 하 여 수행 됩니다. 18 나열 앞에 표시 된 두 개의 페이지 메서드를 호출 합니다. 예를 보여 줍니다.

**18를 나열 합니다. PageMethods JavaScript 개체와 페이지 메서드를 호출 합니다.**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample23.js)]

PageMethods 개체를 사용 하 여 JavaScript 프록시 개체를 사용 하 여 매우 비슷합니다. 먼저 모든 페이지 메서드에 전달 해야 하 고 다음 비동기 호출이 반환 될 때 호출 해야 하는 콜백 함수를 정의 하는 매개 변수 데이터를 지정 합니다. 실패 콜백 지정 될 수도 있습니다 (오류 처리에 대 한 예제 14 목록 참조).

## <a name="the-autocompleteextender-and-the-aspnet-ajax-toolkit"></a>AutoCompleteExtender 및 ASP.NET AJAX 도구 키트

ASP.NET AJAX Toolkit (에서 사용할 수 있는 [ http://ajax.asp.net ](http://ajax.asp.net)) 웹 서비스에 액세스 하는 데 사용할 수 있는 몇 가지 컨트롤을 제공 합니다. 도구 키트 라는 유용한 컨트롤을 포함 하는 구체적으로, `AutoCompleteExtender` 웹 서비스를 호출 하 고 모든 JavaScript 코드를 전혀 작성 하지 않고도 페이지에 데이터 표시를 사용할 수 있는 합니다.

AutoCompleteExtender 컨트롤 textbox의 기존 기능을 확장 하 고 사용자가 더 쉽게 찾고 있는 데이터를 찾을 데 사용할 수 있습니다. 텍스트 상자에 입력 컨트롤은 웹 서비스를 쿼리 하는 데 사용할 수 하 고 텍스트 상자 아래 결과 동적으로 보여 줍니다. 그림 4 AutoCompleteExtender 컨트롤을 사용 하 여 지원 응용 프로그램에 대 한 고객 id를 표시 합니다. 예를 보여 줍니다. Textbox에 서로 다른 문자를 충분할 서로 다른 항목이 입력에 따라 그 아래에 나타납니다. 그런 다음 사용자가 원하는 고객 id를 선택할 수 있습니다.

ASP.NET AJAX 페이지 내에서 AutoCompleteExtender를 사용 하 여 AjaxControlToolkit.dll 어셈블리가 웹 사이트의 bin 폴더에 추가 될 필요 합니다. 도구 키트 어셈블리 추가 되 면 포함 된 컨트롤을 응용 프로그램의 모든 페이지에 사용할 수 있도록 web.config에서 참조 합니다. Web.config의 내에 다음 태그를 추가 하 여이 작업을 수행할 수 있습니다 &lt;컨트롤&gt; 태그:

[!code-xml[Main](understanding-asp-net-ajax-web-services/samples/sample24.xml)]

에 해야 하는 경우 특정 페이지에 컨트롤을 사용 하도록 web.config를 업데이트 하는 대신 다음 예와 같이 페이지의 맨 위에 참조 지시문을 추가 하 여 참조할 수 있습니다.

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample25.aspx)]


[![AutoCompleteExtender 컨트롤 사용.](understanding-asp-net-ajax-web-services/_static/image11.png)](understanding-asp-net-ajax-web-services/_static/image10.png)

**그림 4**: AutoCompleteExtender 컨트롤을 사용 합니다.  ([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-web-services/_static/image12.png))


ASP.NET AJAX 도구 키트를 사용 하도록 웹 사이트를 구성한 후 AutoCompleteExtender 컨트롤에 추가 하려면 페이지 훨씬 일반 ASP.NET 서버 컨트롤을 추가할 때 처럼 합니다. 19 나열 하는 웹 서비스를 호출 하는 컨트롤을 사용 하는 예제를 보여 줍니다.

**19를 나열 합니다. ASP.NET AJAX Toolkit AutoCompleteExtender 컨트롤 사용.**

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample26.aspx)]

AutoCompleteExtender에 서버 컨트롤에 표준 ID와 runat 속성을 포함 하는 여러 다른 속성이 있습니다. 뿐만 아니라 수 있습니다는 최종 사용자 유형 웹 서비스 하기 전에 데이터를 쿼리 하는 문자 수를 정의할 수 있습니다. 19 나열 MinimumPrefixLength 속성 하면 문자를 textbox에 입력 될 때마다 호출 되는 서비스. 텍스트 상자에는 문자를 일치 하는 값을 검색할 호출할 수 있으므로 사용자가 웹 서비스는 문자를 입력할 때마다가이 값을 설정 하 고 주의를 기울여야 합니다. 대상 웹 메서드에 뿐만 아니라 웹 서비스를 호출 하도록 각각 ServicePath 및 ServiceMethod 속성을 사용 하 여 정의 됩니다. 마지막으로, targetcontrolid가 속성 AutoCompleteExtender 컨트롤을 연결 하는 textbox를 식별 합니다.

웹 서비스 호출 이전에 설명한 대로 적용 ScriptService 특성이 있어야 합니다. क र च 대상 웹 메서드에 해야 prefixText 및 count 라는 두 개의 매개 변수입니다. 최종 사용자가 입력 한 문자를 나타내는 prefixText 매개 변수 및 count 매개 변수 항목을 반환 하는 수를 나타냅니다 (기본값은 10). 20 나열 하는 앞의 목록 19에 AutoCompleteExtender 컨트롤에서 호출 GetCustomerIDs 웹 메서드의 예를 보여 줍니다. 웹 메서드를 차례로 호출 데이터 계층 메서드를 처리 데이터를 필터링 하 고 일치 하는 결과 반환 하는 비즈니스 계층 메서드를 호출 합니다. 데이터 계층 방법에 대 한 코드는 21 목록에 표시 됩니다.

**20을 나열 합니다. AutoCompleteExtender 컨트롤에서 전송 된 데이터를 필터링 합니다.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample27.cs)]

**21을 나열 합니다. 최종 사용자 입력에 따라 결과 필터링 합니다.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample28.cs)]

## <a name="conclusion"></a>결론

ASP.NET AJAX 많이 요청 및 응답 메시지를 처리 하는 사용자 지정 JavaScript 코드를 작성 하지 않고도 웹 서비스 호출에 대 한 강력한 지원을 제공 합니다. 이 문서에서 보았을 AJAX 기능을 사용 하도록.NET 웹 서비스 다시 사용 하도록 ScriptManager 컨트롤을 사용 하 여 JavaScript 프록시를 정의 하는 방법 및 JSON 메시지를 처리 하는 방법입니다. 또한 JavaScript 프록시를 사용 하 여 웹 서비스를 호출 하 수 단순 / 복합 형식 처리 하 고 오류를 처리 하는 방법을 살펴보았습니다. 마지막으로, 생성 및 웹 서비스 호출을 수행 하는 과정을 간소화 하기 위해 페이지 메서드를 사용할 수 있는 방법을 고 어떻게 AutoCompleteExtender 컨트롤 수 도움말을 제공할 최종 사용자에 게를 입력 살펴보았습니다. ASP.NET AJAX에서 사용할 수 있는 UpdatePanel을 확실히 단순성 인해 많은 AJAX 프로그래머에 대 한 선택 컨트롤 수 있는, JavaScript 프록시를 통한 웹 서비스를 호출 하는 방법을 알아 두어야 많은 응용 프로그램에서 유용할 수 있습니다.

## <a name="bio"></a>약력

Dan Wahlin (Microsoft 가장 중요 한 Professional ASP.NET 및 XML 웹 서비스)는 기술 교육 인터페이스에서.NET 개발 강사 및 아키텍처 컨설턴트 ([http://www.interfacett.com](http://www.interfacett.com)). Dan ASP.NET 개발자 웹 사이트에 대 한 XML을 기초로 ([www.XMLforASP.NET](http://www.XMLforASP.NET)), INETA 스피커 Bureau에 및 여러 강연 합니다. Dan Professional Windows DNA (Wrox) ASP.NET을 함께 작성: 팁, 자습서 및 코드 (Sam), ASP.NET 1.1 내부자 솔루션, Professional ASP.NET 2.0 AJAX (Wrox), ASP.NET 2.0 MVP 해킹 및 ASP.NET 개발자 (Sam)에 대 한 작성 된 XML입니다. 그 코드, 문서 또는 책을 기록 하지 않습니다, 작성 및 음악 기록 및 재생 있고 그의 아내와 어린이 야구 Dan 이용할 수 있습니다.

Scott 인증서의 근무 기간이 Microsoft 웹 기술을 1997 년부터 이며 myKB.com 부서장 ([www.myKB.com](http://www.myKB.com)) ASP.NET 작성 i 여기서 기반 응용 프로그램 기술 자료 소프트웨어 솔루션에 집중 합니다. Scott에 전자 메일을 통해 연결할 수 [ scott.cate@myKB.com ](mailto:scott.cate@myKB.com) 또는에서 그의 블로그 [ScottCate.com](http://ScottCate.com)

> [!div class="step-by-step"]
> [이전](understanding-asp-net-ajax-localization.md)
> [다음](understanding-asp-net-ajax-debugging-capabilities.md)
