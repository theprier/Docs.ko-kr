---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment
title: "웹 배포에 적절 한 방식을 선택 | Microsoft Docs"
author: jrjlee
description: "인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포) 2.0 이상 작업할 때는 다음 3 가지 주요 방법 가져오는 데 사용할 수 있습니다..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 787a53fd-9901-4a11-9d58-61e0509cda45
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 5265f9962ca6244b1fe13ca6e37a5217c15b8cdf
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="choosing-the-right-approach-to-web-deployment"></a>웹 배포에 적합 한 접근 방식을 선택합니다.
====================
으로 [Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포) 2.0 이상 작업할 때는 다음 3 가지 주요 방법 웹 서버에 패키지에 포함 된 웹 응용 프로그램을 가져오는 데 사용할 수 있습니다. 제출할 수 있습니다.
> 
> - 대상으로 하 여 원격 위치에서 응용 프로그램을 배포는 *웹 배포 에이전트 서비스가* (라고도 "원격 에이전트") 대상 서버에 있습니다.
> - 웹 배포 요청 시 (또는 "임시 에이전트")를 사용 하 여 원격 위치에서 응용 프로그램을 배포 합니다.
> - 대상으로 하 여 원격 위치에서 응용 프로그램 배포는 *IIS 웹 배포 처리기* 대상 서버에 있습니다.
> - 수동으로 웹 패키지에서 대상 서버로 복사 하 고 IIS 관리자를 통해 가져와서 응용 프로그램을 배포 합니다.
> 
> 대상 웹 서버를 구성 하는 방법에 사용 하려는 방법 배포에 따라 달라 집니다. 이 항목은 어떤 배포 방법이 적합 한지 결정 하는 데 도움이 됩니다.


이 표에서 가장 일반적으로 각 접근 방식에 따라 시나리오와 함께 각 배포 방법의 주요 장단점을 보여 줍니다.

| 방법 | 장점 | 단점 | 일반적인 시나리오 |
| --- | --- | --- | --- |
| 원격 에이전트 | 설정 하는 것이 쉽습니다. 이 웹 응용 프로그램 및 콘텐츠를 정기적으로 업데이트에 적합 합니다. | 사용자는 대상 서버에서 관리자 여야 합니다. 사용자 대체 자격 증명을 지정할 수 없습니다. | 개발 환경입니다. 테스트 환경. |
| 임시 에이전트 | 대상 컴퓨터에 웹 배포를 설치 하지 않아도가 있습니다. 최신 버전의 웹 배포를 자동으로 사용 됩니다. | 사용자는 대상 서버에서 관리자 여야 합니다. 사용자 대체 자격 증명을 지정할 수 없습니다. | 개발 환경입니다. 테스트 환경. |
| 웹 배포 처리기 | 관리자가 아닌 사용자가 콘텐츠를 배포할 수 있습니다. 이 웹 응용 프로그램 및 콘텐츠를 정기적으로 업데이트에 적합 합니다. | 이를 설정 하려면 훨씬 복잡 합니다. | 스테이징 환경입니다. 인트라넷 프로덕션 환경입니다. 호스트 된 환경입니다. |
| 오프 라인 배포 | 매우를 설정 하는 것이 쉽습니다. 이 격리 된 환경에 적합 합니다. | 수동으로 서버 관리자를 복사 하 고 매번 웹 패키지를 가져올 해야 합니다. | 인터넷 연결 프로덕션 환경입니다. 격리 된 네트워크 환경입니다. |
  

## <a name="using-the-remote-agent"></a>원격 에이전트를 사용 하 여

대상 서버에서 기본 설정을 사용 하 여 웹 배포를 설치할 때 웹 배포 에이전트 서비스 ("원격 에이전트") 자동으로 설치 및 시작 합니다. 기본적으로 원격 에이전트는이 주소에 HTTP 끝점을 노출합니다.


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample1.cmd)]


> [!NOTE]
> 바꿀 수 있습니다 [*서버*] 웹 서버의 컴퓨터 이름, 웹 서버 또는 호스트 이름에 대 한 IP 주소 하는 확인을 웹 서버.


서버 관리자는이 끝점 주소를 지정 하 여 개발자 컴퓨터 또는 빌드 서버와 같은 원격 위치에서 웹 패키지를 배포할 수 있습니다. 예를 들어, Fabrikam, Inc.에서 Matt Hink가 개발자 컴퓨터에서 ContactManager.Mvc 웹 응용 프로그램 프로젝트를 만들었습니다. 빌드 프로세스와 함께 웹 패키지를 생성 한 *. deploy.cmd* 패키지를 설치 하는 데 필요한 웹 배포 명령이 포함 된 파일입니다. Matt TESTWEB1 서버에서 서버 관리자 이면가 개발자 컴퓨터에서이 명령을 실행 하 여 테스트 웹 서버에 웹 응용 프로그램을 배포할 수 그:


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample2.cmd)]


실제 팩트 Matt만에 다음과 같이 입력 해야 하므로 컴퓨터 이름을 제공 하는 경우 웹 배포 실행 파일 원격 에이전트의 끝점 주소를 유추할 수 있습니다.


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample3.cmd)]


> [!NOTE]
> 웹 배포 명령줄 구문에 대 한 자세한 내용은 및 *. deploy.cmd* 파일, 참조 [하는 방법: 설치는 배포 패키지를 사용 하 여 파일 deploy.cmd](https://msdn.microsoft.com/en-us/library/ff356104.aspx)합니다.


원격 에이전트는 원격 위치에서 콘텐츠를 배포 하는 간단한 방법을 제공 하 고이 방법은 한 번의 클릭 또는 자동화 된 배포 함께 사용할 수 있습니다. 그러나 대상 서버에서 로컬 관리자 그룹의 멤버 또는 도메인 관리자는 배포 명령을 실행 하는 사용자 수도 있어야 합니다. 또한 원격 에이전트 명령줄에서 대체 자격 증명을 전달할 수 없으며 하므로 기본 인증을 지원 하지 않습니다.

원격 에이전트를 배포 개발 또는 테스트 시나리오를 여기서 개발자가 테스트 서버 환경에 대 한 전체 관리자 제어도 드물지 않습니다 및 응용 프로그램은 일반적으로 다시 작성 하며 매우 다시 배포에 유용한 접근 방법 제공 자주 있습니다. 그러나이 방법은 스테이징 또는 프로덕션 환경에 대 한 일반적으로 허용 합니다.

원격 에이전트 접근 방식을 사용 하는 시나리오의 종단 간 예제를 보려면 [시나리오: 웹 배포를 위해 테스트 환경 구성](scenario-configuring-a-test-environment-for-web-deployment.md)합니다.

## <a name="using-the-temp-agent"></a>임시 에이전트 사용

배포 하는 임시 에이전트 방법은 원격 에이전트 접근 하는 것과 비슷합니다. 그러나 원격 에이전트 접근 방식을 달리 대상 웹 서버에 웹 배포를 설치할 필요가 없습니다. 배포를 수행 하는 경우 대신, 대상 서버에 웹 배포 에이전트 서비스의 임시 버전을 설치 합니다 웹 배포 및 IIS에 콘텐츠를 배포 하려면이 사용 합니다. 배포가 완료 되 면 임시 파일을 모두 제거 됩니다.

임시 에이전트 공급자 설정을 사용 하 여, 추가 하려는 경우는 **/g** 사용자의 배포 명령 플래그:


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample4.cmd)]


> [!NOTE]
> 사용할 수 없습니다 임시 에이전트 웹 배포 에이전트 서비스가 대상 컴퓨터에 설치 된 경우는 서비스가 실행 되지 않는 경우에 합니다.


이 방법의 장점은 대상 서버에 웹 배포의 설치를 유지 관리할 필요가 없습니다. 또한 원본 및 대상 컴퓨터는 동일한 버전의 웹 배포를 실행 중인지 확인 필요가 없습니다. 그러나이 방법은 저하 원격 에이전트 방법으로 동일한 주 제한 사항을 즉 콘텐츠를 배포 하기 위해 대상 서버에서 로컬 관리자 여야 합니다. 및 NTLM 인증만 지원 됩니다. 임시 에이전트 접근 방식을 대상 환경의 훨씬 더 초기 구성을 해야합니다.

임시 에이전트 사용에 대 한 자세한 내용은 참조 하십시오. [하는 방법: 설치 된 배포 패키지를 사용 하 여 파일 deploy.cmd](https://msdn.microsoft.com/en-us/library/ff356104.aspx) 및 [주문형 웹 배포](https://technet.microsoft.com/en-us/library/ee517345(WS.10).aspx)합니다.

## <a name="using-the-web-deploy-handler"></a>처리기를 배포 하는 웹을 사용 하 여

IIS 7부터에 대 한 웹 배포에서는 IIS 웹 배포 처리기를 통해 다른 배포 방법을 제공합니다. 웹 배포 처리기 IIS 웹 관리 서비스 (WMSvc)를 통해 사용자가 원격 위치에서 IIS 웹 사이트를 관리할 수 있는 밀접 하 게 통합 되어 있습니다.

기본적으로 원격 에이전트는이 주소에 HTTP 끝점을 노출합니다.


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample5.cmd)]


> [!NOTE]
> 바꿀 수 있습니다 [*서버*] 웹 서버의 컴퓨터 이름, 웹 서버 또는 호스트 이름에 대 한 IP 주소 하는 확인을 웹 서버.


원격 에이전트와 임시 에이전트를 통해 웹 배포 처리기의 가장 큰 장점은 관리자가 아닌 사용자가 특정 IIS 웹 사이트에 응용 프로그램 및 콘텐츠를 배포할 수 있도록 IIS를 구성할 수 있습니다. 웹 배포 명령에서는 매개 변수로 대체 자격 증명을 제공할 수 있도록 웹 배포 처리기는 또한 기본 인증을 지원 합니다. 주요 단점은 웹 배포 처리기가 처음 설정 및 구성에 훨씬 더 복잡 합니다.

관리자가 아닌 사용자의 경우 웹 관리 서비스 (WMSvc)만 하면 사용자 IIS에 연결할 서버 수준 연결이 아닌 사이트 수준 연결을 사용 하 여 있습니다. 특정 사이트에 액세스 하는 끝점 주소에 사이트별 쿼리 문자열을 포함할 수 있습니다.


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample6.cmd)]


예를 들어 빌드 프로세스를 자동으로 모든 작업을 성공적으로 빌드한 후 스테이징 환경에 웹 응용 프로그램을 배포 하도록 구성 됩니다. 원격 에이전트 접근을 사용 하는 경우 대상 서버에서 관리자가 빌드 프로세스 id를 확인 해야 합니다. 반면, 웹 배포 처리기 방식을 사용 하 여 제공할 수 있습니다는 관리자가 아닌 사용자 & #x 2014; **FABRIKAM\stagingdeployer** 특정 IIS 웹 사이트 에서만 및 빌드 프로세스에 사용 권한을이 대/소문자 & #x 2014;에 웹 패키지를 배포 하려면 이러한 자격 증명을 제공할 수 있습니다.


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample7.cmd)]


> [!NOTE]
> 명령줄 작업 웹 배포 및 구문에 대 한 자세한 내용은 참조 하십시오. [배포 명령줄 참조 웹](https://technet.microsoft.com/en-us/library/dd568991(v=ws.10).aspx)합니다. 사용 하 여 대 한 자세한 내용은 *. deploy.cmd* 파일에서 참조 [하는 방법: 설치는 배포 패키지를 사용 하 여 파일 deploy.cmd](https://msdn.microsoft.com/en-us/library/ff356104.aspx)합니다.


웹 배포 처리기 배포 환경, 호스팅된 환경 및 인트라넷 기반 프로덕션 환경에서는 원격 액세스 서버를 사용할 수 있지만 관리자 자격 증명이 있는 준비에 유용한 접근 방법을 제공 합니다.

웹 배포 처리기 접근 방식을 사용 하는 시나리오의 종단 간 예제를 참조 하세요. [시나리오: 웹 배포에 대 한 스테이징 환경 구성](scenario-configuring-a-staging-environment-for-web-deployment.md)합니다.

## <a name="using-offline-deployment"></a>오프 라인 배포를 사용 하 여

경우에 따라 것 수 없거나 원격 위치에서 IIS 웹 사이트를 응용 프로그램 및 콘텐츠를 배포 하기에 적합 합니다. 예를 들어 원본 및 대상 컴퓨터에 격리 된 네트워크 또는 네트워크 세그먼트 중이거나 방화벽 정책을 원격 액세스를 허용 하지 않을 수도 있습니다.

이와 같은 시나리오에서 사용할 수 있습니다 패키징 및 게시 웹 배포;의 기능 바로 사용할 수 없습니다는 원격 위치에서 합니다. 대신, 대상 서버에서 관리자는 서버에 웹 패키지를 복사 하 고 IIS 관리자를 통해 가져올 해야 합니다.

![](choosing-the-right-approach-to-web-deployment/_static/image1.png)

오프 라인 배포 방법은 여기서 경계 네트워크에에서 서버를 제한 한 내부 네트워크의 컴퓨터와 연결 되는 인터넷 연결 프로덕션 환경에서 일반적으로 유용 합니다.

오프 라인 배포 방법을 사용 하 여 시나리오의 종단 간 예제를 보려면 [시나리오: 웹 배포를 위해 프로덕션 환경 구성](scenario-configuring-a-production-environment-for-web-deployment.md)합니다.

## <a name="further-reading"></a>추가 정보

명령줄 작업 웹 배포 및 구문에 대 한 자세한 내용은 참조 하십시오. [배포 명령줄 참조 웹](https://technet.microsoft.com/en-us/library/dd568991(v=ws.10).aspx)합니다. 사용 하 여 대 한 자세한 내용은 *. deploy.cmd* 파일에서 참조 [하는 방법: 설치는 배포 패키지를 사용 하 여 파일 deploy.cmd](https://msdn.microsoft.com/en-us/library/ff356104.aspx)합니다.

원격 컴퓨터에서 웹 패키지를 배포할 수 있는 다양 한 방법에 대 한 보다 일반적인 지침을 참조 하십시오. [를 사용 하 여 웹 배포 원격으로](https://technet.microsoft.com/en-us/library/ee461175(WS.10).aspx)합니다. 주문형 웹 배포 사용에 대 한 자세한 내용은 참조 하십시오. [주문형 웹 배포](https://technet.microsoft.com/en-us/library/ee517345(WS.10).aspx)합니다.

>[!div class="step-by-step"]
[이전](configuring-server-environments-for-web-deployment.md)
[다음](scenario-configuring-a-test-environment-for-web-deployment.md)
