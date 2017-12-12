---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-3
title: "Code First 마이그레이션을 사용 하 여 데이터베이스의 초기값 | Microsoft Docs"
author: MikeWasson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/16/2014
ms.topic: article
ms.assetid: 76e2013a-65b7-488c-834d-9448ecea378e
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-3
msc.type: authoredcontent
ms.openlocfilehash: df75a69644033cc76fee86b5a9692ab65beb4d01
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="use-code-first-migrations-to-seed-the-database"></a>Code First 마이그레이션을 사용 하 여 데이터베이스의 초기값
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트를 다운로드 합니다.](https://github.com/MikeWasson/BookService)

이 섹션을 사용 하 여 [Code First 마이그레이션을](https://msdn.microsoft.com/en-us/data/jj591621) 를 테스트 데이터로 데이터베이스를 시드하는 EF에 있습니다.

**도구** 메뉴 선택 **라이브러리 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다. 패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

[!code-console[Main](part-3/samples/sample1.cmd)]

이 명령은 마이그레이션 프로젝트에 라는 폴더를 더한 Migrations 폴더에서 Configuration.cs 라는 코드 파일을 추가 합니다.

![](part-3/_static/image1.png)

Configuration.cs 파일을 엽니다. 다음 추가 **를 사용 하 여** 문.

[!code-csharp[Main](part-3/samples/sample2.cs)]

다음 코드를 다음 추가 **Configuration.Seed** 메서드:

[!code-csharp[Main](part-3/samples/sample3.cs)]

패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

[!code-console[Main](part-3/samples/sample4.cmd)]

첫 번째 명령은 데이터베이스가 생성 하는 코드를 생성 하 고 두 번째 명령은 해당 코드를 실행 합니다. 데이터베이스를 로컬로 사용 하 여 만들어집니다 [LocalDB](https://msdn.microsoft.com/en-us/library/hh510202.aspx)합니다.

![](part-3/_static/image2.png)

## <a name="explore-the-api-optional"></a>(선택 사항) API를 탐색 합니다.

F5 키를 눌러 디버그 모드에서 응용 프로그램을 실행 합니다. Visual Studio는 IIS Express를 시작 하 고 웹 응용 프로그램을 실행 합니다. 그런 다음 visual Studio는 브라우저를 시작 하 고 응용 프로그램의 홈 페이지를 엽니다.

Visual Studio 웹 프로젝트를 실행 하는 경우 포트 번호를 할당 합니다. 아래 이미지에 포트 번호가 50524입니다. 응용 프로그램을 실행 하는 경우에 다른 포트 번호를 표시 됩니다.

![](part-3/_static/image3.png)

홈 페이지는 ASP.NET MVC를 사용 하 여 구현 됩니다. 페이지 맨 위에 있는 링크는 "API" 있습니다. 이 링크는 web API에 대 한 자동 생성 된 도움말 페이지를 가져옵니다. (이 도움말 페이지 생성 되는 방식 및 추가 하는 방법을 직접 설명서 페이지를 참조 [ASP.NET Web API에 대 한 도움말 페이지 만들기](../../getting-started-with-aspnet-web-api/creating-api-help-pages.md).) 요청 및 응답 형식을 비롯 한 API에 대 한 자세한 내용을 보려면 페이지 링크 제공 도움말 클릭할 수 있습니다.

![](part-3/_static/image4.png)

API를 통해 데이터베이스에 대해 CRUD 작업 합니다. 다음은 API에 대 한 요약입니다.

| 만든 이 |  |
| --- | -- |
| Api/작성자 가져오기 | 모든 작성자를 가져옵니다. |
| GET api/작성자 / {id} | 만든 id 가져오기 |
| POST/api/작성자 | 새로운 저자를 만듭니다. |
| PUT /api/작성자 / {id} | 기존 author를 업데이트 합니다. |
| 삭제 /api/작성자 / {id} | 제작자를 삭제 합니다. |

| 설명서 |  |
| --- | -- |
| /Api/books 가져오기 | 모든 책을 가져옵니다. |
| 가져오기 /api/설명서 / {id} | 책 id 가져오기 |
| 게시/api/설명서 | 새 책을 만듭니다. |
| PUT /api/설명서 / {id} | 기존 책을 업데이트 합니다. |
| 삭제 /api/설명서 / {id} | 책을 삭제 합니다. |

## <a name="view-the-database-optional"></a>(선택 사항) 데이터베이스 보기

Update-database 명령을 실행할 때 EF에서 데이터베이스를 만든 호출의 `Seed` 메서드. EF 사용 하 여 응용 프로그램을 로컬로 실행할 때 [LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx)합니다. Visual Studio에서 데이터베이스를 볼 수 있습니다. **보기** 메뉴 선택 **SQL Server 개체 탐색기**합니다.

![](part-3/_static/image5.png)

에 **서버에 연결** 대화에는 **서버 이름** 편집 상자, "(localdb) \v11.0"를 입력 합니다. 둡니다는 **인증** "Windows 인증"으로 옵션입니다. **연결**을 클릭합니다.

![](part-3/_static/image6.png)

Visual Studio는 LocalDB에 연결 하 고 SQL Server 개체 탐색기 창에서 기존 데이터베이스를 보여 줍니다. EF 만든 테이블을 보려면 노드를 확장할 수 있습니다.

![](part-3/_static/image7.png)

데이터를 보려면 테이블을 마우스 오른쪽 단추로 클릭 하 고 선택 **데이터 보기**합니다.

![](part-3/_static/image8.png)

다음 스크린 샷에서 설명서 테이블에 대 한 결과 보여 줍니다. EF는 데이터베이스 시드 데이터로 채워진 Authors 테이블에 외래 키를 포함 하는 테이블에 유의 하십시오.

![](part-3/_static/image9.png)

>[!div class="step-by-step"]
[이전](part-2.md)
[다음](part-4.md)
