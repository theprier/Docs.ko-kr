---
uid: web-forms/overview/moving-to-aspnet-20/server-controls
title: 서버 컨트롤 | Microsoft Docs
author: microsoft
description: ASP.NET 2.0에는 여러 가지 방법으로 서버 컨트롤을 향상 시킵니다. 이 단원에서는 ASP.NET 2.0 방법 및 Visual Studio 200에 대 한 아키텍처 변경 사항 중 일부 설명 합니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2005
ms.topic: article
ms.assetid: 43f6ac47-76fc-4cf7-8e9f-c18ce673dfd8
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/server-controls
msc.type: authoredcontent
ms.openlocfilehash: 72e9cac7cf9a01791c30783fa56ad7ea205a5a11
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
ms.locfileid: "28885195"
---
<a name="server-controls"></a>서버 컨트롤
====================
by [Microsoft](https://github.com/microsoft)

> ASP.NET 2.0에는 여러 가지 방법으로 서버 컨트롤을 향상 시킵니다. 이 단원에서는 ASP.NET 2.0 하는 방법에 대 한 아키텍처 변경 사항 중 일부 다루게 될 것 및 Visual Studio 2005 서버 컨트롤을 처리 합니다.


ASP.NET 2.0에는 여러 가지 방법으로 서버 컨트롤을 향상 시킵니다. 이 단원에서는 ASP.NET 2.0 하는 방법에 대 한 아키텍처 변경 사항 중 일부 다루게 될 것 및 Visual Studio 2005 서버 컨트롤을 처리 합니다.

## <a name="view-state"></a>상태 보기

뷰 상태에 ASP.NET 2.0의 주요 변경 작업은 크기가 크게 절감 합니다. 달력 컨트롤에 있는 페이지를 고려 합니다. ASP.NET 1.1에서 뷰 상태 다음과 같습니다.

[!code-css[Main](server-controls/samples/sample1.css)]

이제 여기는 보기 상태와 동일한 페이지에서 ASP.NET 2.0입니다.

[!code-css[Main](server-controls/samples/sample2.css)]

매우 중요 한 변경 된 주며 뷰 상태 연결을 통해 앞뒤로 수행을 고려이 변경 수 개발자 성능이 많이 향상 합니다. 상태 보기의 크기를 줄이는 것 내부적으로 처리 하는 방식 때문 크게입니다. 뷰 상태는 Base64 인코딩된 문자열을 기억 합니다. ASP.NET 2.0에서 뷰 상태 변경을 더 잘 이해 하려면 위 예제에서 디코딩된 값 살펴보겠습니다 죠.

디코딩된 1.1 뷰 상태는 다음과 같습니다.

[!code-css[Main](server-controls/samples/sample3.css)]

이 값은 알 수 없는, 처럼 약간 보일 수 있지만 패턴을 있습니다. ASP.NET에서 1.x에서는 사용 되지 않는 단일 문자 데이터 형식을 식별 하 고 사용 하 여 값을 구분는 &lt; &gt; 문자입니다. 위의 보기 상태 예제에서 "t"는 세 개를 나타냅니다. 세 개 포함 한 쌍의 ArrayLists ("l" ArrayList를 나타냅니다.) 이러한 ArrayLists 중 하나는 i n t 32에 포함 ("i") 값이 1과 다른 다른 세 개를 포함 합니다. 세 개 ArrayLists 등 쌍을 포함 합니다. 쌍을 포함 하는 개가 형식이 사용, 우리에 문자를 통해 데이터 형식을 식별 하 고 사용 하 여 기억 하는 것이 중요은 &lt; 및 &gt; 문자 구분 기호로 사용 합니다.

ASP.NET 2.0에서 디코딩된 뷰 상태 약간 다르게 보입니다.

[!code-powershell[Main](server-controls/samples/sample4.ps1)]

디코딩된 뷰 상태의 모양이 크게 변화를 확인 해야 합니다. 이러한 변경에 몇 가지 아키텍처 토대가 있습니다. 뷰 상태는 LosFormatter 데이터를 직렬화 하 1.x ASP.NET에서 사용 합니다. 2.0에서는 새로운 ObjectStateFormatter 클래스를 사용 했습니다. 이 클래스는 serialization 및 deserialization 상태 보기 상태와 컨트롤을 지원 하기 위해 특별히 설계 되었습니다. (컨트롤 상태는 다음 섹션 살펴보겠습니다.) 기준인 serialization 및 deserialization을 수행 하는 방법을 변경 하 여 얻은 많은 이점이 있습니다. 가장 큰 중 하나는 TextWriter를 사용 하 여 LosFormatter 달리는 ObjectStateFormatter 사용 BinaryWriter 사실입니다. 따라서 ASP.NET 2.0 바이트 문자열 대신 일련 뷰 상태를 저장할 수 있습니다. 예를 들어 정수를 사용 합니다. ASP.NET 1.1 정수 4 바이트의 뷰 상태를 필요합니다. ASP.NET 2.0에서이 동일한 정수 1 바이트가 필요합니다. 저장 된 뷰 상태 불필요 한 다른 개선 되었습니다. 날짜/시간 값을 예를 들어 이제 저장 됩니다는 TickCount를 사용 하 여 문자열 대신.

아직 충분 하지 그 하는 경우 특별히 주의 기울여야 DataGrid와 비슷한 컨트롤이 가장 큰 소비자 1.x에서 뷰 상태 중 하나에 팩트로 지불 합니다. 같은 뷰 상태 관련 되어 DataGrid 컨트롤의 주요 단점은 대량의 반복 되는 정보가 종종 포함 한다는 점입니다. ASP.NET에서 1.x 및에 비해 너무 커지면된 뷰 상태에 다시 결과 단순히 정보가 저장 된 반복 합니다. ASP.NET 2.0을 사용 하 여 새 IndexedString 클래스 이러한 데이터를 저장 합니다. 문자열 반복 되는 경우는 IndexedString 및 IndexedString 개체의 실행 중인 테이블에서 인덱스에 대 한 토큰만 저장 합니다.

## <a name="control-state"></a>컨트롤 상태

뷰 상태와 함께 개발자 있던 주요 gripes 하나인 HTTP 페이로드를 추가 하는 크기입니다. 에서 설명한 대로 DataGrid 컨트롤 뷰 상태의 가장 큰 소비자 중 하나입니다. 많은 양의 DataGrid에 의해 생성 된 뷰 상태를 방지 하려면 많은 개발자에 게 해당 컨트롤에 대 한 뷰 상태를 단순히 사용할 수 없습니다. 그러나 해당 솔루션에 적절 한 항상 없습니다. 뷰 상태 1.x ASP.NET에서 컨트롤의 올바른 작동을 위해 필요한 데이터 뿐만 아니라를 포함 합니다. 또한 컨트롤의 UI 상태에 대 한 정보를 포함 합니다. 이 모든 UI 정보를 볼 필요가 없는 경우에 뷰 상태를 사용 하도록 설정 해야 DataGrid에 페이지 매김 허용 하려는 경우 상태 포함 되어 있음을 의미 합니다. 동작만 있는 시나리오는

ASP.NET 2.0 컨트롤 상태 컨트롤 상태의 도입을 통해 원활 하 게 문제를 해결합니다. 컨트롤 상태 컨트롤의 적절 한 기능에 반드시 필요한 데이터를 포함 합니다. 뷰 상태와는 달리 컨트롤 상태를 해제할 수 없습니다. 따라서이 컨트롤 상태에 저장 되는 데이터 신중 하 게 제어는 중요 합니다.

> [!NOTE]
> 제어 상태에서 뷰 상태와 함께 유지 되는 \_ \_VIEWSTATE 숨겨진된 양식 필드입니다.


이 비디오는 상태 보기 상태와 컨트롤의 연습입니다.


![](server-controls/_static/image1.png)


[전체 화면 비디오 열기](server-controls/_static/state1.wmv)


읽기 / 쓰기 상태를 제어를 위해 서버 컨트롤에 대 한 순서로 세 단계를 수행 해야 합니다.

## <a name="step-1-call-the-registerrequirescontrolstate-method"></a>1 단계: RegisterRequiresControlState 메서드를 호출 합니다.

RegisterRequiresControlState 메서드 컨트롤 컨트롤 상태를 유지 해야 함을 ASP.NET에 알립니다. 컨트롤인 등록 되는 컨트롤 형식의 인수 하나를 사용 합니다.

등록 요청 요청 지속 되지 않는 확인 하는 것이 유용 합니다. 따라서이 메서드 컨트롤 상태를 유지 하는 컨트롤이 이면 모든 요청에 대해 호출 되어야 합니다. OnInit에서 메서드를 호출 하는 것이 좋습니다.

[!code-csharp[Main](server-controls/samples/sample5.cs)]

## <a name="step-2-override-savecontrolstate"></a>2 단계: SaveControlState 재정의

SaveControlState 메서드 다시 마지막 게시 이후로 컨트롤 컨트롤에 대 한 상태 변경 내용을 저장합니다. 컨트롤의 상태를 나타내는 개체를 반환 합니다.

## <a name="step-3-override-loadcontrolstate"></a>3 단계: LoadControlState 재정의

LoadControlState 메서드 컨트롤에 저장 된 상태를 로드합니다. 메서드는 개체는 컨트롤에 대 한 저장된 된 상태를 보유 하는 형식의 인수 하나를 사용 합니다.

## <a name="full-xhtml-compliance"></a>전체 XHTML 규정 준수

모든 웹 개발자는 웹 응용 프로그램의 표준의 중요성을 알고 있습니다. 표준 기반 개발 환경을 유지 하기 위해 ASP.NET 2.0은 XHTML 호환 완벽 하 게 합니다. 따라서 모든 태그는 HTML 4.0을 지 원하는 브라우저에서 XHTML 표준에 따라 렌더링 이상입니다.

ASP.NET 1.1에서 DOCTYPE 정의 다음과 같습니다.

[!code-html[Main](server-controls/samples/sample6.html)]

ASP.NET 2.0에서 기본 문서 종류 정의 다음과 같습니다.

[!code-html[Main](server-controls/samples/sample7.html)]

를 선택한 경우에 구성 파일에서 xhtmlConformance 노드를 통해 기본 XHML 규정 준수를 변경할 수 있습니다. 예를 들어 web.config 파일에서 다음 노드 XHTML 1.0 Strict로 XHTML 규정 준수를 변경 합니다.

[!code-xml[Main](server-controls/samples/sample8.xml)]

을 선택 하면 ASP.NET에서 사용 되는 레거시 구성을 사용 하려면 ASP.NET 구성할 수도 있습니다 다음과 같이 1.x:

[!code-xml[Main](server-controls/samples/sample9.xml)]

## <a name="adaptive-rendering-using-adapters"></a>어댑터를 사용 하 여 렌더링 적응

ASP.NET에서 1.x, 포함 된 구성 파일을 &lt;browserCaps&gt; HttpBrowserCapabilities 개체를 채우는 섹션. 이 개체는 개발자가 어떤 장치는 특정 요청을 수행할 결정 및 코드를 적절 하 게 표시할 수 있습니다. ASP.NET 2.0에서 모델이 개선 하 고 이제 새 ControlAdapter 클래스를 사용 합니다. ControlAdapter 클래스는 컨트롤의 수명 주기에서 이벤트를 재정의 하 고 사용자 에이전트의 기능에 따라 컨트롤의 렌더링을 제어 합니다. 특정 사용자 에이전트의 기능에는 c:\windows\microsoft.net\framework\v2.0 저장 브라우저 정의 파일 (브라우저 파일 확장명으로 파일)에 정의 됩니다. \* \* \* \*\CONFIG\Browsers 폴더입니다.

> [!NOTE]
> ControlAdapter 클래스는 추상 클래스입니다.


과 거의 동일한는 &lt;browserCaps&gt; 1.x 브라우저 정의 파일의에서 섹션을 요청 하는 브라우저를 식별 하기 위해 사용자 에이전트 문자열을 구문 분석 정규식을 사용 합니다. 이 해당 사용자 에이전트에 대 한 특정 기능을 정의 하 합니다. ControlAdapter Render 메서드를 통해 컨트롤을 렌더링 합니다. 따라서 Render 메서드를 재정의 하면에서 호출 하지 않아야 렌더링 기본 클래스입니다. 이렇게 하면 어댑터에 대해 한 번씩 하 고 컨트롤 자체에 대 한 한 번, 두 번 발생 하도록 렌더링 발생할 수 있습니다.

## <a name="developing-a-custom-adapter"></a>사용자 지정 어댑터 개발

ControlAdapter에서 상속 하 여 사용자 지정 어댑터를 개발할 수 있습니다. 또한 어댑터는 페이지에 대 한 필요한 상황의 경우 PageAdapter 추상 클래스에서 상속할 수 있습니다. 컨트롤을 사용자 지정 어댑터의 매핑을 통해 수행 됩니다는 &lt;controlAdapters&gt; 브라우저 정의 파일의 요소입니다. 예를 들어 브라우저 정의 파일에서 다음과 같은 XML 메뉴 어댑터 클래스에 메뉴 컨트롤을 매핑합니다.

[!code-html[Main](server-controls/samples/sample10.html)]

컨트롤 개발자가 특정 장치 또는 브라우저를 대상에 대 한 매우 쉽게 됩니다이 모델을 사용 합니다. 모든 장치에서 페이지가 렌더링 되는 방식을 완전히 제어 하는 개발자에 대 한 매우 간단 이기도 합니다.

## <a name="per-device-rendering"></a>장치 단위 렌더링

ASP.NET 2.0에서 서버 컨트롤 속성에 지정 된 장치는 브라우저의 접두사를 사용 하 여 수 있습니다. 예를 들어 아래 코드 페이지를 검색 하는 장치 사용량에 따라 레이블의 텍스트를 변경 됩니다.

[!code-aspx[Main](server-controls/samples/sample11.aspx)]

레이블이 "탐색 하는 Internet Explorer에서." 라는 텍스트를 표시할 수 Internet Explorer에서이 레이블을 포함 하는 페이지를 찾아볼 때 Firefox에서 페이지를 찾아볼 때는 표시 될 텍스트 "Firefox에서 이동 하는 있습니다." 다른 모든 장치에서 페이지를 찾아볼 때 표시될지 "알 수 없는 장치에서 이동 하는 있습니다." 이 특수 구문을 사용 하 여 모든 속성을 지정할 수 있습니다.

## <a name="setting-focus"></a>포커스 설정

ASP.NET 1.x 개발자가 특정 컨트롤에 초기 포커스를 설정 하는 방법에 대 한 질문과 대답입니다. 예를 들어 로그인 페이지에서 페이지 처음 로드 될 때 포커스를 가져올 사용자 ID 텍스트 상자에 있어야는 것이 유용 합니다. ASP.NET이 1.x 일부 클라이언트 쪽 스크립트를 작성할 필요 합니다. 이러한 스크립트는 간단한 작업이, 이지만 SetFocus 메서드 덕분에 ASP.NET 2.0에서 필요는 더 이상입니다. SetFocus 메서드 포커스 받아야 하는 제어를 표시 하는 하나의 인수를 사용 합니다. 이 인수를 문자열로 컨트롤의 클라이언트 ID 또는 제어 개체로 서버 컨트롤의 이름을 수 있습니다. 예를 들어 초기 포커스 페이지가 처음 로드 될 때 txtUserID 호출 TextBox 컨트롤을 설정 하려면 페이지에 다음 코드 추가\_부하:

[!code-csharp[Main](server-controls/samples/sample12.cs)]

-또는

[!code-csharp[Main](server-controls/samples/sample13.cs)]

ASP.NET 2.0 (이전에 설명) Webresource.axd 처리기를 사용 하 여 포커스를 설정 하는 클라이언트 쪽 함수 렌더링. 클라이언트 쪽 함수 이름은 WebForm\_AutoFocus 다음과 같이 합니다.

[!code-html[Main](server-controls/samples/sample14.html)]

또는 해당 컨트롤에 초기 포커스를 설정 하는 컨트롤에 대 한 포커스 메서드를 사용할 수 있습니다. 포커스 메서드 Control 클래스에서 파생 되 고 모든 ASP.NET 2.0 컨트롤에 사용할 수 있습니다. 유효성 검사 오류가 발생 하는 경우 특정 컨트롤에 포커스를 설정 하는 것도 가능 합니다. 이후 단원에서 설명 합니다.

## <a name="new-server-controls-in-aspnet-20"></a>ASP.NET 2.0의에서 새로운 서버 컨트롤

ASP.NET 2.0의 새로운 서버 컨트롤은 다음과 같습니다. 이후 모듈에서 그 중 일부에 대해 좀 더 자세히 이동지 것입니다.

## <a name="imagemap-control"></a>ImageMap 컨트롤

ImageMap 컨트롤을 사용 하면 핫스폿 다시 게시를 시작 하거나 URL을 탐색할 수 있는 이미지를 추가할 수 있습니다. 세 가지가 핫스폿에의 사용할 수 있습니다. CircleHotSpot, RectangleHotSpot, 및 PolygonHotSpot 합니다. 핫스팟 Visual Studio 또는 프로그래밍 방식으로 코드에서 컬렉션 편집기를 통해 추가 됩니다. 이미지에 핫스폿 그리기에 사용할 수 있는 사용자 인터페이스 없이 있습니다. 좌표 및 크기 또는 핫 스폿의 반지름을 선언적으로 지정 되어야 합니다. 디자이너에서 핫스팟의 시각적 표시가 이기도합니다. 핫스팟을 URL로 이동한 다음에 구성 된 경우 URL 핫 스폿의 NavigateUrl 속성을 통해 지정 됩니다. 게시의 경우 속성을 사용 하면 서버 쪽 코드에 다시 게시에서 검색할 수 있는 문자열을 전달할 수 있습니다 PostBackValue 핫스팟을 백업 합니다.


![Visual Studio에서 hotSpot 컬렉션 편집기](server-controls/_static/image1.jpg)

**그림 1**: Visual Studio에서 HotSpot 컬렉션 편집기


## <a name="bulletedlist-control"></a>BulletedList 컨트롤

BulletedList 컨트롤은 쉽게 수 있는 데이터 바인딩된 글머리 기호 목록입니다. 목록 순서를 지정할 수 (숫자) 또는 BulletStyle 속성을 통해 순서가 지정 되지 않은 합니다. 목록의 각 항목은 ListItem 개체에 의해 표시 됩니다.


![Visual Studio에서 BulletedList 컨트롤](server-controls/_static/image1.gif)

**그림 2**: Visual Studio에서 BulletedList 컨트롤


## <a name="hiddenfield-control"></a>HiddenField 컨트롤

HiddenField 컨트롤을 해당 값은 서버 쪽 코드에서 사용할 수 있는 페이지에는 숨겨진된 폼 필드를 추가 합니다. 숨겨진된 폼 필드의 값은 일반적으로 post 백업 간에 변경 되지 않고 유지 해야 합니다. 그러나 악의적인 사용자가 다시 게시 값 전에 변경에 대 한 같습니다. 이 경우 HiddenField 컨트롤 경우 재정의 발생 합니다. HiddenField 컨트롤에 중요 한 정보가 있는 경우 변경 되지 않은 상태로 유지 되는지 확인 하려는 경우 재정의 코드에서 처리 해야 합니다.

## <a name="fileupload-control"></a>파일 업로드 컨트롤

ASP.NET 2.0에서 파일 업로드 컨트롤을 사용 하면 ASP.NET 페이지를 통해 웹 서버에 파일을 업로드할 수 있습니다. 이 컨트롤은 몇 가지 예외를 사용 하 여 ASP.NET 1.x HtmlInputFile 클래스와 매우 비슷합니다. ASP.NET에서 1.x 것을 권장 했습니다 좋은 파일을 갖는 경우를 확인 하기 위해 null에 대 한 PostedFile 속성을 확인할 수 있습니다. ASP.NET 2.0에서 파일 업로드 컨트롤 같은 목적을 위해 사용할 수 있으며이 좀 더 효율적 새 HasFile 속성을 추가 합니다.

PostedFile 속성이 HttpPostedFile 개체에 대 한 액세스를 위해 계속 사용할 수 이지만 이제 파일 업로드 컨트롤 기본적으로 사용할 수는 HttpPostedFile 기능 중 일부입니다. 예를 들어, ASP.NET에 업로드 된 파일을 저장 하려면 HttpPostedFile 개체에서 SaveAs 메서드를 호출할 1.x 합니다. 파일 업로드 컨트롤을 사용 하 여 ASP.NET 2.0에서, 파일 업로드 컨트롤 자체에서 SaveAs 메서드를 호출 합니다.

2.0 동작 (및 가능성이 가장 중요 한 변경)의 또 다른 큰 변화가 전체 업로드 된 파일을 저장 하기 전에 메모리에 로드 하는 데 필요한 더 이상 된다는 점입니다. 1.x 업로드 된 모든 파일이 기록 되기 전에 메모리에 완전히 저장 됩니다 디스크에 있습니다. 이 아키텍처는 큰 파일 업로드를 방지합니다.

ASP.NET 2.0에서 requestLengthDiskThreshold 특성 httpRuntime 요소의 크기를 구성할 수 있습니다 기록 되기 전에 메모리에 버퍼에 저장 된 디스크에 있습니다.

**중요 한**:이 값 (킬로바이트) (바이트)에서 이며 기본값은 256 MSDN 설명서 (및 다른 곳에서 설명서) 지정 합니다. 킬로바이트 단위로 실제로 지정 된 값 및 기본값은 80입니다. 기본값은 80 K 함으로써 대형 개체 힙에 버퍼 종료 하지 않습니다 확인 합니다.

## <a name="wizard-control"></a>마법사 컨트롤

것이 일반적 패널을 사용 하 여 "페이지" 또는 페이지를 전송 하 여 일련의 정보를 수집 하려는 ASP.NET 개발자 발생할 수 있습니다. 것, 노력은 하면 당황 스 러 하나 이며 시간이 걸립니다. 새 Wizard 컨트롤 사용자가 잘 알고 있는 마법사 인터페이스의 선형 및 비선형 단계에 대 한 허용 하 여 문제를 해결 합니다. 마법사 컨트롤 입력된 양식 처럼 일련의 단계를 제공합니다. 각 단계는 특정 유형의 컨트롤의 StepType 속성에 지정 된 것입니다. 사용 가능한 단계 종류는 다음과 같습니다.

| **단계 유형** | **설명** |
| --- | --- |
| 자동 | 마법사는 단계의 단계 계층 구조 내에서 위치에 따라 유형을 자동으로 결정 합니다. |
| 시작 | 소개 문에 제공 자주 사용 되는 첫 번째 단계입니다. |
| 단계 | 일반적인 단계입니다. |
| 마침 | 마법사를 완료 하는 단추를 표시 하는 데 일반적으로 최종 단계입니다. |
| 완료 | 성공 또는 실패를 통신 하는 메시지를 표시 합니다. |

> [!NOTE]
> 마법사 컨트롤은 ASP.NET 컨트롤 상태를 사용 하 여 해당 상태입니다. 따라서 EnableViewState 속성 모든 단점이 없이 false로 설정할 수 있습니다.


이 비디오는 Wizard 컨트롤의 연습 과정입니다.


![](server-controls/_static/image2.png)


[전체 화면 비디오 열기](server-controls/_static/wizard1.wmv)


## <a name="localize-control"></a>컨트롤 지역화

Localize 컨트롤 리터럴 제어 하는 것과 비슷합니다. 그러나 Localize 컨트롤에는 **모드** 여기에 추가 되는 태그를 렌더링 하는 방식을 제어 하는 속성이 있습니다. 모드 속성은 다음 값을 지원합니다.

| **모드** | **설명** |
| --- | --- |
| 변형 | 태그는 요청 하는 브라우저의 프로토콜에 따라 변환 됩니다. |
| PassThrough | 로 태그를 렌더링할-됩니다. |
| 인코딩 | 컨트롤에 추가 되는 태그는 HtmlEncode를 사용 하 여 인코딩됩니다. |

## <a name="multiview-and-view-controls"></a>MultiView 및 뷰 컨트롤

MultiView 컨트롤 뷰 컨트롤에 대 한 컨테이너로 사용 하 고 View 컨트롤 컨테이너 역할을 훨씬 (패널 컨트롤)를 같은 다른 컨트롤에 대 한 키를 누릅니다. MultiView 컨트롤의 각 보기는 단일 뷰 컨트롤에서 표시 됩니다. MultiView에서 뷰 컨트롤에서 첫 번째 뷰입니다 0, 두 번째는 1, 뷰 등입니다. MultiView 컨트롤 ActiveViewIndex를 지정 하 여 보기를 전환할 수 있습니다.

## <a name="substitution-control"></a>대체 컨트롤

대체 컨트롤은 ASP.NET 캐싱와 함께에서 사용 됩니다. 캐싱, 활용 하려는 하지만 (즉, 페이지의 부분 캐싱을에서 제외 되는) 각 요청에 대해 업데이트 해야 하는 페이지의 부분에 있는 경우, 대체 구성 요소 뛰어난 솔루션을 제공 합니다. 컨트롤에서 어떠한 출력도 자체적으로 렌더링 실제로 하지 않습니다. 대신, 서버 쪽 코드의 메서드에 바인딩됩니다. 페이지 요청 되 면 메서드가 호출 되 고 대체 컨트롤 대신 반환 된 태그 렌더링 됩니다.

대체 컨트롤 연결 된 메서드를 통해 지정 됩니다는 **MethodName** 속성입니다. 해당 메서드는 다음 조건을 충족 해야 합니다.

- 정적 (VB의 경우 공유) 메서드에 이어야 합니다.
- HttpContext 형식의 매개 변수 하나를 허용합니다.
- 페이지에 컨트롤을 대체 해야 하는 태그를 나타내는 문자열을 반환 합니다.

해당 매개 변수를 통해 현재 HttpContext에 대 한 액세스는 것은 하지만 대체 컨트롤에는 페이지에 있는 다른 컨트롤을 수정할 수 없는 합니다.

## <a name="gridview-control"></a>GridView 컨트롤

GridView 컨트롤은 DataGrid 컨트롤의 대체 합니다. 이 컨트롤은 이후 단원에서 자세히 설명 합니다.

## <a name="detailsview-control"></a>DetailsView 컨트롤

DetailsView 컨트롤을 사용 하면 데이터 원본에서 단일 레코드를 표시 하 고 편집 하거나 삭제할 수 있습니다. 이후 단원에서 자세히 다룹니다.

## <a name="formview-control"></a>FormView 컨트롤

FormView 컨트롤을 사용 하 여 구성 가능한 인터페이스에 데이터 원본에서 단일 레코드를 표시 합니다. 이후 단원에서 자세히 다룹니다.

## <a name="accessdatasource-control"></a>AccessDataSource 컨트롤

AccessDataSource 컨트롤에 사용 되는 Access 데이터베이스를 바인딩할 데이터입니다. 이후 단원에서 자세히 다룹니다.

## <a name="objectdatasource-control"></a>ObjectDataSource 컨트롤

ObjectDataSource 컨트롤은 컨트롤 수 수에 데이터 바인딩된 2 계층 모델 대신 중간 계층 비즈니스 개체 데이터 소스에 직접 바인딩된은 컨트롤이 있도록 3 계층 아키텍처를 지 원하는 데 사용 됩니다. 이후 단원에서 자세히 설명 합니다.

## <a name="xmldatasource-control"></a>XmlDataSource 컨트롤

XmlDataSource 컨트롤에 XML 데이터 소스에 데이터 바인딩을 사용 됩니다. 이후 단원에서 자세히 다룹니다.

## <a name="sitemapdatasource-control"></a>SiteMapDataSource 제어

SiteMapDataSource 컨트롤 사이트 맵을 기반으로 하는 사이트 탐색 컨트롤에 대 한 데이터 바인딩을 제공 합니다. 이후 단원에서 자세히 설명 합니다.

## <a name="sitemappath-control"></a>SiteMapPath 컨트롤

SiteMapPath 컨트롤에는 일련의 breadcrumb 흔히 탐색 링크를 표시 합니다. 이후 단원에서 자세히 다룹니다.

## <a name="menu-control"></a>Menu 컨트롤

Menu 컨트롤 DHTML을 사용 하 여 동적 메뉴를 표시 합니다. 이후 단원에서 자세히 다룹니다.

## <a name="treeview-control"></a>TreeView 컨트롤

TreeView 컨트롤을 사용 하 여 데이터의 계층적 트리 뷰를 표시 합니다. 이후 단원에서 자세히 다룹니다.

## <a name="login-control"></a>Login 컨트롤

웹 사이트에 로그인 하는 메커니즘에 대 한 로그인 제어를 제공 합니다. 이후 단원에서 자세히 다룹니다.

## <a name="loginview-control"></a>LoginView 컨트롤

LoginView 컨트롤 허용 사용자의 로그인 상태에 따라 서로 다른 템플릿 표시 합니다. 이후 단원에서 자세히 다룹니다.

## <a name="passwordrecovery-control"></a>PasswordRecovery 제어

PasswordRecovery 컨트롤은 ASP.NET 응용 프로그램의 사용자가 잊어버린된 암호 검색에 사용 됩니다. 이후 단원에서 자세히 다룹니다.

## <a name="loginstatus"></a>LoginStatus

LoginStatus 컨트롤은 사용자의 로그인 상태를 나타냅니다. 이후 단원에서 자세히 다룹니다.

## <a name="loginname"></a>LoginName

LoginName 컨트롤 후 ASP.NET 응용 프로그램에 로그인 하는 사용자의 사용자 이름을 표시 합니다. 이후 단원에서 자세히 다룹니다.

## <a name="createuserwizard"></a>CreateUserWizard

CreateUserWizard는 사용자가 ASP.NET 응용 프로그램에서 사용 하기 위해 ASP.NET 멤버 자격 계정을 만들 수 있도록 구성할 수 있는 마법사입니다. 이후 단원에서 자세히 다룹니다.

## <a name="changepassword"></a>ChangePassword

ChangePassword 컨트롤을 사용 하면 ASP.NET 응용 프로그램에 대 한 암호를 변경할 수 있습니다. 이후 단원에서 자세히 다룹니다.

## <a name="various-webparts"></a>다양 한 웹 파트

ASP.NET 2.0 웹 파트를 다양 한 함께 제공 됩니다. 이후 단원에서 자세히 설명 합니다.
