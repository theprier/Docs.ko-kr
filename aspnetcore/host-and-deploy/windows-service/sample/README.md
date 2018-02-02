# <a name="custom-webhost-service-sample"></a><span data-ttu-id="47f29-101">사용자 지정 웹 호스트 서비스 예제 추가 정보</span><span class="sxs-lookup"><span data-stu-id="47f29-101">Custom WebHost Service Sample</span></span>

<span data-ttu-id="47f29-102">이 예제는 Windows 서비스로 IIS를 사용 하지 않고 Windows에서 ASP.NET Core 응용 프로그램을 호스트 하는 권장된 방법은 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="47f29-102">This sample shows the recommended way to host an ASP.NET Core app on Windows without using IIS as a Windows Service.</span></span> <span data-ttu-id="47f29-103">이 샘플에서 설명 하는 기능을 보여 줍니다. [Windows 서비스에서 ASP.NET Core 응용 프로그램 호스트](https://docs.microsoft.com/aspnet/core/host-and-deploy/windows-service)합니다.</span><span class="sxs-lookup"><span data-stu-id="47f29-103">This sample demonstrates the features described in [Host an ASP.NET Core app in a Windows Service](https://docs.microsoft.com/aspnet/core/host-and-deploy/windows-service).</span></span>

## <a name="instructions"></a><span data-ttu-id="47f29-104">지침</span><span class="sxs-lookup"><span data-stu-id="47f29-104">Instructions</span></span>

<span data-ttu-id="47f29-105">샘플 응용 프로그램의 지침에 따라 수정 된 간단한 MVC 웹 응용 프로그램은 [Windows 서비스에서 ASP.NET Core 응용 프로그램 호스트](https://docs.microsoft.com/aspnet/core/host-and-deploy/windows-service)합니다.</span><span class="sxs-lookup"><span data-stu-id="47f29-105">The sample app is a simple MVC web app modified according to the instructions in [Host an ASP.NET Core app in a Windows Service](https://docs.microsoft.com/aspnet/core/host-and-deploy/windows-service).</span></span>

<span data-ttu-id="47f29-106">서비스 응용 프로그램을 실행 하려면 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="47f29-106">To run the app in a service, perform the following steps:</span></span>

1. <span data-ttu-id="47f29-107">에서는 폴더를 만들 *c:\svc*합니다.</span><span class="sxs-lookup"><span data-stu-id="47f29-107">Create a folder at *c:\svc*.</span></span>

1. <span data-ttu-id="47f29-108">사용 하 여 폴더에 앱을 게시 `dotnet publish --configuration Release --output c:\\svc`합니다.</span><span class="sxs-lookup"><span data-stu-id="47f29-108">Publish the app to the folder with `dotnet publish --configuration Release --output c:\\svc`.</span></span> <span data-ttu-id="47f29-109">명령을 포함 하 여 필요한 폴더에 응용 프로그램의 자산을 이동 합니다 `appsettings.json` 파일 및 `wwwroot` 폴더의 내용에 대해 합니다.</span><span class="sxs-lookup"><span data-stu-id="47f29-109">The command will move the app's assets to the folder, including the required `appsettings.json` file and the `wwwroot` folder with its contents.</span></span>

1. <span data-ttu-id="47f29-110">열기는 **관리자** 명령 셸 합니다.</span><span class="sxs-lookup"><span data-stu-id="47f29-110">Open an **administrator** command shell.</span></span>

1. <span data-ttu-id="47f29-111">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="47f29-111">Execute the following commands:</span></span>

   ```console
   sc create MyService binPath="c:\svc\aspnetcoreservice.exe"
   sc start MyService
   ```

1. <span data-ttu-id="47f29-112">브라우저에서로 이동 `http://localhost:5000` 서비스가 실행 되 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="47f29-112">In a browser, go to `http://localhost:5000` to verify that the service is running.</span></span>

1. <span data-ttu-id="47f29-113">서비스를 중지 하려면 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="47f29-113">To stop the service, use the command:</span></span>

   ```console
   sc stop MyService
   ```

<span data-ttu-id="47f29-114">오류 메시지에 액세스할 수 있도록 하는 빠른 방법을 같은 로깅 공급자를 추가 하는 응용 프로그램은 서비스에서 실행 하는 경우 예상 대로 최대 시작 되지 않으면는 [Windows 이벤트 로그 공급자](https://docs.microsoft.com/aspnet/core/fundamentals/logging/index#eventlog)합니다.</span><span class="sxs-lookup"><span data-stu-id="47f29-114">If the app doesn't start up as expected when running in a service, a quick way to make error messages accessible is to add a logging provider, such as the [Windows EventLog provider](https://docs.microsoft.com/aspnet/core/fundamentals/logging/index#eventlog).</span></span> <span data-ttu-id="47f29-115">또 다른 옵션은 시스템에서 이벤트 뷰어를 사용 하 여 응용 프로그램 이벤트 로그를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="47f29-115">Another option is to check the Application Event Log using the Event Viewer on the system.</span></span> <span data-ttu-id="47f29-116">예를 들어 다음은 FileNotFound 오류 응용 프로그램 이벤트 로그에 대 한 처리 되지 않은 예외가입니다.</span><span class="sxs-lookup"><span data-stu-id="47f29-116">For example, here's an unhandled exception for a FileNotFound error in the Application Event Log:</span></span>

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
