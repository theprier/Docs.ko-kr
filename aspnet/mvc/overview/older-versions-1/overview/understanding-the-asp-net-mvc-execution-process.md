---
uid: mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
title: ASP.NET MVC 실행 프로세스 이해 | Microsoft Docs
author: microsoft
description: ASP.NET MVC 프레임 워크에서 단계별 브라우저 요청을 처리 하는 방법에 대해 알아봅니다.
ms.author: aspnetcontent
ms.date: 01/27/2009
ms.assetid: d1608db3-660d-4079-8c15-f452ff01f1db
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
msc.type: authoredcontent
ms.openlocfilehash: 34699c314eb862e91ecba8831c5092af9d47dc70
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37823737"
---
<a name="understanding-the-aspnet-mvc-execution-process"></a>ASP.NET MVC 실행 프로세스 이해
====================
[Microsoft](https://github.com/microsoft)

> ASP.NET MVC 프레임 워크에서 단계별 브라우저 요청을 처리 하는 방법에 대해 알아봅니다.


ASP.NET MVC 기반 웹 응용 프로그램에 대 한 요청을 통해 먼저 전달 합니다 **UrlRoutingModule** 개체는 HTTP 모듈입니다. 이 모듈 요청을 구문 분석 하 고 경로 선택을 수행 합니다. 합니다 **UrlRoutingModule** 개체가 현재 요청과 일치 하는 첫 번째 경로 개체를 선택 합니다. (경로 개체는 구현 하는 클래스 **RouteBase**, 이며 인스턴스는 일반적으로 **경로** 클래스입니다.) 경로가 일치 하는 경우는 **UrlRoutingModule** 개체 아무 작업도 수행 하지 및 대체 일반 ASP.NET 또는 IIS 요청 처리 요청을 수 있습니다.

선택한 **경로** 개체를 **UrlRoutingModule** 개체를 가져옵니다 합니다 **IRouteHandler** 연관 된 개체는 **경로**개체입니다. 일반적으로 MVC 응용 프로그램에서이의 인스턴스여야 **MvcRouteHandler**합니다. 합니다 **IRouteHandler** 인스턴스를 만듭니다를 **IHttpHandler** 개체를 전달 합니다 **IHttpContext** 개체입니다. 기본적으로 **IHttpHandler** MVC에 대 한 인스턴스를 **MvcHandler** 개체입니다. 합니다 **MvcHandler** 개체에는 다음 최종적으로 요청을 처리 하는 컨트롤러를 선택 합니다.

> [!NOTE]
> ASP.NET MVC 웹 응용 프로그램을 IIS 7.0에서 실행 되 면 파일 이름 확장명이 없는 경우 MVC 프로젝트에 필요 하므로 그러나 IIS 6.0에서는 처리기가 ASP.NET ISAPI DLL에 따라.mvc 파일 확장명에 매핑하는 합니다.


모듈 및 처리기는 ASP.NET MVC 프레임 워크에 대 한 진입점입니다. 다음 작업을 수행합니다.

- MVC 웹 응용 프로그램에서 적절 한 컨트롤러를 선택 합니다.
- 특정 컨트롤러 인스턴스를 가져옵니다.
- 컨트롤러의 호출 **Execute** 메서드.

다음은 MVC 웹 프로젝트에 대 한 실행의 모든 단계에 대 한 목록입니다.

- 응용 프로그램에 대 한 첫 번째 요청 받기 

    - Global.asax 파일에서 **경로** 개체에 추가 되는 **RouteTable** 개체입니다.
- 라우팅 수행 

    - **UrlRoutingModule** 모듈의 첫 번째 일치를 사용 **경로** 개체를 **RouteTable** 만들려는 컬렉션의 **RouteData** 그런 다음 만들기를 사용 하는 개체를 **RequestContext** (**IHttpContext**) 개체입니다.
- MVC 요청 처리기 만들기 

    - **MvcRouteHandler** 개체의 인스턴스를 만듭니다 합니다 **MvcHandler** 클래스를 전달 합니다 **RequestContext** 인스턴스.
- 컨트롤러 만들기 

    - **MvcHandler** 개체에서 사용 하는 **RequestContext** 인스턴스를 식별 하는 **IControllerFactory** 개체 (일반적으로 인스턴스를  **DefaultControllerFactory** 클래스)를 사용 하 여 컨트롤러 인스턴스를 만듭니다.
- Execute 컨트롤러-합니다 **MvcHandler** s 컨트롤러를 호출 하는 인스턴스 **Execute** 메서드. |
- 작업 호출 

    - 대부분의 컨트롤러에서 상속 된 **컨트롤러** 기본 클래스입니다. 이렇게 하는 컨트롤러에 대 한 합니다 **ControllerActionInvoker** 컨트롤러와 연결 된 개체를 호출 하려면 컨트롤러 클래스의 동작 방법을 결정 합니다. 해당 메서드를 호출 합니다.
- 결과 실행 

    - 일반적인 동작 메서드를 사용자 입력을 받을 수 있습니다, 그리고 적절 한 응답 데이터 준비 및 결과 형식을 반환 하 여 결과 실행 한 다음 실행할 수 있는 기본 제공 결과 형식은 다음과 같습니다: **ViewResult** 는 뷰를 렌더링과 가장 자주 사용 되는 결과 형식입니다 **RedirectToRouteResult**,  **된 RedirectResult**, **ContentResult**합니다 **JsonResult**, 및 **EmptyResult**합니다.
