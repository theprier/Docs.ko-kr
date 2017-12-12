---
uid: mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
title: "ASP.NET MVC 실행 프로세스를 이해 | Microsoft Docs"
author: microsoft
description: "ASP.NET MVC 프레임 워크에서 단계별 브라우저 요청을 처리 하는 방법에 대해 알아봅니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/27/2009
ms.topic: article
ms.assetid: d1608db3-660d-4079-8c15-f452ff01f1db
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
msc.type: authoredcontent
ms.openlocfilehash: 5837c6e49709d6b86ee52cd88ffd4759c1850544
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="understanding-the-aspnet-mvc-execution-process"></a>ASP.NET MVC 실행 프로세스 이해
====================
여 [Microsoft](https://github.com/microsoft)

> ASP.NET MVC 프레임 워크에서 단계별 브라우저 요청을 처리 하는 방법에 대해 알아봅니다.


ASP.NET MVC 기반 웹 응용 프로그램 요청을 통과 하는 **UrlRoutingModule** 개체 HTTP 모듈입니다. 이 모듈에서 요청을 구문 분석 하 고 경로 선택을 수행 합니다. **UrlRoutingModule** 개체가 현재 요청과 일치 하는 첫 번째 경로 개체를 선택 합니다. (경로 개체를 구현 하는 클래스는 **RouteBase**, 이며 일반적으로의 인스턴스는 **경로** 클래스입니다.) 일치 하는 경로가 없을 경우는 **UrlRoutingModule** 개체 작업이 없으며 요청이 처리 다시 일반 ASP.NET 또는 IIS 요청을 처리 합니다.

선택한 **경로** 개체는 **UrlRoutingModule** 개체를 가져옵니다는 **IRouteHandler** 연결 된 개체에는 **경로**개체입니다. 일반적으로 MVC 응용 프로그램에서이 프로그램의 인스턴스가 될 **MvcRouteHandler**합니다. **IRouteHandler** 인스턴스를 만듭니다는 **IHttpHandler** 개체 하 고 전달 된 **IHttpContext** 개체입니다. 기본적으로는 **IHttpHandler** MVC에 대 한 인스턴스는 **MvcHandler** 개체입니다. **MvcHandler** 개체 다음 최종적으로 요청을 처리 하는 컨트롤러를 선택 합니다.

> [!NOTE]
> ASP.NET MVC 웹 응용 프로그램 IIS 7.0에서 실행 되 면 파일 이름 확장명이 없는 MVC 프로젝트에 필요 합니다. 그러나 IIS 6.0에서는 처리기 해야.mvc 파일 이름 확장명을 ASP.NET ISAPI DLL에 매핑하는.


모듈 및 이벤트 처리기는 ASP.NET MVC 프레임 워크에 있는 진입점입니다. 다음 작업을 수행 합니다.

- MVC 웹 응용 프로그램에서 적절 한 컨트롤러를 선택 합니다.
- 특정 컨트롤러 인스턴스를 가져옵니다.
- 컨트롤러의 호출 **Execute** 메서드.

다음은 MVC 웹 프로젝트에 대 한 실행 단계에 대 한 설명입니다.

- 응용 프로그램에 대 한 첫 번째 요청 받기 

    - Global.asax 파일에 **경로** 개체에 추가 되는 **RouteTable** 개체입니다.
- 라우팅 수행 

    - **UrlRoutingModule** 모듈에 일치 하는 첫 번째 사용 **경로** 개체에 **RouteTable** 만들 컬렉션의 **RouteData** 개체를 사용 하 여 만들려는 **RequestContext** (**IHttpContext**) 개체입니다.
- MVC 요청 처리기 만들기 

    - **MvcRouteHandler** 개체의 인스턴스를 만듭니다는 **MvcHandler** 클래스 하 고 전달 된 **RequestContext** 인스턴스.
- 컨트롤러 만들기 

    - **MvcHandler** 개체에서 사용 하는 **RequestContext** 인스턴스를 식별 하는 **IControllerFactory** 개체 (일반적으로의 인스턴스는  **DefaultControllerFactory** 클래스) 컨트롤러 인스턴스를 만들려고 합니다.
- Execute 컨트롤러-는 **MvcHandler** 인스턴스를 호출 하는 컨트롤러 s **Execute** 메서드. |
- 작업 호출 

    - 상속 하는 대부분의 컨트롤러는 **컨트롤러** 기본 클래스입니다. 이렇게 하는 컨트롤러에 대 한는 **ControllerActionInvoker** 컨트롤러와 연결 된 개체를 호출 하려면 컨트롤러 클래스의 동작 방법을 결정 한 다음 해당 메서드를 호출 합니다.
- 결과 실행 

    - 일반적인 동작 메서드에 사용자 입력을 받을 수 있습니다, 그리고 적절 한 응답 데이터를 준비 하 고 결과 형식을 반환 하 여 결과 실행 합니다. 실행 될 수 있는 기본 제공 결과 형식은 다음과 같습니다: **ViewResult** (뷰를 렌더링 하 고 있는 가장 자주 사용 되는 결과 형식), **RedirectToRouteResult**,  **된 RedirectResult**, **ContentResult**, **JsonResult**, 및 **EmptyResult**합니다.
