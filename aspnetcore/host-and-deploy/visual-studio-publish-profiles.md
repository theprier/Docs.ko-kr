---
title: Visual Studio ASP.NET Core 응용 프로그램 배포에 대 한 프로필 게시
author: rick-anderson
description: 만드는 방법을 알아보려면 Visual Studio의 프로필 게시 하 고 다양 한 대상에 ASP.NET Core 응용 프로그램 배포를 관리 하기 위한 사용 합니다.
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 04/10/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/visual-studio-publish-profiles
ms.openlocfilehash: 3dc858793cd4ddb2630d05a5084f4b7caeaa30eb
ms.sourcegitcommit: c79fd3592f444d58e17518914f8873d0a11219c0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="visual-studio-publish-profiles-for-aspnet-core-app-deployment"></a>Visual Studio ASP.NET Core 응용 프로그램 배포에 대 한 프로필 게시

작성자: [Sayed Ibrahim Hashimi](https://github.com/sayedihashimi) 및 [Rick Anderson](https://twitter.com/RickAndMSFT)

이 문서에서는 Visual Studio 2017를 사용 하 여 만들고 사용 하 여 중점적 게시 프로필. Visual Studio에서 만들어진 게시 프로필은 MSBuild 및 Visual Studio 2017에서 실행할 수 있습니다. Azure에 게시에 관한 지침은 [Visual Studio를 사용하여 Azure App Service에 ASP.NET Core 웹앱 게시](xref:tutorials/publish-to-azure-webapp-using-vs)를 참조하세요.

명령을 사용 하 여 다음 프로젝트 파일을 만든 `dotnet new mvc`:

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>netcoreapp2.0</TargetFramework>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.AspNetCore.All" Version="2.0.0" />
  </ItemGroup>

  <ItemGroup>
    <DotNetCliToolReference Include="Microsoft.VisualStudio.Web.CodeGeneration.Tools" Version="2.0.0" />
  </ItemGroup>

</Project>
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>netcoreapp1.1</TargetFramework>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.AspNetCore" Version="1.1.5" />
    <PackageReference Include="Microsoft.AspNetCore.Mvc" Version="1.1.6" />
    <PackageReference Include="Microsoft.AspNetCore.StaticFiles" Version="1.1.3" />
  </ItemGroup>

</Project>
```

---

`<Project>` 요소의 `Sdk` 특성 다음 작업을 수행 합니다.

* 속성 파일에서 가져온 *$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Web\Sdk\Sdk.Props* 시작 부분에 있습니다.
* 종료 시 *$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Web\Sdk\Sdk.targets*에서 대상 파일을 가져옵니다.

`MSBuildSDKsPath`의 기본 위치(Visual Studio 2017 Enterprise 사용)는 *%programfiles(x86)%\Microsoft Visual Studio\2017\Enterprise\MSBuild\Sdks* 폴더입니다.

`Microsoft.NET.Sdk.Web` SDK에 따라 달라 집니다.

* *Microsoft.NET.Sdk.Web.ProjectSystem*
* *Microsoft.NET.Sdk.Publish*

그러면 다음과 같은 속성 및 가져올 대상:

* *$ (MSBuildSDKsPath)\Microsoft.NET.Sdk.Web.ProjectSystem\Sdk\Sdk.Props*
* *$ (MSBuildSDKsPath)\Microsoft.NET.Sdk.Web.ProjectSystem\Sdk\Sdk.targets*
* *$ (MSBuildSDKsPath)\Microsoft.NET.Sdk.Publish\Sdk\Sdk.Props*
* *$ (MSBuildSDKsPath)\Microsoft.NET.Sdk.Publish\Sdk\Sdk.targets*

대상을 가져오기 오른쪽 사용 되는 게시 방법에 따라 대상 집합을 게시 합니다.

MSBuild 또는 Visual Studio가 프로젝트 로드 될 때 다음과 같은 개략적인 작업이 수행 됩니다.

* 프로젝트 빌드
* 게시할 파일 계산
* 대상에 파일 게시

## <a name="compute-project-items"></a>프로젝트 항목 계산

프로젝트가 로드되면 프로젝트 항목(파일)이 계산됩니다. `item type` 특성에 따라 파일 처리 방법이 결정됩니다. 기본적으로 *.cs* 파일은 `Compile` 항목 목록에 포함됩니다. `Compile` 항목 목록의 파일이 컴파일됩니다.

`Content` 항목 목록에 빌드 출력 외에도 게시 된 파일입니다. 기본적으로 패턴과 일치 하는 파일 `wwwroot/**` 에 포함 된 `Content` 항목입니다. `wwwroot/\*\*` [와일드 카드 사용 패턴](https://gruntjs.com/configuring-tasks#globbing-patterns) 모든 파일에 *wwwroot* 폴더 **및** 하위 폴더입니다. 게시 목록에 파일을 명시적으로 추가 하려면에서 직접 파일을 추가 *.csproj* 파일에 표시 된 대로 [파일 포함](#include-files)합니다.

선택 하는 경우는 **게시** 단추 Visual Studio 또는 명령줄에서 게시 하는 경우:

* 속성/항목이 계산됩니다(빌드하는 데 필요한 파일).
* **Visual Studio만**: NuGet 패키지를 복원 합니다. (CLI에서 사용자가 명시적으로 복원해야 합니다.)
* 프로젝트가 빌드됩니다.
* 게시 항목이 계산됩니다(게시하는 데 필요한 파일).
* 프로젝트가 게시 된 (계산된 파일 게시 대상에 복사 됩니다.).

ASP.NET Core 프로젝트가 참조 하는 경우 `Microsoft.NET.Sdk.Web` 프로젝트 파일에는 *app_offline.htm* 파일이 웹 응용 프로그램 디렉터리의 루트에 배치 됩니다. 파일이 있는 경우 ASP.NET Core 모듈은 앱을 정상적으로 종료하고, 배포하는 동안 *app_offline.htm* 파일을 제공합니다. 자세한 내용은 [ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module#app_offlinehtm)를 참조하세요.

## <a name="basic-command-line-publishing"></a>기본 명령줄 게시

명령줄 게시.NET Core에서 지 원하는 모든 플랫폼에서 작동 하 고 Visual Studio 필요 하지 않습니다. 아래 예제에는 [dotnet 게시](/dotnet/core/tools/dotnet-publish) 프로젝트 디렉터리에서 명령을 실행 (포함 하는 *.csproj* 파일). 그렇지 않으면 프로젝트 폴더의 프로젝트 파일 경로에 명시적으로 전달 합니다. 예를 들어:

```console
dotnet publish C:\Webs\Web1
```

다음 명령을 실행하여 웹앱을 만들고 게시합니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

```console
dotnet new mvc
dotnet publish
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

```console
dotnet new mvc
dotnet restore
dotnet publish
```

---

[dotnet 게시](/dotnet/core/tools/dotnet-publish) 명령은 다음과 유사한 출력을 생성 합니다.

```console
C:\Webs\Web1>dotnet publish
Microsoft (R) Build Engine version 15.3.409.57025 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Web1 -> C:\Webs\Web1\bin\Debug\netcoreapp2.0\Web1.dll
  Web1 -> C:\Webs\Web1\bin\Debug\netcoreapp2.0\publish\
```

기본 게시 폴더는 `bin\$(Configuration)\netcoreapp<version>\publish`입니다. 에 대 한 기본 `$(Configuration)` 은 *디버그*합니다. 앞의 예제에서는 `<TargetFramework>` 은 `netcoreapp2.0`합니다.

`dotnet publish -h`는 게시에 대한 도움말 정보를 표시합니다.

다음 명령은 `Release` 빌드 및 게시 디렉터리를 지정합니다.

```console
dotnet publish -c Release -o C:\MyWebs\test
```

[dotnet 게시](/dotnet/core/tools/dotnet-publish) 호출 MSBuild를 호출 하는 명령에서 `Publish` 대상입니다. 모든 매개 변수가 전달 `dotnet publish` MSBuild에 전달 됩니다. `-c` 매개 변수는 `Configuration` MSBuild 속성에 매핑됩니다. `-o` 매개 변수는 `OutputPath`에 매핑됩니다.

MSBuild 속성 형식 중 하나를 사용 하 여 전달 될 수 있습니다.

* ` p:<NAME>=<VALUE>`
* `/p:<NAME>=<VALUE>`

다음 명령은 `Release` 빌드를 네트워크 공유에 게시합니다.

`dotnet publish -c Release /p:PublishDir=//r8/release/AdminWeb`

네트워크 공유는 슬래시(*//r8/*)를 사용하여 지정하고 모든 .NET Core 지원 플랫폼에서 작동합니다.

배포할 게시된 앱이 실행되고 있지 않은지 확인합니다. 앱이 실행 중이면 *publish* 폴더의 파일이 잠겨 있습니다. 잠긴 파일을 복사할 수 없으므로 배포를 수행할 수 없습니다.

## <a name="publish-profiles"></a>게시 프로필

이 섹션에서는 게시 프로필을 만들려면 Visual Studio 2017을 사용 합니다. 를 만든 후 Visual Studio 또는 명령줄에서 게시를 사용할 수 있습니다.

게시 프로필 게시 프로세스를 간소화할 수 및 프로필 개수에 관계 없이 존재할 수 있습니다. 다음 경로 중 하나를 선택 하 여 Visual Studio에서 게시 프로필을 만듭니다.

* 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다.
* 선택 **게시 &lt;project_name&gt;**  에서 **빌드** 메뉴.

**게시** 앱 용량 페이지의 탭이 표시 됩니다. 프로젝트에 게시 프로필을이 없으면 다음 페이지가 표시 됩니다.

![앱 용량 페이지에서의 게시 탭](visual-studio-publish-profiles/_static/az.png)

때 **폴더** 은 선택한 경우 게시 된 자산을 저장 하는 폴더 경로 지정 합니다. 기본 폴더는 *bin\Release\PublishOutput*합니다. 클릭는 **프로필 만들기** 단추를 완료 합니다.

게시 프로필을 만든 후의 **게시** 변경을 탭 합니다. 새로 만든된 프로필 드롭 다운 목록에 나타납니다. 클릭 **새 프로필 만들기** 다른 새 프로필을 만듭니다.

![FolderProfile 보여 주는 앱 용량 페이지에서의 게시 탭](visual-studio-publish-profiles/_static/create_new.png)

게시 마법사는 다음 게시 대상을 지원합니다.

* Azure App Service
* Azure Virtual Machines
* (모든 웹 서버)에 대 한 IIS, FTP 등
* 폴더
* 프로필 가져오기

자세한 내용은 참조 [어떤 게시 옵션은 내게 적합 한](/visualstudio/ide/not-in-toc/web-publish-options)합니다.

Visual Studio와 함께 게시 프로필을 만들 때 한 *속성/PublishProfiles/&lt;profile_name&gt;.pubxml* MSBuild 파일이 만들어집니다. *.pubxml* 파일 MSBuild 파일은 포함 하 고 게시 설정을 구성 합니다. 빌드 사용자 지정 및 프로세스를 게시 하려면이 파일을 변경할 수 있습니다. 게시 프로세스에서 이 파일을 읽습니다. `<LastUsedBuildConfiguration>` 전역 속성을 빌드에 가져온 모든 파일에 되지 않아야 하기 때문에 특별 합니다. 참조 [MSBuild: 구성 속성을 설정 하는 방법](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx) 자세한 정보에 대 한 합니다.

Azure는 대상에 게시 하는 경우는 *.pubxml* 파일 Azure 구독 id를 포함 합니다. 해당 대상 형식으로이 파일을 소스 제어에 추가 권장 되지 않습니다. 비 Azure 대상을 게시할 때이 체크 인할 안전는 *.pubxml* 파일입니다.

중요 한 정보 (예: 암호로 게시는)에서 암호화 한 사용자/컴퓨터 수준 당 합니다. 에 저장 되는 *속성/PublishProfiles/&lt;profile_name&gt;. pubxml.user* 파일입니다. 이 파일에서 중요 한 정보를 저장할 수 있으므로 소스 제어에 체크 인할 수 없습니다.

ASP.NET core 웹 앱을 게시 하는 방법의 개요를 참조 하십시오. [호스트 하 고 배포](xref:host-and-deploy/index)합니다. MSBuild 작업 및 ASP.NET Core 응용 프로그램을 게시 하는 데 필요한 대상은 오픈 소스에서 https://github.com/aspnet/websdk합니다.

`dotnet publish` 폴더를 MSDeploy צ ְ ײ 및 [Kudu](https://github.com/projectkudu/kudu/wiki) 게시 프로필:

폴더 (플랫폼 간에 작동):

```console
dotnet publish WebApplication.csproj /p:PublishProfile=<FolderProfileName>
```

MSDeploy (현재는 기능만 MSDeploy 없는 플랫폼 간 이후 Windows의):

```console
dotnet publish WebApplication.csproj /p:PublishProfile=<MsDeployProfileName> /p:Password=<DeploymentPassword>
```

MSDeploy 패키지 (현재는 기능만 MSDeploy 없는 플랫폼 간 이후 Windows의):

```console
dotnet publish WebApplication.csproj /p:PublishProfile=<MsDeployPackageProfileName>
```

위의 샘플에서 **하지** 전달 `deployonbuild` 를 `dotnet publish`합니다.

자세한 내용은 참조 [Microsoft.NET.Sdk.Publish](https://github.com/aspnet/websdk#microsoftnetsdkpublish)합니다.

`dotnet publish` 모든 플랫폼에서 Azure로 게시할 Kudu Api를 지원 합니다. Visual Studio 게시 지원 플랫폼 간 Azure에 게시에 대 한 Kudu Api 하지만 WebSDK에서 지원 됩니다.

게시 프로필에 추가 된 *속성/PublishProfiles* 다음 내용 사용 하 여 폴더:

```xml
<Project>
  <PropertyGroup>
    <PublishProtocol>Kudu</PublishProtocol>
    <PublishSiteName>nodewebapp</PublishSiteName>
    <UserName>username</UserName>
    <Password>password</Password>
  </PropertyGroup>
</Project>
```

Kudu Api를 사용 하 여 Azure에 게시 하 고 게시 콘텐츠를 압축 하려면 다음 명령을 실행 합니다.

```console
dotnet publish /p:PublishProfile=Azure /p:Configuration=Release
```

게시 프로필을 사용할 경우 다음 MSBuild 속성을 설정합니다.

* `DeployOnBuild=true`
* `PublishProfile=<Publish profile name>`

명명 된 프로필을 게시할 때 *FolderProfile*, 다음 명령 중 하나를 실행할 수 있습니다.

* `dotnet build /p:DeployOnBuild=true /p:PublishProfile=FolderProfile`
* `msbuild      /p:DeployOnBuild=true /p:PublishProfile=FolderProfile`

호출할 때 [dotnet 빌드](/dotnet/core/tools/dotnet-build), 호출 `msbuild` 를 빌드를 실행 하 고 프로세스를 게시 합니다. 호출 `dotnet build` 또는 `msbuild` 폴더 프로 파일에 전달할 때과 같습니다. MSBuild를 Windows에서 직접 호출할 때.NET Framework 버전의 MSBuild 사용 됩니다. MSDeploy는 현재 게시를 위해 Windows 컴퓨터로 제한됩니다. 폴더가 아닌 프로필에서 `dotnet build`를 호출하면 MSBuild가 호출되고 MSBuild는 폴더가 아닌 프로필에서 MSDeploy를 사용합니다. 폴더가 아닌 프로필에서 `dotnet build`를 호출하면 MSBuild가 호출되고(MSDeploy 사용) Windows 플랫폼에서 실행될 경우에도 오류가 발생합니다. 폴더가 아닌 프로필을 사용하여 게시하려면 MSBuild를 직접 호출합니다.

다음 폴더 게시 프로필은 Visual Studio를 사용하여 만들어졌고 네트워크 공유에 게시됩니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<!--
This file is used by the publish/package process of your Web project.
You can customize the behavior of this process by editing this 
MSBuild file.
-->
<Project ToolsVersion="4.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <PropertyGroup>
    <WebPublishMethod>FileSystem</WebPublishMethod>
    <PublishProvider>FileSystem</PublishProvider>
    <LastUsedBuildConfiguration>Release</LastUsedBuildConfiguration>
    <LastUsedPlatform>Any CPU</LastUsedPlatform>
    <SiteUrlToLaunchAfterPublish />
    <LaunchSiteAfterPublish>True</LaunchSiteAfterPublish>
    <ExcludeApp_Data>False</ExcludeApp_Data>
    <PublishFramework>netcoreapp1.1</PublishFramework>
    <ProjectGuid>c30c453c-312e-40c4-aec9-394a145dee0b</ProjectGuid>
    <publishUrl>\\r8\Release\AdminWeb</publishUrl>
    <DeleteExistingFiles>False</DeleteExistingFiles>
  </PropertyGroup>
</Project>
```

`<LastUsedBuildConfiguration>`은 `Release`로 설정됩니다. Visual Studio에서 게시할 경우 `<LastUsedBuildConfiguration>` 구성 속성 값은 게시 프로세스가 시작될 때의 값을 사용하여 설정됩니다. `<LastUsedBuildConfiguration>` 구성 속성은 특수 하며 가져온된 MSBuild 파일에서 재정의할 수 없습니다. 명령줄에서이 속성을 재정의할 수 있습니다.

.NET Core CLI를 사용 하 여:

```console
dotnet build -c Release /p:DeployOnBuild=true /p:PublishProfile=FolderProfile
```

MSBuild 사용:

```console
msbuild /p:Configuration=Release /p:DeployOnBuild=true /p:PublishProfile=FolderProfile
```

## <a name="publish-to-an-msdeploy-endpoint-from-the-command-line"></a>명령줄에서 MSDeploy 끝점에 게시

.NET Core CLI 또는 MSBuild를 사용 하 여 게시를 수행할 수 있습니다. `dotnet publish`는 .NET Core의 컨텍스트에서 실행됩니다. `msbuild` 명령 Windows 환경으로 제한 하는.NET Framework에 필요 합니다.

MSDeploy를 사용하여 게시하는 가장 좋은 방법은 먼저 Visual Studio 2017에서 게시 프로필을 만들고 명령줄에서 프로필을 사용하는 것입니다.

다음 샘플에서는 ASP.NET Core 웹 앱을 만듭니다 (사용 하 여 `dotnet new mvc`), Azure 게시 프로필이 Visual Studio와 함께 추가 됩니다.

실행 `msbuild` 에서 **VS 2017 용 개발자 명령 프롬프트**합니다. 개발자 명령 프롬프트에 올바른 *msbuild.exe* 일부 MSBuild 변수 집합과 그 경로에 있습니다.

MSBuild는 다음 구문을 사용합니다.

```console
msbuild <path-to-project-file> /p:DeployOnBuild=true /p:PublishProfile=<Publish Profile> /p:Username=<USERNAME> /p:Password=<PASSWORD>
```

가져오기는 `Password` 에서  *\<게시 이름 >. PublishSettings* 파일입니다. 다운로드는 *합니다. PublishSettings* 파일 중 하나에서:

* 솔루션 탐색기: 웹 응용 프로그램을 마우스 오른쪽 단추로 클릭 하 고 선택 **게시 프로필 다운로드**합니다.
* Azure 포털: 클릭 **Get 게시 프로필** 웹 앱에서 **개요** 패널입니다.

`Username`은 게시 프로필에서 찾을 수 있습니다.

다음 샘플에서는 *Web11112-웹 배포* 게시 프로필:

```console
msbuild "C:\Webs\Web1\Web1.csproj" /p:DeployOnBuild=true
 /p:PublishProfile="Web11112 - Web Deploy"  /p:Username="$Web11112"
 /p:Password="<password removed>"
```

## <a name="exclude-files"></a>파일 제외

ASP.NET Core 웹앱을 게시할 경우 *wwwroot* 폴더의 빌드 아티팩트 및 콘텐츠가 포함됩니다. `msbuild`는 [와일드카드 사용 패턴](https://gruntjs.com/configuring-tasks#globbing-patterns)을 지원합니다. 예를 들어, 다음 `<Content>` 모든 텍스트를 제외 하는 요소 (*.txt*)에서 파일을 *wwwroot/content* 폴더와 모든 하위 폴더입니다.

```xml
<ItemGroup>
  <Content Update="wwwroot/content/**/*.txt" CopyToPublishDirectory="Never" />
</ItemGroup>
```

위의 태그 게시 프로필에 추가할 수 있습니다 또는 *.csproj* 파일입니다. *.csproj* 파일에 추가된 규칙은 프로젝트의 모든 게시 프로필에 추가됩니다.

다음 `<MsDeploySkipRules>` 에서 모든 파일을 제외 하는 요소는 *wwwroot/content* 폴더:

```xml
<ItemGroup>
  <MsDeploySkipRules Include="CustomSkipFolder">
    <ObjectName>dirPath</ObjectName>
    <AbsolutePath>wwwroot\\content</AbsolutePath>
  </MsDeploySkipRules>
</ItemGroup>
```

`<MsDeploySkipRules>` 삭제 되지 않습니다는 *건너뛸* 배포 사이트에서 대상으로 합니다. `<Content>` 대상된 파일 및 폴더는 배포 사이트에서 삭제 됩니다. 예를 들어 배포 된 웹 응용 프로그램에는 다음 파일이 있다고 가정 합니다.

* *Views/Home/About1.cshtml*
* *Views/Home/About2.cshtml*
* *Views/Home/About3.cshtml*

하는 경우 다음 `<MsDeploySkipRules>` 요소가 추가, 배포 사이트에서 해당 파일을 삭제할 수 없습니다.

```xml
<ItemGroup>
  <MsDeploySkipRules Include="CustomSkipFile">
    <ObjectName>filePath</ObjectName>
    <AbsolutePath>Views\\Home\\About1.cshtml</AbsolutePath>
  </MsDeploySkipRules>

  <MsDeploySkipRules Include="CustomSkipFile">
    <ObjectName>filePath</ObjectName>
    <AbsolutePath>Views\\Home\\About2.cshtml</AbsolutePath>
  </MsDeploySkipRules>

  <MsDeploySkipRules Include="CustomSkipFile">
    <ObjectName>filePath</ObjectName>
    <AbsolutePath>Views\\Home\\About3.cshtml</AbsolutePath>
  </MsDeploySkipRules>
</ItemGroup>
```

앞의 `<MsDeploySkipRules>` 요소 방지는 *건너뛴* 를 배포할 파일입니다. 배포 되는 되 면 해당 파일을 삭제 되지 않습니다 것입니다.

다음 `<Content>` 배포 사이트에서 대상으로 지정 된 파일을 삭제 하는 요소:

```xml
<ItemGroup>
  <Content Update="Views/Home/About?.cshtml" CopyToPublishDirectory="Never" />
</ItemGroup>
```

명령줄 배포를 사용 하 여 앞으로 `<Content>` 요소는 다음과 같은 출력을 생성 합니다.

```console
MSDeployPublish:
  Starting Web deployment task from source: manifest(C:\Webs\Web1\obj\Release\netcoreapp1.1\PubTmp\Web1.SourceManifest.
  xml) to Destination: auto().
  Deleting file (Web11112\Views\Home\About1.cshtml).
  Deleting file (Web11112\Views\Home\About2.cshtml).
  Deleting file (Web11112\Views\Home\About3.cshtml).
  Updating file (Web11112\web.config).
  Updating file (Web11112\Web1.deps.json).
  Updating file (Web11112\Web1.dll).
  Updating file (Web11112\Web1.pdb).
  Updating file (Web11112\Web1.runtimeconfig.json).
  Successfully executed Web deployment task.
  Publish Succeeded.
Done Building Project "C:\Webs\Web1\Web1.csproj" (default targets).
```

## <a name="include-files"></a>포함 파일

다음 태그를 포함 한 *이미지* 폴더를 프로젝트 디렉터리 외부의 *wwwroot/이미지* 게시 사이트의 폴더:

```xml
<ItemGroup>
  <_CustomFiles Include="$(MSBuildProjectDirectory)/../images/**/*" />
  <DotnetPublishFiles Include="@(_CustomFiles)">
    <DestinationRelativePath>wwwroot/images/%(RecursiveDir)%(Filename)%(Extension)</DestinationRelativePath>
  </DotnetPublishFiles>
</ItemGroup>
```

태그는 *.csproj* 파일 또는 게시 프로필에 추가될 수 있습니다. 에 추가 되 면는 *.csproj* 파일을 프로젝트에 각 게시 프로필에 포함 된 것입니다.

다음 강조 표시된 태그는 방법을 표시합니다.

* 프로젝트 외부에서 *wwwroot* 폴더로 파일을 복사합니다.
* *wwwroot\Content* 폴더를 제외합니다.
* *Views\Home\About2.cshtml*을 제외합니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<!--
This file is used by the publish/package process of your Web project.
You can customize the behavior of this process by editing this 
MSBuild file.
-->
<Project ToolsVersion="4.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <PropertyGroup>
    <WebPublishMethod>FileSystem</WebPublishMethod>
    <PublishProvider>FileSystem</PublishProvider>
    <LastUsedBuildConfiguration>Release</LastUsedBuildConfiguration>
    <LastUsedPlatform>Any CPU</LastUsedPlatform>
    <SiteUrlToLaunchAfterPublish />
    <LaunchSiteAfterPublish>True</LaunchSiteAfterPublish>
    <ExcludeApp_Data>False</ExcludeApp_Data>
    <PublishFramework />
    <ProjectGuid>afa9f185-7ce0-4935-9da1-ab676229d68a</ProjectGuid>
    <publishUrl>bin\Release\PublishOutput</publishUrl>
    <DeleteExistingFiles>False</DeleteExistingFiles>
  </PropertyGroup>
  <ItemGroup>
    <ResolvedFileToPublish Include="..\ReadMe2.MD">
      <RelativePath>wwwroot\ReadMe2.MD</RelativePath>
    </ResolvedFileToPublish>

    <Content Update="wwwroot\Content\**\*" CopyToPublishDirectory="Never" />
    <Content Update="Views\Home\About2.cshtml" CopyToPublishDirectory="Never" />

  </ItemGroup>
</Project>
```

더 많은 배포 샘플을 보려면 [WebSDK Readme](https://github.com/aspnet/websdk)(WebSDK 추가 정보)를 참조하세요.

## <a name="run-a-target-before-or-after-publishing"></a>게시 이전 또는 이후 대상 실행

기본 제공 `BeforePublish` 및 `AfterPublish` 앞 이나 뒤 게시 대상이 대상 대상이 실행 합니다. 게시 후 및 하기 전에 콘솔 메시지를 기록 하려면 게시 프로필에 다음 요소를 추가 합니다.

```xml
<Target Name="CustomActionsBeforePublish" BeforeTargets="BeforePublish">
    <Message Text="Inside BeforePublish" Importance="high" />
  </Target>
  <Target Name="CustomActionsAfterPublish" AfterTargets="AfterPublish">
    <Message Text="Inside AfterPublish" Importance="high" />
</Target>
```

## <a name="publish-to-a-server-using-an-untrusted-certificate"></a>신뢰할 수 없는 인증서를 사용 하 여 서버에 게시

추가 `<AllowUntrustedCertificate>` 속성의 값과 `True` 게시 프로필:

```xml
<PropertyGroup>
  <AllowUntrustedCertificate>True</AllowUntrustedCertificate>
</PropertyGroup>
```

## <a name="the-kudu-service"></a>Kudu 서비스

파일을 보려면 Azure 앱 서비스 웹 응용 프로그램 배포에서를 사용 하 여는 [Kudu 서비스](https://github.com/projectkudu/kudu/wiki/Accessing-the-kudu-service)합니다. 추가 `scm` 토큰을 웹 응용 프로그램 이름입니다. 예를 들어:

| URL                                    | 결과       |
| -------------------------------------- | ------------ |
| `http://mysite.azurewebsites.net/`     | 웹앱      |
| `http://mysite.scm.azurewebsites.net/` | Kudu 서비스 |

선택 된 [디버그 콘솔](https://github.com/projectkudu/kudu/wiki/Kudu-console) 메뉴 항목을 보고, 편집, 삭제 또는 파일을 추가 합니다.

## <a name="additional-resources"></a>추가 자료

* [웹 배포](https://www.iis.net/downloads/microsoft/web-deploy) (MSDeploy)는 웹 응용 프로그램 및 웹 사이트는 IIS 서버에 배포를 간소화 합니다.
* [https://github.com/aspnet/websdk](https://github.com/aspnet/websdk/issues): 파일 문제 및 배포에 대 한 기능을 요청 합니다.
