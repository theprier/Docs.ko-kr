---
title: ASP.NET Core 디렉터리 구조
author: guardrex
description: 게시된 ASP.NET Core 앱의 디렉터리 구조에 대해 알아봅니다.
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 04/09/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/directory-structure
ms.openlocfilehash: a5cc1f23d624643facddc9e2006fb246e5ae66dc
ms.sourcegitcommit: 477d38e33530a305405eaf19faa29c6d805273aa
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2018
---
# <a name="aspnet-core-directory-structure"></a>ASP.NET Core 디렉터리 구조

[Luke Latham](https://github.com/guardrex)으로

ASP.NET Core, 게시 된 응용 프로그램 디렉터리에서에서 *게시*, 응용 프로그램 파일, config 파일, 정적 자산, 패키지 및 런타임 구성 됩니다 (에 대 한 [자체 포함된 배포](/dotnet/core/deploying/#self-contained-deployments-scd)).


| 앱 유형 | 디렉터리 구조 |
| -------- | ------------------- |
| [프레임 워크 종속 배포](/dotnet/core/deploying/#framework-dependent-deployments-fdd) | <ul><li>publish&dagger;<ul><li>로그&dagger; (stdout 로그를 받을 수 필요로 하지 않는 경우 선택 사항)</li><li>뷰&dagger; (MVC 앱; 뷰 아닌 미리 컴파일하는 경우)</li><li>페이지&dagger; (MVC 또는 Razor 페이지 앱; 페이지가 아닌 미리 컴파일하는 경우)</li><li>wwwroot&dagger;</li><li>*\.dll 파일</li><li>\<어셈블리 이름 >. deps.json</li><li>\<어셈블리 이름 >.dll</li><li>\<어셈블리 이름 >.pdb</li><li>\<어셈블리 이름 >. PrecompiledViews.dll</li><li>\<어셈블리 이름 >. PrecompiledViews.pdb</li><li>\<어셈블리 이름 >. runtimeconfig.json</li><li>web.config (IIS 배포)</li></ul></li></ul> |
| [자체 포함된 배포](/dotnet/core/deploying/#self-contained-deployments-scd) | <ul><li>publish&dagger;<ul><li>로그&dagger; (stdout 로그를 받을 수 필요로 하지 않는 경우 선택 사항)</li><li>refs&dagger;</li><li>뷰&dagger; (MVC 앱; 뷰 아닌 미리 컴파일하는 경우)</li><li>페이지&dagger; (MVC 또는 Razor 페이지 앱; 페이지가 아닌 미리 컴파일하는 경우)</li><li>wwwroot&dagger;</li><li>\*.dll 파일</li><li>\<어셈블리 이름 >. deps.json</li><li>\<어셈블리 이름 >.exe</li><li>\<어셈블리 이름 >.pdb</li><li>\<어셈블리 이름 >. PrecompiledViews.dll</li><li>\<어셈블리 이름 >. PrecompiledViews.pdb</li><li>\<어셈블리 이름 >. runtimeconfig.json</li><li>web.config (IIS 배포)</li></ul></li></ul> |

&dagger;디렉터리를 나타냅니다.

*게시* 디렉터리를 나타냅니다는 *콘텐츠 루트 경로*라고도 하는 *응용 프로그램 기본 경로*를 배포 합니다. 에 원하는 이름이 지정 됩니다는 *게시* 서버에 배포 된 응용 프로그램의 디렉터리를 해당 위치 역할을 서버의 실제 경로 호스팅된 응용 프로그램입니다.

*wwwroot* 디렉터리에 있는 경우 정적 자산이 포함만 합니다.

stdout *로그* 다음 두 가지 방법 중 하나를 사용 하 여 배포에 대 한 디렉터리를 만들 수 있습니다.

* 다음 추가 `<Target>` 프로젝트 파일에는 요소:

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

   `<MakeDir>` 요소는 빈 만듭니다 *로그* 게시 된 출력에는 폴더입니다. 요소를 사용 하 여는 `PublishDir` 폴더를 만들기 위한 대상 위치를 확인 하는 속성입니다. 웹 배포와 같은 몇 가지 배포 방법, 배포 하는 동안 빈 폴더를 건너뜁니다. `<WriteLinesToFile>` 에 파일을 생성 하는 요소는 *로그* 폴더를이 서버에 폴더의 배포를 보장 합니다. 작업자 프로세스가 대상 폴더에 대 한 쓰기 권한이 하지 않는 경우 폴더 만들기 오류가 여전히 발생할 수 있는 참고 합니다.

* 실제로 만들지는 *로그* 디렉터리는 배포의 서버에 있습니다.

배포 디렉터리에 읽기/Execute 권한이 필요합니다. *로그* 디렉터리에 대 한 읽기/쓰기 권한이 필요 합니다. 추가 디렉터리를이 파일은 읽기/쓰기 권한이 필요 합니다.
