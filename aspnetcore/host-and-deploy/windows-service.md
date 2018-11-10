---
title: Windows 서비스에서 ASP.NET Core 호스트
author: guardrex
description: Windows 서비스에서 ASP.NET Core 앱을 호스트하는 방법을 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 10/30/2018
uid: host-and-deploy/windows-service
ms.openlocfilehash: 11913019bfe5d06c259b806fce9cc580a8280ad5
ms.sourcegitcommit: fc2486ddbeb15ab4969168d99b3fe0fbe91e8661
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/01/2018
ms.locfileid: "50758195"
---
# <a name="host-aspnet-core-in-a-windows-service"></a><span data-ttu-id="6bbd8-103">Windows 서비스에서 ASP.NET Core 호스트</span><span class="sxs-lookup"><span data-stu-id="6bbd8-103">Host ASP.NET Core in a Windows Service</span></span>

<span data-ttu-id="6bbd8-104">작성자: [Luke Latham](https://github.com/guardrex) 및 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="6bbd8-104">By [Luke Latham](https://github.com/guardrex) and [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="6bbd8-105">IIS를 [Windows 서비스](/dotnet/framework/windows-services/introduction-to-windows-service-applications)로 사용하지 않고 Windows에서 ASP.NET Core 앱을 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-105">An ASP.NET Core app can be hosted on Windows without using IIS as a [Windows Service](/dotnet/framework/windows-services/introduction-to-windows-service-applications).</span></span> <span data-ttu-id="6bbd8-106">Windows Service로 호스팅되는 앱은 재부팅 후 자동으로 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-106">When hosted as a Windows Service, the app automatically starts after reboots.</span></span>

<span data-ttu-id="6bbd8-107">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/samples)([다운로드 방법](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="6bbd8-107">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/samples) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="convert-a-project-into-a-windows-service"></a><span data-ttu-id="6bbd8-108">프로젝트를 Windows 서비스로 변환</span><span class="sxs-lookup"><span data-stu-id="6bbd8-108">Convert a project into a Windows Service</span></span>

<span data-ttu-id="6bbd8-109">기존 ASP.NET Core 프로젝트를 서비스로 실행되도록 설정하려면 다음과 같은 최소 변경 작업이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-109">The following minimum changes are required to set up an existing ASP.NET Core project to run as a service:</span></span>

1. <span data-ttu-id="6bbd8-110">프로젝트 파일에서:</span><span class="sxs-lookup"><span data-stu-id="6bbd8-110">In the project file:</span></span>

   * <span data-ttu-id="6bbd8-111">Windows [RID(런타임 식별자)](/dotnet/core/rid-catalog)가 있는지 확인하거나, 대상 프레임워크가 포함된 `<PropertyGroup>`에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-111">Confirm the presence of a Windows [Runtime Identifier (RID)](/dotnet/core/rid-catalog) or add it to the `<PropertyGroup>` that contains the target framework:</span></span>

      ```xml
      <PropertyGroup>
        <TargetFramework>netcoreapp2.2</TargetFramework>
        <RuntimeIdentifier>win7-x64</RuntimeIdentifier>
      </PropertyGroup>
      ```

      <span data-ttu-id="6bbd8-112">여러 개의 RID를 게시하려면</span><span class="sxs-lookup"><span data-stu-id="6bbd8-112">To publish for multiple RIDs:</span></span>

      * <span data-ttu-id="6bbd8-113">세미콜론으로 구분된 목록으로 RID를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-113">Provide the RIDs in a semicolon-delimited list.</span></span>
      * <span data-ttu-id="6bbd8-114">속성 이름 `<RuntimeIdentifiers>`(복수)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-114">Use the property name `<RuntimeIdentifiers>` (plural).</span></span>

      <span data-ttu-id="6bbd8-115">자세한 내용은 [.NET Core RID 카탈로그](/dotnet/core/rid-catalog)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-115">For more information, see [.NET Core RID Catalog](/dotnet/core/rid-catalog).</span></span>

   * <span data-ttu-id="6bbd8-116">[Microsoft.AspNetCore.Hosting.WindowsServices](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.WindowsServices)에 패키지 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-116">Add a package reference for [Microsoft.AspNetCore.Hosting.WindowsServices](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.WindowsServices).</span></span>

1. <span data-ttu-id="6bbd8-117">`Program.Main`에서 다음과 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-117">Make the following changes in `Program.Main`:</span></span>

   * <span data-ttu-id="6bbd8-118">`host.Run` 대신 [host.RunAsService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostwindowsserviceextensions.runasservice)를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-118">Call [host.RunAsService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostwindowsserviceextensions.runasservice) instead of `host.Run`.</span></span>

   * <span data-ttu-id="6bbd8-119">[UseContentRoot](xref:fundamentals/host/web-host#content-root)를 호출하여 `Directory.GetCurrentDirectory()` 대신 앱의 게시 위치에 대한 경로를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-119">Call [UseContentRoot](xref:fundamentals/host/web-host#content-root) and use a path to the app's published location instead of `Directory.GetCurrentDirectory()`.</span></span>

     [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/Program.cs?name=ServiceOnly&highlight=8-9,16)]

1. <span data-ttu-id="6bbd8-120">[dotnet publish](/dotnet/articles/core/tools/dotnet-publish), [Visual Studio 게시 프로필](xref:host-and-deploy/visual-studio-publish-profiles) 또는 Visual Studio Code를 사용하여 앱을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-120">Publish the app using [dotnet publish](/dotnet/articles/core/tools/dotnet-publish), a [Visual Studio publish profile](xref:host-and-deploy/visual-studio-publish-profiles), or Visual Studio Code.</span></span> <span data-ttu-id="6bbd8-121">Visual Studio를 사용하는 경우 **FolderProfile**을 선택하고 **대상 위치**를 구성한 후 **게시** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-121">When using Visual Studio, select the **FolderProfile** and configure the **Target Location** before selecting the **Publish** button.</span></span>

   <span data-ttu-id="6bbd8-122">CLI(명령줄 인터페이스) 도구를 사용하여 샘플 앱을 게시하려면 프로젝트 폴더의 명령 프롬프트에서 [dotnet publish](/dotnet/core/tools/dotnet-publish) 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-122">To publish the sample app using command-line interface (CLI) tools, run the [dotnet publish](/dotnet/core/tools/dotnet-publish) command at a command prompt from the project folder.</span></span> <span data-ttu-id="6bbd8-123">프로젝트 파일의 `<RuntimeIdenfifier>`(또는 `<RuntimeIdentifiers>`) 속성에 RID를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-123">The RID must be specified in the `<RuntimeIdenfifier>` (or `<RuntimeIdentifiers>`) property of the project file.</span></span> <span data-ttu-id="6bbd8-124">다음 예제에서는 앱이 `win7-x64` 런타임에 대한 릴리스 구성에서 *c:\\svc*에 생성된 폴더에 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-124">In the following example, the app is published in Release configuration for the `win7-x64` runtime to a folder created at *c:\\svc*:</span></span>

   ```console
   dotnet publish --configuration Release --runtime win7-x64 --output c:\svc
   ```

1. <span data-ttu-id="6bbd8-125">`net user` 명령을 사용하여 서비스에 대한 사용자 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-125">Create a user account for the service using the `net user` command:</span></span>

   ```console
   net user {USER ACCOUNT} {PASSWORD} /add
   ```

   <span data-ttu-id="6bbd8-126">샘플 앱의 경우, 이름이 `ServiceUser`인 사용자 계정과 암호를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-126">For the sample app, create a user account with the name `ServiceUser` and a password.</span></span> <span data-ttu-id="6bbd8-127">다음 명령에서 `{PASSWORD}`를 [강력한 암호](/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements)로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-127">In the following command, replace `{PASSWORD}` with a [strong password](/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements).</span></span>

   ```console
   net user ServiceUser {PASSWORD} /add
   ```

   <span data-ttu-id="6bbd8-128">그룹에 사용자를 추가해야 하는 경우 `net localgroup` 명령을 사용합니다. 여기서 `{GROUP}`은 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-128">If you need to add the user to a group, use the `net localgroup` command, where `{GROUP}` is the name of the group:</span></span>

   ```console
   net localgroup {GROUP} {USER ACCOUNT} /add
   ```

   <span data-ttu-id="6bbd8-129">자세한 내용은 [서비스 사용자 계정](/windows/desktop/services/service-user-accounts)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-129">For more information, see [Service User Accounts](/windows/desktop/services/service-user-accounts).</span></span>

1. <span data-ttu-id="6bbd8-130">[icacls](/windows-server/administration/windows-commands/icacls) 명령을 사용하여 앱의 폴더에 쓰기/읽기/실행 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-130">Grant write/read/execute access to the app's folder using the [icacls](/windows-server/administration/windows-commands/icacls) command:</span></span>

   ```console
   icacls "{PATH}" /grant {USER ACCOUNT}:(OI)(CI){PERMISSION FLAGS} /t
   ```

   * <span data-ttu-id="6bbd8-131">`{PATH}` &ndash; 앱의 폴더에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-131">`{PATH}` &ndash; Path to the app's folder.</span></span>
   * <span data-ttu-id="6bbd8-132">`{USER ACCOUNT}` &ndash; 사용자 계정(SID)입니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-132">`{USER ACCOUNT}` &ndash; The user account (SID).</span></span>
   * <span data-ttu-id="6bbd8-133">`(OI)` &ndash; 개체 상속 플래그는 권한을 하위 파일에 전파합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-133">`(OI)` &ndash; The Object Inherit flag propagates permissions to subordinate files.</span></span>
   * <span data-ttu-id="6bbd8-134">`(CI)` &ndash; 컨테이너 상속 플래그는 권한을 하위 폴더에 전파합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-134">`(CI)` &ndash; The Container Inherit flag propagates permissions to subordinate folders.</span></span>
   * <span data-ttu-id="6bbd8-135">`{PERMISSION FLAGS}` &ndash; 앱의 액세스 권한을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-135">`{PERMISSION FLAGS}` &ndash; Sets the app's access permissions.</span></span>
     * <span data-ttu-id="6bbd8-136">쓰기(`W`)</span><span class="sxs-lookup"><span data-stu-id="6bbd8-136">Write (`W`)</span></span>
     * <span data-ttu-id="6bbd8-137">읽기(`R`)</span><span class="sxs-lookup"><span data-stu-id="6bbd8-137">Read (`R`)</span></span>
     * <span data-ttu-id="6bbd8-138">실행(`X`)</span><span class="sxs-lookup"><span data-stu-id="6bbd8-138">Execute (`X`)</span></span>
     * <span data-ttu-id="6bbd8-139">전체(`F`)</span><span class="sxs-lookup"><span data-stu-id="6bbd8-139">Full (`F`)</span></span>
     * <span data-ttu-id="6bbd8-140">수정(`M`)</span><span class="sxs-lookup"><span data-stu-id="6bbd8-140">Modify (`M`)</span></span>
   * <span data-ttu-id="6bbd8-141">`/t` &ndash; 기존 하위 폴더 및 파일에 재귀적으로 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-141">`/t` &ndash; Apply recursively to existing subordinate folders and files.</span></span>

   <span data-ttu-id="6bbd8-142">*c:\\svc* 폴더에 게시된 샘플 앱과 쓰기/읽기/실행 권한이 있는 `ServiceUser` 계정의 경우 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-142">For the sample app published to the *c:\\svc* folder and the `ServiceUser` account with write/read/execute permissions, use the following command:</span></span>

   ```console
   icacls "c:\svc" /grant ServiceUser:(OI)(CI)WRX /t
   ```

   <span data-ttu-id="6bbd8-143">자세한 내용은 [icacls](/windows-server/administration/windows-commands/icacls)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-143">For more information, see [icacls](/windows-server/administration/windows-commands/icacls).</span></span>

1. <span data-ttu-id="6bbd8-144">[sc.exe](https://technet.microsoft.com/library/bb490995) 명령줄 도구를 사용하여 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-144">Use the [sc.exe](https://technet.microsoft.com/library/bb490995) command-line tool to create the service.</span></span> <span data-ttu-id="6bbd8-145">`binPath` 값은 실행 파일 이름을 포함하는 앱의 실행 파일 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-145">The `binPath` value is the path to the app's executable, which includes the executable file name.</span></span> <span data-ttu-id="6bbd8-146">**각 매개 변수의 등호 및 인용 문자 값 사이에 공백이 필요합니다.**</span><span class="sxs-lookup"><span data-stu-id="6bbd8-146">**The space between the equal sign and the quote character of each parameter and value is required.**</span></span>

   ```console
   sc create {SERVICE NAME} binPath= "{PATH}" obj= "{DOMAIN}\{USER ACCOUNT}" password= "{PASSWORD}"
   ```

   * <span data-ttu-id="6bbd8-147">`{SERVICE NAME}` &ndash; [서비스 제어 관리자](/windows/desktop/services/service-control-manager)의 서비스에 할당하는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-147">`{SERVICE NAME}` &ndash; The name to assign to the service in [Service Control Manager](/windows/desktop/services/service-control-manager).</span></span>
   * <span data-ttu-id="6bbd8-148">`{PATH}` &ndash; 서비스 실행 파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-148">`{PATH}` &ndash; The path to the service executable.</span></span>
   * <span data-ttu-id="6bbd8-149">`{DOMAIN}` (또는 머신이 도메인에 가입되어 있지 않은 경우 로컬 머신 이름) 및 `{USER ACCOUNT}` &ndash; 서비스가 실행되는 도메인(또는 로컬 머신 이름) 및 사용자 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-149">`{DOMAIN}` (or if the machine isn't domain joined, the local machine name) and `{USER ACCOUNT}` &ndash; The domain (or local machine name) and user account under which the service runs.</span></span> <span data-ttu-id="6bbd8-150">`obj` 매개 변수를 생략하지 **마세요**.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-150">Do **not** omit the `obj` parameter.</span></span> <span data-ttu-id="6bbd8-151">`obj`의 기본값은 [LocalSystem 계정](/windows/desktop/services/localsystem-account) 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-151">The default value for `obj` is the [LocalSystem account](/windows/desktop/services/localsystem-account) account.</span></span> <span data-ttu-id="6bbd8-152">`LocalSystem` 계정으로 서비스를 실행하면 상당한 보안 위험이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-152">Running a service under the `LocalSystem` account presents a significant security risk.</span></span> <span data-ttu-id="6bbd8-153">항상 서버에서 제한된 권한을 가진 사용자 계정으로 서비스를 실행하세요.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-153">Always run a service under a user account with restricted privileges on the server.</span></span>
   * <span data-ttu-id="6bbd8-154">`{PASSWORD}` &ndash; 사용자 계정 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-154">`{PASSWORD}` &ndash; The user account password.</span></span>

   <span data-ttu-id="6bbd8-155">다음 예제에서는</span><span class="sxs-lookup"><span data-stu-id="6bbd8-155">In the following example:</span></span>

   * <span data-ttu-id="6bbd8-156">서비스의 이름은 **MyService**입니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-156">The service is named **MyService**.</span></span>
   * <span data-ttu-id="6bbd8-157">게시된 서비스는 *c:\\svc* 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-157">The published service resides in the *c:\\svc* folder.</span></span> <span data-ttu-id="6bbd8-158">앱 실행 파일의 이름은 *AspNetCoreService.exe*입니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-158">The app executable is named *AspNetCoreService.exe*.</span></span> <span data-ttu-id="6bbd8-159">`binPath` 값은 곧은 따옴표(")로 묶입니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-159">The `binPath` value is enclosed in straight quotation marks (").</span></span>
   * <span data-ttu-id="6bbd8-160">서비스는 `ServiceUser` 계정으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-160">The service runs under the `ServiceUser` account.</span></span> <span data-ttu-id="6bbd8-161">`{DOMAIN}`을 사용자 계정의 도메인 또는 로컬 머신 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-161">Replace `{DOMAIN}` with the user account's domain or local machine name.</span></span> <span data-ttu-id="6bbd8-162">`obj` 값을 곧은 따옴표(")로 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-162">Enclose the `obj` value in straight quotation marks (").</span></span> <span data-ttu-id="6bbd8-163">예: 호스팅 시스템이 이름이 `MairaPC`인 로컬 머신인 경우 `obj`를 `"MairaPC\ServiceUser"`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-163">Example: If the hosting system is a local machine named `MairaPC`, set `obj` to `"MairaPC\ServiceUser"`.</span></span>
   * <span data-ttu-id="6bbd8-164">`{PASSWORD}`를 사용자 계정의 암호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-164">Replace `{PASSWORD}` with the user account's password.</span></span> <span data-ttu-id="6bbd8-165">`password` 값은 곧은 따옴표(")로 묶입니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-165">The `password` value is enclosed in straight quotation marks (").</span></span>

   ```console
   sc create MyService binPath= "c:\svc\aspnetcoreservice.exe" obj= "{DOMAIN}\ServiceUser" password= "{PASSWORD}"
   ```

   > [!IMPORTANT]
   > <span data-ttu-id="6bbd8-166">매개 변수의 등호와 매개 변수의 값 사이에 공백이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-166">Make sure that the spaces between the parameters' equal signs and the parameters' values are present.</span></span>

1. <span data-ttu-id="6bbd8-167">`sc start {SERVICE NAME}` 명령을 사용하여 서비스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-167">Start the service with the `sc start {SERVICE NAME}` command.</span></span>

   <span data-ttu-id="6bbd8-168">샘플 앱 서비스를 시작하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-168">To start the sample app service, use the following command:</span></span>

   ```console
   sc start MyService
   ```

   <span data-ttu-id="6bbd8-169">명령은 서비스를 시작하는 데 몇 초 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-169">The command takes a few seconds to start the service.</span></span>

1. <span data-ttu-id="6bbd8-170">서비스 상태를 확인하려면 `sc query {SERVICE NAME}` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-170">To check the status of the service, use the `sc query {SERVICE NAME}` command.</span></span> <span data-ttu-id="6bbd8-171">상태는 다음 값 중 하나로 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-171">The status is reported as one of the following values:</span></span>

   * `START_PENDING`
   * `RUNNING`
   * `STOP_PENDING`
   * `STOPPED`

   <span data-ttu-id="6bbd8-172">다음 명령을 사용하여 샘플 앱 서비스의 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-172">Use the following command to check the status of the sample app service:</span></span>

   ```console
   sc query MyService
   ```

1. <span data-ttu-id="6bbd8-173">이 서비스가 `RUNNING` 상태이며 서비스가 웹앱인 경우 해당 경로에서 앱을 찾습니다(기본적으로 `http://localhost:5000`이며 [HTTPS 리디렉션 미들웨어](xref:security/enforcing-ssl)를 사용하는 경우 `https://localhost:5001`로 리디렉션함).</span><span class="sxs-lookup"><span data-stu-id="6bbd8-173">When the service is in the `RUNNING` state and if the service is a web app, browse the app at its path (by default, `http://localhost:5000`, which redirects to `https://localhost:5001` when using [HTTPS Redirection Middleware](xref:security/enforcing-ssl)).</span></span>

   <span data-ttu-id="6bbd8-174">샘플 앱 서비스의 경우 `http://localhost:5000`에서 앱을 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-174">For the sample app service, browse the app at `http://localhost:5000`.</span></span>

1. <span data-ttu-id="6bbd8-175">`sc stop {SERVICE NAME}` 명령을 사용하여 서비스를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-175">Stop the service with the `sc stop {SERVICE NAME}` command.</span></span>

   <span data-ttu-id="6bbd8-176">다음 명령은 샘플 앱 서비스를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-176">The following command stops the sample app service:</span></span>

   ```console
   sc stop MyService
   ```

1. <span data-ttu-id="6bbd8-177">서비스를 중지하는 짧은 지연 후에 `sc delete {SERVICE NAME}` 명령을 사용하여 서비스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-177">After a short delay to stop a service, uninstall the service with the `sc delete {SERVICE NAME}` command.</span></span>

   <span data-ttu-id="6bbd8-178">샘플 앱 서비스의 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-178">Check the status of the sample app service:</span></span>

   ```console
   sc query MyService
   ```

   <span data-ttu-id="6bbd8-179">이 샘플 앱 서비스가 `STOPPED` 상태인 경우 다음 명령을 사용하여 샘플 앱 서비스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-179">When the sample app service is in the `STOPPED` state, use the following command to uninstall the sample app service:</span></span>

   ```console
   sc delete MyService
   ```

## <a name="run-the-app-outside-of-a-service"></a><span data-ttu-id="6bbd8-180">서비스 외부에서 앱 실행</span><span class="sxs-lookup"><span data-stu-id="6bbd8-180">Run the app outside of a service</span></span>

<span data-ttu-id="6bbd8-181">서비스 외부에서 실행하면 테스트하고 디버그하기가 더 쉬우므로 특정 조건에서만 `RunAsService`를 호출하는 코드를 추가하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-181">It's easier to test and debug when running outside of a service, so it's customary to add code that calls `RunAsService` only under certain conditions.</span></span> <span data-ttu-id="6bbd8-182">예를 들어 `--console` 명령줄 인수를 사용하거나 디버거가 연결된 경우 앱을 콘솔 앱으로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-182">For example, the app can run as a console app with a `--console` command-line argument or if the debugger is attached:</span></span>

[!code-csharp[](windows-service/samples/2.x/AspNetCoreService/Program.cs?name=ServiceOrConsole)]

<span data-ttu-id="6bbd8-183">ASP.NET Core 구성에 명령줄 인수에 대한 이름 값 쌍이 필요하기 때문에 인수가 [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder)에 전달되기 전에 `--console` 스위치를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-183">Because ASP.NET Core configuration requires name-value pairs for command-line arguments, the `--console` switch is removed before the arguments are passed to [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder).</span></span>

> [!NOTE]
> <span data-ttu-id="6bbd8-184">[통합 테스트](xref:test/integration-tests)가 제대로 작동하려면 `CreateWebHostBuilder`의 서명이 `CreateWebHostBuilder(string[])`이어야 하므로 `isService`는 `Main`에서 `CreateWebHostBuilder`로 전달되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-184">`isService` isn't passed from `Main` into `CreateWebHostBuilder` because the signature of `CreateWebHostBuilder` must be `CreateWebHostBuilder(string[])` in order for [integration testing](xref:test/integration-tests) to work properly.</span></span>

## <a name="handle-stopping-and-starting-events"></a><span data-ttu-id="6bbd8-185">이벤트 중지 및 시작 처리</span><span class="sxs-lookup"><span data-stu-id="6bbd8-185">Handle stopping and starting events</span></span>

<span data-ttu-id="6bbd8-186">[OnStarting](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstarting), [OnStarted](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstarted) 및 [OnStopping](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstopping) 이벤트를 처리하려면 다음과 같이 추가로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-186">To handle [OnStarting](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstarting), [OnStarted](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstarted), and [OnStopping](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstopping) events, make the following additional changes:</span></span>

1. <span data-ttu-id="6bbd8-187">[WebHostService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice)에서 파생되는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-187">Create a class that derives from [WebHostService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice):</span></span>

   [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/CustomWebHostService.cs?name=NoLogging)]

2. <span data-ttu-id="6bbd8-188">사용자 지정 `WebHostService`를 [ServiceBase.Run](/dotnet/api/system.serviceprocess.servicebase.run)에 전달하는 [IWebHost](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost)에 대한 확장 메서드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-188">Create an extension method for [IWebHost](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost) that passes the custom `WebHostService` to [ServiceBase.Run](/dotnet/api/system.serviceprocess.servicebase.run):</span></span>

   [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/WebHostServiceExtensions.cs?name=ExtensionsClass)]

3. <span data-ttu-id="6bbd8-189">`Program.Main`에서 [RunAsService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostwindowsserviceextensions.runasservice) 대신 새 확장 메서드(`RunAsCustomService`)를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-189">In `Program.Main`, call the new extension method, `RunAsCustomService`, instead of [RunAsService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostwindowsserviceextensions.runasservice):</span></span>

   [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/Program.cs?name=HandleStopStart&highlight=17)]

   > [!NOTE]
   > <span data-ttu-id="6bbd8-190">[통합 테스트](xref:test/integration-tests)가 제대로 작동하려면 `CreateWebHostBuilder`의 서명이 `CreateWebHostBuilder(string[])`이어야 하므로 `isService`는 `Main`에서 `CreateWebHostBuilder`로 전달되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-190">`isService` isn't passed from `Main` into `CreateWebHostBuilder` because the signature of `CreateWebHostBuilder` must be `CreateWebHostBuilder(string[])` in order for [integration testing](xref:test/integration-tests) to work properly.</span></span>

<span data-ttu-id="6bbd8-191">사용자 지정 `WebHostService` 코드에 종속성 주입의 서비스(예: 로거)가 필요한 경우 [IWebHost.Services](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost.services) 속성에서 서비스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-191">If the custom `WebHostService` code requires a service from dependency injection (such as a logger), obtain it from the [IWebHost.Services](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost.services) property:</span></span>

[!code-csharp[](windows-service/samples/2.x/AspNetCoreService/CustomWebHostService.cs?name=Logging&highlight=7-8)]

## <a name="proxy-server-and-load-balancer-scenarios"></a><span data-ttu-id="6bbd8-192">프록시 서버 및 부하 분산 장치 시나리오</span><span class="sxs-lookup"><span data-stu-id="6bbd8-192">Proxy server and load balancer scenarios</span></span>

<span data-ttu-id="6bbd8-193">인터넷 또는 회사 네트워크의 요청과 상호 작용하고 프록시 또는 부하 분산 장치 뒤에 있는 서비스에는 추가 구성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-193">Services that interact with requests from the Internet or a corporate network and are behind a proxy or load balancer might require additional configuration.</span></span> <span data-ttu-id="6bbd8-194">자세한 내용은 <xref:host-and-deploy/proxy-load-balancer>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-194">For more information, see <xref:host-and-deploy/proxy-load-balancer>.</span></span>

## <a name="configure-https"></a><span data-ttu-id="6bbd8-195">HTTPS 구성</span><span class="sxs-lookup"><span data-stu-id="6bbd8-195">Configure HTTPS</span></span>

<span data-ttu-id="6bbd8-196">보안 엔드포인트로 서비스를 구성하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-196">To configure the service with a secure endpoint:</span></span>

1. <span data-ttu-id="6bbd8-197">플랫폼의 인증서 획득 및 배포 메커니즘을 사용하여 호스팅 시스템에 대한 X.509 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-197">Create an X.509 certificate for the hosting system using your platform's certificate acquisition and deployment mechanisms.</span></span>
1. <span data-ttu-id="6bbd8-198">[Kestrel 서버 HTTPS 엔드포인트 구성](xref:fundamentals/servers/kestrel#endpoint-configuration)을 지정하여 인증서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-198">Specify a [Kestrel server HTTPS endpoint configuration](xref:fundamentals/servers/kestrel#endpoint-configuration) to use the certificate.</span></span>

<span data-ttu-id="6bbd8-199">서비스 엔드포인트를 보호하기 위해 ASP.NET Core HTTPS 개발 인증서 사용은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-199">Use of the ASP.NET Core HTTPS development certificate to secure a service endpoint isn't supported.</span></span>

## <a name="current-directory-and-content-root"></a><span data-ttu-id="6bbd8-200">현재 디렉터리 및 콘텐츠 루트</span><span class="sxs-lookup"><span data-stu-id="6bbd8-200">Current directory and content root</span></span>

<span data-ttu-id="6bbd8-201">Windows 서비스에 대해 `Directory.GetCurrentDirectory()`를 호출하여 반환된 현재 작업 디렉터리는 *C:\\WINDOWS\\system32* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-201">The current working directory returned by calling `Directory.GetCurrentDirectory()` for a Windows Service is the *C:\\WINDOWS\\system32* folder.</span></span> <span data-ttu-id="6bbd8-202">*system32* 폴더는 서비스의 파일(예: 설정 파일)을 저장을 저장하는 데 적절한 위치가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-202">The *system32* folder isn't a suitable location to store a service's files (for example, settings files).</span></span> <span data-ttu-id="6bbd8-203">다음 방법 중 하나를 사용하여 [IConfigurationBuilder](/dotnet/api/microsoft.extensions.configuration.iconfigurationbuilder)를 사용할 때 [FileConfigurationExtensions.SetBasePath](/dotnet/api/microsoft.extensions.configuration.fileconfigurationextensions.setbasepath)로 서비스의 자산 및 설정 파일을 유지 관리 및 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-203">Use one of the following approaches to maintain and access a service's assets and settings files with [FileConfigurationExtensions.SetBasePath](/dotnet/api/microsoft.extensions.configuration.fileconfigurationextensions.setbasepath) when using an [IConfigurationBuilder](/dotnet/api/microsoft.extensions.configuration.iconfigurationbuilder):</span></span>

* <span data-ttu-id="6bbd8-204">콘텐츠 루트 경로를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-204">Use the content root path.</span></span> <span data-ttu-id="6bbd8-205">`IHostingEnvironment.ContentRootPath`는 서비스가 만들어질 때 `binPath` 인수에 제공된 동일한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-205">The `IHostingEnvironment.ContentRootPath` is the same path provided to the `binPath` argument when the service is created.</span></span> <span data-ttu-id="6bbd8-206">설정 파일에 대한 경로를 만들려면 `Directory.GetCurrentDirectory()`를 사용하는 대신 콘텐츠 루트 경로를 사용하고 앱의 콘텐츠 루트의 파일을 유지 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-206">Instead of using `Directory.GetCurrentDirectory()` to create paths to settings files, use the content root path and maintain the files in the app's content root.</span></span>
* <span data-ttu-id="6bbd8-207">디스크의 적합한 위치에 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-207">Store the files in a suitable location on disk.</span></span> <span data-ttu-id="6bbd8-208">파일을 포함하는 폴더에 `SetBasePath`로 절대 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6bbd8-208">Specify an absolute path with `SetBasePath` to the folder containing the files.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6bbd8-209">추가 자료</span><span class="sxs-lookup"><span data-stu-id="6bbd8-209">Additional resources</span></span>

* <span data-ttu-id="6bbd8-210">[Kestrel 엔드포인트 구성](xref:fundamentals/servers/kestrel#endpoint-configuration)(HTTPS 구성 및 SNI 지원 포함)</span><span class="sxs-lookup"><span data-stu-id="6bbd8-210">[Kestrel endpoint configuration](xref:fundamentals/servers/kestrel#endpoint-configuration) (includes HTTPS configuration and SNI support)</span></span>
* <xref:fundamentals/host/web-host>
