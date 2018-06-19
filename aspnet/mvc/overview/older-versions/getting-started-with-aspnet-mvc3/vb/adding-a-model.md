---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-model
title: 모델 (VB) 추가 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 즉를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 구축 하는 기초 설명...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2011
ms.topic: article
ms.assetid: b3aa7720-5c78-4ca2-baef-9a52234fb7ce
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: e9a271c64347b4004d5cc5d9d91085c4e642e95d
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30868141"
---
<a name="adding-a-model-vb"></a>모델 (VB)를 추가합니다.
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
> 이 항목에 수반 VB.NET 소스 코드를 사용 하 여 Visual Web Developer 프로젝트 ´ ù. [VB.NET 버전을 다운로드](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)합니다. 원하는 경우 C#으로 전환 된 [C# 버전](../cs/adding-a-model.md) 이 자습서의 합니다.


## <a name="adding-a-model"></a>모델 추가

이 섹션에서는 데이터베이스에서 영화를 관리 하기 위한 몇 가지 클래스를 추가 합니다. 이러한 클래스는 ASP.NET MVC 응용 프로그램의 "모델" 일부 됩니다.

정의 하 고 이러한 모델 클래스를 사용 하려면.NET Framework 데이터 액세스 기술을 통해 Entity Framework를 사용 합니다. Entity Framework (EF 라고도 함)에서 지 원하는 개발 패러다임 호출 *Code First*합니다. 먼저 코드에서는 간단한 클래스를 작성 하 여 모델 개체를 만들 수 있습니다. (이러한는 POCO 클래스에서 "일반 이전 CLR 개체" 라고도 함) 다음 클래스에서는 매우 명확 하 고 신속 하 게 개발 워크플로 매핑함으로써 즉석에서 생성 된 데이터베이스를 사용할 수 있습니다.

## <a name="adding-model-classes"></a>모델 클래스를 추가합니다.

**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 *모델* 폴더를 **추가**를 선택한 후 **클래스**합니다.

![](adding-a-model/_static/image1.png)

"영화" 클래스를 이름을 지정 합니다.

다음 5 개의 속성을 추가 `Movie` 클래스:

[!code-vb[Main](adding-a-model/samples/sample1.vb)]

에서는 `Movie` 를 데이터베이스에서 영화를 나타내는 클래스입니다. 각 인스턴스는 `Movie` 개체는 데이터베이스 테이블과의 각 속성에 있는 행에 해당 하는 `Movie` 클래스는 테이블의 열에 매핑됩니다.

같은 파일에 다음 추가 `MovieDBContext` 클래스:

[!code-vb[Main](adding-a-model/samples/sample2.vb)]

`MovieDBContext` 클래스 인출 저장 하 고 업데이트를 처리 하는 Entity Framework 영화 데이터베이스 컨텍스트를 나타냅니다. `Movie` 클래스 인스턴스는 데이터베이스에 있습니다. `MovieDBContext` 에서 파생 되는 `DbContext` 기본 클래스는 Entity Framework에서 제공 합니다. 에 대 한 자세한 내용은 `DbContext` 및 `DbSet`, 참조 [Entity Framework에 대 한 성능 향상 기능](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0)합니다.

참조할 수 있도록 `DbContext` 및 `DbSet`, 다음 코드를 추가 해야 할 `imports` 문을 파일의 맨:

[!code-vb[Main](adding-a-model/samples/sample3.vb)]

전체 *Movie.vb* 파일은 다음과 같습니다.

[!code-vb[Main](adding-a-model/samples/sample4.vb)]

## <a name="creating-a-connection-string-and-working-with-sql-server-compact"></a>연결 문자열 만들기 및 SQL Server Compact 작업

`MovieDBContext` 만든 클래스 매핑 및 데이터베이스에 연결 하는 작업을 처리 `Movie` 데이터베이스 레코드에는 개체입니다. 그러나 인지 궁금할 질문 중 하나는에 연결 하는 데이터베이스를 지정 하는 방법을입니다. 연결 정보를 추가 하 여 작업입니다는 *Web.config* 응용 프로그램의 파일입니다.

응용 프로그램 루트를 열고 *Web.config* 파일입니다. (하지는 *Web.config* 파일에 *뷰* 폴더입니다.) 다음 이미지는 둘 다 표시 *Web.config* 파일; 열기는 *Web.config* 빨간색에서 원이 표시 된 파일입니다.

![](adding-a-model/_static/image2.png)

## 

다음 연결 문자열을 추가할는 `<connectionStrings>` 요소에는 *Web.config* 파일입니다.

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

다음 예제에서는의 일부는 *Web.config* 파일을 추가 하는 새 연결 문자열:

[!code-xml[Main](adding-a-model/samples/sample6.xml)]

이 적은 양의 코드 및 XML을 나타내고 동영상 데이터는 데이터베이스에 저장 하기 위해 작성 해야 할 모든 항목입니다.

다음으로 빌드합니다.이 새 `MoviesController` 동영상 데이터를 표시 하 고 사용자가 새 동영상 목록을 만들 수 있도록 허용 하는 데 사용할 수 있는 클래스입니다.

> [!div class="step-by-step"]
> [이전](adding-a-view.md)
> [다음](accessing-your-models-data-from-a-controller.md)
