---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-your-site-using-visual-studio-cs
title: Visual Studio (C#)를 사용 하 여 사이트를 배포 합니다. | Microsoft Docs
author: rick-anderson
description: Visual Studio에는 웹 사이트를 배포 하기 위한 도구가 포함 됩니다. 이 자습서에서는 이러한 도구에 대 한 자세한 정보를 알아봅니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/01/2009
ms.topic: article
ms.assetid: cde4ee53-a5d0-4937-a54b-67877e8266c3
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-your-site-using-visual-studio-cs
msc.type: authoredcontent
ms.openlocfilehash: d549c615ea822d58ae71876ff3acd28c5f773d8a
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37399762"
---
<a name="deploying-your-site-using-visual-studio-c"></a>Visual Studio (C#)를 사용 하 여 사이트 배포
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/4/5/F/45F815EC-8B0E-46D3-9FB8-2DC015CCA306/ASPNET_Hosting_Tutorial_04_CS.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial04_DeployingViaVS_cs.pdf)

> Visual Studio에는 웹 사이트를 배포 하기 위한 도구가 포함 됩니다. 이 자습서에서는 이러한 도구에 대 한 자세한 정보를 알아봅니다.


## <a name="introduction"></a>소개

이전 자습서는 웹 호스트 공급자에 간단한 ASP.NET 웹 응용 프로그램을 배포 하는 방법을 살펴보았습니다. 특히 자습서 FileZilla 같은 FTP 클라이언트를 사용 하 여 개발 환경에서 프로덕션 환경에 필요한 파일을 전송 하는 방법을 보여 줬습니다. 또한 visual Studio는 웹 호스트 공급자는 배포를 용이 하 게 기본 제공 도구를 제공 합니다. 이 자습서에서는 이러한 두 도구를 검토 합니다: FTP 또는 FrontPage Server Extensions;를 사용 하 여 원격 웹 서버에서 파일을 이동할 수 있는 웹 사이트 복사 도구 와 전체 웹 사이트를 지정 된 위치로 복사 하는 게시 도구를 지정 합니다.


> [!NOTE]
> Visual Studio에서 제공 하는 기타 배포 관련 도구 포함 [웹 설치 프로젝트](https://msdn.microsoft.com/library/wx3b589t.aspx) 하 고 [웹 배포 프로젝트](https://www.microsoft.com/downloads/details.aspx?FamilyId=0AA30AE8-C73B-4BDD-BB1B-FE697256C459&amp;displaylang=en) 추가 합니다. 웹 설치 프로젝트에는 웹 사이트의 콘텐츠 및 구성 정보를 단일 MSI 파일로 패키지 합니다. 이 옵션은 고객은 자신의 웹 서버에 설치 하는 미리 패키지 된 웹 응용 프로그램을 판매 하는 회사 또는 인트라넷 내에서 배포 된 웹 사이트에 대 한 가장 유용 합니다. 웹 배포 프로젝트 추가 기능에서 Visual Studio에서 추가 기능을 지정 하 여 구성 차이 원활 하 게 개발 환경 및 프로덕션 환경에 대 한 빌드 됩니다. 이 자습서 시리즈; 웹 설치 프로젝트를 다루지 않습니다. 웹 배포 프로젝트에 요약 되어는 [ *일반적인 구성 차이 간의 개발 및 프로덕션* ](common-configuration-differences-between-development-and-production-cs.md) 자습서입니다.


## <a name="deploying-your-site-using-the-copy-web-site-tool"></a>웹 사이트 복사 도구를 사용 하 여 사이트 배포

Visual Studio의 웹 사이트 복사 도구는 독립 실행형 FTP 클라이언트 비슷합니다 기능. 간단히 말해 웹 사이트 복사 도구를 사용 하 원격 웹 사이트 FTP 또는 FrontPage Server Extensions를 통해 연결할 수 있습니다. 두 창으로 구성 되어 FileZilla의 사용자 인터페이스와 마찬가지로 웹 사이트 복사 사용자 인터페이스: 왼쪽된 창의 오른쪽 창에 대상 서버에서 해당 파일을 나열 하는 동안 로컬 파일을 나열 합니다.

> [!NOTE]
> 웹 사이트 복사 도구만 웹 사이트 프로젝트에 대 한 제공 됩니다. Visual Studio는 웹 응용 프로그램 프로젝트를 사용 하는 경우이 도구를 제공 합니다.

서적 검토 응용 프로그램을 프로덕션에 게시를 웹 사이트 복사 도구를 사용 하 여 살펴보겠습니다. 웹 사이트 복사 도구는 웹 사이트 프로젝트 모델을 사용 하는 프로젝트와만 작동 하기 때문에 수만 살펴봅니다 BookReviewsWSP 프로젝트와 함께이 도구를 사용 합니다. 해당 프로젝트를 엽니다.

(그림 1에는이 아이콘은 원으로 표시)의 솔루션 탐색기에서 웹 사이트 복사 아이콘을 클릭 하 여 웹 사이트 복사 도구 프로젝트를 시작 합니다. 또는 웹 사이트 메뉴에서 웹 사이트 복사 옵션을 선택할 수 있습니다. 그림 1에 표시 된 웹 사이트 복사 사용자 인터페이스를 시작 하는 방법 중 하나 그림 1의 왼쪽된 창에만 원격 서버에 연결할 아직 때문에 채워집니다.


[![웹 사이트 복사 도구의 사용자 인터페이스는 두 개의 창으로 구분](deploying-your-site-using-visual-studio-cs/_static/image2.png)](deploying-your-site-using-visual-studio-cs/_static/image1.png)

**그림 1**:의 웹 사이트 복사 도구의 사용자 인터페이스는 두 개의 창으로 나뉩니다 ([큰 이미지를 보려면 클릭](deploying-your-site-using-visual-studio-cs/_static/image3.png))


사이트를 배포 하려면 먼저 웹 호스트 공급자에 연결 해야 합니다. 웹 사이트 복사 사용자 인터페이스의 맨 위에 있는 연결 단추를 클릭 합니다. 이 그림 2에 표시 된 웹 사이트 열기 대화 상자를 표시 합니다.

왼쪽에서 네 가지 옵션 중 하나를 선택 하 여 대상 웹 사이트에 연결할 수 있습니다.

- **파일 시스템** -컴퓨터에서 액세스할 수 있는 폴더 또는 네트워크 공유에 사이트를 배포 하려면이 옵션을 선택 합니다.
- **로컬 IIS** -컴퓨터에 설치 된 IIS 웹 서버에 사이트를 배포 하려면이 옵션을 사용 합니다.
- **FTP 사이트** -FTP를 사용 하 여 원격 웹 사이트에 연결 합니다.
- **원격 사이트** -FrontPage Server Extensions를 사용 하 여 원격 웹 사이트에 연결 합니다.

대부분의 웹 호스트 공급자를 FTP 지원 없지만 적은 FrontPage 서버 확장이 지원 됩니다. 이런 이유로 FTP 사이트 옵션을 선택 하 고 그림 2에 표시 된 대로 연결 정보를 입력 했습니다.


[![대상 웹 사이트를 지정 합니다.](deploying-your-site-using-visual-studio-cs/_static/image5.png)](deploying-your-site-using-visual-studio-cs/_static/image4.png)

**그림 2**: 대상 웹 사이트를 지정 ([큰 이미지를 보려면 클릭](deploying-your-site-using-visual-studio-cs/_static/image6.png))


웹 사이트 복사 도구에 연결한 후 오른쪽 창에서 원격 사이트의 파일을 로드 하 고 각 파일의 상태를 나타냅니다: 새 삭제, 변경, 또는 Unchanged 합니다. 원격 사이트 또는 그 반대로는 로컬 사이트에서 파일을 복사할 수 있습니다.

새를 추가 해 보겠습니다 BookReviewsWSP 프로젝트에 페이지를 실행 중인 웹 사이트 복사 도구 볼 수 있도록 배포입니다. 명명 된 루트 디렉터리에서 Visual Studio에서 새 ASP.NET 페이지를 만들 `Privacy.aspx`합니다. 마스터 페이지를 사용 하 여 페이지가 `Site.master` 사이트의 개인 정보 취급 방침이이 페이지에 추가 합니다. 그림 3에서는이 페이지는 만들어진 후 Visual Studio를 보여 줍니다.


[![명명 된 새 페이지 추가 &lt;코드&gt;Privacy.aspx&lt;/c o d&gt; 웹 사이트의 루트 폴더에](deploying-your-site-using-visual-studio-cs/_static/image8.png)](deploying-your-site-using-visual-studio-cs/_static/image7.png)

**그림 3**: 명명 된 새 페이지 추가 `Privacy.aspx` 웹 사이트의 루트 폴더 ([클릭 하 여 큰 이미지 보기](deploying-your-site-using-visual-studio-cs/_static/image9.png))


다음으로, 웹 사이트 복사 사용자 인터페이스를 반환 합니다. 왼쪽된 창에 이제 새 파일-그림 4에서 알 수 있듯이 `Policy.aspx` 고 `Policy.aspx.cs`입니다. 게다가 이러한 파일은와 상태의 새 원격 사이트에는 없지만 로컬 사이트에 있는지를 나타내는 화살표 아이콘으로 표시 됩니다.


[![새로 만들기를 포함 하는 웹 사이트 복사 도구 &lt;코드&gt;Privacy.aspx&lt;/c o d&gt; 페이지의 왼쪽 창에서](deploying-your-site-using-visual-studio-cs/_static/image11.png)](deploying-your-site-using-visual-studio-cs/_static/image10.png)

**그림 4**: 새로 만들기를 포함 하는 웹 사이트 복사 도구 `Privacy.aspx` 페이지의 왼쪽 창에서 ([클릭 하 여 큰 이미지 보기](deploying-your-site-using-visual-studio-cs/_static/image12.png))


새 배포에 파일을 모두 선택 하 고 원격 사이트로 전송할 화살표 아이콘을 클릭 합니다. 전송이 완료 된 후 합니다 `Policy.aspx` 및 `Policy.aspx.cs` Unchanged 상태를 사용 하 여 로컬 및 원격 사이트에 있는 파일입니다.

새 파일을 나열할 함께 웹 사이트 복사 도구는 로컬 및 원격 사이트 간의 다른 모든 파일을 강조 표시 합니다. 이 실행 중인 확인 하려면 돌아갑니다는 `Privacy.aspx` 페이지 및 개인 정보 취급 방침에 몇 가지 단어를 추가 합니다. 페이지를 저장 하 고 웹 사이트 복사 도구를 반환 합니다. 그림 5에서 알 수 있듯이는 `Privacy.aspx` 페이지 왼쪽된 창에서 변경 된 원격 사이트와 동기화 중임을 나타내는 상태가 됩니다.


[![나타내는 웹 사이트 복사 도구를 &lt;코드&gt;Privacy.aspx&lt;/c o d&gt; 페이지 바뀌었습니다.](deploying-your-site-using-visual-studio-cs/_static/image14.png)](deploying-your-site-using-visual-studio-cs/_static/image13.png)

**그림 5**: 웹 사이트 복사 도구 나타냅니다는 `Privacy.aspx` 페이지가 변경 되었습니다 ([클릭 하 여 큰 이미지 보기](deploying-your-site-using-visual-studio-cs/_static/image15.png))


웹 사이트 복사 도구는 또한 파일을 마지막 복사 작업 이후 삭제 된 경우 나타냅니다. 삭제 된 `Privacy.aspx` 로컬 프로젝트에서 새로 고침 웹 사이트 복사 도구입니다. 합니다 `Privacy.aspx` 및 `Privacy.aspx.cs` 파일 왼쪽된 창에 나열 된 상태로 유지 되지만 삭제 됨 상태의 마지막 복사 작업 이후 제거 된 나타내는입니다.

## <a name="publishing-a-web-application"></a>웹 응용 프로그램 게시

Visual Studio 내에서 웹 응용 프로그램을 배포 하는 또 다른 방법은 빌드 메뉴를 통해 액세스할 수 있는 게시 옵션을 사용 하는 것입니다. 게시 옵션을 명시적으로 응용 프로그램을 컴파일하고 및 모든 지정된 된 원격 사이트까지 필요한 파일을 복사 합니다. 앞으로 살펴보겠지만 곧, 게시 옵션 웹 사이트 복사 도구 보다 더 대략적인입니다. 웹 사이트 복사 도구는 로컬 및 원격 사이트에서 파일을 검사할 수 있습니다 하 고 업로드 하거나 필요에 따라 개별 파일을 다운로드할 수 있습니다, 게시 옵션은 전체 웹 응용 프로그램을 배포 합니다.


지정된 된 원격 사이트에 필요한 파일을 모두 복사 하는 것 외에도 게시 옵션을 명시적으로 응용 프로그램을 컴파일합니다. 해야 할 웹 응용 프로그램 프로젝트는 컴파일된 명시적으로 가져와야 게시 옵션은 웹 응용 프로그램 프로젝트에 사용할 수 있는 놀라운 일이 아닙니다. 다소 놀라울 수 있지만 어떤 게시 옵션 웹 사이트 프로젝트에 대 한 사용 가능한도 된다는 것입니다. 설명한 대로 합니다 [ *결정 파일이 필요한 배포* ](determining-what-files-need-to-be-deployed-cs.md) 라고 하는 프로세스를 통해 명시적으로 컴파일할 수 있는 자습서에서는 웹 사이트 프로젝트 *미리 컴파일*. 게시 옵션을 사용 하 여 웹 응용 프로그램 프로젝트를 사용 하 여에 중점을 두고이 자습서 이후 자습서 미리 컴파일을, 이때 돌아가 게시 옵션을 사용 하 여 웹 사이트 프로젝트와 함께 검색할 살펴봅니다.

> [!NOTE]
> 게시 옵션은 웹 사이트 프로젝트와 웹 응용 프로그램 프로젝트에 대 한 Visual Studio에서 사용할 수 있는, Visual Web Developer만 웹 응용 프로그램 프로젝트에 대 한 게시 옵션을 제공 합니다.


게시 옵션을 사용 하 여도 서 리뷰 응용 프로그램 배포에 대해 살펴보겠습니다. Visual Studio에서 BookReviewsWAP (웹 응용 프로그램 프로젝트)을 열어 시작 합니다. 게시 메뉴에서 빌드 BookReviewsWAP 프로젝트를 선택 합니다. 이 다른 구성 옵션 (그림 6 참조) 중 대상 위치를 묻는 대화 상자가 나타납니다. 훨씬 같은 웹 사이트 복사 도구를 사용 하 여 입력할 수 있습니다 로컬 폴더, 로컬 iis 웹 사이트, FrontPage Server Extensions, 또는 FTP 서버 주소는 지원 되는 원격 웹 사이트를 가리키는 위치. 배포 된 파일을 사용 하 여 원격 웹 서버에서 파일을 대체할 것인지 아니면 모든 게시 하기 전에 원격 사이트에서 콘텐츠를 삭제 하려면 선택할 수 있습니다. 복사할지 여부를 지정할 수 있습니다.

- 만 불필요 한 소스 코드 및 프로젝트 관련 파일을 생략 하는 응용 프로그램을 실행 하는 데 필요한 프로젝트의 파일입니다.
- 모든 소스 코드 파일을 포함 하는 프로젝트 파일을 Visual Studio 프로젝트 파일과 같은 솔루션 파일입니다.
- 프로젝트에 포함 되는지 여부에 관계 없이 원본 프로젝트 폴더의 모든 파일을 복사 하는 소스 프로젝트 폴더의 모든 파일.

콘텐츠를 업로드 하는 옵션이 이기도 합니다 `App_Data` 폴더입니다.


[![대상 웹 사이트를 지정 합니다.](deploying-your-site-using-visual-studio-cs/_static/image17.png)](deploying-your-site-using-visual-studio-cs/_static/image16.png)

**그림 6**: 대상 웹 사이트를 지정 ([큰 이미지를 보려면 클릭](deploying-your-site-using-visual-studio-cs/_static/image18.png))


서적 검토 응용 프로그램에 대 한 원격 사이트는 웹 사이트 복사 도구를 통해 BookReviewsWSP 프로젝트를 복사 하는 경우에 배포 된 파일을 포함 합니다. 따라서 모든 기존 콘텐츠를 삭제 하 여 시작 된 게시 옵션을 보겠습니다. 또한 방금 복사 불필요 한 소스 코드 및 프로젝트 파일을 사용 하 여 프로덕션 환경 어지럽히지 하는 것이 아니라 필요한 파일입니다. 이러한 옵션을 지정한 후 게시 단추를 클릭 합니다. 다음 몇 초 동안 Visual Studio는 필요한 파일을 배포 대상 사이트에서 출력 창에 진행률을 표시 합니다.

그림 7에서는 게시 작업이 완료 된 후 FTP 사이트에 있는 파일을 보여 줍니다. 태그 페이지만 및는 필요한 서버 및 클라이언트 쪽 지원 파일 업로드 되었습니다.


[![필요한 파일만 프로덕션 환경에 게시 된](deploying-your-site-using-visual-studio-cs/_static/image20.png)](deploying-your-site-using-visual-studio-cs/_static/image19.png)

**그림 7**:만 필요한 파일 게시 된 프로덕션 환경으로 ([큰 이미지를 보려면 클릭](deploying-your-site-using-visual-studio-cs/_static/image21.png))


게시 옵션에는 웹 사이트 복사 도구 보다 덜 미묘한 도구입니다. 웹 사이트 복사 도구를 사용 하면 로컬 및 원격 사이트에서 파일을 검사 하 고 서로 어떻게 볼 수 있습니다, 있지만 게시 옵션 없는 이러한 인터페이스를 제공 합니다. 또한 웹 사이트 복사 도구를 사용 하 일회용 변경, 업로드 또는 개별 파일을 삭제 수 있습니다. 게시 옵션에는 이러한 세밀 하 게 제어할; 없도록 합니다. 게시 하는 대신 합니다 *전체* 응용 프로그램입니다. 이 동작에 해당 장점 및 단점이 있습니다. 더하기 측에서 중요 한 파일을 업로드 하지 않았기 때문 없습니다 게시 옵션을 사용 하면 알 수 있습니다. 하지만 작은 변화는 매우 큰 웹 사이트에 대 한 게시 옵션을 사용 하 여 해당 페이지로 사용할지 두 개의 수정 된 업데이트할 수 없습니다 되지만 Visual Studio 전체 사이트를 배포 하는 동안 대기 해야 대신 어떤 일이 생기는 것이 좋습니다.

특정 파일 내용이 프로덕션 환경과 개발 환경 간에 다른 경우도 일반적이 지 않은 것입니다. 주요 예제는 응용 프로그램의 구성 파일인 `Web.config`합니다. 게시 옵션 맹목적으로 웹 응용 프로그램 파일을 복사 하기 때문에 프로덕션 환경의 사용자 지정된 구성 파일 개발 환경에서 버전으로 덮어씁니다. 후속 자습서에서는이 항목을 추가 하 고 이러한 차이점이 존재 하는 경우 웹 응용 프로그램을 배포 하기 위한 팁을 제공 합니다.

## <a name="summary"></a>요약

웹 사이트 배포에서는 개발 환경에서 프로덕션 환경에 필요한 파일을 복사 합니다. 이전 자습서에는 같은 FileZilla는 FTP 클라이언트를 사용 하 여 파일을 전송 하는 방법을 보여 주었습니다. 이 자습서는 Visual Studio의 두 가지 배포 도구를 검사 합니다: 웹 사이트 복사 도구 및 게시 옵션입니다. 웹 사이트 복사 도구는 로컬 컴퓨터와 쉽게 두 컴퓨터 간에 파일을 업로드 하거나 다운로드할는 지정된 된 원격 컴퓨터에 파일을 나열 하는 두 개의 창이 인터페이스에는 FTP 클라이언트와 비슷합니다. 게시 옵션에는 명시적으로 프로젝트를 컴파일 및 다음 지정된 된 대상에 전체 응용 프로그램을 배포 하는 보다 대략적인 도구입니다.

즐거운 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [웹 사이트 복사 도구를 사용 하 여 웹 사이트 복사](https://msdn.microsoft.com/library/1cc82atw.aspx)
- [I: 웹 사이트 복사 도구를 사용 하 여 웹 사이트 배포](../../../videos/how-do-i/how-do-i-deploy-a-web-site-using-the-copy-web-site-tool.md) (비디오)
- [방법: 웹 응용 프로그램 프로젝트 게시](https://msdn.microsoft.com/library/aa983453.aspx)
- [방법: 웹 사이트 게시](https://msdn.microsoft.com/library/20yh9f1b.aspx)
- [설치 및 Visual Studio에서 배포 프로젝트](https://msdn.microsoft.com/library/wx3b589t.aspx)

> [!div class="step-by-step"]
> [이전](deploying-your-site-using-an-ftp-client-cs.md)
> [다음](common-configuration-differences-between-development-and-production-cs.md)
