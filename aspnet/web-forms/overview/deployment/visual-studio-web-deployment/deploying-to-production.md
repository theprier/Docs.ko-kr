---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-production
title: 'Visual Studio를 사용 하 여 ASP.NET 웹 배포: 프로덕션에 배포 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시) 실행 하 여 웹 응용 프로그램을 Azure 앱 서비스 웹 앱 또는 타사 호스팅 공급자 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/15/2013
ms.topic: article
ms.assetid: 416438a1-3b2f-4d27-bf53-6b76223c33bf
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-production
msc.type: authoredcontent
ms.openlocfilehash: f3b3898bd003ace100ba05619f2c45ca808462df
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30889809"
---
<a name="aspnet-web-deployment-using-visual-studio-deploying-to-production"></a>Visual Studio를 사용 하 여 ASP.NET 웹 배포: 프로덕션에 배포
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> 이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시) Visual Studio 2012 또는 Visual Studio 2010을 사용 하 여 웹 응용 프로그램을 Azure 앱 서비스 웹 앱 또는 타사 호스팅 공급자입니다. 계열에 대 한 정보를 참조 하십시오. [시리즈의 첫 번째 자습서](introduction.md)합니다.


## <a name="overview"></a>개요

이 자습서에서는 Microsoft Azure 계정을 설정 하 고 스테이징 및 프로덕션 환경을 만들 준비를 ASP.NET 웹 응용 프로그램 배포 및 한 번의 클릭 Visual Studio를 사용 하 여 프로덕션 환경 기능을 게시 합니다.

원하는 경우에 제 3 자 호스팅 공급자에 배포할 수 있습니다. 각 공급자에는 계정 및 웹 사이트 관리에 대 한 자체 사용자 인터페이스는 점을 제외 하 고이 자습서에 설명 된 절차의 대부분은 Azure 또는 호스팅 공급자에 대 한 동일 합니다. 호스팅 공급자를 찾을 수 있습니다는 [공급자의 갤러리](https://www.microsoft.com/web/hosting) Microsoft.com 웹 사이트에 있습니다.

미리 알림: 오류 메시지가 자습서를 진행할 때 작동 하지 않는 경우 해야이 자습서 시리즈의 문제 해결 페이지를 확인 합니다.

## <a name="get-a-microsoft-azure-account"></a>Microsoft Azure 계정 얻기

Azure 계정이 없는 경우 몇 분에서에서 무료 평가판 계정을 만들 수 있습니다. 자세한 내용은 참조 [Azure 무료 평가판](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)합니다.

## <a name="create-a-staging-environment"></a>스테이징 환경 만들기

> [!NOTE]
> 이 자습서 기록 되었기 때문 Azure 앱 서비스 다양 한 준비 및 프로덕션 환경을 만들기 위한 프로세스를 자동화 하는 새 기능을 추가 합니다. 참조 [스테이징 환경에서 Azure 앱 서비스 웹 앱에 대 한 설정](https://azure.microsoft.com/documentation/articles/web-sites-staged-publishing/)합니다.


에 설명 된 대로 [테스트 환경 자습서로 배포](deploying-to-iis.md)는 가장 신뢰할 수 있는 테스트 환경은 프로덕션 웹 사이트와 방금 호스팅 공급자에서 웹 사이트입니다. 호스팅 공급자는 대부분에 중요 한 추가 비용에 대해이 가치가 해야 하지만 Azure에서 스테이징 응용 프로그램으로 추가 무료 웹 앱을 만들 수 있습니다. 또한 데이터베이스, 해야 이며 프로덕션 데이터베이스의 비용을 통해 해당 추가 비용은 없음 또는 / 최소 합니다. Azure의 비용을 지불이 아니라 각 데이터베이스에 대 한 데이터베이스 저장을 사용 하면 용량을 초과 하 고 준비 단계에서 사용 하는 추가 저장소 양을 최소화 됩니다.

에 설명 된 대로 [테스트 환경 자습서로 배포](deploying-to-iis.md), 스테이징 및 프로덕션 데이터베이스에 두 개의 데이터베이스를 배포 하 겠 군요. 분리 하려는 경우 프로세스는 같습니다는 각 환경에 대 한 추가 데이터베이스를 만들면 됩니다 게시 프로필을 만들 때 각 데이터베이스에 대 한 올바른 대상 문자열을 선택 합니다.

이 자습서의이 섹션에 만듭니다 web app 및 스테이징 환경에 사용할 데이터베이스를 및 스테이징에 배포 하 고 있는 만들기 및 프로덕션 환경에 배포 하기 전에 테스트 합니다.

> [!NOTE]
> 다음 단계에는 Azure 관리 포털을 사용 하 여 Azure 앱 서비스의 웹 응용 프로그램을 만드는 방법을 보여 줍니다. Azure SDK의 최신 버전의 서버 탐색기를 사용 하 여 Visual Studio를 종료 하지 않고이 수행할 수 있습니다. Visual Studio 2013에서 게시 대화 상자에서 직접 웹 응용 프로그램을 만들 수 있습니다. 자세한 내용은 참조 [Azure 앱 서비스에서 ASP.NET 웹 응용 프로그램을 만듭니다.](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)


1. 에 [Azure 관리 포털](https://manage.windowsazure.com/), 클릭 **웹 사이트**, 클릭 하 고 **새로**합니다.
2. 클릭 **웹 사이트**, 클릭 하 고 **사용자 지정 만들기**합니다.

    **새 웹 사이트-사용자 지정 만들기** 마법사가 열립니다. **사용자 지정 만들기** 마법사를 사용 하는 동시에 웹 사이트 및 데이터베이스를 만들 수 있습니다.
3. 에 **웹 사이트 만들기** 단계 마법사에 문자열을 입력에서 **URL** 응용 프로그램에 대 한 고유 URL로 사용 하 여 상자의 스테이징 환경입니다. 예를 들어 ContosoUniversity staging123 (고유 하 게 지정 ContosoUniversity 준비를 수행 하는 경우 끝에 임의의 숫자 포함)을 입력 합니다.

    전체 URL 텍스트 상자 옆에 볼 수 있는 접미사 함께 내용을 여기에 입력으로 구성 됩니다.
4. 에 **지역** 드롭 다운 목록에서 사용자와 가장 가까운 지역을 선택 합니다.

    이 설정은 웹 응용 프로그램에서 실행 되는 데이터 센터를 지정 합니다.
5. 에 **데이터베이스** 드롭 다운 목록에서 선택 **새 SQL 데이터베이스 만들기**합니다.
6. 에 **DB 연결 문자열 이름** 상자에서 기본값을 그대로 두고 *DefaultConnection*합니다.
7. 오른쪽 상자의 맨 아래에 있는 화살표를 클릭 합니다.

    다음 그림에서는 **웹 사이트 만들기** 샘플 값에 포함 된 대화 상자. URL과 입력 한 지역 달라 집니다.

    ![웹 사이트 단계 만들기](deploying-to-production/_static/image1.png)

    마법사 열립니다는 **데이터베이스 설정 지정** 단계입니다.
8. 에 **이름** 상자에 입력 *ContosoUniversity* 고유 하 게 것, 예를 들어 난수 더하기 *ContosoUniversity123*합니다.
9. 에 **서버** 상자 **새 SQL 데이터베이스 서버**합니다.
10. 관리자 이름 및 암호를 입력 합니다.

    기존 이름 및 암호를 여기 입력 되지 않습니다. 새 이름 및 데이터베이스에 액세스할 때 나중에 사용 하려면 지금 정의 하는 암호를 입력 합니다.
11. 에 **지역** 상자에서 웹 앱에 대해 선택한 동일한 지역을 선택 합니다.

    웹 서버와 데이터베이스 서버를 동일한 지역에 유지 하면 최상의 성능을 제공 하 고 비용을 최소화 합니다.
12. 작업이 완료 되 나타내려면 상자 맨 아래에 있는 확인 표시를 클릭 합니다.

    다음 그림에서는 **데이터베이스 설정 지정** 샘플 값에 포함 된 대화 상자. 입력 한 값은 달라질 수 있습니다.

    ![데이터베이스 설정 단계 새 웹 사이트-의 데이터베이스 마법사를 사용 하 여 만들기](deploying-to-production/_static/image2.png)

    관리 포털 웹 사이트 페이지를 반환 및 **상태** 열에는 웹 응용 프로그램 생성 되 고 있음을 표시 합니다. 잠시 후 (일반적으로 보다 작음 1 분)는 **상태** 열에는 웹 응용 프로그램을 만들었음을 표시 합니다. 왼쪽 탐색 모음에서 계정에 제공 하는 웹 앱의 수 옆에 표시는 **웹 사이트** 아이콘과 데이터베이스 수가 옆에 표시 된 **SQL 데이터베이스** 아이콘입니다.

    ![관리 포털에서 만든 웹 사이트의 웹 사이트 페이지](deploying-to-production/_static/image3.png)

    그림에서 예제 응용 프로그램에서 웹 앱 이름은 달라 집니다.

## <a name="deploy-the-application-to-staging"></a>스테이징 응용 프로그램 배포

웹 앱 및 스테이징 환경에 대 한 데이터베이스를 만든 프로젝트를 배포할 수 있습니다.

> [!NOTE]
> 이러한 지침을 다운로드 하 여 게시 프로필을 만드는 방법을 보여 줍니다는 *.publishsettings* 파일 뿐만 아니라 타사 호스팅 공급자에 대해 뿐만 아니라 Azure에 대 한 작동 합니다. 최신 Azure SDK도를 사용 하면 Visual Studio에서 Azure에 직접 연결 하 고 Azure 계정에서 사용 하는 웹 응용 프로그램의 목록에서 선택할 수 있습니다. Visual Studio 2013에서에 로그인 하려면에서 Azure로의 **웹 게시** 대화 또는 **서버 탐색기** 창. 자세한 내용은 참조 [Azure 앱 서비스에서 ASP.NET 웹 앱을 만들](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)합니다.


### <a name="download-the-publishsettings-file"></a>.Publishsettings 파일을 다운로드

1. 방금 만든 웹 응용 프로그램의 이름을 클릭 합니다.

    ![사이트를 대시보드로 이동 하려면 클릭](deploying-to-production/_static/image4.png)
2. 아래 **눈에 보는** 에 **대시보드** 탭을 클릭 **게시 프로필 다운로드**합니다.

    ![다운로드 게시 프로필 링크](deploying-to-production/_static/image5.png)

    이 단계는 모든 응용 프로그램 웹 앱을 배포 하는 데 필요한 설정을 포함 하는 파일을 다운로드 합니다. Visual Studio에이 파일을 가져옵니다 하므로이 정보를 수동으로 입력할 필요가 없습니다.
3. 저장 된 *.publishsettings* Visual Studio에서 액세스할 수 있는 폴더의 파일입니다.

    ![.publishsettings 파일을 저장합니다.](deploying-to-production/_static/image6.png)

    > [!WARNING]
    > 보안-는 *.publishsettings* 자격 증명 (인코딩되지 않음) Azure 구독 및 서비스를 관리 하는 데 사용 되는 파일에 포함 되어 있습니다. 이 파일에 대 한 보안 모범 사례를 일시적으로 원본 디렉터리 외부 (예: Libraries\Documents 폴더)를 저장 한 다음 가져오기가 완료 되 면 삭제 됩니다. 에 액세스할 수 있는 악의적인 사용자는 *.publishsettings* 파일 편집, 생성 및, Azure 서비스를 삭제할 수 있습니다.

### <a name="create-a-publish-profile"></a>게시 프로필 만들기

1. Visual Studio에서 ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 **솔루션 탐색기** 선택 **게시** 상황에 맞는 메뉴입니다.

    **웹 게시** 마법사가 열립니다.
2. 클릭는 **프로필** 탭 합니다.
3. **가져오기**를 클릭합니다.
4. 로 이동 된 *.publishsettings* 이전에 다운로드 한 파일을 누르고 **열려**합니다.

    ![가져오기 게시 설정 대화 상자](deploying-to-production/_static/image7.png)
5. 에 **연결** 탭을 클릭 **연결 유효성 검사** 를 설정이 정확한 지 확인 합니다.

    연결 검증 된 녹색 확인 표시가 옆에 표시 되는 **연결 유효성 검사** 단추입니다.

    일부 호스팅 공급자를 클릭할 때 **연결 유효성 검사**, 표시 될 수 있습니다는 **인증서 오류** 대화 상자. 이렇게 하면 서버 이름이 예상 대로 인지 확인 합니다. 서버 이름이 올바른 경우 선택 **Visual Studio의 이후 세션에 대 한이 인증서 저장** 클릭 **Accept**합니다. (이 오류는 SSL 인증서를 배포 하는 URL에 대 한 구매 비용을 방지 하기 위해 호스팅 공급자가 선택한 의미 하는 데 사용 합니다. 유효한 인증서를 사용 하 여 보안 연결을 설정 하려는 호스팅 공급자에 문의 합니다.)
6. **다음**을 클릭합니다.

    ![연결 성공 아이콘 및 연결 탭에서 다음 단추](deploying-to-production/_static/image8.png)
7. 에 **설정** 탭을 확장 하 고 **파일 게시 옵션**를 선택한 후 **응용 프로그램에서 파일을 제외\_데이터 폴더**합니다.

    아래에 있는 다른 옵션에 대 한 내용은 **파일 게시 옵션**, 참조는 [IIS에 배포](deploying-to-iis.md) 자습서입니다. 스크린 샷 데이터베이스 구성 단계 후에이 단계와 다음 데이터베이스 구성 절차의 결과 해당 보여 줍니다.
8. 아래 **DefaultConnection** 에 **데이터베이스** 섹션에서 멤버 자격 데이터베이스에 대 한 데이터베이스 배포를 구성 합니다.
9. 1. 선택 **데이터베이스 업데이트**합니다.

        **원격 연결 문자열** 바로 아래의 상자 **DefaultConnection** .publishsettings 파일에서 연결 문자열을 사용 하 여 채워집니다. 연결 문자열에 일반 텍스트로 저장 되어 있는 SQL Server 자격 증명에 포함 되어는 *.pubxml* 파일입니다. 영구적으로 저장 하지 않으려는 경우에 데이터베이스를 배포한 후 게시 프로필에서 제거 하 및 대신 Azure에서 저장할 수 있습니다. 자세한 내용은 참조 [유지 하는 방법을 ASP.NET 데이터베이스 연결 문자열 보안 소스에서 Azure에 배포할 때](http://www.hanselman.com/blog/HowToKeepYourASPNETDatabaseConnectionStringsSecureWhenDeployingToAzureFromSource.aspx) Scott Hanselman의 블로그입니다.
      2. 클릭 **데이터베이스 업데이트 구성**합니다.
      3. 에 **데이터베이스 업데이트 구성** 대화 상자를 클릭 **SQL 스크립트 추가**합니다.
      4. 에 **SQL 스크립트 추가** 상자는 *aspnet-데이터-prod.sql* 솔루션 폴더에 이전에 저장 하 고 클릭 한 다음 스크립트는 **열려**합니다.
      5. 닫기는 **데이터베이스 업데이트 구성** 대화 상자.
10. 아래 **SchoolContext** 에 **데이터베이스** 섹션에서 **실행 Code First 마이그레이션을 (응용 프로그램 시작 시 실행)** 합니다.

    Visual Studio에서 표시 **Code First 마이그레이션 실행** 대신 **데이터베이스 업데이트** 에 대 한 `DbContext` 클래스입니다. 사용 하 여 액세스할 수 있는 데이터베이스를 배포 하려면 마이그레이션 대신 dbDacFx 공급자를 사용 하려는 경우는 `DbContext` 클래스를 참조 하십시오 [마이그레이션 없이 코드 첫 번째 데이터베이스를 어떻게 배포 합니까?](https://msdn.microsoft.com/library/ee942158.aspx#deploy_code_first_without_migrations) 에서 Visual Studio에 대 한 웹 배포 FAQ 및 MSDN에서 ASP.NET을 추가 합니다.

    **설정을** 탭은 이제 다음 예제와 같습니다.

    ![준비 단계에 대 한 설정 탭](deploying-to-production/_static/image9.png)
11. 프로필을 저장 하 고이 파일 이름을 하려면 다음 단계를 수행 *준비*:

    1. 클릭는 **프로필** 탭을 클릭 한 다음 **프로필 관리**합니다.
    2. 가져오기에는 두 개의 새 프로필, FTP 및 웹 배포에 대 한 만들어집니다. 웹 배포 프로필 구성:이 프로필을 이름 바꾸기 *준비*합니다.

        ![스테이징 프로필 이름 바꾸기](deploying-to-production/_static/image10.png)
    3. 닫기는 **웹 게시 프로필 편집** 대화 상자.
    4. 닫기는 **웹 게시** 마법사.

### <a name="configure-a-publish-profile-transform-for-the-environment-indicator"></a>환경 표시기에 대 한 게시 프로필 변환 구성

> [!NOTE]
> 이 섹션에는 f i g 변환 환경 표시기를 설정 하는 방법을 보여 줍니다. 표시기가 있는 때문에 `<appSettings>` 요소를 Azure 앱 서비스에 배포 하는 경우 변환 지정 하기 위한 또 다른 방법은 있어야 합니다. 자세한 내용은 참조 [Azure에서 지정 하는 Web.config 설정을](web-config-transformations.md#watransforms)합니다.


1. **솔루션 탐색기**, 확장 **속성**을 펼친 다음 **PublishProfiles**합니다.
2. 마우스 오른쪽 단추로 클릭 *Staging.pubxml*, 클릭 하 고 **Config 변환 추가**합니다.

    ![준비 단계에 대 한 구성 변환 추가](deploying-to-production/_static/image11.png)

    Visual Studio 만듭니다는 *Web.Staging.config* 변환 파일을 엽니다.
3. 에 *Web.Staging.config* 변환 파일을 여는 바로 뒤에 다음 코드를 삽입 `configuration` 태그입니다.

    [!code-xml[Main](deploying-to-production/samples/sample1.xml)]

    준비 게시 프로필을 사용 하 여이 변환 환경 표시기 "Prod"를 설정 합니다. 배포 된 웹 응용 프로그램에서 "Contoso 대학" H1 제목을 후 "(테스트)" 또는 "(Dev)"와 같은 모든 접미사를 볼 수 있습니다.
4. 마우스 오른쪽 단추로 클릭는 *Web.Staging.config* 파일을 클릭 하 여 **미리 보기 변환** 코딩 변환 된 예상된 변경 내용이 생성 되도록 합니다.

    **Web.config 미리 보기** 창 모두에 적용 한 결과 표시는 *Web.Release.config* 변환 및 *Web.Staging.config* 변환 합니다.

### <a name="prevent-public-use-of-the-test-app"></a>테스트 응용 프로그램의 공용 사용을 방지

준비 앱에 대 한 중요 한 고려는 것은 인터넷에서 사용 중인 있지만 사용을 공개 하지 않으려면입니다. 사용자를 찾을 사용 하는 가능성을 최소화 하려면 다음 방법 중 하나 이상을 사용할 수 있습니다.

- 준비 테스트를 사용 하는 IP 주소 에서만에서 준비 응용 프로그램에 대 한 액세스를 허용 하는 방화벽 규칙을 설정 합니다.
- 추측할 수 될 난독 처리 된 URL을 사용 합니다.
- 만들기는 *robots.txt* 파일에는 검색 엔진을 크롤링하지 것입니다 테스트 응용 프로그램 및 보고서 링크를 검색 결과에 있습니다.

이러한 메서드의 첫 번째 가장 효과적 이지만 Azure 앱 서비스 하는 대신 Azure 클라우드 서비스를 배포 하는 것이 해야 하므로이 자습서에서 다루지 않습니다. 클라우드 서비스에 대 한 자세한 내용 및 Azure에서 IP 제한을 참조 [계산 호스팅 옵션 Azure에서 제공](https://docs.microsoft.com/azure/cloud-services/cloud-services-choose-me) 및 [웹 역할에 액세스 하지 못하도록 하는 특정 IP 주소 블록](https://msdn.microsoft.com/library/windowsazure/jj154098.aspx)합니다. 제 3 자 호스팅 공급자에 게 배포 하는 경우 IP 제한을 구현 하는 방법을 알아보려면 공급자에 게 문의 합니다.

이 자습서에서는 만듭니다는 *robots.txt* 파일입니다.

1. **솔루션 탐색기**ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **새 항목 추가**합니다.
2. 새 **텍스트 파일** 라는 *robots.txt*, 여기에 다음 텍스트를 넣 및:

    [!code-console[Main](deploying-to-production/samples/sample2.cmd)]

    `User-agent` 줄 지시 파일의 규칙은 모든 검색 엔진 웹 크롤러에 (로봇)에 적용 되는 검색 엔진 및 `Disallow` 줄 사이트 페이지가 해야 크롤링할 수를 지정 합니다.

    프로덕션 배포에서이 파일을 제외 해야 하므로 프로덕션 응용 프로그램 카탈로그를 검색 엔진 않을 수 있습니다. 구성, 작업을 수행 하는 프로덕션 환경에서 설정을 게시 프로필을 만들 때.

### <a name="deploy-to-staging"></a>스테이징 배포

1. 열기는 **웹 게시** Contoso 대학 프로젝트를 마우스 오른쪽 단추로 클릭 하 여 마법사 **게시**합니다.
2. 다음 사항을 확인는 **준비** 프로 파일을 선택 합니다.
3. **게시**를 클릭합니다.

    **출력** 창 수행 된 배포 작업을 표시 및 배포를 성공적으로 완료를 보고 합니다. 배포 된 웹 응용 프로그램의 URL에 기본 브라우저가 자동으로 열립니다.

## <a name="test-in-the-staging-environment"></a>스테이징 환경에서 테스트

환경 표시기가 있는지 확인 ("(테스트가)" 또는 "(Dev)"를 보여 주는 H1 제목을 후는 *Web.config* 환경 표시기에 대 한 변환을 성공적으로 수행 합니다.

![홈 페이지 준비](deploying-to-production/_static/image12.png)

실행 된 **학생** 페이지는 배포 된 데이터베이스에 없는 학생에 있는지 확인 합니다.

실행 된 **강사** 페이지 Code First 있는지 instructor 데이터로 데이터베이스 시드 된 확인:

선택 **추가 학생** 에서 **학생** 메뉴는 학생을 추가 하 고 다음에 새 학생을 볼는 **학생** 페이지는 데이터베이스에 성공적으로 쓸 수 있는지 확인 합니다. .

**Courses** 페이지 **업데이트 크레딧**합니다. **업데이트 크레딧** 페이지에는 관리자 권한이 필요 하므로 **로그인** 페이지가 표시 됩니다. 이전 버전 ("admin" 및 "prodpwd")를 만든 관리자 계정 자격 증명을 입력 합니다. **업데이트 크레딧** 이전 자습서에서 만든 관리자 계정을 테스트 환경에 잘못 배포 된 검증 페이지가 표시 됩니다.

ELMAH 추적 되며 다음 ELMAH 오류 보고서를 요청 하면 오류가 발생 하 여 잘못 된 URL을 요청 합니다. 제 3 자 호스팅 공급자에 게 배포 하는 경우 보면 개발한 되기 이전 자습서에서 빈 보고서가 비어 있습니다. ELMAH 로그 폴더에 쓸 수 있도록 폴더 사용 권한을 구성 하는 호스팅 공급자 계정 관리 도구를 사용 해야 합니다.

만든 응용 프로그램은 프로덕션 환경에 사용 됩니다 하는 것과 같은 웹 앱의 경우 클라우드에서 실행 됩니다. 모든 기능이 올바르게 작동 하므로 다음 단계에서는 프로덕션 환경에 배포 하는 것입니다.

## <a name="deploy-to-production"></a>프로덕션 환경에 배포

제외 제외 해야 하 고 프로덕션 웹 앱을 만들고 프로덕션에 배포 하기 위한 프로세스는 스테이징 구문과 동일는 *robots.txt* 배포에서 합니다. 이렇게 하기 위해 게시 프로필 파일을 편집 합니다.

### <a name="create-the-production-environment-and-the-production-publish-profile"></a>프로덕션 환경을 만들고 프로덕션 게시 프로필

1. 스테이징에 사용 하는 동일한 절차를 수행 하는 Azure에서 프로덕션 웹 앱 및 데이터베이스를 만듭니다.

    데이터베이스를 만들 때 앞에서 만든 동일한 서버에 전송 하도록 선택할 하거나 새 서버를 만들 수 있습니다.
2. 다운로드는 *.publishsettings* 파일입니다.
3. 프로덕션 가져와 게시 프로필을 만들 *.publishsettings* 파일을 스테이징에 사용 하는 동일한 절차를 수행 합니다.

    데이터 배포 스크립트에서 구성에 반드시 **DefaultConnection** 에 **데이터베이스** 의 섹션은 **설정** 탭 합니다.
4. 게시 프로필의 이름 바꾸기 *프로덕션*합니다.
5. 스테이징에 사용 하는 동일한 절차를 수행 하는 환경 표시기에 대 한 게시 프로필 변환을 구성...

### <a name="edit-the-pubxml-file-to-exclude-robotstxt"></a>제외할 robots.txt.pubxml 파일 편집

게시 프로필 파일의 이름은 &lt;profilename&gt;*.pubxml* 에 살고 있는 및은 *PublishProfiles* 폴더입니다. *PublishProfiles* 폴더는는 *속성* 폴더는 C# 웹 응용 프로그램의 프로젝트는 *My Project* 폴더 또는 VB 웹 응용 프로그램 프로젝트에는 *앱\_데이터* 웹 응용 프로그램 프로젝트의 폴더에에서 있습니다. 각 *.pubxml* 파일 하나에 적용 되는 설정이 포함 게시 프로필. 웹 게시 마법사에서 입력 값이이 파일에 저장 됩니다 및 Visual Studio UI에서 사용할 수 없는 설정을 만들거나 변경 하도록 편집할 수 있습니다.

기본적으로 *.pubxml* 파일은 프로젝트에서 제외할 수 있습니다를 Visual Studio는 이러한 사용할 수 있지만 게시 프로필을 만들 때 프로젝트에 포함 됩니다. Visual Studio에서 찾습니다는 *PublishProfiles* 폴더에 대 한 *.pubxml* 파일을 프로젝트에 포함 되어 있는지에 관계 없이 합니다.

각 *.pubxml* 는 파일을 *. pubxml.user* 파일입니다. *. pubxml.user* 파일을 선택한 경우 암호화 된 암호가 들어는 **암호 저장** 옵션을은 프로젝트에서 제외 되는 기본적으로 합니다.

A *.pubxml* 파일에 특정 게시 프로필 관련 설정이 포함 됩니다. 모든 프로필에 적용 하는 설정을 구성 하려는 경우 만들 수 있습니다는 *. wpp.targets* 파일입니다. 빌드 프로세스에 이러한 파일을 가져오는 *.csproj* 또는 *.vbproj* 프로젝트 파일, 프로젝트 파일에서 구성할 수 있는 대부분의 설정을이 파일에서 구성할 수 있습니다. 에 대 한 자세한 내용은 *.pubxml* 파일 및 *. wpp.targets* 파일, 참조 [하는 방법: 게시 프로 파일 (.pubxml) 파일에서 배포 설정 편집 및. wpp.targets Visual Studio에서 파일 웹 프로젝트](https://msdn.microsoft.com/library/ff398069.aspx)합니다.

1. **솔루션 탐색기**를 확장 하 고 **속성** 확장 **PublishProfiles**합니다.
2. 마우스 오른쪽 단추로 클릭 *Production.pubxml* 클릭 **열려**합니다.

    ![.Pubxml 파일 열기](deploying-to-production/_static/image13.png)
3. 마우스 오른쪽 단추로 클릭 *Production.pubxml* 클릭 **열려**합니다.
4. 닫는 바로 앞에 다음 줄 추가 `PropertyGroup` 요소:

    [!code-xml[Main](deploying-to-production/samples/sample3.xml)]

    .Pubxml 파일은 이제 다음과 같이 표시 됩니다.

    [!code-xml[Main](deploying-to-production/samples/sample4.xml?highlight=18-20)]

    파일 및 폴더를 제외 하는 방법에 대 한 자세한 내용은 참조 [수 나타나지 않게 특정 파일 또는 폴더 배포에서?](https://msdn.microsoft.com/library/ee942158.aspx#can_i_exclude_specific_files_or_folders_from_deployment) 에 **Visual Studio 및 ASP.NET에 대 한 웹 배포 FAQ** msdn 합니다.

### <a name="deploy-to-production"></a>프로덕션 환경에 배포

1. 열기는 **웹 게시** 마법사 확인는 **프로덕션** 게시 프로필을 선택한 다음 클릭 **미리 보기 시작** 에 **미리보기**탭 되었는지 확인 하 고 *robots.txt* 파일 프로덕션 앱으로 복사 되지 것입니다.

    ![프로덕션 환경에 게시 하는 파일의 미리 보기](deploying-to-production/_static/image14.png)

    복사할 파일의 목록을 검토 합니다. 표시 됩니다 모든는 *.cs* 파일을 포함 하 여 *. aspx.cs*, *. aspx.designer.cs*, *Master.cs*, 및  *Master.designer.cs* 파일 생략 됩니다. 로 컴파일 되었으면 모든이 코드는 *ContosoUniversity.dll* 및 *ContosUniversity.pdb* 에 나와 있는 파일의 *bin* 폴더입니다. 때문에는 *.dll* 하는 데 필요한 응용 프로그램에서 이전에 지정한 응용 프로그램을 실행 하는 데 필요한 파일만 배포 해야 하는 실행, no *.cs* 파일이 대상에 복사 되었으므로 환경입니다. *obj* 폴더 및 *ContosoUniversity.csproj* 및 *. csproj.user* 파일 같은 이유로 생략 됩니다.

    클릭 **게시** 프로덕션 환경에 배포할 수 있습니다.
2. 스테이징에 사용 되는 동일한 절차를 수행 하는 프로덕션 환경에서 테스트 합니다.

    모든 항목은 URL 제외 하 고 준비 하 고 없는 경우와 동일는 *robots.txt* 파일입니다.

## <a name="summary"></a>요약

이제 성공적으로 배포 및 웹 앱을 테스트 되며 사용할 수 있는 공개적으로 인터넷을 통해 있습니다.

![홈 페이지 프로덕션](deploying-to-production/_static/image15.png)

다음 자습서에서는 응용 프로그램 코드를 업데이트 하 고 변경 내용을 테스트, 스테이징 및 프로덕션 환경에 배포 합니다.

> [!NOTE]
> 응용 프로그램은 프로덕션 환경에서 사용 중인 동안 복구 계획을 구현 해야 합니다. 즉, 있습니다 해야 정기적으로 백업 데이터베이스를 프로덕션 앱에서 보안 저장소 위치를 하 고 몇 가지 세대의 이러한 백업 유지 해야 합니다. 데이터베이스를 업데이트할 때 변경 직전의 백업 복사본을 확인 해야 합니다. 그런 다음 실수 하 고 프로덕션 환경에 배포한 후 때까지 검색 하지 않는 경우에 데이터베이스를 손상 되기 전의 상태로 복구할 수 계속 합니다. 자세한 내용은 참조 [Azure SQL 데이터베이스 백업 및 복원](https://msdn.microsoft.com/library/windowsazure/jj650016.aspx)합니다.
> 
> 
> [!NOTE]
> 이 자습서는 SQL Server에 배포 하는 버전은 Azure SQL 데이터베이스입니다. 배포 과정은 다른 버전의 SQL Server 비슷합니다를 실제 프로덕션 응용 프로그램은 일부 시나리오에서 특수 한 코드를 Azure SQL 데이터베이스에 대 한 필요할 수 있습니다. 자세한 내용은 참조 [Azure SQL 데이터베이스 작업을](../../../../whitepapers/aspnet-data-access-content-map.md#ssdb) 및 [SQL Server 및 Azure SQL 데이터베이스 중에서 선택](../../../../whitepapers/aspnet-data-access-content-map.md#ssdbchoosing)합니다.
> 
> [!div class="step-by-step"]
> [이전](setting-folder-permissions.md)
> [다음](deploying-a-code-update.md)
