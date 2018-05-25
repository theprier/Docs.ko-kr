---
title: ASP.NET Core 2.1 이상용 Microsoft.AspNetCore.App 메타패키지
author: Rick-Anderson
description: Microsoft.AspNetCore.App 메타패키지에는 지원되는 모든 ASP.NET Core 및 Entity Framework Core 패키지가 포함됩니다.
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.date: 09/20/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/metapackage-app
ms.openlocfilehash: 7c7f69a6176d3f7982a67106cb823ff42200b50e
ms.sourcegitcommit: 3a893ae05f010656d99d6ddf55e82f1b5b6933bc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/18/2018
---
# <a name="microsoftaspnetcoreapp-metapackage-for-aspnet-core-21"></a>ASP.NET Core 2.1용 Microsoft.AspNetCore.App 메타패키지

이 기능을 사용하려면 .NET Core 2.1 이상을 대상으로 하는 ASP.NET Core 2.1 이상이 필요합니다.

ASP.NET Core용 [Microsoft.AspNetCore.App](https://www.nuget.org/packages/Microsoft.AspNetCore.App) [메타패키지](/dotnet/core/packages#metapackages):

* [Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/), [Remotion.Linq](https://www.nuget.org/packages/Remotion.Linq/) 및 [IX-Async](https://www.nuget.org/packages/System.Interactive.Async/)를 제외한 타사 종속성을 포함하지 마세요. 이러한 타사 종속성은 주요 프레임워크 기능이 작동하도록 하는 데 필요한 것으로 간주됩니다.
* 이전에 언급한 것 이외의 타사 종속성을 포함하는 것을 제외하고 ASP.NET Core 팀에서 지원하는 모든 패키지를 포함합니다.
* 이전에 언급한 것 이외의 타사 종속성을 포함하는 것을 제외하고 Entity Framework 팀에서 지원하는 모든 패키지를 포함합니다.

ASP.NET Core 2.1 이상 Entity Framework Core 2.1 이상의 모든 기능은 `Microsoft.AspNetCore.App` 패키지에 포함됩니다. ASP.NET Core 2.1 이상을 대상으로 하는 기본 프로젝트 템플릿에는 이 패키지를 사용합니다. ASP.NET Core 2.1 이상과 Entity Framework Core 2.1 이상을 대상으로 하는 응용 프로그램은 `Microsoft.AspNetCore.App` 패키지를 사용하는 것이 좋습니다.

`Microsoft.AspNetCore.App` 메타패키지의 버전 번호는 ASP.NET Core 버전 및 Entity Framework Core 버전을 나타냅니다.

`Microsoft.AspNetCore.App` 메타패키지 사용 시에는 앱을 보호하기 위한 버전 제한 사항이 적용됩니다.

* `Microsoft.AspNetCore.App`에 패키지에 대한 전이적인(직접적이지 않은) 종속성을 가진 패키지가 포함되어 있고, 이러한 버전 번호가 서로 다를 경우 NuGet에서 오류를 생성합니다.
* 앱에 추가된 다른 패키지는 `Microsoft.AspNetCore.App`에 포함된 패키지 버전을 변경할 수 없습니다.
* 버전 일관성은 안정적인 환경을 보장합니다. `Microsoft.AspNetCore.App`은 동일한 앱에서 함께 사용되는 관련 비트의 테스트되지 않은 버전 조합을 방지하도록 설계되었습니다.

`Microsoft.AspNetCore.App` 메타패키지를 사용하는 응용 프로그램은 ASP.NET Core 공유 프레임워크를 자동으로 활용합니다. `Microsoft.AspNetCore.App` 메타패키지를 사용할 경우, 참조되는 ASP.NET Core NuGet 패키지의 자산이 응용 프로그램을 사용하여 배포되지 **않습니다**. 이러한 자산은 &mdash; ASP.NET Core 공유 프레임워크에 포함됩니다. 공유 프레임워크의 자산은 응용 프로그램 시작 시간 단축을 위해 미리 컴파일됩니다. 자세한 내용은 [.NET Core 배포 패키징](/dotnet/core/build/distribution-packaging)의 "공유 프레임워크"를 참조하세요.

다음 *.csproj* 프로젝트 파일은 ASP.NET Core용 `Microsoft.AspNetCore.App` 메타패키지를 참조합니다.

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>netcoreapp2.1</TargetFramework>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.AspNetCore.App" />
  </ItemGroup>

</Project>

```

이전의 표시는 일반적인 ASP.NET Core 2.1 이상의 템플릿을 나타냅니다. `Microsoft.AspNetCore.App` 패키지 참조의 버전 번호는 지정하지 않습니다. 버전이 지정되지 않은 경우 SDK에서 [암시적](https://github.com/dotnet/core/blob/master/release-notes/1.0/sdk/1.0-rc3-implicit-package-refs.md) 버전, 즉 `Microsoft.NET.Sdk.Web`을 지정합니다. SDK에서 지정하는 암시적 버전을 사용하고, 패키지 참조에 버전 번호를 명시적으로 설정하지 않는 것이 좋습니다. GitHub의 [Microsoft.AspNetCore.App 암시적 버전에 대한 토론](https://github.com/aspnet/Docs/issues/6430)에 의견을 남길 수 있습니다.

휴대용 앱의 암시적 버전은 `major.minor.0`으로 설정됩니다. 공유 프레임워크 롤포워드 메커니즘은 설치된 공유 프레임워크 중 최신 호환 버전에서 앱을 실행합니다. 개발, 테스트 및 프로덕션에서 동일한 버전이 사용되도록 하려면 모든 환경에 동일한 버전의 공유 프레임워크를 설치하도록 하세요. 자체 포함 앱의 경우 암시적 버전 번호가 설치된 SDK에 포함된 공유 프레임워크의 `major.minor.patch`로 설정됩니다.

`Microsoft.AspNetCore.App` 참조에 버전 번호를 지정해도 해당 버전의 고유 프레임워크가 선택된다고 보장할 수 **없습니다**. 예를 들어 "2.1.1" 버전을 지정했는데 "2.1.3"이 설치되는 경우가 있습니다. 이 경우 앱은 "2.1.3"을 사용합니다. 권장되는 방법은 아니지만 롤포워드를 비활성화할 수 있습니다(패치 및/또는 부 버전). DotNet 호스트 롤포워드 및 이 동작을 구성하는 방법에 대한 자세한 내용은 [DotNet 호스트 롤포워드](https://github.com/dotnet/core-setup/blob/master/Documentation/design-docs/roll-forward-on-no-candidate-fx.md)를 참조하세요.

`Microsoft.AspNetCore.App` [메타패키지](/dotnet/core/packages#metapackages)는 기존 패키지가 NuGet에서 업데이트된 것이 아닙니다. `Microsoft.NETCore.App`과 유사한 `Microsoft.AspNetCore.App`은 공유 런타임을 나타내며, NuGet 외부에서 처리되는 특별한 버전 관리 의미 체계가 있습니다. 자세한 내용은 [패키지, 메타패키지 및 프레임워크](/dotnet/core/packages)를 참조하세요.

응용 프로그램에서 이전에 `Microsoft.AspNetCore.All`을 사용한 경우 [Microsoft.AspNetCore.All에서 Microsoft.AspNetCore.App으로 마이그레이션](xref:fundamentals/metapackage#migrate)을 참조하세요.
