---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
title: ASP.NET 4.7 Web Forms 및 Visual Studio 2017 시작 | Microsoft Docs
author: Erikre
description: 이 단계별 자습서 시리즈는 ASP.NET 4.7 및 Microsoft Visual Studio를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항 설명
ms.author: riande
ms.date: 01/09/2019
ms.assetid: 9b96eaa1-8ef0-4338-a2e8-e0f970bfaf68
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
msc.type: authoredcontent
ms.openlocfilehash: fb41ce72e9454d8d670a0b95234d2bc3f909f0ee
ms.sourcegitcommit: 42a8164b8aba21f322ffefacb92301bdfb4d3c2d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54341555"
---
<a name="getting-started-with-aspnet-45-web-forms-and-visual-studio-2017"></a>ASP.NET 4.5 Web Forms 및 Visual Studio 2017을 사용 하 여 시작
====================

[Wingtip Toys 샘플 프로젝트 (C#)를 다운로드](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자책 (PDF) 다운로드](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

이 자습서 시리즈에서는 ASP.NET 4.5와 Microsoft Visual Studio 2017을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 방법을 보여 줍니다. 

## <a name="introduction"></a>소개

이 자습서 시리즈 ASP.NET 4.5와 Visual Studio 2017을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 과정을 안내 합니다. 명명 된 응용 프로그램을 만든 **Wingtip Toys** -간소화 된 storefront 웹 사이트를 온라인으로 항목을 판매 합니다. 시리즈 중 ASP.NET 4.5의 새로운 기능에 강조 표시 됩니다.

### <a name="target-audience"></a>대상 사용자

새 ASP.NET Web forms 개발자는이 자습서 시리즈에 대 한 대상입니다.

다음 영역에서 약간의 지식이 있어야 합니다.

- 개체 지향 프로그래밍 (OOP) 및 언어
- 웹 개발 (HTML, CSS, JavaScript)
- 관계형 데이터베이스
- N 계층 아키텍처

다양 한이 분야를 검토 하려면 다음 콘텐츠를 연구 하는 것이 좋습니다.

- [Visual C# 시작](https://msdn.microsoft.com/library/a72418yk.aspx)
- [Web Development](https://msdn.microsoft.com/beginner/bb308760.aspx), [HTML, CSS, JavaScript, SQL, PHP, JQuery](http://w3schools.com/)
- [관계형 데이터베이스](http://en.wikipedia.org/wiki/Relational_database)
- [다중 계층 아키텍처](http://en.wikipedia.org/wiki/Multitier_architecture)

### <a name="application-features"></a>응용 프로그램 기능

이 시리즈에 제공 된 ASP.NET Web Form 기능은 다음과 같습니다.

- 웹 응용 프로그램 프로젝트 (웹 사이트 프로젝트가 아닌)
- Web Forms
- 마스터 페이지, 구성
- 부트스트랩
- Entity Framework 코드 먼저 LocalDB
- 요청 유효성 검사
- 강력한 형식의 데이터 컨트롤
- 모델 바인딩
- 데이터 주석
- 값 공급자
- SSL 및 OAuth
- ASP.NET Id, 구성 및 권한 부여
- 비간섭 유효성 검사
- 라우팅
- ASP.NET 오류 처리

### <a name="application-scenarios-and-tasks"></a>응용 프로그램 시나리오 및 작업

자습서 시리즈 작업에는 다음이 포함 됩니다.

- 만들기, 검토 및 새 프로젝트를 실행 합니다.
- 데이터베이스 구조 만들기
- 초기화 및 데이터베이스 시 딩
- 스타일, 그래픽 및 마스터 페이지를 사용 하 여 UI 사용자 지정
- 페이지 및 탐색 기능 추가
- 메뉴 세부 정보 및 제품 데이터를 표시합니다.
- 쇼핑 카트 만들기
- 추가 SSL 및 OAuth 지원
- 지불 방법 추가
- 관리자 역할 및 응용 프로그램에 사용자를 포함 하 여
- 특정 페이지 및 폴더에 대 한 액세스 제한
- 웹 응용 프로그램 파일을 업로드합니다.
- 입력된 유효성 검사 구현
- 웹 응용 프로그램에 대 한 경로 등록합니다.
- 오류 처리 및 오류 로깅 구현

## <a name="overview"></a>개요

이 자습서 시리즈에 프로그래밍 개념에 익숙한 사용자에 게 적합 하지만 새 ASP.NET Web forms는입니다. 인 경우 이미 친숙 한 ASP.NET Web Forms를 사용 하 여이 시리즈도 도움이 될 수 있습니다 새 ASP.NET 4.5 기능에 대해 알아봅니다. 프로그래밍 개념 및 ASP.NET Web Forms를 사용 하 여 알 수 없는 판독기에 제공 된 추가 Web Forms 자습서를 참조 하세요. 합니다 [Getting Started](../../../index.md) ASP.NET 웹 사이트의 섹션입니다.

이 자습서 시리즈에서 제공 하는 ASP.NET 4.5에는 다음 기능이 포함 됩니다.

- 제공 하는 프로젝트를 만들기 위한 간단한 UI [많은 ASP.NET 프레임 워크에 대 한 지원을](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#add) (Web Forms, MVC 및 Web API).
- [부트스트랩](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap), 레이아웃, 테마 및 반응 형 디자인 프레임 워크입니다.
- [ASP.NET Id](../../../../identity/index.md), 웹 호스팅 IIS 외에 소프트웨어를 사용 하 여 모든 ASP.NET 프레임 워크와에서 동일 하 게 작동 하는 새로운 ASP.NET 멤버 자격 시스템입니다.
- [Entity Framework 6](https://msdn.microsoft.com/data/ef.aspx)

  수 있도록 하는 Entity Framework에 대 한 업데이트:
  - 강력한 형식의 개체로 데이터 검색 및 조작
  - 데이터를 비동기적으로 액세스
  - 일시적인 연결 오류 처리
  - 로그 SQL 문

ASP.NET 4.5 기능 목록은 참조 하세요 [ASP.NET 및 Web Tools for Visual Studio 2013 릴리스 정보](../../../../visual-studio/overview/2013/release-notes.md)합니다.

### <a name="the-wingtip-toys-sample-application"></a>Wingtip Toys 샘플 응용 프로그램

다음 스크린샷에서이 자습서 시리즈에서 만든 ASP.NET Web Forms 응용 프로그램에서. Visual Studio에서 응용 프로그램을 실행 하는 경우 다음 웹 홈 페이지가 나타납니다.

![Wingtip Toys-기본 페이지](introduction-and-overview/_static/image1.png)

새 사용자로 등록 하거나 기존 사용자로 로그인 수 있습니다. 위쪽 탐색 모음에는 데이터베이스에서 제품 범주 및 해당 제품에 대 한 링크에 있습니다.

선택 하는 경우 **제품**, 사용 가능한 제품은 모두 표시 됩니다. 

![Wingtip Toys-제품](introduction-and-overview/_static/image2.png)

특정 제품을 선택 하면 제품 정보가 표시 됩니다.


![Wingtip Toys-제품 세부 정보](introduction-and-overview/_static/image3.png)

사용자로 등록 한 Web Forms 템플릿 기본 기능을 사용 하 여 로그인 합니다. 이 자습서에는 또한 기존 Gmail 계정을 사용 하 여 로그인 하는 방법을 설명 합니다. 또한 추가 하 고 데이터베이스에서 제품을 제거 하려면 관리자 권한으로 로그인 할 수 있습니다.

![Wingtip Toys-로그인](introduction-and-overview/_static/image4.png)

사용자로 로그인 한 후 PayPal로 체크 아웃을 쇼핑 카트에 제품을 추가할 수 있습니다. 샘플 응용 프로그램은 PayPal의 개발자 샌드박스에서 작동 하도록 설계 되었습니다. 실제 비용 트랜잭션이 수행이 됩니다.

![Wingtip Toys-쇼핑 카트](introduction-and-overview/_static/image5.png)

PayPal 계정, 순서 및 결제 정보를 확인합니다.

![Wingtip Toys-PayPal](introduction-and-overview/_static/image6.png)

PayPal에서 반환한 검토 하 고 주문을 완료 수 있습니다.

![Wingtip Toys-주문 검토](introduction-and-overview/_static/image7.png)

## <a name="prerequisites"></a>전제 조건

시작 하기 전에 다음 소프트웨어가 컴퓨터에 설치 되어 있는지 확인 합니다.

- [Microsoft Visual Studio 2017 또는 Microsoft Visual Studio Community 2017](https://visualstudio.microsoft.com/downloads/)합니다.

.NET Framework는 자동으로 설치 됩니다.

이 자습서 시리즈는 Microsoft Visual Studio Community 2017을 사용합니다. 중 하나를 사용할 수 있습니다 또는 Microsoft Visual Studio 2017이 자습서 시리즈를 완료 합니다.

Visual Studio에 대 한 다음 note:

* Microsoft Visual Studio 2017 및 Microsoft Visual Studio Community 2017 이라고 *Visual Studio* 이 자습서 시리즈 전체.

* Visual Studio 2017이 이미 설치 된 이전 버전 옆에 있는 설치 됩니다. 이전 버전에서 만든 사이트는 Visual Studio 2017에서 열 수 있습니다 하 고 이전 버전에서 계속 합니다.

* 처음으로 Visual Studio를 시작, 선택한 가정 합니다 *웹 개발* 설정 합니다. 자세한 내용은 [방법: 웹 개발 환경 설정 선택](https://msdn.microsoft.com/library/ff521558.aspx)합니다.

필수 구성 요소를 설치한 후이 자습서 시리즈에서 제공 하는 웹 프로젝트 만들기를 시작 하려면 준비가입니다.

## <a name="download-the-sample-application"></a>샘플 응용 프로그램 다운로드

 MSDN 샘플 사이트에서 언제 든 지에서 완성 된 샘플 applicatiion를 다운로드할 수 있습니다.

[Getting Started with ASP.NET 4.5 Web Forms 및 Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) 

 이 다운로드에는 다음 항목에 있습니다.

- 샘플 응용 프로그램을 *WingtipToys* 폴더입니다.
- 샘플 응용 프로그램을 만들려면 사용 하는 리소스를 *WingtipToys 자산* 폴더에는 *WingtipToys* 폴더입니다.

다운로드 되는 *.zip* 파일입니다. 이 자습서 시리즈에서 만든 완료 된 프로젝트, 찾기 및 선택 합니다 *C#* .zip 파일에는 폴더입니다. 저장 된 C# 폴더로 Visual Studio 프로젝트를 사용 하 여 작업에 사용 합니다. 기본적으로 Visual Studio 2017 프로젝트 폴더는:

<strong>C:\Users&#92;</strong><strong><em>&lt;username&gt;</em></strong><strong>\source\repos</strong>

이름 바꾸기는 ***C#*** 폴더 ***WingtipToys***합니다.

> [!NOTE]
> 라는 폴더를 이미 있다면 *WingtipToys* 에 프로젝트 폴더의 이름을 일시적으로 기존 폴더 이름을 바꾸기 전에 *C#* 폴더를 *WingtipToys*합니다.

완료 된 프로젝트를 실행 하려면 엽니다는 *WingtipToys* 폴더를 두 번 클릭 합니다 *WingtipToys.sln* 파일입니다. Visual Studio 2017 프로젝트를 엽니다. 그런 다음 마우스 오른쪽 단추로 클릭 합니다 *Default.aspx* 파일 **솔루션 탐색기** 선택한 **브라우저에서 보기**합니다.

## <a name="take-a-aspnet-web-forms-quiz-to-review-content"></a>ASP.NET Web Forms 퀴즈를 통해 콘텐츠를 검토 합니다.

자습서 시리즈를 완료 한 후 퀴즈를 배운 내용을 테스트 하 고 주요 개념을 보강 합니다. 각 질문 설명 및 추가 지침에 대 한 링크를 제공합니다.

 * [ASP.NET Web Forms 퀴즈](https://blogs.msdn.microsoft.com/erikreitan/2016/01/08/asp-net-web-forms-quiz/) 

## <a name="tutorial-support-and-comments"></a>자습서 지원 및 주석

의견 및 질문에 대 한 질문과 대답 섹션에 포함을 사용 합니다 [Getting Started with ASP.NET 4.5 Web Forms 및 Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) 샘플 페이지입니다.

이 자습서 시리즈에 대 한 의견을 기다리겠습니다. 이 자습서 시리즈를 업데이트 하는 경우에 수정 또는 향상 된 기능에 대 한 제안 사항을 고려해 야 할 노력이 이루어집니다.

오류가 발생을 해당 하는 오류 메시지는 혼동 될 수 없습니다를 해결 하는 방법에 대 한 설명이 없으므로 좋은 사용 하 여 합니다. 에 대 한 도움말을 확인할 수 있습니다 합니다 [ASP.NET 포럼](https://forums.asp.net/)합니다. 또 다른 좋은 소스는 질문과 대답 섹션에는 [Getting Started with ASP.NET 4.5 Web Forms 및 Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) 샘플 페이지입니다. 

> [!div class="step-by-step"]
> [다음](create-the-project.md)
