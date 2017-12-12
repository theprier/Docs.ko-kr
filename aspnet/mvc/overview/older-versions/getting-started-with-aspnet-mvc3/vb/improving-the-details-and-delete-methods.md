---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/improving-the-details-and-delete-methods
title: "세부 정보 및 삭제 메서드 (VB) 개선 | Microsoft Docs"
author: Rick-Anderson
description: "이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 즉를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 구축 하는 기초 설명..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2011
ms.topic: article
ms.assetid: c5c14ef0-c128-4dc1-8c01-7f0fdb09e411
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/improving-the-details-and-delete-methods
msc.type: authoredcontent
ms.openlocfilehash: 24c986f7ec8376bc997f1ebc575338772507cbc9
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="improving-the-details-and-delete-methods-vb"></a>세부 정보 및 삭제 메서드 (VB) 향상
====================
으로 [Rick Anderson](https://github.com/Rick-Anderson)

> 이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 즉 Microsoft Visual Studio의 무료 버전을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 구축 하는 기초 설명 합니다. 시작 하기 전에 아래에 나열 된 필수 구성 요소가 설치 되어 있는지 확인 합니다. 다음 링크를 클릭 하 여 모두를 설치할 수 있습니다: [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)합니다. 또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.
> 
> - [Visual Studio Web Developer Express SP1 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 도구 업데이트](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)
> 
> Visual Studio 2010 Visual Web Developer 2010 대신를 사용 하는 경우 다음 링크를 클릭 하 여 필수 구성 요소 설치: [Visual Studio 2010 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)합니다.
> 
> 이 항목에 수반 VB.NET 소스 코드를 사용 하 여 Visual Web Developer 프로젝트 ´ ù. [VB.NET 버전을 다운로드](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)합니다. 원하는 경우 C#으로 전환 된 [C# 버전](../cs/improving-the-details-and-delete-methods.md) 이 자습서의 합니다.


자습서의이 부분에서는 할 몇 가지 향상 된 자동으로 생성 된 `Details` 및 `Delete` 메서드. 이러한 변경 내용은 필수는 아니지만 몇 가지 약간의 코드를 있는 쉽게 향상 시킬 수 있습니다는 응용 프로그램입니다.

## <a name="improving-the-details-and-delete-methods"></a>세부 정보 및 삭제 메서드를 개선합니다.

때 있습니다 스 캐 폴드 된는 `Movie` 컨트롤러, ASP.NET MVC 보다 강력한 몇 개의 작은 변경 내용으로 변경할 수는 없지만 다행, 작동 한 코드를 생성 합니다.

열기는 `Movie` 컨트롤러를 수정 하 고는 `Details` 메서드를 반환 하 여 `HttpNotFound` 영화를 찾을 수 없을 때. 수정 해야는 `Details` 메서드를 전달 되는 ID에 대 한 기본값을 설정 합니다. (유사한의 변경 된 `Edit` 에서 메서드 [6 부](examining-the-edit-methods-and-edit-view.md) 이 자습서의 합니다.) 하지만 반환 형식을 변경 해야는 `Details` 에서 메서드 `ViewResult` 를 `ActionResult`때문에 `HttpNotFound` 을 반환 하지 않는 한 `ViewResult` 개체입니다. 다음 예에서는 수정 된 `Details` 메서드.

[!code-vb[Main](improving-the-details-and-delete-methods/samples/sample1.vb)]

코드 먼저 쉽게 사용 하 여 데이터를 검색 하는 `Find` 메서드. म 메서드에 구성 하는 중요 한 보안 기능 코드 확인 되는 `Find` 메서드 코드와 어떤 작업을 시도 하기 전에 동영상을 발견 했습니다. 예를 들어 해커가 오류가 발생할 수를 사이트에 링크를에서 만든 URL을 변경 하 여 `http://localhost:xxxx/Movies/Details/1` 같이 `http://localhost:xxxx/Movies/Details/12345` (또는 실제 영화 표시 되지 않은 다른 값). Null 동영상에 대 한 검사를 지정 하지 않으면 데이터베이스 오류가 될 수 있습니다.

마찬가지로, 변경 된 `Delete` 및 `DeleteConfirmed` ID 매개 변수의 기본값을 지정 하 고 반환 하는 방법 `HttpNotFound` 영화를 찾을 수 없을 때. 업데이트 된 `Delete` 의 메서드는 `Movie` 컨트롤러는 다음과 같습니다.

[!code-vb[Main](improving-the-details-and-delete-methods/samples/sample2.vb)]

`Delete` 메서드 데이터를 삭제 하지 않습니다. GET 요청에 대한 응답에서 삭제 작업 수행(또는 해당 문제를 위해 편집 작업 수행, 작업 만들기 또는 데이터를 변경하는 기타 작업)은 보안 허점을 야기합니다. 이 대 한 자세한 내용은 Stephen Walther 블로그 항목을 참조 하십시오. [ASP.NET MVC 팁 #46-보안 허점을 만들기 때문에 삭제 링크를 사용 하지 않는](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)합니다.

데이터를 삭제하는 `HttpPost` 메서드는 HTTP POST 메서드에 고유한 서명 또는 이름을 제공하기 위해 `DeleteConfirmed`로 이름이 지정됩니다. 두 개의 메서드 서명은 다음과 같습니다.

[!code-vb[Main](improving-the-details-and-delete-methods/samples/sample3.vb)]

공용 언어 런타임 (CLR) (동일한 이름, 매개 변수 목록이 서로 다른)에 고유의 시그니처가 있어야 하는 오버 로드 된 메서드를 필요 합니다. 그러나 여기 해야 두 삭제 메서드-각각에 대 한 GET-와 게시에 두 동일한 서명 해야 합니다. (모두 매개 변수로 단일 정수를 허용해야 합니다.)

이 출력을 정렬 하려면 몇 가지 기능을 수행할 수 있습니다. 하나는 메서드를 서로 다른 이름을 지정입니다. 그 예에서는 앞에서 수행한 것입니다. 그러나 이는 작은 문제를 가져옵니다. ASP.NET은 URL의 세그먼트를 이름으로 작업 메서드에 매핑하고 메서드의 이름을 바꾸면 정상적으로 라우팅하여 해당 메서드를 찾을 수 없게 됩니다. 솔루션은 예제에서 확인한 것으로, `ActionName("Delete")` 특성을 `DeleteConfirmed` 메서드에 추가하는 것입니다. 포함 하는 URL 라우팅 시스템에 대 한 매핑을 효과적으로 수행 */Delete/*게시물에 대 한 요청 찾을 수는 `DeleteConfirmed` 메서드.

동일한 이름 및 시그니처가 있는 메서드에서 문제를 방지 하는 다른 방법은 인위적으로 사용 되지 않는 매개 변수를 포함 하도록 POST 메서드의 시그니처를 변경 하는 것입니다. 예를 들어, 일부 개발자가 추가 매개 변수 형식 `FormCollection` POST 메서드에 전달 되는 다음 단순히 하지 않는 매개 변수를 사용 하 고 있습니다.

[!code-vb[Main](improving-the-details-and-delete-methods/samples/sample4.vb)]

## <a name="wrapping-up"></a>정리

이제 SQL Server Compact 데이터베이스에 데이터를 저장 하는 전체 ASP.NET MVC 응용 프로그램을 준비 되었습니다. 있습니다 수 만들기, 읽기, 업데이트, 삭제 및 영화를 검색 합니다.

![](improving-the-details-and-delete-methods/_static/image1.png)

이 기본 자습서 컨트롤러, 뷰와 연관 하 고 하드 코드 된 데이터에 대 한 전달 하기 시작 했습니다. 생성 하 고이 정보는 데이터 모델을 설계 합니다. Entity Framework Code First 데이터 모델은 바로 데이터베이스를 만든 및 ASP.NET MVC 스 캐 폴딩 시스템의 작업 메서드 및 한 기본적인 CRUD 작업에 대 한 보기를 자동으로 생성 합니다. 사용자가 데이터베이스를 검색할 수 있도록 하는 검색 폼을 추가 합니다. 데이터를 새 열을 포함 하도록 데이터베이스를 변경 하 고 그런 다음 두 페이지를 만들고이 새 데이터를 표시 합니다. 유효성 검사 특성을 사용 하 여 데이터 모델을 표시 하 여 추가 된 `DataAnnotations` 네임 스페이스입니다. 결과 유효성 검사는 클라이언트와 서버를 실행합니다.

응용 프로그램을 배포 하려는 경우에 첫 번째 테스트 로컬 IIS 7 서버에서 응용 프로그램에 도움이 됩니다. 이 사용 하 여 [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=ASPNET;) 링크 ASP.NET 응용 프로그램에 대 한 IIS 설정을 사용 하도록 설정 합니다. 다음 배포 링크를 참조 하십시오.

- [ASP.NET 배포 콘텐츠 맵](https://msdn.microsoft.com/en-us/library/dd394698.aspx)
- [IIS를 사용 하도록 설정 7.x](https://blogs.msdn.com/b/rickandy/archive/2011/03/14/enabling-iis-7-x-on-windows-7-vista-sp1-windows-2008-windows-2008-r2.aspx)
- [웹 응용 프로그램 프로젝트 배포](https://msdn.microsoft.com/en-us/library/dd394698.aspx)

이 중간 수준으로 이동 이제 확인해 [ASP.NET MVC 응용 프로그램에 대 한 Entity Framework 데이터 모델을 만드는](../../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) 및 [MVC Music Store](../../mvc-music-store/mvc-music-store-part-1.md) 자습서 탐색 하는 [ASP.NET MSDN에 대 한 문서](https://msdn.microsoft.com/en-us/library/gg416514(VS.98).aspx), 많은 비디오 및 리소스에을 체크 아웃 하 고 [https://asp.net/mvc](https://asp.net/mvc) ASP.NET MVC에 대해 훨씬 더 자세한! [ASP.NET MVC 포럼](https://forums.asp.net/1146.aspx) 질문 하기에 적합 합니다.

원하는 작업 합니다.

-Scott Hanselman ([http://hanselman.com](http://hanselman.com) 및 [ @shanselman ](http://twitter.com/shanselman) Twitter의) 및 Rick Anderson [blogs.msdn.com/rickAndy](https://blogs.msdn.com/rickAndy)

>[!div class="step-by-step"]
[이전](adding-validation-to-the-model.md)
