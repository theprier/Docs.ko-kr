---
uid: web-forms/overview/moving-to-aspnet-20/profiles-themes-and-web-parts
title: 프로필, 테마 및 웹 파트 | Microsoft Docs
author: microsoft
description: 구성의 주요 변경 사항 및 ASP.NET 2.0의 계측 됩니다. 새 ASP.NET 구성 API 구성 변경 하려면 프로젝트를 만들 수 있습니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2005
ms.topic: article
ms.assetid: 92df4051-77c6-492c-bd34-23d24189cea4
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/profiles-themes-and-web-parts
msc.type: authoredcontent
ms.openlocfilehash: b749ed093fbaacf45b60f2826a2c20bac219a5c7
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30892116"
---
<a name="profiles-themes-and-web-parts"></a>프로필, 테마 및 웹 파트
====================
by [Microsoft](https://github.com/microsoft)

> 구성의 주요 변경 사항 및 ASP.NET 2.0의 계측 됩니다. 새 ASP.NET 구성 API 구성 변경 내용을 프로그래밍 방식으로 만들 수 있습니다. 또한 다양 한 새 구성 설정을 존재 새 구성 및 계측을 허용 합니다.


ASP.NET 2.0 개인 설정 된 웹 사이트의 영역에서 향상을 나타냅니다. 이미 멤버 자격 기능 마십시오, 외에도 ASP.NET 프로필, 테마 및 웹 파트 대폭 향상 시킬 웹 사이트에서 개인 설정 합니다.

## <a name="aspnet-profiles"></a>ASP.NET 프로필

ASP.NET 프로필 세션와 비슷합니다. 차이점은 프로필은 영구 브라우저를 닫을 때 세션에는 손실 됩니다. 또 다른 큰 차이점 세션 및 프로필은 프로필은 강력한 형식입니다, 따라서 개발 프로세스 중 IntelliSense와 함께 제공 합니다.

프로필은 컴퓨터 구성 파일 또는 응용 프로그램에 대 한 web.config 파일에 정의 됩니다. (하위 폴더 web.config 파일에 프로필을 정의할 수 없습니다.) 아래 코드를 저장 하는 웹 사이트 방문자 먼저 고 성 프로필을 정의 합니다.

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample1.xml)]

프로필 속성에 대 한 기본 데이터 형식은 System.String입니다. 위의 예에 없는 데이터 형식이 지정 되었습니다. 따라서 FirstName 및 LastName 속성은 String 형식 둘 다. 앞에서 언급 한 프로필 속성은 강력한 형식입니다. 아래 코드 사용 기간을 Int32 형식에 대 한 새 속성을 추가 합니다.

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample2.xml)]

프로필은 일반적으로 ASP.NET 폼 인증으로 사용 됩니다. 각 사용자가 해당 사용자 ID와 연결 된 별도 프로필을 조합 하 여 폼 인증 사용 그러나 것도 가능 사용 하 여 익명 응용 프로그램 프로필을 사용할 수 있도록는 &lt;anonymousIdentification&gt; 와 함께 구성 파일의 요소는 **allowAnonymous** 특성은 다음과 같습니다.

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample3.xml)]

ASP.NET의 인스턴스를 만들고 익명 사용자가 해당 사이트를 찾아볼 때 **ProfileCommon** 사용자에 대 한 합니다. 이 프로필 고유 방문자로 사용자를 식별 하는 브라우저에서 쿠키에 저장 하는 고유한 ID를 사용 합니다. 이러한 방식으로 사용자에 게 익명으로 이동 하는 프로필 정보를 저장할 수 있습니다.

## <a name="profile-groups"></a>프로필 그룹

프로필의 그룹 속성을 두는 것이 불가능 합니다. 그룹화 속성으로 특정 응용 프로그램에 대 한 여러 프로필을 시뮬레이션 하는 것이 같습니다.

다음 구성에서는 FirstName 및 LastName의 속성을 두 그룹;를 구성합니다 구매자 및 잠재 고객 합니다.

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample4.xml)]

다음과 같이 특정 그룹에 속성을 설정할 수는 다음:

[!code-csharp[Main](profiles-themes-and-web-parts/samples/sample5.cs)]

## <a name="storing-complex-objects"></a>복잡 한 개체를 저장합니다.

지금까지 설명한 예에서는 단순 데이터 유형 프로필에 저장 합니다. 직렬화를 사용 하 여의 방법을 지정 하 여 프로필에 복잡 한 데이터 형식을 저장할 수 이기도 **serializeAs** 특성을 다음과 같이 합니다.

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample6.xml)]

이 경우 형식은 PurchaseInvoice입니다. PurchaseInvoice 클래스 serializable로 표시 되어야 하며 다양 한 속성이 포함 될 수 있습니다. 예를 들어 PurchaseInvoice 라는 속성이 **NumItemsPurchased**를 다음과 같이 코드에서 해당 속성을 참조할 수 있습니다.

[!code-css[Main](profiles-themes-and-web-parts/samples/sample7.css)]

## <a name="profile-inheritance"></a>프로필 상속

여러 응용 프로그램에서 사용 하기 위해 프로필을 만드는 것 같습니다. ProfileBase에서 파생 되는 프로필 클래스를 만들면 다시 사용할 수 있습니다는 여러 응용 프로그램에서 프로필을 사용 하 여는 **상속** 아래와 같이 특성:

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample8.xml)]

이 경우 클래스 **PurchasingProfile** 유사할 것 같이:

[!code-csharp[Main](profiles-themes-and-web-parts/samples/sample9.cs)]

## <a name="profile-providers"></a>프로필 공급자

ASP.NET 프로필 공급자 모델을 사용합니다. 앱에서 SQL Server Express 데이터베이스에 있는 정보를 저장 하는 기본 공급자\_SqlProfileProvider 공급자를 사용 하는 웹 응용 프로그램 데이터 폴더. 데이터베이스가 존재 하지 않는 경우 ASP.NET을 자동으로 만듭니다 프로필 정보를 저장 하려고 할 때.

그러나 경우에 따라 좋습니다 프로필 공급자를 개발 하 합니다. ASP.NET 프로필 기능을 사용 하면 쉽게 다른 공급자를 사용할 수 있습니다.

사용자 지정 프로필 공급자를 만들 때:

- .NET Framework에 포함 된 프로필 공급자에서 지원 되지 않는 FoxPro 데이터베이스 또는 Oracle 데이터베이스와 같은 데이터 원본에 프로필 정보를 저장 해야 합니다.
- .NET Framework에 포함 된 공급자가 사용 되는 데이터베이스 스키마와에서는 다른 데이터베이스 스키마를 사용 하 여 프로필 정보를 관리 해야 합니다. 기존 SQL Server 데이터베이스의 사용자 데이터와 함께 프로필 정보를 통합 하려면 한 일반적인 예가입니다.

### <a name="required-classes"></a>필요한 클래스

프로필 공급자를 구현 하려면 System.Web.Profile.ProfileProvider 추상 클래스를 상속 하는 클래스를 만듭니다. **ProfileProvider** 추상 클래스 상속 System.Configuration.SettingsProvider System.Configuration.Provider.ProviderBase 추상 클래스를 상속 하는 추상 클래스입니다. 필수 멤버 외에도이 상속 체인으로 인해는 **ProfileProvider** 클래스의 필수 멤버를 구현 해야 합니다는 **SettingsProvider** 및  **ProviderBase** 클래스입니다.

다음 표에서 설명에서 구현 해야 하는 메서드와 속성은 **ProviderBase**, **SettingsProvider**, 및 **ProfileProvider** 추상 클래스입니다.

### <a name="providerbase-members"></a>ProviderBase 멤버

| **멤버** | **설명** |
| --- | --- |
| Initialize 메서드 | 공급자 인스턴스의 이름 및 구성 설정의 NameValueCollection 입력으로 사용 합니다. 속성 값 구현 별 값 및 컴퓨터 구성 파일 또는 Web.config 파일에 지정 된 옵션을 포함 하 여 공급자 인스턴스에 대 한 옵션을 설정 하는 데 사용 합니다. |

### <a name="settingsprovider-members"></a>SettingsProvider 멤버

| **멤버** | **설명** |
| --- | --- |
| ApplicationName 속성 | 각 프로필에 저장 하는 응용 프로그램 이름입니다. 프로필 공급자 응용 프로그램 이름을 사용 하 여 별도로 각 응용 프로그램에 대 한 프로필 정보를 저장 합니다. 그러면 동일한 사용자 이름이 생성 되는 다른 응용 프로그램에서 충돌 없이 동일한 데이터 원본을 사용 하려면 여러 ASP.NET 응용 프로그램. 또는 여러 ASP.NET 응용 프로그램은 동일한 응용 프로그램 이름을 지정 하 여 프로필 데이터 소스를 공유할 수 있습니다. |
| GetPropertyValues 메서드 | SettingsPropertyCollection 용이고 SettingsContext 입력 변수로 사용 합니다. **SettingsContext** 사용자에 대 한 정보를 제공 합니다. 사용자에 대 한 프로필 속성 정보를 검색 하는 기본 키로 정보를 사용할 수 있습니다. 사용 하 여는 **SettingsContext** 사용자 이름 및 인증 또는 익명 사용자가을 가져올 개체입니다. **SettingsPropertyCollection** SettingsProperty 개체의 컬렉션을 포함 합니다. 각 **SettingsProperty** 개체는 이름 및 속성 및 읽기 전용 속성 인지에 대 한 기본값 등의 추가 정보 뿐만 아니라 속성의 형식을 제공 합니다. **GetPropertyValues** 메서드 SettingsPropertyValue 개체를 기반으로 한 SettingsPropertyValueCollection 채웁니다는 **SettingsProperty** 입력으로 제공 하는 개체입니다. 지정된 된 사용자에 대 한 데이터 소스의 값 각각에 대해 PropertyValue 속성에 할당 된 **SettingsPropertyValue** 개체가 고 전체 컬렉션 반환 됩니다. 현재 날짜 및 시간에 지정 된 사용자 프로필에 대 한 LastActivityDate 값도 업데이트 메서드를 호출 합니다. |
| SetPropertyValues 메서드 | 입력으로 사용 된 **SettingsContext** 및 **SettingsPropertyValueCollection** 개체입니다. **SettingsContext** 사용자에 대 한 정보를 제공 합니다. 사용자에 대 한 프로필 속성 정보를 검색 하는 기본 키로 정보를 사용할 수 있습니다. 사용 하 여는 **SettingsContext** 사용자 이름 및 인증 또는 익명 사용자가을 가져올 개체입니다. **SettingsPropertyValueCollection** 의 컬렉션을 포함 **SettingsPropertyValue** 개체입니다. 각 **SettingsPropertyValue** 개체 이름, 형식 및 속성 및 읽기 전용 속성 인지에 대 한 기본값 등의 추가 정보 뿐만 아니라 속성의 값을 제공 합니다. **SetPropertyValues** 메서드는 지정된 된 사용자에 대 한 데이터 원본에 프로필 속성 값을 업데이트 합니다. 메서드를 호출 하면도 업데이트는 **LastActivityDate** 와 현재 날짜 및 시간에 지정 된 사용자 프로필에 대 한 LastUpdatedDate 값입니다. |

### <a name="profileprovider-members"></a>ProfileProvider 멤버

| **멤버** | **설명** |
| --- | --- |
| DeleteProfiles 메서드 | 일치 하는 응용 프로그램 이름이 문자열 배열 사용자의 이름을 지정 하 고 데이터 소스에서 지정 된 이름에 대 한 모든 프로필 정보 및 속성 값을 삭제 하는 입력으로 사용 된 **ApplicationName** 속성 값입니다. 데이터 원본 트랜잭션을 지원할 경우 트랜잭션을에 모든 삭제 작업을 포함 하 고 트랜잭션을 삭제 작업이 실패 하는 경우 예외를 throw 하는 것이 좋습니다. |
| DeleteProfiles 메서드 | 일치 하는 응용 프로그램 이름이 ProfileInfo의 컬렉션 개체 및 데이터 원본의 각 프로필에 대 한 모든 프로필 정보 및 속성 값을 삭제 하는 입력으로 사용 된 **ApplicationName** 속성 값입니다. 데이터 원본 트랜잭션을 지원할 경우 트랜잭션의 모든 삭제 작업을 포함 하 고 트랜잭션을 해 서 삭제 작업이 실패 하는 경우 예외를 throw 좋습니다. |
| DeleteInactiveProfiles 메서드 | ProfileAuthenticationOption 값을 입력으로 사용 및 DateTime 개체와 삭제 된 데이터에서 소스 모든 프로필 정보 및 마지막 작업 날짜 보다 작거나 지정 된 날짜 및 시간 고 모집단 속성 값이 응용 프로그램 이름 일치는 **ApplicationName** 속성 값입니다. **ProfileAuthenticationOption** 매개 변수는 익명 프로필 프로필에만 인증 되었는지 여부를 지정 된 모든 프로필에서 삭제할 또는 합니다. 데이터 원본 트랜잭션을 지원할 경우 트랜잭션의 모든 삭제 작업을 포함 하 고 트랜잭션을 해 서 삭제 작업이 실패 하는 경우 예외를 throw 좋습니다. |
| GetAllProfiles 메서드 | 입력으로 사용 된 **ProfileAuthenticationOption** 값, 페이지 인덱스를 지정 하는 정수, 페이지 크기와 프로필의 총 수로 설정 하는 정수에 대 한 참조를 지정 하는 정수입니다. 포함 된 ProfileInfoCollection 반환 **ProfileInfo** 일치 하는 응용 프로그램 이름이 데이터 원본에 있는 모든 프로필에 대 한 개체는 **ApplicationName** 속성 값입니다. **ProfileAuthenticationOption** 매개 변수 익명 프로필 프로필에만 인증 되었는지 여부를 지정 합니다. 모든 프로필을 반환할 또는 합니다. 반환 된 결과 **GetAllProfiles** 메서드 페이지 인덱스 및 페이지 크기 값에 의해 제한 됩니다. 최대 수를 지정 하는 페이지 크기 값 **ProfileInfo** 에서 반환 하는 개체는 **ProfileInfoCollection**합니다. 페이지 인덱스 값은 1에서 첫 번째 페이지를 식별 하는 위치를 반환 하려면 결과 페이지를 지정 합니다. 총 레코드에 대 한 매개 변수는 out 매개 변수입니다 (사용할 수 있습니다 **ByRef** Visual basic에서) 프로필의 총 수로 설정 되어 있는 합니다. 예를 들어 13 응용 프로그램 프로필을 포함 하는 데이터 저장소 및 페이지 인덱스 값은 5, 페이지 크기가 2는 **ProfileInfoCollection** 반환에 6 번째부터 10 번째까지의 프로필이 포함 합니다. 총 레코드 값의 메서드가 반환 될 때 13으로 설정 됩니다. |
| GetAllInactiveProfiles 메서드 | 입력으로 사용 된 **ProfileAuthenticationOption** 값은 **DateTime** 개체, 페이지 인덱스를 지정 하는 정수, 페이지 크기 및 설정 되는 정수에 대 한 참조를 지정 하는 정수 프로필의 총 개수입니다. 반환 된 **ProfileInfoCollection** 포함 된 **ProfileInfo** 보다 작거나 지정 된 마지막 작업 날짜는 데이터 원본에 있는 모든 프로필에 대 한 개체 **날짜/시간**  일치 하는 응용 프로그램 이름이 고는 **ApplicationName** 속성 값입니다. **ProfileAuthenticationOption** 매개 변수 익명 프로필 프로필에만 인증 되었는지 여부를 지정 합니다. 모든 프로필을 반환할 또는 합니다. 반환 된 결과 **GetAllInactiveProfiles** 메서드 페이지 인덱스 및 페이지 크기 값에 의해 제한 됩니다. 최대 수를 지정 하는 페이지 크기 값 **ProfileInfo** 에서 반환 하는 개체는 **ProfileInfoCollection**합니다. 페이지 인덱스 값은 1에서 첫 번째 페이지를 식별 하는 위치를 반환 하려면 결과 페이지를 지정 합니다. 총 레코드에 대 한 매개 변수는 out 매개 변수입니다 (사용할 수 있습니다 **ByRef** Visual basic에서) 프로필의 총 수로 설정 되어 있는 합니다. 예를 들어 13 응용 프로그램 프로필을 포함 하는 데이터 저장소 및 페이지 인덱스 값은 5, 페이지 크기가 2는 **ProfileInfoCollection** 반환에 6 번째부터 10 번째까지의 프로필이 포함 합니다. 총 레코드 값의 메서드가 반환 될 때 13으로 설정 됩니다. |
| FindProfilesByUserName 메서드 | 입력으로 사용 된 **ProfileAuthenticationOption** 사용자 이름, 페이지 인덱스를 지정 하는 정수, 페이지 크기와의 총 수로 설정 하는 정수에 대 한 참조를 지정 하는 정수를 포함 하는 문자열 값 프로필입니다. 반환 된 **ProfileInfoCollection** 포함 된 **ProfileInfo** 지정된 된 사용자 이름과 일치 하는 사용자 이름이 고 일치 하는 응용 프로그램 이름이 모든 프로필에는 데이터 원본에 대 한 개체는 **ApplicationName** 속성 값입니다. **ProfileAuthenticationOption** 매개 변수 익명 프로필 프로필에만 인증 되었는지 여부를 지정 합니다. 모든 프로필을 반환할 또는 합니다. 데이터 원본에 와일드 카드 문자 등의 추가 검색 기능을 지 원하는 경우 사용자 이름에 대 한 보다 광범위 한 검색 기능을 제공할 수 있습니다. 반환 된 결과 **FindProfilesByUserName** 메서드 페이지 인덱스 및 페이지 크기 값에 의해 제한 됩니다. 최대 수를 지정 하는 페이지 크기 값 **ProfileInfo** 에서 반환 하는 개체는 **ProfileInfoCollection**합니다. 페이지 인덱스 값은 1에서 첫 번째 페이지를 식별 하는 위치를 반환 하려면 결과 페이지를 지정 합니다. 총 레코드에 대 한 매개 변수는 out 매개 변수입니다 (사용할 수 있습니다 **ByRef** Visual basic에서) 프로필의 총 수로 설정 되어 있는 합니다. 예를 들어 13 응용 프로그램 프로필을 포함 하는 데이터 저장소 및 페이지 인덱스 값은 5, 페이지 크기가 2는 **ProfileInfoCollection** 반환에 6 번째부터 10 번째까지의 프로필이 포함 합니다. 총 레코드 값의 메서드가 반환 될 때 13으로 설정 됩니다. |
| FindInactiveProfilesByUserName method | 입력으로 사용 된 **ProfileAuthenticationOption** 값, 사용자 이름을 포함 하는 문자열은 **DateTime** 개체, 페이지 인덱스를 지정 하는 정수, 페이지 크기를 지정 하는 정수 및 프로필의 총 수로 설정 하는 정수에 대 한 참조입니다. 반환 된 **ProfileInfoCollection** 포함 된 **ProfileInfo** 여기서 마지막 작업 날짜는 지정한 사용자 이름이 일치 하는 사용자 이름이 데이터 원본에 있는 모든 프로필에 대 한 개체 보다 작거나 또는 지정 된 같음 **DateTime**, 일치 하는 응용 프로그램 이름이 고는 **ApplicationName** 속성 값입니다. **ProfileAuthenticationOption** 매개 변수 익명 프로필 프로필에만 인증 되었는지 여부를 지정 합니다. 모든 프로필을 반환할 또는 합니다. 데이터 원본에 와일드 카드 문자 등의 추가 검색 기능을 지 원하는 경우 사용자 이름에 대 한 보다 광범위 한 검색 기능을 제공할 수 있습니다. 반환 된 결과 **FindInactiveProfilesByUserName** 메서드 페이지 인덱스 및 페이지 크기 값에 의해 제한 됩니다. 최대 수를 지정 하는 페이지 크기 값 **ProfileInfo** 에서 반환 하는 개체는 **ProfileInfoCollection**합니다. 페이지 인덱스 값은 1에서 첫 번째 페이지를 식별 하는 위치를 반환 하려면 결과 페이지를 지정 합니다. 총 레코드에 대 한 매개 변수는 out 매개 변수입니다 (사용할 수 있습니다 **ByRef** Visual basic에서) 프로필의 총 수로 설정 되어 있는 합니다. 예를 들어 13 응용 프로그램 프로필을 포함 하는 데이터 저장소 및 페이지 인덱스 값은 5, 페이지 크기가 2는 **ProfileInfoCollection** 반환에 6 번째부터 10 번째까지의 프로필이 포함 합니다. 총 레코드 값의 메서드가 반환 될 때 13으로 설정 됩니다. |
| GetNumberOfInActiveProfiles 메서드 | 입력으로 사용 된 **ProfileAuthenticationOption** 값 및 **DateTime** 개체 하 고 마지막 작업 날짜가 지정 된 보다작거나같은데이터원본의모든프로필의수를반환합니다. **날짜/시간** 일치 하는 응용 프로그램 이름이 고는 **ApplicationName** 속성 값입니다. **ProfileAuthenticationOption** 매개 변수 익명 프로필 프로필에만 인증 되었는지 여부를 지정 합니다. 모든 프로필을 계산 또는 합니다. |

### <a name="applicationname"></a>ApplicationName

개별적으로 각 응용 프로그램에 대 한 프로필 정보를 저장 하는 프로필 공급자 때문에 데이터 스키마에 응용 프로그램 이름 포함 되도록 하 고 쿼리 및 업데이트도 포함 응용 프로그램 이름을 확인 해야 합니다. 다음 명령은 사용자 이름 및의 프로필 익명 인지 여부에 따라 데이터베이스에서 속성 값을 검색 하는 데 사용 됩니다 하 고 있는지 확인 하는 예를 들어는 **ApplicationName** 값 쿼리에 포함 됩니다.

[!code-sql[Main](profiles-themes-and-web-parts/samples/sample10.sql)]

## <a name="aspnet-themes"></a>ASP.NET 테마

## <a name="what-are-aspnet-20-themes"></a>ASP.NET 2.0 테마 이란?

웹 응용 프로그램의 가장 중요 한 측면 중 하나에 사이트에 걸쳐 일관 된 모양과 느낌입니다. ASP.NET 1.x 개발자는 일반적으로 일관 된 모양과 느낌을 구현 하려면 (CSS 스타일 시트)를 사용 합니다. ASP.NET 2.0 테마 CSS에 HTML 요소 뿐만 아니라 ASP.NET 서버 컨트롤의 모양을 정의 하는 기능은 ASP.NET 개발자를 제공 하므로 크게 개선 합니다. ASP.NET 테마 개별 컨트롤, 특정 웹 페이지 또는 웹 응용 프로그램 전체에 적용할 수 있습니다. 테마는 이미지는 필요한 경우 CSS 파일, 선택적 스킨 파일 및 선택적 이미지 디렉터리의 조합을 사용 합니다. 스킨 파일에는 ASP.NET 서버 컨트롤의 시각적 모양을 제어합니다.

## <a name="where-are-themes-stored"></a>테마 저장 어디 입니까?

테마 저장 되는 위치 해당 범위에 따라 달라 집니다. 모든 응용 프로그램에 적용할 수 있는 테마는 다음 폴더에 저장 됩니다.

`C:\WINDOWS\Microsoft.NET\Framework\v2.x.xxxxx\ASP.NETClientFiles\Themes\<Theme_Name>`

특정 응용 프로그램에만 적용 되는 테마에 저장 되는 `App\_Themes\<Theme\_Name>` 디렉터리에서 웹 사이트의 루트입니다.

> [!NOTE]
> 스킨 파일 모양에 영향을 주는 서버 컨트롤 속성 수정만 해야 합니다.

전역 테마는 응용 프로그램 또는 웹 서버에서 실행 중인 웹 사이트에 적용할 수 있는 테마입니다. 이러한 테마는 기본적으로 v2.x.xxxxx 디렉터리 내에 있는 ASP.NETClientfiles\Themes 디렉터리에 저장 됩니다. Aspnet에 테마 파일을 이동할 수 또는\_클라이언트/시스템\_웹 / [버전] /Themes/ [테마\_이름]에서 웹 사이트의 루트 폴더입니다.

응용 프로그램별 테마 파일 위치는 응용 프로그램에만 적용할 수 있습니다. 이러한 파일에 저장 되는 `App\_Themes/<theme\_name>` 디렉터리에서 웹 사이트의 루트입니다.

## <a name="the-components-of-a-theme"></a>테마의 구성 요소

테마 하나 이상의 CSS 파일, 선택적 스킨 파일 및 선택적 이미지 폴더도 이루어져 있습니다. CSS 파일에는 (즉, 다음과 같이 default.css 또는 theme.css 등)를 선택 하 고 테마 폴더의 루트에 있어야 어떤 이름도 될 수 있습니다. CSS 파일 일반 CSS 클래스 및 특정 선택기에 대 한 특성을 정의 하는 데 사용 됩니다. 페이지 요소에 CSS 클래스 중 하나를 적용 하는 **CSSClass** 속성을 사용 합니다.

스킨 파일은 ASP.NET 서버 컨트롤 속성 정의 포함 하는 XML 파일입니다. 아래에 나열 된 코드 예제에서는 스킨 파일입니다.

[!code-aspx[Main](profiles-themes-and-web-parts/samples/sample11.aspx)]

**그림 1** 다음 테마가 적용 하지 않고 작은 ASP.NET 페이지를 검색 합니다. **그림 2** 테마가 적용 된 동일한 파일을 보여 줍니다. 배경색과 텍스트 색은 CSS 파일을 통해 구성 됩니다. Button 및 textbox의 모양 위에 나열 된 스킨 파일을 사용 하 여 구성 됩니다.


![테마 없음](profiles-themes-and-web-parts/_static/image1.gif)

**그림 1**: 테마 없음


![적용 된 테마](profiles-themes-and-web-parts/_static/image2.gif)

**그림 2**: 테마가 적용


위에 나열 된 스킨 파일 모든 TextBox 컨트롤 및 단추 컨트롤에 대 한 기본 스킨을 정의 합니다. 즉, 모든 TextBox 컨트롤 및 페이지에 삽입 하는 단추 컨트롤에서이 모양을 걸립니다. 사용 하 여 이러한 컨트롤의 특정 인스턴스에 적용할 수 있는 스킨을 정의할 수도 있습니다는 **SkinID** 컨트롤의 속성입니다.

아래 코드는 단추 컨트롤의 스킨을 정의합니다. 단추만 컨트롤과 **SkinID** 속성 **goButton** 스킨의 모양에 걸립니다.

[!code-aspx[Main](profiles-themes-and-web-parts/samples/sample12.aspx)]

서버 컨트롤 형식 당 하나의 기본 스킨을 하나만 사용할 수 있습니다. 필요한 경우 추가 스킨, SkinID 속성을 사용 해야 합니다.

## <a name="applying-themes-to-pages"></a>페이지에 테마를 적용합니다.

다음 방법 중 하나를 사용 하는 테마를 적용할 수 있습니다.

- 에 &lt;페이지&gt; web.config 파일의 요소
- 에 @Page 페이지 지시문
- 프로그래밍 방식으로

## <a name="applying-a-theme-in-the-configuration-file"></a>구성 파일에서 테마를 적용

응용 프로그램 구성 파일에 테마를 적용 하려면 다음 구문을 사용 합니다.

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample13.xml)]

여기에 지정 된 테마 이름 테마 폴더의 이름과 일치 해야 합니다. 이 폴더는이 과정의 앞부분에 언급 된 위치 중 하나에 있을 수 있습니다. 존재 하지 않는 테마를 적용 하려는 경우 구성 오류가 발생 합니다.

## <a name="applying-a-theme-in-the-page-directive"></a>Page 지시문에서 테마를 적용

@ Page 지시문에서 테마를 적용할 수 있습니다. 이 메서드를 사용 하면 특정 페이지에 대 한 테마를 사용할 수 있습니다.

에 테마를 적용 하는 @Page 지시문을 다음 구문을 사용 합니다.

[!code-aspx[Main](profiles-themes-and-web-parts/samples/sample14.aspx)]

다시 한 번, 여기에 지정 된 테마 앞에서 언급 한 테마 폴더를 일치 해야 합니다. 존재 하지 않는 테마를 적용 하려고 하면 빌드 오류가 발생 합니다. Visual Studio 특성을 강조 표시 및 이러한 테마 없음 있는지 알려도 됩니다.

## <a name="applying-a-theme-programmatically"></a>테마를 프로그래밍 방식으로 적용

테마를 프로그래밍 방식으로 적용 하려면를 지정 해야는 **테마** 페이지에 대 한 속성의 **페이지\_PreInit** 메서드.

테마를 프로그래밍 방식으로 적용 하려면 다음 구문을 사용 합니다.

[!code-csharp[Main](profiles-themes-and-web-parts/samples/sample15.cs)]

페이지 수명 주기의 응답으로 PreInit 메서드에서 테마를 적용 해야 하는 합니다. 적용 하는 경우 해당 시점 이후에, 페이지 테마는 이미 적용 된 런타임에 의해 및 변경 해당 시점에 너무 늦었습니다 수명 주기에서 합니다. 존재 하지 않는 테마를 적용 하는 경우는 **HttpException** 발생 합니다. 테마를 프로그래밍 방식으로 적용 하면 서버 컨트롤은 SkinID 속성이 지정 된 경우 빌드 경고가 발생 합니다. 이 경고 테마 없음 선언적으로 적용 되 고 무시 될 수 있습니다 알리기 위한 것입니다.

## <a name="exercise-1--applying-a-theme"></a>연습 1: 테마를 적용합니다.

이 연습에서는 웹 사이트에 ASP.NET 테마를 적용 합니다.

> [!IMPORTANT]
> 스킨 파일에 정보를 입력 되어 있는지 확인 합니다 Microsoft Word를 사용 하는 경우 따옴표를 일반 따옴표로 바꾸기 없습니다. 따옴표 스킨 파일 문제가 발생 합니다.

1. 새 ASP.NET 웹 사이트를 만듭니다.
2. 솔루션 탐색기에서 프로젝트 단추로 클릭 하 고 새 항목 추가 선택 합니다.
3. 파일의 목록에서 웹 구성 파일을 선택 하 고 추가 클릭 합니다.
4. 솔루션 탐색기에서 프로젝트 단추로 클릭 하 고 새 항목 추가 선택 합니다.
5. 스킨 파일을 선택 하 고 추가 클릭 합니다.
6. 예를 묻는 메시지가 나타나면 경우 youd 응용 프로그램 내부에서 파일을 배치 하는 경우 클릭 하 여\_테마 폴더입니다.
7. 응용 프로그램 내부에서 SkinFile 폴더를 마우스 오른쪽 단추로 클릭\_테마 폴더 솔루션 탐색기에서 새 항목 추가 선택 합니다.
8. 파일의 목록에서 스타일 시트를 선택 하 고 추가 클릭 합니다. 이제 새 테마를 구현 하는 데 필요한 파일이 모두 있는 합니다. 그러나 Visual Studio 테마 SkinFile 폴더의 이름이 했습니다. 해당 폴더 단추로 클릭 하 고 이름을 CoolTheme로 변경 합니다.
9. SkinFile.skin 파일을 열고 다음 코드는 파일의 끝을 추가 합니다. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample16.aspx)]
10. SkinFile.skin 파일을 저장 합니다.
11. StyleSheet.css를 엽니다.
12. 모든 텍스트를 다음과 같이 바꿉니다. 

    [!code-css[Main](profiles-themes-and-web-parts/samples/sample17.css)]
13. StyleSheet.css 파일을 저장 합니다.
14. Default.aspx 페이지를 엽니다.
15. Button 컨트롤 및 TextBox 컨트롤을 추가 합니다.
16. 페이지를 저장합니다. Default.aspx 페이지를 검색 합니다. 이 웹 정규형으로 표시 되어야 합니다.
17. Web.config 파일을 엽니다.
18. 여는 바로 아래에서 다음 추가 `<system.web>` 태그: 

    [!code-xml[Main](profiles-themes-and-web-parts/samples/sample18.xml)]
19. Web.config 파일을 저장 합니다. Default.aspx 페이지를 검색 합니다. 테마가 적용 된 표시할지 합니다.
20. 열려 있지 않으면 Visual Studio에서 Default.aspx 페이지를 엽니다.
21. 단추를 선택 합니다.
22. 변경 된 **SkinID** 속성 goButton 합니다. Visual Studio 유효한 SkinID 값이 포함 된 드롭다운 단추 컨트롤에 대 한 제공 하는지 확인 합니다.
23. 페이지를 저장합니다. 브라우저에서 페이지를 다시 미리 보기 이제 합니다. 단추 이제 "go" 이어야 하 고 모양을 스트로크가 있어야 합니다.

사용 하는 **SkinID** 속성을 특정 형식의 서버 컨트롤의 다른 인스턴스에 대 한 다른 스킨을 쉽게 구성할 수 있습니다.

## <a name="the-stylesheettheme-property"></a>StyleSheetTheme 속성

지금까지 여태만 한 테마 속성을 사용 하 여 테마를 적용 합니다. 테마 속성을 사용 하면 스킨 파일 서버 컨트롤에 대 한 선언적 설정을 재정의 합니다. 예를 들어 1 연습에서는 단추 컨트롤에 대 한 "goButton"의 SkinID를 지정 하며 "go"를 단추의 텍스트를 변경 하는. 디자이너에 있는 단추의 텍스트 속성이 "단추"로 설정 된 있지만 테마를가 하는 알 수 있습니다. 테마는 디자이너에서 속성 설정을 항상 보다 우선 합니다.

테마의 스킨 파일에서 정의 된 속성을 무시할 수 있게 되기를 원하는 경우 속성에에서 지정 된 디자이너를 사용할 수 있습니다는 **StyleSheetTheme** 테마 속성 대신 합니다. StyleSheetTheme 속성은 테마 속성 같이 모든 명시적 속성 설정을 재정의 하지 않으므로 제외 하 고 테마 속성과 동일 합니다.

이 작업에서을 보려면을 연습 1에서에서 프로젝트의 web.config 파일을 열고 변경는 `<pages>` 요소에서 다음:

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample19.xml)]

Default.aspx 페이지를 검색 하 고 단추 컨트롤에는 "단추"의 Text 속성 다시 표시 됩니다. SkinID goButton 설정한 Text 속성을 디자이너에서 명시적 속성 설정을 재정의 하는 때문입니다.

## <a name="overriding-themes"></a>테마를 재정의합니다.

응용 프로그램에서 같은 이름의 테마를 적용 하 여 전역 테마를 재정의할 수 있습니다\_응용 프로그램의 테마 폴더입니다. 그러나 테마 true 재정의 시나리오에 적용 되지 않습니다. 런타임에 응용 프로그램에 테마 파일을 발견 하는 경우\_테마 폴더를 해당 파일을 사용 하 여 테마가 적용 됩니다 하 고 전역 테마를 무시 합니다.

StyleSheetTheme 속성 재정의 가능한 이며 코드에서 다음과 같이 재정의할 수 있습니다.

[!code-csharp[Main](profiles-themes-and-web-parts/samples/sample20.cs)]

## <a name="web-parts"></a>웹 파트

ASP.NET 웹 파트는 최종 사용자가 콘텐츠, 모양 및 동작의 웹 페이지는 브라우저에서 직접 수정할 수 있는 웹 사이트를 만들기 위한 컨트롤의 통합된 집합입니다. 사이트에서 모든 사용자에 게 또는 개별 사용자가 수정 작업을 적용할 수 있습니다. 페이지 및 컨트롤 사용자가 수정할 때 설정을 향후 브라우저 세션 전체에서 사용자의 개인 기본 설정을 유지 하려면 설정은 저장할 수 있습니다. 이러한 웹 파트 기능 개발자가 최종 사용자가을 개발자 또는 관리자의 개입 없이 동적으로 웹 응용 프로그램을 개인 설정할 수 있는 권한 부여 수를 의미 합니다.

웹 파트 컨트롤 집합을 사용 하 여, 최종 사용자가을 활성화할 수 개발자 있습니다.

- 페이지 콘텐츠를 개인 설정 합니다. 사용자 수 페이지에 새 웹 파트 컨트롤을 추가, 제거, 숨기기, 또는 일반 창과 마찬가지로 최소화 합니다.
- 페이지 레이아웃 개인 설정 합니다. 사용자가 페이지, 웹 파트 컨트롤을 다른 영역으로 끌어 하거나 해당 모양, 속성 및 동작을 변경할 수 있습니다.
- 내보내고 컨트롤을 가져옵니다. 사용자가 가져오거나 속성을 컨트롤의 데이터에도 그대로 유지 하 고 다른 페이지 또는 사이트에서 사용 하기 위해 웹 파트 컨트롤 설정을 내보낼 수 있습니다. 이렇게 하면 최종 사용자에 게 데이터 항목 및 구성 요구 줄어듭니다.
- 연결을 만듭니다. 사용자는 차트 컨트롤 주식 시세 컨트롤의 데이터에 대 한 그래프를 표시할 수 예를 들어 있도록 컨트롤 간의 연결을 설정할 수 있습니다. 사용자가 자체에 연결 하지만 모양 및 차트 컨트롤에서 데이터를 표시 하는 방법에 대 한 세부 정보 뿐만 아니라 개인 설정할 수 없습니다.
- 관리 및 사이트 수준 설정을 개인 설정 합니다. 권한이 있는 사용자 사이트 수준 설정을 구성, 사이트 또는 페이지에 액세스할 수, 컨트롤에 대 한 역할 기반 액세스를 설정 및 등가 결정할 수 있습니다. 예를 들어 관리 역할의 사용자 모든 사용자가 공유 하도록 웹 파트 컨트롤을 설정 하 고 공유 제어를 개인 설정에서 관리자가 아닌 사용자가 수 없습니다.

다음 세 가지 방법 중 하나에서 웹 파트를 일반적으로 사용 합니다: 웹 파트 컨트롤을 사용 하는 페이지를 만들어 개별 웹 파트 컨트롤을 만들거나 완전 하 고 개인 설정 가능한 웹 응용 프로그램을 만들 포털 같은 합니다.

## <a name="page-development"></a>페이지 개발

페이지 개발자가 웹 파트를 사용 하는 페이지를 만들려면 Microsoft Visual Studio 2005 등 비주얼 디자인 도구를 사용할 수 있습니다. Visual Studio는 웹 파트 컨트롤 집합와 같은 도구를 사용 하 여 장점 중 하나는 비주얼 디자이너에서 웹 파트 컨트롤의 끌어서 놓기 생성 및 구성에 대 한 기능을 제공 합니다. 디자이너를 사용 하 여 웹 파트 영역 또는 웹 파트 편집기 컨트롤을 디자인 화면으로 끌어 다음 컨트롤 권한을 구성 하는 예를 들어 웹 파트에서 제공 하는 UI를 사용 하 여 디자이너에서 컨트롤 집합입니다. 이 웹 파트 응용 프로그램의 개발 속도 향상 하 고를 작성 해야 하는 코드의 양을 줄일 수 있습니다.

## <a name="control-development"></a>컨트롤 개발

표준 웹 서버 컨트롤, 사용자 지정 서버 컨트롤 및 사용자 정의 컨트롤을 포함 하 여 웹 파트 컨트롤을 기존 ASP.NET 컨트롤을 사용할 수 있습니다. 사용자 환경의 최대 프로그래밍 방식 제어, WebPart 클래스에서 파생 되는 사용자 지정 웹 파트 컨트롤 만들 수도 있습니다. 개별 웹 파트 컨트롤 개발에 대 한 있습니다 일반적으로 사용자 정의 컨트롤 만들기 및 컨트롤을 웹 파트를 사용 하거나 사용자 지정 웹 파트 컨트롤을 개발 합니다.

사용자 지정 웹 파트 컨트롤 개발의 예를 들어 개인 설정할 수 있는 컨트롤을 웹 파트 패키지에 유용할 수 있는 다른 ASP.NET 서버 컨트롤에서 제공 하는 기능을 제공 하는 컨트롤을 만들 수 있습니다: 일정, 목록, 재무 정보 뉴스, 계산기, 콘텐츠, 편집 가능한 표를 업데이트 하기 위한 서식 있는 텍스트 컨트롤 하는 동적으로 표시, 업데이트를 정보를 제공 하는 차트, 데이터베이스에 연결 합니다. 컨트롤과 함께 비주얼 디자이너를 제공 하는 경우 다음 Visual Studio를 사용 하는 페이지 개발자 수 컨트롤 웹 파트 영역으로 끌어서 추가 코드를 작성할 필요 없이 디자인 타임에 구성 됩니다.

개인 설정에는 웹 파트 기능의 기초입니다. 사용자가을 수정 하거나 레이아웃, 모양 및 페이지에 웹 파트 컨트롤의 동작을 개인 설정할 수 있습니다. 사용자 개인된 설정을 수명이 긴: 현재 브라우저 세션 동안이 아니라 유지 됩니다 (와 마찬가지로 뷰 상태), 장기 저장에도도 이후 브라우저 세션에 대 한 사용자의 설정을 저장할 수 있도록 합니다. 개인 설정 웹 파트 페이지에 대 한 기본으로 사용 됩니다.

UI 구조적 구성 요소는 개인 설정에 의존 하 고는 핵심 구조 및 모든 웹 파트 컨트롤에 필요한 서비스를 제공 합니다. 모든 웹 파트 페이지에 필요한 하나 UI 구조적 구성에는 WebPartManager 컨트롤입니다. 에 표시 되지는 않지만이 컨트롤은 페이지에서 모든 웹 파트 컨트롤을 조정 하의 중요 한 작업입니다. 예를 들어 개별 모든 웹 파트 컨트롤을 추적 합니다. 웹 파트 영역 (웹 파트 페이지에 있는 컨트롤을 포함 하는 영역)에서 관리 하 고 어떤 영역에 있는 컨트롤입니다. 또한 추적 하 고 페이지 수와 같이 있을 찾아보기, 연결, 편집 또는 카탈로그 모드 및 모든 사용자에 게 또는 개별 사용자에 게 개인 설정 변경 내용은 적용 되는지 여부를 다른 디스플레이 모드를 제어 합니다. 마지막으로 시작 하 고 웹 파트 컨트롤 간의 연결 및 통신을 추적 합니다.

두 번째 종류의 UI 구조적 구성 요소는 영역입니다. 영역 레이아웃 관리자 역할을 웹 파트 페이지에 있습니다. 포함 하 고 (파트 컨트롤), 파트 클래스에서 파생 되는 컨트롤을 구성 하며 모듈식 페이지 레이아웃 가로 또는 세로 방향으로 작업을 수행 하는 기능을 제공 합니다. 또한 영역 포함 하는 각 컨트롤에 대 한 공통 일관성 있는 UI 요소 (예: 머리글 및 바닥글의 스타일, 제목, 테두리 스타일, 실행 단추, 및 등)을 제공 이러한 공통 요소를 컨트롤의 크롬 라고 합니다. 영역 중 몇 가지 특수 유형은 다양 한 디스플레이 모드에서 한 다양 한 컨트롤에 사용 됩니다. 다양 한 유형의 영역 아래의 웹 파트에 대 한 필수 컨트롤 섹션에 설명 되어 있습니다.

파생 되는 모든 웹 파트 UI 컨트롤의 **부분** 클래스, 웹 파트 페이지에서 기본 UI를 구성 합니다. 웹 파트 컨트롤 집합은 유연 하 고 포괄적인 옵션 제공 파트 컨트롤을 만드는 합니다. 사용자 고유의 사용자 지정 웹 파트 컨트롤을 만들 뿐만 아니라 기존의 ASP.NET 서버 컨트롤, 사용자 정의 컨트롤 또는 사용자 지정 서버 컨트롤을 웹 파트 컨트롤로 사용할 수도 있습니다. 웹 파트 페이지를 만드는 데 가장 일반적으로 사용 되는 필수 컨트롤은 다음 섹션에 설명 되어 있습니다.

## <a name="web-parts-essential-controls"></a>웹 파트 필수 컨트롤

웹 파트 컨트롤 집합 광범위 하지만 작동 하도록 하는 웹 파트에 대 한 필요 하므로 또는 웹 파트 페이지에서 가장 자주 사용 하는 컨트롤을 되기 때문에 일부 컨트롤은 필수입니다. 웹 파트를 사용 하 여 시작 하 고 기본 웹 파트 페이지를 만드는 것 다음 표에 설명 된 필수 웹 파트 컨트롤에 익숙해지는 것이 도움이 됩니다.

| **웹 파트 컨트롤** | **설명** |
| --- | --- |
| WebPartManager | 페이지에서 모든 웹 파트 컨트롤을 관리합니다. (한 개만) **WebPartManager** 컨트롤은 모든 웹 파트 페이지에 필요 합니다. |
| CatalogZone | CatalogPart 컨트롤만 포함 되어 있습니다. 이 영역을 사용 하 여 사용자가 페이지에 추가할 컨트롤을 선택할 수 있는 웹 파트 컨트롤의 카탈로그를 만듭니다. |
| EditorZone | EditorPart 컨트롤만 포함 되어 있습니다. 이 영역을 사용 하 여 사용자를 편집 하 여 웹 파트 페이지에 있는 컨트롤을 개인 설정할 수 있도록 합니다. |
| WebPartZone | 포함 하 고 페이지의 기본 UI를 구성 하는 웹 파트 컨트롤에 대 한 전체 레이아웃을 제공 합니다. 웹 파트 컨트롤이 있는 페이지를 만들 때마다이 영역을 사용 합니다. 페이지는 하나 이상의 영역을 포함할 수 있습니다. |
| ConnectionsZone | WebPartConnection 컨트롤을 포함 하 고 연결을 관리 하는 UI를 제공 합니다. |
| 웹 파트 (GenericWebPart) | 기본 UI; 렌더링 대부분의 웹 파트 UI 컨트롤이이 범주에 속합니다. 최대 프로그래밍 방식으로 컨트롤에 대 한 기본에서 파생 되는 사용자 지정 웹 파트 컨트롤을 만들 수 있습니다 **WebPart** 제어 합니다. 웹 파트 컨트롤로 기존 서버 컨트롤, 사용자 정의 컨트롤 또는 사용자 지정 컨트롤도 사용할 수 있습니다. 이러한 컨트롤 중 하나는 영역에 배치 됩니다 때마다는 **WebPartManager** 자동으로 컨트롤은를 사용 하 여 줄 바꿈 **GenericWebPart** 웹 파트 기능으로 사용할 수 있도록 런타임에 제어 합니다. |
| CatalogPart | 사용자가 페이지에 추가할 수 있는 사용 가능한 웹 파트 컨트롤의 목록을 포함 합니다. |
| WebPartConnection | 페이지에 두 웹 파트 컨트롤 간의 연결을 만듭니다. 연결 (데이터)의 공급자 및 소비자로 다른 웹 파트 컨트롤 중 하나를 정의 합니다. |
| EditorPart | 특수 편집기 컨트롤에 대 한 기본 클래스로 사용 됩니다. |
| EditorPart 컨트롤만 (AppearanceEditorPart, LayoutEditorPart, BehaviorEditorPart, 및 PropertyGridEditorPart) | 사용자가 페이지에 웹 파트 UI 컨트롤의 다양 한 측면을 개인 설정할 수 있도록 허용 |

## <a name="lab-create-a-web-part-page"></a>랩: 웹 파트 페이지 만들기

이 랩에서 ASP.NET 프로필을 통해 정보를 유지 하는 웹 파트 페이지를 만들게 됩니다.

### <a name="creating-a-simple-page-with-web-parts"></a>웹 파트가 포함 된 단순한 페이지 만들기

이 연습 부분에서는 웹 파트 컨트롤을 사용 하 여 정적 콘텐츠를 표시 하는 페이지를 만듭니다. 웹 파트를 사용 하는 첫 번째 단계는 두 개의 필수 구조적 요소가 있는 페이지를 만드는 것입니다. 첫째, 웹 파트 페이지를 추적 하 고 모든 웹 파트 컨트롤을 조정 합니다. WebPartManager 컨트롤이 필요 합니다. 둘째, 웹 파트 페이지에 웹 파트 또는 다른 서버 컨트롤을 포함 하는 페이지의 지정된 된 영역을 차지 하는 복합 컨트롤 영역 중 하나 이상이 필요 합니다.

> [!NOTE]
> 웹 파트 개인 설정;를 사용 하도록 설정 하려면 어떤 작업도 수행할 필요가 없습니다. 웹 파트 컨트롤 집합에 대해 기본적으로 설정 됩니다. 사이트에서 웹 파트 페이지를 처음 실행 하면 ASP.NET 사용자 개인 설정을 저장 하는 기본 개인 설정 공급자를 설정 합니다. 개인 설정에 대 한 자세한 내용은 웹 파트 개인 설정 개요를 참조 하십시오.


### <a name="to-create-a-page-for-containing-web-parts-controls"></a>웹 파트 컨트롤을 포함 하는 것에 대 한 페이지를 만들려면

1. 기본 페이지를 닫고 WebPartsDemo.aspx 이라는 사이트를 새 페이지를 추가 합니다.
2. 로 전환 **디자인** 보기.
3. **보기** 메뉴에서 다음 사항을 확인는 **비시각적 컨트롤** 및 **세부 정보** 레이아웃 태그 및 UI를 갖지 않는 컨트롤을 볼 수 있도록 옵션을 선택 합니다.
4. 앞에 삽입 포인터를 배치할는 `<div>` 다음 enter 키를 눌러 새 줄을 추가 하 고 디자인 화면에 태그를 삽입 합니다. 줄 바꿈 문자 앞에 삽입 포인터를 놓고 클릭는 **블록 형식을** 드롭 다운 목록 메뉴에서 제어 하 고 선택 된 **제목 1** 옵션입니다. 머리글에서 텍스트를 추가 **웹 파트 데모 페이지**합니다.
5. **WebParts** 끌어서 도구 상자 탭은 **WebPartManager** 컨트롤을 줄 바꿈 문자 바로 뒤와 앞에 배치 페이지로 `<div>`태그입니다.   
  
   **WebPartManager** 디자이너 화면에는 회색 상자로 표시 되도록 컨트롤에 출력을 렌더링 하지 않습니다.
6. 내에서 커서는 `<div>` 태그입니다.
7. 에 **레이아웃** 메뉴를 클릭 **표 삽입**, 3 개의 열과 한 행이 있는 새 테이블을 만듭니다. 클릭는 **셀 속성** 단추를 선택 **top** 에서 **세로 맞춤** 드롭 다운 목록에서 클릭 **확인**, 클릭**확인** 다시 테이블을 만들 수 있습니다.
8. 왼쪽된 테이블 열에는 WebPartZone 컨트롤을 끌어 놓습니다. 마우스 오른쪽 단추로 클릭는 **WebPartZone** 컨트롤을 선택 **속성**, 다음 속성을 설정 합니다.   
  
   ID: SidebarZone   
  
   HeaderText: 사이드바
9. 두 번째 끌어 **WebPartZone** 중간 테이블 열에 대 한 제어 하 고 다음 속성을 설정 합니다.   
  
   ID: MainZone   
  
   HeaderText: 주
10. 파일을 저장합니다.

이제 페이지에는 개별적으로 제어할 수 있는 두 개의 영역이 포함 되어 있습니다. 그러나 두 영역에 콘텐츠를 없으므로 다음 단계를 콘텐츠를 만듭니다. 이 연습에서는 정적 콘텐츠만 표시 하는 웹 파트 컨트롤을 사용 하 여 작업할 합니다.

웹 파트 영역의 레이아웃으로 지정 된 &lt;zonetemplate&gt; 요소입니다. 영역 템플릿 내의 모든 ASP.NET 컨트롤을 사용자 지정 웹 파트 컨트롤, 사용자 정의 컨트롤 또는 기존 서버 컨트롤을 추가할 수 있습니다. Label 컨트롤을 사용 하는 여기에 단순히 추가 하는 정적 텍스트에 유의 하십시오. 에 일반 서버 컨트롤을 배치 하는 경우는 **WebPartZone** 영역 ASP.NET 컨트롤로 처리 웹 파트 컨트롤을 컨트롤에 웹 파트 기능을 사용할 수 있는 런타임 시.

**주요 영역에 대 한 콘텐츠를 만들려면**

1. **디자인** 보기, 끌어는 **레이블** 에서 제어는 **표준** 영역의 콘텐츠 영역으로 도구 상자 탭 인 **ID** 속성 MainZone로 설정 됩니다.
2. 로 전환 **소스** 보기. 다음에 유의 &lt;zonetemplate&gt; 요소가 줄 바꿈에 추가 **레이블** 는 MainZone에서 제어 합니다.
3. 명명 된 특성을 추가 **제목** 에 &lt;p: label&gt; 요소, 콘텐츠를 해당 값을 설정 합니다. 텍스트를 제거 =에서 "Label" 특성은 &lt;p: label&gt; 요소입니다. 여는 태그와 닫는 태그 사이 &lt;p: label&gt; 요소를 일부 텍스트와 같은 추가 **홈 페이지 내에 시작** 쌍 안의 &lt;h2&gt; 요소 태그입니다. 코드는 다음과 같이 표시 됩니다. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample21.aspx)]
4. 파일을 저장합니다.

다음으로 컨트롤을 웹 파트 페이지에도 추가할 수 있는 사용자 정의 컨트롤을 만듭니다.

### <a name="to-create-a-user-control"></a>사용자 정의 컨트롤을 만들려면

1. 검색 컨트롤 역할을 사이트에 새 웹 사용자 정의 컨트롤을 추가 합니다. 옵션을 선택 취소 **별도 파일에 소스 코드를 배치할**합니다. WebPartsDemo.aspx 페이지와 같은 디렉터리에 추가 하 고 SearchUserControl.ascx 이름을 키를 누릅니다.   
  
    > [!NOTE]
    > 이 연습에 대 한 사용자 정의 컨트롤 실제 검색 기능을 구현 하지 않습니다. 웹 파트 기능을 설명 하기 위해서만 사용 됩니다.
2. 로 전환 **디자인** 보기. **표준** 탭의 도구 상자 TextBox 컨트롤을 페이지로 끌어 합니다.
3. 방금 추가한 텍스트 상자 뒤 삽입점을 배치 하 고 enter 키를 눌러 새 줄을 추가 합니다.
4. 방금 추가한 입력란 아래로 새 줄에 단추 컨트롤을 페이지로 끌어 합니다.
5. 로 전환 **소스** 보기. 사용자 정의 컨트롤에 대 한 소스 코드는 다음 예제와 표시 되는지 확인 합니다. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample22.aspx)]
6. 파일을 저장한 후 닫습니다.

이제 사이드바 영역에 웹 파트 컨트롤을 추가할 수 있습니다. 세로 막대 영역에 두 개의 컨트롤을 추가 하는, 이전 절차에서 만든 사용자 정의 컨트롤 된와 링크의 목록을 포함 합니다. 표준으로 링크 추가 **레이블** 서버 컨트롤을 Main 영역에 대 한 정적 텍스트를 생성 하는 방식과 비슷합니다. 그러나 개별 서버 컨트롤에 포함 되어 있지만 사용자 정의 컨트롤 (예: 레이블 컨트롤) 영역에 직접 포함 될 수,이 경우 않습니다. 대신, 이전 절차에서 만든 사용자 정의 컨트롤의 포함 됩니다. 이 모든 컨트롤 및 사용자 정의 컨트롤에 포함 하려는 추가 기능을 패키지 하 고 다음 컨트롤을 웹 파트 영역에 해당 컨트롤을 참조 하는 일반적인 방법은 보여 줍니다.

런타임 시 웹 파트 컨트롤 집합 GenericWebPart 컨트롤과 두 컨트롤을 래핑합니다. 경우는 **GenericWebPart** 컨트롤이 웹 서버 컨트롤이 래핑될 만큼, 일반 부품 컨트롤은 부모 컨트롤 및 부모 컨트롤의 ChildControl 속성을 통해 서버 컨트롤에 액세스할 수 있습니다. 일반 파트 컨트롤의이 사용 하면 표준 웹 서버 컨트롤에는 같은 기본 동작 및 특성에서 파생 되는 웹 파트 컨트롤와는 **WebPart** 클래스입니다.

### <a name="to-add-web-parts-controls-to-the-sidebar-zone"></a>사이드바 영역에 웹 파트 컨트롤을 추가 하려면

1. WebPartsDemo.aspx 페이지를 엽니다.
2. 로 전환 **디자인** 보기.
3. 사용자 컨트롤 만든 페이지, SearchUserControl.ascx를 끌어 **솔루션 탐색기** 영역으로 해당 **ID** 속성 SidebarZone로 설정 되 고 있는 삭제 합니다.
4. WebPartsDemo.aspx 페이지를 저장 합니다.
5. 로 전환 **소스** 보기.
6. 내에서 &lt;asp: webpartzone&gt; 추가 사용자 정의 컨트롤에 대 한 참조 바로 위에 SidebarZone에 대 한 요소는 &lt;p: label&gt; 요소를 다음 예제와 같이, 링크를 포함 합니다. 또한 추가 **제목** 특성을 사용자 정의 컨트롤 태그의 값을 가진 **검색**표시 된 것 처럼 합니다. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample23.aspx)]
7. 파일을 저장한 후 닫습니다.

이제 페이지를 브라우저에서 이동 하 여 테스트할 수 있습니다. 페이지에는 두 개의 영역이 표시 됩니다. 다음 스크린 샷에서 페이지를 보여줍니다.

**두 영역으로 웹 파트 데모 페이지**


![웹 파트 VS 연습 1 스크린 샷](profiles-themes-and-web-parts/_static/image3.gif)

**그림 3**: 웹 파트 VS 연습 1 스크린 샷


제목에 각 컨트롤의 표시줄은 컨트롤에서 수행할 수 있습니다 사용할 수 있는 동작 동사 메뉴에 대 한 액세스를 제공 하는 아래쪽 화살표를 사용 합니다. 컨트롤 중 하나에 대 한 동사 메뉴를 클릭 한 다음 클릭는 **최소화** verb 및 참고 컨트롤 최소화 됩니다. 동사 메뉴에서 클릭 **복원**, 보통 크기로 컨트롤을 반환 합니다.

### <a name="enabling-users-to-edit-pages-and-change-layout"></a>사용자가을 페이지 편집 및 레이아웃 변경

웹 파트 한 영역에서 다른 위치로 끌어서 웹 파트 컨트롤의 레이아웃을 변경 하는 사용자에 대 한 기능을 제공 합니다. 사용자가 이동 하도록 허용 하는 것 외에도 **WebPart** 한 영역에서 다른 컨트롤의 모양, 레이아웃 및 동작을 포함 하 여 컨트롤의 다양 한 특성을 편집 하려면 사용자가 허용할 수 있습니다. 웹 파트 컨트롤 집합에 대 한 기본 편집 기능을 제공 **WebPart** 컨트롤입니다. 기능을 편집할 수 있도록 하는 사용자 지정 편집기 컨트롤을 만들 수도 수 하므로이 연습에서 수행 하지는 않지만 **WebPart** 컨트롤입니다. 위치를 변경 하는 것과 마찬가지로 **WebPart** , 컨트롤의 속성 편집에 의존 하 여 사용자가 변경 내용을 저장 하려면 ASP.NET 개인 설정 합니다.

이 연습 부분에서는 사용자가 모든 기본 특성을 편집할 수 있는 기능을 추가 하면 **WebPart** 페이지에서 제어 합니다. 이러한 기능을 사용 하려면 다른 사용자 지정 사용자 정의 컨트롤을 추가한 페이지와 함께 &lt;e&gt; 요소와 두 개의 편집 컨트롤과 합니다.

### <a name="to-create-a-user-control-that-enables-changing-page-layout"></a>페이지 레이아웃을 변경할 수 있도록 하는 사용자 정의 컨트롤을 만들려면

1. Visual Studio에서에 **파일** 메뉴를 선택는 **새로** 하위 메뉴를 클릭 하 고는 **파일** 옵션입니다.
2. 에 **새 항목 추가** 대화 상자에서 **웹 사용자 정의 컨트롤**합니다. DisplayModeMenu.ascx 새 파일을 이름을 지정 합니다. 옵션을 선택 취소 **다른 파일에 소스 코드를 입력**합니다.
3. 새 컨트롤을 만들려면 추가 클릭 합니다.
4. 로 전환 **소스** 보기.
5. 새 파일에 모든 기존 코드를 제거 하 고 다음 코드를 붙여 넣습니다. 이 사용자 정의 컨트롤 코드 또는 모드를 표시 합니다. 해당 뷰를 변경 하려면 페이지를 사용할 수 있는 웹 파트 컨트롤 집합의 기능을 사용 하 여 실제 모양을 변경할 수 있습니다 및 특정 디스플레이 모드에 있는 동안 페이지의 레이아웃입니다. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample24.aspx)]
6. 저장을 클릭 하 여 파일을 저장 아이콘을 선택 하 여 또는 도구 모음의 **저장** 에 **파일** 메뉴.

### <a name="to-enable-users-to-change-the-layout"></a>레이아웃을 변경 하려면 사용자가 사용 하도록 설정 하려면

1. WebPartsDemo.aspx 페이지를 열고 전환할 **디자인** 보기.
2. 에 삽입 포인터는 **디자인** 볼 바로 뒤의 **WebPartManager** 이전에 추가한 컨트롤. 다음에 빈 줄 되도록 하드 리턴 텍스트 뒤에 추가 된 **WebPartManager** 제어 합니다. 빈 줄에 삽입 포인터를 놓습니다.
3. 방금 만든 사용자 정의 컨트롤을 끌어 옵니다 (파일의 이름은 DisplayModeMenu.ascx) 페이지는 WebPartsDemo.aspx에 빈 줄에 놓습니다.
4. EditorZone 컨트롤을 끌어는 **WebParts** WebPartsDemo.aspx 페이지의 나머지 열려 있는 테이블 셀에 도구 상자의 섹션.
5. **WebParts** 섹션 도구 상자의 AppearanceEditorPart 컨트롤과 LayoutEditorPart 컨트롤에 컨트롤을 끌어는 **EditorZone** 제어 합니다.
6. 로 전환 **소스** 보기. 테이블 셀의 결과 코드는 다음 코드와 유사한 찾아야 합니다. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample25.aspx)]
7. WebPartsDemo.aspx 파일을 저장 합니다. 디스플레이 모드를 변경 하 고 페이지 레이아웃을 변경할 수 있도록 사용자 정의 컨트롤을 만들고 기본 웹 페이지에 컨트롤을 참조 했습니다.

이제 페이지를 편집 하 고 레이아웃을 변경 하는 기능을 테스트할 수 있습니다.

### <a name="to-test-layout-changes"></a>레이아웃 변경 내용을 테스트 하려면

1. 브라우저에서 페이지를 로드 합니다.
2. 클릭는 **디스플레이 모드** 드롭 다운 메뉴에서을 선택 **편집**합니다. 영역 제목이 표시 됩니다.
3. 끌어서는 **내 링크** Main 영역 아래쪽에 세로 막대 영역에서의 제목 표시줄 컨트롤입니다. 페이지에서는 다음 스크린 샷과 같이 표시 됩니다.

### <a name="web-parts-demo-page-with-my-links-control-moved"></a>웹 파트 데모 페이지 내 링크 컨트롤 이동


![웹 파트 VS 연습 2 스크린 샷](profiles-themes-and-web-parts/_static/image4.gif)

**그림 4**: 웹 파트 VS 연습 2 스크린 샷


1. 클릭는 **디스플레이 모드** 드롭 다운 메뉴에서을 선택 **찾아보기**합니다. 영역 이름이 사라지는, 페이지를 새로 고 **내 링크** 계속 배치 된 위치를 제어 합니다.
2. 가 작업을 보여 주기 위해 브라우저를 닫고 페이지를 다시 로드 합니다. 이후 브라우저 세션에 대 한 변경 내용을 저장 됩니다.
3. **디스플레이 모드** 메뉴 선택 **편집**합니다.   
  
   페이지에 있는 각 컨트롤 동사 드롭다운 메뉴를 포함 하는 제목 표시줄에 있는 아래쪽 화살표와 함께 표시 됩니다.
4. 동사 메뉴를 표시 하려면 화살표를 클릭는 **내 링크** 제어 합니다. 클릭는 **편집** 동사입니다.   
  
   **EditorZone** 컨트롤이 표시 되 고, 추가한 컨트롤은 EditorPart 표시 합니다.
5. 에 **모양** 변경 하는 편집 컨트롤의 섹션은 **제목** 즐겨찾기를 사용 하 여는 **크롬 유형** 를 선택 하려면 드롭다운 목록 **제목만**, 클릭 하 고 **적용**합니다. 다음 스크린 샷에서 편집 모드에 있는 페이지를 보여줍니다.

### <a name="web-parts-demo-page-in-edit-mode"></a>편집 모드에서 웹 파트 데모 페이지


![웹 파트 VS 연습 3 스크린 샷](profiles-themes-and-web-parts/_static/image5.gif)

**그림 5**: 웹 파트 VS 연습 3 스크린 샷


1. 클릭는 **디스플레이 모드** 메뉴에서을 선택 **찾아보기** 찾아보기 모드로 돌아갑니다.
2. 이제 컨트롤에는 업데이트 된 제목과 테두리가 없습니다 다음 스크린 샷에 표시 된 것 처럼 합니다.

### <a name="edited-web-parts-demo-page"></a>편집 된 웹 파트 데모 페이지


![웹 파트 VS 연습 4 스크린 샷](profiles-themes-and-web-parts/_static/image6.gif)

**그림 4**: 웹 파트 VS 연습 4 스크린 샷


### <a name="adding-web-parts-at-run-time"></a>런타임 시 웹 파트 추가

또한 런타임 시 해당 페이지에 웹 파트 컨트롤을 추가 하려면 사용자가 허용할 수 있습니다. 이렇게 하려면 페이지를 사용자에 게 사용할 수 있도록 설정할 웹 파트 컨트롤의 목록이 포함 된 웹 파트 카탈로그를 구성 합니다.

**런타임 시 웹 파트를 추가할 수 있도록 하려면**

1. WebPartsDemo.aspx 페이지를 열고 전환할 **디자인** 보기.
2. **WebParts** 탭의 도구 상자 컨트롤을 끌어 CatalogZone 표의 오른쪽 열에 아래에 **EditorZone** 제어 합니다.   
  
   두 컨트롤 모두 같은 표 셀에 수 있습니다 동시에 표시 되지 것입니다.
3. 속성 창에서 문자열을 할당 **웹 파트 추가** 의 HeaderText 속성에는 **CatalogZone** 제어 합니다.
4. **WebParts** 섹션 도구 상자의 DeclarativeCatalogPart 컨트롤의 콘텐츠 영역으로 끕니다는 **CatalogZone** 제어 합니다.
5. 오른쪽 위 모서리에 있는 화살표를 클릭 합니다.는 **DeclarativeCatalogPart** 해당 작업 메뉴를 노출 하도록 제어 하 고 다음 선택 **템플릿 편집**합니다.
6. **표준** 끌어서 도구 상자의 섹션은 **파일 업로드** 제어 및 **달력** 컨트롤을 **WebPartsTemplate** 섹션은 **DeclarativeCatalogPart** 제어 합니다.
7. 로 전환 **소스** 보기. 소스 코드 검사는 &lt;asp: catalogzone&gt; 요소입니다. 에 **DeclarativeCatalogPart** 컨트롤에 포함 되어는 &lt;webpartstemplate&gt; 카탈로그에서 페이지에 추가할 수 있는 두 개의 포함 된 서버 컨트롤 요소입니다.
8. 추가 **제목** 속성을 아래 코드 예제에서는 각 타이틀에 대해 표시 되는 문자열 값을 사용 하 여 카탈로그에 추가 된 컨트롤의 각 합니다. 제목 속성인 경우에 설정할 수 있습니다 일반적으로 이러한 두 명의 서버 컨트롤에는 사용자 이러한 컨트롤을 추가 하는 경우 디자인 타임에는 **WebPartZone** 영역 런타임 시 카탈로그에서 각각 래핑되고와  **GenericWebPart** 제어 합니다. 이 통해 역할 웹 파트 컨트롤을 되므로 책 제목은 표시할 수 있습니다.   
  
   에 포함 된 두 컨트롤에 대 한 코드는 **DeclarativeCatalogPart** 컨트롤이 다음과 같이 표시 됩니다. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample26.aspx)]
9. 페이지를 저장합니다.

이제 카탈로그를 테스트할 수 있습니다.

### <a name="to-test-the-web-parts-catalog"></a>웹 파트 카탈로그를 테스트 하려면

1. 브라우저에서 페이지를 로드 합니다.
2. 클릭는 **디스플레이 모드** 드롭 다운 메뉴에서을 선택 **카탈로그**합니다.   
  
   라는 카탈로그 **웹 파트 추가** 표시 됩니다.
3. 끌어서는 **즐겨찾기** 사이드바 영역의 맨 위로 이동 Main 영역에서 제어 하 고 있는 놓습니다.
4. 에 **웹 파트 추가** 카탈로그 두 확인란을 선택한 다음 선택 **Main** 사용 가능한 영역에 있는 드롭 다운 목록에서.
5. 클릭 **추가** 카탈로그에 있습니다. 컨트롤을 Main 영역에 추가 합니다. 원할 경우 카탈로그에서 페이지에 컨트롤의 여러 인스턴스를 추가할 수 있습니다.   
  
   다음 스크린 샷에서 Main 영역에서 파일 업로드 컨트롤 및 일정 페이지를 보여 줍니다. 

![카탈로그에서 Main 영역에 추가 된 컨트롤](profiles-themes-and-web-parts/_static/image7.gif)

    **Figure 5**: Controls added to Main zone from the catalog
6. 클릭는 **디스플레이 모드** 드롭 다운 메뉴에서을 선택 **찾아보기**합니다. 카탈로그 사라지고 페이지가 새로 고쳐집니다.
7. 브라우저를 닫습니다. 페이지를 다시 로드 합니다. 변경 내용이 유지 됩니다.
