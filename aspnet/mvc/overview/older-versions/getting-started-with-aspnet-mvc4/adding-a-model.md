---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
title: 모델 추가 | Microsoft Docs
author: Rick-Anderson
description: '참고: 업데이트 된이이 자습서는 ASP.NET MVC 5 및 Visual Studio 2013을 사용 하는 있습니다. 것이 더 안전 하 고 더 간단 하 게 따르고 데모 중...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 53db72da-e0b9-44d9-b60b-6e6988c00b28
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: 5308d2d1d11f954db8a4502adb42223f69e0c675
ms.sourcegitcommit: 7b4e3936feacb1a8fcea7802aab3e2ea9c8af5b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48578512"
---
<a name="adding-a-model"></a>모델 추가
====================
[Rick Anderson]((https://twitter.com/RickAndMSFT))

> > [!NOTE]
> > 이 자습서는 업데이트 된 버전을 사용할 수 [여기](../../getting-started/introduction/getting-started.md) 는 ASP.NET MVC 5 및 Visual Studio 2013을 사용 합니다. 보다 안전 하 고 더 간단 하 게 수행 되며 더 많은 기능을 보여 줍니다.


이 섹션에서는 데이터베이스에서 동영상을 관리 하기 위한 일부 클래스를 추가 합니다. 이러한 클래스는 &quot;모델&quot; ASP.NET MVC 응용 프로그램의 일부입니다.

라고 하는.NET Framework 데이터 액세스 기술 사용 합니다 [Entity Framework](https://msdn.microsoft.com/library/bb399572(VS.110).aspx) 를 정의한 다음 이러한 모델 클래스를 사용 합니다. 라고 하는 개발 패러다임을 Entity Framework (EF 라고도 함) 지원 *Code First*합니다. 먼저 코드를 사용 하면 간단한 클래스를 작성 하 여 모델 개체를 만들 수 있습니다. (이러한 이라고 POCO 클래스에서 &quot;plain old CLR object.&quot;) 그런 다음이 매우 명확 하 고 신속한 개발 워크플로 통해 클래스를에서 즉석에서 생성 된 데이터베이스를 사용할 수 있습니다.

## <a name="adding-model-classes"></a>모델 클래스 추가

**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 *모델* 폴더를 선택 **추가**를 선택한 후 **클래스**합니다.

![](adding-a-model/_static/image1.png)

입력 된 *클래스* 이름 &quot;영화&quot;합니다.

다음 5 개의 속성을 추가 합니다 `Movie` 클래스:

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

사용 된 `Movie` 데이터베이스에서 동영상을 나타내는 클래스입니다. 각 인스턴스는 `Movie` 개체의 각 속성과 데이터베이스 테이블 내의 행에 해당 합니다 `Movie` 클래스는 테이블의 열에 매핑됩니다.

동일한 파일에 다음 추가 `MovieDBContext` 클래스:

[!code-csharp[Main](adding-a-model/samples/sample2.cs)]

`MovieDBContext` 페치, 저장 및 업데이트를 처리 하는 Entity Framework 영화 데이터베이스 컨텍스트 클래스를 나타냅니다 `Movie` 클래스 인스턴스의 데이터베이스에 있습니다. 합니다 `MovieDBContext` 에서 파생 되는 `DbContext` 기본 Entity Framework에서 제공 하는 클래스입니다.

참조할 수 있도록 `DbContext` 하 고 `DbSet`, 다음을 추가 해야 `using` 파일의 맨 위에 있는 문을:

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

전체 *Movie.cs* 파일은 다음과 같습니다. (여러이 아닌 문을 사용 하 여 필요한 제거 되었습니다.)

[!code-csharp[Main](adding-a-model/samples/sample4.cs)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a>연결 문자열 만들기 및 SQL Server LocalDB 사용

합니다 `MovieDBContext` 데이터베이스에 연결 및 매핑 작업을 처리 하는 클래스를 만든 `Movie` 데이터베이스 레코드에는 개체입니다. 할 질문 중 하나는 그러나에서 연결할 데이터베이스를 지정 하는 방법입니다. 연결 정보를 추가 하 여 로그인 할 수 있습니다 합니다 *Web.config* 응용 프로그램의 파일입니다.

응용 프로그램 루트를 엽니다 *Web.config* 파일입니다. (하지 합니다 *Web.config* 파일을 *뷰* 폴더입니다.) 엽니다는 *Web.config* 빨간색 윤곽선이 있는 파일입니다.

![](adding-a-model/_static/image2.png)

다음 연결 문자열을 추가 합니다 `<connectionStrings>` 요소에는 *Web.config* 파일입니다.

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

다음 예제에서는 부분 합니다 *Web.config* 추가 되는 새 연결 문자열을 사용 하 여 파일:

[!code-xml[Main](adding-a-model/samples/sample6.xml?highlight=6-9)]

코드 및 XML이 적은 양의 나타내고 영화 데이터를 데이터베이스에 저장 하기 위해 작성 하는 데 필요한 모든 경우

다음으로 빌드할 새 `MoviesController` 영화 데이터를 표시 하 고 새 동영상 목록을 만들 수 있도록 하는 데 사용할 수 있는 클래스입니다.

> [!div class="step-by-step"]
> [이전](adding-a-view.md)
> [다음](accessing-your-models-data-from-a-controller.md)
