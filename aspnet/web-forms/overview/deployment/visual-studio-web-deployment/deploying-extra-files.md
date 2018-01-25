---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files
title: "Visual Studio를 사용 하 여 ASP.NET 웹 배포: 불필요 한 파일이 배포 | Microsoft Docs"
author: tdykstra
description: "이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시) 실행 하 여 웹 응용 프로그램을 Azure 앱 서비스 웹 앱 또는 타사 호스팅 공급자 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/23/2015
ms.topic: article
ms.assetid: 1cd91055-84bc-42c6-9d80-646f41429d4d
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files
msc.type: authoredcontent
ms.openlocfilehash: 46e18ba81c3db8bb04c5cb997bcc1607e4e38bae
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="aspnet-web-deployment-using-visual-studio-deploying-extra-files"></a>Visual Studio를 사용 하 여 ASP.NET 웹 배포: 그 외의 파일 배포
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> 이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시) Visual Studio 2012 또는 Visual Studio 2010을 사용 하 여 웹 응용 프로그램을 Azure 앱 서비스 웹 앱 또는 타사 호스팅 공급자입니다. 계열에 대 한 정보를 참조 하십시오. [시리즈의 첫 번째 자습서](introduction.md)합니다.


## <a name="overview"></a>개요

이 자습서에는 Visual Studio 웹 게시 파이프라인 배포 중에 추가 작업을 수행 하려면 확장 하는 방법을 보여 줍니다. 작업 대상 웹 사이트에 프로젝트 폴더에 없는 추가 파일을 복사 하는 것입니다.

이 자습서에 대 한 하나의 추가 파일을 복사 합니다. *robots.txt*합니다. 이 파일을 준비 속하지만 프로덕션에 배포 하려고 합니다. [프로덕션 환경에 배포](deploying-to-production.md) tutorial 프로젝트에이 파일을 추가 하 고 프로덕션 구성 된 게시 프로필에는 제외 합니다. 이 자습서의 모든 파일을 배포 하려고 하지만 프로젝트에 포함 하지 않을 유용할 것이 상황을 처리 하는 대체 방법을 볼 수 있습니다.

## <a name="move-the-robotstxt-file"></a>Robots.txt 파일 이동

처리는 다른 방법에 대 한 준비 하려면 *robots.txt*, 자습서의이 섹션은 프로젝트에 포함 되지 않은 폴더에 파일 이동 및 삭제 하면 *robots.txt* 스테이징 환경입니다. 해당 환경에 파일을 배포 하는의 새로운 메서드가 제대로 작동 하는지 확인할 수 있도록 준비에서 파일을 삭제 해야 하는 합니다.

1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 *robots.txt* 파일을 클릭 하 여 **프로젝트에서 제외**합니다.
2. Windows 파일 탐색기를 사용 하 여 새 폴더를 솔루션 폴더에 만들고 이름을 *ExtraFiles*합니다.
3. 이동의 *robots.txt* 에서 파일을 *ContosoUniversity* 에 프로젝트 폴더는 *ExtraFiles* 폴더입니다.

    ![ExtraFiles 폴더](deploying-extra-files/_static/image1.png)
4. FTP 도구를 사용 하 여 삭제 된 *robots.txt* 스테이징 웹 사이트에서 파일입니다.

    선택할 수 있습니다 **대상에서 추가 파일 제거** 아래 **파일 게시 옵션** 에 **설정을** 준비 게시 프로필을 탭 하 고 준비를 다시 게시 합니다.

## <a name="update-the-publish-profile-file"></a>업데이트 게시 프로필 파일

하기만 하면 *robots.txt* 를 배포 하기 위해 업데이트 해야 하는 유일한 게시 프로필은 준비 하도록 준비 합니다.

1. Visual Studio에서 열고 *Staging.pubxml*합니다.
2. 닫기 전에 파일의 끝에 `</Project>` 태그에 다음 태그를 추가 합니다.

    [!code-xml[Main](deploying-extra-files/samples/sample1.xml)]

    이 코드에서는 새 *대상* 를 배포할 추가 파일을 수집 합니다. 하나의 구성 됩니다는 MSBuild를 실행 하는 더 많은 작업 지정한 조건에 따라 또는.

    `Include` 특성을 지정 파일을 찾을 수 있는 폴더 *ExtraFiles*프로젝트 폴더와 같은 수준에 있는 합니다. MSBuild는 해당 폴더와 하위 폴더 (이중 별표는 재귀 하위 폴더를 지정 하는 데 사용)로 재귀적으로에서 모든 파일을 수집 합니다. 이 코드로 수 여러 파일 및 파일에에서 넣으면 포함 된 하위 폴더는 *ExtraFiles* 폴더 및 모든 배포 됩니다.

    `DestinationRelativePath` 요소 폴더와 파일 복사 되어야 함을 동일한 파일 및 폴더 구조에는 대상 웹 사이트의 루트 폴더에서 찾을 수는 지정 된 *ExtraFiles* 폴더입니다. 복사 하려는 경우는 *ExtraFiles* 폴더 자체는 `DestinationRelativePath` 번호 값은 *ExtraFiles\%(RecursiveDir)%(Filename)%(Extension)*합니다.
3. 닫기 전에 파일의 끝에 `</Project>` 태그, 새 대상이 실행 하는 시기를 지정 하는 다음 태그를 추가 합니다.

    [!code-xml[Main](deploying-extra-files/samples/sample2.xml)]

    이 코드는 새 `CustomCollectFiles` 대상 대상 폴더에 파일을 복사 하는 대상을 실행 될 때마다 실행 되도록 합니다. 에 대 한 별도 대상 배포 패키지 만들기 및 게시 하 고 게시 하는 대신 배포 패키지를 사용 하 여 배포 하려는 경우 새 대상 대상을 모두에 주입 합니다.

    *.pubxml* 파일은 이제 다음 예제와 같습니다.

    [!code-xml[Main](deploying-extra-files/samples/sample3.xml?highlight=53-71)]
4. 저장 하 고 닫습니다는 *Staging.pubxml* 파일입니다.

## <a name="publish-to-staging"></a>스테이징에 게시

게시 한 번의 클릭을 사용 하 여 또는 명령줄 준비 프로필을 사용 하 여 응용 프로그램을 게시 합니다.

한 번의 클릭을 사용 하는 경우 게시에서 확인할 수 있습니다는 **미리 보기** 창 있는 *robots.txt* 복사 됩니다. 그렇지 않은 경우 FTP 도구를 사용 하 여 확인 하는 *robots.txt* 배포 후 파일은 웹 사이트의 루트 폴더에 있습니다.

## <a name="summary"></a>요약

이 일련의 제 3 자 호스팅 공급자에 ASP.NET 웹 응용 프로그램 배포에 대 한 자습서를 완료 했습니다. 이 자습서에 포함 된 항목 중 하나에 대 한 자세한 내용은 참조는 [ASP.NET 배포 콘텐츠 맵](https://go.microsoft.com/fwlink/p/?LinkId=282413)합니다.

## <a name="more-information"></a>추가 정보

MSBuild 파일을 사용 하는 방법을 알고 있는 경우에 코드를 작성 하 여 다른 많은 배포 작업을 자동화할 수 있습니다 *.pubxml* (프로필 관련 작업)에 대 한 파일 또는 프로젝트 *. wpp.targets* 파일 (하는 태스크 모든 프로필에 적용). 에 대 한 자세한 내용은 *.pubxml* 및 *. wpp.targets* 파일, 참조 [하는 방법: 게시 프로 파일 (.pubxml) 파일에서 배포 설정 편집 및. wpp.targets Visual Studio 웹에서 파일 프로젝트](https://msdn.microsoft.com/library/ff398069)합니다. MSBuild 코드에 대 한 기본적인 소개를 참조 하십시오. **프로젝트 파일의 분석** 에 [엔터프라이즈 배포 시리즈: 프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)합니다. 를 고유한 시나리오에 대 한 작업을 수행 하는 MSBuild 파일을 사용 하는 방법을 확인 하려면이 가이드를 참조 하십시오.: [Microsoft Build Engine 안에: MSBuild를 사용 하 여 및 Team Foundation Build](http://msbuildbook.com) Sayed Ibraham Hashimi 및 William Bartholomew 합니다.

## <a name="acknowledgements"></a>감사의 글

이 자습서 시리즈의 내용에 중요 한 기여를 수행한 다음 사람에 게 감사 하 고 싶습니다.

- [Alberto Poblacion, MVP &amp; MCT, 스페인](https://mvp.microsoft.com/mvp/Alberto%20Poblacion%20Bolano-36772)
- Jarod 퍼거슨, 데이터 플랫폼 개발 MVP United States
- Harsh Mittal, Microsoft
- [Jon Galloway](https://weblogs.asp.net/jgalloway) (twitter: [ @jongalloway ](http://twitter.com/jongalloway))
- [Kristina Olson, Microsoft](https://blogs.iis.net/krolson/default.aspx)
- [Mike Pope, Microsoft](http://www.mikepope.com/blog/DisplayBlog.aspx)
- Mohit Srivastava, Microsoft
- [Raffaele Rialdi 이탈리아](http://www.iamraf.net/)
- [Rick Anderson, Microsoft](https://blogs.msdn.com/b/rickandy/)
- [Sayed Hashimi, Microsoft](http://sedodream.com/default.aspx)(twitter: [ @sayedihashimi ](http://twitter.com/sayedihashimi))
- [Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [ @shanselman ](http://twitter.com/shanselman))
- [Scott 헌터, Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [ @coolcsh ](http://twitter.com/coolcsh))
- [Srđan Božović, 세르비아](http://msforge.net/blogs/zmajcek/)
- [Vishal Joshi, Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [ @vishalrjoshi ](http://twitter.com/vishalrjoshi))

>[!div class="step-by-step"]
[이전](command-line-deployment.md)
[다음](troubleshooting.md)
