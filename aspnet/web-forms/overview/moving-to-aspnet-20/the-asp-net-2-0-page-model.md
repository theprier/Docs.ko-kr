---
uid: web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
title: ASP.NET 2.0 페이지 모델 | Microsoft Docs
author: microsoft
description: ASP.NET에서 1.x 개발자가 인라인 코드 모델 및 코드 숨김 코드 모델 중에서 선택 했습니다. 코드 숨김의 Src attr 중 하나를 사용 하 여 구현할 수 있습니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2005
ms.topic: article
ms.assetid: af4575a3-0ae3-4638-ba4d-218fad7a1642
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
msc.type: authoredcontent
ms.openlocfilehash: fda85ec03f845cafa7720382bf85652937932c44
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30891297"
---
<a name="the-aspnet-20-page-model"></a>ASP.NET 2.0 페이지 모델
====================
by [Microsoft](https://github.com/microsoft)

> ASP.NET에서 1.x 개발자가 인라인 코드 모델 및 코드 숨김 코드 모델 중에서 선택 했습니다. 코드 숨김 Src 특성 또는 코드 숨김 특성을 사용 하 여 구현할 수는 @Page 지시문입니다. ASP.NET 2.0에서는 개발자가 인라인 코드 및 코드 숨김 사이 선택을 하지만 코드 숨김 모델을 크게 개선 되었습니다.


ASP.NET에서 1.x 개발자가 인라인 코드 모델 및 코드 숨김 코드 모델 중에서 선택 했습니다. 코드 숨김 Src 특성 또는 코드 숨김 특성을 사용 하 여 구현할 수는 @Page 지시문입니다. ASP.NET 2.0에서는 개발자가 인라인 코드 및 코드 숨김 사이 선택을 하지만 코드 숨김 모델을 크게 개선 되었습니다.

## <a name="improvements-in-the-code-behind-model"></a>코드 숨김 모델의 향상 된 기능

ASP.NET 2.0에서 코드 숨김 모델의 변경 내용을 완전히 이해 하기 위해 ASP.NET에서 신속 하 게 검토 되 모델 최적화 존재 1.x 합니다.

## <a name="the-code-behind-model-in-aspnet-1x"></a>Asp.net에서 코드 숨김 모델 1.x

ASP.NET에서 1.x, ASPX 파일 (Webform) 및 프로그래밍 코드를 포함 하는 코드 숨김 파일의 코드 숨김 모델 구성 되었습니다. 두 개의 파일이 사용 하 여 연결 된는 @Page ASPX 파일에 지시문입니다. 코드 숨김 파일에서 해당 선언을 인스턴스 변수로 포함 하는 ASPX 페이지에 있는 각 컨트롤입니다. 또한 코드 숨김 파일 이벤트 바인딩에 대 한 코드를 포함 하 고 Visual Studio 디자이너에 대 한 필요한 코드를 생성 합니다. 이 모델은 상당히를 잘 했지만 모든 ASP.NET 요소 ASPX 페이지에 코드 숨김 파일에 해당 코드가 필요 했으므로, 때문에 코드 및 콘텐츠와 true 분리할 수 없습니다. 예를 들어 디자이너 라는 새 서버 컨트롤이 Visual Studio IDE 외부은 ASPX 파일에 추가 하는 경우 응용 프로그램이 해당 컨트롤에 대 한 선언 없어서 코드 숨김 파일에 작동 하지 않으므로 합니다.

## <a name="the-code-behind-model-in-aspnet-20"></a>ASP.NET 2.0에서에서 코드 숨김 모델

ASP.NET 2.0이이 모델 크게 향상 시켰습니다. 사용 하 여 새 코드 숨김은 구현 하는 ASP.NET 2.0에서 *partial 클래스* ASP.NET 2.0에서 제공 합니다. ASP.NET 2.0에서 코드 숨김 클래스 클래스 정의의 일부분만 포함 되어 있는 것을 의미 하는 partial 클래스로 정의 됩니다. 클래스 정의의 남은 부분 런타임 시 또는 웹 사이트를 미리 컴파일된 ASPX 페이지를 사용 하 여 ASP.NET 2.0에 의해 동적으로 생성 됩니다. 코드 숨김 파일 및 ASPX 페이지 간 링크는 @ Page 지시문을 사용 하 여 여전히 설정 되어 있습니다. 그러나 코드 숨김 또는 Src 특성 대신 ASP.NET 2.0 이제 CodeFile는 특성을 사용 합니다. Inherits 특성 페이지에 대 한 클래스 이름을 지정할 수도 사용 됩니다.

일반적인 @ Page 지시문을 다음과 같이 표시 될 수 있습니다.

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample1.aspx)]

ASP.NET 2.0 코드 숨김 파일의 일반적인 클래스 정의 다음과 같이 표시 될 수 있습니다.

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample2.cs)]

> [!NOTE]
> C# 및 Visual Basic은 현재 partial 클래스를 지원만 관리 되는 언어는 합니다. 따라서 개발자 J#을 사용 하 여 ASP.NET 2.0에서 코드 숨김 모델을 사용할 수 있게 됩니다.


새 모델을 개발자가 작성 한 코드만 포함 하는 코드 파일 들은 이제 때문에 코드 숨김 모델을 향상 시킵니다. 또한 제공 코드와 콘텐츠를 true 분리에 대 한 코드 숨김 파일에서 인스턴스 변수 선언이 없으면 있기 때문입니다.

> [!NOTE]
> Partial 클래스 ASPX 페이지에 대 한 이벤트 바인딩을 일어나 이기 때문에 Visual Basic 개발자 이벤트에 바인딩할 코드 숨김에서 Handles 키워드를 사용 하 여 약간의 성능 향상을 인식할 수 있습니다. C#에 해당 하는 키워드가 없습니다.


## <a name="new--page-directive-attributes"></a>새로운 @ Page 지시문 특성

ASP.NET 2.0 @ Page 지시문에 많은 새 특성을 추가합니다. 다음 특성은 ASP.NET 2.0의 새로운 기능입니다.

## <a name="async"></a>Async

Async 특성을 사용 하면 비동기적으로 실행 되는 페이지를 구성할 수 있습니다. 이 모듈의 뒷부분에 나오는 비동기 페이지도 포함 합니다.

## <a name="asynctimeout"></a>AsyncTimeout

비동기 페이지에 대 한 제한 시간을 지정 합니다. 기본값은 45 초입니다.

## <a name="codefile"></a>CodeFile

CodeFile 특성은 Visual Studio 2002/2003에서 코드 숨김 파일 특성에 대 한 대체 합니다.

### <a name="codefilebaseclass"></a>CodeFileBaseClass

CodeFileBaseClass 특성은 하나의 기본 클래스에서 파생 되도록 여러 페이지를 원하는 경우에 사용 됩니다. 이 특성이 없으면 asp.net에서는 partial 클래스의 구현으로 인해 ASPX 페이지에 선언 된 컨트롤을 참조 하려면 공유 공통 필드를 사용 하는 기본 클래스는 제대로 작동 하지 때문에 ASP 합니다. 네트 컴파일 엔진의 페이지의 컨트롤에 따라 새 멤버를 자동으로 만들어집니다. 따라서 ASP.NET에서 두 개 이상의 페이지에 대 한 공통 기본 클래스를 원하는 할 경우를 정의 하는 CodeFileBaseClass 특성에 기본 클래스를 지정 하 고 각 페이지 클래스의 기본 클래스에서 파생 됩니다. CodeFile 특성은이 특성을 사용 하는 경우에 필요 합니다.

## <a name="compilationmode"></a>CompilationMode

이 특성을 사용 하면 ASPX 페이지의 CompilationMode 속성을 설정할 수 있습니다. CompilationMode 속성 값을 포함 하는 열거형은 **항상**, **자동**, 및 **Never**합니다. 기본값은 **항상**합니다. **자동** 설정에 따라 동적으로 페이지를 가능한 경우 컴파일에서 ASP.NET을 차단 합니다. 페이지를 제외 하 고 동적 컴파일에서 성능을 향상 시킵니다. 그러나 컴파일해야 하는 코드가 제외 된 페이지에 있는 경우 페이지를 찾아볼 때 오류가 throw 됩니다.

## <a name="enableeventvalidation"></a>EnableEventValidation

이 특성 포스트백 및 콜백 이벤트 한지 여부를 지정 합니다. 이 사용 하는 경우 원래 렌더링 되는 서버 컨트롤에서 발생 될 수 있도록 인수에 다시 게시 또는 콜백 이벤트 확인 됩니다.

## <a name="enabletheming"></a>EnableTheming

이 특성 페이지에서 ASP.NET 테마가 사용 되는지 여부를 지정 합니다. 기본값은 **false**입니다. ASP.NET 테마에 대해서는 설명 [모듈 10](profiles-themes-and-web-parts.md)합니다.

## <a name="linepragmas"></a>LinePragmas

이 특성 컴파일하는 동안 줄 pragma를 추가할지 여부를 지정 합니다. 줄 pragma은 코드의 특정 부분을 표시 하려면 디버거에서 사용 하는 옵션입니다.

## <a name="maintainscrollpositiononpostback"></a>MaintainScrollPositionOnPostback

이 특성 다시 게시 하는 스크롤 위치를 유지 하기 위해 JavaScript 페이지에 삽입 여부를 지정 합니다. 이 특성은 **false** 기본적으로 합니다.

이 특성이 **true**, ASP.NET 추가 됩니다 한 &lt;스크립트&gt; 다시 게시 될 때 다음과 같은 블록:

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample3.html)]

이 스크립트 블록에 대 한 src WebResource.axd 인지 확인 합니다. 이 리소스는 실제 경로가 아닙니다. 이 스크립트 요청 될 때 ASP.NET 스크립트를 동적으로 작성 합니다.

### <a name="masterpagefile"></a>MasterPageFile

이 특성의 현재 페이지에 대 한 마스터 페이지 파일을 지정합니다. 상대 또는 절대 경로일 수 있습니다. 마스터 페이지에 대해서는 설명 [모듈 4](master-pages.md)합니다.

## <a name="stylesheettheme"></a>StyleSheetTheme

이 특성을 사용 하면 ASP.NET 2.0 테마에 정의 된 사용자 인터페이스 모양 속성을 재정의할 수 있습니다. 테마에 대해서는 설명 [모듈 10](profiles-themes-and-web-parts.md)합니다.

## <a name="theme"></a>테마

페이지에 대 한 테마를 지정합니다. StyleSheetTheme 특성에 대 한 값을 지정 하지 않으면, 테마 특성 페이지에 있는 컨트롤에 적용 된 모든 스타일을 재정의 합니다.

## <a name="title"></a>제목

페이지의 제목을 설정합니다. 여기에 지정 된 값이 표시 됩니다는 &lt;제목&gt; 렌더링된 된 페이지의 요소입니다.

### <a name="viewstateencryptionmode"></a>ViewStateEncryptionMode

ViewStateEncryptionMode 열거형에 대 한 값을 설정합니다. 사용 가능한 값은 **항상**, **자동**, 및 **Never**합니다. 기본값은 **자동**합니다. 이 특성의 값으로 설정 된 경우 **자동**, viewstate를 암호화 하는 컨트롤에서 호출 하 여 요청 되는 **RegisterRequiresViewStateEncryption** 메서드.

## <a name="setting-public-property-values-via-the--page-directive"></a>공용 속성 값을 통해 @ Page 지시문

ASP.NET 2.0에서 @ Page 지시문의 새로운 기능으로 다른 기본 클래스의 공용 속성의 초기 값을 설정할 수 있다는 점입니다. 예를 들어 이라는 공용 속성이 있다고 가정 **SomeText** 기본 클래스 및 그 기입할 있습니다를 초기화할 **Hello** 페이지가 로드 될 때입니다. @ Page 지시문에 값을 설정 하면이 작업을 수행할 수 같이:

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample4.aspx)]

**SomeText** 를 기본 클래스에서 SomeText 속성의 초기 값을 설정 하는 @ Page 지시문 특성 *Hello!* 합니다. 아래 동영상은 @ Page 지시문을 사용 하 여 기본 클래스의 공용 속성의 초기 값을 설정할 때의 연습 과정입니다.


![](the-asp-net-2-0-page-model/_static/image1.png)


[전체 화면 비디오 열기](the-asp-net-2-0-page-model/_static/setprop1.wmv)


## <a name="new-public-properties-of-the-page-class"></a>새 공용 클래스의 속성 페이지

다음 공용 속성은 ASP.NET 2.0의 새로운 기능입니다.

## <a name="apprelativetemplatesourcedirectory"></a>AppRelativeTemplateSourceDirectory

페이지 또는 컨트롤에 응용 프로그램 상대 경로 반환합니다. 에 있는 페이지에 대 한 예를 들어 http://app/folder/page.aspx, 속성은 반환 ~ / 폴더/합니다.

## <a name="apprelativevirtualpath"></a>AppRelativeVirtualPath

페이지 또는 컨트롤에는 가상 디렉터리를 상대 경로 반환합니다. 에 있는 페이지에 대 한 예를 들어 http://app/folder/page.aspx, 속성은 반환 ~ / folder/page.aspx 합니다.

## <a name="asynctimeout"></a>AsyncTimeout

비동기 페이지 처리에 사용 되는 제한 시간을 가져오거나 설정 합니다. (비동기 페이지 살펴보겠습니다이 모듈의 뒷부분에 나오는.)

## <a name="clientquerystring"></a>ClientQueryString

요청된 된 URL의 쿼리 문자열 부분을 반환 하는 읽기 전용 속성입니다. 이 값은 URL로 인코딩됩니다. 디코딩해야 HttpServerUtility 클래스의 UrlDecode 메서드를 사용할 수 있습니다.

## <a name="clientscript"></a>ClientScript

이 속성에는 클라이언트 쪽 스크립트를 내보낼 ASP.NETs 관리를 사용할 수 있는 ClientScriptManager 개체를 반환 합니다. (ClientScriptManager 클래스는 나중에이 모듈에서에서 다룹니다.)

## <a name="enableeventvalidation"></a>EnableEventValidation

이 속성 포스트백 및 콜백 이벤트에 대 한 이벤트 유효성 검사를 활성화 하는 지 여부를 제어 합니다. 사용 하도록 설정 하면 원래 렌더링 되는 서버 컨트롤에서 발생 될 수 있도록 인수에 다시 게시 또는 콜백 이벤트 확인 됩니다.

## <a name="enabletheming"></a>EnableTheming

이 속성은 페이지에는 ASP.NET 2.0 테마 적용 여부를 지정 하는 부울을 가져오거나 설정 합니다.

## <a name="form"></a>Form

이 속성 htmlform에서 개체로 ASPX 페이지에서 HTML 폼을 반환합니다.

## <a name="header"></a>Header

이 속성 페이지 머리글을 포함 하는 HtmlHead 개체에 대 한 참조를 반환 합니다. Get/set 스타일 시트, 메타 태그를 반환된 된 HtmlHead 개체를 사용할 수 있습니다.

## <a name="idseparator"></a>IdSeparator

이 읽기 전용 속성은 ASP.NET 페이지에 있는 컨트롤에 대 한 고유 ID를 구성 하는 경우 컨트롤 식별자를 구분 하는 데 사용 되는 문자를 가져옵니다. 코드에서 직접 사용하기에 적합하지 않습니다.

## <a name="isasync"></a>IsAsync

이 속성에 대 한 비동기 페이지 있습니다. 비동기 페이지는이 모듈의 뒷부분에 설명 되어 있습니다.

## <a name="iscallback"></a>IsCallback

이 읽기 전용 속성은 반환 **true** 페이지가 다시 호출의 결과일 경우. 콜백은이 모듈의 뒷부분에 설명 되어 있습니다.

## <a name="iscrosspagepostback"></a>IsCrossPagePostBack

이 읽기 전용 속성은 반환 **true** 페이지는 페이지 간 다시 게시의 일부인 경우. 이 모듈의 뒷부분에 나오는 페이지 간 포스트백 다룹니다.

## <a name="items"></a>항목

페이지 컨텍스트에 저장 된 모든 개체가 포함 된 IDictionary 인스턴스에 대 한 참조를 반환 합니다. 이 IDictionary 개체에 항목을 추가할 수 있습니다 및 컨텍스트의 수명 내내 사용할 수 있습니다.

## <a name="maintainscrollpositiononpostback"></a>MaintainScrollPositionOnPostBack

이 속성은 ASP.NET 페이지에서 포스트백에서 발생 한 후 브라우저의 위치에에서 스크롤을 유지 하는 JavaScript를 내보내는 여부 제어 합니다. (이 속성의 세부 정보는이 모듈의 앞부분에 나오는 설명 했습니다.)

## <a name="master"></a>마스터

이 읽기 전용 속성 마스터 페이지 적용 된 페이지에 대 한 MasterPage 인스턴스에 대 한 참조를 반환 합니다.

## <a name="masterpagefile"></a>MasterPageFile

페이지에 대 한 마스터 페이지 파일 이름을 가져오거나 설정 합니다. 이 속성은 PreInit 메서드에만 설정할 수 있습니다.

## <a name="maxpagestatefieldlength"></a>MaxPageStateFieldLength

이 속성에는 바이트에서 페이지 상태에 대 한 최대 길이 설정 하거나 가져옵니다. 속성을 양수로, 페이지 보기 상태 손상 됩니다 여러 숨겨진된 필드에 지정 된 바이트 수를 초과 하지 않습니다. 속성이 음수 이면 보기 상태가 청크로 분할 되지 됩니다.

## <a name="pageadapter"></a>PageAdapter

요청 하는 브라우저에 대 한 페이지를 수정 하는 PageAdapter 개체에 대 한 참조를 반환 합니다.

## <a name="previouspage"></a>PreviousPage

에 Server.Transfer 또는 페이지 간 포스트백의 이전 페이지에 대 한 참조를 반환합니다.

## <a name="skinid"></a>SkinID

ASP.NET 2.0 적용할 스킨을 페이지에 지정 합니다.

## <a name="stylesheettheme"></a>StyleSheetTheme

이 속성 페이지에 적용 되는 스타일 시트를 가져오거나 설정 합니다.

## <a name="templatecontrol"></a>TemplateControl

페이지에 대 한 포함 하는 컨트롤에 대 한 참조를 반환합니다.

## <a name="theme"></a>테마

페이지에 적용 하는 ASP.NET 2.0 테마의 이름을 가져오거나 설정 합니다. 이 값은 PreInit 메서드 전에 설정 되어야 합니다.

## <a name="title"></a>제목

이 속성 가져오거나 페이지 머리글에서 가져온 대로 페이지의 제목을 설정 합니다.

## <a name="viewstateencryptionmode"></a>ViewStateEncryptionMode

페이지의 ViewStateEncryptionMode을 가져오거나 설정 합니다. 이 모듈의 앞부분에 나오는이 속성에 대 한 자세한 내용은 참조 하십시오.

## <a name="new-protected-properties-of-the-page-class"></a>보호 되는 속성 페이지 클래스의 새

ASP.NET 2.0에서 페이지 클래스의 새 보호 된 속성은 다음과 같습니다.

## <a name="adapter"></a>어댑터

요청 하는 장치에서 페이지를 렌더링 하는 ControlAdapter에 대 한 참조를 반환 합니다.

## <a name="asyncmode"></a>AsyncMode

이 속성 페이지를 비동기식으로 처리 되는지 여부를 나타냅니다. 것은 사용 하기 위해 런타임 및 코드에서 직접 하지 않습니다.

## <a name="clientidseparator"></a>ClientIDSeparator

이 속성은 컨트롤에 대 한 고유한 클라이언트 Id를 만들 때 구분 기호로 사용 되는 문자를 반환 합니다. 것은 사용 하기 위해 런타임 및 코드에서 직접 하지 않습니다.

## <a name="pagestatepersister"></a>PageStatePersister

이 속성 페이지에 대 한 PageStatePersister 개체를 반환합니다. 이 속성은 주로 컨트롤 개발자가 ASP.NET 사용 됩니다.

## <a name="uniquefilepathsuffix"></a>UniqueFilePathSuffix

이 속성의 파일 경로를 브라우저 캐시에 추가 되는 고유 suffic를 반환 합니다. 기본값은 \_ \_ufps = 및 6 자리 숫자입니다.

## <a name="new-public-methods-for-the-page-class"></a>Page 클래스에 대 한 새 공용 메서드

다음 공용 메서드는 ASP.NET 2.0에서 Page 클래스를 처음 사용 합니다.

## <a name="addonprerendercompleteasync"></a>AddOnPreRenderCompleteAsync

이 메서드는 비동기 페이지 실행에 대 한 이벤트 처리기 대리자를 등록합니다. 비동기 페이지는이 모듈의 뒷부분에 설명 되어 있습니다.

## <a name="applystylesheetskin"></a>ApplyStyleSheetSkin

페이지 스타일 시트의 속성 페이지에 적용 됩니다.

## <a name="executeregisteredasynctasks"></a>ExecuteRegisteredAsyncTasks

이 메서드가 존재 하는 비동기 작업입니다.

### <a name="getvalidators"></a>GetValidators

지정 하지 않으면 지정 된 유효성 검사 그룹 또는 기본 유효성 검사 그룹에 대 한 유효성 검사기의 컬렉션을 반환 합니다.

## <a name="registerasynctask"></a>RegisterAsyncTask

이 메서드는 새 비동기 작업을 등록합니다. 비동기 페이지는이 모듈 뒷부분에서 설명 됩니다.

## <a name="registerrequirescontrolstate"></a>RegisterRequiresControlState

이 메서드는 페이지 컨트롤 상태를 유지 해야 되도록 ASP.NET을 알려 줍니다.

## <a name="registerrequiresviewstateencryption"></a>RegisterRequiresViewStateEncryption

이 메서드는 페이지 viewstate 암호화를 요구 하는 ASP.NET을 지시 합니다.

## <a name="resolveclienturl"></a>ResolveClientUrl

이미지 등에 대 한 클라이언트 요청에 대해 사용할 수 있는 상대 URL을 반환 합니다.

## <a name="setfocus"></a>SetFocus

이 메서드는 페이지가 처음 로드 될 때 지정 된 컨트롤에 포커스를 설정 합니다.

## <a name="unregisterrequirescontrolstate"></a>UnregisterRequiresControlState

이 메서드는 더 이상 컨트롤 상태 지 속성을 필요로 하는 컨트롤로 전달 되는 컨트롤 등록을 취소 합니다.

## <a name="changes-to-the-page-lifecycle"></a>페이지 수명에 대 한 변경

ASP.NET 2.0의 페이지 수명 주기를 크게 변경 되지 않은 있지만 알고 있어야 하는 몇 가지 새로운 메서드가 있습니다. ASP.NET 2.0 페이지 수명 주기는 다음과 같습니다.

## <a name="preinit-new-in-aspnet-20"></a>(ASP.NET 2.0)의 새로운 PreInit

PreInit 이벤트에는 개발자가 액세스할 수 있는 수명 주기에서 최초의 단계입니다. 이 이벤트의 추가 액세스 등 ASP.NET 2.0 프로필에 대 한 속성을 프로그래밍 방식으로 ASP.NET 2.0 테마, 마스터 페이지 변경 수입니다. 다시 게시 상태를 해당 사실을 알아야 수명 주기에서이 시점에서 컨트롤에 Viewstate 아직 적용 되지 않습니다 사용 하는 경우. 따라서 개발자가이 단계에서 컨트롤의 속성이 변경 되 면 페이지 수명 주기의 뒷부분에 나오는 덮어씁니다 가능성이 됩니다.

## <a name="init"></a>Init

Init 이벤트 ASP.NET에서 변경 되지 않은 1.x 합니다. 읽거나 페이지에 컨트롤의 속성을 초기화 저장할 것입니다. 이 단계, 마스터 페이지, 테마에서 등의 페이지에 이미 적용 됩니다.

## <a name="initcomplete-new-in-20"></a>(2.0)의 새로운 InitComplete

InitComplete 이벤트 페이지 초기화 단계가 끝날 때 호출 됩니다. 이 시점에서 수명 주기에서 액세스할 수 페이지의 컨트롤에는 있지만 상태로 아직 채워지지 않았습니다.

## <a name="preload-new-in-20"></a>(2.0의 새로운) 미리 로드

이 이벤트는 모든 포스트백 데이터가 적용 된 후 및 페이지 바로 앞 이라고\_로드 합니다.

## <a name="load"></a>Load

Load 이벤트 ASP.NET에서 변경 되지 않은 1.x 합니다.

## <a name="loadcomplete-new-in-20"></a>(2.0)의 새로운 LoadComplete

LoadComplete 이벤트 페이지 로드 단계에서 마지막 이벤트가입니다. 이 단계에서는 모든 포스트백 및 viewstate 데이터 페이지에 적용 되었습니다.

## <a name="prerender"></a>PreRender

Viewstate를 페이지에 동적으로 추가 된 컨트롤에 대 한 제대로 유지 하려는 경우 PreRender 이벤트를 추가할 수 있는 마지막 기회입니다.

## <a name="prerendercomplete-new-in-20"></a>(2.0)의 새로운 PreRenderComplete

PreRenderComplete 단계에서 모든 컨트롤이 페이지에 추가 된 및 페이지는 렌더링할 수 있도록 준비 합니다. PreRenderComplete 이벤트 페이지 viewstate를 저장 하기 전에 발생 하는 마지막 이벤트가입니다.

## <a name="savestatecomplete-new-in-20"></a>(2.0)의 새로운 SaveStateComplete

모든 페이지 보기 상태 및 제어 상태 저장 한 후에 즉시 SaveStateComplete 이벤트 라고 합니다. 해당 페이지를 브라우저에 실제로 렌더링 하기 전에 마지막 이벤트입니다.

## <a name="render"></a>렌더링

Render 메서드는 ASP.NET 이후 변경 되지 않은 1.x 합니다. 이 여기서는 HtmlTextWriter 초기화 되 고 해당 페이지를 브라우저에 렌더링 합니다.

## <a name="cross-page-postback-in-aspnet-20"></a>ASP.NET 2.0에서에서 페이지 간 포스트백

ASP.NET에서 1.x 포스트백 된 동일한 페이지에 게시 하는 데 필요 합니다. 페이지 간 포스트백 허용 되지 않았습니다. ASP.NET 2.0 IButtonControl 인터페이스를 통해 서로 다른 페이지에 다시 게시 하는 기능을 추가 합니다. 새 IButtonControl 인터페이스 (예: 단추, LinkButton을 및 타사 사용자 지정 컨트롤 외에도 ImageButton)를 구현 하는 모든 컨트롤 PostBackUrl 특성의 사용을 통해이 새 기능을 이용을 걸릴 수 있습니다. 다음 코드는 두 번째 페이지에 다시 게시 하는 단추 컨트롤을 보여 줍니다.

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample5.aspx)]

페이지 다시 게시 되 면 페이지 포스트백을 시작 하는 두 번째 페이지 PreviousPage 속성을 통해 액세스할 수 됩니다. 이 기능은 새 WebForm를 통해 구현 됩니다\_DoPostBackWithOptions 클라이언트 쪽 함수는 컨트롤이 다른 페이지에 다시 게시 하는 경우 페이지에 렌더링 되는 ASP.NET 2.0입니다. 이 JavaScript 함수를 클라이언트에 대 한 스크립트를 내보내는 새 WebResource.axd 처리기에 의해 제공 됩니다.

아래 동영상은 페이지 간 포스트백의 연습 과정입니다.


![](the-asp-net-2-0-page-model/_static/image2.png)


[전체 화면 비디오 열기](the-asp-net-2-0-page-model/_static/xpage1.wmv)


## <a name="more-details-on-cross-page-postbacks"></a>페이지 간 포스트백에 대 한 자세한 내용

### <a name="viewstate"></a>Viewstate

질문 수도 있습니다는 직접 이미 페이지 간 다시 게시 시나리오의 첫 번째 페이지에서 viewstate의 진행 상황에 대 한. 즉, IPostBackDataHandler를 구현 하지 않는 모든 컨트롤에 유지 됩니다 viewstate 통해 상태 이므로 페이지 간 포스트백의 두 번째 페이지에서 해당 컨트롤의 속성에 대 한 액세스 권한이, viewstate 페이지에 대 한 액세스 권한이 있어야 합니다. ASP.NET 2.0 라는 두 번째 페이지에 있는 새 숨겨진된 필드를 사용 하 여이 시나리오는 담당 \_ \_PREVIOUSPAGE 합니다. \_ \_PREVIOUSPAGE 양식 필드 포함 viewstate 첫 번째 페이지에 대 한 두 번째 페이지에서 모든 컨트롤의 속성에 대 한 액세스를 가질 수 있습니다.

### <a name="circumventing-findcontrol"></a>FindControl을 회피

페이지 간 포스트백 연습 비디오 FindControl 메서드를 사용 하려면를 첫 번째 페이지에 TextBox 컨트롤에 대 한 참조를 가져옵니다. 해당 메서드에 해당 용도에 적합 하지만 FindControl 상당히 소모 되며 필요한 추가 코드를 작성 합니다. 다행히 ASP.NET 2.0 다양 한 시나리오에서 작동 하는이 목적을 위해 FindControl에 대 한 대안을 제공 합니다. PreviousPageType 지시문을 사용 하면 TypeName 또는 VirtualPath 특성 중 하나를 사용 하 여 이전 페이지에 대 한 강력한 형식의 참조는 포함할 수 있습니다. TypeName 특성을 사용 하면 VirtualPath 특성을 사용 하면 가상 경로 사용 하 여 이전 페이지를 참조 하는 동안에 이전 페이지의 종류를 지정할 수 있습니다. PreviousPageType 지시문을 설정한 후 컨트롤, 등 공용 속성을 사용 하 여 액세스를 허용 하려면 다음 노출 해야 합니다.

## <a name="lab-1-cross-page-postback"></a>랩 1 페이지 간 포스트백

이 랩의 경우 ASP.NET 2.0의 새로운 페이지 간 다시 게시 기능을 사용 하는 응용 프로그램에 만들어집니다.

1. Visual Studio 2005를 열고 새 ASP.NET 웹 사이트를 만듭니다.
2. Page2.aspx 라는 새 Webform를 추가 합니다.
3. 디자인 보기에서 Default.aspx를 열고 단추 컨트롤과 TextBox 컨트롤을 추가 합니다. 

    1. 단추 컨트롤의 ID를 부여 **제출 단추** TextBox 컨트롤의 ID 및 **UserName**합니다.
    2. 단추의 PostBackUrl 속성 page2.aspx을 설정 합니다.
4. 소스 뷰에서 page2.aspx를 엽니다.
5. 아래와 같이 @ PreviousPageType 지시문을 추가 합니다.
6. 페이지에 다음 코드를 추가\_page2.aspx의 코드 숨김의 부하: 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample6.cs)]
7. 빌드 메뉴에서 빌드에 클릭 하 여 프로젝트를 빌드하십시오.
8. Default.aspx에 대 한 코드 숨김에 다음 코드를 추가 합니다. 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample7.cs)]
9. 페이지 변경\_다음과 page2.aspx에 로드 합니다. 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample8.cs)]
10. 프로젝트를 빌드합니다.
11. 프로젝트를 실행합니다.
12. 텍스트 상자에 이름을 입력 하 고 단추를 클릭 합니다.
13. 결과 무엇입니까?

## <a name="asynchronous-pages-in-aspnet-20"></a>ASP.NET 2.0에서에서 비동기 페이지

ASP.NET에서 대부분의 경합 문제는 외부 호출 (예: 웹 서비스 또는 데이터베이스 호출), 파일 IO 대시 시간 등의 지연이 발생 합니다. 에 ASP.NET 응용 프로그램에 대해 요청이 수행 ASP.NET 해당 요청을 처리할 작업자 스레드 중 하나를 사용 합니다. 요청이 완료 되 고 응답을 보낸 될 때까지 해당 스레드를 소유 하는 해당 요청 합니다. ASP.NET 2.0 사항은 페이지를 비동기적으로 실행할 수 있는 기능을 추가 하 여 대기 시간 문제 이러한 유형의 문제를 해결 하는 것입니다. 즉, 작업자 스레드가 요청을 시작 하 고 신속 하 게 사용할 수 있는 스레드 풀으로 반환 되므로 다른 스레드로 추가 실행에 게 제공할 수 있습니다. 파일 IO, 데이터베이스 호출 등이 완료 되 면 새 스레드 요청을 완료 하기 스레드 풀에서 가져옵니다.

설정 하는 비동기 방식으로 실행 하는 페이지의 첫 단계는 **비동기** 같이 page 지시문의 특성:

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample9.aspx)]

이 특성은 페이지에 대해 내부적으로 지시 합니다.

다음 단계 PreRender 이전 페이지의 수명 주기에서 시점 AddOnPreRenderCompleteAsync 메서드를 호출 하는 것입니다. (이 메서드는 일반적으로 페이지에서 호출\_로드 합니다.) AddOnPreRenderCompleteAsync 메서드를 사용 하며 두 개의 매개 변수입니다. BeginEventHandler 및는 EndEventHandler 합니다. BeginEventHandler는 EndEventHandler를 매개 변수로 전달 되는 IAsyncResult를 반환 합니다.

아래 동영상은 비동기 페이지 요청의 연습 과정입니다.


![](the-asp-net-2-0-page-model/_static/image3.png)


[전체 화면 비디오 열기](the-asp-net-2-0-page-model/_static/async1.wmv)


> [!NOTE]
> EndEventHandler 완료 된 비동기 페이지를 브라우저에 렌더링 하지 않습니다. 의심 했지만 일부 개발자는 비동기 요청을 비동기 콜백을 유사한 것으로 생각 됩니다. 않은지를 나타내려고 하는 것이 유용 합니다. 비동기 요청에 기능은 첫 번째 작업자 스레드 등 바인딩된 IO 되지 않았으므로 경합이 줄어듭니다 새 서비스 요청을 스레드 풀만 반환 될 수 있습니다.


## <a name="script-callbacks-in-aspnet-20"></a>ASP.NET 2.0에서에서 콜백 스크립트

항상 웹 개발자는 콜백과와 관련 된 깜박임 방지 하는 방법에 대 한를 찾습니다. ASP.NET에서 1.x SmartNavigation 깜박임를 방지 하기 위한 가장 일반적인 방법은 했지만 SmartNavigation 클라이언트에는 구현의 복잡성으로 인해 일부 개발자 들에 대 한 문제가 발생 합니다. ASP.NET 2.0 스크립트 콜백과 함께이 문제를 해결합니다. 스크립트 콜백을 XMLHttp JavaScript 통해 웹 서버에 대 한 요청을 사용 합니다. XMLHttp 요청 브라우저의 DOM.를 통해 다음 조작할 수 있는 XML 데이터를 반환 합니다. XMLHttp 코드는 사용자 로부터 새 WebResource.axd 처리기에 의해 숨겨져 있습니다.

ASP.NET 2.0에서 콜백 스크립트를 구성 하는 데 필요한 몇 가지 단계가 있습니다.

## <a name="step-1--implement-the-icallbackeventhandler-interface"></a>1 단계: ICallbackEventHandler 인터페이스를 구현 합니다.

스크립트 콜백에 참여 하 여 페이지 인식 하기 위해 ASP.NET에서 ICallbackEventHandler 인터페이스를 구현 해야 합니다. 코드 숨김 파일에서 이렇게 하려면 다음과 같이 합니다.

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample10.cs)]

또한 이렇게 하려면 하므로 @ Implements 지시문 like를 사용 하 여:

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample11.aspx)]

일반적으로 인라인 ASP.NET 코드를 사용 하는 경우에 @ Implements 지시문을 사용 합니다.

## <a name="step-2--call-getcallbackeventreference"></a>2 단계: GetCallbackEventReference 호출

앞에서 설명한 대로 XMLHttp 호출 WebResource.axd 처리기에 캡슐화 됩니다. ASP.NET WebForm에 대 한 호출을 추가 합니다 페이지를 렌더링할 때\_DoCallback, WebResource.axd에서 제공 되는 클라이언트 스크립트입니다. WebForm\_DoCallback 함수 대체는 \_ \_doPostBack 함수는 콜백에 대 한 합니다. 에 유의 해야 \_ \_doPostBack 페이지에서 폼을 프로그래밍 방식으로 전송 합니다. 따라서에서 포스트백을 방지 하려면 콜백 시나리오에서 \_ \_doPostBack 적절 하지 것입니다.

> [!NOTE]
> \_\_doPostBack은 클라이언트 스크립트 콜백 시나리오의 페이지에 계속 렌더링 됩니다. 그러나 콜백에 대 한 사용 되지 않습니다.


인수는 WebForm\_DoCallback 클라이언트 쪽 함수는 서버 쪽 기능 GetCallbackEventReference 페이지에서 정상적으로 호출을 통해 제공 됩니다\_로드 합니다. GetCallbackEventReference 호출을 다음과 같이 표시 될 수 있습니다.

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample12.cs)]

> [!NOTE]
> 이 경우 cm는 ClientScriptManager의 인스턴스입니다. 이 모듈의 뒷부분에 나오는 ClientScriptManager 클래스를 설명 합니다.


GetCallbackEventReference의 몇 가지 오버 로드 된 버전이 있습니다. 이 경우 인수는 다음과 같습니다.

`this`

GetCallbackEventReference 호출 되는 컨트롤에 대 한 참조입니다. 이 경우,이 페이지 자체입니다.

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample13.js)]

서버 쪽 이벤트를 클라이언트 코드에서 전달 되는 문자열 인수입니다. 이 경우의 드롭다운 값을 전달 하는 Im ddlCompany 호출 됩니다.

`ShowCompanyName`

서버 쪽 콜백 이벤트에서 반환 값 (문자열)으로 허용 하는 클라이언트 쪽 함수의 이름. 이 함수는 서버 쪽 콜백에 성공할 경우에 호출 됩니다. 따라서 견고성을 위해 오류 발생 시 실행 하는 클라이언트 쪽 함수 이름을 지정 하는 추가 문자열 인수를 사용 하는 GetCallbackEventReference의 오버 로드 된 버전을 사용 하도록 좋습니다 일반적으로 됩니다.

`null`

서버에는 콜백 전에 시작 된 클라이언트 쪽 함수를 나타내는 문자열입니다. 이 경우가 해당 스크립트가 없습니다. 인수가 null입니다.

`true`

콜백을 비동기적으로 수행 여부를 지정 하는 부울입니다.

WebForm에 대 한 호출\_DoCallback 클라이언트에서 이러한 인수를 전달 합니다. 따라서 클라이언트에서이 페이지를 렌더링할 때 해당 코드는 같습니다 같이:

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample14.js)]

클라이언트에서 함수의 서명이 약간 다르게 표시 됩니다. 클라이언트 쪽 함수는 5 개 문자열 및 부울 값을 전달합니다. 서버 쪽 콜백이 발생 하는 오류를 처리 하는 클라이언트 쪽 함수를 포함 하는 추가 문자열 (위의 예제에서 null은)이 표시를 합니다.

## <a name="step-3--hook-the-client-side-control-event"></a>3 단계: 클라이언트 쪽 컨트롤 이벤트를 후크

위의 GetCallbackEventReference의 반환 값을 문자열 변수에 할당 된를 확인 합니다. 해당 문자열이 콜백을 시작 하는 컨트롤에 대 한 클라이언트 쪽 이벤트를 후크 하는 데 사용 됩니다. 이 예제에서는 콜백이 시작 페이지에서 드롭다운 이므로 연결 하고자 하는 경우는 *OnChange* 이벤트입니다.

연결할 클라이언트측 이벤트 처리기를 클라이언트 쪽 태그를 다음과 같이 추가:

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample15.cs)]

이전에 설명한 대로 *cbRef* GetCallbackEventReference에 대 한 호출에서 반환 값입니다. WebForm에 대 한 호출을 포함\_위에 나온 DoCallback 합니다.

## <a name="step-4--register-the-client-side-script"></a>4 단계: 클라이언트 쪽 스크립트를 등록 합니다.

회수 GetCallbackEventReference에 대 한 호출 클라이언트 쪽 스크립트에 호출 되도록 지정 **ShowCompanyName** 하면 서버 쪽 콜백 성공할 때 실행할 수 있습니다. 해당 스크립트 ClientScriptManager 인스턴스를 사용 하 여 페이지에 추가 해야 합니다. (ClientScriptManager 클래스에이 모듈의 뒷부분에 나오는 표에서 수 있습니다.) 해당 같은 지금 수행합니다.

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample16.js)]

## <a name="step-5--call-the-methods-of-the-icallbackeventhandler-interface"></a>5 단계: ICallbackEventHandler 인터페이스의 메서드를 호출 합니다.

ICallbackEventHandler 코드에서 구현 해야 하는 두 개의 메서드를 포함 합니다. 이들은 **RaiseCallbackEvent** 및 **GetCallbackEvent**합니다.

**RaiseCallbackEvent** 인수로 문자열을 nothing을 반환 합니다. WebForm 클라이언트 호출에서 문자열 인수가 전달 되었습니다\_DoCallback 합니다. 이 경우 해당 값은는 *값* 특성 ddlCompany 라는 드롭다운입니다. 서버 쪽 코드 RaiseCallbackEvent 메서드에 배치 해야 합니다. 예를 들어 콜백은 외부 리소스에 대해 WebRequest를 하는 경우 해당 코드 RaiseCallbackEvent에 배치 해야 합니다.

**GetCallbackEvent** 을 클라이언트에 콜백 반환을 처리 합니다. 인수를 받지 않는 하 고 문자열을 반환 합니다. 반환 되는 문자열 전달 됩니다 인수로 서 클라이언트 쪽 함수에이 예에서 *ShowCompanyName*합니다.

위의 단계를 완료 후 스크립트 콜백을 수행 하 여 ASP.NET 2.0에서 준비가 되었습니다.


![](the-asp-net-2-0-page-model/_static/image4.png)


[전체 화면 비디오 열기](the-asp-net-2-0-page-model/_static/callback1.wmv)


ASP.NET에서 콜백 스크립트는 함으로써 XMLHttp 호출을 지 원하는 모든 브라우저에서 지원 됩니다. 포함 된 모든 최신 브라우저 사용 하 여 오늘날. Internet Explorer (예정 된 IE 7 포함) 다른 최신 브라우저 내장 XMLHttp 개체를 사용 하는 동안 XMLHttp ActiveX 개체를 사용 합니다. 프로그래밍 방식으로 사용할 수 있는 브라우저 콜백을 지 원하는 경우를 결정 하는 **Request.Browser.SupportCallback** 속성입니다. 이 속성은 반환 **true** 요청 하는 클라이언트 스크립트 콜백을 지 원하는 경우.

## <a name="working-with-client-script-in-aspnet-20"></a>ASP.NET 2.0에서에서 클라이언트 스크립트 작업

ASP.NET 2.0에서 클라이언트 스크립트 ClientScriptManager 클래스의 용도 통해 관리 됩니다. 형식과 이름을 사용 하 여 클라이언트 스크립트 ClientScriptManager 클래스는 추적입니다. 이렇게 하면 동일한 스크립트를 두 번 이상 삽입 페이지에 프로그래밍 방식으로 되지 않습니다.

> [!NOTE]
> 스크립트를 페이지에 성공적으로 등록 된 후 스크립트를 두 번째로 등록 되었을 단순히 후속 동일한 스크립트를 등록 하려고가 됩니다. 중복 된 스크립트가 추가 되 고 예외가 발생 하지 않으면. 불필요 한 계산을 방지 하려면 두 번 이상 등록 하지 마십시오 하는 스크립트가 이미 등록 되었는지 확인 하는 데 사용할 수 있는 메서드가 있습니다.


ClientScriptManager의 메서드는 모든 현재 ASP.NET 개발자에 게 잘 알고 있어야 합니다.

## <a name="registerclientscriptblock"></a>RegisterClientScriptBlock

이 메서드는 렌더링 된 페이지의 맨 위에 스크립트를 추가합니다. 클라이언트에서 명시적으로 호출 될 함수를 추가 하는 데 유용 합니다.

이 메서드의 두 오버 로드 된 버전이 있습니다. 4 개 인수 중 3 개는 해당 간에 공통적으로 적용 합니다. 다음 창이 여기에 포함됩니다.

`type (string)`

***형식*** 인수는 스크립트에 대 한 유형을 식별 합니다. 일반적으로 것이 좋습니다 (이 페이지의 형식을 사용 하려면입니다. 유형에 대 한 GetType()) 합니다.

`key (string)`

***키*** 인수는 스크립트에 대 한 사용자 정의 키입니다. 각 스크립트에 대해 고유 해야 합니다. 동일한 키 및 이미 추가 된 스크립트 유형을 사용 하 여 스크립트를 추가 하려고 하면 추가 되지 않습니다.

`script (string)`

***스크립트*** 인수는 실제 스크립트 추가를 포함 하는 문자열입니다. 스크립트를 만들고 다음를 할당 하려면 StringBuilder에 tostring () 메서드를 사용 하는 StringBuilder를 사용 하는 것이 좋습니다.는 ***스크립트*** 인수입니다.

Script 요소를 포함 해야만 세 개의 인수를 받아들이는 오버 로드 된 RegisterClientScriptBlock를 사용 하는 경우 (&lt;스크립트&gt; 및 &lt;/script&gt;) 스크립트에 있습니다.

RegisterClientScriptBlock 네 번째 인수를 받아들이는 오버 로드를 사용 하도록 선택할 수 있습니다. 네 번째 인수에는 ASP.NET 드립니다 script 요소를 추가할지 여부를 지정 하는 부울입니다. 이 인수가 **true**, 스크립트는 스크립트 요소 명시적으로 합니다.

스크립트를 이미 등록 되었는지 확인 하려면 IsClientScriptBlockRegistered 메서드를 사용 합니다. 이렇게 하면 이미 등록 되어 있는 스크립트를 다시 등록 하는 시도 방지할 수 있습니다.

### <a name="registerclientscriptinclude-new-in-20"></a>(2.0)의 새로운 RegisterClientScriptInclude

RegisterClientScriptInclude 태그 외부 스크립트 파일에 연결 되는 스크립트 블록을 만듭니다. 두 오버 로드를가지고 있습니다. 하나는 키와 URL을 사용합니다. 두 번째 유형을 지정 하는 세 번째 인수를 추가 합니다.

예를 들어 다음 코드에서는 스크립트 블록 jsfunctions.js에 연결 되는 응용 프로그램의 스크립트 폴더의 루트에서:

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample17.cs)]

이 코드는 렌더링 된 페이지에 다음 코드를 생성합니다.

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample18.html)]

> [!NOTE]
> 스크립트 블록은 페이지 아래쪽에 렌더링 됩니다.


스크립트를 이미 등록 되었는지 확인 하려면 IsClientScriptIncludeRegistered 메서드를 사용 합니다. 이렇게 하면 스크립트를 다시 등록 하는 시도 방지할 수 있습니다.

## <a name="registerstartupscript"></a>RegisterStartupScript

RegisterStartupScript 메서드가 RegisterClientScriptBlock 방법으로 동일한 인수를 사용 합니다. 등록 된 RegisterStartupScript 스크립트 페이지가 로드 하기 전에 실행 OnLoad 클라이언트 쪽 이벤트입니다. 1.X 등록 RegisterStartupScript 된 스크립트는 닫는 직전 배치 된 &lt;/f&gt; 등록 된 RegisterClientScriptBlock 스크립트 열기 바로 뒤에 배치 된 동안 태그 &lt;양식&gt; 태그입니다. ASP.NET 2.0에서는 닫는 직전 배치 됩니다 둘 다 &lt;/f&gt; 태그입니다.

> [!NOTE]
> RegisterStartupScript와 함수를 등록 하는 경우 클라이언트 코드에서 명시적으로 호출 될 때까지 해당 함수가 실행 되지 않습니다.


스크립트를 이미 등록 되었는지 확인 하는 스크립트를 다시 등록 하려고를 방지 하려면 IsStartupScriptRegistered 메서드를 사용 합니다.

## <a name="other-clientscriptmanager-methods"></a>다른 ClientScriptManager 메서드

다음은 ClientScriptManager 클래스의 다른 유용한 메서드 중 일부입니다.


|  <strong>GetCallbackEventReference</strong>   |                                                 이 모듈의 앞부분에 나오는 스크립트 콜백을 참조 하십시오.                                                 |
|-----------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
|  <strong>GetPostBackClientHyperlink</strong>  |                JavaScript 참조를 가져옵니다 (javascript:&lt;호출&gt;) 클라이언트 쪽 이벤트에서 다시 게시 하려면 사용할 수 있는 합니다.                 |
|  <strong>GetPostBackEventReference</strong>   |                                   클라이언트에서 다시 게시를 시작 하려면 사용할 수 있는 문자열을 가져옵니다.                                    |
|      <strong>GetWebResourceUrl</strong>       | 어셈블리에 포함 된 리소스에 대 한 URL을 반환 합니다. 와 함께에서 사용 해야 <strong>RegisterClientScriptResource</strong>합니다. |
| <strong>RegisterClientScriptResource</strong> |     페이지와 웹 리소스를 등록합니다. 이들은 새 WebResource.axd 처리기에서 처리 및 어셈블리에 포함 된 리소스입니다.      |
|     <strong>RegisterHiddenField</strong>      |                                                 페이지와 숨겨진된 양식 필드를 등록합니다.                                                 |
|  <strong>RegisterOnSubmitStatement</strong>   |                                  HTML 폼이 전송 될 때 실행 되는 클라이언트 쪽 코드를 등록 합니다.                                   |

