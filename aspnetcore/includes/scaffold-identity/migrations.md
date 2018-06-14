생성 된 Identity 데이터베이스 코드를 실행 하려면 [Entity Framework Core 마이그레이션](/ef/core/managing-schemas/migrations/)합니다. 마이그레이션 만들고 데이터베이스를 업데이트 합니다. 예를 들어 다음 명령을 실행 합니다.

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

Visual Studio에서 **패키지 관리자 콘솔**:

```PMC
Add-Migration CreateIdentitySchema
Update-Database
```

# <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli)

```cli
dotnet ef migrations add CreateIdentitySchema
dotnet ef database update
```

------

에 대 한 "CreateIdentitySchema" name 매개 변수는 `Add-Migration` 명령은 임의로 지정 됩니다. `"CreateIdentitySchema"` 마이그레이션하는 방법을 설명 합니다.