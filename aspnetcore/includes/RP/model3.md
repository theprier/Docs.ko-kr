<a name="cli"></a>
## <a name="add-scaffold-tooling-and-perform-initial-migration"></a><span data-ttu-id="a9e13-101">스캐폴드 도구 추가 및 초기 마이그레이션 수행</span><span class="sxs-lookup"><span data-stu-id="a9e13-101">Add scaffold tooling and perform initial migration</span></span>

<span data-ttu-id="a9e13-102">`</Project>` 태그를 닫기 직전에 *RazorPagesMovie.csproj* 파일에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a9e13-102">Add the following lines to the *RazorPagesMovie.csproj* file, just before the closing `</Project>` tag:</span></span>

```xml
<ItemGroup>
  <DotNetCliToolReference Include="Microsoft.VisualStudio.Web.CodeGeneration.Tools" Version="2.1.0-preview1-final"/>
</ItemGroup>
```  
<span data-ttu-id="a9e13-103">명령줄에서 다음 .NET Core CLI 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a9e13-103">From the command line, run the following .NET Core CLI commands:</span></span>

```console
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet restore
dotnet ef migrations add InitialCreate
dotnet ef database update
```

<span data-ttu-id="a9e13-104">`DotNetCliToolReference` 요소 및 `add package` 명령은 스캐폴딩 엔진을 실행하는 데 필요한 도구를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a9e13-104">The `DotNetCliToolReference` element and the `add package` command install the tooling required to run the scaffolding engine.</span></span>

<span data-ttu-id="a9e13-105">`ef migrations add InitialCreate` 명령은 초기 데이터베이스 스키마를 만드는 코드를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="a9e13-105">The `ef migrations add InitialCreate` command generates code to create the initial database schema.</span></span> <span data-ttu-id="a9e13-106">스키마는 `DbContext`에 지정된 모델을 기반으로 합니다(*Models/MovieContext.cs* 파일에서).</span><span class="sxs-lookup"><span data-stu-id="a9e13-106">The schema is based on the model specified in the `DbContext` (In the *Models/MovieContext.cs* file).</span></span> <span data-ttu-id="a9e13-107">`InitialCreate` 인수는 마이그레이션 이름을 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9e13-107">The `InitialCreate` argument is used to name the migrations.</span></span> <span data-ttu-id="a9e13-108">모든 이름을 사용할 수 있지만 일반적으로 마이그레이션을 설명하는 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a9e13-108">You can use any name, but by convention you choose a name that describes the migration.</span></span> <span data-ttu-id="a9e13-109">자세한 내용은 [마이그레이션 소개](xref:data/ef-mvc/migrations#introduction-to-migrations)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9e13-109">See [Introduction to migrations](xref:data/ef-mvc/migrations#introduction-to-migrations) for more information.</span></span>

<span data-ttu-id="a9e13-110">`ef database update` 명령은 데이터베이스를 만드는 *Migrations/\<time-stamp>_InitialCreate.cs* 파일에서 `Up` 메서드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a9e13-110">The `ef database update` command runs the `Up` method in the *Migrations/\<time-stamp>_InitialCreate.cs* file, which creates the database.</span></span>
