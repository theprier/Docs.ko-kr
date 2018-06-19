---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/common-configuration-differences-between-development-and-production-vb
title: 개발 및 프로덕션 (VB) 간의 일반적인 구성 차이 | Microsoft Docs
author: rick-anderson
description: 이전 자습서의 모든 관련 파일을 개발 환경에서 프로덕션 환경에 복사 하 여 웹 사이트를 배포 되었습니다. 그러나 i...
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/01/2009
ms.topic: article
ms.assetid: 548e75f6-4d6c-4cb4-8da8-417915eb8393
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/common-configuration-differences-between-development-and-production-vb
msc.type: authoredcontent
ms.openlocfilehash: 079f6c5a67ec378991ff63694c30e94ed8011bb4
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30889373"
---
<a name="common-configuration-differences-between-development-and-production-vb"></a>개발 및 프로덕션 (VB) 간의 일반적인 구성 차이
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[PDF 다운로드](http://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial05_ConfigDifferences_vb.pdf)

> 이전 자습서의 모든 관련 파일을 개발 환경에서 프로덕션 환경에 복사 하 여 웹 사이트를 배포 되었습니다. 그러나 각 환경 고유한 Web.config 파일을가지고 필요로 하는 환경 구성에 따라 수 거기에 대 한 일반적이 지 않습니다. 이 자습서를 일반적인 구성의 차이 검사 하 고 별도 구성 정보를 유지 관리 하기 위한 전략을 살펴봅니다.


## <a name="introduction"></a>소개


마지막 두 개의 자습서 연습을 통해 간단한 웹 응용 프로그램을 배포 합니다. [ *FTP 클라이언트를 사용 하 여 사이트를 배포* ](deploying-your-site-using-an-ftp-client-vb.md) 자습서에는 독립 실행형 FTP 클라이언트를 사용 하 여 최대 프로덕션 개발 환경에서 필요한 파일을 복사 하는 방법을 배웠습니다. 이전 자습서 [ *배포 Your 사이트를 사용 하 여 Visual Studio*](deploying-your-site-using-visual-studio-vb.md), Visual Studio의 웹 사이트 복사 도구 및 게시 옵션을 사용 하 여 배포에서 조회할 합니다. 두 자습서 프로덕션 환경에서 모든 파일에는 개발 환경에서 파일의 복사본을 했습니다. 그러나와 다를 개발 환경에서 프로덕션 환경에서 구성 파일에 대 한 일반적이 지 않습니다. 웹 응용 프로그램의 구성에 저장 됩니다는 `Web.config` 파일, 일반적으로 데이터베이스, 웹 및 메일 서버 등의 외부 리소스에 대 한 정보를 포함 합니다. 것도 줄이지 않고 처리 되지 않은 예외가 발생할 때 실행 하는 작업 과정 같은 특정 상황에서 응용 프로그램의 동작 합니다.

웹 응용 프로그램을 배포 하는 경우에 올바른 구성 정보는 프로덕션 환경에서 결국 중요 합니다. 대부분의 경우에는 `Web.config` 개발 환경에서 파일을 프로덕션 환경으로 복사할 수 없습니다-됩니다. 대신, 사용자 지정 된 버전의 `Web.config` 프로덕션 환경으로 업로드 해야 합니다. 이 자습서에서는 몇 가지 일반적인 구성 차이점; 살펴봅니다. 또한 환경 간에 서로 다른 구성 정보를 유지 관리 하기 위한 몇 가지 기술을 요약 되어 있습니다.

## <a name="typical-configuration-differences-between-the-development-and-production-environments"></a>개발 및 프로덕션 환경에서의 일반적인 구성 차이점

`Web.config` 파일 다양 한 ASP.NET 응용 프로그램에 대 한 구성 정보를 포함 합니다. 이 구성 정보 중 일부는 환경에 관계 없이 동일 합니다. 예를 들어, 인증 설정과 URL 권한 부여 규칙에 명시 된 `Web.config` 파일의 `<authentication>` 및 `<authorization>` 요소는 일반적으로 환경에 관계 없이 동일 합니다. 하지만-외부 리소스에 대 한 정보 등의 다른 구성 정보가-일반적으로 환경에 따라 다릅니다.

데이터베이스 연결 문자열은 환경에 따라 다른 구성 정보의 가장 대표적인 예입니다. 한 연결을 먼저 설정 해야를 통해 작업을 수행 하 고 웹 응용 프로그램 데이터베이스 서버와 통신 하면는 [연결 문자열](http://www.connectionstrings.com/Articles/Show/what-is-a-connection-string)합니다. 웹 페이지 또는 데이터베이스에 연결 하는 코드에서 직접 데이터베이스 연결 문자열이 하드 코딩 하는 가능 하지만 것이 좋습니다 배치할 `Web.config`의 [ `<connectionStrings>` 요소](https://msdn.microsoft.com/library/bf7sd233.aspx) 되도록 연결 문자열 정보를 하나의 중앙된 위치입니다. 종종 다른 데이터베이스를 사용 합니다. 개발 하는 동안 프로덕션;에 사용 따라서 연결 문자열 정보는 각 환경에 대해 고유 해야 합니다.

> [!NOTE]
> 이후 자습서 지점을 시작 해 봅니다가 구성 파일에 데이터베이스 연결 문자열을 저장 하는 방법에 대해 구체적으로는 데이터 기반 응용 프로그램 배포를 탐색 합니다.


개발 및 프로덕션 환경의 정상적인된 동작 크게 달라 집니다. 웹 응용 프로그램 개발 환경에서 만들어지고, 테스트 및 디버깅 개발자의 작은 그룹으로 있습니다. 프로덕션 환경에서 서로 다른 많은 동시 사용자가 동일한 응용 프로그램 방문. ASP.NET에 다양 한 개발자가 테스트 및 응용 프로그램 디버깅에 도움이 되는 기능이 포함 되어 있지만 성능과 보안상의 이유로 프로덕션 환경에서 이러한 기능을 비활성화 해야 합니다. 그러한 구성 설정은 몇 가지를 살펴보겠습니다.

### <a name="configuration-settings-that-impact-performance"></a>성능에 영향을 주는 구성 설정

ASP.NET 페이지를 방문 하는 경우 처음으로 (또는 변경 된 후 처음으로)에 대 한 선언적 태그 클래스를 변환 해야 하 고이 클래스를 컴파일해야 합니다. 웹 응용 프로그램 자동 컴파일을 사용 하 여 페이지의 코드 숨김 클래스 너무 컴파일할 수 해야 합니다. 다양 한를 통해 컴파일 옵션을 구성할 수 있습니다는 `Web.config` 파일의 [ `<compilation>` 요소](https://msdn.microsoft.com/library/s10awwz0.aspx)합니다.

Debug 특성은에서 가장 중요 한 특성 중 하나는 `<compilation>` 요소입니다. 경우는 `debug` 특성이 컴파일된 어셈블리는 Visual Studio에서 응용 프로그램을 디버깅할 때 필요한 디버그 기호를 포함 한 다음 "true"로 설정 되어 있습니다. 하지만 디버그 기호는 어셈블리의 크기가 증가 하 고 코드를 실행 하는 경우 추가 메모리 요구 사항이 적용 됩니다. 또한 때는 `debug` 특성에서 반환 된 모든 콘텐츠를 "true"로 설정 되어 `WebResource.axd` 은 캐시 되지 있는지 될 때마다 사용자가 방문에서 반환 된 정적 콘텐츠를 다시 다운로드 해야 합니다는 페이지 `WebResource.axd`합니다.

> [!NOTE]
> `WebResource.axd` HTTP 처리기를 기본 제공 ASP.NET 2.0에서 도입 서버 컨트롤 사용 하 여 스크립트 파일, 이미지, CSS 파일 및 기타 콘텐츠 등의 포함된 리소스를 검색 하는입니다. 방법에 대 한 자세한 내용은 `WebResource.axd` 작동 하며 사용 하 여 사용자 지정 서버 컨트롤에서 포함된 리소스를 액세스 하는 방법을 참조 [액세스 포함 된 리소스를 통해 정도 URL 사용 하 여 `WebResource.axd` ](http://aspnet.4guysfromrolla.com/articles/080906-1.aspx)합니다.


`<compilation>` 요소의 `debug` 특성이로 설정 되어 일반적으로 개발 환경에서 "true"입니다. 이 특성을 "true"는 웹 응용 프로그램을 디버깅 하는 데로 설정 해야 하는 사실, Visual Studio에서 ASP.NET 응용 프로그램을 디버깅 하려고 할 경우 및 `debug` 특성이 "false"로 설정 된, Visual Studio 응용 프로그램까지 디버깅할 수 없는 경우 설명 메시지가 표시 됩니다는 `debug` 특성이으로 "true"로 설정 된 이 변경 하려면이 옵션을 제공 합니다.

수행 해야 **되지** 가 `debug` 성능에 미치는 영향 때문에 프로덕션 환경에서 사용 되는 "true"로 특성이 설정 합니다. 에 대 한 보다 철저 한 내용은이 항목을 참조 [Scott Guthrie](https://weblogs.asp.net/scottgu/)의 블로그 게시물 [없습니다 실행 프로덕션 ASP.NET 응용 프로그램으로 `debug="true"` Enabled](https://weblogs.asp.net/scottgu/442448)합니다.

### <a name="custom-errors-and-tracing"></a>사용자 지정 오류 및 추적

ASP.NET 응용 프로그램에서 처리 되지 않은 예외가 발생할 때 다음 세 가지 중 하나가 발생 시점 런타임에 버블링:

- 일반 런타임 오류 메시지가 표시 됩니다. 이 페이지에서는 사용자를 런타임 오류가 발생 했지만 오류에 대 한 정보를 제공 하지 않는 알립니다.
- 방금 throw 된 예외에 대 한 정보를 포함 하는 예외 세부 정보 메시지가 표시 됩니다.
- 원하는 모든 메시지를 표시 하는 ASP.NET 페이지를 만들면 되는 사용자 지정 오류 페이지가 표시 됩니다.

에 따라 달라 집니다 처리 되지 않은 예외가 발생할 때 어떤 일이 생기는 `Web.config` 파일의 [ `<customErrors>` 섹션](https://msdn.microsoft.com/library/h0hfz6fc.aspx)합니다.

개발 및 응용 프로그램을 테스트할 때 브라우저에서 모든 예외에 대 한 세부 정보를 볼 수 있습니다. 그러나 보안상 위험할은 프로덕션에서 응용 프로그램에 예외 정보를 표시 합니다. 또한 flattering 아니며 비 전문적으로 보이는 웹 사이트를 만듭니다. 이상적으로 처리 되지 않은 예외가 발생할 경우 개발 환경에서 웹 응용 프로그램 예외의 세부 정보가 표시 됩니다 동안 프로덕션 환경에서 동일한 응용 프로그램 사용자 지정 오류 페이지에 표시 됩니다.

> [!NOTE]
> 기본 `<customErrors>` 섹션 설정이 예외 세부 정보 페이지를 통해 로컬 호스트를 방문 하 그렇지 않은 경우 제네릭 런타임 오류 페이지를 표시 하는 경우에 메시지를 표시 합니다. 이 방식이 적절 아니지만 기본 동작은 로컬이 아닌 방문자에 게 예외 정보를 표시 되지 않으며 알아야 보장 됩니다. 검사 하는 이후 자습서에서 `<customErrors>` 단원에서 자세히 및 프로덕션 환경에서 오류가 발생할 때 표시 된 사용자 지정 오류 페이지를 사용 하는 방법을 보여 줍니다.


개발 중에 유용한 ASP.NET 기능을 다른 추적입니다. 추적을 사용 하도록 설정 하는 경우 들어오는 각 요청에 대 한 정보를 기록 하 고는 특별 한 웹 페이지를 제공 `Trace.axd`, 최근 요청 세부 정보를 보기 위한 합니다. 켜고를 통해 추적을 구성할 수 있습니다는 [ `<trace>` 요소](https://msdn.microsoft.com/library/6915t83k.aspx) 에서 `Web.config`합니다.

사용 하도록 설정 하면 추적 확인 있는지 프로덕션 환경에서 비활성화 되어 있습니다. 추적 정보는 쿠키, 세션 데이터 및 기타 잠재적으로 중요 한 정보를 포함 하기 때문에는 프로덕션 환경에서 추적을 사용 하지 않도록 설정 해야 합니다. 다행 스럽게도, 기본적으로 추적 해제 되었음 및 `Trace.axd` 파일은 로컬 호스트를 통해 액세스할 수만 있습니다. 개발에서 이러한 기본 설정을 변경 하는 경우는 해제 다시 프로덕션 환경에 있는지 확인 합니다.

## <a name="techniques-for-maintaining-separate-configuration-information"></a>기술에 대 한 별도 구성 정보

배포 프로세스 복잡 하 게 개발 및 프로덕션 환경에서 서로 다른 구성 설정이 필요 합니다. 이전 두 자습서에서 배포 프로세스 관계 필요한 파일의 개발에서 프로덕션 환경에 복사 했지만 해당 접근 방식을 구성 정보를 두 환경에서 동일한 경우에 작동 합니다. 다양 한 구성 정보가 포함 된 응용 프로그램 배포에 대 한 기술의 여러 가지가 있습니다. 호스트 된 웹 응용 프로그램에 대 한 이러한 옵션 중 일부를 카탈로그 보겠습니다.

### <a name="manually-deploying-the-production-environment-configuration-file"></a>프로덕션 환경 구성 파일을 수동 배포

가장 간단한 방법은 두 가지 버전의 유지 관리 하는 `Web.config` 파일: 개발 환경 및 프로덕션 환경에 대 한 하나 있습니다. 개발 환경에서 프로덕션 서버로 복사 하는 모든 파일에 수반 되는 사이트를 프로덕션 배포 *제외 하 고* 에 대 한는 `Web.config` 파일입니다. 대신, 프로덕션 환경 관련 `Web.config` 프로덕션에 파일을 복사 합니다.

이 방법은 매우 정교한 이지만 구성 정보는 자주 변경 되기 때문에 구현 하는 것이 쉽습니다. 응용 프로그램의 작은 개발 팀과 함께 단일 웹 서버에서 호스팅되는 구성 정보를 가져올 자주 변경 및 가장 잘을 작동 합니다. 독립 실행형 FTP 클라이언트를 사용 하 여 응용 프로그램 파일을 수동으로 배포 하는 경우 가장 해 됩니다. 먼저 배포 관련을 교체 해야 Visual Studio의 웹 사이트 복사 도구 또는 게시 옵션을 사용 하는 경우 `Web.config` 를 배포 하기 전에 프로덕션 관련 항목으로 파일을 다음 배포가 완료 된 후 교체 합니다.

### <a name="change-the-configuration-during-the-build-or-deployment-process"></a>빌드 또는 배포 프로세스 중에 구성을 변경 합니다.

토론 지금까지 독자를 대상으로 임시 빌드 및 배포 프로세스입니다. 대부분의 큰 소프트웨어 프로젝트 오픈 소스 홈 재배 또는 타사 도구 활용 하는 프로세스를 공식화 더 있어야 합니다. 이러한 프로젝트에 대 한 가능성이 프로덕션 밀어넣기됩니다 전에 구성 정보를 적절 하 게 수정 하는 빌드 또는 배포 프로세스를 지정할 수 있습니다. 사용 하 여 웹 응용 프로그램을 작성 하는 경우 [MSBuild](http://en.wikipedia.org/wiki/MSBuild), [코 버 넌 트](http://nant.sourceforge.net/), 또는 다른 빌드 도구를 추가할 수 있습니다 가능성이 빌드 단계를 수정 하는 `Web.config` 파일 프로덕션 전용 설정을 포함 하도록 합니다. 프로그래밍 방식으로 소스 제어 서버에 연결 하 고 적절 한 검색할 수 없습니다 배포 워크플로 또는 `Web.config` 파일입니다.

실제 프로덕션 환경에 적절 한 구성 정보를 가져오는 방법을 도구 및 워크플로에 따라 크게 달라 집니다. 이와 같이 하지 설명을이 항목을 추가 합니다. MSBuild 또는 코 버 넌 트와 같은 인기 있는 빌드 도구를 사용 하는 경우 찾을 수 있습니다 배포 문서와 자습서 웹 검색을 통해 이러한 도구에 특정 합니다.

### <a name="managing-configuration-differences-via-the-web-deployment-project-add-in"></a>추가 기능을 통해 웹 배포 구성의 차이 관리 프로젝트

2006 년에서 Microsoft는 Visual Studio 2005 용 웹 개발 프로젝트에서 추가 기능 릴리스. Visual Studio 2008에 대 한 추가 기능을 2008에 출시 되었습니다. 이 추가 기능을 ASP.NET 개발자에 게 빌드 시 해당 웹 응용 프로그램 프로젝트와 함께 별도 웹 배포 프로젝트를 만들 수 있습니다, 그리고 명시적으로 웹 응용 프로그램을 컴파일 및 로컬 출력 디렉터리에 배포할 파일을 복사 합니다. 웹 응용 프로그램 프로젝트 원리를 자세히 파악할수록 MSBuild를 사용합니다.

기본적으로 개발 환경의 `Web.config` 파일은 출력 디렉터리에 복사 되지만 사용자 지정 하는 웹 배포 프로젝트를 설정할 수 있습니다.는

다음과 같은 방법으로이 디렉터리에 복사 하는 구성 정보:

- 통해 `Web.config` 파일 섹션 교체를 바꿀 섹션을 지정할 수 있는 및 바꿀 텍스트를 포함 하는 XML 파일입니다.
- 외부 구성 원본 파일 경로 제공 합니다. 이 옵션을 선택 하면 웹 배포 프로젝트는 특정 복사 `Web.config` 출력 디렉터리에 파일 (보다는 `Web.config` 개발 환경에서 사용 되는 파일).
- 웹 배포 프로젝트에서 사용 되는 MSBuild 파일을 사용자 지정 규칙을 추가 하 여 합니다.

웹 배포 응용 프로그램 웹 배포 프로젝트를 빌드한 다음 프로덕션 환경에는 프로젝트의 출력 폴더에서 파일을 복사 합니다.

확인 웹 배포 프로젝트를 사용 하 여에 대 한 자세한 내용을 보려면 [웹 배포 프로젝트 여기서](https://msdn.microsoft.com/magazine/cc163448.aspx) 의 2007 년 4 월 문제에서 [MSDN Magazine](https://msdn.microsoft.com/magazine/default.aspx)에 추가 정보 섹션에서 링크를 참조 하거나는 이 자습서의 끝입니다.

> [!NOTE]
> 웹 배포 프로젝트로는 Visual Studio 추가 기능에 구현 되 고 Visual Studio Express Edition (Visual Web Developer 포함) 추가 기능을 지원 하지 않는 때문에 Visual Web Developer에 웹 배포 프로젝트를 사용할 수 없습니다.


## <a name="summary"></a>요약

웹 응용 프로그램 개발에서의 동작과 외부 리소스는는 일반적으로 프로덕션 환경에서 동일한 응용 프로그램의 경우 다릅니다. 예를 들어, 데이터베이스 연결 문자열, 컴파일 옵션 및 처리 되지 않은 예외가 발생 하는 일반적으로 할 때 수행할 동작 환경 간에 서로 다릅니다. 배포 프로세스는 이러한 차이 수용 해야 합니다. 이 자습서에서 설명한 대로 프로덕션 환경에는 대체 구성 파일 수동으로 복사 하는 가장 간단한 방법이입니다. 보다 효과적인 솔루션을 만들 수 있습니다. 웹 배포 프로젝트 추가 기능을 사용 하는 경우 또는 이러한 사용자 지정을 사용할 수 있는 더욱 형식화 빌드 또는 배포 프로세스와 합니다.

만족도 매우 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [설명 하는 연결 문자열](http://www.connectionstrings.com/Articles/Show/what-is-a-connection-string)
- [데이터베이스 연결 문자열 @ ConnectionStrings.com](http://www.connectionstrings.com/)
- [프로덕션 ASP.NET 응용 프로그램을 실행 하지 마십시오 `debug="true"` 사용 하도록 설정](https://weblogs.asp.net/scottgu/Don_1920_t-run-production-ASP.NET-Applications-with-debug_3D001D20_true_1D20_-enabled)
- [정상적으로 처리 되지 않은 예외-친숙 한 오류 페이지 표시에 응답](http://aspnet.4guysfromrolla.com/articles/090606-1.aspx)
- [작업 방법: Visual Studio 2008 웹 배포 프로젝트를 사용?](../../../videos/how-do-i/how-do-i-use-a-visual-studio-2008-web-deployment-project.md)
- [데이터베이스를 배포 하는 경우 키 구성 설정](http://aspnet.4guysfromrolla.com/articles/121008-1.aspx)
- [Visual Studio 2008 웹 배포 프로젝트 다운로드](https://www.microsoft.com/downloads/details.aspx?FamilyId=0AA30AE8-C73B-4BDD-BB1B-FE697256C459&amp;displaylang=en) | [Visual Studio 2005 웹 배포 프로젝트 다운로드](https://download.microsoft.com/download/9/4/9/9496adc4-574e-4043-bb70-bc841e27f13c/WebDeploymentSetup.msi)
- [VS 2008 웹 배포 프로젝트](https://weblogs.asp.net/scottgu/archive/2005/11/06/429723.aspx) | [VS 2008 웹 배포 프로젝트 지원 발표](https://weblogs.asp.net/scottgu/archive/2008/01/28/vs-2008-web-deployment-project-support-released.aspx)
- [웹 배포 프로젝트](https://msdn.microsoft.com/magazine/cc163448.aspx)

> [!div class="step-by-step"]
> [이전](deploying-your-site-using-visual-studio-vb.md)
> [다음](core-differences-between-iis-and-the-asp-net-development-server-vb.md)
