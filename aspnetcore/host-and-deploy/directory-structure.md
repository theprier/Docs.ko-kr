---
title: ASP.NET Core 디렉터리 구조
author: guardrex
description: 게시된 ASP.NET Core 앱의 디렉터리 구조에 대해 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 04/09/2018
uid: host-and-deploy/directory-structure
ms.openlocfilehash: 8e2693397f826d0e9a36ff52aa1d1d623b31043d
ms.sourcegitcommit: 356c8d394aaf384c834e9c90cabab43bfe36e063
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2018
ms.locfileid: "36960829"
---
# <a name="aspnet-core-directory-structure"></a>ASP.NET Core 디렉터리 구조

[Luke Latham](https://github.com/guardrex)으로

ASP.NET Core에서 게시된 응용 프로그램 디렉터리인 *publish*는 응용 프로그램 파일, 구성 파일, 정적 자산, 패키지 및 런타임([자체 포함 배포](/dotnet/core/deploying/#self-contained-deployments-scd)의 경우)으로 구성됩니다.


| 앱 형식 | 디렉터리 구조 |
| -------- | ------------------- |
| [프레임워크 종속 배포](/dotnet/core/deploying/#framework-dependent-deployments-fdd) | <ul><li>publish&dagger;<ul><li>Logs&dagger;(stdout 로그를 수신하는 데 필요한 경우가 아니면 선택 사항)</li><li>Views&dagger;(MVC 앱, 뷰가 미리 컴파일되지 않은 경우)</li><li>Pages&dagger;(MVC 또는 Razor 페이지 앱, 페이지가 미리 컴파일되지 않은 경우)</li><li>wwwroot&dagger;</li><li>*\.dll 파일</li><li>\<assembly-name>.deps.json</li><li>\<assembly-name>.dll</li><li>\<assembly-name>.pdb</li><li>\<assembly-name>.PrecompiledViews.dll</li><li>\<assembly-name>.PrecompiledViews.pdb</li><li>\<assembly-name>.runtimeconfig.json</li><li>web.config(IIS 배포)</li></ul></li></ul> |
| [자체 포함 배포](/dotnet/core/deploying/#self-contained-deployments-scd) | <ul><li>publish&dagger;<ul><li>Logs&dagger;(stdout 로그를 수신하는 데 필요한 경우가 아니면 선택 사항)</li><li>refs&dagger;</li><li>Views&dagger;(MVC 앱, 뷰가 미리 컴파일되지 않은 경우)</li><li>Pages&dagger;(MVC 또는 Razor 페이지 앱, 페이지가 미리 컴파일되지 않은 경우)</li><li>wwwroot&dagger;</li><li>\*.dll 파일</li><li>\<assembly-name>.deps.json</li><li>\<assembly-name>.exe</li><li>\<assembly-name>.pdb</li><li>\<assembly-name>.PrecompiledViews.dll</li><li>\<assembly-name>.PrecompiledViews.pdb</li><li>\<assembly-name>.runtimeconfig.json</li><li>web.config(IIS 배포)</li></ul></li></ul> |

&dagger;디렉터리를 나타냄

*publish* 디렉터리는 배포의 *응용 프로그램 기본 경로*라고도 하는 *콘텐츠 루트 경로*를 나타냅니다. 서버에 배포된 앱의 *publish* 디렉터리에 어떤 이름을 지정하더라도 해당 위치는 호스트된 앱에 대한 서버의 실제 경로로 사용됩니다.

*wwwroot* 디렉터리(있는 경우)에는 정적 자산만 포함됩니다.

다음 두 가지 방법 중 하나를 사용하여 stdout *Logs* 디렉터리를 배포용으로 만들 수 있습니다.

* 다음 `<Target>` 요소를 프로젝트 파일에 추가합니다.

   ```xml
   <Target Name="CreateLogsFolder" AfterTargets="Publish">
     <MakeDir Directories="$(PublishDir)Logs" 
              Condition="!Exists('$(PublishDir)Logs')" />
     <WriteLinesToFile File="$(PublishDir)Logs\.log" 
                       Lines="Generated file" 
                       Overwrite="True" 
                       Condition="!Exists('$(PublishDir)Logs\.log')" />
   </Target>
   ```

   `<MakeDir>` 요소는 게시된 출력에 빈 *Logs* 폴더를 만듭니다. 이 요소는 `PublishDir` 속성을 사용하여 폴더를 만들 대상 위치를 확인합니다. 웹 배포와 같은 여러 배포 방법에서는 배포 중에 빈 폴더를 건너뜁니다. `<WriteLinesToFile>` 요소는 파일이 서버에 배포되도록 *Logs* 폴더에 파일을 생성합니다. 대상 폴더에 대한 쓰기 권한이 작업자 프로세스에 없는 경우에는 폴더 만들기에 실패할 수 있습니다.

* 배포 시 서버에서 *Logs* 디렉터리를 실제로 만드세요.

배포 디렉터리에는 읽기/실행 권한이 필요합니다. *Logs* 디렉터리에는 읽기/쓰기 권한이 필요합니다. 파일이 작성되는 추가 디렉터리에는 읽기/쓰기 권한이 필요합니다.
