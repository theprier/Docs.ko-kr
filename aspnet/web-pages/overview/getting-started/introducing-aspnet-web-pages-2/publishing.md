---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/publishing
title: "ASP.NET 웹 페이지를 소개-WebMatrix를 사용 하 여 사이트를 게시 | Microsoft Docs"
author: tfitzmac
description: "이 자습서에서 Microsoft WebMatrix 및 ASP.NET 웹 페이지를 소개 하는 자습서 집합입니다. T 사이트를 게시 하는 방법에 설명..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/28/2015
ms.topic: article
ms.assetid: 7e85c70e-1a88-4408-8b3d-29611c7713ed
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/publishing
msc.type: authoredcontent
ms.openlocfilehash: 1e718c92a2f94df50fcf7af6859917746a4982ac
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="introducing-aspnet-web-pages---publishing-a-site-by-using-webmatrix"></a>WebMatrix를 사용 하 여 사이트를 게시 하는 ASP.NET 웹 페이지-소개
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 자습서에서 Microsoft WebMatrix 및 ASP.NET 웹 페이지를 소개 하는 자습서 집합입니다. 다른 사람이 사용할 수 있도록 사이트를 인터넷에 게시 하는 방법을 설명 합니다. 통해 시리즈를 완료 한 것으로 가정 [ASP.NET 웹 페이지 사이트에 대 한 일관성 확인을 만드는](https://go.microsoft.com/fwlink/?LinkId=251585)합니다.
> 
> 사용 하 여 사이트를 게시 하는 방법을 배웁니다.
> 
> - Microsoft Azure
> - 웹 호스팅 회사


## <a name="about-publishing-your-site"></a>사이트에 게시 하는 방법에 대 한

지금 까지는 페이지 테스트를 비롯 하 여 로컬 컴퓨터에서 모든 작업 작업을 수행 하면 됩니다. 실행 하 여*.cshtml* 페이지를 사용한 적이 있다면 WebMatrix, IIS Express 즉에 기본 제공 되는 웹 서버입니다. 하지만 물론 온다는 점만 다릅니다 만든 사이트를 볼 수 사람이 없습니다. 사용자 사이트와 함께 작업을 수 있게 하려면 인터넷에 게시 해야 합니다.

게시 포함 된 계정을 보유 해야 한다는 의미는 공용 웹 서버에 대 한 액세스를 이미 있는 경우가 아니면는 *클라우드 플랫폼* 또는 *호스팅 공급자*합니다. Microsoft Azure 같은 클라우드 플랫폼 응용 프로그램에 대 한 주문형 인프라를 제공합니다. 호스팅 공급자는 공개적으로 액세스할 수 있는 웹 서버를 소유 하 고 있습니다 됩니다 대 여 회사 사이트에 대 한 공간. 호스팅 계획 한 달에 몇 달러 실행 (또는 심지어 무료) 한 달 대규모 상용 웹 사이트에 대 한 달러의 많은 수백 소규모 사이트입니다.

> [!NOTE]
> 인터넷 서비스 집에서 가져오는 데 사용할 수 있는 인터넷 서비스 공급자 (ISP)를 통해 공용 웹 서버에 대 한 액세스를 할 수 있습니다. 그러나 호스팅 공급자는 ASP.NET 웹 페이지를 지원 해야 합니다. 많은 Isp 하지 하지만 항상 검사 합니다.


이 자습서에서는 게시 하는 방법에 대해 간략하게를 하겠습니다. 프로세스는 모든 호스팅 공급자에 대 한 약간 다르기 때문에 모든 항목에 대 한 정확한 세부 정보를 제공 하지 유용 합니다. 하지만 프로세스의 작동 방식에 대 한 유용한 정보를 얻게 됩니다.

이 자습서에는 4 개의 섹션이 포함 됩니다.

1. [기본 페이지 설정](#defaultpage)
2. 게시 (다음 중 하나를 선택)  
 a. [Microsoft Azure 사이트에 게시](#azure)  
 b. [웹 호스팅 회사 사이트에 게시](#host)
3. [라이브 사이트 업데이트: 다시 게시](#update)

<a id="defaultpage"></a>
## <a name="setting-up-the-default-page"></a>기본 페이지 설정

사용자가 웹 사이트에 대 한 기본 주소를 탐색 하는 경우 사이트에 대 한 기본 페이지가 사용자에 게 표시 됩니다. 예를 들어 Default.htm www.contoso.com에는 사이트에 대 한 기본 페이지로 설정 되 면 다음로 이동 **www.contoso.com** 로 이동 하는 것과 같습니다 **www.contoso.com/Default.htm**합니다.

사이트에서 사용 하는 현재 **Default.cshtml** 기본 페이지로 합니다. 이 페이지는 사용자의 기본 페이지에 대 한 세밀 하 게 하지만이 자습서에서는 추가 하지 않은 모든 콘텐츠 해당 페이지에는 빈 페이지를 표시 하도록 합니다. Default.cshtml 열고 콘텐츠를 다음 코드로 바꿉니다.

[!code-cshtml[Main](publishing/samples/sample1.cshtml)]

사이트에 게시할 준비가 됩니다. 첫째, 사이트, Azure로 배포 하는 방법 및 웹 호스팅 회사에 배포 하는 방법 나타납니다. 웹 사이트가 있으며 둘 다 옵션 작동 배포 옵션 중 하나를 수행 해야 합니다.

<a id="azure"></a>
## <a name="publishing-your-site-to-microsoft-azure"></a>Microsoft Azure 사이트에 게시

이 자습서는 Microsoft azure 사이트를 배포 하는 방법을 먼저 표시 됩니다. Microsoft 계정, 로그인 하 여 Azure에서 최대 10 개의 무료 사이트를 만들 수 있습니다. 이러한 무료 사이트는 사이트를 테스트 하는 편리한 방법을 제공 합니다. 항상 모든 사용 가능한 사이트를 사용 하지 않도록 하려면 나중에이 예제에서는 사이트를 삭제할 수 있습니다. 몇 분에서에서 무료 평가판 계정을 만들 수 있습니다. 자세한 내용은 참조 [Azure 무료 평가판](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)합니다.

WebMatrix 리본에서는 **게시** 단추입니다.

![WebMatrix 리본 메뉴의 'publish' 단추](publishing/_static/image1.png)

**사이트 게시** 대화 상자가 표시 됩니다. Microsoft 계정에 로그인 하지 않은 경우에 대화 상자가 포함 됩니다는 **Azure를 시작** 링크 합니다. 이 링크를 클릭 합니다.

![사이트 게시](publishing/_static/image2.png)

Microsoft 계정에 로그인 하지 않은 경우 로그인 할 수 있는 기회를 다시 제공 됩니다. Azure에서 사이트를 게시 하려면 Microsoft 계정에 로그인 해야 합니다.

![링크를](publishing/_static/image3.png)

Microsoft 계정에 로그인 한 후 대화 상자는 Azure에서 새 사이트를 만들거나 Azure에서 기존 사이트 중 하나에 연결 하는 링크를 포함 합니다.

![새 사이트 만들기](publishing/_static/image4.png)

선택 **새 사이트를 만들**합니다.

프로젝트의 이름을 **WebPagesMovies**, 사이트에 대 한 기본 이름은 **webpagesmovies.azurewebsites.net**합니다. 이 기본 이름은 가능성이 가장 높은 빨간색 느낌표가 표시 된 대로 사용할 수 있는 없습니다.

![기본 웹 사이트 이름](publishing/_static/image5.png)

를 사용할 수 있는 사이트 이름을 변경 하 고 사용자의 위치 가까이 있는 위치를 선택 합니다.

![변경 된 사이트 이름](publishing/_static/image6.png)

**확인**을 클릭합니다.

WebMatrix performss 서버 사이트와 호환 되는지 확인 하는 테스트 합니다.

![호환성 테스트](publishing/_static/image7.png)

선택 **계속**합니다.

호환성 테스트 결과가 표시 됩니다.

![호환성 결과](publishing/_static/image8.png)

선택 **계속**합니다.

WebMatrix는 파일 및 사이트에 게시 되는 데이터베이스를 표시 합니다. 이 사이트를 게시 하는 처음으로 이므로 파일을 모두 나열 됩니다. 게시할 준비가 되지 않은 파일이 선택을 취소할 수 있습니다. 후속 게시에서 변경 된 파일만 표시 됩니다. 참조 [라이브 사이트 업데이트: 재게시](#update)합니다.

![게시 미리 보기](publishing/_static/image9.png)

선택 **계속**합니다.

사이트에 Azure에 배포 된 배포 완료 되었음을 나타내는 메시지가 표시 됩니다.

![전체 게시](publishing/_static/image10.png)

사이트 및 데이터베이스를 Azure에 게시 된 및 공개적으로 제공 됩니다. 게시가 완료 되 고 사이트에 배포 된 표시를 나타내는 메시지의 링크를 클릭 합니다. 인터넷에 연결 된 모든 사용자를 추가 하거나 데이터베이스에서 레코드를 수정할 수 있습니다.

![](publishing/_static/image11.png)

<a id="host"></a>
## <a name="publishing-your-site-to-a-web-hosting-company"></a>웹 호스팅 회사 사이트에 게시

Azure에 게시 하지 않으려면 사이트는 웹 호스팅 회사를 대신 게시할 수 있습니다.

클릭는 **웹 호스팅 찾기** 링크 합니다.

![게시 설정 대화 상자에서 '웹 호스팅 찾기' 단추](publishing/_static/image12.png)

ASP.NET을 지 원하는 호스팅 공급자를 나열 하는 Microsoft 사이트는 페이지로 이동 합니다.

![호스팅 공급자를 나열 하는 Microsoft 사이트에서 페이지](publishing/_static/image13.png)

물론, 장기간 동안 필요할 수 있습니다 호스팅 기능 정확히 알고 이제 어려울 수 있습니다. 다음은 몇 가지 고려 사항입니다.

- WebPagesMovies 사이트를 위해 추가 비용이 자주 하는 SQL Server에 대 한 별도 추가 기능을 포함 필요가 없습니다. 사이트에 사용 하는 SQL Server Compact Edition는 독립적인 항목입니다. 그러나 수행 하는 몇 가지 이후 웹 사이트 작업에 대 한 SQL Server 액세스를 할 수 있습니다. 생각 되 면 나중에 SQL Server 기능을 추가할 수 있는지 확인 합니다.
- 호스팅 공급자는 웹 배포 게시 프로토콜을 지원 하는지 여부를 확인 합니다. FTP 프로토콜을 사용 하 여 게시할 수는 있지만 웹 배포 사용 하려면 편리 합니다.

일부 사이트 무료 평가 기간을 제공합니다. 무료 평가판 이면 게시를 시도 하는 좋은 방법 및 동안 호스팅 중인 계속 작업할 수 있도록 WebMatrix 및 ASP.NET 웹 페이지입니다.

마음에 드는 선택 합니다. 이 자습서에서는 있기 때문에 자습서 등을 만드는 것 하는 동안 해당 회사 사이트에 대 한 몇 개월 무료 사용자 수 있도록 프로 모션 DiscountASP.NET를 선택 합니다.

> [!NOTE]
> 이 자습서에 대 한 호스팅 공급자의 선택한 다른 언어가 해당 회사의 인증으로 해석 해서는 안 합니다. 이해를 돕기 하나를 선택 해야 하지만 DiscountASP.NET 게시에 대 한 ASP.NET 웹 페이지 및 Web Deploy 프로토콜을 지 원하는 된 많은 회사 중 하나입니다.


일반적으로 호스팅 공급자와 함께 등록 한 후에 회사 사용자 이름 및 암호를 웹 서버 및 등의 URL 포함 하는 메일 있습니다 보냅니다. 호스팅 회사에 Web Deploy 프로토콜을 지 원하는 경우 포함 하는 파일 게시 설정 하거나 하나를 다운로드 하면 보내는 수 있습니다. 게시 설정 파일을 간단 하 게 합니다.

가입 하 고 게시할 준비가 되 면 클릭는 **게시** WebMatrix 리본 메뉴의 단추입니다. **게시 설정** 대화 상자가 표시 됩니다.

호스팅 공급자는 게시 설정 파일을 전송, 클릭는 **게시 설정 가져오기** 에 연결 하 고 파일을 가져옵니다. 호스팅 회사 전자 메일의 보낸 사람 값을 사용 하 여 게시 설정 파일에 없을 경우 필드에 입력 합니다. 다음은 무엇는 **게시 설정** 대화 상자를 완료 하면 같을 수 있습니다.

![게시 설정 대화 상자에서 게시 설정 입력](publishing/_static/image14.png)

클릭 **연결 확인**합니다. 대화 상자를 보고 하는 경우 모든 텍스트가 유효함을 **성공적으로 연결**, 호스팅 공급자의 서버와 통신할 수 있다는 의미입니다.

![성공 하는 경우 메시지 게시 설정이 올바른지](publishing/_static/image15.png)

문제가 경우 WebMatrix 문제가 무엇 인지 파악 하 최적화를 수행 합니다.

![문제가 있는 경우 오류 메시지 게시 설정](publishing/_static/image16.png)

클릭 **저장** 여 설정을 저장 합니다. WebMatrix는 호스팅 사이트와 올바르게 통신할 수 있는지 확인 하는 테스트를 수행 하는 제공 합니다.

![게시 프로세스의 테스트를 수행 하려면 제공 메시지](publishing/_static/image17.png)

**예**를 클릭합니다. WebMatrix는 호스팅 공급자에 몇 가지 샘플 파일을 업로드합니다. 호환성 테스트 수행 되는 경우 WebMatrix는 결과 보고 합니다.

![게시 테스트의 결과](publishing/_static/image18.png)

준비가 끝난 것 계속 진행 하 고 클릭 **계속** 실제 게시 프로세스를 시작 합니다. WebMatrix 찾습니다 어떤 파일에 사이트 및 (ा त, 없음)은 호스트 서버에 이미 있는 있으며 게시 프로세스의 미리 보기를 제공 합니다.

![게시 프로세스에 업로드 하는 파일의 미리 보기](publishing/_static/image19.png)

와 같은 사용자가 만든 웹 페이지를 포함 하는 게시 파일 목록이 *Movies.cshtml*합니다. 또한 목록 파일을 데이터베이스에 대 한 SQL Server Compact Edition을 실행 하 고 등를 설치한 다음 도우미에 대 한 파일을 포함 합니다. 결과적으로, 초기 게시 프로세스가 상당히 커질 수 있습니다.

**계속**을 클릭합니다. WebMatrix는 호스팅 공급자의 서버에 파일을 복사합니다. 완료 되 면 상태 표시줄에 결과가 보고 됩니다.

![게시 프로세스가 성공적으로 완료 되 면 상태 표시줄 메시지](publishing/_static/image20.png)

라이브 사이트를 확인 하려면 상태 표시줄에 링크를 클릭 합니다. 추가 *동영상* URL로 표시 됩니다는 *Movies.cshtml* 만든 파일:

![영화 페이지를 보여 주는 라이브 사이트](publishing/_static/image21.png)

<a id="update"></a>
## <a name="updating-the-live-site-republishing"></a>라이브 사이트 업데이트: 다시 게시

두 개 있는 사이트에 게시 (중 하나 또는 Azure에는 웹 호스팅 회사), 한 &mdash; 컴퓨터와 서비스 공급자에 있는 버전의 버전입니다. 사이트를 개발 계속 좋을 것 (여기서도 하는 경우 다음 자습서 집합의 일부로). 이렇게 하면 서비스 공급자에 게 컴퓨터에서 변경 내용을 복사 하려면 사이트를 다시 게시 해야 합니다. WebMatrix에서 게시 프로세스 파일이 사이트에서 변경 된를 확인 하 고 해당 파일을 게시 합니다.

다시 게시의 작동 방식을 확인 하려면 열고는 *Movies.cshtml* 사이트 일부 약간만 변경 하 고 다음 파일을 저장 합니다. 예를 들어 제목을 변경 `Movies - Updated`합니다.

클릭는 **게시** 리본의 단추입니다. WebMatrix 기능 변경 되 고 게시 하는 파일의 위치를 결정 합니다.

![재게시 작업을 위한 기록할 파일을 보여 주는 변경 된 [게시] 대화 상자](publishing/_static/image22.png)

> [!IMPORTANT] 
> 
> 기본적으로 WebMatrix 게시 데이터베이스 (*.sdf* 파일)만 사이트를 게시할 처음으로 합니다. 사이트에 게시 되 면 사용자 웹 사이트와 상호 작용 하는 라이브 사이트에 있는 데이터베이스는 일반적으로 사이트의 실제 데이터에 있습니다. 라이브 데이터베이스를 덮어쓰지 매우 주의 해야 할는 *.sdf* 만 테스트 데이터를 포함 하는 컴퓨터에 있는 파일입니다. 바로 이러한 이유로 경고가 표시 **게시 모든 원격 데이터베이스를 덮어쓰게 됩니다**에 대 한 확인란 이유 및 *WebPagesMovies.sdf* 은 기본적으로 선택 취소 되어 있습니다.


**계속**을 클릭합니다. WebMatrix는 변경 된 파일을 게시 하 고 처음으로 게시와 같게 성공 메시지를 표시 합니다.

라이브 사이트 (클릭할 수 있는 성공 메시지의 링크 여전히 표시)로 이동 하 고 변경 내용을 게시 되었는지 확인 합니다.

> [!TIP] 
> 
> **원격 파일 편집**
> 
> 사이트를 변경 하 고 다음 다시 게시 하는 대신, WebMatrix 원격 파일을 직접 편집할 수 있습니다. 이 시나리오에서는 서비스 공급자에 있는 파일을 열면 및 WebMatrix 다운로드는 해당 복사본을 편집할 수 있습니다. 파일을 저장할 때마다 WebMatrix 사이트는 변경 내용을 보냅니다.
> 
> 원격 편집은 쉽게 라이브 사이트를 변경 해야 합니다. 그러나 이러한 방식으로 수행한 변경 내용은 로컬 사이트에서 파일에 대해 동기화 되지 않았습니다. 로컬 파일을 원격 사이트와 동기화 하려면 원격 파일을 다운로드할 수 있습니다. 이 방법은 매우 비슷한 게시를 제외 하 고 반대 방향으로.
> 
> 원격 편집 및 다운로드 원격 기능을 WebMatrix 여기에 대 한 더 설명 하지 않습니다. 여러 사용자가 작업 서로 다른 컴퓨터에 동일한 사이트에서 수행 해야 하는 경우 매우 유용 합니다. 자세한 내용은 참조 [게시 및 WebMatrix 2 베타와 원격 사이트 편집](https://go.microsoft.com/fwlink/?LinkId=251591)합니다.


## <a name="additional-resources"></a>추가 리소스

- [ASP.NET WebMatrix ASP.NET 웹 페이지 포럼](https://forums.asp.net/1224.aspx/1?WebMatrix+and+ASP+NET+Web+Pages), 게시 하는 좋은 장소 질문 및 답변 합니다.

>[!div class="step-by-step"]
[이전](layouts.md)
