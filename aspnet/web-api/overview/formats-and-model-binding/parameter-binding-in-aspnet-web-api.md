---
uid: web-api/overview/formats-and-model-binding/parameter-binding-in-aspnet-web-api
title: ASP.NET Web API의에서 바인딩 매개 변수 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/11/2013
ms.topic: article
ms.assetid: e42c8388-04ed-4341-9fdb-41b1b4c06320
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/formats-and-model-binding/parameter-binding-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 5aa532137436922519c86246ebfa834910ac0d86
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="parameter-binding-in-aspnet-web-api"></a>ASP.NET Web API의에서 바인딩 매개 변수
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

매개 변수를 호출 하는 프로세스에 대 한 값을 설정 해야 Web API 컨트롤러에서 메서드를 호출할 때 *바인딩*합니다. 이 문서에서는 웹 API 매개 변수를 바인딩하여 하는 방법에 대 한 바인딩 프로세스를 사용자 지정할 수는 어떻게 설명 합니다.

기본적으로 웹 API 매개 변수를 바인딩하는 다음 규칙을 사용 합니다.

- 매개 변수가 "simple" 형식인 경우 Web API URI에서 값을 가져오려고 합니다. 단순 유형에.NET [기본 형식](https://msdn.microsoft.com/library/system.type.isprimitive.aspx) (**int**, **bool**, **double**, 등)를 더한 **TimeSpan**, **DateTime**, **Guid**, **10 진수**, 및 **문자열**, *플러스* 모든 문자열에서 변환할 수 있는 형식 변환기 입력 합니다. (에 대 한 자세한 나중에 형식 변환기입니다.)
- 사용 하 여 복합 형식의 경우 Web API 메시지 본문에서 값을 읽을 하려고에 대 한는 [미디어 유형 포맷터](media-formatters.md)합니다.

예를 들어 다음은 일반적인 웹 API 컨트롤러 메서드에서가입니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample1.cs)]

*id* 매개 변수는 한 &quot;간단한&quot; 입력, 웹 API 요청 URI에서에서 값을 가져오려고 시도 합니다. *항목* Web API는 미디어 유형 포맷터를 사용 하 여 요청 본문에서 값을 읽을 수 있도록 매개 변수는 복합 유형입니다.

URI에서 값을 가져오려면 웹 API 경로 데이터 및 URI 쿼리 문자열에서 찾습니다. 경로 데이터 라우팅 시스템 URI 구문 분석 하는 경로에 일치 때 채워집니다. 자세한 내용은 참조 [라우팅 및 작업 선택](../web-api-routing-and-actions/routing-and-action-selection.md)합니다.

이 문서의 나머지 부분에서는 모델 바인딩 프로세스를 사용자 지정할 수는 방법을 보여 드리 려 합니다. 그러나 복합 형식에 대 한 가능 하면 미디어 유형 포맷터를 사용 하십시오. HTTP의 핵심 원칙은 리소스가 있는 리소스의 표현을 지정 하려면 콘텐츠 협상을 사용 하 여 메시지 본문에 전송 됩니다. 미디어 유형 포맷터는 정확 하 게이 목적을 위해 설계 되었습니다.

## <a name="using-fromuri"></a>[FromUri]를 사용 하 여

URI에서 복합 형식을 읽을 수 있는 웹 API를 강제로 표시 하려면 추가 **[FromUri]** 특성을 매개 변수입니다. 다음 예제에서는 정의 `GeoPoint` 컨트롤러를 가져오는 메서드를 함께 종류는 `GeoPoint` URI에서 합니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample2.cs)]

클라이언트 쿼리 문자열의 위도 및 경도 값을 정렬할 수 및 Web API를 사용 하 여을 생성 한 `GeoPoint`합니다. 예:

`http://localhost/api/values/?Latitude=47.678558&Longitude=-122.130989`

## <a name="using-frombody"></a>[FromBody]를 사용 하 여

요청 본문에서 단순 형식을 읽을 수 있는 웹 API를 강제로 표시 하려면 추가 **[FromBody]** 특성을 매개 변수:

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample3.cs)]

이 예제에서는 웹 API를 사용 하 여 미디어 유형 포맷터의 값을 읽을 *이름* 요청 본문에서. 다음 예제에서는 클라이언트 요청은입니다.

[!code-console[Main](parameter-binding-in-aspnet-web-api/samples/sample4.cmd)]

매개 변수는 [FromBody], 웹 API는 포맷터를 선택 하려면 콘텐츠 형식 헤더를 사용 합니다. 이 예제에서는 콘텐츠 형식이 &quot;응용 프로그램/json&quot; 및 요청 본문은 원시 JSON 문자열 (JSON 개체).

최대 하나의 매개 변수는 메시지 본문에서 읽을 수 있습니다. 따라서이 작동 하지 않습니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample5.cs)]

이 규칙에 대 한 이유는 요청 본문은 한 번만 읽을 수 있는 버퍼링 되지 않은 스트림을에 보관할 수 있습니다.

## <a name="type-converters"></a>형식 변환기

만들어 (있도록 Web API는 URI에서에 연결 하려고) 클래스를 단순 형식으로 처리 하는 Web API를 만들 수 있습니다는 **TypeConverter** 문자열 변환을 제공 합니다.

다음 코드는 `GeoPoint` 지리적 시점을 나타내는 클래스 뒤에 **TypeConverter** 에서 문자열을 변환 하 `GeoPoint` 인스턴스. `GeoPoint` 로 데코레이팅된 클래스는 **[TypeConverter]** 형식 변환기를 지정 하는 특성입니다. (이 예에서는 Mike Stall 블로그 게시물에서 영감을 얻은 [작업 서명은 MVC/WebAPI에서의 사용자 지정 개체에 바인딩하는 방법을](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx).)

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample6.cs)]

Web API에서 처리 하는 이제 `GeoPoint` 단순 형식으로 바인딩할 시도 것을 의미 `GeoPoint` URI에서 매개 변수입니다. 포함할 필요가 없습니다 **[FromUri]** 매개 변수입니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample7.cs)]

클라이언트는 다음과 같은 URI 사용 하 여 메서드를 호출할 수 있습니다.

`http://localhost/api/values/?location=47.678558,-122.130989`

## <a name="model-binders"></a>모델 바인더

형식 변환기를 사용자 지정 모델 바인더를 만드는 것 보다 더 유연한 옵션입니다. 모델 바인더를 사용 하 여에서 액세스할 수 있는 등으로 HTTP 요청, 작업 설명 및 원시 값에 경로 데이터입니다.

모델 바인더를 만들려면 구현는 **IModelBinder** 인터페이스입니다. 이 인터페이스는 단일 메서드를 정의 **BindModel**:

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample8.cs)]

다음에 대 한 모델 바인더를은 `GeoPoint` 개체입니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample9.cs)]

모델 바인더의 원시 입력된 값을 가져옵니다는 *값 공급자*합니다. 이 설계에서는 두 가지 고유 함수를 구분합니다.

- 값 공급자는 HTTP 요청을 사용 하 고 키-값 쌍의 사전을 채웁니다.
- 모델 바인더가이 사전을 사용 하 여 모델을 채웁니다.

Web API의 기본 값 공급자에서 경로 데이터 및 쿼리 문자열 값을 가져옵니다. 예를 들어, URI가 `http://localhost/api/values/1?location=48,-122`, 값 공급자는 다음 키-값 쌍을 만듭니다.

- id = &quot;1&quot;
- 위치 = &quot;48,122&quot;

(않는 기본 경로 템플릿을 한다고 가정 &quot;api / {controller} / {id}&quot;.)

바인딩할 매개 변수 이름에 저장 됩니다는 **ModelBindingContext.ModelName** 속성입니다. 모델 바인더 사전에이 값을 사용 하 여 키를 찾습니다. 값으로 변환 될 수 있고 한 `GeoPoint`, 모델 바인더에 바인딩된 값을 할당는 **ModelBindingContext.Model** 속성입니다.

공지 모델 바인더는 단순 형식 변환을 제한 되지 않습니다. 이 예제에서는 모델 바인더 알려진된 위치의 테이블에서 먼저 찾습니다 및 형식 변환을 사용 하 여 실패할 경우.

**모델 바인더를 설정합니다.**

모델 바인더를 설정 하는 방법은 여러 가지가 있습니다. 첫째, 추가할 수 있습니다는 **[ModelBinder]** 특성을 매개 변수입니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample10.cs)]

추가할 수도 있습니다는 **[ModelBinder]** 특성을 형식입니다. Web API는 해당 형식의 모든 매개 변수에 대해 지정 된 모델 바인더를 사용 합니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample11.cs)]

마지막으로, 모델 바인더 공급자를 추가할 수 있습니다는 **HttpConfiguration**합니다. 모델 바인더 공급자는 모델 바인더를 만드는 팩터리 클래스 단순히 합니다. 파생 하 여 공급자를 만들 수는 [ModelBinderProvider](https://msdn.microsoft.com/library/system.web.http.modelbinding.modelbinderprovider.aspx) 클래스입니다. 그러나 단일 형식을 처리 하는 모델 바인더를 경우 기본 제공 사용 하기 쉽게 **SimpleModelBinderProvider**,이 목적을 위해 디자인 된 합니다. 다음 코드에서는 이 작업을 수행하는 방법을 보여 줍니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample12.cs)]

모델 바인딩 공급자와도 추가 해야는 **[ModelBinder]** 특성을 모델 바인더 및 미디어 유형 포맷터 하지 사용 해야 함을 웹 API를 구별 하는 매개 변수입니다. 하지만 이제 특성에 모델 바인더의 형식을 지정할 필요가 없습니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample13.cs)]

## <a name="value-providers"></a>값 공급자

언급 한 모델 바인더 값 공급자에서 값을 가져옵니다. 사용자 지정 값 공급자를 작성 하려면 구현 된 **IValueProvider** 인터페이스입니다. 요청에서 쿠키의 값을 가져오는 예는 다음과 같습니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample14.cs)]

파생 하 여 값 공급자 팩터리를 만들 필요가 **ValueProviderFactory** 클래스입니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample15.cs)]

값 공급자 팩터리를 추가 **HttpConfiguration** 다음과 같습니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample16.cs)]

Web API 하므로 모든 값 공급자 작성 한 모델 바인더를 호출 하는 경우 **ValueProvider.GetValue**, 모델 바인더를 만들 수 있는 첫 번째 값 공급자에서 값을 받습니다.

사용 하 여 매개 변수 수준에서 값 공급자 팩터리를 설정할 수는 또한는 **ValueProvider** 특성을 다음과 같이 합니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample17.cs)]

지정 된 값 공급자 팩터리 모델 바인딩을 사용 하 고 사용 하지 않는 다른 등록 된 값 공급자의 웹 API 인지를 나타냅니다.

## <a name="httpparameterbinding"></a>HttpParameterBinding

모델 바인더는 보다 일반적인 메커니즘의 특정 인스턴스에 있습니다. 보면는 **[ModelBinder]** 특성 나타납니다 추상에서 파생 되며 **ParameterBindingAttribute** 클래스입니다. 이 클래스는 단일 메서드를 정의 **GetBinding**를 반환 하는 **HttpParameterBinding** 개체:

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample18.cs)]

**HttpParameterBinding** 매개 변수 값에 바인딩할 담당 합니다. 경우 **[ModelBinder]**, 특성을 반환는 **HttpParameterBinding** 구현을 사용 하는 **IModelBinder** 실제 바인딩을 수행할 수 있습니다. 구현할 수도 있습니다 직접 **HttpParameterBinding**합니다.

예를 들어, Etag에서 가져오려는 `if-match` 및 `if-none-match` 요청의 헤더입니다. Etag를 나타내는 클래스를 정의 하 여 시작 합니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample19.cs)]

ETag를 가져올 것인지를 지정 하는 열거형 정의 `if-match` 헤더 또는 `if-none-match` 헤더입니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample20.cs)]

다음은 **HttpParameterBinding** 하는 ETag에서 원하는 헤더 가져오고 ETag 형식의 매개 변수를 바인딩합니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample21.cs)]

**ExecuteBindingAsync** 메서드는 바인딩을 수행 합니다. 이 메서드 내에서 추가 바인딩된 매개 변수 값은 **ActionArgument** 사전에는 **HttpActionContext**합니다.

> [!NOTE]
> 경우에 **ExecuteBindingAsync** 메서드 요청 메시지의 본문을 읽고, 재정의 **WillReadBody** 속성을 true를 반환 합니다. 요청 본문은 한 버퍼링 되지 않은 스트림을 읽을 수만 있고 한 번, 웹 API 적용 규칙 최대 하나의 바인딩 메시지 본문을 읽을 수 수 있습니다.


사용자 지정을 적용 하려면 **HttpParameterBinding**에서 파생 되는 특성을 정의할 수 있습니다 **ParameterBindingAttribute**합니다. 에 대 한 `ETagParameterBinding`에 대 한 두 가지 특성을 정의 하겠습니다 `if-match` 머리글과 대 한 `if-none-match` 헤더입니다. 둘 다 추상 기본 클래스에서 파생 됩니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample22.cs)]

다음은 사용 하는 컨트롤러 메서드는 `[IfNoneMatch]` 특성입니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample23.cs)]

외에 **ParameterBindingAttribute**, 사용자 지정을 추가 하기 위한 다른 후크는 **HttpParameterBinding**합니다. 에 **HttpConfiguration** 개체는 **ParameterBindingRules** 속성은 형식의 anomymous 함수의 컬렉션 (**HttpParameterDescriptor**  - &gt; **HttpParameterBinding**). 예를 들어 GET 메서드의 모든 ETag 매개 변수를 사용 하는 규칙을 추가할 수 있습니다 `ETagParameterBinding` 와 `if-none-match`:

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample24.cs)]

함수 반환 해야 `null` 바인딩을 적용할 수 없는 매개 변수에 대 한 합니다.

## <a name="iactionvaluebinder"></a>IActionValueBinder

전체 매개 변수 바인딩 프로세스는 플러그형 서비스에 의해 제어 됩니다 **IActionValueBinder**합니다. 기본 구현은 **IActionValueBinder** 다음 작업을 수행 합니다.

1. 검색할는 **ParameterBindingAttribute** 매개 변수입니다. 여기에 **[FromBody]**, **[FromUri]**, 및 **[ModelBinder]**, 또는 사용자 지정 특성입니다.
2. 그렇지 않으면, 찾는 위치 **HttpConfiguration.ParameterBindingRules** null이 아닌 반환 하는 함수에 대 한 **HttpParameterBinding**합니다.
3. 그렇지 않으면 이전에 설명 되어 있는 기본 규칙을 사용 합니다. 

    - 매개 변수 형식이 "단순" 형식 변환기가 있는 경우에 URI에서 바인딩하십시오. 배치 같습니다는 **[FromUri]** 매개 변수에 특성입니다.
    - 그렇지 않은 경우 메시지 본문에서 매개 변수를 읽고 하려고 합니다. 배치 같습니다 **[FromBody]** 매개 변수입니다.

원하는 경우 전체를 바꿀 수 있습니다 **IActionValueBinder** 서비스 사용자 지정 구현입니다.

## <a name="additional-resources"></a>추가 리소스

[사용자 지정 매개 변수 바인딩 예제](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/CustomParameterBinding/ReadMe.txt)

Mike Stall 웹 API 매개 변수 바인딩에 대 한 좋은 일련의 블로그 게시물을 작성:

- [매개 변수 바인딩 웹 API을 수행 하는 방법](https://blogs.msdn.com/b/jmstall/archive/2012/04/16/how-webapi-does-parameter-binding.aspx)
- [웹 API에 대 한 MVC 스타일 매개 변수 바인딩](https://blogs.msdn.com/b/jmstall/archive/2012/04/18/mvc-style-parameter-binding-for-webapi.aspx)
- [작업 서명은 MVC/웹 API에서의 사용자 지정 개체에 바인딩하는 방법](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx)
- [Web API에서 사용자 지정 값 공급자를 만드는 방법](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)
- [내부에서 web API 매개 변수 바인딩](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx)
