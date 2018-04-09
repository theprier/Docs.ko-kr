---
uid: whitepapers/ms03-32-issue
title: IE에 대 한 보안 업데이트를 적용 한 후 '서버 응용 프로그램 사용할 수 없는 오류에 대 한 수정 | Microsoft Docs
author: rick-anderson
description: 이 문서에서는 m s 03 32 보안 업데이트 Wi에서 실행 되는 ASP.NET 1.0 응용 프로그램에 영향을 주는 Internet Explorer에 대 한 문제를 해결 하는 패치 설명...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/10/2010
ms.topic: article
ms.assetid: 1365eebb-bdf7-4a05-8d18-7f200531be55
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /whitepapers/ms03-32-issue
msc.type: content
ms.openlocfilehash: dd1a564cd347364abc3ca5ac0a9ffda448bcede8
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="fix-for-server-application-unavailable-error-after-applying-security-update-for-ie"></a>IE에 대 한 보안 업데이트를 적용 한 후 '서버 응용 프로그램 사용할 수 없는 오류에 대 한 수정
====================
> 이 문서에서는 m s 03 32 보안 업데이트와 함께 Windows XP Professional에서 실행 중인 ASP.NET 1.0 응용 프로그램에 영향을 주는 Internet Explorer에 대 한 문제를 해결 하는 패치를 설명 합니다.
> 
> ASP.NET 1.0 및 Windows XP Professional에 적용 됩니다.


Microsoft은 Internet Explorer 보안 패치 m s 03 32 보안 업데이트 및 Windows XP에서 실행 되는 ASP.NET 1.0 사용 하 여 문제를 확인 합니다. 수동으로 또는 Windows 업데이트 사이트에서 최신 중요 업데이트를 가져와서이 패치를 설치할 수 있습니다.

이 문제의 증상은는 Windows XP 컴퓨터에서 패치를 설치한 후 로컬 IIS 5.1 웹 서버에서 실행 중인 ASP.NET 응용 프로그램에 대 한 모든 요청 "서버 응용 프로그램이 사용할 수 없음" 라는 오류 메시지가. 요청을 원격 웹 서버에 영향을 받지 않습니다.

이 문제는 Windows XP에서 ASP.NET 1.0을 실행 하는 설치에만 영향을 줍니다. Windows 2000 또는 Windows Server 2003을 실행 하는 컴퓨터 영향을 주지 않습니다. ASP.NET 1.1이 설치 된 Windows XP를 실행 하는 컴퓨터 영향 하지 않습니다.

유의 사항:이 문제 **않습니다** asp.net 보안 버그입니다. 그 **없는** 개방 또는 ASP.NET 응용 프로그램 또는 서버에 대 한 모든 악의적인 공격을 허용 합니다. 만으로도 자체 패치로 인 한 기능 버그 순수 하 게 합니다.

최선을 다하고이 문제에 대 한 영구적인 솔루션에 있습니다. 그 동안에 문제에 대 한 문제를 해결 하려면 다음 배치 파일을 실행할 수 있습니다. 배치 파일은 다음을 수행합니다.

1. IIS 및 ASP.NET 상태 서비스를 중지합니다.
2. 삭제 하 고 알려진 임시 암호로 ASPNET 계정을 다시 만듭니다.
3. Windows를 사용 하 여 `runas` ASPNET 사용자 프로필을 만드는 실행 파일 시작 명령을
4. ASP.NET을 다시 등록합니다. 이 계정에 대 한 새로운 임의의 암호를 만들고 기본 ASP.NET 액세스 제어에 대 한 설정에 적용
5. IIS 서비스를 다시 시작

배치 파일의 하드 코드 된 임시 암호를 포함 합니다. "<strong>1pass@word</strong>" 배치 파일을 실행할 때의 실행 명령에 대해를 입력 하 라는 메시지가 수 있습니다. Runas 명령을 완료 되 면 ASPNET 계정 암호가 강력한 임의 값으로 다시 만들어집니다. 배치 파일은 하드 코드 된 암호 사용자 환경에서 암호 복잡성 요구 사항에 맞지 않는 경우 오류가 발생할 수 있는 참고 합니다. 해당 되는 경우, 사용자 환경에 적합 한 다른 값으로 변경할 수 있습니다.

*> [!IMPORTANT]* 사용자 지정 액세스 제어 설정 또는 ASPNET 계정에 대 한 데이터베이스 계정 사용 권한을 추가한 경우이 배치 파일에서 완료 된 후 다시 만들어야 할 수 있습니다. 즉, 계정을 다시 만들 때 새 보안 식별자 (SID)를 가져와야 합니다.

*> [!IMPORTANT]* 다음으로 사용자 지정 ASPNET 계정 이외의 계정을 사용 하 여 ASP.NET 작업자 프로세스를 실행 하는 경우이 배치 파일으로 실행 해야 합니다. 대신, 대화형으로 로그인 하거나 해당 계정에 대 한 사용자 프로필을 만드는 해당 계정에서 runas 명령을 사용 해야 합니다.

배치 파일은 아래 자동 압축 풀기 보관 파일에 포함 됩니다. 사용:

1. 관리자 권한이 있는 계정으로 실행 해야
2. [다운로드 하 여 자동 압축 풀기 실행 파일을 열고](ms03-32-issue/_static/fixup1.exe)
3. C:\에 콘텐츠를 추출
4. 시작 메뉴에서 실행... 선택 하 고 입력 `cmd.exe`
5. 열기 명령 창이 입력 `c:\fixup.cmd`합니다.
6. 메시지가 표시 되 면 입력 <strong>1pass@word</strong> 암호로 합니다.
7. 를 이전에 사용자 지정 액세스 제어 설정 또는 ASPNET 계정에 대 한 데이터베이스 계정 사용 권한 있는 지금 이러한 설정을 다시 적용 해야 합니다.

이 인해 불편을 드려 많은 드리지 합니다. 추가 정보를 사용할 수 있도록 게시 합니다.

아래 표는 플랫폼 및 버전이이 문제의 영향을 자세히 설명 합니다.

| .NET Framework | 플랫폼 | 영향을 |
| --- | --- | --- |
| 버전 1.0 | Windows 2000 Professional | 아니요 |
| 버전 1.0 | Windows 2000 Server | 아니요 |
| 버전 1.0 | Windows XP Professional | 예 |
| 버전 1.0 | Windows Server 2003 | 아니요 |
| 버전 1.0 | Windows XP Home Cassini와 | 아니요 |
| 버전 1.1 | Windows 2000 Professional | 아니요 |
| 버전 1.1 | Windows 2000 Server | 아니요 |
| 버전 1.1 | Windows XP Professional | 아니요 |
| 버전 1.1 | Windows Server 2003 | 아니요 |
| 버전 1.1 | Windows XP Home Cassini와 | 아니요 |

감사,   
 ASP.NET 팀
