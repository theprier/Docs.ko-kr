---
uid: whitepapers/denied-access-to-iis-directories
title: ASP.NET IIS 디렉터리에 대 한 액세스가 거부 | Microsoft Docs
author: rick-anderson
description: 이 백서에서는 ASP.NET 응용 프로그램에 요청 "DirectoryName 디렉터리에 액세스 거부 오류를 반환 하는 경우 수행할 해야 작업을 설명 합니다. 합니다. S 하지 못했습니다.
ms.author: aspnetcontent
ms.date: 02/10/2010
ms.assetid: 3cb27b8a-354f-4332-bfe0-232b13bbf8aa
msc.legacyurl: /whitepapers/denied-access-to-iis-directories
msc.type: content
ms.openlocfilehash: 4853ee29d2468c4b67375123c5b2ec15089fe09b
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37842412"
---
<a name="aspnet-denied-access-to-iis-directories"></a>ASP.NET은 IIS 디렉터리에 대 한 액세스가 거부
====================
> 이 백서 작업을 설명 하는 오류를 반환 하는 ASP.NET 응용 프로그램에 요청 하는 경우 "에 대 한 액세스 거부 *DirectoryName* 디렉터리입니다. 디렉터리 변경 모니터링을 시작 하지 못했습니다. "
> 
> ASP.NET 1.0 및 ASP.NET 1.1에 적용 됩니다.


작음을 사용 하 여 실행 이제 ASP.NET V1 RTM 권한 있는 windows 계정-로컬 컴퓨터에서 "ASPNET" 계정으로 등록 합니다.

일부 시스템 잠겨이 수 기본적 읽기 웹 사이트의 콘텐츠 디렉터리, 응용 프로그램 루트 디렉터리 또는 웹 사이트 루트 디렉터리에 대 한 보안 액세스 합니다. 이 경우 오류가 표시 됩니다는 다음 지정 된 웹 응용 프로그램에서 페이지를 요청 하는 경우:

![](denied-access-to-iis-directories/_static/image1.jpg)

이 문제를 해결 하는 적절 한 디렉터리에서 보안 권한을 변경 해야 합니다.

특히 ASP.NET 필요 읽기, 실행 및 웹 사이트 루트에 대해 ASPNET 계정에 대 한 액세스 목록 (예: c:\inetpub\wwwroot 또는 대체 사이트 디렉터리의 IIS 구성 되었을 수도 있습니다), content 디렉터리와 응용 프로그램 루트 디렉터리 구성 파일 변경을 모니터링. 응용 프로그램 루트에 연결 된 IIS 관리 도구 (inetmgr)에서 응용 프로그램 가상 디렉터리 폴더 경로에 해당 합니다.

예를 들어, 다음 응용 프로그램 계층을 wwwroot 폴더 아래에 있는 것이 좋습니다.

`C:\inetpub\wwwroot\myapp\default.aspx`

예를 들어 ASPNET 계정은 myapp 및 wwwroot 디렉터리의 콘텐츠에 대 한 위에 정의 된 읽기 권한이 필요 합니다. 루트 폴더에 단일 상속 된 ACL은 사용할 수도 있습니다 필요에 따라 두 디렉터리에 대 한 중첩 하는 경우.

디렉터리에 권한을 추가 하려면 다음 단계를 수행 합니다.

- Windows 탐색기를 사용 하는 디렉터리로 이동
- 디렉터리 폴더를 마우스 오른쪽 단추로 클릭 하 고 "Properties"를 선택 합니다.
- 속성 대화 상자에서 "보안" 탭으로 이동
- "추가" 단추를 클릭 하 고 ASPNET 계정 이름 뒤에 컴퓨터 이름을 입력 합니다. 예를 들어, "웹 개발자" 라는 컴퓨터에서 webdev\ASPNET를 입력 하는 "확인"을 누릅니다.
- ASPNET 계정에 있는지 확인 합니다 "읽기 &amp; 실행", "폴더 내용" 및 "읽기" 확인란을 선택 합니다.
- 대화 상자를 닫고 변경 내용을 저장 하려면 확인을 누릅니다.

![](denied-access-to-iis-directories/_static/image2.jpg)

원하는 경우에 Windows를 사용 하 여 스크립트 또는 함께 제공 되는 "cacls.exe" 도구를 사용 하 여 이러한 변경 내용의 자동화할 수 있습니다. ASPNET 계정에 대 한 자세한 내용은 참조 하십시오 합니다 [FAQ 문서](https://go.microsoft.com/fwlink/?LinkId=5828)합니다.

지정 된 웹 응용 프로그램을 보유 쓰기 의존 하는 경우 또는 특정 폴더 또는 파일에 대 한 사용 권한을 수정 하는 경우이 동일한 절차를 수행 하 고 "쓰기" 및/또는 "수정" 확인란을 선택 하 여 부여할 수 있습니다.

모든 사용자 또는이 디렉터리 (즉, 기본 구성)에 사용자 그룹 읽기 액세스를 허용 하는 컴퓨터에서 문제가 발생할 수 하 고 위의 단계를 필요한 되지 않습니다.
