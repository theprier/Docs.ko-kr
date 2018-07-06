---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files
title: 'Visual Studio를 사용 하 여 ASP.NET 웹 배포: 배포 추가 파일 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시)에서 실행 중인 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자...
ms.author: aspnetcontent
ms.date: 03/23/2015
ms.assetid: 1cd91055-84bc-42c6-9d80-646f41429d4d
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files
msc.type: authoredcontent
ms.openlocfilehash: 609c0be968e8f38d7be6e5f5c96a569a9a35c2eb
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37820852"
---
<a name="aspnet-web-deployment-using-visual-studio-deploying-extra-files"></a>Visual Studio를 사용 하 여 ASP.NET 웹 배포: Extra Files 배포
====================
[Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> 이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시) Visual Studio 2012 또는 Visual Studio 2010을 사용 하 여 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자입니다. 시리즈에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](introduction.md)합니다.


## <a name="overview"></a>개요

이 자습서에는 Visual Studio 웹 게시를 배포 하는 동안 추가 작업을 수행 하는 파이프라인을 확장 하는 방법을 보여 줍니다. 작업 대상 웹 사이트에 프로젝트 폴더에 없는 추가 파일을 복사 하는 것입니다.

이 자습서에 대 한 하나의 여분 파일 복사: *robots.txt*합니다. 스테이징이 아니라 프로덕션이이 파일을 배포 하려고 합니다. [프로덕션에 배포](deploying-to-production.md) tutorial 프로젝트에이 파일을 추가 하 고 프로덕션에 구성 된 게시 프로필에는 제외 합니다. 이 자습서에서 배포 하려고 하지만 프로젝트에 포함 하지 않으려는 모든 파일에 대 한 유용한 것이 상황을 처리 하는 다른 방법은 볼 수 있습니다.

## <a name="move-the-robotstxt-file"></a>Robots.txt 파일로 이동

처리의 다른 메서드에 대 한 준비가 *robots.txt*, 자습서의이 섹션에서는 프로젝트에 포함 되지 않은 폴더에 파일 이동 및 삭제할 *robots.txt* 준비 환경입니다. 해당 환경에 파일을 배포 하는 새로운 메서드가 제대로 작동 하는지 확인할 수 있도록 준비에서 파일을 삭제 하는 것이 반드시 합니다.

1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 *robots.txt* 파일을 클릭 **프로젝트에서 제외**합니다.
2. 솔루션 폴더에 새 폴더를 만들 Windows 파일 탐색기를 사용 하 고 이름을 *ExtraFiles*합니다.
3. 이동는 *robots.txt* 에서 파일을 *ContosoUniversity* 프로젝트 폴더를 *ExtraFiles* 폴더입니다.

    ![ExtraFiles 폴더](deploying-extra-files/_static/image1.png)
4. FTP 도구를 사용 하 여 삭제 합니다 *robots.txt* 스테이징 웹 사이트에서 파일입니다.

    선택할 수 있습니다 **대상에서 추가 파일 제거** 아래에서 **파일 게시 옵션** 에 **설정** 스테이징 게시 프로필의 탭 및 스테이징에 다시 게시 합니다.

## <a name="update-the-publish-profile-file"></a>게시 프로필 파일 업데이트

하기만 하면 *robots.txt* 스테이징 배포를 업데이트 해야 할 유일한 게시 프로필은 준비 하도록 합니다.

1. Visual Studio에서 엽니다 *Staging.pubxml*합니다.
2. 닫기 전에 파일의 끝 `</Project>` 태그, 다음 태그를 추가 합니다.

    [!code-xml[Main](deploying-extra-files/samples/sample1.xml)]

    이 코드를 만듭니다 *대상* 는 배포할 추가 파일을 수집 합니다. MSBuild를 실행 하는 더 많은 작업 기반 지정한 조건으로 또는 대상 하나 구성 됩니다.

    합니다 `Include` 특성은 파일을 찾을 폴더 지정 *ExtraFiles*프로젝트 폴더와 동일한 수준에 있는 합니다. MSBuild 해당 폴더를 재귀적으로 하위 폴더 (double 별표는 하위 폴더를 지정 하는 데 사용)에서 모든 파일을 수집 합니다. 이 코드를 사용 하 여 배치할 수 있습니다 여러 파일 및 파일 내의 하위 폴더에는 *ExtraFiles* 폴더 및 모든 배포 됩니다.

    합니다 `DestinationRelativePath` 폴더 및 파일 복사 되어야 함을 동일한 파일 및 폴더 구조에서 대상 웹 사이트의 루트 폴더에 있는 대로 요소를 지정 합니다 *ExtraFiles* 폴더입니다. 복사 하려는 경우는 *ExtraFiles* 자체 폴더를 `DestinationRelativePath` 값 *ExtraFiles\%(RecursiveDir)%(Filename)%(Extension)* 합니다.
3. 닫기 전에 파일의 끝 `</Project>` 태그, 새 대상을 실행 하는 시기를 지정 하는 다음 태그를 추가 합니다.

    [!code-xml[Main](deploying-extra-files/samples/sample2.xml)]

    이 코드를 사용 하면 새 `CustomCollectFiles` 대상 폴더로 파일을 복사 하는 대상 실행 될 때마다 실행 될 대상입니다. 별도 대상 배포 패키지 만들기 및 게시 하 고 게시 하는 대신 배포 패키지를 사용 하 여 배포 하려는 경우 새 대상 모두 대상으로 주입 합니다.

    합니다 *.pubxml* 파일은 이제 다음과 같습니다.

    [!code-xml[Main](deploying-extra-files/samples/sample3.xml?highlight=53-71)]
4. 저장 후 닫기 합니다 *Staging.pubxml* 파일입니다.

## <a name="publish-to-staging"></a>스테이징 게시

한 번의 클릭을 사용 하 여 게시 또는 명령줄 스테이징 프로필을 사용 하 여 응용 프로그램을 게시 합니다.

한 번의 클릭을 사용 하는 경우 게시에서 확인할 수 있습니다 합니다 **미리 보기** 창입니다 *robots.txt* 복사 됩니다. 이 고, 그렇지 FTP 도구를 사용 하 여 확인 합니다 *robots.txt* 배포 후 웹 사이트의 루트 폴더에 파일을 합니다.

## <a name="summary"></a>요약

이 타사 호스팅 공급자에 ASP.NET 웹 응용 프로그램에 대 한 자습서이 시리즈를 마칩니다. 이 자습서에서 다루는 항목에 대 한 자세한 내용은 참조는 [ASP.NET 배포 콘텐츠 맵](https://go.microsoft.com/fwlink/p/?LinkId=282413)합니다.

## <a name="more-information"></a>추가 정보

MSBuild 파일을 사용 하는 방법의 이름을 알고 있는 경우에 코드를 작성 하 여 다른 많은 배포 작업을 자동화할 수 있습니다 *.pubxml* (프로필 관련 작업용) 파일 또는 프로젝트 *. wpp.targets* 파일 (태스크는 모든 프로필에 적용). 에 대 한 자세한 내용은 *.pubxml* 하 고 *. wpp.targets* 파일을 참조 하세요 [방법: 게시 프로필 (.pubxml) 파일에서 배포 설정을 편집 및. wpp.targets Visual Studio 웹에서 파일 프로젝트](https://msdn.microsoft.com/library/ff398069)합니다. MSBuild 코드에 대 한 기본적인 소개를 참조 하세요 **프로젝트 파일의 분석** 에 [엔터프라이즈 배포 시리즈: 프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)합니다. 고유한 시나리오에 대 한 작업을 수행 하는 MSBuild 파일을 사용 하는 방법에 알아보려면이 설명서를 참조 하세요.: [Microsoft 빌드 엔진 내:를 사용 하 여 MSBuild 및 Team Foundation Build](http://msbuildbook.com) Sayed Ibraham Hashimi William Bartholomew 하 합니다.

## <a name="acknowledgements"></a>감사의 글

이 자습서 시리즈의 콘텐츠에 중요 한 기여를 수행한 다음 사용자를 감사 하려고 합니다.

- [Alberto Poblacion, MVP &amp; MCT, 스페인](https://mvp.microsoft.com/mvp/Alberto%20Poblacion%20Bolano-36772)
- 데이터 플랫폼 개발 MVP Jarod Ferguson United States
- Harsh Mittal, Microsoft
- [Jon Galloway](https://weblogs.asp.net/jgalloway) (twitter: [ @jongalloway ](http://twitter.com/jongalloway))
- [Kristina Olson, Microsoft](https://blogs.iis.net/krolson/default.aspx)
- [Mike 되, Microsoft](http://www.mikepope.com/blog/DisplayBlog.aspx)
- Mohit Srivastava, Microsoft
- [Raffaele Rialdi 이탈리아](http://www.iamraf.net/)
- [Rick Anderson, Microsoft](https://blogs.msdn.com/b/rickandy/)
- [Sayed Hashimi, Microsoft](http://sedodream.com/default.aspx)(twitter: [ @sayedihashimi ](http://twitter.com/sayedihashimi))
- [Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [ @shanselman ](http://twitter.com/shanselman))
- [Scott Hunter, Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [ @coolcsh ](http://twitter.com/coolcsh))
- [Srđan Božović, 세르비아](http://msforge.net/blogs/zmajcek/)
- [인 Vishal Joshi, Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [ @vishalrjoshi ](http://twitter.com/vishalrjoshi))

> [!div class="step-by-step"]
> [이전](command-line-deployment.md)
> [다음](troubleshooting.md)
