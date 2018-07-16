# <a name="custom-webhost-service-sample"></a><span data-ttu-id="a86e6-101">사용자 지정 WebHost 서비스 샘플</span><span class="sxs-lookup"><span data-stu-id="a86e6-101">Custom WebHost Service Sample</span></span>

<span data-ttu-id="a86e6-102">이 샘플에서는 IIS를 사용하지 않고 Windows 서비스로 ASP.NET Core 앱을 호스트하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="a86e6-102">This sample shows how to host an ASP.NET Core app as a Windows Service without using IIS.</span></span> <span data-ttu-id="a86e6-103">이 샘플에서는 [Windows 서비스에서 ASP.NET Core 앱 호스트](https://docs.microsoft.com/aspnet/core/host-and-deploy/windows-service)에 설명된 시나리오를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="a86e6-103">This sample demonstrates the scenario described in [Host an ASP.NET Core app in a Windows Service](https://docs.microsoft.com/aspnet/core/host-and-deploy/windows-service).</span></span>

## <a name="instructions"></a><span data-ttu-id="a86e6-104">지침</span><span class="sxs-lookup"><span data-stu-id="a86e6-104">Instructions</span></span>

<span data-ttu-id="a86e6-105">샘플 앱은 [Windows 서비스에서 ASP.NET Core 앱 호스트](https://docs.microsoft.com/aspnet/core/host-and-deploy/windows-service)의 지침에 따라 수정된 Razor Pages 웹앱입니다.</span><span class="sxs-lookup"><span data-stu-id="a86e6-105">The sample app is a Razor Pages web app modified according to the instructions in [Host an ASP.NET Core app in a Windows Service](https://docs.microsoft.com/aspnet/core/host-and-deploy/windows-service).</span></span>

<span data-ttu-id="a86e6-106">서비스에서 앱을 실행하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a86e6-106">To run the app in a service, perform the following steps:</span></span>

1. <span data-ttu-id="a86e6-107">*c:\svc*에 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a86e6-107">Create a folder at *c:\svc*.</span></span>

1. <span data-ttu-id="a86e6-108">`dotnet publish --configuration Release --output c:\\svc`를 사용하여 앱을 폴더에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="a86e6-108">Publish the app to the folder with `dotnet publish --configuration Release --output c:\\svc`.</span></span> <span data-ttu-id="a86e6-109">이 명령은 필수 `appsettings.json` 파일 및 `wwwroot` 폴더를 비롯한 앱의 자산을 *svc* 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a86e6-109">The command moves the app's assets to the *svc* folder, including the required `appsettings.json` file and the `wwwroot` folder.</span></span>

1. <span data-ttu-id="a86e6-110">**관리자** 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a86e6-110">Open an **administrator** command prompt.</span></span>

1. <span data-ttu-id="a86e6-111">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a86e6-111">Execute the following commands:</span></span>

   ```console
   sc create MyService binPath= "c:\svc\aspnetcoreservice.exe"
   sc start MyService
   ```

  <span data-ttu-id="a86e6-112">*등호와 경로 문자열의 시작 사이에 공간이 필요합니다.*</span><span class="sxs-lookup"><span data-stu-id="a86e6-112">*The space between the equal sign and the start of the path string is required.*</span></span>

1. <span data-ttu-id="a86e6-113">브라우저에서 `http://localhost:5000`으로 이동하여 서비스가 실행 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a86e6-113">In a browser, navigate to `http://localhost:5000` and verify that the service is running.</span></span> <span data-ttu-id="a86e6-114">앱은 보안 엔드포인트 `https://localhost:5001`로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="a86e6-114">The app redirects to the secure endpoint `https://localhost:5001`.</span></span>

1. <span data-ttu-id="a86e6-115">서비스를 중지하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a86e6-115">To stop the service, use the command:</span></span>

   ```console
   sc stop MyService
   ```

<span data-ttu-id="a86e6-116">앱이 예상대로 시작되지 않는 경우 액세스 가능한 오류 메시지를 빠르게 만드는 방법은 [Windows EventLog 공급자](https://docs.microsoft.com/aspnet/core/fundamentals/logging/index#eventlog)와 같은 로깅 공급자를 추가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a86e6-116">If the app doesn't start as expected, a quick way to make error messages accessible is to add a logging provider, such as the [Windows EventLog provider](https://docs.microsoft.com/aspnet/core/fundamentals/logging/index#eventlog).</span></span> <span data-ttu-id="a86e6-117">다른 옵션은 시스템에서 이벤트 뷰어를 사용하여 응용 프로그램 이벤트 로그를 확인하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a86e6-117">Another option is to check the Application Event Log using the Event Viewer on the system.</span></span> <span data-ttu-id="a86e6-118">예를 들면 응용 프로그램 이벤트 로그의 FileNotFound 오류에 대해 처리되지 않은 예외가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a86e6-118">For example, here's an unhandled exception for a FileNotFound error in the Application Event Log:</span></span>

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
