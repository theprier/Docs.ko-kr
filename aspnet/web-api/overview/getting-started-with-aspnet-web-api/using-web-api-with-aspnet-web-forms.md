---
uid: web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
title: ASP.NET Web Forms를 사용 하 여 웹 API를 사용 하 여 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/03/2012
ms.topic: article
ms.assetid: 25da8c3f-4e90-4946-9765-4f160985e1e4
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
msc.type: authoredcontent
ms.openlocfilehash: 91811031b937d3ca05888ce8d4f28bcc33537c76
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37400881"
---
<a name="using-web-api-with-aspnet-web-forms"></a>ASP.NET Web Forms를 사용 하 여 웹 API를 사용 하 여
====================
[Mike Wasson](https://github.com/MikeWasson)

ASP.NET Web API는 ASP.NET MVC를 사용 하 여 패키지를 이지만 쉽게 기존의 ASP.NET Web Forms 응용 프로그램에 Web API를 추가할 수 있습니다. 이 자습서의 단계를 안내합니다.

## <a name="overview"></a>개요

Web Forms 응용 프로그램에서 웹 API를 사용 하려면 두 가지 주요 단계:

- 파생 되는 Web API 컨트롤러를 추가 합니다 **ApiController** 클래스입니다.
- 경로 테이블을 추가 합니다 **응용 프로그램\_시작** 메서드.

## <a name="create-a-web-forms-project"></a>Web Forms 프로젝트 만들기

Visual Studio를 시작 하 고 선택 **새 프로젝트** 에서 합니다 **시작** 페이지입니다. 또는에서 **파일** 메뉴에서 **새로 만들기** 차례로 **프로젝트**합니다.

에 **템플릿** 창 **설치 된 템플릿** 확장 하 고는 **Visual C#** 노드. 아래 **Visual C#** 를 선택 **웹**합니다. 프로젝트 템플릿 목록에서 선택 **ASP.NET Web Forms 응용 프로그램**합니다. 프로젝트에 대 한 이름을 입력 하 고 클릭 **확인**합니다.

![](using-web-api-with-aspnet-web-forms/_static/image1.png)

## <a name="create-the-model-and-controller"></a>모델 및 컨트롤러 만들기

이 자습서와 동일한 모델 및 컨트롤러 클래스를 사용 합니다 [Getting Started](tutorial-your-first-web-api.md) 자습서입니다.

먼저 모델 클래스를 추가 합니다. **솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 **클래스 추가**합니다. 제품에 클래스 이름을 지정 하 고 다음 구현을 추가 합니다.

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample1.cs)]

그런 다음에 프로젝트에는 Web API 컨트롤러를 추가 *컨트롤러* 는 웹 API에 대 한 HTTP 요청을 처리 하는 개체입니다.

**솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 클릭 합니다. 선택 **새 항목 추가**합니다.

![](using-web-api-with-aspnet-web-forms/_static/image2.png)

아래 **설치 된 템플릿**를 확장 하 고 **Visual C#** 선택한 **웹**합니다. 그런 다음 템플릿의 목록에서 선택 **Web API 컨트롤러 클래스**합니다. "ProductsController" 컨트롤러 이름을 지정 하 고 클릭 **추가**합니다.

![](using-web-api-with-aspnet-web-forms/_static/image3.png)

합니다 **새 항목 추가** ProductsController.cs 라는 파일을 자동으로 만들어집니다. 마법사를 포함 하는 메서드를 삭제 하 고 다음 메서드를 추가 합니다.

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample2.cs)]

이 컨트롤러의 코드에 대 한 자세한 내용은 참조는 [Getting Started](tutorial-your-first-web-api.md) 자습서입니다.

## <a name="add-routing-information"></a>라우팅 정보를 추가 합니다.

다음으로, 추가 URI 경로 이므로 폼의 해당 Uri &quot;/a pi/제품/&quot; 컨트롤러로 라우팅됩니다.

**솔루션 탐색기**, 코드 숨김 파일 Global.asax.cs Global.asax를 두 번 클릭 합니다. 다음을 추가 합니다 **를 사용 하 여** 문입니다.

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample3.cs)]

다음 코드를 추가 합니다 **응용 프로그램\_시작** 메서드:

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample4.cs)]

라우팅 테이블에 대 한 자세한 내용은 참조 하십시오 [ASP.NET Web API에서 라우팅](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)합니다.

## <a name="add-client-side-ajax"></a>클라이언트 쪽 AJAX를 추가 합니다.

이것이 전부 웹 클라이언트가 액세스할 수 있는 API를 생성 해야 합니다. 이제 jQuery를 사용 하 여 API를 호출 하는 HTML 페이지를 추가 해 보겠습니다.

마스터 페이지에 있는지 확인 (예를 들어 *Site.Master*) 포함 된 `ContentPlaceHolder` 사용 하 여 `ID="HeadContent"`:

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample8.html)]

Default.aspx 파일을 엽니다. 표시 된 것 처럼 주 콘텐츠 섹션에 있는 상용구 텍스트를 바꿉니다.

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample5.aspx)]

다음으로, jQuery 원본 파일에 대 한 참조를 추가 합니다 `HeaderContent` 섹션:

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample6.aspx?highlight=2)]

참고: 쉽게 추가할 수 있습니다 스크립트 참조의 파일을 끌어서 놓아 **솔루션 탐색기** 코드 편집기 창에 있습니다.

![](using-web-api-with-aspnet-web-forms/_static/image4.png)

JQuery 스크립트 태그 아래 다음 스크립트 블록을 추가 합니다.

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample7.html)]

이 스크립트는 AJAX 요청에 문서가 로드 되 면 &quot;api/제품&quot;합니다. 요청에는 JSON 형식으로 제품 목록을 반환합니다. 스크립트를 HTML 테이블에는 제품 정보를 추가합니다.

응용 프로그램을 실행 하면 다음과 같아야 합니다.

![](using-web-api-with-aspnet-web-forms/_static/image5.png)
