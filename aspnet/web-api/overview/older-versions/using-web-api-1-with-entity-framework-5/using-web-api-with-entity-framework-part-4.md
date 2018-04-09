---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-4
title: '4 단계: 추가 관리 보기 | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/04/2012
ms.topic: article
ms.assetid: 792f4513-a508-4d14-a0dd-1a2fe282c7bb
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-4
msc.type: authoredcontent
ms.openlocfilehash: cbf42f1dbd744d7b85dde7d2dcd99a13c6208a13
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="part-4-adding-an-admin-view"></a>4 단계: 관리 보기를 추가 합니다.
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트를 다운로드 합니다.](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-an-admin-view"></a>관리 보기를 추가 합니다.

이제 클라이언트 쪽 설정 알아보고 관리 컨트롤러에서 데이터를 사용할 수 있는 페이지를 추가 하겠습니다. 페이지에는 사용자 만들기, 편집 또는 제품에는 컨트롤러에 AJAX 요청을 전송 하 여 삭제할 수 있습니다.

솔루션 탐색기에서 Controllers 폴더를 확장 하 고 HomeController.cs 라는 파일을 엽니다. 이 파일에 포함 된 MVC 컨트롤러입니다. 라는 메서드를 추가 `Admin`:

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample1.cs)]

**HttpRouteUrl** 메서드는 web API에 대 한 URI를 만들고 나중에 대 한 뷰 모음에 저장이 있습니다.

다음으로 내에서 텍스트 커서의 위치는 `Admin` 작업 메서드 후 마우스 오른쪽 단추 클릭 및 선택 **뷰 추가**합니다. 그러면 표시 됩니다는 **뷰 추가** 대화 상자.

![](using-web-api-with-entity-framework-part-4/_static/image1.png)

에 **뷰 추가** 대화 상자에서 이름 보기 "Admin"입니다. 레이블이 있는 확인란을 선택 **강력한 형식의 뷰 만들기**합니다. 아래 **모델 클래스**, "Product (ProductStore.Models)"를 선택 합니다. 기본 값으로 다른 모든 옵션을 그대로 둡니다.

![](using-web-api-with-entity-framework-part-4/_static/image2.png)

클릭 하면 **추가** 뷰/홈에서 Admin.cshtml 라는 파일을 추가 합니다. 이 파일을 열고 다음 HTML을 추가 합니다. 이 HTML 페이지의 구조를 정의 하지만 기능이 없는 아직 연결 됩니다.

[!code-cshtml[Main](using-web-api-with-entity-framework-part-4/samples/sample2.cshtml)]

## <a name="create-a-link-to-the-admin-page"></a>관리 페이지에 대 한 링크 만들기

솔루션 탐색기에서 Views 폴더를 확장 한 다음 공유 폴더를 확장 합니다. 명명 된 파일을 열고 \_Layout.cshtml 합니다. 찾을 **ul** 요소 id = "메뉴" 및 관리 보기에 대 한 작업 링크:

[!code-cshtml[Main](using-web-api-with-entity-framework-part-4/samples/sample3.cshtml)]

> [!NOTE]
> 샘플 프로젝트에 내용이 몇 가지 형식적 같은 다른 변경 "사용자 로고는 여기" 문자열을 대체 합니다. 이러한 응용 프로그램의 기능에 영향을 하지 않습니다. 프로젝트를 다운로드 하 고 파일을 비교 수 있습니다.


응용 프로그램을 실행 하 고 홈 페이지의 위쪽에 표시 되는 "Admin" 링크를 클릭 합니다. 관리 페이지는 다음과 같이 표시 됩니다.

![](using-web-api-with-entity-framework-part-4/_static/image3.png)

오른쪽 이제 페이지 작업도 하지 않습니다. 다음 섹션에서 Knockout.js 동적 UI를 만들려면 사용 합니다.

## <a name="add-authorization"></a>추가 권한 부여

관리 페이지는 사이트를 방문 하는 모든를 현재 액세스할 수 있습니다. 관리자에 게 사용 권한을 제한 하려면이 옵션을 변경해 보겠습니다.

먼저 "관리자" 역할 및 관리자 사용자를 추가 합니다. 솔루션 탐색기에서 필터 폴더를 확장 하 고 InitializeSimpleMembershipAttribute.cs 라는 파일을 엽니다. 찾기의 `SimpleMembershipInitializer` 생성자입니다. 호출한 후 **WebSecurity.InitializeDatabaseConnection**, 다음 코드를 추가 합니다.

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample4.cs)]

이 간단한 방법은 "Administrator" 역할을 추가 하는 역할에 대 한 사용자를 만듭니다.

솔루션 탐색기에서 Controllers 폴더를 확장 하 고 HomeController.cs 파일을 엽니다. 추가 **Authorize** 특성을 `Admin` 메서드.

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample5.cs)]

AdminController.cs 파일을 열고 추가 된 **Authorize** 전체 특성 `AdminController` 클래스입니다.

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample6.cs)]

> [!NOTE]
> MVC 및 Web API를 모두 정의 **Authorize** 특성을 다른 네임 스페이스에 있습니다. MVC를 사용 하 여 **System.Web.Mvc.AuthorizeAttribute**, 웹 API를 사용 하는 반면, **System.Web.Http.AuthorizeAttribute**합니다.


이제 관리자만 관리 페이지를 볼 수 있습니다. 또한 관리 컨트롤러에는 HTTP 요청을 보낼 경우 요청 된 인증 쿠키를 포함 해야 합니다. 그렇지 않은 경우 서버에서 HTTP 401 (권한 없음) 응답을 보냅니다. GET 요청을 전송 하 여 Fiddler에서 볼 수 있습니다 `http://localhost:*port*/api/admin`합니다.

> [!div class="step-by-step"]
> [이전](using-web-api-with-entity-framework-part-3.md)
> [다음](using-web-api-with-entity-framework-part-5.md)
