---
uid: whitepapers/ms03-32-issue
title: IE 용 보안 업데이트를 적용 한 후 '서버 응용 프로그램이 사용할 수 없음' 오류 수정 | Microsoft Docs
author: rick-anderson
description: 이 문서에서는 마법사를 실행 하는 ASP.NET 1.0 응용 프로그램에 영향을 주는 Internet Explorer에 대 한 m s 03-32 보안 업데이트를 사용 하 여 문제를 해결 하는 패치를 설명 하는 중...
ms.author: aspnetcontent
ms.date: 02/10/2010
ms.assetid: 1365eebb-bdf7-4a05-8d18-7f200531be55
msc.legacyurl: /whitepapers/ms03-32-issue
msc.type: content
ms.openlocfilehash: 1a289379229335a9841dec48e577c19173419891
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37836725"
---
<a name="fix-for-server-application-unavailable-error-after-applying-security-update-for-ie"></a>IE 용 보안 업데이트를 적용 한 후 '서버 응용 프로그램이 사용할 수 없음' 오류에 대 한 수정
====================
> 이 문서에서는 Windows XP Professional을 실행 하는 ASP.NET 1.0 응용 프로그램에 영향을 주는 Internet Explorer에 대 한 m s 03-32 보안 업데이트를 사용 하 여 문제를 해결 하는 패치를 설명 합니다.
> 
> Windows XP Professional ASP.NET 1.0에 적용 됩니다.


Microsoft은 Internet Explorer 보안 패치 m s 03-32 보안 업데이트 및 Windows XP에서 실행 중인 ASP.NET 1.0을 사용 하 여 문제를 식별 합니다. 수동으로 또는 Windows 업데이트 사이트에서 최신 중요 업데이트를 가져와서이 패치를 설치할 수 있습니다.

이 문제의 증상으로 패치를는 Windows XP 컴퓨터를 설치한 후 로컬 IIS 5.1 웹 서버에서 실행 중인 ASP.NET 응용 프로그램에 대 한 모든 요청 하면 "서버 응용 프로그램 사용할 수 없음" 라는 오류 메시지가 됩니다. 원격 웹 서버에 대 한 요청을 받지 않습니다.

이 문제는 Windows XP에서 ASP.NET 1.0을 실행 하는 설치에만 영향을 줍니다. Windows 2000 또는 Windows Server 2003을 실행 하는 컴퓨터는 영향을 주지 않습니다. 또한 영향을 주지 않습니다 ASP.NET 1.1이 설치를 사용 하 여 Windows XP를 실행 하는 컴퓨터입니다.

유의 사항:이 문제 **아닙니다** ASP.NET 사용 하 여 보안 버그입니다. 것 **하지 않습니다** 열거나 악의적인 공격이 ASP.NET 응용 프로그램 또는 서버에 허용 합니다. 대신 순수 함수형 버그로 인해 자체 패치 것입니다.

노력이 문제에 대 한 영구 솔루션에 있습니다. 그동안 문제에 대 한 대 안으로 다음 배치 파일을 실행할 수 있습니다. 배치 파일은 다음을 수행합니다.

1. IIS 및 ASP.NET 상태 서비스를 중지합니다.
2. 삭제 한 알려진 임시 암호로 ASPNET 계정을 다시 만듭니다.
3. Windows를 사용 하 여 `runas` ASPNET 사용자 프로필을 만드는 실행 파일을 시작 하는 명령
4. ASP.NET을 다시 등록 합니다. 이 만들고 계정의 새로운 임의의 암호를 적용 하는 것에 대 한 기본 ASP.NET 액세스 제어 설정
5. IIS 서비스를 다시 시작

하드 코드 된 임시 암호를 포함 하는 배치 파일 "<strong>1pass@word</strong>" runas 명령을 일괄 처리 파일을 실행 하는 경우에 입력 하 라는 메시지가 될 수 있습니다. 실행 명령이 완료 되 면 강력한 임의 값을 사용 하 여 ASPNET 계정 암호를 다시 생성 됩니다. 배치 파일을 하드 코드 된 암호를 사용자 환경에서 암호 복잡성 요구 사항에 맞지 않는 경우 실패할 수 있는 참고 합니다. 하는 경우에 사용자 환경에 적합 한 다른 값을 변경할 수 있습니다.

*> [!IMPORTANT]* 사용자 지정 액세스 제어 설정이 나 ASPNET 계정에 대 한 데이터베이스 계정 권한을 추가한 경우이 배치 파일에서 완료 된 후 다시 만들어야 할 수 있습니다. 즉, 계정을 다시 만들 때 새 보안 식별자 (SID)를 가져와야 합니다.

*> [!IMPORTANT]* 다음으로 사용자 지정 ASPNET 계정 이외의 계정을 사용 하 여 ASP.NET 작업자 프로세스를 실행 하는 경우이 일괄 처리 파일으로 실행 해야 합니다. 대신 대화형으로 로그인 하거나 해당 계정에 대 한 사용자 프로필을 만드는 해당 계정의 runas 명령을 사용 해야 합니다.

배치 파일은 자동 압축 풀기 보관 파일 아래에 포함 됩니다. 사용 합니다.

1. 관리자 권한이 있는 계정으로 실행 해야
2. [다운로드 하 고 자동 압축 풀기 실행 파일을 엽니다](ms03-32-issue/_static/fixup1.exe)
3. C:\에 압축을 풉니다
4. 시작 메뉴에서 실행... 선택 하 고 입력 `cmd.exe`
5. 열려 있는 명령 창에서 입력 `c:\fixup.cmd`합니다.
6. 메시지가 표시 되 면 입력 <strong>1pass@word</strong> 암호로 합니다.
7. 이전에 사용자 지정 액세스 제어 설정 또는 ASPNET 계정에 대 한 계정 권한이 데이터베이스에 있는 경우 이제 이러한 설정을 다시 적용 해야 합니다.

이 인해 불편을 드려 많은 정말 죄송 합니다. 추가 정보를 사용할 수 있는 게시 됩니다.

아래 행렬에는 플랫폼 및 버전이이 문제의 영향을 자세히 설명 합니다.

| .NET Framework | 플랫폼 | 영향을 받는 |
| --- | --- | --- |
| 버전 1.0 | Windows 2000 Professional | 아니요 |
| 버전 1.0 | Windows 2000 Server | 아니요 |
| 버전 1.0 | Windows XP Professional | 예 |
| 버전 1.0 | Windows Server 2003 | 아니요 |
| 버전 1.0 | Cassini 사용 하 여 Windows XP 홈 | 아니요 |
| 버전 1.1 | Windows 2000 Professional | 아니요 |
| 버전 1.1 | Windows 2000 Server | 아니요 |
| 버전 1.1 | Windows XP Professional | 아니요 |
| 버전 1.1 | Windows Server 2003 | 아니요 |
| 버전 1.1 | Cassini 사용 하 여 Windows XP 홈 | 아니요 |

감사 합니다.   
 ASP.NET 팀
