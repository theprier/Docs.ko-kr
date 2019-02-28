---
title: Blazor용 링커 구성
author: guardrex
description: Blazor 앱을 빌드할 때 IL(Intermediate Language) 링커를 제어하는 방법을 알아봅니다.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 02/20/2019
uid: host-and-deploy/razor-components/configure-linker
ms.openlocfilehash: 7c53e7912ec3b0ae471ea38777f874f55a32487d
ms.sourcegitcommit: 0945078a09c372f17e9b003758ed87e99c2449f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/21/2019
ms.locfileid: "56647943"
---
# <a name="configure-the-linker-for-blazor"></a><span data-ttu-id="2f834-103">Blazor용 링커 구성</span><span class="sxs-lookup"><span data-stu-id="2f834-103">Configure the Linker for Blazor</span></span>

<span data-ttu-id="2f834-104">[Luke Latham](https://github.com/guardrex)으로</span><span class="sxs-lookup"><span data-stu-id="2f834-104">By [Luke Latham](https://github.com/guardrex)</span></span>

[!INCLUDE[](~/includes/razor-components-preview-notice.md)]

<span data-ttu-id="2f834-105">Blazor는 각 릴리스 모드 빌드 중에 [IL(Intermediate Language)](/dotnet/standard/managed-code#intermediate-language--execution) 연결을 수행하여 출력 어셈블리에서 불필요한 IL을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="2f834-105">Blazor performs [Intermediate Language (IL)](/dotnet/standard/managed-code#intermediate-language--execution) linking during each Release mode build to remove unnecessary IL from the output assemblies.</span></span>

<span data-ttu-id="2f834-106">다음 방법 중 하나를 사용하여 어셈블리 연결을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f834-106">You can control assembly linking with either of the following approaches:</span></span>

* <span data-ttu-id="2f834-107">MSBuild 속성을 사용하여 전역적으로 링크를 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2f834-107">Disable linking globally with an MSBuild property.</span></span>
* <span data-ttu-id="2f834-108">구성 파일을 사용하여 어셈블리별로 연결을 제어합니다</span><span class="sxs-lookup"><span data-stu-id="2f834-108">Control linking on a per-assembly basis with a configuration file.</span></span>

## <a name="disable-linking-with-an-msbuild-property"></a><span data-ttu-id="2f834-109">MSBuild 속성을 사용하여 연결을 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2f834-109">Disable linking with an MSBuild property</span></span>

<span data-ttu-id="2f834-110">게시를 포함하는 앱이 빌드되면 릴리스 모드에서 연결이 기본적으로 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f834-110">Linking is enabled by default in Release mode when an app is built, which includes publishing.</span></span> <span data-ttu-id="2f834-111">모든 어셈블리에 대한 연결을 비활성화하려면 프로젝트 파일에서 `<BlazorLinkOnBuild>` MSBuild 속성을 `false`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2f834-111">To disable linking for all assemblies, set the `<BlazorLinkOnBuild>` MSBuild property to `false` in the project file:</span></span>

```xml
<PropertyGroup>
  <BlazorLinkOnBuild>false</BlazorLinkOnBuild>
</PropertyGroup>
```

## <a name="control-linking-with-a-configuration-file"></a><span data-ttu-id="2f834-112">구성 파일과의 연결 제어</span><span class="sxs-lookup"><span data-stu-id="2f834-112">Control linking with a configuration file</span></span>

<span data-ttu-id="2f834-113">연결은 XML 구성 파일을 제공하고 프로젝트 파일에서 해당 파일을 MSBuild 항목으로 지정하여 어셈블리별로 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f834-113">Linking can be controlled on a per-assembly basis by providing an XML configuration file and specifying the file as an MSBuild item in the project file.</span></span>

<span data-ttu-id="2f834-114">다음은 예제 구성 파일(*Linker.xml*)입니다.</span><span class="sxs-lookup"><span data-stu-id="2f834-114">The following is an example configuration file (*Linker.xml*):</span></span>

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!--
  This file specifies which parts of the BCL or Blazor packages must not be
  stripped by the IL Linker even if they aren't referenced by user code.
-->
<linker>
  <assembly fullname="mscorlib">
    <!--
      Preserve the methods in WasmRuntime because its methods are called by 
      JavaScript client-side code to implement timers.
      Fixes: https://github.com/aspnet/Blazor/issues/239
    -->
    <type fullname="System.Threading.WasmRuntime" />
  </assembly>
  <assembly fullname="System.Core">
    <!--
      System.Linq.Expressions* is required by Json.NET and any 
      expression.Compile caller. The assembly isn't stripped.
    -->
    <type fullname="System.Linq.Expressions*" />
  </assembly>
  <!--
    In this example, the app's entry point assembly is listed. The assembly
    isn't stripped by the IL Linker.
  -->
  <assembly fullname="MyCoolBlazorApp" />
</linker>
```

<span data-ttu-id="2f834-115">구성 파일의 파일 형식에 대한 자세한 내용은 [IL 링커: Xml 설명자 구문](https://github.com/mono/linker/blob/master/src/linker/README.md#syntax-of-xml-descriptor)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2f834-115">To learn more about the file format for the configuration file, see [IL Linker: Syntax of xml descriptor](https://github.com/mono/linker/blob/master/src/linker/README.md#syntax-of-xml-descriptor).</span></span>

<span data-ttu-id="2f834-116">`BlazorLinkerDescriptor` 항목을 사용하여 프로젝트 파일에서 구성 파일을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2f834-116">Specify the configuration file in the project file with the `BlazorLinkerDescriptor` item:</span></span>

```xml
<ItemGroup>
  <BlazorLinkerDescriptor Include="Linker.xml" />
</ItemGroup>
```
