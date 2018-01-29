---
title: "ASP.NET Core 디렉터리 구조"
author: guardrex
description: "게시 된 ASP.NET Core 응용 프로그램의 디렉터리 구조를 참조 하십시오."
ms.author: riande
manager: wpickett
ms.custom: mvc
ms.date: 03/15/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: host-and-deploy/directory-structure
ms.openlocfilehash: 27f0f40aea1c55315642d7d6f9b9d7be3e111cb4
ms.sourcegitcommit: 12e5194936b7e820efc5505a2d5d4f84e88eb5ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/11/2018
---
# <a name="directory-structure-of-published-aspnet-core-apps"></a>게시 된 ASP.NET Core 응용 프로그램의 디렉터리 구조

[Luke Latham](https://github.com/guardrex)으로

ASP.NET Core, 응용 프로그램 디렉터리에서에서 *게시*, 응용 프로그램 파일, config 파일, 정적 자산, 패키지 및 런타임 (앱에 대 한 자체 포함)의 구성 됩니다.

| 앱 유형                       | 디렉터리 구조 |
| ------------------------------ | ------------------- |
| 프레임 워크 종속 배포 | <ul><li>publish\*<ul><li>로그\* (publishOptions에 포함 됨) 하는 경우</li><li>refs\*</li><li>런타임\*</li><li>뷰\* (publishOptions에 포함 됨) 하는 경우</li><li>wwwroot\* (publishOptions에 포함 됨) 하는 경우</li><li>.dll 파일</li><li>myapp.deps.json</li><li>myapp.dll</li><li>myapp.pdb</li><li>myapp 합니다. PrecompiledViews.dll (Razor 뷰 미리 컴파일) 하는 경우</li><li>myapp 합니다. PrecompiledViews.pdb (Razor 뷰 미리 컴파일) 하는 경우</li><li>myapp.runtimeconfig.json</li><li>web.config (publishOptions에 포함 됨) 하는 경우</li></ul></li></ul> |
| 자체 포함된 배포      | <ul><li>publish\*<ul><li>로그\* (publishOptions에 포함 됨) 하는 경우</li><li>refs\*</li><li>뷰\* (publishOptions에 포함 됨) 하는 경우</li><li>wwwroot\* (publishOptions에 포함 됨) 하는 경우</li><li>.dll 파일</li><li>myapp.deps.json</li><li>myapp.exe</li><li>myapp.pdb</li><li>myapp 합니다. PrecompiledViews.dll (Razor 뷰 미리 컴파일) 하는 경우</li><li>myapp 합니다. PrecompiledViews.pdb (Razor 뷰 미리 컴파일) 하는 경우</li><li>myapp.runtimeconfig.json</li><li>web.config (publishOptions에 포함 됨) 하는 경우</li></ul></li></ul> |
\*디렉터리를 나타냅니다.

내용을 *게시* 디렉터리 나타냅니다는 *콘텐츠 루트 경로*라고도 하는 *응용 프로그램 기본 경로*, 배포의 합니다. 에 이름이 지정 된는 *게시* 배포에 있는 디렉터리를 해당 위치 역할 호스팅된 응용 프로그램에는 서버의 실제 경로입니다. *wwwroot* 디렉터리에 있는 경우 정적 자산이 포함만 합니다. *로그* 디렉터리를 프로젝트에서 만들고 추가 하 여 배포에 포함 될 수 있습니다는 `<Target>` 요소 아래에 표시 된 프로그램 *.csproj* 파일 또는에 디렉터리를 만들어 물리적으로 서버입니다.

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

배포 디렉터리에 읽기/실행 권한이 필요로 하는 동안는 *로그* 디렉터리에 대 한 읽기/쓰기 권한이 필요 합니다. 자산을 쓸 추가 디렉터리 읽기/쓰기 권한이 필요 합니다.
