---
uid: mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
title: 업그레이드 되었으며 수정 자습서 소개 | Microsoft Docs
author: shanselman
description: 새로운 프레임 워크를 파악 하는 가장 좋은 방법은 다른 구성 요소로 작성 하는 것입니다. 이 자습서는 ASP.NE를 사용 하 여 완료 하지만 크기가 작은 응용 프로그램을 빌드하는 방법을 안내 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: 397522d5-0402-4b94-b810-a2fb564f869d
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
msc.type: authoredcontent
ms.openlocfilehash: 3d925a7dc89fc0c742468653c5c138a0f1d71231
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30868557"
---
<a name="introducing-the-nerddinner-tutorial"></a>업그레이드 되었으며 수정 자습서 소개
====================
으로 [Scott Hanselman](https://github.com/shanselman)

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 새로운 프레임 워크를 파악 하는 가장 좋은 방법은 다른 구성 요소로 작성 하는 것입니다. 이 자습서는 작고 빌드만 ASP.NET MVC 1을 사용 하 여 응용 프로그램을 완료 하는 방법을 안내 하 고 필요한 핵심 개념 중 일부를 소개 합니다.
> 
> ASP.NET MVC 3을 사용 하는 경우 수행한 것이 좋습니다는 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.


## <a name="nerddinner-tutorial"></a>업그레이드 되었으며 수정 자습서

새로운 프레임 워크를 파악 하는 가장 좋은 방법은 다른 구성 요소로 작성 하는 것입니다. 이 자습서는 작고 빌드만 ASP.NET MVC를 사용 하 여 응용 프로그램을 완료 하는 방법을 안내 하 고 필요한 핵심 개념 중 일부를 소개 합니다.

빌드 하려는 응용 프로그램 "업그레이드 되었으며 수정" 라고 합니다. 업그레이드 되었으며 수정 찾고 dinners 온라인을 구성 하는 사용자는 쉬운 방법을 제공 합니다.

![](introducing-the-nerddinner-tutorial/_static/image1.png)

업그레이드 되었으며 수정에는 등록 된 사용자를 만들고 편집 하 고 dinners 삭제할 수 있습니다. 응용 프로그램 간에 일관 된 유효성 검사 및 비즈니스 규칙 집합이 적용합니다.

![](introducing-the-nerddinner-tutorial/_static/image2.png)

방문자는 AJAX 기반 지도 사용 하 여 향후 dinners 근처 보유 하 고 검색할 수 있습니다.

![](introducing-the-nerddinner-tutorial/_static/image3.png)

클릭 하면는 dinner 됩니다으로 이동 세부 정보 페이지에 알아볼 수 있는 더 자세한 정보:

![](introducing-the-nerddinner-tutorial/_static/image4.png)

사이트에 등록 하거나 로그인 하려면 dinner 참석 하려고 경우:

![](introducing-the-nerddinner-tutorial/_static/image5.png)

이벤트 참석자는 AJAX 기반 RSVP 링크를 클릭 한 다음 수 있습니다.:

![](introducing-the-nerddinner-tutorial/_static/image6.png)

![](introducing-the-nerddinner-tutorial/_static/image7.png)

### <a name="implementing-nerddinner"></a>업그레이드 되었으며 수정 구현

파일-를 사용 하 여 업그레이드 되었으며 수정 응용 프로그램을 시작 하겠습니다&gt;새로운 ASP.NET MVC 프로젝트를 만들려면 Visual Studio 내에서 새 프로젝트 명령을 합니다. 그런 다음 증분 기능 및 추가 기능입니다. 방식에 따라 설명 합니다.

1. [새 ASP.NET MVC 프로젝트를 만드는 방법](# "새 ASP.NET MVC 프로젝트 만들기")
2. [데이터베이스를 만드는 방법](# "데이터베이스 만들기")
3. [비즈니스 규칙 유효성 검사를 사용 하 여 모델을 작성 하는 방법](# "비즈니스 규칙 유효성 검사를 사용 하 여 모델 빌드")
4. [등록/정보 UI를 구현 하려면 컨트롤러와 뷰를 사용 하는 방법](# "사용 하 여 컨트롤러와 뷰 목록/세부 정보 UI를 구현 하려면")
5. [CRUD 제공 하는 방법 (만들기, 읽기, 업데이트, 삭제) 데이터 항목 지원 형성](# "제공 CRUD (만들기, 읽기, 업데이트, 삭제) 데이터 형식 항목 지원")
6. [ViewData를 사용 하 고 ViewModel 클래스를 구현 하는 방법](# "ViewData 사용 및 ViewModel 클래스 구현")
7. [마스터 페이지 및 부분을 사용 하 여 UI를 다시 사용 하는 방법을](# "마스터 페이지를 사용 하 여 UI 다시 사용 및 부분")
8. [효율적인 데이터 페이징을 구현 하는 방법을](# "구현 효율적인 데이터 페이징")
9. [인증 및 권한 부여를 사용 하 여 응용 프로그램을 보호 하는 방법](# "보안 응용 프로그램 사용 하 여 인증 및 권한 부여")
10. [AJAX를 사용 하 여 동적 업데이트를 제공 하는 방법](# "동적 업데이트 제공을 사용 하 여 AJAX")
11. [AJAX를 사용 하 여 매핑 시나리오를 구현 하는 방법](# "구현 매핑 시나리오를 사용 하 여 AJAX")
12. [자동화 된 단위 테스트를 사용 하는 방법](# "자동화 된 단위 테스트 설정")

업그레이드 되었으며 수정의 고유 사본을 만들 수 있습니다 각를 완료 하 여 처음부터 단계에서는이 장에서 연습입니다. 여기에 소스 코드의 전체 버전을 다운로드할 수 또는: [GitHub에서 업그레이드 되었으며 수정](https://github.com/AspNetMVPSamples/NerdDinner)합니다. 또한 필요에 따라 수도 있습니다 [이 자습서의 무료 PDF 버전을 다운로드할](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf) 자습서를 오프 라인으로 보려는 경우.

응용 프로그램을 빌드하려면 Visual Studio 2008 또는 무료 Visual Web Developer 2008 Express를 사용할 수 있습니다. 데이터베이스에 대 한 SQL Server 또는 무료 SQL Server Express를 사용할 수 있습니다.

ASP.NET MVC, Visual Web Developer 2008 Express 및 SQL Server Express (모든 사용 가능)의 v 2를 사용 하 여 설치할 수는 [Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)

### <a name="now-lets-get-started"></a>이제 시작 하겠습니다.

이제 업그레이드 되었으며 수정 란 설명한 보겠습니다 우리의 진행할 롤업을 일부 코드를 작성 합니다.

파일-를 사용 하 여 먼저&gt;업그레이드 되었으며 수정 응용 프로그램을 만들려면 Visual Studio 내에서 새 프로젝트.

> [!div class="step-by-step"]
> [다음](create-a-new-aspnet-mvc-project.md)
