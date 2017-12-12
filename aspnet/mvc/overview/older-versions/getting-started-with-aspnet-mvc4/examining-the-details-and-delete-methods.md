---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-details-and-delete-methods
title: "세부 정보 및 삭제 메서드 검사 | Microsoft Docs"
author: Rick-Anderson
description: "참고:이 자습서의 업데이트 된 버전은 ASP.NET MVC 5 및 Visual Studio 2013을 사용 하는 있습니다. 것이 더 안전 하 고 진행할 데모를 단순..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/28/2012
ms.topic: article
ms.assetid: 11425ff3-09fc-4efa-be9a-b53bce503460
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-details-and-delete-methods
msc.type: authoredcontent
ms.openlocfilehash: 213626147424e08d10d6442034ec450174200b09
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="examining-the-details-and-delete-methods"></a>세부 정보 및 삭제 메서드를 검사합니다.
====================
으로 [Rick Anderson](https://github.com/Rick-Anderson)

> > [!NOTE]
> > 이 자습서의 업데이트 된 버전은 사용할 수 있는 [여기](../../getting-started/introduction/getting-started.md) ASP.NET MVC 5 및 Visual Studio 2013을 사용 하 합니다. 더 안전 하 고 따라 하기 쉽고 이며 더 많은 기능을 보여 줍니다.


자습서의이 부분에서는 검토해 자동으로 생성 된 `Details` 및 `Delete` 메서드.

## <a name="examining-the-details-and-delete-methods"></a>세부 정보 및 삭제 메서드를 검사합니다.

열기는 `Movie` 컨트롤러 검사는 `Details` 메서드.

![](examining-the-details-and-delete-methods/_static/image1.png)

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample1.cs)]

이 작업 메서드를 만든 MVC 스 캐 폴딩 엔진 메서드를 호출 하는 HTTP 요청을 보여 주는 메모를 추가 합니다. 이 경우에 `GET` URL 세그먼트를 사용 하 여 요청은 `Movies` 컨트롤러는 `Details` 메서드 및 `ID` 값입니다.

코드 먼저 쉽게 사용 하 여 데이터를 검색 하는 `Find` 메서드. 메서드에 구성 하는 중요 한 보안 기능 코드 확인 되는 `Find` 메서드 코드와 어떤 작업을 시도 하기 전에 동영상을 발견 했습니다. 예를 들어 해커가 오류가 발생할 수를 사이트에 링크를에서 만든 URL을 변경 하 여 `http://localhost:xxxx/Movies/Details/1` 같이 `http://localhost:xxxx/Movies/Details/12345` (또는 실제 영화 표시 되지 않은 다른 값). Null 동영상에 대 한 선택 하지 않은 경우 null 영화, 데이터베이스 오류가 생깁니다.

`Delete` 및 `DeleteConfirmed` 메서드를 검사합니다.

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample2.cs?highlight=17)]

`HTTP Get``Delete` 메서드는 지정 된 영화를 삭제 하지 않습니다, 동영상의 보기 반환 제출할 수 있습니다 (`HttpPost`) 삭제... GET 요청에 대한 응답에서 삭제 작업 수행(또는 해당 문제를 위해 편집 작업 수행, 작업 만들기 또는 데이터를 변경하는 기타 작업)은 보안 허점을 야기합니다. 이 대 한 자세한 내용은 Stephen Walther 블로그 항목을 참조 하십시오. [ASP.NET MVC 팁 #46-보안 허점을 만들기 때문에 삭제 링크를 사용 하지 않는](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)합니다.

데이터를 삭제하는 `HttpPost` 메서드는 HTTP POST 메서드에 고유한 서명 또는 이름을 제공하기 위해 `DeleteConfirmed`로 이름이 지정됩니다. 두 개의 메서드 서명은 다음과 같습니다.

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample3.cs)]

CLR(공용 언어 런타임)은 고유한 매개 변수 서명을 갖기 위해 오버로드된 메서드가 필요합니다(동일한 메서드 이름이지만 다른 매개 변수의 목록). 그러나 여기 해야 두 삭제 메서드-각각에 대 한 GET-와 게시에 매개 변수 시그니처를 포함 하는 두 합니다. (모두 매개 변수로 단일 정수를 허용해야 합니다.)

이 출력을 정렬 하려면 몇 가지 기능을 수행할 수 있습니다. 하나는 메서드를 서로 다른 이름을 지정입니다. 앞의 예에서 스캐폴딩 메커니즘이 수행한 것입니다. 그러나 이는 작은 문제를 가져옵니다. ASP.NET은 URL의 세그먼트를 이름으로 작업 메서드에 매핑하고 메서드의 이름을 바꾸면 정상적으로 라우팅하여 해당 메서드를 찾을 수 없게 됩니다. 솔루션은 예제에서 확인한 것으로, `ActionName("Delete")` 특성을 `DeleteConfirmed` 메서드에 추가하는 것입니다. 포함 하는 URL 라우팅 시스템에 대 한 매핑을 효과적으로 수행 */Delete/*게시물에 대 한 요청 찾을 수는 `DeleteConfirmed` 메서드.

동일한 이름 및 시그니처가 있는 메서드에서 문제를 방지 하는 다른 일반적인 방법은 인위적으로 사용 되지 않는 매개 변수를 포함 하도록 POST 메서드의 시그니처를 변경 하는 것입니다. 예를 들어, 일부 개발자가 추가 매개 변수 형식 `FormCollection` POST 메서드에 전달 되는 다음 단순히 하지 않는 매개 변수를 사용 하 고 있습니다.

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample4.cs)]

## <a name="summary"></a>요약

이제 로컬 DB 데이터베이스에 데이터를 저장 하는 전체 ASP.NET MVC 응용 프로그램을 준비 되었습니다. 있습니다 수 만들기, 읽기, 업데이트, 삭제 및 영화를 검색 합니다.

![](examining-the-details-and-delete-methods/_static/image2.png)

## <a name="next-steps"></a>다음 단계

작성 하 고 웹 응용 프로그램을 테스트 후 다른 사람이 인터넷을 통해 사용 하도록 사용할 수 있도록 하려면 다음 단계가입니다. 이렇게 하려면 웹 호스팅 공급자를 배포 해야 합니다. Microsoft에서 제공 하는 최대 10 개의 웹 사이트의 무료 웹 호스팅는 [Windows Azure 평가판 계정 무료](https://www.windowsazure.com/en-us/pricing/free-trial/?WT.mc_id=A443DD604)합니다. 다음 내 자습서를 따라 보시기 [Windows Azure 웹 사이트 멤버 자격, OAuth, SQL 데이터베이스와 Secure ASP.NET MVC 응용 프로그램 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)합니다. 뛰어난 자습서가 Tom Dykstra 중간 수준 [ASP.NET MVC 응용 프로그램에 대 한 Entity Framework 데이터 모델을 만드는](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다. [Stackoverflow](http://stackoverflow.com/help) 및 [ASP.NET MVC 포럼](https://forums.asp.net/1146.aspx) 질문을 하는 좋은 배치 됩니다. 에 따라 [me](https://twitter.com/RickAndMSFT) 에서 twitter 때문 내 최신 자습서에 대 한 업데이트를 가져올 수 있습니다.

피드백을 보내 주십시오.

- [Rick Anderson](https://blogs.msdn.com/rickAndy) twitter:[@RickAndMSFT](https://twitter.com/RickAndMSFT)  
- [Scott Hanselman](http://www.hanselman.com/blog/) twitter:[@shanselman](https://twitter.com/shanselman)

>[!div class="step-by-step"]
[이전](adding-validation-to-the-model.md)
