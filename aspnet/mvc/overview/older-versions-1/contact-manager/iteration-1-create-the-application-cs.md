---
uid: mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-cs
title: '반복 #1 – 응용 프로그램 (C#) 만들기 | Microsoft Docs'
author: microsoft
description: '첫 번째 반복에서 연락처 관리자에서에서 만드는 가장 간단한 방법은 가능 합니다. 기본 데이터베이스 작업에 대 한 지원 추가: 만들기, 읽기, 업데이트 및 D....'
ms.author: aspnetcontent
ms.date: 02/20/2009
ms.assetid: db0f160b-901c-46d3-865e-7ab6cd4ed68d
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-cs
msc.type: authoredcontent
ms.openlocfilehash: 0d756541d2dc911154afb427e52eb5cfdd5d59b4
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37821364"
---
<a name="iteration-1--create-the-application-c"></a>반복 #1 – 응용 프로그램 (C#) 만들기
====================
[Microsoft](https://github.com/microsoft)

[코드 다운로드](iteration-1-create-the-application-cs/_static/contactmanager_1_cs1.zip)

> 첫 번째 반복에서 연락처 관리자에서에서 만드는 가장 간단한 방법은 가능 합니다. 기본 데이터베이스 작업에 대 한 지원 추가: 만들기, 읽기, 업데이트 및 삭제 (CRUD).


## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>연락처 관리 ASP.NET MVC 응용 프로그램을 작성 (VB)

이 시리즈의 자습서에서 전체 연락처 관리 응용을 프로그램 시작부터 완료를 빌드합니다. 연락처 관리자 응용 프로그램에 사용자의 목록을 포함 된 상점 연락처 정보-이름, 전화 번호 및 전자 메일 주소-할 수 있습니다.

여러 반복에 응용 프로그램을 빌드합니다. 각 반복에서 점진적으로 응용 프로그램을 개선 했습니다. 이렇게 여러 반복의 목표는 각 변경의 이유를 이해할 수 있습니다.

- 반복 #1-응용 프로그램을 만듭니다. 첫 번째 반복에서 연락처 관리자에서에서 만드는 가장 간단한 방법은 가능 합니다. 기본 데이터베이스 작업에 대 한 지원 추가: 만들기, 읽기, 업데이트 및 삭제 (CRUD).

- 반복 #2-보기 좋게 응용 프로그램을 확인 합니다. 이 반복에서 기본 ASP.NET MVC 보기 마스터 페이지를 수정 및 스타일 시트를 연계 하 여 응용 프로그램의 모양을 개선 합니다.

- 반복 #3-양식 유효성 검사를 추가 합니다. 세 번째 반복에서는 기본 양식 유효성 검사를 추가합니다. 사용자를 방지할 수를 필요한 형식의 필드를 완료 하지 않고 폼을 제출 합니다. 또한 전자 메일 주소 및 전화 번호 유효성을 검사 합니다.

- 반복 #4-느슨하게 결합 된 응용 프로그램을 확인 합니다. 이 세 번째 반복에서는 활용 쉽게 유지 관리 하 고 연락처 관리자 응용 프로그램을 수정 하려면 몇 가지 소프트웨어 디자인 패턴입니다. 예를 들어, 리포지토리 패턴 및 종속성 주입 패턴을 사용 하 여 응용 프로그램을 리팩터링 했습니다.

- 반복 #5-단위 테스트를 만듭니다. 다섯 번째 반복에서에서는 쉽게 응용 프로그램 유지 관리 하 고 단위 테스트를 추가 하 여 수정 합니다. 데이터 모델 클래스를 모의 하 고는 컨트롤러 및 유효성 검사 논리에 대 한 단위 테스트를 작성 합니다.

- 반복 #6-테스트 중심 개발을 사용 합니다. 이 여섯 번째 반복에서는 추가 새로운 기능을 응용 프로그램 먼저 단위 테스트를 작성 하 고 단위 테스트에 대 한 코드를 작성 합니다. 이 반복에서는 메일 그룹을 추가합니다.

- 반복 #7 – Ajax 기능을 추가 합니다. 일곱 번째 반복에서 개선할 응용 프로그램의 성능과 응답성 Ajax에 대 한 지원을 추가 하 여 합니다.

## <a name="this-iteration"></a>이 반복

이 첫 번째 반복에서 기본 응용 프로그램을 빌드합니다. 목표 가능한 가장 빠르고 가장 간단한 방법으로 연락처 관리자를 빌드하는 것입니다. 이후 반복에서 응용 프로그램의 디자인을 향상 했습니다.

연락처 관리자 응용 프로그램은 기본 데이터베이스 중심 응용 프로그램입니다. 새 연락처를 만들고 기존 연락처를 편집 하 고 연락처를 삭제 하는 응용 프로그램을 사용할 수 있습니다.

이 반복에서 다음 단계를 완료 했습니다.

1. ASP.NET MVC 응용 프로그램
2. 이 연락처를 저장 하기 위한 데이터베이스 만들기
3. Microsoft Entity Framework를 사용 하 여 데이터베이스에 대 한 모델 클래스를 생성 합니다.
4. 컨트롤러 작업 및 모든 데이터베이스에 연락처를 나열할 수 있게 해 주는 보기 만들기
5. 컨트롤러 작업을 만들고 데이터베이스에 새 연락처를 만들 수 있게 해 주는 보기
6. 컨트롤러 작업을 만들고 데이터베이스에 있는 기존 연락처를 편집할 수 있게 해 주는 보기
7. 컨트롤러 작업을 만들고 데이터베이스에 있는 기존 연락처를 삭제할 수 있게 해 주는 보기

## <a name="software-prerequisites"></a>소프트웨어 필수 구성 요소

ASP.NET MVC 응용 프로그램에서 Visual Studio 2008 또는 Visual Web Developer 2008 (Visual Web Developer는 모든 Visual Studio의 고급 기능을 포함 하지 않는 Visual Studio의 무료 버전) 컴퓨터에 설치 되어 있어야 합니다. 다음 주소에서의 Visual Studio 2008 평가판 또는 Visual Web Developer를 다운로드할 수 있습니다.

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

> [!NOTE] 
> 
> Visual Web Developer를 사용 하 여 ASP.NET MVC 응용 프로그램에 대 한 설치 Visual Web Developer 서비스 팩 1 있어야 합니다. 서비스 팩 1 없이 웹 응용 프로그램 프로젝트를 만들 수 없습니다.


ASP.NET MVC 프레임 워크입니다. 다음 주소에서 ASP.NET MVC 프레임 워크를 다운로드할 수 있습니다.

[https://www.asp.net/mvc](../../../index.md)

이 자습서에서는 데이터베이스에 액세스 하려면 Microsoft Entity Framework 사용 합니다. Entity Framework는.NET Framework 3.5 서비스 팩 1 포함 되어 있습니다. 다음 위치에서이 서비스 팩을 다운로드할 수 있습니다.

[https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&ampdisplaylang = en](https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;displaylang=en)

각이 다운로드 하나씩 수행 하는 대신, Web Platform Installer (Web PI)를 활용할 수 있습니다. 다음 주소에서 웹 PI를 다운로드할 수 있습니다.

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

## <a name="aspnet-mvc-project"></a>ASP.NET MVC 프로젝트

ASP.NET MVC 웹 응용 프로그램 프로젝트입니다. Visual Studio를 시작 하 고 메뉴 옵션을 선택 **파일, 새 프로젝트**합니다. 합니다 **새 프로젝트** 대화 상자가 나타납니다 (그림 1 참조). 선택 된 **웹** 프로젝트 형식 및 **ASP.NET MVC 웹 응용 프로그램** 템플릿. 새 프로젝트의 이름을 *ContactManager* 확인 단추를 클릭 합니다.


.NET Framework 3.5 맨 위에 있는 드롭다운 목록에서 선택 되어 있는지 확인의 오른쪽의 **새 프로젝트** 대화 합니다. 그렇지 않으면 t-이득 ASP.NET MVC 웹 응용 프로그램 템플릿이 표시 합니다.


[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image1.jpg)](iteration-1-create-the-application-cs/_static/image1.png)

**그림 01**: 새 프로젝트 대화 상자 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image2.png))


ASP.NET MVC 응용 프로그램을 **단위 테스트 프로젝트 만들기** 대화 상자가 나타납니다. 이 대화 상자를 만들고 ASP.NET MVC 응용 프로그램을 만들 때 솔루션에 단위 테스트 프로젝트를 추가할 것인지 나타내기 위해 사용할 수 있습니다. T 땀 있지만이 반복에서 단위 테스트 빌드 옵션을 선택 해야 **예, 단위 테스트 프로젝트 만들기** 이후 반복에서 단위 테스트를 추가할 계획 이기 때문에 있습니다. 새 ASP.NET MVC 프로젝트를 처음 만들 때 테스트 프로젝트를 추가 하는 것은 ASP.NET MVC 프로젝트를 만든 후 테스트 프로젝트를 추가 하는 것 보다 훨씬 쉽습니다.

> [!NOTE] 
> 
> Visual Web Developer는 테스트 프로젝트를 지원 하지 않으므로 얻지 못하는 단위 테스트 프로젝트 만들기 대화 상자 Visual Web Developer를 사용 하는 경우.


[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image2.jpg)](iteration-1-create-the-application-cs/_static/image3.png)

**그림 02**:의 단위 테스트 프로젝트 만들기 대화 상자 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image4.png))


ASP.NET MVC 응용 프로그램 Visual Studio 솔루션 탐색기 창에 나타납니다 (그림 3 참조). Don t 메뉴 옵션을 선택 하 여이 창을 열 수 있습니다 다음 솔루션 탐색기 창 표시 **보기, 솔루션 탐색기**합니다. 솔루션에 두 개의 프로젝트 알림: ASP.NET MVC 프로젝트와 테스트 프로젝트. ASP.NET MVC 프로젝트 이름이 ContactManager 및 테스트 프로젝트 이름이 ContactManager.Tests 합니다.


[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image3.jpg)](iteration-1-create-the-application-cs/_static/image5.png)

**그림 03**:의 솔루션 탐색기 창 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image6.png))


## <a name="deleting-the-project-sample-files"></a>프로젝트 샘플 파일 삭제

ASP.NET MVC 프로젝트 템플릿은 컨트롤러 및 뷰에 대 한 샘플 파일이 포함 되어 있습니다. 새 ASP.NET MVC 응용 프로그램을 만들기 전에 이러한 파일을 삭제 해야 합니다. 파일 또는 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 하 여 솔루션 탐색기 창에서 파일 및 폴더를 삭제할 수 있습니다 **삭제**합니다.

ASP.NET MVC 프로젝트에서 다음 파일을 삭제 해야 합니다.

- \Controllers\HomeController.cs

- \Views\Home\About.aspx

- \Views\Home\Index.aspx

및 테스트 프로젝트에서 다음 파일을 삭제 해야 합니다.

\Controllers\HomeControllerTest.cs

## <a name="creating-the-database"></a>데이터베이스 만들기

연락처 관리자 응용 프로그램은 데이터베이스 기반 웹 응용 프로그램입니다. 연락처 정보를 저장할 데이터베이스를 사용 합니다.

Microsoft SQL Server, Oracle, MySQL 및 IBM DB2 데이터베이스를 비롯 한 모든 최신 데이터베이스를 사용 하 여 ASP.NET MVC 프레임 워크입니다. 이 자습서에서는 Microsoft SQL Server 데이터베이스를 사용합니다. Visual Studio를 설치할 때 Microsoft SQL Server 데이터베이스의 무료 버전인 Microsoft SQL Server Express 설치 옵션으로 제공 됩니다.

앱을 마우스 오른쪽 단추로 클릭 하 여 새 데이터베이스를 만들\_솔루션 탐색기 창 및 메뉴 옵션을 선택 하면 데이터 폴더 **추가, 새 항목**합니다. 에 **새 항목 추가** 대화 상자에서 선택 합니다 **데이터** 범주 및 **SQL Server 데이터베이스** 템플릿 (그림 4 참조). 새 데이터베이스 ContactManagerDB.mdf 이름과 확인 단추를 클릭 합니다.


[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image4.jpg)](iteration-1-create-the-application-cs/_static/image7.png)

**그림 04**: 새 Microsoft SQL Server Express 데이터베이스를 만드는 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image8.png))


데이터베이스 응용 프로그램에 표시 되는 새 데이터베이스를 만든 후\_솔루션 탐색기 창에서 데이터 폴더. 서버 탐색기 창을 열고 데이터베이스에 연결 된 ContactManager.mdf 파일을 두 번 클릭 합니다.

> [!NOTE] 
> 
> 서버 탐색기 창에는 Microsoft Visual Web Developer의 경우 데이터베이스 탐색기 창을 이라고 합니다.


데이터베이스 테이블, 뷰, 트리거 및 저장된 프로시저와 같은 새 데이터베이스 개체를 만들려면 서버 탐색기 창에서 사용할 수 있습니다. 테이블 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **새 테이블 추가**합니다. 데이터베이스 테이블 디자이너 나타납니다 (그림 5 참조).


[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image5.jpg)](iteration-1-create-the-application-cs/_static/image9.png)

**그림 05**: 데이터베이스 테이블 디자이너 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image10.png))


다음 열이 포함 된 테이블을 만들려고 해야 합니다.

<a id="0.1_table01"></a>


| **열 이름** | **데이터 형식** | **Null 허용** |
| --- | --- | --- |
| ID | int | False |
| FirstName | nvarchar(50) | False |
| LastName | nvarchar(50) | False |
| 전화 번호 | nvarchar(50) | False |
| 메일 | nvarchar(255) | False |


첫 번째 열, Id 열은 특별 합니다. Id 열을 Id 열 및 기본 키 열으로 표시 해야 합니다. 열 속성 (그림 6의 맨 아래에서 확인)를 확장 하 고 Id 사양 속성까지 아래로 스크롤 하 여 열이 Identity 열 임을 나타낼 있습니다. 설정 된 **(Id)** 속성을 값 **예**합니다.

열을 선택 하 고 키 아이콘이 있는 단추를 클릭 하 여 기본 키 열으로 열을 표시 합니다. 열은 기본 키 열으로 표시 되 면 열 옆에 있는 키 아이콘이 나타납니다 (그림 6 참조).

테이블 만들기를 마친 후 새 테이블을 저장 하려면 저장 단추 (플로피 아이콘이 포함 된 단추)를 클릭 합니다. 새 테이블 이름을 *연락처*합니다.

마침을 연락처 데이터베이스 테이블을 만든 후 테이블에 일부 레코드를 추가 해야 합니다. 서버 탐색기 창에서 Contacts 테이블을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **테이블 데이터 표시**합니다. 표시 된 표에서 하나 이상의 연락처를 입력 합니다.

## <a name="creating-the-data-model"></a>데이터 모델 만들기

ASP.NET MVC 응용 프로그램 모델, 뷰 및 컨트롤러 구성 됩니다. 이전 섹션에서 만든 Contacts 테이블을 나타내는 모델 클래스를 만들어 시작 합니다.

이 자습서에서는 데이터베이스에서 모델 클래스를 자동으로 생성 하는 Microsoft Entity Framework 사용 합니다.

> [!NOTE] 
> 
> ASP.NET MVC 프레임 워크는 어떤 방식으로 Microsoft Entity Framework는 관련이 없습니다. NHibernate, LINQ to SQL 또는 ADO.NET을 포함 하 여 다른 데이터베이스 액세스 기술을 사용 하 여 ASP.NET MVC를 사용할 수 있습니다.


데이터 모델 클래스를 만들려면 다음이 단계를 수행 합니다.

1. 솔루션 탐색기 창에서 Models 폴더를 마우스 오른쪽 단추로 누르고 **추가, 새 항목**합니다. 합니다 **새 항목 추가** 대화 상자가 나타납니다 (그림 6 참조).
2. 선택 된 **데이터** 범주 및 **ADO.NET Entity Data Model** 템플릿. 데이터 모델의 이름을 *ContactManagerModel.edmx* 을 클릭 합니다 **추가** 단추입니다. 엔터티 데이터 모델 마법사가 나타납니다 (그림 7 참조).
3. 에 **모델 콘텐츠 선택** 선택 단계 **데이터베이스에서 생성** (그림 7 참조).
4. 에 **데이터 연결 선택** 단계 ContactManagerDB.mdf 데이터베이스를 선택 하 고 이름을 입력 합니다 *ContactManagerDBEntities* 엔터티 연결 설정 (그림 8 참조).
5. 에 **데이터베이스 개체 선택** 단계 테이블 (그림 9 참조) 확인란을 선택 합니다. 데이터 모델 (에 하나만 Contacts 테이블) 데이터베이스에 포함 된 모든 테이블이 포함 됩니다. 네임 스페이스를 입력 *모델*합니다. 마법사를 완료 하려면 "마침" 단추를 클릭 합니다.


[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image6.jpg)](iteration-1-create-the-application-cs/_static/image11.png)

**그림 06**: 새 항목 추가 대화 상자 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image12.png))


[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image7.jpg)](iteration-1-create-the-application-cs/_static/image13.png)

**그림 07**: Model 콘텐츠 선택 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image14.png))


[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image8.jpg)](iteration-1-create-the-application-cs/_static/image15.png)

**그림 08**: 데이터 연결 선택 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image16.png))


[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image9.jpg)](iteration-1-create-the-application-cs/_static/image17.png)

**그림 09**: 데이터베이스 개체 선택 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image18.png))


엔터티 데이터 모델 마법사를 완료 하면 엔터티 데이터 모델 디자이너에 표시 됩니다. 디자이너를 모델링 하는 각 테이블에 해당 하는 클래스를 표시 합니다. 연락처 이라는 하나의 클래스에 표시 됩니다.

엔터티 데이터 모델 마법사 기반 데이터베이스 테이블 이름으로 클래스 이름을 생성 합니다. 거의 항상 마법사에서 생성 된 클래스의 이름을 변경 해야 합니다. 디자이너에서 연락처 클래스를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **이름 바꾸기**합니다. (단일) 담당자에 게 연락처 (복수)에서 클래스의 이름을 변경 합니다. 클래스 이름으로 변경한 후 클래스는 그림 10 처럼 표시 됩니다.


[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image10.jpg)](iteration-1-create-the-application-cs/_static/image19.png)

**그림 10**: The 연락처 클래스 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image20.png))


이 시점에서 데이터베이스 모델을 만들었습니다. 데이터베이스에서 특정 연락처 레코드를 나타내는 연락처 클래스를 사용할 수 있습니다.

## <a name="creating-the-home-controller"></a>홈 컨트롤러 만들기

다음 단계는 Home 컨트롤러를 만드는 것입니다. Home 컨트롤러는 ASP.NET MVC 응용 프로그램에서 호출 되는 기본 컨트롤러입니다.

솔루션 탐색기 창에서 컨트롤러 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 하 여 홈 컨트롤러 클래스를 만듭니다 **추가, 컨트롤러** (그림 11 참조). 확인 확인란 **Create, Update 및 세부 정보 시나리오에 대 한 작업 메서드를 추가**합니다. 이 확인란을 클릭 하기 전에 선택 되어 있는지 확인 합니다 **추가** 단추입니다.


[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image11.jpg)](iteration-1-create-the-application-cs/_static/image21.png)

**그림 11**: Home 컨트롤러 추가 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image22.png))


Home 컨트롤러를 만들 때에 목록 1에서 클래스를 가져옵니다.

**1-controllers\ homecontroller.cs를 나열합니다.**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample1.cs)]

## <a name="listing-the-contacts"></a>연락처 나열

연락처 데이터베이스 테이블에 레코드를 표시 하려면 index () 작업 및 인덱스 뷰를 생성 해야 합니다.

Home 컨트롤러 index () 작업을 이미 있습니다. 목록 2와 같은 표시 되도록이 메서드를 수정 해야 합니다.

**2-controllers\ homecontroller.cs를 나열합니다.**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample2.cs)]

라는 private 필드 2 목록에서 홈 컨트롤러 클래스를 포함 하는 알림 \_엔터티. \_엔터티 필드 데이터 모델에서 엔터티를 나타냅니다. 사용 하 여는 \_엔터티 필드는 데이터베이스와 통신할 수 있습니다.

Index () 메서드를 연락처 데이터베이스 테이블에서 모든 연락처를 나타내는 뷰를 반환 합니다. 식 \_엔터티. ContactSet.ToList() 제네릭 목록으로 연락처 목록을 반환합니다.

이제는 우리 ve 인덱스 컨트롤러를 만든 다음 인덱스 뷰를 생성 해야 합니다. 인덱스 뷰를 만들기 전에 메뉴 옵션을 선택 하 여 응용 프로그램을 컴파일합니다 **빌드, 솔루션 빌드**합니다. 항상이 모델 클래스 목록 표시 하려면에서 보기를 추가 하기 전에 프로젝트를 컴파일해야 합니다 **뷰 추가** 대화 합니다.

Index () 메서드를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 하 여 인덱스 뷰를 만든 **뷰 추가** (그림 12 참조). 이 메뉴 옵션을 선택 하면 열립니다는 **뷰 추가** 대화 상자 (그림 13 참조).


[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image12.jpg)](iteration-1-create-the-application-cs/_static/image23.png)

**그림 12**: 인덱스 뷰 추가 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image24.png))


에 **뷰 추가** 대화 상자에서 레이블이 지정 된 확인란 **강력한 형식의 뷰를 만들**합니다. 데이터 클래스 ContactManager.Models.Contact 보기 및 콘텐츠 목록 보기를 선택 합니다. 이러한 옵션을 선택 하면 연락처 레코드의 목록을 표시 하는 보기를 생성 합니다.


[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image13.jpg)](iteration-1-create-the-application-cs/_static/image25.png)

**그림 13**: 뷰 추가 대화 상자 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image26.png))


클릭할 때 합니다 **추가** 단추, 목록 3 인덱스 뷰 생성 됩니다. 알림 합니다 &lt;% @ 페이지 %&gt; 파일의 위쪽에 표시 되는 지시문입니다. 인덱스 보기 ViewPage에서 상속&lt;IEnumerable&lt;ContactManager.Models.Contact&gt; &gt; 클래스입니다. 즉, 뷰에서 모델 클래스에는 연락처 엔터티 목록을 나타냅니다.

인덱스 뷰의 본문 모델 클래스를 나타내는 연락처의 각 반복 되는 foreach 루프를 포함 합니다. 연락처 클래스의 각 속성의 값은 HTML 표 내의 표시 됩니다.

**3-Views\Home\Index.aspx (수정 되지 않은)를 나열 합니다.**

[!code-aspx[Main](iteration-1-create-the-application-cs/samples/sample3.aspx)]

하나의 인덱스 보기 수정 해야 합니다. 세부 정보 보기를 만들지 않는 것을 하기 때문에 세부 정보 링크를 제거할 수 있습니다. 검색 하 고 인덱스 보기에서 다음 코드를 제거 합니다.

{0} id = 항목입니다. Id}) %&gt;

인덱스 보기를 수정한 후에 연락처 관리자 응용 프로그램을 실행할 수 있습니다. 디버깅 시작 메뉴 옵션 디버그을 선택 하거나 간단히 f5 키를 누릅니다. 처음으로 응용 프로그램을 실행 하면 대화 상자를 그림 14에서 가져옵니다. 옵션을 선택 **디버깅을 사용 하려면 Web.config 파일 수정** 확인 단추를 클릭 합니다.


[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image14.jpg)](iteration-1-create-the-application-cs/_static/image27.png)

**그림 14**: 디버깅 사용 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image28.png))


인덱스 보기는 기본적으로 반환 됩니다. 이 보기 연락처 데이터베이스 테이블에서 데이터의 모든를 나열 합니다 (그림 15 참조).


[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image15.jpg)](iteration-1-create-the-application-cs/_static/image29.png)

**그림 15**: The 인덱스 보기 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image30.png))


인덱스 보기 보기의 맨 아래에서 새로 만들기를 레이블이 지정 된 링크가 포함 되어 있는지 확인 합니다. 다음 섹션에서는 새 연락처를 만드는 방법을 알아봅니다.

## <a name="creating-new-contacts"></a>새 연락처 만들기

사용자가 새 연락처를 만들 수 있도록 홈 컨트롤러에 두 create () 작업을 추가 해야 합니다. 새 연락처 만들기에 대 한 HTML 폼을 반환 하는 하나의 create () 작업을 생성 해야 합니다. 새 연락처의 실제 데이터베이스 삽입을 수행 하는 두 번째 create () 작업을 생성 해야 합니다.

홈 컨트롤러에 추가 해야 하는 새로운 create () 메서드는 목록 4에 포함 됩니다.

**4-controllers\ homecontroller.cs (메서드로 만들기)를 나열합니다.**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample4.cs)]

두 번째 create () 메서드는 HTTP POST를 통해서만 호출할 수 있지만 HTTP GET을 사용 하 여 첫 번째 create () 메서드를 호출할 수 있습니다. 즉, HTML 폼 게시 하는 경우에 두 번째 create () 메서드를 호출할 수 있습니다. 첫 번째 create () 메서드는 단순히 새 연락처를 만들기 위한 HTML 양식을 포함 하는 뷰를 반환 합니다. 두 번째 create () 메서드는 훨씬 더 흥미로운: 데이터베이스에 새 연락처를 추가 합니다.

두 번째 create () 메서드 담당자 클래스의 인스턴스를 허용 하도록 수정 되었다는 사실을 알 수 있습니다. HTML 폼 게시 된 양식 값은 자동으로 ASP.NET MVC 프레임 워크에서이 연락처 클래스에 바인딩된 됩니다. 만들 HTML 폼에서 각 폼 필드 연락처 매개 변수의 속성에 할당 됩니다.

문의 매개 변수 [바인딩] 특성으로 데코 레이트 된 있는지 확인 합니다. [바인딩] 특성은 바인딩에서 연락처 Id 속성을 제외 하려면 사용 됩니다. Id 속성 Identity 속성을 나타내기 때문에 Id 속성을 설정 하려면 t 하지 것입니다.

Create () 메서드의 본문에 새 연락처 데이터베이스에 삽입 하는 Entity Framework 사용 됩니다. 새 연락처가 연락처의 기존 집합에 추가 하 고 기본 데이터베이스에 이러한 변경 내용을 다시 푸시할 savechanges () 메서드는 키를 누릅니다.

두 create () 메서드 중 하나를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 하 여 새 연락처 만들기에 대 한 HTML 폼을 생성할 수 있습니다 **뷰 추가** (그림 16 참조).


[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image16.jpg)](iteration-1-create-the-application-cs/_static/image31.png)

**그림 16**: 만들기 뷰 추가 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image32.png))


에 **뷰 추가** 대화 상자에서 선택 합니다 **ContactManager.Models.Contact** 클래스 및 **만들기** 콘텐츠 보기에 대 한 옵션 (그림 17 참조). 클릭할 때 합니다 **추가** 보기를 자동으로 생성 하는 만들기 단추입니다.


[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image17.jpg)](iteration-1-create-the-application-cs/_static/image33.png)

**그림 17**: 분해 하는 페이지가 표시 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image34.png))


만들기 뷰는 각 연락처 클래스의 속성에 대 한 양식 필드를 포함합니다. 뷰 만들기에 대 한 코드 목록 5에 포함 됩니다.

**5-Views\Home\Create.aspx 나열**

[!code-aspx[Main](iteration-1-create-the-application-cs/samples/sample5.aspx)]

Create () 메서드를 수정 하 고 만들기 뷰 추가 후에 연락처 관리자 응용 프로그램을 실행 하 고 새 연락처를 만들 수 있습니다. 클릭 합니다 **새로 만들기** 만들기 뷰를 이동할 인덱스 보기에 표시 되는 링크입니다. 그림 18에서 보기가 표시 됩니다.


[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image18.jpg)](iteration-1-create-the-application-cs/_static/image35.png)

**그림 18**: The Create View ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image36.png))


## <a name="editing-contacts"></a>연락처를 편집합니다.

연락처 레코드를 편집 하기 위한 기능을 추가 하는 것은 새 연락처 레코드를 만들기 위한 기능 추가 매우 비슷합니다. 먼저, 홈 컨트롤러 클래스에 두 개의 새 편집 메서드를 추가 해야 합니다. 이러한 새 되 메서드 목록 6에 포함 됩니다.

**6-(메서드로 편집) controllers\ homecontroller.cs를 나열합니다.**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample6.cs)]

첫 번째 되 메서드는 HTTP GET 작업에서 호출 됩니다. Id 매개 변수를 편집 하 고 연락처 레코드의 Id를 나타내는이 메서드에 전달 됩니다. Entity Framework id와 일치 하는 연락처를 검색 하는 레코드 편집에 대 한 HTML 폼을 포함 하는 보기 반환 됩니다.

두 번째 되 방법은 데이터베이스에 실제 업데이트를 수행 합니다. 이 메서드는 매개 변수로 연락처 클래스의 인스턴스를 허용합니다. ASP.NET MVC 프레임 워크를 바인딩합니다 양식 필드 편집 양식에서이 클래스에 자동으로. 인할 통지 연락처 (에서는 Id 속성의 값이 필요)를 편집 하는 경우 [바인딩] 특성을 포함 합니다.

Entity Framework는 수정 된 연락처 데이터베이스에 저장 하는 데 사용 됩니다. 먼저 원래 연락처 데이터베이스에서 검색 해야 합니다. 다음으로, Entity Framework ApplyPropertyChanges() 메서드 담당자에 게 변경 내용을 기록 하 라고 합니다. 마지막으로, Entity Framework savechanges () 메서드는 기본 데이터베이스에 변경 내용을 유지 하려면 호출 됩니다.

편집 양식 되 메서드를 마우스 오른쪽 단추로 클릭 하 고 추가 보기 메뉴 옵션을 선택 하 여 포함 하는 뷰를 생성할 수 있습니다. 뷰 추가 대화 상자에서 선택 합니다 **ContactManager.Models.Contact** 클래스와 **편집** 콘텐츠 보기 (그림 19 참조).


[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image19.jpg)](iteration-1-create-the-application-cs/_static/image37.png)

**그림 19**:는 편집 뷰 추가 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image38.png))


추가 단추를 클릭 하면 새 편집 뷰를 자동으로 생성 됩니다. 생성 되는 HTML 폼의 각 연락처 클래스 (참조 코드 7)의 속성에 해당 하는 필드를 포함 합니다.

**Listing 7 - Views\Home\Edit.aspx**

[!code-aspx[Main](iteration-1-create-the-application-cs/samples/sample7.aspx)]

## <a name="deleting-contacts"></a>연락처 삭제

연락처를 삭제 하려는 경우 홈 컨트롤러 클래스에 두 delete () 작업을 추가 해야 합니다. 첫 번째 delete () 작업 삭제 확인 양식을 표시 합니다. 두 번째 delete () 작업을 실제 삭제를 수행합니다.

> [!NOTE] 
> 
> 나중에 반복 #7에서는 수정 Contact Manager Ajax 삭제 한 단계를 지원 하도록 해당 합니다.


두 개의 새 delete () 메서드는 목록 8에 포함 됩니다.

**8-controllers\ homecontroller.cs (삭제 메서드)를 나열합니다.**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample8.cs)]

첫 번째 delete () 메서드는 데이터베이스에서 연락처 레코드를 삭제 하는 확인 형태를 반환 합니다. (Figure20 참조). 두 번째 delete () 메서드는 데이터베이스에 대해 실제 삭제 작업을 수행합니다. 원래 연락처 데이터베이스에서 검색 되 면 데이터베이스 삭제 하는 데 Entity Framework DeleteObject() 및 savechanges () 메서드를 호출 됩니다.


[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image20.jpg)](iteration-1-create-the-application-cs/_static/image39.png)

**그림 20**: 삭제 확인 보기로 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image40.png))


(그림 21 참조) 하는 연락처 레코드를 삭제 하는 것에 대 한 링크 포함 되도록 인덱스 뷰를 수정 해야 합니다. 편집 링크를 포함 하는 동일한 테이블 셀에 다음 코드를 추가 해야 합니다.

Html.ActionLink( { id=item.Id }) %&gt;


[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image21.jpg)](iteration-1-create-the-application-cs/_static/image41.png)

**그림 21**: 인덱스 편집 링크를 사용 하 여 뷰 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image42.png))


다음으로, 삭제 확인 보기로 생성 해야 합니다. 홈 컨트롤러 클래스의 delete () 메서드를 마우스 오른쪽 단추로 클릭 하 고 추가 보기 메뉴 옵션을 선택 합니다. 뷰 추가 대화 상자가 나타납니다 (그림 22 참조).

와 달리 목록, 만들기 및 편집 보기의 경우 뷰 추가 대화 상자에 삭제 뷰를 만드는 옵션 대신 선택 합니다 **ContactManager.Models.Contact** 데이터 클래스 및 **빈** 콘텐츠 보기입니다. 콘텐츠 옵션 뷰를 직접 만들 필요는 빈 뷰를 선택 합니다.


[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image22.jpg)](iteration-1-create-the-application-cs/_static/image43.png)

**그림 22**: 삭제 확인 보기로 추가 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image44.png))


삭제 보기의 내용은 나열 하는 9에 포함 됩니다. 이 보기에 확인 하는 양식이 있습니다 (그림 21을 참조 하는 경우)를 삭제 하는 특정 연락처를 여부를 지정 해야 합니다.

**Listing 9 - Views\Home\Delete.aspx**

[!code-aspx[Main](iteration-1-create-the-application-cs/samples/sample9.aspx)]

## <a name="changing-the-name-of-the-default-controller"></a>기본 컨트롤러의 이름 변경

이 연락처를 사용 하 여 작업에 대 한 컨트롤러 클래스의 이름은 HomeController 클래스를 지정 하 고는 문제 될 수 있습니다. 해서는 t 컨트롤러 contact ¡© Controller 이름은?

이 문제는 쉽게 해결할 수 있습니다. 첫째, Home 컨트롤러의 이름을 리팩터링 해야 합니다. HomeController 클래스 Visual Studio 코드 편집기에서 열고, 클래스의 이름을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **이름 바꾸기 리팩터링**합니다. 이 메뉴 옵션을 선택 하면 이름 바꾸기 대화 상자를 엽니다.


[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image23.jpg)](iteration-1-create-the-application-cs/_static/image45.png)

**그림 23**: 컨트롤러 이름 리팩터링 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image46.png))


[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image24.jpg)](iteration-1-create-the-application-cs/_static/image47.png)

**그림 24**: 이름 바꾸기 대화 상자를 사용 하 여 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image48.png))


컨트롤러 클래스의 이름을 바꾸면 Visual Studio의 Views 폴더의 폴더 이름을 업데이트 됩니다. Visual Studio는 \Views\Contact 폴더로 \Views\Home 폴더를 이름을 바꿉니다.

이 변경을 수행한 후 응용 프로그램은 더 이상 Home 컨트롤러를 해야 합니다. 응용 프로그램을 실행 하면 그림 25에서 오류 페이지를 얻게 됩니다.


[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image25.jpg)](iteration-1-create-the-application-cs/_static/image49.png)

**그림 25**: 기본 컨트롤러 없음 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image50.png))


홈 컨트롤러 대신 연락처 컨트롤러를 사용 하려면 Global.asax 파일의 기본 경로 업데이트 해야 합니다. Global.asax 파일을 열고 기본 경로 (참조 코드 10)에 의해 사용 되는 기본 컨트롤러를 수정 합니다.

**10-Global.asax.cs를 나열합니다.**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample10.cs)]

이러한 변경을 수행한 후 Contact Manager 올바르게 실행 됩니다. 이제 연락처 컨트롤러 클래스 기본 컨트롤러로 사용 됩니다.

## <a name="summary"></a>요약

이 첫 번째 반복에서 기본 연락처 관리자 응용 프로그램에서에서 만든 가장 빠른 방법은 가능 합니다. 이 컨트롤러 및 뷰에 대 한 초기 코드를 자동으로 생성 하려면 Visual Studio를 활용을 했습니다. 데이터베이스 모델 클래스를 자동으로 생성 하려면 엔터티 프레임 워크를 활용을 했습니다.

현재에서는 수 목록, 만들기, 편집 및 연락처 관리자 응용 프로그램을 사용 하 여 연락처 레코드를 삭제 합니다. 즉, 모든 데이터베이스 기반 웹 응용 프로그램에 필요한 기본 데이터베이스 작업을 수행할 수 있습니다.

그러나 응용 프로그램에 몇 가지 문제가 있습니다. 첫 번째 고 언제 든 지이 인정, 연락처 관리자 응용 프로그램의 가장 매력적인 응용 프로그램이 아닙니다. 일부 디자인 작업을 해야합니다. 다음 반복에서 기본 보기 마스터 페이지 및 응용 프로그램의 모양을 개선 하기 위해 연계 스타일 시트를 변경할 수 있습니다 하는 방법을 살펴보겠습니다.

둘째, 양식 유효성 검사를 구현 하지 않았습니다. 예를 들어 없는 양식 필드에 대 한 값을 입력 하지 않고 만들기 연락처 양식을 제출 하지 못하도록 됩니다. 또한 잘못 된 전화 번호 및 전자 메일 주소를 입력할 수 있습니다. 반복 # 3에서에서 양식 유효성 검사의 문제를 해결 하기 시작 합니다.

마지막으로, 가장 중요 한 점은 연락처 관리자 응용 프로그램의 현재 반복 하거나 수 없습니다 쉽게 수정 유지 관리 합니다. 예를 들어, 데이터베이스 액세스 논리는 컨트롤러 작업에 오른쪽을 반영 됩니다. 이 컨트롤러를 수정 하지 않고 데이터 액세스 코드를 수정할 수 없습니다 것을 의미 합니다. 이후 반복에서는 복원 력을 연락처 관리자를 변경 하려면를 구현할 수 있습니다 하는 소프트웨어 디자인 패턴을 알아봅니다.

> [!div class="step-by-step"]
> [다음](iteration-2-make-the-application-look-nice-cs.md)
