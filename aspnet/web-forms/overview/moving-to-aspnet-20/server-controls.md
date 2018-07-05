---
uid: web-forms/overview/moving-to-aspnet-20/server-controls
title: 서버 컨트롤 | Microsoft Docs
author: microsoft
description: ASP.NET 2.0에는 여러 가지 방법으로 서버 컨트롤 강화합니다. 이 모듈에서는 다루게 방식으로 ASP.NET 2.0 및 Visual Studio 200 아키텍처 변경 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2005
ms.topic: article
ms.assetid: 43f6ac47-76fc-4cf7-8e9f-c18ce673dfd8
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/server-controls
msc.type: authoredcontent
ms.openlocfilehash: 989986c45e76a65582f35172c7d837a78484d09a
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37374226"
---
<a name="server-controls"></a>서버 컨트롤
====================
[Microsoft](https://github.com/microsoft)

> ASP.NET 2.0에는 여러 가지 방법으로 서버 컨트롤 강화합니다. 이 단원에서는 ASP.NET 2.0 방법 아키텍처 변경 사항 중 일부를 다룹니다 및 서버 컨트롤을 사용 하 여 Visual Studio 2005를 처리 합니다.


ASP.NET 2.0에는 여러 가지 방법으로 서버 컨트롤 강화합니다. 이 단원에서는 ASP.NET 2.0 방법 아키텍처 변경 사항 중 일부를 다룹니다 및 서버 컨트롤을 사용 하 여 Visual Studio 2005를 처리 합니다.

## <a name="view-state"></a>뷰 상태

뷰 상태에 ASP.NET 2.0의 주요 변경 내용은 크기가 크게 감소 하는 합니다. 달력 컨트롤에 있는 페이지를 고려해 야 합니다. ASP.NET 1.1에서 뷰 상태는 다음과 같습니다.

[!code-css[Main](server-controls/samples/sample1.css)]

이제 여기 보기 상태가입니다 동일한 페이지에 ASP.NET 2.0.

[!code-css[Main](server-controls/samples/sample2.css)]

상당한 변경 하는 고 뷰 상태 연결을 통해 앞뒤로 전달 되는 고려,이 변경 보일 수 있습니다 개발자 성능을 크게 향상 합니다. 에서는 내부적으로 처리 하는 방식으로 인해 주로 보기 상태의 크기를 줄이는 경우 보기 상태는 Base64로 인코딩된 문자열을 기억 합니다. ASP.NET 2.0의 뷰 상태 변경에 더 잘 이해 하려면 위 예제에서 디코딩된 값 보도록 하겠습니다.

디코딩된 1.1 뷰 상태는 다음과 같습니다.

[!code-css[Main](server-controls/samples/sample3.css)]

이 값은 알 수 없는, 처럼 약간 보일 수 있습니다 이지만 여기에 패턴입니다. Asp.net에서 1.x에서 사용 되는 단일 문자 데이터 형식을 식별 하 고 사용 하 여 값을 구분 합니다 &lt; &gt; 문자입니다. 위의 보기 상태 샘플에서 "t"를 세 개를 나타냅니다. ArrayLists ("l" ArrayList를 나타냅니다.)의 쌍을 포함 하는 세 개 Int32를 포함 하는 이러한 ArrayLists 중 하나 ("i") 1과 다른 값을 사용 하 여 다른 세 개를 포함 합니다. 세 개 ArrayLists 등 쌍을 포함 합니다. 중요 한 점은 Triplets 쌍을 포함 하는 사용에 문자를 통해 데이터 형식 식별을 사용 합니다 &lt; 및 &gt; 구분 기호 문자로 합니다.

ASP.NET 2.0의 디코딩된 뷰 상태를 약간 다르게 보입니다.

[!code-powershell[Main](server-controls/samples/sample4.ps1)]

디코딩된 보기 상태의 모양이 크게 변화 된 유의 해야 합니다. 이 변경에 몇 가지 아키텍처 기초가 있습니다. 뷰 상태를 ASP.NET 1.x 하는 데 사용 된 LosFormatter 데이터를 직렬화 합니다. 2.0에서는 새 ObjectStateFormatter 클래스를 사용합니다. 이 클래스는 직렬화 및 역직렬화의 뷰 상태 및 컨트롤 상태를 지원 하기 위해 설계 되었습니다. (컨트롤 상태는 다음 섹션에서 다룰 수 됩니다.) serialization 및 deserialization 수행 방법을 변경 하 여 얻은 많은 이점이 있습니다. 가장 큰 중 하나는 TextWriter를 사용 하는 LosFormatter, 달리는 ObjectStateFormatter 사용 BinaryWriter를 사실입니다. 따라서 ASP.NET 2.0 바이트 문자열 대신 일련 뷰 상태를 저장할 수 있습니다. 예를 들어 정수를 사용 합니다. ASP.NET 1.1 정수 4 바이트의 뷰 상태를 필요합니다. ASP.NET 2.0에는 동일한 정수 1 바이트 필요합니다. 저장 된 뷰 상태 크기를 줄이기 위해 다른 향상 되었습니다. 날짜/시간 값을 예를 들어, 이제 저장 됩니다는 TickCount를 사용 하 여 문자열 대신.

충분 하지 모든 처럼 DataGrid와 유사한 컨트롤 되었는지 1.x에서 보기 상태의 가장 큰 소비자 사실에 주의 지불 되었는지 합니다. 뷰 상태 관련이 있는 DataGrid와 같은 컨트롤의 주요 단점은 대량의 반복 되는 정보가 종종 포함 한다는 점입니다. Asp.net에서 1.x 정보 및는 보기 상태가 너무 커지면된 다시 생성을 통해 저장 된 반복입니다. ASP.NET 2.0에서는 이러한 데이터를 저장할 새 IndexedString 클래스를 사용 합니다. 문자열을 반복 하는 경우는 IndexedString 및 IndexedString 개체의 실행 중인 테이블의 인덱스에 대 한 토큰만 저장 합니다.

## <a name="control-state"></a>컨트롤 상태

뷰 상태를 사용 하 여 개발자가 있던 주요 고민을 들어 보십시오 중 하나 였습니다 크기 HTTP 페이로드를 추가할 것입니다. 앞서 언급 했 듯이, DataGrid 컨트롤 뷰 상태의 가장 큰 소비자 중 하나입니다. 방대한 양의 DataGrid에서 생성 된 뷰 상태를 방지 하려면 많은 개발자가 해당 컨트롤의 뷰 상태를 간단히 사용할 수 없습니다. 그러나 해당 솔루션 적절 한 항상 않았습니다. 뷰 상태를 asp.net에서 1.x 데이터가 뿐만 아니라 컨트롤의 올바른 작동을 위해 필요 합니다. 또한 컨트롤의 UI 상태에 관한 정보를 포함 합니다. 즉, 모든 UI 정보를 볼 필요가 없는 경우에 뷰 상태를 사용 해야 합니다는 DataGrid에서 페이지 매김 허용 하려는 경우 상태를 포함 합니다. 이 이것 아니면 저것 인 시나리오입니다.

ASP.NET 2.0 컨트롤 상태 컨트롤 상태의 도입을 통해 원활 하 게 문제를 해결합니다. 컨트롤 상태를 컨트롤의 적절 한 기능에 대 한 절대적으로 필요한 데이터를 포함 합니다. 뷰 상태와 달리 컨트롤 상태를 해제할 수 없습니다. 따라서 컨트롤 상태에 저장 되는 데이터는 신중 하 게 제어는 중요 한 것입니다.

> [!NOTE]
> 컨트롤 상태에서 뷰 상태와 함께 유지 되는 \_ \_VIEWSTATE 숨겨진된 폼 필드입니다.


이 비디오는 보기 상태 및 컨트롤 상태를 연습 합니다.


![](server-controls/_static/image1.png)


[전체 화면 비디오 열기](server-controls/_static/state1.wmv)


읽기 및 쓰기 상태를 제어 하는 서버 컨트롤에 대 한 순서 대로 세 가지 단계를 수행 해야 합니다.

## <a name="step-1-call-the-registerrequirescontrolstate-method"></a>1 단계: RegisterRequiresControlState 메서드를 호출 합니다.

RegisterRequiresControlState 메서드 컨트롤 컨트롤 상태를 유지 해야 하는 ASP.NET에 알립니다. 등록 되는 컨트롤인 컨트롤 형식의 인수 하나가 걸립니다.

등록 요청 간 지속 되지 않는 하는 것이 반드시 합니다. 따라서 컨트롤 상태를 유지 하는 것을 제어 하는 경우이 메서드는 모든 요청에서 호출 되어야 합니다. OnInit에서 메서드를 호출 하는 것이 좋습니다.

[!code-csharp[Main](server-controls/samples/sample5.cs)]

## <a name="step-2-override-savecontrolstate"></a>2 단계: SaveControlState를 재정의 합니다.

SaveControlState 메서드 마지막 포스트백 이후에 컨트롤 컨트롤에 대 한 상태 변경 내용을 저장합니다. 컨트롤의 상태를 나타내는 개체를 반환 합니다.

## <a name="step-3-override-loadcontrolstate"></a>3 단계: LoadControlState 재정의

LoadControlState 메서드는 컨트롤에 저장 된 상태를 로드합니다. 메서드는 컨트롤에 대 한 저장된 된 상태를 포함 하는 개체 유형의 하나의 인수를 사용 합니다.

## <a name="full-xhtml-compliance"></a>전체 XHTML 규격

모든 웹 개발자는 웹 응용 프로그램에서 표준의 중요성을 알고 있습니다. 표준 기반 개발 환경을 유지 하기 위해 ASP.NET 2.0은 XHTML 호환 완벽 하 게 합니다. 따라서 모든 태그는 HTML 4.0을 지 원하는 브라우저에서 XHTML 표준에 따라 렌더링 이상.

ASP.NET 1.1에서 DOCTYPE 정의 다음과 같습니다.

[!code-html[Main](server-controls/samples/sample6.html)]

ASP.NET 2.0의 기본 문서 종류 정의 다음과 같습니다.

[!code-html[Main](server-controls/samples/sample7.html)]

원하는 경우 구성 파일에서 xhtmlConformance 노드를 통해 기본 XHML 규정 준수를 변경할 수 있습니다. 예를 들어 web.config 파일에서 다음 노드는 XHTML 1.0 Strict로 XHTML 규격을 변경 합니다.

[!code-xml[Main](server-controls/samples/sample8.xml)]

원하는 경우 구성할 수도 있습니다 레거시 ASP.NET에서 사용 된 구성을 사용 하는 ASP.NET 1.x 같이:

[!code-xml[Main](server-controls/samples/sample9.xml)]

## <a name="adaptive-rendering-using-adapters"></a>어댑터를 사용 하 여 렌더링 적응

Asp.net에서 1.x에서 포함 된 구성 파일을 &lt;browserCaps&gt; HttpBrowserCapabilities 개체를 입력 하는 섹션입니다. 이 개체는 어떤 장치는 특정 요청 하는 확인 코드를 적절 하 게 렌더링 하는 개발자를 허용 합니다. ASP.NET 2.0에서 향상 되었습니다 모델과 이제 새 ControlAdapter 클래스를 사용 합니다. 컨트롤의 수명 주기에서 이벤트를 재정의 하 고 사용자 에이전트의 기능에 따라 컨트롤의 렌더링을 제어 하는 ControlAdapter 클래스. 특정 사용자 에이전트의 기능을 c:\windows\microsoft.net\framework\v2.0에 저장 된 브라우저 정의 파일 (.browser 파일 확장명을 가진 파일)에서 정의 됩니다. \* \* \* \*\CONFIG\Browsers 폴더입니다.

> [!NOTE]
> ControlAdapter 클래스는 추상 클래스입니다.


마찬가지로 합니다 &lt;browserCaps&gt; 1.x의 경우 브라우저 정의 파일의 섹션에서는 요청 하는 브라우저를 식별 하기 위해 사용자 에이전트 문자열을 구문 분석할 정규식을 사용 합니다. 이 사용자 에이전트에 대 한 특정 기능을 정의 합니다. ControlAdapter 렌더링 메서드를 통해 컨트롤을 렌더링합니다. 따라서 Render 메서드를 재정의 하는 경우 호출 하지 않아야 렌더링 기본 클래스입니다. 이렇게 하면 어댑터에 한 번씩와 자체 컨트롤을 두 번 발생 하도록 렌더링 발생할 수 있습니다.

## <a name="developing-a-custom-adapter"></a>사용자 지정 어댑터 개발

ControlAdapter에서 상속 하 여 사용자 고유의 사용자 지정 어댑터를 개발할 수 있습니다. 또한 어댑터는 페이지에 대 한 필요한 경우 PageAdapter 추상 클래스에서 상속할 수 있습니다. 사용자 지정 어댑터에는 컨트롤의 매핑을 통해 수행 됩니다는 &lt;controlAdapters&gt; 브라우저 정의 파일의 요소입니다. 예를 들어 브라우저 정의 파일에서 다음 XML MenuAdapter 클래스 메뉴 컨트롤을 매핑합니다.

[!code-html[Main](server-controls/samples/sample10.html)]

특정 장치 또는 브라우저를 대상으로 하는 컨트롤 개발자가 쉽게 됩니다이 모델을 사용 합니다. 것도 개발자가 모든 장치에서 페이지가 렌더링 되는 방식을 완전히 제어할 수를 매우 간단 합니다.

## <a name="per-device-rendering"></a>장치별 렌더링

ASP.NET 2.0에서 서버 컨트롤 속성에 지정 된 장치당 브라우저별 접두사를 사용 하 여 수 있습니다. 예를 들어 아래 코드 페이지 찾아보기에 사용 되는 장치에 따라 레이블의 텍스트를 변경 됩니다.

[!code-aspx[Main](server-controls/samples/sample11.aspx)]

레이블에 "Internet Explorer에서 검색 된 있습니다." 라는 텍스트를 표시는 Internet Explorer에서이 레이블을 포함 하는 페이지를 찾아볼 때 Firefox에서 페이지를 찾아볼 때를 표시 될 텍스트를 "를 검색 하는 Firefox에서." 다른 장치에서 페이지를 찾아볼 표시 됩니다. "알 수 없는 장치에서 검색 된 있습니다." 이 특수 구문을 사용 하 여 모든 속성을 지정할 수 있습니다.

## <a name="setting-focus"></a>포커스를 설정합니다.

ASP.NET 1.x 개발자에 게 특정 컨트롤에서 초기 포커스를 설정 하는 방법에 대 한 질문과입니다. 예를 들어 로그인 페이지에 있는 페이지를 처음 로드 될 때 포커스를 가져올 사용자 ID 텍스트 상자에는 것이 유용 합니다. ASP.NET 1.x에서 이렇게 일부 클라이언트 쪽 스크립트를 작성 해야 합니다. 이러한 스크립트의 간단한 작업 인 경우에 SetFocus 메서드 덕분 ASP.NET 2.0의 필요는 없습니다. SetFocus 메서드 포커스를 수신 해야 하는 컨트롤을 나타내는 하나의 인수입니다. 문자열로 나타낸 컨트롤의 클라이언트 ID 또는 컨트롤 개체로 서버 컨트롤의 이름에는 두이 일 수 있습니다. 예를 들어 초기 포커스 페이지가 처음 로드 될 때 txtUserID를 호출 하는 TextBox 컨트롤을 설정 하려면 페이지에 다음 코드를 추가\_부하:

[!code-csharp[Main](server-controls/samples/sample12.cs)]

-또는

[!code-csharp[Main](server-controls/samples/sample13.cs)]

ASP.NET 2.0 포커스를 설정 하는 클라이언트 쪽 함수를 렌더링 하 여 Webresource.axd 처리기 (앞에서 설명한)를 사용 합니다. 클라이언트 쪽 함수의 이름은 WebForm\_AutoFocus 다음과 같이 합니다.

[!code-html[Main](server-controls/samples/sample14.html)]

또는 해당 컨트롤에 초기 포커스를 설정 하려면 컨트롤의 Focus 메서드를 사용할 수 있습니다. Focus 메서드 Control 클래스에서 파생 되며 모든 ASP.NET 2.0 컨트롤에 사용할 수 있습니다. 유효성 검사 오류가 발생 하면 특정 컨트롤에 포커스를 설정 하는 것도 가능 합니다. 이후 단원에서 설명 합니다.

## <a name="new-server-controls-in-aspnet-20"></a>ASP.NET 2.0의에서 새로운 서버 컨트롤

다음은 ASP.NET 2.0의 새로운 서버 컨트롤입니다. 뒷부분에 나오는 모듈에서 그 중 일부에 대해 자세히 이동지 것입니다.

## <a name="imagemap-control"></a>ImageMap 컨트롤

ImageMap 컨트롤을 사용 하면 핫스폿 다시 게시를 시작 하거나 URL을 탐색할 수 있는 이미지를 추가할 수 있습니다. 사용할 수는 핫스폿 CircleHotSpot RectangleHotSpot, 하며 PolygonHotSpot 합니다. 핫스폿 Visual Studio 또는 프로그래밍 방식으로 코드에서 컬렉션 편집기를 통해 추가 됩니다. 핫스폿 이미지의 그리기에 사용할 수 있는 사용자 인터페이스가 없는 있습니다. 좌표 및 크기나 핫스폿의 radius를 선언적으로 지정 되어야 합니다. 디자이너에서 핫스팟의 시각적 표시가 있습니다. 핫스팟을 URL로 이동 하도록 구성 하는 경우 URL의 핫스폿 NavigateUrl 속성을 통해 지정 됩니다. 게시물의 경우 속성을 사용 하면 서버 쪽 코드에서 게시물을 다시 검색할 수 있는 문자열을 전달할 수 있습니다 PostBackValue 핫스팟으로 전환한 후를 다시 초대 합니다.


![Visual Studio에서 hotSpot 컬렉션 편집기](server-controls/_static/image1.jpg)

**그림 1**: Visual Studio에서 HotSpot 컬렉션 편집기


## <a name="bulletedlist-control"></a>BulletedList 컨트롤

BulletedList 컨트롤에 바인딩된 데이터를 쉽게 수 있는 글머리 기호 목록입니다. 목록 (번호가 매겨진) 정렬할 수 또는 BulletStyle 속성을 통해 순서가 지정 되지 않은 합니다. 목록의 각 항목은 ListItem 개체로 표시 됩니다.


![Visual Studio에서 BulletedList 컨트롤](server-controls/_static/image1.gif)

**그림 2**: Visual Studio에서 BulletedList 컨트롤


## <a name="hiddenfield-control"></a>HiddenField 컨트롤

HiddenField 컨트롤의 값은 서버 쪽 코드에서 사용할 수 있는 페이지에 숨겨진된 양식 필드를 추가 합니다. 일반적으로 숨겨진된 폼 필드의 값은 포스트백 간에 변경 되지 않은 상태로 유지 해야 합니다. 그러나 악의적인 사용자가 다시 게시 하려면 이전 값을 변경 하는 것이 같습니다. 이 경우 HiddenField 컨트롤 ValueChanged 이벤트를 발생 합니다. HiddenField 컨트롤에서 중요 한 정보가 있고 변경 되지 않은 상태로 남아 있는지 확인 하려는 경우에 코드에서 ValueChanged 이벤트를 처리 해야 합니다.

## <a name="fileupload-control"></a>FileUpload 컨트롤

ASP.NET 2.0에서 FileUpload 컨트롤을 사용 하면 ASP.NET 페이지를 통해 웹 서버에 파일을 업로드할 수 있습니다. 이 컨트롤은 몇 가지 예외를 사용 하 여 ASP.NET 1.x HtmlInputFile 클래스와 매우 비슷합니다. Asp.net에서 1.x는 것이 좋았습니다 좋은 파일로 했다면 확인 하기 위해 null PostedFile 속성을 확인 수 있습니다. ASP.NET 2.0에서 FileUpload 컨트롤 같은 목적을 위해 사용할 수 있습니다 하는 것이 더 효율적인 새 HasFile 속성을 추가 합니다.

PostedFile 속성 HttpPostedFile 개체에 대 한 액세스에 여전히 사용할 수 있지만 HttpPostedFile 기능의 일부 FileUpload 컨트롤을 사용 하 여 기본적으로 제공 됩니다. 예를 들어, ASP.NET에서 업로드 된 파일을 저장 하려면 HttpPostedFile 개체의 SaveAs 메서드를 호출 1.x의 경우. FileUpload 컨트롤을 사용 하 여 ASP.NET 2.0에서, FileUpload 컨트롤 자체에 SaveAs 메서드를 호출할 것 있습니다.

2.0 동작 (및 가능성이 가장 중요 한 변경)의 또 다른 큰 변화가 점 업로드 된 전체 파일을 저장 하기 전에 메모리에 로드 하는 데 필요한 더 이상입니다. 1.x에서 업로드 된 파일 기록 되기 전에 메모리에 완전히 저장은 디스크에 있습니다. 이 아키텍처는 큰 파일 업로드를 방지합니다.

ASP.NET 2.0에서는 httpRuntime 요소의 저장할지 킬로바이트 수를 구성할 수 있습니다 기록 되기 전에 메모리에 버퍼에 보관 된 디스크에 있습니다.

**중요 한**:이 값 (킬로바이트) (바이트)에서 이며 기본값은 256는 MSDN 설명서 (및 설명서를 다른 곳에서)를 지정 합니다. (킬로바이트)에서 실제로 지정 된 값 및 기본값은 80입니다. 기본값은 80 K 함으로써 대형 개체 힙에 버퍼 종료 하지 않습니다 확인 합니다.

## <a name="wizard-control"></a>마법사 컨트롤

매우 일반적인 ASP.NET 개발자에 게 집중할 패널을 사용 하 여 "페이지" 또는 페이지를 전송 하 여 계열에서 정보를 수집 하는 동안 발생할 것입니다. 더 경우가 노력은 불편 한 및 시간이 오래 걸립니다. 선형 및 비선형 단계 사용자에 잘 알고 있는 마법사 인터페이스에 대 한 허용 하 여 문제를 해결 하는 새 마법사 컨트롤입니다. 마법사 컨트롤 일련의 단계에서 입력된 된 폼을 표시합니다. 각 단계는 특정 컨트롤의 StepType 속성에 지정 된 형식입니다. 사용할 수 있는 단계 유형 아래와 같습니다.

| **단계 유형** | **설명** |
| --- | --- |
| 자동 | 마법사는 자동으로 단계 계층 구조 내에서 해당 위치에 따라 단계의 유형을 결정 합니다. |
| 시작 | 첫 번째 단계를 소개는 문을 나타내는 데 주로 사용 합니다. |
| 단계 | 일반적인 단계입니다. |
| 마침 | 마법사를 완료 하려면 단추를 나타내는 데 일반적으로 최종 단계입니다. |
| 완료 | 성공 또는 실패를 통신 하는 메시지를 표시 합니다. |

> [!NOTE]
> 마법사 컨트롤은 ASP.NET 컨트롤 상태를 사용 하 여 해당 상태입니다. 따라서 EnableViewState 속성은 모든 손해를 주지 않고 false로 설정할 수 있습니다.


이 비디오는 Wizard 컨트롤의 연습입니다.


![](server-controls/_static/image2.png)


[전체 화면 비디오 열기](server-controls/_static/wizard1.wmv)


## <a name="localize-control"></a>컨트롤 지역화

Localize 컨트롤 리터럴 컨트롤을 하는 것과 비슷합니다. 그러나 Localize 컨트롤에는 **모드** 태그에 추가 되는 렌더링 되는 방식을 제어 하는 속성입니다. Mode 속성 값을 지원 합니다.

| **모드** | **설명** |
| --- | --- |
| 변형 | 태그를 요청 하는 브라우저의 프로토콜에 따라 변환 됩니다. |
| 통과 | 로 태그를 렌더링할-됩니다. |
| 인코딩 | HtmlEncode를 사용 하 여 컨트롤에 추가 되는 태그는 인코딩됩니다. |

## <a name="multiview-and-view-controls"></a>MultiView 및 View 컨트롤

MultiView 컨트롤 뷰 컨트롤에 대 한 컨테이너로 작동 하 고 뷰 컨트롤에서 컨테이너로 (훨씬 패널 컨트롤)와 같은 다른 컨트롤에 대 한 키를 누릅니다. 각 보기는 MultiView 컨트롤에는 단일 뷰 컨트롤에서 표시 됩니다. 첫 번째 보기는 MultiView 컨트롤 보기 0 이면 두 번째 뷰입니다 1, 등입니다. MultiView 컨트롤의 ActiveViewIndex를 지정 하 여 뷰를 전환할 수 있습니다.

## <a name="substitution-control"></a>대체 제어

대체 컨트롤은 ASP.NET 캐싱와 함께에서 사용 됩니다. 캐싱을 활용 하려는 하지만 (즉, 부분 페이지 캐싱에서 제외 되는) 각 요청에 업데이트 해야 하는 페이지의 부분에 있는 경우, 대체 구성 요소는 최고의 솔루션을 제공 합니다. 컨트롤 자체에서 모든 출력을 실제로 렌더링할 하지 않습니다. 대신, 서버 쪽 코드의 메서드에 바인딩됩니다. 페이지가 요청 될 때 메서드가 호출 되 고 반환 된 태그 대신 대체 컨트롤 렌더링 됩니다.

대체 컨트롤이 바인딩되는 메서드를 통해 지정 된 **MethodName** 속성입니다. 해당 메서드는 다음 조건을 충족 해야 합니다.

- 정적 (VB의 경우 공유) 메서드에 이어야 합니다.
- HttpContext 형식의 매개 변수 하나를 허용합니다.
- 페이지의 컨트롤을 대체 해야 하는 태그를 나타내는 문자열을 반환 합니다.

대체 컨트롤 페이지의 다른 컨트롤을 수정할 수 없지만 해당 매개 변수를 통해 현재 HttpContext에 액세스 하지 않는 것입니다.

## <a name="gridview-control"></a>GridView 컨트롤

GridView 컨트롤은 DataGrid 컨트롤을 대체 합니다. 이 컨트롤은 이후 단원에서 자세히 설명 합니다.

## <a name="detailsview-control"></a>DetailsView 컨트롤

DetailsView 컨트롤을 사용 하면 데이터 원본에서 단일 레코드를 표시 하 고 편집 또는 삭제 수 있습니다. 이후 단원에서 자세히 다룹니다.

## <a name="formview-control"></a>FormView 컨트롤

데이터 원본에서 단일 레코드를 구성할 수 있는 인터페이스에 표시할 FormView 컨트롤이 사용 됩니다. 이후 단원에서 자세히 다룹니다.

## <a name="accessdatasource-control"></a>AccessDataSource 컨트롤

AccessDataSource 컨트롤에 사용 되는 데이터는 Access 데이터베이스를 바인딩합니다. 이후 단원에서 자세히 다룹니다.

## <a name="objectdatasource-control"></a>ObjectDataSource 컨트롤

ObjectDataSource 컨트롤은 컨트롤 수 데이터 바인딩할 수는 2 계층 모델 대신 중간 계층 비즈니스 개체에 데이터 원본에 직접 바인딩된 컨트롤 위치는 3 계층 아키텍처를 지원 하기 위해 사용 됩니다. 이후 단원에서 자세히 설명 합니다.

## <a name="xmldatasource-control"></a>XmlDataSource 컨트롤

XML 데이터 원본에 데이터 바인딩할 XmlDataSource 컨트롤이 사용 됩니다. 이후 단원에서 자세히 다룹니다.

## <a name="sitemapdatasource-control"></a>SiteMapDataSource 컨트롤

SiteMapDataSource 컨트롤 사이트 맵을 기반으로 하는 사이트 탐색 컨트롤에 대 한 데이터 바인딩을 제공 합니다. 이후 단원에서 자세히 설명 합니다.

## <a name="sitemappath-control"></a>SiteMapPath 컨트롤

SiteMapPath 컨트롤에는 일련의 이동 경로 라고 하는 탐색 링크를 표시 합니다. 이후 단원에서 자세히 다룹니다.

## <a name="menu-control"></a>Menu 컨트롤

메뉴 컨트롤 DHTML을 사용 하 여 동적 메뉴를 표시 합니다. 이후 단원에서 자세히 다룹니다.

## <a name="treeview-control"></a>TreeView 컨트롤

TreeView 컨트롤을 데이터의 계층적 트리 뷰가 표시 됩니다. 이후 단원에서 자세히 다룹니다.

## <a name="login-control"></a>로그인 컨트롤

웹 사이트에 로그인 하는 메커니즘에 대 한 로그인 제어를 제공 합니다. 이후 단원에서 자세히 다룹니다.

## <a name="loginview-control"></a>LoginView 컨트롤

통해 LoginView 컨트롤은 사용자의 로그인 상태에 따라 다양 한 템플릿 표시를 허용 합니다. 이후 단원에서 자세히 다룹니다.

## <a name="passwordrecovery-control"></a>PasswordRecovery 컨트롤

PasswordRecovery 컨트롤은 ASP.NET 응용 프로그램의 사용자가 잊어버린된 암호 검색에 사용 됩니다. 이후 단원에서 자세히 다룹니다.

## <a name="loginstatus"></a>LoginStatus

LoginStatus 컨트롤을 사용자의 로그인 상태를 표시합니다. 이후 단원에서 자세히 다룹니다.

## <a name="loginname"></a>LoginName

LoginName 컨트롤과 ASP.NET 응용 프로그램에 기록 된 후 사용자의 사용자 이름을 표시 합니다. 이후 단원에서 자세히 다룹니다.

## <a name="createuserwizard"></a>CreateUserWizard

CreateUserWizard는 사용자에 게 ASP.NET 응용 프로그램에서 사용 하 여 ASP.NET 멤버 자격 계정을 만드는 기능을 제공 하는 마법사가 구성할 수 있습니다. 이후 단원에서 자세히 다룹니다.

## <a name="changepassword"></a>ChangePassword

ChangePassword 컨트롤을 사용 하면 ASP.NET 응용 프로그램에 대 한 암호를 변경할 수 있습니다. 이후 단원에서 자세히 다룹니다.

## <a name="various-webparts"></a>다양 한 웹 파트

ASP.NET 2.0은 다양 한 웹 파트 포함 되어 있습니다. 이후 단원에서 자세히 설명 합니다.
