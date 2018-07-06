---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment
title: 웹 배포에 적절 한 방식을 선택 | Microsoft Docs
author: jrjlee
description: 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포) 2.0 이상을 사용 하 여 작업할 때 다음 3 가지 주요 방법 가져오는 데 사용할 수 있습니다...
ms.author: aspnetcontent
ms.date: 05/04/2012
ms.assetid: 787a53fd-9901-4a11-9d58-61e0509cda45
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: eb1b7d50e5d7461d760ad7a963cc70369b7a4513
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37807053"
---
<a name="choosing-the-right-approach-to-web-deployment"></a>웹 배포에 적절 한 방식을 선택
====================
[Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포) 2.0 이상을 사용 하 여 작업할 때 세 가지 기본 방법이 패키징된 웹 응용 프로그램을 웹 서버를 사용할 수 있습니다. 하거나 다음을 수행할 수 있습니다.
> 
> - 대상으로 하 여 원격 위치에서 응용 프로그램을 배포 합니다 *웹 배포 에이전트 서비스가* (라고도 "원격 에이전트") 대상 서버에서.
> - 주문형 웹 배포 (라고도 "임시 에이전트")를 사용 하 여 원격 위치에서 응용 프로그램을 배포 합니다.
> - 대상으로 하 여 원격 위치에서 응용 프로그램을 배포 합니다 *IIS 웹 배포 처리기* 대상 서버에서.
> - 수동으로 웹 패키지를 대상 서버로 복사 하 고 IIS 관리자를 통해 가져와서 응용 프로그램을 배포 합니다.
> 
> 대상 웹 서버를 구성 하는 방법을 사용 하려는 배포 하는 방법에 따라 달라 집니다. 이 항목에서는 배포에 어떤 접근 방식이 적합 한지 결정 하는 데 도움이 됩니다.


이 표에서 가장 일반적으로 각 접근 방식에 맞는 시나리오와 함께 각 배포 접근 방법의 주요 장단점을 보여줍니다.

| 방법 | 장점 | 단점 | 일반적인 시나리오 |
| --- | --- | --- | --- |
| 원격 에이전트 | 설정 하는 것이 쉽습니다. 정기적으로 웹 응용 프로그램 및 콘텐츠 업데이트에는 것이 적합합니다. | 사용자는 대상 서버의 관리자 여야 합니다. 사용자는 대체 자격 증명을 제공할 수 없습니다. | 개발 환경입니다. 테스트 환경입니다. |
| 임시 에이전트 | 대상 컴퓨터에서 웹 배포를 설치할 필요가 없습니다 있습니다. 최신 버전의 웹 배포를 자동으로 사용 됩니다. | 사용자는 대상 서버의 관리자 여야 합니다. 사용자는 대체 자격 증명을 제공할 수 없습니다. | 개발 환경입니다. 테스트 환경입니다. |
| 웹 배포 처리기 | 관리자가 아닌 사용자가 콘텐츠를 배포할 수 있습니다. 정기적으로 웹 응용 프로그램 및 콘텐츠 업데이트에는 것이 적합합니다. | 이 설정 하기 위해 훨씬 더 복잡 합니다. | 스테이징 환경입니다. 인트라넷 프로덕션 환경입니다. 호스 티 드 환경입니다. |
| 오프 라인 배포 | 매우 설정 하는 것이 쉽습니다. 격리 된 환경에 적합 합니다. | 수동으로 서버 관리자를 복사 하 고 때마다 웹 패키지를 가져올 해야 합니다. | 인터넷 프로덕션 환경입니다. 격리 된 네트워크 환경입니다. |
  

## <a name="using-the-remote-agent"></a>원격 에이전트를 사용 하 여

대상 서버에서 기본 설정을 사용 하 여 웹 배포를 설치할 때 웹 배포 에이전트 서비스 ("원격 에이전트") 자동으로 설치 및 시작 합니다. 기본적으로 원격 에이전트는이 주소에서 HTTP 끝점을 노출합니다.


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample1.cmd)]


> [!NOTE]
> 바꿀 수 있습니다 [*server*] 웹 서버의 컴퓨터 이름을 사용 하 여 웹 서버 또는 호스트 이름에 대 한 IP 주소를 확인 하는 웹 서버에 있습니다.


서버 관리자는이 끝점 주소를 지정 하 여 개발자 컴퓨터 또는 빌드 서버와 같은 원격 위치에서 웹 패키지를 배포할 수 있습니다. 예를 들어, Fabrikam, Inc.에서 Matt Hink 개발자 컴퓨터 ContactManager.Mvc 웹 응용 프로그램 프로젝트를 만들었습니다. 빌드 프로세스와 함께 웹 패키지를 생성 한 *. deploy.cmd* 웹 배포 명령이 포함 된 파일 패키지를 설치 하는 데 필요한 합니다. Matt TESTWEB1 서버의 서버 관리자 인 경우 그의 개발자 컴퓨터에서이 명령을 실행 하 여 테스트 웹 서버에 웹 응용 프로그램을 배포할 수 그.


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample2.cmd)]


사실 실제 웹 배포 실행 파일 Matt만 입력 해야 하므로 컴퓨터 이름을 제공 하는 경우 원격 에이전트의 끝점 주소를 유추할 수 있습니다.


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample3.cmd)]


> [!NOTE]
> 웹 배포 명령줄 구문에 대 한 자세한 내용은 및 *. deploy.cmd* 파일을 참조 하세요 [방법: 설치 된 배포 패키지를 사용 하 여 deploy.cmd 파일](https://msdn.microsoft.com/library/ff356104.aspx).


원격 에이전트는 원격 위치에서 콘텐츠를 배포 하는 간단한 방법을 제공 하 고이 이렇게 한 번의 클릭 또는 자동화 된 배포 함께 사용할 수 있습니다. 그러나 도메인 관리자 또는 멤버인 대상 서버의 로컬 관리자 그룹의 배포 명령을 실행 하는 사용자 수도 있어야 합니다. 또한 원격 에이전트 명령줄에서 대체 자격 증명을 전달할 수 없습니다 있도록 기본 인증을 지원 하지 않습니다.

원격 에이전트는 개발 또는 테스트 시나리오에서 개발자가 테스트 서버 환경에 대 한 전체 관리자 제어도 드물지 않습니다 않았고 응용 프로그램을 다시 작성 및 다시 매우 일반적으로 배포 하는 유용한 방법을 제공합니다 자주 합니다. 그러나이 방법은 스테이징 또는 프로덕션 환경에 대 한 일반적으로 허용 합니다.

원격 에이전트 방법을 사용 하는 시나리오의 종단 간 예제를 참조 하세요 [시나리오: 웹 배포용 테스트 환경 구성](scenario-configuring-a-test-environment-for-web-deployment.md)합니다.

## <a name="using-the-temp-agent"></a>임시 에이전트 사용

배포 하는 임시 에이전트 방법은 원격 에이전트 접근 방식은 비슷합니다. 그러나 원격 에이전트 방법을 달리 대상 웹 서버에서 웹 배포를 설치할 필요가 없습니다. 배포를 수행 하면 대신 대상 서버에 웹 배포 에이전트 서비스의 임시 버전을 설치 하는 웹 배포 및 IIS에 콘텐츠를 배포 하려면이 사용 됩니다. 배포가 완료 되 면 임시 파일을 모두 제거 됩니다.

임시 에이전트 공급자 설정을 사용 하 여, 추가 하려는 경우는 **/g** 배포 명령 플래그:


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample4.cmd)]


> [!NOTE]
> 사용할 수 없습니다 임시 에이전트가 대상 컴퓨터의 웹 배포 에이전트 서비스가 설치 된 경우 서비스를 실행 하지 않는 경우에 합니다.


이 방식의 장점은 대상 서버에서의 웹 배포 설치를 유지 관리할 필요가 없습니다. 또한 원본 및 대상 컴퓨터를 동일한 버전의 웹 배포 실행 되도록 필요가 없습니다. 그러나이 방법은 저하 원격 에이전트 접근 방식으로 동일한 보안 주체 제한에서 namely 콘텐츠를 배포 하려면 대상 서버의 로컬 관리자를 사용 해야 하 고 NTLM 인증만 지원 됩니다. 임시 에이전트 접근 방식에는 또한 대상 환경의 훨씬 초기 구성이 필요합니다.

임시 에이전트 사용에 대 한 자세한 내용은 참조 하세요. [방법:는 배포 패키지를 사용 하 여 deploy.cmd 파일 설치](https://msdn.microsoft.com/library/ff356104.aspx) 하 고 [주문형 웹 배포](https://technet.microsoft.com/library/ee517345(WS.10).aspx)합니다.

## <a name="using-the-web-deploy-handler"></a>처리기는 웹을 사용 하 여 배포

IIS 7 이상에 대 한 웹 배포는 IIS 웹 배포 처리기를 통해 다른 배포 방법을 제공합니다. 웹 배포 처리기는 IIS 웹 관리 서비스 (WMSvc)를 사용자가 원격 위치에서 IIS 웹 사이트를 관리할 수 있도록 설계 된와 밀접 하 게 통합 됩니다.

기본적으로 원격 에이전트는이 주소에서 HTTP 끝점을 노출합니다.


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample5.cmd)]


> [!NOTE]
> 바꿀 수 있습니다 [*server*] 웹 서버의 컴퓨터 이름을 사용 하 여 웹 서버 또는 호스트 이름에 대 한 IP 주소를 확인 하는 웹 서버에 있습니다.


원격 에이전트와 임시 에이전트를 통해 웹 배포 처리기의 가장 큰 장점은 관리자가 아닌 사용자가 특정 IIS 웹 사이트에 응용 프로그램 및 콘텐츠를 배포할 수 있도록 IIS를 구성할 수 있습니다. 웹 배포 명령에서는 매개 변수로 대체 자격 증명을 제공할 수 있도록 웹 배포 처리기는 또한 기본 인증을 지원 합니다. 주요 단점은 웹 배포 처리기가 처음 설정 하 고 구성 하려면 훨씬 더 복잡 합니다.

관리자가 아닌 사용자의 경우 웹 관리 서비스 (WMSvc)만 하면 IIS에 연결할 서버 수준 연결이 아닌 사이트 수준 연결을 사용 합니다. 특정 사이트에 액세스 하려면 끝점 주소에서 사이트별 쿼리 문자열을 포함할 수 있습니다.


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample6.cmd)]


예를 들어, 빌드 프로세스를 자동으로 모든 빌드가 성공한 후 스테이징 환경에 웹 응용 프로그램을 배포 하도록 구성 되어 있습니다. 원격 에이전트 접근 방식, 사용 하는 경우 대상 서버에서 관리자로 빌드 프로세스 id를 확인 해야 합니다. 반면, 웹 배포 처리기 방식을 사용 하 여 제공할 수 있습니다 비관리자 사용자&#x2014;**FABRIKAM\stagingdeployer** 여기서&#x2014;이러한 특정 IIS 웹 사이트에만 되며 빌드 프로세스가 권한을 제공할 수 있습니다 웹 패키지를 배포 자격 증명입니다.


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample7.cmd)]


> [!NOTE]
> 웹 배포 명령줄 작업 구문에 대 한 자세한 내용은 참조 하세요. [웹 배포 명령줄 참조](https://technet.microsoft.com/library/dd568991(v=ws.10).aspx)합니다. 사용 하 여 대 한 자세한 내용은 합니다 *. deploy.cmd* 파일을 참조 하세요 [방법:는 배포 패키지를 사용 하 여 deploy.cmd 파일 설치](https://msdn.microsoft.com/library/ff356104.aspx).


웹 배포 처리기를 스테이징 환경, 호스팅된 환경 및 원격 액세스 서버를 사용할 수 있지만 관리자 자격 증명이 있는 인트라넷을 기반으로 프로덕션 환경에 배포 하는 유용한 방법을 제공 합니다.

웹 배포 처리기 방법을 사용 하는 시나리오의 종단 간 예제를 참조 하세요 [시나리오: 웹 배포용 스테이징 환경 구성](scenario-configuring-a-staging-environment-for-web-deployment.md)합니다.

## <a name="using-offline-deployment"></a>오프 라인 배포를 사용 하 여

경우에 따라 가능한 또는 아닙니다 원격 위치에서 IIS 웹 사이트에 응용 프로그램 및 콘텐츠를 배포 하는 데 적합 합니다. 예를 들어, 원본 및 대상 컴퓨터를 격리 된 네트워크 또는 네트워크 세그먼트에 있을 수 있습니다 또는 방화벽 정책을 원격 액세스를 허용 하지 않을 수 있습니다.

다음과 같은 시나리오에서 계속 사용할 수 있습니다 패키징 및 게시 웹 배포;의 기능 바로 사용할 수 없습니다 하 원격 위치에서. 대신, 대상 서버에서 관리자로 서버에 웹 패키지를 복사 하 고 IIS 관리자를 통해 가져올 해야 합니다.

![](choosing-the-right-approach-to-web-deployment/_static/image1.png)

오프 라인 배포 방식은 있는 경계 네트워크의 서버 제한 될 수 있습니다 내부 네트워크에서 컴퓨터와 연결 되는 인터넷 프로덕션 환경에서는 일반적으로 유용 합니다.

오프 라인 배포 방법을 사용 하는 시나리오의 종단 간 예제를 참조 하세요 [시나리오: 웹 배포용 프로덕션 환경 구성](scenario-configuring-a-production-environment-for-web-deployment.md)합니다.

## <a name="further-reading"></a>추가 정보

웹 배포 명령줄 작업 구문에 대 한 자세한 내용은 참조 하세요. [웹 배포 명령줄 참조](https://technet.microsoft.com/library/dd568991(v=ws.10).aspx)합니다. 사용 하 여 대 한 자세한 내용은 합니다 *. deploy.cmd* 파일을 참조 하세요 [방법:는 배포 패키지를 사용 하 여 deploy.cmd 파일 설치](https://msdn.microsoft.com/library/ff356104.aspx).

원격 컴퓨터에서 웹 패키지를 배포할 수 있는 다양 한 방법에 대 한 보다 일반적인 지침을 참조 하세요 [를 사용 하 여 웹 배포 원격](https://technet.microsoft.com/library/ee461175(WS.10).aspx)합니다. 주문형 웹 배포 사용에 대 한 자세한 내용은 참조 하세요. [주문형 웹 배포](https://technet.microsoft.com/library/ee517345(WS.10).aspx)합니다.

> [!div class="step-by-step"]
> [이전](configuring-server-environments-for-web-deployment.md)
> [다음](scenario-configuring-a-test-environment-for-web-deployment.md)
