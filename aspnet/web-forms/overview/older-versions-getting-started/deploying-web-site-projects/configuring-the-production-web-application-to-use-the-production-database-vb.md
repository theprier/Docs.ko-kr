---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-the-production-web-application-to-use-the-production-database-vb
title: 프로덕션 데이터베이스 (VB)를 사용 하도록 프로덕션 웹 응용 프로그램 구성 | Microsoft Docs
author: rick-anderson
description: 이전 자습서에서 설명 했 듯이 드물지 않습니다 구성 정보를 개발 및 프로덕션 환경에 따라 다릅니다. 이 es...
ms.author: aspnetcontent
ms.date: 04/23/2009
ms.assetid: a64a7aa0-6608-449e-83bf-1ef8cceee504
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-the-production-web-application-to-use-the-production-database-vb
msc.type: authoredcontent
ms.openlocfilehash: 952bdafd06143ce24e9e8beb0d6e6343400ffdc6
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37840702"
---
<a name="configuring-the-production-web-application-to-use-the-production-database-vb"></a>프로덕션 데이터베이스 (VB)를 사용 하도록 프로덕션 웹 응용 프로그램 구성
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/E/6/F/E6FE3A1F-EE3A-4119-989A-33D1A9F6F6DD/ASPNET_Hosting_Tutorial_08_VB.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/C/3/9/C391A649-B357-4A7B-BAA4-48C96871FEA6/aspnet_tutorial08_DBConfig_vb.pdf)

> 이전 자습서에서 설명 했 듯이 드물지 않습니다 구성 정보를 개발 및 프로덕션 환경에 따라 다릅니다. 개발 및 프로덕션 환경 간의 데이터베이스 연결 문자열을 다르게 이것이 데이터 기반 웹 응용 프로그램의 경우 특히 그렇습니다. 이 자습서에서는 자세히 적절 한 연결 문자열을 포함 하도록 프로덕션 환경을 구성 하는 방법을 살펴봅니다.


## <a name="introduction"></a>소개

데이터 기반 웹 응용 프로그램은 일반적으로 프로덕션 환경에서 경우 보다는 개발의 경우 다른 데이터베이스를 사용 합니다. 웹 호스트 공급자에 의해 호스팅되며 로컬로 개발한 응용 프로그램의 경우 개발 데이터베이스 일반적으로 컴퓨터에 있는 개발자가의 프로덕션 데이터베이스는 웹 호스팅 회사의 시설에서 데이터베이스 서버에서 호스트 되는 동안. 데이터 기반 웹 응용 프로그램을 배포 하려면 개발 데이터베이스로 프로덕션 데이터베이스 서버에 복사 해야 합니다. 이전 자습서에서이 단계를 수행 하는 방법에 살펴보았습니다.

웹 응용 프로그램에서 정보를 사용 하는 *연결 문자열* 데이터베이스와 연결 합니다. 일반적으로 저장 되 고 연결 문자열을 `Web.config`, 데이터베이스 서버 이름, 데이터베이스, 보안 컨텍스트 및 기타 정보의 이름을 지정 합니다. 웹 응용 프로그램에서 사용 하는 데이터베이스 개발 또는 프로덕션 환경에서 웹 응용 프로그램의 실행 여부에 따라 달라 집니다, 때문에 두 환경 간의 연결 문자열이 달라 야 합니다.

개발 및 프로덕션 환경 간에 다를 구성 정보에 대 한 일반적이 지 않은 것입니다. 합니다 *일반적인 구성 차이 간의 개발 및 프로덕션* 자습서에 대 한 간략 한 설명 뿐만 아니라 이러한 두 환경 간에 별도 구성 정보를 유지 관리 하는 기술을 설명 데이터베이스 연결 문자열입니다. 이 자습서에서는 자세히 적절 한 연결 문자열을 포함 하도록 프로덕션 환경을 구성 하는 방법을 살펴봅니다.

## <a name="examining-the-connection-string-information"></a>연결 문자열 정보를 검사합니다.

도 서 리뷰 웹 응용 프로그램에서 사용 된 연결 문자열은 응용 프로그램의 구성 파일에 저장 됩니다 `Web.config`합니다. `Web.config` 연결 문자열을 적절 하 게 저장 하기 위한 특별 한 섹션이 포함 되어 있습니다 [ &lt;connectionStrings&gt;](https://msdn.microsoft.com/library/bf7sd233.aspx)합니다. 합니다 `Web.config` 도 서 리뷰 웹 사이트 라는이 섹션에 정의 된 하나의 연결 문자열에 대 한 파일 `ReviewsConnectionString`:

[!code-xml[Main](configuring-the-production-web-application-to-use-the-production-database-vb/samples/sample1.xml)]

데이터 원본 연결 문자열 =. \SQLEXPRESS; AttachDbFilename = | DataDirectory|\Reviews.mdf;Integrated Security = True; 사용자 인스턴스 = True-옵션/값 쌍을 세미콜론 및 각 옵션을 구분 하 고 등호를 구분 하는 값을 사용 하 여 다양 한 옵션 및 값으로 구성 됩니다. 이 연결 문자열에 사용 되는 네 가지 옵션은 같습니다.

- `Data Source` -(있는 경우) 데이터베이스 서버 및 데이터베이스 서버 인스턴스 이름을의 위치를 지정 합니다. 값을 `.\SQLEXPRESS`, 예로 데이터베이스 서버 및 인스턴스 이름을 있는 합니다. 데이터베이스 서버 응용 프로그램으로 동일한 컴퓨터에는 기간 지정 인스턴스 이름이 `SQLEXPRESS`합니다.
- `AttachDbFilename` -데이터베이스 파일의 위치를 지정 합니다. 자리 표시자를 포함 하는 값 `|DataDirectory|`에 응용 프로그램의 전체 경로로 확인 되 `App_Data` 런타임에 폴더입니다.
- `Integrated Security` -연결할 때 (false) 데이터베이스 또는 현재 Windows 계정 자격 증명 (true)을 지정된 하는 사용자 이름/암호를 사용할지 여부를 나타내는 부울 값입니다.
- `User Instance` -SQL Server Express 버전으로 로컬 컴퓨터의 관리자가 아닌 사용자가 연결 하 고 SQL Server Express Edition 데이터베이스에 연결할 수 있도록 할지 여부를 지정 하는 특정 구성 옵션입니다. 참조 [SQL Server Express 사용자 인스턴스](https://msdn.microsoft.com/library/ms254504.aspx) 이 설정에 대 한 자세한 내용은 합니다.
  

허용 되는 연결 문자열 옵션에 연결 하는 데이터베이스에 따라 달라 집니다 하며 [ADO.NET](http://ADO.NET) 데이터베이스 공급자를 사용 합니다. 예를 들어, Oracle 데이터베이스에 연결할 때 사용할 데이터베이스에서 다른 Microsoft SQL Server에 연결 하기 위한 연결 문자열입니다. 마찬가지로 SqlClient 공급자를 사용 하 여 Microsoft SQL Server 데이터베이스에 연결 된 OLE DB 공급자를 사용할 때 보다 다양 한 연결 문자열을 사용 합니다.

같은 사이트를 사용 하 여 수동으로 데이터베이스 연결 문자열을 빌드할 수 있습니다 [ConnectionStrings.com](http://www.connectionstrings.com/) 리소스로 사용할 수 있는 옵션에 대 한 합니다. 그러나 보다 쉬운 접근을 Visual Studio에서 서버 탐색기에 데이터베이스를 추가 하는 다음 속성 창에서 연결 문자열입니다. 이 후자의 기법을 사용 하 여 프로덕션 데이터베이스 서버에 연결 문자열을 생성 하는 것에 대 한 s 수 있습니다.

Visual Studio를 열고 다음 서버 탐색기 창에 탐색 (Visual Web developer에서이 창 이라고 데이터베이스 탐색기). 데이터 연결 옵션을 단추로 클릭 하 고 상황에 맞는 메뉴에서 추가 연결 옵션을 선택 합니다. 그러면 그림 1 에서처럼 마법사. 적절 한 데이터 원본을 선택 하 고 계속을 클릭 합니다.


[![서버 탐색기에 새 데이터베이스를 추가 하려면 선택 합니다.](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image2.jpg)](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image1.jpg) 

**그림 1**: 서버 탐색기에 새 데이터베이스를 추가 하려면 선택 ([큰 이미지를 보려면 클릭](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image3.jpg))


다음으로, 다양 한 데이터베이스 연결 정보를 지정 (그림 2 참조). 웹 호스팅 회사를 사용 하 여 등록할 때 해당 데이터베이스 서버 이름, 데이터베이스 이름, 사용자 이름 및 암호를 사용 하는 데이터베이스에 연결 하 고 등 데이터베이스에 연결 하는 방법에 정보를 제공 하 고 있어야 합니다. 이 정보를 입력 한 후이 마법사를 완료 하 고 서버 탐색기에 데이터베이스를 추가 하려면 확인을 클릭 합니다.


[![데이터베이스 연결 정보 지정](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image5.jpg)](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image4.jpg) 

**그림 2**: 데이터베이스 연결 정보 지정 ([큰 이미지를 보려면 클릭](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image6.jpg))


이제 프로덕션 환경 데이터베이스 서버 탐색기에 나열 됩니다. 서버 탐색기에서 데이터베이스를 선택 하 고 속성 창으로 이동 합니다. 여기서 명명 된 데이터베이스의 연결 문자열을 사용 하 여 연결 문자열 속성을 찾을 수 있습니다. 프로덕션 및 SqlClient 공급자에서 Microsoft SQL Server 데이터베이스를 사용 하는 경우 연결 문자열에 다음과 비슷하게 표시 됩니다.

<strong>데이터 원본 =<em>serverName</em>; 초기 카탈로그 =<em>databaseName</em>; Persist Security Info = True; 사용자 ID =<em>username</em>; 암호 =*암호</strong>*

여기서 *serverName*를 *databaseName*를 *username*, 및 *암호* 데이터베이스 서버 이름, 데이터베이스에 대 한 값으로는 이름 및 username 및 password 웹 호스트 회사에 게 제공 합니다.

## <a name="deploying-the-book-reviews-web-application"></a>책 검토 웹 응용 프로그램 배포

이전 자습서 프로덕션 환경에 개발 데이터베이스 복사를 진행 하면서 하지만 데이터 기반 응용 프로그램을 배포 하는 것을 탐색 하지 않았습니다. 이 시점에서 프로덕션 환경 데이터베이스를 포함 하지만 정적 검토를 사용 하 여 서평 응용 프로그램의 버전을 사용 하는 합니다. 업데이트 된 구성 정보와 함께 프로덕션 서버에 새, 데이터 기반 응용 프로그램을 배포 해야 합니다.

시간을 내어 데이터 기반 응용 프로그램 개발 환경에서 프로덕션에 배포 합니다. 이 프로세스는 이전 자습서에서 세부 정보에 설명 했습니다. 리프레셔가 필요한 경우 참조를 *FTP 클라이언트를 사용 하 여 웹 사이트를 배포* 또는 *배포 웹 사이트를 사용 하 여 Visual Studio* 자습서입니다. 프로덕션 데이터베이스 연결 문자열을 대체 하는 것을 의미 하는 프로덕션 환경에서 사용 된 것을 인지 확인 해야 `Web.config` 파일을 배포 해야 합니다. 수정이 특히 `Web.config` s 파일 `<connectionStrings>` 요소 프로덕션 데이터베이스 연결 문자열을 포함 해야 하며 다음과 유사 합니다.

[!code-xml[Main](configuring-the-production-web-application-to-use-the-production-database-vb/samples/sample2.xml)]

연결 문자열에 `<connectionStrings>` 요소 이름이 (`ReviewsConnectionString`), 개발 데이터베이스 연결 문자열 대신 프로덕션 데이터베이스 연결 문자열을 포함 하 고 있습니다. 하지만 합니다.

배포 워크플로 더욱 형식화 없다면 수동으로 수정 하거나는 `Web.config` (개발 데이터베이스 연결 문자열을 사용 하도록 다시 되돌리려면 기억 합니다. 배포 하기 전에 프로덕션 데이터베이스 연결 문자열을 사용 하는 파일 나중에) 별도 유지 관리 또는 `Web.config` 배포 프로세스의 일환으로 프로덕션 환경으로 업로드 가져옵니다 프로덕션 환경 구성 정보를 사용 하 여 파일입니다.

> [!NOTE]
> 실수로 배포 하는 경우는 `Web.config` 프로덕션에서 응용 프로그램 데이터베이스에 연결 하려고 할 때 오류가 발생 됩니다 개발 데이터베이스 연결 문자열을 포함 하는 파일입니다. 이 오류와 매니페스트는 `SqlException` 서버를 찾을 수 없거나 액세스할 수 없습니다를 보고 하는 메시지를 사용 하 여 합니다.


프로덕션 사이트에 배포 되 면 브라우저를 통해 프로덕션 사이트를 방문 합니다. 데이터 기반 응용 프로그램을 로컬로 실행할 때와 동일한 사용자 환경을 즐길 수 및 표시 됩니다. 물론 프로덕션에서 웹 사이트를 방문 하는 경우 사이트 전원이 프로덕션 데이터베이스 서버에서 데이터베이스를 사용 하 여 개발에서 개발 환경에서 웹 사이트를 방문 하는 반면 있습니다. 그림 3 합니다 *가르치는 직접 ASP.NET 3.5 24 시간 동안에서* 프로덕션 환경 (참고의 브라우저 주소 표시줄에서 URL)에서 웹 사이트에서 페이지를 검토 합니다.


[![데이터 기반 응용 프로그램은 이제 사용 가능한에서 프로덕션!](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image8.jpg)](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image7.jpg) 

**그림 3**: The Data-Driven 응용 프로그램은 이제 사용 가능한에서 프로덕션! ([클릭 하 여 큰 이미지 보기](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image9.jpg))


### <a name="storing-connection-strings-in-a-separate-configuration-file"></a>별도 구성 파일에서 연결 문자열 저장

두 버전의 개발 및 프로덕션 환경에 대 한 별도 구성 정보를 유지 관리 하기 위한 일반적인 기술 되는 `Web.config`: 개발 환경 및 프로덕션에 대 한 하나. 배포 시 적절 한 `Web.config` 버전을 프로덕션 환경으로 복사할 수 있습니다. 이상적으로이 프로세스 배포 워크플로의 일부로 자동화할 수는 있습니다.

두 개의 별도 유지 관리 하는 대신 `Web.config` 필요에 따라 있습니다 파일 보다 세부적인 차이 제공 합니다. 구성 하는 요소는 `Web.config` 파일에서 다음 참조 되는 외부 구성 파일에서 정의할 수 있습니다는 `Web.config` 파일입니다. 간단히 말해 하나가 있습니다 `Web.config` 두 환경 모두는 연결 문자열을 포함 하는 databaseConnectionStrings.config 파일을 참조 하는 응용 프로그램에서 사용 하는 각 환경에 대 한 고유한 것에 대 한 파일입니다. 필자는 별도 파일에 서로 다른 구성 정보를 구분 하는 좀 더 깔끔하게는 간단 하 고 `Web.config` 파일 등 명확 하 게 개발 및 프로덕션 환경 간의 구성 차이 구분 합니다.

이 기법을 사용 하려면 이라는 웹 응용 프로그램에서 새 폴더를 만들어 시작 `ConfigSections`합니다. 다음으로, databaseConnectionStrings.dev.config 및 databaseConnectionStrings.production.config 라는 새 폴더에 두 개의 파일을 추가 합니다. 다음으로 복사 합니다 `<connectionStrings>` 요소에서 `Web.config` databaseConnectionStrings.dev.config 및 databaseConnectionStrings.production.config 파일로 다음의 연결 문자열을 수정 하 고는 databaseConnectionStrings.production.config 파일에 프로덕션 데이터베이스 연결 문자열을 지정 합니다. 예를 들어 databaseConnectionStrings.dev.config 파일에 있어야만 `<connectionStrings>` 개발 데이터베이스를 참조 하는 연결 문자열을 사용 하 여 요소:

[!code-xml[Main](configuring-the-production-web-application-to-use-the-production-database-vb/samples/sample3.xml)]

마찬가지로, databaseConnectionStrings.production.config 파일만 포함 해야는 `<connectionStrings>` 요소를 사용할 수 있지만 프로덕션 데이터베이스 연결 문자열이 있는 합니다.

DatabaseConnectionStrings.dev.config 파일의 복사본을 만들고 databaseConnectionStrings.config 라는 이름을 지정 합니다.

> [!NOTE]
> 이름을 지정할 수 있습니다 구성 파일 databaseConnectionStrings.config, 이외의 경우 d와 같은 `connectionStrings.config` 또는 `dbInfo.config`합니다. 그러나 사용 하 여 파일 이름을 지정 해야는 `.config` 확장 `.config` 파일에 기본적으로 제공 하지 ASP.NET 엔진입니다. 파일에 다른 이름을 지정 하면 같은 `connectionStrings.txt`, 사용자가 브라우저를 가리킬 수 있습니다 [www.yoursite.com/ConfigSettings/connectionStrings.txt](http://www.yoursite.com/ConfigSettings/connectionStrings.txt) 선택한 파일의 내용을 봅니다.


이 시점에서 `ConfigSections` 폴더 (그림 4 참조) 파일 세 개를 포함 해야 합니다. DatabaseConnectionStrings.dev.config 파일과 databaseConnectionStrings.production.config 각각 개발 및 프로덕션 환경에 대 한 연결 문자열을 포함 합니다. DatabaseConnectionStrings.config 파일에는 런타임 시 웹 응용 프로그램에서 사용할 연결 문자열 정보를 포함 합니다. 따라서 databaseConnectionStrings.config 파일 같아야 databaseConnectionStrings.dev.config 파일 개발 환경에서 프로덕션에서 databaseConnectionStrings.config 파일 동일 해야 하는 반면 databaseConnectionStrings.production.config 합니다.


[![ConfigSections](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image11.jpg)](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image10.jpg) 

**그림 4**: ConfigSections ([큰 이미지를 보려면 클릭](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image12.jpg))


이제 지시 해야 `Web.config` 해당 연결 문자열 저장소에 대 한 databaseConnectionStrings.config 파일을 사용 하도록 합니다. `Web.config`을 열고 기존 `<connectionStrings>` 요소를 다음과 같이 바꿉니다.

[!code-xml[Main](configuring-the-production-web-application-to-use-the-production-database-vb/samples/sample4.xml)]

합니다 `configSource` 특성에 상대적인 실제 경로 지정 합니다 `Web.config` 파일입니다. 경우 외부 `.config` 파일이 동일한 디렉터리에 있는 `Web.config` 설정한 다음 파일 이름으로이 특성을 `.config` 파일입니다. 하는 경우 해당 하위 디렉터리에서 그대로 databaseConnectionStrings.config 사용 하는 경우 지정 ConfigSections\databaseConnectionStrings.config 같은 폴더 및 파일 이름을 구분 하는 백슬래시를 사용 하 여 하위 폴더입니다.

이렇게 수정 하면 개발 및 프로덕션 환경 같으면 `Web.config` 파일입니다. 이제 점만 databaseConnectionStrings.config 파일입니다. 프로덕션으로 databaseConnectionStrings.production.config 파일을 복사 하 고 databaseConnectionStrings.config로 바꿉니다. 나중에 프로덕션 데이터베이스 연결 문자열에는 변경 내용이 있으면 해야 databaseConnectionStrings.production.config 파일을 프로덕션에서 해당 파일을 업로드 한 다음 databaseConnectionStrings.config 이름을 바꾸면 합니다.

> [!NOTE]
> 에 대 한 정보를 지정할 수 있습니다 `Web.config` 별도 파일 및 사용 하 여 요소를 `configSource` 내에서 해당 파일을 참조 하는 특성 `Web.config`합니다.


## <a name="summary"></a>요약

일반적으로 데이터 기반 응용 프로그램 개발 및 프로덕션 환경에서 다른 데이터베이스를 사용합니다. 따라서 웹 응용 프로그램의 구성에 저장 된 데이터베이스 연결 문자열 환경 별로 고유 해야 합니다. 이 자습서에서는 두 환경에서 고유한 연결 문자열 정보를 유지 관리 하는 방법을 확인 하 고 프로덕션 데이터베이스 연결 문자열을 확인 하는 방법에 살펴보았습니다.

즐거운 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [연결 문자열 및 구성 파일](https://msdn.microsoft.com/library/ms254494.aspx)
- [데이터베이스 구성 정보 @ ConnectionStrings.com 문자열](http://www.connectionstrings.com/)
- [Web.config 파일에서 설정 이동](http://www.asp101.com/tips/index.asp?id=154)
- [에 대 한 기술 설명서를 &lt;connectionStrings&gt; 요소](https://msdn.microsoft.com/library/bf7sd233.aspx)

> [!div class="step-by-step"]
> [이전](deploying-a-database-vb.md)
> [다음](configuring-a-website-that-uses-application-services-vb.md)
