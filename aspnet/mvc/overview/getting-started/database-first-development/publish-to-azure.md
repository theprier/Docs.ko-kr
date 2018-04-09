---
uid: mvc/overview/getting-started/database-first-development/publish-to-azure
title: Azure에 데이터베이스에 첫 번째 MVC 사이트 게시 | Microsoft Docs
author: tfitzmac
description: MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다. 이 자습서 seri 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/22/2014
ms.topic: article
ms.assetid: 7131f1c1-cef3-4396-ab44-ed4519676546
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/database-first-development/publish-to-azure
msc.type: authoredcontent
ms.openlocfilehash: 839bbceba6f0e098303facd40dbb1496bd449ba3
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="publish-mvc-database-first-site-to-azure"></a>MVC 데이터베이스 첫 번째 사이트를 Azure에 게시
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

> MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다. 이 자습서 시리즈 자동으로 표시, 편집를 만들 수 있도록 하는 코드를 생성 하 고 데이터베이스 테이블에 있는 데이터를 삭제 하는 방법을 보여 줍니다. 생성 된 코드는 데이터베이스 테이블의 열에 해당합니다.
> 
> 시리즈의이 부분 웹 응용 프로그램 및 데이터베이스를 Azure에 게시에 중점을 둡니다. 웹 응용 프로그램 및 데이터베이스를 게시 하는 방법에 대 한 자세한 내용은 하지만 실제로 자습서의 시작 부분에서 시작 해야 하는 단계를 수행 하려면이 항목을 읽을 수 있습니다. 참조 [시작](setting-up-database.md)합니다.


## <a name="deploy-your-web-app-on-azure"></a>Azure에 웹 앱 배포

이 자습서를 완료 하려면 Azure 계정이 필요 합니다.

- 있습니다 수 [무료로 Azure 계정을 개설](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) -크레딧을 얻게 유료 Azure 서비스를 실행 해 사용할 수 있으며, 사용 후에 최대 계정 등에 사용 가능한 Azure 서비스입니다.
- 있습니다 수 [MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) -Your MSDN을 구독 하면 크레딧 매달 유료 Azure 서비스에 사용할 수 있습니다.

웹 앱을 게시 하려면 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다.

![사이트 게시](publish-to-azure/_static/image1.png)

Microsoft Azure 웹 사이트를 선택 합니다.

![Azure를 선택 합니다.](publish-to-azure/_static/image2.png)

Azure에 로그인 하지 않은 경우 Azure 계정 자격 증명을 제공 합니다. 새 웹 앱을 만들려면 새로 만들기를 선택 합니다.

![새 사이트](publish-to-azure/_static/image3.png)

웹 앱에 대 한 고유한 이름을 만듭니다. 이름 필드의 오른쪽에 녹색 확인 표시가 표시 이름은 고유 알 수 있습니다. 웹 앱에 대 한 지역을 선택 합니다. 선택 **새 서버 만들기** 는 데이터베이스에 대 한이 새 데이터베이스 서버에 대 한 사용자 이름 및 암호를 제공 합니다. 완료 되 면 클릭 **만들기**합니다.

![사이트 만들기](publish-to-azure/_static/image4.png)

연결 값 이제 모두 설정 됩니다. 이러한 값을 변경 되지 않은 상태로 둘 수 있습니다.

![connection](publish-to-azure/_static/image5.png)

**다음**을 클릭합니다.

설정의 경우 두 데이터베이스 연결 통지 지정-ApplicationDBContext 및 ContosoUniversityDataEntities 합니다. ApplicationDBContext은 사용자 계정 테이블에 대 한 연결입니다. 이러한 값은 데이터베이스에 대 한 연결 문자열 표시 됩니다. 사이트를 게시 하는 경우 이러한 데이터베이스 게시 될 것이 아닙니다. 웹 응용 프로그램 게시를 완료 한 후에 데이터베이스 프로젝트를 게시 합니다.

![](publish-to-azure/_static/image6.png)

데이터베이스 연결 옆에 있는 줄임표 (...)는 연결 문자열의 세부 정보를 표시 합니다. ContosoUniversityDataEntities 옆의 줄임표를 클릭 합니다.

![](publish-to-azure/_static/image7.png)

Note 데이터베이스 서버와 데이터베이스의 이름입니다. 서버 이름은 임의로 생성 됩니다. 데이터베이스 이름이 단순 이름을 사용 하 여 사이트의  **\_db** 추가 합니다. 나중에 데이터베이스에 게시할 때 두 이름이 필요 합니다.

클릭 **확인** 하 여 데이터베이스 연결 문자열 창을 닫습니다.

웹 게시 창에서 클릭 **다음** 미리 보기를 볼 수 있습니다.

![](publish-to-azure/_static/image8.png)

게시 파일의 목록을 보려면 미리 보기 시작을 클릭할 수 있습니다. 이 이므로이 사이트를 게시 한 처음으로, 목록은 프로젝트의 모든 관련 파일입니다.

**게시**를 클릭합니다.

출력 창에는 게시의 결과 표시 됩니다.

![](publish-to-azure/_static/image9.png)

를 게시 한 후 사이트가 immedialely 웹 브라우저에서 실행 됩니다. 사이트를 배포 하 고 사이트에 새 사용자를 등록할 수 있습니다. 그러나 ContosoUniversityData 프로젝트에 있는 테이블 하지 아직 게시 되었습니다. 학생 링크의 경우 목록에서 클릭 하는 경우 오류가 발생 합니다.

## <a name="publish-database-to-sql-azure"></a>SQL Azure에 데이터베이스를 게시 합니다.

데이터베이스를 게시 하기 전에 로컬 컴퓨터에서 데이터베이스 서버에 연결할 수 있는지 확인 해야 합니다. 데이터베이스 서버에 대 한 방화벽 컴퓨터가 데이터베이스에 연결할 수 있는 제한 합니다. 방화벽에 대 한 허용된 된 IP 주소에 컴퓨터의 IP 주소를 추가 해야 합니다.

Azure 포털을 통해 Azure 계정에 로그인 합니다.

새 데이터베이스를 선택 하 고 선택 **관리**합니다.

![관리](publish-to-azure/_static/image10.png)

데이터베이스 서버 컴퓨터에서 연결을 허용 하도록 구성 해야 합니다. 관리를 선택 하는 경우 데이터베이스 서버에 허용 된 경우 현재 IP 주소를 추가 하 라는 메시지가 표시 됩니다. 예를 선택 합니다.

![ip 주소 추가](publish-to-azure/_static/image11.png)

이전 단계에서 추가한 IP 주소를 연결에 대 한 구성 해야 유일한 IP 주소가 없는 가능성이 높습니다. 연결 제대로 설정 되어 있는지 확인 하는 데이터베이스에 로그인을 시도할 수 있습니다. 사용자 이름 및 앞에서 만든 암호를 제공 합니다.

![login](publish-to-azure/_static/image12.png)

오류 메시지가 표시 되 면 다른 IP 주소를 추가 해야 합니다. 오류에 대 한 자세한 내용을 보려면 오류 메시지를 클릭 합니다. 세부 정보에서를 추가 해야 하는 IP 주소를 표시 됩니다. 이 IP 주소를 note 합니다.

![허용 되지 않음](publish-to-azure/_static/image13.png)

이 로그인 창을 닫고 Azure 포털로 돌아갑니다.

데이터베이스에 대 한 대시보드로 이동 합니다. 클릭 **허용 IP 주소 관리**합니다.

![ip 주소 관리](publish-to-azure/_static/image14.png)

현재 오류 메시지에서 IP 주소를 추가 해야 합니다. 오류 메시지를 포함 하도록 허용 된 IP 주소 범위를 변경 하거나 해당 IP 주소를 별도 항목으로 추가 하십시오.

![새 주소를 추가 합니다.](publish-to-azure/_static/image15.png)

허용 된 IP 주소 변경 내용을 저장 합니다.

관리를 클릭 하 고 데이터베이스에 다시 로그인 해 보십시오. 방화벽에 대 한 허용된 된 IP 주소가 올바르게 구성 되어 되기까지 몇 분 정도 기다려야 할 수 있습니다. 데이터베이스에 성공적으로 로그인 할 수 있습니다 때 데이터베이스에 연결을 설정을 했습니다.

잠시 후에 데이터베이스 배포 결과 확인 하기 때문에이 관리 창을 열어 놓을 수 있습니다.

데이터베이스 프로젝트를 반환 합니다. 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다.

![데이터베이스 게시](publish-to-azure/_static/image16.png)

데이터베이스 게시 창에서 선택한 **편집**합니다.

![편집](publish-to-azure/_static/image17.png)

서버에 대 한 데이터베이스 서버 및 인증 자격 증명의 이름을 제공 합니다. 자격 증명을 입력 한 후 사용 가능한 데이터베이스 목록에서 이전에 만든 데이터베이스를 선택 합니다. Visual Studio는 기본적으로 만든 데이터베이스를 동일 않을 수도 있는 프로젝트의 이름으로 데이터베이스 필드의 이름을 설정 합니다.

![](publish-to-azure/_static/image18.png)

확인을 클릭합니다.

모든 연결 정보를 다시 입력 하지 않고 나중에 업데이트를 게시할 수 있도록이 프로필을 저장 하려고 할 수 있습니다. **프로필 만들기**를 선택합니다.

![프로필 저장](publish-to-azure/_static/image19.png)

이라는 프로젝트에 파일을 만드는 **ContosoUniversityData.publish.xml**합니다. 데이터베이스를 Azure에 게시 하려면 다음에 단순히 해당 프로필을 로드 합니다.

이제 클릭 **게시** Azure에서 데이터베이스를 만들려고 합니다.

![게시](publish-to-azure/_static/image20.png)

잠시 동안 실행 한 후 게시 결과가 표시 됩니다.

![results](publish-to-azure/_static/image21.png)

이제 데이터베이스에 대 한 관리 포털에 다시 이동할 수 있습니다. 디자인 보기를 새로 고 3 테이블 미리 채워진된 데이터와 함께 배포 된 확인 합니다.

![새 테이블](publish-to-azure/_static/image22.png)

이제 Azure에 배포 되는 웹 응용 프로그램을 테스트할 준비가 되었습니다. Azure에서 웹 앱으로 이동 (예: http://contosositeexample.azurewebsites.net/)합니다. 학생 목록에 대 한 링크를 클릭 하 고 학생을 위한 인덱스 보기 확인 해야 합니다.

![보기](publish-to-azure/_static/image23.png)

경우에 따라 연결 및 데이터베이스 충분 한 시간을 적절히 구성 해야 합니다. 오류가 발생 하는 경우 몇 분 정도 기다린 후 다시 시도 하십시오.

## <a name="conclusion"></a>결론

이 시리즈 사용자가 편집, 업데이트, 만들기 및 데이터를 삭제할 수 있는 기존 데이터베이스에서 코드를 생성 하는 방법의 간단한 예를 제공 합니다. 프로젝트를 만들려면 ASP.NET MVC 5, Entity Framework, ASP.NET 스 캐 폴딩을 사용 합니다.

Code First 개발의 기본 예제를 보려면 [Getting Started with ASP.NET MVC 5](../introduction/getting-started.md)합니다.

고급 예제를 보려면 [ASP.NET MVC 4 응용 프로그램에 대 한 Entity Framework 데이터 모델을 만드는](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다. Note DbContext API 첫 번째 데이터베이스의 데이터 작업에 사용 하는 첫 번째 코드에서 데이터 작업에 사용할 API와 동일 합니다. Database First 사용 하려는 경우에 코드 첫 번째 자습서에서 가져오고 동시성 충돌을 처리 관련된 데이터 읽기 및 업데이트와 같은 보다 복잡 한 시나리오를 처리 하는 방법을 배울 수 있습니다. 유일한 차이점은 데이터베이스, 컨텍스트 클래스 및 엔터티 클래스 만들어지는 방식입니다.

> [!div class="step-by-step"]
> [이전](enhancing-data-validation.md)
