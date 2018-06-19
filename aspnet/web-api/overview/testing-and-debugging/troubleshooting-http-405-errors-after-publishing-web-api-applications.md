---
uid: web-api/overview/testing-and-debugging/troubleshooting-http-405-errors-after-publishing-web-api-applications
title: HTTP 문제 해결 405 오류 게시 후 Web API 2 응용 프로그램 | Microsoft Docs
author: rmcmurray
description: 이 자습서에는 프로덕션 웹 서버에는 Web API 응용 프로그램을 게시 한 후 HTTP 405 오류를 해결 하는 방법을 설명 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/01/2014
ms.topic: article
ms.assetid: 07ec7d37-023f-43ea-b471-60b08ce338f7
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/testing-and-debugging/troubleshooting-http-405-errors-after-publishing-web-api-applications
msc.type: authoredcontent
ms.openlocfilehash: b87ae7420e1295030e90c30e97b1e331413ce263
ms.sourcegitcommit: f1436107b4c022b26f5235dddef103cec5aa6bff
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/15/2017
ms.locfileid: "26743275"
---
<a name="troubleshooting-http-405-errors-after-publishing-web-api-2-applications"></a>HTTP 문제 해결 405 오류 게시 후 Web API 2 응용 프로그램
====================
으로 [Robert McMurray](https://github.com/rmcmurray)

> 이 자습서에는 프로덕션 웹 서버에는 Web API 응용 프로그램을 게시 한 후 HTTP 405 오류를 해결 하는 방법을 설명 합니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - [인터넷 정보 서비스 (IIS)](https://www.iis.net/) (버전 7 이상)
> - [Web API](../../index.md) (버전 1 또는 2)


Web API 응용 프로그램은 일반적으로 몇 가지 일반적인 HTTP 동사 사용: GET, POST, PUT, DELETE, 하며 때때로 패치 합니다. 개발자가 이러한 동사는 Visual Studio 또는 개발 서버에서 제대로 작동 하는 Web API 컨트롤러를 반환 하는 상황에는 프로덕션 서버에 다른 IIS 모듈에 의해를 구현 하는 경우에 실행할 수 있습니다는 프로그램 HTTP 405 프로덕션 서버에 배포 될 때 오류가 발생 합니다. 다행히이 문제를 쉽게 해결 되지만 해상도 문제가 발생 하는 이유와 설명은 수행 되도록 합니다.

## <a name="what-causes-http-405-errors"></a>어떤 원인을 HTTP 405 오류

HTTP 405 오류 문제 하는 방법을 배우 위한 첫 번째 단계에서 HTTP 405 오류 실제로 의미를 이해 하는 것입니다. HTTP에 대 한 문서 주 제어 [RFC 2616](http://www.ietf.org/rfc/rfc2616.txt), HTTP 405 상태 코드를 정의 하는 ***메서드가 허용 되지 않습니다***, 상황으로이 상태 코드에 자세히 설명 하 고 여기서 &quot;메서드 에 지정 된 요청 줄 요청 URI로 식별 되는 리소스에 허용 되지 않습니다.&quot; 즉, HTTP 동사 HTTP 클라이언트 요청에 있는 특정 URL에 대 한 허용 되지 않습니다.

간단 하 게 검토,으로 다음은 일부의 가장 사용 되는 HTTP 메서드 RFC 2616, RFC 4918 및 RFC 5789에 정의 된 대로:

| HTTP 메서드 | 설명 |
| --- | --- |
| **가져오기** | 이 메서드는 데이터를 검색 하는 URI에서 아마도 가장 사용 되는 HTTP 메서드가 사용 됩니다. |
| **H E A D** | 이 메서드는 것과 마찬가지로 GET 메서드 요청 URI에서에서 실제로 데이터를 검색 하지 않는 것-단순히 HTTP 상태를 검색 한다는 점이 다릅니다. |
| **올리기** | 이 메서드는; URI를 새 데이터를 보내는 데 일반적으로 POST 양식 데이터 전송에 주로 사용 됩니다. |
| **PUT** | 이 메서드는; URI를 원시 데이터를 보내는 데 일반적으로 Web API 응용 프로그램에 JSON 또는 XML 데이터를 제출 하려면 PUT 자주 사용 됩니다. |
| **삭제** | 이 메서드는 데이터를 제거 하는 URI에서 사용 됩니다. |
| **옵션** | 이 메서드는 일반적으로 URI에 지원 되는 HTTP 메서드 목록을 가져오는 데 사용 됩니다. |
| **복사 이동** | 그 목적은 자체 설명 및이 두 방법을 WebDAV로 사용 됩니다. |
| **MKCOL** | WebDAV에이 메서드를 사용 하 고 지정된 된 URI에 컬렉션 (예: 디렉터리)를 만드는 데 사용 됩니다. |
| **PROPFIND PROPPATCH** | WebDAV와 이러한 두 메서드가 사용 됩니다 하 고 쿼리하거나 URI에 대 한 속성을 설정 하는 데 사용 됩니다. |
| **잠금 잠금 해제** | 만들 때 요청 URI에 의해 식별 되는 리소스 잠금/잠금 해제를 사용 하는 이러한 두 가지 방법 WebDAV를 함께 사용 됩니다. |
| **패치** | 이 메서드는 기존 HTTP 리소스를 수정 하려면 사용 됩니다. |

서버에서 사용 하기 위해 구성 된 이러한 HTTP 메서드 중 하나를 경우 서버는 HTTP 상태 및 기타 데이터를 요청에 대 한 적합 한에 응답 합니다. (예를 들어 GET 메서드는 HTTP 200 받게 ***확인*** 응답 및 PUT 메서드 HTTP 201 나타날 수 ***Created*** 응답 합니다.)

HTTP 메서드는 서버에서 사용 하기 위해 구성 되지 않은 경우 서버는 HTTP 501으로 응답 ***구현 되지*** 오류입니다.

그러나 HTTP 메서드는 서버에서 사용 하기 위해 구성 된 경우 지정된 된 URI에 대 한 비활성화 된 경우 서버는 응답으로 HTTP 405 ***메서드가 허용 되지 않습니다*** 오류입니다.

## <a name="example-http-405-error"></a>예제에서는 HTTP 405 오류

다음 예제에서는 HTTP 요청 및 응답에이 경우를 HTTP 클라이언트가 웹 서버에서 Web API 응용 프로그램에 값을 입력 하려고 합니다. PUT 메서드를 하지 않은 상태에서 사용할 수 있는 HTTP 오류를 반환 하는 서버를 보여 줍니다.


HTTP 요청:


[!code-console[Main](troubleshooting-http-405-errors-after-publishing-web-api-applications/samples/sample1.cmd)]


HTTP 응답:


[!code-console[Main](troubleshooting-http-405-errors-after-publishing-web-api-applications/samples/sample2.cmd)]


이 예제에서는 HTTP 클라이언트는 유효한 JSON 요청 웹 서버에서 Web API 응용 프로그램에 대 한 URL을 보냈지만 서버 URL에 대해 PUT 메서드를 사용할 수 없습니다 되었음을 나타내는 HTTP 405 오류 메시지를 반환 했습니다. 반면, 요청 URI는 Web API 응용 프로그램에 대 한 경로 일치 하지 않은 서버 반환에서 HTTP 404 ***찾지*** 오류입니다.

## <a name="resolving-http-405-errors"></a>해결 HTTP 405 오류

왜 특정 HTTP 동사는 허용 되지 않을 수 있습니다 하지만 IIS에서이 오류의 주요 원인입니다. 한 가지 주요 시나리오는 다음과 같은 경우: 여러 처리기 동일한 동사/방법에 대해 정의 되 고 처리기 중 하나에서 예상된 처리기 차단 요청을 처리 합니다. 통해 IIS 마지막 순서 처리기 항목 경로, 동사, 리소스 등의 일치 하는 첫 번째 조합을 사용 하는 요청을 처리 하는 여기서 \t<li>applicationhost.config 및 web.config 파일에 기반 하 여 첫 번째 범위에서 처리기를 처리 합니다.

다음 예제에서는 PUT 메서드를 사용 하 여 Web API 응용 프로그램에 데이터를 전송 하는 경우에서 HTTP 405 오류를 반환 했습니다는 IIS 서버에 대 한 applicationHost.config 파일 발췌 구문입니다. 발췌 한이 몇 가지 HTTP 처리기를 정의 하 고 각 처리기에 HTTP 메서드를 구성 집합이 다른-목록의 마지막 항목은 다른 처리기는 chanc 전에 사용 되는 기본 처리기는 정적 콘텐츠 처리기 요청을 검사 하려면 e:

[!code-xml[Main](troubleshooting-http-405-errors-after-publishing-web-api-applications/samples/sample3.xml)]

위의 예에서 WebDAV 처리기 및 해당 확장명이 없는 URL 이벤트 처리기 (하는 ASP.NET Web API 사용 됨)에 대 한 HTTP 메서드의 별도 목록에 대 한 정의 명확 하 게 됩니다. 이 구성이 반드시 인해 않지만 오류가 ISAPI DLL 처리기 모든 HTTP 메서드에 대해 구성 되어 있는지 확인 합니다. 그러나 HTTP 405 오류 문제 해결 시 고려해 야 할이 이와 같은 구성 설정입니다.

위의 예에서 ISAPI DLL 처리기 문제가 아닙니다. 실제로 문제가 IIS 서버에 대 한 applicationHost.config 파일에 정의 되지 않았습니다-Visual Studio에서 Web API 응용 프로그램을 만들 때 web.config 파일에 작성 된 항목에 의해 문제가 발생 했습니다. 응용 프로그램의 web.config 파일에서 다음 발췌 구문 문제가의 위치를 보여 줍니다.

[!code-xml[Main](troubleshooting-http-405-errors-after-publishing-web-api-applications/samples/sample4.xml)]

이 인용문에서 ASP.NET에 대 한 확장명 없는 URL 처리기 Web API 응용 프로그램과 함께 사용할 수 있는 추가 HTTP 메서드를 포함 하도록 다시 정의 됩니다. 그러나 HTTP 메서드 집합을 유사한 WebDAV 처리기에 대 한 정의 때문에 충돌이 발생 합니다. 이 특정 한 경우 WebDAV 처리기가 정의 되 고 Web API 응용 프로그램을 포함 하는 웹 사이트에 대 한 WebDAV가 사용 하지 않도록 설정 하는 경우에 IIS에 의해 로드 됩니다. HTTP PUT 요청을 처리 하는 동안 PUT 동사에 대해 정의 된 이후 IIS WebDAV 모듈을 호출 합니다. 해당 구성을 확인 하 고는 HTTP 405를 반환 하므로 비활성 상태임을 확인 WebDAV 모듈 호출 될 때 ***메서드가 허용 되지 않습니다*** 유사한 WebDAV 요청 하는 모든 요청에 대 한 오류입니다. 이 문제를 해결 하려면 WebDAV 웹 API 응용 프로그램이 정의 되어 있는 웹 사이트에 대 한 HTTP 모듈 목록에서 제거 해야 합니다. 다음 예제는 모양 좋아할 만한 기능 보여줍니다.

[!code-xml[Main](troubleshooting-http-405-errors-after-publishing-web-api-applications/samples/sample5.xml)]

이 시나리오는 응용 프로그램 개발 환경에서 프로덕션 환경에 게시 하 고이 목록에 모듈 처리기/개발 및 프로덕션 환경 간에 차이가 있는 때문에 발생 한 후에 종종 발생 합니다. 예를 들어 Visual Studio 2012 또는 2013을 사용 하는 Web API 응용 프로그램을 개발 하는, 하는 경우 IIS Express 8은 테스트에 대 한 기본 웹 서버. 이 개발 웹 서버는 서버 제품에서 제공 되는 모든 IIS 기능 축소 버전 및이 개발 웹 서버에는 개발 시나리오에 대해 추가 된 몇 가지 변경 내용이 포함 되어 있습니다. 예를 들어 실제 사용에서 되지 않지만 WebDAV 모듈은 종종 정식 버전의 IIS 실행 하는 프로덕션 웹 서버에 설치 됩니다. 개발 버전 (IIS Express) IIS의 WebDAV 모듈을 설치 하지만 WebDAV 모듈에 대 한 항목은 의도적으로 주석 처리 하므로 IIS Express 구성에 특별히 변경 하지 않는 경우 IIS Express에서 WebDAV 모듈이 로드 되지 않았습니다. WebDAV 기능을 IIS Express 설치에 추가 하는 설정입니다. 결과적으로, 웹 응용 프로그램 개발 컴퓨터에 제대로 작동 될 수 있습니다 하지만 프로덕션 웹 서버에 Web API 응용 프로그램을 게시 하면 HTTP 405 오류가 발생할 수 있습니다.

## <a name="summary"></a>요약

HTTP 405 오류는 요청 된 URL에 대 한 HTTP 메서드는 웹 서버에서 허용 하지 않는 경우에 발생 합니다. 특정 처리기 특정 동사에 대해 정의 되 고 해당 처리기가 요청을 처리할 수 있어야 하는 처리기를 재정의 하는 경우에 자주이 상태가 표시 됩니다.

구체적인 기능은 서버에 구현 되지 않은 것을 의미 하는 HTTP 501 오류 메시지가 나타나는 상황이 발생 하면이 종종 있다는 것을 의미 HTTP 요청에 일치 하는 IIS 설정에 정의 된 처리기를 아마도 문제가 올바르게 시스템에 설치 되지 않았습니다 또는 않도록 하는 특정 HTTP 지 원하는 메서드를 정의 하는 처리기가 없는 IIS 설정을 변경 했습니다 것을 나타냅니다. 이 문제를 해결 하려면 맺은 없는 해당 모듈 또는 처리기 정의 하는 HTTP 메서드를 사용 하려고 시도 하는 모든 응용 프로그램을 다시 설치 해야 합니다.
