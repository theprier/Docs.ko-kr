---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-partial-page-updates-with-asp-net-ajax
title: ASP.NET AJAX와 함께 부분 페이지 업데이트 이해 | Microsoft Docs
author: scottcate
description: 아마도 가장 눈에 띄는 ASP.NET AJAX Extensions의 기능은 t에 대 한 전체 포스트백을 수행 하지 않고 증분 또는 부분 페이지 업데이트를 수행 하는 기능 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/28/2008
ms.topic: article
ms.assetid: 54d9df99-1161-4899-b4e8-2679c85915e7
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-partial-page-updates-with-asp-net-ajax
msc.type: authoredcontent
ms.openlocfilehash: 91a98bf1c9a71ae84c569f7ae40930422cb652e0
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="understanding-partial-page-updates-with-aspnet-ajax"></a>ASP.NET AJAX와 함께 이해 부분 페이지 업데이트
====================
으로 [Scott 인증서](https://github.com/scottcate)

[PDF 다운로드](http://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial01_Partial_Page_Updates_cs.pdf)

> 아마도 ASP.NET AJAX 확장의 가장 눈에 띄는 기능은는 최소한의 태그 변경 없고 코드 변경 내용을 서버에 대 한 전체 포스트백을 수행 하지 않고 증분 또는 부분 페이지 업데이트를 수행 하는 기능입니다. 장점은 광범위 한 – 프로그램 멀티미디어 (예: Adobe Flash 또는 Windows Media)의 상태가 변경 된, 대역폭 비용을 감소 및 클라이언트 포스트백을 통해 일반적으로 관련 깜빡임을 발생 하지 않습니다.


## <a name="introduction"></a>소개

Microsoft의 ASP.NET 기술을 개체 지향 및 이벤트 기반 프로그래밍 모델을 가져오며 컴파일된 코드의 장점을 함께 결합 합니다. 그러나 피어 채널의 서버 쪽 처리 모델에는 기술에 내재 된 몇 가지 단점이 있습니다.

- 페이지 업데이트 하려면 페이지 새로 고침 하는 서버에 대 한 라운드트립이 필요 합니다.
- 왕복은 Javascript 또는 다른 클라이언트 기술 (예: Adobe Flash)에 의해 생성 된 영향이 유지 되지 않습니다.
- 다시 게시 하는 동안 Microsoft Internet Explorer 이외의 브라우저를 지원 하지 않습니다는 스크롤 위치를 자동으로 복원. 않으며 Internet Explorer에도 여전히 깜빡임 대로 페이지가 새로 고쳐집니다.
- 포스트백에는 많은 양의 대역폭으로 포함 될 수 있습니다는 \_ \_GridView 컨트롤 또는 반복기 등의 컨트롤로 처리할 때 VIEWSTATE 양식 필드 증가할 수 있습니다.
- JavaScript 또는 기타 클라이언트 쪽 기술을 통해 웹 서비스에 액세스 하기 위한 통합 된 모델이 있습니다.

Microsoft의 ASP.NET AJAX 확장명을 입력 합니다. 에 AJAX **A** 동기 **J** avaScript **A** nd **X** ML는 증분 페이지를 제공 하기 위한 통합 된 프레임 워크 플랫폼 간 JavaScript 통해 업데이트를 구성 하는 Microsoft AJAX Framework 및 Microsoft AJAX 스크립트 라이브러리를 호출 하는 스크립트 구성 요소를 구성 하는 서버 쪽 코드. ASP.NET AJAX extensions JavaScript 통해 ASP.NET 웹 서비스에 액세스 하기 위한 플랫폼 간 지원도 제공 합니다.

이 백서와에 ScriptManager 구성 요소가, UpdatePanel 컨트롤 및 UpdateProgress 제어를 포함 해야 하거나 되지 않아야 하는 시나리오를 고려 하는 ASP.NET AJAX 확장에의 부분 페이지 업데이트 기능 검사 사용 됩니다.

이 백서 최종 릴리스는 Visual Studio 2008의 및 ASP.NET AJAX Extensions (있던 이전에 ASP.NET 2.0에 사용할 수 있는 추가 기능 구성 요소) 기본 클래스 라이브러리에 통합 하는.NET Framework 3.5를 기반으로 합니다. 이 백서는 또한를 사용 하는 Visual Studio 2008 및 하지 Visual Web Developer Express Edition; 가정 참조 되는 일부 프로젝트 템플릿은 Visual Web Developer Express 사용자에 게 하지 못할 수 있습니다.

## <a name="partial-page-updates"></a>부분 페이지 업데이트

아마도 ASP.NET AJAX 확장의 가장 눈에 띄는 기능은는 최소한의 태그 변경 없고 코드 변경 내용을 서버에 대 한 전체 포스트백을 수행 하지 않고 증분 또는 부분 페이지 업데이트를 수행 하는 기능입니다. 장점은 광범위 한-프로그램 멀티미디어 (예: Adobe Flash 또는 Windows Media)의 상태가 변경 된, 대역폭 비용을 감소 및 클라이언트는 일반적으로 관련 다시 게시 된 깜빡임 발생 하지 않습니다.

부분 페이지 렌더링을 통합 하는 기능 ASP.NET에 최소한의 변경 내용을 프로젝트에 통합 되어 있습니다.

## <a name="walkthrough-integrating-partial-rendering-into-an-existing-project"></a>연습: 부분 렌더링을 기존 프로젝트에 통합


1. Microsoft Visual Studio 2008에서으로 이동 하 여 새 ASP.NET 웹 사이트 프로젝트를 만듭니다 <em>파일</em>  <em>- &gt; 새로</em>  <em>- &gt; 웹사이트</em> 대화 상자에서 ASP.NET 웹 사이트를 선택 하 고 있습니다. 이름을 지정할 수 있습니다이 든 및 파일 시스템 또는 인터넷 정보 서비스 (IIS)에 설치할 수 있습니다.
2. 기본 ASP.NET 태그와 빈 기본 페이지가 표시 됩니다 (서버 쪽 폼 및 `@Page` 지시문). 라는 레이블을 삭제 `Label1` 단추 호출 `Button1` form 요소 안에 페이지로 끌어다 놓습니다. 원하는를 해당 텍스트 속성을 설정할 수 있습니다.
3. 디자인 보기에서 두 번 클릭 `Button1` 코드 숨김 이벤트 처리기를 생성 합니다. 이 이벤트 처리기 내에서 설정할 `Label1.Text` 에 단추를 클릭 하면! 이어야 합니다.

**부분 렌더링이 활성화 하기 전에 default.aspx에 대 한 태그 목록 1:**

[!code-aspx[Main](understanding-partial-page-updates-with-asp-net-ajax/samples/sample1.aspx)]

**Default.aspx.cs에서 (잘립니다) 목록 2: 코드 숨김**

[!code-csharp[Main](understanding-partial-page-updates-with-asp-net-ajax/samples/sample2.cs)]

1. F5 키를 눌러 웹 사이트를 시작 합니다. Visual Studio; 디버깅할 수 있도록 web.config 파일을 추가 하 라는 메시지가 나타납니다. 이렇게 해야 합니다. 단추를 클릭할 때는 레이블 텍스트를 변경 하려면 페이지가 새로 고쳐지고을 페이지 다시 그려지는 경우와 간략 한 깜박임 하는 방식을 살펴봅니다.
2. 브라우저 창을 닫은 후, Visual Studio를 태그 페이지를 반환 합니다. Visual Studio 도구 상자에서 아래로 스크롤하여 AJAX 확장명 탭을 찾습니다. (AJAX 또는 Atlas 확장의 이전 버전을 사용 하 고 있으므로이 탭 없는,이 백서에서는 뒷부분에 나오는 AJAX 확장 도구 상자 항목을 등록 하기 위한 연습을 참조 하거나 현재 버전을 다운로드할 수 있는 경우 Windows installer 설치 웹 사이트에서).


[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image2.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image1.png)

([전체 크기 이미지를 보려면 클릭](understanding-partial-page-updates-with-asp-net-ajax/_static/image3.png))


1. <em>알려진된 문제:</em>ASP.NET 2.0 AJAX 확장와 함께 설치 된 Visual Studio 2005이 이미 있는 컴퓨터에 Visual Studio 2008을 설치 하는 경우 Visual Studio 2008에서 AJAX 확장 도구 상자 항목을 가져옵니다. 구성 요소;의 도구 설명을 검사 하 여 대/소문자 인지를 확인할 수 있습니다. 버전 3.5.0.0 이제 합니다. 버전 2.0.0.0 야 말로 하는 경우 다음가 오래 된 도구 상자 항목을 가져와서 Visual Studio에서 도구 상자 항목 선택 대화 상자를 사용 하 여이 수동으로 가져오는 필요 합니다. 디자이너를 통해 버전 2 컨트롤을 추가할 수 없습니다.

2. 전에 `<asp:Label>` 태그 시작 공백, 줄 만들고 도구 상자에서 UpdatePanel 컨트롤을 두 번 클릭 합니다. 새 `@Register` 지시어를 사용 하 여 컨트롤 System.Web.UI 네임 스페이스 내에서 가져와야 하는지 나타내는 페이지의 맨 아래에 포함 되어는 `asp:` 접두사입니다.
3. 닫는 끌어 `</asp:UpdatePanel>` 래핑된 레이블 및 단추 컨트롤 요소를 제대로 구성 된 있도록 Button 요소 끝을 지나서 태그입니다.
4. 에서는 여 `<asp:UpdatePanel>` 태그, 여는 새 태그를 시작 합니다. 참고는 IntelliSense 묻는 메시지를 두 가지 옵션이 있습니다. 이 경우에 만듭니다는 `<ContentTemplate>` 태그입니다. 태그는 올바른 형식의 레이블 및 단추 주위이 태그를 줄 바꿈 해야 합니다.


[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image5.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image4.png)

([전체 크기 이미지를 보려면 클릭](understanding-partial-page-updates-with-asp-net-ajax/_static/image6.png))


1. 내는 `<form>` 요소를 두 번 클릭 하 여 ScriptManager 컨트롤 포함는 `ScriptManager` 도구 상자의 항목.
2. 편집 된 `<asp:ScriptManager>` 특성 포함 되도록 태그 `EnablePartialRendering= true`합니다.

**Default.aspx 사용 하도록 설정 하는 부분 렌더링에 대 한 마크업 코드 3:**

[!code-aspx[Main](understanding-partial-page-updates-with-asp-net-ajax/samples/sample3.aspx)]

1. Web.config 파일을 엽니다. Visual Studio System.Web.Extensions.dll에 대 한 컴파일 참조를 자동으로 추가 했습니다 확인 합니다.

1. Visual Studio 2008의 새로운: 자동으로 ASP.NET 웹 사이트 프로젝트 템플릿이 함께 제공 되는 web.config의 ASP.NET AJAX 확장에 필요한 모든 참조 및 포함 주석 처리 된 섹션의 구성 정보를 얻을 수 있습니다 추가 기능을 사용 하도록 주석 처리 되지 않은 합니다. Visual Studio 2005는 ASP.NET 2.0 AJAX 확장 설치 된 경우 유사한 서식 파일에 있습니다. 그러나 옵트아웃은 AJAX 확장 Visual Studio 2008에서 기본적으로 (즉, 기본적으로 참조 되지만 참조로 제거할 수 있습니다).


[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image8.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image7.png)

([전체 크기 이미지를 보려면 클릭](understanding-partial-page-updates-with-asp-net-ajax/_static/image9.png))


1. 웹 사이트를 시작 하려면 F5 키를 누릅니다. Note 어떻게 소스 코드 변경 없이 부분 렌더링을 지 원하는 데 필요 했습니다.-태그만 변경 되었습니다.

웹 사이트를 시작할 때 부분 렌더링 때문에 클릭 하면 확인 표시가 나타납니다 없습니다 깜빡임이 됩니다 (이 예에서는 보여 주지 않습니다 하)의 페이지 스크롤 위치에 변경 내용이 됩니까, 사용 하도록 설정 하는 이제 임을 표시 됩니다. 단추를 클릭 한 후 페이지의 렌더링 된 소스를 확인 하는 경우, 것은 확인 실제로 다시 게시 하는 발생 하지 않은-원래 레이블 텍스트 소스 태그의 일부분이 며을 JavaScript를 통해 레이블을 변경 되었습니다.

Visual Studio 2008는 ASP.NET AJAX 사용 웹 사이트에 대 한 미리 정의 된 템플릿을 사용 하 여 상태가 될 때까지 나타나지 않습니다. 그러나 Visual Studio 2005와 ASP.NET 2.0 AJAX 확장 설치 된 경우 이러한 템플릿을 Visual Studio 2005 내에서 사용할 수 없었습니다. 따라서 웹 사이트를 구성 하 고 AJAX-Enabled 웹 사이트 템플릿을 사용 하 여 시작 되기 마련 더욱 쉽게 서식 파일 (웹 서비스 액세스를 포함 하 여 ASP.NET AJAX 확장에 중 일부를 지원할 완전히 구성 된 web.config 파일을 포함 해야 하는 대로 및 JSON serialization-JavaScript Object Notation) 기본적으로는 UpdatePanel 및 ContentTemplate 주 Web Forms 페이지 내에 포함 합니다. 이 기본 페이지를 사용 하 여 부분 렌더링을 사용 하는 것은 하기만 하면 10이 연습의 단계를 다시 방문 및 페이지에 컨트롤을 삭제 합니다.

## <a name="the-scriptmanager-control"></a>ScriptManager 컨트롤

## <a name="scriptmanager-control-reference"></a>ScriptManager 컨트롤 참조

태그 사용이 가능한 속성:

| **속성 이름** | **Type** | **설명** |
| --- | --- | --- |
| AllowCustomErrors-Redirect | Bool | 오류를 처리 하는 web.config 파일의 사용자 지정 오류 섹션이 사용할지 여부를 지정 합니다. |
| AsyncPostBackError-Message | 문자열 | 오류가 발생 하는 경우 클라이언트에 보낸 오류 메시지를 가져오거나 설정 합니다. |
| AsyncPostBack-Timeout | Int32 | 완료에 대 한 비동기 요청에 대 한 클라이언트가 대기 해야 하는 한 번의 기본 시간을 가져오거나 설정 합니다. |
| EnableScript-Globalization | Bool | 전역화 스크립트를 사용할지 여부를 나타내는 값을 가져오거나 설정 합니다. |
| EnableScript-Localization | Bool | 스크립트 지역화를 사용할지 여부를 나타내는 값을 가져오거나 설정 합니다. |
| ScriptLoadTimeout | Int32 | 클라이언트에 스크립트를 로드 하기 위한 허용 하는 시간 (초) 수를 결정 |
| ScriptMode | Enum (자동, 디버그, 릴리스, 상속) | 릴리스 버전의 스크립트를 렌더링할지 여부를 가져오거나 |
| ScriptPath | 문자열 | 클라이언트에 보낼 스크립트 파일의 위치를 루트 경로 가져오거나 설정 합니다. |

코드 으로만 이동 가능한 속성:

| **속성 이름** | **Type** | **설명** |
| --- | --- | --- |
| AuthenticationService | AuthenticationService-Manager | 클라이언트에 전송 될 ASP.NET 인증 서비스 프록시에 대 한 세부 정보를 가져옵니다. |
| IsDebuggingEnabled | Bool | 여부 가져옵니다 스크립팅하고 코드 디버깅을 사용 합니다. |
| IsInAsyncPostback | Bool | 페이지는 현재 비동기 다시 게시 요청에 있는지 여부를 가져옵니다. |
| ProfileService | ProfileService-Manager | 클라이언트에 전송 되는 ASP.NET 프로 파일링 서비스 프록시에 대 한 세부 정보를 가져옵니다. |
| 스크립트 | 컬렉션&lt;스크립트 참조&gt; | 클라이언트에 전송 되는 스크립트 참조의 컬렉션을 가져옵니다. |
| 서비스 | 컬렉션&lt;서비스 참조&gt; | 클라이언트에 전송 되는 웹 서비스 프록시 참조의 컬렉션을 가져옵니다. |
| SupportsPartialRendering | Bool | 현재 클라이언트 부분 렌더링을 지원 하는지 여부를 가져옵니다. 이 속성을 반환 하는 경우 **false**, 표준 포스트백이 페이지에 대 한 모든 요청 됩니다. |

공용 코드 메서드:

| **메서드 이름** | **Type** | **설명** |
| --- | --- | --- |
| SetFocus(string) | Void | 요청이 완료 되었을 때 특정 컨트롤로 클라이언트의 포커스를 설정 합니다. |

태그의 하위 항목:

| **태그** | **설명** |
| --- | --- |
| &lt;AuthenticationService&gt; | ASP.NET 인증 서비스에 대 한 프록시에 대 한 세부 정보를 제공합니다. |
| &lt;ProfileService&gt; | ASP.NET 서비스를 프로 파일링 하는 프록시에 대 한 세부 정보를 제공 합니다. |
| &lt;스크립트&gt; | 추가 스크립트 참조를 제공 합니다. |
| &lt;asp:ScriptReference&gt; | 특정 스크립트 참조를 나타냅니다. |
| &lt;Service&gt; | 생성 된 프록시 클래스를 포함 하는 추가 웹 서비스 참조를 제공 합니다. |
| &lt;asp:ServiceReference&gt; | 특정 웹 서비스 참조를 나타냅니다. |

ASP.NET AJAX 확장에 대 한 필수 코어 ScriptManager입니다. 스크립트 라이브러리 (클라이언트 쪽 스크립트 광범위 한 형식 시스템 포함)에 대 한 액세스를 제공, 부분 렌더링을 지원 하 고 추가 ASP.NET 서비스 (예: 인증 및 프로 파일링, 뿐만 아니라 다른 웹 서비스)에 대 한 포괄적인 지원을 제공 합니다. ScriptManager 컨트롤은 또한 전역화 및 지역화 클라이언트 스크립트에 대 한 지원 제공 합니다.

## <a name="providing-alterative-and-supplemental-scripts"></a>Alterative 및 추가 스크립트를 제공합니다.

개발자는 사용자 지정된 스크립트 파일에 ScriptManager를 리디렉션할 수 있을 뿐만 아니라 등록 디버그에 전체 스크립트 코드를 포함 하 고 참조 된 어셈블리에 포함 된 리소스로 버전을 릴리스 하는 Microsoft ASP.NET 2.0 AJAX 확장, 필요한 스크립트를 추가 합니다.

에 대 한 등록할 수 있습니다 (예: 스페이스 네임 스페이스 및 사용자 정의 형식 지정 체계를 지 원하는 특정) 일반적으로 포함 된 스크립트에 대 한 기본 바인딩의 재정의 하려면는 `ResolveScriptReference` ScriptManager 클래스의 이벤트입니다. 이 메서드는 이벤트 처리기는 문제의; 스크립트 파일의 경로 변경할 수 있습니다. 스크립트 관리자는 클라이언트에 스크립트의 사용자 정의 된 또는 서로 다른 사본을 보냅니다.

또한 스크립트 참조 (나타내는 `ScriptReference` 클래스) 태그를 통해 프로그래밍 방식으로 또는 포함 될 수 있습니다. 이렇게 하려면 프로그래밍 방식으로 수정 하거나는 `ScriptManager.Scripts` 컬렉션, 포함 또는 `<asp:ScriptReference>` 에서 태그는 `<Scripts>` ScriptManager 컨트롤의 첫 번째 수준 자식 태그입니다.

## <a name="custom-error-handling-for-updatepanels"></a>사용자 지정 오류 적어지므로 대 한 처리

하지만 업데이트 트리거 UpdatePanel 컨트롤에서 지정 하 여 처리 오류 처리 및 사용자 정의 오류 메시지에 대 한 지원 페이지의 ScriptManager 컨트롤 인스턴스에 의해 처리 됩니다. 이벤트를 노출 하 여 이렇게 `AsyncPostBackError`을 수 있는 페이지에 다음 사용자 지정 예외 처리 논리를 제공 합니다.

AsyncPostBackError 이벤트를 사용 하 여 지정할 수 있습니다는 `AsyncPostBackErrorMessage` 속성 다음 경고 대화 상자를 콜백 완료 되 면 발생 합니다.

클라이언트 쪽 사용자 지정에서 기본 경고 상자;를 사용 하는 대신도 가능. 예를 들어, 사용자 지정 표시 하려면 수 `<div>` 기본 브라우저 모달 대화 상자 대신 요소입니다. 이 경우 클라이언트 스크립트에서 오류를 처리할 수 있습니다.

**사용자 지정 오류를 표시 하려면 목록 5: 클라이언트 쪽 스크립트**

[!code-html[Main](understanding-partial-page-updates-with-asp-net-ajax/samples/sample4.html)]

만 위의 스크립트는 콜백을 등록에 대 한 클라이언트 쪽 AJAX 런타임 비동기 요청이 완료 되 면 합니다. 다음 오류가 보고 된 되었는지 확인 하는 검사 하 고이 경우에 대 한 세부 정보를 마지막으로 런타임에 오류 처리 되었음을 나타내는 사용자 지정 스크립트에 처리 합니다.

## <a name="globalization-and-localization-support"></a>전역화 및 지역화 지원

ScriptManager 컨트롤 지역화 스크립트 문자열 및 사용자 인터페이스 구성 요소;에 대 한 광범위 한 지원 제공 그러나 해당 항목은이 백서의 범위를 벗어났습니다. 자세한 내용은 ASP.NET AJAX 확장에 대 한 전역화 지원을 백서를 참조 합니다.

## <a name="the-updatepanel-control"></a>UpdatePanel 컨트롤

## <a name="updatepanel-control-reference"></a>UpdatePanel 컨트롤 참조

태그 사용이 가능한 속성:

| **속성 이름** | **Type** | **설명** |
| --- | --- | --- |
| ChildrenAsTriggers | bool | 자식 컨트롤이 포스트백에서 새로 고침을 자동으로 호출 여부를 지정 합니다. |
| RenderMode | enum (블록, 인라인) | 지정 방식으로 콘텐츠를 시각적으로 표시 됩니다. |
| UpdateMode | enum (항상, 조건부) | UpdatePanel 부분 렌더링 하는 동안 새로 고침은 항상 여부 또는 경우만 새로 고쳐집니다 트리거 적중 될 때 지정 합니다. |

코드 으로만 이동 가능한 속성:

| **속성 이름** | **Type** | **설명** |
| --- | --- | --- |
| IsInPartialRendering | bool | UpdatePanel 현재 요청에 대 한 부분 렌더링을 지원 하는지 여부를 가져옵니다. |
| ContentTemplate | ITemplate | 업데이트 요청에 대 한 태그 서식 파일을 가져옵니다. |
| ContentTemplateContainer | Control | 업데이트 요청에 대 한 프로그래밍 방식으로 서식 파일을 가져옵니다. |
| 트리거 | UpdatePanel- TriggerCollection | 현재 UpdatePanel와 연결 된 트리거 목록을 가져옵니다. |

공용 코드 메서드:

| **메서드 이름** | **Type** | **설명** |
| --- | --- | --- |
| Update() | Void | 지정 된 UpdatePanel을 프로그래밍 방식으로 업데이트합니다. 그렇지 않으면 트리거되지 UpdatePanel의 부분 렌더링을 트리거할 서버 요청을 허용 합니다. |

태그의 하위 항목:

| **태그** | **설명** |
| --- | --- |
| &lt;ContentTemplate&gt; | 부분 렌더링 결과 렌더링 하는 데 사용할 태그를 지정 합니다. 자식 &lt;asp: UpdatePanel&gt;합니다. |
| &lt;트리거&gt; | 컬렉션을 지정 *n* 이 UpdatePanel이 업데이트와 연관 된 컨트롤입니다. 자식 &lt;asp: UpdatePanel&gt;합니다. |
| &lt;asp:AsyncPostBackTrigger&gt; | 주어진된 UpdatePanel에 대 한 부분 페이지 렌더링을 호출 하는 트리거를 지정 합니다. 있거나 해당 UpdatePanel의 하위 항목으로 컨트롤을 되지 않을 수 있습니다. 세분화 된 이벤트 이름입니다. 자식 &lt;트리거&gt;합니다. |
| &lt;asp:PostBackTrigger&gt; | 전체 페이지를 새로 고칠을 발생 시키는 컨트롤을 지정 합니다. 있거나 해당 UpdatePanel의 하위 항목으로 컨트롤을 되지 않을 수 있습니다. 개체에 세분화 합니다. 자식 &lt;트리거&gt;합니다. |

`UpdatePanel` 컨트롤은 서버 쪽 콘텐츠 AJAX 확장의 부분 렌더링 기능에 관여 합니다를 구분 하는 컨트롤입니다. 페이지, 될 수 있는 UpdatePanel 컨트롤의 수에 제한이 없음을 의미 이며 중첩 될 수 있습니다. 각 수 독립적으로 작업할 수 있도록 각 UpdatePanel 격리 되 (해당 페이지의 다른 부분을 독립적으로 페이지의 포스트백 렌더링 같은 시간에 실행 중인 두 개의 적어지므로 있을 수 있습니다).

UpdatePanel 컨트롤 트리거와 함께-기본적으로 UpdatePanel에 포함 된 모든 컨트롤 거래 주로 제어 `ContentTemplate` 포스트백을 야기 하는 UpdatePanel의 트리거로 등록 합니다. 즉, UpdatePanel 사용자 정의 컨트롤 (예: GridView) 기본 데이터 바인딩된 컨트롤을 작업할 수 스크립트에서 프로그래밍할 수 있습니다.

기본적으로, 부분 페이지 렌더링 트리거될 때 페이지에 있는 모든 UpdatePanel 컨트롤 새로 고쳐집니다, 그리고 이러한 작업에 대 한 트리거를 정의 여부 UpdatePanel 제어 합니다. 예를 들어 한 UpdatePanel 단추 컨트롤을 정의 하는 경우 해당 단추 컨트롤을 클릭 하면 해당 페이지에 있는 모든 UpdatePanel 컨트롤 기본적으로 새로 고쳐집니다. 때문에,이 기본적으로는 `UpdateMode` UpdatePanel의 속성이로 설정 되어 `Always`합니다. UpdateMode 속성 설정할 수 있습니다 또는 `Conditional`, 즉, 특정 트리거 수에 도달 UpdatePanel 새로 됩니다.

## <a name="custom-control-notes"></a>사용자 지정 컨트롤 정보

모든 사용자 정의 컨트롤 또는 사용자 지정 컨트롤;에 UpdatePanel은 추가할 수 있습니다. 그러나 이러한 컨트롤은 포함 하는 페이지도 포함 해야 속성이 EnablePartialRendering로 설정 된 ScriptManager 컨트롤 **true**합니다.

한 가지 방법은 수에 대해 계정을이 재정의 보호 된 웹 사용자 지정 컨트롤을 사용 하는 경우 `CreateChildControls()` 의 메서드는 `CompositeControl` 클래스입니다. 이렇게 함으로써 주입할 수 판단 페이지에서 부분 렌더링을 지원 되는 경우 컨트롤의 자식와 외부 세계 간의 UpdatePanel 컨테이너에 자식 컨트롤이 단순히 계층화 할 수 있습니다, `Control` 인스턴스.

## <a name="updatepanel-considerations"></a>UpdatePanel 고려 사항

UpdatePanel은 JavaScript XMLHttpRequest의 컨텍스트 내에서 ASP.NET 포스트백 래핑 축 블랙 박스 작동 합니다. 그러나 동작 및 속도 관점 기억해 야 할 중요 한 성능 고려 사항이 있습니다. UpdatePanel의 작동 방식을 이해, 사용이 적절 한 경우를 가장 잘 결정할 수 있도록 하는 AJAX exchange를 검사 해야 합니다. 다음 예제에서는 기존 사이트 및, Mozilla Firefox (Firebug XMLHttpRequest 데이터가 캡처되고 해당 데이터가) Firebug 확장명으로 사용 합니다.

양식을, 특히, 우편 번호 textbox 폼 이나 컨트롤에 city 및 state 필드를 채울 해야 하는 것이 좋습니다. 이 폼에는 궁극적으로 구성원 정보를 사용자의 이름, 주소 및 연락처 정보를 포함 하 여 수집 합니다. 특정 프로젝트의 요구 사항에 따라 계정을 고려 되도록 많은 디자인 고려 사항이 있습니다.


[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image11.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image10.png)

([전체 크기 이미지를 보려면 클릭](understanding-partial-page-updates-with-asp-net-ajax/_static/image12.png))


[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image14.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image13.png)

([전체 크기 이미지를 보려면 클릭](understanding-partial-page-updates-with-asp-net-ajax/_static/image15.png))


이 응용 프로그램의 원래 반복에서는 전체 우편 번호, 도시, 및 상태를 포함 하 여 사용자 등록 데이터를 통합 하는 컨트롤이 만들어졌습니다. 전체 컨트롤 UpdatePanel 내에 포함될지 이었으며 웹 폼으로 끌어 놓으면 됩니다. 사용자가 우편 번호를 입력 하면 UpdatePanel 이벤트 (백 엔드, 또는 트리거를 지정 하 여 경우 ChildrenAsTriggers 속성이 true로 설정을 사용 하 여에서 해당 TextChanged 이벤트)를 검색 합니다. AJAX 게시 FireBug에서 확보는 UpdatePanel 내에서 필드의 모든 (오른쪽에 다이어그램 참조).

UpdatePanel 내에서 모든 컨트롤의 값을 제공 되며, 화면 캡처 나타나듯이 (이 경우 이들이 모두 비어), ViewState 필드 뿐만 아니라 합니다. 모든를 told 넘는 9 kb의 사용 데이터 전송 됩니다 5 바이트의 데이터가이 특정 요청에 실제로 필요한 경우. 응답은 훨씬 더 너무 커지면: 전체적으로 57 kb 보내집니다는 클라이언트에 단순히와 드롭 다운 텍스트 필드를 업데이트 합니다.

ASP.NET AJAX 프레젠테이션을 업데이트 하는 방법을 확인 하려면 관심 있는 수도 있습니다. UpdatePanel의 업데이트 요청의 응답 부분 왼쪽; Firebug 콘솔 디스플레이에 표시 형식은 특수 공식화 파이프로 구분 된 문자열로 클라이언트 스크립트에 의해 분할 되 고 페이지 리 어셈블합니다. ASP.NET AJAX 설정 하는 구체적으로 *innerHTML* 프로그램 UpdatePanel을 나타내는 클라이언트에는 HTML 요소의 속성입니다. 브라우저를 다시 DOM 생성, 처리 해야 하는 정보의 양에 따라 약간의 지연이 있습니다.

DOM의 재생성 추가 문제가 많이 트리거됩니다.


[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image17.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image16.png)

([전체 크기 이미지를 보려면 클릭](understanding-partial-page-updates-with-asp-net-ajax/_static/image18.png))


- 포커스가 있는 HTML 요소 UpdatePanel 내에 있으면 포커스를 손실 됩니다. 따라서 사용자의 우편 번호 텍스트 상자를 종료 하려면 Tab 키를 누른 경우 다음 대상 것 City 텍스트 상자입니다. 그러나 UpdatePanel을 새로 고치면 표시 되 면 폼 포커스를 했지만 더 이상 및 Tab을 눌러 시작 포커스 요소 (예: 링크)를 강조 표시 합니다.
- 모든 유형의 사용자 지정 클라이언트 쪽 스크립트 사용 중인 함수에 의해 액세스 DOM 요소 참조 유지 되도록 될 수도 있습니다 존재 하지 않는 부분 포스트백 후.

적어지므로 포괄적인 솔루션 수 없습니다. 대신, 프로필은 빠른 해결 방법 상황에서 프로토타입 만들기, 작은 컨트롤 업데이트를 포함 하 여 특정 제공 하며 파일.NET 개체 모델에 잘 알고 있지만 DOM으로 덜 하도록 해야 할 수 있는 ASP.NET 개발자에 게 친숙 한 인터페이스를 제공 합니다. 응용 프로그램 시나리오에 따라 성능이 향상 될 수 있는 대안 많습니다.

- 개발자가 호출 되는 웹 서비스 호출 하는 경우 페이지에서 정적 메서드를 호출할 수 있습니다 PageMethods 및 JSON (JavaScript Object Notation)을 사용 하는 것이 좋습니다. 메서드는 정적 상태가 필요 합니다. 스크립트 호출자에 게 매개 변수를 제공 하 고 결과 비동기적으로 반환 됩니다.
- 응용 프로그램을 통해 여러 위치에서 사용 해야 하는 단일 제어 하는 경우 웹 서비스 및 JSON을 사용 하는 것이 좋습니다. 이 다시 특별 한 작업이 거의 필요 하며 비동기적으로 작동 합니다.

웹 서비스 또는 페이지 메서드를 통해 기능을 통합 단점이 있습니다. 무엇 보다도, ASP.NET 개발자가 일반적으로 사용자 정의 컨트롤 (.ascx 파일)에 기능의 작은 구성 요소를 작성 하는 경향이 있습니다. 이러한 파일;의 페이지 메서드를 호스팅할 수 없습니다. 실제.aspx 페이지 클래스 내에서 호스팅해야 합니다. 마찬가지로, 웹 서비스.asmx 클래스 내에서 호스트 해야 합니다. 응용 프로그램에 따라이 아키텍처 거의 또는 전혀 화합 동률 수 있는 두 개 이상의 물리 구성에 걸쳐 이제 단일 구성 요소에 대 한 기능에 단일 책임 원칙을 위반 될 수 있습니다.

마지막으로, 응용 프로그램을 적어지므로 사용 되 고 필요한 경우 다음 지침 문제 해결 및 유지 관리 지원 해야 합니다.

- **코드 단위에 걸쳐 뿐만 아니라 적어지므로으로 가능한 뿐만 아니라 내에서 단위를 중첩 합니다.** 예를 들어 UpdatePanel UpdatePanel을 포함 하는 다른 컨트롤을 포함 하는 UpdatePanel도 포함 되 고 제어 하는 컨트롤을 래핑하는 페이지를 단위 간 중첩 합니다. 이렇게 하면 가까이 요소를 새로 고치는 중, 이어야 하며 자식 적어지므로에 예기치 않은 새로 고침을 방지 합니다.
- **유지 된 *경우 ChildrenAsTriggers* 속성이 false로 설정 하 고 이벤트 트리거를 명시적으로 설정 합니다.** 활용 하 여 `<Triggers>` 컬렉션 이벤트를 처리 하는 훨씬 더 명확 하 게 방법 및 예기치 않은 동작을를 유지 관리 작업에 도움을 주고에 참여 하는 이벤트에 대 한 개발자 강제 적용 되지 않을 수 있습니다.
- **가능한 가장 작은 단위를 사용 하 여 기능을 활용할 수 있습니다.** 에서 설명한 대로 래핑 우편 번호 서비스에 대 한 설명만 최소한 서버, 전체 처리 및 클라이언트 서버 교환에 필요한 공간에 시간을 줄일 수, 성능 향상.

## <a name="the-updateprogress-control"></a>UpdateProgress 컨트롤

## <a name="updateprogress-control-reference"></a>UpdateProgress 컨트롤 참조

태그 사용이 가능한 속성:

| **속성 이름** | **Type** | **설명** |
| --- | --- | --- |
| AssociatedUpdate-PanelID | 문자열 | 이 UpdateProgress에 대해 보고 해야 하는 UpdatePanel의 ID를 지정 합니다. |
| DisplayAfter | Int | 비동기 요청이 시작 된 후이 컨트롤이 표시 되기 전에 밀리초 단위로 제한 시간을 지정 합니다. |
| DynamicLayout | bool | 진행 상황을 동적으로 렌더링 되는지 여부를 지정 합니다. |

태그의 하위 항목:

| **태그** | **설명** |
| --- | --- |
| &lt;ProgressTemplate&gt; | 이 컨트롤에 표시 되는 콘텐츠에 대 한 설정 제어 템플릿을 포함 합니다. |

UpdateProgress 컨트롤 측정 한 서버에 전송 하는 데 필요한 작업을 수행 하는 동안 사용자의 관심을 유지 하는 피드백을 제공 합니다. 이렇게 하면 사용자에 게는 현재 수행 중인 문제가 아닐 명백한, 특히 하기 때문에 대부분의 사용자 페이지를 새로 고치고 강조 표시 상태 표시줄을 표시 하는 데 사용 되는 경우에 도움이 됩니다.

메모, UpdateProgress 컨트롤 페이지 계층 구조에서 아무 곳 이나 나타날 수 있습니다. 그러나 부분 포스트백은 자식 UpdatePanel (여기서는 UpdatePanel 내에 중첩 된 다른 UpdatePanel)에서 시작 하는 경우에서 해당 트리거 UpdatePanel의 자식에 대 한 UpdateProgress 템플릿을 표시 하지 하면 자식 다시 게시 UpdatePanel 뿐만 아니라 부모 UpdatePanel입니다. 그러나 트리거 부모 UpdatePanel의 직계 자식이 이면 다음 부모와 연결 된 UpdateProgress 템플릿만 표시 됩니다.

## <a name="summary"></a>요약

Microsoft ASP.NET AJAX extensions는 웹 콘텐츠를 보다 쉽게 액세스할 수 있도록 지원 하기 위해 웹 응용 프로그램에 풍부한 사용자 환경을 제공 하도록 고안 된 정교한 제품입니다. ASP.NET AJAX 확장에 부분 페이지 렌더링 컨트롤의 일부로 ScriptManager, UpdatePanel, 및 UpdateProgress 컨트롤을 포함 하 여은 몇 도구 키트의 가장 눈에 띄는 구성 요소입니다.

ScriptManager 구성 요소가 통합 하는 확장에 대 한 클라이언트 JavaScript 프로 비전으로의 개발 투자와 함께 작동 하도록 다양 한 서버 및 클라이언트 쪽 구성 요소를 사용 하도록 설정 합니다.

UpdatePanel 컨트롤은 명백한 매직 상자-UpdatePanel 내의 태그 서버 쪽 코드 숨김 파일을 포함할 수 있으며 페이지 새로 고침을 트리거하지 않습니다. UpdatePanel 컨트롤 중첩 될 수 있습니다 및 다른 적어지므로 컨트롤에 종속 될 수 있습니다. 기본적으로 적어지므로 있지만이 기능은 정밀 하 게 조정할 수를 선언적으로 또는 프로그래밍 방식으로 해당 하위 컨트롤을 호출한 모든 포스트백을 처리 합니다.

UpdatePanel 컨트롤을 사용 하는 경우 개발자가 잠재적으로 발생 하는 성능에 영향을 알고 있어야 합니다. 잠재적인 대안 응용 프로그램의 디자인 고려해 야 하는 경우 웹 서비스 및 페이지 메서드를 포함 됩니다.

컨트롤을 사용 하면 사용자 수 있음을 알고 증명, 무시 되지 않습니다는 페이지가 있는 동안 백그라운드 요청에서 일어나는 그렇지 않은 경우 하지 UpdateProgress 사용자 입력에 응답 하도록 작업을 수행 합니다. 또한 부분 렌더링 결과 중단 하는 기능이 포함 됩니다.

함께 이러한 도구는 서버 작업을 사용자에 게는 덜 명확 하 고 덜 워크플로 중단 하 여 풍부 하 고 원활한 사용자 환경이 생성을 지원 합니다.

## <a name="bio"></a>약력

Scott 인증서의 근무 기간이 Microsoft 웹 기술을 1997 년부터 이며 myKB.com 부서장 ([www.myKB.com](http://www.myKB.com)) ASP.NET 작성 i 여기서 기반 응용 프로그램 기술 자료 소프트웨어 솔루션에 집중 합니다. Scott에 전자 메일을 통해 연결할 수 [ scott.cate@myKB.com ](mailto:scott.cate@myKB.com) 또는에서 그의 블로그 [ScottCate.com](http://ScottCate.com)

> [!div class="step-by-step"]
> [다음](understanding-asp-net-ajax-updatepanel-triggers.md)
