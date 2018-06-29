---
title: Identity 모델 사용자 지정
author: ajcvickers
description: 이 문서에는 ASP.NET Core Id에 대 한 기본 Framework Core 엔터티 데이터 모델을 사용자 지정 하는 방법을 설명 합니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: avickers
ms.date: 04/12/2018
uid: security/authentication/customize_identity_model
ms.openlocfilehash: 41ea125414c5997ee36f4e312beba4ff318a4a8d
ms.sourcegitcommit: 931b6a2d7eb28a0f1295e8a95690b8c4c5f58477
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37077681"
---
# <a name="identity-model-customization"></a>Identity 모델 사용자 지정

으로 [Arthur Vickers](https://github.com/ajcvickers)

ASP.NET Core Identity ASP.NET Core 응용 프로그램에서 사용자 계정을 저장 및 관리 하기 위한 프레임 워크를 제공 합니다. Identity "개별 사용자 계정" 인증 메커니즘으로 선택 된 경우 프로젝트에 추가 됩니다. 에서는 기본적으로 Identity는 Entity Framework (EF)를 사용 하 여 핵심 데이터 모델입니다. 이 문서에서는 Id 모델을 사용자 지정 하는 방법을 설명 합니다.

<a name="identity-migrations"></a>

## <a name="identity-and-ef-core-migrations"></a>Id 및 EF 코어 마이그레이션

모델을 검사 하기 전에 Identity와 작동 하는 방법을 이해 하는 데 유용이 [EF 코어 마이그레이션](/ef/core/managing-schemas/migrations/) 를 만들고 데이터베이스를 업데이트 합니다. 최상위 수준에 프로세스는.

1. 정의 또는 업데이트 한 [코드에서 데이터 모델](/ef/core/modeling/)합니다.
1. 이 모델 데이터베이스에 적용할 수 있는 변경 내용으로 변환할 마이그레이션을 추가 합니다.
1. 마이그레이션을 제대로 사용자의 의도 반영을 확인 합니다.
1. 마이그레이션 모델 동기화 되도록 데이터베이스를 업데이트를 적용 합니다.
1. 추가로 모델 구체화 하 고 데이터베이스 동기화 상태를 유지 하기 위해 1-4 단계를 반복 합니다.

마이그레이션 추가 되 고 사용 하 여 적용 합니다.

* [패키지 관리자 콘솔](/ef/core/miscellaneous/cli/powershell) Visual Studio를 사용 하는 경우 (PMC).
* [dotnet 명령을](/ef/core/miscellaneous/cli/dotnet) 명령줄에서.
* 응용 프로그램이 실행 될 때 오류 페이지에서 마이그레이션 링크를 선택 합니다.

ASP.NET Core 응용 프로그램이 실행 될 때 마이그레이션을 적용을 사용할 수 있는 개발 시 오류 페이지 처리기를 있습니다. 프로덕션 응용 프로그램의 경우이 마이그레이션의 SQL 스크립트를 생성 하 고 제어 된 응용 프로그램 및 데이터베이스 배포의 일부로 데이터베이스에 배포 하기에 적합 합니다.

Id를 사용 하는 새 응용 프로그램을 만든 경우 위 1과 2 단계가 이미 완료 되었습니다. 즉, 초기 데이터 모델이 이미 있으면 및 초기 마이그레이션 프로젝트에 추가 되었습니다. 초기 마이그레이션 데이터베이스에 적용 해야 합니다. 초기 마이그레이션은 데이터베이스 업데이트 (PMC), dotnet ef 데이터베이스 업데이트 (.NET Core CLI) 명령을 실행 하 여 또는 응용 프로그램이 실행 될 때 오류 페이지를 사용 하 여 수행할 수 있습니다.

앞의 단계는 모델에 변경 내용이 반복 해야 합니다.

<a name="identity-model"></a>

## <a name="the-identity-model"></a>Id 모델

### <a name="entity-types"></a>엔터티 형식

Id 모델의 7 가지 엔터티 형식으로 구성 됩니다.

* `User` -사용자를 나타냅니다
* `Role` -역할을 나타냅니다
* `UserClaim` -사용자가 소유 하는 클레임을 나타냅니다
* `UserToken` -사용자에 대 한 인증 토큰을 나타냅니다.
* `UserLogin` -는 사용자를 로그인 연결
* `RoleClaim` -역할 내의 모든 사용자에 게 부여 하는 클레임을 나타냅니다.
* `UserRole` -사용자 및 역할을 연결 하는 엔터티를 조인 합니다.

### <a name="entity-type-relationships"></a>엔터티 형식 관계

이러한 엔터티 형식은 다음과 같은 방법으로 서로를 관련이 있습니다.

* 각 `User` 가질 수 있습니다 `UserClaims`
* 각 `User` 가질 수 있습니다 `UserLogins`
* 각 `User` 가질 수 있습니다 `UserTokens`
* 각 `Role` 관련 가질 수 있습니다 `RoleClaims`
* 각 `User` 수는 관련 된 많은 `Roles`, 및 각 `Role` 많은 사용자 들과 연관 될 수 있습니다
  * 이것이 데이터베이스에 조인 테이블을 필요로 하는 다 대 다 관계입니다. 조인 테이블으로 표시 됩니다는 `UserRole` 엔터티.

### <a name="default-model-configuration"></a>기본 모델 구성

다양 한에서 상속 하는 "컨텍스트 클래스"를 정의 하는 identity [DbContext](/dotnet/api/microsoft.entityframeworkcore.dbcontext) 를 구성 하 여 모델을 사용 합니다. 이 구성을 수행 해야를 사용 하는 [EF 핵심 코드 첫 번째 Fluent API](/ef/core/modeling/) 에 [OnModelCreating](/dotnet/api/microsoft.entityframeworkcore.dbcontext.onmodelcreating#Microsoft_EntityFrameworkCore_DbContext_OnModelCreating_Microsoft_EntityFrameworkCore_ModelBuilder_) 컨텍스트 클래스의 메서드. 기본 구성은 다음과 같습니다.

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

### <a name="model-generic-types"></a>모델 제네릭 형식

Identity 위에 나열 된 엔터티 형식의 각각에 대해 기본 CLR 형식을 정의 합니다. 이러한 형식은 모두 "Id"와 접두사가: `IdentityUser`, `IdentityRole`, `IdentityUserClaim`, `IdentityUserToken`, `IdentityUserLogin`, `IdentityRoleClaim`, 및 `IdentityUserRole`합니다.

직접 이러한 형식을 사용 하는 대신 응용 프로그램 자체의 형식에 대 한 있는 형식은 기본 클래스로 사용할 수 있습니다. `DbContext` Id로 정의 된 클래스는 제네릭 다른 CLR 형식을 하나 이상의 모델에 엔터티 형식에 대해 사용할 수 있도록 합니다. 이 제네릭 형식도 허용 사용자 기본 키의 형식에 대 한 변경할 수 있습니다.

역할에 대 한 지원과 함께 Id를 사용 하는 경우는 [IdentityDbContext](/dotnet/api/microsoft.aspnetcore.identity.entityframeworkcore.identitydbcontext) 클래스를 사용 해야 합니다.

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

역할 (클레임만),이 경우 Id를 사용 하도록 수 이기도 한 `IdentityUserContext` 클래스를 사용 해야 합니다.


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

## <a name="customizing-the-model"></a>모델을 사용자 지정

적절 한 컨텍스트 형식;에서 파생 하는 모델을 사용자 지정 하기 위한 시작 지점 이전 섹션을 참조 하십시오. 이 컨텍스트 형식은 라고 관례적 `ApplicationDbContext` ASP.NET Core 템플릿에 의해 생성 됩니다.

컨텍스트를 사용 하 여 두 가지 방법으로 모델을 구성 하려면:
* 엔터티 및 키 형식을 제네릭 형식 매개 변수를 제공 하 여 합니다.
* 재정의 하 여 `OnModelCreating` 이러한 형식의 매핑을 수정할 수 있습니다.

재정의 하는 경우 `OnModelCreating`, `base.OnModelCreating` 먼저 호출 되어야, 재정의 하는 구성 다음 호출 해야 합니다. EF 코어에는 일반적으로 구성에 대 한 최신 하나 업데이트 정책을 있습니다. 예를 들어 경우는 `ToTable` 엔터티에 대 한 형식은 하나의 테이블 이름의 처음 호출 하 고 다른 테이블 이름을 사용할 경우 나중에 다시 다음 다음 두 번째 호출에서 테이블 이름이 사용 되는 것입니다.

### <a name="using-a-custom-user-type"></a>사용자 지정 사용자 형식을 사용 하 여

사용자 지정 사용자 유형을 사용 하는 형식을 만들고에서 상속 하 게 `IdentityUser`합니다. 이 형식의 이름을 지정 하는 일반적인은 `ApplicationUser`합니다. 이 형식은 기본 형식에 없는 추가 속성을 일반적으로, 그렇지 않으면 없습니다 것 값이 없는 만드는. 예를 들어:

```CSharp
public class ApplicationUser : IdentityUser
{
    public string CustomTag { get; set; }
}
```

다음이 형식을 사용 하 여 컨텍스트를 제네릭 인수로:

```CSharp
public class ApplicationDbContext : IdentityDbContext<ApplicationUser>
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
        : base(options)
    {
    }
}
```

업데이트 `ConfigureServices` 사용할 새 `ApplicationUser` 클래스:

```CSharp
services.AddDefaultIdentity<ApplicationUser>()
    .AddEntityFrameworkStores<ApplicationDbContext>();
```

재정의할 필요가 없습니다 `OnModelCreating` EF 코어 매핑됩니다 때문에 여기서는 `CustomTag` 규칙에 따라 속성입니다. 그러나 데이터베이스는 새 가져오려는 업데이트 해야 할 `CustomTag` 열입니다. 이 위해 마이그레이션, 추가 하 고 다음에 설명 된 대로 데이터베이스를 업데이트 [Id 및 EF 코어 마이그레이션](#identity-migrations)합니다.

### <a name="changing-the-key-type"></a>키 유형 변경

데이터베이스를 만든 후 기본 키 열 (PK)의 형식을 변경 하는 것은 많은 데이터베이스 시스템에 문제가 있습니다. 일반적으로 PK 변경를 삭제 하 고 다시 테이블을 만드는 작업이 포함 됩니다. 따라서 데이터베이스를 만들 때 대상 키 형식을 만드는 경우는 되도록 초기 마이그레이션에서는 키 형식을 지정할 수는 것이 좋습니다.

데이터베이스에 생성 된 경우 다음 `Drop-Database` (PMC) 또는 `dotnet ef database drop` (.NET 코어 CLI)를 사용 하 여 삭제할 수 있습니다.

데이터베이스가 존재 하지 않습니다 확인 되 면 제거 된 초기 마이그레이션 `Remove-Migration` (PMC) 또는 `dotnet ef migrations remove` .NET Core CLI ().

업데이트는 `ApplicationDbContext` 에 대 한 새 키 형식을 지정 하는 다른 기본 클래스를 사용 하도록 `TKey`합니다. 예를 들어, 사용 하는 `Guid` 키:

```CSharp
public class ApplicationDbContext : IdentityDbContext<IdentityUser<Guid>, IdentityRole<Guid>, Guid>
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
        : base(options)
    {
    }
}
```

제네릭 클래스 `IdentityUser<TKey>` 및 `IdentityRole<TKey>` 새 키 유형을 사용 하도록 지정 해야 합니다. `ConfigureServices` 일반 사용자를 사용 하도록 업데이트 해야 합니다.

```CSharp
services.AddDefaultIdentity<IdentityUser<Guid>>()
    .AddEntityFrameworkStores<ApplicationDbContext>();
```

사용자 지정 하는 경우 `ApplicationUser` 은에서 상속 하도록 업데이트 사용 중인 `IdentityUser<TKey>`합니다. 예를 들어:

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

### <a name="adding-navigation-properties"></a>탐색 속성 추가

관계에 대 한 모델 구성을 변경 하는 것은 기타 변경을 보다 더 어려울 수 있습니다. 기존 관계 교체가에 비해 새로운 추가 관계를 만들 주의 해야 합니다. 특히, 변경 된 관계는 기존 관계와 같은 외래 키 속성을 지정 해야 합니다. 예를 들어 간의 관계 `Users` 및 `UserClaims` 기본값이 지정 된 경우:

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

이 관계에 대 한 외래 키로 지정 되는 `UserClaim.UserId` 속성입니다. `HasMany` 및 `WithOne` 탐색 속성이 없는 관계를 만들 수는 인수 없이 호출 됩니다.

탐색 속성을 추가 `ApplicationUser` 연결 수 `UserClaims` 사용자에서 참조 되도록 합니다.

```CSharp
public class ApplicationUser : IdentityUser
{
    public virtual ICollection<IdentityUserClaim<string>> Claims { get; set; }
}
```

`TKey` 에 대 한 `IdentityUserClaim<TKey>` -이 경우 사용자의 기본 키에 대 한 지정 된 형식이 `string` 기본값 사용 하므로 합니다. **하지** 에 대 한 기본 키 유형을 `UserClaim` 엔터티 형식입니다.

구성에서 해야 탐색 속성이 있는 했으므로 `OnModelCreating`:

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

관계 된 대로 정확 하 게 하면 이전에 대 한 호출에 지정 된 탐색 속성에만 구성 되어 `HasMany`합니다.

탐색 속성에서 데이터베이스가 아니라 EF 모델에만 존재합니다. 외래 키 관계에 대 한 변경 되지 않았기 때문에 이러한 종류의 모델 변경 데이터베이스를 업데이트할 필요 하지 않습니다. 이 변경을 수행한 후 마이그레이션을 추가 하 여 확인할 수 있습니다:는 `Up` 및 `Down` 메서드는 비어 있습니다.

### <a name="adding-all-user-navigation-properties"></a>모든 사용자 탐색 속성 추가

여기 위의 섹션을 사용 하 여 지침으로,은 사용자에 모든 관계에 대 한 단방향 탐색 속성을 구성 하는 예입니다.

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

### <a name="adding-user-and-role-navigation-properties"></a>사용자 및 역할 탐색 속성 추가

위의 섹션을 사용 하 여 지침으로, 사용자 및 역할에서 모든 관계에 대 한 탐색 속성을 구성 하는 예제 다음은:

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

메모:

* 이 예제도 포함 되어는 `UserRole` 역할에 사용자의 다 대 다 관계를 탐색 하는 데 필요한 엔터티를 조인 합니다.
* 반영 하기 위해 탐색 속성의 형식을 변경 해야 `ApplicationXxx` 형식을 현재 사용 되 고 대신 `IdentityXxx` 형식입니다.
* 사용 해야는 `ApplicationXxx` 제네릭에서 `ApplicationContext` 정의 합니다.

### <a name="adding-all-navigation-properties"></a>모든 탐색 속성 추가

다음 위의 섹션을 사용 하 여 지침으로,은 모든 엔터티 형식에 대해 모든 관계에 대 한 탐색 속성을 구성 하는 예제입니다.

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

### <a name="using-composite-keys"></a>복합 키를 사용 하 여

앞의 섹션에서는 Id 모델에 사용 된 키 유형을 변경 하 나와 있습니다. 복합 키를 사용 하려면 Id 키 모델 변경은 지원 되지 않거나 것이 좋습니다. Identity manager 코드는 지원 되지 않는 사용자 지정 모델을 사용 하 고이 문서의 범위를 벗어나는 상호 작용 하는 방식 변경 Id를 가진 복합 키를 사용 하는 포함 됩니다.

### <a name="changing-tablecolumn-names-and-facets"></a>테이블/열 이름과 패싯을 변경

열과 테이블의 이름을 변경 하려면 호출 `base.OnModelCreating`, 다음 기본값을 재정의 하는 구성을 추가 합니다. 예를 들어, 모든 identity 테이블의 이름을 변경 하려면:

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

이 예제에서는 기본 Id 유형을 사용 하는 참고 합니다. 응용 프로그램 종류와 같은 사용 중인 경우 `ApplicationUser` 기본 형식 대신 해당 형식을 구성 합니다.

일부 열 이름을 변경 하는 예제는 다음과 같습니다.

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

특정으로 일부 유형의 데이터베이스 열을 구성할 수 있습니다 _패싯_ 허용 되는 최대 문자열 길이 등입니다. 모델에 여러 문자열 속성에 열 최대 길이 설정 하는 예제는 다음과 같습니다.

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

### <a name="mapping-to-a-different-schema"></a>다른 스키마에 매핑

스키마의 다른 데이터베이스 공급자에서에서 다르게 동작할 수 있습니다 하지만 SQL Server에 대 한 기본값 "dbo" 스키마의 모든 테이블을 만드는 것입니다. 대신 다른 스키마에 테이블을 만들기 위해이 변경할 수 있습니다. 예를 들어:

```CSharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    base.OnModelCreating(modelBuilder);

    modelBuilder.HasDefaultSchema("notdbo");
}
```

### <a name="lazy-loading"></a>지연 로드

이 섹션의 지연 로드 프록시 Id 모델에 대 한 지원이 추가 됩니다. Lazy 로드는 탐색 속성을 로드 되는 첫 번째 확인 하지 않고 사용할 수 있기 때문에 유용 합니다.

엔터티 형식을 만들 수 있습니다에 적합 한 여러 가지 방법으로 지연 로드에 설명 된 대로 [EF 핵심 설명서](/ef/core/querying/related-data#lazy-loading)합니다. 간단히 하기 위해 사용 합니다 지연 로드 프록시 해야 함:

* 설치는 [Microsoft.EntityFrameworkCore.Proxies](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Proxies/) 패키지 합니다.
* 에 대 한 호출 `.UseLazyLoadingProxies()` 내 `AddDbContext`합니다.
* 공용 가상 탐색 속성이 있는 public 엔터티 형식입니다.

호출의 예로 `.UseLazyLoadingProxies()`:

```CSharp
services
    .AddDbContext<ApplicationDbContext>(
        b => b.UseSqlServer(connectionString)
            .UseLazyLoadingProxies())
    .AddDefaultIdentity<ApplicationUser>()
    .AddEntityFrameworkStores<ApplicationDbContext>();
```

위 예제는 엔터티 형식에 탐색 속성을 추가 하기 위한 다시 참조 합니다.
