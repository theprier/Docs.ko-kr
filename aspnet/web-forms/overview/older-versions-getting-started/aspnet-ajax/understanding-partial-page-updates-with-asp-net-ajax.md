---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-partial-page-updates-with-asp-net-ajax
title: ASP.NET AJAX를 사용한 부분 페이지 업데이트 이해 | Microsoft Docs
author: scottcate
description: 아마도 ASP.NET AJAX Extensions의 두드러진 기능 하는 기능 t 전체 포스트백을 수행 하지 않고 부분 또는 증분 페이지 업데이트를 수행 하는 중...
ms.author: riande
ms.date: 03/28/2008
ms.assetid: 54d9df99-1161-4899-b4e8-2679c85915e7
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-partial-page-updates-with-asp-net-ajax
msc.type: authoredcontent
ms.openlocfilehash: 4883046aa16d5e67b7f0c92e15c897ef1a933b67
ms.sourcegitcommit: 97d7a00bd39c83a8f6bccb9daa44130a509f75ce
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2019
ms.locfileid: "54098937"
---
<a name="understanding-partial-page-updates-with-aspnet-ajax"></a>ASP.NET AJAX를 사용 하 여 이해 부분 페이지 업데이트
====================
[Scott Cate](https://github.com/scottcate)

[PDF 다운로드](http://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial01_Partial_Page_Updates_cs.pdf)

> 아마도 ASP.NET AJAX Extensions의 두드러진 기능 하는 기능 코드 변경 내용 및 최소 태그 변경 내용을 서버에 전체 포스트백을 수행 하지 않고 부분 또는 증분 페이지 업데이트를 수행 합니다. 장점은 광범위 한 – 멀티미디어 (예: Adobe Flash 또는 Windows 미디어)의 상태가 변경, 대역폭 비용을 감소 및 클라이언트 포스트백을 통해 일반적으로 관련 된 깜박임 발생 하지 않습니다.


## <a name="introduction"></a>소개

Microsoft의 ASP.NET 기술을 개체 지향 및 이벤트 구동 프로그래밍 모델을 제공 및 컴파일된 코드의 이점과 결합 합니다. 그러나 해당 서버 쪽 처리 모델에는 기술에 내재 된 몇 가지 단점이 있습니다.

- 페이지 업데이트 페이지 새로 고침 해야 하는 서버에 대 한 왕복 작업이 필요 합니다.
- 왕복은 Javascript 또는 기타 클라이언트 쪽 기술 (예: Adobe Flash)에서 생성 된 모든 결과 유지 되지 않습니다.
- 포스트백, Microsoft Internet Explorer 이외의 브라우저 지원 하지 않습니다 스크롤 위치를 자동으로 복원. 되며 Internet Explorer에도 여전히 깜빡임 페이지를 새로 고칠 때.
- 포스트백으로 대역폭 대량의 포함 될 수 있습니다 합니다 \_ \_GridView 컨트롤 또는 반복기와 같은 컨트롤을 사용 하 여 처리 하는 경우에 특히 VIEWSTATE 폼 필드 커질 수 있습니다.
- JavaScript 또는 기타 클라이언트 쪽 기술을 통해 웹 서비스에 액세스 하기 위한 통합 된 모델이 없는 합니다.

Microsoft의 ASP.NET AJAX 확장을 입력 합니다. AJAX의 약자인 **A** 동기 **J** avaScript **A** nd **X** ML는 증분 페이지를 제공 하기 위한 통합 된 프레임 워크 플랫폼 간 JavaScript 통해 업데이트는 Microsoft AJAX 프레임 워크 및 Microsoft AJAX 스크립트 라이브러리를 호출 하는 스크립트 구성 요소를 구성 하는 서버 쪽 코드 이루어져 있습니다. ASP.NET AJAX 확장은 또한 JavaScript 통해 ASP.NET 웹 서비스에 액세스 하기 위한 플랫폼 간 지원을 제공 합니다.

이 백서에 ScriptManager 구성 요소가, UpdatePanel 컨트롤 및 UpdateProgress 컨트롤을 포함 해야 하거나 안 이러한 있는 시나리오를 고려 하며 ASP.NET AJAX Extensions, 부분 페이지 업데이트 기능 검사 사용 됩니다.

이 백서는 Visual studio 2008 베타 2 릴리스 및 ASP.NET AJAX Extensions (있던 이전에 ASP.NET 2.0에 대 한 사용 가능한 추가 기능 구성 요소) 기본 클래스 라이브러리에 통합 하는.NET Framework 3.5를 기반으로 합니다. 이 백서는 또한 Visual Studio 2008 및 없습니다 Visual Web Developer Express Edition; 사용 한다고 가정 Visual Web Developer Express 사용자에 게 참조 되는 일부 프로젝트 서식 파일을 사용 하지 못할 수도 있습니다.

## <a name="partial-page-updates"></a>부분 페이지 업데이트

아마도 ASP.NET AJAX Extensions의 두드러진 기능 하는 기능 코드 변경 내용 및 최소 태그 변경 내용을 서버에 전체 포스트백을 수행 하지 않고 부분 또는 증분 페이지 업데이트를 수행 합니다. 장점은 광범위 한-(예: Adobe Flash 또는 Windows 미디어) 멀티미디어의 상태가 변경, 대역폭 비용을 감소 및 클라이언트 포스트백을 통해 일반적으로 관련 된 깜박임 발생 하지 않습니다.

부분 페이지 렌더링을 통합 하는 기능 프로젝트에 대 한 변경을 최소화 하 여 ASP.NET에 통합 됩니다.

## <a name="walkthrough-integrating-partial-rendering-into-an-existing-project"></a>연습: 부분 렌더링을 기존 프로젝트에 통합


1. Microsoft Visual Studio 2008로 이동 하 여 새 ASP.NET 웹 사이트 프로젝트를 만듭니다 <em>파일</em>  <em>- &gt; New</em>  <em>- &gt; 웹사이트</em> 대화 상자에서 ASP.NET 웹 사이트를 선택 합니다. 원하는 이름을 지정할 수 있습니다 하 고 파일 시스템 또는 인터넷 정보 서비스 (IIS)에 설치할 수 있습니다.
2. 기본 ASP.NET 태그를 사용 하 여 빈 기본 페이지를 사용 하 여 표시 됩니다 (서버 쪽 양식의 및 `@Page` 지시문). 라는 레이블을 넣으면 `Label1` 단추를 호출 하 고 `Button1` form 요소 안에 있는 페이지를 합니다. 원하는을 해당 텍스트 속성을 설정할 수 있습니다.
3. 디자인 뷰에서 두 번 클릭 `Button1` 코드 숨김 이벤트 처리기를 생성 합니다. 이 이벤트 처리기 내에서 설정 `Label1.Text` 에 단추를 클릭 하면! .

**목록 1: 부분 렌더링이 활성화 전에 default.aspx에 대 한 태그**

[!code-aspx[Main](understanding-partial-page-updates-with-asp-net-ajax/samples/sample1.aspx)]

**2를 나열 합니다. 코드 숨김 default.aspx.cs의 (트리밍)**

[!code-csharp[Main](understanding-partial-page-updates-with-asp-net-ajax/samples/sample2.cs)]

1. F5 키를 눌러 웹 사이트를 시작 합니다. Visual Studio 디버깅을 사용 하도록 설정 하려면 web.config 파일을 추가 하 라는 메시지가 나타납니다. 이렇게 합니다. 단추를 클릭 하면 레이블은 텍스트를 변경 하려면 페이지가 새로 고쳐지고 하 고 페이지를 다시 그릴 간략 한 깜박임이 알 수 있습니다.
2. 브라우저 창을 닫으면 Visual Studio에는 태그 페이지를 반환 합니다. Visual Studio 도구 상자에서 아래로 스크롤하여 AJAX Extensions 라는 레이블이 지정 된 탭을 찾습니다. (이전 버전의 Atlas 또는 AJAX 확장을 사용 하 고 있으므로이 탭 없는, 하는 경우이 백서 뒷부분에서 AJAX 확장 도구 상자 항목을 등록 하는 것에 대 한 연습을 참조 또는 다운로드할 수 있는 Windows Installer를 사용 하 여 현재 버전을 설치 합니다. 웹 사이트에서).


[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image2.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image1.png)

([클릭 하 여 큰 이미지 보기](understanding-partial-page-updates-with-asp-net-ajax/_static/image3.png))


1. <em>알려진된 문제:</em>Visual Studio 2008 AJAX 확장 도구 상자 항목을 가져오게 ASP.NET 2.0 AJAX Extensions를 사용 하 여 설치 하는 Visual Studio 2005에 이미 있는 컴퓨터에 Visual Studio 2008을 설치 하는 경우. 구성 요소;의 도구 설명을 검사 하 여 대/소문자 인지 여부를 확인할 수 있습니다. 이러한 버전 3.5.0.0 나타나야 합니다. 버전 2.0.0.0 야 말로 다음 이전 도구 상자 항목을 가져온를 Visual Studio에서 도구 상자 항목 선택 대화 상자를 사용 하 여 수동으로 가져올 해야 합니다. 디자이너를 통해 버전 2 컨트롤을 추가할 수 없습니다.

2. 전에 `<asp:Label>` 태그 시작, 공백, 줄 만들기 및 도구 상자에서 UpdatePanel 컨트롤을 두 번 클릭 합니다. 새 `@Register` 지시문이 나타내는 컨트롤 System.Web.UI 네임 스페이스 내에서를 사용 하 여 가져올 수는 페이지의 맨 위에 있는 포함 된 `asp:` 접두사입니다.
3. 닫는 끌어 `</asp:UpdatePanel>` 래핑된 레이블과 단추 컨트롤을 사용 하 여 요소를 제대로 구성 된 있도록 단추 요소의 끝 태그입니다.
4. 연 후 `<asp:UpdatePanel>` 태그, 여는 새 태그를 시작 합니다. IntelliSense 묻는 두 가지 옵션을 참고 합니다. 이 경우 만들기는 `<ContentTemplate>` 태그입니다. 태그는 잘 구성 된이 태그에 레이블 및 단추 주위를 래핑할 해야 합니다.


[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image5.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image4.png)

([클릭 하 여 큰 이미지 보기](understanding-partial-page-updates-with-asp-net-ajax/_static/image6.png))


1. 어느 부분에 `<form>` 요소를 ScriptManager 컨트롤을 두 번 클릭 하 여 포함는 `ScriptManager` 도구 상자의 항목.
2. 편집 된 `<asp:ScriptManager>` 특성이 포함 되도록 태그 `EnablePartialRendering= true`합니다.

**코드 3: 사용 하도록 설정 하는 부분 렌더링을 사용 하 여 default.aspx에 대 한 태그**

[!code-aspx[Main](understanding-partial-page-updates-with-asp-net-ajax/samples/sample3.aspx)]

1. Web.config 파일을 엽니다. Visual Studio System.Web.Extensions.dll 컴파일 참조를 자동으로 추가 했습니다 알 수 있습니다.

1. Visual Studio 2008의 새로운: Web.config를 사용 하 여 ASP.NET 웹 사이트 프로젝트 템플릿을 자동으로 ASP.NET AJAX 확장에 대 한 모든 필요한 참조를 포함 하 고 포함을 함께 제공 되는 추가 사용 하도록 설정 되지 않은 mmented 수 있는 구성 정보의 섹션을 주석 처리 기능입니다. Visual Studio 2005는 ASP.NET 2.0 AJAX Extensions가 설치 된 경우 유사한 템플릿이 있었습니다. 그러나 Visual Studio 2008에서의 AJAX 확장은 옵트아웃 기본적으로 (즉, 기본적으로 참조는 있지만 참조를 제거할 수 있습니다).


[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image8.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image7.png)

([클릭 하 여 큰 이미지 보기](understanding-partial-page-updates-with-asp-net-ajax/_static/image9.png))


1. F5 키를 눌러 웹 사이트를 시작 합니다. 소스 코드 변경 내용이 없습니다. 부분 렌더링을 지 원하는 데 필요한-만 태그를 변경 하는 방법을 note 합니다.

웹 사이트를 시작할 때 부분 렌더링은 이제 사용 하도록 설정, 때문에 클릭 하면 단추를 없습니다 깜박임이 됩니다 (이 예제에서는 보여 주지 않지만) 페이지 스크롤 위치를 변경 해도 요금이 표시 됩니다. 단추를 클릭 한 후 페이지의 렌더링 된 소스를 확인 하려는 경우이 하는지 확인 실제로 다시 게시 하는 발생 하지 않은-원래 레이블 텍스트를은 여전히 소스 태그 중 일부 JavaScript를 통해 레이블을 변경 된 합니다.

Visual Studio 2008에는 ASP.NET AJAX 지원 웹 사이트에 대 한 미리 정의 된 템플릿을 사용 하 여 표시 되지 않습니다. 그러나 Visual Studio 2005 및 ASP.NET 2.0 AJAX Extensions를 설치 된 경우 이러한 템플릿을 Visual Studio 2005 내에서 사용할 수 있었습니다. 따라서 웹 사이트를 구성 하 고 ajax 지원 웹 사이트 템플릿을 사용 하 여 시작 됩니다 가능성이 훨씬 더 쉽게 템플릿 (지 원하는 모든 웹 서비스 액세스를 포함 하 여 ASP.NET AJAX Extensions, 완벽 하 게 구성 된 web.config 파일을 포함 해야 하는 대로 및 JSON serialization-JavaScript Object Notation) 및 기본적으로 UpdatePanel 및 ContentTemplate 기본 Web Forms 페이지 내에 포함 합니다. 이 기본 페이지를 사용 하 여 부분 렌더링을 사용 하도록 설정 하는 것은 10이 연습의 단계를 다시 방문 하 여 페이지에 컨트롤을 삭제 합니다.

## <a name="the-scriptmanager-control"></a>ScriptManager 컨트롤

## <a name="scriptmanager-control-reference"></a>ScriptManager 컨트롤 참조

속성 태그 지원:

| **속성 이름** | **Type** | **설명** |
| --- | --- | --- |
| AllowCustomErrors-Redirect | Bool | 오류를 처리 하는 web.config 파일의 사용자 지정 오류 섹션을 사용할지 여부를 지정 합니다. |
| AsyncPostBackError-Message | 문자열 | 오류가 발생 하는 경우 클라이언트에 보낸 오류 메시지를 가져오거나 설정 합니다. |
| AsyncPostBack-Timeout | Int32 | 클라이언트가 비동기 요청이 완료 되기를 기다려야 합니다. 한 번의 기본 크기를 가져오거나 설정 합니다. |
| EnableScript 세계화 | Bool | 스크립트 국제화를 사용할지 여부를 나타내는 값을 가져오거나 설정 합니다. |
| EnableScript-Localization | Bool | 스크립트 지역화를 사용할지 여부를 나타내는 값을 가져오거나 설정 합니다. |
| ScriptLoadTimeout | Int32 | 클라이언트 스크립트를 로드 하는 것에 대 한 허용 하는 시간 (초) 수를 결정 합니다. |
| ScriptMode | 열거형 (Auto, 디버그, 릴리스, 상속) | 릴리스 버전의 스크립트를 렌더링할지 여부를 가져오거나 |
| ScriptPath | 문자열 | 클라이언트에 보낼 스크립트 파일의 위치에 루트 경로 가져오거나 설정 합니다. |

코드 전용 속성:

| **속성 이름** | **Type** | **설명** |
| --- | --- | --- |
| AuthenticationService | AuthenticationService-Manager | 클라이언트에 전송 될 ASP.NET 인증 서비스 프록시에 대 한 세부 정보를 가져옵니다. |
| IsDebuggingEnabled | Bool | 가져옵니다 여부 스크립트 및 코드 디버깅을 사용할 수 있습니다. |
| IsInAsyncPostback | Bool | 페이지는 현재 비동기 포스트백 요청 여부를 가져옵니다. |
| ProfileService | ProfileService-Manager | 클라이언트에 전송 될 ASP.NET 프로 파일링 서비스 프록시에 대 한 세부 정보를 가져옵니다. |
| 스크립트 | 컬렉션&lt;스크립트 참조&gt; | 클라이언트에 보낼 스크립트 참조의 컬렉션을 가져옵니다. |
| 서비스 | 컬렉션&lt;서비스 참조&gt; | 클라이언트에 전송 될 웹 서비스 프록시 참조의 컬렉션을 가져옵니다. |
| SupportsPartialRendering | Bool | 현재 클라이언트 부분 렌더링을 지원 하는지 여부를 가져옵니다. 이 속성을 반환 하는 경우 **false**, 모든 페이지 요청에는 표준 포스트백 됩니다. |

공용 코드 메서드:

| **메서드 이름** | **Type** | **설명** |
| --- | --- | --- |
| SetFocus(string) | Void | 요청이 완료 된 경우에 특정 컨트롤에 클라이언트의 포커스를 설정 합니다. |

태그 하위 항목:

| **태그** | **설명** |
| --- | --- |
| &lt;AuthenticationService&gt; | ASP.NET 인증 서비스에 프록시에 대 한 세부 정보를 제공합니다. |
| &lt;ProfileService&gt; | 서비스 프로 파일링 하는 asp.net 프록시에 대 한 정보를 제공 합니다. |
| &lt;스크립트&gt; | 추가 스크립트 참조를 제공합니다. |
| &lt;asp:ScriptReference&gt; | 특정 스크립트 참조를 나타냅니다. |
| &lt;Service&gt; | 생성 된 프록시 클래스를 포함 하는 추가 웹 서비스 참조를 제공 합니다. |
| &lt;asp:ServiceReference&gt; | 특정 웹 서비스 참조를 나타냅니다. |

ScriptManager 컨트롤이 ASP.NET AJAX 확장에 대 한 필수 핵심입니다. 스크립트 라이브러리 (광범위 한 클라이언트 쪽 스크립트 형식 시스템 포함)에 대 한 액세스를 제공, 부분 렌더링을 지원 하 고 추가 ASP.NET 서비스 (예: 인증 하 고 프로 파일링 뿐만 아니라 다른 웹 서비스)에 대 한 광범위 한 지원을 제공 합니다. ScriptManager 컨트롤은 또한 클라이언트 스크립트에 대 한 전역화 및 지역화 지원 제공 합니다.

## <a name="providing-alternative-and-supplemental-scripts"></a>대체 및 추가 스크립트를 제공합니다.

개발자는 ScriptManager를 사용자 지정된 스크립트 파일을 리디렉션할 수 있을 뿐만 아니라 등록 Microsoft ASP.NET 2.0 AJAX Extensions 디버그에 전체 스크립트 코드를 포함 하는 참조 된 어셈블리에 포함 된 리소스로 버전을 릴리스 하는 동안 필요한 스크립트를 추가 합니다.

에 등록할 수 있습니다 (예: Sys.WebForms 네임 스페이스 및 사용자 지정 입력 시스템을 지 원하는 경우에 해당) 일반적으로 포함 된 스크립트에 대 한 기본 바인딩을 재정의 하는 `ResolveScriptReference` ScriptManager 클래스의 이벤트입니다. 이 메서드를 호출 하는 경우 이벤트 처리기는 질문의 스크립트 파일 경로 변경 하려면 스크립트 관리자는 클라이언트 스크립트의 다른 또는 사용자 지정 복사본을 보냅니다.

또한 스크립트 참조 (나타내는 `ScriptReference` 클래스) 태그를 통해 프로그래밍 방식으로 나 포함할 수 있습니다. 이 위해 프로그래밍 방식으로 수정 하거나 합니다 `ScriptManager.Scripts` 컬렉션 또는 포함 `<asp:ScriptReference>` 에서 태그를 `<Scripts>` ScriptManager 컨트롤의 첫 번째 수준 자식 태그입니다.

## <a name="custom-error-handling-for-updatepanels"></a>사용자 지정 오류 Updatepanel에 대 한 처리

UpdatePanel 컨트롤에서 지정 하는 트리거에 의해 업데이트 처리 하지만 오류 처리 및 사용자 지정 오류 메시지에 대 한 지원 페이지의 ScriptManager 컨트롤 인스턴스에 의해 처리 됩니다. 이벤트를 노출 하 여 이렇게 `AsyncPostBackError`수 있는 페이지로 차례로 사용자 지정 예외 처리 논리를 제공 합니다.

AsyncPostBackError 이벤트를 사용 하 여 지정할 수 있습니다는 `AsyncPostBackErrorMessage` 하면 콜백이 완료 될 때 발생 하는 경고 상자에 다음 속성이 있습니다.

클라이언트 쪽 사용자 지정의 기본 경고 상자를 사용 하는 대신도 가능. 사용자 지정 표시 해야 하는 예를 들어 `<div>` 기본 브라우저 모달 대화 상자를 사용 하지 않고 요소입니다. 이 경우 클라이언트 스크립트에서 오류를 처리할 수 있습니다.

**코드 5: 사용자 지정 오류를 표시 하는 클라이언트 쪽 스크립트**

[!code-html[Main](understanding-partial-page-updates-with-asp-net-ajax/samples/sample4.html)]

간단히 말해, 위의 스크립트를 비동기 요청이 완료 되 면에 콜백을 대 한 클라이언트 쪽 AJAX 런타임에 등록 합니다. 그런 다음 오류가 보고 된 여부를 확인 하 고 그렇다면 마지막 런타임에 오류가 처리 되었음을 나타내는 사용자 지정 스크립트에서의 세부 정보를 처리 합니다.

## <a name="globalization-and-localization-support"></a>전역화 및 지역화 지원

ScriptManager 컨트롤 지역화 스크립트 문자열 및 사용자 인터페이스 구성 요소에 대 한 광범위 한 지원을 제공합니다 그러나이 시스템에서는이 백서에서는 범위를 벗어납니다. 자세한 내용은 ASP.NET AJAX Extensions의 세계화 지원은 백서를 참조 합니다.

## <a name="the-updatepanel-control"></a>UpdatePanel 컨트롤

## <a name="updatepanel-control-reference"></a>UpdatePanel 컨트롤 참조

속성 태그 지원:

| **속성 이름** | **Type** | **설명** |
| --- | --- | --- |
| ChildrenAsTriggers | bool | 자식 컨트롤이 다시 게시할 때 새로 고침을 자동으로 호출 여부를 지정 합니다. |
| RenderMode | 열거형 (블록, 인라인) | 서 콘텐츠를 시각적으로 표시 됩니다 지정 합니다. |
| UpdateMode | 열거형 (항상, 조건부) | UpdatePanel 부분 렌더링 하는 동안 항상 고쳐집니다 여부 또는 경우만 새로 고쳐집니다 트리거 적중 될 때 지정 합니다. |

코드 전용 속성:

| **속성 이름** | **Type** | **설명** |
| --- | --- | --- |
| IsInPartialRendering | bool | UpdatePanel은 현재 요청에 대 한 부분 렌더링을 지원 하는지 여부를 가져옵니다. |
| ContentTemplate | ITemplate | 업데이트 요청에 대 한 태그 템플릿을 가져옵니다. |
| ContentTemplateContainer | Control | 업데이트 요청에 대 한 프로그래밍 방식으로 템플릿을 가져옵니다. |
| 트리거 | UpdatePanel-TriggerCollection | 현재 UpdatePanel과 사용 하 여 연결 된 트리거 목록을 가져옵니다. |

공용 코드 메서드:

| **메서드 이름** | **Type** | **설명** |
| --- | --- | --- |
| Update) | Void | 지정 된 UpdatePanel을 프로그래밍 방식으로 업데이트합니다. 서버 요청을 트리거되지 그렇지 UpdatePanel의 부분 렌더링을 트리거할 수 있습니다. |

태그 하위 항목:

| **태그** | **설명** |
| --- | --- |
| &lt;ContentTemplate&gt; | 부분 렌더링 결과 렌더링 하는 데 사용할 태그를 지정 합니다. 자식의 &lt;asp: UpdatePanel&gt;합니다. |
| &lt;트리거&gt; | 컬렉션을 지정 *n* 이 UpdatePanel 업데이트와 연결 된 컨트롤입니다. 자식의 &lt;asp: UpdatePanel&gt;합니다. |
| &lt;asp:AsyncPostBackTrigger&gt; | 지정 된 UpdatePanel에 대 한 부분 페이지 렌더링을 호출 하는 트리거를 지정 합니다. 이 있고 해당 UpdatePanel의 하위 항목으로 컨트롤을 되지 않을 수 있습니다. 세분화 된 이벤트 이름입니다. 자식의 &lt;트리거&gt;합니다. |
| &lt;asp:PostBackTrigger&gt; | 전체 페이지 새로 고침을 발생 시키는 컨트롤을 지정 합니다. 이 있고 해당 UpdatePanel의 하위 항목으로 컨트롤을 되지 않을 수 있습니다. 세분화 된 개체입니다. 자식의 &lt;트리거&gt;합니다. |

`UpdatePanel` 컨트롤은 AJAX Extensions는 부분 렌더링 기능에 일부 걸리는 서버 쪽 콘텐츠를 구분 하는 컨트롤입니다. UpdatePanel 컨트롤을 페이지에 있을 수 있는 수에 제한이 있으며 중첩 될 수 있습니다. 각 UpdatePanel 격리는 각 수는 독립적으로 작업 (두 Updatepanel을 동시에 실행 페이지의 다른 파트를 페이지의 포스트백의 독립적인 렌더링 있을 수 있습니다).

UpdatePanel 컨트롤 트리거로-기본적으로 UpdatePanel 내에 포함 된 모든 컨트롤 주로 거래 제어 `ContentTemplate` 포스트백을 야기 하는 UpdatePanel에 대 한 트리거로 등록 됩니다. 즉, 하 UpdatePanel 사용자 정의 컨트롤을 사용 하 여 기본 데이터 바인딩된 컨트롤 (예: GridView)를 사용 하 여 사용할 수 있으며 스크립트에서 프로그래밍할 수 있습니다.

기본적으로 부분 페이지 렌더링 트리거될 때 모든 UpdatePanel 컨트롤 페이지의 새로 고쳐집니다, 그리고 이러한 작업에 대 한 트리거를 정의 하 UpdatePanel 컨트롤 여부. 예를 들어 UpdatePanel 중 하나가 단추 컨트롤을 정의 하 고 해당 단추 컨트롤을 클릭할 경우 해당 페이지에 있는 모든 UpdatePanel 컨트롤 기본적으로 새로 고쳐집니다. 이므로 기본적으로 `UpdateMode` UpdatePanel의 속성이 `Always`합니다. UpdateMode 속성을 설정할 수 있습니다 또는 `Conditional`, 즉, 하 UpdatePanel만 새로 고쳐집니다 특정 트리거 수에 도달 합니다.

## <a name="custom-control-notes"></a>사용자 지정 컨트롤 정보

모든 사용자 정의 컨트롤 또는 사용자 지정 컨트롤에 UpdatePanel은 추가할 수 있습니다. 그러나 이러한 컨트롤에 포함 된 페이지를 포함 해야 EnablePartialRendering로 속성을 사용 하 여 ScriptManager 컨트롤 **true**합니다.

한 가지 방법은 수에 대해 계정을이 보호 되는 웹 사용자 지정 컨트롤을 사용 하는 경우 `CreateChildControls()` 메서드는 `CompositeControl` 클래스입니다. 이 작업을 수행 하면 주입할 수 있는 UpdatePanel 컨트롤의 자식 외부 세계 사이의 페이지에서 부분 렌더링을 지원 합니다. 확인 한 경우 컨테이너에 자식 컨트롤이 단순히 넣을 수이 고, 그렇지 `Control` 인스턴스.

## <a name="updatepanel-considerations"></a>UpdatePanel 고려 사항

UpdatePanel은 JavaScript XMLHttpRequest의 컨텍스트 내에서 ASP.NET 포스트백을 래핑하는 블랙 박스의 것으로 작동 합니다. 단, 동작 및 속도 측면에서 기억해 야 할 중요 한 성능 고려 사항이 있습니다. UpdatePanel의 작동 방식을 이해, 사용이 적절 한 경우를 가장 잘 결정할 수 있습니다를 AJAX exchange를 검사 해야 합니다. 다음 예제에서는 (Firebug는 XMLHttpRequest 데이터 캡처) Firebug 확장을 기존 사이트와, Mozilla Firefox를 사용 합니다.

폼을, 무엇 보다도 폼 이나 컨트롤에 city 및 state 필드를 채우는 해야 하는 우편 번호 textbox는 것이 좋습니다. 이 폼은 궁극적으로 사용자의 이름, 주소 및 연락처 정보를 포함 한 멤버 자격 정보를 수집 합니다. 특정 프로젝트 요구 사항에 기반을 고려해 야 할 많은 디자인 고려 사항이 있습니다.


[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image11.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image10.png)

([클릭 하 여 큰 이미지 보기](understanding-partial-page-updates-with-asp-net-ajax/_static/image12.png))


[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image14.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image13.png)

([클릭 하 여 큰 이미지 보기](understanding-partial-page-updates-with-asp-net-ajax/_static/image15.png))


이 응용 프로그램의 원래 반복 우편 번호, 도시 및 상태를 포함 하 여 사용자 등록 데이터의 전체를 통합 하는 컨트롤을 구축 되었습니다. 전체 컨트롤 UpdatePanel 내 래핑되고 웹 폼으로 삭제 되었습니다. 사용자가 우편 번호를 입력 하면 UpdatePanel 이벤트 (백 엔드, 또는 트리거를 지정 하 여 true로 ChildrenAsTriggers 속성 집합을 사용 하 여 해당 TextChanged 이벤트)를 검색 합니다. FireBug에서 확보 UpdatePanel에 있는 필드의 모든 AJAX 포스트백 (오른쪽 다이어그램 참조).

화면 캡처에 표시 하는 대로 모든 컨트롤이 UpdatePanel 내에서 값 전달 됩니다 (이 경우 모두 비어 있는), ViewState 필드 뿐만 아니라 합니다. 모든, told 넘는 9 (kb) 데이터 전송 됩니다만 5 바이트 데이터를이 특정 요청에 실제로 필요한 경우. 응답은 훨씬 더 커지면: 전체적으로 57 kb 보낼 클라이언트에 단순히 텍스트 필드 및 드롭다운 필드를 업데이트 합니다.

ASP.NET AJAX는 프레젠테이션을 업데이트 하는 방법을 확인 하려면 관심 수도 있습니다. UpdatePanel의 업데이트에 대 한 요청의 응답 부분 왼쪽; Firebug 콘솔 디스플레이에 표시 됩니다. 이 클라이언트 스크립트를 통해 분할 되 고 페이지의 리 어셈블합니다 특별히 작성 파이프로 구분 된 문자열. 특히, ASP.NET AJAX를 설정 합니다 *innerHTML* 하 UpdatePanel을 나타내는 클라이언트에서 HTML 요소의 속성입니다. 브라우저 DOM를 다시 생성할 때 처리 해야 하는 정보의 양에 따라 약간의 지연 합니다.

DOM의 재생성 다양을 한 추가 문제를 트리거합니다.


[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image17.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image16.png)

([클릭 하 여 큰 이미지 보기](understanding-partial-page-updates-with-asp-net-ajax/_static/image18.png))


- 포커스가 있는 HTML 요소 UpdatePanel 내에 있으면 포커스가 사라집니다. 따라서 우편 텍스트 상자를 종료 하려면 Tab 키를 누르면 사용자에 대 한 다음 대상 되었을 City 텍스트 상자입니다. 그러나 UpdatePanel 새로 표시 되 면 폼은 더 이상 포커스를 하며 Tab 키를 누르면 시작 포커스 요소 (예: 링크)를 강조 표시 합니다.
- 모든 유형의 사용자 지정 클라이언트 쪽 스크립트 사용 중인 경우 함수에 의해 액세스 DOM 요소에 대 한 참조 유지 되도록 될 수 있습니다 존재 하지 않는 부분 포스트백 후.

범용 솔루션 되도록 Updatepanel은 사용 하는 것이 없습니다. 아니라 빠른 해결책 상황, 프로토타입 생성, 작은 컨트롤 업데이트를 포함 하 여 특정 제공 하 고.NET 개체 모델을 잘 알고 있지만 DOM을 사용 하 여 덜 있으므로 있을 수 있는 ASP.NET 개발자에 게 친숙 한 인터페이스를 제공 합니다. 응용 프로그램 시나리오에 따라 성능이 향상 될 수 있는 대안의 수 있습니다.

- 개발자가 웹 서비스 호출을 호출한 되 처럼 페이지에 정적 메서드를 호출할 수 있습니다 PageMethods 및 JSON (JavaScript Object Notation)을 사용 하는 것이 좋습니다. 메서드는 정적 이므로 상태가 필요 합니다. 스크립트 호출자에 게 매개 변수를 제공 하 고 결과 비동기적으로 반환 됩니다.
- 단일 컨트롤을 응용 프로그램 간에 여러 위치에서 사용 해야 하는 경우 JSON을 웹 서비스를 사용 하는 것이 좋습니다. 이 다시 특별 한 작업이 거의 필요 하며 비동기적으로 작동 합니다.

웹 서비스 또는 페이지 메서드를 통해 기능을 통합 하는 것에 단점이 있습니다. 무엇 보다도, ASP.NET 개발자에 게 일반적으로 사용자 컨트롤 (.ascx 파일)에 기능의 작은 구성 요소를 작성 하는 경향이 있습니다. 이러한 파일에서 페이지 메서드를 호스팅할 수 없습니다. 실제.aspx 페이지 클래스 내에서 호스팅해야 합니다. 마찬가지로, 웹 서비스.asmx 클래스 내에서 호스트 되어야 합니다. 응용 프로그램에 따라이 아키텍처는 단일 구성 요소에 대 한 기능을 이제 거의 또는 전혀 응집력 ties를 가질 수 있는 두 개 이상의 실제 구성에 걸쳐 단일 책임 원칙을 위반할 수 있습니다.

마지막으로, 응용 프로그램에 Updatepanel 사용 되 고 필요한 경우 다음 지침 문제 해결 및 유지 관리를 사용 하 여 지원 해야 합니다.

- **코드 단위에서 뿐만 아니라 Updatepanel을 최소화 뿐만 아니라 내-단위를 중첩 합니다.** 예를 들어 UpdatePanel를 제어 하는 UpdatePanel을 포함 하는 다른 컨트롤을 포함 하는 UpdatePanel을 포함 하는 동안 컨트롤을 래핑하는 페이지에는 것이 단위 간 중첩 합니다. 이렇게 하면 명확한 유지 요소 새로 고침, 이어야 하며 자식 Updatepanel에 예기치 않은 새로 고침을 방지 합니다.
- **유지 된 *ChildrenAsTriggers* 속성을 false로 설정 하 고 이벤트 트리거를 명시적으로 설정 합니다.** 활용 하 여 `<Triggers>` 수집 이벤트를 처리 하는 훨씬 더 명확 하 게 방법 및 예기치 않은 동작을 유지 관리 작업을 사용 하 여 하 고 이벤트에 대 한 옵트인 하는 개발자를 강제 적용 하지 못할 수 있습니다.
- **가능한 가장 작은 단위를 사용 하 여 기능을 활용할 수 있습니다.** 서버, 총 처리 및 클라이언트-서버 exchange의 공간에 시간을 단축 하는 최소 사항만 래핑 우편 서비스를 논의에서 언급 했 듯이 성능 향상.

## <a name="the-updateprogress-control"></a>UpdateProgress 컨트롤

## <a name="updateprogress-control-reference"></a>UpdateProgress 컨트롤 참조

속성 태그 지원:

| **속성 이름** | **Type** | **설명** |
| --- | --- | --- |
| AssociatedUpdate-PanelID | 문자열 | 이 UpdateProgress에 보고 해야 하는 UpdatePanel의 ID를 지정 합니다. |
| 기능에서는 DisplayAfter | Int | 비동기 요청이 시작 된 후이 컨트롤이 표시 되기 전에 제한 시간을 밀리초 단위로 지정 합니다. |
| DynamicLayout | bool | 진행률을 동적으로 렌더링 되는지 여부를 지정 합니다. |

태그 하위 항목:

| **태그** | **설명** |
| --- | --- |
| &lt;ProgressTemplate&gt; | 이 컨트롤을 사용 하 여 표시 되는 콘텐츠에 대 한 설정 제어 템플릿을 포함 합니다. |

UpdateProgress 컨트롤 정도의 한 서버로 전송 하는 데 필요한 작업을 수행 하는 동안 사용자의 관심을 유지 하는 피드백을 제공 합니다. 이 사용자에 게는 수행 하는 것과 대부분의 사용자는 페이지를 새로 고치고 강조 표시 상태 표시줄을 표시 하는 데 특히 되지 경우에 도움이 됩니다.

참고로 UpdateProgress 컨트롤 페이지 계층의 아무 곳 이나 나타날 수 있습니다. 그러나 자식 (여기서는 UpdatePanel 내에 중첩 된 다른 UpdatePanel) UpdatePanel에서에서 부분 포스트백을 시작 하는 경우에는 트리거 UpdatePanel 자식에 대 한 템플릿을 표시 하지 UpdateProgress 하면 자식 포스트백 UpdatePanel 뿐만 아니라 UpdatePanel 부모입니다. 그러나 경우 부모 UpdatePanel의 직계 자식이 부모와 연결 된 UpdateProgress 템플릿만 표시 됩니다.

## <a name="summary"></a>요약

Microsoft ASP.NET AJAX 확장 웹 콘텐츠를 보다 쉽게 액세스할 수 있도록 지 원하는 웹 응용 프로그램에 풍부한 사용자 환경을 제공 하도록 고안 된 복잡 한 제품이 있습니다. ASP.NET AJAX Extensions, 부분 페이지 렌더링 컨트롤의 일부로 ScriptManager, UpdatePanel 및 UpdateProgress 컨트롤을 포함 하 여은 일부 도구 키트의 두드러진 구성 요소입니다.

ScriptManager 구성 요소 확장을 위한 클라이언트 JavaScript 프로 비전 통합 뿐만 아니라 최소한의 개발 투자와 함께 작동 하도록 다양 한 서버 및 클라이언트 쪽 구성 요소를 사용 하도록 설정 합니다.

UpdatePanel 컨트롤은 명백한 magic 상자-UpdatePanel 내의 태그 서버 쪽 코드 숨김 파일을 포함할 수 있으며 페이지 새로 고침을 트리거하지 않습니다. UpdatePanel 컨트롤을 중첩할 수 및 다른 Updatepanel 컨트롤에 따라 달라질 수 있습니다. 기본적으로 Updatepanel이이 기능은 세밀 하 게 튜닝할 수를 선언적으로 또는 프로그래밍 방식으로 하지만 해당 하위 컨트롤을 호출한 모든 포스트백을 처리 합니다.

UpdatePanel 컨트롤을 사용 하는 경우에 개발자가 잠재적으로 발생 하는 성능에 미치는 영향을 알고 있어야 합니다. 잠재적인 대체 응용 프로그램의 디자인 고려해 야 하지만 웹 서비스 및 페이지 메서드를 포함 됩니다.

컨트롤을 사용 하면 증명, 무시 되지 않습니다 하는 백그라운드 요청 진행 된 페이지가 있는 동안 없는 알아야 UpdateProgress 사용자 입력에 응답할 작업을 수행 합니다. 또한 부분 렌더링 결과 중단 하는 기능을 포함 합니다.

함께 이러한 도구는 서버 작업을 사용자에 게 덜 명확 하 고 워크플로 덜 방해 하 여 풍부 하 고 원활한 사용자 환경을 구축을 지원 합니다.

## <a name="bio"></a>사용자 정보

Scott Cate 1997 년부터 Microsoft 웹 기술을 사용 하 여 왔습니다 이며 myKB.com의 대표이사로 서 ([www.myKB.com](http://www.myKB.com)) ASP.NET 작성 전문적 기반 응용 프로그램 기술 자료 소프트웨어 솔루션에 집중 합니다. Scott 전자 메일을 통해 연락할 수 있습니다 [ scott.cate@myKB.com ](mailto:scott.cate@myKB.com) 저자의 블로그 또는 [ScottCate.com](http://ScottCate.com)

> [!div class="step-by-step"]
> [다음](understanding-asp-net-ajax-updatepanel-triggers.md)
