---
uid: mvc/overview/getting-started/database-first-development/creating-the-web-application
title: '자습서: 만들기는 웹 응용 프로그램 및 데이터 모델 EF에 대 한 ASP.NET MVC를 사용 하 여 첫 번째 데이터베이스'
description: 이 문서에서는 웹 응용 프로그램을 만들고 데이터베이스 테이블 기반 데이터 모델 생성에 중점을 둡니다.
author: Rick-Anderson
ms.author: riande
ms.date: 01/23/2019
ms.topic: tutorial
ms.assetid: bc8f2bd5-ff57-4dcd-8418-a5bd517d8953
msc.legacyurl: /mvc/overview/getting-started/database-first-development/creating-the-web-application
msc.type: authoredcontent
ms.openlocfilehash: 095d355866c9ab8fba3759f3e05e2a521992f3d6
ms.sourcegitcommit: d5223cf6a2cf80b4f5dc54169b0e376d493d2d3a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54889771"
---
# <a name="tutorial-create-the-the-web-application-and-data-models-for-ef-database-first-with-aspnet-mvc"></a>자습서: 만들기는 웹 응용 프로그램 및 데이터 모델 EF에 대 한 ASP.NET MVC를 사용 하 여 첫 번째 데이터베이스

 MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여, 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다. 이 자습서 시리즈에서는 자동으로 표시, 편집, 만들기, 사용자를 사용 하는 코드를 생성 하 고 데이터베이스 테이블에 있는 데이터를 삭제 하는 방법을 보여 줍니다. 생성된 된 코드는 데이터베이스 테이블의 열에 해당합니다.

이 문서에서는 웹 응용 프로그램을 만들고 데이터베이스 테이블 기반 데이터 모델 생성에 중점을 둡니다.

이 자습서에서는 다음을 수행했습니다.

> [!div class="checklist"]
> * ASP.NET 웹앱 만들기
> * 모델 생성

## <a name="prerequisites"></a>전제 조건

* [Entity Framework 6 Database First MVC 5를 사용 하 여 시작](setting-up-database.md)

## <a name="create-an-aspnet-web-app"></a>ASP.NET 웹앱 만들기

새 솔루션 또는 데이터베이스 프로젝트와 동일한 솔루션에서 Visual Studio에서 새 프로젝트 만들기 및 선택 합니다 **ASP.NET 웹 응용 프로그램** 템플릿. 프로젝트 이름을 **ContosoSite**합니다.

![프로젝트 만들기](creating-the-web-application/_static/image1.png)

**확인**을 클릭합니다.

새 ASP.NET 프로젝트 창에서 선택 합니다 **MVC** 템플릿. 지울 수는 **클라우드에서 호스트** 나중에 응용 프로그램을 클라우드에 배포 하기 때문에 지금은 옵션입니다. 클릭 **확인** 응용 프로그램을 만들려고 합니다.

프로젝트 기본 파일 및 폴더를 사용 하 여 만들어집니다.

이 자습서에서는 Entity Framework 6을 사용 합니다. NuGet 패키지 관리 창을 통해 프로젝트에서 Entity Framework의 버전을 다시 확인 수 있습니다. 필요한 경우 Entity Framework의 버전을 업데이트 합니다.

![버전 표시](creating-the-web-application/_static/image3.png)

## <a name="generate-the-models"></a>모델 생성

이제 데이터베이스 테이블에서 Entity Framework 모델을 만듭니다. 이러한 모델은 데이터를 사용 하 여 작업을 사용 하는 클래스입니다. 각 모델 미러 데이터베이스의 테이블 및 테이블의 열에 해당 하는 속성을 포함 합니다.

마우스 오른쪽 단추로 클릭 합니다 **모델** 폴더를 선택한 **추가** 하 고 **새 항목**합니다.

새 항목 추가 창에서 선택 **데이터** 왼쪽된 창에서 및 **ADO.NET Entity Data Model** 가운데 창에 있는 옵션에서입니다. 새 모델 파일의 이름을 **ContosoModel**합니다.

**추가**를 클릭합니다.

엔터티 데이터 모델 마법사에서 선택 **데이터베이스의 EF 디자이너**합니다.

**다음**을 클릭합니다.

개발 환경 내에 정의 된 데이터베이스 연결에 있는 경우 미리 선택이 연결 중 하나가 표시 될 수 있습니다. 그러나이 자습서의 첫 번째 부분에서 만든 데이터베이스에 새 연결을 만들려고 할 수도 있습니다. 클릭 합니다 **새 연결** 단추입니다.

연결 속성 창에서 데이터베이스에 만들어진 로컬 서버의 이름을 제공 합니다 (이 예제의 **(localdb) \Projects13**). 서버 이름을 입력 한 후 사용 가능한 데이터베이스에서의 ContosoUniversityData를 선택 합니다.

![연결 속성 설정](creating-the-web-application/_static/image8.png)

**확인**을 클릭합니다.

올바른 연결 속성 표시 됩니다. Web.Config 파일에서 연결에 대 한 기본 이름을 사용할 수 있습니다.

**다음**을 클릭합니다.

Entity Framework의 최신 버전을 선택 합니다.

**다음**을 클릭합니다.

선택 **테이블** 세 테이블 모두에 대 한 모델을 생성 하도록 합니다.

**마침**을 클릭합니다.

보안 경고를 받은 경우 선택할 **확인** 템플릿 실행을 계속 합니다.

데이터베이스 테이블에서 생성 되어 및 속성 및 테이블 간의 관계를 보여 주는 다이어그램 표시 됩니다.

![모델의 다이어그램](creating-the-web-application/_static/image11.png)

Models 폴더에는 이제 데이터베이스에서 생성 된 모델에 관련 된 많은 새 파일이 포함 됩니다.

**ContosoModel.Context.cs** 파일에서 파생 된 클래스를 포함 합니다 **DbContext** 클래스 및 데이터베이스 테이블에 해당 하는 각 모델 클래스에 대 한 속성을 제공 합니다. 합니다 **Course.cs**, **Enrollment.cs**, 및 **Student.cs** 파일 데이터베이스 테이블을 나타내는 모델 클래스를 포함 합니다. 스 캐 폴딩을 사용 하는 경우 컨텍스트 클래스와 모델 클래스를 사용 합니다.

이 자습서를 진행 하기 전에 프로젝트를 빌드하십시오. 다음 섹션에서는 섹션에는 프로젝트가 빌드되지 않은 경우 작동 하지 것입니다 하지만 데이터 모델을 기반으로 하는 코드를 생성 합니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음을 수행했습니다.

> [!div class="checklist"]
> * ASP.NET 웹 앱을 생성합니다.
> * 모델 생성

만드는 방법에 알아보려면 다음 문서는 고급 데이터 모델을 기반으로 하는 코드를 생성 합니다.
> [!div class="nextstepaction"]
> [뷰 생성](generating-views.md)