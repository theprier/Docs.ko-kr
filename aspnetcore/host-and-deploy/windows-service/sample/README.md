# <a name="custom-webhost-service-sample"></a>사용자 지정 웹 호스트 서비스 예제 추가 정보

이 예제는 Windows 서비스로 IIS를 사용 하지 않고 Windows에서 ASP.NET Core 응용 프로그램을 호스트 하는 권장된 방법은 보여 줍니다. 이 샘플에서 설명 하는 기능을 보여 줍니다. [Windows 서비스에서 ASP.NET Core 응용 프로그램 호스트](https://docs.microsoft.com/aspnet/core/host-and-deploy/windows-service)합니다.

## <a name="instructions"></a>지침

샘플 응용 프로그램의 지침에 따라 수정 된 간단한 MVC 웹 응용 프로그램은 [Windows 서비스에서 ASP.NET Core 응용 프로그램 호스트](https://docs.microsoft.com/aspnet/core/host-and-deploy/windows-service)합니다.

서비스 응용 프로그램을 실행 하려면 다음 단계를 수행 합니다.

1. 에서는 폴더를 만들 *c:\svc*합니다.

1. 사용 하 여 폴더에 앱을 게시 `dotnet publish --configuration Release --output c:\\svc`합니다. 명령을 포함 하 여 필요한 폴더에 응용 프로그램의 자산을 이동 합니다 `appsettings.json` 파일 및 `wwwroot` 폴더의 내용에 대해 합니다.

1. 열기는 **관리자** 명령 셸 합니다.

1. 다음 명령을 실행합니다.

   ```console
   sc create MyService binPath="c:\svc\aspnetcoreservice.exe"
   sc start MyService
   ```

1. 브라우저에서로 이동 `http://localhost:5000` 서비스가 실행 되 고 있는지 확인 합니다.

1. 서비스를 중지 하려면 명령을 사용 합니다.

   ```console
   sc stop MyService
   ```

오류 메시지에 액세스할 수 있도록 하는 빠른 방법을 같은 로깅 공급자를 추가 하는 응용 프로그램은 서비스에서 실행 하는 경우 예상 대로 최대 시작 되지 않으면는 [Windows 이벤트 로그 공급자](https://docs.microsoft.com/aspnet/core/fundamentals/logging/index#eventlog)합니다. 또 다른 옵션은 시스템에서 이벤트 뷰어를 사용 하 여 응용 프로그램 이벤트 로그를 확인 합니다. 예를 들어 다음은 FileNotFound 오류 응용 프로그램 이벤트 로그에 대 한 처리 되지 않은 예외가입니다.

```console
Application: AspNetCoreService.exe
Framework Version: v4.0.30319
Description: The process was terminated due to an unhandled exception.
Exception Info: System.IO.FileNotFoundException
   at Microsoft.Extensions.Configuration.FileConfigurationProvider.Load(Boolean)
   at Microsoft.Extensions.Configuration.ConfigurationRoot..ctor(System.Collections.Generic.IList`1<Microsoft.Extensions.Configuration.IConfigurationProvider>)
   at Microsoft.Extensions.Configuration.ConfigurationBuilder.Build()
   ...
```
