---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
title: '1 부: 개요 및 프로젝트 만들기 | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/03/2012
ms.topic: article
ms.assetid: 94421d86-68c4-4471-bf5f-82d654a17252
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
msc.type: authoredcontent
ms.openlocfilehash: f9cdff0cb0cad9adad546c8f8d46ba9b010e1079
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30873328"
---
<a name="part-1-overview-and-creating-the-project"></a>1 부: 개요 및 프로젝트 만들기
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트를 다운로드 합니다.](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

Entity Framework는 개체/관계형 매핑 프레임 워크입니다. 코드에서 도메인 개체를 관계형 데이터베이스의 엔터티에 매핑됩니다. 대부분의 경우 않아도 데이터베이스 계층에 대 한 걱정 Entity Framework에서는 자동으로 하기 때문에 있습니다. 코드는 개체를 조작 하 고 변경 내용이 데이터베이스에 유지 됩니다.

## <a name="about-the-tutorial"></a>자습서 정보

이 자습서에서는 단순한 스토어 응용 프로그램이 만들어집니다. 응용 프로그램에 두 가지 요소가 있습니다. 일반 사용자가 제품을 볼 수 있고 주문을 작성 됩니다.

![](using-web-api-with-entity-framework-part-1/_static/image1.png)

관리자 만들기, 삭제 또는 제품 편집 수 있습니다.:

![](using-web-api-with-entity-framework-part-1/_static/image2.png)

## <a name="skills-youll-learn"></a>기술을 알아봅니다

학습할 다음과 같습니다.

- ASP.NET 웹 API와 함께 Entity Framework를 사용 하는 방법.
- Knockout.js 동적 클라이언트 UI를 만들려면 사용 하는 방법입니다.
- 사용자를 인증 웹 API와 함께 폼 인증을 사용 하는 방법.

이 자습서는 독립적인 항목 있지만 다음과 같은 자습서를 우선 확인 해야 할 수 있습니다.

- [첫 번째 ASP.NET Web API](../../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)
- [CRUD 작업을 지원 하는 Web API 만들기](../creating-a-web-api-that-supports-crud-operations.md)

약간의 지식이 [ASP.NET MVC](../../../../mvc/index.md) 에 도움이 됩니다.

## <a name="overview"></a>개요

상위 수준 응용 프로그램의 아키텍처는 다음과 같습니다.

- ASP.NET MVC의 클라이언트에 대 한 HTML 페이지를 생성합니다.
- ASP.NET Web API (products 및 orders) 데이터에 대해 CRUD 작업을 표시합니다.
- Entity Framework 웹 API 데이터베이스 엔터티를 사용 하는 C# 모델을 변환 합니다.

![](using-web-api-with-entity-framework-part-1/_static/image3.png)

다음 다이어그램은 응용 프로그램의 다양 한 계층에서 도메인 개체 표현 되는 방식을 보여 줍니다: 데이터베이스 계층, 개체 모델 및 마지막으로 통신 형식에 HTTP 통해 클라이언트에 데이터를 전송 하는 데 사용 됩니다.

![](using-web-api-with-entity-framework-part-1/_static/image4.png)

## <a name="create-the-visual-studio-project"></a>Visual Studio 프로젝트 만들기

Visual Web Developer Express 또는 정식 버전의 Visual Studio를 사용 하 여 자습서 프로젝트를 만들 수 있습니다.

**시작** 페이지 **새 프로젝트**합니다.

에 **템플릿** 창 선택 **설치 된 템플릿** 확장는 **Visual C#** 노드. 아래 **Visual C#** 선택, **웹**합니다. 프로젝트 템플릿 목록에서 선택 **ASP.NET MVC 4 웹 응용 프로그램**합니다. "ProductStore" 프로젝트 이름을 지정 하 고 클릭 **확인**합니다.

![](using-web-api-with-entity-framework-part-1/_static/image5.png)

에 **새 ASP.NET MVC 4 프로젝트** 대화 상자에서 **인터넷 응용 프로그램** 클릭 **확인**합니다.

![](using-web-api-with-entity-framework-part-1/_static/image6.png)

"인터넷 응용 프로그램" 템플릿은 폼 인증을 지 원하는 ASP.NET MVC 응용 프로그램을 만듭니다. 지금 응용 프로그램을 실행 하는 경우 일부 기능이 이미 있습니다.

- 오른쪽 위 모서리에 있는 "Register" 링크를 클릭 하 여 새 사용자가 등록할 수 있습니다.
- "로그인" 링크를 클릭 하 여 등록된 한 사용자 로그인 수입니다.

멤버 자격 정보는 자동으로 생성 되는 데이터베이스에 유지 됩니다. ASP.NET MVC에서 폼 인증에 대 한 자세한 내용은 참조 [연습: ASP.NET MVC에서 폼 인증을 사용 하 여](https://msdn.microsoft.com/library/ff398049(VS.98).aspx)합니다.

## <a name="update-the-css-file"></a>CSS 파일 업데이트

이 단계는 cosmetic이 고, 이지만 이전 스크린 샷 같은 렌더링 하는 페이지입니다.

솔루션 탐색기에서 콘텐츠 폴더를 확장 하 고 Site.css 라는 파일을 엽니다. 다음과 같은 CSS 스타일을 추가 합니다.

[!code-css[Main](using-web-api-with-entity-framework-part-1/samples/sample1.css)]

> [!div class="step-by-step"]
> [다음](using-web-api-with-entity-framework-part-2.md)
