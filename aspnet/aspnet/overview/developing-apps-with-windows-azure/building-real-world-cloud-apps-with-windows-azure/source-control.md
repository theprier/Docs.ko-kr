---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control
title: 소스 제어 (실제 클라우드 앱 빌드 azure) | Microsoft Docs
author: MikeWasson
description: 실제 세계 클라우드 앱 빌드 Azure 전자책을 사용 하 여 Scott Guthrie를 개발한 프레젠테이션을 기반으로 합니다. 13 패턴과 그을 수 있는 방법을 설명 하는 중...
ms.author: aspnetcontent
ms.date: 06/23/2015
ms.assetid: 2a0370d3-c2fb-4bf3-88b8-aad5a736c793
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control
msc.type: authoredcontent
ms.openlocfilehash: 045dc654057802be4ad96f5ecc3ed6c3d7a1ccb1
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37823315"
---
<a name="source-control-building-real-world-cloud-apps-with-azure"></a>소스 제어 (실제 클라우드 앱 빌드 Azure 사용 하 여)
====================
하 여 [Mike Wasson](https://github.com/MikeWasson)하십시오 [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)

[다운로드 해결 프로젝트](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자책 다운로드](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> 합니다 **실제 세계 클라우드 앱 빌드 Azure** 전자책 Scott Guthrie를 개발한 프레젠테이션을 기반으로 합니다. 13 패턴 설명 하 고 도움이 될 수 있는 사례 성공적인 클라우드를 위한 웹 앱을 개발할 수 있습니다. 전자책에 대 한 정보를 참조 하세요 [첫 번째 장에서](introduction.md)합니다.


소스 제어에 대 한 모든 클라우드 개발 프로젝트, 팀 환경 뿐 아니라 반드시 필요 합니다. 생각 하지 않습니다. 소스 코드를 편집 하거나 실행 취소 기능과 및 자동 백업, 소스 제어 하지 않고 Word 문서도 오류가 발생 하면 더 많은 시간을 절약할 수 있는 프로젝트 수준에서 이러한 함수를 제공 합니다. 클라우드 소스 제어 서비스를 사용 하 여 복잡 한 설정에 걱정할 필요가 없습니다 및 Visual Studio Online 소스 제어 사용자 5 명까지 무료로 사용할 수 없습니다.

이 장의 첫 번째 부분에서는 염두에 세 가지 주요 모범 사례를 설명 합니다.

- [자동화 스크립트를 소스 코드로 처리](#scripts) 버전과 응용 프로그램 코드와 함께 합니다.
- [비밀 정보에서 확인 하지 않음](#secrets) (자격 증명과 같은 중요 한 데이터) 소스 코드 리포지토리를 합니다.
- [소스 분기 설정](#devops) DevOps 워크플로 사용 하도록 합니다.

이 장의 나머지 Visual Studio, Azure 및 Visual Studio Online에서 이러한 패턴의 몇 가지 샘플 구현을 제공합니다.

- [Visual Studio에서 소스 제어에 스크립트 추가](#vsscripts)
- [Azure에서 중요 한 데이터를 저장 합니다.](#appsettings)
- [Visual Studio 및 Visual Studio Online에서 Git 사용](#gittfs)

<a id="scripts"></a>
## <a name="treat-automation-scripts-as-source-code"></a>자동화 스크립트를 소스 코드로 처리

클라우드 프로젝트에서 작업할 때 작업을 자주 변경 하는 하 고 고객이 보고 한 문제에 빠르게 대응할 수 있게 되기를 원하는 합니다. 에 설명 된 대로도 포함 자동화 스크립트를 사용 하 여 신속 하 게 응답 합니다 [모든 자동화](automate-everything.md) 장입니다. 모든 환경의 만드는 데 사용할 수 있는 스크립트를 크기 조정 응용 프로그램 소스 코드와 동기화 되도록 해야 하는 것 등을 배포 합니다.

스크립트 코드를 사용 하 여 동기화를 유지 하려면 소스 제어 시스템에 저장 합니다. 그런 다음 이전 변경 내용을 롤백하거나 개발 코드에서 다른 프로덕션 코드를 빠른 픽스를 확인 해야 하는 경우 설정을 변경 되었거나 필요한 버전을 복사본이 팀 멤버를 추적 하려고 하는 시간을 낭비 필요가 없습니다. 필요한 스크립트, 필요한 및 모든 팀 멤버는 동일한 스크립트를 사용 하 여 작동 하는지 확인 하는 코드 베이스를 사용 하 여 동기화 된 확신할 수는 있습니다. 그런 다음 테스트 및 프로덕션 또는 새로운 기능을 개발 하는 핫픽스가 배포를 자동화 해야 하는지 여부를 업데이트 해야 하는 코드에 대 한 올바른 스크립트를 해야 합니다.

<a id="secrets"></a>
## <a name="dont-check-in-secrets"></a>비밀 정보에서 확인 하지 않음

소스 코드 리포지토리는 암호와 같은 중요 한 데이터를 적절 하 게 보안 위치가 너무 많은 사람들에 대 한 일반적으로 액세스할 수 있습니다. 스크립트 예: 암호는 암호를 사용 하는 경우에 소스 코드를 저장 하지 않으며 다른 곳에서 비밀을 저장할 수 있도록 이러한 설정의 매개 변수화 합니다.

예를 들어 포함 된 파일을 다운로드 하는 Azure 있습니다 게시 게시 프로필의 생성을 자동화 하기 위해 설정 합니다. 이러한 파일에는 사용자 이름 및 암호를 통해 Azure 서비스 관리 권한이 있는 포함 됩니다. 이 사용 하는 경우 게시 프로필을 만드는 방법 및 소스 제어에 이러한 파일을 선택 하면 모든 리포지토리에 대 한 액세스를 사용 하 여 볼 수 있습니다 이러한 사용자 이름 및 암호입니다. 안전 하 게에 저장할 수 있습니다 암호 게시 프로필 자체 암호화 되어 있기 때문는 *. pubxml.user* 기본적으로 소스 제어에 포함 되지 않은 파일입니다.

<a id="devops"></a>
## <a name="structure-source-branches-to-facilitate-devops-workflow"></a>DevOps 워크플로 용이 하 게 소스 분기 구조

리포지토리에 분기를 구현 하는 방법을 새 기능을 개발 및 프로덕션 환경에서 문제를 해결 하는 능력을 영향을 줍니다. 패턴 중간 많은 팀 사용 크기는 다음과 같습니다.

![소스 분기 구조](source-control/_static/image1.png)

마스터 분기에는 항상 프로덕션에 있는 코드와 일치 합니다. 아래에 있는 master 분기 개발 수명 주기의 여러 단계에 해당합니다. Development 분기는 새로운 기능을 구현 하는 위치입니다. 소규모 팀에 대 한만 있을 수 마스터와 개발, 있지만 종종 사용자는 좋습니다 개발 사이의 마스터 분기를 준비 합니다. 업데이트를 프로덕션으로 이동 하기 전에 최종 통합 테스트에 대 한 준비를 사용할 수 있습니다.

큰 팀을 위한 있을 수 있습니다 각 새 기능에 대 한 별도 분기 작은 팀 development 분기로 체크 인 모든 사용자가 해야 할 수 있습니다.

기능은 준비 하면 병합 하는 경우 각 기능에 대 한 분기가 있는 경우 해당 소스 코드를 개발에 구성 변경 분기 및 기타 기능 분기를 다운 합니다. 이 소스 코드 병합 프로세스는 시간이 오래 걸릴 수 있습니다 하 고 별도 기능을 계속 유지 하면서 해당 작업을 방지 하려면 일부 팀은 구현 호출 대안 *[기능 토글](http://en.wikipedia.org/wiki/Feature_toggle)* (라고도 *기능 플래그*). 즉, 같은 분기에서의 모든 기능에 대 한 코드는 있지만 사용 하도록 설정 하거나 코드에서 스위치를 사용 하 여 각 기능을 사용 하지 않도록 설정 합니다. 예를 들어 기능 A는 Fix It 응용 프로그램 작업에 대 한 새 필드 및 캐싱 기능을 추가 하는 기능 B를 가정 합니다. 두 기능에 대 한 코드 개발 분기에 있을 수 있지만 앱은 유일한 표시 변수를 true로 설정 된 경우 새 필드를 다른 변수에 설정 된 경우 캐싱을 사용만 true로 합니다. 기능 수준을 올릴 수 없지만 기능 B는 준비를 하는 경우에 모든 해제는 기능 스위치를 사용 하 여 프로덕션 환경에 코드를 승격할 수 있습니다 하 고 기능 B 전환 합니다. 그런 다음 기능 A를 완료 하 고 승격 나중에 모든 소스 코드 병합 되지 않을 수 있습니다.

분기 또는 설정/해제를 사용 하 여 기능에 대 한 여부 이와 같은 분기 구조를 사용 하면 민첩 하 고 반복 가능한 방식으로 프로덕션 환경에 개발에서 코드를 이동할 수 있습니다.

이 구조를 사용 하면 고객의 의견에 빠르게 대응할 수 있습니다. 프로덕션으로 빠른 수정 해야 할 경우 있습니다 에서도 수행할 수는 효율적으로 민첩 하 게 합니다. 마스터 또는 스테이징 분기를 만들 수 있습니다 및 마스터에 병합 하 고 아래쪽 준비 되었을 때 개발 및 기능 분기에 있습니다.

![핫픽스 분기](source-control/_static/image2.png)

프로덕션 및 개발 분기의 해당 분리를 사용 하 여 이와 같은 분기 구조를 하지 않고 프로덕션 문제에에서 배치할 수 있습니다 프로덕션 수정 사항을 함께 새 기능 코드를 승격할 필요가 위치. 새 기능 코드를 완벽 하 게 테스트 및 준비에 대 한 프로덕션 되지 않을 수 있습니다 하 고 많은 준비 되지 않은 변경 내용을 백업 작업을 수행 해야 합니다. 또는 지연 변경 내용을 테스트 하 고 배포를 준비 하기 위해 수정 해야 할 수 있습니다.

그런 다음 Visual Studio, Azure 및 Visual Studio Online에서 이러한 세 가지 패턴을 구현 하는 방법의 예제를 볼 수 있습니다. 자세한 단계별 방법-을 수행-it 지침은; 보다는 예제는 모든 필요한 컨텍스트를 제공 하는 자세한 지침을 참조 합니다 [리소스](#resources) 장의 끝에 있는 섹션입니다.

<a id="vsscripts"></a>
## <a name="add-scripts-to-source-control-in-visual-studio"></a>Visual Studio에서 소스 제어에 스크립트 추가

(소스 제어에 프로젝트 것으로 간주) Visual Studio 솔루션 폴더에 포함 하 여 Visual Studio에서 소스 제어에 스크립트를 추가할 수 있습니다. 작업을 수행 하는 한 가지 방법은 다음과 같습니다.

솔루션 폴더에 스크립트에 대 한 폴더를 만듭니다 (되 고 동일한 폴더에 *.sln* 파일).

![Automation 폴더](source-control/_static/image3.png)

스크립트 파일을 폴더로 복사 합니다.

![Automation 폴더 내용](source-control/_static/image4.png)

Visual Studio에서 솔루션 폴더를 프로젝트에 추가 합니다.

![새 솔루션 폴더 메뉴 선택](source-control/_static/image5.png)

고 솔루션 폴더에 스크립트 파일을 추가 합니다.

![기존 항목 메뉴 선택 항목 추가](source-control/_static/image6.png)

![기존 항목 추가 대화 상자](source-control/_static/image7.png)

스크립트 파일은 이제 프로젝트에 포함 하 고 소스 컨트롤에서 해당 소스 코드 변경에 따라 버전 변경 사항을 추적 합니다.

<a id="appsettings"></a>
## <a name="store-sensitive-data-in-azure"></a>Azure에서 중요 한 데이터를 저장 합니다.

응용 프로그램을 Azure 웹 사이트에서를 실행 하면 소스 제어에서 자격 증명을 저장 하지 않도록 하는 한 가지 방법은 경우 대신 Azure에 저장 합니다.

예를 들어 Fix It 응용 프로그램의 Web.config 파일 두 연결 문자열의 프로덕션 및 Azure storage 계정에 대 한 액세스를 제공 하는 키의 암호를 갖게 되는 저장 합니다.

[!code-xml[Main](source-control/samples/sample1.xml?highlight=2-3,11)]

이러한 설정에 대 한 실제 값을 입력 하는 경우에 *Web.config* 파일 배치 하는 경우 또는 합니다 *Web.Release.config* 파일 배포 중에 삽입 하도록 Web.config 변환을 구성 하려면 이러한 소스 리포지토리에 저장 됩니다. 게시 프로필을 프로덕션 환경에 데이터베이스 연결 문자열을 입력 하는 경우, 암호 됩니다 하 *.pubxml* 파일입니다. (제외할 수 있습니다 합니다 *.pubxml* 소스 제어에서 파일 하지만 다른 모든 배포 설정은 공유의 이점을 손실 합니다.)

Azure 제공에 대 한 대안을 **appSettings** 부분 문자열을 연결 합니다 *Web.config* 파일. 여기의 관련 부분은 합니다 **구성** Azure 관리 포털에서 웹 사이트에 대 한 탭:

![포털의 connectionStrings 및 appSettings](source-control/_static/image8.png)

이 웹 사이트 및 응용 프로그램을 실행 하는 프로젝트를 배포할 때 Azure에 저장 된 값의 Web.config 파일에서 모든 값은 재정의 합니다.

관리 포털 또는 스크립트를 사용 하 여 Azure에서 이러한 값을 설정할 수 있습니다. 살펴본 환경 생성 automation 스크립트는 [모든 자동화](automate-everything.md) 장 Azure SQL Database를 만들고, storage 및 SQL Database 연결 문자열을 가져옵니다 및 웹 사이트에 대 한 설정에서 이러한 암호를 저장 합니다.

[!code-powershell[Main](source-control/samples/sample2.ps1)]

[!code-powershell[Main](source-control/samples/sample3.ps1)]

실제 값 소스 리포지토리로 유지 하지 않도록 스크립트를 매개 변수화는 알 수 있습니다.

를 실행 하면 로컬 개발 환경에서 앱을 읽고 로컬 Web.config 파일에 연결 문자열 지점에 SQL Server LocalDB 데이터베이스에는 *앱\_데이터* 웹 프로젝트의 폴더입니다. Azure에서 앱을 실행 하 고 앱의 Web.config 파일에서 이러한 값을 읽을 하려고 하는 경우 어떤 다시 가져옵니다 하 고 사용 하 여는 것이 아니라 실제로 Web.config 파일에서 웹 사이트에 대해 저장 값이 됩니다.

<a id="gittfs"></a>
## <a name="use-git-in-visual-studio-and-visual-studio-online"></a>Visual Studio 및 Visual Studio Online에서 Git 사용

이전에 제공 되는 DevOps 분기 구조를 구현 하려면 모든 원본 제어 환경을 사용할 수 있습니다. 분산 된 팀에는 [분산 버전 제어 시스템](http://en.wikipedia.org/wiki/Distributed_revision_control) (DVCS) 가장 잘 작동 될 수 있습니다 다른 팀에 대 한를 [시스템을 중앙 집중식](http://en.wikipedia.org/wiki/Revision_control) 더 적합할 수입니다.

[Git](http://git-scm.com/) 는 DVCS 매우 인기가 됩니다. 소스 제어에 Git를 사용 하는 경우 로컬 컴퓨터에 모든 기록과 사용 하 여 저장소의 전체 복사본이 있는 합니다. 많은 사람들이 더 쉽기 때문에 계속 해 서 작업을 계속 수행할 수 있습니다-네트워크에 연결 되지 않은 커밋 만들고 롤백, 및 분기를 전환 등을 선호 합니다. 네트워크에 연결 하는 경우에 쉽고 빠르게 분기를 만들고 로컬 상태인 경우 분기를 전환 됩니다. 또한 다른 개발자에 게 영향을 하지 않고도 로컬 커밋 및 롤백을 수행할 수 있습니다. 및 커밋을 서버에 보내기 전에 일괄 처리할 수 있습니다.

[Microsoft Visual Studio Online](https://www.visualstudio.com/)VSO (), Team Foundation Service 라고 두 Git를 제공 하는 이전 하 고 [Team Foundation 버전 제어](https://msdn.microsoft.com/library/ms181237(v=vs.120).aspx) (TFVC; 중앙 집중식 소스 제어). 여기 Microsoft Azure 그룹의 일부 팀은 사용 하 여 중앙 집중식된 소스 제어, 배포 하는 몇 가지 사용 및 몇 가지를 조합 (일부 프로젝트에 대 한 중앙 집중식 및 다른 프로젝트에 대 한 분산)를 사용 합니다. VSO 서비스를 최대 5 명의 사용자 무료. 무료 플랜에 등록할 수 있습니다 [여기](https://go.microsoft.com/fwlink/?LinkId=307137)합니다.

기본 제공 첫 번째 클래스를 포함 하는 visual Studio 2013 [Git 지원](https://msdn.microsoft.com/library/hh850437.aspx); 같습니다. 빠른 동작 원리를 데모 합니다.

Visual Studio 2013에서 열려 있는 프로젝트에서 솔루션을 마우스 오른쪽 단추로 클릭 **솔루션 탐색기**, 선택한 **원본 제어에 솔루션 추가**합니다.

![소스 제어에 솔루션 추가](source-control/_static/image9.png)

Visual Studio (중앙 집중식된 버전 제어) TFVC 또는 Git를 사용 하려는 경우 요청 합니다.

![소스 제어 선택](source-control/_static/image10.png)

Git를 선택 하 고 클릭 **확인**, Visual Studio 솔루션 폴더에 새 로컬 Git 리포지토리를 만듭니다. 새 저장소에 파일이 없으면 아직; Git 커밋을 수행 하 여 저장소에 추가 해야 합니다. 솔루션을 마우스 오른쪽 단추로 클릭 **솔루션 탐색기**를 클릭 하 고 **커밋**합니다.

![커밋](source-control/_static/image11.png)

Visual Studio에서 자동으로 모든 커밋에 대 한 프로젝트 파일을 준비 하 고에 나열 **팀 탐색기** 에 **포함 된 변경 내용** 창입니다. (경우 커밋에 포함 하지 않으려는 일부를 선택할 수 있습니다 마우스 오른쪽 단추를 클릭 **제외**.)

![팀 탐색기](source-control/_static/image12.png)

커밋 설명을 입력 하 고 클릭 **커밋**, Visual Studio 커밋을 실행 및 커밋 ID를 표시 하 고

![팀 탐색기 변경 내용](source-control/_static/image13.png)

이제 저장소에는 무엇이 다른 되도록 일부 코드를 변경한 경우에 쉽게 차이점을 볼 수 있습니다. 선택, 변경한 하는 파일을 마우스 오른쪽 단추로 클릭 **Unmodified 비교할**, 커밋되지 않은 변경 내용을 보여 주는 비교 표시를 표시 하 고 있습니다.

![수정 되지 않은 항목과 비교](source-control/_static/image14.png)

![차이 표시 변경](source-control/_static/image15.png)

쉽게 수행 하 고 체크 인해야 내용을 볼 수 있습니다.

분기를 확인 해야 할 수 있는 하는 Visual Studio에서 너무 – 가정 합니다. **팀 탐색기**, 클릭 **새 분기**합니다.

![팀 탐색기에 대 한 새 분기](source-control/_static/image16.png)

분기 이름을 입력, 클릭 **분기 만들기**를 선택한 경우 **분기 체크 아웃**, Visual Studio에서 새 분기 자동으로 확인 합니다.

![팀 탐색기에 대 한 새 분기](source-control/_static/image17.png)

이제 파일을 변경 해야 하 고이 분기를 체크 인할 수 있습니다. 및 쉽게 전환할 수 있습니다 분기와 Visual Studio 간에 자동으로 동기화 파일을 분기 체크 아웃 합니다. 이 예제에서 웹 페이지에서 제목을  *\_Layout.cshtml* "핫 1"의 수정 HotFix1 분기로 변경 되었습니다.

![Hotfix1 분기](source-control/_static/image18.png)

마스터에 다시 전환 하면 분기의 콘텐츠를  *\_Layout.cshtml* 파일 마스터 분기에 있기를 자동으로 되돌리려면 합니다.

![마스터 분기](source-control/_static/image19.png)

이 간단한 예제를 하는 방법을 신속 하 게 분기를 만들 분기 간에 앞뒤로 이동 합니다. 이 기능을 사용 하면 분기 구조를 사용 하 여 항상 agile 워크플로 및 자동화 스크립트에 표시 되는 [모든 자동화](automate-everything.md) 장입니다. 예를 들어 수 Development 분기에서 작업 마스터에서 핫픽스 분기 만들기, 새 분기로 전환, 변경 내용을 확인 하면 및 Development 분기로 다시 전환 합니다 커밋한 하 던 작업을 계속 합니다.

여기서 살펴본 것은 Visual Studio에서 로컬 Git 리포지토리를 사용 하는 방법입니다. 팀 환경에서 일반적으로 변경 내용을 푸시할 공용 리포지토리에 있습니다. Visual Studio 도구에서는 원격 Git 리포지토리를 가리키도록 수도 수 있습니다. GitHub.com를 사용 하 여이 위해 또는 사용할 수 있습니다 [Visual Studio Online에서 Git](https://msdn.microsoft.com/library/hh850437.aspx) 작업 항목 및 버그 추적 같은 다른 모든 Visual Studio Online 기능과 통합 합니다.

물론 agile 분기 전략을 구현할 수 있습니다 하는 유일한 방법은 아닙니다. 중앙 집중식된 소스 제어 리포지토리를 사용 하 여 동일한 agile 워크플로 사용할 수 있습니다.

## <a name="summary"></a>요약

변경 안전 하 고 예측 가능한 방식으로 라이브 되도록 하는 속도에 따라 소스 제어 시스템의 성공 여부를 측정 합니다. 직접 변경 하는 하루나 이틀에 수동 테스트를 수행 해야 하므로 장단점이 찾은 경우 일까요 않거나 process-wise test-wise 최악의 시간 보다 더 이상이 든 몇 분 안에 변경을 수행할 수 있도록 해야 합니다. 이렇게 하는 한 가지 전략을 연속 통합 및 지속적인 업데이트에서 다루게 될를 구현 하는 것은 [다음 장에서](continuous-integration-and-continuous-delivery.md)합니다.

<a id="resources"></a>
## <a name="resources"></a>자료

합니다 [Visual Studio Online](https://www.visualstudio.com/) 포털 설명서 및 지원 서비스를 제공 하 고 계정에 등록할 수 있습니다. Visual Studio 2012 하 고 Git를 사용 하려는 경우 [Visual Studio Tools for Git](https://visualstudiogallery.msdn.microsoft.com/abafc7d6-dcaa-40f4-8a5e-d6724bdb980c)합니다.

(중앙 집중식된 버전 제어) TFVC와 Git (분산된 버전 제어)에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [버전 제어 시스템을 사용 해야 합니다: TFVC 또는 Git?](https://msdn.microsoft.com/library/vstudio/ms181368.aspx#tfvc_or_git_summary) MSDN 설명서 TFVC와 Git 간의 차이점을 요약 하는 표를 포함 합니다.
- [물론 필자는 Team Foundation Server 및 필자는 Git 이지만 더 나은?](https://blogs.msdn.com/b/visualstudiouk/archive/2013/08/05/well-i-like-team-foundation-server-and-i-like-git-but-which-is-better.aspx) Git 및 TFVC 비교 합니다.

분기 전략에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [Team Foundation Server 2012 사용 하 여 릴리스 파이프라인 빌드](https://msdn.microsoft.com/library/dn449957.aspx)합니다. Microsoft Patterns and Practices 설명서입니다. 에 대 한 분기 전략 설명은 6 장을 참조 하십시오. 옹호자 기능에는 기능에 대 한 분기를 사용 하는 경우 대표 유지 단기 (시간 또는 일에서 최대) 및 기능 분기를 통해 설정/해제 합니다.
- [버전 제어 가이드](https://aka.ms/vsarsolutions)합니다. ALM Rangers에서 분기 전략을 안내 합니다. 다운로드 탭에서 Strategies.pdf 분기를 참조 하세요.
- [기능 토글 사용 하 여 소프트웨어 개발](https://msdn.microsoft.com/magazine/dn683796.aspx)합니다. MSDN Magazine 기사입니다.
- [설정/해제 기능](http://martinfowler.com/bliki/FeatureToggle.html)합니다. 설정/해제 하는 기능 소개/Martin Fowler의 블로그에서 기능 플래그입니다.
- [기능 설정/해제 vs 기능 분기](http://geekswithblogs.net/Optikal/archive/2013/02/10/152069.aspx)합니다. Dylan Smith가 기능 설정/해제 하는 방법에 대 한 다른 블로그 게시물입니다.

소스 제어 저장소에 보관 해야 하는 중요 한 정보를 처리 하는 방법에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET 및 Azure App Service에 암호 및 기타 중요 한 데이터 배포에 대 한 유용한](../../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)합니다.
- [Azure 웹 사이트: 어떻게 응용 프로그램 문자열 및 연결 문자열의 작동](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)합니다. 재정의 하는 Azure 기능에 설명 `appSettings` 하 고 `connectionStrings` 에서 데이터를 *Web.config* 파일입니다.
- [사용자 지정 구성 및 응용 프로그램 설정에서 Azure 웹 사이트-Stefan Schackow](https://azure.microsoft.com/documentation/videos/configuration-and-app-settings-of-azure-web-sites/)합니다.

소스 제어에서 중요 한 정보를 유지 하기 위한 다른 방법에 대 한 정보를 참조 하세요 [ASP.NET MVC: 소스 제어의 개인 설정의 유지](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx)합니다.

> [!div class="step-by-step"]
> [이전](automate-everything.md)
> [다음](continuous-integration-and-continuous-delivery.md)
