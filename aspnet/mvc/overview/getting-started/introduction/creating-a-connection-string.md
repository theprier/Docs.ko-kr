---
uid: mvc/overview/getting-started/introduction/creating-a-connection-string
title: 연결 문자열 만들기 및 SQL Server LocalDB 사용 | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: aspnetcontent
ms.date: 10/17/2013
ms.assetid: 6127804d-c1a9-414d-8429-7f3dd0f56e97
msc.legacyurl: /mvc/overview/getting-started/introduction/creating-a-connection-string
msc.type: authoredcontent
ms.openlocfilehash: 8c8db3fc121b2ff263ab033404211e167e19cd71
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37820245"
---
<a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a>연결 문자열 만들기 및 SQL Server LocalDB 사용
====================
[Rick Anderson](https://github.com/Rick-Anderson)

[!INCLUDE [Tutorial Note](sample/code-location.md)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a>연결 문자열 만들기 및 SQL Server LocalDB 사용

합니다 `MovieDBContext` 데이터베이스에 연결 및 매핑 작업을 처리 하는 클래스를 만든 `Movie` 데이터베이스 레코드에는 개체입니다. 할 질문 중 하나는 그러나에서 연결할 데이터베이스를 지정 하는 방법입니다. 사용할 데이터베이스를 지정할 필요는 없습니다, Entity Framework는 기본적으로 기본 [LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb)합니다. 이 섹션에서는 명시적으로 추가 연결 문자열을 *Web.config* 응용 프로그램의 파일입니다.

## <a name="sql-server-express-localdb"></a>SQL Server Express LocalDB

[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) 는 SQL Server Express 데이터베이스 엔진의 요청 시 시작 하 고 사용자 모드에서 실행 되는 경량 버전입니다. LocalDB 데이터베이스를 사용 하 여 작업할 수 있도록 하는 SQL Server Express의 특수 실행 모드에서 실행 *.mdf* 파일입니다. 일반적으로, LocalDB 데이터베이스 파일에 보관 되는 *앱\_데이터* 웹 프로젝트의 폴더입니다.

SQL Server Express는 프로덕션 웹 응용 프로그램에서 사용 하 여에 대 한 권장 되지 않습니다. LocalDB 특히 해서는 안 웹 응용 프로그램을 사용 하 여 프로덕션에 있으므로 IIS를 사용 하 여 작동 하도록 설계 되지는 않았습니다. 그러나 LocalDB 데이터베이스를 SQL Server 또는 SQL Azure 쉽게 마이그레이션할 수 있습니다.

Visual Studio 2017에서 Visual Studio를 사용 하 여 기본적으로 LocalDB는 설치 됩니다.

기본적으로 Entity Framework 개체 컨텍스트 클래스와 동일 하 게 명명 된 연결 문자열을 찾습니다 (`MovieDBContext` 이 프로젝트에 대 한). 자세한 내용은 참조 [ASP.NET 웹 응용 프로그램에 대 한 SQL Server 연결 문자열](https://msdn.microsoft.com/library/jj653752.aspx)합니다.

응용 프로그램 루트를 엽니다 *Web.config* 파일 아래에 표시 합니다. (하지 합니다 *Web.config* 파일을 *뷰* 폴더입니다.)

![](creating-a-connection-string/_static/image1.png)

찾기는 `<connectionStrings>` 요소:

![](creating-a-connection-string/_static/image2.png)

다음 연결 문자열을 추가 합니다 `<connectionStrings>` 요소에는 *Web.config* 파일입니다.

[!code-xml[Main](creating-a-connection-string/samples/sample1.xml)]

다음 예제에서는 부분 합니다 *Web.config* 추가 되는 새 연결 문자열을 사용 하 여 파일:

[!code-xml[Main](creating-a-connection-string/samples/sample2.xml)]

두 연결 문자열은 매우 유사 합니다. 첫 번째 연결 문자열 이름은 `DefaultConnection` 멤버 자격 데이터베이스가 응용 프로그램에 액세스할 수 있는 사용자를 제어 하는 데 사용 됩니다. 추가한 다음 연결 문자열을 명명 된 LocalDB 데이터베이스를 지정 합니다. *Movie.mdf* 에 *앱\_데이터* 폴더입니다. 에서는 멤버 자격 데이터베이스를 사용 하 여 멤버 자격, 인증 및 보안에 대 한 자세한 내용은이 자습서에서는 won't, 내 자습서를 참조 하세요 [인증 및 SQL DB를 사용 하 여 ASP.NET MVC 앱을 만들고 Azure App Service에 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)합니다.

연결 문자열의 이름을의 이름과 일치 해야 합니다 [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) 클래스입니다.

[!code-csharp[Main](creating-a-connection-string/samples/sample3.cs?highlight=15)]

추가할 필요가 실제로 `MovieDBContext` 연결 문자열입니다. 연결 문자열을 지정 하지 않으면, Entity Framework 데이터베이스가 만들어집니다. LocalDB 사용자 디렉터리의 정규화 된 이름에는 [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) 클래스 (이 경우 `MvcMovie.Models.MovieDBContext`). 이름은 데이터베이스 원하는 붙어 있다면는 *합니다. MDF* 접미사. 예를 들어 데이터베이스 이름이 했습니다 *MyFilms.mdf*합니다.

다음으로 빌드할 새 `MoviesController` 영화 데이터를 표시 하 고 새 동영상 목록을 만들 수 있도록 하는 데 사용할 수 있는 클래스입니다.

> [!div class="step-by-step"]
> [이전](adding-a-model.md)
> [다음](accessing-your-models-data-from-a-controller.md)
