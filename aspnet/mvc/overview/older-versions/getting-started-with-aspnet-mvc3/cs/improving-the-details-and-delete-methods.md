---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/improving-the-details-and-delete-methods
title: 세부 정보 및 삭제 메서드 (C#)를 향상 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 인를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 설명 하는 중...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 3f42edd9-c5b8-4712-9055-970f7d38e350
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/improving-the-details-and-delete-methods
msc.type: authoredcontent
ms.openlocfilehash: 255374eb21568d05569f8af6727ad4b558acfc2f
ms.sourcegitcommit: 7b4e3936feacb1a8fcea7802aab3e2ea9c8af5b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48576445"
---
<a name="improving-the-details-and-delete-methods-c"></a>세부 정보 및 삭제 메서드 (C#) 개선
====================
[Rick Anderson]((https://twitter.com/RickAndMSFT))

> > [!NOTE]
> > 이 자습서는 업데이트 된 버전을 사용할 수 [여기](../../../getting-started/introduction/getting-started.md) 는 ASP.NET MVC 5 및 Visual Studio 2013을 사용 합니다. 보다 안전 하 고 더 간단 하 게 수행 되며 더 많은 기능을 보여 줍니다.
> 
> 
> 이 자습서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, Microsoft Visual Studio의 무료 버전인를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 설명 합니다. 시작 하기 전에 아래에 나열 된 필수 구성 요소를 설치한 다음 있는지 확인 합니다. 다음 링크를 클릭 하 여 이들 모두를 설치할 수 있습니다: [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)합니다. 또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.
> 
> - [Visual Studio Web Developer Express SP1 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 도구 업데이트](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)
> 
> Visual Studio 2010 Visual Web Developer 2010 대신를 사용 하는 경우 다음 링크를 클릭 하 여 필수 구성 요소를 설치 합니다. [Visual Studio 2010 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)합니다.
> 
> C# 소스 코드를 사용 하 여 Visual Web Developer 프로젝트는 다음이 항목과 함께 사용할 수 있습니다. [C# 버전 다운로드](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)합니다. Visual Basic을 원한다 면으로 전환 합니다 [Visual Basic 버전](../vb/intro-to-aspnet-mvc-3.md) 이 자습서의 합니다.


자습서의이 부분에서는 일부 향상 된 자동 생성 된 만들어야 `Details` 고 `Delete` 메서드. 이러한 변경 내용이 필요 하지 않습니다 하지만 몇 가지 약간의 코드를 사용 하 여 쉽게 향상 시킬 수 있습니다 응용 프로그램입니다.

## <a name="improving-the-details-and-delete-methods"></a>세부 정보 및 삭제 메서드 개선

스 캐 폴드 경우는 `Movie` 컨트롤러를 ASP.NET MVC, 작동 한 있지만 수 있도록 몇 가지 작은 변경과 더 강력한 코드를 생성 합니다.

열기는 `Movie` 컨트롤러 및 수정 합니다 `Details` 메서드를 반환 하 여 `HttpNotFound` 동영상을 찾을 수 없는 경우. 또한 수정 해야 합니다 `Details` 에 전달 되는 ID에 대 한 기본값을 설정 하는 방법. (에 비슷한 변경을 수행한 합니다 `Edit` 의 메서드 [6 부](examining-the-edit-methods-and-edit-view.md) 이 자습서의.) 하지만 반환 형식을 변경 해야 합니다 `Details` 메서드에서 `ViewResult` 에 `ActionResult`이므로 `HttpNotFound` 메서드에서 반환 하지 않는 `ViewResult` 개체. 다음 예제에서는 수정 된 `Details` 메서드.

[!code-csharp[Main](improving-the-details-and-delete-methods/samples/sample1.cs)]

코드 먼저 쉽게 사용 하 여 데이터를 검색 합니다 `Find` 메서드. 메서드로 구축한 중요 한 보안 기능을 코드 확인 되는 `Find` 메서드 코드에서 무언가를 수행 하려고 하기 전에 동영상을 발견 했습니다. 예를 들어 해커 오류가 발생할 수 사이트로 링크에서 만든 URL을 변경 하 여 `http://localhost:xxxx/Movies/Details/1` 비슷하게 `http://localhost:xxxx/Movies/Details/12345` (또는 실제 동영상을 표시 하지 않는 다른 값). Null 동영상을 확인 하지 않으면이 인해 데이터베이스 오류가 발생에서 합니다.

마찬가지로 변경 합니다 `Delete` 및 `DeleteConfirmed` ID 매개 변수에 대 한 기본값을 지정 하는 방법과 반환할 `HttpNotFound` 동영상을 찾을 수 없는 경우. 업데이트 된 `Delete` 의 메서드는 `Movie` 컨트롤러는 다음과 같습니다.

[!code-csharp[Main](improving-the-details-and-delete-methods/samples/sample2.cs)]

`Delete` 메서드 데이터를 삭제 하지 않습니다. GET 요청에 대한 응답에서 삭제 작업 수행(또는 해당 문제를 위해 편집 작업 수행, 작업 만들기 또는 데이터를 변경하는 기타 작업)은 보안 허점을 야기합니다. 이 대 한 자세한 내용은 Stephen Walther의 블로그 항목을 참조 하세요 [ASP.NET MVC 팁 #46-보안 허점을 만들기 때문에 삭제 링크를 사용 하지 않는](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)합니다.

데이터를 삭제하는 `HttpPost` 메서드는 HTTP POST 메서드에 고유한 서명 또는 이름을 제공하기 위해 `DeleteConfirmed`로 이름이 지정됩니다. 두 개의 메서드 서명은 다음과 같습니다.

[!code-csharp[Main](improving-the-details-and-delete-methods/samples/sample3.cs)]

CLR (공용 언어 런타임) 오버 로드 된 메서드 시그니처가 고유 (동일한 이름, 다른 매개 변수의 목록)에 필요 합니다. 그러나 여기 해야 삭제 메서드와-get-및 POST 둘 다 동일한 시그니처는 필요 합니다. (모두 매개 변수로 단일 정수를 허용해야 합니다.)

이 정렬 하려면 몇 가지를 수행할 수 있습니다. 하나 메서드를 서로 다른 이름을 지정 하는 것입니다. 예제에서는 이전에 수행한 것입니다. 그러나 이는 작은 문제를 가져옵니다. ASP.NET은 URL의 세그먼트를 이름으로 작업 메서드에 매핑하고 메서드의 이름을 바꾸면 정상적으로 라우팅하여 해당 메서드를 찾을 수 없게 됩니다. 솔루션은 예제에서 확인한 것으로, `ActionName("Delete")` 특성을 `DeleteConfirmed` 메서드에 추가하는 것입니다. URL을 포함 하는 수 있도록 라우팅 시스템에 대 한 매핑을 효과적으로 수행 <em>찾도록</em>게시물에 대해 요청 찾을 수는 `DeleteConfirmed` 메서드.

동일한 이름 및 시그니처가 있는 메서드를 사용 하 여 문제를 방지 하는 다른 방법은 인위적으로 변경 하는 사용 되지 않는 매개 변수를 포함 된 POST 메서드의 서명을 것입니다. 예를 들어, 일부 개발자가 추가 매개 변수 형식 `FormCollection` POST 메서드로 전달 되는 단순히 없습니다 사용 하 여 매개 변수:

[!code-csharp[Main](improving-the-details-and-delete-methods/samples/sample4.cs)]

## <a name="wrapping-up"></a>마무리

이제 SQL Server Compact 데이터베이스의 데이터를 저장 하는 전체 ASP.NET MVC 응용 프로그램을 해야 합니다. 있습니다 수 만들기, 읽기, 업데이트, 삭제 및 영화를 검색 합니다.

![](improving-the-details-and-delete-methods/_static/image1.png)

이 기본 자습서를 가져온 컨트롤러 뷰를 사용 하 여 연결 하 고 하드 코드 된 데이터를 전달 하기 시작 합니다. 생성 되 고 데이터 모델을 설계 합니다. Entity Framework Code First는 즉석에서 데이터 모델에서 데이터베이스를 생성 하 고 ASP.NET MVC 스 캐 폴딩 시스템 작업 메서드 및 기본 CRUD 작업에 대 한 뷰를 자동으로 생성 합니다. 사용자가 데이터베이스를 검색할 수 있는 검색 폼을 추가 합니다. 데이터의 새 열을 포함 하도록 데이터베이스를 변경 하 고 만들고이 새 데이터를 표시 하려면 두 페이지를 업데이트 합니다. 특성을 사용 하 여 데이터 모델을 표시 하 여 유효성 검사를 추가 합니다 `DataAnnotations` 네임 스페이스입니다. 결과 유효성 검사에는 클라이언트 및 서버에서 실행 됩니다.

응용 프로그램을 배포 하려는 경우 첫 번째 테스트 로컬 IIS 7 서버에서 응용 프로그램에 유용 합니다. 사용할 수 있습니다 [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=ASPNET;) 링크 ASP.NET 응용 프로그램에 대 한 IIS 설정을 사용 하도록 설정 합니다. 다음 배포 링크를 참조 하세요.

- [ASP.NET 배포 콘텐츠 맵](https://msdn.microsoft.com/library/dd394698.aspx)
- [IIS를 사용 하도록 설정 하면 7.x](https://blogs.msdn.com/b/rickandy/archive/2011/03/14/enabling-iis-7-x-on-windows-7-vista-sp1-windows-2008-windows-2008-r2.aspx)
- [웹 응용 프로그램 프로젝트 배포](https://msdn.microsoft.com/library/dd394698.aspx)

이 중간 수준으로 이동 하려면 이제 바랍니다 [ASP.NET MVC 응용 프로그램에 대 한 Entity Framework 데이터 모델을 만드는](../../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) 및 [MVC Music Store](../../mvc-music-store/mvc-music-store-part-1.md) 소개 자습서는 [ASP.NET msdn 문서](https://msdn.microsoft.com/library/gg416514(VS.98).aspx), 및를 다양 한 비디오 및 리소스를 확인해 [ https://asp.net/mvc ](https://asp.net/mvc) ASP.NET MVC에 대 한 더 자세한! 합니다 [ASP.NET MVC 포럼](https://forums.asp.net/1146.aspx) 질문 하기에 적합 합니다.

즐겨보세요!

-Scott Hanselman ([ http://hanselman.com ](http://hanselman.com) 하 고 [ @shanselman ](http://twitter.com/shanselman) twitter) 및 Rick Anderson [blogs.msdn.com/rickAndy](https://blogs.msdn.com/rickAndy)

> [!div class="step-by-step"]
> [이전](adding-validation-to-the-model.md)
