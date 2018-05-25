---
uid: web-api/overview/security/working-with-ssl-in-web-api
title: Web API의에서 SSL 작업 | Microsoft Docs
author: MikeWasson
description: SSL 클라이언트 인증서를 사용 하는 등 ASP.NET Web API를 함께 SSL을 사용 하는 방법을 보여 줍니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/12/2012
ms.topic: article
ms.assetid: 97f6164f-59cf-45c0-b820-e4aa29b45396
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/security/working-with-ssl-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 127b336cb628e55bd59481ecb1c4df83960dc25b
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="working-with-ssl-in-web-api"></a>Web API의에서 SSL 작업
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

일반 HTTP를 통해 몇 가지 일반적인 인증 체계는 안전 하지 않습니다. 특히 기본 인증 및 폼 인증 암호화 되지 않은 자격 증명을 보냅니다. 보안 이러한 인증 체계 *해야* SSL을 사용 합니다. 또한 클라이언트를 인증 하 SSL 클라이언트 인증서를 사용할 수 있습니다.

## <a name="enabling-ssl-on-the-server"></a>서버에 SSL을 사용 하도록 설정

이상 IIS 7에서 SSL을 설정 하려면:

- 만들거나 인증서를 가져옵니다. 테스트를 위해 자체 서명 된 인증서를 만들 수 있습니다.
- HTTPS 바인딩을 추가 합니다.

자세한 내용은 참조 [IIS 7에서 SSL을 설정 하는 방법을](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis)합니다.

로컬 테스트에 대 한 Visual Studio에서 IIS Express에서 SSL을 사용할 수 있습니다. 속성 창에서 설정 **SSL 사용** 를 **True**합니다. 값을 확인 **SSL URL**;이 URL을 사용 하 여 HTTPS 연결을 테스트 합니다.

![](working-with-ssl-in-web-api/_static/image1.png)

### <a name="enforcing-ssl-in-a-web-api-controller"></a>Web API 컨트롤러에서 SSL을 강제 적용

에서 HTTPS 및 HTTP 바인딩을 모두 있는 경우 클라이언트는 사이트 액세스에 HTTP를 계속 사용할 수 있습니다. 다른 리소스 ssl을 사용 하는 동안 HTTP를 통해 사용할 수 있는 일부 리소스를 통합할 수 있습니다. 이 경우 작업 필터를 사용 하 여 보호 된 리소스에 대 한 SSL을 요구 하도록 합니다. 다음 코드에서는 SSL을 확인 하는 Web API 인증 필터를 보여 줍니다.

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample1.cs)]

Ssl을 사용 하는 모든 웹 API 작업에이 필터를 추가 합니다.

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample2.cs)]

## <a name="ssl-client-certificates"></a>SSL 클라이언트 인증서

SSL은 인증서 공개 키 인프라를 사용 하 여 인증을 제공 합니다. 서버는 클라이언트에 서버를 인증 하는 인증서를 제공 해야 합니다. 서버에 인증서를 제공 하는 클라이언트에 대 한 덜 일반적 이기는 하지만이 클라이언트 인증을 위해 한 가지 옵션입니다. Ssl 클라이언트 인증서를 사용 하려면 사용자에 게 서명 된 인증서를 배포 하는 방법이 필요 합니다. 많은 응용 프로그램 종류에 대 한 효율적인 사용자 환경이 되지 않습니다 되지만 일부 환경 (예를 들어 enterprise) 가능 될 수 있습니다.

| 장점 | 단점 |
| --- | --- |
| -인증서 자격 증명은 사용자 이름/암호 보다 더 강력 합니다. SSL 인증, 메시지 무결성 및 메시지 암호화 전체 보안 채널을 제공합니다. | -해야 받으며 PKI 인증서를 관리 합니다. -클라이언트 플랫폼 SSL 클라이언트 인증서를 지원 해야 합니다. |

클라이언트 인증서를 수락 하도록 IIS를 구성 하려면 IIS 관리자를 열고 다음 단계를 수행 합니다.

1. 트리 보기에서 사이트 노드를 클릭 합니다.
2. 두 번 클릭 하 여 **SSL 설정** 가운데 창에서 기능.
3. 아래 **클라이언트 인증서**, 이러한 옵션 중 하나를 선택 합니다. 

    - **수락**: IIS는 클라이언트에서 발급 한 인증서 허용 되지만 필요 하지 않습니다.
    - **필요한**: 클라이언트 인증서가 필요 합니다. (이 옵션을 사용 하려면 선택 해야 "SSL 필요)

ApplicationHost.config 파일에 이러한 옵션을 설정할 수도 있습니다.

[!code-xml[Main](working-with-ssl-in-web-api/samples/sample3.xml)]

**사용** 플래그 의미 IIS는 클라이언트에서 발급 한 인증서 허용 되지만 (IIS 관리자에서 "허용" 옵션에 해당 하는) 하나 필요 하지 않습니다. 인증서를 요구 하도록 설정 된 **SslRequireCert** 플래그입니다. 테스트를 위해 로컬 applicationhost에 IIS Express에서 이러한 옵션을도 설정할 수 있습니다. "Documents\IISExpress\config"에 있는 구성 파일을 제공 합니다.

### <a name="creating-a-client-certificate-for-testing"></a>테스트를 위해 클라이언트 인증서 만들기

테스트를 위해 사용할 수 있습니다 [MakeCert.exe](https://msdn.microsoft.com/library/bfsktky3.aspx) 클라이언트 인증서를 만들 수 있습니다. 먼저, 테스트 루트 기관을 만듭니다.

[!code-console[Main](working-with-ssl-in-web-api/samples/sample4.cmd)]

Makecert는 개인 키에 대 한 암호를 입력 하 라는 메시지가 됩니다.

다음으로, 다음과 같이 서버의 "신뢰할 수 있는 루트 인증 기관" 저장소 테스트에 인증서를 추가 합니다.

1. MMC를 엽니다.
2. 아래 **파일**선택, **스냅인 추가/제거**합니다.
3. 선택 **컴퓨터 계정**합니다.
4. 선택 **로컬 컴퓨터** 마법사를 완료 합니다.
5. 탐색 창에서 "신뢰할 수 있는 루트 인증 기관" 노드를 확장 합니다.
6. 에 **동작** 메뉴에서 **모든 작업**, 클릭 하 고 **가져오기** 인증서 가져오기 마법사를 시작 합니다.
7. 인증서 파일을 TempCA.cer 찾습니다.
8. 클릭 **열려**, 클릭 **다음** 마법사를 완료 합니다. (메시지가 표시 됩니다 다시 암호를 입력 합니다.)

이제 첫 번째 인증서에서 서명 된 클라이언트 인증서를 만듭니다.

[!code-console[Main](working-with-ssl-in-web-api/samples/sample5.cmd)]

### <a name="using-client-certificates-in-web-api"></a>클라이언트 인증서를 사용 하 여 Web API의

서버 쪽에서 호출 하 여 클라이언트 인증서를 가져올 수 있습니다 [GetClientCertificate](https://msdn.microsoft.com/library/system.net.http.httprequestmessageextensions.getclientcertificate.aspx) 요청 메시지에 있습니다. 메서드가 없는 클라이언트 인증서가 있는 경우 null을 반환 합니다. 그렇지 않으면 반환 된 **X509Certificate2** 인스턴스. 정보 발급자 및 주체와 같이 인증서를 가져오기 위해이 개체를 사용 합니다. 그런 다음 인증 및/또는 권한 부여에 대 한이 정보를 사용할 수 있습니다.

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample6.cs)]
