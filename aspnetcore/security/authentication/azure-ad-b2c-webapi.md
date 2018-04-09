---
title: 웹 Api와 ASP.NET 코어의 Azure Active Directory B2C에에서 대 한 클라우드 인증
author: camsoper
description: ASP.NET Core 웹 API와 Azure Active Directory B2C 인증을 설정 하는 방법을 알아봅니다. 인증 된 웹 우체부를 사용 하 여 API를 테스트 합니다.
ms.author: casoper
manager: wpickett
ms.date: 01/25/2018
ms.topic: tutorial
ms.technology: aspnet
ms.prod: asp.net-core
ms.custom: mvc
uid: security/authentication/azure-ad-b2c-webapi
ms.openlocfilehash: 621290f7e303f9157577b5c1b32646b750ed5159
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="cloud-authentication-in-web-apis-with-azure-active-directory-b2c-in-aspnet-core"></a>웹 Api와 ASP.NET 코어의 Azure Active Directory B2C에에서 대 한 클라우드 인증

작성자: [Cam Soper](https://twitter.com/camsoper)

[Azure Active Directory B2C](/azure/active-directory-b2c/active-directory-b2c-overview) (Azure AD B2C)는 웹 및 모바일 앱에 대 한 클라우드 id 관리 솔루션입니다. 서비스는 클라우드 및 온-프레미스에서 호스트 되는 앱에 대 한 인증을 제공 합니다. 인증 유형을 개별 계정, 소셜 네트워크 계정 등 엔터프라이즈 계정을 페더레이션 합니다. 또한 Azure AD B2C 최소 구성으로 다단계 인증을 제공할 수 있습니다.

> [!TIP]
> Azure Active Directory (Azure AD) 및 Azure AD B2C 별도 제품이 제공 됩니다. Azure AD 테 넌 트 조직을 나타내고 Azure AD B2C 테 넌 트를 신뢰 당사자 응용 프로그램과 함께 사용할 id의 컬렉션을 나타냅니다. 자세한 내용은 참고 [Azure AD B2C: 질문과 대답 (FAQ)](/azure/active-directory-b2c/active-directory-b2c-faqs)합니다.

웹 Api에는 사용자 인터페이스가 없는, 이후 Azure AD B2C와 같은 보안 토큰 서비스에 사용자를 리디렉션할 수 있지 않는 합니다. 대신, API가 이미 Azure AD B2C를 사용 하 여 사용자를 인증 하는 호출 응용 프로그램에서 전달자 토큰을 전달 됩니다. 다음 API를 직접 사용자 상호 작용 없이 토큰 유효성을 검사 합니다.

이 자습서에 설명 하는 방법:

> [!div class="checklist"]
> * Azure Active Directory B2C 테 넌 트를 만듭니다.
> * Azure AD B2C에 Web API를 등록 합니다.
> * 인증을 위해 Azure AD B2C 테 넌 트를 사용 하도록 구성 된 웹 API 키를 만들려면 Visual Studio를 사용 합니다.
> * Azure AD B2C 테 넌 트의 동작을 제어 하는 정책을 구성 합니다.
> * 사용 하 여 우체부는 로그인 대화 상자를 표시 하는 웹 앱을 시뮬레이션 하는 토큰을 검색 하 고 web API에 대 한 요청을 사용 하 여 합니다.

## <a name="prerequisites"></a>전제 조건

다음은이 연습에 필요한입니다.

* [Microsoft Azure 구독](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio)
* [Visual Studio 2017](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs) (모든 버전)
* [Postman](https://www.getpostman.com/postman)

## <a name="create-the-azure-active-directory-b2c-tenant"></a>Azure Active Directory B2C 테 넌 트 만들기

Azure AD B2C 테 넌 트 만들기 [설명서에 설명 된 대로](/azure/active-directory-b2c/active-directory-b2c-get-started)합니다. 메시지가 표시 되 면 테 넌 트 Azure 구독과 연결 옵션인 경우이 자습서에 대 한

## <a name="configure-a-sign-up-or-sign-in-policy"></a>등록 또는 로그인 시 정책 구성

에 Azure AD B2C 설명서의 단계를 사용 하 여 [등록 또는 로그인 시 정책 만들기](/azure/active-directory-b2c/active-directory-b2c-reference-policies#create-a-sign-up-or-sign-in-policy)합니다. 정책 이름을 **SiUpIn**합니다.  에 대 한 설명서에 제공 된 예제 값을 사용 하 여 **Id 공급자**, **등록 특성**, 및 **응용 프로그램 클레임**합니다. 사용 하 여 **지금 실행** 설명서에 설명 된 대로 정책을 테스트 하려면 단추는 선택 사항입니다.

## <a name="register-the-api-in-azure-ad-b2c"></a>Azure AD B2C에 API를 등록 합니다.

새로 만든된 Azure AD B2C 테 넌 트에서 사용 하 여 API를 등록 [설명서에 나와 있는 단계](/azure/active-directory-b2c/active-directory-b2c-app-registration#register-a-web-api) 아래는 **web API 등록** 섹션.

다음 값을 사용 합니다.

| 설정                       | 값               | 노트                                                                                  |
|-------------------------------|---------------------|----------------------------------------------------------------------------------------|
| **이름**                      | *&lt;Api 앱 이름&gt;*  | 입력 한 **이름** 소비자에 게 앱을 설명 하는 앱에 대 한 합니다.                     |
| **웹 앱/웹 API** | 예                 |                                                                                        |
| **암시적 흐름 허용**       | 예                 |                                                                                        |
| **회신 URL**                 | `https://localhost` | 회신 Url은 Azure AD B2C 응용 프로그램을 요청 하는 모든 토큰을 반환 하는 위치 끝점입니다. |
| **앱 ID URI**                | *api*               | URI는 실제 주소로 확인할 필요가 없습니다. 만 고유 해야 합니다.     |
| **네이티브 클라이언트를 포함 합니다.**     | 아니요                  |                                                                                        |

API를 등록 한 후 테 넌 트의 앱 및 Api의 목록이 표시 됩니다. 방금 등록 된 API를 선택 합니다. 선택은 **복사** 아이콘의 오른쪽에는 **응용 프로그램 ID** 필드를 클립보드에 복사 합니다. 선택 **범위 게시** 기본 확인 하 고 *user_impersonation* 범위가 있는지 합니다.

## <a name="create-an-aspnet-core-app-in-visual-studio-2017"></a>Visual Studio 2017에서 ASP.NET Core 응용 프로그램 만들기

Visual Studio 웹 응용 프로그램 템플릿은 인증에 Azure AD B2C 테 넌 트를 사용 하도록 구성할 수 있습니다.

Visual Studio에서 합니다.

1. 새 ASP.NET Core 웹 응용 프로그램을 만듭니다. 
2. 선택 **웹 API** 템플릿 목록에서.
3. 선택 된 **인증 변경** 단추입니다.

    ![변경 인증 단추](./azure-ad-b2c-webapi/change-auth-button.png)

4. 에 **인증 변경** 대화 상자에서 **개별 사용자 계정**를 선택한 후 **클라우드의 기존 사용자 저장소에 연결** 드롭다운에 합니다. 

    ![변경 인증 대화 상자](./azure-ad-b2c-webapi/change-auth-dialog.png)

5. 다음 값을 갖는 양식을 작성 하 여:

    | 설정                       | 값                                                 |
    |-------------------------------|-------------------------------------------------------|
    | **도메인 이름**               | *&lt;B2C 테 넌 트의 도메인 이름&gt;*          |
    | **응용 프로그램 ID**            | *&lt;클립보드의 응용 프로그램 ID를 붙여 넣습니다.&gt;* |
    | **등록 또는 로그인 시 정책** | `B2C_1_SiUpIn`                                        |

    선택 **확인** 를 닫으려면는 **인증 변경** 대화 상자. 선택 **확인** 웹 앱을 만듭니다.

Visual Studio 라는 컨트롤러와 web API 만듭니다 *ValuesController.cs* GET 요청에 대 한 하드 코드 된 값을 반환 하는 합니다. 로 데코레이팅된 클래스의 [Authorize 특성](xref:security/authorization/simple)이므로 모든 요청 인증에 필요 합니다.

## <a name="run-the-web-api"></a>Web API를 실행 합니다.

Visual Studio에서 API를 실행 합니다. Visual Studio는 API 루트 URL을 가리키는 브라우저를 시작 합니다. 주소 표시줄에는 URL을 확인 하 고 백그라운드에서 실행 되는 API를 그대로 둡니다.

> [!NOTE]
> 루트 URL에 대해 정의 된 컨트롤러 없음 이므로 브라우저 404 (찾을 수 없음 페이지) 오류를 표시 합니다. 이는 예상된 동작입니다.

## <a name="use-postman-to-get-a-token-and-test-the-api"></a>우체부를 사용 하 여 테스트 하는 토큰을 가져오는 API

[우체부](https://getpostman.com/postman) Api 웹 테스트를 위한 도구입니다. 이 자습서에서는 우체부는 사용자 대신 웹 API에 액세스 하는 웹 앱을 시뮬레이션 합니다.

### <a name="register-postman-as-a-web-app"></a>웹 앱으로 우체부 등록

Azure AD B2C 테 넌 트의 토큰을 얻을 수 있는 웹 앱을 시뮬레이션 하는 우체부, 이후 테 넌 트에서 웹 응용 프로그램으로 등록 되어야 합니다. 사용 하 여 우체부 등록 [설명서에 나와 있는 단계](/azure/active-directory-b2c/active-directory-b2c-app-registration#register-a-web-app) 아래는 **웹 앱 등록** 섹션. 중지 된 **웹 응용 프로그램 클라이언트 암호를 만들** 섹션. 이 자습서에 대 한 클라이언트 암호는 필요 없습니다. 

다음 값을 사용 합니다.

| 설정                       | 값                            | 노트                           |
|-------------------------------|----------------------------------|---------------------------------|
| **이름**                      | 우체부                          |                                 |
| **웹 앱/웹 API** | 예                              |                                 |
| **암시적 흐름 허용**       | 예                              |                                 |
| **회신 URL**                 | `https://getpostman.com/postman` |                                 |
| **앱 ID URI**                | *&lt;비워&gt;*            | 이 자습서에 대 한 필요 하지 않습니다. |
| **네이티브 클라이언트를 포함 합니다.**     | 아니요                               |                                 |

새로 등록 된 웹 응용 프로그램에서 사용자 대신 web API에 액세스할 수 있는 권한이 필요 합니다.  

1. 선택 **우체부** 앱 선택한 후 목록에서 **API 액세스** 왼쪽 메뉴에서 합니다.
2. 선택 **+ 추가**합니다.
3. 에 **API 선택** 드롭다운에서 web API의 이름을 선택 합니다.
4. 에 **선택 범위** 드롭다운에서 모든 범위가 선택 되어 있는지 확인 합니다.
5. 선택 **확인**합니다.

전달자 토큰을 가져오는 데 필요한 것 처럼 우체부 응용 프로그램의 응용 프로그램 ID, note 합니다.

### <a name="create-a-postman-request"></a>우체부 요청 만들기

우체부를 시작 합니다. 기본적으로 우체부 표시는 **새로 만들기** 대화 시작 시. 대화 상자 표시 되어 있지 않으면 선택 된 **+ 새로 만들기** 왼쪽 위에 있는 단추입니다.

**새로 만들기** 대화 상자:

1. 선택 **요청**합니다.

    ![요청 단추](./azure-ad-b2c-webapi/postman-create-new.png)

2. 입력 *값 가져오기* 에 **요청 이름** 상자입니다.
3. 선택 **+ 모음 만들기** 요청을 저장 하기 위한 새 컬렉션을 만들 수 있습니다. 컬렉션 이름을 *ASP.NET Core 자습서* 한 다음 확인 표시를 선택 합니다.

    ![새 컬렉션 만들기](./azure-ad-b2c-webapi/postman-create-collection.png)

4. 선택 된 **ASP.NET Core 자습서로 저장** 단추입니다.

### <a name="test-the-web-api-without-authentication"></a>인증 없이 web API를 테스트 합니다.

웹 API에 인증이 필요한을 확인 하려면 먼저 인증 없이 요청을 확인 합니다.

1. 에 **요청 URL을 입력** 상자에 대 한 URL을 입력 합니다 `ValuesController`합니다. URL이 사용 하 여 브라우저에 표시 된 것과 동일 **api/값** 추가 됩니다. 예를 들어 `https://localhost:44375/api/values`합니다.
2. 선택 된 **보낼** 단추입니다.
3. 응답의 상태는 *401 권한 없음*합니다.

    ![401 권한 없는 응답](./azure-ad-b2c-webapi/postman-401-status.png)

### <a name="obtain-a-bearer-token"></a>전달자 토큰을 가져올

Web API에 인증 된 요청을 하려면 전달자 토큰은 필요 합니다. 우체부를 통해 Azure AD B2C 테 넌 트에 로그인 하 고 토큰을 가져올 수 있습니다.

1. 에 **권한 부여** 탭에 **형식** 드롭다운 **OAuth 2.0**합니다. 에 **권한 부여 데이터를 추가할** 드롭다운 **요청 헤더**합니다. 선택 **새 액세스 토큰 가져오기**합니다.

    ![설정 사용 하 여 권한 부여 탭](./azure-ad-b2c-webapi/postman-auth-tab.png)

2. 완료 된 **새 액세스 토큰 가져오기** 다음과 같이 대화 상자:


   |                설정                 |                                             값                                             |                                                                                                                                    노트                                                                                                                                     |
   |----------------------------------------|-----------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |      <strong>토큰 이름</strong>       |                                  <em>&lt;토큰 이름&gt;</em>                                  |                                                                                                                   토큰에 대 한 설명이 포함 된 이름을 입력 합니다.                                                                                                                    |
   |      <strong>Grant 유형</strong>       |                                           암시적 방법                                            |                                                                                                                                                                                                                                                                              |
   |     <strong>콜백 URL</strong>      |                               `https://getpostman.com/postman`                                |                                                                                                                                                                                                                                                                              |
   |       <strong>인증 URL</strong>        | `https://login.microsoftonline.com/<tenant domain name>/oauth2/v2.0/authorize?p=B2C_1_SiUpIn` |                                                                                                  대체 <em>&lt;테 넌 트 도메인 이름&gt;</em> 테 넌 트의 도메인 이름을 사용 합니다.                                                                                                  |
   |       <strong>클라이언트 ID</strong>       |                <em>&lt;우체부 응용 프로그램의 입력 <b>응용 프로그램 ID</b>&gt;</em>                 |                                                                                                                                                                                                                                                                              |
   |     <strong>클라이언트 암호</strong>     |                                 <em>&lt;비워&gt;</em>                                  |                                                                                                                                                                                                                                                                              |
   |         <strong>범위</strong>         |         `https://<tenant domain name>/<api>/user_impersonation openid offline_access`         | 대체 <em>&lt;테 넌 트 도메인 이름&gt;</em> 테 넌 트의 도메인 이름을 사용 합니다. 대체 <em>&lt;api&gt;</em> 웹 API 프로젝트 이름으로 합니다. 응용 프로그램 id입니다. 사용할 수도 있습니다. URL에 대 한 패턴은: <em>https://{tenant}.onmicrosoft.com/{app_name_or_id}/{scope 이름}</em>합니다. |
   | <strong>클라이언트 인증</strong> |                                본문에 클라이언트 자격 증명 보내기                                |                                                                                                                                                                                                                                                                              |


3. 선택 된 **토큰 요청** 단추입니다.

4. 우체부 대화 상자에서 Azure AD B2C 테 넌 트의 기호를 포함 하는 새 창을 엽니다. (하나는 정책을 테스트 생성) 하는 경우 기존 계정으로 로그인 하거나 선택 **지금 등록** 새 계정을 만들 수 있습니다. **암호를 잊으셨습니까?** 링크는 잊어버린된 암호를 재설정 하는 데 사용 됩니다.

5. 성공적으로 로그인 한 후 창이 닫히고 및 **관리 액세스 토큰** 대화 상자가 나타납니다. 선택 되며 맨 아래까지 아래로 스크롤합니다는 **사용 토큰** 단추입니다.

    !["토큰 사용" 단추를 찾을 수 있는 위치](./azure-ad-b2c-webapi/postman-access-token.png)

### <a name="test-the-web-api-with-authentication"></a>인증을 사용 하 여 웹 API를 테스트 합니다.

선택의 **보낼** 단추 요청을 다시 보낼 수 있습니다. 이 경우 응답 상태는 *200 확인* JSON 페이로드는 응답에 표시 되 고 **본문** 탭 합니다.

![페이로드 및 성공 상태](./azure-ad-b2c-webapi/postman-success.png)

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음 방법을 학습했습니다.

> [!div class="checklist"]
> * Azure Active Directory B2C 테 넌 트를 만듭니다.
> * Azure AD B2C에 Web API를 등록 합니다.
> * 인증을 위해 Azure AD B2C 테 넌 트를 사용 하도록 구성 된 웹 API 키를 만들려면 Visual Studio를 사용 합니다.
> * Azure AD B2C 테 넌 트의 동작을 제어 하는 정책을 구성 합니다.
> * 사용 하 여 우체부는 로그인 대화 상자를 표시 하는 웹 앱을 시뮬레이션 하는 토큰을 검색 하 고 web API에 대 한 요청을 사용 하 여 합니다.

학습 하 여 API 개발을 계속 합니다.

* [ASP.NET Core 웹 앱을 Azure AD B2C를 사용 하 여 보안](xref:security/authentication/azure-ad-b2c)합니다.
* [Azure AD B2C를 사용 하 여.NET 웹 앱에서.NET web API를 호출](/azure/active-directory-b2c/active-directory-b2c-devquickstarts-web-api-dotnet)합니다.
* [Azure AD B2C 사용자 인터페이스 사용자 지정](/azure/active-directory-b2c/active-directory-b2c-reference-ui-customization)합니다.
* [암호 복잡성 요구 사항을 구성](/azure/active-directory-b2c/active-directory-b2c-reference-password-complexity)합니다.
* [Multi-factor authentication 사용](/azure/active-directory-b2c/active-directory-b2c-reference-mfa)합니다.
* 추가 id 공급자와 같은 구성 [Microsoft](/azure/active-directory-b2c/active-directory-b2c-setup-msa-app), [Facebook](/azure/active-directory-b2c/active-directory-b2c-setup-fb-app), [Google](/azure/active-directory-b2c/active-directory-b2c-setup-goog-app), [Amazon](/azure/active-directory-b2c/active-directory-b2c-setup-amzn-app), [Twitter ](/azure/active-directory-b2c/active-directory-b2c-setup-twitter-app), 등입니다.
* [Azure AD Graph API를 사용 하 여](/azure/active-directory-b2c/active-directory-b2c-devquickstarts-graph-dotnet) Azure AD B2C 테 넌 트에서 그룹 구성원 자격 등의 추가 사용자 정보를 검색 합니다.
