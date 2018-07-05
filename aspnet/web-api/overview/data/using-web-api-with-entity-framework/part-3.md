---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-3
title: Code First 마이그레이션을 사용 하 여 데이터베이스를 시드하려면 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/16/2014
ms.topic: article
ms.assetid: 76e2013a-65b7-488c-834d-9448ecea378e
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-3
msc.type: authoredcontent
ms.openlocfilehash: 0d753ea52c57af2cbffff9e1e8741bbe49bc6d7b
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37370528"
---
<a name="use-code-first-migrations-to-seed-the-database"></a>Code First 마이그레이션을 사용 하 여 데이터베이스를 시드합니다.
====================
[Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트 다운로드](https://github.com/MikeWasson/BookService)

이 섹션에서는 사용할지 [Code First 마이그레이션을](https://msdn.microsoft.com/data/jj591621) 테스트 데이터로 데이터베이스를 시드하려면 EF의 합니다.

**도구** 메뉴에서 **라이브러리 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다. 패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

[!code-console[Main](part-3/samples/sample1.cmd)]

이 명령은 프로젝트에 마이그레이션을 이라는 폴더와 마이그레이션 폴더에 Configuration.cs 라는 코드 파일을 추가 합니다.

![](part-3/_static/image1.png)

Configuration.cs 파일을 엽니다. 다음을 추가 합니다 **를 사용 하 여** 문입니다.

[!code-csharp[Main](part-3/samples/sample2.cs)]

다음 코드를 추가 합니다 **Configuration.Seed** 메서드:

[!code-csharp[Main](part-3/samples/sample3.cs)]

패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

[!code-console[Main](part-3/samples/sample4.cmd)]

첫 번째 명령은 데이터베이스를 만드는 코드를 생성 하 고 두 번째 명령은 해당 코드를 실행 합니다. 데이터베이스를 로컬로 사용 하 여 만들어집니다 [LocalDB](https://msdn.microsoft.com/library/hh510202.aspx)합니다.

![](part-3/_static/image2.png)

## <a name="explore-the-api-optional"></a>(선택 사항) API를 탐색 합니다.

F5 키를 눌러 디버그 모드에서 응용 프로그램을 실행 합니다. Visual Studio IIS Express를 시작 하 고 웹 앱을 실행 합니다. 그런 다음 visual Studio가 브라우저를 시작 하 고 앱의 홈 페이지를 엽니다.

Visual Studio 웹 프로젝트를 실행할 때 포트 번호를 할당 합니다. 아래 이미지에서 포트 번호가 50524입니다. 응용 프로그램을 실행 하는 경우 다른 포트 번호를 표시 됩니다.

![](part-3/_static/image3.png)

홈 페이지는 ASP.NET MVC를 사용 하 여 구현 됩니다. 페이지의 맨 위에 있는 "API" 이라는 링크가 있습니다. 이 링크는 web API에 대 한 자동 생성 된 도움말 페이지에 제공합니다. (이 도움말 페이지 생성 방법 및 고유한 설명서 페이지에 추가할 수 있습니다 하는 방법에 대해 알아보려면 [ASP.NET Web API에 대 한 도움말 페이지 만들기](../../getting-started-with-aspnet-web-api/creating-api-help-pages.md).) 페이지 링크를 요청 및 응답 형식을 비롯 한 API에 대 한 자세한 내용은 도움말을 클릭할 수 있습니다.

![](part-3/_static/image4.png)

API를 통해 데이터베이스에 대 한 CRUD 작업을 수 있습니다. 다음 API를 요약합니다.

| 만든 이 |  |
| --- | -- |
| Api/작성자 가져오기 | 모든 작성자를 가져옵니다. |
| GET api/작성자 / {id} | 작성자 id 가져오기 |
| POST/api/작성자 | 새 작성자를 만듭니다. |
| PUT/a p i/작성자 / {id} | 기존 author를 업데이트 합니다. |
| 삭제/a p i/작성자 / {id} | 작성자를 삭제 합니다. |

| 책 |  |
| --- | -- |
| /Api/books 가져오기 | 모든 책을 가져옵니다. |
| 가져오기/a p i/책 / {id} | 책 id 가져오기 |
| Api 설명서를 게시 합니다. | 새 책을 만듭니다. |
| PUT/a p i/책 / {id} | 기존 책을 업데이트 합니다. |
| 삭제/a p i/책 / {id} | 책을 삭제 합니다. |

## <a name="view-the-database-optional"></a>(선택 사항) 데이터베이스 보기

Update-database 명령을 실행할 때 EF에서 데이터베이스를 만든 호출을 `Seed` 메서드. EF가 사용 하는 응용 프로그램을 로컬로 실행 하면 [LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx)합니다. Visual Studio에서 데이터베이스를 볼 수 있습니다. **뷰** 메뉴에서 **SQL Server 개체 탐색기**합니다.

![](part-3/_static/image5.png)

에 **서버에 연결** 대화의 합니다 **서버 이름** 편집 상자에 "(localdb) \v11.0"를 입력 합니다. 유지 된 **인증** 옵션 "Windows 인증"으로 합니다. **연결**을 클릭합니다.

![](part-3/_static/image6.png)

Visual Studio는 LocalDB에 연결 하 고 SQL Server 개체 탐색기 창에서 기존 데이터베이스를 보여 줍니다. EF에서 만든 테이블을 보려면 노드를 확장할 수 있습니다.

![](part-3/_static/image7.png)

데이터를 보려면 테이블을 마우스 오른쪽 단추로 클릭 하 고 선택 **데이터 보기**합니다.

![](part-3/_static/image8.png)

다음 스크린 샷에서 책 테이블에 대 한 결과 보여 줍니다. EF 시드 데이터를 사용 하 여 데이터베이스를 채울 Authors 테이블에 외래 키를 포함 하는 테이블에 유의 하십시오.

![](part-3/_static/image9.png)

> [!div class="step-by-step"]
> [이전](part-2.md)
> [다음](part-4.md)
