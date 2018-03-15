---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/the-contact-manager-solution
title: "Contact Manager 솔루션 | Microsoft Docs"
author: jrjlee
description: "이 일련의 자습서는 샘플 솔루션 & #x 2014;는 Contact Manager 솔루션 & #x 2014; 현실적인 수준으로 엔터프라이즈 규모 응용 프로그램을 나타내는 데 사용 하 여..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 4d8c8d19-055b-4b70-9ee1-f748f0db3a01
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/the-contact-manager-solution
msc.type: authoredcontent
ms.openlocfilehash: b7f691a1ee855788f6a57616aea35d960e4c85c7
ms.sourcegitcommit: 493a215355576cfa481773365de021bcf04bb9c7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
<a name="the-contact-manager-solution"></a>Contact Manager 솔루션
====================
으로 [Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 [일련의 자습서](web-deployment-in-the-enterprise.md) 샘플 솔루션 & #x 2014;는 Contact Manager 솔루션 & #x 2014; 현실적인 수준의 복잡성으로 엔터프라이즈 규모 응용 프로그램을 나타내는 데 사용 합니다. 이 항목 Contact Manager 솔루션을 소개 하 고, 솔루션의 주요 구성 요소에 설명, 이러한 종류의 엔터프라이즈 환경에서 다양 한 대상 플랫폼에 응용 프로그램 배포에서 문제를 식별 합니다.
> 
> 이 자습서에는 항목을 진행할 때는 특정 한 엔터프라이즈 배포 시나리오 요구를 충족할 수 있는 방법을 보여 주는 참조 구현으로 Contact Manager 솔루션을 사용할 수 있습니다. 다음 항목인 [the Contact Manager 솔루션 설정](setting-up-the-contact-manager-solution.md)를 다운로드 하 고 개발자 워크스테이션에서 솔루션을 실행 하는 방법을 설명 합니다.


## <a name="solution-overview"></a>솔루션 개요

Contact Manager 솔루션 4 개의 개별 프로젝트가 이루어져 있습니다.

![](the-contact-manager-solution/_static/image1.png)

- **ContactManager.Mvc**. 이 ASP.NET MVC 3 웹 응용 프로그램 프로젝트를 솔루션에 대 한 진입점을 나타냅니다. 만들고 연락처 세부 정보를 볼 수 있는 사용자가 제공 하는 등 몇 가지 기본 웹 응용 프로그램 기능을 제공 합니다. 응용 프로그램 연락처와 인증 및 권한 부여를 관리 하는 ASP.NET 응용 프로그램 서비스 데이터베이스를 관리 하려면 Windows Communication Foundation (WCF) 서비스를 사용 합니다.
- **ContactManager.Database**. 이것이 Visual Studio 데이터베이스 프로젝트입니다. 프로젝트는 저장소 연락처 세부 정보는 데이터베이스에 대 한 스키마를 정의 합니다.
- **ContactManager.Service**. 이 WCF 웹 서비스 프로젝트입니다. 검색, 업데이트 및 삭제 (CRUD) 작업에서 수행 하는 호출자를 허용 하는 끝점을 만들려면 WCF 서비스 노출 된 **ContactManager** 데이터베이스입니다. 서비스는 **ContactManager** 데이터베이스 및 **ContactManager.Common.dll** 어셈블리입니다.
- **ContactManager.Common**. 이 클래스 라이브러리 프로젝트입니다. WCF 서비스는이 어셈블리에 정의 된 형식을 사용 합니다.

솔루션에는 게시 라는 솔루션 폴더를 포함 됩니다. 다양 한 사용자 지정 프로젝트 파일 및 제어 빌드 및 배포 프로세스를 조작 하는 방법을 보여 주기는 명령 파일을 포함 합니다. 이 자습서의 뒷부분에서 좀 더 자세히 다룰는 이러한 합니다.

개념 수준에서 솔루션의 구성 요소에 부합 함께 다음과 같이 합니다.

![](the-contact-manager-solution/_static/image2.png)

> [!NOTE]
> ASP.NET MVC 3 웹 응용 프로그램에서 ASP.NET 멤버 자격 공급자를 사용 하는 동안 웹 응용 프로그램 내의 모든 페이지는 익명 액세스를 허용 합니다. 이 명확 하 게 현실적인 구성 되지 않습니다. 그러나 솔루션을 쉽게 배포 하 고 사용자 계정 및 역할을 구성 하지 않고 솔루션을 테스트에 대 한이 방식으로 설정 됩니다.


## <a name="deployment-challenges"></a>배포 문제

Contact Manager 솔루션에서는 다양 한 엔터프라이즈 배포 시나리오에 공통 된 몇 가지 배포 문제를 보여 줍니다.

- 여러 개의 종속 프로젝트가 솔루션 구성 됩니다. 이러한 프로젝트를 동시에 배포 해야 합니다.
- 각 환경에 대해 업데이트 해야 할 연결 문자열 및 서비스 끝점 및 대부분의 경우에이 정보 됩니다 개발자에 게 사용할 수 있습니다.
- 배포 하는 경우는 **ContactManager** 데이터베이스 준비 및 프로덕션 환경에 맞게 후속 배포에 기존 데이터를 보존 해야 합니다.
- ASP.NET 응용 프로그램 서비스 데이터베이스를 배포할 때 일부 구성 데이터를 배포 하지만 사용자 계정 데이터를 생략 해야 합니다.
- 프로젝트에는 일부 파일 및 폴더를 배포 해서는 안 포함 됩니다. 배포 과정에서 이러한 파일 및 폴더를 제외 해야 합니다.
- 솔루션에서 Team Foundation Server (TFS) 빌드 서버에서 자동화 된 배포를 지원 해야 합니다.

## <a name="conclusion"></a>결론

이 항목 않아 솔루션의 상위 수준 개요를 제공 하 고 일부의 다양 한 엔터프라이즈 배포 시나리오에 공통 된 내재 된 배포 문제를 식별 합니다. 이 자습서의 나머지 항목에는 이러한 과제를 충족 하는 데 기술 중 일부를 설명 합니다.

다음 항목인 [the Contact Manager 솔루션 설정](setting-up-the-contact-manager-solution.md)를 다운로드 하 고 개발자 워크스테이션에서 솔루션을 실행 하는 방법을 설명 합니다.

>[!div class="step-by-step"]
[이전](web-deployment-in-the-enterprise.md)
[다음](setting-up-the-contact-manager-solution.md)
