---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
title: "ASP.NET 4.5 Web Forms 및 Visual Studio 2013 시작 | Microsoft Docs"
author: Erikre
description: "이 단계별 자습서 시리즈 ASP.NET 4.5 및 Microsoft Visual Studio Expres를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 구축 하는 기초 알려 드리겠습니다 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/08/2014
ms.topic: article
ms.assetid: 9b96eaa1-8ef0-4338-a2e8-e0f970bfaf68
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
msc.type: authoredcontent
ms.openlocfilehash: 6ae398f94c0ac3872601bdc8fd935f6d285793db
ms.sourcegitcommit: 493a215355576cfa481773365de021bcf04bb9c7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
<a name="getting-started-with-aspnet-45-web-forms-and-visual-studio-2013"></a>ASP.NET 4.5 Web Forms 및 Visual Studio 2013 시작
====================
으로 [Erik Reitan](https://github.com/Erikre)

[Wingtip Toys 샘플 프로젝트 (C#)를 다운로드](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자책 (PDF)를 다운로드 합니다.](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 이 단계별 자습서 시리즈 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 웹에 대 한 ASP.NET Web Forms 응용 프로그램을 구축 하는 기초 알려 드리겠습니다. [ASP.NET Web Forms 퀴즈](http://quizapp.cloudapp.net/?quiz=ASP.NET)  
> 사용자가 모르는 테스트 하 고 ASP.NET Web Forms 퀴즈를 수행 하 여 주요 개념을 강화 합니다. 이 퀴즈가 자습서 시리즈에 포함 된 콘텐츠에서 특별히 설계 되었습니다. 각 질문 퀴즈에 설명 된 추가 지침에 대 한 링크를 제공합니다.


## <a name="introduction"></a>소개

이 일련의 자습서에서는 웹 및 ASP.NET 4.5 용 Visual Studio Express 2013을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 데 필요한 단계를 안내 합니다.

만들게 응용 프로그램의 이름이 **Wingtip Toys**합니다. 온라인 항목을 판매 하는 전면 스토어 웹 사이트의 간단한 예입니다. 이 자습서 시리즈 ASP.NET 4.5의 새로운 기능을 강조 표시합니다.

주석은, 설정이 및 제안 사항에 따라이 자습서 시리즈를 업데이트 하기 위한 모든 작업 하도록 합니다.

### <a name="download-completed-project"></a>다운로드가 완료 프로젝트

완성 된 자습서를 포함 하는 C# 프로젝트를 다운로드할 수 있습니다.

- [ASP.NET 4.5 Web Forms 및 Visual Studio 2013-Wingtip Toys 시작](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#)

### <a name="review-the-content-by-taking-the-related-aspnet-web-forms-quiz"></a>ASP.NET Web Forms 퀴즈 관련 하 여 콘텐츠 검토

이 자습서를 완료 한 후 사용자가 모르는 테스트 하 고 주요 개념을 수행 하 여 강화할는 [ASP.NET Web Forms 퀴즈](http://quizapp.cloudapp.net/?quiz=ASP.NET&cdn_id=2014-01-17-001)합니다. 이 퀴즈가 자습서 시리즈에 포함 된 콘텐츠에서 특별히 설계 되었습니다. 각 질문 퀴즈에 설명 된 추가 지침에 대 한 링크를 제공합니다.

- [ASP.NET Web Forms 퀴즈](http://quizapp.cloudapp.net/?quiz=ASP.NET)

### <a name="audience"></a>대상 사용자

이 자습서 시리즈의 사용자는 ASP.NET Web Forms를 처음 접하는 숙련 된 개발자. 이 자습서 시리즈의 관심 있는 개발자는 다음과 같은 기술 해야 합니다.

- 친숙 한 개체 지향 프로그래밍 (OOP) 언어
- 익숙한 웹 개발 개념 (HTML, CSS, JavaScript)
- 관계형 데이터베이스 개념을 이해
- N 계층 아키텍처 개념을 이해

위에 나열 된 영역을 검토 하려는 경우 다음 콘텐츠를 검토 하는 것이 좋습니다.

- [Visual C# 시작](https://msdn.microsoft.com/library/a72418yk.aspx)
- [Web Development](https://msdn.microsoft.com/beginner/bb308760.aspx), [HTML, CSS, JavaScript, SQL, PHP, JQuery](http://w3schools.com/)
- [관계형 데이터베이스](http://en.wikipedia.org/wiki/Relational_database)
- [다중 계층 아키텍처](http://en.wikipedia.org/wiki/Multitier_architecture)

### <a name="application-features"></a>응용 프로그램 기능

이 시리즈에 ASP.NET Web Form 기능은 다음과 같습니다.

- 웹 응용 프로그램 프로젝트 (웹 사이트 프로젝트가 아닌)
- Web Forms
- 마스터 페이지, 구성
- 부트스트랩
- Entity Framework Code First,를 LocalDB
- 요청 유효성 검사
- 강력한 형식의 데이터 컨트롤 바인딩, 데이터 주석 모델 및 공급자 값
- OAuth 및 SSL
- ASP.NET Id, 구성 및 권한 부여
- 비 가시적인 유효성 검사
- 라우팅
- ASP.NET 오류 처리

### <a name="application-scenarios-and-tasks"></a>응용 프로그램 시나리오 및 작업

이 시리즈에 설명 된 작업은 다음과 같습니다.

- 새 프로젝트를 실행 하 고 생성, 검토
- 데이터베이스 구조 만들기
- 초기화 하 고 데이터베이스 시드
- 스타일, 그래픽 및 마스터 페이지를 사용 하 여 UI를 사용자 지정
- 페이지 및 탐색 추가
- 메뉴 세부 정보 및 제품 데이터를 표시합니다.
- 쇼핑 카트 만들기
- 추가 SSL 및 OAuth 지원
- 결제 방법을 추가
- 관리자 역할 및 응용 프로그램에 사용자를 포함 하 여
- 특정 페이지와 폴더에 대 한 액세스 제한
- 웹 응용 프로그램에 파일을 업로드 하는 중입니다.
- 입력된 유효성 검사를 구현합니다.
- 웹 응용 프로그램에 대 한 경로 등록 하는 중
- 오류 처리 및 오류 로깅 구현

## <a name="overview"></a>개요

ASP.NET Web Forms을 처음 접하는 경우 있지만 프로그래밍 개념에 익숙한 저마다를 오른쪽 자습서를 수 있습니다. ASP.NET Web Forms에 익숙한 경우 ASP.NET 4.5의 새로운 기능으로이 자습서 시리즈에서 얻을 수 있습니다. 프로그래밍 개념 및 ASP.NET Web Forms에 익숙한 경우 참조는 Web Forms에 제공 된 추가 자습서 [시작](../../../index.md) ASP.NET 웹 사이트에서 섹션.

특정 **최신** 자습서 시리즈가 Web Forms에는 다음이 포함 된 ASP.NET 4.5 기능:

- 간단한 UI를 만들기 위한 프로젝트 해당 제품 [여러 ASP.NET 프레임 워크에 대 한 지원](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#add) (Web Forms, MVC 및 Web API).
- [부트스트랩](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap), 반응 형 디자인 및 테마 설정 기능을 제공 하는 레이아웃 및 테마 프레임 워크입니다.
- [ASP.NET Identity](../../../../identity/index.md)를 웹 호스팅 IIS가 아닌 다른 소프트웨어와 모든 ASP.NET 프레임 워크와 작동에 동일 하 게 작동 하는 새로운 ASP.NET 멤버 자격 시스템.
- [Entity Framework 6](https://msdn.microsoft.com/data/ef.aspx)형식의 개체를 검색 하 고 강력 하 게 데이터를 조작할 수 있는 Entity Framework에 대 한 업데이트, 비동기적으로 일시적인 연결 오류 처리 및 SQL 문을 로그 데이터에 액세스 합니다.

ASP.NET 4.5 기능의 전체 목록은 참조 하십시오. [ASP.NET 및 Web Tools for Visual Studio 2013 릴리스 정보](../../../../visual-studio/overview/2013/release-notes.md)합니다.

### <a name="the-wingtip-toys-sample-application"></a>Wingtip Toys 샘플 응용 프로그램

다음 스크린샷은이 자습서 시리즈의 만들 ASP.NET Web forms 응용 프로그램의 빠른 보기를 제공 합니다. Visual Studio Express 2013 for Web에서에서 응용 프로그램을 실행 하는 경우 다음 웹 홈 페이지 표시 됩니다.

![기본 페이지-: wingtip Toys](introduction-and-overview/_static/image1.png)

새 사용자로 등록 하거나 기존 사용자로 로그인 수 있습니다. 탐색은 데이터베이스에서 사용할 수 있는 제품을 검색 하 여 각 제품 범주에 대 한 최상위에 제공 됩니다.

제품 링크를 선택 하면 모든 사용 가능한 제품의 목록을 볼 수 있습니다.

![Wingtip Toys-제품](introduction-and-overview/_static/image2.png)

또한 나열 된 제품 중 하나를 선택 하 여 개별 제품 세부 정보를 볼 수 있습니다.

![Wingtip Toys-제품 세부 정보](introduction-and-overview/_static/image3.png)

사용자로 등록 한 Web Forms 서식 파일의 기본 기능을 사용 하 여 로그인 합니다. 이 자습서에는 기존 Gmail 계정을 사용 하 여 로그인 하는 방법도 설명 합니다. 또한 추가 하 고 데이터베이스에서 제품을 제거 하려면 관리자 권한으로 로그인 할 수 있습니다.

![Wingtip Toys-로그인](introduction-and-overview/_static/image4.png)

사용자로 로그인 하면 PayPal으로 체크 아웃을 쇼핑 카트에 제품을 추가할 수 있습니다. 이 샘플 응용 프로그램 PayPal의 개발자 샌드박스 에서만 작동 하도록 되어 note 합니다. 실제 금액 트랜잭션이 수행 됩니다.

![쇼핑 카트: wingtip Toys-](introduction-and-overview/_static/image5.png)

PayPal는 계정, 순서 및 지불 정보를 확인 합니다.

![Wingtip Toys-PayPal](introduction-and-overview/_static/image6.png)

PayPal을 통한 반환한 검토 하 고 주문을 완료 수 있습니다.

![Wingtip Toys-순서 검토](introduction-and-overview/_static/image7.png)

## <a name="prerequisites"></a>전제 조건

시작 하기 전에 다음 소프트웨어가 컴퓨터에 설치 되어 있는지 확인 합니다.

- [Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) 또는 [Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web)합니다. .NET Framework는 자동으로 설치 됩니다.

이 자습서 시리즈 웹에 대 한 Microsoft Visual Studio Express 2013을 사용합니다. 이 자습서 시리즈를 완료 하려면 Microsoft Visual Studio Express 2013 for Web 또는 Microsoft Visual Studio 2013을 사용할 수 있습니다.

> [!NOTE] 
> 
> Microsoft Visual Studio 2013 및 Microsoft Visual Studio Express 2013 for Web은 종종로 간주 Visual Studio이 자습서 시리즈 합니다.


이미 Visual Studio 버전이 설치 되어 있으면 설치 프로세스는 기존 버전 옆에 있는 Visual Studio 2013 또는 Microsoft Visual Studio Express 2013 for Web 설치 됩니다. 이전 버전에서 만든 사이트 Visual Studio 2013에서 열 수 및 이전 버전에서 열을 계속 합니다.

> [!NOTE] 
> 
> 이 연습에서는 선택 했다고 가정은 *웹 개발* 설정의 컬렉션 서 처음으로 Visual Studio를 시작 하면 됩니다. 자세한 내용은 참조 [하는 방법: 웹 개발 환경 설정 선택](https://msdn.microsoft.com/library/ff521558.aspx)합니다.


## <a name="download-the-sample-application"></a>샘플 응용 프로그램 다운로드

필수 구성 요소를 설치한 후 했으면 이제이 자습서 시리즈에 제공 되는 새 웹 프로젝트 만들기를 시작할 수 있습니다. 원하는 경우 **필요에 따라** 이 자습서 시리즈 만듭니다 샘플 응용 프로그램을 실행 하면에서 다운로드할 수 MSDN 샘플 사이트입니다. 이 다운로드에는 다음이 포함 되어 있습니다.

- 예제 응용 프로그램에는 *WingtipToys* 폴더입니다.
- 샘플 응용 프로그램을 만드는 사용 되는 리소스는 *WingtipToys 자산* 폴더에는 *WingtipToys* 폴더입니다.

#### <a name="download-the-file-from-msdn-samples-site"></a>MSDN 샘플 사이트에서 파일을 다운로드 합니다.

[ASP.NET 4.5 Web Forms 및 Visual Studio 2013-Wingtip Toys 시작](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) 

다운로드 되는 *.zip* 파일입니다. 이 자습서 시리즈 만듭니다 완료 된 프로젝트, 찾기 및 선택은 *C#*폴더에는 *.zip* 파일입니다. 저장 된 *C#* folderto Visual Studio 2013 프로젝트 작업에 사용할 폴더입니다. 기본적으로 Visual Studio 2013 프로젝트 폴더는 다음입니다.

**C:\Users\*****&lt;username&gt;*****\Documents\Visual Studio 2013\Projects**

이름 바꾸기는 ***C#*** 폴더를 ***WingtipToys***합니다.

> [!NOTE]
> 라는 폴더가 이미 있는 경우 *WingtipToys* 프로젝트 폴더의 이름을 임시로 바꾸거나 기존 폴더 이름을 바꾸기 전에 *C#* 폴더를 *WingtipToys*합니다.


완료 된 프로젝트를 실행 하려면 열고는 *WingtipToys* 폴더를 두 번 클릭은 *WingtipToys.sln* 파일입니다. Visual Studio 2013 프로젝트를 열립니다. 그런 다음 마우스 오른쪽 단추로 클릭는 *Default.aspx* 솔루션 탐색기 창에서 파일을 브라우저에서 보기의 오른쪽 클릭 메뉴에서를 클릭 합니다.

### <a name="tutorial-support-and-comments"></a>자습서 지원 및 주석

에 포함 된 Q &AMP; A 섹션을 사용 하는 [ASP.NET 4.5 Web Forms 및 Visual Studio 2013-Wingtip Toys 시작](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 한 질문이 나 의견에 대 한 샘플 (C#).

이 자습서 시리즈에 대 한 의견을 기다리겠습니다, 하 고이 자습서 시리즈 업데이트 될 때 모든 노력 됩니다 계정 수정 또는 제안이 자습서 주석에서 제공 되는 향상 된 기능에 대 한 고려 되도록 합니다.

개발 하는 동안 오류가 발생 하거나 웹 사이트가 올바르게 실행 되지 않은 경우 오류 메시지가 문제의 소스에 복잡 한 단서를 제공할 수 있습니다 또는 해결 방법을 확인할 수 있습니다. 몇 가지 일반적인 문제 시나리오 연결해보세요를 사용할 수도 있습니다는 [ASP.NET 포럼](https://forums.asp.net/) 또는에 포함 된 Q &AMP; A 섹션의 [ASP.NET 4.5 Web Forms 및 Visual Studio 2013-Wingtip Toys 시작](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 드 ( C#) 샘플. 오류 메시지가 자습서를 진행할 때 작동 하지 않는 경우에 위의 위치를 확인 해야 합니다.

>[!div class="step-by-step"]
[다음](create-the-project.md)
