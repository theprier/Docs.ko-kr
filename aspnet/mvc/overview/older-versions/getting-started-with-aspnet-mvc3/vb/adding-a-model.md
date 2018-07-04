---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-model
title: 모델 (VB) 추가 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 인를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 설명 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2011
ms.topic: article
ms.assetid: b3aa7720-5c78-4ca2-baef-9a52234fb7ce
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: fb5620921aa2575e7336661b61bb6d1f4afa4517
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37389100"
---
<a name="adding-a-model-vb"></a>모델 (VB) 추가
====================
[Rick Anderson](https://github.com/Rick-Anderson)

> 이 자습서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, Microsoft Visual Studio의 무료 버전인를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 설명 합니다. 시작 하기 전에 아래에 나열 된 필수 구성 요소를 설치한 다음 있는지 확인 합니다. 다음 링크를 클릭 하 여 이들 모두를 설치할 수 있습니다: [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)합니다. 또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.
> 
> - [Visual Studio Web Developer Express SP1 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 도구 업데이트](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)
> 
> Visual Studio 2010 Visual Web Developer 2010 대신를 사용 하는 경우 다음 링크를 클릭 하 여 필수 구성 요소를 설치 합니다. [Visual Studio 2010 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)합니다.
> 
> VB.NET 소스 코드를 사용 하 여 Visual Web Developer 프로젝트는 다음이 항목과 함께 사용할 수 있습니다. [VB.NET 버전](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)합니다. 원하는 경우 C#으로 전환 합니다 [C# 버전](../cs/adding-a-model.md) 이 자습서의 합니다.


## <a name="adding-a-model"></a>모델 추가

이 섹션에서는 데이터베이스에서 동영상을 관리 하기 위한 일부 클래스를 추가 합니다. 이러한 클래스는 ASP.NET MVC 응용 프로그램에는 "모델" 포함 됩니다.

이러한 모델 클래스를 정의 및 작업에.NET Framework 데이터 액세스 기술을 통해 Entity Framework를 사용 합니다. 라고 하는 개발 패러다임을 Entity Framework (EF 라고도 함) 지원 *Code First*합니다. 먼저 코드를 사용 하면 간단한 클래스를 작성 하 여 모델 개체를 만들 수 있습니다. (이 경우 "plain old CLR object. POCO 클래스에도 함) 그런 다음이 매우 명확 하 고 신속한 개발 워크플로 통해 클래스를에서 즉석에서 생성 된 데이터베이스를 사용할 수 있습니다.

## <a name="adding-model-classes"></a>모델 클래스 추가

**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 *모델* 폴더를 선택 **추가**를 선택한 후 **클래스**합니다.

![](adding-a-model/_static/image1.png)

"영화" 클래스를 이름을 지정 합니다.

다음 5 개의 속성을 추가 합니다 `Movie` 클래스:

[!code-vb[Main](adding-a-model/samples/sample1.vb)]

사용 된 `Movie` 데이터베이스에서 동영상을 나타내는 클래스입니다. 각 인스턴스는 `Movie` 개체의 각 속성과 데이터베이스 테이블 내의 행에 해당 합니다 `Movie` 클래스는 테이블의 열에 매핑됩니다.

동일한 파일에 다음 추가 `MovieDBContext` 클래스:

[!code-vb[Main](adding-a-model/samples/sample2.vb)]

`MovieDBContext` 페치, 저장 및 업데이트를 처리 하는 Entity Framework 영화 데이터베이스 컨텍스트 클래스를 나타냅니다 `Movie` 클래스 인스턴스의 데이터베이스에 있습니다. 합니다 `MovieDBContext` 에서 파생 되는 `DbContext` 기본 Entity Framework에서 제공 하는 클래스입니다. 에 대 한 자세한 내용은 `DbContext` 하 고 `DbSet`를 참조 하세요 [Entity Framework에 대 한 생산성 향상](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0).

참조할 수 있도록 `DbContext` 하 고 `DbSet`, 다음을 추가 해야 `imports` 파일의 맨 위에 있는 문을:

[!code-vb[Main](adding-a-model/samples/sample3.vb)]

전체 *Movie.vb* 파일은 다음과 같습니다.

[!code-vb[Main](adding-a-model/samples/sample4.vb)]

## <a name="creating-a-connection-string-and-working-with-sql-server-compact"></a>연결 문자열 만들기 및 SQL Server Compact를 사용 하 여 작업

합니다 `MovieDBContext` 데이터베이스에 연결 및 매핑 작업을 처리 하는 클래스를 만든 `Movie` 데이터베이스 레코드에는 개체입니다. 할 질문 중 하나는 그러나에서 연결할 데이터베이스를 지정 하는 방법입니다. 연결 정보를 추가 하 여 로그인 할 수 있습니다 합니다 *Web.config* 응용 프로그램의 파일입니다.

응용 프로그램 루트를 엽니다 *Web.config* 파일입니다. (하지 합니다 *Web.config* 파일을 *뷰* 폴더입니다.) 아래 이미지는 둘 다 표시 *Web.config* 파일; 열기를 *Web.config* 빨간색 원이 표시 된 파일입니다.

![](adding-a-model/_static/image2.png)

## 

다음 연결 문자열을 추가 합니다 `<connectionStrings>` 요소에는 *Web.config* 파일입니다.

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

다음 예제에서는 부분 합니다 *Web.config* 추가 되는 새 연결 문자열을 사용 하 여 파일:

[!code-xml[Main](adding-a-model/samples/sample6.xml)]

코드 및 XML이 적은 양의 나타내고 영화 데이터를 데이터베이스에 저장 하기 위해 작성 하는 데 필요한 모든 경우

다음으로 빌드할 새 `MoviesController` 영화 데이터를 표시 하 고 새 동영상 목록을 만들 수 있도록 하는 데 사용할 수 있는 클래스입니다.

> [!div class="step-by-step"]
> [이전](adding-a-view.md)
> [다음](accessing-your-models-data-from-a-controller.md)
