---
title: ASP.NET Core 자습서
author: rick-anderson
description: ASP.NET Core 응용 프로그램을 개발하는 방법을 배우기 위한 단계별 가이드 목록입니다.
ms.author: riande
ms.date: 10/14/2017
uid: tutorials/index
ms.openlocfilehash: 3d2fbb453c8f6510806d8dc263ea344023aa4cda
ms.sourcegitcommit: 32f5ee0690604d451f61e9a5c28881c9fcf85738
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/29/2018
ms.locfileid: "47454793"
---
# <a name="aspnet-core-tutorials"></a>ASP.NET Core 자습서

ASP.NET Core 응용 프로그램을 개발하기 위해 다음 단계별 가이드를 사용할 수 있습니다.

## <a name="build-web-apps"></a>웹 앱 개발

[Razor 페이지](xref:razor-pages/index)는 ASP.NET Core 2.0을 사용하여 새로운 웹 UI 앱을 만드는 좋은 방법입니다.

* [ASP.NET Core의 Razor 페이지 소개](xref:razor-pages/index)
* ASP.NET Core를 사용하여 Razor 페이지 웹앱 만들기

   * [Windows의 Razor 페이지](xref:tutorials/razor-pages/index)
   * [macOS의 Razor 페이지](xref:tutorials/razor-pages-mac/index)
   * [VS Code를 사용하는 Razor 페이지](xref:tutorials/razor-pages-vsc/index)  

* [실시간 SignalR 웹앱 만들기](xref:tutorials/signalr)
* [TypeScript를 사용하여 SignalR 웹앱 만들기](xref:tutorials/signalr-typescript-webpack)

* ASP.NET Core MVC 웹앱 만들기

   * [Windows용 Visual Studio를 사용하는 웹앱](xref:tutorials/first-mvc-app/index)
   * [Mac용 Visual Studio를 사용하는 웹앱](xref:tutorials/first-mvc-app-mac/index)
   * [macOS 또는 Linux에서 Visual Studio Code를 사용하는 웹앱](xref:tutorials/first-mvc-app-xplat/index)

* [Visual Studio를 사용하여 ASP.NET Core 및 Entity Framework Core 시작](xref:data/ef-mvc/index)
* [태그 도우미 만들기](xref:mvc/views/tag-helpers/authoring)
* [간단한 뷰 구성 요소 만들기](xref:mvc/views/view-components#walkthrough-creating-a-simple-view-component)
* [파일 감시자를 사용하여 앱 개발](xref:tutorials/dotnet-watch)

## <a name="build-web-apis"></a>웹 API 개발

* ASP.NET Core를 사용하여 Web API 만들기

  * [Windows용 Visual Studio를 사용하는 Web API](xref:tutorials/first-web-api)
  * [Mac용 Visual Studio를 사용하는 Web API](xref:tutorials/first-web-api-mac)
  * [Visual Studio Code를 사용하는 Web API](xref:tutorials/web-api-vsc)

* [Swagger를 사용한 ASP.NET Core Web API 도움말 페이지](xref:tutorials/web-api-help-pages-using-swagger)
  * [NSwag 시작](xref:tutorials/get-started-with-nswag)
  * [Swashbuckle 시작](xref:tutorials/get-started-with-swashbuckle)

* [네이티브 모바일 앱에 대한 백 엔드 웹 서비스 만들기](xref:mobile/native-mobile-backend)

## <a name="data-access-and-storage"></a>데이터 액세스 및 저장소

* [Visual Studio를 사용하여 Razor 페이지 및 EF Core 시작](xref:data/ef-rp/intro)
* [Visual Studio를 사용하여 ASP.NET Core MVC 및 Entity Core 시작](xref:data/ef-mvc/index)
* [ASP.NET Core MVC 및 EF Core - 새 데이터베이스](/ef/core/get-started/aspnetcore/new-db)
* [ASP.NET Core MVC 및 EF Core - 기존 데이터베이스](/ef/core/get-started/aspnetcore/existing-db)

## <a name="authentication-and-authorization"></a>인증 및 권한 부여

* [Facebook, Google 및 기타 외부 공급자를 통해 인증 사용](xref:security/authentication/social/index)
* [계정 확인 및 암호 복구](xref:security/authentication/accconfirm)
* [SMS를 사용한 2단계 인증](xref:security/authentication/2fa)

## <a name="client-side-development"></a>클라이언트 쪽 개발

* [Gulp 사용](xref:client-side/using-gulp)
* [Grunt 사용](xref:client-side/using-grunt)
* [Bower를 사용하여 클라이언트 쪽 패키지 관리](xref:client-side/bower)
* [부트스트랩을 사용하여 반응이 빠른 사이트 빌드](xref:client-side/bootstrap)

## <a name="test"></a>테스트

* [Dotnet 테스트를 사용한 .NET Core의 유닛 테스트](/dotnet/articles/core/testing/unit-testing-with-dotnet-test)

## <a name="host-and-deploy"></a>호스트 및 배포

* [Visual Studio를 사용하여 Azure에 ASP.NET Core 웹앱 배포](xref:tutorials/publish-to-azure-webapp-using-vs)
* [명령줄을 사용하여 Azure에 ASP.NET Core 웹앱 배포](/azure/app-service/app-service-web-get-started-dotnet)
* [연속 배포를 사용하여 Azure 웹앱에 게시](xref:host-and-deploy/azure-apps/azure-continuous-deployment)
* [원격 Docker 호스트에 ASP.NET 컨테이너 배포](/azure/vs-azure-tools-docker-hosting-web-apps-in-docker)
* [ASP.NET Core 및 Azure Service Fabric](/azure/service-fabric/service-fabric-add-a-web-frontend)

<a name="download"></a>
## <a name="how-to-download-a-sample"></a>샘플 다운로드 방법

1. [ASP.NET 리포지토리 zip 파일을 다운로드합니다](https://codeload.github.com/aspnet/Docs/zip/master).
1. *Docs-master.zip* 파일의 압축을 풉니다.
1. 샘플 링크의 URL을 사용하여 샘플 디렉터리로 이동할 수 있습니다.
