---
title: Identity 모델 사용자 지정
author: ajcvickers
description: 이 문서에는 ASP.NET Core Id에 대 한 기본 Framework Core 엔터티 데이터 모델을 사용자 지정 하는 방법을 설명 합니다.
ms.author: avickers
ms.date: 04/12/2018
ms.prod: asp.net-core
uid: security/authentication/customize_identity_model
ms.openlocfilehash: b44b4fd0f24d245b969588a7226ea6aacbe2a722
ms.sourcegitcommit: 7003d27b607e529642ded0400aa48ae692a0e666
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2018
ms.locfileid: "37036900"
---
# <a name="identity-model-customization"></a><span data-ttu-id="809b7-103">Identity 모델 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="809b7-103">Identity model customization</span></span>

<span data-ttu-id="809b7-104">으로 [Arthur Vickers](https://github.com/ajcvickers)</span><span class="sxs-lookup"><span data-stu-id="809b7-104">By [Arthur Vickers](https://github.com/ajcvickers)</span></span>

<span data-ttu-id="809b7-105">ASP.NET Core Identity ASP.NET Core 응용 프로그램에서 사용자 계정을 저장 및 관리 하기 위한 프레임 워크를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-105">ASP.NET Core Identity provides a framework for managing and storing user accounts in ASP.NET Core applications.</span></span> <span data-ttu-id="809b7-106">Identity "개별 사용자 계정" 인증 메커니즘으로 선택 된 경우 프로젝트에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-106">Identity is added to your project when "Individual User Accounts" is selected as the authentication mechanism.</span></span> <span data-ttu-id="809b7-107">에서는 기본적으로 Identity는 Entity Framework (EF)를 사용 하 여 핵심 데이터 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-107">By default, Identity makes use of an Entity Framework (EF) Core data model.</span></span> <span data-ttu-id="809b7-108">이 문서에서는 Id 모델을 사용자 지정 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-108">This article describes how to customize the Identity model.</span></span>

<a name="identity-migrations"></a>

## <a name="identity-and-ef-core-migrations"></a><span data-ttu-id="809b7-109">Id 및 EF 코어 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="809b7-109">Identity and EF Core Migrations</span></span>

<span data-ttu-id="809b7-110">모델을 검사 하기 전에 Identity와 작동 하는 방법을 이해 하는 데 유용이 [EF 코어 마이그레이션](/ef/core/managing-schemas/migrations/) 를 만들고 데이터베이스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-110">Before examining the model, it's useful to understand how Identity works with [EF Core Migrations](/ef/core/managing-schemas/migrations/) to create and update a database.</span></span> <span data-ttu-id="809b7-111">최상위 수준에 프로세스는.</span><span class="sxs-lookup"><span data-stu-id="809b7-111">At the top level, the process is:</span></span>

1. <span data-ttu-id="809b7-112">정의 또는 업데이트 한 [코드에서 데이터 모델](/ef/core/modeling/)합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-112">Define or update a [data model in code](/ef/core/modeling/).</span></span>
1. <span data-ttu-id="809b7-113">이 모델 데이터베이스에 적용할 수 있는 변경 내용으로 변환할 마이그레이션을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-113">Add a migration to translate this model into changes that can be applied to the database.</span></span>
1. <span data-ttu-id="809b7-114">마이그레이션을 제대로 사용자의 의도 반영을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-114">Check that the migration correctly represents your intentions.</span></span>
1. <span data-ttu-id="809b7-115">마이그레이션 모델 동기화 되도록 데이터베이스를 업데이트를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-115">Apply the migration to update the database to be in sync with the model.</span></span>
1. <span data-ttu-id="809b7-116">추가로 모델 구체화 하 고 데이터베이스 동기화 상태를 유지 하기 위해 1-4 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-116">Repeat steps 1-4 to further refine the model and keep the database in sync.</span></span>

<span data-ttu-id="809b7-117">마이그레이션 추가 되 고 사용 하 여 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-117">Migrations are added and applied using:</span></span>

* <span data-ttu-id="809b7-118">[패키지 관리자 콘솔](/ef/core/miscellaneous/cli/powershell) Visual Studio를 사용 하는 경우 (PMC).</span><span class="sxs-lookup"><span data-stu-id="809b7-118">The [Package Manager Console](/ef/core/miscellaneous/cli/powershell) (PMC) if you are using Visual Studio.</span></span>
* <span data-ttu-id="809b7-119">[dotnet 명령을](/ef/core/miscellaneous/cli/dotnet) 명령줄에서.</span><span class="sxs-lookup"><span data-stu-id="809b7-119">The [dotnet commands](/ef/core/miscellaneous/cli/dotnet) on the command line.</span></span>
* <span data-ttu-id="809b7-120">응용 프로그램이 실행 될 때 오류 페이지에서 마이그레이션 링크를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-120">Selecting the migrations link on the error page when the application is run.</span></span>

<span data-ttu-id="809b7-121">ASP.NET Core 응용 프로그램이 실행 될 때 마이그레이션을 적용을 사용할 수 있는 개발 시 오류 페이지 처리기를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-121">ASP.NET Core has a development-time error page handler that can be used to apply migrations when the application is run.</span></span> <span data-ttu-id="809b7-122">프로덕션 응용 프로그램의 경우이 마이그레이션의 SQL 스크립트를 생성 하 고 제어 된 응용 프로그램 및 데이터베이스 배포의 일부로 데이터베이스에 배포 하기에 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-122">For production applications, it is often more appropriate to generate SQL scripts from the migrations and deploy these to the database as part of a controlled application and database deployment.</span></span>

<span data-ttu-id="809b7-123">Id를 사용 하는 새 응용 프로그램을 만든 경우 위 1과 2 단계가 이미 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-123">When a new application using Identity is created, steps 1 and 2 above have already been completed.</span></span> <span data-ttu-id="809b7-124">즉, 초기 데이터 모델이 이미 있으면 및 초기 마이그레이션 프로젝트에 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-124">That is, the initial data model already exists, and the initial migration has been added to the project.</span></span> <span data-ttu-id="809b7-125">초기 마이그레이션 데이터베이스에 적용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-125">The initial migration still needs to be applied to the database.</span></span> <span data-ttu-id="809b7-126">초기 마이그레이션은 데이터베이스 업데이트 (PMC), dotnet ef 데이터베이스 업데이트 (.NET Core CLI) 명령을 실행 하 여 또는 응용 프로그램이 실행 될 때 오류 페이지를 사용 하 여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-126">The initial migration can be done by running the Update-Database (PMC), the dotnet ef database update (.NET Core CLI) command, or by using the error page when the application is run.</span></span>

<span data-ttu-id="809b7-127">앞의 단계는 모델에 변경 내용이 반복 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-127">The preceding steps need to be repeated as changes are made to the model.</span></span>

<a name="identity-model"></a>

## <a name="the-identity-model"></a><span data-ttu-id="809b7-128">Id 모델</span><span class="sxs-lookup"><span data-stu-id="809b7-128">The Identity model</span></span>

### <a name="entity-types"></a><span data-ttu-id="809b7-129">엔터티 형식</span><span class="sxs-lookup"><span data-stu-id="809b7-129">Entity types</span></span>

<span data-ttu-id="809b7-130">Id 모델의 7 가지 엔터티 형식으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-130">The Identity model consists of seven entity types:</span></span>

* <span data-ttu-id="809b7-131">`User` -사용자를 나타냅니다</span><span class="sxs-lookup"><span data-stu-id="809b7-131">`User` - represents the user</span></span>
* <span data-ttu-id="809b7-132">`Role` -역할을 나타냅니다</span><span class="sxs-lookup"><span data-stu-id="809b7-132">`Role` - represents a role</span></span>
* <span data-ttu-id="809b7-133">`UserClaim` -사용자가 소유 하는 클레임을 나타냅니다</span><span class="sxs-lookup"><span data-stu-id="809b7-133">`UserClaim` - represents a claim that a user possess</span></span>
* <span data-ttu-id="809b7-134">`UserToken` -사용자에 대 한 인증 토큰을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-134">`UserToken` - represents an authentication token for a user</span></span>
* <span data-ttu-id="809b7-135">`UserLogin` -는 사용자를 로그인 연결</span><span class="sxs-lookup"><span data-stu-id="809b7-135">`UserLogin` - associates a user with a login</span></span>
* <span data-ttu-id="809b7-136">`RoleClaim` -역할 내의 모든 사용자에 게 부여 하는 클레임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-136">`RoleClaim` - represents a claim that is granted to all users within a role</span></span>
* <span data-ttu-id="809b7-137">`UserRole` -사용자 및 역할을 연결 하는 엔터티를 조인 합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-137">`UserRole` - join entity that associates users and roles</span></span>

### <a name="entity-type-relationships"></a><span data-ttu-id="809b7-138">엔터티 형식 관계</span><span class="sxs-lookup"><span data-stu-id="809b7-138">Entity type relationships</span></span>

<span data-ttu-id="809b7-139">이러한 엔터티 형식은 다음과 같은 방법으로 서로를 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-139">These entity types are related to each other in the following ways:</span></span>

* <span data-ttu-id="809b7-140">각 `User` 가질 수 있습니다 `UserClaims`</span><span class="sxs-lookup"><span data-stu-id="809b7-140">Each `User` can have many `UserClaims`</span></span>
* <span data-ttu-id="809b7-141">각 `User` 가질 수 있습니다 `UserLogins`</span><span class="sxs-lookup"><span data-stu-id="809b7-141">Each `User` can have many `UserLogins`</span></span>
* <span data-ttu-id="809b7-142">각 `User` 가질 수 있습니다 `UserTokens`</span><span class="sxs-lookup"><span data-stu-id="809b7-142">Each `User` can have many `UserTokens`</span></span>
* <span data-ttu-id="809b7-143">각 `Role` 관련 가질 수 있습니다 `RoleClaims`</span><span class="sxs-lookup"><span data-stu-id="809b7-143">Each `Role` can have many associated `RoleClaims`</span></span>
* <span data-ttu-id="809b7-144">각 `User` 수는 관련 된 많은 `Roles`, 및 각 `Role` 많은 사용자 들과 연관 될 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="809b7-144">Each `User` can have many associated `Roles`, and each `Role` can be associated with many Users</span></span>
  * <span data-ttu-id="809b7-145">이것이 데이터베이스에 조인 테이블을 필요로 하는 다 대 다 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-145">This is a many-to-many relationship, which requires a join table in the database.</span></span> <span data-ttu-id="809b7-146">조인 테이블으로 표시 됩니다는 `UserRole` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="809b7-146">The join table is represented by the `UserRole` entity.</span></span>

### <a name="default-model-configuration"></a><span data-ttu-id="809b7-147">기본 모델 구성</span><span class="sxs-lookup"><span data-stu-id="809b7-147">Default model configuration</span></span>

<span data-ttu-id="809b7-148">다양 한에서 상속 하는 "컨텍스트 클래스"를 정의 하는 identity [DbContext](/dotnet/api/microsoft.entityframeworkcore.dbcontext) 를 구성 하 여 모델을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-148">Identity defines a variety of "context classes" which inherit from [DbContext](/dotnet/api/microsoft.entityframeworkcore.dbcontext) to configure and use the model.</span></span> <span data-ttu-id="809b7-149">이 구성을 수행 해야를 사용 하는 [EF 핵심 코드 첫 번째 Fluent API](/ef/core/modeling/) 에 [OnModelCreating](/dotnet/api/microsoft.entityframeworkcore.dbcontext.onmodelcreating#Microsoft_EntityFrameworkCore_DbContext_OnModelCreating_Microsoft_EntityFrameworkCore_ModelBuilder_) 컨텍스트 클래스의 메서드.</span><span class="sxs-lookup"><span data-stu-id="809b7-149">This configuration is done using the [EF Core Code First Fluent API](/ef/core/modeling/) in the [OnModelCreating](/dotnet/api/microsoft.entityframeworkcore.dbcontext.onmodelcreating#Microsoft_EntityFrameworkCore_DbContext_OnModelCreating_Microsoft_EntityFrameworkCore_ModelBuilder_) method of the context class.</span></span> <span data-ttu-id="809b7-150">기본 구성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-150">The default configuration is:</span></span>

```CSharp
builder.Entity<TUser>(b =>
{
    // Primary key
    b.HasKey(u => u.Id);

    // Indexes for "normalized" username and email, to allow efficient lookups
    b.HasIndex(u => u.NormalizedUserName).HasName("UserNameIndex").IsUnique();
    b.HasIndex(u => u.NormalizedEmail).HasName("EmailIndex");

    // Maps to the AspNetUsers table
    b.ToTable("AspNetUsers");

    // A concurrency token for use with the optimistic concurrency checking
    b.Property(u => u.ConcurrencyStamp).IsConcurrencyToken();

    // Limit the size of columns to use efficient database types
    b.Property(u => u.UserName).HasMaxLength(256);
    b.Property(u => u.NormalizedUserName).HasMaxLength(256);
    b.Property(u => u.Email).HasMaxLength(256);
    b.Property(u => u.NormalizedEmail).HasMaxLength(256);

    // The relationships between User and other entity types
    // Note that these relationships are configured with no navigation properties

    // Each User can have many UserClaims
    b.HasMany<TUserClaim>().WithOne().HasForeignKey(uc => uc.UserId).IsRequired();

    // Each User can have many UserLogins
    b.HasMany<TUserLogin>().WithOne().HasForeignKey(ul => ul.UserId).IsRequired();

    // Each User can have many UserTokens
    b.HasMany<TUserToken>().WithOne().HasForeignKey(ut => ut.UserId).IsRequired();

    // Each User can have many entries in the UserRole join table
    b.HasMany<TUserRole>().WithOne().HasForeignKey(ur => ur.UserId).IsRequired();
});

builder.Entity<TUserClaim>(b =>
{
    // Primary key
    b.HasKey(uc => uc.Id);

    // Maps to the AspNetUserClaims table
    b.ToTable("AspNetUserClaims");
});

builder.Entity<TUserLogin>(b =>
{
    // Composite primary key consisting of the LoginProvider and the key to use
    // with that provider
    b.HasKey(l => new { l.LoginProvider, l.ProviderKey });

    // Limit the size of the composite key columns due to common database restrictions
    b.Property(l => l.LoginProvider).HasMaxLength(128);
    b.Property(l => l.ProviderKey).HasMaxLength(128);

    // Maps to the AspNetUserLogins table
    b.ToTable("AspNetUserLogins");
});

builder.Entity<TUserToken>(b =>
{
    // Composite primary key consisting of the UserId, LoginProvider and Name
    b.HasKey(t => new { t.UserId, t.LoginProvider, t.Name });

    // Limit the size of the composite key columns due to common database restrictions
    b.Property(t => t.LoginProvider).HasMaxLength(maxKeyLength);
    b.Property(t => t.Name).HasMaxLength(maxKeyLength);

    // Maps to the AspNetUserTokens table
    b.ToTable("AspNetUserTokens");
});

builder.Entity<TRole>(b =>
{
    // Primary key
    b.HasKey(r => r.Id);

    // Index for "normalized" role name to allow efficient lookups
    b.HasIndex(r => r.NormalizedName).HasName("RoleNameIndex").IsUnique();

    // Maps to the AspNetRoles table
    b.ToTable("AspNetRoles");

    // A concurrency token for use with the optimistic concurrency checking
    b.Property(r => r.ConcurrencyStamp).IsConcurrencyToken();

    // Limit the size of columns to use efficient database types
    b.Property(u => u.Name).HasMaxLength(256);
    b.Property(u => u.NormalizedName).HasMaxLength(256);

    // The relationships between Role and other entity types
    // Note that these relationships are configured with no navigation properties

    // Each Role can have many entries in the UserRole join table
    b.HasMany<TUserRole>().WithOne().HasForeignKey(ur => ur.RoleId).IsRequired();

    // Each Role can have many associated RoleClaims
    b.HasMany<TRoleClaim>().WithOne().HasForeignKey(rc => rc.RoleId).IsRequired();
});

builder.Entity<TRoleClaim>(b =>
{
    // Primary key
    b.HasKey(rc => rc.Id);

    // Maps to the AspNetRoleClaims table
    b.ToTable("AspNetRoleClaims");
});

builder.Entity<TUserRole>(b =>
{
    // Primary key
    b.HasKey(r => new { r.UserId, r.RoleId });

    // Maps to the AspNetUserRoles table
    b.ToTable("AspNetUserRoles");
});
```

### <a name="model-generic-types"></a><span data-ttu-id="809b7-151">모델 제네릭 형식</span><span class="sxs-lookup"><span data-stu-id="809b7-151">Model generic types</span></span>

<span data-ttu-id="809b7-152">Identity 위에 나열 된 엔터티 형식의 각각에 대해 기본 CLR 형식을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-152">Identity defines default CLR types for each of the entity types listed above.</span></span> <span data-ttu-id="809b7-153">이러한 형식은 모두 "Id"와 접두사가: `IdentityUser`, `IdentityRole`, `IdentityUserClaim`, `IdentityUserToken`, `IdentityUserLogin`, `IdentityRoleClaim`, 및 `IdentityUserRole`합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-153">These types are all prefixed with "Identity": `IdentityUser`, `IdentityRole`, `IdentityUserClaim`, `IdentityUserToken`, `IdentityUserLogin`, `IdentityRoleClaim`, and `IdentityUserRole`.</span></span>

<span data-ttu-id="809b7-154">직접 이러한 형식을 사용 하는 대신 응용 프로그램 자체의 형식에 대 한 있는 형식은 기본 클래스로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-154">Rather than using these types directly, the types can be used as base classes for the application's own types.</span></span> <span data-ttu-id="809b7-155">`DbContext` Id로 정의 된 클래스는 제네릭 다른 CLR 형식을 하나 이상의 모델에 엔터티 형식에 대해 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-155">The `DbContext` classes defined by Identity are generic such that different CLR types can be used for one or more of the entity types in the model.</span></span> <span data-ttu-id="809b7-156">이 제네릭 형식도 허용 사용자 기본 키의 형식에 대 한 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-156">These generic types also allow for the type of the User primary key to be changed.</span></span>

<span data-ttu-id="809b7-157">역할에 대 한 지원과 함께 Id를 사용 하는 경우는 [IdentityDbContext](/dotnet/api/microsoft.aspnetcore.identity.entityframeworkcore.identitydbcontext) 클래스를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-157">When using Identity with support for roles, an [IdentityDbContext](/dotnet/api/microsoft.aspnetcore.identity.entityframeworkcore.identitydbcontext) class should be used:</span></span>

```CSharp
// Uses all the built-in Identity types
// Uses `string` as the key type
public class IdentityDbContext
    : IdentityDbContext<IdentityUser, IdentityRole, string>
{
}

// Uses the built-in Identity types except with a custom User type
// Uses `string` as the key type
public class IdentityDbContext<TUser>
    : IdentityDbContext<TUser, IdentityRole, string>
        where TUser : IdentityUser
{
}

// Uses the built-in Identity types except with custom User and Role types
// The key type is defined by TKey
public class IdentityDbContext<TUser, TRole, TKey>
    : IdentityDbContext<TUser, TRole, TKey, IdentityUserClaim<TKey>, IdentityUserRole<TKey>, IdentityUserLogin<TKey>, IdentityRoleClaim<TKey>, IdentityUserToken<TKey>>
        where TUser : IdentityUser<TKey>
        where TRole : IdentityRole<TKey>
        where TKey : IEquatable<TKey>
{
}

// No built-in Identity types are used; all are specified by generic arguments
// The key type is defined by TKey
public abstract class IdentityDbContext<TUser, TRole, TKey, TUserClaim, TUserRole, TUserLogin, TRoleClaim, TUserToken>
    : IdentityUserContext<TUser, TKey, TUserClaim, TUserLogin, TUserToken>
         where TUser : IdentityUser<TKey>
         where TRole : IdentityRole<TKey>
         where TKey : IEquatable<TKey>
         where TUserClaim : IdentityUserClaim<TKey>
         where TUserRole : IdentityUserRole<TKey>
         where TUserLogin : IdentityUserLogin<TKey>
         where TRoleClaim : IdentityRoleClaim<TKey>
         where TUserToken : IdentityUserToken<TKey>

```

<span data-ttu-id="809b7-158">역할 (클레임만),이 경우 Id를 사용 하도록 수 이기도 한 `IdentityUserContext` 클래스를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-158">It is also possible to use Identity without roles (only claims), in which case an `IdentityUserContext` class should be used:</span></span>


```CSharp
// Uses the built-in non-role Identity types except with a custom User type
// Uses `string` as the key type
public class IdentityUserContext<TUser>
    : IdentityUserContext<TUser, string>
        where TUser : IdentityUser
{
}

// Uses the built-in non-role Identity types except with a custom User type
// The key type is defined by TKey
public class IdentityUserContext<TUser, TKey>
    : IdentityUserContext<TUser, TKey, IdentityUserClaim<TKey>, IdentityUserLogin<TKey>, IdentityUserToken<TKey>>
        where TUser : IdentityUser<TKey>
        where TKey : IEquatable<TKey>
{
}

// No built-in Identity types are used; all are specified by generic arguments, with no roles
// The key type is defined by TKey
public abstract class IdentityUserContext<TUser, TKey, TUserClaim, TUserLogin, TUserToken>
    : DbContext
        where TUser : IdentityUser<TKey>
        where TKey : IEquatable<TKey>
        where TUserClaim : IdentityUserClaim<TKey>
        where TUserLogin : IdentityUserLogin<TKey>
        where TUserToken : IdentityUserToken<TKey>
{
}
```

## <a name="customizing-the-model"></a><span data-ttu-id="809b7-159">모델을 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="809b7-159">Customizing the model</span></span>

<span data-ttu-id="809b7-160">적절 한 컨텍스트 형식;에서 파생 하는 모델을 사용자 지정 하기 위한 시작 지점 이전 섹션을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="809b7-160">The starting point for customizing the model is to derive from the appropriate context type; see the preceding section.</span></span> <span data-ttu-id="809b7-161">이 컨텍스트 형식은 라고 관례적 `ApplicationDbContext` ASP.NET Core 템플릿에 의해 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-161">This context type is customarily called `ApplicationDbContext` and is created by the ASP.NET Core templates.</span></span>

<span data-ttu-id="809b7-162">컨텍스트를 사용 하 여 두 가지 방법으로 모델을 구성 하려면:</span><span class="sxs-lookup"><span data-stu-id="809b7-162">The context is used to configure the model in two ways:</span></span>
* <span data-ttu-id="809b7-163">엔터티 및 키 형식을 제네릭 형식 매개 변수를 제공 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-163">By supplying entity and key types for the generic type parameters.</span></span>
* <span data-ttu-id="809b7-164">재정의 하 여 `OnModelCreating` 이러한 형식의 매핑을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-164">By overriding `OnModelCreating` to modify the mapping of these types.</span></span>

<span data-ttu-id="809b7-165">재정의 하는 경우 `OnModelCreating`, `base.OnModelCreating` 먼저 호출 되어야, 재정의 하는 구성 다음 호출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-165">When overriding `OnModelCreating`, `base.OnModelCreating` should be called first, the overriding configuration should be called next.</span></span> <span data-ttu-id="809b7-166">EF 코어에는 일반적으로 구성에 대 한 최신 하나 업데이트 정책을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-166">EF Core generally has a last-one-wins policy for configuration.</span></span> <span data-ttu-id="809b7-167">예를 들어 경우는 `ToTable` 엔터티에 대 한 형식은 하나의 테이블 이름의 처음 호출 하 고 다른 테이블 이름을 사용할 경우 나중에 다시 다음 다음 두 번째 호출에서 테이블 이름이 사용 되는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-167">For example, if the `ToTable` for an entity type is called first with one table name and then again later with a different table name, then the table name in the second call is the one that is used.</span></span>

### <a name="using-a-custom-user-type"></a><span data-ttu-id="809b7-168">사용자 지정 사용자 형식을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="809b7-168">Using a custom User type</span></span>

<span data-ttu-id="809b7-169">사용자 지정 사용자 유형을 사용 하는 형식을 만들고에서 상속 하 게 `IdentityUser`합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-169">To use a custom User type, create the type and have it inherit from `IdentityUser`.</span></span> <span data-ttu-id="809b7-170">이 형식의 이름을 지정 하는 일반적인은 `ApplicationUser`합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-170">It is customary to name this type `ApplicationUser`.</span></span> <span data-ttu-id="809b7-171">이 형식은 기본 형식에 없는 추가 속성을 일반적으로, 그렇지 않으면 없습니다 것 값이 없는 만드는.</span><span class="sxs-lookup"><span data-stu-id="809b7-171">This type will typically have additional properties not in the base type, otherwise there would be no value in creating it.</span></span> <span data-ttu-id="809b7-172">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="809b7-172">For example:</span></span>

```CSharp
public class ApplicationUser : IdentityUser
{
    public string CustomTag { get; set; }
}
```

<span data-ttu-id="809b7-173">다음이 형식을 사용 하 여 컨텍스트를 제네릭 인수로:</span><span class="sxs-lookup"><span data-stu-id="809b7-173">Next use this type as a generic argument for the context:</span></span>

```CSharp
public class ApplicationDbContext : IdentityDbContext<ApplicationUser>
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
        : base(options)
    {
    }
}
```

<span data-ttu-id="809b7-174">업데이트 `ConfigureServices` 사용할 새 `ApplicationUser` 클래스:</span><span class="sxs-lookup"><span data-stu-id="809b7-174">Update `ConfigureServices` to use the new `ApplicationUser` class:</span></span>

```CSharp
services.AddDefaultIdentity<ApplicationUser>()
    .AddEntityFrameworkStores<ApplicationDbContext>();
```

<span data-ttu-id="809b7-175">재정의할 필요가 없습니다 `OnModelCreating` EF 코어 매핑됩니다 때문에 여기서는 `CustomTag` 규칙에 따라 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-175">There is no need to override `OnModelCreating` here because EF Core will map the `CustomTag` property by convention.</span></span> <span data-ttu-id="809b7-176">그러나 데이터베이스는 새 가져오려는 업데이트 해야 할 `CustomTag` 열입니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-176">However, the database will need to be updated to get a new `CustomTag` column.</span></span> <span data-ttu-id="809b7-177">이 위해 마이그레이션, 추가 하 고 다음에 설명 된 대로 데이터베이스를 업데이트 [Id 및 EF 코어 마이그레이션](#identity-migrations)합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-177">To do this, add a migration, and then update the database as described in  [Identity and EF Core Migrations](#identity-migrations).</span></span>

### <a name="changing-the-key-type"></a><span data-ttu-id="809b7-178">키 유형 변경</span><span class="sxs-lookup"><span data-stu-id="809b7-178">Changing the key type</span></span>

<span data-ttu-id="809b7-179">데이터베이스를 만든 후 기본 키 열 (PK)의 형식을 변경 하는 것은 많은 데이터베이스 시스템에 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-179">Changing the type of a primary key (PK) column after the database has been created is problematic on many database systems.</span></span> <span data-ttu-id="809b7-180">일반적으로 PK 변경를 삭제 하 고 다시 테이블을 만드는 작업이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-180">Changing the PK typically involves dropping and re-creating the table.</span></span> <span data-ttu-id="809b7-181">따라서 데이터베이스를 만들 때 대상 키 형식을 만드는 경우는 되도록 초기 마이그레이션에서는 키 형식을 지정할 수는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-181">Therefore, it is recommended that key types be specified in the initial migration such that the target key types are created when the database is created.</span></span>

<span data-ttu-id="809b7-182">데이터베이스에 생성 된 경우 다음 `Drop-Database` (PMC) 또는 `dotnet ef database drop` (.NET 코어 CLI)를 사용 하 여 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-182">If the database has been created, then `Drop-Database` (PMC) or `dotnet ef database drop` (.NET Core CLI) can be used to delete it.</span></span>

<span data-ttu-id="809b7-183">데이터베이스가 존재 하지 않습니다 확인 되 면 제거 된 초기 마이그레이션 `Remove-Migration` (PMC) 또는 `dotnet ef migrations remove` .NET Core CLI ().</span><span class="sxs-lookup"><span data-stu-id="809b7-183">Once it is confirmed that the database doesn't exist,  remove the initial migration with `Remove-Migration` (PMC) or `dotnet ef migrations remove` (.NET Core CLI).</span></span>

<span data-ttu-id="809b7-184">업데이트는 `ApplicationDbContext` 에 대 한 새 키 형식을 지정 하는 다른 기본 클래스를 사용 하도록 `TKey`합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-184">Update the `ApplicationDbContext` to use a different base class, specifying the new key type for `TKey`.</span></span> <span data-ttu-id="809b7-185">예를 들어, 사용 하는 `Guid` 키:</span><span class="sxs-lookup"><span data-stu-id="809b7-185">For example, to use a `Guid` key:</span></span>

```CSharp
public class ApplicationDbContext : IdentityDbContext<IdentityUser<Guid>, IdentityRole<Guid>, Guid>
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
        : base(options)
    {
    }
}
```

<span data-ttu-id="809b7-186">제네릭 클래스 `IdentityUser<TKey>` 및 `IdentityRole<TKey>` 새 키 유형을 사용 하도록 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-186">Notice that the generic classes `IdentityUser<TKey>` and `IdentityRole<TKey>` must also be specified to use the new key type.</span></span> <span data-ttu-id="809b7-187">`ConfigureServices` 일반 사용자를 사용 하도록 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-187">`ConfigureServices` must be updated to use the generic user:</span></span>

```CSharp
services.AddDefaultIdentity<IdentityUser<Guid>>()
    .AddEntityFrameworkStores<ApplicationDbContext>();
```

<span data-ttu-id="809b7-188">사용자 지정 하는 경우 `ApplicationUser` 은에서 상속 하도록 업데이트 사용 중인 `IdentityUser<TKey>`합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-188">If a custom `ApplicationUser` is being used, update it to inherit from `IdentityUser<TKey>`.</span></span> <span data-ttu-id="809b7-189">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="809b7-189">For example:</span></span>

```CSharp
public class ApplicationUser : IdentityUser<Guid>
{
    public string CustomTag { get; set; }
}

public class ApplicationDbContext : IdentityDbContext<ApplicationUser, IdentityRole<Guid>, Guid>
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
        : base(options)
    {
    }
}
```

```CSharp
services.AddDefaultIdentity<ApplicationUser>()
    .AddEntityFrameworkStores<ApplicationDbContext>();
```

### <a name="adding-navigation-properties"></a><span data-ttu-id="809b7-190">탐색 속성 추가</span><span class="sxs-lookup"><span data-stu-id="809b7-190">Adding navigation properties</span></span>

<span data-ttu-id="809b7-191">관계에 대 한 모델 구성을 변경 하는 것은 기타 변경을 보다 더 어려울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-191">Changing the model configuration for relationships can be a more difficult than making other changes.</span></span> <span data-ttu-id="809b7-192">기존 관계 교체가에 비해 새로운 추가 관계를 만들 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-192">Care must be taken to replace the existing relationships rather than create a new additional relationships.</span></span> <span data-ttu-id="809b7-193">특히, 변경 된 관계는 기존 관계와 같은 외래 키 속성을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-193">In particular, the changed relationship must specify the same foreign key property as the existing relationship.</span></span> <span data-ttu-id="809b7-194">예를 들어 간의 관계 `Users` 및 `UserClaims` 기본값이 지정 된 경우:</span><span class="sxs-lookup"><span data-stu-id="809b7-194">For example, the relationship between `Users` and `UserClaims` is by default specified as:</span></span>

```CSharp
builder.Entity<TUser>(b =>
{
    // Each User can have many UserClaims
    b.HasMany<TUserClaim>()
     .WithOne()
     .HasForeignKey(uc => uc.UserId)
     .IsRequired();
});
```

<span data-ttu-id="809b7-195">이 관계에 대 한 외래 키로 지정 되는 `UserClaim.UserId` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-195">The foreign key for this relationship is specified as the `UserClaim.UserId` property.</span></span> <span data-ttu-id="809b7-196">`HasMany` 및 `WithOne` 탐색 속성이 없는 관계를 만들 수는 인수 없이 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-196">`HasMany` and `WithOne` are called without arguments to create the relationship without navigation properties.</span></span>

<span data-ttu-id="809b7-197">탐색 속성을 추가 `ApplicationUser` 연결 수 `UserClaims` 사용자에서 참조 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-197">Add a navigation property to `ApplicationUser` that will allow associated `UserClaims` to be referenced from the user:</span></span>

```CSharp
public class ApplicationUser : IdentityUser
{
    public virtual ICollection<IdentityUserClaim<string>> Claims { get; set; }
}
```

<span data-ttu-id="809b7-198">`TKey` 에 대 한 `IdentityUserClaim<TKey>` -이 경우 사용자의 기본 키에 대 한 지정 된 형식이 `string` 기본값 사용 하므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-198">Note that the `TKey` for `IdentityUserClaim<TKey>` is type specified for the primary key of users--in this case `string` since we're using the defaults.</span></span> <span data-ttu-id="809b7-199">**하지** 에 대 한 기본 키 유형을 `UserClaim` 엔터티 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-199">It is **not** the primary key type for the `UserClaim` entity type.</span></span>

<span data-ttu-id="809b7-200">구성에서 해야 탐색 속성이 있는 했으므로 `OnModelCreating`:</span><span class="sxs-lookup"><span data-stu-id="809b7-200">Now that the navigation property exists it must be configured in `OnModelCreating`:</span></span>

```CSharp
public class ApplicationDbContext : IdentityDbContext<ApplicationUser>
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
        : base(options)
    {
    }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        base.OnModelCreating(modelBuilder);

        modelBuilder.Entity<ApplicationUser>(b =>
        {
            // Each User can have many UserClaims
            b.HasMany(e => e.Claims)
                .WithOne()
                .HasForeignKey(uc => uc.UserId)
                .IsRequired();
        });
    }
}
```

<span data-ttu-id="809b7-201">관계 된 대로 정확 하 게 하면 이전에 대 한 호출에 지정 된 탐색 속성에만 구성 되어 `HasMany`합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-201">Notice that relationship is configured exactly as it was before, only with a navigation property specified in the call to `HasMany`.</span></span>

<span data-ttu-id="809b7-202">탐색 속성에서 데이터베이스가 아니라 EF 모델에만 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-202">The navigation properties only exist in the EF model, not the database.</span></span> <span data-ttu-id="809b7-203">외래 키 관계에 대 한 변경 되지 않았기 때문에 이러한 종류의 모델 변경 데이터베이스를 업데이트할 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-203">Because the foreign key for the relationship has not changed, this kind of model change does not require the database to be updated.</span></span> <span data-ttu-id="809b7-204">이 변경을 수행한 후 마이그레이션을 추가 하 여 확인할 수 있습니다:는 `Up` 및 `Down` 메서드는 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-204">This can be checked by adding a migration after making the change: the `Up` and `Down` methods are empty.</span></span>

### <a name="adding-all-user-navigation-properties"></a><span data-ttu-id="809b7-205">모든 사용자 탐색 속성 추가</span><span class="sxs-lookup"><span data-stu-id="809b7-205">Adding all User navigation properties</span></span>

<span data-ttu-id="809b7-206">여기 위의 섹션을 사용 하 여 지침으로,은 사용자에 모든 관계에 대 한 단방향 탐색 속성을 구성 하는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-206">Using the section above as guidance, here is an example that configures unidirectional navigation properties for all relationships on User:</span></span>

```CSharp
public class ApplicationUser : IdentityUser
{
    public virtual ICollection<IdentityUserClaim<string>> Claims { get; set; }
    public virtual ICollection<IdentityUserLogin<string>> Logins { get; set; }
    public virtual ICollection<IdentityUserToken<string>> Tokens { get; set; }
    public virtual ICollection<IdentityUserRole<string>> UserRoles { get; set; }
}
```

```CSharp
public class ApplicationDbContext : IdentityDbContext<ApplicationUser>
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
        : base(options)
    {
    }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        base.OnModelCreating(modelBuilder);

        modelBuilder.Entity<ApplicationUser>(b =>
        {
            // Each User can have many UserClaims
            b.HasMany(e => e.Claims)
                .WithOne()
                .HasForeignKey(uc => uc.UserId)
                .IsRequired();

            // Each User can have many UserLogins
            b.HasMany(e => e.Logins)
                .WithOne()
                .HasForeignKey(ul => ul.UserId)
                .IsRequired();

            // Each User can have many UserTokens
            b.HasMany(e => e.Tokens)
                .WithOne()
                .HasForeignKey(ut => ut.UserId)
                .IsRequired();

            // Each User can have many entries in the UserRole join table
            b.HasMany(e => e.UserRoles)
                .WithOne()
                .HasForeignKey(ur => ur.UserId)
                .IsRequired();
        });
    }
}
```

### <a name="adding-user-and-role-navigation-properties"></a><span data-ttu-id="809b7-207">사용자 및 역할 탐색 속성 추가</span><span class="sxs-lookup"><span data-stu-id="809b7-207">Adding User and Role navigation properties</span></span>

<span data-ttu-id="809b7-208">위의 섹션을 사용 하 여 지침으로, 사용자 및 역할에서 모든 관계에 대 한 탐색 속성을 구성 하는 예제 다음은:</span><span class="sxs-lookup"><span data-stu-id="809b7-208">Using the section above as guidance, here is an example that configures navigation properties for all relationships on User and Role:</span></span>

```CSharp
public class ApplicationUser : IdentityUser
{
    public virtual ICollection<IdentityUserClaim<string>> Claims { get; set; }
    public virtual ICollection<IdentityUserLogin<string>> Logins { get; set; }
    public virtual ICollection<IdentityUserToken<string>> Tokens { get; set; }
    public virtual ICollection<ApplicationUserRole> UserRoles { get; set; }
}

public class ApplicationRole : IdentityRole
{
    public virtual ICollection<ApplicationUserRole> UserRoles { get; set; }
}

public class ApplicationUserRole : IdentityUserRole<string>
{
    public virtual ApplicationUser User { get; set; }
    public virtual ApplicationRole Role { get; set; }
}
```

```CSharp
public class ApplicationDbContext
    : IdentityDbContext<
        ApplicationUser, ApplicationRole, string,
        IdentityUserClaim<string>, ApplicationUserRole, IdentityUserLogin<string>,
        IdentityRoleClaim<string>, IdentityUserToken<string>>
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
        : base(options)
    {
    }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        base.OnModelCreating(modelBuilder);

        modelBuilder.Entity<ApplicationUser>(b =>
        {
            // Each User can have many UserClaims
            b.HasMany(e => e.Claims)
                .WithOne()
                .HasForeignKey(uc => uc.UserId)
                .IsRequired();

            // Each User can have many UserLogins
            b.HasMany(e => e.Logins)
                .WithOne()
                .HasForeignKey(ul => ul.UserId)
                .IsRequired();

            // Each User can have many UserTokens
            b.HasMany(e => e.Tokens)
                .WithOne()
                .HasForeignKey(ut => ut.UserId)
                .IsRequired();

            // Each User can have many entries in the UserRole join table
            b.HasMany(e => e.UserRoles)
                .WithOne(e => e.User)
                .HasForeignKey(ur => ur.UserId)
                .IsRequired();
        });

        modelBuilder.Entity<ApplicationRole>(b =>
        {
            // Each Role can have many entries in the UserRole join table
            b.HasMany(e => e.UserRoles)
                .WithOne(e => e.Role)
                .HasForeignKey(ur => ur.RoleId)
                .IsRequired();
        });

    }
}
```

<span data-ttu-id="809b7-209">메모:</span><span class="sxs-lookup"><span data-stu-id="809b7-209">Notes:</span></span>

* <span data-ttu-id="809b7-210">이 예제도 포함 되어는 `UserRole` 역할에 사용자의 다 대 다 관계를 탐색 하는 데 필요한 엔터티를 조인 합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-210">This example also includes the `UserRole` join entity, which is needed to navigate the many-to-many relationship from Users to Roles.</span></span>
* <span data-ttu-id="809b7-211">반영 하기 위해 탐색 속성의 형식을 변경 해야 `ApplicationXxx` 형식을 현재 사용 되 고 대신 `IdentityXxx` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-211">Remember to change the types of the navigation properties to reflect that `ApplicationXxx` types are now being used instead of `IdentityXxx` types.</span></span>
* <span data-ttu-id="809b7-212">사용 해야는 `ApplicationXxx` 제네릭에서 `ApplicationContext` 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-212">Remember to use the `ApplicationXxx` in the generic `ApplicationContext` definition.</span></span>

### <a name="adding-all-navigation-properties"></a><span data-ttu-id="809b7-213">모든 탐색 속성 추가</span><span class="sxs-lookup"><span data-stu-id="809b7-213">Adding all navigation properties</span></span>

<span data-ttu-id="809b7-214">다음 위의 섹션을 사용 하 여 지침으로,은 모든 엔터티 형식에 대해 모든 관계에 대 한 탐색 속성을 구성 하는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-214">Using the section above as guidance, here is an example that configures navigation properties for all relationships on all entity types:</span></span>

```CSharp
public class ApplicationUser : IdentityUser
{
    public virtual ICollection<ApplicationUserClaim> Claims { get; set; }
    public virtual ICollection<ApplicationUserLogin> Logins { get; set; }
    public virtual ICollection<ApplicationUserToken> Tokens { get; set; }
    public virtual ICollection<ApplicationUserRole> UserRoles { get; set; }
}

public class ApplicationRole : IdentityRole
{
    public virtual ICollection<ApplicationUserRole> UserRoles { get; set; }
    public virtual ICollection<ApplicationRoleClaim> RoleClaims { get; set; }
}

public class ApplicationUserRole : IdentityUserRole<string>
{
    public virtual ApplicationUser User { get; set; }
    public virtual ApplicationRole Role { get; set; }
}

public class ApplicationUserClaim : IdentityUserClaim<string>
{
    public virtual ApplicationUser User { get; set; }
}

public class ApplicationUserLogin : IdentityUserLogin<string>
{
    public virtual ApplicationUser User { get; set; }
}

public class ApplicationRoleClaim : IdentityRoleClaim<string>
{
    public virtual ApplicationRole Role { get; set; }
}

public class ApplicationUserToken : IdentityUserToken<string>
{
    public virtual ApplicationUser User { get; set; }
}
```

```CSharp
public class ApplicationDbContext
    : IdentityDbContext<
        ApplicationUser, ApplicationRole, string,
        ApplicationUserClaim, ApplicationUserRole, ApplicationUserLogin,
        ApplicationRoleClaim, ApplicationUserToken>
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
        : base(options)
    {
    }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        base.OnModelCreating(modelBuilder);

        modelBuilder.Entity<ApplicationUser>(b =>
        {
            // Each User can have many UserClaims
            b.HasMany(e => e.Claims)
                .WithOne(e => e.User)
                .HasForeignKey(uc => uc.UserId)
                .IsRequired();

            // Each User can have many UserLogins
            b.HasMany(e => e.Logins)
                .WithOne(e => e.User)
                .HasForeignKey(ul => ul.UserId)
                .IsRequired();

            // Each User can have many UserTokens
            b.HasMany(e => e.Tokens)
                .WithOne(e => e.User)
                .HasForeignKey(ut => ut.UserId)
                .IsRequired();

            // Each User can have many entries in the UserRole join table
            b.HasMany(e => e.UserRoles)
                .WithOne(e => e.User)
                .HasForeignKey(ur => ur.UserId)
                .IsRequired();
        });

        modelBuilder.Entity<ApplicationRole>(b =>
        {
            // Each Role can have many entries in the UserRole join table
            b.HasMany(e => e.UserRoles)
                .WithOne(e => e.Role)
                .HasForeignKey(ur => ur.RoleId)
                .IsRequired();

            // Each Role can have many associated RoleClaims
            b.HasMany(e => e.RoleClaims)
                .WithOne(e => e.Role)
                .HasForeignKey(rc => rc.RoleId)
                .IsRequired();
        });

    }
}
```

### <a name="using-composite-keys"></a><span data-ttu-id="809b7-215">복합 키를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="809b7-215">Using composite keys</span></span>

<span data-ttu-id="809b7-216">앞의 섹션에서는 Id 모델에 사용 된 키 유형을 변경 하 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-216">The preceding sections demonstrated changing the type of key used in the Identity model.</span></span> <span data-ttu-id="809b7-217">복합 키를 사용 하려면 Id 키 모델 변경은 지원 되지 않거나 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-217">Changing the Identity key model to use composite keys is not supported or recommended.</span></span> <span data-ttu-id="809b7-218">Identity manager 코드는 지원 되지 않는 사용자 지정 모델을 사용 하 고이 문서의 범위를 벗어나는 상호 작용 하는 방식 변경 Id를 가진 복합 키를 사용 하는 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-218">Using a composite key with Identity would involve changing how the Identity manager code interacts with the model, which is an unsupported customization and beyond the scope of this document.</span></span>

### <a name="changing-tablecolumn-names-and-facets"></a><span data-ttu-id="809b7-219">테이블/열 이름과 패싯을 변경</span><span class="sxs-lookup"><span data-stu-id="809b7-219">Changing table/column names and facets</span></span>

<span data-ttu-id="809b7-220">열과 테이블의 이름을 변경 하려면 호출 `base.OnModelCreating`, 다음 기본값을 재정의 하는 구성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-220">To change the names of tables and columns, call `base.OnModelCreating`, and then add configuration to override any of the defaults.</span></span> <span data-ttu-id="809b7-221">예를 들어, 모든 identity 테이블의 이름을 변경 하려면:</span><span class="sxs-lookup"><span data-stu-id="809b7-221">For example, to change the name of all the identity tables:</span></span>

```CSharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    base.OnModelCreating(modelBuilder);

    modelBuilder.Entity<IdentityUser>(b =>
    {
        b.ToTable("MyUsers");
    });

    modelBuilder.Entity<IdentityUserClaim<string>>(b =>
    {
        b.ToTable("MyUserClaims");
    });

    modelBuilder.Entity<IdentityUserLogin<string>>(b =>
    {
        b.ToTable("MyUserLogins");
    });

    modelBuilder.Entity<IdentityUserToken<string>>(b =>
    {
        b.ToTable("MyUserTokens");
    });

    modelBuilder.Entity<IdentityRole>(b =>
    {
        b.ToTable("MyRoles");
    });

    modelBuilder.Entity<IdentityRoleClaim<string>>(b =>
    {
        b.ToTable("MyRoleClaims");
    });

    modelBuilder.Entity<IdentityUserRole<string>>(b =>
    {
        b.ToTable("MyUserRoles");
    });
}
```

<span data-ttu-id="809b7-222">이 예제에서는 기본 Id 유형을 사용 하는 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-222">Note that these examples use the default Identity types.</span></span> <span data-ttu-id="809b7-223">응용 프로그램 종류와 같은 사용 중인 경우 `ApplicationUser` 기본 형식 대신 해당 형식을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-223">If you are using an application type, such as `ApplicationUser` then configure that type instead of the default type.</span></span>

<span data-ttu-id="809b7-224">일부 열 이름을 변경 하는 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-224">Here is an example that changes some column names:</span></span>

```CSharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    base.OnModelCreating(modelBuilder);

    modelBuilder.Entity<IdentityUser>(b =>
    {
        b.Property(e => e.Email).HasColumnName("EMail");
    });

    modelBuilder.Entity<IdentityUserClaim<string>>(b =>
    {
        b.Property(e => e.ClaimType).HasColumnName("CType");
        b.Property(e => e.ClaimValue).HasColumnName("CValue");
    });
}
```

<span data-ttu-id="809b7-225">특정으로 일부 유형의 데이터베이스 열을 구성할 수 있습니다 _패싯_ 허용 되는 최대 문자열 길이 등입니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-225">Some types of database columns can be configured with certain _facets_ such as the maximum string length allowed.</span></span> <span data-ttu-id="809b7-226">모델에 여러 문자열 속성에 열 최대 길이 설정 하는 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-226">Here is an example that sets column max lengths for several string properties in the model:</span></span>

```CSharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    base.OnModelCreating(modelBuilder);

    modelBuilder.Entity<IdentityUser>(b =>
    {
        b.Property(u => u.UserName).HasMaxLength(128);
        b.Property(u => u.NormalizedUserName).HasMaxLength(128);
        b.Property(u => u.Email).HasMaxLength(128);
        b.Property(u => u.NormalizedEmail).HasMaxLength(128);
    });

    modelBuilder.Entity<IdentityUserToken<string>>(b =>
    {
        b.Property(t => t.LoginProvider).HasMaxLength(128);
        b.Property(t => t.Name).HasMaxLength(128);
    });
}
```

### <a name="mapping-to-a-different-schema"></a><span data-ttu-id="809b7-227">다른 스키마에 매핑</span><span class="sxs-lookup"><span data-stu-id="809b7-227">Mapping to a different schema</span></span>

<span data-ttu-id="809b7-228">스키마의 다른 데이터베이스 공급자에서에서 다르게 동작할 수 있습니다 하지만 SQL Server에 대 한 기본값 "dbo" 스키마의 모든 테이블을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-228">Schemas can behave differently in different database providers, but for SQL Server, the default is to create all tables in the "dbo" schema.</span></span> <span data-ttu-id="809b7-229">대신 다른 스키마에 테이블을 만들기 위해이 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-229">This can be changed to instead create the tables in a different schema.</span></span> <span data-ttu-id="809b7-230">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="809b7-230">For example:</span></span>

```CSharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    base.OnModelCreating(modelBuilder);

    modelBuilder.HasDefaultSchema("notdbo");
}
```

### <a name="lazy-loading"></a><span data-ttu-id="809b7-231">지연 로드</span><span class="sxs-lookup"><span data-stu-id="809b7-231">Lazy loading</span></span>

<span data-ttu-id="809b7-232">이 섹션의 지연 로드 프록시 Id 모델에 대 한 지원이 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-232">In this section support for lazy-loading proxies in the Identity model is added.</span></span> <span data-ttu-id="809b7-233">Lazy 로드는 탐색 속성을 로드 되는 첫 번째 확인 하지 않고 사용할 수 있기 때문에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-233">Lazy-loading is useful since it allows navigation properties to be used without first ensuring they are loaded.</span></span>

<span data-ttu-id="809b7-234">엔터티 형식을 만들 수 있습니다에 적합 한 여러 가지 방법으로 지연 로드에 설명 된 대로 [EF 핵심 설명서](/ef/core/querying/related-data#lazy-loading)합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-234">Entity types can be made suitable for lazy-loading in several ways, as described in the [EF Core documentation](/ef/core/querying/related-data#lazy-loading).</span></span> <span data-ttu-id="809b7-235">간단히 하기 위해 사용 합니다 지연 로드 프록시 해야 함:</span><span class="sxs-lookup"><span data-stu-id="809b7-235">For simplicity, we will use lazy-loading proxies, which requires:</span></span>

* <span data-ttu-id="809b7-236">설치는 [Microsoft.EntityFrameworkCore.Proxies](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Proxies/) 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-236">Installation of the [Microsoft.EntityFrameworkCore.Proxies](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Proxies/) package.</span></span>
* <span data-ttu-id="809b7-237">에 대 한 호출 `.UseLazyLoadingProxies()` 내 `AddDbContext`합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-237">A call to `.UseLazyLoadingProxies()` inside `AddDbContext`.</span></span>
* <span data-ttu-id="809b7-238">공용 가상 탐색 속성이 있는 public 엔터티 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-238">Public entity types with public virtual navigation properties.</span></span>

<span data-ttu-id="809b7-239">호출의 예로 `.UseLazyLoadingProxies()`:</span><span class="sxs-lookup"><span data-stu-id="809b7-239">Here is an example of calling `.UseLazyLoadingProxies()`:</span></span>

```CSharp
services
    .AddDbContext<ApplicationDbContext>(
        b => b.UseSqlServer(connectionString)
            .UseLazyLoadingProxies())
    .AddDefaultIdentity<ApplicationUser>()
    .AddEntityFrameworkStores<ApplicationDbContext>();
```

<span data-ttu-id="809b7-240">위 예제는 엔터티 형식에 탐색 속성을 추가 하기 위한 다시 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="809b7-240">Refer back to the examples above for adding navigation properties to the entity types.</span></span>
