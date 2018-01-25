---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment
title: "웹 패키지 배포에 대 한 매개 변수 구성 | Microsoft Docs"
author: jrjlee
description: "이 항목에서는 인터넷 정보 서비스 (IIS) 웹 응용 프로그램 이름, 연결 문자열 및 서비스 끝점 등의 매개 변수 값을 설정 하는 방법을 설명..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 37947d79-ab1e-4ba9-9017-52e7a2757414
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment
msc.type: authoredcontent
ms.openlocfilehash: 12a4ba8ad30df43e7192500ad4514dfa9679f899
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="configuring-parameters-for-web-package-deployment"></a>웹 패키지 배포에 대 한 매개 변수를 구성합니다.
====================
으로 [Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 원격 IIS 웹 서버에 웹 패키지를 배포할 때 인터넷 정보 서비스 (IIS) 웹 응용 프로그램 이름, 연결 문자열 및 서비스 끝점 등의 매개 변수 값을 설정 하는 방법에 설명 합니다.


빌드할 때 웹 응용 프로그램 프로젝트, 빌드 및 패키징 프로세스에서는 세 개의 키 파일 생성 됩니다.

- A *[프로젝트 이름].zip* 파일입니다. 웹 응용 프로그램 프로젝트에 대 한 웹 배포 패키지입니다. 이 패키지는 모든 어셈블리, 파일, 데이터베이스 스크립트 및 원격 IIS 웹 서버에서 웹 응용 프로그램을 다시 만드는 데 필요한 리소스를 포함 합니다.
- A *[프로젝트 이름].deploy.cmd* 파일입니다. 이는 원격 IIS 웹 서버에 웹 배포 패키지를 게시 하는 매개 변수가 있는 Web Deploy (MSDeploy.exe) 명령 집합을 포함 합니다.
- A *[프로젝트 name]. SetParameters.xml* 파일입니다. MSDeploy.exe 명령에 매개 변수 값 집합을 제공합니다. 이 파일의 값을 업데이트 하 고 웹 배포 매개 변수로 전달 된 명령줄 웹 패키지를 배포할 때 수 있습니다.

> [!NOTE]
> 빌드 및 패키징 프로세스에 대 한 자세한 내용은 참조 하십시오. [빌드 및 패키징 웹 응용 프로그램 프로젝트](building-and-packaging-web-application-projects.md)합니다.


*SetParameters.xml* 파일은 웹 응용 프로그램 프로젝트 파일 및 프로젝트 내에서 구성 파일에서 동적으로 생성 됩니다. 빌드하고 웹 게시 파이프라인 (WPP) 프로젝트를 패키지 배포 환경, 예: 대상 IIS 웹 응용 프로그램 및 데이터베이스 연결 문자열 사이 변경 가능성이 있는 변수를 많은 자동으로 검색 합니다. 이러한 값은 자동으로 웹 배포 패키지에서 매개 변수가 있으며에 추가 된 *SetParameters.xml* 파일입니다. 예를 들어, 연결 문자열을 추가 하는 경우는 *web.config* 파일 웹 응용 프로그램 프로젝트에서 빌드 프로세스를이 변경 내용을 검색 하 고 항목을 추가 합니다는 *SetParameters.xml* 파일 적절 하 게 합니다.

이 자동 매개 변수화는 대부분의 경우에 적용 됩니다. 그러나 응용 프로그램 설정 또는 서비스 끝점 Url과 같은 배포 환경 간에 다른 설정을 변경 해야 하는 경우 지시 해야 배포 패키지에 이러한 값을 매개 변수화 하는 에해당하는항목이추가WPP*SetParameters.xml* 파일입니다. 다음 섹션에서는이 작업을 수행 하는 방법을 설명 합니다.

### <a name="automatic-parameterization"></a>자동 매개 변수화

웹 응용 프로그램 패키지를 빌드할 때 WPP 이러한 것 들 매개 변수화 자동으로 됩니다.

- 대상 IIS 웹 응용 프로그램 경로 및 이름입니다.
- 모든 연결 문자열에 *web.config* 파일입니다.
- 에 추가 하는 모든 데이터베이스에 대 한 연결 문자열은 **SQL 패키지 및 게시** 프로젝트 속성 페이지에서 탭 합니다.

예를 들어, 빌드 및 패키징합니다 하는 경우는 [않아](the-contact-manager-solution.md) WPP 어떤 방식으로 매개 변수화 프로세스를 건드리지 않고 간단히 샘플 솔루션을 생성이 *ContactManager.Mvc.SetParameters.xml* 파일:


[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample1.xml)]


이 경우:

- **IIS 웹 응용 프로그램 이름** 매개 변수는 웹 응용 프로그램을 배포 하려면 IIS 경로입니다. 기본 값을 가져오는 **웹 패키지 및 게시** 프로젝트 속성 페이지의 페이지입니다.
- **ApplicationServices Web.config 연결 문자열** 에서 생성 된 매개 변수는 **connectionStrings/추가** 요소에는 *web.config* 파일입니다. 응용 프로그램 멤버 자격 데이터베이스에 연결 하는 데 사용 해야 하는 연결 문자열을 나타냅니다. 여기 됩니다 제공 하는 값에는 배포 된 대체 *web.config* 파일입니다. 배포 전에서 기본 값을 가져오는 *web.config* 파일입니다.

WPP에 생성 된 배포 패키지에서 이러한 속성 매개 변수화 합니다. 배포 패키지를 설치할 때 이러한 속성에 대 한 값을 제공할 수 있습니다. 에 설명 된 대로 수동으로 IIS 관리자를 통해 패키지를 설치 하면 [수동으로 웹 패키지 설치](manually-installing-web-packages.md), 설치 마법사에 대 한 매개 변수 값을 제공 하 라는 메시지를 표시 합니다. 원격으로 사용 하 여 패키지를 설치 하는 경우는 *. deploy.cmd* 파일에 설명 된 대로 [웹 패키지 배포](deploying-web-packages.md),이 게 표시 되 웹 배포 *SetParameters.xml* 파일을 매개 변수 값을 제공 합니다. 값을 편집할 수는 *SetParameters.xml* 파일을 수동으로 또는 자동화 된 빌드 및 배포 프로세스의 일부로 파일을 사용자 지정할 수 있습니다. 이 프로세스는이 항목의 뒷부분에 자세히 설명 되어 있습니다.

### <a name="custom-parameterization"></a>사용자 지정 매개 변수화

더 복잡 한 배포 시나리오에서 프로젝트를 배포 하기 전에 추가 속성을 매개 변수화 하고자 합니다. 일반적으로 모든 속성 및 설정을 대상 환경 간에 달라 집니다 매개 변수화 해야 합니다. 이러한 포함할 수 있습니다.

- 서비스 끝점에는 *web.config* 파일입니다.
- 응용 프로그램 설정에는 *web.config* 파일입니다.
- 하려는 다른 선언적 속성 지정 내용 메시지를 표시 합니다.

이러한 속성을 매개 변수화 하는 가장 쉬운 방법은 추가 하는 것을 *parameters.xml* 파일을 웹 응용 프로그램 프로젝트의 루트 폴더입니다. 예를 들어 연락처 관리자 솔루션에서는 ContactManager.Mvc 프로젝트에 포함 되어는 *parameters.xml* 루트 폴더에는 파일입니다.

![](configuring-parameters-for-web-package-deployment/_static/image1.png)

이 파일을 열는 단일 있음을 볼 수 있습니다 **매개 변수** 항목입니다. 항목 XML 경로 언어 (XPath) 쿼리를 찾아에 ContactService Windows Communication Foundation (WCF) 서비스의 끝점 URL을 매개 변수화를 사용 하 여는 *web.config* 파일입니다.


[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample2.xml)]


외에 배포 패키지에는 끝점 URL을 매개 변수화를 WPP도 추가 하기 위해 해당 항목은 *SetParameters.xml* 배포 패키지와 함께 생성 되는 파일입니다.


[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample3.xml)]


배포 패키지를 수동으로 설치 하는 경우 IIS 관리자는 해당 속성을 자동으로 매개 변수화 된와 함께 서비스 끝점 주소에 대 한 묻는 됩니다. 실행 하 여 배포 패키지를 설치 하는 경우는 *. deploy.cmd* 파일을 편집할 수 있습니다는 *SetParameters.xml* 파일에 대 한 값과 함께 서비스 끝점 주소에 대 한 값을 제공 하는 자동으로 매개 변수화 된는 속성입니다.

만드는 방법에 대 한 자세한 내용은 *parameters.xml* 파일에서 참조 [하는 방법: 설치 되어 구성 배포 설정을 때는 패키지에 매개 변수 사용](https://msdn.microsoft.com/library/ff398068.aspx)합니다. 라는 프로시저 **Web.config 파일 설정에 대 한 배포 매개 변수를 사용 하려면** 단계별 지침을 제공 합니다.

## <a name="modifying-the-setparametersxml-file"></a>SetParameters.xml 파일 수정

경우 수동으로 웹 응용 프로그램 패키지를 배포 하도록 계획 & #x 2014; 중 하나를 실행 하 여는 *. deploy.cmd* 파일 또는 명령줄 & #x 2014;에서 MSDeploy.exe를 실행 하 여 더 할 게 없습니다을 수동으로 편집 하 여 중지*SetParameters.xml* 배포 하기 전에 파일입니다. 그러나 엔터프라이즈 규모 솔루션에서 작업할 경우 큰, 자동화 된 빌드 및 배포 프로세스의 일부로 웹 응용 프로그램 패키지를를 배포 해야 할 수 있습니다. 이 시나리오에서는 Microsoft Build Engine (MSBuild)를 수정할 필요는 *SetParameters.xml* 파일에 있습니다. MSBuild를 사용 하 여 이렇게 하려면 **XmlPoke** 작업 합니다.

[않아 샘플 솔루션](the-contact-manager-solution.md) 이 과정을 보여 줍니다. 다음 코드 예제이 예제에 관련 된 정보만 표시 하도록 편집 되었습니다.

> [!NOTE]
> 일반적으로 사용자 지정 프로젝트 파일에 대 한 소개와 샘플 솔루션에서 프로젝트 파일 모델의 광범위 한 개요를 참조 하십시오. [프로젝트 파일 이해](understanding-the-project-file.md) 및 [빌드 프로세스를 이해](understanding-the-build-process.md)합니다.


관심 있는 매개 변수 값 환경별 프로젝트 파일에 속성으로 정의 된 첫째, (예를 들어 *Env Dev.proj*).


[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample4.xml)]


> [!NOTE]
> 사용자 고유의 서버 환경에 대 한 환경 관련 프로젝트 파일 사용자 지정 하는 방법에 대 한 지침을 참조 하십시오. [대상 환경에 대 한 배포 속성 구성](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)합니다.


다음으로 *Publish.proj* 파일은 이러한 속성을 가져옵니다. 때문에 각 *SetParameters.xml* 파일과 관련 된 한 *. deploy.cmd* 파일과 우리 궁극적으로 프로젝트 파일을 만들 각 호출 *. deploy.cmd* 파일, 프로젝트 파일을 만듭니다는 MSBuild *항목* 각 *. deploy.cmd* 서 대상의 속성을 정의 하 고 파일 *항목 메타 데이터*합니다.


[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample5.xml)]


이 경우:

- **ParametersXml** 메타 데이터 값의 위치를 나타냅니다.는 *SetParameters.xml* 파일입니다.
- **IisWebAppName** 값은 웹 응용 프로그램을 배포 하려면 IIS 경로입니다.
- **MembershipDBConnectionString** 값은 멤버 자격 데이터베이스에 대 한 연결 문자열 및 **MembershipDBConnectionName** 값이 고 **이름** 특성 해당 매개 변수는 *SetParameters.xml* 파일입니다.
- **ServiceEndpointValue** 값은 대상 서버에서 WCF 서비스에 대 한 끝점 주소 및 **ServiceEndpointParamName** 값은에서 해당 매개 변수의 이름 특성 *SetParameters.xml* 파일입니다.

마지막으로 *Publish.proj* 파일을는 **PublishWebPackages** 대상으로 사용 하 여는 **XmlPoke** 작업에서 이러한 값을 수정 하는 *SetParameters.xml* 파일입니다.


[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample6.xml)]


각 보면 **XmlPoke** 작업 4 가지 특성 값을 지정 합니다.

- **XmlInputPath** 특성은 태스크를 수정 하려는 파일을 찾을 위치를 지시 합니다.
- **쿼리** 특성은 변경 하려면 XML 노드를 식별 하는 XPath 쿼리입니다.
- **값** 특성은 선택 된 XML 노드를 삽입 하려면 새 값입니다.
- **조건** 특성은 조건에서 작업을 실행 하거나 실행 되지 않습니다. 이러한 경우 조건을 사용 하면에 null 또는 빈 값을 삽입 하려고 하지 않습니다는 *SetParameters.xml* 파일입니다.

## <a name="conclusion"></a>결론

이 항목의 역할을 설명는 *SetParameters.xml* 파일을 웹 응용 프로그램 프로젝트를 빌드할 때 생성 되는 방식을 설명 합니다. 추가 설정의 매개 변수화를 추가 하 여는 방법을 설명 하는 *parameters.xml* 파일을 프로젝트입니다. 도 수정 하는 방법을 설명는 *SetParameters.xml* 파일을 사용 하 여 더 큰, 자동화 된 빌드 프로세스의 일부로 **XmlPoke** 프로젝트 파일에서 작업 합니다.

다음 항목 [웹 패키지 배포](deploying-web-packages.md), 배포 하는 방법 웹 패키지를 실행 하거나 설명의 *. deploy.cmd* 파일 또는 MSDeploy.exe를 사용 하 여 명령을 직접 합니다. 두 경우 모두 지정할 수 있습니다 프로그램 *SetParameters.xml* 파일 배포 매개 변수로 합니다.

## <a name="further-reading"></a>추가 정보

웹 패키지를 만드는 방법에 대 한 자세한 내용은 참조 하십시오. [빌드 및 패키징 웹 응용 프로그램 프로젝트](building-and-packaging-web-application-projects.md)합니다. 실제로 웹 패키지를 배포 하는 방법에 대 한 지침을 참조 하십시오. [웹 패키지 배포](deploying-web-packages.md)합니다. 만드는 방법에 대 한 단계별 연습은 *parameters.xml* 파일에서 참조 [하는 방법: 설치 되어 구성 배포 설정을 때는 패키지에 매개 변수 사용](https://msdn.microsoft.com/library/ff398068.aspx)합니다.

매개 변수화 웹 배포에 대 한 일반적인 정보를 참조 하십시오. [웹 배포에서 매개 변수화 동작](https://go.microsoft.com/?linkid=9805119) (블로그 게시물).

>[!div class="step-by-step"]
[이전](building-and-packaging-web-application-projects.md)
[다음](deploying-web-packages.md)
