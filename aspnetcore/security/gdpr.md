---
title: 일반 데이터 보호 규정 (GDPR)에서 ASP.NET Core 지원
author: rick-anderson
description: ASP.NET Core 웹 앱에서 GDPR 확장 지점에 액세스 하는 방법에 알아봅니다.
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.custom: mvc
ms.date: 05/29/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/gdpr
ms.openlocfilehash: c3c8a3fcd4a303aea65c57ff6be2ff0434383f33
ms.sourcegitcommit: 7e87671fea9a5f36ca516616fe3b40b537f428d2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35341927"
---
# <a name="eu-general-data-protection-regulation-gdpr-support-in-aspnet-core"></a><span data-ttu-id="24bd7-103">ASP.NET Core의 EU 일반 데이터 보호 규정 (GDPR) 지원</span><span class="sxs-lookup"><span data-stu-id="24bd7-103">EU General Data Protection Regulation (GDPR) support in ASP.NET Core</span></span>

<span data-ttu-id="24bd7-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="24bd7-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="24bd7-105">ASP.NET Core Api 및 서식 파일 중 일부를 충족 하기 위해 제공 된 [EU 일반 데이터 보호 규정 (GDPR)](https://www.eugdpr.org/) 요구 사항:</span><span class="sxs-lookup"><span data-stu-id="24bd7-105">ASP.NET Core provides APIs and templates to help meet some of the [EU General Data Protection Regulation (GDPR)](https://www.eugdpr.org/) requirements:</span></span>

* <span data-ttu-id="24bd7-106">프로젝트 템플릿 등이 확장점 스텁된 태그 개인 정보 및 쿠키 사용 정책으로 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24bd7-106">The project templates include extension points and stubbed markup you can replace with your privacy and cookie use policy.</span></span>
* <span data-ttu-id="24bd7-107">쿠키 동의 기능을 사용 하면 동의 요청 (및 추적할) 사용자가 개인 정보를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="24bd7-107">A cookie consent feature allows you to ask for (and track) consent from your users for storing personal information.</span></span> <span data-ttu-id="24bd7-108">사용자가 데이터 수집에 동의 하지 및 응용 프로그램으로 설정 된 경우 [CheckConsentNeeded](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions.checkconsentneeded) 를 `true`, 브라우저에 필수적이 지 않은 쿠키를 전송 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="24bd7-108">If a user has not consented to data collection and the app is set with [CheckConsentNeeded](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions.checkconsentneeded) to `true`, non-essential cookies will not be sent to the browser.</span></span>
* <span data-ttu-id="24bd7-109">기본적인 쿠키를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24bd7-109">Cookies can be marked as essential.</span></span> <span data-ttu-id="24bd7-110">필수 쿠키는 사용자가 동의 하지 추적을 사용할 수 없습니다. 경우에 브라우저에 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="24bd7-110">Essential cookies are sent to the browser even when the user has not consented and tracking is disabled.</span></span>
* <span data-ttu-id="24bd7-111">[TempData 및 세션 쿠키](#tempdata) 추적을 사용 하지 않도록 설정 하는 경우에 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="24bd7-111">[TempData and Session cookies](#tempdata) are not functional when tracking is disabled.</span></span>
* <span data-ttu-id="24bd7-112">[Identity 관리](#pd) 페이지를 다운로드 하 여 사용자 데이터를 삭제 한 링크를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="24bd7-112">The [Identity manage](#pd) page provides a link to download and delete user data.</span></span>

<span data-ttu-id="24bd7-113">[샘플 응용 프로그램](https://github.com/aspnet/Docs/tree/live/aspnetcore/security/gdpr/sample) GDPR 확장점 및 ASP.NET Core 2.1 서식 파일에 추가 하는 Api의 대부분을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24bd7-113">The [sample app](https://github.com/aspnet/Docs/tree/live/aspnetcore/security/gdpr/sample) lets you test most of the GDPR extension points and APIs added to the ASP.NET Core 2.1 templates.</span></span> <span data-ttu-id="24bd7-114">참조는 [ReadMe](https://github.com/aspnet/Docs/tree/live/aspnetcore/security/gdpr/sample) 지침을 테스트 하기 위한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="24bd7-114">See the [ReadMe](https://github.com/aspnet/Docs/tree/live/aspnetcore/security/gdpr/sample) file for testing instructions.</span></span>

<span data-ttu-id="24bd7-115">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/live/aspnetcore/security/gdpr/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="24bd7-115">[View or download sample code](https://github.com/aspnet/Docs/tree/live/aspnetcore/security/gdpr/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="aspnet-core-gdpr-support-in-template-generated-code"></a><span data-ttu-id="24bd7-116">생성 된 코드 서식 파일에서 ASP.NET Core GDPR 지원</span><span class="sxs-lookup"><span data-stu-id="24bd7-116">ASP.NET Core GDPR support in template generated code</span></span>

<span data-ttu-id="24bd7-117">Razor 페이지 및 MVC 프로젝트 템플릿을 사용 하 여 만든 프로젝트에는 다음 GDPR 지원을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="24bd7-117">Razor Pages and MVC projects created with the project templates include the following GDPR support:</span></span>

* <span data-ttu-id="24bd7-118">[CookiePolicyOptions](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions) 및 [UseCookiePolicy](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyappbuilderextensions.usecookiepolicy) 에 설정 된 `Startup`합니다.</span><span class="sxs-lookup"><span data-stu-id="24bd7-118">[CookiePolicyOptions](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions) and [UseCookiePolicy](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyappbuilderextensions.usecookiepolicy) are set in `Startup`.</span></span>
* <span data-ttu-id="24bd7-119">*_CookieConsentPartial.cshtml* [부분 뷰](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper)합니다.</span><span class="sxs-lookup"><span data-stu-id="24bd7-119">The *_CookieConsentPartial.cshtml* [partial view](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper).</span></span>
* <span data-ttu-id="24bd7-120">*Pages/Privacy.cshtml* 또는 *Home/Privacy.cshtml* 보기 사이트의 개인 정보 취급 방침에 자세히 설명 하는 페이지를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="24bd7-120">The *Pages/Privacy.cshtml* or *Home/Privacy.cshtml* view provides a page to detail your site's privacy policy.</span></span> <span data-ttu-id="24bd7-121">*_CookieConsentPartial.cshtml* 파일 개인 정보 페이지에 대 한 링크를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="24bd7-121">The *_CookieConsentPartial.cshtml* file generates a link to the privacy page.</span></span>
* <span data-ttu-id="24bd7-122">개별 사용자 계정을 사용 하 여 만든 응용 프로그램에 대 한 관리 페이지를 다운로드 하 여 삭제는 링크를 제공 [개인 사용자 데이터](#pd)합니다.</span><span class="sxs-lookup"><span data-stu-id="24bd7-122">For applications created with individual user accounts, the manage page provides links to download and delete [personal user data](#pd).</span></span>

### <a name="cookiepolicyoptions-and-usecookiepolicy"></a><span data-ttu-id="24bd7-123">CookiePolicyOptions 및 UseCookiePolicy</span><span class="sxs-lookup"><span data-stu-id="24bd7-123">CookiePolicyOptions and UseCookiePolicy</span></span>

<span data-ttu-id="24bd7-124">[CookiePolicyOptions](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions) 에서 초기화 되는 `Startup` 클래스 `ConfigureServices` 메서드:</span><span class="sxs-lookup"><span data-stu-id="24bd7-124">[CookiePolicyOptions](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions) are initialized in the `Startup` class `ConfigureServices` method:</span></span>

[!code-csharp[Main](gdpr/sample/Startup.cs?name=snippet1&highlight=14-20)]

<span data-ttu-id="24bd7-125">[UseCookiePolicy](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyappbuilderextensions.usecookiepolicy) 에서 호출 되는 `Startup` 클래스 `Configure` 메서드:</span><span class="sxs-lookup"><span data-stu-id="24bd7-125">[UseCookiePolicy](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyappbuilderextensions.usecookiepolicy) is called in the `Startup` class `Configure` method:</span></span>

[!code-csharp[Main](gdpr/sample/Startup.cs?name=snippet1&highlight=49)]

### <a name="cookieconsentpartialcshtml-partial-view"></a><span data-ttu-id="24bd7-126">_CookieConsentPartial.cshtml 부분 뷰</span><span class="sxs-lookup"><span data-stu-id="24bd7-126">_CookieConsentPartial.cshtml partial view</span></span>

<span data-ttu-id="24bd7-127">*_CookieConsentPartial.cshtml* 부분 뷰:</span><span class="sxs-lookup"><span data-stu-id="24bd7-127">The *_CookieConsentPartial.cshtml* partial view:</span></span>

[!code-html[Main](gdpr/sample/RP/Pages/Shared/_CookieConsentPartial.cshtml)]

<span data-ttu-id="24bd7-128">이 부분:</span><span class="sxs-lookup"><span data-stu-id="24bd7-128">This partial:</span></span>

* <span data-ttu-id="24bd7-129">사용자에 대 한 추적의 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="24bd7-129">Gets the state of tracking for the user.</span></span> <span data-ttu-id="24bd7-130">응용 프로그램의 동의 요구 하도록 구성 된 경우 사용자는 쿠키를 추적 하려면 먼저 동의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24bd7-130">If the application is configured to require consent the user must consent before cookies can be tracked.</span></span> <span data-ttu-id="24bd7-131">쿠키 동의 크롬에서 만든 탐색 모음의 맨 위에 고정 되어 동의가 필요한 경우는 *Pages/Shared/_Layout.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="24bd7-131">If consent is required, the cookie consent chrome is fixed on top of the navigation bar created in the *Pages/Shared/_Layout.cshtml* file.</span></span>
* <span data-ttu-id="24bd7-132">HTML 제공 `<p>` 정책을 사용 하 여 개인 정보 및 쿠키를 요약 하는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="24bd7-132">Provides an HTML `<p>` element to summarize your privacy and cookie use policy.</span></span>
* <span data-ttu-id="24bd7-133">에 대 한 링크도 *Pages/Privacy.cshtml* 사이트의 개인 정보 취급 방침을 자세히 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24bd7-133">Provides a link to *Pages/Privacy.cshtml* where you can detail your site's privacy policy.</span></span>

## <a name="essential-cookies"></a><span data-ttu-id="24bd7-134">필수 쿠키</span><span class="sxs-lookup"><span data-stu-id="24bd7-134">Essential cookies</span></span>

<span data-ttu-id="24bd7-135">동의 적용 되지 않은 경우 브라우저에 필수로 표시 하는 쿠키만 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="24bd7-135">If consent has not been given, only cookies marked essential are sent to the browser.</span></span> <span data-ttu-id="24bd7-136">다음 코드에서는 쿠키를 필수:</span><span class="sxs-lookup"><span data-stu-id="24bd7-136">The following code makes a cookie essential:</span></span>

[!code-csharp[Main](gdpr/sample/RP/Pages/Cookie.cshtml.cs?name=snippet1&highlight=5)]

<a name="tempdata"></a>

## <a name="tempdata-provider-and-session-state-cookies-are-not-essential"></a><span data-ttu-id="24bd7-137">Tempdata 공급자 및 세션 상태 쿠키 중요 하지 않은 경우</span><span class="sxs-lookup"><span data-stu-id="24bd7-137">Tempdata provider and session state cookies are not essential</span></span>

<span data-ttu-id="24bd7-138">[Tempdata 공급자](xref:fundamentals/app-state#tempdata) 쿠키가 중요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="24bd7-138">The [Tempdata provider](xref:fundamentals/app-state#tempdata) cookie is not essential.</span></span> <span data-ttu-id="24bd7-139">추적을 해제 하면 Tempdata 공급자 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="24bd7-139">If tracking is disabled, the Tempdata provider is not functional.</span></span> <span data-ttu-id="24bd7-140">추적 사용 불가능 Tempdata 공급자를 사용 하려면 TempData로 표시할지 필수적인 `ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="24bd7-140">To enable the Tempdata provider when tracking is disabled, mark the TempData cookie as essential in `ConfigureServices`:</span></span>

[!code-csharp[Main](gdpr/sample/RP/Startup.cs?name=snippet1)]

<span data-ttu-id="24bd7-141">[세션 상태](xref:fundamentals/app-state) 쿠키는 중요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="24bd7-141">[Session state](xref:fundamentals/app-state) cookies are not essential.</span></span> <span data-ttu-id="24bd7-142">추적을 사용할 수 없습니다. 세션 상태 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="24bd7-142">Session state is not functional when tracking is disabled.</span></span>

<a name="pd"></a>

## <a name="personal-data"></a><span data-ttu-id="24bd7-143">개인 데이터</span><span class="sxs-lookup"><span data-stu-id="24bd7-143">Personal data</span></span>

<span data-ttu-id="24bd7-144">개별 사용자 계정을 사용 하 여 만든 ASP.NET Core 응용 프로그램을 다운로드 하 고 개인 데이터를 삭제 하는 코드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="24bd7-144">ASP.NET Core applications created with individual user accounts include code to download and delete personal data.</span></span>

<span data-ttu-id="24bd7-145">사용자 이름을 선택한 다음 선택 **개인 데이터**:</span><span class="sxs-lookup"><span data-stu-id="24bd7-145">Select the user name and then select **Personal data**:</span></span>

![개인 데이터 페이지 관리](gdpr/_static/pd.png)

<span data-ttu-id="24bd7-147">메모:</span><span class="sxs-lookup"><span data-stu-id="24bd7-147">Notes:</span></span>

* <span data-ttu-id="24bd7-148">생성 하는 `Account/Manage` 코드 참조, [스 캐 폴드 Identity](xref:security/authentication/scaffold-identity)합니다.</span><span class="sxs-lookup"><span data-stu-id="24bd7-148">To generate the `Account/Manage` code, see [Scaffold Identity](xref:security/authentication/scaffold-identity).</span></span>
* <span data-ttu-id="24bd7-149">삭제 하 고 영향 기본 id 데이터를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="24bd7-149">Delete and download only impact the default identity data.</span></span> <span data-ttu-id="24bd7-150">앱 사용자 지정 사용자 데이터 만들기 삭제/다운로드 사용자 지정 사용자 데이터를 확장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24bd7-150">Apps the create custom user data must be extended to delete/download the custom user data.</span></span> <span data-ttu-id="24bd7-151">GitHub 문제 [Id에 사용자 지정 사용자 데이터를 추가/삭제 하는 방법을](https://github.com/aspnet/Docs/issues/6226) 사용자 지정/삭제/다운로드 사용자 지정 사용자 데이터를 만드는 방법에 제안 된 문서를 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="24bd7-151">GitHub issue [How to add/delete custom user data to Identity](https://github.com/aspnet/Docs/issues/6226) tracks a proposed article on creating custom/deleting/downloading custom user data.</span></span> <span data-ttu-id="24bd7-152">우선 순위를 지정 하는 항목을 참조 하려는 경우에 문제에 반응을 엄지 둡니다.</span><span class="sxs-lookup"><span data-stu-id="24bd7-152">If you'd like to see that topic prioritized, leave a thumbs up reaction in the issue.</span></span>
* <span data-ttu-id="24bd7-153">Id 데이터베이스 테이블에 저장 된 사용자에 대 한 토큰을 저장 `AspNetUserTokens` 사용자로 인해 연계 삭제 동작을 통해 삭제 될 때 삭제 되는 [외래 키](https://github.com/aspnet/Identity/blob/release/2.1/src/EF/IdentityUserContext.cs#L152)합니다.</span><span class="sxs-lookup"><span data-stu-id="24bd7-153">Saved tokens for the user that are stored in the Identity database table `AspNetUserTokens` are deleted when the user is deleted via the cascading delete behavior due to the [foreign key](https://github.com/aspnet/Identity/blob/release/2.1/src/EF/IdentityUserContext.cs#L152).</span></span>

## <a name="encryption-at-rest"></a><span data-ttu-id="24bd7-154">미사용 데이터 암호화</span><span class="sxs-lookup"><span data-stu-id="24bd7-154">Encryption at rest</span></span>

<span data-ttu-id="24bd7-155">일부 데이터베이스와 저장 메커니즘을 미사용 데이터 암호화에 대 한 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="24bd7-155">Some databases and storage mechanisms allow for encryption at rest.</span></span> <span data-ttu-id="24bd7-156">미사용 데이터 암호화:</span><span class="sxs-lookup"><span data-stu-id="24bd7-156">Encryption at rest:</span></span>

* <span data-ttu-id="24bd7-157">저장 된 데이터를 자동으로 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="24bd7-157">Encrypts stored data automatically.</span></span>
* <span data-ttu-id="24bd7-158">구성, 프로그래밍, 또는 데이터에 액세스 하는 소프트웨어에 대 한 다른 작업 없이 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="24bd7-158">Encrypts without configuration, programming, or other work for the software that accesses the data.</span></span>
* <span data-ttu-id="24bd7-159">쉽고 안전한 옵션이입니다.</span><span class="sxs-lookup"><span data-stu-id="24bd7-159">Is the easiest and safest option.</span></span>
* <span data-ttu-id="24bd7-160">데이터베이스를 키와 암호화를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24bd7-160">Lets the database manage keys and encryption.</span></span>

<span data-ttu-id="24bd7-161">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="24bd7-161">For example:</span></span>

* <span data-ttu-id="24bd7-162">Microsoft SQL 및 Azure SQL 제공 [투명 한 데이터 암호화](/sql/relational-databases/security/encryption/transparent-data-encryption) (TDE).</span><span class="sxs-lookup"><span data-stu-id="24bd7-162">Microsoft SQL and Azure SQL provide [Transparent Data Encryption](/sql/relational-databases/security/encryption/transparent-data-encryption) (TDE).</span></span>
* [<span data-ttu-id="24bd7-163">기본적으로 데이터베이스를 암호화 하는 SQL Azure</span><span class="sxs-lookup"><span data-stu-id="24bd7-163">SQL Azure encrypts the database by default</span></span>](https://azure.microsoft.com/updates/newly-created-azure-sql-databases-encrypted-by-default/)
* <span data-ttu-id="24bd7-164">[기본적으로 암호화 되어 azure Blob, 파일, 테이블 및 큐 저장소](https://azure.microsoft.com/blog/announcing-default-encryption-for-azure-blobs-files-table-and-queue-storage/)합니다.</span><span class="sxs-lookup"><span data-stu-id="24bd7-164">[Azure Blobs, Files, Table, and Queue Storage are encrypted by default](https://azure.microsoft.com/blog/announcing-default-encryption-for-azure-blobs-files-table-and-queue-storage/).</span></span>

<span data-ttu-id="24bd7-165">기본 제공 암호화를 제공 하지 않는 데이터베이스에 대 한 동일한 보호를 제공 하 디스크 암호화를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24bd7-165">For databases that don't provide built-in encryption at rest you may be able to use disk encryption to provide the same protection.</span></span> <span data-ttu-id="24bd7-166">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="24bd7-166">For example:</span></span>

* [<span data-ttu-id="24bd7-167">Windows Server에 대 한 BitLocker</span><span class="sxs-lookup"><span data-stu-id="24bd7-167">BitLocker for Windows Server</span></span>](/windows/security/information-protection/bitlocker/bitlocker-how-to-deploy-on-windows-server)
* <span data-ttu-id="24bd7-168">Linux:</span><span class="sxs-lookup"><span data-stu-id="24bd7-168">Linux:</span></span>
  * [<span data-ttu-id="24bd7-169">eCryptfs</span><span class="sxs-lookup"><span data-stu-id="24bd7-169">eCryptfs</span></span>](https://launchpad.net/ecryptfs)
  * <span data-ttu-id="24bd7-170">[EncFS](https://github.com/vgough/encfs)합니다.</span><span class="sxs-lookup"><span data-stu-id="24bd7-170">[EncFS](https://github.com/vgough/encfs).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="24bd7-171">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="24bd7-171">Additional Resources</span></span>

* [<span data-ttu-id="24bd7-172">Microsoft.com/GDPR</span><span class="sxs-lookup"><span data-stu-id="24bd7-172">Microsoft.com/GDPR</span></span>](https://www.microsoft.com/trustcenter/Privacy/GDPR)
