---
uid: web-api/overview/mobile-clients/calling-web-api-from-a-windows-phone-8-application
title: "8 응용 프로그램 (C#)는 Windows Phone에서 웹 API를 호출 | Microsoft Docs"
author: rmcmurray
description: "Windows Phone 8 응용 프로그램에는 책의 카탈로그를 제공 하는 ASP.NET Web API 응용 프로그램으로 구성 된 전체 종단 간 시나리오를 만듭니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/09/2013
ms.topic: article
ms.assetid: b9775f41-352a-4f82-baa6-23e95b342e20
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/mobile-clients/calling-web-api-from-a-windows-phone-8-application
msc.type: authoredcontent
ms.openlocfilehash: 2025f31f369153b93cd293884880c97635fc8ab8
ms.sourcegitcommit: 016f4d58663bcd442930227022de23fb3abee0b3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/12/2018
---
<a name="calling-web-api-from-a-windows-phone-8-application-c"></a>Windows Phone 8 응용 프로그램 (C#)에서 Web API를 호출합니다.
====================
으로 [Robert McMurray](https://github.com/rmcmurray)

이 자습서에서는 Windows Phone 8 응용 프로그램에는 책의 카탈로그를 제공 하는 ASP.NET Web API 응용 프로그램으로 구성 된 전체 종단 간 시나리오를 만드는 방법에 설명 합니다.

### <a name="overview"></a>개요

ASP.NET Web API와 같은 rESTful 서비스 서버 쪽 및 클라이언트 쪽 응용 프로그램에 대 한 아키텍처를 추출 하 여 HTTP 기반 응용 프로그램 개발자를 위한 만들기 과정을 간소화 합니다. 통신에 대 한 소유 소켓 기반 프로토콜을 만들지 않고 웹 API를 개발자가 단순히 게시 해야 해당 응용 프로그램에 대 한 필수 HTTP 메서드 (예: GET, POST, PUT, DELETE), 클라이언트 응용 프로그램 개발자는만 사용 해야 하 고 응용 프로그램에 필요한 HTTP 메서드.

이 종단 간 자습서에서는 다음 프로젝트를 만드는 웹 API를 사용 하는 방법을 배웁니다.

- 에 [이 자습서의 첫 번째 부분](#STEP1)를 지 원하는 모든 만들기, 읽기, 업데이트 및 삭제 (CRUD) 작업 책 카탈로그를 관리 하는 ASP.NET Web API 응용 프로그램을 만듭니다. 이 응용 프로그램에서 사용 된 [샘플 XML 파일 (books.xml)](https://msdn.microsoft.com/library/windows/desktop/ms762271.aspx) MSDN에서.
- 에 [이 자습서의 두 번째 부분](#STEP2), Web API 응용 프로그램에서 데이터를 검색 하는 대화형 Windows Phone 8 응용 프로그램을 만듭니다.

#### <a name="prerequisites"></a>필수 구성 요소

- Windows Phone 8 SDK가 설치 된 visual Studio 2013
- Windows 8 또는 나중에 Hyper-v 설치와 함께 64 비트 시스템
- 목록이 추가 요구 사항에 대 한 참조는 *시스템 요구 사항* 섹션에서 [Windows Phone SDK 8.0](https://www.microsoft.com/download/details.aspx?id=35471) 페이지를 다운로드 합니다.

> [!NOTE]
> Web API 및 로컬 시스템에서 Windows Phone 8 프로젝트 간의 연결을 테스트 하려는 경우의 지침에 따라 해야 합니다는  *[로컬 웹 API 응용 프로그램에 연결 하는 Windows Phone 8 에뮬레이터 컴퓨터](https://go.microsoft.com/fwlink/?LinkId=324014)*  테스트 환경의를 설정 하는 문서입니다.


<a id="STEP1"></a>
### <a name="step-1-creating-the-web-api-bookstore-project"></a>1 단계: 웹 API Bookstore 프로젝트 만들기

이 종단 간 자습서의 첫 번째 단계는 모든; CRUD 작업을 지 원하는 웹 API 프로젝트를 만들려면 에이 솔루션에서 Windows Phone 응용 프로그램 프로젝트를 추가할 됩니다 [2 단계](#STEP2) 이 자습서의 합니다.

1. 열기 **Visual Studio 2013**합니다.
2. 클릭 **파일**, 다음 **새**, 차례로 **프로젝트**합니다.
3. 경우는 **새 프로젝트** 대화 상자가 표시 됩니다, 확장 **설치 됨**, 다음 **템플릿**, 다음 **Visual C#**, 차례로 **웹**합니다.

    | [![](calling-web-api-from-a-windows-phone-8-application/_static/image2.png)](calling-web-api-from-a-windows-phone-8-application/_static/image1.png) |
    | --- |
    | 확장 하는 이미지를 클릭 합니다. |
4. 강조 표시 **ASP.NET 웹 응용 프로그램**, 입력 **BookStore** 프로젝트 이름과 클릭 한 다음에 대 한 **확인**합니다.
5. 경우는 **새 ASP.NET 프로젝트** 대화 상자가 표시 됩니다, 선택는 **웹 API** 템플릿과 클릭 **확인**합니다.

    | [![](calling-web-api-from-a-windows-phone-8-application/_static/image4.png)](calling-web-api-from-a-windows-phone-8-application/_static/image3.png) |
    | --- |
    | 확장 하는 이미지를 클릭 합니다. |
6. 웹 API 프로젝트를 열 때 프로젝트에서 샘플 컨트롤러를 제거 합니다.

    1. 확장 된 **컨트롤러** 솔루션 탐색기에서 폴더입니다.
    2. 마우스 오른쪽 단추로 클릭는 **ValuesController.cs** 파일을 선택한 다음 클릭 **삭제**합니다.
    3. 클릭 **확인** 삭제를 확인 하 라는 메시지가 나타나면 합니다.
7. 웹 API 프로젝트; XML 데이터 파일 추가 이 파일의 bookstore 카탈로그 내용이 포함 되어 있습니다.

    1. 마우스 오른쪽 단추로 클릭는 **앱\_데이터** 솔루션 탐색기에서 폴더를 클릭 한 다음 **추가**, 클릭 하 고 **새 항목**합니다.
    2. 경우는 **새 항목 추가** 대화 상자가 표시 됩니다, 강조 표시는 **XML 파일** 템플릿.
    3. 파일 이름을 **Books.xml**, 클릭 하 고 **추가**합니다.
    4. 경우는 **Books.xml** 파일을 열, 파일의 코드 샘플에서 XML로 바꿉니다 **books.xml** msdn 파일: 

        [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample1.xml)]
    5. 저장 하 고 XML 파일을 닫습니다.
8. 웹 API 프로젝트; bookstore 모델 추가 이 모델 bookstore 응용 프로그램에 대 한 만들기, 읽기, 업데이트 및 삭제 (CRUD) 논리를 포함합니다.

    1. 마우스 오른쪽 단추로 클릭는 **모델** 솔루션 탐색기에서 폴더를 클릭 한 다음 **추가**, 클릭 하 고 **클래스**합니다.
    2. 경우는 **새 항목 추가** 대화 상자가 표시 됩니다, 클래스 파일의 이름을 **BookDetails.cs**, 클릭 하 고 **추가**합니다.
    3. 경우는 **BookDetails.cs** 파일을 열, 파일의 코드를 다음과 같이 바꿉니다. 

        [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample2.cs)]
    4. 저장 하 고 닫습니다는 **BookDetails.cs** 파일입니다.
9. Bookstore 컨트롤러 웹 API 프로젝트에 추가 합니다.

    1. 마우스 오른쪽 단추로 클릭는 **컨트롤러** 솔루션 탐색기에서 폴더를 클릭 한 다음 **추가**, 클릭 하 고 **컨트롤러**합니다.
    2. 때는 **추가 스 캐 폴드** 대화 상자가 표시 됩니다, 강조 표시 **Web API 2 컨트롤러-비어 있지**, 클릭 하 고 **추가**합니다.
    3. 경우는 **컨트롤러 추가** 대화 상자가 표시 됩니다, 컨트롤러 이름을 **BooksController**, 클릭 하 고 **추가**합니다.
    4. 경우는 **BooksController.cs** 파일을 열, 파일의 코드를 다음과 같이 바꿉니다. 

        [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample3.cs)]
    5. 저장 하 고 닫습니다는 **BooksController.cs** 파일입니다.
10. 오류에 대 한 확인 하도록 Web API 응용 프로그램을 빌드하십시오.

<a id="STEP2"></a>
### <a name="step-2-adding-the-windows-phone-8-bookstore-catalog-project"></a>2 단계: Windows Phone 8 Bookstore 카탈로그 프로젝트 추가

이 종단 간 시나리오의 다음 단계는 Windows Phone 8 용 카탈로그 응용 프로그램을 만드는 것입니다. 이 응용 프로그램에서 사용할는 *Windows Phone 데이터 바인딩된 앱* 하며 기본 사용자 인터페이스에 대 한 서식 파일에서 생성 한 Web API 응용 프로그램을 사용 합니다 [1 단계](#STEP1) 데이터 원본으로이 자습서의 합니다.

1. 마우스 오른쪽 단추로 클릭는 **BookStore** 에서 솔루션은 솔루션 탐색기에서 클릭 **추가**, 차례로 **새 프로젝트**합니다.
2. 경우는 **새 프로젝트** 대화 상자가 표시 됩니다, 확장 **설치 됨**, 다음 **Visual C#**, 차례로 **Windows Phone**합니다.
3. 강조 표시 **Windows Phone 데이터 바인딩된 앱**, 입력 **BookCatalog** 이름과 클릭 한 다음에 대 한 **확인**합니다.
4. Json.NET NuGet 패키지를 추가할는 **BookCatalog** 프로젝트:

    1. 마우스 오른쪽 단추로 클릭 **참조** 에 대 한는 **BookCatalog** 솔루션 탐색기에서 프로젝트를 마우스 클릭 **NuGet 패키지 관리**합니다.
    2. 경우는 **NuGet 패키지 관리** 대화 상자가 표시 됩니다, 확장 된 **온라인** 섹션을 강조 표시 **nuget.org**합니다.
    3. 입력 **Json.NET** 검색에 필드를 검색 아이콘을 클릭 합니다.
    4. 강조 표시 **Json.NET** 클릭 한 다음 확인 하 고 검색 결과에서 **설치**합니다.
    5. 설치가 완료 되 면 클릭 **닫기**합니다.
5. 추가 **BookDetails** 모델은 **BookCatalog** 프로젝트; 여기 bookstore 클래스의 일반 모델에 포함:

    1. 마우스 오른쪽 단추로 클릭는 **BookCatalog** 클릭 한 다음 솔루션 탐색기에서 프로젝트 **추가**, 클릭 하 고 **새 폴더**합니다.
    2. 새 폴더 이름을 **모델**합니다.
    3. 마우스 오른쪽 단추로 클릭는 **모델** 솔루션 탐색기에서 폴더를 클릭 한 다음 **추가**, 클릭 하 고 **클래스**합니다.
    4. 경우는 **새 항목 추가** 대화 상자가 표시 됩니다, 클래스 파일의 이름을 **BookDetails.cs**, 클릭 하 고 **추가**합니다.
    5. 경우는 **BookDetails.cs** 파일을 열, 파일의 코드를 다음과 같이 바꿉니다. 

        [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample4.cs)]
    6. 저장 하 고 닫습니다는 **BookDetails.cs** 파일입니다.
6. 업데이트는 **MainViewModel.cs** BookStore Web API 응용 프로그램과 통신 하는 기능을 포함 하도록 클래스:

    1. 확장 된 **Viewmodel** 폴더의 솔루션 탐색기에서 마우스 두 번 클릭은 **MainViewModel.cs** 파일입니다.
    2. 경우는 **MainViewModel.cs** 파일을 열면 파일의 코드를 다음과 같이 바꿉니다;의 값을 업데이트 해야 합니다는 `apiUrl` Web API의 실제 URL로 상수: 

        [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample5.cs)]
    3. 저장 하 고 닫습니다는 **MainViewModel.cs** 파일입니다.
7. 업데이트는 **MainPage.xaml** 응용 프로그램 이름을 사용자 지정 하는 파일:

    1. 두 번 클릭 하 여 **MainPage.xaml** 솔루션 탐색기에서 파일입니다.
    2. 경우는 **MainPage.xaml** 파일을 열을 다음 코드 줄을 찾습니다. 

        [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample6.xml)]
    3. 해당 줄을 다음으로 바꿉니다. 

        [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample7.xml)]
    4. 저장 하 고 닫습니다는 **MainPage.xaml** 파일입니다.
8. 업데이트는 **DetailsPage.xaml** 표시 된 항목을 사용자 지정 하는 파일:

    1. 두 번 클릭 하 여 **DetailsPage.xaml** 솔루션 탐색기에서 파일입니다.
    2. 경우는 **DetailsPage.xaml** 파일을 열을 다음 코드 줄을 찾습니다. 

        [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample8.xml)]
    3. 해당 줄을 다음으로 바꿉니다. 

        [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample9.xml)]
    4. 저장 하 고 닫습니다는 **DetailsPage.xaml** 파일입니다.
9. 오류를 확인 하려면 Windows Phone 응용 프로그램을 빌드하십시오.

### <a name="step-3-testing-the-end-to-end-solution"></a>3 단계: 종단 간 솔루션 테스트

설명한 것 처럼는 *필수 구성 요소* 로컬 시스템에서이 자습서에서는 웹 API 및 Windows Phone 8 간의 연결을 테스트할 때의 섹션 프로젝트의 지침에 따라 해야 합니다는  *[ 로컬 컴퓨터에 Web API 응용 프로그램에 연결 하는 Windows Phone 8 Emulator](https://go.microsoft.com/fwlink/?LinkId=324014)*  테스트 환경의를 설정 하는 문서입니다.

구성 된 테스트 환경을 설정한 후에 Windows Phone 응용 프로그램 시작 프로젝트로 설정 해야 합니다. 이렇게 하려면 강조 표시는 **BookCatalog** 응용 프로그램 솔루션 탐색기에서 마우스 클릭을 **시작 프로젝트로 설정**:

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image6.png)](calling-web-api-from-a-windows-phone-8-application/_static/image5.png) |
| --- |
| 확장 하는 이미지를 클릭 합니다. |

F5 키를 눌러 Visual Studio 시작 됩니다 모두 Windows Phone 에뮬레이터를 표시 하는 &quot;잠시 기다려 주십시오&quot; Web API에서 응용 프로그램 데이터를 검색 하는 동안 메시지:

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image8.png)](calling-web-api-from-a-windows-phone-8-application/_static/image7.png) |
| --- |
| 확장 하는 이미지를 클릭 합니다. |

성공한 경우 모든 항목 표시 카탈로그를 표시 되어야 합니다.

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image10.png)](calling-web-api-from-a-windows-phone-8-application/_static/image9.png) |
| --- |
| 확장 하는 이미지를 클릭 합니다. |

모든 책 제목을 누르면 응용 프로그램에는 책 설명을 표시 됩니다.

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image12.png)](calling-web-api-from-a-windows-phone-8-application/_static/image11.png) |
| --- |
| 확장 하는 이미지를 클릭 합니다. |

응용 프로그램이 Web API과 통신할 수 없는 경우 오류 메시지가 표시 됩니다.

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image14.png)](calling-web-api-from-a-windows-phone-8-application/_static/image13.png) |
| --- |
| 확장 하는 이미지를 클릭 합니다. |

오류 메시지를 누르면 오류에 대 한 추가 정보가 표시 됩니다.

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image16.png)](calling-web-api-from-a-windows-phone-8-application/_static/image15.png) |
| --- |
| 확장 하는 이미지를 클릭 합니다. |
