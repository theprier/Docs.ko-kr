---
uid: web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-cs
title: 도구 키트 컨트롤 Extender (C#)를 제어 하는 사용자 지정 AJAX 만들기 | Microsoft Docs
author: microsoft
description: 사용자 지정 Extender를 사용 하 여 사용자 지정 하 고 새 클래스를 만들 필요 없이 ASP.NET 컨트롤의 기능을 확장할 수 있습니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/12/2009
ms.topic: article
ms.assetid: 96b56eca-a892-45a4-96b4-67e61178650a
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-cs
msc.type: authoredcontent
ms.openlocfilehash: 0dd243ec1709324174ff48b52e7dfb5185d3aaa2
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37390955"
---
<a name="creating-a-custom-ajax-control-toolkit-control-extender-c"></a>사용자 지정 AJAX 컨트롤 도구 키트 컨트롤 Extender (C#) 만들기
====================
[Microsoft](https://github.com/microsoft)

> 사용자 지정 Extender를 사용 하 여 사용자 지정 하 고 새 클래스를 만들 필요 없이 ASP.NET 컨트롤의 기능을 확장할 수 있습니다.


이 자습서에서는 사용자 지정 AJAX 컨트롤 도구 키트 컨트롤 extender를 만드는 방법을 알아봅니다. 텍스트 상자에 텍스트를 입력할 때 사용 안 함 상태에서 단추의 상태를 변경 하는 extender 유용 하 고 새 하지만 단순 하 고 만듭니다. 이 자습서를 읽은 후 사용자 고유의 컨트롤 extender 사용 하 여 ASP.NET AJAX Toolkit를 확장할 수 있습니다.

Visual Studio 또는 Visual Web Developer를 사용 하 여 사용자 지정 컨트롤 extender를 만들 수 있습니다 (Visual Web Developer의 최신 버전이 있는지 확인).

## <a name="overview-of-the-disabledbutton-extender"></a>DisabledButton Extender의 개요

이 새 컨트롤 extender DisabledButton extender를 이라고 합니다. 이 extender에는 세 가지 속성이 포함 됩니다.

- TargetControlID-컨트롤을 확장 하는 텍스트입니다.
- TargetButtonIID-단추를 비활성화 하거나 활성화입니다.
- DisabledText-단추를 처음 표시 되는 텍스트입니다. 입력을 시작 하는 경우 단추 텍스트 속성의 값을 표시 합니다.

TextBox와 Button 컨트롤에 DisabledButton extender에 연결 합니다. 모든 텍스트를 입력 하기 전에 단추가 비활성화 되 고 TextBox와 Button 다음과 같이 표시 합니다.


[![](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image2.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image1.png)

([클릭 하 여 큰 이미지 보기](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image3.png))


텍스트 입력을 시작 하면이 단추가 활성화 됩니다 후 TextBox와 Button 다음과 같이 표시 됩니다.


[![](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image5.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image4.png)

([클릭 하 여 큰 이미지 보기](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image6.png))


이 컨트롤 extender를 만들려면 다음 세 가지 파일을 만드는 데 필요 합니다.

- DisabledButtonExtender.cs-이 파일은 프로그램 extender 만들기 관리 되며 디자인 타임에 속성을 설정할 수 있도록 하는 서버 쪽 컨트롤 클래스. 또한 extender의 설정할 수 있는 속성을 정의 합니다. 이러한 속성은 코드를 통해 및 디자인 타임에 액세스할 수 및 DisableButtonBehavior.js 파일에 정의 된 속성과 일치 합니다.
- DisabledButtonBehavior.js-이 파일은 모든 클라이언트 스크립트 논리에 추가할 위치입니다.
- DisabledButtonDesigner.cs-이 클래스를 사용 하면 디자인 타임 기능입니다. Visual Studio/Visual Web Developer 디자이너를 사용 하 여 제대로 작동 하려면 컨트롤 extender를 하려는 경우이 클래스가 필요 합니다.

따라서 컨트롤 extender를 서버 쪽 컨트롤, 동작을 클라이언트 쪽 및 서버 쪽 디자이너 클래스 이루어져 있습니다. 다음 섹션에서 이러한 파일의 세 가지 모두를 만드는 방법에 알아봅니다.

## <a name="creating-the-custom-extender-website-and-project"></a>사용자 지정 Extender 웹 사이트 및 프로젝트 만들기

먼저 Visual Studio/Visual Web Developer에서 클래스 라이브러리 프로젝트 및 웹 사이트를 만드는 것입니다. 에서는 ll 클래스 라이브러리 프로젝트에서 사용자 지정 extender를 만들고 웹 사이트에서 사용자 지정 extender를 테스트 합니다.

S를 웹 사이트를 시작할 수 있습니다. 웹 사이트를 만들려면 다음이 단계를 수행 합니다.

1. 메뉴 옵션을 선택 **파일, 새 웹 사이트**합니다.
2. 선택 된 **ASP.NET 웹 사이트** 템플릿.
3. 새 웹 사이트 이름을 *Website1*합니다.
4. 클릭 합니다 **확인** 단추입니다.

다음으로, 컨트롤 extender에 대 한 코드를 포함 하는 클래스 라이브러리 프로젝트를 만들려면 해야 합니다.

1. 메뉴 옵션을 선택 **파일을 추가, 새 프로젝트**합니다.
2. 선택 된 **클래스 라이브러리** 템플릿.
3. 이름의 새 클래스 라이브러리의 이름을 **CustomExtenders**합니다.
4. 클릭 합니다 **확인** 단추입니다.

다음이 단계를 완료 한 후 솔루션 탐색기 창 그림 1과 같아야 합니다.


[![웹 사이트 및 클래스 라이브러리 프로젝트를 사용 하 여 솔루션](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image8.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image7.png)

**그림 01**: 웹 사이트 및 클래스 라이브러리 프로젝트를 사용 하 여 솔루션 ([큰 이미지를 보려면 클릭](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image9.png))


다음으로, 모든 클래스 라이브러리 프로젝트에 필요한 어셈블리 참조를 추가 해야 합니다.

1. CustomExtenders 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **참조 추가**합니다.
2. .NET 탭을 선택 합니다.
3. 다음 어셈블리에 대한 참조를 추가합니다.

    1. System.Web.dll
    2. System.Web.Extensions.dll
    3. System.Design.dll
    4. System.Web.Extensions.Design.dll
4. 찾아보기 탭을 선택 합니다.
5. AjaxControlToolkit.dll 어셈블리에 대 한 참조를 추가 합니다. 이 어셈블리는 AJAX Control Toolkit을 다운로드 한 폴더에 있습니다.

다음이 단계를 완료 한 후 클래스 라이브러리 프로젝트 참조 폴더는 그림 2와 같습니다.


[![필요한 참조를 사용 하 여 참조 폴더](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image11.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image10.png)

**그림 02**: 필요한 참조를 사용 하 여 참조 폴더 ([큰 이미지를 보려면 클릭](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image12.png))


## <a name="creating-the-custom-control-extender"></a>사용자 지정 컨트롤 Extender 만들기

클래스 라이브러리 만들었으므로 extender 컨트롤 작성을 시작할 수 있습니다. 사용자 지정 extender 컨트롤 클래스 (참조 목록 1)의 bare 뼈 시작 s 수 있습니다.

**1-MyCustomExtender.cs 나열**

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample1.cs)]

목록 1에서 extender 컨트롤 클래스에 대 한 확인 하는 몇 가지 있습니다. 먼저 기본 ExtenderControlBase 클래스에서 클래스를 상속 함을 알 수 있습니다. 모든 AJAX Control Toolkit extender 컨트롤은이 기본 클래스에서 파생 됩니다. 예를 들어, 기본 클래스 TargetID 속성 모든 컨트롤 extender의 필수 속성을 포함 합니다.

다음으로, 클라이언트 스크립트와 관련 된 다음 두 특성 클래스에 알 수 있습니다.

- WebResource-파일을 어셈블리에 포함 리소스로 포함 하면 됩니다.
- ClientScriptResource-어셈블리에서 검색 해야 하는 스크립트 리소스를 하면 됩니다.

웹 리소스의 특성을 사용자 지정 extender 컴파일될 때 MyControlBehavior.js JavaScript 파일을 어셈블리에 포함 됩니다. 웹 페이지에서 사용자 지정 extender를 사용 하면 어셈블리에서 MyControlBehavior.js 스크립트를 검색 하려면 ClientScriptResource 특성이 사용 됩니다.


작동 하려면 WebResource 및 ClientScriptResource 특성에 대 한 순서 대로 포함 리소스로 JavaScript 파일을 컴파일해야 합니다. 솔루션 탐색기 창에서 파일을 선택 하 고, 속성 시트를 열고, 값을 할당 *포함 리소스* 에 **빌드 작업** 속성입니다.


컨트롤 extender에도 TargetControlType 특성을 포함 하는 알 수 있습니다. 이 특성은 컨트롤 extender에 의해 확장 된 컨트롤의 형식을 지정 하는 데 사용 됩니다. 목록 1의 경우 컨트롤 extender는 텍스트 상자를 확장 하는 데 사용 됩니다.

마지막으로, 사용자 지정 extender MyProperty 라는 속성에 알 수 있습니다. 속성은 ExtenderControlProperty 특성으로 표시 됩니다. GetPropertyValue() 메서드와 SetPropertyValue() 클라이언트 쪽 동작을 서버 쪽 컨트롤 extender 속성 값을 전달 하기 위해 사용 됩니다.

가 계속 해 서 우리의 DisabledButton extender에 대 한 코드를 구현할 수 있습니다. 이 extender에 대 한 코드 목록 2에서 찾을 수 있습니다.

**2-DisabledButtonExtender.cs 나열**

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample2.cs)]

목록 2에서 DisabledButton extender TargetButtonID 및 DisabledText 라는 두 속성이 있습니다. TargetButtonID 속성에 적용할 IDReferenceProperty이이 속성에 할당 하는 단추 컨트롤의 ID 이외의 수 없습니다.

WebResource 및 ClientScriptResource 특성은이 extender를 사용 하 여 DisabledButtonBehavior.js 라는 파일에 있는 클라이언트 쪽 동작을 연결 합니다. 이 JavaScript 파일의 다음 섹션에서 설명합니다.

## <a name="creating-the-custom-extender-behavior"></a>사용자 지정 Extender 동작 만들기

컨트롤 extender의 클라이언트 쪽 구성 요소를 동작을 이라고 합니다. 사용 하지 않도록 설정 하 고 단추를 사용 하도록 설정 하는 실제 논리 DisabledButton 동작이 포함 되어 있습니다. 동작에 대 한 JavaScript 코드는 목록 3에 포함 됩니다.

**3-DisabledButton.js 나열**

[!code-javascript[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample3.js)]

보기 3의 JavaScript 파일 DisabledButtonBehavior 클라이언트 쪽 클래스를 포함 합니다. TargetButtonID 라는 두 속성을 포함 하는이 클래스는 서버 쪽 쌍 가져오고 사용 하 여 액세스할 수 있는 DisabledText\_TargetButtonID/set\_TargetButtonID 받고\_DisabledText/set\_ DisabledText 합니다.

Initialize () 메서드는 동작에 대 한 대상 요소를 사용 하 여 keyup 이벤트 처리기를 연결합니다. 이 동작과 연결 된 텍스트 상자에 문자를 입력할 때마다 keyup 처리기를 실행 합니다. Keyup 처리기를 사용 하도록 설정 또는 동작과 연결 된 텍스트 상자에서 모든 텍스트를 포함 하는 여부에 따라 단추를 사용 하지 않도록 설정 합니다.

JavaScript 파일 목록 3에 포함 리소스로 컴파일해야 해야 합니다. 솔루션 탐색기 창에서 파일을 선택 하 고, 속성 시트를 열고, 값을 할당 *포함 리소스* 에 **빌드 작업** 속성 (그림 3 참조). 이 옵션은 Visual Studio 및 Visual Web Developer에서 사용할 수 있습니다.


[![JavaScript 파일을 포함 리소스로 추가](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image14.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image13.png)

**그림 03**: 포함된 리소스와 JavaScript 파일을 추가 ([큰 이미지를 보려면 클릭](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image15.png))


## <a name="creating-the-custom-extender-designer"></a>사용자 지정 Extender 디자이너 만들기

이 extender를 완료 하려면 만들어야 하는 하나의 마지막 클래스가 있습니다. 목록 4에서 디자이너 클래스를 생성 해야 합니다. 이 클래스는 Visual Studio/Visual Web Developer 디자이너를 사용 하 여 올바르게 작동 하는 extender를 확인 해야 합니다.

**4-DisabledButtonDesigner.cs 나열**

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample4.cs)]

Designer 특성을 사용 하 여 DisabledButton extender 4에서 디자이너를 연결합니다. 이와 같은 DisabledButtonExtender 클래스에 Designer 특성을 적용 해야 합니다.

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample5.cs)]

## <a name="using-the-custom-extender"></a>사용자 지정 Extender를 사용 하 여

이제 DisabledButton 컨트롤 extender 만들기를 마친 것, ASP.NET 웹 사이트에서 사용 하는 시간입니다. 먼저, 도구 상자에 사용자 지정 extender를 추가 해야 합니다. 아래 단계를 수행합니다.

1. 솔루션 탐색기 창에서 페이지를 두 번 클릭 하 여 ASP.NET 페이지를 엽니다.
2. 도구 상자를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **선택 항목**합니다.
3. 도구 상자 항목 선택 대화 상자에서 CustomExtenders.dll 어셈블리를 찾습니다.
4. 클릭 합니다 **확인** 단추를 대화 상자를 닫습니다.

다음이 단계를 완료 하면 DisabledButton 컨트롤 extender 도구 상자에 나타납니다 (그림 4 참조).


[![도구 상자에서 DisabledButton](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image17.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image16.png)

**그림 04**: 도구 상자에서 DisabledButton ([큰 이미지를 보려면 클릭](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image18.png))


그런 다음 새 ASP.NET 페이지를 만들 해야 합니다. 아래 단계를 수행합니다.

1. ShowDisabledButton.aspx 라는 새로운 ASP.NET 페이지를 만듭니다.
2. ScriptManager를 페이지로 끌어옵니다.
3. TextBox 컨트롤을 페이지로 끌어옵니다.
4. 단추 컨트롤을 페이지로 끌어옵니다.
5. 속성 창에서 단추 ID 속성 값을 변경 <em>btnSave</em> 및 텍스트 속성을 값 *저장할\** 합니다.
  

표준 ASP.NET TextBox와 Button 컨트롤을 사용 하 여 페이지를 만들었습니다.

다음으로, DisabledButton extender 사용 하 여 텍스트 상자 컨트롤을 확장 해야 합니다.

1. 선택 된 **Extender 추가** 작업 옵션 Extender 마법사 대화 상자를 엽니다 (그림 5 참조). 대화 상자에 사용자 지정 DisabledButton extender는 포함 되어 있는지 확인 합니다.
2. DisabledButton extender를 선택 하 고 클릭 합니다 **확인** 단추입니다.


[![Extender 마법사 대화 상자](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image20.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image19.png)

**그림 05**: Extender 마법사 대화 상자 ([큰 이미지를 보려면 클릭](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image21.png))


마지막으로, DisabledButton extender의 속성을 설정할 수 있습니다. TextBox 컨트롤의 속성을 수정 하 여 DisabledButton extender의 속성을 수정할 수 있습니다.

1. 디자이너에서 텍스트 상자를 선택 합니다.
2. 속성 창에서 Extender 노드를 확장 (그림 6 참조).
3. 값을 할당 *저장할* DisabledText 속성 및 값에 *btnSave* TargetButtonID 속성입니다.


[![Extender 속성 설정](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image23.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image22.png)

**그림 06**: extender 속성을 설정 ([큰 이미지를 보려면 클릭](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image24.png))


페이지 (F5를 눌러)를 실행 하면 단추 컨트롤은 처음에 사용할 수 없습니다. 입력란에 텍스트 입력을 시작 하는 즉시 컨트롤은 단추 (그림 7 참조)를 사용 합니다.


[![실행 중인 DisabledButton extender](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image26.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image25.png)

**그림 07**: 작업의 The DisabledButton extender ([큰 이미지를 보려면 클릭](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image27.png))


## <a name="summary"></a>요약

이 자습서의 목표는 AJAX Control Toolkit 사용자 지정 extender 컨트롤을 사용 하 여 확장 하는 방법을 설명 하는 것 이었습니다. 이 자습서에서는 간단한 DisabledButton 컨트롤 extender를 만들었습니다. DisabledButtonExtender 클래스, DisabledButtonBehavior JavaScript 동작 및 DisabledButtonDesigner 클래스를 만들어이 extender를 구현 했습니다. 사용자 지정 컨트롤 extender를 만들 때마다 비슷한 일련의 단계를 따릅니다.

> [!div class="step-by-step"]
> [이전](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)
> [다음](get-started-with-the-ajax-control-toolkit-vb.md)
