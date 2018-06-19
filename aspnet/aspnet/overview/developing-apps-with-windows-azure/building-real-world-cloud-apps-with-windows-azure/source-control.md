---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control
title: 소스 제어 (Azure로 응용 프로그램 빌딩 실제 클라우드) | Microsoft Docs
author: MikeWasson
description: 실제 세계 클라우드로 응용 프로그램 빌딩 Azure 전자책 Scott Guthrie에서 개발 된 프레젠테이션을 기반으로 합니다. 13 패턴 및 그을 수 있는 방법에 설명...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/23/2015
ms.topic: article
ms.assetid: 2a0370d3-c2fb-4bf3-88b8-aad5a736c793
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control
msc.type: authoredcontent
ms.openlocfilehash: 0022458fa89a3be7ee8303750ad0e072df3b1bab
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30875697"
---
<a name="source-control-building-real-world-cloud-apps-with-azure"></a>소스 제어 (Azure로 응용 프로그램 빌딩 실제 클라우드)
====================
여 [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)

[다운로드 해결 프로젝트](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자책 다운로드](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **실제 세계 클라우드로 응용 프로그램 빌딩 Azure** 전자책 Scott Guthrie에서 개발 된 프레젠테이션을 기반으로 합니다. 13 패턴에 설명 하 고 사례 수 있는 클라우드에 대 한 웹 앱을 개발 성공적으로 수행 되어야 합니다. 전자책에 대 한 정보를 참조 하십시오. [첫 번째 장](introduction.md)합니다.


소스 제어에 대 한 모든 클라우드 개발 프로젝트 팀 환경 뿐 아니라 반드시 필요 합니다. 소스 코드 편집으로 인해 생각 하는지 또는 실행 취소 함수 및 자동 백업 및 소스 제어 없이 Word 문서 문제가 발생 하면 더 많은 시간을 저장할 수 있도록 프로젝트 수준에서 이러한 기능을 제공 합니다. 클라우드 소스 제어 서비스를 통해 복잡 한 설치에 걱정할 필요가 없습니다 및 사용자 5 명까지에 대 한 무료 Visual Studio Online 소스 제어를 사용할 수 없습니다.

이 장의 첫 번째 부분에서는 염두에 세 가지 주요 모범 사례를 설명 합니다.

- [자동화 스크립트 소스 코드로 처리할](#scripts) 버전과 응용 프로그램 코드와 함께 합니다.
- [비밀 정보에서 확인 안 함](#secrets) (자격 증명과 같은 중요 한 데이터)로 소스 코드 리포지토리 합니다.
- [소스 분기를 설정](#devops) DevOps 워크플로에 사용할 수 있도록 합니다.

이 장의 나머지 부분에서는 Visual Studio, Azure 및 Visual Studio Online에서 이러한 패턴의 일부 샘플 구현을 제공합니다.

- [Visual Studio에서 소스 제어에 스크립트 추가](#vsscripts)
- [Azure에서 중요 한 데이터 저장](#appsettings)
- [Visual Studio 및 Visual Studio에서 Git를 사용 하 여 온라인](#gittfs)

<a id="scripts"></a>
## <a name="treat-automation-scripts-as-source-code"></a>소스 코드로 취급 자동화 스크립트

클라우드 프로젝트에서 작업 하는 경우 자주 작업을 변경 하 고 고객에 게 보고 하는 문제를 신속 하 게 대응할 수 있게 되기를 원하는 합니다. 에 설명 된 대로도에서는 자동화 스크립트를 사용 하 여 신속 하 게 대응는 [모든 자동화](automate-everything.md) 장 합니다. 환경을 만드는 데 사용 하는 스크립트의 모든 배포를 크기 조정 응용 프로그램 소스 코드와 동기화 되도록 하 고, 등에서 필요 합니다.

스크립트 코드와 동기화를 유지 하려면 소스 제어 시스템에 저장 합니다. 그런 다음 해야 변경 내용을 적용 하거나 프로덕션 코드 개발 코드와에서 다른 빠른 수정을 확인, 되는 설정 변경 되었거나 필요한 버전의 복사본이 있는 팀 멤버 추적 하려고 하는 시간을 낭비 필요가 없습니다. 필요한 스크립트에 대 한 필요한 및 모든 팀 멤버는 동일한 스크립트를 사용 하는 보장 하는 코드 베이스를 가진 동기화 된 보장 하는 합니다. 그런 다음 테스트 및 프로덕션 또는 새로운 기능을 개발 하는 핫픽스의 배포를 자동화 해야 하는지 여부를 업데이트 해야 하는 코드에 대 한 올바른 스크립트를 해야 합니다.

<a id="secrets"></a>
## <a name="dont-check-in-secrets"></a>비밀 정보에서 확인 안 함

소스 코드 리포지토리는 일반적으로 너무 많은 사람들이 대 한 암호와 같은 중요 한 데이터에는 적절 하 게 안전한 곳에 액세스할 수 있습니다. 스크립트 암호와 같은 기밀 정보를 사용 하는 경우 이러한 설정을 다른 곳에 기밀 정보를 저장 하 고 소스 코드에 저장 하지 않는 있도록 매개 변수화 합니다.

예를 들어 Azure 사용 하면 포함 된 파일을 다운로드 게시의 게시 프로필 만들기를 자동화 하기 위해 설정 합니다. 이러한 파일에는 Azure 서비스를 관리 하려면 권한이 있는 사용자 이름 및 암호 포함 됩니다. 이 사용 하는 경우 게시 프로필을 만드는 메서드를 및 소스 제어에 이러한 파일을 선택 하면 해당 사용자 이름 및 암호 볼 수 있습니다 프로그램 저장소에 액세스할 수 있는 모든 사용자입니다. 안전 하 게에 저장할 수 있습니다는 암호 자체 게시 프로필은 암호화 되기 때문에 *. pubxml.user* 파일을 기본적으로 소스 제어에 포함 되지 않습니다.

<a id="devops"></a>
## <a name="structure-source-branches-to-facilitate-devops-workflow"></a>DevOps 워크플로 용이 하 게 하려면 소스 분기 구조

저장소에서 분기를 구현 하는 방법은 모두 새로운 기능을 개발 및 프로덕션 환경에서 문제를 해결 하는 기능을 영향을 줍니다. 패턴 중간 많은 팀 사용 크기는 다음과 같습니다.

![소스 분기 구조](source-control/_static/image1.png)

항상 마스터 분기에는 프로덕션 환경에 있는 코드와 일치 합니다. 마스터 아래 개발 수명 주기의 다른 단계에 해당합니다. Development 분기는 새로운 기능을 구현 하는 위치입니다. 소규모 팀에 대 한만 있을 수 마스터와 개발, 있지만 자주 사용자는 좋습니다 개발 및 마스터 간 준비 분기 합니다. 프로덕션 환경에 대 한 업데이트를 이동 하기 전에 최종 통합 테스트에 대 한 준비를 사용할 수 있습니다.

큰 팀에 있을 수 있습니다; 각 새로운 기능에 대 한 별도 분기 더 작은 팀에 대 한 체크 인에서 development 분기로 모든 사용자를 할 수 있습니다.

A 기능은 준비 하면 병합 하는 경우 각 기능에 대 한 분기를 설정한 경우 해당 소스 코드를 개발에 구성 변경 분기 하 고 다른 기능 분기 다운 합니다. 이 소스 코드 병합 프로세스는 시간이 오래 걸릴 수 있습니다 하 고 작동 하는 별도 기능을 그대로 유지 하면서를 방지 하려면 일부 팀 구현 호출 하는 대신 *[기능 설정/해제](http://en.wikipedia.org/wiki/Feature_toggle)* (라고도 *플래그 기능*). 즉, 같은 분기에서는의 모든 기능에 대 한 코드의 모든 있지만 사용 하도록 설정 하거나 코드에서 스위치를 사용 하 여 각 기능을 사용 하지 않도록 설정 합니다. 예를 들어, A 기능은 수정 응용 프로그램 작업에 대 한 새 필드 및 캐싱 기능을 추가 하는 기능 B Development 분기에 두 기능에 대 한 코드 수 있지만 앱 합니다만 표시 변수는 true로 설정 된 경우 새 필드 됩니다만 사용할 캐싱을 다른 변수에 설정 된 경우 true로 합니다. A 기능 수준을 올릴 수 없습니다. 기능 B가 준비 표시 되지만 모든 기능 A 스위치를 off를 사용 하 여 프로덕션 환경에 코드를 승격할 수 있습니다 하 고 기능 B 전환 합니다. 그런 다음 기능 A를 완료 하 고 승격 나중 없는 소스 코드 병합을 모두 수 있습니다.

예: 분기 또는 설정/해제를 사용 하 여 기능에 대 한 여부 이와 같은 분기 구조를 통해를 민첩 하 고 반복 가능한 방식으로 프로덕션 환경으로 개발에서 코드를 이동할 수 있습니다.

이 구조를 사용 하면 고객 피드백에 신속 하 게 대응할 수 있습니다. 프로덕션 환경에 빠른 픽스를 확인 해야 하는 경우 할 수 있는 하는 효율적으로 agile 방법으로 합니다. Master 또는 준비 분기를 만들 수 있습니다 및 마스터를 병합 하 고 아래쪽 설정이 끝나면로 기능 및 개발 합니다.

![Hotfix branch](source-control/_static/image2.png)

분기 구조 다음과 같이 프로덕션 및 development 분기의 해당 구분을 사용 하지 않고 프로덕션 문제 수 있습니다 위치에 배치 되어 프로덕션 수정 함께 새 기능 코드를 승격 하지 않아도 됩니다. 새 기능 코드에서 완전히 테스트 및 준비에 대 한 프로덕션 되지 않을 수 있습니다 및 많은 준비 되지 않은 변경 된 철회 하는 작업을 수행 해야 할 수 있습니다. 또는 지연 변경 내용을 테스트 하 고 배포할 준비가 얻으십시오 하기 위해 수정 해야 할 수 있습니다.

그런 다음 Visual Studio, Azure 및 Visual Studio Online에서 이러한 세 가지 패턴을 구현 하는 방법의 예에 표시 됩니다. 자세한 단계별 사용법-하려는 do-it 지침은; 보다는 예는 모든 필요한 컨텍스트를 제공 하는 자세한 지침을 참조 하십시오.는 [리소스](#resources) 장의 마지막 부분에 있습니다.

<a id="vsscripts"></a>
## <a name="add-scripts-to-source-control-in-visual-studio"></a>Visual Studio에서 소스 제어에 스크립트 추가

(소스 제어에 프로젝트 라고 가정함) Visual Studio 솔루션 폴더에 포함 하 여 Visual Studio에서 소스 제어에 스크립트를 추가할 수 있습니다. 한 가지 방법은 다음과 같습니다.

솔루션 폴더에는 스크립트에 대 한 폴더를 만듭니다 (동일한 폴더에 있는 프로그램 *.sln* 파일).

![자동화 폴더](source-control/_static/image3.png)

스크립트 파일을 폴더에 복사 합니다.

![자동화 폴더 내용](source-control/_static/image4.png)

Visual Studio에서 솔루션 폴더를 프로젝트에 추가 합니다.

![새 솔루션 폴더 메뉴 선택](source-control/_static/image5.png)

스크립트 파일은 솔루션 폴더에 추가 하십시오.

![기존 항목 메뉴 선택 항목 추가](source-control/_static/image6.png)

![기존 항목 추가 대화 상자](source-control/_static/image7.png)

이제 프로젝트에 포함 되므로 스크립트 파일 및 소스 제어의 버전 변경 내용 해당 소스 코드 변경 내용과 추적 하 합니다.

<a id="appsettings"></a>
## <a name="store-sensitive-data-in-azure"></a>Azure에서 중요 한 데이터 저장

응용 프로그램을 Azure 웹 사이트에서 실행 하는 경우 소스 제어에 자격 증명을 저장 하지 않도록 하는 한 가지 방법은 대신 Azure에 저장 하는 것입니다.

예를 들어 수정 응용 프로그램의 Web.config 파일 두 개의 연결 문자열에 한 프로덕션 및 Azure 저장소 계정에 대 한 액세스를 제공 하는 키의 암호를 저장 합니다.

[!code-xml[Main](source-control/samples/sample1.xml?highlight=2-3,11)]

이러한 설정에 대 한 실제 값을 두면 프로그램 *Web.config* 파일에 배치 하면 또는 *Web.Release.config* 파일을 배포 하는 동안에 삽입 하도록 Web.config 변환 구성 소스 저장소에 저장할 수 있습니다. 게시 프로필, 암호에 포함 됩니다는 프로덕션 환경에 데이터베이스 연결 문자열을 입력 하는 경우 프로그램 *.pubxml* 파일입니다. (제외할 수는 *.pubxml* 소스 제어에서 파일 있지만 다른 모든 배포 설정은 공유 활용할 수 없게 됩니다.)

Azure에 대 한 대안에서는 **appSettings** 연결 문자열의 섹션은 *Web.config* 파일입니다. 다음의 관련 부분을은 **구성** Azure 관리 포털에서 웹 사이트에 대 한 탭:

![포털에서 connectionStrings 및 appSettings](source-control/_static/image8.png)

이 웹 사이트 및 응용 프로그램을 실행 하는 프로젝트를 배포할 때 Azure에 저장 된 값의 Web.config 파일에 모든 값은 재정의 합니다.

관리 포털 또는 스크립트를 사용 하 여 Azure에서 이러한 값을 설정할 수 있습니다. 표시 하 여 환경 만들기 자동화 스크립트는 [모든 자동화](automate-everything.md) 장 Azure SQL 데이터베이스, 저장소 및 SQL 데이터베이스 연결 문자열을 가져옵니다 만들고 웹 사이트에 대 한 설정에서 이러한 암호를 저장 합니다.

[!code-powershell[Main](source-control/samples/sample2.ps1)]

[!code-powershell[Main](source-control/samples/sample3.ps1)]

스크립트는 실제 값 소스 저장소에 지속 되지 않도록 매개 변수화를 확인 합니다.

개발 환경에서 로컬로 실행할 때 앱 읽습니다 로컬 Web.config 파일 및 연결 문자열 지점에서 SQL Server LocalDB 데이터베이스에는 *앱\_데이터* 웹 프로젝트의 폴더입니다. Azure에서 응용 프로그램을 실행 하는 경우 응용 프로그램 Web.config 파일에서이 값을 읽을 하려고 어떻게 다시 가져오고 사용 하는 것이 아니라 실제로 Web.config 파일에서 웹 사이트에 대해 저장 된 값이 됩니다.

<a id="gittfs"></a>
## <a name="use-git-in-visual-studio-and-visual-studio-online"></a>Visual Studio 및 Visual Studio에서 Git를 사용 하 여 온라인

앞에서 제공한 DevOps 분기 구조를 구현 하는 원본 제어 환경을 사용할 수 있습니다. 분산된 팀에 대 한는 [분산 버전 제어 시스템](http://en.wikipedia.org/wiki/Distributed_revision_control) (DVCS) 가장 잘 작동 될 수 있습니다 다른 팀에 대 한;는 [시스템 중앙 집중식으로](http://en.wikipedia.org/wiki/Revision_control) 더 적합할 수 있습니다.

[Git](http://git-scm.com/) 있는 DVCS 인기 있는 바뀌었기 됩니다. 소스 제어에 Git를 사용 하면 로컬 컴퓨터에 기록의 모든 저장소의 전체 복사본이 있어야 합니다. 많은 사람들이 것이 더 쉬우므로 계속 해 서 네트워크에 연결 되지 않은 작업을 수행 하는 것 등의 작업을 커밋하고 롤백, 만들고 분기를 전환 하며 등을 선호 합니다. 네트워크에 연결 된 경우에 쉽고 빠르게 분기를 만들고 로컬 있으면 모든 분기를 변환할 수는 있습니다. 다른 개발자에 게 영향을 미치는 필요 없이 로컬 커밋 및 롤백 수행할 수 있습니다. 및 서버에 보내기 전에 커밋 일괄 처리할 수 있습니다.

[Microsoft Visual Studio Online](https://www.visualstudio.com/)(VSO) Team Foundation Service 라고 모두 Git를 제공 하는 이전 및 [Team Foundation 버전 제어](https://msdn.microsoft.com/library/ms181237(v=vs.120).aspx) (TFVC; 소스 제어를 중앙 집중식). 여기 Microsoft Azure의 그룹에서 어떤 팀 사용 하 여 중앙 집중식된 소스 제어에 배포 된 경우 일부 사용 하 고 일부는 조합 (일부 프로젝트에 대 한 중앙 집중식 및 다른 프로젝트에 대 한 분산)를 사용 합니다. VSO 서비스는 최대 5 명의 사용자에 대 한 무료입니다. 무료 계획에 등록할 수 [여기](https://go.microsoft.com/fwlink/?LinkId=307137)합니다.

기본 제공 기본 클래스를 포함 하는 visual Studio 2013 [Git 지원](https://msdn.microsoft.com/library/hh850437.aspx); 같습니다. 빠른 작동 하는 방법의 데모입니다.

Visual Studio 2013에서 열려 있는 프로젝트에서 솔루션을 마우스 오른쪽 단추로 **솔루션 탐색기**, 선택 **소스 제어에 솔루션 추가**합니다.

![소스 제어에 솔루션 추가](source-control/_static/image9.png)

Visual Studio (중앙 집중식된 버전 제어) TFVC 또는 Git을 사용 하려는 경우 요청 합니다.

![소스 컨트롤 선택](source-control/_static/image10.png)

Git를 선택 하 고 클릭 **확인**, Visual Studio 솔루션 폴더에 새 로컬 Git 리포지토리를 만듭니다. 새 저장소에 파일이 없습니다. Git 커밋 수행 하 여 저장소에 추가 해야 합니다. 솔루션을 마우스 오른쪽 단추로 클릭 **솔루션 탐색기**, 클릭 하 고 **커밋**합니다.

![커밋](source-control/_static/image11.png)

Visual Studio에서 자동으로 커밋에 대 한 프로젝트 파일을 모두 준비 하 고 목록에서 **팀 탐색기** 에 **포함 된 변경 내용** 창. (, 선택할 수 있는 경우 커밋에 포함 하지 않으려는 일부, 클릭 **제외**.)

![팀 탐색기](source-control/_static/image12.png)

커밋 주석에 입력 하 고 클릭 **커밋**, 커밋을 실행 하 고 커밋 ID를 표시 하는 Visual Studio 및

![팀 탐색기의 변경 내용](source-control/_static/image13.png)

이제 저장소에 포함 된 내용 다르도록 되도록 일부 코드를 변경한 경우에 쉽게 차이점을 볼 수 있습니다. 선택 파일을 변경 했으면을 마우스 오른쪽 단추로 **Unmodified 비교**, 커밋되지 않은 변경 내용을 보여 주는 비교 디스플레이 수 있게 합니다.

![수정 되지 않은 비교](source-control/_static/image14.png)

![차이점 표시 된 변경 내용](source-control/_static/image15.png)

변경 내용을 수행 하 고 체크 인을 쉽게 확인할 수 있습니다.

분기를 확인 해야 할 수 있는 하는 Visual Studio에서 너무 – 가정 합니다. **팀 탐색기**, 클릭 **새 분기**합니다.

![팀 탐색기의 새로운 분기](source-control/_static/image16.png)

분기 이름 입력 **분기 생성**, 선택한 **체크 아웃 분기**, 자동으로 체크 아웃 새 분기 합니다.

![팀 탐색기의 새로운 분기](source-control/_static/image17.png)

이제 파일을 변경 하 고이 분기를 체크 인할 수 있습니다. 및 쉽게 전환할 수 있습니다 분기와 Visual Studio 간에 자동으로 동기화 하면 분기 중 파일이 체크 아웃 합니다. 이 예에서 웹 페이지에 제목  *\_Layout.cshtml* "핫 1"의 수정 HotFix1 분기로 변경 되었습니다.

![Hotfix1 분기](source-control/_static/image18.png)

마스터로 다시 전환 하는 경우 분기, 내용의  *\_Layout.cshtml* 파일 마스터 분기에 무엇 인지에 자동으로 되돌립니다.

![마스터 분기](source-control/_static/image19.png)

이 간단한 예제를 신속 하 게 분기를 만들 하는 방법 간에 분기 사이 대칭 이동 합니다. 이 기능을 사용 하면 분기 구조를 사용 하는 매우 민첩 한 워크플로 및 자동화 스크립트에 표시 되는 [모든 자동화](automate-everything.md) 장 합니다. 예를 들어 할 수 있습니다 Development 분기에서 작업 마스터에서 핫픽스 분기 만들기, 새 분기로 전환, 변경 내용을 확인 및 커밋하기 하 고 Development 분기 다시 전환 합니다 및 하 던 작업을 계속 합니다.

Visual Studio의 로컬 Git 리포지토리를 이용한 사용법은 무엇을 보았을 여기입니다. 팀 환경에서 일반적으로 푸시할 변경 공용 리포지토리로 합니다. Visual Studio 도구를 사용 하면 원격 Git 리포지토리를 가리키도록 수도 있습니다. GitHub.com를 사용 하 여이 위해서는 하거나 사용할 수 있습니다 [Visual Studio Online에서 Git](https://msdn.microsoft.com/library/hh850437.aspx) 작업 항목 및 버그 추적와 같이 다른 모든 Visual Studio Online 기능에 통합 합니다.

물론 agile 분기 전략을 구현할 수 있습니다 하는 유일한 방법은 아닙니다. 중앙 집중식된 소스 제어 저장소를 사용 하 여 동일한 agile 워크플로 사용할 수 있습니다.

## <a name="summary"></a>요약

변경 하는 하 한 안전 하 고 예측 가능한 방식으로 동시에 얻을 수 하는 속도에 따라 소스 제어 시스템의 성공 여부를 측정 합니다. 를 찾을 경우 사용자가 직접 변경 하는 하루 또는에 수동 테스트 중 두 가지를 수행 해야 하기 때문에 무서 일까요 분 또는 1 시간 보다 더 이상 최저에서 변경을 수행할 수 있도록 process-wise 또는 test-wise 수행 해야 합니다. 작업을 수행 하는 한 가지 전략 연속 통합 및 지속적인 업데이트에서 다룰 것입니다를 구현 하는 것은 [다음 장에서](continuous-integration-and-continuous-delivery.md)합니다.

<a id="resources"></a>
## <a name="resources"></a>자료

[Visual Studio Online](https://www.visualstudio.com/) 설명서 및 지원 서비스를 제공 하는 포털 및 계정에 등록할 수 있습니다. Visual Studio 2012 있고 Git를 사용 하려는 경우 참조 [Visual Studio Tools for Git](https://visualstudiogallery.msdn.microsoft.com/abafc7d6-dcaa-40f4-8a5e-d6724bdb980c)합니다.

(중앙 집중식된 버전 제어) TFVC 및 Git (분산된 버전 제어)에 대 한 자세한 내용은 다음 리소스를 참조 합니다.

- [버전 제어 시스템을 사용 해야 합니까: TFVC 또는 Git?](https://msdn.microsoft.com/library/vstudio/ms181368.aspx#tfvc_or_git_summary) MSDN 설명서 TFVC 및 Git 간의 차이점을 요약 하는 테이블로 포함 됩니다.
- [마음에 Team Foundation Server 및 마음에 Git, 하지만, 보다 효율적인 프로토콜?](https://blogs.msdn.com/b/visualstudiouk/archive/2013/08/05/well-i-like-team-foundation-server-and-i-like-git-but-which-is-better.aspx) Git 및 TFVC 비교 합니다.

분기 전략에 대 한 자세한 내용은 다음 리소스를 참조 합니다.

- [Team Foundation server 2012 릴리스 파이프라인을 구축](https://msdn.microsoft.com/library/dn449957.aspx)합니다. Microsoft Patterns and Practices 설명서입니다. 분기 전략에 대 한 6 장을 참조 하십시오. 대표 기능은 기능 분기를 설정/해제 하 고 기능에 대 한 분기를 사용 하는 경우 보관 수명이 짧은 (시간 또는 일에서 최대) 대표 합니다.
- [버전 제어 가이드](https://aka.ms/vsarsolutions)합니다. ALM rangers 분기 전략을 안내 합니다. 다운로드 탭에 Strategies.pdf 분기를 참조 하십시오.
- [기능 설정/해제와 소프트웨어 개발](https://msdn.microsoft.com/magazine/dn683796.aspx)합니다. MSDN Magazine 문서입니다.
- [기능 설정/해제](http://martinfowler.com/bliki/FeatureToggle.html)합니다. 설정/해제 기능 소개/기능 Martin Fowler 블로그에서 플래그를 지정 합니다.
- [기능 설정/해제 vs 기능 분기](http://geekswithblogs.net/Optikal/archive/2013/02/10/152069.aspx)합니다. Dylan Smith가 기능 설정/해제 하는 방법에 대 한 다른 블로그 게시물

소스 제어 저장소에 보관할 하지 않은 중요 한 정보를 처리 하는 방법에 대 한 자세한 내용은 다음 리소스를 참조 합니다.

- [ASP.NET 및 Azure 앱 서비스에 암호 및 기타 중요 한 데이터 배포에 대 한 유용한](../../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)합니다.
- [Azure 웹 사이트: 방법을 응용 프로그램 문자열 및 연결 문자열의 작동](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)합니다. 재정의 하는 Azure 기능에 설명 `appSettings` 및 `connectionStrings` 의 데이터는 *Web.config* 파일입니다.
- [사용자 지정 구성 및 응용 프로그램 설정에서 Azure 웹 사이트-Stefan Schackow](https://azure.microsoft.com/documentation/videos/configuration-and-app-settings-of-azure-web-sites/)합니다.

소스 제어에서 중요 한 정보를 유지 하기 위한 다른 방법에 대 한 정보를 참조 하십시오. [ASP.NET MVC: 소스 제어의 개인 설정의 유지](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx)합니다.

> [!div class="step-by-step"]
> [이전](automate-everything.md)
> [다음](continuous-integration-and-continuous-delivery.md)
