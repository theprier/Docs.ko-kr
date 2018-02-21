---
title: "IIS 모듈을 사용 하 여 ASP.NET 코어"
author: guardrex
description: "ASP.NET Core 응용 프로그램 및 IIS 모듈을 관리 하는 방법에 대 한 활성 및 비활성 IIS 모듈을 검색 합니다."
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 02/15/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/iis/modules
ms.openlocfilehash: 5032c9f07af4f9291b44538cecbc310bfabc8e02
ms.sourcegitcommit: 9f758b1550fcae88ab1eb284798a89e6320548a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/19/2018
---
# <a name="using-iis-modules-with-aspnet-core"></a>IIS 모듈을 사용 하 여 ASP.NET 코어

[Luke Latham](https://github.com/guardrex)으로

ASP.NET Core 응용 프로그램의 역방향 프록시 구성에서 IIS에서 호스팅됩니다. 네이티브 IIS 모듈의 일부와 모든 관리 되는 IIS 모듈 ASP.NET Core 응용 프로그램에 대 한 요청을 처리할 수 없습니다. 대부분의 경우 ASP.NET Core IIS 네이티브 및 관리 되는 모듈의 기능에 대 한 대안을 제공합니다.

## <a name="native-modules"></a>네이티브 모듈

| Module | .NET Core Active | ASP.NET Core 옵션 |
| ------ | :--------------: | ------------------- |
| **익명 인증**<br>`AnonymousAuthenticationModule` | 예 | |
| **기본 인증**<br>`BasicAuthenticationModule` | 예 | |
| **클라이언트 인증 매핑 인증**<br>`CertificateMappingAuthenticationModule` | 예 | |
| **CGI**<br>`CgiModule` | 아니요 | |
| **구성 유효성 검사**<br>`ConfigurationValidationModule` | 예 | |
| **HTTP 오류**<br>`CustomErrorModule` | 아니요 | [상태 코드 페이지 미들웨어입니다.](xref:fundamentals/error-handling#configuring-status-code-pages) |
| **사용자 지정 로깅**<br>`CustomLoggingModule` | 예 | |
| **기본 문서**<br>`DefaultDocumentModule` | 아니요 | [기본 파일 미들웨어입니다.](xref:fundamentals/static-files#serve-a-default-document) |
| **다이제스트 인증**<br>`DigestAuthenticationModule` | 예 | |
| **디렉터리 검색**<br>`DirectoryListingModule` | 아니요 | [디렉터리 검색 미들웨어](xref:fundamentals/static-files#enable-directory-browsing) |
| **동적 압축**<br>`DynamicCompressionModule` | 예 | [응답 압축 미들웨어](xref:performance/response-compression) |
| **추적**<br>`FailedRequestsTracingModule` | 예 | [ASP.NET Core Logging](xref:fundamentals/logging/index#the-tracesource-provider) |
| **파일 캐싱**<br>`FileCacheModule` | 아니요 | [응답 캐싱 미들웨어](xref:performance/caching/middleware) |
| **HTTP 캐싱**<br>`HttpCacheModule` | 아니요 | [응답 캐싱 미들웨어](xref:performance/caching/middleware) |
| **HTTP 로깅**<br>`HttpLoggingModule` | 예 | [ASP.NET Core Logging](xref:fundamentals/logging/index)<br>구현: [elmah.io](https://github.com/elmahio/Elmah.Io.Extensions.Logging), [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging), [NLog](https://github.com/NLog/NLog.Extensions.Logging), [Serilog](https://github.com/serilog/serilog-extensions-logging)
| **HTTP 리디렉션**<br>`HttpRedirectionModule` | 예 | [URL 재작성 미들웨어](xref:fundamentals/url-rewriting) |
| **IIS 클라이언트 인증서 매핑 인증**<br>`IISCertificateMappingAuthenticationModule` | 예 | |
| **IP 및 도메인 제한**<br>`IpRestrictionModule` | 예 | |
| **ISAPI 필터**<br>`IsapiFilterModule` | 예 | [미들웨어](xref:fundamentals/middleware/index) |
| **ISAPI**<br>`IsapiModule` | 예 | [미들웨어](xref:fundamentals/middleware/index) |
| **프로토콜 지원**<br>`ProtocolSupportModule` | 예 | |
| **요청 필터링**<br>`RequestFilteringModule` | 예 | [URL 다시 쓰기 미들웨어 `IRule`](xref:fundamentals/url-rewriting#irule-based-rule) |
| **요청 모니터**<br>`RequestMonitorModule` | 예 | |
| **URL 다시 쓰기**<br>`RewriteModule` | Yes&#8224; | [URL 재작성 미들웨어](xref:fundamentals/url-rewriting) |
| **서버 측 Include**<br>`ServerSideIncludeModule` | 아니요 | |
| **정적 압축**<br>`StaticCompressionModule` | 아니요 | [응답 압축 미들웨어](xref:performance/response-compression) |
| **정적 콘텐츠**<br>`StaticFileModule` | 아니요 | [정적 파일 미들웨어](xref:fundamentals/static-files) |
| **토큰 캐싱**<br>`TokenCacheModule` | 예 | |
| **URI 캐싱**<br>`UriCacheModule` | 예 | |
| **URL 권한 부여**<br>`UrlAuthorizationModule` | 예 | [ASP.NET Core Identity](xref:security/authentication/identity) |
| **Windows 인증**<br>`WindowsAuthenticationModule` | 예 | |

&#8224; URL 재작성 모듈의 `isFile` 및 `isDirectory` 유형과 일치 변경 때문에 ASP.NET Core 응용 프로그램을 사용 하지 않는 [디렉터리 구조](xref:host-and-deploy/directory-structure)합니다.

## <a name="managed-modules"></a>관리 되는 모듈

| Module                  | .NET Core Active | ASP.NET Core 옵션 |
| ----------------------- | :--------------: | ------------------- |
| AnonymousIdentification | 아니요               | |
| DefaultAuthentication   | 아니요               | |
| FileAuthorization       | 아니요               | |
| FormsAuthentication     | 아니요               | [쿠키 인증 미들웨어입니다.](xref:security/authentication/cookie) |
| OutputCache             | 아니요               | [응답 캐싱 미들웨어](xref:performance/caching/middleware) |
| 프로필                 | 아니요               | |
| RoleManager             | 아니요               | |
| ScriptModule-4.0        | 아니요               | |
| 세션                 | 아니요               | [세션 미들웨어](xref:fundamentals/app-state) |
| UrlAuthorization        | 아니요               | |
| UrlMappingsModule       | 아니요               | [URL 재작성 미들웨어](xref:fundamentals/url-rewriting) |
| UrlRoutingModule-4.0    | 아니요               | [ASP.NET Core Identity](xref:security/authentication/identity) |
| WindowsAuthentication   | 아니요               | |

## <a name="iis-manager-application-changes"></a>IIS 관리자 응용 프로그램 변경

IIS 관리자를 사용 하 여 설정을 구성 하는 *web.config* 앱의 파일을 변경 합니다. 응용 프로그램 배포 하는 경우 포함 하 여 *web.config*, IIS 관리자를 사용 하 여 변경한 내용은 덮어씁니다가 배포 하 여 *web.config* 파일입니다. 서버의 변경 되 면 *web.config* 파일, 업데이트 된 복사 *web.config* 즉시 로컬 프로젝트에 서버에서 파일입니다.

## <a name="disabling-iis-modules"></a>IIS 모듈을 사용 하지 않도록 설정

IIS 모듈 응용 프로그램에서는 응용 프로그램에 추가 된 항목에 대 한 사용 하지 않아야 하는 서버 수준에서 구성 된 경우 *web.config* 파일 모듈을 사용 하지 않도록 설정할 수 있습니다. 모듈 위치에 그대로 둡니다 (있는 경우)에 구성 설정을 사용 하 여 비활성화 하거나 응용 프로그램에서 모듈을 제거 합니다.

### <a name="module-deactivation"></a>모듈 비활성화

많은 모듈을 응용 프로그램에서 모듈을 제거 하지 않고 사용 하지 않도록 설정할 수 있는 구성 설정을 제공 합니다. 이것이 모듈을 비활성화 하려면 가장 간단 하 고 가장 빠른 방법입니다. 예를 들어와 IIS URL 재작성 모듈을 비활성화할 수 있습니다는  **\<httpRedirect >** 요소 *web.config*:

```xml
<configuration>
  <system.webServer>
     <httpRedirect enabled="false" />
  </system.webServer>
</configuration>
```

구성 설정 사용 하 여 모듈을 사용 하지 않도록 설정에 대 한 자세한 내용은 있는 링크는 *자식 요소* 섹션 [IIS \<system.webServer >](/iis/configuration/system.webServer/)합니다.

### <a name="module-removal"></a>모듈 제거

설정을 사용 하 여 모듈을 제거 하도록 선택 하는 경우 *web.config*모듈의 잠금을 해제 하 고 잠금 해제는  **\<모듈 >** 섹션 *web.config* 첫 번째:

1. 서버 수준에서 모듈의 잠금을 해제 합니다. IIS 관리자에서 IIS 서버를 선택 합니다. **연결** 사이드바 합니다. 열기는 **모듈** 에 **IIS** 영역입니다. 목록에서 모듈을 선택 합니다. 에 **동작** , 오른쪽에 선택 **잠금 해제**합니다. 많은 모듈을 제거할 계획을 수립할 때 잠금을 해제 *web.config* 나중입니다.

1. 없이 앱을 배포는  **\<모듈 >** 섹션 *web.config*합니다. 응용 프로그램으로 배포 하는 경우는 *web.config* 포함 하는  **\<모듈 >** 섹션에 있는 섹션 잠금을 해제는 먼저 IIS 관리자에서 Configuration Manager 예외를 throw 합니다. 섹션 잠금 해제 하는 동안 합니다. 따라서 없이 앱을 배포는  **\<모듈 >** 섹션.

1. 잠금 해제는  **\<모듈 >** 섹션 *web.config*합니다. 에 **연결** 사이드바에서 웹 사이트를 선택 **사이트**합니다. 에 **관리** 영역을 열고는 **구성 편집기**합니다. 탐색 컨트롤을 사용 하 여 선택 된 `system.webServer/modules` 섹션. 에 **동작** 하려면, 오른쪽에 선택 **잠금 해제** 섹션입니다.

1. 이 시점에서  **\<모듈 >** 섹션에 추가할 수는 *web.config* 파일는  **\<제거 >** 요소에서 모듈을 제거 하려면 응용 프로그램입니다. 여러  **\<제거 >** 여러 모듈을 제거 하는 요소를 추가할 수 있습니다. 경우 *web.config* 서버에서 정의가 변경 되어도, 해당 프로젝트의 동일 하 게 변경 즉시 *web.config* 파일을 로컬입니다. 이러한 방식으로 모듈을 제거 하면 서버에서 다른 앱을 사용 하 여 모듈의 사용을 적용 되지 않습니다.

  ```xml
  <configuration> 
    <system.webServer> 
      <modules> 
        <remove name="MODULE_NAME" /> 
      </modules> 
    </system.webServer> 
  </configuration>
  ```

설치 된 기본 모듈로 IIS 설치의 경우 다음을 사용 하 여  **\<모듈 >** 기본 모듈을 제거 하려면 섹션.

```xml
<modules>
  <remove name="CustomErrorModule" />
  <remove name="DefaultDocumentModule" />
  <remove name="DirectoryListingModule" />
  <remove name="HttpCacheModule" />
  <remove name="HttpLoggingModule" />
  <remove name="ProtocolSupportModule" />
  <remove name="RequestFilteringModule" />
  <remove name="StaticCompressionModule" /> 
  <remove name="StaticFileModule" /> 
</modules>
```

와 IIS 모듈을 제거할 수도 있습니다 *Appcmd.exe*합니다. 제공 된 `MODULE_NAME` 및 `APPLICATION_NAME` 명령에:

```console
Appcmd.exe delete module MODULE_NAME /app.name:APPLICATION_NAME
```

예를 들어 제거는 `DynamicCompressionModule` 기본 웹 사이트에서:

```console
%windir%\system32\inetsrv\appcmd.exe delete module DynamicCompressionModule /app.name:"Default Web Site"
```

## <a name="minimum-module-configuration"></a>최소 모듈 구성

ASP.NET Core 응용 프로그램을 실행 하는 데 필요한 유일한 모듈은 익명 인증 모듈 및 ASP.NET Core 모듈입니다.

![표시 된 최소 모듈 구성을 사용 하 여 모듈에 IIS 관리자를 열려면](modules/_static/modules.png)

## <a name="additional-resources"></a>추가 리소스

* [IIS를 사용하여 Windows에서 호스트](xref:host-and-deploy/iis/index)
* [IIS 모듈 개요](https://docs.microsoft.com/iis/get-started/introduction-to-iis/iis-modules-overview)
* [IIS 7.0 역할 및 모듈을 사용자 지정](https://technet.microsoft.com/library/cc627313.aspx)
* [IIS `<system.webServer>`](https://docs.microsoft.com/iis/configuration/system.webServer/)
