---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
title: 모델 추가 | Microsoft Docs
author: Rick-Anderson
description: 참고:이 자습서의 업데이트 된 버전은 ASP.NET MVC 5 및 Visual Studio 2013을 사용 하는 있습니다. 것이 더 안전 하 고 진행할 데모를 단순...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/28/2012
ms.topic: article
ms.assetid: 53db72da-e0b9-44d9-b60b-6e6988c00b28
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: 562a06e22aad62b6982aca3316a2dfe18a6eba2e
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30871963"
---
<a name="adding-a-model"></a>모델 추가
====================
으로 [Rick Anderson](https://github.com/Rick-Anderson)

> > [!NOTE]
> > 이 자습서의 업데이트 된 버전은 사용할 수 있는 [여기](../../getting-started/introduction/getting-started.md) ASP.NET MVC 5 및 Visual Studio 2013을 사용 하 합니다. 더 안전 하 고 따라 하기 쉽고 이며 더 많은 기능을 보여 줍니다.


이 섹션에서는 데이터베이스에서 영화를 관리 하기 위한 몇 가지 클래스를 추가 합니다. 이러한 클래스 됩니다는 &quot;모델&quot; ASP.NET MVC 응용 프로그램의 일부입니다.

라고 하는.NET Framework 데이터 액세스 기술 사용의 [Entity Framework](https://msdn.microsoft.com/library/bb399572(VS.110).aspx) 정의 하 고 이러한 모델 클래스를 사용 합니다. Entity Framework (EF 라고도 함)에서 지 원하는 개발 패러다임 호출 *Code First*합니다. 먼저 코드에서는 간단한 클래스를 작성 하 여 모델 개체를 만들 수 있습니다. (이러한 라 하 고 POCO 클래스에서 &quot;old CLR 개체입니다.&quot;) 다음 클래스에서는 매우 명확 하 고 신속 하 게 개발 워크플로 매핑함으로써 즉석에서 생성 된 데이터베이스를 사용할 수 있습니다.

## <a name="adding-model-classes"></a>모델 클래스를 추가합니다.

**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 *모델* 폴더를 **추가**를 선택한 후 **클래스**합니다.

![](adding-a-model/_static/image1.png)

입력은 *클래스* 이름 &quot;영화&quot;합니다.

다음 5 개의 속성을 추가 `Movie` 클래스:

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

에서는 `Movie` 를 데이터베이스에서 영화를 나타내는 클래스입니다. 각 인스턴스는 `Movie` 개체는 데이터베이스 테이블과의 각 속성에 있는 행에 해당 하는 `Movie` 클래스는 테이블의 열에 매핑됩니다.

같은 파일에 다음 추가 `MovieDBContext` 클래스:

[!code-csharp[Main](adding-a-model/samples/sample2.cs)]

`MovieDBContext` 클래스 인출 저장 하 고 업데이트를 처리 하는 Entity Framework 영화 데이터베이스 컨텍스트를 나타냅니다. `Movie` 클래스 인스턴스는 데이터베이스에 있습니다. `MovieDBContext` 에서 파생 되는 `DbContext` 기본 클래스는 Entity Framework에서 제공 합니다.

참조할 수 있도록 `DbContext` 및 `DbSet`, 다음 코드를 추가 해야 할 `using` 문을 파일의 맨:

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

전체 *Movie.cs* 파일은 다음과 같습니다. (여러 되지 않는 문을 사용 하 여 필요한 제거 되었습니다.)

[!code-csharp[Main](adding-a-model/samples/sample4.cs)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a>연결 문자열 만들기 및 SQL Server LocalDB 사용

`MovieDBContext` 만든 클래스 매핑 및 데이터베이스에 연결 하는 작업을 처리 `Movie` 데이터베이스 레코드에는 개체입니다. 그러나 인지 궁금할 질문 중 하나는에 연결 하는 데이터베이스를 지정 하는 방법을입니다. 연결 정보를 추가 하 여 작업입니다는 *Web.config* 응용 프로그램의 파일입니다.

응용 프로그램 루트를 열고 *Web.config* 파일입니다. (하지는 *Web.config* 파일에 *뷰* 폴더입니다.) 열기는 *Web.config* 빨간색으로 윤곽선 처리 파일.

![](adding-a-model/_static/image2.png)

다음 연결 문자열을 추가할는 `<connectionStrings>` 요소에는 *Web.config* 파일입니다.

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

다음 예제에서는의 일부는 *Web.config* 파일을 추가 하는 새 연결 문자열:

[!code-xml[Main](adding-a-model/samples/sample6.xml?highlight=6-9)]

이 적은 양의 코드 및 XML을 나타내고 동영상 데이터는 데이터베이스에 저장 하기 위해 작성 해야 할 모든 항목입니다.

다음으로 빌드합니다.이 새 `MoviesController` 동영상 데이터를 표시 하 고 사용자가 새 동영상 목록을 만들 수 있도록 허용 하는 데 사용할 수 있는 클래스입니다.

> [!div class="step-by-step"]
> [이전](adding-a-view.md)
> [다음](accessing-your-models-data-from-a-controller.md)
