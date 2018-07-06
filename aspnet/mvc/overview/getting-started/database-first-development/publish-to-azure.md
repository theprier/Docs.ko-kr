---
uid: mvc/overview/getting-started/database-first-development/publish-to-azure
title: 데이터베이스에 첫 번째 MVC 사이트를 Azure에 게시 | Microsoft Docs
author: tfitzmac
description: MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여, 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다. 이 자습서 seri...
ms.author: aspnetcontent
ms.date: 12/22/2014
ms.assetid: 7131f1c1-cef3-4396-ab44-ed4519676546
msc.legacyurl: /mvc/overview/getting-started/database-first-development/publish-to-azure
msc.type: authoredcontent
ms.openlocfilehash: 0aaa8e2a586a89f6ea5eaeb4f3d280993342b2f9
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37835750"
---
<a name="publish-mvc-database-first-site-to-azure"></a>데이터베이스에 첫 번째 MVC 사이트를 Azure에 게시
====================
[Tom FitzMacken](https://github.com/tfitzmac)

> MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여, 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다. 이 자습서 시리즈에서는 자동으로 표시, 편집, 만들기, 사용자를 사용 하는 코드를 생성 하 고 데이터베이스 테이블에 있는 데이터를 삭제 하는 방법을 보여 줍니다. 생성된 된 코드는 데이터베이스 테이블의 열에 해당합니다.
> 
> 시리즈의이 부분을 Azure 웹 앱 및 데이터베이스를 게시에 중점을 둡니다. 웹 앱 및 데이터베이스를 게시 하는 방법에 대 한 자세한 하지만 실제로 자습서의 시작 부분에서 시작 해야 하는 단계를 수행 하려면이 항목을 읽을 수 있습니다. 참조 [Getting Started](setting-up-database.md)합니다.


## <a name="deploy-your-web-app-on-azure"></a>Azure에서 웹 앱 배포

이 자습서를 완료 하려면 Azure 계정이 필요 합니다.

- 할 수 있습니다 [Azure 계정을 무료로 개설](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) -크레딧을 받게 사용 하면 유료 Azure 서비스를 사용해볼 수 있습니다 하 고 사용한 후에 계정을 유지 하면 최대 사용 하 여 무료 Azure 서비스입니다.
- 할 수 있습니다 [MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) -MSDN 구독은 크레딧을 매달 제공 유료 Azure 서비스에 사용할 수 있는 합니다.

웹 앱을 게시 하려면 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다.

![사이트 게시](publish-to-azure/_static/image1.png)

Microsoft Azure 웹 사이트를 선택 합니다.

![Azure를 선택 합니다.](publish-to-azure/_static/image2.png)

Azure에 로그인 하지 않은 경우 Azure 계정 자격 증명을 제공 합니다. 새 웹 앱을 만들려면 새로 만들기를 선택 합니다.

![새 사이트](publish-to-azure/_static/image3.png)

웹 앱에 대 한 고유한 이름을 만듭니다. 이름 필드의 오른쪽에 녹색 확인 표시가 표시 되 면 이름이 고유한 알 수 있습니다. 웹 앱에 대 한 지역을 선택 합니다. 선택 **새 서버 만들기** 데이터베이스에 대해이 새 데이터베이스 서버에 대 한 사용자 이름 및 암호를 제공 합니다. 완료 되 면, 클릭 **만들기**합니다.

![사이트 만들기](publish-to-azure/_static/image4.png)

연결 값 이제 모두 완료 되었습니다. 이러한 값을 변경 되지 않은 상태로 둘 수 있습니다.

![connection](publish-to-azure/_static/image5.png)

**다음**을 클릭합니다.

설정에 대 한 알림을 두 데이터베이스 연결 된-ApplicationDBContext 및 ContosoUniversityDataEntities 합니다. ApplicationDBContext은 사용자 계정 테이블에 대 한 연결이 메시지를 표시 합니다. 이러한 값을 데이터베이스에 대 한 연결 문자열을 표시합니다. 이러한 데이터베이스에 사이트를 게시할 때는 게시 한다는 것이 아닙니다. 웹 앱 게시 후에 데이터베이스 프로젝트를 게시 합니다.

![](publish-to-azure/_static/image6.png)

데이터베이스 연결 옆에 있는 줄임표 (...) 연결 문자열의 세부 정보를 표시 합니다. ContosoUniversityDataEntities 옆의 줄임표를 클릭 합니다.

![](publish-to-azure/_static/image7.png)

데이터베이스 서버 및 데이터베이스 이름의 note 합니다. 서버 이름은 임의로 생성 됩니다. 데이터베이스 이름은 간단한 사용 하 여 사이트의 이름을  **\_db** 추가 합니다. 나중에 데이터베이스를 게시할 때 이름을 모두 해야 합니다.

클릭 **확인** 데이터베이스 연결 문자열 창을 닫습니다.

웹 게시 창에서 클릭 **다음** 미리 보기를 볼 수 있습니다.

![](publish-to-azure/_static/image8.png)

게시할 파일의 목록을 보려면 미리 보기 시작 클릭 수 있습니다. 이 사이트를 게시 한 첫 번째 시간 이므로 목록은 프로젝트의 모든 관련 파일입니다.

**게시**를 클릭합니다.

출력 창에는 게시의 결과 표시 됩니다.

![](publish-to-azure/_static/image9.png)

게시 후 사이트가 immedialely 웹 브라우저에서 시작 됩니다. 배포 된 사이트 및 사이트에 새 사용자를 등록할 수 있습니다. 그러나 ContosoUniversityData 프로젝트에 테이블 게시 되지 않은 아직 있습니다. 학생 링크 목록을 클릭 하면 오류가 발생 합니다.

## <a name="publish-database-to-sql-azure"></a>SQL Azure 데이터베이스 게시

데이터베이스를 게시 하기 전에 로컬 컴퓨터에 데이터베이스 서버에 연결할 수 있는지 확인 해야 합니다. 데이터베이스 서버용 방화벽 컴퓨터가 데이터베이스에 연결할 수는 제한 합니다. 방화벽에 대 한 허용 된 IP 주소에 컴퓨터의 IP 주소를 추가 해야 합니다.

Azure portal 통해 Azure 계정에 로그인 합니다.

새 데이터베이스를 선택 하 고 선택 **관리**합니다.

![관리](publish-to-azure/_static/image10.png)

데이터베이스 서버 컴퓨터에서 연결을 허용 하도록 구성 해야 합니다. 관리를 선택 하면 데이터베이스 서버에 허용 된 대로 현재 IP 주소를 추가 하 라는 메시지가 표시 됩니다. 예 선택 합니다.

![ip 주소 추가](publish-to-azure/_static/image11.png)

이전 단계에서 추가한 IP 주소 연결을 구성 해야 할 유일한 IP 주소가 없는 가능성이 있습니다. 연결이 제대로 설정 된 경우를 확인 하려면 데이터베이스에 로그인을 시도할 수 있습니다. 사용자 이름 및 이전에 만든 암호를 제공 합니다.

![login](publish-to-azure/_static/image12.png)

오류 메시지가 나타나면 다른 IP 주소를 추가 해야 합니다. 오류에 대 한 자세한 내용을 보려면 오류 메시지를 클릭 합니다. 세부 정보에 추가 해야 하는 IP 주소가 표시 됩니다. 이 IP 주소를 note 합니다.

![허용 되지 않음](publish-to-azure/_static/image13.png)

이 로그인 창을 닫고 Azure 포털로 돌아갑니다.

데이터베이스에 대 한 대시보드로 이동 합니다. 클릭 **허용 된 IP 주소 관리**합니다.

![ip 주소 관리](publish-to-azure/_static/image14.png)

이제 오류 메시지에서 IP 주소를 추가 해야 합니다. 오류 메시지에서 항목을 포함 하도록 허용 된 IP 주소 범위를 변경 하거나 별도 항목으로 해당 IP 주소를 추가 합니다.

![새 주소를 추가 합니다.](publish-to-azure/_static/image15.png)

허용 된 IP 주소에 변경 내용을 저장 합니다.

관리를 클릭 하 고 데이터베이스에 다시 로그인을 시도 합니다. 허용 된 IP 주소는 방화벽을 올바르게 구성 하기 전에 몇 분을 대기 해야 합니다. 데이터베이스에 로그인 할 수 있는 경우 데이터베이스에 연결 설정을 완료 했습니다.

잠시 후에 데이터베이스 배포 결과 확인 하기 때문에이 관리 창을 열어 놓을 수 있습니다.

데이터베이스 프로젝트를 반환 합니다. 프로젝트를 마우스 오른쪽 단추로 누르고 **게시**합니다.

![데이터베이스 게시](publish-to-azure/_static/image16.png)

데이터베이스 게시 창에서 선택 **편집**합니다.

![편집](publish-to-azure/_static/image17.png)

서버에 대 한 데이터베이스 서버 이름과 인증 자격 증명을 제공 합니다. 자격 증명을 입력 한 후 사용 가능한 데이터베이스 목록에서 만든 데이터베이스를 선택 합니다. Visual Studio는 기본적으로 만든 데이터베이스를 동일 않을 수도 있는 프로젝트의 이름으로 데이터베이스 필드의 이름을 설정 합니다.

![](publish-to-azure/_static/image18.png)

확인을 클릭합니다.

다시 모든 연결 정보를 입력 하지 않고 나중에 업데이트를 게시할 수 있도록이 프로필을 저장 하려면 아마도 해야 합니다. **프로필 만들기**를 선택합니다.

![프로필 저장](publish-to-azure/_static/image19.png)

라는 프로젝트에 파일을 만드는 **ContosoUniversityData.publish.xml**합니다. 데이터베이스를 Azure에 게시 하려면 다음에 해당 프로필을 로드 하면 됩니다.

이제 클릭 **게시** Azure에서 데이터베이스를 만들려고 합니다.

![게시](publish-to-azure/_static/image20.png)

한 동안 실행 한 후 게시 결과가 표시 됩니다.

![results](publish-to-azure/_static/image21.png)

이제 데이터베이스에 대 한 관리 포털에 다시 이동 수 있습니다. 디자인 뷰를 새로 고치고 미리 채워진된 데이터를 사용 하 여 3 개의 테이블을 배포한 알 수 있습니다.

![새 테이블](publish-to-azure/_static/image22.png)

이제 Azure에 배포 되는 웹 앱을 테스트할 준비가 되었습니다. Azure에서 웹 앱으로 이동 (같은 http://contosositeexample.azurewebsites.net/)합니다. 학생 목록에 대 한 링크를 클릭 하 고 학생 인덱스 뷰에 표시 됩니다.

![보기](publish-to-azure/_static/image23.png)

경우에 따라 연결 및 데이터베이스를 적절히 구성 해야 하는 데 약간의 시간만이 필요 합니다. 오류가 발생 하는 경우를 몇 분 기다린 후 다시 시도 하십시오.

## <a name="conclusion"></a>결론

이 시리즈 사용자가 편집, 업데이트, 만들기 및 데이터를 삭제할 수 있는 기존 데이터베이스에서 코드를 생성 하는 방법의 간단한 예제를 제공 합니다. ASP.NET MVC 5, Entity Framework 및 ASP.NET 스 캐 폴딩 프로젝트를 만들려면 사용 합니다.

Code First 개발을 소개 하는 예제를 보려면 [ASP.NET MVC 5 시작](../introduction/getting-started.md)합니다.

고급 예제를 보려면 [ASP.NET MVC 4 응용 프로그램에 대 한 Entity Framework 데이터 모델을 만드는](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다. Database First에서 데이터로 작업에 사용 하는 DbContext API는 동일 Code First에서 데이터로 작업 하기 위한 사용 API로 note 합니다. Database First 사용 하려는 경우에 코드 첫 번째 자습서 등에서 동시성 충돌 처리 관련된 데이터 읽기 및 업데이트와 같은 더 복잡 한 시나리오를 처리 하는 방법을 알아볼 수 있습니다. 유일한 차이점은 데이터베이스, 상황에 맞는 클래스 및 엔터티 클래스를 생성 하는 방법

> [!div class="step-by-step"]
> [이전](enhancing-data-validation.md)
