---
uid: web-api/overview/formats-and-model-binding/parameter-binding-in-aspnet-web-api
title: ASP.NET Web API에서에서 매개 변수 바인딩 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
ms.date: 07/11/2013
ms.assetid: e42c8388-04ed-4341-9fdb-41b1b4c06320
msc.legacyurl: /web-api/overview/formats-and-model-binding/parameter-binding-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 97785db962691c25bac03f904924321af2f6b500
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37810084"
---
<a name="parameter-binding-in-aspnet-web-api"></a>ASP.NET Web API에서에서 매개 변수 바인딩
====================
[Mike Wasson](https://github.com/MikeWasson)

Web API 컨트롤러에서 메서드를 호출 하는 경우 매개 변수를 호출 하는 프로세스에 대 한 값을 설정 합니다 *바인딩*합니다. 이 문서에서는 웹 API의 매개 변수를 바인딩하는 방법을 바인딩 프로세스를 사용자 지정할 수는 방법을 설명 합니다.

기본적으로 웹 API 매개 변수를 바인딩하는 다음 규칙을 사용 합니다.

- 매개 변수가 "simple" 형식이 면 웹 API URI에서 값을 가져오려고 합니다. .NET을 포함 하는 단순 형식 [기본 형식](https://msdn.microsoft.com/library/system.type.isprimitive.aspx) (**int**를 **bool**, **double**등), plus **TimeSpan**, **DateTime**를 **Guid**를 **10 진수**, 및 **문자열**를 *plus* 모든 문자열에서 변환할 수 있는 형식 변환기를 사용 하 여 입력 합니다. (자세한 내용은 나중에 형식 변환기에 대 한입니다.)
- 복합 형식, Web API 메시지 본문에서 값을 읽을 하려고에 대 한 사용 하는 [미디어 유형 포맷터](media-formatters.md)합니다.

예를 들어, 다음은 일반적인 Web API 컨트롤러 메서드에입니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample1.cs)]

합니다 *id* 매개 변수는를 &quot;단순&quot; 입력, Web API가 요청 URI에서에서 값을 가져오려고 합니다. 합니다 *항목* 매개 변수는 복합 유형, Web API는 미디어 유형 포맷터를 사용 하 여 요청 본문에서 값을 읽을 수 있도록 합니다.

URI에서 값을 가져오려면, Web API 경로 데이터 및 URI 쿼리 문자열을 찾습니다. 경로 데이터는 라우팅 시스템 URI를 구문 분석 하 고 경로에 일치 하는 경우에 채워집니다. 자세한 내용은 [라우팅 및 작업 선택](../web-api-routing-and-actions/routing-and-action-selection.md)합니다.

이 문서의 나머지 부분에서는 모델 바인딩 프로세스를 사용자 지정할 수는 방법을 살펴보겠습니다. 그러나 복합 형식에 대 한 가능한 경우 미디어 유형 포맷터를 사용 하십시오. HTTP의 핵심 원칙은 리소스 리소스의 표현을 지정를 콘텐츠 협상을 사용 하 여 메시지 본문에 전송 되는 경우 미디어 유형 포맷터는 정확 하 게이 목적을 위해 설계 되었습니다.

## <a name="using-fromuri"></a>[FromUri]를 사용 하 여

URI에서 복합 형식을 읽을 수 있는 Web API를 강제 적용 하려면 추가 합니다 **[FromUri]** 매개 변수 특성입니다. 다음 예제에서는 정의 `GeoPoint` 컨트롤러를 가져오는 메서드를 함께 형식은 `GeoPoint` URI에서 합니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample2.cs)]

클라이언트 쿼리 문자열에 위도 및 경도 값을 삽입할 수 있고, 웹 API를 사용 하 여 해당 생성을 `GeoPoint`입니다. 예를 들어:

`http://localhost/api/values/?Latitude=47.678558&Longitude=-122.130989`

## <a name="using-frombody"></a>[FromBody]를 사용 하 여

요청 본문을 사용 하 여 단순 형식을 읽어올 수 있는 Web API를 강제 적용 하려면 다음을 추가 합니다 **[FromBody]** 매개 변수 특성:

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample3.cs)]

이 예제에서는 웹 API를 사용 하 여 미디어 유형 포맷터의 값을 읽을 *이름을* 요청 본문에서. 클라이언트 요청 예제는 다음과 같습니다.

[!code-console[Main](parameter-binding-in-aspnet-web-api/samples/sample4.cmd)]

매개 변수 [FromBody]에 있는 경우 Web API 포맷터를 선택 하는 Content-type 헤더를 사용 합니다. 이 예제에서는 콘텐츠 형식은 &quot;application/json&quot; 및 요청 본문은 원시 JSON 문자열 (JSON 개체).

최대 하나의 매개 변수는 메시지 본문에서 읽을 수 있습니다. 따라서이 작동 하지 않습니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample5.cs)]

이 규칙에 대 한 이유는 요청 본문을 버퍼링 되지 않은 한 번만 읽을 수 있는 스트림을에 저장 될 수 있습니다.

## <a name="type-converters"></a>형식 변환기

만들기 (있도록 Web API는 URI에서 바인딩할 시도) 클래스를 간단한 형식으로 처리 하는 Web API를 만들 수 있습니다는 **TypeConverter** 문자열 변환을 제공 합니다.

다음 코드에서는 `GeoPoint` 지리적 시점을 나타내는 클래스 및 **TypeConverter** 문자열에서 변환 `GeoPoint` 인스턴스. 합니다 `GeoPoint` 으로 데코 레이트 된 클래스를 **[TypeConverter]** 형식 변환기를 지정 하는 특성입니다. (이 예제에서는 된 Mike Stall의 블로그 게시물에서 영감을 받았습니다 [MVC/WebAPI에서 작업 서명에서 사용자 지정 개체에 바인딩하는 방법을](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx).)

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample6.cs)]

Web API에서 처리 하는 이제 `GeoPoint` 단순 형식으로 바인딩할 시도 의미 `GeoPoint` URI에서 매개 변수입니다. 포함할 필요가 없습니다 **[FromUri]** 매개 변수입니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample7.cs)]

클라이언트는 다음과 같은 URI 사용 하 여 메서드를 호출할 수 있습니다.

`http://localhost/api/values/?location=47.678558,-122.130989`

## <a name="model-binders"></a>모델 바인더

형식 변환기 보다 더 유연한 옵션을 사용자 지정 모델 바인더를 만드는 것입니다. 모델 바인더를 사용 하 여에서 액세스할 수 있는 HTTP 요청, 작업 설명에 원시 값 등을 경로 데이터입니다.

모델 바인더를 만들려면 다음을 구현 합니다 **IModelBinder** 인터페이스입니다. 이 인터페이스는 단일 메서드를 정의 **BindModel**:

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample8.cs)]

여기에 대 한 모델 바인더는 `GeoPoint` 개체입니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample9.cs)]

모델 바인더를 가져옵니다에서 원시 입력된 값을 *값 공급자*합니다. 이 설계는 두 가지 고유한 기능을 구분합니다.

- 값 공급자 HTTP 요청을 사용 하 여 키-값 쌍의 사전을 채웁니다.
- 모델 바인더는이 사전을 사용 하 여 모델을 채웁니다.

Web API에서 기본 값 공급자에서 경로 데이터 및 쿼리 문자열 값을 가져옵니다. 예를 들어, URI가 `http://localhost/api/values/1?location=48,-122`, 값 공급자에는 다음 키-값 쌍을 만듭니다.

- id = &quot;1&quot;
- 위치 = &quot;48,122&quot;

(기본 경로 템플릿에 있다고 가정 하겠습니다 &quot;api / {컨트롤러} / {id}&quot;.)

바인딩할 매개 변수의 이름에 저장 되는 **ModelBindingContext.ModelName** 속성입니다. 모델 바인더 사전에이 값을 사용 하 여 키를 찾습니다. 값 존재 하 고 변환할 수는 `GeoPoint`, 모델 바인더에 바인딩된 값을 할당 합니다 **ModelBindingContext.Model** 속성입니다.

모델 바인더는 단순 형식 변환을 제한 인지 확인 합니다. 이 예제에서는 모델 바인더를 먼저 테이블을 알려진된 위치를 찾습니다 및 형식 변환 실패 하는 경우 사용 합니다.

**모델 바인더를 설정합니다.**

모델 바인더를 설정 하는 방법은 여러 가지가 있습니다. 먼저 추가할 수 있습니다는 **[ModelBinder]** 매개 변수 특성입니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample10.cs)]

추가할 수도 있습니다는 **[ModelBinder]** 형식 특성입니다. 웹 API는 해당 형식의 모든 매개 변수에 대해 지정 된 모델 바인더를 사용 합니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample11.cs)]

마지막으로, 모델 바인더 공급자를 추가할 수 있습니다 합니다 **HttpConfiguration**합니다. 모델 바인더 공급자는 모델 바인더를 만드는 팩터리 클래스 하기만 하면 됩니다. 파생 하 여 공급자를 만들 수는 [ModelBinderProvider](https://msdn.microsoft.com/library/system.web.http.modelbinding.modelbinderprovider.aspx) 클래스입니다. 그러나 단일 형식을 처리 하는 모델 바인더를 경우 기본 제공 사용 하기 쉽습니다 **SimpleModelBinderProvider**,이 목적을 위해 디자인 된 합니다. 다음 코드에서는 이 작업을 수행하는 방법을 보여 줍니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample12.cs)]

모델 바인딩 공급자에 추가 해야 합니다 **[ModelBinder]** 모델 바인더 및 없습니다 미디어 유형 포맷터를 사용 하도록 Web API를 구별 하는 매개 변수 특성입니다. 하지만 이제 모델 바인더의 형식 특성에 지정할 필요가 없습니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample13.cs)]

## <a name="value-providers"></a>값 공급자

모델 바인더 값 공급자에서 값을 언급 했습니다. 사용자 지정 값 공급자를 작성 하려면 구현 합니다 **IValueProvider** 인터페이스입니다. 요청에서 쿠키의 값을 가져오는 예제는 다음과 같습니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample14.cs)]

파생 하 여 값 공급자 팩터리를 생성 해야 합니다 **ValueProviderFactory** 클래스입니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample15.cs)]

값 공급자 팩터리를 추가 합니다 **HttpConfiguration** 다음과 같습니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample16.cs)]

Web API 이므로 모든 값 공급자를 작성 하는 모델 바인더를 호출 하는 경우 **ValueProvider.GetValue**, 모델 바인더를 만들 수 있는 첫 번째 값 공급자에서 값을 받습니다.

사용 하 여 매개 변수 수준에서 값 공급자 팩터리를 설정할 수는 또는 **ValueProvider** 특성을 다음과 같이 합니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample17.cs)]

이렇게 하면 Web API는 지정 된 값 공급자 팩터리를 사용 하 여 모델 바인딩을 사용 하려면 및 다른 등록 된 값 공급자를 사용할 수 없습니다.

## <a name="httpparameterbinding"></a>HttpParameterBinding

모델 바인더는 보다 일반적인 메커니즘의 특정 인스턴스. 보면 합니다 **[ModelBinder]** 특성을 보면 추상에서 파생 **ParameterBindingAttribute** 클래스입니다. 이 클래스는 단일 메서드를 정의 **GetBinding**를 반환 하는 **HttpParameterBinding** 개체:

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample18.cs)]

**HttpParameterBinding** 값으로 매개 변수를 바인딩할 담당 합니다. 경우 **[ModelBinder]**, 특성을 반환 합니다는 **HttpParameterBinding** 구현을 사용 하는 **IModelBinder** 실제 바인딩을 수행 합니다. 구현할 수도 있습니다 고유한 **HttpParameterBinding**합니다.

예를 들어, Etag에서 가져오려는 `if-match` 고 `if-none-match` 요청의 헤더입니다. Etag를 나타내는 클래스를 정의 하 여 시작 하겠습니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample19.cs)]

ETag를 가져옵니다을 여부를 나타내는 열거형도 정의 합니다 `if-match` 헤더 또는 `if-none-match` 헤더입니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample20.cs)]

다음은 **HttpParameterBinding** 원하는 헤더에서 ETag를 가져옵니다을 ETag 형식의 매개 변수를 바인딩합니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample21.cs)]

합니다 **ExecuteBindingAsync** 메서드 바인딩을 수행 하지 않습니다. 이 메서드 내에서 바인딩된 매개 변수 값을 추가 합니다 **ActionArgument** 사전에는 **HttpActionContext**합니다.

> [!NOTE]
> 경우에 **ExecuteBindingAsync** 메서드는 요청 메시지의 본문을 읽고, 재정의 **WillReadBody** 속성을 true를 반환 합니다. 요청 본문에만 읽을 수 있는 한 번, Web API 규칙을 시행 최대 하나의 바인딩 있도록 버퍼링 되지 않은 스트림을 메시지 본문을 읽을 수 수 있습니다.


사용자 지정을 적용할 **HttpParameterBinding**에서 파생 되는 특성을 정의할 수 있습니다 **ParameterBindingAttribute**합니다. 에 대 한 `ETagParameterBinding`에 대 한 두 가지 특성을 정의 하겠습니다 `if-match` 머리글과 프로그램용 `if-none-match` 헤더입니다. 둘 다 추상 기본 클래스에서 파생 됩니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample22.cs)]

같습니다. 사용 하는 컨트롤러 메서드는 `[IfNoneMatch]` 특성입니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample23.cs)]

외에 **ParameterBindingAttribute**에 사용자 지정을 추가 하는 것에 대 한 다른 후크 **HttpParameterBinding**합니다. 에 **HttpConfiguration** 개체를 **ParameterBindingRules** 속성은 컬렉션 형식의 anomymous 함수 (**HttpParameterDescriptor**  - &gt; **HttpParameterBinding**). 예를 들어, 모든 ETag 매개 변수는 GET 메서드를 사용 하는 규칙을 추가할 수 있습니다 `ETagParameterBinding` 사용 하 여 `if-none-match`:

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample24.cs)]

함수 반환 해야 `null` 매개 변수 바인딩이 적용 되지 않습니다.

## <a name="iactionvaluebinder"></a>IActionValueBinder

전체 매개 변수 바인딩 프로세스는 플러그형 서비스에 의해 제어 됩니다 **IActionValueBinder**합니다. 기본 구현의 **IActionValueBinder** 다음을 수행 합니다.

1. 검색할를 **ParameterBindingAttribute** 매개 변수입니다. 여기에 **[FromBody]** 를 **[FromUri]**, 및 **[ModelBinder]**, 또는 사용자 지정 특성입니다.
2. 찾는 위치이 고, 그렇지 **HttpConfiguration.ParameterBindingRules** null이 아닌 반환 하는 함수에 대 한 **HttpParameterBinding**합니다.
3. 앞서 설명 했 듯이 기본 규칙을 사용 하십시오. 

    - 매개 변수 형식을 "단순" 하거나 형식 변환기가, 경우에 URI에서 바인딩하십시오. 배치와 동일 합니다 **[FromUri]** 매개 변수에 특성입니다.
    - 그렇지 않은 경우 메시지 본문에서 매개 변수를 읽고 하려고 합니다. 배치 같습니다 **[FromBody]** 매개 변수입니다.

전체를 바꿀 수 있습니다 **IActionValueBinder** 사용자 지정 구현을 사용 하 여 서비스입니다.

## <a name="additional-resources"></a>추가 리소스

[사용자 지정 매개 변수 바인딩 샘플](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/CustomParameterBinding/ReadMe.txt)

Mike Stall Web API 매개 변수 바인딩에 대 한 적절 한 일련의 블로그 게시물을 작성:

- [어떻게 웹 API에는 매개 변수 바인딩](https://blogs.msdn.com/b/jmstall/archive/2012/04/16/how-webapi-does-parameter-binding.aspx)
- [웹 API에 대 한 MVC 스타일 매개 변수 바인딩](https://blogs.msdn.com/b/jmstall/archive/2012/04/18/mvc-style-parameter-binding-for-webapi.aspx)
- [작업 서명은 MVC/웹 API에서의 사용자 지정 개체에 바인딩하는 방법](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx)
- [Web API에서 사용자 지정 값 공급자를 만드는 방법](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)
- [내부에서 웹 API 매개 변수 바인딩](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx)
