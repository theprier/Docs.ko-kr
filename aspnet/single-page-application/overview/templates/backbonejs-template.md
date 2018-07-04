---
uid: single-page-application/overview/templates/backbonejs-template
title: 백본 템플릿 | Microsoft Docs
author: madskristensen
description: Backbone.js SPA 템플릿
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/04/2013
ms.topic: article
ms.assetid: 00aca413-f067-4108-9bd1-cf21e64a2646
ms.technology: ''
msc.legacyurl: /single-page-application/overview/templates/backbonejs-template
msc.type: authoredcontent
ms.openlocfilehash: 641e149155fbee2655024bec3b76dce5243e7d59
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37362507"
---
<a name="backbone-template"></a>백본 템플릿
====================
[제작: Mads Kristensen](https://github.com/madskristensen)

> Kazi Manzur Rashid 여 백본 SPA 템플릿 작성
> 
> [Backbone.js SPA 템플릿 다운로드](https://go.microsoft.com/fwlink/?LinkId=293631)


Backbone.js SPA 템플릿을 신속 하 게 사용 하 여 대화형 클라이언트 쪽 웹 앱을 빌드하기 시작할 수 있도록 디자인 [Backbone.js 합니다.](http://backbonejs.org/)

템플릿은은 ASP.NET MVC에서 Backbone.js 응용 프로그램을 개발 하기 위한는 초기 스 켈 레 톤을 제공 합니다. 기본적으로 사용자 등록, 로그인, 암호 재설정 및 기본 전자 메일 템플릿 사용 하 여 사용자에 게 확인을 비롯 한 기본 사용자 로그인 기능을 제공 합니다.

요구 사항:

- [ASP.NET 및 웹 도구 2012.2 업데이트](https://go.microsoft.com/fwlink/?LinkId=282650)

## <a name="create-a-backbone-template-project"></a>백본 템플릿 프로젝트 만들기

다운로드 하 고 위의 다운로드 단추를 클릭 하 여 템플릿을 설치 합니다. 서식 파일은 Visual Studio 확장 (VSIX) 파일로 패키지 됩니다. Visual Studio를 다시 시작 해야 합니다.

에 **템플릿** 창 **설치 된 템플릿** 확장 하 고는 **Visual C#** 노드. 아래 **Visual C#** 를 선택 **웹**합니다. 프로젝트 템플릿 목록에서 선택 **ASP.NET MVC 4 웹 응용 프로그램**합니다. 프로젝트 이름을 지정 하 고 클릭 **확인**합니다.

![](backbonejs-template/_static/image1.png)

에 **새 프로젝트** Backbone.js SPA 프로젝트 마법사를 선택 합니다.

![](backbonejs-template/_static/image2.png)

Ctrl-F5 키를 눌러 빌드하고 디버깅 하지 않고 응용 프로그램을 실행 또는 디버깅 실행 하려면 F5 키를 누릅니다.

![](backbonejs-template/_static/image3.png)

"내 계정"을 클릭 하면 로그인 페이지 표시:

![](backbonejs-template/_static/image4.png)

## <a name="walkthrough-client-code"></a>연습: 클라이언트 코드

클라이언트 쪽을 사용 하 여 시작 해 보겠습니다. 클라이언트 응용 프로그램 스크립트 ~/Scripts/application 폴더에 있습니다. 응용 프로그램 쓰여질 [TypeScript](http://www.typescriptlang.org/) (.ts 파일)는 JavaScript (.js 파일)로 컴파일됩니다.

**응용 프로그램**

`Application` application.ts에서 정의 됩니다. 이 개체는 응용 프로그램을 초기화 하 고 루트 네임 스페이스 역할. 사용자 로그인 여부와 같은 응용 프로그램 간에 공유 되는 구성 및 상태 정보를 유지 관리 합니다.

`application.start` 메서드 모달 뷰를 만들고 사용자 로그인 등의 응용 프로그램 수준 이벤트에 대 한 이벤트 처리기를 연결 합니다. 다음으로, 기본 라우터 만들고 모든 클라이언트 쪽 URL 지정 되었는지 여부를 확인 합니다. 기본 url로 리디렉션합니다. 그렇지 않은 경우 (#! /).

**이벤트**

이벤트는 느슨하게 개발 구성 요소를 결합 하는 경우에 항상 중요 합니다. 응용 프로그램 사용자 작업에 대 한 응답에서 여러 작업을 수행 하는 경우가 많습니다. 백본 모델, 컬렉션 및 보기와 같은 구성 요소를 사용 하 여 기본 제공 이벤트를 제공합니다. 이러한 구성 요소 간의 상호 종속성을 만드는 대신 템플릿을 사용 하 여 "pub/sub" 모델:는 `events` events.ts에 정의 된 개체를 게시 하 고 응용 프로그램 이벤트를 구독에 대 한 이벤트 허브로 서 작동 합니다. `events` 개체가 singleton입니다. 다음 코드는 이벤트를 구독할 이벤트를 트리거해야 하는 방법을 보여 줍니다.

[!code-csharp[Main](backbonejs-template/samples/sample1.cs)]

**라우터**

Backbone.js, 라우터는 클라이언트 쪽 페이지 라우팅 및 작업 및 이벤트에 연결 하는 메서드를 제공 합니다. 템플릿을 router.ts 단일 라우터를 정의합니다. 라우터 activable 뷰를 만들고이 보기를 전환할 때 상태를 유지 합니다. (Activable 뷰 다음 섹션에 설명 되어 있습니다.) 처음에 프로젝트에는 두 개의 더미 뷰가 홈 및에 대 한 합니다. 또한 경로 알 수 없는 경우 표시 되는 NotFound 뷰일이 있습니다.

**Views**

뷰는 ~/Scripts/application/보기에서 정의 됩니다. 보기, activable 뷰 및 모달 대화 보기는 방법은 두 가지가 있습니다. Activable 뷰 router에 의해 호출 됩니다. Activable 보기를 표시 되 면 다른 모든 activable 보기 비활성 상태가 됩니다. Activable 뷰를 만들려면 뷰를 확장 합니다 `Activable` 개체:

[!code-javascript[Main](backbonejs-template/samples/sample2.js)]

사용 하 여 확장 `Activable` 뷰를 두 개의 새 메서드를 추가 `activate` 및 `deactivate`합니다. 라우터를 활성화 하 고 뷰를 비활성화할 이러한 메서드를 호출 합니다.

모달 뷰로 구현 됩니다 [Twitter Bootstrap](http://twitter.github.com/bootstrap/) 모달 대화 상자. 합니다 `Membership` 고 `Profile` 뷰는 모달 뷰. 모델 뷰는 모든 응용 프로그램 이벤트에서 호출할 수 있습니다. 예를 들어, 합니다 `Navigation` "내 계정" 링크를 클릭 하면 보기 중 하나를 보여 줍니다는 `Membership` 보기 또는 `Profile` 사용자 로그인 여부에 따라 보기. 합니다 `Navigation` 연결 클릭 이벤트 처리기에 있는 모든 자식 요소는 `data-command` 특성입니다. HTML 태그는 다음과 같습니다.

[!code-html[Main](backbonejs-template/samples/sample3.html)]

이벤트 후크 navigation.ts의 코드는 다음과 같습니다.

[!code-csharp[Main](backbonejs-template/samples/sample4.cs)]

**모델**

모델은 ~/Scripts/application/모델에 정의 됩니다. 모든 모델은 세 개의 기본 항목이 있어야 합니다: 기본 특성, 유효성 검사 규칙 및 서버 쪽 끝점을 합니다. 일반적인 예는 다음과 같습니다.

[!code-javascript[Main](backbonejs-template/samples/sample5.js)]

**플러그 인**

~/Scripts/application/lib 폴더는 몇 가지 유용한 jQuery 플러그 인을 포함합니다. Form.ts 파일 형식 데이터로 작업 하기 위한 플러그 인을 정의 합니다. 종종 또는 serialize 하 고, 양식 데이터를 deserialize 하 고, 모델 유효성 검사 오류를 표시 해야 할 수도 있습니다. 플러그 인 form.ts와 같은 메서드를가지고 `serializeFields`하십시오 `deserializeFields`, 및 `showFieldErrors`합니다. 다음 예제에서는 모델에 폼을 serialize 하는 방법을 보여 줍니다.

[!code-javascript[Main](backbonejs-template/samples/sample6.js)]

플러그 인 flashbar.ts 사용자에 게 다양 한 피드백 메시지를 제공합니다. 메서드는 `$.showSuccessbar`하십시오 `$.showErrorbar` 및 `$.showInfobar`합니다. 내부적으로 사용 하 여 Twitter Bootstrap 경고 보기 좋게 애니메이션이 적용 된 메시지를 보여 줍니다.

플러그 인 confirm.ts 브라우저의 대체 API는 약간 다른 대화 상자에서 확인 합니다.

[!code-javascript[Main](backbonejs-template/samples/sample7.js)]

## <a name="walkthrough-server-code"></a>연습: 서버 코드

이제 서버 쪽에 살펴보겠습니다.

**Controllers**

단일 페이지 응용 프로그램에서는 서버 사용자 인터페이스에서 작은 역할만 재생합니다. 일반적으로 서버 초기 페이지를 렌더링 한 다음 보내고 JSON 데이터를 수신 합니다.

서식 파일에 2 명의 MVC 컨트롤러가: `HomeController` 초기 페이지를 렌더링 하 고 `SupportsController` 새 사용자 계정을 확인 및 암호 다시 설정 하는 데 사용 됩니다. 템플릿에서 다른 모든 컨트롤러는 JSON 데이터를 송수신 하는 ASP.NET Web API 컨트롤러입니다. 기본적으로 컨트롤러를 사용 하 여 새 `WebSecurity` 사용자 관련 작업을 수행 하는 클래스입니다. 그러나 이러한 작업에 대 한 대리자에 전달할 수 있는 선택적 생성자 또한 있습니다. 더 쉽게 테스트 하 고 대체할 수 있도록 허용이 `WebSecurity` IoC 컨테이너를 사용 하 여 다른 작업을 수행 합니다. 예를 들면 다음과 같습니다.

[!code-csharp[Main](backbonejs-template/samples/sample8.cs)]

## <a name="views"></a>보기

뷰는 모듈식 되도록 설계 되었습니다: 페이지의 각 섹션에는 고유한 전용된 보기입니다. 이 단일 페이지 응용 프로그램에서 모든 해당 컨트롤러 없는 뷰를 포함 하도록 일반적입니다. 호출 하 여 뷰를 포함할 수 있습니다 `@Html.Partial('myView')`,이 작업을 가져옵니다. 쉽게이 템플릿에 도우미 메서드를 정의 `IncludeClientViews`를 렌더링 하는 모든 지정된 된 폴더에 보기:

[!code-cshtml[Main](backbonejs-template/samples/sample9.cshtml)]

폴더 이름을 지정 하지 않으면 경우 기본 폴더 이름은 "ClientViews"입니다. 클라이언트 보기 부분 뷰를 사용 하는 경우 밑줄 문자를 사용 하 여 부분 뷰 이름 (예를 들어 `_SignUp`). `IncludeClientViews` 메서드 이름이 밑줄로 시작 하는 모든 보기를 제외 합니다. 부분 뷰를 클라이언트 보기에 포함 하려면 호출 `Html.ClientView('SignUp')` 대신 `Html.Partial('_SignUp')`합니다.

**전자 메일 보내기**

템플릿을 사용 하 여 전자 메일을 보내려면 [Postal](http://aboutcode.net/postal)합니다. 그러나 사용 하 여 코드의 나머지 부분에서 우편 추상화 되는는 `IMailer` 인터페이스를 쉽게 다른 구현으로 바꿀 수 있도록 합니다. 전자 메일 템플릿 보기/전자 메일 폴더에 있습니다. 보낸 사람의 전자 메일 주소는 web.config 파일에 지정 된 합니다 `sender.email` 의 키를 **appSettings** 섹션입니다. 또한, `debug="true"` 응용 프로그램 web.config에서 개발 속도 사용자 전자 메일 확인이 필요 하지 않습니다.

## <a name="github"></a>GitHub

Backbone.js SPA 템플릿의 찾을 수도 있습니다 [GitHub](https://github.com/kazimanzurrashid/AspNetMvcBackboneJsSpa)합니다.
