---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/displaying-a-custom-error-page-cs
title: 표시를 사용자 지정 오류 페이지 (C#) | Microsoft Docs
author: rick-anderson
description: 표시 되는 내용에 사용자는 ASP.NET 웹 응용 프로그램에서 런타임 오류가 발생 하는 경우 답변 하는 방법에 따라 달라 집니다 웹 사이트 &lt;customErrors&gt; 구성 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/09/2009
ms.topic: article
ms.assetid: cb061642-faf3-41b2-9372-69e13444d458
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/displaying-a-custom-error-page-cs
msc.type: authoredcontent
ms.openlocfilehash: 7f2e9165acf86ce62d51e7c8d67205684d68e214
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37362945"
---
<a name="displaying-a-custom-error-page-c"></a>사용자 지정 오류 페이지 (C#)를 표시합니다.
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/1/0/C/10CC829F-A808-4302-97D3-59989B8F9C01/ASPNET_Hosting_Tutorial_11_CS.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial11_CustomErrors_cs.pdf)

> 표시 되는 내용에 사용자는 ASP.NET 웹 응용 프로그램에서 런타임 오류가 발생 하는 경우 답변 하는 방법에 따라 달라 집니다 웹 사이트 &lt;customErrors&gt; 구성 합니다. 기본적으로 사용자 proclaiming 런타임 오류가 발생 하는 힘든 노란색 화면을 표시 됩니다. 이 자습서에는 사이트의 모양과 느낌을 일치 하는 사용자 지정 오류 페이지를 표시는 심미안-것과 달리 이러한 설정을 사용자 지정 하는 방법을 보여 줍니다.


## <a name="introduction"></a>소개

완벽 한 환경에서 런타임 오류가 있을 것입니다. 프로그래머는 무한 급수 코드로 버그 쓰고 강력한 사용자 입력된 유효성 검사와 외부 데이터베이스 서버와 전자 메일 서버와 같은 리소스는 절대로 오프 라인입니다. 물론, 실제로 오류를 피할 수 없습니다. .NET Framework의 클래스는 예외를 throw 하 여 오류를 표시 합니다. 개체의 Open 메서드는 연결 문자열에서 지정한 데이터베이스에 대 한 연결을 설정 하는 예를 들어 SqlConnection을 호출 합니다. 그러나 데이터베이스 다운 된 경우 또는 연결 문자열의 자격 증명이 유효 하지 않으면 Open 메서드가 throw를 `SqlException`입니다. 예외를 사용 하 여 처리할 수 `try/catch/finally` 블록입니다. 경우 내의 코드는 `try` 예외를 throw 하는 블록, 제어가 개발자 오류 로부터 복구 하려면 시작할 수 있는 적절 한 catch 블록으로 전달 됩니다. 일치 하는 catch 블록이 없는 없거나 예외 percolates search의 호출 스택으로 예외를 발생 시킨 코드를 try 블록에 없는 경우 `try/catch/finally` 블록입니다.

예외가 처리 되 고 하지 않고 ASP.NET 런타임이까지 올라갑니다 전달 하는 경우는 [ `HttpApplication` 클래스](https://msdn.microsoft.com/library/system.web.httpapplication.aspx)의 [ `Error` 이벤트](https://msdn.microsoft.com/library/system.web.httpapplication.error.aspx) 발생 하는 구성 된 *오류 페이지*  표시 됩니다. 기본적으로 ASP.NET 일컬어지는 라고 하는 오류 페이지를 표시 합니다 [사망 노란색 화면](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow) (YSOD). 두 가지 버전의 YSOD의: 하나 표시 예외 세부 정보, 스택 추적 및 기타 정보 응용 프로그램을 디버깅 하는 개발자에 게 유용한 (참조 **그림 1**); (참조 런타임오류가발생하는기타단순히상태 **그림 2**).

예외 세부 정보 YSOD는 응용 프로그램을 디버깅 하는 개발자를 위한 매우 유용한 이지만 최종 사용자에 게는 YSOD를 보여 주는 끈적이거나 및 비 전문적으로 합니다. 대신 최종 사용자에 게 상황을 설명 하는 보다 친숙 한 prose를 사용 하 여 사이트의 모양과 느낌을 유지 관리 하는 오류 페이지에 취해야 합니다. 좋은 소식은 상당히 쉽습니다 이러한 사용자 지정 오류 페이지를 만드는 것입니다. 이 자습서를 살펴보고 ASP 시작합니다. NET의 다른 오류는 페이지입니다. 그런 다음 사용자 오류가 발생 하는 경우 사용자 지정 오류 페이지를 표시 하려면 웹 응용 프로그램을 구성 하는 방법을 보여 줍니다.

### <a name="examining-the-three-types-of-error-pages"></a>세 가지 유형의 오류 페이지를 검사합니다.

오류 페이지의 세 가지 유형 중 하나는 ASP.NET 응용 프로그램에서 처리 되지 않은 예외가 발생 하는 경우 표시 됩니다.

- 예외 세부 정보 노란색 화면 죽음의 오류 페이지
- 런타임 오류 노란색 화면 죽음의 오류 페이지 또는
- 사용자 지정 오류 페이지

오류 페이지 개발자가 가장 친숙 한 된 예외 세부 정보 YSOD 합니다. 기본적으로이 페이지 로컬로 방문 하는 사용자에 게 표시 되 고 따라서는 개발 환경에서 사이트를 테스트할 때 오류가 발생 하면 표시 되는 페이지. 이름에서 알 수 있듯이 예외 세부 정보 YSOD 유형, 메시지 및 스택 추적 된 예외에 대 한 정보를 제공 합니다. 게다가 ASP.NET 페이지의 코드 숨김 클래스의 코드에서 예외가 발생 하는 경우 및 응용 프로그램 디버깅을 위해 구성 된 경우 다음 예외 세부 정보 YSOD도 표시 됩니다이 줄의 코드 (및 그 아래 및 위의 코드 몇 줄).

**그림 1** 예외 세부 정보 YSOD 페이지를 보여 줍니다. 브라우저의 주소 창에 url: `http://localhost:62275/Genre.aspx?ID=foo`합니다. 이전에 설명한 대로 `Genre.aspx` 페이지는 특정 장르를의 서 리뷰를 나열 합니다. 필요한 `GenreId` 값 (을 `uniqueidentifier`) querystring; 전달 fiction 검토를 보려면 적절 한 URL은 예를 들어, `Genre.aspx?ID=7683ab5d-4589-4f03-a139-1c26044d0146`합니다. 경우 비-`uniqueidentifier` 값이 전달 되는 쿼리 문자열 (예: "foo")를 통해 예외가 throw 됩니다.

> [!NOTE]
> 데모 웹 응용 프로그램에서이 오류를 재현 하는 다운로드할 수 있습니다 방문 하거나 `Genre.aspx?ID=foo` 직접에서 "런타임 오류 생성" 링크를 클릭 또는 `Default.aspx`합니다.


에 제공 된 예외 정보를 참조 하십시오 **그림 1**합니다. 예외 메시지를 "변환이 실패 한 문자열에서을 uniqueidentifier로" 페이지의 맨 위에 있는 없는 경우 예외의 유형을 `System.Data.SqlClient.SqlException`에 나열 됩니다. 스택 추적 이기도합니다.

[![](displaying-a-custom-error-page-cs/_static/image2.png)](displaying-a-custom-error-page-cs/_static/image1.png)

**그림 1**: YSOD 예외 정보에는 예외에 대 한 정보가 포함 되어 있습니다.  
 ([클릭 하 여 큰 이미지 보기](displaying-a-custom-error-page-cs/_static/image3.png))

다른 유형의 YSOD 런타임 오류 YSOD 이며 같으며 **그림 2**합니다. 런타임 오류 YSOD 방문자에서 런타임 오류가 발생 했음을 알립니다 있지만 throw 된 예외에 대 한 정보가 포함 되지 않습니다. 하지만 (수정 하 여 오류 세부 정보를 볼 수 있도록 하는 방법에 지침을 제공,는 `Web.config` 비 전문적으로 보이는 이러한는 YSOD 때문에 참가 하는 파일입니다.)

기본적으로 런타임 오류 YSOD에 원격으로 방문 하는 사용자에 게 표시 됩니다 (통해 http://www.yoursite.com) 에서 브라우저의 주소 표시줄에 URL에서 알 수 있듯이, **그림 2**: `http://httpruntime.web703.discountasp.net/Genre.aspx?ID=foo`합니다. 개발자는 오류 세부 정보를 알고 싶을 때 하지만 잠재적인 보안 문제 또는 기타 중요 한 정보를 방문 하는 사람에 게 표시 될 수 있습니다 하는 대로 이러한 정보는 라이브 사이트에 표시 되지 않아야 하기 때문에 두 개의 다른 YSOD 화면 존재 하면 사이트입니다.

> [!NOTE]
> 중인 DiscountASP.NET 웹 호스트를 사용 하는 경우, 라이브 사이트를 방문할 때 런타임 오류 YSOD 표시 되지 않습니다 볼 수 있습니다. DiscountASP.NET 기본적으로 예외 세부 정보 YSOD 표시 하도록 구성 하는 서버에 때문입니다. 다행 스럽게도 추가 하 여이 기본 동작을 재정의할 수 있습니다는 `<customErrors>` 섹션을 프로그램 `Web.config` 파일입니다. "구성 하는 오류 페이지가 표시 됩니다" 섹션을 검사 합니다 `<customErrors>` 자세히 섹션입니다.


[![](displaying-a-custom-error-page-cs/_static/image5.png)](displaying-a-custom-error-page-cs/_static/image4.png)

**그림 2**: 런타임 오류 YSOD 오류 세부 정보를 포함 되지 않습니다  
 ([클릭 하 여 큰 이미지 보기](displaying-a-custom-error-page-cs/_static/image6.png))

오류 페이지의 세 번째 형식은 사용자가 만든 웹 페이지 사용자 지정 오류 페이지입니다. 사용자 지정 오류 페이지의 혜택 페이지의 모양과 느낌;와 함께 사용자에 게 표시 되는 정보를 통해 완전히 제어 해야 하는 사용자 지정 오류 페이지에 다른 페이지와 같은 마스터 페이지 및 스타일을 사용 수 있습니다. "사용자 지정 오류 페이지를 사용 하 여" 섹션을 사용자 지정 오류 페이지를 만들고 구성 되지 않은 예외를 발생 시 표시 되도록 안내 합니다. **그림 3** 이 사용자 지정 오류 페이지의 보시고 최고값을 제공 합니다. 알 수 있듯이 오류 페이지의 모양과 느낌 훨씬 더 전문적인 노란색 화면의 쇠퇴 그림 1과 2에 표시 된 것 중 하나 보다 됩니다.

[![](displaying-a-custom-error-page-cs/_static/image8.png)](displaying-a-custom-error-page-cs/_static/image7.png)

**그림 3**: 사용자 지정 오류 페이지를 더 맞춤화 된 모양 및 느낌을 제공  
 ([클릭 하 여 큰 이미지 보기](displaying-a-custom-error-page-cs/_static/image9.png))

브라우저의 주소 표시줄에서 검사할 잠시 **그림 3**합니다. 사용자 지정 오류 페이지의 URL 주소 표시줄에 표시 되는지 확인 (`/ErrorPages/Oops.aspx`). 그림 1과 2에 노란색 사망 화면에서 발생 한 오류는 동일한 페이지에 표시 됩니다 (`Genre.aspx`). 사용자 지정 오류 페이지를 통해 오류가 발생 하는 페이지의 URL에 전달 되는 `aspxerrorpath` querystring 매개 변수입니다.

## <a name="configuring-which-error-page-is-displayed"></a>표시 되는 오류 페이지를 구성 합니다.

표시 되는 세 가지 가능한 오류 페이지는 두 개의 변수를 기반으로 합니다.

- 구성 정보는 `<customErrors>` 섹션 및
- 여부 사용자 로컬 또는 원격으로 사이트를 방문 됩니다.

[ `<customErrors>` 섹션](https://msdn.microsoft.com/library/h0hfz6fc.aspx) 에서 `Web.config` 어떤 오류 페이지가 표시에 영향을 주는 두 개의 특성이: `defaultRedirect` 고 `mode`입니다. `defaultRedirect` 특성은 선택 사항이며 제공 된 경우 사용자 지정 오류 페이지의 URL을 지정 하 고 런타임 오류 YSOD 대신 사용자 지정 오류 페이지 표시 됨을 나타냅니다. 합니다 `mode` 특성은 필수 이며 세 가지 값 중 하나를 받아: `On`를 `Off`, 또는 `RemoteOnly`합니다. 이러한 값에는 다음 동작

- `On` -사용자 지정 오류 페이지나 런타임 오류 YSOD 로컬 인지 원격 인지에 관계 없이 모든 방문자에 게 표시 됨을 나타냅니다.
- `Off` -예외 세부 정보 YSOD 로컬 인지 원격 인지에 관계 없이 모든 방문자에 게 표시 되도록 지정 합니다.
- `RemoteOnly` -사용자 지정 오류 페이지나 런타임 오류 YSOD 나타나는지 원격 방문자에 게 예외 세부 정보 YSOD 로컬 방문자에 게 표시 되는 동안 나타냅니다.

별도로 지정 하지 않으면 ASP.NET 처럼 작동 모드 특성을 설정 했습니다 `RemoteOnly` 지정 하지 않았으면 하 고는 `defaultRedirect` 값입니다. 즉, 기본 동작은 예외 세부 정보 YSOD 런타임 오류 YSOD 원격 방문자에 게 표시 되는 동안 로컬 방문자에 게 표시 됩니다. 추가 하 여이 기본 동작을 재정의할 수는 `<customErrors>` 웹 응용 프로그램의 섹션 `Web.config file.`

## <a name="using-a-custom-error-page"></a>사용자 지정 오류 페이지를 사용 하 여

모든 웹 응용 프로그램을 사용자 지정 오류 페이지에 있어야 합니다. 런타임 오류 YSOD 전문가 수준의 대안을 제공, 쉽게 만들고, 이므로 몇 분만에 사용자 지정 오류 페이지를 사용 하도록 응용 프로그램을 구성 합니다. 첫 번째 단계는 사용자 지정 오류 페이지를 만드는 것입니다. 명명 된도 서 리뷰 응용 프로그램에 폴더를 새로 추가한 `ErrorPages` 명명 된 새 ASP.NET 페이지에 추가 하 고 `Oops.aspx`입니다. 같은 모양과 느낌을 자동으로 상속 되도록 사이트에 있는 페이지의 나머지 부분과 동일한 마스터 페이지를 사용 하는 페이지가 있습니다.

[![](displaying-a-custom-error-page-cs/_static/image11.png)](displaying-a-custom-error-page-cs/_static/image10.png)

**그림 4**: 사용자 지정 오류 페이지 만들기

다음으로 몇 분간 방법으로 오류 페이지에 대 한 콘텐츠 만들기. 예기치 않은 오류가 발생 했습니다을 링크 사이트의 홈 페이지를 나타내는 메시지와 함께 단순한 사용자 지정 오류 페이지를 만들었습니다.

[![](displaying-a-custom-error-page-cs/_static/image13.png)](displaying-a-custom-error-page-cs/_static/image12.png)

**그림 5**: 사용자 지정 오류 페이지 디자인  
 ([클릭 하 여 큰 이미지 보기](displaying-a-custom-error-page-cs/_static/image14.png))

완료 오류 페이지를 사용 하 여 런타임 오류 YSOD 대신 사용자 지정 오류 페이지를 사용 하도록 웹 응용 프로그램을 구성 합니다. 오류 페이지의 URL을 지정 하 여 이렇게 합니다 `<customErrors>` 섹션의 `defaultRedirect` 특성입니다. 응용 프로그램에 다음 태그를 추가 `Web.config` 파일:

[!code-xml[Main](displaying-a-custom-error-page-cs/samples/sample1.xml)]

위의 태그는 예외 세부 정보 YSOD Oops.aspx 사용자 지정 오류 페이지를 사용 하 여 해당 사용자가 원격으로 방문 하는 동안 로컬에 방문 하는 사용자에 게 표시 하도록 응용 프로그램을 구성 합니다. 이 실행 중인 확인 하려면 프로덕션 환경에 웹 사이트를 배포 하 고 잘못 된 쿼리 문자열 값을 사용 하 여 라이브 사이트의 Genre.aspx 페이지를 방문 합니다. 사용자 지정 오류 페이지가 표시 됩니다 (다시 가리킵니다 **그림 3**).

사용자 지정 오류 페이지에는 원격 사용자에만 표시 되는지 확인, 참조는 `Genre.aspx` 개발 환경에서 잘못 된 querystring으로 페이지입니다. 예외 세부 정보 YSOD 계속 표시 (다시 가리킵니다 **그림 1**). `RemoteOnly` 설정 하면 프로덕션 환경에서 사이트를 방문 하는 사용자가 로컬로 작업 하는 개발자 예외의 세부 정보를 확인 하는 동안 사용자 지정 오류 페이지를 참조 합니다.

## <a name="notifying-developers-and-logging-error-details"></a>개발자에 알리고 오류 세부 정보 로깅

자신의 컴퓨터에 앉아 개발자가 개발 환경에서 발생 하는 오류 발생 합니다. 그녀는 예외 정보 예외 세부 정보 YSOD 표시 되며 오류가 발생 했을 때 수행 된 그녀 단계 알고 있습니다. 하지만 개발자가 최종 사용자 사이트를 방문 하 여 오류를 보고 시간이 하지 않으면 오류가 발생 했음을 알지 프로덕션에서 오류가 발생 합니다. 및 사용자가 자신의 방식으로 예외 유형, 메시지 및 스택 추적을 수정 하는 커녕 오류의 원인을 진단 하기 어려울 수 알지 못해도 오류가 발생 하는 개발 팀 경고를 벗어날 경우에 합니다.

일부 영구 저장소 (예: 데이터베이스) 있는를 프로덕션 환경에서 모든 오류가 기록 됩니다 있는지 방식을 나타낸다는 이러한 이유로 개발자는이 오류 경고가 표시 됩니다. 사용자 지정 오류 페이지에는이 로깅 및 알림 작업을 수행 하는 것이 좋습니다 처럼 보입니다. 그러나 사용자 지정 오류 페이지 오류 세부 정보를 액세스 하지 못합니다 및 하므로이 정보를 기록 하는 데 사용할 수 없습니다. 좋은 소식은 오류 세부 정보를 차단 하 고, 로그 방법은 많이 하는 다음 세 개의 자습서 탐색이 항목에서는 좀 더 자세히 보여 줍니다.

## <a name="using-different-custom-error-pages-for-different-http-error-statuses"></a>다른 HTTP 오류 상태에 대 한 다른 사용자 지정 오류 페이지를 사용 하 여

ASP.NET 페이지에서 예외가 발생 했으며 처리 되지 않은, 경우 예외를 구성된 오류 페이지를 표시 하는 ASP.NET 런타임 최대 percolates 합니다. 요청을 ASP.NET 엔진에는 있지만 어떤 이유로 처리할 수 없습니다-아마도 요청된 된 파일은 찾을 수 없거나 읽기 권한을 파일에 대 한 비활성화 된 경우 ASP.NET 엔진을 `HttpException`입니다. ASP.NET 페이지에서 발생 하는 예외와 같은이 예외를 적절 한 오류 페이지 표시를 일으키는 런타임을 전달 합니다.

프로덕션 환경에서 웹 응용 프로그램에 대 한 의미 하는 경우 사용자는 사용자 지정 오류 페이지를 볼 수 없는 페이지를 요청 합니다. **그림 6** 이러한 예를 보여 줍니다. 존재 하지 않는 페이지에 대 한 요청 이므로 (`NoSuchPage.aspx`), `HttpException` throw 되 고 사용자 지정 오류 페이지가 표시 됩니다 (에 대 한 참조를 확인 `NoSuchPage.aspx` 에서 `aspxerrorpath` querystring 매개 변수).

[![](displaying-a-custom-error-page-cs/_static/image16.png)](displaying-a-custom-error-page-cs/_static/image15.png)

**그림 6**: ASP.NET 런타임 응답을 표시 구성 오류 페이지에 잘못 된 요청 ([큰 이미지를 보려면 클릭](displaying-a-custom-error-page-cs/_static/image17.png))

기본적으로 모든 유형의 오류는 동일한 사용자 지정 오류 페이지 표시에 발생 합니다. 그러나 사용 하 여 특정 HTTP 상태 코드를 다른 사용자 지정 오류 페이지를 지정할 수 있습니다 `<error>` 내에서 자식 요소는 `<customErrors>` 섹션입니다. 예를 들어 업데이트에 페이지를 찾을 수 있는 HTTP 상태 코드 404 오류를 발생 시 표시 되는 다른 오류 페이지를는 `<customErrors>` 절에 다음 태그를 포함 합니다.

[!code-xml[Main](displaying-a-custom-error-page-cs/samples/sample2.xml)]

이 변경을 사용 하 여 원격으로 방문한 사용자 존재 하지 않는 ASP.NET 리소스를 요청할 때마다 리디렉션됩니다에 `404.aspx` 대신 사용자 지정 오류 페이지 `Oops.aspx`합니다. 로 **그림 7** 있듯이 `404.aspx` 페이지에는 일반 사용자 지정 오류 페이지에는 보다 구체적인 메시지가 포함 될 수 있습니다.

> [!NOTE]
> 체크 아웃 [404 오류 페이지를 하나 더 시간](http://www.smashingmagazine.com/2009/01/29/404-error-pages-one-more-time/) 효과적인 404 오류 페이지를 만들기에 대 한 지침에 대 한 합니다.


[![](displaying-a-custom-error-page-cs/_static/image19.png)](displaying-a-custom-error-page-cs/_static/image18.png)**그림 7**: 사용자 지정 404 오류 페이지 보다 구체적인된 메시지가 표시 됩니다. `Oops.aspx`  
 ([클릭 하 여 큰 이미지 보기](displaying-a-custom-error-page-cs/_static/image20.png)) 

알고 있으므로 `404.aspx` 페이지만 하면 찾을 수 없는 페이지에 대 한 요청에 도달 하면, 사용자가이 특정 유형의 오류를 해결할 수 있도록 하는 기능을 포함 하려면이 사용자 지정 오류 페이지를 향상 시킬 수 있습니다. 예를 들어, 있습니다 수 적절 한 Url에 잘못 된 Url을 알려진으로 매핑되는 데이터베이스 테이블을 작성 한 후의 `404.aspx` 테이블과 페이지를 사용자에 도달 하려고 할 수 있습니다를 제안 하는 사용자 지정 오류 페이지에 대 한 쿼리를 실행 합니다.

> [!NOTE]
> 사용자 지정 오류 페이지는 ASP.NET 엔진에서 처리 하는 리소스에는 요청이 만들어질 때에 표시 됩니다. 설명한 대로 합니다 [IIS 간의 차이점 Core 및 ASP.NET Development Server](core-differences-between-iis-and-the-asp-net-development-server-cs.md) 자습서, 웹 서버 수 특정 요청을 처리 자체입니다. 기본적으로 IIS 웹 ASP.NET 엔진을 호출 하지 않고 HTML 파일 및 이미지와 같은 정적 콘텐츠에 대 한 서버 프로세스 요청 합니다. 따라서 존재 하지 않는 이미지 파일을 요청 하는 경우 이러한 드리겠습니다 ASP 보다는 IIS의 기본 404 오류 메시지입니다. NET의 오류 페이지를 구성 합니다.


## <a name="summary"></a>요약

사용자에 게 세 가지 오류 페이지 중 표시 ASP.NET 응용 프로그램에서 처리 되지 않은 예외가 발생 합니다: 예외 세부 정보 노란색 화면의 쇠퇴; 런타임 오류; 퍼플 스크린이 노란색 또는 사용자 지정 오류 페이지입니다. 응용 프로그램에 따라 달라 집니다는 오류 페이지가 표시 됩니다 `<customErrors>` 구성 및 로컬 또는 원격으로 사용자가 방문 하는 여부. 기본 동작은 로컬 방문자에 게 예외 세부 정보 YSOD 및 런타임 오류 YSOD 원격 방문자에 게 표시 합니다.

런타임 오류 YSOD 숨깁니다 사이트를 방문 하는 사용자의 잠재적으로 중요 한 오류 정보를 표시 하는 동안 사이트의 모양과 느낌에서 중단 하 고 잘못 된 코드를 확인 하는 응용 프로그램을 만듭니다. 사용자 지정 오류 페이지 디자인을 만들고 해당 URL을 지정 해야 하는 사용자 지정 오류 페이지를 사용 하는 것이 좋습니다 합니다 `<customErrors>` 섹션의 `defaultRedirect` 특성입니다. 다른 HTTP 오류 상태에 대 한 여러 사용자 지정 오류 페이지도 있습니다.

사용자 지정 오류 페이지에는 프로덕션 환경에서 웹 사이트에 대 한 전략을 처리 하는 포괄적인 오류에서 첫 번째 단계입니다. 오류의 개발자에 게 경고와 해당 세부 정보 로깅 중요 한 단계도 됩니다. 다음 세 개의 자습서 오류 알림 및 로깅에 대 한 기법을 살펴봅니다.

즐거운 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [오류 페이지, 한 번 더](http://www.smashingmagazine.com/2009/01/29/404-error-pages-one-more-time/)
- [예외 디자인 지침](https://msdn.microsoft.com/library/ms229014.aspx)
- [친숙 한 오류 페이지](http://aspnet.4guysfromrolla.com/articles/090606-1.aspx)
- [예외 처리 및 Throw](https://msdn.microsoft.com/library/5b2yeyab.aspx)
- [ASP.NET에서 사용자 지정 오류 페이지를 올바르게 사용](http://professionalaspnet.com/archive/2007/09/30/Properly-Using-Custom-Error-Pages-in-ASP.NET.aspx)

> [!div class="step-by-step"]
> [이전](strategies-for-database-development-and-deployment-cs.md)
> [다음](processing-unhandled-exceptions-cs.md)
