---
uid: mvc/overview/getting-started/mvc-learning-sequence
title: MVC 권장 자습서 및 기사 | Microsoft Docs
author: Rick-Anderson
description: 이 페이지는 ASP.NET MVC 자습서 및 이러한 규칙에 따라 제안 된 시퀀스에 대 한 링크를 포함 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/22/2015
ms.topic: article
ms.assetid: 8513a57a-2d45-4d6b-881c-15a01c5cbb1c
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/mvc-learning-sequence
msc.type: authoredcontent
ms.openlocfilehash: 538eff2b2b2fdab5b0be879f0a5dfa5c9403b089
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
ms.locfileid: "28032643"
---
<a name="mvc-recommended-tutorials-and-articles"></a>MVC 자습서 및 문서를 권장 합니다.
====================
으로 [Rick Anderson](https://github.com/Rick-Anderson)

<a id="pwd"></a>
## <a name="getting-started"></a>시작

- [ASP.NET MVC 5 시작](introduction/getting-started.md) 이 11 시리즈는부터 시작 하는 것이 좋습니다.
- [ASP.NET MVC 5 기본 사항 Pluralsight](https://pluralsight.com/training/Player?author=scott-allen&amp;name=aspdotnet-mvc5-fundamentals-m1-introduction&amp;mode=live&amp;clip=0&amp;course=aspdotnet-mvc5-fundamentals) (비디오 과정)
- [ASP.NET MVC 소개](https://www.microsoftvirtualacademy.com/training-courses/introduction-to-asp-net-mvc) Jon Galloway 및 Christopher Harrison
- [ASP.NET 5 응용 프로그램의 수명 주기](lifecycle-of-an-aspnet-mvc-5-application.md) ASP.NET MVC 5 앱의 수명 주기를 차트를 PDF 문서.

<a id="con"></a>
## <a name="working-with-data"></a>데이터 작업

- [EF 6 Code First MVC 5를 사용 하 여 시작](getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) EF 심층적으로 시리즈 우세한 Tom Dykstra 수상 소개 합니다.

<a id="wj"></a>
## <a name="security"></a>보안

- [인증 및 SQL DB ASP.NET MVC 응용 프로그램을 만들고 Azure에 배포](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/) 인기 있는이 자습서에서는 간단한 응용 프로그램을 만들고 멤버 자격 및 역할을 추가 합니다.
- [Facebook, Twitter, LinkedIn 및 Google OAuth2 로그온에 ASP.NET MVC 5 앱 만들기](../security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 이 자습서는 OAuth 2.0을 사용 하 여 외부 인증의 자격 증명으로 사용자가 로그인 할 수 있도록 하는 ASP.NET MVC 5 웹 응용 프로그램을 작성 하는 방법을 보여줍니다. Facebook, Twitter, LinkedIn, Microsoft 또는 Google 같은 공급자입니다.
- [전자 메일 확인 및 암호 재설정에 대 한 로그와 함께 보안 ASP.NET MVC 5 웹 응용 프로그램 만들기](../security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) 먼저 Id에 일련의 코드가 포함 되어 [확인 링크를 다시 보낼](../security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md#rsend)합니다.
- [SMS 및 전자 메일 2 단계 인증을 사용 하는 ASP.NET MVC 5 앱](../security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md) Identity 시리즈에서 두 번째입니다.
- [ASP.NET 및 Azure App Service에 암호와 기타 중요한 데이터를 배포하는 방법에 대한 모범 사례](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)
- [SMS 및 전자 메일을 사용 하 여 ASP.NET Identity와 2 단계 인증](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) `isPersistent` 및 사용자가 로그온 수 하기 전에 유효성이 검사 된 전자 메일 계정을 보유 하는 코드를 보안 쿠키 SignInManager 2FA 요구 사항 등에 대 한 확인 하는 방법입니다.
- [계정 확인 및 ASP.NET Id와 암호 복구](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) 에서 찾을 수 없는 Id에 세부 정보를 제공 [전자 메일 확인 및 암호 재설정에 대 한 로그와 보안 ASP.NET MVC 5 웹 응용 프로그램을 만들](../security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) 수 있도록 하는 방법 등 사용자는 잊어버린된 암호 다시 설정 합니다.

<a id="da"></a>
## <a name="azure"></a>Azure

- [Azure에서 ASP.NET 웹 앱을 만들](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/) 짧고 간단한 자습서를 Azure에 배포 합니다.
- [인증 및 SQL DB ASP.NET MVC 응용 프로그램을 만들고 Azure에 배포](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)

<a id="perf"></a>
## <a name="performance-and-debugging"></a>성능 및 디버깅

- [Glimpse를 사용하여 ASP.NET MVC 앱 프로파일링 및 디버깅](../performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse.md)
