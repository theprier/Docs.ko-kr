---
title: "ASP.NET Core 자습서"
author: rick-anderson
description: "ASP.NET Core 응용 프로그램을 개발하는 방법을 배우기 위한 단계별 가이드 목록입니다."
manager: wpickett
ms.author: riande
ms.date: 10/14/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: tutorials/index
ms.openlocfilehash: 45b00fbc15740fad60202bb7e5ab14beb9ebe495
ms.sourcegitcommit: 9622bdc6326c28c3322c70000468a80ef21ad376
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/12/2018
---
# <a name="aspnet-core-tutorials"></a>ASP.NET Core 자습서

ASP.NET Core 응용 프로그램을 개발하기 위해 다음 단계별 가이드를 사용할 수 있습니다.

## <a name="build-web-apps"></a>웹 앱 개발

[Razor 페이지](xref:mvc/razor-pages/index)는 ASP.NET Core 2.0을 사용하여 새로운 웹 UI 앱을 만드는 좋은 방법입니다.

* [ASP.NET Core의 Razor 페이지 소개](xref:mvc/razor-pages/index)
* ASP.NET Core를 사용하여 Razor 페이지 웹앱 만들기

   * [Windows의 Razor 페이지](xref:tutorials/razor-pages/index)
   * [Mac의 Razor 페이지](xref:tutorials/razor-pages-mac/index)
   * [VS Code를 사용하는 Razor 페이지](xref:tutorials/razor-pages-vsc/index)  

* ASP.NET Core MVC 웹앱 만들기

   * [Windows용 Visual Studio를 사용하는 웹앱](first-mvc-app/index.md)
   * [Mac용 Visual Studio를 사용하는 웹앱](first-mvc-app-mac/index.md)
   * [Mac 또는 Linux에서 Visual Studio Code를 사용하는 웹앱](first-mvc-app-xplat/index.md)

* [Visual Studio를 사용하여 ASP.NET Core 및 Entity Framework Core 시작](../data/ef-mvc/index.md)
* [태그 도우미 만들기](../mvc/views/tag-helpers/authoring.md)
* [간단한 뷰 구성 요소 만들기](../mvc/views/view-components.md#walkthrough-creating-a-simple-view-component)
* [dotnet watch를 사용하여 ASP.NET Core 앱 개발](dotnet-watch.md)

## <a name="build-web-apis"></a>웹 API 개발
* ASP.NET Core를 사용하여 Web API 만들기

  * [Windows용 Visual Studio를 사용하는 Web API](first-web-api.md)
  * [Mac용 Visual Studio를 사용하는 Web API](xref:tutorials/first-web-api-mac)
  * [Visual Studio Code를 사용하는 Web API](web-api-vsc.md)

* [Swagger를 사용한 ASP.NET Core Web API 도움말 페이지](xref:tutorials/web-api-help-pages-using-swagger)
  * [NSwag 시작](xref:tutorials/get-started-with-nswag)
  * [Swashbuckle 시작](xref:tutorials/get-started-with-swashbuckle)

* [네이티브 모바일 앱에 대한 백 엔드 웹 서비스 만들기](../mobile/native-mobile-backend.md)

## <a name="data-access-and-storage"></a>데이터 액세스 및 저장소
* [Visual Studio를 사용하여 Razor 페이지 및 EF Core 시작](xref:data/ef-rp/intro)
* [Visual Studio를 사용하여 ASP.NET Core MVC 및 Entity Core 시작](../data/ef-mvc/index.md)
* [ASP.NET Core MVC 및 EF Core - 새 데이터베이스](https://docs.microsoft.com/ef/core/get-started/aspnetcore/new-db)
* [ASP.NET Core MVC 및 EF Core - 기존 데이터베이스](https://docs.microsoft.com/ef/core/get-started/aspnetcore/existing-db)

## <a name="authentication-and-authorization"></a>인증 및 권한 부여
* [Facebook, Google 및 기타 외부 공급자를 통해 인증 사용](../security/authentication/social/index.md)
* [계정 확인 및 암호 복구](../security/authentication/accconfirm.md)
* [SMS를 사용한 2단계 인증](../security/authentication/2fa.md)

## <a name="client-side-development"></a>클라이언트 쪽 개발
* [Gulp 사용](../client-side/using-gulp.md)
* [Grunt 사용](../client-side/using-grunt.md)
* [Bower를 사용하여 클라이언트 쪽 패키지 관리](../client-side/bower.md)
* [부트스트랩을 사용하여 반응이 빠른 사이트 빌드](../client-side/bootstrap.md)

## <a name="test"></a>테스트
* [Dotnet 테스트를 사용한 .NET Core의 유닛 테스트](https://docs.microsoft.com/dotnet/articles/core/testing/unit-testing-with-dotnet-test)

## <a name="publish-and-deploy"></a>게시 및 배포
* [Visual Studio를 사용하여 Azure에 ASP.NET Core 웹앱 배포](publish-to-azure-webapp-using-vs.md)
* [명령줄을 사용하여 Azure에 ASP.NET Core 웹앱 배포](publish-to-azure-webapp-using-cli.md)
* [연속 배포를 사용하여 Azure 웹앱에 게시](xref:host-and-deploy/azure-apps/azure-continuous-deployment)
* [원격 Docker 호스트에 ASP.NET 컨테이너 배포](https://docs.microsoft.com/azure/vs-azure-tools-docker-hosting-web-apps-in-docker)
* [Nano Server의 ASP.NET Core](nano-server.md)
* [ASP.NET Core 및 Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-add-a-web-frontend)

<a name="download"></a> 
## <a name="how-to-download-a-sample"></a>샘플 다운로드 방법
1. [ASP.NET 리포지토리 zip 파일을 다운로드합니다](https://codeload.github.com/aspnet/Docs/zip/master).
1. *Docs-master.zip* 파일의 압축을 풉니다.
1. 샘플 링크의 URL을 사용하여 샘플 디렉터리로 이동할 수 있습니다. 
