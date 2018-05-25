---
title: 일반 데이터 보호 규정 (GDPR)에서 ASP.NET Core 지원
author: rick-anderson
description: 웹 응용 프로그램에서 ASP.NET Core GDPR 확장 지점에 액세스 하는 방법을 보여 줍니다.
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.date: 5/29/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/gdpr
ms.openlocfilehash: 3adfd1703dbf6446356886a662168bf1dbf65d56
ms.sourcegitcommit: 300a1127957dcdbce1b6ad79a7b9dc676f571510
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2018
---
# <a name="eu-general-data-protection-regulation-gdpr-support-in-aspnet-core"></a>ASP.NET Core의 EU 일반 데이터 보호 규정 (GDPR) 지원

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)

ASP.NET Core Api 및 서식 파일 중 일부를 충족 하기 위해 제공 된 [UE 일반 데이터 보호 규정 (GDPR)](https://www.eugdpr.org/) 요구 사항:

* 프로젝트 템플릿 등이 확장점 스텁된 태그 개인 정보 및 쿠키 사용 정책으로 바꿀 수 있습니다.
* 쿠키 동의 기능을 사용 하면 동의 요청 (및 추적할) 사용자가 개인 정보를 저장 합니다. 사용자가 데이터 수집에 동의 하지 및 응용 프로그램으로 설정 된 경우 [CheckConsentNeeded](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions.checkconsentneeded?view=aspnetcore-2.1#Microsoft_AspNetCore_Builder_CookiePolicyOptions_CheckConsentNeeded) 를 `true`, 브라우저에 필수적이 지 않은 쿠키를 전송 되지 것입니다.
* 기본적인 쿠키를 표시할 수 있습니다. 필수 쿠키는 사용자가 동의 하지 추적을 사용할 수 없습니다. 경우에 브라우저에 전송 됩니다.
* [TempData 및 세션 쿠키](#tempdata) 추적을 사용 하지 않도록 설정 하는 경우에 작동 하지 않습니다.
* [Identity 관리](#pd) 페이지를 다운로드 하 여 사용자 데이터를 삭제 한 링크를 제공 합니다.

[샘플 응용 프로그램](https://github.com/aspnet/Docs/tree/live/aspnetcore/security/gdpr) GDPR 확장점 및 ASP.NET Core 2.1 서식 파일에 추가 하는 Api의 대부분을 테스트할 수 있습니다. 참조는 [ReadMe](https://github.com/aspnet/Docs/tree/live/aspnetcore/security/gdpr) 지침을 테스트 하기 위한 파일입니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/live/aspnetcore/security/gdpr)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

## <a name="aspnet-core-gdpr-support-in-template-generated-code"></a>생성 된 코드 서식 파일에서 ASP.NET Core GDPR 지원

Razor 페이지 및 MVC 프로젝트 템플릿을 사용 하 여 만든 프로젝트에는 다음 GDPR 지원을 포함 합니다.

* [CookiePolicyOptions](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions?view=aspnetcore-2.0) 및 [UseCookiePolicy](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyappbuilderextensions.usecookiepolicy?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_CookiePolicyAppBuilderExtensions_UseCookiePolicy_Microsoft_AspNetCore_Builder_IApplicationBuilder_) 에 설정 된 `Startup`합니다.
* *_CookieConsentPartial.cshtml* [부분 뷰](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper)합니다.
* *Pages/Privacy.cshtml* 또는 *Home/rivacy.cshtml* 보기 사이트의 개인 정보 취급 방침에 자세히 설명 하는 페이지를 제공 합니다. *_CookieConsentPartial.cshtml* 파일 개인 정보 페이지에 대 한 링크를 생성 합니다.
* 개별 사용자 계정을 사용 하 여 만든 응용 프로그램에 대 한 관리 페이지를 다운로드 하 여 삭제는 링크를 제공 [개인 사용자 데이터](#pd)합니다.

### <a name="cookiepolicyoptions-and-usecookiepolicy"></a>CookiePolicyOptions 및 UseCookiePolicy

[CookiePolicyOptions](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions?view=aspnetcore-2.0) 에서 초기화 되는 `Startup` 클래스 `ConfigureServices` 메서드:

[!code-csharp[Main](gdpr/sample/Startup.cs?name=snippet1&highlight=14-20)]

[UseCookiePolicy](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyappbuilderextensions.usecookiepolicy?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_CookiePolicyAppBuilderExtensions_UseCookiePolicy_Microsoft_AspNetCore_Builder_IApplicationBuilder_) 에서 호출 되는 `Startup` 클래스 `Configure` 메서드:

[!code-csharp[Main](gdpr/sample/Startup.cs?name=snippet1&highlight=49)]

### <a name="cookieconsentpartialcshtml-partial-view"></a>_CookieConsentPartial.cshtml 부분 뷰

*_CookieConsentPartial.cshtml* 부분 뷰:

[!code-html[Main](gdpr/sample/RP/Pages/Shared/_CookieConsentPartial.cshtml)]

이 부분:

* 사용자에 대 한 추적의 상태를 가져옵니다. 응용 프로그램의 동의 요구 하도록 구성 된 경우 사용자는 쿠키를 추적 하려면 먼저 동의 해야 합니다. 쿠키 동의 크롬에서 만든 탐색 모음의 맨 위에 고정 되어 동의가 필요한 경우는 *Pages/Shared/_Layout.cshtml* 파일입니다.
* HTML 제공 `<p>` 정책을 사용 하 여 개인 정보 및 쿠키를 요약 하는 요소입니다.
* 에 대 한 링크도 *Pages/Privacy.cshtml* 사이트의 개인 정보 취급 방침을 자세히 수 있습니다.

## <a name="essential-cookies"></a>필수 쿠키

동의 적용 되지 않은 경우 브라우저에 필수로 표시 하는 쿠키만 전송 됩니다. 다음 코드에서는 쿠키를 필수:

[!code-csharp[Main](gdpr/sample/RP/Pages/Cookie.cshtml.cs?name=snippet1&highlight=5)]

<a name="tempdata"></a>

## <a name="tempdata-provider-and-session-state-cookies-are-not-essential"></a>Tempdata 공급자 및 세션 상태 쿠키 중요 하지 않은 경우

[Tempdata 공급자](xref:fundamentals/app-state#tempdata) 쿠키가 중요 하지 않습니다. 추적을 해제 하면 Tempdata 공급자 작동 하지 않습니다. 추적 사용 불가능 Tempdata 공급자를 사용 하려면 TempData로 표시할지 필수적인 `ConfigureServices`:

[!code-csharp[Main](gdpr/sample/RP/Startup.cs?name=snippet1)]

[세션 상태](xref:fundamentals/app-state) 쿠키는 중요 하지 않습니다. 추적을 사용할 수 없습니다. 세션 상태 작동 하지 않습니다.

<a name="pd"></a>

## <a name="personal-data"></a>개인 데이터

개별 사용자 계정을 사용 하 여 만든 ASP.NET Core 응용 프로그램을 다운로드 하 고 개인 데이터를 삭제 하는 코드를 포함 합니다.

사용자 이름을 선택한 다음 선택 **개인 데이터**:

![개인 데이터 페이지 관리](gdpr/_static/pd.png)

메모:

* 생성 하는 `Account/Manage` 코드 참조, [스 캐 폴드 Identity](xref:security/authentication/scaffold-identity)합니다.
* 삭제 하 고 영향 기본 id 데이터를 다운로드 합니다. 앱 사용자 지정 사용자 데이터 만들기 삭제/다운로드 사용자 지정 사용자 데이터를 확장 해야 합니다. GitHub 문제 [Id에 사용자 지정 사용자 데이터를 추가/삭제 하는 방법을](https://github.com/aspnet/Docs/issues/6226) 사용자 지정/삭제/다운로드 사용자 지정 사용자 데이터를 만드는 방법에 제안 된 문서를 추적 합니다. 우선 순위를 지정 하는 항목을 참조 하려는 경우에 문제에 반응을 엄지 둡니다.
* Id 데이터베이스 테이블에 저장 된 사용자에 대 한 토큰을 저장 `AspNetUserTokens` 사용자로 인해 연계 삭제 동작을 통해 삭제 될 때 삭제 되는 [외래 키](https://github.com/aspnet/Identity/blob/b4fc72c944e0589a7e1f076794d7e5d8dcf163bf/src/EF/IdentityUserContext.cs#L152)합니다.

## <a name="encryption-at-rest"></a>미사용 데이터 암호화

일부 데이터베이스와 저장 메커니즘을 미사용 데이터 암호화에 대 한 허용 합니다. 미사용 데이터 암호화:

* 저장 된 데이터를 자동으로 암호화합니다.
* 구성, 프로그래밍, 또는 데이터에 액세스 하는 소프트웨어에 대 한 다른 작업 없이 암호화 합니다.
* 쉽고 안전한 옵션이입니다.
* 데이터베이스를 키와 암호화를 관리할 수 있습니다.

예를 들어:

* Microsoft SQL 및 Azure SQL 제공 [투명 한 데이터 암호화](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption?view=sql-server-2017) (TDE).
* [기본적으로 데이터베이스를 암호화 하는 SQL Azure](https://azure.microsoft.com/en-us/updates/newly-created-azure-sql-databases-encrypted-by-default/)
* [기본적으로 암호화 되어 azure Blob, 파일, 테이블 및 큐 저장소](https://azure.microsoft.com/en-us/blog/announcing-default-encryption-for-azure-blobs-files-table-and-queue-storage/)합니다.

기본 제공 암호화를 제공 하지 않는 데이터베이스에 대 한 동일한 보호를 제공 하 디스크 암호화를 사용할 수 있습니다. 예를 들어:

* [Windows 서버에 대 한 Bitlocker](https://docs.microsoft.com/en-us/windows/security/information-protection/bitlocker/bitlocker-how-to-deploy-on-windows-server)
* Linux:
  * [eCryptfs](https://launchpad.net/ecryptfs)
  * [EncFS](https://github.com/vgough/encfs)합니다.

## <a name="additional-resources"></a>추가 자료

* [Microsoft.com/GDPR](https://www.microsoft.com/en-us/trustcenter/Privacy/GDPR)