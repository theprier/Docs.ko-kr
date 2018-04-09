---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/displaying-a-custom-error-page-vb
title: 사용자 지정 오류 페이지 (VB)를 표시 합니다. | Microsoft Docs
author: rick-anderson
description: 가 사용자 볼 ASP.NET 웹 응용 프로그램에서 런타임 오류가 발생할 때? 방법에 따라 결정 웹 사이트의 &lt;customErrors&gt; 구성 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/09/2009
ms.topic: article
ms.assetid: 14873c5d-81a9-455b-bd71-30fb555583e7
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/displaying-a-custom-error-page-vb
msc.type: authoredcontent
ms.openlocfilehash: eda7ceeac174f0d1697cb95d2eab4127f124011e
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="displaying-a-custom-error-page-vb"></a>사용자 지정 오류 페이지 (VB)를 표시합니다.
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/1/0/C/10CC829F-A808-4302-97D3-59989B8F9C01/ASPNET_Hosting_Tutorial_11_VB.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial11_CustomErrors_vb.pdf)

> 가 사용자 볼 ASP.NET 웹 응용 프로그램에서 런타임 오류가 발생할 때? 방법에 따라 결정 웹 사이트의 &lt;customErrors&gt; 구성 합니다. 기본적으로 사용자는 런타임 오류가 발생 했습니다 proclaiming 흉한는 노란색 화면을 표시 됩니다. 이 자습서에는 사이트의 모양과 느낌을 일치 하는-시선을 표시 사용자 지정 오류 페이지에 이러한 설정을 사용자 지정 하는 방법을 보여 줍니다.


## <a name="introduction"></a>소개

완벽 한 상황에서는 런타임에 오류가 있을 것. 강력한 사용자 입력된 유효성 검사 및 외부 데이터베이스 서버와 전자 메일 서버와 같은 리소스는 오프 라인 안함와 프로그래머 링크도 확인을 사용 하 여 코드 버그 작성할 것입니다. 물론, 실제로 오류는 불가피 아닙니다. .NET Framework의 클래스는 예외를 throw 하 여 오류를 표시 합니다. Open 메서드를 개체의 연결 문자열에서 지정 된 데이터베이스에 연결을 설정 하는 예를 들어 SqlConnection을 호출 합니다. 그러나 데이터베이스 다운 된 경우 또는 연결 문자열에 자격 증명이 유효 하지 않으면 다음 Open 메서드가 throw는 `SqlException`합니다. 예외를 사용 하 여 처리 될 수 `Try/Catch/Finally` 블록입니다. 경우 내의 코드는 `Try` 제어가 적절 한 catch 블록으로 개발자 수 오류에서 복구를 시도 하는 위치, 블록에서 예외가 발생 합니다. 일치 하는 catch 블록이 없는 없거나 예외 percolates search의 호출 스택으로 예외를 발생 시킨 코드 try 블록에 없는 경우 `Try/Catch/Finally` 블록입니다.

예외 처리 되 고 하지 않고 ASP.NET 런타임이 이르기까지 버블링 되는 경우는 [ `HttpApplication` 클래스](https://msdn.microsoft.com/library/system.web.httpapplication.aspx)의 [ `Error` 이벤트](https://msdn.microsoft.com/library/system.web.httpapplication.error.aspx) 발생 구성 된 *오류 페이지*  표시 됩니다. 기본적으로 ASP.NET가 단계적으로 라고 하는 오류 페이지가 표시 됩니다는 [노란색 화면 사망](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow) (YSOD). 두 가지 버전의는 YSOD: 한 표시 예외 정보, 스택 추적 및 기타 정보는 응용 프로그램을 디버깅 하는 개발자가 (참조 **그림 1**); 다른 명시 하 고 런타임 오류 (참조 했습니다 **그림 2**).

예외 정보 YSOD 매우 응용 프로그램을 디버깅 하는 개발자를 위한 하지만 끈적이거나 및 비 전문적을 최종 사용자에 게는 YSOD를 표시 합니다. 대신, 최종 사용자가 상황을 설명 하는 보다 사용자 친화적인 용어일와 사이트의 모양과 느낌을 유지 하는 오류 페이지를 취해야 합니다. 다행히도는 사용자 지정 오류 페이지를 만드는 쉽게 된다는 점입니다. 이 자습서를 살펴보고 ASP 시작합니다. NET의 다른 오류는 페이지입니다. 그런 다음 사용자에 게 오류가 발생 한 경우에도 사용자 지정 오류 페이지를 표시할 웹 응용 프로그램을 구성 하는 방법을 보여 줍니다.

### <a name="examining-the-three-types-of-error-pages"></a>세 가지 유형의 오류 페이지를 검사합니다.

세 가지 유형의 오류 페이지 중 하나는 ASP.NET 응용 프로그램에서 처리 되지 않은 예외가 발생 하는 경우 표시 됩니다.

- 예외 세부 정보 노란색 화면의 사망 오류 페이지
- 런타임 오류 노란색 화면의 사망 오류 페이지 또는
- 사용자 지정 오류 페이지

오류 페이지 개발자는은 가장 친숙 한 된 예외 세부 정보 YSOD 합니다. 기본적으로이 페이지는 로컬로 방문 하는 사용자에 게 표시 되 고 따라서는 개발 환경에서 사이트를 테스트할 때 오류가 발생할 때 표시 되는 페이지. 이름에서 알 수 있듯이 예외 세부 정보 YSOD 유형, 메시지 및 스택 추적-예외에 대 한 정보를 제공 합니다. 게다가 ASP.NET 페이지의 코드 숨김 클래스의 코드에서 예외가 발생 하 고 응용 프로그램 디버깅을 위해 구성 된 경우 다음 예외 세부 정보 YSOD도 표시 됩니다이 줄의 코드 (및 그 아래의 및 위의 코드 몇 줄만 작성).

**그림 1** 예외 세부 정보 YSOD 페이지를 보여 줍니다. 브라우저의 주소 창에는 URL을 확인: `http://localhost:62275/Genre.aspx?ID=foo`합니다. 이전에 설명한 대로 `Genre.aspx` 특정 장르의 책 검토를 나열 하는 페이지입니다. `GenreId` 값 (한 `uniqueidentifier`) querystring; 통과 소설 검토를 보려면 적절 한 URL은 예를 들어 `Genre.aspx?ID=7683ab5d-4589-4f03-a139-1c26044d0146`합니다. 아닌`uniqueidentifier` 값이 전달 되는 쿼리 문자열 (예: "foo")을 통해 예외가 throw 됩니다.

> [!NOTE]
> 데모 웹 응용 프로그램에서이 오류를 재현 다운로드할 수 있는 하려면 다음 중 하나가 방문 `Genre.aspx?ID=foo` 직접 "런타임 오류 생성" 링크를 클릭 하거나 `Default.aspx`합니다.


제공 되는 예외 정보를 참고 **그림 1**합니다. 예외 메시지를 "변환이 실패 한 문자열에서을 uniqueidentifier로"가 페이지 맨 앞에 있어야 합니다. 예외의 유형을 `System.Data.SqlClient.SqlException`도 나열 됩니다. 스택 추적 이기도합니다.

[![](displaying-a-custom-error-page-vb/_static/image2.png)](displaying-a-custom-error-page-vb/_static/image1.png)

**그림 1**: YSOD 예외 정보는 예외에 대 한 정보를 포함 합니다.  
 ([전체 크기 이미지를 보려면 클릭](displaying-a-custom-error-page-vb/_static/image3.png))

다른 유형의 YSOD 런타임 오류 YSOD는 및에 표시 되는지 **그림 2**합니다. 런타임 오류 YSOD 방문자에서 런타임 오류가 발생 했음을 알립니다 있지만 throw 된 예외에 대 한 정보를 포함 하지 않습니다. 하지만 (오류 세부 정보를 수정 하 여 볼 수 있도록 하는 방법에 지침을 제공,는 `Web.config` 비 전문적으로 보이는 이러한 YSOD 하는 요소에 포함 되어 있는 파일입니다.)

기본적으로 런타임 오류 YSOD에 원격으로 방문 하는 사용자에 게 표시 됩니다 (통해 http://www.yoursite.com)에서 브라우저의 주소 표시줄에 URL에서 알 수 있듯이, **그림 2**: `http://httpruntime.web703.discountasp.net/Genre.aspx?ID=foo`합니다. 개발자가 오류 세부 정보를 알고 싶을 아니라 보안 문제 또는 기타 중요 한 정보를 방문 하는 모든 사용자에 게 표시 될 수 있습니다 때 등의 정보가 라이브 사이트에 표시 되지 않아야 때문에 두 개의 서로 다른 YSOD 화면 존재 하면 사이트입니다.

> [!NOTE]
> 중인 DiscountASP.NET 웹 호스트로 사용 하는 경우 런타임 오류 YSOD 라이브 사이트를 방문할 때 표시 되지 않습니다 확인할 수 있습니다. 기본적으로 예외 세부 정보 YSOD 표시 하도록 구성 하는 서버를 보유 하는 DiscountASP.NET 때문입니다. 다행 스럽게도 추가 하 여이 기본 동작을 재정의할 수 있습니다는 `<customErrors>` 섹션을 프로그램 `Web.config` 파일입니다. "구성 오류 페이지 표시할" 섹션을 검사 하는 `<customErrors>` 섹션 자세히 설명에서 합니다.


[![](displaying-a-custom-error-page-vb/_static/image5.png)](displaying-a-custom-error-page-vb/_static/image4.png)

**그림 2**: YSOD 런타임 오류가 발생 한 오류 세부 정보를 포함 되지 않습니다  
 ([전체 크기 이미지를 보려면 클릭](displaying-a-custom-error-page-vb/_static/image6.png))

오류 페이지의 세 번째 형식은 만들어진 웹 페이지 사용자 지정 오류 페이지 합니다. 사용자 지정 오류 페이지의 혜택에는 페이지의 모양과 느낌; 함께 사용자에 게 표시 되는 정보를 완전히 제어할 있는 사용자 지정 오류 페이지는 다른 페이지도 동일한 마스터 페이지 및 스타일 사용할 수 있습니다. "사용자 지정 오류 페이지를 사용 하 여" 섹션 존재 하지 않는 사용자 지정 오류 페이지를 만들고 구성 하는 처리 되지 않은 예외가 발생할 경우를 표시 하도록 안내 합니다. **그림 3** 이 사용자 지정 오류 페이지 최고 힌트를 제공 합니다. 볼 수 있듯이 오류 페이지의 모양과 느낌 훨씬 더 많은 전문적인 보다는 노란색 화면의 사망 그림 1과 2에 표시 된 것 중 하나입니다.

[![](displaying-a-custom-error-page-vb/_static/image8.png)](displaying-a-custom-error-page-vb/_static/image7.png)

**그림 3**: 사용자 지정 오류 페이지에서는 더 맞춤형된 모양 및 느낌을 제공 합니다.  
 ([전체 크기 이미지를 보려면 클릭](displaying-a-custom-error-page-vb/_static/image9.png))

브라우저의 주소 표시줄에 검사을 **그림 3**합니다. 주소 표시줄에 사용자 지정 오류 페이지의 URL이 표시 됩니다 (`/ErrorPages/Oops.aspx`). 그림 1과 2에서 노란색 사망 화면에서 오류가 발생 한 동일한 페이지에 표시 됩니다 (`Genre.aspx`). 사용자 지정 오류 페이지를 통해 오류가 발생 하는 페이지의 URL에 전달 되는 `aspxerrorpath` querystring 매개 변수입니다.

## <a name="configuring-which-error-page-is-displayed"></a>표시 되는 오류 페이지 구성

표시 되는 세 가지 가능한 오류 페이지는 두 개의 변수를 기반으로 합니다.

- 구성 정보는 `<customErrors>` 섹션 및
- 여부 사용자가 로컬 또는 원격으로 사이트를 방문 합니다.

[ `<customErrors>` 섹션](https://msdn.microsoft.com/library/h0hfz6fc.aspx) 에 `Web.config` 어떤 오류 페이지가 표시 될 영향을 주는 두 개의 특성이: `defaultRedirect` 및 `mode`합니다. `defaultRedirect` 특성은 선택 사항이며 제공 된 경우 사용자 지정 오류 페이지의 URL을 지정 하 고 런타임 오류 YSOD 대신 사용자 지정 오류 페이지 표시 됨을 나타냅니다. `mode` 특성은 필수 이며 세 가지 값 중 하나를 허용: `On`, `Off`, 또는 `RemoteOnly`합니다. 이러한 값은 다음과 같이 동작:

- `On` -사용자 지정 오류 페이지나 런타임 오류 YSOD 로컬 또는 원격 인지 여부에 관계 없이 모든 방문자에 게 표시 됨을 나타냅니다.
- `Off` -예외 세부 정보 YSOD 로컬 또는 원격 인지 여부에 관계 없이 모든 방문자에 게 표시 되도록 지정 합니다.
- `RemoteOnly` -사용자 지정 오류 페이지나 런타임 오류 YSOD 나타나는지 원격 방문자에 게 예외 세부 정보 YSOD 로컬 방문자에 게 표시 되 나타냅니다.

별도로 지정 하지 않으면 ASP.NET 것 처럼 작동 모드 특성 설정한 경우 `RemoteOnly` 지정 하지 않았으면 및는 `defaultRedirect` 값입니다. 즉, 기본 동작은 런타임 오류 YSOD 원격 방문자에 게 표시 되는 예외 세부 정보 YSOD 로컬 방문자에 게 표시 됩니다. 추가 하 여이 기본 동작을 재정의할 수 있습니다는 `<customErrors>` 웹 응용 프로그램에 섹션 `Web.config file.`

## <a name="using-a-custom-error-page"></a>사용자 지정 오류 페이지를 사용 하 여

모든 웹 응용 프로그램 사용자 지정 오류 페이지에 있어야 합니다. 런타임 오류 YSOD 하는 전문가 수준의 대신 제공 하 고를 쉽게 만들 수는 몇 분만에 사용자 지정 오류 페이지를 사용 하 여 응용 프로그램 구성 합니다. 첫 번째 단계는 사용자 지정 오류 페이지를 만드는 것입니다. 명명 된 책 검토 응용 프로그램에 새 폴더를 추가 했습니다 `ErrorPages` 명명 된 새 ASP.NET 페이지에 추가 하 고 `Oops.aspx`합니다. 동일한 모양 및 느낌을 자동으로 상속 되도록 사이트에 있는 페이지의 나머지 부분과 동일한 마스터 페이지를 사용 하는 페이지가 있습니다.

[![](displaying-a-custom-error-page-vb/_static/image11.png)](displaying-a-custom-error-page-vb/_static/image10.png)

**그림 4**: 사용자 지정 오류 페이지 만들기

오류 페이지에 대 한 콘텐츠를 작성 하는 몇 분을 다음으로 보냅니다. 예기치 않은 오류가 발생 하는 사이트의 홈 페이지에 링크를 다시 없다는 메시지와 함께 간단한 사용자 지정 오류 페이지를 만들었습니다.

[![](displaying-a-custom-error-page-vb/_static/image13.png)](displaying-a-custom-error-page-vb/_static/image12.png)

**그림 5**: 사용자 지정 오류 페이지 디자인  
 ([전체 크기 이미지를 보려면 클릭](displaying-a-custom-error-page-vb/_static/image14.png))

오류 페이지 완료와 런타임 오류 YSOD 대신이 대화 상자 사용자 지정 오류 페이지를 사용 하도록 웹 응용 프로그램을 구성 합니다. 이 작업에 오류 페이지의 URL을 지정 하 여 수행 됩니다는 `<customErrors>` 섹션의 `defaultRedirect` 특성입니다. 응용 프로그램에 다음 태그를 추가 `Web.config` 파일:

[!code-xml[Main](displaying-a-custom-error-page-vb/samples/sample1.xml)]

위의 태그 예외 세부 정보 YSOD Oops.aspx 사용자 지정 오류 페이지를 사용 하 여 해당 사용자가 원격으로 방문 하는 동안 로컬에 방문 하는 사용자에 게 표시 하도록 응용 프로그램을 구성 합니다. 예를 보려면, 하려면 프로덕션 환경에 웹 사이트를 배포 하 고 Genre.aspx 페이지 잘못 된 쿼리 문자열 값으로 라이브 사이트를 방문 하십시오. 사용자 지정 오류 페이지가 표시 됩니다 (다시 참조 **그림 3**).

사용자 지정 오류 페이지만 원격 사용자에 게 표시 되어 있는지를 확인 하려면 다음을 방문는 `Genre.aspx` 개발 환경에서 잘못 된 querystring 페이지입니다. 예외 세부 정보 YSOD 여전히 나타납니다 (다시 참조 **그림 1**). `RemoteOnly` 예외의 세부 정보를 계속 해 서 개발자가 로컬로 작업 동안 프로덕션 환경에 있는 사이트를 방문 하는 사용자의 사용자 지정 오류 페이지에 표시 되도록 설정 합니다.

## <a name="notifying-developers-and-logging-error-details"></a>세부 정보를 기록 하 고 개발자에 게 알리는

그녀의 컴퓨터를 직접 개발자가 개발 환경에서 발생 하는 오류 발생 합니다. 그녀는 예외 정보 예외 세부 정보 YSOD 고 보고서 영업 관리자가 수행 중에 오류가 발생 한 단계 알고 있습니다. 하지만 개발자가 최종 사용자는 사이트를 방문 하는 오류를 보고 하는 데 시간 하지 않으면 오류가 발생 했음을 알지 프로덕션에 오류가 발생 합니다. 한 사용자가 예외 유형, 메시지 및 스택 추적 해결 아니며, 오류의 원인을 진단 하기 어려울 수 있습니다 알 필요 없이 오류가 발생 하는 개발 팀에 게 알리도록 하려면 비로소를 벗어날 경우에 합니다.

가장 중요 하며 프로덕션 환경에서 오류 (예: 데이터베이스) 영구 저장소에 기록 됩니다는 이러한 이유로 개발자는이 오류의 경고가 표시 됩니다. 사용자 지정 오류 페이지는이 로깅 및 알림 작업을 수행 하는 것이 좋습니다 처럼 보입니다. 그러나 사용자 지정 오류 페이지 오류 세부 정보에 액세스할 수 없고이 정보를 기록 하도록 사용할 수 없습니다. 다행히도 다양 한 방법으로, 로그 및 오류 세부 정보를 가로챌 수는 다음 세 개의 자습서에서는이 항목에서 자세히 탐색할입니다.

## <a name="using-different-custom-error-pages-for-different-http-error-statuses"></a>다른 HTTP 오류 상태에 대 한 다른 사용자 지정 오류 페이지를 사용 하 여

예외는 ASP.NET 페이지에 의해 throw 되 고 처리 되지 않은 구성 된 오류 페이지를 표시 하는 ASP.NET 런타임에 예외 percolates 합니다. 아마도 요청된 된 파일은 찾을 수 없거나 읽기-요청 ASP.NET 엔진에 제공 되지만 몇 가지 이유로 처리할 수 없는 경우 사용 권한을 사용할 수 없습니다-파일에 대 한 다음 ASP.NET 엔진에서 발생 한 `HttpException`합니다. ASP.NET 페이지에서 발생 한 예외는 같은이 예외가 버블링 인해 적절 한 오류 페이지가 표시 될 런타임에 합니다.

프로덕션 환경에서 웹 응용 프로그램에 대 한 의미 하는 경우 사용자가 이러한 사용자 지정 오류 페이지를 볼 수 없는 페이지를 요청 합니다. **그림 6** 이러한 예를 보여 줍니다. 존재 하지 않는 페이지에 대 한 요청을 하기 때문에 (`NoSuchPage.aspx`), `HttpException` throw 되 고 사용자 지정 오류 페이지가 표시 됩니다 (에 대 한 참조를 확인 `NoSuchPage.aspx` 에 `aspxerrorpath` querystring 매개 변수).

[![](displaying-a-custom-error-page-vb/_static/image16.png)](displaying-a-custom-error-page-vb/_static/image15.png)**그림 6**: ASP.NET 런타임이 잘못 된 요청에 대 한 응답에서 구성 된 오류 페이지가 표시 됩니다.  
 ([전체 크기 이미지를 보려면 클릭](displaying-a-custom-error-page-vb/_static/image17.png)) 

기본적으로 모든 오류 유형이 표시를 동일한 사용자 지정 오류 페이지를 발생 합니다. 그러나 사용 하 여 특정 HTTP 상태 코드는 다른 사용자 지정 오류 페이지를 지정할 수 있습니다 `<error>` 내에서 자식 요소는 `<customErrors>` 섹션. 예를 들어 업데이트에 페이지 오류가 있는 경우 HTTP 상태 코드 404 찾을 수 없음 발생 시 표시 되는 다른 오류 페이지를는 `<customErrors>` 섹션에 다음 태그를 포함 하려면:

[!code-xml[Main](displaying-a-custom-error-page-vb/samples/sample2.xml)]

위치에이 변경으로 인해 원격으로 방문한 사용자 존재 하지 않는 ASP.NET 리소스를 요청할 때마다 리디렉션됩니다에 `404.aspx` 대신 사용자 지정 오류 페이지 `Oops.aspx`합니다. 으로 **그림 7** 에서는 `404.aspx` 페이지 일반 사용자 지정 오류 페이지 보다 더 구체적인 메시지를 포함할 수 있습니다.

> [!NOTE]
> 체크 아웃 [404 오류 페이지를 하나 더 시간](http://www.smashingmagazine.com/2009/01/29/404-error-pages-one-more-time/) 효과적인 404 오류 페이지 만들기에 대 한 지침입니다.


[![](displaying-a-custom-error-page-vb/_static/image19.png)](displaying-a-custom-error-page-vb/_static/image18.png)**그림 7**: 404 사용자 지정 오류 페이지 보다 정확한 메시지를 표시 합니다. `Oops.aspx`  
 ([전체 크기 이미지를 보려면 클릭](displaying-a-custom-error-page-vb/_static/image20.png)) 

됨을 알고 있으므로 `404.aspx` 사용자가 찾을 수 없는 페이지에 대 한 요청을 하면 페이지에 도달만,이 특정 유형의 오류를 해결 하는 사용자를 제공 하는 기능이 포함 하려면이 사용자 지정 오류 페이지를 향상 시킬 수 있습니다. 예를 들어 있습니다 수 좋은 Url에 잘못 된 Url을 알려진으로 매핑되는 데이터베이스 테이블을 작성 한 다음는 `404.aspx` 테이블 및 페이지는 사용자에 도달 하려고 할 수 있습니다를 제안 하는 사용자 지정 오류 페이지에 대 한 쿼리를 실행 합니다.

> [!NOTE]
> 사용자 지정 오류 페이지는 ASP.NET 엔진에서 처리 하는 리소스를 요청이 있을 때에 표시 됩니다. 설명한 것 처럼는 [IIS 간의 차이점 Core 및 ASP.NET 개발 서버](core-differences-between-iis-and-the-asp-net-development-server-vb.md) 자습서, 웹 서버 수 특정 요청을 처리 자체입니다. 기본적으로 IIS는 ASP.NET 엔진을 호출 하지 않고 HTML 파일 및 이미지와 같은 정적 콘텐츠에 대 한 서버 프로세스 요청을 웹입니다. 따라서 사용자가 존재 하지 않는 이미지 파일을 요청할 경우 볼 수 ASP 보다는 IIS의 기본 404 오류 메시지입니다. NET의 오류 페이지를 구성합니다.


## <a name="summary"></a>요약

사용자 3 개의 오류 페이지 중 하나 표시 ASP.NET 응용 프로그램에서 처리 되지 않은 예외가 발생 하는 경우:는 예외 세부 정보 노란색 화면의 사망; 런타임 오류 노란색 사망;의 화면 또는 사용자 지정 오류 페이지입니다. 응용 프로그램에 따라 달라 집니다 표시 되는 오류 페이지 `<customErrors>` 구성 및 로컬 또는 원격으로 사용자가 방문 하는 여부. 기본 동작은 로컬 방문자에 게 예외 세부 정보 YSOD 및 런타임 오류 YSOD 원격 방문자에 게 표시 하는 것입니다.

런타임 오류 YSOD 사이트를 방문 하는 사용자의 잠재적으로 중요 한 오류 정보를 숨기면 동안 사이트의 모양과 느낌을 중단 하 고 추가 하면 잘못 된 코드를 확인 하는 응용 프로그램입니다. 더 나은 방법은 만들어 사용자 지정 오류 페이지를 디자인 하 고에서 해당 URL을 지정 하는 과정이 수반 됩니다 사용자 지정 오류 페이지를 사용 하는 `<customErrors>` 섹션의 `defaultRedirect` 특성입니다. 여러 HTTP 오류 상태에 대 한 여러 사용자 지정 오류 페이지 될 수도 있습니다.

사용자 지정 오류 페이지는 처리 전략 프로덕션 환경에서 웹 사이트에 대 한 포괄적인 오류는 첫 번째 단계입니다. 개발자는 오류를 경고 하 고 로깅 세부 정보는 중요 한 단계 됩니다. 다음 세 개의 자습서에서는 오류 알림 및 로깅에 대 한 기술 탐색합니다.

만족도 매우 프로그래밍!

## <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [오류 페이지, 한 번 더](http://www.smashingmagazine.com/2009/01/29/404-error-pages-one-more-time/)
- [예외 디자인 지침](https://msdn.microsoft.com/library/ms229014.aspx)
- [사용자에 게 친숙 오류 페이지](http://aspnet.4guysfromrolla.com/articles/090606-1.aspx)
- [예외 처리 및 Throw](https://msdn.microsoft.com/library/5b2yeyab.aspx)
- [ASP.NET에서 사용자 지정 오류 페이지를 사용 하 여 제대로](http://professionalaspnet.com/archive/2007/09/30/Properly-Using-Custom-Error-Pages-in-ASP.NET.aspx)

> [!div class="step-by-step"]
> [이전](strategies-for-database-development-and-deployment-vb.md)
> [다음](processing-unhandled-exceptions-vb.md)
