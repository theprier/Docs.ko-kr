---
uid: identity/overview/migrations/migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity
title: 멤버 자격 및 ASP.NET Identity (C#)에 사용자 프로필에 대 한 유니버설 공급자 데이터 마이그레이션 | Microsoft Docs
author: rustd
description: 이 자습서에서는 사용자와 역할 데이터는 기존 응용 프로그램의 Universal Providers를 사용 하 여 만든 사용자 프로필 데이터를 마이그레이션하는 데 필요한 단계를 설명...
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/13/2013
ms.topic: article
ms.assetid: 2e260430-d13c-4658-bd05-e256fc0d63b8
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /identity/overview/migrations/migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 75d273d9fdb5d8ff0f7a910f42abe8bcce6e397d
ms.sourcegitcommit: e22097b84d26a812cd1380a6b2d12c93e522c125
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/22/2018
ms.locfileid: "36314002"
---
<a name="migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity-c"></a>멤버 자격 및 ASP.NET Identity (C#)에 사용자 프로필에 대 한 유니버설 공급자 데이터 마이그레이션
====================
여 [Pranav Rastogi](https://github.com/rustd), [Rick Anderson](https://github.com/Rick-Anderson), [Robert McMurray](https://github.com/rmcmurray), [Suhas Joshi](https://github.com/suhasj)

> 이 자습서에서는 사용자 역할 데이터 및 ASP.NET Id 모델에는 기존 응용 프로그램의 Universal Providers를 사용 하 여 만든 사용자 프로필 데이터를 마이그레이션하는 데 필요한 단계를 설명 합니다. 접근 방식 여기에 언급 된 사용자 프로필 데이터를 마이그레이션하 SQL 멤버 자격도 응용 프로그램에서 사용할 수 있습니다.


Visual Studio 2013의 릴리스로 ASP.NET 팀 새 ASP.NET Identity 시스템을 도입 되었으며 읽어볼 수 있는 해당 버전에 대 한 [여기](../../index.md)합니다. 웹 응용 프로그램을 마이그레이션할 문서 이후의 [새 Id 시스템에 SQL 멤버 자격](migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md),이 문서를 사용자 및 역할 관리를 위한 공급자 모델을 따르는 기존 응용 프로그램을 마이그레이션하는 단계를 보여 줍니다. 에 새 Id 모델입니다. 이 자습서의 초점은 새 시스템으로 원활 하 게 연결 하는 사용자 프로필 데이터를 마이그레이션한에서 주로 됩니다. 사용자 및 역할에 대 한 마이그레이션 정보는 SQL 멤버 자격에 대 한 유사 합니다. 응용 프로그램에서 SQL 멤버 자격도와 프로필 데이터를 마이그레이션할 접근 방식을 사용할 수 있습니다.

예를 들어, 우리는 공급자 모델을 사용 하는 Visual Studio 2012를 사용 하 여 만든 웹 응용 프로그램으로 시작 됩니다. 그런 다음 프로필 관리에 대 한 코드를 추가, 사용자 등록, 사용자에 대 한 프로필 데이터를 추가, 데이터베이스 스키마를 마이그레이션하려면 알아보고 하겠습니다 사용자 및 역할 관리에 대 한 Id 시스템을 사용 하도록 응용 프로그램을 변경 합니다. 마이그레이션 테스트로 Universal Providers를 사용 하 여 만든 사용자가 로그인 할 수 있어야 합니다. 및 새 사용자가 등록할 수 있어야 합니다.

> [!NOTE]
> 전체 샘플을 찾을 수 있습니다 [ https://github.com/suhasj/UniversalProviders-Identity-Migrations ](https://github.com/suhasj/UniversalProviders-Identity-Migrations)합니다.


## <a name="profile-data-migration-summary"></a>프로필 데이터 마이그레이션 요약

마이그레이션을 시작 하기 전에 주세요 공급자 모델에 프로필 데이터를 저장 하는 환경을 살펴봅니다. 여러 가지 방법으로 사용자가 저장할 수는 응용 프로그램에 대 한 프로필 데이터를에서 그 중 가장 일반적인 되 고 사용 하 여 기본 제공 된 프로필 공급자 유니버설 공급자와 함께 제공 합니다. 이 단계는 같습니다.

1. 프로필 데이터를 저장 하는 데 사용 되는 속성을 가진 클래스를 추가 합니다.
2. 'ProfileBase'를 확장 하 고 사용자에 대 한 위의 프로필 데이터를 가져오려는 메서드를 구현 하는 클래스를 추가 합니다.
3. 기본 프로필 공급자를 사용 하 여 사용 하도록 설정 된 *web.config* 파일을 2 프로필 정보에 액세스 하는 데 사용할 단계에서 선언 된 클래스를 정의 합니다.

프로필 정보 serialize 된 xml 및 이진 데이터는 데이터베이스의 '프로필' 테이블에 저장 됩니다.

새 ASP.NET Id 시스템을 사용 하도록 응용 프로그램으로 마이그레이션한 후 프로필 정보 deserialize 및 사용자 클래스에 속성으로 저장 합니다. 그런 다음 사용자 테이블의 열에 각 속성을 매핑할 수 있습니다. 여기서 이점은 속성 여 데이터 정보를 직렬화/역직렬화 필요가 없다는 것 외에도 사용자 클래스를 사용 하 여 직접에 수행 관점에서 볼 때 시간입니다.

## <a name="getting-started"></a>시작

1. Visual Studio 2012에서 새 ASP.NET 4.5 Web Forms 응용 프로그램을 만듭니다. 현재이 샘플에서는 Web Forms 서식 파일을 사용 하지만 MVC 응용 프로그램에도 사용할 수 있습니다.  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image1.jpg)
2. '모델' 프로필 정보를 저장할 새 폴더 만들기  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image1.png)
3. 예를 들어 프로필에 생년월일, city, 높이 및 사용자의 가중치의 날짜를 저장할 알려 주세요. 높이 두께로 'PersonalStats' 라는 사용자 지정 클래스도 저장 됩니다. 저장 하 고 프로필을 검색, 'ProfileBase'를 확장 하는 클래스가 필요 합니다. 'AppProfile' 가져오고 프로필 정보를 저장 하는 새 클래스를 만들어 보겠습니다.

    [!code-csharp[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample1.cs)]
4. 프로필을 사용 하도록 설정 된 *web.config* 파일입니다. 3 단계에서 만든 사용자 정보를 저장/검색 하는 데 사용할 클래스 이름을 입력 합니다.

    [!code-xml[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample2.xml)]
5. Web forms 페이지에서 사용자 프로필 데이터를 가져오고 저장 'Account' 폴더에 추가 합니다. 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 새 항목 추가를 선택 합니다. 마스터 페이지 'AddProfileData.aspx'와 새 webforms 페이지를 추가 합니다. 'MainContent' 섹션에서 다음을 복사 합니다.

    [!code-html[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample3.html)]

   코드 숨김에 다음 코드를 추가 합니다.

    [!code-csharp[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample4.cs)]

   컴파일 오류를 제거 하는 AppProfile에서 클래스가 정의 된 네임 스페이스를 추가 합니다.
6. 응용 프로그램을 실행 하 고 사용자 이름을 가진 새 사용자를 만들려면 '**olduser'.** 'AddProfileData' 페이지로 이동한 다음 사용자에 대 한 프로필 정보를 추가 합니다.  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image2.png)

서버 탐색기 창을 사용 하 여 '프로필' 테이블에서 직렬화 된 xml로는 데이터가 저장 되어 있는지 확인할 수 있습니다. Visual Studio에서 [보기] 메뉴에서 ' 서버 탐색기 '를 선택 합니다. 데이터 연결에 정의 된 데이터베이스에 대 한 있어야는 *web.config* 파일입니다. 데이터 연결 클릭 하면 서로 다른 하위 범주를 표시 합니다. 확장 '테이블' 프로그램 데이터베이스의 여러 테이블을 표시 한 다음 '프로필' 마우스 오른쪽 단추로 클릭 하 고 프로필 테이블에 저장 된 프로필 데이터를 보려면 ' 테이블 데이터 표시 '를 선택 합니다.

![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image3.png)

![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image4.png)

## <a name="migrating-database-schema"></a>데이터베이스 스키마 마이그레이션

Id 시스템을 사용 하는 기존 데이터베이스를 원래 데이터베이스에 추가한 필드를 지원 하도록 Id 데이터베이스에서 스키마를 업데이트 해야 합니다. 이렇게 하려면 SQL 스크립트를 사용 하 여 새 테이블을 만들고 기존 정보를 복사 합니다. ' 서버 탐색기 ' 창의 'DefaultConnection' 테이블을 표시 하려면 확장 합니다. 테이블을 마우스 오른쪽 단추로 클릭 하 고 새 쿼리를 선택 합니다.

![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image5.png)

SQL 스크립트를 붙여 [ https://raw.github.com/suhasj/UniversalProviders-Identity-Migrations/master/Migration.txt ](https://raw.github.com/suhasj/UniversalProviders-Identity-Migrations/master/Migration.txt) 하 고 실행 합니다. 'DefaultConnection' 새로 고치면 새 테이블이 추가 되는 표시 됩니다. 정보 마이그레이션 되었는지 확인 하려면 테이블에 있는 데이터를 확인할 수 있습니다.

![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image6.png)

## <a name="migrating-the-application-to-use-aspnet-identity"></a>ASP.NET Id를 사용 하 여 응용 프로그램 마이그레이션

1. ASP.NET Id에 필요한 Nuget 패키지를 설치 합니다.

    - Microsoft.AspNet.Identity.EntityFramework
    - Microsoft.AspNet.Identity.Owin
    - Microsoft.Owin.Host.SystemWeb
    - Microsoft.Owin.Security.Facebook
    - Microsoft.Owin.Security.Google
    - Microsoft.Owin.Security.MicrosoftAccount
    - Microsoft.Owin.Security.Twitter

   Nuget 패키지 관리에 대 한 자세한 내용은 있습니다 [여기](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog)
2. 테이블의 기존 데이터를 사용 하려면 테이블에 다시 매핑할 및 Id 시스템에 연결 하는 모델 클래스를 만들어야 할 합니다. Identity 계약의 일부로 모델 클래스 Identity.Core dll에 정의 된 인터페이스를 구현 해야 하거나 또는 Microsoft.AspNet.Identity.EntityFramework에서 사용할 수 있는 이러한 인터페이스의 기존 구현을 확장할 수 있습니다. 역할, 사용자 로그인 및 사용자 클레임에 대 한 기존 클래스 사용 합니다. 이 샘플에 대 한 사용자 지정 사용자를 사용 해야 합니다. 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 'IdentityModels' 폴더를 새로 만듭니다. 아래와 같이 새 'User' 클래스를 추가 합니다.

    [!code-csharp[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample5.cs)]

   이제 'ProfileInfo' 사용자 클래스에서 속성 인지 확인 합니다. 따라서 프로필 데이터로 직접 작업 하는 사용자 클래스를 사용할 수 있습니다.

파일 복사는 **IdentityModels** 및 **IdentityAccount** 다운로드 원본의 폴더 ( [ https://github.com/suhasj/UniversalProviders-Identity-Migrations/tree/master/UniversalProviders-Identity-Migrations ](https://github.com/suhasj/UniversalProviders-Identity-Migrations/tree/master/UniversalProviders-Identity-Migrations) ). 이러한 남은 모델 클래스 및 사용자와 ASP.NET Identity Api를 사용 하 여 역할 관리에 필요한 새 페이지가 포함 됩니다. 사용 하는 방법 SQL 멤버 자격에 비슷합니다. 자세한 설명은 수 있으며 [여기](migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md)합니다.

[!INCLUDE[](../../../includes/identity/alter-command-exception.md)]

## <a name="copying-profile-data-to-the-new-tables"></a>프로필 데이터를 새 테이블에 복사

앞서 언급 했 듯이 프로필 테이블에 xml 데이터를 역직렬화 하 고 AspNetUsers 테이블의 열에 저장 해야 합니다. 새 열에 필요한 데이터와 해당 열을 채우기 위해 즉 이므로 이전 단계에서 사용자 테이블에서 만들었습니다. 이 수행 하려면 사용자가 테이블의 새로 만든된 열을 채우기 위해 한 번 실행 되는 콘솔 응용 프로그램을 사용 합니다.

1. 기존 솔루션에 새 콘솔 응용 프로그램을 만듭니다.  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image2.jpg)
2. Entity Framework 패키지의 최신 버전을 설치 합니다.
3. 콘솔 응용 프로그램에 대 한 참조로 위에서 만든 웹 응용 프로그램을 추가 합니다. 프로젝트에 대해 클릭 마우스 오른쪽 단추로이 작업을 수행 하 한 다음 ' 참조 추가 '를 다음 솔루션 다음 프로젝트를 클릭 하 고 확인을 클릭 합니다.
4. 복사는 아래 코드는 Program.cs 클래스에 있습니다. 이 논리는 각 사용자에 대 한 프로필 데이터를 읽는 하 고 'ProfileInfo' 개체로 직렬화 및 다시 데이터베이스에 저장 합니다.

    [!code-csharp[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample6.cs)]

   해당 네임 스페이스를 포함 해야 하므로 사용 하는 모델 중 일부는 웹 응용 프로그램 프로젝트의 'IdentityModels' 폴더에 정의 됩니다.
5. 위의 코드는 응용 프로그램에서 데이터베이스 파일에 적용\_이전 단계에서 만든 웹 응용 프로그램 프로젝트의 데이터 폴더. 참조 하는 웹 응용 프로그램의 web.config에서 연결 문자열과 함께 콘솔 응용 프로그램의 app.config 파일에서 연결 문자열을 업데이트 합니다. 또한 'AttachDbFilename' 속성에 전체 실제 경로 제공 합니다.
6. 명령 프롬프트를 열고 위의 콘솔 응용 프로그램의 bin 폴더를 이동 합니다. 실행 파일을 실행 하 고 다음 그림에 나와 있는 것 처럼 로그 출력을 검토 합니다.  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image3.jpg)
7. 서버 탐색기에서 'AspNetUsers' 테이블을 열고 속성을 보유 하는 새 열에 데이터를 확인 합니다. 해당 속성 값으로 업데이트 해야 합니다.

## <a name="verify-functionality"></a>기능 확인

ASP.NET Id를 사용 하 여 기존 데이터베이스에서 사용자 로그인 구현 되는 새로 추가 된 멤버 자격 페이지를 사용 합니다. 사용자는 동일한 자격 증명을 사용 하 여 로그인 할 수 있어야 합니다. 사용자 역할 등에 추가할 추가 OAuth, 암호를 변경 하는 새 사용자 만들기 역할을 추가 하는 등 다른 기능을 시도 하십시오.

기존 사용자 및 새 사용자에 대 한 프로필 데이터를 검색 하 고 사용자가 테이블에 저장 해야 합니다. 이전 테이블은 더 이상 참조할 수 없습니다.

## <a name="conclusion"></a>결론

문서는 ASP.NET Identity에 멤버 자격에 대 한 공급자 모델을 사용 하는 웹 응용 프로그램 마이그레이션 프로세스를 설명 합니다. 또한 문서 Id 시스템을 후크 될 사용자에 대 한 프로필 데이터를 마이그레이션하는 테두리가 표시. 아래 질문 및 응용 프로그램을 마이그레이션하는 경우 발생 하는 문제에 대 한 의견을 남겨 주세요.

*문서를 검토 하기 위한 Rick Anderson 및 Robert McMurray 가져주셔서 감사 합니다.*
