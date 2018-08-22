---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/taking-web-applications-offline-with-web-deploy
title: 관련 웹 응용 프로그램은 오프 라인 웹 배포 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 웹 응용 프로그램을 오프 라인으로 인터넷 정보 서비스 (IIS) 웹 배포 관리자를 사용 하 여 자동화 된 배포 중에 사용 하는 방법을 설명 하는 중...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 3e9f6e7d-8967-4586-94d5-d3a122f12529
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/taking-web-applications-offline-with-web-deploy
msc.type: authoredcontent
ms.openlocfilehash: 9b18a48914a74a7fea85278d0e601f6f84376b23
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41829358"
---
<a name="taking-web-applications-offline-with-web-deploy"></a>관련 웹 응용 프로그램은 오프 라인 웹 배포
====================
[Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 웹 응용 프로그램을 오프 라인으로 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포)를 사용 하 여 자동화 된 배포 중에 사용 하는 방법을 설명 합니다. 웹 응용 프로그램으로 이동 하는 사용자 리디렉션됩니다를 *앱\_offline.htm* 배포가 완료 될 때까지 파일입니다.


이 항목의 Fabrikam, Inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항 기반 자습서 시리즈의 일부를 형성 합니다. 샘플 솔루션을 사용 하 여이 자습서 시리즈&#x2014;는 [Contact Manager 솔루션](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;현실적인 수준의 복잡성을 Windows Communication ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내는 Foundation (WCF) 서비스 및 데이터베이스 프로젝트입니다.

이 자습서의 핵심 배포 방법에 설명 된 분할 프로젝트 파일 방법을 기반으로 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md), 두 개의 프로젝트 파일에서 빌드 프로세스에 의해 제어 되는&#x2014;포함 된 모든 대상 환경 및 환경 관련 빌드 및 배포 설정을 포함 하는 하나에 적용 되는 지침을 빌드하십시오. 빌드 시 환경 관련 프로젝트 파일은 빌드 지침의 전체 집합을 이루는 환경을 알 수 없는 프로젝트 파일에 병합 됩니다.

## <a name="task-overview"></a>작업 개요

많은 시나리오를 데이터베이스 또는 웹 서비스와 같은 관련된 구성 요소를 변경 하는 동안 웹 응용 프로그램을 오프 라인 해야 합니다. 일반적으로 IIS 및 ASP.NET에서이를 위해서는 라는 파일을 배치할 *앱\_offline.htm* IIS 웹 사이트 또는 웹 응용 프로그램의 루트 폴더에 있습니다. 합니다 *앱\_offline.htm* 파일은 표준 HTML 파일이 며 일반적으로 사이트 유지 관리로 인해 일시적으로 사용할 수 없는 사용자 라는 간단한 메시지가 포함 됩니다. 하지만 합니다 *앱\_offline.htm* 파일이 웹 사이트의 루트 폴더에 있는, IIS는 파일에 모든 요청을 자동으로 리디렉션합니다. 제거 하면 업데이트를 완료 한 경우는 *앱\_offline.htm* 파일 및 웹 사이트를 다시 시작 요청을 정상적으로 처리 합니다.

추가 및 제거를 통합 하려는 대상 환경에 배포를 자동화 하거나 단일 단계를 수행 하려면 웹 배포를 사용 하는 경우는 *앱\_offline.htm* 배포 프로세스에는 파일입니다. 이 위해 이러한 상위 수준의 작업을 완료 해야 합니다.

- Microsoft Build Engine (MSBuild) 프로젝트 파일에서 배포 프로세스를 제어 하는 MSBuild 대상 만들기를 사용 하는 복사를 *앱\_offline.htm* 파일을 모든 배포 작업 전에 대상 서버 시작 합니다.
- 제거 하는 다른 MSBuild 대상을 추가 합니다 *앱\_offline.htm* 모든 배포 태스크가 완료 되 면 대상 서버에서 파일입니다.
- 웹 응용 프로그램 프로젝트를 만듭니다는 *. wpp.targets* 되도록 하는 파일을 *앱\_offline.htm* Web Deploy를 호출 하면 파일이 배포 패키지에 추가 됩니다.

이 항목에서는 이러한 절차를 수행 하는 방법을 보여줍니다. 작업은이 문서의 연습 가정 이미 만든 하나 이상의 웹 응용 프로그램 프로젝트를 포함 하는 솔루션 및 사용자 지정 프로젝트 파일을 사용 하 여에 설명 된 대로 배포 프로세스를 제어 하려면 [웹 배포에는 엔터프라이즈](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)합니다. 사용할 수 있습니다 합니다 [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) 샘플 항목의 예제를 실행 하는 솔루션입니다.

## <a name="adding-an-appoffline-file-to-a-web-application-project"></a>앱 추가\_오프 라인 파일을 웹 응용 프로그램 프로젝트

첫 번째 태스크를 완료 해야 할 추가 하는 것을 *앱\_오프 라인* 웹 응용 프로그램 프로젝트 파일:

- 파일 개발 프로세스를 간섭 하지 않도록 설정 하려면 (영구적으로 오프 라인 상태가 될 응용 프로그램)를 않으려면 메서드를 호출 해야 것 이외의 *앱\_offline.htm*합니다. 예를 들어, 파일 이름이 있습니다 *앱\_오프 라인 template.htm*합니다.
- 파일 배포 되지 않게 하려면-는 빌드 작업을 설정 해야 **None**합니다.

**앱에 추가할\_오프 라인 파일을 웹 응용 프로그램 프로젝트**

1. Visual Studio 2010에서 솔루션을 엽니다.
2. 에 **솔루션 탐색기** 창에서 웹 응용 프로그램 프로젝트를 마우스 오른쪽 단추로 클릭을 가리킵니다 **추가**를 클릭 하 고 **새 항목**합니다.
3. 에 **새 항목 추가** 대화 상자에서 **HTML 페이지**합니다.
4. 에 **이름** 상자에 입력 **앱\_template.htm 오프 라인**를 클릭 하 고 **추가**합니다.

    ![](taking-web-applications-offline-with-web-deploy/_static/image1.png)
5. 사용자에 게 알려 응용 프로그램을 사용할 수 없는 몇 가지 간단한 HTML을 추가 하 고 파일을 저장 합니다. 서버 쪽 태그를 포함 하지 마세요 (예를 들어 태그가 접두사로 사용 하는 "asp:"). 

    ![](taking-web-applications-offline-with-web-deploy/_static/image2.png)
6. 에 **솔루션 탐색기** 창에서 새 파일을 마우스 오른쪽 단추로 클릭 하 고 클릭 **속성**합니다.
7. 에 **속성** 창에서를 **빌드 작업** 행을 선택 **None**합니다.

    ![](taking-web-applications-offline-with-web-deploy/_static/image3.png)

## <a name="deploying-and-deleting-an-appoffline-file"></a>배포 하 고 앱을 삭제 해도\_오프 라인 파일

다음 단계는 배포 프로세스의 시작 부분에 대상 서버로 파일을 복사한 후에 제거를 배포 논리를 수정 하는 것입니다.

> [!NOTE]
> 다음 절차에 설명 된 대로 배포 프로세스를 제어 하는 사용자 지정 MSBuild 프로젝트 파일을 사용 하는 것으로 가정 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)합니다. Visual Studio에서 직접에 배포 하는 경우에 다른 방법을 사용 해야 합니다. Sayed Ibrahim Hashimi 설명에서 이러한 한 가지 방법은 [수행할 사용자 웹 앱 오프 라인 중 게시 방법](http://sedodream.com/2012/01/08/HowToTakeYourWebAppOfflineDuringPublishing.aspx)합니다.


배포 하는 *앱\_오프 라인* 파일 대상 IIS 웹 사이트에 MSDeploy.exe를 사용 하 여 호출 해야 합니다 [웹 배포 **contentPath** 공급자](https://technet.microsoft.com/library/dd569034(WS.10).aspx)합니다. 합니다 **contentPath** 공급자 지원 실제 디렉터리 경로 IIS 웹 사이트 또는 응용 프로그램 경로 Visual Studio 프로젝트 폴더와 IIS 웹 응용 프로그램 간에 파일을 동기화 하는 데 이상적인 있도록 합니다. 파일을 배포 하려면 MSDeploy 명령을 다음과 비슷합니다.


[!code-console[Main](taking-web-applications-offline-with-web-deploy/samples/sample1.cmd)]


배포 프로세스의 끝에 있는 대상 사이트에서 파일을 제거 하려면 MSDeploy 명령을 다음과 비슷합니다.


[!code-console[Main](taking-web-applications-offline-with-web-deploy/samples/sample2.cmd)]


이러한 명령은 빌드 및 배포 프로세스의 일부로 자동화 하기 위해 사용자 지정 MSBuild 프로젝트 파일에 통합 해야 합니다. 다음 절차에는이 작업을 수행 하는 방법을 설명 합니다.

**배포 하 고 앱을 삭제 하려면\_오프 라인 파일**

1. Visual Studio 2010에서 배포 프로세스를 제어 하는 MSBuild 프로젝트 파일을 엽니다. 에 [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) 이것이 샘플 솔루션을 *Publish.proj* 파일.
2. 루트에서 **프로젝트** 요소를 만듭니다 **PropertyGroup** 요소에 대 한 변수를 저장 하는 *앱\_오프 라인* 배포:

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample3.xml)]
3. 합니다 **SourceRoot** 속성에서 다른 곳에서 정의 되는 *Publish.proj* 파일. 현재 경로 상대적인 원본 콘텐츠에 대 한 루트 폴더의 위치를 나타냅니다&#x2014;의 위치를 기준으로 말해 합니다 *Publish.proj* 파일입니다.
4. 합니다 **contentPath** 공급자는 소스 파일에 절대 경로 배포 하기 전에 준비 해야 하므로 상대 파일 경로 수락 하지 않습니다. 사용할 수는 [ConvertToAbsolutePath](https://msdn.microsoft.com/library/bb882668.aspx) 이 작업을 수행 하는 작업입니다.
5. 새 **대상** 명명 된 요소가 **GetAppOfflineAbsolutePath**합니다. 이 대상을 사용 하 여는 **ConvertToAbsolutePath** 의 절대 경로를 가져오는 작업을 합니다 *앱\_오프 라인 템플릿* 프로젝트 폴더의 파일.

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample4.xml)]
6. 이 대상의 상대 경로를 사용 합니다 *앱\_템플릿을 오프 라인* 프로젝트 폴더의 파일 절대 파일 경로로 새 속성에 저장 합니다. **BeforeTargets** 특성 지정이 대상 보다 먼저 실행 하려는 합니다 **DeployAppOffline** 다음 단계에 만들게 될 대상입니다.
7. 라는 새 대상 추가 **DeployAppOffline**합니다. 이 대상 내에서 배포 하는 MSDeploy.exe 명령을 호출 하 *앱\_오프 라인* 파일을 대상 웹 서버입니다.

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample5.xml)]
8. 이 예제는 **ContactManagerIisPath** 속성은 프로젝트 파일의 다른 곳에서 정의 합니다. 이 단순히 IIS 응용 프로그램 경로 형태로 *[IIS 웹 사이트 이름] / [응용 프로그램 이름]* 합니다. 사용자가 전환할 수 있도록 대상에서 조건을 포함 하는 *앱\_오프 라인* 속성 값을 변경 하거나 명령줄 매개 변수를 제공 하 여 배포 하거나 해제 합니다.
9. 라는 새 대상 추가 **DeleteAppOffline**합니다. 이 대상에서 제거 하는 MSDeploy.exe 명령을 호출 하면 *앱\_오프 라인* 대상 웹 서버에서 파일.

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample6.xml)]
10. 마지막 작업 프로젝트 파일의 실행 하는 동안 적절 한 시점에 이러한 새 대상을 호출 하는 것입니다. 다양 한 방법으로이 수행할 수 있습니다. 예를 들어,를 *Publish.proj* 파일을 **FullPublishDependsOn** 속성에는 실행 해야 하는 대상의 목록을 지정 합니다의 경우 주문를 **FullPublish** 기본 대상 호출 됩니다.
11. 호출 하기 위해 MSBuild 프로젝트 파일을 수정 합니다 **DeployAppOffline** 및 **DeleteAppOffline** 게시 프로세스에 적절 한 시점에 대상입니다.

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample7.xml)]

사용자 지정 MSBuild 프로젝트 파일을 실행 합니다 *앱\_오프 라인* 파일은 빌드에 성공한 후 바로 서버에 배포 됩니다. 그런 다음 삭제 됩니다 서버에서 모든 배포 작업이 완료 되 면 합니다.

## <a name="adding-an-appoffline-file-to-deployment-packages"></a>앱 추가\_배포 패키지를 오프 라인 파일

대상 IIS에 콘텐츠를 기존 웹 응용 프로그램 배포를 구성 하는 방법에 따라&#x2014;와 같은 합니다 *앱\_offline.htm* 파일&#x2014;웹을 배포 하는 경우 자동으로 삭제 될 수 있습니다 패키지 대상입니다. 되도록 합니다 *앱\_offline.htm* 파일은 배포의 기간에 대 한 곳에서 유지 됩니다. 파일의 시작 부분에 직접 배포 하는 데 또한 웹 배포 패키지 자체 내에서 파일을 포함 해야 합니다. 배포 프로세스입니다.

- 경우에이 항목의 이전 태스크를 수행한,에서는 추가한 합니다 *앱\_offline.htm* 파일을 다른 파일 이름에서 웹 응용 프로그램 프로젝트 (했습니다 *앱\_ 오프 라인 template.htm*)에서는 빌드 작업으로 설정한 및 **None**합니다. 이러한 변경은 방해 개발 및 디버깅에서 파일을 방지 하기 위해 필요 합니다. 되도록 패키징 프로세스를 사용자 지정 해야 하는 결과적으로 *앱\_offline.htm* 파일이 웹 배포 패키지에 포함 되어 있습니다.

웹 게시 파이프라인 (WPP) 라는 항목 목록을 사용 하 여 **FilesForPackagingFromProject** 웹 배포 패키지에 포함 되어야 하는 파일의 목록을 빌드할 수 있습니다. 이 목록에 고유한 항목을 추가 하 여 웹 패키지의 콘텐츠를 사용자 지정할 수 있습니다. 이렇게 하려면 다음 대략적인 단계를 완료 해야 합니다.

1. 라는 사용자 지정 프로젝트 파일을 만듭니다 *[프로젝트 이름].wpp.targets* 프로젝트 파일과 동일한 폴더에 있습니다.

    > [!NOTE]
    > 합니다 *. wpp.targets* 파일을 웹 응용 프로그램 프로젝트 파일과 동일한 폴더에 이동 해야&#x2014;예를 들어 *ContactManager.Mvc.csproj*&#x2014;아닌 같은 사용자 지정 폴더 프로젝트 파일을 사용 하면 빌드 및 배포 프로세스를 제어할 수 있습니다.
2. 에 *. wpp.targets* 파일을 실행 하는 새 MSBuild 대상 만들기 *하기 전에* 는 **CopyAllFilesToSingleFolderForPackage** 대상입니다. 이 패키지에 포함할 항목의 목록을 작성 하는 WPP 대상입니다.
3. 만들 새 대상에 **ItemGroup** 요소입니다.
4. 에 **ItemGroup** 요소를 추가 **FilesForPackagingFromProject** 항목을 지정 합니다 *앱\_offline.htm* 파일.

합니다 *. wpp.targets* 파일 다음과 유사 합니다.


[!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample8.xml)]


다음은이 예에서의 핵심 포인트입니다.

- 합니다 **BeforeTargets** 특성 삽입 하기 바로 전에 실행 해야 하는이 대상 지정 하 여 WPP 합니다 **CopyAllFilesToSingleFolderForPackage** 대상입니다.
- **FilesForPackagingFromProject** 사용 하 여 항목는 **DestinationRelativePath** 메타 데이터 값에서 파일 이름을 바꾸려면 *앱\_오프 라인 template.htm* 하 *앱\_offline.htm* 목록에 추가 됩니다.

다음 절차에서는이 추가 하는 방법을 보여 줍니다 *. wpp.targets* 파일을 웹 응용 프로그램 프로젝트입니다.

**추가 하는. 웹 배포 패키지에.wpp.targets 파일**

1. Visual Studio 2010에서 솔루션을 엽니다.
2. 에 **솔루션 탐색기** 창에서 웹 응용 프로그램 프로젝트 노드를 마우스 오른쪽 단추로 클릭 (예를 들어 **ContactManager.Mvc**), 가리킵니다 **추가**, 클릭하고**새 항목**합니다.
3. 에 **새 항목 추가** 대화 상자를 선택 합니다 **XML 파일** 템플릿.
4. 에 **이름** 상자에 입력 *[프로젝트 이름] * * *.wpp.targets** (예를 들어 **ContactManager.Mvc.wpp.targets**)를 클릭 하 고 **추가**.

    ![](taking-web-applications-offline-with-web-deploy/_static/image4.png)

    > [!NOTE]
    > 새 항목을 프로젝트의 루트 노드로 추가 하는 경우 파일은 프로젝트 파일과 동일한 폴더에 생성 됩니다. Windows 탐색기에서 폴더를 열어이 확인할 수 있습니다.
5. 파일에서 이전에 설명 된 MSBuild 태그를 추가 합니다.

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample9.xml)]
6. 저장 후 닫기 합니다 *[프로젝트 이름].wpp.targets* 파일입니다.

다음에 웹 응용 프로그램 프로젝트 빌드 및 패키지 있습니다, WPP가 자동으로 감지 합니다 *. wpp.targets* 파일입니다. *앱\_오프 라인 template.htm* 파일을 결과 웹 배포 패키지에 포함 됩니다 *앱\_offline.htm*합니다.

> [!NOTE]
> 배포에 실패할 경우 합니다 *앱\_offline.htm* 파일 위치에 남아 있고 응용 프로그램은 오프 라인 상태로 유지 됩니다. 이것이 일반적으로 원하는 동작입니다. 응용 프로그램을 다시 온라인으로 삭제할 수 있습니다 합니다 *앱\_offline.htm* 웹 서버에서 파일입니다. 또는 오류를 수정 하 고 성공적인 배포를 실행 하는 경우는 *앱\_offline.htm* 파일이 제거 됩니다.


## <a name="conclusion"></a>결론

이 항목에서는 게시 하 여 웹 응용 프로그램을 오프 라인 배포의 기간을 사용 하는 방법을 설명한를 *앱\_offline.htm* 배포 프로세스의 시작 부분에 대상 서버로 파일 및에서 제거 합니다 끝입니다. 포함 하는 방법을 설명 된 *앱\_offline.htm* 웹 배포 패키지에서 파일입니다.

## <a name="further-reading"></a>추가 정보

패키징 및 배포 프로세스에 대 한 자세한 내용은 참조 하세요. [빌드 및 패키징 웹 응용 프로그램 프로젝트](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)하십시오 [웹 패키지 배포용 매개 변수 구성](../web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment.md), 및 [ 웹 패키지 배포](../web-deployment-in-the-enterprise/deploying-web-packages.md)합니다.

이 자습서에 설명 된 사용자 지정 MSBuild 프로젝트 파일 방법을 사용 해야 응용 프로그램 오프 라인으로 게시 하는 동안 되려면 약간 다른 방법을 사용 하는 것이 아니라 Visual Studio에서 직접 웹 응용 프로그램을 게시 하는 경우 프로세스입니다. 자세한 내용은 [게시 하는 동안 오프 라인 웹 앱을 사용 하는 방법을](https://go.microsoft.com/?linkid=9805135) (블로그 게시물).

> [!div class="step-by-step"]
> [이전](excluding-files-and-folders-from-deployment.md)
> [다음](running-windows-powershell-scripts-from-msbuild-project-files.md)
