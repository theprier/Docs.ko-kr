---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-the-production-web-application-to-use-the-production-database-cs
title: "프로덕션 데이터베이스 (C#)를 사용 하 여 프로덕션 웹 응용 프로그램 구성 | Microsoft Docs"
author: rick-anderson
description: "이전 자습서에서 설명 했 듯이 구성 정보를 개발 및 프로덕션 환경 간에 다도 드물지 않습니다. 이 es 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/23/2009
ms.topic: article
ms.assetid: 0177dabd-d888-449f-91b2-24190cf5e842
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-the-production-web-application-to-use-the-production-database-cs
msc.type: authoredcontent
ms.openlocfilehash: e99b74030104bf17d4d79cd7670cf903270fa51f
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="configuring-the-production-web-application-to-use-the-production-database-c"></a>프로덕션 데이터베이스 (C#)를 사용 하 여 프로덕션 웹 응용 프로그램 구성
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/E/6/F/E6FE3A1F-EE3A-4119-989A-33D1A9F6F6DD/ASPNET_Hosting_Tutorial_08_CS.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/C/3/9/C391A649-B357-4A7B-BAA4-48C96871FEA6/aspnet_tutorial08_DBConfig_cs.pdf)

> 이전 자습서에서 설명 했 듯이 구성 정보를 개발 및 프로덕션 환경 간에 다도 드물지 않습니다. 이 개발 및 프로덕션 환경 간에 데이터베이스 연결 문자열 다르게 데이터 기반 웹 응용 프로그램의 경우 특히 그렇습니다. 이 자습서에는 프로덕션 환경 보다 자세히 적절 한 연결 문자열을 포함 하도록 구성할 수 있는 방법을 탐색 합니다.


## <a name="introduction"></a>소개

데이터 기반 웹 응용 프로그램은 일반적으로 프로덕션 환경에서 되었을 때 보다 개발에 있을 때 다른 데이터베이스를 사용 합니다. 웹 호스트 공급자에 의해 호스팅되며 로컬로 개발 된 응용 프로그램의 경우 개발 데이터베이스 일반적으로 컴퓨터에 있는 개발자 s 동안 프로덕션 데이터베이스를 웹 호스팅 회사의 기관에서 데이터베이스 서버에서 호스팅됩니다. 데이터 기반 웹 응용 프로그램을 배포 하려면 개발 데이터베이스를 프로덕션 데이터베이스 서버에 복사 해야 합니다. 이전 자습서의이 단계를 수행 하는 방법을 찾았습니다.

웹 응용 프로그램에 정보를 사용 하는 *연결 문자열* 데이터베이스와 연결을 설정할 수 있습니다. 일반적으로에 저장 된 연결 문자열 `Web.config`, 데이터베이스 서버 이름, 데이터베이스, 보안 컨텍스트 및 기타 정보의 이름을 지정 합니다. 웹 응용 프로그램에서 사용 되는 데이터베이스 개발 또는 프로덕션 환경에서 웹 응용 프로그램의 실행 여부에 따라 달라, 연결 문자열은 두 환경 간에 달라 야 합니다.

구성 정보를 개발 및 프로덕션 환경 간에 다도 드물지 않습니다. *일반적인 구성 차이점 간의 개발 및 프로덕션* 자습서에 대 한 간단한 설명은 뿐만 아니라 이러한 두 가지 환경 간에 별도 구성 정보를 유지 관리에 대 한 기술 설명 데이터베이스 연결 문자열입니다. 이 자습서에는 프로덕션 환경 보다 자세히 적절 한 연결 문자열을 포함 하도록 구성할 수 있는 방법을 탐색 합니다.

## <a name="examining-the-connection-string-information"></a>연결 문자열 정보를 검토합니다.

책 검토 웹 응용 프로그램에서 사용 하는 연결 문자열은 응용 프로그램의 구성 파일에 저장 `Web.config`합니다. `Web.config`연결 문자열에 적절 하 게 저장 하기 위한 특별 한 섹션이 포함 되어 [ &lt;connectionStrings&gt;](https://msdn.microsoft.com/en-us/library/bf7sd233.aspx)합니다. `Web.config` 책 검토 웹 사이트에이 섹션에 정의 된 하나의 연결 문자열에 대 한 파일 `ReviewsConnectionString`:

[!code-xml[Main](configuring-the-production-web-application-to-use-the-production-database-cs/samples/sample1.xml)]

데이터 원본 연결 문자열-=. \SQLEXPRESS; AttachDbFilename = | DataDirectory|\Reviews.mdf;Integrated 보안 = True; 사용자 인스턴스 = True-각 옵션 및 세미콜론으로 구분 하는 옵션/값 쌍 및 등호로 구분 된 값을 가진 다양 한 옵션 및 값으로 구성 됩니다. 이 연결 문자열에서 사용 되는 네 가지 옵션이 있습니다.

- `Data Source`-(있는 경우) 데이터베이스 서버 및 데이터베이스 서버 인스턴스 이름의 위치를 지정 합니다. 값을 `.\SQLEXPRESS`, 한 예로 데이터베이스 서버 및 인스턴스 이름입니다. 기간 응용 프로그램;와 같은 컴퓨터에 데이터베이스 서버를 지정 합니다. 인스턴스 이름이 `SQLEXPRESS`합니다.
- `AttachDbFilename`-데이터베이스 파일의 위치를 지정 합니다. 자리 표시자를 포함 하는 값 `|DataDirectory|`, 응용 프로그램 s의 전체 경로 됨 `App_Data` 런타임 시 폴더입니다.
- `Integrated Security`-계정 자격 증명 (true) (false) 데이터베이스 또는 현재 Windows에 연결할 때 지정 된 사용자 이름/암호를 사용할지 여부를 나타내는 부울 값입니다.
- `User Instance`-SQL Server Express Edition 비관리 사용자에 게 로컬 컴퓨터에 연결 하 고 SQL Server Express Edition 데이터베이스에 연결할 수 있도록 할지 여부를 나타내는 관련 구성 옵션입니다. 참조 [SQL Server Express 사용자 인스턴스](https://msdn.microsoft.com/en-us/library/ms254504.aspx) 이 설정에 대 한 자세한 내용은 합니다.
  

허용 가능한 연결 문자열 옵션 사용 중인 ADO.NET 데이터베이스 공급자에 연결 하는 데이터베이스에 따라 다릅니다. 예를 들어 Oracle 데이터베이스에 연결 하는 데 사용 되는 데이터베이스에서와 다른 Microsoft SQL Server에 연결 하기 위한 연결 문자열입니다. 마찬가지로, SqlClient 공급자를 사용 하 여 Microsoft SQL Server 데이터베이스에 연결 하는 OLE DB 공급자를 사용할 때 보다 다른 연결 문자열을 사용 합니다.

같은 사이트를 사용 하 여 수동으로 데이터베이스 연결 문자열을 빌드할 수 [ConnectionStrings.com](http://www.connectionstrings.com/) 사용할 수 있는 옵션과 각 옵션에 대 한 리소스로 합니다. 그러나 보다 쉬운 접근을 Visual Studio에서 서버 탐색기에 데이터베이스를 추가 하는 다음 속성 창에서 연결 문자열을 잡고를 합니다. 프로덕션 데이터베이스 서버에 연결 문자열을 생성 하기 위한 마지막 기술을 사용 하 여 s를 사용 합니다.

Visual Studio를 열고 서버 탐색기 창으로 이동 합니다 (Visual Web Developer에서이 창을 라고 데이터베이스 탐색기). 데이터 연결 옵션 단추로 클릭 하 고 상황에 맞는 메뉴에서 추가 연결 옵션을 선택 합니다. 그림 1에 표시 된 마법사가 표시 됩니다. 적절 한 데이터 원본을 선택 하 고 계속을 클릭 합니다.


[![서버 탐색기에 새 데이터베이스를 추가 하려면 선택 합니다.](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image2.jpg)](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image1.jpg) 

**그림 1**: 서버 탐색기에 새 데이터베이스를 추가 하도록 선택 ([전체 크기 이미지를 보려면 클릭](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image3.jpg))


그런 다음 다양 한 데이터베이스 연결 정보 지정 (그림 2 참조). 웹 호스팅 회사에 게 등록 하는 경우 해야 제공한 정보-데이터베이스 서버 이름, 데이터베이스 이름, 사용자 이름 및 암호를 사용 하는 데이터베이스에 연결 하 고 등 데이터베이스에 연결 하는 방법에 있습니다. 이 정보를 입력 한 후이 마법사를 완료 하 고 서버 탐색기에 데이터베이스를 추가 하려면 확인을 클릭 합니다.


[![데이터베이스 연결 정보를 지정 합니다.](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image5.jpg)](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image4.jpg) 

**그림 2**: 데이터베이스 연결 정보 지정 ([전체 크기 이미지를 보려면 클릭](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image6.jpg))


이제 프로덕션 환경 데이터베이스 서버 탐색기에 나열 됩니다. 서버 탐색기에서 데이터베이스를 선택 하 고 속성 창으로 이동 합니다. 있습니다 라는 데이터베이스의 연결 문자열과 함께 연결 문자열 속성을 찾을 수 있습니다. 프로덕션 및 SqlClient 공급자는 Microsoft SQL Server 데이터베이스를 사용할 경우 연결 문자열이 다음과 비슷하게 표시 됩니다.

**데이터 원본 =*serverName*; 초기 카탈로그 =*databaseName*; 보안 정보 유지 = True; 사용자 ID =*username*; 암호 =*암호***

여기서 *serverName*, *databaseName*, *username*, 및 *암호* 데이터베이스 서버 이름, 데이터베이스에 대 한 값으로는 이름 및 사용자 이름 및 암호 웹 호스트 귀사에 게 제공 합니다.

## <a name="deploying-the-book-reviews-web-application"></a>책 검토 웹 응용 프로그램 배포

이전 자습서 개발 데이터베이스를 프로덕션 환경에 복사를 진행 하면서 하지만 데이터 기반 응용 프로그램 배포를 탐색 하지 못했습니다. 이 시점에서 프로덕션 환경 데이터베이스를 포함 하지만 정적 검토 된 책을 검토 하는 응용 프로그램의 버전을 사용 합니다. 업데이트 된 구성 정보와 함께 프로덕션 서버에 새, 데이터 기반 응용 프로그램을 배포 해야 합니다.

데이터 기반 응용 프로그램 배포 개발 환경에서 프로덕션 환경에 잠시 설명 합니다. 이 프로세스를 이전 자습서에서 자세히 설명 합니다. 세부 정보를 보려면 참고는 *FTP 클라이언트를 사용 하 여 웹 사이트 배포* 또는 *배포 사용자 웹 사이트를 사용 하 여 Visual Studio* 자습서입니다. 프로덕션 데이터베이스 연결 문자열을 대체 하는 의미 프로덕션 환경에서 사용 되는 인지 확인 해야 합니다 `Web.config` 파일을 배포 해야 합니다. 특히,이 수정할 `Web.config` 파일의 `<connectionStrings>` 요소 프로덕션 데이터베이스 연결 문자열을 포함 해야 하 고 다음과 비슷해야 합니다.

[!code-xml[Main](configuring-the-production-web-application-to-use-the-production-database-cs/samples/sample2.xml)]

연결 문자열에 `<connectionStrings>` 요소 이름이 (`ReviewsConnectionString`), 이제 개발 데이터베이스 연결 문자열 대신 프로덕션 데이터베이스 연결 문자열을 포함 합니다.

배포 워크플로 더욱 형식화 없는 경우 수동으로 수정 하거나는 `Web.config` (개발 데이터베이스 연결 문자열을 사용 하 여으로 되돌아가도록 기억 합니다. 배포 하기 전에 프로덕션 데이터베이스 연결 문자열을 사용 하는 파일 나중에) 하거나 별도 유지 관리 `Web.config` 파일을 프로덕션 환경 구성 정보는 프로덕션 환경으로 배포 프로세스의 일부로 업로드를 가져옵니다.

> [!NOTE]
> 실수로 배포 하는 경우는 `Web.config` 프로덕션에서 응용 프로그램 데이터베이스에 연결 하려고 할 때 오류가 됩니다 개발 데이터베이스 연결 문자열이 포함 된 파일입니다. 이 오류도 매니페스트는 `SqlException` 보고 서버를 찾을 수 없거나 액세스할 수 없으므로 메시지를 사용 합니다.


사이트에 프로덕션에 배포 된 후 브라우저를 통해 프로덕션 사이트를 방문 합니다. 참조 해야 하며 데이터 기반 응용 프로그램을 로컬로 실행할 때와 동일한 사용자 환경을 즐길 수 있습니다. 물론 프로덕션에 웹 사이트를 방문할 때 사이트는 연결 된 프로덕션 데이터베이스 서버는 데이터베이스를 사용 하 여 개발에서 개발 환경에서 웹 사이트를 방문 하는 반면 합니다. 그림 3는 *업무량이 직접 ASP.NET 3.5 24 시간 동안에서* (참고의 브라우저 주소 표시줄에 URL) 프로덕션 환경에서 웹 사이트에서 페이지를 검토 하세요.


[![데이터 기반 응용 프로그램은 이제 사용 가능한에서 프로덕션!](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image8.jpg)](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image7.jpg) 

**그림 3**: The Data-Driven 응용 프로그램은 이제 사용 가능한에서 프로덕션! ([전체 크기 이미지를 보려면 클릭](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image9.jpg))


### <a name="storing-connection-strings-in-a-separate-configuration-file"></a>별도 구성 파일에서 연결 문자열을 저장합니다.

개발 및 프로덕션 환경에 별도 구성 정보를 유지 하기 위한 일반적인 방법의 두 가지 버전은 `Web.config`: 개발 환경 및 프로덕션 환경에 한 합니다. 배포 시간 적절 한 `Web.config` 버전을 프로덕션 환경에 복사할 수 있습니다. 이상적으로 배포 워크플로의 일부분으로이 프로세스를 자동화 합니다.

두 개의 별도 유지 하는 대신 `Web.config` 필요에 따라 수 파일 보다 세부적인 차이 제공 합니다. 구성 하는 요소는 `Web.config` 파일에서 다음 참조 되는 외부 구성 파일에서 정의할 수 있습니다는 `Web.config` 파일입니다. 간단히 말해 개 사용할 수 있습니다 `Web.config` 두 환경 모두에서 databaseConnectionStrings.config 파일을 연결 문자열에는 참조 하는 응용 프로그램에서 사용 하 고 각 환경에 대 한 고유는 대 한 파일입니다. 필자는 서로 다른 구성 정보를 개별 파일로 구분 하는 좀 더 깔끔하게에서 제공 하는 기능을 원하는 `Web.config` 파일 등 명확 하 게 개발 및 프로덕션 환경 간의 구성 차이 구분 합니다.

이 기법을 사용 하려면 라는 웹 응용 프로그램에서 새 폴더를 만들어 시작 `ConfigSections`합니다. 다음으로 databaseConnectionStrings.dev.config 및 databaseConnectionStrings.production.config 라는이 새 폴더에 두 개의 파일을 추가 합니다. 다음으로 복사는 `<connectionStrings>` 요소 `Web.config` databaseConnectionStrings.dev.config 및 databaseConnectionStrings.production.config 파일에 다음의 연결 문자열을 수정 하 고는 databaseConnectionStrings.production.config은 프로덕션 데이터베이스 연결 문자열을 지정할 수 있도록 파일입니다. 예를 들어 databaseConnectionStrings.dev.config 파일에 있어야 테이블만 `<connectionStrings>` 개발 데이터베이스를 참조 하는 연결 문자열을 사용 하는 요소:

[!code-xml[Main](configuring-the-production-web-application-to-use-the-production-database-cs/samples/sample3.xml)]

마찬가지로, databaseConnectionStrings.production.config 파일만 포함 되어야 합니다는 `<connectionStrings>` 요소를 사용할 수 있지만 프로덕션 데이터베이스 연결 문자열이 있습니다.

DatabaseConnectionStrings.dev.config 파일의 복사본을 만들고 databaseConnectionStrings.config 라는 이름을 지정 합니다.

> [!NOTE]
> 이름을 지정할 수 있습니다는 구성 파일 이외의 노드 databaseConnectionStrings.config, d 원한다 면와 같은 `connectionStrings.config` 또는 `dbInfo.config`합니다. 하지만 사용 하 여 파일 이름을 지정 해야 한 `.config` 확장으로 `.config` 파일, 기본적으로 제공 되지 않습니다. ASP.NET 엔진에서. 다음과 같은 경우 파일을 다른 작업 이름을 `connectionStrings.txt`, 사용자가 브라우저를 가리킬 수 [www.yoursite.com/ConfigSettings/connectionStrings.txt](http://www.yoursite.com/ConfigSettings/connectionStrings.txt) 파일의 내용을 볼!


이 시점에서 `ConfigSections` 폴더 (그림 4 참조) 3 개의 파일을 포함 해야 합니다. DatabaseConnectionStrings.dev.config 및 databaseConnectionStrings.production.config 파일 각각 개발 및 프로덕션 환경에 대 한 연결 문자열을 포함 합니다. DatabaseConnectionStrings.config 파일 런타임 시 웹 응용 프로그램에서 사용할 연결 문자열 정보를 포함 합니다. 따라서 databaseConnectionStrings.config 파일 동일 해야 databaseConnectionStrings.dev.config 파일 개발 환경에서 프로덕션에 databaseConnectionStrings.config 파일 동일 해야 하는 반면 databaseConnectionStrings.production.config 합니다.


[![ConfigSections](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image11.jpg)](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image10.jpg) 

**그림 4**: ConfigSections ([전체 크기 이미지를 보려면 클릭](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image12.jpg))


이제 하도록 지시 해야 `Web.config` 해당 연결 문자열 저장소에 대 한 databaseConnectionStrings.config 파일을 사용 하도록 합니다. 열기 `Web.config` 바꾸고 기존 `<connectionStrings>` 요소를 다음으로:

[!code-xml[Main](configuring-the-production-web-application-to-use-the-production-database-cs/samples/sample4.xml)]

`configSource` 특성 지정 기준으로 실제 경로 `Web.config` 파일입니다. 하는 경우 외부 `.config` 파일이 동일한 디렉터리에 `Web.config` 다음의 파일 이름으로이 특성을 설정는 `.config` 파일입니다. 경우이 하위 디렉터리에 s 경우 databaseConnectionStrings.config와 마찬가지로 지정 ConfigSections\databaseConnectionStrings.config와 같은 폴더 및 파일 이름을 구분 하는 백슬래시를 사용 하 여 하위 폴더입니다.

이렇게 수정 개발 및 프로덕션 환경에 포함 동일한 `Web.config` 파일입니다. 이제 점만 databaseConnectionStrings.config 파일입니다. 프로덕션 환경에 databaseConnectionStrings.production.config 파일을 복사 하 고 databaseConnectionStrings.config로 이름을 바꿉니다. 나중에 프로덕션 데이터베이스 연결 문자열에는 변경 된 경우 해야 합니다 databaseConnectionStrings.production.config 파일에 더 하 고 다음 프로덕션 환경에 해당 파일을 업로드 databaseConnectionStrings.config 이름을 변경할 수 있습니다.

> [!NOTE]
> 에 대 한 정보를 지정할 수 `Web.config` 별도 파일을 사용 하 여 요소는 `configSource` 내에서 해당 파일을 참조 하는 특성 `Web.config`합니다.


## <a name="summary"></a>요약

일반적으로 데이터 기반 응용 프로그램 개발 및 프로덕션 환경에서 서로 다른 데이터베이스를 사용 합니다. 따라서 웹 응용 프로그램의 구성에 저장 된 데이터베이스 연결 문자열 환경당 고유 해야 합니다. 이 자습서에서는 프로덕션 데이터베이스 연결 문자열 및 두 환경에서 고유 연결 문자열 정보를 유지 관리 하는 방법을 결정 하는 방법을 찾았습니다.

만족도 매우 프로그래밍!

#### <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [연결 문자열 및 구성 파일](https://msdn.microsoft.com/en-us/library/ms254494.aspx)
- [데이터베이스 구성 정보 @ ConnectionStrings.com 문자열](http://www.connectionstrings.com/)
- [Web.config 파일에서 설정 이동](http://www.asp101.com/tips/index.asp?id=154)
- [에 대 한 기술 문서는 &lt;connectionStrings&gt; 요소](https://msdn.microsoft.com/en-us/library/bf7sd233.aspx)

>[!div class="step-by-step"]
[이전](deploying-a-database-cs.md)
[다음](configuring-a-website-that-uses-application-services-cs.md)
