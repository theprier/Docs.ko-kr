Identity scaffolder를 실행 합니다.

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

* **솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 클릭 > **추가** > **스 캐 폴드 된 새 항목**합니다.
* 왼쪽된 창에서는 **추가 스 캐 폴드** 대화 상자에서 **Identity** > **추가**합니다.
* 에 **추가 Identity** 대화 상자에서 원하는 옵션을 선택 합니다.
  * 기존 레이아웃 페이지에서 선택 하거나 잘못 된 태그와 함께 레이아웃 파일을 덮어쓰게 됩니다. 기존 _Layout.cshtml 파일을 선택 하면 **하지** 덮어씁니다.

 예를 들어 `~/Pages/Shared/_Layout.cshtml` Razor 페이지에 대 한 `~/Views/Shared/_Layout.cshtml` MVC 프로젝트
* 기존 데이터 컨텍스트를 사용 하려면 재정의 하는 하나 이상의 파일을 선택 합니다. 데이터 컨텍스트를 추가 하려면 파일을 하나 이상 선택 해야 합니다.
  * 데이터 컨텍스트 클래스를 선택 합니다.
  * 선택 **추가**합니다.
* 에 새 사용자 컨텍스트를 만들고 Id에 대 한 사용자 지정 사용자 클래스를 만들어야 합니다.
  * 선택 된 **+** 단추를 새 **데이터 컨텍스트 클래스가**합니다.
  * 선택 **추가**합니다.

참고: 새 사용자 컨텍스트를 만드는 경우 재정의 하기 위한 파일을 선택할 필요가 없습니다.

# <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli)

ASP.NET scaffolder 이전에 설치 하지 않은 경우 지금 설치 합니다.

```cli
dotnet tool install -g dotnet-aspnet-codegenerator
```

에 대 한 패키지 참조 추가 [Microsoft.VisualStudio.Web.CodeGeneration.Design](https://www.nuget.org/packages/Microsoft.VisualStudio.Web.CodeGeneration.Design/) 프로젝트 (\*.csproj) 파일입니다. 프로젝트 디렉터리에서 다음 명령을 실행 합니다.

```cli
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet restore
```

Identity scaffolder 옵션을 나열 하려면 다음 명령을 실행 합니다.

```cli
dotnet aspnet-codegenerator identity -h
```

프로젝트 폴더에서 원하는 옵션으로 Identity scaffolder를 실행 합니다. 예를 들어 기본 UI 사용 하는 id 및 파일의 최소 수를 설정 하려면 다음 명령을 실행 합니다. DB 컨텍스트에 대 한 올바른 정규화 된 이름을 사용 합니다.

```cli
dotnet aspnet-codegenerator identity -dc MyWeb.Data.ApplicationDbContext --files Account.Register
```

-------------
