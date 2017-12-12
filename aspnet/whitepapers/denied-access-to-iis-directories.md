---
uid: whitepapers/denied-access-to-iis-directories
title: "ASP.NET IIS 디렉터리에 대 한 액세스가 거부 | Microsoft Docs"
author: rick-anderson
description: "이 백서에서는 ASP.NET 응용 프로그램에 요청 \"디렉터리 이름 디렉터리에 액세스 거부 오류를 반환 하는 경우 수행 해야 작업 설명 합니다. S를 못했습니다..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/10/2010
ms.topic: article
ms.assetid: 3cb27b8a-354f-4332-bfe0-232b13bbf8aa
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /whitepapers/denied-access-to-iis-directories
msc.type: content
ms.openlocfilehash: 64118ac7a5f280775106d2dc7636923b08f28d89
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="aspnet-denied-access-to-iis-directories"></a>ASP.NET은 IIS 디렉터리에 대 한 액세스가 거부
====================
> 이 백서 작업을 설명 하는 오류를 반환 하는 ASP.NET 응용 프로그램에 요청 하는 경우 "에 대 한 액세스를 거부 *디렉터리 이름* 디렉터리입니다. 디렉터리 chaanges 모니터링을 시작 하지 못했습니다. "
> 
> ASP.NET 1.0 및 1.1 ASP.NET에 적용 됩니다.


ASP.NET V1 RTM은 이제 실행 작음을 사용 하 여 권한 있는 windows 계정-로컬 컴퓨터에서 "ASPNET" 계정으로 등록 합니다.

일부 잠겨 있으며 시스템에서이 수 기본적이 지 읽기는 웹 사이트 콘텐츠 디렉터리, 응용 프로그램 루트 디렉터리 또는 웹 사이트 루트 디렉터리에 대 한 보안 액세스 합니다. 이 경우에 지정 된 웹 응용 프로그램에서 페이지를 요청할 때 다음 오류가 나타납니다.

![](denied-access-to-iis-directories/_static/image1.jpg)

이 문제를 해결 하려면 적절 한 디렉터리에 대 한 보안 권한을 변경 해야 합니다.

특히, ASP.NET 필요 읽기, 실행 및 웹 사이트 루트에 대 한 ASPNET 계정에 대 한 액세스 목록 (예: c:\inetpub\wwwroot 또는 IIS에서 구성할 수 있습니다 하 든 대체 사이트 디렉터리), 콘텐츠 디렉터리와 응용 프로그램 루트 디렉터리 구성 파일의 변경에 대 한 모니터링. 응용 프로그램 루트는 IIS 관리 도구 (inetmgr)에서 응용 프로그램 가상 디렉터리와 연결 된 폴더 경로에 해당 합니다.

예를 들어 wwwroot 폴더에서 다음 응용 프로그램 계층 구조를 것이 좋습니다.

`C:\inetpub\wwwroot\myapp\default.aspx`

이 예제에서는 ASPNET 계정을 myapp 파일과 있는 wwwroot 디렉터리의 콘텐츠에 대 한 위에 정의 된 읽기 권한이 있어야 합니다. 루트 폴더에는 단일 상속 된 ACL은 사용할 수도 있습니다 필요에 따라 두 디렉터리에 대 한 중첩 하는 경우.

디렉터리에 사용 권한을 추가 하려면 다음 단계를 수행 합니다.

- Windows 탐색기를 사용 하 여 디렉터리로 이동
- 디렉터리 폴더를 마우스 오른쪽 단추로 클릭 하 고 "속성" 선택
- 속성 대화 상자에서 "보안" 탭으로 이동
- "추가" 단추를 클릭 하 고 컴퓨터 이름 뒤에 ASPNET 계정 이름을 입력 합니다. 예를 들어 "웹 개발자" 라는 컴퓨터에서 webdev\ASPNET를 입력 하는 "확인"에 도달 합니다.
- ASPNET 계정에 있는지 확인 된 "읽기 &amp; Execute", "폴더 내용" 및 "읽기" 확인란을 선택 합니다.
- 대화 상자를 닫고 변경 내용을 저장 하려면 확인에 도달 했습니다.

![](denied-access-to-iis-directories/_static/image2.jpg)

원하는 경우 Windows와 함께 제공 되는 "cacls.exe" 도구 또는 스크립트를 사용 하 여 이러한 변경 내용을 자동화할 수 있습니다. ASPNET 계정에 대 한 자세한 내용은 참조 하십시오는 [FAQ 문서](https://go.microsoft.com/fwlink/?LinkId=5828)합니다.

지정 된 웹 응용 프로그램에서 쓰기 또는 특정 폴더 또는 파일에 대 한 수정 하는 경우이 동일한 절차를 수행 하 고 "수정" 또는 "쓰기" 확인란을 선택 하 여 부여할 수 있습니다.

모든 사용자 또는 사용자 그룹 읽기 액세스 (즉, 기본 구성)는 이러한 디렉터리를 허용 하는 컴퓨터에 없는 문제가 발생할 수 및가 위 단계를 입력할 필요가 없습니다.
