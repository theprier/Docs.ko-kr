---
uid: identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory
title: "Azure Active Directory와 ASP.NET 응용 프로그램 개발 | Microsoft Docs"
author: Rick-Anderson
description: "Azure Active Directory 용 Microsoft ASP.NET 도구가 간단히 Azure에서 호스팅되는 웹 응용 프로그램에 대 한 인증을 사용 하도록 설정 합니다. Azure 인증을 사용할 수 있습니다..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/14/2014
ms.topic: article
ms.assetid: 457d7eaf-ee76-4ceb-9082-c7c1721435ad
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory
msc.type: authoredcontent
ms.openlocfilehash: 425f8edff41588db363055d166995d5f563c5a23
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="developing-aspnet-apps-with-azure-active-directory"></a>Azure Active Directory와 ASP.NET 앱 개발
====================
으로 [Rick Anderson](https://github.com/Rick-Anderson)

> Azure Active Directory를 사용 하면 간단 하 게에서 호스팅된 웹 응용 프로그램에 대 한 인증을 사용 하도록 설정에 대 한 Microsoft ASP.NET 도구 [Azure](https://www.windowsazure.com/en-us/home/features/web-sites/)합니다. Office 365 사용자 인증을 위해 조직, 온-프레미스 Active Directory에서 동기화 된 회사 계정 또는 사용자 고유의 사용자 지정 Azure Active Directory 도메인에서 만든 사용자가 Azure 인증을 사용할 수 있습니다. Windows Azure 인증을 사용 하도록 설정 단일을 사용 하 여 사용자를 인증 하는 응용 프로그램을 구성 [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) 테 넌 트입니다.
> 
>  이 자습서는 Rick Anderson에 의해 작성 되었으므로[@RickAndMSFT](https://twitter.com/#!/RickAndMSFT)


이 자습서를 사용 하 여 로그온에 대해 구성 된 ASP.NET 응용 프로그램을 만드는 방법을 보여 됩니다 [Azure Active Directory](https://msdn.microsoft.com/en-us/library/azure/mt168838.aspx) (Azure AD). 또한 현재 로그인 한 사용자에 대 한 정보에 Graph API를 호출 하는 방법과 Azure에 응용 프로그램을 배포 하는 방법을 배웁니다.

## <a name="prerequisites"></a>필수 구성 요소

1. [Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/eng/2013-downloads#d-2013-express) 또는 [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)합니다.
2. [Visual Studio 2013 업데이트 4](https://www.microsoft.com/en-us/download/details.aspx?id=44921) -업데이트 3 이상 작업이 필요 합니다.
3. Azure 계정입니다. [여기를 클릭](https://azure.microsoft.com/en-us/pricing/free-trial/) 무료 평가판 계정을 이미 있는 하지 않는 경우.

## <a name="add-a-global-administrator-to-your-active-directory"></a>Active Directory에 전역 관리자를 추가 합니다.

1. 에 로그인 하 고 [Azure 관리 포털](https://manage.windowsazure.com/)합니다.
2. 모든 Azure 계정에 포함 한 **기본 디렉터리** -을 클릭 한 다음 클릭는 **사용자** 페이지의 맨 위 탭 (아래 그림 참조).
3. 사용자를 추가 클릭 합니다.  
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image1.png)
4. 사용 하 여 새 사용자를 만들는 **전역 관리자** 역할입니다. 클릭 **사용자** 클릭 한 다음 확인 하 고 상단 메뉴에서는 **사용자 추가** 명령 모음에서 단추입니다.
5. 에 **사용자 추가** 대화 상자에서 새 사용자에 대 한 이름을 입력 한 다음 오른쪽 화살표를 클릭 합니다.  
  
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image2.png)
6. 사용자 이름을 입력 하 고 역할을 설정 **전역 관리자**합니다. 암호 복구를 위해 대체 전자 메일 주소를 필요로 하는 전역 관리자입니다. 작업을 완료 한 후 오른쪽 화살표를 클릭 합니다.  
  
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image3.png)
7. 대화 상자의 다음 페이지에서 클릭 **만들기**합니다. 임시 암호를 새 사용자에 대해 생성 되며 대화 상자에 표시 합니다.   
  
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image4.png)  
  
 암호를 저장 후 첫 번째 로그인 암호를 변경 하는 데 필요한 됩니다. 다음 그림은 새 관리자 계정을 보여 줍니다. 또한이 페이지에 표시 된 Microsoft 계정이 아닌 앱에 로그인 하려면 Azure Active Directory를 사용 해야 합니다.  
  
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image5.png)

## <a name="create-an-aspnet-application"></a>ASP.NET 응용 프로그램 만들기

다음 단계를 사용 하 여 [Visual Studio Express 2013 for Web](https://www.microsoft.com/en-us/download/details.aspx?id=40747),으로 이루어지며 [Visual Studio 2013 업데이트 3](https://www.microsoft.com/en-us/download/details.aspx?id=43721)합니다.

1. Visual Studio에서 클릭 **파일** 차례로 **새 프로젝트**합니다. 에 **새 프로젝트** 대화 상자에서 선택 하는 Visual C# 웹 왼쪽된 메뉴에서 프로젝트를 하 고 클릭 **확인**합니다. 선택을 취소 하려면는 **프로젝트에 Application Insights 추가** 않으려면 응용 프로그램에 대 한 기능입니다.
2. 에 **새 ASP.NET 프로젝트** 대화 상자에서 **MVC**, 클릭 하 고 **인증 변경**합니다.   
  
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image6.png)
3. 에 **인증 변경** 대화 상자에서 **조직 계정**합니다. 자동으로 Azure AD와 통합 하는 응용 프로그램을 구성할 수 있을 뿐 아니라 Azure AD와 응용 프로그램을 자동으로 등록 하려면이 옵션을 사용할 수 있습니다. 사용할 필요가 없습니다는 **인증 변경** 등록 하 고 있지만 응용 프로그램 구성 대화 상자를 통해 훨씬 쉬워졌습니다. Visual Studio 2012 예를 사용 하는 경우 수동으로 Azure 관리 포털에서 응용 프로그램을 등록 하 고 업데이트할 수 Azure AD와 통합 하는 구성 합니다.  
 드롭 다운 메뉴에서 선택 **클라우드-단일 조직** 및 **Single Sign On, 디렉터리 데이터 읽기**합니다. 예를 들어 (이미지에 아래)를 Azure AD 디렉터리에 대 한 도메인을 입력 합니다. *aricka0yahoo.onmicrosoft.com*, 클릭 하 고 **확인**합니다. Azure 포털에서 기본 디렉터리에 대 한 도메인 탭에서 도메인 이름을 가져올 수 있습니다 (다음 이미지 아래 참조).   
  
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image7.png)  
  
 다음 이미지는 Azure 포털에서 도메인 이름을 표시 합니다.  
  
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image8.png)  

    > [!NOTE]
    > 클릭 하 여 Azure AD에 등록 될 응용 프로그램 ID URI를 선택적으로 구성할 수 **기타 옵션**합니다. 앱 ID URI에는 Azure AD에 등록 되 고 Azure AD와 통신할 때 자체 식별을 위해 응용 프로그램에서 사용 하는 응용 프로그램에 대 한 고유 식별자입니다. 앱 ID URI 및 등록 된 응용 프로그램의 다른 속성에 대 한 자세한 내용은 참조 [이 항목](https://msdn.microsoft.com/en-us/library/azure/dn499820.aspx#BKMK_Registering)합니다. 앱 ID URI 필드 아래 확인란을 클릭 하 여 동일한 앱 ID URI를 사용 하 여 Azure AD에서 기존 등록을 덮어쓰려면 선택할 수 있습니다.
4. 클릭 한 후 **확인**, 로그인 대화 상자가 나타납니다 및 전역 관리자 계정 (Microsoft 계정이 아니라 구독에 연결 된)를 사용 하 여 로그인 해야 합니다. 이전에 새 관리자 계정을 만든 경우 암호를 변경 하 여 새 암호를 사용 하 여 다시 서명 해야 할 수 있습니다.   
  
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image9.png)
5. 성공적으로 인증 했습니다는 **새 ASP.NET 프로젝트** 인증 선택 대화 상자에 표시 됩니다 (**조직** ) 하 고 새 응용 프로그램 될 위치는 디렉터리 (등록*aricka0yahoo.onmicrosoft.com* 아래 그림 참조). 이 정보를 아래 확인란을 선택 **클라우드의 호스트에에서**합니다. 이 확인란을 선택 하는 경우 프로젝트 Azure 웹 앱으로 프로 비전 할 및 쉽게 게시에 대해 사용 하도록 설정 합니다. **확인**을 클릭합니다.   
  
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image10.png)
6. **Azure 웹 사이트 구성** 자동 생성 된 사이트 이름 및 지역을 사용 하 여 대화 상자가 표시 됩니다. 또한 note 계정 대화 상자에서에 현재 로그인 되어 있습니다. 이 계정은 Azure 구독 연결 된 하나 인지 확인 하려면 일반적으로 Microsoft 계정입니다.

    > [!NOTE]
    > 이 프로젝트는 데이터베이스가 필요합니다. 기존 데이터베이스 중 하나를 선택 하거나 새로 만듭니다 해야 합니다. 데이터베이스가 이미 프로젝트 적은 양의 인증 구성 데이터를 저장할 로컬 데이터베이스 파일을 사용 하기 때문에 필요 합니다. 응용 프로그램을 Azure 웹 사이트를 배포 하면 클라우드에서 액세스할 수 있는 하나를 선택 해야 배포에이 데이터베이스 패키지 되지 않습니다. **확인**을 클릭합니다.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image11.png)
7. 프로젝트 만들어짐 및 인증 옵션 및 웹 응용 프로그램 옵션은 자동으로 구성 되므로 프로젝트입니다. 이 프로세스가 완료 되 면 로컬 키를 눌러 프로젝트를 실행 **^ F5**합니다. 조직 계정을 사용 하 여 로그인 해야 합니다. 앞에서 만든 계정에 대 한 사용자 이름 및 암호를 입력 하 고 클릭 **로그인**합니다.   
  
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image12.png)
8. 성공적인 로그인 후 ASP.NET 사이트 페이지의 오른쪽 위 모퉁이에 사용자 이름을 표시 하 여 인증 되었습니다 표시 됩니다.  
  
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image13.png)  
  
 오류가 표시될 경우:  
 값은 null 이거나 비워 둘 수 없습니다. 매개 변수 이름: linkText   
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image14.png)  
  
 참조는 [디버그](#dbg) 자습서의 마지막 부분에 있습니다.

## <a name="basics-of-the-graph-api"></a>Graph API의 기본 사항

[Graph API](https://msdn.microsoft.com/en-us/library/azure/hh974476.aspx) 는 Azure AD 디렉터리의 CRUD 및 개체에 다른 작업을 수행 하는 데 프로그래밍 인터페이스입니다. Visual Studio 2013에서 새 프로젝트를 만들 때 인증에 대 한 조직 계정 옵션을 선택 하는 경우 응용 프로그램 이미 Graph API를 호출 하 여 구성 됩니다. 이 섹션 간단 하 게에서는 Graph API의 작동 방식입니다.

1. 실행 중인 응용 프로그램에서 맨 위쪽에 로그인 한 사용자의 이름을 클릭 페이지의 오른쪽입니다. 이 홈 컨트롤러에 대 한 작업은 사용자 프로필 페이지로 이동 합니다. 앞에서 만든 관리자 계정에 대 한 사용자 정보 테이블에 포함 되어 있음을 알 수 있습니다. 이 정보는 디렉터리에 저장 됩니다 및 Graph API는 페이지가 로드 될 때이 정보를 검색 하기 위해 호출 됩니다.   
  
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image15.png)
2. Visual Studio로 다시 이동 하 고 확장 하 고는 **컨트롤러** 폴더를 연 후는 **HomeController.cs** 파일입니다. 표시는 **UserProfile()** 토큰을 검색 한 다음 Graph API를 호출 하는 코드를 포함 하는 작업입니다. 이 코드는 아래 중복 됩니다. 

    [!code-csharp[Main](developing-aspnet-apps-with-windows-azure-active-directory/samples/sample1.cs?highlight=22)]

    Graph API를 호출 하려면 먼저 토큰 검색 해야 합니다. 토큰을 검색할 때 해당 문자열 값이 Graph API에 대 한 모든 후속 요청에 대 한 인증 헤더에 추가 해야 합니다. 위의 코드의 대부분을 토큰을 가져와서 Azure AD에 인증 하 고, 토큰을 사용 하 여 Graph API를 호출 하려면, 보기에 표시 될 수 있도록 응답을 변형 한 다음 세부 정보를 처리 합니다.

    에 대 한 토론 관련성이 가장 높은 부분은 다음 강조 표시 된 줄: `UserProfile profile = JsonConvert.DeserializeObject<UserProfile>(responseString);`합니다. 이 줄에서는 JSON 응답에서 deserialize 될 수 있으며, 보기에서 제공 하는 사용자의 이름을 나타냅니다.

    HttpClient를 사용 하 여 Graph API를 호출 하 고 원시 데이터를 직접 처리할 수 있지만 있는 더욱 손쉬운 방법을 사용 하는 것은 [NuGet을 통해 사용할 수 있는 그래프 클라이언트 라이브러리](http://www.nuget.org/packages/Microsoft.Azure.ActiveDirectory.GraphClient/)합니다. 클라이언트 라이브러리는 원시 HTTP 요청 및, 반환된 된 데이터의 변환을 처리 하 고 Graph api는.NET 환경에서 작업 하기 쉽게 있습니다. 에 관련된 그래프 API 코드 예제를 참조 하십시오. [GitHub 합니다.](https://github.com/AzureADSamples)

## <a name="deploy-the-application-to-azure"></a>Azure 응용 프로그램 배포

다음 단계에서는 Azure에 응용 프로그램을 배포 하는 방법을 설명 합니다. 이전 단계에서 몇 개의 단계에서 게시 될 준비가 이므로 Azure에서 웹 앱과 새 프로젝트를 연결 합니다.

1. Visual Studio에서 단추로 클릭 하 여 프로젝트 고 **게시**합니다. **웹 게시** 대화 상자가 이미 구성 된 각 설정으로 표시 됩니다. 클릭는 **다음** 이동 하는 **설정을** 페이지. 인증 하 라는 메시지가 표시 될 수 있습니다. Azure 구독 계정 (일반적으로 Microsoft 계정) 및 이전에 만든 조직 계정이 아닌를 사용 하 여 인증할 수 있는지 확인 합니다.  
  
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image16.png)
2. 확인 된 **조직 인증을 사용 하도록 설정** 옵션입니다. 에 **도메인** 필드에서 디렉터리에 대 한 도메인을 입력 합니다. **액세스 수준을** 드롭다운 목록에서 선택 **Single Sign On, 디렉터리 데이터 읽기**합니다. 사용 하 고 이전 데이터베이스에 이미 채워져 있는지 알 수는 **데이터베이스** 섹션. **게시**를 클릭합니다.  
  
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image17.png)
3. Visual Studio는 웹 사이트의 배포를 시작 하 고 새 브라우저 창이 표시 됩니다. 디렉터리에 다시 인증 하 라는 메시지가 표시 될 수 있습니다. 인증을 수행한, Azure에서 새로 게시 된 웹 사이트에 리디렉션됩니다 합니다.  
  
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image18.png)

<a id="dbg"></a>
## <a name="debugging-the-app"></a>응용 프로그램 디버깅

다음과 같은 오류가 발생 하면:   
 값은 null 이거나 비워 둘 수 없습니다. 매개 변수 이름: linkText   
   
![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image19.png)  
  

코드는 *Views\Shared\\_LoginPartial.cshtml* 다음 파일:

[!code-cshtml[Main](developing-aspnet-apps-with-windows-azure-active-directory/samples/sample2.cshtml?highlight=1-8,15-16)]

앱을 실행 한 후 "Null 사용자"를 표시 하는 로그인된 한 사용자를 로그 아웃 하 고 앞에서 만든 Active Directory 계정으로 다시 로그인 합니다.

따라야 하는 뛰어난 자습서는 Rick Rainey [심층 분석: Azure 웹 사이트 및 Azure AD를 사용 하 여 조직의 인증](http://rickrainey.com/2014/08/19/deep-dive-azure-websites-and-organizational-authentication-using-azure-ad/)합니다.

## <a name="more-information"></a>추가 정보

- [심층 분석: Azure 웹 사이트와 Azure AD를 사용 하 여 조직의 인증](http://rickrainey.com/2014/08/19/deep-dive-azure-websites-and-organizational-authentication-using-azure-ad/)
- [Azure AD 그래프 API 개요](https://msdn.microsoft.com/en-us/library/azure/hh974476.aspx)
- [Azure AD의 인증 시나리오](https://msdn.microsoft.com/en-us/library/azure/dn499820.aspx)
- [GitHub의 azure AD 코드 샘플](https://github.com/AzureADSamples)
