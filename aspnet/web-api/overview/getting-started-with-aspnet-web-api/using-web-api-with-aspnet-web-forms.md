---
uid: web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
title: Web API를 사용 하 여 ASP.NET Web forms | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/03/2012
ms.topic: article
ms.assetid: 25da8c3f-4e90-4946-9765-4f160985e1e4
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
msc.type: authoredcontent
ms.openlocfilehash: af918671a8bcc97a0050ea033ccd14dd96416e73
ms.sourcegitcommit: 037d3900f739dbaa2ba14158e3d7dc81478952ad
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/01/2017
---
<a name="using-web-api-with-aspnet-web-forms"></a>Web API를 사용 하 여 ASP.NET Web forms
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

ASP.NET Web API는 ASP.NET MVC와 함께 패키지 되어, 하지만 기존 ASP.NET Web Forms 응용 프로그램에 Web API를 추가 하려면 쉽습니다. 이 자습서의 단계를 안내합니다.

## <a name="overview"></a>개요

Web Forms 응용 프로그램을 웹 API를 사용 하려면 두 가지 주요 단계가 있습니다.

- 파생 된 웹 API 컨트롤러 추가 **ApiController** 클래스입니다.
- 경로 테이블을 추가 하는 **응용 프로그램\_시작** 메서드.

## <a name="create-a-web-forms-project"></a>Web Forms 프로젝트 만들기

Visual Studio를 시작 하 고 선택 **새 프로젝트** 에서 **시작** 페이지. 또는에서 **파일** 메뉴 선택 **새로** 차례로 **프로젝트**합니다.

에 **템플릿** 창 선택 **설치 된 템플릿** 확장는 **Visual C#** 노드. 아래 **Visual C#** 선택, **웹**합니다. 프로젝트 템플릿 목록에서 선택 **ASP.NET Web Forms 응용 프로그램**합니다. 프로젝트에 대 한 이름을 입력 하 고 클릭 **확인**합니다.

![](using-web-api-with-aspnet-web-forms/_static/image1.png)

## <a name="create-the-model-and-controller"></a>모델과 컨트롤러 만들기

이 자습서로 동일한 모델 및 컨트롤러 클래스를 사용 하 여 [시작](tutorial-your-first-web-api.md) 자습서입니다.

먼저, 모델 클래스를 추가 합니다. **솔루션 탐색기**프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **클래스 추가**합니다. 제품 클래스 이름을 지정 하 고 다음 구현을 추가 합니다.

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample1.cs)]

다음으로 프로젝트에, A Web API 컨트롤러 추가 *컨트롤러* 웹 API에 대 한 HTTP 요청을 처리 하는 개체입니다.

**솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 클릭 합니다. 선택 **새 항목 추가**합니다.

![](using-web-api-with-aspnet-web-forms/_static/image2.png)

아래 **설치 된 템플릿**를 확장 하 고 **Visual C#** 선택 **웹**합니다. 다음 템플릿 목록에서 선택 **Web API 컨트롤러 클래스**합니다. "ProductsController" 컨트롤러 이름을 지정 하 고 클릭 **추가**합니다.

![](using-web-api-with-aspnet-web-forms/_static/image3.png)

**새 항목 추가** 마법사 ProductsController.cs 라는 파일이 만들어집니다. 마법사를 포함 하는 메서드를 삭제 하 고 다음 메서드를 추가 합니다.

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample2.cs)]

이 컨트롤러에 코드에 대 한 자세한 내용은 참조는 [시작](tutorial-your-first-web-api.md) 자습서입니다.

## <a name="add-routing-information"></a>라우팅 정보를 추가 합니다.

다음으로 추가 URI 경로 이므로 형식의 해당 Uri &quot;/api/제품/&quot; 컨트롤러에 라우팅됩니다.

**솔루션 탐색기**, Global.asax Global.asax.cs 코드 숨김 파일을 열 수를 두 번 클릭 합니다. 다음 추가 **를 사용 하 여** 문.

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample3.cs)]

다음 코드를 다음 추가 **응용 프로그램\_시작** 메서드:

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample4.cs)]

라우팅 테이블에 대 한 자세한 내용은 참조 [ASP.NET Web API에서 라우팅](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)합니다.

## <a name="add-client-side-ajax"></a>클라이언트 쪽 AJAX를 추가 합니다.

웹 클라이언트가 액세스할 수 있는 API를 만드는 하면 됩니다. 이제 jQuery를 사용 하 여 API를 호출 하는 HTML 페이지를 추가 해 보겠습니다.

마스터 페이지에 있는지 확인 (예를 들어 *Site.Master*)를 포함 한 `ContentPlaceHolder` 와 `ID="HeadContent"`:

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample8.html)]

Default.aspx 파일을 엽니다. 표시 된 것 처럼 주 콘텐츠 섹션에 있는 상용구 텍스트를 바꿉니다.

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample5.aspx)]

다음으로에서 jQuery 소스 파일에 대 한 참조를 추가 `HeaderContent` 섹션:

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample6.aspx?highlight=2)]

참고: 쉽게 추가할 수 있습니다 스크립트 참조에서 파일을 끌어다 **솔루션 탐색기** 코드 편집기 창에 있습니다.

![](using-web-api-with-aspnet-web-forms/_static/image4.png)

JQuery 스크립트 태그 아래 다음과 같은 스크립트 블록을 추가 합니다.

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample7.html)]

이 스크립트는 AJAX 요청을 사용 하면 문서 로드 될 때 &quot;api/제품&quot;합니다. 요청이는 JSON 형식으로 제품 목록을 반환합니다. 스크립트는 HTML 테이블에는 제품 정보를 추가합니다.

응용 프로그램을 실행 하면 다음과 같이 표시 됩니다.

![](using-web-api-with-aspnet-web-forms/_static/image5.png)
