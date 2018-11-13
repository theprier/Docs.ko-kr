---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/publishing
title: Introducing ASP.NET Web Pages-WebMatrix를 사용 하 여 사이트를 게시 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서는 ASP.NET Web Pages 및 Microsoft WebMatrix를 소개 하는 자습서 집합에서 마지막 3 부입니다. T 사이트를 게시 하는 방법에 설명 하는 중...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 7e85c70e-1a88-4408-8b3d-29611c7713ed
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/publishing
msc.type: authoredcontent
ms.openlocfilehash: fe196e5db8fd1cecbe84b2eb970939303f9313d1
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51021458"
---
<a name="introducing-aspnet-web-pages---publishing-a-site-by-using-webmatrix"></a>ASP.NET Web Pages-WebMatrix를 사용 하 여 사이트를 게시 소개
====================
[Tom FitzMacken](https://github.com/tfitzmac)

> 이 자습서는 ASP.NET Web Pages 및 Microsoft WebMatrix를 소개 하는 자습서 집합에서 마지막 3 부입니다. 다른 사용자가 작업할 수 있도록 사이트를 인터넷에 게시 하는 방법에 설명 합니다. 통해 시리즈를 완료 했다고 가정 하 [ASP.NET Web Pages 사이트에 대 한 일관성 확인을 만드는](https://go.microsoft.com/fwlink/?LinkId=251585)합니다.
> 
> 사용 하 여 사이트를 게시 하는 방법을 알아봅니다.
> 
> - Microsoft Azure
> - 웹 호스팅 업체


## <a name="about-publishing-your-site"></a>사이트를 게시 하는 방법에 대 한

지금 까지는 테스트 페이지를 비롯 하 여 로컬 컴퓨터에서 모든 작업을 완료 했으면 합니다. 실행 하 여<em>.cshtml</em> 페이지, WebMatrix, IIS Express namely에 기본 제공 되는 웹 서버를 사용 했습니다. 하지만 물론 온다는 점만 다릅니다 만든 사이트를 볼 수 없습니다. 사용자 사이트를 사용 하 여 작업을 수 있게 하려면 인터넷에 게시 해야 합니다.

게시 된 계정이 있다고 의미 공용 웹 서버에 대 한 액세스를 이미 없다면를 *클라우드 플랫폼* 또는 *호스팅 공급자*합니다. Microsoft Azure와 같은 클라우드 플랫폼, 응용 프로그램에 대 한 주문형 인프라를 제공합니다. 호스팅 공급자는 공개적으로 액세스할 수 있는 웹 서버를 소유 하 고 있습니다 임대는 회사 사이트에 대 한 공간. 호스팅 계획 한 달에 몇 달러에서 실행 (또는 무료)에 수백 달러 대규모 상업용 웹 사이트에 대 한 한 달의 소규모 사이트에 대 한 합니다.

> [!NOTE]
> 집에 인터넷 서비스를 가져오는 데 사용할 수 있는 인터넷 서비스 공급자 (ISP)를 통해 공용 웹 서버에 대 한 액세스를 해야 합니다. 그러나 호스팅 공급자는 ASP.NET 웹 페이지를 지원 해야 합니다. 여러 Isp 하지 않으면 하지만 가치가 항상 확인 합니다.


이 자습서에서는 게시 하는 방법에 간략하게를 살펴보겠습니다. 이 아니므로 모든 것에 대 한 정확한 세부 정보를 제공 하는 데 적합 프로세스는 모든 호스팅 공급자에 대 한 약간 달라 집니다. 하지만 프로세스의 작동 방식을 잘 받게 됩니다.

이 자습서는 4 개의 섹션이 포함 되어 있습니다.

1. [기본 페이지 설정](#defaultpage)
2. 게시 (다음 중 하나를 선택)  
 a. [Microsoft Azure 사이트에 게시](#azure)  
 b. [웹 호스팅 회사 사이트에 게시](#host)
3. [라이브 사이트를 업데이트 하는 중: 다시 게시](#update)

<a id="defaultpage"></a>
## <a name="setting-up-the-default-page"></a>기본 페이지 설정

사용자가 웹 사이트에 대 한 기본 주소를 탐색 하는 경우 사이트에 대 한 기본 페이지는 사용자에 게 표시 됩니다. 예를 들어 사이트에 대 한 기본 페이지로 www.contoso.com에 Default.htm으로 설정 하면 다음 이동할 <strong>(www.contoso.com)[www.contoso.com]</strong> 로 이동 하는 것과 같습니다 <strong>www.contoso.com/Default.htm</strong>합니다.

사이트에서 사용 하는 현재 **Default.cshtml** 기본 페이지와 합니다. 이 페이지는 사용자의 기본 페이지에 적합 하지만이 자습서에서는 추가 하지 않은 내용이 해당 페이지에 있으므로 빈 페이지가 표시 됩니다. Default.cshtml 열고 내용을 다음 코드로 바꿉니다.

[!code-cshtml[Main](publishing/samples/sample1.cshtml)]

이제 사이트 게시에 대 한 준비 되었습니다. 먼저 사이트를 Azure에 배포 하는 방법 및 그런 다음 웹 호스팅 회사에 배포 하는 방법을 표시 됩니다. 웹 사이트에 둘 다 옵션 작동 배포 옵션 중 하나를 수행 해야 합니다.

<a id="azure"></a>
## <a name="publishing-your-site-to-microsoft-azure"></a>Microsoft Azure 사이트에 게시

이 자습서는 Microsoft azure 사이트를 배포 하는 방법을 먼저 표시 됩니다. Microsoft 계정으로 로그인 하 여 Azure에서 최대 10 개의 무료 사이트를 만들 수 있습니다. 이러한 무료 사이트는 사이트를 테스트 하는 편리한 방법을 제공 합니다. 항상 모든 사용 가능한 사이트를 사용 하지 않기 위해 나중에이 예제에서는 사이트를 삭제할 수 있습니다. 몇 분만에 무료 평가판 계정을 만들 수 있습니다. 자세한 내용은 참조 하세요 [Azure 무료 평가판](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)합니다.

WebMatrix 리본을 클릭 합니다 **게시** 단추입니다.

![WebMatrix 리본 메뉴의 'publish' 단추](publishing/_static/image1.png)

합니다 **사이트 게시** 대화 상자가 표시 됩니다. Microsoft 계정에 로그인 하지 않은 경우에 대화 상자 포함 됩니다는 **Azure 시작** 링크 합니다. 이 링크를 클릭 합니다.

![사이트 게시](publishing/_static/image2.png)

Microsoft 계정으로 로그인 하지 않은 경우 다시 로그인 할 수 있는 기회를 제공 됩니다. Azure에서 사이트를 게시 하려면 Microsoft 계정으로 로그인 해야 합니다.

![링크를](publishing/_static/image3.png)

Microsoft 계정에 로그인 한 후 대화 상자에 Azure에서 새 사이트를 만들거나 Azure에서 기존 사이트 중 하나에 연결에 대 한 링크가 포함 되어 있습니다.

![새 사이트 만들기](publishing/_static/image4.png)

선택 **새 사이트 만들기**합니다.

프로젝트 이름을 **WebPagesMovies**, 사이트의 기본 이름은 **webpagesmovies.azurewebsites.net**합니다. 이 기본 이름은 가능성이 빨간색 느낌표가 표시 된 대로 제공 되지 않습니다.

![기본 웹 사이트 이름](publishing/_static/image5.png)

를 사용할 수 있는 사이트 이름을 변경 하 고 사용자의 위치와 가까운 위치를 선택 합니다.

![변경 된 사이트 이름](publishing/_static/image6.png)

**확인**을 클릭합니다.

WebMatrix performss 서버 사이트와 호환 되는지 확인 하는 테스트 합니다.

![호환성 테스트](publishing/_static/image7.png)

선택 **계속**합니다.

호환성 테스트의 결과가 표시 됩니다.

![호환성 결과](publishing/_static/image8.png)

선택 **계속**합니다.

WebMatrix에는 파일 및 사이트에 게시 되는 데이터베이스를 표시 합니다. 사이트를 게시 하는 첫 번째 시간 이므로 모든 파일이 나열 됩니다. 게시할 준비가 되지 않은 파일을 취소할 수 있습니다. 후속 게시에서 변경 된 파일만 표시 됩니다. 참조 [라이브 사이트를 업데이트 하는 중: 재게시](#update)합니다.

![게시 미리 보기](publishing/_static/image9.png)

선택 **계속**합니다.

사이트에 Azure에 배포 된 후 배포가 완료 되었음을 나타내는 메시지가 표시 됩니다.

![게시 완료](publishing/_static/image10.png)

에 사이트 및 데이터베이스를 Azure에 게시 된 공개적으로 사용할 수 있습니다. 게시 완료 되 고 표시 되며 배포 된 사이트를 나타내는 메시지에 대 한 링크를 클릭 합니다. 인터넷에 연결 된 모든 사용자 추가 하거나 데이터베이스의 레코드를 수정할 수 있습니다.

![](publishing/_static/image11.png)

<a id="host"></a>
## <a name="publishing-your-site-to-a-web-hosting-company"></a>웹 호스팅 회사 사이트에 게시

Azure에 게시 하지 않으려면 웹 호스팅 회사를 대신 사이트를 게시할 수 있습니다.

클릭 합니다 **웹 호스팅 찾기** 링크 합니다.

![게시 설정 대화 상자에서 '웹 호스팅 찾기' 단추](publishing/_static/image12.png)

ASP.NET을 지 원하는 호스팅 공급자를 나열 하는 Microsoft 사이트에서 페이지로 이동 합니다.

![호스팅 공급자를 나열 하는 Microsoft 사이트의 페이지](publishing/_static/image13.png)

물론, 정확 하 게 호스팅 기능 장기간 동안 필요할 수 이제 알아야 어려울 수 있습니다. 두 가지 사항 고려해 야 할 다음과 같습니다.

- WebPagesMovies 사이트를 위해 별도 추가 기능을 추가 비용 자주 하는 SQL Server에 필요가 없습니다. 사이트에서 사용 하는 SQL Server Compact Edition에는 자체 포함 합니다. 그러나 일부 이후 웹 사이트 작업에 대 한 SQL Server 액세스를 해야 합니다. 수 있다면 나중에 SQL Server 기능을 추가할 수 있는지 확인 합니다.
- 호스팅 공급자는 웹 배포 게시 프로토콜을 지원 하는지 여부를 확인 합니다. FTP 프로토콜을 사용 하 여 게시할 수 이지만 웹 배포를 사용 하는 것이 편리 합니다.

일부 사이트를 무료 평가 기간을 제공합니다. 무료 평가판을 게시를 시도 하는 좋은 방법 이며 WebMatrix 및 ASP.NET Web Pages를 사용 하 여 여전히 시험해 하는 동안 호스트 합니다.

하나를 선택 합니다. 이 자습서에서는 했으므로 자습서 등을 만드는 것 하는 동안 해당 회사 몇 개월 동안 무료 사이트를 호스트할 수 있게 해 주는 홍보 행사 DiscountASP.NET를 선택 합니다.

> [!NOTE]
> 이 자습서에 대 한 호스팅 공급자의 원하는 다른 언어가 해당 회사는 인증으로 해석 해서는 안 됩니다. 하지만 그림에 대 한 하나를 선택 해야 하 고 DiscountASP.NET 게시에 대 한 ASP.NET Web Pages 및 Web Deploy 프로토콜을 지 원하는 많은 회사 중 하나인 메시지를 표시 합니다.


일반적으로 호스팅 공급자를 사용 하 여 등록 한 후에 회사 사용자 이름 및 암호를 웹 서버 및 등의 URL 포함 하는 전자 메일이 있습니다 보냅니다. 호스팅 회사 Web Deploy 프로토콜을 지 원하는 경우 수 나에 게 보낼 수 있는 파일 게시 설정 다운로드할 수 있습니다. 게시 설정 파일 수에 대 한 프로세스를 간소화합니다.

등록 하 고 게시할 준비가 되 면 클릭 합니다 **게시** WebMatrix 리본에서 단추입니다. 합니다 **게시 설정** 대화 상자가 표시 됩니다.

호스팅 공급자는 게시 설정 파일을 전송를 클릭 합니다 **게시 설정 가져오기** 에 연결 하 고 파일을 가져옵니다. 게시 설정 파일에 없는 경우 호스팅 회사 전자 메일에서 전송 하는 값을 사용 하 여 필드에 입력 합니다. 같습니다 합니다 **게시 설정** 대화 상자 완료 되 면 다음과 같을 수 있습니다.

![게시 설정 대화 상자에서 게시 설정 입력](publishing/_static/image14.png)

클릭 **연결의 유효성을 검사**합니다. 모든 경우 확인 대화 상자를 보고 **성공적으로 연결**, 즉 호스팅 공급자의 서버와 통신할 수 있습니다.

![성공 이면 메시지를 게시 설정이 올바른지](publishing/_static/image15.png)

문제가 있으면 WebMatrix는 문제가 무엇 인지 알려줍니다.

![오류 메시지에 문제가 있으면 게시 설정](publishing/_static/image16.png)

클릭 **저장할** 여 설정을 저장 합니다. WebMatrix 호스팅 사이트와 올바르게 통신할 수 있는지 확인 하기 위한 테스트를 수행할 것을 제안 합니다.

![게시 프로세스의 테스트를 수행 하려면 제공 된 메시지](publishing/_static/image17.png)

**예**를 클릭합니다. WebMatrix는 호스팅 공급자에 샘플 파일을 업로드합니다. 호환성 테스트가 완료 되 면 WebMatrix 결과 보고 합니다.

![게시 테스트의 결과](publishing/_static/image18.png)

클릭 해 보면 이동할 준비가 **계속** 실제 게시 프로세스를 시작 합니다. 어떤 파일과 사이트에 호스트 서버 (지금은 없음)에 포함 되어 및 게시 프로세스의 미리 보기를 사용 하면 WebMatrix 파악 합니다.

![게시 프로세스를 업로드 하는 어떤 파일의 미리 보기](publishing/_static/image19.png)

사용자가 만든 같은 웹 페이지를 포함 하는 게시할 파일 목록이 *Movies.cshtml*합니다. 목록 파일을 데이터베이스에 대 한 SQL Server Compact Edition을 실행 하 고 등를 설치한 다음 도우미에 대 한 파일도 포함 됩니다. 결과적으로, 초기 게시 프로세스 길 수 있습니다.

**Continue(계속)** 를 클릭합니다. WebMatrix는 호스팅 공급자의 서버에 파일을 복사합니다. 완료 되 면 상태 표시줄에는 결과가 보고:

![게시 프로세스가 성공적으로 완료 하는 경우 상태 표시줄 메시지](publishing/_static/image20.png)

라이브 사이트를 확인 하려면 상태 표시줄의 링크를 클릭 합니다. 추가 *영화* URL로 확인할 수는 *Movies.cshtml* 만든 파일:

![동영상 페이지를 보여 주는 라이브 사이트](publishing/_static/image21.png)

<a id="update"></a>
## <a name="updating-the-live-site-republishing"></a>라이브 사이트를 업데이트 하는 중: 다시 게시

두 개의 복사본이 가지 사이트 (Azure 또는 웹 호스팅 회사)에 게시 한 후 &mdash; 컴퓨터 및 서비스 공급자의 버전에서 버전입니다. 사이트를 개발 합니다. 계속 하 고 싶을 (발표자 노트를 다음 자습서 집합의 일부로). 이렇게 하면 서비스 공급자 컴퓨터에서 변경 내용을 복사 하려면 사이트를 다시 게시 해야 합니다. WebMatrix에서 게시 프로세스는 사이트에서 파일 변경 된 항목을 확인 하 고 해당 파일을 게시할 수 있습니다.

다시 게시의 작동 원리를 보려면 합니다 *Movies.cshtml* 사이트 일부 약간만 변경 하 고 파일을 저장 합니다. 예를 들어, 제목을 변경 `Movies - Updated`합니다.

클릭 합니다 **게시** 리본에서 단추입니다. WebMatrix는 변경 내용과 게시는 파일의 미리 보기를 표시를 확인 합니다.

![다시 게시에 대 한 준비가 된 파일을 보여 주는 변경 [게시] 대화 상자](publishing/_static/image22.png)

> [!IMPORTANT] 
> 
> 기본적으로 WebMatrix 게시 데이터베이스 (*.sdf* 파일)만 처음으로 게시할 사이트입니다. 사이트에 게시 하 고 사용자 웹 사이트와 상호 작용 하는 라이브 사이트에 있는 데이터베이스는 일반적으로 사이트의 실제 데이터에 있습니다. 사용 하 여 라이브 데이터베이스를 덮어쓰지 매우 주의 해야 합니다 *.sdf* 만 테스트 데이터를 포함 하는 컴퓨터에 있는 파일입니다. 때문에 경고가 표시 **게시 원격 데이터베이스를 덮어씁니다**에 대 한 확인란 이유 및 *WebPagesMovies.sdf* 기본적으로 지워집니다.


**Continue(계속)** 를 클릭합니다. WebMatrix는 변경된 된 파일을 게시 하 고 처음으로 게시를 수행한 것과 같은 성공 메시지를 표시 합니다.

라이브 사이트 (클릭할 수 성공 메시지에 대 한 링크를 계속 표시 되는 경우)로 이동 하 고 변경 내용을 게시 된를 확인 합니다.

> [!TIP] 
> 
> **파일을 원격으로 편집**
> 
> 사이트를 변경 하 고 다음 다시 게시 하는 대신, WebMatrix에서 직접 원격 파일을 편집할 수 있습니다. 이 시나리오에서는 서비스 공급자에 있는 파일을 열고 WebMatrix 다운로드 복사본 편집 합니다. 파일을 저장할 때마다 WebMatrix 사이트에 보냅니다.
> 
> 쉬운 라이브 사이트를 변경 하는 원격으로 편집 합니다. 그러나 이러한 방식으로 변경 내용은 로컬 사이트의 파일을 사용 하 여 동기화 되지 않았습니다. 원격 사이트를 사용 하 여 로컬 파일을 동기화 하려면 원격 파일을 다운로드할 수 있습니다. 이 프로세스 유사 하 게 작동 게시를 제외 하 고 반대로 합니다.
> 
> 원격 편집 하 고 원격 다운로드 기능 WebMatrix의 여기에 대 한 더 설명 하지 않습니다. 여러 사용자가 다른 컴퓨터에서 동일한 사이트에서 작동 하도록 하는 경우 매우 유용 합니다. 자세한 내용은 [게시 하 고 WebMatrix 2 베타를 사용 하 여 원격 사이트 편집](https://go.microsoft.com/fwlink/?LinkId=251591)합니다.


## <a name="additional-resources"></a>추가 리소스

- [ASP.NET WebMatrix ASP.NET Web Pages 포럼](https://forums.asp.net/1224.aspx/1?WebMatrix+and+ASP+NET+Web+Pages), 게시를 살펴보는 질문 및 답변 합니다.

> [!div class="step-by-step"]
> [이전](layouts.md)
