---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment
title: 웹 패키지 배포용 매개 변수 구성 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 서비스 끝점을 인터넷 정보 서비스 (IIS) 웹 응용 프로그램 이름, 연결 문자열 등의 매개 변수 값을 설정 하는 방법을 설명 하는 중...
ms.author: aspnetcontent
ms.date: 05/04/2012
ms.assetid: 37947d79-ab1e-4ba9-9017-52e7a2757414
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment
msc.type: authoredcontent
ms.openlocfilehash: dd8924b0b0055bd32ef55a9ec3a139c4d9b4eb81
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37825117"
---
<a name="configuring-parameters-for-web-package-deployment"></a>웹 패키지 배포용 매개 변수 구성
====================
[Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 원격 IIS 웹 서버에 웹 패키지를 배포할 때 서비스 끝점을 인터넷 정보 서비스 (IIS) 웹 응용 프로그램 이름, 연결 문자열 등의 매개 변수 값을 설정 하는 방법을 설명 합니다.


웹 응용 프로그램 프로젝트, 빌드 및 패키징 프로세스 빌드할 때 세 가지 키 파일을 생성 합니다.

- A *[프로젝트 이름].zip* 파일입니다. 웹 응용 프로그램 프로젝트에 대 한 웹 배포 패키지입니다. 이 패키지는 모든 어셈블리, 파일, 데이터베이스 스크립트 및 원격 IIS 웹 서버에서 웹 응용 프로그램을 다시 만드는 데 필요한 리소스를 포함 합니다.
- A *[프로젝트 이름].deploy.cmd* 파일입니다. 원격 IIS 웹 서버에 웹 배포 패키지를 게시 하는 매개 변수가 있는 Web Deploy (MSDeploy.exe) 명령 집합을 포함 합니다.
- *[프로젝트 이름]. SetParameters.xml* 파일입니다. MSDeploy.exe 명령에 매개 변수 값 집합을 제공합니다. 이 파일에서 값을 업데이트 하 고 전달할 웹 배포 명령줄 매개 변수로 웹 패키지를 배포할 때 수 있습니다.

> [!NOTE]
> 빌드 및 패키징 프로세스에 대 한 자세한 내용은 참조 하세요. [빌드 및 패키징 웹 응용 프로그램 프로젝트](building-and-packaging-web-application-projects.md)합니다.


합니다 *SetParameters.xml* 파일을 웹 응용 프로그램 프로젝트 파일 및 프로젝트 내에서 모든 구성 파일에서 동적으로 생성 됩니다. 빌드하고 웹 게시 파이프라인 (WPP) 프로젝트에 패키지는 IIS 웹 응용 프로그램 대상 처럼 배포 환경 및 데이터베이스 연결 문자열에 따라 달라질 가능성이 있는 변수는 많은 자동으로 검색 합니다. 이 값은 자동으로 웹 배포 패키지에 매개 변수가 있는 하며에 추가 합니다 *SetParameters.xml* 파일입니다. 예를 들어, 연결 문자열을 추가 하는 경우는 *web.config* 파일 웹 응용 프로그램 프로젝트에서 빌드 프로세스에서이 변경 감지 하 고 항목을 추가 합니다 *SetParameters.xml* 파일 적절 하 게 합니다.

대부분의 경우에 이러한 자동 매개 변수화가 됩니다. 그러나 사용자가 응용 프로그램 설정 또는 서비스 끝점 Url과 같은 배포 환경 간의 기타 설정을 변경할 경우 지시 해야 배포 패키지에 이러한 값을 매개 변수화 는해당항목을추가하는WPP*SetParameters.xml* 파일입니다. 다음 단원에서는이 작업을 수행 하는 방법에 설명 합니다.

### <a name="automatic-parameterization"></a>자동 매개 변수화

를 빌드 및 웹 응용 프로그램을 패키지 WPP이 들 매개 변수화 자동으로 됩니다.

- 대상 IIS 웹 응용 프로그램 경로 및 이름입니다.
- 모든 연결 문자열에 *web.config* 파일입니다.
- 추가할 모든 데이터베이스에 대 한 연결 문자열을 **SQL 패키지 및 게시** 프로젝트 속성 페이지에서 탭 합니다.

예를 들어, 빌드 및 패키지화 하는 경우는 [Contact Manager](the-contact-manager-solution.md) 샘플 솔루션을 어떤 방식으로든 WPP 매개 변수화 프로세스를 변경 하지 않고도이 생성 하는 *ContactManager.Mvc.SetParameters.xml* 파일:


[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample1.xml)]


이 경우:

- 합니다 **IIS 웹 응용 프로그램 이름** 매개 변수는 웹 응용 프로그램을 배포 하려는 IIS 경로입니다. 기본 값을 가져옵니다 합니다 **웹 패키지 및 게시** 프로젝트 속성 페이지에서 페이지입니다.
- 합니다 **ApplicationServices-Web.config Connection String** 매개 변수에서 생성 된를 **connectionStrings 추가** 요소에는 *web.config* 파일입니다. 응용 프로그램 멤버 자격 데이터베이스에 연결할 사용 해야 하는 연결 문자열을 나타냅니다. 값을 제공 됩니다 여기에 배포 된 대체 *web.config* 파일입니다. 사전 배포에서 기본 값을 가져옵니다 *web.config* 파일입니다.

WPP에는 생성 된 배포 패키지에서 이러한 속성 매개 변수화 합니다. 배포 패키지를 설치할 때 이러한 속성에 대 한 값을 제공할 수 있습니다. 에 설명 된 대로 수동으로 IIS 관리자를 통해 패키지를 설치 하면 [수동으로 웹 패키지 설치](manually-installing-web-packages.md), 설치 마법사는 모든 매개 변수에 대 한 값을 제공 하 라는 메시지가 표시 됩니다. 원격으로 사용 하 여 패키지를 설치 하는 경우는 *. deploy.cmd* 파일에 설명 된 대로 [웹 패키지 배포](deploying-web-packages.md),이 게 보이는지 Web Deploy *SetParameters.xml* 파일을 매개 변수 값을 제공 합니다. 값을 편집할 수는 *SetParameters.xml* 파일을 수동으로 또는 자동화 된 빌드 및 배포 프로세스의 일부로 파일을 사용자 지정할 수 있습니다. 이 프로세스는이 항목의 뒷부분에 자세히 설명 되어 있습니다.

### <a name="custom-parameterization"></a>사용자 지정 매개 변수화

더 복잡 한 배포 시나리오에서 프로젝트를 배포 하기 전에 추가 속성을 매개 변수화 하려는 경우가 많습니다. 일반적으로 모든 속성 및 설정을 대상 환경 간에 달라 지는 매개 변수화 해야 합니다. 포함할 수 있습니다.

- 서비스 끝점에는 *web.config* 파일입니다.
- 응용 프로그램 설정에는 *web.config* 파일입니다.
- 하려는 다른 선언적 속성 지정 하는 사용자에 게 합니다.

이러한 속성을 매개 변수화 하는 가장 쉬운 방법은 추가 하는 것을 *되므로* 웹 응용 프로그램 프로젝트의 루트 폴더에는 파일입니다. 예를 들어 Contact Manager 솔루션에서는 ContactManager.Mvc 프로젝트에 포함 된 *되므로* 루트 폴더에 파일입니다.

![](configuring-parameters-for-web-package-deployment/_static/image1.png)

이 파일을 열면 단일 있음을 볼 수 있습니다 **매개 변수** 항목입니다. 항목 XML Path Language (XPath) 쿼리를 찾아 ContactService Windows Communication Foundation (WCF) 서비스의 끝점 URL을 매개 변수화를 사용 하 여 합니다 *web.config* 파일입니다.


[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample2.xml)]


배포 패키지에서 끝점 URL을 매개 변수화 하는 것 외에도 WPP 추가 하기 위해 해당 항목의 *SetParameters.xml* 배포 패키지와 함께 생성 되는 파일입니다.


[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample3.xml)]


배포 패키지를 수동으로 설치한 경우 IIS 관리자 때문에 자동으로 매개 변수화 된 속성을 함께 서비스 끝점 주소에 대 한 메시지가 나타납니다. 배포 패키지를 실행 하 여 설치 하는 경우는 *. deploy.cmd* 파일을 편집할 수 있습니다 합니다 *SetParameters.xml* 파일에 대 한 값과 함께 서비스 끝점 주소에 대 한 값을 제공 하는 자동으로 매개 변수화 된 속성입니다.

만드는 방법에 대 한 자세한 내용은 *되므로* 파일을 참조 하십시오 [방법: 구성 배포 설정 하면 패키지를 사용 하 여 매개 변수는 설치](https://msdn.microsoft.com/library/ff398068.aspx)합니다. 라는 프로시저가 **Web.config 파일 설정에 대 한 배포 매개 변수를 사용 하려면** 단계별 지침을 제공 합니다.

## <a name="modifying-the-setparametersxml-file"></a>SetParameters.xml 파일 수정

웹 응용 프로그램 패키지를 수동으로 배포 하려는 경우&#x2014;를 실행 하 여 하나를 *. deploy.cmd* 파일 또는 명령줄에서 MSDeploy.exe를 실행 하 여&#x2014;을 수동으로 편집 하는 항목이 없는 합니다  *SetParameters.xml* 배포 하기 전에 파일입니다. 그러나 엔터프라이즈 규모 솔루션을 작업할 경우 큰, 자동화 된 빌드 및 배포 프로세스의 일부로 웹 응용 프로그램 패키지를 배포 해야 할 수 있습니다. 이 시나리오에서는 Microsoft Build Engine (MSBuild)을 수정 해야 합니다 *SetParameters.xml* 파일입니다. MSBuild를 사용 하 여 이렇게 **XmlPoke** 작업 합니다.

합니다 [Contact Manager 샘플 솔루션](the-contact-manager-solution.md) 이 프로세스를 보여 줍니다. 다음 코드 예제에서는이 예제와 관련 된 정보만 표시 하도록 편집 되었습니다.

> [!NOTE]
> 일반적으로 사용자 지정 프로젝트 파일에 대 한 소개와 샘플 솔루션에서 프로젝트 파일 모델의 광범위 한 개요를 참조 하세요 [프로젝트 파일 이해](understanding-the-project-file.md) 하 고 [빌드 프로세스를 이해](understanding-the-build-process.md)합니다.


첫째, 관심 매개 변수 값은 환경 관련 프로젝트 파일의 속성으로 정의 됩니다 (예를 들어 *Env Dev.proj*).


[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample4.xml)]


> [!NOTE]
> 사용자 고유의 서버 환경에 대 한 환경 관련 프로젝트 파일 사용자 지정 하는 방법에 대 한 지침을 참조 하세요 [대상 환경에 대 한 배포 속성 구성](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)합니다.


다음으로 *Publish.proj* 파일 이러한 속성을 가져옵니다. 때문에 각 *SetParameters.xml* 파일과 관련 된를 *. deploy.cmd* 프로젝트 파일 각 호출을 최종적으로 파일 및 했습니다 *. deploy.cmd* 파일을 프로젝트 파일은 MSBuild를 만듭니다 *항목* 마다 *. deploy.cmd* 파일을 속성으로 관심을 정의 합니다 *항목 메타 데이터*합니다.


[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample5.xml)]


이 경우:

- 합니다 **ParametersXml** 메타 데이터 값의 위치를 나타내는 합니다 *SetParameters.xml* 파일입니다.
- 합니다 **IisWebAppName** 값은 웹 응용 프로그램을 배포 하려는 IIS 경로입니다.
- 합니다 **MembershipDBConnectionString** 값은 멤버 자격 데이터베이스에 대 한 연결 문자열 및 **MembershipDBConnectionName** 값은 합니다 **이름** 특성 해당 매개 변수를 *SetParameters.xml* 파일입니다.
- 합니다 **ServiceEndpointValue** 값은 대상 서버에서 WCF 서비스의 끝점 주소와 **ServiceEndpointParamName** 값은 해당 매개 변수 이름 특성 합니다 *SetParameters.xml* 파일입니다.

마지막으로 *Publish.proj* 파일을 **PublishWebPackages** 사용 하 여 대상를 **XmlPoke** 에서 이러한 값을 수정 하는 작업을 *SetParameters.xml* 파일입니다.


[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample6.xml)]


각 보면 **XmlPoke** 작업 4 개의 특성 값을 지정 합니다.

- 합니다 **XmlInputPath** 특성 수정 하려는 파일을 찾을 수 있는 위치 태스크에 알려 줍니다.
- 합니다 **쿼리** 특성이 변경 하려는 XML 노드를 식별 하는 XPath 쿼리입니다.
- 합니다 **값** 특성 선택 된 XML 노드를 삽입 하려면 새 값입니다.
- 합니다 **조건을** 특성이 조건을 작업을 실행 하거나 실행 되지 않습니다. 이러한 경우 조건에 null 또는 빈 값을 삽입 하려고 하지 확인 합니다 *SetParameters.xml* 파일입니다.

## <a name="conclusion"></a>결론

이 항목에서는의 역할을 설명 합니다 *SetParameters.xml* 파일 및 웹 응용 프로그램 프로젝트를 빌드할 때 생성 되는 방법을 설명 합니다. 추가 하 여 추가 설정을 매개 변수화 하는 방법을 설명 하는 *되므로* 파일을 프로젝트입니다. 도 수정 하는 방법을 설명 합니다 *SetParameters.xml* 사용 하 여 더 큰, 자동화 된 빌드 프로세스의 일부로 파일을 **XmlPoke** 프로젝트 파일에서 작업 합니다.

다음 항목에서는 [웹 패키지 배포](deploying-web-packages.md), 배포 하는 방법을 웹 패키지를 실행 하 여 중 하나에 대해 설명 합니다 *. deploy.cmd* 파일 또는 MSDeploy.exe를 사용 하 여 명령을 직접. 두 경우 모두 지정할 수 있습니다 하 *SetParameters.xml* 배포 매개 변수로 파일입니다.

## <a name="further-reading"></a>추가 정보

웹 패키지를 만드는 방법에 대 한 자세한 내용은 [빌드 및 패키징 웹 응용 프로그램 프로젝트](building-and-packaging-web-application-projects.md)합니다. 실제로 웹 패키지를 배포 하는 방법에 대 한 지침을 참조 하세요 [웹 배포 패키지](deploying-web-packages.md)합니다. 만드는 방법에 대 한 단계별 연습은 *되므로* 파일을 참조 하세요 [방법: 구성 배포 설정 하면 패키지를 사용 하 여 매개 변수는 설치](https://msdn.microsoft.com/library/ff398068.aspx)합니다.

웹 배포에서 매개 변수화에 대 한 일반적인 내용은 참조 하세요. [웹 배포에서 매개 변수화 동작](https://go.microsoft.com/?linkid=9805119) (블로그 게시물).

> [!div class="step-by-step"]
> [이전](building-and-packaging-web-application-projects.md)
> [다음](deploying-web-packages.md)
