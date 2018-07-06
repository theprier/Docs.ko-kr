---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/the-contact-manager-solution
title: Contact Manager 솔루션 | Microsoft Docs
author: jrjlee
description: 이 자습서 시리즈에서는 샘플 솔루션을 사용 하 여&#x2014;Contact Manager 솔루션&#x2014;현실적인 수준을 사용 하 여 엔터프라이즈급 응용 프로그램을 나타내는...
ms.author: aspnetcontent
ms.date: 05/04/2012
ms.assetid: 4d8c8d19-055b-4b70-9ee1-f748f0db3a01
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/the-contact-manager-solution
msc.type: authoredcontent
ms.openlocfilehash: c8044c37738e9d23ca83648a6b571059338dc1a3
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37835161"
---
<a name="the-contact-manager-solution"></a>Contact Manager 솔루션
====================
[Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 [시리즈의 자습서](web-deployment-in-the-enterprise.md) 샘플 솔루션을 사용 하 여&#x2014;Contact Manager 솔루션&#x2014;현실적인 수준의 복잡성을 사용 하 여 엔터프라이즈급 응용 프로그램을 나타내는입니다. 이 항목에서는 Contact Manager 솔루션을 소개 하 고, 솔루션의 주요 구성 요소에 설명,이 종류의 엔터프라이즈 환경에서 다양 한 대상 플랫폼에 응용 프로그램 배포 문제를 식별 합니다.
> 
> 이 자습서에서 항목을 통해 작업 하는 동안에 엔터프라이즈 배포 시나리오에서 특정 과제를 충족 하는 방법을 보여 주는 참조 구현으로 Contact Manager 솔루션을 사용할 수 있습니다. 다음 항목인 [the Contact Manager 솔루션 설정](setting-up-the-contact-manager-solution.md)를 다운로드 하 고 개발자 워크스테이션에서 솔루션을 실행 하는 방법을 설명 합니다.


## <a name="solution-overview"></a>솔루션 개요

Contact Manager 솔루션 4 개의 개별 프로젝트가 이루어져 있습니다.

![](the-contact-manager-solution/_static/image1.png)

- **ContactManager.Mvc**. 솔루션에 대 한 진입점을 나타내는 ASP.NET MVC 3 웹 응용 프로그램 프로젝트입니다. 생성 및 연락처 세부 정보를 확인 하는 기능을 사용 하 여 사용자를 제공 하는 등 몇 가지 기본 웹 응용 프로그램 기능을 제공 합니다. 응용 프로그램은 연락처 및 인증 및 권한 부여를 관리 하는 ASP.NET 응용 프로그램 서비스 데이터베이스를 관리 하는 Windows Communication Foundation (WCF) 서비스입니다.
- **ContactManager.Database**. Visual Studio 데이터베이스 프로젝트입니다. 프로젝트는 저장소 연락처 세부 정보는 데이터베이스에 대 한 스키마를 정의 합니다.
- **ContactManager.Service**. WCF 웹 서비스 프로젝트입니다. 검색, 업데이트 및 삭제 (CRUD) 작업에서 수행 하는 호출자를 허용 하는 끝점을 만들려면 WCF 서비스 노출 합니다 **ContactManager** 데이터베이스입니다. 서비스에 의존 합니다 **ContactManager** 데이터베이스 및 **ContactManager.Common.dll** 어셈블리입니다.
- **ContactManager.Common**. 클래스 라이브러리 프로젝트입니다. WCF 서비스는이 어셈블리에 정의 된 형식을 사용 합니다.

솔루션에는 게시를 폴더가 솔루션도 포함 됩니다. 다양 한 사용자 지정 프로젝트 파일 및 제어 하 고 빌드 및 배포 프로세스를 조작할 수는 방법을 보여 주는 명령 파일을 포함 합니다. 이러한이 자습서의 뒷부분에서 자세히 설명 됩니다.

개념 수준에서 솔루션의 구성 요소 처럼 잘 맞습니다이:

![](the-contact-manager-solution/_static/image2.png)

> [!NOTE]
> ASP.NET 멤버 자격 공급자를 사용 하는 ASP.NET MVC 3 웹 응용 프로그램을 웹 응용 프로그램 내의 모든 페이지는 익명 액세스를 허용 합니다. 이 명확 하 게 실제 구성이 아닙니다. 그러나 솔루션을 쉽게 배포 및 사용자 계정 및 역할을 구성 하지 않고 솔루션을 테스트할 수 있도록이 방식으로 설정 됩니다.


## <a name="deployment-challenges"></a>배포 과제

Contact Manager 솔루션은 많은 엔터프라이즈 배포 시나리오에 공통 되는 여러 가지 배포 문제를 보여 줍니다.

- 여러 종속 프로젝트가 솔루션 구성 됩니다. 이러한 프로젝트를 동시에 배포 해야 합니다.
- 연결 문자열 및 서비스 끝점을 각 환경에 대 한 업데이트 해야 하 고는 대부분의 경우가이 정보를 사용할 수 없습니다 개발자에 게 키를 누릅니다.
- 배포 하는 경우는 **ContactManager** 데이터베이스 스테이징 및 프로덕션 환경에 후속 배포에서 기존 데이터를 유지 해야 합니다.
- ASP.NET 응용 프로그램 서비스 데이터베이스를 배포할 때 일부 구성 데이터를 배포 하지만 모든 사용자 계정 데이터를 생략 해야 합니다.
- 일부 파일 및 배포 해야 하는 폴더를 프로젝트에 포함 됩니다. 배포 프로세스에서 이러한 파일 및 폴더를 제외 해야 합니다.
- 솔루션은 Team Foundation Server (TFS) 빌드 서버에서 자동화 된 배포를 지원 해야 합니다.

## <a name="conclusion"></a>결론

이 항목에서는 Contact Manager 솔루션의 대략적인 개요를 제공 하 고 일부의 다양 한 엔터프라이즈 배포 시나리오에 공통 되는 고유한 배포 문제를 식별 합니다. 이 자습서의 나머지 항목에서는 이러한 과제를 충족 하 여 기술 중 일부를 설명 합니다.

다음 항목인 [the Contact Manager 솔루션 설정](setting-up-the-contact-manager-solution.md)를 다운로드 하 고 개발자 워크스테이션에서 솔루션을 실행 하는 방법을 설명 합니다.

> [!div class="step-by-step"]
> [이전](web-deployment-in-the-enterprise.md)
> [다음](setting-up-the-contact-manager-solution.md)
