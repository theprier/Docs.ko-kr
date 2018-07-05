---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/common-configuration-differences-between-development-and-production-vb
title: 일반적인 구성 차이 개발 및 프로덕션 (VB) | Microsoft Docs
author: rick-anderson
description: 이전 자습서에서 모든 관련 파일을 개발 환경에서 프로덕션 환경으로 복사 하 여 웹 사이트를 배포 했습니다. 그러나 필자는 중...
ms.author: aspnetcontent
ms.date: 04/01/2009
ms.assetid: 548e75f6-4d6c-4cb4-8da8-417915eb8393
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/common-configuration-differences-between-development-and-production-vb
msc.type: authoredcontent
ms.openlocfilehash: 083c07a42fab1f655798f8cfb444ed0e6aa38ff0
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37842807"
---
<a name="common-configuration-differences-between-development-and-production-vb"></a>일반적인 구성 차이 개발 및 프로덕션 (VB)
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[PDF 다운로드](http://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial05_ConfigDifferences_vb.pdf)

> 이전 자습서에서 모든 관련 파일을 개발 환경에서 프로덕션 환경으로 복사 하 여 웹 사이트를 배포 했습니다. 그러나 각 환경에 고유한 Web.config 파일이 있는지 필요로 하는 환경 간의 구성 차이 경우도 흔히 아닙니다. 이 자습서는 일반적인 구성 차이 검사 하 고 별도 구성 정보를 유지 관리 전략을 살펴봅니다.


## <a name="introduction"></a>소개


마지막 두 자습서 연습을 통해 간단한 웹 응용 프로그램을 배포 합니다. 합니다 [ *FTP 클라이언트를 사용 하 여 사이트 배포* ](deploying-your-site-using-an-ftp-client-vb.md) 자습서에는 독립 실행형 FTP 클라이언트를 사용 하 여 프로덕션 개발 환경에서 필요한 파일을 복사 하는 방법을 보여 주었습니다. 이전 자습서 [ *배포 사이트를 사용 하 여 Visual Studio*](deploying-your-site-using-visual-studio-vb.md), Visual Studio의 웹 사이트 복사 도구 및 게시 옵션을 사용 하 여 배포를 살펴보았습니다. 두 자습서에서 프로덕션 환경에서 모든 파일 개발 환경에서 파일의 복사본을 했습니다. 그러나 개발 환경에서 다 프로덕션 환경에서 구성 파일에 대 한 일반적이 지 않은 아닙니다. 에 웹 응용 프로그램의 구성이 저장 되는 `Web.config` 파일을 일반적으로 데이터베이스, 웹 및 전자 메일 서버와 같은 외부 리소스에 대 한 정보를 포함 합니다. 이 또한 줄이지 않고 처리 되지 않은 예외가 발생할 때 수행할 동작의 코스와 같이 특정 상황에서 응용 프로그램의 동작 합니다.

웹 응용 프로그램을 배포 하는 경우 올바른 구성 정보를 프로덕션 환경에서 결국 중요 한 것입니다. 대부분의 경우에는 `Web.config` 프로덕션 환경으로 개발 환경에서 파일을 복사할 수 없습니다-됩니다. 대신 사용자 지정된 버전 `Web.config` 프로덕션으로 업로드 해야 합니다. 이 자습서에 몇 가지 일반적인 구성 차이; 항목을 간략하게 검토 또한 환경 간에 서로 다른 구성 정보를 유지 관리 하기 위한 몇 가지 기술을 요약 되어 있습니다.

## <a name="typical-configuration-differences-between-the-development-and-production-environments"></a>개발 및 프로덕션 환경에서의 일반적인 구성 차이

`Web.config` 파일에는 다양 한 ASP.NET 응용 프로그램에 대 한 구성 정보를 포함 합니다. 이 구성 정보 중 일부는 환경에 관계 없이 동일 합니다. 예를 들어, 인증 설정 및 URL 권한 부여 규칙을 정확 하 게 합니다 `Web.config` 파일의 `<authentication>` 고 `<authorization>` 요소는 일반적으로 환경에 관계 없이 동일 합니다. 하지만 외부 리소스에 대 한 정보 등의 기타 구성 정보-일반적으로 환경에 따라 다릅니다.

데이터베이스 연결 문자열은 환경에 따라 다른 구성 정보의 가장 대표적인 예입니다. 연결을 먼저 설정 해야 하 고를 통해 구현 되는 웹 응용 프로그램을 데이터베이스 서버와 통신할 때를 [연결 문자열](http://www.connectionstrings.com/Articles/Show/what-is-a-connection-string)합니다. 웹 페이지 또는 데이터베이스에 연결 하는 코드에서 직접 데이터베이스 연결 문자열을 하드 코딩할 수 있지만, 것이 좋습니다에 배치할 `Web.config`의 [ `<connectionStrings>` 요소](https://msdn.microsoft.com/library/bf7sd233.aspx) 되도록 연결 문자열 정보는 하나의 중앙된 위치에 있습니다. 종종 다른 데이터베이스는 개발 하는 동안 프로덕션;에서 사용 하는 것 보다 따라서 연결 문자열 정보를 각 환경에 대해 고유 해야 합니다.

> [!NOTE]
> 이후 자습서에서는 데이터 기반 응용 프로그램 배포, 구성 파일에서 데이터베이스 연결 문자열 저장 방법에 대해 구체적으로 알아보겠습니다 이때 살펴봅니다.


개발 및 프로덕션 환경의 의도 한 동작에는 크게 다릅니다. 웹 응용 프로그램 개발 환경에서 만들어지고, 테스트 및 디버깅 개발자의 작은 그룹으로 있습니다. 프로덕션 환경에서 동일한 응용 프로그램에 많은 다른 동시 사용자가 방문 중인 합니다. ASP.NET에 다양 한 개발자가 테스트 및 응용 프로그램을 디버깅할 수 있도록 하는 기능이 포함 되어 있지만 성능 및 보안상의 이유로 프로덕션 환경에서 이러한 기능을 비활성화 해야 합니다. 이러한 몇 가지 구성 설정을 살펴보겠습니다.

### <a name="configuration-settings-that-impact-performance"></a>성능에 영향을 주는 구성 설정

ASP.NET 페이지를 방문 하는 경우 처음으로 (또는 변경 된 후 처음으로)에 대 한 선언적 태그 클래스로 변환 해야 하며이 클래스를 컴파일해야 합니다. 웹 응용 프로그램에 자동 컴파일을 사용 하는 경우 페이지의 코드 숨김 클래스를 너무 컴파일할 수 해야 합니다. 다양 한 컴파일 옵션을 통해 구성할 수 있습니다 합니다 `Web.config` 파일의 [ `<compilation>` 요소](https://msdn.microsoft.com/library/s10awwz0.aspx)합니다.

Debug 특성을 사용 하면 가장 중요 한 특성 중 하나인는 `<compilation>` 요소입니다. 경우는 `debug` 특성이 컴파일된 어셈블리는 Visual Studio에서 응용 프로그램을 디버깅 하는 경우 필요한 디버그 기호를 포함 한 다음 "true"로 설정 됩니다. 그러나 디버그 기호는 어셈블리의 크기가 증가 하 고 코드를 실행 하는 경우 추가 메모리 요구 사항이 적용 됩니다. 또한, 합니다 `debug` 특성에서 반환 된 모든 콘텐츠를 "true"로 설정 되어 `WebResource.axd` 캐시 되지 될 때마다 사용자 방문에서 반환 된 정적 콘텐츠를 다시 다운로드 해야 하는 페이지는 의미 `WebResource.axd`합니다.

> [!NOTE]
> `WebResource.axd` 기본 제공 HTTP 처리기에에서 도입 된 ASP.NET 2.0 스크립트 파일, 이미지, CSS 파일 및 기타 콘텐츠 등의 포함된 리소스를 검색할 서버 컨트롤을 사용 하는 합니다. 하는 방법에 대 한 자세한 내용은 `WebResource.axd` 작동 하 고 사용 하 여 사용자 지정 서버 컨트롤에서 포함 된 리소스에 액세스 하는 방법을 참조 하세요 [액세스 포함 된 리소스를 통해을 사용 하 여 URL `WebResource.axd` ](http://aspnet.4guysfromrolla.com/articles/080906-1.aspx)합니다.


`<compilation>` 요소의 `debug` 특성이 일반적으로로 설정 된 개발 환경에서 "true"입니다. 이 특성을 웹 응용 프로그램을 디버그 하려면 "true"로 설정 해야 실제로 Visual Studio에서 ASP.NET 응용 프로그램을 디버깅 하려고 하며 `debug` 특성이 "false"로 설정 된, Visual Studio에서 응용 프로그램까지 디버깅할 수 없습니다는 설명 메시지를 표시는 `debug` 특성이 고 "true"로 설정 된 이 변경 하려면이 옵션을 제공 합니다.

수행 해야 합니다 **되지** 가 `debug` 성능에 미치는 영향으로 인해 프로덕션 환경에서 사용 되는 "true" 특성이 설정 합니다. 이 항목에 자세한 내용은 참조 [Scott Guthrie](https://weblogs.asp.net/scottgu/)의 블로그 게시물 [하지 실행 프로덕션 ASP.NET 응용 프로그램 사용 하 여 `debug="true"` 사용](https://weblogs.asp.net/scottgu/442448)합니다.

### <a name="custom-errors-and-tracing"></a>사용자 지정 오류 및 추적

ASP.NET 응용 프로그램에서 처리 되지 않은 예외가 발생 하면 런타임은 다음 세 가지 중 하나가 발생 시점까지 버블링:

- 일반 런타임 오류 메시지가 표시 됩니다. 이 페이지 있는지 런타임 오류가 발생 했지만 오류에 대 한 세부 정보를 제공 하지 않는 사용자를 게 알립니다.
- 방금 throw 된 예외에 대 한 정보를 포함 하는 예외 세부 정보 메시지가 표시 됩니다.
- 원하는 모든 메시지를 표시 하는 사용자가 만든 ASP.NET 페이지는 사용자 지정 오류 페이지 표시 됩니다.

처리 되지 않은 예외가 발생 하는 경우 발생 하는 상황에 따라 달라 집니다 합니다 `Web.config` 파일의 [ `<customErrors>` 섹션](https://msdn.microsoft.com/library/h0hfz6fc.aspx)합니다.

개발 및 응용 프로그램을 테스트할 때 브라우저에서 모든 예외의 세부 정보를 볼 수 있습니다. 그러나 프로덕션에서 응용 프로그램에서 예외 정보를 보여 주는 잠재적인 보안 위험이 초래 됩니다. 또한 flattering 아니며 비 전문적으로 보이는 웹 사이트를 만듭니다. 이상적으로 처리 되지 않은 예외가 발생할 경우 개발 환경에서 웹 응용 프로그램 예외 세부 정보가 표시 됩니다는 프로덕션 환경에서 동일한 응용 프로그램 사용자 지정 오류 페이지를 표시 합니다.

> [!NOTE]
> 기본 `<customErrors>` 섹션 설정 예외 세부 정보 페이지를 통해 localhost를 방문 하 고 그렇지 않으면 일반 런타임 오류 페이지를 보여 줍니다 하는 경우에 메시지를 보여 줍니다. 이러한 방식이 이상적 이지만 기본 동작은 로컬이 아닌 방문자에 게 예외 세부 정보를 표시 되지 않으며 알아야 보장 됩니다. 이후 자습서 검사는 `<customErrors>` 단원에서 자세히 프로덕션에서 오류가 발생 하는 경우 표시 된 사용자 지정 오류 페이지를 사용 하는 방법을 보여 줍니다.


개발 하는 동안 사용 되는 다른 ASP.NET 기능 추적 됩니다. 추적을 사용 하도록 설정 하는 경우 들어오는 각 요청에 대 한 정보를 기록 하 고 특수 한 웹 페이지를 제공 `Trace.axd`, 최근 요청 세부 정보 보기에 대 한 합니다. 설정를 통해 추적을 구성 합니다 [ `<trace>` 요소](https://msdn.microsoft.com/library/6915t83k.aspx) 에서 `Web.config`합니다.

사용 하도록 설정 하면 추적 확인 있는지 프로덕션 환경에서 사용 하지 않도록 설정 됩니다. 추적 정보를 쿠키, 세션 데이터 및 기타 잠재적으로 중요 한 정보를 포함 되므로 프로덕션 환경에서 추적을 사용 하지 않도록 설정 합니다. 다행 스럽게도, 기본적으로 추적 해제 되었음 및 `Trace.axd` localhost를 통해 액세스할 수 있습니다. 개발에서 이러한 기본 설정을 변경한 경우에 이러한 해제 되어 다시 프로덕션 있는지 확인 합니다.

## <a name="techniques-for-maintaining-separate-configuration-information"></a>별도 구성 정보를 유지 관리 기술

다른 구성 설정을 개발 및 프로덕션 환경에 있으면 배포 프로세스를 복잡해 집니다. 이전 두 자습서에서 배포 프로세스 관련 프로덕션에서 개발에서 모든 필요한 파일 복사 방법은 구성 정보를 두 환경 모두에서 동일 하는 경우에 작동 하지만 해당 합니다. 다양 한 구성 정보를 사용 하 여 응용 프로그램을 배포 하기 위한 기술의 여러 가지가 있습니다. 호스트 된 웹 응용 프로그램에 대 한 이러한 옵션 중 일부를 카탈로그 보겠습니다.

### <a name="manually-deploying-the-production-environment-configuration-file"></a>프로덕션 환경 구성 파일을 수동으로 배포

두 버전을 유지 하는 가장 간단한 방법입니다는 `Web.config` 파일: 개발 환경 및 프로덕션 환경에 대해 각각 하나씩 있습니다. 개발 환경에서 프로덕션 서버로 복사 하는 모든 파일을 수반 사이트를 프로덕션에 배포 *제외한* 에 대 한는 `Web.config` 파일입니다. 대신, 프로덕션 환경 특정 `Web.config` 파일 프로덕션에 복사 합니다.

이 방법은 매우 복잡 한 이지만 구성 정보는 자주 변경 되기 때문에 구현 하기 쉽습니다. 응용 프로그램 소규모 개발 팀을 사용 하 여 단일 웹 서버에서 호스트 되는 구성 정보를 가져올 자주 변경 되지 적합을 작동 합니다. 독립 실행형 FTP 클라이언트를 사용 하 여 응용 프로그램 파일을 수동으로 배포 하는 경우 가장 해입니다. 먼저 배포 별 스왑 해야 Visual Studio의 웹 사이트 복사 도구 또는 게시 옵션을 사용 하는 경우 `Web.config` 를 배포 하기 전에 프로덕션 별 하나를 사용 하 여 파일을 다음 배포 완료 된 후에 다시 교체 합니다.

### <a name="change-the-configuration-during-the-build-or-deployment-process"></a>빌드 또는 배포 프로세스 중에 구성을 변경 합니다.

지금 토론 임시 빌드 및 배포 프로세스를 가정 있어야 합니다. 많은 대규모 소프트웨어 프로젝트 타사 도구 또는 오픈 소스 홈 증가 사용 하는 프로세스를 공식화 더 있어야 합니다. 이러한 프로젝트에 대 한 가능성이 프로덕션에 푸쉬 되기 전에 구성 정보를 적절 하 게 수정 하는 빌드 또는 배포 프로세스를 지정할 수 있습니다. 사용 하 여 웹 응용 프로그램을 작성 하는 경우 [MSBuild](http://en.wikipedia.org/wiki/MSBuild)를 [NAnt](http://nant.sourceforge.net/), 또는 다른 빌드 도구를 추가할 수 있습니다 것을 수정 하는 빌드 단계는 `Web.config` 프로덕션 전용 설정을 포함 하도록 파일입니다. 프로그래밍 방식으로 원본 제어 서버에 연결 하 고 적절 한 수 배포 워크플로 또는 `Web.config` 파일입니다.

프로덕션 환경에 적절 한 구성 정보를 가져오기 위한 실제 방법은 널리 도구 및 워크플로에 따라 다릅니다. 이와 같이 하지 설명을이 항목을 추가 합니다. MSBuild 또는 NAnt와 같은 인기 있는 빌드 도구를 사용 하는 경우 있습니다 배포 문서 및 자습서 웹 검색을 통해 이러한 도구에 특정 합니다.

### <a name="managing-configuration-differences-via-the-web-deployment-project-add-in"></a>웹 배포를 통해 관리 구성 차이 프로젝트 추가

2006 Microsoft Visual Studio 2005 용 웹 개발 프로젝트에서 추가 기능 출시 합니다. Visual Studio 2008에 추가-2008에 출시 되었습니다. 이 추가 기능에 해당 웹 응용 프로그램 프로젝트와 함께 별도 웹 배포 프로젝트를 만들려면 기본 제공 ASP.NET 개발자를 위한, 명시적으로 웹 응용 프로그램을 컴파일하고 있으며 로컬 출력 디렉터리에 배포할 파일을 복사 합니다. 웹 응용 프로그램 프로젝트를 백그라운드에서 MSBuild를 사용합니다.

기본적으로 개발 환경의 `Web.config` 파일이 출력 디렉터리에 복사 됩니다 있지만 사용자 지정 하려면 웹 배포 프로젝트를 설정할 수 있습니다.는

다음과 같은 방법으로이 디렉터리에 복사 하는 구성 정보:

- 통해 `Web.config` 파일 섹션 대체를 바꿀 섹션을 지정 하는 및 바꿀 텍스트를 포함 하는 XML 파일입니다.
- 외부 구성 소스 파일에는 경로 제공 합니다. 이 옵션을 선택 하면 웹 배포 프로젝트는 특정 복사 `Web.config` 파일을 출력 디렉터리 (대신 `Web.config` 개발 환경에서 사용 되는 파일).
- 웹 배포 프로젝트에서 사용 되는 MSBuild 파일 사용자 지정 규칙 추가 하 여

웹 배포 프로젝트의 웹 응용 프로그램 빌드를 배포 및 프로덕션 환경에 프로젝트의 출력 폴더에서 파일을 복사 합니다.

확인 웹 배포 프로젝트를 사용 하 여 자세히 알아보려면 [웹 배포 프로젝트 기사의](https://msdn.microsoft.com/magazine/cc163448.aspx) 2007 년 4 월호에서 [MSDN Magazine](https://msdn.microsoft.com/magazine/default.aspx), 또는에서 추가 정보 섹션의 링크를 참조 하세요.는 이 자습서의 끝입니다.

> [!NOTE]
> 웹 배포 프로젝트를 Visual Studio에서 추가 기능을 구현 되 고 Visual Studio Express Edition (Visual Web Developer) 추가 기능을 지원 하지 않습니다 때문에 Visual Web Developer를 사용 하 여 웹 배포 프로젝트를 사용할 수 없습니다.


## <a name="summary"></a>요약

웹 응용 프로그램 개발에서의 동작과 외부 리소스는는 프로덕션 환경에서 동일한 응용 프로그램의 경우 일반적으로 다릅니다. 예를 들어 데이터베이스 연결 문자열, 컴파일 옵션 및 동작 처리 되지 않은 예외는 일반적으로 발생 하는 경우 환경 간에 다릅니다. 배포 프로세스는 이러한 차이 수용 해야 합니다. 이 자습서에서 설명한 대로 간단 하 게 대체 구성 파일을 프로덕션 환경에 수동으로 복사 방법은입니다. 세련 된 솔루션은 가능한 웹 배포 프로젝트 추가 기능에서 사용 하는 경우 또는 이러한 사용자 지정을 수용할 수 있는 더 공식화 된 빌드 또는 배포 프로세스를 사용 하 여 합니다.

즐거운 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [설명 하는 연결 문자열](http://www.connectionstrings.com/Articles/Show/what-is-a-connection-string)
- [데이터베이스 연결 문자열 @ ConnectionStrings.com](http://www.connectionstrings.com/)
- [사용 하 여 프로덕션 ASP.NET 응용 프로그램을 실행 하지 마세요 `debug="true"` 사용 하도록 설정](https://weblogs.asp.net/scottgu/Don_1920_t-run-production-ASP.NET-Applications-with-debug_3D001D20_true_1D20_-enabled)
- [정상적으로 처리 되지 않은 예외-친숙 한 오류 페이지 표시에 응답](http://aspnet.4guysfromrolla.com/articles/090606-1.aspx)
- [방법: 사용 하 여 Visual Studio 2008 웹 배포 프로젝트?](../../../videos/how-do-i/how-do-i-use-a-visual-studio-2008-web-deployment-project.md)
- [데이터베이스를 배포 하는 경우 키 구성 설정](http://aspnet.4guysfromrolla.com/articles/121008-1.aspx)
- [Visual Studio 2008 웹 배포 프로젝트 다운로드](https://www.microsoft.com/downloads/details.aspx?FamilyId=0AA30AE8-C73B-4BDD-BB1B-FE697256C459&amp;displaylang=en) | [Visual Studio 2005 웹 배포 프로젝트 다운로드](https://download.microsoft.com/download/9/4/9/9496adc4-574e-4043-bb70-bc841e27f13c/WebDeploymentSetup.msi)
- [VS 2008 웹 배포 프로젝트](https://weblogs.asp.net/scottgu/archive/2005/11/06/429723.aspx) | [VS 2008 웹 배포 프로젝트 지원이 출시](https://weblogs.asp.net/scottgu/archive/2008/01/28/vs-2008-web-deployment-project-support-released.aspx)
- [웹 배포 프로젝트](https://msdn.microsoft.com/magazine/cc163448.aspx)

> [!div class="step-by-step"]
> [이전](deploying-your-site-using-visual-studio-vb.md)
> [다음](core-differences-between-iis-and-the-asp-net-development-server-vb.md)
