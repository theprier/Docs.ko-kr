---
title: "Visual Studio를 사용해서 Azure 앱 서비스에 ASP.NET Core 앱 게시하기"
author: rick-anderson
description: 
keywords: ASP.NET Core
ms.author: riande
manager: wpickett
ms.date: 10/05/2017
ms.topic: get-started-article
ms.assetid: 78571e4a-a143-452d-9cf2-0860f85972e6
ms.technology: aspnet
ms.prod: asp.net-core
uid: tutorials/publish-to-azure-webapp-using-vs
ms.openlocfilehash: 6f697ed4d8876a19cd058533e4f6a5d4f7cdc2fb
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
# <a name="publish-an-aspnet-core-web-app-to-azure-app-service-using-visual-studio"></a>Visual Studio를 사용해서 Azure 앱 서비스에 ASP.NET Core 앱 게시하기

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT), [Cesar Blum Silveira](https://github.com/cesarbs) 및 [Rachel Appel](https://twitter.com/rachelappel)

Mac에서 작업하고 있다면 [Visual Studio for Mac에서 Azure에 게시하기](https://blog.xamarin.com/publish-azure-visual-studio-mac/)를 참조하시기 바랍니다.

## <a name="set-up"></a>설치

* 아직 Azure 계정이 없다면 [Azure 무료 계정 만들기](https://azure.microsoft.com/ko-kr/free/) 페이지를 방문하시기 바랍니다. 

## <a name="create-a-web-app"></a>웹 앱 만들기

Visual Studio 시작 페이지에서 **파일 > 새로 만들기 > 프로젝트...**를 선택합니다.

![파일 메뉴](publish-to-azure-webapp-using-vs/_static/file_new_project.png)

**새 프로젝트** 대화 상자의 항목을 입력해서 완료합니다.

* 왼쪽 창에서 **.NET Core**를 선택합니다.

* 가운데 창에서 **ASP.NET Core 웹 응용 프로그램**을 선택합니다.

* **확인**을 선택합니다.

![새 프로젝트 대화 상자](publish-to-azure-webapp-using-vs/_static/new_prj.png)

**새 ASP.NET Core 웹 응용 프로그램** 대화 상자에서:

* **웹 응용 프로그램**을 선택합니다.

* **인증 변경**을 선택합니다.

![새 프로젝트 대화 상자](publish-to-azure-webapp-using-vs/_static/new_prj_2.png)

**인증 변경** 대화 상자가 나타납니다. 

* **개별 사용자 계정**을 선택합니다.

* **확인**을 선택해서 **새 ASP.NET Core 웹 응용 프로그램** 대화 상자로 돌아간 다음, 다시 **확인**을 선택합니다.

![새 ASP.NET Core 웹 인증 대화 상자](publish-to-azure-webapp-using-vs/_static/new_prj_auth.png) 

그러면 Visual Studio가 솔루션을 생성합니다.

## <a name="run-the-app-locally"></a>로컬에서 앱 실행하기

* **디버그**를 선택한 다음 **디버깅하지 않고 시작**을 선택해서 로컬에서 앱을 실행합니다.

* **About** 링크나 **Contact** 링크를 클릭해서 웹 응용 프로그램이 정상적으로 동작하는지 확인합니다.

![localhost의 Microsoft Edge에서 열린 웹 응용 프로그램](publish-to-azure-webapp-using-vs/_static/show.png)

* **Register** 링클를 선택해서 새로운 사용자를 등록해봅니다. 이때 임의의 전자 메일 주소를 사용해서 테스트할 수 있습니다. 그러나 양식을 제출하면 페이지에 다음과 같은 오류가 출력됩니다.

    *“내부 서버 오류: 요청을 처리하는 동안 데이터베이스 작업이 실패했습니다. SQL 예외: 데이터베이스를 열 수 없습니다. 응용 프로그램 DB 컨텍스트에 대한 기존 마이그레이션 적용으로 이 문제를 해결할 수 있습니다.”*

* **Apply Migrations**를 선택한 다음, 페이지가 갱신되면 페이지를 새로 고칩니다.

![내부 서버 오류: 요청을 처리하는 동안 데이터베이스 작업이 실패했습니다. SQL 예외: 데이터베이스를 열 수 없습니다. 응용 프로그램 DB 컨텍스트에 대한 기존 마이그레이션 적용으로 이 문제를 해결할 수 있습니다.](publish-to-azure-webapp-using-vs/_static/mig.png)

앱 상단에 새로운 사용자를 등록하는 데 사용한 전자 메일과 **Log out** 링크가 출력됩니다.

![Microsoft Edge에서 열린 웹 앱. Register 링크는 Hello email@domain.com이라는 텍스트로 교체됩니다.](publish-to-azure-webapp-using-vs/_static/hello.png)

## <a name="deploy-the-app-to-azure"></a>Azure에 앱 배포하기

웹 페이지를 닫고 Visual Studio로 돌아간 다음 **디버그** 메뉴에서 **디버깅 중지**를 선택합니다.

솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시...**를 선택합니다.

![강조 표시된 게시 링크로 열린 바로 가기 메뉴](publish-to-azure-webapp-using-vs/_static/pub.png)

**게시** 대화 상자에서 **Microsoft Azure App Service**를 선택하고 **게시**를 클릭합니다.

![게시 대화 상자](publish-to-azure-webapp-using-vs/_static/maas1.png)

* 앱에 고유한 이름을 지정합니다. 

* 구독을 선택합니다.

* 리소스 그룹에서 **새로 만들기...**를 선택하고 새 리소스 그룹의 이름을 입력합니다.

* App Service Plan에서 **새로 만들기...**를 선택하고 가까운 위치를 선택합니다. 기본적으로 생성되는 이름을 그대로 사용해도 무방합니다.

![App Service 대화 상자](publish-to-azure-webapp-using-vs/_static/newrg1.png)

* **서비스** 탭을 선택해서 새 데이터베이스를 만듭니다.

* 녹색 **+** 아이콘을 선택해서 새 SQL 데이터베이스를 만듭니다.

![새 SQL 데이터베이스](publish-to-azure-webapp-using-vs/_static/sql.png)

* **SQL 데이터베이스 구성** 대화 상자에서 **새로 만들기...**를 선택해서 새로운 데이터베이스 서버를 만듭니다.

![새 SQL 데이터베이스 및 서버](publish-to-azure-webapp-using-vs/_static/conf.png)

**SQL Server 구성** 대화 상자가 나타납니다.

* 관리자 사용자 이름 및 암호를 입력한 다음 **확인**을 선택합니다. 이 단계에서 만드는 사용자 이름 및 암호를 잊어버리지 않도록 주의하십시오. 기본으로 지정된 **서버 이름**을 그대로 사용해도 무방합니다.

* 데이터베이스 및 연결 문자열의 이름을 입력합니다.

> [!NOTE]
> "admin"은 관리자 사용자 이름으로 사용할 수 없습니다.

![SQL Server 구성 대화 상자](publish-to-azure-webapp-using-vs/_static/conf_servername.png)

* **확인**을 선택합니다.

Visual Studio가 **Create App Service** 대화 상자로 돌아갑니다.

* **Create App Service** 대화 상자에서 **만들기**를 선택합니다.

![SQL Database 구성 대화 상자](publish-to-azure-webapp-using-vs/_static/conf_final.png)

* **게시** 대화 상자에서 **설정** 링크를 클릭합니다.

![게시 대화 상자: 연결 패널](publish-to-azure-webapp-using-vs/_static/pubc.png)

그려면 다시 **게시** 대화 상자가 나타나는데 **설정** 페이지에서:

  * **데이터베이스**를 확장하고 **런타임에 이 연결 문자열 사용**을 선택합니다.

  * **Entity Framework 마이그레이션**을 확장하고 **게시할 때 이 마이그레이션 적용**을 선택합니다.

* **저장**을 선택합니다. 그러면 다시 Visual Studio의 **게시** 대화 상자로 돌아갑니다. 

![게시 대화 상자: 설정 패널](publish-to-azure-webapp-using-vs/_static/pubs.png)

**게시**를 클릭합니다. 그러면 Visual Studio가 앱을 Azure에 게시하고 브라우저에서 클라우드 앱을 실행합니다.

### <a name="test-your-app-in-azure"></a>Azure에서 앱 테스트하기

* **About** 링크 및 **Contact** 링크를 테스트해 봅니다.

* 새로운 사용자를 등록합니다.

![Azure App Service의 Microsoft Edge에서 열린 웹 응용 프로그램](publish-to-azure-webapp-using-vs/_static/register.png)

### <a name="update-the-app"></a>앱 수정하기

* *Pages/About.cshtml* Razor 페이지를 편집해서 내용을 변경합니다. 예를 들어, 문단을 수정해서 “Hello ASP.NET Core!”라는 문장을 표시할 수 있습니다.

    [!code-html[About](publish-to-azure-webapp-using-vs/sample/about.cshtml?highlight=9&range=1-9)]

* 다시 프로젝트를 마우스 오른쪽 버튼으로 클릭한 다음, **게시...**를 선택합니다.

![강조 표시된 게시 링크로 열린 바로 가기 메뉴](publish-to-azure-webapp-using-vs/_static/pub.png)

* 앱이 게시된 다음, 변경한 내용이 Azure에 반영되어 있는지 확인합니다.

![작업이 완료되었는지 확인합니다.](publish-to-azure-webapp-using-vs/_static/final.png)

### <a name="clean-up"></a>정리하기

앱 테스트를 완료했으면 [Azure Portal](https://portal.azure.com/)로 이동해서 앱을 삭제합니다.

* **리소스 그룹**을 선택한 다음, 본문에서 만든 리소스 그룹을 선택합니다.

![Azure Portal: 사이드바 메뉴에 있는 리소스 그룹](publish-to-azure-webapp-using-vs/_static/portalrg.png)

* **리소스 그룹** 페이지에서 **리소스 그룹 삭제**를 선택합니다.

![Azure Portal: 리소스 그룹 페이지](publish-to-azure-webapp-using-vs/_static/rgd.png)

* 리소스 그룹의 이름을 입력하고 **삭제**를 선택합니다. 그러면 본문에서 만든 앱과 다른 모든 리소스들이 Azure에서 삭제됩니다.

### <a name="next-steps"></a>다음 단계

* [Visual Studio 및 Git을 사용해서 Azure에 연속 배포하기](../publishing/azure-continuous-deployment.md)
