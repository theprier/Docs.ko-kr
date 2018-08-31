---
title: Visual Studio에서 ASP.NET Core와 함께 사용 하 여 LibMan
author: scottaddie
description: LibMan Visual Studio를 사용 하 여 ASP.NET Core 프로젝트에서 사용 하는 방법에 알아봅니다.
ms.author: scaddie
ms.custom: mvc
ms.date: 08/20/2018
uid: client-side/libman/libman-vs
ms.openlocfilehash: a653b1a5c07feca8672ba38e0cda3ddc30482c5a
ms.sourcegitcommit: ecf2cd4e0613569025b28e12de3baa21d86d4258
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43312181"
---
# <a name="use-libman-with-aspnet-core-in-visual-studio"></a>Visual Studio에서 ASP.NET Core와 함께 사용 하 여 LibMan

작성자: [Scott Addie](https://twitter.com/Scott_Addie)

Visual Studio는 기본 제공 [LibMan](xref:client-side/libman/index) 포함 하 여 ASP.NET Core 프로젝트에서:

* 구성 하 고 빌드 시 LibMan 복원 작업 실행을 지원 합니다.
* LibMan 복원 및 정리 작업을 트리거하기 위한 메뉴 항목입니다.
* 라이브러리를 찾고 파일을 프로젝트에 추가 하기 위한 검색 대화 상자입니다.
* 편집에 대 한 지원과 *libman.json*&mdash;LibMan 매니페스트 파일.

[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/client-side/libman/samples/) [(다운로드 하는 방법)](xref:tutorials/index#how-to-download-a-sample)

## <a name="prerequisites"></a>전제 조건

* Visual Studio 2017 버전 15.8 이상 합니다 **ASP.NET 및 웹 개발** 워크 로드

## <a name="add-library-files"></a>라이브러리 파일 추가

라이브러리 파일은 두 가지 방법으로 ASP.NET Core 프로젝트에 추가할 수 있습니다.

1. [클라이언트 쪽 라이브러리 추가 대화 상자를 사용 합니다.](#use-the-add-client-side-library-dialog)
1. [LibMan 매니페스트 파일 항목을 수동으로 구성](#manually-configure-libman-manifest-file-entries)

### <a name="use-the-add-client-side-library-dialog"></a>클라이언트 쪽 라이브러리 추가 대화 상자를 사용 합니다.

클라이언트 쪽 라이브러리를 설치 하려면 다음이 단계를 수행 합니다.

* **솔루션 탐색기**, 파일을 추가 해야 합니다는 프로젝트 폴더를 마우스 오른쪽 단추로 클릭 합니다. 선택할 **추가할** > **클라이언트 쪽 라이브러리**합니다. 합니다 **클라이언트 쪽 라이브러리 추가** 대화 상자가 나타납니다.

  ![추가 클라이언트 쪽 라이브러리 대화 상자](_static/add-library-dialog.png)

* 라이브러리 공급자를 선택 합니다 **공급자** 드롭다운 합니다. CDNJS 기본 공급자입니다.
* 형식 라이브러리 이름 대로 인출 하는 **라이브러리** 입력란입니다. IntelliSense는 제공된 된 텍스트를 사용 하 여 시작 하는 라이브러리의 목록을 제공 합니다.
* IntelliSense 목록에서 라이브러리를 선택 합니다. 라이브러리 이름이 붙습니다 통지를 `@` 기호 및 선택한 공급자에 게 알려진 안정적인 최신 버전입니다.
* 포함할 파일을 결정 합니다.
  * 선택 된 **모든 라이브러리 파일을 포함** 라디오 단추를 포함 하는 모든 라이브러리의 파일입니다.
  * 선택 된 **특정 파일 선택** 라이브러리의 파일 하위 집합을 포함 하려면 라디오 단추입니다. 라디오 단추를 선택 하 고, 파일 선택기 트리에 사용 됩니다. 다운로드 파일 이름의 왼쪽에 있는 확인란을 선택 합니다.
* 파일을 저장 하는 것에 대 한 프로젝트 폴더를 지정 합니다 **대상 위치** 입력란입니다. 권장 구성으로 각 라이브러리를 별도 폴더에 저장 합니다.

  제안 **대상 위치** 폴더 대화 상자 시작 된 위치를 기반으로 합니다.

  * 프로젝트 루트에서 시작:
    * *wwwroot/lib* 경우에 사용 됩니다 *wwwroot* 존재 합니다.
    * *lib* 경우에 사용 됩니다 *wwwroot* 존재 하지 않습니다.
  * 프로젝트 폴더에서 시작 하는 경우에 해당 폴더 이름이 사용 됩니다.

  폴더 제안 라이브러리 이름이 붙습니다. 다음 표에서 Razor 페이지 프로젝트에 jQuery를 설치 하는 경우 폴더 제안을 보여 줍니다.
  
  |시작 위치                           |제안 된 폴더      |
  |------------------------------------------|----------------------|
  |프로젝트 루트 (하는 경우 *wwwroot* 존재)        |*jquery/wwwroot/lib /* |
  |프로젝트 루트 (하는 경우 *wwwroot* 존재 하지 않는) |*lib/jquery /*         |
  |*페이지* 프로젝트의 폴더                 |*페이지/jquery /*       |

* 클릭 합니다 **설치** 에서 구성에 따라 파일을 다운로드 하려면 단추 *libman.json*합니다.
* 검토 합니다 **라이브러리 관리자** 의 피드 합니다 **출력** 설치 세부 정보 창. 예를 들어:

  ```console
  Restore operation started...
  Restoring libraries for project LibManSample
  Restoring library jquery@3.3.1... (LibManSample)
  wwwroot/lib/jquery/jquery.min.js written to destination (LibManSample)
  wwwroot/lib/jquery/jquery.js written to destination (LibManSample)
  wwwroot/lib/jquery/jquery.min.map written to destination (LibManSample)
  Restore operation completed
  1 libraries restored in 2.32 seconds
  ```

### <a name="manually-configure-libman-manifest-file-entries"></a>LibMan 매니페스트 파일 항목을 수동으로 구성

Visual Studio에서 모든 LibMan 작업은 프로젝트 루트의 LibMan 매니페스트의 내용에 따라 (*libman.json*). 수동으로 편집할 수 있습니다 *libman.json* 프로젝트에 대 한 라이브러리 파일을 구성 합니다. Visual Studio 모든 라이브러리 파일을 한 번 복원 *libman.json* 저장 됩니다.

열려는 *libman.json* 편집을 위해 다음 옵션 존재 합니다.

* 두 번 클릭 합니다 *libman.json* 파일 **솔루션 탐색기**합니다.
* 프로젝트를 마우스 오른쪽 단추로 클릭 **솔루션 탐색기** 선택한 **클라이언트 쪽 라이브러리 관리**합니다. **&#8224;**
* 선택 **클라이언트 쪽 라이브러리 관리** Visual studio에서 **프로젝트** 메뉴. **&#8224;**

**&#8224;** 경우는 *libman.json* 파일은 프로젝트 루트에 존재 하지 않는 경우 기본 항목 템플릿 콘텐츠를 사용 하 여 만들어집니다.

Visual Studio는 다양 한 JSON 색 지정 등의 지원 편집, 서식 지정, IntelliSense 및 스키마 유효성 검사를 제공 합니다. LibMan 매니페스트의 JSON 스키마의 위치 [ http://json.schemastore.org/libman ](http://json.schemastore.org/libman)합니다.

LibMan 다음 매니페스트 파일을 사용 하 여에 정의 된 구성에 따라 파일을 검색 합니다 `libraries` 속성입니다. 내에 정의 된 개체 리터럴에서 설명은 `libraries` 따릅니다.

* 하위 집합 [jQuery](https://jquery.com/) 버전 3.3.1 CDNJS 공급자에서 검색 됩니다. 하위 집합에 정의 되어는 `files` 속성&mdash;*jquery.min.js*에 *jquery.js*, 및 *jquery.min.map*합니다. 프로젝트의 파일이 배치 되도록 *wwwroot/lib/jquery* 폴더입니다.
* 전체 [부트스트랩](https://getbootstrap.com/) 4.1.3 버전을 검색 하 고 배치를 *wwwroot/lib/부트스트랩* 폴더입니다. 개체 리터럴의 `provider` 속성 재정의 `defaultProvider` 속성 값입니다. LibMan은 unpkg 공급자에서 부트스트랩 파일을 검색 합니다.
* 하위 집합 [및 Lodash](https://lodash.com/) 조직 내 관리 본문을 승인 합니다. *lodash.js* 하 고 *lodash.min.js* 파일에 로컬 파일 시스템에서 검색 됩니다 *c:\\temp\\및 lodash\\*합니다. 프로젝트의 파일을 복사할 *wwwroot/lib/및 lodash* 폴더입니다.

[!code-json[](samples/LibManSample/libman.json)]

> [!NOTE]
> LibMan는만 각 공급자의 각 라이브러리의 버전을 지원합니다. 합니다 *libman.json* 파일 지정된 된 공급자에 대 한 라이브러리 이름이 같은 두 라이브러리가 포함 된 경우 스키마 유효성 검사에 실패 합니다.

## <a name="restore-library-files"></a>라이브러리 파일 복원

Visual Studio 내에서 라이브러리 파일을 복원 하려면 있어야 유효한 *libman.json* 프로젝트 루트에 있는 파일입니다. 복원 된 파일은 각 라이브러리에 대해 지정 된 위치에서 프로젝트에 배치 됩니다.

두 가지 방법으로 ASP.NET Core 프로젝트에서 라이브러리 파일을 복원할 수 있습니다.

1. [빌드 중 파일을 복원 합니다.](#restore-files-during-build)
1. [파일을 수동으로 복원](#restore-files-manually)

### <a name="restore-files-during-build"></a>빌드 중 파일을 복원 합니다.

LibMan 빌드 프로세스의 일부로 정의 된 라이브러리 파일을 복원할 수 있습니다. 기본적으로 *빌드 시 복원* 동작을 사용 하지 않도록 설정 합니다.

사용 하도록 설정 하 고 빌드 시 복원 동작을 테스트 합니다.

* 마우스 오른쪽 단추로 클릭 *libman.json* 에 **솔루션 탐색기** 선택한 **빌드 시 복원 클라이언트 쪽 라이브러리를 사용 하도록 설정** 상황에 맞는 메뉴입니다.
* 클릭 합니다 **예** NuGet 패키지를 설치 하 라는 메시지가 나타나면 단추입니다. 합니다 [Microsoft.Web.LibraryManager.Build](https://www.nuget.org/packages/Microsoft.Web.LibraryManager.Build/) NuGet 패키지를 프로젝트에 추가 됩니다.

  [!code-xml[](samples/LibManSample/LibManSample.csproj?name=snippet_RestoreOnBuildPackage)]

* LibMan 파일 복원이 수행 되는 확인 하려면 프로젝트를 빌드하십시오. `Microsoft.Web.LibraryManager.Build` 패키지 LibMan 프로젝트의 빌드 작업 중 실행 되는 MSBuild 대상을 삽입 합니다.
* 검토 합니다 **빌드** 의 피드 합니다 **출력** LibMan 활동 로그 창:

  ```console
  1>------ Build started: Project: LibManSample, Configuration: Debug Any CPU ------
  1>
  1>Restore operation started...
  1>Restoring library jquery@3.3.1...
  1>Restoring library bootstrap@4.1.3...
  1>
  1>2 libraries restored in 10.66 seconds
  1>LibManSample -> C:\LibManSample\bin\Debug\netcoreapp2.1\LibManSample.dll
  ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
  ```

빌드 시 복원 동작을 사용 하는 경우는 *libman.json* 상황에 맞는 메뉴 표시를 **빌드 시 복원 클라이언트 쪽 라이브러리 사용 안 함** 옵션입니다. 이 옵션을 선택 하면 제거를 `Microsoft.Web.LibraryManager.Build` 패키지는 프로젝트 파일에서 참조 합니다. 따라서 클라이언트 쪽 라이브러리는 더 이상 각 빌드에 복원 됩니다.

빌드 시 복원 설정에 관계 없이 수동으로 복원한에서 언제 든 지 합니다 *libman.json* 상황에 맞는 메뉴입니다. 자세한 내용은 [파일을 수동으로 복원](#restore-files-manually)합니다.

### <a name="restore-files-manually"></a>파일을 수동으로 복원

파일을 수동으로 복원할 라이브러리:

* 솔루션의 모든 프로젝트:
  * 솔루션 이름을 마우스 오른쪽 단추로 클릭 **솔루션 탐색기**합니다.
  * 선택 된 **클라이언트 쪽 라이브러리 복원** 옵션입니다.
* 특정 프로젝트:
  * 마우스 오른쪽 단추로 클릭 합니다 *libman.json* 파일 **솔루션 탐색기**합니다.
  * 선택 된 **클라이언트 쪽 라이브러리 복원** 옵션입니다.

복원 작업이 실행 하는 동안:

* 작업 상태 센터 (TSC) Visual Studio 상태 표시줄에 애니메이션이 적용 될 아이콘과 읽을지를 *복원 작업이 시작*합니다. 아이콘을 클릭 하는 알려진된 백그라운드 작업을 나열 하는 도구 설명이 열립니다.
* 상태 표시줄에 메시지를 전송할 하며 **라이브러리 관리자** 의 피드 합니다 **출력** 창입니다. 예를 들어:

  ```console
  Restore operation started...
  Restoring libraries for project LibManSample
  Restoring library jquery@3.3.1... (LibManSample)
  wwwroot/lib/jquery/jquery.min.js written to destination (LibManSample)
  wwwroot/lib/jquery/jquery.js written to destination (LibManSample)
  wwwroot/lib/jquery/jquery.min.map written to destination (LibManSample)
  Restore operation completed
  1 libraries restored in 2.32 seconds
  ```

## <a name="delete-library-files"></a>라이브러리 파일 삭제

수행 하는 *정리* 이전에 Visual Studio에서 복원 하는 라이브러리 파일을 삭제 하는 작업:

* 마우스 오른쪽 단추로 클릭 합니다 *libman.json* 파일 **솔루션 탐색기**합니다.
* 선택 된 **정리 클라이언트 쪽 라이브러리** 옵션입니다.

라이브러리가 아닌 파일의 의도 하지 않게 제거를 방지 하려면 정리 작업 전체 디렉터리를 삭제 하지 않습니다. 이전 복원 작업에서 포함 된 파일이 제거 됩니다.

정리 작업 실행 하는 동안:

* TSC Visual Studio 상태 표시줄에 애니메이션이 적용 될 아이콘과 읽을지를 *클라이언트 라이브러리 작업을 시작할*합니다. 아이콘을 클릭 하는 알려진된 백그라운드 작업을 나열 하는 도구 설명이 열립니다.
* 상태 표시줄 메시지와 **라이브러리 관리자** 의 피드를 **출력** 창입니다. 예를 들어:

```console
Clean libraries operation started...
Clean libraries operation completed
2 libraries were successfully deleted in 1.91 secs
```

만 정리 작업 프로젝트에서 파일을 삭제합니다. 라이브러리 파일은 이후 복원 작업에서 빠른 검색을 위해 캐시에 남아 있습니다. 로컬 컴퓨터의 캐시에 저장 된 라이브러리 파일을 관리 하려면 사용 합니다 [LibMan CLI](xref:client-side/libman/libman-cli)합니다.

## <a name="uninstall-library-files"></a>라이브러리 파일을 제거

라이브러리 파일을 제거 합니다.

* 오픈 *libman.json*합니다.
* 해당 내부 캐럿 배치 `libraries` 리터럴 개체입니다.
* 왼쪽된 여백에 표시 되는 전구 아이콘을 클릭 하 고 선택 **제거 \<library_name > @\<library_version >**:

  ![라이브러리 상황에 맞는 메뉴 옵션을 제거 합니다.](_static/uninstall-menu-option.png)

또는 수동으로 편집 하 고 저장할 수 LibMan 매니페스트 (*libman.json*). 합니다 [복원 작업](#restore-library-files) 파일을 저장할 때 실행 됩니다. 라이브러리 파일에서 더 이상 정의한 *libman.json* 프로젝트에서 제거 됩니다.

## <a name="update-library-version"></a>라이브러리 버전 업데이트

확인 하려면 업데이트 된 라이브러리 버전:

* 오픈 *libman.json*합니다.
* 해당 내부 캐럿 배치 `libraries` 리터럴 개체입니다.
* 왼쪽된 여백에 표시 되는 전구 아이콘을 클릭 합니다. 마우스로 **업데이트 확인**합니다.

LibMan 설치 된 버전 보다 최신 라이브러리 버전을 확인 합니다. 다음 결과 발생할 수 있습니다.

* A **업데이트를 찾을 수 없는** 최신 버전이 이미 설치 되어 있는 경우 메시지가 표시 됩니다.
* 안정적인 최신 버전은 아직 설치 되지 않으면 표시.

  ![업데이트 상황에 맞는 메뉴 옵션에 대 한 확인](_static/update-menu-option.png)

* 설치 된 버전 보다 최신 시험판 사용 가능한 경우 시험판 버전 표시 됩니다.

이전 라이브러리 버전으로 다운 그레이드 하려면 수동으로 편집 하 여 *libman.json* 파일입니다. 파일 저장 될 경우에 LibMan [복원 작업](#restore-library-files):

* 이전 버전에서 중복 파일을 제거합니다.
* 새 버전에서 새로운 기능과 업데이트 된 파일을 추가합니다.

## <a name="additional-resources"></a>추가 자료

* <xref:client-side/libman/libman-cli>
* [LibMan GitHub 리포지토리](https://github.com/aspnet/LibraryManager)
