---
uid: mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-vb
title: '반복 #1 – (VB) 응용 프로그램 만들기 | Microsoft Docs'
author: microsoft
description: '첫 번째 반복에서는 만듭니다 연락처 관리자에는 가장 간단한 방법은 가능한. 기본적인 데이터베이스 작업에 대 한 지원을 추가 하 여: 만들기, 읽기, 업데이트 및 D....'
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2009
ms.topic: article
ms.assetid: 5b033582-1646-42c2-b20d-7edc8814e970
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-vb
msc.type: authoredcontent
ms.openlocfilehash: 52029816bd9f37c3d5c3321d3c5e60599314a33b
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30877062"
---
<a name="iteration-1--create-the-application-vb"></a>반복 #1 – (VB) 응용 프로그램 만들기
====================
by [Microsoft](https://github.com/microsoft)

[코드 다운로드](iteration-1-create-the-application-vb/_static/contactmanager_1_vb1.zip)

> 첫 번째 반복에서는 만듭니다 연락처 관리자에는 가장 간단한 방법은 가능한. 기본적인 데이터베이스 작업에 대 한 지원을 추가 하 여: 만들기, 읽기, 업데이트 및 삭제 (CRUD).


## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>연락처 관리 ASP.NET MVC 응용 프로그램 (VB) 빌드

이 일련의 자습서에서는 전체 연락처 관리 응용을 프로그램의 시작 끝나기를 빌드합니다. 관리자에 게 문의 응용 프로그램을 사람 목록에 대 한 사용-이름, 전화 번호 및 전자 메일 주소-연락처 정보를 저장할 수 있습니다.

여러 반복을 통해에 응용 프로그램을 빌드합니다. 각 반복에서 점진적으로 응용 프로그램을 개선 했습니다. 이 여러 개의 반복 접근 방법의 목적은 각 변경의 이유를 이해 하는 데 사용할 수 있도록 하는 것입니다.

- 반복 #1-응용 프로그램을 만듭니다. 첫 번째 반복에서는 만듭니다 연락처 관리자에는 가장 간단한 방법은 가능한. 기본적인 데이터베이스 작업에 대 한 지원을 추가 하 여: 만들기, 읽기, 업데이트 및 삭제 (CRUD).

- 반복 #2-모양이 아닌 응용 프로그램을 확인 합니다. 이 반복에서 기본 ASP.NET MVC 뷰 마스터 페이지를 수정 및 스타일 시트를 연계 하 여 응용 프로그램의 모양을 개선 합니다.

- 반복 #3-폼 유효성 검사를 추가 합니다. 세 번째 반복에서 기본적인 형태의 유효성 검사를 추가 했습니다. म 중이거나 사용자에서 필수 양식 필드를 완료 하지 않고 폼을 제출 합니다. 또한 전자 메일 주소, 전화 번호를 확인 합니다.

- 반복 #4-느슨하게 결합 된 응용 프로그램을 확인 합니다. 이 세 번째 반복에서 우리 활용 여러 가지 소프트웨어 디자인 패턴을 쉽게 유지 관리 하 고 않아 응용 프로그램을 수정 합니다. 예를 들어 리팩터링한 리포지토리 패턴 및 종속성 주입 패턴을 사용 하도록 응용 프로그램입니다.

- 반복 #5-단위 테스트를 만듭니다. 다섯 번째 반복에서 하도록 응용 프로그램이 쉽게 유지 관리 및 단위 테스트를 추가 하 여 수정 합니다. 데이터 모델 클래스를 모의 하 고 우리의 컨트롤러 및 유효성 검사 논리에 대 한 단위 테스트를 작성 합니다.

- 반복 6-테스트 기반 개발을 사용 합니다. 이 6 번째 반복에서에서는 새 기능을 추가할 응용 프로그램 먼저 단위 테스트를 작성 하 고 단위 테스트에 대해 코드를 작성 합니다. 이 반복 메일 그룹을 추가합니다.

- 반복 #7-Ajax 기능을 추가 합니다. 일곱 번째 반복에서 개선할 응용 프로그램의 성능과 응답성 ajax 지원을 추가 하 여 합니다.

## <a name="this-iteration"></a>이 반복

이 첫 번째 반복에서 기본적인 응용 프로그램을 빌드합니다. 목표 가능한 빠르고 간편한 방식으로 연락처 관리자를 빌드하는 것입니다. 이후 반복에서 응용 프로그램의 디자인을 향상 합니다.

않아 응용 프로그램은 기본 데이터베이스 기반 응용 프로그램. 새 연락처를 만들고 기존 연락처를 편집 하 고 연락처를 삭제 하는 응용 프로그램을 사용할 수 있습니다.

이 반복에서 다음 단계를 완료 했습니다.

1. ASP.NET MVC 응용 프로그램
2. 이 연락처를 저장 하기 위한 데이터베이스 만들기
3. Microsoft Entity Framework와 함께 데이터베이스에 대 한 모델 클래스를 생성 합니다.
4. 컨트롤러 동작 및 모든 데이터베이스에 연락처를 나열할 수 있도록 하는 보기 만들기
5. 컨트롤러 작업 및 데이터베이스에 새 연락처를 만들 수 있도록 하는 뷰 만들기
6. 컨트롤러 작업 및 데이터베이스에 있는 기존 연락처를 편집할 수 있도록 해 주는 보기
7. 컨트롤러 작업 및 데이터베이스에 있는 기존 연락처를 삭제할 수 있게 하는 보기 만들기

## <a name="software-prerequisites"></a>소프트웨어 필수 구성 요소

ASP.NET MVC 응용 프로그램에서 Visual Studio 2008 또는 Visual Web Developer 2008 (Visual Web Developer는 Visual Studio의 고급 기능 중 일부가 포함 되지 않은 Visual Studio의 무료 버전) 컴퓨터에 설치 되어 있어야 합니다. 다음 주소에서 Visual Studio 2008의 평가판 버전 또는 Visual Web Developer를 다운로드할 수 있습니다.

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

> [!NOTE] 
> 
> Visual Web Developer와 ASP.NET MVC 응용 프로그램에 대 한 설치 된 Visual Web Developer 서비스 팩 1이 있어야 합니다. 서비스 팩 1 없이 웹 응용 프로그램 프로젝트를 만들 수 없습니다.


ASP.NET MVC 프레임 워크입니다. 다음 주소에서 ASP.NET MVC 프레임 워크를 다운로드할 수 있습니다.

[https://www.asp.net/mvc](../../../index.md)

이 자습서에서는 데이터베이스에 액세스 하려면 Microsoft Entity Framework를 사용 했습니다. Entity Framework는.NET Framework 3.5 서비스 팩 1 포함 되어 있습니다. 다음 위치에서이 서비스 팩을 다운로드할 수 있습니다.

[https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;displaylang=en](https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;displaylang=en)

이러한 다운로드 한 각 수행 하는 대신, 웹 플랫폼 설치 관리자 (웹 PI)를 활용할 수 있습니다. 다음 주소에서 웹 PI를 다운로드할 수 있습니다.

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

## <a name="aspnet-mvc-project"></a>ASP.NET MVC Project

ASP.NET MVC 웹 응용 프로그램 프로젝트입니다. Visual Studio를 시작 하 고 메뉴 옵션을 선택 **파일, 새 프로젝트**합니다. **새 프로젝트** (그림 1 참조) 대화 상자가 나타납니다. 선택 된 **웹** 프로젝트 형식 및 **ASP.NET MVC 웹 응용 프로그램** 템플릿. 새 프로젝트 이름을 *ContactManager* 확인 단추를 클릭 합니다.


.NET Framework 3.5가 맨 위에 있는 드롭다운 목록에서 선택 했는지 확인의 오른쪽은 **새 프로젝트** 대화 상자. 그렇지 않으면 t 성공한 ASP.NET MVC 웹 응용 프로그램 템플릿을 표시 합니다.


[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image1.jpg)](iteration-1-create-the-application-vb/_static/image1.png)

**그림 01**:의 새 프로젝트 대화 상자 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image2.png))


ASP.NET MVC 응용 프로그램의 **단위 테스트 프로젝트 만들기** 대화 상자가 나타납니다. 이 대화 상자를 만들고 ASP.NET MVC 응용 프로그램을 만들 때 솔루션에 단위 테스트 프로젝트를 추가 지정할 사용할 수 있습니다. T 성공한 있지만이 반복의 단위 테스트를 작성 하는 옵션을 선택 해야 **예, 단위 테스트 프로젝트 만들기** 이후의 반복에서 단위 테스트 추가 계획 이기 때문에 있습니다. 새 ASP.NET MVC 프로젝트를 처음 만들 때 테스트 프로젝트를 추가 합니다. ASP.NET MVC 프로젝트를 만든 후에 테스트 프로젝트를 추가 하는 보다 훨씬 쉽습니다.

> [!NOTE] 
> 
> Visual Web Developer에서 테스트 프로젝트를 지원 하지 않으므로 Visual Web Developer를 사용 하는 경우 단위 테스트 프로젝트 만들기 대화 상자를 발생 하지 않습니다.


[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image2.jpg)](iteration-1-create-the-application-vb/_static/image3.png)

**그림 02**: The 단위 테스트 프로젝트 만들기 대화 상자 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image4.png))


ASP.NET MVC 응용 프로그램 Visual Studio 솔루션 탐색기 창에 표시 됩니다 (그림 3 참조). T don 메뉴 옵션을 선택 하 여이 창을 열 수 있습니다 다음 솔루션 탐색기 창 표시 **보기, 솔루션 탐색기**합니다. 두 개의 프로젝트가 솔루션에 공지: ASP.NET MVC 프로젝트와 테스트 프로젝트입니다. ASP.NET MVC 프로젝트 ContactManager 이름이 하 고 테스트 프로젝트 이름은 ContactManager.Tests 합니다.


[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image3.jpg)](iteration-1-create-the-application-vb/_static/image5.png)

**그림 03**: 솔루션 탐색기 창 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image6.png))


## <a name="deleting-the-project-sample-files"></a>프로젝트 샘플 파일 삭제

ASP.NET MVC 프로젝트 템플릿은 컨트롤러 및 뷰에 대 한 샘플 파일을 포함합니다. 새 ASP.NET MVC 응용 프로그램을 만들기 전에 이러한 파일을 삭제 해야 합니다. 파일 또는 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 하 여 솔루션 탐색기 창에서 파일 및 폴더를 삭제할 수 있습니다 **삭제**합니다.

ASP.NET MVC 프로젝트에서 다음 파일을 삭제 해야 합니다.

- \Controllers\HomeController.vb

- \Views\Home\About.aspx

- \Views\Home\Index.aspx

및 테스트 프로젝트에서 다음 파일을 삭제 해야 합니다.

\Controllers\HomeControllerTest.vb

## <a name="creating-the-database"></a>데이터베이스를 만드는 중

않아 응용 프로그램은 데이터베이스 기반 웹 응용 프로그램. 상점 연락처 정보를 위해 데이터베이스를 사용 합니다.

Microsoft SQL Server, Oracle, MySQL 및 IBM DB2 데이터베이스를 비롯 한 최신 데이터베이스와 ASP.NET MVC 프레임 워크입니다. 이 자습서에서는 Microsoft SQL Server 데이터베이스를 사용 했습니다. Visual Studio를 설치 하면 Microsoft SQL Server 데이터베이스의 무료 버전인 Microsoft SQL Server Express를 설치 하는 옵션이 제공 됩니다.

응용 프로그램을 마우스 오른쪽 단추로 클릭 하 여 새 데이터베이스를 만들\_메뉴 옵션을 선택 하 고 솔루션 탐색기 창에서 데이터 폴더 **추가, 새 항목**합니다. 에 **새 항목 추가** 대화 상자에서는 **데이터** 범주 및 **SQL Server 데이터베이스** 서식 파일 (그림 4 참조). ContactManagerDB.mdf 새 데이터베이스 이름을 지정 하 고 확인 단추를 클릭 합니다.


[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image4.jpg)](iteration-1-create-the-application-vb/_static/image7.png)

**그림 04**: 새 Microsoft SQL Server Express 데이터베이스 만들기 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image8.png))


데이터베이스 응용 프로그램에 표시 되는 새 데이터베이스를 만든 후\_솔루션 탐색기 창에서 데이터 폴더. 서버 탐색기 창을 열고 데이터베이스에 연결 하려면 ContactManager.mdf 파일을 두 번 클릭 합니다.

> [!NOTE] 
> 
> 서버 탐색기 창에서 Microsoft Visual Web Developer의 경우 데이터베이스 탐색기 창에 호출 됩니다.


데이터베이스 테이블, 뷰, 트리거, 저장된 프로시저와 같은 새 데이터베이스 개체를 만들 서버 탐색기 창에서 사용할 수 있습니다. 테이블 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **새 테이블 추가**합니다. 데이터베이스 테이블 디자이너 (그림 5 참조)가 나타납니다.


[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image5.jpg)](iteration-1-create-the-application-vb/_static/image9.png)

**그림 05**: 데이터베이스 테이블 디자이너 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image10.png))


같은 열이 포함 된 테이블을 생성 해야 합니다.

<a id="0.2_table01"></a>


| **열 이름** | **데이터 형식** | **Null 허용** |
| --- | --- | --- |
| ID | int | False |
| FirstName | nvarchar(50) | False |
| LastName | nvarchar(50) | False |
| 전화 번호 | nvarchar(50) | False |
| 메일 | nvarchar(255) | False |


첫 번째 열, Id 열은 특별 합니다. Id 열을 Id 열 및 기본 키 열으로 표시 해야 합니다. 열 속성 (그림 6의 맨 아래에 검색)를 확장 하 고 Id 사양 속성 아래로 스크롤 하 여 열이 Identity 열 임을 나타낼 있습니다. 설정의 **(Id)** 속성 값을 **예**합니다.

열을 선택 하는 키 아이콘이 있는 단추를 클릭 하 여 기본 키 열으로 열을 표시 합니다. 열은 기본 키 열으로 표시 되 면 키 아이콘이 열 옆에 나타납니다 (그림 6 참조).

테이블 생성을 완료 한 후 새 테이블을 저장 하려면 저장 단추 (플로피의 아이콘이 있는 단추)를 클릭 합니다. 새 테이블 이름을 *연락처*합니다.

연락처 데이터베이스 테이블 만들기를 클릭 한 후 테이블에 일부 레코드를 추가 해야 합니다. 서버 탐색기 창에서 Contacts 테이블을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **테이블 데이터 표시**합니다. 에 표시 된 표에서 하나 이상의 연락처를 입력 합니다.

## <a name="creating-the-data-model"></a>데이터 모델 만들기

ASP.NET MVC 응용 프로그램 모델, 뷰 및 컨트롤러 구성 됩니다. 이전 섹션에서 만든 연락처 테이블을 나타내는 모델 클래스를 만들어 시작 합니다.

이 자습서에서 사용 하 여 Microsoft Entity Framework 데이터베이스에서 모델 클래스를 자동으로 생성 합니다.

> [!NOTE] 
> 
> ASP.NET MVC 프레임 워크는 어떤 방식으로든에서 Microsoft Entity Framework 연결 되지 않습니다. ASP.NET MVC와 LINQ to SQL 또는 ADO.NET NHibernate를 포함 하 여 다른 데이터베이스 액세스 기술을 사용할 수 있습니다.


데이터 모델 클래스를 만드는 다음이 단계를 수행 합니다.

1. 솔루션 탐색기 창에 모델 폴더를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가, 새 항목**합니다. **새 항목 추가** (그림 6 참조) 대화 상자가 나타납니다.
2. 선택 된 **데이터** 범주 및 **ADO.NET 엔터티 데이터 모델** 템플릿. 데이터 모델 이름을 *ContactManagerModel.edmx* 클릭는 **추가** 단추입니다. 엔터티 데이터 모델 마법사 (그림 7 참조)가 나타납니다.
3. 에 **모델 콘텐츠 선택** 단계에서는 **데이터베이스에서 생성** (그림 7 참조).
4. 에 **데이터 연결 선택** 단계 ContactManagerDB.mdf 데이터베이스를 선택 하 고 이름을 입력 *ContactManagerDBEntities* 엔터티 연결 설정 (그림 8 참조).
5. 에 **데이터베이스 개체 선택** 단계, 테이블 (그림 9 참조) 확인란을 선택 합니다. 데이터 모델 (에 하나 또는 Contacts 테이블) 데이터베이스에 포함 된 모든 테이블이 포함 됩니다. 네임 스페이스를 입력 *모델*합니다. 마법사를 완료 하려면 "마침" 단추를 클릭 합니다.


[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image6.jpg)](iteration-1-create-the-application-vb/_static/image11.png)

**그림 06**: 새 항목 추가 대화 상자 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image12.png))


[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image7.jpg)](iteration-1-create-the-application-vb/_static/image13.png)

**그림 07**: Model 콘텐츠 선택 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image14.png))


[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image8.jpg)](iteration-1-create-the-application-vb/_static/image15.png)

**그림 08**: 데이터 연결 선택 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image16.png))


[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image9.jpg)](iteration-1-create-the-application-vb/_static/image17.png)

**그림 09**: 데이터베이스 개체 선택 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image18.png))


엔터티 데이터 모델 마법사를 완료 한 후에 엔터티 데이터 모델 디자이너 나타납니다. 디자이너 모델링 되 고 각 테이블에 해당 하는 클래스를 표시 합니다. 연락처 라는 하나의 클래스에 표시 됩니다.

엔터티 데이터 모델 마법사를 데이터베이스 테이블 이름에 따라 클래스 이름을 생성 합니다. 거의 항상 마법사에서 생성 되는 클래스의 이름을 변경 해야 합니다. 연락처 클래스 디자이너에서 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **이름 바꾸기**합니다. 클래스의 이름을 연락처 (복수)에서 연락처 (단 수)를 변경 합니다. 클래스 이름을 변경 하 고 나면 그림 10과 같은 클래스가 표시 됩니다.


[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image10.jpg)](iteration-1-create-the-application-vb/_static/image19.png)

**그림 10**: Contact The 클래스 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image20.png))


이 시점에서 예제의 데이터베이스 모델을 만들었습니다. 데이터베이스에 특정 연락처 레코드를 나타내기 위해 연락처 클래스를 사용할 수 있습니다.

## <a name="creating-the-home-controller"></a>홈 컨트롤러 만들기

다음 단계는 우리의 Home 컨트롤러를 만드는 것입니다. Home 컨트롤러는 ASP.NET MVC 응용 프로그램에서 호출 되는 기본 컨트롤러입니다.

솔루션 탐색기 창에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 하 여 홈 컨트롤러 클래스 만들기 **추가, 컨트롤러** (11 그림 참조). 확인란 확인 **만들기, 업데이트 및 세부 정보 시나리오에 대 한 작업 메서드를 추가**합니다. 클릭 하기 전에 선택 되어 있는지 확인은 **추가** 단추입니다.


[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image11.jpg)](iteration-1-create-the-application-vb/_static/image21.png)

**그림 11**: Home 컨트롤러를 추가 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image22.png))


Home 컨트롤러를 만들 때에 목록 1의 클래스를 가져옵니다.

**Listing 1 - Controllers\HomeController.vb**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample1.vb)]

## <a name="listing-the-contacts"></a>연락처를 나열합니다.

연락처 데이터베이스 테이블에 레코드를 표시 하려면 index () 작업 및 인덱스 보기 해야 합니다.

Home 컨트롤러 index () 작업을 이미 있습니다. 이 메서드를 나열 하는 2의 모양 수정 해야 합니다.

**Listing 2 - Controllers\HomeController.vb**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample2.vb)]

목록 2의 홈 컨트롤러 클래스 라는 private 필드가 들어 \_엔터티. \_엔터티 필드의 데이터 모델에서 엔터티를 나타냅니다. 사용 하 여는 \_엔터티 필드는 데이터베이스와 통신할 수 있습니다.

Index () 메서드를 나타내는 모든 연락처 연락처 데이터베이스 테이블 뷰를 반환 합니다. 식 \_엔터티. ContactSet.ToList() 제네릭 목록으로 연락처 목록을 반환합니다.

해당 म 것은 사용 이제 했습니다 인덱스 컨트롤러를 만든 다음 인덱스 뷰를 만들 필요 합니다. 인덱스 뷰를 만들기 전에 메뉴 옵션을 선택 하 여 응용 프로그램을 컴파일하 **빌드, 솔루션 빌드**합니다. 모델 클래스 목록에 표시 하려면 보기를 추가 하기 전에 프로젝트를 컴파일하여 항상는 **뷰 추가** 대화 상자.

Index () 메서드를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 하 여 인덱스 뷰를 만들면 **뷰 추가** (그림 12 참조). 이 메뉴 옵션을 선택 하면 열립니다는 **뷰 추가** 대화 상자 (그림 13 참조).


[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image12.jpg)](iteration-1-create-the-application-vb/_static/image23.png)

**그림 12**: 인덱스 뷰 추가 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image24.png))


에 **뷰 추가** 대화 상자에서 확인란 확인 **강력한 형식의 뷰 만들기**합니다. 데이터 클래스 ContactManager.Contact 보기와 보기 콘텐츠 목록을 선택 합니다. 이러한 옵션을 선택 하면 연락처 레코드를 표시 하는 보기를 생성 합니다.


[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image13.jpg)](iteration-1-create-the-application-vb/_static/image25.png)

**그림 13**: 뷰 추가 대화 상자 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image26.png))


클릭는 **추가** 단추, 목록 3에서 인덱스 뷰 생성 됩니다. 공지는 &lt;% @ 페이지 %&gt; 지시문을 파일의 맨 위에 나타납니다. 인덱스 뷰는 ViewPage에서 상속&lt;IEnumerable&lt;ContactManager.Models.Contact&gt; &gt; 클래스입니다. 즉, 보기에서 모델 클래스 연락처 엔터티 목록을 나타냅니다.

인덱스 뷰의 본문 모델 클래스를 나타내는 연락처의 각 반복 하는 foreach 루프를 포함 합니다. 연락처 클래스의 각 속성의 값은 HTML 테이블 내에서 표시 됩니다.

**3-Views\Home\Index.aspx (수정 되지 않은)를 나열 합니다.**

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample3.aspx)]

가지 인덱스 뷰를 수정 해야 합니다. 세부 정보 보기를 만드는 하지 것 때문에 세부 정보 링크를 제거할 수 있습니다. 찾기 및 인덱스 보기에서 다음 코드를 제거 합니다.

{.id = item.Id})%&gt;

인덱스 뷰를 수정한 후에 연락처 관리자 응용 프로그램을 실행할 수 있습니다. 디버깅 시작 메뉴 옵션 디버그을 선택 하거나 단순히 F5 키를 누릅니다. 처음에 응용 프로그램을 실행할 때 얻게 대화 상자 그림 14에서입니다. 옵션을 선택 **디버깅할 수 있도록 Web.config 파일을 수정** 확인 단추를 클릭 합니다.


[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image14.jpg)](iteration-1-create-the-application-vb/_static/image27.png)

**그림 14**: 디버깅 사용 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image28.png))


인덱스 뷰는 기본적으로 반환 됩니다. 이 보기의 모든 연락처 데이터베이스 테이블에서 데이터를 나열 합니다 (그림 15 참조).


[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image15.jpg)](iteration-1-create-the-application-vb/_static/image29.png)

**그림 15**: The 인덱스 보기 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image30.png))


인덱스 뷰 보기의 맨 아래에 새로 만들기를 레이블이 지정 된 링크가 포함 되어 있는지 확인 합니다. 다음 섹션에서는 새 연락처를 만드는 방법을 설명 합니다.

## <a name="creating-new-contacts"></a>새 연락처 만들기

사용자가 새 연락처를 만들 수 있도록 홈 컨트롤러에 두 개의 create () 작업을 추가 해야 합니다. 새 연락처를 만들기 위한 HTML 폼을 반환 하는 하나의 create () 동작을 만들려면 해야 합니다. 새 연락처의 실제 데이터베이스 삽입을 수행 하는 두 번째 create () 작업을 만들기 위해 필요 합니다.

홈 컨트롤러에 추가 해야 하는 새 create () 메서드 목록 4에 포함 됩니다.

**4-Controllers\HomeController.vb (메서드로 만들기)를 나열합니다.**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample4.vb)]

HTTP POST에서만 두 번째 create () 메서드를 호출할 수 있습니다 하는 동안 HTTP GET와 첫 번째 create () 메서드를 호출할 수 있습니다. 즉, HTML 폼 게시 하는 경우에 두 번째 create () 메서드를 호출할 수 있습니다. 첫 번째 create () 메서드는 단순히 새 연락처를 만들기 위한 HTML 폼을 포함 하는 뷰를 반환 합니다. 두 번째 create () 메서드는 훨씬 더 흥미로운: 데이터베이스에 새 연락처를 추가 합니다.

공지를 두 번째 create () 메서드는 연락처 클래스의 인스턴스를 허용 하도록 수정 되었습니다. HTML 양식 으로부터 게시 된 양식 값은 자동으로 ASP.NET MVC 프레임 워크에서이 연락처 클래스에 바인딩된 됩니다. 양식 HTML 만들기에서 각 양식 필드의 연락처 매개 변수 속성에 할당 됩니다.

연락처 매개 변수 [바인드] 특성으로 데코레이팅되 어 있는지를 확인 합니다. 바인딩에서 연락처 Id 속성을 제외 하려면 [Bind] 속성 사용 됩니다. Id 속성 Identity 속성을 나타내므로 Id 속성을 설정 하려면 원하지를 않는 했습니다.

Create () 메서드 본문에서 Entity Framework 데이터베이스에 새 연락처 삽입에 사용 됩니다. 새 연락처가 연락처의 기존 세트에 추가 하 고 savechanges () 메서드를 호출 기본 데이터베이스에 이러한 변경 내용 다시 적용 하 합니다.

두 create () 방법 중 하나를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 하 여 새 연락처 만들기에 대 한 HTML 폼을 생성할 수 있습니다 **뷰 추가** (16 그림 참조).


[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image16.jpg)](iteration-1-create-the-application-vb/_static/image31.png)

**그림 16**: 만들기 뷰 추가 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image32.png))


에 **뷰 추가** 대화 상자에서는 **ContactManager.Contact** 클래스 및 **만들기** 콘텐츠 보기에 대 한 옵션 (그림 17 참조). 클릭는 **추가** 단추는 Create view 자동으로 생성 됩니다.


[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image17.jpg)](iteration-1-create-the-application-vb/_static/image33.png)

**그림 17**: 분해 페이지가 표시 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image34.png))


만들기 뷰는 각 연락처 클래스의 속성에 대 한 양식 필드를 포함합니다. 뷰 만들기에 대 한 코드 목록 5에 포함 됩니다.

**Listing 5 - Views\Home\Create.aspx**

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample5.aspx)]

Create () 메서드를 수정 하 고 만들기 뷰 추가 후에 연락처 Manger 응용 프로그램을 실행 하 고 새 연락처를 만들 수 있습니다. 클릭는 **새로 만들기** 만들기 보기로 이동 하도록 인덱스 보기에 표시 되는 링크입니다. 그림 18에서 보기를 확인 해야 합니다.


[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image18.jpg)](iteration-1-create-the-application-vb/_static/image35.png)

**그림 18**: The Create View ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image36.png))


## <a name="editing-contacts"></a>연락처를 편집합니다.

연락처 레코드를 편집 하기 위한 기능 추가 기능 새 연락처 레코드를 만들기 위한 매우 비슷합니다. 먼저, 홈 컨트롤러 클래스에 두 개의 새 편집 메서드를 추가 해야 합니다. 이러한 새 Edit() 메서드 목록 6에 포함 됩니다.

**6-Controllers\HomeController.vb (메서드로 편집)를 나열합니다.**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample6.vb)]

첫 번째 Edit() 메서드는 HTTP GET 작업에서 호출 됩니다. Id 매개 변수를 편집 하 고 연락처 레코드의 Id를 나타내는이 메서드에 전달 됩니다. Entity Framework는 id와 일치 하는 연락처를 검색 하는 데 사용 됩니다. 레코드 편집에 대 한 HTML 폼을 포함 하는 뷰 반환 됩니다.

두 번째 Edit() 메서드는 데이터베이스에 대 한 실제 업데이트를 수행합니다. 이 메서드는 연락처 클래스의 인스턴스를 매개 변수로 받아들입니다. ASP.NET MVC 프레임 워크가 바인딩합니다 양식 필드 편집 폼에서이 클래스에 자동으로. T 않으려는 공지 (Id 속성의 값 필요) 연락처를 편집할 때 [바인드] 특성을 포함 합니다.

Entity Framework는 수정 된 연락처 데이터베이스에 저장 하는 데 사용 됩니다. 원래 연락처를 데이터베이스에서 먼저 검색 해야 합니다. 다음으로, Entity Framework ApplyPropertyChanges() 메서드 연락처에 변경 내용을 기록할 호출 됩니다. 마지막으로, Entity Framework savechanges () 메서드는 기본 데이터베이스에 변경 내용을 유지 합니다.

Edit() 메서드를 마우스 오른쪽 단추로 클릭 하 고 추가 보기 메뉴 옵션을 선택 하 여 편집 폼을 포함 하는 보기를 생성할 수 있습니다. 뷰 추가 대화 상자에서 선택 된 **ContactManager.Models.Contact** 클래스 및 **편집** 콘텐츠를 볼 (그림 19 참조).


[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image19.jpg)](iteration-1-create-the-application-vb/_static/image37.png)

**그림 19**: 편집 뷰 추가 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image38.png))


추가 단추를 클릭 하면 새 편집 뷰를 자동으로 생성 됩니다. 생성 되는 HTML 폼에는 각 연락처 클래스 (참조 목록 7)의 속성에 해당 하는 필드가 포함 됩니다.

**Listing 7 - Views\Home\Edit.aspx**

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample7.aspx)]

## <a name="deleting-contacts"></a>연락처 삭제

연락처를 삭제 하려면 홈 컨트롤러 클래스에 두 개의 delete () 작업을 추가 해야 합니다. 첫 번째 delete () 작업 삭제 확인 폼이 표시 됩니다. 두 번째 delete () 동작 실제 삭제를 수행합니다.

> [!NOTE] 
> 
> 이상 버전에서는 반복 #7에서는 Contact Manager 되도록 수정 Ajax 삭제 한 단계를 지원 합니다.


두 개의 새 delete () 메서드 목록 8에 포함 됩니다.

**8-Controllers\HomeController.vb (삭제 메서드)를 나열합니다.**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample8.vb)]

데이터베이스에서 연락처 레코드를 삭제 하기 위한 확인 형태를 반환 하는 첫 번째 delete () 메서드 (Figure20 참조). 두 번째 delete () 메서드는 데이터베이스에 대해 실제 삭제 작업을 수행합니다. 데이터베이스에서 검색 되 면 원래 연락처 후 데이터베이스 삭제 작업을 수행 Entity Framework DeleteObject() 및 savechanges () 메서드 호출 됩니다.


[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image20.jpg)](iteration-1-create-the-application-vb/_static/image39.png)

**그림 20**: 삭제 확인 뷰 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image40.png))


(그림 21 참조) 연락처 레코드를 삭제 하기 위한 링크를 포함 하도록 인덱스 뷰를 수정 해야 합니다. 편집 링크를 포함 하는 동일한 테이블 셀에 다음 코드를 추가 해야 합니다.

{.id = item.Id})%&gt;


[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image21.jpg)](iteration-1-create-the-application-vb/_static/image41.png)

**그림 21**: 편집 링크가 있는 뷰 인덱스 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image42.png))


다음으로, 삭제 확인 뷰를 생성 해야 합니다. 홈 컨트롤러 클래스에서 delete () 메서드를 마우스 오른쪽 단추로 클릭 하 고 추가 보기 메뉴 옵션을 선택 합니다. 뷰 추가 대화 상자가 나타나면 (그림 22 참조).

와 달리 목록, 만들기 및 편집 보기의 경우 뷰 추가 대화 상자에 삭제 뷰를 만드는 옵션을 대신, 선택는 **ContactManager.Models.Contact** 데이터 클래스 및 **빈** 콘텐츠를 볼 합니다. 에서는 콘텐츠 옵션 보기를 직접 만들 수 빈 뷰를 선택 합니다.


[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image22.jpg)](iteration-1-create-the-application-vb/_static/image43.png)

**그림 22**: 삭제 확인 뷰 추가 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image44.png))


Delete 보기의 내용은 목록 9에 포함 됩니다. 이 뷰를 확인 하는 양식을 포함 여부는 특정 연락처 해야 삭제할 (그림 21 참조).

**Listing 9 - Views\Home\Delete.aspx**

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample9.aspx)]

## <a name="changing-the-name-of-the-default-controller"></a>기본 컨트롤러의 이름 변경

그 연락처를 사용 하기 위한 컨트롤러 클래스의 이름은 HomeController 클래스 이름이 이라고 문제 수 있습니다. 이내에 사용 해야 t 컨트롤러 ContactController 이름은?

이 문제는 쉽게 수정할 수 있습니다. 먼저, Home 컨트롤러의 이름을 리팩터링 해야 합니다. HomeController 클래스에 Visual Studio 코드 편집기에서 열고 클래스의 이름을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **이름 바꾸기**합니다. 이 메뉴 옵션을 선택 하면 이름 바꾸기 대화 상자를 엽니다.


[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image23.jpg)](iteration-1-create-the-application-vb/_static/image45.png)

**그림 23**: 컨트롤러 이름 리팩터링 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image46.png))


[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image24.jpg)](iteration-1-create-the-application-vb/_static/image47.png)

**그림 24**: 이름 바꾸기 대화 상자를 사용 하 여 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image48.png))


컨트롤러 클래스의 이름을 바꾸면 하는 경우 Visual Studio도 뷰 폴더에 폴더 이름을 업데이트 합니다. Visual Studio \Views\Contact 폴더로 \Views\Home 폴더를 이름은지 것입니다.

이 변경을 수행한 후 응용 프로그램은 더 이상 Home 컨트롤러를 갖습니다. 응용 프로그램을 실행 하는 경우에 그림 25에서 오류 페이지를 볼 수 있습니다.


[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image25.jpg)](iteration-1-create-the-application-vb/_static/image49.png)

**그림 25**: 기본 컨트롤러 없음 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image50.png))


홈 컨트롤러 대신 연락처 컨트롤러를 사용 하도록 Global.asax 파일에 기본 경로 업데이트 해야 합니다. Global.asax 파일을 열고 기본 경로 (참조 목록 10)에 의해 사용 되는 기본 컨트롤러를 수정 합니다.

**10-Global.asax.vb 나열**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample10.vb)]

이러한 변경을 수행한 후 Contact Manager 제대로 실행 됩니다. 이제, 연락처 컨트롤러 클래스 기본 컨트롤러도 사용 됩니다.

## <a name="summary"></a>요약

이 첫 번째 반복에서 기본적인 않아 응용 프로그램에서에서 만든는 가장 빠른 방법은 가능 합니다. 이 컨트롤러 및 뷰에 대 한 초기 코드를 자동으로 생성 하도록 Visual Studio의 순서로 합니다. 데이터베이스 모델 클래스를 자동으로 생성 하려면 Entity Framework의 순서로 합니다.

현재 나열 하 고 만들기 하 고 편집 수 있으며 관리자에 게 문의 응용 프로그램에 대 한 연락처 레코드를 삭제 수 했습니다. 즉, 모든 데이터베이스 기반 웹 응용 프로그램에 필요한 기본 데이터베이스 작업은 수행할 수 있습니다.

그러나 응용 프로그램에 몇 가지 문제가 있습니다. 이를 원하는 대로 첫 번째와 I, 않아 응용 프로그램 가장 매력적인 응용 프로그램이 아닙니다. 몇 가지 디자인 작업을 해야합니다. 다음 반복에는 기본 뷰 마스터 페이지 및 응용 프로그램의 모양을 향상 시킬 연계 스타일 시트 변경할 수 있습니다 어떻게 살펴보겠습니다.

둘째, 폼 유효성 검사를 구현 하지 않았습니다. 예를 들어 없는 연락처 양식 만들기 폼 필드에 대해 값을 입력 하지 않고 제출 하는 것을 방지 하기 됩니다. 또한 잘못 된 전화 번호 및 전자 메일 주소를 입력할 수 있습니다. 반복 # 3에서에서 폼 유효성 검사 문제를 해결 하기 시작 합니다.

마지막으로, 가장 중요 한 점은 않아 응용 프로그램의 현재 반복 하거나 수 없습니다 쉽게 수정 유지 관리 합니다. 예를 들어 데이터베이스 액세스 논리 컨트롤러 작업에 오른쪽을 반영 됩니다. 이이 컨트롤러를 수정 하지 않고 데이터 액세스 코드를 수정할 수 없습니다 것을 의미 합니다. 이후 반복에서 연락처 관리자를 변경 하려면 복원 성도 뛰어납니다 확인 하기 위해 구현할 수 있습니다 하는 소프트웨어 디자인 패턴을 탐색 합니다.

> [!div class="step-by-step"]
> [이전](iteration-7-add-ajax-functionality-cs.md)
> [다음](iteration-2-make-the-application-look-nice-vb.md)
