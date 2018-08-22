---
title: 인증 ASP.NET 멤버 자격에서에서 ASP.NET Core 2.0 Id로 마이그레이션
author: isaac2004
description: ASP.NET Core 2.0 Id 멤버 자격 인증을 사용 하 여 기존 ASP.NET 앱을 마이그레이션하는 방법에 알아봅니다.
ms.author: scaddie
ms.custom: mvc
ms.date: 04/24/2018
uid: migration/proper-to-2x/membership-to-core-identity
ms.openlocfilehash: 82158ec500151a0bb61fb1da55a53684367d9a4e
ms.sourcegitcommit: 2e054638b69f2b14f6d67d9fa3664999172ee1b2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2018
ms.locfileid: "41827722"
---
# <a name="migrate-from-aspnet-membership-authentication-to-aspnet-core-20-identity"></a><span data-ttu-id="59b9d-103">인증 ASP.NET 멤버 자격에서에서 ASP.NET Core 2.0 Id로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="59b9d-103">Migrate from ASP.NET Membership authentication to ASP.NET Core 2.0 Identity</span></span>

<span data-ttu-id="59b9d-104">작성자: [Isaac Levin](https://isaaclevin.com)</span><span class="sxs-lookup"><span data-stu-id="59b9d-104">By [Isaac Levin](https://isaaclevin.com)</span></span>

<span data-ttu-id="59b9d-105">이 문서에서는 ASP.NET Core 2.0 Id 멤버 자격 인증을 사용 하 여 ASP.NET 앱에 대 한 데이터베이스 스키마를 마이그레이션하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-105">This article demonstrates migrating the database schema for ASP.NET apps using Membership authentication to ASP.NET Core 2.0 Identity.</span></span>

> [!NOTE]
> <span data-ttu-id="59b9d-106">이 문서에서는 ASP.NET Core Id에 사용 되는 데이터베이스 스키마를 ASP.NET 멤버 자격 기반 앱에 대 한 데이터베이스 스키마를 마이그레이션하는 데 필요한 단계를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-106">This document provides the steps needed to migrate the database schema for ASP.NET Membership-based apps to the database schema used for ASP.NET Core Identity.</span></span> <span data-ttu-id="59b9d-107">ASP.NET 멤버 자격 기반 인증에서 ASP.NET Id로 마이그레이션에 대 한 자세한 내용은 참조 하세요. [SQL 멤버 자격에서 ASP.NET Id로 기존 앱을 마이그레이션](/aspnet/identity/overview/migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity)합니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-107">For more information about migrating from ASP.NET Membership-based authentication to ASP.NET Identity, see [Migrate an existing app from SQL Membership to ASP.NET Identity](/aspnet/identity/overview/migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity).</span></span> <span data-ttu-id="59b9d-108">ASP.NET Core Id에 대 한 자세한 내용은 참조 하세요. [ASP.NET core Id 소개](xref:security/authentication/identity)합니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-108">For more information about ASP.NET Core Identity, see [Introduction to Identity on ASP.NET Core](xref:security/authentication/identity).</span></span>

## <a name="review-of-membership-schema"></a><span data-ttu-id="59b9d-109">멤버 자격 스키마 검토</span><span class="sxs-lookup"><span data-stu-id="59b9d-109">Review of Membership schema</span></span>

<span data-ttu-id="59b9d-110">ASP.NET 2.0 이전 개발자를 해당 앱에 대 한 전체 인증 및 권한 부여 프로세스를 작성 해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-110">Prior to ASP.NET 2.0, developers were tasked with creating the entire authentication and authorization process for their apps.</span></span> <span data-ttu-id="59b9d-111">ASP.NET 2.0을 사용 하 여 ASP.NET 앱 내에서 보안을 처리 하는 상용구 솔루션 제공 멤버 자격 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-111">With ASP.NET 2.0, Membership was introduced, providing a boilerplate solution to handling security within ASP.NET apps.</span></span> <span data-ttu-id="59b9d-112">개발자가 사용 하 여 SQL Server 데이터베이스에 스키마를 부트스트랩 하 이제 있었습니다 합니다 [aspnet_regsql.exe](https://msdn.microsoft.com/library/ms229862.aspx) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-112">Developers were now able to bootstrap a schema into a SQL Server database with the [aspnet_regsql.exe](https://msdn.microsoft.com/library/ms229862.aspx) command.</span></span> <span data-ttu-id="59b9d-113">이 명령은 실행 한 후 다음 표에 데이터베이스에서 생성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-113">After running this command, the following tables were created in the database.</span></span>

  ![멤버 자격 테이블](identity/_static/membership-tables.png)

<span data-ttu-id="59b9d-115">기존 앱을 ASP.NET Core 2.0 Id로 마이그레이션하기 위해 이러한 테이블의 데이터를 새 Id 스키마에서 사용 하는 테이블을 마이그레이션할 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-115">To migrate existing apps to ASP.NET Core 2.0 Identity, the data in these tables needs to be migrated to the tables used by the new Identity schema.</span></span>

## <a name="aspnet-core-identity-20-schema"></a><span data-ttu-id="59b9d-116">ASP.NET Core Identity 2.0 스키마</span><span class="sxs-lookup"><span data-stu-id="59b9d-116">ASP.NET Core Identity 2.0 schema</span></span>

<span data-ttu-id="59b9d-117">ASP.NET Core 2.0을 따릅니다 합니다 [Identity](/aspnet/identity/index) 원칙 ASP.NET 4.5에서 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-117">ASP.NET Core 2.0 follows the [Identity](/aspnet/identity/index) principle introduced in ASP.NET 4.5.</span></span> <span data-ttu-id="59b9d-118">프레임 워크 간에 구현은 ASP.NET Core의 버전 간에 다양 한 원칙을 공유 하지만 (참조 [ASP.NET Core 2.0으로 인증 및 Id 마이그레이션](xref:migration/1x-to-2x/index)).</span><span class="sxs-lookup"><span data-stu-id="59b9d-118">Though the principle is shared, the implementation between the frameworks is different, even between versions of ASP.NET Core (see [Migrate authentication and Identity to ASP.NET Core 2.0](xref:migration/1x-to-2x/index)).</span></span>

<span data-ttu-id="59b9d-119">ASP.NET Core 2.0 Id에 대 한 스키마를 볼 수 있는 가장 빠른 방법은 새 ASP.NET Core 2.0 앱을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-119">The fastest way to view the schema for ASP.NET Core 2.0 Identity is to create a new ASP.NET Core 2.0 app.</span></span> <span data-ttu-id="59b9d-120">Visual Studio 2017에서 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-120">Follow these steps in Visual Studio 2017:</span></span>

* <span data-ttu-id="59b9d-121">**파일** > **새로 만들기** > **프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-121">Select **File** > **New** > **Project**.</span></span>
* <span data-ttu-id="59b9d-122">새 **ASP.NET Core 웹 응용 프로그램** 하 고 프로젝트 이름을 *CoreIdentitySample*합니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-122">Create a new **ASP.NET Core Web Application** and name the project *CoreIdentitySample*.</span></span>
* <span data-ttu-id="59b9d-123">선택 **ASP.NET Core 2.0** 한 다음 선택한 드롭다운 **웹 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-123">Select **ASP.NET Core 2.0** in the dropdown and then select **Web Application**.</span></span> <span data-ttu-id="59b9d-124">이 템플릿에서 생성 된 [Razor 페이지](xref:razor-pages/index) 앱.</span><span class="sxs-lookup"><span data-stu-id="59b9d-124">This template produces a [Razor Pages](xref:razor-pages/index) app.</span></span> <span data-ttu-id="59b9d-125">클릭 하기 전에 **확인**, 클릭 **인증 변경**합니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-125">Before clicking **OK**, click **Change Authentication**.</span></span>
* <span data-ttu-id="59b9d-126">선택할 **개별 사용자 계정** Identity 템플릿에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-126">Choose **Individual User Accounts** for the Identity templates.</span></span> <span data-ttu-id="59b9d-127">마지막으로, 클릭 **확인**, 한 다음 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-127">Finally, click **OK**, then **OK**.</span></span> <span data-ttu-id="59b9d-128">Visual Studio ASP.NET Core Id 템플릿을 사용 하 여 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-128">Visual Studio creates a project using the ASP.NET Core Identity template.</span></span>

<span data-ttu-id="59b9d-129">사용 하 여 ASP.NET Core 2.0 Identity [Entity Framework Core](/ef/core) 인증 데이터를 저장 하는 데이터베이스를 사용 하 여 상호 작용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-129">ASP.NET Core 2.0 Identity uses [Entity Framework Core](/ef/core) to interact with the database storing the authentication data.</span></span> <span data-ttu-id="59b9d-130">새로 만든 앱이 작동 하려면 순서로 필요이 데이터를 저장할 데이터베이스 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-130">In order for the newly created app to work, there needs to be a database to store this data.</span></span> <span data-ttu-id="59b9d-131">새 앱을 만든 후 데이터베이스 환경에서 스키마를 검사 하는 가장 빠른 방법은 Entity Framework 마이그레이션을 사용 하 여 데이터베이스를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-131">After creating a new app, the fastest way to inspect the schema in a database environment is to create the database using Entity Framework migrations.</span></span> <span data-ttu-id="59b9d-132">이 프로세스에서는 데이터베이스, 로컬로 또는 다른 곳에서 해당 스키마를 모방 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-132">This process creates a database, either locally or elsewhere, which mimics that schema.</span></span> <span data-ttu-id="59b9d-133">자세한 내용은 이전 설명서를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-133">Review the preceding documentation for more information.</span></span>

<span data-ttu-id="59b9d-134">ASP.NET Core Id 스키마를 사용 하 여 데이터베이스를 만들려면 다음을 실행 합니다 `Update-Database` Visual studio의 명령을 **패키지 관리자 콘솔** (PMC) 창&mdash;에 있는 **도구**  >  **NuGet 패키지 관리자** > **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-134">To create a database with the ASP.NET Core Identity schema, run the `Update-Database` command in Visual Studio's **Package Manager Console** (PMC) window&mdash;it's located at **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="59b9d-135">PMC는 Entity Framework 명령 실행을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-135">PMC supports running Entity Framework commands.</span></span>

<span data-ttu-id="59b9d-136">지정 된 데이터베이스에 대 한 연결 문자열을 사용 하는 엔터티 프레임 워크 명령 *appsettings.json*합니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-136">Entity Framework commands use the connection string for the database specified in *appsettings.json*.</span></span> <span data-ttu-id="59b9d-137">다음 연결 문자열에 데이터베이스를 대상 *localhost* 라는 *asp net-core id*합니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-137">The following connection string targets a database on *localhost* named *asp-net-core-identity*.</span></span> <span data-ttu-id="59b9d-138">이 설정을 사용 하면 Entity Framework 사용 하도록 구성 되는 `DefaultConnection` 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-138">In this setting, Entity Framework is configured to use the `DefaultConnection` connection string.</span></span>

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=localhost;Database=aspnet-core-identity;Trusted_Connection=True;MultipleActiveResultSets=true"
  }
}
```

<span data-ttu-id="59b9d-139">이 명령은 앱 초기화에 필요한 모든 데이터 및 스키마를 사용 하 여 지정 된 데이터베이스를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-139">This command builds the database specified with the schema and any data needed for app initialization.</span></span> <span data-ttu-id="59b9d-140">다음 이미지에서는 이전 단계를 사용 하 여 만든 테이블 구조를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-140">The following image depicts the table structure that's created with the preceding steps.</span></span>

   ![Identity 테이블](identity/_static/identity-tables.png)

## <a name="migrate-the-schema"></a><span data-ttu-id="59b9d-142">스키마 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="59b9d-142">Migrate the schema</span></span>

<span data-ttu-id="59b9d-143">테이블 구조와 멤버 및 ASP.NET Core Id에 대 한 필드에 미묘한 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-143">There are subtle differences in the table structures and fields for both Membership and ASP.NET Core Identity.</span></span> <span data-ttu-id="59b9d-144">ASP.NET 및 ASP.NET Core 앱을 사용 하 여 인증/권한 부여에 대 한 패턴은 크게 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-144">The pattern has changed substantially for authentication/authorization with ASP.NET and ASP.NET Core apps.</span></span> <span data-ttu-id="59b9d-145">Id로도 사용 되는 키 개체는 *사용자가* 하 고 *역할*입니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-145">The key objects that are still used with Identity are *Users* and *Roles*.</span></span> <span data-ttu-id="59b9d-146">매핑 테이블에는 다음과 같습니다 *사용자*하십시오 *역할*, 및 *UserRoles*합니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-146">Here are mapping tables for *Users*, *Roles*, and *UserRoles*.</span></span>

### <a name="users"></a><span data-ttu-id="59b9d-147">사용자</span><span class="sxs-lookup"><span data-stu-id="59b9d-147">Users</span></span>

| <span data-ttu-id="59b9d-148">*Identity(AspNetUsers)*</span><span class="sxs-lookup"><span data-stu-id="59b9d-148">*Identity(AspNetUsers)*</span></span> |   | <span data-ttu-id="59b9d-149">*Membership(aspnet_Users/aspnet_Membership)*</span><span class="sxs-lookup"><span data-stu-id="59b9d-149">*Membership(aspnet_Users/aspnet_Membership)*</span></span> ||
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="59b9d-150">**필드 이름**</span><span class="sxs-lookup"><span data-stu-id="59b9d-150">**Field Name**</span></span> | <span data-ttu-id="59b9d-151">**Type**</span><span class="sxs-lookup"><span data-stu-id="59b9d-151">**Type**</span></span>  |   <span data-ttu-id="59b9d-152">**필드 이름**</span><span class="sxs-lookup"><span data-stu-id="59b9d-152">**Field Name**</span></span> | <span data-ttu-id="59b9d-153">**Type**</span><span class="sxs-lookup"><span data-stu-id="59b9d-153">**Type**</span></span>  |
|`Id` | <span data-ttu-id="59b9d-154">string</span><span class="sxs-lookup"><span data-stu-id="59b9d-154">string</span></span> | `aspnet_Users.UserId` | <span data-ttu-id="59b9d-155">string</span><span class="sxs-lookup"><span data-stu-id="59b9d-155">string</span></span>
|`UserName` | <span data-ttu-id="59b9d-156">string</span><span class="sxs-lookup"><span data-stu-id="59b9d-156">string</span></span> | `aspnet_Users.UserName` | <span data-ttu-id="59b9d-157">string</span><span class="sxs-lookup"><span data-stu-id="59b9d-157">string</span></span>
|`Email` | <span data-ttu-id="59b9d-158">string</span><span class="sxs-lookup"><span data-stu-id="59b9d-158">string</span></span> | `aspnet_Membership.Email` | <span data-ttu-id="59b9d-159">string</span><span class="sxs-lookup"><span data-stu-id="59b9d-159">string</span></span>
|`NormalizedUserName` | <span data-ttu-id="59b9d-160">string</span><span class="sxs-lookup"><span data-stu-id="59b9d-160">string</span></span> | `aspnet_Users.LoweredUserName` | <span data-ttu-id="59b9d-161">string</span><span class="sxs-lookup"><span data-stu-id="59b9d-161">string</span></span>
|`NormalizedEmail` | <span data-ttu-id="59b9d-162">string</span><span class="sxs-lookup"><span data-stu-id="59b9d-162">string</span></span> | `aspnet_Membership.LoweredEmail` | <span data-ttu-id="59b9d-163">string</span><span class="sxs-lookup"><span data-stu-id="59b9d-163">string</span></span>
|`PhoneNumber` | <span data-ttu-id="59b9d-164">string</span><span class="sxs-lookup"><span data-stu-id="59b9d-164">string</span></span> | `aspnet_Users.MobileAlias` | <span data-ttu-id="59b9d-165">string</span><span class="sxs-lookup"><span data-stu-id="59b9d-165">string</span></span>
|`LockoutEnabled` | <span data-ttu-id="59b9d-166">비트</span><span class="sxs-lookup"><span data-stu-id="59b9d-166">bit</span></span> | `aspnet_Membership.IsLockedOut` | <span data-ttu-id="59b9d-167">비트</span><span class="sxs-lookup"><span data-stu-id="59b9d-167">bit</span></span>

> [!NOTE]
> <span data-ttu-id="59b9d-168">일부 필드 매핑이 ASP.NET Core Id 멤버 자격에서 한 일 관계와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-168">Not all the field mappings resemble one-to-one relationships from Membership to ASP.NET Core Identity.</span></span> <span data-ttu-id="59b9d-169">앞의 표에 기본 멤버 자격 사용자 스키마 및 ASP.NET Core Id 스키마에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-169">The preceding table takes the default Membership User schema and maps it to the ASP.NET Core Identity schema.</span></span> <span data-ttu-id="59b9d-170">멤버 자격에 사용 된 다른 사용자 지정 필드를 수동으로 매핑할 수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-170">Any other custom fields that were used for Membership need to be mapped manually.</span></span> <span data-ttu-id="59b9d-171">이 매핑에 암호에 대 한 맵이 없습니다 암호 조건 및 암호 솔트 둘 사이 마이그레이션되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-171">In this mapping, there's no map for passwords, as both password criteria and password salts don't migrate between the two.</span></span> <span data-ttu-id="59b9d-172">**null로 암호를 그대로 두고 자신의 암호를 재설정 하도록 요청 하려면 해당 하는 것이 좋습니다.**</span><span class="sxs-lookup"><span data-stu-id="59b9d-172">**It's recommended to leave the password as null and to ask users to reset their passwords.**</span></span> <span data-ttu-id="59b9d-173">ASP.NET Core Id에 `LockoutEnd` 사용자 잠겨 있으면 일부 미래 날짜를 설정 해야 합니다. 이 작업은 마이그레이션 스크립트에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-173">In ASP.NET Core Identity, `LockoutEnd` should be set to some date in the future if the user is locked out. This is shown in the migration script.</span></span>

### <a name="roles"></a><span data-ttu-id="59b9d-174">역할</span><span class="sxs-lookup"><span data-stu-id="59b9d-174">Roles</span></span>

| <span data-ttu-id="59b9d-175">*Identity(AspNetRoles)*</span><span class="sxs-lookup"><span data-stu-id="59b9d-175">*Identity(AspNetRoles)*</span></span> |   | <span data-ttu-id="59b9d-176">*Membership(aspnet_Roles)*</span><span class="sxs-lookup"><span data-stu-id="59b9d-176">*Membership(aspnet_Roles)*</span></span> ||
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="59b9d-177">**필드 이름**</span><span class="sxs-lookup"><span data-stu-id="59b9d-177">**Field Name**</span></span> | <span data-ttu-id="59b9d-178">**Type**</span><span class="sxs-lookup"><span data-stu-id="59b9d-178">**Type**</span></span>  |   <span data-ttu-id="59b9d-179">**필드 이름**</span><span class="sxs-lookup"><span data-stu-id="59b9d-179">**Field Name**</span></span> | <span data-ttu-id="59b9d-180">**Type**</span><span class="sxs-lookup"><span data-stu-id="59b9d-180">**Type**</span></span>  |
|`Id` | <span data-ttu-id="59b9d-181">string</span><span class="sxs-lookup"><span data-stu-id="59b9d-181">string</span></span> | `RoleId` | <span data-ttu-id="59b9d-182">string</span><span class="sxs-lookup"><span data-stu-id="59b9d-182">string</span></span>
|`Name` | <span data-ttu-id="59b9d-183">string</span><span class="sxs-lookup"><span data-stu-id="59b9d-183">string</span></span> | `RoleName` | <span data-ttu-id="59b9d-184">string</span><span class="sxs-lookup"><span data-stu-id="59b9d-184">string</span></span>
|`NormalizedName` | <span data-ttu-id="59b9d-185">string</span><span class="sxs-lookup"><span data-stu-id="59b9d-185">string</span></span> | `LoweredRoleName` | <span data-ttu-id="59b9d-186">string</span><span class="sxs-lookup"><span data-stu-id="59b9d-186">string</span></span>

### <a name="user-roles"></a><span data-ttu-id="59b9d-187">사용자 역할</span><span class="sxs-lookup"><span data-stu-id="59b9d-187">User Roles</span></span>

| <span data-ttu-id="59b9d-188">*Identity(AspNetUserRoles)*</span><span class="sxs-lookup"><span data-stu-id="59b9d-188">*Identity(AspNetUserRoles)*</span></span> |   | <span data-ttu-id="59b9d-189">*Membership(aspnet_UsersInRoles)*</span><span class="sxs-lookup"><span data-stu-id="59b9d-189">*Membership(aspnet_UsersInRoles)*</span></span> ||
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="59b9d-190">**필드 이름**</span><span class="sxs-lookup"><span data-stu-id="59b9d-190">**Field Name**</span></span> | <span data-ttu-id="59b9d-191">**Type**</span><span class="sxs-lookup"><span data-stu-id="59b9d-191">**Type**</span></span>  |   <span data-ttu-id="59b9d-192">**필드 이름**</span><span class="sxs-lookup"><span data-stu-id="59b9d-192">**Field Name**</span></span> | <span data-ttu-id="59b9d-193">**Type**</span><span class="sxs-lookup"><span data-stu-id="59b9d-193">**Type**</span></span>  |
|`RoleId` | <span data-ttu-id="59b9d-194">string</span><span class="sxs-lookup"><span data-stu-id="59b9d-194">string</span></span> | `RoleId` | <span data-ttu-id="59b9d-195">string</span><span class="sxs-lookup"><span data-stu-id="59b9d-195">string</span></span>
|`UserId` | <span data-ttu-id="59b9d-196">string</span><span class="sxs-lookup"><span data-stu-id="59b9d-196">string</span></span> | `UserId` | <span data-ttu-id="59b9d-197">string</span><span class="sxs-lookup"><span data-stu-id="59b9d-197">string</span></span>

<span data-ttu-id="59b9d-198">에 대 한 마이그레이션 스크립트를 만들 때 이전 매핑 테이블을 참조할 *사용자가* 하 고 *역할*입니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-198">Reference the preceding mapping tables when creating a migration script for *Users* and *Roles*.</span></span> <span data-ttu-id="59b9d-199">다음 예제에서는 두 개의 데이터베이스가 데이터베이스 서버에 있는 것을 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-199">The following example assumes you have two databases on a database server.</span></span> <span data-ttu-id="59b9d-200">하나의 데이터베이스에는 기존 ASP.NET 멤버 자격 스키마와 데이터를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-200">One database contains the existing ASP.NET Membership schema and data.</span></span> <span data-ttu-id="59b9d-201">다른 데이터베이스 앞에서 설명한 단계를 사용 하 여 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-201">The other database was created using steps described earlier.</span></span> <span data-ttu-id="59b9d-202">주석은 대 한 자세한 내용은 인라인으로 포함된 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-202">Comments are included inline for more details.</span></span>

```sql
-- THIS SCRIPT NEEDS TO RUN FROM THE CONTEXT OF THE MEMBERSHIP DB
BEGIN TRANSACTION MigrateUsersAndRoles
use aspnetdb

-- INSERT USERS
INSERT INTO coreidentity.dbo.aspnetusers
            (id,
             username,
             normalizedusername,
             passwordhash,
             securitystamp,
             emailconfirmed,
             phonenumber,
             phonenumberconfirmed,
             twofactorenabled,
             lockoutend,
             lockoutenabled,
             accessfailedcount,
             email,
             normalizedemail)
SELECT aspnet_users.userid,
       aspnet_users.username,
       aspnet_users.loweredusername,
       --Creates an empty password since passwords don't map between the two schemas
       '',
       --Security Stamp is a token used to verify the state of an account and is subject to change at any time. It should be initialized as a new ID.
       NewID(),
       --EmailConfirmed is set when a new user is created and confirmed via email. Users must have this set during migration to ensure they're able to reset passwords.
       1,
       aspnet_users.mobilealias,
       CASE
         WHEN aspnet_Users.MobileAlias is null THEN 0
         ELSE 1
       END,
       --2-factor Auth likely wasn't setup in Membership for users, so setting as false.
       0,
       CASE
         --Setting lockout date to time in the future (1000 years)
         WHEN aspnet_membership.islockedout = 1 THEN Dateadd(year, 1000,
                                                     Sysutcdatetime())
         ELSE NULL
       END,
       aspnet_membership.islockedout,
       --AccessFailedAccount is used to track failed logins. This is stored in membership in multiple columns. Setting to 0 arbitrarily.
       0,
       aspnet_membership.email,
       aspnet_membership.loweredemail
FROM   aspnet_users
       LEFT OUTER JOIN aspnet_membership
                    ON aspnet_membership.applicationid =
                       aspnet_users.applicationid
                       AND aspnet_users.userid = aspnet_membership.userid
       LEFT OUTER JOIN coreidentity.dbo.aspnetusers
                    ON aspnet_membership.userid = aspnetusers.id
WHERE  aspnetusers.id IS NULL

-- INSERT ROLES
INSERT INTO coreIdentity.dbo.aspnetroles(id,name)
SELECT roleId,rolename
FROM aspnet_roles;

-- INSERT USER ROLES
INSERT INTO coreidentity.dbo.aspnetuserroles(userid,roleid)
SELECT userid,roleid
FROM aspnet_usersinroles;

IF @@ERROR <> 0
  BEGIN
    ROLLBACK TRANSACTION MigrateUsersAndRoles
    RETURN
  END

COMMIT TRANSACTION MigrateUsersAndRoles
```

<span data-ttu-id="59b9d-203">이 스크립트를 완료 하면 앞에서 만든 ASP.NET Core Id 앱은 멤버 자격 사용자를 사용 하 여 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-203">After completion of this script, the ASP.NET Core Identity app created earlier is populated with Membership users.</span></span> <span data-ttu-id="59b9d-204">사용자 로그인 시 자신의 암호를 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-204">Users need to change their passwords before logging in.</span></span>

> [!NOTE]
> <span data-ttu-id="59b9d-205">멤버 자격 시스템에는 사용자가 자신의 전자 메일 주소를 일치 하지 않는 사용자 이름으로,이 수용 하기 위해 앞에서 만든 앱에 필요한 변경 내용이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-205">If the Membership system had users with user names that didn't match their email address, changes are required to the app created earlier to accommodate this.</span></span> <span data-ttu-id="59b9d-206">기본 템플릿을 예상 `UserName` 및 `Email` 동일 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-206">The default template expects `UserName` and `Email` to be the same.</span></span> <span data-ttu-id="59b9d-207">경우에는 다른 지 알아두면에 대 한 로그인 프로세스를 사용 하 여 수정 해야 `UserName` 대신 `Email`합니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-207">For situations in which they're different, the login process needs to be modified to use `UserName` instead of `Email`.</span></span>

<span data-ttu-id="59b9d-208">에 `PageModel` 위치한 로그인 페이지의 *Pages\Account\Login.cshtml.cs*, 제거를 `[EmailAddress]` 에서 특성을 *전자 메일* 속성.</span><span class="sxs-lookup"><span data-stu-id="59b9d-208">In the `PageModel` of the Login Page, located at *Pages\Account\Login.cshtml.cs*, remove the `[EmailAddress]` attribute from the *Email* property.</span></span> <span data-ttu-id="59b9d-209">이 파일 이름을 *UserName*합니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-209">Rename it to *UserName*.</span></span> <span data-ttu-id="59b9d-210">이 변경 해야 때마다 `EmailAddress` 에서 언급 되는 *보기* 및 *PageModel*.</span><span class="sxs-lookup"><span data-stu-id="59b9d-210">This requires a change wherever `EmailAddress` is mentioned, in the *View* and *PageModel*.</span></span> <span data-ttu-id="59b9d-211">결과 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-211">The result looks like the following:</span></span>

 ![고정된 로그인](identity/_static/fixed-login.png)

## <a name="next-steps"></a><span data-ttu-id="59b9d-213">다음 단계</span><span class="sxs-lookup"><span data-stu-id="59b9d-213">Next steps</span></span>

<span data-ttu-id="59b9d-214">이 자습서에서는 ASP.NET Core 2.0 Id를 SQL 멤버 자격에서 사용자를 이식 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-214">In this tutorial, you learned how to port users from SQL membership to ASP.NET Core 2.0 Identity.</span></span> <span data-ttu-id="59b9d-215">ASP.NET Core Id에 대 한 자세한 내용은 [Id 소개](xref:security/authentication/identity)합니다.</span><span class="sxs-lookup"><span data-stu-id="59b9d-215">For more information regarding ASP.NET Core Identity, see [Introduction to Identity](xref:security/authentication/identity).</span></span>
