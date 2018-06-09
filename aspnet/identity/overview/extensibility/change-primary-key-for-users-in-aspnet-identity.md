---
uid: identity/overview/extensibility/change-primary-key-for-users-in-aspnet-identity
title: ASP.NET Identity에서 사용자에 대 한 기본 키를 변경 합니다. | Microsoft Docs
author: tfitzmac
description: Visual Studio 2013에서 기본 웹 응용 프로그램 사용자 계정에 대 한 키에 대 한 문자열 값을 사용합니다. ASP.NET Id를 사용 하면의 형식을 변경 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/30/2014
ms.topic: article
ms.assetid: 44925849-5762-4504-a8cd-8f0cd06f6dc3
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /identity/overview/extensibility/change-primary-key-for-users-in-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 79812efb4de2461fad3765d6005bbd20393e62b2
ms.sourcegitcommit: 6784510cfb589308c3875ccb5113eb31031766b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2018
ms.locfileid: "26498232"
---
<a name="change-primary-key-for-users-in-aspnet-identity"></a>ASP.NET Identity에서 사용자에 대 한 기본 키를 변경 합니다.
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

> Visual Studio 2013에서 기본 웹 응용 프로그램 사용자 계정에 대 한 키에 대 한 문자열 값을 사용합니다. ASP.NET Id를 사용 하면 데이터 요구 사항을 충족 하기 위해 키 유형을 변경할 수 있습니다. 예를 들어 키의 형식 문자열에서 정수로 변경할 수 있습니다.
> 
> 이 항목에서는 기본 웹 응용 프로그램 및 사용자 계정 키를 정수로 변경 방법을 보여 줍니다. 프로젝트에서 모든 유형의 키를 구현 하기 위해 수정에 사용할 수 있습니다. 기본 웹 응용 프로그램에서 이러한 변경을 수행 하는 방법을 보여 줍니다 하지만 사용자 지정된 응용 프로그램에 비슷한 수정 사항을 적용할 수 있습니다. MVC 또는 Web Forms에서 작업할 때 필요한 변경 사항을 보여 줍니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - Visual Studio 2013 업데이트 2 (또는 이상)
> - ASP.NET Identity 2.1 이상


이 자습서의 단계를 수행 하려면 Visual Studio 2013 업데이트 2 (또는 이상) 및 ASP.NET 웹 응용 프로그램 템플릿에서 만든 웹 응용 프로그램이 있어야 합니다. 업데이트 3에서 변경 하는 템플릿. 이 항목에서는 업데이트 2와 업데이트 3에서 서식 파일을 변경 하는 방법을 보여 줍니다.

이 항목에는 다음과 같은 단원이 포함되어 있습니다.

- [Id 사용자 클래스에서 키의 형식 변경](#userclass)
- [키 유형을 사용 하는 사용자 지정 된 Id 클래스 추가](#customclass)
- [키 유형을 사용 하는 상황에 맞는 클래스 및 사용자 관리자 변경](#context)
- [시작 키 유형을 사용 하는 구성 변경](#startup)
- [MVC 업데이트 2에 대 한 키 형식을 전달할 AccountController 변경](#mvcupdate2)
- [MVC 업데이트 3에 대 한 키 형식을 전달할 AccountController 및 ManageController 변경](#mvcupdate3)
- [업데이트 2의 Web Forms에 대 한 키 형식을 전달할 계정 페이지를 변경 합니다.](#webformsupdate2)
- [업데이트 3 Web Forms에 대 한 키 형식을 전달할 계정 페이지를 변경 합니다.](#webformsupdate3)
- [응용 프로그램 실행](#run)
- [기타 리소스](#other)

<a id="userclass"></a>
## <a name="change-the-type-of-the-key-in-the-identity-user-class"></a>Id 사용자 클래스에서 키의 형식 변경

ASP.NET 웹 응용 프로그램 템플릿에서 만들어진 프로젝트에 ApplicationUser 클래스는 정수를 사용 하 여 사용자 계정에 대 한 키를 지정 합니다. IdentityModels.cs, 변경의 형식을 갖는 IdentityUser 상속할 ApplicationUser 클래스 **int** TKey 제네릭 매개 변수입니다. 아직 구현 하지는 세 가지 사용자 지정 된 클래스의 이름을 전달할 수도 있습니다.

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample1.cs?highlight=1-2)]

키의 형식 변경 하지만 기본적으로 응용 프로그램의 나머지 부분은 여전히 가정 키는 문자열입니다. 명시적으로 문자열로 가정 하는 코드에서 키의 형식을 나타내야 합니다.

에 **ApplicationUser** 클래스, 변경의 **GenerateUserIdentityAsync** 메서드 아래 강조 표시 된 코드에 나와 있는 것 처럼 int를 포함 하도록 합니다. 이 변경 내용을 업데이트 3 템플릿 사용 하 여 Web Forms 프로젝트에 대 한 필요는 없습니다.

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample2.cs?highlight=2)]

<a id="customclass"></a>
## <a name="add-customized-identity-classes-that-use-the-key-type"></a>키 유형을 사용 하는 사용자 지정 된 Id 클래스 추가

IdentityUserRole, IdentityUserClaim, IdentityUserLogin, IdentityRole, UserStore, RoleStore, 등의 다른 Id 클래스는 여전히 문자열 키를 사용 하도록 설정 됩니다. 키에 대 한 정수를 지정 하는 이러한 클래스의 새 버전을 만듭니다. 이러한 클래스에 구현 코드를 제공할 필요가 없습니다, 주로 방금 int 키로 설정 합니다.

IdentityModels.cs 파일에 다음 클래스를 추가 합니다.

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample3.cs)]

<a id="context"></a>
## <a name="change-the-context-class-and-user-manager-to-use-the-key-type"></a>키 유형을 사용 하는 상황에 맞는 클래스 및 사용자 관리자 변경

IdentityModels.cs의 정의 변경는 **ApplicationDbContext** 클래스를 사용 하 여 새 클래스를 사용자 지정 및 **int** 강조 표시 된 코드에 표시 된 키에 대 한 합니다.

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample4.cs?highlight=1-2)]

ThrowIfV1Schema 매개 변수는 생성자에 더 이상 유효합니다. 생성자를 변경 하 여 ThrowIfV1Schema 값을 전달 하지 않습니다.

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample5.cs)]

IdentityConfig.cs을 열고 변경는 **ApplicationUserManger** 데이터 유지를 위한 클래스를 저장 하는 새 사용자를 사용 하는 클래스 및 **int** 키에 대 한 합니다.

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample6.cs?highlight=1,3,12,14,32,37,48)]

업데이트 3 템플릿을 ApplicationSignInManager 클래스를 변경 해야 합니다.

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample7.cs?highlight=1)]

<a id="startup"></a>
## <a name="change-start-up-configuration-to-use-the-key-type"></a>시작 키 유형을 사용 하는 구성 변경

Startup.Auth.cs, 아래 강조 표시 된 대로 OnValidateIdentity 코드를 대체 합니다. GetUserIdCallback 정의 문자열 값 구문 분석 하는 정수를 확인 합니다.

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample8.cs?highlight=7-12)]

프로젝트의 제네릭 구현을 인식 하지 못합니다는 **GetUserId** 메서드를 버전 2.1에는 ASP.NET Identity NuGet 패키지를 업데이트 해야 할 수 있습니다

ASP.NET Identity에서 사용 하는 인프라 클래스를 많이 변경 했습니다. 프로젝트 컴파일 시도 하면 많은 오류를 확인할 수 있습니다. 다행히 나머지 오류가 모두 비슷합니다. Id 클래스는 키에 대 한 정수 하는데 컨트롤러 (또는 Web Form)는 문자열 값을 전달 하는 있습니다. 각각의 경우에서 호출 하 여 문자열 및 정수 변환 해야 **GetUserId&lt;int&gt;** 합니다. 컴파일 오류 목록을 통해 작업 하거나 아래에 변경 내용에 따라 수 있습니다.

나머지 변경을 Visual Studio에 설치 된 업데이트를 만드는 프로젝트의 유형에 따라 달라 집니다. 다음 링크를 통해 관련 섹션으로 직접 이동할 수 있습니다.

- [MVC 업데이트 2에 대 한 키 형식을 전달할 AccountController 변경](#mvcupdate2)
- [MVC 업데이트 3에 대 한 키 형식을 전달할 AccountController 및 ManageController 변경](#mvcupdate3)
- [업데이트 2의 Web Forms에 대 한 키 형식을 전달할 계정 페이지를 변경 합니다.](#webformsupdate2)
- [업데이트 3 Web Forms에 대 한 키 형식을 전달할 계정 페이지를 변경 합니다.](#webformsupdate3)

<a id="mvcupdate2"></a>
## <a name="for-mvc-with-update-2-change-the-accountcontroller-to-pass-the-key-type"></a>MVC 업데이트 2에 대 한 키 형식을 전달할 AccountController 변경

AccountController.cs 파일을 엽니다. 다음 메서드를 변경 해야 합니다.

**ConfirmEmail** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample9.cs?highlight=1,3)]

**한 연결을 끊을** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample10.cs?highlight=5,9)]

**Manage(ManageUserViewModel)** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample11.cs?highlight=11,17,41)]

**LinkLoginCallback** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample12.cs?highlight=10)]

**RemoveAccountList** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample13.cs?highlight=3)]

**HasPassword** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample14.cs?highlight=3)]

이제 수 [응용 프로그램을 실행](#run) 새 사용자를 등록 하 고 있습니다.

<a id="mvcupdate3"></a>
## <a name="for-mvc-with-update-3-change-the-accountcontroller-and-managecontroller-to-pass-the-key-type"></a>MVC 업데이트 3에 대 한 키 형식을 전달할 AccountController 및 ManageController 변경

AccountController.cs 파일을 엽니다. 다음 메서드를 변경 해야 합니다.

**ConfirmEmail** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample15.cs?highlight=1,3)]

**SendCode** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample16.cs?highlight=4)]

ManageController.cs 파일을 엽니다. 다음 메서드를 변경 해야 합니다.

**인덱스** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample17.cs?highlight=15-17)]

**RemoveLogin** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample18.cs?highlight=3,13,17)]

**AddPhoneNumber** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample19.cs?highlight=9)]

**EnableTwoFactorAuthentication** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample20.cs?highlight=3-4)]

**DisableTwoFactorAuthentication** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample21.cs?highlight=3-4)]

**VerifyPhoneNumber** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample22.cs?highlight=4,18,21)]

**RemovePhoneNumber** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample23.cs?highlight=3,8)]

**ChangePassword** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample24.cs?highlight=10,13)]

**SetPassword** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample25.cs?highlight=5,8)]

**ManageLogins** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample26.cs?highlight=7,12)]

**LinkLoginCallback** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample27.cs?highlight=8)]

**HasPassword** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample28.cs?highlight=3)]

**HasPhoneNumber** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample29.cs?highlight=3)]

이제 수 [응용 프로그램을 실행](#run) 새 사용자를 등록 하 고 있습니다.

<a id="webformsupdate2"></a>
## <a name="for-web-forms-with-update-2-change-account-pages-to-pass-the-key-type"></a>업데이트 2의 Web Forms에 대 한 키 형식을 전달할 계정 페이지를 변경 합니다.

업데이트 2의 Web Forms에 대 한 다음 페이지를 변경 해야 합니다.

**Confirm.aspx.cx**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample30.cs?highlight=8)]

**RegisterExternalLogin.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample31.cs?highlight=36)]

**Manage.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample32.cs?highlight=3,22,47,52,69,85,93,98)]

이제 수 [응용 프로그램을 실행](#run) 새 사용자를 등록 하 고 있습니다.

<a id="webformsupdate3"></a>
## <a name="for-web-forms-with-update-3-change-account-pages-to-pass-the-key-type"></a>업데이트 3 Web Forms에 대 한 키 형식을 전달할 계정 페이지를 변경 합니다.

업데이트 3 Web Forms에 대 한 다음 페이지를 변경 해야 합니다.

**Confirm.aspx.cx**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample33.cs?highlight=8)]

**RegisterExternalLogin.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample34.cs?highlight=36)]

**Manage.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample35.cs?highlight=11,27,32,34,82,87,99,108)]

**VerifyPhoneNumber.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample36.cs?highlight=8,23,27)]

**AddPhoneNumber.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample37.cs?highlight=7)]

**ManagePassword.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample38.cs?highlight=11,47,50,68)]

**ManageLogins.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample39.cs?highlight=16,23,32,41,45)]

**TwoFactorAuthenticationSignIn.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample40.cs?highlight=14-15,29,53)]

<a id="run"></a>
## <a name="run-application"></a>응용 프로그램 실행

모든 기본 웹 응용 프로그램 템플릿에 필요한 변경 사항을 완료 했습니다. 응용 프로그램을 실행 하 고 새 사용자를 등록 합니다. 사용자를 등록 한 후 AspNetUsers 테이블에는 정수 Id 열에 알 수 있습니다.

![새 기본 키](change-primary-key-for-users-in-aspnet-identity/_static/image1.png)

이전에 만든 ASP.NET Identity 테이블 서로 다른 기본 키가 있는 경우 일부 변경 해야 합니다. 가능 하면 기존 데이터베이스를 삭제 하기만 합니다. 웹 응용 프로그램을 실행 하 고 새 사용자를 추가 하는 경우 데이터베이스와 올바른 디자인 다시 생성 됩니다. 삭제할 수 없는 경우, 테이블을 변경 하려면 code first 마이그레이션 실행 합니다. 그러나 새 정수 기본 키 되지 설정 됩니다는 데이터베이스에서 SQL IDENTITY 속성으로. Id 열의 ID로 수동으로 설정 해야 합니다.

<a id="other"></a>
## <a name="other-resources"></a>기타 리소스

- [ASP.NET ID에 대한 사용자 지정 저장소 공급자 개요](overview-of-custom-storage-providers-for-aspnet-identity.md)
- [기존 웹 사이트를 SQL 멤버 자격에서 ASP.NET ID로 마이그레이션](../migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md)
- [멤버 자격 및 ASP.NET Identity에 대 한 사용자 프로필에 대 한 유니버설 공급자 데이터 마이그레이션](../migrations/migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity.md)
- [샘플 응용 프로그램](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/ChangePK/readme.txt) 변경 된 기본 키가 있는
