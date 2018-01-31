---
title: "클라우드 인증을 Azure Active Directory B2C"
author: camsoper
description: "ASP.NET Core와 Azure Active Directory B2C 인증을 설정 하는 방법을 알아봅니다."
manager: wpickett
ms.date: 01/25/2018
ms.topic: tutorial
ms.technology: aspnet
ms.prod: asp.net-core
ms.custom: mvc
uid: security/authentication/azure-ad-b2c
ms.openlocfilehash: d60698b5798e837a5946dbe158a647aae9e149d4
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="cloud-authentication-with-azure-active-directory-b2c"></a>클라우드 인증을 Azure Active Directory B2C

작성자: [Cam Soper](https://twitter.com/camsoper)

[Azure Active Directory B2C](/azure/active-directory-b2c/active-directory-b2c-overview) (Azure AD B2C)는 웹 및 모바일 앱에 대 한 클라우드 id 관리 솔루션입니다. 서비스는 클라우드 및 온-프레미스에서 호스트 되는 앱에 대 한 인증을 제공 합니다. 인증 형식에는 엔터프라이즈 계정을 페더레이션 및 개별 계정, 소셜 네트워크 계정을 포함 합니다. 또한 Azure AD B2C 최소 구성으로 다단계 인증을 제공할 수 있습니다.

> [!TIP]
> Azure Active Directory (Azure AD) Azure AD B2C 별도 제품이 제공 됩니다. Azure AD 테 넌 트 조직을 나타내고 Azure AD B2C 테 넌 트를 신뢰 당사자 응용 프로그램과 함께 사용할 id의 컬렉션을 나타냅니다. 자세한 내용은 참고 [Azure AD B2C: 질문과 대답 (FAQ)](/azure/active-directory-b2c/active-directory-b2c-faqs)합니다.

이 자습서에 설명 하는 방법:

> [!div class="checklist"]
> * Azure Active Directory B2C 테 넌 트 만들기
> * Azure AD B2C에 앱을 등록
> * Visual Studio를 사용 하 여 인증을 위해 Azure AD B2C 테 넌 트를 사용 하도록 구성 된 ASP.NET Core 웹 응용 프로그램을 만들려면
> * Azure AD B2C 테 넌 트의 동작을 제어 하는 정책 구성

## <a name="prerequisites"></a>필수 구성 요소

다음은이 연습에 필요한입니다.

* [Microsoft Azure 구독](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio)
* [Visual Studio 2017](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs) (모든 버전)

## <a name="create-the-azure-active-directory-b2c-tenant"></a>Azure Active Directory B2C 테 넌 트 만들기

Azure Active Directory B2C 테 넌 트 만들기 [설명서에 설명 된 대로](/azure/active-directory-b2c/active-directory-b2c-get-started)합니다. 메시지가 표시 되 면 테 넌 트 Azure 구독과 연결 옵션인 경우이 자습서에 대 한

## <a name="register-the-app-in-azure-ad-b2c"></a>Azure AD B2C에 응용 프로그램을 등록 합니다.

새로 만든된 Azure AD B2C 테 넌 트에서 사용 하 여 앱을 등록 [설명서에 나와 있는 단계](/azure/active-directory-b2c/active-directory-b2c-app-registration#register-a-web-app) 아래는 **웹 앱 등록** 섹션. 중지 된 **웹 응용 프로그램 클라이언트 암호를 만들** 섹션. 이 자습서에 대 한 클라이언트 암호는 필요 없습니다. 

다음 값을 사용 합니다.

| 설정                       | 값                     | 노트                                                                                                                                                                                              |
|-------------------------------|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **이름**                      | *&lt;응용 프로그램 이름&gt;*        | 입력 한 **이름** 소비자에 게 앱을 설명 하는 앱에 대 한 합니다.                                                                                                                                 |
| **웹 앱/웹 API** | 예                       |                                                                                                                                                                                                    |
| **암시적 흐름 허용**       | 예                       |                                                                                                                                                                                                    |
| **회신 URL**                 | `https://localhost:44300` | 회신 Url은 Azure AD B2C 응용 프로그램을 요청 하는 모든 토큰을 반환 하는 위치 끝점입니다. Visual Studio를 사용 하 여 회신 URL을 제공 합니다. 지금은 입력 `https://localhost:44300` 양식을 완성 하 합니다. |
| **앱 ID URI**                | 비워               | 이 자습서에 대 한 필요 하지 않습니다.                                                                                                                                                                    |
| **네이티브 클라이언트를 포함 합니다.**     | 아니요                        |                                                                                                                                                                                                    |

> [!WARNING]
> 경우 고려해 야 localhost가 아닌 회신 URL을 설정는 [회신 URL 목록에 허용 되는 제약 조건을](/azure/active-directory-b2c/active-directory-b2c-app-registration#choosing-a-web-app-or-api-reply-url)합니다. 

앱을 등록 한 후 테 넌 트에 있는 앱의 목록이 표시 됩니다. 방금 등록 된 응용 프로그램을 선택 합니다. 선택은 **복사** 아이콘의 오른쪽에는 **응용 프로그램 ID** 필드를 클립보드에 복사 합니다.

아무 것도 더 이번에 Azure AD B2C 테 넌 트에 구성할 수 있지만 브라우저 창을 열어 둡니다. ASP.NET Core 응용 프로그램을 만든 후 더 복잡 한 구성이 있습니다.

## <a name="create-an-aspnet-core-app-in-visual-studio-2017"></a>Visual Studio 2017에서 ASP.NET Core 응용 프로그램 만들기

Visual Studio 웹 응용 프로그램 템플릿은 인증에 Azure AD B2C 테 넌 트를 사용 하도록 구성할 수 있습니다.

Visual Studio에서 합니다.

1. 새 ASP.NET Core 웹 응용 프로그램을 만듭니다. 
2. 선택 **웹 응용 프로그램** 템플릿 목록에서.
3. 선택 된 **인증 변경** 단추입니다.
    
    ![변경 인증 단추](./azure-ad-b2c/_static/changeauth.png)

4. 에 **인증 변경** 대화 상자에서 **개별 사용자 계정**를 선택한 후 **클라우드의 기존 사용자 저장소에 연결** 드롭다운에 합니다. 
    
    ![변경 인증 대화 상자](./azure-ad-b2c/_static/changeauthdialog.png)

5. 다음 값을 갖는 양식을 작성 하 여:
    
    | 설정                       | 값                                                 |
    |-------------------------------|-------------------------------------------------------|
    | **도메인 이름**               | *&lt;B2C 테 넌 트의 도메인 이름&gt;*          |
    | **응용 프로그램 ID**            | *&lt;클립보드의 응용 프로그램 ID를 붙여 넣습니다.&gt;* |
    | **콜백 경로**             | *&lt;기본값을 사용 하 여&gt;*                       |
    | **등록 또는 로그인 시 정책** | `B2C_1_SiUpIn`                                        |
    | **암호 재설정 정책**     | `B2C_1_SSPR`                                          |
    | **프로필 정책 편집**       | *&lt;비워&gt;*                                 |
    
    선택의 **복사** 옆에 연결 **회신 URI** 회신 URI를 클립보드에 복사 합니다. 선택 **확인** 를 닫으려면는 **인증 변경** 대화 상자. 선택 **확인** 웹 앱을 만듭니다.

## <a name="finish-the-b2c-app-registration"></a>B2C 앱 등록 완료

B2C 앱 속성이 계속 열려 있는 브라우저 창으로 돌아갑니다. 임시 변경 **회신 URL** Visual Studio에서 복사한 이전 값으로 지정 합니다. 선택 **저장** 창의 위쪽에 있습니다.

> [!TIP]
> 회신 URL을 복사 하지 않은 웹 프로젝트 속성의 디버그 탭에서 SSL 주소를 사용 하 고 추가 **CallbackPath** 에서 값 *appsettings.json*합니다.

## <a name="configure-policies"></a>정책 구성

에 Azure AD B2C 설명서의 단계를 사용 [등록 또는 로그인 시 정책 만들기](/azure/active-directory-b2c/active-directory-b2c-reference-policies#create-a-sign-up-or-sign-in-policy), 차례로 [암호 재설정 정책 만들기](/azure/active-directory-b2c/active-directory-b2c-reference-policies#create-a-password-reset-policy)합니다. 에 대 한 설명서에 제공 된 예제 값을 사용 하 여 **Id 공급자**, **등록 특성**, 및 **응용 프로그램 클레임**합니다. 사용 하 여 **지금 실행** 설명서에 설명 된 대로 정책을 테스트 하려면 단추는 선택 사항입니다.

> [!WARNING]
> 정책 이름에 해당 정책을 사용한 같이 문서에 설명 된 대로 정확 하 게이 확인은 **인증 변경** Visual Studio에서 대화 상자. 정책 이름을 확인할 수 있습니다 *appsettings.json*합니다.

## <a name="run-the-app"></a>앱 실행

키를 눌러 Visual Studio에서 **F5** 작성 하 고 응용 프로그램을 실행 합니다. 웹 앱이 시작 된 후에 선택 **로그인**합니다.

![응용 프로그램에 로그인](./azure-ad-b2c/_static/signin.png)

브라우저에서 Azure AD B2C 테 넌 트에 이동 합니다. (하나는 정책을 테스트 생성) 하는 경우 기존 계정으로 로그인 하거나 선택 **지금 등록** 새 계정을 만들 수 있습니다. **암호를 잊으셨습니까?** 링크는 잊어버린된 암호를 재설정 하는 데 사용 됩니다.

![Azure AD B2C 로그인](./azure-ad-b2c/_static/b2csts.png)

성공적으로 로그인 한 후 브라우저에서 웹 앱으로 이동 합니다.

![성공](./azure-ad-b2c/_static/success.png)

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음 방법을 학습했습니다.

> [!div class="checklist"]
> * Azure Active Directory B2C 테 넌 트 만들기
> * Azure AD B2C에 앱을 등록
> * Visual Studio를 사용 하 여 인증을 위해 Azure AD B2C 테 넌 트를 사용 하도록 구성 된 ASP.NET Core 웹 응용 프로그램을 만들려면
> * Azure AD B2C 테 넌 트의 동작을 제어 하는 정책 구성

ASP.NET Core 응용 프로그램은 인증을 위해 Azure AD B2C를 사용 하도록 구성 하는 [Authorize 특성](xref:security/authorization/simple) 응용 프로그램 보안에 사용할 수 있습니다. 학습 하 여 응용 프로그램 개발을 계속 진행 합니다.

* [Azure AD B2C 사용자 인터페이스 사용자 지정](/azure/active-directory-b2c/active-directory-b2c-reference-ui-customization)합니다.
* [암호 복잡성 요구 사항을 구성](/azure/active-directory-b2c/active-directory-b2c-reference-password-complexity)합니다.
* [Multi-factor authentication 사용](/azure/active-directory-b2c/active-directory-b2c-reference-mfa)합니다.
* 추가 id 공급자와 같은 구성 [Microsoft](/azure/active-directory-b2c/active-directory-b2c-setup-msa-app), [Facebook](/azure/active-directory-b2c/active-directory-b2c-setup-fb-app), [Google](/azure/active-directory-b2c/active-directory-b2c-setup-goog-app), [Amazon](/azure/active-directory-b2c/active-directory-b2c-setup-amzn-app), [Twitter ](/azure/active-directory-b2c/active-directory-b2c-setup-twitter-app), 등입니다.
* [Azure AD Graph API를 사용 하 여](/azure/active-directory-b2c/active-directory-b2c-devquickstarts-graph-dotnet) Azure AD B2C 테 넌 트에서 그룹 구성원 자격 등의 추가 사용자 정보를 검색 합니다.
* [ASP.NET Core Azure AD B2C를 사용 하 여 웹 API 보안](xref:security/authentication/azure-ad-b2c-api)합니다.
* [Azure AD B2C를 사용 하 여.NET 웹 앱에서.NET web API를 호출](/azure/active-directory-b2c/active-directory-b2c-devquickstarts-web-api-dotnet)합니다.
